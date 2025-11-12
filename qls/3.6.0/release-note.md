Release note
============
QLS 3.6.0 release is a feature release.
It adds new following features:
  - Local Report Storage: Keep local copies of license usage reports for easier access and backup.
  - Optimized Performance for Floating Licenses: High-concurrency license usage is now handled more efficiently, improving performance under heavy loads.
  - Email Notifications for Lost Connections: Configure an SMTP server with On-Prem Server to automatically send notifications when the connection to the Qt Cloud is lost
  - Interactive License Registration: Prompt for credentials interactively if not provided and warn when insecure (HTTP) connections are used.
  - Enhanced Offline License Usage Reports: Reports now include Consumer auxiliary info and Name fields and exported reports cover all record types.
  - New REST API Endpoints: Query current license pool utilization and active users for easier integration with external systems.
  - IPv6 Support: Local TCP connections between client applications and Qt License Service now support IPv6.
  - Log File Rotation: Limit log file size automatically, new log files are created when the maximum size is reached
  - Automatic Qt Account Login Renewal: Automatically refreshes Qt Account credentials with a configurable renewal interval.
  - Error Reporting for License Reservation Failures: Qt License Service provides clearer diagnostics when license reservations fail.
  - Telemetry Configuration via CLI: Update telemetry preferences directly through the Qt License Service command-line interface.


Release also maintains backward compatibility (source and binary; 'server version' >= 'daemon version' >= 'client api library version')
with QLS 3.x.x series.

Some of the changes listed in this file include issue tracking numbers
corresponding to tasks in the Qt Bug Trackers: https://bugreports.qt.io/ and https://jira.qtgroup.qt.io/

Each of these identifiers can be entered in the bug tracker to obtain
more information about a particular change.


Changes in 3.6.0
============

### License-service
- CIP: fix leaving of zombie processes on Linux and macOS
- [QLS-1998] Fix dynamic libcrypto dependency in Windows on ARM binaries
- [QLS-2172] Fix Visual Studio 16 2019 binaries built on wrong VS version
- Fix potential nullptr dereference on retrieving user's home directory
- [QLS-2168] Add IPv4/IPv6 address prioritization for client connections
- [QLS-2112] 3rdparty: update OpenSSL version to 3.5.4
- [QLS-1520] Improve user visible error messages
- [QLS-2075] Windows: create a static and dynamic CRT variant of all build artifacts
- [QLS-2156] QtAccount: consider user to be logged in if JWT is found
- [QLS-2112] 3rdparty: update curl to version 8.14.1
- [QLS-2153] Improve request retry handling with structured rule and state management
- [QLS-359] Implement file size based log rotation
- [QLS-1958] qtlicensetool: add cli option for updating the telemetry preference
- [QLS-683] TcpClient/Server: add support for IPv6 local connectivity
- [QLS-2037] Allow configuring the on-demand service shutdown timeout by applications
- [QLS-1727] Include all supported consumers of a license in reservation response
- [QLS-2083] Do not allow authentication or login renewal over plain HTTP
- [QLS-2059] Pass detailed reservation error report from server to applications
- [QLS-1922] Add additional binaries of the client library for CentOS 7 x86
- [QLS-2011] QtAccount: improve error message when attempting login over plain HTTP
- [QLS-1934] Fix service being blocked on startup with internal only network
- [QLS-2053] Refactor the core architecture of the service into more cohesive subsystems
- HttpClient: hide potentially sensitive information from raw request debug logs
- [QLS-1767] Add support for periodical renew of logins for cached Qt Accounts
- TcpClient: guard against dereference of hostent with no useful addresses
- [QLS-1628] TcpClient/Server: retry interrupted POSIX syscalls
- [QTCREATORBUG-33157] LockFile: create missing leading directories for the lock file
- [QLS-1932] Provide license information API from precheck library also in CIP
- [QLS-1957] Add a way to disable all telemetry that requires consent
- [QLS-1651] Add support for auxiliary product metadata in license requests
- CIP: do not purge installations when checking if service is available
- [QLS-1562] qtlicensetool: add option for renewing license reservations
- [QLS-1522] Add additional binaries for MSVC 2015

### License-server
- General:
    * [QLS-1651]: Add 'consumer_auxiliary_info' field to logs table
    * [QLS-2030]: Improve error reporting in case of license reservation failures
    * [QTBSI-2913]: Improve fault tolerance of logs backup process
    * [QLS-2052]: Add optional pagination for /usage-downloads end-point
    * [QLS-2058]: Fix and optimize node-locked license filtering
- On-prem:
    * [QLS-1790]: Optimize reservation process on QLS on-prem for floating licenses
    * [QLS-2015]: Add an option to keep reports on the local disk after the upload is completed
    * [QLS-2013]: Prompt the credentials query if it is not presented in the register command
    * [QLS-2065]: Add a "Name" field to statistics report
    * [QLS-1979]: Handle all possible HTTP errors for CLI commands
    * [QLS-1859]: Notify user about security risk when the user makes a registration request via insecure HTTP
    * [QLS-1729]: Enable sending email notifications when the server connection to Qt cloud is lost
    * [QLS-2048]: Introduce license user endpoint to acquire information about who are currently consuming a license
    * [QLS-2019]: Introduce license usage statistics endpoint to acquire information about current license usage
    * Remove --recordType option from data export command
- Bug fix:
    * [QLS-1980]: Fix database initialization during server startup
    * [QLS-2016]: Improve system logs when there is an issue with registering licenses in connected mode
