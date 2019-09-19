---
id: new-property
title: Register Property Application
sidebar_label: Register New Property
---

A new property can be registered using NewPropertyApplication

v0.11

## Oracles

### Oracle rewards

Oracle rewards can be claimed from the following application statuses:
* STORED
* REJECTED
* CLOSED

## Timeouts

All the values are provided in seconds

#### PM_APPLICATION_CANCEL_TIMEOUT 
* the timer starts after the application was changed into PENDING status
* after the timeout an applicant can #cancel() the application being in PENDING status

#### PM_APPLICATION_CLOSE_TIMEOUT;
* the timer starts after the application was changed into REVERSED status
* after the timeout anyone can #close() the application being in REVERSED status

#### PM_ROLE_UNLOCK_TIMEOUT;
* the timer starts after an oracle role was changed into LOCKED status
* after the timeout anyone can #unlock() the oracle role being in LOCKED status back to PENDING

## Application Status Flow

![Application Status List](/img/NewPropertyManager.v0.11.png?raw=true "NewPropertyManager")

### Application Status List
* NOT_EXISTS: 0,
* PARTIALLY_SUBMITTED: 1,
* CONTOUR_VERIFICATION: 2,
* CANCELLED: 3,
* CV_REJECTED: 4,
* PENDING: 5,
* APPROVED: 6,
* REJECTED: 7,
* REVERTED: 8,
* PARTIALLY_RESUBMITTED: 9,
* STORED: 10,
* CLOSED: 11


### Detailed Application Status Description

#### NOT_EXISTS (0)

There is no application with the given ID.

Available actions:

* #submit() - submit a new application, changes status to PARTIALLY_SUBMITTED

#### PARTIALLY_SUBMITTED (1)

There is contour and the highest point values not submitted yet

Previous statuses:

* SUBMITTED

Further statuses:

* CONTOUR_VERIFICATION

Available actions:

* #setContour() - add a contour and the highest point values, changes status to CONTOUR_VERIFICATION


#### CONTOUR_VERIFICATION (2)

Previous statuses:

* PARTIALLY_SUBMITTED
* PARTIALLY_RESUBMITTED
* CV_REJECTED

Further statuses:

* PENDING - if contour verifiers approved the application
* CV_REJECTED - if contour verifiers rejected the application

Available actions:

* there is no any action required


#### CANCELLED (3)

The applicant cancelled the application.
He is able to call #cancel() method only after `PM_APPLICATION_CANCEL_TIMEOUT` timeout had been passed after
the application status changed into PENDING.

Previous statuses:

* PENDING
* PARTIALLY_RESUBMITTED
* CV_REJECTED

Further statuses:

* this is a final status

Available actions:

* this is a final status

#### CV_REJECTED (4)

The application was rejected by Contour Verifiers. The status was triggered by
CV contract #pushRejected() method.

The applicant can resubmit the application with #setContour() method again

Previous statuses:

* CONTOUR_VERIFICATION

Further statuses:

* CONTOUR_VERIFICATION

Available actions:

* #setContour() - add a contour and the highest point values, changes status to CONTOUR_VERIFICATION

#### PENDING (5)

The application work in progress. Any oracle can lock his role in order to work on it.

Previous statuses:

* CONTOUR_VERIFICATION
* REVERTED

Further statuses:

* APPROVED
* REJECTED
* REVERTED
* CANCELLED

Available actions:

* #approve() - any oracle who locked the application can approved it, approvals from all the roles required 
    in order to trigger the application to APPROVED status
* #reject() - any oracle who locked the application can reject it if he found malicious behaviour from the applicant,
    despite the other oracle decisions
* #revert() - any oracle who locked the application can revert it if he found that not all the details were
    correct
* #cancel() - anyone can cancel the application after `PM_APPLICATION_CANCEL_TIMEOUT`

#### APPROVED (6)

The application was approved by all required oracle roles.

Previous statuses:

* PENDING

Further statuses:

* STORED

Available actions:

* #store() - anyone can store a contour and the highest point into SpaceGeoDataRegistry as a separate step

#### REJECTED (7)

The application was rejected by one of the oracles in case of malicious behaviour.

Previous statuses:

* PENDING

Further statuses:

* this is a final status

Available actions:

* this is a final status

#### REVERTED (8)

The application was reverted in order to allow the applicant to adjust the data and resubmit it again.
There only one #revert() call enough to change a status to REVERTED despite of the other oracle role decisions.

Previous statuses:

* PENDING

Further statuses:

* PENDING
* PARTIALLY_RESUBMITTED
* CLOSED

Available actions:

* #resubmit() - the applicant can resubmit the application with different data. Depends on either the 
    contour/highest point should be changed or not, the status changes to PARTIALLY_RESUBMITTED or
    PENDING correspondingly.
* #close() - the applicant can close the application anytime if he wants to. After a `PM_APPLICATION_CLOSE_TIMEOUT`
    anyone can close the application. If the applicant don't want to allow anyone to close his application,
    he should resubmit it before the timeout passes.
    
#### PARTIALLY_RESUBMITTED (8)

The applicant decided to resubmit the application with a contour and/or the highest point modification.

Previous statuses:

* REVERTED

Further statuses:

* CONTOUR_VERIFICATION

Available actions:

* #setContour() - add a contour and the highest point values, changes status to CONTOUR_VERIFICATION

#### STORED (10)

All the information from an approved application was stored into SpaceGeoDataRegistry.
The separate method and status are required in order to allow the applicant to store a long enough contour.

Previous statuses:

* APPROVED

Further statuses:

* this is a final status

Available actions:

* this is a final status

#### CLOSED (11)

The application was closed either by the applicant himself or by anyone after `PM_APPLICATION_CLOSE_TIMEOUT`

Previous statuses:

* REVERTED

Further statuses:

* this is a final status

Available actions:

* this is a final status

## Oracle Role Status Flow

### Oracle Role Status List

* NOT_EXISTS: 0,
* PENDING: 1,
* LOCKED: 2,
* APPROVED: 3,
* REJECTED: 4,
* REVERTED: 5

### Detailed Application Status Description

#### NOT_EXISTS (0)

There is no oracle role was assigned yet

Further statuses:

* PENDING

Available actions:

* there is no explicit action required. All the roles would be assigned during #submit() call

#### PENDING (1)

There role was assigned to participate in an application review

Previous statuses:

* NOT_EXISTS

Further statuses:

* LOCKED
* APPROVED
* REVERTED

Available actions:

* #lock() - an oracle with a corresponding role can lock the application

#### LOCKED (2)

The role has been locked by an oracle

Previous statuses:

* PENDING

Further statuses:

* APPROVED
* REJECTED
* REVERTED

Available actions:

* #approve() - an oracle approves the application
* #reject() - an oracle rejects the application
* #reverts() - an oracle reverts the application
* #unlock() - anyone can unlock an oracle from his role after `PM_ROLE_UNLOCK_TIMEOUT`

#### APPROVED (3)

The oracle has approved the application. He can't change his decision.

Previous statuses:

* LOCKED

Further statuses:

* LOCKED - in case when one of the other oracles #revert() the application

Available actions:

* there is no action available in this status

#### REJECTED (4)

The oracle has rejected the application. He can't change his decision.

Previous statuses:

* LOCKED

Further statuses:

* LOCKED - in case when one of the other oracles #revert() the application

Available actions:

* there is no action available in this status

#### REVERTED (5)

The oracle has reverted the application. He can't change his decision.
The applicant can resubmit the application and reset all the oracle roles to `LOCKED` status

Previous statuses:

* LOCKED

Further statuses:

* LOCKED

Available actions:

* there is no action available in this status
