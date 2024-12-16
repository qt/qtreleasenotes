Release note
============
QLS 3.3.2 release is a patch release made on the top of QLS 3.3.1.
As a patch release, QLS 3.3.2 does not add any new functionality but provides
bug fixes and other improvements. It also maintains forward and backforward compatibility
with QLS 3.x.x series.

Some of the changes listed in this file include issue tracking numbers
corresponding to tasks in the Qt Bug Tracker: https://bugreports.qt.io/

Each of these identifiers can be entered in the bug tracker to obtain
more information about a particular change.


Changes
============

### License-service
Changes in 3.3.2
- [QLS-1605] mocwrapper: do not repurpose existing options of moc
- [QLS-1576] UsageStatistics: allow leeway in using a completed statistic
- [QLS-1598] mocwrapper: preserve original environment when calling moc
- [QLS-1577] mocwrapper: fix handling of quotes on formation of the command string
- [QLS-1567] mocwrapper: use Qt framework version as the "consumer_version"
- [QLS-1575] TcpClient: fix getting gethostbyname() error details on Unix platforms
- [QLS-1572] Fix cip.lock file descriptor inheritance by qtlicd and close it

### License-server
Changes in 3.3.2:
- Bug fix:
    * [QLS-1601]: Regression: Cannot purge the existing reservations after fetching the licenses from entitlement.json
