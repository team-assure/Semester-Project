# Description
*What is it?, Contributors, Activity, Use, Popularity, Languages used, platform, documentation sources, etc.*

The [MISP Project](http://www.misp-project.org/) is an open source platform for sharing and analyzing malware.

# Licensing & Contributions
*Discuss License, procedures for making contributions, and contributor agreements*

The [MISP Project](http://www.misp-project.org/) is licensed using the GNU Affero General Public License v3.0, a copyleft license that is very similar to the GNU General Public License v3 with one additional requirement [1].  The GNU GPL v3 allows open source software to stay open source by permitting it to be used in subsequent projects but requiring that the source code of those subsequent works is made open source under the same terms set forward by the GNU GPL v3 license [2].  The GNU Affero General Public License v3.0 adheres to these same rules with the added requirement of publishing the source code when changes are made to the code and it is run on a server where users are allowed to connect to it.  This ensures that developers that take the code and modify it to run on their own servers are also required to share those changes with the community, ensuring that the software stay open source.

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
* https://nvd.nist.gov/vuln/detail/CVE-2017-13671 app/View/Helper/CommandHelper.php in MISP before 2.4.79 has persistent XSS via comments. It only impacts the users of the same instance because the comment field is not part of the MISP synchronisation.
* https://nvd.nist.gov/vuln/detail/CVE-2015-5721 Malware Information Sharing Platform (MISP) before 2.3.90 allows remote attackers to conduct PHP object injection attacks via crafted serialized data, related to TemplatesController.php and populate_event_from_template_attributes.ctp.
* Multiple cross-site scripting (XSS) vulnerabilities in the template-creation feature in Malware Information Sharing Platform (MISP) before 2.3.90 allow remote attackers to inject arbitrary web script or HTML via vectors involving (1) add.ctp, (2) edit.ctp, and (3) ajaxification.js.
* https://nvd.nist.gov/vuln/detail/CVE-2015-5719 app/Controller/TemplatesController.php in Malware Information Sharing Platform (MISP) before 2.3.92 does not properly restrict filenames under the tmp/files/ directory, which has unspecified impact and attack vectors.

## Functional Security requirements for the software
* Protect group private data from leaking to another's group data
* Only authorized users can modify other user's data

# Motivation
*Your motivation for selecting this project*
* manageable code base
* multi-user web environment provides many security requiremnts
* written in PHP which is readable and has many tools available to evaluate the code
* appears to have a strong user community

# References
[1] https://www.gnu.org/licenses/licenses.html#GPL
[2] https://choosealicense.com/licenses/gpl-3.0/
