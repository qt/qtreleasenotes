Release note  
============  
Qt 6.5.3 release is a patch release made on the top of Qt 6.5.2.  
As a patch release, Qt 6.5.3 does not add any new functionality but provides  
bug fixes and other improvements and maintains both forward and backward  
compatibility (source and binary) with Qt 6.5.2.  

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
* 79a67d099a Consult QIcon::fallbackThemeName() even for themes with  
explicit parents  
QIcon::fallbackThemeName() will now be used as fallback even for themes  
that declare a parent theme.  
  
* d5db8c6d77 Consult QIcon::fallbackSearchPaths() even when theme name  
is empty  
QIcon::fallbackSearchPaths() will now be consulted for fallback icons  
even if the current theme name is empty.  
  
* 1641f3bf5c QFutureSynchronizer: fix aliasing problem in setFuture()  
Fixed a crash in setFuture() if the argument was already a member of  
QFutureSynchronizer::futures().  
  
* 6d65e06abc SSL: upgrade the default DH parameters  
The default Diffie-Hellman parameters are now using the 2048-bit MODP  
group from RFC 3526.  
  
* e6e545f8ad QGtk3Theme: Do not default Active WindowText to button  
foreground  
Default to GTK Entry Text / Normal Text / qt_fusionPalette  
  
* 6511fb9b21 QCborValue: fix memleak on Array to Map coercion  
Fixed a memory leak when an array was coerced into a map.  
  
* b6267f7ca8 QSslDiffieHellmanParameters: fix mem-leak  
Fixed a memory leak in parsing of PEM-encoded Diffie-Hellman  
parameters.  
  
* 9fd108dce6 Update bundled libjpeg-turbo to version 3.0.0  
libjpeg-turbo was updated to version 3.0.0  
  
* 6332711973 Update bundled libpng to version 1.6.40  
libpng was updated to version 1.6.40  
  
* 07adef0c9b QGuiApplication: Report default platform name before  
initialization  
QGuiApplication::platformName now reports the default platform name if  
QGuiApplication hasn't been instantiated yet. It used to return an empty  
string.  
  
* de86906e4f SQLite: Update SQLite to v3.43.0  
Updated SQLite to v3.43.0  
  
* 5929b175f5 Set color scheme after handling theme change in windows  
Update colorScheme property after palette change.  
  
* 4a928bb545 Update bundled zlib to version 1.3  
zlib was updated to version 1.3.  
  
* eb5be509dc Fix qHash(qfloat16) to match Qt 6.4 behavior  
Fixed qHash(qfloat16) which was broken from 6.5.0 to 6.5.3, inclusive.  
If you compiled against one of the affected Qt versions, you need to  
recompile against either Qt 6.4 or earlier or 6.5.4 or later, because  
the problematic code is inline.  
  
* 580ee6389c SQLite: Update SQLite to v3.43.1  
Updated SQLite to v3.43.1  
  
* fdfbb61069 [docs] Fix \since for qHash(qfloat16)  
Delete the old entry for qHash(qfloat16), keep the one from this  
commit.  
  
### qtdeclarative  
* 1001b385f2 Fix memory leak when invalidating NativeRendering fonts  
Fixed a controlled memory leak with Text.NativeRendering where loading  
and unloading the same application fonts could cause memory usage to  
increase indefinitely and not be regained until the window was closed.  
  
### qttools  
* a7f85d4e8 lupdate: remove number heuristics  
Removed the number heuristics feature. Users are advised to avoid hard-  
coded numbers in translatable strings and use QString::arg instead.  
  
### qtconnectivity  
* daefa8e2 QBluetoothUuid: remove default case labels and fix the  
fallout  
Fixed missing result of  
characteristicToString(CharacteristicType::WeightScaleFeature).  
  
### qt3d  
* 6d225afa5 Texture array support for RHI renderer  
Enable texture array on the RHI render plugin  
  
### qtimageformats  
* dc35e55 Update bundled libtiff to version 4.5.1  
Bundled libtiff was updated to version 4.5.1  
  
* 39852c3 Update bundled libwebp to version 1.3.1  
Update bundled libwebp to version 1.3.1  
  
* fbf8d38 Update bundled libwebp to version 1.3.2  
Update bundled libwebp to version 1.3.2  
  
* cb83a13 Update bundled libtiff to version 4.6.0  
Bundled libtiff was updated to version 4.6.0  
  
### qtwebengine  
* 53b5d93d9 RenderWidgetHostViewQtDelegateItem: keep grabs  
WebEngineView (or WebView backed by Qt WebEngine) no longer allows  
components outside to take over the mouse or touch exclusive grab. For  
example if the user starts dragging a scrollbar inside the web view,  
that continues until release, regardless of any DragHandler, Flickable  
etc.  
  
### qtvirtualkeyboard  
* 6c6db722 Restore style path for backwards compatibility  
Restored style path /QtQuick/VirtualKeyboard/content/styles for  
backwards compatibility.  
  
### qtgrpc  
* cb64d8e Remove silent reconnection to grpc server stream  
Client HTTP/2 channel doesn't retry to start server-stream  
automatically after connection is lost, since this contradicts gRPC  
streaming concepts. The error should be handled by business logic of an  
application instead.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-114078 wasm: NetworkReply with empty data generates runtimeError  
* QTBUG-113573 When dragging a header section it will no longer scroll  
when at the edge  
* QTBUG-111330 error: Not a signal or slot declaration in code generated  
by qt_add_dbus_interface  
* QTBUG-114530 Qt build in jenkins triggers message boxes with help  
messages from Qt tools  
* QTBUG-114625 TRY_RUN failure on cross-compilation  
* QTBUG-108015 [CMake] [MSVC2022] TEST_separate_debug_info always fail  
* QTBUG-114629 QJsonValueRef inherits non-exported class  
QJsonValueConstRef  
* QTBUG-62912 Hover is not reset properly with touchscreens  
* QTBUG-114334 [REG 6.5.0 -> 6.5.1] Segfault in  
QXcbConnection::handleXcbEvent with touch(pad) gestures after  
disconnecting input device  
* QTBUG-114537 linking of QtNetwork against GSSAPI fails on macOS with  
CMAKE_FIND_FRAMEWORK=LAST  
* QTBUG-114546 [Reg 6.2.8->6.5.1] [macOS] Prior modal dialog and manual  
event processing can break QMessageBox  
* QTBUG-112491 examples/widgets/mainwindows/mainwindow crashes  
* QTBUG-114542 DockWidget Crashes when undocked and tabbified  
* QTBUG-107627 AndroidAssetsFileEngineHandler is broken  
* QTBUG-114576 QFileInfo("assets:/path/to/file").fileName() returns  
wrong name  
* QTBUG-114219 QFileInfo::fileName() does not strip assets prefix on  
Android  
* QTBUG-112261 [REGRESSION] QDir::entryList returns invalid names (6.4.2  
-> 6.4.3)  
* QTBUG-113641 PlatformCommonInternal INTERFACE_LINK_OPTIONS property is  
propagated to user projects  
* QTBUG-114606 Cancelling a QPromise with a failure handler crashes  
* QTBUG-114654 KeyRelease event not propagated to parent of QLineEdit  
* QTBUG-112200 Possible memory leak with Fusion style  
* QTBUG-114073 qdoc resolves "QML Import Path" reference incorrectly  
* QTBUG-114115 Unable to run on Gitlab CI / Windows Server Core docker  
image  
* QTBUG-48161 QDockWidget emits visibilityChanged(false) when minimizing  
the window or switching virtual desktops  
* QTBUG-114785 MinGW v13.1.0: errors in TinyCBOR (Windows 10 22H2  
x86_64)  
* QTBUG-111105 QT_WIDGETS_HIGHDPI_DOWNSCALE doesn't work with  
QOpenGLWidget  
* QTBUG-114571 Incorrect colors after switching between light and dark  
modes  
* QTBUG-113169 QStyleHints::colorScheme reports incorrect value and  
breaks app palette  
* QTBUG-114191 [Dialog QML] Dialog becomes dark after putting the app in  
the background and resuming it back with iOS style  
* QTBUG-112351 Incorrect description of QtConcurrent::run()  
* QTBUG-114431 FindEGL.cmake fails for static linking with Qt  
* QTBUG-114416 iOS: Focussing on a read-only TextEdit can prevent Button  
from receiving further clicks  
* QTBUG-113975 [iOS] Button cannot be focused and take action if it is  
placed in text area  
* QTBUG-113438 AT-SPI: Wrong char reported by GetCharAtOffset when code  
point > 65535  
* QTBUG-114821 [Reg 6.4->6.5] QMenu no longer renders disabled text  
correctly  
* QTBUG-108482 Mention more clearly that only a subset of features of  
supported HTML tags are implemented  
* QTBUG-114583 Headers use things in <iterator> without including it  
* QTBUG-106483 Moving a window to another screen (different DPI) using  
keyboard shortcuts while a menu is open has unexpected behavior  
* QTBUG-114605 [macOS] Hover events are not received if the parent of  
the QWindow is embedded  
* QTBUG-114865 macos: Building with sanitizer enabled fails  
* QTBUG-109781 QXmlStreamReader asserts trying to construct XmlStringRef  
of negative len on external input  
* QTBUG-114829 [REG 6.5.1 -> 6.5.2] Crash/failed assert by passing  
certain xml file to QXmlStreamReader  
* QTBUG-114847 QMAKE_APPLE_DEVICE_ARCHS not documented  
* QTBUG-113698 Nullptr dereference in qcoretextfontdatabase.mm  
* QTBUG-68821 QNetworkAccessManager does not propagate proxy errors  
properly  
* QTBUG-114470 Build failure for iOS  
* QTBUG-112995 Long press on touch screen breaks drag and drop  
* QTBUG-111162 WASM: Platform minimum size only enforced on window  
initialization  
* QTBUG-114925 Reg->6.6/MSVC/WIndows:  Cannot build with debug due to  
compiler flag clash in syncqt  
* QTBUG-114803 iOS Simulator build fails  
* QTBUG-113685 macOS: QMessageBox does not emit the accepted signal when  
parented  
* QTBUG-114919 QFileDialog spams users with permission requests  
* QTBUG-114944 qtestcase.h may need a fix to avoid unreachable code  
warning.  
* QTBUG-112371 Unreachable code warning with MSVC2019 with QTestCase  
class  
* QTBUG-114797 QVariant::convert may crash even if QVariant::canConvert  
returns true  
* QTBUG-112893 WASM: exec() fails, even when ASYNCIFY is enabled  
* QTBUG-114918 qvulkanwindow.cpp:451:3: error: redefinition of  
'qvk_sampleCounts  
* QTBUG-114600 [REG 6.4.3 -> 6.5.0] Strange UI styles  
* QTBUG-112956 [REG 6.4] syncqt.cpp does not install headers marked with  
qt_deprecates pragma  
* QTBUG-92464 QCompleter breaking use of keyboard accents  
* QTBUG-108522 [Regression: 4 - 5&6] QCompleter can not use input method  
when completer popup is visible on Linux  
* QTBUG-114225 QTableView create extra row  
* QTBUG-114683 Not null value is not enforced in SQL iBase plugin  
* QTBUG-115003 QPainter crash when drawing image  
* QTBUG-114991 QVariant<double> comparison uses <float> on  `-qreal  
float`  platforms  
* QTBUG-115002 Can't import MTLDevice with QRhi Metal.  
* QTBUG-114377 Broken focus when hiding a button of a QDialogButtonBox  
* QTBUG-115101 WaylandGlobalPrivate_sync_headers is not running if  
nothing depends on WaylandGlobalPrivate  
* QTBUG-115062 Incorrect handling of  
QT_FATAL_CRITICALS/QT_FATAL_WARNINGS (non-UB data race)  
* QTBUG-115124 qtpaths JSON output is invalid  
* QTBUG-112961 Opening QSqlDatabase in parallel causes endless loop at  
shutdown  
* QTBUG-64132 QToolButton should elide text when width constraints  
prevent from showing whole text  
* QTBUG-113319 ICOReader does not read AND mask for 16bpp/24bpp ico  
* QTBUG-113461 QML TextField Popup  
* QTBUG-115154 tst_QSocketNotifier::unexpectedDisconnection is flaky on  
macOS  
* QTBUG-92113 QXmlStreamReader freezes  
* QTBUG-95188 Out-of-memory in QXmlStreamReader  
* QTBUG-114854 windeployqt deploys debug versions of QML plugins  
* QTBUG-112895 bool ParseResult::operator bool() returns true if no  
error  
* QTBUG-115105 QAtomicScopedValueRollback: CTAD from  
Q(Basic)AtomicPointer fails  
* QTBUG-115031 qtbase -unity-build-batch-size 103 fails  
* QTBUG-111896 Accessibility button is visible if QWasmWindow canvas is  
transparent  
* QTBUG-114199 macOS: Clicking on a menu item which opens a submenu  
erroneously closes menu  
* QTBUG-114069 qt_generate_deploy_app_script error when cross-compiling  
* QTBUG-115041 Qt 6 documentation: "int" should be "QByteArray"  
* QTBUG-115243 qtbase 6.6.0-beta2 fails to build (linux-clang target) at  
cmake stage if -DQT_FEATURE_gc_binaries is used  
* QTBUG-115229 Qt 6.5.1 MSVC 2019 fails to compile QtMqtt because of  
Chinese text encoding  
* QTBUG-97482 Android: QPushButton with QMenu does not work on Qt6  
* QTBUG-115249 QCborValue mem leak in or near convertArrayToMap()  
* QTBUG-115263 QHostInfo is leaking QSlotObjectBase in  
tst_QHostInfo::lookupConnectToFunctionPointerDeleted()  
* QTBUG-115318 QT_ANDROID_DEPLOY_RELEASE CMake variable has no effect  
* QTBUG-112921 Cannot create packages for Google PlayStore  
* QTBUG-108132 cannot set --release option to androiddeployqt when  
building app with cmake ?  
* QTBUG-114909 QLocale::toTime with ShortFormat returns invalid QTime  
for en_US "h:mm AP"  
* QTBUG-115324 Qt6 configured wrong when is placed inside "3rdparty"  
folder  
* QTBUG-115054 QWidget::createWindowContainer does not work on 6.5.1  
* QTBUG-115286 QFactoryLoader memory leak on follow-up setExtraPath()  
* QTBUG-115189 QColorDialog regression in 6.5.1  
* QTBUG-114575 Value changes when cursor is moved in date/time field  
* QTBUG-115473 Missing QSet::removeIf() method  
* QTBUG-114338 Qt Quick with metal crashes on older macOS 11  
* QTBUG-108216 Investigate the QRhi pipeline cache (MTLBinaryArchive  
usage) on macOS 13  
* QTBUG-109326 QTableView and QTreeView with Fixed vertical size policy  
and AdjustToContents sizeAdjustPolicy always reserve space for  
horizontal scroll bar  
* QTBUG-113552 Wrong sizeHint for QTreeWidget having an AdjustToContents  
sizeAndAdjustPolicy  
* QTBUG-69120 QTreeView viewportSizeHint is wrong when called before  
showing the widget  
* QTBUG-115646 QTypeTraits::has_operator_less_than_v behaves  
surprisingly  
* QTBUG-114825 Blacklisting of tst_qquickpopup::hover doesn't work  
* QTBUG-115135 a11y: Top-level item views don't have the application as  
accessible parent  
* QTBUG-95569 CMake infinite loop when configuring with Vulkan support  
in Conan  
* QTBUG-115327 echoplugin uses an ambiguous project name  
* QTBUG-115149  Unwanted highlight of arrows in tree view when hovering  
with mouse  
* QTBUG-115599 Possible SEGV (null pointer deref) in  
QXcbConnection::initializeAllAtoms()  
* QTBUG-115330 QCoreApplication::requestPermission() is leaking slot  
objects  
* QTBUG-115758 Tuio Fiducials always contain invalid UniqueIds  
* QTBUG-114559 SPNEGO/Negotiate:  Can't set spn Option - Signal not  
firing  
* QTBUG-115732 Incorrect IANA ID detected for Windows timezone La Paz,  
Mazatlan  
* QTBUG-40315 doc: QFontMetrics::elidedText(...) does not work as  
expected for ElideNone  
* QTBUG-115740 QLocale for Spanish does not work correctly with  
thousands separators.  
* QTBUG-105007 On macOS, QMimeType::comment returns value for the  
secondary language  
* QTBUG-115516 QColorDialog: WA_Hover breaks color and luminance picker  
* QTBUG-115756 Android: QLineEdit setText() from textEdited signal does  
not move cursor to the end  
* QTBUG-115597 QMenu crash if app loses focus immediately after  
selecting sub-menu item  
* QTBUG-115809 warning: ‘malloc’ may be used uninitialized [-Wmaybe-  
uninitialized]  
* QTBUG-115964 qdbuscpp2xml only exports methods/signals with  
QDBusVariant arguments if there's at least one method/signal with  
QVariant as argument  
* QTBUG-25944 QXmlStreamReader::readNextStartElement() works inelegantly  
with isEndDocument()  
* QTBUG-115058 QDockWidget group window still visible when empty  
(regression)  
* QTBUG-114435 Regression 5.15.14: Cannot open Files from Android  
FileDialog with spaces or umlauts  
* QTBUG-115652 Child quick widget fails to draw if it's child of raster  
native widget  
* QTBUG-108344 Something is rotten with texture-based widgets that are  
native child widgets or are children of a native child widget  
* QTBUG-113557 Raster native widget fail to draw when there is a quick  
widget sibling  
* QTBUG-115109 [REG] QTabWidget doesn't draw tabs on the left of the  
initially current tab  
* QTBUG-113140 Resizing a QTabBar resets the scroll position  
* QTBUG-116137 Compile and install QtBase 6.5.2 does not provide header  
files in -prefix path  
* QTBUG-115853 There is NO method current() for QVulkanInstance  
* QTBUG-115632 Long press textfield popup teleports after being drawn  
for the first time  
* QTBUG-116224 Wrong QScrollBar with Qt6.5 + windows vista style in RTL  
mode  
* QTBUG-111975 QVideoFrame::toImage has a memory leak at 3840 * 2160  
resolution  
* QTBUG-116166 Network tests fail with OpenSSL 3.1.1  
* QTBUG-116287 [REG BiC 6.5.2 → 6.5.3] New QDialogButtonBox symbol  
* QTBUG-116231 wasm: on windows, shift key produces the word "Shift"  
* QTBUG-116499 Use of edid serial number in qwindowsscreen.cpp is broken  
* QTBUG-115801 Exception in NVDA screen reader when hovering over text  
edit (due to invalid return value)  
* QTBUG-83733 Don't use deprecated/removed functions and structs with  
OpenSSL v3  
* QTBUG-116527 Regression; (QML) Locale enums no longer exist  
* QTBUG-116056 signal not found when deleting QAbstractItemModel  
* QTBUG-116181 Android: QFile can't open file in directory which is  
chosen by QFileDialog::getExistingDirectory()  
* QTBUG-114423 [Reg 6.4.3->6.5] QTreeWidget crash inside QDialog on  
MacOS  
* QTBUG-116609 MinGW 13.1.0: Coin testing fails at qtbase  
* QTBUG-115461 [REG 6.5.1 -> 6.5.2] QT_WIDGETS_HIGHDPI_DOWNSCALE is  
broken again  
* QTBUG-113995 QDesktopServices::openUrl: Local files don't open anymore  
* QTBUG-115511 QToolTip StyleSheet Color Property Broken in 6.5.2  
* QTBUG-115087 getOpenFileContent does not open the dialog  
* QTBUG-112653 Incorrect colour name returned when handling  
colorSchemeChanged  
* QTBUG-115043 Minor source compatibility break in QLoggingCategory  
* QTBUG-112735 Typo in QTextStream documentation ("ISO-5589-1")  
* QTBUG-114446 wasm: native keyboard does not popup on iOS  
* QTBUG-113765 QComboBox: Wrong popup position when switching to Fusion  
style  
* QTBUG-116696 Menus have window type _NET_WM_WINDOW_TYPE_NORMAL instead  
of _NET_WM_WINDOW_TYPE_POPUP_MENU  
* QTBUG-39887 Regression bug: QWidget::setAttribute() does not set  
Qt::WA_X11NetWmWindowType in Qt 5.  
* QTBUG-108402 tst_Gestures failures on macOS 13  
* QTBUG-116517 Zero-width space in qaccessiblewidgets.cpp causing  
compilation error  
* QTBUG-116060 Reg 6.4.3->6.5.1 QTimer - signal/slot connection not  
working  
* QTBUG-116695 Contradictory statements about signal's return type  
* QTBUG-116277 QFileDialog not cleaned up when parent deleted  
* QTBUG-112914 Qt3D/Windows[D3D11]: Crash at destruction  
* QTBUG-116788 Sporadic crash on  
QNetworkReplyHttpImplPrivate::loadFromCacheIfAllowed() with nullptr  
access  
* QTBUG-116338 Vulkan-based QQuickWidget or QRhiWidget is rendered  
incorrectly when in a QScrollArea  
* QTBUG-116155 Crash with native QComboBox in refreshing QWidget  
* QTBUG-3287 Reads a '\0'-terminated string from the QDataStream  
* QTBUG-114203 keyReleaseEvent not triggered on windows devices with  
touch display  
* QTBUG-116330 wasm: Exit app with async main() results on runtime error  
* QTBUG-116732 ld: warning: -undefined error is deprecated  
* QTBUG-115699 [REG 6.4.3-6.5] Changing the minimum size get the window  
out of maximized state  
* QTBUG-115752 stack-use-after-return in tst_assetimport  
* QTBUG-116715 docs: qsettings path on embdded linux  
* QTBUG-116064 [REG SiC 6.4 -> 6.5] qHash(qfloat16(x)) is now ambiguous  
on GCC13  
* QTBUG-116076 qHash(qfloat16(x), seed) != qHash(float(x), seed) unless  
seed == 0  
* QTBUG-117021 ASSERT: "self.window" in file qiosviewcontroller.mm, line  
110  
* QTBUG-116357 Build fails with -march=native  
* QTBUG-111698 Build fails with -march=amdfam10  
* QTBUG-107072 build chooses unavailable hardware flags  
* QTBUG-117200 Reg -> 6.6b4: Exit warning :"QItemSelectionModel:  
Selecting when no model has been set will result in a no-op" from apps  
with  sort proxy filter model  
* QTBUG-104878 xcb wacom support gets confused about device instances  
* QTBUG-114243 Qt 6.5 regression with static cross-compiling for Windows  
* QTBUG-112896 gtk3 platformtheme returns the font of GtkFixed widget  
instead of monospace font  
* QTBUG-110025 Android tests aren't bundling OpenSSL for any test  
* QTBUG-109776 tst_QAbstractItemView::selectionAutoScrolling() with  
QtWayland failed on Ubuntu 22.04, GNOME  
* QTBUG-112824 There is no way to get to the Open GL examples page from  
the Open GL Index  
* QTBUG-101926 "AutoMoc subprocess error" when building in CI  
* QTBUG-115293 tst_QGraphicsItem::itemUsesExtendedStyleOption() with  
QtWayland failed on Ubuntu 22.04, GNOME  
* QTBUG-83160 moc stumbles on _GLIBCXX_VISIBILITY  
* QTBUG-96374 Inactive Qt::Tool window with Qt::FramelessWindowHint flag  
does not show custom cursor  
* QTBUG-114175 QWizard default Style not drawn correctly when scaling  
other than 100%  
* QTBUG-99555 [RE: 6.2.1->6.2.2] macdeployqt fails to produce  
notarizable packages  
* QTBUG-115598 tst_QWidget::render() with QtWayland failed on Ubuntu  
22.04, GNOME  
* QTBUG-115247 \target after \row generates invalid HTML  
* QTBUG-113233 Need a way atomically adjust QWindow minimum and maximum  
sizes  
* QTBUG-93763 Systematic announcement of combobox selected element  
* QTBUG-116077 Inconsistent hashing between different FP types  
* QTBUG-116080 Inconsistent hashing between qint{32,64} on 32-bit  
platforms  
* QTBUG-112957 Toplevel developer build fails to link: undefined symbol:  
vtable for QNetworkAccessDebugPipeBackendFactory  
* QTBUG-114613 QWindow::winId() crashes when QWindowPrivate::create()  
fails  
* COIN-1075 QEMU tests fail randomly on "Exec format error"  
* QTBUG-115832 iOS: About Qt dialog displays incorrectly when launched  
from menu  
* QTBUG-116483 qttools' CMake test test_uiplugin_via_designer fails  
* QTBUG-111514 QtCore fails to link with lld 16.0  
* QTBUG-43674 Accessibility is not enabled when running as root  
* QTBUG-113556 QWhatThis::showText() brings Mac Permission Dialog  
* QTBUG-116689 Debugging qtbase with Creator on boot2qt because of "no-  
prefix" on a prefix build  
* QTBUG-108796 Some examples crash when running with Qt 6.5 kit  
  
### qtsvg  
* QTBUG-95237 [REG 6.0.4 -> 6.1.0] Integer-overflow in  
QFixed::operator+= through QImage::loadFromData(QByteArray)  
* QTBUG-114108 qtsvgglobal_p.h is not correctly installed  
* QTBUG-115648 QSvgRenderer::boundsOnElement() can return wrong results  
with multiple child <text> elements  
  
### qtdeclarative  
* QTBUG-114407 [Boot2Qt] UI of imagine style example - automotive is  
distorted on B2Qt devices  
* QTBUG-114364 qmlformat changes ComponentBehavior  
* QTBUG-114418 qmlsc: compile error with === or !== against undefined or  
null  
* QTBUG-114430 heap-use-after-free when assigning undefined to width and  
height of Control background item  
* QTBUG-114458 [Reg 6.2->6.3] Component.createObject() no longer copies  
QQmlListProperty values correctly  
* QTBUG-114421 Documentation error on ListView orientation table  
* QTBUG-114494 QML rect property as a parameter causing a crash  
* QTBUG-109995 Can not interact with tumblers inside interactive  
flickable on touch  
* QTBUG-113653 [REG 5.15->6.2.3] MultiPointTouchArea doesn't receive  
gestureStarted signal when used inside PathView or Flickable  
* QTBUG-114329 [Reg 5.15 -> 6.2] QML Binding on new object not re-  
evaluated  
* QTBUG-113497 QGuiApplication::setLayoutDirection does not change the  
window to RTL  
* QTBUG-113854 V4 Crashes when using Reflect.ownKeys(...)  
* QTBUG-114492 Automotive example's Dial background image has  
downscaling artifacts  
* QTBUG-114691 Rectangle (with gradient) software backend does not match  
RHI backend  
* QTBUG-109464 Drawer running exit transition during destruction causes  
crash  
* QTBUG-113474 REG: Material.background has no effect on flat buttons  
* QTBUG-114476 qmlsc: crashes with let and control structs  
* QTBUG-114561 Material style highlighted & flat button shows no text  
* QTBUG-113495 Examples imageprovider and imageresponseprovider leave  
garbage files under the qt5 build directory  
* QTBUG-114715 Doc: Stale info about QML module versioning  
* QTBUG-112434 [Regr: 6.3.1->6.3.2] MouseArea stays pressed after double  
click on touch screen  
* QTBUG-109393 [Regr: 6.3.1->6.3.2] iPad: DoubleClicking in MouseArea +  
Popup breaks  
* QTBUG-114186 QQC leaks attached objects  
* QTBUG-113855 qmlsc: unused import false positive for template strings  
* QTBUG-113714 REG: Memory leak when loading/unloading application fonts  
* QTBUG-114874 REG [5.15 → 6.x]: With `height: implicitHeight` binding  
changes to implicitHeight won't trigger property interceptor (e.g.  
Behavior + Animation)  
* QTBUG-113738 [REG 6.4.3 -> 6.5.0] TableView positionViewAtCell crash  
* QTBUG-110328 QEventPoint not being released correctly  
* QTBUG-114687 Qt.application.screens does not update if primary screen  
changes  
* QTBUG-114858 Dynamically adding State causes Segfault  
* QTBUG-98365 Memory leak with removed persisted items  
* QTBUG-114961 Regression: Keyboard input unusable with redirected Qt  
Quick scenes (QQuickRenderControl)  
* QTBUG-114897 Generated QML code doesn't compile with -Wshadow -Werror  
* QTBUG-114910 Missing constructor params crashes program  
* QTBUG-113991 [Reg 6.4 -> 6.5] qmldir javascript library does not  
respect qualified import  
* QTBUG-111013 HorizontalHeaderView with resizableColums true eats input  
when visible (Quick 3D DebugView)  
* QTBUG-114693 Galleryexample app Textarea and Drawer bug.  
* QTBUG-115106 State switched model crashes with ComponentBehaviour  
Bound  
* QTBUG-115179 Clip optimization in  
QQuickDeliveryAgentPrivate::pointerTargets is too aggressive  
* QTBUG-114978 Wearable example icons hard to distinguish from  
background and other cosmetic issues  
* QTBUG-110827 Qt's Gallery example producing tons of warning/errors  
* QTBUG-109306 Standard virtual keyboard typing does't generate standard  
QML events.  
* QTBUG-108144 Race condition when using QQuickMenu  
* QTBUG-95107 ListView item pooling breaks fetchMore  
* QTBUG-115320 memcpy-param-overlap in qv4runtime.cpp  
* QTBUG-115115 [Reg 5.15 -> 6.2]  
QV4::Heap::QObjectMethod::ensureMethodsCache crash when calling a  
function in a js file  
* QTBUG-115159 QmlCache cpp files are always generated differently  
* QTBUG-58718 Problems with JS array sorting after unshift  
* QTBUG-114596 Ownership of QObject* returned to qml by Q_INVOKABLE  
differs for const and non-const pointers  
* QTBUG-115523 [REG: 6.5.1->6.5.2] More complex javascript objects not  
converted to QVariantMap anymore  
* QTBUG-114258 Cannot click on buttons inside Flickable in QQuickWidget  
with stylus  
* QTBUG-115251 Infinite loop in QPropertyObserverPointer::notify on  
startup  
* QTBUG-115319 Issue with number as a context property name  
* QTBUG-115322 Theme properties set on Item are not propagated to  
children  
* QTBUG-115537 [QML Docs] Image.fillMode enum documentation has a broken  
table formatting  
* QTBUG-104904 [REG 5.15.9 -> 6.3.1] SwipeDelegate does not forward  
mouse events to nested items in left, right, behind  
* QTBUG-110589 Property bindings produce wrong values for Animation.to  
* QTBUG-61282 Changing an Animation duration has no effect  
* QTBUG-95840 QML Animations: not specified how they react to property  
changes while running  
* QTBUG-115733 [REG 6.5.1-6.5.2] Automatic conversion JS Array ->  
QByteArray is broken  
* QTBUG-113842 DropArea blocks scrollwheel of a mouse  
* QTBUG-115468 Dynamically adding items to SwipeView may add new items  
behind the current item  
* QTBUG-114801 qmlformat: two spaces in 'NumberAnimation on x  {'  
* QTBUG-115951 qml::UnknownTestFunc() QVERIFY()  
* QTBUG-105090 tst_QQuickMenu AddressSanitizer: heap-use-after-free in  
QQmlData::signalHasEndpoint(int)  
* QTBUG-116028 Material Switch doesn't respect Dense variant  
* QTBUG-104469 Assertion failure when clearing model in  
Component.onCompleted of delegate in Repeater  
* QTBUG-115510 undefined reference to `QQuickTextLine::staticMetaObject'  
when using qmlsc in direct mode  
* QTBUG-113940 FileSelector doesn't work correctly  
* QTBUG-114655 heap-use-after-free when calling console.log() (and  
friends) from QML using cachegen  
* QTBUG-116148 A property alias for a property alias leads to a segfault  
in QQmlPropertyCacheAliasCreator<QV4::ExecutableCompilationUnit>::proper  
tyDataForAlias()  
* QTBUG-116049 [Reg 6.2 -> 6.3] Segmentation fault when using attached  
`Component` property with `Binding`  
* QTBUG-116304 Missing code snippet in Scene Graph - Vulkan Under QML  
example  
* QTBUG-116228 Garbage collector can crash the QML Debugger  
* QTBUG-114482 [Boot2Qt] Cannot run Attached Style Properties example on  
Boot2Qt device  
* QTBUG-105745 QtQuick.Dialogs.quickimpl plugin not linked in static  
builds  
* QTBUG-115707 REG: Child popup inherits palette from parent popup  
rather than its associated window  
* QTBUG-114326 [REG] Non-Singlebit Q_FLAGS not exposed correctly in  
property declarations  
* QTBUG-115557 Missing type "QQuickTapHandler::ExclusiveSignals" in  
property  
* QTBUG-114467 qmllint does not warn about unqualified id lookup  
* QTBUG-113472 [REG 6.4.1->6.5.0] Qt.binding in initial properties  
silently fails for certain types  
* QTBUG-100392 Animations crash at runtime because list properties do  
not emit onChanged signal when their items are destroyed  
* QTBUG-32132 Qml do not updates roles names on  
QAbstractItemModel::reset signal  
* QTBUG-103220 QQmlDelegateModel::_q_modelReset should handle roleNames  
changes  
* QTBUG-116749 missing right bracket  
* QTBUG-97557 Qt Quick batch rendering issue when a batch contain nodes  
that have different index types  
* QTBUG-102589  tst_SceneGraph::render fails on Android  
* QTBUG-114602 Documentation: LineShape is part of QtQuick.Particles?  
* QTBUG-114166 resizing of ListView (possible Flickable) change in  
qt6.5.1  
* QTBUG-116587 If using QQuickRenderTarget and setMirrorVertically(true)  
will lead to the qml Item's clip area damage  
* QTBUG-116576 [REG 6.2 → 6.4]: Connections and signals whose names  
start with an underscore  
* QTBUG-115328 Invalid qmllint_json target generated  
* QTBUG-115004 [Android] TextEdit text selection works incorrect  
* QTBUG-116289 Placing a HoverHandler on a Button makes it respond to a  
right-click.  
* QTBUG-115687 Text loaded with Loader inside Flickable is not visible  
when scrolling  
* QTBUG-116164 [Regr: 6.5.0->6.5.1] Broken "implicitWidth",  
"implicitHeight" bindings  
* QTBUG-106683 qt_add_qml_module: _automoc_json_extraction target and  
resources are rebuilding every time with Visual Studio Generator  
* QTBUG-113426 Crash in QtRhi with QQuickWidget  
* QTBUG-112306 Crash in QRhiResourceUpdateBatch::merge  
* QTBUG-111779  change signal of contentData and contentChildren in  
Dialog doesn't work  
* QTBUG-113473 [REG 6.4.1->6.5.0] Assigning undefined to gadget qreal  
property doesn't reset  
* QTBUG-89023 tst_Animators::testTransitionsWithImplicitFrom is flaky on  
Ubuntu  
* QTBUG-114396 Change "OpenGL" to "Graphics API"  
* QTBUG-114571 Incorrect colors after switching between light and dark  
modes  
* QTBUG-114718 [Tests] tst_QQuickPopup fails  
* QTBUG-40856 MouseArea containsMouse flag is not reset on Touch Screen  
* QTBUG-86729 many Qt Quick test failures after input event refactoring  
* QTBUG-114845 qt6 qml documentation: "font.style" should be  
"font.styleName"  
* QTBUG-114959 Pushing Qt.binding to JS variable in StackView results in  
the pushed item's property not reacting to changes  
* QTBUG-114475 QML QQuickPointerHandler crashes  
* QTBUG-112537 A Window's background cannot be semitransparent anymore  
* QTBUG-113456 Window background cannot be transparent.  
* QTBUG-115015 [REG 5.15.14->6.5.1]: Qt6 QML component Window setting  
property color: "transparent" doesn't make the Window transparent for  
Windows 11 and MacOS  
* QTBUG-115140 qtdeclarative -unity-build-batch-size 100000 fails  
* QTBUG-61783 SwipeDelegate left and right components not reacting on  
touchscreen press  
* QTBUG-114338 Qt Quick with metal crashes on older macOS 11  
* QTBUG-61646 Sample code for GridView.isCurrentItem is in the wrong  
place  
* QTBUG-68404 Using property values in QML animations triggers an  
assertion  
* QTBUG-115317 ListView can't reuse items when its integer model is  
modified  
* QTBUG-109542 TreeView: TreeView.modelIndex() has the order of row and  
column swapped  
* QTBUG-114688 QML application does not start if some QML modules are  
built static  
* QTBUG-115554 QQuickAttachedPropertyPropagator cannot propagate through  
popup and window  
* QTBUG-114953 PdfMultiPageView: Very poor memory performance when  
zooming in/out of long documents  
* QTBUG-113228 Pane only stops some input events from propagating  
* QTBUG-107771 QML Native ScrollBar: Unable to assign [undefined] to int  
* QTBUG-116537 Add \examplecategory to qtqml  
  
### qtactiveqt  
* QTBUG-56172 ActiveQt components are not well behaved when  
unloading/reloading  
* QTBUG-111191 Qutlook Example (ActiveQt) crashes with Qt6.4.2  
  
### qtmultimedia  
* QTBUG-112226 android: Camera does not work  
* QTBUG-114889 Android: Camera does not work at all  
* QTBUG-114659 [DeclarativeCamera] Zoom control is incorrectly  
positioned and does not work on Android  
* QTBUG-114660 [DeclarativeCamera] Locking the phone causes the app to  
crash on Android  
* QTBUG-111912 The content in MediaPlayer is not cleared, when the next  
file has no video or cover art  
* QTBUG-114039 App crash after changing Media Player source  
* QTBUG-113832 6.5.1 Qt MM crashes when playing a simple mp4 on AMD  
cards  
* QTBUG-111543 Heavy flickering with 60 fps videos  
* QTBUG-111911 Some videos has artifacts when playing in MediaPlayer.  
* QTBUG-111459 Heavy jittering in video playback if animations are  
active  
* QTBUG-109213 Video flickering when there is a ParticleSystem component  
or playing some animation at same time  
* QTBUG-114658 [DeclarativeCamera] The image is displayed upside down  
when using the front camera  
* QTBUG-99709 The size of the video missing in QMediaMetaData  
* QTBUG-115122 Documentation: PlaybackRate is not only about audio  
speed.  
* QTBUG-115360 QAudioDevice is exported twice  
* QTBUG-115563 QCameraDevice is declared twice in the qmltypes file  
* QTBUG-115564 QMediaFormat is declared twice in the qmltypes file  
* QTBUG-115566 QMediaMetaData is declared twice in the qmltypes file  
* QTBUG-115842 Android: Cannot take photo if CONTINUOUS_PICTURE  mode  
unavailable  
* QTBUG-109710 [EVR] Crash on readWglNvDxInteropProc() with nullptr  
access  
* QTBUG-115747 H264 MKV duration and position is zero  
* QTBUG-115843 Android:  Supported flashmodes not cleared in FFmpeg-  
backend  
* QTBUG-116533 Sporadic crash on QSGVideoMaterial::updateTextures() with  
nullptr access  
* QTBUG-115935 REG: FFMPEG backend causes Android 13 crash on Launch  
* QTBUG-112219 `QMediaDevices::defaultAudioInput()` wrong device  
* QTBUG-113211 Windows: QMediaPlayer stuttering with some wave files  
* QTBUG-113481 MediaPlayer not reading video orientation metadata  
* QTBUG-115212 [Possible regression 5.15->6.4/6.5]Cannot load video from  
device on Windows Network in 6.4/6.5  
* QTBUG-111567 masOS audio deadlock with AudioOutputUnitStart /  
AudioOutputUnitStop  
* QTBUG-111975 QVideoFrame::toImage has a memory leak at 3840 * 2160  
resolution  
* QTBUG-114174 Camera active property stays true when stopped  
* QTBUG-115763 CMake Error at /home/qt/work/install/lib/cmake/Qt6Multime  
dia/Qt6QFFmpegMediaPluginTargets.cmake  
* QTBUG-113247 Crash when recording wav audio  
* QTBUG-113020 [Regression] Android: declarative-camera example does not  
save picture/picture gets deleted on Qt 6.5  
* QTBUG-115471 FFmpeg video decoding not using hardware accleration.  
* QTBUG-108427 Hardware accelerated video decoding on Windows  
* QTBUG-113256 [macOS] Warnings when connecting/disconnecting AirPods  
* QTBUG-115575 Can not set camera pixel format on MacOS.  
* QTBUG-116393 MediaPlayer freezes if RTSP stream not found  
* QTBUG-115463 QCamera does not support hot plug in and out. Bug or how  
it is designed?  
* QTBUG-116467 [Reg 6.4->6.5] Stopping QCamera when it is not started  
properly causes crash  
* QTBUG-116671 Fix capture_capturesToFile_whenConnectedToMediaRecorder  
on linux CI  
* QTBUG-116836 Android: MediaCodec encoder doesn't accept  
AV_PIX_FMT_MEDIACODEC  
* QTBUG-116075 [Windows] Audio recording starts not at once  
* QTBUG-116979 VideoOutput implicit size doesn't update until playback  
begins  
  
### qttools  
* QTBUG-107853 qt6_add_translations() deletes CMake-generated *.ts files  
when project is cleaned  
* QTBUG-113863 \typealias not highlighted with a clickable link on  
usages  
* QTBUG-110949 lupdate: trailing return type with template parameters  
* QTBUG-112677 Qt lingust, Translation file broken when qsTrId contain <  
* QTBUG-114151 QML Layout don't have a title  
* QTBUG-114956 \generatelist <groupname> does not sort the generated  
list  
* PYSIDE-2379 pyside6-lupdate names the context incorrectly when  
indentation detection is offset by oddly indented multiline string or  
similar  
* PYSIDE-2380 pyside6-lupdate ignores r-strings  
* QTBUG-95340 Linguist wrong warning about %n place markers  
* QTBUG-115048 Qt Quick 6 documentation for Window QML Type still  
recommends to assign to visibility property even though it's now read-  
only  
* QTBUG-113015 [QDoc] Duplicate QML property name causes confusion:  
qml[attached]property QWindow::Visibility Window::visibility  
* QTBUG-115465 Designer injects bogus "<normaloff>.</normaloff>." for  
icon properties  
* QTBUG-115602 A Minimal qdocconf File incorrect  
* QTBUG-115116 Doc: QObject overview documentation lists incomplete  
signatures of connect  
* QTBUG-116305 Qt Creator 11.0.2  layout alignment disable  
* QTBUG-115578 Maybe TS file format documentation needs a correction?  
* QTBUG-116441 qdoc: Pages with multiple \ingroup commands lose  
navigation to parent \group  
* QTBUG-114862 qdbusviewer shows tab for system bus although no system  
bus is present  
* QTBUG-106380 Hello tr() example exits immediately after being run  
* QTBUG-115448 qttools -unity-build-batch-size 100000 fails  
* QTBUG-116534 Add \examplecategory to qthelp  
* QTBUG-116536 Add \examplecategory to qtassistant  
* QTBUG-111873 qt_attributions.json files should be valid JSON  
* QTBUG-115686 qt5.git build of qttools/examples places .ts files in  
SRCDIR, not BUILDDIR  
* QTBUG-115962 lupdate generates invalid translation  
  
### qttranslations  
* QTBUG-115634 qttranslations configure takes ages on CMake 3.27  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-111748 [Turkish] Inconsistent translations  
  
### qtdoc  
* QTBUG-114529 ANDROID_NDK_ROOT example has wrong version  
* QTBUG-114759 add_library cannot create target "CustomControls" because  
another target with the same name already exists  
* QTBUG-114848 Document Viewer looks broken in 6.5.2 examples  
* QTCREATORBUG-29330 Widget designer standard icons invisible on macOS  
* QTBUG-114592 todolist demo fails to configure  
* QTBUG-115343 Submodule update at 6.5 fails  
* QTBUG-115961 Documentation about building Qt for iOS from source  
requires corrections  
* QTBUG-114998 Example can't run, missing module  
* QTBUG-113300 The documentation "How to Create Qt Plugins" seems to  
need a review and update  
* QTBUG-116149 Deploying QML Applications: wrongly instructs to use  
declarative instead of quick  
* QTBUG-116580 "Selected Material Icons" attribution shown twice  
* QTBUG-110921 Documentation for building iOS apps is plain wrong  
* QTBUG-114396 Change "OpenGL" to "Graphics API"  
* QTBUG-115108 FX_Material_Showroom fails to compile due to long paths  
* QTBUG-115247 \target after \row generates invalid HTML  
  
### qtlocation  
* QTBUG-115359 QGeoManeuver is exported twice  
* QTBUG-114080 QML module documentation should move out of "List of  
types" page  
  
### qtpositioning  
* QTBUG-114657 [SatelliteInfo] The app stops responding after some time  
on macOS  
* QTBUG-115361 QGeoSatelliteInfo is exported twice  
* QTBUG-115217 NMEA SatelliteInfo Simulation mode stops providing  
updates  
* QTBUG-114080 QML module documentation should move out of "List of  
types" page  
  
### qtconnectivity  
* QTBUG-116563 [REG 6.4 -> 6.5] ISO7816 smart cards are considered to be  
NDEF tags  
* QTBUG-116580 "Selected Material Icons" attribution shown twice  
  
### qtwayland  
* QTBUG-114671 Crash without input device connected  
* QTBUG-114995 tst_qgraphicsanchorlayout crash with QtWayland failed on  
Ubuntu 22.04, GNOME  
* QTBUG-115112 Key injection fails in QML test  
* QTBUG-115757 [REG: 6.5.1-6.5.2] Drag and Drop segfaults programs  
* QTBUG-116051 QMenuBar doesn't open neighbouring menus on mouseover  
* QTBUG-97037 DragHandler / startSystemMove window move issue with QT6  
Webengine on Wayland  
  
### qt3d  
* QTBUG-100386 Crash in GLTFImporter::commonMaterial  
* QTBUG-116229 Please fix Qt3DCore documentation  
* QTBUG-116354 Qt3D - Enable texture array  
* QTBUG-116494 Documentation for QCylinderMesh misses Detailed  
Description  
  
### qtserialbus  
* QTBUG-114619 QCanDbcFileParser fails to parse non-ASCII characters  
like '°'  
  
### qtwebengine  
* QTBUG-113806 Chromium attributions missing from 'Licences used in Qt'  
docs  
* QTBUG-114339 FAIL!  : qmltests::WebEngineViewSingleFileUpload::test_ac  
ceptSingleFileSelection(test.txt)  
* QTBUG-103518 QML WebView scrolling events are picked up by DragHandler  
and Flickables behind it  
* QTBUG-114117 [WebEngine] Incorrect name of the app is shown in the  
system location permission pop up  
* QTBUG-114953 PdfMultiPageView: Very poor memory performance when  
zooming in/out of long documents  
* QTBUG-113512  WebEngineView not visible in Designer on macOS  
* QTBUG-114471 Recipe browser starts in upside down mode  
* QTBUG-113981 QPdfView does not scroll reliably with mouse wheel event  
(two finger sliding on touchpad)  
* QTBUG-113251 [REG 6.4 -> 6.5] Context menu functionality in devtools  
broken  
* QTBUG-115365 QWebEngineCertificateError is exported twice  
* QTBUG-99555 [RE: 6.2.1->6.2.2] macdeployqt fails to produce  
notarizable packages  
* QTBUG-115844 qtwebengine ignores some key remaps  
* QTBUG-115976 Dev tools not hidden with closing cross  
* QTBUG-114752 Crash with  --device=software when running on battery  
* QTBUG-114875 Cannot detect Visual Studio when configuring QPdf and  
QWebEngine  
* QTBUG-115994 Duplicate character when long-pressing for accented char  
on macOS/webengine  
* QTBUG-115753 ERROR: AddressSanitizer: heap-use-after-free  in  
tst_origins  
* QTBUG-116445 [REG][Windows] Crash on  
NativeSkiaOutputDevice::releaseTexture() with nullptr access  
* QTBUG-113551 Update documentation for limitation building QtPdf for  
Android with supported  LTS versions  
* QTBUG-105342 Test on qemu are very flacky  
* QTBUG-113369 dark mode enabled causes crashes on specific sites  
* QTBUG-115188 QtWebEngine use after free in Extensions GetPreferences  
  
### qtwebview  
* QTBUG-114495  FAIL!  : tst_QWebView::load()  
  
### qtcharts  
* QTBUG-114221 Charts API Documentation Snippets broken, Examples  
broken.  
* QTBUG-113195 QtCharts/QXYSeries::colorBy method behave incorrectly  
after points are selected in QScatterSeries.  
* QTBUG-114943 Crash in Qt Audio Example on iPhone with Qt Kit 6.2.9 for  
iOS  
* QTBUG-115072 Crash while clicking on scatter points to perform  
selection  
* QTBUG-115977 QML Charts Galleryu example: Charts are hard to read on  
Android  
* QTBUG-116647 Application hangs on calling QXYSeries::sizeBy and  
QXYSeries::colorBy methods for a large number of scatter points.  
* QTBUG-114080 QML module documentation should move out of "List of  
types" page  
* QTBUG-116535 Add \examplecategory to qtcharts (1 update left)  
  
### qtvirtualkeyboard  
* QTBUG-116078 [REG] Behavior breakage in Qt 6.5: Virtual keyboard style  
qrc import path changed  
* QTBUG-108030 Virtual keyboard basic example freezes on Android  
* QTBUG-116432 Virtual keyboard import version number from Qt 5.15 does  
not work in Qt 6.5 version  
  
### qtspeech  
* QTBUG-115363 QVoice is exported twice  
* QTBUG-113820 Can't run Quick Speech Example on Android  
  
### qtremoteobjects  
* QTBUG-115458 QRemoteObjectRegistry has incorrect info about  
QRemoteObjectSourceLocation(s)  
  
### qtquick3d  
* QTBUG-114557  FAIL!  : tst_RotationDataClass::test_construct()  
Compared values are not the same  
* QTBUG-114313 [Reg: 5.15 -> 6.2/6.5?] QQuaternion::getAxisAndAngle()  
can produce NaN, even when normalized  
* QTBUG-105918 REG: Jittery skeletal animations  
* QTBUG-106371 CMake Build Fails with "Some targets in this export were  
already defined" when using system assimp draco  
* QTBUG-115064 'Some (but not all) targets in this export set were  
already defined' error during building from source process  
* QTBUG-115522 Unshaded CustomMaterial shader does not receive per-  
vertex COLOR attribute from custom QQuick3DGeometry  
* QTBUG-115362 ShaderBuildMessage is exported twice  
* QTBUG-114110 QtQuick3d scene freeze when deleting many nodes  
* QTBUG-116559 Quick3D doesn't compile with -trace lttng  
* QTBUG-115450 qtquick3d -unity-build-batch-size 100000 fails  
  
### qt5compat  
* QTBUG-115467 Qt 6 QML Documentation: Wrong example for  
"verticalOffset"  
  
### qtcoap  
* QTBUG-115501 [Qt CoAP] CI integrations pass even when the tests fail  
  
### qtopcua  
* QTBUG-113504 [MSVC] Qt6 failed to build due to error C2362 on Windows  
with option /permissive-  
  
### qtquick3dphysics  
* QTBUG-114111 Crash when destroying a body with scale  
* QTBUG-114183 Collision shape calculates orientation incorrectly when  
parent has scale  
* QTBUG-115539 Missing dependencies in qmldir  
* QTBUG-114114 PhysX has ODR violations  
* QTBUG-117058 ERROR: AddressSanitizer: heap-use-after-free in  
tst_callback  
  
### qtgrpc  
* QTBUG-115032 -platform linux-clang-libc++ fails to compile  
qtprotobufgen  
* QTBUG-115055 Qt6Grpc package depends on system WrapgRPC to be found  
and be compatible  
* QTBUG-110107 RTA CMake test fails on 6.5.0  
* QTBUG-115057 when using qtgrpc, .proto files should appear in project  
hierarchy  
* QTBUG-115175 QtProtobuf nested message generation error  
* QTBUG-116043 configure fails with "PROTO_FILES list is empty"  
* QTBUG-116463 qt_add_protobuf() broken in 6.6.0-beta3 for VS2019 build  
system  
* QTBUG-116461 qt_add_protobuf() broken in 6.6.0-beta3 for WASM  
* QTBUG-115708 windows build failure when using protobuf  
GENERATE_PACKAGE_SUBFOLDERS  
* QTBUG-115180 QtProtobuf: Enum forward declaration is required  
  
### qtquickeffectmaker  
* QTBUG-114561 Material style highlighted & flat button shows no text  
  
Known Issues  
------------  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Amir Masoud Abdol  
Laszlo Agocs  
Anu Aliyas  
Dimitrios Apostolou  
Albert Astals Cid  
Mahmoud Badri  
Mate Barany  
Vladimir Belyavsky  
Nicholas Bennett  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
Mikolaj Boc  
Tatiana Borisova  
Joerg Bornemann  
Rym Bouabid  
Assam Boudjelthia  
Aurélien Brooke  
Kai Uwe Broulik  
Michael Brüning  
Olivier De Cannière  
John Chadwick  
Mike Chen  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Pranta Dastider  
Szabolcs David  
Marius Dege  
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
Joshua Goins  
Mikko Gronoff  
Kaj Grönholm  
Richard Moe Gustavsen  
Lucie Gérard  
Ralf Habacker  
Kamil Hajdukiewicz  
Heikki Halmet  
Amanda Hamblin-Trué  
Jøger Hansegård  
Inkamari Harjula  
Elias Hautala  
Jani Heikkinen  
Miikka Heikkinen  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Mats Honkamaa  
Martin Jansa  
Allan Sandfeld Jensen  
Jonas Karlsson  
Timothée Keller  
Michael Klein  
Friedemann Kleint  
André Klitzing  
Michal Klocek  
Jarek Kobus  
Sze Howe Koh  
Jarkko Koivikko  
Fabian Kosmale  
Volker Krause  
Konrad Kujawa  
Santhosh Kumar  
Kai Köhne  
Inho Lee  
Paul Lemire  
Kimmo Leppälä  
Wladimir Leuschner  
Thorbjørn Lindeijer  
Thiago Macieira  
Thorbjørn Lund Martsum  
Aaron McCarthy  
Ievgenii Meshcheriakov  
Leena Miettinen  
Jan Moeller  
Safiyyah Moosa  
Bartlomiej Moskal  
Marc Mutz  
Antti Määttä  
Martin Negyokru  
Andy Nichols  
Mårten Nordheim  
Dennis Oberst  
Pasi Petäjäjärvi  
Samuli Piippo  
Timur Pocheptsov  
Joni Poikelin  
Aleix Pol  
Cajus Pollmeier  
Lorn Potter  
Shyamnath Premnadh  
MohammadHossein Qanbari  
Liang Qi  
Khem Raj  
Matthias Rauter  
David Redondo  
Arno Rehn  
Topi Reinio  
Alexey Rochev  
Bernhard Rosenkränzer  
Shawn Rutledge  
Toni Saario  
Casimir Saastamoinen  
Ahmad Samir  
Philip Schuchardt  
Björn Schäpers  
Andy Shaw  
Venugopal Shivashankar  
Colin Snover  
Ivan Solovev  
Axel Spoerl  
Christian Strømme  
Tarja Sundqvist  
Lars Sutterud  
Tasuku Suzuki  
Jan Arve Sæther  
Morten Sørvig  
Samuel Thibault  
Ivan Tkachenko  
Jens Trillmann  
Paul Olav Tvete  
Peter Varga  
BogDan Vatra  
Doris Verria  
Tor Arne Vestbø  
Jannis Voelker  
Ville Voutilainen  
Jaishree Vyas  
Michael Weghorn  
Bernd Weimer  
Edward Welbourne  
Paul Wicking  
Piotr Wierciński  
Oliver Wolff  
Li Xinwei  
Semih Yavuz  
Vlad Zahorodnii  
JiDe Zhang  
Yuhang Zhao  
Eike Ziller  
Andrius Štikonas  
