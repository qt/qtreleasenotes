Release note
============
QLS 3.6.5 release is a patch release made on the top of QLS 3.6.4. As a patch release, QLS 3.6.5 does not bring much new functionality but provides mostly bug fixes and other improvements.

Release also maintains backward compatibility (source and binary; 'server version' >= 'daemon version' >= 'client api library version')
with QLS 3.x.x series.

Some of the changes listed in this file include issue tracking numbers
corresponding to tasks in the Qt Bug Trackers: https://bugreports.qt.io/ and https://jira.qtgroup.qt.io/

Each of these identifiers can be entered in the bug tracker to obtain
more information about a particular change.


Changes in 3.6.5
============
### License-service
- Fix qtlicd.ini corruption when new keys are written to a file that carries
  a [/QtLicenseDaemon] closing tag
- Start the license service without a registration of one's own
    - The client tools now also look for qtlicd(.exe) in the directory they were started from.
      The installations.ini file still takes precedence.
    - New QTLICD_INSTALL_DIR names the directory to start the service from, taking
      precedence over both.
    - New QTLICD_NO_EXEDIR_FALLBACK=1 restores the previous behaviour of using only
      installations.ini
    - A service reached through a symbolic link is registered under the binary it points
      at. An entry an earlier release made under the link is replaced on --register,
      and found by --unregister
- Seed a new qtlicd.ini from the one next to the service executable
    - A second user of a shared installation gets the server address configured for that
      installation, instead of silently falling back to the Qt hosted server
    - The shipped defaults are written first and the installation's values laid over them,
      so a setting the installation's file does not mention keeps its default instead of
      being left empty
- 3rdparty: update used OpenSSL version to 3.5.7
- [UTAC-1282] Fix handling of user names carrying special characters
    - A user name rejected by the license server is now reported as such, instead of
      as a generic invalid request telling the user to contact Qt Support
    - A user name that cannot be carried by a request is refused with the reason,
      instead of being silently truncated on the way to the license service
        - This rejects abnormal user names that were accepted before: one starting with a
          dash, containing a space followed by a dash, starting or ending with
          whitespace, or containing a control character. Adjust the account name,
          or QTLICD_CLIENT_USERNAME, if a license request starts failing for it
    - A dash inside a request value, such as the one in a domain-qualified account name,
      is no longer taken for the start of a request parameter.
    - Licenses cached for a user whose name carries a path separator, such as a
      domain-qualified account name, are no longer lost on restart
    - A user name that is not valid UTF-8 is refused instead of terminating the
      license service when the request payload is serialized
- Add support for releasing a single license reservation by its id
    - New CIP API method ILicenseClient::releaseReservation(), and an optional
      reservation id argument for the existing "qtlicensetool -c" option
- Release the reservations from the license server when the license cache is cleared
    - "qtlicensetool -c" asks the license server to release each cached reservation
    - The license server decides whether a reservation is actually released. The local
      cache is cleared in any case, also when the server cannot be reached
- Speed up the release of many reservations at once
    - Tearing down a reservation no longer scans every connected client, so a mass
      release no longer slows down quadratically with the number of clients
- Reserve in-flight request slots for license releases
    - Fixes a stall during which no license is granted, when a burst of client requests
      occupies every outbound slot and the releases that would free the seats cannot get through
- mocwrapper: fix a failing qtmoc being reported as success on Windows
    - Build tools such as ninja or make can now detect a failed qtmoc invocation
- [QLS-2530] Distinguish the license server seat wait re-poll from other 503 responses
    - A reservation waiting for a free seat is re-polled immediately instead of on the
      retry back-off ramp
- Throttle outbound requests to the license server and rework the retry ladder
    - Fixes reservations failing in bulk when thousands of clients start at the same time
    - request_timeout now bounds the whole request instead of a single transfer, and
      its default changed from 15 to 120 seconds
    - Busy or unreachable server responses are retried until the request budget runs
      out, instead of giving up after roughly nine seconds
    - HTTP 429 is now retried, honouring the Retry-After header
    - The fallback server is no longer contacted when the primary answers with a busy signal
    - Retry delays are randomised, so fleets of daemons no longer retry in synchronised waves
    - New settings outbound_max_in_flight, outbound_request_rate, outbound_request_burst,
      attempt_timeout_cap and queue_steady_retry_interval, each with a matching QTLICD_*
      environment override
- Experimental qtlicensetool option to manage throttling parameters
    - "qtlicensetool --profile=<default|medium-concurrency|high-concurrency>" stores
      preset values for outbound_max_in_flight, outbound_request_rate,
      outbound_request_burst and request_timeout
    - The outbound throttling settings take effect when the license service starts the
      next time, and can now also be stored with "qtlicensetool --settings set"
- CIP: fail fast on connection failures caused by exhausted local resources
- Drop half-open license server connections after 60s of unacknowledged data
    - Configurable with QTLICD_TCP_USER_TIMEOUT_SECS
- Cancel a client's pending license server reservation when the client disconnects
- CIP: ride out a service handoff instead of failing the connection
- Keep the port file published until the service lock is released
    - Fixes "Not able to get the TCP port for license service" while an instance is
      shutting down
- Warn while system memory runs low, before the OOM killer strikes
    - Threshold configurable with QTLICD_LOW_MEM_THRESHOLD_LIMIT
- Report file descriptor usage in the service heartbeat and warn near the limit
- Handle thread-creation failure without aborting or zombifying
    - Client applications no longer terminate when the host runs out of threads
- Explain socket exhaustion in user-facing terms with mitigation hints
- [QLS-2628] Allocate license server request ids collision-safely
- [QLS-2627] Always answer the client when its request cannot be dispatched
    - Adds status code MaxClientCountReached (1001), reported instead of leaving the
      client waiting
- [QLS-2626] Bound control-plane license server requests and detect dead connections
- [QLS-2625] Make service health observable: PID per log line, load heartbeat
- [QLS-2624] Survive the on-demand startup herd without crashing instances
- [QLS-2623] Order the on-demand shutdown so clients can fail over cleanly
    - Adds status code ServiceShuttingDown (220) for requests received during shutdown
- [QLS-2622] Do not idle-shutdown the on-demand service under live connections
- [QLS-2621] Scale the TCP event loop to storm-size connection counts
- [QLS-2620] TcpServer: make replies to clients non-blocking
    - Fixes an unresponsive client stalling the service for all other clients
    - QTLICD_SEND_TIMEOUT_SECS is renamed to QTLICD_SEND_CLIENT_TIMEOUT_SECS
- [QLS-2618] TcpServer: bound replies to clients with a timeout

### License-server
- On-prem:
    * [QLS-2662]: Bounded the reserve wait under heavy load and returned 503 (server_busy) instead of accumulating connections; added configurable HTTP socket timeouts
    * [QLS-2662]: Reduced per-request cost of reservations under heavy load and raised the TCP listen backlog
    * [QLS-2662]: Added a periodic diagnostic heartbeat log with an adaptive interval
    * [QLS-2530]: Replaced floating-license polling retry with event-driven seat hand-off that preserves the waiting order
    * [QLS-2668]: Added QLS_SEAT_WAIT_WINDOW and QLS_PROXY_IDLE_TIMEOUT; QLS_WAIT_FREE_SEAT_TIME is deprecated
    * Added a "Wait time (seconds)" column to the Logs sheet of the usage report showing how long a client waited for its license (floating license)
    * [QLS-2553]: Added a per-reservation device limit for site and named licenses
    * [QLS-2553]: Listed all hardware IDs of a reservation in the reports
    * [QLS-2519]: Widened the accepted user_id character set
    * Returned the specific response code invalid_user_id (1002) for an invalid user_id
    * [QLS-2704]: Normalized Qt Account email to lowercase
    * Improved the CLI warning message when switching the user
    * [QLS-2522]: Disabled stdout/stderr log files for qt-service.exe on Windows
- Build and dependencies:
    * [QLS-2712]: Updated dependencies to fix npm audit issues (including uuid, sqlite3, exceljs and newrelic)
- Bug fix:
    * [QLS-2698]: Fixed on-prem registration not recovering when the cloud is unreachable at startup
    * [QLS-2596]: Fixed QLS not warning about expired licenses in the license file
    * [QLS-2343]: Fixed email values not being substituted in the error message
