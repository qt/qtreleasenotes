Release note  
============  
  
Qt 6.2.4 release is a patch release made on the top of Qt 6.2.3.  
As a patch release, Qt 6.2.4 does not add any new functionality but provides  
bug fixes and other improvements and maintains both forward and backward  
compatibility (source and binary) with Qt 6.2.3.  

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
* fa8b14f830 QTzTimeZonePrivate: fix UB (data race on m_icu)  
Fixed a data race on Unix platforms when implicitly-shared copies of  
QTimeZone objects were used in certain ways (e.g. calling displayName())  
from different threads and Qt was configured with ICU support.  
  
* 6eed0d3f4e JSON: When clearing duplicate object entries, also clear  
containers  
A memory leak in the JSON parser when reading objects with duplicate  
keys was fixed.  
  
* 9540c0b27f Fix crash when text shaping fails  
Fixed a possible crash with certain fonts when shaping strings  
consisting only of control characters.  
  
* 3c193fa077 QScreen_win: retrieve user friendly monitor name  
QScreen::name() now returns the user friendly name instead of the GDI  
device name on Windows. This is consistent with other platforms and also  
obeys the documentation.  
  
* 8f79520cd6 Enable all supported 1.0 device features in QVulkanWindow  
QVulkanWindow is now enabling all Vulkan 1.0 features reported as  
supported from the physical device.  
  
* 2e2d544588 Fix clipped glyphs in text rendering of QGraphicsTextItem  
Clipping of visible glyphs when doing partial updates of a graphics  
view was off by 1. Also fixed an issue that caused rounding errors when  
transforming the clip rect into the glyphs draw space which was caused  
by transforming a QRect instead of a QRectF.  
  
* 44335e65bf Sequential erase/_if: don't apply predicate twice to  
element  
A fix in the implementation of the erase-like algorithms of sequential  
Qt container may re-enable signed/unsigned comparison warnings  
previously suppressed by having occurred in std library code. To fix,  
cast the value to look for such that it has the same signedness as the  
container's elements.  
  
* 899ab8f0df Fix C++20 ambiguous relational operators between  
QJsonValue{,Ref}  
Fixed relational operators to not cause warnings/ambiguities when  
compiling in C++20.  
  
* ab6915f0ef QProcess/Unix: ensure we don't accidentally execute  
something from CWD  
When passed a simple program name with no slashes, QProcess on Unix  
systems will now only search the current directory if "." is one of the  
entries in the PATH environment variable. This bug fix restores the  
behavior QProcess had before Qt 5.9. If launching an executable in the  
directory set by setWorkingDirectory() or inherited from the parent is  
intended, pass a program name starting with "./". For more information  
and best practices about finding an executable, see QProcess'  
documentation.  
  
* 4114c1163b QDesktopServices: fix ABA problem in  
QOpenUrlHandlerRegistry  
Fixed a bug where destroying and re-creating a handler object in quick  
succession could cause the registration for the handler to be lost.  
  
* 360f181857 configure: Allow specifying arbitrary variable assignments  
Users can directly assign CMake variables with configure, for example  
"configure CMAKE_CXX_COMPILE=clang++-11".  
  
* b3d1ea8530 QDesktopServices: deprecate destroying URL handlers w/o  
explicit unsetUrlHandler()  
URL handlers that have been passed to setUrlHandler() must now be  
removed by calling unsetUrlHandler() before they are destroyed. Relying  
on the handler's destructor to implicitly unset it is now deprecated,  
because it may already be in use by concurrent openUrl() calls. Support  
for implicit unsetting will be removed in 6.6 and, until then, a  
qWarning() is raised if it is exercised.  
  
* b3d19fbf95 QMetaObjectBuilder: fix addProperty() recording of the  
property type  
Fixed a bug that would cause addProperty() to use the incorrect type  
for the property if the property's name matched a valid type registered  
with QMetaType.  
  
### qttools  
* 5b641c12a Qt Designer: Enable the QWebEngineView, QQuickWidget plugins  
on Windows  
Qt Designer now sets the Graphics API to OpenGL in order to enable the  
QWebEngineView and QQuickWidget plugins.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-99630 tst_QShortcut::text is flaky in dev  
* QTBUG-99620 QMetaType: type QMap<int,QFlags<Qt::AlignmentFlag>> has  
more than one typedef alias: ColumnAlignmentMap, ColumnAlignmentMap  
* QTBUG-96916 Qt 6 breaks compatibility of QVariant streaming into  
QDataStream  
* QTBUG-99743 QTabWidget rendering broken on macOS 12  
* QTBUG-99676 markdown (and html) import/export should not rely on use  
of a fixed-pitched font to remember a `monospace` span  
* QTBUG-92445 Markdown smashes nested formatting inside lists  
* QTBUG-99148 Broken html list rendering because <code> element  
* PYSIDE-1773 uic doesn't import QAbstractItemView for  
QTableView/QTreeView EditTriggers  
* PYSIDE-1404 Incompatible import of "Object" in compiled UI  

* QTBUG-99771 Porting guide does not mention binary JSON  
* QTBUG-72103 Conversion between QQuaternion and Euler angles has issues  
in special cases  
* QTBUG-99642 Can't define CSS with properties for QToolButton with Qt 6  
* QTBUG-99666 Qt module builds mix install and staging prefixes  
* QTBUG-99799 Memory leak in QJsonDocument::fromJson()  
* QTBUG-92358 One More Crash in text shaping on special string with  
EmojiOneColor font.  
* QTBUG-89155 Assertion violation in text shaping on special string with  
EmojiOneColor font.  
* QTBUG-80666 QNetworkRequest::setHeader(IfModifiedSince) treats local  
time as UTC  
* QTBUG-97535 Bug in examples for QListIterator Class  
* QTBUG-99486 Extra dot appears in top left corner of Fusion style spin  
box frames with no buttons  
* QTBUG-99323 [REG: 5.14.2 -> 5.15.0] Posted events get stuck when  
QCoreApplication::processEvents with QEventLoop::WaitForMoreEvents is  
used  
* QTBUG-100067 network/torrent examples ProgressBar text should be  
layout with horizontal  
* QTBUG-96718 Crash in inBindingWrapper() (Creator built against Qt 6.2  
build)  
* QTBUG-99534 tst_qfuture memleaks  
* QTBUG-95309 Compile fails with Qt in namespace and C++20  
* QTBUG-100072 Building Qt from source fails to compile with C++20  
standard enabled when using MSVC 2022  
* QTBUG-100144 Dependency update on qt/qtwebchannel failed in dev  
* QTBUG-99747 QDate::startOfDay( ) leads to assert in debug build  
* QTBUG-99522 qmake adds @ mark after then the output file name when it  
calls g++ on either Qt's MinGW or MSYS2 platform  
* QTBUG-100074 Building QSharedMemory fails when bootstrapping  
* QTBUG-87136 Animations run twice as fast on a 120hz Android device  
* QTBUG-93823 Android QPlatformScreen does not expose the refresh rate:  
Animations (and timers) too fast on higher refresh rate monitors  
* QTBUG-94959 Timer and animations runs faster after screen touch event  
on Android 11  
* QTBUG-93393 Android A11Y TalkBack: Hidden onPressAction still called  
* QTBUG-100233 Android broken project/wrong libraries linked when adding  
UiTools  
* QTBUG-62185 QVersionNumber seems broken on -O1 and higher with g++  
* QTBUG-95842 testlib's autotest compilation fails with glibc 2.34  
* QTBUG-100315 FEATURE_headersclean does not work with if  
CMAKE_CXX_FLAGS contains more than one option  
* QTBUG-100365 Can't build qt libraries on Windows  
* QTBUG-94608 Nonsensical full path to examples  
* QTBUG-100317 QMacStyle code references missing image resource  
* QTBUG-44096 QNetworkAuthenticationManager does not emit  
authenticationRequired when using NTLM  
* QTBUG-100071 QtFuture::connect fails to compile if the passed signal  
takes a std::tuple as argument  
* QTBUG-93432 QGraphicsTextItem font gets incorrectly clipped when a  
clip rect is set on the painter.  
* QTBUG-100037 QSqlQuery: crash on executing query if connection is  
already closed  
* QTBUG-100416 QPluginLoader::loadHints return "no hints set" but by  
default PreventUnloadHint is set  
* QTBUG-97157 attempting to interact with any widget dialog on  
touchscreen fails; mouse causes crash after that  
* QTBUG-100327 CompositionMode_Screen wrong with drawImage  
* QTBUG-93402 Android A11Y TalkBack: Focus Rect not updated on  
orientation Change  
* QTBUG-100290 Custom build fails with PCH  
* QTBUG-100362  
tst_QNetworkReply::putWithServerClosingConnectionImmediately is flaky  
* QTBUG-63196 QNetworkReply::putWithServerClosingConnectionImmediately  
fails on Windows  
* QTBUG-98476  
tst_QNetworkReply::putWithServerClosingConnectionImmediately fails in  
QtBase with Windows 11  
* QTBUG-100420 QPicture doesn't respect Qt::IntersectClip when used with  
setClipPath  
* QTBUG-100493 QtFinishPrlFile.cmake: No such file or directory with  
multi-config build on Linux  
* QTBUG-96212 The visibility of placeHolderText of the QPlainTextEdit is  
not reevaluated in the setter  
* QTBUG-78797 Shift-select drag distance is zero in QTreeView  
* QTBUG-81542 QListView range selection changes after 1 pixel move  
* QTBUG-99512 QListview  selectcount  error with items of differing  
sizes  
* QTBUG-100438 Incorrect rounding to ms in QTimer when clock too coarse  
* QTBUG-51327 [Windows 8.1]: After maximizing a window and toggling the  
frameless window hint and moving to another monitor then the window can  
be too big  
 
* QTBUG-100545 Nested QML items with Accessible properties set does not  
work on Android  
* QTBUG-100217 [REG 6.2.2  -> 6.2.3] Integer overflow when rendering svg  
image  
* QTBUG-88136 tst_QFutureWatcher fails on Android  
* QTBUG-100775 Several data races around handlers of  
QDesktopServices::openUrl()  
* QTBUG-100482 Network monitoring not working when ZScaler Internet  
Security is active  
* QTBUG-87405 tst_QFontDatabase::systemFixedFont fails for Android  
* QTBUG-88137 tst_QTimeLine fails on Android  
* QTBUG-87400 tst_QAbstractItemView fails on Android  
* QTBUG-87408 tst_QTreeView has failing tests  
* QTBUG-100574 qtbase/src/gui/vulkan/qvulkanfunctions_p.cpp is missing  
dependency on qvkgen tool  
* QTBUG-100364 QStandardPaths GenericDataLocation for iOS seems to  
mention wrong path  
* QTBUG-100518 Crash on iOS 13.3.1  
* QTBUG-100261 QPrinter property setup not effect  
* QTBUG-99504 Linux: QPrinter::setDuplex not effective ( Canon  
imageRUNNER 2520  )  
* QTBUG-100915 moc code generates warning [-Wredundant-parens]  
* QTBUG-52472 Undefined Behaviour in qsimpledrag.cpp line 207  
* QTBUG-45045 SIGFPE in QQuickMenu  
* QTBUG-81917 QtWidgets fails to build with clang 10.0-rc1 in C++20 mode  
* QTBUG-99368 TLS handshake fails due to incorrect cipher handling  
(Secure Transport macOS backend)  
* QTBUG-81583 QTextMarkdownWriter: if a task list item's first line ends  
with monospace text, trailing backtick is omitted  
* QTBUG-99775 Crash on QObject::objectName access when using QThreadPool  
from non-owning thread  
* QTBUG-99009 QCursor::setPos X coordinates is wrong when DPI scaling is  
used    
* QTBUG-92909 When following redirects, a PROPFIND request (and probably  
others) are converted to a GET  
* QTBUG-99803 QVulkanWindow doesn't enable any device features (e.g.  
VkDeviceCreateInfo::pEnabledFeatures)  
* COIN-762 Coin's configure command gets warning about unused  
-DBUILD_EXAMPLES=OFF  
* QTBUG-99506 Loader with states and children loaders crashes on  
Integrity (release only)  
* QTBUG-95764 pure virtual call in QAccessibleQuickItem  
* QTBUG-98478 tst_QFileSystemWatcher::signalsEmittedAfterFileMoved fails  
in QtBase with Windows 11  
* QTBUG-6905 font-weight: bold can truncate tab label  
* QTBUG-100412 tst_qsrceen::grabWindow is flaky on Windows  
* QTBUG-99491 Windows - Android App, cmake build does not update  
correctly if app library is bigger than 2GB  
* QTBUG-100651 Unable to follow HTTP/2 redirects  
* QTBUG-45582 Duplicated vtables due to inline virtual functions  
(probably all dtors)  
* QTBUG-93396 Android A11Y TalkBack: Slider does not announce value on  
change  
* QTBUG-100401 QToolbutton with popupMode QToolButton::InstantPopup and  
stylesheet have 2 arrows  
* QTBUG-100790 tst_QInputDevice::multiSeatDevices() fails on Wayland  
* QTBUG-100891  
tst_QGuiApplication::genericPluginsAndWindowSystemEvents() fails on  
Wayland  
* QTBUG-100792 tst_QScreen::grabWindow() fails on Wayland  
* QTBUG-66818 tst_QWindow::initialSize fails on Wayland  
* QTBUG-100887 tst_QWindow::mouseToTouchTranslation() fails on Wayland  
* QTBUG-100888 tst_QWindow::modalWindowPosition() fails on Wayland  
* QTBUG-100889 tst_QWindow::requestUpdate() fails on Wayland  
* QTBUG-100930 tst_QGraphicsWidget::updateFocusChainWhenChildDie fails  
on QNX  
* QTBUG-100929 tst_QImage::hugeQImage fails on platforms without  
adequate memory  
* QTBUG-87674 qaccessibility fails on Android  
  
### qtsvg  
* QTBUG-99642 Can't define CSS with properties for QToolButton with Qt 6  
  
### qtdeclarative  
* QTBUG-99477 Crash in QRhiD3D11::executeCommandBuffer with nullptr  
access  
* QTBUG-99644 invalid access of indicator item inside switch type  
destructor  
* QTBUG-99888 configure fails when only qtdeclarative and qtbase are  
checked out  
* QTBUG-99273 QtDeclarative fails to configure when Python is not in  
PATH but is found via FindPython  
* QTBUG-100046 FAIL!  : tst_qquickborderimage::borderImageMesh()  
* QTBUG-99604 TextArea and TextField don't use IBeamCursor when readOnly  
and selectByMouse are both true  
* QTBUG-99608 tst_qmlcachegen (Failed)  
* QTBUG-99974 qt.labs.qmlmodels classes documented twice  
* QTBUG-99311 QtQuick Window does not expose enum of visibility property  
of Window  
* QTBUG-100339 qmllint does not find ApplicationWindow.window  
* QTBUG-100326 *.mjs files not added to qmldir when added to  
qt_add_qml_module()  
* QTBUG-99124 Properly document ScrollBar in ScrollView  
* QTBUG-98039 QML javascript: "this" in class ctor becomes undefined  
during if(){...} in arrow functions  
* QTBUG-100366 tst_qmlcachegen tests using generateCache are valid only  
for host  
* QTBUG-100260 Crash on access after using QML singleton as a model  
* QTBUG-95033 ButtonGroup does not work with Windows style Button  
* QTBUG-97185 Quick DragHandler Reporting Wrong Coordinates using  
TouchScreen Input  
* QTBUG-98486 Touch points coordinates does not take into account the  
Device Pixel Ratio on Windows  
* QTBUG-98543 Invalid updates of contentY of Flickable on touch screen  
* QTBUG-99547 PathView item does not appear in certain circumstance  
* QTBUG-51078 Use of Item obligatory in SwipeView?  
* QTBUG-51669 QQC2: SwipeView is not working as expected  
* QTBUG-100469 Qml runtime resizeToItem configuration is not working  
* QTBUG-100221 qtdeclarative compilation fails on arm64  
* QTBUG-100279 Building fails on Linux ARM64  
* QTBUG-94161 "QTransform::translate with NaN called" when hovering over  
window containing Imagine style GroupBox containing a TextEdit  
* QTBUG-86695 [REG: 5.12 -> 5.14] Broken State::when behavior after  
suspicious change  
* QTBUG-95763 Configuring an executable with an attached qml module  
fails when using the Xcode generator  
* QTBUG-100380 valueAt(int index) method of ComboBox QML type (QQC2) is  
undocumented  
* QTBUG-100680 TableView: positionViewAtRow will in some cases move the  
viewport too far  
* QTBUG-100377 [REG 5.15 -> 6.2] Date.parse() can't handle some dates on  
Qt 6 but works in Qt 5  
* QTBUG-100855 qmljs tool doesn't link on iOS build  
* QTBUG-95587 icon.source of Control is not resolved relative to user  
code  
* QTBUG-99615 Most QMutableEventPoint usage depends on Undefined  
Behaviour  
* QTBUG-99665 tst_qquickfolderlistmodel segfaults on ARM  
* QTBUG-98404  tst_qmlcachegen (Failed)  
* QTBUG-99436 Quick Drag and Drop Tiles example broken in Qt 6  
* QTBUG-91706 QML: Subclassing a QQuickItem that has revisioned  
properties fails  
* QTBUG-92591 QtDeclarative autotest configure fails on Android builds  
* QTBUG-100040 Configuring qtdeclarative fails for qmljs, qmljsrootgen  
and qjstest fails when cross-compiling  
* QTBUG-99128 qmlsc does not see property revisions  
* QTBUG-64470 tst_QQuickFramebufferObject::testInvalidate is failing on  
macOS  
* QTBUG-65614 tst_QQuickFramebufferObject failed on b2qt  
* QTBUG-76546 QML debugger tests that run a sub-process fail on QNX  
* QTBUG-95750 RangeSlider::test_overlappingHandles test fails on  
LinuxUbuntu_20_04x86_64LinuxQEMUarmv7GCC  
* QTBUG-100003 tst_qqmlmoduleplugin fails on Android  
* QTBUG-100014 tst_qqmlqt fails on Android  
* QTBUG-100016 tst_qquickfolderlistmodel fails on Android  
* QTBUG-100018 tst_qmltc_manual fails on Android  
* QTBUG-100020 tst_qqmljsscope fails on Android  
* QTBUG-100021 tst_qdebugmessageservice crashes on Android  
* QTBUG-100164 tst_qqmldebugtranslationservice fails on Android  
* QTBUG-100166 tst_qqmlenginedebugservice fails on Android  
* QTBUG-100167 QML debugger tests fail on Android  
* QTBUG-100169 tst_qqmlextensionplugin fails on Android  
* QTBUG-100171 tst_qmldomitem fails on Android  
* QTBUG-100173 tst_qquickwidget fails on Android  
* QTBUG-100175 tst_testfiltering fails on Android  
* QTBUG-100176 tst_qquickapplicationwindow crashes on Android  
* QTBUG-100177 tst_qquickheaderview fails on Android  
* QTBUG-100191 tst_sanity and tst_snippets fail on Android  
* QTBUG-100253 tst_qquickpopup fails on Android  
* QTBUG-100254 tst_qquickmenubar fails on Android  
* QTBUG-100256 tst_qquickmenu fails on Android  
* QTBUG-100257 tst_qquickdrawer fails on Android  
* QTBUG-100258 tst_focus crashes on Android  
* QTBUG-100431 Crash in libQt5Qml V4 engine caused by wrong memory  
access  
* QTBUG-45045 SIGFPE in QQuickMenu  
* QTBUG-52472 Undefined Behaviour in qsimpledrag.cpp line 207   
* QTBUG-75786 macOS 10.14 autotest failures  
* QTBUG-82015 qquickanimations::simplePath() is flakey on macOS  
* QTBUG-82043 tst_qquickmousearea::pressAndHold() is flakey on macOS  
* QTBUG-82404 tst_qquickbehaviors::currentValue is flaky on macos  
* QTBUG-85622 tst_qquickloader: urlToComponent is flaky on macos  
* QTBUG-85624 tst_qquickanimations: reparent is flaky on macos  
* QTBUG-88541 tst_qquickpointhander::tabletStylus doesn't work on hidpi  
* QTBUG-95863 tst_qquickpathview::snapOneItem() is flaky on macOS  
  
### qtmultimedia  
* QTBUG-99661 audioDevice & cameraDevice list properties as methods  
* QTBUG-97838 Recording broken on Apple Silicon / M1  
* QTBUG-99583 Default audio output device not listed as default in  
MediaDevices.audioOutputs  
* QTBUG-99357 Fix SeekPauseSeek Test in Android  
* QTBUG-99849 Doc refers to nonexistent QImageCapture::CaptureToBuffer  
setting.  
* QTBUG-99650 QVideoSink unworkable on Android  
* QTBUG-100050 [REG 6.2.3(and 2)->6.2.1] namespace build fails on  
Windows, MinGW9.0 and MSVC2019  
* QTBUG-100106 Qml Video::seek() fails with TypeError  
* QTBUG-99643 Documentation shows use of deleted QImageCapture  
constructor  
* QTBUG-100341 [REG 6.2.2 - 6.2.3] Memory leak on MediaPlayer  
destruction  
* QTBUG-100283 "Video" keep sending positionChanged signal  
* QTBUG-100347 [qtmultimedia] win32 compile error with 6.2.3  
* QTBUG-100501 Typo in documentation of QMediaRecorder  
* QTBUG-100363 [REG 6.2.2 - 6.2.3] Video is always black with OpenGL RHI  
* QTBUG-100337 [Win] Vertically oriented video is upside down  
* QTBUG-100665 Crash in OpenGlVideoBuffer destructor  
* QTBUG-100638 SoundEffect fails to load .wav files  
* QTBUG-99038 Android:  Fix qmlvideo issues  
  
### qttools  
* QTBUG-100308 Unable to build qttools with tests with the 'Ninja Multi-  
Config' generator  
* QTBUG-100316 qdoc: ASSERT: "actualNode" in file  
qttools/src/qdoc/docbookgenerator.cpp, line 4246  
* QTBUG-96549 make clean removes ts file when using  
qt5_create_translation()  
* QTBUG-94345  Qt Designer crash in QQuickWidget plugin  
* QTBUG-100285 Windows: Qt Designer crash when selecting QWebEngineView  
  
### qtdoc  
* QTBUG-99847 Update Qt Creator info in Qt Quick tutorial  
* QTBUG-100434 Tutorials/alarms not launching on macOS  
* QTBUG-100383 Qt 6.2.3: 3rd party code update missing in docs  
* QTBUG-98542 new purchasing is broken on Android when using public key  
verification  
* QTBUG-97449 Clean Android build docs for Qt 6  
  
### qtpositioning  
* QTBUG-92967 Port addon-module cmake tests from Qt5 to Qt6  
  
### qtconnectivity  
* QTBUG-99617 SDP attribute write fail  
* QTBUG-99673 Service discovery with UUID filter doesn't work on macOS  
Monterey  
* QTBUG-99687 Windows BT service scan scans just one device  
* QTBUG-99410 [macOS 12.1] Bluetooth data stream blocked when main menu  
opened  
* QTBUG-100445 macOS bluetooth SDP records contain anomalies  
* QTBUG-99689 Windows BT service scan filter fails against Linux server  
* QTBUG-100289 pingpong Linux => Windows doesn't work  
* QTBUG-100819 Bluez lowenergy peripheral incomplete initialization  
* QTBUG-100303 Bluetooth RFComm [Outbound] connection issue with  
Monterey  
* QTBUG-100894 Linux bluetooth crash when multiple services found  
* QTBUG-100042 Windows BT (server) pingpong service is not found  
* QTBUG-99685 Windows BT classic service scan doesn't always start  
* QTBUG-94001 QtBluetooth uses deprecated Windows API  
  
### qtwayland  
* QTBUG-99746 QtWayland fails to compile against recent EGL headers  
* QTBUG-97593 Qt with QtWayland doesn't build without QtQml  
* QTBUG-99965 Build with -no-feature-tabletevent fails for Linux/Wayland  
* QTBUG-100150 Touch event ignored when main GUI thread is slow  
  
### qt3d  
* QTBUG-99945 [REG 6.2.2-> 6.2.3] qt3d/audio-visualizer-qml fails to  
compile  
  
### qtwebsockets  
* QTBUG-100054 QWebSocket can emit binaryMessageReceived signal after  
being disconnected  
* QTBUG-92967 Port addon-module cmake tests from Qt5 to Qt6  
  
### qtwebchannel  
* QTBUG-92967 Port addon-module cmake tests from Qt5 to Qt6  
  
### qtwebengine  
* QTBUG-99215 Html popups do not work correctly.   
* QTBUG-99669 Glib network plugins doesn't configure or build  
* QTBUG-99890 QtWebEngine ozone platform needs pkgconfig check for  
xkbfile include  
* QTBUG-94924 Load signals not emitted when opening a google result  
* QTBUG-100032 tst_qquickwebview: malloc_consolidate(): invalid chunk  
size  
* QTBUG-100285 Windows: Qt Designer crash when selecting QWebEngineView  
* QTBUG-100293 spellcheck error: session_bridge_ was not declared  
* QTBUG-100435 Cannot enable webrtc-pipewire feature  
* QTBUG-96597 Crash on WebEngine(View|Profile).userScripts.collection  
property get  
* QTBUG-100500 System libxslt is not used  
* QTBUG-101084 Test  #1: tst_qwebenginecookiestore  
.................***Failed  
* QTBUG-101215 QML certifciate errror test is broken, but works on c++  
side  
  
### qtcharts  
* QTBUG-100810 QML ChartView series color can get wrong on RHI if  
useOpenGL  
* QTBUG-92967 Port addon-module cmake tests from Qt5 to Qt6  
  
### qtscxml  
* QTBUG-92967 Port addon-module cmake tests from Qt5 to Qt6  
  
### qtremoteobjects  
* QTBUG-85124 QRemoteObjectHost::hostUrl() crashes if no URL is set  
* QTBUG-92967 Port addon-module cmake tests from Qt5 to Qt6  
  
### qtquick3d  
* QTBUG-99430 Crash if a Model is created via Repeater3D  
* QTBUG-94616 Low saturation of sky texture  
* QTBUG-99992 AssetUtils.RuntimeLoader requires absolute file path for  
source  
* QTBUG-97715 Quick3D examples fail on imx6  
* QDS-6081 Changing camera on View3D doesn't change the view in form  
editor  
* QDS-4966 Editing Model source with property editor fails  
  
### qt5compat  
* QTBUG-100024 qt5compat requires qtdeclarative despite it's not really  
required  
* QTBUG-100359 tst_qlinkedlist.cpp doesn't build: missing  
QLinkedListIterator  
  
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
Agocs Laszlo  
Arvidsson Viktor  
Bennett Nicholas  
Blackquill Jan  
Blomfeldt Eskil Abrahamsen  
Bohn Sören  
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
Davis Noah  
Edelev Alexey  
Eftevaag Oliver  
Eklund Iikka  
Fedin Ilya  
Funk Kevin  
Gaist Samuel  
Gehör Pekka  
Goldstein Maximilian  
Gruendl Henning  
Gustavsen Richard Moe  
Haixiang Tang  
Halmet Heikki  
Hao Zhang  
Hartmetz Andreas  
Heikkinen Jani  
Heikkinen Miikka  
Heimlich Christian  
Hermann Ulf  
Hilsheimer Volker  
Jensen Allan Sandfeld  
Kleint Friedemann  
Klocek Michal  
Knoll Lars  
Ko Seokha  
Korteniemi Jani  
Kosmale Fabian  
Krus Mike  
Kurazyan Sona  
Kvinge Jonas  
Köhne Kai  
Lee Inho  
Leinonen Tony  
Li Qiang  
Macieira Thiago  
Meshcheriakov Ievgenii  
Miettinen Leena  
Mira Samuel  
Mozzhuhin Andrey  
Mutz Marc  
Nanthiran Sivan  
Neumann Alexander  
Nichols Andy  
Nishihara Yuya  
Nordheim Mårten  
Ollila Kimmo  
Petäjäjärvi Pasi  
Piippo Samuli  
Pocheptsov Timur  
Poikelin Joni  
Qi Liang  
Reinio Topi  
Rocha André de la  
Rosenkraenzer Bernhard  
Rutledge Shawn  
Saario Toni  
Schäpers Björn  
Shaw Andy  
Solovev Ivan  
Spoerl Axel  
Srebrny Piotr  
Stewart Patrick  
Storsjö Martin  
Strømme Christian  
Sørvig Morten Johan  
Terrier Benjamin  
Tkachenko Ivan  
Trotsenko Alex  
Tuliniemi Jere  
Varga Peter  
Vatra BogDan  
Verria Doris  
Vestbø Tor Arne  
Vuolle Juha  
Wang ChunLin  
Weimer Bernd  
Welbourne Edward  
Wolff Oliver  
Xuetian Weng  
Yong Zhang  
Zhao Yuhang  
