Release note  
============  
  
Qt 6.4.1 release is a patch release made on the top of Qt 6.4.0.  
As a patch release, Qt 6.4.1 does not add any new functionality but provides  
bug fixes and other improvements and maintains both forward and backward  
compatibility (source and binary) with Qt 6.4.0.  

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
* d7620f1b74 Fix crash when setting override cursor on multiple clients  
Fixed a crash when setting an override cursor on multiple clients.  
  
* 75a9a0ad5e Update bundled libjpeg-turbo to version 2.1.4  
libjpeg-turbo was updated to version 2.1.4  
  
* b627f51978 Document QAtomic testAndSet  
Documented new overloads of testAndSet() that were originally added for  
5.3.  
  
* 1cb57091ac Revert "Keep original text for text/plain mime data"  
The fix to preserve special characters like &nbsp; the text/plain part  
of the clipboard when copied from a QTextEdit or QLineEdit had to be  
reverted (QTBUG-107004).  
  
* ed3d60cfca QTaggedPointer: disable operator= with an empty initializer  
list  
The operator assignment taking a raw pointer has been reimplemented in  
order to avoid subtle issues when assigning `{}` to a QTaggedPointer.  
This will cause code that assigns a braced-init-list to a QTaggedPointer  
object to stop compiling (for instance, `tagPtr = {ptr}` is now ill-  
formed).  
  
* a111c15c0a Skip early return from test loops during cleanup()  
During the cleanup() phase of a test, the QTRY_* macros and  
QTestEventLoop now ignore the test resolution, in contrast to when they  
are used from the test itself, which (since 6.3.0) exits the loops early  
if the test has failed.  
  
* 9ac433b40a Fix generating PDFs with DirectWrite engine  
Fixed glitches in generated PDFs when the DirectWrite backend was in  
use, e.g. when high-dpi scaling was active.  
  
* c0b54bf6fa macOS: Fix less common writing systems on Catalina and  
later  
Fixed missing text with certain writing systems on macOS Catalina and  
later.  
  
* c2f85da3be Update bundled libpng to version 1.6.38  
libpng was updated to version 1.6.38  
  
* e0fea817a5 QBenchlib/Perf: don't try to benchmark the kernel  
Fixed support of Linux performance counters for QBENCHMARK, which used  
to fail with "Permission denied" errors in default configurations. Now,  
QtTest will automatically fall back to profiling only userspace, like  
the perf(1) tool does.  
  
### qtdeclarative  
* ef6fe3e499 DA: ignore disabled HoverHandlers when delivering hover  
events  
Disabled hover handlers will no longer receive hover events, or block  
siblings from being hovered.  
  
### qttools  
* 838f8e2e0 QDoc: Remove the "\newcode" and "\oldcode" command pair  
The deprecated \oldcode, \newcode commands were removed.  
  
* ab89fee0b qdoc: Enable correct linking to externally-built  
dependencies  
  
  
### qt5compat  
* 16774f1 Avoid recreating gaussian blur shader multiple times  
Improve creation time of Gaussian Blur-based effects.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-105057 vnc: Setting override cursor causes a crash on client  
disconnect  
* QTBUG-105923 WebAssembly loader broken when using the CMake  
RUNTIME_OUTPUT_DIRECTORY property  
* QTBUG-105347 [Wasm] Stack example from documentation exits application  
* QTBUG-102004 [wasm] QML switch does not react on toggle  
* QTBUG-104518 Swipeview doesn't function correctly in Webassembly app  
* QTBUG-106153 wasm: Changing QTimer interval in multithreaded  
application breaks the timer  
* QTBUG-106223 assertion failed after Flickable takes grab from  
PinchHandler  
* QTBUG-91774 QTextEdit::cursorForPosition() doesn't work with invisible  
blocks  
* QTBUG-106064 [REG] Undocking QDockWidget with drag misplaces it (a  
lot)  
* QTBUG-106279 I doubt if QTextStream setAutoDetectUnicode doesn't work  
* QTBUG-105711 QDrag with invalid URLs in QMimeData crash on macOS  
* QTBUG-106000 tst_QLocale::fpExceptions() triggers assertion failure on  
Windows  
* QTBUG-104930 QLocale shows German text for "en_DE"  
* QTBUG-106374 Unable to build qtbase due to incomplete type in  
qtessellator.cpp  
* QTBUG-106222 -junitxml produces invalid time in output log (seconds  
divided by 1000 instead of seconds)  
* QTBUG-106394 Android Multi ABI honors only for first abi the flag  
-DQT_NO_PACKAGE_VERSION_CHECK=TRUE  
* QTBUG-106463 Make QT_HOST_PATH well visible and communicated clearly  
* QTBUG-104999 crash in QTextMarkdownWriter  
* QTBUG-104856 Non-Qt headers in 6.3.1\msvc2019_64\include  
* QTBUG-106354 Last QNetworkReply::readyRead() is not always emitted  
* QTBUG-106016 tst_QNetworkReply::contentEncodingBigPayload fails with  
Ubuntu 22.04 xorg and Rhel 9  
* QTBUG-106560 WASM: Menus are resizable  
* QTBUG-106397 wasm: native keyboard does not popup on iOS  
* QTBUG-106573 QNetworkAccessManager can not get 404 reponse body.  
* QTBUG-42661 Wrong dialog activation  
* QTBUG-23699 tst_QGraphicsWidget::updateFocusChainWhenChildDie() fails  
on Mac OS X  
* QTBUG-106652 applicationName() default value broken on macOS  
* QTBUG-105618 QNetworkReplyFileImpl synchronously emits  
QNetworkReply::finished() from constructor in case of error  
* QTBUG-7211 QFile::permissions() returns old, cached value after call  
to QFile::setPermissions() on the same QFile object  
* QTBUG-101236 FAIL!  : tst_QPainter::hdrColors in Windows_11_21H2  
* QTBUG-106393 Mac OS: Dot and Comma key combinations not working for  
russian layout  
* QTBUG-36281 QKeyEvent regression in Qt5  
* QTBUG-35734 When pressing CTRL+SHIFT+number on a German keyboard then  
the key() you get in the key press is not always as expected  
* QTBUG-87339 wasm: Emoji couldn't show while the text contains Chinese  
and emoji mix  
* QTBUG-71948  Containers with drag "rubber band effect" should react on  
pointer cancel  
* QTBUG-106436 Scene Graph - Direct3D 11 Under QML Example has wrong tag  
* QTBUG-106438 Scene Graph - Metal Texture Import Example has wrong tag  
* QTBUG-106439 Scene Graph - Metal Under QML Example has wrong tag  
* QTBUG-106469 QQuickRenderControl D3D11 Example has wrong tag  
* QTBUG-106668 Cannot paste content from external sources  
* QTBUG-89557 QML Text's implicitWidth is wrong when wrapMode is set for  
multiline text.  
* QTBUG-104986 QTextLayout::maximumWidth() is not correct for multi-line  
text  
* QTBUG-104805 QColorDialog : Buttons are highlighted incorrectly  
* QTBUG-103503 Frameless window is resizable  
* QTBUG-106710 Regression: macOS windows with Qt::FramelessWindowHint  
are resizable  
* QTBUG-105182 Access violation / infinite loop in  
QFutureInterfaceBase::isChainCanceled()  
* QTBUG-106083 QFuture::then(QObject *context, Function &&function)  
throws "read access violation" when used in chained QFuture  
* QTBUG-106616 androiddeployqt not found on MultiABI android build with  
custom install dir  
* QTBUG-106672 [Reg: 6.3 -> 6.4] C3615: constexpr function  
'QtPrivate::QMetaTypeForType<T>::getName' cannot result in a constant  
expression  
* QTBUG-106531 QDockWidget Docking resizes (widens) the widget by a set  
number of pixels  
* QTBUG-106689 QNetworkReply: it is confusing whether the reply data has  
been decompressed or not.  
* QTBUG-106387 Application crash when writing in textfield  
* QTBUG-106899 tst_qquicktext::dependentImplicitSizes() Compared doubles  
are not the same  
* QTBUG-106530 QDockWidget Undocking incorrectly offset from cursor  
(native titlebar) when dragging  
* QTBUG-101339 Hardware keyboard up/down keystrokes interpreted as  
home/end when interacting with a QML TextArea  
* QTBUG-106980 dladdr() in qlogging.cpp - error: invalid conversion from  
'const void*' to 'void*'  
* QTBUG-107004 Copying from QTextEdit to other program turns newline  
into paragraph separator (U+2029)  
* QTBUG-107043 Qt 6.4 QDateTime is broken with clang-cl when compiling  
with c++20  
* QTBUG-100917 tst_QImageReader::setScaledClipRect() SVG/SVGZ fails on  
Wayland  
* QTBUG-81044 SVG: QImageReader::setScaledClipRect() uses wrong  
coordinate system  
* QTBUG-92199 [REG] The color of QLineEdit and QPlainTextEdit  
placeholder text is not grayed-out if stylesheet was applied  
* QTBUG-93009 QPalette::PlaceholderText color is not followed after  
setting color in a style sheet  
* QTBUG-107072 build chooses unavailable hardware flags  
* QTBUG-106607 QODBC: QSqlQuery::isNull returns false for SELECT NULL  
* QTBUG-69608 cocoa: key press events for modifier keys do not have  
nativeVirtualKey  
* QTBUG-106984 Setting background brush in QTableWidgetItem used as  
header item is incorrectly cached leading to incorrect display colours  
* QTBUG-106219 [macOS] Typing accented/alternate characters doesn't work  
correctly  
* QTBUG-105984 windeployqt: Multimedia plugins missing  
* QTBUG-107178 plugins/platforms/libqminimal.so' is not a valid ELF  
object (file is for a different processor)  
* PYSIDE-2069 pyside6-uic generates dynamic properties with C++ types  
* QTBUG-106912 MoltenVK: Failed to create Vulkan instance when  
implementation supports is_portability_driver  
* QTBUG-104441 REG: No longer possible to use macros or functions that  
rely on an event loop in cleanup() after failed test function  
* QTBUG-100891  
tst_QGuiApplication::genericPluginsAndWindowSystemEvents() fails on  
Wayland  
* QTBUG-100918 tst_QOpenGL::bufferMapRange() fails on Wayland  
* QTBUG-107128 qtbase/src/dbus/dbus_minimal_p.h SPDX-License-Identifier  
misses AFL-2.1  
* QTBUG-107174 Units unclear for QWaitCondition::wait  
* QTBUG-107038 Non-aliased Text is rendered incorrectly using  
NativeRendering  
* QTBUG-97697 Missing documentation for GrabTransition enum in  
DragHandler  
* QTBUG-107246 QVariant.toList method not working properly  
* QTBUG-107188 Reg: Behavior Change: Modal dialogs seem to block events  
to other dialogs/widget  
* QTBUG-107544 [Reg 6.3.2 -> 6.4.0] qsql_oci.cpp no longer compiles  
* QTBUG-107155 tst_QWidget_window::resetFocusObjectOnDestruction() with  
QtWayland failed on Ubuntu 22.04, GNOME  
* QTBUG-107166 QQuickWidget causes crash when combined with dock and  
toolbar  
* QTBUG-107262 REG: Enter on r/o QComboBox does not close a dialog  
anymore  
* QTBUG-107569 Use of std::aligned_union and std::aligned_union_t  
deprecated in C++23  
* QTBUG-104831 windeployqt does not deploy Designer plugins for  
QUiLoader  
* QTBUG-107719 Typo in the document?  
* QTBUG-107450 Reg[5->6]QSlider handle size is not correct  
* QTBUG-79977 QMessageBox does not work at  IOS 13  
* QTBUG-101000 macOS: QPushbutton text color changes  
* QTBUG-105292 Documented way of printing whole document produces  
warning  
* QTBUG-107249 [REG 6.4.0->6.5.0] Can not compile Qt examples with  
Android armv7 pre-build binaries on linux and macOS  
* QTBUG-107777 Typo in the document  
* QTBUG-77210  QML Image object causes a crash when it gets deleted  
while it's still loading  
* QTBUG-102098 QPrinter::PdfFormat causes some fonts to be doubly-scaled  
when using DirectWrite font engine  
* QTBUG-47979 QDesktopServices is unable to open a file on Android  
* QTBUG-106713 android.bundle.enableUncompressedNativeLibs=false  
deprecated in Android Gradle plug-in ver 8.0  
* QTBUG-85773 QML TextEdit copy() copies text twice on Android  
* QTBUG-100245 tst_qsqlquery should not create unique data tags when  
testing  
* QTBUG-107618 QFileDialog freeze when selecting large zip-file using  
the windows native dialog  
* QTBUG-96384 Tagalog cannot be displayed correctly  
* QTBUG-98920 Font fallback is not working properly on macOS  
* QTBUG-107539 wasm: 2dpainting sample not working with  
webassembly/webgl  
* QTBUG-107629 [REG 6.3->6.4] WebEngineWidget OpenGL rendering is broken  
on Windows  
* QTBUG-107627 AndroidAssetsFileEngineHandler is broken  
* QTBUG-107814 Reg:[6.3->6.4]QOpenGLWidget tries to render duplicate  
controls  
* QTBUG-104709 [REG. 6.2->6.3] macOS: Default Edit menu entries shown  
twice  
* QTBUG-106542 qCompress()/qUncompress() cannot handle more than 4GiB of  
data on Win64  
* QTBUG-106227 Alternate row background color does not starts from  
beginning  
* QTBUG-107649 valgrind issue due to 9 bits in flags  
* QTBUG-107879 FAIL!  : tst_AndroidAssets::loadsFromAssetsPath  
* QTBUG-80992 QT_SCALE_FACTOR don't work properly with WebAssembly  
* QTBUG-106277 QProperty fails to compile on MSVC in C++20 mode  
* QTBUG-107843 cmake: multi-ABI Android builds do not work in-tree  
* QTBUG-107720 "This feature is not supported on the Windows platform."  
is a bit vague  
* QTBUG-104319 Program crash on exit after monitor disconnect  
* QTBUG-98354 Windows 11: State of checkable QAction with icon is not  
shown  
* QTBUG-105472 WASM version of QFileDialog::getOpenFileContent not  
honoring nameFilter  
* QTBUG-107991 QString asprintf behaves differently than printf with  
"%03.f" format for example  
* QTBUG-107008 window list in macOS' dock icon context menu includes  
entry for QSystemTrayIcon  
* QTBUG-106108 REG/macOS:  context menu corners are not rounded  
* QTBUG-106368 Wrong Usage of DoDragDrop() Causes Drag and Drop via  
Touch to Hang  
* QTBUG-57577 Windows: Drag and drop through touch sometimes gets stuck  
with -platform windows:nomousefromtouch  
* QTBUG-100788 TapHandler tapped signal is emitted twice when using a  
stylus  
* QTBUG-77414 Drag and Drop with mimeData does not work properly on the  
touch screen  
* QTBUG-104594 qpushbutton: pressed signal not emitted until button is  
released, unsing touchscreen as input  
* QTBUG-91882 eglfs with a cloned screen cause app to flicker  
* QTBUG-105707 EGLFS: Modal windows get stacked behind non-modal windows  
* QTBUG-103611 [Reg 5.15 -> 6.x] Re-initializing QGuiApplication causes  
QQmlApplicationEngine to crash  
* QTBUG-108039 Error with qproperty: expression  
‘std::source_location::current()’ is not a constant expression  
* QTBUG-105857 Qt application does not follow the DPI change when the  
DPI setting is changed before showing the first window  
* QTBUG-106983 Wrong description in documentation for  
QPartialOrdering::Greater  
* QTBUG-107687  [REG 6.3.1 -> 6.3.2] qt_add_resources with .qm  
translation files no longer rebuild generated .qrc when .qm files change  
* QTBUG-108113 "RCC: Cannot find file" in qt_add_translations  
* QTBUG-103470 [iOS] CMake translation handling fails  
* QTBUG-108156 Unhandled exception on QNetworkInformation::load()  
* QTBUG-106018  tst_QSslSocket fails with Ubuntu 22.04 xorg and Windows  
10 21H2 plus OpenSSL 3  
* QTBUG-106020 tst_QSocks5SocketEngine::passwordAuth fails with Ubuntu  
22.04 xorg  
* QTBUG-41170 [Android]: When the window resizes then there it will  
cause flicker  
* QTBUG-66727 [Android]: When changing focus between TextInput fields  
there is a flicker of the QQuickWidget  
* QTBUG-84258 tst_Gestures::graphicsItemGesture fails  
* QTBUG-103054 FAIL!  : tst_Gestures::graphicsItemGesture in  
Ubuntu_20_04  
* QTBUG-106071 Example code in QPropertyAnimation documentation has  
memory leak  
* QTBUG-35409 MouseArea does not detect mouse pointer if it was already  
there on Mac OS X  
* QTBUG-100324 QHelpEvent::globalPos() returns frequently a wrong value.  
* QTBUG-106939 Error: "qmlimportscanner not found" while building  
examples while using cmake  
* QTBUG-106712 HostPrefix & HostData reference incorrect dir in  
target_qt.conf (when cross compiling)  
* QTBUG-107538 OpenSUSE 15.3 developer build with OpenSSL 3 fails:  
‘QSslSocket’ has not been declared  
* QTBUG-107157 tst_QWidget with QtWayland failed on Ubuntu 22.04, GNOME  
* QTBUG-107186 tst_QCompleter::showPopupInGraphicsView() with QtWayland  
failed on Ubuntu 22.04, GNOME  
* QTBUG-107184 tst_QGridLayout::setMinAndMaxSize() with QtWayland  
crashed on Ubuntu 22.04, GNOME  
* QTBUG-107578 tst_selftests failed with qtwayland qpa plugin on Ubuntu  
22.04 GNOME  
* QTBUG-107158  
tst_QTouchEvent::multiPointRawEventTranslationOnTouchPad() with  
QtWayland failed on Ubuntu 22.04, GNOME  
* QTBUG-107154 tst_QWidget_window::mouseMoveWithPopup(Dialog) with  
QtWayland failed on Ubuntu 22.04 GNOME  
* QTBUG-106925 Context menus on mac os 12.5.1 are resizeable (and not  
native in appearance)  
* QTBUG-99795 Mouse scroll wheel can't be used to interact with  
scrollable elements on iOS  
* QTBUG-106896 QDir::drive() does not shows DVD drive  
* QTBUG-63324 iOS/macOS: system localization always returns english  
language  
* QTBUG-106082 [Qt 3D] QSG_RHI_BACKEND : d3d11 produces unexpected  
results  
* QTBUG-73251 QTreeview stylesheet "show-decoration-selected" has no  
effect  
* QTBUG-102480 Build fails when examples enabled but Sql and/or Linguist  
are disabled  
* QTBUG-83185 [Android]: When using night or dark mode on a device, then  
the style extracted is still set as if it is light mode  
* QTBUG-107780 Rendering Texture in WebAssembly  
* QTBUG-105753 QDir is not re-entrant  
* QTBUG-107604 [Reg 5.15.10 -> 5.15.11] Incorrect fullscreen dimensions  
on some Android devices  
* QTBUG-107709 Android screen size mismatch [Reg 5.15.10 -> 5.15.11]  
* QTBUG-107523 [REG 5.15.10 -> 5.15.11] Android edge-to-edge layout  
broken  
  
### qtdeclarative  
* QTBUG-104629 QML FolderDialog: CurrentFolder is not correctly  
* QTBUG-106256 qml crash when binding alias to property  
* QTBUG-104077 Build failure in 3rdparty/masm/assembler/ARM64Assembler.h  
* QTBUG-93188 tst_qqmlecmascript::gcCrashRegressionTest fails with ARM  
macOS 11 in Qt Declarative  
* QTBUG-98479 QObject that was previously exposed to QML as a const  
pointer remains frozen  
* QTBUG-106391 assertion failure in  
QQuickItemPrivate::localizedTouchEvent  
* QTBUG-104535 REG: Android's Back button does not close QQC2 Dialogs  
anymore  
* QTBUG-106347 Build warns about QML code in C++ header with extension  
".hh"  
* QTBUG-101488 tst_QQuickFileDialogImpl is flaky  
* QTBUG-106392 Alias is invalid when accessed from C++ via  
QObject::property()  
* QTBUG-106042 QtQuick.Controls creates delegates in separate contexts  
* QTBUG-105110 Android: FileDialog not working - unable to select file  
correctly  
* QTBUG-102339 Conan: multiple prefixes not supported when building e.g.  
examples  
* QTBUG-106457 Assert on invalid code  
* QTBUG-106357 crash in QIntrusiveListNode::remove() when pinch-zooming  
in QtPDF on iOS  
* QTBUG-103746 QML javascript URL does not add a colon at the end of  
protocol field  
* QTBUG-106465 ToolTip::test_activateShortcutWhileToolTipVisible is  
flaky  
* QTBUG-105058 PathView steals touch event of PinchArea delegate  
* QTBUG-106491 tst_QQuickMenu fails on webOS  
* QTBUG-106557 QuickControls Texteditor fails to launch on embedded  
devices  
* QTBUG-106553 Quick styled text processes HTML case sensitively (this  
is wrong)  
* QTBUG-106594 Text baseline anchor not updating properly  
* QTBUG-104911 qmllint warns about acceptedDevices in TapHandler  
* QTCREATORBUG-27655 Qt Quick Controls – Chat Tutorial not working  
* QTBUG-106548  [REG 6.2.4 - 6.3.2] HoverHandler "eats" all hover events  
even when disabled  
* QTBUG-106604 Multiple Qt Quick Sliders repaint incorrectly in macOS  
* QTBUG-106566 qmllint crashes on invalid alias property  
* QTBUG-35409 MouseArea does not detect mouse pointer if it was already  
there on Mac OS X  
* QTBUG-46460 MouseArea.containsMouse doesn't revert to false if enabled  
is set to false  
* QTBUG-106611 qml: signals cannot use inline components as argument  
type  
* QTBUG-106114 tst_qmltc_examples fails on webOS  
* QTBUG-106613 qmllint crash due to index out of range  
* QTBUG-106887 CMake does not pass --private-includes to  
qmltyperegistrar if the QML module target is the private library itself  
* QTBUG-106704 HoverHandler and MouseArea: if hover is enabled/disabled  
but mouse does not move AND no item is marked dirty, state doesn't  
change immediately  
* QTBUG-105192 Loader3D crashes when active property is dynamically  
changed  
* QTBUG-105899 ColorDialog: The text fields on ColorInputs.qml are buggy  
for the Fusion, Imagine and Universal styles.  
* QTBUG-107014 [REG 6.2.4 -> 6.2.5] Items covered by Popup receive mouse  
events  
* QTBUG-107077  
tst_qquickdeliveryagent::undoDelegationWhenSubsceneFocusCleared fails  
* QTBUG-106864 Reg-5.15.9->5.15.10: Android crash on startup on armv7  
(32bit) devices  
* QTBUG-106269 Qt Quick apps immediately crash under Android 6  
* QTBUG-106824 Bad casts in qquickshapegenericrenderer.cpp  
* QTBUG-107208 [Reg 5.15 -> 6.x] QQmlApplicationEngine::retranslate()  
doesn't work for ComboBox and ListView  
* QTBUG-106612 qmllint hits assert related to inline components  
* QTBUG-107091 [qmltc] repeater generates invalid code  
* QTBUG-107038 Non-aliased Text is rendered incorrectly using  
NativeRendering  
* QTBUG-107619 V4: Memory corruption due to unchecked length usage  
* QTBUG-107080 qmlcachegen assertion failure  
* QTBUG-107176 cachegen eats all memory and fails  
* QTBUG-107542 qmlcachegen infinite loop with certain statements  
* QTBUG-89933 tst_HoverHandler fails with macOS 10.15 and Xcode 12.3  
* QTBUG-107594 Crash when rendering emojis with NotoEmoji font  
* QTBUG-107013 Wheel scroll event propagated from a modal dialog to the  
dialog below (Quick)  
* QTBUG-104960 DelegateModel is only 1 dimensional  
* QTBUG-106645 "TypeError: Cannot read property of null" error in "QML  
Dynamic View Ordering Tutorial 1" example  
* QTBUG-103939 Text editor example  Font bold/Italic etc. attributes not  
working  
* QTBUG-95225 When the D3D11 RHI backend is used then a white line can  
appear at the border when there is an odd number of pixels in either  
width or height  
* QTBUG-103877 TreeView from Qt 6.3 is not re-sorted when  
dynamicSortFilter is set in the QSortFilterProxyModel  
* QTBUG-104526 text in TextArea disappear when scrolling up large text  
by using scrollbar button "up"  
* QTBUG-99887 TapHandler on TextField (for showing right click context  
menu) stops working in Qt6  
* QTBUG-105609 should be able to add a TapHandler to a Button to modify  
behavior  
* QTBUG-105610 should be able to add a DragHandler to a Button or other  
control  
* QTBUG-103620 [Reg 5.15 -> 6.2] Flicking is inconsistent with touch  
screen  
* QTBUG-99276 Fusion style sets button text color to white automatically  
* QTBUG-107837 HorizontalHeaderView has wrong column sizes  
* QTBUG-103268 QML item Menu doesn't close with touch screen on  
CloseOnPressOutside  
* QTBUG-107867 QQuickSliderPrivate::handleUngrab() is called during  
multi-touch on QQuickSlider  
* QTBUG-107533 [qmltc] live-lock when resolving multi-level alias  
properties  
* QTBUG-107534 [qmltc] cannot resolve alias into component  
* QTBUG-107254 Crash when assigning non existing properties  
* QTBUG-106223 assertion failed after Flickable takes grab from  
PinchHandler  
* QTCREATORBUG-3708 Context sensitive help does not work for several QML  
properties  
* QTBUG-106365 qmlsc doesn't find modules from sysroot  
* QTBUG-106284 tst_QQuickColorDialogImpl::eyeDropper fails with RHEL 9  
* COIN-870 MinGW Windows build exceeds timeout limit  
* QTBUG-30801 Button: tooltip not shown when the button is disabled  
* QTBUG-98130 QtQuick and controls examples use qt_add_resources to add  
QML files  
* QTBUG-107028 tst_qquicktextfield and tst_qquicktextarea fail on  
Android  
* QTBUG-106520 FAIL!  :  
qtquickcontrols::Tests_StackLayout::test_addAndRemoveItems in  
Ubuntu_20_04  
* QTBUG-106521 FAIL!  :  
qtquickcontrols::Tests_StackLayout::test_addAndRemoveItems in MacOS_12  
* QTBUG-104058 tst_qqmlnotifier::deleteFromHandler fails and give  
timeout with macOS 12  
* QTBUG-107591 TreeViewDelegate: selection via onClicked does not work  
* QTBUG-107763 tst_qquickhoverhandler::deviceCursor is flaky  
* QTBUG-106407 Signal connect warnings when opening ColorDialog  
* QTBUG-107703 QML MenuBar : "Alt" does not activate/focus the first  
Menu  
* QTBUG-107168 [Reg 6.2.6 -> 6.4.0] qmlsc: Use of native JS console is  
now treated as an Error  
* QTBUG-107795 Reg-5.15.10->5.15.11 Setting property on TextField  
crashes  
* QTBUG-107684 background of ToolTip template is ignored  
  
### qtactiveqt  
* QTBUG-106014 ActiveQt fails to handle VT_UNKNOWN  
* QTBUG-106024 [QAxServerBase::Invoke] ActiveQt should only call the  
dispatch method if the types match  
  
### qtmultimedia  
* QTBUG-103729 [REG 5.15-6.2] App isn't able to start on Windows 10 N  
* QTBUG-106092 Binding to CaptureSession.imageCapture fails  
* QTBUG-103239 [macOS] Crash in AVFMediaPlayerObserver  
* QTBUG-104943 Multimedia examples not shown in Qt Creator although  
module installed from Installer  
* QTBUG-106204 Multimedia framework requires "record audio"  
authorisation  
* QTBUG-97789 Listening on QVideoSink::videoFrameChanged on Android  
fails to map/unmap QVideoFrame  
* QTBUG-105169 videoFrame.toImage() does not work in a different thread  
than the video rendering thread  
* QTBUG-106881 Camera with multiple streams cannot be detected for the  
second stream  
* QTBUG-107701 [REG 6.4.0->6.4.1] namespace build fails on Windows  
* QTBUG-104226 QmediaDevices::videoInputs() fails to find a camera if  
libcamera is installed.  
* QTBUG-107885 [Recorder Example] Not working mute for AudioInput  
* QTBUG-107205 Video with sound fails to play if sound device is  
unavailable  
* QTBUG-108009 QML Camera maximumZoomFactor in iPad  
* QTBUG-97814 QML MediaPlayer only reports position changes at 10hz  
  
### qttools  
* QTBUG-106552 qttools: Build failure if litehtml is found on the system  
* QTBUG-106706 Non-retina artwork  
* QTBUG-106255 qdoc: \wrapper command is undocumented  
* QTBUG-107107 lupdate -locations absolute creates relatives and not  
absolute paths  
* QTBUG-107845 Can not disable Linguist in Qt 6.4.0 when qttools are  
enabled  
* QTBUG-107762 qdoc: Cannot link to externally-built projects via .index  
files  
  
### qtdoc  
* QTBUG-107245 Typo in the document?  
* QTBUG-103856 Add replacement for some QX11Info alternatives to Qt6  
porting guide  
* QTBUG-103715 QNativeInterface::QX11Application::display() example  
missing  
* QTBUG-106677 "Back" button breaks UI of Coffee Machine Example  
* QTBUG-107121 Hangman example doesn't build for android with build  
tools >= 31.0.0  
  
### qtpositioning  
* QTBUG-107580 [REG 5.15.10 -> 5.15.11], PositionSource: last known  
position is never read  
* QTBUG-103478 QGeoPositionInfoSource on Android always asks for  
location permission  
  
### qtconnectivity  
* QTBUG-106282 tst_QLowEnergyController::tst_emptyCtor fails with RHEL 9  
in QtConnectivity  
* QTBUG-106654 Error Unable to handle unregistered datatype  
'std::shared_ptr<QWinRTBluetoothDeviceDiscoveryWorker>'  
* QTBUG-104473 (Classic) Bluetooth discovery agents to clear previous  
errors  
* QTBUG-107195 Typo in the document  
* QTBUG-107224 Typo in the document?  
* QTBUG-107192 Link is dead in the document  
* QTBUG-107196 Is Advertisement really unavailable on Qt Bluetooth?  
* QTBUG-106614  
tst_QBluetoothDeviceDiscoveryAgent::tst_startStopDeviceDiscoveries fail  
on Android 12  
  
### qtwayland  
* QTBUG-106638 QtWayland tests crash on webOS  
* QTBUG-107076 Copying image data from Qt aplications is still broken on  
GNOME Wayland  
  
### qt3d  
* QTCREATORBUG-27852 Audio visualizer example has blank white screen  
* QTBUG-106865 RHI RenderCapture capture results differ from OpenGL  
renderer  
  
### qtimageformats  
* QTBUG-107040 Tiff images with LZW compression do not work in debug  
builds  
  
### qtserialbus  
* QTBUG-106524 Typo in the document  
  
### qtwebsockets  
* QTBUG-106372 wasm: Using WebSockets from worker threads fail to work  
* QTBUG-106937 Since Qt 6.3 QWebSocket::errorString() displays random  
http status code if status != 400  
  
### qtwebengine  
* QTBUG-104769 pdfviewer example: Pinch zoom on laptop trackpad stops  
working if zoom way in  
* QTBUG-105168 Build of Qt Pdf for iOS fails  
* QTBUG-106355 QtPDF: crash when pinch-zooming on a PDF page with text  
on iOS  
* QTBUG-106358 QtPDF: hard to hide the keyboard on iOS  
* QTBUG-106361 duplicate symbol qLcNav  
* QTBUG-106461 QWebEngineUrlRequestJob::reply() does not support a  
QIODevice that cannot be read completely instantly  
* QTBUG-100391 Application built with Qt 6.2.2 fails to run because of  
missing mf.dll error  
* QTBUG-106095 [REG] 5.15.8 -> 5.15.9 WebEngine crash with software  
OpenGL  
* QTBUG-106588 Accessibility in QWebEngine crashes application  
* QTBUG-106254 Windows offline installer creation fails due to long path  
in QtWebEngine  
* QTBUG-97392 WebEngine fails to load urls from resources  
* QTBUG-106688 Loading html from qrc in QtWebEngine fails  
* QTBUG-106944 [REG 6.4.0rc->final] Can not compile examples on iOS if  
QfPDF is included in installation  
* QTBUG-86972 [REG] QtPDF isn't properly installed as a framework unless  
WebEngine is also installed  
* QTBUG-106967 email privacy: DNS prefetch still leak from local content  
* QTBUG-107144 WebEngine crashes on github.com  
* QTBUG-105953 QtQuick: WebEngineView resize regression  
* QTBUG-106975 Qt webengineview Web page requestfullscreen invalid  
* QTBUG-103958 Unable to remove warning, "Qt WebEngine seems to be  
initialized from a plugin..."  
* QTBUG-107529 QWebEnginePage only uses part of QWebEngineView  
* QTBUG-107502 [Reg 6.3.2 -> 6.4.0] Qt WebEngine --remote-debugging-port  
no longer works  
* QTBUG-108008 FAIL!  :  
tst_QWebEngineView::inputFieldOverridesShortcuts() 'actionTriggered'  
returned FALSE  
* QTBUG-108029 Can't build qtwebengine with MSVC2019  
* QTBUG-106406 gn not build in host build when not building QtWebEngine  
or QtPdf at the same time  
* QTBUG-105342 Test on qemu are very flacky  
  
### qtdatavis3d  
* QTBUG-107505 Wasm build fails when linking both QtMultimedia and  
QtDataVisualization  
  
### qtvirtualkeyboard  
* QTBUG-106894 QtVirtualKeyboard does not popup on static builds  
* QTBUG-106895 QtVirtualKeyboard on mac desktop wrong rotation  
* QTBUG-83217 rotation of virtualkeyboard does not work  
* QTBUG-98750 [VKB] AutoScroller does not work in the basic virtual  
keyboard example  
* QTBUG-105371 [Virtual keyboard] The fallback to layouts/fallback is  
not mentioned  
  
### qtscxml  
* QTBUG-107209 Update documentation on how to integrate state machines  
into QML modules  
* QTBUG-80262 SCXML StateMachine state properties get incorrect values  
if History is used  
  
### qtspeech  
* QTBUG-106286 tst_QTextToSpeech::sayWithVoices fails with RHEL 9 in  
QtSpeech  
  
### qtlottie  
* QTBUG-107501 Lottie produces warnings  
  
### qtquick3d  
* QTBUG-102477 Adding the same effect twice to SceneEnviroment leads to  
a hanging application  
* QTBUG-106544 Antialiasing example doesn't animate when progressive AA  
is enabled  
* QTBUG-107203 Crash when a texture is deleted  
* QDS-7793 propertyGroups.json is not installed  
* QTBUG-104843 QtQuick 3D leaks memory after destroying View3D  
* QDS-8014 Missing properties and types in qtquick3d property sheets  
* QTBUG-105458 Incorrect primitive position when skin property set to  
null  
* QTBUG-96339 Fails to build QtQuick3d on MSYS2/MinGW-w64 due to "The  
command line is too long"  
* QTBUG-98336 WIN10 Qt6 build error in qtquick3d module  
* QTBUG-107734 [REG 6.4.0->6.4.1 and 6.5.0] too long command on MinGW  
shadow build  
* QTBUG-105217 [REG: 6.3.2->6.4.0] Picking of 3D geometry works  
incorrectly (with BBox only)  
* QTBUG-106481 PrincipledMaterial clearcoat shader error with no lights  
* QTBUG-107667 RobotArm example is disfunctional  
* QDS-7662 Drop-down menu for shaders in Properties&Material Editor  
lists irrelevant files from the project  
* QDS-8087 SpecularGlossyMaterial was added in Qt 6.4. It should be  
treated like one of the other basic material types  
  
### qt5compat  
* QTBUG-107468 [Regression] Creating DropShadow is almost 20x slower  
  
### qtmqtt  
* QTBUG-92817 QMqttTopicFilter also matches topics just starting with  
the filter name  
* QTBUG-80440 MqttClient Invalid Property assignment: unsupported type  
"ushort"  
  
### qthttpserver  
* QTBUG-105329 QHttpServer: returning a value from a route handler  
should be an error when the function uses a QHttpServerResponder  
* QTBUG-106378 Qt HTTP Server examples do not show up under module name  
in 'All examples'  
* QTBUG-104348 .gitignore file present in qthttpserver and  
qtquick3dphysics  
  
### qtquick3dphysics  
* QTBUG-104348 .gitignore file present in qthttpserver and  
qtquick3dphysics  
* QTBUG-107007 Configuring Qt with -no-gui fails  
* QTBUG-108045 [FTBFS] iter.physx::PxContactStreamIterator::faceIndice’  
may be used uninitialized  
  
Known Issues  
------------  
  
* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-6/supported-platforms.html  
* RTA reported issues from Qt 6.4  
https://bugreports.qt.io/issues/?filter=24174  
* See Qt 6.4 Known Issues from:  
https://wiki.qt.io/Qt_6.4_Known_Issues  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Amir Masoud Abdol  
Laszlo Agocs  
YAMAMOTO Atsushi  
Mahmoud Badri  
Mate Barany  
Rolf Eike Beer  
Vladimir Belyavsky  
Nicholas Bennett  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
Mikolaj Boc  
Joerg Bornemann  
Assam Boudjelthia  
Michael Brüning  
Andreas Buhr  
Hxcan Cai  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Artem Dyomin  
Alexey Edelev  
Oliver Eftevaag  
Christian Ehrlicher  
Hatem ElKharashy  
Balazs Erseki  
Ilya Fedin  
Alexandros Frantzis  
Christophe Giboudeaux  
Maximilian Goldstein  
Robert Griebl  
Magnus Groß  
Kaj Grönholm  
Richard Moe Gustavsen  
Lucie Gérard  
Tang Haixiang  
Heikki Halmet  
Thomas Hartmann  
Jani Heikkinen  
Miikka Heikkinen  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Dominik Holland  
Allan Sandfeld Jensen  
Janne Juntunen  
Maurice Kalinowski  
Jonas Karlsson  
Johannes Kauffmann  
Timothée Keller  
Ali Kianian  
Friedemann Kleint  
Michal Klocek  
Lars Knoll  
Seokha Ko  
Jarek Kobus  
Kai Koehne  
Sze Howe Koh  
Jarkko Koivikko  
Tomi Korpipaa  
Fabian Kosmale  
Volker Krause  
Konrad Kujawa  
Santhosh Kumar  
Sona Kurazyan  
Kai Köhne  
Inho Lee  
Eric Lemanissier  
Moody Liu  
Jenny Lofthus  
Thiago Macieira  
Sérgio Martins  
Thorbjørn Lund Martsum  
Ievgenii Meshcheriakov  
Samuel Mira  
Bartlomiej Moskal  
Marc Mutz  
Tommi Mänttäri  
Antti Määttä  
Martin Negyokru  
Andy Nichols  
Mårten Nordheim  
Bumjoon Park  
Samuli Piippo  
Timur Pocheptsov  
Rami Potinkara  
Lorn Potter  
Liang Qi  
Topi Reinio  
Aleksandr Reviakin  
Rob De Reycke  
André de la Rocha  
Alexey Rochev  
Shawn Rutledge  
Toni Saario  
Björn Schäpers  
Luca Di Sera  
Dmitry Shachnev  
Sami Shalayel  
Venugopal Shivashankar  
David Skoland  
Johan Solbakken  
Ivan Solovev  
Axel Spoerl  
Piotr Srebrny  
Patrick Stewart  
Martin Storsjö  
Christian Strømme  
Tarja Sundqvist  
Jan Arve Sæther  
Morten Sørvig  
Duan Ting  
Jere Tuliniemi  
Paul Olav Tvete  
Leticia Valladares  
Sami Varanka  
Peter Varga  
Doris Verria  
Tor Arne Vestbø  
Ville Voutilainen  
Juha Vuolle  
Jaishree Vyas  
Michael Weghorn  
Edward Welbourne  
Fushan Wen  
Paul Wicking  
Oliver Wolff  
Semih Yavuz  
Yuhang Zhao  
