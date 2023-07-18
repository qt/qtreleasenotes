Release note  
============  
Qt 6.2.5 release is a patch release made on the top of Qt 6.2.4. As a patch  
release, Qt 6.2.5 does not add any new functionality but provides bug fixes  
and other improvements.  
  
For detailed information about Qt, see the Qt 6.2 online documentation:  
https://doc.qt.io/qt-6.2/.  
  
Important Changes  
-----------------  
  
### qtbase  
* 4e71b29013 QStringConverter: fix move special member functions of  
State class  
Fixed a potential data corruption in the move constructor and move-  
assignment operator on 32-bit platforms.  
  
* 47e3429483 CMake: Make configure less verbose by default  
The configure output verbosity of non developer-builds of Qt is now  
reduced by default. Pass "-- --log-level=STATUS" to configure to make it  
verbose again.  
  
* 32f6db7b46 Update bundled libjpeg-turbo to version 2.1.3  
libjpeg-turbo was updated to version 2.1.3  
  
* 51f1d4e400 qDecodeDataUrl(): treat ";base64" marker as case-  
insensitive  
Now recognizes the ";base64" marker in "data:" URLs case-insensitively.  
  
* 09c7f37ce3 QMetaType: add a missing check for null d_ptr  
Fixed a bug that would cause QMetaType::compare() and  
QVariant::compare() to crash on invalid meta types and variants.  
  
* cadd1cb0ef QByteArray: fix isUpper/isLower  
The semantics of QByteArray::isLower() and QByteArray::isUpper() have  
been changed. Now lowercase (resp. uppercase) byte arrays are allowed to  
contain any character; a byte array is considered lowercase (resp.  
uppercase) if it's equal to its own toLower() (resp. toUpper()) folding.  
For instance, the "abc123" byte array is now considered to be lowercase.  
Previously, the isLower() (resp. isUpper()) functions checked whether  
the byte array only contained ASCII lowercase (resp. uppercase)  
characters, and was at least 1 character long. This had the side effect  
that byte array containing ASCII non-letters (e.g. numbers, symbols,  
etc.) were not lowercase nor uppercase.  
  
* 714bb09d55 FreeType: Load multiple font faces from the same file on  
macOS  
Fixed a bug where the macOS FreeType backend would fail to load font  
faces from font files containing multiple faces.  
  
* 59b0a70bb4 Update bundled zlib to version 1.2.12  
zlib was updated to version 1.2.12.  
  
* fb19f77aa3 QBuffer: fix writing more than two GiB of data  
Fixed silent data truncation when writing more than two GiB at once on  
64-bit platforms.  
  
* ceb236954a QBuffer: fail early in seek() beyond QByteArray's max  
capacity  
Fixed silent data corruption on 32-bit platforms when seek() fails due  
to position > INT_MAX.  
  
* c9b0131210 XmlStringRef: fix length truncation  
Fixed several bugs regarding handling of documents larger than 2Gi  
characters on 64-bit platforms.  
  
* 2c76d223b8 Fix int/qsizetype mismatches in qstring.h  
Fixed result truncation mod INT_MAX in fromStdSstring(),  
fromStdU16string(), fromStdU32string(), and fromStdWstring().  
  
* a0b974c290 CMake: Pick first non-free team id for iOS Xcode projects  
A non-free Xcode team id is now preferred for project signing.  
  
* d0a9b53023 CMake: Ensure creation of a unique iOS bundle identifier  
The build system tries to create a unique bundle identifier based on  
the team id if no organization prefix can be retrieved from Xcode  
preferences.  
  
* 0b33a57221 Upgrade PCRE2 to 10.40  
PCRE2 has been updated to 10.40.  
  
* 6da29b51ad Doc: Fix documentation for vulkan licenses  
Vulkan API Registry is available not only under MIT License, but also  
Apache License 2.0. Make this explicit in the license documentation.  
  
* 8ac3ddb9ba QCOMPARE/QVERIFY: fix huge pessimisation in QTestResult  
Optimized successful QCOMPARE and QVERIFY for an up to 2x speedup.  
  
* 9d5c935cff CMake: Automatically use Xcode generator in qt-cmake + iOS  
qt-cmake now defaults to using the Xcode generator when targeting iOS  
projects.  
  
* 71be528e92 CoreText: Fix fonts with synthetic stretch  
Fixed a bug where synthetically stretched fonts would get the wrong  
advances and sometimes glyphs would be clipped.  
  
* 2a885f1e77 Fix font rendering when Qt is configured with -no-harfbuzz  
Fixed font layouts when Qt was configured without Harfbuzz.  
  
### qtdeclarative  
* 6be1936d9f QQmlDebug: reliably print the debugger warning  
The warning about enabled debuggers is now printed when at least one  
translation unit in the final executable requests it, independent of the  
order in which translation units are linked/initialized.  
  
### qttools  
* 8c60d2d28 lupdate: Allow multiple specifiers after method signature  
lupdate does not trip anymore over tr() calls in methods with multiple  
specifiers. For example "QString MyClass::foo() const noexcept" now gets  
the correct context.  
  
### qtdoc  
* 44ea92ff Remove "Generic Linux (x86, x64)" as supported desktop  
platform  
Linux x86 (Desktop) was removed from the list of officially supported  
platforms. We only provide binaries for Linux x64 since a while, and  
also do not actively test native builds on x86 Linux anymore.  
  
### qtwayland  
* 1d7b2aca client: Avoid protocol error with invalid min/max size  
Fixed an issue where setting an invalid minimum and maximum size on a  
window would cause some compositors to raise a protocol error.  
  
* 0bf7f657 Compositor: Re-enable touch events for Wayland clients  
Fixed a bug where multi-touch would not work with Qt Wayland  
Compositor.  
  
### qtimageformats  
* 850c7f0 Update bundled libwebp to version 1.2.2  
Update bundled libwebp to version 1.2.2  
  
* c5953ed Update bundled libtiff to version 4.4.0  
Bundled libtiff was updated to version 4.4.0  
  
### qtserialbus  
* 191d1b9f Make pduFromStream work on big endian (again)  
Fix reading from stream on big endian systems  
  
### qtwebengine  
* 5f723fe74 Fix QWebEngineQuick namespace for webenginequick module  
Use namespace QtWebEngineQuick QtWebEngine::initialize() is now  
QtWebEnigneQuick::initialize()  
  
* 2ad450018 Add API for favicon database  
image:/favicon/ URLs now can be used to access icon database.  
  
* d0ff107c0 Make default profile off the record  
Default profile is off-the-record Off-the-record profile can have  
registered protocol handlers.  
  
* 8f7a386a5 Remove deprecated useforglobalcertificateverification  
(Q)WebEngineSettings::useForGlobalCertificateVerification has been  
removed.  
  
* 13254e795 WebEngineNavigationRequest: add accept/reject and deprecate  
setAction  
setAction(action) is deprecated in favor of new accept/reject methods  
  
* b7634f470 Disable kAllowContentInitiatedDataUrlNavigations  
Page content may no longer navigate to data-urls, if this is needed we  
recommend using custom-url schemes instead or force old behavior using  
--enable-features=AllowContentInitiatedDataUrlNavigations, though the  
feature switch may be removed in any later update.  
  
* e90ed198b Add charset parsing to custom scheme handler's content type  
Charset is now explicitly parsed from provided contentType  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-100559 wasm: Linking commands too long for Windows  
* QTBUG-100651 Unable to follow HTTP/2 redirects  
* QTBUG-101172 Android help from configure-cmake-mapping.md seems  
outdated (or wrong)?  
* QTBUG-87401 tst_QFormLayout::wrapping fails on Android  
* QTBUG-84466 startSystemMove and startSystemResize does not enable aero  
snap on windows with frameless window.  
* QTBUG-87674 qaccessibility fails on Android  
* QTBUG-101020 tst_QPlugin::scanInvalidPlugin fails on QNX  
* QTBUG-69064 Android: tst_QFrame::testPainting fails  
* QTBUG-100537 Can not build Qt 6 with cmake when preferring package  
configuration  
* QTBUG-101306 enum-enum warning in qxcbwindow.cpp is genuiune  
* QTBUG-87389 tst_QDialog::snapToDefaultButton fails on Android  
* QTBUG-93505 Unable to retrieve the swiped Filedialog  
* QTBUG-101028 argv passed to Android apps is not sufficiently  
terminated  
* QTBUG-101286 [Regression] QNetworkReply::finished() is not emitted if  
an error occurs.  
* QTBUG-101411 QT_WARNING_DISABLE_* macros do not work under QCC (8.3.0)  
* QTBUG-101381 QtScxml: Fix compiler warnings for QNX  
* QTBUG-101415 QtPositioning: Fix compiler warnings for QNX  
* QTBUG-101384 QtRO: Fix compiler warnings for QNX  
* QTBUG-101382 QtBase: Fix compiler warnings for QNX  
* QTBUG-100795 QWeakPointer d pointer is private  
* QTBUG-28379 QFileDialog: aliases to folders disabled  
* QTBUG-52472 Undefined Behaviour in qsimpledrag.cpp line 207  
* QTBUG-45045 SIGFPE in QQuickMenu  
* QTBUG-67576 QAbstractSocket::setSocketOption() has no effect if called  
before QAbstractSocket::connectToHost()  
* QTBUG-101581 Crash when zooming invalid image  
* QTBUG-101551 wasm multiple "use after free" in  
QNetworkReplyWasmImplPrivate::doSendRequest  
* QTBUG-100154 deprecated-declarations warning in  
examples/network/secureudpserver/server.cpp  
* QTBUG-100670 QDockWidgetGroupWindow effectively sets new dockarea  
permissions on qdockwidget  
* QTBUG-98755 QIconEngine::IconNameHook disappeared  
* QTBUG-94366 Backslash is converted to double forward slash in  
configure on Windows  
* QTBUG-101620 QOpenGLWidget does not update when content changed while  
its hidden  
* QTBUG-87407 tst_QTableView has failing tests for Android  
* QTBUG-99548 Qt6 CMake target compile options propagation (CUDA)  
* QTCREATORBUG-24600 some clicks in call stack don't register  
* QTBUG-99640 Reg->6: QByteArray::append(const char *str, qsizetype len)  
crashes if len < 0  
* QTBUG-99960 A crash when comparing two null QVariants  
* QTBUG-100107 QByteArray::isLower() is completely different from  
QString::isLower() , ditto isUpper()  
* QTBUG-101474 setClipRect() after setClipRegion() call doesn't change  
clipping region  
* QTBUG-101745 Running qmake on iOS build fails on macOS 12.3 Monterey  
* QTBUG-89545 CMake: on macOS (w/ framework build) the module includes  
the binary  
* QTBUG-101718 [REG 6.3.0beta2->beta3] quick3d/principledmaterial not  
launching on macOS  
* QTBUG-101775 Don't add framework directories as include paths  
* QTBUG-99472 "Pick Screen Color" button in QColorDialog doesn't scan  
secondary screen colors in Windows  
* QTBUG-100693 WebAssembly (WASM) MEMORY control fixes  
* QTBUG-101651 Random crashes in QGraphicsScene  
* QTBUG-101897 The 'movie' example should only build if  
'QT_FEATURE_movie' is available  
* QTBUG-100802 [REG 6.2.2->6.2.3]Checkable QPushButton does not visually  
display checked state when toggled on macOS  
* QTBUG-101456 QTabBar::setTabTextColor does not change color when  
QPalette::Base background role is used  
* QTBUG-101916 Build Qt 6.3.0 beta2 / beta3 for Android fails only on  
Windows  
* QTBUG-101776 qhelpgenerator installed to $prefix/bin location instead  
of $prefix/libexec  
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
* QTBUG-101423 tst_QPlainTextEdit::ensureCursorVisibleOnInitialShow is  
crashing on Android  
* QTBUG-101321 tst_QDialog::dialogInGraphicsView crashes on Android  
* QTBUG-101996 Android Qt file system fails to communicate with some  
content provider app (like Google Drive)  
* QTBUG-101992 QDomDocument silently erases empty CDATA section  
* QTBUG-87422 tst_QAtomicInt::alignment fails on Android  
* QTBUG-87427 tst_QFileSystemModel::specialFiles fails on Android  
* QTBUG-87431 tst_QThreadStorage::crashOnExit fails on Android  
* QTBUG-87418 tst_QStringConverter::convertUtf8 fails on Android  
* QTBUG-102064 binary_for_strip cannot be found on installed qtbase  
* QTBUG-70564 QT_NO_SIGNALS_SLOTS_KEYWORDS/QT_NO_KEYWORDS are  
undocumented  
* QTBUG-102066 SDK version detection does not ignore stderr  
* QTBUG-53290 QWindowsPrintDevice::defaultPrintDeviceId() may crash,  
when no printers are installed  
* QTBUG-87414 tst_QLocale::initTestCase fails on Android  
* QTBUG-99624 REG->6: Android: Fullscreen does not cover the navigation  
bar area  
* QTBUG-99020 -Wnull-pointer-subtraction when compiling  
qtdeclarative/src/qml/qml/ftw/qintrusivelist_p.h:244:69  
* QTBUG-87385 tst_QNetworkProxyFactory::genericSystemProxy fails on  
Android  
* QTBUG-101283 QThread does not indicate that an event dispatcher is  
created in start()  
* QTBUG-98369 [macOS] Qt internal warning when FontMetrics is used  
* QTBUG-99216 QMessageBox with Japanese characters gives "Missing font  
family" warning on macOS  
* QTBUG-95114 When accessibility is made active after the start up of an  
application then it will trigger an update of all existing controls to  
update roles and names  
* QTBUG-100997 Regression and UI Freeze (5.15 -> 6.2) in QTableView with  
Accessibility  
* QTBUG-97103 REG: 5.15.0->5.15.1: Under some circumstances the  
performance of an application on Windows when switching application  
focus  
* QTBUG-101307 tst_qbytearrayview fails to compile with ubsan  
* QTBUG-99747 QDate::startOfDay( ) leads to assert in debug build  
* QTBUG-102181 [Reg 6.2.3->6.2.4] Painting issues when scrolling in code  
editor  
* QTBUG-102171 On 64-bit platforms, QBuffer::write(ptr, 2GiB + 1)  
incorrectly reports success  
* QTBUG-99484 Android - QML Camera freezes app  
* QTBUG-101758 REG[6.2.3->6.3] native QMessageBox crash on Android  
* QTBUG-97482 Android: QPushButton with QMenu does not work on Qt6  
* QTBUG-102202 [REG:6.2.3->6.2.4]: Cannot use c++latest with qmake and  
MSVC  
* QTBUG-102249 QSplitter: Handle moves in non-pressed state too  
* QTBUG-87671 Android tests crashing with  
"java.lang.UnsatisfiedLinkError: dlopen failed: invalid ELF file"  
* QTBUG-101217 tst_qmessagebox has failing tests for Android  
* QTBUG-102274 QBuffer silent data corruption on seek() past INT_MAX  
(32-bit only)  
* QTBUG-102067 REG: QHash reserve endless loop with size < currently  
used one  
* QTBUG-101361 Mac: File Dialog filters different category than selected  
* QTBUG-69216 Android: tst_QFontDatabase::condensedFontMatching fails  
* QTBUG-100312 androidtestrunner: A test with XPASS does not return  
error  
* QTBUG-102366 When filling a rect on a screen that has 150% scaling  
then it is possible that a line of pixels is not filled in  
* QTBUG-102199 QLocale::toDateTime asserts  
* QTBUG-102358 Using system pcre2 fails when using pcre2 with cmake  
* QTBUG-87390 tst_QScreen has tests  failing for Android  
* QTBUG-101460 QTimeZone::displayName ignores locale on Android  
* QTBUG-101723 Configure failure with linux-clang-libc++  
* QTBUG-100173 tst_qquickwidget fails on Android  
* QTBUG-102246 windows arm64 broken QAtomicPointer ctor/copy/move  
* QTBUG-102484 Race condition in QSemaphore  
* QTBUG-100297 QXdgDesktopPortalFileDialog::openPortal() does not set  
current_name  
* QTBUG-100039 QPlainTextEdit scrolls to cursor on alt-tab on ubuntu  
* QTCREATORBUG-26628 Switching from Creator to other window changes  
scroll position in editor  
* QTBUG-102952 tst_QNetworkReply::autoDeleteReplies* tests are flaky  
* QTBUG-103356 [REG 6.3->6.4] Android arm64 and armv7 binary size  
increased  
* QTBUG-103245 Configure fails when specifying -no-freetype  
* QTBUG-103002 linker error with qmake projects on static linux Qt6  
build  
* QTBUG-100059 Objective-C usage can result in undefined behavior  
* QTBUG-102717 [REG Qt 6 -> Qt 6] QGraphicsView Artifacts  
* QTBUG-97533 QMenu pops up on wrong screen  
* QTBUG-103009 QML performance regression when accessibility is active  
* QTBUG-75106 Entries in the QAccessiblePluginsHash should be removed  
when a QQuickWindow is deleted  
* QTBUG-99335 Documentation for QtAndroidPrivate is wrong  
* QTBUG-103370 REG: Qt does not build without Freetype  
* QTBUG-103001 Implicit conversion loses integer  
* QTBUG-38971 QtActivity did not call through to  
super.onConfigurationChanged() on orientation change (crash)  
* QTBUG-102298 Android: Switching navigation bar between buttons /  
gestures hides qml elements  
* QTBUG-97813 Namespace with "enum" at its begining not being properly  
handled  
* QTBUG-102493 [REG 6.2.2 -> 6.2.3] Keyboard layout resets to English  
* QTBUG-102640 [REGRESSION] Keyboard layout not respected for *some* key  
combinations  
* QTBUG-95933 Using scanner input IRcode will result in an error when  
second character is uppercase  
* QTBUG-100351 [REG 5.12 -> 6.2] Pasting an image in Windows is not  
converted to a QImage correctly.  
* QTBUG-102866 [REG 5.12.3->6.2.1] Horizontal part of subcontrol-  
position of menu-indicator is ignored  
* QTBUG-102374 [REG:5.15.7->5.15.8]: repaint() on a widget makes  
QGraphicsOpacityEffect apply multiple times  
* QTBUG-95468 XCB: Memory leak of QXcbScrollingDevicePrivate for a  
device that is not a mouse  
* QTBUG-94557 Menu causes touch failure  
* QTBUG-98519 [REG: 5.15.0->5.15.7] xcb: Synthesized mouse from touch  
gets stuck if receiving widget gets destroyed  
* QTBUG-102751 Can not receive touch event after the widget that  
WindowFlags is Qt::Popup is closed on ubuntu20.04  
* QTBUG-103706 Synthesized touch event not recognized with Widgets  
* QTBUG-98003 InputMethod hides soon with ShiftModifier.  
* QTBUG-102999 QtConcurrent::blockingMapped behavior changed since Qt5  
if the output container does have a non-explit size c'tor  
* QTBUG-103741 Signals carrying smart pointers to const QObject fail to  
compile  
* QTBUG-103576 [REG] Broken Qt::TextAlignmentRole  
* QTBUG-93268 target_link_libraries does not work with a target name on  
iOS  
* QTBUG-95381 CMake library install target does not copy binaries on iOS  
* QTBUG-87198 Configuring example targeting iOS with CMake + Xcode  
generator fails  
* QTBUG-102747 -DQT_GENERATE_WRAPPER_SCRIPTS_FOR_ALL_HOSTS=ON on windows  
generates windows line endings for unix script  
* QTBUG-102134 QSplitter when hidden sets replaced widgets as hidden  
* QTBUG-103742 QVectorIterator & QMutableVectorIterator CamelCase  
headers missing  
* QTBUG-103745 QPainter::drawText method truncates inputs  
* QTBUG-102083 Switching between app windows breaks IME  
* QTBUG-101278 Chinese text input issues on macOS 12.x  
* QTBUG-98785 Button menu pops up at wrong position on a  
QGraphicsProxyWidget  
* QTBUG-102584 Drag and drop always assumes to have [NSWindow  
contentView] with drag drop API  
* QTBUG-103605 qfilesystemmodel.cpp fails to compile on Windows with  
oneAPI icx using c++20  
* QTBUG-103590 QKeySequenceEdit: not blocking quit on Mac  
* QTBUG-102744  QML items with Accessible properties set does not set  
properly for Android  
* QTBUG-102327 Address sanitizer caught heap-use-after-free in  
tst_QWidget::deleteWindowInCloseEvent  
* QTBUG-102718 Crash when restoring a QDockAreaLayout  
* QTBUG-102541 crash when restoring QMainWindow state when screen scale  
has changed  
* QTBUG-101347 QMainWindow Menu / actions sometimes not displayed when  
performing long operations  
* QTBUG-99810 [REG: 5.15.5->5.15.6] xcb: Dock widgets disappear if  
trying to float them from QMainWindow that contains native window  
* QTBUG-69515 Linux, WindowStaysOnTopHint does not work.  
* QTBUG-102438 Drag/drop of "text/plain" does not work,  
QMimeData::text() returns an empty string  
* QTBUG-101284 QPromise destructor doesn't transition to canceled state  
if it wasn't start()-ed  
* QTBUG-101320 Apps targeting Android 12 or higher must explicitly  
declare the android:exported attribute for app components  
* QTBUG-102821 Global variable found in qeglfsx11integration.cpp  
* QTBUG-99691 Starting QtService causes black screen  
* QTBUG-103000 [Reg: 5.15->6.3.0] Q_EMIT does not wait for slots to  
return on FreeBSD  
* QTBUG-102782 QPushButton setEnabled(false) doesn't grey out button  
* QTBUG-102334 QSettings / QDateTime incompatible when switching from  
Qt6 -> Qt5  
* QTBUG-103852 QDir fails for paths of length over 260 characters  
* QTBUG-88934 [Reg 5.15 -> 6] QFrame in the menu isn't drawing  
* QTBUG-102960 iOS: input panel shows wrong suggestions  
* QTBUG-73485 Issue with Qt::WindowStaysOnTopHint  
* QTBUG-81341 Window won't receive events above Gnome Dock despite  
X11ByPassWindowManager + WindowsStaysOnTop is set  
* QTBUG-102628 Application will crash if setWindowsIcon with a big ICON  
* QTBUG-97537 Fix failing line-break and word-break tests  
* QTBUG-100833 Default iOS project to both iPhone and iPad deployment  
* QTBUG-104056 Conan: qmlimportscanner: No such file or directory  
* QTBUG-88519 androiddeployqt doesn't know about Conan's build path  
* QTBUG-89588 androiddeployqt fails with error from qmlimportscanner if  
qtdeclarative is not installed  
* QTBUG-103836 Fusion menu text with mnemonic clipped on Windows  
* QTBUG-94481 [REG 5.15.2 -> 6.1.1] Ellipsis in the worst possible place  
* QTBUG-103894 Configuring fails on Manjaro Linux  
* QTBUG-103455 Settings don't work with content:// URL on Android  
* QTBUG-103568 Android 13: Warnings when starting qt apps  
* QTBUG-104123 "configure -no-pkg-config" doesn't turn off pkg-config  
* QTBUG-95957 Scaled pixmap with ellipse clipping leaves lines in output  
* QTBUG-100329 Clipping glitches when painting with fractional scaling  
* QTBUG-100343 MDI subwindows leave artifacts when moving/resizing with  
fractional scaling  
* QTBUG-104003 QTabBar/QTabWidget crashes when closing last tab and  
there are hidden tabs  
* QTBUG-98417 Bundling translation file of plist does not work with  
XCode 13  
* QTBUG-49704 QLoggingCategory::installFilter crashes with the code from  
documentation  
* QTBUG-103775 Downstream crash when bad index passed to insert methods  
of QBoxLayout  
* QTBUG-100188 Page layout settings are reset when QPrintDialog is shown  
if there is no printer installed on macOS  
* QTBUG-103007 Resetting a QComboBox custom model doesn't emit  
currentIndexChanged or currentTextChanged  
* QTBUG-102395 QMainWindow::restoreState corrupts relation between  
toolbars layout item  
* QTBUG-104231 tst_QVulkan fails with Ubuntu 22.04 due to broken Mesa  
lavapipe included in the distro  
* QTBUG-91896 QTableView span gets confused with logical indexes when  
columns are moved  
* QTBUG-85474 QGraphicsScene::clearSelection() may leave internal state  
inconsistent  
* QTBUG-103497 [iOS] CMake handling qt_add_big_resources() fails  
* QTBUG-104362 QDomImplementation::DropInvalidChars strips emoji and  
other non-BMP characters  
* QTBUG-86790 Mingw Qt provides debug libraries in the wrong folder  
* QTBUG-103838 QFontMetrics::horizontalAdvance() does not seems to give  
correct value  
* QTBUG-100361 No font rendering at all when configured with -no-  
harfbuzz  
* PYSIDE-1750 QMouseEvent.pos marked as deprecated in source but not in  
docs  
* QTBUG-104085 QJsonValue::toObject(const QJsonObject &defaultValue) and  
QJsonValue::toArray(const QJsonArray &defaultValue) parse empty default  
values incorrectly  
* QTBUG-104396 qmake projects try to link to static qt libraries with  
hardcoded CI paths (no such file or directory)  
* QTBUG-85109 QPainter::drawImage draws images in different places  
depending on image format  
* QTBUG-53661 QDom internalSubset is never set  
* QTBUG-104708 qmake projects try to link to static qt libraries with  
hardcoded CI paths part 2  
* QTBUG-98475 tst_QWindow::modalWindowEnterEventOnHide fails in QtBase  
with Windows 11  
* QTBUG-99295 The tool "Qt6::sdpscanner" was not found  
* QTBUG-87397 tst_QGraphicsView fails on Android  
* QTBUG-100412 tst_qsrceen::grabWindow is flaky on Windows  
* QTBUG-101332 FAIL!  : tst_QXmlStream::initTestCase in QNX_710  
* QTBUG-101194 tst_QFileDialog has failing tests for Android  
* QTBUG-87424 tst_QMenu fails on Android  
* QTBUG-100948 tst_QFontDatabase::systemFixedFont() fails on QNX  
* QTBUG-100917 tst_QImageReader::setScaledClipRect() SVG/SVGZ fails on  
Wayland  
* QTBUG-100918 tst_QOpenGL::bufferMapRange() fails on Wayland  
* QTBUG-100982 tst_QStaticText fails on Wayland  
* QTBUG-93955 Material.System does not work on Ubuntu (Gnome)  
* QTBUG-94459 Android reports incorrect screen size after rotation  
* QTBUG-97009 Broken rendering on Qt 6.2 Android arm64-v8a  
* QTBUG-101519 FAIL!  :  
tst_QTouchEvent::multiPointRawEventTranslationOnTouchPad in  
Windows_11_21H2  
* QTBUG-101590 FAIL!  : tst_QSystemSemaphore::basicProcesses in QNX_710  
* QTBUG-101571 FAIL!  : tst_QWidget::enterLeaveOnWindowShowHide in  
Windows_11_21H2  
* QTBUG-89402 tst_QPlainTextEdit fails test cases on Android  
* QTBUG-87396 tst_toolsupport::offsets fails on Android  
* QTBUG-87423 tst_QPlainTextEdit fails on Android  
* COIN-828 Fix build error message  
* QTBUG-101771 [Reg 5.15 -> 6.2] Item ignores the initial size from a  
binding when implicit size is used with Behavior  
* QTBUG-101888 tst_QGraphicsProxyWidget failing tests  
* QTBUG-87417 tst_QLineEdit fails on Android  
* QTBUG-100698 Fix BIC tests  
* QTBUG-99948 Fix enum/enum arithmetic in Qt  
* QTBUG-87438 corelib plugin tests fail on Android  
* QTBUG-102034 Merely subclassing QHeaderView causes it to lose built-in  
functionality  
* QTBUG-87668 tst_QWidget has many failing tests on Android  
* QTBUG-102095 tst_QFilesystemWatcher::watchDirectory() fails on macOS  
12 arm64  
* QTBUG-102096 tst_QFilesystemWatcher::signalsEmittedAfterFileMoved()  
fails on macOS  
* QTBUG-102043 tst_openglwidget has crashing cases  
* QTBUG-102258 tst_QCalendarWidget::showPrevNext() might crash on  
Android  
* QTBUG-100928 tst_QGlyphRun::mixedScripts fails on QNX  
* QTBUG-100515 tst_qtextmarkdownwriter fails on QNX  
* QTBUG-102253 tst_qwebengineview (Failed)  
* QTBUG-102121 QT_FEATURE_tslib is On for INTEGRITY in case Desktop has  
tslib installed  
* QTBUG-101274 QNX: Failing networks tests  
* QTBUG-95764 pure virtual call in QAccessibleQuickItem  
* QTBUG-102447 tst_drawingmodes failed  
* QTBUG-96513 CI: qmake examples should not be built from tainted source  
tree  
* QTBUG-102880 tst_QLocalSocket::threadedConnection is flaky on Windows  
* QTBUG-96353 Test run procedure and flaky detection  
* QTBUG-103056 FAIL!  : tst_QTcpServer::serverAddress in QNX_710  
* QTBUG-99545 App crashes in function QQmlPropertyCache::property(int)  
const on ARM 64bit  
* QTBUG-102594 [REG 5.15.6 -> 5.15.9] Many ANR issues by QtAccessibility  
* QTBUG-89819 tst_qmarkdown tests fail on QEMU ARMv7  
* QTBUG-99676 markdown (and html) import/export should not rely on use  
of a fixed-pitched font to remember a `monospace` span  
* QTBUG-103484 rich text gets converted to monospace in CI because  
QFontDatabase::GeneralFont is "Sans Serif" and is monospace  
* QTBUG-103309 Menus can be truncated (REG from 5.15.2)  
* QTBUG-72103 Conversion between QQuaternion and Euler angles has issues  
in special cases  
* QTBUG-103923 GCC 12: failure to build from source [<QtBase>]  
* QTBUG-102021 QCocoaScreen::UpdateScreens crash  
* QTBUG-104128 top-level configure is still verbose in a non-developer  
build  
* QTBUG-103470 [iOS] CMake translation handling fails  
* QTBUG-104012 QDateTime constructor performance regression when year is  
below epoch  
* QTBUG-103723 [iOS] CMake shader handling fails  
* QTBUG-87137 tst_QApplication::sendEventsOnProcessEvents() failed on  
Ubuntu 20.04/22.04 and RHEL 9  
* QTBUG-68860 tst_QGlyphRun::mixedScripts autotest fails on Ubuntu 18.04  
and QEMU builds  
* QTBUG-68865 tst_QMenuBar::check_menuPosition autotest fails on Ubuntu  
18.04  
* QTBUG-84248 tst_QFont::defaultFamily fails  
* QTBUG-104450 qmake: it's impossible to configure some compiler and  
linker options in the generated vcxproj  
* QTBUG-102595 Builds can't find the projects qml modules  
* QTBUG-101008 Using Text.NativeRendering results in characters drawn  
too close to each other with fractional scale factors  
* QTBUG-108523 tst_QMetaType::typeNameNormalization fails with macOS  
  
### qtdeclarative  
* QTBUG-98115 qmllint crashes when id is assigned to string  
* QTBUG-100338 qmllint warns about all members of model index  
* QTBUG-101155 qml binding to a QML_EXTENDED property doesn't update  
when changed signal emitted  
* QTBUG-67950 Crash when changing Loader source inside a Repeater when  
the model changes  
* QTBUG-99436 Quick Drag and Drop Tiles example broken in Qt 6  
* QTBUG-98857 [REG 6.2.0->6.2.1] QML: Wrong item position after  
drag&drop  
* QTBUG-98181 Importing directory into namespace triggers assert  
* QTBUG-92006 Fractional font size is displayed incorrectly  
* QTBUG-77371 Accessibility: Multiple Text items with Accessible  
properties grouped together on Android  
* QTBUG-101186 [REG 6.1.3 -> 6.2.0] AnchorAnimation causes Rectangle  
width and height to be zero  
* QTBUG-98011 qmltc crashes due to insufficient import locations in a  
specific Qt build configuration  
* QTBUG-101163 Qmltc error prevents qtdeclarative from compiling  
* QTBUG-101349 qmlsc and qmlcachegen miscompile draganddrop/grid example  
* QTBUG-101383 QtDeclarative: Fix compiler warnings for QNX  
* QTBUG-101402 There doesn't appear to be a list of text-field  
validators  
* QTBUG-61971 ComboBox wrong touch behavior  
* QTBUG-100508 SEGFAULT Crash on  
QQuickOpenGLShaderEffectMaterial::updateTextures()  
* QTBUG-101386 TableView: a TapHandler / PointerHandler doesn't always  
detect a tap  
* QTBUG-100355 [REG 6.2.2 - 6.2.3] Custom image providers do not scale  
on High DPI displays  
* QTBUG-101573 Popup is not closed when MouseArea on ToolTip is pressed  
* QTBUG-101739 tst_qmlcompiler_manual::cppBinding fails on Android  
* QTBUG-100018 tst_qmltc_manual fails on Android  
* QTBUG-101738 tst_QQmlDebugTranslationService::initTestCase fails on  
macOS 12/arm 64  
* QTBUG-94391 FileDialog unwanted uri suffix for Android11 SAF  
* QTBUG-101771 [Reg 5.15 -> 6.2] Item ignores the initial size from a  
binding when implicit size is used with Behavior  
* QTBUG-101700 DelegateModel: using for ... of loop in JS to iterate  
DelegateModel.groups attached property causes a crash  
* QTBUG-102022 tst_codegen_direct fails  
* QTBUG-100431 Crash in libQt5Qml V4 engine caused by wrong memory  
access  
* QTBUG-95726 [REG 5.15.2-6.2.0] MouseArea loses hover when cursor is  
inside of nested MouseArea  
* QTBUG-95398 MouseArea inside of SpinBox contentItem is blocking  
hovered property  
* QTBUG-101394 ItemDelegate blocks ScrollView hovered  
* QTBUG-100543 [REG 5.15.2-6.2.2] Control doesn't propagate hover to his  
parent  
* QTBUG-100149 [Regression] Parent Button is not hovered if a child  
button is hovered  
* QTBUG-98940 Button inside MouseArea does not pass mouse hover events  
* QTBUG-98850 [REG 6.1->6.2] HoverHandler doesn't get hoverevents, when  
a button is on the parent  
* QTBUG-102153 qmlcachegen does not properly handle ambiguous types  
* QTBUG-102424 Doc: FileDialog doesn't mention that the native Android  
file dialog is supported  
* QTBUG-100253 tst_qquickpopup fails on Android  
* QTBUG-102416 tst_qv4debugger fails on Android  
* QTBUG-102446 tst_qquickfontloader_static Failed  
* QTBUG-99063 static top-level developer configuration fails in  
qtdeclarative doc snippet  
* QTBUG-100177 tst_qquickheaderview fails on Android  
* QTBUG-101005 tst_qquickmenu and tst_qquickpopup tests fail to return  
test result  
* QTBUG-77335 tst_qquickfolderlistmodel::basicProperties fails on  
Android  
* QTBUG-101655 [Reg 6.1 -> 6.2] Error creating inline component in Qt  
6.2  
* QTBUG-100166 tst_qqmlenginedebugservice fails on Android  
* QTBUG-102646 QQuickFlickable wheel event not work correct for mouse  
device with pixel scroll wheel support for NoScrollPhase  
* QTBUG-84280 TextArea inside Flickable - cursor does not appear with  
LayoutMirroring.enabled  
* QTBUG-77055 When pixelAligned is set to true in a Flickable, then it  
is possible that doing a flick away the boundaries (so you see a gap)  
will not cause it to snap back  
* QTBUG-100560 Crash when closing SwipeDelegate in onCompleted handler  
* QTBUG-35995 Clicked signal not emitted on MouseArea when changing  
visibility and listening for doubleClicked  
* QTBUG-102158 Click signal not emitted in MouseArea after DoubleClicked  
is emitted and tab changed  
* QTBUG-102793 [REG: 5.13->5.14] Bindings in delegates get triggered  
multiple times if delegate and/or model is changed  
* QTBUG-101628 Pinch gestures are not cancelled when pinch.accepted  
property is set to false on macOS.  
* QTBUG-67512 Dialog is closed when releasing a drag outside of it  
* QTBUG-78090 When active focus changes then it will set active focus on  
the new item first before it loses active focus on the other item  
* QTBUG-87190 Application freezes when there is no control to focus next  
* QTBUG-99117 Custom style names not added to file selectors  
* QTBUG-103224 [read-only] marking is missing from acceptableInput  
property of TextInput QML type in the documentation  
* QTBUG-75197 Editable ComboBox doesn't clear the selection  
* QTBUG-91461 GridView: resizing items causes view to reposition  
incorrectly  
* QTBUG-92868 GridView: the number of visible items is miscalculated  
* QTBUG-102487 [REG 5.15.8 -> 5.15.9 + 6.2.3 -> 6.3.0] SwipeView shows  
last page on first page  
* QTBUG-51078 Use of Item obligatory in SwipeView?  
* QTBUG-51669 QQC2: SwipeView is not working as expected  
* QTBUG-99547 PathView item does not appear in certain circumstance  
* QTBUG-84375 Animation without 'from' value set and loops > 1 slows  
down at the end  
* QTBUG-93649 Regression 5.15.3->6.0.0: Mouse Events not accepted on a  
MouseArea placed inside Popup::background  
* QTBUG-103522 The PreventStealing of mouseArea does not work properly  
in Flickable's(ListView) child item.  
* QTBUG-102339 Conan: multiple prefixes not supported when building e.g.  
examples  
* QTBUG-100176 tst_qquickapplicationwindow crashes on Android  
* QTBUG-100991 Some tests crash on Android CI  
* QTBUG-102449 Native TextField: placeholderText does not respect  
horizontalAlignment  
* QTBUG-102724 Popup doesn't redraw if content exceeds window size  
* QTBUG-100257 tst_qquickdrawer fails on Android  
* QTBUG-102558 DialogButtonBox not regenerating layout on change of  
child Button width  
* QTBUG-100256 tst_qquickmenu fails on Android  
* QTBUG-102425 QML engine crashes if there are errors while setting up  
property bindings  
* QTBUG-102138 QML ComboBox: Customization example is broken  
* QTBUG-102729 Crash in QQmlBinding::evaluate()  
* QTBUG-102454 rootContext()->setContextProperty assertion with frozen  
`QQmlPropertyMap`  
* QTBUG-100016 tst_qquickfolderlistmodel fails on Android  
* QTBUG-95395 Code snippets for HoverHandler show TapHandler  
* QTBUG-101932 two HoverHandlers with different  
acceptedDevices/acceptedPointerTypes: cursorShape doesn't change  
accordingly  
* QTBUG-103017 Qt.labs.platform Menu does not show icons  
* QTBUG-102944 [Reg 5.15 -> 6.2] Relative QML import does not work from  
Android assets  
* QTBUG-103924 GCC 12: failure to build from source [<QtDeclarative>]  
* QTBUG-99639 Rotated flickable decelerates in wrong direction  
* QTBUG-103187 Reconfiguration is slow due to qmlimportscanner  
* QTBUG-83413 Text rendering glitches in combination with loader and  
elide  
* QTBUG-102996 QML MouseArea containsPress / containsMouse / pressed are  
stuck when using multitouch  
* QTBUG-103766 MouseArea onRelease event is not triggered after second  
finger touch'n'release  
* QTBUG-74028 Text inside MultiPointTouchArea has invalid coordinates on  
touch events  
* QTBUG-100014 tst_qqmlqt fails on Android  
* QTBUG-102136 QML Slider: (Lack of) implicitWidth affects background  
height when anchors are used  
* QTBUG-101401 Crash in QQmlObjectCreator::populateInstance  
* QTBUG-104026 TypeError warnings from attached property usage in  
tst_qquicklistview  
* QTBUG-100161 DelegateModelGroup crashes on insert  
* QTBUG-103203 [REG 5.15.9 -> 6.0.4] Crash when dynamically inserting  
Item's to DelegateModelGroup  
* QTBUG-102719 [Reg 5.15 -> 6.1] Not possible to use Loader inside  
inline component  
* QTBUG-104361 [REG: 6.1->6.2] QMetaObject::invokeMethod of qml function  
has no effect  
* QTBUG-100820 [REG 5.15.2-6.2.3] Wrong rendering of semi-transparent  
text if Text.NativeRendering is used  
* QTBUG-100644 Document how to properly add javascript files with  
qt_add_qml_module  
* QTBUG-75109 tst_QQuickListView::currentIndex() is failing  
* QTBUG-103832 The delegate item of ListView is not pressed if the  
boundsBehavior is to set Flickable.StopAtBounds  
* QTBUG-102965 File order of CMake project can break compilation due to  
QMetaTypeId<T> specialization  
* QTBUG-38765 When propagateComposedEvents is set, drag does not always  
move the flickable  
* QTBUG-74842 Flickable behind MouseArea does not steal first drag event  
after creation  
* QTBUG-104523 error: no member named 'offsetsAndSize' in  
'qt_meta_stringdata_TestClass_t  
* QTBUG-101268 ListView does not preserve its relative scrollbar  
position when window is restored down on Windows if height of  
ListView.header changes dynamically  
* QTBUG-101266 Changing ListView.header height dynamically doesn't  
preserve relative scrollbar position when window is Maximized  
* QTBUG-104471 tst_QQuickListView2::tapDelegateDuringFlicking fails on  
Android  
* QTBUG-104698 tst_qqmllanguage::(installed)() Function not found:  
(installed)  
* QTBUG-101327 FAIL!  : qquicklayouts::tst_gridlayout::compile in  
QNX_710  
* QTBUG-99761 Port remaining modules with manually generated qmltypes  
files to use qmltyperegistrar (and declarative registration)  
* QTBUG-101174 Qt Design Studio crashes when built with Qt 6.3 Beta  
* QTBUG-101341 Some autotests cannot find libraries to which it is  
indirectly dependent (quicktest)  
* QTBUG-101006 tst_qquickiconimage fails on Android  
* QTBUG-95940 tst_qquicktextinput is flaky on OpenSUSE  
* QTBUG-102345 QtQuick rectangle has one pixel spacing on Android  
* QTBUG-102447 tst_drawingmodes failed  
* QTBUG-100173 tst_qquickwidget fails on Android  
* QTBUG-102462 tst_qquickitem2 fails on Android  
* QTBUG-103082 tst_qquickdrag tests fail on Android  
* QTBUG-103047 tst_qquickimageprovider::requestImage_sync fails on  
Android  
* QTBUG-103060 tst_qquicklayouts fails on Android  
* QTBUG-103094 tst_qquickshape tests fail on Android  
* QTBUG-103083 tst_QQuickDropArea::signalOrder() fails on Android  
* QTBUG-103260 tst_qquickanimatedsprite fails on Android  
* QTBUG-103257 tst_qquickcanvasitem crashes on Android  
* QTBUG-102776 JIT is disabled on Android  
* QTBUG-103310 tst_qqmlbinding::delayed() crashes on Android  
* QTBUG-103258 tst_qquickrendercontrol fails on Android  
* QTBUG-99545 App crashes in function QQmlPropertyCache::property(int)  
const on ARM 64bit  
* QTBUG-103507 tst_qquicktextedit::inFlickableTouch(editable) fails  
* QTBUG-103096 tst_qquicktext fails on Android  
* QTBUG-103256 tst_qquicktextinput fails on Android  
* QTBUG-102721 QQuickWindow::grabWindow() broken on Android  
* QTBUG-102833 tst_qqmlenginecleanup::test_customModuleCleanup() broken  
on Android  
* QTBUG-102780 Vulkan-based rendering test flaky on Android  
* QTBUG-103092 tests in tst_qquickmousearea fail on Android  
* QTBUG-103065 tst_HoverHandler::movingItemWithHoverHandler() fails on  
Android  
* QTBUG-103068 tst_PointHandler::tabletStylus() fails on Android  
* QTBUG-103066 tst_QQuickPinchHandler::scaleNativeGesture() fails on  
Android  
* QTBUG-103064 tst_DragHandler::touchDragMulti fails on Android  
* QTBUG-103098 tst_qquicktextedit fails on Android  
* QTBUG-103099 tst_qquickcanvasitem fails on Android  
* QTBUG-103078 tst_qquickwindow fails on Android  
* QTBUG-103080 tst_qquickdeliveryagent::passiveGrabberOrder() fails on  
Android  
* QTBUG-103077 tst_qquickborderimage tests fail on Android  
* QTBUG-103076 tst_qquickanimatedimage::mirror_* tests fail on Android  
* QTBUG-103086 tst_qquickfocusscope::canvasFocus() fails on Android  
* QTBUG-103088 tst_qquickitemlayer tests fail on Android  
* QTBUG-103205 SpinBox, no way to listen for text entered  
* QTBUG-102403 QObject::objectName() leads to heap-use-after-free in  
tst_qquickanimations::cleanupWhenRenderThreadStops()  
* QTBUG-103061 tst_FlickableInterop tests fail on Android  
* QTBUG-103089  
tst_QQuickListView::QTBUG_48044_currentItemNotVisibleAfterTransition()  
fails on Android  
* QTBUG-103072 tst_TapHandler::gesturePolicyDragWithinBounds fails on  
Android  
* QTBUG-102589  tst_SceneGraph::render fails on Android  
* QTBUG-102862 Build failure with lttng enabled  
* QTBUG-104157 Delegate Controls documentation: Introduction and details  
out of sync  
* QTBUG-103743 tst_v4misc::nestingDepth in qtdeclarative crashes on  
Android in 6.3 branch  
* QTBUG-104509 QtTest looks for not existing function  
  
### qtmultimedia  
* QTBUG-100181 QMediaPlayer::setPosition doesn't jump to precisely  
position while playing an FLAC file  
* QTBUG-100773 Android Multimedia arm64v8a target Huawei P40 Lite  
Android 10 QML Recorder example wont work  
* QTBUG-100835 [WMF] Resuming a video after pause generates WMF error  
* QTBUG-100854 [WMF] Crash on resuming playback of specific video  
* QTBUG-101434 QMediaRecorder is stop write to file after bluetooth  
headset is reconnected  
* QTBUG-101591 MediaRecorder/CaptureSession doesn't release audio input  
(mic) on stop recording  
* QTBUG-101719 [REG6.3.0beta2->beta3] some multimedia examples not  
compiling on macOS  
* QTBUG-99641 MacOS Monterey - QCamera stops render after a second  
* QTBUG-99361 Fix videoDimensions Test in Android  
* QTBUG-98262 Recording with audio fails on macOS 10.15 (Catalina)  
* QTBUG-99228 Qt-6.2.2 Example declarative-camera crash on Android 6.0.1  
* QTBUG-102962 Android: Update audio subsystem for SampleFormat::Float  
* QTBUG-99094 Android tst_qaudiodecoderbackend test failed  
* QTBUG-60575 QtSpeech flite backend not working on Ubuntu Linux  
* QTBUG-102707 Several videos can't be played simultaneously with OpenGL  
RHI  
* QTBUG-102843 Audioinput example: [5.15 -> 6.3] a lot of noise for the  
volume level  
* QTBUG-102969 After changing the position QMediaPlayer::setPosition in  
the pause state, a sound is heard  
* QTBUG-103394 QMediaCaptureSession crashes with QCoreApplication  
* QTBUG-99095 Android tst_QAudioSource test failed  
* QTBUG-102029 Android camera preview broken in Qt 6.2.4 (regression)  
* QTBUG-100079 Android: fix QAndroidAudioDecoder issues  
* QTBUG-97492 QAudioSink returns always UnderrunError on Android  
  
### qttools  
* QTCREATORBUG-27087 Bad colors for Stylesheet editor in dark mode  
* QTBUG-101070 Qhelpgenerator endless loop with -c option  
* QTBUG-101893 The 'help' example should only build if 'Qt::Help' is  
built  
* QTBUG-101319 Multiple qt_add_translations does not work in static  
projects  
* QTBUG-101776 qhelpgenerator installed to $prefix/bin location instead  
of $prefix/libexec  
* QTBUG-93238 [REG 5.15.2 -> 6.0.3] Cannot build docs with static build  
of Qt  
* QTBUG-101782 lrelease does not respect EXTRA_TRANSLATIONS in pro file.  
* QTBUG-102832 Qt Linguist incorrectly translates some language names  
* QTBUG-48104 QUiLoader calls property setter twice while loading an ui-  
file  
* QTBUG-102342 List of all members misses inherited method with same  
name (but different signature)  
* QTBUG-102088 Automatically generated "New QML Properties", "New QML  
Methods" miss type information  
* QTBUG-99415 lupdate ignores tr() call in a function with noexcept  
operator  
* QTBUG-104377 Qt Designer: Alignment property moves to wrong place in  
property editor  
  
### qtdoc  
* QTBUG-100383 Qt 6.2.3: 3rd party code update missing in docs  
* QTBUG-103466 Update "Implementing Atomic Operations" section  
* QTBUG-102268 There is no possibility to attach egl lib dependencies  
for Integrity  
* QTBUG-101320 Apps targeting Android 12 or higher must explicitly  
declare the android:exported attribute for app components  
* QTBUG-103597 sgexamples qtdoc test fails on Android  
* QTBUG-101323 Apps running on Android 12 and above must comply with the  
latest Unicode version  
  
### qtpositioning  
* QTBUG-102836 Configure fails when trying to configure QtPositioning  
with -no-dbus  
* QTBUG-103807 QGeoAreaMonitorSource seg fault on exit on Android  
* QTBUG-103907 sccache: error: failed to store  
`mocs_compilation.cpp.obj` to cache  
* QTBUG-103478 QGeoPositionInfoSource on Android always asks for  
location permission  
* QTBUG-101345 FAIL!  :  
tst_DeclarativePositionSource::supportedMethodsBinding in QNX_710  
* QTBUG-102994 Adding the Qt Bluetooth module produces a Makefile that  
looks for "user32.lib.lib" and "runtimeobject.lib.lib"  
  
### qtsensors  
* QTBUG-102256 Some examples not compiling on iOS: "duplicate symbol for  
architecture arm64"  
* QTBUG-102994 Adding the Qt Bluetooth module produces a Makefile that  
looks for "user32.lib.lib" and "runtimeobject.lib.lib"  
  
### qtconnectivity  
* QTBUG-101018 Bluez backend doesnt extract socket protocol information  
from service info  
* QTBUG-101071 Bluez dbus socket gives different error codes than other  
platforms  
* QTBUG-99295 The tool "Qt6::sdpscanner" was not found  
* QTBUG-101586 Bluetooth Android server asserts if disposed too quickly  
after listen()  
* QTBUG-101690 QBluetoothSocket::canReadLine can sometimes return false  
negative  
* QTBUG-101721 QBluetoothSocket double-emits connected() on macOS  
* QTBUG-101953 Windows BT COM initialization is incomplete  
* QTBUG-101984 Windows bluetooth socket not marked as unbuffered  
* QTBUG-102178 Test #10: tst_qbluetoothserver failed  
* QTBUG-102367 (potential BiC) Exported class QNdefMessage inherits from  
QList  
* QTBUG-103067 QBluetoothServer leaks RFCOMM and L2CAP Linux sockets  
* QTBUG-70222 Qt  Bluetooth LE doesn't detect Battery services  
* QTBUG-102319 Android BT service discovery agent crash when stopped  
* QTBUG-103209 As a user who compiles Qt himself, I'm left in the dark  
regarding the configuration of QtConnectivity  
* QTBUG-103826 Fix bluetooth deprecation warnings on macOS/iOS  
* QTBUG-102442 Bluetooth hostmode change Discoverable=>Connectable  
doesn't work on Android  
* QTBUG-104105 Bluez LE advertiser dispose crash when bluetooth off  
* QTBUG-104106 Android Bluetooth LE claims to advertise even if  
bluetooth off  
* QTBUG-101309 Bluez handle Enhanced LE connection complete  
* QTBUG-102256 Some examples not compiling on iOS: "duplicate symbol for  
architecture arm64"  
* QTBUG-102994 Adding the Qt Bluetooth module produces a Makefile that  
looks for "user32.lib.lib" and "runtimeobject.lib.lib"  
* QTBUG-101066 QBluetoothServiceDiscoveryAgent::finished sometimes  
(spuriously) is not emmited on Android 10  
  
### qtwayland  
* QTBUG-59627 Crash when window decorations are disabled (or switching  
to fullscreen)  
* QTBUG-100467 Window geometry is not updated when toggling the  
frameless window flag  
* QTBUG-87303 Wayland context menus can go off the screen because Qt  
does not do set_constraint_adjustment  
* QTBUG-100942 Mouse button kept pressed state after closing the window  
in mouse press handler  
* QTBUG-99802 qtwayland doesn't have all options in qt_cmdline.cmake  
* QTBUG-100148 Hover state of QCombobox has not been reset  
* QTBUG-102626 Crash with invalid min/max sizes  
* QTBUG-103391 crash on start: The Wayland connection experienced a  
fatal error: Protocol error  
* QTBUG-102829 [Wayland] Multitouch is not working in Qt6  
* QTBUG-104435 Build failure in qtwayland with libcxx  
  
### qt3d  
* QTBUG-101176 Linker error when AVX2 is disabled in core but enabled in  
Qt3D  
* QTBUG-102328 Qt3D.Core can't be imported from a static Qt build  
* QTBUG-103881 FAIL!  : tst_RayCastingJob::worldSpaceRayCaster(short  
ray)  
* QTBUG-95650 Qt3D Light Module is not working.  
* QTBUG-100402 Light uniform is hardcoded to use PointLight only  
* QTBUG-104534 QImage received from QRenderCapture using Qt3D RHI  
renderer causes crash.  
  
### qtimageformats  
* QTBUG-103454 Null-dereference read in QICNSHandler  
* QTBUG-103337 Vulnerabilities in bundled libtiff version  
* QTBUG-104398 Segmentation fault in Jpeg2000JasperReader when Jasper 3  
is used  
  
### qtserialbus  
* QTBUG-101689 QtSerialbus library linking is done using wrong Network  
library interface  
* QTBUG-101351 QModbusClient::processResponse() is never called  
* QTBUG-103879 [Reg 5.15.2 -> 5.15.9] QModbusClient:: sendRawRequest()  
produces ModbusDevice::UnknownError when there is no error  
  
### qtserialport  
* QTBUG-101444 QSerialPort: trouble with high baud rates /  
waitForReadyRead() stalls  
* QTBUG-103822 QSerialPort::waitForReadyRead always returns false on  
older Windows systems  
* QTBUG-91237 QSerialPort: moving / resizing / clicking window title bar  
blocks serial port read/write  
* QTBUG-87151 QSerialPort: synchronous read fails as waitForReadyRead()  
always times out.  
  
### qtwebsockets  
* QTBUG-101333 FAIL!  : tst_QWebSocketServer::tst_handleConnection in  
QNX_710  
* QTBUG-102713 tst_QWebSocketServer has failing tests on Android  
  
### qtwebchannel  
* QTBUG-101521 FAIL!  : qml::tst_bench::compile in QNX_710  
  
### qtwebengine  
* QTBUG-94333 Examples can't be configured due to target name conflict  
* QTBUG-94572 Update dependencies on '6.2' in qt/qtwebengine fails  
* QTBUG-88105 Windows fails sandboxed on the CIs  
* QTBUG-94759 webengine needs more dependencies checks  
* QTBUG-94343 QtWebEngineCore include paths sometimes missing when  
building core files  
* QTBUG-94709 6.2.0 Qt src package, webengine not compiling  
* QTBUG-94702 Doc: Qt WebEngine docs aren't getting built in dev/6.2  
* QTBUG-95153 6.2 QtWebEngineProcess is also in /bin  
* QTBUG-94757 Incorrect CMAKE_TOOLCHAIN_FILE check  
* QTBUG-94804 QtWebEngine install doesn't honor DESTDIR  
* QTBUG-95051 qtwebengine not forwarding CMAKE_BUILD_TYPE correctly.  
* QTBUG-94997 qtwebengine not respecting CMAKE_INSTALL_PREFIX  
* QTBUG-95473 Qt WebEngine build fails to locate the xkbcommon include  
* QTBUG-95367 Webengine examples fails to build: undefined reference to  
`QApplication::QApplication(int&, char**, int)'  
* QTBUG-95571 Console window for QtWebengineProcess.exe is displayed on  
initialization QML WebEngineView  
* QTBUG-95614 Google looks weird with QtWebEngine built with cmake  
* QTBUG-95331 QWebEnginePage::view() disappeared without a trace  
* QTBUG-94937 Clean up Qt WebEngine documentation for Qt 6.2  
* QTBUG-95564 Minimum ICU version is too low  
* QTBUG-94933 Add Qt 6 Porting Guide to Qt WebEngine  
* QTBUG-94349 cmake cannot find Qt6Targets.cmake and  
Qt6VersionlessTargets.cmake when configuring prefix build  
* QTBUG-94922 base/logging_buildflags.h may not be generated in time  
with top-level build  
* QTBUG-95152 A QtWebEngine build fails on dev on M1 MacBook  
* QTBUG-95158 Insource/Namespace/Shadow build fails.  
* QTBUG-95972 CMake build tries to link after compile error  
* QTBUG-95231 qtwebengine translations and resources installed to wrong  
path  
* QTBUG-95590 Rewrite cmake-gn intergration  
* QTBUG-96093 QtWebEngineProcess cannot start  
* QTBUG-95668 Webengine widget not visible in Designer UI  
* QTBUG-94772 Crash in Page's test: openLinkInNewPage:OverridePopup  
* QTBUG-76249 [Reg 5.9->5.11]Custom UserAgent ignored if page opened  
with window.open or _blank  
* QTBUG-96196 configure -list-features does not list webengine features  
* QTBUG-95717  Configuring: Qt 6.2 " Unknown command line option  
'-webengine-proprietary-codecs'."  
* QTBUG-96266 webengine not building (linking): LINK : fatal error  
LNK1104: cannot open file  
'CMakeFiles_QtWebEngineCore_Release_objects.rsp'  
* QTBUG-96308 Drag and drop does not work on macOS  
* QTBUG-95770 Cannot open recently saved file  
* QTBUG-95580 Crash on GetFaviconsForURL  
* QTBUG-96398 Build fails on arm  
* QTBUG-96539 WebEngineView: QtWebEngineProcess cannot start.  
* QTBUG-96002 The document QtWebengine is self-contradictory  
* QTBUG-96771 Webengine/quicknanobrowser fails to build: undefined  
reference to `QApplication::QApplication(int&, char**, int)'  
* QTBUG-96375 Build failure with webengine  
* QTBUG-96930 REG:5.15.3->5.15.4 - When doing a pinch gesture inside a  
WebEngineView then it has no effect  
* QTBUG-96855 QWebEngineDownloadItem::setDownloadFileName failed in disk  
root  
* QTBUG-97598 [Windows] Deadlock on WebEngineView rendering  
* QTBUG-94604 QtWebEngineProcess and resource paths are wrong with  
-developer-build -framework on macOS  
* QTBUG-97897 Tooltips hide by themselves almost immediatelly when  
launched from QWebEngineView  
* QTBUG-97926 QWebengine can not play the  embeded vimeo video  
* QTBUG-97836 QtWebEngineCore still not compiling from source  
* QTBUG-84105 Out-of-proc networking causes firewall confusion  
* QTBUG-92539 Weird behavior when pasting certain HTML into element with  
contentEditable attribute set  
* QTBUG-90904 Crash on calling QAccessible::registerAccessibleInterface  
* QTBUG-97472 [REG] Crash/segfault in ozone implementation when calling  
XkbGetState  
* QTBUG-98400 CVE-2021-3541 in chromium  
* QTBUG-98401 CVE-2021-3517 in chromium  
* QTBUG-71277 Nanobrowser example has confusing project layout  
* QTBUG-97414 tst_CertificateError::fatalError()  
'!page.error->isOverridable()' returned FALSE.  
* QTBUG-98918 [REG] recentlyAudible does not implement 2s cooldown  
anymore  
* QTBUG-99511 Top level cross build fails  
* QTBUG-99526 developer tools no longer highlights page elements when  
inspecting them  
* QTBUG-99485 Qt WebEngine AutomationId issue  
* QTBUG-99215 Html popups do not work correctly.  
* QTBUG-99263 QProcess::finished not emitted  
* QTBUG-99669 Glib network plugins doesn't configure or build  
* QTBUG-99890 QtWebEngine ozone platform needs pkgconfig check for  
xkbfile include  
* QTBUG-86972 [REG] QtPDF isn't properly installed as a framework unless  
WebEngine is also installed  
* QTBUG-100023 Cannot use Qt6::Pdf Module (Not Found)  
* QTBUG-94924 Load signals not emitted when opening a google result  
* QTBUG-100032 tst_qquickwebview: malloc_consolidate(): invalid chunk  
size  
* QTBUG-100285 Windows: Qt Designer crash when selecting QWebEngineView  
* QTBUG-100293 spellcheck error: session_bridge_ was not declared  
* QTBUG-100291 abort early on missing dependency: gssapi.h for kerberos  
* QTBUG-96597 Crash on WebEngine(View|Profile).userScripts.collection  
property get  
* QTBUG-100500 System libxslt is not used  
* QTBUG-101084 Test  #1: tst_qwebenginecookiestore  
.................***Failed  
* QTBUG-100996 WebEngine crashes in Accessibility  
* QTBUG-100672 Universal builds of WebEngine fail on M1 mac  
* QTBUG-101290 Unable to build examples when building as module with  
-DQT_BUILD_EXAMPLES=ON  
* QTBUG-101706 [REG] ASSERT: "event->reason() != Qt::PopupFocusReason"  
in file \Users\qt\work\qt\qtwebengine\src\webenginewidgets\render_widget  
_host_view_qt_delegate_widget.cpp, line 79  
* QTBUG-94368 [QtPDF] bitcode bundle could not be generated because  
libQt5Pdf.a was built without full bitcode  
* QTBUG-86948 When using QImageReader to load a PDF then the PDF images  
can be blurry and seem to be at half the size they should be  
* QTBUG-94046 QtPDF: configuration with -static-runtime causes linker  
errors for projects  
* QTBUG-96525 QWebEngineScript::setSourceUrl doesn't load scripts from  
qrc  
* QTBUG-101697 QtPDF's plugins.qmltypes is not installed  
* QTBUG-101935 FAIL!  : tst_QWebEnginePage::pasteImage() Compared values  
are not the same  
* QTBUG-94963 QWebEngineLoadingInfo::errorDomain() returns  
WebEngineError::InternalErrorDomain when there is no error  
* QTBUG-100806 QMimeData::html() returns undesirable meta data  
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
* QTBUG-104057 Dependency update fails: error: no matching member  
function for call to 'addAction'  
* QTBUG-92519 [REG 5.15.2 -> 5.15.3] Can't upload files on Photopea  
* QTBUG-91467 [REG 5.15.0 -> 5.15.2] OCSP is used even if not enabled  
* QTBUG-86021 WebEngineView "backgroundColor" has no documentation  
* QTBUG-94911 change locale does not work on embedded(QEMU)  
* QTBUG-95924 Touch events are not accepted in webenginequick by default  
* COIN-699 add ulimit for linux nodes  
* QTBUG-86533 Yocto and QNX builds are missing -rpath-link linker flag  
which causes non-prefix builds to fail  
* QTBUG-95269 Clicking on a link in the PDF viewer crashes with SIGSEGV  
* QTBUG-95339 QPrintPreviewDialog crash  
* QTBUG-88875 WebChannel is broken in ApplicationWorld with javascript  
disabled in MainWorld  
* QTBUG-96127 Broken external links in Qt docs  
* QTBUG-96928 QtWebEngine continuously allocates memory until it get  
killed  
* QTBUG-85084 Skip executing unnecessary commands when building tools  
during cross-compilation  
* QTBUG-96942 Developer tools open with "toogle screencast" enabled  
* QTBUG-97188 Make sure that all bots know about the new repo  
* QTBUG-99119 [REG 5 -> 6] Segfault in  
QtWebEngineCore::WebContentsDelegateQt::webEngineSettings() on Google  
Meet  
* QTBUG-98941 [Qt5.15.4][QWebEngine]QWebEnginePage::print() function  
printing a grey paper while printing a PDF in Qt5.15.4  
* QTBUG-101215 QML certifciate errror test is broken, but works on c++  
side  
* QTBUG-50686 QWebSettings::LocalContentCanAccessRemoteUrls not working  
with audio tags  
* QTBUG-87154 Add static dependencies from 3rdparty in qtbase  
* QTBUG-100404 Changes around WebEngineScript are not documented  
* QTBUG-100713 Qt WebEngine: --disable-gpu does not disable GPU  
* QTBUG-100435 Cannot enable webrtc-pipewire feature  
* QTBUG-102192 Navigation on drop broken  
* QTBUG-102323 cmake seems to treat builddir as a regex and fails if  
builddir contains quantor characters (+)  
* QTBUG-100073 Conan: leaf module options are missing -no-feature  
possibility  
* QTBUG-103859 qt-testrunner.py ERROR: exception:ParseError no element  
found  
  
### qtwebview  
* QTBUG-101487 FAIL!  : tst_QWebView::load in QNX_710  
* QTBUG-101525 FAIL!  : tst_QQuickWebView::stopEnabledAfterLoadStarted  
in QNX_710  
* QTBUG-101520 FAIL!  : tst_QQuickWebView::stopEnabledAfterLoadStarted  
in QNX_710  
  
### qtcharts  
* QTBUG-102140 error C2220: the following warning is treated as an  
errorchartpresenter.cpp(141): warning C4996:  
'QScopedPointer<ChartAxisElement,QScopedPointerDeleter<T>>::take  
* QTBUG-102286 [REG 5.15 -> 6.2] QTChartView zoom area does not work in  
x direction  
* QTBUG-101945 Changing to QValueAxis::TicksDynamic on horizontal axes  
moves ticks to the opposite side  
* QTBUG-99190 Performance issue with VXYModelMapper  
* QTBUG-102392 X-axis vanishes when difference between min and max is  
less than two  
* QTBUG-101517 FAIL!  : example::tst_barcategoryaxis::compile in QNX_710  
* QTBUG-102723 tst_qpieslice and tst_qpieseries fail on Android  
* QTBUG-102722 tst_QAreaSeries has test failures on Android  
* QTBUG-102725 charts_qml (tst_qml) fails on Android  
  
### qtdatavis3d  
* QTBUG-102735 ERROR: The test executable CRASHed uncontrollably!  
* QTBUG-101513 FAIL!  : qmltest::tst_category::compile in QNX_710  
  
### qtvirtualkeyboard  
* QTBUG-97830 Some Qt Virtual Keyboard tests checking the position of  
selection handles are failing  
* QTBUG-101512 FAIL!  : inputpanel::tst_inputpanel::compile in QNX_710  
* QTBUG-101536 FAIL!  : styles::tst_styles::compile in QNX_710  
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
  
### qtremoteobjects  
* QTBUG-102852 tst_usertypes::remoteCompositeType fails on Android  
* QTBUG-104098 Update dependencies on '6.4' fails in qt/qtremoteobjects  
* QTBUG-101336 FAIL!  : ModelreplicaTest::basicFunctions in QNX_710  
* QTBUG-101384 QtRO: Fix compiler warnings for QNX  
  
### qtquick3d  
* QTBUG-99759 Dynamically creating and destroying models causes  
assertion failure  
* QTBUG-100009  
qtquick3d/src/runtimerender/graphobjects/qssgrenderparticles.cpp:57:33:  
error: call of overloaded sqrt(int&) is ambiguous  
* QTBUG-100832 View3D.mapFrom3DScene crashes for large values  
* QTBUG-101373 Item2D node rendered indefinitey on threaded render loop,  
blocks updates on basic render loop  
* QTBUG-101882 Particle shapes don't support reparenting  
* QTBUG-102023 Incorrect shadows from SpotLight and PointLight  
* QDS-6761 Model Picking is not working correctly  
* QTBUG-102193 Negative joint index leads to crashes  
* QTBUG-101371 Node.sceneRotation may get wrong if parent node is scaled  
non-uniformly  
* QTBUG-102711 tst_MultiWindow crashes on Android  
* QTBUG-102710 tst_RenderControl fails on Android  
  
### qtshadertools  
* QTBUG-103723 [iOS] CMake shader handling fails  
  
### qt5compat  
* QTBUG-102254 tst_qtextcodec (Failed)  
* QTBUG-103927 GCC 12: failure to build from source [<Qt5Compat>]  
* QTBUG-99545 App crashes in function QQmlPropertyCache::property(int)  
const on ARM 64bit  
  
### qtopcua  
* QTBUG-103905 No target "OpenSSL::SSL" failure on qtopcua dependency  
update  
* QTBUG-100007 opcua::SubscriptionsTest is flaky on macOS  
  
Known Issues  
------------  
  
 Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-6.2/supported-platforms.html  
  
The RTA (release test automation) reported issues in Qt 6.2.x:  
https://bugreports.qt.io/issues/?filter=23315  
  
Qt 6.2.5 Open issues in Jira:  
https://bugreports.qt.io/issues/?filter=24493  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Mike Achtelik  
Laszlo Agocs  
Dimitrios Apostolou  
Soheil Armin  
Viktor Arvidsson  
YAMAMOTO Atsushi  
Vladimir Belyavsky  
Nicholas Bennett  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
Mikolaj Boc  
Francisco Boni  
Tatiana Borisova  
Joerg Bornemann  
Assam Boudjelthia  
Kai Uwe Broulik  
Florian Bruhin  
Michael Brüning  
Marco Bubke  
Andreas Buhr  
Kirill Burtsev  
Albert Astals Cid  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Szabolcs David  
Anton Demchenko  
Alexey Edelev  
Oliver Eftevaag  
Balazs Egedi  
Iikka Eklund  
Hatem ElKharashy  
David Faure  
Ilya Fedin  
Nicolas Fella  
Pekka Gehör  
Roman Genkhel  
Christophe Giboudeaux  
Maximilian Goldstein  
Andrei Golubev  
Magnus Groß  
Richard Moe Gustavsen  
Lucie Gérard  
Tang Haixiang  
Heikki Halmet  
Thomas Hartmann  
Andreas Hartmetz  
Jani Heikkinen  
Miikka Heikkinen  
Karsten Heimrich  
Ulf Hermann  
Volker Hilsheimer  
Sam James  
Allan Sandfeld Jensen  
Hu Jialun  
William Jones  
Friedemann Kleint  
André Klitzing  
Michal Klocek  
Lars Knoll  
Sze Howe Koh  
Jarkko Koivikko  
Łukasz Korbel  
Tomi Korpipaa  
Jani Korteniemi  
Janne Koskinen  
Fabian Kosmale  
Mike Krus  
Marcel Kummer  
Sona Kurazyan  
Jonas Kvinge  
Kai Köhne  
Inho Lee  
Paul Lemire  
Jonathan Liu  
Moody Liu  
Robert Loehning  
Robert Löhning  
Thiago Macieira  
Thorbjørn Lund Martsum  
Ievgenii Meshcheriakov  
Samuel Mira  
Fawzi Mohamed  
Marc Mutz  
Tommi Mänttäri  
Antti Määttä  
Martin Negyokru  
Andy Nichols  
Yuya Nishihara  
Mårten Nordheim  
Sukyoung Oh  
Kimmo Ollila  
Laszlo Papp  
Bumjoon Park  
Pasi Petäjäjärvi  
Thomas Piekarski  
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
Sami Shalayel  
Ye ShanShan  
Andy Shaw  
Venugopal Shivashankar  
David Skoland  
Daniel Smith  
Ivan Solovev  
Axel Spoerl  
Michael Spork  
Piotr Srebrny  
Christian Strømme  
Tarja Sundqvist  
Tasuku Suzuki  
Jan Arve Sæther  
Morten Johan Sørvig  
Nodir Temirkhodjaev  
Benjamin Terrier  
Duan Ting  
Ivan Tkachenko  
Jere Tuliniemi  
Paul Olav Tvete  
Jüri Valdmann  
Sami Varanka  
Peter Varga  
Doris Verria  
Tor Arne Vestbø  
Alexander Volkov  
Ville Voutilainen  
Juha Vuolle  
Jaishree Vyas  
ChunLin Wang  
Stefan Wastl  
Edward Welbourne  
Niklas Wenzel  
Clemens Werther  
Paul Wicking  
Anna Wojciechowska  
Oliver Wolff  
Li Xinwei  
Yuhang Zhao  
Volodymyr Zibarov  
Eike Ziller  
