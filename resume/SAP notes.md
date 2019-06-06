[Performance Testing for SAP Applications](https://www.worksoft.com/performance-testing-sap-applications/)

**Performance testing** is the process of measuring and tuning the system’s user response time and transaction throughput under normal load conditions. 

**Load testing** is the introduction of varying levels and profiles of demand to pinpoint potential bottlenecks. 

**Stress testing** is the application of extreme demand to uncover breaking points and observe the system’s ability to handle failure.



why performance test:

- Before going “live”, you need to test the behavior of the SAP application under real-world workload scenarios. 
- You need to uncover performance issues that will only surface when a realistic and adequate workload is placed on the application.
- You need to understand the capacity of the application – its limits and thresholds.
- You may need to fine tune the application and its underlying infrastructure based on these performance characteristics (e.g. hardware, storage, etc.).



These factors include:

- inaccurate volume/sizing estimates, 
- undefined operational profiles, 
- poorly written custom transactions, 
- an un-tuned database, 
- mis-configured SAP landscape, 
- inaccurate hardware sizing, and so forth.



[5 CHALLENGES ASSOCIATED WITH PERFORMANCE TESTING AN SAP APPLICATION](https://www.neotys.com/blog/challenges-performance-testing-sap-application/)

- Test data availability
- Use case description accuracy
- Test infrastructure size
- SAP Basis team interaction
- Capacity management



[SAP Monitoring & Performance Checks: Complete Tutorial with Tcodes](https://www.guru99.com/system-monitoring-performance-checks.html)

Checking Application Servers (SM51)

Monitoring Work Processes for Individual Instances SM50

Monitoring System-wide Work Processes (SM66)

Monitor Application User (AL08 and SM04)

Monitoring Update Processes (SM13)

Monitoring Lock Entries (SM12)

Monitoring System Log (SM21)

Tune Summary (ST02)

CPU Utilization (ST06)

ABAP Dumps (ST22)

Spool Request Monitoring (SP01)

Monitoring Batch Jobs (SM37)

Transactional RFC Administration (SM58)

Database Administration (DB02)



Daily Monitoring Tasks

1. Critical tasks
2. SAP System
3. Database



**Critical tasks**

| **No** | **Task**                                        | **Transaction** | **Procedure / Remark**  |
| :----- | :---------------------------------------------- | :-------------- | :---------------------- |
| 1      | Check that the R/3System is up.                 |                 | Log onto the R/3 System |
| 2      | Check that daily backup executed without errors | DB12            | Check database backup.  |

**SAP System**

| **No** | **Task**                                         | **Transaction** | **Procedure / Remark**                                       |
| :----- | :----------------------------------------------- | :-------------- | :----------------------------------------------------------- |
| 1      | Check that all application servers are up.       | SM51            | Check that all servers are up.                               |
| 2      | Check work processes (started from SM51).        | SM50            | All work processes with a “running” or a “waiting” status    |
| 3      | Global Work Process overview                     | SM66            | Check no work process is running more than 1800 second       |
| 3      | Look for any failed updates (update terminates). | SM13            | Set date to one day agoEnter * in the user IDSet to “all” updates Check for lines with “Err.” |
| 4      | Check system log.                                | SM21            | Set date and time to before the last log review. Check for:ErrorsWarningsSecurity messagesDatabase problems |
| 5      | Review for canceled jobs.                        | SM37            | Enter an asterisk (*) in User ID.Verify that all critical jobs were successful. |
| 6      | Check for “old” locks.                           | SM12            | Enter an asterisk (*) for the user ID.                       |
| 7      | Check for users on the system.                   | SM04AL08        | Review for an unknown or different user ID and terminal.This task should be done several times a day. |
| 8      | Check for spool problems.                        | SP01            | Enter an asterisk (*) for Created ByLook for spool jobs that have been “In process” for over an hour. |
| 9      | Check job log                                    | SM37            | Check for:New jobsIncorrect jobs                             |
| 10     | Review and resolve dumps.                        | ST22            | Look for an excessive number of dumps. Look for dumps of an unusual nature. |
| 11     | Review buffer statistics.                        | ST02            | Look for swaps.                                              |

**Database**

| **No** | **Task**                       | **Transaction** | **Procedure /  Remark**                                      |
| :----- | :----------------------------- | :-------------- | :----------------------------------------------------------- |
| 1      | Review error log for problems. | ST04            |                                                              |
| 2      | Database GrowthMissing Indexes | DB02            | If tablespace is used more than 90 % add new data file to itRebuild the Missing Indexes |
| 3      | Database Statistics log        | DB13            |                                                              |