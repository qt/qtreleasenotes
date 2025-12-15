Release note
============
QLS 3.6.1 release is a patch release made on the top of QLS 3.6.0. As a patch release, QLS 3.6.1 does not bring much new functionality but provides
mostly bug fixes and other improvements.

Release also maintains backward compatibility (source and binary; 'server version' >= 'daemon version' >= 'client api library version')
with QLS 3.x.x series.

Some of the changes listed in this file include issue tracking numbers
corresponding to tasks in the Qt Bug Trackers: https://bugreports.qt.io/ and https://jira.qtgroup.qt.io/

Each of these identifiers can be entered in the bug tracker to obtain
more information about a particular change.


Changes in 3.6.1
============

### License-service
- Linux: close all inherited file descriptors in the detached qtlicd process
- [QLS-2243] QtAccount: store unique user id on login and renewal
- [QLS-2275] RetryManager: limit fallback server usage to whitelisted QLS domains
- [QLS-2267] Fix globals.h missing in some of the release artifacts
- [QLS-2240] macOS: use posix_spawn for safe detached process creation
- [QLS-2240] utils::startDetached: use _Exit() for async-safe termination

### License-server
- [QLS-2244]: Support license registration for deputy manager in QLS on-prem
- [QLS-2300]: Fix QLS uploading license usage to S3 issue
- [QLS-2177]: Fix error message for server CLI and make the promt warning user friendly
