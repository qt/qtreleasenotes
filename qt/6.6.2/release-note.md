Release note  
============  
Qt 6.6.2 release is a patch release made on the top of Qt 6.6.1.  
As a patch release, Qt 6.6.2 does not add any new functionality but provides  
bug fixes and other improvements and maintains both forward and backward  
compatibility (source and binary) with Qt 6.6.1.  

For detailed information about Qt 6.6, refer to the online documentation  
included in this distribution. The documentation is also available online:  
  
https://doc.qt.io/qt-6/index.html  
  
The Qt version 6.6 series is binary compatible with the 6.5.x series.  
Applications compiled for 6.5 will continue to run with 6.6.  
  
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
* CVE-2023-51714 in qtbase  
    
### qtbase  
* 9ceb7cb555 QMimeDatabase: handle buggy type definitions with circular  
inheritance  
Added code to detect and break circular inheritance loops in the MIME  
data, which were causing infinite loops  
  
* 14c4da28f1 configure: Make sure the configure script exits with  
cmake's exit code  
The configure script on UNIX systems will now exit with the same exit  
code that the underlying cmake process exited with.  
  
* 59a2d5bdba SQLite: Update SQLite to v3.44.1  
Updated SQLite to v3.44.1  
  
* 28bdd104fd OpenSSL: remove support for 1.1  
Support for OpenSSL 1.1 has been dropped. Qt now only supports OpenSSL  
3.  
  
* 6adf78c511 macOS: Implement QPlatformServiceColorPicker via  
NSColorSampler  
Non native color dialogs now use native color picking when picking  
colors from the screen.  
  
* 5c8e47d2dd SQLite: Update SQLite to v3.44.2  
Updated SQLite to v3.44.2  
  
* 7270e2ab75 Fix QStringConverter::encodingForName() for trailing `-`,  
`_`  
Fixed a bug where encodingForName() failed due to trailing characters  
(`_`, `-`) that ought to have been ignored.  
  
* cf26c939d7 Fix return value of qbswap(qint128)  
Fixed return type of qbswap(qint128) (was: quint128).  
  
* 19a473137a Fix Maximized frameless window painting wrong with  
WS_THICKFRAME  
Adding a check for the maximized state of the window during the  
calculation of margins. Margins calculation will not be skipped for  
maximized windows.  
  
* 57e98a4136 SQLite: Update SQLite to v3.45.0  
Updated SQLite to v3.45.0  
  
* e2598f175f QUuid: Fix Id128Bytes alignment on some architectures  
The QUuid::Id128Bytes type had a loose definition that could cause it  
be passed incompatibly between functions, in some architectures,  
depending on whether GNU extensions were allowed. This is now fixed, but  
may cause code compiled with Qt 6.6.0 and 6.6.1 to fail when recompiled  
with 6.6.2 or later.  
  
* f7add7ad0f Increase precision for QGraphicsView::AnchorUnderMouse  
Increase precision for QGraphicsView::AnchorUnderMouse and  
QGraphicsView::centerOn  
  
* a619b6dd41 SQL/MySQL: Fix compilation with MySQL 8.3  
Fixed compilation with MySQL 8.3.  
  
* 6914f7ce3b Update Zlib to 1.3.1  
zlib was updated to version 1.3.1.  
  
* bf196d0dd3 Doc: Update Copyright in md4c license text  
Updated md4c (optional part of Qt Gui) to version 0.5.1.  
  
* 0710865eed API Review Widgets: Remove QDockWidget debug operators  
Removed debug streaming operator incorrectly introduced as a new symbol  
in Qt 6.6.1.  
  
* 1ac17f25fa Update bundled libpng to version 1.6.41  
libpng was updated to version 1.6.41  
  
* bda58a780c SQLite: Update SQLite to v3.45.1  
Updated SQLite to v3.45.1  
  
* d1348ac94f Update md4c to 0.5.2  
md4c was updated to 0.5.2.  
  
* 736d6300bb CMake: Fix undefined symbol: qt_resourceFeatureZstd issue  
Targets created with qt_add_executable and qt_add_library will now add  
the --no-zstd option to AUTORCC_OPTIONS when the target platform does  
not support zstd decompression. You can opt out via the  
QT_NO_AUTORCC_ZSTD cmake variable.  
  
* f9537eda1d Update bundled libjpeg-turbo to version 3.0.2  
libjpeg-turbo was updated to version 3.0.2  
  
* 303586dd18 Update bundled libpng to version 1.6.42  
libpng was updated to version 1.6.42  
  
### qtdeclarative  
* 29fc139acc Disable TapHandler.longPressed signal if longPressThreshold  
== 0  
TapHandler.longPressThreshold can now be set to 0 to disable its press-  
and-hold feature, and can be reset to undefined to restore the platform  
default.  
  
* d8a4fda904 Drawer: adjust opening edge to the rotation of the window's  
content item  
If the window's content item is rotated, then the drawer will adapt the  
edge from which it can be drawn out accordingly. Only multiple of 90  
degrees are supported.  
  
* 852067de0c QML: Let IDs in outer context override bound components'  
properties  
In QML documents with bound components, IDs defined in outer contexts  
override properties defined in inner contexts now. This is how  
qmlcachegen has always interpreted bound components when generating C++  
code, and it is required to make access to outer IDs actually safe. The  
interpreter and JIT have previously preferred inner properties over  
outer IDs.  
  
* 18fc3862d0 MessageDialog: Dont rely on accept or reject signal  
emissions from QPA  
The MessageDialog will now close when a button is pressed, regardless  
of the button's role.  
  
* 9e44f21a2e CMake: Fix the all_qmllint* targets for VS generators, take  
II  
When using CMake's Visual Studio project generator, the creation of the  
targets all_qmllint, all_qmllint_json and all_qmllint_module requires  
now CMake 3.19 or newer. A warning is printed for older CMake versions.  
This warning can be disabled by setting QT_NO_QMLLINT_CREATION_WARNING.  
  
### qttools  
* 96289e100 CMake: Fix qt_add_translations in different subdirs for VS  
generators  
When using CMake's Visual Studio project generator, the creation of the  
update_translations target requires now CMake 3.19 or newer. A warning  
is printed for older CMake versions. This warning can be disabled by  
setting QT_NO_GLOBAL_LUPDATE_TARGET_CREATION_WARNING to ON.  
  
### qt3d  
* dbc230139 Enable uniform buffer for RHI compute shaders  
Enable uniform buffer for RHI compute shaders  
  
### qtgrpc  
* 1906fad Add the missing Licenses and Attributions sections  
qtprotobufgen, qtgrpcgen tools link against protobuf libraries,  
licensed under BSD 3-clause "New" or "Revised" License. This is now  
documented.  
  
### qtinsighttracker (Commercial only)  
* 148593e Support remote configurations  
Application's insight tracker configuration can be changed at runtime  
from the Qt Insight Console.  
  
* d9dc7f6 Support compressed sqlite databases  
The SQLite event storage can now be compressed with either zlib or zstd  
algorithms.  
  
* 5cb9322 Add context data to event API  
New API: Context data can now be included in the interaction and  
transition events.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-118458 TLS Invalid Token  
* QTBUG-105395 WM_TRANSIENT_FOR is not kept in sync  
* QTBUG-41696 QApplication::widgetAt() doesn't work with widgets with  
Qt::WA_TransparentForMouseEvents on Mac  
* QTBUG-119092 [REG: 6.5.2->6.5.3] macOS: topLevelAt/widgetAt cannot  
find something under a window with setIgnoresMouseEvents set  
* PYSIDE-2525 Segfaults related to QMenu on macOS  
* QTBUG-102831 QCompleter's suggestion list hides native Chinese Input  
method  
* QTBUG-114188 QMdiArea::TabbedView not honored with single subwindow  
* QTBUG-117762 "The cached device pixel ratio value was stale on window  
expose" when closing window on Wayland  
* QTBUG-112479 Touch Drag doesn't cause mousePressEvent after Touch  
Press  
* QTBUG-119032 Mouse Release is not fired with touch screen  
* QTBUG-100688 TapHandler doesn't emit  onDoubleTapped when using a  
touchscreen  
* QTBUG-119219 macOS: NPE in QNSWindow applicationActivationChanged  
* QTBUG-118605 CTRL+Tab don't work in combobox  
* QTBUG-115156 Last character missing with JAWS  
* QTBUG-119366 QTabBar is incorrectly offset when changing the  
TabPosition  
* QTBUG-111528 Android font does not depend on locale/OS preference but  
is hardcoded  
* QTBUG-117765 moc chokes on <concepts> from xcode13  
* QTBUG-114539 QToolButton arrow clipped on screen with non-integer  
device pixel ratio  
* QTBUG-119338 Objective-C usage can result in undefined behavior (part  
2)  
* QTBUG-87334 Graphical issue on some Android smartphones: white line at  
the top and the right side of the screen  
* QTBUG-119239 Incorrect reading of Plain PBM images  
* QTBUG-118416 [wasm] Signal from another thread is discarded while the  
thread is temporarily blocking  
* QTBUG-106928 QObject: Cannot create children for a parent that is in a  
different thread when exiting Android app  
* QTBUG-118421 TextField logs "Cannot create children for a parent that  
is in a different thread" when closing virtual keyboard  
* QTBUG-88508 some tests are not saving result output to file on Android  
* QTBUG-115045 Don't overwrite my CMAKE_<Config>_POSTFIX  
* QTBUG-115730 Qt uses Macros and config files from install tree when  
building qtdeclarative "again"  
* QTBUG-119511 windeployqt -v has no effect  
* QTBUG-64373 QPushButton with RightToLeft layoutDirection and an icon  
crops text in Fusion style  
* QTBUG-114253 [REG: 5.11->6] Performance issue with loading images in  
static build  
* QTBUG-119424 windows: Too long tooltip crashes  
* QTBUG-118070 When configuring with debug info, installed libraries  
shoudn't be stripped  
* QTBUG-118907 Not correct QDataStream version  
* QTBUG-106479 androidtestrunner does not honour QTEST_FUNCTION_TIMEOUT  
* QTBUG-115298 Androidtestrunner freezes after obtaining SDK version  
* QTBUG-119602 PainterPaths-Graphic&Multimedia-Example typo in the  
documentation  
* QTBUG-118568 qvulkanwindow  repeatedly recreate swapchain  
* QTBUG-119499 Document QMessageAuthenticationCode  using HMAC  
* QTBUG-116898 Change deprecation information for  
QtFuture::makeReadyFuture  
* QTBUG-119716 qt6_add_repc_sources produces an error if a genex is used  
for preprocessor macros  
* QTBUG-119464 QSslSocket::setCiphers() documentation uses weak cyphers  
* QTBUG-118223 QDockWidget generates leftover containers + crash  
* QTBUG-99136 QDockWidget not correctly parented/setup if dragged from  
another floating and tabified QDockWidget  
* QTBUG-118578 Undocking tabbed widget from floating window creates  
empty redundant window  
* QTBUG-118579 Undocking tabbed widget from main window onto the  
floating window crashes app  
* QTBUG-56799 [QDockWidget - Crash] Double Clicking to re-parent docks  
can cause a crash.  
* QTBUG-35736 "Index out of range" situation in QMainWindowLayout class  
* QTBUG-63448 Undocking window does not send topLevelChanged signal  
* QTBUG-88329 Delete a QDockWidget while drag in progress causes crash  
* QTBUG-88157 tabPosition called with out-of-bounds when closing an  
undocked QDockWidget  
* QTBUG-94097 creating QDockWidget after application startup prevents  
correct termination on Ubuntu  
* QTBUG-44540 QDockAreaLayoutInfo crashes in restoreState (l. 1978-9)  
when restoring closed, floating QDockWidget  
* QTBUG-53808 QDockWidget losing decoration on undocking when  
GroupedDragging is enabled  
* QTBUG-72915 QDockWidget doesn't properly dock anymore after it was  
undocked (regression)  
* QTBUG-53438 QMainWindow: tabbed QDockWidgets leave invisible QTabBar  
* QTBUG-116350 Fix documentation to refer to QNtfsPermissionCheckGuard  
instead of qt_ntfs_permission_lookup  
* QTBUG-114849 Big icons in QTabWidget are badly aligned (regression  
from Qt5 to Qt6)  
* QTBUG-119650 Model adapter/replica incompatible across different Qt  
versions and platforms  
* QTBUG-119526 [Reg 6.6.0->6.6.1]QCocoaAccessibility Crash with Mac  
VoiceOver enabled  
* QTBUG-118585 "Crash" in QMacAccessibilityElement initWithId:role:  
* QTBUG-118800 Programmatically selecting item view item breaks a11y  
focus  
* QTBUG-119797 [Reg 6.5.3 -> 6.6.1]QFileIconProvider.icon of a file only  
give general file icon  
* QTBUG-118667 QIcon::addFile() with an invalid filename results in  
QFile::isNull() == false  
* QTBUG-119155 [REG: 6.5.2->6.5.3] headerDataChanged is now queued and  
parameters may be out of sync  
* QTBUG-119371 [macOS] (File|Folder)Dialog.currentFolder holds stale  
data  
* QTBUG-119054 Mac: Focus issues when embedding into non-Qt apps  
* QTBUG-120025 The QMainWindowLayout::restoreState causes a crash  
* QTBUG-118642 [Reg6.4->6.5]WebAssembly - QML - failing to use Noto  
Color Emoji font  
* QTBUG-49720 Documentation for QFileDialog::DontConfirmOverwrite should  
mention QFileDialog::AcceptMode  
* QTBUG-18057 QPixmap::toWinHBITMAP(): 2 Bugs when running out of memory  
(Access violation or lost HBITMAP handle)  
* QTBUG-119406 QFuture::then() with context object deadlocks  
* QTBUG-119103 QFuture hangs when continuation uses a context object and  
is resolved from the same thread  
* QTBUG-117918 Debug builds with QFuture::waitForFinished and same-  
thread continuations may deadlock  
* QTBUG-119579 [Reg 6.5 -> 6.6] Calling QPromise::finish() from the same  
thread deadlocks i  
* QTBUG-119810 QFuture continuation with deleted context  
* QTBUG-120036 DFEATURE_libjpeg CMake option not working  
* QTBUG-120006 DeleteStartOfWord with a selection in QLineEdit has  
unexpected behavior  
* QTBUG-119225 [Reg 6.2 -> 6.5] QSplashScreen no longer shows on Linux  
with a single call to QCoreApplication::processEvents()  
* QTBUG-120054 Reg6.4->6.5 Stylesheet has no Effect on QMessageBox  
* QTBUG-119306 drawPoints and drawPolygon don't match  
* QTBUG-119972 Clang-tidy reports possible memory leak with  
QMetaObject::invokeMethod  
* QTBUG-115765 QAbstractItemView::EditingState: state stale when editing  
with a proxy model  
* QTBUG-117903 WM_CHAR creates unwanted keyboard event - activating  
shortcut  
* QTBUG-119309 Qt fails to flush to Mac native sub window when tlw is  
RHI  
* QTBUG-119902 Crash in QImage::scaled  
* QTBUG-110266 affine example crashes when moving the center hoverpoint  
* QTBUG-119167 Atspi.Table.get_row_column_extents_at_index can cause  
segfault in tree  
* QTBUG-118225 QtQuick Loader doesn't load over http(s)  
* QTBUG-120050 Configuring a CMake-based Qt WASM project fails if emsdk  
path has spaces  
* QTBUG-119752 Customized QToolTip with padding or margin displays  
incorrectly  
* QTBUG-119708 VS2022 simple program fails to link in Release mode with  
ProtobufWellKnownTypes  
* QTBUG-112920 FTBFS qt 6.5.0 on gcc 9  
* QTBUG-120062 Non-native QFileDialog gets frozen on destruction if  
remote mapped drive is disconnected  
* QTBUG-115260 Hang during drag and drop [REG]  
* QTBUG-120055 When dragging QTableView columns scrolling behaves oddly  
* QTBUG-113573 When dragging a header section it will no longer scroll  
when at the edge  
* QTBUG-47159 QFileDialog::selectFile does not keep native separators  
* QTBUG-120141 cmake build of a Qt project with static Qt linkage fails  
due to error in qtbase/cmake/FindWrapResolv.cmake  
* QTBUG-119619 CMake deploy script finds x64 libraries for WoA  
application.  
* QTBUG-117704 Dragging Window handling WM_NCCALCSIZE and WM_NCHITTEST  
squishes contents  
* QTBUG-120121 a11y QComboBox: Problematic signal/slot activation order  
* QTBUG-120125 CMake subarch extraction does not always succeed  
* QTBUG-120257 widgets/itemviews/editabletreemodel not compiling on  
Android  
* QTBUG-113865 [Text Editor]Using undo function causes the app to crash  
* QTBUG-120012 Limiting maximum allocation size for QDataStream  
* QTBUG-119178 Crash after registering an invalid resource file  
* QTBUG-120107 PDF view gets render mistakes on Android 10  
* QTCREATORBUG-30117 Help viewer: "[read-only]" tags have unreadably low  
contrast in dark mode  
* QTBUG-120379 The `QStringLiterals` header is lost  
* QTBUG-119808 [REG 6.1 -> 6.6] QPlainTextEdit: Placeholder is not  
hidden on input  
* QTBUG-118161 QFileDialog::getOpenFileContent not working in sometimes  
* QTBUG-116989 wasm:  pen pointerhandler example does not work as  
expected  
* QTBUG-101404 wasm: mobile keyboard keeps popping on on android  
* QTBUG-120327 Pen PointerEvents not handled in WebAssembly (fix  
attached)  
* QTBUG-119995 QML - Text - Font weight - macOS/Windows difference  
* QTBUG-112870 clang-tidy warnings on static global variables in moc  
generated code  
* QTBUG-113507 macOS: Popups opening on wrong screen  
* QTBUG-67708 QGroupBox title does not follow vertical alignment with  
fusion style  
* QTBUG-103825 Wrong resolution of Icon in Windows (Toast) Notifications  
* QTBUG-120335 On certain machines QtConcurrent crashes if no free  
threads on thread pool  
* QTBUG-120614 QImage::convertToFormat: wrong conversion from RGBA64 to  
RGBA16FPx4  
* QTBUG-120302 AddressSanitizer: heap-use-after-free in  
tst_QFuture::continuationsWithContext()  
* QTBUG-120574 QComboBox popup high decreases when hiding view items  
* QTBUG-83604 QSlider with ticks is glitchy with QFusionStyle  
* QTBUG-120572 [QDoc] Redundant text in QTabBar detailed description  
* QTBUG-120297 Q_GADGET forces following elements to be private  
* QTBUG-120758 qtdeclarative fails to build with conan 2 on windows:  
include path too long  
* QTBUG-120474 4xMSAA doesn't work with Mali400 using Lima driver  
* QTBUG-117975 Memory leaks when QObject::deleteLater is used without  
QApplication runloop  
* QTBUG-117533 QProcess does not work with thread sanitizer  
* QTBUG-117954 QProcess::startDetached quits application when running  
with ASAN  
* QTBUG-104493 Application performance drops if many threads are running  
while QProcess creates sub-processes on Unix  
* QTBUG-120624 UB when passing null string to QString::arg()  
* QTBUG-120350 QOffScreenSurface::isValid always returns false on  
WebAssembly  
* QTBUG-58005 ibus: commit does not properly reset the preedit string  
* QTBUG-120487 Symlinks generated in user_facing_tool_links.txt during  
configuration are incorrect for MacOS  
* QTBUG-120732 Qimagereader manual test - Image file is missing  
* QTBUG-121041 Fusion style: add clip region for groupbox title  
* QTBUG-121030 QIconLoader failed to find icon in hicolor  
* QTBUG-121015 tst_QGuiApplication::topLevelAt() failed on Wayland  
* QTBUG-120485 QT_INSTALL_DOCS configured with wrong path  
* QTBUG-120619 QHttpServer with QtConcurrent blocks until the very first  
request has finished before being able to process in parallel  
* QTBUG-118503 WASM: arrow keys and select-all not working for  
QPlainTextEdit on touchscreen  
* QTBUG-119248 The result of calling serviceUUID is different in Q5 and  
Qt6  
* QTBUG-120961 QLocale::monthName() doesn't work correctly on Windows  
* QTBUG-121204 ~unique_ptr() static assertion failure due to incomplete  
type T (C++23)  
* QTBUG-120577 qt6.5.3 QTextEdit can't display image ! but qt5.15 is ok  
。  
* QTBUG-120968 QProcess::start(): Fix docs about Starting state on  
Windows  
* QTCREATORBUG-30066 Git commands fail on windows when using the  
QProcess backend  
* QTBUG-120976 REG: QPushButton of a menu will still appear pressed even  
after you click somewhere outside the button area.  
* QTBUG-121183 [QMYSQL] The mysql_list_fields() was removed in MySQL  
v8.3  
* QTBUG-120509 Crash when Qt re-create native windows if  
WA_DontCreateNativeAncestors is set  
* QTBUG-121512 [Reg 6.6.0(1) -> 6.6.2] Drag & Drop not working in  
Designer  
* QTBUG-119216 macOS: REG->6.5: DnD with custom text MIME type got  
broken/crashes  
* QTBUG-120469 Crash in QCocoaSystemTrayIcon::emitActivated() when  
calling QComboBox clear() then addItem()  
* QTBUG-121008 Crash in QMacAccessibilityElement when using  
QTreeView/QCombobox  
* QTBUG-121515 [Reg 6.6.1 -> 6.6.2] QNetworkAccessManager never finishes  
request if server sends status code 401 without a challenge  
* QTBUG-121514 [Reg 6.6.0->6.6.2] Focus wrong in dialog with  
QDialogButtonBox  
* QTBUG-121557 [Reg 6.4.3->6.6] Application unusable after closing  
nested message boxes  
* QTBUG-121948 RCC compression is broken when deploying to Android from  
a Linux host using CMake  
* QTBUG-106466 build android app with Debian host fails on undefined  
symbol qt_resourceFeatureZstd  
* QTBUG-101353 AUTORCC uses zstd even if Qt is build without rcc support  
* QTBUG-121697 Critical crash when creating QPlainTextEdit when using  
styles/stylesheets.  
* QTBUG-121790 QApplication::setStyleSheet crashes QTextEdit  
* QTBUG-87438 corelib plugin tests fail on Android  
* PYSIDE-2492 uic does not generate enumeration name into enum values  
causing type checking warnings  
* QTBUG-117702 qbittorrent dumped core  
* QTBUG-114604 Setting initial page orientation for QPrintDialog does  
not work in Windows 11  
* QTBUG-119359 tst_QGuiEventLoop::processEvents is flaky on QNX  
* QTBUG-118489 Can't tab to last button in QDialogButtonBox  
* QTBUG-88264 [REG v6.0.0-beta3 -> dev] Top-level configure fails if  
told to build tests  
* QTBUG-86035 Split QtBuild.cmake into smaller files  
* QTBUG-119490 qcocoaapplicationdelegate.mm:354:20: error: cannot  
initialize return object of type 'BOOL'  
* QTBUG-119081 QProcessPrivate::waitForDeadChild() doesn't check  
forkfd_wait's return code  
* QTBUG-119616 tst_Http2::duplicateRequestsWithAborts fails in CI  
* QTBUG-116905 QMimeDatabase doesn't return all glob patterns for mime  
types specified in multiple locations  
* QTBUG-82434 Incorrect Appearance QCursor with AA_EnableHighDpiScaling  
* QTBUG-101141 moc: namespaced base class not properly resolved in  
cpp.json file  
* QTBUG-119998 CMake errors out with recursion in latest dev when using  
qt-cmake-standalone-test on in-source auto test  
* QTBUG-111443 macOS/iOS: "Detected system locale encoding (US-ASCII,  
locale "C") is not UTF-8"  
* QTBUG-119077 CMake deployment API does not deploy Qt Webengine  
* QTBUG-116577 ASSERT: "sumFactors > 0.0"  in qgridlayoutengine.cpp  
* QTBUG-120196 Maximized frameless window painting wrong view region  
with Qt::FramelessWindowHint and Windows api WS_THICKFRAME  
* QTBUG-115125 QObject::connect warns, but also fails to connect to  
lambdas with Qt::UniqueConnection  
* QTBUG-118829 androiddeployqt with --release includes various  
qmltooling libs  
* QTBUG-117443 Two Android executables mix their build artifacts if  
targets are added in a single CMakeLists.txt  
* QTBUG-114583 Headers use things in <iterator> without including it  
* QTBUG-120460 tst_QHostInfo::reverseLookup() fails on qemu and blocks  
CI  
* QTBUG-109877 macOS: QFileDialog::getSaveFileName() truncates a  
compound extension  
* QTBUG-99750 cannot activate file system watcher in QFileSystemModel  
* QTBUG-117910 [windeployqt] The QtPDF module will always be deployed if  
it's installed  
* QTBUG-116763 out-of-bounds operator+  
* QTBUG-113498 QVideoWidget in QDialog does not show / crashes (macOS)  
when shown twice  
* QTBUG-119601 iOS: Sometimes soft keyboard can't be closed  
* QTBUG-96879 QGraphicsView::setTransformationAnchor(AnchorUnderMouse)  
drifts when zooming with trackpad  
  
### qtdeclarative  
* QTBUG-29676 Signals not disconnected when target object is destroyed  
* QTBUG-75483 QML Tooltip visibility is set to false but should not  
* QTBUG-115166 qt_add_qml_module() causes non-Ninja generators to think  
that projects are never up-to-date  
* QTBUG-93856 Menus with a certain fixed height, element height and  
window height not scrolled when they should  
* QTBUG-119132 it should be possible to disable the  
TapHandler.longPressed signal  
* QTBUG-105810 iOS: TapHandler emits clicked, even if long pressed more  
than StyleHint::MousePressAndHoldInterval  
* QTBUG-119091 QmlCacheGen crashes on QML-file, but won't disclose  
where/why it cashes  
* QTBUG-119090 QmlCacheGen miscompiles Enum constant reference, yielding  
"undefined"  
* QTBUG-53987 Cursor is not updated on mouse wheel over flickable  
* QTBUG-90457 HoverHandler.cursorShape doesn't change dynamically within  
same bounds  
* QTBUG-54019 regression in certain MouseArea hover use cases  
* QTBUG-115696 Delegates are not re-positioned when ListView orientation  
is changed runtime  
* QTBUG-119122 Using a specific as-cast asserts and fails compilation  
* QTBUG-112673 Drag.imageSource example - no image on first drag  
* QTBUG-115491 Drag.imageSource Only Works On Second try  
* QTBUG-118779 QT quick control-wearable demo-example Issue with the  
background when switching light/dark mode  
* QTBUG-119298 [macOS] Using Imagine style controls provokes Qt warning  
* QTBUG-119181 Crash in QQmlDelegateModelGroup::insert  
* QTBUG-83155 Roboto font used in Material style slows down startup time  
* QTBUG-115121 PathView can be clicked through if it is flicking and  
delegate has MouseArea  
* QTBUG-119216 macOS: REG->6.5: DnD with custom text MIME type got  
broken/crashes  
* QTBUG-119165 qmlsc: QUrl does not compile in console.log()  
* QTBUG-80910 Drawer item does not support rotation  
* QTBUG-71117 When the contentOrientation is changed for the  
ApplicationWindow, then the Drawer does not drag out as expected  
* QTBUG-115536 Setting Window.contentOrientation breaks Popup on regular  
desktop  
* QTBUG-119160 Graphics corruption when toggling depth-aware rendering  
* QTBUG-119005 QML FileDialog file size overflow  
* QTBUG-115710 [Windows and WSL2] QML module that only contains C++ code  
breaks `all_qmllint` target  
* QTBUG-119147 Invalid input not handled in Qt Quick Controls - Contact  
List example  
* QTBUG-119451 the document is incorrect about the data type in the code  
snippet  
* QTBUG-119162 Qml: Behaviour differs between interpreted/compiled code  
* QTBUG-118902 Qmltyperegistrar doesn't escape "-" in "#ifdef" generated  
code  
* QTBUG-119531 [Reg 6.6.0 -> 6.6.1] TypeError: Type error with aliases  
* QTBUG-119084 Connections type doesn't work in qmltc'ed app  
* QTBUG-117948 qt_generate_deploy_qml_app_script() deploys QML plugin  
target but not the corresponding backing target  
* QTBUG-119838 [REG] qt_add_qml_module broken for the VS generator when  
called in different subdirectories  
* QTBUG-119395 crash on QML property bindings  
* QTBUG-118445 Native macOS MessageDialog doesn't reopen  
* QTBUG-118212 [Reg 5.15->6.x][Android] MessageDialog's standard buttons  
do not accept/reject the dialog  
* QTBUG-120005 Native TextArea: placeholderText does not respect  
horizontalAlignment  
* QTBUG-108807 QQC2 TabBar first TabButton visual state incorrect when  
deselected  
* QTBUG-109488 tst_qquicktextedit FAIL  
* QTBUG-119715 REG: ScrollView content size broken  
* QTBUG-119675 [qmllint ] Enabling the qmllint for a lot of QML files  
exceeds the command line limitation on Windows host  
* QTBUG-117387 TapHandler and DragHandler interoperability breaks  
* QTBUG-66360 PointHandler goes inactive releasing mouse button when  
multiple pressed  
* QTBUG-83980 HoverHandler: sometimes point.position returns (0, 0)  
* QTBUG-119363 UniformAnimator makes app crash when being destroyed by  
other component  
* QTBUG-119793 QML Button (Material 3) contents truncated  
* QTBUG-119640 Typo in the document  
* QTBUG-119794 QJSValue: url does not convert to QUrl  
* QTBUG-119963 [Reg 6.5.1->6.5.3] QJSEngine no longer converts new'ed JS  
object to QVariantMap  
* QTBUG-120205 [REG: 6.5->6.6] Image implicitWidth/Height no longer  
available in onStatusChanged  
* QTBUG-119916 Non-native FileDialog does not prompt about overwriting  
an existing file  
* QTBUG-120349 Window Qml Type doc is missing the default visible  
property value  
* QTBUG-116306 Mention indeterminate state for Qt Quick Controls 2  
ProgressBar customization  
* QTBUG-120346  hovered property of HoverHandler stays true when sliding  
by touch outside of hover area  
* QTBUG-117899 [REG 6.4->6.5] Binding Loops -> Wrong layout because of  
interruption  
* QTBUG-118511 Binding loop if ColumnLayout implicitWidth is changed  
* QTBUG-120296 Qt Quick Widgets Example  -  Grab Framebuffer is  
susceptible to crash  
* QTBUG-119917 Non-native FileDialog loses current filename when  
changing folders  
* QTBUG-120052 TextArea/TextField: placeholderText does not respect  
horizontalAlignment after the component creation  
* QTBUG-119646 [Tests] Warnings in  
qtdeclarative/tests/auto/quickcontrols/controls/data/tst_textfield.qml  
* QTBUG-119645 [Tests] Warnings in  
qtdeclarative/tests/auto/quickcontrols/controls/data/tst_textarea.qml  
* QTBUG-99231 "Could not set initial property horizontalAlignment" when  
trying to set resettable property  
* QTBUG-119372 build fails with Q_IMPORT_QML_PLUGIN macro  
* QTBUG-120628 TableView: cannot select cells when using mouse press +  
shift  
* QTBUG-113776 qmlformat fails to format if there is a escape char in  
the key string  
* QTBUG-119760 Crash when dereferencing a deleted QRhi after native  
window is re-created  
* QTBUG-106598 MessageDialog won't open if its parent is a plain item  
* QTBUG-121022 Miscompilation of condition  
* QTBUG-119992 qt5 code is used for the qt6.6 documentation  
* QTBUG-121206 NO_LINT has not effect in qt_add_qml_module  
* QTBUG-121132 TableView: overlapping selections are cleared  
* QTBUG-120555 AnimatedImage: issues with loading web source  
* QTBUG-121139 qmlcachegen locks up in some situations  
* QTBUG-121035 QSettings::value("Theme") returns an empty QByteArray if  
beginGroup has been called  
* QTBUG-120479 qmldir file not placed with library with CMake Xcode  
generator  
* QTBUG-113558 QQuickWidget does not handle touch event via QML  
TapHandler correctly  
* QTBUG-65012 TapHandler: should not emit longPressed if the point is  
dragged  
* QTBUG-102846 [Windows] Restoring OpenGL context logic doesn't seem  
valid  
* QTBUG-114718 [Tests] tst_QQuickPopup fails  
* QTBUG-118163 Flaky race-condition in QuickTest when running  
tst_inputpanel built with ASAN  
* QTBUG-111873 qt_attributions.json files should be valid JSON  
* QTBUG-119663 extending qml tutorial cannot be found in the examples  
available in the qt creator  
* QTBUG-120262 Use SPDX-License-Ref in 3rdparty directories  
* QTBUG-108808 QQC2 BusyIndicator does not inherit visibility from  
parent consistently  
* QTBUG-117667 REG: TextEdit height gets stuck due to binding loops  
(forever) or anchor changes (temporarily until further resize event)  
* QTBUG-25489 QtQuick2 TextEdit emits unnecessary cursorRectangleChanged  
on all kinds of modifications  
  
### qtmultimedia  
* QTBUG-119083 MediaPlayer-Graphic&Multimedia There exists an empty  
selection when going through next and previous media  
* QTBUG-118699 The video playback is corrupted with Android native  
backend  
* QTBUG-118777 Emulation layer crash / cannot run project after adding  
two Audio Listeners  
* QTBUG-118309 QML Camera - Zoom not observed in Preview  
* QTBUG-116324 Request to implement thumbnail realization for multimedia  
FFMPEG backend  
* QTBUG-119089 QML Camera crashing on some devices  
* QTBUG-119445 Camera crash on image acquire on Android  
* QTBUG-117099 Video jerks when playing (Windows backend)  
* QTBUG-118734 Attribution scanner can not refer to files downloaded  
during provisioning  
* QTBUG-119471 Camera usage randomly crashes when the camera surface is  
destroyed with android backend  
* QTBUG-119236 Unexpected value for QML Camera.error enum  
* QTBUG-119693 [REG] 6.7.0 namespace build fails on Windows  
(MSVC&MinGW), multimedia  
* QTBUG-118573 Android tests on CI part 3/3 (screen/window capture)  
* QTBUG-118839 [DeclarativeCamera] The app crashes when unlocking the  
screen on Android  
* QTBUG-116519 [Reg 6.2 -> 6.5] Repeated QSoundEffect is broken on  
PulseAudio  
* QTBUG-113616 Android: Crash when mapping QVideoFrame object  
(minimize/restore)  
* QTBUG-118127 QMediaPlayer can not play sound again after the sound  
finished.  
* QTBUG-120449 Qt6 Multimedia WebAssembly Docs reference nonexistent  
method  
* QTBUG-118593 QML Camera ImageCapture Parameter not declared  
* QTBUG-113498 QVideoWidget in QDialog does not show / crashes (macOS)  
when shown twice  
* QTBUG-118572 Android tests on CI part 2/3 (audio)  
* QTBUG-118587 [WMF] Video position may exceed it's duration  
* QTBUG-120198 Process abruptly terminates while executing static  
destructor in Qt6Multimedia.dll  
* QTBUG-121455 QtMultimedia module fails Yocto CI build  
* QTBUG-116020 Audio from QMediaPlayer crackles and stutters on pause  
and resume  
* QTBUG-117407 Document limitations of QScreenCapture  
* QTBUG-118668 QTextToSpeech::synthesize under window does not get data  
* QTBUG-118571 Android tests on CI part 1/3 (camera & media  
capture/player)  
* QTBUG-117746 eglfs: Capturing the screen crashes  
* QTBUG-117878 Cannot capture screen from QQuickWidget  
* QTBUG-111045 QSoundEffect not playing  
* QTBUG-118099 Volume Discrepancies Between QMediaPlayer and  
QSoundEffect with ffmpeg  
* QTBUG-111815 Bumpy rendering of D3D11 textures  
* QTBUG-111459 Heavy jittering in video playback if animations are  
active  
* QTBUG-109213 Video flickering when there is a ParticleSystem component  
or playing some animation at same time  
  
### qttools  
* QTBUG-119555 [REG] Qt 6.6.1 breaks qt_add_translations  
* QTBUG-115166 qt_add_qml_module() causes non-Ninja generators to think  
that projects are never up-to-date  
* QTBUG-121226 qdoc extraimages.HTML not supported  
* QTBUG-62697 qhc files cannot be created in a reproducible way  
* QTBUG-120236 macOS: Qt Designer appears on a start on macOS as if it  
was broken  
* QTBUG-119051 With Linguist it seems only the last segment from the  
XLIFF is used as translated string.  
  
### qtdoc  
* QTBUG-118754 assertObjectType is triggered with a correct signal/slot  
connection on macOS  
* QTBUG-118672 [DocumentViewer] Cannot open PDF files using the app.  
* QTBUG-119286 Typos in Thermostat example  
* QTBUG-119294 Settings tab in Thermostat example behaves oddly  
* QTBUG-119320 Thermostat example buttons inactive  
* QTBUG-119290 Icon highlighting in Thermostat example is barely visible  
* QTBUG-119297 Room icons in Thermostat example not correct  
* QTBUG-117647 Audio track is not played when opening audio file after  
playing video file in media player example  
* QTBUG-117090 CMake docs: incorrect code example for  
qt_generate_qml_app_script  
* QTBUG-120372 Typo in the document  
* QTBUG-119458 Initializing with QQuickView is missing cmake instruction  
* QTBUG-120364 [6.7 beta1] Qt Dice demo crashes on Android devices  
* QTBUG-120471 Fix minor issues in stocqt  
* QTBUG-121165 Error in WebAssembly documentation  
* QTBUG-121524 [REG 6.6.1 -> 6.6.2] StocQt CMake error for Android  
* QTBUG-115373 Hangman Demo uses unsupported version of Google Play  
Billing Library  
* QTCREATORBUG-30077 TodoList example app does not work out of the box  
* QTBUG-120014 Dependency for libxcb-cursor0 since Qt 6.5 is not  
mentioned in the documentation.  
  
### qtpositioning  
* QTBUG-118739 The SatelliteInfo demo app is constantly crashing  
  
### qtconnectivity  
* QTBUG-119060 Read access violation when calling stop() during  
Bluetooth service discovery  
* QTBUG-119063 Segfault in Bluetooth module's Windows COM de-init  
* QTBUG-120410 NDEF Editor Example - Clicking on 'read tag' will erase  
existing records  
  
### qtwayland  
* QTBUG-119110 There are potential crash issues when some submenus are  
expanded.  
* QTBUG-118612 Large size cursor overlaps tooltips on linux  
* QTBUG-119136 qt creator does not restore to maximized state when  
minimized from maximized state  
* QTBUG-118890 QWaylandWindow::reset() mutex race/deadlock with  
QWaylandWindow::beginFrame()  
* QTBUG-120393 The link is ill formed in the document  
* QTBUG-120392 QWayland CSD window has unclickable area  
* QTBUG-120397 "output" property seems to be missing in WaylandQuickItem  
QML type documentation  
* QTBUG-120477 Overriding swap interval for Wayland EGL windows doesn't  
work  
* QTBUG-105703 QWaylandWindow::createDecoration() is called from  
multiple threads  
  
### qt3d  
* QTBUG-116494 Documentation for QCylinderMesh misses Detailed  
Description  
* QTBUG-77139 QText2DEntity isn't working with parent entity in  
constructor  
* QTBUG-100387 QText2DEntity does not create any geometry in certain  
cases  
* QTBUG-120964 delayed creation of QAttribute with parent in constructor  
causes crash  
* QTBUG-119659 Qt3D RHI - Uniform buffers not bound for compute shaders  
* QTBUG-119137 ERROR: AddressSanitizer: heap-use-after-free in  
tst_qmesh::checkSourceUpdate() in qt3d  
* QTBUG-69463 Camera view matrix computation unstable (regression)  
  
### qtimageformats  
* QTBUG-118797 ICNS format: QImageReader::setAllocationLimit() bug  
  
### qtserialbus  
* QTBUG-114397 QCanDbcFileParser will not parse signals with certain  
valid utf-8 encoded characters  
  
### qtwebengine  
* QTBUG-119525 error: field ‘responseHeaders’ has incomplete type  
‘QMultiMap<QByteArray, QByteArray>’  
* QTBUG-115357 qt 6.5.2 fails to build from source with system libpng  
(regression from 6.5.1)  
* QTBUG-119536 Lack of documentation regarding QPdfBookmarkModel's  
document property  
* QTBUG-118995 Dev tools not working  
* QTBUG-118398 QWebEngineView in QScrollArea is not scrollable  
* QTBUG-119776 PDF Multipage viewer example - Clicking on previous  
(upward arrow) will crash the example  
* QTBUG-104766 QtQuick.Pdf PdfDocument gets  
"QCoreApplication::postEvent: Unexpected null receiver" warning when  
instantiated standalone  
* QTBUG-120245 A crash occurred in C:\Users\qt\work\qt\qtwebengine_stand  
alone_tests\tests\auto\pdfquick\multipageview\tst_multipageview.exe  
* QTBUG-120446 Alternated item color in list is not always alternated  
* QTBUG-119722 [REG 5 → 6] Default context menu is missing icons  
* QTBUG-104767 Using PdfPageImage instead of Image on PDF file results  
in EXC_BAD_ACCESS (SIGSEGV)  
* QTBUG-118120 qtwebengine: build failure with x86_64h  
* QTBUG-119245 Qt Web Engine alert quotes not working  
* QTBUG-83338 Default implementations of javaScriptAlert/Confirm/Prompt  
treat message as rich text  
* QTBUG-119789 [Accessibility] Qt 6.5.3 cannot be built with the option  
' -no-feature-accessibility''.  
* QTBUG-119991 Unable to print at all if the first page of multi page  
document is not printed  
* QTBUG-118746 Japanese input on macOS regressed in Qt 6.5.3  
* QTBUG-114865 macos: Building QtWebEngine  with sanitizer enabled fails  
* QTBUG-116595 QtPfd build failure on 32-bit arm  
* QTBUG-119763 [REG 6.5.2?] Rare segfaults in  
QWebEngineDownloadItem::page()  
* QTBUG-111873 qt_attributions.json files should be valid JSON  
* QTBUG-119077 CMake deployment API does not deploy Qt Webengine  
* QTBUG-119878 [Reg 5.15->6.x] Crash and/or bad output when printing via  
Qt WebEngine's PDF plugin  
* QTBUG-120692 Cannot cross-compile webengine for x86_64  
  
### qtwebview  
* QTBUG-119356 WebViewSettings QML Type documentation of  
javaScriptEnabled property has a spelling mistake  
  
### qtcharts  
* QTBUG-119712 QChartView prevents parent QScrollView from receiving  
touch screen scroll events.  
* QTBUG-77403 Scrolling via trackpad does not work on Chart  
* QTBUG-119900 Deleting a visible QAbstractSeries with OpenGL enabled  
causes an error  
  
### qtvirtualkeyboard  
* QTBUG-118565 VirtualKeyboard documentation incorrect  
* QTBUG-120262 Use SPDX-License-Ref in 3rdparty directories  
  
### qtscxml  
* QTBUG-119562 StateMachine Documentation wrong  
* QTBUG-120576 The Note is duplicated for EventConnection::occurred  
* QTBUG-120262 Use SPDX-License-Ref in 3rdparty directories  
  
### qtremoteobjects  
* QTBUG-117379 [REG: 5->6] Enums with ENUM in the type name cause error  
in repc  
* QTBUG-120242 SubClassReplicaTest crashes  
  
### qtquicktimeline  
* QTBUG-119204 Not possible to exclude qtquicktimeline from the build  
  
### qtquick3d  
* QTBUG-119373 typo in the document  
* QTBUG-120579 The link to the Fog QML type is not correct  
* QTBUG-120431 QQ3DPhysics customshapes example looks different on  
opengl vs d3d11  
* QTBUG-120629 Baking Lightmap fails with msvc2019 kit  
* QTBUG-120424 Segmentation fault in the process of loading/unloading 3D  
objects  
* QTBUG-121390 Live Preview with a 3D project crashes on with Qt 6.6.1  
  
### qtmqtt  
* QTBUG-104478 Mqtt topic wildcard failure  
  
### qthttpserver  
* QTBUG-121219 QtHttpServer crashes when during GET of a larger content  
remote closes connection  
  
### qtquick3dphysics  
* QTBUG-120045 Application crashes in Qt Quick 3D Physics  
  
### qtgrpc  
* QTBUG-119227 Segfault assigning to a moved-out protobuf message  
* QTBUG-119475 examples/grpc/magic8ball/clientservice.cpp:26:14: error:  
invalid use of incomplete type ‘class QDebug’  
* QTBUG-119244 Non-packed repeated fields do not preserve the order when  
making roundtrip as unknown fields  
* QTBUG-120227 AddressSanitizer: heap-use-after-free in QtProtobufRepeat  
edTypesJsonDeserializationTest::RepeatedComplexMessageTest()  
* QTBUG-120432 Protobuf: Nested enums lack their protobuf and metatype  
regestering  
* QTBUG-116640 Protobuf generator doesn't support C++ keywords field  
names  
* QTBUG-120945 QGrpcChannelOptions::withMetadata  
* QTBUG-114079 qt_add_protobuf() macro should warn a user in case of  
adding proto files with the same name  
* QTBUG-120946 QGrpcHttp2Channel description refers to deprecated  
call/channel credentials  
  
### qtgraphs  
* QTBUG-121021 Qt Graphs module not marked as TP in the 6.6.x  
documentation  
  
### qtapplicationmanager (Commercial only)  
* QTBUG-119476 qtapplicationmanager/src/main-lib/main.cpp:16:12: fatal  
error: packagemanagerdbuscontextadaptor.h: No such file or directory  
* QTBUG-118743 Notification not dismissing when dismissOnAction is true  
  
### qtinterfaceframework (Commercial only)  
* QTBUG-119428 Enums in simulationData cannot be parsed correctly  
* QTBUG-122036 ModuleNotFoundError: No module named 'dataclasses'  
  
### qtvncserver (Commercial only)  
* QTBUG-119312 Cannot input text to an input field in a dialog  
* QTBUG-115515 Compiling Qt top level does not compiles Qt Vncserver  
  
Known Issues  
------------  
  
* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-6.6/supported-platforms.html  
* RTA reported issues from Qt 6.6  
https://bugreports.qt.io/issues/?filter=25128  
* See Qt 6.6  known issues from:  
https://wiki.qt.io/Qt_6.6_Known_Issues  
* Qt 6.6.2 Open issues in Jira:  
https://bugreports.qt.io/issues/?filter=25663
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Amir Masoud Abdol  
James Addison  
Laszlo Agocs  
Konsta Alajärvi  
Anu Aliyas  
Tim Angus  
Karolina Sofia Bang  
Mate Barany  
Vladimir Belyavsky  
Nicholas Bennett  
Eskil Abrahamsen Blomfeldt  
Tatiana Borisova  
Joerg Bornemann  
Rym Bouabid  
Assam Boudjelthia  
Aurélien Brooke  
Kai Uwe Broulik  
Michael Brüning  
Mike Chen  
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
Fabio Falsini  
David Faure  
Ilya Fedin  
GHENADY  
Samuel Gaist  
Florian de Gaulejac  
Zoltan Gera  
Joshua Goins  
Aleix Pol Gonzalez  
Julian Greilich  
Robert Griebl  
Mikko Gronoff  
Johannes Grunenberg  
Kaj Grönholm  
Richard Moe Gustavsen  
Lucie Gérard  
Kamil Hajdukiewicz  
Rob Hall  
Mikko Hallamaa  
Jøger Hansegård  
Inkamari Harjula  
Andre Hartmann  
Tero Heikkinen  
Jani Heikkinen  
Paul Heimann  
Christian Heimlich  
Alex Henrie  
Ulf Hermann  
Volker Hilsheimer  
Dominik Holland  
Samuli Hölttä  
Allan Sandfeld Jensen  
Maurice Kalinowski  
Jonas Karlsson  
Timothée Keller  
Friedemann Kleint  
Michal Klocek  
Lars Knoll  
Jarek Kobus  
Sze Howe Koh  
Jarkko Koivikko  
Tomi Korpipaa  
Jani Korteniemi  
Fabian Kosmale  
Volker Krause  
Mike Krus  
Santhosh Kumar  
Ghenady Kuznetsov  
Kai Köhne  
Inho Lee  
Paul Lemire  
Wladimir Leuschner  
Thorbjørn Lindeijer  
Thiago Macieira  
Ievgenii Meshcheriakov  
Leena Miettinen  
Safiyyah Moosa  
Bartlomiej Moskal  
Marc Mutz  
Martin Negyokru  
Andy Nichols  
Mårten Nordheim  
Dennis Oberst  
Samuli Piippo  
Timur Pocheptsov  
Lauri Pohjanheimo  
Joni Poikelin  
Cajus Pollmeier  
Alessandro Portale  
Lorn Potter  
Sakaria Pouke  
MohammadHossein Qanbari  
Liang Qi  
Matthias Rauter  
David Redondo  
Arno Rehn  
Topi Reinio  
Shawn Rutledge  
Ahmad Samir  
Lars Schmertmann  
Philip Schuchardt  
Carl Schwan  
Thomas Senyk  
Ws ShawnWoo  
Kristoffer Skau  
Ivan Solovev  
Axel Spoerl  
Patryk Stachniak  
Christian Strømme  
Tarja Sundqvist  
Audun Sutterud  
Lars Sutterud  
Tasuku Suzuki  
Jan Arve Sæther  
Morten Sørvig  
Nodir Temirkhodjaev  
Ivan Tkachenko  
Orkun Tokdemir  
Tuukka Turunen  
Paul Olav Tvete  
Esa Törmänen  
Peter Varga  
Doris Verria  
Tor Arne Vestbø  
Fabian Vogt  
Alexander Volkov  
Juha Vuolle  
Sune Vuorela  
Jaishree Vyas  
Michael Weghorn  
Bernd Weimer  
Edward Welbourne  
Paul Wicking  
Piotr Wiercinski  
Piotr Wierciński  
Jakub Wincenciak  
Milian Wolff  
Oliver Wolff  
Semih Yavuz  
Vlad Zahorodnii  
Yansheng Zhu  
shjiu  
Fredrik Ålund  
