Release notes
=============
Qt 6.11.3 release is a patch release made on the top of Qt 6.11.2.
As a patch release, Qt 6.11.3 does not add any new functionality but provides
bug fixes and other improvements and maintains both forward and backward
compatibility (source and binary) with the 6.11.x series.

For detailed information about Qt 6.11, refer to the online documentation
included in this distribution. The documentation is also available online:

https://doc.qt.io/qt-6/index.html

The Qt version 6.11 series is binary compatible with the 6.10.x series.
Applications compiled for 6.10 will continue to run with 6.11.

Some of the changes listed in this file include issue tracking numbers
corresponding to tasks in the Qt Bug Tracker:

https://qt-project.atlassian.net/

Each of these identifiers can be entered in the bug tracker to obtain
more information about a particular change.

To make it easier to port to Qt 6, we have created a porting guide to
summarize what changed between Qt 5 and Qt 6 and provide guidance on how to
adapt to those changes. In the guide, you can find links to articles about
changes that may affect your application and help you transition from Qt
5.15 to Qt 6:

https://doc.qt.io/qt-6/portingguide.html


Important Changes
-----------------
### Security fixes
* [CVE-2026-82292](https://nvd.nist.gov/vuln/detail/CVE-2026-82292) in qtbase
* [CVE-2026-95620](https://nvd.nist.gov/vuln/detail/CVE-2026-95620) in qtbase
* [CVE-2026-96432](https://nvd.nist.gov/vuln/detail/CVE-2026-96432) in qtbase
* [CVE-2026-97845](https://nvd.nist.gov/vuln/detail/CVE-2026-97845) in qt5compat
* [CVE-2026-100140](https://nvd.nist.gov/vuln/detail/CVE-2026-100140) in qt5compat
* [CVE-2026-101201](https://nvd.nist.gov/vuln/detail/CVE-2026-101201) in qt5compat
* [CVE-2026-103645](https://nvd.nist.gov/vuln/detail/CVE-2026-103645) in qt5compat
* [CVE-2026-103653](https://nvd.nist.gov/vuln/detail/CVE-2026-103653) in qtcoap
* [CVE-2026-105923](https://nvd.nist.gov/vuln/detail/CVE-2026-105923) in qtbase
* [CVE-2026-105924](https://nvd.nist.gov/vuln/detail/CVE-2026-105924) in qtbase
* [CVE-2026-105925](https://nvd.nist.gov/vuln/detail/CVE-2026-105925) in qt5compat
* [CVE-2026-105939](https://nvd.nist.gov/vuln/detail/CVE-2026-105939) in qtwebsockets
* [CVE-2026-107457](https://nvd.nist.gov/vuln/detail/CVE-2026-107457) in qtmqtt
* [CVE-2026-107472](https://nvd.nist.gov/vuln/detail/CVE-2026-107472) in qt5compat
* [CVE-2026-107479](https://nvd.nist.gov/vuln/detail/CVE-2026-107479) in qt5compat
* [CVE-2026-107590](https://nvd.nist.gov/vuln/detail/CVE-2026-107590) in qt5compat
* [CVE-2026-108081](https://nvd.nist.gov/vuln/detail/CVE-2026-108081) in qtbase
* [CVE-2026-110944](https://nvd.nist.gov/vuln/detail/CVE-2026-110944) in qthttpserver
* [CVE-2026-111487](https://nvd.nist.gov/vuln/detail/CVE-2026-111487) in qt3d
* [CVE-2026-114366](https://nvd.nist.gov/vuln/detail/CVE-2026-114366) in qtwebsockets

### qtbase
* 8f376c89b21 qpa/wayland: Only enable text-input-v3 surfaces when
  needed
    * Make it so that surfaces under text-input-v3 are only enabled if
      they are entered and want to receive text input.

* 35e0ebb5fae QNetworkInfo[android]: Advertise Metered feature
    * Fixed the Android backend not advertising Feature::Metered, which
      made supports(Metered) and loadBackendByFeatures(Metered) fail on
      Android, even though isMetered() returned the correct value.

* 6eb299c49fa QThreadStorage: fix use-after-free on setLocalData() re-
  entrancy
    * Fixed a use-after-free bug triggered by the destructor of a
      payload object recursing into (any other) QThreadStorage.

* ce666252b42 QThreadStorage: unbreak setLocalData(move-only-type)
    * Fixed a compile error in value-based
      QThreadStorage<T>::setLocalData() for move-only T. This makes the
      tls.localData() = std::move(newObject) work-around superfluous
      (though it still works, of course).

* 7c2e97dc381 Add limits on glyph sizes to harden font handling
    * For font rendering, Qt now limits cached rasterization of glyphs
      to 16x em square size or 4096px in either dimension (whichever is
      smallest). For large font sizes, rasterization will normally not
      be cached, but this change may affect QRawFont, text rendered with
      NativeRendering in Qt Quick, as well as smaller font sizes with
      malformed glyphs that extend far outside the em square of the
      font. Setting  QT_MAX_GLYPH_SIZE to 0 in the environment will
      disable the limit.

* 634a44e1d69 QFileInfo::canonicalFilePath(): fix handling of
  inaccessible paths
    * Fixed a bug in canonicalPath() that would cause it to return a
      non-empty but possibly not canonical path if an error occurs
      during the process. This affected Unix systems other than Android
      and Apple OSes.

* 9deebde7bac Upgrade Harfbuzz to 14.4.0
    * Upgraded Harfbuzz to version 14.4.0

* 5b833552b14 Upgrade PCRE2 to 10.48
    * PCRE2 was updated to version 10.48.

* 45d2a38b573 Normalize QEventPoint y coordinate by height instead of
  width
    * QEventPoint::normalizedPosition() now normalizes the y coordinate
      by the height of the available virtual geometry instead of its
      width, correcting the result on non-square devices.

* 2d02f598c1a QNetworkAccessManager: wait for reconnect after GOAWAY
    * When a server sends an HTTP/2 GOAWAY frame, requests it has
      signaled as not processed are now held and sent on a new
      connection instead of stalling. Requests that cannot be sent again
      fail with ContentReSendError; previously they failed with
      ProtocolUnknownError or, in some cases, never finished.

* d214201f837 QByteArray: fix UB (signed overflow) in
  fromBase64Encoding()
    * Fixed an integer overflow in fromBase64Encoding() that could lead
      to a buffer overflow.

* 1ceea1f7d27 QByteArray: fix crash if zlib reurns Z_BUF_ERROR
    * Fixed a bug that could cause qUncompress() to crash or have
      undefined behavior on specific corrupted input streams.

* 5a1194b2d36 QString: fix UB (type mismatch) in asprintf() %jd handling
    * Fixed asprintf() to correctly extract `j` as intmax_t, not as long
      int.

* 1c0657bc64f Upgrade PCRE2 to 10.49
    * PCRE2 was updated to version 10.49.

* b5069144d40 Update md4c to 0.6.0
    * Updated md4c to version 0.6.0.

* 837a94ff520 QAuthenticator: pass the SPN to SSPI for NTLM as well
    * On Windows, NTLM authentication now sends the target SPN (the
      "spn" option, or HTTP/<host>) to SSPI, as Negotiate already did.

* af26ecf8c35 Upgrade Harfbuzz to 14.6.0
    * Upgraded Harfbuzz to version 14.6.0

* 853fdcabcee Update Freetype to 2.15.0
    * Updated bundled Freetype to 2.15.0.

* ba39a857fd9 SQLite: Update SQLite to v3.54.0
    * Updated SQLite to v3.54.0

* 138f955f0b5 Update bundled libpng to version 1.6.59
    * libpng was updated to version 1.6.59

### qtdeclarative
* 68d6d80033 QQuickWidget: Return the window our content is composited
  into
    * QQuickRenderControl::renderWindowFor() now returns the window that
      the QQuickWidget's content is composited into, which for a
      QQuickWidget below a widget with Qt::WA_NativeWindow set is that
      widget's window, and not the top level window.

* 98a9dc700f Prevent textChanged signal on select method call
    * TextEdit.select() no longer emits the textChanged signal.

### qtmultimedia
* 884fc4a59 Update FFmpeg => 7.1.5
    * Update FFmpeg to version 7.1.5

* 9a94e5975 3rdparty: update dr_wav snapshot
    * Update dr_wav to 0.14.6-snapshot-955edd32

* 0fb3c7374 dr_libs: pull in upstream snapshot and fuzzing fixes
    * Update dr_wav to 0.14.6-snapshot-ee937527 and fix integer
      overflow/assertion failures.

### qtserialbus
* 61fe7bd4 TinyCAN: Fix sending and receiving
    * Fixed that the TinyCAN plugin did not send or receive.

### qtwebsockets
* e7c5a1a QWebSocket: fix off-by-one header size limit
    * A handshake header whose size is exactly the limit (100 lines of 8
      KiB plus the terminator) is now refused rather than accepted.

* b895151 QWebSocket: fix quadratic copy and scan during pre-handshake
    * An over-sized handshake response now closes the connection, and
      QWebSocket::closeCode() reports
      QWebSocketProtocol::CloseCodeTooMuchData. The size limit is also
      now applied as the response arrives, rather than only while the
      end of the headers has not been seen.

* 4a9a7be QWebSocketServer: Fix quadratic copy and scan during pre-
  handshake
    * The handshake header size limit is now applied as the request
      arrives, rather than only while the end of the headers has not
      been seen. An over-sized request now fails with
      QWebSocketProtocol::CloseCodeTooMuchData and "Header is too
      large." instead of CloseCodeProtocolError and "Invalid handshake
      request."

### qt5compat
* 2e3b94b QTextCodec: fix int overflow and infinite loop in ICU
    * Fixed a bug in an ICU codec that could loop infinitely when the
      input to toUnicode() or fromUnicode() was too long. The updated
      code now raises a warning and returns an empty QString/QByteArray
      immediately. To process long inputs, implement the chunking of the
      input data on the client side, using the toUnicode() and
      fromUniocode() overloads that take the ConverterState as the last
      parameter.

* 299c11f QTextCodec: fix silent truncation of input data to int
    * Fixed a bug in toUnicode(), fromUnicode(), and canEncode() methods
      that could silently truncate the size of input data if it exceeded
      INT_MAX. The updated code now raises a warning and returns an
      empty QString/QByteArray immediately. To process long inputs,
      implement chunking of the input data on the client side, using the
      toUnicode() and fromUnicode() overloads that take the
      ConverterState as the last parameter.

* a90bd07 QBinaryJson: reject a misaligned Base::tableOffset
    * Fixed a bug that would cause undefined behavior on certain invalid
      inputs to occur, making rejection of such inputs unreliable (we
      did not observe them in our CI, but UB can manifest in surprising
      ways, so absence of proof isn't proof of absence).

* ca50a88 Enable exceptions in Qt5CoreCompat
    * Is now built with exceptions enabled. Before, exceptions (e.g.
      thrown from QtCore) could still travel through the module's code,
      but would not run the module's cleanup, leaking resources such as
      memory and mutex locks.

* f6d0b35 QXmlSimpleReader: fix unbounded recursion when parsing nested
  elements
    * Fixed a stack overflow when parsing documents with very deeply
      nested elements.

* 6faf4c2 QXmlSimpleReader: add a property to control entity expansion
  limit
    * The entity expansion limit of 4096 characters is now applied more
      strictly, which can lead to some previously valid documents to be
      considered malformed. Use setProperty() with a new property
      "http://qt-project.org/xml/properties/entity-expansion-limit" to
      adjust the limit.

### qtcoap
* fcd2788 Read the 16-bit extended option delta/length correctly
    * Fixed the decoding of options that use the 16-bit extended delta
      or length encoding. Such an option was previously read as a single
      byte, producing an incorrect value and causing the remainder of
      the message to be misparsed.

### qthttpserver
* 2c06fe1 Reject invalid or out-of-range Content-Length
    * A request with a malformed Content-Length (non-numeric, negative,
      or too large to represent) is now rejected with 400 (Bad Request)
      over HTTP/1.Previously such a value was ignored and the request
      processed as if it had no body.

* b8980f7 Parse Transfer-Encoding as a coding list instead of a
  substring
    * Transfer-Encoding is now parsed as a list of transfer-codings
      rather than matched as a substring. Requests are rejected when the
      header contains a coding other than "chunked" (including
      "identity") with 501 Not Implemented, or when "chunked" is
      combined with another coding or appears more than once with 400
      Bad Request. Previously such requests were accepted.

### qtgrpc
* 8254cfa4 QGrpcHttp2Channel: don't send DATA frames before HEADERS
    * Fixed a race on client- and bidi-streaming RPCs where the first
      request message could be dropped when written before the HTTP/2
      HEADERS frame had been sent. Most visible on HTTPS, where TLS
      handshake latency widened the window between stream attachment and
      HEADERS emission.

* 46ef4798 QGrpcHttp2Channel: reject all reserved metadata keys from
  user metadata
    * User-provided metadata with reserved HTTP/2 or gRPC keys is now
      dropped when building requests to avoid conflicts with transport-
      managed headers.

* 8a5dde0e QGrpcHttp2Channel: make hostUri() round-trip across all
  transports
    * hostUri() now preserves the 'unix' and 'unix-abstract' schemes
      instead of reporting them as 'http'.

* d6ff9a76 QGrpcHttp2Channel: reject messages exceeding a configurable
  size limit
    * Incoming messages larger than 4 MiB are now rejected by default,
      matching the gRPC specification. The environment variable
      QT_GRPC_MAXIMUM_RECEIVE_MESSAGE_SIZE overrides this limit; a value
      of 0 disables it.

* 5f2e137e QGrpcHttp2Channel: enforce frame size limit on outbound
  messages
    * Outgoing messages exceeding the maximum frame size are now
      rejected with StatusCode::ResourceExhausted instead of being
      silently truncated on the wire.

* cd3811c3 QGrpcHttp2Channel: drain the outgoing queue iteratively
    * Fixed a stack overflow that could crash the client when burst-
      writing a very large number of messages on a client-streaming or
      bidirectional RPC.

* f9ab8872 QGrpcHttp2Channel: raise the default HTTP/2 receive window
    * The default HTTP/2 receive window was raised from 64 KiB to 4 MiB
      per stream and 16 MiB per connection. The per-stream window can be
      tuned via the QT_GRPC_HTTP2_STREAM_RECEIVE_WINDOW_SIZE environment
      variable and the connection window via
      QT_GRPC_HTTP2_CONNECTION_RECEIVE_WINDOW_SIZE

* aefca7d2 QGrpcHttp2Channel: add reconnect backoff and connect timeout
    * The channel no longer reconnects immediately after a connection
      failure. It now applies exponential backoff with jitter, starting
      at 1 s and capped at 120 s, and aborts a single connection attempt
      that hangs for more than 20 s. The environment variables
      QT_GRPC_INITIAL_RECONNECT_BACKOFF_MS,
      QT_GRPC_MAXIMUM_RECONNECT_BACKOFF_MS, and
      QT_GRPC_CONNECT_TIMEOUT_MS override the three defaults.

* d474446e QGrpcHttp2Channel: add a configurable maximum metadata size
    * The channel now rejects metadata larger than 16 KiB, matching the
      gRPC specification. The environment variable
      QT_GRPC_MAXIMUM_METADATA_SIZE overrides the limit.

### qtinterfaceframework (Commercial only)
* 44487478 Update the bundled qface to the latest version (2.0.14)
    * The copy of qface in Qt was updated to 2.0.14


Fixes
-----

### qtbase
* [QTBUG-147854](https://qt-project.atlassian.net/browse/QTBUG-147854) QSurfaceFormat::setSwapInterval doesn't work with
GLX/mesa
* [QTBUG-147155](https://qt-project.atlassian.net/browse/QTBUG-147155) EGLFS/libinput drops slow relative mouse motion
* [QTBUG-147156](https://qt-project.atlassian.net/browse/QTBUG-147156) EGLFS/libinput can place edge touches outside the target
window
* [QTBUG-146211](https://qt-project.atlassian.net/browse/QTBUG-146211) IME under text-input-v3 is never disabled on COSMIC
* [QTBUG-133804](https://qt-project.atlassian.net/browse/QTBUG-133804) Qt 5 and Qt 6 both use QtProject.conf, but in an
incompatible way
* [QTBUG-148216](https://qt-project.atlassian.net/browse/QTBUG-148216) Crash in QVulkanInstance::create() when
vkCreateDebugUtilsMessengerEXT is unavailable
* [QTBUG-145862](https://qt-project.atlassian.net/browse/QTBUG-145862) NumberAnimation on Rectangle in Node causes assertion
failure on stop
* [QTBUG-147419](https://qt-project.atlassian.net/browse/QTBUG-147419) Integer-overflow in QJalaliCalendar::dateToJulianDay
* [QTBUG-147453](https://qt-project.atlassian.net/browse/QTBUG-147453) [REG 6.10.3 -> 6.11.0] windows11 style rounds corners of
fullscreen windows
* [QTBUG-148603](https://qt-project.atlassian.net/browse/QTBUG-148603) Unable to build with qmake with VxWorks Qt 6.8.8
* [QTBUG-148646](https://qt-project.atlassian.net/browse/QTBUG-148646) QSpinBox up button does not respond when border is set
via stylesheet
* [QTBUG-148792](https://qt-project.atlassian.net/browse/QTBUG-148792) Integer-overflow in QIslamicCivilCalendar
* [QTBUG-136999](https://qt-project.atlassian.net/browse/QTBUG-136999) Top flaky test: tst_QWindow::testInputEvents
* [QTBUG-101519](https://qt-project.atlassian.net/browse/QTBUG-101519) FAIL!  :
tst_QTouchEvent::multiPointRawEventTranslationOnTouchPad in
Windows_11_21H2
* [QTBUG-148524](https://qt-project.atlassian.net/browse/QTBUG-148524) Windows: title-bar and taskbar icon is blurry at
fractional DPI scaling — icon is sized for the primary monitor and
requested at DPR 1 (incomplete fix for QTBUG-90363)
* [QTBUG-148525](https://qt-project.atlassian.net/browse/QTBUG-148525) Windows: title-bar / taskbar icon is not rebuilt on DPI
change (WM_DPICHANGED) — stays sized for the startup monitor
* [QTBUG-141755](https://qt-project.atlassian.net/browse/QTBUG-141755) Build failure with latest vs 2022 (17.14.19)
* [QTBUG-146146](https://qt-project.atlassian.net/browse/QTBUG-146146) Clash with unity-build on Windows
* [QTBUG-149232](https://qt-project.atlassian.net/browse/QTBUG-149232) QtWayland reuses a committed SHM buffer after a frame
callback timeout, causing raster windows to stop updating
* [QTBUG-149220](https://qt-project.atlassian.net/browse/QTBUG-149220) QRhiTextureRenderTarget with multiple color attachments
could crash with D3D12
* [QTBUG-149045](https://qt-project.atlassian.net/browse/QTBUG-149045) Incomplete qtbase docs after cmake --build -t docs
* [QTBUG-148810](https://qt-project.atlassian.net/browse/QTBUG-148810) Android: QNetworkInformation does not report "Metered"
feature
* [QTBUG-149293](https://qt-project.atlassian.net/browse/QTBUG-149293) Qt 5.15.16: SRGB8_Alpha8 texture upload/sampling fails
on Mali, shader samples a 1x1 black texture; similar code path exists in
Qt 6
* [QTBUG-149010](https://qt-project.atlassian.net/browse/QTBUG-149010) QDoubleValidator asserts when one limit is left
unbounded
* [QTBUG-148845](https://qt-project.atlassian.net/browse/QTBUG-148845) `QLockFile::unlock()` cannot remove its own lock file on
a Dell EMC Unity NFSv4.2 mount after Qt 6 changed to unlink before close
* [QTBUG-132577](https://qt-project.atlassian.net/browse/QTBUG-132577) QLocale::system() returns same QLocale after OS language
change
* [QTBUG-116642](https://qt-project.atlassian.net/browse/QTBUG-116642) Provide a refresh mechanism for system locale data
* [QTBUG-147832](https://qt-project.atlassian.net/browse/QTBUG-147832) Qt program built with clang-cl.exe cannot start when
upgrading from 6.10.3 -> 6.11.1
* [QTBUG-149431](https://qt-project.atlassian.net/browse/QTBUG-149431) [REG 6.11.1->6.11.2] QIcon::setFallbackThemeName()
affects QIcon::themeName()
* [QTBUG-135044](https://qt-project.atlassian.net/browse/QTBUG-135044) tst_QStringApiSymmetry fails under ASAN
(GenerationalCollator is leaked?)
* [QTBUG-147933](https://qt-project.atlassian.net/browse/QTBUG-147933) QMetalLayer displayLock not released when displayLayer
returns early for offline screen
* [QTBUG-149426](https://qt-project.atlassian.net/browse/QTBUG-149426) QRhi Vulkan: Resolved depth is undefined when sampled in
Vulkan backend
* [QTBUG-149391](https://qt-project.atlassian.net/browse/QTBUG-149391) SPDX: failed creation of SBOM on Cygwin
* [QTBUG-149297](https://qt-project.atlassian.net/browse/QTBUG-149297) Qt Checkbox graphics glitch if text font is large
* [QTBUG-149316](https://qt-project.atlassian.net/browse/QTBUG-149316) QtDBus aborts the process (SIGABRT) when the bus
connection is lost: getNameOwnerNoCache() passes a NULL DBusPendingCall
to dbus_pending_call_block()
* [QTBUG-149503](https://qt-project.atlassian.net/browse/QTBUG-149503) Qt Concurrent: suspending map()/filter() releases a
thread slot on the global pool instead of its own
* [QTBUG-149130](https://qt-project.atlassian.net/browse/QTBUG-149130) QLockFile/Unix: race condition when creating a lock
takes longer than staleLockTime
* [QTBUG-144852](https://qt-project.atlassian.net/browse/QTBUG-144852) Android Accessibility focus lost after Talkback menu was
opened
* [QTBUG-149608](https://qt-project.atlassian.net/browse/QTBUG-149608) Missing trailing '>' in QMetaType::name() for nested
std::pair
* [QTBUG-140455](https://qt-project.atlassian.net/browse/QTBUG-140455) Wait cursor is lost after MessageBox is shown
* [QTBUG-149616](https://qt-project.atlassian.net/browse/QTBUG-149616) Setting QT_ANDROID_SDK_BUILD_TOOLS_REVISION generates
invalid gradle.properties
* [QTBUG-147824](https://qt-project.atlassian.net/browse/QTBUG-147824) Build error - Android SDK Build Tools version
* [QTBUG-149580](https://qt-project.atlassian.net/browse/QTBUG-149580) QNX 8.0.5: QThread::start warns "Cannot determine
scheduler priority range", failing
tst_QQuickFolderDialogImpl::defaults()
* [QTBUG-149880](https://qt-project.atlassian.net/browse/QTBUG-149880) Clarify how QPainterPath calculates arcs
* [QTBUG-149559](https://qt-project.atlassian.net/browse/QTBUG-149559) `QCborValue::type()` changes after `toCbor()` and
`fromCbor()` round-trip for an empty `QDateTime`
* [QTBUG-149887](https://qt-project.atlassian.net/browse/QTBUG-149887) Markdown fenced code block under a tight list item
generates list items for each line
* [QTBUG-149770](https://qt-project.atlassian.net/browse/QTBUG-149770) Unsupported value: android-37.0
* [QTBUG-149843](https://qt-project.atlassian.net/browse/QTBUG-149843) QtXml: QDomElement::text() is worst-case quadratic
(XMLBUG-05)
* [QTBUG-137533](https://qt-project.atlassian.net/browse/QTBUG-137533) Crash during drag and drop
* [QTBUG-106879](https://qt-project.atlassian.net/browse/QTBUG-106879) QEventPoint::normalizedPosition() returns incorrect
position on Y axis
* [QTBUG-149562](https://qt-project.atlassian.net/browse/QTBUG-149562) QIODevice::read (QSslSocket): device not open
* [QTBUG-144577](https://qt-project.atlassian.net/browse/QTBUG-144577) Android: Crash in screenInputItemRectangle() seen in
Google Play Console
* [QTBUG-133221](https://qt-project.atlassian.net/browse/QTBUG-133221) [REG: 6.7->6.8] SVG file mime type not recognized if the
file contains xml header
* [QTBUG-145739](https://qt-project.atlassian.net/browse/QTBUG-145739) [Reg] QMimeDatabase tests broken by "Incorporate the
sub-class-of info when deriving mimetypes"
* [QTBUG-148579](https://qt-project.atlassian.net/browse/QTBUG-148579) QPaintEngine::drawTextItem() fallback misplaces color-
font glyphs and ignores the pen color
* [QTBUG-148302](https://qt-project.atlassian.net/browse/QTBUG-148302) Text in a color font (OT-SVG / COLR) is garbled when
printed to PDF
* [QTBUG-147237](https://qt-project.atlassian.net/browse/QTBUG-147237) HTTP2 GOAWAY ContentReSendError not sent out / requests
timing out and not
* [QTBUG-150636](https://qt-project.atlassian.net/browse/QTBUG-150636) qtbase build failure with md4c 0.6.0
* [QTBUG-100412](https://qt-project.atlassian.net/browse/QTBUG-100412) tst_qsrceen::grabWindow is flaky on Windows
* [QTBUG-148721](https://qt-project.atlassian.net/browse/QTBUG-148721) Many crashes within QNSView
* [QTBUG-148717](https://qt-project.atlassian.net/browse/QTBUG-148717) Widget backing store crashes after graphics device loss
on D3D11/D3D12 (device loss never reported by beginFrame())
* [QTBUG-146948](https://qt-project.atlassian.net/browse/QTBUG-146948) Update llvm-mingw to 22.1.1 fails: qtbase
tst_Collections::map() 'j1 == map1.find("1") && k1 == j1' returned
FALSE. ()
* [QTBUG-145948](https://qt-project.atlassian.net/browse/QTBUG-145948) QMultiMap has incorrect behavior with LLVM libc++
starting with 22
* [QTBUG-134105](https://qt-project.atlassian.net/browse/QTBUG-134105) tst_qscroller::overshoot() is flaky on macOS
* [QTBUG-49640](https://qt-project.atlassian.net/browse/QTBUG-49640) QLockFile stale lock file removal detection fails if non-
ASCII characters in host name
* [QTBUG-147228](https://qt-project.atlassian.net/browse/QTBUG-147228) QMetalLayer displayLock triggers spurious TSan "double
lock of a mutex" on macOS
* [QTBUG-149000](https://qt-project.atlassian.net/browse/QTBUG-149000) QVariant(0.1).toBool() == false, but should be true
* [QTBUG-148616](https://qt-project.atlassian.net/browse/QTBUG-148616) QDateTime / std::chrono arithmetic is prone to UB
(signed overflow)
* [QTBUG-149402](https://qt-project.atlassian.net/browse/QTBUG-149402) Top crashing test: tst_QGraphicsView scrollBarRanges
* [QTBUG-148640](https://qt-project.atlassian.net/browse/QTBUG-148640) Unvalidated offsets in binary mime.cache parsing
* [QTBUG-148790](https://qt-project.atlassian.net/browse/QTBUG-148790) Validate negative XML MIME magic offsets
* [QTBUG-141568](https://qt-project.atlassian.net/browse/QTBUG-141568) List item marker misaligned with inline image content
* [QTBUG-109307](https://qt-project.atlassian.net/browse/QTBUG-109307) issues with QVulkanVindow
* [QTBUG-149362](https://qt-project.atlassian.net/browse/QTBUG-149362) macOS 27: refused TCP emits connected() + wrong error,
HTTP hangs

### qtdeclarative
* [QTBUG-90761](https://qt-project.atlassian.net/browse/QTBUG-90761) [FileDialog] Files from selected folder cannot be opened
in photosurface
* [QTBUG-109990](https://qt-project.atlassian.net/browse/QTBUG-109990) Photosurface example doesn't show any photos
* [QTBUG-147847](https://qt-project.atlassian.net/browse/QTBUG-147847) Dialog size incorrectly overridden by implicit size
resize logic when size is explicitly set
* [QTBUG-148633](https://qt-project.atlassian.net/browse/QTBUG-148633) qmllint crash on signatureIgnored.qml
* [QTBUG-146781](https://qt-project.atlassian.net/browse/QTBUG-146781) Pointer handlers: UngrabExclusive uses wrong coordinate
system for local position
* [QTBUG-147003](https://qt-project.atlassian.net/browse/QTBUG-147003) [Reg 6.8.7 -> 6.11.1] Pointer handlers: UngrabPassive
uses the wrong coordinate system for local position
* [QTBUG-146209](https://qt-project.atlassian.net/browse/QTBUG-146209) Wheel events can cause TapHandler's grab to silently
disappear
* [QTBUG-144449](https://qt-project.atlassian.net/browse/QTBUG-144449) qmllint doesn't find alias starting with underscore
* [QTBUG-146947](https://qt-project.atlassian.net/browse/QTBUG-146947) Hardening needed against underscores in case-significant
identifiers
* [QTBUG-148532](https://qt-project.atlassian.net/browse/QTBUG-148532) Crash in QQuickShapeGenericRenderer: done() signal
emitted from worker thread races with GUI-thread teardown
* [QTBUG-148598](https://qt-project.atlassian.net/browse/QTBUG-148598) Qt Quick Shapes (CurveRenderer): stroke not repainted
when strokeColor and fillColor change together
* [QTBUG-147603](https://qt-project.atlassian.net/browse/QTBUG-147603) Popup.Window: DragHandler causes dragged item to jump
off-screen on drag start
* [QTBUG-148690](https://qt-project.atlassian.net/browse/QTBUG-148690) qmlls autocompletions: local importPaths (.qmlls.ini)
ignored when QML file is currently invalid
* [QTBUG-148191](https://qt-project.atlassian.net/browse/QTBUG-148191) Double free resulting in segfault in curve renderer when
paths modified while dialog opened
* [QTBUG-149123](https://qt-project.atlassian.net/browse/QTBUG-149123) PathView drops one delegate when the whole model is
cached and incubation is synchronous
* [QTBUG-141568](https://qt-project.atlassian.net/browse/QTBUG-141568) List item marker misaligned with inline image content
* [QTBUG-149401](https://qt-project.atlassian.net/browse/QTBUG-149401) QJSEngine: regexps silently fail after moveToThread
* [QTBUG-148695](https://qt-project.atlassian.net/browse/QTBUG-148695) VectorImage.generatedItem is not reset to null when the
source is cleared; it keeps a stale item from the previous load
* [QTBUG-149244](https://qt-project.atlassian.net/browse/QTBUG-149244) qmlls crashes with a stack overflow on a function
declaration inside a property binding
* [QTBUG-149089](https://qt-project.atlassian.net/browse/QTBUG-149089) qmlls returns no semantic tokens for any QML document
containing an `id` that starts with an underscore
* [QTBUG-83224](https://qt-project.atlassian.net/browse/QTBUG-83224) TextEdit always sends a textChanged signal, after select
method calls
* [QTBUG-149360](https://qt-project.atlassian.net/browse/QTBUG-149360) qmllint/qmlls segfaults when the imported QtQuick module
resolves without usable type information
* [QTBUG-149518](https://qt-project.atlassian.net/browse/QTBUG-149518) QObject wrapper reuse can make QML state dependent on GC
timing.
* [QTBUG-149307](https://qt-project.atlassian.net/browse/QTBUG-149307) Doing QQmlComponent::setData() repeatedly retains an
mmap of the cache file per iteration
* [QTBUG-149446](https://qt-project.atlassian.net/browse/QTBUG-149446) Qt 6.11.2: reading an alias-to-a-local-alias returns
garbage / crashes
* [QTBUG-148846](https://qt-project.atlassian.net/browse/QTBUG-148846) Re-entrant deferred execution leaks an in-progress
creation when a deferred property evaluates to `null`
* [QTBUG-148459](https://qt-project.atlassian.net/browse/QTBUG-148459) Null dereference in
QQmlConnections::connectSignalsToMethods() during asynchronous
incubation
* [QTBUG-142387](https://qt-project.atlassian.net/browse/QTBUG-142387) Internal error with Qt.callLater() on invalid context
* [QTBUG-104016](https://qt-project.atlassian.net/browse/QTBUG-104016) After calling Qt.CallLater C++ context is destroyed
while the QML contex is not
* [QTBUG-74517](https://qt-project.atlassian.net/browse/QTBUG-74517) tst_TouchMouse::buttonOnFlickable() and
tst_TouchMouse::touchButtonOnFlickable() are flaky on mingw
* [QTBUG-146741](https://qt-project.atlassian.net/browse/QTBUG-146741) Windows/Accessibility: Accessible.ignored is ignored
* [QTBUG-147828](https://qt-project.atlassian.net/browse/QTBUG-147828) TextArea.placeholderText does not respect wrapMode
* [QTBUG-144225](https://qt-project.atlassian.net/browse/QTBUG-144225) Undefined Behaviour in TextArea

### qtmultimedia
* [QTBUG-143067](https://qt-project.atlassian.net/browse/QTBUG-143067) Quitting a camera application hangs on HMD Skyline
TA-1600
* [QTBUG-141688](https://qt-project.atlassian.net/browse/QTBUG-141688) Android: Camera does not recover after minimizing.
* [QTBUG-149181](https://qt-project.atlassian.net/browse/QTBUG-149181) Qt 6.11.1 QAudioSink PipeWire - spins or crashes when
server died while playing
* [QTBUG-149346](https://qt-project.atlassian.net/browse/QTBUG-149346) [REG 6.10.3 - 6.11.1] QMediaPlayer silently stops
playback ~400ms after setSource() + play()
* [QTBUG-148231](https://qt-project.atlassian.net/browse/QTBUG-148231) Android QMediaDevices does not list USB audio devices
* [QTBUG-149907](https://qt-project.atlassian.net/browse/QTBUG-149907) A muted SoundEffect silences the sound effects that
started before it
* [QTBUG-149917](https://qt-project.atlassian.net/browse/QTBUG-149917) An audio output device change doubles a playing
SoundEffect's voices
* [QTBUG-142743](https://qt-project.atlassian.net/browse/QTBUG-142743) QtMultimediaPrivate::QRtAudioEngine::getEngineFor crash
with remote connection
* [QTBUG-149229](https://qt-project.atlassian.net/browse/QTBUG-149229) Android: Deadlock on app shutdown when
QAndroidVideoDevices is destroyed
* [QTBUG-
150172](https://qt-project.atlassian.net/browse/QTBUG-150172) play_playsTransformedVideoOutput_whenVideoFileHasTransformationMe
tadata failure on macOS 26 host
* [QTBUG-151355](https://qt-project.atlassian.net/browse/QTBUG-151355) Crashing/flaky qtmultimedia tests in Windows after
adding audio in CI

### qttools
* [QTBUG-148562](https://qt-project.atlassian.net/browse/QTBUG-148562) lcheck does not report all violations
* [QTBUG-107193](https://qt-project.atlassian.net/browse/QTBUG-107193) fatal error: 'QtDesigner/uilib_global.h' file not found

### qtdoc
* [QTBUG-143416](https://qt-project.atlassian.net/browse/QTBUG-143416) [Boot to Qt 6.11.0 beta2] Linking 'toycustomizer' fails
on Windows
* [QTBUG-147624](https://qt-project.atlassian.net/browse/QTBUG-147624) ToyCustomizer demo fails to build on case-insensitive
filesystems (macOS)
* [QTBUG-142754](https://qt-project.atlassian.net/browse/QTBUG-142754) New example demos/toycustomizer fails to configure on
iOS

### qtlocation
* [QTBUG-107193](https://qt-project.atlassian.net/browse/QTBUG-107193) fatal error: 'QtDesigner/uilib_global.h' file not found

### qtconnectivity
* [QTBUG-149163](https://qt-project.atlassian.net/browse/QTBUG-149163) Null DeviceInformation() projection crashes
QWinRTBluetoothDeviceDiscoveryWorker during BLE discovery
* [QTBUG-80580](https://qt-project.atlassian.net/browse/QTBUG-80580) Error "Could not await descriptor read result" when
connect to service of BLE device

### qtwayland
* [QTBUG-146200](https://qt-project.atlassian.net/browse/QTBUG-146200) Dialogs miss separating border on Gnome/Wayland

### qt3d
* [QTBUG-135853](https://qt-project.atlassian.net/browse/QTBUG-135853) Scene2D not rendering

### qtserialbus
* [QTBUG-111551](https://qt-project.atlassian.net/browse/QTBUG-111551) MHS TinyCAN plugin does not work

### qtwebsockets
* [QTBUG-107193](https://qt-project.atlassian.net/browse/QTBUG-107193) fatal error: 'QtDesigner/uilib_global.h' file not found

### qtwebchannel
* [QTBUG-141665](https://qt-project.atlassian.net/browse/QTBUG-141665) Doc: Suppress "No output generated for ..."

### qtwebengine
* [QTBUG-146565](https://qt-project.atlassian.net/browse/QTBUG-146565) [qtwebengine] QWebEngineWebAuthUxRequest objects have
garbage/uninitialized fields
* [QTBUG-148751](https://qt-project.atlassian.net/browse/QTBUG-148751) [REG 6.11.2->6.12.0] webenginequick/quicknanobrowser not
launching on linux and Windows
* [QTBUG-149540](https://qt-project.atlassian.net/browse/QTBUG-149540) The Qt PDF module doc page does not state, nor explains
the use of PDFium

### qtspeech
* [QTBUG-151355](https://qt-project.atlassian.net/browse/QTBUG-151355) Crashing/flaky qtmultimedia tests in Windows after
adding audio in CI

### qtnetworkauth
* [QTBUG-148995](https://qt-project.atlassian.net/browse/QTBUG-148995) QOAuth2 ignores invalid_grant response

### qtquick3d
* [QTBUG-148707](https://qt-project.atlassian.net/browse/QTBUG-148707) View3D, render mode View3D.Inline crashes on application
exit, Win only
* [QTBUG-88320](https://qt-project.atlassian.net/browse/QTBUG-88320) Dynamically creating a View3D second time crashes
* [QTBUG-144962](https://qt-project.atlassian.net/browse/QTBUG-144962) crash in scene manager when swapping scenes
* [QTBUG-147451](https://qt-project.atlassian.net/browse/QTBUG-147451) Qt Quick3D: use-after-free in View3D teardown
* [QTBUG-150763](https://qt-project.atlassian.net/browse/QTBUG-150763) Qt Quick 3D: the automatic disk shader cache
(q3dshadercache.qsbc) never hits for default materials
* [QTBUG-148806](https://qt-project.atlassian.net/browse/QTBUG-148806) QDoc: error: Documentation warnings (2) exceeded the
limit (1) for 'QtQuick3D'.
* [QTBUG-144929](https://qt-project.atlassian.net/browse/QTBUG-144929) QObject::disconnect(const Connection &) const_cast<>s
its argument

### qt5compat
* [QTBUG-149006](https://qt-project.atlassian.net/browse/QTBUG-149006) QLinkedList restores incorrect size if operator+=()
throws
* [QTBUG-149054](https://qt-project.atlassian.net/browse/QTBUG-149054) QBinaryJson::to{Raw,Binary}Data() does not own the
allocated memory
* [QTBUG-149430](https://qt-project.atlassian.net/browse/QTBUG-149430) QStringRef can compute a negative size when passed a Qt6
QString
* [QTBUG-150303](https://qt-project.atlassian.net/browse/QTBUG-150303) [REG Qt 5→6] Potential deadlock d/t -fno-exceptions
[Qt5Support]

### qtcoap
* [QTBUG-149883](https://qt-project.atlassian.net/browse/QTBUG-149883) Crash in tst_QCoapClient

### qtmqtt
* [QTBUG-149571](https://qt-project.atlassian.net/browse/QTBUG-149571) Number overflow while rejecting a too-long length
* [QTBUG-149570](https://qt-project.atlassian.net/browse/QTBUG-149570) Skip remaining data for messages with unknown requests
* [QTBUG-149662](https://qt-project.atlassian.net/browse/QTBUG-149662) finalize_pingresp() lowers m_pingTimeout every time,
with no lower limit
* [QTBUG-149569](https://qt-project.atlassian.net/browse/QTBUG-149569) Read the Remaining Length as a variable byte integer
everywhere

### qthttpserver
* [QTBUG-150270](https://qt-project.atlassian.net/browse/QTBUG-150270) Fix unbounded chunk-size/chunk-extension line
accumulation in QHttpServerParser
* [QTBUG-150274](https://qt-project.atlassian.net/browse/QTBUG-150274) Fix chunked body-size gate integer overflow
* [QTBUG-150275](https://qt-project.atlassian.net/browse/QTBUG-150275) Fix Content-Length quint64->qint64 wrap

### qtgrpc
* [QTBUG-146913](https://qt-project.atlassian.net/browse/QTBUG-146913) QGrpcHttp2Channel: hostUri() is not idempotent for unix
transports
* [QTBUG-148062](https://qt-project.atlassian.net/browse/QTBUG-148062) GRPC: Client crashes when writing a large number of
messages to a streaming RPC
* [QTBUG-147934](https://qt-project.atlassian.net/browse/QTBUG-147934) QtGrpc: Provide write backpressure for streaming RPCs
* [QTBUG-148148](https://qt-project.atlassian.net/browse/QTBUG-148148) QGrpcHttp2Channel: validate server-sent grpc-status
range
* [QTBUG-148149](https://qt-project.atlassian.net/browse/QTBUG-148149) QGrpcHttp2Channel: sanitize server-controlled bytes in
warning logs
* [QTBUG-147829](https://qt-project.atlassian.net/browse/QTBUG-147829) QGrpcHttp2Channel: add exponential reconnect backoff
* [QTBUG-145758](https://qt-project.atlassian.net/browse/QTBUG-145758) Top flaky test: tst_grpc_client_clientstream_qml
checkClientStreamResult::test_testClientStreamCheck
* [QTBUG-145588](https://qt-project.atlassian.net/browse/QTBUG-145588) Top flaky test: tst_grpc_client_serverstream_qml
checkServerStreamResult::test_testServerStreamCheck
* [QTBUG-145587](https://qt-project.atlassian.net/browse/QTBUG-145587) Top flaky test: tst_grpc_client_unarycall_qml
qtgrpcClientTestCall::test_testMethodCallCheck
* [QTBUG-145586](https://qt-project.atlassian.net/browse/QTBUG-145586) Top flaky test: tst_grpc_client_unarycall_qml
unaryCallWithOptionsCheck::test_unaryCallWithOptionsCheck
* [QTBUG-148066](https://qt-project.atlassian.net/browse/QTBUG-148066) GRPC: Allow bounding the outgoing message queue for
streaming RPCs

### qtgraphs
* [QTBUG-146779](https://qt-project.atlassian.net/browse/QTBUG-146779)  AxisRenderer::initialize() spams qCCritical "window
doesn't exist." on every window visibility change
* [QTBUG-149302](https://qt-project.atlassian.net/browse/QTBUG-149302) Custom point markers not removed when pointDelegate set
to null
* [QTBUG-147723](https://qt-project.atlassian.net/browse/QTBUG-147723) [Reg 6.11.1 -> 6.12.0b1] GraphsView axes are incorrectly
positioned at startup
* [QTBUG-147576](https://qt-project.atlassian.net/browse/QTBUG-147576) [Android] widgetgraphgallery 3D example crashes with
SIGSEGV (null pointer dereference) on startup on Android
* [QTBUG-148514](https://qt-project.atlassian.net/browse/QTBUG-148514) Crash when a selected point is removed and the user
presses empty space again
* [QTBUG-149930](https://qt-project.atlassian.net/browse/QTBUG-149930) GraphsView: Toggling panStyle/zoomStyle can lead to a
crash
* [QTBUG-149369](https://qt-project.atlassian.net/browse/QTBUG-149369) QQuickDragHandler list desyncs from marker list in
PointRenderer, when dragging after a marker teardown/rebuild
* [QTBUG-149245](https://qt-project.atlassian.net/browse/QTBUG-149245) XYModelMapper crashes with SplineSeries

### qtopenapi
* [QTBUG-149200](https://qt-project.atlassian.net/browse/QTBUG-149200) openapi\colorpalette not launching after installing, WoA
* [QTBUG-149429](https://qt-project.atlassian.net/browse/QTBUG-149429) Replace quoted includes with angle-bracket includes in
OpenAPI public headers

### qtvncserver (Commercial only)
* [QTBUG-149087](https://qt-project.atlassian.net/browse/QTBUG-149087) Qt VNC Server: ClientCutText integer truncation bug

Known Issues
------------
* Check that your system meets Qt's requirements:
  https://doc.qt.io/qt-6.11/supported-platforms.html
* RTA reported issues from Qt 6.11
  https://qt-project.atlassian.net/issues?filter=21382
* See Qt 6.11 known issues from:
  https://wiki.qt.io/Qt_6.11_Known_Issues
* Qt 6.11.3 Open issues in Jira:
  https://qt-project.atlassian.net/issues/?filter=24561

Credits for the release goes to:
---------------------------------

* Eirik Aavitsland
* Laszlo Agocs
* Dilek Akcay
* Mate Barany
* Thierry Bastian
* Vladimir Belyavsky
* Lena Biliaieva
* Alex Blasche
* Tim Blechmann
* Eskil Abrahamsen Blomfeldt
* Tatiana Borisova
* Assam Boudjelthia
* Carlo Bramini
* Aurélien Brooke
* Michael Brüning
* Eren Bursali
* Olivier De Cannière
* Alexei Cazacov
* Jean-Michaël Celerier
* Kaloyan Chehlarski
* Alexandru Croitor
* Mitch Curtis
* Giuseppe D'Angelo
* Artem Dyomin
* Adrian Eddy
* Oliver Eftevaag
* Christian Ehrlicher
* Hatem ElKharashy
* David Faure
* Mylo Fawcett
* Nicolas Fella
* Julian Greilich
* Robert Griebl
* Jan Grulich
* Mikko Hallamaa
* Andre Hartmann
* Andreas Hartmetz
* Jani Heikkinen
* Moss Heim
* Jeff Heller
* Ulf Hermann
* Volker Hilsheimer
* Dominik Holland
* Linus Jahn
* Masoud Jami
* Morteza Jamshidi
* Allan Sandfeld Jensen
* Wu JiangYu
* Jukka Jokiniva
* Jonas Karlsson
* Friedemann Kleint
* Michal Klocek
* Seokha Ko
* Kai Koehne
* Sze Howe Koh
* Jarkko Koivikko
* Fabian Kosmale
* Jonas Kvinge
* Kai Köhne
* Frédéric Lefebvre
* Wladimir Leuschner
* Robert Löhning
* Thiago Macieira
* Sergio Martins
* Baurzhan Muftakhidinov
* Marc Mutz
* Andy Nichols
* Mårten Nordheim
* Dennis Oberst
* Frank Osterfeld
* Jerome Pasion
* Mauro Persano
* Yauheni Pervenenka
* Nhung Pham
* Karim Pinter
* Lauri Pohjanheimo
* Imre Péntek
* MohammadHossein Qanbari
* Topi Reinio
* Shawn Rutledge
* Manikandan K. S.
* Ahmad Samir
* David Schulz
* Sami Shalayel
* Ivan Solovev
* Axel Spoerl
* Magdalena Stojek
* Christian Strømme
* Tasuku Suzuki
* Jan Arve Sæther
* Sadegh Taghavi
* Jere Tuliniemi
* Paul Olav Tvete
* Tuomas Vaarala
* Jonathan Vannier
* Sami Varanka
* Tor Arne Vestbø
* Juha Vuolle
* Jaishree Vyas
* Vadim Vysokoostrovskiy
* Jannis Völker
* Edward Welbourne
* Piotr Wiercinski
* Oliver Wolff
* Semih Yavuz
* Li Zequan
* JiDe Zhang
* Liu Zheng
* Wang Zichong
* Жора Змейкин
