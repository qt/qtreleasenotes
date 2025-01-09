Release note  
============  
Qt 6.5.4 release is a patch release made on the top of Qt 6.5.3.  
As a patch release, Qt 6.5.4 does not add any new functionality but provides  
bug fixes and other improvements and maintains both forward and backward  
compatibility (source and binary) with Qt 6.5.3.  

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
  
* CVE-2023-51714 in qtbase  
  
* CVE-2023-45872 in qtsvg  

### qtbase
* 5121ffc21bb Fix crash when reading corrupt font data
Fixed a possible crash that could happen when loading corrupted font
data.

* de59f732fc2 QMessageBox::about / aboutQt - use native modal dialog on
iOS
QMessageBox::about(Qt) now shows native, modal dialog.

* def88ec7fa3 SQLite: Update SQLite to v3.43.1
Updated SQLite to v3.43.1

* 3974778dc9b [docs] Fix \since for qHash(qfloat16)
Delete the old entry for qHash(qfloat16), keep the one from this
commit.

* 601a1d5486d QDockWidget: ignore close event if DockWidgetClosable is
not set
A floating dockwidget that doesn't have the DockWidgetClosable feature
flag set can no longer be closed by a call to QWidget::close or a
corresponding keyboard shortcut (such as Alt+F4).

* fac706849a0 Fix renamed and duplicated namespaces in QXmlStreamWriter
Fix renamed and duplicated namespaces in QXmlStreamWriter.

* 93c6c8b397b Un-deprecate qSwap()
Un-deprecated qSwap().

* 88d62ca1acd Use the actual target name as base name for android
deployment settings
The target name is used as a base name of android deployment settings,
but not the OUTPUT_NAME property.

* 1b2a4383225 Remove framework-related functionality from syncqt
'-framework' and '-frameworkIncludeDir' arguments were removed. The
related logic is moved to cmake scripts.

* 2ec31b5fb17 SQLite: Update SQLite to v3.43.2
Updated SQLite to v3.43.2

* b548c93c24c Update bundled libjpeg-turbo to version 3.0.1
libjpeg-turbo was updated to version 3.0.1

* 1989e419a3b Android: use all nameFilters at once for native file
dialog
use all nameFilters at once since Android file picker can't change
nameFilters after being opened.

* 9433dff701d SQLite: Update SQLite to v3.44.0
Updated SQLite to v3.44.0

* 3bd6e16978f Cocoa MessageBox: don't use native message box if detailed
text is set
On Apple platforms, the native message box is no longer used when
detailed text is set.

* 2a243d790aa configure: Make sure the configure script exits with
cmake's exit code
The configure script on UNIX systems will now exit with the same exit
code that the underlying cmake process exited with.

* dbd2d1a31fb SQLite: Update SQLite to v3.44.1
Updated SQLite to v3.44.1

* 131a868e467 OpenSSL: remove support for 1.1
Support for OpenSSL 1.1 has been dropped. Qt now only supports OpenSSL
3.

* 02225eabead SQLite: Update SQLite to v3.44.2
Updated SQLite to v3.44.2

### qtsvg
* 7a3abdc1 Fix crash when reading text with line breaks
Fixed a regression where the application would crash on certain SVG
files.

### qtdeclarative
* 274e81dd0e Fix translucent NativeRendering text on transparent window
Fixed an issue where NativeRendering text with a translucent color
combined with a transparent window would cause unexpected translucency
effects on opaque parts of the scene.

* a1d35bd531 Fix missing paragraph containing object replacement char
Fixed an issue where a paragraph containing the Object Replacement
Character (U+FFFC) would be invisible.

* 90ccadc890 Disable TapHandler.longPressed signal if longPressThreshold
== 0
TapHandler.longPressThreshold can now be set to 0 to disable its press-
and-hold feature, and can be reset to undefined to restore the platform
default.

### qt3d
* 4eb0953ad Fix Race Condition in NodePostConstructorInit::processNodes
Fix Race Condition in NodePostConstructorInit::processNodes

### qtimageformats
* 135ee22 Update bundled libwebp to version 1.3.2
Update bundled libwebp to version 1.3.2

* 6164a03 Update bundled libtiff to version 4.6.0
Bundled libtiff was updated to version 4.6.0

### qtwebengine
* 30c141c64 Fix corrupted load/fetch state on start up in case of
NoCache
Switching profile to NoCache do not longer implicitly removes cache
from old data store.

### qt5compat
* 2b6f873 SAX: Remove unused QtXml/qtxmlglobal.h header inclusion
The QtCore5Compat/qxml.h header no longer includes QtXml/qtxmlglobal.h.


Fixes
-----

### qtbase
* [QTBUG-116773](https://bugreports.qt.io/browse/QTBUG-116773) Adding
"Fuzzed" .otf font files causes access violation exception
* [QTBUG-116920](https://bugreports.qt.io/browse/QTBUG-116920) FAIL!  :
tst_QGeoAreaMonitorSource::tst_monitor() 'obj != nullptr' returned
FALSE.
* [PYSIDE-2460](https://bugreports.qt.io/browse/PYSIDE-2460)
QOpenGLContext is not valid when aboutToBeDestroyed is run
* [QTBUG-115832](https://bugreports.qt.io/browse/QTBUG-115832) iOS:
About Qt dialog displays incorrectly when launched from menu
* [QTBUG-117097](https://bugreports.qt.io/browse/QTBUG-117097) [Windows]
Sporadic crash on
QNetworkConnectionEvents::getNetworkConnectionFromAdapterGuid()
* [QTBUG-116557](https://bugreports.qt.io/browse/QTBUG-116557) [REG
6.2.4 → 6.5.2]: TextField in StackView doesn't receive KeyEvents in Qt
6.5.2 wasm
* [QTBUG-117200](https://bugreports.qt.io/browse/QTBUG-117200) Reg ->
6.6b4: Exit warning :"QItemSelectionModel: Selecting when no model has
been set will result in a no-op" from apps with  sort proxy filter model
* [QTBUG-116752](https://bugreports.qt.io/browse/QTBUG-116752) Floatable
non-closable dock widget can be closed when floating, but cannot be
reopened
* [QTBUG-116890](https://bugreports.qt.io/browse/QTBUG-116890) Typo in
the document
* [QTBUG-117109](https://bugreports.qt.io/browse/QTBUG-117109) QBindable
example fails to configure
* [QTBUG-116903](https://bugreports.qt.io/browse/QTBUG-116903) [REG
6.5.0-6.5.2][macOS] Emoji edit menu items are not visible in a specific
case
* [QTBUG-117383](https://bugreports.qt.io/browse/QTBUG-117383)
QFile::moveToTrash does nothing but returns true
* [QTBUG-115196](https://bugreports.qt.io/browse/QTBUG-115196) QMenubar
only works once
* [QTBUG-116769](https://bugreports.qt.io/browse/QTBUG-116769) [Boot2Qt]
QMenu not re-appearing after closing in widgets app
* [QTBUG-117483](https://bugreports.qt.io/browse/QTBUG-117483)
QWeakPointer's converting move constructor is not threadsafe
* [QTBUG-115486](https://bugreports.qt.io/browse/QTBUG-115486) Item view
headers with stylesheets include space for sort indicator on all
sections
* [QTBUG-117482](https://bugreports.qt.io/browse/QTBUG-117482) should be
"external" instead of  'exernal'
* [QTBUG-116926](https://bugreports.qt.io/browse/QTBUG-116926) Table
view delegate(derived from QStyledItemDelegate) can not get new value
when Spinbox loses focus and spinbox->setKeyboardTracking(false)
* [QTBUG-117412](https://bugreports.qt.io/browse/QTBUG-117412) Vulkan
instance validation error on Raspberry Pi 4
* [QTBUG-117416](https://bugreports.qt.io/browse/QTBUG-117416) RPi4 with
Vulkan: choosing the output screen does not work
* [QTBUG-75456](https://bugreports.qt.io/browse/QTBUG-75456) Streaming
XMLs from reader to writer changes namespace name
* [QTBUG-109465](https://bugreports.qt.io/browse/QTBUG-109465) [REG:
5.15 → 6.2] binding doesn't update when it should
* [QTBUG-117518](https://bugreports.qt.io/browse/QTBUG-117518) syncqt:
qt_sync_skip_header_check header not skipped
* [QTBUG-117509](https://bugreports.qt.io/browse/QTBUG-117509) Examples
that set OUTPUT_NAME will not build for Android
* [QTBUG-117674](https://bugreports.qt.io/browse/QTBUG-117674) [Reg
5.15->6.x] CONFIG += qt causes failure to link to WinMain
* [QTBUG-107598](https://bugreports.qt.io/browse/QTBUG-107598)
HorizontalHeaderView crashes the app if it's synced to model changed
from bg thread
* [QTBUG-102196](https://bugreports.qt.io/browse/QTBUG-102196)
QDockWidget: wrong mouse cursor icon used when dock widget floating, has
custom title bar & contains window container
* [QTBUG-109718](https://bugreports.qt.io/browse/QTBUG-109718)
QWebSocket cannot handle HTTP 407 response ("Proxy Authentication
Required")
* [QTBUG-115233](https://bugreports.qt.io/browse/QTBUG-115233) OpenSSL-3
QCryptographicHash leaks OSSL_PROVIDER_load()'ed objects
* [QTBUG-89904](https://bugreports.qt.io/browse/QTBUG-89904) Possible
error in Qt 6 "Container Classes" documentation
* [QTBUG-117644](https://bugreports.qt.io/browse/QTBUG-117644) Orca
screen reader doesn't announce combobox value when focused
* [QTBUG-114437](https://bugreports.qt.io/browse/QTBUG-114437) REG:
Android: Layout in display cut mode being overridden to short edges
always
* [QTBUG-96877](https://bugreports.qt.io/browse/QTBUG-96877) Qt6 won't
render into cutout area (regression)
* [QTBUG-117820](https://bugreports.qt.io/browse/QTBUG-117820) xcb:
Adding and removing devices while the application is running may spam
the application output with unregistered device messages
* [QTBUG-117787](https://bugreports.qt.io/browse/QTBUG-117787) Cached
network requests leak memory
* [QTBUG-117764](https://bugreports.qt.io/browse/QTBUG-117764) [REG
6.5.1->6.5.2] Setting a DockWidget title when the DockWidget is closed
causes windowTitle to be null or desync
* [QTBUG-117705](https://bugreports.qt.io/browse/QTBUG-117705) Incorrect
documentation for QStringEncoder and QStringDecoder
* [QTBUG-117817](https://bugreports.qt.io/browse/QTBUG-117817)
Windeployqt --qpaths
* [QTBUG-117745](https://bugreports.qt.io/browse/QTBUG-117745) Warning
message from app compiled with XCode 15
* [QTBUG-117473](https://bugreports.qt.io/browse/QTBUG-117473) crash
occuring at shutdown
* [QTBUG-113486](https://bugreports.qt.io/browse/QTBUG-113486) Inactive
components not correcly rendered in dark-mode environments in Qt 6.5.0
* [QTBUG-109025](https://bugreports.qt.io/browse/QTBUG-109025) High DPI
scaling breaks Mouse/Stylus on Android
* [QTBUG-117950](https://bugreports.qt.io/browse/QTBUG-117950)
qxkbcommon.cpp:242:16: error: 'XKB_KEY_dead_lowline' was not declared in
this scope
* [QTBUG-112879](https://bugreports.qt.io/browse/QTBUG-112879) [QT6.5]
gtk3 theme glitches when moving the window
* [QTBUG-117153](https://bugreports.qt.io/browse/QTBUG-117153) lastest
commit for QLoggingCategory trigger compile error in other impotant
project
* [QTBUG-86297](https://bugreports.qt.io/browse/QTBUG-86297) Qt does not
handle the ACTION_POINTER_UP  event on android
* [QTBUG-115161](https://bugreports.qt.io/browse/QTBUG-115161) Crash in
QAccessibleComboBox::focusChild()
* [QTBUG-116167](https://bugreports.qt.io/browse/QTBUG-116167) Duplicate
requests of QNetworkAccessManager do not work
* [QTBUG-115446](https://bugreports.qt.io/browse/QTBUG-115446)
qcocoanativeinterface.mm:4:10: fatal error:
'QtGui/private/qopenglcontext_p.h' file not found
* [QTBUG-117779](https://bugreports.qt.io/browse/QTBUG-117779) [Reg
6.5.3->6.5.2] Showing a secondary Window is broken: the second Window
unexpectedly depends on the main Window position
* [QTBUG-118192](https://bugreports.qt.io/browse/QTBUG-118192)
QNetworkAccessManager hang with low integrity level (low IL) sandboxing
* [QTBUG-118041](https://bugreports.qt.io/browse/QTBUG-118041) selftests
don't appear to respect ASAN_OPTIONS environment variable
* [QTBUG-117490](https://bugreports.qt.io/browse/QTBUG-117490) QNetworkI
nformation:loadBackendByFeatures(QNetworkInformation::Feature::Reachabil
ity) doesn't work in snap
* [QTBUG-117367](https://bugreports.qt.io/browse/QTBUG-117367) [Reg 5.15
->6.x] Android: Unable to dismiss "teardrop" cursor from text inputs
* [QTBUG-117804](https://bugreports.qt.io/browse/QTBUG-117804)
Incomplete JPEG writing after libjpeg-turbo 3.0.0 upgrade
* [QTBUG-106527](https://bugreports.qt.io/browse/QTBUG-106527) AT-SPI2:
Incorrect sizes returned for WINDOW and PARENT coordinates
* [QTBUG-118320](https://bugreports.qt.io/browse/QTBUG-118320) [Reg
6.4.3->6.5] Application window not active after closing message box
* [QTBUG-104905](https://bugreports.qt.io/browse/QTBUG-104905) Window
modal not blocking ancestor window interaction on Mac
* [QTBUG-118419](https://bugreports.qt.io/browse/QTBUG-118419) [Reg
6.4->6.5] Cannot create button with menu in message box
* [QTBUG-118308](https://bugreports.qt.io/browse/QTBUG-118308) [Reg
6.4->6.5] QMessageBox::set(Default|Escape)Button does not work
* [QTBUG-118244](https://bugreports.qt.io/browse/QTBUG-118244)
QVulkanWindow::grab() assumes RGBA which leads to inverted R and B
channels
* [QTBUG-118315](https://bugreports.qt.io/browse/QTBUG-118315)
Misleading documentation of QWaylandApplication
* [QTBUG-118586](https://bugreports.qt.io/browse/QTBUG-118586)
QTimeZone::isTimeZoneIdAvailable is giving wrong result.
* [QTBUG-117428](https://bugreports.qt.io/browse/QTBUG-117428) [Reg
6.4->6.5] QWizard does not draw the buttons
* [QTBUG-117897](https://bugreports.qt.io/browse/QTBUG-117897)
QWidget::createWindowContainer child does not follow parent position
* [QTBUG-118612](https://bugreports.qt.io/browse/QTBUG-118612) Large
size cursor overlaps tooltips on linux
* [QTBUG-118649](https://bugreports.qt.io/browse/QTBUG-118649)
tst_QGlyphRun fails with Linux on ARM
* [QTBUG-118318](https://bugreports.qt.io/browse/QTBUG-118318)
QStringConverter/Win doesn't handle resumption for encodings with more
than 2 octets per character for convertToUnicode
* [QTBUG-118241](https://bugreports.qt.io/browse/QTBUG-118241)
QMessageBox::button(QMessageBox::Close)->setText() does not work
* [QTBUG-115005](https://bugreports.qt.io/browse/QTBUG-115005) [Android]
Text cursor handle visible out of the TextEdit clip region
* [QTBUG-118553](https://bugreports.qt.io/browse/QTBUG-118553) Incorrect
composition when place a software-rendered widget over a OpenGL-based
widget
* [QTBUG-118703](https://bugreports.qt.io/browse/QTBUG-118703) Crash
(divison by zero) in QLocaleData::applyIntegerFormatting()
* [QTBUG-118227](https://bugreports.qt.io/browse/QTBUG-118227)
QCryptographicHash broken with OpenSSL 3 (feature "openssl_hash")
* [QTBUG-117460](https://bugreports.qt.io/browse/QTBUG-117460) Android
FileDialog: 2nd and subsequent nameFilters are ignored
* [QTBUG-111952](https://bugreports.qt.io/browse/QTBUG-111952) tslib
input plugin broken
* [QTBUG-113307](https://bugreports.qt.io/browse/QTBUG-113307) tslib
input not working
* [QTBUG-118759](https://bugreports.qt.io/browse/QTBUG-118759)
[Regr:6.5->6.6] QDateTime comparison performance regression on macOS
* [QTBUG-116763](https://bugreports.qt.io/browse/QTBUG-116763) out-of-
bounds operator+
* [QTBUG-118667](https://bugreports.qt.io/browse/QTBUG-118667)
QIcon::addFile() with an invalid filename results in QFile::isNull() ==
false
* [QTBUG-116550](https://bugreports.qt.io/browse/QTBUG-116550)
[schannel] Qt warning "QIODevice::write (QTcpSocket): device not open"
* [QTBUG-118627](https://bugreports.qt.io/browse/QTBUG-118627) Build
error for QNX, incomplete type QQnxWindowMapper
* [QTBUG-114971](https://bugreports.qt.io/browse/QTBUG-114971)
QAndroidBinder: implementation for native methods missing
* [QTBUG-118695](https://bugreports.qt.io/browse/QTBUG-118695) popup
menu on QToolButton displays at wrong screen
* [QTBUG-93368](https://bugreports.qt.io/browse/QTBUG-93368) Windows:
QGuiApplication::primaryScreenChanged is not emitted when changing
primary screen
* [QTBUG-116013](https://bugreports.qt.io/browse/QTBUG-116013)
QHeaderView::resetDefaultSectionSize doesn't invalidate cached size
hints / update view
* [QTBUG-118741](https://bugreports.qt.io/browse/QTBUG-118741) Windows:
QNetworkInformation does not report "metered" feaature
* [QTBUG-117499](https://bugreports.qt.io/browse/QTBUG-117499) Mouse
scroll events stop working with `-platform windows:reverse`
* [QTBUG-28463](https://bugreports.qt.io/browse/QTBUG-28463) Unable to
use Arabic right to left (RTL) layout in the title bar of own custom
dialog.
* [QTBUG-118580](https://bugreports.qt.io/browse/QTBUG-118580)
QPrinter::setPageLayout does behaves different on windows and Linux
* [QTBUG-117206](https://bugreports.qt.io/browse/QTBUG-117206)
QT_ANDROID_EXTRA_LIBS ignored for secondary ABIs
* [QTBUG-118870](https://bugreports.qt.io/browse/QTBUG-118870) Icon of a
cell with a background color disappears if a stylesheet is used for
QTreeView::indicator
* [QTBUG-116757](https://bugreports.qt.io/browse/QTBUG-116757)
QMessageBox does not show hyperlinks on macOS
* [QTBUG-118992](https://bugreports.qt.io/browse/QTBUG-118992)
Reg6.4->6.5 QMessageBox Hide/Show detailed section is gone
* [QTBUG-114760](https://bugreports.qt.io/browse/QTBUG-114760)
tst_QComboBox::popupPositionAfterStyleChange is flaky
* [QTBUG-116349](https://bugreports.qt.io/browse/QTBUG-116349) Doc:
Documentation of qAsConst missing
* [QTBUG-117900](https://bugreports.qt.io/browse/QTBUG-117900) [REG
5.15.2->6.5.1] Behavioural inconsistency when reparenting QStandardItems
* [QTBUG-89145](https://bugreports.qt.io/browse/QTBUG-89145)
QStandardItemModel takeItem / takeChild does not emit the right signals
* [QTBUG-119053](https://bugreports.qt.io/browse/QTBUG-119053) macOS:
QSystemTrayIcon::activated signal slot is called multiple times if
QSystemTrayIcon::setContextMenu is called from it
* [QTBUG-119068](https://bugreports.qt.io/browse/QTBUG-119068)
QSystemTrayIcon - unable to reset context menu
* [QTBUG-101219](https://bugreports.qt.io/browse/QTBUG-101219) Hidden
tabs via QTabWidget::setTabVisible are still available
* [QTBUG-118194](https://bugreports.qt.io/browse/QTBUG-118194) Adding
QOpenGLWidget to FullScreen window breaks Full Screen
* [QTBUG-104641](https://bugreports.qt.io/browse/QTBUG-104641) QDial:
division by zero while changing minimal or maximum value
* [QTBUG-78737](https://bugreports.qt.io/browse/QTBUG-78737) Windows:
Two menus instead of one appear by clicking on the QSystemTrayIcon
* [QTBUG-117111](https://bugreports.qt.io/browse/QTBUG-117111)
QProperty's documentation has a Note section which seems to be displayed
in an unintended way
* [QTBUG-118993](https://bugreports.qt.io/browse/QTBUG-118993) MSVC
warns as error on stdext::checked_array_iterator in QtCore/qvector.h
* [QTBUG-119044](https://bugreports.qt.io/browse/QTBUG-119044)
CXXFLAGS='-D_GLIBCXX_DEBUG' build crashes (e.g. in sharedmemory example)
* [QTBUG-118133](https://bugreports.qt.io/browse/QTBUG-118133) Windows
QPA:  QSystemIconTrayIcon::show() not working after calling hide()
* [QTBUG-105150](https://bugreports.qt.io/browse/QTBUG-105150)
QStandardItem is using un-documented value of Qt::ItemDataRole
* [QTBUG-117494](https://bugreports.qt.io/browse/QTBUG-117494)
QSvgRenderer produces different results randomly when it is run the same
way  many times
* [QTBUG-105395](https://bugreports.qt.io/browse/QTBUG-105395)
WM_TRANSIENT_FOR is not kept in sync
* [QTBUG-118458](https://bugreports.qt.io/browse/QTBUG-118458) TLS
Invalid Token
* [QTBUG-116295](https://bugreports.qt.io/browse/QTBUG-116295) Qt build
with SSL3, is not picking up SSL3
* [PYSIDE-2525](https://bugreports.qt.io/browse/PYSIDE-2525) Segfaults
related to QMenu on macOS
* [QTBUG-41696](https://bugreports.qt.io/browse/QTBUG-41696)
QApplication::widgetAt() doesn't work with widgets with
Qt::WA_TransparentForMouseEvents on Mac
* [QTBUG-119092](https://bugreports.qt.io/browse/QTBUG-119092) [REG:
6.5.2->6.5.3] macOS: topLevelAt/widgetAt cannot find something under a
window with setIgnoresMouseEvents set
* [QTBUG-102831](https://bugreports.qt.io/browse/QTBUG-102831)
QCompleter's suggestion list hides native Chinese Input method
* [QTBUG-112479](https://bugreports.qt.io/browse/QTBUG-112479) Touch
Drag doesn't cause mousePressEvent after Touch Press
* [QTBUG-119032](https://bugreports.qt.io/browse/QTBUG-119032) Mouse
Release is not fired with touch screen
* [QTBUG-100688](https://bugreports.qt.io/browse/QTBUG-100688)
TapHandler doesn't emit  onDoubleTapped when using a touchscreen
* [QTBUG-119219](https://bugreports.qt.io/browse/QTBUG-119219) macOS:
NPE in QNSWindow applicationActivationChanged
* [QTBUG-118605](https://bugreports.qt.io/browse/QTBUG-118605) CTRL+Tab
don't work in combobox
* [QTBUG-119366](https://bugreports.qt.io/browse/QTBUG-119366) QTabBar
is incorrectly offset when changing the TabPosition
* [QTBUG-117765](https://bugreports.qt.io/browse/QTBUG-117765) moc
chokes on <concepts> from xcode13
* [QTBUG-119526](https://bugreports.qt.io/browse/QTBUG-119526) [Reg
6.6.0->6.6.1]QCocoaAccessibility Crash with Mac VoiceOver enabled
* [QTBUG-118585](https://bugreports.qt.io/browse/QTBUG-118585) "Crash"
in QMacAccessibilityElement initWithId:role:
* [QTBUG-108796](https://bugreports.qt.io/browse/QTBUG-108796) Some
examples crash when running with Qt 6.5 kit
* [QTBUG-116789](https://bugreports.qt.io/browse/QTBUG-116789) [REG]
-platform linux-clang-libc++ -c++std c++2b fails to compile synctqt
* [QTBUG-116064](https://bugreports.qt.io/browse/QTBUG-116064) [REG SiC
6.4 -> 6.5] qHash(qfloat16(x)) is now ambiguous on GCC13
* [QTBUG-116076](https://bugreports.qt.io/browse/QTBUG-116076)
qHash(qfloat16(x), seed) != qHash(float(x), seed) unless seed == 0
* [QTBUG-109444](https://bugreports.qt.io/browse/QTBUG-109444) Qt's
CMake deployment API Error: Extra libraries copied
* [QTBUG-113645](https://bugreports.qt.io/browse/QTBUG-113645)
QWindowsTheme::queryHighContrast: incorrect parameters passed to
SystemParametersInfo for SPI_GETHIGHCONTRAST
* [QTBUG-113123](https://bugreports.qt.io/browse/QTBUG-113123) Mixed
indexes in QListWidget when setSortingEnabled is True
* [QTBUG-116483](https://bugreports.qt.io/browse/QTBUG-116483) qttools'
CMake test test_uiplugin_via_designer fails
* [QTBUG-109708](https://bugreports.qt.io/browse/QTBUG-109708) Startup
crash in QRhiD3D11::endFrame() with nullptr access
* [QTBUG-110921](https://bugreports.qt.io/browse/QTBUG-110921)
Documentation for building iOS apps is plain wrong
* [QTBUG-116784](https://bugreports.qt.io/browse/QTBUG-116784) iOS built
with CMAKE is not uploadable on Appstore (Transporter)
* [QTBUG-117535](https://bugreports.qt.io/browse/QTBUG-117535) Cannot
enable at-spi bridge with wayland
* [QTBUG-116017](https://bugreports.qt.io/browse/QTBUG-116017) [REG]
tst_QDate::startOfDay_endOfDay_bounds() test failure
* [PYSIDE-2492](https://bugreports.qt.io/browse/PYSIDE-2492) uic does
not generate enumeration name into enum values causing type checking
warnings
* [QTBUG-118211](https://bugreports.qt.io/browse/QTBUG-118211)
Generation of alias targets for executable needs to be guarded
* [QTBUG-118569](https://bugreports.qt.io/browse/QTBUG-118569) crash in
qschannelbackend
QTlsPrivate::X509CertificateSchannel::QSslCertificate_from_CERT_CONTEXT
* [QTBUG-118909](https://bugreports.qt.io/browse/QTBUG-118909) Touches
cancelled when interacting with multiple windows
* [QTBUG-111873](https://bugreports.qt.io/browse/QTBUG-111873)
qt_attributions.json files should be valid JSON
* [QTBUG-116532](https://bugreports.qt.io/browse/QTBUG-116532)
tst_QStandardItemModel leaks memory in multiple test cases
* [QTBUG-87438](https://bugreports.qt.io/browse/QTBUG-87438) corelib
plugin tests fail on Android
* [QTBUG-114253](https://bugreports.qt.io/browse/QTBUG-114253) [REG:
5.11->6] Performance issue with loading images in static build
* [QTBUG-118578](https://bugreports.qt.io/browse/QTBUG-118578) Undocking
tabbed widget from floating window creates empty redundant window
* [QTBUG-118579](https://bugreports.qt.io/browse/QTBUG-118579) Undocking
tabbed widget from main window onto the floating window crashes app
* [QTBUG-119216](https://bugreports.qt.io/browse/QTBUG-119216) macOS:
REG->6.5: DnD with custom text MIME type got broken/crashes
* [QTBUG-118489](https://bugreports.qt.io/browse/QTBUG-118489) Can't tab
to last button in QDialogButtonBox

### qtsvg
* [QTBUG-113042](https://bugreports.qt.io/browse/QTBUG-113042) Loading
particular svg file takes too long
* [QTBUG-117944](https://bugreports.qt.io/browse/QTBUG-117944) [Qt SVG]
QML Image bad source crashes application instead of error status
(QSvgHandler::parse)

### qtdeclarative
* [QTBUG-116795](https://bugreports.qt.io/browse/QTBUG-116795)
QQuickBasicProgressBar::setColor() does nothing after initialization?
* [QTBUG-116672](https://bugreports.qt.io/browse/QTBUG-116672)
Application crashes when MenuItem text contains img tag
* [QTBUG-116681](https://bugreports.qt.io/browse/QTBUG-116681) QtCore
Settings does not support ini files located in resources
* [QTBUG-114144](https://bugreports.qt.io/browse/QTBUG-114144) qmllint:
false positive [read-only-property] with QQmlListProperty
* [QTBUG-116748](https://bugreports.qt.io/browse/QTBUG-116748)
HorizontalHeaderView does not use QAbstractItemModel::roleNames()
* [QTBUG-117062](https://bugreports.qt.io/browse/QTBUG-117062)
DelegatePage in Qt Quick Controls - Gallery example is broken
* [QTBUG-115227](https://bugreports.qt.io/browse/QTBUG-115227)
VerticalHeaderView/TableView required properties go all over the place
when using syncView
* [QTBUG-116566](https://bugreports.qt.io/browse/QTBUG-116566) QML
TableView: resizableColumns/resizableRows breaks the default interactive
behavior
* [QTBUG-116153](https://bugreports.qt.io/browse/QTBUG-116153) Qmlformat
makes code uncompilable when destructuring objects in lambda expressions
* [QTBUG-109444](https://bugreports.qt.io/browse/QTBUG-109444) Qt's
CMake deployment API Error: Extra libraries copied
* [QTBUG-115485](https://bugreports.qt.io/browse/QTBUG-115485) QtQuick
shapes example has misleading file names
* [QTBUG-116828](https://bugreports.qt.io/browse/QTBUG-116828) Aborting
incubation may lead to a crash with some controls
* [QTBUG-117642](https://bugreports.qt.io/browse/QTBUG-117642) Crash
when trying to trick property bindings
* [QTBUG-117077](https://bugreports.qt.io/browse/QTBUG-117077) qmllint
does not allow 'print' as invokable method name
* [QTBUG-117513](https://bugreports.qt.io/browse/QTBUG-117513) Restore
pthread_attr_init() to stackPropertiesGeneric() for FreeBSD
* [QTBUG-117361](https://bugreports.qt.io/browse/QTBUG-117361)
qmlcachegen crashes in QQmlJSTypeResolver::adjustTrackedType
* [QTBUG-117130](https://bugreports.qt.io/browse/QTBUG-117130) crash in
tryLoadFromDiskCache with corrupted cache
* [QTBUG-117891](https://bugreports.qt.io/browse/QTBUG-117891) [REG
6.5.2 → 6.5.3] Unable to determine callable overload with QVariantMap
* [QTBUG-113785](https://bugreports.qt.io/browse/QTBUG-113785) Warn
about  setContextProperty() in documentation
* [QTBUG-116804](https://bugreports.qt.io/browse/QTBUG-116804) QML
incubation documentation issues
* [QTBUG-117880](https://bugreports.qt.io/browse/QTBUG-117880) Material
3 misaligns Button icon
* [QTBUG-118100](https://bugreports.qt.io/browse/QTBUG-118100) readonly
property can be written via unqualified access
* [QTBUG-117451](https://bugreports.qt.io/browse/QTBUG-117451)
private/qquickevents_p_p.h: No such file or directory when compiling a
new Qt Quick Project with QML to C++ Compilation
* [QTBUG-117829](https://bugreports.qt.io/browse/QTBUG-117829) QML
engine mis-converts QQmlListProperty
* [QTBUG-108883](https://bugreports.qt.io/browse/QTBUG-108883) Improve
documentation on how to expose value types with enums to QML
* [QTBUG-117384](https://bugreports.qt.io/browse/QTBUG-117384) [REG 6.4
→ 6.5] Calling a Q_INVOKABLE function with a std::vector<long> parameter
zeroes the vector
* [QTBUG-118091](https://bugreports.qt.io/browse/QTBUG-118091) qmltc
includes a non-existent qquickcheckbox_p_p.h
* [QTBUG-117479](https://bugreports.qt.io/browse/QTBUG-117479)
Segmentation fault in qml debugger
* [QTBUG-118469](https://bugreports.qt.io/browse/QTBUG-118469) [REG
6.3.2 → 6.5.0] qsTranslate function no longer translates if directly
bound to property
* [QTBUG-118089](https://bugreports.qt.io/browse/QTBUG-118089) Enums
exposed to QML seem only working when the QML code gets compiled by
qmlsc
* [QTBUG-117922](https://bugreports.qt.io/browse/QTBUG-117922)
Unexpected and inconsistent overload resolution when calling C++ from
QML
* [QTBUG-117788](https://bugreports.qt.io/browse/QTBUG-117788) Assert
due to cyclic dependencies
* [QTBUG-117703](https://bugreports.qt.io/browse/QTBUG-117703)
Unclear/missing documentation on using QML_FOREIGN_NAMESPACE
* [QTBUG-117793](https://bugreports.qt.io/browse/QTBUG-117793) QML-
managed objects are garbage collected when stored in QML-declared list
properties
* [QTBUG-118397](https://bugreports.qt.io/browse/QTBUG-118397)
~QQuickContainer() Crash when calling QQmlIncubator::abort
* [QTBUG-118738](https://bugreports.qt.io/browse/QTBUG-118738) Not
possible to exclude qtquicktimeline and qtquick control styles from the
build
* [QTBUG-118514](https://bugreports.qt.io/browse/QTBUG-118514) [Reg 6.5
-> 6.6] Miscompilation of arithmetic operators
* [QTBUG-118744](https://bugreports.qt.io/browse/QTBUG-118744) Flaky
crash (segfault) when running tst_inputpanel
tst_plugin::test_fullScreenModeWordReselection
* [QTBUG-118163](https://bugreports.qt.io/browse/QTBUG-118163) Flaky
race-condition in QuickTest when running tst_inputpanel built with ASAN
* [QTBUG-118052](https://bugreports.qt.io/browse/QTBUG-118052)
Text.NativeRendering causes text to show through.
* [QTBUG-78441](https://bugreports.qt.io/browse/QTBUG-78441) Text
disappears when using a U+FFFC unicode character
* [QTBUG-117831](https://bugreports.qt.io/browse/QTBUG-117831) [REG:
6.5.2->6.5.3] Destroying active popup with dim layer leaves the dimming
layer behind
* [QTBUG-118897](https://bugreports.qt.io/browse/QTBUG-118897) Qt Quick
TableView performance issue when updating ContentY in onModelChanged
* [QTBUG-118237](https://bugreports.qt.io/browse/QTBUG-118237)
Documentation of QML font weights is incorrect
* [QTBUG-117958](https://bugreports.qt.io/browse/QTBUG-117958)
qt_add_qml_module does not register QML_SINGLETON classes if version
starts with 0
* [QTBUG-116606](https://bugreports.qt.io/browse/QTBUG-116606) unable to
deselect text in text input using touch
* [QTBUG-119024](https://bugreports.qt.io/browse/QTBUG-119024) Window
position is bypassed by Wayland.
* [QTBUG-119065](https://bugreports.qt.io/browse/QTBUG-119065) Unable to
reset tray icon menu for QML SystemTrayIcon
* [QTBUG-117917](https://bugreports.qt.io/browse/QTBUG-117917)
HorizontalHeaderView with plain JavaScript array model crashes on flick
* [QTBUG-115579](https://bugreports.qt.io/browse/QTBUG-115579) Rebinding
of property alias does not work for some aliases that refer to certain
(grouped) properties
* [QTBUG-118856](https://bugreports.qt.io/browse/QTBUG-118856)
Placeholder text does not follow the set horizontalAlignment in Material
style.
* [QTBUG-117160](https://bugreports.qt.io/browse/QTBUG-117160)
touchUngrabEvent is not implemented for qquickflickable
* [QTBUG-93856](https://bugreports.qt.io/browse/QTBUG-93856) Menus with
a certain fixed height, element height and window height not scrolled
when they should
* [QTBUG-118069](https://bugreports.qt.io/browse/QTBUG-118069) Wrong
position reported uppon touch release
* [QTBUG-119091](https://bugreports.qt.io/browse/QTBUG-119091)
QmlCacheGen crashes on QML-file, but won't disclose where/why it cashes
* [QTBUG-53987](https://bugreports.qt.io/browse/QTBUG-53987) Cursor is
not updated on mouse wheel over flickable
* [QTBUG-90457](https://bugreports.qt.io/browse/QTBUG-90457)
HoverHandler.cursorShape doesn't change dynamically within same bounds
* [QTBUG-54019](https://bugreports.qt.io/browse/QTBUG-54019) regression
in certain MouseArea hover use cases
* [QTBUG-119132](https://bugreports.qt.io/browse/QTBUG-119132) it should
be possible to disable the TapHandler.longPressed signal
* [QTBUG-105810](https://bugreports.qt.io/browse/QTBUG-105810) iOS:
TapHandler emits clicked, even if long pressed more than
StyleHint::MousePressAndHoldInterval
* [QTBUG-115696](https://bugreports.qt.io/browse/QTBUG-115696) Delegates
are not re-positioned when ListView orientation is changed runtime
* [QTBUG-119090](https://bugreports.qt.io/browse/QTBUG-119090)
QmlCacheGen miscompiles Enum constant reference, yielding "undefined"
* [QTBUG-115166](https://bugreports.qt.io/browse/QTBUG-115166)
qt_add_qml_module() causes non-Ninja generators to think that projects
are never up-to-date
* [QTBUG-119122](https://bugreports.qt.io/browse/QTBUG-119122) Using a
specific as-cast asserts and fails compilation
* [QTBUG-119181](https://bugreports.qt.io/browse/QTBUG-119181) Crash in
QQmlDelegateModelGroup::insert
* [QTBUG-118779](https://bugreports.qt.io/browse/QTBUG-118779) QT quick
control-wearable demo-example Issue with the background when switching
light/dark mode
* [QTBUG-83155](https://bugreports.qt.io/browse/QTBUG-83155) Roboto font
used in Material style slows down startup time
* [QTBUG-119216](https://bugreports.qt.io/browse/QTBUG-119216) macOS:
REG->6.5: DnD with custom text MIME type got broken/crashes
* [QTBUG-117700](https://bugreports.qt.io/browse/QTBUG-117700)
StackView's enter transitions are broken when pushing/replacing onto an
empty stack
* [QTBUG-117830](https://bugreports.qt.io/browse/QTBUG-117830) Crash on
QQuickMultiEffectPrivate::updateEffectShaders() with nullptr access
* [QTBUG-117806](https://bugreports.qt.io/browse/QTBUG-117806)
QQmlApplicationEngine::loadFromModule() not working on Android
* [QTBUG-117899](https://bugreports.qt.io/browse/QTBUG-117899) [REG
6.4->6.5] Binding Loops -> Wrong layout because of interruption
* [QTBUG-116589](https://bugreports.qt.io/browse/QTBUG-116589) Dynamic
translations seem not working with
QQmlApplicationEngine::loadFromModule()
* [QTBUG-118532](https://bugreports.qt.io/browse/QTBUG-118532)
tst_qquickpopup::doubleClickInMouseArea and overlay are flaky on android
* [QTBUG-117968](https://bugreports.qt.io/browse/QTBUG-117968)
Initialization behavior difference between precompiled and not compiled
QML component
* [QTBUG-117800](https://bugreports.qt.io/browse/QTBUG-117800)
QmlCompiler generates bogus warning about internal conversion
* [QTBUG-118636](https://bugreports.qt.io/browse/QTBUG-118636) Some
missing content of the rich text table while displaying HTML file with
TextArea
* [QTBUG-117795](https://bugreports.qt.io/browse/QTBUG-117795) Bogus
compile warning
* [QTBUG-65012](https://bugreports.qt.io/browse/QTBUG-65012) TapHandler:
should not emit longPressed if the point is dragged
* [QTBUG-115536](https://bugreports.qt.io/browse/QTBUG-115536) Setting
Window.contentOrientation breaks Popup on regular desktop
* [QTBUG-102846](https://bugreports.qt.io/browse/QTBUG-102846) [Windows]
Restoring OpenGL context logic doesn't seem valid

### qtactiveqt
* [QTBUG-100657](https://bugreports.qt.io/browse/QTBUG-100657) Crash
while receiving COM IDispatch events when initializing
* [QTBUG-96871](https://bugreports.qt.io/browse/QTBUG-96871) Crash on
calling connect on   QAxObject source instance
* [QTBUG-119064](https://bugreports.qt.io/browse/QTBUG-119064) Build
fail on Windows (reg 6.5.3 -> 6.6.0)

### qtmultimedia
* [QTBUG-117086](https://bugreports.qt.io/browse/QTBUG-117086) [WMF]
Excessive Qt warning "No audio output"
* [QTBUG-115460](https://bugreports.qt.io/browse/QTBUG-115460) Camera
crash on image acquire on Android
* [QTBUG-116526](https://bugreports.qt.io/browse/QTBUG-116526) Android
camera crash in example project
* [QTBUG-114932](https://bugreports.qt.io/browse/QTBUG-114932)
[DeclarativeCamera] Capture crashes the example
* [QTBUG-117056](https://bugreports.qt.io/browse/QTBUG-117056) ERROR:
AddressSanitizer: heap-use-after-free in
tst_QAudioSink::pullResumeFromUnderrun()
* [QTBUG-114083](https://bugreports.qt.io/browse/QTBUG-114083)
[QtDeclarativeCamera] Popup list of available cameras is not available
after changing the orientation
* [QTBUG-116688](https://bugreports.qt.io/browse/QTBUG-116688)
QVideoFrame::toImage: failed to get textures for frame; format: 172
textureConverter null
* [QTBUG-116801](https://bugreports.qt.io/browse/QTBUG-116801) Path with
space leads to crash Qmultimedia example
* [QTBUG-117599](https://bugreports.qt.io/browse/QTBUG-117599)
Compilation error for FFmpeg with dynamically linked OpenSSL
* [QTBUG-115568](https://bugreports.qt.io/browse/QTBUG-115568) Missing
type "QScreen" is referenced in qmltypes
* [QTBUG-115444](https://bugreports.qt.io/browse/QTBUG-115444)
MediaPlayer has no sound on Android
* [QTBUG-116779](https://bugreports.qt.io/browse/QTBUG-116779) FFmpeg
backend: GUI thread freezes when initializing an network source
* [QTBUG-117006](https://bugreports.qt.io/browse/QTBUG-117006)
MediaPlayer::playing isn't always true when it should be
* [QTBUG-118749](https://bugreports.qt.io/browse/QTBUG-118749)
tst_qtexttospeech_qml (Failed)
* [QTBUG-118624](https://bugreports.qt.io/browse/QTBUG-118624) [WASM]
Qt's internal shaders can easily conflict with user shaders
* [QTBUG-118706](https://bugreports.qt.io/browse/QTBUG-118706) Crash on
QWindowsMediaDevices::availableDevices() with nullptr access
* [QTBUG-117744](https://bugreports.qt.io/browse/QTBUG-117744) Bluish
hue in video
* [QTBUG-115075](https://bugreports.qt.io/browse/QTBUG-115075)
WebAssembly audio input not working
* [QTBUG-119087](https://bugreports.qt.io/browse/QTBUG-119087)
MediaPlayer-Graphic&Multimedia-example Volume slider is being compressed
and becomes unusable
* [QTBUG-116991](https://bugreports.qt.io/browse/QTBUG-116991)
QVideoFrame allocation broken for YUV422P
* [QTBUG-118699](https://bugreports.qt.io/browse/QTBUG-118699) The video
playback is corrupted with Android native backend
* [QTBUG-116444](https://bugreports.qt.io/browse/QTBUG-116444) [Windows]
Qt warning "Failed to retrieve default audio endpoint -2147023728"
* [QTBUG-116978](https://bugreports.qt.io/browse/QTBUG-116978)
MediaPlayer::position cannot be declared in QML
* [QTBUG-107563](https://bugreports.qt.io/browse/QTBUG-107563)
QMediaPlayer can't play AVI with Apple codecs
* [QTBUG-108403](https://bugreports.qt.io/browse/QTBUG-108403) FFmpeg
backend doesn't work as expected
* [QTBUG-110498](https://bugreports.qt.io/browse/QTBUG-110498)
QtMultimedia leaks a lot of memory on Windows when opengl contexts are
shared
* [QTBUG-117099](https://bugreports.qt.io/browse/QTBUG-117099) Video
jerks when playing (Windows backend)
* [QTBUG-110012](https://bugreports.qt.io/browse/QTBUG-110012) QML Video
Example: example not displaying video
* [QTBUG-114954](https://bugreports.qt.io/browse/QTBUG-114954) Media
Player Example: Default video does not play on Android
* [QTBUG-113980](https://bugreports.qt.io/browse/QTBUG-113980) Playing
videos over network still an issue on Android
* [QTBUG-116782](https://bugreports.qt.io/browse/QTBUG-116782) FFmpeg
backend: RTSP stream is very choppy in Qt, compared to FFplay
* [QTBUG-117528](https://bugreports.qt.io/browse/QTBUG-117528) [REG
6.3.2->6.5.2] QMediaPlayer always captures the audio device what blocks
sleep mode on Windows
* [QTBUG-117612](https://bugreports.qt.io/browse/QTBUG-117612) [REG
6.3.2->6.5.2] Windows 10: CPU core stucks at minimum friequency
* [QTBUG-117919](https://bugreports.qt.io/browse/QTBUG-117919) REG:
Qt6.7 QML MediaPlayer duration property doesn't update declaratively
* [QTBUG-111045](https://bugreports.qt.io/browse/QTBUG-111045)
QSoundEffect not playing
* [QTBUG-118587](https://bugreports.qt.io/browse/QTBUG-118587) [WMF]
Video position may exceed it's duration
* [QTBUG-101364](https://bugreports.qt.io/browse/QTBUG-101364) qmllint
spurious error: QML State AnchorChanges: with type QQuickAnchorLine to
QQmlScriptString of QQmlScriptString
* [QTBUG-118654](https://bugreports.qt.io/browse/QTBUG-118654)
QMediaPlayer does not allow negative playback rate hence no rewinding
possible
* [QTBUG-118510](https://bugreports.qt.io/browse/QTBUG-118510) Errors
when building Qt with FFMpeg/vaapi on Ubuntu 20.04
* [QTBUG-108754](https://bugreports.qt.io/browse/QTBUG-108754) Video not
stretched properly
* [QTBUG-116020](https://bugreports.qt.io/browse/QTBUG-116020) Audio
from QMediaPlayer crackles and stutters on pause and resume
* [QTBUG-117407](https://bugreports.qt.io/browse/QTBUG-117407) Document
limitations of QScreenCapture

### qttools
* [QTBUG-117214](https://bugreports.qt.io/browse/QTBUG-117214) "Multiple
Inheritance" example - medata broken
* [QTBUG-116483](https://bugreports.qt.io/browse/QTBUG-116483) qttools'
CMake test test_uiplugin_via_designer fails
* [QTBUG-116335](https://bugreports.qt.io/browse/QTBUG-116335)
QMessageBox::options not correctly linked to
* [QTBUG-117510](https://bugreports.qt.io/browse/QTBUG-117510) qdoc:
Incorrect links to qhash-proxy.html page
* [QTBUG-117974](https://bugreports.qt.io/browse/QTBUG-117974) CMake
Error at qttools/src/assistant/qhelpgenerator/CMakeLists.txt:66
(add_dependencies)
* [QTBUG-115720](https://bugreports.qt.io/browse/QTBUG-115720) \value
followed by \table merges contents and breaks table
* [QTBUG-115537](https://bugreports.qt.io/browse/QTBUG-115537) [QML
Docs] Image.fillMode enum documentation has a broken table formatting
* [QTBUG-118769](https://bugreports.qt.io/browse/QTBUG-118769) lupdate
leaves behind .json files if it fails to load pro file
* [QTBUG-115166](https://bugreports.qt.io/browse/QTBUG-115166)
qt_add_qml_module() causes non-Ninja generators to think that projects
are never up-to-date
* [QTBUG-116833](https://bugreports.qt.io/browse/QTBUG-116833) QDoc
generates .sha1 files for each qhp file, but they all contain wrong hash
* [PYSIDE-2492](https://bugreports.qt.io/browse/PYSIDE-2492) uic does
not generate enumeration name into enum values causing type checking
warnings

### qtdoc
* [QTBUG-54267](https://bugreports.qt.io/browse/QTBUG-54267) Qt Quick
Calqlatr example does not properly reflect the current way of using Qt
Quick
* [QTBUG-117089](https://bugreports.qt.io/browse/QTBUG-117089)
qt_add_qml_module - what has changed between versions?
* [QTBUG-118104](https://bugreports.qt.io/browse/QTBUG-118104) Typo in
the document
* [QTBUG-118211](https://bugreports.qt.io/browse/QTBUG-118211)
Generation of alias targets for executable needs to be guarded
* [QTBUG-118789](https://bugreports.qt.io/browse/QTBUG-118789) Target
Devices used in Automated Testing is out-dated
* [QTBUG-118043](https://bugreports.qt.io/browse/QTBUG-118043) QML Media
Player doesn't fit on smaller screens
* [QTBUG-119286](https://bugreports.qt.io/browse/QTBUG-119286) Typos in
Thermostat example
* [QTBUG-119297](https://bugreports.qt.io/browse/QTBUG-119297) Room
icons in Thermostat example not correct
* [QTBUG-119290](https://bugreports.qt.io/browse/QTBUG-119290) Icon
highlighting in Thermostat example is barely visible
* [QTBUG-119320](https://bugreports.qt.io/browse/QTBUG-119320)
Thermostat example buttons inactive
* [QTBUG-119294](https://bugreports.qt.io/browse/QTBUG-119294) Settings
tab in Thermostat example behaves oddly
* [QTBUG-110921](https://bugreports.qt.io/browse/QTBUG-110921)
Documentation for building iOS apps is plain wrong
* [QTBUG-116784](https://bugreports.qt.io/browse/QTBUG-116784) iOS built
with CMAKE is not uploadable on Appstore (Transporter)
* [QTBUG-114437](https://bugreports.qt.io/browse/QTBUG-114437) REG:
Android: Layout in display cut mode being overridden to short edges
always
* [QTBUG-96877](https://bugreports.qt.io/browse/QTBUG-96877) Qt6 won't
render into cutout area (regression)
* [QTIFW-3139](https://bugreports.qt.io/browse/QTIFW-3139) Online
Installer 4.6.1 : Command Line Interface "-default-answer" "--accept-
messages" doesn't work together
* [QTBUG-114375](https://bugreports.qt.io/browse/QTBUG-114375) User got
stuck and is not taken back to the home in coffee example
* [QTBUG-114713](https://bugreports.qt.io/browse/QTBUG-114713)
Enhancements in the Color Palette REST API example

### qtlocation
* [QTBUG-118447](https://bugreports.qt.io/browse/QTBUG-118447) Here
plugin does not support authentication via apiKey

### qtpositioning
* [QTBUG-116645](https://bugreports.qt.io/browse/QTBUG-116645) [Android]
providerList() returns NULL list

### qtconnectivity
* [QTBUG-115370](https://bugreports.qt.io/browse/QTBUG-115370) Android
device (Android12 Go Edition) cannot reconnect  to BLE peripheral device
* [QTBUG-118895](https://bugreports.qt.io/browse/QTBUG-118895) No
signals are emmited after error Failed to create pairing
"org.bluez.Error.AuthenticationCanceled"

### qtwayland
* [QTBUG-117067](https://bugreports.qt.io/browse/QTBUG-117067) ERROR:
AddressSanitizer: heap-use-after-free in tst_seatv4::animatedCursor()
* [QTBUG-112161](https://bugreports.qt.io/browse/QTBUG-112161) Drag and
drop with wayland display error
* [QTBUG-118042](https://bugreports.qt.io/browse/QTBUG-118042) cannot
forward key event from compositor to client
* [QTBUG-111022](https://bugreports.qt.io/browse/QTBUG-111022) Custom
Extension example not working on NVIDIA

### qt3d
* [QTBUG-114037](https://bugreports.qt.io/browse/QTBUG-114037) [Android]
Could not launch any app with Qt 3D module on Android 12
* [QTBUG-114036](https://bugreports.qt.io/browse/QTBUG-114036) [Android]
Qt3D.Renderer.RHI.Backend: : Failed to build graphics pipeline: Creation
Failed
* [QTBUG-116770](https://bugreports.qt.io/browse/QTBUG-116770) Race
Condition or Crash in Qt3D due to Thread Affinity of
NodePostConstructorInit::processNodes()
* [QTBUG-117065](https://bugreports.qt.io/browse/QTBUG-117065) ERROR:
AddressSanitizer: memcpy-param-overlap in
tst_AspectCommandDebugger::checkBufferTrim()

### qtserialport
* [QTBUG-115205](https://bugreports.qt.io/browse/QTBUG-115205)
QSerialPort does not properly set baud rate

### qtwebchannel
* [QTBUG-115779](https://bugreports.qt.io/browse/QTBUG-115779)
Webchannel's standalone example doesn't work when opened with CMake

### qtwebengine
* [QTBUG-115753](https://bugreports.qt.io/browse/QTBUG-115753) ERROR:
AddressSanitizer: heap-use-after-free  in tst_origins
* [QTBUG-115994](https://bugreports.qt.io/browse/QTBUG-115994) Duplicate
character when long-pressing for accented char on macOS/webengine
* [QTBUG-112614](https://bugreports.qt.io/browse/QTBUG-112614)
QPdfPageNavigator::backAvailableChanged and forwardAvailableChanged are
not always emitted for jumps
* [QTBUG-116445](https://bugreports.qt.io/browse/QTBUG-116445)
[REG][Windows] Crash on NativeSkiaOutputDevice::releaseTexture() with
nullptr access
* [QTBUG-117119](https://bugreports.qt.io/browse/QTBUG-117119) Some Qt
WebEngine documentation issues
* [QTBUG-117489](https://bugreports.qt.io/browse/QTBUG-117489) [REG 6.4
-> 6.5] Invalid QDataStream data when serializing uninited
QWebEngineHistory
* [QTBUG-118455](https://bugreports.qt.io/browse/QTBUG-118455) Crash in
Compositor::Observer::compositor() with nullptr access
* [QTBUG-118850](https://bugreports.qt.io/browse/QTBUG-118850) WebEngine
build fails in yocto for lts-6.5
* [QTBUG-104610](https://bugreports.qt.io/browse/QTBUG-104610) Does
WebEngine support document download and print operations in the document
preview screen?
* [QTBUG-117382](https://bugreports.qt.io/browse/QTBUG-117382) Clicking
the print button in built-in PDF viewer crashes
* [QTBUG-116478](https://bugreports.qt.io/browse/QTBUG-116478) [Reg
5.14.2 -> 5.15.0] Significant performance decrease when loading
QtWebEngine pages simultaneously in many windows
* [QTBUG-117673](https://bugreports.qt.io/browse/QTBUG-117673) Only
black screen and mouse is captured on wayland

* CVE-2023-5217: Heap buffer overflow in vp8 encoding in libvpx  
* CVE-2023-5218: Use after free in Site Isolation  
* CVE-2023-5474: Heap buffer overflow in PDF  
* CVE-2023-5475: Inappropriate implementation in DevTools  
* CVE-2023-5482  
* CVE-2023-5484: Inappropriate implementation in Navigation  
* CVE-2023-5487: Inappropriate implementation in Fullscreen  
* CVE-2023-5849  
* CVE-2023-5996: Use after free in WebAudio  
* CVE-2023-5997: Use after free in Garbage Collection  
* CVE-2023-6112: Use after free in Navigation  
* CVE-2023-6345: Integer overflow in Skia  
* CVE-2023-6347: Use after free in Mojo  
* CVE-2023-45853: Buffer overflow in MiniZip  
* Security bug 1447972  
* Security bug 1479104  
* Security bug 1471305  
* Security bug 1472365  
* Security bug 1472366  
* Security bug 1472368  
* Security bug 1478470  
* Security bug 1480184  
* Security bug 1486316  

### qtwebview
* [QTBUG-69801](https://bugreports.qt.io/browse/QTBUG-69801) Qml WebView
on Android eats touch events
* [QTBUG-119356](https://bugreports.qt.io/browse/QTBUG-119356)
WebViewSettings QML Type documentation of javaScriptEnabled property has
a spelling mistake

### qtcharts
* [QTBUG-113437](https://bugreports.qt.io/browse/QTBUG-113437) QML
XYSeries bestFitLineColor doc type
* [QTBUG-118322](https://bugreports.qt.io/browse/QTBUG-118322) Fix
licensing of Qt Charts examples
* [QTBUG-114814](https://bugreports.qt.io/browse/QTBUG-114814)
QColorAxis::setVisible method is not behaving as expected.
* [QTBUG-118669](https://bugreports.qt.io/browse/QTBUG-118669) Qt chart
crash on showing context menu

### qtvirtualkeyboard
* [QTBUG-116432](https://bugreports.qt.io/browse/QTBUG-116432) Virtual
keyboard import version number from Qt 5.15 does not work in Qt 6.5
version
* [QTBUG-111873](https://bugreports.qt.io/browse/QTBUG-111873)
qt_attributions.json files should be valid JSON

### qtscxml
* [QTBUG-118050](https://bugreports.qt.io/browse/QTBUG-118050) Empty
script element ends up invoking Q_UNREACHABLE()

### qtnetworkauth
* [QTBUG-117680](https://bugreports.qt.io/browse/QTBUG-117680)
NetworkAuth examples do not show up in Qt Creator

### qtremoteobjects
* [QTBUG-116151](https://bugreports.qt.io/browse/QTBUG-116151) Replica
can crash with QHostAddress being called with a <null reference>

### qtquicktimeline
* [QTBUG-119204](https://bugreports.qt.io/browse/QTBUG-119204) Not
possible to exclude qtquicktimeline from the build

### qtquick3d
* [QTBUG-113164](https://bugreports.qt.io/browse/QTBUG-113164) Crash
when you have two models with same mesh in the scene, one with
BakedLightmap and one without
* [QTBUG-116136](https://bugreports.qt.io/browse/QTBUG-116136) Memory
leaks in Loader qml component
* [QTBUG-117023](https://bugreports.qt.io/browse/QTBUG-117023) Picking
and rotating don't work on bars after clicking buttons
* [QTBUG-118806](https://bugreports.qt.io/browse/QTBUG-118806) Exporting
functionality in the material editor is broken
* [QTBUG-118773](https://bugreports.qt.io/browse/QTBUG-118773) Baking
emissive materials without shadow
* [QTBUG-116911](https://bugreports.qt.io/browse/QTBUG-116911)
tst_surfacetest massive data test crash
* [QTBUG-111873](https://bugreports.qt.io/browse/QTBUG-111873)
qt_attributions.json files should be valid JSON

### qtshadertools
* [QTBUG-117780](https://bugreports.qt.io/browse/QTBUG-117780)
qt_add_shaders is not executed if the target does not exist

### qt5compat
* [QTBUG-117825](https://bugreports.qt.io/browse/QTBUG-117825) [REG
6.6.0 RC->6.6.0] static build on macOS fails, qt5compat(?)

### qtopcua
* [QTBUG-117681](https://bugreports.qt.io/browse/QTBUG-117681) qtopcua
is confused about SSL and OpenSSL

### qtlanguageserver
* [QTBUG-118201](https://bugreports.qt.io/browse/QTBUG-118201) namespace
"std" has no member "exception_ptr"

### qthttpserver
* [QTBUG-114713](https://bugreports.qt.io/browse/QTBUG-114713)
Enhancements in the Color Palette REST API example

### qtquick3dphysics
* [QTBUG-117058](https://bugreports.qt.io/browse/QTBUG-117058) ERROR:
AddressSanitizer: heap-use-after-free in tst_callback

### qtgrpc
* [QTBUG-117066](https://bugreports.qt.io/browse/QTBUG-117066) ERROR:
AddressSanitizer: heap-use-after-free in
QtGrpcClientServerStreamTest::Deadline()

Known Issues
------------

* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-6.5/supported-platforms.html  
  
* The RTA (release test automation) reported issues in Qt 6.5.x:  
https://bugreports.qt.io/issues/?filter=24558  
  
* See Qt 6.5 known issues from:  
https://wiki.qt.io/Qt_6.5_Known_Issues  
  
* Qt 6.5.4 Open issues in Jira:  
https://bugreports.qt.io/issues/?filter=25530  

Credits for the  release goes to:
---------------------------------

Eirik Aavitsland  
Amir Masoud Abdol  
Laszlo Agocs  
Dmitrii Akshintsev  
Dimitrios Apostolou  
Viktor Arvidsson  
Mate Barany  
Vladimir Belyavsky  
Nicholas Bennett  
Eskil Abrahamsen Blomfeldt  
Mikolaj Boc  
Joerg Bornemann  
Rym Bouabid  
Assam Boudjelthia  
Kai Uwe Broulik  
Michael Brüning  
Alex Bu  
Olivier De Cannière  
Mike Chen  
Albert Astals Cid  
Andreas Cord-Landwehr  
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
Julian Greilich  
Jan Grulich  
Kaj Grönholm  
Richard Moe Gustavsen  
Lucie Gérard  
Mikko Hallamaa  
Jøger Hansegård  
Inkamari Harjula  
Jani Heikkinen  
Miikka Heikkinen  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Andreas Holzammer  
Allan Sandfeld Jensen  
Tim Jenssen  
Jonas Karlsson  
Timothée Keller  
Kurt Kiefer  
Friedemann Kleint  
Michal Klocek  
Lars Knoll  
Jarkko Koivikko  
Fabian Kosmale  
Volker Krause  
Mike Krus  
Anton Kudryavtsev  
Konrad Kujawa  
Santhosh Kumar  
Kai Köhne  
Inho Lee  
Paul Lemire  
Wladimir Leuschner  
Lorenzo Lucignano  
Thiago Macieira  
Kuntal Majumder  
Leena Miettinen  
Safiyyah Moosa  
Bartlomiej Moskal  
Marc Mutz  
Antti Määttä  
Martin Negyokru  
Andy Nichols  
Mårten Nordheim  
Dennis Oberst  
Samuli Piippo  
Timur Pocheptsov  
Joni Poikelin  
Rami Potinkara  
Lorn Potter  
MohammadHossein Qanbari  
Liang Qi  
Khem Raj  
Matthias Rauter  
Topi Reinio  
Shawn Rutledge  
Toni Saario  
Ahmad Samir  
Philip Schuchardt  
Sami Shalayel  
Andy Shaw  
Ws ShawnWoo  
Harald Sitter  
Kristoffer Skau  
Ivan Solovev  
Axel Spoerl  
Christian Strømme  
Tarja Sundqvist  
Lars Sutterud  
Tasuku Suzuki  
Jan Arve Sæther  
Morten Sørvig  
Orkun Tokdemir  
Jens Trillmann  
Paul Olav Tvete  
Esa Törmänen  
Peter Varga  
BogDan Vatra  
Doris Verria  
Tor Arne Vestbø  
Jannis Voelker  
Fabian Vogt  
Alexander Volkov  
Ville Voutilainen  
Juha Vuolle  
Jaishree Vyas  
Michael Weghorn  
Edward Welbourne  
Paul Wicking  
Piotr Wierciński  
Jakub Wincenciak  
Semih Yavuz  
