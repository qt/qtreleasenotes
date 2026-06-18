Release note
============
QLS 3.6.4 release is a patch release made on the top of QLS 3.6.3. As a patch release, QLS 3.6.4 does not bring much new functionality but provides mostly bug fixes and other improvements.

Release also maintains backward compatibility (source and binary; 'server version' >= 'daemon version' >= 'client api library version')
with QLS 3.x.x series.

Some of the changes listed in this file include issue tracking numbers
corresponding to tasks in the Qt Bug Trackers: https://bugreports.qt.io/ and https://jira.qtgroup.qt.io/

Each of these identifiers can be entered in the bug tracker to obtain
more information about a particular change.


Changes in 3.6.4
============

### License-server
- Bug fix:
    * Fix backward compatibility of hardware fingerprint
    * [QLS-2561]: Fix: Convert license object into readable string
