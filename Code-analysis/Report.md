# Code Review Strategy
To start our code review strategy, we first needed to decide what we needed to review.  To do this, it was important to first review our assurance cases.  This helped us think about what areas we were initially concerned about regarding the software. Then reviewing our mis-use cases and our threat models help further define possible attack vectors or miss configurations that may exist.  From this, it could be decided what needed to be reviewed.  For example, one assurance case was authentication.  So, one would want to do static analysis of code surrounding authentication to ensure that the application functions related to authentication and session management are implemented correctly.  Checking to see that user credentials are properly protected by hashing or encryption, confirming strong account management functions, no sessions ID’s are exposed in URL, session ID’s are not vulnerable to fixation attacks, and that they are not rotated after login.  
Another example for our assurance cases was access control.  Again, a review of the code to verify that restrictions are in place for what authenticated users are allowed to do.  For data references, does the application use a reference map or do an access control check to ensure the user is authorized.  For function requests, does the application make sure that the user is authenticated and has the proper roles for that function.  A code review can verify if this has been implemented correctly and manual testing can be done to identify access control flaws.
A last example from our assurance cases would be within our common attacks case, which dealt with cross-site scripting.  Here we would want to review the code to see if it uses user supplied input as part of the HTML output or to make sure the attacker controllable data cannot be added to a web page.  This could be done with automatic tools fairly effectively.


# Manual code review of critical security functions identified in mis-use cases and threat models
# Automated code scanning (if available). Include links to full reports
# Summary of key findings from manual and/or automated scanning. This may include: Categorization, Mappings to CWEs, CAPECs, Risk Levels etc
# Authentication and session management
* CWE-287: Improper Authentication
* CWE-384: Session Fixation
# Access Control
* CWE-285: Improper Authorization
* CWE-639: Authorization Bypass Through User-Controlled Key
* CWE-22: Improper Limitation of a Pathname to a Restricted Directory ('Path Traversal')
# Common Attacks (Cross-site scripting)
* CWE-79: Improper Neutralization of Input During Web Page Generation ('Cross-site Scripting')

# Links to any pull requests, issues, discussion, etc. from the team to the original project and any follow-up interactions
