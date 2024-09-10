Release note
============
QLS 3.2.1 release is a patch release made on the top of QLS 3.2.0.
As a patch release, QLS 3.2.1 does not add any new functionality but provides
bug fixes and other improvements. It also maintains backward compatibility
(source and binary; 'server version' >= 'daemon version' >= 'client api library version')
with QLS 3.x.x series.

Some of the changes listed in this file include issue tracking numbers
corresponding to tasks in the Qt Bug Tracker: https://bugreports.qt.io/

Each of these identifiers can be entered in the bug tracker to obtain
more information about a particular change.


Changes
============

### License-service
- [QTBUG-128491] Utils: fix startDetached() not detaching child process properly
    - This caused mocwrapper to hang when building with CMake
- [QLS-1023] Fix invalid SSL CA path on openSUSE
    - This caused network requests, and thus license reservations to fail
- [QLS-1067] Ask operating system for TCP port instead of searching for a free one
    - This may have caused false alarms with virus scanners
- [QLS-1039] Improve error message details on TCP socket related errors
- [QLS-1182] Fix repeating print of search path when importing local licenses
- Improve default logging level messages related to license reservation
- Logger: fix null characters ending up printed to the log file
- [QLS-1064] CIP: fix dubious prints about not being able to open log file
- [QLS-1144] CIP: add separate client status codes for SSL related errors
- [QLS-1218] CIP: add support for revoking current license
- CIP: Use same count of max tries for waiting and starting the service
- CIP: Fix error message about not being able to remove non-existent port file
- [QLS-1209] mocwrapper: improve user visible messages
- [QLS-1217] [QLS-1250] mocwrapper: add fallback mechanism for license check
    - This can be enabled in case the primary license reservation mechanism fails
- [QLS-1208] qtlicensetool: add support for clearing local reservation cache
    - A workaround until the server is able to automatically switch to a better
      version of the same license if such becomes available for the user
- tools: fix missing build date and revision SHA in binaries

### License-server
- [QLS-1107] Fixed ACL management issues
- [QLS-1114] Data export returns invalid data
