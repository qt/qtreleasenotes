Release note  
============  
Qt 6.7.1 release is a patch release made on the top of Qt 6.7.0.  
As a patch release, Qt 6.7.1 does not add any new functionality but provides  
bug fixes and other improvements and maintains both forward and backward  
compatibility (source and binary) with Qt 6.7.0.  

For detailed information about Qt 6.7, refer to the online documentation  
included in this distribution. The documentation is also available online:  
  
https://doc.qt.io/qt-6/index.html  
  
The Qt version 6.7 series is binary compatible with the 6.6.x series.  
Applications compiled for 6.5 will continue to run with 6.7.  
  
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
  
### Security fixes  
* CVE-2024-33861 in qtbase  
  
### qtbase  
* e1f069e65d Update bundled libpng to version 1.6.43  
libpng was updated to version 1.6.43  
  
* 9478e25284 SQLite: Update SQLite to v3.45.2  
Updated SQLite to v3.45.2  
  
* 091ce6477c Revert default FlickDeceleration to 1500  
The default value for the platform FlickDeceleration hint is reverted  
to 1500 (rather than 5000 as in Qt 6.6). This sets the default value for  
Flickable.flickDeceleration, which can be overridden directly; and the  
default can also be overridden in any QPlatformTheme subclass.  
  
* 0e75b141b8 CMake: Consider NO_UNSUPPORTED_PLATFORM_ERROR for non-  
bundle mac apps  
The qt6_generate_deploy_app_script NO_UNSUPPORTED_PLATFORM_ERROR option  
will now have an effect when calling the API on non-bundle macOS  
executable targets.  
  
* 2fb9ac0de8 CMake: Move various rcc generated files into .qt  
subdirectory  
Generated resource files (and supporting files) will now be placed into  
the .qt/rcc subdirectory of a project build dir. The location is an  
implementation detail that might still change in the future, so it  
should not be relied upon.  
  
* 9c1752d7b1 QObject: add check for Q_OBJECT macro to findChild(ren)  
The class template parameter passed to QObject::findChild() or  
findChildren() is now required to have the Q_OBJECT macro. Forgetting to  
add it could result in finding children of the nearest ancestor class  
that has the macro.  
  
* 2cd1cd1541 QCborValue: fix sorting of UTF8-to-UTF16 strings  
Fixed a bug that caused certain non-US-ASCII string comparisons to  
produce results not in line with the CBOR specifications.  
  
* b62b6094dd Implement aliased text rendering with DirectWrite  
Support QFont::NoAntialias with the DirectWrite font engine.  
  
* 771cfca2ab Android: don't call JNI_OnLoad for libraries opened with  
QLibrary  
Loading a shared library with QLibrary no longer implicily calls a  
JNI_OnLoad implementation.  
  
* 74563f95ae SQLite: Update SQLite to v3.45.3  
Updated SQLite to v3.45.3  
  
* 7c4e1357e4 QStringConverterICU: Pass correct pointer to callback  
Fixed a bug involving moved QStringEncoder/QStringDecoder objects  
accessing invalid state.  
  
* 6bef40cb82 QXmlStreamWriter: decode UTF-8 into code points  
Fixed a bug that caused the class to fail to write UTF-8 strings with  
non-US-ASCII content when passed as a QUtf8StringView.  
  
* bdb713b1b7 QXmlStreamWriter: fix attempts to write bad QStrings  
The class now rejects writing UTF-8 and UTF-16 invalid input (improper  
code unit sequences).  
  
* d24b0c05a4 QProcess: fix startCommand() with whitespace-only strings  
Fixed a bug that would cause startCommand() to crash if passed a string  
that was empty or contained only whitespace characters.  
  
* 5be8cf4e9a QString: ensure multi-arg arg() parses replacement like  
single-arg arg()  
The QString::arg() overload taking multiple QString-like arguments is  
now fixed to interpret placeholders like the other arg() overloads: it  
will find at most two digits after the '%' character. That is, the  
sequence "%123" is now interpreted as placeholder #12 followed by  
character '3' (verbatim).  
  
### qtdeclarative  
* bfe8bffbb9 Material: remove ComboBox's insets  
ComboBox's insets were removed. This may cause visual changes to UIs.  
  
* 1b5b3e4b36 ApplicationWindow: explicitly set background size if not  
explicitly set  
ApplicationWindow now explicitly sets the width and height of its  
background if no size was explicitly set by the user. This matches the  
behavior of Control, and ensures that if e.g. an Image is used as a  
window's background, any changes in its implicit size (e.g. after a  
source change) won't affect its actual size.  
  
* 74bc2f9d1a Flickable: don't allow dragging with mouse buttons other  
than left  
Flickable is meant to be dragged (flicked) by touch events; and as a  
matter of legacy support, for now it can also be dragged by the left  
mouse button. Dragging with other mouse buttons, such as the right and  
middle buttons, is not allowed.  
  
* 3b95280fc9 CMake: Move generated qmltypes file into .qt subdirectory  
of build dir  
Generated .qmltypes files will now be placed into the .qt/qmltypes  
subdirectory of a target build directory. The location is an  
implementation detail that might still change in the future, so it  
should not be relied upon.  
  
* 8a349714af CMake: Consider NO_UNSUPPORTED_PLATFORM_ERROR for non-  
bundle mac apps  
The qt6_generate_deploy_qml_app_script NO_UNSUPPORTED_PLATFORM_ERROR  
option will now have an effect when calling the API on non-bundle macOS  
executable targets.  
  
* 8d28f98112 ItemView: Avoid undesired repositioning in updateCurrent  
If highlightFollowsCurrentItem is set to false, and highlightRangeMode  
is set to NoHighlightRange, then programatically setting the  
currentIndex of the list will no longer scroll the view to that item.  
  
### qtmultimedia  
* 7fcea568c Fix ABI breakage wrt QAudioSink/Source::stateChanged signals  
Qt 6.7.0 broke binary compatibility by renaming the QAudio namespace to  
QtAudio. Qt 6.7.1 restores compatibility with previous Qt 6 versions  
again by making QtAudio an alias for the QAudio namespace, but breaks BC  
with 6.7.0. Code previously built against 6.7.0 needs to be recompiled.  
  
* b99c83b21 Update pffft version to the latest version from upstream  
Updated pffft to fbc4058.  
  
### qtimageformats  
* 21116ae Update bundled libwebp to version 1.4.0  
Update bundled libwebp to version 1.4.0  
  
### qtserialbus  
* 23b2331c VectorCAN: Set CAN-FD configuration only for uninitialized  
channels  
Fixed XL_ERROR when try to set CAN-FD configuration for a virtual  
channel which was already opened by another application.  
  
### qtshadertools  
* 90142aa Change classification of NVIDIA license  
Re-classify previous custom nvidia license as AML-glslang, as  
introduced by the newest SPDX version.  
  
### qt5compat  
* b183f7e QText{En,De}coder: use DefaultConversion  
Fixed a bug that caused QTextEncoder not to write the Byte Order Mark  
for UTF codecs when the constructor without explicit flags was used.  
  
### qtopcua  
* 24709bf5 Fix status code handling for monitored items  
Report the right status code for monitored item updates  
  
### qtinsighttracker (Commercial only)  
* 9ef22dd Store local and remote configs separately  
Remote configurations always take precedence over local configurations  
and cannot be overridden using APIs.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-121514 [Reg 6.6.0->6.6.2] Focus wrong in dialog with  
QDialogButtonBox  
* QTBUG-120049 [REG 6.6.0 --> 6.6.1] Incorrect child widget has focus in  
dialog by default  
* QTBUG-123005 [Reg 6.2->6.5+] Qt::AA_ShareOpenGLContexts has stopped  
working for offscreen rendering  
* QTCREATORBUG-30425 Android C++ breakpoints does not work with Qt  
Creator  
* QTBUG-123059 "package android.location.altitude does not exist" when  
building qtpositioning for Android on Linux  
* QTBUG-118434 [Reg Qt5->Qt6] QMenu cannot arrange menu entries  
correctly when there are large quantity of them  
* QTBUG-120639 [REG 6.6.1 -> 6.7.0-beta1] Menu items too wide on 4K  
* QTBUG-122973 QDateTime::operator== documentation is wrong  
* QTBUG-113432 RubberBand update area is too small in QListView  
* QTBUG-86407 Accelerators in QDockWidget titles are displayed  
incorrectly in some styles  
* QTBUG-122821 QListView with checkable items duplicates checkbox  
* QTBUG-122825 QAbstractItemView::indicator not working properly  
* QTBUG-102820 [REG 5.15.2 => 6.2.4] Styled indicators not drawn in  
itemviews  
* QTBUG-123083 tst_QProcess::setChildProcessModifier fails in dev  
* QTBUG-123186 "Target "tst_qsvgdevice" links to:  
Qt6::QSvgIconPlugin_init but the target was not found" when building  
qtsvg for iOS  
* QTBUG-122181 Allow finding qtmultimedia mock plugin in manual tests  
* QTBUG-123151 tst_QStorageInfo::caching is flaky on RHEL  
* QTBUG-118209 Several issues when aborting network request  
* QTBUG-36127 Internal warning when aborting a QNetworkReply  
* QTBUG-122205 OpenXR feature breaks test builds  
* QTBUG-123286 'load_local_libs' and 'bunlded_libs' libraries in  
libs.xml are always prefixed with "lib"  
* QTBUG-118226 Rejected QMessageBox emits Accepted Signal  
* QTBUG-122996 Delegate definition should be in front of QGuiApplication  
but doing so sometimes makes reflection delegate unusable  
* QTBUG-122838 Android multi-abi builds broken if depfiles are used  
* QTBUG-122893 Sending QNetworkRequest fails on singlethreaded WASM  
* QTBUG-119169 QFutureWatcher::resultReadyAt() signals sent in random  
order  
* QTBUG-122257 windeployqt --list option prints status messages  
* QTBUG-123339 Critical QTextEngine regression in Qt 6.7.0 RC1.  
* QTBUG-119611 QPlainTextEdit access violation crash when inserting  
136,348,169 latin characters  
* QTBUG-122664 windeployqt can not find qtpaths executable  
* QTBUG-119619 CMake deploy script finds x64 libraries for WoA  
application.  
* QTBUG-123324 dSYM warning: skipping debug map object with duplicate  
name and timestamp  
* QTBUG-121500 Default flick deceleration is far too high for  
touchscreens, can't be customized through platform theme  
* QTBUG-35608 Flickable speed and deceleration does not scale with pixel  
density  
* QTBUG-35609 Flickable speed and deceleration are not easily  
customisable  
* QTBUG-52643 Dragging threshold on high DPI touch devices is too small  
* QTBUG-97055 QQC2 Flickable scrolling is not linear with clicky wheels  
on Qt 6.2.0  
* QTBUG-122588 AA_UseStyleSheetPropagationInWidgetStyles does not work  
if parent widget is already shown  
* QTBUG-122910 Hinting is bad with fractional scaling, Wayland and  
hintfull  
* QTBUG-116086 tst_qqmlbinding::restoreBindingWithoutCrash leaks memory  
* QTBUG-123374 Linux on Arm fails with '-headersclean' in  
global/qfloat16.h  
* QTBUG-123401 Ambigious overload of operator<<(QDBusArgument &arg,  
const Container<Key, T> &map) for QMap with nested pairs  
* QTBUG-122747 Reparenting QTabWidget with a native window tab can cause  
crash  
* QTBUG-123486 qcontainertools_impl.h:383:14: error: ‘D.279326’ is used  
uninitialized [-Werror=uninitialized]  
* QTBUG-106709 Application looks too small on an external display with  
iPadOS 16.1 on M1 iPad  
* QTBUG-123032 [REG: 6.6.1->6.6.2] Override cursor changes together with  
window creation and destruction crashes on KDE  
* QTBUG-120768 Non-Native Dialog opens file when attempting to open  
invalid file  
* QTBUG-123554 xcb: Enabling touch device while application is running  
causes a crash on first touch  
* QTBUG-123092 Explain the order and the logic of using various SSL  
backends  
* QTBUG-123588 Compiler warnings in generated code of user project  
* QTBUG-123353 building androidnotifier example with qmake fails  
* QTBUG-123722 QComboBox shown with black popup background  
* QTBUG-122684 Inconsistent QPolygonF serialization  
* QTBUG-122704 QPainterPath de-serialisation from QDataStream fails if  
item isn't empty  
* QTBUG-122083 Markdown writer fails to escape special characters  
* QTBUG-96051 markdown writer: in a table cell ending with backslash,  
it's not escaped  
* QTBUG-123875 QRestAccessManager include documentation is incorrect  
* QTBUG-123334 QMessageBox wrong icons displayed on Android  
* QTBUG-123937 Wrong preprocessor conditional in qspan.h  
* QTBUG-123959 qApp crashes after being deleted when hosted as a plugin  
and when focus application is changed  
* QTBUG-123932 qstorageinfo_linux.cpp:15:10: fatal error: linux/mount.h:  
No such file or directory  
* QTBUG-80167 QOpenGLWidget no longer repaint if a paint-on-screen  
widget is updated  
* QTBUG-123989 Building Qt for Android with examples fails with missing  
QObject:connect() overload  
* QTBUG-120276 Crash when reparent a native child to a different tlw if  
QT_WIDGETS_RHI=1 is set on Windows  
* QTBUG-123444 regression: ODBC connection strings no longer work with  
QSqlDatabase::setDatabaseName()  
* QTBUG-123478 regression:  ODBC QSqlDatase::record() broken  
* QTBUG-114243 Qt 6.5 regression with static cross-compiling for Windows  
* QTBUG-111235 tst_QOpenGLWidget::reparentHidden() fails on Android 12  
CI  
* QTBUG-111236 tst_qvulkan cases fail Android 12 CI  
* QTBUG-123791 Crash in qwindows11style with null widget  
* QTBUG-124164 QFileSystemModel delete takes 1s  
* QTBUG-122135 uri manual test fail  
* QTBUG-123632 Regression: Setting background-color style of  
QTreeView::item breaks alternatingRowColors  
* QTBUG-124151 Layout Item Is Not Properly Deleted if Layout Is Disabled  
* QTBUG-123848 Short cuts involving 2 (or more) modifier keys are not  
longer handled by the Input Methods on macos.  
* QTBUG-106516 Multi-modifier key events not correctly handled on macOS  
* QTBUG-124254 Names can start with a non-letter char in Address Book  
example  
* QTBUG-124186 syncqt is not found when building qt submodules using  
cmake >= 3.29  
* QTBUG-103019 MinGW Qt6Platform.pc has an extra '>' after '-D_UNICODE'  
* QTBUG-122180 When changing the stylesheet for a selected, checked  
QHeaderView section then it disregards the font weight setting  
* QTBUG-92855 Dock widgets' title bars on macOS dark mode do not fit in  
* QTBUG-123162 macOS: QMdiSubWindow title bar gradient stands out too  
much in dark mode  
* QTBUG-124191 [REG: 6.6->6.7] QComboBox custom view is destroyed if  
style changes  
* QTBUG-118887 Screen.orientation broken on android 14  
* QTBUG-118236 Declarative Camera Example orientation errors on Android  
13 / Android 14  
* QTBUG-123054 Reg[5->6] QSvgRenderer generated images are not identical  
* QTBUG-93413 uic and overloaded slots  
* QTBUG-122208 Randomly getting "Access is denied" error  when saving  
files with QSaveFile.  
* QTBUG-124085 Incorrect icon used for "document-properties" on Windows  
* QTBUG-123798 tst_QComboBox::popupPositionAfterStyleChange() flaky on  
QNX  
* QTBUG-124267 QTableView's corner button documentation is inconsistent  
with its implementation  
* QTBUG-113492 META + Tab and CTRL + Tab shortcuts do not function on  
macOS  
* QTBUG-8596 Mac cocoa only: QKeyEvent Qt::Key_Tab not accessible to  
event or eventFilter  
* QTBUG-118985 The screen becomes blank after unlocking the screen in  
the app with Vulkan content rendered under a Qt Quick scene  
* QTBUG-118840 [Crash] Vulkan examples crash on Android when unlocking  
the screen  
* QTBUG-124003 xcb: Mouse enter event is no longer delivered when mouse  
leaves windows with pressed button  
* QTBUG-97645 QWindowsFontEngineDirectWrite ignores QFont::NoAntialias  
flag  
* QTBUG-73386 Serializing Qt Data Types Documentation not up to date  
* QTBUG-121046 Some dependencies are always considered not up to date.  
* QTBUG-92007 [REG: 5.13->5.14] QLibrary is now automatically calling  
JNI_OnLoad of loaded library  
* QTBUG-124349 Duplicate data tags in tst_QVariant::compareNumerics()  
* QTBUG-123962 [regression] QMenu crashes on eglfs  
* QTBUG-67807 QOpenGLFunctions_4_5_Core has wrong prototypes for  
*NamedBuffer* functions  
* QTBUG-87219 MOC's preprocessing is not conformant  
* QTBUG-124288 Moc compile error when using enums  
* QTBUG-124301 QTableView resize causes infinite loop if signal is  
connected before model is set  
* QTBUG-124232 wasm: Not possible to type TAB character, it always moves  
focus  
* QTBUG-124343 QMenu documentation points to deprecated  
QMouseEvent::globalPos()  
* QTBUG-124366 wasm: keyboard input on linux touchscreen device not  
working  
* QTBUG-122740 Android Embedded QML View: App crashes when selecting  
text  
* QTBUG-120331 rendering svg causes int overflows in  
blend_vertical_gradient_argb  
* QTBUG-123167 QTextBrowser.toHtml is not rendering supported CSS border  
property for html table tag.  
* QTBUG-123839 useless file accesses in qt_findAtNxFile() originating  
from QStyleSheetStyle::loadPixmap()  
* QTBUG-2188 QTextDocument: Bullets in bullet lists are not affected by  
text color  
* QTBUG-213 Error in drawing of bullets in QTextDocument  
* QTBUG-57833 QTextEdit list number/bullets inherit the following text  
style  
* QTBUG-116197 org.freedesktop.appearance.color-scheme is supported in a  
weird way  
* QTBUG-123579 QLocale::toDatetime does not always work when it should?  
* QTBUG-124160 [Reg] NSSearchField no longer visible after hide/show  
QDialog  
* QTBUG-124117 Compiling code based on Qt 6.7.0 with MSVC compiler vc16  
(14.29.30133) causes compile error "unreachable code"  
* QTBUG-124221 [Doc] QStringConverter lacks ICU support information  
* QTBUG-122241 QXmlStreamWriter::writeCharacters fails to write UTF-8  
encoded QAnyStringView  
* QTBUG-124512 QProcess::startCommand crash if empty string is passed  
* QTBUG-118581 QString multi-arg wrong behaviors: percent(%) eats all  
numbers  
* QTBUG-123891 HTTP2: finished and errorOccurred signals never emitted  
when auth fails with code 401  
* QTBUG-121653 License clarification for unicode & unicode-cldr related  
files  
* QTBUG-113404 Wayland: Gestures are not delivered to correct top level  
widget  
* QTBUG-124554 QPushButton menu dropdown arrow looks odd on 100% DPI at  
HD (1920x1080) resolution  
* QTBUG-114539 QToolButton arrow clipped on screen with non-integer  
device pixel ratio  
* QTBUG-124580 QMimeData::setData("text/uri-list",…) loses last url  
* QTBUG-124376 Slow UI build in Release mode with MSVC  
* QTBUG-123928 Not all widgets follow mode switching at runtime in the  
Widget Gallery example  
* QTBUG-124447 Doing style->drawControl(QStyle::CE_ProgressBar) inside  
QStyledItemDelegate causes a crash  
* QTBUG-121583 Windeployqt does not take into account all dependencies  
and exits with failure due to missing platform plugin  
* QTBUG-123115 Finalize 6.7 API review of QCborStreamReader  
* QTBUG-123130 QDoc with Clang 18 drops noexcept from default methods  
* QTBUG-110502 Qt fills in private use unicode if a font is found using  
it  
* QTBUG-117948 qt_generate_deploy_qml_app_script() deploys QML plugin  
target but not the corresponding backing target  
* QTBUG-100336 QObject::connect using loadRelaxed to synchronize non-  
atomic writes  
* QTBUG-123229 Q_OBJECT in multi-line(?) C comment triggers automoc (but  
not qmake)  
* QTBUG-123438 syncqt fails on MSVC build  
* QTBUG-122580 Screenshorts for "Qt Widget Gallery" are cut off  
* QTBUG-48488 Cancelling Print to File Crashes Application  
* QTBUG-123306 Orientation issues with embedding QML to Android Java  
application  
* QTBUG-118234 tst_qvulkan (Failed) on Android 14  
* QTBUG-118220 tst_qrhi (Failed) on Android 14 emulator when running  
within a CI VM  
* QTBUG-124291  tst_QWidget::setParentChangesFocus(make dialog  
parentless, after) fails on Android 8 in CI  
* QTBUG-117500 Sporadic crash on  QFontEngineMulti::ensureEngineAt()  
* QTBUG-124111 Fix QNetworkReply on WASM  
* QTBUG-115158 Time zone names and abbreviations are not localised  
* QTBUG-123900 error: cannot pass object of non-trivial type  
'QtJniTypes::Context' through variadic function; call will abort at  
runtime  
* QTBUG-107185 Some tests appear to be re-testing the exact same data  
tag  
* PYSIDE-2648 Both sample/widget bindings examples fail in CMake on  
configure  
* QTBUG-124465 QDate::fromString very slow in 6.7.0  
* QTBUG-125142 [REG 6.7.0->6.7.1] Can't deploy to iOS/iOS simulator:  
ASSERT: "m_view.window" in file qioswindow.mm  
  
### qtsvg  
* QTBUG-123010 SVG supported by 6.6 but not by 6.7  
* QTBUG-122752 [Reg: 6.4.2 -> 6.5.3] QFont::setPixelSize warning when  
rendering svg files with painter font size set in pixels  
* QTBUG-121981 QtSvg parser does not handle nested svg elements  
correctly  
* QTBUG-124287 QtSvg allocation too large memory when load the svg image  
  
### qtdeclarative  
* QTBUG-120149 Material 3 - TextField placeholder issues when padding  
changed  
* QTBUG-113532 Animate RadioButton in the Material style  
* QTBUG-122230 Broken links in qtdeclarative docs  
* QTBUG-122894 Crash when QQuickView loads QML document that binds  
Overlay.overlay.[property]  
* QTBUG-122008 The child window does not get the style of the parent in  
the attached style properties example (QQuickAttachedPropertyPropagator)  
* QTBUG-117923 ItemParticle causes constant CPU usage and rerenders  
* QTBUG-122985 toggling TextEdit.format back and forth between AutoText  
and PlainText loses markdown after a couple of times  
* QTBUG-120772 TextEdit.textDocument loads according to mime type  
regardless of TextEdit.textFormat  
* QTBUG-121388 Qt Quick Controls: Palette role values don't get live  
updates  
* QTBUG-121466 ApplicationWindow background Image does not resize when  
source changed  
* QTBUG-119812 QML Advanced Tutorial 4  -  Example -  Highscores are  
doubled  
* QTBUG-122340 MultiEffect - Wrong initial position of the shadow  
(MultiEffect)  
* QTBUG-122746 Quick controls Popup - shadow is rendered incorrectly  
* QTBUG-123118 QQuickShaderEffect missing property updates  
* QTBUG-122665 [Reg 6.6.1 → 6.6.2] ListView footer item cannot be  
vertically placed  
* QTBUG-123225 REG[6.6 → 6.7]: QML: unscoped enums stopped working  
* QTBUG-122076 QQuickItem::classBegin()/componentComplete() never  
invoked when using QQmlComponent::loadFromModule()  
* QTBUG-123307 build fails "qtdeclarative/src/quick/platform/android/qan  
droidquickviewembedding.cpp"  
* QTBUG-123111 Particle System Application stuck on GUI thread  
* QTBUG-121500 Default flick deceleration is far too high for  
touchscreens, can't be customized through platform theme  
* QTBUG-35608 Flickable speed and deceleration does not scale with pixel  
density  
* QTBUG-35609 Flickable speed and deceleration are not easily  
customisable  
* QTBUG-120542 Editable SpinBox crashes Quick3d application  
* QTBUG-119765 [Reg 6.5.2 -> 6.6.1]default roles are not available in  
abstract table model headerdata  
* QTBUG-123428 [REG 6.6 → 6.7 ]Using QML_DISABLE_DISK_CACHE breaks QML  
code  
* QTBUG-97252 Swipeview stops responding after right-clicking  
* QTBUG-123421 Documentation wrong for QML_CONSTRUCTIBLE_VALUE  
* QTBUG-108019 QSGTexture::nativeInterface() doesn't work for  
QSGMetalTexture  
* QTBUG-95939 tst_taphandler is flaky on OpenSUSE  
* QTBUG-123413 qmltypes warning when using const in Q_INVOKABLE  
* QTBUG-123332 Install dir is incorrect for Qt6AndroidQuick.jar  
* QTBUG-123394 [REG 6.5.5 -> 6.6.2] Dial control looks wrong  
* QTBUG-114694 [Tests]  
tst_controls::Basic::SpinBox::test_editable_doubleSpinBox fails on macOS  
* QTBUG-123490 Flickable doesn't react to second touchpoint while first  
touchpoint is dragging DragHandler  
* QTBUG-86729 many Qt Quick test failures after input event refactoring  
* QTBUG-113226 Flickable emit flickStarted even though the child is  
processing the pinch gesture  
* QTBUG-123395 QML EXC_BAD_ACCESS crash  
* QTBUG-120267 qmllint: Member "destroy" not found on type "Popup"  
* QTBUG-123588 Compiler warnings in generated code of user project  
* QTBUG-123484 [Reg 6.7 > 6.6.2] Crash in QJSValue copy constructor  
* QTBUG-123594 Missing dependency in QtQuick/Controls/Material/impl  
* QTBUG-123613 qmlcachegen crashing with Qt 6.7.0-rc2  
* QTBUG-122564 Contactlist example not opening (CMake)  
* QTBUG-123535 qt_generate_foreign_qml_types fails with Q_ENUM_NS  
* QTBUG-118076 pragma FunctionSignatureBehavior: Enforced is broken for  
object lists  
* QTBUG-116589 Dynamic translations seem not working with  
QQmlApplicationEngine::loadFromModule()  
* QTBUG-123805 CurveRenderer crashes when calculating dash pattern  
* QTBUG-123114 QQuickPopupPositioner uses wrong bounds when  
Window.contentOrientation == Screen.orientation  
* QTBUG-115536 Setting Window.contentOrientation breaks Popup on regular  
desktop  
* QTBUG-120033 Binding not evaluated  
* QTBUG-119756 [Tests] Warnings in tst_controls::macOS::SpinBox  
* QTBUG-123596 Crash JS for x in o  { delete o[x] } if o is a  
sparsearray  
* QTBUG-123050 Crash when trying to build QML files (qmlcachegen)  
* QTBUG-119572 [Tests] Warnings in  
tst_controls::Imagine::RangeSlider::test_nullHandles()  
* QTBUG-119633 [Tests] Warnings in  
qtdeclarative/tests/auto/quickcontrols/controls/data/tst_slider.qml  
* QTBUG-118636 Some missing content of the rich text table while  
displaying HTML file with TextArea  
* QTBUG-124084 [Reg 6.5.3->6.7.0] Nested ListModel set from c++ is not  
working any more  
* QTBUG-123865 [Reg 6.2 -> 6.5] Crash when using PropertyChanges with  
multiple inline components  
* QTBUG-117899 [REG 6.4->6.5] Binding Loops -> Wrong layout because of  
interruption  
* QTBUG-118511 Binding loop if ColumnLayout implicitWidth is changed  
* QTBUG-122925 QQmlComponentPrivate::doBeginCreate can crash in some  
scenarios  
* QTBUG-124163 With SW backend, QQuickPaintedItems show aliasing when  
transformed  
* QTBUG-68527 Automatic ListView content positioning while disabled  
* QTBUG-124201 [Tests] Warnings in tst_controls::Windows::SpinBox  
* QTBUG-123378 QML TextInput makes the application unresponsive if made  
invisible when it has keyboard focus on Android  
* QTBUG-124226 Confusing example code for Qt.createComponent  
* QTBUG-43842 Scanning for QML imports of projects fails  
* QTBUG-123196  the Shape object doesn't display ShapePath objects  
injected by Shape.data.push() function.  
* QTBUG-124275 [Tests] Warnings in tst_controls::iOS::RangeSlider  
* QTBUG-117641 Loader and loaded item sizes can get unsynchronized  
* QTBUG-120670 TextField causing activeFocus of the calling item to be  
triggered multiple times.  
* QTBUG-84976 When Window has no activeFocus, activeFocus lost after  
transitioning back from Dialog to Window  
* QTBUG-124290 [Tests] Warnings in tst_controls::iOS::Slider  
* QTBUG-122250 GridView is missing documentation for reuseItems  
* QTBUG-124281 MultiEffect doesn't seem to free resources at its  
destruction  
* QTBUG-83408 Text disappears with ElideRight.  
* QTBUG-33608 Elide property of Text breaks component resizing  
* QTBUG-123773 [Contact List Example] Example not running on MacOS  
* QTBUG-124359 Cannot use variableAxes due to wrong component versioning  
* QTBUG-123227 Qt Quick Test missing cmake support  
* QTBUG-46487 PathView. DelegateModel::item: index out range error when  
model is reset with less number of items  
* QTBUG-75887 The delegate object in the Listview for DelegateModel with  
DelegateChoice is not being updated on role value change in the model  
* QTBUG-120097 Screen Reader reads password in Password TextField  
* QTBUG-124428 Customisation documentation includes deprecated  
DropShadow example  
* QTBUG-124225 [REG 6.7 → dev] Assert: start > 0 in  
QQmlComponentPrivate::beginCreate  
* QTBUG-121143 SelectionRectangle does not work correctly when de-  
selecting  
* QTBUG-123763 MessageDialog detailed text goes out of bounds in  
Material style  
* QTBUG-94100 TreeView: adding columns not handled  
* QTBUG-124459 qmlls: no completions after "id." when components are not  
bound  
* QTBUG-122783 Material.theme doesn't propagate to ListView header when  
elevation animated  
* QTBUG-123993 [Reg 6.6 -> 6.7] QVariantList conversion from/to QML  
broken in Qt 6.7  
* QTBUG-124220 Weird compiler warning for functions without return type  
annotation  
* QTBUG-124730 MultiEffects Shadow in repeater causes application to  
crash  
* QTBUG-124456 [6.4.2] Margins in QuickLayouts causing a QList exception  
(index out of range)  
* QTBUG-124363 [6.7 REG] Changing QML Window visible property clobbers  
window state  
* QTBUG-120067 Material 3 - Controls height issues  
* QTBUG-115438 [REG: 5->6] MouseArea onEnter triggers before onExit on  
the previous item  
* QTBUG-123014 tst_qquicktextdocument (Failed)  
* QTBUG-123160 crash in qquickspinbox  
* QTBUG-110475 [REG 6.4.1 → 6.4.2] Interactive elements in SwipeDelegate  
receive no events  
* QTBUG-123318 QT Quick controls - Wearable Demo example: Notifications  
in the demo mode is skipped  
* QTBUG-123210 QML: Rectangle with rounded corners and border width = 1  
shows not good anti-aliasing  
* QTBUG-108831 Some Rectangle borders are double the width with  
fractional scale ratios  
* QTBUG-122321 qmltc: WebEngineView with anchors causes assertion at  
component creation  
* QTBUG-123592 Foreign generation fails with namespace  
* QTBUG-123999 Heap buffer overflow in JS Set.delete  
* QTBUG-118222 tst_nodestest (failed) on Android 14 emulator when  
running in a CI VM  
* QTBUG-92855 Dock widgets' title bars on macOS dark mode do not fit in  
* QTBUG-123162 macOS: QMdiSubWindow title bar gradient stands out too  
much in dark mode  
* QTBUG-90479 [Reg 5.13.2->5.14.0] PathView's strange behaviour with  
model having 19 items  
* QTBUG-42504 QML PathView cacheItemCount does not work, crashes  
* QTBUG-59108 PathView enters in to loop of Creation/Destruction of  
delegates  
* QTBUG-50540 Pathview delegates not created correctly with caching  
enabled  
* QTBUG-112840 Please write the realistic usecase of Qt Quick Test to  
the documentation  
* QTBUG-114969 qmllint should consider QML2_IMPORT_PATH for import paths  
  
### qtactiveqt  
* QTBUG-122762 [Reg 5.15 -> 6.5] ActiveQt server does not return  
QVariantList properly  
  
### qtmultimedia  
* QTBUG-122959 GStreamer: "stop camera" does not stop camera  
* QTBUG-122575 Mediaplayer example not showing video on some Android  
emulators  
* QTBUG-112312 QFFmpeg EGL VAAPI failures  
* QTBUG-123312 [gstreamer] video playback broken with gstreamer older  
than 1.20  
* QTBUG-123205 Allow defining platform specific gstreamers  
colorconversion-plugins  
* QTBUG-123117 MediaPlayer crashes on seek after loop reset.  
* QTBUG-119583 ScreenCapture-Graphic&Multimedia- Issue when a captured  
window is being closed  
* QTBUG-122638 [gstreamer] deadlock when switching camera  
* QTBUG-123139 GStreamer: Qt Camera in stops after switching VideoOutput  
* QTBUG-113421 Qt Camera in QML Dies after closes the drawer with Camera  
* QTBUG-122968 QML Camera: Using zoom and switching cameras breaks the  
example  
* QTBUG-120266 [Windows] App hangs on destroying QML Video component  
during video playback  
* QTBUG-123131 Modified video frames are not updated for rendering  
* QTBUG-123215 fatal error: qplatformmediadevices_p.h: No such file or  
directory when building from source for Qt 6.6.2 on Windows  
* QTBUG-122184 [Crash] The 'Widgets camera' app crashes on Android when  
starting and stopping the video recording  
* QTBUG-123045 [Examples] Qt warning on changing audio input in Audio  
Source example  
* QTBUG-123597 QAudioDecoder crashes on files without audio track  
* QTBUG-120198 Process abruptly terminates while executing static  
destructor in Qt6Multimedia.dll  
* QTBUG-123899 [GStreamer] createVideoProfile unit test failure  
* QTBUG-123997 Public ABI breakage between 6.6 and 6.7 for  
QAudioSink::stateChanged(QtAudio::State)  
* QTBUG-124115 QtMultimedia configure fails for GPU-less yocto target  
* QTBUG-123967 QML media player example project fails to play AV1  
encoded videos.  
* QTBUG-123526 No video input devices with QT_MEDIA_BACKEND set to  
ffmpeg  
* QTBUG-124253 Direct3D debug layer reports error when playing videos of  
same size and pixel format  
* QTBUG-119914 VideoSink frame to image does not work on android  
* QTBUG-117771 Qt6.5.3 QMediaPlayer play video an error on android 11  
* QTBUG-123904 [gstreamer] tst_QMediaCaptureSession::testAudioMute test  
failure  
* QTBUG-123905 [gstreamer]  
tst_QMediaCaptureSession::stress_test_setup_and_teardown test failure  
* QTBUG-120963 QScreenCapture/QWindowCapture with HDR shows dark scene  
* QTBUG-123447 Incorrect log format in qaudioengine_pulse.cpp  
* QTBUG-120671 User control issues in QML Media Player with WASM  
* QTBUG-112316 wasm: declarative-camera fails to show camera  
* QTBUG-120622 Recorder sample app does not work as expected with  
WebAssembly  
* QTBUG-118072 MediaPlayer with VideoOutput doesn't autoplay  
* QTBUG-121172 [REG 6.5.5 - > 6.5.6] Declarative Camera: Black Screen  
Issue when Clicking "View" Button in Video Mode  
* QTBUG-122224 [Crash] The audiorecorder example crashes when selecting  
output and start recording  
* QTBUG-87969 MediaPlayer looses current position when playbackRate  
changes  
* QTBUG-123356 ERROR: Crash detected  
* QTBUG-123224 tst_qmediacapturesession crashes in  
CI(opensuse-15.5-host-asan)  
* QTBUG-123023 [Examples] Audio input devices list is not updated when  
connecting new device  
* QTBUG-123459 [gstreamer] player example does not update "Buffering"  
percentage  
* QTBUG-119535 [Boot2Qt] Switching between audio output devices while  
playing video causes the player app to freeze  
* QTBUG-123177 OpenSUSE crash in tst_QMediaCaptureSession with  
PulseAudio  
* QTBUG-96985 Video and MediaPlayer don't allow to use relative URLs  
* QTBUG-123931 With gstreamer as backend, playing mp4 file resulted in  
internal data stream error  
* QTBUG-124501 [gstreamer] media player does not play without outputs  
connected  
  
### qttools  
* QTBUG-123011 wrong xxx_lupdate_project.json is generated when no  
targets are specified in qt6_add_lupdate  
* QTBUG-123109 qdoc fails to compile with clang 18  
* QTBUG-122994 [Reg 6.6.1->6.6.2] Performance regression in  
qhelpcollection.cpp  
* QTBUG-123338 cmake translation handling not backwards compatible  
* QTBUG-123405 [REG 6.6 -> 6.7.0 RC] Translations were generated in the  
wrong folder  
* QTBUG-124188 [REG 6.6 -> 6.7] Automatic resource embedding path of  
qt_add_translations() has changed from Qt 6.6 to Qt 6.7  
* QTCREATORBUG-30625 [Reg 12 -> 13] Help: links to QML properties do not  
work anymore  
* QTBUG-123611 libclang15-based lupdate fails with MSVC2022  
  
### qttranslations  
* QTBUG-115634 qttranslations configure takes ages on CMake 3.27  
* QTBUG-115497 Typo in Qt Linguist  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-111748 [Turkish] Inconsistent translations  
  
### qtdoc  
* QTBUG-122444 Qt Dice Example: The control menu's lower half is cut off  
in landscape mode  
* QTBUG-123164 New example demos/osmbuildings not compiling on Android  
* QTBUG-124146 [demos/hangman] Clicking on the vowels button crashes the  
demo  
* QTBUG-122907 Show real time data for lighting viewer (or document that  
it is demo data)  
* QTBUG-123414 Coffee Machine Example calculates its initial size too  
big in case of two monitors on macOS  
* QTBUG-123305 Incorrect link  
* QTBUG-122605 Calqlatr example landscape grid buttons not showing  
symbols correctly  
* QTBUG-122682 "Porting to iOS" documentation only mentions qmake, not  
CMake  
* QTBUG-123714 [REG 6.7.0 beta3 -> beta4] demos/calqlatr not launching  
when building with qmake  
* QTBUG-122273 [MediaPlayerApp] The file names on the playlist in the  
app have specific format on Android  
* QTBUG-124707 Coffee Machine example coffee cup image breaks with Qt  
6.7.0 on Android  
* QTBUG-123543 Incomplete docs about the status of Linux on ARM desktops  
in 6.7  
* QTBUG-124518 The debian packages documentation has incorrect example  
  
### qtlocation  
* QTBUG-123112 GeoJson Viewer example doesn't show maps on Android  
  
### qtpositioning  
* QTBUG-119477 SatelliteInfo example crashes  
* QTBUG-115933 [QtPositioning] geoclue2 backend crashes randomly  
* QTBUG-121997 BUS ERROR in examples/positioning/satelliteinfo on  
aarch64  
  
### qtwayland  
* QTBUG-123007 Under Wayland Qt does not correctly handle key modifiers  
during key repeating  
* QTBUG-107858 qtwayland caches clipboard content  
* QTBUG-122412 Buggy rendering on RHEL 8 with 200% system scaling  
* QTBUG-97037 DragHandler / startSystemMove window move issue with QT6  
Webengine on Wayland  
* QTBUG-123489 Qt Wayland Client requires QtGui to be build with support  
for wayland  
* QTBUG-124304 [REG 6.7.1-> 6.7.0] no-gui (-DFEATURE_gui=OFF) build  
fails, qtspeech  
* QTBUG-100148 Hover state of QCombobox has not been reset  
* QTBUG-113404 Wayland: Gestures are not delivered to correct top level  
widget  
  
### qt3d  
* QTBUG-123483 Qt3D: Fix Stereo back buffer selection  
  
### qtimageformats  
* QTBUG-113349 [static linking] duplicate symbol with QIIOFHelper  
  
### qtserialbus  
* QTBUG-123012 vectorcan can not set the DataBitRateKey and the  
BitRateKey  
  
### qtwebsockets  
* QTBUG-123346 Expired (and near-expiring) certificates shipped with  
examples  
  
### qtwebengine  
* QTBUG-122997 The Spellcheck example doesn't work on macOS  
* QTBUG-123548 PDF multipage viewer converts a simple local filename in  
the cwd to an http url  
* QTBUG-122655 6.8.0 toplevel build fails on macOS, qtwebengine  
* QTBUG-120764 PDF Viewer Widget example search error  
* QTBUG-106565 The coordinate of QPdfSelection seems like to be wrong  
when pdf page contains non-displayable area  
* QTBUG-100630 PdfLinkModel don't give the right rect everytime  
* QTBUG-124527 qtwebengine integrations fail on 6.7: qt-testrunner.py  
ERROR: Full test run failed repeatedly, aborting!  
* QTBUG-124375 Qt Webengine spellcheck_buildflags.h not found on macOS  
* QTBUG-122916 Print preview: crash when pressing a resize button  
* QTBUG-124747 [REG 6.7.0->6.7.1] iOS examples not compiling  
* QTBUG-124790 QtWebengine 6.8 (dev) doesn't render with basic html  
files  
* QTBUG-124635 [REG 6.7.0->6.7.1] WebEngine does not render anything on  
embedded  
* QTBUG-120414 Recipe Browser example crashes  
* QTBUG-122699 Failed DCHECK in v8 when watching livestream  
  
### qtdatavis3d  
* QTBUG-122209 Manual testing - "Cannot override Final property" error  
in qmldynamicdata  
  
### qtvirtualkeyboard  
* QTBUG-80663 inputpanel::tst_plugin::test_zhuyinInputMethod is  
extremely unstable  
  
### qtquick3d  
* QTBUG-122722 qt6-declarative/quick3d build-time race condition around  
qmlcachegen  
* QTBUG-123316 QQuickGeometry JointSemantic does not work with F32Type  
* QTBUG-111709 FAIL!  : tst_Input::singleTap2D  
* QTBUG-119196 Bad rendering in Qt Quick 3D - Particles 3D Testbed  
example  
  
### qt5compat  
* QTBUG-122795 Incompatibility in QTextCodec between Qt5 and Qt6 (lack  
of BOM)  
  
### qtopcua  
* QTBUG-123094 Dependency update on qt/qtopcua failed in 6.7.0  
  
### qtquick3dphysics  
* QTBUG-123888 discrepancy between PTHREAD_POOL_SIZE and  
QThreadPrivate::idealThreadCount  
  
### qtgrpc  
* QTBUG-123345 Qt GRPC HTTP2 regression  
* QTBUG-123996 QGrpcReply is never deleted and causes errorOccurred  
after successful response  
* QTBUG-123400 QtProtobuf: cannot use Qt reserved names as fields  
  
### qtgraphs  
* QTBUG-122600 Manual testing - tst_volumetrictest is missing a file  
* QTBUG-121210 Axis Y line size not updating correctly  
* QTBUG-123382 Crash on Axis Formatting  
* QTBUG-123226 Custom item updating is incorrect  
* QTBUG-122943 Public GraphPositionQuery methods are broken  
* QTBUG-123624 Graph Gallery example crashes  
* QTBUG-123630 Selected point in scatter graph is resized or stretched  
* QTBUG-123433 Axis Handling example crashes with index out of range  
error  
* QTBUG-123418 [Reg 6.6 -> 6.7] Q3DSurface and Q3DScatter crash in  
removeSeries  
* QTBUG-121993 AxisLabel and GridLine are Components  
* QTBUG-123984 [REG] Returning from slice view does not work if slice  
mode is changed while in the slice view  
* QTBUG-113199 Changing a theme or color styles between object and range  
gradient accumulates memory in scatter and bars  
  
### qtapplicationmanager (Commercial only)  
* QTBUG-123088  Qt Application Manager examples fail to scan  
* QTBUG-123420 Clicking desktop icons in Animated Windows System UI  
example may not always close application windows  
* QTBUG-123796 qtapplicationmanager examples not compiling with linux on  
arm binaries  
  
### qtinterfaceframework (Commercial only)  
* QTBUG-115221 Add support for WebAssembly in the autotests  
  
Known Issues  
------------  
  
* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-6.7/supported-platforms.html  
* RTA reported issues from Qt 6.7  
https://bugreports.qt.io/issues/?filter=25756  
* See Qt 6.7 known issues from:  
https://wiki.qt.io/Qt_6.7_Known_Issues  
* Qt 6.7.1 Open issues in Jira:  
https://bugreports.qt.io/issues/?filter=26028  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Amir Masoud Abdol  
Cristian Adam  
Laszlo Agocs  
Dilek Akcay  
Konsta Alajärvi  
Anu Aliyas  
Albert Astals Cid  
Even Oscar Andersen  
Soheil Armin  
Vladimir Belyavsky  
Nicholas Bennett  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
Tatiana Borisova  
Joerg Bornemann  
Rym Bouabid  
Assam Boudjelthia  
Mark Brand  
Kai Uwe Broulik  
Michael Brüning  
Oswald Buddenhagen  
Alexander Busse  
Olivier De Cannière  
Kaloyan Chehlarski  
Ed Cooke  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Oliver Dawes  
Pavel Dubsky  
Artem Dyomin  
Alexey Edelev  
David Edmundson  
Oliver Eftevaag  
Christian Ehrlicher  
Hatem ElKharashy  
Andreas Eliasson  
David Faure  
Ilya Fedin  
Nicolas Fella  
Robert Griebl  
Jan Grulich  
Kaj Grönholm  
Richard Moe Gustavsen  
Lucie Gérard  
Mikko Hallamaa  
Jøger Hansegård  
Inkamari Harjula  
Thomas Hartmann  
Jani Heikkinen  
Tero Heikkinen  
Moss Heim  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Dominik Holland  
Marc Hüskens  
Allan Sandfeld Jensen  
Tim Jenssen  
Jonas Karlsson  
Timothée Keller  
Ahmed El Khazari  
Marius Kittler  
Friedemann Kleint  
Andre Klitzing  
Jarek Kobus  
Sze Howe Koh  
Jarkko Koivikko  
Tomi Korpipaa  
Fabian Kosmale  
Volker Krause  
Mike Krus  
Jaroslaw Kubik  
Santhosh Kumar  
Keith Kyzivat  
Kai Köhne  
Inho Lee  
Frédéric Lefebvre  
Chris Lerner  
Wladimir Leuschner  
Thiago Macieira  
Sergio Martins  
Safiyyah Moosa  
Bartlomiej Moskal  
Marc Mutz  
Antti Määttä  
Jithin Nair  
Martin Negyokru  
Andy Nichols  
Mårten Nordheim  
Dennis Oberst  
Tinja Paavoseppä  
Ekaterine Papava  
Kwanghyo Park  
Samuli Piippo  
Timur Pocheptsov  
Milla Pohjanheimo  
Lauri Pohjanheimo  
Michał Policht  
Rami Potinkara  
Lorn Potter  
Sakaria Pouke  
MohammadHossein Qanbari  
Liang Qi  
Matthias Rauter  
David Redondo  
Topi Reinio  
Shawn Rutledge  
Toni Saario  
Ahmad Samir  
Lars Schmertmann  
Sami Shalayel  
Andy Shaw  
Venugopal Shivashankar  
Ivan Solovev  
Krzysztof Sommerfeld  
Axel Spoerl  
Stefan Steinwasser  
Martin Storsjö  
Tarja Sundqvist  
Lars Sutterud  
Jan Arve Sæther  
Morten Sørvig  
Sadegh Taghavi  
Marcus Tillmanns  
Paul Olav Tvete  
Sami Varanka  
Peter Varga  
Doris Verria  
Tor Arne Vestbø  
Jannis Voelker  
Juha Vuolle  
Olli Vuolteenaho  
Jaishree Vyas  
Gary Wang  
Bernd Weimer  
Edward Welbourne  
Fushan Wen  
Paul Wicking  
Piotr Wierciński  
Oliver Wolff  
Lu YaNing  
Vlad Zahorodnii  
Yifan Zhu  
Eike Ziller  
Fredrik Ålund  
