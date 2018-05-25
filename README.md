# CSCum05372
ACS activity logs show no new content following upgrade to 5.5


## Symptom:
ACS activity logs (RADIUS and TACACS+ authentication, accounting, authorization) show no new content.

## Conditions:
This is observed after upgrading to ACS 5.5.

## Workaround:
Stop and restart the log collector, using the following command:
```
# acs stop view-collector
```
Monitor the status of the ACS application and wait until the view process has stopped:
```
# show app status acs

ACS role: PRIMARY

Process 'database' running
Process 'management' running
Process 'runtime' running
Process 'adclient' running
Process 'ntpd' running
Process 'view-database' running
Process 'view-jobmanager' running
Process 'view-alertmanager' running
Process 'view-collector' not monitored
Process 'view-logprocessor' not monitored
```
Then restart the log collector:
```
# acs start view-collector
# acs start view-logprocessor
```
Then wait until all of the services are running, and verify that activity is being logged.
```
# show app status acs

ACS role: PRIMARY

Process 'database' running
Process 'management' running
Process 'runtime' running
Process 'adclient' running
Process 'ntpd' running
Process 'view-database' running
Process 'view-jobmanager' running
Process 'view-alertmanager' running
Process 'view-collector' running
Process 'view-logprocessor' running
```
