Release note
============
Qt 5.15.17 release is a patch release made on the top of Qt 5.15.16. As a patch  
release, Qt 5.15.17 does not add any new functionality but provides bug fixes  
and other improvements.  
  
For detailed information about Qt, see the Qt 5.15 online documentation:  
https://doc.qt.io/qt-5/index.html. 

Important Changes
-----------------

### Security fixes  
  
*  CVE-2024-25580 in qtbase  
*  CVE-2023-51714 in qtbase  
*  CVE-2024-36048 in qtnetworkauth  

### qtbase
* d5d70450651 SQLite: Update SQLite to v3.44.0
Updated SQLite to v3.44.0

* 396e8cc57db SQLite: Update SQLite to v3.44.1
Updated SQLite to v3.44.1

* d369389a3f0 SQLite: Update SQLite to v3.44.2
Updated SQLite to v3.44.2

* 043fdbad553 Update Zlib to 1.3.1
zlib was updated to version 1.3.1.

* 96a21d71968 SQLite: Update SQLite to v3.45.0
Updated SQLite to v3.45.0

* d42cfb5ccbc windows: Avoid infinite recursion with certain fonts
Fixed an issue where an infinite recursion could occur if the system
had a font with multiple preferred names in non-English languages.

* cbb8025ab60 Update public suffix list
Updated the public suffix list to upstream SHA
883ced078a83f9d79a98933145425c221a5e51f0.

* 3a7246b58f9 Update bundled libpng to version 1.6.41
libpng was updated to version 1.6.41

* 1c8e420433b Update bundled libpng to version 1.6.42
libpng was updated to version 1.6.42

* d40b54a0e5b Update bundled libjpeg-turbo to version 3.0.2
libjpeg-turbo was updated to version 3.0.2

* 5b06f836b98 SQLite: Update SQLite to v3.45.1
Updated SQLite to v3.45.1

* e64c054631e Update bundled libpng to version 1.6.43
libpng was updated to version 1.6.43

* b3573f5ad82 SQLite: Update SQLite to v3.45.2
Updated SQLite to v3.45.2

* 1b6f0972849 PCRE2: upgrade to 10.43
PCRE2 was updated to version 10.43.

* 4055c760f20 Update md4c to 0.5.2
md4c was updated to 0.5.2.

* 6b36951d45b SQLite: Update SQLite to v3.45.3
Updated SQLite to v3.45.3

### qtdeclarative
* 73eeb35f09 Flickable: don't allow dragging with mouse buttons other
than left
Flickable is meant to be dragged (flicked) by touch events; and as a
matter of legacy support, for now it can also be dragged by the left
mouse button. Dragging with other mouse buttons, such as the right and
middle buttons, is not allowed.

### qtmultimedia
* 6b950406b Fix device file contention when setting parameters on v4l
cameras
Use GstElement "device-fd" property where possible to avoid multiple
access to device file

### qtdoc
* 2416765f Update iOS supported platforms and toolchain to iOS 17/Xcode
15
Xcode 15 is now both supported and required for Qt for iOS. To develop
for iOS 17 devices, please use Qt Creator 13, or generate an Xcode
project using qmake or CMake and use Xcode directly.

### qtimageformats
* 348a2b3 Update bundled libwebp to version 1.4.0
Update bundled libwebp to version 1.4.0

### qtwebengine
* 2294cc4ed Add option to chose python version for building 5.15
WebEngine
Adds the configure option --webengine-python-version to allow the user
to select the python version for building.

* 71dd46b37 Update Chromium  
Includes the following fixes in the qtwebengine-chromium submodule:  
  CVE-2023-6345: Integer overflow in Skia  
  CVE-2023-6347: Use after free in Mojo  
  CVE-2023-6510: Use after free in Media Capture  
  CVE-2023-6702: Type Confusion in V8  
  CVE-2023-7024: Heap buffer overflow in WebRTC  
  CVE-2024-1060: Use after free in Canvas  
  CVE-2024-1283: Heap buffer overflow in Skia  
  CVE-2024-1077: Use after free in Network  
  CVE-2024-0807: Use after free in WebAudio  
  CVE-2024-0808: Integer underflow in WebUI  
  CVE-2024-0222: Use after free in ANGLE  
  CVE-2024-0224: Use after free in WebAudio  
  CVE-2024-0333: Insufficient data validation in Extensions  
  CVE-2024-0518: Type Confusion in V8  
  CVE-2024-0519: Out of bounds memory access in V8  
  CVE-2024-1059: Use after free in WebRTC  
  Security bug 1488199  
  Security bug 1505632  
  Security bug 1506535  
  Security bug 1511689  
  Security bug 1518994  
  Security bug 1519980  
  Security bug 325296797  
  
* ece335f5a Update Chromium  
Includes the following fixes in the qtwebengine-chromium submodule:  
  CVE-2023-710  
  Security bug 41495984  


Fixes
-----

### qtbase
* QTBUG-124757 Update Harfbuzz to 8.4.0
* QTBUG-78737 Windows: Two menus instead of one appear by clicking on
the QSystemTrayIcon
* QTBUG-118993 MSVC warns as error on stdext::checked_array_iterator in
QtCore/qvector.h
* QTBUG-105395 WM_TRANSIENT_FOR is not kept in sync
* QTBUG-111528 Android font does not depend on locale/OS preference but
is hardcoded
* QTBUG-104895 Text rendering letter-spacing error
* QTBUG-120554 Text spacing changes between 5.15.10 and 5.15.16 versions
* QTBUG-118238 【Windows】stack overflow after launch Any Qt Application
(or Official Demo)
* QTBUG-119864 QPushButton or QToolButton does not receive mouse events
after calling setMenu().
* QTBUG-122451 Floating point in raster drawBitmap together with strict
QImage::scanLine causes assertion "i >= 0 && i < height()"
* QTBUG-96348 QWindowsSystemTrayIcon::showMessage: Windows Handle leak
* QTBUG-62945 Windows: QSystemTrayIcon::showMessage causes GDI-Object
leak
* QTBUG-123032 [REG: 6.6.1->6.6.2] Override cursor changes together with
window creation and destruction crashes on KDE
* QTBUG-114253 [REG: 5.11->6] Performance issue with loading images in
static build
* QTBUG-117702 qbittorrent dumped core

### qtsvg
* QTBUG-122752 [Reg: 6.4.2 -> 6.5.3] QFont::setPixelSize warning when
rendering svg files with painter font size set in pixels

### qtdeclarative
* QTBUG-120349 Window Qml Type doc is missing the default visible
property value
* QTBUG-120296 Qt Quick Widgets Example  -  Grab Framebuffer is
susceptible to crash
* QTBUG-119326 application crash when using QML-Debugger: Component vs
.qml
* QTBUG-120450 Allocating or deallocating a QJSEngine object causes a
crash if the application has called mlockall(MCL_CURRENT|MCL_FUTURE)
* QTBUG-123111 Particle System Application stuck on GUI thread
* QTBUG-84339 tst_qmlmin::qmlMinify is flaky
* QTBUG-97252 Swipeview stops responding after right-clicking

### qtmultimedia
* QTBUG-121750 QCameraImageProcessing fails to set settings on linux
v4l2 camera
* QTBUG-119747 Qt build produces JSON file and duplicate recipe warnings

### qtdoc
* QTBUG-93638 Typos in Debian package list

### qtwayland
* QTBUG-123007 Under Wayland Qt does not correctly handle key modifiers
during key repeating
* QTBUG-107858 qtwayland caches clipboard content

### qtquickcontrols2
* QTBUG-110114 Qt Quick Controls Button: Unable to override
Accessible.role
* QTBUG-84858 [REG 5.14->5.15] crash on close in QQuickItemLayer
destructor on Linux

### qtpurchasing
* QTBUG-115373 Hangman Demo uses unsupported version of Google Play
Billing Library

### qtscxml
* QTBUG-118050 Empty script element ends up invoking Q_UNREACHABLE()

### qtremoteobjects
* QTBUG-116151 Replica can crash with QHostAddress being called with a
<null reference>
* QTBUG-120242 SubClassReplicaTest crashes

### qtopcua
* QTBUG-104418 tst_opcua:AbsoluteNodeTest is flaky on Mac

Known Issues
------------

 * Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-5.15/supported-platforms.html  
  
* The RTA (release test automation) reported issues in Qt 5.15.x:  
https://bugreports.qt.io/issues/?filter=21874  
  
* Qt 5.15.17 Open issues in Jira:  
https://bugreports.qt.io/issues/?filter=26029  

Credits for the  release goes to:
---------------------------------

Eirik Aavitsland
Vladimir Belyavsky
Nicholas Bennett
Eskil Abrahamsen Blomfeldt
Joerg Bornemann
Kai Uwe Broulik
Michael Brüning
Alexandru Croitor
Giuseppe D'Angelo
Christian Ehrlicher
Ilya Fedin
Austin Goddard
Jani Heikkinen
Ulf Hermann
Volker Hilsheimer
Samuli Hölttä
Jonas Karlsson
Friedemann Kleint
Jarek Kobus
Jani Korteniemi
Jaroslaw Kubik
Kai Köhne
Inho Lee
Thiago Macieira
Safiyyah Moosa
Marc Mutz
Antonio Napolitano
Mårten Nordheim
Lauri Pohjanheimo
MohammadHossein Qanbari
Liang Qi
Shawn Rutledge
Ahmad Samir
Andy Shaw
Ziming Song
Axel Spoerl
Tarja Sundqvist
Jan Arve Sæther
Ivan Tkachenko
Elias Toivola
Esa Törmänen
Tor Arne Vestbø
Semih Yavuz
