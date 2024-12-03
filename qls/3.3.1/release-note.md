Release note
============
QLS 3.3.1 release is a patch release made on the top of QLS 3.3.0.
As a patch release, QLS 3.3.1 does not add any new functionality but provides
bug fixes and other improvements. It also maintains backward compatibility and add's forward compatibility
(source and binary; 'server version' >= 'daemon version' >= 'client api library version')
with QLS 3.x.x series.

Some of the changes listed in this file include issue tracking numbers
corresponding to tasks in the Qt Bug Tracker: https://bugreports.qt.io/

Each of these identifiers can be entered in the bug tracker to obtain
more information about a particular change.


Changes
============

### License-service
Changes in 3.3.1
- [QLS-1456] TcpServer: fix confusing error logging when POLLERR is set
- [QLS-1536] Ensure forward version compatibility of the QLS:
    - Make CIP version compatibility check only for major version range
    - CipCommandParser: allow unknown request parameters
    - Make protocol version compatibility check only for major version range
    - Make installation.ini compatibility check only for major version range
    - LicenseJsonParser: do not remove values from response JSON
- [QLS-1466] CIP: include client library version in TCP messages
- [QLS-1473] Add guard against double release of license
- Do not skip fetching license server version if already fetched
- Fix incorrect message for ServiceVersionTooNew status code

### License-server
Changes in 3.3.1:
- Bug fix:
    * [QLS-1531]: Disable service version check in minor level to support forward compatibility
    * [QLS-1535]: The server must not throw error if the entitlement.json contains new attributes it does not recognize
    * [QLS-1555]: Allow unknown field to be include in reservation/extension response payload
    * [QLS-1460]: Disable data export feature in online mode
    * [QLS-1499]: Limit route usage for online connectivity
    * [QLS-1507]: Fix service installation script for QLS linux
