Release note  
============  
Qt 6.2.6 release is a patch release made on the top of Qt 6.2.5. As a patch  
release, Qt 6.2.6 does not add any new functionality but provides bug fixes  
and other improvements.  
  
For detailed information about Qt, see the Qt 6.2 online documentation:  
https://doc.qt.io/qt-6.2/.  
  
Important Changes  
-----------------  
  
### qtbase  
* bd27707c20 Always update QPalette resolve mask, regardless of QBrush  
change  
Always update resolve mask in QPalette::setBrush, even if the value of  
brush has not changed.  
  
* 1bdf2799eb Support test-case selection based on global data tag  
When specifying what tests to run on a QtTest command-line, it is now  
possible to include a global data tag in the same way as a function-  
specific data tag or in combination with it. Thus if the test reports  
itself as tst_Class::function(global:local), command-line option  
function:global:local will select that specific test and function:global  
will run all data-rows for the function on the given global data tag.  
  
* bdb4b80e9d SQLite: Update SQLite to v3.39.2  
Updated SQLite to v3.39.2  
  
* eb915be5ee QDebug: finish porting to qsizetype/size_t  
Fixed issues on 64-bit platforms when streaming containers (incl.  
strings) of more than 2Gi elements.  
  
* 1cd5b6baee Update bundled libjpeg-turbo to version 2.1.4  
libjpeg-turbo was updated to version 2.1.4  
  
* 118558c5b2 QHttp2Configuration: in QNAM, use old, higher values in  
flow control  
Stream receive window that HTTP/2 protocol in QNAM is using increased  
to 214748364 octets (from the previous 64K) not to throttle download  
speed. Clients, working with servers, not accepting such parameters,  
must set HTTP/2 configuration on their requests accordingly.  
  
* 978087f351 Fix crash when setting override cursor on multiple clients  
Fixed a crash when setting an override cursor on multiple clients.  
  
### qtdeclarative  
* 7b61ac904a QQuickAbstractDialog: emit rejected() on mere close()  
QtQuick dialogs now emit rejected() on a mere close(), too.  
  
* c6780664c6 Fix fractional scaling of text in Qt Quick  
Fixed a kerning issue with native-rendered text when there is a  
fractional system scale factor set.  
  
* 2ef0a7a920 Fix SplitView containmentMask hit testing  
SplitView now correctly handles mouse events when using  
containmentMask.  
  
### qtimageformats  
* a564617 Update bundled libwebp to version 1.2.4  
Update bundled libwebp to version 1.2.4  
  
### qtremoteobjects  
* 5ada39f Fix race condition when accessing invalid index  
Fix race condition when accessing invalid index  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-95933 Using scanner input IRcode will result in an error when  
second character is uppercase  
* QTBUG-104484 Missing documentation for QDropEvent methods: position,  
buttons, modifiers  
* QTBUG-92485 Q_ASSERT added in qrasterizer.cpp  
* QTBUG-71900 Double tapping on a word does not show the selection  
handles in the right place after the initial selection  
* QTBUG-58503 Text Handle Cursor Position Offset Error  
* QTBUG-104383 QExpandingLineEdit::resizeToContents crashes  
conditionally in qBound (since Qt 6.3.0)  
* QTBUG-104565 QTableWidgets: crash when double click into table cell  
end that expands beyond   window  
* QTBUG-101615 QMLPATHS not documented  
* QTBUG-95319 The cursor size is unstable when multiple QT_SCALE_FACTOR  
is used  
* QTBUG-103415 [Reg 6.1.3->6.2.0] Parallel Animation bug on macOS  
* QTBUG-98651 [iOS 15] Application freezes when QDialog is executed by  
button clicked() signal  
* QTBUG-104596 [reg->6.4] Qt Designer crashes when OpenGL widget is  
dragged to form  
* QTBUG-104726 Build failure on x86  
* QTBUG-104708 qmake projects try to link to static qt libraries with  
hardcoded CI paths part 2  
* QTBUG-104396 qmake projects try to link to static qt libraries with  
hardcoded CI paths (no such file or directory)  
* QTBUG-104232 tst_QSslKey::constructor fails with Ubuntu 22.04 and  
openssl 3  
* QTBUG-103794 B2qt fails with Ubuntu 22.04: undefined reference to  
`qt_resourceFeatureZstd'  
* QTBUG-103571 QWindowsContext::findPlatformWindowAt stuck in infinite  
loop  
* QTBUG-104809 Crash in QKmsDevice::createScreenForConnector  
* QTBUG-104583 Buffer overrun and crash in  
QColorTransferTable::applyInverse()  
* QTBUG-104696 QFontDialog:: selectedFont and fontSelected always  
returns one font  
* QTBUG-101161 Android Assets awfully slow to be loaded  
* QTBUG-104412 FAIL!  : tst_AndroidAssets during dependency update  
* QTBUG-101058 Pixelated images on Windows  
* QTBUG-104851 qdoc: Ignore Q_WEAK_OVERLOAD  
* QTBUG-104877 wacom: QTabletEvent rotation goes to -180 when absent  
* QTBUG-99136 QDockWidget not correctly parented/setup if dragged from  
another floating and tabified QDockWidget  
* QTBUG-104774 macOS: [Enter] key in TextField generates Qt.Key_Return  
instead of Qt.KeyEnter  
* QTBUG-103473 Regression: Pressing numeric keypad Enter doesn't dismiss  
QDialog containing QLineEdit  
* QTBUG-103892 Stop binding to iBridge interface when unit testing  
QTcpServer on macOS  
* QTBUG-102825 Popping QML StackView Item makes a11y unusable  
* QTBUG-104827 Huge APK sizes under Windows  
* QTBUG-98762 REGRESSION: QPalette::setBrush does not reliably detach  
* QTBUG-46113 tst_qcompleter fails on Ubuntu  
* QTBUG-49205 tst_qnetworkreply::ioGetFromBuiltinHttp  
* QTBUG-98921 tst_QGraphicsWidget::initialShow is uber flaky on OpenSUSE  
* QTBUG-104718 fuzz: QCborValue::fromCbor out of memory error 32bit  
* QTBUG-102239 tst_QWidget::enterLeaveOnWindowShowHide is flaky  
* QTBUG-100870 QtTestLib's blacklisting doesn't take global data tags  
into account  
* QTBUG-102269 Test cases can't be called with a global data tag  
* QTBUG-24240 testlib: executing a test with an invalid data label  
doesn't count as a failure and doesn't return a non-zero exit code  
* QTBUG-104213 Add \brief descriptions to Concurrent topics  
* QTBUG-82477 QClipboard doesn't support custom mimeTypes  
* QTBUG-104268  
tst_QTouchEvent::multiPointRawEventTranslationOnTouchPad() ASSERT  
failure in QList::at: "index out of range"  
* QTBUG-104270 cmake loads native sysroot cmake config and tries to look  
for libs  
* QTBUG-102879 Examples not linking to Qt::Core are installed in the  
wrong folder  
* QTBUG-105049 Improper styling of placeholder text in Qt6  
* QTBUG-104801 Crash with QPainter::drawText used on a QQuickView with a  
Text item  
* QTBUG-105310 Using deprecated keyword breaks the build  
* QTBUG-69354 QGtk3FileDialogHelper isn't modal  
* QTBUG-105041 openssl 3.x 32bit platform regression  
* QTBUG-105302 qputenv sometimes puts garbage at the end of the value  
* QTBUG-105010 Font underline rendering bug  
* QTBUG-104959 QT_NO_TRANSLATION define breaks QML build  
* QTBUG-105339 Typo in since version for QStyledItemDelegate  
* QTBUG-105517 Redundant "does" in QFrame  
* QTBUG-105501 Qt6 build fails with system double-conversion  
* QTBUG-101177 QTimer random segmentation fault (SIGSEGV)  
* QTBUG-101681 tst_QPointer::threadSafety() is flaky (probably race  
condition)  
* QTBUG-105341 QDoubleValidator can report "Intermediate" for inputs  
that are unambiguously out-of-range  
* QTBUG-105527 Vulkan validation shows (useless but annoying) "errors"  
with vkkhrdisplay  
* QTCREATORBUG-27685 Sliders Example not scaling well  
* QTBUG-105031 a11y AT-SPI: Window-relative positions are incorrect  
* QTBUG-105042 a11y AT-SPI: Window-relative positions are wrong for  
dialogs, screen coordinates returned instead  
* QTBUG-105281 a11y AT-SPI: incorrect handling of window-relative coords  
for "GetOffsetAtPoint" (text interface)  
* QTBUG-105520 a11y AT-SPI: "GetCaption" result (from AT-SPI table  
interface) has incorrect D-Bus type  
* QTBUG-102359  NTLM authentication crashes  
* QTBUG-102021 QCocoaScreen::UpdateScreens crash  
* QTBUG-84741 Crash on QCocoaScreen::isOnline() when calling  
CGDisplayIsOnline  
* QTBUG-101150 static initialisation fiasco with initializeWindowManager  
* QTBUG-105810 iOS: TapHandler emits clicked, even if long pressed more  
than StyleHint::MousePressAndHoldInterval  
* QTCREATORBUG-27634 Basic Layouts Example UI elemnets get squished  
* QTBUG-105286 Crash with UpdateWindowTitle event triggered by closing a  
dialog (mac)  
* QTBUG-105814 Accessibility tools cannot find tree items inside the  
app's UI on Windows  
* QTBUG-104740 Accessibility: NVDA not narrating full state of QTabBar  
* QTBUG-104940 post in/decrements of QBEInteger and QLEInteger return  
reference according to documentation  
* QTBUG-105374 Modules in 5.15 branch missing MinGW debug files  
* QTBUG-105231 reusing editor by reimplementing  
QAbstractItemDelegate::destroyEditor causes crashing  
* QTBUG-106001 tst_QMap::beginEnd() triggers assertion failure on  
Windows  
* QTBUG-56893 Closing a dialog via mouse click on a button causes an XCB  
error  
* QTBUG-105711 QDrag with invalid URLs in QMimeData crash on macOS  
* QTBUG-105951 Crash when closing dialog directly after closing popup  
* QTBUG-104917 QStyleSheetStyle::drawPrimitive(QStyle::PE_PanelLineEdit)  
crashes with widget==nullptr  
* QTBUG-106017 tst_QSslCertificate fails with Ubuntu 22.04 xorg and  
Windows 10 21H2 OpenSSL 3  
* QTBUG-92964 Empty tree not spoken  
* QTBUG-106019 tst_QDtls::verifyClientCertificate fails with Ubuntu  
22.04 xorg and Windows 10 OpenSSL 3  
* QTBUG-105004 Links to the code of examples for QCC2 were not updated  
at the move to QtDeclarative  
* QTBUG-105591 Closing application with toolbar floating breaks toolbar  
the next time you start the application  
* QTBUG-104014 tst_QPointer::threadSafety crashed in CI  
(QBindingStorage::reinitAfterThreadMove)  
* QTBUG-104872 Calling QClipboard::image() corrupts image inside Win 11  
clipboard memory (from Windows Snipping Tool)  
* QTBUG-105338 lose alphachannel in imagedata from QClipboard  
* QTBUG-99990 windows: Painting an image with DPR >1.0  to a QPrinter  
does not produce correct result  
* QTBUG-104930 QLocale shows German text for "en_DE"  
* QTBUG-106374 Unable to build qtbase due to incomplete type in  
qtessellator.cpp  
* QTBUG-103988 State of QTreeWidgetItem not announce by screenreader  
* QTBUG-105735 Focus is not set to a child widget when a modal is open  
* QTBUG-106222 -junitxml produces invalid time in output log (seconds  
divided by 1000 instead of seconds)  
* QTBUG-106223 assertion failed after Flickable takes grab from  
PinchHandler  
* QTBUG-103740 QTemporaryFile::rename does not document that it can only  
rename, not copy+delete like QFile::rename  
* QTBUG-106279 I doubt if QTextStream setAutoDetectUnicode doesn't work  
* QTBUG-104999 crash in QTextMarkdownWriter  
* QTBUG-104205 QDockwidget screen change issue(s) more involved parts.  
* QTBUG-102091 [Reg Qt 5->6] Disabled QCheckBoxes block scrolling of  
QScrollArea with mouse wheel  
* QTBUG-105932 [Reg in Qt 6] setProperty() fails for QFlags types  
* QTBUG-96185 Cannot use  "qproperty-" to set enum properties in qss  
* QTBUG-96276 _NET_STARTUP_ID not supported  
* QTBUG-91774 QTextEdit::cursorForPosition() doesn't work with invisible  
blocks  
* QTBUG-106036 Tst_QSslKey fails with Windows 1021H2 and openssl 3  
* QTBUG-105160 Bad access when destroying QComboBox immediately after  
selecting item  
* QTBUG-105043 HTTP2 downloads can be very slow  
* QTBUG-104948 QFileDialog::getOpenFileContent not honoring nameFilter  
* QTBUG-103093 Palette Change And Application PaletteChange Never Emited  
* QTBUG-105057 vnc: Setting override cursor causes a crash on client  
disconnect  
* QTBUG-106463 Make QT_HOST_PATH well visible and communicated clearly  
* QTBUG-105140 [REG] default constuctor requirement for meta type  
(QVariant) breaks webengine api  
* QTBUG-103992 QFuture::onCanceled is not called when promise is deleted  
* QTBUG-104580 androiddeployqt fails with "unknown argument '--libs'"  
when call llvm-readobj v14  
* QTBUG-103753 incorrect document about QDomDocument::setContent()  
* QTBUG-104857 QtBase does not compile with QT_DISABLE_DEPRECATED_BEFORE  
= 0x060000  
* QTBUG-102594 [REG 5.15.6 -> 5.15.9] Many ANR issues by QtAccessibility  
* QTBUG-103706 Synthesized touch event not recognized with Widgets  
* QTBUG-104878 xcb wacom support gets confused about device instances  
* QTBUG-87414 tst_QLocale::initTestCase fails on Android  
* QTBUG-101932 two HoverHandlers with different  
acceptedDevices/acceptedPointerTypes: cursorShape doesn't change  
accordingly  
* QTBUG-104787 Thread Sanitizer reports data races in QtConcurrent  
* QTBUG-89702 Improve the QRegExp->QRegularExpression docs  
* QTBUG-105051 pkg-config does not expose libexecdir for finding some  
tools  
* QTBUG-85248 Qt warning  
"QHttpNetworkConnectionPrivate::_q_hostLookupFinished could not de-queue  
request, failed to report HostNotFoundError"  
* QTBUG-105038 QCollator is limited to ≤ 2Gi characters  
* QTBUG-102403 QObject::objectName() leads to heap-use-after-free in  
tst_qquickanimations::cleanupWhenRenderThreadStops()  
* QTBUG-105048 QSqlQuery is supposed to be move-only, however we copy it  
in our code  
* QTBUG-104730 androidtestrunner splits data row names by whitespace and  
treats them as test functions  
* QTBUG-98988 Qt bugs when portal implementation is not available  
* QTBUG-105736 tst_qfile unixPipe and socketPair tests fail on Android  
12  
* QTBUG-105738 tst_qopengl:: fboRenderingRGB30() fails on Android 12  
* QTBUG-105739 tst_vulkan vulkan11() and vulkanWindowGrab() fail on  
Android 12  
* QTBUG-103591 Windows: Comboboxes (Qml and QtWidgets) don't have the  
UIAutomation (UIA) ExpandCollapse pattern  
* QTBUG-106018  tst_QSslSocket fails with Ubuntu 22.04 xorg and Windows  
10 21H2 plus OpenSSL 3  
* QTBUG-83185 [Android]: When using night or dark mode on a device, then  
the style extracted is still set as if it is light mode  
* QTBUG-105388 qhash.h:553:17: warning: argument 1 value  
'18446744073709551615' exceeds maximum object size 9223372036854775807  
* QTBUG-105958 [Android] Intent + Talkback leads to deadlock  
* QTBUG-103499 Android a11y: Flickable items outside of view are not  
selectable  
* QTBUG-103513 A11Y: Flickable child item focus frame position not  
updated  
* QTBUG-87728 tst_QGraphicsAnchorLayout::layoutDirection() failed on  
Ubuntu 20.04 in CI  
* QTBUG-63481 tst_QSslSocket_onDemandCertificates_member::onDemandRootCe  
rtLoadingMemberMethods tests fail in the CI  
  
### qtsvg  
* QTBUG-101698 [REG 6.2.2 -> 6.2.3] Integer overflow when loading svg  
image  
  
### qtdeclarative  
* QTBUG-104258 tst_QQuickPopup::Material fails with Ubuntu 22.04  
* QTBUG-104603 Clarify the QML_EXTENDED documentation  
* QTBUG-101488 tst_QQuickFileDialogImpl is flaky  
* QTBUG-104642 iOS: TextField has blinking cursor, but no input panel is  
showing  
* QTBUG-104625 tst_Qmlls::testWorkspace fails  
* QTBUG-104491 mouse event broken after continuous transition animation  
in StackView.  
* QTBUG-104242 tst_QQuickDrawer tests are failing with Ubuntu 22.04  
* QTBUG-104257 tst_QQuickMenu(bar) tests are failing with Ubuntu 22.04  
* QTBUG-104698 tst_qqmllanguage::(installed)() Function not found:  
(installed)  
* QTBUG-104657 Custom ComboBox does not function properly with model  
passed from c++  
* QTBUG-104803 Crash when calling QJSValue::hasProperty("x") from Qml on  
a QVector3D received from a Q_PROPERTY  
* QTBUG-101973 File Dialog does not re open in some situation.  
* QTBUG-104325 QQuickPointerHandler::currentEvent() exposes stale event  
* QTBUG-101008 Using Text.NativeRendering results in characters drawn  
too close to each other with fractional scale factors  
* QTBUG-98769 QML StackView heap-use-after-free on pop()  
* QTBUG-104865 QQuickPaddedRectangle emits topPaddingChanged incorrectly  
* QTBUG-103081 QQmlComponent::create() crashes when creeating a  
QML_EXTENDED_NAMESPACE(Type) object when Type is a Q_OBJECT extending a  
property  
* QTBUG-104700 QQuickDialog::accept() slot not executed when called from  
QML when making QPlatformDialogHelper::StandardButtons available via  
QML_EXTENDED_NAMESPACE  
* QTBUG-90466 Missing line number in tst_qquickloader error message on  
macOs  
* QTBUG-91687 QML fails to run benchmarks in qmlbench's v8bench  
directory  
* QTBUG-58559 Deletion of a dynamic properties to JSObject ends up using  
all memory  
* QTBUG-104197 qmllint: unknown attached property scope T.  
* QTBUG-94983 Crash when binding to aliased grouped property  
* QTBUG-98914 QML Test with grabImage() fails on iOS  
* QTBUG-105239 Split "Module Definition qmldir Files"'s table  
* QTBUG-105566 Touch panning a ListView in View3D broken  
* QTBUG-105058 PathView steals touch event of PinchArea delegate  
* QTBUG-104983 [REG] 908aa77d16e00f2bccc0ddae0f8b61955c56a6a1 breaks  
scrollbars if contentItem is accessed before it is set  
* QTBUG-92192 Issues calling JSON.stringify() on objects  
* QTBUG-87119 MouseArea inside SplitView item takes mouse events away  
from Splitview handle  
* QTBUG-97385 QtQuick SplitView with Flickable gets stuck  
* QTBUG-95232 Qt Quick Local Storage does not work with absolute paths  
* QTBUG-89567 [REG 5.15.0 -> 5.15.1] Qt.labs.platform.MenuItem is  
triggering shortcut even in disabled state  
* QTBUG-104022 tst_SignalSpy::testCount fails in CI on macOS  
* QTBUG-105907 Use the time stamp of the touch event when deliver touch  
as mouse  
* QTBUG-103832 The delegate item of ListView is not pressed if the  
boundsBehavior is to set Flickable.StopAtBounds  
* QTBUG-38765 When propagateComposedEvents is set, drag does not always  
move the flickable  
* QTBUG-74842 Flickable behind MouseArea does not steal first drag event  
after creation  
* QTBUG-104471 tst_QQuickListView2::tapDelegateDuringFlicking fails on  
Android  
* QTBUG-105812 Small typo in Accessible.description documentation  
* QTBUG-93603 Document that mixing old/new forms in QML Connections  
causes new form to not work  
* QTBUG-92068 Remote loading ui files in Qml fails to load from existing  
directory  
* QTBUG-104084 tst_qmldomitem ERROR: AddressSanitizer: alloc-dealloc-  
mismatch  
* QTBUG-105860 REG: Dialog box and action bar buttons missing in  
texteditor example  
* QTBUG-106110 PinchHandler.minimum/maximumScale properties aren't  
enforced with native gestures  
* QTBUG-104966 The Items in the ListView is not showing when the model  
is changed during dragging  
* QTBUG-105899 ColorDialog: The text fields on ColorInputs.qml are buggy  
for the Fusion, Imagine and Universal styles.  
* QTBUG-106347 Build warns about QML code in C++ header with extension  
".hh"  
* QTBUG-106392 Alias is invalid when accessed from C++ via  
QObject::property()  
* QTBUG-106098 ComboBox: The implicitContentWidthPolicy property doesn't  
work for the Imagine style  
* QTBUG-93188 tst_qqmlecmascript::gcCrashRegressionTest fails with ARM  
macOS 11 in Qt Declarative  
* QTBUG-102339 Conan: multiple prefixes not supported when building e.g.  
examples  
* QTBUG-103924 GCC 12: failure to build from source [<QtDeclarative>]  
* QTBUG-86729 many Qt Quick test failures after input event refactoring  
* QTBUG-101736 QQuickWidget: button in a popup doesn't receive touch end  
event  
* QTBUG-89927 tst_qquickfontloader::changeFontSourceViaState fails with  
macOS 10.15 and Xcode 12.3  
* QTBUG-102984 tst_QQmlDebugJS hangs on macOS in CI  
* QTBUG-101678 tst_qqmlinspector (and other tests in  
tests/auto/qml/debugger/) times out on macOS 12 (x86_64) in CI  
* QTBUG-101932 two HoverHandlers with different  
acceptedDevices/acceptedPointerTypes: cursorShape doesn't change  
accordingly  
* QTBUG-104928 qmlimportscanner: segfault on unexpected argument  
* QTBUG-105149 QML ComboBox displays an unwanted shadow effect on  
Android  
* QTBUG-94919 Control changes hover state even though it is disabled  
* QTBUG-103513 A11Y: Flickable child item focus frame position not  
updated  
* QTBUG-101499 FAIL!  : tst_QQuickMultiPointTouchArea::nonOverlapping in  
Ubuntu_20_04  
* QTCREATORBUG-3708 Context sensitive help does not work for several QML  
properties  
* QTBUG-101662 Dialog Header/Footer cover over background instead of  
being inset  
  
### qtmultimedia  
* QTBUG-104483 ASSERT: "viewport.size() == size" in  
qquickvideooutput.cpp  
* QTBUG-104133 QML animation overlaid on video becomes unusably slow &  
with increasing memory consumption over time  
* QTBUG-102772 Declarative-camera preview freezes when takes photo  
* QTBUG-105381 Qt Multimedia fails to read crop info from a HEVC video  
stream's VPS.  
* QTBUG-106092 Binding to CaptureSession.imageCapture fails  
* QTBUG-99022 Android: Changing a Audio sink on Audiooutput example  
issue  
* QTBUG-98121 Android: Filters out unsupported audio codecs(flac) on  
AudioRecorder app  
  
### qttools  
* QTBUG-104713 GCC 12: failure to build from source [<QtTools>]  
* QTBUG-105130 qttools: CMake failure if litehtml is found on the system  
* QTBUG-102607 macdeployqt: errors when producing a universal binary  
(universal binary)  
* QTBUG-105097 \since says the macro is a function even if it isn't  
* QTBUG-104490 qhelpgenerator can't find QSqlDatabase drivers in static  
builds  
* QTBUG-105987 Make order of elements in .qhp deterministic  
* QTBUG-86507 ASSERT: "it.isUnused()" in file  
/home/qt/work/install/include/QtCore/qhash.h, line 525  
  
### qtpositioning  
* QTBUG-104448 Fix QtPositioning tests for static builds  
* QTBUG-104465 It is impossible to build tests with custom plugins in  
static build configurations  
  
### qtconnectivity  
* QTBUG-104479 (Classic) bluetooth service scan sometimes hangs  
indefinitely on Android  
* QTBUG-97797 QBluetoothDeviceDiscoveryAgent take CPU/Ram usage to 100%  
* QTBUG-105556 BT LE repeated characteristic recurses into event loops  
until it crashes on Windows  
* QTBUG-105803 tst_qbluetoothdevicediscoveryagent and  
tst_qbluetoothservicediscoveryagent fail on Android 12 in CI  
* QTBUG-106029 Crash during device discovery in Qt RO bleclient example  
* QTBUG-105742 Memory leak in BLE discovery  
* QTBUG-104914 tst_qbluetoothlocaldevice and tst_qbluetoothserver tests  
fail on Android 12 emulator in CI  
* QTBUG-94001 QtBluetooth uses deprecated Windows API  
  
### qtwayland  
* QTBUG-104227 QWaylandTextInput: Not possible to inject keys with  
Shift- or Ctrl-Modifiers  
* QTBUG-105308 ASSERT failure in QWindow: "Updates can only be scheduled  
from the GUI (main) thread"  
  
### qt3d  
* QTBUG-104593 Qt3D Application Crashes when rendering first frame  
* QTBUG-104592 RHI Render Capture crashed with debug build  
* QTBUG-101949 A crash occurred in C:\Users\qt\work\qt\qt3d_standalone_t  
ests\tests\auto\render\scene2d\tst_scene2d.exe.  
  
### qtimageformats  
* QTBUG-104692 qtimageformats breaks top-level build  
  
### qtserialbus  
* QTBUG-106524 Typo in the document  
  
### qtserialport  
* QTBUG-101444 QSerialPort: trouble with high baud rates /  
waitForReadyRead() stalls  
  
### qtwebengine  
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
* QTBUG-104763 WebEngine view becomes white if minimized and restored  
* QTBUG-106090 moc_qquickwebenginesingleton_p.cpp:38:69: error: use of  
undeclared identifier 'QtMocHelpers'; did you mean  
'::TestNamespace::TestNamespace::QtMocHelpers'?  
* QTBUG-106241 Qt build from source failed  
* QTBUG-100391 Application built with Qt 6.2.2 fails to run because of  
missing mf.dll error  
* QTBUG-106461 QWebEngineUrlRequestJob::reply() does not support a  
QIODevice that cannot be read completely instantly  
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
  
### qtwebview  
* QTBUG-102712 qtwebview tests fail on Android  
* QTBUG-102801 qtwebview setAndDeleteCookie tests crash on Android  
  
### qtcharts  
* QTCREATORBUG-27650 Pie Chart Customization Example doesn't scale  
properly  
  
### qtdatavis3d  
* QTBUG-105398 Q3DScatter should fail gracefully when mesh is missing UV  
coordinates  
  
### qtscxml  
* QTBUG-98368 Dependency cycle in qtscxml  
  
### qtremoteobjects  
* QTBUG-74124 QAbstractItemModelReplica internal error crash  
* QTBUG-97790 Generated SourceAPI class can't be used without compiler  
warnings  
* QTBUG-106003 remoteobjects does not checks for Declarative's private  
headers existance, but makes use of them  
  
### qtquick3d  
* QTBUG-105566 Touch panning a ListView in View3D broken  
  
### qt5compat  
* QTBUG-89702 Improve the QRegExp->QRegularExpression docs  
  
### qtmqtt  
* QTBUG-105873 QMqttClient documentation does not include the  
constructor  
  
### qtopcua  
* QTBUG-104646 [C++20 FTBFS] open62541.h is running afoul of volatile  
compound statement deprecation in C++20  
  
Known Issues  
------------  
  
Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-6.2/supported-platforms.html  
  
The RTA (release test automation) reported issues in Qt 6.2.x:  
https://bugreports.qt.io/issues/?filter=23315  
  
Qt 6.2.6 Open issues in Jira:  
https://bugreports.qt.io/issues/?filter=24494  
  
### Boot2Qt  
* A fix for an Intel QBSP-specific issue (QTBUG-106660: Building a  
  custom image for intel-skylake-64 fails) was included in the released  
  QBSP image. However, the fix's commit is not present in the  
  corresponding meta-boo2qt release branch (lts-6.2.6).  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Mike Achtelik  
Chris Adams  
Laszlo Agocs  
Dimitrios Apostolou  
YAMAMOTO Atsushi  
Mate Barany  
Nicholas Bennett  
Eskil Abrahamsen Blomfeldt  
Mikolaj Boc  
Joerg Bornemann  
Assam Boudjelthia  
Michael Brüning  
Igor Bugaev  
Alexandru Croitor  
Mitch Curtis  
Thibaut Cuvelier  
Giuseppe D'Angelo  
Alexey Edelev  
Oliver Eftevaag  
Iikka Eklund  
Andreas Eliasson  
Ilya Fedin  
Alexandros Frantzis  
Pekka Gehör  
Maximilian Goldstein  
Andrei Golubev  
Jan Grulich  
Richard Moe Gustavsen  
Tang Haixiang  
Heikki Halmet  
Elias Hautala  
Jani Heikkinen  
Christian Heimlich  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Dominik Holland  
Allan Sandfeld Jensen  
Friedemann Kleint  
André Klitzing  
Michal Klocek  
Seokha Ko  
Jarek Kobus  
Sze Howe Koh  
Tomi Korpipaa  
Fabian Kosmale  
Volker Krause  
Mike Krus  
Jaroslaw Kubik  
Sona Kurazyan  
Kai Köhne  
Inho Lee  
Paul Lemire  
Thiago Macieira  
Thorbjørn Lund Martsum  
Samuel Mira  
Fawzi Mohamed  
Bartlomiej Moskal  
Marc Mutz  
Antti Määttä  
Martin Negyokru  
Mårten Nordheim  
Laszlo Papp  
Bumjoon Park  
Samuli Piippo  
Timur Pocheptsov  
Joni Poikelin  
Liang Qi  
Topi Reinio  
André de la Rocha  
Niclas Rosenvik  
Shawn Rutledge  
Michael Saxl  
Eli Schwartz  
Sami Shalayel  
Andy Shaw  
Venugopal Shivashankar  
Ivan Solovev  
Axel Spoerl  
Piotr Srebrny  
Elias Steurer  
Tarja Sundqvist  
Tasuku Suzuki  
Jan Arve Sæther  
Morten Sørvig  
Mike Trahearn  
Jens Trillmann  
Peter Varga  
Louis du Verdier  
Doris Verria  
Tor Arne Vestbø  
Petri Virkkunen  
Ville Voutilainen  
Juha Vuolle  
Michael Weghorn  
Edward Welbourne  
Fushan Wen  
Paul Wicking  
Oliver Wolff  
Lu YaNing  
JiDe Zhang  
Yuhang Zhao  
