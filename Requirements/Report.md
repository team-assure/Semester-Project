## Security requirements based on assurance claims

### Assurance Claims
The final assurance claims for the MISP project are as follows:
  1. System prevents distribution of event information to those who are not permitted to view it.
  
  2. Role based access is implemented in an acceptably secure manner.
  
  3. The system's authentication mechanism is acceptably secure against common authentication attacks.
  
  4. There are no exploitable Cross-Site Scripting weaknesses in the code.
  
  5. The user management interface is acceptably secure.

### Security requirements for the project

  1. Data Leakage
         
     Description: The system has a method for defining which individuals and groups, if any, will receive a submitted event.  The administrators are responsible for assigning the users to the appropriate groups.  However, users are able to create sharing groups to facilitate the sharing of events, if they are assigned that permission.  Depending on how the group is configured determines if and how they are able to access the event information.
 
     Link: [Data Leakage](https://www.lucidchart.com/invitations/accept/1518de8f-6cbb-4010-923b-a17f04cffb25)

  2. Access Control
  
     Description: Security requirements around access control should consider the restrictions placed on authenticated users.  Done properly, this will prevent attackers from accessing unauthorized functionality or data.  Functionality references should require that the user is authenticated and that the user has the proper roles or privileges to use that function.  Data references should require that the user is authorized by using a reference map or access control check.
 
     Link: [Access Control](https://www.lucidchart.com/invitations/accept/1518de8f-6cbb-4010-923b-a17f04cffb25)

  3. Authentication
  
     Description: The system has a security requirement to ensure that the authentication mechanism properly protects access to sensitive data.  Authentication centers around the login mechanism, but additional requirements exist around this login to ensure it is adequate.  THe login mechanism has a requirement to operate securely in the face of a variety of attacks, including Insufficient authentication, weak password recovery, and brute force attacks.  This can be accomplished by adding additional requirements to the login mechanism, including ensuring that login attempts are limited and that authentication and authorization is checked with every attempt to access data.  Requirements for other processes that may affect the security of the login include having adequate help desk processes to verify the identity of callers when they wish to change their passwords to protect against weak password recovery attacks.
     
     Link: [Authentication](https://www.lucidchart.com/invitations/accept/1518de8f-6cbb-4010-923b-a17f04cffb25)

  4. Common Attacks
     
     Description:  The system has a security requirement to secure the sensitive data it stores in the face of any common web application attack, including XSS, SQL injection, etc.  To ensure this takes place, the system has a security requirement to sanitize user-inputted data and employ other secure development practices such as utilizing prepared statements to prevent against SQL injection attacks.
     
     Link: [Common Attacks](https://www.lucidchart.com/invitations/accept/1518de8f-6cbb-4010-923b-a17f04cffb25)

  5. Identity Management
  
     Description:  Security requirements around identity management are important to ensure that user accounts are removed when there is a separation.  Standardized, consolidated, and automated identity management services are in place to reduce risk, cost, and improve operational efficiency.  Identity and access management aid in reducing risk for an organization by removing access and roles from all services of an organization by deprovisioning.

     
     Link: [Fired employee](https://www.lucidchart.com/invitations/accept/1518de8f-6cbb-4010-923b-a17f04cffb25)


### Project documentation review
#### Alignment of security requirements with advertised features

MISP focuses on ease of use as their number one selling point, which adds concern that security requirements may be over looked to promote this feature.  Another advertised feature is the ease of sharing with trusted partners and trust-groups.  This is supposed to eliminate the duplication of work and enable collaborative analysis.  As part of this ease of use idea, data sharing is made easier by automatically exchanging and synchronizing with other parties and trust-groups in MISP.  MISP allows for simple built in sharing to delegate the publication of events or indicators to other organizations.  Each organization can use the advanced filtering functionality to tailor their own sharing policy including flexible sharing group policy and attribute level distribution mechanisms.

These features align to some extent with our security requirements.  It does require authentication.  But, in the documentation, is does not say that you could connect MISP to an identity store.  This would allow your own identity management system to control access.  This would help with identity creation and decommissioning.  It also not clear whether a user can create accounts as well, even an admin account.  There is user and role creation to dictate access control.  They promote the automatic exchange and synchronization of data and events, which would be done by an API.  Applications and API’s do not always verify the user is authorized for that target resource.  This would result in an access control flaw.

#### Security related configuration
The features section of the MISP website does not suggest an emphasis on the security of the system, rather it focuses on the ease of use for the user to add, edit, and share the event information as they have entered it.  It also focuses on the flexibility of it's design in various capacities, i.e. storing of data, integration with in-house solutions, and sharing of information wtih colleagues and others.

However, many of the system components involved in the security requirements above are discussed in the features section.  Like most programs, an administrator has the responsibility to add, edit, or delete users, maintain organizations (both internal and external), and create roles, to which users are assigned, among other tasks.  This implies that role-based access control is a capability of the system.  The features indicate that the system has a "flexible API to integrate MISP with \[other\] solutions" but does not discuss how it secures the admin features of that API.  Also, the documentation heavily references the sharing of data but does not allude to any of the security measures around such sharing other than the role-based access control already discussed.

The User Guide does discuss security-related topics in more detail.  For instance, it describes how to set up GPG encryption keys to be used for login, which fits into the secure authentication requirement.

The User Guide documentation does not reference all the security requirements. The requirement to protect against common web apps is not discussed in the documentation.

#### Installation
The installation guide references multiple security best practices.  To start, it recommends installing a minimal server version and enabling the server features required by the system.  After the necessary features are enabled, it recommends hardening them, specifically the OS, apache, and MySQL.  In addition, it recommends changing many of the default settings after installation, including the admin password, email address, and GPG key and the salt used to generate GPG keys.

<include stuff about certificate:
If a valid SSL certificate is not already created for the server, create a self-signed certificate - not good!
sudo openssl req -newkey rsa:4096 -days 365 -nodes -x509 \ - good algorithm used in rsa 4096 to generate certificate>

Some things that could be improved:
<includes config for 80 and 443 so doesn't force https.
database password included in config file in plaintext>
