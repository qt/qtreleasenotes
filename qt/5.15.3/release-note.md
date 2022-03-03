Release note  
============  
  
Qt 5.15.3 release is a patch release made on the top of Qt 5.15.2. As a patch  
release, Qt 5.15.3 does not add any new functionality but provides bug fixes  
and other improvements.  
  
For detailed information about Qt, see the Qt 5.15 online documentation:  
https://doc.qt.io/qt-5/index.html.  
  
  
Important Changes  
-----------------  
  
### qtbase  
* 6485b6d45a Fix allocated memory of QByteArray returned by  
QIODevice::readLine  
Fixes a regression in Qt 5.15 causing the QByteArray returned by  
QIODevice::readLine() to consume large amounts of memory.  
  
* 5425305597 Update CLDR to v37, adding Nigerian Pidgin as a new  
language  
Updated to new version of CLDR (the Unicode Consortium's Common Locale  
Data Repository) v37. Various Adlam-script locales are dropped due to  
its use of a number system unsupported by 5.15's QLocale. Support for  
these locales shall be restored in Qt 6.  
  
* f1f650dc3a Deprecate ordering on QItemSelectionRange  
Ordering of QItemSelectionRange is now deprecated. It was not  
consistent with equality and should not be needed.  
  
* b8518414c3 Deprecate QLocale::Language entries that no locale data  
relates to  
Many obsolete language names are now deprecated in preparation for  
removal at Qt 6.0. No data has been available for any locale using these  
languages since CLDR v29 (at least; Qt now uses v37).  
  
* 9fbc5f1489 Deprecate old aliases for two countries and several  
languages  
Deprecated several Language and Country aliases, ready for removal in  
Qt 6.0, in favor of their newer names.  
  
* 1a991e1862 Fix delay first time a font is used  
Fixed an issue where on some platforms, there would be a delay the  
first time any font was used, sometimes causing a visible delay in the  
UI.  
  
* 5f935eeed4 Update third-party md4c to version 0.4.6  
md4c was updated to 0.4.6.  
  
* 6d306a0e37 Fix shaping problems on iOS 14 / macOS 11  
Fixed shaping of default UI font on macOS 11 and iOS 14.  
  
* 720304f703 Be more consistent when converting JSON values from variant  
Restored pre-5.15.0 behavior when converting from numeric QVariant  
values to QJson* types. Such values now always convert to a double  
QJsonValue.  
  
* bb8522682d Avoid integer overflow and division by zero  
Pen patterns are restrained to a maximum length and values of 1024,  
fixing oss-fuzz issue 25310.  
  
* c39fd63d71 Return a more useful date-time on parser failure in spring-  
forward gap  
Restored pre-5.15.0 behavior when parsing a date-time from a string  
(and document what it implies): if the string has the right form but  
represents a date-time that was skipped by a time-zone transition (e.g.  
a DST spring-forward), the invalid date-time object returned can, none  
the less, be used to recover a near-by date-time that may be more useful  
in some cases. From 5.15.0 to 5.15.2 and in 6.0.0, a default-constructed  
QDateTime was returned in place of this more informative invalid date-  
time.  
  
* 76671a57b5 Containers: call constructors even for primitive types  
The semantics of Q_PRIMITIVE_TYPE have been slightly changed. Qt now  
value-initializes types marked as primitive (which, by default, include  
trivial types) instead of simply using memset(0), which is wrong in some  
corner cases.  
  
* f4152d268e QSslSocket::verify: do not alter the default configuration  
QSslSocket::verify - do not change the default configuration  
  
* cf797c611d PCRE: update to 10.36  
PCRE2 has been updated to version 10.36.  
  
* be0301b42f QString: fix count(QRegularExpression)  
Fixed a corner case when using QString::count(QRegularExpression),  
causing an empty match in the last position not to be accounted for in the  
returned result.  
  
* 0ce98b1cf8 Fix qt_alphaVersion and qt_opaqueVersion in the trivial  
case  
Opaque pixmaps on devices with a non-standard opaque format will now  
correctly match format for faster blitting. Same with semitransparent  
pixmaps on devices with a non-standard semitransparent format.  
  
* 6146f4553b SQLite: Update to 3.34.0  
Updated to 3.34.0  
  
* 4cec3ecd2d Change QLineF::setLength() to work whenever length() is  
non-zero  
QLineF::setLength() will now set the length if the line's length() is  
non-zero. Previously, it was documented to only set the length if  
isNull() was false; this is a fuzzy check, so isNull() could be true for  
a line with non-zero length().  
  
* 39c1c54e0c Fix problems with offset-derived ids for QTimeZone  
QTimeZone instances created by offset from UTC (in seconds) shall now  
only include minutes in their ID when the offset is not a whole number  
of hours. They shall also include the seconds in their ID when the  
offset is not a whole number of minutes.  
  
* 99d3a65cf3 Use design metrics when adding text to QPainterPath  
Fixed an issue where QPainterPath::addText() would get inconsistent  
kerning for smaller font sizes when hinting is enabled.  
  
* dbaac6e5c1 Remove false Q_UNREACHABLE from shaping code  
Fixed a possible crash with certain fonts when shaping strings  
consisting only of control characters.  
  
* 6a64b8ed56 Fix crash when requesting A32 glyph on Wayland  
Fixed crash when calling QRawFont::alphaMapForGlyph() with subpixel  
antialiasing on Wayland.  
  
### qtdeclarative  
* e203a185cf doc: explain QQItem event delivery, handlers,  
setAcceptTouchEvents()  
When subclassing QQuickItem, you should call setAcceptTouchEvents(true)  
if you need the item to receive touch events. It will be required in Qt  
6.  
  
### qtlocation  
* 6b1dc419 Allow removal of layers and sources created using parameters  
in MapboxGL  
Sources and layers from parameters can be removed  
  
### qtwayland  
* a8d35b3c Fix leaked subsurface wayland items  
Fixed a memory leak when creating subsurfaces.  
  
* adc364c9 Fix memory leak in QWaylandGLContext  
Fixed a memory leak when creating QOpenGLContexts on Wayland and using  
the wayland-egl backend.  
  
### qtwebengine  
* node.js is now a hard build-time dependency  
  
* More chrome WebUIs made accessible  
(chrome://tracing, chrome://webrtc-logs, chrome://user-actions)  
  
* Added support for running in Rosetta2 on ARM macs [QTBUG-86406]  
  
* Fixed screen sharing on Google Meet by supporting the Chrome hangout  
extension [QTBUG-85731]  
  
* The Chromium version has been updated to 87.0.4280.144  
 - Security fixes from Chromium up to version 88.0.4324.150, including:  
- CVE-2020-16044: Use after free in WebRTC  
- CVE-2021-21118: Insufficient data validation in V8  
- CVE-2021-21119: Use after free in Media  
- CVE-2021-21120: Use after free in WebSQL  
- CVE-2021-21121: Use after free in Omnibox  
- CVE-2021-21122: Use after free in Blink  
- CVE-2021-21123, CVE-2021-21125, CVE-2021-21129,CVE-2021-21130,  
CVE-2021-21131, CVE-2021-21141:  
Insufficient data validation in File System API  
- CVE-2021-21126: Insufficient policy enforcement in extensions  
- CVE-2021-21127: Insufficient policy enforcement in extensions  
- CVE-2021-21128: Heap buffer overflow in Blink  
- CVE-2021-21132: Inappropriate implementation in DevTools  
- CVE-2021-21135: Inappropriate implementation in Performance API  
- CVE-2021-21137: Inappropriate implementation in DevTools  
- CVE-2021-21140: Uninitialized Use in USB  
- CVE-2021-21145: Use after free in Fonts  
- CVE-2021-21146: Use after free in Navigation  
- CVE-2021-21147: Inappropriate implementation in Skia  
- CVE-2021-21148: Heap buffer overflow in V8  
- CVE-2021-21149: Stack overflow in Data Transfer  
- CVE-2021-21150: Use after free in Downloads  
- CVE-2021-21152: Heap buffer overflow in Media  
- CVE-2021-21153: Stack overflow in GPU Process  
- CVE-2021-21156: Heap buffer overflow in V8  
- CVE-2021-21157: Use after free in Web Sockets  
- Security bug 937131  
- Security bug 1097499  
- Security bug 1127774  
- Security bug 1135594  
- Security bug 1144646  
- Security bug 1161654  
- Security bug 1162198  
- Security bug 1171954  
- WebRTC bug 12105  
  
* ed8fe2b3 Fix QtWebEngineProcess.exe build on windows to include  
version resources  
Fix missing version resources in QtWebEngineProcess.exe.  
  
* 2b6f6ad0 Enable hangout services extension  
Enable hangout services extension and implement its WebRTC desktop  
capture extension API dependency.  
  
### qtquickcontrols2  
* 5f6133aac Reset the opacity and scale properties after the exit  
transition  
After the exit transition is finished, then the opacity and scale  
properties will be reset to their values before the enter transition is  
started.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-87010 lconvert uses huge amounts of RAM  
* QTBUG-87621 Selftest failure with CentOS 8.1 during qtbase tests  
* QTBUG-71737 Font family fallback cache results in startup lag on  
Windows  
* QTBUG-85090 QLineEdit with PasswordEchoOnEdit removes the first  
entered character after second  
* QTBUG-86733 [Android] NoSuchMethodException when using QtMultimedia  
* QTBUG-82978 Allow "-Wextra-semi-stmt" on Q_UNUSED  
* QTBUG-87706 QPushButton click is not working when Margin is set via  
styleheet  
* QTBUG-67515 MinGW: process fails with wildcards under windows command  
prompt: ASSERT: "allArguments.size() == d->origArgc" in file  
kernel/qcoreapplication.cpp, line 2362  
* QTBUG-84002 Qt detects Unicode command line arguments as question  
marks  
* QTBUG-81533 StyleSheet is ignored when changing a QComboBox to be  
editable  
* QTBUG-81866 Android, wrong libraries added as ANDROID_EXTRA_LIBS for  
armeabi-v7a  
* QTBUG-84849 Android application crash  
* QTBUG-87965 [REG 5.15.1 -> 6.0] Crash in QTextDocument().setMarkdown()  
* QTBUG-88125 [REG: 5.12->5.15]Error processing an enumeration type  
containing the include directive  
* QTBUG-88016 click Scence inputMethod does not disAppear when preview  
input chinese while use QGraphicsProxyWidget  
* QTBUG-84643 QMenu crashes when released  
* QTBUG-88185 QMapNode and strict-aliasing  
* QTBUG-60793 Rich Text, html still fail to find high-dpi images  
* QTBUG-87307 processEvents behavior inconsistend with documentation  
* QTBUG-84291 tst_QTimer::zeroTimer fails on Ubuntu 20.04  
* QTBUG-88227 QDirIterator (Windows) should be case insensitive but not  
* QTBUG-82626 Cmd-H Doesn't Hide App When Tooltip Displayed  
* QTBUG-88295 Incorrect configure output when passing -system-pcre  
* QTBUG-88076 Crash on Android 6  
* QTBUG-88247 Memory ordering problem in QBasicMutex::lockInternal()  
* QTBUG-87627 Android java res folder is not copied over on Windows for  
-developer-build  
* QTBUG-88431 QT_NO_CAST_FROM_ASCII can break code without warning with  
QCharRef::operator=(*) and char > 127  
* QTBUG-72110 MouseArea stops responding  
* QTBUG-87984 QTransform reports type TxRotate instead of TxShear for  
shear transforms  
* QTBUG-88309 QGraphicsItem crash if click right button of mouse  
* QTBUG-69159 Android: tst_QWindow::initialSize fails  
* QTBUG-69156 Android: tst_QWindow::childWindowPositioning(show) fails  
* QTBUG-69154 Android: tst_QWindow::setVisible fails  
* QTBUG-87014 Qt application gets stuck trying to open main window under  
Big Sur  
* QTBUG-88495 Text rendering: spaces are rendered incorrectly on macOS  
Big Sur after commas, dots.  
* QTBUG-85749 QGradient Preset enum not in documentation  
* QTBUG-86976 Input method widget is closed on destructing a widget  
* QTBUG-88600 SystemTrayIcon icon too big /squashed on second screen  
(Big Sur)  
* QTBUG-88168 QJsonObject::fromVariantMap converts ulonglong variant to  
signed  
* QTBUG-88653 QEventLoop::processEvents does not take the timeout into  
account as expected  
* QTBUG-87781 QSortFilterProxyModel does not emit dataChanged when  
calling setSourceModel() after modifying the source model  
* QTBUG-77320 QAccessible::isActive on Android incorrectly returns false  
* QTBUG-85644 defaulted default constructor cannot be constexpr because  
the corresponding implicitly declared default constructor would not be  
constexpr  
* QTBUG-85361 When a dialog has a resize grip handle then it is not  
possible to resize with it  
* QTBUG-86857 QPushButton style "text-align: bottom" not working in Qt  
5.15.1  
* QTBUG-88952 Implicit conversion QGuiApplication  
* QTBUG-86850 QSortFilterModel forwards dataChanged() when the source  
model changes data incolumns that the filter model refuses  
* QTBUG-88656 Undefined behavior in QDateTime::fromString  
* QTBUG-87740 tst_networkselftest is still dependent on qt-test-server  
* QTBUG-88435 QXcbConnection::getTimestamp runs in indefinite loop when  
X server shuts down  
* QTBUG-88688 Qt application fails to start on Debian 10 Buster because  
libqxcb.so requires missing libxcb-util.so.1  
* QTBUG-86287 Static 5.15.0 compile results in "undefined reference to  
xcb_aux_create_gc"  
* QTBUG-88238 [REG] qsslkey autotest has compile error when QT_NO_SSL is  
defined  
* QTBUG-85712 WebAssembly: RoundButton has odd behaviour on repeated  
clicks  
* QTBUG-88417 tst_qnetworkreply authenticationCacheAfterCancel fails on  
Ubuntu 20.04  
* QTBUG-86179 QTranslator::load() search order doesn't follow  
uiLanguages order  
* QTBUG-88825 Undefined behavior in moc  
* QTBUG-88639 QSslConfiguration::setCaCertificates() does not disable  
system certificates  
* QTBUG-89008 tst_QFontDatabase::aliases() failed on openSUSE 15.2  
* QTBUG-89118 style animated scroll bars might freeze(stop animating) if  
we do a heavy paint event  
* QTBUG-88188 Cannot click to select an item in a QTreeWidget  
* QTBUG-88985 Context QMenu without parent blocked by modal dialog on  
macOS  
* QTBUG-87849 QLineEdit completion in QDialog is not clickable  
* QTBUG-86845 [Reg5.14->5.15.1]Item selection in Custom popup menu in  
QComboBox stopped working in 5.15.1  
* QTBUG-89059 Mac: Missing namespace mangling in corelib/kernel  
* QTBUG-88982 QSplashScreen missing QPainter::SmoothPixmapTransform  
* QTBUG-89281 Android apps don't include QML modules  
* QTBUG-83457 secureupdclient example crashes  
* QTBUG-85683 Windows: "Unable to enumerate family" for fonts with  
lengthy family name  
* QTBUG-85621 Lower color depths don't seem to be handled correctly in  
VNC QPA  
* QTBUG-89915 MediaPlayPause key incorrectly reported as MediaPlay  
* QTBUG-85846 Top level QTextEdit looses cursor  after right mouse click  
to show context menu  
* QTBUG-90246 QImage::scale doesn't work for Format_Grayscale16 images  
* QTBUG-89130 setLibraryPaths keeps the applications directory in path,  
docs should mention it  
* QTBUG-86632 QCombobox text elide doesnot work with fusion style  
* QTBUG-89599 Performance regression in QTextDocument in 5.15  
* QTBUG-20354 Disappearing lines when using a syntax highlighter  
* QTBUG-89812 OpenGLWidget in QDockWidget not painted when flaoting  
* QTBUG-88230 When the display is set to 200% then the icons used for  
the close button in a QTabBar are too small in comparison to the text  
* QTBUG-90354 Failed to build Qt Core on dev on 32 bit system  
* QTBUG-87107 QFontMetricsF::boundingRect handles a null QRectF  
differently when passed in as it does not constrain to the size of it  
* QTBUG-89709 Broken link in QMatrix4x4 docs  
* QTBUG-84575 QCalendar class is not reentrant  
* QTBUG-88815 QDate::FromString breaks when accessed from multiple  
threads using default calendar parameter  
* QTBUG-85692 Race in QTime::toString  
* QTBUG-85791 Vulkan Validation Error VUID-VkSwapchainCreateInfoKHR-  
minImageCount-01271  
* QTBUG-90350 Could not close DRM (NV) device (Bad file descriptor).  
* QTBUG-86582 REG 5.13->5.14: Segfault upon close and then show  
* QTBUG-85715 Android: Problem entering IP address with Samsung Number  
and regex validator  
* QTBUG-65229 [Android] Text select handle misplaced on fields inside  
QDialog  
* QTBUG-58503 Text Handle Cursor Position Offset Error  
* QTBUG-89815 [Reg 5.11->5.12.2] Wrong color for placeholder text for  
QLineEdit if disabled in constructor of parent  
* QTBUG-73286 QODBC driver doesn't count decimal point when calculate  
string length for NUMERIC type with QSql::HighPrecision  
numericalPrecisionPolicy  
* QTBUG-89846 QObject::dumpObjectInfo might segfault  
* QTBUG-74088 Menu Bar Items Disabled When QMainWindow Has Window Modal  
Child and Another Window Made Active  
* QTBUG-79147 Windows: QColorDialog displays at wrong position when  
reshowing after closing via title bar  
* QTBUG-90595 QCombobox placeholderText not visible  
* QTBUG-86898 [REG 5.14->5.15] QTabBar last tab incorrectly styled after  
insertTab  
* QTBUG-89133 Button with focus looks wrong in macOS Big Sur for  
QMessageBox  
* QTBUG-81452 QPushButton has empty space in layout  
* QTBUG-88715 QComboBox DropDown items are displayed very closed to its  
right edge.  
* QTBUG-81097 When the tab order is explicitly set then Backtabbing  
might not work correctly  
* QTBUG-90716 QGuiApplication::primaryScreen() not returning the correct  
screen if the user changes their main display.  
* QTBUG-89361 QPlatformScreen::logicalDpi crashes with  
QPlatformPlaceholderScreen  
* QTBUG-75319 [REG 5.12.1 -> 5.12.2] QApplication::clipboard()->text()  
call blocks execution for ~5 seconds sometimes  
* QTBUG-80298 iOS: edit menu shows while selecting text  
* QTBUG-90332 iOS: edit menu doesn't hide when tapping on screen  
* QTBUG-89172 Integer-overflow in QFixed::fromReal(qreal r) through  
QImage::.loadFromData(QByteArray);  
* QTBUG-89910 The default font resolution of a QWidget subclass is  
random w.r.t. QApplication::font  
* QTBUG-39791 QFileDialog::DontConfirmOverwrite option does not work  
when OS X App is sandboxed  
* QTBUG-90628 [REG: 5.14.2->5.15.0]: When resizing a window that is  
translucent and using stylesheets then this can flicker quite a lot when  
the window is resized smaller  
* QTBUG-86960 QDateTime at beginning of DST is created wrongly with  
recent glibc  
* QTBUG-89208 tst_QDateTimeEdit::springForward() failed on openSUSE 15.2  
in CI  
* QTBUG-89547 Comparison of QSslCertificate broken (extensions()  
crashes)  
* QTBUG-89899 Integer-overflow in QFixed::QFixed  
* QTBUG-89184 Unicode key mappings are not working in all Qt based  
applications  
* QTBUG-90743 iOS: edit menu and magnifier glass is showing  
simultaneously  
* QTBUG-90553 tst_QDateTime::timeZones fails with glibc 2.31 on Clear  
Linux  
* QTBUG-85556 QProxyStyle will not work properly with another proxy  
style as a baseStyle  
* QTBUG-86518 QSystemTrayIcon menu is not opened on press  
* QTBUG-89569 [REG] Division by 0 in QLineF::setLength()  
* QTBUG-89905 QTimeZone IANA id broken on Android  
* QTBUG-69122 Android: tst_QTimeZone::dataStreamTest fails  
* QTBUG-69132 Android: tst_QTimeZone::transitionEachZone crashes for a  
few cases  
* QTBUG-87435 tst_QTimeZone::createTest fails on Android  
* QTBUG-88610 [Android] JNI crash at QTimeZone::systemTimeZone  
(Regression?)  
* QTBUG-83056 Stylesheet with pseudo state on QTextBrowser does not work  
* QTBUG-90242 QMenu stylesheet has alignment issue when one item has  
icon/checkable  
* QTBUG-89578 QLineEdit Cursor show white line when use property of  
setInputMask  
* QTBUG-75106 Entries in the QAccessiblePluginsHash should be removed  
when a QQuickWindow is deleted  
* QTBUG-89647 ARM OpenSSL DLLs for Windows are not found due to missing  
suffix  
* QTBUG-85484 [Reg. 5.14->5.15]Resize Widget inside QTableWidget  
* QTBUG-20900 QPainterPath::addText has incorrect font spacing on  
Windows only  
* QTBUG-86776 QComboBox showPopup doesn't select all columns of an item  
* QTBUG-85547 macOS/Catalina: Modal File Dialog Save-Replace Always  
Rejected  
* QTBUG-89959 Saving a new file fails on Big Sur (11.1)  
* QTBUG-89625 QJsonObject The take function caused an error!!  
* QTBUG-90775 Documentation incorrect for QDateTime  
* QTBUG-90395 FTBFS: qendian.h missing <limits> include  
* QTBUG-89155 Assertion violation in text shaping on special string with  
EmojiOneColor font.  
* QTBUG-90860 [iOS] The edit menu doesn't hide when typing on the input  
panel  
* QTBUG-84616  Mac Checkbox Accessibility does not returns mixed State  
* QTBUG-85787 [Android] TextField password becomes visible  
* QTBUG-90236 QRawFont::alphaMapForGlyph() shows garbage and eventually  
leads to crash  
* QTBUG-88984 Memory leak in QPSQLDriver when connection is lost before  
the connection could be closed  
* QTBUG-84737 When using Qt NFC to scan NFC tags it will not work when  
the application is first started  
* QTBUG-90801 QMake: if you #include a C file from another C file, the  
original file no make target is created  
* QTBUG-88758 Building vcprojects fails with Qt  
* QTBUG-91033 Multiple extra compilers with same input are broken for VS  
projects  
* QTBUG-90963 QDoc manual has overlapping captions with images  
* QTBUG-88198 Documentation needs updates regarding ODBC SQL types  
* QTBUG-88512 Use-after-free in QXcbConnection::initializeScreens()  
* QTBUG-87227 Tooltips are not working  
* QTBUG-91038 tst_QTextLayout::longText failures  
* QTBUG-75630 QPainter drops e.g. lines using small (< 1e-12) user world  
coords  
* QTBUG-90937 [iOS] edit menu stays open after changing focus  
* QTBUG-90625 subset of downloads stall and die with connection closed  
on some systems  
* QTVSADDINBUG-819 Qt_INCLUDEPATH_ not defined  
* QTBUG-76902 Widgets and fonts have wrong size after moving to screen  
due to disconnect with different DPI when dpiawareness = 2  
* QTBUG-87601 Incorrect qmake output with 'vc' template  
* QTBUG-84096 FreeType: crash with unicode Variation Selector-16  
* QTBUG-88063 Memory leak in QNetworkAccessManager from  
QMetaObjectPrivate::connect  
* QTBUG-85139 QTextDocument::setMarkdown slow on certain input  
* QTCREATORBUG-24674 When the kit is changed to be an Android one then  
it will add an entry for ANDROID_ABIS into the pro file even if it is  
not needed  
* QTBUG-87154 Add static dependencies from 3rdparty in qtbase  
* QTBUG-88633 Generating QDateTime with invalid transition hour is no  
more possible  
* QTBUG-68338 Qt shouldn't create or change the permission of  
XDG_RUNTIME_DIR  
* QTBUG-81687 Pasting text on android broken when copied from TextEdit  
* QTBUG-87803  
QStandardPaths::writableLocation(QStandardPaths::GenericDataLocation)  
points to an inaccessible location  
* QTBUG-79611 QAccessible::notifyAccessibilityUpdate not implemented on  
Android  
* QTBUG-86785 Qt fails to build from source for single-arch Android  
x86_64  
* QTBUG-41343 tst_qmdiarea fails on Mac OS X  
* QTBUG-90441 Update to 20H2 broke auto test for winrt  
* QTBUG-86368 QQmlContext leak when connecting to and destroying  
dynamically created object  
* QTBUG-85869 Black screen in QtOpenGL apps under Xvnc4 when using Mesa  
with Gallium or XLib drivers  
* QTBUG-90016 tst_QListView::internalDragDropMove(list, model doesn't  
move, replace item) causes fails in CI  
* QTBUG-89354 When the native virtual keyboard shows up, it does not  
shift the Qt Quick Window up in order to show where the cursor is in the  
text input field  
* QTBUG-89896 Example: undoframework. The background is not displayed  
* QTBUG-59879 X selection clipboard (PRIMARY buffer) should be set by  
keyboard selection too  
* QTBUG-85226 Reg->5.15 [Vista Style]QStyle::standardPalette returns  
empty QPalette  
  
### qtdeclarative  
* QTBUG-85713 Inline components trigger assertion with ListElement  
* QTBUG-87464 Inline component state issue  
* QTBUG-85379 Crash when changing enabled state of Button in onPressed  
when using Material style  
* QTBUG-88033 [integrity] static release build fails to register QML  
plugins  
* QTBUG-87150 QML_FOREIGN needs clearer documentation to indicate that  
it is using the name of the struct or QML_NAMED_ELEMENT  
* QTBUG-87228 When running Valgrind/Leak Sanitizer there are indications  
that there are problems with the property cache  
* QTBUG-88807 direct memory leak in qquicktextinput.cpp  
* QTBUG-88786 Crash when calling hasOwnProperty() on a JS Proxy Object  
* QTBUG-85888 Qml *.qmltypes files are incomplete for android  
* QTBUG-87117 plugins.qmltypes incorrectly generated due to foreign  
types path  
* QTBUG-83599 Signal parameter referenced in a JS closure is undefined  
while QML debugger is attached  
* QTBUG-89173 Adding an object with a null property in a nested object  
in an array crashes QQmlListModel::append  
* QTBUG-87526 QML HorizontalHeaderView does not show up if rowcount in  
Tablemodel is 0  
* QDS-3301 Resetting scale and pivot values for 3D models doesn't update  
3D Editor  
* QTBUG-86323 Iterating over Properties of a Proxied Object does not  
work  
* QTBUG-89513 Generating JIT code crashes QML app  
* QTBUG-83895 QML Loader forgets source parameters after "active" change  
* QTBUG-85103 Qml Shape as Button's background  doesn't manage well  
transparent color  
* QTBUG-83408 Text disappears with ElideRight.  
* QTBUG-33608 Elide property of Text breaks component resizing  
* QTBUG-85106 Crash when restoring/apply PropertyChanges during a  
StateMachine state change in certain cases  
* QTBUG-89898 REG 5.15.0 - > 5.15.1 clip: true with rotation asserts  
* QTBUG-83108 Only clear the area that updates stencil buffer  
* QTBUG-87253 Quick Layout causes crash if child item  
Layout.preferredWidth bound to the Layouts width  
* QTBUG-86567 When destroying an item in a model that has an animation  
running as part of its delegate then it can cause a crash to occur  
* QTBUG-89738 QDoc: Formatting errors on Creating C++ Plugins for QML  
page  
* QTBUG-90538 "required" existing property not reflects model data if  
CONFIG+=qtquickcompiler enabled  
* QTBUG-72757 iOS: Text input cursor moving incorrect with using  
magnifying glass  
* QTBUG-88682 Not able to trigger "Alt+Enter" shortcut  
* QTBUG-89203 qtdeclarative build error due to 'trunc' already defined  
when doing a static build on Windows  
* QTBUG-89955 Ambiguous string comparison in QML Plugin Dumper  
* QTBUG-90489 Segfault in QQuickWindowIncubationController when  
accessing QSGRenderLoop on Application shutdown  
* QTBUG-84458 QML Text doesn't reset lineCount when text is empty  
* QTBUG-79611 QAccessible::notifyAccessibilityUpdate not implemented on  
Android  
* QTBUG-87018 Touch/mouse-related test failures in qtquickcontrols2  
* QTBUG-87082 explain input event handling better in the docs  
* QTBUG-89889 tst_QDateTime::systemTimeZoneChange fails on 32bit systems  
* QTBUG-89659 Crash in with JITting enabled  
* QTBUG-90401 Heap-use-after-free in QAbstractAnimationJob  
* QTBUG-75042 [Accesssibility] Qt Quick Control 2 Dialog parts (title,  
body, footer) are read in wrong order  
* QTBUG-90676 tst_EcmaScriptTests::runJitted() Received a fatal error  
* QTBUG-85557 When doing a sort on a ListModel in a WorkerScript then  
after syncing the ListView does not show the updated model  
  
### qtmultimedia  
* QTBUG-90997 simple spell error in QMediaPlayer documentation  
* QTBUG-91154 qtmultimedia build fails without gstreamer  
  
### qttools  
* QTBUG-86192 QT5_CREATE_TRANSLATION doesn't set directory dependencies  
correctly  
* QTBUG-81596 QDoc doesn't parse JSON files correctly  
* QTBUG-84224 qdoc: DocBook: Incomplete content generated for  
\headerfile  
* QTBUG-86101 [REG] Wrong help page gets opened  
* QTBUG-88603 qdoc: Excess warnings about undocumented namespaces  
* QTBUG-89835 qdoc: Group links missing from the navigation bar  
* QTBUG-85572 Documentation errors in SwipeDelegate QML  
* QTBUG-90691 Qdoc generates an empty TOC for a \qmlbasictype page with  
members  
* QTBUG-89980 Tools (Assistant, Designer, Linguist) copyright still 2020  
* QTBUG-90867 qdoc: Warning limit has no effect in single-exec mode  
* QTBUG-87058 qtpaths --types does not support all values provided by  
QStandardPaths  
* QTBUG-88167 ../shared/numerus.cpp:165:5: error: ‘Bihari’ is not a  
member of ‘QLocale’  
* QTBUG-71354 Qt5LinguistTools CMake scripts don't declare BYPRODUCTS  
* QTBUG-62697 qhc files cannot be created in a reproducible way  
  
### qttranslations  
* QTBUG-81089 Translation in Italian  
  
### qtdoc  
* QTBUG-90640 examples-android.html links to invalid Creating a Mobile  
Application page  
* QTBUG-90921 Wrong destination link for Qt for DC in doc.qt.io  
* QTBUG-87959 The Wayland license should be GPL not LGPL  
  
### qtlocation  
* QTBUG-85260 QSG Render Thread crash  
* QTBUG-88017 qdeclarativepolylinemapitem has errors in it  
* QTBUG-90244 declarative_core::ReviewModel::test_reset fails on CI  
  
### qtsensors  
* QTBUG-77423 QRotationSensor reporting invalid values  
  
### qtconnectivity  
* QTBUG-82407 No error signal is emitted with latest Bluez version  
  
### qtwayland  
* QTBUG-87959 The Wayland license should be GPL not LGPL  
* QTBUG-87762 [Wayland] The usage of setFixedSize on a window is not  
properly scaled by QT_SCALE_FACTOR  
* QTBUG-88277 Do not try to eglMakeCurrent for unintended case  
* QTBUG-88064 Setting window size in Qml is not scaled correctly on  
Wayland  
* QTBUG-85608 Qt5.15, it created 2 more commandbuffer. but they were not  
freed.  
* QTBUG-87597 Race conditions/improper texture handling in multi-screen  
wayland compositor  
* QTBUG-88782 Wayland compositor memory leak  
  
### qt3d  
* QTBUG-88821 [REG: 5.15.1->5.15.2] Assimp plugin is only built for gcc  
* QTBUG-64110 Parameter prioritization doesn't match documentation  
  
### qtquickcontrols  
* QTBUG-62239 FontDialog looks ugly  
* QTBUG-62240 FontDialog doesn't support RTL  
  
### qtserialbus  
* QTBUG-89066 Setting CAN bus bitrate with socketcan returns error  
  
### qtwinextras  
* QTBUG-90351 tst_QWinJumpList::testRecent fails with Windows 7  
  
### qtwebsockets  
* QTBUG-88663 Qt WebSocket by default loads all system certificates even  
SSL is not used  
* QTBUG-88923 Websocket reading error on reconnect  
  
### qtwebengine  
* QTBUG-88110 QtWebEngineProcess.exe lacks file version resources on  
Windows  
* QTBUG-87378 QttWebEngine doesnt block new view request when  
`request.openIn` is not called  
* QTBUG-88861 QWebEngineUrlRequestInterceptor ignores extra HTTP headers  
when redirecting  
* QTBUG-88938 QtPdf: local files can't be loaded with QQuickPdfDocument  
on Windows  
* QTBUG-89001 event.getModifierState("CapsLock") does not work  
* QTBUG-86389 QtWebengine's touch becomes unresponsive in Youtube  
* QTBUG-65223 [REG 5.9 -> 5.10] loadStarted is emitted twice when  
loading link with anchor  
* QTBUG-87089 Unreliable QWebEnginePage::loadFinished signal depending  
on page content  
* QTBUG-89740 [REG 5.15.1 -> 5.15.2] Visiting LinkedIn causes  
"Terminating renderer for bad IPC message"  
* QTBUG-81263 tst_QWebEnginePage::devTools fails with MSVC 2019  
* QTBUG-85731 Screen sharing does not work on Google Meet  
* QTBUG-90490 Crash on system with non-standard locale  
* QTBUG-90355 Wrong suggested filename with data: URLs  
* QTBUG-90347 Heap corruption in WebEngineLibraryInfo::isRemoteDrivePath  
* QTBUG-90517 [REG 5.15.2 -> 5.15.3] QWebEnginePage::loadFinished signal  
is not emitted if the page is loaded but the server sends 404 http  
status code  
* QTBUG-86286 [REG 5.10.0 -> 5.15.0]  
QWebEngine(Profile|Page)::set[Url]RequestInterceptor does not reliably  
replace existing interceptor  
* QTBUG-91178 [REG 5.15.2 -> 5.15.3] DevTools do not highlight elements  
when hovering  
* QTBUG-72368 Mac : QtWebEngine crashes in case the system volume  
formatting is 'case-sensitive'  
* QTBUG-88001 Testing giving QWidgets a second finger alone crashes Qt  
* QTBUG-87154 Add static dependencies from 3rdparty in qtbase  
* QTBUG-88976 Regression in pdf printing font subsetting in Qt Webengine  
5.15.2  
* QTBUG-89627 tst_QWebEngineView::horizontalScrollbarTest fails with  
macOS  
* QTBUG-86034 When showing the popup for a drop-down on a webpage it  
will not show correctly  
* QTBUG-89358 QtWebengine: Overlay positions miscalculated on rotated  
windows  
* QTBUG-89753 prefers-color-scheme does not seem to work  
* QTBUG-90035 PDF zoom is broken  
* QTBUG-57636 WebEngineView LoadStoppedStatus is not documented  
* QTBUG-91187 Segfault in  
tst_QWebEngineUrlRequestInterceptor::jsServiceWorker  
  
### qtwebview  
* QTBUG-89638 When using multiple webviews via a QQuickWidget then it  
will show the first WebView fine but not the subseqent ones  
* QTBUG-90506 [REG 5.15.2 -> 5.15.3] qtwebview has .gitignore file in  
source archive  
  
### qtquickcontrols2  
* QTBUG-88184 property count of SplitView is not documented  
* QTBUG-87283 REG: Popup position changes after opening once  
* QTBUG-85770 SwipeDelegate resizes incorrectly while it is open  
* QTBUG-84426 Tumbler without wrap ignores initial currentIndex  
* QTBUG-75042 [Accesssibility] Qt Quick Control 2 Dialog parts (title,  
body, footer) are read in wrong order  
* QTBUG-89673 Destroying a modal Dialog with exit transition blocks all  
mouse input to other dialogs  
* QTBUG-61021 Autocomplete of editable ComboBox not working on Android  
  
### qtcharts  
* QTBUG-85909 QList::insert(): Index out of range  
  
### qtvirtualkeyboard  
* QTBUG-89018 The prediction of Pinyin input method is incorrect  
* QTBUG-85245 Candidate characters are mixed in uppercase and lowercase  
when using Pinyin in Simplified Chinese  
* QTBUG-85554 When the Qt Virtual Keyboard is rendered in Wayland  
compositor, QInputMethod::keyboardRectangle() doesn’t return correct  
values  
  
### qtscxml  
* QTBUG-89521 When connecting to the relevant state changed signals for  
a StateMachine then when running via Valgrind there is an invalid read  
on exit  
  
### qtremoteobjects  
* QTBUG-86241 Q22020 Flaky failing autotest function testProxy in  
ProxyTest  
  
### qtquicktimeline  
* QTBUG-89479 TimelineAnimation type documentation is missing properties  
  
### qtquick3d  
* QDS-3049 It is not possible to use a floating point value for the U  
and V scale properties in a Texture type, although they are float based  
* QTBUG-88768 View3D having node with Qt Quick texture as material  
crashes when loaded and unloaded with Loader  
* QTBUG-88769 Nodes with Qt Quick texture as material created and  
destroyed dynamically leads to crash  
* QTBUG-88771 Adding and removing items in model of Repeater3D having Qt  
Quick texture as material causes crash  
* QTBUG-88236 qtquick3d doesn't compile with no-gui flag  
* QTBUG-85168 Qt Quick3D skybox crash on android  
* QDS-3330 Crash when importing 3D studio project  
* QTBUG-78975 Importing .dae file with global scale only applies the  
scale to x-axis  
* QTBUG-86078 Parallel static build of Qt Quick 3D can fail (somehow  
because of qtwayland)  
* QTBUG-87952 Balsam does not generate all materials from FBX or gltf2  
* QTBUG-88775 Transparent areas of Qt Quick content of a texture in  
node's material are initially grey  
* QTBUG-83830 Switching from Offscreen to Underlay render mode causes a  
crash  
  
Known Issues  
------------  
  
Credits for the  release goes to:  
---------------------------------  
  
Aavitsland Eirik  
Achtelik Mike  
Agocs Laszlo  
Aiguo Ma  
Albamont Jim  
Blomfeldt Eskil Abrahamsen  
Bornemann Joerg  
Boudjelthia Assam  
Brasser Michael  
Bruhin Florian  
Brüning Michael  
Buddenhagen Oswald  
Buhr Andreas  
Burtsev Kirill  
Casafranca Juan  
Casafranca Juan José  
Castro Helio Chissini de  
Chuan Wang  
ChunLin Wang  
Cord-Landwehr Andreas  
Croitor Alexandru  
Curtis Mitch  
D'Angelo Giuseppe  
David Szabolcs  
Duivenvoorde Richard  
Edelev Alexey  
Edmundson David  
Ehrlicher Christian  
Falsini Fabio  
Faure David  
Gehör Pekka  
Gladhorn Frederik  
Goldstein Maximilian  
Golubev Andrei  
Gustavsen Richard Moe  
Gutman Cameron  
Habacker Ralf  
Haixiang Tang  
Halmet Heikki  
Hao Zhang  
Hartmann Andre  
Hartmann Thomas  
Hartmetz Andreas  
Heikkinen Jani  
Heikkinen Miikka  
Heimrich Karsten  
Hermann Ulf  
Hilsheimer Volker  
Holappa Teemu  
Hufthammer Karl Ove  
Jeisecke Nils  
Jensen Allan Sandfeld  
Kartashov Alexander  
Kleint Friedemann  
Klitzing André  
Klocek Michal  
Koehne Kai  
Koivikko Jarkko  
Kokko Antti  
Koscheev Vyacheslav  
Kosmale Fabian  
Krus Mike  
Kudryavtsev Anton  
Kurazyan Sona  
Kushnir Igor  
Kyzivat Keith  
Köhne Kai  
Lee Inho  
Lee Jaehak  
Leinonen Tony  
Lemire Paul  
Loehning Robert  
Macieira Thiago  
Mandriva Hiweed  
Mao Sheng  
Martinec Tamas  
Martins Sergio  
Matikainen Vikke  
Miettinen Leena  
Mikolajczyk Piotr  
Moskal Bartlomiej  
Määttä Antti  
Möller Matthias  
Nichols Andy  
Nikiforov Aleksei  
Nordheim Mårten  
Novak Tadej  
Okada Shinichi  
Oksa Tapio  
Ollila Kimmo  
Pan Yi-Jyun  
Pastor Kai  
Pernu Miika  
Piippo Samuli  
Pocheptsov Timur  
Poikelin Joni  
Pol Aleix  
Portale Alessandro  
Potter Lorn  
Qi Liang  
Rabiei Soroush  
Ranghetti Luiz Fernando  
Redondo David  
Reinio Topi  
Rutledge Shawn  
Saario Toni  
Samir Ahmad  
Samokhatko Volodymyr  
Shaw Andy  
Shouwei Niu  
Solovev Ivan  
Storsjö Martin  
Strømme Christian  
Sundqvist Tarja  
Sæther Jan Arve  
Sørvig Morten Johan  
Varga Peter  
Verria Doris  
Vestbø Tor Arne  
Volkov Alexander  
Vuolle Juha  
Wang ChunLin  
Wang Wenjia  
Weickelt Richard  
Welbourne Edward  
Wicking Paul  
Wolff Oliver  
Xiaojun Xiang  
Xinwei Li  
YaNing Lu  
Yelenskiy Stanislav  
Yu Zhang  
Zahorodnii Vlad  
Zakor Tamas  
