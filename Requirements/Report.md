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
         
     Description:
 
     Link: [Data Leakage](./misuse-cases/Data-Leakage.svg)

  2. Access Control
  
     Description: Security requirements around access control should consider the restrictions placed on authenticated users.  Done properly, this will prevent attackers from accessing unauthorized functionality or data.
 
     Link: [Access Control](./misuse-cases/Access-Control.svg)

  3. Authentication
  
     Description: The system has a security requirement to ensure that the authentication mechanism properly protects access to sensitive data.  Authentication centers around the login mechanism, but additional requirements exist around this login to ensure it is adequate.  THe login mechanism has a requirement to operate securely in the face of a variety of attacks, including Insufficient authentication, weak password recovery, and brute force attacks.  This can be accomplished by adding additional requirements to the login mechanism, including ensuring that login attempts are limited and that authentication and authorization is checked with every attempt to access data.  Requirements for other processes that may affect the security of the login include having adequate help desk processes to verify the identity of callers when they wish to change their passwords to protect against weak password recovery attacks.
     
     Link: [Authentication](./misuse-cases/Authentication.svg)

  4. Common Attacks
     
     Description:
     
     Link: [Common Attacks](./misuse-cases/Common-Attacks.svg)

  5. Fired Employee
  
     Description:
     
     Link: [Fired employee](./misuse-cases/Fired-employee.svg)


### Project documentation review

#### Security related configuration
#### Installation
