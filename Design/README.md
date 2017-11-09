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

##### SMTP Configuration
One of our threat properties was spoofing of emails external destination entity and to mitigate this, the software should require authentication.  Something else to investigate will be the possibility of sniffing the data flow to determine if all data is encrypted.  It is possible to leak some data in the MISP.extended_alert_subject, which allows you to have an extended subject, so the subject would not be encrypted. To mitigate, ensure that all data is encrypted.
  * 25 - Spoofing of the Email servers External Destination Entity
  * 33 - Data Flow Sniffing 


A few threats need to be further investigated in the MISP implementation. One of these threats was regarding denial of service attacks on various threat properties of MISP.       Another area which we noticed deserved some attention was to make sure that there were no gaps in logging and that the appropriate information was being captured.
