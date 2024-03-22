Release note  
============  
Qt 6.6.3 release is a patch release made on the top of Qt 6.6.2.  
As a patch release, Qt 6.6.3 does not add any new functionality but provides  
bug fixes and other improvements and maintains both forward and backward  
compatibility (source and binary) with Qt 6.6.2.  

For detailed information about Qt 6.6, refer to the online documentation  
included in this distribution. The documentation is also available online:  
  
https://doc.qt.io/qt-6/index.html  
  
The Qt version 6.6 series is binary compatible with the 6.5.x series.  
Applications compiled for 6.5 will continue to run with 6.6.  
  
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
* 1772c99267 Update Zlib to 1.3.1  
zlib was updated to version 1.3.1.  
  
* 2a2875ce67 windows: Avoid infinite recursion with certain fonts  
Fixed an issue where an infinite recursion could occur if the system  
had a font with multiple preferred names in non-English languages.  
  
* c64fb06afa Fix clipped text when combining multiple writing systems  
Fixed an issue where drawing text from different writing systems in the  
same line and including a background could cause parts of the text to be  
clipped.  
  
* 64736d2ece Doc: Update Copyright in md4c license text  
Updated md4c (optional part of Qt Gui) to version 0.5.1.  
  
* fb92bb073e API Review Widgets: Remove QDockWidget debug operators  
Removed debug streaming operator incorrectly introduced as a new symbol  
in Qt 6.6.1.  
  
* 0624fb868f Update public suffix list  
Updated the public suffix list to upstream SHA  
883ced078a83f9d79a98933145425c221a5e51f0.  
  
* 3610198ab0 QPainterPath: Fix boundingRect and controlPointRect  
ignoring start point  
boundingRect() and controlPointRect() now use the start point from  
QPainterPath(const QPointF &startPoint).  
  
* b5ae9666b4 QBitArray: avoid overflow in size-to-storage calculations  
Fixed a bug with QBitArrays whose size() came within 7 of the  
size_type's maximum.  
  
* aef6388a17 QBitArray: fix potential truncation in QDataStream op>>()  
Fixed undetected overflows in the deserialisation (opertor>>()) from  
QDataStream.  
  
* 48b36d89c4 Update bundled libpng to version 1.6.41  
libpng was updated to version 1.6.41  
  
* 5de945fb3c SQLite: Update SQLite to v3.45.1  
Updated SQLite to v3.45.1  
  
* 0f541bbc1b QMovie non-anim: use QImageReader::imageCount but not  
nextImageDelay  
QMovie now handles non-animated multi-frame image formats (such as  
tiff): QImageIOHandler::imageCount() is observed, and the default frame  
rate is 1 FPS.  
  
* 14671775ed Update md4c to 0.5.2  
md4c was updated to 0.5.2.  
  
* 027724d66e Update bundled libjpeg-turbo to version 3.0.2  
libjpeg-turbo was updated to version 3.0.2  
  
* 4f88c3e3ac Update QLocale and calendar data to CLDR v44.1  
Updated QLocale's data extracted from the Unicode Common Locale Data  
Repository (CLDR) to v44.1. The license changed to Unicode License V3.  
  
* 85ac5cb979 Update bundled libpng to version 1.6.42  
libpng was updated to version 1.6.42  
  
* 42aa064c9d Update Valgrind to version 3.22.0  
Updated Valgrind header used by QtTest. The change only affects  
portability of s390 inline assembler.  
  
* 3738a2dc67 CMake: Fix undefined symbol: qt_resourceFeatureZstd issue  
Targets created with qt_add_executable and qt_add_library will now add  
the --no-zstd option to AUTORCC_OPTIONS when the target platform does  
not support zstd decompression. You can opt out via the  
QT_NO_AUTORCC_ZSTD cmake variable.  
  
* 1e75a10294 QBitArray: don't create invalid Qt 5 streams  
Now refuses to stream a QBitArray with size() > INT_MAX to a  
Qt-5-compatible QDataStream.  
  
* bf7c7f0d74 WASM builds now handle bitmap and pixmap cursors  
Previously, bitmap and pixmap cursors were nonfunctional in wasm builds  
and would trigger warnings.  These cursors now work as expected.  
  
* 1286c7e5c8 QDialogButtonBox: Fix focus chain and default button  
assignment  
Default button becomes focus proxy of a QDialogButtonBox. This ensures  
that Enter triggers the default button, instead of the first button in  
the layout.  
  
* 3e284681db QGtk3Theme: Fix QGtk3Interface::fileIcon  
Fixed file icons provided by QFileIconProvider when using the gtk3  
platform theme.  
  
* 179164ef14 PCRE2: upgrade to 10.43  
PCRE2 was updated to version 10.43.  
  
* 566fe27f4a Update bundled libpng to version 1.6.43  
libpng was updated to version 1.6.43  
  
* 2287723ed3 SQLite: Update SQLite to v3.45.2  
Updated SQLite to v3.45.2  
  
### qtdeclarative  
* bb28e7e14f Fall back to retrying with "software" when swapchain fails  
The fallback to a software rasterizer, if applicable to the platform  
and 3D API, is now performed also upon the first swapchain creation  
failure. Previously this was only done if the QRhi initialization  
failed. Relevant in particular on Windows, potentially allowing  
functioning on systems that are incapable of proper accelerated D3D  
rendering, but, for whatever reason, do not fail early on upon the  
device/context creation, only later at swapchain creation.  
  
* fe7687785a Material: remove ComboBox's insets  
ComboBox's insets were removed. This may cause visual changes to UIs.  
  
### qtmultimedia  
* ae13259f6 Update doc and attributions with new FFmpeg version in  
Multimedia  
Updated FFmpeg to n6.1.  
  
### qtdoc  
* c322b847 Update iOS supported platforms and toolchain to iOS 17/Xcode  
15  
Xcode 15 is now both supported and required for Qt for iOS. To develop  
for iOS 17 devices, please use Qt Creator 13, or generate an Xcode  
project using qmake or CMake and use Xcode directly.  
  
### qtopcua  
* 37890bd6 Replace incorrect license attribution for 3rdparty/open62541  
Correctly refer to the CC-BY-SA0 license as "Creative Commons  
Attribution Share Alike 4.0 International".  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-120509 Crash when Qt re-create native windows if  
WA_DontCreateNativeAncestors is set  
* QTBUG-120962 QTextCursor::removeSelectedText leads to crash  
* QTBUG-114941 Qt 6.6 Beta 1 and Qt Creator 11.0.0-beta2 - Test  
permissions - Bluetooth fails on Android 14  
* QTBUG-120436 sqldrivers always build in release  
* QTBUG-114958 dev/6.7: Windows: qsb crashes in debug build, causing  
qtdeclarative build to fail  
* QTBUG-120317 qt6<target_name>_debug_metatypes.json: illegal value  
* QTBUG-121472 qmltyperegistrar.exe fails to parse metatypes.json file  
* QTBUG-121498 tst_QAbstractItemView::removeIndexWhileEditing() failed  
on Wayland  
* QTBUG-120469 Crash in QCocoaSystemTrayIcon::emitActivated() when  
calling QComboBox clear() then addItem()  
* QTBUG-121008 Crash in QMacAccessibilityElement when using  
QTreeView/QCombobox  
* QTBUG-121515 [Reg 6.6.1 -> 6.6.2] QNetworkAccessManager never finishes  
request if server sends status code 401 without a challenge  
* QTBUG-118238 【Windows】stack overflow after launch Any Qt Application  
(or Official Demo)  
* QTBUG-121040 [Reg 5.1 -> 5.15 and all 6.*] QTextDocumentation does not  
handle background of HTML string correctly  
* QTBUG-74471 QFileSystemModel shows directories with  
setFilter(QDir::Files)  
* QTBUG-115459 Possible infinite loop triggered by unmaximizing the  
window in 6.5.0+  
* QTBUG-121557 [Reg 6.4.3->6.6] Application unusable after closing  
nested message boxes  
* QTBUG-121713 QXkbCommon::keysymToQtKey does not map XF86Calculator  
* QTBUG-121729 error: Multiple commands produce same *_metatypes.json  
* QTBUG-121926 rerun of cmake loses build type  
* QTBUG-117429 TIFF AnimatedImage memory leak  
* QTBUG-120369 iOS: Crash after changing screen orientation  
* QTBUG-120530 QDomDocument doc refers to QXmlQuery which doesn't exist  
in Qt6  
* QTBUG-99178 QFileSystemModel should have an option to disable icon  
loading; crashes if the icon provider is null  
* QTBUG-121873 The description and the snippet don't match in  
QDBusAbstractInterface::asyncCall  
* QTBUG-121697 Critical crash when creating QPlainTextEdit when using  
styles/stylesheets.  
* QTBUG-121790 QApplication::setStyleSheet crashes QTextEdit  
* QTBUG-121485 QLocale method nativeCountryName returns wrong values.  
* QTBUG-121948 RCC compression is broken when deploying to Android from  
a Linux host using CMake  
* QTBUG-106466 build android app with Debian host fails on undefined  
symbol qt_resourceFeatureZstd  
* QTBUG-101353 AUTORCC uses zstd even if Qt is build without rcc support  
* QTBUG-121668 Qt Notifier example - notifications do not work on  
Android 13  
* QTBUG-103476 Custom`Delegate::destroyEditor()` is not called for some  
editor when removing a tree branch  
* QTBUG-122054 Massive performance loss of QTreeView::expandAll  
* QTBUG-121875 Typo in the document  
* QTBUG-120688 Explicitly document behavior for QFileInfo if file is  
directory  
* QTBUG-119148 layer.samples value not clipped in Qt6  
* QTBUG-85425 Fusion style adds unneeded space for QGroupBoxes without a  
title on Linux  
* QTBUG-95472 CLONE - Fusion style adds unneeded space for QGroupBoxes  
without a title  
* QTBUG-119795 Adding QOpenGLWidget to a QDialog in a maximized  
QMainWindow maximizes the QDialog  
* QTBUG-122210 [REG 6.6.1->6.6.2] widgets/itemviews/editabletreemodel  
not compiling on iOS  
* QTBUG-118489 Can't tab to last button in QDialogButtonBox  
* QTBUG-122200 Header files are not being copied into the Qt* frameworks  
in custom build  
* QTBUG-119447 RHI - QRhiResourceUpdateBatch::readBackBuffer() fails to  
read compute buffer on Metal  
* QTBUG-116927 markdown writer omits trailing ** if a bold span exceeds  
the wrap limit  
* QTBUG-121881 QT_DEPLOY_QML_DIR: Custom value causes empty "qml" folder  
to be created  
* QTBUG-106526 markdown writer should never wrap headings, but wraps  
them if they are too long  
* QTBUG-122087 QTimer::isActive returns true if interval is Invalid  
* QTBUG-122139 DirectWrite's default hinting looks off  
* QTBUG-122167 REG: Kerning errors with DirectWrite font backend  
* QTBUG-122266 property "AUTORCC_OPTIONS" is not allowed  
* QTBUG-122254 Documentation example of  
QCborStreamReader::readString()/QCborStreamReader::readByteArray is  
wrong  
* QTBUG-114608 Programmatically setting focus does not move VoiceOver  
* QTBUG-119864 QPushButton or QToolButton does not receive mouse events  
after calling setMenu().  
* QTBUG-121906 Copyright year in so files not updated to 2024  
* QTBUG-121928 Remove Copyright year from About Qt & command line tools  
* QTBUG-122192 CONFIG *= silent fails at linking  
* QTBUG-122451 Floating point in raster drawBitmap together with strict  
QImage::scanLine causes assertion "i >= 0 && i < height()"  
* QTBUG-122622 configure on Windows can't handle unquoted -DFOO=0  
arguments  
* QTBUG-118983 CTest prints output from a failed test twice  
* QTBUG-88721 QTextDocument::find() does not work well with  
QRegularExpressions  
* QTBUG-122637 qmessagebox.h: extra ';' after member function definition  
[-Wextra-semi]  
* QTBUG-122109 QTreeWidget's columns do not seem to resize properly  
after upgrading from Qt6.5.3 to Qt6.1.1  
* QTBUG-120699 QHeaderView in QTableView doesn't restore geometry  
* QTBUG-116550 [schannel] Qt warning "QIODevice::write (QTcpSocket):  
device not open"  
* QTBUG-122674 Build failure on x32 ABI  
* QTBUG-107486 Typo in the document  
* QTBUG-119080 a11y: Checkbox lacks AT-SPI "checkable" state  
* QTBUG-96348 QWindowsSystemTrayIcon::showMessage: Windows Handle leak  
* QTBUG-62945 Windows: QSystemTrayIcon::showMessage causes GDI-Object  
leak  
* QTBUG-122073 If SQL Engine does not support lastInsertId QList will  
assert  
* QTBUG-122739 qtpaths/qmake don't honor qtconf in some cases with LTO  
enabled  
* QTBUG-121126 Crash when restoring maximized window of application with  
tabified dock widgets  
* QTBUG-122001 QMainWindow::tabifiedDockWidgets() - Not accurate  
* QTBUG-81662 Indentation in QML RichText after list is wrong  
* QTBUG-122749 [Crash] WebEngine Print Me example app crashes when  
changing the page orientation  
* QTBUG-120694 QDockWidget resize issue with Qt 6.6.1  
* QTBUG-102196 QDockWidget: wrong mouse cursor icon used when dock  
widget floating, has custom title bar & contains window container  
* QTBUG-105871 QUdpSocket stop emitting ReadyRead signal in  
QueuedConnection  
* QTBUG-115598 tst_QWidget::render() with QtWayland failed on Ubuntu  
22.04, GNOME  
* QTBUG-40561 QDomText::splitText leaks memory  
* QTBUG-122663 Live Preview doesn't work on Boot2Qt  
* QTBUG-122944 Dragged toplevel is re-attached even after  
wl_data_device.leave  
* QTBUG-122949 Toplevel drag only works on left monitor  
* QTBUG-121561 Android: in TextField: cannot edit inside of words, only  
at the end [regression]  
* QTBUG-118434 [Reg Qt5->Qt6] QMenu cannot arrange menu entries  
correctly when there are large quantity of them  
* QTBUG-122973 QDateTime::operator== documentation is wrong  
* QTBUG-113432 RubberBand update area is too small in QListView  
* QTBUG-122821 QListView with checkable items duplicates checkbox  
* QTBUG-122825 QAbstractItemView::indicator not working properly  
* QTBUG-102820 [REG 5.15.2 => 6.2.4] Styled indicators not drawn in  
itemviews  
* QTBUG-122893 Sending QNetworkRequest fails on singlethreaded WASM  
* QTBUG-119216 macOS: REG->6.5: DnD with custom text MIME type got  
broken/crashes  
* QTBUG-120602 Cannot build Qt modules standalone for iOS  
* QTBUG-120682 Creating QSslSocket when schannel is in use takes too  
long time  
* QTBUG-101141 moc: namespaced base class not properly resolved in  
cpp.json file  
* QTBUG-119490 qcocoaapplicationdelegate.mm:354:20: error: cannot  
initialize return object of type 'BOOL'  
* QTBUG-122042 Shortcut icons for the delete and backspace keys seem to  
be wrong  
* QDS-11733 Delete icon points in wrong direction on macOS  
* QTBUG-94460 QLocale's names for languages, scripts and territories  
don't match CLDR's en.xml's proper names  
* QTBUG-52021 Blink timer for QLineEdit not killed after QMenu spawn  
* QTBUG-118318 QStringConverter/Win doesn't handle resumption for  
encodings with more than 2 octets per character for convertToUnicode  
* QTBUG-120276 Crash when reparent a native child to a different tlw if  
QT_WIDGETS_RHI=1 is set on Windows  
* QTBUG-122596 [REG 6.7.0->6.8.0] error in configure step, top level  
build, MinGW  
* QTBUG-122138 QTzTimeZoneCache::findEntry() parses files while holding  
QTzTimeZoneCache::m_mutex  
* QTBUG-122137 REG: QtWebEngine / Pdfwidgets no longer supports plugins  
* QTBUG-122704 QPainterPath de-serialisation from QDataStream fails if  
item isn't empty  
* QTBUG-109708 Startup crash in QRhiD3D11::endFrame() with nullptr  
access  
* QTBUG-122838 Android multi-abi builds broken if depfiles are used  
* QTBUG-105009 [REG 5.15.2->6.3.1/6.4.0 Beta2] You can still insert  
Chinese text into a QTextEdit when "readOnly" property is enabled.  
* QTBUG-110838 edit components ReadOnly invalid via some input method  
* QTBUG-119182 Readonly QLineEdit writable using input method  
  
### qtsvg  
* QTBUG-120653 All SVGs with paths with more than 32768 points render  
incorrectly  
* QTBUG-121981 QtSvg parser does not handle nested svg elements  
correctly  
* QTBUG-120507 [REG 6.2.2 -> 6.2.3] Trying to render particular svg file  
takes much longer than before  
  
### qtdeclarative  
* QTBUG-120568 "Using the Configuration File in a Project" only covers  
qmake way and not cmake  
* QTBUG-119994 the documentation seems to be contradictory to the code  
snippet  
* QTBUG-119903 the link to elevated card cannot be found  
* QTBUG-120065 Non-native FileDialog loses URL schema when filename is  
manually entered  
* QTBUG-115953 Interactive Flickable with pressDelay makes  
childMouseEventFilter to lose MouseButtonPress event  
* QTBUG-120301 QQuickStateGroup taking null pointers leads to crash  
* QTBUG-120512 Inconsistent behaviour between qmlsc and JIT compiler  
when setting a property to "undefined"  
* QTBUG-111729 Assertion failed in QJSEngine when repeatedly deleting &  
adding property getters on an object  
* QTBUG-116426 crash in QQuickItemPrivate::derefWindow  
* QTBUG-120450 Allocating or deallocating a QJSEngine object causes a  
crash if the application has called mlockall(MCL_CURRENT|MCL_FUTURE)  
* QTBUG-113695 qmllint: property-changes-parsed suggests can code that  
don't understand  
* QTBUG-118710 [REG 6.5.2 → 6.5.3] QQmlProperty: wrong warning about  
signal handler capitalization  
* QTBUG-121216 Drawer item does not support rotation for touch input  
* QTBUG-80910 Drawer item does not support rotation  
* QTBUG-71117 When the contentOrientation is changed for the  
ApplicationWindow, then the Drawer does not drag out as expected  
* QTBUG-115536 Setting Window.contentOrientation breaks Popup on regular  
desktop  
* QTBUG-119326 application crash when using QML-Debugger: Component vs  
.qml  
* QTBUG-109261 qmlsc dead code analysis is incomplete  
* QTBUG-121710 [Reg 6.6.0 -> 6.6.1] Aliasing to enums does not work as  
in Qt 6.6.0 an earlier anymore  
* QTBUG-121734 SetLookup crashes on hierarchy of shadowable properties  
* QTBUG-119984 old way of exposing c++ class to qml is written  
* QTBUG-122081 FAIL!  : tst_qqmllocale::toString(locale.toString(new  
Date(2000, 1, 1))) Compared values are not the same  
* QTBUG-119459 [Reg 5.15 -> 6.2] the line number output by  
console.trace() is too big  
* QTBUG-122173 tst_qquickanimatedimage::currentFrame() is flaky on  
windows  
* QTBUG-120499 [REG 6.5.3 - 6.6.1] QML warning "Final member modelData  
is overridden in class QQmlDMAbstractItemModelData. The override won't  
be used."  
* QTBUG-122106 QList<int> is converted to int by qmlsc  
* QTBUG-120105 Unreliable QML Timer / qmltest wait() / QTest:qWait()  
with offscreen platform  
* QTBUG-118889 Assert when changing focus fast of  
qquickmaterialplaceholdertext  
* QTBUG-120506 [Reg 6.5 -> 6.6] Using `CameraLens.ProjectionType` as  
type hinting cause runtime error  
* QTBUG-122252 [REG: 6.4->6.5] Qt.point cannot be used as a return type  
* QTBUG-121349 Flickable: strange defaults for mouse wheel triggered  
boundsMovement  
* QTBUG-119829 [Reg 6.5 -> 6.6] Shadowing default property crashes QML  
* QTBUG-121592 Attached ScrollBar and ScrollIndicator fail when using  
QML Type Compiler  
* QTBUG-119448 Fix documentation: initializing a property of aliased  
property won't actually cause an error  
* QTBUG-118982 qmllint multiple pragma ComponentBehavior in same file  
* QTBUG-120526 qmllint complains wrongly when changing Layout attached  
properties in a PropertyChanges  
* QTBUG-116994 qt_add_add_qml_module runs into command line length  
limits on Windows  
* QTBUG-119911 Incubated object is garbage collected before a reference  
to it can be created  
* QTBUG-113039 Crash when accessing properties of line parameter in  
Text.onLineLaidOut  
* QTBUG-122024 Advertised and documented property of Layouts does not  
work.  
* QTBUG-116505 HoverHandler is broken when using a stylus  
* QTBUG-101932 two HoverHandlers with different  
acceptedDevices/acceptedPointerTypes: cursorShape doesn't change  
accordingly  
* QTBUG-122454 Gallery example radio buttons not working as expected  
* QTBUG-115478 Qmllint interferes with qmldir file in source directory  
if present  
* QTBUG-115439 Qmllint throws warnings at TapHandler's signals  
* QTBUG-109488 tst_qquicktextedit::largeTextObservesViewport fails / is  
flaky  
* QTBUG-122707 [Reg 5.15 -> 6.4] Binding QML type does not restore  
original value in some cases  
* QTBUG-109708 Startup crash in QRhiD3D11::endFrame() with nullptr  
access  
* QTBUG-101200 Qt crash/freeze when doing a graphics driver update on  
Windows  
* QTBUG-122790 Child window is not closed upon closing the main window  
in Qt Quick Widgets Example  
* QTBUG-122686 Crash when processing hover events modifies object tree  
* QTBUG-118804 The link is looping for Qt Quick Effect Maker  
* QTBUG-122251 qmltc crashes with Qt.point as a return type  
* QTBUG-120433 AnimationController segfaults on exit  
* QTBUG-113384 QQuickWidget - touchpad click not working after scrolling  
* QTBUG-91272 [Regression]On Mouse Area press, deleting other  
overlapping mouse area crashes the Application  
* QTBUG-122915 [REG 6.6.1-6.6.2] Overlay remains visible when a Popup is  
destroyed via Loader  
* QTBUG-120149 Material 3 - TextField placeholder issues when padding  
changed  
* QTBUG-113532 Animate RadioButton in the Material style  
* QTBUG-122894 Crash when QQuickView loads QML document that binds  
Overlay.overlay.[property]  
* QTBUG-117923 ItemParticle causes constant CPU usage and rerenders  
* QTBUG-123428 [REG 6.6 → 6.7 ]Using QML_DISABLE_DISK_CACHE breaks QML  
code  
* QTBUG-120356 padding not applied to header and footer for  
QuickControls.Dialog  
* QTBUG-117654 TextArea multi-line placeholder text overlaps the  
TextEdit area  
* QTBUG-121643 qt6-declarative: possible build-time race condition  
around qmlcachegen  
* QTBUG-122256 Crash on  
QQuickMultiEffectPrivate::updateBlurItemsAmount() with nullptr access  
* QTBUG-62111 Docs: Fixed day/year format in QDateTime  
* QTBUG-122405 tst_qquickhoverhandler::window is flaky on OpenSuse  
* QTBUG-63363 QPointingDevices for the trackpad and mouse are  
dynamically instantiated on macOS  
* QTBUG-112432 wayland plugin should distinguish touchpads from mice,  
etc.  
* QTBUG-122679 tst_how-to-qml timePicker is flaky  
* QTBUG-78846 tst_qquicktextedit::mouseSelectionMode is flaky on  
OpenSuse 15  
* QTBUG-74342 QML RichText hr element doesn't work  
* QTBUG-120067 Material 3 - Controls height issues  
* QTBUG-115438 [REG: 5->6] MouseArea onEnter triggers before onExit on  
the previous item  
* QTBUG-123160 crash in qquickspinbox  
  
### qtmultimedia  
* QTBUG-121455 QtMultimedia module fails Yocto CI build  
* QTBUG-121200 QML Video Recorder - Missing Text in Buttons on Android  
* QTBUG-121495 COM is uninitialized too many times with FFmpeg and  
QWindowsResampler  
* QTBUG-121187  Spectrum App Crashes after recording sound in "Record  
and Playback" Mode  
* QTBUG-119737 MediaRecorder.isAvailable not defined  
* QTBUG-120465 QML Camera unloading crash on iOS  
* QTBUG-119746 Audio recording volume extremely low  
* QTBUG-114900 alsa backend causes warning messages  
* QTBUG-122053 Qt continues to occupy the microphone unless you call  
QMediaCaptureSession::setAudioInput() with a null pointer after  
recording is complete  
* QTBUG-122045 [MediaPlayerExample] The timeline is not reset when the  
loop mode for single file is turned on  
* QTBUG-120026 Retrieving videoDevices blocks main event loop  
* QTBUG-120198 Process abruptly terminates while executing static  
destructor in Qt6Multimedia.dll  
* QTBUG-122096 Wrong colors are displayed when playing videos with IMC2  
color format  
* QTBUG-116519 [Reg 6.2 -> 6.5] Repeated QSoundEffect is broken on  
PulseAudio  
* QTBUG-113317 QVideoWidget rendering video incorrectly on macOS  
Monterey  
* QTBUG-122640 QtMultimedia plugins are not deployed to Android .apks  
* QTBUG-121714 Camera preview stops working when recording on Android-  
backend  
* QTBUG-121943 QPlatformMediaDevices is accessed before main on Android  
* QTBUG-121221  Camera Example - Recording Denied with "Invalid  
Argument" Error  
* QTBUG-122750 [Regression] QSoundEffect cuts audio with FFmpeg backend  
* QTBUG-122706 onBufferProgressChanged not emited at all  
* QTBUG-121678 eglfs: Capturing the screen crashes on a Qt Quick  
application  
* QTBUG-122753 Qt Multimedia: implicit instantiation of undefined  
template 'std::char_traits<unsigned char>' (libc++ 19 / musl libc /  
amd64)  
* QTBUG-122193 QSoundEffect hangs on Loading  
* QTBUG-121182 QML Video Example: Simultaneous videos playback crashes  
the App on Android  
* QTBUG-122649  Playing multiple videos simultaneously fails for the  
second video with the FFMPEG backend on Android.  
* QTBUG-122608 [REG 6.6.1-6.6.2] [windows] QMediaPlayer failed to set  
topology on custom QVideoSink  
* QTBUG-122817 [REG 6.6.1-6.6.2] [windows] QML MediaPlayer unable to  
play a video when 'audioOutput' is not specified  
* QTBUG-122199 [ffmpeg] player crash in libavcodec if libnvidia-decode  
is not installed  
* QTBUG-122638 [gstreamer] deadlock when switching camera  
* QTBUG-98437 QMediaPlayer does not emit destroyed signal  
* QTBUG-122959 GStreamer: "stop camera" does not stop camera  
* QTBUG-118099 Volume Discrepancies Between QMediaPlayer and  
QSoundEffect with ffmpeg  
* QTBUG-121750 QCameraImageProcessing fails to set settings on linux  
v4l2 camera  
* QTBUG-122577 QScreenCapture tests are flaky on OpenSuse 15.5  
* QTBUG-108754 Video not stretched properly  
* QTBUG-116324 Request to implement thumbnail realization for multimedia  
FFMPEG backend  
* QTBUG-111190 V4L2m2m encoder gets failed on linux  
* QTBUG-122224 [Crash] The audiorecorder example crashes when selecting  
output and start recording  
* QTBUG-87969 MediaPlayer looses current position when playbackRate  
changes  
  
### qttools  
* QTBUG-118808 qt_add_translations with source autodetection mishandles  
id-based generated UI headers  
* QTBUG-121850 QDoc: SHA1-files generated for QHP files differ across  
platforms  
* QTBUG-118558 QDoc: DocParser::getRestOfLine no longer strips trailing  
backslashes and whitespace properly  
* QTBUG-120531 lupdate doesn't understand template literals  
* QTBUG-121906 Copyright year in so files not updated to 2024  
  
### qtdoc  
* QTBUG-120230 'coffee' fails when cross-compiling on Windows  
* QTBUG-121044 Calqlatr example not scaling properly in landscape mode  
* QTBUG-121524 [REG 6.6.1 -> 6.6.2] StocQt CMake error for Android  
* QTBUG-121660 Calqlatr example missing naming for Android package  
* QTBUG-119285 MediaPlayerApp-Desktop-Example Scrolling issues when  
using the mousewheel  
* QTBUG-121578 demos/hangman fails to build on Android and macOS  
* QTBUG-120643 [REG 6.2.4 -> 6.5.3] "Classes" page is empty  
* QTBUG-122258 [REG 6.6.1->6.7.0] demos/stocqt not compiling  
* QTBUG-122178 [Media Player Example] App hangs when previous track is  
clicked  
* QTBUG-122767 QTP0001 warning for FX & Material Showroom example  
  
### qtlocation  
* QTBUG-121412 Make sure that QtLocation examples use new QPermissions  
API  
  
### qtwayland  
* QTBUG-116600 The Virtual keyboard is not hidden when the TextField  
loses focus on the Wayland client.  
* QTBUG-122965 Qt 6.5.4 don't generate XDG_RUNTIME_DIR  
* QTBUG-95817 Quick windows break  on nvidia wayland when resized  
  
### qt3d  
* QTBUG-111427 Race condition in UniformBlockValueBuilder  
* QTBUG-122613 QPaintedTextureImage in a Texture2D crashes with size  
256x256  
  
### qtserialport  
* QTBUG-120412 Blocking receiver example - Will crash when clicking  
'start' if no Serial port is selected  
  
### qtwebengine  
* QTBUG-120218 QML WebEngineView.printToPdf(): paper formats are wrong  
in the resulting document  
* QTBUG-115502 PdfMultiPageView: repeated pinch-zooming jumps to wrong  
zoom level  
* QTBUG-121564 tst_MultiPageView::pinchDragPinch is flaky  
* QTBUG-120245 A crash occurred in C:\Users\qt\work\qt\qtwebengine_stand  
alone_tests\tests\auto\pdfquick\multipageview\tst_multipageview.exe  
* QTBUG-121502 crash in QPdfIOHandler if document is deleted too early  
* QTBUG-119416 Loading a specific page in a PDF document does not always  
show the correct page  
* QTBUG-120273 QWebEngineView shows blank content on initial show when  
page bg set to transparent  
* QTBUG-121227 QWebEngineView shows blank content on initial show when  
page bg set to transparent  
* QTBUG-112013 QWebEnginePage.setBackground(Qt::black) doesn't work for  
page loading.  
* QTBUG-120926 QWebEnginePage::setBackgroundColor doesn't work properly  
* QTBUG-122153 QWebEngineView::setFocus() doesn't give focus to the view  
after calling QWebEngineView::load() for the second time  
* QTBUG-122137 REG: QtWebEngine / Pdfwidgets no longer supports plugins  
* QTBUG-121589 Can't build qt6 due to failed ozone platform assertion  
* QTBUG-118035 QtWebengine build fails on pure wayland  
* QTBUG-122997 The Spellcheck example doesn't work on macOS  
* QTBUG-86948 When using QImageReader to load a PDF then the PDF images  
can be blurry and seem to be at half the size they should be  
* QTBUG-120764 PDF Viewer Widget example search error  
* QTCREATORBUG-30308 QtCreator is not able to debug pdb files when lib  
linked with pdbpagesize  
* QTBUG-120420 QtWebEngine inspector crashes  
  
### qtwebview  
* QTBUG-112346 qmllint fails when WebView is used  
  
### qtvirtualkeyboard  
* QTBUG-121658 Virtual keyboard example crashes after startup on Android  
* QTBUG-121643 qt6-declarative: possible build-time race condition  
around qmlcachegen  
  
### qtscxml  
* QTBUG-120578 The date type of "event" in occurred should be specified  
  
### qtspeech  
* QTBUG-122950  FAIL!  :  
tst_qtexttospeech_qml::Voice::test_default_voice() Compared values are  
not the same  
* QTBUG-122884 QML TextToSpeech enqueue does not work with Darwin engine  
* QTBUG-122900 Android App dies immediately if I add TextToSpeech to the  
project  
  
### qtquick3d  
* QTBUG-120424 Segmentation fault in the process of loading/unloading 3D  
objects  
* QTBUG-121390 Live Preview with a 3D project crashes on with Qt 6.6.1  
* QDS-11396 Node QML type from QtQuick3D is not available in Components  
* QTBUG-122143 balsam ktx build error with ASAN build  
* QTBUG-108755 [REGRESSION] number of drawcalls don't show up in QML  
profiler  
* QTBUG-123015 When configuring with -no-qml-debug then it will fail to  
build QtQuick3D  
* QTBUG-120109 WasdController: Models stutter in Qt Quick 3D Physics  
example  
  
### qtopcua  
* QTBUG-120911 Qt OPC UA landing page misses license information  
* QTBUG-122277 QtOpcUa does not compile using VS2022 17.9.0 on "subst"  
drive  
  
### qthttpserver  
* QTBUG-120746 QWebSocket immediately disconnects after without  
receiving anything  
  
### qtquick3dphysics  
* QTBUG-121033 onBodyContact being called after object is deleted  
  
### qtgrpc  
* QTBUG-121429 qtprotobuf.html:  Clash between C++ namespace and group  
documentation  
* QTBUG-121544 qtprotobufgen generates the corrupted  
protobufwellknowntypes_exports.qpb.h  
* QTBUG-121585 wrong license filename in LICENSES folder ?  
* QTBUG-122700 qt_add_protobuf doesn't set neither OUTPUT_HEADERS nor  
OUTPUT_TARGETS  
* QTBUG-121813 qt_attribution.json issues  
  
### qtgraphs  
* QTBUG-121372 Theme3D::baseColors is written as Theme3D::baseColor in  
the document  
* QTBUG-121998 Q3DSurface/Q3DBars opens up as white screen by default  
* QTBUG-119674 Surface Graph Gallery example crashes  
  
### qtapplicationmanager (Commercial only)  
* QTBUG-122425 AppMan: Documented logging category for QML logging is  
incorrect  
* QTBUG-122721 [AppMan] Discrepancies in documented types of Application  
+ Package Categories  
* QTBUG-117010 [Boot2Qt] Cannot run any application that uses Qt  
Application Manager  
* QTBUG-123088  Qt Application Manager examples fail to scan  
  
### qtinterfaceframework (Commercial only)  
* QTBUG-121575 Interface files are generated in configuration time, not  
compilation time  
* QTBUG-121696 This page about QtIf is only talking about qmake, not  
cmake  
* QTBUG-121740 The page about Jinja Template Syntax has its link  
malformed  
* QTBUG-121778 QIfAbstractFeature::connectToServiceObject()'s code  
snippet is ill-formed  
* QTBUG-122036 ModuleNotFoundError: No module named 'dataclasses'  
* QTBUG-121800 IfSimulator QML type's doc doesn't specify the return  
types of methods  
  
### qmlcompilerplus (Commercial only)  
* QTBUG-122726 Dependency update on qt/tqtc-qmlcompilerplus is failing  
  
Known Issues  
------------  
  
* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-6.6/supported-platforms.html  
* RTA reported issues from Qt 6.6  
https://bugreports.qt.io/issues/?filter=25128  
* See Qt 6.6  known issues from:  
https://wiki.qt.io/Qt_6.6_Known_Issues  
* Qt 6.6.3 Open issues in Jira:  
https://bugreports.qt.io/issues/?filter=25766
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Laszlo Agocs  
Dilek Akcay  
Konsta Alajärvi  
Anu Aliyas  
Dimitrios Apostolou  
Viktor Arvidsson  
Vladimir Belyavsky  
Nicholas Bennett  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
Tatiana Borisova  
Joerg Bornemann  
Assam Boudjelthia  
Aurélien Brooke  
Kai Uwe Broulik  
Michael Brüning  
Olivier De Cannière  
Kaloyan Chehlarski  
Ed Cooke  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Szabolcs David  
Noah Davis  
Oliver Dawes  
Artem Dyomin  
Alexey Edelev  
David Edmundson  
Oliver Eftevaag  
Christian Ehrlicher  
Hatem ElKharashy  
Andreas Eliasson  
David Faure  
Nicolas Fella  
Simo Fält  
Joshua Goins  
Robert Griebl  
Mikko Gronoff  
Kaj Grönholm  
Richard Moe Gustavsen  
Lucie Gérard  
Mikko Hallamaa  
Jøger Hansegård  
Inkamari Harjula  
Jani Heikkinen  
Tero Heikkinen  
Miikka Heikkinen  
Moss Heim  
Jari Helaakoski  
Ulf Hermann  
Volker Hilsheimer  
Dominik Holland  
Alexander Hulander  
Allan Sandfeld Jensen  
Tim Jenssen  
Jonas Karlsson  
Kevin Keating  
Timothée Keller  
Friedemann Kleint  
André Klitzing  
Michal Klocek  
Jarek Kobus  
Tomi Korpipaa  
Tomi Korpipää  
Fabian Kosmale  
Volker Krause  
Santhosh Kumar  
Ghenady Kuznetsov  
Kai Köhne  
Lauri Laanmets  
Inho Lee  
Paul Lemire  
Chris Lerner  
Thorbjørn Lindeijer  
Thiago Macieira  
Ievgenii Meshcheriakov  
Safiyyah Moosa  
Bartlomiej Moskal  
Marc Mutz  
Antti Määttä  
Antonio Napolitano  
Andy Nichols  
Mårten Nordheim  
Dennis Oberst  
Samuli Piippo  
Timur Pocheptsov  
Joni Poikelin  
Aleix Pol  
Lorn Potter  
Sakaria Pouke  
MohammadHossein Qanbari  
Liang Qi  
Matthias Rauter  
David Redondo  
Topi Reinio  
Shawn Rutledge  
Ahmad Samir  
Philip Schuchardt  
Sami Shalayel  
Orgad Shaneh  
Andy Shaw  
Ivan Solovev  
Axel Spoerl  
Frank Su  
Tarja Sundqvist  
Lars Sutterud  
Tasuku Suzuki  
Jan Arve Sæther  
Morten Sørvig  
Sadegh Taghavi  
Paul Olav Tvete  
Peter Varga  
Doris Verria  
Tor Arne Vestbø  
Jannis Voelker  
Juha Vuolle  
Olli Vuolteenaho  
Jaishree Vyas  
Michael Weghorn  
Edward Welbourne  
Paul Wicking  
Piotr Wierciński  
Semih Yavuz  
Vlad Zahorodnii  
Yansheng Zhu  
Yifan Zhu  
