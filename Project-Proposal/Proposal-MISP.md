# Description
*What is it?, Contributors, Activity, Use, Popularity, Languages used, platform, documentation sources, etc.*

# Contributions & Licensing
*Discuss License, procedures for making contributions, and contributor agreements*
* GNU Affero General Public License v3.0
  * requires stating changes
  * allows commercial use
  * give credit
* Contribute by identifying bug, issue, or new feature
  * include as much info as possible including version, screenshots, and steps to reproduce the issue
  * welcomes interacting with existing issues to see what is the top priority
* When reporting security vulnerabilities, report directly to CIRCL or encrypt the message with their PGP key
  * willing to acknowledge contributors who identify security vulnerabilities
* Roadmap and future features is largely determined by user community
* Steps
  * Branch from core project
  * commit with meaningful commit message
  * generate a changelog
  * open a pull request
  * prefer small, gradual changes
  * if documentation needs to be updated, should make commit to misp-book as well
  * include as much detail in the commit message as possible
  * don't commit sensitive information

# Security
## Security related history (E.g. known vulnerabilities), 
* Malware Information Sharing Platform (MISP) before 2.3.90 allows remote attackers to conduct PHP object injection attacks via crafted serialized data, related to TemplatesController.php and populate_event_from_template_attributes.ctp.
* Multiple cross-site scripting (XSS) vulnerabilities in the template-creation feature in Malware Information Sharing Platform (MISP) before 2.3.90 allow remote attackers to inject arbitrary web script or HTML via vectors involving (1) add.ctp, (2) edit.ctp, and (3) ajaxification.js.
* app/Controller/TemplatesController.php in Malware Information Sharing Platform (MISP) before 2.3.92 does not properly restrict filenames under the tmp/files/ directory, which has unspecified impact and attack vectors.

Functional Security requirements for the software*

# Motivation
*Your motivation for selecting this project*
* manageable code base
* multi-user web environment provides many security requiremnts
* written in PHP which is readable and has many tools available to evaluate the code
* appears to have a strong user community
