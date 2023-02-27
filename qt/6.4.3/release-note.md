Release note  
============  
  
Qt 6.4.3 release is a patch release made on the top of Qt 6.4.2.  
As a patch release, Qt 6.4.3 does not add any new functionality but provides  
bug fixes and other improvements and maintains both forward and backward  
compatibility (source and binary) with Qt 6.4.2.  

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
* 95811fba5e CMake: Make it possible to specify a debug MySQL client  
library  
If pkg-config is not used, a debug build of the MySQL client library  
can be specified with -DMySQL_LIBRARY_DEBUG=<path-to-library>. The debug  
and release variants of the library are automatically detected. Setting  
MySQL_ROOT and MySQL_LIBRARY_DIR is sufficient in most cases.  
  
* 2b65c4943e Fix missing text when Harfbuzz fails to shape a substring  
Fixed a regression which would sometimes cause text to disappear if the  
string contained an unmatched variation selector character.  
  
* f11a9b203b QNetworkRequest: Make header parsing locale-independent  
Fixed a bug where certain QNetworkRequest::KnownHeaders wouldn't be  
recognized as such in certain locales.  
  
* 08a0f332b5 PCRE2: upgrade to 10.42  
PCRE2 has been updated to 10.42.  
  
* 81f1611cc8 windows: Fix vertical metrics with GDI engine  
Fixed an issue where the line gap of some fonts would be included twice  
in the font's leading.  
  
* db9d604357 QT_INLINE_SINCE: never inline for static Qt builds  
Restored binary compatibility for static Qt builds broken by the  
QT_INLINE_SINCE mechanism. Qt still does not guarantee BC for static  
build configurations otherwise.  
  
* 3801ac5db5 SQLite: Update SQLite to v3.40.0  
Updated SQLite to v3.40.0  
  
* 4a68590fb3 QTest::WatchDog: fix missing timeout resets on test  
function change  
Fixed a bug which caused QTEST_FUNCTION_TIMEOUT to be applied to the  
whole test execution, as opposed to each test function.  
  
* d045fe1f51 SQLite: Update SQLite to v3.40.1  
Updated SQLite to v3.40.1  
  
* 7b0fc393a0 Move QTypeInfo<std::pair> from qpair.h to qtypeinfo.h to  
avoid ODR violation  
The QTypeInfo for std::pair/QPair will now be correct even if qpair.h  
hasn't been included, fixing an One-Definition-Rule (ODR) violation.  
  
* 02a03f28f5 QMimeDatabase: don't stat() something that isn't a local  
file  
Fixed a regression from 6.4.0 that made certain QMimeDatabase functions  
that inspected file contents to fail on Unix systems, if the file was  
not a native file (e.g., a Qt resource).  
  
* 7dddb9df64 Update bundled libjpeg-turbo to version 2.1.5  
libjpeg-turbo was updated to version 2.1.5  
  
* 8bb9290b72 QVarLengthArray: clear() is not resize(0)  
clear() no longer requires the value_type to be default-constructible.  
  
* cffe6800d1 QFileSystemWatcher/Win: remove the pre-QFileInfo path  
normalization  
Fixed a bug that prevented removePaths() from removing the root of a  
drive on Windows.  
  
* 550ee1d752 CMake: Fix position independent code linker flags not being  
set  
Qt tools are now built with position independent code even with Unix  
toolchains where this is not the default, for example clang.  
  
* 3e9ffad0c8 SQLite: Update SQLite to v3.41.0  
Updated SQLite to v3.41.0  
  
### qtdeclarative  
* db8c78b176 Fix missing glyphs when using NativeRendering  
Fixed an issue where text using NativeRendering would sometimes be  
missing glyphs.  
  
* 2ce59cad5a QQuickTableView: change the order of row and column to  
modelIndex()  
Because of a source incompatible change in Qt 6.4.0 and Qt 6.4.1,  
modelIndex(column, row) has been reverted back to modelIndex(row,  
column), equal to how it was in Qt 6.3. This also affects modelIndex()  
in TableView. If the order used in Qt 6.4.1 is needed, you can set the  
environment variable QT_QUICK_TABLEVIEW_COMPAT_VERSION=6.4  
  
* 291d3ed0da TableView: deprecate modelIndex(row, column) in favor of  
index(row, column)  
modelIndex(row, column) has been deprecated in favor of index(row,  
column).  
  
* 4f7cda0c9f QmlCompiler: Fix coercion of undefined to float and double  
Converting a JavaScript value to a double or float, for example by  
inserting it into a typed array, now assumes JavaScript type coercion  
semantics. In particular, converting a value that is not actually a  
number now results in NaN where it previously sometimes resulted in 0.  
  
### qttools  
* 820a6a14e qdoc: Unify handling of QML types and QML value types  
  
  
### qtconnectivity  
* 85d04c1b SDP scanner: encode input URLs and escape XML-specific  
characters  
sdpscanner now %-encodes the URLs and escapes all XML-specific  
characters in them before adding the result to the generated XML output.  
  
### qtwayland  
* acd81a50 client: Fix infinite recursion with text-input-v2  
Fixed a possible crash when editing a field in an item view.  
  
* f8aac960 compositor: Fix crash when raising shell surface item  
Fixed an issue where the compositor would sometimes crash if a shell  
surface item was brought to front.  
  
### qtimageformats  
* beb3764 TGA Plugin: Fix reading of CMapDepth  
Fixed reading of TGA files with a non-zero X-origin  
  
* 8a1b61e Update bundled libwebp to version 1.3.0  
Update bundled libwebp to version 1.3.0  
  
* 6f678f7 Update bundled libtiff to version 4.5.0  
Bundled libtiff was updated to version 4.5.0  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-105046 Linker failures when building with  
-DFEATURE_openssl_linked=ON  
* QTBUG-109093 tst_QWidget::optimizedResizeMove flakes on openSuSE Leap  
15.4  
* QTBUG-108747 QTabletEvent TabletMove not sent to a QWidget without any  
children  
* QTBUG-108799 [REG 6.2.4-6.3.2] Airplane emoji completely breaks text  
rendering  
* QTBUG-108815 Installing qtdeclarative fails  
* QTBUG-108908 closing QComboBox popup with Escape key also closes  
QDialog on macOS  
* QTBUG-101680 MySQL plugin: QSqlQuery::prepare + exec no results when  
table contains JSON type  
* QTBUG-109060 QAction() handling of text does not seem correctly  
documented  
* QTBUG-109061 QAction and ampersands in text  
* QTBUG-109240 file INSTALL cannot find "/home/qt/work/qt/qtremoteobject  
s_build/mkspecs/modules/qt_lib_repparser_private.pri":  
* QTBUG-109239 file INSTALL cannot find "/home/qt/work/qt/qttools_build/  
mkspecs/modules/qt_lib_linguist_private.pri"  
* QTBUG-108677 macdeployqt tool does not copy networkinformation plugin  
* QTBUG-108641 system tray icons in Windows 10 goes blurry  
* QTBUG-109169 Invalid QColorTrcLut use causes unreadable text with  
16-bit X11 visuals  
* QTBUG-106634 Android examples: cmake error with cmake 3.18  
* QTBUG-104776 AndroidContentFileEngineIterator hangs when listing  
shared content with nested dirs  
* QTBUG-109226 Rare crashes in QXcbBackingStoreImage::flushPixmap  
* QTBUG-108440 Wrong icon picked in QMenu in multi monitor multi DPI  
setup (Vista style)  
* QTBUG-107627 AndroidAssetsFileEngineHandler is broken  
* QTBUG-107662 Android keyboard doesn't close when clicking on done  
* QTBUG-109375 [REG.]Widgets lose their focus frame when QProxyStyle is  
set  
* QTBUG-109165 No repaint when QGraphicsEffect gets destroyed  
* QTBUG-103515 QSystemTrayIcon/macOS: Cannot quit the app when the  
context menu is opened by secondary click  
* QTBUG-109400 Windows: Font Line spacing differs between Qt 5 and 6  
* QTBUG-99601 ios: QMAKE_PRE_LINK Gives Error :Multiple commands produce  
* QTBUG-109449 inlining QByteArray::isNull() causes BC break on static  
Qt builds  
* QTBUG-108848 iOS: Voice Control Accessibility feature breaks in iOS 16  
* QTBUG-106701 Crash with any QML app on external display with iPadOS  
16.1 on M1 iPad  
* QTBUG-109428 ABI broke for QJniObject::callVoidMethodV in 6.4  
* QTBUG-109466 QTEST_FUNCTION_TIMEOUT applies to the whole test, not per  
function  
* QTBUG-108365 [REG 6.4.0 -> 6.5] Low contrast status bar in Android  
applications  
* QTBUG-88652 QTEST_FUNCTION_TIMEOUT and test function limit (5 minutes)  
are not documented.  
* QTBUG-109329 tst_qprocess crash in OpenSUSE 15.4  
* QTBUG-109214 Documentation for QtAndroidPrivate is still wrong for  
CMake  
* QTBUG-109212 QLabel with embedded image using 'qrc:/' will no longer  
load  
* QTBUG-109026 Android: UI is scaled smaller than before  
* QTBUG-63700 QSharedPointer missing documentation for move operators  
* QTBUG-109453 GDI fallback surface format for Win 11 (21H2)  
* QTBUG-109586 QAndroidApplication::runOnAndroidMainThread() UB when  
timeout is set  
* QTBUG-106531 QDockWidget Docking resizes (widens) the widget by a set  
number of pixels  
* QTBUG-107026 http://matek.hu/xaos/doku.php is dead  
* QTBUG-103393 IBus input method cannot set panel position correctly  
with DPI scaling  
* QTBUG-109754 QTextEdit::setTabChangesFocus has no effect  
* QTBUG-106393 Mac OS: Dot and Comma key combinations not working for  
russian layout  
* QTBUG-109619 Enabling 2 extra Android CMake options leads to a build  
error  
* QTBUG-109746 tst_QWidget::optimizedResizeMove() and  
optimizedResize_topLevel() with QtWayland failed on Ubuntu 22.04, GNOME  
* QTBUG-109477 QImageReader will cause heap corruption when load jpeg  
(width: 1px height:100px) on Apple M1  
* QTBUG-106653 Crash on Accessibility interface  
* QTBUG-108790 Crash on QFuture::cancel() with continuation and thread  
context  
* QTBUG-109289 Documentation of QWidget::acceptDrops links to  
GraphicsView  
* QTBUG-109875 -Werror=type-limits for  
src/corelib/tools/qoffsetstringarray_p.h:85:27  
* QTBUG-109036 QXcbBackingStore::toImage() returns wrong image.  
* QTBUG-109230 Crash in QFuture  
* QTBUG-109610 developer-build fails for xcb  
* QTBUG-109958 tst_qalgorithms should not create unique datatags when  
testing  
* QTBUG-109547 Unnecessary dependency to Qt6QmlTools / qtdeclarative-  
native  
* QTBUG-110058 QCryptographicHash is not re-entrant  
* QTBUG-110002 FAILED:  
qtbase/src/xml/CMakeFiles/qattributionsscanner_XXX  
* QTBUG-110068 qmake: Generated Visual Studio project defaults  
"GenerateDebugInformation" to "false"  
* QTBUG-109237 [Reg-6.3.1->6.4.1] Calling formLayout->addRow can result  
in assert in Debug builds  
* QTBUG-110070 [REG]Qt crashes on all platforms when trying to paste  
using an empty clipboard  
* QTBUG-109738 Deploying a universal app for macOS fails  
* QTBUG-109745 Static assertion failed with  
QVarLengthArray<std::vector<std::unique_ptr<int>>>  
* QTBUG-110268 On macOS, Expose events cannot be filtered with  
QWindowSystemEventHandler  
* QTBUG-109840 QUrlQuery: operator== does not handle a case where  
exactly one object has null pimpl  
* QTBUG-110412 Crashes in many qml scenes when using vulkan  
* QTBUG-108183 Crash triggered by assertion in QTextDocumentLayout  
* QTBUG-84315 QUrl::setAuthority() behavior changes  
* QTBUG-110586 QRegularExpression wrong behavior (behaves differently  
from QRegExp)  
* QTBUG-64132 QToolButton should elide text when width constraints  
prevent from showing whole text  
* QTBUG-61042 A QML FileDialog shows a warning in a console after  
reseting the 'nameFilters' property  
* QTBUG-77211 Warning on nameFilters change in QML FileDialog  
* QTBUG-108325 QuicControls2 documentations incorrectly suggests to link  
to the library  
* QTBUG-110627 Qt doesn't really follow Windows short time format  
* QTBUG-109838 QFontMetricsF::horizontalAdvance seems to do unnecessary  
scanning  
* QTBUG-104836 [Reg 6.3.1 -> 6.4.0b1] Unavoidable "unreachable code"  
warnings from qanystringview.h  
* QTBUG-110707 Optimization in QMimeDatabasePrivate::mimeTypeForFile  
does not work for Custom File Engines  
* QTBUG-56595 QXcbConnection::getTimestamp() returns old timestamp  
* QTBUG-110271 Copyright year not updated to 2023 on documentation  
* QTBUG-108822 QDBus: unable to connect the InterfacesAdded signal of  
org.freedesktop.DBus.ObjectManager on the system bus (unless using  
QDBUS_DEBUG)  
* QTBUG-109518 QPdfWriter loses some of the content if it is positioned  
right  
* QTBUG-109206 QODBC: Reading Time fails when using ODBC Driver 17 for  
Sql Server  
* QTBUG-110967 MySQL Prepared Statement QDateTime: Not Working  
* QTBUG-110595 [REG 5.15 -> 6.x] QSvgRenderer::render(QPainter*) is now  
~100x slower  
* QTBUG-105870 QListItemView with SingleSelection unselects item when  
clicking on empty area  
* QTBUG-107526 action Cmd+Return does not emit shortcut override event  
on macOS  
* QTBUG-109832 QMYSQL plugin no longer works with older supported  
versions of MySQL/MariaDB  
* QTBUG-106718 [REG] QCoreApplication::processEvents() processes  
deferred delete  
* QTBUG-106569 Ctrl-C in QTreeView passes invalid QModelIndex to model  
when model is empty  
* QTBUG-107844 FileDialog: cannot open image picker dialog on iOS  
* QTBUG-107770 no member named 'init' in 'QStyleOption'  
* QTBUG-110986 QFileSystemWatcher::removePaths() Does not removes drive  
* QTBUG-111131 setDragEnabled() is breaking interactive item selection  
in QTreeView  
* QTBUG-102010 QScroller prevents QAbstractItemView::DoubleClicked edit  
trigger  
* QTBUG-111268 three dependencies in binding of  
Q_OBJECT_BINDABLE_PROPERTY causes crash  
* QTBUG-111149 Reg->6.4.2: Windows: Qt Designer freezes when dragging  
actions in QMenu  
* QTBUG-109511 QtConcurrent in 6.4.0 and later shows undesirable  
behaviour  
* QTBUG-111698 Build fails with -march=amdfam10  
* QTBUG-107687  [REG 6.3.1 -> 6.3.2] qt_add_resources with .qm  
translation files no longer rebuild generated .qrc when .qm files change  
* QTBUG-108113 "RCC: Cannot find file" in qt_add_translations  
* QTBUG-109135 Qt warning "Failed to create SecCertificate from  
QSslCertificate"  
* QTBUG-107604 [Reg 5.15.10 -> 5.15.11] Incorrect fullscreen dimensions  
on some Android devices  
* QTBUG-107923 Wrong height of the window on Android  
* QTBUG-25280 QNetworkAccessManager concurrent request limit not  
configurable  
* QTBUG-109235 Review toupper/tolower uses [Qt]  
* QTBUG-105820 windeployqt does not support Qt compiled with -libinfix  
option  
* QTBUG-107893 cmake: multi-ABI Android builds do not forward cmake  
arguments  
* QTBUG-105736 tst_qfile unixPipe and socketPair tests fail on Android  
12  
* QTBUG-106906 tst_qtcuncurrentrun::pollForIsFinished occasionally  
crashes  
* QTBUG-105958 [Android] Intent + Talkback leads to deadlock  
* QTBUG-99125 windeployqt does not deploy qml stuff in a call with  
multiple applications  
* PYSIDE-2182 QTimer.singleShot example documentation does not work  
* QTBUG-109857 qt-configure-module not executable for android_armv7 on  
linux host  
* QTBUG-105804 The qt_ntfs_permission_lookup mechanism is prone to data  
races  
* QTBUG-110703 tst_QFocusEvent::checkReason_ActiveWindow() fails on  
macOS 13.2  
* QTBUG-109268 QWindow on Android doesn't use full area on some devices.  
* QTBUG-97503 Reg[5.15.2-5.15.6] Android: Keyboard covers the inputfield  
* QTBUG-109351 Bottom Navigation Bar overlaps app window  
* QTBUG-110501 Wrong calculation of display area on android when virtual  
keyboard is present before opening the app  
* QTBUG-110952 uic-generated connnection to QLCDNumber::display() fails  
to compile due to overloads  
* QTBUG-110899 Incorrect warning about binding loop in  
QtQuick.Controls.Control  
* QTBUG-103514 Possible crash in imagescaling example.  
* QTBUG-102474 Sometime SSL leads to hang application on exit  
  
### qtdeclarative  
* QTBUG-107079 [qmltc] dash in filename breaks compilatino  
* QTBUG-109200 Shape with QT_QUICK_BACKEND=software crashes sometimes  
* QTBUG-109007 [REG 6.3->6.4] lost the ability to test  
HandlerPoint.pressedButtons (flags) using & operator  
* QTBUG-109048 qmlsc crashes with enum method parameters  
* QTBUG-108994 qml: signal handler crash on wrong arguments  
* QTBUG-108831 Some Rectangle borders are double the width with  
fractional scale ratios  
* QTBUG-107492 Typo in the document  
* QTBUG-105312 REG: SplitView no longer works with touch  
* QTBUG-109144 qmllint crashes with annotated function parameter  
* QTBUG-108024 [Non-qmlsc] `State.when` evaluation fails when an object  
is bound  
* QTBUG-109196 Changes assigning into array property  
* QTBUG-86744 ListView.isCurrentItem not available until model is  
refreshed  
* QTBUG-108600 [macOS] ListView's items get hover while scrolling in  
Inactive window and behaviour seems completely broken  
* QTBUG-108601 Hover handling is broken for ListView's items in specific  
scenario  
* QTBUG-103811 Drawer: Different behavior with mouse & touch input  
* QTBUG-109411 Quick Text's implicitWidth doesn't respect  
maximumLineCount  
* QTBUG-109140 [REG: 5->6] Slowly dragging Tumbler causes numbers to  
jump around  
* QTBUG-108713 Native font rendering in some cases misses letters  
* QTBUG-105148 Rotated qml combobox popup placed incorrectly  
* QTBUG-109542 TreeView: TreeView.modelIndex() has the order of row and  
column swapped  
* QTBUG-101736 QQuickWidget: button in a popup doesn't receive touch end  
event  
* QTBUG-109584 [Reg 6.3 -> 6.4] Cannot assign QVariantList to lists of  
other value types anymore in QML  
* QTBUG-109597 Seg fault in QQmlObjectCreator::finalize when creating  
QML object with initial bindings  
* QTBUG-109854 [REG 6.2.4 -> 6.2.5] QQuickImageProvider doesn't scale  
properly if Image size is not set on High DPI displays  
* QTBUG-96700 Strikethrough formatting changes to underline.  
* QTBUG-97594 Mac - Strikeout bugged in QML TextEdit for Japanese  
* QTBUG-109882 ShapePath: Switching from a transparent colour to a non-  
transparent one causes the wrong colour to be displayed  
* QTBUG-109567 Masked MouseArea containsMouse value incorrect after  
visibility changes  
* QTBUG-110023 Mouse Wheel broken inside Popup opened from a modal Popup  
* QTBUG-108664 TableView positions incorrectly  
* QTBUG-107797 linux: File selectors cannot be used  
* QTBUG-109074 qmlformat removes (extra)comments  
* QTBUG-95448 Re-add QQmlExtensionPlugin documentation  
* QTBUG-110315 Accessing the length of a QML_SEQUENTIAL_CONTAINER  
crashes  
* QTBUG-110438 QML_SEQUENTIAL_CONTAINERS and assignment to QML property  
does not work  
* QTBUG-110628 [Reg 6.2 -> 6.4] Binding does not accept local signal  
handlers anymore  
* QTBUG-110117 Building tst_qmlsplitlib fails  
* QTBUG-106074 Add and explain naming conventions and restrictions for  
files in QML  
* QTBUG-91390 ListModel doesn't keep objects of JavaScriptOwnership  
alive  
* QTBUG-95895 REG 5.15 -> 6.2: destroy() does not destroy objects after  
appending listModel.  
* QTBUG-96167 Ownership of C++ owned object flips when added to  
ListModel  
* QTBUG-75954 Flipable draws incorrectly when rotated and the angle is  
45°  
* QTBUG-110594 containsMouse of MouseArea is always true after pressed  
with propagateComposedEvents  
* QTBUG-111078 ExecutableCompilationUnit::saveToDisk() does not  
invalidate the cache it uses for loadFromDisk()  
* QTBUG-108704 QQmlGadgetPtrWrapper is dangerous  
* QTBUG-111136 Trying to debug samegame demos crashes it  
* QTBUG-111019 "Debug Error!" on lowenergyscanner example  
* QTBUG-107902 "Defining QML Types from C++" lacks CMake documentation  
* QTBUG-111179 Incorrect coercion to number for undefined  
* QTBUG-110111 [Reg 6.3.2 -> 6.4.x] DropShadow: Changing radius to 0 at  
runtime causes a crash when attached to Canvas  
* QTBUG-108441 Function call with destructured argument silently aborts  
compilation  
* PYSIDE-1345 vertexDataAsPoint2D() in QSGGeometry returns only one  
point  
* QTBUG-108150 Adding qml files from the build folder to the QRC is  
creating filenames so long it breaks the build on Windows host  
* QTBUG-107707 tst_qquickimageparticle fails with Ubuntu 22.04  
* QTBUG-109506 QQuickItemLayer::updateOpacity can be called with no  
effect internally and assert/crash  
* QTBUG-109235 Review toupper/tolower uses [Qt]  
* QTBUG-104679 [REG 6.2.4-6.3.1] ListView: ASSERT if PullBackHeader or  
PullBackFooter is used  
* QTBUG-110933 qmlsc mistakes Enum for Property  
* QTBUG-104761 acceptedButtons in DragHandler is apparently ignored  
* QTBUG-104570 QQuickHandlerPoint has no QML_ELEMENT declaration  
  
### qtactiveqt  
* QTBUG-109235 Review toupper/tolower uses [Qt]  
  
### qtmultimedia  
* QTBUG-109070 [DOCS] QCameraDevice docs refers to missing orientation()  
* QTBUG-108668 QAudioDevice shows incorrect (old Qt5) QMediaDevices  
usage  
* QTBUG-108383 QWindowsResampler "Failed to setup resampler"  
* QTBUG-108995 Seeking on a paused audio file causes it to "play" it  
* QTBUG-103567 QML MediaPlayer fails to playback rtsp media properly.  
* QTBUG-109443 Android: tst_QVideoWidget timeout  
* QTBUG-59726 no access to second camera on android phones with dual  
front/back cameras  
* QTBUG-109583 Doc: Stale references in QAudioDevice docs  
* QTBUG-109535 infinite loop in ffmpeg camera check  
* QTBUG-97265 Qt6 mediarecorder QML has invalid syntax in example code  
* QTBUG-109539 Devices example crash  
* QTBUG-109415 Camera is automatically activated by CaptureSession  
* QTBUG-108221 QAudioOutput crashes on Qt 6  
* QTBUG-109613 duplicate symbols in gstreamer and ffmpeg backends  
* QTBUG-109561 QML Camera working on Android is random  
* QTBUG-109391 Camera goes black after turning off and on.  
* QTBUG-110131 QML Camera unloading crash on iOS  
* QTBUG-109956 Example manifest data for Spatial Audio Panning Example  
wrong  
* QTBUG-109504 [REG 6.4.2->6.5.0] windows namespace build fails  
* QTBUG-110797 On android devices, when a 'Video' object is destroyed,  
the screen does not detect mouse events any more  
* QTBUG-109659 Audio capturing and playing does not work on Android  
* QTBUG-110844 QMediaRecorder frequently returns unknown errors when  
trying to record on Mac  
* QTBUG-104849 audio input examples do not work on mac os  
* QTBUG-108412 Playing mjpeg streams through ffmpeg crashes  
* QTBUG-108176 [macOS] QAudioDevice "perferedFormat" warnings  
* QTBUG-109168 Unloading Camera (QML) item on Android hangs app.  
* QTBUG-97166 Qt6 Multimedia - Subtitle Language Metadata Detection  
Incorrect?  
* QTBUG-108403 FFmpeg backend doesn't work as expected  
* QTBUG-110453  tst_QVideoWidget::fullScreen fails with Android target  
in RHEL-8.4  
* QTBUG-109149 [Windows] Crash on MFPlayerControl::handleStatusChanged()  
* QTBUG-109731 6.4.2, 6.5beta1 & 6.6 regression QML MediaPlayer shows  
Corrupt/Blank Video If Playback Starts at Launch  
* QTBUG-108693 [EVR] Crash on D3DPresentEngine::makeVideoFrame  
* QTBUG-98506 QImageCapture not functioning properly on boot2qt embedded  
device  
  
### qttools  
* QTBUG-109132 qdoc: QML value type documentation doesn't accept QML  
module information  
* QTBUG-109618 QtAttributionsScanner crashes frequently  
* QTBUG-110440 Qt Designer: Items just added to scratch pad are not  
visible on Windows  
* QTBUG-109614 QDoc creates truncated temporary header files  
* QTBUG-109316 lupdate produces identical rows  
* QTBUG-109735 \include docs should state snippet marker '//!' must be  
at the beginning on the line  
* QTBUG-110930 cross builds: designer examples installed incorrectly  
* QTBUG-111093 [QDoc] Fails for template instantiation with 2 types  
* QTBUG-110963 Q Designer: inactive QPalette color values not stored  
correctly  
  
### qtdoc  
* QTBUG-107723 Ensure a good visibility of the "what's new" pages  
* QTBUG-109324 Clarify the doc page about module changes in Qt6  
* QTBUG-110281 Link to current Apple documentation not archive for  
Info.plist  
* QTBUG-110668 wasm: WebSockets don't actually work from other threads  
* QTBUG-110742 "Qt for macOS - Specific Issues": sample code is wrong  
  
### qtpositioning  
* QTBUG-105551 Missing nmeaSource property in geoflickr example  
* QTBUG-105558 GeoFlickr example does not ask for permissions on Android  
* QTBUG-107584 [iOS] Missing plist/location properties in positioning  
examples  
* QTBUG-110902 tst_qgeoareamonitor execution failed with exit code 3.  
* QTBUG-110931 tst_qgeoareamonitor::multipleThreads randomly hangs on  
macOS ARM  
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
* QTBUG-108767 Examples don't shut down gracefully  
* QTBUG-109302 Segmentation Fault with Wayland and QTreeWidget  
* QTBUG-109051 Crash in multi-screen example when moving window  
  
### qt3d  
* QTBUG-109203 build fails when qtbase is configured without vulkan  
* QTBUG-108405 bounding volume results are not checked for validity in  
concurrent calcuation  
* QTBUG-99019 PhongMaterial does not work in GLES2  
* QTBUG-110762 Intel Skylake embedded target fails yocto build for Qt3D  
* QTBUG-107693 tst_QResourceManager received signal 11 (SIGSEGV) with  
Ubuntu 22.04 QEMU  
* QTBUG-107694 tst_RayCasting::shouldReturnAllResults fails with Ubuntu  
22.04 QNX  
  
### qtserialbus  
* QTBUG-107141 Typo in the document  
* QTBUG-109940 [REG 6.4.2->6.5/6.0] serialbus modbus examples not  
compiling on iOS  
* QTBUG-107137 CMake instruction is not written in the document; grammar  
  
### qtserialport  
* QTBUG-109219 [SerialPort] bindable property tests fail  
* QTBUG-108450 REG: Qt 6.3.2 WinOverlappedNotifier possible crash  
  
### qtwebsockets  
* QTBUG-108996 wasm: Threaded build causes unaligned or out of bounds  
access after calling deleteLater() on a WebSocket  
* QTBUG-84315 QUrl::setAuthority() behavior changes  
  
### qtwebengine  
* QTBUG-106816 quicknanobrowser's popup window can't be moved or closed  
* QTBUG-109357 [REG 5.12 -> 5.15/6.x] QWebEngineUrlRequestInterceptor:  
Multiple redirects crashes the application  
* QTBUG-109179 auto test qwebengineclientcertificatestore fails to build  
* QTBUG-104869 QWebEngineDownloadItem::totalBytes() always returns -1  
* QTBUG-111574 documentation is wrong for WebEngineCertificateError  
* QTBUG-106072 QtPdf can't open password-protected PDF files on  
Windows/Android  
* QTBUG-105342 Test on qemu are very flacky  
* QTBUG-109235 Review toupper/tolower uses [Qt]  
* QTBUG-110749 Video decoding bug  
* QTBUG-110504 Webengine extremely slow in loading webpage in debug  
build  
* QTBUG-105988 a11y: Accessible interface can't be retrieved after  
calling QAccessibleEvent::setChild on event created using the  
constructor taking QAccessibleInterface*  
  
### qtcharts  
* QTBUG-108090 Qt chart does not show best fit line correctly  
* QTBUG-107890 When changing the label of a legend marker it will not  
update until something else triggers an update  
* QTBUG-108018 Camera Example crashes on macOS 13 ventura  
* PYSIDE-2179 QtCharts not available in PySide6 qml  
  
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
  
### qtvirtualkeyboard  
* QTBUG-97901 tst_plugin::test_hangulInputMethod(row 24) fails  
* QTBUG-97830 Some Qt Virtual Keyboard tests checking the position of  
selection handles are failing  
  
### qtscxml  
* QTBUG-109235 Review toupper/tolower uses [Qt]  
* QTBUG-110286 SignalTransition::triggered can cause Segfault  
  
### qtspeech  
* QTBUG-108773 Cannot compile qtexttospeech.h for C++ projects  
* QTBUG-103611 [Reg 5.15 -> 6.x] Re-initializing QGuiApplication causes  
QQmlApplicationEngine to crash  
  
### qtremoteobjects  
* QTBUG-104068 Fix qlalr warning when building qtremoteobjects  
  
### qtlottie  
* QTBUG-102550 Bugs with lottie animations  
  
### qtquick3d  
* QTBUG-108606 All View3D instances where material is used are not  
updated when material color changes  
* QDS-8451 Adjusting horizon property value of sceneEnvironment does not  
work with drag  
* QTBUG-109157 QtQuick3D fails to compile with C++20 : allocator.destroy  
called in qtquick3d/src/3rdparty/embree//common/sys/vector.h:137  
* QTBUG-109389 Crash if a Node with 2D item is deleted  
* QTBUG-109249 Passing sourceItem-based texture to postprocessing effect  
uses the dummy texture  
* QDS-8853 Adding Height Field Geometry component to scene in 3D freezes  
3D view  
* QDS-8862 Hidden components come visible after resetting view  
* QTBUG-109994 Runtime loader Example crash  
* QTBUG-110593 [REG 6.5.0 beta1->beta2] libassimp.a & libassimp.prl  
missing on Wasm  
* QDS-8865 Issues/emulation layer crash when hiding scene that has  
Quick3DEffect applied  
* QTBUG-110695 SkyBoxCubeMap does not work (regression from 6.4)  
* QTBUG-110870 no matching function for call to min  
* QTBUG-109992 Lights example controls obstruct view  
* QTBUG-107841 tst_Input crashes a lot  
* QTBUG-111135 tst_input crashes  
* QTBUG-109296 Clean up resources properly on scene manager destruction  
* QTBUG-109564 Handle software backend more gracefully, not by crashing  
(Custominstancing, morphing & particles3d applications stopped  
unexpectedly, colibri-imx6ull)  
* QTBUG-109088 Not skinned Mesh doesn't follow parent node  
* QTBUG-105609 should be able to add a TapHandler to a Button to modify  
behavior  
  
### qtopcua  
* QTBUG-104418 tst_opcua:AbsoluteNodeTest is flaky on Mac  
  
### qtquick3dphysics  
* QTBUG-109015 qtquick3dphysics PhysX build fails using oneapi icx on  
windows  
* QTBUG-108897 QFATAL : tst_physicsscene::UnknownTestFunc() ASSERT  
  
Known Issues  
------------  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Amir Masoud Abdol  
Laszlo Agocs  
Martin Andersson  
Mate Barany  
Sebastian Beckmann  
Rolf Eike Beer  
Vladimir Belyavsky  
Nicholas Bennett  
Alex Blasche  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
Joerg Bornemann  
Assam Boudjelthia  
Aurélien Brooke  
Michael Brüning  
Albert Astals Cid  
Creapermann  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Szabolcs David  
Oliver Dawes  
James DeLisle  
Artem Dyomin  
Alexey Edelev  
Oliver Eftevaag  
Christian Ehrlicher  
Hatem ElKharashy  
Andreas Eliasson  
Lionel Fafchamps  
Ilya Fedin  
Markus Goetz  
Julian Greilich  
Robert Griebl  
Kaj Grönholm  
Richard Moe Gustavsen  
Heikki Halmet  
Thomas Hartmann  
Andre Hartmann  
Elias Hautala  
Jani Heikkinen  
Miikka Heikkinen  
Ulf Hermann  
Volker Hilsheimer  
Johnny Jazeix  
Allan Sandfeld Jensen  
Jonas Karlsson  
Timothée Keller  
Friedemann Kleint  
Michal Klocek  
Lars Knoll  
Sze Howe Koh  
Jarkko Koivikko  
Tomi Korpipaa  
Fabian Kosmale  
Mike Krus  
Santhosh Kumar  
Sona Kurazyan  
Kai Köhne  
Lauri Laanmets  
Inho Lee  
Paul Lemire  
Thorbjørn Lindeijer  
Robert Löhning  
Thiago Macieira  
Leena Miettinen  
Samuel Mira  
Bartlomiej Moskal  
Marc Mutz  
Martin Negyokru  
Andy Nichols  
Mårten Nordheim  
Roland Pallai  
Kwanghyo Park  
Ari Parkkila  
Samuli Piippo  
Timur Pocheptsov  
Joni Poikelin  
Lorn Potter  
Liang Qi  
Matthias Rauter  
Topi Reinio  
Christian Riggenbach  
Shawn Rutledge  
Ahmad Samir  
David Schulz  
Björn Schäpers  
Thomas Senyk  
Luca Di Sera  
Sami Shalayel  
Andy Shaw  
Venugopal Shivashankar  
David Skoland  
Ivan Solovev  
Axel Spoerl  
Piotr Srebrny  
Brett Stottlemyer  
Christian Strømme  
Tarja Sundqvist  
Tasuku Suzuki  
Morten Sørvig  
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
WANG Xuerui  
Weng Xuetian  
Andrey Yaromenok  
Semih Yavuz  
Thomas Zander  
Leon Zhang  
JiDe Zhang  
Yuhang Zhao  
abijak  
