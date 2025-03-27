Release note
============
QLS 3.4.0 release is a feature release.
It adds support for Site and Floating licenses in the QLS cloud including feature to manage license accessbility.
It also adds a feature to configure the passive lease renewal time and new options to easier usage of the license server.


Release also maintains backward compatibility (source and binary; 'server version' >= 'daemon version' >= 'client api library version')
with QLS 3.x.x series.

Some of the changes listed in this file include issue tracking numbers
corresponding to tasks in the Qt Bug Tracker: https://bugreports.qt.io/

Each of these identifiers can be entered in the bug tracker to obtain
more information about a particular change.


Changes in 3.4.0
============

### License-service
* [QLS-1751] Ensure the daemon clears the cache when a server connection is unavailable
- Support qtlicd.ini config migration with the qtlicensetool
* [QLS-1777] CIP: Ensure compatibility with pre 3.4.0 service versions
- [QLS-1753] Fix unconditional renewal of reservations on startup
- CMake: Ensure all libraries are built with -fPIC
- [QLS-1637] Prefer latest minor parser version in unified license JSON parsers
- [QLS-1771] Fix registration of qtlicd if the settings folder does not exist
- [QLS-1659] Fix daemon to correctly read settings containing whitespace within values
- 3rdparty: update curl to version 8.12.1
- [QLS-1731] Fix IniFileParser breaking formatting of the file
- CIP: provide a method to return the string name of a status code
- [QLS-1754] LicenseClient: send -settings-type only for the 'set_settings' operation
- mocwrapper: print string representation of errno on failure to call moc
- [QLS-1755] mocwrapper: return EXIT_FAILURE on errors when invoking moc executable
- [QLS-522] qtlicensetool: fix exit codes on failed operations
- [QLS-1730] Pipe: use condition variable to wait for data instead of polling
    - Fixes excessive CPU usage
- [QLS-1278] Support lease renewal policy from the unified license itself
- [QLS-1749] Require acceptance of Terms & Conditions to use the license service
- Add LICENSES folder and licenseRule.json to adhere to QUIP 18 rules
- [QLS-956] CIP: generate a unique UUID for consumer process ID
- [QLS-1432] Add support for changing the server URL by clients
    - qtlicensetool: add convenience options to get and set the server URL
- [QLS-1743] mocwrapper: treat errors and failures as warnings
- qtlicensetool: fix a crash resulted from constructing std::string from null C string
- [QLS-1662] Collect information about the OS architecture
- [QLS-1512] CIP: add interface for supporting dynamic settings
    - Client applications can now change supported settings of the license service
    - Support changing request_timeout
- [QLS-1655] Use dedicated endpoint for sending execution statistics
- [QLS-1445] Export qlicensecore library for usage by external applications
    - Make LicdSetup and InstallationManager usable by external applications
- [QLS-1532] Support expired perpetual licenses correctly
    - ClientHandler: do not send empty consumer_build_timestamp in requests
- qtlicensetool: fix output for option -r when there are no reservations
- JsonHandler: fix missing details when logging parsing exceptions
- [QLS-1525] Add new client library for installation time license pre-check
- CIP: Split license info related types to separate header
- [QLS-1607] Fix linking binaries built on Xcode 14 and newer on Xcode 13 and older
- [QLS-1456] TcpClient: adjust WinSock2 shutdown and socket closure sequence
    - Fixes errors on some client application disconnections
- [QLS-1471] TcpClient/Server: send protocol capabilities as a message header
    - Enables dynamic buffer size for messages
- [QLS-1445] Create new default settings if settings file does not exist
- [QLS-1279] CIP: add extension API for license check
- Print error log when reservation valid_to and valid_from are not sane

### License-server
- General:
    * [QLS-1532]: Support expired perpetual licenses
    * [QLS-1654]: API for usage upload
    * [QLS-1640]: Support Installation check API in QLS Cloud
- On-prem:
    * [QLS-1475]: Remove IIFE from DB init
    * [QLS-1529]: Refuse to operate the server in online mode if license sync fails
    * [QLS-1455]: Enable Brotli compression in pkg build process
    * [QLS-1449]: Purge reservations when the unified license list is updated
    * [QLS-1746]: Support passive license lease renewal policy
- Bug fix:
    * [QLS-1723]: Calculate license usage correctly in log
    * Fix column name in data export
    * [QLS-1611]: Fix bug that cause the license lease end is shorter than the license expiry date
    * [QLS-1638]: Prevent qt-license-server.service from restarting on-failure (Linux)
    * [QLS-1783]: Fix wrong env variable name and value in qt-license-server.sevice
