Release note
============
QLS 3.6.2 release is a patch release made on the top of QLS 3.6.1. As a patch release, QLS 3.6.2 does not bring much new functionality but provides
mostly bug fixes and other improvements.

Release also maintains backward compatibility (source and binary; 'server version' >= 'daemon version' >= 'client api library version')
with QLS 3.x.x series.

Some of the changes listed in this file include issue tracking numbers
corresponding to tasks in the Qt Bug Trackers: https://bugreports.qt.io/ and https://jira.qtgroup.qt.io/

Each of these identifiers can be entered in the bug tracker to obtain
more information about a particular change.


Changes in 3.6.2
============

### License-service
- [QLS-2394] CIP: Add support for connecting to daemon from inside a docker container
- [QLS-2435] CIP: allow expressing preferred share policy for cached reservation
- [QLS-2395] Fix home directory resolution in sandboxed environment
- [QLS-2392] CIP: include version.h in client library artifacts
- [QLS-2338] CIP: support cached licenses for 'listLicenses' operation
- [QLS-2344] InstallationManager: unregister installations with case insensitive path
- [QLS-2344] IniFileParser: add support for case insensitive mode

### License-server
- [QLS-2434] Stabilize disk selection when generating hardware fingerprint
- [QLS-2444] Fix /api/v2/status reports utilization_rate calculation
