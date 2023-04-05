Release note  
============  
  
Qt 5.15.9 release is a patch release made on the top of Qt 5.15.8. As a patch  
release, Qt 5.15.9 does not add any new functionality but provides bug fixes  
and other improvements.  
  
For detailed information about Qt, see the Qt 5.15 online documentation:  
https://doc.qt.io/qt-5/index.html.    
  
Important Changes  
-----------------  
  
### macOS  
  
* Apple Silicon (`arm64`) is now supported for both single architecture  
and universal builds.  
  
    A universal build of Qt is provided by the Qt Maintenance Tool as a  
    standalone option, in addition to the existing `x86_64` build.  
  
    ##### Known issues  
  
    * Build system support for universal builds is limited to the qmake build  
    system. See the [documentation](https://doc.qt.io/qt-5/macos.html) for
    details on how to enable universal  
    builds for your application.
  
    * The Qt WebEngine and Qt PDF modules are not supported.  
  
### qtbase  
* bcd32b0a66 QTestData: fix streaming of u8 string literals in C++20  
mode  
Fixed streaming of u8 string literals in C++20 mode.  
  
* 8c74061dd9 SQLite: Update SQLite to v3.37.0  
Updated SQLite to v3.37.0  
  
* c25d9ee376 QTzTimeZonePrivate: fix UB (data race on m_icu)  
Fixed a data race on Unix platforms when implicitly-shared copies of  
QTimeZone objects were used in certain ways (e.g. calling displayName())  
from different threads and Qt was configured with ICU support.  
  
* 5a86aa3b17 Fix crash when text shaping fails  
Fixed a possible crash with certain fonts when shaping strings  
consisting only of control characters.  
  
* 47d77dd552 JSON: When clearing duplicate object entries, also clear  
containers  
A memory leak in the JSON parser when reading objects with duplicate  
keys was fixed.  
  
* 7888d846eb Enable all supported 1.0 device features in QVulkanWindow  
QVulkanWindow is now enabling all Vulkan 1.0 features reported as  
supported from the physical device.  
  
* 059c8f9381 QDesktopServices: fix ABA problem in  
QOpenUrlHandlerRegistry  
Fixed a bug where destroying and re-creating a handler object in quick  
succession could cause the registration for the handler to be lost.  
  
* 2b0105cdc1 QDesktopServices: deprecate destroying URL handlers w/o  
explicit unsetUrlHandler()  
URL handlers that have been passed to setUrlHandler() must now be  
removed by calling unsetUrlHandler() before they are destroyed. Relying  
on the handler's destructor to implicitly unset it is now deprecated,  
because it may already be in use by concurrent openUrl() calls. Support  
for implicit unsetting will be removed in 6.6 and, until then, a  
qWarning() is raised if it is exercised.  
  
* 851d69eebc QProcess/Unix: ensure we don't accidentally execute  
something from CWD  
When passed a simple program name with no slashes, QProcess on Unix  
systems will now only search the current directory if "." is one of the  
entries in the PATH environment variable. This bug fix restores the  
behavior QProcess had before Qt 5.9. If launching an executable in the  
directory set by setWorkingDirectory() or inherited from the parent is  
intended, pass a program name starting with "./". For more information  
and best practices about finding an executable, see QProcess'  
documentation.  
  
* 9d10338d58 Update bundled libjpeg-turbo to version 2.1.3  
libjpeg-turbo was updated to version 2.1.3  
  
* 48d04fbbbf Fix C++20 ambiguous relational operators between  
QJsonValue{,Ref}  
Fixed relational operators to not cause warnings/ambiguities when  
compiling in C++20.  
  
* 41637c0727 Fix clipped glyphs in text rendering of QGraphicsTextItem  
Clipping of visible glyphs when doing partial updates of a graphics  
view was off by 1. Also fixed an issue that caused rounding errors when  
transforming the clip rect into the glyphs draw space which was caused  
by transforming a QRect instead of a QRectF.  
  
* 168ff3419f Update bundled zlib to version 1.2.12  
zlib was updated to version 1.2.12.  
  
### qtimageformats  
* c4b95ac Update bundled libwebp to version 1.2.2  
Update bundled libwebp to version 1.2.2  
  
### qtwebengine  
* Security fixes from Chromium up to version 98.0.4758.102, plus fixes for
  CVE-2022-0971 and CVE-2022-1096
  
### qtvirtualkeyboard  
* 222d99e0 Disable Windows IME when Qt Virtual Keyboard plugin is loaded  
Disable Windows IME when Qt Virtual Keyboard plugin is loaded  
  
* 84c0466a Fix activation of input panel when initial active focus is  
set  
It is now possible to open the input panel implicitly when activating  
the window. Before, this failed because the "visible" state was reset  
(due to a bug) during activation.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-99163 QTransform rotate big image will crash  
* QTBUG-98901 QtConcurrent::run crashes on program exit  
* QTBUG-99338 Configure option change QNX armv7: neon -> no  
* QTBUG-99147 <!---->  
* QTBUG-99371 QWidget::customContextMenuRequested coordinates are off  
for widgets in a QMenu  
* QTBUG-81503 qtbase contains code that isn't allowed to be distributed  
* COIN-777 *** Could not find any device matching '--platform iOS  
--minimum-deployment-target  
* QTBUG-99148 Broken html list rendering because <code> element  
* QTBUG-97771 Interaction with Apple Pencil causes crash when app window  
is shown in Sidecar  
* QTBUG-97841 MacOS Monterey - scrolling issues with touch pad  
* QTBUG-99676 markdown (and html) import/export should not rely on use  
of a fixed-pitched font to remember a `monospace` span  
* QTBUG-99427 [REG:5.15.6->5.15.7]: Qt 5.15 can no longer be build with  
C++11  
* QTBUG-85040 tst_QVulkan::vulkanVersionRequest fails with CentOS 8.1  
x64  
* QTBUG-99668 Using QDateTime with QTimeZone specified asserts in debug  
build  
* QTBUG-80666 QNetworkRequest::setHeader(IfModifiedSince) treats local  
time as UTC  
* QTBUG-92358 One More Crash in text shaping on special string with  
EmojiOneColor font.  
* QTBUG-89155 Assertion violation in text shaping on special string with  
EmojiOneColor font.  
* QTBUG-99799 Memory leak in QJsonDocument::fromJson()  
* QTBUG-97535 Bug in examples for QListIterator Class  
* QTBUG-99486 Extra dot appears in top left corner of Fusion style spin  
box frames with no buttons  
* QTBUG-95309 Compile fails with Qt in namespace and C++20  
* QTBUG-99743 QTabWidget rendering broken on macOS 12  
* QTBUG-93393 Android A11Y TalkBack: Hidden onPressAction still called  
* QTBUG-62185 QVersionNumber seems broken on -O1 and higher with g++  
* QTBUG-87136 Animations run twice as fast on a 120hz Android device  
* QTBUG-93823 Android QPlatformScreen does not expose the refresh rate:  
Animations (and timers) too fast on higher refresh rate monitors  
* QTBUG-94959 Timer and animations runs faster after screen touch event  
on Android 11  
* QTBUG-44096 QNetworkAuthenticationManager does not emit  
authenticationRequired when using NTLM  
* QTBUG-99050 Windows/5.15: Some dx symbols cannot be found due to  
directxsdk update  
* QTBUG-99323 [REG: 5.14.2 -> 5.15.0] Posted events get stuck when  
QCoreApplication::processEvents with QEventLoop::WaitForMoreEvents is  
used  
* QTBUG-100364 QStandardPaths GenericDataLocation for iOS seems to  
mention wrong path  
* QTBUG-86733 [Android] NoSuchMethodException when using QtMultimedia  
* QTBUG-93402 Android A11Y TalkBack: Focus Rect not updated on  
orientation Change  
* QTBUG-100511 windows: QLocalSocket can emit readyRead() after  
disonnected()  
* QTBUG-100217 [REG 6.2.2  -> 6.2.3] Integer overflow when rendering svg  
image  
* QTBUG-100545 Nested QML items with Accessible properties set does not  
work on Android  
* QTBUG-100775 Several data races around handlers of  
QDesktopServices::openUrl()  
* QTBUG-100362  
tst_QNetworkReply::putWithServerClosingConnectionImmediately is flaky  
* QTBUG-63196 QNetworkReply::putWithServerClosingConnectionImmediately  
fails on Windows  
* QTBUG-98476  
tst_QNetworkReply::putWithServerClosingConnectionImmediately fails in  
QtBase with Windows 11  
* QTBUG-82314 WinRT UWP (x64 and x86) missing Microsoft.VCLibs.160.00  
* QTBUG-100261 QPrinter property setup not effect  
* QTBUG-99504 Linux: QPrinter::setDuplex not effective ( Canon  
imageRUNNER 2520  )  
* QTBUG-100651 Unable to follow HTTP/2 redirects  
* QTBUG-101306 enum-enum warning in qxcbwindow.cpp is genuiune  
* QTBUG-101028 argv passed to Android apps is not sufficiently  
terminated  
* QTBUG-28379 QFileDialog: aliases to folders disabled  
* QTBUG-101551 wasm multiple "use after free" in  
QNetworkReplyWasmImplPrivate::doSendRequest  
* QTBUG-100670 QDockWidgetGroupWindow effectively sets new dockarea  
permissions on qdockwidget  
* QTBUG-93505 Unable to retrieve the swiped Filedialog  
* QTBUG-51327 [Windows 8.1]: After maximizing a window and toggling the  
frameless window hint and moving to another monitor then the window can  
be too big  
* QTBUG-93432 QGraphicsTextItem font gets incorrectly clipped when a  
clip rect is set on the painter.  
* QTBUG-100327 CompositionMode_Screen wrong with drawImage  
* QTBUG-100037 QSqlQuery: crash on executing query if connection is  
already closed  
* QTBUG-101745 Running qmake on iOS build fails on macOS 12.3 Monterey  
* QTBUG-99345 Document footer copyright note has old year, 2020  
* QTBUG-97503 Reg[5.15.2-5.15.6] Android: Keyboard covers the inputfield  
* QTBUG-81917 QtWidgets fails to build with clang 10.0-rc1 in C++20 mode  
* QTBUG-81583 QTextMarkdownWriter: if a task list item's first line ends  
with monospace text, trailing backtick is omitted  
* QTBUG-96718 Crash in inBindingWrapper() (Creator built against Qt 6.2  
build)  
* QTBUG-99009 QCursor::setPos X coordinates is wrong when DPI scaling is  
used  
* QTBUG-99642 Can't define CSS with properties for QToolButton with Qt 6  
* QTBUG-92909 When following redirects, a PROPFIND request (and probably  
others) are converted to a GET  
* QTBUG-99803 QVulkanWindow doesn't enable any device features (e.g.  
VkDeviceCreateInfo::pEnabledFeatures)  
* QTBUG-99506 Loader with states and children loaders crashes on  
Integrity (release only)  
* QTBUG-84248 tst_QFont::defaultFamily fails  
* QTBUG-95764 pure virtual call in QAccessibleQuickItem  
* QTBUG-98478 tst_QFileSystemWatcher::signalsEmittedAfterFileMoved fails  
in QtBase with Windows 11  
* QTBUG-84258 tst_Gestures::graphicsItemGesture fails  
* QTBUG-98649 Qt Android creates View IDs in a way potentially leading  
to a collision  
* QTBUG-68860 tst_QGlyphRun::mixedScripts autotest fails on Ubuntu 18.04  
and QEMU builds  
* QTBUG-93396 Android A11Y TalkBack: Slider does not announce value on  
change  
* QTBUG-95237 [REG 6.0.4 -> 6.1.0] Integer-overflow in  
QFixed::operator+= through QImage::loadFromData(QByteArray)  
* QTBUG-101636 FAIL!  : tst_QDBusConnection::registerObjectPeer2 in  
Ubuntu_20_04  
* QTBUG-94459 Android reports incorrect screen size after rotation  
* QTBUG-72110 MouseArea stops responding  
  
### qtsvg  
* QTBUG-99407 [REG 6.1.3  -> 6.2.0] Loading svg file takes too long  
  
### qtdeclarative  
* QTBUG-75799 Strange flickering when restarting an animation with  
PauseAnimation and ScaleAnimator  
* QTBUG-84196 Crash when calling QQmlEngine::retranslate  
* QTBUG-92998 Items in GridView shifts to the right when using RTL  
layoutDirection  
* QTBUG-97771 Interaction with Apple Pencil causes crash when app window  
is shown in Sidecar  
* QTBUG-99400 [Reg 5.2 -> 5.3] qmlplugindump: error details missing on  
linux  
* QTBUG-99608 tst_qmlcachegen (Failed)  
* QTBUG-49049 arcTo doesn't always get drawn  
* QTBUG-86453 Instantiator creates delegates when active is false if  
items are dynamically added to a ListModel  
* QTBUG-88331 Instantiator creates delegate when active is false and  
delegate is updated  
* QTBUG-83315 Qt Quick SceneGraph: Indices alignment problem  
* QTBUG-86695 [REG: 5.12 -> 5.14] Broken State::when behavior after  
suspicious change  
* QTBUG-100260 Crash on access after using QML singleton as a model  
* QTBUG-77371 Accessibility: Multiple Text items with Accessible  
properties grouped together on Android  
* QTBUG-85325 when a PointerHandler with a custom cursor deactivates,  
the cursor doesn't change until the next mouse move  
* QTBUG-85303 HoverHandler margin not changing cursorShape  
* QTBUG-81938 qtdeclarative:  
tst_QPauseAnimationJob::multipleSequentialGroups is flakey  
* QTBUG-99765 tst_QQuickDropArea::containsDrag_internal fails in Ubuntu  
20.04  
* QTBUG-64470 tst_QQuickFramebufferObject::testInvalidate is failing on  
macOS  
* QTBUG-65614 tst_QQuickFramebufferObject failed on b2qt  
* QTBUG-89193 ListView delegate position resets after displaced  
transition  
* QTBUG-100431 Crash in libQt5Qml V4 engine caused by wrong memory  
access  
* QTBUG-89380 Cannot use QtObject as containmentMask  
* QTBUG-92809 ListView can go out of sync with the model if item is  
removed and inserted outside of the view before the current item  
* QTBUG-101499 FAIL!  : tst_QQuickMultiPointTouchArea::nonOverlapping in  
Ubuntu_20_04  
* QTBUG-101498 FAIL!  : tst_QQuickListView::currentIndex in Ubuntu_20_04  
  
### qtmultimedia  
* QTBUG-101450 gstreamer: QMediaPlayer::duration gives wrong result in  
very long videos  
  
### qttools  
* QTBUG-96549 make clean removes ts file when using  
qt5_create_translation()  
* QTBUG-97562 qdoc: Assert when there's an empty link target  
* QTBUG-98466 Misleading error messages when using macdeployqt on  
AppleSilicon Macs  
  
### qtdoc  
* QTBUG-99847 Update Qt Creator info in Qt Quick tutorial  
* QTBUG-100434 Tutorials/alarms not launching on macOS  
  
### qtconnectivity  
* QTBUG-98582 QT Bluetooth LE crashed when connect/disconnect to a  
device  
* QTBUG-98719 QBluetoothSocket deletion occasionally crashes on Windows  
* QTBUG-99687 Windows BT service scan scans just one device  
* QTBUG-99410 [macOS 12.1] Bluetooth data stream blocked when main menu  
opened  
* QTBUG-99689 Windows BT service scan filter fails against Linux server  
* QTBUG-99673 Service discovery with UUID filter doesn't work on macOS  
Monterey  
* QTBUG-100445 macOS bluetooth SDP records contain anomalies  
* QTBUG-99767 [5.15.7 -> 5.15.8] Bluetooth error: Make sure  
'QHash<QLowEnergyHandle,QLowEnergyServicePrivate::CharData>' is  
registered using qRegisterMetaType()  
* QTBUG-100289 pingpong Linux => Windows doesn't work  
* QTBUG-100303 Bluetooth RFComm [Outbound] connection issue with  
Monterey  
* QTBUG-100894 Linux bluetooth crash when multiple services found  
* QTBUG-101018 Bluez backend doesnt extract socket protocol information  
from service info  
* QTBUG-101690 QBluetoothSocket::canReadLine can sometimes return false  
negative  
* QTBUG-98351 Thread-safe Android BT LE Java implementation  
* QTBUG-98955 tst_QBluetoothServiceInfo::tst_assignment fails on macOS  
12 ARM  
* QTBUG-100042 Windows BT (server) pingpong service is not found  
* QTBUG-99685 Windows BT classic service scan doesn't always start  
* QTBUG-101309 Bluez handle Enhanced LE connection complete  
  
### qtwayland  
* QTBUG-90530 Low resolution title bar icon on Wayland on Hi DPI  
displays  
* QTBUG-95032 Dialogs on Wayland/Sway not drawn correctly when using  
client side decorations  
* QTBUG-99965 Build with -no-feature-tabletevent fails for Linux/Wayland  
* QTBUG-100467 Window geometry is not updated when toggling the  
frameless window flag  
* QTBUG-87303 Wayland context menus can go off the screen because Qt  
does not do set_constraint_adjustment  
* QTBUG-100942 Mouse button kept pressed state after closing the window  
in mouse press handler  
* QTBUG-100150 Touch event ignored when main GUI thread is slow  
  
### qt3d  
* QTBUG-99414 License.txt file not found under  
src/3rdparty/assimp/contrib/clipper  
* QTBUG-85575 Qt3D access violation (SIGSEGV) while closing example  
application  
* QTBUG-98421 tst_QChangeArbiter::distributePropertyChanges fails with  
Ubuntu 20.04 in Qt3d  
* QTBUG-101556 FAIL!  : tst_GraphicsHelperGL4::bindFrameBufferAttachment  
in Ubuntu_20_04  
  
### qtwebengine  
* QTBUG-98918 [REG] recentlyAudible does not implement 2s cooldown  
anymore  
* QTBUG-99403 MacOS 12 x86_64 build fails with Webengine: Undefined  
symbols for architecture x86_64  
* QTBUG-99263 QProcess::finished not emitted  
* QTBUG-86972 [REG] QtPDF isn't properly installed as a framework unless  
WebEngine is also installed  
* QTBUG-100023 Cannot use Qt6::Pdf Module (Not Found)  
* QTBUG-94924 Load signals not emitted when opening a google result  
* QTBUG-86948 When using QImageReader to load a PDF then the PDF images  
can be blurry and seem to be at half the size they should be  
* QTBUG-98941 [Qt5.15.4][QWebEngine]QWebEnginePage::print() function  
printing a grey paper while printing a PDF in Qt5.15.4  
* Security fixes from Chromium up to version 98.0.4758.102  
  
### qtquickcontrols2  
* QTBUG-96888 Not possible to quickly click buttons  
* QTBUG-99644 invalid access of indicator item inside switch type  
destructor  
* QTBUG-96551 Crash while processing a shortcut key  
* QTBUG-96561 MenuItem does not clear shortcuts from GUI kernel  
* QTBUG-99547 PathView item does not appear in certain circumstance  
* QTBUG-51078 Use of Item obligatory in SwipeView?  
* QTBUG-51669 QQC2: SwipeView is not working as expected  
  
### qtpurchasing  
* QTBUG-99568 [REG: 5.15.6->5.15.8] Qt Purchasing doesn't restore  
purchased products.  
  
### qtdatavis3d  
* QTBUG-99764 tst_proxy::addModel fails with Ubuntu 20.04 in lts-5.15  
* QTBUG-100815  tst_proxy::construct failed with Ubuntu 20.04  
  
### qtvirtualkeyboard  
* QTBUG-93042 Program crashed when type with keyboard  
* QTBUG-86190 Shift button on virtual keyboard is disabled on startup of  
application  
* QTBUG-97830 Some Qt Virtual Keyboard tests checking the position of  
selection handles are failing  
* QTBUG-101622 FAIL!  : inputpanel::tst_plugin::test_hangulInputMethod  
in Ubuntu_20_04  
  
### qtspeech  
* QTBUG-66034 Locales are not displayed QtSpeech example on Android  
  
### qtremoteobjects  
* QTBUG-85124 QRemoteObjectHost::hostUrl() crashes if no URL is set  
  
### qtquick3d  
* QTBUG-101371 Node.sceneRotation may get wrong if parent node is scaled  
non-uniformly  
  
Known Issues  
------------  
  
* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-5.15/supported-platforms.html  
  
* The RTA (release test automation) reported issues in Qt 5.15.x:  
https://bugreports.qt.io/issues/?filter=21874  
  
* Qt 5.15.9 Open issues in Jira:  
https://bugreports.qt.io/issues/?filter=24473  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Mike Achtelik  
Laszlo Agocs  
Viktor Arvidsson  
Albert Astals Cid  
Eskil Abrahamsen Blomfeldt  
Sören Bohn  
Joerg Bornemann  
Assam Boudjelthia  
Michael Brüning  
Andreas Buhr  
Michał Cieślak  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Szabolcs David  
Alexey Edelev  
Oliver Eftevaag  
Hatem ElKharashy  
David Faure  
Ilya Fedin  
Maximilian Goldstein  
Richard Moe Gustavsen  
Tang Haixiang  
Heikki Halmet  
Zhang Hao  
Andreas Hartmetz  
Jani Heikkinen  
Ulf Hermann  
Volker Hilsheimer  
Allan Sandfeld Jensen  
William Jones  
André Klitzing  
Seokha Ko  
Jarek Kobus  
Jarkko Koivikko  
Tomi Korpipaa  
Jani Korteniemi  
Fabian Kosmale  
Sona Kurazyan  
Jonas Kvinge  
Kai Köhne  
Inho Lee  
Tony Leinonen  
Paul Lemire  
Thiago Macieira  
Ievgenii Meshcheriakov  
Leena Miettinen  
Andrey Mozzhuhin  
Marc Mutz  
Antti Määttä  
Sivan Nanthiran  
Delf Neumärker  
Yuya Nishihara  
Mårten Nordheim  
Kimmo Ollila  
Pasi Petäjäjärvi  
Samuli Piippo  
Timur Pocheptsov  
Joni Poikelin  
Rami Potinkara  
Lorn Potter  
Liang Qi  
Topi Reinio  
Bernhard Rosenkraenzer  
Shawn Rutledge  
Lars Schmertmann  
Ye ShanShan  
Tianlu Shao  
Andy Shaw  
Ivan Solovev  
Axel Spoerl  
Patrick Stewart  
Christian Strømme  
Tarja Sundqvist  
Morten Johan Sørvig  
Benjamin Terrier  
Ivan Tkachenko  
Tor Arne Vestbø  
Juha Vuolle  
Edward Welbourne  
Oliver Wolff  
Weng Xuetian  
Marianne Yrjänä  
Vlad Zahorodnii  
