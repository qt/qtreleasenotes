Release note  
============  

Qt 6.1 introduces many new features and improvements as well as bugfixes  
over the 6.0.x series. For more details, refer to the online  
documentation included in this distribution. The documentation is also  
available online:  
  
https://doc.qt.io/qt-6/index.html  
  
The Qt version 6.1 series is binary compatible with the 6.0.x series.  
Applications compiled for 6.0 will continue to run with 6.1.  
  
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
* 168855901a QCoreApplication::exit: make it a slot  
exit() is now a slot, like quit().  
  
* dcc4605bf0 QString: add missing char8_t* constructor / fromUtf8  
overloads  
Added a constructor and a fromUtf8() overload taking a `const char8_t  
*` argument.  
  
* 20a9f74851 Read DPI from X Settings initially as well  
Qt now reads Xft/DPI from X settings at startup, and will prefer this  
value over Xft.dpi from X resources.  
  
* f4292c10a3 Fix case sensitivity handling QSFPM  
Case sensitivity as well as regular expression options handling have  
been fixed. The original value is properly kept when using  
setFilterWildCard and setFilterFixedString. The regular expression  
options are now also properly kept when changing the case senstitivity  
through setFilterCaseSensitivity.  
  
* 8c0dab650d QSFPM: fix filterCaseSensitivityChanged signal emission  
logic  
A call to QRegularExpression overload of setFilterRegularExpression now  
emits a filterCaseSensitivityChanged signal, if required.  
  
* bced3a2477 ItemViews: don't delete dragged items when a subclass  
accepted the move  
Classes overriding dropEvent for MoveAction events to move data can  
call accept() on the event before calling the superclass to prevent  
QAbstractItemView from deleting the source item.  
  
* 4f5c8fecac Write out the HTML correctly for nested lists  
The output of toHtml() now handles nested lists correctly.  
  
* 3b78f6d94b Windows: Work-around misreporting of Script and Roman  
Fixed text in "Roman" and "Script" bitmap fonts not showing in Qt Quick  
applications.  
  
* 975e693747 Update bundled libjpeg-turbo to version 2.1.0  
libjpeg-turbo was updated to version 2.1.0  
  
* 2a2680ea22 macOS: Fix synthesized bold  
Fixed an issue where boldness would not be correctly synthesized for  
families with no bold variant.  
  
* 3e971f6fb4 SQLite: Update SQLite to v3.35.5  
Updated SQLite to v3.35.5  
  
* 90fe6301ba rhi: Fix memory leak  
Fixed a memory leak in QRhiGles2  
  
* c5e6a06305 Windows: Add synthesized fonts also when there is a style  
name  
Fixed an issue where bold/italic would not be synthesized for fonts if  
QFont::NoFontMerging was set.  
  
* b552e75561 QPageSize: make PageSizeId ctor non-explicit  
Conversion from a QPageSize::PageSizeId is now implicit.  
  
* 562187fc55 Fix memory leak when using small caps font  
Fixed a memory leak when initializing a small caps font.  
  
* 9e908fc57a Enable UNICODE for all Qt targets and Qt consumers by  
default  
Enables the UNICODE and _UNICODE definitions on WIN32 platforms by  
default for all cmake projects to reflect the qmake behavior. Use  
qt6_disable_unicode_defines function to disable the default unicode  
definitions.  
  
### qtdeclarative  
* 12a14164a7 Fix regression where qtquickcompiler cannot find rcc  
Fixed regression in Qt 6.1.0 which broke 'QT += qtquickcompiler' on  
Linux, macOS.  
  
### qttools  
* d34cf404 macdeployqt: Fix bug parsing otool output when deploying  
plugins  
Fix plugin deployment bug caused by otool parsing  
  
* 3b88ee4f macdeployqt: Fix plugin resolution bugs for non-standard  
installs  
Uses QLibraryInfo to resolve plugins at install locations.  
  
### qtquickcontrols2  
* a2b56c366 ToolTip: use contentWidth of Text contentItem to account for  
newlines  
The implicit width of ToolTips now accounts for newlines in the text.  
If you want to use the old behavior, set ToolTip's contentWidth to  
implicitContentWidth.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-92040 [macOS] Labs platform context menu items are disabled on  
modal window  
* QTBUG-92451 Static build fails on MinGW and MSVC2019, shadertools?  
* QTBUG-87861 Handle PLUGIN_EXTENDS = - in qmake plugin projects and in  
pro2cmake  
* QTBUG-86670 Fix qtwayland / qtquickcontrols2 static builds failing to  
reconfigure in a non-prefix build  
* QTBUG-91957 Assert while trying to load SVG  
* QTBUG-92568 Using QNetworkInformation will cause application crash  
when exit  
* QTBUG-89456 QTypeTraits templates break existing code  
* QTBUG-92890 Qt 6.1.0 Android binary size on Windows host increased  
significantly  
* QTBUG-92908 gradients widget example crashes  
* QTBUG-92886 QAbstractItemModelTester false positive removing rows with  
no columns  
* QTBUG-86847 QXmlStreamReader.prefix() cannot return EndElement's  
prefix  
* QTBUG-19983 Setting a cancel button on QProgressDialog more than once  
causes layout to be invalid  
* QTBUG-92963 tst_qpromise fails to compile with C++20 standard enabled  
* QTBUG-86823 REG: Blinking cursor leaving an artifact in QTextEdit  
* QTBUG-92838 Redownloading same file in parallel produces a warning  
about removal of cache file  
* QTBUG-92260 QSortFilterProxyModel::setFilterRegularExpression(const  
QString &) preserves all pattern options  
* QTBUG-91885 QSqlTableModel support column names with dots  
* QTBUG-93007 QThreadPool should make sure maxThreadCount is > 0 as < 1  
breaks it even though the docs say otherwise.  
* QTBUG-93021 Qt6 Static build for macOS problem: Undefined symbols for  
architecture x86_64 and issues with libraries linking.  
* QTBUG-90030 Persistent index handling in QAbstractItemModel is wrong  
* QTBUG-91405 qt-configure-module does not work as expected with multi  
config ninja generator  
* QTBUG-93002 CMake: linker error with Linux Static Libraries while  
using QtQuick.Controls  
* QTBUG-85136 "qmake -qtconf foo.conf -query" does not work  
* QTBUG-87429 tst_QRhi::renderToTextureArrayOfTexturedQuad fails on  
Android Emulator in CI  
* QTBUG-92826 JSON documentation needs updating for deprecations  
* QTBUG-77427 setDropAction() is not respected in ItemViews during move  
operation on MAC  
* QTBUG-91284 Http2: authenticationRequired is not emitted  
* PYSIDE-1404 Incompatible import of "Object" in compiled UI  
* QTBUG-86670 Fix qtwayland / qtquickcontrols2 static builds failing to  
reconfigure in a non-prefix build  
* QTBUG-91770 qvnc: Arbitrary memory read vulnerability  
* QTBUG-67944 If user pressed back button during application startup.  
Application becomes unresponsive.  
* QTBUG-92940 MSVC: warning C4723: potential divide by 0 in Qt Gui  
* QTBUG-90945 SizeGrip missing  
* QTBUG-92584 QSqlTableModel ORDER BY doesn't quote table name [with  
spaces]  
* QTCREATORBUG-25389 Can't use manual tests from Creator  
* QTBUG-92579 Different Screen.pixelDensity and Screen.devicePixelRatio  
* QTBUG-71123 "moc" failed to parse auto in trailing-return-type signals  
and slots  
* QTBUG-93416 Sample code doesn't compile  
* QTBUG-92490 Stylesheet with pseudo state on QPlainTextEdit  
* QTBUG-88374 QTextDocument::toHtml: nested lists (ul, ol) not nested in  
output  
* QTBUG-85826 Some Windows fonts don't work in Text  
* QTBUG-92240 MDI Sub window title remains in main window title when  
DontMaximizeSubWindowOnActivation option used  
* QTBUG-91758 [REG 5.13.2->5.14.0]: QPainter renders <Spaces> in Text  
wrong when units  set to micrometers  
* QTBUG-92988 if font size is set via stylesheet for QTab, it chops off  
text  
* QTBUG-90840 QSyntaxHighlighter does not apply capitalization with  
QTextCharFormat::setFontCapitalization  
* QTBUG-85634 Japanese and Chinese characters have no effect by bold  
enabled  
* QTBUG-91538 qtshadertools/qtools require cmake wrappers from  
qtimageformats (WebP/Jasper) in static builds  
* QTBUG-93032 Reg:5.15.2->5.15.3 QPushButton Focus rect is change of  
behavior  
* QTBUG-91236 background-color does not propagate beyond first child  
element  
* QTBUG-93475 QPainter rotate causes pixmap rendering issues  
* QTBUG-92599 QLabel with word wrap makes unable to decrease parent  
items size  
* QTBUG-93620 W System.err: java.lang.NoSuchMethodException:  
notifyQtAndroidPluginRunning  
* QTBUG-92366 QListView has abnormal spacing when setWordWrap is true  
* QTBUG-87334 Graphical issue on some Android smartphones: white line at  
the top and the right side of the screen  
* QTBUG-89145 QStandardItemModel takeItem / takeChild does not emit the  
right signals  
* QTBUG-93635 Reg->6.0: Windows vista style: placeholderText has wrong  
color  
* QTBUG-93295 Session Resumption with Session ID - IPv6 -  
ephemeralServerKey is missing  
* QTBUG-91398 When QFont::NoFontMerging is set then if bold or italics  
is requested that is not provided by the font then it will end up not  
synthesizing this  
* QTBUG-70137 Dockwidgets - Placing QDockWidget is almost impossible  
* QTBUG-93636 Unnecessary hard link from qmake.exe to qmake6.exe  
* QTBUG-93494 iOS A11Y VoiceOver: QAccessible::EditableText not  
implemented as "TextField" and value is missing last character  
* QTBUG-93739 QT 6.1.0 does not compile with -DQT_NO_EXCEPTIONS=1  
* QTBUG-92182 Qt Dock Widgets super slow to dock  
* QTBUG-74291 QTemporaryFile does not work for Windows network paths  
* QTBUG-93779 [elxr] (error #412) unresolved symbols: 1  
* QTBUG-93831 [REG 5.15.2->5.15.4]: Android: Copy-pasting text is not  
possible after pasting  
* QTBUG-93750 Updating dependencies in qtdeclarative fails  
* QTBUG-85051 CMake doesn't support big resources  
* QTBUG-93770 Wrong pixel ratio when using OpenGL in an embedded window  
context  
* QTBUG-89951 Why does Qt 6 cmake add `UNICODE` to public definitions on  
Windows?  
* QTBUG-92188 Stack smashing detected using QImage::scaled  
* QTBUG-93895 Error C2440: 'initializing': cannot convert from 'const  
TCHAR *' to 'const wchar_t *  
* QTBUG-90662 Fix CI warnings qtbase  
* QTBUG-71701 QFileSystemModel fails to locate a host from the root  
node's visible children  
* QTBUG-93270 QPropertyBindingSourceLocation won't compile bacause of  
wrong source_location selection  
* QTBUG-93230 Conflict name for qt_add_resources  
* QTBUG-92861 QtQml does not provide version 6.2  
* QTBUG-88093 qtbase unable to build with system jpeg  
* QTBUG-87580 Add minimal set of tests to build for static Qt configs in  
Coin  
* QTBUG-87580 Add minimal set of tests to build for static Qt configs in  
Coin  
* QTBUG-93033 Deprecated Function "isTopLevel" in qwidget.h defined  
* QTBUG-91801 Potential memory leak in sending queued signals?  
* QTBUG-93019 [REG 5.15-6.0] QList/QVector regressions  
* QTBUG-93019 [REG 5.15-6.0] QList/QVector regressions  
* QTBUG-93176 Data race in tst_qurl::testThreading() detected by Thread  
Sanitizer  
* QTBUG-93019 [REG 5.15-6.0] QList/QVector regressions  
* QTBUG-86033 Update QtPlatformAndroid.cmake to include features in the  
old Qt5AndroidSupport.cmake  
* QTBUG-86033 Update QtPlatformAndroid.cmake to include features in the  
old Qt5AndroidSupport.cmake  
* QTBUG-86033 Update QtPlatformAndroid.cmake to include features in the  
old Qt5AndroidSupport.cmake  
* QTBUG-90341 The QtStartUpFunction function may be called repeatedly  
* QTCREATORBUG-25389 Can't use manual tests from Creator  
* QTBUG-87580 Add minimal set of tests to build for static Qt configs in  
Coin  
* QTBUG-92944 input problems in DynamicTexture example  
* QTBUG-87057 QListView item looses items from models that don't  
override moveRows during internal drag'n'drop  
* QTBUG-92944 input problems in DynamicTexture example  
* QTBUG-92500 When using a ShaderEffect which has been compiled with the  
qsb tool, it does not apply the effect at all  
* QTBUG-90662 Fix CI warnings qtbase  
* QTBUG-86677 QToolBar button resize chops text  
* QTBUG-93494 iOS A11Y VoiceOver: QAccessible::EditableText not  
implemented as "TextField" and value is missing last character  
* QTBUG-93565 Unnecessary dependency to host Tools package in cross-  
builds  
* QTBUG-63557 Showing / hiding QML Dialog type keeps allocating memory  
without releasing it  
* QTBUG-88989 Build errors on Android with latest gradle  
* QTBUG-64446 tst_QWidget::multipleToplevelFocusCheck() on linux  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
* QTBUG-80863 [cmake] excessive compilation of Import.cpp files for  
static plugins  
  
### qtsvg  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
  
### qtdeclarative  
* QTBUG-91749 Incorrect batching using overlapping QSGGeometry with  
lines having a width > 1  
* QTBUG-92562 qtdeclarative build error on x86-windows  
* QTBUG-89736 focusable item becomes impossible to focus after  
reparenting to a newly loaded item  
* QTBUG-91867 TextInput cursorDelegate position not updated after left  
padding change  
* QTBUG-92966 MSVC compiler warning C4267 in qqmlirbuilder.cpp  
* QTBUG-93048 Signal and Handler Event System   demo Grammatical errors  
* QTBUG-93083 setSceneGraphBackend(const QString &backend): where is the  
list of possible strings?  
* QTBUG-93404 QML Debugging : Breakpoints' internal ID is not assigned  
properly  
* QTBUG-63673 PinchArea uses wrong coordinate system when inside a  
rotated container item  
* QTBUG-92224 Show let type variable in Locals  
* QTBUG-92165 REG 5.15->6.0: when PinchHandler and DragHandler are used  
together, trackpad pinch gesture causes a jump  
* QTBUG-93175  tst_EcmaScriptTests::runInterpreted fails with Windows 10  
developer build  
* QTBUG-93264 TableView: first column does not unhide when changing  
column width  
* QTBUG-74572 When using a syntax highligher on the QQuickTextDocument,  
then triggering a rehighlight does not automatically update the text  
control using it  
* QTBUG-93563 [REG] qmake: Cannot locate rcc when using Qt Quick  
Compiler  
* QTBUG-69577 while using both qml and JavaScriptCore.framwork, iOS app  
got a non-public api references error  
* QTBUG-91716 TapHandler works only in the upper left corner of the  
screen when QQuickView given another window as parent  
* QTBUG-92839 QQuickRenderControl D3D11 should be made working with  
MinGW too  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
* QTBUG-92861 QtQml does not provide version 6.2  
* QTBUG-92944 input problems in DynamicTexture example  
* QTBUG-92944 input problems in DynamicTexture example  
* QTBUG-72906 ListView rejects QList models  
* QTBUG-92500 When using a ShaderEffect which has been compiled with the  
qsb tool, it does not apply the effect at all  
* QTBUG-80415 segfault in software renderer inside  
QSGSoftwareInternalImageNode  
* QTBUG-92944 input problems in DynamicTexture example  
* QTBUG-92944 input problems in DynamicTexture example  
* QTBUG-88644 tst_QQuickGridView::snapToRow() failed on msvc2019  
developer build in CI  
* QTBUG-92944 input problems in DynamicTexture example  
* QTBUG-88644 tst_QQuickGridView::snapToRow() failed on msvc2019  
developer build in CI  
* QTBUG-27671 QMLTest: Some subtests of  
tests/auto/qmltest/events/tst_events.qml are flaky  
  
### qtactiveqt  
* QTBUG-93446 MingGW: activeqt/qutlook configure fails  
* QTBUG-93944 error: "NOMINMAX" redefined  
  
### qttools  
* QTBUG-92590 qdoc generates 'quick3', 'qt3' tags for qtquick3d, qt3d  
* QTBUG-92478 [QDoc] Links for obsolete methods point to the wrong page  
* QTBUG-92355 scoped enum values can't be linked in documentation  
* QTBUG-65810 Outdated copyright notes  
* QTBUG-92386 [QDoc]  \omitvalue does not omit the enum's description  
* QTBUG-91644 macdeployqt doesn't deploy plugins when build qt with  
custom -plugindir and frameworks in app bundle cannot resolve rpath  
* QTBUG-49591 Qt Designer: QTableWidget : Horizontal labels are not  
visible (horizontalHeaderVisible property is not saved correctly) when  
in page-based container  
* QTBUG-91644 macdeployqt doesn't deploy plugins when build qt with  
custom -plugindir and frameworks in app bundle cannot resolve rpath  
  
### qtdoc  
* QTBUG-93245 Documentation: New 6.1 modules missing from overview  
* QTBUG-91239 Porting to Qt6: high dpi scale factor default rounding  
policy not documented  
* QTBUG-93895 Error C2440: 'initializing': cannot convert from 'const  
TCHAR *' to 'const wchar_t *  
  
### qtwayland  
* QTBUG-89680 Touch is ignored if up and down arrives in the same  
wl_touch.frame  
* QTBUG-93751 Update dependencies on 'dev' in qt/qtwayland  
* QTBUG-92861 QtQml does not provide version 6.2  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
  
### qt3d  
* QTBUG-92163 top-level configure returns with exit code != 0 if qt3d is  
checked out  
* QTBUG-93240 Configure error in qt3d for -developer-build -release  
* QTBUG-92861 QtQml does not provide version 6.2  
* QTBUG-90243 Unable to build Qt3D Add-On with Conan, Qt6.0.1,  
Qt6.1.0Alpha,6.0.2, 6.0.3, 6.0.4  
  
### qtimageformats  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
  
### qtquickcontrols2  
* QTBUG-92883 [qt6] duplicate symbols in mac style plugin  
* QTBUG-93172 Duplicate symbol qInitResources_qmake_immediate when  
building qtquickcontrols2 gallery example against static macOS Qt  
* QTBUG-88220 Add documentation pages for the new native styles  
* QTBUG-92214 QML Dial with stepsize set gives unexpected result  
* QTBUG-93430 macOS: sliders should not get focus from clicking on them  
* QTBUG-93423 macOS: slider handle focus ring is too big  
* QTBUG-91924 With the Imagine style then it is possible that the  
background of a GroupBox is clipped by two pixels  
* QTBUG-83630 Qt Quick Control 2 Tooltip can be way too big when you  
have newlines  
* QTBUG-92158 [REG 5->6]QML Customised scrollbar has incorrect size and  
scrolling behaviour  
* QTBUG-89126 REG: ScrollView doesn't remove ScrollBar after settinging  
the new one  
* QTBUG-92861 QtQml does not provide version 6.2  
* QDS-4212 Changing Range Slider snap mode changes it's orientation  
* QTBUG-89938 tst_QQuickPopup::macOS fails with macOS 10.15 and 11.1 and  
with Xcode 12.3  
* QTBUG-83630 Qt Quick Control 2 Tooltip can be way too big when you  
have newlines  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
  
### qtcharts  
* QTBUG-59040 QtCharts performance bad when min/max values changed  
* QTBUG-79218 When zooming out enough then the labels on the axes will  
end up showing drawing errors  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
  
### qtdatavis3d  
* QTBUG-93263 QtDatavisualization examples not compiling on Android  
* QTBUG-91103 QML theme shows as totally dark when specified during  
creation  
* QTBUG-93506 Gradients don't show.  
* QTBUG-93676 Itemmodel example draws text as garbage  
* QTBUG-92995 Some datavisualization examples run with warnings  
* QTBUG-92861 QtQml does not provide version 6.2  
  
### qtvirtualkeyboard  
* QTBUG-90809 Inconsistent behavior of InputPanel between release and  
debug config on Windows  
* QTBUG-93459 [Highlighted example] virtualkeyboard/static fails to  
compile on iOS  
* QTBUG-93997 Warnings with virtual keyboard in Qt 6  
* QTBUG-92861 QtQml does not provide version 6.2  
  
### qtscxml  
* QTBUG-93444 [Highlighted example] qtscxml/trafficlights-qml-dynamic  
crashes on Android hw  
* QTBUG-92861 QtQml does not provide version 6.2  
* QTBUG-92541 statemachine/padnavigator, build fails: QOpenGLWidget: No  
such file or directory  
  
### qtlottie  
* QTBUG-92861 QtQml does not provide version 6.2  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
  
### qtquicktimeline  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
  
### qtquick3d  
* QTBUG-92389 QQuick3DInstancing not clearing m_instanceDataChanged  
* QTBUG-92917 Changing instanceCountOverride has no effect  
* QTBUG-93097 Quick3D Texture might not capture the latest state of  
sourceItem  
* QTBUG-93095 View3D picking breaks if 2D Quick Item added to scene  
* QTBUG-90564 Crash if some importer plugin can't be loaded  
* QTBUG-93266 The new QML types in Qt Quick 3D for the particle system  
miss  a \since  
* QTBUG-93605 PointLight is not properly projected on skinned meshes  
* QTBUG-92953 Mesh rotation is not correct if it is not in Skeleton node  
* QTBUG-93095 View3D picking breaks if 2D Quick Item added to scene  
* QTBUG-92831 Particles testbed Animated Sprite not working with qmake  
* QTBUG-92861 QtQml does not provide version 6.2  
* QTBUG-93034 No changed signals from particlesystem time  
* QTBUG-92917 Changing instanceCountOverride has no effect  
* QTBUG-92892 Rotated emitter velocity not always correct  
* QTBUG-90817 Quick3D Model bounds not set in an imported scene  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
  
### qtshadertools  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
  
### qt5compat  
* QTBUG-92861 QtQml does not provide version 6.2  
* QTBUG-93015 ColorOverlay color property documentation wrong  
  
### qtcoap  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
  
### qtmqtt  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
  
Known Issues  
------------  
  
Credits for the  release goes to:  
---------------------------------  
  
Aavitsland Eirik  
Adam Cristian  
Agocs Laszlo  
Apostolou Dimitrios  
Baijot Vincent  
Beldi Luca  
Bin Chen  
Blasche Alex  
Blomfeldt Eskil Abrahamsen  
Bornemann Joerg  
Boudjelthia Assam  
Broulik Kai Uwe  
Chuan Wang  
Cid Albert Astals  
Croitor Alexandru  
Curtis Mitch  
D'Angelo Giuseppe  
David Szabolcs  
Dushistov Evgeniy A.  
Edelev Alexey  
Eklund Iikka  
Faure David  
Fedin Ilya  
Gaist Samuel  
Gehör Pekka  
Goldstein Maximilian  
Golubev Andrei  
Gruendl Henning  
Grönholm Kaj  
Gustavsen Richard Moe  
Haixiang Tang  
Halmet Heikki  
Hao Zhang  
Heikkinen Jani  
Heikkinen Miikka  
Heimrich Karsten  
Heng Gong  
Hermann Ulf  
Hilsheimer Volker  
Jensen Allan Sandfeld  
Karlsson Jonas  
Keller Christoph  
Khang Hyunkook  
Kittler Marius  
Kleint Friedemann  
Kobus Jarek  
Koehne Kai  
Koivikko Jarkko  
Korpipaa Tomi  
Kosmale Fabian  
Krus Mike  
Kushnir Igor  
Köhne Kai  
Lee Inho  
Lemire Paul  
Li Qiang  
Löhning Robert  
Macieira Thiago  
Martinec Tamas  
Mutz Marc  
Määttä Antti  
Nichols Andy  
Nordheim Mårten  
Parker Seth  
PengCheng Fan  
Persano Mauro  
Piippo Samuli  
Pocheptsov Timur  
Pohjanheimo Milla  
Pokrzywka Romain  
Qi Liang  
Reinio Topi  
Rocha Andre de la  
Rojas Antonio  
Rosenvik Niclas  
Rutledge Shawn  
Schmertmann Lars  
Scott Craig  
Seo Siyeon  
Shaw Andy  
Shivashankar Venugopal  
Solovev Ivan  
Srebrny Piotr  
Strømme Christian  
Suzuki Tasuku  
Sæther Jan Arve  
Sørvig Morten  
Sørvig Morten Johan  
Tuliniemi Jere  
Tvete Paul Olav  
Varanka Sami  
Verria Doris  
Vertriest Nico  
Vestbø Tor Arne  
Vuolle Juha  
Wang Dongmei  
Welbourne Edward  
Wicking Paul  
Xiang Zhang  
Xinwei Li  
Yrjänä Marianne  
Zhang JiDe  
Zimmermann John  
