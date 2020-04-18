# Official Requirements Document

Authors: Giovanni Blangiardi

Date: 19/04/2020

Version: 1

Change history

| Version | Changes | 
| ----------------- |:-----------|



# Contents
- [Abstract](#abstract)
- [Stakeholders](#stakeholders)
- [Context Diagram and interfaces](#context-diagram-and-interfaces)
	+ [Context Diagram](#context-diagram)
	+ [Interfaces](#interfaces) 
	
- [Stories and personas](#stories-and-personas)
- [Functional and non functional requirements](#functional-and-non-functional-requirements)
	+ [Functional Requirements](#functional-requirements)
	+ [Non functional requirements](#non-functional-requirements)
- [Use case diagram and use cases](#use-case-diagram-and-use-cases)
	+ [Use case diagram](#use-case-diagram)
	+ [Use cases](#use-cases)
	+ [Relevant scenarios](#relevant-scenarios)
- [Glossary](#glossary)
- [System design](#system-design)
- [Deployment diagram](#deployment-diagram)

# Abstract

When drivers need to refuel their vehicles they usually tend to go to the nearest gas station, or to one that they could find along the way. This comes with a cost: accepting whatever rates the said gas station is currently offering, ignoring possible chances to save some money when there may be close gas stations that are running lower prices.

The EzGas application offers to users the possibility to check the list of the prices of different gas stations, to compare them and to find close gas stations using a map. The list of gas stations is costantly updated by users, following a crowdsourcing approach. 
 


# Stakeholders

| Stakeholder name  | Description | 
| ----------------- |:-----------:|
| Users  |Use the application to look for gas station and their prices| 
| Google Maps  |Does not use the application, supports API to embed map service| 
|Gas Station| Does not use the application, gets visibility from it|
|Developers | Do not use the application, invested time and resources to develop it|

# Context Diagram and interfaces

## Context Diagram

```plantuml
left to right direction
actor User as d
actor "Google Maps" as g
actor "Authenticated User" as a
d - (EzGas)
(EzGas) - g
top to bottom direction
d <|-- a
```

## Interfaces
| Actor | Logical Interface | Physical Interface  |
| ------------- |:-------------:| -----:|
|Driver | GUI |Touchscreen |
|Gas Station | GUI |Touchscreen |
|Google Maps| Google Maps API |Internet connection |


# Stories and personas
Anna is a travelling salesman that has to drive her own car to work and between clients. Sometimes, in order to reach her clients, she needs to drive to nearby towns, and in general she has no set daily route. Since she is covering long distances every day, she is constantly in need of fuel for her car and she would like to purchase it at profitable rates. Most of the times she doesn't know where to find close gas stations and which of them is the most convenient, so she uses EzGas to look for them.

It's Friday afternoon, and Anna has just closed a deal with a distant customer. She needs to reach another customer but her car is out of fuel, so she opens EzGas to check a map of close gas stations. She can touch on one gas station to see the prices and the date they were last updated. If she wants she can also input her next costumer address and look for gas stations in that area.

Mike is a student that has recently been gifted with a new car by his parents. Marco has also a part-time job and since he has to maintain the cost of the car and of his free time hobbies, he is on a low budget for fuel expenses.
He drives almost every day to his job place and along the way he has different choices of gas station to refuel when in need. Before choosing a gas station between those, he opens EzGas to check the updated prices of his bookmarked gas stations to see which one is currently running the lowest prices.

It's Monday and Mike has spent his weekend out of town with his friends. He's running late for work and his car is out of fuel so he needs to reach as quickly as possible a gas station which is on his way to work. He decides to use EzGas, and since he is a registered user, he logs in to find his user defined list of favourites gas stations sorted by ascending prices. With a touch of his finger he has access to the quickest route to his gas station of choice, provided by Google Maps.

# Functional and non functional requirements

## Functional Requirements

| ID     | Description  |
| ------------- |:-------------:|  
|**FR1** |**Select a gas station in the map to show prices**|
|*FR1.1* |*Search the map for user's input address*		  |
|*FR1.2* |*Retrieves best route to selected Gas Station*|
|**FR2** |**Handles User Authentication** |
|*FR2.1* |*Log in*							|
|*FR2.2* |*Log out*							|
|*FR2.3* |*User Registration*   			|
|**FR3** |**Handles Update of the System**  |
|*FR3.1* |*Authenticated User inserts new Gas Station* 	|
|*FR3.2* |*Authenticated User inserts new prices for selected Gas Station*|
|**FR4** |**Implements rating system for updates of gas station position and prices** |
|**FR5** |**Handles User Preferences**|
|*FR5.1* |*Show sorted list of bookmarked Gas Stations*|
|*FR5.2* |*Add selected Gas Station to bookmarks*|

## Non Functional Requirements

| ID        | Type (efficiency, reliability, ... see iso 9126)           | Description  | Refers to |
| ------------- |:-------------:| :-----:| -----:|
|  NFR1     | Usability | Application should be used with no training by any user| All FR |
|  NFR2     | Performance | All functions should complete in < 0.5 sec  | All FR |
|  NFR3     | Portability | The Application should be supported by web(accsesible by smartphone or PC) | All FR |



# Use case diagram and use cases

## Use case diagram

```plantuml
left to right direction
actor User as U
actor "Authenticated User" as Au
actor "Google Maps" as G
U <|- Au
(Select a Gas Station in the map\n) as UC1
(Show prices of Gas Station\n**FR1**) as UC11
(Retrieves best route to Gas Station\n**FR1.2**) as UC13
(Search the map for user input address\n**FR1.1**) as UC12
(Authenticate User\n**FR2**) as UC2
(Log in\n**FR2.1**) as UC21
(Log out\n**FR2.2**) as UC22
(Update System\n**FR3**) as UC3
(Insert new Gas Station\n**FR3.1**) as UC31
(Updates prices of a Gas Station\n**FR3.2**) as UC32
(View list of bookmarks\n**FR5.1**) as UC51
(Add a Gas station to bookmarks\n**FR5.2**) as UC52
U-->UC1
UC1 ..> UC11 : <include>
UC1 ..> UC13 : <include>
UC13 --> G
UC1 ..> UC12 : <include>
Au --> UC2
UC12 --> G
UC2 ..> UC21 : <include>
UC2 ..> UC22 : <include>
Au --> UC3
UC3 ..> UC31 : <include>
UC3 ..> UC32 : <include>
Au --> UC51
Au --> UC52


```
## Use Cases

### Use case 1, UC1 - FR1 Select a Gas Station on the Map to show prices

| Actors Involved        | User |
| ------------- |:-------------:| 
|  Precondition     | Gas Station G exists in the DB, G.prices != null |  
|  Post condition     | |
|  Nominal Scenario     |  User opens map, selects a Gas Station G and he can see its prices|
|  Variants     ||

### Use case 1.1, UC1.1 - FR1.1 Search the map for user's input address

| Actors Involved        | User |
| ------------- |:-------------:| 
|  Precondition     |Input address is valid |  
|  Post condition     | Map shows the address and nearby Gas Stations |
|  Nominal Scenario     | User types the address A in the search bar of the map, map moves to address A  |
|  Variants     ||

### Use case 1.2, UC1.2 - FR1.2 Retrieves best route to selected Gas Station

| Actors Involved        | User |
| ------------- |:-------------:| 
|  Precondition     | Gas Station G exists in the DB |  
|  Post condition     | Map shows best route to G |
|  Nominal Scenario     | User selects a Gas Station G and clicks on the gui button to retrieve indications|
|  Variants     ||


### Use case 2, UC2 - FR2 Authenticate User

| Actors Involved        | Authenticated User |
| ------------- |:-------------:| 
|  Precondition     | User account is present in the DB|  
|  Post condition     | User is Authenticated|
|  Nominal Scenario     |User U that has an account credentials can log in in the system to acces optional features  |
|  Variants     | Wrong Username or Password, password forgotten |

### Use case 3.1, UC3.1 - FR3.1 Authenticated User inserts new Gas Station

| Actors Involved        | Authenticated User |
| ------------- |:-------------:| 
|  Precondition     | User Account exists in the DB, User is logged in, Gas Station G is still not present in the DB |  
|  Post condition     | G is inserted succesfully in the system |
|  Nominal Scenario     |User sees a missing Gas Station in the map and decides to add it|
|  Variants     |  |

### Use case 3.2, UC3.2 - FR3.2 Authenticated User inserts new prices for selected Gas Station

| Actors Involved        | Authenticated User |
| ------------- |:-------------:| 
|  Precondition     | User Account exists in the DB, User is logged in, Gas Station G is present in the DB |  
|  Post condition     | G.prices_pre != G.prices_post |
|  Nominal Scenario     |User notices that prices of the Gas Station G have changed and decides to update them|
|  Variants     |  |

### Use case 5.1, FR5.1 View sorted list of Bookmarks

| Actors Involved        | Authenticated User  |
| ------------- |:-------------:| 
|  Precondition     | User is logged in, bookmark list is not empty |  
|  Post condition     | A list of Gas Stations sorted by ascending orices is shown |
|  Nominal Scenario     |User wants to consult the prices of his favourite Gas Stations|
|  Variants     | |

### Use case 5.2, FR5.2 Add selected Gas Station to bookmarks

| Actors Involved        | Authenticated User  |
| ------------- |:-------------:| 
|  Precondition     | User is logged in, Gas Station G exists on the DB |  
|  Post condition     |Bookmarked Gas station count += 1|
|  Nominal Scenario     |User selects a Gas Station G from the map and adds it to his bookmark list|
|  Variants     | |

# Relevant scenarios

## Scenario 1

| Scenario ID: SC1        | Corresponds to UC3.2  |
| ------------- |:-------------| 
| Description | Authenticated User inserts new prices for selected Gas Station |
| Precondition | Gas Station G has already been defined in the DB and User is logged in |
| Postcondition | Prices of G updated |
| Step#        |  Step description   |
|  1     | User search for G in the map |  
|  2     | User clicks on G  |
|  3     | User clicks on "Update prices" button |
| 4 | User types new prices |
|5  | User confirms changes|


# Glossary

```plantuml
class Ezgas
class User
class "Authenticated User" as AU {
	+ Email
	+ Username
	+ Password
	+ Bookmarks
}

class "Gas Station" as G {
	+name
	+price of fuel
}

class "Map Position" as M {
	+address
	+latitude
	+longitude
}

class "UpdatePrice" as Upd {
	+newprice
	+date
	+rating
}

class "Create New GS" as CNG {
	+name 
}

User "*"-up- Ezgas
User <|-- AU
Ezgas --"*" G
G "1"--"1" M
AU "1"-right-"*" Upd
Upd "*"-right-"1" G

```

# System Design

```plantuml
class "DB Server" as S

S -- "*"Smartphone
"Google Maps" -- "*" Smartphone
Smartphone .. "*" Application
```

# Deployment Diagram

```plantuml
artifact "EZGas" as a
node "Google Play store" as g
node "iOS App store" as i
node "Smartphone" as p
a -- g 
a -- i
g --p 
i -- p
```
