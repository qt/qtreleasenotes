Release note  
============  
  
Qt 5.15.6 release is a patch release made on the top of Qt 5.15.5. As a patch  
release, Qt 5.15.6 does not add any new functionality but provides bug fixes  
and other improvements.  
  
For detailed information about Qt, see the Qt 5.15 online documentation:  
https://doc.qt.io/qt-5/index.html.  
  
Important Changes  
-----------------  
  
### qtbase  
* a273c68018 QPageSize: make PageSizeId ctor non-explicit  
Conversion from a QPageSize::PageSizeId is now implicit.  
  
* 8e6b4f5d2a Fix conversion of swap interval from QGLFormat to  
QSurfaceFormat  
Fixed an issue where the default swap interval of QGLWidget's surface  
format would be set to an invalid value.  
  
* 0095b87903 macOS: allow Qt::AA_DontShowShortcutsInContextMenus  
overrides  
The shortcutVisibleInContextMenu property defaults to the value of the  
Qt::AA_DontShowShortcutsInContextMenus attribute, which in turn defaults  
to the platform integration. To override the default, set the  
application attribute after instantiating QApplication, or override the  
default for each QAction instance.  
  
* f76bea3951 Fix mapping between Han and other CJK scripts  
Fixed an issue where certain shared CJK characters would be displayed  
using the Chinese system font rather than the Japanese one, even on  
Japanese locale.  
  
* 9572473e4f Revert "Windows: Add synthesized fonts also when there is a  
style name"  
Fixed a regression where different font styles and/or weights would not  
be available.  
  
* 8cda03b066 Change QCollator's default locale to QLocale().collation()  
The default locale used by QCollator is now the collation locale of the  
default QLocale. This restores the ability (lost at 5.14) to control the  
locale used by QString::localeAwareCompare(), while retaining the use of  
a collation locale when the default is the system locale.  
  
* a8409dc92c QVarLengthArray: fix aliasing error in insert(it, n, v)  
Fixed an aliasing bug affecting insertions of objects aliasing existing  
elements.  
  
* 8ffc652f1e QXpmHandler: fix re-entrancy bug in xpm_color_name  
Fixed a race condition when concurrently writing .xpm files.  
  
* b94eda4f81 QXpmHandler: actually limit characters-per-pixel to four  
Instead of writing a corrupt file, rejects to write XPM files with more  
than 64^4 colors (more than four characters per pixel) now.  
  
* dde4061f37 MySQL: remove the version number checks in favor of actual  
functionality  
Fixed the detection of whether the client and server support prepared  
statements. This was caused by the mariadb connector library reporting  
its own version numbers (starting in version 3.2) instead of the server  
version.  
  
* 2762bbb5c3 Fix memory leak if eXIf has incorrect crc  
Fix for possible memory leak in libpng was backported.  
  
### qtsvg  
* 22388ac Limit font size to avoid numerous overflows  
Avoid numerous overflows by limiting font size to 0xffff. This fixes  
oss-fuzz issue 31701.  
  
### qtwayland  
* a3ee3b1a client: Gracefully handle shutdown and window hiding  
Fixed a crash that could happen when hiding or closing windows while Qt  
Quick was actively rendering on a different thread.  
  
### qt3d  
* 3e7af0520 Fix multi-view picking  
Non rendered entities (due to layer filtering) are no longer pickable  
  
### qtimageformats  
* d2f7d79 Update bundled libtiff to version 4.3.0  
Bundled libtiff was updated to version 4.3.0  
  
### qtwebengine  
* Security fixes from Chromium up to version 92.0.4515.159, including:  
    - CVE-2021-30522: Use after free in WebAudio  
    - CVE-2021-30523: Use after free in WebRTC  
    - CVE-2021-30530: Out of bounds memory access in WebAudio  
    - CVE-2021-30533: Insufficient policy enforcement in PopupBlocker  
    - CVE-2021-30534: Insufficient policy enforcement in iFrameSandbox  
    - CVE-2021-30535: Double free in ICU  
    - CVE-2021-30536: Out of bounds read in V8  
    - CVE-2021-30541: Use after free in V8  
    - CVE-2021-30544: Use after free in BFCache  
    - CVE-2021-30547: Out of bounds write in ANGLE  
    - CVE-2021-30548: Use after free in Loader  
    - CVE-2021-30551: Type Confusion in V8  
    - CVE-2021-30553: Use after free in Network service  
    - CVE-2021-30554 Use after free in WebGL  
    - CVE-2021-30556: Use after free in WebAudio  
    - CVE-2021-30559: Out of bounds write in ANGLE  
    - CVE-2021-30560: Use after free in Blink XSLT  
    - CVE-2021-30563: Type Confusion in V8  
    - CVE-2021-30566: Stack buffer overflow in Printing  
    - CVE-2021-30568: Heap buffer overflow in WebGL  
    - CVE-2021-30569  
    - CVE-2021-30573: Use after free in GPU  
    - CVE-2021-30585: Use after free in sensor handling  
    - CVE-2021-30587: Inappropriate implementation in Compositing on Windows  
    - CVE-2021-30588: Type Confusion in V8  
    - CVE-2021-30598: Type Confusion in V8  
    - CVE-2021-30599: Type Confusion in V8  
    - CVE-2021-30602: Use after free in WebRTC  
    - CVE-2021-30603: Race in WebAudio  
    - CVE-2021-30604: Use after free in ANGLE  
    - Security bug 1184294  
    - Security bug 1194330  
    - Security bug 1194689  
    - Security bug 1197786  
    - Security bug 1198216  
    - Security bug 1198385  
    - Security bug 1202534  
    - Security bug 1204814  
    - Security bug 1205059  
    - Security bug 1209558  
    - Security bug 1211215  
    - Security bug 1227933  
    - Security bug 1228036  
  
### qtwebsockets  
* 30b0376 Clear frame before emitting signals to prevent duplicating  
messages  
Clear frame before emitting signals to prevent duplicating messages  
  
### qtquickcontrols2  
* 10ede696d ToolTip: use contentWidth of Text contentItem to account for  
newlines  
The implicit width of ToolTips now accounts for newlines in the text.  
If you want to use the old behavior, set ToolTip's contentWidth to  
implicitContentWidth.  
  
### qtvirtualkeyboard  
* 0d2174eb Fix high CPU utilization caused by key repeat timer  
Fixed high CPU utilization caused by key repeat timer.  
  
* 005e6f28 Fix processing of hard Qt::Key_Backspace and Qt::Key_Delete  
Fix processing of hard backspace and delete keys.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-94070 Memory corruption in sqlite plugin  
* QTBUG-93600 90° X rotation as quaternion produces NaN on euler angle  
* QTBUG-93295 Session Resumption with Session ID - IPv6 -  
ephemeralServerKey is missing  
* QTBUG-94087 [reg 5.11->5.15] No longer possible to start a drag from  
item views with a double-click  
* QTBUG-77771 A Double click on QtreeView/QTreeWidget index is emitting  
two clicked() and one doubleClicked() signal  
* QTBUG-94226 QListView - broken drag-n-drop items movement  
* QTBUG-94269 QIntValidator: integer values exceeding top "intermediate"  
according to validate() func  
* QTBUG-86754 [Reg 5.12.4-> 5.12.5]Action text overlaps the shortcut in  
menu when padding is used  
* QTBUG-92234 QTranslator.load problem by skipping some  
* QTBUG-70498 Cannot scroll first tab right, using scroll button in  
QTabBar, when tab size do not fit into visible rect.  
* QTBUG-56322 Qt for Android source package build error in examples  
* QTBUG-36565 Some key symbols generated by xkb level 3 shift don't work  
in QTextBrowser, QTextEdit, QLineEdit  
* QTBUG-93742 Error in public function "setclearbuttonenabled" of  
"QLineEdit" control  
* QTBUG-91120 QDate::fromString() fails on isolated dates on macOS with  
TZ=Europe/Lisbon  
* QTBUG-94347 QRandomGenerator64 refers to functions as static, aren't.  
* QTBUG-71894 Hangul composition bug  
* QTBUG-94032 Command line is too long when building large projects  
* QTBUG-94470 Incorrect parsing of HTTP2 frame headers.  
* QTBUG-93764 QPrintPreviewDialog: printer orientation not updated by  
QPageSetupDialog  
* QTBUG-76948 IOS: disconnect second screen while app in b/g, it crashes  
when app goes into foreground  
* QTBUG-94532 Markdown checkboxes are clipped when text range selected  
* QTBUG-89379 QQuickWindow::QtTextRendering cause font problem on Apple  
M1  
* QTBUG-83089 NameFilters not working in FileDialog in Android 10  
* QTBUG-67944 If user pressed back button during application startup.  
Application becomes unresponsive.  
* QTBUG-65637 Window minimizing broken after building QT app with Mac OS  
High Sierra SDK  
* QTBUG-94246 Memory leak in qsql_oci plugin  
* QTBUG-94069 MacOS ComboBox Focus Ring is Too Tall  
* QTBUG-91919 Qt will crash if changing screen resolution on Mac  
* QTBUG-94706 missing documentaiton details about QFile::copy()  
* QTBUG-81251 _debug libraries are missing from pre build Qt on Mac  
* QTBUG-83869 Correction to the documentation:  
https://doc.qt.io/qt-5/qtransform.html#basic-matrix-operations  
* QTBUG-85598 [REG: 5.13 -> 5.14] Japanese character appears incorrectly  
* QTBUG-94175 QGraphicsProxyWidget: rendered Arabic text incomplete in  
large font sizes when OpenGL is used  
* QTBUG-91619 QCFSocketNotifier does not handle connect  
* QTBUG-94781 [Reg-5.15.4->5.15.5] Bold font is not picked up when  
QFontDatabase is used  
* QTBUG-91398 When QFont::NoFontMerging is set then if bold or italics  
is requested that is not provided by the font then it will end up not  
synthesizing this  
* QTBUG-94802 [Reg-5.15.4->5.15.5]Menu separator is not visible  
* QTBUG-95005 Typo in QOpenGLPaintDevice::dotsPerMeterY  
* QTBUG-94824 In qlinedit, icon and text overlap  
* QTBUG-94463 QThreadPool creates one thread more than maxThreadCount  
* QTBUG-92182 Qt Dock Widgets super slow to dock  
* QTBUG-92232 [REG] Option Clicking Window Close Button Crashes App  
* QTBUG-94799 QFileDialog file name completer doesn't work with Proxy  
Model  
* QTBUG-78043 non-native QFileDialog displaying incorrect mapped network  
drive names  
* QTBUG-91125 QTextFormat::FullWidthSelection does not work with right-  
to-left text layout  
* QTBUG-95042 QFrame Qt::WA_TranslucentBackground is broken with  
specific window flags and drawable child item  
* QTBUG-94981 QTreeView: expandToDepth() and expandAll() ends  
prematurely for asynchronous models  
* QTBUG-94788 QListView will be reset when setSelectionMode  is  
MultiSelection  
* QTBUG-86846 the password box not refreshed under Chinese input method  
* QTBUG-95009 QNetworkDiskCache::cacheSize() returns a size twice as  
large as the real one.  
* QTBUG-94733 When the display is set to 150% and a QMdiSubWindow is  
maximized then the icons can be incorrectly displayed  
* QTBUG-95277 HTTP2: QNetworkReply::encrypted not emitted  
* QTBUG-95293 QCocoaAccessibilityElement incorrect selector for  
"enabled": should be isAccessibilityEnabled not  
accessibilityEnabledAttribute  
* QTBUG-91459 When using Speech Recognition on a multiple monitor setup  
telling it to click a button does not always work on the secondary  
monitor  
* QTBUG-95239 Massive memory consumption when rendering small svg  
* QTBUG-83182 QFutureWatcher resultsReadyAt may report rubbish  
* QTBUG-77656 Crash when waking up with multiple displays in clamshell  
mode  
* QTBUG-94790 moc fails to parse include inside enum  
* QTBUG-95429 Expired certificates in tst_QSslCertificate  
* QTBUG-95351 In the help pages: A fromVector() example is not right  
* QTBUG-95071 mysql client version detection broken with MariaDB 10.6  
* QTBUG-56595 QXcbConnection::getTimestamp() returns old timestamp  
* QTBUG-95631 Stylesheet issue when try to change background color with  
a editable combobox on hover  
* QTBUG-95619 [Mac] Memory leak in  
QNSWindow::applicationActivationChanged  
* QTBUG-69515 Linux, WindowStaysOnTopHint does not work.  
* QTBUG-85529 Polytonic Greek characters cannot be composed both ways  
* QTBUG-94990 REG: 5.15.4->5.15.5: When a window is switched to be  
FullScreen then it will end up keeping a bar at the bottom of the window  
which should not be visible  
* QTBUG-87863 CMake configuration fails with multiple calls to  
find_package(Qt)  
* QTBUG-87813 WASM: App sometimes crashes on aborting NetworkRequest  
* QTBUG-2390 Generated .la files are not correct for frameworks  
* QTBUG-92477 Memory leak in QFontDatabase  
* QTBUG-83419 Q2-2020 Flaky failing autotest function remainingTime in  
qtimer  
* QTBUG-58519 tst_QTimer::remainingTime() 'qAbs(remainingTime - 150) <  
50' returned FALSE on Windows and OS X  
* QTBUG-81504 QWaylandWindow::handleUpdate creates thousands of pending  
frame callbacks, causing wayland connection termination  
* QTBUG-73990 Context Menu Items Fonts and Hotkeys Not Displaying  
* QTBUG-91713 QtBase benchmarks fail for qtimezone, qdiriterator, and  
qfile  
* QTBUG-95050 [REG: 5.2->5.14] Locale used by  
QString::localeAwareCompare() no longer changeable  
* QTBUG-80957 QFutureInterface: reportResults with an empty vector  
breaks results  
* QTBUG-85839 Documentation: wrong default value for Layout Direction  
* QTBUG-88248 QObject orphaned connections soft-leak  
* QTBUG-87774 QToolBar::clear() leaks memory  
* QTBUG-95314 WASM: Diverging timezones in C++/QML  
* QTBUG-71590 Qt is using "Non-SDK" interfaces, will be blocked by  
Android  
* QTBUG-94215 [Reg 5.15.2->5.15.3/6] QString::lastIndexOf is broken  
  
### qtsvg  
* QTBUG-94878 QSvgRenderer crash  
* QTBUG-92184 QtSVG cannot understand minified SVGs if they contain arcs  
  
### qtdeclarative  
* QTBUG-93857 Mac Link Accessibility, Link cannot be triggered by  
VoiceOver  
* QTBUG-89736 focusable item becomes impossible to focus after  
reparenting to a newly loaded item  
* QTBUG-94223 Regression[5.14->5.15] 'model' is no longer an implicit  
data role in delegates in Custom delegate  
* QTBUG-75553 QML Canvas, reset line dash failed  
* QTBUG-89375 No C++ documentation for containmentMask  
* QTBUG-93880 MultiPointHandlers (DragHandler, PinchHandler) don't emit  
the grabChanged signal  
* QTBUG-78258 DragHandler's grab permission CanTakeOverFromAnything does  
not respect keep grab  
* QTBUG-79163 DragHandler steals events from a MouseArea with  
preventStealing = true  
* QTBUG-94622 svg Image is  Pixelated when windows is scaled  
* QTBUG-94844 Rendering errors with ShaderEffect after hiding and  
reshowing a window  
* QTBUG-95417 Regression 5.15.4: gc() within generator functions crash  
* QTBUG-94820 Crash when declaring an alias to a readonly object-typed  
subproperty  
* QTBUG-89822 Error with readonly alias property  
* QTBUG-95314 WASM: Diverging timezones in C++/QML  
* QTBUG-95825 Live preview not starting  
* QTBUG-76310 Dragging (QDrag) triggered by touch event requires an  
additional press to move drag target  
* QTBUG-94798 crash in QQuickDesignerSupport with gcc at ubuntu  
* QTBUG-93973 Races in QJSEngine()  
* QTBUG-75862 FocusReason is broken in Controls 2  
* QTBUG-94928 loop QQuickDesignerSupport with simple example  
  
### qttools  
* QTBUG-74353 Qt Assistant doesn't take stylesheet into account with  
search result view  
* QTBUG-91082 [REG: 5.12->5.13] Assistant does not support custom  
filters anymore  
* QTBUG-95561 Typo in the "Introduction To QDoc" manual page.  
* QTBUG-87677 windeployqt locates a release version of icudtXX.dll for a  
debug binary  
  
### qtlocation  
* QTBUG-95221 QGeoCoordinate::toString() sometimes return wrong values  
  
### qtconnectivity  
* QTBUG-90760 BT discovery stopped working after moving to Qt 5.15.2  
* QTBUG-90369 Heart-rate crashes during its use  
* QTBUG-95156 Crash when discovery Bluetooth LE device on Windows with  
Bluetooth off  
* QTBUG-95349 Typo in Bluetooth Low Energy Overview documentation  
  
### qtwayland  
* QTBUG-91264 ASSERT on shutdown in Qt Wayland  
* QTBUG-90037 Crash when hiding QtQuick window with wayland/EGL  
* QTBUG-92249 quick3d examples crashes or hangs on exit on wayland  
* QTBUG-94602 Releasing wayland buffer from Qt compositor side  
  
### qt3d  
* QTBUG-93035 Adding a disable entity to the scene and enabling it later  
isn't properly picked up  
  
### qtwebsockets  
* QTBUG-87279 [REG: 5.13.2-5.14.0] When interacting with a webpage that  
will trigger a signal via QWebChannel then if the slot is still running  
it can cause it to resend the same message rather than a new one  
  
### qtwebengine  
* QTBUG-93082 [REG 5.15.3 -> 5.15.4] qtwebengine: touchpad scroll is  
broken in wayland  
  
### qtquickcontrols2  
* QTBUG-83630 Qt Quick Control 2 Tooltip can be way too big when you  
have newlines  
* QTBUG-55705 SwipeDelegate is not swiping inside SwipeView  
* QTBUG-94307 ComboBox: without a validator bindings to acceptableInput  
don't work  
* QTBUG-77946 tst_QQuickDrawer::Universal::position(right) failed on  
Linux openSUSE_15_0 (gcc-x86_64)  
* QTBUG-87708 [Reg 5.15.0 -> 5.15.1] header's width isn't resized to  
window's width when Layout is used  
* QTBUG-94764 REG: Attached ToolTips shrink  
  
### qtcharts  
* QTBUG-94469 Doc: Wrong return type for QValueAxis::labelFormat qml  
property  
* QTBUG-94998 5.15.4 -> 5.15.5, some labels disappeared from axes  
* QTBUG-79218 When zooming out enough then the labels on the axes will  
end up showing drawing errors  
  
### qtdatavis3d  
* QTBUG-80194 Q3DScatter Memory Leak  
* QTBUG-90371 The labels for the bars are not displayed when property  
"Rotate horizontally" set max to the right  
  
### qtvirtualkeyboard  
* QTBUG-94259 High CPU load on embedded targets caused by timers  
* QTBUG-94560 The first item of selection list sometimes get highlight  
* QTBUG-94017 Cursor position moves when un-converted Japanese is  
deleted  
* QTBUG-68412 tst_plugin::test_pinyinInputMethod crashes on arm  
* QTBUG-94715 Qt Virtualkeyboards support for Chinese language doesn't  
work properly  
* QTBUG-95664 VirtualKeyboardSettings: Readonly property is not marked  
as such  
  
### qtremoteobjects  
* QTBUG-94570 QEventDispatcherWin32::registerTimer: Failed to create a  
timer  
  
### qtquicktimeline  
* QDS-3216 Flickering when using default value as implcit first keyframe  
  
### qtquick3d  
* QTBUG-91495 When importing a .fbx file it will end up not placing some  
elements correct and some angle/positions of components are also wrong  
  
### qtcoap  
* QTBUG-94763 [CoAP] When resource is observed the QT CoAP client sends  
an acknowledgement packet which is not empty.  
  
Known Issues  
------------  
  
The RTA (release test automation) reported issues in Qt 5.15.x:  
https://bugreports.qt.io/issues/?filter=21874  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Laszlo Agocs  
Jim Albamont  
Dimitrios Apostolou  
Eskil Abrahamsen Blomfeldt  
Joerg Bornemann  
Assam Boudjelthia  
Andreas Buhr  
Albert Astals Cid  
Mitch Curtis  
Giuseppe D'Angelo  
Oliver Eftevaag  
Alexandros Frantzis  
Samuel Gaist  
Pekka Gehör  
Maximilian Goldstein  
Henning Gruendl  
Richard Moe Gustavsen  
Tang Haixiang  
Heikki Halmet  
Sean Harmer  
Thomas Hartmann  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Dominik Holland  
Allan Sandfeld Jensen  
Tim Jenssen  
Jeremy Katz  
Friedemann Kleint  
Jarek Kobus  
Sze Howe Koh  
Jarkko Koivikko  
Fabian Kosmale  
Mike Krus  
Sona Kurazyan  
Igor Kushnir  
Kai Köhne  
Inho Lee  
Paul Lemire  
Robert Löhning  
Thiago Macieira  
Marc Mutz  
Yuya Nishihara  
Mårten Nordheim  
Gatis Paeglis  
Jukka Passi  
Timur Pocheptsov  
Aleix Pol  
Lorn Potter  
Liang Qi  
Topi Reinio  
André de la Rocha  
Fan RuiJie  
Shawn Rutledge  
Lars Schmertmann  
Luca Di Sera  
Andy Shaw  
Ivan Solovev  
Brett Stottlemyer  
Tarja Sundqvist  
Tasuku Suzuki  
Jan Arve Sæther  
Morten Johan Sørvig  
Ivan Tkachenko  
Jens Trillmann  
Sami Varanka  
Nico Vertriest  
Tor Arne Vestbø  
Edward Welbourne  
Paul Wicking  
Oliver Wolff  
JiDe Zhang  
