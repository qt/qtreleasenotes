Release note
============
QLS 3.6.7 release is a patch release made on the top of QLS 3.6.6. As a patch release, QLS 3.6.7 does not bring much new functionality but provides mostly bug fixes and other improvements.

Release also maintains backward compatibility (source and binary; 'server version' >= 'daemon version' >= 'client api library version')
with QLS 3.x.x series.

Some of the changes listed in this file include issue tracking numbers
corresponding to tasks in the Qt Bug Trackers: https://bugreports.qt.io/ and https://jira.qtgroup.qt.io/

Each of these identifiers can be entered in the bug tracker to obtain
more information about a particular change.


Changes in 3.6.7
============
### License-service
- No functional changes, released together with QLS as a version bump on top of 3.6.6

### License-server
- Build and dependencies:
    * [QLS-2780]: Upgraded Node.js engine from 22.23.4 to 22.23.5 to fix security vulnerabilities (including yao-pkg/pkg-fetch upgrade to 3.6.8)
    * [QLS-2772]: Updated dependencies to fix npm audit issues (including joi and systeminformation)
- Bug fix:
    * Squish: Fix existing floating reservation re-use. It should re-use existing reservation when the parent process
      (e.g. Squish IDE) launches a child process (e.g. Squish Executor) with the same consumer_process_id. Before the fix it resulted in two license seats to be taken.
    * [QLS-2732]: Fixed an empty execution stop time being stored as an invalid date, and logged usage records that are dropped
    * [QLS-2771]: Fixed a force-released expired reservation being recorded twice in the usage logs and data export report
    * [QLS-2777]: On-prem: Fixed the database size not shrinking after data-offload
