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
* Firewall Configuration: 
  * 6 - Potential Process Crash or Stop for 1.0 MISP Apache Process

There were xx threats where the MISP project appears to be vulnerable.  These are


A few threats need to be further investigated in the MISP implementation.  These are
