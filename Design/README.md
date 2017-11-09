# Designing for Software Security Engineering

Threat Model Report: [Level 1](http://htmlpreview.github.io/?https://github.com/team-assure/Semester-Project/blob/master/Design/Level_1.htm)

### Observations

Of the 35 threats identified, 13 are properly mitigated within the MISP system.  These include the following:
* 1 - Elevation Using Impersonation
* 2 - Spoofing the 1.0 MISP Apache Process
* 3 - Potential Lack of Input Validation for 1.0 MISP Apache Process
* 4 - Potential Data Repudiation by 1.0 MISP Apache Process
* 7 - Data Flow HTTP REST request Is Potentially Interrupted
* 8 - MISP Apache Process May be Subject to Elevation of Privilege Using Remote Code Execution
* 9 - Elevation by Changing the Execution Flow in MISP Apache Process
* 10 - Cross Site Request Forgery
* 11 - Potential Data Repudiation by 1.0 MISP Apache Process
* 15 - MISP Apache Process May be Subject to Elevation of Privilege Using Remote Code Execution
* 16 - Elevation by Changing the Execution Flow in MISP Apache Process
* 17 - Cross Site Request Forgery
* 18 - Spoofing of the REST API Users External Destination Entity
* 19 - External Entity REST API Users Potentially Denies Receiving Data
* 20 - Data Flow HTTP REST response Is Potentially Interrupted
* 21 - Spoofing the 1.0 MISP Apache Process Process
* 23 - Data Store Denies MySQL database Potentially Writing Data
* 24 - Data Flow Sniffing
* 26 - Data Store Inaccessible
* 28 - Potential Data Repudiation by 1.0 MISP Apache Process
* 29 - Potential Process Crash or Stop for 1.0 MISP Apache Process
* 30 - Data Flow Generic Data Flow Is Potentially Interrupted
* 31 - Data Store Inaccessible
* 32 - 1.0 MISP Apache Process May be Subject to Elevation of Privilege Using Remote Code Execution
* 36 - Authenticated Data Flow Compromised
* 37 - Authenticated Data Flow Compromised

#### Threats requiring further investigation

There were 5 threats that have the ability to be mitigated based on configuration choices.  These occur as follows.
##### Apache configuration:
Apache must be configured by the administrator at installation time.  MISP does recommend several security best practices during installation, but it is up to the system administrator to research Apache configurations and ensure that the proper settings are configured for their environment.   This is needed for secure apache configuration to keep the certificate secured. The following vulnerabilities depend on proper Apache configurations.
  * 5 - Data Flow Sniffing
  * 6 - Potential Process Crash or Stop for MISP Apache Process
  * 12 - Data Flow Sniffing
  * 13 - Potential Process Crash or Stop for MISP Apache Process
  * 14 - Data Flow HTTP REST request Is Potentially Interrupted

##### Firewall Configuration:
One solution for this possible vulnerability at implementation time would be to ensure the appropriate firewall rules were in place to prevent denial of service.  When high volumes of traffic are identified, we will need to investigate if it is possible to rate limit the traffic, so that other connections may persist.  The following vulnerabilities can be mitigated by appropriate firewall configurations.
  * 7 - Data Flow HTTP REST request Is Potentially Interrupted
  * 14 - Data Flow HTTP REST response Is Potentially Interrupted
  * 21 - Data Flow Generic Data Flow Is Potentially Interrupted
  * 22 - Data Store Inaccessible
  * 27 - Data Flow SMTP Is Potentially Interrupted
  * 34 - Data Flow SQL query Is Potentially Interrupted
  * 35 - Data Store Inaccessible

##### SMTP Configuration
One of our threat properties was spoofing of emails external destination entity and to mitigate this, the software should require authentication.  Something else to investigate will be the possibility of sniffing the data flow to determine if all data is encrypted.  It is possible to leak some data in the MISP.extended_alert_subject, which allows you to have an extended subject, so the subject would not be encrypted. To mitigate, ensure that all data is encrypted.
  * 25 - Spoofing of the Email servers External Destination Entity
  * 33 - Data Flow Sniffing

### Reflections on contributing back to the MISP community
*  Helping to improve configuration documentation
*  Applying design patterns to identity ways
   * Move separate functions needing different privilege levels into mutually untrusting components
   * Reduce functionality and data exposed to an attacker if one of the mutually untrusting components is compromised
   * Reduce the amount of exposed code that runs with special/high privilege without affecting or limiting the functionality of the program
   * Run exposed system interfaces as limited privilege clients to high privilege system services with defined information requests only 

As we reflect on the project, a few things come to mind.  One addition that we would like to make to the community would be documentation.  Many things were not documented well.  Something else that is not addressed in the documentation or code was how the program handles an overload of requests.  It is not clear if there is a mechanism in place to rate limit excessive traffic or to just start dropping packets.  This could involve authentication attempts against the web UI or SQL calls to the database.  Nowhere is it discussed how it handles any type denial of service, whether it is accidental, self-inflicted, or malicious.  Lastly, the documentation was missing some of the vulnerabilities that the tool identified for MISP that could be fixed by ensuring that Apache, MySQL, and the email system were properly configured.  Something else we would like to add would be better database logging.  It would be good to know who made a SQL call and if it was returned.  The software does a fairly good job of logging, so putting in a request to the community to add logging in additional places may be helpful for the user base.
