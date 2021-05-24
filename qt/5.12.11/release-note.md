Release note  
============  
Qt 5.12.11 release is a patch release made on the top of Qt 5.12.10.  
As a patch release, Qt 5.12.11 does not add any new functionality but provides  
bug fixes and other improvements and maintains both forward and backward  
compatibility (source and binary) with Qt 5.12.10.  
  
For detailed information about Qt 5.12, refer to the online documentation  
included in this distribution. The documentation is also available online:  
  
  https://doc.qt.io/qt-5.12/index.html  
  
The Qt version 5.12 series is binary compatible with the 5.11.x series.  
Applications compiled for 5.11 will continue to run with 5.12.  
  
Some of the changes listed in this file include issue tracking numbers  
corresponding to tasks in the Qt Bug Tracker:  
  
  https://bugreports.qt.io/  
  
Each of these identifiers can be entered in the bug tracker to obtain more  
information about a particular change.  
  
Important Changes  
-----------------  
  
### qtbase  
* f411be7a4a sqlite: Upgrade to 3.33.0  
Upgraded to v3.33.0  
  
* 47a842ee0c Fix included license text for PCRE2 - Stack-less Just-In-  
Time Compiler  
Changed license text of "PCRE2 - Stack-less Just-In-Time Compiler"  
component. The documentation (incorrectly) included the generic PCRE2  
license so far.  
  
* e2c0cc9bb3 Avoid integer overflow and division by zero  
Pen patterns are restrained to a maximum length and values of 1024,  
fixing oss-fuzz issue 25310.  
  
* 0943ad0241 Containers: call constructors even for primitive types  
The semantics of Q_PRIMITIVE_TYPE have been slightly changed. Qt now  
value-initializes types marked as primitive (which, by default, include  
trivial types) instead of simply using memset(0), which is wrong in some  
corner cases.  
  
* 5d33ae6d94 Update bundled libjpeg-turbo to version 2.0.6  
libjpeg-turbo was updated to version 2.0.6  
  
* f464d4f75a Update bundled libjpeg-turbo to version 2.0.6  
libjpeg-turbo was updated to version 2.0.6  
  
* 391c9f6e66 Update bundled libjpeg-turbo to version 2.1.0  
libjpeg-turbo was updated to version 2.1.0  
  
### qtwayland  
* b2ee9ff3 Client: Fix reverse screen order  
Fixed a bug where QGuiApplication::screens() and primaryScreen() would  
return initial screens in the reverse order they were added by the  
compositor. QGuiApplication::primaryScreen() will now return the first  
output added by the compositor.  
  
* 8fe61d79 Fix leaked subsurface wayland items  
Fixed a memory leak when creating subsurfaces.  
  
### qtimageformats  
* 7addba2 Update bundled libtiff to version 4.2.0  
Bundled libtiff was updated to version 4.2.0  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-86718 qmake cannot run target compiler for iOS Xcode 12  
* QTBUG-85594 Race in QFseventsFileSystemWatcher destructor  
* QTBUG-87659 qwindow.cpp fails to build  
* QTBUG-88247 Memory ordering problem in QBasicMutex::lockInternal()  
* QTBUG-88512 Use-after-free in QXcbConnection::initializeScreens()  
* QTBUG-87014 Qt application gets stuck trying to open main window under  
Big Sur  
* QTBUG-86976 Input method widget is closed on destructing a widget  
* QTBUG-88600 SystemTrayIcon icon too big /squashed on second screen  
(Big Sur)  
* QTBUG-88435 QXcbConnection::getTimestamp runs in indefinite loop when  
X server shuts down  
* QTBUG-88288 QScroller crashes on certain screen and/or window  
arrangements  
* QTBUG-66448 Android KEYCODE_MEDIA_PLAY_PAUSE is incorrectly translated  
to Qt.Key_MediaPlay in QML  
* QTBUG-89547 Comparison of QSslCertificate broken (extensions()  
crashes)  
* QTBUG-91223 qt_memrotate270, qt_memrotate180 , qt_memrotate90,  
segfaults  
* QTBUG-75319 [REG 5.12.1 -> 5.12.2] QApplication::clipboard()->text()  
call blocks execution for ~5 seconds sometimes  
* QTBUG-87078 xcb: showMaximized() in full screen only restores the  
window with some WMs  
* QTBUG-91770 qvnc: Arbitrary memory read vulnerability  
* QTBUG-89172 Integer-overflow in QFixed::fromReal(qreal r) through  
QImage::.loadFromData(QByteArray);  
* QTBUG-89899 Integer-overflow in QFixed::QFixed  
* QTBUG-93779 [elxr] (error #412) unresolved symbols: 1  
* QTBUG-74287 QLocale::nativeCountryName does not use country  
information from locale object  
* QTBUG-84096 FreeType: crash with unicode Variation Selector-16  
* QTBUG-87803  
QStandardPaths::writableLocation(QStandardPaths::GenericDataLocation)  
points to an inaccessible location  
* QTBUG-68338 Qt shouldn't create or change the permission of  
XDG_RUNTIME_DIR  
* QTBUG-75786 macOS 10.14 autotest failures  
* QTBUG-82617 Crash on exit via back button on Huawei Mate 20 Pro  
  
### qtsvg  
* QTBUG-87583 SVG icons with with <DOCTYPE svg> not loading  
* QTBUG-91507 Out of bounds read in function  
`QRadialFetchSimd<QSimdSse2>::fetch` when input craft svg file  
  
### qtdeclarative  
* QTBUG-86402 [REG 5.12 -> 5.13] Animation in Popup causes app's crash  
after Popup closed  
* QTBUG-86676 QML garbage collector doesn't work correctly with Loader  
* QTBUG-87228 When running Valgrind/Leak Sanitizer there are indications  
that there are problems with the property cache  
* QTBUG-91867 TextInput cursorDelegate position not updated after left  
padding change  
* QTBUG-90401 Heap-use-after-free in QAbstractAnimationJob  
* QTBUG-46350 Crash when deleting item currently set in PropertyChanges  
target  
  
### qtwayland  
* QTBUG-81657  Snapdragon 820A /Wayland: The handling of  
QEvent::UpdateRequest hangs when QQuickItem::update() is not scheduled  
on time  
* QTBUG-88782 Wayland compositor memory leak  
  
### qtwebengine  
* QTBUG-76181 Segfault in  
QtWebEngineCore::DelegatedNodeTreeUpdater::setupTextureContentNode  
* QTBUG-72368 Mac : QtWebEngine crashes in case the system volume  
formatting is 'case-sensitive'  
  
### qtquickcontrols2  
* QTBUG-83698 Using Keys.onReturnPressed from Button to open Menu causes  
the first MenuItem to get triggered on show  
  
### qtvirtualkeyboard  
* QTBUG-85554 When the Qt Virtual Keyboard is rendered in Wayland  
compositor, QInputMethod::keyboardRectangle() doesn’t return correct  
values  
  
### qtremoteobjects  
* QTBUG-82284 TestModelView::testDataInsertionTree fails for Windows 7  
* QTBUG-84640 Disconnected ExternalIODevice Not Handled  

Known Issues  
------------

* RTA reported issues from Qt 5.12 LTS:  
https://bugreports.qt.io/issues/?filter=22251

Credits for the  release goes to:  
---------------------------------  
  
Aavitsland Eirik  
Avtomonov Nikolay  
Blomfeldt Eskil Abrahamsen  
Bornemann Joerg  
Bruhin Florian  
Brüning Michael  
Buddenhagen Oswald  
Burtsev Kirill  
Chuan Wang  
Curtis Mitch  
D'Angelo Giuseppe  
Duivenvoorde Richard  
Dushistov Evgeniy A.  
Fella Nicolas  
Goldstein Maximilian  
Golubev Andrei  
Heikkinen Jani  
Helsing Johan Klokkhammer  
Hermann Ulf  
Jensen Allan Sandfeld  
Kartashov Alexander  
Keller Christoph  
Koehne Kai  
Koivikko Jarkko  
Kokko Antti  
Kosmale Fabian  
Kudryavtsev Anton  
Kurazyan Sona  
Kushnir Igor  
Kyzivat Keith  
Loehning Robert  
Macieira Thiago  
Mao Sheng  
Mikolajczyk Piotr  
Pocheptsov Timur  
Qi Liang  
Rabiei Soroush  
Ranghetti Luiz Fernando  
Samir Ahmad  
Shaw Andy  
Stottlemyer Brett  
Suzuki Tasuku  
Sørvig Morten Johan  
Verbruggen Erik  
Vestbø Tor Arne  
Vogt Fabian  
Volgutov Valery  
Volkov Alexander  
Voutilainen Ville  
Wang Wenjia  
Welbourne Edward  
Xinwei Li  
