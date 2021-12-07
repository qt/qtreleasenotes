Release note  
============  
> PLACEHOLDER FOR RELEASE NOTE HEADER  
  
Important Changes  
-----------------  
  
### qtbase  
* 0c4d476e8a Fix text issues when using typographic names  
Fixes an issue where fonts would sometimes not fail to work when  
selected using typographic names.  
  
* c9635b99df Fix java mkspec for compatibility with JDK 12  
  
  
* a69195c86c Doc: Improve WinTab license information  
Changed classification of the wintab license from "Custom" to "LCS-  
Telegraphics License"  
  
* a82032351c forkfd/Linux: ask clone() to use the SIGCHLD as the  
termination signal  
Fixed an issue that would cause debugging a Qt application that uses  
QProcess to confuse both gdb and lldb if the Linux kernel was version  
5.4 or higher. Behavior outside of a debugging session was not affected.  
  
* 5d715e09ae Avoid heap-buffer-overflow  
Avoid heap-buffer-overflow  
  
* a8ad906652 Fix a bug in the initialization (and debug-output) of BSP  
trees  
Fixed a bug in the initialization of BSP trees to increase the  
performance of QGraphicsScenes with non quadratic scene rectangles.  
  
* 9ef4fba108 QUrl::fromLocalFile: accept invalid hostnames  
Changed QUrl::fromLocalFile() to accept Windows UNC paths whose  
hostname component is not a valid Internet hostname. This makes QUrl  
able to accept extended-length paths (\\?\), device namespace (\\.\),  
WSL (\\wsl$), etc.  
  
* 80e3ded22d Avoid heap-buffer-overflow  
Avoid a heap-buffer-overflow found by oss- fuzz as issue 25243.  
  
* 8e01088b55 Add some missing QStringView overloads to QString  
A couple of methods have been added to QStringView that make it easier  
to write code that is portable between Qt 5.15 and Qt 6. Those include  
QStringView::split(), QStringView::count(), number conversion methods  
(QStringView::toInt() and friends). A couple of overloads taking  
QStringView have been added to QRegularExpression (match() and  
globalMatch()) and QString (append(), prepend(), insert() and  
localeAwareCompare()).  
  
* 75fb810340 sqlite: Upgrade to 3.33.0  
Upgraded to v3.33.0  
  
* d587f0139d Use valid glyph index for box font engine  
Fixed a potential crash when rendering text with an empty font  
database.  
  
* 03495149d2 Fix copyright year of tinycbor  
Fix aggregated copyright information of TinyCBOR component to reflect  
the years in the individual source files. Note that this is not same as  
the Copyright year in the upstream MIT license text.  
  
* 8a25540206 Fix copyright information for src/3rdparty/xcb  
Fixed copyright information for "XCB-XInput".  
  
* 17021ce53e Fix included license text for PCRE2 - Stack-less Just-In-  
Time Compiler  
Changed license text of "PCRE2 - Stack-less Just-In-Time Compiler"  
component. The documentation (incorrectly) included the generic PCRE2  
license so far.  
  
* c008da8508 Deprecate QLocale::Language entries that no locale data  
relates to  
Many obsolete language names are now deprecated in preparation for  
removal at Qt 6.0. No data has been available for any locale using these  
languages since CLDR v29 (at least; Qt now uses v37).  
  
* 171c3c3446 Deprecate ordering on QItemSelectionRange  
Ordering of QItemSelectionRange is now deprecated. It was not  
consistent with equality and should not be needed.  
  
* 4b601331c7 Update CLDR to v37, adding Nigerian Pidgin as a new  
language  
Updated to new version of CLDR (the Unicode Consortium's Common Locale  
Data Repository) v37. Various Adlam-script locales are dropped due to  
its use of a number system unsupported by 5.15's QLocale. Support for  
these locales shall be restored in Qt 6.  
  
* 1459cc8bf6 Deprecate old aliases for two countries and several  
languages  
Deprecated several Language and Country aliases, ready for removal in  
Qt 6.0, in favor of their newer names.  
  
### qtsvg  
* fdbe89e Change classification of XSVG License  
XSVG license was re-classified to HPND-sell-variant, "Historical  
Permission Notice and Disclaimer - sell variant"  
  
### qtlocation  
* 3e9d5379 Add actual text of Boost Software License  
Added actual license text of Boost Software License (used in Clipper  
Polygon Clipping Library)  
  
* 4fdb479b Update src/3rdparty/mapbox-gl-native  
Update and extend third-party documentation for Mapbox GL plugin  
dependencies: libc++, Optional, Mapbox GL Native, Boost, CSS Color  
Parser, cURL Parse Date, Earcut Polygon Triangulation Library, geojson-  
cpp, geojson-vt-cpp, geometry.hpp, kdbush.hpp, polylabel, protozero,  
RapidJSON, shelf-pack-cpp, supercluster.hpp, tao_tuple, unique_resource,  
variant, Vector Tile Library, Wagyu Geometry Processing Library,  
nunicode.  
  
* 9ac778b2 Make names of poly2tri, clipper, clip2tri libraries unique  
The generated clipper2tri, clipper, poly2tri libraries have been  
renamed to qt_clipper2tri, qt_clipper, qt_poly2tri. This avoids  
conflicts for static builds.  
  
### qt3d  
* fc5020454 Fix third-party license information about imgui  
Fix issue in the documentation that caused attributions for imgui  
third-party code to not show up.  
  
* aa13ce25a Improve third-party license information about assimp  
Also document sub-projects that are part of the Assimp project:  
Clipper, irrXML, Open3DGC, OpenDLL-Parser, Poly2Tri, RapidJSON, Unzip,  
Utf8Cpp, and Zip.  
  
### qtserialbus  
* f49a99f SocketCAN: Fix loading libsocketcan on Debian  
Fixed that libsocketcan could not be loaded when no symlink  
libsocketcan.so -> libsocketcan.so.2 was present.  
  
### qtwebchannel  
* 62f2be9 Fix infinite recursion when wrapping a self-contained object  
twice  
Fixed infinite recursion when dealing with self contained objects.  
  
### qtnetworkauth  
* c7dba07 Add client id and shared secret to token refresh requests  
Fixed starting a new session with some servers (e.g. Google) when using  
a refresh token.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-85193 [REG: 5.12.4->5.12.5]: A SVG path with a high stroke width  
is not rendered correctly  
* QTBUG-81723 [REG: 5.13->5.14 & 5.12.5->5.12.6] Widgets are only half  
repainted when shown on SSH-forwarded X display  
* QTBUG-83313 Setting CaseSensitivity in QSortFilterProxymodel for  
QRegularExpression doesn't work  
* QTBUG-60022 Documentation: ANDROID_EXTRA_PLUGINS needs additional  
information  
* QTBUG-85981 [REG: 5.14 -> 5.15] Windows: Posted events get stuck with  
nested event loops  
* QTBUG-86191 QLocale::system().standaloneMonthName() wrong value on  
macos  
* QTBUG-86170  QLabel::setPixmap appears truncated under high screen  
device pixel ratio  
* QTBUG-86166 inconsistent ctrl-c copy in qtableview  
* QTBUG-86268 [REG 5.12.4 -> 5.13.0] QTableView::sortByColumn() no  
longer allows re-sorting if sortingEnabled  
* QTBUG-86392 Possible binary break 5.15.0->5.15.1, Qt5Core.dll  
* QTBUG-86383 Uninitialized memory sent to X server in  
QXcbDrag::handleDrop  
* QTBUG-85560 [REG: 5.12 -> 5.13] Non English characters fail to render  
correctly  
* QTBUG-79094 Qt cannot be build with JDK version >=12  
* QTBUG-83409 Array read/write doesn't work in QIBASE Driver  
* QTBUG-86394 QNetworkInterface methods broken when targeting Android 11  
(API-30)  
* QTBUG-86418 http2 crash when I use unicode in http header  
* QTBUG-86546 Tracegen error  
* QTBUG-46203 tst_qsslkey fails on Red Hat 6.6 x64  
* QTBUG-86483 QDoubleSpinBox and QSpinBox valueChanged called twice  
* QTBUG-83152 It's impossible to prepare sql statements, with the  
firebird/interbase driver, which contains PSQL variable names, because  
they are colon prefixed.  
* QTBUG-86336 tst_QNetworkReply tests are failing with CentOS 8.1 and  
system OpenSSL  
* QTBUG-86497 Missing build system dependencies for doc snippets results  
in broken build  
* QTBUG-86607 QFile::open(int fd, ...) refers to 'raw' mode  
* QTBUG-86587 QPushButton: styling causes clicked() signal not to emit  
when clicked  
* QTBUG-84356 QSqlDriver::subscribeToNotification lost if PGSQL server  
restarts  
* QTBUG-86282 Use more recent JDK version to build Qt for Android  
* QTBUG-86319 Use of CLONE_PIDFD for forkfd interacts badly with  
debugging  
* QTBUG-86635 Wrong suggestions for an obsolete method  
* QTBUG-86575 qwindowsservices.cpp doesn't compile with mingw64 GCC  
10.1.0  
* QTBUG-85676 Issue with openUrlExternally  
* QTBUG-86691 Inconsistent XPM handling  
* QTBUG-84256 tst_QTcpServer::qtbug6305 fails with CentOS 8.1 x64  
* QTBUG-84253 tst_QNetworkInterface::localAddress fails with CentOS 8.1  
x64  
* QTBUG-84254 tst_QUdpSocket::multicast fails with CentOS 8.1 x64  
* QTBUG-85105 QWindow::startSystemMove() does not work with QML  
DragHandler on macOS  
* QTBUG-86062 qmake accepts only last /MERGE option from QMAKE_LFLAGS  
when generate VS project  
* QTBUG-86702 Some GIFs don't load/play anymore in Qt apps I tested  
* QTBUG-86547 Heap corruption happens due to double memory release when  
QDomAttr::setNodeValue is called.  
* QTBUG-86585 qfilesystemengine_unix.cpp compilation error on QNX  
* QTBUG-69608 cocoa: key press events for modifier keys do not have  
nativeVirtualKey  
* QTBUG-86718 qmake cannot run target compiler for iOS Xcode 12  
* QTBUG-10561 Modal QProgressDialog's setValue() does not always need to  
call processEvents()  
* QTBUG-86287 Static 5.15.0 compile results in "undefined reference to  
xcb_aux_create_gc"  
* QTBUG-85436 QMimeDatabase may not use mime type file globs properly  
* QTBUG-86620 When doing a XMLHttpRequest then the status code will be  
set to 0 indicating that an error occured even though it is not actually  
having a problem  
* QTBUG-86580 QComboBox::setPlaceholderText() has side-effects, changes  
currentText  
* QTBUG-86675 qmake creates nondeterministic results  
* QTBUG-86411 Fusion style: QGroupBox height doesn't adjust if no title  
* QTBUG-86306 /etc/localtime is always treated as symlink  
* QTBUG-86873 QJsonDocument problem on chinese key  
* QTBUG-87047 MSVC 2019 raises Warning C4619 about C4345 in QVector when  
compiling with /W4  
* QTBUG-86604 Only availableGeometryChanged() (not geometryChanged() )  
is emitted when the logical DPI of a screen changes  
* QTBUG-76902 Widgets and fonts have wrong size after moving to screen  
due to disconnect with different DPI when dpiawareness = 2  
* QTBUG-79248 TrayIcons Menu does not scales its size when changing DPI  
* QTBUG-87092 Crash in QThreadPool::clear()  
* QTBUG-85366 QTreeView: FetchMore is not getting called for all the  
entries  
* QTBUG-86207 QGuiApplicationPrivate::processMouseEvent() crashes on NaN  
event globalPos  
* QTBUG-87174 Wrong initialization of the bsp tree used by  
QGraphicsScene  
* QTBUG-86883 CMake error in Qt5BootstrapConfig.cmake  
* QTBUG-86253 Mouse source point error caused by multi-touch  
* QTBUG-87259 doc typo on The State Machine Framework  
* QTBUG-86277 QUrl::fromLocalFile should return valid URLs for UNC paths  
with invalid hosts (\\wsl$)  
* QTBUG-87009 tst_QTcpSocket::connectToHostError fails in Windows 10  
MinGW developer-build  
* QTBUG-87320 Segfault in qimage_conversions.cpp  
* QTBUG-87267 QFont::exactMatch() returns false for installed fonts in  
Qt 5.15.1  
* QTBUG-87273 QFileSystemModel / QSFPM / QTreeView : infinite loop in  
latest 5.15 commits  
* QTBUG-86516 QStringView-related API missing in Qt5  
* QTBUG-87611 qnearfieldtarget.cpp:239:14: error: ambiguous overload for  
'operator<'  
* QTBUG-87057 QListView item looses items from models that don't  
override moveRows during internal drag'n'drop  
* QTBUG-85006 Mouse cursor is displayed only after a while when a VNC  
client connects  
* QTBUG-87483 QFontDialog::selectedFont() Does not returns Actual  
selected Font  
* QTBUG-85016 Q_UNREACHABLE was reached at qtextengine.cpp:1551  
* QTBUG-69155 Android: tst_QWindow::exposeEventOnShrink_QTBUG54040 fails  
* QTBUG-83916 Any Tooltip crashes on Android  
* QTBUG-86307 Year appears wrong in the Calendar Widget example  
* QTBUG-85966 QCalendarWidget incorrecty localizes year in topbar  
* QTBUG-86733 [Android] NoSuchMethodException when using QtMultimedia  
* QTBUG-86210 Qt 5.15.1 fails to build on INTEGRITY due to type size  
exceeds implementation limit errors  
* QTBUG-85915 macOS crash when opening several times QComboBox drop  
downs after moving application windows from one screen to another  
* QTBUG-67928 Qt uses wrong source for logical DPI on X  
* QTBUG-60822 [REG: 4->5] WA_TranslucentBackground cannot be changed  
after widget has been shown  
* QTBUG-41341 tst_qcolumnview fails on Mac OS X  
* QTBUG-85123 [REG:5.13->5.14]: When using GSSAPI to connect to a server  
requiring NTLM authentication then it can fail to do the authentication  
* QTBUG-86674 Deploying Qt application to Android device is really slow  
* QTBUG-84267 QIcc::fromIccProfile crashes with SIGBUS (unaligned  
access) on ARM  
* QTCREATORBUG-24665 Unable to drag/drop widgets from designer  
* QTBUG-86786 Widgets: drag and drop doesn't work on macOS  
* QTBUG-71939 Not possible to Drag'n Drop files  
* QTBUG-68862 tst_QWidget::updateWhileMinimized autotest fails on Ubuntu  
18.04  
* QTBUG-77126 [REG] Documentation no longer shows the relationship  
between classes from different modules  
* QTBUG-77833 Mac: context menu not closed when minimizing window  
* QTBUG-87066 Qt6: Android, unable to build examples with cmake  
* QTBUG-87143 QXdgDesktopPortalFileDialog sometimes breaks when  
selectedFilter is supplied  
* QTBUG-74542 Test are disabled from MinGW builds with packaging flag  
* QTBUG-80328 tst_QUdpSocket::writeDatagramToNonExistingPeer fails with  
MSVC2019  
* QTBUG-83806 QSystemTrayIcon sends too large pixmap over Dbus if HiDPI  
scaling is enabled  
* QTBUG-87137 tst_QApplication::sendEventsOnProcessEvents() failed on  
Ubuntu 20.04  
* QTBUG-87588 [REG 5.15.1 -> 5.15] QFileSystemModel with QDir::NoDot  
filter hangs  
* QTBUG-87728 tst_QGraphicsAnchorLayout::layoutDirection() failed on  
Ubuntu 20.04 in CI  
* QTBUG-74287 QLocale::nativeCountryName does not use country  
information from locale object  
  
### qtsvg  
* QTBUG-87583 SVG icons with with <DOCTYPE svg> not loading  
  
### qtdeclarative  
* QTBUG-85938 Loader status unexpected  
* QTBUG-85317 qmlformat breaks on template literals  
* QTBUG-85724 Running example "window and screen" gives error on  
immediate run  
* QTBUG-86524 QQuickView, Memory leak of QOpenGLContextGroup object  
* QTBUG-61475 Can not input Chinese in TextEdit when load qml in  
QQuickWidget  
* QTBUG-82157 Application crashes when changing an active Drag's  
supportedActions  
* QTBUG-86989 QML crashes when more than one inline component is defined  
* QTBUG-86979 qmlformat duplicates Inline component in 5.15.1  
* QTBUG-86980 qmlformat fails on "for of"  
* QTBUG-87222 qmlformat remove property name on objects decalred with  
variable as name  
* QTBUG-85302 Mouse-click catch in QML Listview's header with clip =  
true  
* QTBUG-74046 Events stealing happens for MouseArea in some cases  
(preventStealing == true)  
* QTBUG-86402 [REG 5.12 -> 5.13] Animation in Popup causes app's crash  
after Popup closed  
* QTBUG-86676 QML garbage collector doesn't work correctly with Loader  
* QTBUG-87680 TableView: contentHeight doesn't update when new rows are  
added  
* QTBUG-85713 Inline components trigger assertion with ListElement  
* QTBUG-87464 Inline component state issue  
* QTBUG-85431 void QAbstractScrollArea::mouseMoveEvent(QMouseEvent *e)  
is called falsely on double tap on a touchpad of a notebook  
* QTBUG-62989 Layout.left/rightMargin doesn't mirror with  
LayoutMirroring  
* QTBUG-75777 QQmlEngine deadlock in destructor with asynchronous Loader  
* QTBUG-87150 QML_FOREIGN needs clearer documentation to indicate that  
it is using the name of the struct or QML_NAMED_ELEMENT  
* QTBUG-82890 SequentialAnimation does not stop when loops:  
Animation.Infinite and alwaysRunToEnd: true  
* QTBUG-87821 TableView: two sync-ed table views can sometimes end up  
out-of-sync  
  
### qtactiveqt  
* QTBUG-86666 dumpcpp tool not working for x64 components  
  
### qtscript  
* QTBUG-86527 Qt Script: tst_QScriptV8TestSuite fails with MinGW  
  
### qtmultimedia  
* QTBUG-85470 [REG: 5.14.2->5.15.0]: When capturing the camera which is  
showing via a QVideoWidget it will never emit the imageCaptured signal  
  
### qttools  
* QTBUG-86188 qdoc: Crash when using a tagged \fn command  
* QTBUG-86293 "winrtrunner --list-devices" hangs  
* QTBUG-86477 [REG 5.15.0->5.15.1] assistant not build when building  
whole Qt statically  
* QTBUG-86598 Assistant fails to compile if QT_NO_CLIPBOARD is defined  
* QTBUG-84727 QHelpIndexWidget does not emit documentActivated or  
documentsActivated  
* QTBUG-86759 Missing QtWebEngineProcess Application in application  
frameworks  
* QTBUG-86988 qdoc: DocBook output format: XML special characters are  
escaped twice  
* QTBUG-84703 qdoc: DocBook generator: scoped enums not handled  
correctly  
* QTBUG-87802 qdoc: \sincelist generates broken links in certain  
conditions  
* QTBUG-88167 ../shared/numerus.cpp:165:5: error: ‘Bihari’ is not a  
member of ‘QLocale’  
  
### qtlocation  
* QTBUG-86248 qtlocation installs internal libs of 3rdparty libraries  
  
### qtwayland  
* QTBUG-86176 Subsurfaces under dialogs don't have the QEvent::Exposed  
event emitted  
* QTBUG-86109 Wayland:  
* QTBUG-86291 Wayland doesn't export files properly in a no-opengl build  
* QTBUG-83303 qtwayland - configure test failure - Project ERROR: Test  
config.qtwayland_client.tests.dmabuf-server-buffer tries to use  
undeclared library 'drm'  
* QTBUG-83263 Rendering of multiple framebuffers object leads to  
degraded render performance with Wayland  
* QTBUG-87657  clipboard selection does not offer all mime types  
available for the content  
* QTBUG-87959 The Wayland license should be GPL not LGPL  
* QTBUG-85767 Scrolling inverted  
  
### qt3d  
* QTBUG-86721 [Regression] Scene3D rendering with underlay composition  
on HighDpi display is incorrect.  
* QTBUG-86436 Shader errors if there are multiple windows  
* QTBUG-84847 Scene3D crashes on destruction  
* QTBUG-85018 [REG: 5.14->5.15] QOpenGLShader::compile(Fragment): ERROR:  
4:2: 'add' : syntax error syntax error  
  
### qtgraphicaleffects  
* QTBUG-86486 [Reg 5.13.1->5.14.0]ColorOverlay not working well when  
image has empty source  
  
### qtquickcontrols  
* QTBUG-86315 Warning message from Accessible, TableViewColumn  
  
### qtserialbus  
* QTBUG-87328 SocketCAN plugin broken due to libsocketcan being  
unavailable  
  
### qtwinextras  
* QTBUG-87694 Qt compilation fails when passing -no-qml-network  
  
### qtwebchannel  
* QTBUG-84007 Infinite recursion when wrapping  
  
### qtwebengine  
* QTBUG-85494 [REG: 5.14->5.15] Quick minimal browser crashes when  
opening view source  
* QTBUG-86599 Crash on resize in WebEngineView  
* QTBUG-85817 crash on resize  
* QTBUG-86672 Context menu pops up while "grp:menu_toggle" is set  
* QTBUG-65223 [REG 5.9 -> 5.10] loadStarted is emitted twice when  
loading link with anchor  
* QTBUG-87129 Completion in the DevTools "Console" tab only works for  
top-level objects  
* QTBUG-86972 [REG] QtPDF isn't properly installed as a framework unless  
WebEngine is also installed  
* QTBUG-87113 The qt_plugin_qpdf.pri file appears to be missing from the  
iOS package which should be in mkspecs/modules  
* QTBUG-84632 When starting a webengine based example from a network  
share then it will fail to start the QtWebEngineProcess.exe  
* QTBUG-85363 [REG 5.13 -> 5.14] QtWebEngine is listed as "Chromium" in  
PulseAudio  
* QTBUG-88219 webengine build fails without GLES3/gl32.h header  
  
### qtquickcontrols2  
* QTBUG-86212  tst_QQuickPopup::setOverlayParentToNull fails in with  
macOS 10.14  
* QTBUG-85719 SpinBox fails to validate the entry after it failed  
already  
* QTBUG-86851 QQC2 Menu contentModel not deleted  
* QTBUG-83698 Using Keys.onReturnPressed from Button to open Menu causes  
the first MenuItem to get triggered on show  
* QTBUG-85699 Material ToolBar: "QML Material: Binding loop detected for  
property "foreground""  
* QTBUG-85884 When a Dialog is hidden then it is possible that it does  
not reset the focus correctly if when it loses active focus it does the  
process again to hide the dialog  
* QTBUG-87164 qmllint library search regression  
  
### qtcharts  
* QTBUG-75500 Stack overflow on high zoom out of QChart with a  
logarithmic axis  
  
### qtnetworkauth  
* QTBUG-87703 Qt NetworkAuth fails to refresh auth with refresh token  
(using Google's OAuth2)  
  
### qtquick3d  
* QDS-2609 Imported 3D model appearing completely black  
* QDS-2636 Custom effects and materials do not work correctly in editor  
unless defined in components  
* QDS-2637 Shader compilation fails if custom material shaders require  
any shader uniform properties  
  
Known Issues  
------------  
  
Credits for the  release goes to:  
---------------------------------  
  
Aavitsland Eirik  
Achtelik Mike  
Adam Cristian  
Agocs Laszlo  
Asaduzzaman Nadim  
Bin Chen  
Blasche Alex  
Blomfeldt Eskil Abrahamsen  
Bornemann Joerg  
Boudjelthia Assam  
Brasser Michael  
Brüning Michael  
Buhr Andreas  
Burtsev Kirill  
Carlon Luca  
Casafranca Juan  
Casafranca Juan José  
Castro Helio Chissini de  
Chuan Wang  
ChunLin Wang  
Cid Albert Astals  
Croitor Alexandru  
Curtis Mitch  
D'Angelo Giuseppe  
David Szabolcs  
Dewes Aaron  
Doroshchuk Val  
Edmundson David  
Ehrlicher Christian  
Falsini Fabio  
Faure David  
Fella Nicolas  
Funk Kevin  
Gaist Samuel  
Gladhorn Frederik  
Goldstein Maximilian  
Golubev Andrei  
Grulich Jan  
Gustavsen Richard Moe  
Halmet Heikki  
Harmer Sean  
Hartmann Andre  
Heikkinen Jani  
Heikkinen Miikka  
Heimlich Christian  
Hermann Ulf  
Hilsheimer Volker  
Jensen Allan Sandfeld  
Kazakov Dmitry  
Kieß Steffen  
Kleint Friedemann  
Klitzing André  
Klocek Michal  
Klots Andreas  
Knoll Lars  
Kobus Jarek  
Koehne Kai  
Koh Sze Howe  
Kokko Antti  
Kosmale Fabian  
Krause Volker  
Krems Marcel  
Krus Mike  
Kurazyan Sona  
Kyzivat Keith  
Lee Elvis  
Lee Inho  
Lemberg Werner  
Lemire Paul  
Loehning Robert  
Macieira Thiago  
MagnaboscoL MagnaboscoL  
Meusel René  
Mikolajczyk Piotr  
Nordheim Mårten  
Paeglis Gatis  
Pocheptsov Timur  
Pol Aleix  
Potter Lorn  
Qi Liang  
Rehn Arno  
Reinio Topi  
Rineau Laurent  
Romberg Christian  
Rutledge Shawn  
Samir Ahmad  
Schleifenbaum Christoph  
Schwan Carl  
Seiderer Peter  
Shaw Andy  
Skoland David  
Srirattanamet Ratchanan  
Sæther Jan Arve  
Sørvig Morten Johan  
Trotsenko Alex  
Tvete Paul Olav  
USTA Ömer Fadıl  
Valdmann Jüri  
Varga Peter  
Verria Doris  
Vestbø Tor Arne  
Volkov Alexander  
Welbourne Edward  
Wicking Paul  
Wolff Oliver  
Yu Zhang  
Zahorodnii Vlad  
Zakor Tamas  
