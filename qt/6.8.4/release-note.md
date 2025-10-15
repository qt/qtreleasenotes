Release note
============
Qt 6.8.4 release is a patch release made on the top of Qt 6.8.3.
As a patch release, Qt 6.8.4 does not add any new functionality but provides
bug fixes and other improvements and maintains both forward and backward
compatibility (source and binary) with Qt 6.8.3.

For detailed information about Qt 6.8, refer to the online documentation
included in this distribution. The documentation is also available online:

https://doc.qt.io/qt-6/index.html

The Qt version 6.8 series is binary compatible with the 6.7.x series.
Applications compiled for 6.7 will continue to run with 6.8.

Some of the changes listed in this file include issue tracking numbers
corresponding to tasks in the Qt Bug Tracker:

https://bugreports.qt.io/

Each of these identifiers can be entered in the bug tracker to obtain
more information about a particular change.

To make it easier to port to Qt 6, we have created a porting guide to
summarize those changes and provide guidance to handle them. In the
guide, you can find links to articles about changes that may affect your
application and help you transition from Qt 5.15 to Qt 6:

https://doc.qt.io/qt-6/portingguide.html

Important Changes
-----------------

### Security fixes

* CVE-2025-6338 in qtbase
* CVE-2025-5992 in qtbase
* CVE-2025-5455 in qtbase
* CVE-2025-4211 in qtbase
* CVE-2025-3512 in qtbase
* CVE-2025-5683 in qtimageformats

### qtbase
* bfd151fe02f Update Harfbuzz to version 10.3.0
Upgraded Harfbuzz to version 10.3.0.

* f771932f5f2 Upgrade Harfbuzz to 10.4.0
Upgraded Harfbuzz to version 10.4.0.

* d4a90a3f301 CBOR/JSON: fix crash when comparing strings with different
length
Fixed bug that could result in a crash or failing to find a entry in
the map/object with non- ASCII keys.

* 50dfa0a0d5e Make module ready for source SBOM checking
Renaming the license files with prefix LICENSE. to have them ignored by
reuse tool.

* 587b48e67ab 3rdparty: update TinyCBOR to v0.6.1
The copy of TinyCBOR in Qt was updated to 0.6.1.

* a3571d55fdd Only default top levels to
Qt::WA_ContentsMarginsRespectsSafeArea
The Qt::WA_ContentsMarginsRespectsSafeArea attribute is no longer set
by default for non-top-level widgets. Top level widgets still default to
Qt::WA_ContentsMarginsRespectsSafeArea=true, so children are laid out in
the safe areas, but overriding the attribute for the top level now
allows placing widgets in the non-safe areas without also setting the
Qt::WA_ContentsMarginsRespectsSafeArea attribute to false for every
descendant widget that overlaps the non-safe area.

* f2a599c150c QNetworkAccessManager: don't resend non-idempotent
requests
Non-idempotent requests are no longer incorrectly re-sent if the
connection breaks down while reading the response.

* 72d537716fc QUuid: fix qHash() on 64-bit platforms
Improved the performance of the qHash() function on 64-bit platforms by
populating all bits of the output (was: only lower 32 bits).

* a88e522c443 QVariant/QMetaType: fix conversions to/from qfloat16
Implemented converting of qfloat16 to and from the other numeric types,
text conversions to and from QString and QByteArray, and conversions to
and from QJsonValue and QCborValue. This should make qfloat16 behave the
same as float and double.

* a7f1ad81e02 JSON/CBOR: fix conversions from QVariant containing longs
and qfloat16
Fixed conversions from QVariant when the variant contained long,
unsigned long, or qfloat16.

* 0bef58c1110 Account for rounding error when rounding height metrics
Fixed an issue where the line distance for hinted fonts would be off by
one for specific sizes of some fonts.

* bbeccc0c22e QFileSystemEngine/Win: Use GetTempPath2 when available
On Windows, generating temporary directories for processes with
elevated privileges may now return a different path with a stricter set
of permissions. Please consult Microsoft's documentation from when they
made the same change for the .NET framework:
https://support.microsoft.com/en-us/topic/gettemppath-changes-in-
windows-february-cumulative-update-
preview-4cc631fb-9d97-4118-ab6d-f643cd0a7259

* d29b3721988 QTextMarkdownImporter: Fix heap-buffer-overflow
Fixed a heap buffer overflow in QTextMarkdownImporter. The first marker
for Front Matter must begin at the first character of a Markdown
document, and both markers must be exactly ---\n or ---\r\n.

* d852646d300 QXmlStreamReader::addData: lock encoding for QLatin1 case
Fixed a bug when calling addData() with a Latin1-encoded string
containing a full XML document with an encoding attribute, could result
in incorrect parsing of this document.

* 14a84801416 QUrl: expand the square brackets encoding to decoded
setPath() calls
") are now transformed to their percent-encoded forms ("%5B" and "%5D")
when present as inputs to setPath(), setQuery(), and setFragment() if
the parsing mode is QUrl::DecodedMode (the default).

* 8261829c34c Upgrade Harfbuzz to 11.0.0
Upgraded Harfbuzz to version 11.0.0.

* e3a80c2dd34 QPointer: don't cause UB when checking for nullptr
For `QPointer<Derived> p`, `!p` and comparing `p` to nullptr no longer
perform invalid downcasts when the object held in `p` is in the process
of being destroyed and has already been demoted from Derived to one of
its base classes. Before, these expressions invoked data(), which casts
from QObject* to Derived*, a cast which is invalid.

* f58657efc45 QXmlStreamReader: fix addData() unnecessary conversion to
UTF-8
Fixed a bug when addData(QAnyStringView) was incorrectly recoding
UTF-16 and Latin1 data to UTF-8, thus potentially mangling it.

* 4b3fccb68e0 windeployqt: Deploy Qt dependencies of local non Qt
dependencies
windeployqt now takes local non Qt dependencies into consideration
during deployment.

* 05998caa383 QStringConverter: widen nameForEncoding()'s contract
The nameForEncoding() function now returns nullptr for an invalid
Encoding value. Before, such a call resulted in undefined behavior.

* ecff73ccaac Make F11 the fullscreen keyboard shortcut on Gnome (as on
KDE & Windows)
The fullscreen keyboard shortcut is now F11 on Gnome, not Ctrl-F11.

* 45e8c81c525 QAbstractSlider: fix missing "emission" of
SliderOrientationChange
Fixed the missing "emission" of protected
sliderChange(SliderOrientationChange).

* e56bf8d2953 qDecodeDataUrl(): fix precondition violation in call to
QByteArrayView::at()
Fixed a bug in the handling of data: URLs that could lead to a crash if
Qt was built with assertions enabled. This affects QNetworkManager and
links in QTextDocument.

* 9e0bd59d80d Upgrade Harfbuzz to 11.1.0
Upgraded Harfbuzz to version 11.1.0.

* 41016a26c3d SQLite: Update SQLite to v3.49.2
Updated SQLite to v3.49.2

* cb319e88e71 QSslCertificate: fromPath(): check the path arg isn't
empty
fromPath() no longer accepts an empty path, which would previously
result in searching the current directory.

* a1f16bcf55b Upgrade Harfbuzz to 11.2.1
Upgraded Harfbuzz to version 11.2.1.

* c5a10f00450 Update bundled libpng to version 1.6.48
libpng was updated to version 1.6.48

* 5b86b2c714b SQLite: Update SQLite to v3.50.0
Updated SQLite to v3.50.0

* 1acf3ac2e66 Fix long-form zone parts in date-time strings
The tttt format specifier now uses the full long name of the zone,
falling back to its IANA ID only if this cannot be determined. Both
forms are now recognized when reading a datetime from a string.

* 90498585d9e SQLite: Update SQLite to v3.50.1
Updated SQLite to v3.50.1

* f9cf76f2a77 iOS: Report inverted screen orientations via windowScene
orientation
QScreen::orientation() now reflects the inverse portrait and landscape
orientations, as long as system allows rotating the UI to those
orientations.

* 3125001ea6c QByteArray: make toDouble() reject space-only strings
Fixed an old regression that caused toDouble() and toFloat() to return
ok = true for a string containing only whitespaces.

* 97a206400eb QUrl: fix comparisons of URLs with password but no
explicit username
Fixed a number of bugs in QUrl where a URL modified using the setXxx()
functions would fail to compare equal to itself after going through
toString() and setUrl() round-trip.

* d7a233b334b Update bundled libjpeg-turbo to version 3.1.1
libjpeg-turbo was updated to version 3.1.1

* 29497f5222b Bump double-conversion version
Updated double-conversion to v3.3.1.

* 75cb94996df Update public suffix list
Updated the public suffix list to upstream version
2025-06-16_09-45-02_UTC.

* a5f102b765b Update bundled libpng to version 1.6.49
libpng was updated to version 1.6.49

* d07267a3ed0 SQLite: Update SQLite to v3.50.2
Updated SQLite to v3.50.2

* 9cc94554dbc Update CLDR to v47
Updated CLDR data, used by QLocale, to v47.

* 8ae7cb6f0b8 Upgrade Valgrind third-party component to v3.25.1
Updated Valgrind support to v3.25.1; this adds support for RISCV 64-bit
Linux.

* a3d31f3a79e Android: Set proper A11y-element java class names to
support TalkBack
Provide actual Android UI class names for TalkBack to improve a11y
announcements.

### qtsvg
* 16b59c7a Make module ready for source SBOM checking
Renamed certain license files outside of LICENSES with `LICENSE.`
prefix such that reuse will correctly ignore them.

* e0ebc50c CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtdeclarative
* 4610ae066e StackView: Use PushTransition for pushItem(s)
The default operation for pushItem(s) is now PushTransition as
documented. Previously, Immediate was used.

* e42afe7124 TableView: emit commit on editor loss of focus, unless
Qt::Key_Escape
The edit delegate will now emit the onCommit signal when it loses
focus, unless it was closed from Qt::Key_Escape.

* da1e039353 QQuickPopupItem: Set tabFence to be true by default
The popupItem always acts as a tab fence, preventing tab focus
navigation in and out of the popup, except when the popup is a Drawer,
in which case this behavior depends on the drawer's modality.

* 3d486bfce5 QQmlBind: Only restore previous state if current state is
still active
The Binding element now only restores previous bindings or values if
its own binding is still active on destruction or changes to its "when"
property. If it has been overridden by another Binding element, it will
not disable that one anymore.

* e1cd2447eb CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtmultimedia
* 580c9c194 QMake: Add possibility to link and embed FFmpeg frameworks
on iOS
Added the CONFIG value add_ios_ffmpeg_libraries that can be used in iOS
apps that need FFmpeg frameworks for QtMultimedia.

* d5e62fbdc Update FFmpeg version in documentation
Updated FFmpeg to n7.1.1.

* 7708d0153 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qttools
* a66a3f11e Make module ready for source SBOM checking
Renaming the license files with prefix LICENSE. to have them ignored by
reuse tool.

* d2797e5fd CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtpositioning
* 8e1a2810 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

* 6c210e75 Make: Fix incorrect PURL version for clip2tri
Fixed incorrect PURL version for clip2tri in qt_attribution.json.

### qtsensors
* bc04956a CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtconnectivity
* 3289d2e5 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtwayland
* 2bd7d282 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qt3d
* 9ea3365ab Make module ready for source SBOM checking
Renaming the license files with prefix LICENSE. to have them ignored by
reuse tool.

* 50cfb16b5 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtimageformats
* 83d57079 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtwebengine
* aee2b8e8c [Backport] Make download API asynchronous
QWebEngineProfile::downloadRequested() is not limited to synchronous
usage anymore. QWebEngineDownloadRequest can be accepted or rejected
later without blocking the browsing session.

### qtvirtualkeyboard
* f55cd043 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtquick3d
* a6412273f Update meshoptimizer to v0.23
Updated meshoptimizer to v0.23

* 4a93971b7 Update TinyEXR to v1.0.12
Updated TinyEXR to v1.0.12

* eb5d6e6c3 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtshadertools
* 92f476c CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qt5compat
* 3f1f0a8 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtopcua
* e1b263ea Fix handling of ByteString node ids with null bytes
Fix a bug that prevented ByteString node ids    with null bytes from
being used.

* fdff4e1b Fix SimpleAttributeOperand conversion in the open62541 plugin
Fix an interoperability issue with the    Siemens OPC UA server where
the conditionId could not be selected    in an event filter.

* 116d73f7 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtgrpc
* ce20e4f5 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtapplicationmanager (Commercial only)
* 1b0c06e2 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtinterfaceframework (Commercial only)
* b492c0c3 Update license check
Rename license file with LICENSE. prefix. This way the file is ignored
by the reuse tool.

* 6e8bf5af CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

* 2bffd100 Update the bundled qface to the latest version (2.0.13)
The copy of qface in Qt was updated to 2.0.13


Fixes
-----

### qtbase
* [QTBUG-133412](https://bugreports.qt.io/browse/QTBUG-133412) QFileDialog drive icons incorrect scaling on screen with
non-integer device pixel ratio
* [QTBUG-134316](https://bugreports.qt.io/browse/QTBUG-134316) [Reg] QFileOpenEvent isn't emitted for custom URI
* [QTBUG-133406](https://bugreports.qt.io/browse/QTBUG-133406) Unrechable code in MetaTypeQFutureHelper
* [QTBUG-118997](https://bugreports.qt.io/browse/QTBUG-118997) missing D-Bus Viewer manual
* [QTBUG-133744](https://bugreports.qt.io/browse/QTBUG-133744) QString assertion failure using UTF-16 character in
QJsonObject key
* [QTBUG-134235](https://bugreports.qt.io/browse/QTBUG-134235) Build failure of qtbase/src/widgets/styles/qdrawutil.cpp
with disabled features
* [QTBUG-134533](https://bugreports.qt.io/browse/QTBUG-134533) Fusion style: SH_EtchDisabledText in disable QMenu looks
blurry
* [QTBUG-134538](https://bugreports.qt.io/browse/QTBUG-134538) QRandomGenerator, QSimd: RDSEED should be checked for
validity
* [QTBUG-130063](https://bugreports.qt.io/browse/QTBUG-130063) QKeySequence(<QString>) doesn't parse correctly when we
have a space
* [QTBUG-132705](https://bugreports.qt.io/browse/QTBUG-132705) Qt CMake content uses compiler config from qtbase,
instead the current modules
* [QTBUG-134080](https://bugreports.qt.io/browse/QTBUG-134080) "QObject::~QObject: Timers cannot be stopped from
another thread" message in Qt 6.8.2 plugins
* [QTBUG-133861](https://bugreports.qt.io/browse/QTBUG-133861) [macOS] QML Preview: Closing the preview window produces
QObject::killTimer warning
* [QTBUG-132697](https://bugreports.qt.io/browse/QTBUG-132697) FAIL!  :
tst_QQmlDebugJS::setBreakpointInScriptThatQuits(custom)
'm_process->waitForFinished()' returned FALSE.
* [QTBUG-102984](https://bugreports.qt.io/browse/QTBUG-102984) QML debugger and profiler tests hangs on macOS/x86_64 in
CI
* [QTBUG-132381](https://bugreports.qt.io/browse/QTBUG-132381) [REG 6.8 -> 6.9] Crash when QGuiApplication is static
* [QTBUG-134075](https://bugreports.qt.io/browse/QTBUG-134075) Windows Server 2016 is no longer working
* [QTBUG-133710](https://bugreports.qt.io/browse/QTBUG-133710) Fix padding in tabs for pre elements
* [QTBUG-134699](https://bugreports.qt.io/browse/QTBUG-134699) Performance regression in QDirIterator when going from
6.5.3 to 6.8.2 [REG 6.5.3->6.8.2]
* [QTBUG-134497](https://bugreports.qt.io/browse/QTBUG-134497) Mouse hover stylesheet does not renders correct color in
windows11
* [QTBUG-133702](https://bugreports.qt.io/browse/QTBUG-133702) [Android] QDesktopServices::openUrl(): FileProvider
unable to get URI for sharing file
* [QTBUG-40283](https://bugreports.qt.io/browse/QTBUG-40283) QSettings: Documentation and implementation differ
* [QTBUG-131256](https://bugreports.qt.io/browse/QTBUG-131256) QTextEdit will block and crash by
QEventLoop::WaitForMoreEvents when  pressing or dragging selected text
* [QTBUG-133269](https://bugreports.qt.io/browse/QTBUG-133269) QTextStream: suspicious negation when streaming numbers
* [QTBUG-132929](https://bugreports.qt.io/browse/QTBUG-132929) QStyleHints::setColorScheme() doesn't affect the
application's theme on Ubuntu
* [QTBUG-127528](https://bugreports.qt.io/browse/QTBUG-127528) QApplication::fontMetrics() deprecation message is too
vague
* [QTBUG-132121](https://bugreports.qt.io/browse/QTBUG-132121) Bad signal restoration cause infinite loop in
FatalSignalHandler destructor
* [QTBUG-15125](https://bugreports.qt.io/browse/QTBUG-15125) QDomAttr QDomElement::setAttributeNode ( const QDomAttr &
newAttr ) does NOT replaces attribute with the same name as newAttr.
* [QTBUG-28721](https://bugreports.qt.io/browse/QTBUG-28721) QXmlStreamWriter writes newline at beginning of stream if
auto formatting is enabled.
* [QTBUG-134694](https://bugreports.qt.io/browse/QTBUG-134694) QNetworkAccessManager re-sends destructive requests
(POST, possibly others) without user intervention
* [QTBUG-134768](https://bugreports.qt.io/browse/QTBUG-134768) QLocale::toStrings uses E instead of e
* [QTBUG-134785](https://bugreports.qt.io/browse/QTBUG-134785) Provide QLocale::toString() floating-point formats for
locale-appropriate case of exponent
* [QTBUG-134756](https://bugreports.qt.io/browse/QTBUG-134756) QJsonValue::fromVariant converts integers incorrectly
* [QTBUG-134313](https://bugreports.qt.io/browse/QTBUG-134313) can't drag application/x-color from one Qt application
to another (is it hex or raw?)
* [QTBUG-134610](https://bugreports.qt.io/browse/QTBUG-134610) Disconnect all -> crash in QAccessibilityCache
* [QTBUG-132310](https://bugreports.qt.io/browse/QTBUG-132310) Crash in QCocoaAccessible::shouldBeIgnored
* [QTBUG-132459](https://bugreports.qt.io/browse/QTBUG-132459) Windows11 style: QProgressBar needs some work
* [QTBUG-134702](https://bugreports.qt.io/browse/QTBUG-134702) QT_QPA_PLATFORMTHEME=generic doesn't work on KDE and GTK
environments
* [QTBUG-134703](https://bugreports.qt.io/browse/QTBUG-134703) Setting XDG_CURRENT_DESKTOP to xdgdesktopportal, flatpak
or snap causes an instant crash
* [QTBUG-134602](https://bugreports.qt.io/browse/QTBUG-134602) Rendering of QQuickText slightly elevated.
* [QTBUG-130576](https://bugreports.qt.io/browse/QTBUG-130576) Touches Are Handled Incorrectly with QDialog on Qt 6.8.x
Android
* [QTBUG-127925](https://bugreports.qt.io/browse/QTBUG-127925) Touch events end up in wrong place with Widgets gallery
on Android
* [QTBUG-135109](https://bugreports.qt.io/browse/QTBUG-135109) some POSIX-style TZ strings are not supported by Qt on
some Linux-based platform
* [QTBUG-135159](https://bugreports.qt.io/browse/QTBUG-135159) QIcon::fromTheme selects 32px icon instead of 16@2x with
devicePixelRatio 2
* [QTBUG-134788](https://bugreports.qt.io/browse/QTBUG-134788) Copyright footer shows previous year
* [QTBUG-135238](https://bugreports.qt.io/browse/QTBUG-135238) QDateTime::toTimeZone doc's code snippet calls
deprecated ::toTimeSpec
* [QTBUG-134784](https://bugreports.qt.io/browse/QTBUG-134784) macos: Crash in Voice Over/Accessiblity when resetting a
table model
* [QTBUG-127517](https://bugreports.qt.io/browse/QTBUG-127517) Reports of misaligned loads with asan on AArch64 / xcb
* [QTBUG-76976](https://bugreports.qt.io/browse/QTBUG-76976) QSortFilterProxyModel::mapFromSource returns a valid
QModelIndex for the filtered out item
* [QTBUG-134626](https://bugreports.qt.io/browse/QTBUG-134626) [6.8.1 -> 6.8.2] Thicker text underline with certain
fonts (X11)
* [QTBUG-135163](https://bugreports.qt.io/browse/QTBUG-135163) QThread::isRunning returns false while the thread is
still running
* [QTBUG-135033](https://bugreports.qt.io/browse/QTBUG-135033) QXmlStreamReader::addData() can parse Latin1 data
incorrectly
* [QTBUG-135225](https://bugreports.qt.io/browse/QTBUG-135225) qtbase build fails without process(environment) feature
* [QTBUG-135135](https://bugreports.qt.io/browse/QTBUG-135135) QMySqlDriver QDateTime is not consistant between
read/write
* [QTBUG-135338](https://bugreports.qt.io/browse/QTBUG-135338) Sorting indicator size not honored in itemview header
with windows11 style
* [QTBUG-135287](https://bugreports.qt.io/browse/QTBUG-135287) QDirIterator::next no longer returns "" upon iterator
exhaustion
* [QTBUG-130142](https://bugreports.qt.io/browse/QTBUG-130142) 6.8 Regresssion:  QDirIterator::next segfaults
* [QTBUG-135264](https://bugreports.qt.io/browse/QTBUG-135264) Error in qml qmake project with qt 6.8.3
* [QTBUG-135382](https://bugreports.qt.io/browse/QTBUG-135382) Invalid year zero date asserts in
QDateTimeParser::parse()
* [QTBUG-135471](https://bugreports.qt.io/browse/QTBUG-135471) tst_QXmlStream does not test non-wellformed documents
properly
* [QTBUG-134634](https://bugreports.qt.io/browse/QTBUG-134634) tst_QUuid::uint128 fails on big-endian
* [QTBUG-135433](https://bugreports.qt.io/browse/QTBUG-135433) QUrl::setPath and QUrl::fromUserInput encodes local
paths differently from QUrl::fromLocalFile
* [QTBUG-134073](https://bugreports.qt.io/browse/QTBUG-134073) QMimeData does not escape square brackets in text/uri-
list
* [QTBUG-135620](https://bugreports.qt.io/browse/QTBUG-135620) Qt6WebEngineCoreDeploySupport fails when generating RPM
* [QTBUG-109553](https://bugreports.qt.io/browse/QTBUG-109553) CMake deployment API creates too deep directory
hierarchy when DESTDIR is set
* [QTBUG-135340](https://bugreports.qt.io/browse/QTBUG-135340) Regression: Stylesheet breaks QGraphicsProxyWidget
* [QTBUG-128916](https://bugreports.qt.io/browse/QTBUG-128916) QComboBox drop down is not visible on Windows11 in some
situation
* [QTBUG-128329](https://bugreports.qt.io/browse/QTBUG-128329) qt combobox 放入到QGraphicsProxyWidget下拉框不显示
* [QTBUG-135628](https://bugreports.qt.io/browse/QTBUG-135628) QCheckbox without text is right cropped
* [QTBUG-133117](https://bugreports.qt.io/browse/QTBUG-133117) Windows11Style: Check boxes and radio buttons slightly
cropped at 150%
* [QTBUG-134415](https://bugreports.qt.io/browse/QTBUG-134415) Qt FTBFS with GCC < 15 + TSAN + PCH + developer-build
* [QTBUG-99957](https://bugreports.qt.io/browse/QTBUG-99957) No rule to make target 'qtbase/src/platformsupport/input/
CMakeFiles/InputSupportPrivate.dir/cmake_pch.hxx.gch
* [QTBUG-134807](https://bugreports.qt.io/browse/QTBUG-134807) macos: Voice Over/Accessiblity for tabs is lacking
* [QTBUG-135609](https://bugreports.qt.io/browse/QTBUG-135609) Build failure when building iOS on macOS
* [QTBUG-133963](https://bugreports.qt.io/browse/QTBUG-133963) [REG Qt 6.5 -> 6.7] Shortcuts on macOs using
Meta/Command require Shift as well
* [QTBUG-135578](https://bugreports.qt.io/browse/QTBUG-135578) Possible QTimer ABI break between Qt 6.7 and Qt 6.9
* [QTBUG-134139](https://bugreports.qt.io/browse/QTBUG-134139) Windows: Qt::Popup window has wrong initial size on
system with displays with different DPI scales
* [QTBUG-135619](https://bugreports.qt.io/browse/QTBUG-135619) QVariant::canConvert behaves inconsistently with the
documentation
* [QTBUG-135285](https://bugreports.qt.io/browse/QTBUG-135285) QVariant::toInt() asserts if the contained real number
exceeds integer limits
* [QTBUG-135152](https://bugreports.qt.io/browse/QTBUG-135152) qtbase build fails if configured with -no-feature-
desktopservices
* [QTBUG-135076](https://bugreports.qt.io/browse/QTBUG-135076) [QNX] Stale QNX Screen events under load
* [QTBUG-135294](https://bugreports.qt.io/browse/QTBUG-135294) Duplicate data tags in tst_qgraphicslinearlayout
* [QTBUG-135112](https://bugreports.qt.io/browse/QTBUG-135112) QRhiSwapChain (QD3D11SwapChain) createOrResize() crashes
when importing D3D11 Device and Context
* [QTBUG-135806](https://bugreports.qt.io/browse/QTBUG-135806) qtbase autotests to compile without draganddrop
* [QTBUG-135442](https://bugreports.qt.io/browse/QTBUG-135442) QDockWidget/QMainWindow leak widgetItems from
QDockAreaLayoutItem on dragging and QDockWidget::close()
* [QTBUG-135129](https://bugreports.qt.io/browse/QTBUG-135129) QXmlStreamReader::addData(QASV) overload unconditionally
converts UTF-16 and L1 to UTF-8
* [QTBUG-134881](https://bugreports.qt.io/browse/QTBUG-134881) android_content_uri test crashes during test process.
* [QTBUG-135648](https://bugreports.qt.io/browse/QTBUG-135648) [REG 6.7->6.8] macOS: FindWrapResolv.cmake fails
check_cxx_source_compiles with strict flags (-Werror -Wzero-as-null-
pointer-constant)
* [QTBUG-133923](https://bugreports.qt.io/browse/QTBUG-133923) Missing documentation for QFlags' equality operators
* [QTBUG-135079](https://bugreports.qt.io/browse/QTBUG-135079) windeployqt missing plugins
* [QTBUG-135640](https://bugreports.qt.io/browse/QTBUG-135640) Data race in QPointer
(QtSharedPointer::ExternalRefCountData::getAndRef)
* [QTBUG-135230](https://bugreports.qt.io/browse/QTBUG-135230) Configuring xmlstreamreader out of the build fails
* [QTBUG-135636](https://bugreports.qt.io/browse/QTBUG-135636) tst_QTimer::crossThreadSingleShotToFunctor() leaks
(almost) all timers
* [QTBUG-135933](https://bugreports.qt.io/browse/QTBUG-135933) QMenus with a layout and widgets are no longer shown
* [QTBUG-129108](https://bugreports.qt.io/browse/QTBUG-129108) Menus and action visibility
* [QTBUG-135854](https://bugreports.qt.io/browse/QTBUG-135854) Qt Keyboard Shortcut: Fullscreen incorrectly mapped in
GNOME
* [QTBUG-135597](https://bugreports.qt.io/browse/QTBUG-135597) QAbstractSlider is not using SliderOrientationChange
* [QTBUG-136019](https://bugreports.qt.io/browse/QTBUG-136019)  c1: fatal error C1083: Cannot open source file: 'C:\Use
rs\qt\work\qt\qt3d_build\src\plugins\renderers\opengl\debug\OpenGLRender
erPlugin_resource.rc': No such file or directory
* [QTBUG-135617](https://bugreports.qt.io/browse/QTBUG-135617) Compile Android without permissions -feature
* [QTBUG-135893](https://bugreports.qt.io/browse/QTBUG-135893) Allow configuring Windows without highdpiscaling feature
* [QTBUG-135890](https://bugreports.qt.io/browse/QTBUG-135890) Allow configuring Windows without clipboard feature
* [QTBUG-135950](https://bugreports.qt.io/browse/QTBUG-135950) Cocoa window: Updates are not received
* [QTBUG-136042](https://bugreports.qt.io/browse/QTBUG-136042) Qt MySQL driver does not add milliseconds for QDateTime
in formatValue()
* [QTBUG-95071](https://bugreports.qt.io/browse/QTBUG-95071) mysql client version detection broken with MariaDB 10.6
* [QTBUG-133841](https://bugreports.qt.io/browse/QTBUG-133841) 'Failed to initialize graphics backend for OpenGL'
causes the example apps to crash on launch
* [QTBUG-11967](https://bugreports.qt.io/browse/QTBUG-11967) QDateEdit/CalendarPopup(true) has incorrect sizing
* [QTBUG-125586](https://bugreports.qt.io/browse/QTBUG-125586) QVariantAnimation: currentValue should not change when
calling setStartValue() and setEndValue()
* [QTBUG-135693](https://bugreports.qt.io/browse/QTBUG-135693) Compile Android without accessibility -feature
* [QTBUG-135675](https://bugreports.qt.io/browse/QTBUG-135675) Compile Android without clipboard -feature
* [QTBUG-134695](https://bugreports.qt.io/browse/QTBUG-134695) [REG] QPdfWriter: embed font issue: generates very big
pdf file on windows : the workaround doesn't work anymore
* [QTBUG-135326](https://bugreports.qt.io/browse/QTBUG-135326) Linux: QLoggingCategory::setFilterRules() with enabled
CTF tracing causes a crash
* [QTBUG-135934](https://bugreports.qt.io/browse/QTBUG-135934) Mac-style QMenu icons never show Disabled mode
* [QTBUG-130474](https://bugreports.qt.io/browse/QTBUG-130474) QLineEdit/QCompleter popup shows in top-level window
* [QTBUG-136233](https://bugreports.qt.io/browse/QTBUG-136233) [Webassembly] Ghost input field disrupts surface
geometry
* [QTBUG-136348](https://bugreports.qt.io/browse/QTBUG-136348) Problem with macdeployqt not passing CN correctly
* [QTBUG-136609](https://bugreports.qt.io/browse/QTBUG-136609) Can't run appex with 6.8.3 or later
* [QTBUG-136210](https://bugreports.qt.io/browse/QTBUG-136210) Qt installer .pc files unusable due to spurious prefix
* [QTBUG-135800](https://bugreports.qt.io/browse/QTBUG-135800) [REG 6.8 → 6.9] XMLHttpRequest() errors from
qt.network.http2 and rest api data are not displaying to Multimedia
* [QTBUG-129568](https://bugreports.qt.io/browse/QTBUG-129568) tst_QWidget_window::mouseMoveWithPopup() failed on
Ubuntu 24.04 GNOME X11
* [QTBUG-129029](https://bugreports.qt.io/browse/QTBUG-129029) tst_QComboBox:popupPositionAfterStyleChange() failed on
Ubuntu 24.04 GNOME X11
* [QTBUG-134419](https://bugreports.qt.io/browse/QTBUG-134419) systemCaCertificate() openssl backend walks current
working directory if system ca directory contains a broken symlink
* [QTBUG-135945](https://bugreports.qt.io/browse/QTBUG-135945) QLatin1StringView documentation assumes knowledge of
string literals namespace
* [QTBUG-136530](https://bugreports.qt.io/browse/QTBUG-136530) QFuture::isValid() without result
* [QTBUG-125223](https://bugreports.qt.io/browse/QTBUG-125223)  Plugin's install_rpath error during deployment by
qt_generate_deploy_qml_app_script.
* [QTBUG-136083](https://bugreports.qt.io/browse/QTBUG-136083) qtypeinfo.h uses std::is_trivial_v which will be
deprecated in C++26
* [QTBUG-135978](https://bugreports.qt.io/browse/QTBUG-135978) Adding -ObjC linking flag breaks iOS build
* [QTBUG-136497](https://bugreports.qt.io/browse/QTBUG-136497) Android app fails to restart when permission is revoked
* [QTBUG-136077](https://bugreports.qt.io/browse/QTBUG-136077) [Regression 6.8.2->6.8.3] Android apps hang with black
screen or splash screen
* [QTBUG-135961](https://bugreports.qt.io/browse/QTBUG-135961) Blank screen when app is woken up from background
* [QTBUG-136362](https://bugreports.qt.io/browse/QTBUG-136362) [REG 6.8 -> 6.9] QTableView: Header sections' incorrect
painting
* [QTBUG-136477](https://bugreports.qt.io/browse/QTBUG-136477) Header scrolls to opposite direction
* [QTBUG-136812](https://bugreports.qt.io/browse/QTBUG-136812) Bug in http header handling on WASM
* [QTBUG-136799](https://bugreports.qt.io/browse/QTBUG-136799) wasm: unicode alt code processing error when NumLock is
activated
* [QTBUG-135977](https://bugreports.qt.io/browse/QTBUG-135977) [REG 6.8.2 -> 6.8.3] WASM: Loaded Roboto Flex font
rendered as italic by default
* [QTBUG-135315](https://bugreports.qt.io/browse/QTBUG-135315) Possible regression in handling of special style names
* [QTBUG-136678](https://bugreports.qt.io/browse/QTBUG-136678) Hardcoded paths used in
qt_generate_deploy_qml_app_script
* [QTBUG-135481](https://bugreports.qt.io/browse/QTBUG-135481) Android TV system keyboard doesn't process input
correctly
* [QTBUG-135722](https://bugreports.qt.io/browse/QTBUG-135722) Compile Android without desktopservices -feature
* [QTBUG-133746](https://bugreports.qt.io/browse/QTBUG-133746) QFileSystemModel with wrong path of top-directory of a
drive
* [QTBUG-111993](https://bugreports.qt.io/browse/QTBUG-111993) QNetworkAccessManager docs: minor typo referencing non-
existent method
* [QTBUG-135489](https://bugreports.qt.io/browse/QTBUG-135489) [REG 6.8.2->6.8.3] Handling of custom scheme URL is
broken
* [QTBUG-137130](https://bugreports.qt.io/browse/QTBUG-137130) Qt Creator crash on exit accessing destroyed event
dispatcher
* [QTBUG-135376](https://bugreports.qt.io/browse/QTBUG-135376) Fullscreen virtual keyboard key handling
* [QTBUG-128745](https://bugreports.qt.io/browse/QTBUG-128745) [QuickControls] Text inputs displayed as extracted view
in landscape orientation
* [QTBUG-130058](https://bugreports.qt.io/browse/QTBUG-130058) Android Virtual keyboard is broken in landscape mode
* [QTBUG-131655](https://bugreports.qt.io/browse/QTBUG-131655) Memory leak in QNSViewMenuHelper
* [QTBUG-137161](https://bugreports.qt.io/browse/QTBUG-137161) "Leaks" utility in the Instruments app report memory
leak.
* [QTBUG-137277](https://bugreports.qt.io/browse/QTBUG-137277) Stack overflow in QFontEngine (due to infinite
recursion)
* [QTBUG-137316](https://bugreports.qt.io/browse/QTBUG-137316) generateJavaQmlComponents will scan relevant import
directories twice
* [QTBUG-136333](https://bugreports.qt.io/browse/QTBUG-136333)  Crash occurs upon opening QFileDialog from QDialog
* [QTBUG-137297](https://bugreports.qt.io/browse/QTBUG-137297) qmake iOS target: fails to find (prebuilt) .prl
dependencies -> Xcode build fails
* [QTBUG-135634](https://bugreports.qt.io/browse/QTBUG-135634) macOS: Deleted menu is not removed from native menu bar
* [QTBUG-135652](https://bugreports.qt.io/browse/QTBUG-135652) Using QIcon from png and svg file in a toolbar with
>100% scaler ratio causes wrong icon size to be picked elsewhere
* [QTBUG-137108](https://bugreports.qt.io/browse/QTBUG-137108) CE_ComboBoxLabel painting not called anymore on
QProxyStyle, due to QStyleSheetStyle
* [QTBUG-131761](https://bugreports.qt.io/browse/QTBUG-131761) Incorrect display of :selected state of QCombobox on
"windows" style plugin
* [QTBUG-136229](https://bugreports.qt.io/browse/QTBUG-136229) Fullscreen virtual keyboard: issue with selection and
delete
* [QTBUG-136550](https://bugreports.qt.io/browse/QTBUG-136550) QMYSQL: QT application built with libmariadb3.4 won't
connect to MariaDB 10
* [QTBUG-137198](https://bugreports.qt.io/browse/QTBUG-137198) Configure fails with -DFEATURE_sanitize_thread=ON
-DFEATURE_sanitize_address=ON without a proper message
* [QTBUG-133687](https://bugreports.qt.io/browse/QTBUG-133687) Confusing instructions when atomicfptr config.test fails
* [QTBUG-130278](https://bugreports.qt.io/browse/QTBUG-130278) [Reg 6.7.2 -> 6.8.0][macOS] QLocale::LongFormat no
longer produces reversible conversion between QDateTime and QString
* [QTBUG-137168](https://bugreports.qt.io/browse/QTBUG-137168) QtMultimedia fails to install: Cannot find
'plugins/multimedia/libmockmultimediaplugin.a' to compute its checksum
* [QTBUG-136590](https://bugreports.qt.io/browse/QTBUG-136590) Regression in QTextTable: border-collapse cell border
rendering broken
* [QTBUG-133904](https://bugreports.qt.io/browse/QTBUG-133904) Corrupted qml rendering on some Android PowerVR devices
after the app is killed
* [QTBUG-134245](https://bugreports.qt.io/browse/QTBUG-134245) [Reg 6.8.0 -> 6.8.2] Strange 4-quadrant colouration of
Qt Quick items
* [QTBUG-134089](https://bugreports.qt.io/browse/QTBUG-134089) Power VR rendering failure on Qt 6.8.2
* [QTBUG-135411](https://bugreports.qt.io/browse/QTBUG-135411) Android visual Glitches on 6.8.2+
* [QTBUG-134496](https://bugreports.qt.io/browse/QTBUG-134496) Drawing errors on some Android devices
* [QTBUG-135810](https://bugreports.qt.io/browse/QTBUG-135810) [REG 6.8.1 -> 6.8.3] Crashes in QRhi::endFrame /
glDrawElements on Android
* [QTBUG-133407](https://bugreports.qt.io/browse/QTBUG-133407) Tools in qtbase fail to link to QtCore when Qt is
statically built
* [QTBUG-136074](https://bugreports.qt.io/browse/QTBUG-136074) QTreeView a11y: Frequent Qt Creator crashes when Orca
screen reader is active
* [QTBUG-133855](https://bugreports.qt.io/browse/QTBUG-133855)  QtreeView sporadic crash when setCurrentIndex is called
* [QTBUG-126515](https://bugreports.qt.io/browse/QTBUG-126515) Buttons are too small, focus rectangle only seen at the
rounded corners
* [QTBUG-137249](https://bugreports.qt.io/browse/QTBUG-137249) QML Screen.orientation on iOS does not provide all
directions
* [QTBUG-137038](https://bugreports.qt.io/browse/QTBUG-137038) QByteArray::toDouble() behavior changed on whitespaces
only string
* [QTBUG-137041](https://bugreports.qt.io/browse/QTBUG-137041) Schannel plugin incorrectly verifies the
NetscapeCertType extension
* [QTBUG-137346](https://bugreports.qt.io/browse/QTBUG-137346) [Reg 6.8.0->6.8.1]QTableView ignores the stylesheet
background color when hovering over the items.
* [QTBUG-126743](https://bugreports.qt.io/browse/QTBUG-126743) If QT_ANDROID_PACKAGE_SOURCE_DIR is set to a specific
path, a build folder is recursively created within the build folder.
* [QTBUG-136493](https://bugreports.qt.io/browse/QTBUG-136493) FFmpeg not properly configured with multi-abi builds
* [QTBUG-113401](https://bugreports.qt.io/browse/QTBUG-113401) QtConcurrent::run parameter order documentation wrong
* [QTBUG-137157](https://bugreports.qt.io/browse/QTBUG-137157) [macOS] QAccessibleInterface::window() is never called;
accessibility tools cannot see the top-level window that holds a
widget/Item
* [QTBUG-25938](https://bugreports.qt.io/browse/QTBUG-25938) Checkable QGroupBox doesn't keep "enabled" status of
children
* [QTBUG-137011](https://bugreports.qt.io/browse/QTBUG-137011) The icon of the QCommandLinkButton does not update when
the button's visibility is set to true.
* [QTBUG-136990](https://bugreports.qt.io/browse/QTBUG-136990) QML property information rendered mangled (Assistant, Qt
Creator)
* [QTBUG-133221](https://bugreports.qt.io/browse/QTBUG-133221) [REG: 6.7->6.8] SVG file mime type not recognized if the
file contains xml header
* [QTBUG-136097](https://bugreports.qt.io/browse/QTBUG-136097) Can't use the properties and signals when definitions
such as them are enabled by `__has_include`
* [QTBUG-137579](https://bugreports.qt.io/browse/QTBUG-137579) QDebugStateSaver not documented well
* [QTBUG-135044](https://bugreports.qt.io/browse/QTBUG-135044) tst_QStringApiSymmetry fails under ASAN
(GenerationalCollator is leaked?)
* [QTBUG-136055](https://bugreports.qt.io/browse/QTBUG-136055) QWebSocketServer creates persistent files in
Microsoft/Crypto/RSA on each new client connection.
* [QTBUG-137763](https://bugreports.qt.io/browse/QTBUG-137763) windeployqt crash when run through cmake
* [QTBUG-120031](https://bugreports.qt.io/browse/QTBUG-120031) xcb: Modal state may get lost due to a race
* [QTBUG-137838](https://bugreports.qt.io/browse/QTBUG-137838) QMultiHash has undocumented erase method
* [QTBUG-133029](https://bugreports.qt.io/browse/QTBUG-133029) Documentation is inconsistent wrt QChronoTimer
* [QTBUG-87180](https://bugreports.qt.io/browse/QTBUG-87180) Typo in the description of QGraphicsSimpleTextItem class
* [QTBUG-123063](https://bugreports.qt.io/browse/QTBUG-123063) XCB flakiness in tst_qgraphicsscene (race condition
caused by the event dispatcher on Linux)
* [QTBUG-130978](https://bugreports.qt.io/browse/QTBUG-130978) Auto-scrolling breaks when dragging and dropping an item
in QTreeView.
* [QTBUG-137882](https://bugreports.qt.io/browse/QTBUG-137882) top-level build, examples don't respect -linker
configure option
* [QTBUG-133656](https://bugreports.qt.io/browse/QTBUG-133656) During Transition from DST back to standard time. the
local clock time repeats an hour.
* [QTBUG-134795](https://bugreports.qt.io/browse/QTBUG-134795) Add note about HAVE_TICK_COUNTER dependency
* [QTBUG-125319](https://bugreports.qt.io/browse/QTBUG-125319) Scaling issue occurs when the window is moved due to
disconnecting the screen.
* [QTBUG-78013](https://bugreports.qt.io/browse/QTBUG-78013) QIdentityProxyModel::match inappropriately mixes use of
proxy model index and source model data method
* [QTBUG-49564](https://bugreports.qt.io/browse/QTBUG-49564) QTextCharFormat fontPointSize() doesnt not return the
same as QTextCharFormat font().pointSize()
* [QTBUG-135337](https://bugreports.qt.io/browse/QTBUG-135337) crash when connecting with RDP
* [QTBUG-136960](https://bugreports.qt.io/browse/QTBUG-136960) Checkbox in QTreeview shows black outline in dark mode
* [QTBUG-138196](https://bugreports.qt.io/browse/QTBUG-138196) [REG dev] Fusion: Buttons and comboboxes outlined
* [QTBUG-137806](https://bugreports.qt.io/browse/QTBUG-137806) [Android][A11y] Role of UI elements is missing
* [QTBUG-133761](https://bugreports.qt.io/browse/QTBUG-133761) Update Qt Creator help mode colours to match the current
themes
* [QTBUG-127549](https://bugreports.qt.io/browse/QTBUG-127549) QDomNode::save() takes huge amount of time. 10x worse
performance when compared to Qt 5
* [QAA-2836](https://bugreports.qt.io/browse/QAA-2836) Make sure that all references to "Qt Android" are changed to
"Qt for Android"
* [QTBUG-134557](https://bugreports.qt.io/browse/QTBUG-134557) QOpenGLFramebufferObject seems to leak
QOpenGLSharedResourceGuards
* [QTBUG-115926](https://bugreports.qt.io/browse/QTBUG-115926) WASM: In the QML Accessibility demo application, menu
items are not getting focus.
* [QTBUG-83817](https://bugreports.qt.io/browse/QTBUG-83817) potential out-of-bounds access in qcssparser
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-134250](https://bugreports.qt.io/browse/QTBUG-134250) qdoc fails to report warnings for incorrect \fn
signatures
* [QTBUG-86387](https://bugreports.qt.io/browse/QTBUG-86387) Support consuming XCFramework with qmake
* [QTBUG-134105](https://bugreports.qt.io/browse/QTBUG-134105) tst_qscroller::overshoot() is flaky on macOS
* [QTBUG-134671](https://bugreports.qt.io/browse/QTBUG-134671) [VxWorks] QEGLPlatformContext::getProcAddress doesn't
work with static ogl libraries
* [QTBUG-133215](https://bugreports.qt.io/browse/QTBUG-133215) [Reg 6.6 -> 6.8] QMainWindow removes titlebar exception
* [QTBUG-134148](https://bugreports.qt.io/browse/QTBUG-134148) When relying on implicit PCH, QML_ELEMENT is not
processed by qmltyperegistrar
* [QTBUG-127012](https://bugreports.qt.io/browse/QTBUG-127012) iOS: ASSERT: "qmlType.metaObject()" in
fileqqmltypedata.cpp, line 1019
* [QTBUG-134883](https://bugreports.qt.io/browse/QTBUG-134883) QML on Windows: Unable to assign ClassA to ClassA
* [QTBUG-130480](https://bugreports.qt.io/browse/QTBUG-130480) Windows 11 Style does not change the palette before
QEvent::PaletteChange
* [QTBUG-133522](https://bugreports.qt.io/browse/QTBUG-133522) Continuation on 'mapped' yields single result only
* [QTBUG-122980](https://bugreports.qt.io/browse/QTBUG-122980) [REG -> dev] Unity Build broken
* [QTBUG-135055](https://bugreports.qt.io/browse/QTBUG-135055) QScroller::grabGesture() appears to leak its
QFlickGestureRecognizer
* [QTBUG-131459](https://bugreports.qt.io/browse/QTBUG-131459) QDoc: No warning if \qmltype contains \inherits with
non-existing type
* [QTBUG-135146](https://bugreports.qt.io/browse/QTBUG-135146) [vxworks] not possible to build vkb with static build
and dlopen feature turned off
* [QTBUG-135151](https://bugreports.qt.io/browse/QTBUG-135151) UB when active menu of a menu bar is being deleted
* [QTBUG-134913](https://bugreports.qt.io/browse/QTBUG-134913) QLocale::toDouble() gives unexpected result for same
decimal and grouping symbol
* [QTBUG-129754](https://bugreports.qt.io/browse/QTBUG-129754) Top flaky test: tst_qgesturerecognizer::touchReplay
* [QTBUG-135626](https://bugreports.qt.io/browse/QTBUG-135626) QPointer causes unneccessary (invalid) downcasts
* [QTBUG-135621](https://bugreports.qt.io/browse/QTBUG-135621) gn.py needs an -isysroot argument but configure doesn't
create it
* [QTBUG-119205](https://bugreports.qt.io/browse/QTBUG-119205) tst_Android::orientationChange is flaky on android
* [QTBUG-135966](https://bugreports.qt.io/browse/QTBUG-135966) Blacklist tst_QFileDialog::clearLineEdit() on vxworks
* [QTBUG-135976](https://bugreports.qt.io/browse/QTBUG-135976) Memory leaks in QAlphaWidget and QRollEffect
* [QTBUG-136358](https://bugreports.qt.io/browse/QTBUG-136358) FAIL!  :
tst_QTimer::crossThreadSingleShotDestruction(1s) 'deadTimerDestroyed'
returned FALSE.
* [QTBUG-136101](https://bugreports.qt.io/browse/QTBUG-136101) Minimal configuration compile with autotests
* [QTBUG-10506](https://bugreports.qt.io/browse/QTBUG-10506) QCalendarWidget in Chinese locale shows wrong weekday
names
* [QTBUG-84877](https://bugreports.qt.io/browse/QTBUG-84877) QLocale::system() uses short names of days and months for
narrow formats
* [QTBUG-136722](https://bugreports.qt.io/browse/QTBUG-136722) [VxWorks] qthread_unix contains DKM related code
* [QTBUG-136716](https://bugreports.qt.io/browse/QTBUG-136716) QDockWidget glitches when moving/pushing unless undocked
and redocked
* [QTBUG-136755](https://bugreports.qt.io/browse/QTBUG-136755) QQuickWindow::grabWindow() results in a black background
color instead of being transparent with the Offscreen platform.
* [QTBUG-131894](https://bugreports.qt.io/browse/QTBUG-131894) qtranslator loads wrong locale
* [QTBUG-122590](https://bugreports.qt.io/browse/QTBUG-122590) Transparency not working correctly for Window Embedding
in QML
* [QTBUG-135859](https://bugreports.qt.io/browse/QTBUG-135859) WindowContainer cannot handle transparent Window
properly
* [QTBUG-137069](https://bugreports.qt.io/browse/QTBUG-137069) tst_QWidget::palettePropagation3() runs into UB
* [QTBUG-116197](https://bugreports.qt.io/browse/QTBUG-116197) org.freedesktop.appearance.color-scheme is supported in
a weird way
* [QTBUG-137228](https://bugreports.qt.io/browse/QTBUG-137228) Cross-compiled ARM64 Windows binaries are not digitally
signed
* [QTBUG-122596](https://bugreports.qt.io/browse/QTBUG-122596) [REG 6.7.0->6.8.0] error in configure step, top level
build, MinGW
* [QTBUG-122642](https://bugreports.qt.io/browse/QTBUG-122642) The SQL QODBC driver implementation fails to escape
passwords set with setPassword(...) when using special characters.
* [QTBUG-112355](https://bugreports.qt.io/browse/QTBUG-112355) ShaderEffectSource with recursive shader causes magenta
texture on Apple Silicon
* [QTBUG-55421](https://bugreports.qt.io/browse/QTBUG-55421) broken links to QBasicAtomic* in published docs
* [QTBUG-132775](https://bugreports.qt.io/browse/QTBUG-132775) QSortFilterProxyModel fails to receive beginResetModel
* [QTBUG-131897](https://bugreports.qt.io/browse/QTBUG-131897) pdf viewer is not working on nano browser and simple
browser sample apps
* [QTBUG-134900](https://bugreports.qt.io/browse/QTBUG-134900) QUrl's operator==() is taking bygone data into account
* [QTBUG-134896](https://bugreports.qt.io/browse/QTBUG-134896) QUrl's qHash() is inconsistent with its operator==
* [QTBUG-134208](https://bugreports.qt.io/browse/QTBUG-134208) Mnemonic annotation is passed to screen readers

### qtsvg
* [QTBUG-134044](https://bugreports.qt.io/browse/QTBUG-134044) SvgHandler might access out of bound
* [QTBUG-135483](https://bugreports.qt.io/browse/QTBUG-135483) [REG 6.7-> 6.8] Loading order affects QIcon state and
mode when adding svg images
* [QTBUG-123817](https://bugreports.qt.io/browse/QTBUG-123817) QTextLayout::draw() renders text as path and not text
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-49160](https://bugreports.qt.io/browse/QTBUG-49160) Rendering SVG icon in QFileBox on Fedora22 crashes Qt
* [QTBUG-126268](https://bugreports.qt.io/browse/QTBUG-126268) Text rendering does not handle fill and stroke opacities
correctly

### qtdeclarative
* [QTBUG-134274](https://bugreports.qt.io/browse/QTBUG-134274) QML LocationPermission is not a type
* [QTBUG-134226](https://bugreports.qt.io/browse/QTBUG-134226) Warning about application/x-color in QtQuick Drag
* [QTBUG-127098](https://bugreports.qt.io/browse/QTBUG-127098) qmllint: False positive for required property
* [QTBUG-134247](https://bugreports.qt.io/browse/QTBUG-134247) TableView: edit delegate commit upon losing focus
* [QTBUG-134442](https://bugreports.qt.io/browse/QTBUG-134442) tst_qqmlcomponent::loadFromQrc() randomly fails on QNX
* [QTBUG-134001](https://bugreports.qt.io/browse/QTBUG-134001) [iOS] The dial handle is misaligned with the circular
path of the dial
* [QTBUG-129424](https://bugreports.qt.io/browse/QTBUG-129424) iOS style: Dial handle doesn't follow groove
* [QTBUG-134398](https://bugreports.qt.io/browse/QTBUG-134398) Qt Design Studio does not work with Qt 6.8 because of
QML caching
* [QTBUG-134725](https://bugreports.qt.io/browse/QTBUG-134725) Mark QQC2 fusion style as a dependency for macos style
* [QTBUG-67368](https://bugreports.qt.io/browse/QTBUG-67368) QJSValue::strictlyEquals documentation error
* [QTBUG-132931](https://bugreports.qt.io/browse/QTBUG-132931) QJSEngine leaks memory
* [QTBUG-130116](https://bugreports.qt.io/browse/QTBUG-130116) Broken accessibility tree in (at least) certain lists
* [QTBUG-134664](https://bugreports.qt.io/browse/QTBUG-134664) FAIL!  :
tst_examples::examples(examples/quick/multieffect/testbed/qml/main.qml)
Received a fatal error
* [QTBUG-134492](https://bugreports.qt.io/browse/QTBUG-134492) Thread sanitizer (TSAN) warns about data race with QSG
Scenegraph (qsgmaterial)
* [QTBUG-122043](https://bugreports.qt.io/browse/QTBUG-122043) The button appears to be pressed twice, even if it's
pressed only once while you are pressing another button at the same time
on the Android app
* [QTBUG-135039](https://bugreports.qt.io/browse/QTBUG-135039) Import in one component affects type resolution in
another one
* [QTBUG-95887](https://bugreports.qt.io/browse/QTBUG-95887) tst_FlickableInterop is flaky on opensuse
* [QTBUG-132763](https://bugreports.qt.io/browse/QTBUG-132763) Regression: keyboard navigation jumps to main view when
drawer is open
* [QTBUG-122405](https://bugreports.qt.io/browse/QTBUG-122405) tst_qquickhoverhandler::window is flaky on OpenSuse
* [QTBUG-134688](https://bugreports.qt.io/browse/QTBUG-134688) Aliases of properties of bindables don't emit change
signals
* [QTBUG-134781](https://bugreports.qt.io/browse/QTBUG-134781) qmlls: lints out-of-date versions of files in the linter
* [QTBUG-75215](https://bugreports.qt.io/browse/QTBUG-75215) tst_qquickapplication::active() is flaky on opensuse
* [QTBUG-123550](https://bugreports.qt.io/browse/QTBUG-123550) Top flaky test: tst_qquickapplication::active on
openSUSE_15_5 X86_64.
* [QTBUG-122031](https://bugreports.qt.io/browse/QTBUG-122031) tst_qquickapplication::state() is flaky on opensuse
* [QTBUG-132886](https://bugreports.qt.io/browse/QTBUG-132886) qmlformat: The colon in the switch statement is in the
wrong position.
* [QTBUG-133316](https://bugreports.qt.io/browse/QTBUG-133316) qmldom/qmlformat: Comments are broken in certain
positions
* [QTBUG-123386](https://bugreports.qt.io/browse/QTBUG-123386) QmlFormat. Incorrect handling of some comments
* [QTBUG-127107](https://bugreports.qt.io/browse/QTBUG-127107) qmllint does not warn about redeclaration of JS
variables
* [QTBUG-135740](https://bugreports.qt.io/browse/QTBUG-135740) Quick dialogs and templates to compile when draganddrop
feature is disabled
* [QTBUG-135279](https://bugreports.qt.io/browse/QTBUG-135279) FTBFS libc++abi: terminating due to uncaught exception
of type std::runtime_error: file is already signed. pass -f to sign
regardless
* [QTBUG-135475](https://bugreports.qt.io/browse/QTBUG-135475) QML Plugin Example shows a blank window
* [QTBUG-129329](https://bugreports.qt.io/browse/QTBUG-129329) QML Preview doesn't update properly
* [QTBUG-134911](https://bugreports.qt.io/browse/QTBUG-134911) Regression: C++ generated from QML throws compiler
warning (declaration of unit vs. global declaration)
* [QTBUG-134778](https://bugreports.qt.io/browse/QTBUG-134778) Binding: short syntax broken with ComponentBehavior:
Bound
* [QTBUG-135200](https://bugreports.qt.io/browse/QTBUG-135200) QQ4A example documentation does not point where to find
the examples
* [QTBUG-135437](https://bugreports.qt.io/browse/QTBUG-135437) code snippet doesn't build due to a function reference
from inside Component
* [QTBUG-134782](https://bugreports.qt.io/browse/QTBUG-134782) Binding: Documentation should point to multiple bindings
with new syntax
* [QTBUG-135815](https://bugreports.qt.io/browse/QTBUG-135815) QSG wrongly batches QSGGeometryNodes with different
lineWidth
* [QTBUG-135649](https://bugreports.qt.io/browse/QTBUG-135649) qmlcachegen reaches Q_UNREACHABLE
* [QTBUG-134887](https://bugreports.qt.io/browse/QTBUG-134887) [REG 6.9 -> 6.10] qmllint: bogus required property
warning with generalized grouped property
* [QTBUG-135980](https://bugreports.qt.io/browse/QTBUG-135980) error: 'O_RDONLY' was not declared in this scope
* [QTBUG-134772](https://bugreports.qt.io/browse/QTBUG-134772) Occasional crashs on debug service rampdowns
* [QTBUG-135367](https://bugreports.qt.io/browse/QTBUG-135367) Compiler warning in qmlcachegen generated code
* [QTBUG-134922](https://bugreports.qt.io/browse/QTBUG-134922) [REG 6.7 → 6.8] Regression with Qml Binding type
(destruction) in 6.8
* [QTBUG-134206](https://bugreports.qt.io/browse/QTBUG-134206) Using ListElement with QML Type Compiler leads to link
errors
* [QTBUG-135387](https://bugreports.qt.io/browse/QTBUG-135387) Division by zero when changing path elements of
ShapePath imperatively
* [QTBUG-135975](https://bugreports.qt.io/browse/QTBUG-135975) Hover event delivery causes memory leak
* [QTBUG-136120](https://bugreports.qt.io/browse/QTBUG-136120) Qml Runtime fails to correct escape -a after --
* [QTCREATORBUG-32634](https://bugreports.qt.io/browse/QTCREATORBUG-32634) Autocompletion for enum doesn't work without
restarting qml language server
* [QTBUG-134606](https://bugreports.qt.io/browse/QTBUG-134606) eventPoint documentation is hard to read
* [QTBUG-135334](https://bugreports.qt.io/browse/QTBUG-135334) [Reg 6.4 -> 6.5] qmlRegisterSingletonInstance does not
work with importPath over http
* [QTBUG-136452](https://bugreports.qt.io/browse/QTBUG-136452) qmllint - no way to treat `missing-enum-entry` as
warning
* [QTBUG-135020](https://bugreports.qt.io/browse/QTBUG-135020) qmllint: clean up linting categories
* [QTBUG-136008](https://bugreports.qt.io/browse/QTBUG-136008) [REG: 6.8.2 -> 6.9] False warning about missing required
property when using inline component
* [QTBUG-135244](https://bugreports.qt.io/browse/QTBUG-135244) qmlcachegen takes a long time to compile
fluentwinui3/Slider.qml
* [QTBUG-136250](https://bugreports.qt.io/browse/QTBUG-136250) TextEditor example: can't set multiple font attributes
at the same time
* [QTBUG-136127](https://bugreports.qt.io/browse/QTBUG-136127) Crash when calling Object.value() on QQmlListModel
* [QTBUG-136058](https://bugreports.qt.io/browse/QTBUG-136058) [Reg] qmllint: mix up between required properties
* [QTBUG-135965](https://bugreports.qt.io/browse/QTBUG-135965) Application freezes when trigger an Action's shortcut in
sub-sub Menu
* [QTBUG-53863](https://bugreports.qt.io/browse/QTBUG-53863) tst_QQuickListView::populateTransitions(static, no
populate) crashes randomly
* [QTBUG-136735](https://bugreports.qt.io/browse/QTBUG-136735) Line: 1: Internal process (QML Puppet) crashed.
* [QTBUG-136256](https://bugreports.qt.io/browse/QTBUG-136256) When menu items are dynamically added to Menu, it should
resize to fit
* [QTBUG-136552](https://bugreports.qt.io/browse/QTBUG-136552) QMLLS crashes
* [QTBUG-128864](https://bugreports.qt.io/browse/QTBUG-128864) Vulkan RHI Renderer freezes on Windows sometimes after
pressing Win-D
* [QTBUG-136192](https://bugreports.qt.io/browse/QTBUG-136192) qmlformat fails to write file
* [QTBUG-136672](https://bugreports.qt.io/browse/QTBUG-136672) QQuickComboBox::setModel() does an unguarded
qvariant_cast on the previous value
* [QTBUG-133858](https://bugreports.qt.io/browse/QTBUG-133858) tst_QQuickMenu::contextMenuKeyboard is flaky
* [QTBUG-136933](https://bugreports.qt.io/browse/QTBUG-136933) Can't build QtQ4A examples from command line
* [QTBUG-134880](https://bugreports.qt.io/browse/QTBUG-134880) Disable edge-to-edge feature of Android 15 on
qtquickview examples
* [QTBUG-135286](https://bugreports.qt.io/browse/QTBUG-135286) Qml Property Cache heap-use-after-free
* [QTBUG-136581](https://bugreports.qt.io/browse/QTBUG-136581) [REG 6.5.3 -> 6.8.3] ListModel set() on existing index
fails if setting data retrieved from C++ QVariantMap containing a
QVariantList role
* [QTBUG-96580](https://bugreports.qt.io/browse/QTBUG-96580) Missing documentation for QSGRenderNode::RenderState
* [QTBUG-136947](https://bugreports.qt.io/browse/QTBUG-136947) EventModel::repopulate() missing endResetModel() on
early return in eventcalendar example
* [QTBUG-137086](https://bugreports.qt.io/browse/QTBUG-137086) [Reg 6.2 -> 6.5] Crashing QML code
* [QTBUG-137072](https://bugreports.qt.io/browse/QTBUG-137072) [REG: 6.8 → 6.9] QMetaType::metaObject crashes the
program
* [QTBUG-135158](https://bugreports.qt.io/browse/QTBUG-135158) Quick Popup window can no longer have negative x on
Wayland
* [QTBUG-136810](https://bugreports.qt.io/browse/QTBUG-136810) crash on qml cache checksum mismatch
* [QTBUG-136439](https://bugreports.qt.io/browse/QTBUG-136439) No more possible to use a Loader for QML hot/live
reloading since Qt 6.8.3
* [QTBUG-136354](https://bugreports.qt.io/browse/QTBUG-136354) DragHandler doesn't account for scene changes when
calculating threshold
* [QTBUG-133314](https://bugreports.qt.io/browse/QTBUG-133314) Artifacts in rounded rectangle corners with borders
using software backend
* [QTBUG-136738](https://bugreports.qt.io/browse/QTBUG-136738) [Software renderer] Rectangle with e.g. topLeftRadius
set corner drawn black
* [QTBUG-132644](https://bugreports.qt.io/browse/QTBUG-132644) Cannot receive mouse move events when modal dialog is
open
* [QTBUG-134545](https://bugreports.qt.io/browse/QTBUG-134545) Mouse move and touch update events are not delivered
correctly when there are modal dialogs
* [QTBUG-133793](https://bugreports.qt.io/browse/QTBUG-133793) QT_QML_GENERATE_QMLLS_INI doesn't update file if build
directory changes
* [QTBUG-116675](https://bugreports.qt.io/browse/QTBUG-116675) QQuickWindow::grabWindow renders too small on macOS
retina
* [QTBUG-136699](https://bugreports.qt.io/browse/QTBUG-136699) Unexpected removal of enabled binding when parent
enabled is toggled off
* [QTBUG-134403](https://bugreports.qt.io/browse/QTBUG-134403) QtQuick Rectangle: Gradient not displayed when the color
property is set to transparent.
* [QTBUG-135795](https://bugreports.qt.io/browse/QTBUG-135795) QML Locale cannot be compiled in Direct Mode
* [QTBUG-134099](https://bugreports.qt.io/browse/QTBUG-134099) [REG 6.7.3->6.8]Global position for QHoverEvent issued
from a QQuickItem inside a QQuickWidget is wrong.
* [QTBUG-134635](https://bugreports.qt.io/browse/QTBUG-134635) A floating-point precision error with the slider value.
* [QTBUG-137413](https://bugreports.qt.io/browse/QTBUG-137413) [REG 6.9.0 -> 6.9.1] qmlformat crashes on musl
* [QTBUG-136492](https://bugreports.qt.io/browse/QTBUG-136492) TreeView: Editable and non-editable items not working
correctly
* [QTBUG-133924](https://bugreports.qt.io/browse/QTBUG-133924) IconLabel children are positioned under Icon & text
* [QTBUG-137035](https://bugreports.qt.io/browse/QTBUG-137035) qmllint gets stuck
* [QTBUG-137411](https://bugreports.qt.io/browse/QTBUG-137411) [REG 6.9.0 -> 6.9.1] Building for iOS failed:
qmlcachegen segmentation fault
* [QTBUG-137196](https://bugreports.qt.io/browse/QTBUG-137196) qmlcachegen crashes in QQmlJSScope::filePath
* [QTBUG-136998](https://bugreports.qt.io/browse/QTBUG-136998) qmllint crashes when checking  required properties
* [QTBUG-131886](https://bugreports.qt.io/browse/QTBUG-131886) Wrong delta threshold for MultiPointTouchArea using
scale
* [QTBUG-112355](https://bugreports.qt.io/browse/QTBUG-112355) ShaderEffectSource with recursive shader causes magenta
texture on Apple Silicon
* [QTBUG-137561](https://bugreports.qt.io/browse/QTBUG-137561) FAIL!  : tst_QQuickColorDialogImpl::defaults() Received
a warning that resulted in a failure
* [QTBUG-135255](https://bugreports.qt.io/browse/QTBUG-135255) The type compiler incorrectly gives a warning about
insufficient annotation for enum types.
* [QTBUG-135295](https://bugreports.qt.io/browse/QTBUG-135295) [Reg 5.15 -> 6.8] Binding crashes when combined with
StackView and Loader
* [QTBUG-137469](https://bugreports.qt.io/browse/QTBUG-137469) "Cannot assign object to list property" error message
isn't descriptive enough
* [QTBUG-137416](https://bugreports.qt.io/browse/QTBUG-137416) FAIL!  : tst_QQuickFileDialogImpl::defaults() Compared
values are not the same
* [QTBUG-132607](https://bugreports.qt.io/browse/QTBUG-132607) Unexpected text's rectangle behavior in a row
* [QTBUG-137115](https://bugreports.qt.io/browse/QTBUG-137115) [REG 6.5 → 6.8] Issue with inline components and setData
* [QTBUG-94147](https://bugreports.qt.io/browse/QTBUG-94147) QSGGeometryNode docs snippet shows Qt 6 incompatible code
* [QTBUG-136235](https://bugreports.qt.io/browse/QTBUG-136235) Qt 6.8.3 A signal 11 (SIGSEGV) crash observed while
running qtquickview_kotlin sample application (Android 11 / API 30 )
* [QTBUG-137705](https://bugreports.qt.io/browse/QTBUG-137705) qmlls: lazy QmlFile in DOM loads with incorrect import
path
* [QTBUG-134600](https://bugreports.qt.io/browse/QTBUG-134600) FileDialog's currentFolder shows regression on Debian
* [QTBUG-137540](https://bugreports.qt.io/browse/QTBUG-137540) [Reg 6.5.0 -> 6.5.5] Compilation blog post example
doesn't work anymore
* [QTBUG-137256](https://bugreports.qt.io/browse/QTBUG-137256) qmllint warns about missing-type for properties of type
QVector<EnumClass>
* [QTBUG-137270](https://bugreports.qt.io/browse/QTBUG-137270) QML: model-views: bindings evaluate after item/app
destruction -> crashes
* [QTBUG-127863](https://bugreports.qt.io/browse/QTBUG-127863) DragHandler Activates When Dragging Starts Outside the
Item and Moves Inside
* [QTBUG-138053](https://bugreports.qt.io/browse/QTBUG-138053) qqmlprivate compile issue with nvcc
* [QTBUG-137030](https://bugreports.qt.io/browse/QTBUG-137030) Assertion in qmllint
* [QTBUG-124157](https://bugreports.qt.io/browse/QTBUG-124157) QJSEngine crashes when evaluating arithmetic operation
on array with self referencing
* [QTBUG-137326](https://bugreports.qt.io/browse/QTBUG-137326) [Reg 5.15 -> 6.2] Crash in
QQmlAbstractBinding::removeFromObject()
* [QTBUG-118188](https://bugreports.qt.io/browse/QTBUG-118188) QML evaluates bindings after destruction, possibly
resulting in segmentation faults
* [QTBUG-134208](https://bugreports.qt.io/browse/QTBUG-134208) Mnemonic annotation is passed to screen readers
* [QTBUG-134269](https://bugreports.qt.io/browse/QTBUG-134269) Attached properties using REVISION produce error
* [QTBUG-134250](https://bugreports.qt.io/browse/QTBUG-134250) qdoc fails to report warnings for incorrect \fn
signatures
* [QTBUG-110243](https://bugreports.qt.io/browse/QTBUG-110243) Resources are lost when linking static libraries using
CMake build system in a separate project
* [QTCREATORBUG-32591](https://bugreports.qt.io/browse/QTCREATORBUG-32591) qmlls still not work in qt creator
* [QTBUG-133530](https://bugreports.qt.io/browse/QTBUG-133530) Several Controls tests failing after test coverage
restored
* [QTBUG-134768](https://bugreports.qt.io/browse/QTBUG-134768) QLocale::toStrings uses E instead of e
* [QTBUG-135288](https://bugreports.qt.io/browse/QTBUG-135288) qmlsc: crash on if + for
* [QTBUG-134251](https://bugreports.qt.io/browse/QTBUG-134251) Qt Quick for Android is hard to find
* [QTBUG-109553](https://bugreports.qt.io/browse/QTBUG-109553) CMake deployment API creates too deep directory
hierarchy when DESTDIR is set
* [QTBUG-117948](https://bugreports.qt.io/browse/QTBUG-117948) qt_generate_deploy_qml_app_script() deploys QML plugin
target but not the corresponding backing target
* [QTBUG-135164](https://bugreports.qt.io/browse/QTBUG-135164) TextArea with description and no name results in empty
a11y description
* [QTBUG-129947](https://bugreports.qt.io/browse/QTBUG-129947) tst_QQuickTextEdit::mouseSelection() is flaky on macOS
arm 12/13
* [QTBUG-133492](https://bugreports.qt.io/browse/QTBUG-133492) Issue found on Qt 6.8 variant that doesn't exist on 6.6
* [QTBUG-135032](https://bugreports.qt.io/browse/QTBUG-135032) Uncreatable value types behave erratically
* [QTBUG-105856](https://bugreports.qt.io/browse/QTBUG-105856) The Menu Item will continue to be highlighted after the
sub menu is closed
* [QTBUG-136031](https://bugreports.qt.io/browse/QTBUG-136031) MouseArea in a ApplicationWindow's background can not be
hovered since 6.9.0
* [QTBUG-136251](https://bugreports.qt.io/browse/QTBUG-136251) TextEditor example: selection is lost when you open the
Font or Color dialog from the context menu
* [QTBUG-136101](https://bugreports.qt.io/browse/QTBUG-136101) Minimal configuration compile with autotests
* [QTBUG-136248](https://bugreports.qt.io/browse/QTBUG-136248) Crash in QQmlPrivate::callQObjectMethod
* [QTBUG-134790](https://bugreports.qt.io/browse/QTBUG-134790) QML AnchorChanges do not compile in strict mode
* [QTBUG-136755](https://bugreports.qt.io/browse/QTBUG-136755) QQuickWindow::grabWindow() results in a black background
color instead of being transparent with the Offscreen platform.
* [QTBUG-87708](https://bugreports.qt.io/browse/QTBUG-87708) [Reg 5.15.0 -> 5.15.1] header's width isn't resized to
window's width when Layout is used
* [QTBUG-51285](https://bugreports.qt.io/browse/QTBUG-51285) Using nested QtQuick Layouts with spacing generates
binding loops
* [QTBUG-134800](https://bugreports.qt.io/browse/QTBUG-134800) Window.window cannot work as a target of Connections QML
in GridView/RowLayout
* [QTBUG-127605](https://bugreports.qt.io/browse/QTBUG-127605) [QtQuick.Dialogs/Wayland] Native FileDialog does not
respect Qt.ApplicationModal flag
* [QTBUG-133586](https://bugreports.qt.io/browse/QTBUG-133586) F2 shortcut or Ctrl+Click in qml files sometimes leads
to build dir instead of source and sometimes does absolutly nothing
* [QTBUG-118610](https://bugreports.qt.io/browse/QTBUG-118610) ShaderEffectSource in recursive mode with multisampling
is broken
* [QTBUG-122738](https://bugreports.qt.io/browse/QTBUG-122738) QtQuick.Dialogs FileDialog bad color with macOS dark
theme
* [QTBUG-117526](https://bugreports.qt.io/browse/QTBUG-117526) QQuickStylePrivate::fallbackStyle has the wrong value
when using run-time style selection and the fallback style is imported
via the style's qmldir
* [QTBUG-136709](https://bugreports.qt.io/browse/QTBUG-136709) Style import triggers style change
* [QTBUG-137900](https://bugreports.qt.io/browse/QTBUG-137900) QML sslConfiguration has sslOptions propery out of sync
* [QTBUG-137554](https://bugreports.qt.io/browse/QTBUG-137554) qml: list qml --> c++ editing crashes/has no effect
* [QTBUG-137116](https://bugreports.qt.io/browse/QTBUG-137116) Incorrect Semantic Highlighting for QML Property Chains

### qtactiveqt
* [QTBUG-134098](https://bugreports.qt.io/browse/QTBUG-134098) dumpcpp puts native Qt types inside a custom namespace

### qtmultimedia
* [QTBUG-134046](https://bugreports.qt.io/browse/QTBUG-134046) [Android] The audiorecorder example app is crashing when
trying to record anything with disallowed permissions
* [QTBUG-134412](https://bugreports.qt.io/browse/QTBUG-134412) Fix copyAllFiles in multimediatestlib to copy
recursively
* [QTBUG-131711](https://bugreports.qt.io/browse/QTBUG-131711) QML video example: Center Box that renders camera feed
Misalign on Maximizing/Minimizing
* [QTBUG-132755](https://bugreports.qt.io/browse/QTBUG-132755) External USB webcam has incorrect rotation applied
* [QTBUG-132754](https://bugreports.qt.io/browse/QTBUG-132754) List of cameras not getting updated
* [QTBUG-133135](https://bugreports.qt.io/browse/QTBUG-133135) Paused or completed video playback freezes application
using MediaPlayer (gstreamer backend)
* [QTBUG-119141](https://bugreports.qt.io/browse/QTBUG-119141) MediaPlayer-example The data of the files is editable,
but cannot be saved
* [QTBUG-135021](https://bugreports.qt.io/browse/QTBUG-135021) docs link to QVideoFrameFormat::PixelFormat goes to
wikipedia instead
* [QTBUG-135172](https://bugreports.qt.io/browse/QTBUG-135172) FindFFmpeg.cmake doesn't look for correct libraries on
iOS
* [QTBUG-134882](https://bugreports.qt.io/browse/QTBUG-134882) QAudioDevice::isFormatSupported() not working on Android
* [QTBUG-135307](https://bugreports.qt.io/browse/QTBUG-135307) Regression 6.8.2 > 6.8.3: Media player does not play mp3
* [QTBUG-122754](https://bugreports.qt.io/browse/QTBUG-122754) [windows] QML media player always uses audio stream,
even when there is no media playing
* [QTBUG-135939](https://bugreports.qt.io/browse/QTBUG-135939) qgstreameraudiooutput.cpp is missing the inclusion of
header files
* [QTBUG-131785](https://bugreports.qt.io/browse/QTBUG-131785) [Boot2Qt] The media player detects 2 video tracks for
the m2v file
* [QTBUG-135256](https://bugreports.qt.io/browse/QTBUG-135256) Camera not functioning if permission granted later
* [QTBUG-132167](https://bugreports.qt.io/browse/QTBUG-132167) QCamera: Handle AVCaptureDevice being in suspended state
* [QTBUG-136003](https://bugreports.qt.io/browse/QTBUG-136003) QVideoSink documentation mentions nonexistent paint()
function
* [QTBUG-129626](https://bugreports.qt.io/browse/QTBUG-129626) [ffmpeg] pc files not found when building against a
system ffmpeg
* [QTBUG-136052](https://bugreports.qt.io/browse/QTBUG-136052) VideoOutput crash with opacity animation
* [QTBUG-135360](https://bugreports.qt.io/browse/QTBUG-135360) Unexpected Qt Multimedia warning message
* [QTBUG-135911](https://bugreports.qt.io/browse/QTBUG-135911) QRhi claims to not support a working texture format.
* [QTBUG-136191](https://bugreports.qt.io/browse/QTBUG-136191) Screencapture example crashes on permission granted
* [QTBUG-134196](https://bugreports.qt.io/browse/QTBUG-134196) R16 video texture formats don't have a working fallback
for GLES 2.0
* [QTBUG-132458](https://bugreports.qt.io/browse/QTBUG-132458) [static linking] undefined symbols for ffmpeg plugin
* [QTBUG-136680](https://bugreports.qt.io/browse/QTBUG-136680) qt_add_ios_ffmpeg_libraries() not working with 6.9
* [QTBUG-137070](https://bugreports.qt.io/browse/QTBUG-137070) [REG 6.9.1 prev snapshot->6.9.1] Multimedia examples not
compiling, Wasm
* [QTBUG-136920](https://bugreports.qt.io/browse/QTBUG-136920) Access violation on QWindowsFormatInfo construction
* [QTBUG-102716](https://bugreports.qt.io/browse/QTBUG-102716) [Windows] Access violation in QWindowsFormatInfo
* [QTBUG-136227](https://bugreports.qt.io/browse/QTBUG-136227) Crash in camera rundown
* [QTBUG-137150](https://bugreports.qt.io/browse/QTBUG-137150) Assertion hit when unplugging microphone device while
recording
* [QTBUG-137360](https://bugreports.qt.io/browse/QTBUG-137360) Qt multimedia compilation error windows 32 bit
* [QTBUG-137308](https://bugreports.qt.io/browse/QTBUG-137308) [Reg B2Qt 6.7.3 -> 6.8.3] glupload not supported in
GStreamer pipeline
* [QTBUG-120693](https://bugreports.qt.io/browse/QTBUG-120693) Corrupt JPEG data
* [QTBUG-136145](https://bugreports.qt.io/browse/QTBUG-136145) Qt Spatial Audio: Add alt texts
* [QTBUG-137173](https://bugreports.qt.io/browse/QTBUG-137173) Windows native multimedia backend does not agree with
Windows Media Player when dealing with rotated video
* [QTBUG-136676](https://bugreports.qt.io/browse/QTBUG-136676) Linking against static FFmpeg that is built with OpenSSL
support fails
* [QTBUG-136802](https://bugreports.qt.io/browse/QTBUG-136802) Linking against static FFmpeg that has VAAPI support
enabled causes build to fail
* [QTBUG-137973](https://bugreports.qt.io/browse/QTBUG-137973) QMediaPlayer example crashing while changing audio
device output
* [QTBUG-138060](https://bugreports.qt.io/browse/QTBUG-138060) Unable to build: no type named 'lock_guard' in namespace
'std' on macos ventura
* [QTBUG-138059](https://bugreports.qt.io/browse/QTBUG-138059) [REG 6.9.0-6.9.1] [windows] Strange Qt warning on
QAudioSource::start() when non-default sample rate is used
* [QTBUG-98145](https://bugreports.qt.io/browse/QTBUG-98145) Android: Avoid empty file format on the AudioRecorder app
* [QTBUG-133914](https://bugreports.qt.io/browse/QTBUG-133914) FFmpeg plugin tests may fail to build on Linux and
Android
* [QTBUG-129758](https://bugreports.qt.io/browse/QTBUG-129758) Audio playback does not work on linux/aarch64 (sailfish
os)
* [QTBUG-110310](https://bugreports.qt.io/browse/QTBUG-110310) FlushMode property missing from VideoOutput
* [QTBUG-135239](https://bugreports.qt.io/browse/QTBUG-135239) external QAudioDevice no longer provides sample rates
* [QTBUG-125238](https://bugreports.qt.io/browse/QTBUG-125238) QVideoFrame::toImage fails on Android with 16 bit per
component planar YUV formats
* [QTBUG-134430](https://bugreports.qt.io/browse/QTBUG-134430) QCamera stops working entirely if device is disconnected
* [QTBUG-135618](https://bugreports.qt.io/browse/QTBUG-135618) [MacOS] Sporadic crashes when call
QVideoFrame::toImage()
* [QTBUG-135951](https://bugreports.qt.io/browse/QTBUG-135951) QMediaRecorder captures video at a much worse quality on
Linux
* [QTBUG-135873](https://bugreports.qt.io/browse/QTBUG-135873) Crash when trying to play video
* [QTBUG-123073](https://bugreports.qt.io/browse/QTBUG-123073) [macOS] QMediaRecorder failed to record an audio after
reconnecting AirPods
* [QTBUG-136632](https://bugreports.qt.io/browse/QTBUG-136632) There is no sound when playing videos (REGRESSION)
* [QTBUG-135281](https://bugreports.qt.io/browse/QTBUG-135281) Qml Camera not work on webassembly
* [QTBUG-
133652](https://bugreports.qt.io/browse/QTBUG-133652) tst_QMediaPlayerBackend::play_playbackLastsForTheExpectedTime is
flaky on Linux
* [QTBUG-136124](https://bugreports.qt.io/browse/QTBUG-136124) tst_qwindowcapturebackend: flaky deadlocks on
opensuse-15.6
*
[QTBUG-135614](https://bugreports.qt.io/browse/QTBUG-135614) recorder_encodesFrames_toValidMediaFile_whenWindowResizes
fails on opensuse/asan
* [QTBUG-129713](https://bugreports.qt.io/browse/QTBUG-129713) Test times out: tst_QMediaFrameInputsBackend::mediaRecor
derWritesVideo_whenInputFrameGrowsOverTime
* [QTBUG-127733](https://bugreports.qt.io/browse/QTBUG-127733) tst_QAudioSink::pullResumeFromUnderrun() failed on
Ubuntu 24.04 offscreen and X11
* [QTBUG-117099](https://bugreports.qt.io/browse/QTBUG-117099) Video jerks when playing (Windows backend)
* [QTBUG-130636](https://bugreports.qt.io/browse/QTBUG-130636) FFmpeg: QCamera::FlashOn is unreliable
* [QTBUG-138000](https://bugreports.qt.io/browse/QTBUG-138000) tst_QAudioSource::pull fails on ubuntu-22.04-x11-tests
* [QTBUG-137984](https://bugreports.qt.io/browse/QTBUG-137984) Unable to compile QtMultimedia Debug under PiOS

### qttools
* [QTBUG-131572](https://bugreports.qt.io/browse/QTBUG-131572) qdoc: Overrides a previous doc for two QML types with
identical name in different modules
* [QTBUG-134250](https://bugreports.qt.io/browse/QTBUG-134250) qdoc fails to report warnings for incorrect \fn
signatures
* [QTBUG-131856](https://bugreports.qt.io/browse/QTBUG-131856) \qmlproperty docs don't mention how to document enum
type
* [QTBUG-133739](https://bugreports.qt.io/browse/QTBUG-133739) Update qdoc manual for \deprecated and \moduleState
* [QTBUG-136736](https://bugreports.qt.io/browse/QTBUG-136736) [REG: 6.5->6.8] ios: Fails if main app target is in a
subdirectory
* [QTBUG-103470](https://bugreports.qt.io/browse/QTBUG-103470) [iOS] CMake translation handling fails
* [QTBUG-117406](https://bugreports.qt.io/browse/QTBUG-117406) [REG 6.6.0beta4->6.7.0] linguist/i18n and qml/qml-i18n
not compiling on iOS
* [QTBUG-96693](https://bugreports.qt.io/browse/QTBUG-96693) QUiLoader resolves  wrong buddy when UI is loaded twice
* [QTBUG-136115](https://bugreports.qt.io/browse/QTBUG-136115) REG: QDoc never links using relative hrefs when running
in single-exec mode
* [QTBUG-138072](https://bugreports.qt.io/browse/QTBUG-138072) Remove traces of <type> argument to \page command from
documentation
* [QTBUG-136158](https://bugreports.qt.io/browse/QTBUG-136158) Qt UI Tools: Add alt texts
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-130006](https://bugreports.qt.io/browse/QTBUG-130006) lupdate: -mno-sse not recognized if binary linked
against Clang libraries built on ARM-based Mac
* [QTBUG-130096](https://bugreports.qt.io/browse/QTBUG-130096) clang-based lupdate fails on macOS 15
* [QTBUG-136963](https://bugreports.qt.io/browse/QTBUG-136963) qdoc/qmlmarkupvisitor.h:78:16: error:
‘QQmlJS::AST::Expression’ has not been declared

### qtdoc
* [QAA-2836](https://bugreports.qt.io/browse/QAA-2836) Make sure that all references to "Qt Android" are changed to
"Qt for Android"
* [QTBUG-135250](https://bugreports.qt.io/browse/QTBUG-135250) Editorial notes on `Qt for Wayland Requirements` page
* [QTBUG-135289](https://bugreports.qt.io/browse/QTBUG-135289) [Examples] Lightning Viewer app misses tags
* [QTBUG-100340](https://bugreports.qt.io/browse/QTBUG-100340) Remove documentation of QPF2 fonts
* [QTBUG-134789](https://bugreports.qt.io/browse/QTBUG-134789) "Contents" menu hidden behind images
* [QTBUG-136036](https://bugreports.qt.io/browse/QTBUG-136036) colorpaletteclient doesn't compile if qml-network is
disabled
* [QTBUG-136482](https://bugreports.qt.io/browse/QTBUG-136482) REG [6.9.0->6.9.1] demos/hangman not compiling on
Android
* [QTBUG-136974](https://bugreports.qt.io/browse/QTBUG-136974) Qt Licensing page does not list Qt Graphs under GPL
licensed modules
* [QTBUG-132833](https://bugreports.qt.io/browse/QTBUG-132833) QT_QPA_EGLFS_ROTATION rotates mouse events but not touch
events
* [QTBUG-133792](https://bugreports.qt.io/browse/QTBUG-133792) Compiling demos/maroon and demos/hangman on
Windows/MacOS fails
* [QTBUG-138105](https://bugreports.qt.io/browse/QTBUG-138105) [Reg 6.5.9 -> 6.8.3] Alarms demo: TumberDelegate can no
longer read properties
* [QTBUG-138169](https://bugreports.qt.io/browse/QTBUG-138169) Document Viewer: Runtime warnings
* [QTBUG-134251](https://bugreports.qt.io/browse/QTBUG-134251) Qt Quick for Android is hard to find
* [QTBUG-134104](https://bugreports.qt.io/browse/QTBUG-134104) Specific Options for Platforms documentation should have
VxWorks
* [QTBUG-133574](https://bugreports.qt.io/browse/QTBUG-133574) Setting QT_DEFAULT_MAJOR_VERSION to 6 doesn't select Qt6
over Qt5
* [QTBUG-136794](https://bugreports.qt.io/browse/QTBUG-136794) QML debugging is excluded in some of the Android
examples and demos

### qtlocation
* [QTBUG-134097](https://bugreports.qt.io/browse/QTBUG-134097) TapHandler with a MapPolyline is not getting tapped
events when the Map is rotated

### qtpositioning
* [QTBUG-137764](https://bugreports.qt.io/browse/QTBUG-137764) QDoc uses incorrect image source
* [QTBUG-106049](https://bugreports.qt.io/browse/QTBUG-106049) Qt Android's QGeoCoordinate API returns altitude in
wrong reference frame

### qtconnectivity
* [QTBUG-133975](https://bugreports.qt.io/browse/QTBUG-133975) BLUETOOTH_SCAN permission in Split APK / AAB
(QtBluetoothUtility.java)
* [QTBUG-133788](https://bugreports.qt.io/browse/QTBUG-133788) Ndef editor example cross-compiling on Windows to
Boot2Qt fails
* [QTBUG-99410](https://bugreports.qt.io/browse/QTBUG-99410) [macOS 12.1] Bluetooth data stream blocked when main menu
opened
* [QTBUG-136576](https://bugreports.qt.io/browse/QTBUG-136576) QNdefNfcSmartPosterRecord might leak memory
* [QTBUG-136692](https://bugreports.qt.io/browse/QTBUG-136692) BLE devices can't be discovered after initial connection
on iOS 18+

### qtwayland
* [QTBUG-134264](https://bugreports.qt.io/browse/QTBUG-134264) "QtShell Compositor" -example install instructions
missing
* [QTBUG-137333](https://bugreports.qt.io/browse/QTBUG-137333) Wayland Compositor + static build + LTO = crash
* [QTBUG-133866](https://bugreports.qt.io/browse/QTBUG-133866) Using qt-shell, if item in dialog is selected with
mouse, no further focus navigation via keyboard possible
* [QTBUG-137814](https://bugreports.qt.io/browse/QTBUG-137814) Build broken with -no-feature-sharedmemory
* [QTBUG-
137945](https://bugreports.qt.io/browse/QTBUG-137945) ‘QtWaylandClient::QWaylandPrimarySelectionSourceV1::zwp_primary_s
election_source_v1_send(const QString&, int32_t)::sigaction oldAction’
has incomplete type and cannot be defined
* [QTBUG-63039](https://bugreports.qt.io/browse/QTBUG-63039) Threaded scenegraph crash with Nvidia drivers in wayland

### qt3d
* [QTBUG-123885](https://bugreports.qt.io/browse/QTBUG-123885) [cmake] name clash between qt3d and qtquick3d - assimp
target
* [QTBUG-106079](https://bugreports.qt.io/browse/QTBUG-106079) qmllint produces warnings from Qt3D imports and
components
* [QTBUG-135394](https://bugreports.qt.io/browse/QTBUG-135394) MouseHandler may crash if it is destroyed while mouse is
being moved
* [QTBUG-124708](https://bugreports.qt.io/browse/QTBUG-124708) QText2DEntity jagged text when using RHI OpenGL backend
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtserialbus
* [QTBUG-135299](https://bugreports.qt.io/browse/QTBUG-135299) error: ‘QElapsedTimer’ was not declared in this scope
* [QTBUG-135791](https://bugreports.qt.io/browse/QTBUG-135791) QModbusClient: : sendRawRequest returns pointer, if
delete immediately, QModbusRtuSerialClientPrivate: : onReadyRead
function crash
* [QTBUG-135132](https://bugreports.qt.io/browse/QTBUG-135132) [qtserialbus] Cannot build manual tests

### qtwebsockets
* [QTBUG-136216](https://bugreports.qt.io/browse/QTBUG-136216) QWebSocket "Invalid UTF-8 Code Encountered" Error in Qt6
* [QTBUG-136153](https://bugreports.qt.io/browse/QTBUG-136153) Qt WebSockets: Add alt texts

### qtwebengine
* [QTBUG-133495](https://bugreports.qt.io/browse/QTBUG-133495) Missing Documentation of 3rd party component usage
* [QTBUG-134107](https://bugreports.qt.io/browse/QTBUG-134107) Qt WebEngine NumLock detection broken using
KeyboardDriver::Xkb
* [QTBUG-134416](https://bugreports.qt.io/browse/QTBUG-134416) Log noise when building Qt WebEngine documentation
* [QTBUG-128440](https://bugreports.qt.io/browse/QTBUG-128440) Top flaky test:
tst_qwebengineview::inputContextQueryInput
* [QTBUG-135620](https://bugreports.qt.io/browse/QTBUG-135620) Qt6WebEngineCoreDeploySupport fails when generating RPM
* [QTBUG-109553](https://bugreports.qt.io/browse/QTBUG-109553) CMake deployment API creates too deep directory
hierarchy when DESTDIR is set
* [QTBUG-119077](https://bugreports.qt.io/browse/QTBUG-119077) CMake deployment API does not deploy Qt Webengine
* [QTBUG-135047](https://bugreports.qt.io/browse/QTBUG-135047) Excessive X11 pixmap usage on 6.9
* [QTBUG-126722](https://bugreports.qt.io/browse/QTBUG-126722) WebEngine: GPU detection is missing "VmWare" in vendor
list
* [QTBUG-135032](https://bugreports.qt.io/browse/QTBUG-135032) Uncreatable value types behave erratically
* [QTBUG-127758](https://bugreports.qt.io/browse/QTBUG-127758) tst_QWebEnginePage::dynamicFrame() failed on Ubuntu
24.04 offscreen(arm64) and X11(x64)
* [QTBUG-126049](https://bugreports.qt.io/browse/QTBUG-126049) text dump does not work realibly with 122-based
* [QTBUG-123607](https://bugreports.qt.io/browse/QTBUG-123607) Vulkan backend rendering only black on X11
* [QTBUG-131897](https://bugreports.qt.io/browse/QTBUG-131897) pdf viewer is not working on nano browser and simple
browser sample apps
* [QTBUG-133608](https://bugreports.qt.io/browse/QTBUG-133608) Missing documentation on how to install Qt WebEngine
* [QTBUG-111907](https://bugreports.qt.io/browse/QTBUG-111907) Crash when touching text field inside WebEngineView
* [QTBUG-135040](https://bugreports.qt.io/browse/QTBUG-135040) macos: Voice Over rect is wrongly calculated for
WebEngine
* [QTBUG-129769](https://bugreports.qt.io/browse/QTBUG-129769) WebEngine ANGLE error: Failed to make current since
context is marked as lost
* [QTBUG-133570](https://bugreports.qt.io/browse/QTBUG-133570) 6.9beta2/Linux/XCB: WebEngine Simple Browser example
crashes
* [QTBUG-135621](https://bugreports.qt.io/browse/QTBUG-135621) gn.py needs an -isysroot argument but configure doesn't
create it
* [QTBUG-137730](https://bugreports.qt.io/browse/QTBUG-137730) Failed to build sources on tqtc/lts-6.8:
XSLT_DEBUG_INIT’ conflicts with a previous declaration
* CVE-2019-16707
* CVE-2024-50602 Stop XML_ResumeParser from crashing #915 (1/2)
* CVE-2024-55549: Fix UAF related to excluded namespaces
* CVE-2025-2783: Incorrect handle provided in unspecified circumstances in Mojo on Windows
* CVE-2025-3071: Inappropriate implementation in Navigations
* CVE-2025-3277
* CVE-2025-3619
* CVE-2025-4051: Insufficient data validation in DevTools
* CVE-2025-4052: Inappropriate implementation in DevTools
* CVE-2025-4609: Incorrect handle provided in unspecified circumstances in Mojo
* CVE-2025-4664: Insufficient policy enforcement in Loader
* CVE-2025-5063: Use after free in Compositing
* CVE-2025-5064: Inappropriate implementation in Background Fetch
* CVE-2025-5065: Inappropriate implementation in FileSystemAccess API
* CVE-2025-5068
* CVE-2025-5281: Inappropriate implementation in BFCache
* CVE-2025-5283: Use after free in libvpx
* CVE-2025-5419
* CVE-2025-6191: Integer overflow in V8
* CVE-2025-6554: Type Confusion in V8
* CVE-2025-24855 Fix use-after-free of XPath context node
* Security bug 325123679
* Security bug 389707046
* Security bug 396460489
* Security bug 397187119
* Security bug 399002829
* Security bug 403364367
* Security bug 407898107
* Security bug 408294914
* Security bug 409243443
* Security bug 420637585
* Security bug 413080347
* Security bug 414858409
* Security bug 415397143
* Security bug 416535738
* Security bug 420885124

### qtcharts
* [QTBUG-115358](https://bugreports.qt.io/browse/QTBUG-115358) QBarCategoryAxis is exported twice
* [QTBUG-135691](https://bugreports.qt.io/browse/QTBUG-135691) Wasm build fails when linking both QtCharts and QtGraphs
* [QTBUG-136770](https://bugreports.qt.io/browse/QTBUG-136770) QLineSeries.clear() does not remove all lines from the
plot in that series
* [QTBUG-135240](https://bugreports.qt.io/browse/QTBUG-135240) Animation effects in ChartView makes PieSlice lose its
alpha channel
* [QTBUG-132790](https://bugreports.qt.io/browse/QTBUG-132790) Unexpected behaviour of QScatterSeries for
selectedPoints, replace and deselectAllPoints
* [QTBUG-132357](https://bugreports.qt.io/browse/QTBUG-132357) setSelectedColor doesn't work on barsets added to
QBarSeries with insert method
* [QTBUG-134519](https://bugreports.qt.io/browse/QTBUG-134519) tst_QBarSeries::mousehovered() is flaky on Ubuntu 24.04
X11(GNOME)

### qtvirtualkeyboard
* [QTBUG-133400](https://bugreports.qt.io/browse/QTBUG-133400) Mouse/Touch hover propagates to item under VKB
* [QTBUG-136695](https://bugreports.qt.io/browse/QTBUG-136695) VKB: Entering English characters followed by Digits
automatically converts to chinese
* [QTBUG-134582](https://bugreports.qt.io/browse/QTBUG-134582) Languages dropdown appears blank when scrolling in Qt
Keyboard
* [QTBUG-137434](https://bugreports.qt.io/browse/QTBUG-137434) Inconsistent Keyboard Layout Country List Display
* [QTBUG-131374](https://bugreports.qt.io/browse/QTBUG-131374) The wordCandidateList field is not visible on the
virtual keyboard in a widget application.
* [QTBUG-123415](https://bugreports.qt.io/browse/QTBUG-123415) [Qt Virtual Keyboard] Example produces lots of warnings
at startup

### qtscxml
* [QTBUG-135396](https://bugreports.qt.io/browse/QTBUG-135396) Errors point to initial scxml file instead of the
invoked where it happens

### qtspeech
* [QTBUG-135969](https://bugreports.qt.io/browse/QTBUG-135969) Top flaky test: tst_QTextToSpeech::synthesize
* [QTBUG-128818](https://bugreports.qt.io/browse/QTBUG-128818) QTextToSpeech with flite crashes saying ©
* [QTBUG-137735](https://bugreports.qt.io/browse/QTBUG-137735) Failing tests on tqtc/lts-6.8: tst_QTextToSpeech
* [QTBUG-138064](https://bugreports.qt.io/browse/QTBUG-138064) [flite] tst_QTextToSpeech fails on ubuntu/arm
* [QTBUG-137855](https://bugreports.qt.io/browse/QTBUG-137855) QTextToSpeech: flite - sayingWord signals emitted
delayed
* [QTBUG-137947](https://bugreports.qt.io/browse/QTBUG-137947) [flite] QTextToSpeech::pause(BoundaryHint::Word) not
implemented
* [QTBUG-138010](https://bugreports.qt.io/browse/QTBUG-138010) layout / palette glitches with quickspeech example

### qtnetworkauth
* [QTBUG-135257](https://bugreports.qt.io/browse/QTBUG-135257) NetworkAuth Coverity findings

### qtremoteobjects
* [QTBUG-131016](https://bugreports.qt.io/browse/QTBUG-131016) Unexpected warning generated by repc
* [QTBUG-130972](https://bugreports.qt.io/browse/QTBUG-130972) repc is not deterministic
* [QTBUG-139754](https://bugreports.qt.io/browse/QTBUG-139754) FAIL!  : tst_clientSSL::testRun()
'socketClient->waitForEncrypted(-1)' returned FALSE

### qtquicktimeline
* [QTBUG-132502](https://bugreports.qt.io/browse/QTBUG-132502) No way to switch to timeline editor
* [QTBUG-133543](https://bugreports.qt.io/browse/QTBUG-133543) An invalid keyframe file can make the application crash.

### qtquick3d
* [QTBUG-136240](https://bugreports.qt.io/browse/QTBUG-136240) RuntimeLoader example fails on QNX
* [QTBUG-136754](https://bugreports.qt.io/browse/QTBUG-136754) startTime doesn't work without affectors
* [QTBUG-137182](https://bugreports.qt.io/browse/QTBUG-137182) Wrong shading rendered for 3D models imported by
RuntimeLoader
* [QTBUG-136334](https://bugreports.qt.io/browse/QTBUG-136334) The documentation of qt6_add_lightprobe_images is
missing

### qt5compat
* [QTBUG-136146](https://bugreports.qt.io/browse/QTBUG-136146) Qt 5 Core Compatibility: Add alt texts

### qtmqtt
* [QTBUG-135653](https://bugreports.qt.io/browse/QTBUG-135653) MessageReceived not fired when subscribing again to just
unsubscribed topic
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtopcua
* [QTBUG-134674](https://bugreports.qt.io/browse/QTBUG-134674) opcua/waterpump/simulationserver example does not build
with Boot to Qt
* [QTBUG-109096](https://bugreports.qt.io/browse/QTBUG-109096) Installed version of OPC UA example cannot compile
because it relies on the presence of Qt source code
* [QTBUG-134944](https://bugreports.qt.io/browse/QTBUG-134944) Issue with Alarm Acknowledgement - BadNodeIdUnknown with
ByteString NodeId
* [QTBUG-135674](https://bugreports.qt.io/browse/QTBUG-135674) SimpleAttributeOperand for condtionId generated with
BrowsePath of arraySize -1
* [QTBUG-135130](https://bugreports.qt.io/browse/QTBUG-135130) [qtopcua] Cannot build manual tests

### qthttpserver
* [QTBUG-137330](https://bugreports.qt.io/browse/QTBUG-137330) QtHttpServer: Writing from Sequential QIODevices to
HTTP(S)/1.1 Hangs the Client

### qtgrpc
* [QTBUG-134266](https://bugreports.qt.io/browse/QTBUG-134266) grpc chat example doesn't install all libraries
* [QTBUG-134439](https://bugreports.qt.io/browse/QTBUG-134439) qprotobufpropertyordering.cpp:313:47: error: comparison
of integers of different signs with x86 and armeabi-v7a developer builds
for Android
* [QTBUG-134885](https://bugreports.qt.io/browse/QTBUG-134885) Fail to build with protobuf-30
* [QTBUG-137109](https://bugreports.qt.io/browse/QTBUG-137109) Enabling tests for Qt 6.8.3 fails at the configure phase
for protobuf automoc.
* [QTBUG-137313](https://bugreports.qt.io/browse/QTBUG-137313) Build fails if using QML and GENERATE_PACKAGE_SUBFOLDERS
in qt_add_grpc
* [QTBUG-130113](https://bugreports.qt.io/browse/QTBUG-130113) build time paths used in
Qt6ProtobufWellKnownTypesTargets.cmake
* [QTBUG-134273](https://bugreports.qt.io/browse/QTBUG-134273) QtGrpc: Abstract namespaces are not working with
QLocalSocket

### qtgraphs
* [QTBUG-134002](https://bugreports.qt.io/browse/QTBUG-134002) QBarCategoryAxis::setCategories only works once.
* [QTBUG-134641](https://bugreports.qt.io/browse/QTBUG-134641) the Custom3DItem is still in Scatter3D after it is
deleted by removeCustomItem
* [QTBUG-135402](https://bugreports.qt.io/browse/QTBUG-135402) Q3DScene is exported twice in plugins.qmltypes
* [QTBUG-136631](https://bugreports.qt.io/browse/QTBUG-136631) Surface Graph has draws extra unused triangles
* [QTBUG-136950](https://bugreports.qt.io/browse/QTBUG-136950) tst_qmlbarscatter trying to use non-existent property
* [QTBUG-135691](https://bugreports.qt.io/browse/QTBUG-135691) Wasm build fails when linking both QtCharts and QtGraphs

### qtapplicationmanager (Commercial only)
* [QTBUG-134539](https://bugreports.qt.io/browse/QTBUG-134539) Failed to verify signature (no chain of trust)
* [QTBUG-136234](https://bugreports.qt.io/browse/QTBUG-136234) FAIL!  :
qml::ApplicationManager::test_applicationInterface() 'function returned
false' returned FALSE. ()
* [QTBUG-137056](https://bugreports.qt.io/browse/QTBUG-137056) Qt Application Manager - WindowObject Resizing Issue (Qt
6.8.3+)
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-135860](https://bugreports.qt.io/browse/QTBUG-135860) qt_add_qml_module(): Reject invalid inputs
* [QTBUG-136961](https://bugreports.qt.io/browse/QTBUG-136961) qtapplicationmanager: bubblewrap-example may need
bubblewarp

### qtinterfaceframework (Commercial only)
* [QTBUG-134742](https://bugreports.qt.io/browse/QTBUG-134742) The documentation and the snippet seem to be
contradicting
* [QTBUG-131579](https://bugreports.qt.io/browse/QTBUG-131579) [REG 6.8.0->6.8.1] building interfaceframework/remote
has FAILED and SUCCESFULL statements in output
* [QTBUG-134684](https://bugreports.qt.io/browse/QTBUG-134684) A crash occurred in C:\Users\qt\work\qt\qtinterfaceframe
work_standalone_tests\tests\auto\core\qifabstractfeature\tst_qifabstract
feature.exe.
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

Known Issues
------------

* Check that your system meets Qt's requirements:
https://doc.qt.io/qt-6.8/supported-platforms.html
* RTA reported issues from Qt 6.8
https://bugreports.qt.io/issues/?filter=26458
* See Qt 6.8 known issues from:
https://wiki.qt.io/Qt_6.8_Known_Issues
* Qt 6.8.4 Open issues in Jira:
https://bugreports.qt.io/issues/?filter=27463

Credits for the release goes to:
---------------------------------

Eirik Aavitsland  
Laszlo Agocs  
Dmitrii Akshintsev  
Konsta Alajärvi  
Anu Aliyas  
Even Oscar Andersen  
Dimitrios Apostolou  
Soheil Armin  
YAMAMOTO Atsushi  
Mate Barany  
Sebastian Beckmann  
Vladimir Belyavsky  
Nicholas Bennett  
Eric Beuque  
Kizito Birabwa  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
David Boddie  
Joerg Bornemann  
Assam Boudjelthia  
Aurélien Brooke  
Kai Uwe Broulik  
Michael Brüning  
Oswald Buddenhagen  
Olivier De Cannière  
Alexei Cazacov  
Kaloyan Chehlarski  
Albert Astals Cid  
Alexandru Croitor  
Mitch Curtis  
Thibaut Cuvelier  
Giuseppe D'Angelo  
Szabolcs David  
Pavel Dubsky  
Paul Dubsky  
Artem Dyomin  
Alexey Edelev  
David Edmundson  
Oliver Eftevaag  
Christian Ehrlicher  
Hatem ElKharashy  
Andreas Eliasson  
David Faure  
Ilya Fedin  
Nicolas Fella  
Samuel Gaist  
Zoltan Gera  
Robert Griebl  
Johannes Grunenberg  
Richard Moe Gustavsen  
Lucie Gérard  
Mikko Hallamaa  
Jøger Hansegård  
Inkamari Harjula  
Jani Heikkinen  
Miikka Heikkinen  
Moss Heim  
Jari Helaakoski  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Dominik Holland  
Zhang Hongyuan  
Samuli Hölttä  
Morteza Jamshidi  
Allan Sandfeld Jensen  
Tim Jenßen  
Jonas Karlsson  
Ali Kianian  
Marius Kittler  
Friedemann Kleint  
Michal Klocek  
Jarek Kobus  
Sze Howe Koh  
Jarkko Koivikko  
Niko Korkala  
Tomi Korpipaa  
Jani Korteniemi  
Fabian Kosmale  
Mike Krus  
Santhosh Kumar  
Kai Köhne  
Cristian Le  
Inho Lee  
Frédéric Lefebvre  
Paul Lemire  
Robert Löhning  
Thiago Macieira  
Christophe Marin  
Leena Miettinen  
Shveta Mittal  
Thomas Moerschell  
Safiyyah Moosa  
Bartlomiej Moskal  
Marc Mutz  
Antti Määttä  
Andy Nichols  
Mårten Nordheim  
Daniel Nylander  
Dennis Oberst  
Kwanghyo Park  
Jerome Pasion  
Mikhail Paulyshka  
Miika Pernu  
Mauro Persano  
Samuli Piippo  
Karim Pinter  
Timur Pocheptsov  
Lauri Pohjanheimo  
Joni Poikelin  
Rami Potinkara  
Lorn Potter  
Sakaria Pouke  
Dheerendra Purohit  
MohammadHossein Qanbari  
Liang Qi  
Matthias Rauter  
Topi Reinio  
David Rosca  
Shawn Rutledge  
Otto Ryynänen  
Toni Saario  
Ahmad Samir  
Lars Schmertmann  
Michal Seben  
Luca Di Sera  
Sami Shalayel  
Raman Shamotsin  
Tian Shilin  
Kristoffer Skau  
Nils Petter Skålerud  
Nils Peter Skålerud  
Nils Petter Skålerud  
Ivan Solovev  
Axel Spoerl  
Alexander Stippich  
Magdalena Stojek  
Christian Strømme  
Tarja Sundqvist  
Lars Sutterud  
Jan Arve Sæther  
Morten Sørvig  
Vladislav Tarakanov  
Nodir Temirkhodjaev  
Aleksandr Timofeev  
Paul Olav Tvete  
Esa Törmänen  
Tuomas Vaarala  
Johanna Vanhatapio  
Sami Varanka  
Peter Varga  
Doris Verria  
Tor Arne Vestbø  
Petri Virkkunen  
Juha Vuolle  
Olli Vuolteenaho  
Jannis Völker  
Michael Weghorn  
Bernd Weimer  
Edward Welbourne  
Paul Wicking  
Piotr Wiercinski  
Oliver Wolff  
Semih Yavuz  
Marianne Yrjänä  
