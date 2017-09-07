# Description
*What is it?, Contributors, Activity, Use, Popularity, Languages used, platform, documentation sources, etc.*

# Contributions & Licensing
*Discuss License, procedures for making contributions, and contributor agreements*
* GNU Affero General Public License v3.0
  *requires stating changes
  *allows commercial use
  *give credit

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
