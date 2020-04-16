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

The EzGas application offers to users the possibility to check the list of the prices of different gas stations, to compare them and to find close gas stations using a map with the possibility of consulting their prices. The list of gas stations is costantly updated by users, following a crowdsourcing approach. 
 


# Stakeholders

| Stakeholder name  | Description | 
| ----------------- |:-----------:|
| Drivers  |Use the application to look for gas station and their prices| 
| Google Maps  |Does not use the application, supports API to embed map service| 
|Gas Station| Does not use the application, gets visibility from it|
|Developers | Do not use the application, invested time and resources to develop it|

# Context Diagram and interfaces

## Context Diagram

```plantuml
left to right direction
actor Driver as d
actor "Google Maps" as g
d -- (EzGas)
g -- (EzGas)
```

## Interfaces
| Actor | Logical Interface | Physical Interface  |
| ------------- |:-------------:| -----:|
|Driver | GUI |Touchscreen |
|Gas Station | GUI |Touchscreen |
|Google Maps| GMaps API |Internet connection |


# Stories and personas
Anna is a travelling salesman that has to drive her own car to work and between clients. Sometimes, in order to reach her clients, she needs to drive to nearby towns, and in general she has no set daily route. Since she is covering long distances every day, she is constantly in need of fuel for her car and she would like to purchase it at profitable rates. Most of the times she doesn't know where to find close gas stations and which of them is the most convenient, so she uses EzGas to look for them.

It's Friday afternoon, and Anna has just closed a deal with a distant customer. She needs to reach another customer but her car is out of fuel, so she opens EzGas to check a map of close gas stations. She can touch on one gas station to see the prices and the date they were last updated. If she wants she can also input her next costumer address and look for gas stations in that area.

Mike is a student that has recently been gifted with a new car by his parents. Marco has also a part-time job and since he has to maintain the cost of the car and of his free time hobbies, he is on a low budget for fuel expenses.
He drives almost every day to his job place and along the way he has different choices of gas station to refuel when in need. Before choosing a gas station between those, he opens EzGas to check the updated prices of his bookmarked gas stations to see which one is currently running the lowest prices.

It's Monday and Mike has spent his weekend out of town with his friends. He's running late for work and his car is out of fuel so he needs to reach as quickly as possible a gas station which is on his way to work. He decides to use EzGas, and since he is a registered user, he logs in to find his user defined list of favourites gas stations sorted by ascending prices. With a touch of his finger he has access to the quickest route to his gas station of choice, provided by Google Maps.

# Functional and non functional requirements

## Functional Requirements

| ID        | Description  |
| ------------- |:-------------:| 
|  FR1     | Record that a colleague has used n capsules of a certain type, update his account |  
|  FR2     | Record that a visitor has used n capsules of a certain type |
|  FR3     | Record that a colleague has recharged x euros on her account |
|  FR4     | Record that n capsules of a certain type have been received, and paid for |
|  FR5     | Produce a report about consumption and recharges of a colleague over a certain period of time |
|  FR6     | Produce a report about all consumption and recharges over a certain period of time |
|  FR7     | Manage types of capsules and prices |
|  FR8     | Manage colleagues and accounts |

## Non Functional Requirements

| ID        | Type (efficiency, reliability, .. see iso 9126)           | Description  | Refers to |
| ------------- |:-------------:| :-----:| -----:|
|  NFR1     | Usability | Application should be used with no training by any colleague in the office  | All FR |
|  NFR2     | Performance | All functions should complete in < 0.5 sec  | All FR |
|  NFR3     | Portability | The application runs on MS Windows (7 and more recent)  | All FR |
|  NFR4     | Portability | The application (functions and data) should be portable from a PC to another PC in less than 5 minutes | All FR |
|  NFR5     | Localisation | Decimal numbers use . (dot) as decimal separator ||


# Use case diagram and use cases

## Use case diagram

```plantuml
left to right direction
actor Administrator as a
a -- (FR1  Record usage of capsules by colleague)
a -- (FR2 Record usage of capsules by visitor)
a -- (FR3 Record recharge of account of colleague)
a -- (FR4 Record purchase of capsules)
a -- (FR5 Produce report on consumption of colleague)
a -- (FR6 Produce report on all consumptions)
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
