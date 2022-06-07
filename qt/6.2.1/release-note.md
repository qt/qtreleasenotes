Release note  
============  

Qt 6.2.1 release is a patch release made on the top of Qt 6.2.0.  
As a patch release, Qt 6.2.1 does not add any new functionality but provides  
bug fixes and other improvements and maintains both forward and backward  
compatibility (source and binary) with Qt 6.2.0.  

For detailed information about Qt 6.2, refer to the online documentation  
included in this distribution. The documentation is also available online:  
  
https://doc.qt.io/qt-6/index.html  
  
The Qt version 6.2 series is binary compatible with the 6.1.x series.  
Applications compiled for 6.1 will continue to run with 6.2.  
  
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
* 2a5a93a04d SQLite: Update SQLite to v3.36.0  
Updated SQLite to v3.36.0  
  
* 138d07dec7 OpenSSL: Let people opt-in to use TLS 1.3 PSK callback  
When using TLS 1.3 we suppress the first callback from OpenSSL about  
pre-shared keys, as it doesn't conform to the past behavior which  
preSharedKeyAuthenticationRequired provided. With this update you can  
opt-out of that workaround by setting the QT_USE_TLS_1_3_PSK environment  
variable  
  
* d11cbb5643 Fix querying font aliases that share name with other fonts  
Fixed an issue where some font styles and weights would not be  
selectable. This was especially noticeable on Windows.  
  
* 4acc17fa7f qSwap: make it constexpr  
qSwap is now constexpr.  
  
* 8d445e6c73 Use Yu Gothic UI as the main fallback font for Japanese  
Made the primary fallback font on Japanese locale "Yu Gothic UI" (the  
default system font).  
  
* c36932ef6f Update PCRE2 to 10.38  
PCRE2 has been updated to version 10.38.  
  
* fbaf6d0bdf Revert "Support family names that end/start with space"  
Fixed an assert that happened when the system had a font with a  
trailing or leading space in its name.  
  
* 8fbf61c323 freetype/no-fc: Disambiguate fonts with different widths  
Fixed a bug where fonts of different width within the same family would  
be unselectable if the Freetype font database (no-fontconfig  
configuration) was in use.  
  
### qtdeclarative  
* 93911fa45c Add button argument to the  
TapHandler.[single|double|]tapped signals  
TapHandler's tapped(), singleTapped() and doubleTapped() signals now  
have two arguments: the QEventPoint instance, and the button being  
tapped. If you need it, you should write an explicit function for the  
signal handler: onTapped: function(point, button) { ... } or  
onDoubleTapped: (point, button)=> ...  
  
* f51231164e QQmlEngine: Fine grained translation binding tracking  
QQmlEngine::retranslate no longer refreshes all bindings, but only  
translation bindings.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-30617 QtConcurrentMap does not map QJsonArray  
* QTBUG-96062 Integrity linker can't cope with duplicate object files on  
command line  
* QTBUG-95565 Qt Creator cannot build Qt 6 for iOS from the start  
* QTBUG-96305 [REG 5.15.5 -> 5.15.6] xcode builds broken if OBJECTS_DIR  
set  
* QTBUG-96103 Memory corruption in  
tst_qreadwritelock::multipleReadersLoop()  
* QTBUG-96285 QProcess can't be restarted  
* QTBUG-79016 Processing qm file name error when using config  
embed_translations  
* QTBUG-94835 Font Weight not properly reflected  
* QTBUG-72872 Nested QtConcurrent::map cause deadlock  
* COIN-755 Integration is blocked in dev  
* QTBUG-96085 Cannot configure qtdeclarative with tests on Android  
* QTBUG-49771 Backspace key is not working when CapsLock is on  
* QTBUG-96208 macOS: Crash on application exit due to unloading library  
with objc class  
* QTBUG-96600 Some QGuiApplication command line options have incorrect  
descriptions  
* QTBUG-96345 tst_QSocks5SocketEngine::simpleConnectToIMAP() is flaky on  
Ubuntu  
* QTBUG-89765 Vulkan: view3d example occasionally(?) has broken indexed  
drawing  
* QTBUG-96288 QTextEdit cursor postion error when QTextEdit has  
different pointsize  
* QTBUG-95942 The elidedtext() function cannot realize text ellipsis in  
Tibetan  
* QTBUG-94031 FILE_ID_INFO is redefined when using MinGW-w64 version  
9.0.0  
* QTBUG-76948 IOS: disconnect second screen while app in b/g, it crashes  
when app goes into foreground  
* QTBUG-96594 qt_add_dbus_adaptor behaves different than  
qt6_add_dbus_adaptor  
* QTBUG-96619 QRhi declares types with non-relocatable QVLA in them as  
relocatable which can lead to crashes  
* QTBUG-87669 few gui tests fail to build on Android  
* QTBUG-96511 MacOS iframework paths missing when using  
QT_ADDITIONAL_PACKAGES_PREFIX_PATH  
* QTBUG-96300 The build system does not work accept  
-DFEATURE_cxx20:BOOL=TRUE  
* QTBUG-96690 Qt6. Build failed when use std::optional as a signal  
argument  
* QTBUG-96606 CA certificates not fetched on Android  
* QTBUG-54848 Problem with QAbstractItemDelegate and IME (chinese Input  
Method) with edit trigger QAbstractItemView::AnyKeyPressed  
* QTBUG-96392 HAVE_egl_x11 test fails with libglvnd 1.3.4  
* QTBUG-42661 Wrong dialog activation  
* QTBUG-96838 signing Android app bundles fails with 6.2.0-rc  
* QTBUG-78970 REG 5.9.4 => 5.12.4 setAutoRaise not working on Mac  
* QTBUG-96926 QImage::convertToFormat(format, colorTable) doesn't  
preserve devicePixelRatio  
* QTBUG-96322 Crash on RHI with Opacity Mask effect  
* QTBUG-96846 Many messages "QThread::wait: Thread tried to wait on  
itself" when Creator starts new threads  
* QTBUG-96906 iOS / Android / WebAssembly have invalid [DevicePaths]  
Prefix in target_qt.conf when installing Qt from online installer  
* QTBUG-96798 Separate debug info builds are broken when cross-  
compiling, wrong objcopy is used  
* QTBUG-86094 Generating large pdf files when using pen with zero width  
* QTBUG-96466 [REG 5.15.2-6.2.0] Runtime crash on changing screen's  
scale factor  
* QTBUG-85058 Windows: QDir::entryList doesn't work for directories that  
end with '.lnk'  
* QTBUG-96621 Missing QHash include in qcocoawindow.h  
* QTBUG-94341 Windows: Let QLocale::uiLanguages() return all preferred  
languages  
* QTBUG-97023 Fix invalid Qt6::ATSPI2_nolink target  
* QTBUG-96998 CMake: UNIX is not set for INTEGRITY builds  
* QTBUG-96978 Brush transformations are not supported by the PDF engine  
* QTBUG-97085 Crash while JITting QRegularExpression in multiple threads  
(Rosetta)  
* QTBUG-97119 Escape doesn't close popups anymore  
* QTBUG-13965 QPainterPath::addText() does not respect QFont::SmallCaps  
* QTBUG-79140 [REG 5.13.0 -> 5.14.0]OTF fonts don't work correctly  
* QTBUG-83908 Material.System does not work on Windows 10 in Dark Mode  
* QTBUG-97241 Qt no longer compiles when configured with -trace  
* QTBUG-96734 QDoubleSpinBox asserts in validate with default properties  
* QTBUG-97146 QRhiMetal asserts when a given sampleCount is not  
supported by a device  
* QTBUG-96789 Shader cache not able to write out compiled shaders  
* QTBUG-85574 No focus on window after showing and hiding a modal dialog  
* QTBUG-97098 Documentation: building sql drivers following the  
instructions in the docs fails with "CMake Error: Unknown argument  
--build"  
* QTBUG-97179 Assertion failure inside of QNetworkAccessManager thread  
* QTBUG-92958 Blinking scrollbar with QScrollArea and edge cases.  
* QTBUG-8857 Qt::WA_ShowWithoutActivating causes a situation where a  
QLineEdit cursor is blinking but not active  
* QTBUG-93955 Material.System does not work on Ubuntu (Gnome)  
* QTBUG-97122 Regression: UTF-32 codec fails on assert when  
fromUnicode() is called  
* QTBUG-97425 Build from sources fails in Qt 6.2.0 with MSVC 2019 in  
c++20 mode  
* QTBUG-84310 CMake: qt_lib_XXX.pri files don't contain run_depends  
entries  
* QTBUG-89640 font.styleName depends on font loading order  
* QTBUG-97384 [REG 5.15.2-6.2.0] "Flow control error" while loading web  
image  
* QTBUG-97441 Doc: generated lists show only the first word of the  
\brief statement  
* QTBUG-69710 QLineEdit can't be used for keyboard input after popup  
menu from another QDialog  
* QTBUG-96128 Compile error when adding QList::const_iterator and  
std::ptrdiff_t  
* QTBUG-96603 QTextDocument: stylesheet border-color for td applied only  
to first td  
* QTBUG-96861 Geoflickr example dstStep assert crash on mac and iOS  
* QTBUG-79081 Nested foreach generate warnings  
* QTBUG-97458 String "6.2.0" found from 6.2.1 source package  
* QTBUG-97486 Crash in TimeZone ICU backend  
* QTBUG-97475 Crash in QItemSelectionModel  
* QTBUG-97443 Crash - DpiAdjustmentPolicy resolved from wrong  
environment  
* QTBUG-97116 OpenSSL TLS plugin is not loaded for OpenSSLv3  
* QTBUG-95609 cmake names for qml plugins  
* QTBUG-97493 Change of QDateTimeEdit::setDateTime not documented in  
"Changes to Qt Modules in Qt 6"  
* QTBUG-97054 QSqlDatabase.open() warning  
* QTBUG-95200 qt6_add_qml_module only works when used in same folder  
than the backing library  
* QTBUG-95670 PSK doesn't work when both the client and server use TLS  
1.3  
* QTBUG-93340 trafficlight_qml_dynamic crashes on Android device  
* QTBUG-30040 tst_qtooltip::task183679 is unstable in Mac CI  
* QTBUG-96127 Broken external links in Qt docs  
* QTBUG-96303 Review (again) CodeChecker issues for Qt Core  
* QTBUG-96327 qt5.15 examples on qnx710 display "is an invalid ELF  
object (shstrtab section header seems to be at 0)“  
* QTBUG-95042 QFrame Qt::WA_TranslucentBackground is broken with  
specific window flags and drawable child item  
* QTBUG-96290 qmlimportscanner: "qmldir file not found at" when  
configuring quickwidget example with static Qt  
* QTBUG-84877 QLocale::system() uses short names of days and months for  
narrow formats  
* QTBUG-96253 Unable to build qtscxml tests after building with  
components with Conan  
* QTBUG-95832 QtRemoteObjects CMake API is using the internal  
qt_manual_moc API  
* QTBUG-94770 [Qt Virtual keyboard] Keyboards doesn't respond when  
QT_SCALE_FACTOR  is set to 1.5  
* QTBUG-95249 OpenSSL TLS backend plugin missing in macOS installation  
from official binary  
* QTBUG-96441  [REG 6.1.0 - 6.2.0] Windows: QWindow doesn't respect  
minimumWidth/minimumHeight  
* QTBUG-96790 crash in QWindowsFileSystemWatcherEngine::addPaths  
* QTBUG-96786 QPainter::drawRect fills OpenGL window background when  
pen's alpha != 1.0  
* QTBUG-96718 Crash in inBindingWrapper() (Creator built against Qt 6.2  
build)  
* QTBUG-80766 Android app installed from Google  Play store crashes  
* QTBUG-96654 REG[5.15-6.1]QTreeView crash when checkbox triggers reset  
* QTBUG-97028 \relates documentation should mention how it interacts  
with templated classes  
* QTBUG-96057 Bluetooth crash when connectToPairedDevice on windows  
* QTBUG-95285 Create documentation page for Qt for Android Manifest  
* QTBUG-97002 Building for android fail  
* QTBUG-96239 Document CMake component in CMake function documentation  
* QTBUG-96575 Merge "DTLS Client"and "DTLS Server" examples  
* QTBUG-95763 Configuring an executable with an attached qml module  
fails when using the Xcode generator  
* QTBUG-58013 Cursor position changes not properly passed to input  
method  
  
### qtsvg  
* QTBUG-97421 text x,y positions are always parsed as pixels  
* QTBUG-97422 font-size is always parsed as pixels  
  
### qtdeclarative  
* QTBUG-64847 TapHandler does not tell us which button was tapped (and  
this breaks the manual test)  
* QTBUG-96301 qmldir files generated by CMake do not respect .ui.qml  
suffix  
* QTBUG-95589 Customizing checkbox does not fully work when using  
example from documentation  
* QTBUG-87402 Error when using ShaderEffect doesn't tell the user how to  
fix it  
* QTBUG-96130 srbCache exhibits unreasonable, semi-continuous growth  
with dynamic scenes  
* QTBUG-91109 Inconsistent behaviour of TextArea with horizontalCenter  
between different platforms (Gallery example)  
* QTBUG-96405 setGraphicsApi :OpenGLRhi.  QML application resizing  
flickers and is sometimes blank  
* QTBUG-96275 Crash while loading QML type data from disk cache  
* QTBUG-96290 qmlimportscanner: "qmldir file not found at" when  
configuring quickwidget example with static Qt  
* QTBUG-96147 qmlsc does not understand curly braced grouped properties  
* QTBUG-96587 qmlsc ignores return type of CallPropertyLookup  
* QTBUG-96551 Crash while processing a shortcut key  
* QTBUG-96902 Import of JS module to QML does not work  
* QTBUG-96358 ShaderTools package not found when building qtdeclarative  
examples in-tree in a prefix build (not as ExternalProjects)  
* QTBUG-96909 ListView/Flickable: when releasing multitouch, list stays  
in dragging state  
* QTBUG-86744 ListView.isCurrentItem not available until model is  
refreshed  
* QTBUG-96625 Unable to declare variable with identifier equal to  
function name inside getter  
* QTBUG-92841 Offscreen Surfaces should not receive input events in 3D  
scenes  
* QTBUG-96805 quick examples not compiling on Wasm: CMake Error at  
.../wasm_32/lib/cmake/Qt6/QtPublicPluginHelpers.cmake  
* QTBUG-95544 Regression: buttons invisible when using non-sized custom  
backgrounds  
* QTBUG-96668 [Reg 6.1 -> 6.2] Cannot overwrite property bindings in  
aliased elements  
* QTBUG-97099 [cmake] dependent qml plugins not auto-loaded with  
statically linked qt  
* QTBUG-96192 Performance concerns for a qmlengine->retranslate() call  
* QTBUG-97427 Binding an attached property instance to a  
Connection.target results in attachee being set as a target  
* QTBUG-96876 Error initializing PageIndicator with Material style  
* QTBUG-97480 ParentChange crash  
* QTBUG-95200 qt6_add_qml_module only works when used in same folder  
than the backing library  
* QTBUG-93340 trafficlight_qml_dynamic crashes on Android device  
* QTBUG-95587 icon.source of Control is not resolved relative to user  
code  
* QTBUG-96200 Only the first Q_PROPERTY marked as REQUIRED is required  
in reality  
* QTBUG-96127 Broken external links in Qt docs  
* QBS-1676 qmlcache created by QBS causes loading problem if the qml  
filename matches the name of some qml file from Qt package and has  
inline component  
* QTBUG-85151 "module "QtQuick.Templates" is not installed" when some  
files' QML imports specify version and some don't  
* QTBUG-60491 When TextEdit show the file more than 1mb, the soft will  
use many memory  
* QTBUG-91163 cannot build some modules with -developer-build on 32bit  
architectures without -no-warnings-are-errors  
* QTBUG-96964 Changing the ShaderEffect shader crashes  
* QTBUG-96454 QT6.2.0 cross compile failed on QNX7.1 Version  
  
### qtmultimedia  
* QTBUG-94845 autoOrientation in QML VideoOutput doesn't work  
* QTBUG-95626 [REG] Audio playback is not stopped on MediaPlayer  
destruction  
* QTBUG-95576 [REG] MediaPlayer position property is not updated while  
playing a video  
* QTBUG-96376 Recording fails when encoding audio to other codecs other  
than AAC, WAV, or ALAC  
* QTBUG-96368 Mediaplayer's video output doesn't update when changing  
video source on macOS/iOS  
* QTBUG-96089 Multiply defined symbols found for  
QWindowsIntegration::~QWindowsIntegration(void)  
* QTBUG-96609 Outdated code snippet in QMultimediaPlayer documentation  
* QTBUG-96402 QMediaPlayer position inconsistent  
* QTBUG-96652 QML VideoOuput cannot be used directly with QML Camera  
* QTBUG-95066 Multimedia: Missing documentation for QML types  
* QTBUG-96705 The preview parameter from imageCaptured() can no longer  
be used as image source (QML)  
* QTBUG-96642 Loading multiple SoundEffects in QML randomly crashes the  
application  
* QTBUG-96704 In QML, using capture*() after switching between camera  
devices crashes the application  
* QTBUG-95234 MingW build does not find WMF, and builds without a valid  
backend  
* QTBUG-96944 Recorder app crashes while switching between apps  
* QTBUG-96943 Incorrect video orientation for recorded video - recorder  
example  
* QTBUG-95063 audiosource example asserts on startup  
* QTBUG-96984 MediaPlayer example in Detailed Description is missing id  
* QTBUG-96719 Update resolution list by data from the  
QList<QCameraFormat> on QCameraFormat  
* QTBUG-96955 Spectrum app crashes once user try to edit settings  
* QTBUG-97069 [Windows] Crash (use-after-free) on (Q)MediaPlayer  
destruction  
* QTBUG-97152 QMediaPlayer 'play' jumps to wrong position after seek  
* QTBUG-96750 Incorrect return from full screen mode for player example  
* QTBUG-96985 Video and MediaPlayer don't allow to use relative URLs  
* QTBUG-97622 QML ImageCapture preview property does nothing?  
* QTBUG-97379 [Boot2Qt] Declarative-camera example does not work with  
Toradex Apalis i.MX6  
* QTBUG-96401 qtmultimedia fails to configure due to not finding GObject  
due to typo.  
* QTBUG-96406 MM Video playback fails completely when using (linking)  
WebEngine  
* QTBUG-96202 SoundEffect does not work in Qt6.2 beta3 in Windows and  
Linux  
* QTBUG-95883 QtMultimedia tests fail on Android  
* QTBUG-96952 Android MediaPlayer not sending onInfo updates  
* QTBUG-95010 Missing loops property  
* QTBUG-96947 Cannot go back from multi option for qmlvideo example  
  
### qttools  
* QTBUG-95975 [REG Qt 6.2.0 beta1 -> beta2] Rebuilding unchanged sources  
results in build error  
* QTBUG-96837 qdoc: warnings about generatelist incorrectly formatted  
* QTBUG-96694 broken "Contents" links in assistant  
* QTBUG-97028 \relates documentation should mention how it interacts  
with templated classes  
* QTBUG-96521 Windeployqt does not deploy Qt6ShaderTools lib with Rhi  
Renderer  
* QTBUG-97034 qdoc: relative paths in 'includepaths' variable are  
resolved too late  
* QTBUG-96408 QDoc crashed while parsing the index file in Qt5.15  
* QTBUG-97453 qdoc: Unnecessary warnings when running in testing mode  
* QTBUG-97389 'lupdate_sources' variable empty in cmake file generated  
by qt_add_lupdate  
  
### qttranslations  
* QTBUG-95658 Fix qtquickcontrols2 references in qttranslations.git  
* QTBUG-95013 pt_BR translations not loaded  
  
### qtdoc  
* QTBUG-95990 Add support for multi-abi application builds for Android  
with qmake  
* QTBUG-95285 Create documentation page for Qt for Android Manifest  
* QTBUG-97052 Typo in Qt for Windows - Graphics Acceleration  
documentation  
* QTBUG-97438 Compiling universal binaries in Qt Creator error  
* QTBUG-96127 Broken external links in Qt docs  
* QTBUG-96151 QML deployment docs need to be rewritten  
* QTBUG-96590 Qt for Android documentation refers to gcc.exe instead of  
clang.exe  
  
### qtlocation  
* QTBUG-96127 Broken external links in Qt docs  
  
### qtsensors  
* QTBUG-96914 Configuring top-level build on Ubuntu 18.04 without pkg-  
config fails in qtsensors  
  
### qtconnectivity  
* QTBUG-80719 connectToDevice() hangs when trying to connect to faulty  
Bluetooth device  
* QTBUG-97242 Windows: 100% CPU load when reading services and  
characteristics  
* QTBUG-96057 Bluetooth crash when connectToPairedDevice on windows  
* QTBUG-83633 Bluetooth Discovery device crash  
* QTBUG-96688 BT LE Android large characteristic write support  
* QTBUG-86796 Documentation should mention that qt bluetooth and audio  
requires QGuiApplication  
  
### qtwayland  
* QTBUG-87624 Wayland client crash when QDrag is used  
* QTBUG-96464 Wayland client race condition in applyConfigure  
* QTBUG-96845 Failed to build FEATURE_wayland_dmabuf_client_buffer  
  
### qtserialport  
* QTBUG-89536 Remove configure.json files for building Qt 6  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
  
### qtwebsockets  
* QTBUG-96127 Broken external links in Qt docs  
  
### qtwebengine  
* QTBUG-96308 Drag and drop does not work on macOS  
* QTBUG-95770 Cannot open recently saved file  
* QTBUG-95580 Crash on GetFaviconsForURL  
* QTBUG-96266 webengine not building (linking): LINK : fatal error  
LNK1104: cannot open file  
'CMakeFiles_QtWebEngineCore_Release_objects.rsp'  
* QTBUG-96196 configure -list-features does not list webengine features  
* QTBUG-95717  Configuring: Qt 6.2 " Unknown command line option  
'-webengine-proprietary-codecs'."  
* QTBUG-96525 QWebEngineScript::setSourceUrl doesn't load scripts from  
qrc  
* QTBUG-96398 Build fails on arm  
* QTBUG-96539 WebEngineView: QtWebEngineProcess cannot start.  
* QTBUG-96002 The document QtWebengine is self-contradictory  
* QTBUG-95367 Webengine examples fails to build: undefined reference to  
`QApplication::QApplication(int&, char**, int)'  
* QTBUG-96375 Build failure with webengine  
* QTBUG-76249 [Reg 5.9->5.11]Custom UserAgent ignored if page opened  
with window.open or _blank  
* QTBUG-88875 WebChannel is broken in ApplicationWorld with javascript  
disabled in MainWorld  
* QTBUG-96127 Broken external links in Qt docs  
* QTBUG-97414 tst_CertificateError::fatalError()  
'!page.error->isOverridable()' returned FALSE.  
* QTBUG-96928 QtWebEngine continuously allocates memory until it get  
killed  
  
### qtwebview  
* QTBUG-94935 Clean up Qt WebView documentation for Qt 6.2  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
  
### qtcharts  
* QTBUG-92544 charts/audio has dependency to non-existent module  
Multimedia  
  
### qtdatavis3d  
* QTBUG-95270 Can't link to 'Qt Data Visualization' from qdoc  
  
### qtscxml  
* QTBUG-96253 Unable to build qtscxml tests after building with  
components with Conan  
  
### qtnetworkauth  
* QTBUG-97458 String "6.2.0" found from 6.2.1 source package  
* QTBUG-96127 Broken external links in Qt docs  
  
### qtremoteobjects  
* QTBUG-95832 QtRemoteObjects CMake API is using the internal  
qt_manual_moc API  
* QTBUG-91163 cannot build some modules with -developer-build on 32bit  
architectures without -no-warnings-are-errors  
  
### qtquicktimeline  
* QTBUG-97043 qtquicktimeline: commercial only license ?  
  
### qtquick3d  
* QTBUG-96163 ModelParticle3D instanceTable property not documented  
* QDS-5004 FBX imported models broken in 3D Editor  
* QDS-5103 Issues with QtQuick3D.Particles3D module designer specifics  
* QDS-5098 QtQuick3D.FileInstancing component is shown in library as  
"Instancing"  
* QDS-5096 Fix property specifics for QtQuick3D.Repeater3D  
* QTBUG-96730 Custom Material fragment shader sometimes does not have  
access to special variables  
* QTBUG-79026 WasdController can't get control of keyboard back after  
using UI element  
* QTBUG-97260 Model blend particle spatial node is not always  
initialized  
* QTBUG-96307 Issue with stopped particle system and startTime  
* QTBUG-96457 "infinite plane" Item2D prevents event propagation to 2D  
content behind it  
* QTBUG-92841 Offscreen Surfaces should not receive input events in 3D  
scenes  
  
### qtshadertools  
* QTBUG-96618 qtquick3d examples fail to build for QNX  
* QTBUG-96524 Qsb tool output (errors) not visible when called From  
visual studio / cmake  
* QTBUG-96912 No documented way to build GLES shader using  
samplerExternalOES with qsb  
* QTBUG-97458 String "6.2.0" found from 6.2.1 source package  
  
### qtcoap  
* QTBUG-96127 Broken external links in Qt docs  
* QTBUG-91163 cannot build some modules with -developer-build on 32bit  
architectures without -no-warnings-are-errors  
  
Known Issues  
------------  
  
* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-6/gettingstarted.html#platform-requirements  
* RTA reported issues from Qt 6.2  
https://bugreports.qt.io/issues/?filter=23315  
* Supported development platforms are listed here:  
https://bugreports.qt.io/browse/QTBUG-90021  
* See Qt 6.2 Known Issues from:  
https://wiki.qt.io/Qt_6.2_Known_Issues  

Credits for the  release goes to:  
---------------------------------  
  
Aavitsland Eirik  
Achtelik Mike  
Ackers Dan  
Agocs Laszlo  
Akulich Alexander  
Apostolou Dimitrios  
Astals Cid Albert  
Bennett Nicholas  
Bin Chen  
Blasche Alex  
Blomfeldt Eskil Abrahamsen  
Borisova Tatiana  
Bornemann Joerg  
Boudjelthia Assam  
Brüning Michael  
Buddenhagen Oswald  
Buhr Andreas  
Burtsev Kirill  
Casafranca Juan  
Chuan Wang  
Croitor Alexandru  
Curtis Mitch  
D'Angelo Giuseppe  
David Szabolcs  
Dietz Pascal  
Edelev Alexey  
Eftevaag Oliver  
Egedi Balazs  
Eklund Iikka  
Faure David  
Fella Nicolas  
Funk Kevin  
Gehör Pekka  
Goldstein Maximilian  
Golubev Andrei  
Grulich Jan  
Grönholm Kaj  
Gustavsen Richard Moe  
Gérard Lucie  
Haixiang Tang  
Halmet Heikki  
Hao Zhang  
Hartmann Thomas  
Heikkinen Jani  
Heikkinen Miikka  
Heimrich Karsten  
Hermann Ulf  
Hilsheimer Volker  
Holland Dominik  
Jensen Allan Sandfeld  
Jenssen Tim  
Kleint Friedemann  
Klocek Michal  
Knoll Lars  
Kobus Jarek  
Koivikko Jarkko  
Kosmale Fabian  
Kurazyan Sona  
Kvinge Jonas  
Köhne Kai  
Macieira Thiago  
Markovic Pavol  
Martinec Tamás  
Meshcheriakov Ievgenii  
Mira Samuel  
Mohamed Fawzi  
Määttä Antti  
Neumann Alexander  
Nichols Andy  
Nordheim Mårten  
Pelkonen Tuomo  
Persano Mauro  
Petäjäjärvi Pasi  
Piippo Samuli  
Pocheptsov Timur  
Poikelin Joni  
Pol Aleix  
Potter Lorn  
Qi Liang  
Reinio Topi  
Rocha André de la  
RuiJie Fan  
Rutledge Shawn  
Schmertmann Lars  
Scott Craig  
Sera Luca Di  
Shaw Andy  
Shivashankar Venugopal  
Solovev Ivan  
Srebrny Piotr  
Staikov Andrii  
Stottlemyer Brett  
Strømme Christian  
Sæther Jan Arve  
Sørvig Morten Johan  
Thibault Samuel  
Tkachenko Ivan  
Trotsenko Alex  
Tvete Paul Olav  
Varga Peter  
Verria Doris  
Vertriest Nico  
Vestbø Tor Arne  
Voelker Jannis  
Vuolle Juha  
Welbourne Edward  
Wicking Paul  
Wolff Oliver  
Zhang JiDe  
