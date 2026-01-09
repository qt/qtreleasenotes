Release note
============
Qt 6.2.12 release is a patch release made on the top of Qt 6.2.11. As a patch
release, Qt 6.2.12 does not add any new functionality but provides bug fixes
and other improvements.
For detailed information about Qt, see the Qt 6.2 online documentation:
https://doc.qt.io/qt-6.2/.

Important Changes
-----------------

### Security fixes  
  
* CVE-2024-25580 in qtbase

### qtbase
* a5408f4c95a SQLite: Update SQLite to v3.44.2
Updated SQLite to v3.44.2

* bc82ff6ee2d windows: Avoid infinite recursion with certain fonts
Fixed an issue where an infinite recursion could occur if the system
had a font with multiple preferred names in non-English languages.

* d385265d406 Doc: Update Copyright in md4c license text
Updated md4c (optional part of Qt Gui) to version 0.5.1.

* 472ad5938ed Update Zlib to 1.3.1
zlib was updated to version 1.3.1.

* 6406d7ace37 SQLite: Update SQLite to v3.45.0
Updated SQLite to v3.45.0

* f3f584c32a6 Update public suffix list
Updated the public suffix list to upstream SHA
883ced078a83f9d79a98933145425c221a5e51f0.

* 38048010f05 QBitArray: avoid overflow in size-to-storage calculations
Fixed a bug with QBitArrays whose size() came within 7 of the
size_type's maximum.

* 2f1cd87411b Update bundled libpng to version 1.6.41
libpng was updated to version 1.6.41

* 051fa3cfa89 SQLite: Update SQLite to v3.45.1
Updated SQLite to v3.45.1

* 9e181699d03 Update md4c to 0.5.2
md4c was updated to 0.5.2.

* 1bd15d9fae7 QBitArray: fix potential truncation in QDataStream op>>()
Fixed undetected overflows in the deserialisation (opertor>>()) from
QDataStream.

* 7c75dab2fd4 Update bundled libjpeg-turbo to version 3.0.2
libjpeg-turbo was updated to version 3.0.2

* be146e820c7 Update bundled libpng to version 1.6.42
libpng was updated to version 1.6.42

* 7707050cdfa QBitArray: don't create invalid Qt 5 streams
Now refuses to stream a QBitArray with size() > INT_MAX to a
Qt-5-compatible QDataStream.

* ecfd3fb2f53 PCRE2: upgrade to 10.43
PCRE2 was updated to version 10.43.

* d15a975ed75 Update bundled libpng to version 1.6.43
libpng was updated to version 1.6.43

### qtdoc
* c23fba78 Update iOS supported platforms and toolchain to iOS 17/Xcode
15
Xcode 15 is now both supported and required for Qt for iOS. To develop
for iOS 17 devices, please use Qt Creator 13, or generate an Xcode
project using qmake or CMake and use Xcode directly.


Fixes
-----

### qtbase
* [QTBUG-111528](https://bugreports.qt.io/browse/QTBUG-111528) Android font does not depend on locale/OS preference but
is hardcoded
* [QTBUG-117713](https://bugreports.qt.io/browse/QTBUG-117713) [REG: 5->6] Scaling images with Qt::SmoothTransformation
breaks them if scaled to smaller than 50% size
* [QTBUG-118133](https://bugreports.qt.io/browse/QTBUG-118133) Windows QPA:  QSystemIconTrayIcon::show() not working
after calling hide()
* [QTBUG-102831](https://bugreports.qt.io/browse/QTBUG-102831) QCompleter's suggestion list hides native Chinese Input
method
* [QTBUG-118568](https://bugreports.qt.io/browse/QTBUG-118568) qvulkanwindow  repeatedly recreate swapchain
* [QTBUG-115260](https://bugreports.qt.io/browse/QTBUG-115260) Hang during drag and drop [REG]
* [QTBUG-87334](https://bugreports.qt.io/browse/QTBUG-87334) Graphical issue on some Android smartphones: white line
at the top and the right side of the screen
* [QTBUG-97451](https://bugreports.qt.io/browse/QTBUG-97451) QString(QByteArray) constructor behavior change between
Qt5 and Qt6
* [QTBUG-115156](https://bugreports.qt.io/browse/QTBUG-115156) Last character missing with JAWS
* [QTBUG-119464](https://bugreports.qt.io/browse/QTBUG-119464) QSslSocket::setCiphers() documentation uses weak cyphers
* [QTBUG-104895](https://bugreports.qt.io/browse/QTBUG-104895) Text rendering letter-spacing error
* [QTBUG-120554](https://bugreports.qt.io/browse/QTBUG-120554) Text spacing changes between 5.15.10 and 5.15.16
versions
* [QTBUG-120572](https://bugreports.qt.io/browse/QTBUG-120572) [QDoc] Redundant text in QTabBar detailed description
* [QTBUG-120614](https://bugreports.qt.io/browse/QTBUG-120614) QImage::convertToFormat: wrong conversion from RGBA64 to
RGBA16FPx4
* [QTBUG-118458](https://bugreports.qt.io/browse/QTBUG-118458) TLS Invalid Token
* [QTBUG-119371](https://bugreports.qt.io/browse/QTBUG-119371) [macOS] (File|Folder)Dialog.currentFolder holds stale
data
* [QTBUG-118238](https://bugreports.qt.io/browse/QTBUG-118238) 【Windows】stack overflow after launch Any Qt Application
(or Official Demo)
* [QTBUG-120335](https://bugreports.qt.io/browse/QTBUG-120335) On certain machines QtConcurrent crashes if no free
threads on thread pool
* [QTBUG-121515](https://bugreports.qt.io/browse/QTBUG-121515) [Reg 6.6.1 -> 6.6.2] QNetworkAccessManager never
finishes request if server sends status code 401 without a challenge
* [QTBUG-122254](https://bugreports.qt.io/browse/QTBUG-122254) Documentation example of
QCborStreamReader::readString()/QCborStreamReader::readByteArray is
wrong
* [QTBUG-119864](https://bugreports.qt.io/browse/QTBUG-119864) QPushButton or QToolButton does not receive mouse events
after calling setMenu().
* [QTBUG-122451](https://bugreports.qt.io/browse/QTBUG-122451) Floating point in raster drawBitmap together with strict
QImage::scanLine causes assertion "i >= 0 && i < height()"
* [QTBUG-96348](https://bugreports.qt.io/browse/QTBUG-96348) QWindowsSystemTrayIcon::showMessage: Windows Handle leak
* [QTBUG-62945](https://bugreports.qt.io/browse/QTBUG-62945) Windows: QSystemTrayIcon::showMessage causes GDI-Object
leak
* [QTBUG-91627](https://bugreports.qt.io/browse/QTBUG-91627) [OpenGL] Crash when creating context with contextinfo
example app on Android
* [QTBUG-117702](https://bugreports.qt.io/browse/QTBUG-117702) qbittorrent dumped core
* [QTBUG-114583](https://bugreports.qt.io/browse/QTBUG-114583) Headers use things in <iterator> without including it
* [QTBUG-114253](https://bugreports.qt.io/browse/QTBUG-114253) [REG: 5.11->6] Performance issue with loading images in
static build
* [QTBUG-109877](https://bugreports.qt.io/browse/QTBUG-109877) macOS: QFileDialog::getSaveFileName() truncates a
compound extension
* [QTBUG-109708](https://bugreports.qt.io/browse/QTBUG-109708) Startup crash in QRhiD3D11::endFrame() with nullptr
access

### qtsvg
* [QTBUG-121981](https://bugreports.qt.io/browse/QTBUG-121981) QtSvg parser does not handle nested svg elements
correctly
* [QTBUG-120507](https://bugreports.qt.io/browse/QTBUG-120507) [REG 6.2.2 -> 6.2.3] Trying to render particular svg
file takes much longer than before

### qtdeclarative
* [QTBUG-112673](https://bugreports.qt.io/browse/QTBUG-112673) Drag.imageSource example - no image on first drag
* [QTBUG-115491](https://bugreports.qt.io/browse/QTBUG-115491) Drag.imageSource Only Works On Second try
* [QTBUG-118897](https://bugreports.qt.io/browse/QTBUG-118897) Qt Quick TableView performance issue when updating
ContentY in onModelChanged
* [QTBUG-117387](https://bugreports.qt.io/browse/QTBUG-117387) TapHandler and DragHandler interoperability breaks
* [QTBUG-66360](https://bugreports.qt.io/browse/QTBUG-66360) PointHandler goes inactive releasing mouse button when
multiple pressed
* [QTBUG-83980](https://bugreports.qt.io/browse/QTBUG-83980) HoverHandler: sometimes point.position returns (0, 0)
* [QTBUG-119363](https://bugreports.qt.io/browse/QTBUG-119363) UniformAnimator makes app crash when being destroyed by
other component
* [QTBUG-120349](https://bugreports.qt.io/browse/QTBUG-120349) Window Qml Type doc is missing the default visible
property value
* [QTBUG-120296](https://bugreports.qt.io/browse/QTBUG-120296) Qt Quick Widgets Example  -  Grab Framebuffer is
susceptible to crash
* [QTBUG-119372](https://bugreports.qt.io/browse/QTBUG-119372) build fails with Q_IMPORT_QML_PLUGIN macro
* [QTBUG-120346](https://bugreports.qt.io/browse/QTBUG-120346)  hovered property of HoverHandler stays true when
sliding by touch outside of hover area
* [QTBUG-111729](https://bugreports.qt.io/browse/QTBUG-111729) Assertion failed in QJSEngine when repeatedly deleting &
adding property getters on an object
* [QTBUG-119326](https://bugreports.qt.io/browse/QTBUG-119326) application crash when using QML-Debugger: Component vs
.qml
* [QTBUG-121710](https://bugreports.qt.io/browse/QTBUG-121710) [Reg 6.6.0 -> 6.6.1] Aliasing to enums does not work as
in Qt 6.6.0 an earlier anymore
* [QTBUG-120450](https://bugreports.qt.io/browse/QTBUG-120450) Allocating or deallocating a QJSEngine object causes a
crash if the application has called mlockall(MCL_CURRENT|MCL_FUTURE)
* [QTBUG-120105](https://bugreports.qt.io/browse/QTBUG-120105) Unreliable QML Timer / qmltest wait() / QTest:qWait()
with offscreen platform

### qtmultimedia
* [QTBUG-98437](https://bugreports.qt.io/browse/QTBUG-98437) QMediaPlayer does not emit destroyed signal

### qtdoc
* [QTBUG-120372](https://bugreports.qt.io/browse/QTBUG-120372) Typo in the document
* [QTBUG-121578](https://bugreports.qt.io/browse/QTBUG-121578) demos/hangman fails to build on Android and macOS
* [QTBUG-115373](https://bugreports.qt.io/browse/QTBUG-115373) Hangman Demo uses unsupported version of Google Play
Billing Library

### qtconnectivity
* [QTBUG-119063](https://bugreports.qt.io/browse/QTBUG-119063) Segfault in Bluetooth module's Windows COM de-init

### qtwayland
* [QTBUG-120397](https://bugreports.qt.io/browse/QTBUG-120397) "output" property seems to be missing in
WaylandQuickItem QML type documentation

### qtwebengine
* [QTBUG-108843](https://bugreports.qt.io/browse/QTBUG-108843) [WebRTC] Crash inside
RTCStatsCollector::ProduceAudioRTPStreamStats_n
* [QTBUG-112522](https://bugreports.qt.io/browse/QTBUG-112522) Webengine Widgets Client Certificate Example:
Compilation Fails
* [QTBUG-111894](https://bugreports.qt.io/browse/QTBUG-111894) [REG 6.4.3->6.4.2] webenginequick/quicknanobrowser not
launching
* [QTBUG-112661](https://bugreports.qt.io/browse/QTBUG-112661) WebEngine Quick Nano Browser Example: Crashes
* [QTBUG-114883](https://bugreports.qt.io/browse/QTBUG-114883) [REG 6.2.8 -> 6.2.9] shadow build fails on windows,
webengine
* [QTBUG-120420](https://bugreports.qt.io/browse/QTBUG-120420) QtWebEngine inspector crashes

* QtWebEngine security patch version updated to 122.0.6261.128 
* CVE-2023-6510: Use after free in Media Capture  
* CVE-2023-6512: Inappropriate implementation in Web Browser UI  
* CVE-2023-6702: Type Confusion in V8  
* CVE-2023-6703: Use after free in Blink  
* CVE-2024-0222: Use after free in ANGLE  
* CVE-2024-0223: Heap buffer overflow in ANGLE  
* CVE-2024-0224: Use after free in WebAudio  
* CVE-2024-0333: Insufficient data validation in Extensions  
* CVE-2024-0518: Type Confusion in V8  
* CVE-2024-0519: Out of bounds memory access in V8  
* CVE-2024-0807: Use after free in WebAudio  
* CVE-2024-0808: Integer underflow in WebUI  
* CVE-2024-0810: Insufficient policy enforcement in DevTools  
* CVE-2024-1060: Use after free in Canvas  
* CVE-2024-1077: Use after free in Network  
* CVE-2024-1283: Heap buffer overflow in Skia  
* CVE-2024-1284: Use after free in Mojo  
* CVE-2024-1672: Inappropriate implementation in Content Security Policy  
* CVE-2024-1676: Inappropriate implementation in Navigation  
* CVE-2024-1676: Inappropriate implementation in Navigation  
* CVE-2024-25062  
* Security bug 1485266  
* Security bug 1488199  
* Security bug 1504473 / 40945008  
* Security bug 1505632  
* Security bug 1506535  
* Security bug 1508758 / 41481379  
* Security bug 1511389  
* Security bug 1511689  
* Security bug 1518994  
* Security bug 1519980  
* Security bug 325094430  
* Security bug 325296797  

### qtremoteobjects
* [QTBUG-120242](https://bugreports.qt.io/browse/QTBUG-120242) SubClassReplicaTest crashes

### qtquick3d
* [QTBUG-120109](https://bugreports.qt.io/browse/QTBUG-120109) WasdController: Models stutter in Qt Quick 3D Physics
example

### qtmqtt
* [QTBUG-104478](https://bugreports.qt.io/browse/QTBUG-104478) Mqtt topic wildcard failure

Known Issues
------------

* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-6.2/supported-platforms.html  
  
* The RTA (release test automation) reported issues in Qt 6.2.x:  
https://qt-project.atlassian.net/issues/?filter=16060  
  
* Qt 6.2.12 Open issues in Jira:  
https://qt-project.atlassian.net/issues/?filter=16095  

Credits for the  release goes to:
---------------------------------

Eirik Aavitsland  
Laszlo Agocs  
Vladimir Belyavsky  
Eskil Abrahamsen Blomfeldt  
Assam Boudjelthia  
Kai Uwe Broulik  
Michael Brüning  
Kaloyan Chehlarski  
Giuseppe D'Angelo  
Artem Dyomin  
Alexey Edelev  
Christian Ehrlicher  
Hatem ElKharashy  
Andreas Eliasson  
Ilya Fedin  
Richard Moe Gustavsen  
Andre Hartmann  
Ulf Hermann  
Volker Hilsheimer  
Samuli Hölttä  
Allan Sandfeld Jensen  
Maurice Kalinowski  
Jonas Karlsson  
Michal Klocek  
Jarek Kobus  
Jani Korteniemi  
Fabian Kosmale  
Mike Krus  
Santhosh Kumar  
Kai Köhne  
Wladimir Leuschner  
Thiago Macieira  
Marc Mutz  
Antonio Napolitano  
Mårten Nordheim  
Timur Pocheptsov  
Lauri Pohjanheimo  
Joni Poikelin  
Liang Qi  
Matthias Rauter  
Shawn Rutledge  
Ahmad Samir  
Ws ShawnWoo  
Ivan Solovev  
Ziming Song  
Axel Spoerl  
Christian Strømme  
Tarja Sundqvist  
Jan Arve Sæther  
Morten Sørvig  
Ivan Tkachenko  
Tor Arne Vestbø  
Edward Welbourne  
Oliver Wolff  
