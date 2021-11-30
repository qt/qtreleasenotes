Release note  
============  

Qt 6.2.2 release is a patch release made on the top of Qt 6.2.1.  
As a patch release, Qt 6.2.2 does not add any new functionality but provides  
bug fixes and other improvements and maintains both forward and backward  
compatibility (source and binary) with Qt 6.2.1.  

For detailed information about Qt 6.2, refer to the online documentation  
included in this distribution. The documentation is also available online:  
  
https://doc.qt.io/qt-6/index.html  
  
The Qt version 6.2 series is binary compatible with the 6.1.x series.  
Applications compiled for 6.1 will continue to run with 6.2.  
  
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
* 448e45b1f4 QVarLengthArray: Reduce memory allocations in insert()  
Reduced number of memory allocations in insert() by allocating more  
memory at once.  
  
* b4b3343b80 PCRE2: upgrade to 10.39  
PCRE2 has been updated to version 10.39.  
  
* 069dfef5e8 QByteArrayList: fix narrowing in join() implementations  
[1/2]  
Fixed a bug when calling join() on lists with more than INTMAX  
elements.  
  
* de2395d757 qmake: Support Visual Studio 2022  
Added support for Visual Studio 2022.  
  
* 94016862a7 QImageReader: check allocation limit for minimum 32 bpp  
When checking allocation limit during image reading, the memory  
requirements are now calculated for a minimum of 32 bits per pixel,  
since Qt will typically convert an image to that depth when it is used  
in GUI. This means that the effective allocation limit is significantly  
smaller when reading 1 bpp and 8 bpp images.  
  
### qtdeclarative  
* 092f2c4f61 Fix distorted text with subpixel matrix translation  
Fixed an issue where text using NativeRendering would look slightly  
skewed if it was inside a parent that had been positioned at a subpixel  
offset.  
  
* f44aabad32 Use correct plugin name for Android QML plugins  
Starting with Qt 6.4, QML import mechanism won't add URI-based prefixes  
when looking for QML plugins for Android applications. For forward  
compatibility, the 'plugin' record of the qmldir files should contain  
the full file name of the plugin without abi-specific suffixes and the  
file extension. When using the CMake API to create the qmldir, no  
further action is necessary.  
  
### qtwayland  
* 60f908ba Fix the logic for decoding modifiers map in Wayland text  
input protocol  
Fix modifiers map decoding logic when receiving the map from the  
compositor.  
  
### qtvirtualkeyboard  
* d897a740 cerence-hwr: Fix compilation with the latest Cerence SDK (v9)  
Added support for the latest Cerence SDK (9.x).  
  
* 2b84f3b1 Use a containment mask to keep input panel working during  
modal session  
Since Qt 5.15, the virtual keyboard's input panel has automatically  
been reparented to prevent the keyboard UI from being blocked by modal  
dialogs. This is no longer done; the input panel instead uses a  
containment mask on the dimmer item that blocks input during modal  
sessions, allowing clicks through to the keyboard UI.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-97095 Mouse clicks are not delivered to the QWidget beneath  
container QWidget in QOpenGLWIndow on Windows  
* QTBUG-94769 QComboBoxListView display misalignment after sliding  
* QTBUG-91391 androiddeployqt uses deprecated ndk.dir property  
* QTBUG-97491 Android: in TextField: cannot edit inside of words, only  
at the end  
* QTBUG-97475 Crash in QItemSelectionModel  
* QTBUG-57347 [macOS] button doesn't click when having preedit string in  
line edit and text edit  
* QTBUG-91222 Markdown parser improperly handles certain HTML payloads  
* QTBUG-94245 Markdown unexpected render result  
* QTBUG-97478 Configuring CMake based application with QtQuick fails  
* QTBUG-95609 cmake names for qml plugins  
* QTBUG-97099 [cmake] dependent qml plugins not auto-loaded with  
statically linked qt  
* QTBUG-97116 OpenSSL TLS plugin is not loaded for OpenSSLv3  
* QTBUG-255 QTableWidget setSpan + selectedRanges  
* QTBUG-96114 [Reg : 5.12.4 -> ] ActiveX widget not rendering on  
secondary screen when System-DPI Aware is combined with high DPI scaling  
* QTBUG-97493 Change of QDateTimeEdit::setDateTime not documented in  
"Changes to Qt Modules in Qt 6"  
* QTBUG-96558 RTA CMake test fails on macOS10.15 and macOS11.0  
* QTBUG-96870 qt_internal_generate_tool_command_wrapper might fail to  
generate wrapper script due to unrelated configuration failure  
* QTBUG-97486 Crash in TimeZone ICU backend  
* QTBUG-97443 Crash - DpiAdjustmentPolicy resolved from wrong  
environment  
* QTBUG-96560 Android: Keyboard does not show up again if it has been  
closed with back button in some devices  
* QTBUG-60257 [XCB]: QXcbClipboard: SelectionRequest too old messages  
can appear  
* QTBUG-97458 String "6.2.0" found from 6.2.1 source package  
* QTBUG-94352 QTabBar's SelectionBehavior QTabBar::SelectPreviousTab  
does not work as expected  
* QTBUG-96639 QMainWindow crash during "closeEvent"  
* QTBUG-89101 QPainter::fillRect broken with QBrush containing DPR > 1  
pixmap  
* QTBUG-88529 wrong symbol is getting deleted  when tap on clear button  
* QTBUG-94768 Qt::Tool window has no title bar  
* QTBUG-96240 Views are not blurred  
* QTBUG-86533 Yocto and QNX builds are missing -rpath-link linker flag  
which causes non-prefix builds to fail  
* QTBUG-85997 QDir::mkpath() does not return true for existing drive  
* QTBUG-97629 Building qtbase for Android with examples fails to  
configure  
* QTBUG-97110 QDir::mkpath() fails on MACOS given the root path  
* QTBUG-97532 Mention how to properly deploy and use TLS plugins  
* QTBUG-96256 Cannot declare MetaType for a QHash/QMultiHash with key  
type without custom operator==  
* QTBUG-97054 QSqlDatabase.open() warning  
* QTBUG-97009 Broken rendering on Qt 6.2 Android arm64-v8a  
* QTBUG-97673 Update dependencies in qt/qtshadertools fails  
* QTBUG-93810 warnings due to enums in QSize  
* QTBUG-97713 [Reg 6.1->6.2] Unexpected value for QKeyEvent::key() if  
Ctrl+letter is pressed  
* QTBUG-97241 Qt no longer compiles when configured with -trace  
* QTBUG-97246 Qt fails to compile with both tracing and QT_NAMESPACE  
enabled  
* QTBUG-25743 QAction triggered in QMenu within QMenuBar even though the  
QMenu's menuAction is hidden/disabled.  
* QTBUG-6905 font-weight: bold can truncate tab label  
* QTBUG-8209 QTabBar: Tab size incorrect when using bold font in a style  
sheet  
* QTBUG-94806 Having Qmltypes in CONFIG leads to faulty vcxproj file  
* QTBUG-97489 [REG 6.2 -> 6.3.0] QDateTime::fromString slow at handling  
large input  
* QTBUG-94918 QWidget::show triggers windows activation  
* QTBUG-97777 Assertion violation in QDateTime parsing.  
* QTBUG-97269 Antialiasing is disabled when the painter's antialiasing  
attribute is set behind the clipping funcion.  
* QTBUG-97727 Tree Model Completer Example: tree model is broken due to  
bugs in MainWindow::modelFromFile  
* QTBUG-96458 Make it possible to build newer Qt modules against older  
Qt  
* QTBUG-94481 [REG 5.15.2 -> 6.1.1] Ellipsis in the worst possible place  
* QTBUG-83733 Don't use deprecated/removed functions and structs with  
OpenSSL v3  
* QTBUG-93671 Undefined reference to WinMain with MinGW  
* QTBUG-96178 [wasm] Cursor shape does not work  
* QTBUG-97811 QScrollArea performance regression  
* QTBUG-97599 Internal Qt builds prefer target Tools packages over host  
packages  
* QTBUG-95099 [FTBFS] Qt6CoreToolsTargets.cmake not found with  
-DQT_FORCE_FIND_TOOLS=ON  
* QTBUG-96466 [REG 5.15.2-6.2.0] Runtime crash on changing screen's  
scale factor  
* QTBUG-97002 Building for android fail  
* QTBUG-97257 QVideoWidget not showing after minimizing  
* QTBUG-97896 Qt CMake packages should not create targets if  
dependencies are not met  
* QTBUG-97919 include could not find requested file:  C:/Users/qt/work/q  
t/qt5/qtbase/lib/cmake/Qt6EntryPointPrivate/Qt6EntryPointMinGW32Target.c  
make  
* QTBUG-97945 assert in qnsview_mouse.mm  
* QTBUG-97457 Highlighted example quick3d/morphing not compiling on  
Wasm, "wasm-ld: error: initial memory too small, 17835968 bytes needed"  
* QTBUG-97729 Please suppress the annoying logo message from rc.exe  
* QTBUG-97853 Tablewidget_cellClicked not working after opening Dialog  
with cellDoubleClicked  
* QTBUG-97984 HttpStatusCodeAttribute gives 0 in case of success  
* QTBUG-83503 wasm: dialogs wrong size when opened  
* QTBUG-98026 Nested QGraphicsViews do not clip some items when printing  
* QTBUG-98087 top-level in-source build detected as prefix build  
pointing to build dir and removes moc upon install  
* QTBUG-98088 [Regression, macOS] quit() before exec() quits instantly.  
* QTBUG-97747 [REG: 5->6] QDomDocument::setContent now requires  
QIODevice to be open  
* QTBUG-93412 Problem with drawing progressbar as QTreeView delegate  
* QTBUG-98085 qthreadstorage.h fails to compile with namespaces enabled  
* QTBUG-97382 qt.conf not reladed properly after  
QCoreApplication::instance()  
* QTBUG-97383 [REG 5.15 -> 6.2] QtWebEngineProcess + change resources  
location with qt.conf  
* QTBUG-97947 [REG 5.15 -> 6.2] QtWebEngine resources + translations  
location no longer affected by qt.conf  
* QTBUG-97774 Win32: Window contents flicker a lot when resizing  
* QTBUG-59401 QFileDialog::setDefaultSuffix doesn't work when file path  
contains a dot  
* QTBUG-98265 QMultiHash::operator== is broken  
* QTBUG-96069 Qt 6.2.0 Beta3 runtime link error when run  
multimediawidgets sample on android arm  
* QTBUG-98247 qobject_cast pointer conversion crashed  
* QTBUG-98403 tst_QPainter fails with macOS 12 x86 in developer build  
tests  
* QTBUG-98388 Vertical QPainter::drawLine() result on QWidget is skewed  
* QTBUG-98093 QSlider is broken in MacOS Monterey  
* QTBUG-80576 CMake build doesn't find MoltenVK  
* QTBUG-58013 Cursor position changes not properly passed to input  
method  
* QTBUG-93414 Qt Quick application stuck in a cursor update loop  
* QTBUG-95669 Clicking enter on some text fields it might freeze UI  
* QTBUG-96671 Android: Keyboard sometimes stuck and replacing previous  
letter  
* QTBUG-96675 Android: Cursor is shown in wrong place  
* QTBUG-96769 Android: keyboard input can get lost  
* QTBUG-92445 Markdown smashes nested formatting inside lists  
* QTBUG-74606 floating QDockWidget with native child widget fails to  
show() after closing it  
* QTBUG-97247 Fix docs for comparison and debug/data stream operators of  
Qt containers  
* QTBUG-26424 fix disabled test cases of tst_qwidget  
* QTBUG-94344 High CPU load in WASM threaded application  
* QTBUG-97601 Compilation speed decrease with Qt 6.2 compared to Qt  
5.15.2  
* QTBUG-96399 Crash with SIGSEGV in QXcbConnection::getSelectionOwner  
* QTBUG-94250 tst_QListView::internalDragDropMove fails with OpenSUSE  
15.3  
* QTBUG-97656 The article explaining bindable properties is not linked  
in other related parts of the docs  
* QTBUG-95300 [Regression] TextField goes behind soft keyboard on  
android  
* QTBUG-96117 Android soft keyboard no longer pans the screen  
* QTBUG-97503 Reg[5.15.2-5.15.6] Android: Keyboard covers the inputfield  
* QTBUG-72110 MouseArea stops responding  
* QTBUG-74872 Qt/QMake includes the deprecated 'CFBundleGetInfoString'  
key into the Info.plist on macOS  
* QTBUG-96898 Sub-project created with qt_add_qml_module doesn't work on  
Android  
* QTBUG-94530 Disconnecting HDMI output causes application to crash  
* QTBUG-46701 Closing a full screen window via Qt APIs leaves the screen  
black on macOS  
* QTBUG-97903 Sporadic crash on QPMCache::flushDetachedPixmaps  
* QTBUG-91445 Crash in QPixmapCache::setCacheLimit in Windows  
* QTCREATORBUG-26473 Crash inside pixmap cache while RMB inside cpp  
editor  
* QTBUG-97950 Application slowly reads every file in /usr/bin before  
starting  
* QTBUG-94714 Qt's CMake seems to ignore dependencies when generating  
APK targets  
* QTBUG-96127 Broken external links in Qt docs  
* QTBUG-96975 Qurl fails with MSVC 2022 target in windows 10 & 11  
* QTBUG-97715 Quick3D examples fail on imx6  
* QTBUG-97582 QFuture::cancel through then()/onCanceled/onFailed  
  
### qtsvg  
* QTBUG-95891 svg file freezes QImage  
  
### qtdeclarative  
* QTBUG-94975 [ASAN] Heap-use-after-free in QOpenGLFramebufferObject  
* QTBUG-97467 [REG 6.2.0->6.2.1] cmake test fails on RHEL  
* QTBUG-96112 Text tearing on text element when set inside parent  
element with noninteger y value  
* QTBUG-83626 When a Popup has an odd number for the width and/or height  
then texts inside it can be rendered badly  
* QTBUG-55638 garbled font after scrolling with mouse wheel  
* QTBUG-90869 tst_qquickdesignersupport: tests segfault when running on  
QEMU and Windows MinGW developer build  
* QTBUG-94253 When an inputmask is set on a TextInput then it will  
overwrite the first character if the cursor starts from position 0 after  
typing the second character  
* QTBUG-96966 Using stackView.pop(StackView.Immediate) after  
stackView.push(item, StackView.Transition) causes Item to be placed  
unexpectedly  
* QTBUG-61496 StackView: pop() with StackView.Immediate leads to blank  
StackView  
* QTBUG-85956 QQuickPopupPrivate::finalizeExitTransition() not giving  
focus to the highest-z Dialog with focus = true  
* QTBUG-65853 QML ScrollBar Quick Controls 2 - policy:  
ScrollBar.AsNeeded not working when scrollbar is customized  
* QTBUG-95629 SelectionRectangle: Long press on top of a handle clears  
the current selection  
* QTBUG-85918 Focus set to wrong dialog in case of enter transition  
* QTBUG-96929 ToolTip: Make it clearer that ESC is a shortcut used by  
the default closePolicy  
* QTBUG-97480 ParentChange crash  
* QTBUG-86854 When a Tooltip is visible then it is possible to interact  
with a window that is underneath a modal dialog although it should be  
blocking the input to it  
* QTBUG-97606 /home/qt/work/qt/qtdeclarative/src/qml/compiler/qv4bytecod  
egenerator.cpp:40:10: fatal error: private/qv4bytecodegenerator_p.h: No  
such file or directory  
* QTBUG-95373 Component is missing required property index from here  
* QTBUG-95262 TypeErrors in tests  
* QTBUG-97462 Qt Quick "Text editor" example uses deprecated code  
* QTBUG-84269 StackView doesn't work with required properties  
* QTBUG-97600 qmllint segfaults on Connections  
* QTBUG-97466 quick/pointerhandlers example fails to configure  
* QTBUG-97465 [REG 6.2.0->6.2.1] quickcontrols2/texteditor not compiling  
on Wasm  
* QTBUG-86202 DelegateChooser stopped working with enums in QVariants  
* QTBUG-97488 [REG 5.15.2->6.2] DelegateChooser not finding choice  
* QTBUG-96898 Sub-project created with qt_add_qml_module doesn't work on  
Android  
* QTBUG-96458 Make it possible to build newer Qt modules against older  
Qt  
* QTBUG-96934 QQuickFontDialogImpl: update listview indexes when calling  
setCurrentFont()  
* QTBUG-73633 QML FileDialog sort names by capitalised name first  
* QTBUG-96796 qmlcache causes loading problem if the qml filename  
matches the name of some qml file from Qt package and has inline  
component  
* QTBUG-98015 qml tool fails to build when targeting iOS  
* QTBUG-98058 Static Qt plugins not always linked into Qt apps in a top-  
level build  
* QTBUG-98109 Update dependencies on '6.2' in qt/qtdeclarative fails  
* QTBUG-97859 QQuickWindow::tabletEvent() broken in Qt 6.2.1  
* QTBUG-98125 qmllint crashes when there is an animation on a grouped  
property  
* QTBUG-98032 QML/Javascript: Using an anonymous function as a default  
parameter in a function signature crashes the application.  
* QTBUG-98150 Designer puppet keeps crashing at startup in batch  
renderer  
* QDS-5481 Animation looping is not properly set when it is in component  
* QTBUG-98468 CMake Error: AUTOMOC for target affectors_shared: The  
"moc" executable "/Users/qt/work/qt/qt5/qtbase/libexec/moc" does not  
exist  
* QTBUG-98248 SEGFAULT Crash in QQmlAnimationTimer::registerAnimation  
* QTBUG-92591 QtDeclarative autotest configure fails on Android builds  
* QTBUG-97075 [REG: 5.14.2->5.15.0] Anchors don't work with InputPanel  
anymore  
* QTBUG-56918 When the keyboard is shown for a text field in a modal  
popup then it will not be usable  
* QTBUG-92881 InputPanels defaults z value should be lower than max  
value for overlays  
* QTBUG-93956 The QSGBatchRenderer::Renderer's m_vertexUploadPool and  
m_indexUploadPool buffers never shrink  
* QTBUG-83908 Material.System does not work on Windows 10 in Dark Mode  
* QTBUG-93955 Material.System does not work on Ubuntu (Gnome)  
* QTBUG-95587 icon.source of Control is not resolved relative to user  
code  
* QTBUG-72110 MouseArea stops responding  
* QTBUG-92809 ListView can go out of sync with the model if item is  
removed and inserted outside of the view before the current item  
* QTBUG-97986 build problem with qmltc test  
* QTBUG-98130 QtQuick and controls examples use qt_add_resources to add  
QML files  
* QTBUG-96806 quick/customitems/painteditem/TextBalloon/qmltextballoon  
not compiling:  
* QTBUG-84196 Crash when calling QQmlEngine::retranslate  
* QTBUG-91033 Multiple extra compilers with same input are broken for VS  
projects  
* QTBUG-94806 Having Qmltypes in CONFIG leads to faulty vcxproj file  
  
### qtmultimedia  
* QTBUG-96747 Black rectangle visible on the initial screen for player  
example  
* QTBUG-97166 Qt6 Multimedia - Subtitle Language Metadata Detection  
Incorrect?  
* QTBUG-97391 Qt6 QML Multimedia camera example code invalid syntax  
* QTBUG-95369 multimedia/video/android/gstreamer fails on configure  
(typo in CMakeLists.txt?)  
* QTBUG-97091 Disable ALSA and pulse audio by default in the build  
system  
* QTBUG-96985 Video and MediaPlayer don't allow to use relative URLs  
* QTBUG-96956 List of available devices not refreshed while plug in/  
plug out wired headset  
* QTBUG-97485 Build from source of qt multimedia fails on MacOS with  
opengl disabled  
* QTBUG-97622 QML ImageCapture preview property does nothing?  
* QTBUG-97379 [Boot2Qt] Declarative-camera example does not work with  
Toradex Apalis i.MX6  
* QTBUG-97584 qmllint error on VideoOutput: "QQuickItem was not found.  
Did you add all import paths?"  
* QTBUG-97647 Crash on QAudioDecoder when running test  
* QTBUG-97646 Crash on QMediaRecorder when running test  
* QTBUG-97408 multimediawidgets/camera example crashes when launched  
from Finder  
* QTBUG-96899 QAudioDecoder fails on windows  
* QTBUG-97610 Android - QML Camera does not work at first after granting  
permission  
* QTBUG-97402 Qt6 Multimedia: Signals not fired on change of Audio Track  
* QTBUG-97730 Wrong QMediaPlayer::position when  
QMediaPlayer::videoOutput==NULL  
* QTBUG-97440 Qt Multimedia does not compile without EGL 1.5 on Linux  
platform  
* QTBUG-97121 RTSP stream crash Video player  
* QTBUG-96447 Subtitles do not work on iOS  
* QTBUG-97895 fullscreen does not work in the player example on macOS  
* QTBUG-97839 Listes handling on the Audiorecoder example  
* QTBUG-97832 [Windows] MediaRecorder is not functional for local file  
output locations  
* QTBUG-97911 QVideoWidget stopped working as QCamera viewfinder after  
Qt upgrade 6.2.0->6.2.1  
* QTBUG-97952 Qt6 QML MediaRecorder outputs FormatError when output  
location is incorrect  
* QTBUG-98023 Return value of mimeTypeForFormat  is incorrect on  
QMediaFormat  
* QTBUG-97415 Qt6 Multimedia: Imprecise Seek Behavior for a Local Video  
* QTBUG-96957 Created output file is in inncorrect type and in different  
location  
* QTBUG-96953 Spectrum app crashes once user play button after sound  
ended  
* QTBUG-97992 Stopping QMediaPlayer and starting it again may crash on  
Windows  
* QTBUG-97587 int QAndroidImageCapture::captureToBuffer() // ###  
implement me!  
* QTBUG-96945 WebM file format not supported for recorder  
* QTBUG-95186 snapCamera fails to show frames  
* COIN-762 Coin's configure command gets warning about unused  
-DBUILD_EXAMPLES=OFF  
  
### qttools  
* QTBUG-97389 'lupdate_sources' variable empty in cmake file generated  
by qt_add_lupdate  
* QTBUG-97562 qdoc: Assert when there's an empty link target  
* PYSIDE-1687 lupdate -tr-function-alias option doesn't work with custom  
function  
* QTBUG-97125 Assistant is unusable on macOS Dark theme  
* QTBUG-97516 Qt Assistant - Background color missing in embedded  
browser  
* QTBUG-97189 Assistant: some keys not working  
* QTBUG-97517 Qt Designer - Command line option "--help-all" has no  
effect  
* QTBUG-97104 macdeployqt fails when qmlimportscanner takes longer than  
30s  
* QTBUG-97627 heap-use-after-free when running ninja html_docs in qtbase  
* QTBUG-97765 FTBFS qttools  
* QTBUG-97174 QDoc: \page command translates underscores to hyphens  
* QTBUG-97949 qdoc: erratic behavior on link text formatting  
  
### qtdoc  
* QTBUG-98110 Doc defines 5.13 and 5.14 without Extended Support, not  
true  
* QTBUG-98327 qt6 doc error  
  
### qtconnectivity  
* QTBUG-97242 Windows: 100% CPU load when reading services and  
characteristics  
* QTBUG-96996 BT LE Android Large descriptor write support  
* QTBUG-97691 lowenergyscanner yields 'width' of 'null' QML warnings  
* QTBUG-96997 BT LE Android min/max characteristic size checks  
* QTBUG-97576 BT LE Android server connectivity status with multiple  
connections  
* QTBUG-97900 Crash when connecting to Bluetooth device on macOS 12  
* QTBUG-98005 QBluetoothDevice asserts in device discovery  
* QTBUG-98073 cork board example crashes on android 12 device when  
targetSDK set to 31  
* QTBUG-98323 Assertion failure when running bluetooth/btchat example  
* QTBUG-96995 BT LE Android mtu() method error on peripheral side  
* QTBUG-93991 Run example Heartrate monitor server on iOS and on Windows  
* QTBUG-98090 macOS examples that need special plist keys need their own  
plist files  
  
### qtwayland  
* QTBUG-97245 Wayland compositor crash when creating and destroying  
windows  
* QTBUG-97094 Wayland modifiers map decoding has flawed logic  
* QTBUG-96298 QInputMethod::visibleChanged was not send when keyboard is  
open and close with QtTextInputMethodManager  
  
### qt3d  
* QTBUG-86493 ComputeCommand.trigger(1) executes compute shader more  
than 1 time  
  
### qtserialbus  
* QTBUG-97685 Qt SerialBus Qt 6 change documentation replaced SerialPort  
documentation  
  
### qtwebsockets  
* QTBUG-97681 C++ classes of the QtWebSockets module have misspelled  
package names in the instructions for CMake  
  
### qtwebengine  
* QTBUG-96930 REG:5.15.3->5.15.4 - When doing a pinch gesture inside a  
WebEngineView then it has no effect  
* QTBUG-96855 QWebEngineDownloadItem::setDownloadFileName failed in disk  
root  
* QTBUG-97598 [Windows] Deadlock on WebEngineView rendering  
* QTBUG-94604 QtWebEngineProcess and resource paths are wrong with  
-developer-build -framework on macOS  
* QTBUG-96375 Build failure with webengine  
* QTBUG-84105 Out-of-proc networking causes firewall confusion  
* QTBUG-97472 [REG] Crash/segfault in ozone implementation when calling  
XkbGetState  
* QTBUG-90904 Crash on calling QAccessible::registerAccessibleInterface  
* QTBUG-98400 CVE-2021-3541 in chromium  
* QTBUG-98401 CVE-2021-3517 in chromium  
* QTBUG-96928 QtWebEngine continuously allocates memory until it get  
killed  
* QTBUG-96942 Developer tools open with "toogle screencast" enabled  
* QTBUG-97188 Make sure that all bots know about the new repo  
* QTBUG-96127 Broken external links in Qt docs  
  
### qtcharts  
* QTBUG-92544 charts/audio has dependency to non-existent module  
Multimedia  
* QTBUG-95870 Setting plotArea for a ChartView in a layout is not  
respected  
* QTBUG-81278 Switching axis that is shared by multiple series to  
another doesn't work  
  
### qtdatavis3d  
* QTBUG-97931 CMake warning about linked plugins in Qt Data  
Visualization  
* QTBUG-97683 [REG 6.2.0.6.2.1] examples-manifest has wrong paths,  
examples not visible in Creator UI  
  
### qtvirtualkeyboard  
* QTBUG-97075 [REG: 5.14.2->5.15.0] Anchors don't work with InputPanel  
anymore  
* QTBUG-56918 When the keyboard is shown for a text field in a modal  
popup then it will not be usable  
* QTBUG-92881 InputPanels defaults z value should be lower than max  
value for overlays  
* QTBUG-97983 Highlighted example virtualkeyboard/basic not configuring  
on Wasm  
* QTBUG-96578 Virtual Keyboard Deployment guide does not cover widget  
applications  
* QTBUG-97830 Some Qt Virtual Keyboard tests checking the position of  
selection handles are failing  
* QTBUG-97901 tst_plugin::test_hangulInputMethod(row 24) fails  
  
### qtnetworkauth  
* QTBUG-97458 String "6.2.0" found from 6.2.1 source package  
  
### qtremoteobjects  
* QTBUG-91041 Remote Objects: Model headers are not updated  
* QTBUG-97688 Clients don't reconnect to replaced nodes over TCP  
  
### qtquick3d  
* QTBUG-96736 Insert #line directives to custom material and effect  
shaders in order to print useful line numbers in error messages  
* QTBUG-98342 View3D mapping functions do not work correctly with  
orthographic camera and 2x pixel ratio  
* QTBUG-96558 RTA CMake test fails on macOS10.15 and macOS11.0  
* QTBUG-97920 Designer editor view has shadow image with model-blend  
particles  
* QTBUG-97586 Setting delegate dynamically before model is set breaks  
Repeater3D  
* QTBUG-97950 Application slowly reads every file in /usr/bin before  
starting  
* QTBUG-98007 Designer puppet crashes at startup  
  
### qtshadertools  
* QTBUG-97458 String "6.2.0" found from 6.2.1 source package  
  
### qt5compat  
* QTBUG-97122 Regression: UTF-32 codec fails on assert when  
fromUnicode() is called  
* QTBUG-96127 Broken external links in Qt docs  
  
### qtopcua  
* QTBUG-96228 [OPCUA] Qt Opc UA client crashes after disconnect /  
reconnect  
  
Known Issues  
------------  
  
* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-6/gettingstarted.html#platform-requirements  
* RTA reported issues from Qt 6.2  
https://bugreports.qt.io/issues/?filter=23315  
* Supported development platforms are listed here:  
https://bugreports.qt.io/browse/QTBUG-90021  
* See Qt 6.2 Known Issues from:  
https://wiki.qt.io/Qt_6.2_Known_Issues  
  
Credits for the  release goes to:  
---------------------------------  
  
Aavitsland Eirik  
Achtelik Mike  
Agocs Laszlo  
Bin Chen  
Blasche Alex  
Blomfeldt Eskil Abrahamsen  
Borisova Tatiana  
Bornemann Joerg  
Boudjelthia Assam  
Brüning Michael  
Buhr Andreas  
Burtsev Kirill  
Croitor Alexandru  
Curtis Mitch  
D'Angelo Giuseppe  
David Szabolcs  
Dawes Rodney  
Edelev Alexey  
Eftevaag Oliver  
Egedi Balazs  
Eklund Iikka  
ElKharashy Hatem  
Funk Kevin  
Gehör Pekka  
Goldstein Maximilian  
Golubev Andrei  
Grönholm Kaj  
Gustavsen Richard Moe  
Haixiang Tang  
Halmet Heikki  
Hao Zhang  
Heikkinen Jani  
Heikkinen Miikka  
Heimrich Karsten  
Hermann Ulf  
Heskestad Øystein  
Hilsheimer Volker  
Jensen Allan Sandfeld  
Jenssen Tim  
Kanapickas Povilas  
Kleint Friedemann  
Klocek Michal  
Knoll Lars  
Kobus Jarek  
Koivikko Jarkko  
Korpipaa Tomi  
Korteniemi Jani  
Kosmale Fabian  
Kurazyan Sona  
Kvinge Jonas  
Köhne Kai  
Lee Inho  
Leinonen Tony  
Lemire Paul  
Li Qiang  
Löhning Robert  
Macieira Thiago  
Martinec Tamas  
Meshcheriakov Ievgenii  
Mira Samuel  
Mohamed Fawzi  
Moskal Bartlomiej  
Mutz Marc  
Määttä Antti  
Nath Biswapriyo  
Nichols Andy  
Nordheim Mårten  
Petäjäjärvi Pasi  
Piippo Samuli  
Pocheptsov Timur  
Pohjanheimo Milla  
Poikelin Joni  
Potinkara Rami  
Potter Lorn  
Qi Liang  
Reinio Topi  
Rocha André de la  
RuiJie Fan  
Rutledge Shawn  
Saario Toni  
Sera Luca Di  
Shaw Andy  
Skoland David  
Solovev Ivan  
Srebrny Piotr  
Strømme Christian  
Sæther Jan Arve  
Sørvig Morten Johan  
Tkachenko Ivan  
Tvete Paul Olav  
Varga Peter  
Verria Doris  
Vestbø Tor Arne  
Voelker Jannis  
Volkov Alexander  
Vuolle Juha  
Weimer Bernd  
Welbourne Edward  
Wicking Paul  
Xi Li  
Yrjänä Marianne  
Zahorodnii Vlad  
Zhao Yuhang  
