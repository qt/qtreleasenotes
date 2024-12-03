Release note
============
QLS 3.3.0 release is a feature release.
It add's connection between on-premises server and cloud backend to fetch and sync licenses plus export usage data reports to the backend.
It also add's features needed by the Squish.

Release also maintains backward compatibility (source and binary; 'server version' >= 'daemon version' >= 'client api library version')
with QLS 3.x.x series.

Some of the changes listed in this file include issue tracking numbers
corresponding to tasks in the Qt Bug Tracker: https://bugreports.qt.io/

Each of these identifiers can be entered in the bug tracker to obtain
more information about a particular change.


Changes
============

### License-service
Changes in 3.3.0
- [QLS-1439] CIP: retry TCP connection if the port information was changed after initial attempt
- [QLS-1054] CIP: improve error message when no suitable service installation was found
- [QLS-1423] TcpServer: fix missing handling for some socket events
- libcurl: remove dependency to libssh2
- [QLS-1415] Fix issues caused by creating a file lock for the port file
- [QLS-1314] LicenseCache: include daemon version in default cache paths
- [QLS-1281] CIP: do not remove port file if license service process is running
- [QLS-1350] Update libcurl to version 8.10.1
- [QLS-1404] LicenseCache: fix wrong path for reservation files
- [QLS-1347] Send attached consumer properties in renewal request payload
   - This allows the server to decide if a better license has become
     available for any of the consumers
- [QLS-1334] Allow usage of expired perpetual licenses
- [QLS-1306] Windows: make certificate revocation check behavior configurable
   - This also changes the default behavior from strict to best effor check,
     an allowed failure case is when the CRL distribution point is unreachable
- [QLS-1335] Allow using process based reservation for multiple matching clients
- [QLS-1322] Make network request timeout configurable
- Avoid creating a temporary copy of the JsonData in JsonHandler
- Retry renewal request at later time on request errors
- Licenser: fix warning logs for network request errors
- [QLS-1324] Replace "restore server connection" mechanism with individual retries for requests
- Optimize parsing of license and reservation data for better performance
- LicenseCache: print warnings for non-fatal fails on removing directories
- TcpClient: fix confusing error message on graceful socket closing
- [QLS-1321] Optimize license cache flushing for better performance
- Fix renewal event triggering when reservation is already waiting for release
- [QLS-1252] Track consumer usage statistics in milliseconds accuracy
- [QLS-1254] Attach unique consumer applications to reservation
   - This allows retrieving the best possible license for clients that
     have not previously used a cached reservation
- CIP: split StatusCode::BadRequest into more meaningful error enumerators
- [QLS-1311] Fix incomplete usage statistics left hanging in license cache
- macOS: remove obsolete environment variables from service property list
- CMake: set to explicitly look for static OpenSSL libraries
- TcpServer: fix incorrect destruction of the worker thread
- Windows: fix return value check for Winsock functions
- Improve error handling and user visible messages from TcpClient
- [QLS-1303] CIP: allow app configurable retries in case connecting to service socket failed
   - Retries are disabled by default
- [QLS-1304] Fix wrong username in license requests in high concurrency situations
- Licenser: fix dubious condition on network error
- CIP: remove dubious error about not being able to open port file
- [QLS-1272] Fix daemon not shutting down due to TcpServer missing a notify
- Licenser: remove unnecessary disconnection of client on error
- [QLS-1302] Increase the maximum count of simultaneously open file handles on all platforms
- [QLS-1281] TcpServer: fix limitations with select() based socket monitoring
    - This fixes several issues in high concurrency situations, where multiple
      client applications attempt to connect to the service simultaneously
- Windows: remove duplicate parsing of log level environment variable
- [QLS-1277] mocwrapper: suppress output for successful reservation by default
- [QLS-1139] CIP: fix extra quotes in some LicenseReservationInfo values
- [QLS-1262] Fix sending extra parameters to daemon via TCP causing crash
- Windows: add VERSIONINFO resource file for executables

### License-server
- Cloud support:
    * [QLS-1282] Migrate OTF from QLS to license service
    * [QLS-1276] Return a temporary reservation when DB is under maintenance
    * [QLS-1345] Upgrade an existing reservation if a better license is available
    * [QLS-1297] API discovery
    * [QLS_1403] Login and renewJWT API in QLS cloud to support on-prem online mode

- Registration service:
    * [QLS-1292] Create on-prem instance register end-point
    * [QLS-1292] Add license sync feature for on-prem registration service

- On-prem online connectivity:
    * [QLS-1241] Create online mode and offline mode in on-prem QLS instance
    * [QLS-1308] Register licenses for on-prem instance
    * [QLS-1197] Qt Account login to authenticate user
    * [QLS-1317] Store JWT and user credential in cache after login
    * [QLS-1198] Cron job to fetch registered license from Qt cloud
    * [QLS-1244] Cron job to automatically renew login credentials
    * [QLS-1349] [QLS-1295] Cron job to upload usage data to S3
    * [QLS-1247] Deregister licenses from the on-premises usage

- On-prem support:
    * [QLS-1265] Remove default ACL in Access Control management
    * Add QLS prefix for environment variable

- Bug fix:
    * [QLS-1256] Fix: Allow making new reservation for expired perpetual license
    * [QLS-1438] Disk info is missing from fingerprint generation
    * Fix: Accept empty ACL users
    * [QLS-1451] Fix longterm access regression
    * Bug fix: Modify version check to Ignore Patch Level
    * [QLS-1397] Refactor data export logic
