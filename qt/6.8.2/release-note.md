Release note
============
Qt 6.8.2 release is a patch release made on the top of Qt 6.8.1.
As a patch release, Qt 6.8.2 does not add any new functionality but provides
bug fixes and other improvements and maintains both forward and backward
compatibility (source and binary) with Qt 6.8.1.

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
* CVE-2025-23050 in qtconnectivity

### qtbase
* 214101b1b36 Remove assert in QImageTextureGlyphCache::fillTexture()
Fixed possible assert when transforming bitmap fonts.

* 83a749c4f94 Upgrade to Harfbuzz 10.1.0
Upgraded Harfbuzz to version 10.1.0.

* e2ba5d90538 CMake: Add PURL and CPE info to 3rd party attribution
files
Added PURL and CPE information to the attribution files of 3rd party
sources.

* c73cc95ba72 Don't count overflowing inline image height to previous
line
Fixed an issue which could cause the height of a word-wrapped text line
to grow if the immediate line after it began with an inline image.

* 1ff68ff3fd0 QCupsPrintEngine::setProperty(): defend against malformed
PPK_CupsOptions values
Fixed a bug where setting a value string-list with an odd number of
elements as the PPK_CupsOptions value would read uninitialized data.

* 992f81931e1 Windows: Fix arbitrary outline on emojis
Fixed an issue where emojis would sometimes get an outline.

* 69da5314ff9 SQLite: Update SQLite to v3.47.1
Updated SQLite to v3.47.1

* 06f77ab19cf Correct handling of World in mapping MS's zone IDs to IANA
ones
Corrected handling of QLocale::World and clarified in docs how
QLocale::AnyTerritory is handled when QTimeZone selects zones by
territory.

* 948599e7b71 QDomDocument::toByteArray() crashed in case of high XML
nesting level
QDomDocument::toByteArray() now iterates the nodes of the document
instead of recursing into subnodes. This avoids a stack-overflow crash
that used to arise with deeply-nested document structures.

* 4941c0232e6 SQLite: Update SQLite to v3.47.2
Updated SQLite to v3.47.2

* e11edced7eb QStringView: fix construction from arrays of unknown size
Made construction from arrays of unknown size compile. Such arrays will
use the const Char* constructor, determining the size of the array at
runtime.

* f9b65770a1a qstringfwd.h: don't include qglobal.h
The qstringfwd.h header no longer includes qglobal.h. A backwards-
compatible fix is to include qglobal.h yourself instead of relying on
the transitive include.

* fb91b0d3077 Q{Any,Utf8}StringView: fix construction from arrays of
unknown size
Made construction from arrays of unknown size compile. Such arrays will
use the const Char* constructor, determining the size of the array at
runtime.

* d5544a6d0d0 Update bundled libjpeg-turbo to version 3.1.0
libjpeg-turbo was updated to version 3.1.0

* d490a1ac09a QCommandLineParser: include the positional arguments'
sizes in --help
Made it so the positional argument descriptions are taken into account
in the aligning of text for helpText().

* 7e2b84b8be5 Apple: Use automatic rendering mode for icon engine
The Apple icon engine, used for theme icons on macOS and iOS, will now
use the default rendering mode for icons, typically monochrome, instead
of always using hierarchical icons.

* f3fc37146d7 QSaveFile: make it so flush() errors imply commit() failed
Fixed a bug that caused commit() to return true and overwrite its
intended target file even though it failed to flush buffered data to the
storage, which could cause data loss. This issue can be worked around by
calling flush() first and only calling commit() if that returns success.

* bb81ac778fd 3rdparty: patch BLAKE2 sources to not export anything in
static builds
Fixed a bug that caused the BLAKE2 symbols to be visible from QtCore in
a static build. If you need to use the BLAKE2 hashing algorithm in your
own code, either use QCryptographicHash or import libb2 into your build
environment. Using libb2 remains the recommended solution for all
systems, especially those for which it has optimized (vectorized)
implementations.

* 76a7e0e7934 Remove QT_NO_CAST_FROM_ASCII from
QT_ENABLE_STRICT_MODE_UP_TO
No longer includes QT_NO_CAST_FROM_ASCII. If you wish to continue using
QT_NO_CAST_FROM_ASCII, you need to define it in addition to
QT_ENABLE_STRICT_MODE_UP_TO. The reason for this change is that, while
everything else in strict mode should eventually become the default,
we're not proposing to remove the ability to construct a QString from a
const char*. QT_NO_CAST_FROM_BYTEARRAY and QT_NO_CAST_TO_ASCII remain
enabled in strict mode, though.

* 5fbe185931f Update CLDR to v46
Updated CLDR data, used by QLocale, to v46.

* 29a1c571839 Implement COLRv0 support in Freetype engine
Added support for COLRv0 format color fonts.

* 92b47c27432 Update bundled libpng to version 1.6.45
libpng was updated to version 1.6.45

* df99f590d1f SQLite: Update SQLite to v3.48.0
Updated SQLite to v3.48.0

* 7affce87527 Update Harfbuzz to version 10.2.0
Upgraded Harfbuzz to version 10.2.0.

### qtdeclarative
* 1c4c537307 qmlls: fix compatibility issue due to removal of "p" flag
qmlls tool can take both -p and -d flag to pass documentation path.

### qtmultimedia
* 7f33056a9 GStreamer - implement custom gstreamer bin
QMediaPlayer: GStreamer - support custom pipeline as source

* 82ed74a66 Deprecate QMediaRecorder::encoderSettingsChanged() signal
from Qt 6.9
Deprecate QMediaRecorder::encoderSettingsChanged() because more
specific signals should be used instead.

* 74c9cc5c8 Add REUSE.toml files and missing licenses
Add path to license files within LicenseFiles field.
qtattributionscanner looks for the files associated with licenses listed
in the licenseId fiel within the LICENSES directory. To prevent reuse
from erroring out, the license files only mentioned in
qt_attribution.json need to be moved out of the LICENSES directory. For
the qtattributionscanner to find those files, they need to be listed in
LicenseFiles field.

* 95d5ff248 QAudioDevice: Make comparison only rely on id and mode
Comparison of QAudioDevice now only relies on .id() and .mode()
properties

* edf79016c Update pffft version to the latest version from upstream
Updated pffft to 02fe771.

### qttools
* 60a51628f QDoc: Stop passing $CLANG_RESOURCE_DIR to Clang
QDoc no longer passes the contents of the `CLANG_RESOURCE_DIR`
environment variable as an include path when interfacing with Clang.

* 1ef9d25dd qdoc: QML Visitor: Handle namespaced imports
QDoc now resolves the correct QML base type imported under a namespace
ID.

### qt3d
* 953da993d QRay3D: fix transform
Fix QRay3D::transform

### qtimageformats
* 9b5329c Update bundled libwebp to version 1.5.0
Update bundled libwebp to version 1.5.0

### qtserialport
* 989a676 Linux: add an option to skip udev when enumerating serial
ports
Added the possibility to skip the libudev lookup by setting the
QT_SERIALPORT_SKIP_UDEV_LOOKUP environment variable. In such case, the
information from /sys/class/tty is used to enumerate the available
ports.

* faf12a1 Windows: fix readyRead() signal emission
Fixed a bug where the readyRead() signal did not follow the QIODevice
docs and could be emitted recursively.

### qtnetworkauth
* 4609c26 Fix and improve token request error reporting
Make a better distinction between NetworkErrors and ServerErrors with
token requests.

* b67d48d Improve callback/redirect_uri hostname setting
Changed and clarified callback hostname handling (especially localhost
vs. 127.0.0.1)

* 27ddc09 Change QAbstractOAuth2::expirationAt also when invalidated
Change expirationAt also if expires_in wasn't provided, or has invalid
value, and becomes invalid.

### qtquick3d
* 18ae9981d Add paths to the sub-project attributions for openxr
Added more specific paths to the sub-projects included with openxr.

### qt5compat
* 27c6b75 QStringRef: fix lost null-ness when converting to QStringView
Fixed a Qt 6 regression where conversion to QStringView would no longer
preserve nullness.

* fe34d2f QStringRef: preserve null-ness when converting to
QAnyStringView
Fixed missing conversion to QAnyStringView.

### qtgrpc
* 0a642f49 Avoid generating QList aliases for the protobuf messages
qtprotobufgen doesn't generate protobuf message QList aliases. All
usages of aliases should be replace by respective QList types. Aliases
are still generated and are guarded by the QT_USE_PROTOBUF_LIST_ALIASES
macro in the generated code. The macro is enabled by default and can be
disabled using QT_USE_PROTOBUF_LIST_ALIASES target property.


Fixes
-----

### qtbase
* [QTBUG-111796](https://bugreports.qt.io/browse/QTBUG-111796) Qt Font Scaling for bitmap fonts is broken in Wayland
* [QTBUG-130930](https://bugreports.qt.io/browse/QTBUG-130930) Freetype: Assert when rotating drawing bitmap font with
rotated painter
* [QTBUG-131009](https://bugreports.qt.io/browse/QTBUG-131009) FAIL!  : tst_focus::navigation(tab-all-controls)
Received a warning that resulted in a failure
* [QTBUG-130973](https://bugreports.qt.io/browse/QTBUG-130973) [iOS] Native image picker dialog freezes when asking for
permission
* [QTBUG-131001](https://bugreports.qt.io/browse/QTBUG-131001) QWidget::childAt returns empty children
* [QTBUG-129684](https://bugreports.qt.io/browse/QTBUG-129684) Potential crash when calling QInputDialogue::getText()
* [QTBUG-131093](https://bugreports.qt.io/browse/QTBUG-131093) [REG 6.5.3 - 6.7.3] [macOS] Global scale factor has no
effect on platform's window size anymore
* [QTBUG-130832](https://bugreports.qt.io/browse/QTBUG-130832) [REG 6.8.0 -> dev] Windows System Tray Icon: Context
menu's incorrect position
* [QTBUG-126698](https://bugreports.qt.io/browse/QTBUG-126698) [REG 5->6] QDateEdit defaults to 20th century
* [QTBUG-129108](https://bugreports.qt.io/browse/QTBUG-129108) Menus and action visibility
* [QTBUG-130811](https://bugreports.qt.io/browse/QTBUG-130811) XCB: Async operations between XCB and X11 cause
flakiness in QXcbScreen::topLevelAt()
* [QTBUG-84258](https://bugreports.qt.io/browse/QTBUG-84258) tst_Gestures::graphicsItemGesture fails
* [QTBUG-69648](https://bugreports.qt.io/browse/QTBUG-69648) tst_Gestures::graphicsItemTreeGesture fails on Ubuntu
18.04.
* [QTBUG-67393](https://bugreports.qt.io/browse/QTBUG-67393) tst_Gestures::explicitGraphicsObjectTarget fails on
Ubuntu 17.10.
* [QTBUG-67392](https://bugreports.qt.io/browse/QTBUG-67392) tst_Gestures::graphicsItemTreeGesture fails on Ubuntu
17.10.
* [QTBUG-67389](https://bugreports.qt.io/browse/QTBUG-67389) tst_Gestures::graphicsView fails on Ubuntu 17.10.
* [QTBUG-68861](https://bugreports.qt.io/browse/QTBUG-68861) tst_Gestures::graphicsItemGesture autotest fails on
Ubuntu 18.04
* [QTBUG-70224](https://bugreports.qt.io/browse/QTBUG-70224) tst_Gestures::testReuseCanceledGestures autotest fails on
Ubuntu 18.04 & SLES 15
* [QTBUG-70223](https://bugreports.qt.io/browse/QTBUG-70223) tst_Gestures::partialGesturePropagation autotest fails on
Ubuntu 18.04 & SLES 15
* [QTBUG-67395](https://bugreports.qt.io/browse/QTBUG-67395) tst_Gestures::autoCancelGestures2 fails on Ubuntu 17.10
* [QTBUG-70227](https://bugreports.qt.io/browse/QTBUG-70227) tst_Gestures::panelStacksBehindParent autotest fails on
Ubuntu 18.04
* [QTBUG-70226](https://bugreports.qt.io/browse/QTBUG-70226) tst_Gestures::panelPropagation autotest fails on Ubuntu
18.04
* [QTBUG-70209](https://bugreports.qt.io/browse/QTBUG-70209) tst_Gestures::graphicsViewParentPropagation autotest
fails on Ubuntu 18.04
* [QTBUG-70153](https://bugreports.qt.io/browse/QTBUG-70153) tst_Gestures::autoCancelGestures2 autotest fails on
Ubuntu 18.04
* [QTBUG-45048](https://bugreports.qt.io/browse/QTBUG-45048) 2 QProgressBar's have differing behaviour, if one has
setTextVisible(true)
* [QTBUG-130895](https://bugreports.qt.io/browse/QTBUG-130895) Living QThread after termination
* [QTBUG-129927](https://bugreports.qt.io/browse/QTBUG-129927) [REG: 6.7 -> 6.8] Use after free in QTimeZone
* [QTBUG-129846](https://bugreports.qt.io/browse/QTBUG-129846) Quit in GUI application on linux in qt 6.8.0 does not
quit and process runs indefinitely
* [QTBUG-130341](https://bugreports.qt.io/browse/QTBUG-130341) Crash during QNetworkAccessManager destruction
* [QTBUG-117996](https://bugreports.qt.io/browse/QTBUG-117996) [REG 6.2 -> 6.5] QBasicTimer::stop: Failed. Possibly
trying to stop from a different thread
* [QTBUG-130980](https://bugreports.qt.io/browse/QTBUG-130980) There is a bug with line spacing when QLabel displays
rich text.
* [QTBUG-131108](https://bugreports.qt.io/browse/QTBUG-131108) tst_QFont::italicOblique CI test fails on Android 15
* [QTBUG-131262](https://bugreports.qt.io/browse/QTBUG-131262) Freetype: Variable font named instances with slant not
detected as oblique
* [QTBUG-18068](https://bugreports.qt.io/browse/QTBUG-18068) When a corner widget in a QTabWidget is hidden then the
space is not reclaimed for the tabs
* [QTBUG-130552](https://bugreports.qt.io/browse/QTBUG-130552) QNetworkConnectionMonitorPrivate::updateState crash
* [QTBUG-130799](https://bugreports.qt.io/browse/QTBUG-130799) Remove or fix Q_OBJECT qdoc macro
* [QTBUG-129576](https://bugreports.qt.io/browse/QTBUG-129576) [Boot2Qt] Running "QQuickRenderControl RHI Example" app
with OpenGL graphic api causes the view to become black
* [QTBUG-130887](https://bugreports.qt.io/browse/QTBUG-130887) compose handling is broken
* [QTBUG-130673](https://bugreports.qt.io/browse/QTBUG-130673) Windows11 Style : title bar doesn't highlight for active
mdisubwindow
* [QTBUG-130000](https://bugreports.qt.io/browse/QTBUG-130000) Keyboard does not get focus on Android TV
* [QTBUG-130371](https://bugreports.qt.io/browse/QTBUG-130371) Keyboard navigation focus in WebAssembly is half broken
* [QTBUG-131587](https://bugreports.qt.io/browse/QTBUG-131587) Flaky emoji rendering on Windows
* [QTBUG-131446](https://bugreports.qt.io/browse/QTBUG-131446) QMetaProperty documentation references deprecated
"type()" function
* [QTBUG-131487](https://bugreports.qt.io/browse/QTBUG-131487) QFileSystemModel does not work with QML DelegateModel
* [QTBUG-122609](https://bugreports.qt.io/browse/QTBUG-122609) moc takes 'constexpr' as function return type
* [QTBUG-129439](https://bugreports.qt.io/browse/QTBUG-129439) QToolBar incorrect display on Windows 11
* [QTBUG-129700](https://bugreports.qt.io/browse/QTBUG-129700) Windows 11 modern style | Toolbar buttons state not
legible
* [QTBUG-130822](https://bugreports.qt.io/browse/QTBUG-130822) Windows 11 style does not render ON status of toggle
button in toolbar
* [QTBUG-131664](https://bugreports.qt.io/browse/QTBUG-131664) QApplication in inPopupMode bug popupWindow is not a
widget window will cause a coredump
* [QTBUG-131491](https://bugreports.qt.io/browse/QTBUG-131491) QDateTime comparision is slow even the same timezone is
set
* [QTBUG-131782](https://bugreports.qt.io/browse/QTBUG-131782) [REG 6.8.0 -> 6.8.1] Cannot configure qtbase if
directory contains "++"
* [QTBUG-130557](https://bugreports.qt.io/browse/QTBUG-130557) SBOM has references to build time paths
* [QTBUG-131474](https://bugreports.qt.io/browse/QTBUG-131474) QNetworkRequest::setRawHeader puts header name in
lowercase
* [QTBUG-116042](https://bugreports.qt.io/browse/QTBUG-116042) configure fails when BUILDDIR path contains "++"
* [QTBUG-131799](https://bugreports.qt.io/browse/QTBUG-131799) SQL drivers cannot be configured due to an SBOM error.
* [QTBUG-131801](https://bugreports.qt.io/browse/QTBUG-131801) QHttpNetworkRequestPrivate copy constructor does not
copy fullLocalServerName
* [QTBUG-131731](https://bugreports.qt.io/browse/QTBUG-131731) REG: Possible crash on macOS when disabling emoji
parsing
* [QTBUG-131505](https://bugreports.qt.io/browse/QTBUG-131505) Unable to create multisampled depth-only pipeline
* [QTBUG-131741](https://bugreports.qt.io/browse/QTBUG-131741) [Reg 6.5.7 -> 6.8.0][iOS] QDesktopServices URL Handler
(custom scheme) no longer receives data from external apps
* [QTBUG-129722](https://bugreports.qt.io/browse/QTBUG-129722) [asan] use-after-free in pulseaudio logger
* [QTBUG-130630](https://bugreports.qt.io/browse/QTBUG-130630) AddressSanitizer: heap-use-after-free on
tst_qopcuaclient
* [QTBUG-131338](https://bugreports.qt.io/browse/QTBUG-131338) qtbase tst_android testFullScreenDimensions is flaky
* [QTBUG-131880](https://bugreports.qt.io/browse/QTBUG-131880) [macOS] Crash on [NSSavePanel
didEndPanelWithReturnCode:]
* [QTBUG-110898](https://bugreports.qt.io/browse/QTBUG-110898) Window disappears when monitor is disconnected
* [QTBUG-130714](https://bugreports.qt.io/browse/QTBUG-130714) Qt applications crash when dragging to a different X11
Screen
* [QTBUG-131883](https://bugreports.qt.io/browse/QTBUG-131883) SBOM prevent installing modules in different directory
* [QTBUG-131151](https://bugreports.qt.io/browse/QTBUG-131151) QDomDocument::toByteArray() crashes when parsing svg
file.
* [QTBUG-131950](https://bugreports.qt.io/browse/QTBUG-131950) Creator help mode: footer for main index.html is in
middle of page
* [QTBUG-129178](https://bugreports.qt.io/browse/QTBUG-129178) Broken layout on landing page (offline style)
* [QTBUG-131976](https://bugreports.qt.io/browse/QTBUG-131976) The alternateBase color in dark W11 style is wrong
* [QTBUG-131913](https://bugreports.qt.io/browse/QTBUG-131913) Incorrect QTimeZone documentation
* [QTBUG-131761](https://bugreports.qt.io/browse/QTBUG-131761) Incorrect display of :selected state of QCombobox on
"windows" style plugin
* [QTBUG-73390](https://bugreports.qt.io/browse/QTBUG-73390) QMenu Action is not triggered by numeric mnemonic entered
on keypad
* [QTBUG-132053](https://bugreports.qt.io/browse/QTBUG-132053) FTBFS: Compilation of qsharedmemory_p.h fails with
sysv_sem disabled
* [QTBUG-132150](https://bugreports.qt.io/browse/QTBUG-132150) androiddeployqt does not strip quotation marks from
static namespace string retrieved from build.gradle
* [QTBUG-127522](https://bugreports.qt.io/browse/QTBUG-127522) QBENCHMARK result does not output global data tag
* [QTBUG-45949](https://bugreports.qt.io/browse/QTBUG-45949) QToolBar icon-size can not be styled as documented
* [QTBUG-112746](https://bugreports.qt.io/browse/QTBUG-112746) QAnyStringView missing implicit conversion from char[]
with unknown size
* [QTBUG-122797](https://bugreports.qt.io/browse/QTBUG-122797) QStringRef doesn't convert to QAnyStringView
* [QTBUG-122798](https://bugreports.qt.io/browse/QTBUG-122798) [REG 5.15 -> 6.7 (or earlier)] QStringRef -> QStringView
conversion loses null-ness
* [QTBUG-132256](https://bugreports.qt.io/browse/QTBUG-132256) Drag and drop not working
* [QTBUG-132091](https://bugreports.qt.io/browse/QTBUG-132091) macOS: Key modifiers aren't ignored when dragging
'within the application'
* [QTBUG-131707](https://bugreports.qt.io/browse/QTBUG-131707) Multi-ABI Android builds only work on base kit arch
* [QTBUG-131685](https://bugreports.qt.io/browse/QTBUG-131685) QDoubleSpinBox: Style sheet Property Selector doesn't
reset font back to original style
* [QTBUG-130275](https://bugreports.qt.io/browse/QTBUG-130275) Segmentation Fault when using InsertWidget with too-
large index
* [QTBUG-130992](https://bugreports.qt.io/browse/QTBUG-130992) Crash when rendering radialGradient
* [QTBUG-131716](https://bugreports.qt.io/browse/QTBUG-131716) QCommandLineParser::helpText fails if no options are
added
* [QTBUG-132101](https://bugreports.qt.io/browse/QTBUG-132101) Extra semicolon warnings in qdirlisting.h, qaccessible.h
and qkeysequence.h
* [QTBUG-132115](https://bugreports.qt.io/browse/QTBUG-132115) QDateTimeParser::parse assertion triggered in case of
invalid date
* [QTBUG-112346](https://bugreports.qt.io/browse/QTBUG-112346) qmllint fails when WebView is used
* [QTBUG-132075](https://bugreports.qt.io/browse/QTBUG-132075) tst_qquicktext::multilengthStrings(Wrap) Compared
doubles are not the same (fuzzy compare)
* [QTBUG-131586](https://bugreports.qt.io/browse/QTBUG-131586)  QLineEdit's bottom edge is the wrong color when in Dark
mode.
* [QTBUG-132332](https://bugreports.qt.io/browse/QTBUG-132332) QSaveFile will empty file if no space left on device
* [QTBUG-132347](https://bugreports.qt.io/browse/QTBUG-132347) blake2b symbols exported in static builds
* [QTBUG-132431](https://bugreports.qt.io/browse/QTBUG-132431) Stylesheet Margin/Padding squashes QSpinBox
* [QTBUG-130642](https://bugreports.qt.io/browse/QTBUG-130642) Incorrect QAbstractSpinBox size hint in Windows 11 style
when style sheet is set
* [QTBUG-131959](https://bugreports.qt.io/browse/QTBUG-131959) Build failure on QtFuture::whenAll(QFuture<void>,
QFuture<void>)
* [QTBUG-21329](https://bugreports.qt.io/browse/QTBUG-21329) QTransform::quadToQuad() doesn't work, when passed
QRectFs
* [QTBUG-132340](https://bugreports.qt.io/browse/QTBUG-132340) QmlTools not automatically found
* [QTBUG-132258](https://bugreports.qt.io/browse/QTBUG-132258) _qt_internal_create_command_script fails on windows if
spaces present
* [QTBUG-132085](https://bugreports.qt.io/browse/QTBUG-132085) [REG 6.7 -> 6.8][Android] Stuck in SplashScreen on
Restart
* [QTBUG-130766](https://bugreports.qt.io/browse/QTBUG-130766) QtConcurrent::blockingMapped has incorrect argument
deduction for generic lambdas
* [QTBUG-132188](https://bugreports.qt.io/browse/QTBUG-132188) Could not find external SBOM document
* [QTBUG-132581](https://bugreports.qt.io/browse/QTBUG-132581) QMake triggers abnormally many "zero as null pointer
constant" warnings on macOS
* [QTBUG-123843](https://bugreports.qt.io/browse/QTBUG-123843) Swipping with three finger between apps may cause a
crash after interacting with a text input field
* [QTBUG-132059](https://bugreports.qt.io/browse/QTBUG-132059) Crash when quickly invoking subsequent scrollAction
* [QTBUG-132670](https://bugreports.qt.io/browse/QTBUG-132670) QTreeView does not always refresh on dataChanged
* [QTBUG-124173](https://bugreports.qt.io/browse/QTBUG-124173) QTreeView / QTableView dataChanged very slow when
topLeft and bottomRight span many items
* [QTBUG-132597](https://bugreports.qt.io/browse/QTBUG-132597) Incorrect description of QTemporaryFile behavior when
two placeholders are present
* [QTBUG-132410](https://bugreports.qt.io/browse/QTBUG-132410) Q_JNI_NATIVE_METHOD floating point argument corruption
on x86_64
* [QTBUG-132277](https://bugreports.qt.io/browse/QTBUG-132277) Qt fails to adhere to HTTP/2 HPACK dynamic table size
changes
* [QTBUG-132381](https://bugreports.qt.io/browse/QTBUG-132381) [REG 6.8 -> 6.9] Crash when QGuiApplication is static
* [QTBUG-132697](https://bugreports.qt.io/browse/QTBUG-132697) FAIL!  :
tst_QQmlDebugJS::setBreakpointInScriptThatQuits(custom)
'm_process->waitForFinished()' returned FALSE.
* [QTBUG-102984](https://bugreports.qt.io/browse/QTBUG-102984) tst_QQmlDebugJS hangs on macOS in CI
* [QTBUG-132622](https://bugreports.qt.io/browse/QTBUG-132622) Failed to find required Qt component "Protobuf"
* [QTBUG-132616](https://bugreports.qt.io/browse/QTBUG-132616) Failed to find the host tool "Qt6::qtwaylandscanner"
* [QTBUG-132698](https://bugreports.qt.io/browse/QTBUG-132698) Debug build fails at qtimezonelocale.cpp
* [QTBUG-127467](https://bugreports.qt.io/browse/QTBUG-127467) QtAbstractItemModel asserts when being rapidly modified
* [QTBUG-110878](https://bugreports.qt.io/browse/QTBUG-110878) Fullscreen windows rendered behind navigation bar
* [QTBUG-96105](https://bugreports.qt.io/browse/QTBUG-96105) When a window is switched to be FullScreen then it will
end up keeping a bar at the bottom of the window which should not be
visible
* [QTBUG-101968](https://bugreports.qt.io/browse/QTBUG-101968) Android: a widget is shown incorrectly in fullscreen
mode for the first time
* [QTBUG-127394](https://bugreports.qt.io/browse/QTBUG-127394) Window not drawn to full screen in immersive mode after
orientation change.
* [QTBUG-121820](https://bugreports.qt.io/browse/QTBUG-121820) Android: Mainwindow has black border in the bottom when
set to full screen
* [QTBUG-109878](https://bugreports.qt.io/browse/QTBUG-109878) Qt 6.4.1 - Android - White rectangle at the bottom of
the screen
* [QTBUG-119594](https://bugreports.qt.io/browse/QTBUG-119594) Android: Layout in display cut mode being overridden to
default edges always
* [QTBUG-94890](https://bugreports.qt.io/browse/QTBUG-94890) Shortcut with "Backtab" does not work for Windows
* [QTBUG-131843](https://bugreports.qt.io/browse/QTBUG-131843) File/Folder link overlay is missing, or wrong
size/position
* [QTBUG-129242](https://bugreports.qt.io/browse/QTBUG-129242) QTableWidget selection issue
* [QTBUG-131372](https://bugreports.qt.io/browse/QTBUG-131372) QStandardItem::appendRow does not update model
recursively
* [QTBUG-130909](https://bugreports.qt.io/browse/QTBUG-130909) Color Emojis don't render at all on Android 15
* [QTBUG-131116](https://bugreports.qt.io/browse/QTBUG-131116) Freetype: Support COLR format color fonts
* [QTBUG-129698](https://bugreports.qt.io/browse/QTBUG-129698) Widget doesn't show after windowHandle()->destroy()
* [QTBUG-132841](https://bugreports.qt.io/browse/QTBUG-132841) Android QtAbstractItemModel wrong JNI call for sibling()
method
* [QTBUG-121418](https://bugreports.qt.io/browse/QTBUG-121418) [Regr: 5.x -> 6.x] QTranslator loads zh instead of zh_TW
translation
* [QTBUG-87417](https://bugreports.qt.io/browse/QTBUG-87417) tst_QLineEdit fails on Android
* [QTBUG-132804](https://bugreports.qt.io/browse/QTBUG-132804) Debug build fails at qgenericunixthemes.cpp
* [QTBUG-125285](https://bugreports.qt.io/browse/QTBUG-125285) QKdeTheme falls back to Qt::ColorScheme::Unknown on
invalid desktop theme
* [QTBUG-125892](https://bugreports.qt.io/browse/QTBUG-125892) QtDS compatibility - Improve qmldir path discovery
* [QTBUG-125970](https://bugreports.qt.io/browse/QTBUG-125970) QML components with the same name under a module
* [QTBUG-125971](https://bugreports.qt.io/browse/QTBUG-125971) Java QML codegen source file handling
* [QTBUG-132875](https://bugreports.qt.io/browse/QTBUG-132875) CMYK to RGB conversion on big endian produces
significantly wrong colors
* [QTBUG-126608](https://bugreports.qt.io/browse/QTBUG-126608) QRhi pipeline cache is never written for applications
terminated forcibly without running cleanup for Quick/QWindow/QGuiApp
* [QTBUG-93625](https://bugreports.qt.io/browse/QTBUG-93625) qt_internal_add_test doesn't call qt_import_qml_plugins
* [QTBUG-128455](https://bugreports.qt.io/browse/QTBUG-128455) [VxWorks] configure doesn't recognize graphics settings
* [QTBUG-130932](https://bugreports.qt.io/browse/QTBUG-130932) Top flaky test:
tst_QAbstractItemView::testDialogAsEditor
* [QTBUG-99563](https://bugreports.qt.io/browse/QTBUG-99563) The QMutable*Event construct is Undefined Behaviour
* [QTBUG-130118](https://bugreports.qt.io/browse/QTBUG-130118) [REG: 6.7 -> 6.8] psql: querying pg_timezone_names now
gives 00:00:00 offsets
* [QTBUG-131343](https://bugreports.qt.io/browse/QTBUG-131343) Crash in QXcbScreen::setMonitor() via KDE/xembed-sni-
proxy
* [QTBUG-130884](https://bugreports.qt.io/browse/QTBUG-130884) xdg-desktop-portal should be enabled only environments
that actually supports it
* [QTBUG-94708](https://bugreports.qt.io/browse/QTBUG-94708) qCDebug() and friends could pass the category as a tag in
Android
* [QTBUG-116554](https://bugreports.qt.io/browse/QTBUG-116554) [macOS] Crash on QCocoaDrag::maybeDragMultipleItems()
* [QTBUG-131477](https://bugreports.qt.io/browse/QTBUG-131477) Review SBOM generation and documentation to include
third party components
* [QTBUG-120604](https://bugreports.qt.io/browse/QTBUG-120604) Custom sort/filter model example - The arrow on the
magnifying glass is too high
* [QTBUG-131653](https://bugreports.qt.io/browse/QTBUG-131653) Race condition between androiddeployqt runs for apk and
aab package builds
* [QTBUG-131484](https://bugreports.qt.io/browse/QTBUG-131484) Fix links to QIODeviceBase::OpenMode flags
* [QTBUG-131842](https://bugreports.qt.io/browse/QTBUG-131842) Qt's CSS parser doesn't eat unquoted URL strings with
query
* [QTBUG-128893](https://bugreports.qt.io/browse/QTBUG-128893) sbom for qtpdf gets lost , as it ends up as qtwebengine
sbom
* [QTBUG-64941](https://bugreports.qt.io/browse/QTBUG-64941) QTimeZone parses zone.tab, which is for backwards
compatibility
* [QTBUG-131906](https://bugreports.qt.io/browse/QTBUG-131906) FAIL!  :
tst_qqmlecmascript::componentCreation(invalidMode) Not all expected
messages were received
* [QTBUG-132072](https://bugreports.qt.io/browse/QTBUG-132072) QWidget::mapTo() crashed!
* [QTBUG-132114](https://bugreports.qt.io/browse/QTBUG-132114) qtbase/fe6dda9bb9310878b408b2421f60acb7135bd8ba breaks
-unity-build
* [QTBUG-132051](https://bugreports.qt.io/browse/QTBUG-132051) Converting a QImage to an opaque format does not always
reset the alpha
* [QTBUG-128914](https://bugreports.qt.io/browse/QTBUG-128914) Many examples fail to build when "Build via Junction
Points" is enabled in Qt Creator
* [QTBUG-132102](https://bugreports.qt.io/browse/QTBUG-132102) Windows: Fusion style: Combo-box list: Item with icon
and long text sometimes has elide
* [QTBUG-128900](https://bugreports.qt.io/browse/QTBUG-128900) macOS 15 deployment target build failure due to obsolete
API 'CGDisplayCreateImageForRect'
* [QTBUG-132187](https://bugreports.qt.io/browse/QTBUG-132187) QDrawUtil: qDrawPlainRoundedRect does not work well for
high-dpi screens
* [QTBUG-132244](https://bugreports.qt.io/browse/QTBUG-132244) SQLite not found in qttools when building system SQLite
in Windows
* [QTBUG-132133](https://bugreports.qt.io/browse/QTBUG-132133) QSpan<const T> causes Qt container to detach
* [QTBUG-132261](https://bugreports.qt.io/browse/QTBUG-132261) Many minor styling issues on windows 11
* [QTBUG-131887](https://bugreports.qt.io/browse/QTBUG-131887) [Boot to Qt 6.9.0 snapshot] jetson-agx-orin cannot start
qtlauncher
* [QTBUG-132507](https://bugreports.qt.io/browse/QTBUG-132507) Fix review findings in QUniqueHandle
* [QTBUG-119490](https://bugreports.qt.io/browse/QTBUG-119490) qcocoaapplicationdelegate.mm:354:20: error: cannot
initialize return object of type 'BOOL'
* [QTBUG-131377](https://bugreports.qt.io/browse/QTBUG-131377) Include Chromium in SBOM
* [QTBUG-132433](https://bugreports.qt.io/browse/QTBUG-132433) Windows 11 style - QToolButton/QPushButton quirks
* [QTBUG-132459](https://bugreports.qt.io/browse/QTBUG-132459) Windows11 style: QProgressBar needs some work
* [QTBUG-131585](https://bugreports.qt.io/browse/QTBUG-131585) The QTreeWidget is painting poorly when the frame style
is set to QFrame::Plain | QFrame::Box when using Windows 11 style.
* [QTBUG-128420](https://bugreports.qt.io/browse/QTBUG-128420) Qt 6.8 does not support build paths with white spaces
anymore
* [QTBUG-130313](https://bugreports.qt.io/browse/QTBUG-130313) Garbage text output
* [QTBUG-127777](https://bugreports.qt.io/browse/QTBUG-127777) doc deprecates both ways to open a modal dialog

### qtdeclarative
* [QTBUG-130524](https://bugreports.qt.io/browse/QTBUG-130524) Error in qmldir file of Controls.Windows.imp
* [QTBUG-127538](https://bugreports.qt.io/browse/QTBUG-127538) Crash with Imagine style
* [QTBUG-130694](https://bugreports.qt.io/browse/QTBUG-130694) qmlls: code completion doesn't respect comments
* [QTBUG-126667](https://bugreports.qt.io/browse/QTBUG-126667) tst_QQuickPopup::popupWindowPositioning is flaky
* [QTBUG-130767](https://bugreports.qt.io/browse/QTBUG-130767) Incremental QML gc deletes context property
* [QTBUG-127122](https://bugreports.qt.io/browse/QTBUG-127122) some MouseArea's signals are weirdly triggered
* [QTBUG-131263](https://bugreports.qt.io/browse/QTBUG-131263) FAIL!  : tst_qqmllanguage::retrieveQmlTypeId()
'qmlTypeId("testhelper", 1, 0, "PurelyDeclarativeSingleton") >= 0'
returned FALSE
* [QTBUG-130974](https://bugreports.qt.io/browse/QTBUG-130974) A regular expression pattern gives unexpected results in
QML and QJSEngine.
* [QTBUG-34881](https://bugreports.qt.io/browse/QTBUG-34881) Flickable can have its flick incorrectly stolen
* [QTBUG-125135](https://bugreports.qt.io/browse/QTBUG-125135) [Reg 6.5.3->6.5.4]Qml Popup component is not closing
anymore when instantiated via QQuickWidget.
* [QTBUG-131394](https://bugreports.qt.io/browse/QTBUG-131394) Type assertions don't work properly for inline
components
* [QTBUG-129599](https://bugreports.qt.io/browse/QTBUG-129599) ListView: ListView sometimes lags / pauses when dragging
it
* [QTBUG-131633](https://bugreports.qt.io/browse/QTBUG-131633) QML Palette documentation is incomplete
* [QTBUG-101159](https://bugreports.qt.io/browse/QTBUG-101159) SelectionRectangle does work with TableView in Android
* [QTBUG-120064](https://bugreports.qt.io/browse/QTBUG-120064) Clicking even on TextField vs Mousearea
* [QTBUG-93754](https://bugreports.qt.io/browse/QTBUG-93754) Qt Quick Controls Switch documentation does not state
clearly how to use the checked / not checked state
* [QTBUG-131098](https://bugreports.qt.io/browse/QTBUG-131098) TopLevel Dialogs can be obscured because they are
dynamically centered under their parent Window
* [QTBUG-129427](https://bugreports.qt.io/browse/QTBUG-129427) Focus frame causes items in a RowLayout to change
position when focus navigating
* [QTBUG-131776](https://bugreports.qt.io/browse/QTBUG-131776) TableView: calling positionWithAtColumn when a syncView
is set, fails
* [QTBUG-130266](https://bugreports.qt.io/browse/QTBUG-130266) WheelHandler documentation examples are written for tap
handler
* [QTBUG-131749](https://bugreports.qt.io/browse/QTBUG-131749) Incorrect strokeColor behaviour using property bindings
and CurveRenderer
* [QTBUG-131807](https://bugreports.qt.io/browse/QTBUG-131807) qmlls options incompatibility from 6.8 to 6.9
* [QTBUG-131442](https://bugreports.qt.io/browse/QTBUG-131442) quickBeginDeferred: crash in combination with inline
components
* [QTBUG-132050](https://bugreports.qt.io/browse/QTBUG-132050) [Reg 6.8 -> 6.9] Different behavior in QML regex
compared to javascript
* [QTBUG-131958](https://bugreports.qt.io/browse/QTBUG-131958) qmlls: import warnings on wrong line
* [QTBUG-131296](https://bugreports.qt.io/browse/QTBUG-131296) qmlls fails to parse some QML modules and C++ types when
there is more than one QML module in a directory
* [QTBUG-128462](https://bugreports.qt.io/browse/QTBUG-128462) Qt Quick Dialog colors are wrong when switching themes
* [QTCREATORBUG-31881](https://bugreports.qt.io/browse/QTCREATORBUG-31881) QML Control + Click opens debug file
* [QTBUG-131920](https://bugreports.qt.io/browse/QTBUG-131920) F2 shortcut in qml files leads to build dir instead of
source
* [QTBUG-131980](https://bugreports.qt.io/browse/QTBUG-131980) [REG 6.5.4-6.8.1] Crash on value type property
initialization
* [QTBUG-129231](https://bugreports.qt.io/browse/QTBUG-129231) Sporadic crash on QQuickListViewPrivate::fixup()
* [QTBUG-131261](https://bugreports.qt.io/browse/QTBUG-131261) Use QML types Application QML Type documentation
* [QTBUG-131675](https://bugreports.qt.io/browse/QTBUG-131675) QML: Document "regexp" value type
* [QTBUG-130807](https://bugreports.qt.io/browse/QTBUG-130807) MouseArea::hoverEnabled property unexpectedly propagated
to child Controls.
* [QTBUG-131957](https://bugreports.qt.io/browse/QTBUG-131957) [REG 6.8.0 → 6.8.1] QML applications crash on macOS 12
(x86)
* [QTBUG-130328](https://bugreports.qt.io/browse/QTBUG-130328) the visual focus indicator of Button in FluentWinUI3
style doesn't work well with FocusScope
* [QTBUG-131774](https://bugreports.qt.io/browse/QTBUG-131774) [REG 5.15 → 6] remove warning on signal connect with no
arguments
* [QTBUG-132421](https://bugreports.qt.io/browse/QTBUG-132421) cmake: Specifying PROJECT_VERSION in a Quick project
fails generation
* [QTBUG-132423](https://bugreports.qt.io/browse/QTBUG-132423) [Reg 6.2.13->6.5] qtquickcompiler.prf is missing from
cross-compiling kits, so "CONFIG += qtquickcompiler" no longer works
when cross-compiling
* [QTBUG-132192](https://bugreports.qt.io/browse/QTBUG-132192) Item is not updated if it would be invisible under
software render
* [QTBUG-132355](https://bugreports.qt.io/browse/QTBUG-132355) Build failure with no-feature-quick-draganddrop option
* [QTBUG-129143](https://bugreports.qt.io/browse/QTBUG-129143) QML Text - Wrong implicitWidth
* [QTBUG-132118](https://bugreports.qt.io/browse/QTBUG-132118) Crash when adding JS resources to a QML document
directory
* [QTBUG-132350](https://bugreports.qt.io/browse/QTBUG-132350) "QML debugging is enabled" warning is not guaranteed to
show at startup
* [QTBUG-132523](https://bugreports.qt.io/browse/QTBUG-132523) Null pointer dereference causing crash in QQuickPopup
* [QTBUG-131961](https://bugreports.qt.io/browse/QTBUG-131961) Qml engine crashes when running SameValueZero
* [QTBUG-132100](https://bugreports.qt.io/browse/QTBUG-132100) Foreign QObject with an enum type cannot be registered
for Qml in a nested namespace
* [QTBUG-123764](https://bugreports.qt.io/browse/QTBUG-123764) MessageDialog detailed text does not show in Fusion
style on dark mode
* [QTBUG-130991](https://bugreports.qt.io/browse/QTBUG-130991) 6.8.0: qtdeclarative examples build fail
* [QTBUG-93625](https://bugreports.qt.io/browse/QTBUG-93625) qt_internal_add_test doesn't call qt_import_qml_plugins
* [QTBUG-127174](https://bugreports.qt.io/browse/QTBUG-127174) protobuf scalar types stop working if registered using
QML_USING
* [QTBUG-125631](https://bugreports.qt.io/browse/QTBUG-125631) [ios] Regression QMake -> CMake: slow build time due to
file copying and qmlcachegen
* [QTBUG-126205](https://bugreports.qt.io/browse/QTBUG-126205) CMake build takes 5x as long to build as qmake build
* [QTBUG-130893](https://bugreports.qt.io/browse/QTBUG-130893) ShapePath.fillItem doesn't work with all items; doesn't
scale correctly with QT_SCALE_FACTOR
* [QTBUG-126794](https://bugreports.qt.io/browse/QTBUG-126794) Crash with ListView of LayoutItemProxy
* [QTBUG-131487](https://bugreports.qt.io/browse/QTBUG-131487) QFileSystemModel does not work with QML DelegateModel
* [QTBUG-131702](https://bugreports.qt.io/browse/QTBUG-131702) qmlls sends an error when trying to stop on startup
* [QTBUG-131721](https://bugreports.qt.io/browse/QTBUG-131721) QML type loader thread has data races
* [QTBUG-131898](https://bugreports.qt.io/browse/QTBUG-131898) Moving the window sometimes crashes the application
* [QTBUG-132075](https://bugreports.qt.io/browse/QTBUG-132075) tst_qquicktext::multilengthStrings(Wrap) Compared
doubles are not the same (fuzzy compare)
* [QTCREATORBUG-31897](https://bugreports.qt.io/browse/QTCREATORBUG-31897) simplify qmlls setup / make it work out of the box
* [QTCREATORBUG-31823](https://bugreports.qt.io/browse/QTCREATORBUG-31823) Annotations and CodeCompletion is wrong or not
working
* [QTBUG-127691](https://bugreports.qt.io/browse/QTBUG-127691) qmllint: don't print duplicate warnings
* [QTBUG-132345](https://bugreports.qt.io/browse/QTBUG-132345) [Reg 6.5 -> 6.8] qmlcachegen miscompiles number
coercions
* [QTBUG-130087](https://bugreports.qt.io/browse/QTBUG-130087) QML Compiler statistics doesn't shows all modules
* [QTBUG-101704](https://bugreports.qt.io/browse/QTBUG-101704) ToolTip calculates its width incorrectly
* [QTBUG-132591](https://bugreports.qt.io/browse/QTBUG-132591) tst_QQmlInspector::connect(rectangle/unrestricted)
Received a fatal error
* [QTBUG-125289](https://bugreports.qt.io/browse/QTBUG-125289) Add an overload of toScriptValue that only produces
vanilla JavaScript types
* [QTBUG-101678](https://bugreports.qt.io/browse/QTBUG-101678) tst_qqmlinspector (and other tests in
tests/auto/qml/debugger/) times out on macOS 12 (x86_64) in CI
* [QTBUG-101972](https://bugreports.qt.io/browse/QTBUG-101972) "Killed process: No output received (timeout: 15m0s
seconds)" when running tst_QQmlDebugJS
* [QTBUG-102984](https://bugreports.qt.io/browse/QTBUG-102984) tst_QQmlDebugJS hangs on macOS in CI
* [QTBUG-132697](https://bugreports.qt.io/browse/QTBUG-132697) FAIL!  :
tst_QQmlDebugJS::setBreakpointInScriptThatQuits(custom)
'm_process->waitForFinished()' returned FALSE.
* [QTBUG-132275](https://bugreports.qt.io/browse/QTBUG-132275) timeout in tst_imagine
* [QTBUG-132789](https://bugreports.qt.io/browse/QTBUG-132789)  Killed process: No output received (timeout: 15m0s
seconds)
* [QTBUG-130374](https://bugreports.qt.io/browse/QTBUG-130374) tst_qquicktextedit is flaky on Linux

### qtmultimedia
* [QTBUG-124350](https://bugreports.qt.io/browse/QTBUG-124350) [Boot2Qt] Switching the cameras in QML camera app causes
the app to crash
* [QTBUG-129351](https://bugreports.qt.io/browse/QTBUG-129351) [Boot2Qt][Camera] The QML camera app crashed when
swtiching the camera from USB to CSI
* [QTBUG-130478](https://bugreports.qt.io/browse/QTBUG-130478) QVideoFormat::isSupported returns false with supported
video codecs if audio codec is not specified
* [QTBUG-119506](https://bugreports.qt.io/browse/QTBUG-119506) AudioOutputExample-Graphic&Multimedia-Example Unplugging
& plugging headphones don't work as expected
* [QTBUG-128869](https://bugreports.qt.io/browse/QTBUG-128869) declarative-camera capture-button stops responding under
very specific conditions
* [QTBUG-118827](https://bugreports.qt.io/browse/QTBUG-118827) [REG 6.2..11 -> 6.2.13] Qt Widget Spectrum Example
UnderrunError.
* [QTBUG-119766](https://bugreports.qt.io/browse/QTBUG-119766) Spectrum Example - The sound is not redirected when
output is changed
* [QTBUG-119767](https://bugreports.qt.io/browse/QTBUG-119767) Spectrum Example - Mode - Generated Tone does not work
* [QTBUG-124925](https://bugreports.qt.io/browse/QTBUG-124925) [REG 6.5.5 -> 6.5.6] Spectrum App Crashes after
recording sound in "Record and Playback" Mode
* [QTBUG-130911](https://bugreports.qt.io/browse/QTBUG-130911) Android: Regression for recording after ffmpeg update to
7.1
* [QTBUG-129379](https://bugreports.qt.io/browse/QTBUG-129379) Declarative camera example: video recording stutters.
* [QTBUG-130813](https://bugreports.qt.io/browse/QTBUG-130813) qt_add_ios_ffmpeg_libraries does not generate
SwiftSupport folder so AppStore rejects!
* [QTBUG-114674](https://bugreports.qt.io/browse/QTBUG-114674) Audio fails silently on iOS 16 following app suspended
* [QTBUG-131300](https://bugreports.qt.io/browse/QTBUG-131300) QMultimedia module build fails in Boot2Qt / Yocto
* [QTBUG-131495](https://bugreports.qt.io/browse/QTBUG-131495) GStreamer media player example does not automatically
start playing media
* [QTBUG-130970](https://bugreports.qt.io/browse/QTBUG-130970) [wayland] qtmm examples crash on rockchip when using
wayland
* [QTBUG-131284](https://bugreports.qt.io/browse/QTBUG-131284) The QML video example crashes when running fullscreen
mode for the video and getting back to the main app view
* [QTBUG-124351](https://bugreports.qt.io/browse/QTBUG-124351) [Boot2Qt][Wayland] The widgets camera app crashes when
taking the picture in the full screen
* [QTBUG-131107](https://bugreports.qt.io/browse/QTBUG-131107) QVideoFrame::toImage / qImageFromVideoFrame not safe to
call from worker thread
* [QTBUG-131567](https://bugreports.qt.io/browse/QTBUG-131567) Incorrect images are used for QML Media Player
documentation on the web
* [QTBUG-131715](https://bugreports.qt.io/browse/QTBUG-131715) QML VideoOutput.orientation is broken
* [QTBUG-131530](https://bugreports.qt.io/browse/QTBUG-131530) declarative-camera crashes on startup under iOS 18.1
* [QTBUG-114104](https://bugreports.qt.io/browse/QTBUG-114104) R8 is not supported on GLES 2.0 only systems
* [QTBUG-131832](https://bugreports.qt.io/browse/QTBUG-131832) qtmultimedia fails to build on yocto
* [QTBUG-129692](https://bugreports.qt.io/browse/QTBUG-129692) [darwin] Sporadic crashes on QMediaPlayer destuction
* [QTBUG-131882](https://bugreports.qt.io/browse/QTBUG-131882) QtMultimedia - crashes with 'darwin' plugin (iOS)
* [QTBUG-130898](https://bugreports.qt.io/browse/QTBUG-130898) Guard QML MediaRecorder videoResolution from accessing
invalid memory address
* [QTBUG-131753](https://bugreports.qt.io/browse/QTBUG-131753) QML module QtQuick3D.SpatialAudio depend on nonexisting
QML module QtQuick3DPrivate
* [QTBUG-128253](https://bugreports.qt.io/browse/QTBUG-128253) List of camera devices does not update on runtime
* [QTBUG-130901](https://bugreports.qt.io/browse/QTBUG-130901) Crash on Some Android Device when using Multimedia
* [QTBUG-115023](https://bugreports.qt.io/browse/QTBUG-115023) Video QML widget does not reset errorString after
assigning source and always resets after play
* [QTBUG-126305](https://bugreports.qt.io/browse/QTBUG-126305) Setting camera pixel format and resolution is failed.
* [QTBUG-132478](https://bugreports.qt.io/browse/QTBUG-132478) Memory leak in video playback
* [QTBUG-123023](https://bugreports.qt.io/browse/QTBUG-123023) [Examples] Audio input devices list is not updated when
connecting new device
* [QTBUG-129394](https://bugreports.qt.io/browse/QTBUG-129394) Qt Dice freeze (not hang, just jerky)
* [QTBUG-132266](https://bugreports.qt.io/browse/QTBUG-132266) QSoundEffect plays choppy WAV sound effects on macOS
* [QTBUG-132779](https://bugreports.qt.io/browse/QTBUG-132779) Regression: Captured images have no rotation data
applied
* [QTBUG-112952](https://bugreports.qt.io/browse/QTBUG-112952) Camera (Widgets) Example missing buttons in topbar
* [QTBUG-131270](https://bugreports.qt.io/browse/QTBUG-131270) Improve QMediaFormat::isSupported to support more codecs
* [QTBUG-129708](https://bugreports.qt.io/browse/QTBUG-129708) Wrong aspect ratio with rotated screen using
QScreenCapture and QMediaRecorder
* [QTBUG-108680](https://bugreports.qt.io/browse/QTBUG-108680) QAudioDeviceInfo does not report 176.4kHz sample rates
* [QTBUG-129915](https://bugreports.qt.io/browse/QTBUG-129915) Qt + VB-CABLE : 8 channels on macOS / 2 channels only on
Windows
* [QTBUG-108681](https://bugreports.qt.io/browse/QTBUG-108681) QAudioDevice min/max sample rate API is inappropriate
and also incorrect
* [QTBUG-127543](https://bugreports.qt.io/browse/QTBUG-127543) QSoundEffect/SoundEffect audioDevice property has no
effect when device is changed
* [QTBUG-123073](https://bugreports.qt.io/browse/QTBUG-123073) [macOS] QMediaRecorder failed to record an audio after
reconnecting AirPods
* [QTBUG-127000](https://bugreports.qt.io/browse/QTBUG-127000) Incorrect frame rate when starting H264 video. Incorrect
playback stop.
* [QTBUG-131759](https://bugreports.qt.io/browse/QTBUG-131759) Log FFmpeg version and license during startup
* [QTBUG-132532](https://bugreports.qt.io/browse/QTBUG-132532) Audiorecoder example bugs

### qttools
* [QTBUG-130873](https://bugreports.qt.io/browse/QTBUG-130873) WIndows/Windows11 Style: Designer signal slot editor
item view drawing artifacts
* [QTBUG-131014](https://bugreports.qt.io/browse/QTBUG-131014) Qt Widgets Designer: Grid not visible in dark mode
* [QTBUG-129392](https://bugreports.qt.io/browse/QTBUG-129392) Linguist doesn't display id for id-based translations
* [QTBUG-131480](https://bugreports.qt.io/browse/QTBUG-131480) Reg->6.8.1/Linux: Qt Linguist exit warning "Timers
cannot be stopped from another thread"
* [QTBUG-130734](https://bugreports.qt.io/browse/QTBUG-130734) QDoc doesn't recognize namespaced QML imports
* [QTBUG-130674](https://bugreports.qt.io/browse/QTBUG-130674) Control over which page a namespaced function appears in
* [QTBUG-131565](https://bugreports.qt.io/browse/QTBUG-131565) Remove \footnote documentation from QDoc manual
* [QTBUG-131375](https://bugreports.qt.io/browse/QTBUG-131375) QDoc generates "List of all members" tree items for
classes without public members.
* [QTBUG-130888](https://bugreports.qt.io/browse/QTBUG-130888) Incorrect formulation of conditonal noexcept \note's
* [QTBUG-128326](https://bugreports.qt.io/browse/QTBUG-128326) Can't document list<T> properties in QML
* [QTBUG-130282](https://bugreports.qt.io/browse/QTBUG-130282) build time path used in qdoc binary
* [QTBUG-130799](https://bugreports.qt.io/browse/QTBUG-130799) Remove or fix Q_OBJECT qdoc macro
* [QTBUG-118728](https://bugreports.qt.io/browse/QTBUG-118728) SimpleTextViewer-example The name of the file being
viewed is not shown
* [QTBUG-131884](https://bugreports.qt.io/browse/QTBUG-131884) qdoc: Segmentation fault when generating .qhp
* [QTBUG-130646](https://bugreports.qt.io/browse/QTBUG-130646) qdoc hangs when generating QML documentation

### qttranslations
* [QTBUG-130699](https://bugreports.qt.io/browse/QTBUG-130699) ts-all targets incredibly inefficient
* [QTBUG-132418](https://bugreports.qt.io/browse/QTBUG-132418) Qt6 Localisation - Cannot Add New Translation Language
* [QTBUG-125151](https://bugreports.qt.io/browse/QTBUG-125151) qt_add_translations CFBundleLocalizations broken

### qtdoc
* [QTBUG-119282](https://bugreports.qt.io/browse/QTBUG-119282) MediaPlayerApp-Example Issue with the audio output
* [QTBUG-130567](https://bugreports.qt.io/browse/QTBUG-130567) Doc: wrong link to XWayland
* [QTWEBSITE-1200](https://bugreports.qt.io/browse/QTWEBSITE-1200) Protect macOS specific file paths from translation
* [QTBUG-130467](https://bugreports.qt.io/browse/QTBUG-130467) Qt for Android build instructions are confusing when it
comes to -developer-build
* [QTBUG-130129](https://bugreports.qt.io/browse/QTBUG-130129) Docs: instruct user to put TQTC keyring in systemwide
folder, not ~
* [QTBUG-131025](https://bugreports.qt.io/browse/QTBUG-131025) Doc: Change documentation for 5 year LTS
* [QTBUG-130307](https://bugreports.qt.io/browse/QTBUG-130307) RobotArmApp example demo is visibly moving frame by
frame at the end of each movement
* [QTBUG-131486](https://bugreports.qt.io/browse/QTBUG-131486) Wrong licensing of "Qt 5 Core Compatibility APIs"
* [QTBUG-131769](https://bugreports.qt.io/browse/QTBUG-131769) Remove traces of VS 2019 in documentation

### qtlocation
* [QTBUG-34881](https://bugreports.qt.io/browse/QTBUG-34881) Flickable can have its flick incorrectly stolen

### qtpositioning
* [QTBUG-131484](https://bugreports.qt.io/browse/QTBUG-131484) Fix links to QIODeviceBase::OpenMode flags

### qtsensors
* [QTBUG-130799](https://bugreports.qt.io/browse/QTBUG-130799) Remove or fix Q_OBJECT qdoc macro

### qtconnectivity
* [QTBUG-124130](https://bugreports.qt.io/browse/QTBUG-124130) Bluetooth LE service data is trunctated at zero value
* [QTBUG-131940](https://bugreports.qt.io/browse/QTBUG-131940) Bluetooth examples does not work on iOS
* [QTBUG-132202](https://bugreports.qt.io/browse/QTBUG-132202) Qt bluetooth qlowenergycontroller_winrt.cpp incorrectly
assumes CharacteristicUserDescription returns UTF16 when it actually
returns UTF8
* [QTBUG-132510](https://bugreports.qt.io/browse/QTBUG-132510) Superfluous optional components
* [QTBUG-132571](https://bugreports.qt.io/browse/QTBUG-132571) Unable to build QtConnectivity without DBus
* [QTBUG-132455](https://bugreports.qt.io/browse/QTBUG-132455) [Android] Lots of deprecated API is used

### qtwayland
* [QTBUG-130627](https://bugreports.qt.io/browse/QTBUG-130627) AddressSanitizer: heap-use-after-free on
tst_WaylandClient::mouseDrag
* [QTBUG-129331](https://bugreports.qt.io/browse/QTBUG-129331) text input v3 preedit_string's cursor position isn't
honored
* [QTBUG-131983](https://bugreports.qt.io/browse/QTBUG-131983) text input v3: first character after refocus doesn't go
through the input method
* [QTBUG-132195](https://bugreports.qt.io/browse/QTBUG-132195) text input v3: disable() request isn't committed

### qt3d
* [QTBUG-131477](https://bugreports.qt.io/browse/QTBUG-131477) Review SBOM generation and documentation to include
third party components
* [QTBUG-132092](https://bugreports.qt.io/browse/QTBUG-132092) RayCasting failing sometimes
* [QTBUG-130470](https://bugreports.qt.io/browse/QTBUG-130470) Issues with BlitFramebuffer::interpolationMethod
* [QTBUG-130490](https://bugreports.qt.io/browse/QTBUG-130490) Unprotected access in animation handler
* [QTBUG-131459](https://bugreports.qt.io/browse/QTBUG-131459) QDoc: No warning if \qmltype contains \inherits with
non-existing type

### qtserialport
* [QTBUG-115292](https://bugreports.qt.io/browse/QTBUG-115292) QSerialPortInfo Provides USBHUB Info instead of Port
Info
* [QTBUG-109455](https://bugreports.qt.io/browse/QTBUG-109455) read() returns qint64 not int
* [QTBUG-120221](https://bugreports.qt.io/browse/QTBUG-120221) clang-tidy, and probably clang complains about dllimport
vs. inline in qtserialportinfo.h
* [QTBUG-105561](https://bugreports.qt.io/browse/QTBUG-105561) QSerialPort Mark/Space Emulation causes recursion and
crash
* [QTBUG-131679](https://bugreports.qt.io/browse/QTBUG-131679) QSerialPort does not have Mark/Space parity emulation
for reading the data
* [QTBUG-84689](https://bugreports.qt.io/browse/QTBUG-84689) readyRead() signal will be reemitted even I have called
waitForReadyRead()
* [QTBUG-67544](https://bugreports.qt.io/browse/QTBUG-67544) QSerialPort emits errorOccurred with NoError

### qtwebengine
* [QTBUG-131397](https://bugreports.qt.io/browse/QTBUG-131397) WebEngineProfile doesn't instantiate in QML if property
declarations are in a specific order
* [QTBUG-
131342](https://bugreports.qt.io/browse/QTBUG-131342) qtwebengine/src/core/compositor/native_skia_output_device_vulkan.
cpp:252:34: error: use of undeclared identifier 'importMemoryHandleInfo'
* [QTBUG-129153](https://bugreports.qt.io/browse/QTBUG-129153) Sporadic crash on NativeSkiaOutputDevice::BeginPaint()
* [QTBUG-131156](https://bugreports.qt.io/browse/QTBUG-131156) Scripts injected on DocumentReady and Deferred are not
always executed on google.com
* [QTBUG-131304](https://bugreports.qt.io/browse/QTBUG-131304) Broken rendering when reparenting WebEngineView to
another window
* [QTBUG-123095](https://bugreports.qt.io/browse/QTBUG-123095) Wheel scrolling issues in WebEngine
* [QTBUG-131896](https://bugreports.qt.io/browse/QTBUG-131896) A sentence is cut in the middle in the Native Dialogs
section in Qt WebEngine features
* [QTBUG-132564](https://bugreports.qt.io/browse/QTBUG-132564) qwebengine-convert-dict fails on .dic wordlist
* [QTBUG-128893](https://bugreports.qt.io/browse/QTBUG-128893) sbom for qtpdf gets lost , as it ends up as qtwebengine
sbom
* [QTBUG-130608](https://bugreports.qt.io/browse/QTBUG-130608) Dropdown in WebEngineView are not zoomed and aligned
properly when parent of WebEngineView is zoomed.
* [QTBUG-131607](https://bugreports.qt.io/browse/QTBUG-131607) Crash on NativeSkiaOutputDeviceDirect3D11::texture()
with nullptr access

### qtvirtualkeyboard
* [QTBUG-131347](https://bugreports.qt.io/browse/QTBUG-131347) Incorrect decimal point for German keyboard

### qtscxml
* [QTBUG-130799](https://bugreports.qt.io/browse/QTBUG-130799) Remove or fix Q_OBJECT qdoc macro
* [QTBUG-132510](https://bugreports.qt.io/browse/QTBUG-132510) Superfluous optional components

### qtnetworkauth
* [QTBUG-130159](https://bugreports.qt.io/browse/QTBUG-130159) [Reg 6.6.3 -> 6.7] QOAuth2AuthorizationCodeFlow uses
"localhost" as the redirect URI when it should be "127.0.0.1"
* [QTBUG-131948](https://bugreports.qt.io/browse/QTBUG-131948) OAuth2 expirationAt doest not change when invalidated
* [QTBUG-131949](https://bugreports.qt.io/browse/QTBUG-131949) Use UTC instead of local time for internal expiresAt
representation

### qtquicktimeline
* [QTBUG-131459](https://bugreports.qt.io/browse/QTBUG-131459) QDoc: No warning if \qmltype contains \inherits with
non-existing type

### qtquick3d
* [QTBUG-130647](https://bugreports.qt.io/browse/QTBUG-130647) hand property is missing in XrInputAction doc
* [QTBUG-131361](https://bugreports.qt.io/browse/QTBUG-131361) Intel skylake fails to build for Boot2Qt lts-6.5(.8)
* [QTBUG-128560](https://bugreports.qt.io/browse/QTBUG-128560) Lancelot test custom material error
* [QTBUG-127406](https://bugreports.qt.io/browse/QTBUG-127406) Add Path to entries of
qtquick3d/src/3rdparty/openxr/qt_attribution.json
* [QTBUG-132273](https://bugreports.qt.io/browse/QTBUG-132273) Quick3D runtime error with gcc >=12.1
* [QTBUG-132080](https://bugreports.qt.io/browse/QTBUG-132080) Directional light order influences shadow mapping
* [QTBUG-132081](https://bugreports.qt.io/browse/QTBUG-132081) Shadow mapping broken with orthographic camera
* [QTBUG-132838](https://bugreports.qt.io/browse/QTBUG-132838) Debug build fails at rendererimpl
* [QTBUG-130962](https://bugreports.qt.io/browse/QTBUG-130962) View3D inside XrItem's contentItem is not rendered
* [QTBUG-132811](https://bugreports.qt.io/browse/QTBUG-132811) ExtendedSceneEnvironment does not work with multiview

### qt5compat
* [QTBUG-122798](https://bugreports.qt.io/browse/QTBUG-122798) [REG 5.15 -> 6.7 (or earlier)] QStringRef -> QStringView
conversion loses null-ness
* [QTBUG-122797](https://bugreports.qt.io/browse/QTBUG-122797) QStringRef doesn't convert to QAnyStringView

### qtopcua
* [QTBUG-122005](https://bugreports.qt.io/browse/QTBUG-122005) qtopcua is not building against OpenSSL-1.1.1

### qthttpserver
* [QTBUG-130500](https://bugreports.qt.io/browse/QTBUG-130500) Various network tests are failing on macOS 15

### qtgrpc
* [QTBUG-131134](https://bugreports.qt.io/browse/QTBUG-131134) Compilation error: ‘class QGrpcChannelOptions’ has no
member named ‘sslConfiguration’
* [QTBUG-131577](https://bugreports.qt.io/browse/QTBUG-131577) FAIL!  :
tst_protobuf_repeated_qml::qtprotobufRepeatedTest::initTestCase()
Uncaught exception
* [QTBUG-131415](https://bugreports.qt.io/browse/QTBUG-131415) qtprotobufgen crashes on Any inside a oneof field
* [QTBUG-131417](https://bugreports.qt.io/browse/QTBUG-131417) qtprotobufgen: header guards with invalid C-identifier
* [QTBUG-129652](https://bugreports.qt.io/browse/QTBUG-129652) Messages that have the 'Repeated' suffix lead to name
clashing with the generated Repeated aliases
* [QTBUG-112423](https://bugreports.qt.io/browse/QTBUG-112423) QtProtobuf: Required.Proto3.ProtobufInput.ValidDataRepea
ted.ENUM.UnpackedInput.ProtobufOutput is failing
* [QTBUG-112425](https://bugreports.qt.io/browse/QTBUG-112425) QtProtobuf:  Recommended.Proto3.ProtobufInput.ValidDataR
epeated.ENUM.UnpackedInput.PackedOutput.ProtobufOutput test is failing
* [QTBUG-112424](https://bugreports.qt.io/browse/QTBUG-112424) QtProtobuf: Recommended.Proto3.ProtobufInput.ValidDataRe
peated.ENUM.UnpackedInput.DefaultOutput.ProtobufOutput test is failing
* [QTBUG-129588](https://bugreports.qt.io/browse/QTBUG-129588) QtGRPC: create a minimal overview example
* [QTBUG-125406](https://bugreports.qt.io/browse/QTBUG-125406) QtGrpc: rework documentation
* [QTBUG-132182](https://bugreports.qt.io/browse/QTBUG-132182) ProtobufQtCoreTypes: missing Qt includes for mapped
messages
* [QTBUG-130555](https://bugreports.qt.io/browse/QTBUG-130555) JSON serialization of google.protobuf.Timestamp seems to
be off
* [QTBUG-131780](https://bugreports.qt.io/browse/QTBUG-131780) GrpcQuick and ProtobufQuick are missing as necessary
dependencies for QML parameter for qt_add_protobuf and qt_add_grpc
* [QTBUG-131689](https://bugreports.qt.io/browse/QTBUG-131689) protobuf and grpc installation example should be clearer
* [QTBUG-132954](https://bugreports.qt.io/browse/QTBUG-132954) QDoc: error: Documentation warnings (2) exceeded the
limit (0) for 'QtProtobuf'
* [QTBUG-129571](https://bugreports.qt.io/browse/QTBUG-129571) QtGRPC: verify examples
* [QTBUG-127174](https://bugreports.qt.io/browse/QTBUG-127174) protobuf scalar types stop working if registered using
QML_USING
* [QTBUG-128753](https://bugreports.qt.io/browse/QTBUG-128753) Protobufgen/grpcgen tests override their results
* [QTBUG-128468](https://bugreports.qt.io/browse/QTBUG-128468) Vehicle client example asserts on exit
* [QTBUG-129918](https://bugreports.qt.io/browse/QTBUG-129918) [FTBFS] gtgrpc: CMake Error: AUTOMOC for target
protocplugintestcommon: The "moc" executable "xxxx" does not exist.
* [QTBUG-132125](https://bugreports.qt.io/browse/QTBUG-132125) Clashing of Quick Components and Protobuf QML messages

### qtgraphs
* [QTBUG-130010](https://bugreports.qt.io/browse/QTBUG-130010) userDefinedMesh is ignored
* [QTBUG-130011](https://bugreports.qt.io/browse/QTBUG-130011) Changing selection pointer mesh with Surface3D does not
work
* [QTBUG-130870](https://bugreports.qt.io/browse/QTBUG-130870) Selection pointer does not follow highlight color
immediately
* [QTBUG-127800](https://bugreports.qt.io/browse/QTBUG-127800) Graphs3D namespace docs are missing from QML
* [QTBUG-131123](https://bugreports.qt.io/browse/QTBUG-131123) Docs mention non-existent Graphs3D.CameraPreset.None
enum value
* [QTBUG-131124](https://bugreports.qt.io/browse/QTBUG-131124) GraphsTheme documentation ambiguities
* [QTBUG-131140](https://bugreports.qt.io/browse/QTBUG-131140) LogValue3DAxisFormatter "edgeLabelsVisible" or
"showEdgeLabels" bug
* [QTBUG-131278](https://bugreports.qt.io/browse/QTBUG-131278) Qt cockpit example .qrc file missing
* [QTBUG-131121](https://bugreports.qt.io/browse/QTBUG-131121) GraphTransition description example unorthodox
indentation
* [QTBUG-131366](https://bugreports.qt.io/browse/QTBUG-131366) Incorrect import and linking target hint for
Q3DSurfaceWidgetItem
* [QTBUG-129824](https://bugreports.qt.io/browse/QTBUG-129824) heightMapFile fails silently if the filename is
incorrect or cannot be found
* [QTBUG-131473](https://bugreports.qt.io/browse/QTBUG-131473) Q3DGraphsWidgetItem::customItems() always returns empty
list
* [QTBUG-131423](https://bugreports.qt.io/browse/QTBUG-131423) QBarDataItem::setRotation does not work as expected
* [QTBUG-131118](https://bugreports.qt.io/browse/QTBUG-131118) SplineSeries inherits XYSeries, but the documentation
indicates otherwise
* [QTBUG-131119](https://bugreports.qt.io/browse/QTBUG-131119) GraphPointAnimation and SplineControlAnimation have no
properties at all according to the docs
* [QTBUG-129767](https://bugreports.qt.io/browse/QTBUG-129767) Axis titleColor doesn't follow theming
* [QTBUG-129109](https://bugreports.qt.io/browse/QTBUG-129109) Unused signals in Q3DGraphsWidgetItem
* [QTBUG-127689](https://bugreports.qt.io/browse/QTBUG-127689) DirectToBackground and qDefaultSurfaceFormat are
probably incorrect
* [QTBUG-131730](https://bugreports.qt.io/browse/QTBUG-131730) aspectRatio and horizontalAspectRatio can be assigned
negative values
* [QTBUG-131120](https://bugreports.qt.io/browse/QTBUG-131120) GraphPointAnimation doesn't work with ScatterSeries
* [QTBUG-131733](https://bugreports.qt.io/browse/QTBUG-131733) Invalid preset can be assigned to theme
* [QTBUG-131735](https://bugreports.qt.io/browse/QTBUG-131735) Invalid value can be set to barThickness
* [QTBUG-131736](https://bugreports.qt.io/browse/QTBUG-131736) Graphs update even if nothing has changed
* [QTBUG-131796](https://bugreports.qt.io/browse/QTBUG-131796) qgraphstheme.cpp:5:10: fatal error: utils_p.h: No such
file or directory
* [QTBUG-131734](https://bugreports.qt.io/browse/QTBUG-131734) Invalid value can be assigned to renderingMode
* [QTBUG-131635](https://bugreports.qt.io/browse/QTBUG-131635) Selected points label flips when adjusting font size
* [QTBUG-131853](https://bugreports.qt.io/browse/QTBUG-131853) Shadow-like artefacts on surface graph
* [QTBUG-131890](https://bugreports.qt.io/browse/QTBUG-131890) Q3DBarsWidgetItem - documentation does not match snippet
* [QTBUG-131112](https://bugreports.qt.io/browse/QTBUG-131112) Vertical ValueAxis title with labels overlap
* [QTBUG-131854](https://bugreports.qt.io/browse/QTBUG-131854) Documentation is missing from some GraphsWidgets methods
* [QTBUG-132084](https://bugreports.qt.io/browse/QTBUG-132084) Legend data returns wrong colors for XYSeries
* [QTBUG-132159](https://bugreports.qt.io/browse/QTBUG-132159) Surface3D requires 2 clicks to display selection pointer
* [QTBUG-132402](https://bugreports.qt.io/browse/QTBUG-132402) SplineSeries remove() malfunctions when used with
GraphPointAnimation
* [QTBUG-129425](https://bugreports.qt.io/browse/QTBUG-129425) Unused signals in 2D side
* [QTBUG-132745](https://bugreports.qt.io/browse/QTBUG-132745) borderVisible property not working in Custom3DLabel in
QtGraphs.
* [QTBUG-132596](https://bugreports.qt.io/browse/QTBUG-132596) plotAreaBackgroundVisible of GraphsTheme not work
* [QTBUG-131131](https://bugreports.qt.io/browse/QTBUG-131131) Graphs3D related documentation bugs
* [QTBUG-131136](https://bugreports.qt.io/browse/QTBUG-131136) 3D scatter graph bugs
* [QTBUG-122089](https://bugreports.qt.io/browse/QTBUG-122089) Graphs3D.RenderingMode.DirectToBackground causes crashes
in autotests
* [QTBUG-131117](https://bugreports.qt.io/browse/QTBUG-131117) Pie graph bugs
* [QTBUG-131846](https://bugreports.qt.io/browse/QTBUG-131846) GraphsView missing plot area and ticks inside dialog
* [QTBUG-132009](https://bugreports.qt.io/browse/QTBUG-132009) LegendData cannot be instantiated
* [QTBUG-131111](https://bugreports.qt.io/browse/QTBUG-131111) LineSeries bugs
* [QTBUG-132107](https://bugreports.qt.io/browse/QTBUG-132107) 3D surface graph bugs
* [QTBUG-132401](https://bugreports.qt.io/browse/QTBUG-132401) SplineSeries removeMultiple() malfunctioning and
incorrectly documented

### qtapplicationmanager (Commercial only)
* [QTBUG-130388](https://bugreports.qt.io/browse/QTBUG-130388) application-features example has broken
* [QTBUG-132585](https://bugreports.qt.io/browse/QTBUG-132585) error: ignoring return value of function declared with
'nodiscard' attribute [-Werror,-Wunused-result]
* [QTBUG-132693](https://bugreports.qt.io/browse/QTBUG-132693) error: ignoring return value of function declared with
'nodiscard' attribute [-Werror,-Wunused-result]

### qtinterfaceframework (Commercial only)
* [QTBUG-130868](https://bugreports.qt.io/browse/QTBUG-130868) tst_simulation_backend_static (Failed)
* [QTBUG-132791](https://bugreports.qt.io/browse/QTBUG-132791) Attempt to promote imported target
"Python3::Interpreter" to global scope

### qtinsighttracker (Commercial only)
* [QTBUG-131763](https://bugreports.qt.io/browse/QTBUG-131763) DOC: Wrong link in to example sources
* [QTBUG-128736](https://bugreports.qt.io/browse/QTBUG-128736) DOC: Add missing configuration value
* [QTBUG-132587](https://bugreports.qt.io/browse/QTBUG-132587) error: ignoring return value of function declared with
'nodiscard' attribute [-Werror,-Wunused-result]

Known Issues
------------

* Check that your system meets Qt's requirements:
https://doc.qt.io/qt-6.8/supported-platforms.html
* RTA reported issues from Qt 6.8
https://qt-project.atlassian.net/issues/?filter=10287
* See Qt 6.8 known issues from:
https://wiki.qt.io/Qt_6.8_Known_Issues
* Qt 6.8.2 Open issues in Jira:
https://qt-project.atlassian.net/issues/?filter=10446

Credits for the  release goes to:
---------------------------------

Eirik Aavitsland  
Laszlo Agocs  
Owais Akhtar  
Anu Aliyas  
Even Oscar Andersen  
Soheil Armin  
Mate Barany  
Vladimir Belyavsky  
Nicholas Bennett  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
David Boddie  
Tatiana Borisova  
Joerg Bornemann  
Assam Boudjelthia  
Aurélien Brooke  
Kai Uwe Broulik  
Michael Brüning  
Olivier De Cannière  
Alexei Cazacov  
Kaloyan Chehlarski  
Mike Chen  
Alexandru Croitor  
Mitch Curtis  
Thibaut Cuvelier  
Giuseppe D'Angelo  
Pieter Dewachter  
Pavel Dubsky  
Artem Dyomin  
Alexey Edelev  
David Edmundson  
Oliver Eftevaag  
Christian Ehrlicher  
Andreas Eliasson  
Ilya Fedin  
Nicolas Fella  
Isak Fyksen  
Zoltan Gera  
Alexander Golubev  
Robert Griebl  
Johannes Grunenberg  
Kaj Grönholm  
Richard Moe Gustavsen  
Balló György  
Lucie Gérard  
Mikko Hallamaa  
Jøger Hansegård  
Inkamari Harjula  
Jani Heikkinen  
Tero Heikkinen  
Moss Heim  
Christian Heimlich  
Liu Heng  
Ulf Hermann  
Volker Hilsheimer  
Dominik Holland  
Botond István Horváth  
Samuli Hölttä  
Masoud Jami  
Morteza Jamshidi  
Allan Sandfeld Jensen  
Jonas Karlsson  
Friedemann Kleint  
Peter Kling  
Niko Korkala  
Tomi Korpipaa  
Fabian Kosmale  
Volker Krause  
Santhosh Kumar  
Jonas Kvinge  
Kai Köhne  
Lauri Laanmets  
Cage Lee  
Inho Lee  
Frédéric Lefebvre  
Paul Lemire  
Wladimir Leuschner  
Qiang Li  
Heng Liu  
Jarno Lämsä  
Robert Löhning  
Thiago Macieira  
Jonathan Marten  
Jan Moeller  
Bartlomiej Moskal  
Marc Mutz  
Antti Määttä  
Andy Nichols  
Mårten Nordheim  
Dennis Oberst  
Daniel Opitz  
Tinja Paavoseppä  
Kwanghyo Park  
David C. Partridge  
Jerome Pasion  
Evgen Pervenenko  
Samuli Piippo  
Timur Pocheptsov  
Rami Potinkara  
Sakaria Pouke  
Dheerendra Purohit  
MohammadHossein Qanbari  
Liang Qi  
David Redondo  
Topi Reinio  
Jaime Resano  
Shawn Rutledge  
Ahmad Samir  
Timon Sassor  
Lars Schmertmann  
Sami Shalayel  
Andy Shaw  
Venugopal Shivashankar  
Nils Petter Skålerud  
Ivan Solovev  
Axel Spoerl  
Patryk Stachniak  
Magdalena Stojek  
Martin Storsjö  
Christian Strømme  
Audun Sutterud  
Tasuku Suzuki  
Jan Arve Sæther  
Morten Sørvig  
Sadegh Taghavi  
Jere Tuliniemi  
Shantanu Tushar  
Paul Olav Tvete  
Esa Törmänen  
Tuomas Vaarala  
Sami Varanka  
Peter Varga  
Doris Verria  
Tor Arne Vestbø  
Juha Vuolle  
Olli Vuolteenaho  
Jaishree Vyas  
Jannis Völker  
David Warner  
Ole Wegen  
Michael Weghorn  
Edward Welbourne  
Paul Wicking  
Oliver Wolff  
Semih Yavuz  
Alexey Zerkin  
Yuhang Zhao  
Eike Ziller  
