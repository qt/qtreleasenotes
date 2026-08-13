Release notes
=============
Qt 6.11.2 release is a patch release made on the top of Qt 6.11.1.
As a patch release, Qt 6.11.2 does not add any new functionality but provides
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
* [CVE-2026-16762](https://nvd.nist.gov/vuln/detail/CVE-2026-16762) in qtbase
* [CVE-2026-19248](https://nvd.nist.gov/vuln/detail/CVE-2026-19248) in qtbase
* [CVE-2026-13326](https://nvd.nist.gov/vuln/detail/CVE-2026-13326) in qtconnectivity
* [CVE-2026-8168](https://nvd.nist.gov/vuln/detail/CVE-2026-8168) in qtsvg

### Prebuild binaries
* 713a3653690 Update FFmpeg => 7.1.5
  * The binary distribution has updated FFmpeg to 7.1.5.

### qtbase
* 2f2bd9834cd QRM: add interfaceVersion method
    * QRangeModel in Qt 6.11 broke binary compatibility with Qt 6.10 by
      adding a new implementation for multiData. If you are using
      QRangeModel, recompile your code if calls to QRM::data() or
      QRM::multiData() fail to return valid data.

* a75cee104f3 SQLite: Update SQLite to v3.53.1
    * Updated SQLite to v3.53.1

* 63ffcbd3391 Windows: QLocalServer: explicitly reject remotes
    * Remote connections to QLocalServer on Windows are rejected now.

* 2d035be3d18 Update QLocale data to CLDR v48.2 and the latest ISO 639-3
  table
    * QLocale now uses CLDR v48.2, a minor update on the earlier v48.1.

* 10a6b87a365 QArrayDataPointer: Fix UB (invalid downcast to
  QArrayDataOps)
    * Fixed a bug that could cause data corruption in optimized builds.

* 2925c7ce635 QCollator/ICU: use QByteArray::compare() instead of
  qstrcmp()
    * Fixed a bug that could cause two keys to compare equal/equivalent,
      when they were different.

* 432b5ab664d Update tika-mimetypes.xml from upstream
    * Updated TIKA mimetypes from upstream

* 4d2b1f1b049 QThread/Win: update idealThreadCount() to deal with
  multiple groups
    * Fixed idealThreadCount() to support more than 64 logical
      processors on Windows. It will now return the number of processors
      in each of the processor groups the thread has affinity to. Note
      the behavior of this function is subtly different than on Linux
      and FreeBSD, if the affinity set is not the default from the OS.

* 76c90f84127 Update public suffix list
    * Updated the public suffix list to upstream version
      2026-05-14_08-35-31_UTC.

* 495093e348c QTextMarkdownImporter: Use QRegularExpressionMatchIterator
    * Sped up processing markdown with many HTML tags

* e378902a3e5 SQLite: Update SQLite to v3.53.2
    * Updated SQLite to v3.53.2

* 02c86ca0ae3 Http2: Don't fail a finished reply on a frame after
  END_STREAM
    * Fixed an issue where an HTTP/2 reply could be reported as a
      protocol error with a truncated body when the server sent a stray
      frame after END_STREAM.

* 490eb66a72e QXmlStream: reject duplicate attributes injected by DTD
  ATTLIST
    * Fixed a bug in namespace processing that would fail to detect
      duplicate attributes if at least one of them was defaulted by a
      DTD ATTLIST.

* b8c274c569e QCborValue: fix buffer overread in fromCbor()
    * Fixed a bug on 64-bit platforms that would mishandle data passed
      to the (ptr, len, error) overloads if len ≥ 2Gi, leading to
      incorrect decoding errors or an overread of ptr past len: the
      bytes following the buffer are copied into a heap-allocated buffer
      and, for crafted input, can be returned to the caller in the
      decoded value (out-of-bounds read / information disclosure). You
      need to recompile users of this function for the fix to take
      effect; updating Qt alone is not sufficient. A backwards-
      compatible fix that does not require a Qt update is to construct
      the QByteArray from (ptr, len) yourself and using the
      fromCbor(QByteArray) overload. This preserves the length.

* ab2def395df QLogging: Don't pass the message to unformatted sinks
  twice
    * Fixed messages being logged twice to the system log (os_log on
      Apple platforms, journald on Linux) when using the default message
      handler.

* 7dd126f6c52 Update bundled libjpeg-turbo to version 3.2.0
    * libjpeg-turbo was updated to version 3.2.0

* 79d3fb98a45 SQLite: Update SQLite to v3.53.3
    * Updated SQLite to v3.53.3

* 37f40587c8d Fix QRandomGenerator's fillBuffer() implementation on Unix
    * QRandomGenerator no longer falls back to insecure PRNG on short
      read from /dev/(u)random. It attempts to read more bytes in a loop
      instead.

* 1f63c29dc7b QXmlStreamAttribute: init m_isDefault
    * Fixed undefined behavior (uninitialized isDefault()) when
      QXmlStreamAttribute objects were created with one of the non-
      default constructors.

* bd091f504a0 Update our copy of FFTW's cycle counter to 3.3.11
    * QtTest's benchmarks now use the cycle-counter code from FFTW
      version 3.3.11. This adds support for LoongArch and RISC-V.

* d86ae6acb99 QSmallByteArray: fix incorrect precondition check
    * Fixed an incorrect assertion triggering on correct input: setKey()
      with an algorithm with 144 byte block size
      (QCryptographicHash::RealSha3_224/Keccak_224) and a key that's
      exactly 144 octets long.

* 0147fc61760 QBasicAtomic: fix UB (signed overflow) in some operators
    * Fixed signed arithmetic in prefix increment and decrement and in
      += and -= to be in two's complement, matching std::atomic's
      behavior, rather than overflowing (causing undefined behavior).

* edaad186181 SQLite: Update SQLite to v3.53.4
    * Updated SQLite to v3.53.4

* f8f06837b5f Upgrade Harfbuzz to 14.3.0
    * Upgraded Harfbuzz to version 14.3.0

* afd7caf1898 Upgrade md4c to 0.5.3
    * Upgraded md4c to version 0.5.3.

### qtmultimedia
* 7ce26311b GStreamer: Disable WMV/WMA encoding support
    * Removed WMV/WMA encoding support from the GStreamer backend

### qtconnectivity
* aed50900 Windows: allow to create Bluetooth classes in secondary
  threads
    * Bluetooth classes on Windows can now be created and used in
      secondary threads.

### qt3d
* a4785555e Update assimp to 6.0.5
    * Updated assimp to 6.0.5

### qtimageformats
* 134a0657 Update bundled libtiff to version 4.7.2
    * Bundled libtiff was updated to version 4.7.2

* c5f06c8c QTiffHandler: fix default strip sizes for 64-bit and float
  images
    * Fixed a bug that caused RGBA64 and float-based formats to be
      written with 8KiB strips, severely limiting the compression
      achievable, compared the 4MiB strip size that the TIFF plugin uses
      for all other formats.

### qtnetworkauth
* 3a8066c Increase default generated state parameter size from 8 to 32
    * Default generated state parameter size is increased from 8 to 32
      characters.

### qtquick3d
* 894a31a86 Update Assimp to v6.0.5
    * Updated Assimp to v6.0.5

### qtgrpc
* afe60e7f Add correctly named Q_PROPERTY for repeated message fields
    * Added correctly named Q_PROPERTY declarations for repeated message
      fields. The old *Data-suffixed properties are deprecated and will
      be removed in Qt 7.


Fixes
-----

### qtbase
* [QTBUG-145030](https://qt-project.atlassian.net/browse/QTBUG-145030) ASSERT: "!std::isnan(value)" in
QQuickColorValueType::alpha
* [QTBUG-145911](https://qt-project.atlassian.net/browse/QTBUG-145911) QTextEngine does not set HarfBuzz language from system
locale, causing incorrect OpenType localized glyph substitution (locl
feature)
* [QTBUG-145584](https://qt-project.atlassian.net/browse/QTBUG-145584) QMenu doesn't repaint a sunken submenu item after
releasing the mouse button
* [QTBUG-145713](https://qt-project.atlassian.net/browse/QTBUG-145713) xamples\grpc\vehicle\vehicle_server.exe : fatal error
LNK1120: 3 unresolved externals
* [QTBUG-129280](https://qt-project.atlassian.net/browse/QTBUG-129280) QScreen::grabWindow does not behave consistently across
platforms
* [QTBUG-145805](https://qt-project.atlassian.net/browse/QTBUG-145805) QNX QPA: handleTouchEvent delivers touch points from all
windows instead of per-window
* [QTBUG-146145](https://qt-project.atlassian.net/browse/QTBUG-146145) [REG 6.11.0->6.11.1] can not compile examples with qmake
on Android armv7 and x86 targets
* [QTBUG-146013](https://qt-project.atlassian.net/browse/QTBUG-146013) Compile error in QByteArray move ctor on Clang 15 with
GCC 15 --gcc-toolchain
* [QTBUG-59638](https://qt-project.atlassian.net/browse/QTBUG-59638) QMultiHash and QMultiMap element insertion order
* [QTBUG-141132](https://qt-project.atlassian.net/browse/QTBUG-141132) Warning from qmetatype.h when instantiated from
qinputcontrol.cpp
* [QTBUG-146163](https://qt-project.atlassian.net/browse/QTBUG-146163) Windows arm64 msvc2026:
tst_qstandardpaths::testFindExecutable(win8-logo) fails
* [QTBUG-85355](https://qt-project.atlassian.net/browse/QTBUG-85355) QStyleHints misleading documentation
* [QTBUG-122969](https://qt-project.atlassian.net/browse/QTBUG-122969) QTextCursor::movePosition(NextCharacter, MoveAnchor)
does not move cursor if a text is selected
* [QTBUG-143193](https://qt-project.atlassian.net/browse/QTBUG-143193) Documentation of overloaded signal/slots is obsolete
* [QTBUG-142735](https://qt-project.atlassian.net/browse/QTBUG-142735) QML iPad app UI freezes when moving to an external
display
* [QTBUG-146116](https://qt-project.atlassian.net/browse/QTBUG-146116) [REG 6.10.3 -> 6.11.0] QTabBar does not always update
hovered tabs in vertical mode
* [QTBUG-146574](https://qt-project.atlassian.net/browse/QTBUG-146574) QMainWindow does not show all dock widgets in Projects
mode ("projects mode" lacks kit selection / projects settings)
* [QTBUG-146636](https://qt-project.atlassian.net/browse/QTBUG-146636) [REG 6.11.0->6.11.1] Dragging QQuickWidget or
QWebEngineView on top of OpenGL Widget crashes Qt Widget Designer on
Windows
* [QTBUG-145383](https://qt-project.atlassian.net/browse/QTBUG-145383) crash when two QQuickWidget instances are initialized
before show
* [QTBUG-146670](https://qt-project.atlassian.net/browse/QTBUG-146670) qtestsupport_core.cpp static_assert on
std::atomic<std::chrono::milliseconds>::is_always_lock_free fails on
MIPS32
* [QTBUG-146651](https://qt-project.atlassian.net/browse/QTBUG-146651) Rename the app-examples-template.qdoc file to app-
examples.qdoc.template
* [QTBUG-146675](https://qt-project.atlassian.net/browse/QTBUG-146675) after requesting markdown via QFileDialog
setMimeTypeFilters it's omitted
* [QTBUG-137286](https://qt-project.atlassian.net/browse/QTBUG-137286) Do REUSE.toml license checks earlier
* [QTBUG-126191](https://qt-project.atlassian.net/browse/QTBUG-126191) Clipboard images lose transparency / alpha channel
* [QTBUG-146553](https://qt-project.atlassian.net/browse/QTBUG-146553) Crash in Vulkan example on Linux using Intel video
controller
* [QTBUG-126980](https://qt-project.atlassian.net/browse/QTBUG-126980) Drag-n-drop from zip file opened in Windows Explorer is
empty
* [QTBUG-146652](https://qt-project.atlassian.net/browse/QTBUG-146652) UB in QArrayDataPointer::operator-> (was:
tst_QArrayData::arrayOps fail with RHEL 10's compiler)
* [QTBUG-88704](https://qt-project.atlassian.net/browse/QTBUG-88704) QCollatorSortKey is not working properly without ICU
support
* [QTBUG-136223](https://qt-project.atlassian.net/browse/QTBUG-136223) Qt6 not working with openssl 3.5.0
* [QTBUG-146785](https://qt-project.atlassian.net/browse/QTBUG-146785) [REG 6.12.0->6.12.0] (analogclock) example not compiled
with shadow build Qt binaries
* [QTBUG-146880](https://qt-project.atlassian.net/browse/QTBUG-146880) qtbase build failure with LLVM-MinGW 22.1.1: std::sort
used with non-random-access QTaggedIterator in tst_qvariant
* [QTBUG-146893](https://qt-project.atlassian.net/browse/QTBUG-146893) Color emoji glyphs are clipped on Windows (COLRv1)
* [QTBUG-145221](https://qt-project.atlassian.net/browse/QTBUG-145221) Build with OpenSSL 4.0 is broken
* [QTBUG-146744](https://qt-project.atlassian.net/browse/QTBUG-146744) QDate roundtrip parsing fails with 2-digit year format
for Jalali and IslamicCivil calendars
* [QTBUG-143926](https://qt-project.atlassian.net/browse/QTBUG-143926) QNAM/QNetworkRequest/Reply should emit signal
QNetworkReply::finished regardless if the connection succeeded or
failed.
* [QTBUG-146900](https://qt-project.atlassian.net/browse/QTBUG-146900) ThreadSanitizer false positives in QObject signal/slot
machinery — missing __tsan_release / __tsan_acquire on lock-free atomic
pointers
* [QTBUG-146665](https://qt-project.atlassian.net/browse/QTBUG-146665) Reg: Qt Widgets Designer: cannot get context menu on
disabled widget
* [QTBUG-146666](https://qt-project.atlassian.net/browse/QTBUG-146666) Reg: Disabled widgets no longer receive context menu
events (in event filters)
* [QTBUG-130317](https://qt-project.atlassian.net/browse/QTBUG-130317) Logical Text Cursor Movement not Consistent with Layout
Base Direction
* [QTBUG-145937](https://qt-project.atlassian.net/browse/QTBUG-145937) QCompleter custom popup is incorrectly located in RTL
mode
* [QTBUG-146974](https://qt-project.atlassian.net/browse/QTBUG-146974) QThread::idealProcessorCount limited due to Windows
processor group affinity
* [QTBUG-147039](https://qt-project.atlassian.net/browse/QTBUG-147039) QNetworkRequest::setTransferTimeout() stops working
after HTTP redirect
* [QTBUG-146919](https://qt-project.atlassian.net/browse/QTBUG-146919) windeployqt re-broken in MSVC integration
* [QTBUG-134518](https://qt-project.atlassian.net/browse/QTBUG-134518) [REG 6.8 -> 6.9] Crash in
QDBusMenuBar::unregisterMenuBar when closing app
* [QTBUG-145464](https://qt-project.atlassian.net/browse/QTBUG-145464) Font hinting forcefully disabled on Linux X11 when X
resources configuration is missing
* [QTBUG-144388](https://qt-project.atlassian.net/browse/QTBUG-144388) UB in QXcbVirtualDesktop
* [QTBUG-138383](https://qt-project.atlassian.net/browse/QTBUG-138383) Reg->6.10: QKeySequence::isEmpty() changed semantics
and/or Windows platform Quit key changed
* [QTBUG-141501](https://qt-project.atlassian.net/browse/QTBUG-141501) tst_baseline_painting: testRasterRGBA32FPM generates NaN
pixels
* [QTBUG-147209](https://qt-project.atlassian.net/browse/QTBUG-147209) Undocked QDockWidget prevents QMainWindow contents from
responding to resize
* [QTBUG-147255](https://qt-project.atlassian.net/browse/QTBUG-147255) Regression in Qt 6.11.1: resources embedded via <img
src=":/..."> in QLabel rich text are incorrectly shared between labels
* [QTBUG-142087](https://qt-project.atlassian.net/browse/QTBUG-142087) SVGs in rich-text (HTML) QTooltips not rendered smoothly
at all device pixel ratios (Windows)
* [QTBUG-141889](https://qt-project.atlassian.net/browse/QTBUG-141889) QDuplicateTracker::clear() may corrupt the heap?
* [QTBUG-147218](https://qt-project.atlassian.net/browse/QTBUG-147218) QSslSocket (SecureTransport): SSLClose() writes to dead
socket when peer RSTs during TLS shutdown
* [QTBUG-146124](https://qt-project.atlassian.net/browse/QTBUG-146124) [Android] Broken legacyPackaging configuration
* [QTBUG-147037](https://qt-project.atlassian.net/browse/QTBUG-147037) QXmlStreamReader wastes memory space storing
prefix/qname/name separately
* [QTBUG-146578](https://qt-project.atlassian.net/browse/QTBUG-146578) failure: tst_QFile::invalidFile(x11)
* [QTBUG-146845](https://qt-project.atlassian.net/browse/QTBUG-146845) Qt components that use <winrt/base.h> trigger errors on
MSVC 19.51+
* [QTBUG-145444](https://qt-project.atlassian.net/browse/QTBUG-145444) Context menu is not visible if opened from secondary
screen
* [QTBUG-134017](https://qt-project.atlassian.net/browse/QTBUG-134017) QWidget does not correctly set the geometry on multi-
screen environments if called from showEvent
* [QTBUG-147309](https://qt-project.atlassian.net/browse/QTBUG-147309) HTTP/2: complete reply fails with ProtocolFailure and
truncated body on a stray DATA frame after END_STREAM
* [QTBUG-145882](https://qt-project.atlassian.net/browse/QTBUG-145882) "Windows" Style Missing Semi Checked Checkbox Icon
* [QTBUG-147161](https://qt-project.atlassian.net/browse/QTBUG-147161) Schannel backend corrupts all other on-going TLS
handshakes when starting a new one
* [QTBUG-147228](https://qt-project.atlassian.net/browse/QTBUG-147228) QMetalLayer displayLock triggers spurious TSan "double
lock of a mutex" on macOS
* [QTBUG-147406](https://qt-project.atlassian.net/browse/QTBUG-147406) Constructing QBindable from QProperty makes binaries
depend on the exact-versioned private symbol
QUntypedPropertyBinding(QPropertyBindingPrivate*)
* [QTBUG-117514](https://qt-project.atlassian.net/browse/QTBUG-117514) QFuture::then marked as private
* [QTBUG-147355](https://qt-project.atlassian.net/browse/QTBUG-147355) FAIL!  :
tst_QWebSocket::authenticationRequired(SslServer:connection-
close,Client:callback-ok) The computed value is expected to be equal to
the baseline, but is not
* [QTBUG-147385](https://qt-project.atlassian.net/browse/QTBUG-147385) SecureTransport: SSLClose() writes to invalid socket
when connection is already lost
* [QTBUG-133976](https://qt-project.atlassian.net/browse/QTBUG-133976) Proper handling of GET request with body in case of
chained redirections
* [QTBUG-146884](https://qt-project.atlassian.net/browse/QTBUG-146884) TextEdit cursorDelegate not repositioned after
QTextDocument::clear()
* [QTBUG-146917](https://qt-project.atlassian.net/browse/QTBUG-146917) Application fails to close if the last used item was a
QComboBox used as a delegate
* [QTBUG-147009](https://qt-project.atlassian.net/browse/QTBUG-147009) Quadratic behaviour in
QXmlStreamReaderPrivate::resolveTag()
* [QTBUG-147219](https://qt-project.atlassian.net/browse/QTBUG-147219) QXmlStreamReader fails to reject duplicate attributes
sometimes
* [QTBUG-147578](https://qt-project.atlassian.net/browse/QTBUG-147578) qt6_deploy_runtime_dependencies fails with relative
install prefix
* [QTBUG-147507](https://qt-project.atlassian.net/browse/QTBUG-147507) Make Qt SQL examples self-contained
* [QTBUG-147510](https://qt-project.atlassian.net/browse/QTBUG-147510) Make Qt OpenGL examples self-contained
* [QTBUG-147511](https://qt-project.atlassian.net/browse/QTBUG-147511) Make Vulkan examples self-contained
* [QTBUG-147326](https://qt-project.atlassian.net/browse/QTBUG-147326) get_filename_component(REALPATH) doesn't prepend drive-
letter in cmake 4.0+ for drive-less paths
* [QTBUG-146818](https://qt-project.atlassian.net/browse/QTBUG-146818) [Reg 6.8.4 -> 6.8.7][Win 11 style] QSS: background-color
for QTextEdit:hover gets applied to the border instead of the background
* [QTBUG-138401](https://qt-project.atlassian.net/browse/QTBUG-138401) [REG dev] Windows11 Style: Check-boxes' drawing
regression
* [QTBUG-138495](https://qt-project.atlassian.net/browse/QTBUG-138495) QCommonStyle subElementRect HeaderLabel QRect size
* [QTBUG-146948](https://qt-project.atlassian.net/browse/QTBUG-146948) Update llvm-mingw to 22.1.1 fails: qtbase
tst_Collections::map() 'j1 == map1.find("1") && k1 == j1' returned
FALSE. ()
* [QTBUG-145948](https://qt-project.atlassian.net/browse/QTBUG-145948) QMultiMap has incorrect behavior with LLVM libc++
starting with 22
* [QTBUG-147588](https://qt-project.atlassian.net/browse/QTBUG-147588) QMetaType::fromName() for const/non-const pointers
affected by registration order
* [QTBUG-147602](https://qt-project.atlassian.net/browse/QTBUG-147602) macOS: QImage::toCGImage() crashes in CGImageCreate with
custom QColorSpace
* [QTBUG-147233](https://qt-project.atlassian.net/browse/QTBUG-147233) Crash in QBackingStoreDefaultCompositor when using
stereo widget and other non-stereo textured widget
* [QTBUG-147653](https://qt-project.atlassian.net/browse/QTBUG-147653) REG->6.12: Mouse rotation broken in OSM demo ( QML /
QFlags handling)
* [QTBUG-137304](https://qt-project.atlassian.net/browse/QTBUG-137304) Qt Quick: Broken behaviour on Windows 11 with
Qt.ExpandedClientAreaHint and Qt.NoTitleBarBackgroundHint
* [QTBUG-146563](https://qt-project.atlassian.net/browse/QTBUG-146563) QHash does not compile on some incomplete types, while
QMap does
* [QTBUG-147612](https://qt-project.atlassian.net/browse/QTBUG-147612) iOS for arm64e fails
* [QTBUG-147580](https://qt-project.atlassian.net/browse/QTBUG-147580) QODBC authentication fails with special characters in MS
SQL Server passwords
* [QTBUG-141838](https://qt-project.atlassian.net/browse/QTBUG-141838) QODBC Oracle: “invalid username/password”
* [QTBUG-145216](https://qt-project.atlassian.net/browse/QTBUG-145216) Hanging after retry connect websocket server
* [QTBUG-144700](https://qt-project.atlassian.net/browse/QTBUG-144700) FTBFS clang-21 with libc++
* [QTBUG-147328](https://qt-project.atlassian.net/browse/QTBUG-147328) QNetworkReply hangs after clearConnectionCache() during
active request
* [QTBUG-144006](https://qt-project.atlassian.net/browse/QTBUG-144006) Android: Drag and drop does not work using DragHandler
and DropArea.
* [QTBUG-76544](https://qt-project.atlassian.net/browse/QTBUG-76544) DropArea doesn't work on Android
* [QTBUG-112170](https://qt-project.atlassian.net/browse/QTBUG-112170) QSystemTrayIcon::messageClicked also invoked if clicked
on foreign notifications
* [QTBUG-147754](https://qt-project.atlassian.net/browse/QTBUG-147754) QCollator does not preserve collation options when
detaching
* [QTBUG-145723](https://qt-project.atlassian.net/browse/QTBUG-145723) wasm QOpenGLContext::doneCurrent inconsistent behavior
* [QTBUG-84033](https://qt-project.atlassian.net/browse/QTBUG-84033) Android 32bit - No large files support
* [QTBUG-141461](https://qt-project.atlassian.net/browse/QTBUG-141461) UnsatisfiedLinkError exception for missing Android ABI
in QtLoader
* [QTBUG-147866](https://qt-project.atlassian.net/browse/QTBUG-147866) QOpenGLTexture: multisample FBO attachments fail to
allocate on Mesa (EXT-DSA glTextureStorage2DMultisampleEXT ->
GL_INVALID_OPERATION)
* [QTBUG-147782](https://qt-project.atlassian.net/browse/QTBUG-147782) Behavior of feature "openssl-hash"
* [QTBUG-147785](https://qt-project.atlassian.net/browse/QTBUG-147785) New memory leaks with Qt 6.12.0-beta1
* [QTBUG-146982](https://qt-project.atlassian.net/browse/QTBUG-146982) Cannot run Android examples from the command line on
Windows
* [QTBUG-147324](https://qt-project.atlassian.net/browse/QTBUG-147324) QXmlStreamReader doesn't flag recursion for enties
expanded via QXmlStreamEntityResolver
* [QTBUG-147320](https://qt-project.atlassian.net/browse/QTBUG-147320) QXmlStreamEntityResolver is under-documented
* [QTBUG-147191](https://qt-project.atlassian.net/browse/QTBUG-147191) CVE-2026-19248 - QDom unbounded recursion on dtor and
clear()
* [QTBUG-142321](https://qt-project.atlassian.net/browse/QTBUG-142321) Potential Data Race in QReadWriteLock
* [QTBUG-148481](https://qt-project.atlassian.net/browse/QTBUG-148481) Android: QDesktopServices::openUrl() corrupts URLs
containing percent-encoded characters in the query (%20 becomes a
literal space in the ACTION_VIEW intent)
* [QTBUG-145092](https://qt-project.atlassian.net/browse/QTBUG-145092) showMaximized()/showNormal() fail to sync Win32 window
state for frameless windows
* [QTBUG-129791](https://qt-project.atlassian.net/browse/QTBUG-129791) Issue with Showmaximized function in case of QMainWindow
with Qt::FramelessWindowHint flag
* [QTBUG-148364](https://qt-project.atlassian.net/browse/QTBUG-148364) QMachOParser misses size validation on some codepaths
* [QTBUG-148076](https://qt-project.atlassian.net/browse/QTBUG-148076) Aligning a QPixmap inside a QLabel (basically
QLabel::setPixmap + QLabel::setAlignment) is broken if DPR is not 1
* [QTBUG-146766](https://qt-project.atlassian.net/browse/QTBUG-146766) Incomplete Documentation for QHash::emplace
* [QTBUG-147418](https://qt-project.atlassian.net/browse/QTBUG-147418) Integer-overflow in QJalaliCalendar::isLeapYear
* [QTBUG-147634](https://qt-project.atlassian.net/browse/QTBUG-147634) lupdate.exe requires elevation (UAC) on latest version
of Windows 11
* [QTBUG-148548](https://qt-project.atlassian.net/browse/QTBUG-148548) QTabWidget tab font color is ignored
* [QTBUG-147817](https://qt-project.atlassian.net/browse/QTBUG-147817) QOpenGL2PaintEngineEx and QRhiGles2 renderers conflict
over vertex-attribute-array state
* [QTBUG-148564](https://qt-project.atlassian.net/browse/QTBUG-148564) QSet::unite(QSet&&) doesn't actually move from other
* [QTBUG-142560](https://qt-project.atlassian.net/browse/QTBUG-142560) [REG 6.9.3 -> 6.10] Screen.pixelDensity returns
inconsistent values on Android when rotating and on foldable devices
depending on initial state
* [QTBUG-143161](https://qt-project.atlassian.net/browse/QTBUG-143161) Keyboard takes full screen on android and there is no
way to hide the extra features
* [QTBUG-145034](https://qt-project.atlassian.net/browse/QTBUG-145034) [REG] Application CMake configuration fails for static
FFmpeg
* [QTBUG-146029](https://qt-project.atlassian.net/browse/QTBUG-146029) Linux: qt-configure-module in wasm_singlethreaded
contains incorrect path separators
* [QTBUG-143699](https://qt-project.atlassian.net/browse/QTBUG-143699) Crash in QOpenGLFunctions::glClear in various Controls
auto tests
* [QTBUG-146558](https://qt-project.atlassian.net/browse/QTBUG-146558) QVectorND are equality-comparable, but not hashable
* [QTBUG-120533](https://qt-project.atlassian.net/browse/QTBUG-120533) Various runtime warnings about Wayland text input
* [QTBUG-141701](https://qt-project.atlassian.net/browse/QTBUG-141701) [a11y] App language is not transparent to Screen Reader
* [QTBUG-146633](https://qt-project.atlassian.net/browse/QTBUG-146633) make-xml-parser.sh wasn't run in some time, and fails
when run
* [QTBUG-146686](https://qt-project.atlassian.net/browse/QTBUG-146686) Windows accessibility: Checkbox state change not
announced when using nextCheckState function or tristate: true
* [QTBUG-146575](https://qt-project.atlassian.net/browse/QTBUG-146575) Non-namespaced include guards abound in Qt sources
* [QTBUG-145703](https://qt-project.atlassian.net/browse/QTBUG-145703) LNK2005 in consumers defining
QT_DISABLE_DEPRECATED_BEFORE linking static builds
* [QTBUG-145975](https://qt-project.atlassian.net/browse/QTBUG-145975) tst_selftests fails on QNX 8.0: libc++ newlocale stub
crashes sub-binaries with LC_ALL=en_US.UTF-8
* [QTBUG-146986](https://qt-project.atlassian.net/browse/QTBUG-146986) QObject: TSAN data race between resizeSignalVector() and
doActivate()
* [QTBUG-144929](https://qt-project.atlassian.net/browse/QTBUG-144929) QObject::disconnect(const Connection &) const_cast<>s
its argument
* [QTBUG-132945](https://qt-project.atlassian.net/browse/QTBUG-132945) QDuplicateTracker::clear() leaks memory
* [QTBUG-110669](https://qt-project.atlassian.net/browse/QTBUG-110669) Q/Date/Time: align unquoting format strings for both
from/toString()
* [QTBUG-145768](https://qt-project.atlassian.net/browse/QTBUG-145768) tst_QDateTime::springForward:Asia/Singapore fails on
some platforms
* [QTBUG-146602](https://qt-project.atlassian.net/browse/QTBUG-146602) [VxWorks] tst_qlatin1stringmatcher fails to buld on
26.03
* [PYSIDE-3362](https://qt-project.atlassian.net/browse/PYSIDE-3362) QTreeWidget documentation snippets are not valid python
* [QTBUG-145789](https://qt-project.atlassian.net/browse/QTBUG-145789) Qt Fortification options vs. -Werror
* [QTBUG-147364](https://qt-project.atlassian.net/browse/QTBUG-147364) windeployqt fails due to file use by another process
* [QTBUG-143289](https://qt-project.atlassian.net/browse/QTBUG-143289) plasmashell crashes in
QHttp2ProtocolHandler::handleHeadersReceived() and
QHttpHeaderParser::setStatusCode
* [QTBUG-145812](https://qt-project.atlassian.net/browse/QTBUG-145812) SIGSEGV / use-after-free in QHttp2Stream::handleHEADERS
when processing HTTP/2 HEADERS frames (plasmashell, kioworker)
* [QTBUG-146206](https://qt-project.atlassian.net/browse/QTBUG-146206) RHEL 10.0: tst_qvulkan crashes with SIGABRT on Wayland
during vulkanWindowRenderer test
* [QTBUG-147475](https://qt-project.atlassian.net/browse/QTBUG-147475) Render target caching issues with D3D11 rhi backend
* [QTBUG-144923](https://qt-project.atlassian.net/browse/QTBUG-144923) QUrlQuery's move constructor is out-of-line (should be
inline)
* [QTBUG-145786](https://qt-project.atlassian.net/browse/QTBUG-145786) Android A11y: keyboard opens on TextInput focus when
Talkback enabled
* [QTBUG-147685](https://qt-project.atlassian.net/browse/QTBUG-147685) GCC internal compiler error: in QRangeModelAdapter
RowGetter with -Wmismatched-tags (gcc 14.2–17, C++26)
* [QTBUG-120167](https://qt-project.atlassian.net/browse/QTBUG-120167) Reg->6.7: QComboxbox hover is broken
* [QTBUG-147798](https://qt-project.atlassian.net/browse/QTBUG-147798) tst_QFontDatabase::systemFixedFonts fails on RHEL
* [QTBUG-147136](https://qt-project.atlassian.net/browse/QTBUG-147136) QDoc: Wildcard patterns in `excludefiles` configuration
variable do not work as expected
* [QTBUG-147323](https://qt-project.atlassian.net/browse/QTBUG-147323) QXmlStreamReader doesn't enforce entityExpansionLimit
for enties expanded via QXmlStreamEntityResolver
* [QTBUG-141230](https://qt-project.atlassian.net/browse/QTBUG-141230) Revert the using of QThread::isMainThread() in
qpixmap.cpp
* [QTBUG-146190](https://qt-project.atlassian.net/browse/QTBUG-146190) QWindowsIntegration constructor creates QPixmap before
platformIntegration() is set — regression Qt 6.6 → 6.8, ACCESS_VIOLATION
in qt_pixmap_thread_test() when hosting multiple Qt ActiveX controls
* [QTBUG-118858](https://qt-project.atlassian.net/browse/QTBUG-118858) On Android widget type is not announced by talkback
* [QTBUG-137426](https://qt-project.atlassian.net/browse/QTBUG-137426) use cups printing protocol data error
* [QTBUG-141988](https://qt-project.atlassian.net/browse/QTBUG-141988) tst_http2::goaway() crash on CI
* [QTBUG-133102](https://qt-project.atlassian.net/browse/QTBUG-133102) Adwaita theme icons not found on Ubuntu 24.04.1

### qtsvg
* [QTBUG-146132](https://qt-project.atlassian.net/browse/QTBUG-146132) QSvgAbstractAnimatedProperty's use of QHash is not
thread-safe
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.
* [QTBUG-146726](https://qt-project.atlassian.net/browse/QTBUG-146726) parseFont() creates and appends a QSvgFontStyle even if
everything is set to `inherit`
* [QTBUG-146716](https://qt-project.atlassian.net/browse/QTBUG-146716) QSvgHandler::parseFont() is ... fishy
* [QTBUG-148476](https://qt-project.atlassian.net/browse/QTBUG-148476) Tag <use> is not able to load id from other file

### qtdeclarative
* [QTBUG-145383](https://qt-project.atlassian.net/browse/QTBUG-145383) crash when two QQuickWidget instances are initialized
before show
* [QTBUG-142207](https://qt-project.atlassian.net/browse/QTBUG-142207) Windows: qml results in "Device loss detected in
Present()" with blank window when scaling is used
* [QTBUG-142153](https://qt-project.atlassian.net/browse/QTBUG-142153) FlexboxLayout: Layout.XMargin attached properties scale
the child
* [QTBUG-112349](https://qt-project.atlassian.net/browse/QTBUG-112349) ListView SnapOneItem positioning wrong index in resize
time
* [QTBUG-44449](https://qt-project.atlassian.net/browse/QTBUG-44449) Changing the size of the window can cause the currently
visible ListView item to change
* [QTBUG-144701](https://qt-project.atlassian.net/browse/QTBUG-144701) [REG 6.10.2 → 6.10.3, 6.11] Valid QML code fails to load
with wrong error about property assignment
* [QTBUG-146038](https://qt-project.atlassian.net/browse/QTBUG-146038) FAIL!  : tst_QQuickMenu::iOS::subMenuFlipsPositionWhenOu
tOfBounds(PopupType::Window) Compared doubles are not the same (fuzzy
compare)
* [QTBUG-144006](https://qt-project.atlassian.net/browse/QTBUG-144006) Android: Drag and drop does not work using DragHandler
and DropArea.
* [QTBUG-133655](https://qt-project.atlassian.net/browse/QTBUG-133655) [REG 6.8.1->6.8.2] QML color dialog uses wrong button
style
* [QTBUG-146555](https://qt-project.atlassian.net/browse/QTBUG-146555) qtquickview_kotlin and qtabstractlistmodel_kotlin fails
to compile
* [QTBUG-144856](https://qt-project.atlassian.net/browse/QTBUG-144856) Check and fix Q_ALLOCA_VAR usage in QtDeclarative
* [QTBUG-144350](https://qt-project.atlassian.net/browse/QTBUG-144350) AbstractButton based types doesn't toggle automatically
with Screenreader
* [QTBUG-141114](https://qt-project.atlassian.net/browse/QTBUG-141114) Qml: Binding on deferred property not reliable
* [QTBUG-145030](https://qt-project.atlassian.net/browse/QTBUG-145030) ASSERT: "!std::isnan(value)" in
QQuickColorValueType::alpha
* [QTBUG-146648](https://qt-project.atlassian.net/browse/QTBUG-146648) TextEdit with RichText extends anchor underline through
tab character to following text
* [QTBUG-145217](https://qt-project.atlassian.net/browse/QTBUG-145217) Quick Control Combobox dropdown not styled correctly for
macOS style
* [QTBUG-146210](https://qt-project.atlassian.net/browse/QTBUG-146210) QQmlEngine: calling addImportPath() causes
asynchronously loading components to never become ready
* [QTBUG-146770](https://qt-project.atlassian.net/browse/QTBUG-146770) ComboBox does not propagate font size to popup
* [QTBUG-146881](https://qt-project.atlassian.net/browse/QTBUG-146881) QML easingCurve property name mismatch in code example
* [QTBUG-142032](https://qt-project.atlassian.net/browse/QTBUG-142032) FlexboxLayout with wrap property misaligns children
* [QTBUG-146847](https://qt-project.atlassian.net/browse/QTBUG-146847) `instanceof` can fail for QML composite types in multi-
engine environment
* [QTBUG-123771](https://qt-project.atlassian.net/browse/QTBUG-123771) QQmlComponent seems unable to create a component that
has a required alias
* [QTBUG-146920](https://qt-project.atlassian.net/browse/QTBUG-146920) [REG 6.11.0 -> 6.11.1]  qmlformat: parse failure when
object id begins with an underscore
* [QTBUG-145611](https://qt-project.atlassian.net/browse/QTBUG-145611) "Go To C++ Definition" does not find file
* [QTBUG-140453](https://qt-project.atlassian.net/browse/QTBUG-140453) Changing alignments of a TextEdit (or TextArea) does not
refresh its cursorDelegate or content
* [QTBUG-146127](https://qt-project.atlassian.net/browse/QTBUG-146127) Accessible.labelFor: null crashes
* [QTBUG-146959](https://qt-project.atlassian.net/browse/QTBUG-146959) A11y-related crash in QQuickScrollbar
* [QTBUG-147178](https://qt-project.atlassian.net/browse/QTBUG-147178) Error  error: reference to 'Default' is ambiguous in
qqmljstyperesolver
* [QTBUG-146887](https://qt-project.atlassian.net/browse/QTBUG-146887) Popup.Window - MouseArea.pressed Drops to false When
Mouse Moves While Button Held
* [QTBUG-146823](https://qt-project.atlassian.net/browse/QTBUG-146823) [REG 6.11.1->6.12.0] demos\lightningviewer not compiled
with MinGW or MSVC
* [QTBUG-139770](https://qt-project.atlassian.net/browse/QTBUG-139770) nested directories in QML modules dont work with
"internal" types
* [QTBUG-143877](https://qt-project.atlassian.net/browse/QTBUG-143877) deploying qml module with JS file does not work
* [QTBUG-133679](https://qt-project.atlassian.net/browse/QTBUG-133679) qmlformat: Post-Comment moves ',' to next line
* [QTBUG-123386](https://qt-project.atlassian.net/browse/QTBUG-123386) QmlFormat. Incorrect handling of some comments
* [QTBUG-146759](https://qt-project.atlassian.net/browse/QTBUG-146759) qmllint: import rule
* [QTBUG-147277](https://qt-project.atlassian.net/browse/QTBUG-147277) StyledText: <span> breaks paragraph direction detection
* [QTBUG-142578](https://qt-project.atlassian.net/browse/QTBUG-142578) QQmlApplicationEngine crashes with
loadFromModule("QtQuick", "Window")
* [QTBUG-147396](https://qt-project.atlassian.net/browse/QTBUG-147396) QuickShapes: failed rendering for certain paths with
curve renderer
* [QTBUG-
147315](https://qt-project.atlassian.net/browse/QTBUG-147315) tst_QQuickPopup::FluentWinUI3::popupWindowRepositionOnImplicitSiz
eChange is flaky on Windows
* [QTBUG-147215](https://qt-project.atlassian.net/browse/QTBUG-147215) qmltc errors out on non-type-compilation-relevant
warnings
* [QTBUG-147450](https://qt-project.atlassian.net/browse/QTBUG-147450) Button with action emits clicked signal twice when
action's enabled property is bound to dialog's visible property
* [QTBUG-146908](https://qt-project.atlassian.net/browse/QTBUG-146908) SpinBox increase() not callable from QML
* [QTBUG-130605](https://qt-project.atlassian.net/browse/QTBUG-130605) Invalid alias target location unless I bind it
* [QTBUG-146732](https://qt-project.atlassian.net/browse/QTBUG-146732) Repeated $/addBuildDirs notifications does not refresh
.qmlls.build.ini for existing build paths.
* [QTBUG-146733](https://qt-project.atlassian.net/browse/QTBUG-146733) No workspace/semanticTokens/refresh sent after
$/addBuildDirs
* [QTBUG-147667](https://qt-project.atlassian.net/browse/QTBUG-147667) Bevel property of PathRectangle does not work
* [QTBUG-
145432](https://qt-project.atlassian.net/browse/QTBUG-145432) QRhiD3D11::executeCommandBuffer(QD3D11CommandBuffer::Command::Upd
ateSubRes) touch nullptr crash
* [QTBUG-147713](https://qt-project.atlassian.net/browse/QTBUG-147713) qmlformat: indent error
* [QTBUG-145767](https://qt-project.atlassian.net/browse/QTBUG-145767) qmlls: rangeformatting does wrong indentations
* [QTBUG-147810](https://qt-project.atlassian.net/browse/QTBUG-147810) qmlformat breaks indentation for if statements without
braces when pragma ComponentBehavior: Bound is present
* [QTBUG-111207](https://qt-project.atlassian.net/browse/QTBUG-111207) Android content URIs do not work with Image
* [QTBUG-76544](https://qt-project.atlassian.net/browse/QTBUG-76544) DropArea doesn't work on Android
* [QTBUG-103064](https://qt-project.atlassian.net/browse/QTBUG-103064) tst_DragHandler::touchDragMulti fails on Android
* [QTBUG-103082](https://qt-project.atlassian.net/browse/QTBUG-103082) tst_qquickdrag tests fail on Android
* [QTBUG-103083](https://qt-project.atlassian.net/browse/QTBUG-103083) tst_QQuickDropArea::signalOrder() fails on Android
* [QTBUG-138621](https://qt-project.atlassian.net/browse/QTBUG-138621) Crash in qv4mm during destruction
* [QTBUG-134687](https://qt-project.atlassian.net/browse/QTBUG-134687) Crash in GC MarkStack drain step
* [QTBUG-147846](https://qt-project.atlassian.net/browse/QTBUG-147846) QtQuick.Dialogs FileDialog in a QQuickWidget shows a
stray visible "Offscreen" window
* [QTBUG-147153](https://qt-project.atlassian.net/browse/QTBUG-147153) QML crashes trying to insert a member
* [QTBUG-147812](https://qt-project.atlassian.net/browse/QTBUG-147812) qmlformat: Essential semicolon mode adds semicolon if a
comment exists on the next line
* [QTBUG-142050](https://qt-project.atlassian.net/browse/QTBUG-142050) TouchPoint: startX and startY update inappropriately
during dragging, if window contents are transformed
* [QTBUG-147807](https://qt-project.atlassian.net/browse/QTBUG-147807) Qt crashes (SIGSEGV) after "Resource update batch pool
exhausted (max is 64)" warning with 64+ QQuickWidgets or windows where
all Text items are hidden
* [QTBUG-144377](https://qt-project.atlassian.net/browse/QTBUG-144377) qmllint suggests to remove an import that is actually
used
* [QTBUG-148578](https://qt-project.atlassian.net/browse/QTBUG-148578) QtDeclarative fails yocto build
* [QTBUG-145967](https://qt-project.atlassian.net/browse/QTBUG-145967) Crash in QQmlEngine::importModule
* [QTBUG-146013](https://qt-project.atlassian.net/browse/QTBUG-146013) Compile error in QByteArray move ctor on Clang 15 with
GCC 15 --gcc-toolchain
* [QTBUG-143920](https://qt-project.atlassian.net/browse/QTBUG-143920) Fix XFAIL - openSUSE 16.0 qtdeclarative -
tst_QQuickColorDialogImpl::moveColorPickerHandle()
'qAbs(colorPicker->color().green() - QColorConstants::Cyan.green()) < 3'
returned FALSE
* [QTBUG-142386](https://qt-project.atlassian.net/browse/QTBUG-142386) openSUSE 16.0 qtdeclarative -
tst_QQuickColorDialogImpl::moveColorPickerHandle()
'qAbs(colorPicker->color().green() - QColorConstants::Cyan.green()) < 3'
returned FALSE
* [QTBUG-142436](https://qt-project.atlassian.net/browse/QTBUG-142436) QmlPreview's window handling is unreliable
* [QTBUG-146652](https://qt-project.atlassian.net/browse/QTBUG-146652) UB in QArrayDataPointer::operator-> (was:
tst_QArrayData::arrayOps fail with RHEL 10's compiler)
* [QTBUG-144365](https://qt-project.atlassian.net/browse/QTBUG-144365) textEditingContextMenuUndoRedo:SearchField fails on
ubuntu-22.04-x11-tests
* [QTBUG-146688](https://qt-project.atlassian.net/browse/QTBUG-146688) qmllint: bogus singleton warnings on examples
* [QTBUG-147177](https://qt-project.atlassian.net/browse/QTBUG-147177) QQuickShapeGenericRenderer::endSync: race accessing rhi
backend
* [QTBUG-142738](https://qt-project.atlassian.net/browse/QTBUG-142738) Crash accessing deleted item in
QQuickItemViewPrivate::updateUnrequestedPositions()
* [QTBUG-133256](https://qt-project.atlassian.net/browse/QTBUG-133256) Crash on dynamically removing items from a custom
QtQuick.Controls.Container with transitions
* [QTBUG-46798](https://qt-project.atlassian.net/browse/QTBUG-46798) Destroying an item crashes ListView
* [QTBUG-136806](https://qt-project.atlassian.net/browse/QTBUG-136806) QtQml restores QmlIR from CompilationUnits when loading
AOT-compiled artefacts
* [QTBUG-147652](https://qt-project.atlassian.net/browse/QTBUG-147652) Do not unconditionally capitalize first word in brief
texts
* [QTBUG-148164](https://qt-project.atlassian.net/browse/QTBUG-148164) Long property list<string> x: ... makes compilation take
forever
* [QTBUG-130116](https://qt-project.atlassian.net/browse/QTBUG-130116) Broken accessibility tree in (at least) certain lists
* [QTBUG-148215](https://qt-project.atlassian.net/browse/QTBUG-148215) Heap-use-after-free in QV4::Function constructor via
dangling QStringView from temporary QString
* [QTBUG-144177](https://qt-project.atlassian.net/browse/QTBUG-144177) RHEL 10: qtdeclarative auto test failures on Wayland

### qtactiveqt
* [QTBUG-146190](https://qt-project.atlassian.net/browse/QTBUG-146190) QWindowsIntegration constructor creates QPixmap before
platformIntegration() is set — regression Qt 6.6 → 6.8, ACCESS_VIOLATION
in qt_pixmap_thread_test() when hosting multiple Qt ActiveX controls
* [QTBUG-148520](https://qt-project.atlassian.net/browse/QTBUG-148520) [Reg 6.8.8 -> 6.11.1] Mismatch between
qualified/unqualified enum types makes COM method argument fail

### qtmultimedia
* [QTBUG-127444](https://qt-project.atlassian.net/browse/QTBUG-127444) QMediaRecorder does not start recording on darwin
backend
* [QTBUG-145034](https://qt-project.atlassian.net/browse/QTBUG-145034) [REG] Application CMake configuration fails for static
FFmpeg
* [QTBUG-131285](https://qt-project.atlassian.net/browse/QTBUG-131285) [Boot2Qt] Cannot run QML video example app on Boot2Qt
device
* [QTBUG-144316](https://qt-project.atlassian.net/browse/QTBUG-144316) [REG: 6.8.3->6.8.6] Static builds of Qt Multimedia fail
to link ffmpeg libraries in qmake projects
* [QTBUG-146764](https://qt-project.atlassian.net/browse/QTBUG-146764) SpatialSound [Quick3D] position changing is ignored in
Qt 6.11.1 (Regression from 6.11.0)
* [QTBUG-146907](https://qt-project.atlassian.net/browse/QTBUG-146907) Multimedia fails to build on selected Boot to Qt targets
* [QTBUG-143727](https://qt-project.atlassian.net/browse/QTBUG-143727) Videooutput does not work on Firefox, and does not
display and throws an exception when playing for the first time on Edge,
and then plays normally.
* [QTBUG-147138](https://qt-project.atlassian.net/browse/QTBUG-147138) [Windows] Sporadic crashes on enumerating codecs (in
QWindowsFormatInfo ctor)
* [QTBUG-131726](https://qt-project.atlassian.net/browse/QTBUG-131726) [Boot2Qt] Cannot record audio file in WMA which is
available on the device
* [QTBUG-147011](https://qt-project.atlassian.net/browse/QTBUG-147011) Crash on application exit in PipeWire audio backend —
QRtAudioEngine deleted synchronously after the event loop has stopped
(regression in 6.11.1)
* [QTBUG-147200](https://qt-project.atlassian.net/browse/QTBUG-147200) [REG Qt 6.11.0->6.11.1] Android: Deadlock on app
shutdown when QAndroidAudioDevices is destroyed
* [QTBUG-147839](https://qt-project.atlassian.net/browse/QTBUG-147839) Qt media player stuck in Buffering on memory-based media
* [QTBUG-147870](https://qt-project.atlassian.net/browse/QTBUG-147870) [REG 6.10.3-6.11.1] AVFVideoBuffer::textureHandle()
emits spurious "Metal texture cache was released?" warning when
QVideoSink has no RHI
* [QTBUG-148196](https://qt-project.atlassian.net/browse/QTBUG-148196) [Android] Assertion hit when switching camera devices
while zoomed in
* [QTBUG-148265](https://qt-project.atlassian.net/browse/QTBUG-148265) MSVC compilation error in PropertyStoreHelper::getGUID()
for Windows x86
* [QTBUG-147146](https://qt-project.atlassian.net/browse/QTBUG-147146) Regression: Can's suspend QAudioSink just after calling
start() with a callback
* [QTBUG-146024](https://qt-project.atlassian.net/browse/QTBUG-146024) QAmbientSound not rendered with OutputMode::Surround
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.
* [QTBUG-139848](https://qt-project.atlassian.net/browse/QTBUG-139848) [ffmpeg] MediaPlayer stably crashes during video
playback on graphics device lost
* [QTBUG-143055](https://qt-project.atlassian.net/browse/QTBUG-143055) [REG->6.8.6] /Android: declarative-camera example app :
captureToFile() fails to complete
* [QTBUG-147351](https://qt-project.atlassian.net/browse/QTBUG-147351) tst_QCameraBackend::testVirtualCameraRemoval flaky on CI
* [QTBUG-147882](https://qt-project.atlassian.net/browse/QTBUG-147882) FFmpeg-8: encoding wav into mpeg4/mov container broken
on windows

### qttools
* [QTBUG-146227](https://qt-project.atlassian.net/browse/QTBUG-146227) QDoc: Confusing output for \since command in a \qmlenum
topic
* [QTBUG-147232](https://qt-project.atlassian.net/browse/QTBUG-147232) QDoc manual lists obsolete .qhp subproject selectors
* [QTBUG-147360](https://qt-project.atlassian.net/browse/QTBUG-147360) lupdate: Treat .qrc file as UTF-8
* [QTBUG-147769](https://qt-project.atlassian.net/browse/QTBUG-147769) The Input Text is not Visible
* [QTBUG-145564](https://qt-project.atlassian.net/browse/QTBUG-145564) lrelease does not work on *.pro files in Qt 6.11 anymore
* [QTBUG-146665](https://qt-project.atlassian.net/browse/QTBUG-146665) Reg: Qt Widgets Designer: cannot get context menu on
disabled widget
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.
* [QTCREATORBUG-34100](https://qt-project.atlassian.net/browse/QTCREATORBUG-34100) Qt Widgets Designer Form Class Wizard templates
are aweful

### qtdoc
* [QTBUG-137815](https://qt-project.atlassian.net/browse/QTBUG-137815) Update "Networking", "Connectivity, "IPC" overviews -
CRA and 2025 changes
* [QTBUG-146802](https://qt-project.atlassian.net/browse/QTBUG-146802) QT_FONT_DPI is misleadingly labelled "legacy"
* [QTBUG-144148](https://qt-project.atlassian.net/browse/QTBUG-144148) Installer requirements aren't clearly documented
* [QTBUG-143161](https://qt-project.atlassian.net/browse/QTBUG-143161) Keyboard takes full screen on android and there is no
way to hide the extra features
* [QTBUG-143916](https://qt-project.atlassian.net/browse/QTBUG-143916) Fix QDoc warnings for Qt 6.11
* [QTBUG-138950](https://qt-project.atlassian.net/browse/QTBUG-138950) Improve format and layouting in 'High DPI' page
* [QTBUG-141341](https://qt-project.atlassian.net/browse/QTBUG-141341) WASM: UI does not respond

### qtqa
* [QTBUG-143566](https://qt-project.atlassian.net/browse/QTBUG-143566) RHEL-9.6: tst_Bic::sizesAndVTables(qt:6.10) Test failed
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtlocation
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtpositioning
* [QTBUG-144952](https://qt-project.atlassian.net/browse/QTBUG-144952) Fix UB in Q{GeoPath,Polygon}Private
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtsensors
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtconnectivity
* [QTBUG-145898](https://qt-project.atlassian.net/browse/QTBUG-145898) Windows/WinRT BLE: null deref in
onAdvertisementDataReceived completion chain
* [QTBUG-146756](https://qt-project.atlassian.net/browse/QTBUG-146756) Crash on Windows upon trying to connect to BLE after
scan
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtwayland
* [QTBUG-147321](https://qt-project.atlassian.net/browse/QTBUG-147321) Closing windows in qtshell example is broken
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qt3d
* [QTBUG-129888](https://qt-project.atlassian.net/browse/QTBUG-129888) Qt3D Warning: Created graphical object was not placed in
the graphics scene
* [QTBUG-135092](https://qt-project.atlassian.net/browse/QTBUG-135092) [qt3d] Cannot configure audio-visualizer-qml manual test
* [QTBUG-148237](https://qt-project.atlassian.net/browse/QTBUG-148237) Warning about unreleased resources on shutdown when
using the RHI renderer
* [QTBUG-148251](https://qt-project.atlassian.net/browse/QTBUG-148251) Qt3D example app leaks memory, crashes Mac when
QT_SCALE_FACTOR is set non-default
* [QTBUG-142683](https://qt-project.atlassian.net/browse/QTBUG-142683) Runaway memory use with Qt3D on macOS using Retina
displays
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtimageformats
* [QTBUG-107223](https://qt-project.atlassian.net/browse/QTBUG-107223) Massive memory consumption when loading TIFF image

### qtwebsockets
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtwebchannel
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtwebengine
* [QTBUG-143735](https://qt-project.atlassian.net/browse/QTBUG-143735) [qtwebengine] Misleading SBOM dependency warning
* [QTBUG-145344](https://qt-project.atlassian.net/browse/QTBUG-145344) Browser based on QtWebEngine would missing web page or
get flickering while enter web site with video content
* [QTBUG-146963](https://qt-project.atlassian.net/browse/QTBUG-146963) The current active SBOM project name was not found
* [QTBUG-147263](https://qt-project.atlassian.net/browse/QTBUG-147263) [Reg 6.11.0->6.11.1] Strange colored artifacts appear on
the right and bottom of the WebView.
* [QTBUG-146564](https://qt-project.atlassian.net/browse/QTBUG-146564) [qtwebengine] Crash during QWebEnginePage destruction
with outstanding QWebEngineWebAuthUxRequest
* [QTBUG-142687](https://qt-project.atlassian.net/browse/QTBUG-142687) [REG 6.10.1-6.10.2] Webpage compositing is broken on
nvidia GPU
* [QTBUG-145902](https://qt-project.atlassian.net/browse/QTBUG-145902) [qtwebengine] Crash during Skia/EGL initialization
* [QTBUG-144178](https://qt-project.atlassian.net/browse/QTBUG-144178) RHEL 10: qtwebengine auto test failures on Wayland
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.
* [QTBUG-146774](https://qt-project.atlassian.net/browse/QTBUG-146774) QQuickWebEngineScriptCollection is not exposed properly
to QML and makes qmllint fail

### qtwebview
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtcharts
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtdatavis3d
* [QTBUG-147570](https://qt-project.atlassian.net/browse/QTBUG-147570) Windows 11 x64: MinGW GCC 15 werror in qtdatavis3d:
qscatterdataitem.cpp
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtvirtualkeyboard
* [QTBUG-146018](https://qt-project.atlassian.net/browse/QTBUG-146018) Qt Virtual Keyboard default style has incorrect arrow-
key navigation from F when arrowKeyNavigationEnabled is enabled
* [QTBUG-148606](https://qt-project.atlassian.net/browse/QTBUG-148606) DesktopInputPanel does not disconnect from the
previously focused window
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.
* [QTBUG-146575](https://qt-project.atlassian.net/browse/QTBUG-146575) Non-namespaced include guards abound in Qt sources
* [QTBUG-141461](https://qt-project.atlassian.net/browse/QTBUG-141461) UnsatisfiedLinkError exception for missing Android ABI
in QtLoader

### qtscxml
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtspeech
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtremoteobjects
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtlottie
* [QTBUG-148136](https://qt-project.atlassian.net/browse/QTBUG-148136) Qt Lottie Animation: Examples are not listed in Qt
Creator Help contents
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtquicktimeline
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtquick3d
* [QTBUG-146019](https://qt-project.atlassian.net/browse/QTBUG-146019) Opacity of materials not imported from OBJ/MTL
* [QTBUG-145753](https://qt-project.atlassian.net/browse/QTBUG-145753)  Continuously changing eulerRotation through gestures in
a multi-threaded build will cause Tried to spawn a new thread, but the
thread pool is exhausted.
* [QTBUG-144947](https://qt-project.atlassian.net/browse/QTBUG-144947) New example quick3d/ssgilightmap not compiling on Wasm
* [QTBUG-147169](https://qt-project.atlassian.net/browse/QTBUG-147169) Visual artifacts when rendering transparent objects with
linked-list oit
* [QTBUG-147165](https://qt-project.atlassian.net/browse/QTBUG-147165) Crash when maximizing a window when using linked-list
oit
* [QTBUG-140392](https://qt-project.atlassian.net/browse/QTBUG-140392) Material.OpaquePrePassDepthDraw Option Causing Graphical
Artifacts with Instancing and CustomMaterial
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.
* [QTBUG-146168](https://qt-project.atlassian.net/browse/QTBUG-146168) crash in setRhiMaterialProperties with material binding
on line geometry
* [QTBUG-146205](https://qt-project.atlassian.net/browse/QTBUG-146205) Sharing a scene on multiple View3Ds (some not visible)
misuses dirty flags
* [QTBUG-145409](https://qt-project.atlassian.net/browse/QTBUG-145409) Crash when reparenting QQuick3DObject using
setParentItem() + QObject parent manipulation during scene graph
synchronization
* [QTBUG-147818](https://qt-project.atlassian.net/browse/QTBUG-147818) QSKIP tst_SourceItem::sourceItem on Wayland as it is
crashing
* [QTBUG-146627](https://qt-project.atlassian.net/browse/QTBUG-146627) Transparent object renders with corrupted fragments
using OpenGL RHI on NVIDIA RTX 3060

### qt5compat
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtmqtt
* [QTBUG-148625](https://qt-project.atlassian.net/browse/QTBUG-148625) error: macro 'Q_ENUMS' has been marked as deprecated:
Use Q_ENUM instead. [-Werror,-Wdeprecated-pragma]
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtopcua
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qthttpserver
* [QTBUG-135426](https://qt-project.atlassian.net/browse/QTBUG-135426) [Reg 6.7.3->6.8.2] QHttpPart fails to set Content-
Disposition header when using
setHeader(QNetworkRequest::ContentDispositionHeader)
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtquick3dphysics
* [QTBUG-145918](https://qt-project.atlassian.net/browse/QTBUG-145918) -Wenum-enum-conversion in PhysX causes FTBFS in Clang 21
C++26 builds
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtgrpc
* [QTBUG-146681](https://qt-project.atlassian.net/browse/QTBUG-146681) Qt6ProtobufWellKnownTypes fails to find .proto files
when protobuf_DIR points to standard cmake config location
* [QTBUG-145124](https://qt-project.atlassian.net/browse/QTBUG-145124) QML and protobuf: Issue with repeated nested message
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtquickeffectmaker
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtgraphs
* [QTBUG-146713](https://qt-project.atlassian.net/browse/QTBUG-146713) There can be no AxisProperties at all when AxisRenderer
tries to get one, causing crash
* [QTBUG-146839](https://qt-project.atlassian.net/browse/QTBUG-146839) Crash after series removed with axis that is referenced
by another series
* [QTBUG-147262](https://qt-project.atlassian.net/browse/QTBUG-147262) DateTimeAxis causes application crash when min and max
are identical
* [QTBUG-147540](https://qt-project.atlassian.net/browse/QTBUG-147540) QGraphsView::removeSeries is not thread-safe: crash
after removal
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.
* [QTBUG-146581](https://qt-project.atlassian.net/browse/QTBUG-146581) Try to reduce warnings generated by aerospacehub example
* [QTBUG-142559](https://qt-project.atlassian.net/browse/QTBUG-142559) Memory use goes up steadily when re-creating GraphsView

### qtopenapi
* [QTBUG-147745](https://qt-project.atlassian.net/browse/QTBUG-147745) code generation error with openapi: 3.1.0
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtcanvaspainter
* [QTBUG-146192](https://qt-project.atlassian.net/browse/QTBUG-146192) Path group issue when two paths share the same group and
the QCanvasPath addresses happen to be the same
* [QTBUG-144831](https://qt-project.atlassian.net/browse/QTBUG-144831) Path caching not working as expected with certain
settings
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtinterfaceframework (Commercial only)
* [QTBUG-146569](https://qt-project.atlassian.net/browse/QTBUG-146569) Reconfiguring certain parent qt repos fails with
"add_library cannot create ALIAS target"

### qtinsighttracker (Commercial only)
* [QTBUG-146965](https://qt-project.atlassian.net/browse/QTBUG-146965) tst_qinsighteventfilter (Failed)
* [QTBUG-146569](https://qt-project.atlassian.net/browse/QTBUG-146569) Reconfiguring certain parent qt repos fails with
"add_library cannot create ALIAS target"

Known Issues
------------
* Check that your system meets Qt's requirements:
  https://doc.qt.io/qt-6.11/supported-platforms.html
* RTA reported issues from Qt 6.11
  https://qt-project.atlassian.net/issues?filter=21382
* See Qt 6.11 known issues from:
  https://wiki.qt.io/Qt_6.11_Known_Issues
* Qt 6.11.2 Open issues in Jira:
  https://qt-project.atlassian.net/issues/?filter=24341

Credits for the release goes to:
---------------------------------

* Eirik Aavitsland
* Laszlo Agocs
* Dilek Akcay
* Konsta Alajärvi
* Even Oscar Andersen
* Albert Astals Cid
* Mate Barany
* Andreas Belke
* Vladimir Belyavsky
* Tim Blechmann
* Eskil Abrahamsen Blomfeldt
* David Boddie
* Tatiana Borisova
* Joerg Bornemann
* Rym Bouabid
* Assam Boudjelthia
* Aurélien Brooke
* Kai Uwe Broulik
* Michael Brüning
* Olivier De Cannière
* Alexei Cazacov
* Christophe Chapuis
* Kaloyan Chehlarski
* Luqiao Chen
* Alexandru Croitor
* Mitch Curtis
* Giuseppe D'Angelo
* Daniele E. Domenichelli
* David Edmundson
* Oliver Eftevaag
* Christian Ehrlicher
* Hatem ElKharashy
* David Faure
* Nicolas Fella
* Josep M. Ferrer
* John Paul Adrian Glaubitz
* Robert Griebl
* Magnus Groß
* Kaj Grönholm
* Richard Moe Gustavsen
* Mikko Hallamaa
* Tero Heikkinen
* Jani Heikkinen
* Moss Heim
* Jeff Heller
* Ulf Hermann
* Øystein Heskestad
* Volker Hilsheimer
* Mats Honkamaa
* Xaver Hugl
* Hitoshi ITO
* Ayesha Ishaq
* Masoud Jami
* Morteza Jamshidi
* Allan Sandfeld Jensen
* Tim Jenssen
* Jonas Karlsson
* Igor Khanin
* Dennis Kim
* Friedemann Kleint
* Michal Klocek
* Seokha Ko
* Jarek Kobus
* Kai Koehne
* Sze Howe Koh
* Jarkko Koivikko
* Tomi Korpipaa
* Fabian Kosmale
* Mike Krus
* Kai Köhne
* Frédéric Lefebvre
* Paul Lemire
* Wladimir Leuschner
* David Loki
* Robert Löhning
* Stuart MacDonald
* Thiago Macieira
* Olaf Mandel
* Jan Moeller
* Safiyyah Moosa
* Ahmad Hasan Mubashshir
* Marc Mutz
* Antti Määttä
* Andy Nichols
* Mårten Nordheim
* Dennis Oberst
* Frank Osterfeld
* Matti Paaso
* Weisser, Pascal
* Jerome Pasion
* Mauro Persano
* Yauheni Pervenenka
* Evgen Pervenenka
* Vyacheslav Petrovets
* Samuli Piippo
* Lauri Pohjanheimo
* Joni Poikelin
* Rami Potinkara
* Lorn Potter
* Dheerendra Purohit
* MohammadHossein Qanbari
* Matthias Rauter
* Topi Reinio
* Shawn Rutledge
* Ahmad Samir
* Timon Sassor
* Lars Schmertmann
* Nick Shaforostov
* Sami Shalayel
* Raman Shamotsin
* Gilsu Shin
* Kristoffer Skau
* Nils Petter Skålerud
* Ivan Solovev
* Axel Spoerl
* Magdalena Stojek
* Christian Strømme
* Tarja Sundqvist
* Lars Sutterud
* Jan Arve Sæther
* Morten Sørvig
* Sadegh Taghavi
* Patrik Teivonen
* Benjamin Terrier
* Alexandros Theodotou
* Elias Toivola
* Jere Tuliniemi
* Paul Olav Tvete
* Tuomas Vaarala
* Sami Varanka
* Peter Varga
* Doris Verria
* Tor Arne Vestbø
* Ville Voutilainen
* Juha Vuolle
* Sune Vuorela
* Vadim Vysokoostrovskiy
* Miao Wang
* Michael Weghorn
* Bernd Weimer
* Edward Welbourne
* Paul Wicking
* Oliver Wolff
* Semih Yavuz
* Wang Yu
* Vlad Zahorodnii
* Li Zequan
* Alexey Zerkin
* Liu Zheng
* Eike Ziller
