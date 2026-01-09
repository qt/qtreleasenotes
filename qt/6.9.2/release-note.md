Release note
============
Qt 6.9.2 release is a patch release made on the top of Qt 6.9.1.
As a patch release, Qt 6.9.2 does not add any new functionality but provides
bug fixes and other improvements and maintains both forward and backward
compatibility (source and binary) with the 6.9.x series.

For detailed information about Qt 6.9, refer to the online documentation
included in this distribution. The documentation is also available online:

https://doc.qt.io/qt-6/index.html

The Qt version 6.9 series is binary compatible with the 6.8.x series.
Applications compiled for 6.8 will continue to run with 6.9.

Some of the changes listed in this file include issue tracking numbers
corresponding to tasks in the Qt Bug Tracker:

https://bugreports.qt.io/

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
* CVE-2025-5992 in qtbase
* CVE-2025-6338 in qtbase

### qtbase
* 23d3d83061d QSslCertificate: fromPath(): check the path arg isn't
  empty. fromPath() no longer accepts an empty path, which would
  previously result in searching the current directory.

* 4e785f1da52 QByteArray: make toDouble() reject space-only strings.
  Fixed an old regression that caused toDouble() and toFloat() to
  return ok = true for a string containing only whitespaces.

* 3915684fb80 dwrite: Support additional font names for system fonts.
  Fixed an issue where legacy names such as 'Arial Narrow' would no
  longer be listed as separate font families.

* c3e0c0099fe Use WS_EX_NOACTIVATE to prevent window from getting
  focused. Windows with flag Qt::WindowDoesNotAcceptFocus no longer
  have a taskbar entry.

* 81bc95704dd QFileSystemEngine::tempPath: bypass QDir and go straight
  to QFSEngine. tempPath() may now return a non-canonical path. This
  means going up from it (cdUp()) may result in different paths from
  string manipulation (adding "/..").

* b630f9fcbf6 iOS: Report inverted screen orientations via windowScene
  orientation. QScreen::orientation() now reflects the inverse portrait
  and landscape orientations, as long as system allows rotating the UI
  to those orientations.

* 8d08bc24130 QUrl: fix comparisons of URLs with password but no
  explicit username.  Fixed a number of bugs in QUrl where a URL
  modified using the setXxx() functions would fail to compare equal to
  itself after going through toString() and setUrl() round-trip.

* f90d762fdc5 Android: Set proper A11y-element java class names to
  support TalkBack.  Provide actual Android UI class names for
  TalkBack to improve a11y announcements.

* d0f58da7c79 Fail builds on Apple platforms with invalid Info.plist.
  Fail builds on Apple platforms if the Info.plist is invalid instead
  of generating corrupt application bundles.

* bec80b7a143 QWeakPointer: don't let IfCompatible<X> make accidental
  SMFs. Fixed a regression whereby the QWeakPointer<T> copy or move
  constructors and/or assignment operators may fail to compile for
  forward-declared (incomplete) T.

* 212f12513ed QTextStream: cope with multi-code-point signs. Fixed
  QTextStream::FieldAlignment::AlignAccountingStyle for locales that
  have negativeSign/positiveSign (-/+) that take more than one UTF-16
  code point (e.g. ar (Arabic)).

* ae8064b1daf QLocale: fix off-by-one error in codeToScript().  Fixed
  a bug where QLocale could not find the QLocale::Script with the
  highest value when looked up by string (codeToString() or
  QLocale(string) constructor).

* 391c716c163 Define macOS QOperatingSystemVersion constants using
  only major version.  QOperatingSystemVersion constants for macOS 11
  and up are now represented with their major version only, and minor
  and patch versions unspecified, as documented.

* b1d73418396 Upgrade Valgrind third-party component to v3.25.1.
  Updated Valgrind support to v3.25.1; this adds support for RISCV
  64-bit Linux.

* 20866f4d680 Update bundled libjpeg-turbo to version 3.1.1

* 921a838dcd7 Updated double-conversion to v3.3.1.

* c628ee2ab78 Update the public suffix list to upstream version
  2025-06-16_09-45-02_UTC.

* 943e8ac26f6 Update CLDR data, used by QLocale, to v47.

* eceb69e2259 Updated bundled libpng to version 1.6.48
* e2fac4bb336 Updated bundled libpng to version 1.6.49
* cced49ab911 Updated bundled libpng to version 1.6.50

* 80fdd12957b SQLite: Updated SQLite to v3.49.2
* 9d3390eb5d1 SQLite: Updated SQLite to v3.50.0
* c436e8ec43a SQLite: Updated SQLite to v3.50.1
* 041beef2900 SQLite: Updated SQLite to v3.50.2
* 4caa0ff9c56 SQLite: Updated SQLite to v3.50.3
* 2b85ac86ae6 SQLite: Updated SQLite to v3.50.4

* f394d470162 Upgraded Harfbuzz to 11.2.1
* 9834352b2ab Upgraded Harfbuzz to 11.3.3

### qtsvg
* d6642cd6 CMake: Added PURL and CPE info to the attribution files of
  3rd party sources.

### qtdeclarative
* 1b68ff0e94 CMake: Added PURL and CPE information to the attribution
  files of 3rd party sources.

### qtmultimedia
* 6e157a74a Updated FFmpeg version in documentation to n7.1.1.

* 7b253e40c CMake: Added PURL and CPE information to the attribution
  files of 3rd party sources.

### qttools
* dc3c1708c CMake: Added PURL and CPE information to the attribution
  files of 3rd party sources.

### qtpositioning
* 79c75b7e CMake: Added PURL and CPE information to the attribution
  files of 3rd party sources.

* dc1de9af Make: Fixed incorrect PURL version for clip2tri in
  qt_attribution.json.

### qtsensors
* 2558f3e9 CMake: Added PURL and CPE information to the attribution
  files of 3rd party sources.

### qtconnectivity
* 3eb18357 Added PURL and CPE information to the attribution files of
  3rd party sources.

### qtwayland
* 02047339 CMake: Added PURL and CPE information to the attribution
  files of 3rd party sources.

### qt3d
* da3e9f28b CMake: Added PURL and CPE information to the attribution
  files of 3rd party sources.

* 8307ac415 Updated assimp dependency to ASSIMP v6.0.2

### qtimageformats
* dbada64 CMake: Added PURL and CPE information to the attribution
  files of 3rd party sources.

* c217eda Updated bundled libwebp to version 1.6.0

### qtvirtualkeyboard
* d52f12ea CMake: Added PURL and CPE information to the attribution
  files of 3rd party sources.

### qtquick3d
* 6b5b9aeaa Updated meshoptimizer to v0.23

* 342584113 Updated TinyEXR to v1.0.12

* fb1fd94eb CMake: Added PURL and CPE information to the attribution
  files of 3rd party sources.

* f07867305 Update assimp to v6.0.2 to ASSIMP v6.0.2

### qtshadertools
* 2d6f06d CMake: Added PURL and CPE information to the attribution
  files of 3rd party sources.

### qt5compat
* 600ac9d CMake: Added PURL and CPE information to the attribution
  files of 3rd party sources.

### qtopcua
* 4e30fdaf Fix a bug where anonymous authentication over a secure
  connection was broken

* 6d80c4b2 Fix SimpleAttributeOperand conversion in the open62541
  plugin.  Fix an interoperability issue with the Siemens OPC UA
  server where the conditionId could not be selected in an event
  filter.

* 4be26219 CMake: Added PURL and CPE information to the attribution
  files of 3rd party sources.

* b57e476c Fix authentication over a None policy secure channel.
  Using encrypted auth tokens over a None security policy channel is
  again possible after it was broken with the update to open62541 1.4
  in Qt 6.9.

* 281f2a3e Fix error handling for security policy initialization.
  Fix a segfault if a client is initialized with a corrupt certificate
  file.

### qtgrpc
* 1bc8ff9e CMake: Added PURL and CPE information to the attribution
  files of 3rd party sources.

* 223dffbc Emit cancelled finished() in channel implementation.
  Cancellation logic should also emit finished now. Custom
  QAbstractGrpcChannel implementations should adapt their logic.

### qtapplicationmanager (Commercial only)
* e27b99de CMake: Added PURL and CPE information to the attribution
  files of 3rd party sources.

### qtinterfaceframework (Commercial only)
* 5eb3a222 CMake: Added PURL and CPE information to the attribution
  files of 3rd party sources.

* d35a10d1 Update the bundled copy of qface to the latest version,
  2.0.13.

### qtinsighttracker (Commercial only)
* 3916afe Add API for sending additional data.  Additional data can
  now be tracked without attaching it to any other event.


Fixes
-----

### qtbase
* [QTBUG-136348](https://bugreports.qt.io/browse/QTBUG-136348) Problem with macdeployqt not passing CN correctly
* [QTBUG-135800](https://bugreports.qt.io/browse/QTBUG-135800) [REG 6.8 → 6.9] XMLHttpRequest() errors from
qt.network.http2 and rest api data are not displaying to Multimedia
* [QTBUG-136609](https://bugreports.qt.io/browse/QTBUG-136609) Can't run appex with 6.8.3 or later
* [QTBUG-136210](https://bugreports.qt.io/browse/QTBUG-136210) Qt installer .pc files unusable due to spurious prefix
* [QTBUG-129568](https://bugreports.qt.io/browse/QTBUG-129568) tst_QWidget_window::mouseMoveWithPopup() failed on
Ubuntu 24.04 GNOME X11
* [QTBUG-129029](https://bugreports.qt.io/browse/QTBUG-129029) tst_QComboBox:popupPositionAfterStyleChange() failed on
Ubuntu 24.04 GNOME X11
* [QTBUG-136497](https://bugreports.qt.io/browse/QTBUG-136497) Android app fails to restart when permission is revoked
* [QTBUG-136077](https://bugreports.qt.io/browse/QTBUG-136077) [Regression 6.8.2->6.8.3] Android apps hang with black
screen or splash screen
* [QTBUG-135961](https://bugreports.qt.io/browse/QTBUG-135961) Blank screen when app is woken up from background
* [QTBUG-134419](https://bugreports.qt.io/browse/QTBUG-134419) systemCaCertificate() openssl backend walks current
working directory if system ca directory contains a broken symlink
* [QTBUG-126515](https://bugreports.qt.io/browse/QTBUG-126515) Buttons are too small, focus rectangle only seen at the
rounded corners
* [QTBUG-136453](https://bugreports.qt.io/browse/QTBUG-136453) QTableView auto-section-resize broken since Qt 6.9
* [QTBUG-136530](https://bugreports.qt.io/browse/QTBUG-136530) QFuture::isValid() without result
* [QTBUG-135945](https://bugreports.qt.io/browse/QTBUG-135945) QLatin1StringView documentation assumes knowledge of
string literals namespace
* [QTBUG-136678](https://bugreports.qt.io/browse/QTBUG-136678) Hardcoded paths used in
qt_generate_deploy_qml_app_script
* [QTBUG-125223](https://bugreports.qt.io/browse/QTBUG-125223)  Plugin's install_rpath error during deployment by
qt_generate_deploy_qml_app_script.
* [QTBUG-136485](https://bugreports.qt.io/browse/QTBUG-136485) QDockWidgets sends visibilityChanged on destruction
* [QTBUG-136083](https://bugreports.qt.io/browse/QTBUG-136083) qtypeinfo.h uses std::is_trivial_v which will be
deprecated in C++26
* [QTBUG-135978](https://bugreports.qt.io/browse/QTBUG-135978) Adding -ObjC linking flag breaks iOS build
* [QTBUG-136549](https://bugreports.qt.io/browse/QTBUG-136549) Race condition and crash when HTTP error received while
QHttp2Stream is uploading
* [QTBUG-136812](https://bugreports.qt.io/browse/QTBUG-136812) Bug in http header handling on WASM
* [QTBUG-136799](https://bugreports.qt.io/browse/QTBUG-136799) wasm: unicode alt code processing error when NumLock is
activated
* [QTBUG-135977](https://bugreports.qt.io/browse/QTBUG-135977) [REG 6.8.2 -> 6.8.3] WASM: Loaded Roboto Flex font
rendered as italic by default
* [QTBUG-135315](https://bugreports.qt.io/browse/QTBUG-135315) Possible regression in handling of special style names
* [QTBUG-136968](https://bugreports.qt.io/browse/QTBUG-136968) qstring.h:1125:40: error: '= delete' with a message is a
C++2c extension
* [QTBUG-133746](https://bugreports.qt.io/browse/QTBUG-133746) QFileSystemModel with wrong path of top-directory of a
drive
* [QTBUG-133332](https://bugreports.qt.io/browse/QTBUG-133332) possible stackoverflow calling setWindowFlag() in style
polish & unpolish
* [QTBUG-136493](https://bugreports.qt.io/browse/QTBUG-136493) FFmpeg not properly configured with multi-abi builds
* [QTBUG-135481](https://bugreports.qt.io/browse/QTBUG-135481) Android TV system keyboard doesn't process input
correctly
* [QTBUG-134110](https://bugreports.qt.io/browse/QTBUG-134110) wasm mkspec distclean deleting all *.html and *.js files
* [QTBUG-137146](https://bugreports.qt.io/browse/QTBUG-137146) CMake error when finding qttools tools
* [QTBUG-135722](https://bugreports.qt.io/browse/QTBUG-135722) Compile Android without desktopservices -feature
* [QTBUG-135283](https://bugreports.qt.io/browse/QTBUG-135283) SafeArea margins not populated
* [QTBUG-135227](https://bugreports.qt.io/browse/QTBUG-135227) QML SafeArea type only works if full screen is entered
first
* [QTBUG-135808](https://bugreports.qt.io/browse/QTBUG-135808) Some problems with Expanded Client Areas on Android
* [QTBUG-111993](https://bugreports.qt.io/browse/QTBUG-111993) QNetworkAccessManager docs: minor typo referencing non-
existent method
* [QTBUG-137168](https://bugreports.qt.io/browse/QTBUG-137168) QtMultimedia fails to install: Cannot find
'plugins/multimedia/libmockmultimediaplugin.a' to compute its checksum
* [QTBUG-137038](https://bugreports.qt.io/browse/QTBUG-137038) QByteArray::toDouble() behavior changed on whitespaces
only string
* [QTBUG-135817](https://bugreports.qt.io/browse/QTBUG-135817) [REG 6.7.2 -> Qt 6.8.2] Windows:
QFontDatabase::families() does not list stylistic variants of families
* [QTBUG-137130](https://bugreports.qt.io/browse/QTBUG-137130) Qt Creator crash on exit accessing destroyed event
dispatcher
* [QTBUG-131714](https://bugreports.qt.io/browse/QTBUG-131714) [Windows] Finishing system move activates the window
even if Qt.WindowDoesNotAcceptFocus is set
* [QTBUG-135489](https://bugreports.qt.io/browse/QTBUG-135489) [REG 6.8.2->6.8.3] Handling of custom scheme URL is
broken
* [QTBUG-135376](https://bugreports.qt.io/browse/QTBUG-135376) Fullscreen virtual keyboard key handling
* [QTBUG-128745](https://bugreports.qt.io/browse/QTBUG-128745) [QuickControls] Text inputs displayed as extracted view
in landscape orientation
* [QTBUG-130058](https://bugreports.qt.io/browse/QTBUG-130058) Android Virtual keyboard is broken in landscape mode
* [QTBUG-136710](https://bugreports.qt.io/browse/QTBUG-136710) QML Image object causes a crash when it gets deleted
while it's still loading
* [QTBUG-131655](https://bugreports.qt.io/browse/QTBUG-131655) Memory leak in QNSViewMenuHelper
* [QTBUG-137161](https://bugreports.qt.io/browse/QTBUG-137161) "Leaks" utility in the Instruments app report memory
leak.
* [QTBUG-137316](https://bugreports.qt.io/browse/QTBUG-137316) generateJavaQmlComponents will scan relevant import
directories twice
* [QTBUG-137277](https://bugreports.qt.io/browse/QTBUG-137277) Stack overflow in QFontEngine (due to infinite
recursion)
* [QTBUG-137198](https://bugreports.qt.io/browse/QTBUG-137198) Configure fails with -DFEATURE_sanitize_thread=ON
-DFEATURE_sanitize_address=ON without a proper message
* [QTBUG-135652](https://bugreports.qt.io/browse/QTBUG-135652) Using QIcon from png and svg file in a toolbar with
>100% scaler ratio causes wrong icon size to be picked elsewhere
* [QTBUG-136550](https://bugreports.qt.io/browse/QTBUG-136550) QMYSQL: QT application built with libmariadb3.4 won't
connect to MariaDB 10
* [QTBUG-133687](https://bugreports.qt.io/browse/QTBUG-133687) Confusing instructions when atomicfptr config.test fails
* [QTBUG-136229](https://bugreports.qt.io/browse/QTBUG-136229) Fullscreen virtual keyboard: issue with selection and
delete
* [QTBUG-137398](https://bugreports.qt.io/browse/QTBUG-137398) A crash occurred in C:\Users\qt\work\qt\qtdeclarative_st
andalone_tests\tests\auto\quickdialogs\qquickfontdialogimpl\tst_qquickfo
ntdialogimpl.exe
* [QTBUG-135634](https://bugreports.qt.io/browse/QTBUG-135634) macOS: Deleted menu is not removed from native menu bar
* [QTBUG-137297](https://bugreports.qt.io/browse/QTBUG-137297) qmake iOS target: fails to find (prebuilt) .prl
dependencies -> Xcode build fails
* [QTBUG-137108](https://bugreports.qt.io/browse/QTBUG-137108) CE_ComboBoxLabel painting not called anymore on
QProxyStyle, due to QStyleSheetStyle
* [QTBUG-131761](https://bugreports.qt.io/browse/QTBUG-131761) Incorrect display of :selected state of QCombobox on
"windows" style plugin
* [QTBUG-136074](https://bugreports.qt.io/browse/QTBUG-136074) QTreeView a11y: Frequent Qt Creator crashes when Orca
screen reader is active
* [QTBUG-133855](https://bugreports.qt.io/browse/QTBUG-133855)  QtreeView sporadic crash when setCurrentIndex is called
* [QTBUG-134602](https://bugreports.qt.io/browse/QTBUG-134602) Rendering of QQuickText slightly elevated.
* [QTBUG-133904](https://bugreports.qt.io/browse/QTBUG-133904) Corrupted qml rendering on some Android PowerVR devices
after the app is killed
* [QTBUG-134245](https://bugreports.qt.io/browse/QTBUG-134245) [Reg 6.8.0 -> 6.8.2] Strange 4-quadrant colouration of
Qt Quick items
* [QTBUG-134089](https://bugreports.qt.io/browse/QTBUG-134089) Power VR rendering failure on Qt 6.8.2
* [QTBUG-135411](https://bugreports.qt.io/browse/QTBUG-135411) Android visual Glitches on 6.8.2+
* [QTBUG-134496](https://bugreports.qt.io/browse/QTBUG-134496) Drawing errors on some Android devices
* [QTBUG-135810](https://bugreports.qt.io/browse/QTBUG-135810) [REG 6.8.1 -> 6.8.3] Crashes in QRhi::endFrame /
glDrawElements on Android
* [QTBUG-136590](https://bugreports.qt.io/browse/QTBUG-136590) Regression in QTextTable: border-collapse cell border
rendering broken
* [QTBUG-133407](https://bugreports.qt.io/browse/QTBUG-133407) Tools in qtbase fail to link to QtCore when Qt is
statically built
* [QTBUG-137249](https://bugreports.qt.io/browse/QTBUG-137249) QML Screen.orientation on iOS does not provide all
directions
* [QTBUG-137011](https://bugreports.qt.io/browse/QTBUG-137011) The icon of the QCommandLinkButton does not update when
the button's visibility is set to true.
* [QTBUG-137329](https://bugreports.qt.io/browse/QTBUG-137329) QFileDialog::getOpenFileContent opens a non-modal dialog
* [QTBUG-137427](https://bugreports.qt.io/browse/QTBUG-137427) HTTP 2 request cancellation timing issue may lead to
severed connection
* [QTBUG-135844](https://bugreports.qt.io/browse/QTBUG-135844) Windows: QPainter errors when maximizing/resizing window
* [QTBUG-137041](https://bugreports.qt.io/browse/QTBUG-137041) Schannel plugin incorrectly verifies the
NetscapeCertType extension
* [QTBUG-137346](https://bugreports.qt.io/browse/QTBUG-137346) [Reg 6.8.0->6.8.1]QTableView ignores the stylesheet
background color when hovering over the items.
* [QTBUG-126743](https://bugreports.qt.io/browse/QTBUG-126743) If QT_ANDROID_PACKAGE_SOURCE_DIR is set to a specific
path, a build folder is recursively created within the build folder.
* [QTBUG-133656](https://bugreports.qt.io/browse/QTBUG-133656) During Transition from DST back to standard time. the
local clock time repeats an hour.
* [QTBUG-113401](https://bugreports.qt.io/browse/QTBUG-113401) QtConcurrent::run parameter order documentation wrong
* [QTBUG-137157](https://bugreports.qt.io/browse/QTBUG-137157) [macOS] QAccessibleInterface::window() is never called;
accessibility tools cannot see the top-level window that holds a
widget/Item
* [QTBUG-25938](https://bugreports.qt.io/browse/QTBUG-25938) Checkable QGroupBox doesn't keep "enabled" status of
children
* [QTBUG-136055](https://bugreports.qt.io/browse/QTBUG-136055) QWebSocketServer creates persistent files in
Microsoft/Crypto/RSA on each new client connection.
* [QTBUG-135337](https://bugreports.qt.io/browse/QTBUG-135337) crash when connecting with RDP
* [QTBUG-133221](https://bugreports.qt.io/browse/QTBUG-133221) [REG: 6.7->6.8] SVG file mime type not recognized if the
file contains xml header
* [QTBUG-136990](https://bugreports.qt.io/browse/QTBUG-136990) QML property information rendered mangled (Assistant, Qt
Creator)
* [QTBUG-136097](https://bugreports.qt.io/browse/QTBUG-136097) Can't use the properties and signals when definitions
such as them are enabled by `__has_include`
* [QTBUG-136960](https://bugreports.qt.io/browse/QTBUG-136960) Checkbox in QTreeview shows black outline in dark mode
* [QTBUG-137579](https://bugreports.qt.io/browse/QTBUG-137579) QDebugStateSaver not documented well
* [QTBUG-137467](https://bugreports.qt.io/browse/QTBUG-137467) qt.qpa.wayland: wrong transient parent of the popup
* [QTBUG-109599](https://bugreports.qt.io/browse/QTBUG-109599) Password characters are not visible with a screenreader
* [QTBUG-136176](https://bugreports.qt.io/browse/QTBUG-136176) [Reg 6.8.3 -> 6.9.0]QIcon::ThemeIcon::DialogInformation
is missing pixels.
* [QTBUG-134604](https://bugreports.qt.io/browse/QTBUG-134604) edit-redo icon is clipped on Windows
* [QTBUG-96379](https://bugreports.qt.io/browse/QTBUG-96379) Missing documentation for QMetaContainer
* [QTBUG-137755](https://bugreports.qt.io/browse/QTBUG-137755) Regression: Segfault on closing a program using
QDockWidgets, introduced by ab6f1ad77852a427ae73172ca11dacf876a0cbf7
* [QTBUG-137763](https://bugreports.qt.io/browse/QTBUG-137763) windeployqt crash when run through cmake
* [QTBUG-120031](https://bugreports.qt.io/browse/QTBUG-120031) xcb: Modal state may get lost due to a race
* [QTBUG-133029](https://bugreports.qt.io/browse/QTBUG-133029) Documentation is inconsistent wrt QChronoTimer
* [QTBUG-123063](https://bugreports.qt.io/browse/QTBUG-123063) XCB flakiness in tst_qgraphicsscene (race condition
caused by the event dispatcher on Linux)
* [QTBUG-87180](https://bugreports.qt.io/browse/QTBUG-87180) Typo in the description of QGraphicsSimpleTextItem class
* [QTBUG-137838](https://bugreports.qt.io/browse/QTBUG-137838) QMultiHash has undocumented erase method
* [QTBUG-130978](https://bugreports.qt.io/browse/QTBUG-130978) Auto-scrolling breaks when dragging and dropping an item
in QTreeView.
* [QTBUG-137452](https://bugreports.qt.io/browse/QTBUG-137452) compile error in moc-generated code if slot/property
name equals return type name
* [QTBUG-137700](https://bugreports.qt.io/browse/QTBUG-137700) QIcon::pixmap selects wrong icon file from theme
* [QTBUG-90634](https://bugreports.qt.io/browse/QTBUG-90634) QIcon not preferring Hi DPI pixmaps when scaling
* [QTBUG-136130](https://bugreports.qt.io/browse/QTBUG-136130) background color of QTreeViewItems with windows 11 style
* [QTBUG-137882](https://bugreports.qt.io/browse/QTBUG-137882) top-level build, examples don't respect -linker
configure option
* [QTBUG-137850](https://bugreports.qt.io/browse/QTBUG-137850) moc_qwaylandxdgshell.cpp:625:60: error: template
argument 1 is invalid
* [QTBUG-138043](https://bugreports.qt.io/browse/QTBUG-138043) QMultiMap documentation error
* [QTBUG-133631](https://bugreports.qt.io/browse/QTBUG-133631) wasm: TextField with echo mode password should not try
to autocomplete
* [QTBUG-134795](https://bugreports.qt.io/browse/QTBUG-134795) Add note about HAVE_TICK_COUNTER dependency
* [QTBUG-130765](https://bugreports.qt.io/browse/QTBUG-130765) Fix excessive use of note sections in QDateTime
documentation
* [QTBUG-113759](https://bugreports.qt.io/browse/QTBUG-113759) Sort alphabetically the list items on
https://doc.qt.io/qt-6/stylesheet-reference.html
* [QTBUG-78013](https://bugreports.qt.io/browse/QTBUG-78013) QIdentityProxyModel::match inappropriately mixes use of
proxy model index and source model data method
* [QTBUG-125319](https://bugreports.qt.io/browse/QTBUG-125319) Scaling issue occurs when the window is moved due to
disconnecting the screen.
* [QTBUG-102240](https://bugreports.qt.io/browse/QTBUG-102240) QStringList incorrect inheritance documentation
* [QTBUG-49564](https://bugreports.qt.io/browse/QTBUG-49564) QTextCharFormat fontPointSize() doesnt not return the
same as QTextCharFormat font().pointSize()
* [QTBUG-136217](https://bugreports.qt.io/browse/QTBUG-136217) Windows11 style does not show underlying content of
index widget.
* [QTBUG-119501](https://bugreports.qt.io/browse/QTBUG-119501) Numbers colliding and not highlighted in Charts with
Widgets Gallery example
* [QTBUG-138172](https://bugreports.qt.io/browse/QTBUG-138172) a11y: QToolButton menu not exposed on a11y layer when it
comes from default action
* [QTBUG-137344](https://bugreports.qt.io/browse/QTBUG-137344) a11y AT-SPI: org.freedesktop.DBus.Properties "GetAll"
queries trigger application crash
* [QTBUG-95325](https://bugreports.qt.io/browse/QTBUG-95325) Removal of QTextStream::setCodec is not documented
* [QTBUG-137806](https://bugreports.qt.io/browse/QTBUG-137806) [Android][A11y] Role of UI elements is missing
* [QTBUG-138201](https://bugreports.qt.io/browse/QTBUG-138201) Arranging QDockWidgets programatically causes
segmentation faults
* [QTBUG-138196](https://bugreports.qt.io/browse/QTBUG-138196) [REG dev] Fusion: Buttons and comboboxes outlined
* [QTBUG-59186](https://bugreports.qt.io/browse/QTBUG-59186) Error in QIODevice::readLine() documentation about
handling newline char
* [QTBUG-137438](https://bugreports.qt.io/browse/QTBUG-137438) [REG 6.9.0 -> 6.9.1] QTemporaryFile
* [QTBUG-112692](https://bugreports.qt.io/browse/QTBUG-112692) QPropertyNotifier and related APIs have no \since
version
* [QTBUG-88466](https://bugreports.qt.io/browse/QTBUG-88466) Thread safety of QTranslator::translate
* [QTBUG-137587](https://bugreports.qt.io/browse/QTBUG-137587) qtdeclarative: do_compile failed when building with high
parallelism.
* [QTBUG-133725](https://bugreports.qt.io/browse/QTBUG-133725) qml_tool_autogen target loses almost all dependencies on
other autogen and sync_headers targets
* [QTBUG-137986](https://bugreports.qt.io/browse/QTBUG-137986) rhi/vulkan: Do something about VUID-vkQueueSubmit-
pSignalSemaphores-00067
* [QTBUG-138130](https://bugreports.qt.io/browse/QTBUG-138130) QTableView misrendered since qt 6.9
* [QTBUG-129242](https://bugreports.qt.io/browse/QTBUG-129242) QTableWidget selection issue
* [QTBUG-137776](https://bugreports.qt.io/browse/QTBUG-137776) Windows11 style, QTableView cell selection behavior
* [QTBUG-138158](https://bugreports.qt.io/browse/QTBUG-138158) QT_DISCARD_FILE_CONTENTS does not work as expected
* [QTBUG-132590](https://bugreports.qt.io/browse/QTBUG-132590) Unclear relation between
QTemporaryFile::{autoRemove,rename}()
* [QTBUG-128794](https://bugreports.qt.io/browse/QTBUG-128794) QLineEdit in Android - no text visual
* [QTBUG-133549](https://bugreports.qt.io/browse/QTBUG-133549) Qt UI stops redrawing on Android
* [QTBUG-128457](https://bugreports.qt.io/browse/QTBUG-128457) QSpinBox does not respond correctly to Android keyboard
* [QTBUG-128422](https://bugreports.qt.io/browse/QTBUG-128422) [Android] Can't change selection in QComboBox with touch
input
* [QTBUG-121757](https://bugreports.qt.io/browse/QTBUG-121757) Entered text is invisible in QLineEdit until field focus
is changed
* [QTBUG-138261](https://bugreports.qt.io/browse/QTBUG-138261) QPlatformBackingStore doesn't handle QtGui-level
fractional scaling
* [QTBUG-117414](https://bugreports.qt.io/browse/QTBUG-117414) Doc: Give hints how to get a QScreen object
* [QTBUG-137120](https://bugreports.qt.io/browse/QTBUG-137120) [Regression] Right and top dockwidget area are not
resizable anymore
* [QTBUG-60355](https://bugreports.qt.io/browse/QTBUG-60355) QMetaEnum docs have no code examples
* [QTBUG-138183](https://bugreports.qt.io/browse/QTBUG-138183) The drop area for QToolBar gets triggered even when the
toolbar is not on the window.
* [QTBUG-138032](https://bugreports.qt.io/browse/QTBUG-138032) calqlatr: Example prints 'stale focus object [...],
doing manual update' warnings
* [QTBUG-138256](https://bugreports.qt.io/browse/QTBUG-138256) QPlatformInputContext::update() called with stale focus
object
* [QTBUG-136138](https://bugreports.qt.io/browse/QTBUG-136138) Blank screen in CarPlay Simulator with Qt-based iOS app
due to assertion: "[scene isKindOfClass:UIWindowScene.class]" in
qiosapplicationdelegate.mm
* [QTBUG-137978](https://bugreports.qt.io/browse/QTBUG-137978) Qt.inputMethod.visible changes to true in orientation
change on iOS26 beta
* [QTBUG-138230](https://bugreports.qt.io/browse/QTBUG-138230) QCheckBox used as editor in delegate does not display
checkmark when using Windows11 style and no text
* [QTBUG-135213](https://bugreports.qt.io/browse/QTBUG-135213) QTreeView creates ghost artifacts when scrolling
* [QTBUG-120254](https://bugreports.qt.io/browse/QTBUG-120254) Cell value leaking into other cells when entering new
value
* [QTBUG-133845](https://bugreports.qt.io/browse/QTBUG-133845)  QSpinBoxes take too much vertical space if an
application-wide style sheet is set since Qt 6.8.2
* [QTBUG-130642](https://bugreports.qt.io/browse/QTBUG-130642) Incorrect QAbstractSpinBox size hint in Windows 11 style
when style sheet is set
* [QTBUG-132431](https://bugreports.qt.io/browse/QTBUG-132431) Stylesheet Margin/Padding squashes QSpinBox
* [QTBUG-138428](https://bugreports.qt.io/browse/QTBUG-138428) tst_QTextStream::pos3LargeFile() takes an extraordinary
amount of time to execute
* [QTBUG-138435](https://bugreports.qt.io/browse/QTBUG-138435) QTextStream::pos() seems to be linear over QFile size
(or QFile::pos())
* [QTBUG-138238](https://bugreports.qt.io/browse/QTBUG-138238) NPE when calling QtNetwork.unregisterReceiver() at exit
* [QTBUG-135928](https://bugreports.qt.io/browse/QTBUG-135928) Connection to D-Bus signals silently breaks if D-Bus was
used before creating QCoreApplication
* [QTBUG-138401](https://bugreports.qt.io/browse/QTBUG-138401) [REG dev] Windows11 Style: Check-boxes' drawing
regression
* [QTBUG-138094](https://bugreports.qt.io/browse/QTBUG-138094) Radiobuttons/Checkboxes in windows11 style do not follow
WinUI3 style
* [QTBUG-137027](https://bugreports.qt.io/browse/QTBUG-137027) GetMethodID received NULL jclass
* [QTBUG-138484](https://bugreports.qt.io/browse/QTBUG-138484) QTextStream assumes single-character
QLocale::{positive,negative}Sign()
* [QTBUG-138168](https://bugreports.qt.io/browse/QTBUG-138168) Fix a typo in the licenseRule.json file in qtbase
* [QTBUG-138008](https://bugreports.qt.io/browse/QTBUG-138008) Permissions test app crashes on emulator.
* [QTBUG-138206](https://bugreports.qt.io/browse/QTBUG-138206) a11y: Docked QDockWidget reports incorrect role and
window-relative position via AT-SPI
* [QTBUG-138566](https://bugreports.qt.io/browse/QTBUG-138566) QLocale::codeToScript() can't find QLocale::LastScript
* [QTBUG-138585](https://bugreports.qt.io/browse/QTBUG-138585) tst_qxmlstream failed on webOS building
* [QTBUG-86287](https://bugreports.qt.io/browse/QTBUG-86287) Static 5.15.0 compile results in "undefined reference to
xcb_aux_create_gc"
* [QTBUG-137004](https://bugreports.qt.io/browse/QTBUG-137004) xcb-image is missing dependency on xcb-aux
* [QTBUG-134757](https://bugreports.qt.io/browse/QTBUG-134757) [REG 6.7.3->6.8.0] QWidgetAction: No contextMenuEvent
* [QTBUG-127705](https://bugreports.qt.io/browse/QTBUG-127705) Android splashscreen not removed
* [QTBUG-124140](https://bugreports.qt.io/browse/QTBUG-124140) [REG]: 6.7.0  full-screen app displays background window
(or splash-screen) graphics at top/bottom during multiwindow split
display
* [QTBUG-136163](https://bugreports.qt.io/browse/QTBUG-136163) sbom/spdx file not reproducible (contains build path)
* [QTBUG-138660](https://bugreports.qt.io/browse/QTBUG-138660) QHttp2Stream: dtor missing sendRST_STREAM for some
state(s)
* [QTBUG-138156](https://bugreports.qt.io/browse/QTBUG-138156) tst_QHttpServer::disconnectedInEventLoop leaves a bad
state making multipleRequests fail
* [QTBUG-138013](https://bugreports.qt.io/browse/QTBUG-138013) Content_uri test fails on Pixel6a Device
* [QTBUG-126531](https://bugreports.qt.io/browse/QTBUG-126531) Manual test android_content_uri fails
* [QTBUG-123319](https://bugreports.qt.io/browse/QTBUG-123319) android_content_uri test crashes when trying to get size
of nonexistent file.
* [QTBUG-134912](https://bugreports.qt.io/browse/QTBUG-134912) Manual test android_content_uri crash on exit
* [QTBUG-110240](https://bugreports.qt.io/browse/QTBUG-110240) "Use qtbase/tests/manual/android_content_uri" is not
found on the installation
* [QTBUG-132403](https://bugreports.qt.io/browse/QTBUG-132403) manual test android_content_uri fails.
* [QTBUG-129324](https://bugreports.qt.io/browse/QTBUG-129324) Don't print exceptions for content file operations that
are supposed to be done under the hood
* [QTBUG-134740](https://bugreports.qt.io/browse/QTBUG-134740) [REG 6.7.3 -> 6.8.0] QDir::entryInfoList slower
accessing SMB share from macOS
* [QTBUG-138374](https://bugreports.qt.io/browse/QTBUG-138374) QFileSystemWatcher::addPath() is slow on macos
* [QTBUG-138372](https://bugreports.qt.io/browse/QTBUG-138372) QLocalSocket never emits ConnectedState in Linux
* [QTBUG-123585](https://bugreports.qt.io/browse/QTBUG-123585) Memory Leak: QGestureRecognizer::unregisterRecognizer()
* [QTBUG-85428](https://bugreports.qt.io/browse/QTBUG-85428) Documentation for QScrollBar can be improved
* [QTBUG-33977](https://bugreports.qt.io/browse/QTBUG-33977) Suggested change to QCoreApplication documentation
* [QTBUG-106709](https://bugreports.qt.io/browse/QTBUG-106709) Application looks too small on an external display with
iPadOS 16.1 on M1 iPad
* [QTBUG-137544](https://bugreports.qt.io/browse/QTBUG-137544) QML iPad app window stays black when launched on
external display
* [QTBUG-131448](https://bugreports.qt.io/browse/QTBUG-131448) Cannot QMovie::moveToThread
* [QTBUG-138157](https://bugreports.qt.io/browse/QTBUG-138157) QWindow::safeAreaMargins() returns incorrect values when
virtual keyboard opens on Android (Qt 6.9)
* [QTBUG-129027](https://bugreports.qt.io/browse/QTBUG-129027) tst_QStatusBar::QTBUG4334_hiddenOnMaximizedWindow()
failed on Ubuntu 24.04 GNOME X11
* [QTBUG-131513](https://bugreports.qt.io/browse/QTBUG-131513) [iOS] QSysInfo::productVersion() incomplete?
* [QTBUG-136629](https://bugreports.qt.io/browse/QTBUG-136629) QUnifiedTimer::updateAnimationTimers() crashes when
QApplication is recreated
* [QTBUG-68865](https://bugreports.qt.io/browse/QTBUG-68865) tst_QMenuBar::check_menuPosition autotest fails on Ubuntu
18.04
* [QTBUG-138864](https://bugreports.qt.io/browse/QTBUG-138864) qt-android-runner.py doesn't find package name
* [QTBUG-135964](https://bugreports.qt.io/browse/QTBUG-135964) Windows theme uses wrong colors if high-contrast mode is
activated
* [QTBUG-135641](https://bugreports.qt.io/browse/QTBUG-135641) QNetworkDiskCache leaks file descriptors
* [QTBUG-138922](https://bugreports.qt.io/browse/QTBUG-138922) Consistent Qt caused crash when navigating with Jetpack
Compose
* [QTBUG-136101](https://bugreports.qt.io/browse/QTBUG-136101) Minimal configuration compile with autotests
* [QTBUG-136687](https://bugreports.qt.io/browse/QTBUG-136687) [regression 6.9.0] Wasm LibreOffice no longer gets
keyboard input events
* [QTBUG-136562](https://bugreports.qt.io/browse/QTBUG-136562) tabbing between textfields and buttons does not work
* [QTBUG-136722](https://bugreports.qt.io/browse/QTBUG-136722) [VxWorks] qthread_unix contains DKM related code
* [QTBUG-136716](https://bugreports.qt.io/browse/QTBUG-136716) QDockWidget glitches when moving/pushing unless undocked
and redocked
* [QTBUG-122590](https://bugreports.qt.io/browse/QTBUG-122590) Transparency not working correctly for Window Embedding
in QML
* [QTBUG-135859](https://bugreports.qt.io/browse/QTBUG-135859) WindowContainer cannot handle transparent Window
properly
* [QTBUG-136755](https://bugreports.qt.io/browse/QTBUG-136755) QQuickWindow::grabWindow() results in a black background
color instead of being transparent with the Offscreen platform.
* [QTBUG-87776](https://bugreports.qt.io/browse/QTBUG-87776) Move Qt::FooPrivate targets into separate CMake packages
* [QTBUG-135044](https://bugreports.qt.io/browse/QTBUG-135044) tst_QStringApiSymmetry fails under ASAN
(GenerationalCollator is leaked?)
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
* [QTBUG-134105](https://bugreports.qt.io/browse/QTBUG-134105) tst_qscroller::overshoot() is flaky on macOS
* [QTBUG-134900](https://bugreports.qt.io/browse/QTBUG-134900) QUrl's operator==() is taking bygone data into account
* [QTBUG-134896](https://bugreports.qt.io/browse/QTBUG-134896) QUrl's qHash() is inconsistent with its operator==
* [QTBUG-134208](https://bugreports.qt.io/browse/QTBUG-134208) Mnemonic annotation is passed to screen readers
* [QTBUG-137005](https://bugreports.qt.io/browse/QTBUG-137005) Qt6::qmltestrunner target no longer available
* [QTBUG-135626](https://bugreports.qt.io/browse/QTBUG-135626) QPointer causes unneccessary (invalid) downcasts
* [QTCREATORBUG-32932](https://bugreports.qt.io/browse/QTCREATORBUG-32932) Automatic selection of too low Android SDK version
* [QTBUG-138246](https://bugreports.qt.io/browse/QTBUG-138246) Q{Shared,Weak}Pointer::IfCompatible cause accidental
copy/move SMFs, causing FTBFS in qtdeclarative
* [QTBUG-138155](https://bugreports.qt.io/browse/QTBUG-138155) qt_generate_deploy_qml_app_script: Error for space in
output name
* [QTBUG-138471](https://bugreports.qt.io/browse/QTBUG-138471) QString::arg() convert floating type to integer
* [QTBUG-138192](https://bugreports.qt.io/browse/QTBUG-138192) Android Templates, Manifest and CMake Properties
* [QTBUG-135413](https://bugreports.qt.io/browse/QTBUG-135413) Accessible.announce not working on iOS and Android
* [QTBUG-138562](https://bugreports.qt.io/browse/QTBUG-138562) QLocalePrivate::codeToLanguage() does not sanitize the
input before passing it to AlphaCode
* [QTBUG-138610](https://bugreports.qt.io/browse/QTBUG-138610) QTemporaryFile::rename() overwrites existing file on
Android
* [QTBUG-132617](https://bugreports.qt.io/browse/QTBUG-132617) Unclear behaviour of QTemporaryFile::rename()
* [QTBUG-138583](https://bugreports.qt.io/browse/QTBUG-138583) QLocale::toUpper() is not 64-bit-safe on ICU
* [QTBUG-137126](https://bugreports.qt.io/browse/QTBUG-137126) QAccessible::ActionChanged event not sent anywhere in Qt
* [QTBUG-2163](https://bugreports.qt.io/browse/QTBUG-2163) Support for conditions in special casing of unicode
characters is missing in Qt
* [QTBUG-138705](https://bugreports.qt.io/browse/QTBUG-138705) Windows backend of QLocale::toLower() does not implement
Greek Final Sigma rule
* [QTBUG-138527](https://bugreports.qt.io/browse/QTBUG-138527) Replace direct links to https://doc.qt.io/qt-6/
* [QTBUG-136045](https://bugreports.qt.io/browse/QTBUG-136045) macOS: Window geometry is not updated correctly when the
OS rejects a change by setGeometry
* [QTBUG-107907](https://bugreports.qt.io/browse/QTBUG-107907) QOperatingSystemVersion::Windows10 <
QOperatingSystemVersion::Windows11 == false
* [QTBUG-132398](https://bugreports.qt.io/browse/QTBUG-132398) Unsupported linker script to make objective-c classnames
unique is broken since Xcode14
* [QTBUG-138851](https://bugreports.qt.io/browse/QTBUG-138851) Quadratic behaviour in qlocale.cpp when building
uiLanguages
* [QTBUG-138831](https://bugreports.qt.io/browse/QTBUG-138831) [VxWorks] EDOOM handling is missing from 6.x
* [QTBUG-134546](https://bugreports.qt.io/browse/QTBUG-134546) [VxWorks] exit on poll error should be on by default
like in 5.15
* [QTBUG-137860](https://bugreports.qt.io/browse/QTBUG-137860) [Windows][A11y] Text can not be selected by NVDA

### qtsvg
* [QTBUG-126482](https://bugreports.qt.io/browse/QTBUG-126482) QtSvg ignores units
* [QTBUG-135483](https://bugreports.qt.io/browse/QTBUG-135483) [REG 6.7-> 6.8] Loading order affects QIcon state and
mode when adding svg images
* [QTBUG-123817](https://bugreports.qt.io/browse/QTBUG-123817) QTextLayout::draw() renders text as path and not text
* [QTBUG-126268](https://bugreports.qt.io/browse/QTBUG-126268) Text rendering does not handle fill and stroke opacities
correctly
* [QTBUG-137700](https://bugreports.qt.io/browse/QTBUG-137700) QIcon::pixmap selects wrong icon file from theme

### qtdeclarative
* [QTBUG-136256](https://bugreports.qt.io/browse/QTBUG-136256) When menu items are dynamically added to Menu, it should
resize to fit
* [QTBUG-136735](https://bugreports.qt.io/browse/QTBUG-136735) Line: 1: Internal process (QML Puppet) crashed.
* [QTBUG-128864](https://bugreports.qt.io/browse/QTBUG-128864) Vulkan RHI Renderer freezes on Windows sometimes after
pressing Win-D
* [QTBUG-136192](https://bugreports.qt.io/browse/QTBUG-136192) qmlformat fails to write file
* [QTBUG-136552](https://bugreports.qt.io/browse/QTBUG-136552) QMLLS crashes
* [QTBUG-136672](https://bugreports.qt.io/browse/QTBUG-136672) QQuickComboBox::setModel() does an unguarded
qvariant_cast on the previous value
* [QTBUG-133858](https://bugreports.qt.io/browse/QTBUG-133858) tst_QQuickMenu::contextMenuKeyboard is flaky
* [QTBUG-136354](https://bugreports.qt.io/browse/QTBUG-136354) DragHandler doesn't account for scene changes when
calculating threshold
* [QTBUG-136933](https://bugreports.qt.io/browse/QTBUG-136933) Can't build QtQ4A examples from command line
* [QTBUG-134880](https://bugreports.qt.io/browse/QTBUG-134880) Disable edge-to-edge feature of Android 15 on
qtquickview examples
* [QTBUG-136581](https://bugreports.qt.io/browse/QTBUG-136581) [REG 6.5.3 -> 6.8.3] ListModel set() on existing index
fails if setting data retrieved from C++ QVariantMap containing a
QVariantList role
* [QTBUG-135286](https://bugreports.qt.io/browse/QTBUG-135286) Qml Property Cache heap-use-after-free
* [QTBUG-96580](https://bugreports.qt.io/browse/QTBUG-96580) Missing documentation for QSGRenderNode::RenderState
* [QTBUG-136947](https://bugreports.qt.io/browse/QTBUG-136947) EventModel::repopulate() missing endResetModel() on
early return in eventcalendar example
* [QTBUG-137086](https://bugreports.qt.io/browse/QTBUG-137086) [Reg 6.2 -> 6.5] Crashing QML code
* [QTBUG-137072](https://bugreports.qt.io/browse/QTBUG-137072) [REG: 6.8 → 6.9] QMetaType::metaObject crashes the
program
* [QTBUG-136810](https://bugreports.qt.io/browse/QTBUG-136810) crash on qml cache checksum mismatch
* [QTBUG-136439](https://bugreports.qt.io/browse/QTBUG-136439) No more possible to use a Loader for QML hot/live
reloading since Qt 6.8.3
* [QTBUG-135158](https://bugreports.qt.io/browse/QTBUG-135158) Quick Popup window can no longer have negative x on
Wayland
* [QTBUG-133314](https://bugreports.qt.io/browse/QTBUG-133314) Artifacts in rounded rectangle corners with borders
using software backend
* [QTBUG-136738](https://bugreports.qt.io/browse/QTBUG-136738) [Software renderer] Rectangle with e.g. topLeftRadius
set corner drawn black
* [QTBUG-137110](https://bugreports.qt.io/browse/QTBUG-137110) [Reg 6.8 -> 6.9] qmllint: Assert in type propagator
* [QTBUG-133793](https://bugreports.qt.io/browse/QTBUG-133793) QT_QML_GENERATE_QMLLS_INI doesn't update file if build
directory changes
* [QTBUG-132644](https://bugreports.qt.io/browse/QTBUG-132644) Cannot receive mouse move events when modal dialog is
open
* [QTBUG-134545](https://bugreports.qt.io/browse/QTBUG-134545) Mouse move and touch update events are not delivered
correctly when there are modal dialogs
* [QTBUG-137285](https://bugreports.qt.io/browse/QTBUG-137285) FAIL!  : tst_QQuickApplicationWindow::implicitFill()
Compared doubles are not the same (fuzzy compare)
* [QTBUG-136699](https://bugreports.qt.io/browse/QTBUG-136699) Unexpected removal of enabled binding when parent
enabled is toggled off
* [QTBUG-116675](https://bugreports.qt.io/browse/QTBUG-116675) QQuickWindow::grabWindow renders too small on macOS
retina
* [QTBUG-134099](https://bugreports.qt.io/browse/QTBUG-134099) [REG 6.7.3->6.8]Global position for QHoverEvent issued
from a QQuickItem inside a QQuickWidget is wrong.
* [QTBUG-134403](https://bugreports.qt.io/browse/QTBUG-134403) QtQuick Rectangle: Gradient not displayed when the color
property is set to transparent.
* [QTBUG-135795](https://bugreports.qt.io/browse/QTBUG-135795) QML Locale cannot be compiled in Direct Mode
* [QTBUG-134635](https://bugreports.qt.io/browse/QTBUG-134635) A floating-point precision error with the slider value.
* [QTBUG-136492](https://bugreports.qt.io/browse/QTBUG-136492) TreeView: Editable and non-editable items not working
correctly
* [QTBUG-137413](https://bugreports.qt.io/browse/QTBUG-137413) [REG 6.9.0 -> 6.9.1] qmlformat crashes on musl
* [QTBUG-132703](https://bugreports.qt.io/browse/QTBUG-132703) Unify spelling of Qt Qml modules
* [QTBUG-133924](https://bugreports.qt.io/browse/QTBUG-133924) IconLabel children are positioned under Icon & text
* [QTBUG-137035](https://bugreports.qt.io/browse/QTBUG-137035) qmllint gets stuck
* [QTBUG-137411](https://bugreports.qt.io/browse/QTBUG-137411) [REG 6.9.0 -> 6.9.1] Building for iOS failed:
qmlcachegen segmentation fault
* [QTBUG-137196](https://bugreports.qt.io/browse/QTBUG-137196) qmlcachegen crashes in QQmlJSScope::filePath
* [QTBUG-136998](https://bugreports.qt.io/browse/QTBUG-136998) qmllint crashes when checking  required properties
* [QTBUG-131886](https://bugreports.qt.io/browse/QTBUG-131886) Wrong delta threshold for MultiPointTouchArea using
scale
* [QTBUG-135255](https://bugreports.qt.io/browse/QTBUG-135255) The type compiler incorrectly gives a warning about
insufficient annotation for enum types.
* [QTBUG-112355](https://bugreports.qt.io/browse/QTBUG-112355) ShaderEffectSource with recursive shader causes magenta
texture on Apple Silicon
* [QTBUG-137561](https://bugreports.qt.io/browse/QTBUG-137561) FAIL!  : tst_QQuickColorDialogImpl::defaults() Received
a warning that resulted in a failure
* [QTBUG-130683](https://bugreports.qt.io/browse/QTBUG-130683) QtQuick.Controls: Native Tooltip size on macOS
* [QTBUG-132512](https://bugreports.qt.io/browse/QTBUG-132512) QtQuickView does not listen to Qt.quit() signal
* [QTBUG-135295](https://bugreports.qt.io/browse/QTBUG-135295) [Reg 5.15 -> 6.8] Binding crashes when combined with
StackView and Loader
* [QTBUG-94147](https://bugreports.qt.io/browse/QTBUG-94147) QSGGeometryNode docs snippet shows Qt 6 incompatible code
* [QTBUG-137705](https://bugreports.qt.io/browse/QTBUG-137705) qmlls: lazy QmlFile in DOM loads with incorrect import
path
* [QTBUG-137416](https://bugreports.qt.io/browse/QTBUG-137416) FAIL!  : tst_QQuickFileDialogImpl::defaults() Compared
values are not the same
* [QTBUG-122738](https://bugreports.qt.io/browse/QTBUG-122738) QtQuick.Dialogs FileDialog bad color with macOS dark
theme
* [QTBUG-137469](https://bugreports.qt.io/browse/QTBUG-137469) "Cannot assign object to list property" error message
isn't descriptive enough
* [QTBUG-137115](https://bugreports.qt.io/browse/QTBUG-137115) [REG 6.5 → 6.8] Issue with inline components and setData
* [QTBUG-132607](https://bugreports.qt.io/browse/QTBUG-132607) Unexpected text's rectangle behavior in a row
* [QTBUG-137323](https://bugreports.qt.io/browse/QTBUG-137323) Flickable jump back when scrolling to the edge in KDE
* [QTBUG-136235](https://bugreports.qt.io/browse/QTBUG-136235) Qt 6.8.3 A signal 11 (SIGSEGV) crash observed while
running qtquickview_kotlin sample application (Android 11 / API 30 )
* [QTBUG-134600](https://bugreports.qt.io/browse/QTBUG-134600) FileDialog's currentFolder shows regression on Debian
* [QTBUG-81803](https://bugreports.qt.io/browse/QTBUG-81803) QML TextInput - Incorrect behavior when all text is
selected and ctrl+backspace is pressed
* [QTBUG-137877](https://bugreports.qt.io/browse/QTBUG-137877) PrototypeChainCycle confuses Qt Design Studio project
storage
* [QTBUG-137540](https://bugreports.qt.io/browse/QTBUG-137540) [Reg 6.5.0 -> 6.5.5] Compilation blog post example
doesn't work anymore
* [QTBUG-137328](https://bugreports.qt.io/browse/QTBUG-137328) [Reg 6.7 -> 6.9] QJSEngine: created JavaScript objects
does not have function hasOwnProperty
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
* [QTBUG-134208](https://bugreports.qt.io/browse/QTBUG-134208) Mnemonic annotation is passed to screen readers
* [QTBUG-137326](https://bugreports.qt.io/browse/QTBUG-137326) [Reg 5.15 -> 6.2] Crash in
QQmlAbstractBinding::removeFromObject()
* [QTBUG-137823](https://bugreports.qt.io/browse/QTBUG-137823) Tab order does not follow visual order
* [QTBUG-137005](https://bugreports.qt.io/browse/QTBUG-137005) Qt6::qmltestrunner target no longer available
* [QTBUG-106900](https://bugreports.qt.io/browse/QTBUG-106900) QML Color type docs missing first few words
* [QTBUG-118188](https://bugreports.qt.io/browse/QTBUG-118188) QML evaluates bindings after destruction, possibly
resulting in segmentation faults
* [QTBUG-49481](https://bugreports.qt.io/browse/QTBUG-49481) Documentation about 'Attached properties' is confused
* [QTBUG-136455](https://bugreports.qt.io/browse/QTBUG-136455) Doc: Some QML methods are missing their return value
types
* [QTBUG-134936](https://bugreports.qt.io/browse/QTBUG-134936) Improve imperative Menu API documentation
* [QTBUG-138216](https://bugreports.qt.io/browse/QTBUG-138216) Errors in English language QML TreeView documentation
* [QTBUG-94965](https://bugreports.qt.io/browse/QTBUG-94965) FontDialog documentation improvements
* [QTBUG-138174](https://bugreports.qt.io/browse/QTBUG-138174) Lightning Viewer: runtime warnings
* [QTBUG-133256](https://bugreports.qt.io/browse/QTBUG-133256) Crash on dynamically removing items from a custom
QtQuick.Controls.Container with transitions
* [QTBUG-46798](https://bugreports.qt.io/browse/QTBUG-46798) Destroying an item crashes ListView
* [QTBUG-72208](https://bugreports.qt.io/browse/QTBUG-72208) Qt.labs.calendar onClicked date is one day off.
* [QTBUG-138200](https://bugreports.qt.io/browse/QTBUG-138200) iOS Style: Wrong palette colors when switching color
scheme from application
* [QTBUG-122436](https://bugreports.qt.io/browse/QTBUG-122436) Android a11y: Changes to Accessible.ignored and
Item.visible are not propagated to the screen reader
* [QTBUG-136959](https://bugreports.qt.io/browse/QTBUG-136959) Read-only TextEdit overrides all Shortcuts when it has
activeFocus
* [QTBUG-138391](https://bugreports.qt.io/browse/QTBUG-138391) Deep-nested QML module containing *.mjs file can cause
ambiguous import
* [QTBUG-138357](https://bugreports.qt.io/browse/QTBUG-138357) Documentation for qt_add_qml_module misses information
about find_package
* [QTBUG-138242](https://bugreports.qt.io/browse/QTBUG-138242) Crash when GC is triggered during script exception
handling in StateChangeScript or ScriptAction
* [QTBUG-138349](https://bugreports.qt.io/browse/QTBUG-138349) QmlPreview does not start with import QtQuick.Controls +
Style=Basic
* [QTBUG-132518](https://bugreports.qt.io/browse/QTBUG-132518) building with cmake 3.31 gives ODR violation warnings on
webassembly
* [QTBUG-127133](https://bugreports.qt.io/browse/QTBUG-127133) Why do I get warning "Multiple C++ types called xxx
found! This violates the One Definition Rule"
* [QTBUG-134292](https://bugreports.qt.io/browse/QTBUG-134292) ODR warnings with static build
* [QTBUG-126193](https://bugreports.qt.io/browse/QTBUG-126193) Crash in XR when clicking on Slider in Android Style
* [QTBUG-138559](https://bugreports.qt.io/browse/QTBUG-138559) qt_add_qml_module: TARGET dependency causes build
failure
* [QTBUG-120706](https://bugreports.qt.io/browse/QTBUG-120706) ScrollView::effectiveScrollBarHeight and
ScrollView::effectiveScrollbarWidth need elaboration on what exactly
"effective" mean
* [QTBUG-136147](https://bugreports.qt.io/browse/QTBUG-136147) Qt Labs Platforms: Add alt texts
* [QTBUG-54605](https://bugreports.qt.io/browse/QTBUG-54605) SignalSpy's clear() function is incorrectly documented as
causing valid to become false
* [QTBUG-127955](https://bugreports.qt.io/browse/QTBUG-127955) Repeater without parent reports its count but does not
create delegates
* [QTBUG-77201](https://bugreports.qt.io/browse/QTBUG-77201) Documentation of QQuickItem::stackAfter/stackBefore is
wrong
* [QTBUG-138358](https://bugreports.qt.io/browse/QTBUG-138358) QSGDefaultRectangleNode always returns invalid color
* [QTBUG-136611](https://bugreports.qt.io/browse/QTBUG-136611) OpenGL: Layering breaks culling
* [QTBUG-138602](https://bugreports.qt.io/browse/QTBUG-138602) Reg[6.9->6.10]Application toolbar turns black
* [QTBUG-137860](https://bugreports.qt.io/browse/QTBUG-137860) [Windows][A11y] Text can not be selected by NVDA
* [QTBUG-133267](https://bugreports.qt.io/browse/QTBUG-133267) Curve renderer does not always show latest version of
path data
* [QTBUG-137029](https://bugreports.qt.io/browse/QTBUG-137029) Qmllint as process on Windows do not populate error
channel unless called in terminal.
* [QTBUG-136101](https://bugreports.qt.io/browse/QTBUG-136101) Minimal configuration compile with autotests
* [QTBUG-136755](https://bugreports.qt.io/browse/QTBUG-136755) QQuickWindow::grabWindow() results in a black background
color instead of being transparent with the Offscreen platform.
* [QTBUG-87708](https://bugreports.qt.io/browse/QTBUG-87708) [Reg 5.15.0 -> 5.15.1] header's width isn't resized to
window's width when Layout is used
* [QTBUG-136747](https://bugreports.qt.io/browse/QTBUG-136747) String 6.9.0 found in 6.9.2 sources
* [QTBUG-51285](https://bugreports.qt.io/browse/QTBUG-51285) Using nested QtQuick Layouts with spacing generates
binding loops
* [QTBUG-134800](https://bugreports.qt.io/browse/QTBUG-134800) Window.window cannot work as a target of Connections QML
in GridView/RowLayout
* [QTBUG-115140](https://bugreports.qt.io/browse/QTBUG-115140) qtdeclarative -unity-build-batch-size 100000 fails
* [QTBUG-127605](https://bugreports.qt.io/browse/QTBUG-127605) [QtQuick.Dialogs/Wayland] Native FileDialog does not
respect Qt.ApplicationModal flag
* [QTBUG-133586](https://bugreports.qt.io/browse/QTBUG-133586) F2 shortcut or Ctrl+Click in qml files sometimes leads
to build dir instead of source and sometimes does absolutly nothing
* [QTBUG-118610](https://bugreports.qt.io/browse/QTBUG-118610) ShaderEffectSource in recursive mode with multisampling
is broken
* [QTBUG-132268](https://bugreports.qt.io/browse/QTBUG-132268) SelectionRectangle is fiddly to get working by default
* [QTBUG-117526](https://bugreports.qt.io/browse/QTBUG-117526) QQuickStylePrivate::fallbackStyle has the wrong value
when using run-time style selection and the fallback style is imported
via the style's qmldir
* [QTBUG-136709](https://bugreports.qt.io/browse/QTBUG-136709) Style import triggers style change
* [QTBUG-137900](https://bugreports.qt.io/browse/QTBUG-137900) QML sslConfiguration has sslOptions propery out of sync
* [QTBUG-109279](https://bugreports.qt.io/browse/QTBUG-109279) JS array vs QVariantList mixup
* [QTBUG-137554](https://bugreports.qt.io/browse/QTBUG-137554) qml: list qml --> c++ editing crashes/has no effect
* [QTBUG-137116](https://bugreports.qt.io/browse/QTBUG-137116) Incorrect Semantic Highlighting for QML Property Chains
* [QTBUG-133315](https://bugreports.qt.io/browse/QTBUG-133315) qmlformat can still insert extra spaces in user code
* [QTBUG-123386](https://bugreports.qt.io/browse/QTBUG-123386) QmlFormat. Incorrect handling of some comments
* [QTBUG-138104](https://bugreports.qt.io/browse/QTBUG-138104) tst_qtquickview_signallistener crashes on Android
* [QTBUG-138565](https://bugreports.qt.io/browse/QTBUG-138565) "Cannot generate qmltypes file" when trying to run in-
app purchase demo app on Android
* [QTBUG-132108](https://bugreports.qt.io/browse/QTBUG-132108) addApplicationFontFromData behaves abnormally after
removeAllApplicationFonts.
* [QTBUG-138155](https://bugreports.qt.io/browse/QTBUG-138155) qt_generate_deploy_qml_app_script: Error for space in
output name

### qtactiveqt
* [QTBUG-134098](https://bugreports.qt.io/browse/QTBUG-134098) dumpcpp puts native Qt types inside a custom namespace
* [QTBUG-136512](https://bugreports.qt.io/browse/QTBUG-136512) [Reg 6.8.3 -> 6.9.0] dumpcpp's output is uncompilable
due to missing namespaces
* [QTBUG-137347](https://bugreports.qt.io/browse/QTBUG-137347) dumpcpp skips namespace and creates syntaxes errors

### qtmultimedia
* [QTBUG-134196](https://bugreports.qt.io/browse/QTBUG-134196) R16 video texture formats don't have a working fallback
for GLES 2.0
* [QTBUG-132458](https://bugreports.qt.io/browse/QTBUG-132458) [static linking] undefined symbols for ffmpeg plugin
* [QTBUG-136680](https://bugreports.qt.io/browse/QTBUG-136680) qt_add_ios_ffmpeg_libraries() not working with 6.9
* [QTBUG-137070](https://bugreports.qt.io/browse/QTBUG-137070) [REG 6.9.1 prev snapshot->6.9.1] Multimedia examples not
compiling, Wasm
* [QTBUG-136052](https://bugreports.qt.io/browse/QTBUG-136052) VideoOutput crash with opacity animation
* [QTBUG-136920](https://bugreports.qt.io/browse/QTBUG-136920) Access violation on QWindowsFormatInfo construction
* [QTBUG-102716](https://bugreports.qt.io/browse/QTBUG-102716) [Windows] Access violation in QWindowsFormatInfo
* [QTBUG-136227](https://bugreports.qt.io/browse/QTBUG-136227) Crash in camera rundown
* [QTBUG-137150](https://bugreports.qt.io/browse/QTBUG-137150) Assertion hit when unplugging microphone device while
recording
* [QTBUG-137308](https://bugreports.qt.io/browse/QTBUG-137308) [Reg B2Qt 6.7.3 -> 6.8.3] glupload not supported in
GStreamer pipeline
* [QTBUG-137360](https://bugreports.qt.io/browse/QTBUG-137360) Qt multimedia compilation error windows 32 bit
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
* [QTBUG-98145](https://bugreports.qt.io/browse/QTBUG-98145) Android: Avoid empty file format on the AudioRecorder app
* [QTBUG-138059](https://bugreports.qt.io/browse/QTBUG-138059) [REG 6.9.0-6.9.1] [windows] Strange Qt warning on
QAudioSource::start() when non-default sample rate is used
* [QTBUG-104515](https://bugreports.qt.io/browse/QTBUG-104515) Documentation for QML's CaptureSession lacks
camera.start() entry
* [QTBUG-130636](https://bugreports.qt.io/browse/QTBUG-130636) FFmpeg: QCamera::FlashOn is unreliable
* [QTBUG-123073](https://bugreports.qt.io/browse/QTBUG-123073) [macOS] QMediaRecorder failed to record an audio after
reconnecting AirPods
* [QTBUG-136632](https://bugreports.qt.io/browse/QTBUG-136632) There is no sound when playing videos (REGRESSION)
* [QTBUG-135281](https://bugreports.qt.io/browse/QTBUG-135281) Qml Camera not work on webassembly
* [QTBUG-
133652](https://bugreports.qt.io/browse/QTBUG-133652) tst_QMediaPlayerBackend::play_playbackLastsForTheExpectedTime is
flaky on Linux
* [QTBUG-136124](https://bugreports.qt.io/browse/QTBUG-136124) tst_qwindowcapturebackend: flaky deadlocks on
opensuse-15.6
* [QTBUG-135614](https://bugreports.qt.io/browse/QTBUG-135614) recorder_encodesFrames_toValidMediaFile_whenWindowResizes
fails on opensuse/asan
* [QTBUG-129713](https://bugreports.qt.io/browse/QTBUG-129713) Test times out: tst_QMediaFrameInputsBackend::mediaRecor
derWritesVideo_whenInputFrameGrowsOverTime
* [QTBUG-127733](https://bugreports.qt.io/browse/QTBUG-127733) tst_QAudioSink::pullResumeFromUnderrun() failed on
Ubuntu 24.04 offscreen and X11
* [QTBUG-117099](https://bugreports.qt.io/browse/QTBUG-117099) Video jerks when playing (Windows backend)
* [QTBUG-133914](https://bugreports.qt.io/browse/QTBUG-133914) FFmpeg plugin tests may fail to build on Linux and
Android
* [QTBUG-138000](https://bugreports.qt.io/browse/QTBUG-138000) tst_QAudioSource::pull fails on ubuntu-22.04-x11-tests
* [QTBUG-137984](https://bugreports.qt.io/browse/QTBUG-137984) Unable to compile QtMultimedia Debug under PiOS

### qttools
* [QTBUG-136436](https://bugreports.qt.io/browse/QTBUG-136436) qdoc doesn't warn about missing alt text for
\inlineimage
* [QTBUG-136532](https://bugreports.qt.io/browse/QTBUG-136532) QRegularExpression::matchView is not indexed by Qt
Assistant
* [QTBUG-54203](https://bugreports.qt.io/browse/QTBUG-54203) Linguist hardcoded background colors when working with >1
language
* [QTBUG-136578](https://bugreports.qt.io/browse/QTBUG-136578) Linguist is unusable in dark mode
* [QTBUG-136736](https://bugreports.qt.io/browse/QTBUG-136736) [REG: 6.5->6.8] ios: Fails if main app target is in a
subdirectory
* [QTBUG-103470](https://bugreports.qt.io/browse/QTBUG-103470) [iOS] CMake translation handling fails
* [QTBUG-117406](https://bugreports.qt.io/browse/QTBUG-117406) [REG 6.6.0beta4->6.7.0] linguist/i18n and qml/qml-i18n
not compiling on iOS
* [QTBUG-136805](https://bugreports.qt.io/browse/QTBUG-136805) Fix typo in the \modulestate description
* [QTBUG-136768](https://bugreports.qt.io/browse/QTBUG-136768) Mis-detection of namespaces
* [QTBUG-96693](https://bugreports.qt.io/browse/QTBUG-96693) QUiLoader resolves  wrong buddy when UI is loaded twice
* [QTBUG-138072](https://bugreports.qt.io/browse/QTBUG-138072) Remove traces of <type> argument to \page command from
documentation
* [QTBUG-136158](https://bugreports.qt.io/browse/QTBUG-136158) Qt UI Tools: Add alt texts
* [QTBUG-138870](https://bugreports.qt.io/browse/QTBUG-138870) QDoc fails to parse templated using statement with
default value for a template arg
* [QTBUG-136963](https://bugreports.qt.io/browse/QTBUG-136963) qdoc/qmlmarkupvisitor.h:78:16: error:
‘QQmlJS::AST::Expression’ has not been declared
* [QTBUG-136483](https://bugreports.qt.io/browse/QTBUG-136483) qdoc non-deterministic .index output
* [QTBUG-137569](https://bugreports.qt.io/browse/QTBUG-137569) make qttools configure more user friendly on windows

### qtdoc
* [QTBUG-136482](https://bugreports.qt.io/browse/QTBUG-136482) REG [6.9.0->6.9.1] demos/hangman not compiling on
Android
* [QTBUG-135840](https://bugreports.qt.io/browse/QTBUG-135840) the doc only contains qmake but not cmake
* [QTBUG-135801](https://bugreports.qt.io/browse/QTBUG-135801) windeployqt: Help output listed for an old version
* [QTBUG-136974](https://bugreports.qt.io/browse/QTBUG-136974) Qt Licensing page does not list Qt Graphs under GPL
licensed modules
* [QTBUG-132833](https://bugreports.qt.io/browse/QTBUG-132833) QT_QPA_EGLFS_ROTATION rotates mouse events but not touch
events
* [QTBUG-133792](https://bugreports.qt.io/browse/QTBUG-133792) Compiling demos/maroon and demos/hangman on
Windows/MacOS fails
* [QTBUG-133462](https://bugreports.qt.io/browse/QTBUG-133462) QNAM cannot get response from Qt HTTP Server due to WASM
app not being allowed to perform Cross-Origin Resource Sharing
* [QTTA-401](https://bugreports.qt.io/browse/QTTA-401) Qt Jenny Demo: Gradle is not called during CMake configure
to generate code
* [QTBUG-138105](https://bugreports.qt.io/browse/QTBUG-138105) [Reg 6.5.9 -> 6.8.3] Alarms demo: TumberDelegate can no
longer read properties
* [QTBUG-138169](https://bugreports.qt.io/browse/QTBUG-138169) Document Viewer: Runtime warnings
* [QTBUG-95325](https://bugreports.qt.io/browse/QTBUG-95325) Removal of QTextStream::setCodec is not documented
* [QTBUG-118823](https://bugreports.qt.io/browse/QTBUG-118823) Debian repository setup suggests putting a password to a
plain text file that is worldreadable
* [QTBUG-138587](https://bugreports.qt.io/browse/QTBUG-138587) Add information on how to subscribe to the mailing list
mentioned on "Security in Qt"
* [QTBUG-136794](https://bugreports.qt.io/browse/QTBUG-136794) QML debugging is excluded in some of the Android
examples and demos
* [QTBUG-136747](https://bugreports.qt.io/browse/QTBUG-136747) String 6.9.0 found in 6.9.2 sources
* [QTBUG-134903](https://bugreports.qt.io/browse/QTBUG-134903) Duplicate context menus when using custom context Menus
in text controls
* [QTBUG-138527](https://bugreports.qt.io/browse/QTBUG-138527) Replace direct links to https://doc.qt.io/qt-6/
* [QTBUG-138676](https://bugreports.qt.io/browse/QTBUG-138676) Coffee machine examples images not getting current
values fom slider

### qtlocation
* [QTBUG-138409](https://bugreports.qt.io/browse/QTBUG-138409) Incorrect qtlocation documentation
* [QTBUG-137557](https://bugreports.qt.io/browse/QTBUG-137557) QtLocation: Using GeocodeModel with OSM plugin in QML
causes app crash when canceling update

### qtpositioning
* [QTBUG-136157](https://bugreports.qt.io/browse/QTBUG-136157) Qt Positioning: Add alt texts
* [QTBUG-137764](https://bugreports.qt.io/browse/QTBUG-137764) QDoc uses incorrect image source
* [QTBUG-106049](https://bugreports.qt.io/browse/QTBUG-106049) Qt Android's QGeoCoordinate API returns altitude in
wrong reference frame

### qtconnectivity
* [QTBUG-136506](https://bugreports.qt.io/browse/QTBUG-136506) NFC target should be invalidated if Java function call
fails
* [QTBUG-136156](https://bugreports.qt.io/browse/QTBUG-136156) Qt Bluetooth: Add alt texts
* [QTBUG-136150](https://bugreports.qt.io/browse/QTBUG-136150) Qt NFC: Add alt texts
* [QTBUG-136692](https://bugreports.qt.io/browse/QTBUG-136692) BLE devices can't be discovered after initial connection
on iOS 18+

### qtwayland
* [QTBUG-137021](https://bugreports.qt.io/browse/QTBUG-137021) make QWindow::requestActivate() working in auto tests on
Wayland
* [QTBUG-137333](https://bugreports.qt.io/browse/QTBUG-137333) Wayland Compositor + static build + LTO = crash
* [QTBUG-133866](https://bugreports.qt.io/browse/QTBUG-133866) Using qt-shell, if item in dialog is selected with
mouse, no further focus navigation via keyboard possible
* [QTBUG-137814](https://bugreports.qt.io/browse/QTBUG-137814) Build broken with -no-feature-sharedmemory
* [QTBUG-135341](https://bugreports.qt.io/browse/QTBUG-135341) text input v3: input method window is misplaced after
closing a popup
* [QTBUG-135921](https://bugreports.qt.io/browse/QTBUG-135921) text-input-v3 skips advertising capabilities
* [QTBUG-131983](https://bugreports.qt.io/browse/QTBUG-131983) text input v3: first character after refocus doesn't go
through the input method
* [QTBUG-137727](https://bugreports.qt.io/browse/QTBUG-137727) Crash in zwp_text_input_v3_set_surrounding_text when
selecting large text
* [QTBUG-137702](https://bugreports.qt.io/browse/QTBUG-137702) [REG Qt 6.9.0 -> 6.9.1] Crash when completing code
* [QTBUG-134234](https://bugreports.qt.io/browse/QTBUG-134234) rare crashes in QWaylandShmBackingStore::flush

### qt3d
* [QTBUG-135394](https://bugreports.qt.io/browse/QTBUG-135394) MouseHandler may crash if it is destroyed while mouse is
being moved

### qtserialbus
* [QTBUG-107140](https://bugreports.qt.io/browse/QTBUG-107140) Typo in the document?

### qtserialport
* [QTBUG-136154](https://bugreports.qt.io/browse/QTBUG-136154) Qt Serial Port: Add alt texts
* [QTBUG-133489](https://bugreports.qt.io/browse/QTBUG-133489) ResourceError does not fire on unplug for QtSerialPort
6.8.2

### qtwebsockets
* [QTBUG-136216](https://bugreports.qt.io/browse/QTBUG-136216) QWebSocket "Invalid UTF-8 Code Encountered" Error in Qt6
* [QTBUG-136153](https://bugreports.qt.io/browse/QTBUG-136153) Qt WebSockets: Add alt texts
* [QTBUG-81084](https://bugreports.qt.io/browse/QTBUG-81084) Websocket client creates TCP RST instead proper shutdown
on close()

### qtwebengine
* [QTBUG-134481](https://bugreports.qt.io/browse/QTBUG-134481) qwebengine_convert_dict Cannot encode command 'TRY ...'
to utf8.
* [QTBUG-136481](https://bugreports.qt.io/browse/QTBUG-136481) QtWebEngine crashes when screen is removed
* [QTBUG-136637](https://bugreports.qt.io/browse/QTBUG-136637) Missing libxml2.so.2 with libxml2 2.14
* [QTBUG-133593](https://bugreports.qt.io/browse/QTBUG-133593) Qt Webengine debug symbols (dSYM) have incorrect install
location on macOS
* [QTBUG-136257](https://bugreports.qt.io/browse/QTBUG-136257) QtWebEngine based browser shows nothing with panthor
driver
* [QTBUG-131897](https://bugreports.qt.io/browse/QTBUG-131897) pdf viewer is not working on nano browser and simple
browser sample apps
* [QTBUG-135974](https://bugreports.qt.io/browse/QTBUG-135974) adding module pdfwidgets leads to a warning
* [QTBUG-136622](https://bugreports.qt.io/browse/QTBUG-136622) Accessiblity:voice over can't read table content
* [QTBUG-134055](https://bugreports.qt.io/browse/QTBUG-134055) Make Qt WebEngine expose accessibility content properly
* [QTBUG-133608](https://bugreports.qt.io/browse/QTBUG-133608) Missing documentation on how to install Qt WebEngine
* [QTBUG-137447](https://bugreports.qt.io/browse/QTBUG-137447) FAIL!  : tst_UIDelegates::javaScriptDialog(AlertDialog)
'(static_cast<QGuiApplication
*>(QCoreApplication::instance()))->focusObject()' returned FALSE.
* [QTBUG-111907](https://bugreports.qt.io/browse/QTBUG-111907) Crash when touching text field inside WebEngineView
* [QTBUG-136231](https://bugreports.qt.io/browse/QTBUG-136231) Min c++ version required for QtWebengine
* [QTBUG-138009](https://bugreports.qt.io/browse/QTBUG-138009) Correct suggestions for building Qt WebEngine
* [QTBUG-138159](https://bugreports.qt.io/browse/QTBUG-138159) Build error:
QtWebEngineCore/private/qtwebenginecoreglobal_p.h: No such file or
directory
* [QTBUG-135786](https://bugreports.qt.io/browse/QTBUG-135786) WebEngine in 6.9.0 with an AMD GPU and on both
Wayland/X11 renders gltiches instead of text
* [QTBUG-134746](https://bugreports.qt.io/browse/QTBUG-134746) [REG 6.8.2 → 6.9] simplebrowser example crashes during
startup on Windows
* [QTBUG-133086](https://bugreports.qt.io/browse/QTBUG-133086) Doc: Improve Networking and WebEngine security topics
* [QTBUG-129970](https://bugreports.qt.io/browse/QTBUG-129970) WebEngine Windows ARM support

### qtcharts
* [QTBUG-135691](https://bugreports.qt.io/browse/QTBUG-135691) Wasm build fails when linking both QtCharts and QtGraphs
* [QTBUG-136770](https://bugreports.qt.io/browse/QTBUG-136770) QLineSeries.clear() does not remove all lines from the
plot in that series
* [QTBUG-135240](https://bugreports.qt.io/browse/QTBUG-135240) Animation effects in ChartView makes PieSlice lose its
alpha channel
* [QTBUG-132790](https://bugreports.qt.io/browse/QTBUG-132790) Unexpected behaviour of QScatterSeries for
selectedPoints, replace and deselectAllPoints
* [QTBUG-132357](https://bugreports.qt.io/browse/QTBUG-132357) setSelectedColor doesn't work on barsets added to
QBarSeries with insert method

### qtvirtualkeyboard
* [QTBUG-133400](https://bugreports.qt.io/browse/QTBUG-133400) Mouse/Touch hover propagates to item under VKB
* [QTBUG-137250](https://bugreports.qt.io/browse/QTBUG-137250) REG->6.9.0: VirtualKeyboard not working (Linux)
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
* [QTBUG-128818](https://bugreports.qt.io/browse/QTBUG-128818) QTextToSpeech with flite crashes saying ©
* [QTBUG-137735](https://bugreports.qt.io/browse/QTBUG-137735) Failing tests on tqtc/lts-6.8: tst_QTextToSpeech
* [QTBUG-138064](https://bugreports.qt.io/browse/QTBUG-138064) [flite] tst_QTextToSpeech fails on ubuntu/arm
* [QTBUG-137855](https://bugreports.qt.io/browse/QTBUG-137855) QTextToSpeech: flite - sayingWord signals emitted
delayed
* [QTBUG-137947](https://bugreports.qt.io/browse/QTBUG-137947) [flite] QTextToSpeech::pause(BoundaryHint::Word) not
implemented
* [QTBUG-138010](https://bugreports.qt.io/browse/QTBUG-138010) layout / palette glitches with quickspeech example

### qtremoteobjects
* [QTBUG-131016](https://bugreports.qt.io/browse/QTBUG-131016) Unexpected warning generated by repc
* [QTBUG-130972](https://bugreports.qt.io/browse/QTBUG-130972) repc is not deterministic

### qtquicktimeline
* [QTBUG-136144](https://bugreports.qt.io/browse/QTBUG-136144) Qt Quick Timeline: Add alt texts

### qtquick3d
* [QTBUG-136754](https://bugreports.qt.io/browse/QTBUG-136754) startTime doesn't work without affectors
* [QTBUG-137182](https://bugreports.qt.io/browse/QTBUG-137182) Wrong shading rendered for 3D models imported by
RuntimeLoader
* [QTBUG-136334](https://bugreports.qt.io/browse/QTBUG-136334) The documentation of qt6_add_lightprobe_images is
missing
* [QTBUG-138591](https://bugreports.qt.io/browse/QTBUG-138591) Broken font-weight tag
* [QTBUG-96159](https://bugreports.qt.io/browse/QTBUG-96159) Qt5.git integration fails in '6.2':  The "moc" executable
"/Users/qt/work/qt/qt5/qtbase/libexec/moc" does not exist

### qt5compat
* [QTBUG-71541](https://bugreports.qt.io/browse/QTBUG-71541) ColorOverlay documentation refers to wrong color format
* [QTBUG-136146](https://bugreports.qt.io/browse/QTBUG-136146) Qt 5 Core Compatibility: Add alt texts

### qtmqtt
* [QTBUG-135653](https://bugreports.qt.io/browse/QTBUG-135653) MessageReceived not fired when subscribing again to just
unsubscribed topic

### qtopcua
* [QTBUG-134674](https://bugreports.qt.io/browse/QTBUG-134674) opcua/waterpump/simulationserver example does not build
with Boot to Qt
* [QTBUG-109096](https://bugreports.qt.io/browse/QTBUG-109096) Installed version of OPC UA example cannot compile
because it relies on the presence of Qt source code
* [QTBUG-136141](https://bugreports.qt.io/browse/QTBUG-136141) Header files not listed in Qt OPC UA example
documentation
* [QTBUG-135674](https://bugreports.qt.io/browse/QTBUG-135674) SimpleAttributeOperand for condtionId generated with
BrowsePath of arraySize -1
* [QTBUG-135130](https://bugreports.qt.io/browse/QTBUG-135130) [qtopcua] Cannot build manual tests
* [QTBUG-137701](https://bugreports.qt.io/browse/QTBUG-137701) Connecting to unsecured endpoint results in
ClientError::UnknownError
* [QTBUG-138754](https://bugreports.qt.io/browse/QTBUG-138754) Build fails with Qt OPC UA when OpenSSL 1.1 is supported

### qthttpserver
* [QTBUG-137849](https://bugreports.qt.io/browse/QTBUG-137849) FAIL!  : tst_QHttpServerMultithreaded::initTestCase()
'localserver->listen(local)' returned FALSE. (Local server listen
failed)
* [QTBUG-136155](https://bugreports.qt.io/browse/QTBUG-136155) Qt HTTP Server: Add alt texts
* [QTBUG-137330](https://bugreports.qt.io/browse/QTBUG-137330) QtHttpServer: Writing from Sequential QIODevices to
HTTP(S)/1.1 Hangs the Client
* [QTBUG-138611](https://bugreports.qt.io/browse/QTBUG-138611) QtHttpServer has out of order writes because it starts
handling the next HTTP/1 request before it's done writing from QIODevice

### qtgrpc
* [QTBUG-137313](https://bugreports.qt.io/browse/QTBUG-137313) Build fails if using QML and GENERATE_PACKAGE_SUBFOLDERS
in qt_add_grpc
* [QTBUG-130113](https://bugreports.qt.io/browse/QTBUG-130113) build time paths used in
Qt6ProtobufWellKnownTypesTargets.cmake
* [QTBUG-138180](https://bugreports.qt.io/browse/QTBUG-138180) Qt GRPC: Weird duplications in documentation tree
* [QTBUG-138494](https://bugreports.qt.io/browse/QTBUG-138494) GRPC, QHttp2Channel: Implement metadata handling
according to protocol
* [QTBUG-129160](https://bugreports.qt.io/browse/QTBUG-129160) QtGrpc: improve lifetime-management of Http2Handler

### qtgraphs
* [QTBUG-136654](https://bugreports.qt.io/browse/QTBUG-136654) Building qtgraphs on mac fails with due to -Wcast-
function-type-mismatch
* [QTBUG-135384](https://bugreports.qt.io/browse/QTBUG-135384) Printing the 3D graph causes the Graph Printing example
to crash
* [QTBUG-135386](https://bugreports.qt.io/browse/QTBUG-135386) [Boot2Qt] Cannot save 3D graph to PDF
* [QTBUG-134592](https://bugreports.qt.io/browse/QTBUG-134592) Dragging points in 2D spline graphs is not working
* [QTBUG-136950](https://bugreports.qt.io/browse/QTBUG-136950) tst_qmlbarscatter trying to use non-existent property
* [QTBUG-138257](https://bugreports.qt.io/browse/QTBUG-138257) Code snippet for PieModelMapper uses undefined
properties
* [QTBUG-137718](https://bugreports.qt.io/browse/QTBUG-137718) XYSeries: opacity property has no effect
* [QTBUG-133759](https://bugreports.qt.io/browse/QTBUG-133759) the Custom3DItem position is not correct when setting
"axisZ.reversed: true" in QtGraphs
* [QTBUG-138470](https://bugreports.qt.io/browse/QTBUG-138470) SurfaceGallery does not start properly
* [QTBUG-136174](https://bugreports.qt.io/browse/QTBUG-136174) 3D bars graph endless sync loop
* [QTBUG-138492](https://bugreports.qt.io/browse/QTBUG-138492) qdoc: Snippet indentation issues
* [QTBUG-138462](https://bugreports.qt.io/browse/QTBUG-138462) QtGraphs pollutes the global namespace
* [QTBUG-135691](https://bugreports.qt.io/browse/QTBUG-135691) Wasm build fails when linking both QtCharts and QtGraphs
* [QTBUG-138456](https://bugreports.qt.io/browse/QTBUG-138456) Documentation contains references to "QGraphsView" which
is a private class

### qtapplicationmanager (Commercial only)
* [QTBUG-137056](https://bugreports.qt.io/browse/QTBUG-137056) Qt Application Manager - WindowObject Resizing Issue (Qt
6.8.3+)
* [QTBUG-137008](https://bugreports.qt.io/browse/QTBUG-137008) FAILED: tests/data/packages C:/Users/qt/work/qt/qtapplic
ationmanager_standalone_tests/tests/data/packages
* [QTBUG-136961](https://bugreports.qt.io/browse/QTBUG-136961) qtapplicationmanager: bubblewrap-example may need
bubblewarp
* [QTBUG-99702](https://bugreports.qt.io/browse/QTBUG-99702) Qt module -tools package has both compile time and
runtime tools

### qmlcompilerplus (Commercial only)
* [QTBUG-135795](https://bugreports.qt.io/browse/QTBUG-135795) QML
  Locale cannot be compiled in Direct Mode

Known Issues
------------
* Check that your system meets Qt's requirements:
  https://doc.qt.io/qt-6.9/supported-platforms.html
* RTA reported issues from Qt 6.9
  https://qt-project.atlassian.net/issues/?filter=10496
* See Qt 6.9 known issues from:
  https://wiki.qt.io/Qt_6.9_Known_Issues
* Qt 6.9.2 Open issues in Jira:
  https://qt-project.atlassian.net/issues/?filter=10627

Credits for the  release goes to:
---------------------------------

Eirik Aavitsland
Laszlo Agocs
Konsta Alajärvi
Anu Aliyas
Even Oscar Andersen
Soheil Armin
Albert Astals Cid
Xavier BESSON
Mate Barany
Vladimir Belyavsky
Nicholas Bennett
Kizito Birabwa
Tim Blechmann
Maximilian Blochberger
Eskil Abrahamsen Blomfeldt
David Boddie
Joerg Bornemann
Assam Boudjelthia
Aurélien Brooke
Kai Uwe Broulik
Michael Brüning
Alex Bu
Oswald Buddenhagen
Olivier De Cannière
Alexei Cazacov
Kaloyan Chehlarski
Wang Chuan
Alexandru Croitor
Mitch Curtis
Thibaut Cuvelier
Giuseppe D'Angelo
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
Tobias Fella
Samuel Gaist
Zoltan Gera
Robert Griebl
Mikko Gronoff
Richard Moe Gustavsen
Mikko Hallamaa
Inkamari Harjula
Andre Hartmann
Elias Hautala
Jani Heikkinen
Tero Heikkinen
Moss Heim
Ulf Hermann
Øystein Heskestad
Volker Hilsheimer
Dominik Holland
Benedikte Holm
Samuli Hölttä
Thorbjørn Martsum / Mjølner Informatics
Masoud Jami
Morteza Jamshidi
Allan Sandfeld Jensen
Jonas Karlsson
Igor Khanin
Ahmed El Khazari
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
Volker Krause
Mike Krus
Santhosh Kumar
Kai Köhne
Cristian Le
Inho Lee
Frédéric Lefebvre
Wladimir Leuschner
Pawel Lopko
Robert Löhning
Thiago Macieira
Thorbjørn Lund Martsum
Leena Miettinen
Jan Moeller
Safiyyah Moosa
Sheree Morphett
Bartlomiej Moskal
Marc Mutz
Antti Määttä
Martin Negyokru
Andy Nichols
Mårten Nordheim
Daniel Nylander
Dennis Oberst
Matti Paaso
Jerome Pasion
Miika Pernu
Samuli Piippo
Karim Pinter
Lauri Pohjanheimo
Joni Poikelin
Jacek Poplawski
Rami Potinkara
Lorn Potter
Sakaria Pouke
Dheerendra Purohit
Liang Qi
Florian RICHER
Matthias Rauter
David Redondo
Arno Rehn
Topi Reinio
David Rosca
Shawn Rutledge
Otto Ryynänen
Toni Saario
Ahmad Samir
Lars Schmertmann
Carl Schwan
Michal Seben
SanthoshKumar Selvaraj
Luca Di Sera
Sami Shalayel
Raman Shamotsin
Tian Shilin
Nils Petter Skålerud
Nils Peter Skålerud
Ivan Solovev
Axel Spoerl
Magdalena Stojek
Christian Strømme
Tarja Sundqvist
Lars Sutterud
Sadegh Taghavi
Nodir Temirkhodjaev
Aleksandr Timofeev
Jens Trillmann
Paul Olav Tvete
Esa Törmänen
Sami Varanka
Peter Varga
Doris Verria
Tor Arne Vestbø
Petri Virkkunen
Ville Voutilainen
Juha Vuolle
Olli Vuolteenaho
Jaishree Vyas
Jannis Völker
Michael Weghorn
Bernd Weimer
Edward Welbourne
Paul Wicking
Piotr Wiercinski
Oliver Wolff
Semih Yavuz
Vlad Zahorodnii
Oleksii Zbykovskyi
Nic Zonta
