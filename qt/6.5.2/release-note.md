Release note  
============  
Qt 6.5.2 release is a patch release made on the top of Qt 6.5.1.  
As a patch release, Qt 6.5.2 does not add any new functionality but provides  
bug fixes and other improvements and maintains both forward and backward  
compatibility (source and binary) with Qt 6.5.1.  

For detailed information about Qt 6.5, refer to the online documentation  
included in this distribution. The documentation is also available online:  
  
https://doc.qt.io/qt-6/index.html  
  
The Qt version 6.5 series is binary compatible with the 6.4.x series.  
Applications compiled for 6.4 will continue to run with 6.5.  
  
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
* 9e7f1f3e57 Fix QMenu (+other theme) sizes on Windows multiscreen  
systems  
Fixed menu sizes on Windows systems with more screens.  
  
* 65528387dc Revert commit "don't ever force fork() instead of forkfd()"  
Reverted a change from Qt 6.0 that made the childProcessModifier()  
callback be run in a child created by means other than a real fork()  
library call, a situation in which certain other library functions would  
be unusable, unreliable, or cause deadlocks. A flag to opt in to the  
solution with better performance will be added to Qt 6.6.  
  
* a2dc11b37f QDnsLookup/Unix: make sure we don't overflow the buffer  
Fixed a bug that could cause a buffer overflow in Unix systems while  
parsing corrupt, malicious, or truncated replies.  
  
* 8eb2be3bb2 SQLite: Update SQLite to v3.42.0  
Updated SQLite to v3.42.0  
  
* b5982b6525 QProcess/Linux: fix file descriptor leak in case of failed  
child start  
Fixed a file descriptor leak in QProcess when running on Linux 5.4 or  
later, if the executable being run failed to start (for example, the  
file for the executable didn't exist).  
  
* 24dfb9176f QVariant::fromStdVariant(): protect against accidental  
fromValue() ADL pick-ups  
The fromStdVariant() function used an unqualifed fromValue() call to  
convert each alternative type in the std::variant. It now uses qualified  
QVariant::fromValue() to avoid picking up unrelated fromValue()  
overloads whose return value just happens to implicitly convert to  
QVariant.  
  
* 492aafd8a7 Generate and set a CFBundleIdentifier when none were  
provided on macOS  
When using Ninja generator, if neither  
`XCODE_ATTRIBUTE_PRODUCT_BUNDLE_IDENTIFIER` nor  
`MACOSX_BUNDLE_GUI_IDENTIFIER` is provided for a target, a bundle  
identifier, i.e., `com.yourcompany.<teamid>.<target>` will be generated  
and set as CFBundleIdentifier.  
  
* 238c30a4a6 QPixmapCache: fix leaking of QStrings and Keys on clear()  
Fixed QString key data not being freed on clear().  
  
* 991d0acf3b Freetype: Don't do image transform for translations  
Fixed an issue where setting a translation matrix on text using a  
bitmap font would cause rendering artifacts.  
  
* 7bdd6247ad QGtk3Theme: Do not default Active WindowText to button  
foreground  
Default to GTK Entry Text / Normal Text / qt_fusionPalette  
  
* 533df7144d Update bundled libpng to version 1.6.40  
libpng was updated to version 1.6.40  
  
### qtdeclarative  
* 8b1ad3c03a Material: fix clipped floating placeholder text  
The outlined TextArea now sets topInset by default if it or its  
Flickable parent clips. This avoids the floating placeholder being  
clipped in those cases. The outlined TextField sets topInset by default  
only if the TextField itself clips.  
  
* e7e9120d61 Remove the 'qml-devtools' feature  
The 'qml-devtools' feature is removed. All tools that depend on this  
feature are mandatory and need to be build unconditionally.  
  
### qttools  
* b009d54bf Qt Designer: Add QFont::HintingPreference to property editor  
Support for the QFont::HintingPreference property has been added.  
  
### qtpositioning  
* 697f2dbb CoreLocation plugin: introduce RequestAlwaysPermission  
parameter  
Introduce an explicit RequestAlwaysPermission parameter to the  
corelocation plugin. When specified and set to true, this parameters  
enables the "Always" location request. When not specified or set to  
false, only the "When In Use" location permission is requested. By  
default this parameter is not specified.  
  
### qtimageformats  
* 0443293 Update bundled libtiff to version 4.5.1  
Bundled libtiff was updated to version 4.5.1  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-111509 WASM: recent accessibility work breaks -no-feature-  
accessibility build  
* QTBUG-113289 Access to GL_POINT_SPRITE fails in GL core profile  
* QTBUG-112990 QProcess::startDetached() freezes threads on QNX?  
* QTBUG-113315 Segmentation fault in a VirtualBox Linux guest with  
-march=native  
* QTBUG-113143 QGenericUnixServices::openDocument /  
xdgDesktopPortalOpenFile fails in flatpak  
* QTBUG-113295 Failure to build Qt 6.5.0 from source on macOS  
* QTBUG-113311 [REG] Mac checkable menu stays on parent click (works in  
6.4.3 + 6.4.0b2)  
* QTBUG-113376 [REG 6.5.0 -> 6.5.1] QTabBar: Jumping non-expandable tabs  
* QTBUG-113140 Resizing a QTabBar resets the scroll position  
* QTBUG-113209 Qt::ItemNeverHasChildren prevents itemChanged() from  
being fired  
* QTBUG-112663 QFile on Android unable to open file content:// with  
space in the name  
* QTBUG-107459 Qt produces warnings when QT_PLUGIN_PATH contains  
different major versions  
* QTBUG-101755 (glob|magic)-deleteall does not remove existing  
globs/magic with xml providers  
* QTBUG-113337 [REG 6.4.3 -> 6.5.0] Integer overflow in qfixed_p.h when  
rendering SVG image on the minimal plugin  
* QTBUG-109324 Clarify the doc page about module changes in Qt6  
* QTBUG-93768 Recursive loop with QCocoaAccessible::unignoredChildren  
causes crash  
* QTBUG-112697 QMessageBox return immediately on macOS if called from  
MenuBar and after a modal dialog [REG]  
* QTBUG-111524 [REG 6.4 -> 6.5-beta3] Exec'd QMessageBoxes from QMenus  
return immediately on macOS  
* QTBUG-112911 QMenu has sizing issues on multi screen systems  
(again/regression)  
* QTBUG-112738 QDir::entryInfoList() broken on Android when nameFilters  
used  
* QTBUG-113500 Assert when using a QWidget inside NSSavePanel  
* QTBUG-105457 Signals might be processed in wrong order in QtDBus  
* QTBUG-112737 clang++: unknown argument: '-permissive-' and unsupported  
'-Zc:__cplusplus'  
* QTBUG-111582 QByteArray(int size, Qt::Initialization) is not  
documented  
* QTBUG-111243 [REG: 5->6] pthread functions seem to refer to the parent  
process in QProcess child setup  
* QTBUG-111964 QProcess::start does not return if setChildModifier hangs  
* QTBUG-104493 Application performance drops if many threads are running  
while QProcess creates sub-processes on Unix  
* QTBUG-36367 Misleading error output of moc on unknown symbols  
* QTBUG-113556 QWhatThis::showText() brings Mac Permission Dialog  
* QTBUG-45381 QTabWidget::setTabText() will cause the tab to shift the  
current position  
* QTBUG-113335 qhash.h:561:17: alloc-size-larger-than warning  
* QTBUG-113619 Incorrect moc file generated when using QOffscreenSurface  
* QTBUG-112885 Qt6AndroidMacros generates invalid android's deployment-  
settings.json  
* QTBUG-112901 wasm: QCameraPermission does not work on Firefox  
* QTBUG-112822 QProperty crashes  
* QTBUG-104785 [REGR:5->6] Performance regression in QLocale on macOS  
* QTBUG-113443 QLocale::toDouble() fails to convert a string with Latin  
"e" or "E" as exponent separator in Ukrainian locale  
* QTBUG-113643 CMake: headersclean depends on way too much  
* QTBUG-33142 Inherited signals do not work via D-Bus  
* QTBUG-113244 Python not detected on reconfigure with the developer-  
build option  
* QTBUG-113771 Qt 6.5 Build from source issue - Can't find class headers  
like QFile  
* QTBUG-113787 error: 'IFF_UP' conflicts with a previous declaration  
* QTCREATORBUG-29216 indentifier for object is missing  
* QTCREATORBUG-29214 text repetition  
* QTBUG-113630 Windows build with LLVM fails with platform header  
missing after successfull configuration  
* QTBUG-113977 Crash on start with QT_SCREEN_SCALE_FACTORS set  
* QTBUG-112921 Cannot create packages for Google PlayStore  
* QTBUG-108132 cannot set --release option to androiddeployqt when  
building app with cmake ?  
* QTBUG-113557 Raster native widget fail to draw when there is a quick  
widget sibling  
* QTBUG-113652 [REG 6.3.2 -> 6.4] Native QOpenGLWidget in QMainWindow  
breaks menu bar  
* QTBUG-108277 QWidget::setParent calls q_evaluateRhiRecursive which is  
slow  
* QTBUG-113694 Qt 6.5 build fails on macOS  
* QTBUG-110889 Missing default CFBundleIdentifier in CMake generated  
projects  
* QTBUG-114064 QDialog always show minimize on macos  
* QTBUG-113990 QTextDocument should render <hr> in WindowText colour  
* QTBUG-106683 qt_add_qml_module: _automoc_json_extraction target and  
resources are rebuilding every time with Visual Studio Generator  
* QTBUG-114204 QTabBar tabs above current index not visible if current  
index is set before the tabbar is drawn  
* QTBUG-108794 Building applications against static QNX build fails  
* QTBUG-114236 Any Drag and Drop crashes on 6.5  
* QTBUG-100094 iOS A11Y unexpected reset  
* QTBUG-113811 [REG: 6.2->6.5] windows: 16x multisampling produces a  
border (NVIDIA)  
* QTBUG-113591 Problem updating QDockWidget's title with translations  
* QTBUG-112829 QGuiApplication::screens() returns only the secondary  
screen  
* QTBUG-114229 Broken bitmap fonts when a non-rotating transform is set  
* QTBUG-112968 QTextEdit hangs when large text is copied  
* QTBUG-114085 qt-configure-module with parameters fail at run at root  
directory  
* QTBUG-112742 REG: QScreen physicalSize() return wrong results on  
Android / Qt 6.5 - returns pixels not millimeters  
* QTBUG-110942 I see 2 icons showing up in our QTreeView since upgrading  
to Qt6  
* QTBUG-112217 setTearOffEnabled() leading to crash  
* QTBUG-111901 Release build still puts debug info into .so files  
* QTBUG-113416 [Reg 6.4->6.5] Static build fails at PDF module  
* QTBUG-54955 Mac: Wrong QDate string conversion with  
Qt::SystemLocaleLongDate on dates prior to 1893-04-02  
* QTBUG-93009 QPalette::PlaceholderText color is not followed after  
setting color in a style sheet  
* QTBUG-112513 QFuture continuation segfaults with move only datatypes  
* QTBUG-109405 [Regression] 6.3.1 -> 6.4.1 Android - QSettings lost  
* QTBUG-109369 QSettings - default file location changed between Qt5 and  
Qt6 on Android  
* QTBUG-114313 [Reg: 5.15 -> 6.2/6.5?] QQuaternion::getAxisAndAngle()  
can produce NaN, even when normalized  
* QTBUG-114530 Qt build in jenkins triggers message boxes with help  
messages from Qt tools  
* QTBUG-111330 error: Not a signal or slot declaration in code generated  
by qt_add_dbus_interface  
* QTBUG-114625 TRY_RUN failure on cross-compilation  
* QTBUG-107627 AndroidAssetsFileEngineHandler is broken  
* QTBUG-114576 QFileInfo("assets:/path/to/file").fileName() returns  
wrong name  
* QTBUG-114219 QFileInfo::fileName() does not strip assets prefix on  
Android  
* QTBUG-112261 [REGRESSION] QDir::entryList returns invalid names (6.4.2  
-> 6.4.3)  
* QTBUG-114334 [REG 6.5.0 -> 6.5.1] Segfault in  
QXcbConnection::handleXcbEvent with touch(pad) gestures after  
disconnecting input device  
* QTBUG-114606 Cancelling a QPromise with a failure handler crashes  
* QTBUG-114600 [REG 6.4.3 -> 6.5.0] Strange UI styles  
* QTBUG-109781 QXmlStreamReader asserts trying to construct XmlStringRef  
of negative len on external input  
* QTBUG-114829 [REG 6.5.1 -> 6.5.2] Crash/failed assert by passing  
certain xml file to QXmlStreamReader  
* QTBUG-31283 QByteArray::clear() should not free the reserved memory.  
* QTBUG-112892 tst_macdeployqt::basicapp is failing randomly in lts-6.2  
* QTBUG-112746 QAnyStringView missing implicit conversion from char[]  
with unknown size  
* QTBUG-75521 Be precise in API dox of QGuiApplication::desktopFileName  
whether .desktop suffix is included  
* QTBUG-103093 Palette Change And Application PaletteChange Never Emited  
* QTBUG-111514 QtCore fails to link with lld 16.0  
* QTBUG-101648 On Windows Touch device(Surface Pro) need to know if  
external keyboard is connected or not  
* QTBUG-101875 Properly register the input devices on Android  
* QTBUG-112432 wayland plugin should distinguish touchpads from mice,  
etc.  
* QTBUG-113706 WASM: QInputDevice::devices() erroneously reports that a  
touchscreen exists  
* QTBUG-113711 Windows: QInputDevice::devices() returns empty list  
* QTBUG-113463 Build issues with symlinks  
* QTBUG-112747 Unable to run configure.bat  
* QTBUG-112200 Possible memory leak with Fusion style  
* QTBUG-113371 locale and/or environment not being properly set for  
ptests  
* QTBUG-114167 A QString::prepend("data") loop never produces  
freeSpaceAtBegin().  
* QTBUG-112814 The window restore geometry is not correct  
  
### qtsvg  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtdeclarative  
* QTBUG-112945 QML RangeSlider does not work well on touch screen  
* QTBUG-104987 REG: flicking TableView is broken  
* QTBUG-113172 Qt 6.5 Material TextField placeholder breaks with  
alignment  
* QTBUG-112897 Can't build app when there is a function in QML Dialog  
* QTBUG-112837 QML fails to bind to QObject property (defined with  
Q_OBJECT_BINDABLE_PROPERTY and BINDABLE) that are a type Q_GADGET  
* QTBUG-112529 MultiPointTouchArea signals deliver QList<QObject*>  
* QTBUG-99363 [Reg 5.15 -> 6.2] Properties are not set on createObject  
* QTBUG-113389 [Reg 6.4 -> 6.5] Qml Compiler doesn't use the correct  
type when calling an overloaded c++ function  
* QTBUG-113353 Crash with qt.qml.binding.removal.info category enabled  
while breaking a binding  
* QTBUG-113321 Material TextArea and TextField placeholder text  
incorrectly clipped  
* QTBUG-112949 splice does not work on list properties  
* QTBUG-106266 [Reg 5.15 -> 6.x] Component.createObject() mangles passed  
properties  
* QTBUG-113221 -no-feature-qml-devtools does not build  
* QTBUG-112946 amendException in QQmlJSAotContext can amend wrong stack  
frame  
* QTBUG-112291 QML_SEQUENTIAL_CONTAINERS affects isArray and breaks  
ComboBox  
* QTBUG-112740 SplitView: Incorrect Rendering Between Layouts and  
Transparent Items  
* QTBUG-113484 [REG] Unable to determine callable overload  
* QTBUG-106164 ListView doesn't render Text in delegates on dataChanged  
signal  
* QTBUG-106205 QML Text are not rendered if outside the screen at its  
creation  
* QTBUG-108803 Named import not recognized  
* QTBUG-113446 KTX, ASTC, PKM image not displayed using NinePatchImage  
* QTBUG-113565 Enhance the warning about the vendor and platform  
specificness of compressed texture format support in the Image docs  
* QTBUG-100678 QML Runtime Tool help all option is not working  
* QTBUG-88195 Change SplitView orientation  
* QTBUG-35244 QWindow visibility/visible property conflict  
* QTBUG-113673 ColorDialog don't resize correctly on small screens  
* QTBUG-112618 Wearable Example Home and Back Button Images Don't Load  
* QTBUG-111679 Item or Rectangle not able to gain focus after Drawer is  
closed  
* QTBUG-111892 wasm: asynchronous image loading never ends  
* QTBUG-113744 Misguiding error message  
* QTBUG-113439 Specifying RESOURCES to qt6_target_qml_sources does not  
make file level dependency  
* QTBUG-108689 TapHandler does not react to clicks when combined with  
PinchHandler  
* QTBUG-113005 Tap handlers are broken on Android.  
* QTBUG-113469 QML ComboBox breaks dark mode window styling  
* QTBUG-112840 Please write the realistic usecase of Qt Quick Test to  
the documentation  
* QTBUG-113852 [Reg Qt6.4->6.5] The contentWidth of QML TableView is 0  
* QTBUG-113853 [REG 5.15.x -> 6.3/6.4/6.5] Mouse Events not accepted on  
a MouseArea placed inside modal Popup::background  
* QTBUG-76830 QML ListView with variable sized delegates causes attached  
scroll bar to change sizes and skip around in an unwanted manner  
* QTBUG-108171 ScrollBar with sections is jumpy  
* QTBUG-112858 [Windows] Quick TextEdit with RTL text placed into a  
ColumnLayout has wrong alignment  
* QTBUG-113584 Typo in the code snippet  
* QTBUG-112613 No way to navigate to a parent topic for Qt Quick  
Compiler doc pages  
* QTBUG-113454 Links for 'Qt Quick Effects', 'Qt Quick Particles'  
landing pages do not work  
* QTBUG-113743 QKeySequence cannot be sent to QML Shortcut from C++ side  
* QTBUG-114340 FAIL!  : tst_usertypes::watcherInQml()  
* QTBUG-113752 Warning when assigning to Map.visibleRegion  
* QTBUG-114086 [Reg 6.4 -> 6.5] Historical NativeMethodBehavior is  
broken when a Q_INVOKABLE function is stored in a QML property  
* QTBUG-114358 ComponentBehavior: Bound causes 'QQmlContext: Cannot set  
property on internal context'  
* QTBUG-105862 [REG] Qt6.3.1 a MultiPointTouchArea inside another  
MultiPointTouchArea is reporting the wrong touch location  
* QTBUG-113745 Qt Quick 2D Renderer: Partial scene update might erase  
items at fractional coordinates  
* QTBUG-113009 TextEdit: rendering issue when highlighting text  
* QTBUG-80788 [5.14 REG] New properties in ComboBox clash with custom  
properties (revision ignored)  
* QTBUG-109995 Can not interact with tumblers inside interactive  
flickable on touch  
* QTBUG-113653 [REG 5.15->6.2.3] MultiPointTouchArea doesn't receive  
gestureStarted signal when used inside PathView or Flickable  
* QTBUG-114494 QML rect property as a parameter causing a crash  
* QTBUG-112434 [Regr: 6.3.1->6.3.2] MouseArea stays pressed after double  
click on touch screen  
* QTBUG-109393 [Regr: 6.3.1->6.3.2] iPad: DoubleClicking in MouseArea +  
Popup breaks  
* QTBUG-113227 ABI issue with QVariant and metatypes from Qt < 6.5  
* QTBUG-98790 ChangeListeners get called even after being semi-deleted  
* QTBUG-109221 Inconsistencies regarding list and value type property  
manipulations  
* QTBUG-113015 [QDoc] Duplicate QML property name causes confusion:  
qml[attached]property QWindow::Visibility Window::visibility  
* QTBUG-111946 How should QML modules be installed with cmake (with Qt  
6.4 or later)?  
* QTBUG-113230 Unexpected width behaviour when using  
Layout.horizontalStretchFactor  
* QTBUG-78261 tst_focus::policy is failing  
* QTBUG-109380 Function overloading  with date related methods fails  
* QTBUG-114073 qdoc resolves "QML Import Path" reference incorrectly  
* QTBUG-106683 qt_add_qml_module: _automoc_json_extraction target and  
resources are rebuilding every time with Visual Studio Generator  
  
### qtactiveqt  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtmultimedia  
* QTBUG-112973 MediaPlayer example cannot open any file  
* QTBUG-113386 MediaPlayer: error, errorString property changes are not  
notified  
* QTBUG-105372 QML Camera - setting zoomFactor does not work  
* QTBUG-113029 Android: declarative-camera example: Captured image is  
not rotated for landscape orientation  
* QTBUG-112454 Android-Multimedia know issue with pixel format need to  
be documented  
* QTBUG-113263 wasm: error when switching cameras  
* QTBUG-114061 WebAssembly audio output not working  
* QTBUG-112707 Qt6 Multimedia: cannot open file if file path contains  
non-ascii characters  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-113782 error: no member named 'unary_function' in namespace  
'std'  
* QTBUG-112512 QSoundEffect cuts out on very short sounds ( ~ 0.2 - 0.3  
seconds )  
* QTBUG-109659 Audio capturing and playing does not work on Android  
* QTBUG-109537 Spectrum example build fails  
* QTBUG-112219 `QMediaDevices::defaultAudioInput()` wrong device  
* QTBUG-114202 QtMultimedia should not crash (qFatal) when using dummy  
implementation  
* QTBUG-110071 [REG 6.3.1->6.4.1]Problems with QMediaDevices  
'videoInputs' and 'videoInputsChanged'  
* QTBUG-114442 [REG 6.5.1->6.5.2] namespace build fails on Windows,  
Multimedia  
  
### qttools  
* PYSIDE-2311 pyside6-lupdate blocks when the input file has no symbols  
in it.  
* QTBUG-113152 [REG 5.15.8 -> 5.15.9] qt5_create_translation breaks  
projects with multiple same-named ts files  
* QTBUG-113864 \typealias doesn't expand with "This is a type alias for  
[...]"  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtdoc  
* QTBUG-111586 Update OpenSSL for Android deployment docs for OpenSSL 3  
* QTBUG-113588 Check attribution details for opengl32sw.dll  
* QTBUG-99900 Leading zeroes for Android app "versionCode" are being  
removed  
* QTBUG-114670 Dependency update on qt/qt5 failed in 6.5.2  
* QTBUG-114592 todolist demo fails to configure  
* QTBUG-114759 add_library cannot create target "CustomControls" because  
another target with the same name already exists  
* QTBUG-114848 Document Viewer looks broken in 6.5.2 examples  
* QTCREATORBUG-29330 Widget designer standard icons invisible on macOS  
* QTBUG-113257 Configure qt failed for arm64 architecture  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-110022 Docs missed for ANDROID_MIN_SDK_VERSION and  
ANDROID_TARGET_SDK_VERSION variables  
  
### qtlocation  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtpositioning  
* QTBUG-109359 Qt on iOS always asks for "always" location permission.  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-113752 Warning when assigning to Map.visibleRegion  
  
### qtsensors  
* QTBUG-113435 dummy plugin gets built by default  
* QTBUG-113651 [REG 6.5.0->6.5.1] sensors/sensorsshowcase not compiling  
on Android  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtconnectivity  
* QTBUG-113318 QBluetoothLocalDevice::pairingStatus always returns  
status unpaired  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtwayland  
* QTBUG-113023 missing cmake module import documentation  
* QTBUG-110924 doc: Pure-QML example claims to only support one text-  
input protocol  
* QTBUG-113233 Need a way atomically adjust QWindow minimum and maximum  
sizes  
* QTBUG-113560 CMake error on static qtwayland build  
* QTBUG-97037 DragHandler / startSystemMove window move issue with QT6  
Webengine on Wayland  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-113145 Gesture handlers crash due to misbehaving compositors  
  
### qt3d  
* QTBUG-113589 planets-qml example doesn't build anymore  
* QTBUG-113314 QSkyboxEntity does not render when using the (default)  
RHI backend  
* QTBUG-112739 Qt3DExtras::QSkyboxEntity is broken  
* QTBUG-97751 Crash when loading .obj files with empty lines - out of  
bounds array access in objgeometryloader.cpp  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtimageformats  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtserialbus  
* QTBUG-114043 QCanDbcFileParser incorrectly parses 29-bit (extended)  
CAN IDs  
* QTBUG-113538 QCanBus not decoding CAN Frames correctly on Mac.  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtserialport  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtwebsockets  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtwebchannel  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtwebengine  
* QTBUG-113035 Under the current conditions specified in the  
documentation, it is not possible to build the module through cross-  
compilation  
* QTBUG-112645 QWebEnginePage::WebWindowType not covered by tests  
* QTBUG-113400 If QWebEngineProcess is terminated and a JavaScript is  
being run that leads to crash  
* QTBUG-112466 libQt6Pdf.so is always built with an embedded copy of  
libpng  
* QTBUG-113270 Improve docs with details about the use of GPL components  
from Chromium  
* QTBUG-113524 WebEngine cannot use https after using -sign-for-  
notarization  
* QTBUG-113579 Clipboard write action doesn't work on 6.5.0  
* QTBUG-113802 CrossBuilding QtPdf fails because of wrong path to  
qt.toolchain.cmake  
* QTBUG-113859 [REG 6.4->6.5] Accessibility crash when clicking on a  
link in a list on macOS  
* QTBUG-113704 Sending certain key events to QQuickView showing a  
focused QtWebEngine causes crash  
* QTBUG-113992 QTWebEngine crash when not working proxy is set  
* QTBUG-113806 Chromium attributions missing from 'Licences used in Qt'  
docs  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-113416 [Reg 6.4->6.5] Static build fails at PDF module  
* QTBUG-115067 [REG 6.5.1 -> 6.5.2] shadow build failure, webengine  
  
### qtwebview  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-114495  FAIL!  : tst_QWebView::load()  
  
### qtcharts  
* QTBUG-114408 add_executable cannot create target "gallery" because  
another target with the same name already exists.  
* QTBUG-114221 Charts API Documentation Snippets broken, Examples  
broken.  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-94181 error: â€˜defaultInputDeviceâ€™ is not a member of  
â€˜QAudioDeviceInfoâ€™  
  
### qtdatavis3d  
* QTBUG-114178 Transparency in gradient results in weird stripes  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtvirtualkeyboard  
* QTBUG-113168 [VKB] fullScreenMode does not work when enabled with a  
Binding  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtscxml  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtspeech  
* QTBUG-114099 Qt TextToSpeech landing page is missing 'Licenses and  
Attributions' section  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtnetworkauth  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtremoteobjects  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtlottie  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtquicktimeline  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtquick3d  
* QTBUG-113044 No callback from QQuick3DLightmapBaker::bake() if there  
are no models set up for baking  
* QTBUG-92944 input problems in DynamicTexture example  
* QTBUG-113987 Typo in the document  
* QTBUG-113986 Typo in the document  
* QTBUG-113985 Data type of aoEnabled seems to be wrong.  
* QTBUG-114557  FAIL!  : tst_RotationDataClass::test_construct()  
Compared values are not the same  
* QTBUG-114313 [Reg: 5.15 -> 6.2/6.5?] QQuaternion::getAxisAndAngle()  
can produce NaN, even when normalized  
* QTBUG-105918 REG: Jittery skeletal animations  
* QDS-9791 Two components named 'Attractor' in QtQuick3D Particles3D  
module components  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-101688 QtQuick3D: Fix compiler warnings for QNX  
* QTBUG-113982 fieldOfViewOrientation property is written twice in the  
PerspectiveCamera's documentation  
  
### qtshadertools  
* QTBUG-114113 qtshadertools contains two copies of spirv.hpp and  
they're different  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qt5compat  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtcoap  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtmqtt  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtopcua  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtlanguageserver  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qthttpserver  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtquick3dphysics  
* QTBUG-113597 ERROR building: Timeout after 15m0s: No output received  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-114183 Collision shape calculates orientation incorrectly when  
parent has scale  
  
### qtgrpc  
* QTBUG-112762 QMetaProperty::write detaches value argument  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtquickeffectmaker  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-113531 EffectMaker not find resources on macOS  
* QTBUG-108171 ScrollBar with sections is jumpy  
  
Known Issues  
------------  
  
* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-6.5/supported-platforms.html  
* RTA reported issues from Qt 6.5  
https://bugreports.qt.io/issues/?filter=24558  
* See Qt 6.5 known issues from:  
https://wiki.qt.io/Qt_6.5_Known_Issues  
* Qt 6.5.2 Open issues in Jira:  
https://bugreports.qt.io/issues/?filter=25146  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Amir Masoud Abdol  
Chris Adams  
Laszlo Agocs  
Anu Aliyas  
Mahmoud Badri  
Mate Barany  
Vladimir Belyavsky  
Nicholas Bennett  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
Mikolaj Boc  
Tatiana Borisova  
Joerg Bornemann  
Assam Boudjelthia  
Aurélien Brooke  
Michael Brüning  
Igor Bugaev  
Olivier De Cannière  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Pranta Dastider  
Szabolcs David  
Pavel Dubsky  
Artem Dyomin  
Alexey Edelev  
David Edmundson  
Oliver Eftevaag  
Christian Ehrlicher  
Hatem ElKharashy  
Andreas Eliasson  
Ahmed Essam  
Fabio Falsini  
David Faure  
Ilya Fedin  
Samuel Gaist  
Jan Grulich  
Kaj Grönholm  
Richard Moe Gustavsen  
Lucie Gérard  
Tang Haixiang  
Kamil Hajdukiewicz  
Jøger Hansegård  
Andre Hartmann  
Thomas Hartmann  
Jani Heikkinen  
Miikka Heikkinen  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Allan Sandfeld Jensen  
Tim Jenssen  
Jonas Karlsson  
Timothée Keller  
Ali Kianian  
Friedemann Kleint  
Michal Klocek  
Lars Knoll  
Sze Howe Koh  
Jarkko Koivikko  
Tomi Korpipaa  
Fabian Kosmale  
Santhosh Kumar  
Kai Köhne  
Jaehak Lee  
Inho Lee  
Kimmo Leppälä  
Thiago Macieira  
Christophe Marin  
Thorbjørn Lund Martsum  
Ievgenii Meshcheriakov  
Phan Quang Minh  
Samuel Mira  
Safiyyah Moosa  
Bartlomiej Moskal  
Marc Mutz  
Antti Määttä  
Martin Negyokru  
Andy Nichols  
Mårten Nordheim  
Dennis Oberst  
Samuli Piippo  
Joni Poikelin  
Lorn Potter  
Matthias Rauter  
Arno Rehn  
Topi Reinio  
Alexey Rochev  
Shawn Rutledge  
Ahmad Samir  
L. E. Segovia  
Luca Di Sera  
Sami Shalayel  
Venugopal Shivashankar  
Ivan Solovev  
Axel Spoerl  
Christian Strømme  
Tarja Sundqvist  
Jan Arve Sæther  
Morten Sørvig  
Paul Olav Tvete  
Peter Varga  
BogDan Vatra  
Doris Verria  
Tor Arne Vestbø  
Ville Voutilainen  
Jaishree Vyas  
Edward Welbourne  
Paul Wicking  
Piotr Wierciński  
Oliver Wolff  
Vlad Zahorodnii  
Yuhang Zhao  
Eike Ziller  
