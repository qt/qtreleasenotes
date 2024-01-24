Release note  
============  
  
Qt 5.15.13 long-term supported (LTS) commercial release is a patch  
release made on the top of Qt 5.15.12 (LTS). As a patch release,  
Qt 5.15.13 does not add any new functionality but provides bug fixes and  
other improvements. The release maintains both forward and backward  
compatibility (source and binary) with Qt 5.15.12.  
Source codes are available via the Qt online installer and  
the Qt Code Review tool (https://codereview.qt-project.org/). To get the  
sources via Qt Code Review, you need to log in with a Qt Account that  
has a valid commercial license. For detailed instructions, see  
https://wiki.qt.io/Qt_5.15_Release#Getting_Source_Codes.  
For detailed information about Qt, see the Qt 5.15 online documentation:  
https://doc.qt.io/qt-5/index.html.    
  
Important Changes  
-----------------  
  
### qtbase  
* a50b7f500c QNetworkRequest: Make header parsing locale-independent  
Fixed a bug where certain QNetworkRequest::KnownHeaders wouldn't be  
recognized as such in certain locales.  
  
* 6bb908bd61 PCRE2: upgrade to 10.42  
PCRE2 has been updated to 10.42.  
  
* 8509e0daae SQLite: Update SQLite to v3.40.0  
Updated SQLite to v3.40.0  
  
* 13752128e8 SQLite: Update SQLite to v3.40.1  
Updated SQLite to v3.40.1  
  
* 23cb910fd6 Update bundled libjpeg-turbo to version 2.1.5  
libjpeg-turbo was updated to version 2.1.5  
  
### qtdeclarative  
* f31d580492 Fix missing glyphs when using NativeRendering  
Fixed an issue where text using NativeRendering would sometimes be  
missing glyphs.  
  
### qtwayland  
* 28a0b1dc client: Fix infinite recursion with text-input-v2  
Fixed a possible crash when editing a field in an item view.  
  
### qtimageformats  
* 0527cee TGA Plugin: Fix reading of CMapDepth  
Fixed reading of TGA files with a non-zero X-origin  
  
* 8cfc422 Update bundled libwebp to version 1.3.0  
Update bundled libwebp to version 1.3.0  
  
* 1eaa734 Update bundled libtiff to version 4.5.0  
Bundled libtiff was updated to version 4.5.0  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-109169 Invalid QColorTrcLut use causes unreadable text with  
16-bit X11 visuals  
* QTBUG-86019 Serializing a null QTimeZone crashes  
* QTBUG-109226 Rare crashes in QXcbBackingStoreImage::flushPixmap  
* QTBUG-99601 ios: QMAKE_PRE_LINK Gives Error :Multiple commands produce  
* QTBUG-108848 iOS: Voice Control Accessibility feature breaks in iOS 16  
* QTBUG-88652 QTEST_FUNCTION_TIMEOUT and test function limit (5 minutes)  
are not documented.  
* QTBUG-107627 AndroidAssetsFileEngineHandler is broken  
* QTBUG-109026 Android: UI is scaled smaller than before  
* QTBUG-109732 Filelight crash on directory scan start  
* QTBUG-103393 IBus input method cannot set panel position correctly  
with DPI scaling  
* QTBUG-109477 QImageReader will cause heap corruption when load jpeg  
(width: 1px height:100px) on Apple M1  
* QTBUG-106653 Crash on Accessibility interface  
* QTBUG-104776 AndroidContentFileEngineIterator hangs when listing  
shared content with nested dirs  
* QTBUG-110066 Build fails on vulkan\qvulkanfunctions.h despite -no-  
vulkan is passed  
* QTBUG-63700 QSharedPointer missing documentation for move operators  
* QTBUG-64132 QToolButton should elide text when width constraints  
prevent from showing whole text  
* QTBUG-104948 QFileDialog::getOpenFileContent not honoring nameFilter  
* QTBUG-110627 Qt doesn't really follow Windows short time format  
* QTBUG-72103 Conversion between QQuaternion and Euler angles has issues  
in special cases  
* QTBUG-56595 QXcbConnection::getTimestamp() returns old timestamp  
* QTBUG-63324 iOS/macOS: system localization always returns english  
language  
* QTBUG-106569 Ctrl-C in QTreeView passes invalid QModelIndex to model  
when model is empty  
* QTBUG-109235 Review toupper/tolower uses [Qt]  
* QTBUG-107604 [Reg 5.15.10 -> 5.15.11] Incorrect fullscreen dimensions  
on some Android devices  
* QTBUG-107923 Wrong height of the window on Android  
* QTBUG-103054 FAIL!  : tst_Gestures::graphicsItemGesture in  
Ubuntu_20_04  
* QTBUG-105958 [Android] Intent + Talkback leads to deadlock  
* QTBUG-105804 The qt_ntfs_permission_lookup mechanism is prone to data  
races  
* QTBUG-110271 Copyright year not updated to 2023 on documentation  
* QTBUG-91627 [OpenGL] Crash when creating context with contextinfo  
example app on Android  
* QTBUG-109268 QWindow on Android doesn't use full area on some devices.  
* QTBUG-97503 Reg[5.15.2-5.15.6] Android: Keyboard covers the inputfield  
* QTBUG-109351 Bottom Navigation Bar overlaps app window  
* QTBUG-110501 Wrong calculation of display area on android when virtual  
keyboard is present before opening the app  
* QTBUG-36637 androiddeployqt puts *.qmltypes files into apk  
* QTBUG-110433 Material UI Controls not styled on Android  
  
### qtdeclarative  
* QTBUG-108713 Native font rendering in some cases misses letters  
* QTBUG-109140 [REG: 5->6] Slowly dragging Tumbler causes numbers to  
jump around  
* QTBUG-98792 Crash when using as-cast  
* QTBUG-109882 ShapePath: Switching from a transparent colour to a non-  
transparent one causes the wrong colour to be displayed  
* QTBUG-110286 SignalTransition::triggered can cause Segfault  
* QTBUG-87334 Graphical issue on some Android smartphones: white line at  
the top and the right side of the screen  
* QTBUG-111542 UI problem with iOS deployments  
* QTBUG-109235 Review toupper/tolower uses [Qt]  
* QTBUG-36637 androiddeployqt puts *.qmltypes files into apk  
* QTBUG-110433 Material UI Controls not styled on Android  
  
### qtactiveqt  
* QTBUG-109235 Review toupper/tolower uses [Qt]  
  
### qtmultimedia  
* QTBUG-59726 no access to second camera on android phones with dual  
front/back cameras  
* QTBUG-106897 Android QAudioRecorder pause does not work  
* QTBUG-105505 QMediaRecorder::Duration reports incorrect recording  
duration  
* QTBUG-110015 QML Video Example: example Crashing  
  
### qttools  
* QTBUG-109618 QtAttributionsScanner crashes frequently  
  
### qtdoc  
* QTBUG-110064 Android getting started doc instructs wrong JDK version  
for Qt5.15  
  
### qtconnectivity  
* QTBUG-111242 sdpscanner strcpy()s sdp_data_t::val::str into a fixed-  
size 1KiB buffer  
* QTBUG-86245 Neard link invalid and not mentionned in Licensed used in  
Qt  
  
### qtwayland  
* QTBUG-109302 Segmentation Fault with Wayland and QTreeWidget  
  
### qtquickcontrols  
* QTBUG-101973 File Dialog does not re open in some situation.  
  
### qtserialport  
* QTBUG-108450 REG: Qt 6.3.2 WinOverlappedNotifier possible crash  
  
### qtwebengine  
* QTBUG-109357 [REG 5.12 -> 5.15/6.x] QWebEngineUrlRequestInterceptor:  
Multiple redirects crashes the application  
* QTBUG-108240 WebEngine can't be built with MSVC 14.34 and LLVM 15.0.6  
* QTBUG-109273 Using client certificates leads to  
ERR_SSL_CLIENT_AUTH_NO_COMMON_ALGORITHMS  
* QTBUG-110504 Webengine extremely slow in loading webpage in debug  
build  
  
### qtcharts  
* QTBUG-107890 When changing the label of a legend marker it will not  
update until something else triggers an update  
* QTBUG-111293 tst_QBarSeries::mousehovered fails with SLES 15.4  
  
### qtscxml  
* QTBUG-109235 Review toupper/tolower uses [Qt]  
  
Known Issues  
------------  
  
* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-5.15/supported-platforms.html  
  
* The RTA (release test automation) reported issues in Qt 5.15.x:  
https://bugreports.qt.io/issues/?filter=21874  
  
* Qt 5.15.13 Open issues in Jira:  
https://bugreports.qt.io/issues/?filter=24811  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Laszlo Agocs  
Martin Andersson  
Mate Barany  
Nicholas Bennett  
Eskil Abrahamsen Blomfeldt  
Joerg Bornemann  
Assam Boudjelthia  
Michael Brüning  
Alexandru Croitor  
Giuseppe D'Angelo  
Alexey Edelev  
Oliver Eftevaag  
Christian Ehrlicher  
Andreas Eliasson  
Ilya Fedin  
Julian Greilich  
Heikki Halmet  
Ulf Hermann  
Volker Hilsheimer  
Allan Sandfeld Jensen  
Michal Klocek  
Sze Howe Koh  
Jarkko Koivikko  
Jani Korteniemi  
Fabian Kosmale  
Jonas Kvinge  
Kai Köhne  
Inho Lee  
Paul Lemire  
Robert Löhning  
Leena Miettinen  
Phan Quang Minh  
Samuel Mira  
Bartlomiej Moskal  
Marc Mutz  
Yuya Nishihara  
Roland Pallai  
Liang Qi  
Topi Reinio  
Andy Shaw  
Venugopal Shivashankar  
Ivan Solovev  
Axel Spoerl  
Tarja Sundqvist  
Lars Sutterud  
Jan Arve Sæther  
Morten Sørvig  
Sami Varanka  
Peter Varga  
Tor Arne Vestbø  
Jaishree Vyas  
Edward Welbourne  
Paul Wicking  
Jannis Xiong  
WANG Xuerui  
Andrey Yaromenok  
Yuhang Zhao  
