Release note
============
QLS 3.5.0 release is a feature release.
It adds support for leeway time and for noninteractive Qt account login.
It also adds support to download statistics from Rest-API and re-attempt to wait for license

Release also maintains backward compatibility (source and binary; 'server version' >= 'daemon version' >= 'client api library version')
with QLS 3.x.x series.

Some of the changes listed in this file include issue tracking numbers
corresponding to tasks in the Qt Bug Trackers: https://bugreports.qt.io/ and https://jira.qtgroup.qt.io/

Each of these identifiers can be entered in the bug tracker to obtain
more information about a particular change.


Changes in 3.5.0
============

### License-service
- [QLS-1565] Licenser: do not disconnect clients on request to release reservations
- [QLS-1811] LicenseCache: improve error message on unable to acquire lock file
- [QLS-1726] Fix unsafe usage of nlohmann::json const reference operator
- 3rdparty: update used OpenSSL version to 3.5.0
- [QLS-1949] Consider all suitable licenses when looking for a cached reservation
- [QLS-1953] Create subdirectory to store qtlicd log
- [QLS-1937] Add support for proxy settings
- [QLS-1924] Ignore bogus entries in installations.ini file
- [QLS-1950] TcpServer: fix thread safety violations for the internal socket map
    - Fixes a random hang in high concurrency situations
- utils::getTempDir(): use GetTempPath2 when available
- [QLS-1420] Windows: add CMake option for controlling the CRT linkage mode
- [QLS-1936] Reservation: ensure no re-use can occur if leeway time is zero
- [QLS-1725] CIP: add support for retrieving the user of a reservation
- [QLS-1848] Allow leeway time before releasing reservation on client disconnect
- [QLS-1849] Introduce a WatchdogPool class
    - Optimizes usage of system resources when tracking reservation times
- LicensePrecheck: bail early if no components were given for precheck
- Make client libraries respect QTLICD_LOG_LEVEL environment variable
- [QLS-1803] CIP: fix started qtlicd not fully detaching from the parent process
- [QLS-1843] CIP: get rid of the libcrypto dependency
- Watchdog: fix delay in destructor when timer is running
    - This could add unnecessary delay for latency critical client applications, such as moc
- [QLS-1618] CIP: fix nullptr dereference on watchdog timeout during destruction
- [QLS-1607] Fix utils_mac.mm being compiled as CXX, not OBJCXX
- [QLS-1074] TcpServer: bind listening socket to loopback address by default
    - Fixes showing a firewall exception dialog at first startup
- [QLS-601] qtlicensetool: add support for non-interactive Qt account login
- CIP: Fix build as part of other projects (e.g. Qt Creator)

### License-server
- General:
    * [QLS-1434]: Rest-API for download Statistics
- On-prem:
    * [QLS-1918]: Re-attempt to wait for license when the pool is full in on-prem
    * [QLS-1561]: Email notification in on-prem server when license is about to be expired
    * [QLS-1846]: Create log from ACL modifications
- Bug fix:
    * [QLS-1808]: Add missing version string in on-prem configuration files
    * [QLS-1939]: Fix floating reservation renewal when the pool is full
    * [QLS-1963]: Release reservation after long-term record is removed
    * [QLS-1971]: Prevent empty string user_id in long-term records in acl.json
    * [QLS-1780]: Fix missing version and Qt logo in Qt license server executable file
    * [QLS-1969]: Prevent logs folder from being created when Qt license server run as CLI
    * [QLS-1973]: Permission issue occurred when running QLS on CLI
    * [QLS-1972]: Improve misleading error messages
