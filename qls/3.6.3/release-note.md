Release note
============
QLS 3.6.3 release is a patch release made on the top of QLS 3.6.2. As a patch release, QLS 3.6.3 does not bring much new functionality but provides mostly bug fixes and other improvements.

Release also maintains backward compatibility (source and binary; 'server version' >= 'daemon version' >= 'client api library version')
with QLS 3.x.x series.

Some of the changes listed in this file include issue tracking numbers
corresponding to tasks in the Qt Bug Trackers: https://bugreports.qt.io/ and https://jira.qtgroup.qt.io/

Each of these identifiers can be entered in the bug tracker to obtain
more information about a particular change.


Changes in 3.6.3
============

### License-service
- [QLS-2042] Add support for configuring the logs path
- [QTBUG-145601] mocwrapper: fix error instructions pointing to inaccessible bug tracker
- Allow making license reservations via the qtlicensetool
- HttpClient: enable HTTP/2 multiplexing with HTTP/1.1 fallback
- Replace curl_easy with curl_multi in HttpClient
    - This improves performance and resource usage under heavy load, especially with floating license setups
- HttpClient: use CURLOPT_POST for plain POST requests
- HttpClient: fix User-Agent header truncation
- Handle server version request asynchronously
- Publish port file atomically after daemon is fully initialized
- Make daemon startup timeout configurable via QTLICD_STARTUP_TIMEOUT_SECS
- Fix waitServiceStart() to poll the port file while waiting for cip.lock
- [QLS-2469] CIP: Add numeric version to version.h
- Add QTLICD_RUNTIME_DIR and QTLICD_CONFIG_DIR env var support

### License-server
- On-prem:
    * [QLS-2197]: Added an environment variable for configuring the time to wait before retrying a license reservation when no free seats are available
    * [QLS-2472]: Added an /clients endpoint option to retrieve client information in Squish legacy format
    * [QLS-2471]: Made the user_id field optional in the /pre-check/licenses endpoint to return all hosted licenses
    * [QLS-2536]: Added metrics to monitor server performance under high loads
    * Prioritized handling of release requests in the request queue
    * Increased the maximum request queue size from 30,000 to 100,000
- Bug fix:
    * [QLS-2463]: Fixed debug-level logs not being written to the log file
    * [QLS-2512]: Fixed an issue where a request retry would hang in the background after a client disconnected
    * [QLS-2515]: Fixed invalid date and time values in export reports in reporting
    * [QLS-2523]: Fixed incorrect values for free seats and reserved seats in reporting
    * [QLS-2529]: Fixed an issue where held connections in the license retry queue were not bounded
    * [QLS-2533]: On-prem: Fixed an unbounded on-prem database write backlog that could cause out-of-memory errors under load
    * [QLS-2534]: On-prem: Fix database initialization for better throughput (Enable WAL + synchronous=NORMAL)
    * On-prem: Fixed unbounded memory growth in the reservation retry path
