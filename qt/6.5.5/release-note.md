Release note
============
Qt 6.5.5 release is a patch release made on the top of Qt 6.5.4.  
As a patch release, Qt 6.5.5 does not add any new functionality but provides  
bug fixes and other improvements and maintains both forward and backward  
compatibility (source and binary) with Qt 6.5.4.  
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
  
* CVE-2024-25580 in qtbase  
  
### qtbase
* b52817db132 CMake: Recompute features when dependent features are
marked dirty
The build system will now try to recompute configure features when
dependent feature values are toggled by the user.

* 7d942e7c72e CMake: Unify CMAKE_BUILD_TYPE behavior on all platforms
When no explicit build type is specified, Windows will now default to
building Release like the other platforms.

* dd5980a4508 SQLite: Update SQLite to v3.44.2
Updated SQLite to v3.44.2

* 77bcc2ee2eb Fix QStringConverter::encodingForName() for trailing `-`,
`_`
Fixed a bug where encodingForName() failed due to trailing characters
(`_`, `-`) that ought to have been ignored.

* 27c8d61e9da Fix Maximized frameless window painting wrong with
WS_THICKFRAME
Adding a check for the maximized state of the window during the
calculation of margins. Margins calculation will not be skipped for
maximized windows.

* 8e6d961a324 SQLite: Update SQLite to v3.45.0
Updated SQLite to v3.45.0

* 561a2857f99 SQL/MySQL: Fix compilation with MySQL 8.3
Fixed compilation with MySQL 8.3.

* 605d1b3e289 Update Zlib to 1.3.1
zlib was updated to version 1.3.1.

* cc46a478971 Fix clipped text when combining multiple writing systems
Fixed an issue where drawing text from different writing systems in the
same line and including a background could cause parts of the text to be
clipped.

* 13ab0a98677 windows: Avoid infinite recursion with certain fonts
Fixed an issue where an infinite recursion could occur if the system
had a font with multiple preferred names in non-English languages.

* 297b58b0048 Doc: Update Copyright in md4c license text
Updated md4c (optional part of Qt Gui) to version 0.5.1.

* 036f8858044 Update public suffix list
Updated the public suffix list to upstream SHA
883ced078a83f9d79a98933145425c221a5e51f0.

* 40777d28562 QBitArray: avoid overflow in size-to-storage calculations
Fixed a bug with QBitArrays whose size() came within 7 of the
size_type's maximum.

* dce60a765e3 Update bundled libpng to version 1.6.41
libpng was updated to version 1.6.41

* 4053e0557b2 SQLite: Update SQLite to v3.45.1
Updated SQLite to v3.45.1

* 1d9c8a9bf18 Update md4c to 0.5.2
md4c was updated to 0.5.2.

* e11e9ff3427 QMovie non-anim: use QImageReader::imageCount but not
nextImageDelay
QMovie now handles non-animated multi-frame image formats (such as
tiff): QImageIOHandler::imageCount() is observed, and the default frame
rate is 1 FPS.

* 735c4a4ae6d QBitArray: fix potential truncation in QDataStream op>>()
Fixed undetected overflows in the deserialisation (opertor>>()) from
QDataStream.

* acccb5d488e Update bundled libjpeg-turbo to version 3.0.2
libjpeg-turbo was updated to version 3.0.2

* c01cd25c1a0 Update Valgrind to version 3.22.0
Updated Valgrind header used by QtTest. The change only affects
portability of s390 inline assembler.

* 982054d96f2 Update bundled libpng to version 1.6.42
libpng was updated to version 1.6.42

* aebb30748e0 CMake: Fix undefined symbol: qt_resourceFeatureZstd issue
Targets created with qt_add_executable and qt_add_library will now add
the --no-zstd option to AUTORCC_OPTIONS when the target platform does
not support zstd decompression. You can opt out via the
QT_NO_AUTORCC_ZSTD cmake variable.

* 163af9395e2 QBitArray: don't create invalid Qt 5 streams
Now refuses to stream a QBitArray with size() > INT_MAX to a
Qt-5-compatible QDataStream.

* 86f1db45985 Update QLocale and calendar data to CLDR v44.1
Updated QLocale's data extracted from the Unicode Common Locale Data
Repository (CLDR) to v44.1. The license changed to Unicode License V3.

* affc83050b9 QGtk3Theme: Fix QGtk3Interface::fileIcon
Fixed file icons provided by QFileIconProvider when using the gtk3
platform theme.

* 0d8f4f65443 PCRE2: upgrade to 10.43
PCRE2 was updated to version 10.43.

### qtdeclarative
* 06c3f86d29 QML: Let IDs in outer context override bound components'
properties
In QML documents with bound components, IDs defined in outer contexts
override properties defined in inner contexts now. This is how
qmlcachegen has always interpreted bound components when generating C++
code, and it is required to make access to outer IDs actually safe. The
interpreter and JIT have previously preferred inner properties over
outer IDs.

* ec8564963e MessageDialog: Dont rely on accept or reject signal
emissions from QPA
The MessageDialog will now close when a button is pressed, regardless
of the button's role.

* ff0196ec79 CMake: Fix the all_qmllint* targets for VS generators, take
II
When using CMake's Visual Studio project generator, the creation of the
targets all_qmllint, all_qmllint_json and all_qmllint_module requires
now CMake 3.19 or newer. A warning is printed for older CMake versions.
This warning can be disabled by setting QT_NO_QMLLINT_CREATION_WARNING.

* f1a41e5e97 qmlformat: Fix property names with escape chars
qmlformat will no longer add "" characters automatically in the object
keys unless the object key is actually a string literal.

### qtwebengine
* 876f11854 Disable WebEngineContext dump by default
Disabled WebEngineContext dump by default.

* 000f31fb6 Add qWebEngineGetDomainAndRegistry()
Add qWebEngineGetDomainAndRegistry()

* 1aa2a71e3 Add QWebEnginePage::devToolsId()
Add devToolsId property

* 4a26a7b92 RenderWidgetHostViewQtDelegateItem: keep grabs
WebEngineView (or WebView backed by Qt WebEngine) no longer allows
components outside to take over the mouse or touch exclusive grab. For
example if the user starts dragging a scrollbar inside the web view,
that continues until release, regardless of any DragHandler, Flickable
etc.

* 5c442bb23 Fix corrupted load/fetch state on start up in case of
NoCache
Switching profile to NoCache do not longer implicitly removes cache
from old data store.

* 303fb8c69 Merge remote-tracking branch 'origin/6.6' into 6.5
WebEngine now uses the version from Qt 6.6 for the 6.5 branch.


Fixes
-----

### qtbase
* [QTBUG-87332](https://bugreports.qt.io/browse/QTBUG-87332) QDockWidget on Wayland is pretty bad: not redockable,
does not visually move when moving
* [QTBUG-118223](https://bugreports.qt.io/browse/QTBUG-118223) QDockWidget generates leftover containers + crash
* [QTBUG-99136](https://bugreports.qt.io/browse/QTBUG-99136) QDockWidget not correctly parented/setup if dragged from
another floating and tabified QDockWidget
* [QTBUG-118578](https://bugreports.qt.io/browse/QTBUG-118578) Undocking tabbed widget from floating window creates
empty redundant window
* [QTBUG-118579](https://bugreports.qt.io/browse/QTBUG-118579) Undocking tabbed widget from main window onto the
floating window crashes app
* [QTBUG-56799](https://bugreports.qt.io/browse/QTBUG-56799) [QDockWidget - Crash] Double Clicking to re-parent docks
can cause a crash.
* [QTBUG-35736](https://bugreports.qt.io/browse/QTBUG-35736) "Index out of range" situation in QMainWindowLayout class
* [QTBUG-63448](https://bugreports.qt.io/browse/QTBUG-63448) Undocking window does not send topLevelChanged signal
* [QTBUG-88329](https://bugreports.qt.io/browse/QTBUG-88329) Delete a QDockWidget while drag in progress causes crash
* [QTBUG-88157](https://bugreports.qt.io/browse/QTBUG-88157) tabPosition called with out-of-bounds when closing an
undocked QDockWidget
* [QTBUG-94097](https://bugreports.qt.io/browse/QTBUG-94097) creating QDockWidget after application startup prevents
correct termination on Ubuntu
* [QTBUG-44540](https://bugreports.qt.io/browse/QTBUG-44540) QDockAreaLayoutInfo crashes in restoreState (l. 1978-9)
when restoring closed, floating QDockWidget
* [QTBUG-53808](https://bugreports.qt.io/browse/QTBUG-53808) QDockWidget losing decoration on undocking when
GroupedDragging is enabled
* [QTBUG-72915](https://bugreports.qt.io/browse/QTBUG-72915) QDockWidget doesn't properly dock anymore after it was
undocked (regression)
* [QTBUG-53438](https://bugreports.qt.io/browse/QTBUG-53438) QMainWindow: tabbed QDockWidgets leave invisible QTabBar
* [QTBUG-115156](https://bugreports.qt.io/browse/QTBUG-115156) Last character missing with JAWS
* [QTBUG-87334](https://bugreports.qt.io/browse/QTBUG-87334) Graphical issue on some Android smartphones: white line
at the top and the right side of the screen
* [QTBUG-119338](https://bugreports.qt.io/browse/QTBUG-119338) Objective-C usage can result in undefined behavior (part
2)
* [QTBUG-106928](https://bugreports.qt.io/browse/QTBUG-106928) QObject: Cannot create children for a parent that is in
a different thread when exiting Android app
* [QTBUG-118421](https://bugreports.qt.io/browse/QTBUG-118421) TextField logs "Cannot create children for a parent that
is in a different thread" when closing virtual keyboard
* [QTBUG-111528](https://bugreports.qt.io/browse/QTBUG-111528) Android font does not depend on locale/OS preference but
is hardcoded
* [QTBUG-88508](https://bugreports.qt.io/browse/QTBUG-88508) some tests are not saving result output to file on
Android
* [QTBUG-117713](https://bugreports.qt.io/browse/QTBUG-117713) [REG: 5->6] Scaling images with Qt::SmoothTransformation
breaks them if scaled to smaller than 50% size
* [QTBUG-118907](https://bugreports.qt.io/browse/QTBUG-118907) Not correct QDataStream version
* [QTBUG-106479](https://bugreports.qt.io/browse/QTBUG-106479) androidtestrunner does not honour QTEST_FUNCTION_TIMEOUT
* [QTBUG-115298](https://bugreports.qt.io/browse/QTBUG-115298) Androidtestrunner freezes after obtaining SDK version
* [QTBUG-115045](https://bugreports.qt.io/browse/QTBUG-115045) Don't overwrite my CMAKE_<Config>_POSTFIX
* [QTBUG-96936](https://bugreports.qt.io/browse/QTBUG-96936) qt features do not re-evaluate correctly on re-configure
* [QTBUG-85962](https://bugreports.qt.io/browse/QTBUG-85962) Improve FEATURE_foo to QT_FEATURE_foo detection
* [QTBUG-112957](https://bugreports.qt.io/browse/QTBUG-112957) Toplevel developer build fails to link: undefined
symbol: vtable for QNetworkAccessDebugPipeBackendFactory
* [QTBUG-116973](https://bugreports.qt.io/browse/QTBUG-116973) [REG 6.5 -> dev] CMakeList: Can't rebuild after changes
with -no-opengl
* [QTBUG-114958](https://bugreports.qt.io/browse/QTBUG-114958) dev/6.7: Windows: qsb crashes in debug build, causing
qtdeclarative build to fail
* [QTBUG-115730](https://bugreports.qt.io/browse/QTBUG-115730) Qt uses Macros and config files from install tree when
building qtdeclarative "again"
* [QTBUG-119499](https://bugreports.qt.io/browse/QTBUG-119499) Document QMessageAuthenticationCode  using HMAC
* [QTBUG-118568](https://bugreports.qt.io/browse/QTBUG-118568) qvulkanwindow  repeatedly recreate swapchain
* [QTBUG-119366](https://bugreports.qt.io/browse/QTBUG-119366) QTabBar is incorrectly offset when changing the
TabPosition
* [QTBUG-114849](https://bugreports.qt.io/browse/QTBUG-114849) Big icons in QTabWidget are badly aligned (regression
from Qt5 to Qt6)
* [QTBUG-119650](https://bugreports.qt.io/browse/QTBUG-119650) Model adapter/replica incompatible across different Qt
versions and platforms
* [QTBUG-119526](https://bugreports.qt.io/browse/QTBUG-119526) [Reg 6.6.0->6.6.1]QCocoaAccessibility Crash with Mac
VoiceOver enabled
* [QTBUG-118585](https://bugreports.qt.io/browse/QTBUG-118585) "Crash" in QMacAccessibilityElement initWithId:role:
* [QTBUG-118800](https://bugreports.qt.io/browse/QTBUG-118800) Programmatically selecting item view item breaks a11y
focus
* [QTBUG-119797](https://bugreports.qt.io/browse/QTBUG-119797) [Reg 6.5.3 -> 6.6.1]QFileIconProvider.icon of a file
only give general file icon
* [QTBUG-118667](https://bugreports.qt.io/browse/QTBUG-118667) QIcon::addFile() with an invalid filename results in
QFile::isNull() == false
* [QTBUG-120025](https://bugreports.qt.io/browse/QTBUG-120025) The QMainWindowLayout::restoreState causes a crash
* [QTBUG-118642](https://bugreports.qt.io/browse/QTBUG-118642) [Reg6.4->6.5]WebAssembly - QML - failing to use Noto
Color Emoji font
* [QTBUG-119054](https://bugreports.qt.io/browse/QTBUG-119054) Mac: Focus issues when embedding into non-Qt apps
* [QTBUG-49720](https://bugreports.qt.io/browse/QTBUG-49720) Documentation for QFileDialog::DontConfirmOverwrite
should mention QFileDialog::AcceptMode
* [QTBUG-18057](https://bugreports.qt.io/browse/QTBUG-18057) QPixmap::toWinHBITMAP(): 2 Bugs when running out of
memory (Access violation or lost HBITMAP handle)
* [QTBUG-119155](https://bugreports.qt.io/browse/QTBUG-119155) [REG: 6.5.2->6.5.3] headerDataChanged is now queued and
parameters may be out of sync
* [QTBUG-119225](https://bugreports.qt.io/browse/QTBUG-119225) [Reg 6.2 -> 6.5] QSplashScreen no longer shows on Linux
with a single call to QCoreApplication::processEvents()
* [QTBUG-120036](https://bugreports.qt.io/browse/QTBUG-120036) DFEATURE_libjpeg CMake option not working
* [QTBUG-120006](https://bugreports.qt.io/browse/QTBUG-120006) DeleteStartOfWord with a selection in QLineEdit has
unexpected behavior
* [QTBUG-120054](https://bugreports.qt.io/browse/QTBUG-120054) Reg6.4->6.5 Stylesheet has no Effect on QMessageBox
* [QTBUG-117903](https://bugreports.qt.io/browse/QTBUG-117903) WM_CHAR creates unwanted keyboard event - activating
shortcut
* [QTBUG-115765](https://bugreports.qt.io/browse/QTBUG-115765) QAbstractItemView::EditingState: state stale when
editing with a proxy model
* [QTBUG-119902](https://bugreports.qt.io/browse/QTBUG-119902) Crash in QImage::scaled
* [QTBUG-110266](https://bugreports.qt.io/browse/QTBUG-110266) affine example crashes when moving the center hoverpoint
* [QTBUG-112920](https://bugreports.qt.io/browse/QTBUG-112920) FTBFS qt 6.5.0 on gcc 9
* [QTBUG-119752](https://bugreports.qt.io/browse/QTBUG-119752) Customized QToolTip with padding or margin displays
incorrectly
* [QTBUG-119309](https://bugreports.qt.io/browse/QTBUG-119309) Qt fails to flush to Mac native sub window when tlw is
RHI
* [QTBUG-115260](https://bugreports.qt.io/browse/QTBUG-115260) Hang during drag and drop [REG]
* [QTBUG-120055](https://bugreports.qt.io/browse/QTBUG-120055) When dragging QTableView columns scrolling behaves oddly
* [QTBUG-113573](https://bugreports.qt.io/browse/QTBUG-113573) When dragging a header section it will no longer scroll
when at the edge
* [QTBUG-118225](https://bugreports.qt.io/browse/QTBUG-118225) QtQuick Loader doesn't load over http(s)
* [QTBUG-119619](https://bugreports.qt.io/browse/QTBUG-119619) CMake deploy script finds x64 libraries for WoA
application.
* [QTBUG-120121](https://bugreports.qt.io/browse/QTBUG-120121) a11y QComboBox: Problematic signal/slot activation order
* [QTCREATORBUG-30117](https://bugreports.qt.io/browse/QTCREATORBUG-30117) Help viewer: "[read-only]" tags have unreadably
low contrast in dark mode
* [QTBUG-120012](https://bugreports.qt.io/browse/QTBUG-120012) Limiting maximum allocation size for QDataStream
* [QTBUG-119178](https://bugreports.qt.io/browse/QTBUG-119178) Crash after registering an invalid resource file
* [QTBUG-120107](https://bugreports.qt.io/browse/QTBUG-120107) PDF view gets render mistakes on Android 10
* [QTBUG-113865](https://bugreports.qt.io/browse/QTBUG-113865) [Text Editor]Using undo function causes the app to crash
* [QTBUG-119464](https://bugreports.qt.io/browse/QTBUG-119464) QSslSocket::setCiphers() documentation uses weak cyphers
* [QTBUG-120379](https://bugreports.qt.io/browse/QTBUG-120379) The `QStringLiterals` header is lost
* [QTBUG-118161](https://bugreports.qt.io/browse/QTBUG-118161) QFileDialog::getOpenFileContent not working in sometimes
* [QTBUG-101404](https://bugreports.qt.io/browse/QTBUG-101404) wasm: mobile keyboard keeps popping on on android
* [QTBUG-113507](https://bugreports.qt.io/browse/QTBUG-113507) macOS: Popups opening on wrong screen
* [QTBUG-112870](https://bugreports.qt.io/browse/QTBUG-112870) clang-tidy warnings on static global variables in moc
generated code
* [QTBUG-115831](https://bugreports.qt.io/browse/QTBUG-115831) REG 5->6: Setting property placeHolderText on
QPlainTextEdit does not have any effect if the QPlainTextEdit does not
have focus
* [QTBUG-120335](https://bugreports.qt.io/browse/QTBUG-120335) On certain machines QtConcurrent crashes if no free
threads on thread pool
* [QTBUG-120614](https://bugreports.qt.io/browse/QTBUG-120614) QImage::convertToFormat: wrong conversion from RGBA64 to
RGBA16FPx4
* [QTBUG-120297](https://bugreports.qt.io/browse/QTBUG-120297) Q_GADGET forces following elements to be private
* [QTBUG-120572](https://bugreports.qt.io/browse/QTBUG-120572) [QDoc] Redundant text in QTabBar detailed description
* [QTBUG-120758](https://bugreports.qt.io/browse/QTBUG-120758) qtdeclarative fails to build with conan 2 on windows:
include path too long
* [QTBUG-119995](https://bugreports.qt.io/browse/QTBUG-119995) QML - Text - Font weight - macOS/Windows difference
* [QTBUG-119972](https://bugreports.qt.io/browse/QTBUG-119972) Clang-tidy reports possible memory leak with
QMetaObject::invokeMethod
* [QTBUG-119371](https://bugreports.qt.io/browse/QTBUG-119371) [macOS] (File|Folder)Dialog.currentFolder holds stale
data
* [QTBUG-120624](https://bugreports.qt.io/browse/QTBUG-120624) UB when passing null string to QString::arg()
* [QTBUG-120474](https://bugreports.qt.io/browse/QTBUG-120474) 4xMSAA doesn't work with Mali400 using Lima driver
* [QTBUG-117975](https://bugreports.qt.io/browse/QTBUG-117975) Memory leaks when QObject::deleteLater is used without
QApplication runloop
* [QTBUG-58005](https://bugreports.qt.io/browse/QTBUG-58005) ibus: commit does not properly reset the preedit string
* [QTBUG-106653](https://bugreports.qt.io/browse/QTBUG-106653) Crash on Accessibility interface
* [QTBUG-118814](https://bugreports.qt.io/browse/QTBUG-118814) [OpenSSL 3.0] QCryptographicHash::Keccak_256 produces
the same output as Sha3_256
* [QTBUG-121015](https://bugreports.qt.io/browse/QTBUG-121015) tst_QGuiApplication::topLevelAt() failed on Wayland
* [QTBUG-120485](https://bugreports.qt.io/browse/QTBUG-120485) QT_INSTALL_DOCS configured with wrong path
* [QTBUG-120191](https://bugreports.qt.io/browse/QTBUG-120191) Unable to restore visibility state of the QDockWidget
* [QTBUG-120619](https://bugreports.qt.io/browse/QTBUG-120619) QHttpServer with QtConcurrent blocks until the very
first request has finished before being able to process in parallel
* [QTBUG-120961](https://bugreports.qt.io/browse/QTBUG-120961) QLocale::monthName() doesn't work correctly on Windows
* [QTBUG-120577](https://bugreports.qt.io/browse/QTBUG-120577) qt6.5.3 QTextEdit can't display image ! but qt5.15 is ok
。
* [QTBUG-120968](https://bugreports.qt.io/browse/QTBUG-120968) QProcess::start(): Fix docs about Starting state on
Windows
* [QTCREATORBUG-30066](https://bugreports.qt.io/browse/QTCREATORBUG-30066) Git commands fail on windows when using the
QProcess backend
* [QTBUG-121183](https://bugreports.qt.io/browse/QTBUG-121183) [QMYSQL] The mysql_list_fields() was removed in MySQL
v8.3
* [QTBUG-119808](https://bugreports.qt.io/browse/QTBUG-119808) [REG 6.1 -> 6.6] QPlainTextEdit: Placeholder is not
hidden on input
* [QTBUG-120487](https://bugreports.qt.io/browse/QTBUG-120487) Symlinks generated in user_facing_tool_links.txt during
configuration are incorrect for MacOS
* [QTBUG-120509](https://bugreports.qt.io/browse/QTBUG-120509) Crash when Qt re-create native windows if
WA_DontCreateNativeAncestors is set
* [QTBUG-120962](https://bugreports.qt.io/browse/QTBUG-120962) QTextCursor::removeSelectedText leads to crash
* [QTBUG-120436](https://bugreports.qt.io/browse/QTBUG-120436) sqldrivers always build in release
* [QTBUG-114941](https://bugreports.qt.io/browse/QTBUG-114941) Qt 6.6 Beta 1 and Qt Creator 11.0.0-beta2 - Test
permissions - Bluetooth fails on Android 14
* [QTBUG-120317](https://bugreports.qt.io/browse/QTBUG-120317) qt6<target_name>_debug_metatypes.json: illegal value
* [QTBUG-121472](https://bugreports.qt.io/browse/QTBUG-121472) qmltyperegistrar.exe fails to parse metatypes.json file
* [QTBUG-120469](https://bugreports.qt.io/browse/QTBUG-120469) Crash in QCocoaSystemTrayIcon::emitActivated() when
calling QComboBox clear() then addItem()
* [QTBUG-121008](https://bugreports.qt.io/browse/QTBUG-121008) Crash in QMacAccessibilityElement when using
QTreeView/QCombobox
* [QTBUG-121515](https://bugreports.qt.io/browse/QTBUG-121515) [Reg 6.6.1 -> 6.6.2] QNetworkAccessManager never
finishes request if server sends status code 401 without a challenge
* [QTBUG-121040](https://bugreports.qt.io/browse/QTBUG-121040) [Reg 5.1 -> 5.15 and all 6.*] QTextDocumentation does
not handle background of HTML string correctly
* [QTBUG-118238](https://bugreports.qt.io/browse/QTBUG-118238) 【Windows】stack overflow after launch Any Qt Application
(or Official Demo)
* [QTBUG-74471](https://bugreports.qt.io/browse/QTBUG-74471) QFileSystemModel shows directories with
setFilter(QDir::Files)
* [QTBUG-115459](https://bugreports.qt.io/browse/QTBUG-115459) Possible infinite loop triggered by unmaximizing the
window in 6.5.0+
* [QTBUG-121498](https://bugreports.qt.io/browse/QTBUG-121498) tst_QAbstractItemView::removeIndexWhileEditing() failed
on Wayland
* [QTBUG-121713](https://bugreports.qt.io/browse/QTBUG-121713) QXkbCommon::keysymToQtKey does not map XF86Calculator
* [QTBUG-121557](https://bugreports.qt.io/browse/QTBUG-121557) [Reg 6.4.3->6.6] Application unusable after closing
nested message boxes
* [QTBUG-117429](https://bugreports.qt.io/browse/QTBUG-117429) TIFF AnimatedImage memory leak
* [QTBUG-121926](https://bugreports.qt.io/browse/QTBUG-121926) rerun of cmake loses build type
* [QTBUG-121729](https://bugreports.qt.io/browse/QTBUG-121729) error: Multiple commands produce same *_metatypes.json
* [QTBUG-120530](https://bugreports.qt.io/browse/QTBUG-120530) QDomDocument doc refers to QXmlQuery which doesn't exist
in Qt6
* [QTBUG-121697](https://bugreports.qt.io/browse/QTBUG-121697) Critical crash when creating QPlainTextEdit when using
styles/stylesheets.
* [QTBUG-121790](https://bugreports.qt.io/browse/QTBUG-121790) QApplication::setStyleSheet crashes QTextEdit
* [QTBUG-121948](https://bugreports.qt.io/browse/QTBUG-121948) RCC compression is broken when deploying to Android from
a Linux host using CMake
* [QTBUG-106466](https://bugreports.qt.io/browse/QTBUG-106466) build android app with Debian host fails on undefined
symbol qt_resourceFeatureZstd
* [QTBUG-101353](https://bugreports.qt.io/browse/QTBUG-101353) AUTORCC uses zstd even if Qt is build without rcc
support
* [QTBUG-121485](https://bugreports.qt.io/browse/QTBUG-121485) QLocale method nativeCountryName returns wrong values.
* [QTBUG-119148](https://bugreports.qt.io/browse/QTBUG-119148) layer.samples value not clipped in Qt6
* [QTBUG-119795](https://bugreports.qt.io/browse/QTBUG-119795) Adding QOpenGLWidget to a QDialog in a maximized
QMainWindow maximizes the QDialog
* [QTBUG-122200](https://bugreports.qt.io/browse/QTBUG-122200) Header files are not being copied into the Qt*
frameworks in custom build
* [QTBUG-116927](https://bugreports.qt.io/browse/QTBUG-116927) markdown writer omits trailing ** if a bold span exceeds
the wrap limit
* [QTBUG-106526](https://bugreports.qt.io/browse/QTBUG-106526) markdown writer should never wrap headings, but wraps
them if they are too long
* [QTBUG-121881](https://bugreports.qt.io/browse/QTBUG-121881) QT_DEPLOY_QML_DIR: Custom value causes empty "qml"
folder to be created
* [QTBUG-121668](https://bugreports.qt.io/browse/QTBUG-121668) Qt Notifier example - notifications do not work on
Android 13
* [QTBUG-122254](https://bugreports.qt.io/browse/QTBUG-122254) Documentation example of
QCborStreamReader::readString()/QCborStreamReader::readByteArray is
wrong
* [QTBUG-122266](https://bugreports.qt.io/browse/QTBUG-122266) property "AUTORCC_OPTIONS" is not allowed
* [QTBUG-122087](https://bugreports.qt.io/browse/QTBUG-122087) QTimer::isActive returns true if interval is Invalid
* [QTBUG-119864](https://bugreports.qt.io/browse/QTBUG-119864) QPushButton or QToolButton does not receive mouse events
after calling setMenu().
* [QTBUG-119081](https://bugreports.qt.io/browse/QTBUG-119081) QProcessPrivate::waitForDeadChild() doesn't check
forkfd_wait's return code
* [QTBUG-86035](https://bugreports.qt.io/browse/QTBUG-86035) Split QtBuild.cmake into smaller files
* [QTBUG-110369](https://bugreports.qt.io/browse/QTBUG-110369) AUTOUIC can't handle relative paths referring to parent
dirs with Ninja Multi-Config
* [QTBUG-88264](https://bugreports.qt.io/browse/QTBUG-88264) [REG v6.0.0-beta3 -> dev] Top-level configure fails if
told to build tests
* [QTBUG-119490](https://bugreports.qt.io/browse/QTBUG-119490) qcocoaapplicationdelegate.mm:354:20: error: cannot
initialize return object of type 'BOOL'
* [QTBUG-114253](https://bugreports.qt.io/browse/QTBUG-114253) [REG: 5.11->6] Performance issue with loading images in
static build
* [QTBUG-119998](https://bugreports.qt.io/browse/QTBUG-119998) CMake errors out with recursion in latest dev when using
qt-cmake-standalone-test on in-source auto test
* [QTBUG-119077](https://bugreports.qt.io/browse/QTBUG-119077) CMake deployment API does not deploy Qt Webengine
* [QTBUG-119760](https://bugreports.qt.io/browse/QTBUG-119760) Crash when dereferencing a deleted QRhi after native
window is re-created
* [QTBUG-120196](https://bugreports.qt.io/browse/QTBUG-120196) Maximized frameless window painting wrong view region
with Qt::FramelessWindowHint and Windows api WS_THICKFRAME
* [QTBUG-116577](https://bugreports.qt.io/browse/QTBUG-116577) ASSERT: "sumFactors > 0.0"  in qgridlayoutengine.cpp
* [QTBUG-87137](https://bugreports.qt.io/browse/QTBUG-87137) tst_QApplication::sendEventsOnProcessEvents() failed on
Ubuntu 20.04/22.04 and RHEL 9
* [QTBUG-117702](https://bugreports.qt.io/browse/QTBUG-117702) qbittorrent dumped core
* [QTBUG-114583](https://bugreports.qt.io/browse/QTBUG-114583) Headers use things in <iterator> without including it
* [QTBUG-117443](https://bugreports.qt.io/browse/QTBUG-117443) Two Android executables mix their build artifacts if
targets are added in a single CMakeLists.txt
* [QTBUG-118829](https://bugreports.qt.io/browse/QTBUG-118829) androiddeployqt with --release includes various
qmltooling libs
* [QTBUG-120460](https://bugreports.qt.io/browse/QTBUG-120460) tst_QHostInfo::reverseLookup() fails on qemu and blocks
CI
* [QTBUG-118489](https://bugreports.qt.io/browse/QTBUG-118489) Can't tab to last button in QDialogButtonBox
* [QTBUG-117910](https://bugreports.qt.io/browse/QTBUG-117910) [windeployqt] The QtPDF module will always be deployed
if it's installed
* [QTBUG-116763](https://bugreports.qt.io/browse/QTBUG-116763) out-of-bounds operator+
* [QTBUG-113498](https://bugreports.qt.io/browse/QTBUG-113498) QVideoWidget in QDialog does not show / crashes (macOS)
when shown twice
* [QTBUG-109877](https://bugreports.qt.io/browse/QTBUG-109877) macOS: QFileDialog::getSaveFileName() truncates a
compound extension
* [QTBUG-119601](https://bugreports.qt.io/browse/QTBUG-119601) iOS: Sometimes soft keyboard can't be closed
* [QTBUG-101141](https://bugreports.qt.io/browse/QTBUG-101141) moc: namespaced base class not properly resolved in
cpp.json file
* [QTBUG-120602](https://bugreports.qt.io/browse/QTBUG-120602) Cannot build Qt modules standalone for iOS
* [QTBUG-120682](https://bugreports.qt.io/browse/QTBUG-120682) Creating QSslSocket when schannel is in use takes too
long time
* [QTBUG-52021](https://bugreports.qt.io/browse/QTBUG-52021) Blink timer for QLineEdit not killed after QMenu spawn
* [QTBUG-94460](https://bugreports.qt.io/browse/QTBUG-94460) QLocale's names for languages, scripts and territories
don't match CLDR's en.xml's proper names
* [QTBUG-122042](https://bugreports.qt.io/browse/QTBUG-122042) Shortcut icons for the delete and backspace keys seem to
be wrong
* [QDS-11733](https://bugreports.qt.io/browse/QDS-11733) Delete icon points in wrong direction on macOS
* [QTBUG-118318](https://bugreports.qt.io/browse/QTBUG-118318) QStringConverter/Win doesn't handle resumption for
encodings with more than 2 octets per character for convertToUnicode

### qtdeclarative
* [QTBUG-119160](https://bugreports.qt.io/browse/QTBUG-119160) Graphics corruption when toggling depth-aware rendering
* [QTBUG-119005](https://bugreports.qt.io/browse/QTBUG-119005) QML FileDialog file size overflow
* [QTBUG-119165](https://bugreports.qt.io/browse/QTBUG-119165) qmlsc: QUrl does not compile in console.log()
* [QTBUG-115710](https://bugreports.qt.io/browse/QTBUG-115710) [Windows and WSL2] QML module that only contains C++
code breaks `all_qmllint` target
* [QTBUG-119147](https://bugreports.qt.io/browse/QTBUG-119147) Invalid input not handled in Qt Quick Controls - Contact
List example
* [QTBUG-112673](https://bugreports.qt.io/browse/QTBUG-112673) Drag.imageSource example - no image on first drag
* [QTBUG-115491](https://bugreports.qt.io/browse/QTBUG-115491) Drag.imageSource Only Works On Second try
* [QTBUG-119451](https://bugreports.qt.io/browse/QTBUG-119451) the document is incorrect about the data type in the
code snippet
* [QTBUG-118902](https://bugreports.qt.io/browse/QTBUG-118902) Qmltyperegistrar doesn't escape "-" in "#ifdef"
generated code
* [QTBUG-119298](https://bugreports.qt.io/browse/QTBUG-119298) [macOS] Using Imagine style controls provokes Qt warning
* [QTBUG-119162](https://bugreports.qt.io/browse/QTBUG-119162) Qml: Behaviour differs between interpreted/compiled code
* [QTBUG-119838](https://bugreports.qt.io/browse/QTBUG-119838) [REG] qt_add_qml_module broken for the VS generator when
called in different subdirectories
* [QTBUG-115166](https://bugreports.qt.io/browse/QTBUG-115166) qt_add_qml_module() causes non-Ninja generators to think
that projects are never up-to-date
* [QTBUG-115121](https://bugreports.qt.io/browse/QTBUG-115121) PathView can be clicked through if it is flicking and
delegate has MouseArea
* [QTBUG-117948](https://bugreports.qt.io/browse/QTBUG-117948) qt_generate_deploy_qml_app_script() deploys QML plugin
target but not the corresponding backing target
* [QTBUG-119084](https://bugreports.qt.io/browse/QTBUG-119084) Connections type doesn't work in qmltc'ed app
* [QTBUG-118445](https://bugreports.qt.io/browse/QTBUG-118445) Native macOS MessageDialog doesn't reopen
* [QTBUG-118212](https://bugreports.qt.io/browse/QTBUG-118212) [Reg 5.15->6.x][Android] MessageDialog's standard
buttons do not accept/reject the dialog
* [QTBUG-120005](https://bugreports.qt.io/browse/QTBUG-120005) Native TextArea: placeholderText does not respect
horizontalAlignment
* [QTBUG-105080](https://bugreports.qt.io/browse/QTBUG-105080) FileDialog ignores fileMode : FileDialog.Save
* [QTBUG-109488](https://bugreports.qt.io/browse/QTBUG-109488) tst_qquicktextedit::largeTextObservesViewport fails / is
flaky
* [QTBUG-119395](https://bugreports.qt.io/browse/QTBUG-119395) crash on QML property bindings
* [QTBUG-119675](https://bugreports.qt.io/browse/QTBUG-119675) [qmllint ] Enabling the qmllint for a lot of QML files
exceeds the command line limitation on Windows host
* [QTBUG-108807](https://bugreports.qt.io/browse/QTBUG-108807) QQC2 TabBar first TabButton visual state incorrect when
deselected
* [QTBUG-117387](https://bugreports.qt.io/browse/QTBUG-117387) TapHandler and DragHandler interoperability breaks
* [QTBUG-66360](https://bugreports.qt.io/browse/QTBUG-66360) PointHandler goes inactive releasing mouse button when
multiple pressed
* [QTBUG-83980](https://bugreports.qt.io/browse/QTBUG-83980) HoverHandler: sometimes point.position returns (0, 0)
* [QTBUG-119363](https://bugreports.qt.io/browse/QTBUG-119363) UniformAnimator makes app crash when being destroyed by
other component
* [QTBUG-119793](https://bugreports.qt.io/browse/QTBUG-119793) QML Button (Material 3) contents truncated
* [QTBUG-119794](https://bugreports.qt.io/browse/QTBUG-119794) QJSValue: url does not convert to QUrl
* [QTBUG-119715](https://bugreports.qt.io/browse/QTBUG-119715) REG: ScrollView content size broken
* [QTBUG-119963](https://bugreports.qt.io/browse/QTBUG-119963) [Reg 6.5.1->6.5.3] QJSEngine no longer converts new'ed
JS object to QVariantMap
* [QTBUG-119916](https://bugreports.qt.io/browse/QTBUG-119916) Non-native FileDialog does not prompt about overwriting
an existing file
* [QTBUG-120349](https://bugreports.qt.io/browse/QTBUG-120349) Window Qml Type doc is missing the default visible
property value
* [QTBUG-116306](https://bugreports.qt.io/browse/QTBUG-116306) Mention indeterminate state for Qt Quick Controls 2
ProgressBar customization
* [QTBUG-120346](https://bugreports.qt.io/browse/QTBUG-120346)  hovered property of HoverHandler stays true when
sliding by touch outside of hover area
* [QTBUG-117899](https://bugreports.qt.io/browse/QTBUG-117899) [REG 6.4->6.5] Binding Loops -> Wrong layout because of
interruption
* [QTBUG-118511](https://bugreports.qt.io/browse/QTBUG-118511) Binding loop if ColumnLayout implicitWidth is changed
* [QTBUG-120296](https://bugreports.qt.io/browse/QTBUG-120296) Qt Quick Widgets Example  -  Grab Framebuffer is
susceptible to crash
* [QTBUG-119917](https://bugreports.qt.io/browse/QTBUG-119917) Non-native FileDialog loses current filename when
changing folders
* [QTBUG-120052](https://bugreports.qt.io/browse/QTBUG-120052) TextArea/TextField: placeholderText does not respect
horizontalAlignment after the component creation
* [QTBUG-119646](https://bugreports.qt.io/browse/QTBUG-119646) [Tests] Warnings in
qtdeclarative/tests/auto/quickcontrols/controls/data/tst_textfield.qml
* [QTBUG-119372](https://bugreports.qt.io/browse/QTBUG-119372) build fails with Q_IMPORT_QML_PLUGIN macro
* [QTBUG-119645](https://bugreports.qt.io/browse/QTBUG-119645) [Tests] Warnings in
qtdeclarative/tests/auto/quickcontrols/controls/data/tst_textarea.qml
* [QTBUG-99231](https://bugreports.qt.io/browse/QTBUG-99231) "Could not set initial property horizontalAlignment" when
trying to set resettable property
* [QTBUG-119760](https://bugreports.qt.io/browse/QTBUG-119760) Crash when dereferencing a deleted QRhi after native
window is re-created
* [QTBUG-119992](https://bugreports.qt.io/browse/QTBUG-119992) qt5 code is used for the qt6.6 documentation
* [QTBUG-121206](https://bugreports.qt.io/browse/QTBUG-121206) NO_LINT has not effect in qt_add_qml_module
* [QTBUG-121139](https://bugreports.qt.io/browse/QTBUG-121139) qmlcachegen locks up in some situations
* [QTBUG-113558](https://bugreports.qt.io/browse/QTBUG-113558) QQuickWidget does not handle touch event via QML
TapHandler correctly
* [QTBUG-120479](https://bugreports.qt.io/browse/QTBUG-120479) qmldir file not placed with library with CMake Xcode
generator
* [QTBUG-120568](https://bugreports.qt.io/browse/QTBUG-120568) "Using the Configuration File in a Project" only covers
qmake way and not cmake
* [QTBUG-119994](https://bugreports.qt.io/browse/QTBUG-119994) the documentation seems to be contradictory to the code
snippet
* [QTBUG-119903](https://bugreports.qt.io/browse/QTBUG-119903) the link to elevated card cannot be found
* [QTBUG-120065](https://bugreports.qt.io/browse/QTBUG-120065) Non-native FileDialog loses URL schema when filename is
manually entered
* [QTBUG-115953](https://bugreports.qt.io/browse/QTBUG-115953) Interactive Flickable with pressDelay makes
childMouseEventFilter to lose MouseButtonPress event
* [QTBUG-120450](https://bugreports.qt.io/browse/QTBUG-120450) Allocating or deallocating a QJSEngine object causes a
crash if the application has called mlockall(MCL_CURRENT|MCL_FUTURE)
* [QTBUG-116426](https://bugreports.qt.io/browse/QTBUG-116426) crash in QQuickItemPrivate::derefWindow
* [QTBUG-111729](https://bugreports.qt.io/browse/QTBUG-111729) Assertion failed in QJSEngine when repeatedly deleting &
adding property getters on an object
* [QTBUG-113695](https://bugreports.qt.io/browse/QTBUG-113695) qmllint: property-changes-parsed suggests can code that
don't understand
* [QTBUG-120301](https://bugreports.qt.io/browse/QTBUG-120301) QQuickStateGroup taking null pointers leads to crash
* [QTBUG-118710](https://bugreports.qt.io/browse/QTBUG-118710) [REG 6.5.2 → 6.5.3] QQmlProperty: wrong warning about
signal handler capitalization
* [QTBUG-119326](https://bugreports.qt.io/browse/QTBUG-119326) application crash when using QML-Debugger: Component vs
.qml
* [QTBUG-120512](https://bugreports.qt.io/browse/QTBUG-120512) Inconsistent behaviour between qmlsc and JIT compiler
when setting a property to "undefined"
* [QTBUG-121710](https://bugreports.qt.io/browse/QTBUG-121710) [Reg 6.6.0 -> 6.6.1] Aliasing to enums does not work as
in Qt 6.6.0 an earlier anymore
* [QTBUG-119984](https://bugreports.qt.io/browse/QTBUG-119984) old way of exposing c++ class to qml is written
* [QTBUG-109261](https://bugreports.qt.io/browse/QTBUG-109261) qmlsc dead code analysis is incomplete
* [QTBUG-113776](https://bugreports.qt.io/browse/QTBUG-113776) qmlformat fails to format if there is a escape char in
the key string
* [QTBUG-119459](https://bugreports.qt.io/browse/QTBUG-119459) [Reg 5.15 -> 6.2] the line number output by
console.trace() is too big
* [QTBUG-122081](https://bugreports.qt.io/browse/QTBUG-122081) FAIL!  : tst_qqmllocale::toString(locale.toString(new
Date(2000, 1, 1))) Compared values are not the same
* [QTBUG-122173](https://bugreports.qt.io/browse/QTBUG-122173) tst_qquickanimatedimage::currentFrame() is flaky on
windows
* [QTBUG-120105](https://bugreports.qt.io/browse/QTBUG-120105) Unreliable QML Timer / qmltest wait() / QTest:qWait()
with offscreen platform
* [QTBUG-122106](https://bugreports.qt.io/browse/QTBUG-122106) QList<int> is converted to int by qmlsc
* [QTBUG-114718](https://bugreports.qt.io/browse/QTBUG-114718) [Tests] tst_QQuickPopup fails
* [QTBUG-118163](https://bugreports.qt.io/browse/QTBUG-118163) Flaky race-condition in QuickTest when running
tst_inputpanel built with ASAN
* [QTBUG-111873](https://bugreports.qt.io/browse/QTBUG-111873) qt_attributions.json files should be valid JSON
* [QTBUG-115536](https://bugreports.qt.io/browse/QTBUG-115536) Setting Window.contentOrientation breaks Popup on
regular desktop
* [QTBUG-108808](https://bugreports.qt.io/browse/QTBUG-108808) QQC2 BusyIndicator does not inherit visibility from
parent consistently
* [QTBUG-120356](https://bugreports.qt.io/browse/QTBUG-120356) padding not applied to header and footer for
QuickControls.Dialog
* [QTBUG-117654](https://bugreports.qt.io/browse/QTBUG-117654) TextArea multi-line placeholder text overlaps the
TextEdit area
* [QTBUG-117667](https://bugreports.qt.io/browse/QTBUG-117667) REG: TextEdit height gets stuck due to binding loops
(forever) or anchor changes (temporarily until further resize event)
* [QTBUG-25489](https://bugreports.qt.io/browse/QTBUG-25489) QtQuick2 TextEdit emits unnecessary
cursorRectangleChanged on all kinds of modifications
* [QTBUG-122256](https://bugreports.qt.io/browse/QTBUG-122256) Crash on
QQuickMultiEffectPrivate::updateBlurItemsAmount() with nullptr access

### qtmultimedia
* [QTBUG-118777](https://bugreports.qt.io/browse/QTBUG-118777) Emulation layer crash / cannot run project after adding
two Audio Listeners
* [QTBUG-118309](https://bugreports.qt.io/browse/QTBUG-118309) QML Camera - Zoom not observed in Preview
* [QTBUG-116324](https://bugreports.qt.io/browse/QTBUG-116324) Request to implement thumbnail realization for
multimedia FFMPEG backend
* [QTBUG-119089](https://bugreports.qt.io/browse/QTBUG-119089) QML Camera crashing on some devices
* [QTBUG-119445](https://bugreports.qt.io/browse/QTBUG-119445) Camera crash on image acquire on Android
* [QTBUG-117099](https://bugreports.qt.io/browse/QTBUG-117099) Video jerks when playing (Windows backend)
* [QTBUG-118734](https://bugreports.qt.io/browse/QTBUG-118734) Attribution scanner can not refer to files downloaded
during provisioning
* [QTBUG-119471](https://bugreports.qt.io/browse/QTBUG-119471) Camera usage randomly crashes when the camera surface is
destroyed with android backend
* [QTBUG-119236](https://bugreports.qt.io/browse/QTBUG-119236) Unexpected value for QML Camera.error enum
* [QTBUG-119693](https://bugreports.qt.io/browse/QTBUG-119693) [REG] 6.7.0 namespace build fails on Windows
(MSVC&MinGW), multimedia
* [QTBUG-118839](https://bugreports.qt.io/browse/QTBUG-118839) [DeclarativeCamera] The app crashes when unlocking the
screen on Android
* [QTBUG-118573](https://bugreports.qt.io/browse/QTBUG-118573) Android tests on CI part 3/3 (screen/window capture)
* [QTBUG-118127](https://bugreports.qt.io/browse/QTBUG-118127) QMediaPlayer can not play sound again after the sound
finished.
* [QTBUG-116519](https://bugreports.qt.io/browse/QTBUG-116519) [Reg 6.2 -> 6.5] Repeated QSoundEffect is broken on
PulseAudio
* [QTBUG-113616](https://bugreports.qt.io/browse/QTBUG-113616) Android: Crash when mapping QVideoFrame object
(minimize/restore)
* [QTBUG-113498](https://bugreports.qt.io/browse/QTBUG-113498) QVideoWidget in QDialog does not show / crashes (macOS)
when shown twice
* [QTBUG-118593](https://bugreports.qt.io/browse/QTBUG-118593) QML Camera ImageCapture Parameter not declared
* [QTBUG-118572](https://bugreports.qt.io/browse/QTBUG-118572) Android tests on CI part 2/3 (audio)
* [QTBUG-118587](https://bugreports.qt.io/browse/QTBUG-118587) [WMF] Video position may exceed it's duration
* [QTBUG-120198](https://bugreports.qt.io/browse/QTBUG-120198) Process abruptly terminates while executing static
destructor in Qt6Multimedia.dll
* [QTBUG-121455](https://bugreports.qt.io/browse/QTBUG-121455) QtMultimedia module fails Yocto CI build
* [QTBUG-121200](https://bugreports.qt.io/browse/QTBUG-121200) QML Video Recorder - Missing Text in Buttons on Android
* [QTBUG-121495](https://bugreports.qt.io/browse/QTBUG-121495) COM is uninitialized too many times with FFmpeg and
QWindowsResampler
* [QTBUG-121187](https://bugreports.qt.io/browse/QTBUG-121187)  Spectrum App Crashes after recording sound in "Record
and Playback" Mode
* [QTBUG-119737](https://bugreports.qt.io/browse/QTBUG-119737) MediaRecorder.isAvailable not defined
* [QTBUG-120465](https://bugreports.qt.io/browse/QTBUG-120465) QML Camera unloading crash on iOS
* [QTBUG-114900](https://bugreports.qt.io/browse/QTBUG-114900) alsa backend causes warning messages
* [QTBUG-119746](https://bugreports.qt.io/browse/QTBUG-119746) Audio recording volume extremely low
* [QTBUG-122053](https://bugreports.qt.io/browse/QTBUG-122053) Qt continues to occupy the microphone unless you call
QMediaCaptureSession::setAudioInput() with a null pointer after
recording is complete
* [QTBUG-120026](https://bugreports.qt.io/browse/QTBUG-120026) Retrieving videoDevices blocks main event loop
* [QTBUG-122096](https://bugreports.qt.io/browse/QTBUG-122096) Wrong colors are displayed when playing videos with IMC2
color format
* [QTBUG-118668](https://bugreports.qt.io/browse/QTBUG-118668) QTextToSpeech::synthesize under window does not get data
* [QTBUG-118571](https://bugreports.qt.io/browse/QTBUG-118571) Android tests on CI part 1/3 (camera & media
capture/player)
* [QTBUG-117746](https://bugreports.qt.io/browse/QTBUG-117746) eglfs: Capturing the screen crashes
* [QTBUG-117878](https://bugreports.qt.io/browse/QTBUG-117878) Cannot capture screen from QQuickWidget
* [QTBUG-111045](https://bugreports.qt.io/browse/QTBUG-111045) QSoundEffect not playing
* [QTBUG-118099](https://bugreports.qt.io/browse/QTBUG-118099) Volume Discrepancies Between QMediaPlayer and
QSoundEffect with ffmpeg
* [QTBUG-111815](https://bugreports.qt.io/browse/QTBUG-111815) Bumpy rendering of D3D11 textures
* [QTBUG-111459](https://bugreports.qt.io/browse/QTBUG-111459) Heavy jittering in video playback if animations are
active
* [QTBUG-109213](https://bugreports.qt.io/browse/QTBUG-109213) Video flickering when there is a ParticleSystem
component or playing some animation at same time

### qttools
* [QTBUG-118808](https://bugreports.qt.io/browse/QTBUG-118808) qt_add_translations with source autodetection mishandles
id-based generated UI headers
* [QTBUG-121226](https://bugreports.qt.io/browse/QTBUG-121226) qdoc extraimages.HTML not supported
* [QTBUG-121850](https://bugreports.qt.io/browse/QTBUG-121850) QDoc: SHA1-files generated for QHP files differ across
platforms

### qtdoc
* [QTBUG-117647](https://bugreports.qt.io/browse/QTBUG-117647) Audio track is not played when opening audio file after
playing video file in media player example
* [QTBUG-117090](https://bugreports.qt.io/browse/QTBUG-117090) CMake docs: incorrect code example for
qt_generate_qml_app_script
* [QTBUG-120372](https://bugreports.qt.io/browse/QTBUG-120372) Typo in the document
* [QTBUG-121165](https://bugreports.qt.io/browse/QTBUG-121165) Error in WebAssembly documentation
* [QTBUG-115373](https://bugreports.qt.io/browse/QTBUG-115373) Hangman Demo uses unsupported version of Google Play
Billing Library
* [QTBUG-120014](https://bugreports.qt.io/browse/QTBUG-120014) Dependency for libxcb-cursor0 since Qt 6.5 is not
mentioned in the documentation.

### qtconnectivity
* [QTBUG-119063](https://bugreports.qt.io/browse/QTBUG-119063) Segfault in Bluetooth module's Windows COM de-init
* [QTBUG-119060](https://bugreports.qt.io/browse/QTBUG-119060) Read access violation when calling stop() during
Bluetooth service discovery
* [QTBUG-120410](https://bugreports.qt.io/browse/QTBUG-120410) NDEF Editor Example - Clicking on 'read tag' will erase
existing records

### qtwayland
* [QTBUG-118612](https://bugreports.qt.io/browse/QTBUG-118612) Large size cursor overlaps tooltips on linux
* [QTBUG-118890](https://bugreports.qt.io/browse/QTBUG-118890) QWaylandWindow::reset() mutex race/deadlock with
QWaylandWindow::beginFrame()
* [QTBUG-120392](https://bugreports.qt.io/browse/QTBUG-120392) QWayland CSD window has unclickable area
* [QTBUG-120397](https://bugreports.qt.io/browse/QTBUG-120397) "output" property seems to be missing in
WaylandQuickItem QML type documentation
* [QTBUG-120477](https://bugreports.qt.io/browse/QTBUG-120477) Overriding swap interval for Wayland EGL windows doesn't
work
* [QTBUG-117932](https://bugreports.qt.io/browse/QTBUG-117932) Crash in texture orphanage
* [QTBUG-116600](https://bugreports.qt.io/browse/QTBUG-116600) The Virtual keyboard is not hidden when the TextField
loses focus on the Wayland client.

### qt3d
* [QTBUG-69463](https://bugreports.qt.io/browse/QTBUG-69463) Camera view matrix computation unstable (regression)

### qtserialbus
* [QTBUG-114397](https://bugreports.qt.io/browse/QTBUG-114397) QCanDbcFileParser will not parse signals with certain
valid utf-8 encoded characters

### qtwebengine
* [QTBUG-100417](https://bugreports.qt.io/browse/QTBUG-100417) [REG 5.15->6.3] Multiple context menus can be opened
with synthetic touch events
* [QTBUG-109357](https://bugreports.qt.io/browse/QTBUG-109357) [REG 5.12 -> 5.15/6.x] QWebEngineUrlRequestInterceptor:
Multiple redirects crashes the application
* [QTBUG-109243](https://bugreports.qt.io/browse/QTBUG-109243) [REG: 5->6] MouseArea under WebEngineView is getting
emitting entered/exited signals even though mouse does not enter or
leave it
* [QTBUG-109348](https://bugreports.qt.io/browse/QTBUG-109348) QtWebEngineView doesn't scroll word document
* [QTBUG-109040](https://bugreports.qt.io/browse/QTBUG-109040) QWebEngineView always prints context
* [QTBUG-110272](https://bugreports.qt.io/browse/QTBUG-110272) webengine tries to use DRI on embedded builds
* [QTBUG-110873](https://bugreports.qt.io/browse/QTBUG-110873) error: ‘QtWebEngineProcess’ was not declared in this
scope; did you mean ‘QtWebEngineCore’?
* [QTWEBSITE-1083](https://bugreports.qt.io/browse/QTWEBSITE-1083) Possible JS error in WebEngine Markdown Editor Example
* [QTBUG-104869](https://bugreports.qt.io/browse/QTBUG-104869) QWebEngineDownloadItem::totalBytes() always returns -1
* [QTBUG-111574](https://bugreports.qt.io/browse/QTBUG-111574) documentation is wrong for WebEngineCertificateError
* [QTBUG-106072](https://bugreports.qt.io/browse/QTBUG-106072) QtPdf can't open password-protected PDF files on
Windows/Android
* [QTBUG-111585](https://bugreports.qt.io/browse/QTBUG-111585) REG: GL Errors with WebGL on macOS 13
* [QTBUG-111784](https://bugreports.qt.io/browse/QTBUG-111784) Regression: macOS: Some video do not show pictures after
WebGL fix
* [QTBUG-106359](https://bugreports.qt.io/browse/QTBUG-106359) QtPDF multipage example should switch to search result
tab during searching
* [QTBUG-112007](https://bugreports.qt.io/browse/QTBUG-112007) Qt WebEngine 3rd party licensing documentation is
generated but hidden
* [QTBUG-87275](https://bugreports.qt.io/browse/QTBUG-87275) Incorrect parsing of local urls in qml
* [QTBUG-111939](https://bugreports.qt.io/browse/QTBUG-111939) Dependency update on qt/qtwebengine failed in 6.5.0
* [QTBUG-88482](https://bugreports.qt.io/browse/QTBUG-88482) License terms are missing for Qtpdf
* [QTBUG-111958](https://bugreports.qt.io/browse/QTBUG-111958) opus detection in QtWebEngine still needs perl
* [QTBUG-112282](https://bugreports.qt.io/browse/QTBUG-112282) Support Metal RHI
* [QTBUG-112280](https://bugreports.qt.io/browse/QTBUG-112280) Support Metal and D3D RHI backends
* [QTBUG-111067](https://bugreports.qt.io/browse/QTBUG-111067) Qt PDF Multipage example is crashing on desktop when
loading pdf files
* [QTBUG-112772](https://bugreports.qt.io/browse/QTBUG-112772) Developer tools open with "screencast" enabled (again)
* [QTBUG-109401](https://bugreports.qt.io/browse/QTBUG-109401) Add DirectX support to QWebEngine
* [QTBUG-111909](https://bugreports.qt.io/browse/QTBUG-111909) QWebEngineView::print margin issues
* [QTBUG-112614](https://bugreports.qt.io/browse/QTBUG-112614) QPdfPageNavigator::backAvailableChanged and
forwardAvailableChanged are not always emitted for jumps
* [QTBUG-111697](https://bugreports.qt.io/browse/QTBUG-111697) Build failure with GCC 13
* [QTBUG-112700](https://bugreports.qt.io/browse/QTBUG-112700) [REG] [macOS] Using getUserMedia() opens new window's
tab in Dock
* [QTBUG-113109](https://bugreports.qt.io/browse/QTBUG-113109) [REG 6.4 -> 6.5] WebEngineScripts don't always run on
pages containing iframes
* [QTBUG-113035](https://bugreports.qt.io/browse/QTBUG-113035) Under the current conditions specified in the
documentation, it is not possible to build the module through cross-
compilation
* [QTBUG-113350](https://bugreports.qt.io/browse/QTBUG-113350) FAIL!  :
tst_QWebEngineGlobalSettings::dnsOverHttps(DnsMode::Secure (real DNS))
'loadSpy.wait()' returned FALSE
* [QTBUG-112645](https://bugreports.qt.io/browse/QTBUG-112645) QWebEnginePage::WebWindowType not covered by tests
* [QTBUG-112483](https://bugreports.qt.io/browse/QTBUG-112483) Custom scheme handler can not handle content-type with
value  "text/html ;charset=utf-8"
* [QTBUG-67716](https://bugreports.qt.io/browse/QTBUG-67716) Weird animation on WebView (WebEngine) on macOS when
dragging pass boundaries
* [QTBUG-112466](https://bugreports.qt.io/browse/QTBUG-112466) libQt6Pdf.so is always built with an embedded copy of
libpng
* [QTBUG-113400](https://bugreports.qt.io/browse/QTBUG-113400) If QWebEngineProcess is terminated and a JavaScript is
being run that leads to crash
* [QTBUG-113270](https://bugreports.qt.io/browse/QTBUG-113270) Improve docs with details about the use of GPL
components from Chromium
* [QTBUG-113524](https://bugreports.qt.io/browse/QTBUG-113524) WebEngine cannot use https after using -sign-for-
notarization
* [QTBUG-113802](https://bugreports.qt.io/browse/QTBUG-113802) CrossBuilding QtPdf fails because of wrong path to
qt.toolchain.cmake
* [QTBUG-113579](https://bugreports.qt.io/browse/QTBUG-113579) Clipboard write action doesn't work on 6.5.0
* [QTBUG-114045](https://bugreports.qt.io/browse/QTBUG-114045) error: expected constructor, destructor, or type
conversion before ‘(’ token QT_FORWARD_DECLARE_CLASS(QThread)
* [QTBUG-113859](https://bugreports.qt.io/browse/QTBUG-113859) [REG 6.4->6.5] Accessibility crash when clicking on a
link in a list on macOS
* [QTBUG-113806](https://bugreports.qt.io/browse/QTBUG-113806) Chromium attributions missing from 'Licences used in Qt'
docs
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
* [QTBUG-114875](https://bugreports.qt.io/browse/QTBUG-114875) Cannot detect Visual Studio when configuring QPdf and
QWebEngine
* [QTBUG-115690](https://bugreports.qt.io/browse/QTBUG-115690)  FAILED:
qtwebengine/src/core/api/chromium_attributions.qdoc
* [QTBUG-115369](https://bugreports.qt.io/browse/QTBUG-115369) QWebEngine can not render page content and throw `Fatal
error` in console
* [QTBUG-115713](https://bugreports.qt.io/browse/QTBUG-115713) [REG 6.6.0 beta2->beta3] QtPDF and QtWebengine not
compiling from sources on MSVC2019
* [QTBUG-115476](https://bugreports.qt.io/browse/QTBUG-115476) QPdfPageSelector doesn't actually handle non-numeric
page label input
* [QTBUG-115365](https://bugreports.qt.io/browse/QTBUG-115365) QWebEngineCertificateError is exported twice
* [QTBUG-99555](https://bugreports.qt.io/browse/QTBUG-99555) [RE: 6.2.1->6.2.2] macdeployqt fails to produce
notarizable packages
* [QTBUG-115844](https://bugreports.qt.io/browse/QTBUG-115844) qtwebengine ignores some key remaps
* [QTBUG-115976](https://bugreports.qt.io/browse/QTBUG-115976) Dev tools not hidden with closing cross
* [QTBUG-115703](https://bugreports.qt.io/browse/QTBUG-115703) QtWebEngine 6.6.0 crashes on Windows
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
* [QTBUG-115994](https://bugreports.qt.io/browse/QTBUG-115994) Duplicate character when long-pressing for accented char
on macOS/webengine
* [QTBUG-115753](https://bugreports.qt.io/browse/QTBUG-115753) ERROR: AddressSanitizer: heap-use-after-free  in
tst_origins
* [QTBUG-116445](https://bugreports.qt.io/browse/QTBUG-116445) [REG][Windows] Crash on
NativeSkiaOutputDevice::releaseTexture() with nullptr access
* [QTBUG-117119](https://bugreports.qt.io/browse/QTBUG-117119) Some Qt WebEngine documentation issues
* [QTBUG-117489](https://bugreports.qt.io/browse/QTBUG-117489) [REG 6.4 -> 6.5] Invalid QDataStream data when
serializing uninited QWebEngineHistory
* [QTBUG-118505](https://bugreports.qt.io/browse/QTBUG-118505) REG: Qt WebEngine debug-and-release builds broken on
macOS.
* [QTBUG-118157](https://bugreports.qt.io/browse/QTBUG-118157) [REG 6.5 -> 6.6] Crash in
`GetServiceWorkerExtendedLifetimeOrigins` on Google Meet
* [QTBUG-85731](https://bugreports.qt.io/browse/QTBUG-85731) Screen sharing does not work on Google Meet
* [QTBUG-117751](https://bugreports.qt.io/browse/QTBUG-117751) building with -no-opengl produces errors in
web_engine_context.cpp
* [QTBUG-117867](https://bugreports.qt.io/browse/QTBUG-117867) QWebEngineNewWindowRequest::openIn() breaks page
interceptor
* [QTBUG-118455](https://bugreports.qt.io/browse/QTBUG-118455) Crash in Compositor::Observer::compositor() with nullptr
access
* [QTBUG-117741](https://bugreports.qt.io/browse/QTBUG-117741) libvpx is not used
* [QTBUG-118655](https://bugreports.qt.io/browse/QTBUG-118655) Manual Deployment document of QtWebengine needs little
update.
* [QTBUG-119023](https://bugreports.qt.io/browse/QTBUG-119023) WebEngine accessibility crash when clicking on a link in
a list on macOS
* [QTBUG-117658](https://bugreports.qt.io/browse/QTBUG-117658) QWebEnginePage property url is missing NOTIFY, not-
usable from QML
* [QTBUG-117031](https://bugreports.qt.io/browse/QTBUG-117031) qmllint: Missing type information for WebEngine
* [QTBUG-119525](https://bugreports.qt.io/browse/QTBUG-119525) error: field ‘responseHeaders’ has incomplete type
‘QMultiMap<QByteArray, QByteArray>’
* [QTBUG-115357](https://bugreports.qt.io/browse/QTBUG-115357) qt 6.5.2 fails to build from source with system libpng
(regression from 6.5.1)
* [QTBUG-119536](https://bugreports.qt.io/browse/QTBUG-119536) Lack of documentation regarding QPdfBookmarkModel's
document property
* [QTBUG-118995](https://bugreports.qt.io/browse/QTBUG-118995) Dev tools not working
* [QTBUG-118398](https://bugreports.qt.io/browse/QTBUG-118398) QWebEngineView in QScrollArea is not scrollable
* [QTBUG-119776](https://bugreports.qt.io/browse/QTBUG-119776) PDF Multipage viewer example - Clicking on previous
(upward arrow) will crash the example
* [QTBUG-104766](https://bugreports.qt.io/browse/QTBUG-104766) QtQuick.Pdf PdfDocument gets
"QCoreApplication::postEvent: Unexpected null receiver" warning when
instantiated standalone
* [QTBUG-120245](https://bugreports.qt.io/browse/QTBUG-120245) A crash occurred in C:\Users\qt\work\qt\qtwebengine_stan
dalone_tests\tests\auto\pdfquick\multipageview\tst_multipageview.exe
* [QTBUG-120446](https://bugreports.qt.io/browse/QTBUG-120446) Alternated item color in list is not always alternated
* [QTBUG-119722](https://bugreports.qt.io/browse/QTBUG-119722) [REG 5 → 6] Default context menu is missing icons
* [QTBUG-104767](https://bugreports.qt.io/browse/QTBUG-104767) Using PdfPageImage instead of Image on PDF file results
in EXC_BAD_ACCESS (SIGSEGV)
* [QTBUG-118120](https://bugreports.qt.io/browse/QTBUG-118120) qtwebengine: build failure with x86_64h
* [QTBUG-119245](https://bugreports.qt.io/browse/QTBUG-119245) Qt Web Engine alert quotes not working
* [QTBUG-83338](https://bugreports.qt.io/browse/QTBUG-83338) Default implementations of javaScriptAlert/Confirm/Prompt
treat message as rich text
* [QTBUG-119789](https://bugreports.qt.io/browse/QTBUG-119789) [Accessibility] Qt 6.5.3 cannot be built with the option
' -no-feature-accessibility''.
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
* [QTBUG-109235](https://bugreports.qt.io/browse/QTBUG-109235) Review toupper/tolower uses [Qt]
* [QTBUG-107442](https://bugreports.qt.io/browse/QTBUG-107442) The endpoint in QWebEnginePage works only with FCM
* [QTBUG-109179](https://bugreports.qt.io/browse/QTBUG-109179) auto test qwebengineclientcertificatestore fails to
build
* [QTBUG-105124](https://bugreports.qt.io/browse/QTBUG-105124) qtwebengine crashes when `/usr/share/X11/xkb` is empty
* [QTBUG-110157](https://bugreports.qt.io/browse/QTBUG-110157) Incorrect command-line parsing if argc=0
* [QTBUG-96010](https://bugreports.qt.io/browse/QTBUG-96010) Issues with lifecycle example
* [QTBUG-110578](https://bugreports.qt.io/browse/QTBUG-110578) tst_QWebEngineView::horizontalScrollbarTest is flaky?
* [QTBUG-110749](https://bugreports.qt.io/browse/QTBUG-110749) Video decoding bug
* [QTBUG-110287](https://bugreports.qt.io/browse/QTBUG-110287) QWebEngineView does not load urls
* [QTBUG-63889](https://bugreports.qt.io/browse/QTBUG-63889) unbundle openjpeg
* [QTWB-67](https://bugreports.qt.io/browse/QTWB-67) Add support for changing text alignment
* [QTBUG-110504](https://bugreports.qt.io/browse/QTBUG-110504) Webengine extremely slow in loading webpage in debug
build
* [QTBUG-111306](https://bugreports.qt.io/browse/QTBUG-111306) tst_MultiPageView::navigation uses fixed positions
* [QTBUG-105988](https://bugreports.qt.io/browse/QTBUG-105988) a11y: Accessible interface can't be retrieved after
calling QAccessibleEvent::setChild on event created using the
constructor taking QAccessibleInterface*
* [QTBUG-108154](https://bugreports.qt.io/browse/QTBUG-108154) Saving to MHTML while printing to PDF crashes with
SIGSEGV
* [QTBUG-111852](https://bugreports.qt.io/browse/QTBUG-111852) Build failure of WebEngine (error when calling
compress_files.js)
* [QTBUG-112685](https://bugreports.qt.io/browse/QTBUG-112685) CMake policies are not in sync between qt repos and
macros included in top-level CMakeLists.txt
* [QTBUG-113413](https://bugreports.qt.io/browse/QTBUG-113413) LocalContentCanAccessFileUrls setting can prevent
navigation between local files
* [QTBUG-113485](https://bugreports.qt.io/browse/QTBUG-113485) Navigation asserts when LocalContentCanAccessRemoteUrls
is false
* [QTBUG-113551](https://bugreports.qt.io/browse/QTBUG-113551) Update documentation for limitation building QtPdf for
Android with supported  LTS versions
* [QTBUG-114367](https://bugreports.qt.io/browse/QTBUG-114367) QtPdf API review  findings
* [QTBUG-113416](https://bugreports.qt.io/browse/QTBUG-113416) [Reg 6.4->6.5] Static build fails at PDF module
* [QTBUG-105342](https://bugreports.qt.io/browse/QTBUG-105342) Test on qemu are very flacky
* [QTBUG-113369](https://bugreports.qt.io/browse/QTBUG-113369) dark mode enabled causes crashes on specific sites
* [QTBUG-104610](https://bugreports.qt.io/browse/QTBUG-104610) Does WebEngine support document download and print
operations in the document preview screen?
* [QTBUG-115188](https://bugreports.qt.io/browse/QTBUG-115188) QtWebEngine use after free in Extensions GetPreferences
* [QTBUG-113149](https://bugreports.qt.io/browse/QTBUG-113149) PDF download  from pdf viewer not working
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
* [QTBUG-114865](https://bugreports.qt.io/browse/QTBUG-114865) macos: Building QtWebEngine  with sanitizer enabled
fails
* [QTBUG-116595](https://bugreports.qt.io/browse/QTBUG-116595) QtPfd build failure on 32-bit arm
* [QTBUG-119763](https://bugreports.qt.io/browse/QTBUG-119763) [REG 6.5.2?] Rare segfaults in
QWebEngineDownloadItem::page()
* [QTBUG-111873](https://bugreports.qt.io/browse/QTBUG-111873) qt_attributions.json files should be valid JSON
* [QTBUG-119077](https://bugreports.qt.io/browse/QTBUG-119077) CMake deployment API does not deploy Qt Webengine
* [QTBUG-119878](https://bugreports.qt.io/browse/QTBUG-119878) [Reg 5.15->6.x] Crash and/or bad output when printing
via Qt WebEngine's PDF plugin
* [QTBUG-120692](https://bugreports.qt.io/browse/QTBUG-120692) Cannot cross-compile webengine for x86_64
* [QTBUG-86948](https://bugreports.qt.io/browse/QTBUG-86948) When using QImageReader to load a PDF then the PDF images
can be blurry and seem to be at half the size they should be
* [QTBUG-120764](https://bugreports.qt.io/browse/QTBUG-120764) PDF Viewer Widget example search error

* CVE-2023-6510: Use after free in Media Capture  
* CVE-2023-6702: Type Confusion in V8  
* CVE-2023-6703: Use after free in Blink  
* CVE-2023-6705: Use after free in WebRTC  
* CVE-2023-6706: Use after free in FedCM  
* CVE-2023-7024: Heap buffer overflow in WebRTC  
* CVE-2024-0222: Use after free in ANGLE  
* CVE-2024-0223: Heap buffer overflow in ANGLE  
* CVE-2024-0224: Use after free in WebAudio  
* CVE-2024-0225: Use after free in WebGPU  
* CVE-2024-0333: Insufficient data validation in Extensions  
* CVE-2024-0518: Type Confusion in V8  
* CVE-2024-0519: Out of bounds memory access in V8  
* CVE-2024-0807: Use after free in WebAudio  
* CVE-2024-0808: Integer underflow in WebUI  
* CVE-2024-0810: Insufficient policy enforcement in DevTools  
* CVE-2024-1059: Use after free in WebRTC  
* CVE-2024-1060: Use after free in Canvas  
* CVE-2024-1077: Use after free in Network  
* CVE-2024-1283: Heap buffer overflow in Skia  
* CVE-2024-1284: Use after free in Mojo  
* Security bug 1407197  
* Security bug 1485266  
* Security bug 1488199  
* Security bug 1505632  
* Security bug 1506535  
* Security bug 1506726  
* Security bug 1511389  
* Security bug 1511689  
* Security bug 1519980  

### qtwebview
* [QTBUG-112346](https://bugreports.qt.io/browse/QTBUG-112346) qmllint fails when WebView is used

### qtcharts
* [QTBUG-119712](https://bugreports.qt.io/browse/QTBUG-119712) QChartView prevents parent QScrollView from receiving
touch screen scroll events.
* [QTBUG-77403](https://bugreports.qt.io/browse/QTBUG-77403) Scrolling via trackpad does not work on Chart
* [QTBUG-119900](https://bugreports.qt.io/browse/QTBUG-119900) Deleting a visible QAbstractSeries with OpenGL enabled
causes an error

### qtscxml
* [QTBUG-119562](https://bugreports.qt.io/browse/QTBUG-119562) StateMachine Documentation wrong

### qtremoteobjects
* [QTBUG-117379](https://bugreports.qt.io/browse/QTBUG-117379) [REG: 5->6] Enums with ENUM in the type name cause error
in repc
* [QTBUG-120242](https://bugreports.qt.io/browse/QTBUG-120242) SubClassReplicaTest crashes

### qtquick3d
* [QTBUG-119373](https://bugreports.qt.io/browse/QTBUG-119373) typo in the document
* [QTBUG-120579](https://bugreports.qt.io/browse/QTBUG-120579) The link to the Fog QML type is not correct
* [QTBUG-120431](https://bugreports.qt.io/browse/QTBUG-120431) QQ3DPhysics customshapes example looks different on
opengl vs d3d11
* [QTBUG-120109](https://bugreports.qt.io/browse/QTBUG-120109) WasdController: Models stutter in Qt Quick 3D Physics
example

### qtmqtt
* [QTBUG-104478](https://bugreports.qt.io/browse/QTBUG-104478) Mqtt topic wildcard failure

### qthttpserver
* [QTBUG-121219](https://bugreports.qt.io/browse/QTBUG-121219) QtHttpServer crashes when during GET of a larger content
remote closes connection
* [QTBUG-120746](https://bugreports.qt.io/browse/QTBUG-120746) QWebSocket immediately disconnects after without
receiving anything

### qtquick3dphysics
* [QTBUG-120045](https://bugreports.qt.io/browse/QTBUG-120045) Application crashes in Qt Quick 3D Physics
* [QTBUG-121033](https://bugreports.qt.io/browse/QTBUG-121033) onBodyContact being called after object is deleted

### qtgrpc
* [QTBUG-119475](https://bugreports.qt.io/browse/QTBUG-119475) examples/grpc/magic8ball/clientservice.cpp:26:14: error:
invalid use of incomplete type ‘class QDebug’
* [QTBUG-116640](https://bugreports.qt.io/browse/QTBUG-116640) Protobuf generator doesn't support C++ keywords field
names
* [QTBUG-121544](https://bugreports.qt.io/browse/QTBUG-121544) qtprotobufgen generates the corrupted
protobufwellknowntypes_exports.qpb.h

Known Issues
------------

* Qt 6.5.5-1 provides a fix for QTBUG-122889 videowidget- fails to play video  
In Qt 6.5.5, the FFmpeg plugin is not delivered with Qt Multimedia on Windows  
platforms and Android armeabi-v7a due to provisioning issues. This was fixed  
with Qt 6.5.5-1 that updates the related Windows and Android targets.  
  
* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-6.5/supported-platforms.html  
  
* The RTA (release test automation) reported issues in Qt 6.5.x:  
https://qt-project.atlassian.net/issues/?filter=15085  
  
* See Qt 6.5 known issues from:  
https://wiki.qt.io/Qt_6.5_Known_Issues  
  
* Qt 6.5.5 Open issues in Jira:  
https://qt-project.atlassian.net/issues/?filter=16115  

Credits for the  release goes to:
---------------------------------

Eirik Aavitsland  
Amir Masoud Abdol  
Laszlo Agocs  
Yigit Akcay  
Anu Aliyas  
Tim Angus  
Karolina Sofia Bang  
Rolf Eike Beer  
Vladimir Belyavsky  
Nicholas Bennett  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
Mikolaj Boc  
Joerg Bornemann  
Rym Bouabid  
Assam Boudjelthia  
Kai Uwe Broulik  
Michael Brüning  
Olivier De Cannière  
Ed Cooke  
Alexandru Croitor  
Mitch Curtis  
Thibaut Cuvelier  
Giuseppe D'Angelo  
Szabolcs David  
Pavel Dubsky  
Artem Dyomin  
Alexey Edelev  
David Edmundson  
Oliver Eftevaag  
Christian Ehrlicher  
Andreas Eliasson  
Ilya Fedin  
Nicolas Fella  
Florian de Gaulejac  
Joshua Goins  
Aleix Pol Gonzalez  
Robert Griebl  
Mikko Gronoff  
Jan Grulich  
Johannes Grunenberg  
Kaj Grönholm  
Richard Moe Gustavsen  
Lucie Gérard  
Rob Hall  
Mikko Hallamaa  
Jøger Hansegård  
Inkamari Harjula  
Andre Hartmann  
Tero Heikkinen  
Jani Heikkinen  
Paul Heimann  
Christian Heimlich  
Ulf Hermann  
Volker Hilsheimer  
Samuli Hölttä  
Sam James  
Allan Sandfeld Jensen  
Maurice Kalinowski  
Jonas Karlsson  
Timothée Keller  
Friedemann Kleint  
André Klitzing  
Michal Klocek  
Lars Knoll  
Jarek Kobus  
Sze Howe Koh  
Jarkko Koivikko  
Jani Korteniemi  
Fabian Kosmale  
Volker Krause  
Mike Krus  
Santhosh Kumar  
Kai Köhne  
Inho Lee  
Kimmo Leppälä  
Thorbjørn Lindeijer  
Thiago Macieira  
Christophe Marin  
Ievgenii Meshcheriakov  
Safiyyah Moosa  
Bartlomiej Moskal  
Marc Mutz  
Antonio Napolitano  
Martin Negyokru  
Andy Nichols  
Mårten Nordheim  
Samuli Piippo  
Timur Pocheptsov  
Lauri Pohjanheimo  
Joni Poikelin  
Aleix Pol  
Alessandro Portale  
Lorn Potter  
Liang Qi  
Matthias Rauter  
David Redondo  
Topi Reinio  
Shawn Rutledge  
Ahmad Samir  
Lars Schmertmann  
Carl Schwan  
Thomas Senyk  
Ivan Solovev  
Axel Spoerl  
Patryk Stachniak  
Christian Strømme  
Tarja Sundqvist  
Lars Sutterud  
Jan Arve Sæther  
Morten Sørvig  
Sadegh Taghavi  
Benjamin Terrier  
Ivan Tkachenko  
Esa Törmänen  
Peter Varga  
Doris Verria  
Tor Arne Vestbø  
Juha Vuolle  
Jaishree Vyas  
Michael Weghorn  
Edward Welbourne  
Paul Wicking  
Piotr Wiercinski  
Piotr Wierciński  
Oliver Wolff  
Jannis Xiong  
Lu YaNing  
Semih Yavuz  
Yifan Zhu  
Yansheng Zhu  
shjiu  
