Table of contents:
- [Script: multi-backup-ctrl.sh](#script-multi-backup-ctrlsh)
  - [Setup](#setup)
  - [Why is this script necessary? When is it useful?](#why-is-this-script-necessary-when-is-it-useful)
  - [Scenario for this script](#scenario-for-this-script)
    - [Ensuring regular backup execution](#ensuring-regular-backup-execution)
    - [Given backup order](#given-backup-order)
    - [Notification only in case of an error](#notification-only-in-case-of-an-error)
  - [Logging](#logging)
  - [Logic Program Flow Sequence](#logic-program-flow-sequence)
  - [Usage](#usage)

# Script: multi-backup-ctrl.sh
This script is built to control the sync of multiple source directories to multiple target directories. The correlation, which source directory shall be synced to which target directory, is provided using an input file. The script is built to keep track of when the last sync job was executed, to make sure there are at least 24 hrs between the last sync and the actual one.  
The following example shows a system with 4 disks of different size, which contain different directories that shall be backed up to different disks. 
This example can be considered typical for a NAS server that has been updated with additional disks of different capacity over time.
![4disk-scenario](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.github.com/OK-API/Documentation/master/images/Manage-My-Server/plantuml/mbc-4disk-scenario.puml)

## Setup
_Prereq:_ The source and target directories must be mounted first. Mounting disks or paths is not in the scope of this script.

1. Copy the script to your server in your preferred directory, either using `git clone` or just copying it using wget:
 `wget https://raw.githubusercontent.com/OK-API/Manage-My-Server/master/multi-backup-ctrl.sh`

2. Place one or more input files at your preferred location. Every line in this file must contain the source directory first, followed by the target directory, both separated by a blank. Using directories with blanks in their name is not tested yet.  
\
    Input file example:
    ```
    /mnt/d/doBackupSource/subdir1 /mnt/f/doBackupTarget/
    /mnt/d/doBackupSource/subdir2 /mnt/f/doBackupTarget/foodir/
    ```

3. Configure a cron job for regular execution or run the script manually. By using multiple input files for multiple calls you can realize more complex sync scenarios. 
The script is built and tested for execution with `sudo` or `root` permission, as it is assumed that the source and target directories for the backups, as well as the logging directories, have different permissions. If you do not want to use `sudo` or `root`, you must make sure that all permissions match the user used to execute the script.  


|:warning: ATTENTION: The script uses the file `/var/log/multiBackupLog/trackingfile` to keep track of its last execution time, and make sure there are at least 24 hrs between the last sync run and the actual one. It uses the modify date of the file for this. If you want to execute it more regularly make sure to remove or modify the trackingfile first. This feature exists to support environments which are not up and running 24/7 and need to handle their backup syncs locally and asynchronously.|
| --- |

## Why is this script necessary? When is it useful?
A lot of NAS software offers to configure backup jobs in their software, which are often rsync based. You can provide an execution time (mostly implemented by cron jobs) and what share/folder shall be synced to which target device, locally or remote. But most of these approaches only work if certain assumptions are made:
- The system runs 24/7
- The disk setup is symetrical with an even number of disks of the same size
- The backup configuration is being applied in all cases
- There is no specific "order" in which the backups shall be taken (e.g. important folders first, less important last.)
- There are not many different source and target disks
- Notification is either sent always after job execution (which leads to loads of notifications)  
  
This leads to several weaknesses in these backup approaches:
- If the NAS does not run 24/7, several backup jobs might not be executed, as cron does not re-run missed jobs if it was shutdown during the scheduled time.
- If you are running into issues with some jobs (e.g. full disks), it might be that unimportant data has been backed up, while there is no more space left for your important data, as some NAS systems do not support a "backup order".
- You cannot implement a Scenario in which you have "at least X hours" between the last successful backup run, and the next one, as cron does not support this. In addition you want to make a backup soon, after your system is back available again.
- When having multiple backup jobs configured and standard notifications apply, one will get a lot of messages just to inform you "everything is ok". A lot of systems just send all output (if existant) or nothing. Just sending output when there has been error, and not notifying you about "successful" runs, is not part of most systems.
  
## Scenario for this script
The scenario for this script has multiple characteristics:
### Ensuring regular backup execution
Have one backup job that can run regularly, e.g. every hour, making sure to perform a backup only once in 24 hrs, as you want a real asynchronous backup. It can backup multiple source directories in a given order to a defined set of target directories. All directories can be on different disks, as they are mounted as a prereq. If the server has been shutdown for a while, and is being restarted, a regular job can run this script, and it will still make sure to have at least 24 hrs between the last successful backup and the next. As the job schedules can be quiet regular (hourly, 2 hourly, etc.) it can make sure to not "miss" the one backup time that can be configured in most NAS software, as described above.  
Regular NAS example:
- A backup job is configured for 11 PM daily
- The system is shutdown during 11 PM (e.g. for power saving)
- No backup will be performed that day. This can happen multiple days in a row.
  
Multi-backup-ctrl example:
- A job is configured to run the script hourly
- The system is shutdown for a while
- When the system is running again, it lasts a maximum of an hour for the script to check if the last backup is longer ago than 1 day, and run the setup.
### Given backup order
By being able to put multiple source and target entries to be backed up in order the script makes sure to only start the next part of the backup when the first one is finished. This prevents the overlap of backups, which can happen if multiple backup jobs are scheduled independently from each other.
In addition the order of source-target combinations can be used to make sure to backup your important data first, and the less important later.
### Notification only in case of an error
In case of using this software with OpenMediavault (or similar systems), the regular execution of can be scheduled as an automated job in OpenMediavault. OMV provides the option to send a notification if there is any output present by the command. By calling the script with the `-s` parameter you can make sure to only produce stdout/stderr output when there is an error. All info and debug level output will still be written to the log files, but it will not provide any output, and thus no notification. This way you can make sure to only get a message in case things went wrong, and reduce the amount of "Everything-is-Ok!" spam in your inbox. This behaviour is imitating the alerting of monitoring systems, which only send an alert if things are leaving the specified parameters or hit certain thresholds.

## Logging
By default all logs are written to log files in the folder `/var/log/multiBackupLog`.
The file `executionLog.log` contains logs about the script run itself, like logs about input parameter parsing, sanity checks of input files, etc.
The file `backup.log` contains the logs about the sync itself. It contains information about the start and end of the sync as well as the complete rsync output.

The two log files have been separated, in order to provide a better overview about the times this script has been run and not clutter it with all the detailed rsync output.

## Logic Program Flow Sequence

![program-flow](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.github.com/OK-API/Documentation/master/images/Manage-My-Server/plantuml/mbc-program-flow.puml)



## Usage
```
Usage: multi-backup-ctrl.sh [OPTIONS]

This script is built to perform a backup of one or more source directories to one or more target directories. It is designed to be run in a NAS System which has multiple backup disks which can be mounted in different paths.
Even though it might run on a large variety of Server systems, it was made for being used with 'openmediavault'.
The configuration which source directory shall be backed up to which target directory is being read from a separate config file.
The script is built to be either executed with sudo or root permissions.

Syntax: multi-backup-ctrl.sh -p|--path file_path [-t|--test] [-h|--help] [-s|--silent]

Options:
-p|--path     Mandatory parameter. Specifies the path of the config file which contains the source and target folders for the backup.
-t|--test     Sets the test flag, which makes the script run without really performing the rsync backup.
-h|--help     Print this Help.
-s|--silent   Sets the 'silent' flag, which prevents the output of DEBUG and INFO level logs to stdout. It will only be logged to the log file. ERROR level will still be logged to stdout and file."

Example usage: ./multi-backup-ctrl.sh -p /tmp/myInputFile.txt
Example usage: ./multi-backup-ctrl.sh -p /tmp/myInputFile.txt -s
Example usage: ./multi-backup-ctrl.sh -p /tmp/myInputFile.txt -t 

The input file must contain a pair of source directory and target directory in each line, separated by a blank.
The required format is: '<sourceDir> <targetDir>'

Example input file:
/mnt/d/doBackupSource/subdir1 /mnt/f/doBackupTarget/
/mnt/d/doBackupSource/subdir2 /mnt/f/doBackupTarget/foodir/

Exit codes:
0         if execution successful.
1         if preparation fails, which can be malformed input or problems with logging environment.
2         if the rsync based backup itself failed for some reason.
```
