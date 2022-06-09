Release note  
============  
  
Qt 6.3.1 release is a patch release made on the top of Qt 6.3.0.  
As a patch release, Qt 6.3.1 does not add any new functionality but provides  
bug fixes and other improvements and maintains both forward and backward  
compatibility (source and binary) with Qt 6.3.0.  

For detailed information about Qt 6.3, refer to the online documentation  
included in this distribution. The documentation is also available online:  
  
https://doc.qt.io/qt-6/index.html  
  
The Qt version 6.3 series is binary compatible with the 6.2.x series.  
Applications compiled for 6.2 will continue to run with 6.3.  
  
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
* 68c17c6fec FreeType: Load multiple font faces from the same file on  
macOS  
Fixed a bug where the macOS FreeType backend would fail to load font  
faces from font files containing multiple faces.  
  
* 8294fa4c35 Update bundled zlib to version 1.2.12  
zlib was updated to version 1.2.12.  
  
* 15919c5bda QBuffer: fix writing more than two GiB of data  
Fixed silent data truncation when writing more than two GiB at once on  
64-bit platforms.  
  
* 26fbc723e4 QPropertyBindingSourceLocation: fix BiC in source_location  
ctors  
(Windows only) Fixed a binary-incompatibility where source_location  
constructors were missing in the ABI.  
  
* 2a6bd54cfa QBuffer: fail early in seek() beyond QByteArray's max  
capacity  
Fixed silent data corruption on 32-bit platforms when seek() fails due  
to position > INT_MAX.  
  
* 5e1f5534dd XmlStringRef: fix length truncation  
Fixed several bugs regarding handling of documents larger than 2Gi  
characters on 64-bit platforms.  
  
* 99ad73ccb7 Upgrade PCRE2 to 10.40  
PCRE2 has been updated to 10.40.  
  
* 4f45c0c5d8 QTextStream: fix streaming of char16_t's  
Added op<<(char16_t).  
  
* c00b8652b5 Fix int/qsizetype mismatches in qstring.h  
Fixed result truncation mod INT_MAX in fromStdSstring(),  
fromStdU16string(), fromStdU32string(), and fromStdWstring().  
  
* 1001f1431e CMake: Pick first non-free team id for iOS Xcode projects  
A non-free Xcode team id is now preferred for project signing.  
  
* 04e87fc25e CMake: Automatically use Xcode generator in qt-cmake + iOS  
qt-cmake now defaults to using the Xcode generator when targeting iOS  
projects.  
  
* 9c809205a4 CMake: Ensure creation of a unique iOS bundle identifier  
The build system tries to create a unique bundle identifier based on  
the team id if no organization prefix can be retrieved from Xcode  
preferences.  
  
* 3c391f066c Update Harfbuzz to version 4.2.1  
Updated the Harfbuzz code included with Qt to version 4.2.1.  
  
* 2091b8d1bb Doc: Fix documentation for vulkan licenses  
Vulkan API Registry is available not only under MIT License, but also  
Apache License 2.0. Make this explicit in the license documentation.  
  
* 2c6ac19595 Support test-case selection based on global data tag  
When specifying what tests to run on a QtTest command-line, it is now  
possible to include a global data tag in the same way as a function-  
specific data tag or in combination with it. Thus if the test reports  
itself as tst_Class::function(global:local), command-line option  
function:global:local will select that specific test and function:global  
will run all data-rows for the function on the given global data tag.  
  
### qtdoc  
* 88e0b82c Remove "Generic Linux (x86, x64)" as supported desktop  
platform  
Linux x86 (Desktop) was removed from the list of officially supported  
platforms. We only provide binaries for Linux x64 since a while, and  
also do not actively test native builds on x86 Linux anymore.  
  
### qtwayland  
* 14bb5b8a Compositor: Re-enable touch events for Wayland clients  
Fixed a bug where multi-touch would not work with Qt Wayland  
Compositor.  
  
* 9b9effe1 client: Avoid protocol error with invalid min/max size  
Fixed an issue where setting an invalid minimum and maximum size on a  
window would cause some compositors to raise a protocol error.  
  
### qtimageformats  
* 79753ce Update bundled libtiff to version 4.4.0  
Bundled libtiff was updated to version 4.4.0  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-101869 tst_QOpenGL fails on webOS  
* QTBUG-101456 QTabBar::setTabTextColor does not change color when  
QPalette::Base background role is used  
* QTBUG-101916 Build Qt 6.3.0 beta2 / beta3 for Android fails only on  
Windows  
* QTBUG-100821 tst_qimagereader fails on Windows 11 21H2  
* QTBUG-98477 tst_QWidget::enterLeaveOnWindowShowHide is flaky in QtBase  
with Windows 11  
* QTBUG-69242 Android: tst_QTextDocument::task240325 fails  
* QTBUG-100470 Undetected test crashes on Android  
* QTBUG-100666 FreeType font backend fails to select font style when a  
single font file contains multiple font faces  
* QTBUG-75172 Wrong documentation for Qt::ItemDataRole expected types  
* QTBUG-101647 Selected item in QTreeWidget cannot be dragged when CTRL-  
key is pressed  
* QTBUG-101653 Windows/MinGW 9/Qt 6.2.3: Step into Qt source code does  
not work  
* QTBUG-88934 [Reg 5.15 -> 6] QFrame in the menu isn't drawing  
* QTBUG-101284 QPromise destructor doesn't transition to canceled state  
if it wasn't start()-ed  
* QTBUG-102041 Android multi-abi builds don't work if the Android  
ndk/sdk install path is different from the CI's one  
* QTBUG-101423 tst_QPlainTextEdit::ensureCursorVisibleOnInitialShow is  
crashing on Android  
* QTBUG-101321 tst_QDialog::dialogInGraphicsView crashes on Android  
* QTBUG-101996 Android Qt file system fails to communicate with some  
content provider app (like Google Drive)  
* QTBUG-101992 QDomDocument silently erases empty CDATA section  
* QTBUG-87422 tst_QAtomicInt::alignment fails on Android  
* QTBUG-87431 tst_QThreadStorage::crashOnExit fails on Android  
* QTBUG-87427 tst_QFileSystemModel::specialFiles fails on Android  
* QTBUG-87418 tst_QStringConverter::convertUtf8 fails on Android  
* QTBUG-87414 tst_QLocale::initTestCase fails on Android  
* QTBUG-99624 REG->6: Android: Fullscreen does not cover the navigation  
bar area  
* QTBUG-102064 binary_for_strip cannot be found on installed qtbase  
* QTBUG-88090 Installed CMake files reference the SOURCE TREE  
* QTBUG-53290 QWindowsPrintDevice::defaultPrintDeviceId() may crash,  
when no printers are installed  
* QTBUG-87385 tst_QNetworkProxyFactory::genericSystemProxy fails on  
Android  
* QTBUG-87390 tst_QScreen has tests  failing for Android  
* QTBUG-98369 [macOS] Qt internal warning when FontMetrics is used  
* QTBUG-99216 QMessageBox with Japanese characters gives "Missing font  
family" warning on macOS  
* QTBUG-101283 QThread does not indicate that an event dispatcher is  
created in start()  
* QTBUG-99020 -Wnull-pointer-subtraction when compiling  
qtdeclarative/src/qml/qml/ftw/qintrusivelist_p.h:244:69  
* QTBUG-95114 When accessibility is made active after the start up of an  
application then it will trigger an update of all existing controls to  
update roles and names  
* QTBUG-100997 Regression and UI Freeze (5.15 -> 6.2) in QTableView with  
Accessibility  
* QTBUG-97103 REG: 5.15.0->5.15.1: Under some circumstances the  
performance of an application on Windows when switching application  
focus  
* QTBUG-101307 tst_qbytearrayview fails to compile with ubsan  
* QTBUG-101758 REG[6.2.3->6.3] native QMessageBox crash on Android  
* QTBUG-97482 QPushButton with QMenu does not work on Qt6  
* QTBUG-102181 [Reg 6.2.3->6.2.4] Painting issues when scrolling in code  
editor  
* QTBUG-102171 On 64-bit platforms, QBuffer::write(ptr, 2GiB + 1)  
incorrectly reports success  
* QTBUG-101038 Wrong physical DPI  
* QTBUG-99484 Android - QML Camera freezes app  
* QTBUG-102202 [REG:6.2.3->6.2.4]: Cannot use c++latest with qmake and  
MSVC  
* QTBUG-102249 QSplitter: Handle moves in non-pressed state too  
* QTBUG-102274 QBuffer silent data corruption on seek() past INT_MAX  
(32-bit only)  
* QTBUG-102067 REG: QHash reserve endless loop with size < currently  
used one  
* QTBUG-96213 QProxyStyle::deleteLater() does not delete the QProxyStyle  
* QTBUG-102066 SDK version detection does not ignore stderr  
* QTBUG-70564 QT_NO_SIGNALS_SLOTS_KEYWORDS/QT_NO_KEYWORDS are  
undocumented  
* QTBUG-101361 Mac: File Dialog filters different category than selected  
* QTBUG-102199 QLocale::toDateTime asserts  
* QTBUG-101460 QTimeZone::displayName ignores locale on Android  
* QTBUG-102327 Address sanitizer caught heap-use-after-free in  
tst_QWidget::deleteWindowInCloseEvent  
* QTBUG-102358 Using system pcre2 fails when using pcre2 with cmake  
* QTBUG-87671 Android tests crashing with  
"java.lang.UnsatisfiedLinkError: dlopen failed: invalid ELF file"  
* QTBUG-101217 tst_qmessagebox has failing tests for Android  
* QTBUG-69216 Android: tst_QFontDatabase::condensedFontMatching fails  
* QTBUG-100312 androidtestrunner: A test with XPASS does not return  
error  
* QTBUG-101723 Configure failure with linux-clang-libc++  
* QTBUG-100297 QXdgDesktopPortalFileDialog::openPortal() does not set  
current_name  
* QTBUG-102431 QBENCHMARK triggers compiler warning  
* QTBUG-102246 windows arm64 broken QAtomicPointer ctor/copy/move  
* QTBUG-100135 40000 chips example - zoom in/out buttons do not work  
* QTBUG-102484 Race condition in QSemaphore  
* QTBUG-102718 Crash when restoring a QDockAreaLayout  
* QTBUG-102541 crash when restoring QMainWindow state when screen scale  
has changed  
* QTBUG-101347 QMainWindow Menu / actions sometimes not displayed when  
performing long operations  
* QTBUG-99810 [REG: 5.15.5->5.15.6] xcb: Dock widgets disappear if  
trying to float them from QMainWindow that contains native window  
* QTBUG-69515 Linux, WindowStaysOnTopHint does not work.  
* QTBUG-73485 Issue with Qt::WindowStaysOnTopHint  
* QTBUG-81341 Window won't receive events above Gnome Dock despite  
X11ByPassWindowManager + WindowsStaysOnTop is set  
* QTBUG-100173 tst_qquickwidget fails on Android  
* QTBUG-102005 [wasm] Canvas not painted initially  
* QTBUG-102744  QML items with Accessible properties set does not set  
properly for Android  
* QTBUG-102584 Drag and drop always assumes to have [NSWindow  
contentView] with drag drop API  
* QTBUG-102157 QDateTime asserts on MSVC 2019 / C++20  
* QTBUG-102334 QSettings / QDateTime incompatible when switching from  
Qt6 -> Qt5  
* QTBUG-38971 QtActivity did not call through to  
super.onConfigurationChanged() on orientation change (crash)  
* QTBUG-102298 Android: Switching navigation bar between buttons /  
gestures hides qml elements  
* QTBUG-100950 wasm: enter and leave events do not happen  
* QTBUG-99691 Starting QtService causes black screen  
* QTBUG-102628 Application will crash if setWindowsIcon with a big ICON  
* QTBUG-102952 tst_QNetworkReply::autoDeleteReplies* tests are flaky  
* QTBUG-102366 When filling a rect on a screen that has 150% scaling  
then it is possible that a line of pixels is not filled in  
* QTBUG-103000 [Reg: 5.15->6.3.0] Q_EMIT does not wait for slots to  
return on FreeBSD  
* QTBUG-100059 Objective-C usage can result in undefined behavior  
* QTBUG-99747 QDate::startOfDay( ) leads to assert in debug build  
* QTBUG-102782 QPushButton setEnabled(false) doesn't grey out button  
* QTBUG-102717 [REG Qt 6 -> Qt 6] QGraphicsView Artifacts  
* QTBUG-103085 QVersionNumber doesn't indicate its type in QDebug output  
* QTBUG-97533 QMenu pops up on wrong screen  
* QTBUG-103003 [Windows] Warning - Unable to open default EUDC font:  
"EUDC.TTE"  
* QTBUG-102820 [REG 5.15.2 => 6.2.4] Styled indicators not drawn in  
itemviews  
* QTBUG-102493 [REG 6.2.2 -> 6.2.3] Keyboard layout resets to English  
* QTBUG-102640 [REGRESSION] Keyboard layout not respected for *some* key  
combinations  
* QTBUG-95933 Using scanner input IRcode will result in an error when  
second character is uppercase  
* QTBUG-99136 QDockWidget not correctly parented/setup if dragged from  
another floating and tabified QDockWidget  
* QTBUG-101601 Wrong QScreen geometry for non-primary screens when  
scaling factors above 1  
* QTBUG-96212 The visibility of placeHolderText of the QPlainTextEdit is  
not reevaluated in the setter  
* QTBUG-102438 Drag/drop of "text/plain" does not work,  
QMimeData::text() returns an empty string  
* QTBUG-98785 Button menu pops up at wrong position on a  
QGraphicsProxyWidget  
* QTBUG-44096 QNetworkAuthenticationManager does not emit  
authenticationRequired when using NTLM  
* QTBUG-102083 Switching between app windows breaks IME  
* QTBUG-101278 Chinese text input issues on macOS 12.x  
* QTBUG-102607 macdeployqt: errors when producing a universal binary  
(universal binary)  
* QTBUG-101320 Apps targeting Android 12 or higher must explicitly  
declare the android:exported attribute for app components  
* QTBUG-102821 Global variable found in qeglfsx11integration.cpp  
* QTBUG-100039 QPlainTextEdit scrolls to cursor on alt-tab on ubuntu  
* QTCREATORBUG-26628 Switching from Creator to other window changes  
scroll position in editor  
* QTBUG-62185 QVersionNumber seems broken on -O1 and higher with g++  
* QTBUG-103009 QML performance regression when accessibility is active  
* QTBUG-75106 Entries in the QAccessiblePluginsHash should be removed  
when a QQuickWindow is deleted  
* QTBUG-103084 Hover events are not receivable in embedded QWindow  
(macOS)  
* QTBUG-102190 Calling showNormal after show does not make windows  
normal in WebAssembly  
* QTBUG-99335 Documentation for QtAndroidPrivate is wrong  
* QTBUG-103245 Configure fails when specifying -no-freetype  
* QTBUG-102960 iOS: input panel shows wrong suggestions  
* QTBUG-103370 REG: Qt does not build without Freetype  
* QTBUG-103356 [REG 6.3->6.4] Android arm64 and armv7 binary size  
increased  
* QTBUG-103002 linker error with qmake projects on static linux Qt6  
build  
* QTBUG-102489 segfault in qsql_mysql.cpp cleanup with icx  
* QTBUG-95468 XCB: Memory leak of QXcbScrollingDevicePrivate for a  
device that is not a mouse  
* QTBUG-103001 Implicit conversion loses integer  
* QTBUG-100351 [REG 5.12 -> 6.2] Pasting an image in Windows is not  
converted to a QImage correctly.  
* QTBUG-102866 [REG 5.12.3->6.2.1] Horizontal part of subcontrol-  
position of menu-indicator is ignored  
* QTBUG-102374 [REG:5.15.7->5.15.8]: repaint() on a widget makes  
QGraphicsOpacityEffect apply multiple times  
* QTBUG-102747 -DQT_GENERATE_WRAPPER_SCRIPTS_FOR_ALL_HOSTS=ON on windows  
generates windows line endings for unix script  
* QTBUG-100515 tst_qtextmarkdownwriter fails on QNX  
* QTBUG-100981 tst_QTextMarkdownWriter::fromHtml(preformats with  
embedded backticks) fails on Wayland  
* QTBUG-101031 markdown fenced code blocks end with unnecessary blank  
lines  
* QTBUG-94557 Menu causes touch failure  
* QTBUG-98519 [REG: 5.15.0->5.15.7] xcb: Synthesized mouse from touch  
gets stuck if receiving widget gets destroyed  
* QTBUG-102751 Can not receive touch event after the widget that  
WindowFlags is Qt::Popup is closed on ubuntu20.04  
* QTBUG-103706 Synthesized touch event not recognized with Widgets  
* QTBUG-103741 Signals carrying smart pointers to const QObject fail to  
compile  
* QTBUG-100833 Default iOS project to both iPhone and iPad deployment  
* QTBUG-93268 target_link_libraries does not work with a target name on  
iOS  
* QTBUG-95381 CMake library install target does not copy binaries on iOS  
* QTBUG-87198 Configuring example targeting iOS with CMake + Xcode  
generator fails  
* QTBUG-102999 QtConcurrent::blockingMapped behavior changed since Qt5  
if the output container does have a non-explit size c'tor  
* QTBUG-98003 InputMethod hides soon with ShiftModifier.  
* QTBUG-102758 Application always starts on wrong screen  
* QTBUG-102637 [REG 6.2.4 -> 6.3.0] No fake screen created without  
xrandr, Qt aborts  
* QTBUG-102134 QSplitter when hidden sets replaced widgets as hidden  
* QTBUG-103603 [REG 5.15.2-6.2.4] Broken country flag emoji in RTL text  
* QTBUG-99487 QHeaderView state incompatible between Qt5/6  
* QTBUG-103742 QVectorIterator & QMutableVectorIterator CamelCase  
headers missing  
* QTBUG-103605 qfilesystemmodel.cpp fails to compile on Windows with  
oneAPI icx using c++20  
* QTBUG-45582 Duplicated vtables due to inline virtual functions  
(probably all dtors)  
* QTBUG-97537 Fix failing line-break and word-break tests  
* QTBUG-103590 QKeySequenceEdit: not blocking quit on Mac  
* QTBUG-100870 QtTestLib's blacklisting doesn't take global data tags  
into account  
* QTBUG-102269 Test cases can't be called with a global data tag  
* QTBUG-87423 tst_QPlainTextEdit fails on Android  
* QTBUG-89402 tst_QPlainTextEdit fails test cases on Android  
* QTBUG-101771 [Reg 5.15 -> 6.2] Item ignores the initial size from a  
binding when implicit size is used with Behavior  
* QTBUG-101933 tst_quicktestmainwithsetup: QML module not found on webOS  
* QTBUG-101382 QtBase: Fix compiler warnings for QNX  
* QTBUG-101888 tst_QGraphicsProxyWidget failing tests  
* COIN-828 Fix build error message  
* QTBUG-87417 tst_QLineEdit fails on Android  
* QTBUG-100698 Fix BIC tests  
* QTBUG-99578 Global Functions are Undocumented  
* QTBUG-102034 Merely subclassing QHeaderView causes it to lose built-in  
functionality  
* QTBUG-87438 corelib plugin tests fail on Android  
* QTBUG-87668 tst_QWidget has many failing tests on Android  
* QTBUG-102095 tst_QFilesystemWatcher::watchDirectory() fails on macOS  
12 arm64  
* QTBUG-102096 tst_QFilesystemWatcher::signalsEmittedAfterFileMoved()  
fails on macOS  
* QTBUG-102121 QT_FEATURE_tslib is On for INTEGRITY in case Desktop has  
tslib installed  
* QTBUG-101461 qdoc does not parse ref-qualified member functions  
* QTBUG-101618 FAIL!  : tst_QSystemSemaphore::initialValue in QNX_710  
* QTBUG-102043 tst_openglwidget has crashing cases  
* QTBUG-100928 tst_QGlyphRun::mixedScripts fails on QNX  
* QTBUG-102253 tst_qwebengineview (Failed)  
* QTBUG-101274 QNX: Failing networks tests  
* QTBUG-95764 pure virtual call in QAccessibleQuickItem  
* QTBUG-102177 Regression: QProcess::readAllStandardError() crash on  
assert when MergedChannels is used  
* QTCREATORBUG-27196 Assert in qtcreator_processlauncher (On Windows,  
and Qt 6.3)  
* QTBUG-102258 tst_QCalendarWidget::showPrevNext() might crash on  
Android  
* QTBUG-102447 tst_drawingmodes failed  
* QTBUG-96353 Test run procedure and flaky detection  
* QTBUG-102880 tst_QLocalSocket::threadedConnection is flaky on Windows  
* QTBUG-103109 FAIL!  : tst_QNetworkReply::ioPostToHttpFromSocket in  
QNX_710  
* QTBUG-103055 FAIL!  : tst_QNetworkReply::ioGetFromHttpWithProxyAuth in  
QNX_710  
* QTBUG-103056 FAIL!  : tst_QTcpServer::serverAddress in QNX_710  
* QTBUG-99545 App crashes in function QQmlPropertyCache::property(int)  
const on ARM 64bit  
* QTBUG-72103 Conversion between QQuaternion and Euler angles has issues  
in special cases  
* QTBUG-100412 tst_qsrceen::grabWindow is flaky on Windows  
* QTBUG-99039 QVarLengthArray::push_back() is not strongly exception-  
safe  
* QTBUG-102594 [REG 5.15.6 -> 5.15.9] Many ANR issues by QtAccessibility  
* QTBUG-89819 tst_qmarkdown tests fail on QEMU ARMv7  
* QTBUG-99676 markdown (and html) import/export should not rely on use  
of a fixed-pitched font to remember a `monospace` span  
* QTBUG-103484 rich text gets converted to monospace in CI because  
QFontDatabase::GeneralFont is "Sans Serif" and is monospace  
* QTBUG-103309 Menus can be truncated (REG from 5.15.2)  
  
### qtdeclarative  
* QTBUG-100508 SEGFAULT Crash on  
QQuickOpenGLShaderEffectMaterial::updateTextures()  
* QTBUG-101386 TableView: a TapHandler / PointerHandler doesn't always  
detect a tap  
* QTBUG-101933 tst_quicktestmainwithsetup: QML module not found on webOS  
* QTBUG-102019 C++-compiled QML crashes on most type lookups  
* QTBUG-101700 DelegateModel: using for ... of loop in JS to iterate  
DelegateModel.groups attached property causes a crash  
* QTBUG-102018 tst_sanity cannot find test data on webOS  
* QTBUG-102022 tst_codegen_direct fails  
* QTBUG-100431 Crash in libQt5Qml V4 engine caused by wrong memory  
access  
* QTBUG-95726 [REG 5.15.2-6.2.0] MouseArea loses hover when cursor is  
inside of nested MouseArea  
* QTBUG-95398 MouseArea inside of SpinBox contentItem is blocking  
hovered property  
* QTBUG-90964 Examples missing cmake support (qml)  
* QTBUG-101771 [Reg 5.15 -> 6.2] Item ignores the initial size from a  
binding when implicit size is used with Behavior  
* QTBUG-101394 ItemDelegate blocks ScrollView hovered  
* QTBUG-100543 [REG 5.15.2-6.2.2] Control doesn't propagate hover to his  
parent  
* QTBUG-100149 [Regression] Parent Button is not hovered if a child  
button is hovered  
* QTBUG-98940 Button inside MouseArea does not pass mouse hover events  
* QTBUG-98850 [REG 6.1->6.2] HoverHandler doesn't get hoverevents, when  
a button is on the parent  
* QTBUG-102153 qmlcachegen does not properly handle ambiguous types  
* QTBUG-101811 Import alias leads to 'Type not found'  
* QTBUG-100018 tst_qmltc_manual fails on Android  
* QTBUG-102273 Qt quick compiler produces error in C++  
* QTBUG-102309 Typo in code generator leads to invalid code  
* QTBUG-102424 Doc: FileDialog doesn't mention that the native Android  
file dialog is supported  
* QTBUG-100253 tst_qquickpopup fails on Android  
* QTBUG-102415 tst_QQuickFolderDialogImpl::goUp() is flakey  
* QTBUG-102416 tst_qv4debugger fails on Android  
* QTBUG-102116 QML/C++ integration needs better cross-linking  
* QTBUG-99063 static top-level developer configuration fails in  
qtdeclarative doc snippet  
* QTBUG-100169 tst_qqmlextensionplugin fails on Android  
* QTBUG-100176 tst_qquickapplicationwindow crashes on Android  
* QTBUG-100991 Some tests crash on Android CI  
* QTBUG-102558 DialogButtonBox not regenerating layout on change of  
child Button width  
* QTBUG-102449 Native TextField: placeholderText does not respect  
horizontalAlignment  
* QTBUG-102729 Crash in QQmlBinding::evaluate()  
* QTBUG-102554 Segmentation fault when using QML_SINGLETON with  
QAbstractListModel  
* QTBUG-102598 Build fails in qtdeclarative with  
localstorageexample_Header_qml.cpp  
* QTBUG-101655 [Reg 6.1 -> 6.2] Error creating inline component in Qt  
6.2  
* QTBUG-102719 [Reg 5.15 -> 6.1] Not possible to use Loader inside  
inline component  
* QTBUG-102857 [Reg 6.2 -> 6.3] QML MediaDevices elements not displayed  
in ListView  
* QTBUG-95395 Code snippets for HoverHandler show TapHandler  
* QTBUG-101932 two HoverHandlers with different  
acceptedDevices/acceptedPointerTypes: cursorShape doesn't change  
accordingly  
* QTBUG-102646 QQuickFlickable wheel event not work correct for mouse  
device with pixel scroll wheel support for NoScrollPhase  
* QTBUG-103017 Qt.labs.platform Menu does not show icons  
* QTBUG-102454 rootContext()->setContextProperty assertion with frozen  
`QQmlPropertyMap`  
* QTBUG-84280 TextArea inside Flickable - cursor does not appear with  
LayoutMirroring.enabled  
* QTBUG-74028 Text inside MultiPointTouchArea has invalid coordinates on  
touch events  
* QTBUG-35995 Clicked signal not emitted on MouseArea when changing  
visibility and listening for doubleClicked  
* QTBUG-102158 Click signal not emitted in MouseArea after DoubleClicked  
is emitted and tab changed  
* QTBUG-102996 QML MouseArea containsPress / containsMouse / pressed are  
stuck when using multitouch  
* QTBUG-99604 TextArea and TextField don't use IBeamCursor when readOnly  
and selectByMouse are both true  
* QTBUG-100016 tst_qquickfolderlistmodel fails on Android  
* QTBUG-100560 Crash when closing SwipeDelegate in onCompleted handler  
* QTBUG-100339 qmllint does not find ApplicationWindow.window  
* QTBUG-102425 QML engine crashes if there are errors while setting up  
property bindings  
* QTBUG-102724 Popup doesn't redraw if content exceeds window size  
* QTBUG-102138 QML ComboBox: Customization example is broken  
* QTBUG-101628 Pinch gestures are not cancelled when pinch.accepted  
property is set to false on macOS.  
* QTBUG-83662 For MultiPointTouchArea with a child PinchArea multiple  
pressed signals for multiple touch points on mouse press  
* QTBUG-102446 tst_qquickfontloader_static Failed  
* QTBUG-83413 Text rendering glitches in combination with loader and  
elide  
* QTBUG-102339 Conan: multiple prefixes not supported when building e.g.  
examples  
* QTBUG-102793 [REG: 5.13->5.14] Bindings in delegates get triggered  
multiple times if delegate and/or model is changed  
* QTBUG-101401 Crash in QQmlObjectCreator::populateInstance  
* QTBUG-103224 [read-only] marking is missing from acceptableInput  
property of TextInput QML type in the documentation  
* QTBUG-99117 Custom style names not added to file selectors  
* QTBUG-78090 When active focus changes then it will set active focus on  
the new item first before it loses active focus on the other item  
* QTBUG-100177 tst_qquickheaderview fails on Android  
* QTBUG-101005 tst_qquickmenu and tst_qquickpopup tests fail to return  
test result  
* QTBUG-77335 tst_qquickfolderlistmodel::basicProperties fails on  
Android  
* QTBUG-100166 tst_qqmlenginedebugservice fails on Android  
* QTBUG-102765 qml type compiler: generated sources not unity buildable  
* QTBUG-102560 qml type compiler: codegen error with Gradients  
* QTBUG-102545 [REG 6.2 -> 6.3] Crash when appending a custom QObject to  
a ListModel  
* QTBUG-84375 Animation without 'from' value set and loops > 1 slows  
down at the end  
* QTBUG-75197 Editable ComboBox doesn't clear the selection  
* QTBUG-91461 GridView: resizing items causes view to reposition  
incorrectly  
* QTBUG-92868 GridView: the number of visible items is miscalculated  
* QTBUG-103361 qquickdeliveryagent.cpp error: unused parameter 'win'  
* QTBUG-102085 Extending QML example has no CMake documentation  
* QTBUG-77055 When pixelAligned is set to true in a Flickable, then it  
is possible that doing a flick away the boundaries (so you see a gap)  
will not cause it to snap back  
* QTBUG-99639 Rotated flickable decelerates in wrong direction  
* QTBUG-100257 tst_qquickdrawer fails on Android  
* QTBUG-100256 tst_qquickmenu fails on Android  
* QTBUG-102983 [Reg 6.2 -> 6.3] QML MediaDevices elements not displayed  
in ComboBox  
* QTBUG-102487 [REG 5.15.8 -> 5.15.9 + 6.2.3 -> 6.3.0] SwipeView shows  
last page on first page  
* QTBUG-51078 Use of Item obligatory in SwipeView?  
* QTBUG-51669 QQC2: SwipeView is not working as expected  
* QTBUG-99547 PathView item does not appear in certain circumstance  
* QTBUG-101768 matrix4x4 doc sample code  
* QTBUG-100014 tst_qqmlqt fails on Android  
* QTBUG-93649 Regression 5.15.3->6.0.0: Mouse Events not accepted on a  
MouseArea placed inside Popup::background  
* QTBUG-103522 The PreventStealing of mouseArea does not work properly  
in Flickable's(ListView) child item.  
* QTBUG-100161 DelegateModelGroup crashes on insert  
* QTBUG-103203 [REG 5.15.9 -> 6.0.4] Crash when dynamically inserting  
Item's to DelegateModelGroup  
* QTBUG-102120 tst_qquickmenubar fails on webOS  
* QTBUG-67512 Dialog is closed when releasing a drag outside of it  
* QTBUG-101488 FAIL!  : tst_QQuickFileDialogImpl::goUp in QNX_710  
* QTBUG-101662 Dialog Header/Footer cover over background instead of  
being inset  
* QTBUG-82043 tst_qquickmousearea::pressAndHold() is flakey on macOS  
* QTBUG-75202 tst_qquicklistview::contentHeightWithDelayRemove() is  
flaky on macOS 10.12  
* QTBUG-95940 tst_qquicktextinput paste-related tests are flaky on  
OpenSUSE  
* QTBUG-101327 FAIL!  : qquicklayouts::tst_gridlayout::compile in  
QNX_710  
* QTBUG-102345 QtQuick rectangle has one pixel spacing on Android  
* QTBUG-102147 Declared alias import not found  
* QTBUG-102447 tst_drawingmodes failed  
* QTBUG-100173 tst_qquickwidget fails on Android  
* QTBUG-102462 tst_qquickitem2 fails on Android  
* QTBUG-102384 JS Stack Overflow test fails on Android  
* QTBUG-96788 Javascript code causes segfault in iOS when using Qt debug  
library  
* QTBUG-102589  tst_SceneGraph::render fails on Android  
* QTBUG-102721 QQuickWindow::grabWindow() broken on Android  
* QTBUG-101342 tst_qmltc::listView() is flaky under QNX qemu and Android  
* QTBUG-45582 Duplicated vtables due to inline virtual functions  
(probably all dtors)  
* QTBUG-103200 A lot of unit tests in 6.3 branch are flaky  
* QTBUG-103094 tst_qquickshape tests fail on Android  
* QTBUG-102776 JIT is disabled on Android  
* QTBUG-102833 tst_qqmlenginecleanup::test_customModuleCleanup() broken  
on Android  
* QTBUG-102780 Vulkan-based rendering test flaky on Android  
* QTBUG-103310 tst_qqmlbinding::delayed() crashes on Android  
* QTBUG-103061 tst_FlickableInterop tests fail on Android  
* QTBUG-103065 tst_HoverHandler::movingItemWithHoverHandler() fails on  
Android  
* QTBUG-103096 tst_qquicktext fails on Android  
* QTBUG-103088 tst_qquickitemlayer tests fail on Android  
* QTBUG-103060 tst_qquicklayouts::Tests_GridLayout::test_spacings fails  
on Android  
* QTBUG-102330 "Creating C++ Plugins for QML" docs need to be updated  
with cmake use  
* QTBUG-103204 tst_cursor: webOS handles arrow cursor as bitmap cursor  
* QTBUG-103280 tst_qquickpixmapcache: webOS always tries to load from  
cache  
* QTBUG-100254 tst_qquickmenubar fails on Android  
* QTBUG-99545 App crashes in function QQmlPropertyCache::property(int)  
const on ARM 64bit  
* QTBUG-100073 Conan: leaf module options are missing -no-feature  
possibility  
* QTBUG-103257 tst_qquickcanvasitem crashes on Android  
* QTBUG-103258 tst_qquickrendercontrol fails on Android  
* QTBUG-103260 tst_qquickanimatedsprite fails on Android  
* QTBUG-103064 tst_DragHandler::touchDragMulti fails on Android  
* QTBUG-103256 tst_qquicktextinput fails on Android  
* QTBUG-103089  
tst_QQuickListView::QTBUG_48044_currentItemNotVisibleAfterTransition()  
fails on Android  
* QTBUG-103099 tst_qquickcanvasitem fails on Android  
* QTBUG-103080 tst_qquickdeliveryagent::passiveGrabberOrder() fails on  
Android  
* QTBUG-103098 tst_qquicktextedit fails on Android  
* QTBUG-103047 tst_qquickimageprovider::requestImage_sync fails on  
Android  
* QTBUG-103092 tests in tst_qquickmousearea fail on Android  
* QTBUG-103068 tst_PointHandler::tabletStylus() fails on Android  
* QTBUG-103066 tst_QQuickPinchHandler::scaleNativeGesture() fails on  
Android  
* QTBUG-103078 tst_qquickwindow fails on Android  
* QTBUG-103072 tst_TapHandler::gesturePolicyDragWithinBounds fails on  
Android  
* QTBUG-103076 tst_qquickanimatedimage::mirror_* tests fail on Android  
* QTBUG-102858 tst_quick_examples fails on Android  
* QTBUG-103077 tst_qquickborderimage tests fail on Android  
* QTBUG-103086 tst_qquickfocusscope::canvasFocus() fails on Android  
* QTBUG-103082 tst_qquickdrag tests fail on Android  
* QTBUG-103083 tst_QQuickDropArea::signalOrder() fails on Android  
* QTBUG-103044 tst_qmlcppcodegen on Android complains module  
"Qt.labs.folderlistmodel" is not installed  
* QTBUG-103743 tst_v4misc::nestingDepth in qtdeclarative crashes on  
Android in 6.3 branch  
* QTBUG-103560 qmlsc allows access to fractional indices of  
QQmlListProperty  
* QTBUG-103766 MouseArea onRelease event is not triggered after second  
finger touch'n'release  
* QTBUG-103205 SpinBox, no way to listen for text entered  
* QTBUG-103924 GCC 12: failure to build from source [<QtDeclarative>]  
* QTBUG-102403 QObject::objectName() leads to heap-use-after-free in  
tst_qquickanimations::cleanupWhenRenderThreadStops()  
  
### qtactiveqt  
* QTBUG-100145 ActiveQt example "outlook" build fails with a wall of  
errors: MSOUTL.cpp(346616): error C2062: type 'unknown-type' unexpected  
  
### qtmultimedia  
* QTBUG-99641 MacOS Monterey - QCamera stops render after a second  
* QTBUG-99361 Fix videoDimensions Test in Android  
* QTBUG-98262 Recording with audio fails on macOS 10.15 (Catalina)  
* QTBUG-99228 Qt-6.2.2 Example declarative-camera crash on Android 6.0.1  
* QTBUG-102962 Android: Update audio subsystem for SampleFormat::Float  
* QTBUG-103272 [Windows] Crash in MFPlayerSession::createSession()  
* QTBUG-102707 Several videos can't be played simultaneously with OpenGL  
RHI  
* QTBUG-102588 MediaMetaData.Duration not updated  
* QTBUG-60575 QtSpeech flite backend not working on Ubuntu Linux  
* QTBUG-103394 QMediaCaptureSession crashes with QCoreApplication  
* QTBUG-102843 Audioinput example: [5.15 -> 6.3] a lot of noise for the  
volume level  
* QTBUG-102969 After changing the position QMediaPlayer::setPosition in  
the pause state, a sound is heard  
* QTBUG-99094 Android tst_qaudiodecoderbackend test failed  
* QTBUG-103853 QMediaPlayer position error when rewind  
* QTBUG-100079 Android: fix QAndroidAudioDecoder issues  
* QTBUG-102029 Android camera preview broken in Qt 6.2.4 (regression)  
* QTBUG-102306 Fix qdoc warnings in mediaplayer.qdoc  
* QTBUG-103567 QML MediaPlayer fails to playback rtsp media properly.  
  
### qttools  
* QTBUG-93238 [REG 5.15.2 -> 6.0.3] Cannot build docs with static build  
of Qt  
* QTBUG-101319 Multiple qt_add_translations does not work in static  
projects  
* QTBUG-101461 qdoc does not parse ref-qualified member functions  
* QTBUG-101782 lrelease does not respect EXTRA_TRANSLATIONS in pro file.  
* QTBUG-102332 qdoc "documented multiple times" warning is bogus  
* QTBUG-102832 Qt Linguist incorrectly translates some language names  
* QTBUG-102387 qdoc: Fix inconsistency in breadcrump menu for sub-  
imports  
* QTBUG-48104 QUiLoader calls property setter twice while loading an ui-  
file  
* QTBUG-102088 Automatically generated "New QML Properties", "New QML  
Methods" miss type information  
* QTBUG-102342 List of all members misses inherited method with same  
name (but different signature)  
* QTBUG-103470 [iOS] CMake translation handling fails  
* QTBUG-100073 Conan: leaf module options are missing -no-feature  
possibility  
  
### qtdoc  
* QTBUG-101652 MessageDialog and FolderDialog links are wrong in What's  
New docs  
* QTBUG-99667 Document CMake API changes in 6.3 Overview  
* QTBUG-103466 Update "Implementing Atomic Operations" section  
* QTBUG-101370 Doc about Mac deployment lacks critical info for Qt 6  
* QTBUG-102268 There is no possibility to attach egl lib dependencies  
for Integrity  
* QTBUG-101320 Apps targeting Android 12 or higher must explicitly  
declare the android:exported attribute for app components  
* QTBUG-102304 Update documentation how to build iOS projects with cmake  
* QTBUG-103597 sgexamples qtdoc test fails on Android  
  
### qtpositioning  
* QTBUG-102836 Configure fails when trying to configure QtPositioning  
with -no-dbus  
* QTBUG-103807 QGeoAreaMonitorSource seg fault on exit on Android  
* QTBUG-103907 sccache: error: failed to store  
`mocs_compilation.cpp.obj` to cache  
* QTBUG-102994 Adding the Qt Bluetooth module produces a Makefile that  
looks for "user32.lib.lib" and "runtimeobject.lib.lib"  
  
### qtsensors  
* QTBUG-102256 Some examples not compiling on iOS: "duplicate symbol for  
architecture arm64"  
* QTBUG-102994 Adding the Qt Bluetooth module produces a Makefile that  
looks for "user32.lib.lib" and "runtimeobject.lib.lib"  
  
### qtconnectivity  
* QTBUG-101953 Windows BT COM initialization is incomplete  
* QTBUG-101984 Windows bluetooth socket not marked as unbuffered  
* QTBUG-102178 Test #10: tst_qbluetoothserver failed  
* QTBUG-102479 QBluetoothDeviceDiscoveryAgent should fail on macOS if  
provided with invalid address  
* QTBUG-70222 Qt  Bluetooth LE doesn't detect Battery services  
* QTBUG-102319 Android BT service discovery agent crash when stopped  
* QTBUG-102442 Bluetooth hostmode change Discoverable=>Connectable  
doesn't work on Android  
* QTBUG-102367 (potential BiC) Exported class QNdefMessage inherits from  
QList  
* QTBUG-103067 QBluetoothServer leaks RFCOMM and L2CAP Linux sockets  
* QTBUG-103826 Fix bluetooth deprecation warnings on macOS/iOS  
* QTBUG-102256 Some examples not compiling on iOS: "duplicate symbol for  
architecture arm64"  
* QTBUG-99578 Global Functions are Undocumented  
* QTBUG-102994 Adding the Qt Bluetooth module produces a Makefile that  
looks for "user32.lib.lib" and "runtimeobject.lib.lib"  
  
### qtwayland  
* QTBUG-102148 qtwayland contains invalid qt_attribution.json file  
* QTBUG-100148 Hover state of QCombobox has not been reset  
* QTBUG-102185 Fix remaining Qt Wayland Compositor documentation  
warnings  
* QTBUG-102379 Fix PresentationTime qml module documentation  
* QTBUG-102829 [Wayland] Multitouch is not working in Qt6  
* QTBUG-103378 Some return values are ignored, causing warnings  
* QTBUG-102626 Crash with invalid min/max sizes  
* QTBUG-103391 crash on start: The Wayland connection experienced a  
fatal error: Protocol error  
  
### qt3d  
* QTBUG-101595 [REG 6.2.4->6.3&4.0]qt3d/qardboard fails to compile  
* QTBUG-101949 A crash occurred in C:\Users\qt\work\qt\qt3d_standalone_t  
ests\tests\auto\render\scene2d\tst_scene2d.exe.  
* QTBUG-100073 Conan: leaf module options are missing -no-feature  
possibility  
* QTBUG-103218 [REG 6.3.0->6.3.1] qt3d examples not compiling on iOS  
  
### qtimageformats  
* QTBUG-103454 Null-dereference read in QICNSHandler  
* QTBUG-103337 Vulnerabilities in bundled libtiff version  
  
### qtserialbus  
* QTBUG-101351 QModbusClient::processResponse() is never called  
* QTBUG-100073 Conan: leaf module options are missing -no-feature  
possibility  
  
### qtwebsockets  
* QTBUG-102111 Custom http header on wss connection  
* QTBUG-101333 FAIL!  : tst_QWebSocketServer::tst_handleConnection in  
QNX_710  
* QTBUG-102713 tst_QWebSocketServer has failing tests on Android  
  
### qtwebchannel  
* QTBUG-101521 FAIL!  : qml::tst_bench::compile in QNX_710  
  
### qtwebengine  
* QTBUG-101697 QtPDF's plugins.qmltypes is not installed  
* QTBUG-101935 FAIL!  : tst_QWebEnginePage::pasteImage() Compared values  
are not the same  
* QTBUG-94963 QWebEngineLoadingInfo::errorDomain() returns  
WebEngineError::InternalErrorDomain when there is no error  
* QTBUG-100806 QMimeData::html() returns undesirable meta data  
* QTBUG-92539 Weird behavior when pasting certain HTML into element with  
contentEditable attribute set  
* QTBUG-101724 Application crash when trigger  
QWebEnginePage::triggerAction( QWebEnginePage::InspectElement )  
* QTBUG-102743 Version getters are undocumented  
* QTBUG-101201 Failed to compile xkb_symbols with multiple layout  
* QTBUG-100799 Dictionaries not found in spellchecker bundle dir on  
macOS  
* QTBUG-100300 cups-config: No such file - build error in  
cups_config_helper.py  
* QTBUG-103217 QtWebEngineQuick form select field popups do not react on  
touch press  
* QTBUG-79254 QWebEngineView couldn't handle touch events for html  
select's popup menus  
* QTBUG-103372 [REG 6.2 -> 6.3] QT_QUICK_BACKEND=software segfaults with  
QtWebEngine in QSGSoftwareRenderableNode::update  
* QTBUG-101030 The zoom factor is reset every time QtWebEngine loads a  
new website  
* QTBUG-103778 [REG 5.15 -> 6.2] ERR_NETWORK_ACCESS_DENIED when clicking  
link from local page  
* QTBUG-103579 Qt PDF: Static build fails on macOS  
* QTBUG-104049 Undefined symbols for architecture x86_64:  
"content::getSandboxPath()"  
* QTBUG-100435 Cannot enable webrtc-pipewire feature  
* QTBUG-102192 Navigation on drop broken  
* QTBUG-102323 cmake seems to treat builddir as a regex and fails if  
builddir contains quantor characters (+)  
* QTBUG-100073 Conan: leaf module options are missing -no-feature  
possibility  
* QTBUG-103859 qt-testrunner.py ERROR: exception:ParseError no element  
found  
  
### qtwebview  
* QTBUG-102801 qtwebview setAndDeleteCookie tests crash on Android  
* QTBUG-101520 FAIL!  : tst_QQuickWebView::stopEnabledAfterLoadStarted  
in QNX_710  
* QTBUG-101487 FAIL!  : tst_QWebView::load in QNX_710  
* QTBUG-102712 qtwebview tests fail on Android  
  
### qtcharts  
* QTBUG-102140 error C2220: the following warning is treated as an  
errorchartpresenter.cpp(141): warning C4996:  
'QScopedPointer<ChartAxisElement,QScopedPointerDeleter<T>>::take  
* QTBUG-102286 [REG 5.15 -> 6.2] QTChartView zoom area does not work in  
x direction  
* QTBUG-101945 Changing to QValueAxis::TicksDynamic on horizontal axes  
moves ticks to the opposite side  
* QTBUG-101517 FAIL!  : example::tst_barcategoryaxis::compile in QNX_710  
* QTBUG-102723 tst_qpieslice and tst_qpieseries fail on Android  
* QTBUG-102722 tst_QAreaSeries has test failures on Android  
* QTBUG-102725 charts_qml (tst_qml) fails on Android  
* QTBUG-100073 Conan: leaf module options are missing -no-feature  
possibility  
  
### qtdatavis3d  
* QTBUG-102735 ERROR: The test executable CRASHed uncontrollably!  
* QTBUG-101513 FAIL!  : qmltest::tst_category::compile in QNX_710  
* QTBUG-102256 Some examples not compiling on iOS: "duplicate symbol for  
architecture arm64"  
  
### qtvirtualkeyboard  
* QTBUG-101536 FAIL!  : styles::tst_styles::compile in QNX_710  
* QTBUG-101512 FAIL!  : inputpanel::tst_inputpanel::compile in QNX_710  
* QTBUG-102756 qtvirtualkeyboard tests fail on Android  
  
### qtscxml  
* QTBUG-102252 tst_qqmlstatemachine (Failed)  
* QTBUG-102284 Qt Scxml examples fail to link when using a static Qt  
* QTBUG-103396 error: reference to non-static member function must be  
called  
* QTBUG-99545 App crashes in function QQmlPropertyCache::property(int)  
const on ARM 64bit  
* QTBUG-101343 FAIL!  : tst_statemachineqml::tst_anonymousstate::compile  
in QNX_710  
* QTBUG-100073 Conan: leaf module options are missing -no-feature  
possibility  
  
### qtremoteobjects  
* QTBUG-102852 tst_usertypes::remoteCompositeType fails on Android  
* QTBUG-101384 QtRO: Fix compiler warnings for QNX  
* QTBUG-101336 FAIL!  : ModelreplicaTest::basicFunctions in QNX_710  
  
### qtquick3d  
* QTBUG-101373 Item2D node rendered indefinitey on threaded render loop,  
blocks updates on basic render loop  
* QTBUG-101882 Particle shapes don't support reparenting  
* QTBUG-102293 QML profiler shows texture load for each frame for  
Quick3D  
* QTBUG-102390 Qt.quaternion() always has precedence over eulerAngles  
even in derived components  
* QTBUG-102389 Issues with relative source urls in imported QML  
components  
* QTBUG-102423 Balsam tool fails to import GLTF model with many  
materials  
* QTBUG-102850 Parallax Correction issue when the probe is not  
positioned at the center  
* QTBUG-102023 Incorrect shadows from SpotLight and PointLight  
* QDS-6761 Model Picking is not working correctly  
* QTBUG-102711 tst_MultiWindow crashes on Android  
* QTBUG-102710 tst_RenderControl fails on Android  
* QTBUG-99948 Fix enum/enum arithmetic in Qt  
  
### qt5compat  
* QTBUG-102254 tst_qtextcodec (Failed)  
* QTBUG-99545 App crashes in function QQmlPropertyCache::property(int)  
const on ARM 64bit  
  
### qtopcua  
* QTBUG-102149 Invalid license file reference in  
./src/3rdparty/open62541/qt_attribution.json  
* QTBUG-100007 qtopcua fails to integrate due to flaky  
opcua::SubscriptionsTest  
  
### qtlanguageserver  
* QTBUG-103924 GCC 12: failure to build from source [<QtDeclarative>]  
  
Known Issues  
------------  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Mike Achtelik  
Laszlo Agocs  
Dimitrios Apostolou  
Soheil Armin  
Viktor Arvidsson  
Mahmoud Badri  
Vladimir Belyavsky  
Nicholas Bennett  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
Sören Bohn  
Tatiana Borisova  
Joerg Bornemann  
Assam Boudjelthia  
Florian Bruhin  
Michael Brüning  
Marco Bubke  
Andreas Buhr  
Kirill Burtsev  
Jungi Byun  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Noah Davis  
Anton Demchenko  
Alexey Edelev  
Oliver Eftevaag  
Christian Ehrlicher  
Iikka Eklund  
Hatem ElKharashy  
Andreas Eliasson  
David Faure  
Ilya Fedin  
Pekka Gehör  
Roman Genkhel  
Christophe Giboudeaux  
Maximilian Goldstein  
Andrei Golubev  
Richard Moe Gustavsen  
Lucie Gérard  
Tang Haixiang  
Heikki Halmet  
Andreas Hartmetz  
Jani Heikkinen  
Miikka Heikkinen  
Karsten Heimrich  
Ulf Hermann  
Volker Hilsheimer  
Allan Sandfeld Jensen  
Tim Jenssen  
Hu Jialun  
Janne Juntunen  
Friedemann Kleint  
André Klitzing  
Michal Klocek  
Lars Knoll  
Jarek Kobus  
Sze Howe Koh  
Jarkko Koivikko  
Łukasz Korbel  
Tomi Korpipaa  
Jani Korteniemi  
Janne Koskinen  
Fabian Kosmale  
Mike Krus  
Simeon Kuran  
Sona Kurazyan  
Jonas Kvinge  
Kai Köhne  
Inho Lee  
Paul Lemire  
Qiang Li  
Jasper Limbago  
Moody Liu  
Robert Löhning  
Thiago Macieira  
Thorbjørn Lund Martsum  
Ievgenii Meshcheriakov  
Samuel Mira  
Marc Mutz  
Tommi Mänttäri  
Antti Määttä  
Martin Negyokru  
Andy Nichols  
Yuya Nishihara  
Mårten Nordheim  
Tadej Novak  
Sukyoung Oh  
Bumjoon Park  
Pasi Petäjäjärvi  
Samuli Piippo  
Timur Pocheptsov  
Joni Poikelin  
Lorn Potter  
Liang Qi  
Martin Reboredo  
Topi Reinio  
André de la Rocha  
Rafael Roquetto  
Johannes Rosenqvist  
Elias Rudberg  
Shawn Rutledge  
Toni Saario  
Luca Di Sera  
Dmitry Shachnev  
Ye ShanShan  
Andy Shaw  
Venugopal Shivashankar  
David Skoland  
Ivan Solovev  
Axel Spoerl  
Michael Spork  
Piotr Srebrny  
Christian Strømme  
Tasuku Suzuki  
Morten Sørvig  
Morten Johan Sørvig  
Nodir Temirkhodjaev  
Paul Olav Tvete  
Peter Varga  
Doris Verria  
Tor Arne Vestbø  
Alexander Volkov  
Ville Voutilainen  
Juha Vuolle  
Jaishree Vyas  
Stefan Wastl  
Edward Welbourne  
Niklas Wenzel  
Oliver Wolff  
YiFang Xiao  
Lu YaNing  
JiDe Zhang  
Yuhang Zhao  
Volodymyr Zibarov  
