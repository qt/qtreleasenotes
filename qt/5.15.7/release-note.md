Release note  
============  
  
Qt 5.15.7 release is a patch release made on the top of Qt 5.15.6. As a patch  
release, Qt 5.15.7 does not add any new functionality but provides bug fixes  
and other improvements.  
  
For detailed information about Qt, see the Qt 5.15 online documentation:  
https://doc.qt.io/qt-5/index.html.  
  
Important Changes  
-----------------  
  
### qtbase  
* 41fabc9b27 Fix bug with NoFontMerging when font does not support  
script  
Fixed an issue with NoFontMerging and changing font families  
dynamically, where boxes would be seen in place of the correct text.  
  
* 07815c61d2 OpenSSL: Let people opt-in to use TLS 1.3 PSK callback  
When using TLS 1.3 we suppress the first callback from OpenSSL about  
pre-shared keys, as it doesn't conform to the past behavior which  
preSharedKeyAuthenticationRequired provided. With this update you can  
opt-out of that workaround by setting the QT_USE_TLS_1_3_PSK environment  
variable  
  
* bc36ae33e8 Fix license information for libjpeg-turbo  
Clarified that libjpeg-turbo is actually covered by three licenses, not  
only IJG.  
  
* 9929873fdf SQLite: Update SQLite to v3.36.0  
Updated SQLite to v3.36.0  
  
* ea5edb67a9 Update bundled libjpeg-turbo to version 2.1.1  
libjpeg-turbo was updated to version 2.1.1  
  
* b7598fd7e9 Fix querying font aliases that share name with other fonts  
Fixed an issue where some font styles and weights would not be  
selectable. This was especially noticeable on Windows.  
  
* 4851da1509 Update PCRE2 to 10.38  
PCRE2 has been updated to version 10.38.  
  
* 4c1a95efa9 Revert "Support family names that end/start with space"  
Fixed an assert that happened when the system had a font with a  
trailing or leading space in its name.  
  
### qtdeclarative  
* 4757cac470 Fix distorted text with subpixel matrix translation  
Fixed an issue where text using NativeRendering would look slightly  
skewed if it was inside a parent that had been positioned at a subpixel  
offset.  
  
### qtwayland  
* 36060ad8 Ignore viewporter buffer size when buffer is null  
Fixed an issue in the wp_viewporter extension, where it would emit a  
protocol error if the viewport was configured before attaching a buffer  
to the surface.  
  
* 3ff4cd60 Implement wp_viewporter support for video buffer formats  
Support for wp_viewporter extended to cover less common buffer formats.  
  
### qtimageformats  
* e8585ba Update bundled libwebp to version 1.2.1  
Update bundled libwebp to version 1.2.1  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-30522 macOS: Closing application window while context menu is  
open leaves menu open  
* QTBUG-94826 Build Failure with LTTNG enabled  
* QTBUG-69975 Cocoa NSFullSizeContentViewWindowMask was wiped when  
toggling fullscreen  
* QTBUG-81770 Garbled character is displayed when switching Arabic to  
another language  
* QTBUG-94951 Qt 6.2 alpha assertion failed in qunicodetools.cpp  
* QTBUG-94091 Nested Graphicsview does not works as expected  
* QTBUG-87128 In the help pages: The QFileInfo::setFile() example is  
really the QDir::setCurrent() one  
* QTBUG-96101 QPMCache deleted from another thread  
* QTBUG-88989 Build errors on Android with latest gradle  
* QTBUG-92018 QLocale date toString uses standalone name where plain  
name should be used  
* QTBUG-86279 QLocale::system()'s standaloneDayName() and dayName() use  
the same back-end  
* QTBUG-52450 macOS: Closing a window that's in fullscreen removes the  
window, but doesn't exit fullscreen  
* QTBUG-81552 macOS: Wrong cursor shown when the mouse is moved slowly  
into window  
* QTBUG-96003 [Reg Qt5.9.9 -> Qt5.15] setCursor() does not work on  
QWidget inside QWidget  
* QTBUG-68069 Exiting fullscreen window leaves the application in  
fullscreen mode on macOS  
* QTBUG-96170 WASM: data URI scheme does not work  
* QTBUG-91059 Mac: Multiple modal dialogs block all input  
* QTBUG-96305 [REG 5.15.5 -> 5.15.6] xcode builds broken if OBJECTS_DIR  
set  
* QTBUG-79016 Processing qm file name error when using config  
embed_translations  
* QTBUG-95108 Reg[Qt 5.15.4->Qt5.15.5] Qt::MetaModifier and  
Qt::GroupSwitchModifier is always set  
* QTBUG-95289 GroupSwitchModifier always present in event.modifiers()  
* QTBUG-49771 Backspace key is not working when CapsLock is on  
* QTBUG-72872 Nested QtConcurrent::map cause deadlock  
* QTBUG-96208 macOS: Crash on application exit due to unloading library  
with objc class  
* QTBUG-87669 few gui tests fail to build on Android  
* QTBUG-95202 Auto-generated android-*-deployment-settings.json contains  
wrong path to immediate qrc file on Qt 6  
* QTBUG-95235 Building Quick Controls 2 examples with Qt 6.1.1 for  
Android fails  
* QTBUG-94835 Font Weight not properly reflected  
* QTBUG-42661 Wrong dialog activation  
* QTBUG-96600 Some QGuiApplication command line options have incorrect  
descriptions  
* QTBUG-95013 pt_BR translations not loaded  
* QTBUG-96926 QImage::convertToFormat(format, colorTable) doesn't  
preserve devicePixelRatio  
* QTBUG-96846 Many messages "QThread::wait: Thread tried to wait on  
itself" when Creator starts new threads  
* QTBUG-96621 Missing QHash include in qcocoawindow.h  
* QTBUG-91438 iOS enormous leak ends with "Terminated due to memory  
issue"  
* QTBUG-95827 qmake CONFIG+=Debug leads to release builds  
* QTBUG-85574 No focus on window after showing and hiding a modal dialog  
* QTBUG-92958 Blinking scrollbar with QScrollArea and edge cases.  
* QTBUG-97179 Assertion failure inside of QNetworkAccessManager thread  
* QTBUG-93885 ASSERT failure in void __cdecl  
QtFontFamily::ensurePopulated(void) on system registed font  
* QTBUG-79140 [REG 5.13.0 -> 5.14.0]OTF fonts don't work correctly  
* QTBUG-86094 Generating large pdf files when using pen with zero width  
* QTBUG-96838 signing Android app bundles fails with 6.2.0-rc  
* QTBUG-95565 Qt Creator cannot build Qt 6 for iOS from the start  
* COIN-777 *** Could not find any device matching '--platform iOS  
--minimum-deployment-target  
* QTBUG-89296 No way to specify C standard for Visual Studio 2019 in  
qmake project  
* QTBUG-83081 QTextCodec::canEncode does not work for ICU conversions  
* QTBUG-95670 PSK doesn't work when both the client and server use TLS  
1.3  
* QTBUG-95661 Test result counts are incorrect  
* QTBUG-94451 Switch Android target SDK to 30 for Qt 6.2  
* QTBUG-96345 tst_QSocks5SocketEngine::simpleConnectToIMAP() is flaky on  
Ubuntu  
* QTBUG-95249 OpenSSL TLS backend plugin missing in macOS installation  
from official binary  
* QTBUG-95042 QFrame Qt::WA_TranslucentBackground is broken with  
specific window flags and drawable child item  
* QTBUG-96057 Bluetooth crash when connectToPairedDevice on windows  
* QTBUG-70137 Dockwidgets - Placing QDockWidget is almost impossible  
* QTBUG-58013 Cursor position changes not properly passed to input  
method  
* QTBUG-93414 Qt Quick application stuck in a cursor update loop  
* QTBUG-95669 Clicking enter on some text fields it might freeze UI  
* QTBUG-96671 Android: Keyboard sometimes stuck and replacing previous  
letter  
* QTBUG-96675 Android: Cursor is shown in wrong place  
* QTBUG-96769 Android: keyboard input can get lost  
  
### qtdeclarative  
* QTBUG-95825 Live preview not starting  
* QTBUG-95461 QQuickTextInput doesn't manage pre-edit text correctly  
* QTBUG-89409 Unable to scroll listview by dragging / swiping if header  
is used  
* QTBUG-95881 Single QSGRenderNode-based element in the scene with  
"clip" property enabled is not rendered  
* QTBUG-55204 Crash when items that use shaders are being used  
* QTBUG-96902 Import of JS module to QML does not work  
* QTBUG-86744 ListView.isCurrentItem not available until model is  
refreshed  
* QTBUG-96275 Crash while loading QML type data from disk cache  
* QTBUG-96112 Text tearing on text element when set inside parent  
element with noninteger y value  
* QTBUG-83626 When a Popup has an odd number for the width and/or height  
then texts inside it can be rendered badly  
* QTBUG-55638 garbled font after scrolling with mouse wheel  
* QTBUG-95788 Singletons with clearComponentCache don't fully work  
  
### qtmultimedia  
* QTBUG-93747 CMake configuration files unable to find QtMultimedia for  
QNX  
  
### qttools  
* QTBUG-96220 qt6_create_translation() mishandles -extensions due to  
malformed regex  
* QTBUG-96369 qdoc: The obsolete members page for the QtMac namespace is  
not generated  
* QTBUG-96837 qdoc: warnings about generatelist incorrectly formatted  
* QTBUG-91082 [REG: 5.12->5.13] Assistant does not support custom  
filters anymore  
* QTBUG-90982 macdeployqt mistakenly detect my library as debug libs  
  
### qttranslations  
* QTBUG-95014 pt_BR translations load incorrect catalogs  
* QTBUG-95013 pt_BR translations not loaded  
  
### qtconnectivity  
* QTBUG-93991 Run example Heartrate monitor server on iOS and on Windows  
* QTBUG-95960 IOBluetoothDeviceInquiry never ends  
* QTBUG-95686 Multiple Bluetooth tests fail on macOS  
* QTBUG-80719 connectToDevice() hangs when trying to connect to faulty  
Bluetooth device  
* QTBUG-89149 QLowEnergyController::connectToDevice  
* QTBUG-97242 Windows: 100% CPU load when reading services and  
characteristics  
* QTBUG-96057 Bluetooth crash when connectToPairedDevice on windows  
* QTBUG-83633 Bluetooth Discovery device crash  
  
### qtwayland  
* QTBUG-95464 Qt wayland surface is empty when gst-launch client is  
playing video  
* QTBUG-87624 Wayland client crash when QDrag is used  
* QTBUG-95715 Incorrect texture handling in multi-screen wayland  
compositor  
  
### qtwebengine  
* QTBUG-95770 Cannot open recently saved file  
* QTBUG-95269 Clicking on a link in the PDF viewer crashes with SIGSEGV  
* QTBUG-96928 QtWebEngine continuously allocates memory until it get  
killed  
* QTBUG-96911 qtwebengine build fails with harfbuzz-3.0.0  
* QTBUG-97414 tst_CertificateError::fatalError()  
'!page.error->isOverridable()' returned FALSE.  
* QTBUG-96214 QtWebEngineProcess crashes on glibc 2.34  
* Linux sandbox: fix fstatat() crash  
* Security fixes from Chromium up to version 94.0.4606.81, including:  
    - CVE-2021-30613: Use after free in Base internals  
    - CVE-2021-30616: Use after free in Media.  
    - CVE-2021-30618: Inappropriate implementation in DevTools  
    - CVE-2021-30625: Use after free in Selection API  
    - CVE-2021-30626: Out of bounds memory access in ANGLE  
    - CVE-2021-30627: Type Confusion in Blink layout  
    - CVE-2021-30628: Stack buffer overflow in ANGLE  
    - CVE-2021-30629: Use after free in Permissions  
    - CVE-2021-30630: Inappropriate implementation in Blink  
    - CVE-2021-30633: Use after free in Indexed DB API  
    - CVE-2021-37962: Use after free in Performance Manager  
    - CVE-2021-37967: Inappropriate implementation in Background Fetch API  
    - CVE-2021-37968: Inappropriate implementation in Background Fetch API  
    - CVE-2021-37971: Incorrect security UI in Web Browser UI.  
    - CVE-2021-37972: Out of bounds read in libjpeg-turbo  
    - CVE-2021-37973: Use after free in Portals  
    - CVE-2021-37975: Use after free in V8  
    - CVE-2021-37978: Heap buffer overflow in Blink  
    - CVE-2021-37979: Heap buffer overflow in WebRTC  
    - CVE-2021-37980: Inappropriate implementation in Sandbox  
    - Security bug 1206289  
    - Security bug 1227228  
    - Security bug 1238178  
    - Security bug 1239116  
    - Security bug 1248665  
  
### qtquickcontrols2  
* QTBUG-93050 Memory leak in qiconhelper.cpp when loading icon by name  
* QTBUG-94251 tst_QQuickPopup fails with OpenSUSE 15.3  
  
### qtpurchasing  
* QTBUG-90839 Google Play billing api must be updated  
  
### qtcharts  
* QTBUG-94998 5.15.4 -> 5.15.5, some labels disappeared from axes  
* QTBUG-79218 When zooming out enough then the labels on the axes will  
end up showing drawing errors  
  
### qtdatavis3d  
* QTBUG-96206 Graph's orthoprojection property doesn't work like  
documentation says  
  
### qtvirtualkeyboard  
* QTBUG-95996 Segmentation fault on exit caused by virtual keyboard  
  
Known Issues  
------------  
  
The RTA (release test automation) reported issues in Qt 5.15.x:  
https://bugreports.qt.io/issues/?filter=21874  
  
### qtwebengine
  The CHROMIUM_VERSION file includes an incorrect version number 94.0.4606.61.  
  The correct Chromium patch level version number is 94.0.4606.81.  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Mike Achtelik  
Laszlo Agocs  
Alexander Akulich  
Dimitrios Apostolou  
Eskil Abrahamsen Blomfeldt  
Joerg Bornemann  
Assam Boudjelthia  
Michael Brasser  
Oswald Buddenhagen  
Andreas Buhr  
Mitch Curtis  
Giuseppe D'Angelo  
David Faure  
Josep Ma. Ferrer  
Richard Moe Gustavsen  
Ulf Hermann  
Volker Hilsheimer  
Andreas Holzammer  
Lars Knoll  
Jarkko Koivikko  
Jani Korteniemi  
Kai Köhne  
Ievgenii Meshcheriakov  
Marc Mutz  
Yuya Nishihara  
Mårten Nordheim  
Timur Pocheptsov  
Joni Poikelin  
Aleix Pol  
Lorn Potter  
Liang Qi  
Topi Reinio  
Shawn Rutledge  
Craig Scott  
Luca Di Sera  
Dmitry Shachnev  
Andy Shaw  
Ivan Solovev  
Tarja Sundqvist  
Jan Arve Sæther  
Morten Johan Sørvig  
Tyson Tan  
Ivan Tkachenko  
Jens Trillmann  
Paul Olav Tvete  
Sami Varanka  
Doris Verria  
Tor Arne Vestbø  
Juha Vuolle  
Edward Welbourne  
