Release note
============

Qt 6.5.7 release is a patch release made on the top of Qt 6.5.6.
As a patch release, Qt 6.5.7 does not add any new functionality but provides
bug fixes and other improvements and maintains both forward and backward
compatibility (source and binary) with Qt 6.5.6.
For detailed information about Qt 6.5, refer to the online documentation
included in this distribution. The documentation is also available online:

https://doc.qt.io/qt-6/index.html

The Qt version 6.5 series is binary compatible with the 6.4.x series.
Applications compiled for 6.4 will continue to run with 6.5.

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

* CVE-2024-39936 in qtbase

### qtbase
* 50683af3477 QStringConverterICU: Pass correct pointer to callback
Fixed a bug involving moved QStringEncoder/QStringDecoder objects
accessing invalid state.

* 538b928406f Don't quit automatically via QEventLoopLocker if there are
open windows
Fixed a regression where the last QEventLoopLocker going out of scope
would quit the app, even if there were open windows, if
quitOnLastWindowClosed was false.

* 9b779e9a3a3 QDBusSignature: accept empty strings as valid
Fixed a bug that caused the class not to accept an empty string as a
valid D-Bus SIGNATURE value.

* f843cd0d07b QXmlStreamWriter: fix attempts to write bad QStrings
The class now rejects writing UTF-8 and UTF-16 invalid input (improper
code unit sequences).

* dc0b5c8096b Update bundled libjpeg-turbo to version 3.0.3
libjpeg-turbo was updated to version 3.0.3

* 626f132a556 QVariant: do reset is_null after setValue()
Fixed a bug that would allow the class to keep returning isNull() =
true even after calling setValue().

* 519c9f14705 SQLite: Update SQLite to v3.46.0
Updated SQLite to v3.46.0

* 96d41da6bcc Entrypoint/Win32: just use __argc and __argv if available
Fixed a bug that caused Qt applications to disregard Unicode command-
lines on Windows even when argc and argv were passed un- modified to
QGuiApplication or QApplication. This happened only for builds with
Visual Studio and in the "windows" subsystem (not "console").

* 8c2e6967ba0 QAnyStringView: fix char-ish ctors to not allocate memory
Fixed a regression where constructing a QAnyStringView from a char-like
type (QChar, QLatin1Char, ...) would first construct a QString and only
then convert that to QAnyStringView.

* 9e538bac5ba Update public suffix list
Updated the public suffix list to upstream SHA
903a83ff7bfc3148e3692e09396f9f3bdc9462ef.

* 9bb369c1ef5 PCRE: upgrade to 10.44
PCRE2 was updated to version 10.44.

* 1b29cc68c13 Change the mimetype database embedded into QtCore
For licensing reasons, QtCore no longer ships a copy of the MIME
database from freedesktop.org's shared-mime-info project, but the one
from the Apache Tika project. The tika definitions don't have icons or
translated descriptions, but are sufficient for matching file types.

* 9a32e1ed9b3 QMimeDatabase: pick up XML mimetypes from :/qt-
project.org/mime/packages
QMimeDatabase can now pick up XML mimetype definitions from :/qt-
project.org/mime/packages. GPL-compatible projects which provide self-
contained binaries can use this to provide a copy of freedesktop.org.xml
that will be used instead of the TIKA mimetypes.

* 430953126da Remove GTK3 native menu
Due to deprecation of the gtk_menu_popup() function, we no longer use
GTK menus on Gnome: they are now rendered by Qt.

* bf734e2ab0f QCborValue: fix sorting of UTF8-to-UTF16 strings
Fixed a bug that caused certain non-US-ASCII string comparisons to
produce results not in line with the CBOR specifications.

* 0a4b037b902 QArrayDataOps: fix FP equality comparison
Fixed a bug when two QLists holding NaN values were considered to be
equal.

* 31e7237ef99 Add __attribute__((format(printf()))) to q(v)nprintf()
Added attributes for GCC-compatible compilers to detect format/argument
mismatches. If this throws warnings for your calls now, don't ignore
them. printf() format mistakes could be security-relevant. You may also
find that you relied on undocumented behavior, such as that certain
implementations (Windows, Android, WASM) of qsnprintf() support
char16_t* instead of wchar_t* for %ls. In that case, you should port to
qUtf16Printable() and QString::asprintf(), or suppress the warning and
port away from the platform dependence at your earliest convenience.

* fb20b23e058 Update CLDR to v45, adding language Kuvi
Updated CLDR data, used by QLocale, to v45.

* a76ed16a818 Fix partial_ordering::unordered != 0 comparison
Fixed a bug where partial_ordering::unordered != 0 comparison produced
an incorrect result.

* dc7ed707dce SQLite: Update SQLite to v3.46.1
Updated SQLite to v3.46.1

* 3b387bad862 Update Freetype to 2.13.3
Updated bundled Freetype to version 2.13.3.

* a1ab641ab62 Update tika-mimetypes.xml from upstream
Updated TIKA MIME types definition file to add the audio/aac and
application/x-java-keystore MIME types.

* 028b9b75165 Android: account for namespace in build.gradle instead of
manifest
Add support for namespace in build.gradle instead of the package
attribute in the manifest.

* c14cb68d5a4 Update tika-mimetypes.xml from upstream
Updated TIKA MIME types definition file to add the audio/flac MIME type
as an alias for audio/x-flac MIME type.

* f81258281b1 Android: upgrade to Gradle 8.10 and AGP 8.5.2
Updated Gradle to 8.10 and AGP to 8.5.2.

* 0bf48e28f4f QUrl::toString: fix using of NormalizePathSegments and
RemoveFilename
Fixed a bug that caused QUrl::toString(), QUrl::toEncoded() and
QUrl::adjusted() to ignore QUrl::NormalizePathSegments if
QUrl::RemoveFilename was set.

* f007270c3f2 Update to Harfbuzz 9.0.0
Updated Harfbuzz to 9.0.0.

* 17cad755b02 Update bundled libpng to version 1.6.44
libpng was updated to version 1.6.44

* 12db43c6bc8 Update bundled libjpeg-turbo to version 3.0.4
libjpeg-turbo was updated to version 3.0.4

### qtdeclarative
* e5e4da09e5 Warn about unset required properties on composite
singletons
Instantiating singletons with unset required properties will now fail
and print a warning instead of creating the singleton with the
properties unset.

* 3e7abefc46 QML: Type-check objects passed to QmlListWrapper
Assignments to list properties in QML are now type-checked. Before you
could, for example, insert a plain QObject into list<Item>, producing
undefined behavior. Now it instead inserts null and warns. In
particular, if you assign a JavaScript array of random objects to a list
property, QML will check each individual element, and insert null as
well as warn when encountering type incompatibilities.

### qtmultimedia
* 430981d7e GStreamer: add private API to access pipeline for capture
session
QMediaCaptureSession: GStreamer - private interface to access
underlying GstPipeline of QMediaCaptureSession

* 2f467b72f ALSA: use first device as default
ALSA: use first device as default, if ALSA doesn't report a default
device.

* a91041d6e GStreamer: custom audio io - introduce factory functions
QAudioInput/QAudioOutput: GStreamer - add private API to customize
audio input/output via a pipeline string.

* 9d9a9e67b Use correct stride factor with YUV420P10 pixel format
Fix display of videos using YUV420P10 pixel format

* f08ef241d Document dynamic linking of FFmpeg on macOS
Document that FFmpeg media backend links dynamically to FFmpeg
libraries on both Windows and macOS, and that applications using Qt
Multimedia with the FFmpeg media backend must deploy shared FFmpeg
libraries as part of their installers.

* 40e164b63 GStreamer: QGstreamerVideoSink - improve conversion element
override
QVideoSink: GStreamer - allow override of conversion element via
environment variable

* a1d53971c Update FFmpeg version in documentation
Updated FFmpeg to n7.0.1.

* f1ae35ed7 Update FFmpeg version in documentation
Updated FFmpeg to n7.0.2.

### qtsensors
* d2c0d8d6 Attribute Third-Party Code in Android Sensors Plugin
Add attribution for Android getRotationMatrix and getOrientation code,
copied from Android sources under Apache-2.0. This code is only used on
Android, as part of the Android Sensor plugin.

### qtconnectivity
* 0a24a7ee sdpscanner: fix format strings for (u)int64_t
Fixed a bug involving broken serialization of SDP_(U)INT64 DTDs on Big-
Endian machines.

### qtimageformats
* cc4c6019 Update bundled libtiff to version 4.7.0
Bundled libtiff was updated to version 4.7.0

### qtserialbus
* 3c84b87b Fix virtual can backend usage in multithreaded environment
Fixed a race condition during creation of the VirtualCanServer when two
QCanBusDevices are instantiated in the same process in different threads

### qtwebengine
* Qt WebEngine 6.5-lts is now based on the Qt WebEngine code from
Qt 6.7 and Chromium 118.

* 3feab861f RenderWidgetHostViewQtDelegateItem: keep grabs
WebEngineView (or WebView backed by Qt WebEngine) no longer allows
components outside to take over the mouse or touch exclusive grab. For
example if the user starts dragging a scrollbar inside the web view,
that continues until release, regardless of any DragHandler, Flickable
etc.

* 37430020d Add clearHttpCacheCompleted signal to profile
Added clearHttpCacheCompleted signal.

* bd8572420 Add QWebEngineSettings::ForceDarkMode
ForceDarkMode added, disabled by default.

* f46e2f2d6 Fix corrupted load/fetch state on start up in case of
NoCache
Switching profile to NoCache do not longer implicitly removes cache
from old data store.

* a82e90223 Add new API for screen capturing
Add QQuickWebEngineView::desktopMediaRequested() signal

* 613be810d Add WebEngineDriver
Added WebEngineDriver

* 6b165e3ad Merge remote-tracking branch 'origin/6.7' into tqtc/lts-6.5
Adjusted the license information to the version used in 6.7.

### qtnetworkauth
* 283a56e Don't clear QAbstractOAuth2::scope upon empty server response
If the authorization server returns an empty 'scope' response, the
requested scope is not cleared anymore. Instead, it is assumed that the
requested 'scope' was granted.

### qtquick3d
* 5bfe48e2c Update TinyEXR to v1.0.9
Updated TinyEXR to v1.0.9

### qt5compat
* 5fda336 QTextCodec: use DefaultConversion too
Fixed a bug that caused QTextCodec not to write the Byte Order Mark for
UTF codecs. QTextCodec now has the same behavior as Qt 5.x.

### qtopcua
* 21f9af49 Replace incorrect license attribution for 3rdparty/open62541
Correctly refer to the CC-BY-SA0 license as "Creative Commons
Attribution Share Alike 4.0 International".


Fixes
-----

### qtbase
* [QTBUG-123054](https://bugreports.qt.io/browse/QTBUG-123054) Reg[5->6] QSvgRenderer generated images are not
identical
* [QTBUG-124386](https://bugreports.qt.io/browse/QTBUG-124386) [Regression] QEventLoopLocker causes application to quit
even with open windows
* [QTBUG-118887](https://bugreports.qt.io/browse/QTBUG-118887) Screen.orientation broken on android 14
* [QTBUG-118236](https://bugreports.qt.io/browse/QTBUG-118236) Declarative Camera Example orientation errors on Android
13 / Android 14
* [QTBUG-111960](https://bugreports.qt.io/browse/QTBUG-111960) NPE: Attempt to invoke virtual method
setActivityDisplayRotation() on a null object reference
* [QTBUG-121046](https://bugreports.qt.io/browse/QTBUG-121046) Some dependencies are always considered not up to date.
* [QTBUG-112721](https://bugreports.qt.io/browse/QTBUG-112721) QLineEdit standard menu actions do not have object names
* [QTBUG-124186](https://bugreports.qt.io/browse/QTBUG-124186) syncqt is not found when building qt submodules using
cmake >= 3.29
* [QTBUG-124919](https://bugreports.qt.io/browse/QTBUG-124919) QDBusSignature considers an empty string to be an
invalid signature
* [QTBUG-123891](https://bugreports.qt.io/browse/QTBUG-123891) HTTP2: finished and errorOccurred signals never emitted
when auth fails with code 401
* [QTBUG-121880](https://bugreports.qt.io/browse/QTBUG-121880) QT_DEPLOY_TRANSLATIONS_DIR is ignored
* [QTBUG-125241](https://bugreports.qt.io/browse/QTBUG-125241) fromIccProfile fails with "failed minimal tag size
sanity"
* [QTBUG-124608](https://bugreports.qt.io/browse/QTBUG-124608) QResource file engine returns read-only memory for some
resources even with MapPrivateOption
* [QTBUG-122973](https://bugreports.qt.io/browse/QTBUG-122973) QDateTime::operator== documentation is wrong
* [QTBUG-125472](https://bugreports.qt.io/browse/QTBUG-125472) [Reg 5.15->6.x] QVariant::isNull() can return true for
non-null values
* [QTBUG-73655](https://bugreports.qt.io/browse/QTBUG-73655) QTableView Not Rendering Icons Correctly
* [QTBUG-125058](https://bugreports.qt.io/browse/QTBUG-125058) QtTest log QCRITICAL due to QApplication::regClass:
Registering window class 'Qt662dScreenChangeObserverWindow' failed.
(Class already exists.)
* [QTBUG-122436](https://bugreports.qt.io/browse/QTBUG-122436) Android a11y: Changes to Accessible.ignored and
Item.visible are not propagated to the screen reader
* [QTBUG-120331](https://bugreports.qt.io/browse/QTBUG-120331) rendering svg causes int overflows in
blend_vertical_gradient_argb
* [QTBUG-121653](https://bugreports.qt.io/browse/QTBUG-121653) License clarification for unicode & unicode-cldr related
files
* [QTBUG-67807](https://bugreports.qt.io/browse/QTBUG-67807) QOpenGLFunctions_4_5_Core has wrong prototypes for
*NamedBuffer* functions
* [QTBUG-122394](https://bugreports.qt.io/browse/QTBUG-122394) Crash when using QDockWidget
* [QTBUG-125531](https://bugreports.qt.io/browse/QTBUG-125531) Unable to drag files into the xwayland widget of
QTextEdit
* [QTBUG-122001](https://bugreports.qt.io/browse/QTBUG-122001) QMainWindow::tabifiedDockWidgets() - Not accurate
* [QTBUG-124262](https://bugreports.qt.io/browse/QTBUG-124262) [Reg] Crash when calling
QMainWindow:.tabifiedDockWidgets after QMainWindow::removeDockWidget
* [QTBUG-114439](https://bugreports.qt.io/browse/QTBUG-114439) No such signal
QPlatformNativeInterface::systemTrayWindowChanged(QScreen*) on Wayland
* [QTBUG-94871](https://bugreports.qt.io/browse/QTBUG-94871) Qt should subscribe to dbus system tray and dbus menu
service appearing/disappearing
* [QTBUG-86203](https://bugreports.qt.io/browse/QTBUG-86203) Documentation on QtAndroid:androidService(),
QtAndroid:androidContext() unclear
* [QTBUG-107486](https://bugreports.qt.io/browse/QTBUG-107486) Typo in the document
* [QTBUG-125958](https://bugreports.qt.io/browse/QTBUG-125958) Numpad 5 is not mapped to Qt::Key_Clear
* [QTBUG-125380](https://bugreports.qt.io/browse/QTBUG-125380) Windows command line arguments mangled by double prime
character
* [QTBUG-125735](https://bugreports.qt.io/browse/QTBUG-125735) [REG 6.4→6.5] QAnyStringView(char-ish) has become slow
* [QTBUG-125776](https://bugreports.qt.io/browse/QTBUG-125776) The Q_OBJECT macro documentation mentions obsolete
requirements
* [QTBUG-126056](https://bugreports.qt.io/browse/QTBUG-126056) Camelcase forwarding headers missing in macOS/iOS builds
* [QTBUG-126084](https://bugreports.qt.io/browse/QTBUG-126084) QDockWidget unplugged from floating tab is in the wrong
position
* [QTBUG-114938](https://bugreports.qt.io/browse/QTBUG-114938) 2dpainting example crashes on QNX
* [QTBUG-119076](https://bugreports.qt.io/browse/QTBUG-119076) Selecting multiple rows is sluggish if there are column
spans
* [QTBUG-123886](https://bugreports.qt.io/browse/QTBUG-123886) [REG 6.5.2->6.5.3] QAbstractScrollArea::sizeHint does
not include the horizontal scrollbar's size
* [QTBUG-23470](https://bugreports.qt.io/browse/QTBUG-23470) QLibrary does not add 'lib' prefix if file name starts
with 'lib' (unix)
* [QTBUG-124898](https://bugreports.qt.io/browse/QTBUG-124898) [Reg 6.2 -> 6.5] Qt.uiLanguage does not work for locale
changes
* [QTBUG-123298](https://bugreports.qt.io/browse/QTBUG-123298) Qt 6.5 on MacOS - In full screen, topmost QMenu action
doesn't fire
* [QTBUG-39403](https://bugreports.qt.io/browse/QTBUG-39403) QDesktopWidget::availableGeometry() returns wrong values
in Mac fullscreen mode
* [QTBUG-125993](https://bugreports.qt.io/browse/QTBUG-125993) Double tap on touch screen not provoking
mouseDoubleClickEvent - patch included
* [QTBUG-126381](https://bugreports.qt.io/browse/QTBUG-126381) qcssparser.cpp ASSERT: "d->parsed.metaType() ==
QMetaType::fromType<QList<QVariant>>()"
* [QTBUG-126594](https://bugreports.qt.io/browse/QTBUG-126594) 6.7.2 qtbase: missing cups dependency in
Qt6PrintSupport.pc and Qt6PrintSupport cmake modules
* [QTBUG-126502](https://bugreports.qt.io/browse/QTBUG-126502) Link broken on Qt Test Overview page in docs.qt.io
* [QTBUG-56590](https://bugreports.qt.io/browse/QTBUG-56590) macdeployqt copying dSYM bundles
* [QTBUG-126456](https://bugreports.qt.io/browse/QTBUG-126456) QWidgetWindow: Use of object after destruction
* [QTBUG-126043](https://bugreports.qt.io/browse/QTBUG-126043) macOS: Double clicking an appliaction in finder opens it
without the window becoming active
* [QTBUG-126678](https://bugreports.qt.io/browse/QTBUG-126678) CMake flag QT_USE_TARGET_ANDROID_BUILD_DIR does not work
with QT_ANDROID_BUILD_ALL_ABIS
* [QTBUG-122755](https://bugreports.qt.io/browse/QTBUG-122755) Dragging text on HighDPI screen results in a warning
"QPixmap::scaled: Pixmap is a null pixmap"
* [QTBUG-68465](https://bugreports.qt.io/browse/QTBUG-68465) macOS: Accessibility: MenuItems are not accessible
* [QTBUG-27205](https://bugreports.qt.io/browse/QTBUG-27205) QFileSystemModel::filename() uses wrong role value for
call to data() method
* [QTBUG-123449](https://bugreports.qt.io/browse/QTBUG-123449) [Reg 6.4->6.5] Quick MenuItems do not appear greyed out
when disabled under GTK
* [QTBUG-62970](https://bugreports.qt.io/browse/QTBUG-62970) tst_QComboBox::autoCompletionCaseSensitivity is flaky on
openSUSE 42.3
* [QTBUG-123998](https://bugreports.qt.io/browse/QTBUG-123998) Top flaky test: tst_qwidget::hoverPosition on
openSUSE_15_5 X86_64, Ubuntu_22_04, QNX_710
* [QTBUG-126610](https://bugreports.qt.io/browse/QTBUG-126610) HTTP2 Support leaks information
* [QTBUG-52292](https://bugreports.qt.io/browse/QTBUG-52292) Pantheon desktop is not recognized as Gtk desktop
* [QTBUG-126479](https://bugreports.qt.io/browse/QTBUG-126479) show()+showMaximized()+activating a layout de-maximizes
the window
* [QTBUG-104201](https://bugreports.qt.io/browse/QTBUG-104201) QWidget: resize() after showMaximized() causes strange
behaviour
* [QTBUG-125589](https://bugreports.qt.io/browse/QTBUG-125589) weired console message with simple application
* [QTBUG-126435](https://bugreports.qt.io/browse/QTBUG-126435) Document QT_NO_UTF8_SOURCE
* [QTBUG-127055](https://bugreports.qt.io/browse/QTBUG-127055) QThread::terminate() ABA problem
* [QTBUG-124561](https://bugreports.qt.io/browse/QTBUG-124561) Qt.labs.platform context Menu appears out of the app
window on Gnome/wayland
* [QTBUG-126598](https://bugreports.qt.io/browse/QTBUG-126598) Qt.labs.platform Menu broken content positioning on
linux
* [QTBUG-126012](https://bugreports.qt.io/browse/QTBUG-126012) [patch] bindTextureImage: clearing GL error: 0x500
* [QTBUG-60674](https://bugreports.qt.io/browse/QTBUG-60674) QSqlRelationalTableModel - relation refresh crash
* [QTBUG-124481](https://bugreports.qt.io/browse/QTBUG-124481) KDE theme plugin always assumes single click activation
on KDE Plasma 6
* [QTBUG-126575](https://bugreports.qt.io/browse/QTBUG-126575) QImage / QImageReader: lost QColorSpace during rotation
* [QTBUG-127473](https://bugreports.qt.io/browse/QTBUG-127473) [REG 5.15 -> 6] QList::op==() is broken for FP types
* [QTBUG-112287](https://bugreports.qt.io/browse/QTBUG-112287) android: Input does not work with QQuickWidget
* [QTBUG-126820](https://bugreports.qt.io/browse/QTBUG-126820) Move all QKeyCombination-returning operators into the
namespace Qt
* [QTBUG-127668](https://bugreports.qt.io/browse/QTBUG-127668) A standalone test can't be configure with a cross-
compiled Qt
* [QTBUG-127342](https://bugreports.qt.io/browse/QTBUG-127342) OCI plugin does not build for ARM
* [QTBUG-120396](https://bugreports.qt.io/browse/QTBUG-120396) `QUrl::resolved` gives wrong result when there are more
`..`s in relative reference
* [QTBUG-120050](https://bugreports.qt.io/browse/QTBUG-120050) Configuring a CMake-based Qt WASM project fails if emsdk
path has spaces
* [QTBUG-127512](https://bugreports.qt.io/browse/QTBUG-127512) tst_QTextLayout::softHyphens(16) failed on Ubuntu
24.04(both x64 and arm64) GNOME
* [QTBUG-116083](https://bugreports.qt.io/browse/QTBUG-116083) Build failure related to fontdatabase / fontconfig
* [QTBUG-127641](https://bugreports.qt.io/browse/QTBUG-127641) QComboBox popup position changes after widget
reparenting
* [QTBUG-125149](https://bugreports.qt.io/browse/QTBUG-125149) Misplaced popup menu for reparented combo box
* [QTBUG-122747](https://bugreports.qt.io/browse/QTBUG-122747) Reparenting QTabWidget with a native window tab can
cause crash
* [QTBUG-127392](https://bugreports.qt.io/browse/QTBUG-127392) Avoid warning: Ignoring window icon xxx exceeds maximum
xcb request length 65535
* [QTBUG-127759](https://bugreports.qt.io/browse/QTBUG-127759) Qt::partial_ordering::unordered implements op!=()
incorrectly
* [QTBUG-124310](https://bugreports.qt.io/browse/QTBUG-124310) QT_DISTANCEFIELD_DEFAULT_BASEFONTSIZE=128 causes a
QDistanceField crash
* [QTBUG-127552](https://bugreports.qt.io/browse/QTBUG-127552) a11y: QFrame reports incorrect top-level role on Linux
(AT-SPI2)
* [QTBUG-127168](https://bugreports.qt.io/browse/QTBUG-127168) Memory Leak: Windows: Result of SetupDiGetClassDevs() is
not freed
* [QTBUG-128137](https://bugreports.qt.io/browse/QTBUG-128137) qt-configure-module does not consider choosen
INSTALL_LIBEXECDIR
* [QTBUG-127926](https://bugreports.qt.io/browse/QTBUG-127926) Outdated Android docs still refer to
QtAndroid::androidActivity()
* [QTBUG-127381](https://bugreports.qt.io/browse/QTBUG-127381) Unexpected shift-selection in QTreeView.
* [QTBUG-128254](https://bugreports.qt.io/browse/QTBUG-128254) Cannot build signed AAB with verbose deployment
* [QTBUG-109619](https://bugreports.qt.io/browse/QTBUG-109619) Enabling 2 extra Android CMake options leads to a build
error
* [QTBUG-122967](https://bugreports.qt.io/browse/QTBUG-122967) [macOS]Calling winId() renders additional undesired
pixmap if scaling factor is not 1
* [QTBUG-128290](https://bugreports.qt.io/browse/QTBUG-128290) QT_THREAD_PARALLEL_FILLS macro causes
semaphore_wait_trap on iOS
* [QTBUG-124733](https://bugreports.qt.io/browse/QTBUG-124733) Tool bar loose focus over mouse hovering
* [QTBUG-125975](https://bugreports.qt.io/browse/QTBUG-125975)  QT_DISABLE_DEPRECATED_UP_TO 0x060400 gives link error
with static build
* [QTBUG-110841](https://bugreports.qt.io/browse/QTBUG-110841)  [REG: 5.10.1->5.11.0-alpha] Mouse events not observed
when Super (Windows) key is held down.
* [QTBUG-123092](https://bugreports.qt.io/browse/QTBUG-123092) Explain the order and the logic of using various SSL
backends
* [QTBUG-123752](https://bugreports.qt.io/browse/QTBUG-123752) Unexpected offset of fixed-height top-level window when
Windows Taskbar is on top
* [QTBUG-127987](https://bugreports.qt.io/browse/QTBUG-127987) Error copying directory: .syncqt_staging
* [QTBUG-94956](https://bugreports.qt.io/browse/QTBUG-94956) "Invalid revision: zipalign" when building for android
* [QTBUG-125239](https://bugreports.qt.io/browse/QTBUG-125239) ERROR: AddressSanitizer: heap-use-after-free WRITE of
size 1 in tst_QGuiApplication::modalWindow()
* [QTBUG-126752](https://bugreports.qt.io/browse/QTBUG-126752) Calling popup() on QCompleter causes an abnormal
behavior of the Qt virtual keyboard.
* [QTBUG-128516](https://bugreports.qt.io/browse/QTBUG-128516) [macOS] Sporadic crash on
QCocoaScreen::deliverUpdateRequests()
* [QTBUG-124465](https://bugreports.qt.io/browse/QTBUG-124465) QDate::fromString very slow in 6.7.0
* [QTBUG-127711](https://bugreports.qt.io/browse/QTBUG-127711) QUrl.adjusted doesn't work with QUrl::RemoveFilename |
QUrl::NormalizePathSegments
* [QTBUG-128800](https://bugreports.qt.io/browse/QTBUG-128800) QFileInfo::isSymLink() returns true with wrong path
* [QTBUG-128848](https://bugreports.qt.io/browse/QTBUG-128848) QTypeRevision::fromVersion fails ( in debug mode ), when
being fed with characters
* [QTBUG-123551](https://bugreports.qt.io/browse/QTBUG-123551) [Boot2Qt] A windows is blacked out in QQuickWidget
Example application
* [QTBUG-128929](https://bugreports.qt.io/browse/QTBUG-128929) Potential integer overflow in QNetworkReplyWasmImpl
* [QTBUG-128940](https://bugreports.qt.io/browse/QTBUG-128940) FAIL!  :
qmltestrunner::AnimatedImage::test_imageSource(local not found) Not all
expected messages were received
* [QTBUG-129434](https://bugreports.qt.io/browse/QTBUG-129434) [[Regr: 6.7.2 -> 6.7.3]] QTranslator::load finds
languages in wrong order
* [QTBUG-115158](https://bugreports.qt.io/browse/QTBUG-115158) Time zone names and abbreviations are not localised
* [QTBUG-122241](https://bugreports.qt.io/browse/QTBUG-122241) QXmlStreamWriter::writeCharacters fails to write UTF-8
encoded QAnyStringView
* [QTBUG-109367](https://bugreports.qt.io/browse/QTBUG-109367) Android native ExtractEditText does not receive text
updates from qml TextEdit in fullscreen mode and landscape orientation
* [QTBUG-125285](https://bugreports.qt.io/browse/QTBUG-125285) QKdeTheme falls back to Qt::ColorScheme::Unknown on
invalid desktop theme
* [QTBUG-101307](https://bugreports.qt.io/browse/QTBUG-101307) tst_qbytearrayview fails to compile with ubsan
* [QTBUG-125588](https://bugreports.qt.io/browse/QTBUG-125588) QString::arg(char16_t{}) prefers the integral, not the
QChar overload
* [QTBUG-126053](https://bugreports.qt.io/browse/QTBUG-126053) QString::arg(u8' ') prefers the integral, not the QChar
overload, when built in C++20
* [QTBUG-126054](https://bugreports.qt.io/browse/QTBUG-126054) QString::arg(wchar_t{}) prefers the integral overload
instead of the QChar one
* [QTBUG-126055](https://bugreports.qt.io/browse/QTBUG-126055) [REG SiC 6.4 -> 6.5] QString::arg(qfloat16{}) is
ambiguous if QFLOAT16_IS_NATIVE
* [QTBUG-124572](https://bugreports.qt.io/browse/QTBUG-124572) Program crash when using a specific glyph from a popular
font file on Linux
* [QTBUG-119469](https://bugreports.qt.io/browse/QTBUG-119469) Targets not yet defined: zstd::libzstd_static
* [QTBUG-126674](https://bugreports.qt.io/browse/QTBUG-126674) Inconsistent hashing between bool and integral overloads
* [QTBUG-127110](https://bugreports.qt.io/browse/QTBUG-127110) Platforms still use the inefficient qvsnprintf() fall-
back
* [QTBUG-119216](https://bugreports.qt.io/browse/QTBUG-119216) macOS: REG->6.5: DnD with custom text MIME type got
broken/crashes
* [QTBUG-125730](https://bugreports.qt.io/browse/QTBUG-125730) QAnyStringView('\xE4') creates an invalid UTF-8 string
(expected: valid L1)
* [QTBUG-126278](https://bugreports.qt.io/browse/QTBUG-126278) QNetworkReply::attribute(HttpReasonPhraseAttribute)
returns empty value when Http2 is used
* [QTBUG-127614](https://bugreports.qt.io/browse/QTBUG-127614) [macOS] [labs.platform] Menu stuck on opening when
standard icons are used
* [QTBUG-119901](https://bugreports.qt.io/browse/QTBUG-119901) Basic <type_traits> not working for q*int128 in QtCore
TUs
* [QTBUG-124011](https://bugreports.qt.io/browse/QTBUG-124011) Android: QFileInfo::isWritable() returns false
erroneously and throws an exception
* [QTBUG-54693](https://bugreports.qt.io/browse/QTBUG-54693) QFileDialog::getOpenFileName crashes when parent is
deleted while dialog is open

### qtsvg
* [QTBUG-128583](https://bugreports.qt.io/browse/QTBUG-128583) Regression in QtSvgTinyDocument: Runtime warnings logged
to the console

### qtdeclarative
* [QTBUG-46487](https://bugreports.qt.io/browse/QTBUG-46487) PathView. DelegateModel::item: index out range error when
model is reset with less number of items
* [QTBUG-124428](https://bugreports.qt.io/browse/QTBUG-124428) Customisation documentation includes deprecated
DropShadow example
* [QTBUG-123227](https://bugreports.qt.io/browse/QTBUG-123227) Qt Quick Test missing cmake support
* [QTBUG-118636](https://bugreports.qt.io/browse/QTBUG-118636) Some missing content of the rich text table while
displaying HTML file with TextArea
* [QTBUG-124281](https://bugreports.qt.io/browse/QTBUG-124281) MultiEffect doesn't seem to free resources at its
destruction
* [QTBUG-124730](https://bugreports.qt.io/browse/QTBUG-124730) MultiEffects Shadow in repeater causes application to
crash
* [QTBUG-124474](https://bugreports.qt.io/browse/QTBUG-124474) The text of QML ComboBox in a Window turns invisible in
dark mode
* [QTBUG-84976](https://bugreports.qt.io/browse/QTBUG-84976) When Window has no activeFocus, activeFocus lost after
transitioning back from Dialog to Window
* [QTBUG-125049](https://bugreports.qt.io/browse/QTBUG-125049) SplitView jumps to an incorrect width when resizing if
another object in SplitView is not visible.
* [QTBUG-124657](https://bugreports.qt.io/browse/QTBUG-124657) qsTrNoOp() is not defined in QML
* [QTBUG-125228](https://bugreports.qt.io/browse/QTBUG-125228) Customizing Quick Controls Documentation should use
Templates instead
* [QTBUG-124357](https://bugreports.qt.io/browse/QTBUG-124357) Quick Controls are not rendered correctly when changing
OS theme
* [QTBUG-117899](https://bugreports.qt.io/browse/QTBUG-117899) [REG 6.4->6.5] Binding Loops -> Wrong layout because of
interruption
* [QTBUG-118511](https://bugreports.qt.io/browse/QTBUG-118511) Binding loop if ColumnLayout implicitWidth is changed
* [QTBUG-56921](https://bugreports.qt.io/browse/QTBUG-56921) Imperatively setting TextEdit's alignment results in
incorrectly aligned text
* [QTBUG-119644](https://bugreports.qt.io/browse/QTBUG-119644) [Tests] Warnings in
qtdeclarative/tests/auto/quickcontrols/controls/data/tst_combobox.qml
* [QTBUG-125580](https://bugreports.qt.io/browse/QTBUG-125580) [Tests] Warnings in
tst_controls::Material::ComboBox::test_comboBoxWithShaderEffect()
* [QTBUG-125393](https://bugreports.qt.io/browse/QTBUG-125393) qmllint fails when given files names with backslashes on
Windows
* [QTBUG-124229](https://bugreports.qt.io/browse/QTBUG-124229) FAILED:
src/qmltest/CMakeFiles/QuickTest.dir/quicktest.cpp.o
* [QTBUG-124230](https://bugreports.qt.io/browse/QTBUG-124230) tst_focus::reason is failing
* [QTBUG-74331](https://bugreports.qt.io/browse/QTBUG-74331) beyond living (aka not really dead) link in colors docs
* [QTBUG-125429](https://bugreports.qt.io/browse/QTBUG-125429) send array from qml to c++
* [QTBUG-125914](https://bugreports.qt.io/browse/QTBUG-125914) Formatting qml code containing an enum with qmlformat
removes enum values
* [QTBUG-122658](https://bugreports.qt.io/browse/QTBUG-122658) ListView crashes when `reuseitems` is set after
`positionViewAtIndex`
* [QTBUG-125529](https://bugreports.qt.io/browse/QTBUG-125529) Lancelot baseline mismatch in Qt Quick's ComboBox using
Basic style
* [QTBUG-126124](https://bugreports.qt.io/browse/QTBUG-126124) Material style Button has extra padding when text
property has a value but display is IconOnly
* [QTBUG-124744](https://bugreports.qt.io/browse/QTBUG-124744) [Reg 6.7.0 -> dev] Bindings on width/height of
ApplicationWindow.background are not respected
* [QTBUG-125157](https://bugreports.qt.io/browse/QTBUG-125157) Clarify the snippet about Editing Cells in a TableView
* [QTBUG-112320](https://bugreports.qt.io/browse/QTBUG-112320) javascript engine:  Proxy handler.get() doesn't work on
field 'name'
* [QTBUG-122998](https://bugreports.qt.io/browse/QTBUG-122998) Crash in QQuickItemView through recursive item release
* [QTBUG-118165](https://bugreports.qt.io/browse/QTBUG-118165) qmlTypeId() causes QML_ELEMENTs to not be registered
* [QTBUG-123527](https://bugreports.qt.io/browse/QTBUG-123527) Unchecked Fusion style RadioButtons / CheckBoxes are
barely visible in dark mode
* [QTBUG-126136](https://bugreports.qt.io/browse/QTBUG-126136) QML signal to C++ slot connection nonfunctional if
declared within the C++ object with the slot
* [QTBUG-125224](https://bugreports.qt.io/browse/QTBUG-125224) Cannot stop animation if it was restarted before the
last loop completed
* [QTBUG-126042](https://bugreports.qt.io/browse/QTBUG-126042) Nested ListView of orthogonal orientation gets stuck
without snapping using touchpad
* [QTBUG-126057](https://bugreports.qt.io/browse/QTBUG-126057) Item state change reverts item's scaled size
* [QTBUG-119866](https://bugreports.qt.io/browse/QTBUG-119866) TapHandler is used in most of the code snippet of
DragHandler
* [QTBUG-124572](https://bugreports.qt.io/browse/QTBUG-124572) Program crash when using a specific glyph from a popular
font file on Linux
* [QTBUG-119647](https://bugreports.qt.io/browse/QTBUG-119647) [Tests] Warnings in
qtdeclarative/tests/auto/quickcontrols/controls/data/tst_tumbler.qml
* [QTBUG-126330](https://bugreports.qt.io/browse/QTBUG-126330) Crash when resizing ListView with reuseItems: true and
custom QQuickAsyncImageProvider
* [QTBUG-126396](https://bugreports.qt.io/browse/QTBUG-126396) Illegal memory access in QQuickShaderEffectPrivate
* [QTBUG-125906](https://bugreports.qt.io/browse/QTBUG-125906) Flicking needs to be done horizontally to delete items
in apps that have been rotated 90°.
* [QTBUG-126723](https://bugreports.qt.io/browse/QTBUG-126723) [REG 6.6 → 6.7] TableModel appendRow() no longer works.
* [QTBUG-123987](https://bugreports.qt.io/browse/QTBUG-123987) QML Popup "palette" property is not linking forward to
the proper palette docs
* [QTBUG-116442](https://bugreports.qt.io/browse/QTBUG-116442) Doubleclick sent to first item when single-clicking
alternating items
* [QTBUG-126626](https://bugreports.qt.io/browse/QTBUG-126626) Hovered property stays when popup is opened from drawer
* [QTBUG-125296](https://bugreports.qt.io/browse/QTBUG-125296) background color of TreeViewDelegate
* [QTBUG-127399](https://bugreports.qt.io/browse/QTBUG-127399) LayoutMirroring warning has typo
* [QTBUG-123191](https://bugreports.qt.io/browse/QTBUG-123191) Scenegraph nodes batching broken beginning with Qt 6.5.3
* [QTBUG-109880](https://bugreports.qt.io/browse/QTBUG-109880) Wrapper method that should create and return a
Javascript Generator object returns undefined
* [QTBUG-127619](https://bugreports.qt.io/browse/QTBUG-127619) FileDialog prints binding loop warning when opened.
* [QTBUG-30768](https://bugreports.qt.io/browse/QTBUG-30768) When an item in a ListView is snapped into place then it
does not take account for the section header
* [QTBUG-126474](https://bugreports.qt.io/browse/QTBUG-126474) QQuickLayout Recursive Rearrange Locks Application
* [QTBUG-124498](https://bugreports.qt.io/browse/QTBUG-124498) qmltyperesolver can't handle ECMAScript resources
* [QTBUG-125095](https://bugreports.qt.io/browse/QTBUG-125095) [REG 6.2 → 6.5] Qt.binding fails with QtQObject inside
createObject
* [QTBUG-81231](https://bugreports.qt.io/browse/QTBUG-81231) QJSEngine and QStringList properties handling, a
potential performance issue
* [QTBUG-126886](https://bugreports.qt.io/browse/QTBUG-126886) Setting format in QQuickTextDocument (TextArea) crashes
* [QTBUG-125053](https://bugreports.qt.io/browse/QTBUG-125053) QAbstractListModel fails to populate QML model
* [QTBUG-97557](https://bugreports.qt.io/browse/QTBUG-97557) Qt Quick batch rendering issue when a batch contain nodes
that have different index types
* [QTBUG-127315](https://bugreports.qt.io/browse/QTBUG-127315) Tumbler's currentIndex is not the same as the initial
value
* [QTBUG-124553](https://bugreports.qt.io/browse/QTBUG-124553) [Reg 5.15 -> 6.2] QML Binding is overwritten after
initialization
* [QTBUG-124921](https://bugreports.qt.io/browse/QTBUG-124921) Tumbler's currentIndex is not working when the model is
changed at runtime
* [QTBUG-126512](https://bugreports.qt.io/browse/QTBUG-126512) Controls styles use Qt.styleHints even though
documentation advises against it
* [QTBUG-124124](https://bugreports.qt.io/browse/QTBUG-124124) QtQuick MessageDialog: Fails on macOS when using
richtext
* [QTBUG-125416](https://bugreports.qt.io/browse/QTBUG-125416) SwipeView shows all elements at once if it is 0x0 in
size
* [QTBUG-127809](https://bugreports.qt.io/browse/QTBUG-127809) TableView forceLayout does not correct contentX/contentY
after columnWidth/rowHeight changed
* [QTBUG-121449](https://bugreports.qt.io/browse/QTBUG-121449) The emojis are pixelated
* [QTBUG-127455](https://bugreports.qt.io/browse/QTBUG-127455) QML ListView crashes in
QQuickItemViewPrivate::itemGeometryChanged
* [QTBUG-128283](https://bugreports.qt.io/browse/QTBUG-128283) Memory leak after calling QQuickItem::grabToImage
* [QTBUG-114984](https://bugreports.qt.io/browse/QTBUG-114984) Software Renderer: Updating a layer-enabled subtree
while it is invisible produces wrong outcomes
* [QTBUG-127440](https://bugreports.qt.io/browse/QTBUG-127440) QML TextField can't deselect by clicking on the text
field
* [QTBUG-10684](https://bugreports.qt.io/browse/QTBUG-10684) Interaction between text input and flickable is lacking
* [QTBUG-111504](https://bugreports.qt.io/browse/QTBUG-111504) Text loses selection when releasing long-press on
Android text input
* [QTBUG-116606](https://bugreports.qt.io/browse/QTBUG-116606) unable to deselect text in text input using touch
* [QTBUG-127343](https://bugreports.qt.io/browse/QTBUG-127343) Incomplete and inconsistent type checking for QML lists
* [QTBUG-123636](https://bugreports.qt.io/browse/QTBUG-123636) Crash when calling QWidget::setFixedSize with larger
values
* [QTBUG-123595](https://bugreports.qt.io/browse/QTBUG-123595) VerticalHeaderView / HorizontalHeaderView should always
use headerData() -- stale docs?
* [QTBUG-127727](https://bugreports.qt.io/browse/QTBUG-127727) tst_SoftwareRenderer::renderTarget fails
* [QTBUG-127906](https://bugreports.qt.io/browse/QTBUG-127906) Qt.labs.platform.Menu opens at the wrong location with
scaling enabled
* [QTBUG-126981](https://bugreports.qt.io/browse/QTBUG-126981) Application crashes with assert when closing the window
with TableView
* [QTBUG-126628](https://bugreports.qt.io/browse/QTBUG-126628) QQuickAsyncImageProvider causes crash without Qt Network
(qml_network)
* [QTBUG-129165](https://bugreports.qt.io/browse/QTBUG-129165) regression ListView not updating count
* [QTBUG-116577](https://bugreports.qt.io/browse/QTBUG-116577) ASSERT: "sumFactors > 0.0"  in qgridlayoutengine.cpp
* [QTBUG-123999](https://bugreports.qt.io/browse/QTBUG-123999) Heap buffer overflow in JS Set.delete
* [QTBUG-122784](https://bugreports.qt.io/browse/QTBUG-122784) QtQuick: Unset required property in Singleton is not an
error?
* [QTBUG-117526](https://bugreports.qt.io/browse/QTBUG-117526) QQuickStylePrivate::fallbackStyle has the wrong value
when using run-time style selection and the fallback style is imported
via the style's qmldir
* [QTBUG-126222](https://bugreports.qt.io/browse/QTBUG-126222) tst_how_to_qml::activeFocusDebugging() fails often
* [QTBUG-112870](https://bugreports.qt.io/browse/QTBUG-112870) clang-tidy warnings on static global variables in moc
generated code
* [QTBUG-126560](https://bugreports.qt.io/browse/QTBUG-126560) ListView's count property not updating when the ListView
is inside a Drawer and the model gets its data from a network request
* [QTBUG-125589](https://bugreports.qt.io/browse/QTBUG-125589) weired console message with simple application
* [QTBUG-125571](https://bugreports.qt.io/browse/QTBUG-125571) YAnimator onRunningChanged can Qt.callLater(jsFunc) with
invalid scope object
* [QTBUG-68465](https://bugreports.qt.io/browse/QTBUG-68465) macOS: Accessibility: MenuItems are not accessible
* [QTBUG-118024](https://bugreports.qt.io/browse/QTBUG-118024) Still referenced objects are deleted during swap
operation between two ListModel instances
* [QTBUG-123491](https://bugreports.qt.io/browse/QTBUG-123491) qmlls memory leak
* [QTBUG-124922](https://bugreports.qt.io/browse/QTBUG-124922) The text in a TextEdit is not updated when
LayoutMirroring is enabled
* [QTBUG-36525](https://bugreports.qt.io/browse/QTBUG-36525) Binding loop warning message does not give sufficient
information in order to fix it
* [QTBUG-96630](https://bugreports.qt.io/browse/QTBUG-96630) MenuItem mnemonic shortcut not triggered
* [QTBUG-128420](https://bugreports.qt.io/browse/QTBUG-128420) Qt 6.8 does not support build paths with white spaces
anymore

### qtactiveqt
* [QTBUG-111760](https://bugreports.qt.io/browse/QTBUG-111760) target_link_libraries(foo INTERFACE Qt::Core) fails for
interface libs with CMake < 3.19 on Windows

### qtmultimedia
* [QTBUG-124431](https://bugreports.qt.io/browse/QTBUG-124431) When using QMediaRecorder or QAudioInput with alsa it
chooses the wrong Endianess with ALSA audio
* [QTBUG-124182](https://bugreports.qt.io/browse/QTBUG-124182) [gstreamer] tst_QCameraBackend::testNativeMetadata test
failure
* [QTBUG-124544](https://bugreports.qt.io/browse/QTBUG-124544) [gstreamer] duration is not extracted from metadata
* [QTBUG-125080](https://bugreports.qt.io/browse/QTBUG-125080) [gstreamer] audio io crashes with FEATURE_alsa
* [QTBUG-125006](https://bugreports.qt.io/browse/QTBUG-125006) MediaPlayer fails to play rpt video stream using sdp
file.
* [QTBUG-124615](https://bugreports.qt.io/browse/QTBUG-124615) Top flaky test: tst_qmediaplayerbackend::play_createsFra
mesWithExpectedContentAndIncreasingFrameTime_whenPlayingRtspMediaStream
on MacOS_14 ARM64, MacOS_12, MacOS_13, Ubuntu_22_04, openSUSE_15_5.
* [QTBUG-124298](https://bugreports.qt.io/browse/QTBUG-124298) [iOS] Loading a new sound stops the play for other
sounds
* [QTBUG-123044](https://bugreports.qt.io/browse/QTBUG-123044) android: Playing something through QMediaPlayer and
adjusting volume from physical buttons shows wrong mode
* [QTBUG-124189](https://bugreports.qt.io/browse/QTBUG-124189) tst_qcamerabackend: crash on exit
* [QTBUG-124228](https://bugreports.qt.io/browse/QTBUG-124228) [gstreamer]
tst_QMediaCaptureSession::can_change_CameraDevice_on_attached_Camera
crashes sometimes
* [QTBUG-122118](https://bugreports.qt.io/browse/QTBUG-122118) QML Camera Application Example does not work with
Android 11 device
* [QTBUG-119472](https://bugreports.qt.io/browse/QTBUG-119472) Camera with ffmpeg backend freezes the application
* [QTBUG-125397](https://bugreports.qt.io/browse/QTBUG-125397) [gstreamer] setPlaybackRate has no effect before play()
* [QTBUG-125552](https://bugreports.qt.io/browse/QTBUG-125552) Document dynamic linking of FFmpeg with Qt Multimedia on
macOS and Windows
* [QTBUG-125213](https://bugreports.qt.io/browse/QTBUG-125213) Flaky crashes on ASAN-compiled tst_qsoundeffect
* [QTBUG-119102](https://bugreports.qt.io/browse/QTBUG-119102) Cannot record video using QML or widgets camera example
on macOS with built-in camera or iOS device continuity camera
* [QTBUG-124537](https://bugreports.qt.io/browse/QTBUG-124537) YUYV format from QCamera is buggy
* [QTBUG-124534](https://bugreports.qt.io/browse/QTBUG-124534) heap overflow in planarYUV420_to_ARGB32
* [QTBUG-123749](https://bugreports.qt.io/browse/QTBUG-123749) QVideoFrame::toImage gives corrupt images when no RHI
backend is present
* [QTBUG-123451](https://bugreports.qt.io/browse/QTBUG-123451) Incorrect frame rate selectiion for QCamera on iOS
* [QTBUG-123220](https://bugreports.qt.io/browse/QTBUG-123220) Green Line Artifact in QML VideoOutput component
* [QTBUG-126203](https://bugreports.qt.io/browse/QTBUG-126203) [darwin] MediaPlayer does not always take into account
the selected audio output device
* [QTBUG-122140](https://bugreports.qt.io/browse/QTBUG-122140) The video freezes when recording it with higher
resolution in widgets camera example
* [QTBUG-124396](https://bugreports.qt.io/browse/QTBUG-124396) [Boot2Qt] "The wayland connection broke" when running
audioooutput example app
* [QTBUG-124925](https://bugreports.qt.io/browse/QTBUG-124925) [REG 6.5.5 -> 6.5.6] Spectrum App Crashes after
recording sound in "Record and Playback" Mode
* [QTBUG-110285](https://bugreports.qt.io/browse/QTBUG-110285) Deadlock in QAndroidCamera destruction
* [QTBUG-118571](https://bugreports.qt.io/browse/QTBUG-118571) Android tests on CI part 1/3 (camera & media
capture/player)
* [QTBUG-126254](https://bugreports.qt.io/browse/QTBUG-126254) [darwin] Camera example crashes when recording with
webcam, "AudioChannelLayout is invalid"
* [QTBUG-126988](https://bugreports.qt.io/browse/QTBUG-126988) [macOS] QAudioSource::start returns invalid pointer if
start failed
* [QTBUG-122104](https://bugreports.qt.io/browse/QTBUG-122104) Missing Info.plist in audio devices example does not
allow using the application on macOS
* [QTBUG-126428](https://bugreports.qt.io/browse/QTBUG-126428) Android: Regression with playing video (H.264)
* [QTBUG-124206](https://bugreports.qt.io/browse/QTBUG-124206) [GStreamer]
tst_QAudioDecoderBackend::play_emitsFormatError_whenMediaHasNoAudioTrack
does not report errors
* [QTBUG-116766](https://bugreports.qt.io/browse/QTBUG-116766) [Boot2Qt] List of cameras should contain only available
(connected) ones
* [QTBUG-127675](https://bugreports.qt.io/browse/QTBUG-127675) Spurious assertion failure in
tst_QSoundEffect::testSetSourceWhilePlaying
* [QTBUG-127320](https://bugreports.qt.io/browse/QTBUG-127320) QMediaPlayer unable to open files with absolute paths
without scheme
* [QTBUG-128246](https://bugreports.qt.io/browse/QTBUG-128246) QMultimedia UYVY rendering is in lower image quality
* [QTBUG-128759](https://bugreports.qt.io/browse/QTBUG-128759) [REG 6.7.2->6.7.3] change in configure options,
gstreamer on LoA
* [QTBUG-125901](https://bugreports.qt.io/browse/QTBUG-125901) IOCTL  call on VIDIOC_ENUM_FRAMEINTERVALS fails to
enumarate frame interval/rate for FFmpeg V4L2 cameras
* [QTBUG-128159](https://bugreports.qt.io/browse/QTBUG-128159) QFFmpegMediaPlayer setMedia assert failure
* [QTBUG-112259](https://bugreports.qt.io/browse/QTBUG-112259) QCameraFocus doesn't work properly on iOS
* [QTBUG-124501](https://bugreports.qt.io/browse/QTBUG-124501) [gstreamer] media player does not play without outputs
connected
* [QTBUG-125251](https://bugreports.qt.io/browse/QTBUG-125251) [gstreamer] spurious assertion failure on shutdown
* [QTBUG-123931](https://bugreports.qt.io/browse/QTBUG-123931) With gstreamer as backend, playing mp4 file resulted in
internal data stream error
* [QTBUG-113399](https://bugreports.qt.io/browse/QTBUG-113399) QVideoSink with Qt 6 on Android ignores requested camera
settings
* [QTBUG-124725](https://bugreports.qt.io/browse/QTBUG-124725) [Camera] The video recorded with webcam on macOS is
corrupted - it only displays green flashing noise
* [QTBUG-125613](https://bugreports.qt.io/browse/QTBUG-125613) Investigate lacking video format support on Android 14
with FFmpeg media player
* [QTBUG-117888](https://bugreports.qt.io/browse/QTBUG-117888) Wide camera is not supported?
* [QTBUG-126143](https://bugreports.qt.io/browse/QTBUG-126143) QMediaFormat on Linux does not show MP3
* [QTBUG-122757](https://bugreports.qt.io/browse/QTBUG-122757) FFmpeg+Intel VAAPI decoding of certain h264/mp4 videos
fails in 6.6.x+
* [QTBUG-126799](https://bugreports.qt.io/browse/QTBUG-126799) [gstreamer] playback rate / seeking unreliable
* [QTBUG-123056](https://bugreports.qt.io/browse/QTBUG-123056) GStreamer: `setLoops` sometimes not working
* [QTBUG-127031](https://bugreports.qt.io/browse/QTBUG-127031) [QMediaPlayer] switching video output while playback is
paused does not update new sink
* [QTBUG-127346](https://bugreports.qt.io/browse/QTBUG-127346) [gstreamer] QMediaPlayer: subsequent playback broken
* [QTBUG-127484](https://bugreports.qt.io/browse/QTBUG-127484) CMake Error if gstreamer_gl_wayland (or gl_x11) feature
is enabled
* [QTBUG-126014](https://bugreports.qt.io/browse/QTBUG-126014) [ffmpeg] setVideoOutput/setAudioOutput while playing
seems broken
* [QTBUG-95952](https://bugreports.qt.io/browse/QTBUG-95952) Seemingly unnecessary check for pulse-mainloop-glib
* [QTBUG-127137](https://bugreports.qt.io/browse/QTBUG-127137) [ffmpeg, macos]
tst_QMediaPlayerBackend::stressTest_setupAndTeardown crashes on CI
* [QTBUG-127927](https://bugreports.qt.io/browse/QTBUG-127927) [gstreamer] record_video_without_preview assertion
failure on CI
* [QTBUG-118594](https://bugreports.qt.io/browse/QTBUG-118594)  QML Camera wrong Orientation on iOS
* [QTBUG-128336](https://bugreports.qt.io/browse/QTBUG-128336) Camera widget example does not record audio with default
AAC format
* [QTBUG-118877](https://bugreports.qt.io/browse/QTBUG-118877) -qreal float configuration option does not compile

### qttools
* [QTBUG-125066](https://bugreports.qt.io/browse/QTBUG-125066) Configure fails in qttools if PrintSupport is disabled
* [QTBUG-125310](https://bugreports.qt.io/browse/QTBUG-125310) tst_lupdate asserts on mingw13
* [QTBUG-119469](https://bugreports.qt.io/browse/QTBUG-119469) Targets not yet defined: zstd::libzstd_static
* [QTBUG-127146](https://bugreports.qt.io/browse/QTBUG-127146) [REG 5.15 -> 6.0] TR_EXCLUDE became too strict
* [QTBUG-126139](https://bugreports.qt.io/browse/QTBUG-126139) Linguist shipped with Qt6 breaks how language tag is
handled
* [QTBUG-27936](https://bugreports.qt.io/browse/QTBUG-27936) Regression: lupdate is very very slow
* [QTBUG-124200](https://bugreports.qt.io/browse/QTBUG-124200) Linguist 'does not know the plural rules for Luganda'
* [QTBUG-127513](https://bugreports.qt.io/browse/QTBUG-127513) qttool: depends on network-support, but should only be
optional
* [PYSIDE-2863](https://bugreports.qt.io/browse/PYSIDE-2863) pyside6-lupdate do not attribute comment to corresponding
text
* [QTBUG-119429](https://bugreports.qt.io/browse/QTBUG-119429) Top flaky test: tst_lupdate::good on Windows_11_22H2,
Windows_11_23H2, and Windows_10_22H2.

### qtdoc
* [QTBUG-124844](https://bugreports.qt.io/browse/QTBUG-124844) Invalid plural form qsTr example
* [QTBUG-126104](https://bugreports.qt.io/browse/QTBUG-126104) Android mobile examples link redirects to WASM page
* [QTBUG-122683](https://bugreports.qt.io/browse/QTBUG-122683) Update trademark information
* [QTBUG-127547](https://bugreports.qt.io/browse/QTBUG-127547) The link in INTEGRITY doc leads to Qt for wasm doc
* [QTBUG-127708](https://bugreports.qt.io/browse/QTBUG-127708) The Writing Source Code for Translation documentation
references undefined _NoOp functions
* [QTBUG-124657](https://bugreports.qt.io/browse/QTBUG-124657) qsTrNoOp() is not defined in QML
* [QTBUG-118038](https://bugreports.qt.io/browse/QTBUG-118038) Qt6WaylandCompositor could not be found because
dependency Wayland could   not be found
* [QTBUG-127926](https://bugreports.qt.io/browse/QTBUG-127926) Outdated Android docs still refer to
QtAndroid::androidActivity()

### qtsensors
* [QTBUG-110806](https://bugreports.qt.io/browse/QTBUG-110806) license discrepency?

### qtconnectivity
* [QTBUG-124650](https://bugreports.qt.io/browse/QTBUG-124650) Missing BLE 5.x Extended Advertisements for Windows
* [QTBUG-123430](https://bugreports.qt.io/browse/QTBUG-123430) QBluetoothSocket::errorOccured is not emitted in certain
circumstances

### qtwayland
* [QTBUG-124502](https://bugreports.qt.io/browse/QTBUG-124502) Drag and drop operation can crash the compositor
* [QTBUG-125878](https://bugreports.qt.io/browse/QTBUG-125878) Cannot pinch-to-zoom after the qt 6.7.1 upgrade
[regression]
* [QTBUG-126313](https://bugreports.qt.io/browse/QTBUG-126313) QScroller gesture blocks mouse clicks
* [QTBUG-113404](https://bugreports.qt.io/browse/QTBUG-113404) Wayland: Gestures are not delivered to correct top level
widget
* [QTBUG-122197](https://bugreports.qt.io/browse/QTBUG-122197) QScreen::size is wrong on GNOME Wayland with 200%
scaling
* [QTBUG-127301](https://bugreports.qt.io/browse/QTBUG-127301) Clipboard cannot be changed from compositor if client
has copied something
* [QTBUG-128350](https://bugreports.qt.io/browse/QTBUG-128350) QWaylandBufferRef::toOpenGLTexture leaks textures
* [QTBUG-125589](https://bugreports.qt.io/browse/QTBUG-125589) weired console message with simple application

### qt3d
* [QTBUG-124658](https://bugreports.qt.io/browse/QTBUG-124658) QAbstractCameraController documentation contains
mistakes

### qtimageformats
* [QTBUG-127540](https://bugreports.qt.io/browse/QTBUG-127540) WebP: QImage detach in WebPPictureImportRGB(A) can cause
a crash

### qtserialport
* [QTBUG-128748](https://bugreports.qt.io/browse/QTBUG-128748) Unused static functions in qserialport_p.h

### qtwebsockets
* [QTBUG-120492](https://bugreports.qt.io/browse/QTBUG-120492) QWebSocket connecting to an URL without a path sends GET
request without leading /

### qtwebchannel
* [QTBUG-116314](https://bugreports.qt.io/browse/QTBUG-116314) qmlsc: WebChannel qmltypes file issue

### qtwebengine
* [QTBUG-114339](https://bugreports.qt.io/browse/QTBUG-114339) FAIL!  : qmltests::WebEngineViewSingleFileUpload::test_a
cceptSingleFileSelection(test.txt)
* [QTBUG-113704](https://bugreports.qt.io/browse/QTBUG-113704) Sending certain key events to QQuickView showing a
focused QtWebEngine causes crash
* [QTBUG-114457](https://bugreports.qt.io/browse/QTBUG-114457) REG [6.5.2 & early 6.6.0 snapshot -> 6.6.0 beta1/FF]
namespace build fails on linux, Webengine
* [QTBUG-113992](https://bugreports.qt.io/browse/QTBUG-113992) QTWebEngine crash when not working proxy is set
* [QTBUG-113981](https://bugreports.qt.io/browse/QTBUG-113981) QPdfView does not scroll reliably with mouse wheel event
(two finger sliding on touchpad)
* [QTBUG-63021](https://bugreports.qt.io/browse/QTBUG-63021) add Window 10 compatible manifest to examples
* [QTBUG-113251](https://bugreports.qt.io/browse/QTBUG-113251) [REG 6.4 -> 6.5] Context menu functionality in devtools
broken
* [QTBUG-103518](https://bugreports.qt.io/browse/QTBUG-103518) QML WebView scrolling events are picked up by
DragHandler and Flickables behind it
* [QTBUG-115129](https://bugreports.qt.io/browse/QTBUG-115129) Backport Security patches from Chrome 113 to 112-based
* [QTBUG-115033](https://bugreports.qt.io/browse/QTBUG-115033) QtWebEngine uses invalid cmake arguments for file()
* [QTBUG-105053](https://bugreports.qt.io/browse/QTBUG-105053) qtwebengine 6.3.1 fails to link against system nss
* [QTBUG-111225](https://bugreports.qt.io/browse/QTBUG-111225) Host include paths from pkg-config not used when
FEATURE_webengine_system_icu=On when cross-compiling
* [QTBUG-114939](https://bugreports.qt.io/browse/QTBUG-114939) Qt WebEngine Geolocation broken in 6.6
* [QTBUG-114953](https://bugreports.qt.io/browse/QTBUG-114953) PdfMultiPageView: Very poor memory performance when
zooming in/out of long documents
* [QTBUG-113512](https://bugreports.qt.io/browse/QTBUG-113512)  WebEngineView not visible in Designer on macOS
* [QTBUG-114471](https://bugreports.qt.io/browse/QTBUG-114471) Recipe browser starts in upside down mode
* [QTBUG-115369](https://bugreports.qt.io/browse/QTBUG-115369) QWebEngine can not render page content and throw `Fatal
error` in console
* [QTBUG-114875](https://bugreports.qt.io/browse/QTBUG-114875) Cannot detect Visual Studio when configuring QPdf and
QWebEngine
* [QTBUG-115476](https://bugreports.qt.io/browse/QTBUG-115476) QPdfPageSelector doesn't actually handle non-numeric
page label input
* [QTBUG-115713](https://bugreports.qt.io/browse/QTBUG-115713) [REG 6.6.0 beta2->beta3] QtPDF and QtWebengine not
compiling from sources on MSVC2019
* [QTBUG-115365](https://bugreports.qt.io/browse/QTBUG-115365) QWebEngineCertificateError is exported twice
* [QTBUG-115844](https://bugreports.qt.io/browse/QTBUG-115844) qtwebengine ignores some key remaps
* [QTBUG-115976](https://bugreports.qt.io/browse/QTBUG-115976) Dev tools not hidden with closing cross
* [QTBUG-111541](https://bugreports.qt.io/browse/QTBUG-111541) QWebEngineProfile::clearHttpCache() can subsequently
cause QWebEnginePage::load() to hang
* [QTBUG-99555](https://bugreports.qt.io/browse/QTBUG-99555) [RE: 6.2.1->6.2.2] macdeployqt fails to produce
notarizable packages
* [QTBUG-115703](https://bugreports.qt.io/browse/QTBUG-115703) QtWebEngine 6.6.0 crashes on Windows
* [QTBUG-116042](https://bugreports.qt.io/browse/QTBUG-116042) configure fails when BUILDDIR path contains "++"
* [QTBUG-116278](https://bugreports.qt.io/browse/QTBUG-116278) [REG 6.6.0 beta2-> beta3] QtWebengine not compiling on
macOS11
* [QTBUG-73994](https://bugreports.qt.io/browse/QTBUG-73994) Changing input method with shortcut key causes hang on
WebEngine
* [QTBUG-116839](https://bugreports.qt.io/browse/QTBUG-116839) [B2Qt 6.6.0-beta4 snapshot] qtpdf and qtwebgine missing
from imx8qmmek and jetson-agx-xavier-devkit
* [QTBUG-116159](https://bugreports.qt.io/browse/QTBUG-116159) Reg 6.4->6.5 QWebView with Q3DSurfaces does not renders
* [QTBUG-115722](https://bugreports.qt.io/browse/QTBUG-115722) [REG 6.6.0 beta2->beta3] QtWebengine not compiling from
sources on SLES15_SP4
* [QTBUG-116738](https://bugreports.qt.io/browse/QTBUG-116738) qtwebengine Address Sanitizer test run: stack-use-after-
return in tst_QQuickWebEngineView::savePage(SingleHtmlSaveFormat)
* [QTBUG-116445](https://bugreports.qt.io/browse/QTBUG-116445) [REG][Windows] Crash on
NativeSkiaOutputDevice::releaseTexture() with nullptr access
* [QTBUG-115994](https://bugreports.qt.io/browse/QTBUG-115994) Duplicate character when long-pressing for accented char
on macOS/webengine
* [QTBUG-115753](https://bugreports.qt.io/browse/QTBUG-115753) ERROR: AddressSanitizer: heap-use-after-free  in
tst_origins
* [QTBUG-117119](https://bugreports.qt.io/browse/QTBUG-117119) Some Qt WebEngine documentation issues
* [QTBUG-117489](https://bugreports.qt.io/browse/QTBUG-117489) [REG 6.4 -> 6.5] Invalid QDataStream data when
serializing uninited QWebEngineHistory
* [QTBUG-117031](https://bugreports.qt.io/browse/QTBUG-117031) qmllint: Missing type information for WebEngine
* [QTBUG-117658](https://bugreports.qt.io/browse/QTBUG-117658) QWebEnginePage property url is missing NOTIFY, not-
usable from QML
* [QTBUG-118505](https://bugreports.qt.io/browse/QTBUG-118505) REG: Qt WebEngine debug-and-release builds broken on
macOS.
* [QTBUG-117751](https://bugreports.qt.io/browse/QTBUG-117751) building with -no-opengl produces errors in
web_engine_context.cpp
* [QTBUG-117867](https://bugreports.qt.io/browse/QTBUG-117867) QWebEngineNewWindowRequest::openIn() breaks page
interceptor
* [QTBUG-117741](https://bugreports.qt.io/browse/QTBUG-117741) libvpx is not used
* [QTBUG-118455](https://bugreports.qt.io/browse/QTBUG-118455) Crash in Compositor::Observer::compositor() with nullptr
access
* [QTBUG-118655](https://bugreports.qt.io/browse/QTBUG-118655) Manual Deployment document of QtWebengine needs little
update.
* [QTBUG-119023](https://bugreports.qt.io/browse/QTBUG-119023) WebEngine accessibility crash when clicking on a link in
a list on macOS
* [QTBUG-113859](https://bugreports.qt.io/browse/QTBUG-113859) [REG 6.4->6.5] Accessibility crash when clicking on a
link in a list on macOS
* [QTBUG-119525](https://bugreports.qt.io/browse/QTBUG-119525) error: field ‘responseHeaders’ has incomplete type
‘QMultiMap<QByteArray, QByteArray>’
* [QTBUG-115357](https://bugreports.qt.io/browse/QTBUG-115357) qt 6.5.2 fails to build from source with system libpng
(regression from 6.5.1)
* [QTBUG-119536](https://bugreports.qt.io/browse/QTBUG-119536) Lack of documentation regarding QPdfBookmarkModel's
document property
* [QTBUG-118995](https://bugreports.qt.io/browse/QTBUG-118995) Dev tools not working
* [QTBUG-119789](https://bugreports.qt.io/browse/QTBUG-119789) [Accessibility] Qt 6.5.3 cannot be built with the option
' -no-feature-accessibility''.
* [QTBUG-112142](https://bugreports.qt.io/browse/QTBUG-112142) [Qt WebEngine] ScreenCapture should provide a way to
select window/screen to capture
* [QTBUG-86869](https://bugreports.qt.io/browse/QTBUG-86869) Unrecognized Chrome version when using Selenium and
Chromedriver
* [QTBUG-118398](https://bugreports.qt.io/browse/QTBUG-118398) QWebEngineView in QScrollArea is not scrollable
* [QTBUG-118120](https://bugreports.qt.io/browse/QTBUG-118120) qtwebengine: build failure with x86_64h
* [QTBUG-119776](https://bugreports.qt.io/browse/QTBUG-119776) PDF Multipage viewer example - Clicking on previous
(upward arrow) will crash the example
* [QTBUG-120446](https://bugreports.qt.io/browse/QTBUG-120446) Alternated item color in list is not always alternated
* [QTBUG-119722](https://bugreports.qt.io/browse/QTBUG-119722) [REG 5 → 6] Default context menu is missing icons
* [QTBUG-104766](https://bugreports.qt.io/browse/QTBUG-104766) QtQuick.Pdf PdfDocument gets
"QCoreApplication::postEvent: Unexpected null receiver" warning when
instantiated standalone
* [QTBUG-120245](https://bugreports.qt.io/browse/QTBUG-120245) A crash occurred in C:\Users\qt\work\qt\qtwebengine_stan
dalone_tests\tests\auto\pdfquick\multipageview\tst_multipageview.exe
* [QTBUG-104767](https://bugreports.qt.io/browse/QTBUG-104767) Using PdfPageImage instead of Image on PDF file results
in EXC_BAD_ACCESS (SIGSEGV)
* [QTBUG-119245](https://bugreports.qt.io/browse/QTBUG-119245) Qt Web Engine alert quotes not working
* [QTBUG-83338](https://bugreports.qt.io/browse/QTBUG-83338) Default implementations of javaScriptAlert/Confirm/Prompt
treat message as rich text
* [QTBUG-119991](https://bugreports.qt.io/browse/QTBUG-119991) Unable to print at all if the first page of multi page
document is not printed
* [QTBUG-118746](https://bugreports.qt.io/browse/QTBUG-118746) Japanese input on macOS regressed in Qt 6.5.3
* [QTBUG-120218](https://bugreports.qt.io/browse/QTBUG-120218) QML WebEngineView.printToPdf(): paper formats are wrong
in the resulting document
* [QTBUG-115502](https://bugreports.qt.io/browse/QTBUG-115502) PdfMultiPageView: repeated pinch-zooming jumps to wrong
zoom level
* [QTBUG-121564](https://bugreports.qt.io/browse/QTBUG-121564) tst_MultiPageView::pinchDragPinch is flaky
* [QTBUG-121502](https://bugreports.qt.io/browse/QTBUG-121502) crash in QPdfIOHandler if document is deleted too early
* [QTBUG-119416](https://bugreports.qt.io/browse/QTBUG-119416) Loading a specific page in a PDF document does not
always show the correct page
* [QTBUG-
120689](https://bugreports.qt.io/browse/QTBUG-120689) tst_qwebenginepage::getUserMediaRequestDesktopVideoManyPages is
flaky
* [QTBUG-120273](https://bugreports.qt.io/browse/QTBUG-120273) QWebEngineView shows blank content on initial show when
page bg set to transparent
* [QTBUG-121227](https://bugreports.qt.io/browse/QTBUG-121227) QWebEngineView shows blank content on initial show when
page bg set to transparent
* [QTBUG-112013](https://bugreports.qt.io/browse/QTBUG-112013) QWebEnginePage.setBackground(Qt::black) doesn't work for
page loading.
* [QTBUG-120926](https://bugreports.qt.io/browse/QTBUG-120926) QWebEnginePage::setBackgroundColor doesn't work properly
* [QTBUG-122153](https://bugreports.qt.io/browse/QTBUG-122153) QWebEngineView::setFocus() doesn't give focus to the
view after calling QWebEngineView::load() for the second time
* [QTBUG-122137](https://bugreports.qt.io/browse/QTBUG-122137) REG: QtWebEngine / Pdfwidgets no longer supports plugins
* [QTBUG-121589](https://bugreports.qt.io/browse/QTBUG-121589) Can't build qt6 due to failed ozone platform assertion
* [QTBUG-118035](https://bugreports.qt.io/browse/QTBUG-118035) QtWebengine build fails on pure wayland
* [QTBUG-122997](https://bugreports.qt.io/browse/QTBUG-122997) The Spellcheck example doesn't work on macOS
* [QTBUG-123548](https://bugreports.qt.io/browse/QTBUG-123548) PDF multipage viewer converts a simple local filename in
the cwd to an http url
* [QTBUG-122655](https://bugreports.qt.io/browse/QTBUG-122655) 6.8.0 toplevel build fails on macOS, qtwebengine
* [QTBUG-120764](https://bugreports.qt.io/browse/QTBUG-120764) PDF Viewer Widget example search error
* [QTBUG-106565](https://bugreports.qt.io/browse/QTBUG-106565) The coordinate of QPdfSelection seems like to be wrong
when pdf page contains non-displayable area
* [QTBUG-100630](https://bugreports.qt.io/browse/QTBUG-100630) PdfLinkModel don't give the right rect everytime
* [QTBUG-124527](https://bugreports.qt.io/browse/QTBUG-124527) qtwebengine integrations fail on 6.7: qt-testrunner.py
ERROR: Full test run failed repeatedly, aborting!
* [QTBUG-124375](https://bugreports.qt.io/browse/QTBUG-124375) Qt Webengine spellcheck_buildflags.h not found on macOS
* [QTBUG-122916](https://bugreports.qt.io/browse/QTBUG-122916) Print preview: crash when pressing a resize button
* [QTBUG-123765](https://bugreports.qt.io/browse/QTBUG-123765) Segfault when dropping elements from Spotify in Firefox
* [QTBUG-124353](https://bugreports.qt.io/browse/QTBUG-124353) [REG 6.5.3 - 6.6.0] Massive memory leak on WebEngineView
resizing
* [QTBUG-123536](https://bugreports.qt.io/browse/QTBUG-123536) PdfPageView documentation page features PdfMultiPageView
in examples
* [QTBUG-92114](https://bugreports.qt.io/browse/QTBUG-92114) Shift-Tab moves focus forward instead of backward in
WebEngineView inside QQuickWidget
* [QTBUG-122970](https://bugreports.qt.io/browse/QTBUG-122970) Copying and pasting using shortcuts is not working in
MacOS
* [QTBUG-124747](https://bugreports.qt.io/browse/QTBUG-124747) [REG 6.7.0->6.7.1] iOS examples not compiling
* [QTBUG-124790](https://bugreports.qt.io/browse/QTBUG-124790) QtWebengine 6.8 (dev) doesn't render with basic html
files
* [QTBUG-124635](https://bugreports.qt.io/browse/QTBUG-124635) [REG 6.7.0->6.7.1] WebEngine does not render anything on
embedded
* [QTBUG-124506](https://bugreports.qt.io/browse/QTBUG-124506) [Qt PDF] Multiple definition error for static builds
* [QTBUG-121359](https://bugreports.qt.io/browse/QTBUG-121359) QtWebEngineView crashes when scrolling using the
touchpad.
* [QTBUG-125452](https://bugreports.qt.io/browse/QTBUG-125452) QT_FEATURE_webengine_system_icu=ON results in broken
runtime
* [QTBUG-126138](https://bugreports.qt.io/browse/QTBUG-126138) Correct QML PdfSelection documentation
* [QTBUG-126401](https://bugreports.qt.io/browse/QTBUG-126401) Qt webengine leaks its WebEngineQuickWidget
* [QTBUG-125035](https://bugreports.qt.io/browse/QTBUG-125035) Webengine: issues compiling with ninja 1.12
* [QTBUG-126722](https://bugreports.qt.io/browse/QTBUG-126722) WebEngine: GPU detection is missing "VmWare" in vendor
list
* [QTBUG-127318](https://bugreports.qt.io/browse/QTBUG-127318) QWebEngineView findText does not clear previous
findText's highlight results at certain conditions
* [QTBUG-111927](https://bugreports.qt.io/browse/QTBUG-111927) Link hovering may not change cursor shape in web view
* [QTBUG-123889](https://bugreports.qt.io/browse/QTBUG-123889) Qt webengine doesn't update cursor properly when
entering/leaving widgets
* [QTBUG-115929](https://bugreports.qt.io/browse/QTBUG-115929) [REG 6.3 -> 6.4/.5] Mouse cursor is pointer-only when
leaving window at bottom edge
* [QTBUG-124878](https://bugreports.qt.io/browse/QTBUG-124878) --no-sandbox through command line does not seem to have
any effect
* [QTBUG-124274](https://bugreports.qt.io/browse/QTBUG-124274) WebEngine build fails on openSUSE 15 due to libre2
* [QTBUG-125300](https://bugreports.qt.io/browse/QTBUG-125300) Potential requirement on C runtime version for Qt 6.5.5
(and newer)?
* [QTBUG-123790](https://bugreports.qt.io/browse/QTBUG-123790) Large number of warnings are output when exiting
QWebEngineView.
* [QTBUG-128241](https://bugreports.qt.io/browse/QTBUG-128241) HTML selection tag crashes app when clicked on
* [QTBUG-113416](https://bugreports.qt.io/browse/QTBUG-113416) [Reg 6.4->6.5] Static build fails at PDF module
* [QTBUG-113551](https://bugreports.qt.io/browse/QTBUG-113551) Update documentation for limitation building QtPdf for
Android with supported  LTS versions
* [QTBUG-114367](https://bugreports.qt.io/browse/QTBUG-114367) QtPdf API review  findings
* [QTBUG-105342](https://bugreports.qt.io/browse/QTBUG-105342) Test on qemu are very flacky
* [QTBUG-85731](https://bugreports.qt.io/browse/QTBUG-85731) Screen sharing does not work on Google Meet
* [QTBUG-113369](https://bugreports.qt.io/browse/QTBUG-113369) dark mode enabled causes crashes on specific sites
* [QTBUG-104610](https://bugreports.qt.io/browse/QTBUG-104610) Does WebEngine support document download and print
operations in the document preview screen?
* [QTBUG-115188](https://bugreports.qt.io/browse/QTBUG-115188) QtWebEngine use after free in Extensions GetPreferences
* [QTBUG-113149](https://bugreports.qt.io/browse/QTBUG-113149) PDF download  from pdf viewer not working
* [QTBUG-116165](https://bugreports.qt.io/browse/QTBUG-116165) FAIL!  :
tst_QWebEnginePage::acceptNavigationRequestNavigationType()
'expectedList.size() == page.navigations.size()' returned FALSE.
* [QTBUG-100417](https://bugreports.qt.io/browse/QTBUG-100417) [REG 5.15->6.3] Multiple context menus can be opened
with synthetic touch events
* [QTBUG-113463](https://bugreports.qt.io/browse/QTBUG-113463) Build issues with symlinks
* [QTBUG-114859](https://bugreports.qt.io/browse/QTBUG-114859) When saving an mhtml page
QWebEngineDownloadRequest::isSavePageDownload() returns false
* [QTBUG-116478](https://bugreports.qt.io/browse/QTBUG-116478) [Reg 5.14.2 -> 5.15.0] Significant performance decrease
when loading QtWebEngine pages simultaneously in many windows
* [QTBUG-117624](https://bugreports.qt.io/browse/QTBUG-117624) Minor issues of QWebEngineDownloadRequest
* [QTBUG-116565](https://bugreports.qt.io/browse/QTBUG-116565) Cannot sign a WebEngine-based application with Qt 6.5.2
(but OK with Qt 6.4.3, 6.3.2, 5.15.2)
* [QTBUG-117752](https://bugreports.qt.io/browse/QTBUG-117752) QWebEngineUrlRequestInterceptor not called on page, if
the one set on the profile changed the info
* [QTBUG-118750](https://bugreports.qt.io/browse/QTBUG-118750) REG: QQuickItem::setParentItem to null triggers
tst_qmltests crash
* [QTBUG-114865](https://bugreports.qt.io/browse/QTBUG-114865) macos: Building QtWebEngine  with sanitizer enabled
fails
* [QTBUG-111873](https://bugreports.qt.io/browse/QTBUG-111873) qt_attributions.json files should be valid JSON
* [QTBUG-117707](https://bugreports.qt.io/browse/QTBUG-117707) MinGW 13.1.0: FAILED:
obj/third_party/icu/bundled_icuuc_private/putil.o
* [QTBUG-116595](https://bugreports.qt.io/browse/QTBUG-116595) QtPfd build failure on 32-bit arm
* [QTBUG-119763](https://bugreports.qt.io/browse/QTBUG-119763) [REG 6.5.2?] Rare segfaults in
QWebEngineDownloadItem::page()
* [QTBUG-119878](https://bugreports.qt.io/browse/QTBUG-119878) [Reg 5.15->6.x] Crash and/or bad output when printing
via Qt WebEngine's PDF plugin
* [QTBUG-119077](https://bugreports.qt.io/browse/QTBUG-119077) CMake deployment API does not deploy Qt Webengine
* [QTBUG-120692](https://bugreports.qt.io/browse/QTBUG-120692) Cannot cross-compile webengine for x86_64
* [QTBUG-86948](https://bugreports.qt.io/browse/QTBUG-86948) When using QImageReader to load a PDF then the PDF images
can be blurry and seem to be at half the size they should be
* [QTBUG-120420](https://bugreports.qt.io/browse/QTBUG-120420) QtWebEngine inspector crashes
* [QTCREATORBUG-30308](https://bugreports.qt.io/browse/QTCREATORBUG-30308) QtCreator is not able to debug pdb files when lib
linked with pdbpagesize
* [QTBUG-120414](https://bugreports.qt.io/browse/QTBUG-120414) Recipe Browser example crashes
* [QTBUG-122699](https://bugreports.qt.io/browse/QTBUG-122699) Failed DCHECK in v8 when watching livestream
* [QTBUG-120247](https://bugreports.qt.io/browse/QTBUG-120247) [Qt WebEngine] Make it easier to re-configure after
installing missing libraries for qpa-xcb support
* [QTBUG-124632](https://bugreports.qt.io/browse/QTBUG-124632) QtWebengine needs to be skipped with Windows 11 on ARM
* [QTBUG-120370](https://bugreports.qt.io/browse/QTBUG-120370) QQuickWebEngineDownloadItem is not public
* CVE-2024-4948: Use after free in Dawn.
* CVE-2024-5157: Use after free in Scheduling
* CVE-2024-5158: Type Confusion in V8
* CVE-2024-5159: Heap buffer overflow in ANGLE
* CVE-2024-5160: Heap buffer overflow in Dawn
* CVE-2024-5274: Type Confusion in V8
* CVE-2024-5493: Heap buffer overflow in WebRTC
* CVE-2024-5494: Use after free in Dawn
* CVE-2024-5495: Use after free in Dawn
* CVE-2024-5496: Use after free in Media Session
* CVE-2024-5499: Out of bounds write in Streams API
* CVE-2024-5831: Use after free in Dawn
* CVE-2024-5832: Use after free in Dawn
* CVE-2024-5836: Inappropriate Implementation in DevTools
* CVE-2024-5840: Policy Bypass in CORS
* CVE-2024-5841: Use after free in V8
* CVE-2024-5845: Use after free in Audio
* CVE-2024-5846: Use after free in PDFium
* CVE-2024-5847: Use after free in PDFium
* CVE-2024-6101: Inappropriate implementation in WebAssembly
* CVE-2024-6103: Use after free in Dawn
* CVE-2024-6290: Use after free in Dawn
* CVE-2024-6291: Use after free in Swiftshader
* CVE-2024-6292: Use after free in Dawn
* CVE-2024-6293: Use after free in Dawn
* CVE-2024-6774: Use after free in Screen Capture
* CVE-2024-6777: Use after free in Navigation
* CVE-2024-6779: Out of bounds memory access in V8
* CVE-2024-6989: Use after free in Loader
* CVE-2024-6991: Use after free in Dawn
* CVE-2024-6992: Out of bounds memory access in ANGLE
* CVE-2024-6996: Race in Frames
* CVE-2024-6999: Inappropriate implementation in FedCM
* CVE-2024-7000: Use after free in CSS
* CVE-2024-7532: Out of bounds memory access in ANGLE
* CVE-2024-7535: Inappropriate implementation in V8
* CVE-2024-7536: Use after free in WebAudio
* CVE-2024-7550: Type Confusion in V8
* CVE-2024-7965: Inappropriate implementation in V8
* CVE-2024-7966: Out of bounds memory access in Skia
* CVE-2024-7969: Type Confusion in V8
* CVE-2024-7971: Type confusion in V8
* CVE-2024-7972: Inappropriate implementation in V8
* CVE-2024-7974: Insufficient data validation in V8 API
* CVE-2024-7975: Inappropriate implementation in Permissions
* CVE-2024-7973: Heap buffer overflow in PDFium
* CVE-2024-7967: Heap buffer overflow in Fonts
* CVE-2024-8193: Heap buffer overflow in Skia
* CVE-2024-8198: Heap buffer overflow in Skia
* CVE-2024-8636: Heap buffer overflow in Skia
* CVE-2024-8362: Use after free in WebAudio
* CVE-2024-8905: Inappropriate implementation in V8
* CVE-2024-9120: Use after free in Dawn
* CVE-2024-9122: Type Confusion in V8
* CVE-2024-9123: Integer overflow in Skia
* CVE-2024-45492 / Security bug 364778067
* Security bug 329693878
* Security bug 329699609
* Security bug 333453962
* Security bug 338574384
* Security bug 339736513
* Security bug 336214779
* Security bug 356649155
* Security bug 340606786
* Security bug 340822365
* Security bug 340895241
* Security bug 341640868
* Security bug 343000522
* Security bug 345261068
* Security bug 346197738
* Security bug 346686148
* Security bug 346799730
* Security bug 348473836
* Security bug 349248170
* Security bug 349517592
* Security bug 352424865
* Security bug 351876778
* Security bugs 40063014 and 40068800

### qtwebview
* [QTBUG-70166](https://bugreports.qt.io/browse/QTBUG-70166) iOS Webview not able to return an object

### qtvirtualkeyboard
* [QTBUG-127120](https://bugreports.qt.io/browse/QTBUG-127120) CMake error in qtvirtualkeyboard: CMake Error: The
inter-target dependency graph contains the following strongly connected
component (cycle)
* [QTBUG-114551](https://bugreports.qt.io/browse/QTBUG-114551) [VKB] Selection handle coordinates fail to take
InputPanel's parent's transformation into account

### qtnetworkauth
* [QTBUG-124333](https://bugreports.qt.io/browse/QTBUG-124333) [OAuth] Ability to open and close the loopback HTTP
server on a need-basis
* [QTBUG-66415](https://bugreports.qt.io/browse/QTBUG-66415) Access token callback clears scope
* [QTBUG-104655](https://bugreports.qt.io/browse/QTBUG-104655) QAbstractOAuth2::setState doesn't work as expected

### qtremoteobjects
* [QTBUG-139754](https://bugreports.qt.io/browse/QTBUG-139754) FAIL!  : tst_clientSSL::testRun()
'socketClient->waitForEncrypted(-1)' returned FALSE

### qtquick3d
* [QTBUG-125875](https://bugreports.qt.io/browse/QTBUG-125875) Manual test modelblendparticles segfaults on startup
* [QTBUG-125876](https://bugreports.qt.io/browse/QTBUG-125876) Instanced models are not taken into account in shadow
mapping bounds
* [QTBUG-127413](https://bugreports.qt.io/browse/QTBUG-127413) Building failure with FEATURE_quick_shadereffect=OFF
* [QTBUG-119888](https://bugreports.qt.io/browse/QTBUG-119888) Texts overlap with each other in Qt Quick3D
* [QTBUG-128370](https://bugreports.qt.io/browse/QTBUG-128370) Instance table cache not invalidated when instance table
is deleted

### qt5compat
* [QTBUG-122795](https://bugreports.qt.io/browse/QTBUG-122795) Incompatibility in QTextCodec between Qt5 and Qt6 (lack
of BOM)

### qthttpserver
* [QTBUG-127333](https://bugreports.qt.io/browse/QTBUG-127333) FAIL! :
tst_QHttpServerResponse::mimeTypeDetection(image/svg+xml) Compared
values are not the same

### qtquick3dphysics
* [QTBUG-127319](https://bugreports.qt.io/browse/QTBUG-127319) Add command line help for cooker
* [QTBUG-100100](https://bugreports.qt.io/browse/QTBUG-100100) Demos should use `qt6_add_qml_module` instead of
`qt6_add_resources`

### qtquickeffectmaker
* [QTBUG-111760](https://bugreports.qt.io/browse/QTBUG-111760) target_link_libraries(foo INTERFACE Qt::Core) fails for
interface libs with CMake < 3.19 on Windows

Known Issues
------------

* Check that your system meets Qt's requirements:
https://doc.qt.io/qt-6.5/supported-platforms.html

* The RTA (release test automation) reported issues in Qt 6.5.x:
https://qt-project.atlassian.net/issues/?filter=15085

* See Qt 6.5 known issues from:
https://wiki.qt.io/Qt_6.5_Known_Issues

* Qt 6.5.7 Open issues in Jira:
https://qt-project.atlassian.net/issues/?filter=10266

Credits for the release goes to:
---------------------------------

Eirik Aavitsland  
Amir Masoud Abdol  
Laszlo Agocs  
Yigit Akcay  
Konsta Alajärvi  
Anu Aliyas  
Even Oscar Andersen  
Viktor Arvidsson  
Karolina Sofia Bang  
Mate Barany  
Vladimir Belyavsky  
Nicholas Bennett  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
Tatiana Borisova  
Joerg Bornemann  
Rym Bouabid  
Assam Boudjelthia  
Michael Brüning  
Olivier De Cannière  
Alexei Cazacov  
Kaloyan Chehlarski  
Ed Cooke  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Szabolcs David  
Pavel Dubsky  
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
Nazar Gerasymchuk  
Mikko Gronoff  
Magnus Groß  
Kaj Grönholm  
Richard Moe Gustavsen  
Lucie Gérard  
Mikko Hallamaa  
Jøger Hansegård  
Jani Heikkinen  
Moss Heim  
Ulf Hermann  
Volker Hilsheimer  
Dominik Holland  
Allan Sandfeld Jensen  
Jonas Karlsson  
Igor Khanin  
Ahmed El Khazari  
Friedemann Kleint  
Michal Klocek  
Jarek Kobus  
Tobias Koenig  
Sze Howe Koh  
Jarkko Koivikko  
Fabian Kosmale  
Mike Krus  
Santhosh Kumar  
Kai Köhne  
Inho Lee  
Kimmo Leppälä  
Thiago Macieira  
Andras Mantia  
Safiyyah Moosa  
Bartlomiej Moskal  
Marc Mutz  
Antti Määttä  
Jithin Nair  
Martin Negyokru  
Andy Nichols  
Mårten Nordheim  
Samuli Piippo  
Timur Pocheptsov  
Lauri Pohjanheimo  
Rami Potinkara  
Shyamnath Premnadh  
MohammadHossein Qanbari  
Liang Qi  
Matthias Rauter  
Topi Reinio  
Shawn Rutledge  
Toni Saario  
Ahmad Samir  
Luca Di Sera  
Dmitry Shachnev  
Sami Shalayel  
Tian Shilin  
Pierre-Yves Siret  
Kristoffer Skau  
Nils Petter Skålerud  
Ivan Solovev  
Axel Spoerl  
Christian Strømme  
Tarja Sundqvist  
Lars Sutterud  
Tasuku Suzuki  
Jan Arve Sæther  
Nodir Temirkhodjaev  
Ivan Tkachenko  
Jens Trillmann  
Paul Olav Tvete  
Fatih Uzunoglu  
Tuomas Vaarala  
Sami Varanka  
Peter Varga  
Doris Verria  
Tor Arne Vestbø  
Jannis Voelker  
Juha Vuolle  
Jaishree Vyas  
Dongmei Wang  
Michael Weghorn  
Edward Welbourne  
Paul Wicking  
Piotr Wierciński  
Oliver Wolff  
Lu YaNing  
Semih Yavuz  
Wang Yu  
Vlad Zahorodnii  
JiDe Zhang  
Liu Zheng  
