# Design

### Objective

Institutes have 'professional' students that are following classes but who are not enrolled in the institute student system. These professional students are entitleed to be rewarded with a 'edubadge' upon a pass of exams but for that they need to have an email-adress related to the institute.

In order to facilitate these professional students with such an email identity, it is proposed to factilitate institutes with a 'guest-idp'.

This Guest IDP has followin structure:

```
/guest-idp
    / admin: platform administrator
         / email: admin@guest-idp.org
         / password: ...
    / institute-a
        / name: displayname of institute-A
        / admin: Institute administrator
            / email: admin@institute-a.guest-idp.org
            / password: ...
        / people
            / John
                / uid: john.doe@institute-a.guest-idp.org
                / email: john666@gmail.com
                / firstname: John
                / lastname: Doe
                / password: ...
            / Jane
                / ...
            / ...
    / institute-b
        / name: displayname of institute-B
        / admin: Institute administrator
            / email: admin@institute-b.guest-idp.org
            / password: ...
         / people
            / Lucy
                / uid: lucy.skywalker@institute-b.guest-idp.org
                / email: lucy49@gmail.com
                / firstname: Lucy
                / lastname: Skywalker
                / password: ...
            / Caroll
                / ...
            / ...    
    / ...
```

### Workflow: Institute enrollment

The guest-idp is deployed. Only the platform adminsitrator exists.
The platform administrator create an 'inistitute' by providing:
* displayname of the institute
* shortname of institute (used in email address subdomains)
* email address of administrator.

By providing these details, the system will create a branch in the tree for this institute. Also an email is send to the institute administrator with a initial one-time-password.

### Workflow: Institute student enrollment

The institute administrator logs in with his administrator email in combination with his password and then he is presented with follwoing options:
* Change his own password
* Invite a student by entering following details:
  * firstname
  * lastname
  * email ( this is personal email address of the student)
  
* Upon entry of above details, the system generates 2 additional attributes:
  * password
  * uid: This uid is in the form of email address: 
  
```
<firstname>.<lastname>@<institute-shortname>.<guest-idp>
```

By inviting a student, the system creates an identity in the people branch of this institute and sends an invitation email to the person with a the initial generated one-time-password.

### Workflow: Student accepting the invitation email

The invitation email contains a link to the profile page that the student needs to visit initially.
The profile page present asks for the password that was in the inviation mail.
When entered the correct password and forcelbly adjusted to a new value, the student will be presented with his 'uid'.


### Workflow: Student authenticating to edudbadges using the guest-idp.

The student needs to:
a) Select Guest IDP as the Identiy Provider
b) Use his provided UID and PASSWORD.

The IDP verrifies the password and allows access.