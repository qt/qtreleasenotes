Release note  
============  
  
Qt 5.15.12 release is a patch release made on the top of Qt 5.15.11. As a patch  
release, Qt 5.15.12 does not add any new functionality but provides bug fixes  
and other improvements.  
  
For detailed information about Qt, see the Qt 5.15 online documentation:  
https://doc.qt.io/qt-5/index.html.    
  
Important Changes  
-----------------  
  
### qtbase  
* 25be15e7d7 Update bundled libpng to version 1.6.38  
libpng was updated to version 1.6.38  
  
* 9374d96406 Update bundled zlib to version 1.2.13  
zlib was updated to version 1.2.13.  
  
* 59845d680c Update bundled libpng to version 1.6.39  
libpng was updated to version 1.6.39  
  
* e48e2ed9d7 macOS: Fix less common writing systems on Catalina and  
later  
Fixed missing text with certain writing systems on macOS Catalina and  
later.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-92199 [REG] The color of QLineEdit and QPlainTextEdit  
placeholder text is not grayed-out if stylesheet was applied  
* QTBUG-93009 QPalette::PlaceholderText color is not followed after  
setting color in a style sheet  
* QTBUG-104917 QStyleSheetStyle::drawPrimitive(QStyle::PE_PanelLineEdit)  
crashes with widget==nullptr  
* QTBUG-107263 QVector::toList() example mistake  
* QTBUG-107038 Non-aliased Text is rendered incorrectly using  
NativeRendering  
* QTBUG-107719 Typo in the document?  
* QTBUG-79977 QMessageBox does not work at  IOS 13  
* QTBUG-85773 QML TextEdit copy() copies text twice on Android  
* QTBUG-47979 QDesktopServices is unable to open a file on Android  
* QTBUG-103852 QDir fails for paths of length over 260 characters  
* QTBUG-106713 android.bundle.enableUncompressedNativeLibs=false  
deprecated in Android Gradle plug-in ver 8.0  
* QTBUG-104085 QJsonValue::toObject(const QJsonObject &defaultValue) and  
QJsonValue::toArray(const QJsonArray &defaultValue) parse empty default  
values incorrectly  
* QTBUG-104930 QLocale shows German text for "en_DE"  
* QTBUG-107673 [REG]Blank button box on MacOS  
* QTBUG-108103 QHostAddress::isEqual() with IPv6 determines valid ip to  
be any  
* QTBUG-46681 [REG 4.x->5.x] QPainter in paintEvent() doesn't work with  
Qt::WA_PaintOnScreen  
* QTBUG-100085 xcb: Native window does not get paint event if another  
window on top of it is hidden unless there is a enter/leave event  
somewhere  
* QTBUG-108186 Crash in qt_memrotate90 or qt_memrotate270  
* QTBUG-67579 QT5 apps running natively under Wayland do not respect  
cursor size setting  
* QTBUG-87778 wayland: cursor size wrong  
* QTBUG-96384 Tagalog cannot be displayed correctly  
* QTBUG-98920 Font fallback is not working properly on macOS  
* QTBUG-108662 Can't build for Android  
* QTBUG-90611 Shortcut Alt+` is not working with non US layout  
* QTBUG-101680 MySQL plugin: QSqlQuery::prepare + exec no results when  
table contains JSON type  
* QTBUG-41170 [Android]: When the window resizes then there it will  
cause flicker  
* QTBUG-85248 Qt warning  
"QHttpNetworkConnectionPrivate::_q_hostLookupFinished could not de-queue  
request, failed to report HostNotFoundError"  
* QTBUG-91882 eglfs with a cloned screen cause app to flicker  
* QTBUG-106896 QDir::drive() does not shows DVD drive  
* QTBUG-98988 Qt bugs when portal implementation is not available  
* QTBUG-87137 tst_QApplication::sendEventsOnProcessEvents() failed on  
Ubuntu 20.04/22.04 and RHEL 9  
* QTBUG-107604 [Reg 5.15.10 -> 5.15.11] Incorrect fullscreen dimensions  
on some Android devices  
* QTBUG-107709 Android screen size mismatch [Reg 5.15.10 -> 5.15.11]  
* QTBUG-107523 [REG 5.15.10 -> 5.15.11] Android edge-to-edge layout  
broken  
* QTBUG-108556 FAIL!  : tst_QTimer::zeroTimer in Ubuntu 20.04 and SLES  
15.4  
* QTBUG-107727 QSystemTrayIcon does not emit the  
QSystemTrayIcon::activated signal on Ubuntu 20.04/22.04 for left click  
and right click.  
* QTBUG-91255 [Android] Add support for APK Signature Scheme v2  
* QTBUG-109022 FAIL!  : tst_QFtp::initTestCase in Ubuntu_20_04  
  
### qtdeclarative  
* QTBUG-106864 Reg-5.15.9->5.15.10: Android crash on startup on armv7  
(32bit) devices  
* QTBUG-106269 Qt Quick apps immediately crash under Android 6  
* QTBUG-107255 [Android 5.15.11] module "QtGraphicalEffects" is not  
installed  
* QTBUG-107038 Non-aliased Text is rendered incorrectly using  
NativeRendering  
* QTBUG-106645 "TypeError: Cannot read property of null" error in "QML  
Dynamic View Ordering Tutorial 1" example  
* QTBUG-107795 Reg-5.15.10->5.15.11 Setting property on TextField  
crashes  
* QTBUG-106457 Assert on invalid code  
* QTBUG-102793 [REG: 5.13->5.14] Bindings in delegates get triggered  
multiple times if delegate and/or model is changed  
* QTBUG-107732 Tumbler sometimes ignores specified index  
* QTBUG-107774 madvise() terminates application due to EBADF code  
* QTBUG-108298 Crash using ConicalGradient in a ShapePath  
* QTBUG-106875 Segfault when Loader is trying to load a file that  
contains the Loader  
* QTBUG-109002 [PinchHandler] Dragging a target is not functional  
* QTBUG-108258 FAIL!  : tst_qquickbehaviors::currentValue in MacOS_12  
* QTBUG-106520 FAIL!  :  
qtquickcontrols::Tests_StackLayout::test_addAndRemoveItems in  
Ubuntu_20_04  
* QTBUG-106521 FAIL!  :  
qtquickcontrols::Tests_StackLayout::test_addAndRemoveItems in MacOS_12  
* QTBUG-108880 FAIL!  : tst_qquickanimations::reparent in MacOS_12  
* QTBUG-107619 V4: Memory corruption due to unchecked length usage  
  
### qtmultimedia  
* QTBUG-105381 Qt Multimedia fails to read crop info from a HEVC video  
stream's VPS.  
* QTBUG-106059 Ended video shows does not follow VideoOutput size  
changes  
* QTBUG-76205 WMF: When playing videos of a certain MP4 type then  
occasionally it will only show the main color and not the whole video  
* QTBUG-96746 Switching between external camera and built-in webcam  
flips the VideoOutput 180 degrees  
* QTBUG-108018 Camera Example crashes on macOS 13 ventura  
  
### qtdoc  
* QTBUG-107245 Typo in the document?  
  
### qtlocation  
* QTBUG-107580 [REG 5.15.10 -> 5.15.11], PositionSource: last known  
position is never read  
* QTBUG-103478 QGeoPositionInfoSource on Android always asks for  
location permission  
  
### qtwayland  
* QTBUG-104259 tst_seatv4 tests are failing with Ubuntu 22.04 Wayland  
* QTBUG-103378 Some return values are ignored, causing warnings  
* QTBUG-107076 Copying image data from Qt aplications is still broken on  
GNOME Wayland  
* QTBUG-75919 Override cursor has no precedence on Wayland  
  
### qt3d  
* QTBUG-105376 Qt Quick Text gets correupted when a Qt3D ShaderProgram's  
shader loads multipule textures  
* QTBUG-56368 Crash when using async NodeInstantiator within Scene3D  
* QTBUG-108918 FAIL!  : tst_RayCasting::shouldReturnAllResults in  
Ubuntu_20_04  
  
### qtimageformats  
* QTBUG-107040 Tiff images with LZW compression do not work in debug  
builds  
* QTBUG-107223 Massive memory consumption when loading TIFF image  
  
### qtquickcontrols  
* QTBUG-106520 FAIL!  :  
qtquickcontrols::Tests_StackLayout::test_addAndRemoveItems in  
Ubuntu_20_04  
* QTBUG-106521 FAIL!  :  
qtquickcontrols::Tests_StackLayout::test_addAndRemoveItems in MacOS_12  
  
### qtwebengine  
* QTBUG-108207 Mac: errors building Qt 6.3.2 with Xcode 14.1  
  
### qtvirtualkeyboard  
* QTBUG-98750 [VKB] AutoScroller does not work in the basic virtual  
keyboard example  
* QTBUG-83217 rotation of virtualkeyboard does not work  
* QTBUG-105371 [Virtual keyboard] The fallback to layouts/fallback is  
not mentioned  
  
### qtscxml  
* QTBUG-80262 SCXML StateMachine state properties get incorrect values  
if History is used  
  
### qtquick3d  
* QTBUG-97680 Reloading View3D will lead memory leak in 5.15  
  
### qtmqtt  
* QTBUG-92817 QMqttTopicFilter also matches topics just starting with  
the filter name  
  
### qtopcua  
* QTBUG-104646 [C++20 FTBFS] open62541.h is running afoul of volatile  
compound statement deprecation in C++20  
  
Known Issues  
------------  
  
* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-5.15/supported-platforms.html  
  
* The RTA (release test automation) reported issues in Qt 5.15.x:  
https://bugreports.qt.io/issues/?filter=21874  
  
* Qt 5.15.12 Open issues in Jira:  
https://bugreports.qt.io/issues/?filter=24555  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Laszlo Agocs  
Eskil Abrahamsen Blomfeldt  
Assam Boudjelthia  
Michael Brüning  
Andrey Butirsky  
Artem Dyomin  
Alexey Edelev  
Christian Ehrlicher  
Hatem ElKharashy  
Ilya Fedin  
Jan Grulich  
Heikki Halmet  
Ulf Hermann  
Dominik Holland  
Janne Juntunen  
Maurice Kalinowski  
Jonas Karlsson  
Timothée Keller  
Fabian Kosmale  
Kai Köhne  
Inho Lee  
Paul Lemire  
Thiago Macieira  
Ievgenii Meshcheriakov  
Samuel Mira  
Marc Mutz  
Mårten Nordheim  
Dennis Oberst  
Timur Pocheptsov  
Liang Qi  
André de la Rocha  
Shawn Rutledge  
Ivan Solovev  
Axel Spoerl  
Christian Strømme  
Tarja Sundqvist  
Jan Arve Sæther  
Sami Varanka  
Doris Verria  
Ville Voutilainen  
Juha Vuolle  
Ole Wegen  
Edward Welbourne  
Paul Wicking  
Vlad Zahorodnii  
