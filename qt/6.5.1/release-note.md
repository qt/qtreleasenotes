Release note  
============  
  
Qt 6.5.1 release is a patch release made on the top of Qt 6.5.0.  
As a patch release, Qt 6.5.1 does not add any new functionality but provides  
bug fixes and other improvements and maintains both forward and backward  
compatibility (source and binary) with Qt 6.5.0.  

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
* bc070591c2 QMessageAuthenticationCode: remove lazy initialization of  
messageHash  
No longer delays processing of the key to the first setData() or  
result() call. While passing a default-constructed key to the  
constructor and then calling setKey() continues to work, for optimal  
performance, we suggest to pass the actual key as a constructor argument  
and call setKey() only to change the key.  
  
* 1ac4375135 QErrorMessage: Reset 'again' check box between each error  
message  
QErrorMessage will now reset the check box for showing a message again  
for each new message shown, as each individual message has its own  
suppression state.  
  
* 7508dad289 QFSFileEngine: fix overflow bug when using lseek64  
Fixed a bug where opening a file in append mode may fail if the file  
size was bigger than INT_MAX.  
  
* fa34315a5a CMake: Add NO_COMPILER_RUNTIME to deploy script macros  
Added the option NO_COMPILER_RUNTIME to qt_generate_deploy_app_script.  
  
* b006c2437a SQLite: Update SQLite to v3.41.1  
Updated SQLite to v3.41.1  
  
* b105e128db QProcess: reimplement systemEnvironment() using  
QProcessEnvironment  
Fixed a bug that would cause systemEnvironment() to produce corrupted  
entries (mojibake) on Windows if the environment contains characters  
outside of the ANSI character set.  
  
* d3bc8c79bb QTimer: fix new-style slot invocation for receiver in  
another thread  
Fixed a bug that caused slots connected to single-slot timers using the  
new-style connection mechanism to be delivered in the wrong thread.  
  
* b9d25848f0 Update license specification for PCRE2  
Clarifying license of PCRE2 to be BSD-3-Clause with advertisement  
exception for binary-like packages.  
  
* 766d5daf3b SQLite: Update SQLite to v3.41.2  
Updated SQLite to v3.41.2  
  
* 72487c52fb QMultiHash: fix missing update to m_size  
to not be counted, resulting in a hash map with an incorrect element  
count and which could cause an assertion failure depending on how the  
hash was later mutated.  
  
* b87883951e QPluginLoader: don't instantiante multiple, identical  
instances  
staticInstances() will not call duplicated registrations of the same  
instantiation function, which can only happen as a result of duplicated  
Q_IMPORT_PLUGIN for the same plugin name.  
  
* dd8b648e69 Fix accessibility on XCB when running as root  
On XCB applications running as root are now accessible.  
  
* 92b56cab18 CMake: Store unsanitized plugin type names in module .json  
files  
The module information JSON files now contain the unsanitized plugin  
types of a module, e.g. wayland-decoration-client instead of  
wayland_decoration_client. Consumers of the module information file must  
sanitize plugin types themselves if necessary.  
  
* e53911842a win: Fix default fallback font for some languages  
Fixed an issue querying a default font for certain languages not  
supported by the primary system font.  
  
* 709e603664 Windeployqt: Add a check for LLVM-MinGW runtimes  
Windeployqt now supports LLVM-MingGW runtimes.  
  
* 55aee86975 QDnsLookup/Unix: make sure we don't overflow the buffer  
Fixed a bug that could cause a buffer overflow in Unix systems while  
parsing corrupt, malicious, or truncated replies.  
  
### qtsvg  
* 2570796 Don't rasterize gigantic shapes  
Unreasonably large shapes are now ignored in SVG files to avoid  
stalling the application. The check can be disabled by setting  
QT_SVG_DISABLE_SIZE_LIMIT=1 in the environment.  
  
* d40f1c6 QSvgFont: Initialize used member, remove unused  
Fixed undefined behavior from using uninitialized variable.  
  
### qtdeclarative  
* 50cff47d14 CMake: Add NO_COMPILER_RUNTIME to  
qt_generate_deploy_qml_app_script  
Added the option NO_COMPILER_RUNTIME to  
qt_generate_deploy_qml_app_script.  
  
* 8fae0aa4ae QQuickItemView: Skip instantiating delegates if size is 0  
If a ListView has size zero, it won't instantiate any delegates until  
its size becomes non-zero.  
  
* 466e17a9ae Fix StackLayout to keep the current visible item after  
insert/removal  
StackLayout will now update currentIndex if an Item is inserted or  
removed at an index less than or equal to the current index.  
  
### qttools  
* 54a77b524 lupdate: Handle C++ string literals  
lupdate now supports prefixed string literals like u"foo".  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-111416 [REG 6.3.2->6.4.2] Repeated QPainter::drawPixmapFragments  
calls draw images at wrong positions for QOpenGLWidget  
* QTBUG-111698 Build fails with -march=amdfam10  
* QTBUG-110898 Window disappears when monitor is disconnected  
* QTBUG-111524 [REG 6.4 -> 6.5-beta3] Exec'd QMessageBoxes from QMenus  
return immediately on macOS  
* QTBUG-111774 FTBFS: qtbase -DQT_FORCE_FIND_TOOLS=ON fails on CMake:  
Some (but not all) targets in this export set were already defined.  
* QTBUG-111803 Native QMessageBox on macOS doesn't show check box  
* QTBUG-111735 QPropertyAlias::addNotifier() is ill-formed  
* QTBUG-111397 QNetworkAccessManager hangs indefinitely when loading a  
corrupted cache file  
* QTBUG-111867 QVariant::operator== between QVariant(0) and QString  
* QTBUG-111443 macOS/iOS: "Detected system locale encoding (US-ASCII,  
locale "C") is not UTF-8"  
* QTBUG-111267 markDirty() does not exist for Q_OBJECT_COMPUTED_PROPERTY  
* QTBUG-96616 QODBC-DB2 Unicode support is not recognised  
* QTBUG-102958 ODBC Oracle wrong detection for unicode  
* QTBUG-102107 [REG 5.15.2 => 6.2.3] QMenuBar can crash on Mac  
* QTBUG-106369 Crash when closing modal window with macOS on-screen  
keyboard  
* QTBUG-111183 Qt crash on macOS when using keyboard viewer  
* QTBUG-105250 Access NULL m_platformWindow in qnsview_complextext.mm  
* QTBUG-111884 FTBFS: qtbase can't be built in static mode  
* QTBUG-111027 Adding asset pack to package crashes androiddeployqt  
* QTBUG-8682 QPlainTextEdit: When scrolling vertically using the arrow  
keys then the valueChanged() signal is not emitted from the vertical  
scrollbar  
* QTBUG-25365 ValueChanged() signal is not emitted by QScrollBar when  
Page Up/Dn is Hit in  QPlainTextEdit having scrollbar  
* QTBUG-85544 androiddeployqt fails with message that neither  
libqtforandroid.so or libqtforandroidGL.so are included  
* QTBUG-97636 Qtbase for Android with examples fails to build  
* QTBUG-83997 Can't deploy a simple console application  
* QTBUG-93185 Android platform plugin not linked when using only QtCore  
* QTBUG-108050 Depth Buffer not working in 5.15.2  
* QTBUG-111753 Manual tests try to use the auto test runner instead of  
wasm shell  
* QTBUG-110485 Empty ApplicationWindow prints a warning  
* QTBUG-111798 Crash on macOS when showing QMainWindow with  
"Preferences" menu item in "Edit" menu  
* QTBUG-111742 QColordialog - cannot input/paste values without #  
(pound) symbol  
* QTBUG-111869 irritating gotcha and crash in QCompleter popup()  
* QTBUG-107842 Style Plugin Example has no CMake docs  
* QTBUG-109227 Style Plugin Example is broken  
* QTBUG-111916 Crash upon copy/paste on Mac in plugin situation  
* QTBUG-68884 Missing isNull check in QOpenGLTexture (crash in driver)  
* QTBUG-109971 Crash during window resize when using QQuickWidget  
* QTBUG-112174 QDebug operator<<(QDebug debug, const QInputDevice  
*device) crashes if device is null  
* QTBUG-56214 Qt Creator stops responding to mouse wheel scrolling  
* QTBUG-98720 Regression: Mouse wheel scrolling randomly stops working  
on Linux.  
* QTBUG-99331 Mouse-wheel scrolling stops working when mouse is  
disconnected and reconnected  
* QTBUG-112141 [Qt6 regression] Scrollwheel doesn't work after KVM  
switch  
* QTBUG-104878 xcb wacom support gets confused about device instances  
* QTBUG-107139 Webassembly cannot input Chinese  
* QTBUG-104905 Window modal not blocking ancestor window interaction on  
Mac  
* QTBUG-112205 QMetaType id of custom QObject subclass unknown prior to  
fetching id from QVariant  
* QTBUG-73260 webassembly: QDialog Transparent background  
* QTBUG-112222 loss of data warnings compiling QTaggedPointer  
* QTBUG-107545 Taking a second future from QPromise overwrites the first  
one  
* QTBUG-106099 QCombobox dropdown not displayed on correct monitor in  
multimonitor setup  
* QTBUG-104781 Tooltip Example: Wrong object is moved when performing  
dragging on another one  
* QTBUG-111102 [REG 6.4.0 -> 6.4.1] QT_WIDGETS_HIGHDPI_DOWNSCALE is  
broken  
* QTBUG-107814 Reg:[6.3->6.4]QOpenGLWidget tries to render duplicate  
controls  
* QTBUG-74478 mouse flicking on qtabwidget non-current tab causes  
segfault  
* QTBUG-108614 QComboBox will emit currentIndexChanged when the index  
isn't changed  
* QTBUG-103498 wasm: touch app cannot move app with dialog titlebar  
* QTBUG-86272 wasm: Dead keys don't work on Linux  
* QTBUG-112162 QTimer::singleShot() can call receiver in wrong thread  
* QTBUG-112458 Failed to generate docs  
* QTBUG-56064 QStandardItem:: setEnabled() has no effect on QComboBox  
items when SH_ComboBox_UseNativePopup is applied  
* QTBUG-105109 Example code related to QHash::erase() fails clazy  
* QTBUG-111417 HTTP/2 request does not finish until closed by remote  
host  
* QTBUG-109120 [iOS] Problems with Native Photo Picker  
* QTBUG-112478 WASM: default network connections broken due to changed  
default  
* QTBUG-112534 QMultiHash functions (size, isEmpty) return unexpected  
values  
* QTBUG-110019 Address Book example crashes on exit  
* QTBUG-97571 Text in column header is not elided for QHeaderView  
* QTBUG-112018 syncqt fails 6.5.0 build  
* QTBUG-111163 [6.5] Parallel builds failing in Docker container  
* QTBUG-112527 QPermission incorrectly checks and requests permissions  
on Android  
* QTBUG-112465 androiddeployqt fail on Android build platform:  
android-33-ext5  
* QTBUG-112611 Can not build Qt 6.5.0 with ClangCl and MSVC 2022 17.5  
due to QDateTime issue  
* QTBUG-100128 QListWidget/QListView: item widget disappears when item  
is dragged and dropped on itself  
* QTBUG-102745 Static plugin loaded twice  
* QTBUG-112648 Extra semicolon warnings in qtablewidget.h, qimage.h and  
qdebug.h  
* QTBUG-96877 Qt6 won't render into cutout area (regression)  
* QTBUG-112656 qcocoanativeinterface.mm:4:10: fatal error:  
'QtGui/private/qopenglcontext_p.h' file not found  
* QTBUG-112204 windeployqt error when creating translations  
* QTBUG-112300 Shared plugin examples do not work  
* QTBUG-112667 qmake QMAKE_BUNDLE not work for mac  
* QTBUG-112668 qmake QMAKE_APPLICATION_BUNDLE_NAME not work for mac  
* QTBUG-111984 Connectivity dependency not installed in 6.4.3  
* QTBUG-110632 Assertion failure in qqmltreemodeltotablemodel.cpp when  
adding/removing files from directory watched by QFileSystemModel used by  
TreeView  
* QTBUG-112257 QIcon::fromTheme very slow for repeated failed lookups  
* QTBUG-111538 QDockAreaLayout::updateSeparatorWidgets crash with null  
pointer dereference sometime after restoring state due to recursion into  
QMainWindowLayout::setGeometry causing corruption of separatorWidgets  
* QTBUG-109763 tst_QAccessibility::focusChild() with QtWayland failed on  
Ubuntu 22.04, GNOME  
* QTBUG-103792 TextField inside a multi sampling layer breaks rendering  
with OpenGL RHI backend  
* QTBUG-34337 Application hangs when enabling a11y for QTableView with  
large number (100k+) rows  
* QTBUG-112317 [REG 6.4.2 -> 6.5] can't NOT install qmltooling anymore  
* QTBUG-105921 Qt: OpenGL does not seem to work on Wayland? (NVIDIA  
515.65.01)  
* QTBUG-112820 Undefined symbols for msgSend stubs when linking with  
Xcode < 14  
* QTBUG-104709 [REG. 6.2->6.3] macOS: Default Edit menu entries shown  
twice  
* QTBUG-79565 Mac: Emoji Picker shortcut (Ctrl + Cmd + Space) doesn't  
work in QML TextEdit  
* QTBUG-112759 Application crashes on QAbstractButton::setChecked if  
button destroyed in toggled signal  
* QTBUG-112756 GL_INVALID_OPERATION in unsupported function called  
(unsupported extension or deprecated function?)  
* QTBUG-110408 [Win] Yet another unhandled exception on  
QNetworkInformation::load()  
* QTBUG-43674 Accessibility is not enabled when running as root  
* QTBUG-112019 QSpinBox/QDoubleSpinBox up/down arrow size incorrect on  
screen with non-integer device pixel ratio  
* QTBUG-112861 Regression in spinbox PlusMinus symbol rendering  
* QTBUG-112448 windeployqt for mingw copies wrong mingw dlls  
* QTBUG-112743 Infinite warnings on failure to load .qrc resource file  
* QTBUG-112252 QSS: QSizeGrip { image: } shows image only when in  
bottom-right corner  
* QTBUG-106701 Crash with any QML app on external display with iPadOS  
16.1 on M1 iPad  
* QTBUG-112872 Module JSON files have wrong plugin_type entries for  
Wayland plugins  
* QTBUG-112953 QTextDocument::contentsChange is emitted several times  
when iBus is on  
* QTBUG-112473 Background of splash screen of QtQuick example Window and  
Screen is not transparent  
* QTBUG-112537 A Window's background cannot be semitransparent anymore  
* QTBUG-111969 Qt6 semi transparent bug in Windows 11  
* QTBUG-112524 The Color Property of Window is no Effect  
* QTBUG-112326 [REG: 5->6] Cannot add items with user data to QComboBox  
that has QSortFilterProxyModel  
* QTBUG-111854 The order fonts are loaded in, can artificially reduce  
their style variants  
* QTBUG-99990 windows: Painting an image with DPR >1.0  to a QPrinter  
does not produce correct result  
* QTBUG-110080 Using FileDialog or FolderDialog makes the mouse cursor  
disappear  
* QTBUG-111978 Setting QComboBox tab order after setting setEditable  
results in incorrect behavior  
* QTBUG-111200 [REG: 5->6] QDomDocument now drops standalone attribute  
* QTBUG-112884 StringLiterals documentation references wrong header  
* QTBUG-109640 QFrame no physical pixel rounding for frame width on  
screen with non-integer device pixel ratio  
* QTBUG-113138 Copyright statements and license identifiers appear in  
the HTML  
* QTBUG-109429 Wrong window and/or content size after screen scaling  
change  
* QTBUG-113127 It is qt_gl_read_framebuffer_rgba8 that cause a crash  
which show info "nvoglv32!DrvPresentBuffers+0xf71ab" at the top of stack  
nvoglv32.dll  
* QTBUG-112881 QFileDialog::saveFileContent() not working on Chrome  
* QTBUG-112814 The window restore geometry is not correct  
* QTBUG-112761 ctf_array produce an error while compiling with lttng  
enabled  
* QTBUG-113140 Resizing a QTabBar resets the scroll position  
* QTBUG-112816 REG [6.5.0->6.5.1] corelib/platform/androidnotifier not  
compiling on Android  
* QTBUG-103514 Possible crash in imagescaling example.  
* QTBUG-113147 Documentation of Q_ARG and Q_RETURN_ARG: return value  
* QTBUG-112899 QMacStyle setupSlider leaks memory painting QSlider  
* QTBUG-98093 QSlider is broken in MacOS Monterey  
* QTBUG-113216 The example for QT_DEPLOY_TRANSLATIONS_DIR doesn't  
actually mention that variable  
* QTBUG-113227 ABI issue with QVariant and metatypes from Qt < 6.5  
* QTBUG-112922 Focus lost if mouse is hover over QGraphicsView  
* QDS-9687 Examples cannot be downloaded  
* QTBUG-112334 False doc for void QList::resize(qsizetype size)  
* QTBUG-112697 QMessageBox return immediately on macOS if called from  
MenuBar and after a modal dialog [REG]  
* QTBUG-113376 [REG 6.5.0 -> 6.5.1] QTabBar: Jumping non-expandable tabs  
* QTBUG-113295 Failure to build Qt 6.5.0 from source on macOS  
* QTBUG-113311 [REG] Mac checkable menu stays on parent click (works in  
6.4.3 + 6.4.0b2)  
* QTBUG-113337 [REG 6.4.3 -> 6.5.0] Integer overflow in qfixed_p.h when  
rendering SVG image on the minimal plugin  
* QTBUG-113209 Qt::ItemNeverHasChildren prevents itemChanged() from  
being fired  
* QTBUG-112885 Qt6AndroidMacros generates invalid android's deployment-  
settings.json  
* QTBUG-108094 Image color changing while opening in QtQuick  
* QTBUG-104595 tst_QScreen::grabWindow XWAYLAND fails with Ubuntu 22.04  
* QTBUG-110356 Building Permissions example for debug with qmake on  
macOS fails  
* QTBUG-111625 COM library crash exposed when using TBB scalable memory  
allocation  
* QTBUG-105140 [REG] default constuctor requirement for meta type  
(QVariant) breaks webengine api  
* QTBUG-111598 Implement get/get_if for QVariant to make it nicer for  
non-default constructible types  
* QTBUG-111772 3D textures behave weird with some Vulkan implementations  
* QTBUG-111741 qt_deploy_runtime_dependencies() doesn't install project  
linked libraries & adds undocumented vcredist installer  
* QTBUG-111262 Review <ctype.h> uses [Qt]  
* QTBUG-99125 windeployqt does not deploy qml stuff in a call with  
multiple applications  
* QTBUG-112275 tst_QImageReader::setClipRect() and setScaledClipRect()  
"SVG: rect" and "SVGZ: rect" with QtWayland failed on Ubuntu 22.04 GNOME  
* QTBUG-63481 tst_QSslSocket_onDemandCertificates_member::onDemandRootCe  
rtLoadingMemberMethods tests fail in the CI  
* QTBUG-94871 Qt should subscribe to dbus system tray and dbus menu  
service appearing/disappearing  
* QTBUG-94232 androiddeployqt is broken when manually defining  
dependencies  
* QTBUG-100563 Invalid style override breaks Qt Quick Control  
applications (incl. crash)  
* QTBUG-103257 tst_qquickcanvasitem crashes on Android  
* QTBUG-41043 tst_qquickcanvasitem tends to fail on CI  
* QTBUG-78648 RHI: Does not work with Windows10 inside VMWare (Fusion)  
* QTBUG-97642 When a mask is set on a widget after being moved to a  
different display with a different DPR then it can end up not being set  
correctly because it is seen as the same as the previous one  
* QTBUG-109779 tst_QGraphicsEffect::draw() with QtWayland failed on  
Ubuntu 22.04, GNOME  
* QTBUG-111304 wasm: Cube example does not work  
* QTBUG-111503 QXkbCommon: No Qt::KeypadModifier in QKeyEvents in  
QtWaylandCompositor  
* QTBUG-112896 gtk3 platformtheme returns the font of GtkFixed widget  
instead of monospace font  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-112965 Dark mode isn't applied  
* QTBUG-113036 Windows: Prevent Vistastyle from changing into darkmode  
at runtime  
* QTBUG-113116 Documentation typos, errors and improvements  
* QTBUG-113161 tracegen creates duplicate argument names for some types  
for lttng  
* QTBUG-104930 QLocale shows German text for "en_DE"  
* QTBUG-53085 Reg[5.6.0-5.6.1] "Start Dictation..." and "Emoji &  
Symbols" are missing in Edit menu in Application  
* QTBUG-112747 Unable to run configure.bat  
* QTBUG-35608 Flickable speed and deceleration does not scale with pixel  
density  
* QTBUG-35609 Flickable speed and deceleration are not easily  
customisable  
* QTBUG-97055 QQC2 Flickable scrolling is not linear with clicky wheels  
on Qt 6.2.0  
* QTBUG-111330 error: Not a signal or slot declaration in code generated  
by qt_add_dbus_interface  
  
### qtsvg  
* QTBUG-111850 [REG 6.2.2 -> 6.2.3] Loading particular svg file takes  
far too long  
  
### qtdeclarative  
* QTBUG-109816 Crash when accessing enums defined in QML_SINGLETON class  
* QTBUG-108896 [REG 6.2.4-6.3.2] Using PinchHandler for Flickable's  
child makes the Flickable transparent for touch events  
* QTBUG-111042 QML cache files are re-generated all the time when they  
contain inline components  
* QTBUG-111511 Object destructuring breaks qmlformat  
* QTBUG-111491 Dark Title on Dark Windows 11 when running native Windows  
Style  
* QTBUG-111359 Removing a button from button group does not clear  
ButtonGroup.group  
* QTBUG-111515 New Material 3 TextField placeholder text does not work  
with smaller heights  
* QTBUG-111557 A left button click followed by a right button click  
triggers a  doubleTabbed event  
* QTBUG-111559 Loader with States creates 2 children instead of 1  
* QTBUG-111634 CalendarModel::indexOf() returns wrong value when model  
month starts from February  
* QTBUG-111230 missing export macro for QQuickWheelEvent  
* QTBUG-111227 WASM: 'Failed to build graphics pipeline state' error  
when using QtQuick Particles  
* QTBUG-74020 PointHandler documentation examples refer to TapHandler  
not PointHandler  
* QTBUG-106878 PointHandler documentation examples refer to TapHandler  
not PointHandler  
* QTBUG-111766 qml issues in Effect Maker  
* QTBUG-111857 tst_snippets verify:qtquickcontrols-material-attributes  
fails on macOS  
* QTBUG-106968 QSGSoftwareRenderContext textures leak  
* QTBUG-111935 Qt V4 JIT engine generates bad JIT code on ARM64 (and  
potentially all arches)  
* QTBUG-111881 Incorrect example in  
QQmlApplicationEngine::objectCreationFailed documentation  
* QTBUG-111481 It is really hard to find the new Qt 6.5 qml MultiEffect  
in the docs  
* QTBUG-95807 QtQuick: Missing headers or documentation bug  
* QTBUG-111986 qmlsc generates invalid code  
* QTBUG-112159 Drawing bug with Material 3 Drawer  
* QTBUG-111995 Crash in QRhiImplementation::textureFormatInfo when using  
ColorAnimation on text containing emojis  
* QTBUG-111809 Qml basic type string is not well documented  
* QTBUG-111918 Null Reference Errors on Deconstruction of nested QML  
QtObjects  
* QTBUG-112322 BorderImage docs: description of border property is in a  
confusing place  
* QTBUG-25244 SVG: Unsupported Image Format when using BorderImage  
* QTBUG-112354 AnchorChanges in states are not released  
* QTBUG-106677 "Back" button breaks UI of Coffee Machine Example  
* QTBUG-108390 Code snippet for custom Dial in the document is not  
working as expected  
* QTBUG-91425 DelegateModel: Crash when DelegateModelGroup is used for  
delegate geometry and model is cleared  
* QTBUG-98402 tst_qquickimage::mirror() is failing on macOS 12  
* QTBUG-108596 [REG 6.3.2->6.4.0] TableView consumes mouse press/click  
events  
* QTBUG-111800 TapHandler.exclusiveSignals: you can only tap once if  
m_doubleTapTimer is used  
* QTBUG-111220 PinchHandler.persistentTranslation has inconsistent  
meaning with native pinch gesture  
* QTBUG-103257 tst_qquickcanvasitem crashes on Android  
* QTBUG-41043 tst_qquickcanvasitem tends to fail on CI  
* QTBUG-112712 [6.5] "QtQuick" dependency on `QmlMeta`  
* QTBUG-95940 tst_qquicktextinput is flaky on OpenSUSE  
* QTBUG-111231 qmlformat does not preserve whitespace in comments and  
whitespace following header comments  
* QTBUG-111792 Dynamically changing the Items in a ColumnLayout while  
resizing leads to crash  
* QTBUG-111902 [Reg 5.15 -> 6.4.2] Loader with StackLayout and Repeater  
displays an incorrect index  
* QTBUG-107037 MultiPointTouchArea with enabled:false blocks events to  
MouseArea  
* QTBUG-108226 quickwidget example crash in QAccessibleQuickWindow /  
QMacAccessibilityElement  
* QTBUG-110592 [REG: 6.4->6.5.0-beta1] Quick tests now open a window  
* QTBUG-111504 Text loses selection when releasing long-press on Android  
text input  
* QTBUG-110850 selectAll does nothing in onFocusChanged triggered by  
touch input  
* QTBUG-112348 Make the options which can be used to control Qt Quick  
Compiler easier to find  
* QTBUG-112838 'visible' of QQuickItem cannot be set to 'true' again  
after being set to 'false' once.  
* QTBUG-109721 Non-Editable ComboBox wrongly propagates KeyEvent that  
has already been accepted  
* QTBUG-84920 StackView's depth is not updating after clear()  
* QTBUG-101985 ListView does not relayout its children when section  
delegate height changes  
* QTBUG-100002 QQuickListView: No layout update is triggered when a  
section delegate has its geometry changed.  
* QTBUG-112860 Binding doesn't seem to be released on changed 'when'  
property  
* QTBUG-106529 QtQuick.Shapes docs lacks mentionning how to make it  
smooth  
* QTBUG-112463 Very pixelated edges of text in PathText  
* QTBUG-110625 QML ListView creating delegate instances for ALL model  
entries  
* QTBUG-89568 Binding delegate height to ListView height causes  
delegates to be created unnecessarily  
* QTBUG-51773 When the height of a delegate is bound to the height of a  
ListView with a large model count, the application is blocked for  
several seconds  
* QTBUG-110114 Qt Quick Controls Button: Unable to override  
Accessible.role  
* QTBUG-70939 QML ComboBox popup menu doesn't respect scaling  
* QTBUG-112434 [Regr: 6.3.1->6.3.2] MouseArea stays pressed after double  
click on touch screen  
* QTBUG-109393 [Regr: 6.3.1->6.3.2] iPad: DoubleClicking in MouseArea +  
Popup breaks  
* QTBUG-110718 QML_ATTACHED in QQuickAttachedPropertyPropagator  
* QTBUG-112691 StackLayout Visible Item Does Not Update During Inserts  
* QTBUG-111322 HoverHandler example is broken in  
qtdeclarative/examples/quick/pointerhandlers  
* QTBUG-113226 Flickable emit flickStarted even though the child is  
processing the pinch gesture  
* QTBUG-112924 movementStarted/movementEnded signals are not emitted,  
the flickStarted/flickEnded signals with flick behavior still occur.  
* QTBUG-113172 Qt 6.5 Material TextField placeholder breaks with  
alignment  
* QTBUG-112945 QML RangeSlider does not work well on touch screen  
* QTBUG-95395 Code snippets for HoverHandler show TapHandler  
* QTBUG-70397 TapHandler fires for all overlapping items  
* QTBUG-73262 it's confusing that TapHandler.gesturePolicy affects event  
propagation  
* QTBUG-100534 TapHandler doesn't stop propagation  
* QTBUG-107239 DragHandler propagates tap event through Flickable to  
underlying TapHandler  
* QTBUG-111310 \image tag breaks \value block  
* QTBUG-111532 qmlsc when enabled gives many errors/warnings  
* QTBUG-65088 TapHandler: detecting double-clicks is not declarative  
enough  
* QTBUG-107264 TapHandler.singleTapped is emitted immediately before we  
know whether a double-tap will occur  
* QTBUG-111741 qt_deploy_runtime_dependencies() doesn't install project  
linked libraries & adds undocumented vcredist installer  
* QTBUG-101488 tst_QQuickFileDialogImpl is flaky  
* QDS-8545 Buttons in default style do not have the correct implicit  
size in the form editor  
* QTBUG-111570 ASSERT: "newInstance != d->animationInstance" in file  
qquickbehavior.cpp  
* QTBUG-111595 Qml Menu, inherited property "opened" is not working  
* QTBUG-112696 QQuickWidget::focusPreserved test fails with RHI warnings  
* QTBUG-106118 Changing contentItem to ScrollView breaks scrollbar  
visibility  
* QTBUG-111012 [Reg 5.15 -> 6.x] QSGGeometry::DrawLineLoop is no longer  
supported  
* QTBUG-112650 TextArea decorator not working as intended  
* QTBUG-104323 Not possible to close a modal ComboBox popup by clicking  
on the ComboBox  
* QTBUG-113116 Documentation typos, errors and improvements  
* QTBUG-113138 Copyright statements and license identifiers appear in  
the HTML  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-111014 QTest backslash escape issue  
* QTBUG-50161 ProgressBar and BusyIndicator are very CPU intensive  
  
### qtactiveqt  
* QTBUG-111718 QAxScript: Changed value of ByRef parameter is not  
returned  
  
### qtmultimedia  
* QTBUG-110995 Qt Multimedia Video not working on Nvidia Xavier and Orin  
platforms  
* QTBUG-110317 Camera active state does not work as expected  
* QTBUG-110868 QML Video crashes on macOS when lazy-loaded  
* QTBUG-110812 Camera not working when using OpenGL Renderer (macOS,  
iOS)  
* QTBUG-111900 FFMPEG library incompatibility on desktop builds  
* QTBUG-111944 wasm: QtMultimedia asks for mic and camera input for  
playing videos  
* QTBUG-98102 [macOS] Specific video can't be played  
* QTBUG-112315 wasm: multimedia examples do not build with qmake  
* QTBUG-110466 Combo Boxes in QML Video Recorder example don't populate  
* QTBUG-110131 QML Camera unloading crash on iOS  
* QTBUG-112352 Crash when destroying page with camera linked to  
VideoOutput  
* QTBUG-109167 QSoundEffect is stuck in Loading state  
* QTBUG-110005 windows: Crash if using asynchronous IO device as a media  
source  
* QTBUG-112601 Spatial Audio is marked as Tech Preview  
* QTBUG-108083 Video color change while playing in QML MediaPlayer  
* QTBUG-113008 REG [6.5.0->6.5.1] camera example not compiling on  
Android  
* QTBUG-112832 Building Qt 6.5.0 for Windows doesn't include QML  
* QTBUG-113286 [REG 6.4.3-6.5.0] [darwin] QMediaPlayer produces invalid  
frames on custom QVideoSink  
* QTBUG-112454 Android-Multimedia know issue with pixel format need to  
be documented  
* QTBUG-111567 masOS audio deadlock with AudioOutputUnitStart /  
AudioOutputUnitStop  
* QTBUG-111209 QML Multimedia looping broken  
* QTBUG-111744 QtMM macOS CI: mediaplayer crashes if playing long video  
of with high playback rate  
* QTBUG-110708 [REG: 6.4->6.5-beta2] ffmpeg cannot play http stream  
* QTBUG-99098 Android tst_QMediaCaptureSession test failed  
* QTBUG-108892 Preview of QScreenCapture with HDR display appears dark  
* QTBUG-111459 Heavy jittering in video playback if animations are  
active  
* QTBUG-109009 Ffmpeg: videotoolbox doesn't support some yuv 8bit  
formats  
* QTBUG-111213 FFmpeg: Audio stream from one device to another  
* QTBUG-112305 Ffmpeg looping is not seamless  
* QTBUG-111951 [Reg 6.4->6.5] QMediaPlayer does not support video files  
with Chinese names  
* QTBUG-112714 Unable to access camera  
* QTBUG-112702 QMediaDevices::videoInputs returns empty list when used  
alone  
  
### qttools  
* QTBUG-111973 qdoc: Something is wrong with qdoc's handling of marked  
code  
* QTBUG-111310 \image tag breaks \value block  
* QTBUG-112256 qdoc should warn about documented global functions that  
do not use \relates  
* QTBUG-112220 Assistant starting with inappropriately small window  
* QTBUG-111775 Out-of-bounds string read in lupdate translationAttempt  
* QTBUG-112682 REG->6.5.0: Qt Designer does not handle horizontal  
alignment properties correctly  
* QTBUG-112641 6.5: qdoc crashes generating WebXML for Qt for Python in  
Qt 3D examples page  
* QTBUG-112841 [Possible regression 6.4.x->6.5.0] Cannot add translation  
to project from subdirectory (CMake)  
* QTBUG-113116 Documentation typos, errors and improvements  
  
### qttranslations  
* QTBUG-112678 Translation catalog for Qt installations is empty  
  
### qtdoc  
* QTBUG-85544 androiddeployqt fails with message that neither  
libqtforandroid.so or libqtforandroidGL.so are included  
* QTBUG-97636 Qtbase for Android with examples fails to build  
* QTBUG-83997 Can't deploy a simple console application  
* QTBUG-93185 Android platform plugin not linked when using only QtCore  
* QTBUG-111982 New example demos/documentviewer fails to compile  
* QTBUG-111751 Qt Print Support doesn't support ALL target.  
* QTBUG-111914 Docs:  Cannot configure Q4A kit for armv7 with the value  
given in docs  
* QTBUG-107849 Qt 6.4.0 Purchasing Hangman example does not start  
* QTBUG-112327 Typo in the document?  
* QTBUG-112416 Android docs: Update to correct platform/API version  
* QTBUG-110914 Deprecated Qt.labs.settings do not link to new QtCore  
alternative  
* QTBUG-104930 QLocale shows German text for "en_DE"  
* QTBUG-113116 Documentation typos, errors and improvements  
  
### qtlocation  
* QTBUG-111005 [REG 6.5.0 beta2->beta3] location/mapviewer and places  
not launching  
* QTBUG-112477 configure -no-gui fails in qtlocation  
* QTBUG-87646 WheelHandler doesn't work correctly with TouchPad  
* QTBUG-112394 Minimal map example - WheelHandler not working  
* QTBUG-112432 wayland plugin should distinguish touchpads from mice,  
etc.  
  
### qtconnectivity  
* QTBUG-111116 QT BLE scanner example causes high cpu usage  
* QTBUG-112194 Error message with heartrate-game Bluetooth example  
* QTBUG-112843 [REG 6.5.0->6.5.1] nfc/annotatedurl not compiling on  
Android  
* QTBUG-104754 manual tests that use qt_internal_add_manual_test don't  
run on iOS  
  
### qtwayland  
* QTBUG-110420 QtWayland fails to build  
* QTBUG-110623 Constrained menus activate items when cursor is not on  
them  
* QTBUG-87303 Wayland context menus can go off the screen because Qt  
does not do set_constraint_adjustment  
* QTBUG-102457 Qt may hit failed state if Wayland compositor provides no  
supported shell integrations  
* QTBUG-113022 wrong cmake module name  
* QTBUG-111503 QXkbCommon: No Qt::KeypadModifier in QKeyEvents in  
QtWaylandCompositor  
* QTBUG-113233 Need a way atomically adjust QWindow minimum and maximum  
sizes  
* QTBUG-97037 DragHandler / startSystemMove window move issue with QT6  
Webengine on Wayland  
* QTBUG-112808 ERROR: cannot convert 'std::nullptr_t' to 'VkSurfaceKHR'  
{aka 'long long unsigned int'} in assignment  
* QTBUG-112853 Cannot send keys that need modifiers  
  
### qt3d  
* QTBUG-111325 Crash at destruction when running Scene3D in QQuickView  
* QTBUG-110128 Gooch material does not work with Direct3D  
* QTBUG-111980 [REG 6.5.0 RC->beta3] qt3d/wireframe, lights and pbr-  
materials fails on configure  
* QTBUG-112914 Qt3D/Windows[D3D11]: Crash at destruction  
  
### qtwebengine  
* QTBUG-111585 REG: GL Errors with WebGL on macOS 13  
* QTBUG-104869 QWebEngineDownloadItem::totalBytes() always returns -1  
* QTBUG-111574 documentation is wrong for WebEngineCertificateError  
* QTBUG-111784 Regression: macOS: Some video do not show pictures after  
WebGL fix  
* QTBUG-112007 Qt WebEngine 3rd party licensing documentation is  
generated but hidden  
* QTBUG-106359 QtPDF multipage example should switch to search result  
tab during searching  
* QTBUG-111939 Dependency update on qt/qtwebengine failed in 6.5.0  
* QTBUG-106072 QtPdf can't open password-protected PDF files on  
Windows/Android  
* QTBUG-87275 Incorrect parsing of local urls in qml  
* QTBUG-111958 opus detection in QtWebEngine still needs perl  
* QTBUG-88482 License terms are missing for Qtpdf  
* QTBUG-112644 FileNotFoundError: [Errno 2] No such file or directory:  
'Gn_EXECUTABLE-NOTFOUND'  
* QTBUG-112282 Support Metal RHI  
* QTBUG-112280 Support Metal and D3D RHI backends  
* QTBUG-111067 Qt PDF Multipage example is crashing on desktop when  
loading pdf files  
* QTBUG-111909 QWebEngineView::print margin issues  
* QTBUG-109401 Add DirectX support to QWebEngine  
* QTBUG-112772 Developer tools open with "screencast" enabled (again)  
* QTBUG-111697 Build failure with GCC 13  
* QTBUG-112700 [REG] [macOS] Using getUserMedia() opens new window's tab  
in Dock  
* QTBUG-113109 [REG 6.4 -> 6.5] WebEngineScripts don't always run on  
pages containing iframes  
* QTBUG-111306 tst_MultiPageView::navigation uses fixed positions  
* QTBUG-108154 Saving to MHTML while printing to PDF crashes with  
SIGSEGV  
* QTBUG-110504 Webengine extremely slow in loading webpage in debug  
build  
  
### qtwebview  
* QTBUG-82810 [Android] Deadlock for dynamically loading webview  
  
### qtcharts  
* QTBUG-106404 Audio Example doesn't scale properly on android  
* QTBUG-109762 Setting plotArea makes the background to disappear  
* QTBUG-112917 sizeBy method of QScatterSeries is not behaving as  
expected.  
* QTBUG-112904 Scatter points become invisible or are plotted  
incorrectly while size configuration is applied.  
* QTBUG-112919 PointsConfiguration not cleared even when there are no  
points in QScatterSeries  
  
### qtdatavis3d  
* QTBUG-112813 Qt6::DataVisualization has a hard dependency on Qt6::Qml  
* QTBUG-112773 FAIL!  : qmltest::Bars3D  
Common::test_3_change_invalid_common() Uncaught exception: Value is null  
and could not be converted to an object  
  
### qtvirtualkeyboard  
* QTBUG-111928 [Reg 6.3.2 -> 6.4.x] Virtual keyboard layout is broken  
* QTBUG-108536 Custom styles are not working  
* QTBUG-111154 [REG Qt 5 → Qt 6] qtvirtualkeyboard is unable to locate  
any custom stylings  
  
### qtspeech  
* QTBUG-112607 [MSVC] Qt6 failed to build due to error C2695 on Windows  
x86 mode  
  
### qtlottie  
* QTBUG-97259 LottieAnimation start() and stop() not work as expected  
  
### qtquick3d  
* QTBUG-111715 infinite grid documentation has errors  
* QTBUG-110160 Continuous memory growth when the source of Loader 3D{}  
continues to change  
* QTBUG-111276 Poor instanced picking performance  
* QTBUG-111929 QQuick3DLightmapBaker not exported for Design Studio  
* QDS-9507 Lightmapper issues  
* QTBUG-111997 Picking a model with custom geometry with huge numbers of  
vertex  
* QTBUG-112928 FAIL!  : tst_MultiWindow::cubeMultiViewportMultiWindow()  
'comparePixelNormPos(result, 0.5, 0.5, QColor::fromRgb(59, 192, 77),  
FUZZ)' returned FALSE. ()  
* QTBUG-112178 Camera's scale affect the scene  
* QTBUG-112450 Shadows are incorrect when scene has no shadow-casting  
objects  
* QTBUG-110400 [macOS] Qt Quick 3D OrbitCameraController : Zooming is  
not working with native gesture  
* QDS-9667 Cannot choose lightmap for a model using combobox in  
Properties view  
* QTBUG-113043 Picking fails with imported scene  
* QTBUG-111709 FAIL!  : tst_Input::singleTap2D  
* QTBUG-107990 item2D cannot be shared by importScene  
* QTBUG-101688 QtQuick3D: Fix compiler warnings for QNX  
  
### qt5compat  
* QTBUG-112985 Access to GL_MAX_VARYING_COMPONENTS fails in macOS with  
core profile context  
  
### qtmqtt  
* QTBUG-111846 MQTT Subscriptions Example Crashes  
  
### qthttpserver  
* QTBUG-112484 QHttpServer: use function pointer as ViewHandler  
  
### qtquick3dphysics  
* QTBUG-112819 Capsule geometry has invalid geometry bounds  
* QTBUG-111870 CharacterController: changing height or diameter is not  
working  
* QTBUG-113597 ERROR building: Timeout after 15m0s: No output received  
* QTBUG-111565 CharacterController does not receive Contact Reports  
* QTBUG-112846 Shadow artifacts  
  
### qtgrpc  
* QTBUG-111983 New examples grpc/magic8ball and chat not compiling on  
iOS or Android  
* QTBUG-112754 The qtprotobuf and qtgrpc example documentation doesn't  
link to the .proto files in the list of the example sources  
  
### qtquickeffectmaker  
* QTBUG-113021 Black areas in Water node  
* QTBUG-108171 ScrollBar with sections is jumpy  
* QTBUG-113531 EffectMaker not find resources on macOS  
  
Known Issues  
------------  
  
* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-6.5/supported-platforms.html  
* RTA reported issues from Qt 6.5  
https://bugreports.qt.io/issues/?filter=24558  
* See Qt 6.5 known issues from:  
https://wiki.qt.io/Qt_6.5_Known_Issues  
* Qt 6.5.1 Open issues in Jira:  
https://bugreports.qt.io/issues/?filter=25090  
  
------------  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Amir Masoud Abdol  
Laszlo Agocs  
Yigit Akcay  
Anu Aliyas  
Dimitrios Apostolou  
Mahmoud Badri  
Mate Barany  
Sebastian Beckmann  
Vladimir Belyavsky  
Nicholas Bennett  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
Mikolaj Boc  
Tatiana Borisova  
Joerg Bornemann  
Assam Boudjelthia  
Aurélien Brooke  
Kai Uwe Broulik  
Michael Brüning  
Andrey Butirsky  
Olivier De Cannière  
Wang Chuan  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Szabolcs David  
James DeLisle  
Pavel Dubsky  
Artem Dyomin  
Alexey Edelev  
David Edmundson  
Oliver Eftevaag  
Christian Ehrlicher  
Iikka Eklund  
Hatem ElKharashy  
Andreas Eliasson  
Fabio Falsini  
David Faure  
Ilya Fedin  
Nicolas Fella  
Ben Fletcher  
Samuel Gaist  
Frederik Gladhorn  
Mikko Gronoff  
Henning Gruendl  
Kaj Grönholm  
Christoph Grüninger  
Richard Moe Gustavsen  
Heikki Halmet  
Jani Heikkinen  
Miikka Heikkinen  
Christian Heimlich  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Mats Honkamaa  
Sam James  
Allan Sandfeld Jensen  
Tim Jenßen  
Maurice Kalinowski  
Jonas Karlsson  
Timothée Keller  
Friedemann Kleint  
Michal Klocek  
Lars Knoll  
Seokha Ko  
Sze Howe Koh  
Jarkko Koivikko  
Antti Kokko  
Tomi Korpipää  
Fabian Kosmale  
Mike Krus  
Konrad Kujawa  
Santhosh Kumar  
Kai Köhne  
Inho Lee  
Kimmo Leppälä  
Wladimir Leuschner  
Robert Löhning  
Thiago Macieira  
Christophe Marin  
Ievgenii Meshcheriakov  
Leena Miettinen  
Samuel Mira  
Jan Moeller  
Hamish Moffatt  
Safiyyah Moosa  
Bartlomiej Moskal  
Marc Mutz  
Antti Määttä  
Martin Negyokru  
Andy Nichols  
Mårten Nordheim  
Dennis Oberst  
Bumjoon Park  
Kwanghyo Park  
Samuli Piippo  
Timur Pocheptsov  
Milla Pohjanheimo  
Joni Poikelin  
Aleix Pol  
Cajus Pollmeier  
Rami Potinkara  
Lorn Potter  
Liang Qi  
Matthias Rauter  
David Redondo  
Topi Reinio  
Mario Roessel  
David Rosca  
Shawn Rutledge  
Ahmad Samir  
David Schulz  
Carl Schwan  
Dmitry Shachnev  
Sami Shalayel  
Andy Shaw  
Kristoffer Skau  
Colin Snover  
Ivan Solovev  
Axel Spoerl  
Christian Strømme  
Tarja Sundqvist  
Lars Sutterud  
Tasuku Suzuki  
Jan Arve Sæther  
Morten Sørvig  
Henrik Thillman  
Jens Trillmann  
Paul Olav Tvete  
Peter Varga  
Doris Verria  
Tor Arne Vestbø  
Ville Voutilainen  
Juha Vuolle  
Jaishree Vyas  
Edward Welbourne  
Paul Wicking  
Oliver Wolff  
Semih Yavuz  
Vlad Zahorodnii  
JiDe Zhang  
Yuhang Zhao  
Shengfeng Zhou  
