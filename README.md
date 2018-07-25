# WorkloadTools

*WorkloadTools is a collection of tools to collect, analyze and replay workloads on a SQL Server instance.*

SqlWorkload is a command line tool to start workload collection, analyze the collected data and replay the workload to a target machine, all in REALTIME.

## Command line switches

`--ListenerType` `SqlTraceWorkloadListener | ProfilerWorkloadListener | ExtendedEventsWorkloadListener` Listener type. 

`--Source` Path to the source of the workload capture. Can be a trace definition (`Listener\Trace\sqlworkload.tdf`), a trace script (`Listener\Trace\sqlworkload.sql`) or an Extended Events session creation script (`Listener\ExtendedEvents\sqlworkload.sql`)

`--SourceServerName` Name of the source SQL Server instance

`--SourceUserName` User name to connect to SQL Server with SQL authentication. Will use Windows authentication if empty or missing.

`--SourcePassword` Password

`--TargetServerName` Name of the target SQL Server instance. If omitted, no replay will be performed. 

`--TargetUserName` User name to connect to SQL Server with SQL authentication. Will use Windows authentication if empty or missing.

`--TargetPassword` Password

`--ApplicationFilter` Name of a single application to filter. Prepend the "^" character to exclude the value (e.g. "^sqlcmd.exe" excludes sqlcmd.exe)

`--DatabaseFilter` Name of a single database to filter. Prepend the "^" character to exclude the value.

`--HostFilter` Name of a single host to filter. Prepend the "^" character to exclude the value.

`--LoginFilter` Name of a single login to filter. Prepend the "^" character to exclude the value.

`--StatsServer` Name of the SQL Server instance to use to log the statistics. If omitted, no workload analysis will be performed.

`--StatsDatabase` Name of the database to store the statistics

`--StatsSchema` Name of the schema to store the statistics. If missing, the schema will be created.

`--StatsInterval` Interval in minutes between each dump of the workload statistics

`--StatsUserName` Username to authenticate to the statistics database 

`--StatsPassword` Password to authenticate to the statistics database

## Example

```text
SqlWorkload.exe --ListenerType SqlTraceWorkloadListener --Source Listener\Trace\sqlworkload.sql --SourceServerName SQLDEMO\SQL2014 --SourceUserName sa --SourcePassword P4$$w0rd! --TargetServerName SQLDEMO\SQL2016 --TargetUserName sa --TargetPassword P4$$w0rd! --DatabaseFilter DS3 --StatsServer SQLDEMO\SQL2014 --StatsDatabase RTR --StatsInterval 1 --StatsUserName sa --StatsPassword P4$$w0rd!
```

## Screenshots

Here are some screenshots of the PowerBI report included with the tool. It can be hooked to the statistics database via Direct Query

### Overview of the analysis

The top filters can be used to restrict the analysis to a particular database  or application or host name.

The time slicer can filter the charts to a particular date.

![SqlWorkload analysis Overview](./Images/SqlWorkloadOverview.png "Overview")

### Regressed Queries

This table shows the queries that have regressed in the replay compared to the baseline.

![SqlWorkload regressed queries](./Images/SqlWorkloadRegresses.png "RegressedQueries")

### Regressed Queries

Drilling on one the regressed queries will bring you to the query detail page, where you can see the text of the query (but not copy it to the clipboard - thanks PowerBI) and the stats broken down by application name, database name, host name and login name.

![SqlWorkload query detail](./Images/SqlWorkloadDetail.png "Detail")