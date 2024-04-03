Release note  
============  
Qt 6.2.8 release is a patch release made on the top of Qt 6.2.7. As a patch  
release, Qt 6.2.8 does not add any new functionality but provides bug fixes  
and other improvements.  
  
For detailed information about Qt, see the Qt 6.2 online documentation:  
https://doc.qt.io/qt-6.2/.  
  
Important Changes  
-----------------  
  
### qtbase  
* 45709222b4 Update bundled libpng to version 1.6.39  
libpng was updated to version 1.6.39  
  
* 549e2a0bd4 CMake: Make it possible to specify a debug MySQL client  
library  
If pkg-config is not used, a debug build of the MySQL client library  
can be specified with -DMySQL_LIBRARY_DEBUG=<path-to-library>. The debug  
and release variants of the library are automatically detected. Setting  
MySQL_ROOT and MySQL_LIBRARY_DIR is sufficient in most cases.  
  
* 15045fa8a9 windows: Fix vertical metrics with GDI engine  
Fixed an issue where the line gap of some fonts would be included twice  
in the font's leading.  
  
* 3310946227 SQLite: Update SQLite to v3.40.0  
Updated SQLite to v3.40.0  
  
* 4e647ab8a6 QNetworkRequest: Make header parsing locale-independent  
Fixed a bug where certain QNetworkRequest::KnownHeaders wouldn't be  
recognized as such in certain locales.  
  
* 2d7753a723 QTest::WatchDog: fix missing timeout resets on test  
function change  
Fixed a bug which caused QTEST_FUNCTION_TIMEOUT to be applied to the  
whole test execution, as opposed to each test function.  
  
* b5164f0fdf SQLite: Update SQLite to v3.40.1  
Updated SQLite to v3.40.1  
  
* 14b6eb6e7d Move QTypeInfo<std::pair> from qpair.h to qtypeinfo.h to  
avoid ODR violation  
The QTypeInfo for std::pair/QPair will now be correct even if qpair.h  
hasn't been included, fixing an One-Definition-Rule (ODR) violation.  
  
* 5ed684e79e QStringConverter: use the QUtf8 codec when Windows is using  
UTF-8  
Fixed support for using Qt applications with UTF-8 as the system  
codepage or by enabling that in the application's manifest.  
  
* 4768b58f09 Update bundled libjpeg-turbo to version 2.1.5  
libjpeg-turbo was updated to version 2.1.5  
  
* c581474dfb QVarLengthArray: clear() is not resize(0)  
clear() no longer requires the value_type to be default-constructible.  
  
* 16407d12e7 Text: fix Soft hyphen rendering in QTextLayout::glyphRuns()  
Fixed an issue where spaces would sometimes be shown in soft hyphen  
positions in a string.  
  
* 5d208fc91b qstrncpy: NUL-terminate even when src is nullptr  
Now NUL-terminates the target buffer even when the source pointer is  
nullptr, provided the target buffer has space for at least one byte.  
  
* d98e9d29ed CMake: Fix position independent code linker flags not being  
set  
Qt tools are now built with position independent code even with Unix  
toolchains where this is not the default, for example clang.  
  
* dfa04903c6 SQLite: Update SQLite to v3.41.0  
Updated SQLite to v3.41.0  
  
* 82dacd839b QFSFileEngine: fix overflow bug when using lseek64  
Fixed a bug where opening a file in append mode may fail if the file  
size was bigger than INT_MAX.  
  
* 34765aae27 SQLite: Update SQLite to v3.41.1  
Updated SQLite to v3.41.1  
  
### qtdeclarative  
* 361d4bdf54 QQuickNinePatchImage: fix aliasing by respecting the smooth  
property  
The Imagine style now supports smooth scaling for 9-patch images when  
the QT_QUICK_CONTROLS_IMAGINE_SMOOTH environment variable is set to 1.  
  
* 413b4d1dc1 Fix missing glyphs when using NativeRendering  
Fixed an issue where text using NativeRendering would sometimes be  
missing glyphs.  
  
* d015bb83ea QtQml: Fix coercion of undefined to float and double  
Converting a JavaScript value to a double or float now always assumes  
JavaScript type coercion semantics. In particular, converting a value  
that is not actually a number now results in NaN where it previously  
sometimes resulted in 0.  
  
### qtconnectivity  
* 934e804b SDP scanner: encode input URLs and escape XML-specific  
characters  
sdpscanner now %-encodes the URLs and escapes all XML-specific  
characters in them before adding the result to the generated XML output.  
  
### qtwayland  
* 537e9c08 client: Fix infinite recursion with text-input-v2  
Fixed a possible crash when editing a field in an item view.  
  
### qtimageformats  
* a32cc0e TGA Plugin: Fix reading of CMapDepth  
Fixed reading of TGA files with a non-zero X-origin  
  
* 73fab89 Update bundled libwebp to version 1.3.0  
Update bundled libwebp to version 1.3.0  
  
* 76b060b Update bundled libtiff to version 4.5.0  
Bundled libtiff was updated to version 4.5.0  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-106025 REG: isSignalConnected creates a dead lock.  
* QTBUG-106000 tst_QLocale::fpExceptions() triggers assertion failure on  
Windows  
* QTBUG-107675 Typo in the document?  
* QTBUG-108662 Can't build for Android  
* QTBUG-105046 Linker failures when building with  
-DFEATURE_openssl_linked=ON  
* QTBUG-101680 MySQL plugin: QSqlQuery::prepare + exec no results when  
table contains JSON type  
* QTBUG-108815 Installing qtdeclarative fails  
* QTBUG-109060 QAction() handling of text does not seem correctly  
documented  
* QTBUG-109061 QAction and ampersands in text  
* QTBUG-108300 Crash when setPersistentGraphics(false),  
setPersistentSceneGraph(false) and visible: true on wayland  
* QTBUG-108194 FAIL!  : data::tst_simulation-behavior::compile() module  
"Simu" is not installed  
* QTBUG-109240 file INSTALL cannot find "/home/qt/work/qt/qtremoteobject  
s_build/mkspecs/modules/qt_lib_repparser_private.pri":  
* QTBUG-109239 file INSTALL cannot find "/home/qt/work/qt/qttools_build/  
mkspecs/modules/qt_lib_linguist_private.pri"  
* QTBUG-109169 Invalid QColorTrcLut use causes unreadable text with  
16-bit X11 visuals  
* QTBUG-108641 system tray icons in Windows 10 goes blurry  
* QTBUG-107627 AndroidAssetsFileEngineHandler is broken  
* QTBUG-107662 Android keyboard doesn't close when clicking on done  
* QTBUG-109400 Windows: Font Line spacing differs between Qt 5 and 6  
* QTBUG-108848 iOS: Voice Control Accessibility feature breaks in iOS 16  
* QTBUG-99601 ios: QMAKE_PRE_LINK Gives Error :Multiple commands produce  
* QTBUG-106701 Crash with any QML app on external display with iPadOS  
16.1 on M1 iPad  
* QTBUG-109466 QTEST_FUNCTION_TIMEOUT applies to the whole test, not per  
function  
* QTBUG-108365 [REG 6.4.0 -> 6.5] Low contrast status bar in Android  
applications  
* QTBUG-104776 AndroidContentFileEngineIterator hangs when listing  
shared content with nested dirs  
* QTBUG-63700 QSharedPointer missing documentation for move operators  
* QTBUG-109026 Android: UI is scaled smaller than before  
* QTBUG-109212 QLabel with embedded image using 'qrc:/' will no longer  
load  
* QTBUG-109453 GDI fallback surface format for Win 11 (21H2)  
* QTBUG-109586 QAndroidApplication::runOnAndroidMainThread() UB when  
timeout is set  
* QTBUG-106531 QDockWidget Docking resizes (widens) the widget by a set  
number of pixels  
* QTBUG-107026 http://matek.hu/xaos/doku.php is dead  
* QTBUG-103393 IBus input method cannot set panel position correctly  
with DPI scaling  
* QTBUG-109226 Rare crashes in QXcbBackingStoreImage::flushPixmap  
* QTBUG-109477 QImageReader will cause heap corruption when load jpeg  
(width: 1px height:100px) on Apple M1  
* QTBUG-106653 Crash on Accessibility interface  
* QTBUG-108790 Crash on QFuture::cancel() with continuation and thread  
context  
* QTBUG-110068 qmake: Generated Visual Studio project defaults  
"GenerateDebugInformation" to "false"  
* QTBUG-84315 QUrl::setAuthority() behavior changes  
* QTBUG-88652 QTEST_FUNCTION_TIMEOUT and test function limit (5 minutes)  
are not documented.  
* QTBUG-64132 QToolButton should elide text when width constraints  
prevent from showing whole text  
* QTBUG-109610 developer-build fails for xcb  
* QTBUG-109838 QFontMetricsF::horizontalAdvance seems to do unnecessary  
scanning  
* QTBUG-103611 [Reg 5.15 -> 6.x] Re-initializing QGuiApplication causes  
QQmlApplicationEngine to crash  
* QTBUG-110058 QCryptographicHash is not re-entrant  
* QTBUG-56595 QXcbConnection::getTimestamp() returns old timestamp  
* QTBUG-105857 Qt application does not follow the DPI change when the  
DPI setting is changed before showing the first window  
* QTBUG-110627 Qt doesn't really follow Windows short time format  
* QTBUG-109518 QPdfWriter loses some of the content if it is positioned  
right  
* QTBUG-110271 Copyright year not updated to 2023 on documentation  
* QTBUG-108822 QDBus: unable to connect the InterfacesAdded signal of  
org.freedesktop.DBus.ObjectManager on the system bus (unless using  
QDBUS_DEBUG)  
* QTBUG-110785 QFbCursor memory leak  
* QTBUG-110595 [REG 5.15 -> 6.x] QSvgRenderer::render(QPainter*) is now  
~100x slower  
* QTBUG-105870 QListItemView with SingleSelection unselects item when  
clicking on empty area  
* QTBUG-109832 QMYSQL plugin no longer works with older supported  
versions of MySQL/MariaDB  
* QTBUG-106718 [REG] QCoreApplication::processEvents() processes  
deferred delete  
* QTBUG-106569 Ctrl-C in QTreeView passes invalid QModelIndex to model  
when model is empty  
* QTBUG-109230 Crash in QFuture  
* QTBUG-107770 no member named 'init' in 'QStyleOption'  
* QTBUG-111131 setDragEnabled() is breaking interactive item selection  
in QTreeView  
* QTBUG-102010 QScroller prevents QAbstractItemView::DoubleClicked edit  
trigger  
* QTBUG-46990 Soft hyphen rendered as space  
* QTBUG-62620 [QtQuick, TextEdit] Soft hypen and incorrectly drawn  
selection  
* QTBUG-67038 Soft hyphens are broken  
* QTBUG-102483 Soft hyphen rendered as space on macOS  
* QTBUG-111275 Inserting a QDate into an Oracle DB with a prepared  
statements fails for timezones like CET  
* QTBUG-111170 mouseMoveEvent fired without mouse being really moved  
(Mac only)  
* QTBUG-63381 Transient scrollbars do not work when using style sheets  
* QTBUG-111149 Reg->6.4.2: Windows: Qt Designer freezes when dragging  
actions in QMenu  
* QTBUG-110497 Qt's CMake Config files reset CMAKE_AUTOMOC_MACRO_NAMES  
* QTBUG-111416 [REG 6.3.2->6.4.2] Repeated QPainter::drawPixmapFragments  
calls draw images at wrong positions for QOpenGLWidget  
* QTBUG-108013 QStandardPaths::PicturesLocation paths on Android  
* QTBUG-104892 QStandardPaths::DocumentsLocation on emulated android  
device returning the same directory twice  
* QTBUG-81860 Android: Add "content:" scheme paths to QStandardPaths  
* QTBUG-109958 tst_qalgorithms should not create unique datatags when  
testing  
* QTBUG-111443 macOS/iOS: "Detected system locale encoding (US-ASCII,  
locale "C") is not UTF-8"  
* QTBUG-102107 [REG 5.15.2 => 6.2.3] QMenuBar can crash on Mac  
* QTBUG-106369 Crash when closing modal window with macOS on-screen  
keyboard  
* QTBUG-111183 Qt crash on macOS when using keyboard viewer  
* QTBUG-105250 Access NULL m_platformWindow in qnsview_complextext.mm  
* QTBUG-111397 QNetworkAccessManager hangs indefinitely when loading a  
corrupted cache file  
* QTBUG-108050 Depth Buffer not working in 5.15.2  
* QTBUG-85544 androiddeployqt fails with message that neither  
libqtforandroid.so or libqtforandroidGL.so are included  
* QTBUG-97636 Qtbase for Android with examples fails to build  
* QTBUG-83997 Can't deploy a simple console application  
* QTBUG-93185 Android platform plugin not linked when using only QtCore  
* QTBUG-68884 Missing isNull check in QOpenGLTexture (crash in driver)  
* QTBUG-112174 QDebug operator<<(QDebug debug, const QInputDevice  
*device) crashes if device is null  
* QTBUG-109971 Crash during window resize when using QQuickWidget  
* QTBUG-104905 Window modal not blocking ancestor window interaction on  
Mac  
* QTBUG-106099 QCombobox dropdown not displayed on correct monitor in  
multimonitor setup  
* QTBUG-104781 Tooltip Example: Wrong object is moved when performing  
dragging on another one  
* QTBUG-74478 mouse flicking on qtabwidget non-current tab causes  
segfault  
* QTBUG-106906 tst_qtcuncurrentrun::pollForIsFinished occasionally  
crashes  
* QTBUG-109135 Qt warning "Failed to create SecCertificate from  
QSslCertificate"  
* QTBUG-109235 Review toupper/tolower uses [Qt]  
* QTBUG-105736 tst_qfile unixPipe and socketPair tests fail on Android  
12  
* PYSIDE-2182 QTimer.singleShot example documentation does not work  
* QTBUG-105804 The qt_ntfs_permission_lookup mechanism is prone to data  
races  
* QTBUG-110703 tst_QFocusEvent::checkReason_ActiveWindow() fails on  
macOS 13.2  
* QTBUG-107604 [Reg 5.15.10 -> 5.15.11] Incorrect fullscreen dimensions  
on some Android devices  
* QTBUG-109268 QWindow on Android doesn't use full area on some devices.  
* QTBUG-97503 Reg[5.15.2-5.15.6] Android: Keyboard covers the inputfield  
* QTBUG-107923 Wrong height of the window on Android  
* QTBUG-109351 Bottom Navigation Bar overlaps app window  
* QTBUG-110501 Wrong calculation of display area on android when virtual  
keyboard is present before opening the app  
* QTBUG-102474 Sometime SSL leads to hang application on exit  
* QTBUG-103514 Possible crash in imagescaling example.  
* QTBUG-105140 [REG] default constuctor requirement for meta type  
(QVariant) breaks webengine api  
* QTBUG-111598 Implement get/get_if for QVariant to make it nicer for  
non-default constructible types  
* QTBUG-105958 [Android] Intent + Talkback leads to deadlock  
* QTBUG-111625 COM library crash exposed when using TBB scalable memory  
allocation  
* QTBUG-25365 ValueChanged() signal is not emitted by QScrollBar when  
Page Up/Dn is Hit in  QPlainTextEdit having scrollbar  
  
### qtdeclarative  
* QTBUG-108697 Program can crash when Connections target is destroyed  
* QTBUG-109002 [PinchHandler] Dragging a target is not functional  
* QTBUG-109010 top-level build: automoc broken yet again in 6.4 branch  
(depending on moc before it's built)  
* QTBUG-109200 Shape with QT_QUICK_BACKEND=software crashes sometimes  
* QTBUG-108831 Some Rectangle borders are double the width with  
fractional scale ratios  
* QTBUG-107989 Aliasing occurs at the image boundary if add Scale  
Animator to nine-patch image  
* QTBUG-107492 Typo in the document  
* QTBUG-108994 qml: signal handler crash on wrong arguments  
* QTBUG-105312 REG: SplitView no longer works with touch  
* QTBUG-86744 ListView.isCurrentItem not available until model is  
refreshed  
* QTBUG-103811 Drawer: Different behavior with mouse & touch input  
* QTBUG-109140 [REG: 5->6] Slowly dragging Tumbler causes numbers to  
jump around  
* QTBUG-108713 Native font rendering in some cases misses letters  
* QTBUG-105148 Rotated qml combobox popup placed incorrectly  
* QTBUG-109417 binding to alias crashes qml  
* QTBUG-101736 QQuickWidget: button in a popup doesn't receive touch end  
event  
* QTBUG-109597 Seg fault in QQmlObjectCreator::finalize when creating  
QML object with initial bindings  
* QTBUG-108610 HorizontalHeaderView & VerticalHeaderView does not  
disconnect from QQmlTableModel::headerDataChanged and can crash app  
* QTBUG-109854 [REG 6.2.4 -> 6.2.5] QQuickImageProvider doesn't scale  
properly if Image size is not set on High DPI displays  
* QTBUG-90480 Not all overloads of Qt.matrix4x4 are listed  
* QTBUG-109882 ShapePath: Switching from a transparent colour to a non-  
transparent one causes the wrong colour to be displayed  
* QTBUG-95448 Re-add QQmlExtensionPlugin documentation  
* QTBUG-107797 linux: File selectors cannot be used  
* QTBUG-108664 TableView positions incorrectly  
* QTBUG-110321 qmlformat runs into an issue with ES classes  
* QTBUG-96700 Strikethrough formatting changes to underline.  
* QTBUG-97594 Mac - Strikeout bugged in QML TextEdit for Japanese  
* QTBUG-91390 ListModel doesn't keep objects of JavaScriptOwnership  
alive  
* QTBUG-95895 REG 5.15 -> 6.2: destroy() does not destroy objects after  
appending listModel.  
* QTBUG-96167 Ownership of C++ owned object flips when added to  
ListModel  
* QTBUG-106074 Add and explain naming conventions and restrictions for  
files in QML  
* QTBUG-75954 Flipable draws incorrectly when rotated and the angle is  
45°  
* QTBUG-110111 [Reg 6.3.2 -> 6.4.x] DropShadow: Changing radius to 0 at  
runtime causes a crash when attached to Canvas  
* QTBUG-111078 ExecutableCompilationUnit::saveToDisk() does not  
invalidate the cache it uses for loadFromDisk()  
* QTBUG-107902 "Defining QML Types from C++" lacks CMake documentation  
* QTBUG-111179 Incorrect coercion to number for undefined  
* QTBUG-109816 Crash when accessing enums defined in QML_SINGLETON class  
* QTBUG-111566 Docs: Faulty sample code in the documentation of  
SwipeDelegate QML Type  
* QTBUG-111559 Loader with States creates 2 children instead of 1  
* QTBUG-104761 acceptedButtons in DragHandler is apparently ignored  
* QTBUG-74020 PointHandler documentation examples refer to TapHandler  
not PointHandler  
* QTBUG-106878 PointHandler documentation examples refer to TapHandler  
not PointHandler  
* QTBUG-111935 Qt V4 JIT engine generates bad JIT code on ARM64 (and  
potentially all arches)  
* QTBUG-95807 QtQuick: Missing headers or documentation bug  
* QTBUG-111986 qmlsc generates invalid code  
* QTBUG-108150 Adding qml files from the build folder to the QRC is  
creating filenames so long it breaks the build on Windows host  
* QTBUG-107707 tst_qquickimageparticle fails with Ubuntu 22.04  
* PYSIDE-1345 vertexDataAsPoint2D() in QSGGeometry returns only one  
point  
* QTBUG-109235 Review toupper/tolower uses [Qt]  
* QTBUG-110933 qmlsc mistakes Enum for Property  
* QTBUG-95395 Code snippets for HoverHandler show TapHandler  
* QTBUG-41043 tst_qquickcanvasitem tends to fail on CI  
* QTBUG-70397 TapHandler fires for all overlapping items  
* QTBUG-73262 it's confusing that TapHandler.gesturePolicy affects event  
propagation  
* QTBUG-100534 TapHandler doesn't stop propagation  
* QTBUG-107239 DragHandler propagates tap event through Flickable to  
underlying TapHandler  
* QTBUG-111310 \image tag breaks \value block  
  
### qtactiveqt  
* QTBUG-109235 Review toupper/tolower uses [Qt]  
  
### qtmultimedia  
* QTBUG-109070 [DOCS] QCameraDevice docs refers to missing orientation()  
* QTBUG-108668 QAudioDevice shows incorrect (old Qt5) QMediaDevices  
usage  
* QTBUG-59726 no access to second camera on android phones with dual  
front/back cameras  
* QTBUG-109583 Doc: Stale references in QAudioDevice docs  
* QTBUG-103567 QML MediaPlayer fails to playback rtsp media properly.  
* QTBUG-97265 Qt6 mediarecorder QML has invalid syntax in example code  
* QTBUG-109539 Devices example crash  
* QTBUG-109659 Audio capturing and playing does not work on Android  
* QTBUG-104849 audio input examples do not work on mac os  
* QTBUG-110844 QMediaRecorder frequently returns unknown errors when  
trying to record on Mac  
* QTBUG-110975 [Camera] Qt QML camera view on android is distorted in  
portrait view  
* QTBUG-111266 VideoOutput aspect ratio is not correct on Android in  
portrait view  
* QTBUG-111421 Camera preview ratio is not respected for portait  
orientation  
* QTBUG-107173 QML Camera is stretched the first time on Android  
* QTBUG-109415 Camera is automatically activated by CaptureSession  
* QTBUG-108018 Camera Example crashes on macOS 13 ventura  
* QTBUG-97166 Qt6 Multimedia - Subtitle Language Metadata Detection  
Incorrect?  
* QTBUG-109149 [Windows] Crash on MFPlayerControl::handleStatusChanged()  
  
### qttools  
* QTBUG-109316 lupdate produces identical rows  
* QTBUG-109614 QDoc creates truncated temporary header files  
* QTBUG-109735 \include docs should state snippet marker '//!' must be  
at the beginning on the line  
* QTBUG-111093 [QDoc] Fails for template instantiation with 2 types  
* QTBUG-111603 Qt Designer crash with custom widget plugin derived from  
QMainWindow with no central widget  
* QTBUG-105820 windeployqt does not support Qt compiled with -libinfix  
option  
* QTBUG-110963 Q Designer: inactive QPalette color values not stored  
correctly  
  
### qttranslations  
* QTBUG-109973 Compiling qt-everywhere-src fails  
  
### qtdoc  
* QTBUG-110742 "Qt for macOS - Specific Issues": sample code is wrong  
* QTBUG-104937 Conflicting android-manifest-file-configuration.html  
files  
* QTBUG-106682 Typo in the document  
* QTBUG-111271 Typo in the document?  
* QTBUG-111279 Typo in the document?  
* QTBUG-85544 androiddeployqt fails with message that neither  
libqtforandroid.so or libqtforandroidGL.so are included  
* QTBUG-97636 Qtbase for Android with examples fails to build  
* QTBUG-83997 Can't deploy a simple console application  
* QTBUG-93185 Android platform plugin not linked when using only QtCore  
* QTBUG-111061 Windows Versions in Supported Platforms is ambiguous  
  
### qtpositioning  
* QTBUG-105551 Missing nmeaSource property in geoflickr example  
* QTBUG-105558 GeoFlickr example does not ask for permissions on Android  
* QTBUG-110902 tst_qgeoareamonitor execution failed with exit code 3.  
* QTBUG-110931 tst_qgeoareamonitor::multipleThreads randomly hangs on  
macOS ARM  
* QTBUG-107584 [iOS] Missing plist/location properties in positioning  
examples  
* QTBUG-109303 Android: single updates for PositionSource and  
SatelliteSource take too long  
  
### qtconnectivity  
* QTBUG-109315 Implicit reconfigure causes error regarding missing  
target PkgConfig::BLUEZ  
* QTBUG-108461 Bluetooth blocks the main thread for a short time  
* QTBUG-111242 sdpscanner strcpy()s sdp_data_t::val::str into a fixed-  
size 1KiB buffer  
* QTBUG-103611 [Reg 5.15 -> 6.x] Re-initializing QGuiApplication causes  
QQmlApplicationEngine to crash  
  
### qtwayland  
* QTBUG-75919 Override cursor has no precedence on Wayland  
* QTBUG-109302 Segmentation Fault with Wayland and QTreeWidget  
* QTBUG-87303 Wayland context menus can go off the screen because Qt  
does not do set_constraint_adjustment  
* QTBUG-97037 DragHandler / startSystemMove window move issue with QT6  
Webengine on Wayland  
  
### qt3d  
* QTBUG-109203 build fails when qtbase is configured without vulkan  
* QTBUG-99019 PhongMaterial does not work in GLES2  
  
### qtserialbus  
* QTBUG-107141 Typo in the document  
* QTBUG-107137 CMake instruction is not written in the document; grammar  
  
### qtserialport  
* QTBUG-109219 [SerialPort] bindable property tests fail  
* QTBUG-108450 REG: Qt 6.3.2 WinOverlappedNotifier possible crash  
  
### qtwebsockets  
* QTBUG-84315 QUrl::setAuthority() behavior changes  
  
### qtwebengine  
* QTBUG-108265 Pasting plain text does not work on Discord web  
* QTBUG-108843 [WebRTC] Crash inside  
RTCStatsCollector::ProduceAudioRTPStreamStats_n  
* QTBUG-106816 quicknanobrowser's popup window can't be moved or closed  
* QTBUG-109357 [REG 5.12 -> 5.15/6.x] QWebEngineUrlRequestInterceptor:  
Multiple redirects crashes the application  
* QTBUG-109179 auto test qwebengineclientcertificatestore fails to build  
* QTBUG-104869 QWebEngineDownloadItem::totalBytes() always returns -1  
* QTBUG-111574 documentation is wrong for WebEngineCertificateError  
* QTBUG-106072 QtPdf can't open password-protected PDF files on  
Windows/Android  
* QTBUG-112522 Webengine Widgets Client Certificate Example: Compilation  
Fails  
* QTBUG-111894 [REG 6.4.3->6.4.2] webenginequick/quicknanobrowser not  
launching  
* QTBUG-112661 WebEngine Quick Nano Browser Example: Crashes  
* QTBUG-105342 Test on qemu are very flacky  
* QTBUG-109235 Review toupper/tolower uses [Qt]  
* QTBUG-110749 Video decoding bug  
* QTBUG-110504 Webengine extremely slow in loading webpage in debug  
build  
* QTBUG-105988 a11y: Accessible interface can't be retrieved after  
calling QAccessibleEvent::setChild on event created using the  
constructor taking QAccessibleInterface*  
  
### qtwebview  
* QTBUG-82810 [Android] Deadlock for dynamically loading webview  
  
### qtcharts  
* QTBUG-108090 Qt chart does not show best fit line correctly  
* QTBUG-107890 When changing the label of a legend marker it will not  
update until something else triggers an update  
* QTBUG-108018 Camera Example crashes on macOS 13 ventura  
  
### qtdatavis3d  
* QTBUG-110036 Qml 3d oscilloscope example doesn't fit on screen  
* QTBUG-110042 Qml scatter example text on buttons not readable  
* QTBUG-110040 Qml custom input ui not mobile friendly  
* QTBUG-110041 Qml multigraph example buttons text not readable  
* QTBUG-110043 Qml spectogram example ui elements overlap  
* QTBUG-110037 Qml axis drag example text not readable  
* QTBUG-110038 Qml bars example graph is not centered  
* QTBUG-110044 Qml surface example text on buttons not readable  
* QTBUG-110045 Qml surface layers example controls not usable  
  
### qtscxml  
* QTBUG-109235 Review toupper/tolower uses [Qt]  
* QTBUG-110286 SignalTransition::triggered can cause Segfault  
  
### qtremoteobjects  
* QTBUG-104068 Fix qlalr warning when building qtremoteobjects  
  
### qtlottie  
* QTBUG-102550 Bugs with lottie animations  
  
### qtquick3d  
* QTBUG-109389 Crash if a Node with 2D item is deleted  
* QTBUG-109994 Runtime loader Example crash  
* QTBUG-110593 [REG 6.5.0 beta1->beta2] libassimp.a & libassimp.prl  
missing on Wasm  
* QTBUG-109992 Lights example controls obstruct view  
  
### qtshadertools  
* QTBUG-107483 Typo in the document?  
  
Known Issues  
------------  
  
### Android  
* OpenSSL does not work on 64-bit architectures (x86_64 and arm64-8a)  
with the prebuilt Qt 6.2.8 Android binaries. If you build binaries yourself,  
OpenSSL works ok. For more information, see  
https://bugreports.qt.io/browse/QTBUG-112815.  
  
### General  
  
Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-6.2/supported-platforms.html  
  
The RTA (release test automation) reported issues in Qt 6.2.x:  
https://bugreports.qt.io/issues/?filter=23315  
  
Qt 6.2.8 Open issues in Jira:  
https://bugreports.qt.io/issues/?filter=25039  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Amir Masoud Abdol  
Laszlo Agocs  
Albert Astals Cid  
Mate Barany  
Sebastian Beckmann  
Rolf Eike Beer  
Vladimir Belyavsky  
Nicholas Bennett  
Alex Blasche  
Eskil Abrahamsen Blomfeldt  
Joerg Bornemann  
Assam Boudjelthia  
Kai Uwe Broulik  
Michael Brüning  
Andreas Buhr  
Albert Astals Cid  
Creapermann  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Szabolcs David  
James DeLisle  
Cédric Le Dillau  
Artem Dyomin  
Alexey Edelev  
Oliver Eftevaag  
Christian Ehrlicher  
Iikka Eklund  
Hatem ElKharashy  
Andreas Eliasson  
Lionel Fafchamps  
Ilya Fedin  
Julian Greilich  
Lucie Gérard  
Heikki Halmet  
Andre Hartmann  
Elias Hautala  
Jani Heikkinen  
Ulf Hermann  
Volker Hilsheimer  
Johnny Jazeix  
Allan Sandfeld Jensen  
Timothée Keller  
Friedemann Kleint  
Michal Klocek  
Sze Howe Koh  
Jarkko Koivikko  
Tomi Korpipaa  
Fabian Kosmale  
Santhosh Kumar  
Sona Kurazyan  
Kai Köhne  
Inho Lee  
Paul Lemire  
Robert Löhning  
Thiago Macieira  
Leena Miettinen  
Samuel Mira  
Bartlomiej Moskal  
Marc Mutz  
Martin Negyokru  
Mårten Nordheim  
Roland Pallai  
Kwanghyo Park  
Timur Pocheptsov  
Joni Poikelin  
Aleix Pol  
Liang Qi  
Matthias Rauter  
Topi Reinio  
Shawn Rutledge  
Ahmad Samir  
Thomas Senyk  
Sami Shalayel  
Andy Shaw  
Venugopal Shivashankar  
Daniel Smith  
Ivan Solovev  
Axel Spoerl  
Piotr Srebrny  
Brett Stottlemyer  
Christian Strømme  
Tarja Sundqvist  
Tasuku Suzuki  
Morten Sørvig  
Ivan Tkachenko  
Jens Trillmann  
Paul Olav Tvete  
Sami Varanka  
Peter Varga  
Doris Verria  
Tor Arne Vestbø  
Ville Voutilainen  
Juha Vuolle  
Jaishree Vyas  
Edward Welbourne  
Paul Wicking  
Oliver Wolff  
Jannis Xiong  
Semih Yavuz  
Vlad Zahorodnii  
JiDe Zhang  
Yuhang Zhao  
abijak  
