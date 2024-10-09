Release note
============
Qt 6.2.10 release is a patch release made on the top of Qt 6.2.9. As a patch
release, Qt 6.2.10 does not add any new functionality but provides bug fixes
and other improvements.

For detailed information about Qt, see the Qt 6.2 online documentation:
https://doc.qt.io/qt-6.2/.

Important Changes
-----------------

### Security fixes

* CVE-2023-38197 in qtbase

* CVE-2023-43114 in qtbase

* CVE-2023-37369 in qtbase

### qtbase
* dddaed1e302 PCRE2: upgrade to 10.42
PCRE2 has been updated to 10.42.

* 6db61454eab QVariant::fromStdVariant(): protect against accidental
fromValue() ADL pick-ups
The fromStdVariant() function used an unqualifed fromValue() call to
convert each alternative type in the std::variant. It now uses qualified
QVariant::fromValue() to avoid picking up unrelated fromValue()
overloads whose return value just happens to implicitly convert to
QVariant.

* 09b46a9f331 QPixmapCache: fix leaking of QStrings and Keys on clear()
Fixed QString key data not being freed on clear().

* e4579edb165 QFutureSynchronizer: fix aliasing problem in setFuture()
Fixed a crash in setFuture() if the argument was already a member of
QFutureSynchronizer::futures().

* 2a47a92734b Update bundled libpng to version 1.6.40
libpng was updated to version 1.6.40

* c336a57b269 QSslDiffieHellmanParameters: fix mem-leak
Fixed a memory leak in parsing of PEM-encoded Diffie-Hellman
parameters.

* 91942a24b4f Update bundled libjpeg-turbo to version 3.0.0
libjpeg-turbo was updated to version 3.0.0

* b0a0a0fcfee SQLite: Update SQLite to v3.43.0
Updated SQLite to v3.43.0

* 37bc7eb5db0 Update bundled zlib to version 1.3
zlib was updated to version 1.3.

* 863419667fc Fix crash when reading corrupt font data
Fixed a possible crash that could happen when loading corrupted font
data.

* a192b38f7cd SQLite: Update SQLite to v3.43.1
Updated SQLite to v3.43.1

### qtconnectivity
* 49e1560c QBluetoothUuid: remove default case labels and fix the
fallout
Fixed missing result of
characteristicToString(CharacteristicType::WeightScaleFeature).

### qtimageformats
* 2e8a74f Update bundled libwebp to version 1.3.1
Update bundled libwebp to version 1.3.1

* 6e5da9a Update bundled libtiff to version 4.5.1
Bundled libtiff was updated to version 4.5.1

* f151e86 Update bundled libtiff to version 4.6.0
Bundled libtiff was updated to version 4.6.0

* 67a9636 Update bundled libwebp to version 1.3.2
Update bundled libwebp to version 1.3.2

### qtwebengine
* 53b5d93d9 RenderWidgetHostViewQtDelegateItem: keep grabs
WebEngineView (or WebView backed by Qt WebEngine) no longer allows
components outside to take over the mouse or touch exclusive grab. For
example if the user starts dragging a scrollbar inside the web view,
that continues until release, regardless of any DragHandler, Flickable
etc.


Fixes
-----

### qtbase
* QTBUG-113630 Windows build with LLVM fails with platform header
missing after successfull configuration
* QTBUG-112246 ios: Assert if closing keyboard and touching the screen
with another finger
* QTBUG-112217 setTearOffEnabled() leading to crash
* QTBUG-114431 FindEGL.cmake fails for static linking with Qt
* QTBUG-112822 QProperty crashes
* QTBUG-109405 [Regression] 6.3.1 -> 6.4.1 Android - QSettings lost
* QTBUG-109369 QSettings - default file location changed between Qt5 and
Qt6 on Android
* QTBUG-112351 Incorrect description of QtConcurrent::run()
* QTBUG-111417 HTTP/2 request does not finish until closed by remote
host
* QTBUG-108482 Mention more clearly that only a subset of features of
supported HTML tags are implemented
* QTBUG-114583 Headers use things in <iterator> without including it
* QTBUG-109781 QXmlStreamReader asserts trying to construct XmlStringRef
of negative len on external input
* QTBUG-114829 [REG 6.5.1 -> 6.5.2] Crash/failed assert by passing
certain xml file to QXmlStreamReader
* QTBUG-113698 Nullptr dereference in qcoretextfontdatabase.mm
* QTBUG-92464 QCompleter breaking use of keyboard accents
* QTBUG-108522 [Regression: 4 - 5&6] QCompleter can not use input method
when completer popup is visible on Linux
* QTBUG-114991 QVariant<double> comparison uses <float> on  `-qreal
float`  platforms
* QTBUG-115062 Incorrect handling of
QT_FATAL_CRITICALS/QT_FATAL_WARNINGS (non-UB data race)
* QTBUG-115124 qtpaths JSON output is invalid
* QTBUG-114825 Blacklisting of tst_qquickpopup::hover doesn't work
* QTBUG-113461 QML TextField Popup
* QTBUG-92113 QXmlStreamReader freezes
* QTBUG-95188 Out-of-memory in QXmlStreamReader
* QTBUG-97482 Android: QPushButton with QMenu does not work on Qt6
* QTBUG-115263 QHostInfo is leaking QSlotObjectBase in
tst_QHostInfo::lookupConnectToFunctionPointerDeleted()
* QTBUG-115473 Missing QSet::removeIf() method
* QTBUG-115002 Can't import MTLDevice with QRhi Metal.
* QTBUG-115327 echoplugin uses an ambiguous project name
* QTBUG-115599 Possible SEGV (null pointer deref) in
QXcbConnection::initializeAllAtoms()
* QTBUG-114575 Value changes when cursor is moved in date/time field
* QTBUG-40315 doc: QFontMetrics::elidedText(...) does not work as
expected for ElideNone
* QTBUG-115516 QColorDialog: WA_Hover breaks color and luminance picker
* QTBUG-115597 QMenu crash if app loses focus immediately after
selecting sub-menu item
* QTBUG-115809 warning: ‘malloc’ may be used uninitialized [-Wmaybe-
uninitialized]
* QTBUG-114435 Regression 5.15.14: Cannot open Files from Android
FileDialog with spaces or umlauts
* QTBUG-115853 There is NO method current() for QVulkanInstance
* QTBUG-25944 QXmlStreamReader::readNextStartElement() works inelegantly
with isEndDocument()
* QTBUG-115058 QDockWidget group window still visible when empty
(regression)
* QTBUG-116181 Android: QFile can't open file in directory which is
chosen by QFileDialog::getExistingDirectory()
* QTBUG-115756 Android: QLineEdit setText() from textEdited signal does
not move cursor to the end
* QTBUG-116696 Menus have window type _NET_WM_WINDOW_TYPE_NORMAL instead
of _NET_WM_WINDOW_TYPE_POPUP_MENU
* QTBUG-39887 Regression bug: QWidget::setAttribute() does not set
Qt::WA_X11NetWmWindowType in Qt 5.
* QTBUG-114654 KeyRelease event not propagated to parent of QLineEdit
* QTBUG-115632 Long press textfield popup teleports after being drawn
for the first time
* QTBUG-105204 QProperty: Notfication missing if binding no longer has
any dependencies
* QTBUG-104982 [Regression] binding stops being evaluated
* QTBUG-116715 docs: qsettings path on embdded linux
* QTBUG-116166 Network tests fail with OpenSSL 3.1.1
* QTBUG-116773 Adding "Fuzzed" .otf font files causes access violation
exception
* QTBUG-112200 Possible memory leak with Fusion style
* QTBUG-115031 qtbase -unity-build-batch-size 103 fails
* QTBUG-114175 QWizard default Style not drawn correctly when scaling
other than 100%
* QTBUG-101926 "AutoMoc subprocess error" when building in CI
* QTBUG-54955 Mac: Wrong QDate string conversion with
Qt::SystemLocaleLongDate on dates prior to 1893-04-02
* QTBUG-93763 Systematic announcement of combobox selected element
* QTBUG-116277 QFileDialog not cleaned up when parent deleted

### qtsvg
* QTBUG-115648 QSvgRenderer::boundsOnElement() can return wrong results
with multiple child <text> elements
* QTBUG-113042 Loading particular svg file takes too long

### qtdeclarative
* QTBUG-113584 Typo in the code snippet
* QTBUG-113497 QGuiApplication::setLayoutDirection does not change the
window to RTL
* QTBUG-114430 heap-use-after-free when assigning undefined to width and
height of Control background item
* QTBUG-109995 Can not interact with tumblers inside interactive
flickable on touch
* QTBUG-113653 [REG 5.15->6.2.3] MultiPointTouchArea doesn't receive
gestureStarted signal when used inside PathView or Flickable
* QTBUG-114329 [Reg 5.15 -> 6.2] QML Binding on new object not re-
evaluated
* QTBUG-113854 V4 Crashes when using Reflect.ownKeys(...)
* QTBUG-114492 Automotive example's Dial background image has
downscaling artifacts
* QTBUG-114715 Doc: Stale info about QML module versioning
* QTBUG-114874 REG [5.15 → 6.x]: With `height: implicitHeight` binding
changes to implicitHeight won't trigger property interceptor (e.g.
Behavior + Animation)
* QTBUG-114687 Qt.application.screens does not update if primary screen
changes
* QTBUG-114910 Missing constructor params crashes program
* QTBUG-115179 Clip optimization in
QQuickDeliveryAgentPrivate::pointerTargets is too aggressive
* QTBUG-109306 Standard virtual keyboard typing does't generate standard
QML events.
* QTBUG-108144 Race condition when using QQuickMenu
* QTBUG-115320 memcpy-param-overlap in qv4runtime.cpp
* QTBUG-58718 Problems with JS array sorting after unshift
* QTBUG-115115 [Reg 5.15 -> 6.2]
QV4::Heap::QObjectMethod::ensureMethodsCache crash when calling a
function in a js file
* QTBUG-113439 Specifying RESOURCES to qt6_target_qml_sources does not
make file level dependency
* QTBUG-114258 Cannot click on buttons inside Flickable in QQuickWidget
with stylus
* QTBUG-115251 Infinite loop in QPropertyObserverPointer::notify on
startup
* QTBUG-115537 [QML Docs] Image.fillMode enum documentation has a broken
table formatting
* QTBUG-105090 tst_QQuickMenu AddressSanitizer: heap-use-after-free in
QQmlData::signalHasEndpoint(int)
* QTBUG-116228 Garbage collector can crash the QML Debugger
* QTBUG-111511 Object destructuring breaks qmlformat
* QTBUG-92998 Items in GridView shifts to the right when using RTL
layoutDirection
* QTBUG-115468 Dynamically adding items to SwipeView may add new items
behind the current item
* QTBUG-103268 QML item Menu doesn't close with touch screen on
CloseOnPressOutside
* QTBUG-105745 QtQuick.Dialogs.quickimpl plugin not linked in static
builds
* QTBUG-115319 Issue with number as a context property name
* QTBUG-106968 QSGSoftwareRenderContext textures leak
* QTBUG-96351 QML: strange "Binding loop detected" warning
* QTBUG-95107 ListView item pooling breaks fetchMore
* QTBUG-100392 Animations crash at runtime because list properties do
not emit onChanged signal when their items are destroyed
* QTBUG-106119 Crash when calling findChild from TestCase
* QTBUG-105361 qmlformat: Unnecessary replacement of 'let' with 'var',
leading to inline write errors
* QTBUG-77629 QML Flickable stealing touch events from PinchArea
* QTBUG-109655 Pinch gestures are broken in QML Photo Surface example
* QTBUG-85278 PinchArea inside Flickable not working properly
* QTBUG-106223 assertion failed after Flickable takes grab from
PinchHandler
* QTBUG-104982 [Regression] binding stops being evaluated
* QTBUG-106683 qt_add_qml_module: _automoc_json_extraction target and
resources are rebuilding every time with Visual Studio Generator
* QTBUG-115317 ListView can't reuse items when its integer model is
modified
* QTBUG-89193 ListView delegate position resets after displaced
transition
* QTBUG-111532 qmlsc when enabled gives many errors/warnings
* QTBUG-113226 Flickable emit flickStarted even though the child is
processing the pinch gesture
* QTBUG-112924 movementStarted/movementEnded signals are not emitted,
the flickStarted/flickEnded signals with flick behavior still occur.
* QTBUG-107863 tst_QQuickMouseArea::disableParentOnPress is flaky on
some platforms
* QTBUG-107864 QTest::touchEvent needs to take a const QPointingDevice *
* QTBUG-117079 tst_QQuickMultiPointTouchArea::inFlickable() crashes on
Android

### qtmultimedia
* QTBUG-114039 App crash after changing Media Player source
* QTBUG-99709 The size of the video missing in QMediaMetaData
* QTBUG-115122 Documentation: PlaybackRate is not only about audio
speed.
* QTBUG-109659 Audio capturing and playing does not work on Android
* QTBUG-113020 [Regression] Android: declarative-camera example does not
save picture/picture gets deleted on Qt 6.5

### qttools
* QTBUG-115465 Designer injects bogus "<normaloff>.</normaloff>." for
icon properties
* QTBUG-116305 Qt Creator 11.0.2  layout alignment disable

### qtdoc
* QTBUG-113588 Check attribution details for opengl32sw.dll
* QTBUG-99900 Leading zeroes for Android app "versionCode" are being
removed
* QTBUG-113257 Configure qt failed for arm64 architecture

### qtqa
* QTBUG-91268 qt5.git integration failing in '5.12'
* QTBUG-56434 Rendering malformed SVG file fails assert
* QTBUG-82978 Allow "-Wextra-semi-stmt" on Q_UNUSED
* QTBUG-86815 Rename all internal CMake functions to start with
qt_internal
* QTBUG-87965 [REG 5.15.1 -> 6.0] Crash in QTextDocument().setMarkdown()
* QTBUG-88656 Undefined behavior in QDateTime::fromString
* QTBUG-88253 [REG 5.15 -> 6.0] QCborStreamReader allocates 2 GiB for 8
B file
* QTBUG-88256 [REG 5.15 -> 6.0] QCborValue::fromCbor allocates 2 GiB for
8 B input
* QTBUG-89476 [REG 5.15 -> 6.0] Configure doesn't build for release by
default
* QTBUG-89789 Qt6.0.1, compiling the sources produces .so.6.0.0 libs
instead of .so.6.0.1
* QTBUG-89899 Integer-overflow in QFixed::QFixed
* QTBUG-90931 compiler given by CC/CXX is ignored by qmake
* QTBUG-91916 [REG 6.1 -> 6.2] Memory leak in QPainterPath
* QTBUG-88820 Undefined behavior in QDateTime::fromString
* QTBUG-88822 Undefined behavior in QDateTime::fromString
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake
counterpart
* QTBUG-93072 Invalid enum value in
QTextHtmlParser::tableCellBorderStyle
* QTBUG-93068 Memory leak QTextDocument::setHtml
* QTBUG-95239 Massive memory consumption when rendering small svg
* QTBUG-97458 String "6.2.0" found from 6.2.1 source package
* QTBUG-99799 Memory leak in QJsonDocument::fromJson()
* QTBUG-100217 [REG 6.2.2  -> 6.2.3] Integer overflow when rendering svg
image
* QTBUG-102484 Race condition in QSemaphore
* QTBUG-100698 Fix BIC tests

### qtpositioning
* QTBUG-114657 [SatelliteInfo] The app stops responding after some time
on macOS

### qtwayland
* QTBUG-97037 DragHandler / startSystemMove window move issue with QT6
Webengine on Wayland
* QTBUG-114671 Crash without input device connected
* QTBUG-114995 tst_qgraphicsanchorlayout crash with QtWayland failed on
Ubuntu 22.04, GNOME
* QTBUG-115757 [REG: 6.5.1-6.5.2] Drag and Drop segfaults programs
* QTBUG-101366 Failure with more than one EGL-based client buffer
integration

### qt3d
* QTBUG-116494 Documentation for QCylinderMesh misses Detailed
Description

### qtwebengine
* QTBUG-113704 Sending certain key events to QQuickView showing a
focused QtWebEngine causes crash
* QTBUG-113992 QTWebEngine crash when not working proxy is set
* QTBUG-113806 Chromium attributions missing from 'Licences used in Qt'
docs
* QTBUG-114339 FAIL!  : qmltests::WebEngineViewSingleFileUpload::test_ac
ceptSingleFileSelection(test.txt)
* QTBUG-103518 QML WebView scrolling events are picked up by DragHandler
and Flickables behind it
* QTBUG-114117 [WebEngine] Incorrect name of the app is shown in the
system location permission pop up
* QTBUG-114953 PdfMultiPageView: Very poor memory performance when
zooming in/out of long documents
* QTBUG-113512  WebEngineView not visible in Designer on macOS
* QTBUG-114471 Recipe browser starts in upside down mode
* QTBUG-113981 QPdfView does not scroll reliably with mouse wheel event
(two finger sliding on touchpad)
* QTBUG-113251 [REG 6.4 -> 6.5] Context menu functionality in devtools
broken
* QTBUG-115365 QWebEngineCertificateError is exported twice
* QTBUG-99555 [RE: 6.2.1->6.2.2] macdeployqt fails to produce
notarizable packages
* QTBUG-115844 qtwebengine ignores some key remaps
* QTBUG-115976 Dev tools not hidden with closing cross
* QTBUG-114752 Crash with  --device=software when running on battery
* QTBUG-114875 Cannot detect Visual Studio when configuring QPdf and
QWebEngine
* QTBUG-116598 Qt 6.2: Qt WebEngine attribution documentation not listed
on 'Licenses used in Qt'
* QTBUG-115753 ERROR: AddressSanitizer: heap-use-after-free  in
tst_origins
* QTBUG-115994 Duplicate character when long-pressing for accented char
on macOS/webengine
* QTBUG-112614 QPdfPageNavigator::backAvailableChanged and
forwardAvailableChanged are not always emitted for jumps
* QTBUG-116445 [REG][Windows] Crash on
NativeSkiaOutputDevice::releaseTexture() with nullptr access
* QTBUG-117119 Some Qt WebEngine documentation issues
* QTBUG-113416 [Reg 6.4->6.5] Static build fails at PDF module
* QTBUG-113551 Update documentation for limitation building QtPdf for
Android with supported  LTS versions
* QTBUG-105342 Test on qemu are very flacky
* QTBUG-113369 dark mode enabled causes crashes on specific sites
* QTBUG-115188 QtWebEngine use after free in Extensions GetPreferences
* QTBUG-104610 Does WebEngine support document download and print
operations in the document preview screen?
* QTBUG-117382 Clicking the print button in built-in PDF viewer crashes
* QTBUG-116478 [Reg 5.14.2 -> 5.15.0] Significant performance decrease
when loading QtWebEngine pages simultaneously in many windows

### qtwebview
* QTBUG-114495  FAIL!  : tst_QWebView::load()

### qtcharts
* QTBUG-114943 Crash in Qt Audio Example on iPhone with Qt Kit 6.2.9 for
iOS
* QTBUG-115072 Crash while clicking on scatter points to perform
selection

### qtremoteobjects
* QTBUG-115458 QRemoteObjectRegistry has incorrect info about
QRemoteObjectSourceLocation(s)

### qtquick3d
* QTBUG-92944 input problems in DynamicTexture example
* QTBUG-113987 Typo in the document
* QTBUG-110160 Continuous memory growth when the source of Loader 3D{}
continues to change
* QTBUG-113986 Typo in the document

Known Issues
------------

Credits for the  release goes to:
---------------------------------

Eirik Aavitsland
Karim Abdelrahman
Amir Masoud Abdol
Laszlo Agocs
Anu Aliyas
Nicholas Bennett
Eskil Abrahamsen Blomfeldt
Joerg Bornemann
Assam Boudjelthia
Kai Uwe Broulik
Michael Brüning
Olivier De Cannière
Alexandru Croitor
Mitch Curtis
Giuseppe D'Angelo
Szabolcs David
Artem Dyomin
Alexey Edelev
Christian Ehrlicher
Iikka Eklund
Hatem ElKharashy
Andreas Eliasson
Ilya Fedin
Simo Fält
Frederik Gladhorn
Richard Moe Gustavsen
Tang Haixiang
Heikki Halmet
Amanda Hamblin-Trué
Jani Heikkinen
Karsten Heimrich
Ulf Hermann
Volker Hilsheimer
Teemu Holappa
Allan Sandfeld Jensen
Friedemann Kleint
Michal Klocek
Lars Knoll
Seokha Ko
Kai Koehne
Sze Howe Koh
Fabian Kosmale
Santhosh Kumar
Kai Köhne
Inho Lee
Tony Leinonen
Kimmo Leppälä
Robert Loehning
Robert Löhning
Thiago Macieira
Ievgenii Meshcheriakov
Safiyyah Moosa
Bartlomiej Moskal
Marc Mutz
Antti Määttä
Martin Negyokru
Andy Nichols
Mårten Nordheim
Dennis Oberst
Timur Pocheptsov
Joni Poikelin
Aleix Pol
MohammadHossein Qanbari
Liang Qi
Topi Reinio
Shawn Rutledge
Toni Saario
Ahmad Samir
Lars Schmertmann
Andy Shaw
Venugopal Shivashankar
David Skoland
Daniel Smith
Ivan Solovev
Axel Spoerl
Christian Strømme
Tarja Sundqvist
Lars Sutterud
Jan Arve Sæther
Morten Sørvig
Paul Olav Tvete
Esa Törmänen
Peter Varga
Doris Verria
Tor Arne Vestbø
Ville Voutilainen
Jaishree Vyas
Edward Welbourne
Paul Wicking
Semih Yavuz
Vlad Zahorodnii
