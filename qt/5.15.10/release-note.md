Release note  
============  
  
Qt 5.15.10 release is a patch release made on the top of Qt 5.15.9. As a patch  
release, Qt 5.15.10 does not add any new functionality but provides bug fixes  
and other improvements.  
  
For detailed information about Qt, see the Qt 5.15 online documentation:  
https://doc.qt.io/qt-5/index.html.    
  
Important Changes  
-----------------  
  
### qtbase  
* 8975b7c2b0 Update bundled zlib to version 1.2.12  
zlib was updated to version 1.2.12.  
  
* da52a120dc QBuffer: fail early in seek() beyond QByteArray's max  
capacity  
Fixed silent data corruption on 32-bit platforms when seek() fails due  
to position > INT_MAX.  
  
* 9c60c8b122 Upgrade PCRE2 to 10.40  
PCRE2 has been updated to 10.40.  
  
### qtwebengine  
* d6512f48b Enable Apple Silicon support  
Apple Silicon universal- and cross-builds on macOS are now supported.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-92445 Markdown smashes nested formatting inside lists  
* QTBUG-99148 Broken html list rendering because <code> element  
* QTBUG-102066 SDK version detection does not ignore stderr  
* QTBUG-53290 QWindowsPrintDevice::defaultPrintDeviceId() may crash,  
when no printers are installed  
* QTBUG-95114 When accessibility is made active after the start up of an  
application then it will trigger an update of all existing controls to  
update roles and names  
* QTBUG-97103 REG: 5.15.0->5.15.1: Under some circumstances the  
performance of an application on Windows when switching application  
focus  
* QTBUG-98369 [macOS] Qt internal warning when FontMetrics is used  
* QTBUG-99216 QMessageBox with Japanese characters gives "Missing font  
family" warning on macOS  
* QTBUG-88042 tst_QTcpSocket::connectToHostError() failed on Ubuntu  
20.04 in CI  
* QTBUG-102109 In Android using Qt::LocalTime with specific timezones  
does not handle daylight-saving time properly  
* QTBUG-102274 QBuffer silent data corruption on seek() past INT_MAX  
(32-bit only)  
* QTBUG-101460 QTimeZone::displayName ignores locale on Android  
* QTBUG-100135 40000 chips example - zoom in/out buttons do not work  
* QTBUG-102484 Race condition in QSemaphore  
* QTBUG-101347 QMainWindow Menu / actions sometimes not displayed when  
performing long operations  
* QTBUG-99810 [REG: 5.15.5->5.15.6] xcb: Dock widgets disappear if  
trying to float them from QMainWindow that contains native window  
* QTBUG-69515 Linux, WindowStaysOnTopHint does not work.  
* QTBUG-73485 Issue with Qt::WindowStaysOnTopHint  
* QTBUG-81341 Window won't receive events above Gnome Dock despite  
X11ByPassWindowManager + WindowsStaysOnTop is set  
* QTBUG-65425 FreeBSD build is broken for qmake  
* QTBUG-102744  QML items with Accessible properties set does not set  
properly for Android  
* QTBUG-84302 No sdkBuildToolsRevision in deployment JSON  
* QTBUG-91391 androiddeployqt uses deprecated ndk.dir property  
* QTBUG-102199 QLocale::toDateTime asserts  
* QTBUG-101320 Apps targeting Android 12 or higher must explicitly  
declare the android:exported attribute for app components  
* QTBUG-102628 Application will crash if setWindowsIcon with a big ICON  
* QTBUG-102366 When filling a rect on a screen that has 150% scaling  
then it is possible that a line of pixels is not filled in  
* QTBUG-41138 Error in the function errorMessageFromComError  
* QTBUG-100802 [REG 6.2.2->6.2.3]Checkable QPushButton does not visually  
display checked state when toggled on macOS  
* QTBUG-102782 QPushButton setEnabled(false) doesn't grey out button  
* QTBUG-100997 Regression and UI Freeze (5.15 -> 6.2) in QTableView with  
Accessibility  
* QTBUG-103009 QML performance regression when accessibility is active  
* QTBUG-75106 Entries in the QAccessiblePluginsHash should be removed  
when a QQuickWindow is deleted  
* QTBUG-102493 [REG 6.2.2 -> 6.2.3] Keyboard layout resets to English  
* QTBUG-102640 [REGRESSION] Keyboard layout not respected for *some* key  
combinations  
* QTBUG-95933 Using scanner input IRcode will result in an error when  
second character is uppercase  
* QTBUG-102821 Global variable found in qeglfsx11integration.cpp  
* QTBUG-86823 REG: Blinking cursor leaving an artifact in QTextEdit  
* QTBUG-92468 QTextEdit cursor is drawn incorrectly  
* QTBUG-20894 QCompleter unexpectedly changes QLineEdit text  
* QTBUG-90442 QFileDialog::saveFileContent crashes on accept  
* QTBUG-95341 QLineEdit lineRect should use boundingRect height  
* QTBUG-59401 QFileDialog::setDefaultSuffix doesn't work when file path  
contains a dot  
* QTBUG-95463 QListView in view mode QListView::IconMode crashes when  
the last row is moved  
* QTBUG-96869 GTK file dialog is invisible if there is QTimer with 0  
interval in the main thread  
* QTBUG-92096 QMenu Scrollable  will  reset Active Action  
* QTBUG-95639 MariaDB 10.6 prepared queries metadata cache causes  
breakage in mysql driver  
* QTBUG-102334 QSettings / QDateTime incompatible when switching from  
Qt6 -> Qt5  
* QTBUG-86847 QXmlStreamReader.prefix() cannot return EndElement's  
prefix  
* QTBUG-94448 QtWidgets: Some stylesheets explode Designer and the whole  
linux terminal (recursion crash)  
* QTBUG-102952 tst_QNetworkReply::autoDeleteReplies* tests are flaky  
* QTBUG-102374 [REG:5.15.7->5.15.8]: repaint() on a widget makes  
QGraphicsOpacityEffect apply multiple times  
* QTBUG-101382 QtBase: Fix compiler warnings for QNX  
* QTBUG-100470 Undetected test crashes on Android  
* QTBUG-101888 tst_QGraphicsProxyWidget failing tests  
* QTBUG-86187 Ubuntu 20.04 has InsignificantTests configurations in the  
CI  
* QTBUG-95764 pure virtual call in QAccessibleQuickItem  
* QTBUG-102202 [REG:6.2.3->6.2.4]: Cannot use c++latest with qmake and  
MSVC  
* QTBUG-102129 LTS 5.15 fails to build with GCC 11 (C++17)  
* QTBUG-102447 tst_drawingmodes failed  
* QTBUG-102443 tst_QSocks5SocketEngine::passwordAuth fails with Ubuntu  
20.04 in lts-5.15  
* QTBUG-51327 [Windows 8.1]: After maximizing a window and toggling the  
frameless window hint and moving to another monitor then the window can  
be too big  
* QTBUG-93360 Compile Qt with gcc 11  
* QTBUG-102034 Merely subclassing QHeaderView causes it to lose built-in  
functionality  
* QTBUG-99545 App crashes in function QQmlPropertyCache::property(int)  
const on ARM 64bit  
* QTBUG-102594 [REG 5.15.6 -> 5.15.9] Many ANR issues by QtAccessibility  
  
### qtdeclarative  
* QTBUG-67950 Crash when changing Loader source inside a Repeater when  
the model changes  
* QTBUG-100431 Crash in libQt5Qml V4 engine caused by wrong memory  
access  
* QTBUG-101700 DelegateModel: using for ... of loop in JS to iterate  
DelegateModel.groups attached property causes a crash  
* QTBUG-102128 [REG] Offscreen render mode is broken in 5.15  
* QTBUG-95395 Code snippets for HoverHandler show TapHandler  
* QTBUG-101932 two HoverHandlers with different  
acceptedDevices/acceptedPointerTypes: cursorShape doesn't change  
accordingly  
* QTBUG-35995 Clicked signal not emitted on MouseArea when changing  
visibility and listening for doubleClicked  
* QTBUG-102158 Click signal not emitted in MouseArea after DoubleClicked  
is emitted and tab changed  
* QTBUG-103224 [read-only] marking is missing from acceptableInput  
property of TextInput QML type in the documentation  
* QTBUG-101628 Pinch gestures are not cancelled when pinch.accepted  
property is set to false on macOS.  
* QTBUG-100221 qtdeclarative compilation fails on arm64  
* QTBUG-100279 Building fails on Linux ARM64  
* QTBUG-98356 JIT crash on invalid yield syntax  
* QTBUG-83662 For MultiPointTouchArea with a child PinchArea multiple  
pressed signals for multiple touch points on mouse press  
* QTBUG-83413 Text rendering glitches in combination with loader and  
elide  
* QTBUG-88207 tst_qquicktext::fontSizeMode() failed on Ubuntu 20.04 in  
CI  
* QTBUG-101499 FAIL!  : tst_QQuickMultiPointTouchArea::nonOverlapping in  
Ubuntu_20_04  
  
### qtmultimedia  
* QTBUG-102316 [Reg: 5.15.7->5.15.8] App crashes by player() for QML  
MediaPlayer + VideoOutput with setAttribute (Qt::AA_UseOpenGLES)  
* QTBUG-102413 [REG:5.15.7->5.15.8]: Angle: Crash when running a video  
with qml Video component  
* QTBUG-60575 QtSpeech flite backend not working on Ubuntu Linux  
  
### qttools  
* QTBUG-101782 lrelease does not respect EXTRA_TRANSLATIONS in pro file.  
* QTBUG-102832 Qt Linguist incorrectly translates some language names  
  
### qtdoc  
* QTBUG-101320 Apps targeting Android 12 or higher must explicitly  
declare the android:exported attribute for app components  
  
### qtlocation  
* QTBUG-101765 Qt.labs.location is not built  
  
### qtconnectivity  
* QTBUG-101586 Bluetooth Android server asserts if disposed too quickly  
after listen()  
* QTBUG-101721 QBluetoothSocket double-emits connected() on macOS  
* QTBUG-102319 Android BT service discovery agent crash when stopped  
* QTBUG-102442 Bluetooth hostmode change Discoverable=>Connectable  
doesn't work on Android  
* QTBUG-70222 Qt  Bluetooth LE doesn't detect Battery services  
* QTBUG-98817 In QtConnectivity multiple QBluetooth autotest failures  
with macOS 12 ARM64  
  
### qtwayland  
* QTBUG-100148 Hover state of QCombobox has not been reset  
* QTBUG-102129 LTS 5.15 fails to build with GCC 11 (C++17)  
  
### qt3d  
* QTBUG-101556 FAIL!  : tst_GraphicsHelperGL4::bindFrameBufferAttachment  
in Ubuntu_20_04  
* QTBUG-99852 MacOS 12 fails with Qt3d: tst_vector4d_sse.cpp:78:14:  
error: no member named 'setY' in 'tst_Vector4D_SSE'  
  
### qtserialbus  
* QTBUG-101351 QModbusClient::processResponse() is never called  
  
### qtwebengine  
* QTBUG-103578 WebEngine: Error when linking gn  
* QTBUG-103618 WebEngine - Project ERROR: Unknown module(s) in QT:  
widgets  
* COIN-854 COIN set LIBRARY_PATH to non existing path , which causes ld  
warnings / errors  
* QTBUG-102192 Navigation on drop broken  
  
### qtquickcontrols2  
* QTBUG-94391 FileDialog unwanted uri suffix for Android11 SAF  
* QTBUG-100508 SEGFAULT Crash on  
QQuickOpenGLShaderEffectMaterial::updateTextures()  
* QTBUG-102036 Release and Clicked not fired for Buttons in ListView  
with pressDelay set with touch screen  
* QTBUG-102037 Invalid value of pressed property in ListView delegate  
* QTBUG-77202 No touch release event for AbstractButton inside of  
ListView with pressDelay set  
* QTBUG-102558 DialogButtonBox not regenerating layout on change of  
child Button width  
* QTBUG-84280 TextArea inside Flickable - cursor does not appear with  
LayoutMirroring.enabled  
  
### qtcharts  
* QTBUG-101945 Changing to QValueAxis::TicksDynamic on horizontal axes  
moves ticks to the opposite side  
  
### qtremoteobjects  
* QTBUG-72789 tst_modelreplicatest failed  
  
### qtquick3d  
* QTBUG-97714 Memory leak with Quick3D 5.15 when loading Texture with  
Loader  
  
Known Issues  
------------  
  
* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-5.15/supported-platforms.html  
  
* The RTA (release test automation) reported issues in Qt 5.15.x:  
https://bugreports.qt.io/issues/?filter=21874  
  
* Qt 5.15.10 Open issues in Jira:  
https://bugreports.qt.io/issues/?filter=24474  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Mike Achtelik  
Laszlo Agocs  
Viktor Arvidsson  
Vincent Baijot  
Nicholas Bennett  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
Tatiana Borisova  
Joerg Bornemann  
Assam Boudjelthia  
Michael Brüning  
Andreas Buhr  
Mitch Curtis  
Giuseppe D'Angelo  
David Faure  
Tang Haixiang  
Heikki Halmet  
Zhang Hao  
Andreas Hartmetz  
Jani Heikkinen  
Karsten Heimrich  
Ulf Hermann  
Volker Hilsheimer  
Allan Sandfeld Jensen  
Friedemann Kleint  
André Klitzing  
Michal Klocek  
Sze Howe Koh  
Fabian Kosmale  
Mike Krus  
Sona Kurazyan  
Jonas Kvinge  
Kai Köhne  
Thiago Macieira  
Samuel Mira  
Marc Mutz  
Antti Määttä  
Mårten Nordheim  
Sukyoung Oh  
Pasi Petäjäjärvi  
Timur Pocheptsov  
Joni Poikelin  
Liang Qi  
Topi Reinio  
André de la Rocha  
Dong Rui  
Fan RuiJie  
Shawn Rutledge  
Lars Schmertmann  
Tianlu Shao  
Andy Shaw  
Ivan Solovev  
Axel Spoerl  
Tarja Sundqvist  
Paul Olav Tvete  
Peter Varga  
Tor Arne Vestbø  
Alexander Volkov  
Ville Voutilainen  
Juha Vuolle  
Jaishree Vyas  
ChunLin Wang  
Edward Welbourne  
Clemens Werther  
Zhang Yu  
JiDe Zhang  
