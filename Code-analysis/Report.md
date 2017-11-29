# Code Review Strategy
To start our code review strategy, we first needed to decide what we needed to review.  To do this, it was important to first review our assurance cases.  This helped us think about what areas we were initially concerned about regarding the software. Then reviewing our mis-use cases and our threat models helped further define possible attack vectors or mis-configurations that may exist.  From this, it could be decided what areas of the code may need to be reviewed for weaknesses and vulnerabilities.  

For example, one assurance case was authentication.  So, one would want to do static analysis of code surrounding authentication to ensure that the application functions related to authentication and session management are implemented correctly.  Checking to see that user credentials are properly protected by hashing or encryption, confirming strong account management functions, no sessions ID’s are exposed in URL, session ID’s are not vulnerable to fixation attacks, and that they are not rotated after login.  

Another example from our assurance cases was access control.  Again, a review of the code to verify that restrictions are in place for what authenticated users are allowed to do.  For data references, does the application use a reference map or an access control check to ensure the user is authorized.  For function requests, does the application make sure that the user is authenticated and has the proper roles for that function.  A code review can verify if this has been implemented correctly and manual testing can be done to identify access control flaws.

A last example from our assurance cases would be from our common attacks case, which dealt with cross-site scripting.  Here we would want to review the code to see if it uses user supplied input as part of the HTML output or to make sure the attacker controllable data cannot be added to a web page.  This could be done with automatic tools fairly effectively.

# Manual code review of critical security functions identified in mis-use cases and threat models

# Automated tools (include links)

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
* Suggested fixes

# Summary of key findings from manual and/or automated scanning. This may include: Categorization, Mappings to CWEs, CAPECs, Risk Levels etc
* Authentication and session management
    * CWE-287: Improper Authentication
    * CWE-384: Session Fixation
* Access Control
    * CWE-285: Improper Authorization
    * CWE-639: Authorization Bypass Through User-Controlled Key
    * CWE-22: Improper Limitation of a Pathname to a Restricted Directory ('Path Traversal')
* Common Attacks (Cross-site scripting)
    * CWE-79: Improper Neutralization of Input During Web Page Generation ('Cross-site Scripting')

# Links to any pull requests, issues, discussion, etc. from the team to the original project and any follow-up interactions
