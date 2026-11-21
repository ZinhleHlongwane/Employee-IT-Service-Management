# Employee IT Service Management

A ServiceNow application for managing employee IT incidents and equipment requests, with automated workflows, approval processes, and fulfilment tracking.

> **Project status:** In development. This repository documents the application configuration and implementation. It does not contain an export of the ServiceNow application itself.

## Overview

Employee IT Service Management is a custom ServiceNow application designed to give employees a structured way to report IT issues and request equipment, while providing support staff with workflows for handling incidents and fulfilling approved requests.

The application is built around two core processes:

- **IT incident management** — employees submit incidents with required descriptions. A Flow Designer workflow processes new incidents, sends configured email actions, checks for high-priority incidents, and assigns records to the Service Desk and a support agent.
- **Equipment request management** — employees submit equipment requests with a business justification. Requests go through an approval workflow; approved requests are routed to the Service Desk and tracked through fulfilment, while rejected requests retain a rejected approval status.

## Implemented features

### IT incidents

- Custom IT Incident table.
- Employee-facing incident record producer.
- Business rule that prevents submission when the Short Description is empty.
- Flow Designer workflow triggered when an incident is created.
- High-priority decision branch with an additional email action.
- Assignment update that routes incidents to the Service Desk and assigns a support agent.

### Equipment requests

- Custom Equipment Request table.
- Employee-facing equipment request catalogue item.
- Equipment type choices and business justification field.
- Business rule that requires a business justification.
- Flow Designer approval workflow with approved and rejected paths.
- Approved requests are routed to the Service Desk and set to Pending fulfilment.
- Fulfilment tracking with Pending, In Progress, Fulfilled, and Cancelled states.
- Assigned Support Agent and Fulfilment Notes fields.

### Application access

The application includes employee, manager, and IT support agent roles, with table-level access control rules configured for the Equipment Request table. Access-control coverage is still being reviewed; complete row-level ownership restrictions and IT Incident ACL coverage are not yet claimed as finished.

## Technology

- ServiceNow
- ServiceNow Studio
- Flow Designer
- Service Catalog and Record Producers
- Business Rules
- Access Control Lists (ACLs)

## Workflow summaries

### IT incident

1. An employee submits an IT incident.
2. The Short Description business rule validates that a description is present.
3. The record-created flow runs its email actions.
4. The flow checks whether the incident is high priority and runs the corresponding branch.
5. The flow updates assignment to the Service Desk and a support agent.

### Equipment request

1. An employee submits an equipment request with a business justification.
2. The justification business rule prevents an empty submission.
3. The record-created flow requests approval.
4. An approved request is assigned to the Service Desk and set to Pending fulfilment.
5. A rejected request is marked Rejected.
6. Support staff can update the fulfilment status and assigned support agent.

## Verification performed

The following behaviours have been manually checked in the ServiceNow instance:

- Empty IT Incident Short Description is blocked.
- Empty Equipment Request Business Justification is blocked.
- Equipment request approval and rejection paths were exercised.
- An approved equipment request was routed to the Service Desk and progressed from Pending to In Progress to Fulfilled.
- The IT Incident flow test run completed its trigger, email actions, priority condition, and record update without a reported flow error.

**Verification limitations:** Email action execution was observed in Flow Designer, but successful email delivery to a recipient has not been independently verified. The application’s ACL configuration is still under review.

## Repository contents

Documentation and supporting project artefacts will be added here as the project is completed. Screenshots and diagrams will be included only when they reflect the actual ServiceNow configuration.

## Future improvements

- Complete and test IT Incident ACL coverage.
- Add and verify record-ownership restrictions where required.
- Replace the temporary System Administrator approval test configuration with the intended manager approval relationship.
- Verify end-to-end email delivery.
- Add further repeatable test evidence and application screenshots.

## About

This is a personal practical development project built in ServiceNow to demonstrate application configuration, workflow automation, validation, approval handling, and service-management process design.

The project is being documented progressively. Features described as implemented have been configured and tested to the extent stated above; planned improvements are listed separately.
