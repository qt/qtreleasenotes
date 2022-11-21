Release note  
============  
  
Qt 5.15.8 release is a patch release made on the top of Qt 5.15.7. As a patch  
release, Qt 5.15.8 does not add any new functionality but provides bug fixes  
and other improvements.  
  
For detailed information about Qt, see the Qt 5.15 online documentation:  
https://doc.qt.io/qt-5/index.html.    
  
Important Changes  
-----------------  
  
### qtbase  
* 88f007f63a PCRE2: upgrade to 10.39  
PCRE2 has been updated to version 10.39.  
  
* 12f13ac1ee qmake: Support Visual Studio 2022  
Added support for Visual Studio 2022.  
  
* 1e763219a8 freetype/no-fc: Disambiguate fonts with different widths  
Fixed a bug where fonts of different width within the same family would  
be unselectable if the Freetype font database (no-fontconfig  
configuration) was in use.  
  
* 762084c492 QVERIFY_EXCEPTION_THROWN: re-throw unknown exceptions  
Now re-throws unknown exceptions (= not derived from std::exception)  
(was: swallowed them and returned from the test function), in order to  
play nice with pthread cancellation.  
  
* 7ec94d2792 QSharedPointer: fix counter-productive QT_PREPEND_NAMESPACE  
use in qHash() impl  
The qHash(QSharedPointer<X>) overload can now use qHash(X*) overloads  
found (only) through ADL (was: ADL was disabled due to qualified lookup  
of qHash(X*)).  
  
* 8444b1ed1f QStringView: fix split(QRegularExpression) returning  
invalid data  
Fixed a bug where invalid references could be returned for  
QString::fromRawData() subjects.  
  
* 26746e4361 Use Yu Gothic UI as the main fallback font for Japanese  
Made the primary fallback font on Japanese locale "Yu Gothic UI" (the  
default system font).  
  
* dad04e532b QVarLengthArray: fix size update on failed append()  
Fixed a bug whereby a failed append() would leave the container with an  
inconsistent size().  
  
* 97e56d4fa4 QVarLengthArray: fix UB (precondition violation) in range-  
erase()  
Fixed a bug where range-erase() could invoke undefined behavior when  
called with an empty range.  
  
* a948c725e5 Fix missing characters or assert with certain font sizes  
Fixed an issue where characters would in some rare cases be missing  
from text, depending on font metrics, font size and system scale factor.  
  
### qtdeclarative  
* 72e8cb6e1d Fix missing glyphs when changing distance field parameters  
Fixed an issue where glyphs would sometimes be missing when changing  
the environment variables that define how distance fields are generated  
to certain values.  
  
* 03143a5e51 Fix Flickable wheel velocity calculation  
Flickable no longer tries to detect whether you're using a "clicky"  
wheel or a touchpad, but rather does the velocity calculation more  
correctly with elapsed time (dθ / dt). A single rotation of a "clicky"  
wheel also moves a fixed distance, which is now adjustable via  
QStyleHints::wheelScrollLines(). Animation is restored, but should now  
stay in control on touchpads; and it will once again transition the  
"moving" properties correctly when scrolling ends.  
  
### qtlocation  
* 45ff6ea6 Fix positioning must be enabled and authorized at startup to  
work on iOS  
Fix positioning must be enabled and authorized on startup to work on iOS  
  
### qtwayland  
* 1887f6b4 Fix the logic for decoding modifiers map in Wayland text  
input protocol  
Fix modifiers map decoding logic when receiving the map from the  
compositor.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-97095 Mouse clicks are not delivered to the QWidget beneath  
container QWidget in QOpenGLWIndow on Windows  
* QTBUG-97491 Android: in TextField: cannot edit inside of words, only  
at the end  
* QTBUG-95565 Qt Creator cannot build Qt 6 for iOS from the start  
* QTBUG-79081 Nested foreach generate warnings  
* QTBUG-94769 QComboBoxListView display misalignment after sliding  
* QTBUG-97116 OpenSSL TLS plugin is not loaded for OpenSSLv3  
* QTBUG-96114 [Reg : 5.12.4 -> ] ActiveX widget not rendering on  
secondary screen when System-DPI Aware is combined with high DPI scaling  
* QTBUG-96560 Android: Keyboard does not show up again if it has been  
closed with back button in some devices  
* QTBUG-93392 QVector in Qt5 still requires default constructible types  
* QTBUG-60257 [XCB]: QXcbClipboard: SelectionRequest too old messages  
can appear  
* QTBUG-89101 QPainter::fillRect broken with QBrush containing DPR > 1  
pixmap  
* QTBUG-96240 Views are not blurred  
* QTBUG-97632 Feature cxx11_future doesn't need pthread on all unix  
platforms  
* QTBUG-97009 Broken rendering on Qt 6.2 Android arm64-v8a  
* QTBUG-94806 Having Qmltypes in CONFIG leads to faulty vcxproj file  
* QTBUG-96789 Shader cache not able to write out compiled shaders  
* QTBUG-94538 Change cursor theme is not applied immediately . The Qt5  
app needs to be restarted.  
* QTBUG-97727 Tree Model Completer Example: tree model is broken due to  
bugs in MainWindow::modelFromFile  
* QTBUG-96178 [wasm] Cursor shape does not work  
* QTBUG-97811 QScrollArea performance regression  
* QTBUG-97257 QVideoWidget not showing after minimizing  
* QTBUG-94918 QWidget::show triggers windows activation  
* QTBUG-96593 Ending a QThread can cause deadlocks  
* QTBUG-97945 assert in qnsview_mouse.mm  
* QTBUG-94028 Cursor not displayed at right margin of QPlainTextEdit  
* QTBUG-97853 Tablewidget_cellClicked not working after opening Dialog  
with cellDoubleClicked  
* QTBUG-83503 wasm: dialogs wrong size when opened  
* QTBUG-97002 Building for android fail  
* QTBUG-97984 HttpStatusCodeAttribute gives 0 in case of success  
* QTBUG-98026 Nested QGraphicsViews do not clip some items when printing  
* QTBUG-93760 tst_macdeployqt::basicapp fails with macOS 11 ARM  
* QTBUG-97085 Crash while JITting QRegularExpression in multiple threads  
(Rosetta)  
* QTBUG-98099 Crash on exit with Application font and QFontComboBox  
* QTBUG-98377 QImage::reinterpretAsFormat wrong reference counting when  
out of memory  
* QTBUG-98137 Disabled button in QDialogButtonBox gets focus by Tab  
* QTBUG-89640 font.styleName depends on font loading order  
* QTBUG-98280 QAuthenticator doesn't check if algorithm is supported  
* QTBUG-90698 tst_QTextLayout::softHyphens() failed on macos 11 in CI  
* QTBUG-94036 tst_QAccessibilityMac::notificationsTest() fails  
* QTBUG-95933 Using scanner input IRcode will result in an error when  
second character is uppercase  
* QTBUG-98544 Combination of 'HangulInputMethod' and 'QGraphicsTextItem'  
does not work as expected.  
* QTBUG-93810 warnings due to enums in QSize  
* QTBUG-82455 QTextDocument::contentsChange(int,int,int) values are  
incompatible with QTextCursor  
* QTBUG-98653 QStringView::split returns invalid data  
* QTBUG-91691 [REG: 5.15.0->5.15.1] QTextDocument tables with colspan  
collapses the starting column to minimum size  
* QTBUG-95240 QTextTabel: column width changes when merging other rows  
* QTBUG-65926 QML SignalTransition crashes if signal emitted from thread  
during object destruction  
* QTBUG-62602 Underline is displayed outside the text box  
* QTBUG-86372 [xcb] WindowTransparentForInput causing problems with  
resizing  
* QTBUG-92521 WASM: QToolTips occasionally makes app exception  
* QTBUG-86671 Table cells overlap with image and relative width  
* QTBUG-97463 Showing Large image in QTextBrowser table overlaps  
* QTBUG-98752 QFontDatabase::addApplicationFontFromData does not mention  
OpenType being supported  
* QTBUG-97649 androiddeployqt exits with signing if the path contains  
spaces  
* QTBUG-72776 QKeyEvent key() only returns value of first surrogate for  
characters in Supplementary Planes  
* QTBUG-95192 Segmentation fault at application closing  
* QTBUG-80653 Keyboard LED states do not change with evdev keyboard  
* QTBUG-98856 Wrong cursor showing when restoreOverrideCursor in  
QDockWidget  
* QTBUG-94995 Changed QML files do not updated on device  
* QTBUG-86633 QML - letters randomly disappear when resizing label  
* QTBUG-99338 Configure option change QNX armv7: neon -> no  
* QTBUG-58013 Cursor position changes not properly passed to input  
method  
* QTBUG-93414 Qt Quick application stuck in a cursor update loop  
* QTBUG-95669 Clicking enter on some text fields it might freeze UI  
* QTBUG-96671 Android: Keyboard sometimes stuck and replacing previous  
letter  
* QTBUG-96675 Android: Cursor is shown in wrong place  
* QTBUG-96769 Android: keyboard input can get lost  
* QTBUG-96399 Crash with SIGSEGV in QXcbConnection::getSelectionOwner  
* QTBUG-94530 Disconnecting HDMI output causes application to crash  
* QTBUG-95300 [Regression] TextField goes behind soft keyboard on  
android  
* QTBUG-96117 Android soft keyboard no longer pans the screen  
* QTBUG-97503 Reg[5.15.2-5.15.6] Android: Keyboard covers the inputfield  
* QTBUG-97115 When an application that is using a background service is  
closed then it will cause an ANR after hanging for about 30 seconds  
* QTBUG-98569 Error in meta-b2qt for Windows Toolchain  
* QTBUG-92231 SSL handshake failure after ignoreSslErrors  
* QTBUG-84291 tst_QTimer::zeroTimer fails on Ubuntu 20.04  
* QTBUG-99036 [REG 5.15 → 6.3] QList(It, It) no longer works with pure  
input_iterators  
  
### qtsvg  
* QTBUG-96044 High memory consumption when rendering svg image  
* QTBUG-95891 svg file freezes QImage  
  
### qtdeclarative  
* QTBUG-94253 When an inputmask is set on a TextInput then it will  
overwrite the first character if the cursor starts from position 0 after  
typing the second character  
* QTBUG-94975 [ASAN] Heap-use-after-free in QOpenGLFramebufferObject  
* QTBUG-96796 qmlcache causes loading problem if the qml filename  
matches the name of some qml file from Qt package and has inline  
component  
* QTBUG-98032 QML/Javascript: Using an anonymous function as a default  
parameter in a function signature crashes the application.  
* QTBUG-98150 Designer puppet keeps crashing at startup in batch  
renderer  
* QTBUG-98248 SEGFAULT Crash in QQmlAnimationTimer::registerAnimation  
* QTBUG-95798 HoverHandler in delegate of Repeater keeps hovered state  
if model is changed  
* QTBUG-97792 Mixing OpenGL and Quick Controls lead to drawing errors in  
TextField  
* QTBUG-56075 QML Flickable: high-precision trackpad scrolling is too  
fast  
* QTBUG-98717 Setting HoverHandler cursorShape in a Window crashes  
* QTBUG-94765 AnimatedSprite has glitches  
* QTBUG-98722 SignalSpy.qml triggers a memory leak in the QML engine  
* QTBUG-82013 Crash handling wheel event  
* QTBUG-96112 Text tearing on text element when set inside parent  
element with noninteger y value  
* QTBUG-83626 When a Popup has an odd number for the width and/or height  
then texts inside it can be rendered badly  
* QTBUG-93956 The QSGBatchRenderer::Renderer's m_vertexUploadPool and  
m_indexUploadPool buffers never shrink  
* QTBUG-91033 Multiple extra compilers with same input are broken for VS  
projects  
* QTBUG-94806 Having Qmltypes in CONFIG leads to faulty vcxproj file  
* QTBUG-86187 Ubuntu 20.04 has InsignificantTests configurations in the  
CI  
* QTBUG-71360 Qml 'Shape' affects RectangluarGlow and other unrelated  
Items (NVIDIA)  
* QTBUG-86633 QML - letters randomly disappear when resizing label  
* QTBUG-97423 heap-use-after-free in SwipeView::test_orientation  
  
### qtmultimedia  
* QTBUG-93762 Memory leak in GStreamer Camerabinsession  
* QTBUG-89803 QML Video doesn't play on macOS 11.0 with Apple M1 chip  
* QTBUG-87000 When playing another video after having stopped the  
previous one can cause a flash of the previous video's frame showing  
before the new one is started  
  
### qttools  
* QTBUG-97104 macdeployqt fails when qmlimportscanner takes longer than  
30s  
  
### qtlocation  
* QTBUG-97722 Geoclue-2 plugin fails to report speed and direction  
* QTBUG-78705 No position updates occur if not permitted at startup on  
iOS, even if permissions change later  
  
### qtconnectivity  
* QTBUG-97900 Crash when connecting to Bluetooth device on macOS 12  
* QTBUG-96742 Timing issues in BTLE peripheral on Android  
* QTBUG-98073 cork board example crashes on android 12 device when  
targetSDK set to 31  
* QTBUG-98090 macOS examples that need special plist keys need their own  
plist files  
* QTBUG-97578 QT Bluetooth hang when scan services/characterictics  
* QTBUG-96557 Qt bluetooth can not scan device on Mac 12 beta  
* QTBUG-98351 Thread-safe Android BT LE Java implementation  
  
### qtwayland  
* QTBUG-97094 Wayland modifiers map decoding has flawed logic  
* QTBUG-95962 Wayland: Crash in XDG Shell when resizing window with  
mouse  
  
### qt3d  
* QTBUG-86493 ComputeCommand.trigger(1) executes compute shader more  
than 1 time  
* QTBUG-98421 tst_QChangeArbiter::distributePropertyChanges fails with  
Ubuntu 20.04 in Qt3d  
* QTBUG-99414 License.txt file not found under  
src/3rdparty/assimp/contrib/clipper  
  
### qtwebengine  
* QTBUG-96930 REG:5.15.3->5.15.4 - When doing a pinch gesture inside a  
WebEngineView then it has no effect  
* QTBUG-84105 Out-of-proc networking causes firewall confusion  
* QTBUG-98428 tst_QQuickWebEngineView fails with Ubuntu 20.04 in  
Webengine  
* QTBUG-90904 Crash on calling QAccessible::registerAccessibleInterface  
* QTBUG-98400 CVE-2021-3541 in chromium  
* QTBUG-98401 CVE-2021-3517 in chromium  
* QTBUG-95568 Possible deadlock at QtWebEngine Startup  
* QTBUG-94368 [QtPDF] bitcode bundle could not be generated because  
libQt5Pdf.a was built without full bitcode  
* QTBUG-94046 QtPDF: configuration with -static-runtime causes linker  
errors for projects  
* QTBUG-71611 [Windows] Suspending (sleep) the OS while a WebEngine app is executed leads to asserts in debug mode and rendering issues (frozen) in release  
* Fixed building and running with glibc > 2.33  
* Security fixes from Chromium up to version 96.0.4664.110, including:  
    - CVE-2021-4057: Use after free in file API  
    - CVE-2021-4058: Heap buffer overflow in ANGLE  
    - CVE-2021-4059: Insufficient data validation in loader  
    - CVE-2021-4062: Heap buffer overflow in BFCache  
    - CVE-2021-4078: Type confusion in V8  
    - CVE-2021-4079: Out of bounds write in WebRTC  
    - CVE-2021-4098: Insufficient data validation in Mojo  
    - CVE-2021-4099: Use after free in Swiftshader  
    - CVE-2021-4101: Heap buffer overflow in Swiftshader.  
    - CVE-2021-4102: Use after free in V8  
    - CVE-2021-37984 : Heap buffer overflow in PDFium  
    - CVE-2021-37987 : Use after free in Network APIs  
    - CVE-2021-37989 : Inappropriate implementation in Blink  
    - CVE-2021-37992 : Out of bounds read in WebAudio  
    - CVE-2021-37993 : Use after free in PDF Accessibility  
    - CVE-2021-37996 : Insufficient validation of untrusted input in Downloads  
    - CVE-2021-38001 : Type Confusion in V8  
    - CVE-2021-38003 : Inappropriate implementation in V8  
    - CVE-2021-38005: Use after free in loader  
    - CVE-2021-38007: Type Confusion in V8  
    - CVE-2021-38009: Inappropriate implementation in cache  
    - CVE-2021-38010: Inappropriate implementation in service workers  
    - CVE-2021-38012: Type Confusion in V8  
    - CVE-2021-38015: Inappropriate implementation in input  
    - CVE-2021-38017: Insufficient policy enforcement in iframe sandbox  
    - CVE-2021-38018: Inappropriate implementation in navigation  
    - CVE-2021-38019: Insufficient policy enforcement in CORS  
    - CVE-2021-38021: Inappropriate implementation in referrer  
    - CVE-2021-38022: Inappropriate implementation in WebAuthentication  
    - Security bug 1245870  
    - Security bug 1252858  
    - Security bug 1259899  
  
### qtquickcontrols2  
* QTBUG-85956 QQuickPopupPrivate::finalizeExitTransition() not giving  
focus to the highest-z Dialog with focus = true  
* QTBUG-85918 Focus set to wrong dialog in case of enter transition  
* QTBUG-86854 When a Tooltip is visible then it is possible to interact  
with a window that is underneath a modal dialog although it should be  
blocking the input to it  
* QTBUG-98482 RangeSlider does not update position/visualPosition based  
on from/to changes  
* QTBUG-97075 [REG: 5.14.2->5.15.0] Anchors don't work with InputPanel  
anymore  
  
### qtpurchasing  
* QTBUG-98053 [REG: 5.15.6->5.15.7] Qt Purchasing crashes on Android  
* QTBUG-98542 new purchasing is broken on Android when using public key  
verification  
  
### qtcharts  
* QTBUG-95870 Setting plotArea for a ChartView in a layout is not  
respected  
* QTBUG-81278 Switching axis that is shared by multiple series to  
another doesn't work  
* QTBUG-98282 QPieSlice label does not indicate it takes html formatted  
text  
  
### qtdatavis3d  
* QTBUG-98425 tst_proxy::multiMatch fail with Ubuntu 20.04 in  
qtdatavis3d  
  
### qtvirtualkeyboard  
* QTBUG-97075 [REG: 5.14.2->5.15.0] Anchors don't work with InputPanel  
anymore  
* QTBUG-56918 When the keyboard is shown for a text field in a modal  
popup then it will not be usable  
* QTBUG-92881 InputPanels defaults z value should be lower than max  
value for overlays  
* QTBUG-96578 Virtual Keyboard Deployment guide does not cover widget  
applications  
* QTBUG-97830 Some Qt Virtual Keyboard tests checking the position of  
selection handles are failing  
  
### qtremoteobjects  
* QTBUG-91041 Remote Objects: Model headers are not updated  
* QTBUG-97688 Clients don't reconnect to replaced nodes over TCP  
  
### qtquick3d  
* QTBUG-97714 Memory leak with Quick3D 5.15 when loading Texture with  
Loader  
  
Known Issues  
------------  
  
* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-5.15/supported-platforms.html  
  
* The RTA (release test automation) reported issues in Qt 5.15.x:  
https://bugreports.qt.io/issues/?filter=21874  
  
* Qt 5.15.8 Open issues in Jira:
https://bugreports.qt.io/issues/?filter=24447
  
  
### Linux..
* QTCREATORBUG-26167 QtC 6.0.0 not launching on Ubuntu 18.04  
* QTCREATORBUG-26811 Installer error on RHEL7.6 (CXXABI/GLIBCXX version issue)  
Qt Creator 6.x.x does not support (K)Ubuntu Linux 18.04.  
For more information, see  
https://doc.qt.io/qtcreator/creator-desktop-platforms.html#linux.  
  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Laszlo Agocs  
Dimitrios Apostolou  
Eskil Abrahamsen Blomfeldt  
Joerg Bornemann  
Assam Boudjelthia  
Andreas Buhr  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Rodney Dawes  
Alexey Edelev  
Christian Ehrlicher  
Hatem ElKharashy  
David Faure  
Samuel Gaist  
Andrei Golubev  
Tang Haixiang  
Zhang Hao  
Jani Heikkinen  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Dominik Holland  
Allan Sandfeld Jensen  
Friedemann Kleint  
Michal Klocek  
Lars Knoll  
Jarek Kobus  
Jarkko Koivikko  
Tomi Korpipaa  
Jani Korteniemi  
Fabian Kosmale  
Mike Krus  
Sona Kurazyan  
Kai Köhne  
Inho Lee  
Paul Lemire  
Ievgenii Meshcheriakov  
Marc Mutz  
Antti Määttä  
Andy Nichols  
Mårten Nordheim  
Samuli Piippo  
Timur Pocheptsov  
Joni Poikelin  
Rami Potinkara  
Lorn Potter  
Liang Qi  
Topi Reinio  
André de la Rocha  
Fan RuiJie  
Shawn Rutledge  
Andy Shaw  
Ivan Solovev  
Tarja Sundqvist  
Morten Johan Sørvig  
Samuel Thibault  
Paul Olav Tvete  
Sami Varanka  
Doris Verria  
Tor Arne Vestbø  
Alexander Volkov  
Juha Vuolle  
Bernd Weimer  
Edward Welbourne  
Marianne Yrjänä  
