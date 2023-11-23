Release note  
============  
Qt 6.6.1 release is a patch release made on the top of Qt 6.6.0.  
As a patch release, Qt 6.6.1 does not add any new functionality but provides  
bug fixes and other improvements and maintains both forward and backward  
compatibility (source and binary) with Qt 6.6.0.  

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
* 66d10dc253 Document q(u)int128 and QT_SUPPORTS_INT128  
Added qint128 and quint128 typedefs on platforms that support them.  
  
* 321dcd1d1d Long live Q_(U)INT128_C()!  
Added Q_INT128_C() and Q_UINT128_C() macros to create qint128 and  
quint128 literals in a platform-independent way.  
  
* d0ed5db781 Fix crash when reading corrupt font data  
Fixed a possible crash that could happen when loading corrupted font  
data.  
  
* 29d20a781c QMessageBox::about / aboutQt - use native modal dialog on  
iOS  
QMessageBox::about(Qt) now shows native, modal dialog.  
  
* 406ad89a3b SQLite: Update SQLite to v3.43.1  
Updated SQLite to v3.43.1  
  
* 8e14e13c16 [docs] Fix \since for qHash(qfloat16)  
Delete the old entry for qHash(qfloat16), keep the one from this  
commit.  
  
* eb1a6263ce QDockWidget: ignore close event if DockWidgetClosable is  
not set  
A floating dockwidget that doesn't have the DockWidgetClosable feature  
flag set can no longer be closed by a call to QWidget::close or a  
corresponding keyboard shortcut (such as Alt+F4).  
  
* a92db9d5fa Fix renamed and duplicated namespaces in QXmlStreamWriter  
Fix renamed and duplicated namespaces in QXmlStreamWriter.  
  
* cec3d03d11 Un-deprecate qSwap()  
Un-deprecated qSwap().  
  
* 416081ef4f Use the actual target name as base name for android  
deployment settings  
The target name is used as a base name of android deployment settings,  
but not the OUTPUT_NAME property.  
  
* 47fad9f1e4 Remove framework-related functionality from syncqt  
'-framework' and '-frameworkIncludeDir' arguments were removed. The  
related logic is moved to cmake scripts.  
  
* a8aa762424 revert "xkbcommon: make shortcuts persistent across  
layouts"  
A change in 6.6.0 that resulted in keyboard shortcuts not respecting  
the user's active layout has been reverted.  
  
* 7b1b40eb5e QPointer: fix missing converting move-assignment operator  
Added missing converting move-assignment operator. This is forwards-  
compatible with Qt 6.6.0: compiling against 6.6.0 will just use the  
lvalue overload.  
  
* b34a911b07 SQLite: Update SQLite to v3.43.2  
Updated SQLite to v3.43.2  
  
* 6173f053a0 Update bundled libjpeg-turbo to version 3.0.1  
libjpeg-turbo was updated to version 3.0.1  
  
* 1781d77092 Align QKeySequence behavior between macOS and iOS  
Keyboard shortcuts now follow the same scheme as on macOS, with their  
native representation expressed via the ⌘, ⌥, and ⌃ modifiers. Use  
Qt::AA_MacDontSwapCtrlAndMeta to override this.  
  
* 9224284f7a SQLite: Update SQLite to v3.44.0  
Updated SQLite to v3.44.0  
  
* 89dd5ab630 Cocoa MessageBox: don't use native message box if detailed  
text is set  
On Apple platforms, the native message box is no longer used when  
detailed text is set.  
  
* ce6a81a6f0 Windeployqt: add options to deploy/block plugins  
Windeployqt now has options that allow for custom plugin deployment.  
Users can include or exclude them, either individually, or by type.  
  
### qtsvg  
* b785c8c Fix crash when reading text with line breaks  
Fixed a regression where the application would crash on certain SVG  
files.  
  
### qtdeclarative  
* 6ff4d3b69a Fix translucent NativeRendering text on transparent window  
Fixed an issue where NativeRendering text with a translucent color  
combined with a transparent window would cause unexpected translucency  
effects on opaque parts of the scene.  
  
* 60ee43d08f Fix missing paragraph containing object replacement char  
Fixed an issue where a paragraph containing the Object Replacement  
Character (U+FFFC) would be invisible.  
  
### qttools  
* de619b5ee lupdate: remove number heuristics  
Removed the number heuristics feature. Users are advised to avoid hard-  
coded numbers in translatable strings and use QString::arg instead.  
  
### qt3d  
* a43c740d4 Fix Race Condition in NodePostConstructorInit::processNodes  
Fix Race Condition in NodePostConstructorInit::processNodes  
  
### qtimageformats  
* 3904372 Update bundled libwebp to version 1.3.2  
Update bundled libwebp to version 1.3.2  
  
* 573966a Update bundled libtiff to version 4.6.0  
Bundled libtiff was updated to version 4.6.0  
  
### qtwebengine  
* 5c442bb23 Fix corrupted load/fetch state on start up in case of  
NoCache  
Switching profile to NoCache do not longer implicitly removes cache  
from old data store.  
  
### qt5compat  
* 9ba1334 SAX: Remove unused QtXml/qtxmlglobal.h header inclusion  
The QtCore5Compat/qxml.h header no longer includes QtXml/qtxmlglobal.h.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-115752 stack-use-after-return in tst_assetimport  
* QTBUG-115196 QMenubar only works once  
* QTBUG-116769 [Boot2Qt] QMenu not re-appearing after closing in widgets  
app  
* QTBUG-116929 Make a decision regarding QFont's feature API  
* QTBUG-116357 Build fails with -march=native  
* QTBUG-111698 Build fails with -march=amdfam10  
* QTBUG-107072 build chooses unavailable hardware flags  
* QTBUG-116925 q(u)int128 are not documented  
* QTBUG-117021 ASSERT: "self.window" in file qiosviewcontroller.mm, line  
110  
* QTBUG-116973 [REG 6.5 -> dev] CMakeList: Can't rebuild after changes  
with -no-opengl  
* QTBUG-112957 Toplevel developer build fails to link: undefined symbol:  
vtable for QNetworkAccessDebugPipeBackendFactory  
* QTBUG-116920 FAIL!  : tst_QGeoAreaMonitorSource::tst_monitor() 'obj !=  
nullptr' returned FALSE.  
* QTBUG-116731 QtFuture::whenAll() leaks when one of the futures is  
already finished  
* QTBUG-117052 Condition of feature ipc_posix erroneously evaluates to  
FALSE  
* QTBUG-116821 QNativeIpcKey: UB (inactive union member used)  
* PYSIDE-2460 QOpenGLContext is not valid when aboutToBeDestroyed is run  
* QTBUG-115832 iOS: About Qt dialog displays incorrectly when launched  
from menu  
* QTBUG-117097 [Windows] Sporadic crash on  
QNetworkConnectionEvents::getNetworkConnectionFromAdapterGuid()  
* QTBUG-117200 Reg -> 6.6b4: Exit warning :"QItemSelectionModel:  
Selecting when no model has been set will result in a no-op" from apps  
with  sort proxy filter model  
* QTBUG-116890 Typo in the document  
* QTBUG-116752 Floatable non-closable dock widget can be closed when  
floating, but cannot be reopened  
* QTBUG-117109 QBindable example fails to configure  
* QTBUG-116903 [REG 6.5.0-6.5.2][macOS] Emoji edit menu items are not  
visible in a specific case  
* QTBUG-117383 QFile::moveToTrash does nothing but returns true  
* QTBUG-115486 Item view headers with stylesheets include space for sort  
indicator on all sections  
* QTBUG-117483 QWeakPointer's converting move constructor is not  
threadsafe  
* QTBUG-117482 should be "external" instead of  'exernal'  
* QTBUG-116926 Table view delegate(derived from QStyledItemDelegate) can  
not get new value when Spinbox loses focus and  
spinbox->setKeyboardTracking(false)  
* QTBUG-117416 RPi4 with Vulkan: choosing the output screen does not  
work  
* QTBUG-117412 Vulkan instance validation error on Raspberry Pi 4  
* QTBUG-75456 Streaming XMLs from reader to writer changes namespace  
name  
* QTBUG-109465 [REG: 5.15 → 6.2] binding doesn't update when it should  
* QTBUG-117509 Examples that set OUTPUT_NAME will not build for Android  
* QTBUG-115161 Crash in QAccessibleComboBox::focusChild()  
* QTBUG-117518 syncqt: qt_sync_skip_header_check header not skipped  
* QTBUG-117644 Orca screen reader doesn't announce combobox value when  
focused  
* QTBUG-117674 [Reg 5.15->6.x] CONFIG += qt causes failure to link to  
WinMain  
* QTBUG-107598 HorizontalHeaderView crashes the app if it's synced to  
model changed from bg thread  
* QTBUG-109718 QWebSocket cannot handle HTTP 407 response ("Proxy  
Authentication Required")  
* QTBUG-102196 QDockWidget: wrong mouse cursor icon used when dock  
widget floating, has custom title bar & contains window container  
* QTBUG-115233 OpenSSL-3 QCryptographicHash leaks  
OSSL_PROVIDER_load()'ed objects  
* QTBUG-89904 Possible error in Qt 6 "Container Classes" documentation  
* QTBUG-114437 REG: Android: Layout in display cut mode being overridden  
to short edges always  
* QTBUG-96877 Qt6 won't render into cutout area (regression)  
* QTBUG-117745 Warning message from app compiled with XCode 15  
* QTBUG-117787 Cached network requests leak memory  
* QTBUG-117764 [REG 6.5.1->6.5.2] Setting a DockWidget title when the  
DockWidget is closed causes windowTitle to be null or desync  
* QTBUG-117820 xcb: Adding and removing devices while the application is  
running may spam the application output with unregistered device  
messages  
* QTBUG-117705 Incorrect documentation for QStringEncoder and  
QStringDecoder  
* QTBUG-117817 Windeployqt --qpaths  
* QTBUG-117473 crash occuring at shutdown  
* QTBUG-113486 Inactive components not correcly rendered in dark-mode  
environments in Qt 6.5.0  
* QTBUG-117740  Insufficient qreal validation in  
./src/gui/painting/qpdf.cpp produces broken PDF with large coordinates  
* QTBUG-109025 High DPI scaling breaks Mouse/Stylus on Android  
* QTBUG-117950 qxkbcommon.cpp:242:16: error: 'XKB_KEY_dead_lowline' was  
not declared in this scope  
* QTBUG-117459 windeployqt: Explicitly disabled plugins are still  
deployed  
* QTBUG-117870 icx on windows has an issue with int128 6.6.0 rc  
* QTBUG-117153 lastest commit for QLoggingCategory trigger compile error  
in other impotant project  
* QTBUG-112879 [QT6.5] gtk3 theme glitches when moving the window  
* QTBUG-117514 QFuture::then marked as private  
* QTBUG-86297 Qt does not handle the ACTION_POINTER_UP  event on android  
* QTBUG-117490 QNetworkInformation:loadBackendByFeatures(QNetworkInforma  
tion::Feature::Reachability) doesn't work in snap  
* QTBUG-118041 selftests don't appear to respect ASAN_OPTIONS  
environment variable  
* QTBUG-116167 Duplicate requests of QNetworkAccessManager do not work  
* QTBUG-115446 qcocoanativeinterface.mm:4:10: fatal error:  
'QtGui/private/qopenglcontext_p.h' file not found  
* QTBUG-117779 [Reg 6.5.3->6.5.2] Showing a secondary Window is broken:  
the second Window unexpectedly depends on the main Window position  
* QTBUG-117709 Protobuf CMakefiles don't work when protobuf libraries  
aren't installed  
* QTBUG-117242 QtStartUpFunction is written as QtCleanUpFunction  
* QTBUG-118075 macdeployqt does not sign any libraries when the  
-exectuable parameter is used  
* QTBUG-115992 Window containing native windows window is excessively  
repainted on move  
* QTBUG-117606 QLineEdit loses its frames when hovering  
* QTBUG-118117 [REG 6.4.3->6.5.3] Opening a modeless QDialog removes a  
previously set taskbar icon overlay from native API on Windows 11  
* QTBUG-108323 qt-cmake.bat configures invalid compiler  
* QTBUG-118192 QNetworkAccessManager hang with low integrity level (low  
IL) sandboxing  
* QTBUG-5903 When a QCOMPARE of two lengthy values fails, the debugging  
output is incomplete  
* QTBUG-117215 "A minimal RSS listing application" example has wrong  
metadata  
* QTBUG-118170 QRhi static constants causing missing symbols  
* QTBUG-118199 Flaky tst_QEventLoop::processEvents on QNX  
* QTBUG-118229 QNetworkDatagram destructor uses private API  
* QTBUG-117367 [Reg 5.15 ->6.x] Android: Unable to dismiss "teardrop"  
cursor from text inputs  
* QTBUG-117804 Incomplete JPEG writing after libjpeg-turbo 3.0.0 upgrade  
* QTBUG-106527 AT-SPI2: Incorrect sizes returned for WINDOW and PARENT  
coordinates  
* QTBUG-118320 [Reg 6.4.3->6.5] Application window not active after  
closing message box  
* QTBUG-104905 Window modal not blocking ancestor window interaction on  
Mac  
* QTBUG-118419 [Reg 6.4->6.5] Cannot create button with menu in message  
box  
* QTBUG-118308 [Reg 6.4->6.5] QMessageBox::set(Default|Escape)Button  
does not work  
* QTBUG-118244 QVulkanWindow::grab() assumes RGBA which leads to  
inverted R and B channels  
* QTBUG-118586 QTimeZone::isTimeZoneIdAvailable is giving wrong result.  
* QTBUG-118315 Misleading documentation of QWaylandApplication  
* QTBUG-117428 [Reg 6.4->6.5] QWizard does not draw the buttons  
* QTBUG-118318 QStringConverter/Win doesn't handle resumption for  
encodings with more than 2 octets per character for convertToUnicode  
* QTBUG-118553 Incorrect composition when place a software-rendered  
widget over a OpenGL-based widget  
* QTBUG-115005 [Android] Text cursor handle visible out of the TextEdit  
clip region  
* QTBUG-118612 Large size cursor overlaps tooltips on linux  
* QTBUG-118649 tst_QGlyphRun fails with Linux on ARM  
* QTBUG-117533 QProcess does not work with thread sanitizer  
* QTBUG-111855 QSharedMemory no longer works using the old constructor  
after recent changes in dev  
* QTBUG-118241 QMessageBox::button(QMessageBox::Close)->setText() does  
not work  
* QTBUG-113165 Native text on macOS and iOS is not the same.  
* QTBUG-118703 Crash (divison by zero) in  
QLocaleData::applyIntegerFormatting()  
* QTBUG-118070 When configuring with debug info, installed libraries  
shoudn't be stripped  
* QTBUG-118227 QCryptographicHash broken with OpenSSL 3 (feature  
"openssl_hash")  
* QTBUG-118194 Adding QOpenGLWidget to FullScreen window breaks Full  
Screen  
* QTBUG-117713 [REG: 5->6] Scaling images with Qt::SmoothTransformation  
breaks them if scaled to smaller than 50% size  
* QTBUG-111952 tslib input plugin broken  
* QTBUG-113307 tslib input not working  
* QTBUG-118759 [Regr:6.5->6.6] QDateTime comparison performance  
regression on macOS  
* QTBUG-118741 Windows: QNetworkInformation does not report "metered"  
feaature  
* QTBUG-116550 [schannel] Qt warning "QIODevice::write (QTcpSocket):  
device not open"  
* QTBUG-116763 out-of-bounds operator+  
* QTBUG-118627 Build error for QNX, incomplete type QQnxWindowMapper  
* QTBUG-106262 Mouse events use rounded float local pos  
* QTBUG-93368 Windows: QGuiApplication::primaryScreenChanged is not  
emitted when changing primary screen  
* QTBUG-118695 popup menu on QToolButton displays at wrong screen  
* QTBUG-116013 QHeaderView::resetDefaultSectionSize doesn't invalidate  
cached size hints / update view  
* QTBUG-116295 Qt build with SSL3, is not picking up SSL3  
* QTBUG-118899 REG: QPrintDialog no longer opens on Windows  
* QTBUG-118814 [OpenSSL 3.0] QCryptographicHash::Keccak_256 produces the  
same output as Sha3_256  
* QTBUG-118716 [REG: 6.5 -> 6.6] windows: Cyclical QCheckBox setChecked  
leads to stack overflow  
* QTBUG-104688 State variable in QCheckBox::stateChanged should be  
emitted as Qt::CheckState instead of int  
* QTBUG-118667 QIcon::addFile() with an invalid filename results in  
QFile::isNull() == false  
* QTBUG-114971 QAndroidBinder: implementation for native methods missing  
* QTBUG-118631 QBitArray::testBit with unsigned enum fails to build with  
gcc13  
* QTBUG-117494 QSvgRenderer produces different results randomly when it  
is run the same way  many times  
* QTBUG-118580 QPrinter::setPageLayout does behaves different on windows  
and Linux  
* QTBUG-117499 Mouse scroll events stop working with `-platform  
windows:reverse`  
* QTBUG-28463 Unable to use Arabic right to left (RTL) layout in the  
title bar of own custom dialog.  
* QTBUG-101219 Hidden tabs via QTabWidget::setTabVisible are still  
available  
* QTBUG-117206 QT_ANDROID_EXTRA_LIBS ignored for secondary ABIs  
* QTBUG-116757 QMessageBox does not show hyperlinks on macOS  
* QTBUG-118992 Reg6.4->6.5 QMessageBox Hide/Show detailed section is  
gone  
* QTBUG-118870 Icon of a cell with a background color disappears if a  
stylesheet is used for QTreeView::indicator  
* QTBUG-117997 WASM: generated index.html lacks exit code details  
* QTBUG-117910 [windeployqt] The QtPDF module will always be deployed if  
it's installed  
* QTBUG-116349 Doc: Documentation of qAsConst missing  
* QTBUG-114760 tst_QComboBox::popupPositionAfterStyleChange is flaky  
* QTBUG-117900 [REG 5.15.2->6.5.1] Behavioural inconsistency when  
reparenting QStandardItems  
* QTBUG-89145 QStandardItemModel takeItem / takeChild does not emit the  
right signals  
* QTBUG-116532 tst_QStandardItemModel leaks memory in multiple test  
cases  
* QTBUG-119068 QSystemTrayIcon - unable to reset context menu  
* QTBUG-119053 macOS: QSystemTrayIcon::activated signal slot is called  
multiple times if QSystemTrayIcon::setContextMenu is called from it  
* QTBUG-104641 QDial: division by zero while changing minimal or maximum  
value  
* QTBUG-118993 MSVC warns as error on stdext::checked_array_iterator in  
QtCore/qvector.h  
* QTBUG-117111 QProperty's documentation has a Note section which seems  
to be displayed in an unintended way  
* QTBUG-78737 Windows: Two menus instead of one appear by clicking on  
the QSystemTrayIcon  
* QTBUG-119044 CXXFLAGS='-D_GLIBCXX_DEBUG' build crashes (e.g. in  
sharedmemory example)  
* QTBUG-118133 Windows QPA:  QSystemIconTrayIcon::show() not working  
after calling hide()  
* QTBUG-105150 QStandardItem is using un-documented value of  
Qt::ItemDataRole  
* QTBUG-116297 QPainter::drawPixmap showing seams  
* QTBUG-116789 [REG] -platform linux-clang-libc++ -c++std c++2b fails to  
compile synctqt  
* QTBUG-108796 Some examples crash when running with Qt 6.5 kit  
* QTBUG-116017 [REG] tst_QDate::startOfDay_endOfDay_bounds() test  
failure  
* QTBUG-116445 [REG][Windows] Crash on  
NativeSkiaOutputDevice::releaseTexture() with nullptr access  
* QTBUG-116064 [REG SiC 6.4 -> 6.5] qHash(qfloat16(x)) is now ambiguous  
on GCC13  
* QTBUG-116076 qHash(qfloat16(x), seed) != qHash(float(x), seed) unless  
seed == 0  
* QTBUG-117120 Debian packages not installing  
* QTBUG-109444 Qt's CMake deployment API Error: Extra libraries copied  
* QTBUG-113645 QWindowsTheme::queryHighContrast: incorrect parameters  
passed to SystemParametersInfo for SPI_GETHIGHCONTRAST  
* QTBUG-113123 Mixed indexes in QListWidget when setSortingEnabled is  
True  
* QTBUG-116483 qttools' CMake test test_uiplugin_via_designer fails  
* QTBUG-108761 QXkbCommon::keysymToQtKey does not correctly handle  
punctuation with modifiers under some keyboard layouts  
* QTBUG-110921 Documentation for building iOS apps is plain wrong  
* QTBUG-116784 iOS built with CMAKE is not uploadable on Appstore  
(Transporter)  
* QTBUG-109708 Startup crash in QRhiD3D11::endFrame() with nullptr  
access  
* QTBUG-117535 Cannot enable at-spi bridge with wayland  
* QTBUG-118116 QRhiWidget has no way to set flags on the top-level's  
QRhi  
* QTBUG-80953 Test failures on sparc  
* PYSIDE-2492 uic does not generate enumeration name into enum values  
causing type checking warnings  
* QTBUG-118211 Generation of alias targets for executable needs to be  
guarded  
* QTBUG-118569 crash in qschannelbackend  
QTlsPrivate::X509CertificateSchannel::QSslCertificate_from_CERT_CONTEXT  
* QTBUG-118578 Undocking tabbed widget from floating window creates  
empty redundant window  
* QTBUG-118579 Undocking tabbed widget from main window onto the  
floating window crashes app  
* QTBUG-118909 Touches cancelled when interacting with multiple windows  
* QTBUG-112479 Touch Drag doesn't cause mousePressEvent after Touch  
Press  
* QTBUG-119032 Mouse Release is not fired with touch screen  
* QTBUG-111873 qt_attributions.json files should be valid JSON  
  
### qtsvg  
* QTBUG-113042 Loading particular svg file takes too long  
* QTBUG-117944 [Qt SVG] QML Image bad source crashes application instead  
of error status (QSvgHandler::parse)  
  
### qtdeclarative  
* QTBUG-114144 qmllint: false positive [read-only-property] with  
QQmlListProperty  
* QTBUG-116289 Placing a HoverHandler on a Button makes it respond to a  
right-click.  
* QTBUG-116164 [Regr: 6.5.0->6.5.1] Broken "implicitWidth",  
"implicitHeight" bindings  
* QTBUG-116672 Application crashes when MenuItem text contains img tag  
* QTBUG-116795 QQuickBasicProgressBar::setColor() does nothing after  
initialization?  
* QTBUG-116681 QtCore Settings does not support ini files located in  
resources  
* QTBUG-116828 Aborting incubation may lead to a crash with some  
controls  
* QTBUG-116748 HorizontalHeaderView does not use  
QAbstractItemModel::roleNames()  
* QTBUG-117062 DelegatePage in Qt Quick Controls - Gallery example is  
broken  
* QTBUG-115227 VerticalHeaderView/TableView required properties go all  
over the place when using syncView  
* QTBUG-105080 FileDialog ignores fileMode : FileDialog.Save  
* QTBUG-116566 QML TableView: resizableColumns/resizableRows breaks the  
default interactive behavior  
* QTBUG-109444 Qt's CMake deployment API Error: Extra libraries copied  
* QTBUG-115485 QtQuick shapes example has misleading file names  
* QTBUG-117642 Crash when trying to trick property bindings  
* QTBUG-117361 qmlcachegen crashes in  
QQmlJSTypeResolver::adjustTrackedType  
* QTBUG-117077 qmllint does not allow 'print' as invokable method name  
* QTBUG-117513 Restore pthread_attr_init() to stackPropertiesGeneric()  
for FreeBSD  
* QTBUG-117789 QmlCompiler generates invalid code for unary operator+  
* QTBUG-117130 crash in tryLoadFromDiskCache with corrupted cache  
* QTBUG-117891 [REG 6.5.2 → 6.5.3] Unable to determine callable overload  
with QVariantMap  
* QTBUG-116804 QML incubation documentation issues  
* QTBUG-113785 Warn about  setContextProperty() in documentation  
* QTBUG-117880 Material 3 misaligns Button icon  
* QTBUG-118052 Text.NativeRendering causes text to show through.  
* QTBUG-101991 QML ListModel should document that it's a QAIM  
* QTBUG-116895 Missing docs for QML_ADDED_IN_VERSION,  
QML_REMOVED_IN_VERSION  
* QTBUG-118132 Failed to compile QML app with VS2019  
* QTBUG-117829 QML engine mis-converts QQmlListProperty  
* QTBUG-108883 Improve documentation on how to expose value types with  
enums to QML  
* QTBUG-118100 readonly property can be written via unqualified access  
* QTBUG-117451 private/qquickevents_p_p.h: No such file or directory  
when compiling a new Qt Quick Project with QML to C++ Compilation  
* QTBUG-93780 QML type versioning mechanism needs better documentation  
* QTBUG-117788 Assert due to cyclic dependencies  
* QTBUG-118089 Enums exposed to QML seem only working when the QML code  
gets compiled by qmlsc  
* QTBUG-118091 qmltc includes a non-existent qquickcheckbox_p_p.h  
* QTBUG-117384 [REG 6.4 → 6.5] Calling a Q_INVOKABLE function with a  
std::vector<long> parameter zeroes the vector  
* QTBUG-117479 Segmentation fault in qml debugger  
* QTBUG-118469 [REG 6.3.2 → 6.5.0] qsTranslate function no longer  
translates if directly bound to property  
* QTBUG-117922 Unexpected and inconsistent overload resolution when  
calling C++ from QML  
* QTBUG-117703 Unclear/missing documentation on using  
QML_FOREIGN_NAMESPACE  
* QTBUG-117793 QML-managed objects are garbage collected when stored in  
QML-declared list properties  
* QTBUG-117160 touchUngrabEvent is not implemented for qquickflickable  
* QTBUG-117969 Fix 'About Qt' dialog in File System Explorer  
* QTBUG-118514 [Reg 6.5 -> 6.6] Miscompilation of arithmetic operators  
* QTBUG-118069 Wrong position reported uppon touch release  
* QTBUG-118397 ~QQuickContainer() Crash when calling  
QQmlIncubator::abort  
* QTBUG-118591 Regression: QQmlScriptString::operator==() crashes  
* QTBUG-108449 Virtual keyboard does not appears until window focus  
changed to another application  
* QTBUG-118738 Not possible to exclude qtquicktimeline and qtquick  
control styles from the build  
* QTBUG-118744 Flaky crash (segfault) when running tst_inputpanel  
tst_plugin::test_fullScreenModeWordReselection  
* QTBUG-118163 Flaky race-condition in QuickTest when running  
tst_inputpanel built with ASAN  
* QTBUG-118525 Crash if popping a StackView causes a nested event loop  
to run  
* QTBUG-118460 Overlay.rotation gets discarded when window is resized  
* QTBUG-78441 Text disappears when using a U+FFFC unicode character  
* QTBUG-116606 unable to deselect text in text input using touch  
* QTBUG-117831 [REG: 6.5.2->6.5.3] Destroying active popup with dim  
layer leaves the dimming layer behind  
* QTBUG-118897 Qt Quick TableView performance issue when updating  
ContentY in onModelChanged  
* QTBUG-118461 Overlay's opacity is ignored  
* QTBUG-118237 Documentation of QML font weights is incorrect  
* QTBUG-117958 qt_add_qml_module does not register QML_SINGLETON classes  
if version starts with 0  
* QTBUG-118856 Placeholder text does not follow the set  
horizontalAlignment in Material style.  
* QTBUG-119065 Unable to reset tray icon menu for QML SystemTrayIcon  
* QTBUG-119024 Window position is bypassed by Wayland.  
* QTBUG-117917 HorizontalHeaderView with plain JavaScript array model  
crashes on flick  
* QTBUG-115579 Rebinding of property alias does not work for some  
aliases that refer to certain (grouped) properties  
* QTBUG-111570 ASSERT: "newInstance != d->animationInstance" in file  
qquickbehavior.cpp  
* QTBUG-101552 FileDialog(SaveFile) doesn't work correctly on KDE  
* QTBUG-108455 FileDialog.SaveFile mode is unusable  
* QTBUG-117700 StackView's enter transitions are broken when  
pushing/replacing onto an empty stack  
* QTBUG-117830 Crash on QQuickMultiEffectPrivate::updateEffectShaders()  
with nullptr access  
* QTBUG-117806 QQmlApplicationEngine::loadFromModule() not working on  
Android  
* QTBUG-117899 [REG 6.4->6.5] Binding Loops -> Wrong layout because of  
interruption  
* QTBUG-116589 Dynamic translations seem not working with  
QQmlApplicationEngine::loadFromModule()  
* QTBUG-118532 tst_qquickpopup::doubleClickInMouseArea and overlay are  
flaky on android  
* QTBUG-117968 Initialization behavior difference between precompiled  
and not compiled QML component  
* QTBUG-118470 no-gui build fails  
* QTBUG-117800 QmlCompiler generates bogus warning about internal  
conversion  
* QTBUG-118624 [WASM] Qt's internal shaders can easily conflict with  
user shaders  
* QTBUG-117795 Bogus compile warning  
* QTBUG-118636 Some missing content of the rich text table while  
displaying HTML file with TextArea  
  
### qtactiveqt  
* QTBUG-100657 Crash while receiving COM IDispatch events when  
initializing  
* QTBUG-96871 Crash on calling connect on   QAxObject source instance  
* QTBUG-119064 Build fail on Windows (reg 6.5.3 -> 6.6.0)  
  
### qtmultimedia  
* QTBUG-115935 REG: FFMPEG backend causes Android 13 crash on Launch  
* QTBUG-116901 QAudioSink: incorrect example code for stopping the  
device  
* QTBUG-115460 Camera crash on image acquire on Android  
* QTBUG-116526 Android camera crash in example project  
* QTBUG-114932 [DeclarativeCamera] Capture crashes the example  
* QTBUG-117086 [WMF] Excessive Qt warning "No audio output"  
* QTBUG-116991 QVideoFrame allocation broken for YUV422P  
* QTBUG-117056 ERROR: AddressSanitizer: heap-use-after-free in  
tst_QAudioSink::pullResumeFromUnderrun()  
* QTBUG-114083 [QtDeclarativeCamera] Popup list of available cameras is  
not available after changing the orientation  
* QTBUG-116688  QVideoFrame::toImage: failed to get textures for frame;  
format: 172 textureConverter null  
* QTBUG-116801 Path with space leads to crash Qmultimedia example  
* QTBUG-117599 Compilation error for FFmpeg with dynamically linked  
OpenSSL  
* QTBUG-115568 Missing type "QScreen" is referenced in qmltypes  
* QTBUG-115444 MediaPlayer has no sound on Android  
* QTBUG-116779 FFmpeg backend: GUI thread freezes when initializing an  
network source  
* QTBUG-118749 tst_qtexttospeech_qml (Failed)  
* QTBUG-117006 MediaPlayer::playing isn't always true when it should be  
* QTBUG-118624 [WASM] Qt's internal shaders can easily conflict with  
user shaders  
* QTBUG-118706 Crash on QWindowsMediaDevices::availableDevices() with  
nullptr access  
* QTBUG-117744 Bluish hue in video  
* QTBUG-115075 WebAssembly audio input not working  
* QTBUG-119087 MediaPlayer-Graphic&Multimedia-example Volume slider is  
being compressed and becomes unusable  
* QTBUG-116979 VideoOutput implicit size doesn't update until playback  
begins  
* QTBUG-116444 [Windows] Qt warning "Failed to retrieve default audio  
endpoint -2147023728"  
* QTBUG-116978 MediaPlayer::position cannot be declared in QML  
* QTBUG-107563 QMediaPlayer can't play AVI with Apple codecs  
* QTBUG-108403 FFmpeg backend doesn't work as expected  
* QTBUG-110498 QtMultimedia leaks a lot of memory on Windows when opengl  
contexts are shared  
* QTBUG-117099 Video jerks when playing (Windows backend)  
* QTBUG-110012 QML Video Example: example not displaying video  
* QTBUG-114954 Media Player Example: Default video does not play on  
Android  
* QTBUG-113980 Playing videos over network still an issue on Android  
* QTBUG-116782 FFmpeg backend: RTSP stream is very choppy in Qt,  
compared to FFplay  
* QTBUG-117528 [REG 6.3.2->6.5.2] QMediaPlayer always captures the audio  
device what blocks sleep mode on Windows  
* QTBUG-117612 [REG 6.3.2->6.5.2] Windows 10: CPU core stucks at minimum  
friequency  
* QTBUG-117919 REG: Qt6.7 QML MediaPlayer duration property doesn't  
update declaratively  
* QTBUG-111045 QSoundEffect not playing  
* QTBUG-118587 [WMF] Video position may exceed it's duration  
* QTBUG-101364 qmllint --compiler spurious error: QML State  
AnchorChanges: with type QQuickAnchorLine to QQmlScriptString of  
QQmlScriptString  
* QTBUG-118654 QMediaPlayer does not allow negative playback rate hence  
no rewinding possible  
* QTBUG-118510 Errors when building Qt with FFMpeg/vaapi on Ubuntu 20.04  
* QTBUG-108754 Video not stretched properly  
* QTBUG-116020 Audio from QMediaPlayer crackles and stutters on pause  
and resume  
  
### qttools  
* QTBUG-117145 Designer FTBFS  
* QTBUG-117214 "Multiple Inheritance" example - medata broken  
* QTBUG-116483 qttools' CMake test test_uiplugin_via_designer fails  
* QTBUG-117510 qdoc: Incorrect links to qhash-proxy.html page  
* QTBUG-116335 QMessageBox::options not correctly linked to  
* QTBUG-117974 CMake Error at  
qttools/src/assistant/qhelpgenerator/CMakeLists.txt:66  
(add_dependencies)  
* QTBUG-115720 \value followed by \table merges contents and breaks  
table  
* QTBUG-115537 [QML Docs] Image.fillMode enum documentation has a broken  
table formatting  
* QTBUG-117778 QDoc: section commands shadows inherited module state  
* QTBUG-118769 lupdate leaves behind .json files if it fails to load pro  
file  
* QTBUG-115166 qt_add_qml_module() causes non-Ninja generators to think  
that projects are never up-to-date  
* QTBUG-116833 QDoc generates .sha1 files for each qhp file, but they  
all contain wrong hash  
* QTBUG-115686 qt5.git build of qttools/examples places .ts files in  
SRCDIR, not BUILDDIR  
* QTBUG-115962 lupdate generates invalid translation  
* PYSIDE-2492 uic does not generate enumeration name into enum values  
causing type checking warnings  
  
### qtdoc  
* QTBUG-110846 Internationalization with Qt: Mention retranslateUi  
* QTBUG-110921 Documentation for building iOS apps is plain wrong  
* QTBUG-116987 DocumentViewer example broken because QPdfPageSelector is  
no longer a QSpinBox subclass  
* QTBUG-117691 DocumentViewer example does not find plugins at runtime  
* QTBUG-117694 Document Viewer example could not be build on Qt 6.7.0  
* QTBUG-54267 Qt Quick Calqlatr example does not properly reflect the  
current way of using Qt Quick  
* QTBUG-111272 "Porting to Android" only covers qmake  
* QTBUG-117089 qt_add_qml_module - what has changed between versions?  
* QTBUG-118104 Typo in the document  
* QTBUG-118577 Android Docs has non-compiling code-snippet.  
* QTBUG-118211 Generation of alias targets for executable needs to be  
guarded  
* QTBUG-118789 Target Devices used in Automated Testing is out-dated  
* QTBUG-118043 QML Media Player doesn't fit on smaller screens  
* QTBUG-116784 iOS built with CMAKE is not uploadable on Appstore  
(Transporter)  
* QTBUG-114437 REG: Android: Layout in display cut mode being overridden  
to short edges always  
* QTBUG-96877 Qt6 won't render into cutout area (regression)  
* QTIFW-3139 Online Installer 4.6.1 : Command Line Interface "-default-  
answer" "--accept-messages" doesn't work together  
* QTBUG-114375 User got stuck and is not taken back to the home in  
coffee example  
* QTBUG-117651 The Webassembly documentation has an incorrect  
target_link_options  
* QTBUG-114713 Enhancements in the Color Palette REST API example  
  
### qtlocation  
* QTBUG-118447 Here plugin does not support authentication via apiKey  
  
### qtpositioning  
* QTBUG-116645 [Android] providerList() returns NULL list  
  
### qtconnectivity  
* QTBUG-115370 Android device (Android12 Go Edition) cannot reconnect  
to BLE peripheral device  
* QTBUG-118895 No signals are emmited after error Failed to create  
pairing "org.bluez.Error.AuthenticationCanceled"  
  
### qtwayland  
* QTBUG-117067 ERROR: AddressSanitizer: heap-use-after-free in  
tst_seatv4::animatedCursor()  
* QTBUG-117932 Crash in texture orphanage  
* QTBUG-112161 Drag and drop with wayland display error  
* QTBUG-118042 cannot forward key event from compositor to client  
* QTBUG-111022 Custom Extension example not working on NVIDIA  
* QTBUG-118650 Qt wayland may freeze with no available buffer in  
QWaylandShmBackingStore if window show/hide very fast  
  
### qt3d  
* QTBUG-114037 [Android] Could not launch any app with Qt 3D module on  
Android 12  
* QTBUG-114036 [Android] Qt3D.Renderer.RHI.Backend: : Failed to build  
graphics pipeline: Creation Failed  
* QTBUG-116770 Race Condition or Crash in Qt3D due to Thread Affinity of  
NodePostConstructorInit::processNodes()  
* QTBUG-118399 https://doc.qt.io/qt-6/qt3drender-qmaterial.html example  
code misses parentheses  
* QTBUG-117065 ERROR: AddressSanitizer: memcpy-param-overlap in  
tst_AspectCommandDebugger::checkBufferTrim()  
  
### qtserialport  
* QTBUG-115205 QSerialPort does not properly set baud rate  
  
### qtwebchannel  
* QTBUG-115779 Webchannel's standalone example doesn't work when opened  
with CMake  
  
### qtwebengine  
* QTBUG-116159 Reg 6.4->6.5 QWebView with Q3DSurfaces does not renders  
* QTBUG-115722 [REG 6.6.0 beta2->beta3] QtWebengine not compiling from  
sources on SLES15_SP4  
* QTBUG-116738 qtwebengine Address Sanitizer test run: stack-use-after-  
return in tst_QQuickWebEngineView::savePage(SingleHtmlSaveFormat)  
* QTBUG-115994 Duplicate character when long-pressing for accented char  
on macOS/webengine  
* QTBUG-115753 ERROR: AddressSanitizer: heap-use-after-free  in  
tst_origins  
* QTBUG-116445 [REG][Windows] Crash on  
NativeSkiaOutputDevice::releaseTexture() with nullptr access  
* QTBUG-117119 Some Qt WebEngine documentation issues  
* QTBUG-117489 [REG 6.4 -> 6.5] Invalid QDataStream data when  
serializing uninited QWebEngineHistory  
* QTBUG-118505 REG: Qt WebEngine debug-and-release builds broken on  
macOS.  
* QTBUG-118157 [REG 6.5 -> 6.6] Crash in  
`GetServiceWorkerExtendedLifetimeOrigins` on Google Meet  
* QTBUG-85731 Screen sharing does not work on Google Meet  
* QTBUG-117751 building with -no-opengl produces errors in  
web_engine_context.cpp  
* QTBUG-117867 QWebEngineNewWindowRequest::openIn() breaks page  
interceptor  
* QTBUG-118455 Crash in Compositor::Observer::compositor() with nullptr  
access  
* QTBUG-117741 libvpx is not used  
* QTBUG-118655 Manual Deployment document of QtWebengine needs little  
update.  
* QTBUG-119023 WebEngine accessibility crash when clicking on a link in  
a list on macOS  
* QTBUG-113859 [REG 6.4->6.5] Accessibility crash when clicking on a  
link in a list on macOS  
* QTBUG-117658 QWebEnginePage property url is missing NOTIFY, not-usable  
from QML  
* QTBUG-117031 qmllint: Missing type information for WebEngine  
* QTBUG-113463 Build issues with symlinks  
* QTBUG-114859 When saving an mhtml page  
QWebEngineDownloadRequest::isSavePageDownload() returns false  
* QTBUG-116478 [Reg 5.14.2 -> 5.15.0] Significant performance decrease  
when loading QtWebEngine pages simultaneously in many windows  
* QTBUG-117624 Minor issues of QWebEngineDownloadRequest  
* QTBUG-116565 Cannot sign a WebEngine-based application with Qt 6.5.2  
(but OK with Qt 6.4.3, 6.3.2, 5.15.2)  
* QTBUG-117752 QWebEngineUrlRequestInterceptor not called on page, if  
the one set on the profile changed the info  
  
### qtwebview  
* QTBUG-69801 Qml WebView on Android eats touch events  
  
### qtcharts  
* QTBUG-113437 QML XYSeries bestFitLineColor doc type  
* QTBUG-118322 Fix licensing of Qt Charts examples  
* QTBUG-115274 "Qml Wheather" example causes 'Too many arguments'  
runtime error  
* QTBUG-114814 QColorAxis::setVisible method is not behaving as  
expected.  
* QTBUG-118669 Qt chart crash on showing context menu  
  
### qtvirtualkeyboard  
* QTBUG-116432 Virtual keyboard import version number from Qt 5.15 does  
not work in Qt 6.5 version  
* QTBUG-118324 Fix licensing of Qt VirtualKeyboard basic example  
* QTBUG-118565 VirtualKeyboard documentation incorrect  
* QTBUG-111873 qt_attributions.json files should be valid JSON  
  
### qtscxml  
* QTBUG-118050 Empty script element ends up invoking Q_UNREACHABLE()  
  
### qtspeech  
* QTBUG-117516 [Qt TextToSpeech] Cannot get the list of languages on  
android device  
* QTBUG-117824 configure -no-gui fails to build  
* QTBUG-118668 QTextToSpeech::synthesize under window does not get data  
  
### qtnetworkauth  
* QTBUG-117680 NetworkAuth examples do not show up in Qt Creator  
  
### qtremoteobjects  
* QTBUG-116151 Replica can crash with QHostAddress being called with a  
<null reference>  
* QTBUG-115458 QRemoteObjectRegistry has incorrect info about  
QRemoteObjectSourceLocation(s)  
  
### qtquick3d  
* QTBUG-113164 Crash when you have two models with same mesh in the  
scene, one with BakedLightmap and one without  
* QTBUG-116136 Memory leaks in Loader qml component  
* QTBUG-117619 [REG] Frustum culling broken in 6.6  
* QTBUG-117023 Picking and rotating don't work on bars after clicking  
buttons  
* QTBUG-118659 [REG 6.6.1 previous snapshot->6.6.1] example  
quick3d/proceduraltexture not launching  
* QTBUG-118806 Exporting functionality in the material editor is broken  
* QTBUG-118773 Baking emissive materials without shadow  
* QTBUG-116911 tst_surfacetest massive data test crash  
* QTBUG-111873 qt_attributions.json files should be valid JSON  
  
### qtshadertools  
* QTBUG-117780 qt_add_shaders is not executed if the target does not  
exist  
  
### qt5compat  
* QTBUG-117825 [REG 6.6.0 RC->6.6.0] static build on macOS fails,  
qt5compat(?)  
* QTBUG-116981 QTextCodec::toUnicode() behavior changed  
  
### qtopcua  
* QTBUG-117681 qtopcua is confused about SSL and OpenSSL  
  
### qtlanguageserver  
* QTBUG-118201 namespace "std" has no member "exception_ptr"  
  
### qthttpserver  
* QTBUG-114713 Enhancements in the Color Palette REST API example  
  
### qtquick3dphysics  
* QTBUG-117058 ERROR: AddressSanitizer: heap-use-after-free in  
tst_callback  
  
### qtgrpc  
* QTBUG-116679 -feature-protobuf-wellknowntypes not working for WASM  
* QTBUG-109332 qtprotobufgen generated invalid include when generating  
code from .proto file with no package  
* QTBUG-117066 ERROR: AddressSanitizer: heap-use-after-free in  
QtGrpcClientServerStreamTest::Deadline()  
* QTBUG-118996 Memory leak in qprotobufserializer.h  
  
### qtgraphs  
* QTBUG-117024 Labels cast shadows, but they should not  
* QTBUG-117213 Fix example category for qtgraph examples  
* QTBUG-116398 widget gallery crashes with surfacegraph  
* QTBUG-116911 tst_surfacetest massive data test crash  
* QTBUG-116823 Picking the surface graphs after changing ranges is  
inaccurate  
* QTBUG-118420 6.6 build requires OpenGL though req removed from cmake  
* QTBUG-118467 Qt Design Studio does not show graph properties  
  
### qtapplicationmanager (Commercial only)  
* QTBUG-117980 CMake install fails on appman for Qt/QNX windows build  
  
### qtinterfaceframework (Commercial only)  
* QTBUG-115221 Add support for WebAssembly in the autotests  
  
### qtinsighttracker (Commercial only)  
* QTBUG-117916 Only enabling QtInsightTracker in C++ side only works for  
MSVC  
* QTBUG-112415 QtInsighttracker component not sending data to QtInsight  
server on Android platforms  
* QTBUG-119043 Events are not sent in the sync value set in  
qtinsight.conf  
  
### qtvncserver (Commercial only)  
* QTBUG-115835 Dependencies.yaml should mention Qt Shader Tools  
  
Known Issues  
------------  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Amir Masoud Abdol  
Laszlo Agocs  
Dmitrii Akshintsev  
Anu Aliyas  
Dimitrios Apostolou  
Viktor Arvidsson  
Albert Astals Cid  
Mate Barany  
Vladimir Belyavsky  
Nicholas Bennett  
Eskil Abrahamsen Blomfeldt  
Tatiana Borisova  
Joerg Bornemann  
Rym Bouabid  
Assam Boudjelthia  
Kai Uwe Broulik  
Michael Brüning  
Alex Bu  
Olivier De Cannière  
Mike Chen  
Andreas Cord-Landwehr  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Szabolcs David  
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
Simo Fält  
Robert Griebl  
Jan Grulich  
Kaj Grönholm  
Richard Moe Gustavsen  
Lucie Gérard  
Mikko Hallamaa  
Jøger Hansegård  
Inkamari Harjula  
Tero Heikkinen  
Jani Heikkinen  
Miikka Heikkinen  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Dominik Holland  
Andreas Holzammer  
Allan Sandfeld Jensen  
Tim Jenssen  
Jonas Karlsson  
Timothée Keller  
Kurt Kiefer  
Kristof Kiszel  
Friedemann Kleint  
Michal Klocek  
Lars Knoll  
Sze Howe Koh  
Jarkko Koivikko  
Tomi Korpipaa  
Tomi Korpipää  
Fabian Kosmale  
Volker Krause  
Anton Kudryavtsev  
Konrad Kujawa  
Santhosh Kumar  
Jonas Kvinge  
Kai Köhne  
Inho Lee  
Paul Lemire  
Wladimir Leuschner  
Lorenzo Lucignano  
Thiago Macieira  
Sergio Martins  
Sérgio Martins  
Frank Meerkötter  
Leena Miettinen  
Safiyyah Moosa  
Bartlomiej Moskal  
Marc Mutz  
Antti Määttä  
Martin Negyokru  
Andy Nichols  
Mårten Nordheim  
Dennis Oberst  
Samuli Piippo  
Timur Pocheptsov  
Milla Pohjanheimo  
Joni Poikelin  
Cajus Pollmeier  
Rami Potinkara  
Lorn Potter  
Sakaria Pouke  
Liang Qi  
Khem Raj  
Matthias Rauter  
Arno Rehn  
Topi Reinio  
Huang Rui  
Shawn Rutledge  
Ahmad Samir  
Philip Schuchardt  
Thomas Senyk  
Sami Shalayel  
Andy Shaw  
Harald Sitter  
Kristoffer Skau  
Ivan Solovev  
Axel Spoerl  
Christian Strømme  
Tarja Sundqvist  
Lars Sutterud  
Tasuku Suzuki  
Jan Arve Sæther  
Morten Sørvig  
Orkun Tokdemir  
Jens Trillmann  
Paul Olav Tvete  
Esa Törmänen  
Sami Varanka  
Peter Varga  
BogDan Vatra  
Doris Verria  
Tor Arne Vestbø  
Jannis Voelker  
Alexander Volkov  
Juha Vuolle  
Jaishree Vyas  
Michael Weghorn  
Bernd Weimer  
Edward Welbourne  
Paul Wicking  
Piotr Wierciński  
Jakub Wincenciak  
Weng Xuetian  
Lu YaNing  
Semih Yavuz  
Zhao Yuhang  
Vlad Zahorodnii  
Yuhang Zhao  
Fredrik Ålund  
