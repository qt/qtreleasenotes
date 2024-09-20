Release note
============
Qt 6.7.3 release is a patch release made on the top of Qt 6.7.2.
As a patch release, Qt 6.7.3 does not add any new functionality but provides
bug fixes and other improvements and maintains both forward and backward
compatibility (source and binary) with Qt 6.7.2.

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
* c794263de0b Update public suffix list
Updated the public suffix list to upstream SHA
903a83ff7bfc3148e3692e09396f9f3bdc9462ef.

* 04072d636d7 PCRE: upgrade to 10.44
PCRE2 was updated to version 10.44.

* a2aa1f81a81 Determine Qt::AA_DontShowIconsInMenus default value based
on platform
The default value of Qt::AA_DontShowIconsInMenus is now determined
based on the platform. On macOS icons will not show by default. To
override, use QAction.iconVisibleInMenu for individual menu actions, or
set Qt::AA_DontShowIconsInMenus to false.

* cdb4472249d Relax QHttpHeaders value field checks to allow UTF-8
Allows UTF-8 in header values now.

* 05f0c6ca0b3 QBitArray: fix read of uninitialized terminating null
Fixed a regression introduced in 6.7.0 that could cause QBitArray to
report wrong bit counts after a bitwise operation.

* 84785289f42 CMake: Add partial fixes for archiving dSYMs with an Xcode
project
CMake-generated Xcode projects will now include debugging symbols by
default, regardless of configuration type, and Release-like
configurations will default to using dSYM bundles instead of keeping the
debug symbols in object files, to match Xcode project defaults.

* cc053a7bbf3 Add Files field
Specify the source file that the "Mipmap generator for D3D12" component
consists of.

* 3571012f362 Change the mimetype database embedded into QtCore
For licensing reasons, QtCore no longer ships a copy of the MIME
database from freedesktop.org's shared-mime-info project, but the one
from the Apache Tika project. The tika definitions don't have icons or
translated descriptions, but are sufficient for matching file types.

* ed208502a66 QMimeDatabase: pick up XML mimetypes from :/qt-
project.org/mime/packages
QMimeDatabase can now pick up XML mimetype definitions from :/qt-
project.org/mime/packages. GPL-compatible projects which provide self-
contained binaries can use this to provide a copy of freedesktop.org.xml
that will be used instead of the TIKA mimetypes.

* a050a0f8cd0 Remove GTK3 native menu
Due to deprecation of the gtk_menu_popup() function, we no longer use
GTK menus on Gnome: they are now rendered by Qt.

* a56aba7d1ae QArrayDataOps: fix FP equality comparison
Fixed a bug when two QLists holding NaN values were considered to be
equal.

* c41db690407 Update CLDR to v45, adding language Kuvi
Updated CLDR data, used by QLocale, to v45.

* 571565c2fce Add __attribute__((format(printf()))) to q(v)nprintf()
Added attributes for GCC-compatible compilers to detect format/argument
mismatches. If this throws warnings for your calls now, don't ignore
them. printf() format mistakes could be security-relevant. You may also
find that you relied on undocumented behavior, such as that certain
implementations (Windows, Android, WASM) of qsnprintf() support
char16_t* instead of wchar_t* for %ls. In that case, you should port to
qUtf16Printable() and QString::asprintf(), or suppress the warning and
port away from the platform dependence at your earliest convenience.

* 82e23d266b0 Fix partial_ordering::unordered != 0 comparison
Fixed a bug where partial_ordering::unordered != 0 comparison produced
an incorrect result.

* 5b229ae55a5 SQLite: Update SQLite to v3.46.1
Updated SQLite to v3.46.1

* 18a38decd20 Update Freetype to 2.13.3
Updated bundled Freetype to version 2.13.3.

* e7dff0c9dce Android: upgrade to Gradle 8.10 and AGP 8.5.2
Updated Gradle to 8.10 and AGP to 8.5.2.

* a0e0b48dc01 Update tika-mimetypes.xml from upstream
Updated TIKA MIME types definition file to add the audio/aac and
application/x-java-keystore MIME types.

* 9bfd96dda25 Update tika-mimetypes.xml from upstream
Updated TIKA MIME types definition file to add the audio/flac MIME type
as an alias for audio/x-flac MIME type.

* 72c82e0fb75 Update to Harfbuzz 9.0.0
Updated Harfbuzz to 9.0.0.

* 9d3f19585aa Update bundled libpng to version 1.6.44
libpng was updated to version 1.6.44

* 92b68578496 Update bundled libjpeg-turbo to version 3.0.4
libjpeg-turbo was updated to version 3.0.4

### qtdeclarative
* 845193aa61 Warn about unset required properties on composite
singletons
Instantiating singletons with unset required properties will now fail
and print a warning instead of creating the singleton with the
properties unset.

* aa757f2051 Fix rendering errors with Calibri Light and curve renderer
text
Fixed an issue where some fonts would exhibit artifacts when renderered
with the CurveRendering render type.

* 2b3a164cb0 QML: Type-check objects passed to QmlListWrapper
Assignments to list properties in QML are now type-checked. Before you
could, for example, insert a plain QObject into list<Item>, producing
undefined behavior. Now it instead inserts null and warns. In
particular, if you assign a JavaScript array of random objects to a list
property, QML will check each individual element, and insert null as
well as warn when encountering type incompatibilities.

### qtmultimedia
* 5f0a7f635 Override the signal 'videoFrameChanged' in qml video sink
Removed QVideoFrame parameter from the not documented qml signal
VideoSink.videoFrameChanged.

* 50ef345f4 Update FFmpeg version in documentation
Updated FFmpeg to n7.0.1.

* ef9d4c696 Update FFmpeg version in documentation
Updated FFmpeg to n7.0.2.

### qtconnectivity
* ee65dbc0 sdpscanner: fix format strings for (u)int64_t
Fixed a bug involving broken serialization of SDP_(U)INT64 DTDs on Big-
Endian machines.

### qt3d
* 2345b4f79 Update assimp to 5.4.3
Update ASSIMP to v5.4.3

### qtserialbus
* 647671eb Fix virtual can backend usage in multithreaded environment
Fixed a race condition during creation of the VirtualCanServer when two
QCanBusDevices are instantiated in the same process in different threads

* 252dd374 Fix virtual can backend usage in multithreaded environment
Fixed a race condition during start of the VirtualCanServer in
multithreaded environment

### qtnetworkauth
* 0924f63 Don't clear QAbstractOAuth2::scope upon empty server response
If the authorization server returns an empty 'scope' response, the
requested scope is not cleared anymore. Instead, it is assumed that the
requested 'scope' was granted.

### qtquick3d
* 1f10d90f9 Update TinyEXR to v1.0.9
Updated TinyEXR to v1.0.9

* 954339d48 Update Assimp to v5.4.3
Updated Assimp to v5.4.3

### qtshadertools
* dab6e06 Update identifier and name for Khronos license
Change name of Khronos license to 'MIT Khronos - old variant', as it is
now called in SPDX: https://spdx.org/licenses/MIT-Khronos-old.html .


Fixes
-----

### qtbase
* QTBUG-125513 crash when mixing QWidget style and styleSheet
* QTBUG-126012 [patch] bindTextureImage: clearing GL error: 0x500
* QTBUG-125120 wasm: qtvirtualkeyboard crashes on startup
* QTBUG-125381 wasm: microphone permissions on firefox dont work
* QTBUG-126056 Camelcase forwarding headers missing in macOS/iOS builds
* QTBUG-125858 REG: Wrong result value in QMessageBox::warning detected
in version 6.7.1
* QTBUG-126084 QDockWidget unplugged from floating tab is in the wrong
position
* QTBUG-126107 tst_QStingConverter::invalidConverter() triggers valgrind
* QTBUG-125479 iOS - The cached device pixel ratio value was stale on
window expose
* QTBUG-126052 submenu overlaps in qWdiget on iOS
* QTBUG-126044 QMenu: Submenu partially hidden by main menu
* QTBUG-126122 [Reg 6.6 -> 6.7] Window resizing on Android is broken
* QTBUG-125410 TextField.inputMethodHints flags are ignored on Android
for Qt 6.7.0
* QTBUG-124786 [Android] NullPointerException at
QtActivityDelegate.java:83
* QTBUG-126265 uic: Code Injection to Potential Code Execution
* QTBUG-121586 [Reg 5.15->6.x] QActionGroup signals missing from
documentation
* QTBUG-126386 qcompare.h build error on MSVC
* QTBUG-124829 The appearance of icons in QFileSystemModel is simplified
and differs from the typical Windows icons.
* QTBUG-126343 QBitArray::count breaks after bitwise opererations
* QTBUG-119076 Selecting multiple rows is sluggish if there are column
spans
* QTBUG-126394 [Regression] Decreased performance in timerEvent
* QTBUG-123886 [REG 6.5.2->6.5.3] QAbstractScrollArea::sizeHint does not
include the horizontal scrollbar's size
* QTBUG-23470 QLibrary does not add 'lib' prefix if file name starts
with 'lib' (unix)
* QTBUG-124898 [Reg 6.2 -> 6.5] Qt.uiLanguage does not work for locale
changes
* QTBUG-126214 QtCore: implicit instantiation of undefined template
'std::char_traits<unsigned char>' (libc++ 19 / musl libc / amd64)
* QTBUG-122753 Qt Multimedia: implicit instantiation of undefined
template 'std::char_traits<unsigned char>' (libc++ 19 / musl libc /
amd64)
* QTBUG-122778 QTreeView stylesheet does apply the border and the
background color to the branches
* QTBUG-125993 Double tap on touch screen not provoking
mouseDoubleClickEvent - patch included
* QTBUG-123298 Qt 6.5 on macOS - In full screen, topmost QMenu action
doesn't fire
* QTBUG-126381 qcssparser.cpp ASSERT: "d->parsed.metaType() ==
QMetaType::fromType<QList<QVariant>>()"
* QTBUG-126594 6.7.2 qtbase: missing cups dependency in
Qt6PrintSupport.pc and Qt6PrintSupport cmake modules
* QTBUG-126502 Link broken on Qt Test Overview page in docs.qt.io
* QTBUG-126678 CMake flag QT_USE_TARGET_ANDROID_BUILD_DIR does not work
with QT_ANDROID_BUILD_ALL_ABIS
* QTBUG-126621 moveToTrash fails to remove a symlink to a directory
after trashing
* QTBUG-33786 Orca reads model columns instead of rows when navigating
through items in QListView
* QTBUG-126596 QListWidgetItem::setForeground() does not work
* QTBUG-126543 windows11 style has QTableView ignoring
Qt::ForegroundRole
* QTBUG-126348 QToolButton widgets have wrong background colors with
windows11 style and dark themes
* QTBUG-56590 macdeployqt copying dSYM bundles
* QTBUG-89484 macdeployqt not deploying QSerialBus (canbus) plugins
* QTBUG-126456 QWidgetWindow: Use of object after destruction
* QTBUG-126043 macOS: Double clicking an appliaction in finder opens it
without the window becoming active
* QTBUG-122755 Dragging text on HighDPI screen results in a warning
"QPixmap::scaled: Pixmap is a null pixmap"
* QTBUG-68465 macOS: Accessibility: MenuItems are not accessible
* QTBUG-27205 QFileSystemModel::filename() uses wrong role value for
call to data() method
* QTBUG-126503 No graphic change on Hover for QPushButton and
QToolbutton
* QTBUG-125781 Cannot distinguish disabled or hovered buttons on Windows
11
* QTBUG-126622 [iOS] Screen Reader focus gets stuck
* QTBUG-123449 [Reg 6.4->6.5] Quick MenuItems do not appear grayed out
when disabled under GTK
* QTBUG-126775 windeployqt does not provide MinGW's libraries
* QTBUG-126391 tst_QDateTime::timeZones() fail on macOS 15
* QTBUG-107139 Webassembly cannot input Chinese
* QTBUG-124932 Incorrect keyboard functionality in a QML 3D scene on the
WebAssembly platform.
* QTBUG-117096 Input fields (QWidgets and QML) don't register dead keys
accents when using a Linux desktop
* QTBUG-112287 android: Input does not work with QQuickWidget
* QTBUG-52292 Pantheon desktop is not recognized as Gtk desktop
* QTBUG-126773 iOS - library not found for -llibavformat
* QTBUG-127168 Memory Leak: Windows: Result of SetupDiGetClassDevs() is
not freed
* QTBUG-127055 QThread::terminate() ABA problem
* QTBUG-125589 weired console message with simple application
* QTBUG-126479 show()+showMaximized()+activating a layout de-maximizes
the window
* QTBUG-104201 QWidget: resize() after showMaximized() causes strange
behaviour
* QTBUG-126435 Document QT_NO_UTF8_SOURCE
* QTBUG-127112 QProgressBar with Windows 11 style is using far too much
cpu
* QTBUG-124561 Qt.labs.platform context Menu appears out of the app
window on Gnome/wayland
* QTBUG-126598 Qt.labs.platform Menu broken content positioning on linux
* QTBUG-126541 Qt FTBFS on clang when C++20 is enabled
* QTBUG-127414 Random configure/build error for android multiabi
* QTBUG-60674 QSqlRelationalTableModel - relation refresh crash
* QTBUG-127473 [REG 5.15 -> 6] QList::op==() is broken for FP types
* QTBUG-124481 KDE theme plugin always assumes single click activation
on KDE Plasma 6
* QTBUG-126575 QImage / QImageReader: lost QColorSpace during rotation
* QTBUG-126721 [REG 6.6->6.7] Overridden setVisible() no longer gets
called when parent widget is shown
* QTBUG-126218 Preview is not generated when QPrintPreviewWidget is
shown
* QTBUG-63485 Documentation for QStringList::replaceInStrings
* QTBUG-126820 Move all QKeyCombination-returning operators into the
namespace Qt
* QTBUG-125778 QMdiSubWindow does not refresh when the Maximize button
is hidden after being created.
* QTBUG-124564 Windows 11: Alternating row colors doesn't work in
windows11 style
* QTBUG-127668 A standalone test can't be configure with a cross-
compiled Qt
* QTBUG-120396 `QUrl::resolved` gives wrong result when there are more
`..`s in relative reference
* QTBUG-127614 [macOS] [labs.platform] Menu stuck on opening when
standard icons are used
* QTBUG-127551 [win] [labs.platform] Standard menu icons looks wrong on
DPR > 1
* QTBUG-127342 OCI plugin does not build for ARM
* QTBUG-127512 tst_QTextLayout::softHyphens(16) failed on Ubuntu
24.04(both x64 and arm64) GNOME
* QTBUG-127641 QComboBox popup position changes after widget reparenting
* QTBUG-125149 Misplaced popup menu for reparented combo box
* QTBUG-122747 Reparenting QTabWidget with a native window tab can cause
crash
* QTBUG-127392 Avoid warning: Ignoring window icon xxx exceeds maximum
xcb request length 65535
* QTBUG-116083 Build failure related to fontdatabase / fontconfig
* QTBUG-127759 Qt::partial_ordering::unordered implements op!=()
incorrectly
* QTBUG-127403 Typo in QRhiTextureRenderTargetDescription
* QTBUG-119753 QSqlRecord access causes hang/memory leak and crash using
QODBC driver
* QTBUG-126303 QWidget::createWindowContainer() managed window deleted
when new widget added due to QRhi
* QTBUG-122774 "--no-qmltoolingsettingsInternal" gives error 'Unknown
option 'no-qmltoolingsettingsInternal''
* QTBUG-124310 QT_DISTANCEFIELD_DEFAULT_BASEFONTSIZE=128 causes a
QDistanceField crash
* QTBUG-127857 -skip-tests and -skip-examples are case sensitive
* QTBUG-127530 Webview does not show header widget on Qt for Android 6.7
and other view issues
* QTBUG-126572 Default qt_generate_deploy_qml_app_script does not deploy
QtWebEngineProcess(d).exe to where it should be
* QTBUG-127732 QT_WIN_DEBUG_CONSOLE breaks windeployqt in CMake install
* QTBUG-127552 a11y: QFrame reports incorrect top-level role on Linux
(AT-SPI2)
* QTBUG-125496 Apps continue running in the background.
* QTBUG-127549 [6.5->6.7 regression] QString::replace() takes huge
amount of time. 10x worse performance
* QTBUG-126013 heap-use-after-free in from QtPrivate::watchContinuationImpl
* QTBUG-127880 Race condition in QFuture implementation
* QTBUG-128137 qt-configure-module does not consider chosen
INSTALL_LIBEXECDIR
* QTBUG-127926 Outdated Android docs still refer to
QtAndroid::androidActivity()
* QTBUG-127288 Windows: MDI subwindow icons have low resolution and an
unattractive appearance when the window is displayed in maximized mode.
* QTBUG-127381 Unexpected shift-selection in QTreeView.
* QTBUG-128254 Cannot build signed AAB with verbose deployment
* QTBUG-109619 Enabling 2 extra Android CMake options leads to a build
error
* QTBUG-122967 [macOS]Calling winId() renders additional undesired
pixmap if scaling factor is not 1
* QTBUG-122751 Top flaky test: tst_qaccessibilitymac::treeViewTest on
MacOS_14 ARM64, MacOS_13, MacOS_12
* QTBUG-128298 QT_ANDROID_DEBUGGER_MAIN_THREAD_SLEEP_MS doesn't work
* QTBUG-123752 Unexpected offset of fixed-height top-level window when
Windows Taskbar is on top
* QTBUG-124733 Tool bar loose focus over mouse hovering
* QTBUG-128290 QT_THREAD_PARALLEL_FILLS macro causes semaphore_wait_trap
on iOS
* QTBUG-125975  QT_DISABLE_DEPRECATED_UP_TO 0x060400 gives link error
with static build
* QTBUG-117417 Regression 5.15: Sharing Files w FileProvider fails
* QTBUG-110841  [REG: 5.10.1->5.11.0-alpha] Mouse events not observed
when Super (Windows) key is held down.
* QTBUG-128325 tst_qbytearrayview test gives deprecated warnings at
compilation
* QTBUG-128337 configure does not properly parse sql options
* QTBUG-124118 QColorDialog on Windows 11: layout is broken
* QTBUG-127788 QSlider's ticks are blurry when using Windows 11 style
* QTBUG-127987 Error copying directory: .syncqt_staging
* QTBUG-94956 "Invalid revision: zipalign" when building for android
* QTBUG-124465 QDate::fromString very slow in 6.7.0
* QTBUG-125239 ERROR: AddressSanitizer: heap-use-after-free WRITE of
size 1 in tst_QGuiApplication::modalWindow()
* QTBUG-126752 Calling popup() on QCompleter causes an abnormal behavior
of the Qt virtual keyboard.
* QTBUG-128516 [macOS] Sporadic crash on
QCocoaScreen::deliverUpdateRequests()
* QTBUG-128390 Crash on QWindowPrivate::updateDevicePixelRatio() with
nullptr access
* QTBUG-123551 [Boot2Qt] A windows is blacked out in QQuickWidget
Example application
* QTBUG-124235 Too small minimumSizeHint for QDateEdit/QDateTimeEdit
with windows11-style
* QTBUG-118794 "The cached device pixel ratio value was stale on window
expose" when opening context menu on macOS with external display
* QTBUG-94871 Qt should subscribe to dbus system tray and dbus menu
service appearing/disappearing
* QTBUG-126053 QString::arg(u8' ') prefers the integral, not the QChar
overload, when built in C++20
* QTBUG-126054 QString::arg(wchar_t{}) prefers the integral overload
instead of the QChar one
* QTBUG-126055 [REG SiC 6.4 -> 6.5] QString::arg(qfloat16{}) is
ambiguous if QFLOAT16_IS_NATIVE
* QTBUG-117321 Inconsistent treatment of char[] with embedded NULs when
target is QString vs. QByteArray
* QTBUG-126178 QtQuickView does not handle user input in a LinearLayout
* QTBUG-126278 QNetworkReply::attribute(HttpReasonPhraseAttribute)
returns empty value when Http2 is used
* QTBUG-124572 Program crash when using a specific glyph from a popular
font file on Linux
* QTBUG-53974 QGraphicsScene always in inactive state if placed in a
QTabWidget
* QTBUG-113404 Wayland: Gestures are not delivered to correct top level
widget
* QTBUG-125878 Cannot pinch-to-zoom after the qt 6.7.1 upgrade
[regression]
* QTBUG-126313 QScroller gesture blocks mouse clicks
* QTBUG-126426 QStyleOptionProgressBar is not properly rendered by a
delegate
* QTBUG-124919 QDBusSignature considers an empty string to be an invalid
signature
* QTBUG-126674 Inconsistent hashing between bool and integral overloads
* QTBUG-124653 Regression in QTemporaryFile::fileName()
* QTBUG-126866 Archiving the application does not have debug info files
(dSYM) included as expected
* QTBUG-127110 Platforms still use the inefficient qvsnprintf() fall-
back
* QTBUG-125730 QAnyStringView('\xE4') creates an invalid UTF-8 string
(expected: valid L1)
* QTBUG-127085 Crash when re-opening laptop lid
* QTBUG-126187 HW Keyboard input is broken after touching UI
* QTBUG-119901 Basic <type_traits> not working for q*int128 in QtCore
TUs
* QTBUG-120637 QUuid::Id128Bytes UB when accessing members
* QTBUG-127468 Building against Android NDK r27 fails
* QTBUG-115158 Time zone names and abbreviations are not localised
* QTBUG-124011 Android: QFileInfo::isWritable() returns false
erroneously and throws an exception
* QTBUG-125610 Constructing a QDate from std::chrono::year_month_day
results in link error
* QTBUG-121653 License clarification for unicode & unicode-cldr related
files

### qtsvg
* QTBUG-123138 QtSvg doesn't support feGaussianBlur
* QTBUG-127018 REG: Incorrect SVG render result for specific SVG file
* QTBUG-128583 Regression in QtSvgTinyDocument: Runtime warnings logged
to the console

### qtdeclarative
* QTBUG-125914 Formatting qml code containing an enum with qmlformat
removes enum values
* QTBUG-122658 ListView crashes when `reuseitems` is set after
`positionViewAtIndex`
* QTBUG-124624 Online documentation doesn't explain how to set dark
theme of Fusion style
* QTBUG-125529 Lancelot baseline mismatch in Qt Quick's ComboBox using
Basic style
* QTBUG-125864 Broken rendering with curve renderer in Shapes example
* QTBUG-125720 Typo in example code in QQuickRhiItem documentation
* QTBUG-124461 qmlls does not exit after receiving an exit request
* QTBUG-125157 Clarify the snippet about Editing Cells in a TableView
* QTBUG-126094 Spelling of Qt Qml/QML very inconsistent
* QTBUG-124744 [Reg 6.7.0 -> dev] Bindings on width/height of
ApplicationWindow.background are not respected
* QTBUG-125725 QQuickControl::focusReasonChanged does not work properly
* QTBUG-112320 javascript engine:  Proxy handler.get() doesn't work on
field 'name'
* QTBUG-118165 qmlTypeId() causes QML_ELEMENTs to not be registered
* QTBUG-126124 Material style Button has extra padding when text
property has a value but display is IconOnly
* QTBUG-122998 Crash in QQuickItemView through recursive item release
* QTBUG-125481 [Reg 6.7.0->6.7.1] Combination of Quick Layouts broken
* QTBUG-123527 Unchecked Fusion style RadioButtons / CheckBoxes are
barely visible in dark mode
* QTBUG-126136 QML signal to C++ slot connection nonfunctional if
declared within the C++ object with the slot
* QTBUG-125224 Cannot stop animation if it was restarted before the last
loop completed
* QTBUG-126042 Nested ListView of orthogonal orientation gets stuck
without snapping using touchpad
* QTBUG-126057 Item state change reverts item's scaled size
* QTBUG-119866 TapHandler is used in most of the code snippet of
DragHandler
* QTBUG-126267 QQuickTextDocument::setTextDocument disables TextEdit
* QTBUG-126510 [REG 6.6 -> 6.7] Type error due to clash between JS and
Qml type names
* QTBUG-125906 Flicking needs to be done horizontally to delete items in
apps that have been rotated 90°.
* QTBUG-126563 [Reg 6.5 -> 6.7] Anonymous function on a signal results
in QML Linter error when compiler warnings are enabled
* QTBUG-124572 Program crash when using a specific glyph from a popular
font file on Linux
* QTBUG-126330 Crash when resizing ListView with reuseItems: true and
custom QQuickAsyncImageProvider
* QTBUG-119647 [Tests] Warnings in
qtdeclarative/tests/auto/quickcontrols/controls/data/tst_tumbler.qml
* QTBUG-30768 When an item in a ListView is snapped into place then it
does not take account for the section header
* QTBUG-126628 QQuickAsyncImageProvider causes crash without Qt Network
(qml_network)
* QTBUG-125526 [REG 6.6.3-6.7.0] TextEdit - warnings on loading embedded
QRC images
* QTBUG-126396 Illegal memory access in QQuickShaderEffectPrivate
* QTBUG-126673 [Regression 6.6 -> 6.7] Higher CPU utilization in large
QML applications
* QTBUG-123894 Top flaky test: tst_qquicklistview::multipleTransitions
on MacOS_14 ARM64, MacOS_12 and MacOS_13
* QTBUG-125095 [REG 6.2 → 6.5] Qt.binding fails with QtQObject inside
createObject
* QTBUG-126834 [Reg 6.5 -> 6.6] Qml: Compiler generates wrong code for
Array.prototype.join invocation
* QTBUG-126626 Hovered property stays when popup is opened from drawer
* QTBUG-126723 [REG 6.6 → 6.7] TableModel appendRow() no longer works.
* QTBUG-123987 QML Popup "palette" property is not linking forward to
the proper palette docs
* QTBUG-122963 Inconsistency in popup positioning logic
* QTBUG-116442 Doubleclick sent to first item when single-clicking
alternating items
* QTBUG-125296 background color of TreeViewDelegate
* QTBUG-126690 Creating dynamic properties and reparenting a Control
break bindings on Singletons
* QTBUG-127292 Failures on tst_qquicktextdocument
* QTBUG-126474 QQuickLayout Recursive Rearrange Locks Application
* QTBUG-127328 NinePatchImageSelector cannot use relative path for
source
* QTBUG-127399 LayoutMirroring warning has typo
* QTBUG-123191 Scenegraph nodes batching broken beginning with Qt 6.5.3
* QTBUG-126886 Setting format in QQuickTextDocument (TextArea) crashes
* QTBUG-127474 qmlls erases user code when updating implicitly defined
signal handlers
* QTBUG-127309 qmllint: uses wrong category for  Property "xxx" has
incomplete type "Unregistered". You may be missing an import. [missing-
property]
* QTBUG-125146 qmllint highlights wrong part in warning message
* QTBUG-109880 Wrapper method that should create and return a Javascript
Generator object returns undefined
* QTBUG-127619 FileDialog prints binding loop warning when opened.
* QTBUG-127602 qmlls does not read .qmllint.ini
* QTBUG-124498 qmltyperesolver can't handle ECMAScript resources
* QTBUG-125053 QAbstractListModel fails to populate QML model
* QTBUG-81231 QJSEngine and QStringList properties handling, a potential
performance issue
* QTBUG-126512 Controls styles use Qt.styleHints even though
documentation advises against it
* QTBUG-126616 CurveRendering artifacts drawing fonts
* QTBUG-97557 Qt Quick batch rendering issue when a batch contain nodes
that have different index types
* QTBUG-127315 Tumbler's currentIndex is not the same as the initial
value
* QTBUG-127687 qmlls does not print warning categories on warnings
* QTBUG-127704 [REG: 6.6.2 → 6.7.2] QList<QObject *> argument causes
TypeError
* QTBUG-124553 [Reg 5.15 -> 6.2] QML Binding is overwritten after
initialization
* QTBUG-124921 Tumbler's currentIndex is not working when the model is
changed at runtime
* QTBUG-124124 QtQuick MessageDialog: Fails on macOS when using richtext
* QTBUG-127650 Strange behaviours in QML warning, "Using attached type
<TYPE> already initialized in a parent scope"
* QTBUG-124764 qt_add_lupdate adds extra location for QML files
* QTBUG-121449 The emojis are pixelated
* QTBUG-127809 TableView forceLayout does not correct contentX/contentY
after columnWidth/rowHeight changed
* QTBUG-125416 SwipeView shows all elements at once if it is 0x0 in size
* QTBUG-126514 [Regr: 6.5.0->6.7.1] Mouse wheel scrolling in nested list
views broken
* QTBUG-128283 Memory leak after calling QQuickItem::grabToImage
* QTBUG-127455 QML ListView crashes in
QQuickItemViewPrivate::itemGeometryChanged
* QTBUG-114984 Software Renderer: Updating a layer-enabled subtree while
it is invisible produces wrong outcomes
* QTBUG-127343 Incomplete and inconsistent type checking for QML lists
* QTBUG-127906 Qt.labs.platform.Menu opens at the wrong location with
scaling enabled
* QTBUG-127440 QML TextField can't deselect by clicking on the text
field
* QTBUG-10684 Interaction between text input and flickable is lacking
* QTBUG-111504 Text loses selection when releasing long-press on Android
text input
* QTBUG-116606 unable to deselect text in text input using touch
* QTBUG-123636 Crash when calling QWidget::setFixedSize with larger
values
* QTBUG-127049 Infinitely Recursvie Iterators Segfault process
* QTBUG-126981 Application crashes with assert when closing the window
with TableView
* QTBUG-110451 emitting dataChanged trips on freed delegate memory
* QTBUG-123595 VerticalHeaderView / HorizontalHeaderView should always
use headerData() -- stale docs?
* QTBUG-127727 tst_SoftwareRenderer::renderTarget fails
* QTBUG-128561 Crash when re-showing shape using CurveRenderer
* QTBUG-122784 QtQuick: Unset required property in Singleton is not an
error?
* QTBUG-117526 QQuickStylePrivate::fallbackStyle has the wrong value
when using run-time style selection and the fallback style is imported
via the style's qmldir
* QTBUG-126222 tst_how_to_qml::activeFocusDebugging() fails often
* QTBUG-125867 SelectionRectangle in Drag mode intercepts events even
when it should not
* QTBUG-68465 macOS: Accessibility: MenuItems are not accessible
* QTBUG-112870 clang-tidy warnings on static global variables in moc
generated code
* QTBUG-126560 ListView's count property not updating when the ListView
is inside a Drawer and the model gets its data from a network request
* QTBUG-125589 weired console message with simple application
* QTBUG-125571 YAnimator onRunningChanged can Qt.callLater(jsFunc) with
invalid scope object
* QTBUG-118109 qmllint: deferred-property-id logging category is muted
* QTBUG-127761 incompatible exported QQmlJS::Dom symbols between MSVC
2019 and 2022
* QTBUG-127691 qmllint: don't print duplicate warnings
* QTBUG-118024 Still referenced objects are deleted during swap
operation between two ListModel instances
* QTBUG-127562 qmllint wrongfully complains about tumbler attached
property
* QTBUG-123491 qmlls memory leak
* QTBUG-124922 The text in a TextEdit is not updated when
LayoutMirroring is enabled
* QTBUG-128368 Make sure that also qt6_ CMake commands are in the help
index
* QTBUG-36525 Binding loop warning message does not give sufficient
information in order to fix it

### qtactiveqt
* QTBUG-123533 dumpcpp generates code that does not compile
* QTBUG-111760 target_link_libraries(foo INTERFACE Qt::Core) fails for
interface libs with CMake < 3.19 on Windows

### qtmultimedia
* QTBUG-125213 Flaky crashes on ASAN-compiled tst_qsoundeffect
* QTBUG-119102 Cannot record video using QML or widgets camera example
on macOS with built-in camera or iOS device continuity camera
* QTBUG-124537 YUYV format from QCamera is buggy
* QTBUG-124534 heap overflow in planarYUV420_to_ARGB32
* QTBUG-123749 QVideoFrame::toImage gives corrupt images when no RHI
backend is present
* QTBUG-123451 Incorrect frame rate selectiion for QCamera on iOS
* QTBUG-123220 Green Line Artifact in QML VideoOutput component
* QTBUG-126203 [darwin] MediaPlayer does not always take into account
the selected audio output device
* QTBUG-118571 Android tests on CI part 1/3 (camera & media
capture/player)
* QTBUG-124396 [Boot2Qt] "The wayland connection broke" when running
audioooutput example app
* QTBUG-124925 [REG 6.5.5 -> 6.5.6] Spectrum App Crashes after recording
sound in "Record and Playback" Mode
* QTBUG-126254 [darwin] Camera example crashes when recording with
webcam, "AudioChannelLayout is invalid"
* QTBUG-126988 [macOS] QAudioSource::start returns invalid pointer if
start failed
* QTBUG-122104 Missing Info.plist in audio devices example does not
allow using the application on macOS
* QTBUG-126968 wasm: MediaPlayer won't work if source is set at creation
* QTBUG-124615 Top flaky test: tst_qmediaplayerbackend::play_createsFram
esWithExpectedContentAndIncreasingFrameTime_whenPlayingRtspMediaStream
on MacOS_14 ARM64, MacOS_12, MacOS_13, Ubuntu_22_04, openSUSE_15_5.
* QTBUG-126192 ios: Zoom factor does not notify changes and cannot zoom
back to 1.0
* QTBUG-126428 Android: Regression with playing video (H.264)
* QTBUG-116766 [Boot2Qt] List of cameras should contain only available
(connected) ones
* QTBUG-124206 [GStreamer]
tst_QAudioDecoderBackend::play_emitsFormatError_whenMediaHasNoAudioTrack
does not report errors
* QTBUG-127453 WASM: seekableChanged is not firing
* QTBUG-127675 Spurious assertion failure in
tst_QSoundEffect::testSetSourceWhilePlaying
* QTBUG-127320 QMediaPlayer unable to open files with absolute paths
without scheme
* QTBUG-127494 [WASM] Multiple VideoOutputs cannot play independently
* QTBUG-127745 tst_qvideoframecolormanagement failed on Ubuntu 24.04
offscreen(arm64)
* QTBUG-127744 tst_qvideoframe failed on Ubuntu 24.04 offscreen(arm64)
* QTBUG-127746 tst_qmediaplayerbackend failed on Ubuntu 24.04
offscreen(arm64)
* QTBUG-127784 Inaccurate color handling when no RHI backend is
available
* QTBUG-128246 QMultimedia UYVY rendering is in lower image quality
* QTBUG-128759 [REG 6.7.2->6.7.3] change in configure options, gstreamer
on LoA
* QTBUG-124725 [Camera] The video recorded with webcam on macOS is
corrupted - it only displays green flashing noise
* QTBUG-125613 Investigate lacking video format support on Android 14
with FFmpeg media player
* QTBUG-117888 Wide camera is not supported?
* QTBUG-122757 FFmpeg+Intel VAAPI decoding of certain h264/mp4 videos
fails in 6.6.x+
* QTBUG-126106 QVideoFrames sent to QML as signal arguments are
deallocated too late
* QTBUG-126143 QMediaFormat on Linux does not show MP3
* QTBUG-126799 [gstreamer] playback rate / seeking unreliable
* QTBUG-123056 GStreamer: `setLoops` sometimes not working
* QTBUG-127031 [QMediaPlayer] switching video output while playback is
paused does not update new sink
* QTBUG-127346 [gstreamer] QMediaPlayer: subsequent playback broken
* QTBUG-127484 CMake Error if gstreamer_gl_wayland (or gl_x11) feature
is enabled
* QTBUG-126014 [ffmpeg] setVideoOutput/setAudioOutput while playing
seems broken
* QTBUG-95952 Seemingly unnecessary check for pulse-mainloop-glib
* QTBUG-127137 [ffmpeg, macos]
tst_QMediaPlayerBackend::stressTest_setupAndTeardown crashes on CI
* QTBUG-127927 [gstreamer] record_video_without_preview assertion
failure on CI
* QTBUG-118594  QML Camera wrong Orientation on iOS
* QTBUG-128336 Camera widget example does not record audio with default
AAC format
* QTBUG-118877 -qreal float configuration option does not compile

### qttools
* QTBUG-126182 Qt Designer  on archlinux always crash when edit an *.ui
file
* QTBUG-126167 CMake fails to configure simple project
* QTBUG-126189 [REG 6.7.1->6.7.2&6.8.0] lconvert, lrelease, lupdate and
few others not combiled in no-gui build
* QTBUG-125066 Configure fails in qttools if PrintSupport is disabled
* QTBUG-126274 [REG: 6.7.1->6.7.2] Windows/Win11/Vista styles: designer:
Spinbox values are shown doubled
* QTBUG-125310 tst_lupdate asserts on mingw13
* QTBUG-61277 Doc: Some modules missing from "All QML Modules" page
* QTBUG-127146 [REG 5.15 -> 6.0] TR_EXCLUDE became too strict
* QTBUG-126139 Linguist shipped with Qt6 breaks how language tag is
handled
* QTBUG-27936 Regression: lupdate is very very slow
* QTBUG-124200 Linguist 'does not know the plural rules for Luganda'
* QTBUG-127630 qdoc crashes when building Qt Creator developer
documentation
* QTBUG-127513 qttool: depends on network-support, but should only be
optional
* QTBUG-127789 Generated TS files are missing the language and
sourcelanguage attributes
* QTBUG-127792  Generated TS file with plural forms contain incorrect
<numerusform> entry count
* QTBUG-127841 Windows ARM: qttools - tst_lconvert::initTestCase() fails
* QTBUG-127828 qt_add_translations: TS_FILE_DIR is ignored when
PLURALS_TS_FILE set
* QTBUG-128186 qlitehtml is built in a directory called "value-NOTFOUND"
* QTBUG-128411 Remove 'corefeatures.html' from qdoc manual
* QTBUG-123034 Accidental strikethrough (<s>) in QSpan documentation
* QTBUG-127352 lupdate's -extension option doesn't work
* QTBUG-80417 QDateTimeEdit cannot handle OffsetFromUTC or TimeZone as
time-spec
* PYSIDE-2492 uic does not generate enumeration name into enum values
causing type checking warnings
* QTBUG-127179 Qt Creator puts wrong fields for spacer objects
* QTBUG-119429 Top flaky test: tst_lupdate::good on Windows_11_22H2,
Windows_11_23H2, and Windows_10_22H2.
* PYSIDE-2840 Enum properties unsupported in Qt Designer custom widgets
* QTBUG-128368 Make sure that also qt6_ CMake commands are in the help
index
* QTBUG-128365 Wrong "Line"  (QFrame) orientation

### qttranslations
* QTBUG-125151 qt_add_translations CFBundleLocalizations broken

### qtdoc
* QTBUG-126104 Android mobile examples link redirects to WASM page
* QTBUG-124144 No buildings in osmbuildings - example
* QTBUG-55199 macdeployqt does not copy SVG image format plugins
* QTBUG-122683 Update trademark information
* QTBUG-127547 The link in INTEGRITY doc leads to Qt for wasm doc
* QTBUG-126866 Archiving the application does not have debug info files
(dSYM) included as expected
* QTBUG-127708 The Writing Source Code for Translation documentation
references undefined _NoOp functions
* QTBUG-124657 qsTrNoOp() is not defined in QML
* QTBUG-127814 Calqlatr fails to remove the unary minus character
* QTBUG-123164 New example demos/osmbuildings not compiling on Android
* QTBUG-127835 demos/lightningviewer not launching when installed
outside of build dir
* QTBUG-128225 Failing to deploy examples that link to dynamic lib qml
modules, but don't explicitly import them
* QTBUG-118038 Qt6WaylandCompositor could not be found because
dependency Wayland could   not be found
* QTBUG-122041 [DocumentViewer] The app is crashing when opening the
file on Android device
* QTBUG-126094 Spelling of Qt Qml/QML very inconsistent
* QTBUG-125329 Grpc generators: fix Policy CMP0071
* QTBUG-127926 Outdated Android docs still refer to
QtAndroid::androidActivity()

### qtpositioning
* QTBUG-127847 QtPositioning Android backend always checks for precise
location

### qtconnectivity
* QTBUG-123430 QBluetoothSocket::errorOccured is not emitted in certain
circumstances

### qtwayland
* QTBUG-124502 Drag and drop operation can crash the compositor
* QTBUG-126275 [REG Qt 6.6.3 -> 6.7.0] Wayland: Can't scroll with
mousewheel in editor
* QTBUG-118640 Qt sends the pointer event serial instead of the tablet
event serial in data_device:start_drag or xdg_toplevel::move.
* QTBUG-125878 Cannot pinch-to-zoom after the qt 6.7.1 upgrade
[regression]
* QTBUG-126313 QScroller gesture blocks mouse clicks
* QTBUG-113404 Wayland: Gestures are not delivered to correct top level
widget
* QTBUG-122197 QScreen::size is wrong on GNOME Wayland with 200% scaling
* QTBUG-125589 weired console message with simple application

### qt3d
* QTBUG-124891 Unredistributable files in qt3d / qtquick3d
* QTBUG-126251 Render to Texture broken following stereo rendering fixes
* QTBUG-128939 [REG 6.8.0 RC snapshot -> 6.8.0 RC snapshot]
Unredistributable files in qt3d

### qtimageformats
* QTBUG-127540 WebP: QImage detach in WebPPictureImportRGB(A) can cause
a crash
* QTBUG-127965 QImage not loading simple heic file

### qtwebsockets
* QTBUG-120492 QWebSocket connecting to an URL without a path sends GET
request without leading /

### qtwebengine
* QTBUG-125452 QT_FEATURE_webengine_system_icu=ON results in broken
runtime
* QTBUG-126138 Correct QML PdfSelection documentation
* QTBUG-126401 Qt webengine leaks its WebEngineQuickWidget
* QTBUG-125035 Webengine: issues compiling with ninja 1.12
* QTBUG-126722 WebEngine: GPU detection is missing "VmWare" in vendor
list
* QTBUG-127318 QWebEngineView findText does not clear previous
findText's highlight results at certain conditions
* QTBUG-111927 Link hovering may not change cursor shape in web view
* QTBUG-123889 Qt webengine doesn't update cursor properly when
entering/leaving widgets
* QTBUG-115929 [REG 6.3 -> 6.4/.5] Mouse cursor is pointer-only when
leaving window at bottom edge
* QTBUG-124878 --no-sandbox through command line does not seem to have
any effect
* QTBUG-124274 WebEngine build fails on openSUSE 15 due to libre2
* QTBUG-125300 Potential requirement on C runtime version for Qt 6.5.5
(and newer)?
* QTBUG-123790 Large number of warnings are output when exiting
QWebEngineView.
* QTBUG-128140 Dead link for QWebEngineScript::sourceUrl
* QTBUG-126256 [REG 6.6 -> 6.7] WebOTP crashes renderer process
* QTBUG-119908 HTML <select> Element Triggers Program Crash in QT on
EGLFS/KMS Platforms

### qtwebview
* QTBUG-70166 iOS Webview not able to return an object

### qtcharts
* QTBUG-127434 The labelsVisible property affects the titleVisible
property behavior if labelsVisible is set to false and titleVisible is
set to true.

### qtvirtualkeyboard
* QTBUG-127120 CMake error in qtvirtualkeyboard: CMake Error: The inter-
target dependency graph contains the following strongly connected
component (cycle)
* QTBUG-114551 [VKB] Selection handle coordinates fail to take
InputPanel's parent's transformation into account

### qtscxml
* QTBUG-128368 Make sure that also qt6_ CMake commands are in the help
index

### qtnetworkauth
* QTBUG-66415 Access token callback clears scope
* QTBUG-104655 QAbstractOAuth2::setState doesn't work as expected

### qtremoteobjects
* QTBUG-128368 Make sure that also qt6_ CMake commands are in the help
index

### qtquick3d
* QTBUG-125875 Manual test modelblendparticles segfaults on startup
* QTBUG-125876 Instanced models are not taken into account in shadow
mapping bounds
* QTBUG-126657 Car configurator demo: shadow mapping glitches
* QTBUG-120001 Game can be played in the results screen in Qt Quick 3D -
Quick Ball example
* QTBUG-127413 Building failure with FEATURE_quick_shadereffect=OFF
* QTBUG-119888 Texts overlap with each other in Qt Quick3D
* QTBUG-128370 Instance table cache not invalidated when instance table
is deleted
* QTBUG-124891 Unredistributable files in qt3d / qtquick3d

### qtopcua
* QTBUG-127840 Windows ARM: qtopcua -
Tst_QOpcUaSecurity::keyPairs(open62541) fails

### qthttpserver
* QTBUG-127333 FAIL! :
tst_QHttpServerResponse::mimeTypeDetection(image/svg+xml) Compared
values are not the same

### qtquick3dphysics
* QTBUG-127319 Add command line help for cooker
* QTBUG-100100 Demos should use `qt6_add_qml_module` instead of
`qt6_add_resources`

### qtgrpc
* QTBUG-127341 Error when building for Android: qqmlgrpchttp2channel.cpp
* QTBUG-127857 -skip-tests and -skip-examples are case sensitive
* QTBUG-127945 New example grpc/vehicle not compiling on iOS
* QTBUG-125328 Grpc genenerators: implicitly created export.qpb.h is
broken
* QTBUG-128368 Make sure that also qt6_ CMake commands are in the help
index

### qtquickeffectmaker
* QTBUG-126255 Qt Quick Effect Maker ships copyrighted Rawpixel-sourced
images in violation of Rawpixel's Business License
* QTBUG-111760 target_link_libraries(foo INTERFACE Qt::Core) fails for
interface libs with CMake < 3.19 on Windows

### qtgraphs
* QTBUG-126102 Grid on surface is not changing color
* QTBUG-125550 Incorrect interpretation of index 255 color in
QCustom3DVolume's colorTable

### qtapplicationmanager (Commercial only)
* QTBUG-128212 FAIL!  : qml::ApplicationManager::test_startAndStopAllApp
lications(StopAllApplications) Uncaught exception: Cannot read property
'modelData' of null

### qtinterfaceframework (Commercial only)
* QTBUG-127627 AttributeError: type object 'Path' has no attribute
'getcwd'
* QTBUG-124279 Interfaceframework examples don't get deployed to
embedded devices

### qtinsighttracker (Commercial only)
* QTBUG-126979 CMake error in dev' branch dependency update round:
package "Qt6InsightTracker"  is considered to be NOT FOUND

Known Issues
------------

Credits for the  release goes to:
---------------------------------

Eirik Aavitsland
Laszlo Agocs
Anu Aliyas
Even Oscar Andersen
Tim Angus
Viktor Arvidsson
Albert Astals Cid
Mate Barany
Vladimir Belyavsky
Nicholas Bennett
Tim Blechmann
Eskil Abrahamsen Blomfeldt
Joerg Bornemann
Rym Bouabid
Assam Boudjelthia
Kai Uwe Broulik
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
Amr Essam
David Faure
Nicolas Fella
Zoltan Gera
Robert Griebl
Magnus Groß
Kaj Grönholm
Richard Moe Gustavsen
Lucie Gérard
Mikko Hallamaa
Jøger Hansegård
Jani Heikkinen
Ulf Hermann
Volker Hilsheimer
Dominik Holland
Samuli Hölttä
Sam James
Allan Sandfeld Jensen
Jonas Karlsson
Timothée Keller
Igor Khanin
Ahmed El Khazari
Marius Kittler
Friedemann Kleint
Michal Klocek
Ingo Klöcker
Jarek Kobus
Tobias Koenig
Sze Howe Koh
Jarkko Koivikko
Tomi Korpipaa
Fabian Kosmale
Mike Krus
Santhosh Kumar
Kai Köhne
Inho Lee
Paul Lemire
Chris Lerner
Wladimir Leuschner
Thiago Macieira
Andras Mantia
Łukasz Matysiak
Jan Moeller
Safiyyah Moosa
Bartlomiej Moskal
Marc Mutz
Antti Määttä
Martin Negyokru
Andy Nichols
Mårten Nordheim
Tinja Paavoseppä
Karim Pinter
Timur Pocheptsov
Lorn Potter
Sakaria Pouke
Shyamnath Premnadh
MohammadHossein Qanbari
Liang Qi
Matthias Rauter
Topi Reinio
Shawn Rutledge
Toni Saario
Ahmad Samir
Philip Schuchardt
Luca Di Sera
Dmitry Shachnev
Sami Shalayel
Tian Shilin
Pierre-Yves Siret
Nils Petter Skålerud
Ivan Solovev
Axel Spoerl
Christian Strømme
Lars Sutterud
Jan Arve Sæther
Morten Sørvig
Sadegh Taghavi
Nodir Temirkhodjaev
Ivan Tkachenko
Orkun Tokdemir
Paul Olav Tvete
Fatih Uzunoglu
Sami Varanka
Niccolò Venerandi
Doris Verria
Tor Arne Vestbø
Petri Virkkunen
Ville Voutilainen
Juha Vuolle
Jaishree Vyas
Jannis Völker
Dongmei Wang
Michael Weghorn
Edward Welbourne
Paul Wicking
Piotr Wierciński
Milian Wolff
Oliver Wolff
Li Xinwei
Lu YaNing
Semih Yavuz
Wang Yu
Vlad Zahorodnii
JiDe Zhang
Liu Zheng
Michał Łoś
