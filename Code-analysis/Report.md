# Code Review Strategy
To start our code review strategy, we first needed to decide what we needed to review.  To do this, it was important to first review our assurance cases.  This helped us think about what areas we were initially concerned about regarding the software. Then reviewing our mis-use cases and our threat models helped further define possible attack vectors or mis-configurations that may exist.  A review of recently reported vulnerabilities in the NIST database revealed a high frequency of cross-site scripting vulnerabilities being reported relative to other vulnerability categories:  [CVE-2017-16802](https://nvd.nist.gov/vuln/detail/CVE-2017-16802)-reported November 13, 2017;  [CVE-2017-15216](https://nvd.nist.gov/vuln/detail/CVE-2017-15216)-reported October 10, 2017;  [CVE-2017-13671](https://nvd.nist.gov/vuln/detail/CVE-2017-13671)-reported August 24, 2017;  [CVE-2017-7215](https://nvd.nist.gov/vuln/detail/CVE-2017-7215)-reported March 21, 2017.  These recent vulnerabilities weighed heavily in our analysis.   Using these analysis factors, the areas of the code and categories of weaknesses and vulnerabilities to be reviewed were decided and prioritized.   

In addition, our code review strategy involved performing static analysis of the code using a publically available open source tool.  We used [RIPS](http://rips-scanner.sourceforge.net/) to perform static analysis, a popular PHP static code analysis tool linked from the OWASP website.  The RIPS tool produced extensive output.  Due to the history of cross-site scripting vulnerabilities within MISP, we investigated several cross-site scripting-specific findings from the RIPS report and categorized the remaining findings by CWE to identify where other common issues may lie.  Due to the amount of output produced by the report, we did not attempt to verify every finding that the automated tool produced.

# Manual code review of critical security functions identified in mis-use cases and threat models
One assurance case was authentication.  So, one would want to do static analysis of code surrounding authentication to ensure that the application functions related to authentication and session management are implemented correctly.  Checking to see that user credentials are properly protected by hashing or encryption, confirming strong account management functions, no sessions ID’s are exposed in URL, session ID’s are not vulnerable to fixation attacks, and that they are not rotated after login are essential.  In addition, we would check that permissions are checked on the server-side so that one user cannot impersonate a higher-privileged user.  This does appear to be the case in the MISP application.  

Another assurance cases was access control.  Again, a review of the code to verify that restrictions are in place for what authenticated users are allowed to do.  For data references, the application should use a reference map or an access control check to ensure the user is authorized.  For function requests, the application should make sure that the user is authenticated and has the proper roles for that function.  A code review can verify if this has been implemented correctly and manual testing can be done to identify access control flaws.

A third assurance case applied to protecting against common web attacks, including cross-site scripting.  Here we would want to review the code to see if it uses user supplied input as part of the HTML output or to make sure the attacker controllable data cannot be added to a web page.  This could be done with automatic tools fairly effectively, but can also be reviewed manually.

# Automated Code Review Analysis
Focusing on the cross-site scripting vulnerabilities, since the system has a history of these issues, we investigated some of the findings in more detail.

In the [app/View/Helper/XmlOutputHelper.php](https://github.com/MISP/MISP/blob/2.4/app/View/Helper/XmlOutputHelper.php) file, there is a possibility for cross-site scripting since the code echos items in an array to php code.  Further investigation would need to be done to confirm that all locations where this function is called properly escapes user-inputed code.  This was not performed due to the size of the code base.

In the [/app/Console/Command/PasswordShell.php](https://github.com/MISP/MISP/blob/2.4/app/Console/Command/PasswordShell.php) file, the RIPS scanner identified Cross-Site Scripting findings that, upon further review, appear to be false postiives.  The findings identified in this file check user input to see if a password is provided, but does not do anything with the input that could cause the input to be stored or executed as is required in a XSS attack.

# Summary of key findings from manual code analysis.
Based on the possible issues discovered during manual code review, we identified the following CWE's that map to these items.

* Authentication and session management
    * [CWE-287: Improper Authentication](https://cwe.mitre.org/data/definitions/287.html)
    * [CWE-384: Session Fixation](https://cwe.mitre.org/data/definitions/384.html)
* Access Control
    * [CWE-285: Improper Authorization](https://cwe.mitre.org/data/definitions/285.html)
    * [CWE-639: Authorization Bypass Through User-Controlled Key](https://cwe.mitre.org/data/definitions/639.html)
    * [CWE-22: Improper Limitation of a Pathname to a Restricted Directory ('Path Traversal')](https://cwe.mitre.org/data/definitions/22.html)
* Common Web Attacks
    * [CWE-79: Improper Neutralization of Input During Web Page Generation ('Cross-site Scripting')](https://cwe.mitre.org/data/definitions/79.html)
    * [CWE-89: Improper Neutralization of Special Elements used in an SQL Command ('SQL Injection')](https://cwe.mitre.org/data/definitions/89.html)
    * [CWE-611: Improper Restriction of XML External Entity Reference ('XXE')](https://cwe.mitre.org/data/definitions/611.html)
    * [CWE-77: Improper Neutralization of Special Elements used in a Command ('Command Injection')](https://cwe.mitre.org/data/definitions/77.html)

# Summary of key finding from automated code analysis.
[Link to RIPS Report](https://github.com/team-assure/Semester-Project/raw/master/Code-analysis/RIPS%20Report.pdf)
* Goals - The goals of our automated tool review was to confirm the veracity of our threat models and determine whether they were affirmed or not.  We utilized [RIPS](http://rips-scanner.sourceforge.net/) to process our static analysis.  While an older version of the program, we found it through a referral from the [OWASP - Security Analysis Tools](https://www.owasp.org/index.php/Source_Code_Analysis_Tools) website.
* Tool execution - the tool is a web based application which scans the selected project for a number of weaknesses.
* Review - RIPS found 260 issues from it's scan.  28 were Cross-Site Scripting findings, which were investigated more fully in the analysis section.  Beyond that, further investigation needs to be done to see if the system has an issue with File and DIrectory Information Exposure or File Exclusions since those are the next two most common issues.
     * Cross-Site Scripting (28)
        * [CWE-93: Improper Neutralization of CRLF Sequences](https://cwe.mitre.org/data/definitions/93.html)
    * [CWE-538: File and Directory Information Exposure](https://cwe.mitre.org/data/definitions/538.html)
        * File Disclosures (101)
        * File Manipulation (40)
	* [CWE-73: External Control of File Name or Path](https://cwe.mitre.org/data/definitions/73.html)
      * File Inclusion (14)
	* [CWE-78: Improper Neutralization of Special Elements used in an OS Command](https://cwe.mitre.org/data/definitions/78.html)
	    * Command Execution (34)
	* [CWE-94: Improper Control of Generation of Code](https://cwe.mitre.org/data/definitions/94.html)
      * Code Execution (29)
      * Possible Flow Control (15)
	* [CWE-88: Argument Injection or Modification](https://cwe.mitre.org/data/definitions/88.html)
      * Protocol Injection (3)
	* [CWE-90: Improper Neutralization of Special Elements used in an LDAP Query](https://cwe.mitre.org/data/definitions/90.html)
      * LDAP Injection (1)
	* [CWE-79: Improper Neutralization of Input During Web Page Generation](https://cwe.mitre.org/data/definitions/79.html)
      * HTTP Response Splitting (3)
	* [CWE-470: Use of Externally-Controlled Input to Select Classes or Code](https://cwe.mitre.org/data/definitions/470.html)
	    * Reflection Injection (12)
