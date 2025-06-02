Release note
============
Qt 6.5.6 release is a patch release made on the top of Qt 6.5.5.  
As a patch release, Qt 6.5.4 does not add any new functionality but provides  
bug fixes and other improvements and maintains both forward and backward  
compatibility (source and binary) with Qt 6.5.5.  
For detailed information about Qt 6.5, refer to the online documentation  
included in this distribution. The documentation is also available online:  
  
https://doc.qt.io/qt-6/index.html  
  
The Qt version 6.5 series is binary compatible with the 6.4.x series.  
Applications compiled for 6.4 will continue to run with 6.5.  
  
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

### Security fixes  
  
* CVE-2024-36048 in qtnetworkauth  
* CVE-2024-33861 in qtbase  
* CVE-2024-30161 in qtbase  

### qtbase
* b65a76a8a43 PCRE2: upgrade to 10.43
PCRE2 was updated to version 10.43.

* 94316192f3d QPainterPath: Fix boundingRect and controlPointRect
ignoring start point
boundingRect() and controlPointRect() now use the start point from
QPainterPath(const QPointF &startPoint).

* 394b6d96b58 Update bundled libpng to version 1.6.43
libpng was updated to version 1.6.43

* 225c6d53d61 SQLite: Update SQLite to v3.45.2
Updated SQLite to v3.45.2

* 7c6e3c297d7 SQLite: Update SQLite to v3.45.3
Updated SQLite to v3.45.3

* 8b7eecb39f5 SQLite: Update identified license
Change identified license for SQLite from 'Public Domain' to more
accurate 'SQLite Blessing': https://spdx.org/licenses/blessing.html

* e88c2a3b357 Implement aliased text rendering with DirectWrite
Support QFont::NoAntialias with the DirectWrite font engine.

* 47dd5b7aed6 QXmlStreamWriter: decode UTF-8 into code points
Fixed a bug that caused the class to fail to write UTF-8 strings with
non-US-ASCII content when passed as a QUtf8StringView.

* 72e405b9079 QStringConverterICU: Pass correct pointer to callback
Fixed a bug involving moved QStringEncoder/QStringDecoder objects
accessing invalid state.

### qtdeclarative
* edef122f86 ApplicationWindow: explicitly set background size if not
explicitly set
ApplicationWindow now explicitly sets the width and height of its
background if no size was explicitly set by the user. This matches the
behavior of Control, and ensures that if e.g. an Image is used as a
window's background, any changes in its implicit size (e.g. after a
source change) won't affect its actual size.

### qtmultimedia
* note: The Qt Multimedia FFmpeg media is updated to link dynamically to  
FFmpeg on Windows. Applications using Qt Multimedia with the FFmpeg media  
backend must therefore deploy the FFmpeg libraries as part of installation.  
* 0f3f309fa Update doc and attributions with new FFmpeg version in
Multimedia
Updated FFmpeg to n6.1.

* 44e7a11bb Update pffft version to the latest version from upstream
Updated pffft to fbc4058.

### qttools
* c4142f3ff CMake: Fix qt_add_translations in different subdirs for VS
generators
When using CMake's Visual Studio project generator, the creation of the
update_translations target requires now CMake 3.19 or newer. A warning
is printed for older CMake versions. This warning can be disabled by
setting QT_NO_GLOBAL_LUPDATE_TARGET_CREATION_WARNING to ON.

### qtdoc
* 71760857 Update iOS supported platforms and toolchain to iOS 17/Xcode
15
Xcode 15 is now both supported and required for Qt for iOS. To develop
for iOS 17 devices, please use Qt Creator 13, or generate an Xcode
project using qmake or CMake and use Xcode directly.

### qtimageformats
* 850b234 Update bundled libwebp to version 1.4.0
Update bundled libwebp to version 1.4.0

### qt5compat
* 3d0b5d4 QText{En,De}coder: use DefaultConversion
Fixed a bug that caused QTextEncoder not to write the Byte Order Mark
for UTF codecs when the constructor without explicit flags was used.


Fixes
-----

### qtbase
* [QTBUG-122192](https://bugreports.qt.io/browse/QTBUG-122192) CONFIG *= silent fails at linking
* [QTBUG-122451](https://bugreports.qt.io/browse/QTBUG-122451) Floating point in raster drawBitmap together with strict
QImage::scanLine causes assertion "i >= 0 && i < height()"
* [QTBUG-122622](https://bugreports.qt.io/browse/QTBUG-122622) configure on Windows can't handle unquoted -DFOO=0
arguments
* [QTBUG-122109](https://bugreports.qt.io/browse/QTBUG-122109) QTreeWidget's columns do not seem to resize properly
after upgrading from Qt6.5.3 to Qt6.1.1
* [QTBUG-120699](https://bugreports.qt.io/browse/QTBUG-120699) QHeaderView in QTableView doesn't restore geometry
* [QTBUG-122637](https://bugreports.qt.io/browse/QTBUG-122637) qmessagebox.h: extra ';' after member function
definition [-Wextra-semi]
* [QTBUG-116550](https://bugreports.qt.io/browse/QTBUG-116550) [schannel] Qt warning "QIODevice::write (QTcpSocket):
device not open"
* [QTBUG-122139](https://bugreports.qt.io/browse/QTBUG-122139) DirectWrite's default hinting looks off
* [QTBUG-122167](https://bugreports.qt.io/browse/QTBUG-122167) REG: Kerning errors with DirectWrite font backend
* [QTBUG-118983](https://bugreports.qt.io/browse/QTBUG-118983) CTest prints output from a failed test twice
* [QTBUG-122739](https://bugreports.qt.io/browse/QTBUG-122739) qtpaths/qmake don't honor qtconf in some cases with LTO
enabled
* [QTBUG-96348](https://bugreports.qt.io/browse/QTBUG-96348) QWindowsSystemTrayIcon::showMessage: Windows Handle leak
* [QTBUG-62945](https://bugreports.qt.io/browse/QTBUG-62945) Windows: QSystemTrayIcon::showMessage causes GDI-Object
leak
* [QTBUG-122749](https://bugreports.qt.io/browse/QTBUG-122749) [Crash] WebEngine Print Me example app crashes when
changing the page orientation
* [QTBUG-114608](https://bugreports.qt.io/browse/QTBUG-114608) Programmatically setting focus does not move VoiceOver
* [QTBUG-121561](https://bugreports.qt.io/browse/QTBUG-121561) Android: in TextField: cannot edit inside of words, only
at the end [regression]
* [QTBUG-105871](https://bugreports.qt.io/browse/QTBUG-105871) QUdpSocket stop emitting ReadyRead signal in
QueuedConnection
* [QTBUG-118434](https://bugreports.qt.io/browse/QTBUG-118434) [Reg Qt5->Qt6] QMenu cannot arrange menu entries
correctly when there are large quantity of them
* [QTBUG-113432](https://bugreports.qt.io/browse/QTBUG-113432) RubberBand update area is too small in QListView
* [QTBUG-122821](https://bugreports.qt.io/browse/QTBUG-122821) QListView with checkable items duplicates checkbox
* [QTBUG-122825](https://bugreports.qt.io/browse/QTBUG-122825) QAbstractItemView::indicator not working properly
* [QTBUG-102820](https://bugreports.qt.io/browse/QTBUG-102820) [REG 5.15.2 => 6.2.4] Styled indicators not drawn in
itemviews
* [QTBUG-115598](https://bugreports.qt.io/browse/QTBUG-115598) tst_QWidget::render() with QtWayland failed on Ubuntu
22.04, GNOME
* [QTBUG-117704](https://bugreports.qt.io/browse/QTBUG-117704) Dragging Window handling WM_NCCALCSIZE and WM_NCHITTEST
squishes contents
* [QTBUG-122205](https://bugreports.qt.io/browse/QTBUG-122205) OpenXR feature breaks test builds
* [QTBUG-122996](https://bugreports.qt.io/browse/QTBUG-122996) Delegate definition should be in front of
QGuiApplication but doing so sometimes makes reflection delegate
unusable
* [QTBUG-118226](https://bugreports.qt.io/browse/QTBUG-118226) Rejected QMessageBox emits Accepted Signal
* [QTBUG-123005](https://bugreports.qt.io/browse/QTBUG-123005) [Reg 6.2->6.5+] Qt::AA_ShareOpenGLContexts has stopped
working for offscreen rendering
* [QTBUG-122664](https://bugreports.qt.io/browse/QTBUG-122664) windeployqt can not find qtpaths executable
* [QTBUG-119619](https://bugreports.qt.io/browse/QTBUG-119619) CMake deploy script finds x64 libraries for WoA
application.
* [QTBUG-122893](https://bugreports.qt.io/browse/QTBUG-122893) Sending QNetworkRequest fails on singlethreaded WASM
* [QTBUG-121514](https://bugreports.qt.io/browse/QTBUG-121514) [Reg 6.6.0->6.6.2] Focus wrong in dialog with
QDialogButtonBox
* [QTBUG-120049](https://bugreports.qt.io/browse/QTBUG-120049) [REG 6.6.0 --> 6.6.1] Incorrect child widget has focus
in dialog by default
* [QTBUG-123324](https://bugreports.qt.io/browse/QTBUG-123324) dSYM warning: skipping debug map object with duplicate
name and timestamp
* [QTBUG-116086](https://bugreports.qt.io/browse/QTBUG-116086) tst_qqmlbinding::restoreBindingWithoutCrash leaks memory
* [QTBUG-123454](https://bugreports.qt.io/browse/QTBUG-123454) Windows DirectWrite fontengine crash with fractional dpi
and woff / woff2 fonts
* [QTBUG-123401](https://bugreports.qt.io/browse/QTBUG-123401) Ambigious overload of operator<<(QDBusArgument &arg,
const Container<Key, T> &map) for QMap with nested pairs
* [QTBUG-123486](https://bugreports.qt.io/browse/QTBUG-123486) qcontainertools_impl.h:383:14: error: ‘D.279326’ is used
uninitialized [-Werror=uninitialized]
* [QTBUG-123032](https://bugreports.qt.io/browse/QTBUG-123032) [REG: 6.6.1->6.6.2] Override cursor changes together
with window creation and destruction crashes on KDE
* [QTBUG-122747](https://bugreports.qt.io/browse/QTBUG-122747) Reparenting QTabWidget with a native window tab can
cause crash
* [QTBUG-120768](https://bugreports.qt.io/browse/QTBUG-120768) Non-Native Dialog opens file when attempting to open
invalid file
* [QTBUG-117514](https://bugreports.qt.io/browse/QTBUG-117514) QFuture::then marked as private
* [QTBUG-123429](https://bugreports.qt.io/browse/QTBUG-123429) ABI break between Qt 6.5 LTS and Qt 6.6/6.7
* [QTBUG-123554](https://bugreports.qt.io/browse/QTBUG-123554) xcb: Enabling touch device while application is running
causes a crash on first touch
* [QTBUG-106709](https://bugreports.qt.io/browse/QTBUG-106709) Application looks too small on an external display with
iPadOS 16.1 on M1 iPad
* [QTBUG-123353](https://bugreports.qt.io/browse/QTBUG-123353) building androidnotifier example with qmake fails
* [QTBUG-123959](https://bugreports.qt.io/browse/QTBUG-123959) qApp crashes after being deleted when hosted as a plugin
and when focus application is changed
* [QTBUG-80167](https://bugreports.qt.io/browse/QTBUG-80167) QOpenGLWidget no longer repaint if a paint-on-screen
widget is updated
* [QTBUG-122180](https://bugreports.qt.io/browse/QTBUG-122180) When changing the stylesheet for a selected, checked
QHeaderView section then it disregards the font weight setting
* [QTBUG-124254](https://bugreports.qt.io/browse/QTBUG-124254) Names can start with a non-letter char in Address Book
example
* [QTBUG-103019](https://bugreports.qt.io/browse/QTBUG-103019) MinGW Qt6Platform.pc has an extra '>' after '-D_UNICODE'
* [QTBUG-111235](https://bugreports.qt.io/browse/QTBUG-111235) tst_QOpenGLWidget::reparentHidden() fails on Android 12
CI
* [QTBUG-111236](https://bugreports.qt.io/browse/QTBUG-111236) tst_qvulkan cases fail Android 12 CI
* [QTBUG-2188](https://bugreports.qt.io/browse/QTBUG-2188) QTextDocument: Bullets in bullet lists are not affected by
text color
* [QTBUG-213](https://bugreports.qt.io/browse/QTBUG-213) Error in drawing of bullets in QTextDocument
* [QTBUG-57833](https://bugreports.qt.io/browse/QTBUG-57833) QTextEdit list number/bullets inherit the following text
style
* [QTBUG-123848](https://bugreports.qt.io/browse/QTBUG-123848) Short cuts involving 2 (or more) modifier keys are not
longer handled by the Input Methods on macos.
* [QTBUG-106516](https://bugreports.qt.io/browse/QTBUG-106516) Multi-modifier key events not correctly handled on macOS
* [QTBUG-120276](https://bugreports.qt.io/browse/QTBUG-120276) Crash when reparent a native child to a different tlw if
QT_WIDGETS_RHI=1 is set on Windows
* [QTBUG-124227](https://bugreports.qt.io/browse/QTBUG-124227) Reg[6.5.4->6.5.5] looks like Gif Frame duration is
changed
* [QTBUG-123839](https://bugreports.qt.io/browse/QTBUG-123839) useless file accesses in qt_findAtNxFile() originating
from QStyleSheetStyle::loadPixmap()
* [QTBUG-124343](https://bugreports.qt.io/browse/QTBUG-124343) QMenu documentation points to deprecated
QMouseEvent::globalPos()
* [QTBUG-116777](https://bugreports.qt.io/browse/QTBUG-116777) Package created with windeployqt gives error when exe
run
* [QTBUG-124551](https://bugreports.qt.io/browse/QTBUG-124551) [macOS] App crashes on quit if the Quick Platform menu
is open
* [QTBUG-97645](https://bugreports.qt.io/browse/QTBUG-97645) QWindowsFontEngineDirectWrite ignores QFont::NoAntialias
flag
* [QTBUG-122241](https://bugreports.qt.io/browse/QTBUG-122241) QXmlStreamWriter::writeCharacters fails to write UTF-8
encoded QAnyStringView
* [QTBUG-124475](https://bugreports.qt.io/browse/QTBUG-124475) tst_QWidget::tabOrderWithProxyDisabled() crash on
Wayland(GNOME, Ubuntu 22.04)
* [QTBUG-122138](https://bugreports.qt.io/browse/QTBUG-122138) QTzTimeZoneCache::findEntry() parses files while holding
QTzTimeZoneCache::m_mutex
* [QTBUG-109708](https://bugreports.qt.io/browse/QTBUG-109708) Startup crash in QRhiD3D11::endFrame() with nullptr
access
* [QTBUG-122596](https://bugreports.qt.io/browse/QTBUG-122596) [REG 6.7.0->6.8.0] error in configure step, top level
build, MinGW
* [QTBUG-122838](https://bugreports.qt.io/browse/QTBUG-122838) Android multi-abi builds broken if depfiles are used
* [QTBUG-100336](https://bugreports.qt.io/browse/QTBUG-100336) QObject::connect using loadRelaxed to synchronize non-
atomic writes
* [QTBUG-123438](https://bugreports.qt.io/browse/QTBUG-123438) syncqt fails on MSVC build
* [QTBUG-117500](https://bugreports.qt.io/browse/QTBUG-117500) Sporadic crash on  QFontEngineMulti::ensureEngineAt()
* [QTBUG-110502](https://bugreports.qt.io/browse/QTBUG-110502) Qt fills in private use unicode if a font is found using
it
* [QTBUG-124723](https://bugreports.qt.io/browse/QTBUG-124723) QThread::start(Priority) should be
QThread::start(QThread::Priority)
* [QTBUG-115583](https://bugreports.qt.io/browse/QTBUG-115583) Redundant declaration of QPageSize equality operator

### qtsvg
* [QTBUG-120653](https://bugreports.qt.io/browse/QTBUG-120653) All SVGs with paths with more than 32768 points render
incorrectly
* [QTBUG-121981](https://bugreports.qt.io/browse/QTBUG-121981) QtSvg parser does not handle nested svg elements
correctly
* [QTBUG-120507](https://bugreports.qt.io/browse/QTBUG-120507) [REG 6.2.2 -> 6.2.3] Trying to render particular svg
file takes much longer than before
* [QTBUG-122752](https://bugreports.qt.io/browse/QTBUG-122752) [Reg: 6.4.2 -> 6.5.3] QFont::setPixelSize warning when
rendering svg files with painter font size set in pixels

### qtdeclarative
* [QTBUG-120506](https://bugreports.qt.io/browse/QTBUG-120506) [Reg 6.5 -> 6.6] Using `CameraLens.ProjectionType` as
type hinting cause runtime error
* [QTBUG-122252](https://bugreports.qt.io/browse/QTBUG-122252) [REG: 6.4->6.5] Qt.point cannot be used as a return type
* [QTBUG-120555](https://bugreports.qt.io/browse/QTBUG-120555) AnimatedImage: issues with loading web source
* [QTBUG-107521](https://bugreports.qt.io/browse/QTBUG-107521) qmlint: Example in documentation produces Cannot assign
binding of type QQmlListProperty<QObject> to QList<QObject *>
* [QTBUG-119911](https://bugreports.qt.io/browse/QTBUG-119911) Incubated object is garbage collected before a reference
to it can be created
* [QTBUG-119448](https://bugreports.qt.io/browse/QTBUG-119448) Fix documentation: initializing a property of aliased
property won't actually cause an error
* [QTBUG-116994](https://bugreports.qt.io/browse/QTBUG-116994) qt_add_add_qml_module runs into command line length
limits on Windows
* [QTBUG-122454](https://bugreports.qt.io/browse/QTBUG-122454) Gallery example radio buttons not working as expected
* [QTBUG-116505](https://bugreports.qt.io/browse/QTBUG-116505) HoverHandler is broken when using a stylus
* [QTBUG-101932](https://bugreports.qt.io/browse/QTBUG-101932) two HoverHandlers with different
acceptedDevices/acceptedPointerTypes: cursorShape doesn't change
accordingly
* [QTBUG-120526](https://bugreports.qt.io/browse/QTBUG-120526) qmllint complains wrongly when changing Layout attached
properties in a PropertyChanges
* [QTBUG-118982](https://bugreports.qt.io/browse/QTBUG-118982) qmllint multiple pragma ComponentBehavior in same file
* [QTBUG-115478](https://bugreports.qt.io/browse/QTBUG-115478) Qmllint interferes with qmldir file in source directory
if present
* [QTBUG-121592](https://bugreports.qt.io/browse/QTBUG-121592) Attached ScrollBar and ScrollIndicator fail when using
QML Type Compiler
* [QTBUG-113039](https://bugreports.qt.io/browse/QTBUG-113039) Crash when accessing properties of line parameter in
Text.onLineLaidOut
* [QTBUG-122707](https://bugreports.qt.io/browse/QTBUG-122707) [Reg 5.15 -> 6.4] Binding QML type does not restore
original value in some cases
* [QTBUG-122790](https://bugreports.qt.io/browse/QTBUG-122790) Child window is not closed upon closing the main window
in Qt Quick Widgets Example
* [QTBUG-122686](https://bugreports.qt.io/browse/QTBUG-122686) Crash when processing hover events modifies object tree
* [QTBUG-120433](https://bugreports.qt.io/browse/QTBUG-120433) AnimationController segfaults on exit
* [QTBUG-113384](https://bugreports.qt.io/browse/QTBUG-113384) QQuickWidget - touchpad click not working after
scrolling
* [QTBUG-91272](https://bugreports.qt.io/browse/QTBUG-91272) [Regression]On Mouse Area press, deleting other
overlapping mouse area crashes the Application
* [QTBUG-120149](https://bugreports.qt.io/browse/QTBUG-120149) Material 3 - TextField placeholder issues when padding
changed
* [QTBUG-113532](https://bugreports.qt.io/browse/QTBUG-113532) Animate RadioButton in the Material style
* [QTBUG-122894](https://bugreports.qt.io/browse/QTBUG-122894) Crash when QQuickView loads QML document that binds
Overlay.overlay.[property]
* [QTBUG-117923](https://bugreports.qt.io/browse/QTBUG-117923) ItemParticle causes constant CPU usage and rerenders
* [QTBUG-121388](https://bugreports.qt.io/browse/QTBUG-121388) Qt Quick Controls: Palette role values don't get live
updates
* [QTBUG-121466](https://bugreports.qt.io/browse/QTBUG-121466) ApplicationWindow background Image does not resize when
source changed
* [QTBUG-122770](https://bugreports.qt.io/browse/QTBUG-122770) MessageDialog accepted handler isn’t called for Ok
button
* [QTBUG-122076](https://bugreports.qt.io/browse/QTBUG-122076) QQuickItem::classBegin()/componentComplete() never
invoked when using QQmlComponent::loadFromModule()
* [QTBUG-123111](https://bugreports.qt.io/browse/QTBUG-123111) Particle System Application stuck on GUI thread
* [QTBUG-120542](https://bugreports.qt.io/browse/QTBUG-120542) Editable SpinBox crashes Quick3d application
* [QTBUG-123413](https://bugreports.qt.io/browse/QTBUG-123413) qmltypes warning when using const in Q_INVOKABLE
* [QTBUG-107143](https://bugreports.qt.io/browse/QTBUG-107143) qmllint ignore RegisterEnumClassesUnscoped
* [QTBUG-120760](https://bugreports.qt.io/browse/QTBUG-120760) Unloading TableView headers via Loaders causes crash
* [QTBUG-123490](https://bugreports.qt.io/browse/QTBUG-123490) Flickable doesn't react to second touchpoint while first
touchpoint is dragging DragHandler
* [QTBUG-86729](https://bugreports.qt.io/browse/QTBUG-86729) many Qt Quick test failures after input event refactoring
* [QTBUG-95939](https://bugreports.qt.io/browse/QTBUG-95939) tst_taphandler is flaky on OpenSUSE
* [QTBUG-123395](https://bugreports.qt.io/browse/QTBUG-123395) QML EXC_BAD_ACCESS crash
* [QTBUG-119765](https://bugreports.qt.io/browse/QTBUG-119765) [Reg 6.5.2 -> 6.6.1]default roles are not available in
abstract table model headerdata
* [QTBUG-123594](https://bugreports.qt.io/browse/QTBUG-123594) Missing dependency in QtQuick/Controls/Material/impl
* [QTBUG-123535](https://bugreports.qt.io/browse/QTBUG-123535) qt_generate_foreign_qml_types fails with Q_ENUM_NS
* [QTBUG-123596](https://bugreports.qt.io/browse/QTBUG-123596) Crash JS for x in o  { delete o[x] } if o is a
sparsearray
* [QTBUG-123050](https://bugreports.qt.io/browse/QTBUG-123050) Crash when trying to build QML files (qmlcachegen)
* [QTBUG-122340](https://bugreports.qt.io/browse/QTBUG-122340) MultiEffect - Wrong initial position of the shadow
(MultiEffect)
* [QTBUG-122746](https://bugreports.qt.io/browse/QTBUG-122746) Quick controls Popup - shadow is rendered incorrectly
* [QTBUG-123118](https://bugreports.qt.io/browse/QTBUG-123118) QQuickShaderEffect missing property updates
* [QTBUG-123983](https://bugreports.qt.io/browse/QTBUG-123983)  Icon color is not set when "Popup component close
policy" set other than 'NoAutoClose''
* [QTBUG-122925](https://bugreports.qt.io/browse/QTBUG-122925) QQmlComponentPrivate::doBeginCreate can crash in some
scenarios
* [QTBUG-123378](https://bugreports.qt.io/browse/QTBUG-123378) QML TextInput makes the application unresponsive if made
invisible when it has keyboard focus on Android
* [QTBUG-124226](https://bugreports.qt.io/browse/QTBUG-124226) Confusing example code for Qt.createComponent
* [QTBUG-122250](https://bugreports.qt.io/browse/QTBUG-122250) GridView is missing documentation for reuseItems
* [QTBUG-83408](https://bugreports.qt.io/browse/QTBUG-83408) Text disappears with ElideRight.
* [QTBUG-33608](https://bugreports.qt.io/browse/QTBUG-33608) Elide property of Text breaks component resizing
* [QTBUG-123773](https://bugreports.qt.io/browse/QTBUG-123773) [Contact List Example] Example not running on MacOS
* [QTBUG-120033](https://bugreports.qt.io/browse/QTBUG-120033) Binding not evaluated
* [QTBUG-98098](https://bugreports.qt.io/browse/QTBUG-98098) Error when Button has a custom background under macOS
style
* [QTBUG-116589](https://bugreports.qt.io/browse/QTBUG-116589) Dynamic translations seem not working with
QQmlApplicationEngine::loadFromModule()
* [QTBUG-123865](https://bugreports.qt.io/browse/QTBUG-123865) [Reg 6.2 -> 6.5] Crash when using PropertyChanges with
multiple inline components
* [QTBUG-43842](https://bugreports.qt.io/browse/QTBUG-43842) Scanning for QML imports of projects fails
* [QTBUG-122783](https://bugreports.qt.io/browse/QTBUG-122783) Material.theme doesn't propagate to ListView header when
elevation animated
* [QTBUG-120670](https://bugreports.qt.io/browse/QTBUG-120670) TextField causing activeFocus of the calling item to be
triggered multiple times.
* [QTBUG-120097](https://bugreports.qt.io/browse/QTBUG-120097) Screen Reader reads password in Password TextField
* [QTBUG-94100](https://bugreports.qt.io/browse/QTBUG-94100) TreeView: adding columns not handled
* [QTBUG-108696](https://bugreports.qt.io/browse/QTBUG-108696) [TapHandler] Internal warning "QObject::disconnect:
Unexpected nullptr parameter"
* [QTBUG-124456](https://bugreports.qt.io/browse/QTBUG-124456) [6.4.2] Margins in QuickLayouts causing a QList
exception (index out of range)
* [QTBUG-62111](https://bugreports.qt.io/browse/QTBUG-62111) Docs: Fixed day/year format in QDateTime
* [QTBUG-63363](https://bugreports.qt.io/browse/QTBUG-63363) QPointingDevices for the trackpad and mouse are
dynamically instantiated on macOS
* [QTBUG-112432](https://bugreports.qt.io/browse/QTBUG-112432) wayland plugin should distinguish touchpads from mice,
etc.
* [QTBUG-122173](https://bugreports.qt.io/browse/QTBUG-122173) tst_qquickanimatedimage::currentFrame() is flaky on
windows
* [QTBUG-78846](https://bugreports.qt.io/browse/QTBUG-78846) tst_qquicktextedit::mouseSelectionMode is flaky on
OpenSuse 15
* [QTBUG-74342](https://bugreports.qt.io/browse/QTBUG-74342) QML RichText hr element doesn't work
* [QTBUG-115438](https://bugreports.qt.io/browse/QTBUG-115438) [REG: 5->6] MouseArea onEnter triggers before onExit on
the previous item
* [QTBUG-110475](https://bugreports.qt.io/browse/QTBUG-110475) [REG 6.4.1 → 6.4.2] Interactive elements in
SwipeDelegate receive no events
* [QTBUG-123210](https://bugreports.qt.io/browse/QTBUG-123210) QML: Rectangle with rounded corners and border width = 1
shows not good anti-aliasing
* [QTBUG-108831](https://bugreports.qt.io/browse/QTBUG-108831) Some Rectangle borders are double the width with
fractional scale ratios
* [QTBUG-123592](https://bugreports.qt.io/browse/QTBUG-123592) Foreign generation fails with namespace
* [QTBUG-123999](https://bugreports.qt.io/browse/QTBUG-123999) Heap buffer overflow in JS Set.delete
* [QTBUG-114969](https://bugreports.qt.io/browse/QTBUG-114969) qmllint should consider QML2_IMPORT_PATH for import
paths

### qtactiveqt
* [QTBUG-122762](https://bugreports.qt.io/browse/QTBUG-122762) [Reg 5.15 -> 6.5] ActiveQt server does not return
QVariantList properly

### qtmultimedia
* [QTBUG-116519](https://bugreports.qt.io/browse/QTBUG-116519) [Reg 6.2 -> 6.5] Repeated QSoundEffect is broken on
PulseAudio
* [QTBUG-122640](https://bugreports.qt.io/browse/QTBUG-122640) QtMultimedia plugins are not deployed to Android .apks
* [QTBUG-113317](https://bugreports.qt.io/browse/QTBUG-113317) QVideoWidget rendering video incorrectly on macOS
Monterey
* [QTBUG-121714](https://bugreports.qt.io/browse/QTBUG-121714) Camera preview stops working when recording on Android-
backend
* [QTBUG-121943](https://bugreports.qt.io/browse/QTBUG-121943) QPlatformMediaDevices is accessed before main on Android
* [QTBUG-121221](https://bugreports.qt.io/browse/QTBUG-121221)  Camera Example - Recording Denied with "Invalid
Argument" Error
* [QTBUG-122045](https://bugreports.qt.io/browse/QTBUG-122045) [MediaPlayerExample] The timeline is not reset when the
loop mode for single file is turned on
* [QTBUG-122706](https://bugreports.qt.io/browse/QTBUG-122706) onBufferProgressChanged not emited at all
* [QTBUG-121678](https://bugreports.qt.io/browse/QTBUG-121678) eglfs: Capturing the screen crashes on a Qt Quick
application
* [QTBUG-122753](https://bugreports.qt.io/browse/QTBUG-122753) Qt Multimedia: implicit instantiation of undefined
template 'std::char_traits<unsigned char>' (libc++ 19 / musl libc /
amd64)
* [QTBUG-121182](https://bugreports.qt.io/browse/QTBUG-121182) QML Video Example: Simultaneous videos playback crashes
the App on Android
* [QTBUG-122649](https://bugreports.qt.io/browse/QTBUG-122649)  Playing multiple videos simultaneously fails for the
second video with the FFMPEG backend on Android.
* [QTBUG-122193](https://bugreports.qt.io/browse/QTBUG-122193) QSoundEffect hangs on Loading
* [QTBUG-122608](https://bugreports.qt.io/browse/QTBUG-122608) [REG 6.6.1-6.6.2] [windows] QMediaPlayer failed to set
topology on custom QVideoSink
* [QTBUG-122817](https://bugreports.qt.io/browse/QTBUG-122817) [REG 6.6.1-6.6.2] [windows] QML MediaPlayer unable to
play a video when 'audioOutput' is not specified
* [QTBUG-122199](https://bugreports.qt.io/browse/QTBUG-122199) [ffmpeg] player crash in libavcodec if libnvidia-decode
is not installed
* [QTBUG-122638](https://bugreports.qt.io/browse/QTBUG-122638) [gstreamer] deadlock when switching camera
* [QTBUG-98437](https://bugreports.qt.io/browse/QTBUG-98437) QMediaPlayer does not emit destroyed signal
* [QTBUG-122750](https://bugreports.qt.io/browse/QTBUG-122750) [Regression] QSoundEffect cuts audio with FFmpeg backend
* [QTBUG-122959](https://bugreports.qt.io/browse/QTBUG-122959) GStreamer: "stop camera" does not stop camera
* [QTBUG-123205](https://bugreports.qt.io/browse/QTBUG-123205) Allow defining platform specific gstreamers
colorconversion-plugins
* [QTBUG-123312](https://bugreports.qt.io/browse/QTBUG-123312) [gstreamer] video playback broken with gstreamer older
than 1.20
* [QTBUG-123117](https://bugreports.qt.io/browse/QTBUG-123117) MediaPlayer crashes on seek after loop reset.
* [QTBUG-122575](https://bugreports.qt.io/browse/QTBUG-122575) Mediaplayer example not showing video on some Android
emulators
* [QTBUG-123139](https://bugreports.qt.io/browse/QTBUG-123139) GStreamer: Qt Camera in stops after switching
VideoOutput
* [QTBUG-113421](https://bugreports.qt.io/browse/QTBUG-113421) Qt Camera in QML Dies after closes the drawer with
Camera
* [QTBUG-122968](https://bugreports.qt.io/browse/QTBUG-122968) QML Camera: Using zoom and switching cameras breaks the
example
* [QTBUG-120266](https://bugreports.qt.io/browse/QTBUG-120266) [Windows] App hangs on destroying QML Video component
during video playback
* [QTBUG-123215](https://bugreports.qt.io/browse/QTBUG-123215) fatal error: qplatformmediadevices_p.h: No such file or
directory when building from source for Qt 6.6.2 on Windows
* [QTBUG-123131](https://bugreports.qt.io/browse/QTBUG-123131) Modified video frames are not updated for rendering
* [QTBUG-122184](https://bugreports.qt.io/browse/QTBUG-122184) [Crash] The 'Widgets camera' app crashes on Android when
starting and stopping the video recording
* [QTBUG-123597](https://bugreports.qt.io/browse/QTBUG-123597) QAudioDecoder crashes on files without audio track
* [QTBUG-123045](https://bugreports.qt.io/browse/QTBUG-123045) [Examples] Qt warning on changing audio input in Audio
Source example
* [QTBUG-120198](https://bugreports.qt.io/browse/QTBUG-120198) Process abruptly terminates while executing static
destructor in Qt6Multimedia.dll
* [QTBUG-123967](https://bugreports.qt.io/browse/QTBUG-123967) QML media player example project fails to play AV1
encoded videos.
* [QTBUG-124115](https://bugreports.qt.io/browse/QTBUG-124115) QtMultimedia configure fails for GPU-less yocto target
* [QTBUG-123899](https://bugreports.qt.io/browse/QTBUG-123899) [GStreamer] createVideoProfile unit test failure
* [QTBUG-112312](https://bugreports.qt.io/browse/QTBUG-112312) QFFmpeg EGL VAAPI failures
* [QTBUG-119914](https://bugreports.qt.io/browse/QTBUG-119914) VideoSink frame to image does not work on android
* [QTBUG-117771](https://bugreports.qt.io/browse/QTBUG-117771) Qt6.5.3 QMediaPlayer play video an error on android 11
* [QTBUG-124253](https://bugreports.qt.io/browse/QTBUG-124253) Direct3D debug layer reports error when playing videos
of same size and pixel format
* [QTBUG-123904](https://bugreports.qt.io/browse/QTBUG-123904) [gstreamer] tst_QMediaCaptureSession::testAudioMute test
failure
* [QTBUG-123905](https://bugreports.qt.io/browse/QTBUG-123905) [gstreamer]
tst_QMediaCaptureSession::stress_test_setup_and_teardown test failure
* [QTBUG-123447](https://bugreports.qt.io/browse/QTBUG-123447) Incorrect log format in qaudioengine_pulse.cpp
* [QTBUG-121172](https://bugreports.qt.io/browse/QTBUG-121172) [REG 6.5.5 - > 6.5.6] Declarative Camera: Black Screen
Issue when Clicking "View" Button in Video Mode
* [QTBUG-123526](https://bugreports.qt.io/browse/QTBUG-123526) No video input devices with QT_MEDIA_BACKEND set to
ffmpeg
* [QTBUG-124414](https://bugreports.qt.io/browse/QTBUG-124414) [gstreamer] MediaPlayer emits BufferedMedia in
StoppedState
* [QTBUG-124415](https://bugreports.qt.io/browse/QTBUG-124415) [gstreamer] MediaPlayer emits too many state change
signals
* [QTBUG-124776](https://bugreports.qt.io/browse/QTBUG-124776) [gstreamer] uridecodebin with https source spurious
playback failure
* [QTBUG-121750](https://bugreports.qt.io/browse/QTBUG-121750) QCameraImageProcessing fails to set settings on linux
v4l2 camera
* [QTBUG-122577](https://bugreports.qt.io/browse/QTBUG-122577) QScreenCapture tests are flaky on OpenSuse 15.5
* [QTBUG-108754](https://bugreports.qt.io/browse/QTBUG-108754) Video not stretched properly
* [QTBUG-116324](https://bugreports.qt.io/browse/QTBUG-116324) Request to implement thumbnail realization for
multimedia FFMPEG backend
* [QTBUG-111190](https://bugreports.qt.io/browse/QTBUG-111190) V4L2m2m encoder gets failed on linux
* [QTBUG-122224](https://bugreports.qt.io/browse/QTBUG-122224) [Crash] The audiorecorder example crashes when selecting
output and start recording
* [QTBUG-87969](https://bugreports.qt.io/browse/QTBUG-87969) MediaPlayer looses current position when playbackRate
changes
* [QTBUG-123356](https://bugreports.qt.io/browse/QTBUG-123356) ERROR: Crash detected
* [QTBUG-123224](https://bugreports.qt.io/browse/QTBUG-123224) tst_qmediacapturesession crashes in
CI(opensuse-15.5-host-asan)
* [QTBUG-123023](https://bugreports.qt.io/browse/QTBUG-123023) [Examples] Audio input devices list is not updated when
connecting new device
* [QTBUG-123459](https://bugreports.qt.io/browse/QTBUG-123459) [gstreamer] player example does not update "Buffering"
percentage
* [QTBUG-119535](https://bugreports.qt.io/browse/QTBUG-119535) [Boot2Qt] Switching between audio output devices while
playing video causes the player app to freeze
* [QTBUG-123177](https://bugreports.qt.io/browse/QTBUG-123177) OpenSUSE crash in tst_QMediaCaptureSession with
PulseAudio
* [QTBUG-96985](https://bugreports.qt.io/browse/QTBUG-96985) Video and MediaPlayer don't allow to use relative URLs
* [QTBUG-124501](https://bugreports.qt.io/browse/QTBUG-124501) [gstreamer] media player does not play without outputs
connected
* [QTBUG-124183](https://bugreports.qt.io/browse/QTBUG-124183) [gstreamer] tst_QCameraBackend::testNativeMetadata test
failure due to duration timeout error
* [QTBUG-122140](https://bugreports.qt.io/browse/QTBUG-122140) The video freezes when recording it with higher
resolution in widgets camera example
* [QTBUG-113627](https://bugreports.qt.io/browse/QTBUG-113627) D3D11 Removing Device on QVideoSink save frame
* [QTBUG-124586](https://bugreports.qt.io/browse/QTBUG-124586) QML video media player segmentation fault on AMD GPU
with FFMPEG
* [QTBUG-124537](https://bugreports.qt.io/browse/QTBUG-124537) YUYV format from QCamera is buggy
* [QTBUG-124647](https://bugreports.qt.io/browse/QTBUG-124647) YUYV and UYVY pixel formats are not rendered correctly
with FFmpeg backend

### qttools
* [QTBUG-119555](https://bugreports.qt.io/browse/QTBUG-119555) [REG] Qt 6.6.1 breaks qt_add_translations
* [QTBUG-115166](https://bugreports.qt.io/browse/QTBUG-115166) qt_add_qml_module() causes non-Ninja generators to think
that projects are never up-to-date

### qtdoc
* [QTBUG-121578](https://bugreports.qt.io/browse/QTBUG-121578) demos/hangman fails to build on Android and macOS
* [QTBUG-120643](https://bugreports.qt.io/browse/QTBUG-120643) [REG 6.2.4 -> 6.5.3] "Classes" page is empty
* [QTBUG-122615](https://bugreports.qt.io/browse/QTBUG-122615) [Document Viewer Example] "about documentviewer" button
opens wrong pop-up message
* [QTBUG-124146](https://bugreports.qt.io/browse/QTBUG-124146) [demos/hangman] Clicking on the vowels button crashes
the demo
* [QTBUG-122682](https://bugreports.qt.io/browse/QTBUG-122682) "Porting to iOS" documentation only mentions qmake, not
CMake
* [QTBUG-122273](https://bugreports.qt.io/browse/QTBUG-122273) [MediaPlayerApp] The file names on the playlist in the
app have specific format on Android

### qtpositioning
* [QTBUG-119477](https://bugreports.qt.io/browse/QTBUG-119477) SatelliteInfo example crashes
* [QTBUG-115933](https://bugreports.qt.io/browse/QTBUG-115933) [QtPositioning] geoclue2 backend crashes randomly
* [QTBUG-121997](https://bugreports.qt.io/browse/QTBUG-121997) BUS ERROR in examples/positioning/satelliteinfo on
aarch64

### qtwayland
* [QTBUG-122965](https://bugreports.qt.io/browse/QTBUG-122965) Qt 6.5.4 don't generate XDG_RUNTIME_DIR
* [QTBUG-123007](https://bugreports.qt.io/browse/QTBUG-123007) Under Wayland Qt does not correctly handle key modifiers
during key repeating
* [QTBUG-107858](https://bugreports.qt.io/browse/QTBUG-107858) qtwayland caches clipboard content
* [QTBUG-123489](https://bugreports.qt.io/browse/QTBUG-123489) Qt Wayland Client requires QtGui to be build with
support for wayland
* [QTBUG-124304](https://bugreports.qt.io/browse/QTBUG-124304) [REG 6.7.1-> 6.7.0] no-gui (-DFEATURE_gui=OFF) build
fails, qtspeech
* [QTBUG-124807](https://bugreports.qt.io/browse/QTBUG-124807) Horizontal scrolling not working under Wayland with
Alt+Wheel
* [QTBUG-100148](https://bugreports.qt.io/browse/QTBUG-100148) Hover state of QCombobox has not been reset
* [QTBUG-113404](https://bugreports.qt.io/browse/QTBUG-113404) Wayland: Gestures are not delivered to correct top level
widget

### qtimageformats
* [QTBUG-113349](https://bugreports.qt.io/browse/QTBUG-113349) [static linking] duplicate symbol with QIIOFHelper

### qtwebsockets
* [QTBUG-123346](https://bugreports.qt.io/browse/QTBUG-123346) Expired (and near-expiring) certificates shipped with
examples

### qtwebengine
* [QTBUG-120273](https://bugreports.qt.io/browse/QTBUG-120273) QWebEngineView shows blank content on initial show when
page bg set to transparent
* [QTBUG-121227](https://bugreports.qt.io/browse/QTBUG-121227) QWebEngineView shows blank content on initial show when
page bg set to transparent
* [QTBUG-120764](https://bugreports.qt.io/browse/QTBUG-120764) PDF Viewer Widget example search error
* [QTBUG-106565](https://bugreports.qt.io/browse/QTBUG-106565) The coordinate of QPdfSelection seems like to be wrong
when pdf page contains non-displayable area
* [QTBUG-100630](https://bugreports.qt.io/browse/QTBUG-100630) PdfLinkModel don't give the right rect everytime
* [QTBUG-112013](https://bugreports.qt.io/browse/QTBUG-112013) QWebEnginePage.setBackground(Qt::black) doesn't work for
page loading.
* [QTBUG-120926](https://bugreports.qt.io/browse/QTBUG-120926) QWebEnginePage::setBackgroundColor doesn't work properly
* [QTBUG-122153](https://bugreports.qt.io/browse/QTBUG-122153) QWebEngineView::setFocus() doesn't give focus to the
view after calling QWebEngineView::load() for the second time
* [QTBUG-122137](https://bugreports.qt.io/browse/QTBUG-122137) REG: QtWebEngine / Pdfwidgets no longer supports plugins
* [QTBUG-121589](https://bugreports.qt.io/browse/QTBUG-121589) Can't build qt6 due to failed ozone platform assertion
* [QTBUG-118035](https://bugreports.qt.io/browse/QTBUG-118035) QtWebengine build fails on pure wayland
* [QTBUG-122997](https://bugreports.qt.io/browse/QTBUG-122997) The Spellcheck example doesn't work on macOS
* [QTBUG-124174](https://bugreports.qt.io/browse/QTBUG-124174) WebEngine regression from 6.6.2 to 6.6.3
* [QTBUG-122655](https://bugreports.qt.io/browse/QTBUG-122655) 6.8.0 toplevel build fails on macOS, qtwebengine
* [QTCREATORBUG-30308](https://bugreports.qt.io/browse/QTCREATORBUG-30308) QtCreator is not able to debug pdb files when lib
linked with pdbpagesize
* [QTBUG-120420](https://bugreports.qt.io/browse/QTBUG-120420) QtWebEngine inspector crashes
* CVE-2024-1670: Use after free in Mojo  
* CVE-2024-1671: Inappropriate implementation in Site Isolation  
* CVE-2024-1672: Inappropriate implementation in Content Security Policy.  
* CVE-2024-1676: Inappropriate implementation in Navigation  
* CVE-2024-2625: Object lifecycle issue in V8  
* CVE-2024-2626: Out of bounds read in Swiftshader  
* CVE-2024-2887: Type Confusion in WebAssembly  
* CVE-2024-3157: Out of bounds write in Compositing  
* CVE-2024-3159: Out of bounds memory access in V8  
* CVE-2024-3516: Heap buffer overflow in ANGLE  
* CVE-2024-3837: Use after free in QUIC  
* CVE-2024-3839: Out of bounds read in Fonts  
* CVE-2024-3840: Insufficient policy enforcement in Site Isolation  
* CVE-2024-3914: Use after free in V8  
* CVE-2024-4331: Use after free in Picture In Picture  
* CVE-2024-4058: Type Confusion in ANGLE  
* CVE-2024-4558: Use after free in ANGLE  
* CVE-2024-4671: Use after free in Visuals  
* CVE-2023-7104  
* CVE-2024-25062 / Security bug 325094430  
* Security bug 1504473 / 40945008  
* Security bug 1508758 / 41481379  
* Security bug 1518994  
* Security bug 323898565  
* Security bug 325296797  
* Security bug 326349405  
* Security bug 326498393  
* Security bug 326521449  
* Security bug 327183408  
* Security bug 327698060  
* Security bug 329674887  
* Security bug 332724843  
* Security bug 339458194  
* Security bug 40940917  
* Security bug 41495984  
  
### qtvirtualkeyboard
* [QTBUG-121658](https://bugreports.qt.io/browse/QTBUG-121658) Virtual keyboard example crashes after startup on
Android

### qtspeech
* [QTBUG-122900](https://bugreports.qt.io/browse/QTBUG-122900) Android App dies immediately if I add TextToSpeech to
the project

### qtquick3d
* [QDS-11396](https://bugreports.qt.io/browse/QDS-11396) Node QML type from QtQuick3D is not available in Components
* [QTBUG-122143](https://bugreports.qt.io/browse/QTBUG-122143) balsam ktx build error with ASAN build
* [QTBUG-108755](https://bugreports.qt.io/browse/QTBUG-108755) [REGRESSION] number of drawcalls don't show up in QML
profiler
* [QTBUG-123015](https://bugreports.qt.io/browse/QTBUG-123015) When configuring with -no-qml-debug then it will fail to
build QtQuick3D

### qt5compat
* [QTBUG-122795](https://bugreports.qt.io/browse/QTBUG-122795) Incompatibility in QTextCodec between Qt5 and Qt6 (lack
of BOM)

### qtquick3dphysics
* [QTBUG-123888](https://bugreports.qt.io/browse/QTBUG-123888) discrepancy between PTHREAD_POOL_SIZE and
QThreadPrivate::idealThreadCount

### qtgrpc
* [QTBUG-122700](https://bugreports.qt.io/browse/QTBUG-122700) qt_add_protobuf doesn't set neither OUTPUT_HEADERS nor
OUTPUT_TARGETS

Known Issues
------------

* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-6.5/supported-platforms.html  
  
* The RTA (release test automation) reported issues in Qt 6.5.x:  
https://bugreports.qt.io/issues/?filter=24558  
  
* See Qt 6.5 known issues from:  
https://wiki.qt.io/Qt_6.5_Known_Issues  
  
* Qt 6.5.6 Open issues in Jira:  
https://bugreports.qt.io/issues/?filter=26125  

Credits for the  release goes to:
---------------------------------

Eirik Aavitsland  
Laszlo Agocs  
Anu Aliyas  
Even Oscar Andersen  
Dimitrios Apostolou  
Viktor Arvidsson  
Vladimir Belyavsky  
Nicholas Bennett  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
Joerg Bornemann  
Rym Bouabid  
Assam Boudjelthia  
Kai Uwe Broulik  
Michael Brüning  
Olivier De Cannière  
Kaloyan Chehlarski  
Mike Chen  
Albert Astals Cid  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Noah Davis  
Oliver Dawes  
Pavel Dubsky  
Artem Dyomin  
Alexey Edelev  
Oliver Eftevaag  
Christian Ehrlicher  
Hatem ElKharashy  
Andreas Eliasson  
David Faure  
Robert Griebl  
Mikko Gronoff  
Kaj Grönholm  
Richard Moe Gustavsen  
Mikko Hallamaa  
Jøger Hansegård  
Miikka Heikkinen  
Moss Heim  
Ulf Hermann  
Volker Hilsheimer  
Marc Hüskens  
Allan Sandfeld Jensen  
Jonas Karlsson  
Timothée Keller  
Friedemann Kleint  
André Klitzing  
Andre Klitzing  
Michal Klocek  
Jarkko Koivikko  
Tomi Korpipaa  
Janne Koskinen  
Fabian Kosmale  
Volker Krause  
Jaroslaw Kubik  
Santhosh Kumar  
Keith Kyzivat  
Kai Köhne  
Lauri Laanmets  
Inho Lee  
Chris Lerner  
Thiago Macieira  
Bartlomiej Moskal  
Marc Mutz  
Antti Määttä  
Jithin Nair  
Andy Nichols  
Mårten Nordheim  
Dennis Oberst  
Liang Qi  
Matthias Rauter  
David Redondo  
Topi Reinio  
Shawn Rutledge  
Toni Saario  
Ahmad Samir  
Sami Shalayel  
Andy Shaw  
Ivan Solovev  
Axel Spoerl  
Martin Storsjö  
Tarja Sundqvist  
Lars Sutterud  
Jan Arve Sæther  
Sadegh Taghavi  
Paul Olav Tvete  
Sami Varanka  
Peter Varga  
Doris Verria  
Tor Arne Vestbø  
Olli Vuolteenaho  
Bernd Weimer  
Edward Welbourne  
Paul Wicking  
Piotr Wierciński  
Yifan Zhu  
