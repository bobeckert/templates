# Run Book / Service Operation Manual

## Service or system overview

**Service or system name:**

### Business overview

> What business need is met by this service or system? What expectations do we have about availability and performance?

_(e.g. Provides reliable automated reconciliation of logistics transactions from the previous 24 hours)_

### Technical overview

> What kind of system is this? Web-connected order processing? Back-end batch system? Internal HTTP-based API? ETL control system?

_(e.g. Internal API for order reconciliation based on Ruby and RabbitMQ, deployed in Docker containers on Kubernetes)_

### Service Level Agreements (SLAs)

> What explicit or implicit expectations are there from users or clients about the availability of the service or system?

> If you can't define explicit or implicit expectations, is this a service that you have to fix now or can it wait until Monday?

_(e.g. Contractual 99.9% service availability outside of the 03:00-05:00 maintenance window)_

### Service Contacts & Notification Methods

#### Unscheduled or Emergency Maintenance
> Who needs to be advised to issues or incidents for this service or system?

*e.g.*
* The *Customer Care* team (Sydney) is the primary user of this service and needs immediate notification of production-impacting events via email: customer.care@company.com
* Steve in Marketing needs immediate notification of production-impacting events via Slack: @SteveInMarketing
* Phyllis in Finance needs post-resolution notification of production-impacting events via phone: 212-555-1212 x1234

#### Scheduled Maintenance
> Who needs to be advised to upcoming changes or maintenance for this service or system, and how much notice do they need?

*e.g.*
* The *Customer Care* team (Sydney) is the primary user of this service and needs 48 hours advance notice for production-impacting events via email: customer.care@company.com
* Steve in Marketing needs 1 week advanced notification of production-impacting events via Slack: @SteveInMarketing

#### Change Requests
> How should change requests for this system be handled?

_(e.g. Change requests should be sent to Helen Waite via email: HelenWaite@company.com, a card should be created on clubhouse under XXX team, simply create a PR and tag XXXX )_


### Contributing applications, daemons, services, middleware

> Which distinct software applications, daemons, services, etc. make up the service or system? What external/3rd party dependencies does it have?

_(e.g. Ruby app + RabbitMQ for source messages + PostgreSQL for reconciled transactions)_

## System characteristics

### Hours of operation

> During what hours does the service or system actually need to operate? Can portions or features of the system be unavailable at times if needed?

#### Hours of operation

_(e.g. 03:00-01:00 GMT+0)_

#### Requested maintenance window

_(e.g. 01:00-03:00 GMT+0)_

### Data and processing flows

> How and where does data flow through the system? What controls or triggers data flows?

_(e.g. mobile requests / scheduled batch jobs / inbound IoT sensor data )_

### Resilience and Fault Tolerance (FT)

> How is the system resilient to failure? What mechanisms for tolerating faults are implemented? What happens if you can't connect to a 3rd party dependency? What happens if a datastore isn't available?

_(e.g. When redis isn't available, the app won't work, so we serve a 500 error page. If we can't send faxes to phaxio we switch to twilio. )_

### Environmental differences

> What are the main differences between Production/Live and other environments? What kinds of things might therefore not be tested in upstream environments?

_(e.g. Self-signed HTTPS certificates in Pre-Production - certificate expiry may not be detected properly in Production)_

## Monitoring and alerting

### Log message format

> What kind of log message format will be used? Structured logging with JSON? `log4j` style single-line output?

_(e.g. Log messages will use log4j compatible single-line format with wrapped stack traces)_

### Events and error messages

> What significant events, state transitions and error events may be logged?

_(e.g. IDs 1000-1999: Database events; IDs 2000-2999: message bus events; IDs 3000-3999: user-initiated action events; ...)_

### Health check

> How is the health of dependencies (components and systems) assessed? How does the system report its own health? What makes the service healthy aka what actions is the health check performing?

## Operational tasks

### Deployment

> How is the software deployed? How does roll-back happen?

_(e.g. We use GoCD to coordinate deployments, We click )_

### Batch processing

> What kind of batch processing takes place?

_(e.g. Files are pushed via SFTP to the media server. The system processes up to 100 of these per hour on a `cron` schedule)_


### Synthetics (Black box testing)

> What are the key transaction routes?

_(e.g. www.billyspizzany.com must respond in under 500 ms)_

### Troubleshooting

> How should troubleshooting happen? What tools are available? If this service were on fire what would be the first 3 things you would check?

_(e.g. Use a combination of the `/health` endpoint checks and the `abc-*.sh` scripts for diagnosing typical problems)_

## Maintenance tasks

### Data cleardown

> Which data needs to be cleared down? How often? Which tools or scripts control cleardown?

_(e.g. Use `abc-cleardown.ps1` run nightly to clear down the document cache)_
