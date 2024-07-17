### Document: Managing Citrix Log Files with nsconmsg

This document outlines the procedures for managing and analyzing Citrix log files using various commands. Each command is explained to help understand its purpose and usage.

#### Uncompress an Archived Log File

To uncompress a compressed log file, use the following command:
```bash
gunzip newnslog.21.gz
```
This command decompresses the file `newnslog.21.gz` to `newnslog.21`.

#### Discover the Time Period Covered by the Log

To find out the time period covered by a specific log file:
```bash
nsconmsg -K newnslog.21 –d setime
```
This command provides the start and end times of the log `newnslog.21`.

#### View Load-Balancing Statistics from the Archived Log

To view load-balancing statistics:
```bash
nsconmsg -K newnslog.21 -s ConLb=2 -d oldconmsg
```
This command extracts and displays detailed load-balancing statistics from the archived log file `newnslog.21`.

#### Extract Logging Information for a Shorter Duration

To extract logs for a specific time period:
```bash
nsconmsg -K newnslog.21 -s time=12Jan2006:00:00 -k short_log.nsl -T 1200 -d copy
```
This command extracts logs starting from `12 Jan 2006 00:00` for a duration of 1200 seconds and saves them to `short_log.nsl`.

#### Start the Log Process for newnslog

To start logging for the `newnslog` file:
```bash
nsconmsg -k /var/nslog/newnslog -T 172800 &
```
This command starts the logging process for `newnslog` and continues for 172800 seconds (2 days).

### Viewing Various Log Details

#### View the Time Span of the Current newnslog File

```bash
nsconmsg -K newnslog -d setime
```
Displays the time span of the current `newnslog` file.

#### View the Time Span of the Archived newnslog File

```bash
zcat filename | nsconmsg -K pipe -d setime
```
Uncompresses the archived log file and displays its time span.

#### View Events in the Current newnslog File

```bash
nsconmsg -K newnslog -d event
```
Displays events recorded in the current `newnslog` file.

#### View Console Messages in the Current newnslog File

```bash
nsconmsg -K newnslog -d consmsg
```
Displays console messages from the current `newnslog` file.

#### View Counter Values in the Current newnslog File

```bash
nsconmsg -K newnslog -d stats
```
Displays all counter values.

```bash
nsconmsg -K newnslog -d stats –d current
```
Displays current counter values.

#### View Non-Zero Counter Values in the Current newnslog File

```bash
nsconmsg -K newnslog -d statswt0 –d current
```
Displays non-zero counter values.

### Display Specific Event Information

#### Display Event Information

```bash
nsconmsg -K newnslog -d event
```
Shows events such as entity up/down, alerts, and configuration saves.

#### Display CPU Usage

```bash
nsconmsg -K newnslog -s totalcount=200 -g cpu_use -d current
```
Displays CPU usage information.

#### Display Memory Utilization

```bash
nsconmsg -s ConMEM=1 -d oldconmsg
```
Shows memory utilization.

#### Display Established HTTP Connections

```bash
nsconmsg -j server_NSSVC_HTTP_vserver -d current
```
Displays information about established HTTP connections.

#### Display Load-Balancing Statistics

```bash
nsconmsg -K newnslog –s ConLb=x –d oldconmsg
```
Displays load-balancing statistics, with `x=1` for basic information and `x=2` for detailed information.

#### View Traffic Distribution

```bash
nsconmsg -K /var/nslog/newnslog -s time -s ConLB=2 -2 distrconmsg
```
Shows traffic distribution information.

#### Display Monitoring Statistics

```bash
nsconmsg -K newnslog –s ConMon=x –d oldconmsg
```
Displays monitoring statistics, with `x=1` for basic and `x=2` for detailed information.

### SSL Statistics

#### View SSL Stats for Front-End Connections

```bash
nsconmsg -K newnslog -s ConSSL=1 -d oldconmsg
```
Displays SSL statistics for front-end connections.

#### View SSL Stats for Back-End Connections

```bash
nsconmsg -K newnslog -s ConSSL=2 -d oldconmsg
```
Displays SSL statistics for back-end connections.

#### View SSL Stats for Both Front and Back-End Connections

```bash
nsconmsg -K newnslog -s ConSSL=3 -d oldconmsg
```
Displays SSL statistics for both front and back-end connections.

### Other Statistics

#### Display Content Switching Statistics

```bash
nsconmsg -K newnslog –s ConCSW=1 -d oldconmsg
```
Displays content switching statistics.

#### Display Compression Statistics

```bash
nsconmsg -K newnslog –s ConCMP=x -d oldconmsg
```
Displays compression statistics, with `x=1` for old method and `x=2` for new method statistics.

#### Display Integrated Caching Statistics

```bash
nsconmsg -K newnslog -s ConIC=1 -d oldconmsg
```
Displays integrated caching statistics.

By following these commands, you can efficiently manage and analyze Citrix log files to troubleshoot and monitor your Citrix environment.
