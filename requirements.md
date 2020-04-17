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
|*FR3.1* |*User inserts new Gas Station* 	|
|*FR3.2* |*User inserts new prices for selected Gas Station*|
|**FR4** |**Implements rating system for updates of gas station position and prices** |
|**FR5** |**Handles User Preferences**|
|*FR5.1* |*Show sorted list of bookmarked Gas Stations*|
|*FR5.2* |*Add selected Gas Station to bookmarks*|

## Non Functional Requirements

| ID        | Type (efficiency, reliability, ... see iso 9126)           | Description  | Refers to |
| ------------- |:-------------:| :-----:| -----:|
|  NFR1     | Usability | Application should be used with no training by any user| All FR |
|  NFR2     | Performance | All functions should complete in < 0.5 sec  | All FR |
|  NFR3     | Portability | The Application should be multiplatform (Android, iOS) | All FR |



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

### Use case 1, UC1 - FR1  Record usage of capsules by colleague

| Actors Involved        | Administrator |
| ------------- |:-------------:| 
|  Precondition     | Capsule T exists, colleague C exists |  
|  Post condition     | T.quantity_post < T.quantity_pre |
| | C.PersonalAccount.balance_post < C.PersonalAccount.balance_pre |
|  Nominal Scenario     | Administrator selects capsule type T, selects colleague C, Deduce quantity for capsule T, deduce price of T by account of colleague C|
|  Variants     | Account of colleague C has not enough money, issue warning |

### Use case 2, UC2 - FR2 Record usage of capsules by visitor

| Actors Involved        | Administrator |
| ------------- |:-------------:| 
|  Precondition     | Capsule T exists, visitor has no account |  
|  Post condition     | T.quantity_post < T.quantity_pre |
| | LaTazzaAccount.amount_post > LaTazzaAccount.amount_pre |
|  Nominal Scenario     | Administrator selects capsule type T, Deduce quantity for capsule T, add price of T on LaTazzaAccount.amount|
|  Variants     |  |

### Use case 3, UC3 - FR3 Record recharge of account of colleague

| Actors Involved        | Administrator |
| ------------- |:-------------:| 
|  Precondition     | Personal Account PA exists , quantity >0 |  
|  Post condition     | PA.balance_post = PA.balance_pre + quantity |
|  | LaTazzaAccount.balance_post = LaTazzaAccount.balance_pre + quantity  |
|  Nominal Scenario     | Administrator selects account PA of colleague C, increase account of  quantity, increase LaTazza account of quantity|
|  Variants     |  |

### Use case 4, UC4 - FR4 Record purchase of capsules

| Actors Involved        | Administrator |
| ------------- |:-------------:| 
|  Precondition     | Capsule type CT exists,  LaTazzaAccount.balance has enough money for the purchase|  
|  Post condition     | CT.quantity_post > CT.quantity _pre |
| | LaTazzaAccount.balance_post < LaTazzaAccount.balance_pre|
|  Nominal Scenario     | At time of order Administrator records money spent for order. At time of reception administrator selects capsule type CT, increases its quantity by a given number|
|  Variants     |  |

### Use case 5, FR5 Produce report on consumption of colleague

| Actors Involved        | Administrator  |
| ------------- |:-------------:| 
|  Precondition     | Colleague C exists |  
|  Post condition     |  |
|  Nominal Scenario     | Administrator selects colleague C, defines a time range,  application collects all transactions for C (recharges and capsules taken) in the time range and presents them|
|  Variants     | |

### Use case 6, FR6 Produce report on all consumptions

| Actors Involved        | Administrator |
| ------------- |:-------------:| 
|  Precondition     |  |  
|  Post condition     |  |
|  Nominal Scenario     | Administrator defines a time range,  application collects all transactions (recharges, purchases, and capsules taken) in the time range and presents them |
|  Variants     | |


# Relevant scenarios

## Scenario 1

| Scenario ID: SC1        | Corresponds to UC1  |
| ------------- |:-------------| 
| Description | Colleague uses one capsule of type T|
| Precondition |  account of C has enough money to buy capsule T|
| Postcondition |  account of C updated, count of T updated |
| Step#        |  Step description   |
|  1     | Administrator selects capsule type T |  
|  2     |  Administrator selects colleague C |
|  3     | Deduce one for quantity of capsule T |
| 4 | Deduce price of T from account of C|

## Scenario 2

| Scenario ID: SC2        | Corresponds to UC1  |
| ------------- |:-------------| 
| Description | Colleague uses one capsule of type T, account negative|
|Precondition |  account of C has not enough money to buy capsule T|
|Postcondition |  account of C updated, count of T updated |
| Step#        | Step description  |
|  1     | Administrator selects capsule type T |  
|  2     | Administrator selects colleague C |
|  3     | Deduce one for quantity of capsule T  |
|  4     | Deduce price of T from account of C  |
|  5     | Account of C is negative, issue warning  |


# Glossary

```plantuml
class LaTazza
class Colleague {
+ name
+ surname
}

class PersonalAccount {
+ balance
}

class CapsuleType {
+ name
+ price
+ quantity
}

class LaTazzaAccount {
+ balance
}

class BoxPurchase {
+ quantity
}

class Transaction {
+ date
+ amount
}

class Recharge
class Consumption


LaTazza -- "*" Colleague
LaTazza -- "*" CapsuleType
LaTazza -- LaTazzaAccount

LaTazzaAccount -- "*" BoxPurchase
LaTazzaAccount -- "*" Consumption

CapsuleType -- "*" Consumption
CapsuleType -- "*" BoxPurchase

Colleague -- PersonalAccount
PersonalAccount -- "*" Transaction

Transaction <|-- Recharge
Transaction <|-- Consumption
Transaction <|-- BoxPurchase

```

# System Design
Not really meaningful in this case. Only one personal computer is needed.

```plantuml
class "Personal Computer"
```

# Deployment Diagram
As a stand-alone application only one node is needed.

```plantuml
artifact "La Tazza Application" as a
node "Personal Computer" as n
a -- n
```
