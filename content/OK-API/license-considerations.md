# License considerations
We can relate to all developers who just want to publish their code, and not want to think about licensing or read any boring legal texts. In addition we wanted to document our thoughts and considerations around the chosen OK-API licenses, so any potential contributor can find and read them. This is why we have chosen to provide some background information about why we have chosen our licenses, which questions we asked and what goals we wanted to achieve.  
Enjoy this wall of text around our considerations about a matching open source license for the OK-API.

- [License considerations](#license-considerations)
  - [Why chosing a license](#why-chosing-a-license)
  - [Questions we asked ourselves](#questions-we-asked-ourselves)
  - [OK-API license goals](#ok-api-license-goals)
  - [Chosing the license type](#chosing-the-license-type)
  - [What about the applicable law?](#what-about-the-applicable-law)
  - [What the EUPL 1.2 provides](#what-the-eupl-12-provides)

## Why chosing a license
We can relate to all developers who just want to publish their code, and not want to think about licensing or read any boring legal texts. This is why we have chosen to provide some background information about why we have chosen this
As soon as you write one line of code, you create content under the copyright law. If you want it or not, these laws apply. When publishing it without any license, everyone downloading it needs an individual permission from the copyright owner, or it will be a copyright violation by law (even though the copyright owner choses to not enforce it). A software published without license is not free, even if everyone can download it.  
Chosing a license under which the content is provided, gives a (more or less) clear definition of the rights and obligations of the users, owners and contributors.

We have chosen to provide our projects under the __EUPL (European Union Public License) 1.2__ license. Following are our considerations why this license fits our goals and projects.


## Questions we asked ourselves
- Which license are in use for third party software that we are going to use in our first programs? Are there dependencies that limit us in the choice of our license?
- What are the terms and condition of the platform that we want to host our content on? (e.g. the Github terms require that every software that is hosted there, must allow the creation of copies, derivatives and changed versions.)
- Do we want to enforce that derivatives, extensions and distributions must use the same license that we use?
- Shall we allow third parties to use our content in their own proprietary software? If yes under which conditions?

## OK-API license goals
Based on these first few questions we came to define the goals we want to reach. There are several goals that we want to reach and that must be backed by the license that we chose:
- Our software shall be free to be used by everyone who wants to.
- As this is a non-profit initiative of private people, no contributor can give any liability or warranty for the content provided. Our contributors must be protected against any claims.
- The license shall provide a protection against patent trolling (even if it is unlikely to happen in our case).
- The license shall protect the authorship and copyrights of our contributors.
- If we ever create a trademark, it should be covered/mentioned by the license, and not left unclarified.
- We want to support the free open source software community by:
-- explicitly provide rights for the usage of our content by everyone
-- explicitly prevent our code to become closed source code ever again. Free software must remain free.

## Chosing the license type
There is a large spectrum of open source licenses available ready to use. All open source licenses make the content available to be used by everyone. This is the core idea of FOSS licenses. So why all these different licenses, which are made for a various set of scenarios? Remember ... usage of the content is already free as it is FOSS. There basically are two major areas they are regulating in different ways:

1. The freedom of other developers of doing what they want with the content. Copy, combine, configure, distribute, remix, etc.
2. The freedom of the content (the software) itself, so the existing software and all its future derivatives remain freely available to everyone (and maybe grant the same rights to their users).

These two main areas are in conflict which each other. For example, if a license forbids the content, and following developments based on it, to be put under a proprietary closed source license ever again, this takes away the freedom to do this from the developers. If a license states that all derivatives and even code that uses the given software must be published under the same license, this takes away freedom to do so from the developers.  
If a license just regulates the warranty and liability exclusion of contributers and allows the developers to do want they want with the content, this allows everyone to put the content in their own creation and put it in a closed source license, which takes away the freedom of the software and the freedom of the users to use it.  
So there are tradeoffs to be made.

Basically all open source licenses can be separated in the following three types:
- Permissive licenses (e.g. MIT, DWTFYW, BSD, Apache License)
  - Maximum freedom to developers, even the freedom to take the freedom of the software away again.
- Weak copyleft licenses (Eclipse License, Mozilla License 2.0, EUPL 1.2, LGPL)
  - Medium freedom of the software, medium freedom of the developers and their work based on it. The software and all derivatives, changed versions etc. must be published under a 'compatible' open source license. The developers are free to chose from the 'compatible' license. Some weak copyleft licenses allow the software to be used and distributed together with closed source components (as long as the open sourced software remains open source and is published.).
- Strong copyleft licenses (GPLv2, GPLv3, AGPL)
  - Maximum freedom of the software and all works based on it, which must be open sourced as well, to the expense of the freedom of the developers to freely chose licenses and permissions as they please for their own work. Strong copyleft licenses enforce the spread of open source licenses to other software projects, if they want to use the open source software under strong copyleft.

Mapping these against our initial goals and questions, we quickly came to the point that a weak copyleft license fits our projects the best.

## What about the applicable law?
Keep in mind, that an open source license is a contract under copyright law, between the copyright owner(s) and the users/distributors of the content.
The overwhelming majority of open source licenses has some private non government organisation as license steward. They decide about how the license will change (with the next revised version) and answer questions regaring 'their' license (e.g. the Mozilla Foundation, Apache Foundation, Free Software Foundation, etc.). These organisations have no mandate to do any jurisdiction. This is being left up to courts and the local laws of the countries. Considering that software is being published globally, and the world is a diverse place with a plethora of different legal systems, it becomes clear that there is no 'real' definitive arbitrator who is responsible in every case. If a judge in some country decides that parts of the chosen license are invalid in their jurisdiction, you cannot do much about it from out of another country.
Mozilla even removed a section about the jurisdiction to be Santa Clara U.S.A. where any claims shall be handled, when going from v1.1 to v2.0 in order to drive worldwide acceptance and adoption of the license. v2.0 only refers to "the applicaple" law of "a jurisdiction where the defendant maintains its principal place of business". One can argue if this made it better or worse to legally apply this license.  
This can be an issue if you want a certain legal philosophy to apply to your license and give certainty to everyone about which courts and legal systems are responsible for judging in case of any conflict.  
To make things a bit more complicated, when working together internationally, nearly all licenses state that the only legal binding language for the license is the english version, even though there might be translations. As licenses are a legal document, it might be hard for non native speakers to understand these documents, and if they use a translation it is not worth anything in case of a legal conflict.

## What the EUPL 1.2 provides
All in all the "European Union Public License 1.2" turned out to be the perfect match for our license requirements, and we decided to publish all our code projects under this license.

https://eupl.eu/
https://joinup.ec.europa.eu/collection/eupl/how-use-eupl

Considering our goals, and the different license types, and what we learned about the legal background of licenses, we decided to use the EUPL (European Union Public License) 1.2 (only) for a number of good reasons.
Following are the main reasons for us:

- It is the only license which is not backed by a private organisation, but by the European Union as a legal entity, backed by the European Comission. This makes it the only international license that is given by an entity which has the democratic mandate and authority to enforce it. This gives a good level of security for our contributors regarding the question of competence and responsibilities in case of any conflict. 
- The license is avaible in 23(!!!) different languages, and all translations are legally equivalent. That means you can read the french version in your native language, while someone else reads it in english, and both have the security that they are reading a document that is legally binding and valid in front of a court. This is absolutely unique in the world of open source licenses, and one of the wonderful side effects of having so many different countries and languages in the EU. Having so many equivalent translations supports international collaboration, as it makes it easier for people to contribute and understand the license.
- The license is a 'weak copyleft' license, which allows developers to take the code and change it or integrate it in their own programs, as long as they publish these derivatives (or work based on the original) under the EUPL or any 'compatible' license, which is the 'copyleft effect' of the EUPL, which makes sure the software remains open source. As many other licenses only have a very limited set of 'compatible' licenses, the EUPL 1.2 has a broad set ot compatible licenses, which are defined in the appendix. This includes all relevant weak copyleft licenses as well as strong copyleft licenses. Only the distribution under permissive licenses is not allowed. This is a good mixture between ensuring the freedom of the software as well as giving developers a lot of freedom to use, change and distribute the software and their work based on it, even under a different license. In addition it allows to be combined and shipped together with closed source components, as long as the EUPL software part remains open source. It has no 'viral copyleft' effect, which enforces that every component of the combined software is open sourced as well.
-  In case of any legal conflict, the jursidiction of the place of living of the author / owner of the software is responsible. If the owner is living in the EU, this can be any country. As the EUPL is based on the European Union, it is compatible to the copyright laws in every member of the union. If the owner is living outside of the European Union, there is still the local court in his/her country responsible, but the law under which the conflict must be judged is the belgian law. This sounds weird at first glance, but it makes sure there is no misunderstanding about the legal framework and jurisdiction. The chosen legal systems and philosophies which are backing the EUPL are the ones we as the authors can get behind and support. It provides security to all contributors and leaves no 'legal grey area'.  We consider this to be a big advantage compared to other open source licenses, which leave this question totally open and provide no real clarification about which philosophy of law applies.
-  The EUPL does not allow the use of any trademarks, signs or protected names of the owners of the work, which is ok for us. We are here to provide software not nice logos. And if we provide nice logos, they should remain with OK-API :-)
-  It protects against patent trolling. The Licensor grants to the Licensee royalty-free, non-exclusive usage rights to any patents held by the Licensor, to the extent necessary to make use of the rights granted on the Work under this Licence. This effectively makes it impossible for license trolls to 'inject' their code / design / process into our  software by contributing, and then claiming any patent violation. In addition software itself is not subject to patents in the European Union, which makes it even harder for patent trolls.
-  The EUPL protects contributors from warranty claims and limits by excluding any warranty by stating the work is provided 'as-is', and making clear that this is an essential part of the license
-  It provides limited liability. All Licensors will in no event be liable for any direct or indirect, material or moral, damages of any kind, arising out of the License or of the use of the work, including without limitation, damages for loss of goodwill, work stoppage, computer failure or malfunction, loss of data or any commercial damage, even if the Licensor has been advised of the possibility of such damage ... except in the case of wilful misconduct or damages directly caused to natural persons. Also the Licensor will be liable under statuary product liability laws, as far as they apply.  
This is absolutely O.K. for us, because of the following reasons:  
A lot of open source licenses exclude EVERY liability, but having a closer look at these clauses it becomes clear, that they do not keep up at court.  
In the European Union (and many countries outside) you cannot exclude liability for wilful misconduct or direct damages to people. You are not allowed to write a software that (somehow) physically harms people and claim that you are not liable for it (crazy idea, right?). Also the application of product liability laws is O.K. for us. As we do not provide a 'product', as defined in the law, but simply publish software, they do not apply in our case. Product liability would apply for someone who bundles our software, builds a derivative, and ships it to his customers who pay e.g. for support of the software. Just open sourcing code is not "providing a product". 
