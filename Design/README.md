# Designing for Software Security Engineering

Threat Model Report: [Level 1](http://htmlpreview.github.io/?https://github.com/team-assure/Semester-Project/blob/master/Design/Level_1.htm)

### Observations

Of the 35 threats identified, xx are properly mitigated within the MISP system.  These include the following:
* 1 - Elevation Using Impersonation
* 2 - Spoofing the 1.0 MISP Apache Process Process
* 3 - Potential Lack of Input Validation for 1.0 MISP Apache Process
* 4 - Potential Data Repudiation by 1.0 MISP Apache Process
* 7 - Data Flow HTTP REST request Is Potentially Interrupted
* 8 - 1.0 MISP Apache Process May be Subject to Elevation of Privilege Using Remote Code Execution
* 9 - Elevation by Changing the Execution Flow in 1.0 MISP Apache Process
* 10 - Cross Site Request Forgery

There were xx threats that have the ability to be mitigated based on implementation decisions.  These occur as follows
* Apache configuration: Apache must be configured by the administrator at installation time.  MISP does recommend several security best practices during instalation, but it is up to the system administrator to research Apache configurations and ensure that the proper settings are configured for their environment.  The following vulnerabilities depend on proper Apache configurations.
  * 5 - Data Flow Sniffing
  * 6 - Potential Process Crash or Stop for 1.0 MISP Apache Process
* Firewall Configuration: 
  
Of the 35 threats identified, 35 are properly mitigated. A few threats need to be further investigated in the MISP implementation. One of these threats was regarding denial of service attacks on various threat properties of MISP.  One solution for this possible vulnerability at implementation time would be to ensure the appropriate firewall rules were in place to prevent denial of service.  When high volumes of traffic are identified, we will need to investigate if it is possible to rate limit the traffic, so that other connections may persist.  Another observation would be to require secure apache configuration to keep the certificate secured.  One of our threat properties was spoofing of emails external destination entity and to mitigate this, the software should require authentication.  Something else to investigate will be the possibility of sniffing the data flow to determine if all data is encrypted.  It is possible to leak some data in the MISP.extended_alert_subject, which allows you to have an extended subject, so the subject would not be encrypted. To mitigate, ensure that all data is encrypted.  Another area which we noticed deserved some attention was to make sure that there were no gaps in logging and that the appropriate information was being captured.

