Release note  
============  
  
Qt 5.15.11 release is a patch release made on the top of Qt 5.15.10. As a patch  
release, Qt 5.15.11 does not add any new functionality but provides bug fixes  
and other improvements.  
  
For detailed information about Qt, see the Qt 5.15 online documentation:  
https://doc.qt.io/qt-5/index.html.    
  
Important Changes  
-----------------  
  
### qtbase  
* 861dcdd245 Upgrade PCRE2 to 10.40  
PCRE2 has been updated to 10.40.  
  
* a9ffb84c31 QCOMPARE/QVERIFY: fix huge pessimisation in QTestResult  
Optimized successful QCOMPARE and QVERIFY for an up to 2x speedup.  
  
* 614ab3a4bd SQLite: Update SQLite to v3.39.2  
Updated SQLite to v3.39.2  
  
* 1f9b635044 Fix crash when setting override cursor on multiple clients  
Fixed a crash when setting an override cursor on multiple clients.  
  
* 6a648d270e Update bundled libjpeg-turbo to version 2.1.4  
libjpeg-turbo was updated to version 2.1.4  
  
### qtdeclarative  
* b368ffc8c6 QQmlDebug: reliably print the debugger warning  
The warning about enabled debuggers is now printed when at least one  
translation unit in the final executable requests it, independent of the  
order in which translation units are linked/initialized.  
  
* 71fb661ef8 Fix fractional scaling of text in Qt Quick  
Fixed a kerning issue with native-rendered text when there is a  
fractional system scale factor set.  
  
### qttools  
* 4b4f38d26 lupdate: Allow multiple specifiers after method signature  
lupdate does not trip anymore over tr() calls in methods with multiple  
specifiers. For example "QString MyClass::foo() const noexcept" now gets  
the correct context.  
  
### qtlocation  
* 63d055e8 Update use of HTTP to HTTPS in esri plugin  
  
  
### qtimageformats  
* fedf3d9 Update bundled libtiff to version 4.4.0  
Bundled libtiff was updated to version 4.4.0  
  
* 8fb9a4f Update bundled libwebp to version 1.2.4  
Update bundled libwebp to version 1.2.4  
  
### qtserialbus  
* db246244 Make pduFromStream work on big endian (again)  
Fix reading from stream on big endian systems  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-103605 qfilesystemmodel.cpp fails to compile on Windows with  
oneAPI icx using c++20  
* QTBUG-103820 Cannot use OpenSSL v3 even with compatibility mode  
* QTBUG-102960 iOS: input panel shows wrong suggestions  
* QTBUG-103782 Buffer overflow in qt_readlink (in qmlplugindump, via  
qmake) with -D_FORTIFY_SOURCE=3 and GCC 12  
* QTBUG-38971 QtActivity did not call through to  
super.onConfigurationChanged() on orientation change (crash)  
* QTBUG-102298 Android: Switching navigation bar between buttons /  
gestures hides qml elements  
* QTBUG-99691 Starting QtService causes black screen  
* QTBUG-103608 Can't set android target sdk version with cmake  
* QTBUG-104262 Fail to build android app cannot find symbol  
QtNative.isStarted  
* QTBUG-98417 Bundling translation file of plist does not work with  
XCode 13  
* QTBUG-49704 QLoggingCategory::installFilter crashes with the code from  
documentation  
* QTBUG-102395 QMainWindow::restoreState corrupts relation between  
toolbars layout item  
* QTBUG-86790 Mingw Qt provides debug libraries in the wrong folder  
* QTBUG-102021 QCocoaScreen::UpdateScreens crash  
* QTBUG-84741 Crash on QCocoaScreen::isOnline() when calling  
CGDisplayIsOnline  
* QTBUG-103568 Android 13: Warnings when starting qt apps  
* QTBUG-104362 QDomImplementation::DropInvalidChars strips emoji and  
other non-BMP characters  
* QTBUG-95933 Using scanner input IRcode will result in an error when  
second character is uppercase  
* QTBUG-71900 Double tapping on a word does not show the selection  
handles in the right place after the initial selection  
* QTBUG-101615 QMLPATHS not documented  
* QTBUG-58503 Text Handle Cursor Position Offset Error  
* QTBUG-36637 androiddeployqt puts *.qmltypes files into apk  
* QTBUG-104809 Crash in QKmsDevice::createScreenForConnector  
* QTBUG-101161 Android Assets awfully slow to be loaded  
* QTBUG-104412 FAIL!  : tst_AndroidAssets during dependency update  
* QTBUG-53661 QDom internalSubset is never set  
* QTBUG-102825 Popping QML StackView Item makes a11y unusable  
* QTBUG-103892 Stop binding to iBridge interface when unit testing  
QTcpServer on macOS  
* QTBUG-49205 tst_qnetworkreply::ioGetFromBuiltinHttp  
* QTBUG-104232 tst_QSslKey::constructor fails with Ubuntu 22.04 and  
openssl 3  
* QTBUG-91139 Select handles Left- and RightPoint disappears when click  
select all on editPopupmenu without margins of textedit.  
* QTBUG-105064 [REGR: 5.15.9 -> 5.15.10] QDateTime::addDays() gives  
wrong result in Qt 5.15.10  
* QTBUG-102109 In Android using Qt::LocalTime with specific timezones  
does not handle daylight-saving time properly  
* QTBUG-104851 qdoc: Ignore Q_WEAK_OVERLOAD  
* QTBUG-69354 QGtk3FileDialogHelper isn't modal  
* QTBUG-105302 qputenv sometimes puts garbage at the end of the value  
* QTBUG-105041 openssl 3.x 32bit platform regression  
* QTBUG-97486 Crash in TimeZone ICU backend  
* QTBUG-105323 [Regression] Keyboard is not properly hidden on ios  
* QTBUG-105374 Modules in 5.15 branch missing MinGW debug files  
* QTBUG-104940 post in/decrements of QBEInteger and QLEInteger return  
reference according to documentation  
* QTBUG-95319 The cursor size is unstable when multiple QT_SCALE_FACTOR  
is used  
* QTBUG-99990 windows: Painting an image with DPR >1.0  to a QPrinter  
does not produce correct result  
* QTBUG-105517 Redundant "does" in QFrame  
* QTBUG-98651 [iOS 15] Application freezes when QDialog is executed by  
button clicked() signal  
* QTBUG-103571 QWindowsContext::findPlatformWindowAt stuck in infinite  
loop  
* QTBUG-82477 QClipboard doesn't support custom mimeTypes  
* QTBUG-102359  NTLM authentication crashes  
* QTBUG-105286 Crash with UpdateWindowTitle event triggered by closing a  
dialog (mac)  
* QTBUG-56893 Closing a dialog via mouse click on a button causes an XCB  
error  
* QTBUG-105711 QDrag with invalid URLs in QMimeData crash on macOS  
* QTBUG-105591 Closing application with toolbar floating breaks toolbar  
the next time you start the application  
* QTBUG-106017 tst_QSslCertificate fails with Ubuntu 22.04 xorg and  
Windows 10 21H2 OpenSSL 3  
* QTBUG-106019 tst_QDtls::verifyClientCertificate fails with Ubuntu  
22.04 xorg and Windows 10 OpenSSL 3  
* QTBUG-105057 vnc: Setting override cursor causes a crash on client  
disconnect  
* QTBUG-106374 Unable to build qtbase due to incomplete type in  
qtessellator.cpp  
* QTBUG-103740 QTemporaryFile::rename does not document that it can only  
rename, not copy+delete like QFile::rename  
* QTBUG-101396 QOpenGLTextureBlitter support for GL_TEXTURE_RECTANGLE  
breaks on some Intel drivers  
* QTBUG-106252 ANDROID_SDK can be used before it is set  
* QTBUG-105618 QNetworkReplyFileImpl synchronously emits  
QNetworkReply::finished() from constructor in case of error  
* QTBUG-94557 Menu causes touch failure  
* QTBUG-98519 [REG: 5.15.0->5.15.7] xcb: Synthesized mouse from touch  
gets stuck if receiving widget gets destroyed  
* QTBUG-102751 Can not receive touch event after the widget that  
WindowFlags is Qt::Popup is closed on ubuntu20.04  
* QTBUG-103706 Synthesized touch event not recognized with Widgets  
* QTBUG-106387 Application crash when writing in textfield  
* QTBUG-98988 Qt bugs when portal implementation is not available  
* QTBUG-99948 Fix enum/enum arithmetic in Qt  
* QTBUG-103923 GCC 12: failure to build from source [<QtBase>]  
* QTBUG-104012 QDateTime constructor performance regression when year is  
below epoch  
* QTBUG-62102 QKeySequenceEdit handles meta keys incorrectly on Wayland  
* QTBUG-87669 few gui tests fail to build on Android  
* QTBUG-95202 Auto-generated android-*-deployment-settings.json contains  
wrong path to immediate qrc file on Qt 6  
* QTBUG-95235 Building Quick Controls 2 examples with Qt 6.1.1 for  
Android fails  
* QTBUG-102594 [REG 5.15.6 -> 5.15.9] Many ANR issues by QtAccessibility  
* QTBUG-104580 androiddeployqt fails with "unknown argument '--libs'"  
when call llvm-readobj v14  
* QTBUG-101008 Using Text.NativeRendering results in characters drawn  
too close to each other with fractional scale factors  
* QTBUG-104450 qmake: it's impossible to configure some compiler and  
linker options in the generated vcxproj  
* QTBUG-104787 Thread Sanitizer reports data races in QtConcurrent  
* QTBUG-105158 Initialize all Vulkan Device Properties  
* QTBUG-87137 tst_QApplication::sendEventsOnProcessEvents() failed on  
Ubuntu 20.04/22.04 and RHEL 9  
* QTBUG-103513 A11Y: Flickable child item focus frame position not  
updated  
* QTBUG-103499 Android a11y: Flickable items outside of view are not  
selectable  
* QTBUG-68865 tst_QMenuBar::check_menuPosition autotest fails on Ubuntu  
18.04  
* QTBUG-84248 tst_QFont::defaultFamily fails  
* QTBUG-68860 tst_QGlyphRun::mixedScripts autotest fails on Ubuntu 18.04  
and QEMU builds  
* QTBUG-106018  tst_QSslSocket fails with Ubuntu 22.04 xorg and Windows  
10 21H2 plus OpenSSL 3  
* QTBUG-106513 FAIL!  : tst_QSqlQuery::queryOnInvalidDatabase in  
MacOS_12  
* QTBUG-106599 FAIL!  : tst_Http2::authenticationRequired in  
Ubuntu_20_04  
* QTBUG-106632 FAIL!  : tst_QDBusConnection::registerObjectPeer in  
Ubuntu_20_04  
* QTBUG-105958 [Android] Intent + Talkback leads to deadlock  
* QTBUG-41170 [Android]: When the window resizes then there it will  
cause flicker  
* QTBUG-66727 [Android]: When changing focus between TextInput fields  
there is a flicker of the QQuickWidget  
  
### qtsvg  
* QTBUG-101698 [REG 6.2.2 -> 6.2.3] Integer overflow when loading svg  
image  
  
### qtdeclarative  
* QTBUG-74028 Text inside MultiPointTouchArea has invalid coordinates on  
touch events  
* QTBUG-103522 The PreventStealing of mouseArea does not work properly  
in Flickable's(ListView) child item.  
* QTBUG-103924 GCC 12: failure to build from source [<QtDeclarative>]  
* QTBUG-69538 Drawing issues with Intel HD530/630, 11th Gen Intel UHD  
* QTBUG-102954 Invalid z-order when rendering custom QQuickItem with  
opengl/d3d12 backend  
* QTBUG-100579 Crash when removing docked QQuickWidget in multiscreen  
setup with Qt 5  
* QTBUG-98914 QML Test with grabImage() fails on iOS  
* QTBUG-94900 python path containing space breaks build from source  
* QTBUG-86805 [Android]TapHandler crash while using the S-Pen  
* QTBUG-94983 Crash when binding to aliased grouped property  
* QTBUG-91687 QML fails to run benchmarks in qmlbench's v8bench  
directory  
* QTBUG-58559 Deletion of a dynamic properties to JSObject ends up using  
all memory  
* QTBUG-105899 ColorDialog: The text fields on ColorInputs.qml are buggy  
for the Fusion, Imagine and Universal styles.  
* QTBUG-104966 The Items in the ListView is not showing when the model  
is changed during dragging  
* QTBUG-93188 tst_qqmlecmascript::gcCrashRegressionTest fails with ARM  
macOS 11 in Qt Declarative  
* QTBUG-106377 Cannot create QML_SINGLETON class with newer gcc versions  
* QTBUG-101008 Using Text.NativeRendering results in characters drawn  
too close to each other with fractional scale factors  
* QTBUG-106594 Text baseline anchor not updating properly  
* QTBUG-106256 qml crash when binding alias to property  
* QTBUG-99545 App crashes in function QQmlPropertyCache::property(int)  
const on ARM 64bit  
* QTBUG-36637 androiddeployqt puts *.qmltypes files into apk  
* QTBUG-103513 A11Y: Flickable child item focus frame position not  
updated  
* QTBUG-106356 FAIL!  :  
tst_QParallelAnimationGroupJob::deleteChildrenWithRunningGroup in  
MacOS_12  
* QTBUG-106424 FAIL!  : tst_QQuickLoader::asyncToSync1 in Ubuntu_20_04  
* QTBUG-106278 FAIL!  :  
tst_qquickflickable::setContentPositionWhileDragging in MacOS_12  
  
### qtmultimedia  
* QTBUG-104041 QAudioRecorder outputLocation set only after recording  
stop  
  
### qttools  
* QTBUG-99415 lupdate ignores tr() call in a function with noexcept  
operator  
* QTBUG-102607 macdeployqt: errors when producing a universal binary  
(universal binary)  
* QTBUG-104755 Qt 5 Designer plugins: Missing pre-built debug plugins  
  
### qtxmlpatterns  
* QTBUG-104707 acceltree/qacceltreeresourceloader.cpp:369:31: error: no  
viable conversion from 'const QChar' to 'char32_t'  
  
### qtdoc  
* QTBUG-103303 Qt PDF module documentation  
  
### qtlocation  
* QTBUG-103807 QGeoAreaMonitorSource seg fault on exit on Android  
* QTBUG-103478 QGeoPositionInfoSource on Android always asks for  
location permission  
* QTBUG-92111 Esri plugin uses HTTP instead of HTTPS, creating 400 Bad  
Request  
  
### qtconnectivity  
* QTBUG-103067 QBluetoothServer leaks RFCOMM and L2CAP Linux sockets  
* QTBUG-104479 (Classic) bluetooth service scan sometimes hangs  
indefinitely on Android  
* QTBUG-101066 QBluetoothServiceDiscoveryAgent::finished sometimes  
(spuriously) is not emmited on Android 10  
  
### qtwayland  
* QTBUG-105308 ASSERT failure in QWindow: "Updates can only be scheduled  
from the GUI (main) thread"  
* QTBUG-104435 Build failure in qtwayland with libcxx  
  
### qt3d  
* QTBUG-104593 Qt3D Application Crashes when rendering first frame  
* QTBUG-102445 [REG]PLY loader failing from 5.15.8  
* QTBUG-101876 Qt3D Viewport documentation states wrong type for Gamma  
property  
* QTBUG-106519 FAIL!  :  
tst_dynamicnodecreation::createEntityAndDynamicChild in Ubuntu_20_04  
  
### qtimageformats  
* QTBUG-103454 Null-dereference read in QICNSHandler  
* QTBUG-103337 Vulnerabilities in bundled libtiff version  
* QTBUG-104398 Segmentation fault in Jpeg2000JasperReader when Jasper 3  
is used  
  
### qtquickcontrols  
* QTBUG-106520 FAIL!  :  
qtquickcontrols::Tests_StackLayout::test_addAndRemoveItems in  
Ubuntu_20_04  
* QTBUG-106521 FAIL!  :  
qtquickcontrols::Tests_StackLayout::test_addAndRemoveItems in MacOS_12  
  
### qtserialbus  
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
  
### qtwebengine  
* QTBUG-103578 WebEngine: Error when linking gn  
* QTBUG-101030 The zoom factor is reset every time QtWebEngine loads a  
new website  
* QTBUG-79254 QWebEngineView couldn't handle touch events for html  
select's popup menus  
* QTBUG-103618 WebEngine - Project ERROR: Unknown module(s) in QT:  
widgets  
* QTBUG-104763 WebEngine view becomes white if minimized and restored  
* QTBUG-97392 WebEngine fails to load urls from resources  
* QTBUG-106688 Loading html from qrc in QtWebEngine fails  
* QTBUG-102099 QWebEngineView ColorPicker  is not modal and freezes  
application  
* QTBUG-104755 Qt 5 Designer plugins: Missing pre-built debug plugins  
* QTBUG-106461 QWebEngineUrlRequestJob::reply() does not support a  
QIODevice that cannot be read completely instantly  
  
### qtwebview  
* QTBUG-97487 [Android] WebView cannot open local file  
(net::ERR_ACCESS_DENIED)  
  
### qtquickcontrols2  
* QTBUG-104009 Issues with Slider in ListView with pressDelay set with  
touch screen  
* QTBUG-77202 No touch release event for AbstractButton inside of  
ListView with pressDelay set  
* QTBUG-104983 [REG] 908aa77d16e00f2bccc0ddae0f8b61955c56a6a1 breaks  
scrollbars if contentItem is accessed before it is set  
* QTBUG-103250 Link to ScrollBar's size property is wrong  
  
### qtcharts  
* QTBUG-103906 QValueAxis::TicksDynamic causes application to freeze  
* QTBUG-99190 Performance issue with VXYModelMapper  
* QTBUG-102392 X-axis vanishes when difference between min and max is  
less than two  
  
### qtvirtualkeyboard  
* QTBUG-94770 [Qt Virtual keyboard] Keyboards doesn't respond when  
QT_SCALE_FACTOR  is set to 1.5  
  
### qtremoteobjects  
* QTBUG-104098 Update dependencies on '6.4' fails in qt/qtremoteobjects  
* QTBUG-105597 tst_Server_Process failed  
  
### qtwebglplugin  
* QTBUG-105606 FAIL!  : tst_WebGL::update(Launcher), the requested  
timeout (5000 ms) was too short  
  
### qtquick3d  
* QTBUG-103866 View3D content turns black when resized while hidden  
  
### qtmqtt  
* QTBUG-105873 QMqttClient documentation does not include the  
constructor  
  
Known Issues  
------------  
  
* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-5.15/supported-platforms.html  
  
* The RTA (release test automation) reported issues in Qt 5.15.x:  
https://bugreports.qt.io/issues/?filter=21874  
  
* Qt 5.15.11 Open issues in Jira:  
https://bugreports.qt.io/issues/?filter=24475  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Mike Achtelik  
Laszlo Agocs  
Dimitrios Apostolou  
Mate Barany  
Eskil Abrahamsen Blomfeldt  
Joerg Bornemann  
Assam Boudjelthia  
Michael Brüning  
Andreas Buhr  
Kirill Burtsev  
Andrey Butirsky  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Alexey Edelev  
Oliver Eftevaag  
Andreas Eliasson  
Tunahan Erkoyuncu  
Ilya Fedin  
Alexandros Frantzis  
Pekka Gehör  
Richard Moe Gustavsen  
Tang Haixiang  
Heikki Halmet  
Christian Heimlich  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Dominik Holland  
Sam James  
Allan Sandfeld Jensen  
Milo Kerr  
Michal Klocek  
Kai Koehne  
Tomi Korpipaa  
Mike Krus  
Jaroslaw Kubik  
Sona Kurazyan  
Jonas Kvinge  
Kai Köhne  
Inho Lee  
Paul Lemire  
Moody Liu  
Robert Loehning  
Robert Löhning  
Thiago Macieira  
Samuel Mira  
Marc Mutz  
Antti Määttä  
Mårten Nordheim  
Laszlo Papp  
Timur Pocheptsov  
Joni Poikelin  
Liang Qi  
Topi Reinio  
Rafael Roquetto  
Niclas Rosenvik  
Elias Rudberg  
Shawn Rutledge  
Michael Saxl  
Dmitry Shachnev  
Sami Shalayel  
Ye ShanShan  
Andy Shaw  
Ivan Solovev  
Axel Spoerl  
Christian Strømme  
Tarja Sundqvist  
Jan Arve Sæther  
Ivan Tkachenko  
Mike Trahearn  
Jens Trillmann  
Jere Tuliniemi  
Peter Varga  
Louis du Verdier  
Tor Arne Vestbø  
Ville Voutilainen  
Juha Vuolle  
Edward Welbourne  
Paul Wicking  
