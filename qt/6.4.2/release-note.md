Release note  
============  
  
Qt 6.4.2 release is a patch release made on the top of Qt 6.4.1.  
As a patch release, Qt 6.4.2 does not add any new functionality but provides  
bug fixes and other improvements and maintains both forward and backward  
compatibility (source and binary) with Qt 6.4.1.  

For detailed information about Qt 6.4, refer to the online documentation  
included in this distribution. The documentation is also available online:  
  
https://doc.qt.io/qt-6/index.html  
  
The Qt version 6.4 series is binary compatible with the 6.3.x series.  
Applications compiled for 6.3 will continue to run with 6.4.  
  
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
* 04f6f4afa9 Update bundled zlib to version 1.2.13  
zlib was updated to version 1.2.13.  
  
* ff52558530 Update bundled libpng to version 1.6.39  
libpng was updated to version 1.6.39  
  
### qtdeclarative  
* 2b258e019e QQuickNinePatchImage: fix aliasing by respecting the smooth  
property  
The Imagine style now supports smooth scaling for 9-patch images when  
the QT_QUICK_CONTROLS_IMAGINE_SMOOTH environment variable is set to 1.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-108128 Absolute coordinates used for pointer events on wasm  
* QTBUG-106031 Mouse cursor location offset if canvas doesn't start at  
0,0  
* QTBUG-107687  [REG 6.3.1 -> 6.3.2] qt_add_resources with .qm  
translation files no longer rebuild generated .qrc when .qm files change  
* QTBUG-108113 "RCC: Cannot find file" in qt_add_translations  
* QTBUG-103470 [iOS] CMake translation handling fails  
* QTBUG-108103 QHostAddress::isEqual() with IPv6 determines valid ip to  
be any  
* QTBUG-46681 [REG 4.x->5.x] QPainter in paintEvent() doesn't work with  
Qt::WA_PaintOnScreen  
* QTBUG-100085 xcb: Native window does not get paint event if another  
window on top of it is hidden unless there is a enter/leave event  
somewhere  
* QTBUG-63324 iOS/macOS: system localization always returns english  
language  
* QTBUG-108186 Crash in qt_memrotate90 or qt_memrotate270  
* QTBUG-108156 Unhandled exception on QNetworkInformation::load()  
* QTBUG-89156 [REG 5.15.0->5.15.1] Focus is limitted after reparenting  
and adding widgets  
* QTBUG-108196 SecKeychain is deprecated [-Wdeprecated-declarations]  
when compiling qnetworkaccessmanager.cpp  
* QTBUG-67579 QT5 apps running natively under Wayland do not respect  
cursor size setting  
* QTBUG-87778 wayland: cursor size wrong  
* QTBUG-108194 FAIL!  : data::tst_simulation-behavior::compile() module  
"Simu" is not installed  
* QTBUG-108047 Setting macos style before creating a QApplication  
crashes  
* QTBUG-108218 [Win] Access violation in QNetworkListManagerEvents  
* QTBUG-107572 Expose QLineEdit focus for QComboBox editable  
* QTBUG-108344 Something is rotten with texture-based widgets that are  
native child widgets or are children of a native child widget  
* QTBUG-108277 QWidget::setParent calls q_evaluateRhiRecursive which is  
slow  
* QTBUG-105017 Crash in QRhiGles2::ensureContext with  
QT_WIDGETS_RHI_BACKEND=vulkan and QOpenGLWidget  
* QTBUG-106583 Windows and dialogs flashing white  
* QTBUG-108382 One more unhandled exception on  
QNetworkInformation::load()  
* QTBUG-108311 [REG: 6.3->6.4]: When moving a QDockWidget under certain  
environments it will trigger a warning message  
* QTBUG-106920 MOC cannot parse nested inline namespace (Parse error at  
"::")  
* QTBUG-108742 macdeployqt: Multimedia plugins missing  
* QTBUG-107057 macdeployqt does not include libdarwinmediaplugin.dylib  
* QTBUG-108605 Unhandled WinRT exception at  
QSystemLocalePrivate::uiLanguages()  
* QTBUG-105857 Qt application does not follow the DPI change when the  
DPI setting is changed before showing the first window  
* QTBUG-108709 [REG 6.4.0 -> 6.4.1] Second ColorRole change via  
QPalette:setBrush() does not modify cacheKey  
* QTBUG-107675 Typo in the document?  
* QTBUG-107806 Link is dead in the document  
* QTBUG-68175 tst_QWidget::raise is flaky  
* QTBUG-108743 QColor - Undefined symbols QColor::QColor(char const*),  
QColor::QColor(QString const&)...  
* QTBUG-108662 Can't build for Android  
* QTBUG-106025 REG: isSignalConnected creates a dead lock.  
* QTBUG-108764 tst_qwidgetrepaintmanager is flaky  
* QTBUG-108300 Crash when setPersistentGraphics(false),  
setPersistentSceneGraph(false) and visible: true on wayland  
* QTBUG-108677 macdeployqt tool does not copy networkinformation plugin  
* QTBUG-83185 [Android]: When using night or dark mode on a device, then  
the style extracted is still set as if it is light mode  
* QTBUG-87137 tst_QApplication::sendEventsOnProcessEvents() failed on  
Ubuntu 20.04/22.04 and RHEL 9  
* QTBUG-91255 [Android] Add support for APK Signature Scheme v2  
* QTBUG-108175 [macOS] Qt warning: "macOS generated a color-profile Qt  
couldn't parse. This shouldn't happen."  
* QTBUG-105735 Focus is not set to a child widget when a modal is open  
* QTBUG-107604 [Reg 5.15.10 -> 5.15.11] Incorrect fullscreen dimensions  
on some Android devices  
* QTBUG-107709 Android screen size mismatch [Reg 5.15.10 -> 5.15.11]  
* QTBUG-107523 [REG 5.15.10 -> 5.15.11] Android edge-to-edge layout  
broken  
* QTBUG-92468 QTextEdit cursor is drawn incorrectly  
* QTBUG-86823 REG: Blinking cursor leaving an artifact in QTextEdit  
* QTBUG-96288 QTextEdit cursor postion error when QTextEdit has  
different pointsize  
* QTBUG-109036 QImage mismatch in QXcbBackingStore  
* QTBUG-106906 tst_qtcuncurrentrun::pollForIsFinished occasionally  
crashes  
* QTBUG-108815 Installing qtdeclarative fails  
* QTBUG-103611 [Reg 5.15 -> 6.x] Re-initializing QGuiApplication causes  
QQmlApplicationEngine to crash  
* QTBUG-106393 Mac OS: Dot and Comma key combinations not working for  
russian layout  
  
### qtdeclarative  
* QTBUG-108026 Memory leak when capturing a 3D scene using  
QQuickItem::grabImage  
* QTBUG-106106 Crash in ~QQuickScrollBarAttached during rearrange of  
QQmlDelegateModel  
* QTBUG-71922 Mime data is corrupted when using QQuickDragAttached and  
it's not UTF-8  
* QTBUG-106940 "QML Import could not be resolved in any of the import  
paths: shared" when trying to QML debug example "emitters"  
* QTBUG-74496 Performance issue: rejected drag re-triggers drag enter  
event every frame while mouse moves  
* QTBUG-107989 Aliasing occurs at the image boundary if add Scale  
Animator to nine-patch image  
* QTBUG-107818 Sometimes ShaderEffect types are not be drawn correctly  
on 2 QQuickWindows  
* QTBUG-108252 Crash occurs when GUI thread accesses QRhi objects  
created by Renderer Thread  
* QTBUG-98979 ListView scrolling is broken for ListView.SnapOneItem mode  
* QTBUG-107774 madvise() terminates application due to EBADF code  
* QTBUG-106602 extending-qml example is missing QtQuick dependency in  
CMakeLists.txt  
* QTBUG-106884 Typo in the document  
* QTBUG-94619 Qt.labs.platform.Menu opens at the wrong location with  
scaling enabled  
* QTBUG-94783 Popup menu in incorrect position when using  
QT_SCALE_FACTOR=1.5 on Wayland Ubuntu  
* QTBUG-108298 Crash using ConicalGradient in a ShapePath  
* QTBUG-108352 tst_touchmouse::strayTouchDoesntAutograb is flaky  
* QTBUG-108549 PinchHandler.scale loses the accumulated scaling if  
target == null  
* QTBUG-92064 PinchHandler target scale jumps when pinching a second  
time via native gesture  
* QTBUG-104890 PointHandler deactivated on touch screen  
* QTBUG-108627 Assertion in QQmlPropertyData::setOverrideIndex  
* QTBUG-106875 Segfault when Loader is trying to load a file that  
contains the Loader  
* QTBUG-108646 Segmentation fault when inspecting QML objects without  
breaking  
* QTBUG-83890 [REG 5.14.1->5.14.2,5.15] Horizontal Scrollbars in  
ScrollView when Flickable fits  
* QTBUG-108388 code snippet in the document is incomplete  
* QTBUG-108820 Infinity - real vs int  
* QTBUG-108634 Invalid code generated for comparison  
* QTBUG-108651 Property change detection for null values doesn't seem to  
be working  
* QTBUG-108683 [Reg 5.15.2/6.3.2 -> 6.4.x] DropShadow: Changing radius  
at runtime also changes Z-order  
* QTBUG-107607 Crash when trying to inspect "this.parent"  
* QTBUG-108913 ->6.4.1: Restore qmllint JSON Output Message  
* QTBUG-108697 Program can crash when Connections target is destroyed  
* QTBUG-109010 top-level build: automoc broken yet again in 6.4 branch  
(depending on moc before it's built)  
* QTBUG-104047 Qt Quick: Drag event coordinates wrong in Release mode  
* QTBUG-104716 draganddrop example issues  
* QTBUG-109002 [PinchHandler] Dragging a target is not functional  
* QTBUG-107171 qmlsc: Cannot resolve type annotations for args of type  
list<T>  
* QTBUG-98130 QtQuick and controls examples use qt_add_resources to add  
QML files  
* QTBUG-107850 Crash on QQuickItem destruction  
* QTBUG-106864 Reg-5.15.9->5.15.10: Android crash on startup on armv7  
(32bit) devices  
* QTBUG-106269 Qt Quick apps immediately crash under Android 6  
  
### qtmultimedia  
* QTBUG-108009 QML Camera maximumZoomFactor in iPad  
* QTBUG-108027 Signal videoFrameChanged not emitted  
* QTBUG-95127 QMediaPlayer::setVideoOutput() no longer takes QList of  
outputs  
* QTBUG-103238 [macOS] Crash in qt_convert_NV12_to_ARGB32  
* QTBUG-107671 Using strcmp instead of gst's methods for classfying  
classes  
* QTBUG-108187 QAudioSink can not be moved to another thread  
* QTBUG-108898 [Windows] Crash on  
QWindowsMediaDevices::availableDevices()  
* QTBUG-109009 Ffmpeg: videotoolbox doesn't support some yuv 8bit  
formats  
* QTBUG-107678 audio device has unknown channel  
* QTBUG-108020 QMediaDevices on MacOS needs additional listeners to  
correctly catch device changes  
* QTBUG-108018 Camera Example crashes on macOS 13 ventura  
* QTBUG-103567 QML MediaPlayer fails to playback rtsp media properly.  
  
### qttools  
* QTBUG-108243 Naming menu separators in design view is broken  
* QTBUG-94365 QDoc: "error code: 4" from clang on macOS  
* QTBUG-108353 qdoc: QHash related warnings with LLVM 15.0.0  
* QTBUG-96239 Document CMake component in CMake function documentation  
  
### qtdoc  
* QTBUG-108513 Disappearing text on a Button on QtQuick Controls when  
the Dark theme is active on macOS  
* QTBUG-108101 String "6.4.0" found in Qt6.4.1 sources  
* QTBUG-108670 doc state, that QOpenGLWidget is not supported, but it  
was fixed in qt 6.4  
* QTBUG-108335 calqlatr demo buttons are broken  
  
### qtwayland  
* QTBUG-104259 tst_seatv4 tests are failing with Ubuntu 22.04 Wayland  
* QTBUG-75919 Override cursor has no precedence on Wayland  
  
### qt3d  
* QTBUG-56368 Crash when using async NodeInstantiator within Scene3D  
* QTBUG-106972 QRenderCapture leaks memory with RHI renderer  
* QTBUG-107693 tst_QResourceManager received signal 11 (SIGSEGV) with  
Ubuntu 22.04 QEMU  
  
### qtserialbus  
* QTBUG-107132 Typo in the document?  
  
### qtwebsockets  
* QTBUG-108276 MQTT WebSocket doesn't connect  
  
### qtwebengine  
* QTBUG-108265 Pasting plain text does not work on Discord web  
* QTBUG-108843 [WebRTC] Crash inside  
RTCStatsCollector::ProduceAudioRTPStreamStats_n  
  
### qtvirtualkeyboard  
* QTBUG-108030 Virtual keyboard basic example freezes on Android  
* QTBUG-108396 The link in the document seems to be wrong  
  
### qtspeech  
* QTBUG-108381 qtspeech does not compile without qtqml  
* QTBUG-108205 tst_QTextToSpeech::pauseResume(darwin) fails on macOS 13  
in CI  
  
### qtquick3d  
* QTBUG-108078 CustomMaterial texture min filter can't be changed  
* QTBUG-96302 3D scenes with 2D subtrees leak graphics resources upon  
destroying the scene  
* QTBUG-106032 If you start an application with View3D not visible from  
one state, it's impossible to get it visible then.  
* QTBUG-86716 Materials shared between views don't always render  
* QTBUG-108811 Skinned mesh doesn't follow skeleton  
* QTBUG-108606 All View3D instances where material is used are not  
updated when material color changes  
* QTBUG-107780 Rendering Texture in WebAssembly  
* QTBUG-107841 tst_Input crashes a lot  
* QDS-8024 Icons needed for new component library items  
* QTBUG-109157 QtQuick3D fails to compile with C++20 : allocator.destroy  
called in qtquick3d/src/3rdparty/embree//common/sys/vector.h:137  
  
### qtshadertools  
* QTBUG-107483 Typo in the document?  
  
### qtmqtt  
* QTBUG-108276 MQTT WebSocket doesn't connect  
  
### qtquick3dphysics  
* QTBUG-108897 QFATAL : tst_physicsscene::UnknownTestFunc() ASSERT  
* QTBUG-108667 libcooker installed in PREFIX/bin  
  
Known Issues  
------------  
  
* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-6.4/supported-platforms.html  
* RTA reported issues from Qt 6.4  
https://bugreports.qt.io/issues/?filter=24174  
* See Qt 6.4 known issues from:  
https://wiki.qt.io/Qt_6.4_Known_Issues  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Laszlo Agocs  
Vladimir Belyavsky  
Nicholas Bennett  
Tim Blechmann  
Mikolaj Boc  
Joerg Bornemann  
Assam Boudjelthia  
Aurélien Brooke  
Michael Brüning  
Hxcan Cai  
Alexandru Croitor  
Mitch Curtis  
Thibaut Cuvelier  
Giuseppe D'Angelo  
Artem Dyomin  
Alexey Edelev  
Oliver Eftevaag  
Hatem ElKharashy  
Andreas Eliasson  
Ilya Fedin  
Nicolas Fella  
Josep M. Ferrer  
Jan Grulich  
Richard Moe Gustavsen  
Lucie Gérard  
Tang Haixiang  
Heikki Halmet  
Jani Heikkinen  
Miikka Heikkinen  
Ulf Hermann  
Volker Hilsheimer  
Allan Sandfeld Jensen  
Jonas Karlsson  
Johannes Kauffmann  
Timothée Keller  
Friedemann Kleint  
Michal Klocek  
Jarkko Koivikko  
Janne Koskinen  
Fabian Kosmale  
Konrad Kujawa  
Santhosh Kumar  
Kai Köhne  
Inho Lee  
Paul Lemire  
Thiago Macieira  
Ievgenii Meshcheriakov  
Phan Quang Minh  
Samuel Mira  
Fawzi Mohamed  
Bartlomiej Moskal  
Marc Mutz  
Mårten Nordheim  
Dennis Oberst  
Bumjoon Park  
Evgen Pervenenko  
Samuli Piippo  
Timur Pocheptsov  
Milla Pohjanheimo  
Lorn Potter  
Liang Qi  
David Redondo  
Topi Reinio  
Alexey Rochev  
Niclas Rosenvik  
Shawn Rutledge  
Sami Shalayel  
Axel Spoerl  
Piotr Srebrny  
Christian Stenger  
Christian Strømme  
Tasuku Suzuki  
Jan Arve Sæther  
Morten Sørvig  
U-GER\tjmaciei  
Peter Varga  
Doris Verria  
Tor Arne Vestbø  
Ville Voutilainen  
Ole Wegen  
Edward Welbourne  
Fushan Wen  
Oliver Wolff  
Semih Yavuz  
Vlad Zahorodnii  
Yuhang Zhao  
