Release note  
============  
Qt 6.2.7 release is a patch release made on the top of Qt 6.2.6. As a patch  
release, Qt 6.2.7 does not add any new functionality but provides bug fixes  
and other improvements.  
  
For detailed information about Qt, see the Qt 6.2 online documentation:  
https://doc.qt.io/qt-6.2/.  
  
Important Changes  
-----------------  
  
### qtbase  
* e4659c13de Document QAtomic testAndSet  
Documented new overloads of testAndSet() that were originally added for  
5.3.  
  
* 5036c971e8 QTaggedPointer: disable operator= with an empty initializer  
list  
The operator assignment taking a raw pointer has been reimplemented in  
order to avoid subtle issues when assigning `{}` to a QTaggedPointer.  
This will cause code that assigns a braced-init-list to a QTaggedPointer  
object to stop compiling (for instance, `tagPtr = {ptr}` is now ill-  
formed).  
  
* 06cc44b7b7 Update bundled libpng to version 1.6.38  
libpng was updated to version 1.6.38  
  
* 5f6bc72cd5 Fix generating PDFs with DirectWrite engine  
Fixed glitches in generated PDFs when the DirectWrite backend was in  
use, e.g. when high-dpi scaling was active.  
  
* afdb88a263 Ensure proper format of Info.plist  
Fixed handling binary Info.plist files in generated Makefiles by always  
converting them to XML before substituting placeholders.  
  
* 03b7d80071 Update bundled zlib to version 1.2.13  
zlib was updated to version 1.2.13.  
  
* d7b3574088 macOS: Fix less common writing systems on Catalina and  
later  
Fixed missing text with certain writing systems on macOS Catalina and  
later.  
  
### qtdeclarative  
* 8435926668 DA: ignore disabled HoverHandlers when delivering hover  
events  
Disabled hover handlers will no longer receive hover events, or block  
siblings from being hovered.  
  
### qttools  
* 854684e99 qdoc: Enable correct linking to externally-built  
dependencies  
  
  
### qtwebengine  
* in Qt 6.2.7, Qt WebEngine from Qt 6.4.1 is used  
  
* c3ae834aa Add charset parsing to custom scheme handler's content type  
Charset is now explicitly parsed from provided contentType  
  
* 82357352b Introduce "--webEngineArgs" to prevent unexpected sub-  
process args  
Command line arguments meant for webengine has to be now stated after "  
--webEngineArgs" option.  
  
* 4c4ac0df9 Introduce http status code domain for loading info  
Added HttpStatusCodeDomain for http status code range of errors  
  
* 196ec015c Add NavigateOnDrop settings  
NavigateOnDropEnabled added, enabled by default.  
  
* 05d82c353 QPdfView: replace enums with enum classes  
All enums are replaced with enum classes.  
  
* 6769bd154 Move QPdf namespace enums into QPdfDocumentRenderOptions  
enum classes  
The QPdf namespace is removed.  
  
* 90f43fd25 Rename QPdfNavigationStack to QPdfPageNavigator; QML type  
too  
The PdfNavigationStack QML type has been renamed to PdfPageNavigator,  
matching the C++ type QPdfPageNavigator. These remember navigation  
history within a document, and are helpful to implement back/forward  
buttons similar to those on a web browser in both Qt Quick and widget-  
based viewer applications.  
  
* 0de16e9a2 Redefine PdfSearchModel.currentResult as document-based; use  
PdfLink  
PdfSearchModel.currentResult is now the result index within the whole  
set of search results rather than on currentPage; and changing  
currentPage no longer makes currentResult change. In the views, this  
means the current highlighted search result stays on the same page even  
when the user views a different page.  
  
* fd39e1eee Add link role to QPdfLinkModel, providing a QPdfLink  
instance  
PdfLinkModel now provides a QPdfLink object for each link. QPdfLink now  
contains everything necessary to render delegates for links and search  
results, and handle clicking links; and there is a copyToClipboard()  
method for use in context menus, which will copy the text returned trom  
toString(), which is also invokable.  
  
* 66aca3c84 Add PdfLinkDelegate instead of link decoration style  
properties  
A PdfLinkDelegate will now be instantiated on top of each hyperlink in  
the PdfMultiPageView, PdfScrollablePageView and PdfPageView components,  
for event handling and to provide tapped() and contextMenuRequested()  
signals. It is non-visual by default, but can be customized, for example  
to draw underlines under hyperlinks if the PDF documents are not  
expected to have them already.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-42661 Wrong dialog activation  
* QTBUG-105140 [REG] default constuctor requirement for meta type  
(QVariant) breaks webengine api  
* QTBUG-105618 QNetworkReplyFileImpl synchronously emits  
QNetworkReply::finished() from constructor in case of error  
* QTBUG-89557 QML Text's implicitWidth is wrong when wrapMode is set for  
multiline text.  
* QTBUG-104986 QTextLayout::maximumWidth() is not correct for multi-line  
text  
* QTBUG-106531 QDockWidget Docking resizes (widens) the widget by a set  
number of pixels  
* QTBUG-105182 Access violation / infinite loop in  
QFutureInterfaceBase::isChainCanceled()  
* QTBUG-106083 QFuture::then(QObject *context, Function &&function)  
throws "read access violation" when used in chained QFuture  
* QTBUG-106387 Application crash when writing in textfield  
* QTBUG-106899 tst_qquicktext::dependentImplicitSizes() Compared doubles  
are not the same  
* QTBUG-106530 QDockWidget Undocking incorrectly offset from cursor  
(native titlebar) when dragging  
* QTBUG-101339 Hardware keyboard up/down keystrokes interpreted as  
home/end when interacting with a QML TextArea  
* QTBUG-104962 [REG 6.3.0 -> 6.3.1]QFileDialog does not allow changing  
column sizes nor sorting  
* QTBUG-104425 Crash when loading header state in QBittorent  
* QTBUG-106920 MOC cannot parse nested inline namespace (Parse error at  
"::")  
* QTBUG-92199 [REG] The color of QLineEdit and QPlainTextEdit  
placeholder text is not grayed-out if stylesheet was applied  
* QTBUG-93009 QPalette::PlaceholderText color is not followed after  
setting color in a style sheet  
* QTBUG-106607 QODBC: QSqlQuery::isNull returns false for SELECT NULL  
* QTBUG-106219 [macOS] Typing accented/alternate characters doesn't work  
correctly  
* QTBUG-100891  
tst_QGuiApplication::genericPluginsAndWindowSystemEvents() fails on  
Wayland  
* QTBUG-100918 tst_QOpenGL::bufferMapRange() fails on Wayland  
* QTBUG-69608 cocoa: key press events for modifier keys do not have  
nativeVirtualKey  
* QTBUG-107038 Non-aliased Text is rendered incorrectly using  
NativeRendering  
* QTBUG-107246 QVariant.toList method not working properly  
* QTBUG-97697 Missing documentation for GrabTransition enum in  
DragHandler  
* QTBUG-107188 Reg: Behavior Change: Modal dialogs seem to block events  
to other dialogs/widget  
* QTBUG-107155 tst_QWidget_window::resetFocusObjectOnDestruction() with  
QtWayland failed on Ubuntu 22.04, GNOME  
* QTBUG-100245 tst_qsqlquery should not create unique data tags when  
testing  
* QTBUG-107719 Typo in the document?  
* QTBUG-107450 Reg[5->6]QSlider handle size is not correct  
* QTBUG-101000 macOS: QPushbutton text color changes  
* QTBUG-79977 QMessageBox does not work at  IOS 13  
* QTBUG-102098 QPrinter::PdfFormat causes some fonts to be doubly-scaled  
when using DirectWrite font engine  
* QTBUG-107249 [REG 6.4.0->6.5.0] Can not compile Qt examples with  
Android armv7 pre-build binaries on linux and macOS  
* QTBUG-47979 QDesktopServices is unable to open a file on Android  
* QTBUG-85773 QML TextEdit copy() copies text twice on Android  
* QTBUG-107627 AndroidAssetsFileEngineHandler is broken  
* QTBUG-106227 Alternate row background color does not starts from  
beginning  
* QTBUG-106542 qCompress()/qUncompress() cannot handle more than 4GiB of  
data on Win64  
* QTBUG-107720 "This feature is not supported on the Windows platform."  
is a bit vague  
* QTBUG-106713 android.bundle.enableUncompressedNativeLibs=false  
deprecated in Android Gradle plug-in ver 8.0  
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
* QTBUG-106984 Setting background brush in QTableWidgetItem used as  
header item is incorrectly cached leading to incorrect display colours  
* QTBUG-98354 Windows 11: State of checkable QAction with icon is not  
shown  
* QTBUG-106108 REG/macOS:  context menu corners are not rounded  
* QTBUG-107991 QString asprintf behaves differently than printf with  
"%03.f" format for example  
* QTBUG-105857 Qt application does not follow the DPI change when the  
DPI setting is changed before showing the first window  
* QTBUG-107879 FAIL!  : tst_AndroidAssets::loadsFromAssetsPath  
* QTBUG-108103 QHostAddress::isEqual() with IPv6 determines valid ip to  
be any  
* QTBUG-91882 eglfs with a cloned screen cause app to flicker  
* QTBUG-46681 [REG 4.x->5.x] QPainter in paintEvent() doesn't work with  
Qt::WA_PaintOnScreen  
* QTBUG-100085 xcb: Native window does not get paint event if another  
window on top of it is hidden unless there is a enter/leave event  
somewhere  
* QTBUG-108186 Crash in qt_memrotate90 or qt_memrotate270  
* QTBUG-89156 [REG 5.15.0->5.15.1] Focus is limitted after reparenting  
and adding widgets  
* QTBUG-67579 QT5 apps running natively under Wayland do not respect  
cursor size setting  
* QTBUG-87778 wayland: cursor size wrong  
* QTBUG-108047 Setting macos style before creating a QApplication  
crashes  
* QTBUG-108196 SecKeychain is deprecated [-Wdeprecated-declarations]  
when compiling qnetworkaccessmanager.cpp  
* QTBUG-107572 Expose QLineEdit focus for QComboBox editable  
* QTBUG-68175 tst_QWidget::raise is flaky  
* QTBUG-45357 Let qmake check whether Info.plist is in XML format  
* QTBUG-96384 Tagalog cannot be displayed correctly  
* QTBUG-98920 Font fallback is not working properly on macOS  
* QTBUG-108605 Unhandled WinRT exception at  
QSystemLocalePrivate::uiLanguages()  
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
* QTBUG-106939 Error: "qmlimportscanner not found" while building  
examples while using cmake  
* QTBUG-107157 tst_QWidget with QtWayland failed on Ubuntu 22.04, GNOME  
* QTBUG-107184 tst_QGridLayout::setMinAndMaxSize() with QtWayland  
crashed on Ubuntu 22.04, GNOME  
* QTBUG-107154 tst_QWidget_window::mouseMoveWithPopup(Dialog) with  
QtWayland failed on Ubuntu 22.04 GNOME  
* QTBUG-107578 tst_selftests failed with qtwayland qpa plugin on Ubuntu  
22.04 GNOME  
* QTBUG-107158  
tst_QTouchEvent::multiPointRawEventTranslationOnTouchPad() with  
QtWayland failed on Ubuntu 22.04, GNOME  
* QTBUG-73251 QTreeview stylesheet "show-decoration-selected" has no  
effect  
* QTBUG-106896 QDir::drive() does not shows DVD drive  
* QTBUG-102480 Build fails when examples enabled but Sql and/or Linguist  
are disabled  
* QTBUG-87137 tst_QApplication::sendEventsOnProcessEvents() failed on  
Ubuntu 20.04/22.04 and RHEL 9  
* QTBUG-107604 [Reg 5.15.10 -> 5.15.11] Incorrect fullscreen dimensions  
on some Android devices  
* QTBUG-107709 Android screen size mismatch [Reg 5.15.10 -> 5.15.11]  
* QTBUG-107523 [REG 5.15.10 -> 5.15.11] Android edge-to-edge layout  
broken  
* QTBUG-92468 QTextEdit cursor is drawn incorrectly  
* QTBUG-86823 REG: Blinking cursor leaving an artifact in QTextEdit  
* QTBUG-96288 QTextEdit cursor postion error when QTextEdit has  
different pointsize  
* QTBUG-83185 [Android]: When using night or dark mode on a device, then  
the style extracted is still set as if it is light mode  
* QTBUG-107727 QSystemTrayIcon does not emit the  
QSystemTrayIcon::activated signal on Ubuntu 20.04/22.04 for left click  
and right click.  
* QTBUG-91255 [Android] Add support for APK Signature Scheme v2  
* QTBUG-107923 Wrong height of the window on Android  
  
### qtdeclarative  
* QTBUG-106457 Assert on invalid code  
* QTBUG-106465 ToolTip::test_activateShortcutWhileToolTipVisible is  
flaky  
* QTBUG-106557 QuickControls Texteditor fails to launch on embedded  
devices  
* QTBUG-105058 PathView steals touch event of PinchArea delegate  
* QTBUG-104537 [REG 6.2.4-6.3.1] HoverHandler do not propagate hover to  
TextEdit  
* QTCREATORBUG-27655 Qt Quick Controls – Chat Tutorial not working  
* QTBUG-106548  [REG 6.2.4 - 6.3.2] HoverHandler "eats" all hover events  
even when disabled  
* QTBUG-106604 Multiple Qt Quick Sliders repaint incorrectly in macOS  
* QTBUG-106594 Text baseline anchor not updating properly  
* QTBUG-106887 CMake does not pass --private-includes to  
qmltyperegistrar if the QML module target is the private library itself  
* QTBUG-106256 qml crash when binding alias to property  
* QTBUG-105899 ColorDialog: The text fields on ColorInputs.qml are buggy  
for the Fusion, Imagine and Universal styles.  
* QTBUG-106611 qml: signals cannot use inline components as argument  
type  
* QTBUG-107014 [REG 6.2.4 -> 6.2.5] Items covered by Popup receive mouse  
events  
* QTBUG-106824 Bad casts in qquickshapegenericrenderer.cpp  
* QTBUG-105192 Loader3D crashes when active property is dynamically  
changed  
* QTBUG-106864 Reg-5.15.9->5.15.10: Android crash on startup on armv7  
(32bit) devices  
* QTBUG-106269 Qt Quick apps immediately crash under Android 6  
* QTBUG-107038 Non-aliased Text is rendered incorrectly using  
NativeRendering  
* QTBUG-107208 [Reg 5.15 -> 6.x] QQmlApplicationEngine::retranslate()  
doesn't work for ComboBox and ListView  
* QTBUG-106800 Component property with any non-literal expression causes  
assertion failure when it's inside inline component and qmlcachegen is  
not being used  
* QTBUG-106645 "TypeError: Cannot read property of null" error in "QML  
Dynamic View Ordering Tutorial 1" example  
* QTBUG-107013 Wheel scroll event propagated from a modal dialog to the  
dialog below (Quick)  
* QTBUG-103939 Text editor example  Font bold/Italic etc. attributes not  
working  
* QTBUG-107837 HorizontalHeaderView has wrong column sizes  
* QTBUG-103620 [Reg 5.15 -> 6.2] Flicking is inconsistent with touch  
screen  
* QTBUG-107867 QQuickSliderPrivate::handleUngrab() is called during  
multi-touch on QQuickSlider  
* QTBUG-101034 Application not detecting submenu shortcuts  
* QTBUG-107254 Crash when assigning non existing properties  
* QTBUG-108026 Memory leak when capturing a 3D scene using  
QQuickItem::grabImage  
* QTBUG-106106 Crash in ~QQuickScrollBarAttached during rearrange of  
QQmlDelegateModel  
* QTBUG-71922 Mime data is corrupted when using QQuickDragAttached and  
it's not UTF-8  
* QTBUG-74496 Performance issue: rejected drag re-triggers drag enter  
event every frame while mouse moves  
* QTBUG-107818 Sometimes ShaderEffect types are not be drawn correctly  
on 2 QQuickWindows  
* QTBUG-108252 Crash occurs when GUI thread accesses QRhi objects  
created by Renderer Thread  
* QTBUG-107774 madvise() terminates application due to EBADF code  
* QTBUG-106602 extending-qml example is missing QtQuick dependency in  
CMakeLists.txt  
* QTBUG-106884 Typo in the document  
* QTBUG-108352 tst_touchmouse::strayTouchDoesntAutograb is flaky  
* QTBUG-108298 Crash using ConicalGradient in a ShapePath  
* QTBUG-106875 Segfault when Loader is trying to load a file that  
contains the Loader  
* QTBUG-107480 Typo in the document  
* QTBUG-104629 QML FolderDialog: CurrentFolder is not correctly  
* QTBUG-104573 DialogButtonBox enums are not known to qmllint  
* QTBUG-107472 testhttpserver_p.h:18:10: fatal error: QTcpServer: No  
such file or directory  
* QTBUG-108549 PinchHandler.scale loses the accumulated scaling if  
target == null  
* QTBUG-92064 PinchHandler target scale jumps when pinching a second  
time via native gesture  
* QTBUG-108647 Build error when trying to compile app with "-" in name  
* QTBUG-101072 Choosing a project name with a dash inside creates a  
broken cmake configuration  
* QTBUG-108627 Assertion in QQmlPropertyData::setOverrideIndex  
* QTBUG-108388 code snippet in the document is incomplete  
* QTBUG-107607 Crash when trying to inspect "this.parent"  
* QTBUG-83630 Qt Quick Control 2 Tooltip can be way too big when you  
have newlines  
* QTBUG-94764 REG: Attached ToolTips shrink  
* QTBUG-101704 Imagine style ToolTip calculates its width incorrectly  
* QTBUG-91545 [iOS] Selection in TextEdit not working for Readonly text  
* QTBUG-75556 Selection in TextEdit not working for Readonly text  
* QTBUG-105530 Can't paste into empty text field on Android  
* QTBUG-107795 Reg-5.15.10->5.15.11 Setting property on TextField  
crashes  
* QTBUG-107684 background of ToolTip template is ignored  
* QTBUG-107619 V4: Memory corruption due to unchecked length usage  
* QTBUG-106520 FAIL!  :  
qtquickcontrols::Tests_StackLayout::test_addAndRemoveItems in  
Ubuntu_20_04  
* QTBUG-106521 FAIL!  :  
qtquickcontrols::Tests_StackLayout::test_addAndRemoveItems in MacOS_12  
* QTBUG-101488 tst_QQuickFileDialogImpl is flaky  
  
### qtmultimedia  
* QTBUG-103239 [macOS] Crash in AVFMediaPlayerObserver  
* QTBUG-106881 Camera with multiple streams cannot be detected for the  
second stream  
* QTBUG-104226 QmediaDevices::videoInputs() fails to find a camera if  
libcamera is installed.  
* QTBUG-107885 [Recorder Example] Not working mute for AudioInput  
* QTBUG-107205 Video with sound fails to play if sound device is  
unavailable  
* QTBUG-95127 QMediaPlayer::setVideoOutput() no longer takes QList of  
outputs  
* QTBUG-103567 QML MediaPlayer fails to playback rtsp media properly.  
* QTBUG-108018 Camera Example crashes on macOS 13 ventura  
  
### qttools  
* QTBUG-106706 Non-retina artwork  
* QTBUG-107845 Can not disable Linguist in Qt 6.4.0 when qttools are  
enabled  
* QTBUG-107762 qdoc: Cannot link to externally-built projects via .index  
files  
* QTBUG-96239 Document CMake component in CMake function documentation  
  
### qtdoc  
* QTBUG-107245 Typo in the document?  
* QTBUG-103856 Add replacement for some QX11Info alternatives to Qt6  
porting guide  
* QTBUG-103715 QNativeInterface::QX11Application::display() example  
missing  
* QTBUG-107121 Hangman example doesn't build for android with build  
tools >= 31.0.0  
* QTBUG-108335 calqlatr demo buttons are broken  
  
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
* QTBUG-106874 Windows bluetooth LE discovery abort when bluetooth is  
OFF  
* QTBUG-107195 Typo in the document  
* QTBUG-106614  
tst_QBluetoothDeviceDiscoveryAgent::tst_startStopDeviceDiscoveries fail  
on Android 12  
  
### qtwayland  
* QTBUG-104259 tst_seatv4 tests are failing with Ubuntu 22.04 Wayland  
* QTBUG-103378 Some return values are ignored, causing warnings  
* QTBUG-107076 Copying image data from Qt aplications is still broken on  
GNOME Wayland  
  
### qt3d  
* QTCREATORBUG-27852 Audio visualizer example has blank white screen  
* QTBUG-56368 Crash when using async NodeInstantiator within Scene3D  
  
### qtimageformats  
* QTBUG-107040 Tiff images with LZW compression do not work in debug  
builds  
* QTBUG-107223 Massive memory consumption when loading TIFF image  
  
### qtserialbus  
* QTBUG-107132 Typo in the document?  
  
### qtwebengine  
* QTBUG-99282  
3rdparty/chromium/content/public/common/content_switches.h:13:10: fatal  
error: 'media/media_buildflags.h' file not found  
* QTBUG-95568 Possible deadlock at QtWebEngine Startup  
* QTBUG-99511 Top level cross build fails  
* QTBUG-99526 developer tools no longer highlights page elements when  
inspecting them  
* QTBUG-99485 Qt WebEngine AutomationId issue  
* QTBUG-99263 QProcess::finished not emitted  
* QTBUG-99215 Html popups do not work correctly.  
* QTBUG-99669 Glib network plugins doesn't configure or build  
* QTBUG-99890 QtWebEngine ozone platform needs pkgconfig check for  
xkbfile include  
* QTBUG-86972 [REG] QtPDF isn't properly installed as a framework unless  
WebEngine is also installed  
* QTBUG-100023 Cannot use Qt6::Pdf Module (Not Found)  
* QTBUG-94924 Load signals not emitted when opening a google result  
* QTBUG-100032 tst_qquickwebview: malloc_consolidate(): invalid chunk  
size  
* QTBUG-100285 Windows: Qt Designer crash when selecting QWebEngineView  
* QTBUG-100293 spellcheck error: session_bridge_ was not declared  
* QTBUG-100291 abort early on missing dependency: gssapi.h for kerberos  
* QTBUG-96597 Crash on WebEngine(View|Profile).userScripts.collection  
property get  
* QTBUG-100500 System libxslt is not used  
* QTBUG-68820 simplebrowser crashes when passing command line argument  
"-type=1"  
* QTBUG-101084 Test  #1: tst_qwebenginecookiestore  
.................***Failed  
* QTBUG-100996 WebEngine crashes in Accessibility  
* QTBUG-96574 Qt Quick API cannot render password protected PDF files  
* QTBUG-100672 Universal builds of WebEngine fail on M1 mac  
* QTBUG-101290 Unable to build examples when building as module with  
-DQT_BUILD_EXAMPLES=ON  
* QTBUG-96525 QWebEngineScript::setSourceUrl doesn't load scripts from  
qrc  
* QTBUG-94368 [QtPDF] bitcode bundle could not be generated because  
libQt5Pdf.a was built without full bitcode  
* QTBUG-94046 QtPDF: configuration with -static-runtime causes linker  
errors for projects  
* QTBUG-86948 When using QImageReader to load a PDF then the PDF images  
can be blurry and seem to be at half the size they should be  
* QTBUG-101706 [REG] ASSERT: "event->reason() != Qt::PopupFocusReason"  
in file \Users\qt\work\qt\qtwebengine\src\webenginewidgets\render_widget  
_host_view_qt_delegate_widget.cpp, line 79  
* QTBUG-101724 Application crash when trigger  
QWebEnginePage::triggerAction( QWebEnginePage::InspectElement )  
* QTBUG-101935 FAIL!  : tst_QWebEnginePage::pasteImage() Compared values  
are not the same  
* QTBUG-100839 qmllint guesses wrong about scope in so-called  
unqualified access  
* QTBUG-94963 QWebEngineLoadingInfo::errorDomain() returns  
WebEngineError::InternalErrorDomain when there is no error  
* QTBUG-100806 QMimeData::html() returns undesirable meta data  
* QTBUG-92539 Weird behavior when pasting certain HTML into element with  
contentEditable attribute set  
* QTBUG-101201 Failed to compile xkb_symbols with multiple layout  
* QTBUG-102303 QtPdf views: get Controls styling working better  
* QTBUG-102746 PdfMultiPageView: starts out with pages centered  
horizontally, switches to left-aligned after using the search results  
sidebar  
* QTBUG-102742 QtPDF MultiPageView: fix horizontal scrolling  
* QTBUG-102743 Version getters are undocumented  
* QTBUG-100799 Dictionaries not found in spellchecker bundle dir on  
macOS  
* QTBUG-100300 cups-config: No such file - build error in  
cups_config_helper.py  
* QTBUG-103217 QtWebEngineQuick form select field popups do not react on  
touch press  
* QTBUG-79254 QWebEngineView couldn't handle touch events for html  
select's popup menus  
* QTBUG-103372 [REG 6.2 -> 6.3] QT_QUICK_BACKEND=software segfaults with  
QtWebEngine in QSGSoftwareRenderableNode::update  
* QTBUG-101030 The zoom factor is reset every time QtWebEngine loads a  
new website  
* QTBUG-103778 [REG 5.15 -> 6.2] ERR_NETWORK_ACCESS_DENIED when clicking  
link from local page  
* QTBUG-102740 PdfMultiPageView: following search results scrolls around  
more than necessary  
* QTBUG-102394 Pdf rendering very slow using Qt Pdf module  
* QTBUG-102951 Qt PDF cannot coexist with TIFF Qt Image Formats plugin  
in statically-linked app  
* QTBUG-96377 Using QWebEngineView::setPage() on page already active  
* QTBUG-103735 QWebEnginePage::iconChanged() not emitted  
* QTBUG-103578 WebEngine: Error when linking gn  
* QTBUG-103579 Qt PDF: Static build fails on macOS  
* QTBUG-92932 [REG 5.12 -> 5.13] QWebEngineUrlRequestInterceptor doesn't  
get called for websocket connections  
* QTBUG-101769 Qt WebEngine reports wrong UIAutomation bounding rects  
with high DPI  
* QTBUG-54433 Support of datalist  
* QTBUG-105134 WebEngineView is crashing while loading the pdf file  
* QTBUG-105082 QtWebEngine freezes on specific Chromium debug command  
* QTBUG-86871 Qt WebEngine incompatible with Selenium's "sendKeys"  
method  
* QTBUG-103760 Conan: Qt WebEngine resources not found  
* QTBUG-104436 V8 error when using WebEngine with --single-process and  
proxy auto-config  
* QTBUG-105072 [REG 6.4] Initial widget focus is wrong  
* QTBUG-106090 moc_qquickwebenginesingleton_p.cpp:38:69: error: use of  
undeclared identifier 'QtMocHelpers'; did you mean  
'::TestNamespace::TestNamespace::QtMocHelpers'?  
* QTBUG-106210 Dependency update on qt/qtwebengine failed in dev  
* QTBUG-105955 [REGRESSION] Web Engine views are painted only partially  
* QTBUG-105960 QtQuick: WebEngineView scaling regression (Windows)  
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
* QTBUG-108843 [WebRTC] Crash inside  
RTCStatsCollector::ProduceAudioRTPStreamStats_n  
* QTBUG-99119 [REG 5 -> 6] Segfault in  
QtWebEngineCore::WebContentsDelegateQt::webEngineSettings() on Google  
Meet  
* QTBUG-98941 [Qt5.15.4][QWebEngine]QWebEnginePage::print() function  
printing a grey paper while printing a PDF in Qt5.15.4  
* QTBUG-50686 QWebSettings::LocalContentCanAccessRemoteUrls not working  
with audio tags  
* QTBUG-82873 import QtQml in dependencies doesn't work on static builds  
if omitted from the main qml  
* QTBUG-101215 QML certifciate errror test is broken, but works on c++  
side  
* QTBUG-87154 Add static dependencies from 3rdparty in qtbase  
* QTBUG-100404 Changes around WebEngineScript are not documented  
* QTBUG-100713 Qt WebEngine: --disable-gpu does not disable GPU  
* QTBUG-100435 Cannot enable webrtc-pipewire feature  
* QTBUG-102253 tst_qwebengineview (Failed)  
* QTBUG-102156 QtPdf: stop using private API  
* QTBUG-102323 cmake seems to treat builddir as a regex and fails if  
builddir contains quantor characters (+)  
* QTBUG-102192 Navigation on drop broken  
* QTBUG-100073 Conan: leaf module options are missing -no-feature  
possibility  
* QTBUG-103859 qt-testrunner.py ERROR: exception:ParseError no element  
found  
* QTBUG-103354 Test #12: tst_uidelegates  
...........................***Failed  
* QTBUG-101744 tst_uidelegates most tests fail on macOS  
* QTBUG-104057 Dependency update fails: error: no matching member  
function for call to 'addAction'  
* QTBUG-99445 quicknanobrowser crashes with --single-process  
* QTBUG-99207 [REG: 5.14.2->5.15.0] Redirection from file to custom url  
schemes does not work  
* QTBUG-104238 [REG 5.15 -> 6.3] Widevine fails on specific sites  
* QTBUG-102099 QWebEngineView ColorPicker  is not modal and freezes  
application  
* QTBUG-102633 [Windows] Linking errors in Blink  
* QTBUG-103221 QtPDF examples are not installed with 6.3.0 or 6.4.0  
* QTBUG-105342 Test on qemu are very flacky  
* QTBUG-105818 gio is not detected correctly  
* QTBUG-106072 QtPdf can't open password-protected PDF files on  
Windows/Android  
* QTBUG-106406 gn not build in host build when not building QtWebEngine  
or QtPdf at the same time  
  
### qtvirtualkeyboard  
* QTBUG-106894 QtVirtualKeyboard does not popup on static builds  
* QTBUG-98750 [VKB] AutoScroller does not work in the basic virtual  
keyboard example  
* QTBUG-83217 rotation of virtualkeyboard does not work  
* QTBUG-105371 [Virtual keyboard] The fallback to layouts/fallback is  
not mentioned  
* QTBUG-108030 Virtual keyboard basic example freezes on Android  
* QTBUG-106895 QtVirtualKeyboard on mac desktop wrong rotation  
  
### qtscxml  
* QTBUG-107209 Update documentation on how to integrate state machines  
into QML modules  
* QTBUG-80262 SCXML StateMachine state properties get incorrect values  
if History is used  
* QTBUG-101777 qscxmlc installed to $prefix/bin location instead of  
$prefix/libexec  
  
### qtquick3d  
* QTBUG-96302 3D scenes with 2D subtrees leak graphics resources upon  
destroying the scene  
* QTBUG-106032 If you start an application with View3D not visible from  
one state, it's impossible to get it visible then.  
* QTBUG-108811 Skinned mesh doesn't follow skeleton  
* QTBUG-107841 tst_Input crashes a lot  
  
### qtmqtt  
* QTBUG-92817 QMqttTopicFilter also matches topics just starting with  
the filter name  
  
### qtinterfaceframework (Commercial only)  
* QTBUG-107661 qt6_ifcodegen_generate pollutes system environment  
variables  
  
Known Issues  
------------  
  
Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-6.2/supported-platforms.html  
  
The RTA (release test automation) reported issues in Qt 6.2.x:  
https://bugreports.qt.io/issues/?filter=23315  
  
Qt 6.2.7 Open issues in Jira:  
https://bugreports.qt.io/issues/?filter=24566  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Laszlo Agocs  
Dimitrios Apostolou  
Rolf Eike Beer  
Vladimir Belyavsky  
Nicholas Bennett  
Maximilian Blochberger  
Eskil Abrahamsen Blomfeldt  
Joerg Bornemann  
Assam Boudjelthia  
Michael Brüning  
Marco Bubke  
Kirill Burtsev  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Szabolcs David  
Artem Dyomin  
Alexey Edelev  
Balazs Egedi  
Christian Ehrlicher  
Iikka Eklund  
Hatem ElKharashy  
Andreas Eliasson  
Nicolas Fella  
Andrei Golubev  
Robert Griebl  
Jan Grulich  
Richard Moe Gustavsen  
Lucie Gérard  
Tang Haixiang  
Heikki Halmet  
Jani Heikkinen  
Ulf Hermann  
Volker Hilsheimer  
Dominik Holland  
Allan Sandfeld Jensen  
Janne Juntunen  
Maurice Kalinowski  
Johannes Kauffmann  
Timothée Keller  
Friedemann Kleint  
Michal Klocek  
Seokha Ko  
Sze Howe Koh  
Jarkko Koivikko  
Tomi Korpipaa  
Janne Koskinen  
Fabian Kosmale  
Konrad Kujawa  
Santhosh Kumar  
Sona Kurazyan  
Kai Köhne  
Inho Lee  
Eric Lemanissier  
Paul Lemire  
Thiago Macieira  
Ievgenii Meshcheriakov  
Samuel Mira  
Bartlomiej Moskal  
Marc Mutz  
Martin Negyokru  
Mårten Nordheim  
Dennis Oberst  
Bumjoon Park  
Samuli Piippo  
Timur Pocheptsov  
Rami Potinkara  
Liang Qi  
Topi Reinio  
André de la Rocha  
Alexey Rochev  
Shawn Rutledge  
Toni Saario  
Sami Shalayel  
Ye ShanShan  
Venugopal Shivashankar  
Ivan Solovev  
Axel Spoerl  
Piotr Srebrny  
Martin Storsjö  
Christian Strømme  
Tarja Sundqvist  
Jan Arve Sæther  
Morten Sørvig  
Benjamin Terrier  
Duan Ting  
Jere Tuliniemi  
Sami Varanka  
Peter Varga  
Doris Verria  
Tor Arne Vestbø  
Ville Voutilainen  
Juha Vuolle  
Jaishree Vyas  
Edward Welbourne  
Fushan Wen  
Paul Wicking  
Anna Wojciechowska  
Semih Yavuz  
