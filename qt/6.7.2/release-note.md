Release note
============
Qt 6.7.2 release is a patch release made on the top of Qt 6.7.1.
As a patch release, Qt 6.7.2 does not add any new functionality but provides
bug fixes and other improvements and maintains both forward and backward
compatibility (source and binary) with Qt 6.7.1.

For detailed information about Qt 6.7, refer to the online documentation
included in this distribution. The documentation is also available online:

https://doc.qt.io/qt-6/index.html

The Qt version 6.7 series is binary compatible with the 6.6.x series.
Applications compiled for 6.6 will continue to run with 6.7.

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

### qtbase
* 0aa0d505b1 SQLite: Update identified license
Change identified license for SQLite from 'Public Domain' to more
accurate 'SQLite Blessing': https://spdx.org/licenses/blessing.html

* a8ef8ea550 Don't quit automatically via QEventLoopLocker if there are
open windows
Fixed a regression where the last QEventLoopLocker going out of scope
would quit the app, even if there were open windows, if
quitOnLastWindowClosed was false.

* bb51347266 QCoreApplication: make removeNativeEventFilter() remove
from main thread
Fixed a mismatch on which event dispatcher was modified between
installNativeEventFilter() and removeNativeEventFilter(). Now both
functions in QCoreApplication access the main thread's event dispatcher.
To access the current thread's dispatcher, use
QAbstractEventDispatcher's functions.

* 12ae2e8075 QDBusSignature: accept empty strings as valid
Fixed a bug that caused the class not to accept an empty string as a
valid D-Bus SIGNATURE value.

* d32f7dc016 Android: account for namespace in build.gradle instead of
manifest
Add support for namespace in build.gradle instead of the package
attribute in the manifest.

* febed4c265 Update bundled libjpeg-turbo to version 3.0.3
libjpeg-turbo was updated to version 3.0.3

* c4b2d2389e Cope with CLDR's "day period" format specifiers
CLDR's 'B' (flexible day period, e.g. "at night" &c.) field, not
currently supported, is now handled as a synonym for the AM/PM field
'a', instead of leaving the B as literal text. Only affects zh_TW at
present.

* 843b0b819b QVariant: do reset is_null after setValue()
Fixed a bug that would allow the class to keep returning isNull() =
true even after calling setValue().

* bf4c9bbf80 SQLite: Update SQLite to v3.46.0
Updated SQLite to v3.46.0

* 229ed81c72 QAnyStringView: fix char-ish ctors to not allocate memory
Fixed a regression where constructing a QAnyStringView from a char-like
type (QChar, QLatin1Char, ...) would first construct a QString and only
then convert that to QAnyStringView.

* a5fdbd73a9 Entrypoint/Win32: just use __argc and __argv if available
Fixed a bug that caused Qt applications to disregard Unicode command-
lines on Windows even when argc and argv were passed un- modified to
QGuiApplication or QApplication. This happened only for builds with
Visual Studio and in the "windows" subsystem (not "console").

### qtmultimedia
* 4acc4e913 Update pffft version to the latest version from upstream
Updated pffft to fbc4058.

* 85c41da64 GStreamer: add private API to access pipeline for capture
session
QMediaCaptureSession: GStreamer - private interface to access
underlying GstPipeline of QMediaCaptureSession

* 77ec6a23f ALSA: use first device as default
ALSA: use first device as default, if ALSA doesn't report a default
device.

* 0e37d823b Use correct stride factor with YUV420P10 pixel format
Fix display of videos using YUV420P10 pixel format

* 17643efb7 GStreamer: custom audio io - introduce factory functions
QAudioInput/QAudioOutput: GStreamer - add private API to customize
audio input/output via a pipeline string.

* e680faf56 Document dynamic linking of FFmpeg on macOS
Document that FFmpeg media backend links dynamically to FFmpeg
libraries on both Windows and macOS, and that applications using Qt
Multimedia with the FFmpeg media backend must deploy shared FFmpeg
libraries as part of their installers.

* 5f3a79e0f GStreamer: QGstreamerVideoSink - improve conversion element
override
QVideoSink: GStreamer - allow override of conversion element via
environment variable

### qtsensors
* a4d7405c Attribute Third-Party Code in Android Sensors Plugin
Add attribution for Android getRotationMatrix and getOrientation code,
copied from Android sources under Apache-2.0. This code is only used on
Android, as part of the Android Sensor plugin.

### qtinsighttracker (Commercial only)
* 20ac8df Add API for sending custom dimension data
Custom dimension data can now tracked without attaching it to other
events.

* d003d17 Remove deprecated APIs
Old deprecated screen view and click event APIs were removed.


Fixes
-----

### qtbase
* QTBUG-124227 Reg[6.5.4->6.5.5] looks like Gif Frame duration is
changed
* PYSIDE-2492 uic does not generate enumeration name into enum values
causing type checking warnings
* QTBUG-124538 ~QGuiGLThreadContext leaks memory
* QTBUG-124719 windeployqt picks some host arch dlls
* QTBUG-117091 Crash during updateApplicationBadge
* QTBUG-124376 Slow UI build in Release mode with MSVC
* QTBUG-124551 [macOS] App crashes on quit if the Quick Platform menu is
open
* QTBUG-123928 Not all widgets follow mode switching at runtime in the
Widget Gallery example
* QTBUG-123035 QDataStream docs give wrong examples
* QTBUG-122436 Android a11y: Changes to Accessible.ignored and
Item.visible are not propagated to the screen reader
* QTBUG-115583 Redundant declaration of QPageSize equality operator
* QTBUG-124386 [Regression] QEventLoopLocker causes application to quit
even with open windows
* QTBUG-124475 tst_QWidget::tabOrderWithProxyDisabled() crash on
Wayland(GNOME, Ubuntu 22.04)
* QTBUG-124861 HistoryCompleter popup stays on top when changing mode
* QTBUG-123939 tst_qdialogbuttonbox non-deterministic failure
* QTBUG-124262 [Reg] Crash when calling QMainWindow:.tabifiedDockWidgets
after QMainWindow::removeDockWidget
* QTBUG-124447 Doing style->drawControl(QStyle::CE_ProgressBar) inside
QStyledItemDelegate causes a crash
* QTBUG-122166 Qt Test tutorials missing a link to the source code
* QTBUG-99106 QMouseEvent always generates Qt::LeftButton events on
Android, even on right mouse click
* QTBUG-112721 QLineEdit standard menu actions do not have object names
* QTBUG-124554 QPushButton menu dropdown arrow looks odd on 100% DPI at
HD (1920x1080) resolution
* QTBUG-114539 QToolButton arrow clipped on screen with non-integer
device pixel ratio
* QTBUG-124135 qtbase/cmake produced pkg-config .pc files no longer emit
dependencies
* QTBUG-109512 Documentation of QThread::setStackSize() wrong (on Unix)
* QTBUG-124783 QCoreApplication::removeNativeEventFilter does not use
MainThread eventDispatcher
* QTBUG-125142 [REG 6.7.0->6.7.1] Can't deploy to iOS/iOS simulator:
ASSERT: "m_view.window" in file qioswindow.mm
* QTBUG-124931 Wrong aligenment for right to left languages in the main
menu with Windows 11
* QTBUG-124919 QDBusSignature considers an empty string to be an invalid
signature
* QTBUG-124286 New native style for Windows 11 ignores stylesheet in
some cases
* QTBUG-96120 zstd both found and not found
* QTBUG-96394 Misleading cmake output about missing optional packages
* QTBUG-111216 CMake configuration summary is wrong about "wrapped" zstd
(and others)
* QTBUG-125079 removed_api.cpp compile error
* QTBUG-125154 Left-clicking in QSlider in modern Windows 11 style uses
old Windows XP/Vista slider stepping behavior
* QTBUG-124608 QResource file engine returns read-only memory for some
resources even with MapPrivateOption
* QTBUG-123872 time wrongly displayed in zh_TW locale
* QTBUG-125241 fromIccProfile fails with "failed minimal tag size
sanity"
* QTBUG-125058 QtTest log QCRITICAL due to QApplication::regClass:
Registering window class 'Qt662dScreenChangeObserverWindow' failed.
(Class already exists.)
* QTBUG-123998 Top flaky test: tst_qwidget::hoverPosition on
openSUSE_15_5 X86_64, Ubuntu_22_04, QNX_710
* QTBUG-124524 QMenuBar with style override submenu all white in dark
mode and crash
* QTBUG-125472 [Reg 5.15->6.x] QVariant::isNull() can return true for
non-null values
* QTBUG-73655 QTableView Not Rendering Icons Correctly
* QTBUG-125506 [Reg 6.7.0->6.7.1] Build break with -no-feature-mdiarea
* QTBUG-125285 QKdeTheme falls back to Qt::ColorScheme::Unknown on
invalid desktop theme
* QTBUG-125222 isAutoRepeat not working for WASAM
* QTBUG-123838 QFile::moveToTrash() description incorrect
* QTBUG-114938 2dpainting example crashes on QNX
* QTBUG-125610 Constructing a QDate from std::chrono::year_month_day
results in link error
* QTBUG-120415 Unable to close Window when changing hide taskbar toggle
* QTBUG-122394 Crash when using QDockWidget
* QTBUG-102347 Qt documentation doesn't specify log level severity order
* QTBUG-125531 Unable to drag files into the xwayland widget of
QTextEdit
* QTBUG-124235 Too small minimumSizeHint for QDateEdit/QDateTimeEdit
with windows11-style
* QTBUG-124150 QAbstractSpinBox size hint miscalculated for Windows 11
style
* QTBUG-86203 Documentation on QtAndroid:androidService(),
QtAndroid:androidContext() unclear
* QTBUG-125776 The Q_OBJECT macro documentation mentions obsolete
requirements
* QTBUG-125889 tst_qfloat16::ordering - conversion of floating to
integral exercise undefined behaviour
* QTBUG-114439 No such signal
QPlatformNativeInterface::systemTrayWindowChanged(QScreen*) on Wayland
* QTBUG-94871 Qt should subscribe to dbus system tray and dbus menu
service appearing/disappearing
* QTBUG-125721 QStorageInfo::mountedDrives() not reporting mounted btrfs
subvolumes on same device as root
* QTBUG-125735 [REG 6.4→6.5] QAnyStringView(char-ish) has become slow
* QTBUG-125436 Windows ARM: HealthCheck fails - QtBase tst_QProcess
* QTBUG-125958 Numpad 5 is not mapped to Qt::Key_Clear
* QTBUG-125380 Windows command line arguments mangled by double prime
character
* QTBUG-125858 REG: Wrong result value in QMessageBox::warning detected
in version 6.7.1
* QTBUG-125120 wasm: qtvirtualkeyboard crashes on startup
* QTBUG-124723 QThread::start(Priority) should be
QThread::start(QThread::Priority)
* QTBUG-120565 Bottlenecks when compositing widgets with RHI
* QTBUG-124771 MACOS_BUNDLE_POST_BUILD generates a symlink to a non-
existent dylib for static QML plugin, fails AppStore validation
* QTBUG-121653 License clarification for unicode & unicode-cldr related
files
* QTBUG-106907 "package" attribute in AndroidManifest is deprecated
* QTBUG-125287 Android: Template args don't work for String[] using
jobjectArray
* QTBUG-118080 QDoc cannot distinguish between template function
overloads differing only  in template arguments
* QTBUG-101307 tst_qbytearrayview fails to compile with ubsan
* QTBUG-125588 QString::arg(char16_t{}) prefers the integral, not the
QChar overload
* QTBUG-125587 Cannot create DateTime from StdTimePoint
* QTBUG-119469 Targets not yet defined: zstd::libzstd_static

### qtsvg
* QTBUG-123994 [REG 6.5->6.7] QML SVG rendering in 6.7 can't render file
properly (regression)
* QTBUG-125065 [REG 6.5.3 -> 6.6.0] Null-pointer deref when loading svg
file

### qtdeclarative
* QTBUG-124521 QT_QML_GENERATE_QMLLS_INI generates wrong buildDir
* QTBUG-124730 MultiEffects Shadow in repeater causes application to
crash
* QTBUG-108696 [TapHandler] Internal warning "QObject::disconnect:
Unexpected nullptr parameter"
* QTBUG-124363 [6.7 REG] Changing QML Window visible property clobbers
window state
* QTBUG-124456 [6.4.2] Margins in QuickLayouts causing a QList exception
(index out of range)
* QTBUG-124569 Qt Quick rendering of html table borders is inconsistent
with widgets
* QTBUG-120986 QML Type TextArea or TextEdit doesn't render CSS table
and table cell border correctly
* QTBUG-113040 Quick Text: SVG inline images have poor quality on High-
DPI displays
* QTBUG-124474 The text of QML ComboBox in a Window turns invisible in
dark mode
* QTBUG-125049 SplitView jumps to an incorrect width when resizing if
another object in SplitView is not visible.
* QTBUG-125076 [Reg 6.5->6.7.0] Doc for QQuickItem no longer says
"Instantiated by: Item"
* QTBUG-125153 cmake: Deployment of shared module fails with Xcode (non-
ninja) generator during the post build step (not during installation)
* QTBUG-124771 MACOS_BUNDLE_POST_BUILD generates a symlink to a non-
existent dylib for static QML plugin, fails AppStore validation
* QTBUG-124657 qsTrNoOp() is not defined in QML
* QTBUG-124229 FAILED:
src/qmltest/CMakeFiles/QuickTest.dir/quicktest.cpp.o
* QTBUG-124357 Quick Controls are not rendered correctly when changing
OS theme
* QTBUG-125228 Customizing Quick Controls Documentation should use
Templates instead
* QTBUG-123871 qmlls crashes
* QTBUG-56921 Imperatively setting TextEdit's alignment results in
incorrectly aligned text
* QTBUG-119644 [Tests] Warnings in
qtdeclarative/tests/auto/quickcontrols/controls/data/tst_combobox.qml
* QTBUG-125393 qmllint fails when given files names with backslashes on
Windows
* QTBUG-125580 [Tests] Warnings in
tst_controls::Material::ComboBox::test_comboBoxWithShaderEffect()
* QTBUG-74331 beyond living (aka not really dead) link in colors docs
* QTBUG-124230 tst_focus::reason is failing
* QTBUG-125127 Documentation of the QML singleton: correct the snippet
for pragma Singleton
* QTBUG-125429 send array from qml to c++
* QTBUG-116577 ASSERT: "sumFactors > 0.0"  in qgridlayoutengine.cpp
* QTBUG-113384 QQuickWidget - touchpad click not working after scrolling
* QTBUG-123999 Heap buffer overflow in JS Set.delete

### qtmultimedia
* QTBUG-124414 [gstreamer] MediaPlayer emits BufferedMedia in
StoppedState
* QTBUG-124415 [gstreamer] MediaPlayer emits too many state change
signals
* QTBUG-122140 The video freezes when recording it with higher
resolution in widgets camera example
* QTBUG-124182 [gstreamer] tst_QCameraBackend::testNativeMetadata test
failure
* QTBUG-124776 [gstreamer] uridecodebin with https source spurious
playback failure
* QTBUG-124431 When using QMediaRecorder or QAudioInput with alsa it
chooses the wrong Endianess with ALSA audio
* QTBUG-124544 [gstreamer] duration is not extracted from metadata
* QTBUG-125080 [gstreamer] audio io crashes with FEATURE_alsa
* QTBUG-124615 Top flaky test: tst_qmediaplayerbackend::play_createsFram
esWithExpectedContentAndIncreasingFrameTime_whenPlayingRtspMediaStream
on MacOS_14 ARM64, MacOS_12, MacOS_13, Ubuntu_22_04, openSUSE_15_5.
* QTBUG-125006 MediaPlayer fails to play rpt video stream using sdp
file.
* QTBUG-124298 [iOS] Loading a new sound stops the play for other sounds
* QTBUG-123044 android: Playing something through QMediaPlayer and
adjusting volume from physical buttons shows wrong mode
* QTBUG-124189 tst_qcamerabackend: crash on exit
* QTBUG-122118 QML Camera Application Example does not work with Android
11 device
* QTBUG-119472 Camera with ffmpeg backend freezes the application
* QTBUG-124228 [gstreamer]
tst_QMediaCaptureSession::can_change_CameraDevice_on_attached_Camera
crashes sometimes
* QTBUG-125397 [gstreamer] setPlaybackRate has no effect before play()
* QTBUG-125632 wasm: Cannot play video in Firefox
* QTBUG-125552 Document dynamic linking of FFmpeg with Qt Multimedia on
macOS and Windows
* QTBUG-124183 [gstreamer] tst_QCameraBackend::testNativeMetadata test
failure due to duration timeout error
* QTBUG-122577 QScreenCapture tests are flaky on OpenSuse 15.5
* QTBUG-113399 QVideoSink with Qt 6 on Android ignores requested camera
settings
* QTBUG-113627 D3D11 Removing Device on QVideoSink save frame
* QTBUG-124586 QML video media player segmentation fault on AMD GPU with
FFMPEG
* QTBUG-124537 YUYV format from QCamera is buggy
* QTBUG-124647 YUYV and UYVY pixel formats are not rendered correctly
with FFmpeg backend
* QTBUG-124501 [gstreamer] media player does not play without outputs
connected
* QTBUG-124534 heap overflow in planarYUV420_to_ARGB32
* QTBUG-123749 QVideoFrame::toImage gives corrupt images when no RHI
backend is present
* QTBUG-125251 [gstreamer] spurious assertion failure on shutdown

### qttools
* QTBUG-118808 qt_add_translations with source autodetection mishandles
id-based generated UI headers
* QTBUG-123995 CMake error "Too many parentheses." on qt_add_lupdate
* QTBUG-124188 [REG 6.6 -> 6.7] Automatic resource embedding path of
qt_add_translations() has changed from Qt 6.6 to Qt 6.7
* QTBUG-125066 Configure fails in qttools if PrintSupport is disabled
* QTBUG-120751 error: ‘DeviceProfileDialog’ in namespace
‘qdesigner_internal::Ui’ does not name a type
* QTBUG-115448 qttools -unity-build-batch-size 100000 fails
* QTBUG-119469 Targets not yet defined: zstd::libzstd_static
* QTBUG-125983 Reg->6.7.1: Qt Designer: Can no longer change int
properties
* QTBUG-126182 Qt Designer  on archlinux always crash when edit an *.ui
file
* QTBUG-123611 libclang15-based lupdate fails with MSVC2022
* QTBUG-119429 Top flaky test: tst_lupdate::good on Windows_11_22H2,
Windows_11_23H2, and Windows_10_22H2.

### qtdoc
* QTBUG-124707 Coffee Machine example coffee cup image breaks with Qt
6.7.0 on Android
* QTBUG-124844 Invalid plural form qsTr example
* QTBUG-125057 [DocumentViewer] Printing becomes inactive after loading
txt file
* QTBUG-123445 Weird beheaviour of and errors on the console from the
"Coffee Machine" example
* QTBUG-122273 [MediaPlayerApp] The file names on the playlist in the
app have specific format on Android

### qtsensors
* QTBUG-110806 license discrepency?

### qtconnectivity
* QTBUG-124650 Missing BLE 5.x Extended Advertisements for Windows

### qtwayland
* QTBUG-124807 Horizontal scrolling not working under Wayland with
Alt+Wheel
* QTBUG-124839 Ctrl+Tab popup list of documents rendered behind main
window on Plasma 6 Wayland
* QTBUG-121551 Qt virtualkeyboard cannot compose Korean on text-input-v3
* QTBUG-125872 Windows are blurry with 200% scaling on Ubuntu 22.04 with
dev branch
* QTBUG-121446 text input : mismatch between QString and byte counts in
protocols

### qt3d
* QTBUG-124658 QAbstractCameraController documentation contains mistakes
* QTBUG-124891 Unredistributable files in qt3d / qtquick3d

### qtwebsockets
* QTBUG-110025 Android tests aren't bundling OpenSSL for any test

### qtwebengine
* QTBUG-123765 Segfault when dropping elements from Spotify in Firefox
* QTBUG-124353 [REG 6.5.3 - 6.6.0] Massive memory leak on WebEngineView
resizing
* QTBUG-123536 PdfPageView documentation page features PdfMultiPageView
in examples
* QTBUG-92114 Shift-Tab moves focus forward instead of backward in
WebEngineView inside QQuickWidget
* QTBUG-122970 Copying and pasting using shortcuts is not working in
MacOS
* QTBUG-124747 [REG 6.7.0->6.7.1] iOS examples not compiling
* QTBUG-124790 QtWebengine 6.8 (dev) doesn't render with basic html
files
* QTBUG-124635 [REG 6.7.0->6.7.1] WebEngine does not render anything on
embedded
* QTBUG-124506 [Qt PDF] Multiple definition error for static builds
* QTBUG-121359 QtWebEngineView crashes when scrolling using the
touchpad.
* QTBUG-112013 QWebEnginePage.setBackground(Qt::black) doesn't work for
page loading.
* QTBUG-122655 6.8.0 toplevel build fails on macOS, qtwebengine
* QTBUG-120247 [Qt WebEngine] Make it easier to re-configure after
installing missing libraries for qpa-xcb support
* QTBUG-124632 QtWebengine needs to be skipped with Windows 11 on ARM
* QTBUG-120370 QQuickWebEngineDownloadItem is not public

### qtcharts
* QTBUG-125262 Missing values from QAbstractAxis::AxisType

### qtspeech
* QTBUG-124868 Enable QTextToSpeech Speechd QLoggingCategory

### qtnetworkauth
* QTBUG-124333 [OAuth] Ability to open and close the loopback HTTP
server on a need-basis

### qtquick3d
* QTBUG-123442 Changing ExtendedSceneEnvironment texture properties at
runtime doesn't change the used texture
* QTBUG-125339 tinyexr: compile error with gcc-14
* QTBUG-122248 tst_QQuick3DNode::testProperties - comparing floats using
the operator== fails on VxWorks on 32bit arm
* QTBUG-122052 View3D as sourceItem of texture in XR not working
* QTBUG-124891 Unredistributable files in qt3d / qtquick3d

### qtmqtt
* QTBUG-120947 QMqttClient::setProtocolVersion's description seems to be
incorrect

### qtgrpc
* QTBUG-124917 [macOS] Cannot run 'magic8ball' example on macOS
* QTBUG-125328 Grpc genenerators: implicitly created export.qpb.h is
broken
* QTBUG-124413 use of EXTRA_NAMESPACE with qt6_add_protobuf ends up in
front of Timestamp
* QTBUG-125016 protobuf tests are fragile

### qtgraphs
* QTBUG-125194 labelFont does not work correctly

### qtinterfaceframework (Commercial only)
* QTBUG-125626 FATAL: Nuitka does not work

### qtapplicationmanager (Commercial only)
* QTBUG-124531 Building a Qt Application Manager Example with Boot2Qt
toolchain failed
* QTBUG-125081 qtapplicationmanager examples not compiling with linux on
arm binaries

Known Issues
------------

* Check that your system meets Qt's requirements:
https://doc.qt.io/qt-6.7/supported-platforms.html
* RTA reported issues from Qt 6.7
https://bugreports.qt.io/issues/?filter=25756
* See Qt 6.7 known issues from:
https://wiki.qt.io/Qt_6.7_Known_Issues
* Qt 6.7.2 Open issues in Jira:
https://bugreports.qt.io/issues/?filter=26139

Credits for the  release goes to:
---------------------------------

Eirik Aavitsland
Laszlo Agocs
Dilek Akcay
Konsta Alajärvi
Anu Aliyas
Viktor Arvidsson
Vladimir Belyavsky
Nicholas Bennett
Tim Blechmann
Eskil Abrahamsen Blomfeldt
Tatiana Borisova
Joerg Bornemann
Assam Boudjelthia
Kai Uwe Broulik
Michael Brüning
Alexei Cazacov
Kirikaze Chiyuki
Ed Cooke
Alexandru Croitor
Mitch Curtis
Giuseppe D'Angelo
Szabolcs David
Pavel Dubsky
Artem Dyomin
Alexey Edelev
David Edmundson
Christian Ehrlicher
Hatem ElKharashy
Andreas Eliasson
Ilya Fedin
Robert Griebl
Mikko Gronoff
Kaj Grönholm
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
Timothée Keller
Friedemann Kleint
André Klitzing
Michal Klocek
Antti Kokko
Tomi Korpipaa
Fabian Kosmale
Tomasz Kozłowski
Mike Krus
Santhosh Kumar
Kai Köhne
Inho Lee
Wladimir Leuschner
Robert Löhning
Thiago Macieira
Łukasz Matysiak
Safiyyah Moosa
Bartlomiej Moskal
Marc Mutz
Andy Nichols
Mårten Nordheim
Dennis Oberst
Tinja Paavoseppä
Samuli Piippo
Timur Pocheptsov
Lorn Potter
Sakaria Pouke
Matthias Rauter
David Redondo
Topi Reinio
Shawn Rutledge
Toni Saario
Lars Schmertmann
Carl Schwan
Sami Shalayel
Kristoffer Skau
Ivan Solovev
Axel Spoerl
Christian Strømme
Lars Sutterud
Audun Sutterud
Jan Arve Sæther
Jens Trillmann
Paul Olav Tvete
Tuomas Vaarala
Peter Varga
Tor Arne Vestbø
Juha Vuolle
Olli Vuolteenaho
Jaishree Vyas
Edward Welbourne
Paul Wicking
Oliver Wolff
Vlad Zahorodnii
Eike Ziller
Michał Łoś
