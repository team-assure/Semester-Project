# Code Review Strategy
To start our code review strategy, we first needed to decide what we needed to review.  To do this, it was important to first review our assurance cases.  This helped us think about what areas we were initially concerned about regarding the software. Then reviewing our mis-use cases and our threat models helped further define possible attack vectors or mis-configurations that may exist.  From this, it could be decided what areas of the code may need to be reviewed for weaknesses and vulnerabilities.  

In addition, our code review strategy involved performing static analysis of the code using a publically avaiable open source tool.  We used [RIPS](http://rips-scanner.sourceforge.net/) to perform static analysis.  This is a popular PHP static code analysis tool.  The RIPS tool produced extensive output.  As part of our strategy, we spot checked the results of the analysis for major issues and categorized all findings by CWE to identify where common issues are.  Due to the amount of output produced by the report, we did not attempt to verify every finding that the automated tool produced.

# Manual code review of critical security functions identified in mis-use cases and threat models
One assurance case was authentication.  So, one would want to do static analysis of code surrounding authentication to ensure that the application functions related to authentication and session management are implemented correctly.  Checking to see that user credentials are properly protected by hashing or encryption, confirming strong account management functions, no sessions ID’s are exposed in URL, session ID’s are not vulnerable to fixation attacks, and that they are not rotated after login.  

Another assurance cases was access control.  Again, a review of the code to verify that restrictions are in place for what authenticated users are allowed to do.  For data references, does the application use a reference map or an access control check to ensure the user is authorized.  For function requests, does the application make sure that the user is authenticated and has the proper roles for that function.  A code review can verify if this has been implemented correctly and manual testing can be done to identify access control flaws.

A third assurance case applied to protecting against common web attacks, including cross-site scripting.  Here we would want to review the code to see if it uses user supplied input as part of the HTML output or to make sure the attacker controllable data cannot be added to a web page.  This could be done with automatic tools fairly effectively.


# Summary of key findings from manual code analysis. 

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
* Review - RIPS found 260 issues from it's scan.
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
      * Cross-Site Scripting (28)
	* [CWE-93: Improper Neutralization of CRLF Sequences](https://cwe.mitre.org/data/definitions/93.html)
      * HTTP Response Splitting (3)
	* [CWE-470: Use of Externally-Controlled Input to Select Classes or Code](https://cwe.mitre.org/data/definitions/470.html)
	    * Reflection Injection (12)
