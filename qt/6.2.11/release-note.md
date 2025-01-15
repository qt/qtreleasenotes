Release note
============
Qt 6.2.11 release is a patch release made on the top of Qt 6.2.10. As a patch
release, Qt 6.2.11 does not add any new functionality but provides bug fixes
and other improvements.

For detailed information about Qt, see the Qt 6.2 online documentation:
https://doc.qt.io/qt-6.2/.

Important Changes
-----------------

### Security fixes

* CVE-2023-45872 in qtsvg
* CVE-2023-51714 in qtbase

### qtbase
* 4787d696376 SQLite: Update SQLite to v3.43.1
Updated SQLite to v3.43.1

* 2b282ca5926 Un-deprecate qSwap()
Un-deprecated qSwap().

* 2faaa1dc0b1 Use the actual target name as base name for android
deployment settings
The target name is used as a base name of android deployment settings,
but not the OUTPUT_NAME property.

* ecd5517aa76 SQLite: Update SQLite to v3.43.2
Updated SQLite to v3.43.2

* 31831580647 Update bundled libjpeg-turbo to version 3.0.1
libjpeg-turbo was updated to version 3.0.1

* 061fb5ae76d SQLite: Update SQLite to v3.44.0
Updated SQLite to v3.44.0

* 0fa011fe2c3 SQLite: Update SQLite to v3.44.1
Updated SQLite to v3.44.1

* dd2449b978e SQLite: Update SQLite to v3.44.2
Updated SQLite to v3.44.2

### qtsvg
* 3537bcb7 Fix crash when reading text with line breaks
Fixed a regression where the application would crash on certain SVG
files.

### qtwebengine
* 30c141c64 Fix corrupted load/fetch state on start up in case of
NoCache
Switching profile to NoCache do not longer implicitly removes cache
from old data store.


Fixes
-----

### qtbase
* [QTBUG-116056](https://bugreports.qt.io/browse/QTBUG-116056) signal
not found when deleting QAbstractItemModel
* [QTBUG-117200](https://bugreports.qt.io/browse/QTBUG-117200) Reg ->
6.6b4: Exit warning :"QItemSelectionModel: Selecting when no model has
been set will result in a no-op" from apps with  sort proxy filter model
* [QTBUG-109465](https://bugreports.qt.io/browse/QTBUG-109465) [REG:
5.15 → 6.2] binding doesn't update when it should
* [QTBUG-117509](https://bugreports.qt.io/browse/QTBUG-117509) Examples
that set OUTPUT_NAME will not build for Android
* [QTBUG-105457](https://bugreports.qt.io/browse/QTBUG-105457) Signals
might be processed in wrong order in QtDBus
* [QTBUG-107598](https://bugreports.qt.io/browse/QTBUG-107598)
HorizontalHeaderView crashes the app if it's synced to model changed
from bg thread
* [QTBUG-102196](https://bugreports.qt.io/browse/QTBUG-102196)
QDockWidget: wrong mouse cursor icon used when dock widget floating, has
custom title bar & contains window container
* [QTBUG-89904](https://bugreports.qt.io/browse/QTBUG-89904) Possible
error in Qt 6 "Container Classes" documentation
* [QTBUG-114437](https://bugreports.qt.io/browse/QTBUG-114437) REG:
Android: Layout in display cut mode being overridden to short edges
always
* [QTBUG-96877](https://bugreports.qt.io/browse/QTBUG-96877) Qt6 won't
render into cutout area (regression)
* [QTBUG-116788](https://bugreports.qt.io/browse/QTBUG-116788) Sporadic
crash on QNetworkReplyHttpImplPrivate::loadFromCacheIfAllowed() with
nullptr access
* [QTBUG-117745](https://bugreports.qt.io/browse/QTBUG-117745) Warning
message from app compiled with XCode 15
* [QTBUG-117950](https://bugreports.qt.io/browse/QTBUG-117950)
qxkbcommon.cpp:242:16: error: 'XKB_KEY_dead_lowline' was not declared in
this scope
* [QTBUG-109025](https://bugreports.qt.io/browse/QTBUG-109025) High DPI
scaling breaks Mouse/Stylus on Android
* [QTBUG-117787](https://bugreports.qt.io/browse/QTBUG-117787) Cached
network requests leak memory
* [QTBUG-115161](https://bugreports.qt.io/browse/QTBUG-115161) Crash in
QAccessibleComboBox::focusChild()
* [QTBUG-117242](https://bugreports.qt.io/browse/QTBUG-117242)
QtStartUpFunction is written as QtCleanUpFunction
* [QTBUG-106064](https://bugreports.qt.io/browse/QTBUG-106064) [REG]
Undocking QDockWidget with drag misplaces it (a lot)
* [QTBUG-118463](https://bugreports.qt.io/browse/QTBUG-118463)
QDockWidget; dock window "jumps" to wrong location when undocked instead
of following cursor position
* [QTBUG-117804](https://bugreports.qt.io/browse/QTBUG-117804)
Incomplete JPEG writing after libjpeg-turbo 3.0.0 upgrade
* [QTBUG-116167](https://bugreports.qt.io/browse/QTBUG-116167) Duplicate
requests of QNetworkAccessManager do not work
* [QTBUG-118244](https://bugreports.qt.io/browse/QTBUG-118244)
QVulkanWindow::grab() assumes RGBA which leads to inverted R and B
channels
* [QTBUG-111952](https://bugreports.qt.io/browse/QTBUG-111952) tslib
input plugin broken
* [QTBUG-113307](https://bugreports.qt.io/browse/QTBUG-113307) tslib
input not working
* [QTBUG-114971](https://bugreports.qt.io/browse/QTBUG-114971)
QAndroidBinder: implementation for native methods missing
* [QTBUG-117900](https://bugreports.qt.io/browse/QTBUG-117900) [REG
5.15.2->6.5.1] Behavioural inconsistency when reparenting QStandardItems
* [QTBUG-89145](https://bugreports.qt.io/browse/QTBUG-89145)
QStandardItemModel takeItem / takeChild does not emit the right signals
* [QTBUG-104641](https://bugreports.qt.io/browse/QTBUG-104641) QDial:
division by zero while changing minimal or maximum value
* [QTBUG-78737](https://bugreports.qt.io/browse/QTBUG-78737) Windows:
Two menus instead of one appear by clicking on the QSystemTrayIcon
* [QTBUG-118993](https://bugreports.qt.io/browse/QTBUG-118993) MSVC
warns as error on stdext::checked_array_iterator in QtCore/qvector.h
* [QTBUG-105395](https://bugreports.qt.io/browse/QTBUG-105395)
WM_TRANSIENT_FOR is not kept in sync
* [QTBUG-115752](https://bugreports.qt.io/browse/QTBUG-115752) stack-
use-after-return in tst_assetimport
* [QTBUG-119219](https://bugreports.qt.io/browse/QTBUG-119219) macOS:
NPE in QNSWindow applicationActivationChanged
* [QTBUG-116532](https://bugreports.qt.io/browse/QTBUG-116532)
tst_QStandardItemModel leaks memory in multiple test cases
* [QTBUG-114253](https://bugreports.qt.io/browse/QTBUG-114253) [REG:
5.11->6] Performance issue with loading images in static build

### qtsvg
* [QTBUG-117944](https://bugreports.qt.io/browse/QTBUG-117944) [Qt SVG]
QML Image bad source crashes application instead of error status
(QSvgHandler::parse)

### qtdeclarative
* [QTBUG-108896](https://bugreports.qt.io/browse/QTBUG-108896) [REG
6.2.4-6.3.2] Using PinchHandler for Flickable's child makes the
Flickable transparent for touch events
* [QTEXT-7](https://bugreports.qt.io/browse/QTEXT-7) TreeView: crash (as
opposed to only runtime warning) if keyword "required" is not satisfied
* [QTBUG-112840](https://bugreports.qt.io/browse/QTBUG-112840) Please
write the realistic usecase of Qt Quick Test to the documentation
* [QTBUG-83662](https://bugreports.qt.io/browse/QTBUG-83662) For
MultiPointTouchArea with a child PinchArea multiple pressed signals for
multiple touch points on mouse press
* [QTBUG-115485](https://bugreports.qt.io/browse/QTBUG-115485) QtQuick
shapes example has misleading file names
* [QTBUG-117642](https://bugreports.qt.io/browse/QTBUG-117642) Crash
when trying to trick property bindings
* [QTBUG-117130](https://bugreports.qt.io/browse/QTBUG-117130) crash in
tryLoadFromDiskCache with corrupted cache
* [QTBUG-117829](https://bugreports.qt.io/browse/QTBUG-117829) QML
engine mis-converts QQmlListProperty
* [QTBUG-117479](https://bugreports.qt.io/browse/QTBUG-117479)
Segmentation fault in qml debugger
* [QTBUG-117891](https://bugreports.qt.io/browse/QTBUG-117891) [REG
6.5.2 → 6.5.3] Unable to determine callable overload with QVariantMap
* [QTBUG-117788](https://bugreports.qt.io/browse/QTBUG-117788) Assert
due to cyclic dependencies
* [QTBUG-119024](https://bugreports.qt.io/browse/QTBUG-119024) Window
position is bypassed by Wayland.
* [QTBUG-115579](https://bugreports.qt.io/browse/QTBUG-115579) Rebinding
of property alias does not work for some aliases that refer to certain
(grouped) properties
* [QTBUG-117917](https://bugreports.qt.io/browse/QTBUG-117917)
HorizontalHeaderView with plain JavaScript array model crashes on flick
* [QTBUG-93856](https://bugreports.qt.io/browse/QTBUG-93856) Menus with
a certain fixed height, element height and window height not scrolled
when they should
* [QTBUG-117079](https://bugreports.qt.io/browse/QTBUG-117079)
tst_QQuickMultiPointTouchArea::inFlickable() crashes on Android
* [QTBUG-107863](https://bugreports.qt.io/browse/QTBUG-107863)
tst_QQuickMouseArea::disableParentOnPress is flaky on some platforms
* [QTBUG-107864](https://bugreports.qt.io/browse/QTBUG-107864)
QTest::touchEvent needs to take a const QPointingDevice *
* [QTBUG-106223](https://bugreports.qt.io/browse/QTBUG-106223) assertion
failed after Flickable takes grab from PinchHandler
* [QTBUG-117700](https://bugreports.qt.io/browse/QTBUG-117700)
StackView's enter transitions are broken when pushing/replacing onto an
empty stack
* [QTBUG-118163](https://bugreports.qt.io/browse/QTBUG-118163) Flaky
race-condition in QuickTest when running tst_inputpanel built with ASAN
* [QTBUG-118897](https://bugreports.qt.io/browse/QTBUG-118897) Qt Quick
TableView performance issue when updating ContentY in onModelChanged

### qtmultimedia
* [QTBUG-114083](https://bugreports.qt.io/browse/QTBUG-114083)
[QtDeclarativeCamera] Popup list of available cameras is not available
after changing the orientation
* [QTBUG-119087](https://bugreports.qt.io/browse/QTBUG-119087)
MediaPlayer-Graphic&Multimedia-example Volume slider is being compressed
and becomes unusable
* [QTBUG-113782](https://bugreports.qt.io/browse/QTBUG-113782) error: no
member named 'unary_function' in namespace 'std'
* [QTBUG-116315](https://bugreports.qt.io/browse/QTBUG-116315) [QML
Camera Example] Camera preview smaller than the window for preview

### qttools
* [QTBUG-116833](https://bugreports.qt.io/browse/QTBUG-116833) QDoc
generates .sha1 files for each qhp file, but they all contain wrong hash

### qtdoc
* [QTBUG-93471](https://bugreports.qt.io/browse/QTBUG-93471) Darwin
linker warns about global weak symbols when linking an executable
against a static Qt
* [QTBUG-105006](https://bugreports.qt.io/browse/QTBUG-105006) iOS
archive builds fail with qt_add_qml_module()s in static libs
* [QTBUG-110921](https://bugreports.qt.io/browse/QTBUG-110921)
Documentation for building iOS apps is plain wrong
* [QTBUG-54267](https://bugreports.qt.io/browse/QTBUG-54267) Qt Quick
Calqlatr example does not properly reflect the current way of using Qt
Quick
* [QTBUG-116784](https://bugreports.qt.io/browse/QTBUG-116784) iOS built
with CMAKE is not uploadable on Appstore (Transporter)
* [QTBUG-114437](https://bugreports.qt.io/browse/QTBUG-114437) REG:
Android: Layout in display cut mode being overridden to short edges
always
* [QTBUG-96877](https://bugreports.qt.io/browse/QTBUG-96877) Qt6 won't
render into cutout area (regression)

### qtpositioning
* [QTBUG-116645](https://bugreports.qt.io/browse/QTBUG-116645) [Android]
providerList() returns NULL list

### qtwayland
* [QTBUG-112161](https://bugreports.qt.io/browse/QTBUG-112161) Drag and
drop with wayland display error

### qtserialport
* [QTBUG-115205](https://bugreports.qt.io/browse/QTBUG-115205)
QSerialPort does not properly set baud rate

### qtwebengine
* [QTBUG-117489](https://bugreports.qt.io/browse/QTBUG-117489) [REG 6.4
-> 6.5] Invalid QDataStream data when serializing uninited
QWebEngineHistory
* [QTBUG-118455](https://bugreports.qt.io/browse/QTBUG-118455) Crash in
Compositor::Observer::compositor() with nullptr access
* [QTBUG-118850](https://bugreports.qt.io/browse/QTBUG-118850) WebEngine
build fails in yocto for lts-6.5
* [QTBUG-119023](https://bugreports.qt.io/browse/QTBUG-119023) WebEngine
accessibility crash when clicking on a link in a list on macOS
* [QTBUG-113859](https://bugreports.qt.io/browse/QTBUG-113859) [REG
6.4->6.5] Accessibility crash when clicking on a link in a list on macOS
* [QTBUG-117751](https://bugreports.qt.io/browse/QTBUG-117751) building
with -no-opengl produces errors in web_engine_context.cpp
* [QTBUG-119536](https://bugreports.qt.io/browse/QTBUG-119536) Lack of
documentation regarding QPdfBookmarkModel's document property
* [QTBUG-117673](https://bugreports.qt.io/browse/QTBUG-117673) Only
black screen and mouse is captured on wayland
* [QTBUG-116478](https://bugreports.qt.io/browse/QTBUG-116478) [Reg
5.14.2 -> 5.15.0] Significant performance decrease when loading
QtWebEngine pages simultaneously in many windows
* [QTBUG-114865](https://bugreports.qt.io/browse/QTBUG-114865) macos:
Building QtWebEngine  with sanitizer enabled fails
* [QTBUG-116565](https://bugreports.qt.io/browse/QTBUG-116565) Cannot
sign a WebEngine-based application with Qt 6.5.2 (but OK with Qt 6.4.3,
6.3.2, 5.15.2)
* [QTBUG-116595](https://bugreports.qt.io/browse/QTBUG-116595) QtPfd
build failure on 32-bit arm

* CVE-2023-5217: Heap buffer overflow in vp8 encoding in libvpx
* CVE-2023-5218: Use after free in Site Isolation
* CVE-2023-5474: Heap buffer overflow in PDF
* CVE-2023-5475: Inappropriate implementation in DevTools
* CVE-2023-5482: Insufficient data validation in USB
* CVE-2023-5484: Inappropriate implementation in Navigation
* CVE-2023-5487: Inappropriate implementation in Fullscreen
* CVE-2023-5849: Integer overflow in USB
* CVE-2023-5996: Use after free in WebAudio
* CVE-2023-5997: Use after free in Garbage Collection
* CVE-2023-6112: Use after free in Navigation
* CVE-2023-6345: Integer overflow in Skia
* CVE-2023-6347: Use after free in Mojo
* CVE-2023-45853: Buffer overflow in MiniZip
* Security bug 1447972
* Security bug 1471305
* Security bug 1472365
* Security bug 1472366
* Security bug 1472368
* Security bug 1478470
* Security bug 1479104
* Security bug 1480184
* Security bug 1486316
* Qt WebEngine in 6.2.11 is using the same version as in 6.5.4

### qtcharts
* [QTBUG-113437](https://bugreports.qt.io/browse/QTBUG-113437) QML
XYSeries bestFitLineColor doc type
* [QTBUG-118669](https://bugreports.qt.io/browse/QTBUG-118669) Qt chart
crash on showing context menu

### qtscxml
* [QTBUG-118050](https://bugreports.qt.io/browse/QTBUG-118050) Empty
script element ends up invoking Q_UNREACHABLE()

### qtremoteobjects
* [QTBUG-116151](https://bugreports.qt.io/browse/QTBUG-116151) Replica
can crash with QHostAddress being called with a <null reference>

### qtquicktimeline
* [QTBUG-119204](https://bugreports.qt.io/browse/QTBUG-119204) Not
possible to exclude qtquicktimeline from the build

Known Issues
------------

* Check that your system meets Qt's requirements:
https://doc.qt.io/qt-6.2/supported-platforms.html

* The RTA (release test automation) reported issues in Qt 6.2.x:
https://bugreports.qt.io/issues/?filter=23315

* Qt 6.2.11 Open issues in Jira:
https://bugreports.qt.io/issues/?filter=25388

Credits for the  release goes to:
---------------------------------

Eirik Aavitsland  
Laszlo Agocs  
Vladimir Belyavsky  
Nicholas Bennett  
Eskil Abrahamsen Blomfeldt  
Assam Boudjelthia  
Kai Uwe Broulik  
Michael Brüning  
Olivier De Cannière  
Alexandru Croitor  
Mitch Curtis  
Artem Dyomin  
Alexey Edelev  
David Edmundson  
Christian Ehrlicher  
Andreas Eliasson  
Richard Moe Gustavsen  
Mikko Hallamaa  
Miikka Heikkinen  
Ulf Hermann  
Volker Hilsheimer  
Allan Sandfeld Jensen  
Jonas Karlsson  
Friedemann Kleint  
Michal Klocek  
Sze Howe Koh  
Fabian Kosmale  
Mike Krus  
Anton Kudryavtsev  
Santhosh Kumar  
Kai Köhne  
Ievgenii Meshcheriakov  
Bartlomiej Moskal  
Marc Mutz  
Martin Negyokru  
Mårten Nordheim  
Samuli Piippo  
Joni Poikelin  
Rami Potinkara  
MohammadHossein Qanbari  
Liang Qi  
Shawn Rutledge  
Ahmad Samir  
Andy Shaw  
Ivan Solovev  
Axel Spoerl  
Christian Strømme  
Tarja Sundqvist  
Lars Sutterud  
Orkun Tokdemir  
Paul Olav Tvete  
Peter Varga  
Tor Arne Vestbø  
Alexander Volkov  
Juha Vuolle  
Semih Yavuz  
