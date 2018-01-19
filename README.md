      ________         ________
     /        \      /        \   
    /          \    /          \  
    |  +    +  |    |  +    +  |  
    |          |    |          |  
    \   {__}   /    \   {__}   /  
     \________/      \________/     
         |               |          
        _|_              |           
       / | \            /|\          
      /  |  \          / | \             Familyfe   
         |               |          
        / \             / \         
       /   \           /___\            
      /_    \_         |_  |_    

:family: Familyfe :couple:
=======================

Familyfe Role Based Acces Control

## Table of Contents                                    

- [Introduction](#introduction)
- [Role Based Access Control](#role-based-access-control)
- [Familyfe](#familyfe)
  - [Why it is needed](#why-it-is-needed)
  - [Where it is needed](#where-it-is-needed)
  - [Features](#features)
  - [Advantages over RBAC](#advantages-over-rbac)
- [Familyfe Role Based Access Control Method](#familyfe-role-based-access-control-method)
  - [Collaborations](#collaborations)
  - [Contracting](#contracting)
  - [Resources](#resources)
- [Relation to the Family](#relation-to-the-family)
  - [The Family](#the-family)
  - [The World](#the-world)
- [Implementations](#implementations)
- [Todo](#todo)

## Introduction
Most web applications rely on some sort of access control to keep users from accessing information not meant for them. If the question was asked as to the most popular access control method, many developers would answer [RBAC](https://en.wikipedia.org/wiki/Role-based_access_control) (Role-Based Access Control). And righty so. For it is the de-facto standard access control method for most web applications. Its popularity is evident from the fact that many products and businesses are using it directly or indirectly. It's also flexible, having different implementations and can enforce MAC (Mandatory  Access Control) and DAC (Discretionary Access Control) without any complication. And it simulates real life role (job) assignments. 

Many organizations use RBAC directly or indirectly. The traditional organizational structure for these organizations is the inline (hierarchical) organizational structure. But there has been a change in organizational structures to those that encourage information flow between members of an organization. Then there has come also the IoT. Central to the success of an IoT project is the ability to leverage an ecosystem of partners who can help provide this broad level of expertise. It is due to lack of such partnership, it was found out, that [75% of IoT projects fail](https://www.slideshare.net/CiscoBusinessInsights/journey-to-iot-value-76163389), with even those that are actually delivered seldom being regarded as a success. These partnerships/collaborations introduce problems difficult to be solved by normal implementations of RBAC.

There are cases in which organizations sign up for services where accounts are created for them on a single instance of an application on a cloud server. A simple example of this is an IoT server, such as [ttn](https://www.thethingsnetwork.org/), [cayenne](https://mydevices.com/), [thinger](https://thinger.io/), etc where different users are signed up and they are able to manage their devices. Although this is an attractive setup for IoT (or other) organizations which would like to concentrate on those things which are core to their businesss (building sensors and their IoT network) and leveraging on these existing servers, it is more suitable to individual users rather to an organizations since it is just a single (user) account that is created for the organization. Organizations are therefore requried (to be able to manage their users) to setup their own instances of these servers, duplicating several other similar servers that have been setup. This unnecessarily increases the cost of server maintenance and, in most cases, the requirement of expertise within the organization to do the server setup and maintenance. This is the problem that familyfe seeks to solve.

Familyfe Role Based Access Control (FRBAC), therefore, describes an access control method which allows organizations (accounts) to exist within a single system reducing the unnecesarry costs of duplication of servers, server maintenance costs and the unnecessary requirement of manpower with technical knowhow of server maintenace within the organizations. With several organizations existing within a single system, it also allows easy management of partnerships between organizations.

We will look very briefly at the basics of Role Based Access Control, then we will go on to explain familyfe: *why and where it is needed, and how it works*

**[⬆ back to top](#table-of-contents)**

**[⬇ Take me directly to Familyfe](#familyfe)**

## Role Based Access Control
In the fields of physical security and information security, access control (AC) is the selective restriction of access to a place or other resource. In computer security, access control approaches determine how users interact with data and other network resources. Access control measures also ensure data is protected from unauthorized disclosure or modification. General access control includes authorization, authentication, access approval, and audit. These are measures that can be used to manage information system accounts. A more narrow definition of access control would cover only access approval, whereby the system makes a decision to grant or reject an access request from an already authenticated subject, based on what the subject is authorized to access. 

[RBAC](https://en.wikipedia.org/wiki/Role-based_access_control) (Role Based Access Control) is an access control method where each identity is assigned a role and the roles determine what access rights the identity has. That is, RBAC allows access based on the job title. This is opposed to IBAC (Identity Based Access Control), where each identity has separate privilege assignment. For example, a human resources specialist should not have permissions to create network accounts; this should be a role reserved for network administrators.

RBAC looses some granularity compared to IBAC, however it gains better manageability in environments with large amounts of users. RBAC is usually implemented as a Hierarchy of roles (HRBAC). This allows roles to inherit privileges from other roles, which in turn makes it easier to add new operational privileges to the whole tree.

Let’s envision an app where we have three roles: ‘Guest’, User, Admin. We can then illustrate the role hierarchy as follows:

         ----------------------------
         | Guest                    |
         | (can Create)             |
         |                          |
         |  ---------------------   |
         |  | User              |   |
         |  | (can Read)        |   |
         |  | (can Update)      |   |
         |  |                   |   |
         |  |   --------------  |   |
         |  |   |Admin        | |   |
         |  |   |(can Create) | |   |
         |  |   --------------  |   |
         |  |                   |   |
         |  --------------------    |
         ----------------------------
<h4 align="center">Role Based Access Control</h4>
In the model shown,User inherits the privileges of Guest and Admin inherits the privileges of User.


Set notation can be used to illustrate this in this way:

    x ∈ Z................................................................[1]

The user x can only perform the functions of a role y if he is a member of the group of users Ry that has that role. That is

    x ∈ Ry...............................................................[2]

    Ry ⊆ Z...............................................................[3]

Where:

     x is a single user of the system

     Z is the set of all users in the system

     Ry is a set of users having the role y


**[⬆ back to top](#table-of-contents)**

## Familyfe
### Why it is needed
FRBAC is needed because:
- There is need to have a system that can be used by several organizations so that they can be free to concentrate on their core business without having to redo what has been done, and is best done, by others.
- There is need to reduce on expenditure by organizations. 
- There is need to reduce on unnecessary manpower employed by organizations. 
- There is need to avoid duplication on code in several servers.
- Of the need to have systems that can enable collaborations/partnerships between organizations.
- Of the need to have systems that that can implement different organizational structures used by different organizations, particularly those that allow for some level of autonomy in different department of an organization.
- RBAC does not sufficiently solve the problem of having several organizations on a single system.
- There is need to have a clear record of as people and their genealogies to prevent the marriage between relatives in this digital age.

### Where it is needed
FRBAC is needed where:
- Several organizations are needed to have (organization) accounts on a single system
- There is a collaboration/partnership between organizations
- An organization needs to leverage on existing server applications and avoid building or setting up its own
- An organization needs to reduce its expenditure by eliminating server setup and maintenance costs
- An organization needs to concentrate on its core business by leveraging on existing services provided by other organizations
- An organization has an organizational structure that allows for some level of autonomy in its departments.
- A system is required that has a deep hierarchy of groups.
- A record keeping of genealogies and finding the family relationship between people is required.

### Features
- Several organizations in a single system
- Collaboration between organizations
- Autonomy of organizations departments
- Single user can belong to several organization
- Single user has multiple identities
- Role hierarchical inheritance
- Hierarchical chain of groups of users
- Simulation of real-life families

### Advantages over RBAC
These are the features obtained by extending RBAC to FRBAC
- Several organizations in a single system
- Collaboration between organizations
- Autonomy of organizations departments
- Single user can belong to several organization
- Single user has multiple identities
- Hierarchical chain of groups of users
- Simulation of real-life families

**[⬆ back to top](#table-of-contents)**

## Familyfe Role Based Access Control Method
Familyfe Role Based Access Control Method is an extension of Role Based Access Control Method which allows several organizations to exist within a single system, giving [several advantages](#advantages-over-rbac) over RBAC systems while allowing normal RBAC to be used for each of the organizations in the system. 

We continue with the method of using sets to represent systems as given in [the introduction to RBAC](#role-based-access-control). In normal RBAC there may be a user x who is a member of the set of all system users Z and also belong to a group of users Ry having some role y. That is 
    
    x ∈ Z

    x ∈ Ry

    Ry ⊆ Z

There are in real life, however, systems that require a user x who is a member of on organization(set of users) A and who is also one of the all the users of a system represented by the set Z. This case can be represented by
   
    x ∈ A ⊆ Z............................................................[4]

[4] means that in this setup [2] gives more permission that required. For the user x should only be able to perfom the function of a role y on a resource owned by the organization A if he is a member of A. We may consider a system with two organizations, csyma(A1) and csynergy(A2) where Alice and John are users respectively. These users may have roles as shown in the table

User (x)                       | Organization            | Roles (y)
------------------------------ | ----------------------- | -----------------------
Alice (x1)                     | csyma (A1)              | admin (a)                 
John (x2)                      | csynergy (A2)           | admin (a)

<h4 align="center">Role Based Access Control in different Organizations</h4>

         ----------------------------         ----------------------------
         | Guest                    |         | Guest                    |
         | (can Create)             |         | (can Create)             |
         |                          |         |                          |
         |  ---------------------   |         |  ---------------------   |
         |  | User              |   |         |  | User              |   |
         |  | (can Read)        |   |         |  | (can Read)        |   |
         |  | (can Update)      |   |         |  | (can Update)      |   |
         |  |                   |   |         |  |                   |   |
         |  |   --------------  |   |         |  |   --------------  |   |
         |  |   |Admin        | |   |         |  |   |Admin        | |   |
         |  |   |(can Create) | |   |         |  |   |(can Create) | |   |
         |  |   --------------  |   |         |  |   --------------  |   |
         |  |                   |   |         |  |                   |   |
         |  --------------------    |         |  --------------------    |
         ----------------------------         ----------------------------
          csynergy                              csyma


In this case x1 and x2 are both members of Ra
    
    x1 ∈ Ra

    x2 ∈ Ra

For either of the users to perform the functions of admin on the resouces of any organization A, they need to fulfil this condition:

    x ∈ A ∩ Ry...........................................................[5]

### Collaborations

In a collaboration or a partnership between csyma and csynergy there will be another set C of users who belong to both organizations.  That is

    C = A1 ∩ A2 ∩...An ..................................................[6]

and for a role

    x ∈ C ∩ Ry...........................................................[7]

### Contracting
It is possible that the set C may be equal to either A1 or A2. If C = A2, then all the resources of csynergy will be accessible to csyma. This represents the case where csyma contracts csynergy to do something in its stead. 

    C = Ax...............................................................[8]

    x ∈ C ∩ Ry

<h4 align="center">Contracting</h4>

         ------------------------------------------------------------------------         
         | Guest                                                                 |
         | (can Create)                                                          |
         |                                                                       |
         |  ---------------------            ----------------------------        |
         |  | User              |            | Guest                    |        |
         |  | (can Read)        |            | (can Create)             |        |
         |  | (can Update)      |            |                          |        |
         |  |                   |            |  ---------------------   |        |
         |  |   --------------  |            |  | User              |   |        |
         |  |   |Admin        | |            |  | (can Read)        |   |        |
         |  |   |(can Create) | |            |  | (can Update)      |   |        |
         |  |   --------------  |            |  |                   |   |        |
         |  |                   |            |  |   --------------  |   |        |
         |  --------------------             |  |   |Admin        | |   |        |
         |                                   |  |   |(can Create) | |   |        |
         |                                   |  |   --------------  |   |        |
         |                                   |  |                   |   |        |
         |                                   |  --------------------    |        |
         |                                   ----------------------------        |
         |                                                                       |
         ------------------------------------------------------------------------


### Identities
In the new set C roles may need to be given to users which should not be carried to their respective organizations. For this to be achived, a user is given several identities and the subject x is changed from the user to the an identity of the user. That is a user P is a set of user identities, and for any user P,
    
    x ∈ P ...............................................................[9]

### Resources
Resources are owned by organizations so that a subject x has only access to the resources that are owned by the organization to which he belongs. That is, a resource t owned by organization a is a member of the resouces owned by organization a, Ta. It is only this set that can be accessed by a subject who belongs to organization a.

    t ∈ Ta .............................................................[10]

**[⬆ back to top](#table-of-contents)**

## Relation to the Family
The problem solved by familyfe is strickingly similar to one that had been solved a long time ago at the creation of the world. In fact, it is from there that the inspiration to extend RBAC in this direction was obtained. We find these things especially beautiful about the family.
- That [God created the family](https://www.biblegateway.com/passage/?search=matthew+19%3A4-6&version=KJV)
- That [God setteth the solitary in families](https://www.biblegateway.com/passage/?search=psalm+68%3A6&version=KJV)
- That [he who finds a wife finds a good thing](https://www.biblegateway.com/passage/?search=proverbs+18%3A22&version=KJV)
- That [a prudent wife is from the LORD](https://www.biblegateway.com/passage/?search=proverbs+19%3A14&version=KJV)
- That [children should "honour your father and your mother"](https://www.biblegateway.com/passage/?search=Exodus+20%3A12&version=KJV)
- That [fathers should not provoke their children](https://www.biblegateway.com/passage/?search=Ephesians+6%3A4&version=KJV)
- That [we all have a Father in heaven](https://www.biblegateway.com/passage/?search=Matthew+6%3A9&version=KJV)

Do you have a family? And would you like to make it a beautiful one, that your home may be a little heaven on earth? We recommend to you any of these free books.
- [Child Guidance](http://centrowhite.org.br/files/ebooks/egw-english/books/Child%20Guidance.pdf)
- [Messages to Young People](http://centrowhite.org.br/files/ebooks/egw-english/books/Messages%20to%20Young%20People.pdf)
- [Adventist Home](http://centrowhite.org.br/files/ebooks/egw-english/books/The%20Adventist%20Home.pdf)

You may also reach us at freebookcenter@gospelsounders.com or freebookcenter@gmail.com for a free hard copy book.

We do not deny that other people may have implemented an access control method similar to FRBAC and that this may in fact be a duplication of effort, but we find so much beauty in the family that we are compeled to develop this access control method and to call it familyfe (family life) RBAC. 

### The Family


### The World
Resources


**[⬆ back to top](#table-of-contents)**

## Implementations
Implementations                |   ...
------------------------------ | -------------------------
Node_FRBAC                     | [ ]  

**[⬆ back to top](#table-of-contents)**

## Todo

Todo                           |   ...
------------------------------ | -------------------------
Node_FRBAC                     | [ ]  
Node_familyfe                  | [ ]  
csymapp                        | [ ]
familyfe app                   | [ ]

**[⬆ back to top](#table-of-contents)**

## Contacts

Want to contribute further to the development of FRBAC? Submit a pull request, or get in touch via email.

- [Brian Onang'o](mailto:surgbc@gmail.com)
- [Brian Onang'o](mailto:brian@cseco.co.ke)

**[⬆ back to top](#table-of-contents)**