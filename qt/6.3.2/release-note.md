Release note  
============  
  
Qt 6.3.2 release is a patch release made on the top of Qt 6.3.1.  
As a patch release, Qt 6.3.2 does not add any new functionality but provides  
bug fixes and other improvements and maintains both forward and backward  
compatibility (source and binary) with Qt 6.3.1.  

For detailed information about Qt 6.3, refer to the online documentation  
included in this distribution. The documentation is also available online:  
  
https://doc.qt.io/qt-6/index.html  
  
The Qt version 6.3 series is binary compatible with the 6.2.x series.  
Applications compiled for 6.2 will continue to run with 6.3.  
  
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
* 6a2f987c08 QCOMPARE/QVERIFY: fix huge pessimisation in QTestResult  
Optimized successful QCOMPARE and QVERIFY for an up to 2x speedup.  
  
* 1b3dbd24c0 xcb: fix missing initialization of m_cursor  
Fixed crash when no monitorInfo is available (e.g. VNC).  
  
* d7b24b469c Fix font rendering when Qt is configured with -no-harfbuzz  
Fixed font layouts when Qt was configured without Harfbuzz.  
  
* a067ae3d76 CoreText: Fix fonts with synthetic stretch  
Fixed a bug where synthetically stretched fonts would get the wrong  
advances and sometimes glyphs would be clipped.  
  
* 98b9b719c7 QPromise: run continuation(s) on destruction  
QFuture now runs its continuations when its associated QPromise has  
been destroyed. Previously, if a QFuture was canceled because the  
associated QPromise has been destroyed, its continuations were skipped.  
  
* 9334e06bdf Always update QPalette resolve mask, regardless of QBrush  
change  
Always update resolve mask in QPalette::setBrush, even if the value of  
brush has not changed.  
  
* 9249bd8404 SQLite: Update SQLite to v3.39.2  
Updated SQLite to v3.39.2  
  
### qtdeclarative  
* 86973d9f33 FileDialog: make selectedFile writable  
FileDialog's selectedFile property can now be set to an initially  
selected file.  
  
* 3baef2b73b QQmlDebug: reliably print the debugger warning  
The warning about enabled debuggers is now printed when at least one  
translation unit in the final executable requests it, independent of the  
order in which translation units are linked/initialized.  
  
* ea92763900 Fix TextEdit/TextArea mouse cursor shape handling logic  
TextEdit and TextArea now set their own mouse cursors more  
consistently, but without regard for any external call to setCursor().  
  
* 4f13770dda Fix SplitView containmentMask hit testing  
SplitView now correctly handles mouse events when using  
containmentMask.  
  
* 54eef38350 QQuickAbstractDialog: emit rejected() on mere close()  
QtQuick dialogs now emit rejected() on a mere close(), too.  
  
* 84c5ae1947 Fix fractional scaling of text in Qt Quick  
Fixed a kerning issue with native-rendered text when there is a  
fractional system scale factor set.  
  
### qttools  
* 18a38fe65 lupdate: Allow multiple specifiers after method signature  
lupdate does not trip anymore over tr() calls in methods with multiple  
specifiers. For example "QString MyClass::foo() const noexcept" now gets  
the correct context.  
  
### qtserialbus  
* dc5a3df Make pduFromStream work on big endian (again)  
Fix reading from stream on big endian systems  
  
### qtremoteobjects  
* 6361735 Fix race condition when accessing invalid index  
Fix race condition when accessing invalid index  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-103740 QTemporaryFile::rename does not document that it can only  
rename, not copy+delete like QFile::rename  
* QTBUG-93298 Windows: Application hangs (or crashes) on quit while  
QtQuick FileDialog is open  
* QTBUG-104053 tst_QFile fails on webOS  
* QTBUG-103733 [Windows] setProcessDpiAwarenessContext(DPI_AWARENESS_CON  
TEXT_PER_MONITOR_AWARE_V2) failed on certain machines  
* QTBUG-103745 QPainter::drawText method truncates inputs  
* QTBUG-98988 Qt bugs when portal implementation is not available  
* QTBUG-103922 Calling QThread::terminate() in destructor causes double  
object destruction  
* QTBUG-104003 QTabBar/QTabWidget crashes when closing last tab and  
there are hidden tabs  
* QTBUG-104056 Conan: qmlimportscanner: No such file or directory  
* QTBUG-88519 androiddeployqt doesn't know about Conan's build path  
* QTBUG-89588 androiddeployqt fails with error from qmlimportscanner if  
qtdeclarative is not installed  
* QTBUG-104123 "configure -no-pkg-config" doesn't turn off pkg-config  
* QTBUG-103568 Android 13: Warnings when starting qt apps  
* QTBUG-103455 Settings don't work with content:// URL on Android  
* QTBUG-103836 Fusion menu text with mnemonic clipped on Windows  
* QTBUG-94481 [REG 5.15.2 -> 6.1.1] Ellipsis in the worst possible place  
* QTBUG-49704 QLoggingCategory::installFilter crashes with the code from  
documentation  
* QTBUG-98417 Bundling translation file of plist does not work with  
XCode 13  
* QTBUG-100093 Deployed third party library points to the original  
location  
* QTBUG-103894 Configuring fails on Manjaro Linux  
* QTBUG-101161 Android Assets awfully slow to be loaded  
* QTBUG-102021 QCocoaScreen::UpdateScreens crash  
* QTBUG-84741 Crash on QCocoaScreen::isOnline() when calling  
CGDisplayIsOnline  
* QTBUG-104231 tst_QVulkan fails with Ubuntu 22.04 due to broken Mesa  
lavapipe included in the distro  
* QTBUG-104320 qt_add_big_resources does not list contents of the qrc  
file in Qt Creator  
* QTBUG-101585 QMessageBox components get skipped by Windows Narrator  
* QTBUG-100188 Page layout settings are reset when QPrintDialog is shown  
if there is no printer installed on macOS  
* QTBUG-103007 Resetting a QComboBox custom model doesn't emit  
currentIndexChanged or currentTextChanged  
* QTBUG-102395 QMainWindow::restoreState corrupts relation between  
toolbars layout item  
* QTBUG-104421 tst_qthread terminateAndPrematureDestruction() ERROR:  
AddressSanitizer: stack-buffer-underflow  
* QTBUG-78826 Cannot enter non ascii characters to the TextField and  
QLineEdit from browser(wasm)  
* QTBUG-104412 FAIL!  : tst_AndroidAssets during dependency update  
* QTBUG-91896 QTableView span gets confused with logical indexes when  
columns are moved  
* QTBUG-85474 QGraphicsScene::clearSelection() may leave internal state  
inconsistent  
* QTBUG-103497 [iOS] CMake handling qt_add_big_resources() fails  
* QTBUG-104443 xcb plugin crashes when running in vnc  
* QTBUG-100361 No font rendering at all when configured with -no-  
harfbuzz  
* QTBUG-103838 QFontMetrics::horizontalAdvance() does not seems to give  
correct value  
* QTBUG-104362 QDomImplementation::DropInvalidChars strips emoji and  
other non-BMP characters  
* PYSIDE-1750 QMouseEvent.pos marked as deprecated in source but not in  
docs  
* QTBUG-103992 QFuture::onCanceled is not called when promise is deleted  
* QTBUG-102343 Windows: Only initial QScreen values are available if  
screen geometry changes between QApplication and before first window is  
open  
* QTBUG-103383 Windows: Qt doesn't respond to DPI changes if Qt window  
is having a non-Qt parent  
* QTBUG-79248 TrayIcons Menu does not scales its size when changing DPI  
* QTBUG-86790 Mingw Qt provides debug libraries in the wrong folder  
* QTBUG-104085 QJsonValue::toObject(const QJsonObject &defaultValue) and  
QJsonValue::toArray(const QJsonArray &defaultValue) parse empty default  
values incorrectly  
* QTBUG-102869 wasm: Resizing is still accessable under a modal dialog  
* QTBUG-53661 QDom internalSubset is never set  
* QTBUG-104396 qmake projects try to link to static qt libraries with  
hardcoded CI paths (no such file or directory)  
* QTBUG-102595 Builds can't find the projects qml modules  
* QTBUG-104583 Buffer overrun and crash in  
QColorTransferTable::applyInverse()  
* QTBUG-104132 [REG 6.2.4->6.3.0] HTTP-Redirect is broken  
(ManualRedirectPolicy)  
* QTBUG-103415 [Reg 6.1.3->6.2.0] Parallel Animation bug on macOS  
* QTBUG-104484 Missing documentation for QDropEvent methods: position,  
buttons, modifiers  
* QTBUG-92485 Q_ASSERT added in qrasterizer.cpp  
* QTBUG-95933 Using scanner input IRcode will result in an error when  
second character is uppercase  
* QTBUG-101615 QMLPATHS not documented  
* QTBUG-104205 QDockwidget screen change issue(s) more involved parts.  
* QTBUG-104383 QExpandingLineEdit::resizeToContents crashes  
conditionally in qBound (since Qt 6.3.0)  
* QTBUG-104565 QTableWidgets: crash when double click into table cell  
end that expands beyond   window  
* QTBUG-71900 Double tapping on a word does not show the selection  
handles in the right place after the initial selection  
* QTBUG-58503 Text Handle Cursor Position Offset Error  
* QTBUG-104527 iOS: Input panel opens when you click on a QPushButton  
* QTBUG-98651 [iOS 15] Application freezes when QDialog is executed by  
button clicked() signal  
* QTBUG-104708 qmake projects try to link to static qt libraries with  
hardcoded CI paths part 2  
* QTBUG-104596 [reg->6.4] Qt Designer crashes when OpenGL widget is  
dragged to form  
* QTBUG-104726 Build failure on x86  
* QTBUG-104232 tst_QSslKey::constructor fails with Ubuntu 22.04 and  
openssl 3  
* QTBUG-102825 Popping QML StackView Item makes a11y unusable  
* QTBUG-103794 B2qt fails with Ubuntu 22.04: undefined reference to  
`qt_resourceFeatureZstd'  
* QTBUG-104809 Crash in QKmsDevice::createScreenForConnector  
* QTBUG-103571 QWindowsContext::findPlatformWindowAt stuck in infinite  
loop  
* QTBUG-85109 QPainter::drawImage draws images in different places  
depending on image format  
* QTBUG-103988 State of QTreeWidgetItem not announce by screenreader  
* QTBUG-104696 QFontDialog:: selectedFont and fontSelected always  
returns one font  
* QTBUG-104740 Accessibility: NVDA not narrating full state of QTabBar  
* QTBUG-98762 REGRESSION: QPalette::setBrush does not reliably detach  
* QTBUG-103940 Insufficient documentation in QRegularExpression variant  
of QString::indexOf(), results in random crash bug  
* QTBUG-104827 Huge APK sizes under Windows  
* QTBUG-99990 windows: Painting an image with DPR >1.0  to a QPrinter  
does not produce correct result  
* QTBUG-104877 wacom: QTabletEvent rotation goes to -180 when absent  
* QTBUG-46113 tst_qcompleter fails on Ubuntu  
* QTBUG-103892 Stop binding to iBridge interface when unit testing  
QTcpServer on macOS  
* QTBUG-24240 testlib: executing a test with an invalid data label  
doesn't count as a failure and doesn't return a non-zero exit code  
* QTBUG-98921 tst_QGraphicsWidget::initialShow is uber flaky on OpenSUSE  
* QTBUG-49205 tst_qnetworkreply::ioGetFromBuiltinHttp  
* QTBUG-104718 fuzz: QCborValue::fromCbor out of memory error 32bit  
* QTBUG-102239 tst_QWidget::enterLeaveOnWindowShowHide is flaky  
* QTBUG-103576 [REG] Broken Qt::TextAlignmentRole  
* QTBUG-104959 QT_NO_TRANSLATION define breaks QML build  
* QTBUG-104851 qdoc: Ignore Q_WEAK_OVERLOAD  
* QTBUG-101058 Pixelated images on Windows  
* QTBUG-104213 Add \brief descriptions to Concurrent topics  
* QTBUG-104083 tst_bench_shared_ptr does not compile on Ubuntu 22.04  
* QTBUG-82477 QClipboard doesn't support custom mimeTypes  
* QTBUG-104875 Wacom proximity events went missing on X11 in 6.3  
* QTBUG-104268  
tst_QTouchEvent::multiPointRawEventTranslationOnTouchPad() ASSERT  
failure in QList::at: "index out of range"  
* QTBUG-105140 [REG] default constuctor requirement for meta type  
(QVariant) breaks webengine api  
* QTBUG-104270 cmake loads native sysroot cmake config and tries to look  
for libs  
* QTBUG-102879 Examples not linking to Qt::Core are installed in the  
wrong folder  
* QTBUG-104917 QStyleSheetStyle::drawPrimitive(QStyle::PE_PanelLineEdit)  
crashes with widget==nullptr  
* QTBUG-105242 [REGRESSION] After  
2f5f276b4a2a19b9f2669b84f28ce8e970aaa39f network printers are missing  
* QTBUG-69354 QGtk3FileDialogHelper isn't modal  
* QTBUG-104801 Crash with QPainter::drawText used on a QQuickView with a  
Text item  
* QTBUG-105310 Using deprecated keyword breaks the build  
* QTBUG-104316 Qt 6.3.1 build for arm failed: selected processor does  
not support `yield' in ARM mode  
* QTBUG-105041 openssl 3.x 32bit platform regression  
* QTBUG-104940 post in/decrements of QBEInteger and QLEInteger return  
reference according to documentation  
* QTBUG-105160 Bad access when destroying QComboBox immediately after  
selecting item  
* QTBUG-105302 qputenv sometimes puts garbage at the end of the value  
* QTBUG-105204 QProperty: Notfication missing if binding no longer has  
any dependencies  
* QTBUG-104982 [Regression] binding stops being evaluated  
* QTBUG-105010 Font underline rendering bug  
* QTCREATORBUG-27634 Basic Layouts Example UI elemnets get squished  
* QTBUG-105323 [Regression] Keyboard is not properly hidden on ios  
* QTBUG-105339 Typo in since version for QStyledItemDelegate  
* QTBUG-105374 Modules in 5.15 branch missing MinGW debug files  
* QTBUG-105341 QDoubleValidator can report "Intermediate" for inputs  
that are unambiguously out-of-range  
* QTBUG-95319 The cursor size is unstable when multiple QT_SCALE_FACTOR  
is used  
* QTBUG-105501 Qt6 build fails with system double-conversion  
* QTBUG-105517 Redundant "does" in QFrame  
* QTBUG-105286 Crash with UpdateWindowTitle event triggered by closing a  
dialog (mac)  
* QTBUG-105951 Crash when closing dialog directly after closing popup  
* QTBUG-103470 [iOS] CMake translation handling fails  
* QTBUG-103923 GCC 12: failure to build from source [<QtBase>]  
* QTBUG-102041 Android multi-abi builds don't work if the Android  
ndk/sdk install path is different from the CI's one  
* QTBUG-104128 top-level configure is still verbose in a non-developer  
build  
* QTBUG-103723 [iOS] CMake shader handling fails  
* QTBUG-87137 tst_QApplication::sendEventsOnProcessEvents() failed on  
Ubuntu 20.04/22.04 and RHEL 9  
* QTBUG-68860 tst_QGlyphRun::mixedScripts autotest fails on Ubuntu 18.04  
and QEMU builds  
* QTBUG-68865 tst_QMenuBar::check_menuPosition autotest fails on Ubuntu  
18.04  
* QTBUG-84248 tst_QFont::defaultFamily fails  
* QTBUG-103591 Windows: Comboboxes (Qml and QtWidgets) don't have the  
UIAutomation (UIA) ExpandCollapse pattern  
* QTBUG-103091 FAIL!  : tst_QDockWidget::floatingTabs in QNX_710  
* QTBUG-93471 Darwin linker warns about global weak symbols when linking  
an executable against a static Qt  
* QTBUG-103730 Qt Test tutorial is missing a clear entrypoint  
* QTBUG-104580 androiddeployqt fails with "unknown argument '--libs'"  
when call llvm-readobj v14  
* QTBUG-101008 Using Text.NativeRendering results in characters drawn  
too close to each other with fractional scale factors  
* QTBUG-102594 [REG 5.15.6 -> 5.15.9] Many ANR issues by QtAccessibility  
* QTBUG-104450 qmake: it's impossible to configure some compiler and  
linker options in the generated vcxproj  
* QTBUG-103753 incorrect document about QDomDocument::setContent()  
* QTBUG-103593 androiddeployqt doesn't work well with user's QML module  
in their subdirectories  
* QTBUG-104012 QDateTime constructor performance regression when year is  
below epoch  
* QTBUG-104857 QtBase does not compile with QT_DISABLE_DEPRECATED_BEFORE  
= 0x060000  
* QTBUG-104878 xcb wacom support gets confused about device instances  
* QTBUG-103706 Synthesized touch event not recognized with Widgets  
* QTBUG-101932 two HoverHandlers with different  
acceptedDevices/acceptedPointerTypes: cursorShape doesn't change  
accordingly  
* QTBUG-104787 Thread Sanitizer reports data races in QtConcurrent  
* QTBUG-105038 QCollator is limited to ≤ 2Gi characters  
* QTBUG-89702 Improve the QRegExp->QRegularExpression docs  
* QTBUG-105051 pkg-config does not expose libexecdir for finding some  
tools  
* QTBUG-104840 heap-use-after-free in QTest::ignoreMessage  
* QTBUG-85248 Qt warning  
"QHttpNetworkConnectionPrivate::_q_hostLookupFinished could not de-queue  
request, failed to report HostNotFoundError"  
* QTBUG-105388 qhash.h:553:17: warning: argument 1 value  
'18446744073709551615' exceeds maximum object size 9223372036854775807  
* QTBUG-104441 REG: No longer possible to use macros or functions that  
rely on an event loop in cleanup() after failed test function  
* QTBUG-105048 QSqlQuery is supposed to be move-only, however we copy it  
in our code  
* QTBUG-104730 androidtestrunner splits data row names by whitespace and  
treats them as test functions  
  
### qtsvg  
* QTBUG-101698 [REG 6.2.2 -> 6.2.3] Integer overflow when loading svg  
image  
  
### qtdeclarative  
* QTBUG-103560 qmlsc allows access to fractional indices of  
QQmlListProperty  
* QTBUG-102944 [Reg 5.15 -> 6.2] Relative QML import does not work from  
Android assets  
* QTBUG-103915 tst_snippets fails on webOS  
* QTBUG-101975 No longer possible to pre-select a file when fileMode is  
SaveFile  
* QTBUG-103187 Reconfiguration is slow due to qmlimportscanner  
* QTBUG-102625 [REG 5.15 -> 6.0] Double click event does not fire when  
using DragHandler as a child of Window in Qt6  
* QTWEBSITE-1051 Incorrect code snippet in QML inheritance and coercion  
example  
* QTBUG-103250 Link to ScrollBar's size property is wrong  
* QTBUG-104051 FAIL!  : tst_qqmlnotifier::deleteFromHandler() Compared  
values are not the same  
* QTBUG-103924 GCC 12: failure to build from source [<QtDeclarative>]  
* QTBUG-104026 TypeError warnings from attached property usage in  
tst_qquicklistview  
* QTBUG-104361 [REG: 6.1->6.2] QMetaObject::invokeMethod of qml function  
has no effect  
* QTBUG-100820 [REG 5.15.2-6.2.3] Wrong rendering of semi-transparent  
text if Text.NativeRendering is used  
* QTBUG-100554 Qt Quick Calendar: 1st row sometimes contains only days  
from the previous month  
* QTBUG-75109 tst_QQuickListView::currentIndex() is failing  
* QTBUG-104089 TextEdit has wrong cursor shape on hover  
* QTBUG-98914 QML Test with grabImage() fails on iOS  
* QTBUG-103832 The delegate item of ListView is not pressed if the  
boundsBehavior is to set Flickable.StopAtBounds  
* QTBUG-104373 [REG: 6.2->6.3] qt_add_qml_module does not register  
QML_ELEMENT classes if version starts with 0  
* QTBUG-102965 File order of CMake project can break compilation due to  
QMetaTypeId<T> specialization  
* QTBUG-104138 Doc: Wrong link to 'Squish'  
* QTBUG-104462 qmlsc miscompiles JavaScript functions with arguments  
* QTBUG-100644 Document how to properly add javascript files with  
qt_add_qml_module  
* QTBUG-38765 When propagateComposedEvents is set, drag does not always  
move the flickable  
* QTBUG-74842 Flickable behind MouseArea does not steal first drag event  
after creation  
* QTBUG-104470 Text overlap in custom menu  
* QTBUG-104523 error: no member named 'offsetsAndSize' in  
'qt_meta_stringdata_TestClass_t  
* QTBUG-104544 When the repeater is used as the contentItem of the menu,  
all items are invisible  
* QTBUG-101268 ListView does not preserve its relative scrollbar  
position when window is restored down on Windows if height of  
ListView.header changes dynamically  
* QTBUG-101266 Changing ListView.header height dynamically doesn't  
preserve relative scrollbar position when window is Maximized  
* QTBUG-102762 QML_ELEMENT is broken in Qt 6.3.0 on Android  
* QTBUG-104447 qmlsc miscompiles bindings that throw exceptions  
* QTBUG-104258 tst_QQuickPopup::Material fails with Ubuntu 22.04  
* QTBUG-104603 Clarify the QML_EXTENDED documentation  
* QTBUG-104442 QML Image does not rescale on setGeometry() when "layer"  
is enabled  
* QTBUG-104536 [Possible regression]: Rendering errors when using  
layer.enabled: true  
* QTBUG-104257 tst_QQuickMenu(bar) tests are failing with Ubuntu 22.04  
* QTBUG-102559 macOS style focus frame incorrectly positioned  
* QTBUG-104642 iOS: TextField has blinking cursor, but no input panel is  
showing  
* QTBUG-104379 [REG 6.3.0 -> 6.3.1] Crash when trying to debug QML  
Application  
* QTBUG-104471 tst_QQuickListView2::tapDelegateDuringFlicking fails on  
Android  
* QTBUG-87119 MouseArea inside SplitView item takes mouse events away  
from Splitview handle  
* QTBUG-97385 QtQuick SplitView with Flickable gets stuck  
* QTBUG-104242 tst_QQuickDrawer tests are failing with Ubuntu 22.04  
* QTBUG-104625 tst_Qmlls::testWorkspace fails  
* QTBUG-101973 File Dialog does not re open in some situation.  
* QTBUG-104491 mouse event broken after continuous transition animation  
in StackView.  
* QTBUG-104084 tst_qmldomitem ERROR: AddressSanitizer: alloc-dealloc-  
mismatch  
* QTBUG-104803 Crash when calling QJSValue::hasProperty("x") from Qml on  
a QVector3D received from a Q_PROPERTY  
* QTBUG-104657 Custom ComboBox does not function properly with model  
passed from c++  
* QTBUG-104325 QQuickPointerHandler::currentEvent() exposes stale event  
* QTBUG-101008 Using Text.NativeRendering results in characters drawn  
too close to each other with fractional scale factors  
* QTBUG-98769 QML StackView heap-use-after-free on pop()  
* QTBUG-104865 QQuickPaddedRectangle emits topPaddingChanged incorrectly  
* QTBUG-98936 Can't use Apple Pencil with Qml controls  
* QTBUG-102764 [REG: 5->6] Pen / Pencil input devices not working  
* QTBUG-103937 QML WebEngineView - Wacom pen not works  
* QTBUG-103081 QQmlComponent::create() crashes when creeating a  
QML_EXTENDED_NAMESPACE(Type) object when Type is a Q_OBJECT extending a  
property  
* QTBUG-104700 QQuickDialog::accept() slot not executed when called from  
QML when making QPlatformDialogHelper::StandardButtons available via  
QML_EXTENDED_NAMESPACE  
* QTBUG-104573 DialogButtonBox enums are not known to qmllint  
* QTBUG-104537 [REG 6.2.4-6.3.1] HoverHandler do not propagate hover to  
TextEdit  
* QTBUG-90466 Missing line number in tst_qquickloader error message on  
macOs  
* QTBUG-105164 ScrollView consumes wheel events even when 'wheelEnabled'  
is set false  
* QTBUG-91687 QML fails to run benchmarks in qmlbench's v8bench  
directory  
* QTBUG-58559 Deletion of a dynamic properties to JSObject ends up using  
all memory  
* QTBUG-104658 macOS style lacks DialogButtonBox implementation  
* QTBUG-94983 Crash when binding to aliased grouped property  
* QTBUG-92192 Issues calling JSON.stringify() on objects  
* QTBUG-105361 qmlformat: Unnecessary replacement of 'let' with 'var',  
leading to inline write errors  
* QTBUG-105208 REG: Selecting text inside a TextEdit causes existing  
lines to disappear and empty lines to appear.  
* QTBUG-105555 REG: Text selection in the text editor example causes the  
text document to reposition the blocks after the selection  
* QTBUG-105728 REG: TextArea & TextEdit breaks when selecting text with  
mouse  
* QTBUG-103819 QML TextEdit memory usage is extreme and the memory is  
not freed  
* QTBUG-102403 QObject::objectName() leads to heap-use-after-free in  
tst_qquickanimations::cleanupWhenRenderThreadStops()  
* QTBUG-102862 Build failure with lttng enabled  
* QTBUG-104157 Delegate Controls documentation: Introduction and details  
out of sync  
* QTBUG-99578 Global Functions are Undocumented  
* QTBUG-86729 many Qt Quick test failures after input event refactoring  
* QTBUG-101736 QQuickWidget: button in a popup doesn't receive touch end  
event  
* QTBUG-89927 tst_qquickfontloader::changeFontSourceViaState fails with  
macOS 10.15 and Xcode 12.3  
* QTBUG-104512 Invalid code generated  
* QTBUG-104508 qmlcachegen fails to compile PhotoCaptureControls.qml in  
multimedia  
* QTBUG-101488 tst_QQuickFileDialogImpl is flaky  
* QTBUG-102984 tst_QQmlDebugJS hangs on macOS in CI  
* QTBUG-101678 tst_qqmlinspector (and other tests in  
tests/auto/qml/debugger/) times out on macOS 12 (x86_64) in CI  
* QTBUG-101932 two HoverHandlers with different  
acceptedDevices/acceptedPointerTypes: cursorShape doesn't change  
accordingly  
* QTBUG-104928 qmlimportscanner: segfault on unexpected argument  
* QTBUG-94919 Control changes hover state even though it is disabled  
* QTBUG-105190 tst_QQuickListView2::flickDuringFlicking is flaky  
* QTBUG-105149 QML ComboBox displays an unwanted shadow effect on  
Android  
  
### qtactiveqt  
* QTBUG-99294 In ActiveQtServer derived from QMainWindow, when  
PushButton exists Lables in StatusBar can not be shown  
* QTBUG-100332 dumpcpp silently generates uncompilable files for some  
.NET libraries  
* QTBUG-100145 ActiveQt example "outlook" build fails with a wall of  
errors: MSOUTL.cpp(346616): error C2062: type 'unknown-type' unexpected  
  
### qtmultimedia  
* QTBUG-99095 Android tst_QAudioSource test failed  
* QTBUG-104520 GDI leak in MediaPlayer  
* QTBUG-104483 ASSERT: "viewport.size() == size" in  
qquickvideooutput.cpp  
* QTBUG-104133 QML animation overlaid on video becomes unusably slow &  
with increasing memory consumption over time  
* QTBUG-102772 Declarative-camera preview freezes when takes photo  
* QTBUG-100079 Android: fix QAndroidAudioDecoder issues  
* QTBUG-97492 QAudioSink returns always UnderrunError on Android  
* QTBUG-98121 Android: Filters out unsupported audio codecs(flac) on  
AudioRecorder app  
* QTBUG-99022 Android: Changing a Audio sink on Audiooutput example  
issue  
  
### qttools  
* QTBUG-99421 Some Qt5 ui file does not compile with Qt6  
* QTBUG-104490 qhelpgenerator can't find QSqlDatabase drivers in static  
builds  
* QTBUG-99415 lupdate ignores tr() call in a function with noexcept  
operator  
* QTBUG-104713 GCC 12: failure to build from source [<QtTools>]  
* QTBUG-105130 qttools: CMake failure if litehtml is found on the system  
* QTBUG-104377 Qt Designer: Alignment property moves to wrong place in  
property editor  
* QTBUG-103470 [iOS] CMake translation handling fails  
* QTBUG-91521 When calling lupdate on a file that uses QT_TR_NOOP in a  
constructor for a static QString it will fail to find the context  
* QTBUG-104426 lupdate uses return type as context for free functions  
* QTBUG-86507 ASSERT: "it.isUnused()" in file  
/home/qt/work/install/include/QtCore/qhash.h, line 525  
  
### qtdoc  
* QTBUG-101323 Apps running on Android 12 and above must comply with the  
latest Unicode version  
  
### qtpositioning  
* QTBUG-103478 QGeoPositionInfoSource on Android always asks for  
location permission  
* QTBUG-104448 Fix QtPositioning tests for static builds  
* QTBUG-104465 It is impossible to build tests with custom plugins in  
static build configurations  
  
### qtconnectivity  
* QTBUG-103209 As a user who compiles Qt himself, I'm left in the dark  
regarding the configuration of QtConnectivity  
* QTBUG-104106 Android Bluetooth LE claims to advertise even if  
bluetooth off  
* QTBUG-104105 Bluez LE advertiser dispose crash when bluetooth off  
* QTBUG-104060 Bluez LE controller crash on too large advertisement data  
* QTBUG-104479 (Classic) bluetooth service scan sometimes hangs  
indefinitely on Android  
* QTBUG-97797 QBluetoothDeviceDiscoveryAgent take CPU/Ram usage to 100%  
* QTBUG-106029 Crash during device discovery in Qt RO bleclient example  
* QTBUG-105742 Memory leak in BLE discovery  
* QTBUG-102442 Bluetooth hostmode change Discoverable=>Connectable  
doesn't work on Android  
* QTBUG-101066 QBluetoothServiceDiscoveryAgent::finished sometimes  
(spuriously) is not emmited on Android 10  
* QTBUG-104914 tst_qbluetoothlocaldevice and tst_qbluetoothserver tests  
fail on Android 12 emulator in CI  
  
### qtwayland  
* QTBUG-97593 Qt with QtWayland doesn't build without QtQml  
* QTBUG-104227 QWaylandTextInput: Not possible to inject keys with  
Shift- or Ctrl-Modifiers  
* QTBUG-105308 ASSERT failure in QWindow: "Updates can only be scheduled  
from the GUI (main) thread"  
* QTBUG-104435 Build failure in qtwayland with libcxx  
  
### qt3d  
* QTBUG-102328 Qt3D.Core can't be imported from a static Qt build  
* QTBUG-101876 Qt3D Viewport documentation states wrong type for Gamma  
property  
* QTBUG-104534 QImage received from QRenderCapture using Qt3D RHI  
renderer causes crash.  
* QTBUG-104592 RHI Render Capture crashed with debug build  
* QTBUG-95650 Qt3D Light Module is not working.  
* QTBUG-100402 Light uniform is hardcoded to use PointLight only  
  
### qtimageformats  
* QTBUG-104398 Segmentation fault in Jpeg2000JasperReader when Jasper 3  
is used  
* QTBUG-104692 qtimageformats breaks top-level build  
  
### qtserialbus  
* QTBUG-103879 [Reg 5.15.2 -> 5.15.9] QModbusClient:: sendRawRequest()  
produces ModbusDevice::UnknownError when there is no error  
  
### qtserialport  
* QTBUG-101444 QSerialPort: trouble with high baud rates /  
waitForReadyRead() stalls  
* QTBUG-103822 QSerialPort::waitForReadyRead always returns false on  
older Windows systems  
* QTBUG-91237 QSerialPort: moving / resizing / clicking window title bar  
blocks serial port read/write  
* QTBUG-87151 QSerialPort: synchronous read fails as waitForReadyRead()  
always times out.  
  
### qtwebengine  
* QTBUG-103579 Qt PDF: Static build fails on macOS  
* QTBUG-103735 QWebEnginePage::iconChanged() not emitted  
* QTBUG-103578 WebEngine: Error when linking gn  
* QTBUG-102394 Pdf rendering very slow using Qt Pdf module  
* QTBUG-102951 Qt PDF cannot coexist with TIFF Qt Image Formats plugin  
in statically-linked app  
* QTBUG-101769 Qt WebEngine reports wrong UIAutomation bounding rects  
with high DPI  
* QTBUG-103760 Conan: Qt WebEngine resources not found  
* QTBUG-104436 V8 error when using WebEngine with --single-process and  
proxy auto-config  
* QTBUG-105082 QtWebEngine freezes on specific Chromium debug command  
* QTBUG-86871 Qt WebEngine incompatible with Selenium's "sendKeys"  
method  
* QTBUG-104057 Dependency update fails: error: no matching member  
function for call to 'addAction'  
* QTBUG-99445 quicknanobrowser crashes with --single-process  
* QTBUG-102099 QWebEngineView ColorPicker  is not modal and freezes  
application  
* QTBUG-102633 [Windows] Linking errors in Blink  
* QTBUG-104238 [REG 5.15 -> 6.3] Widevine fails on specific sites  
* QTBUG-101744 tst_uidelegates most tests fail on macOS  
* QTBUG-103354 Test #12: tst_uidelegates  
...........................***Failed  
  
### qtcharts  
* QTBUG-99190 Performance issue with VXYModelMapper  
* QTBUG-102392 X-axis vanishes when difference between min and max is  
less than two  
  
### qtdatavis3d  
* QTBUG-104714 Dependency cycle between QtDatavisualization and  
QtDatavisualizationQml  
  
### qtscxml  
* QTBUG-98368 Dependency cycle in qtscxml  
  
### qtremoteobjects  
* QTBUG-104098 Update dependencies on '6.4' fails in qt/qtremoteobjects  
* QTBUG-74124 QAbstractItemModelReplica internal error crash  
* QTBUG-97790 Generated SourceAPI class can't be used without compiler  
warnings  
* QTBUG-97092 spelling errors reported by lintian  
  
### qtquick3d  
* QTBUG-102193 Negative joint index leads to crashes  
* QTBUG-104118 [REG 6.3 -> 6.3.1] Global scaling does no longer work in  
3D asset imports  
  
### qtshadertools  
* QTBUG-103723 [iOS] CMake shader handling fails  
  
### qt5compat  
* QTBUG-103927 GCC 12: failure to build from source [<Qt5Compat>]  
* QTBUG-89702 Improve the QRegExp->QRegularExpression docs  
  
### qtopcua  
* QTBUG-104646 [C++20 FTBFS] open62541.h is running afoul of volatile  
compound statement deprecation in C++20  
  
### qtlanguageserver  
* QTBUG-103924 GCC 12: failure to build from source [<QtDeclarative>]  
  
Known Issues  
------------  
  
* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-6/supported-platforms.html
* RTA reported issues from Qt 6.3  
https://bugreports.qt.io/issues/?filter=23976  
* See Qt 6.3 Known Issues from:  
https://wiki.qt.io/Qt_6.3_Known_Issues  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Mike Achtelik  
Cristian Adam  
Chris Adams  
Laszlo Agocs  
Dimitrios Apostolou  
YAMAMOTO Atsushi  
Mahmoud Badri  
Mate Barany  
Vladimir Belyavsky  
Chen Bin  
Eskil Abrahamsen Blomfeldt  
Mikolaj Boc  
Joerg Bornemann  
Assam Boudjelthia  
Michael Brüning  
Marco Bubke  
Igor Bugaev  
Andreas Buhr  
Alexandru Croitor  
Mitch Curtis  
Thibaut Cuvelier  
Giuseppe D'Angelo  
Knud Dollereder  
Alexey Edelev  
Oliver Eftevaag  
Iikka Eklund  
Hatem ElKharashy  
Andreas Eliasson  
Ilya Fedin  
Pekka Gehör  
Roman Genkhel  
Maximilian Goldstein  
Andrei Golubev  
Jan Grulich  
Richard Moe Gustavsen  
Tang Haixiang  
Heikki Halmet  
Elias Hautala  
Jani Heikkinen  
Miikka Heikkinen  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Dominik Holland  
Mats Honkamaa  
Sam James  
Nils Jeisecke  
Allan Sandfeld Jensen  
Janne Juntunen  
Friedemann Kleint  
André Klitzing  
Michal Klocek  
Jarek Kobus  
Tomi Korpipaa  
Fabian Kosmale  
Volker Krause  
Mike Krus  
Sona Kurazyan  
Jonas Kvinge  
Kai Köhne  
Inho Lee  
Paul Lemire  
Moody Liu  
Jonathan Liu  
Robert Loehning  
Thiago Macieira  
Thorbjørn Lund Martsum  
Ievgenii Meshcheriakov  
Samuel Mira  
Fawzi Mohamed  
Bartlomiej Moskal  
Marc Mutz  
Antti Määttä  
Martin Negyokru  
Guineng Ni  
Andy Nichols  
Mårten Nordheim  
Laszlo Papp  
Bumjoon Park  
Thomas Piekarski  
Samuli Piippo  
Timur Pocheptsov  
Joni Poikelin  
Lorn Potter  
Liang Qi  
Umair Raihan  
Topi Reinio  
André de la Rocha  
Rafael Roquetto  
Shawn Rutledge  
Michael Saxl  
Eli Schwartz  
Dmitry Shachnev  
Sami Shalayel  
Ye ShanShan  
Andy Shaw  
Ivan Solovev  
Axel Spoerl  
Piotr Srebrny  
Elias Steurer  
Christian Strømme  
Tasuku Suzuki  
Jan Arve Sæther  
Morten Sørvig  
Duan Ting  
Ivan Tkachenko  
Jere Tuliniemi  
Sami Varanka  
Peter Varga  
Louis du Verdier  
Doris Verria  
Tor Arne Vestbø  
Petri Virkkunen  
Ville Voutilainen  
Juha Vuolle  
Jaishree Vyas  
Edward Welbourne  
Paul Wicking  
Anna Wojciechowska  
Oliver Wolff  
Jiang Wu  
Weng Xuetian  
Lu YaNing  
JiDe Zhang  
Yuhang Zhao  
