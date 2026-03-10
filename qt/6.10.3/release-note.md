Release notes
=============
Qt 6.10.3 release is a patch release made on the top of Qt 6.10.2.
As a patch release, Qt 6.10.3 does not add any new functionality but provides
bug fixes and other improvements and maintains both forward and backward
compatibility (source and binary) with the 6.10.x series.

For detailed information about Qt 6.10, refer to the online documentation
included in this distribution. The documentation is also available online:

https://doc.qt.io/qt-6/index.html

The Qt version 6.10 series is binary compatible with the 6.9.x series.
Applications compiled for 6.9 will continue to run with 6.10.

Some of the changes listed in this file include issue tracking numbers
corresponding to tasks in the Qt Bug Tracker:

https://qt-project.atlassian.net/

Each of these identifiers can be entered in the bug tracker to obtain
more information about a particular change.

To make it easier to port to Qt 6, we have created a porting guide to
summarize what changed between Qt 5 and Qt 6 and provide guidance on how to
adapt to those changes. In the guide, you can find links to articles about
changes that may affect your application and help you transition from Qt
5.15 to Qt 6:

https://doc.qt.io/qt-6/portingguide.html


Important Changes
-----------------

### Security fixes
N/A

### qtbase
* a73711f2f72 CMake: Revisit target-based qt_wrap_cpp
When using the target-based signature of qt_wrap_cpp, qt_wrap_cpp(myapp
myobject.h) will now add the generated moc_myobject.cpp to the target.

* 759fc175d70 Upgrade Harfbuzz to 12.3.0
Upgraded Harfbuzz to version 12.3.0.

* 834c3244f69 macOS: Enable clipping of subviews when QWindow has child
windows
QWindows with child windows will now set the NSView.clipsToBounds
property to YES, to ensure that the child windows are clipped to their
parent.

* 0fda451034b Update tika-mimetypes.xml from upstream and improve
tooling
Updated TIKA mimetypes from upstream

* 774f1a0db91 double-conversion: Update to 3.4.0
Updated double-conversion to v3.4.0.

* e43204a800d Update bundled libpng to version 1.6.54
libpng was updated to version 1.6.54

* b3b24aa8930 CMake: Fix qt_wrap_cpp calls in subdirectories
In the variable-based signature of qt_wrap_cpp, we now add foo.moc
files to the output variable. This simplifies the code flow, and adding
.moc source files to a target doesn't have a negative effect.

* 45b2216cb58 SQLite: Update SQLite to v3.51.2
Updated SQLite to v3.51.2

* b55b3fbf33b Update CLDR to v48.1
QLocale is updated to version 48.1.

* 57c843476d9 Update public suffix list
Updated the public suffix list to upstream version
2026-01-16_13-11-47_UTC.

* 57d10d86a32 Update UCD to Unicode 17.0.0 / revision 36
Updated the Unicode Character Database to UCD revision 36/Unicode 17.

* 79c425cbe8a QString::normalization: fix corrections shrinking the
string
Fixed a bug that caused normalization() to incorrectly apply some
Unicode 3.1 and 3.2 corrections, corrupting the string during the
operation. This affected QUrl::toAce().

* 9a6d1a04f0f Upgrade Harfbuzz to 12.3.2
Upgraded Harfbuzz to version 12.3.2.

* b7027c30ae9 Update bundled libpng to version 1.6.55
libpng was updated to version 1.6.55

* 406903b6ef7 QFileSystemEngine: handle copy_file_range() returning
ENOSYS error
Added a workaround to a compatibility issue of the copy()
implementation in some containerized Linux environments, which could
cause the file copy to fail with a "Function not implemented" error.
This is believed to be a bug in the container runtime, not Qt, in that
the container wrongly filtered the copy_file_range(2) system call that
the Linux kernel supports.

* 6dd70cc6c0d Update zlib to 1.3.2
zlib was updated to version 1.3.2.

* f0619bb5a53 Run valid tests specified on a command-line, even if mixed
with invalid
When non-existent functions are given on a test's command-line, or a
function is paired with a non-existent data-tag, QtTest previously only
reported these invalid arguments. It now also runs the tests for any
valid arguments they were mixed with.

* 9954a11b0d6 QVariant: fix comparison of unsigned enums to integers
Fixed a bug that caused compare() to return wrong results when
comparing an unsigned enumerator to an integer.

* 6028a98d577 Update to TinyCBOR 7 with CMake support
TinyCBOR updated to version 7.0.

* 37624c637a9 Update Freetype to 2.14.2
Updated bundled Freetype to 2.14.2.

* c6920dd2375 Upgrade Harfbuzz to 13.0.0
Upgraded Harfbuzz to version 13.0.0.

* 8dcd99a9098 SQLite: Update SQLite to v3.51.3
Updated SQLite to v3.51.3, 3.52.0 was withdrawn.

* 390f1c19129  Upgrade Harfbuzz to 13.2.1
Upgraded Harfbuzz to version 13.2.1.

* 6ad90018718 Update Freetype to 2.14.3
Updated bundled Freetype to 2.14.3.

* b6b50998df6 Update bundled libpng to version 1.6.56
libpng was updated to version 1.6.56

* 7ddbc87d8e1 Update bundled libjpeg-turbo to version 3.1.4
libjpeg-turbo was updated to version 3.1.4

### qtmultimedia
* c3a9dd887 Update FFmpeg version in documentation
Updated FFmpeg to n7.1.3.

* 2395e5573 3rdparty: dr_wav - update to 0.14.4
Update bundled dr_wav to 0.14.4

* b7a2d8be3 3rdparty: update to dr_wav v0.14.5
update dr_wav to 0.14.5 due to heap buffer overflow

### qt3d
* 49e9a81bf Update Assimp
Updated Assimp to 6.0.4

### qtnetworkauth
* dfe0543 Reduce strictness of QOAuthUriSchemeReplyHandler path check
Treat empty path and '/' as equivalent when comparing redirect URL.

### qtquick3d
* 7f120de14 Update Assimp to v6.0.4
Updated Assimp to v6.0.4

### qtgrpc
* 7b8f1d05 QGrpcHttp2Channel: configure h2 streams to omit the
downloadBuffer
Disabled unused HTTP/2 buffering, fixing a memory growth issue in long-
running streaming scenarios.

* 541f7d19 Revert "Add FINAL to generated properties"
revert to the previous behavior, then property were not final.


Fixes
-----

### qtbase
* [QTBUG-139212](https://qt-project.atlassian.net/browse/QTBUG-139212) New target form of qt6_wrap_cpp() doesn't work if given
header files
* [QTBUG-143075](https://qt-project.atlassian.net/browse/QTBUG-143075) Tab's left/right (close button) widget didn't scroll
with tab in QTabbar if wheel event has PixelScroll capability
* [QTBUG-142184](https://qt-project.atlassian.net/browse/QTBUG-142184) QRangeModel should not refer to its private
implemantation unqualified
* [QTBUG-141732](https://qt-project.atlassian.net/browse/QTBUG-141732) QLibraryInfo produces incorrect paths on Android.
* [QTBUG-143269](https://qt-project.atlassian.net/browse/QTBUG-143269) QStringView::operator std::u16string_view() not
constexpr
* [QTBUG-70408](https://qt-project.atlassian.net/browse/QTBUG-70408) QPainter rotated by 180deg and drawing QPixmap on it,
picture comes out as not rotated when printing
* [QTBUG-141475](https://qt-project.atlassian.net/browse/QTBUG-141475) Wayland: Warning spew related to QWaylandTextInputv3
under COSMIC
* [QTBUG-143183](https://qt-project.atlassian.net/browse/QTBUG-143183) Noto Color Emojies font is not handled correctly on
older Windows 10 (e.g. 1809, 1903, 2004, 21H2, 22H2...)
* [QTBUG-143174](https://qt-project.atlassian.net/browse/QTBUG-143174) [REG 6.8.3-6.10.1] Sporadic crashes on application exit
* [QTBUG-143293](https://qt-project.atlassian.net/browse/QTBUG-143293) Random colors when drawing emojis with CBDT font +
assertion in debug
* [QTBUG-142185](https://qt-project.atlassian.net/browse/QTBUG-142185) tst_qguieventdispatcher::postEventFromThread is flakey
on macOS 26
* [QTBUG-142664](https://qt-project.atlassian.net/browse/QTBUG-142664) macOS native drawing goes outside widget
* [QTBUG-143469](https://qt-project.atlassian.net/browse/QTBUG-143469) [REG 6.10.1] windows11 style on Windows 10 missing
interface icons
* [QTBUG-143059](https://qt-project.atlassian.net/browse/QTBUG-143059) qt_internal_find_apple_system_framework does not find
frameworks libraries
* [QTBUG-143119](https://qt-project.atlassian.net/browse/QTBUG-143119) QWidget handling QEvent::StyleChange during destruction
* [QTBUG-136485](https://qt-project.atlassian.net/browse/QTBUG-136485) QDockWidgets sends visibilityChanged on destruction
* [QTBUG-143294](https://qt-project.atlassian.net/browse/QTBUG-143294) WebAssembly: inputMethodHints not respected for mobile
virtual keyboard type
* [QTBUG-139218](https://qt-project.atlassian.net/browse/QTBUG-139218) Broken dependencies when qt6_wrap_cpp() is called in a
subdirectory
* [QTBUG-143507](https://qt-project.atlassian.net/browse/QTBUG-143507) Qt 6.8 and higher won't build for x86_64 on macos
* [QTBUG-142460](https://qt-project.atlassian.net/browse/QTBUG-142460) [REG 6.83 -> 6.10.1] App crashes when switching to other
application
* [QTBUG-140674](https://qt-project.atlassian.net/browse/QTBUG-140674) Crash failing to create eglSurface while UI thread
locked by QtAndroidAccessibility
* [QTBUG-140501](https://qt-project.atlassian.net/browse/QTBUG-140501) QDialog is broken on Android platform
* [QTBUG-102594](https://qt-project.atlassian.net/browse/QTBUG-102594) [REG 5.15.6 -> 5.15.9] Many ANR issues by
QtAccessibility
* [QTBUG-105958](https://qt-project.atlassian.net/browse/QTBUG-105958) [Android] Intent + Talkback leads to deadlock
* [QTBUG-112931](https://qt-project.atlassian.net/browse/QTBUG-112931) Android App crash in QtAndroidAccessibility
* [QTBUG-143175](https://qt-project.atlassian.net/browse/QTBUG-143175) [REG] Extreme freezing since 6.9
* [QTBUG-142789](https://qt-project.atlassian.net/browse/QTBUG-142789) QFuture::result() crashes
* [QTBUG-139635](https://qt-project.atlassian.net/browse/QTBUG-139635) Unexpected Result When QLCDNumber::display is Set to
INT_MIN
* [QTBUG-143495](https://qt-project.atlassian.net/browse/QTBUG-143495) Segmentation fault in QEGLPlatformContext::hasExtension
* [QTBUG-142680](https://qt-project.atlassian.net/browse/QTBUG-142680) MERGE_QT_TRANSLATIONS results in duplicate qtdeclarative
lrelease arguments
* [QTBUG-142020](https://qt-project.atlassian.net/browse/QTBUG-142020) Incorrect usage of qFuzzyCompare() abounds in Qt source
[QtCore]
* [QTBUG-143452](https://qt-project.atlassian.net/browse/QTBUG-143452) Crash of TlsKeyOpenSSL::publicKeyFromX509 on Fedora
* [QTBUG-142938](https://qt-project.atlassian.net/browse/QTBUG-142938) Data Race in QProcessEnvironment
* [QTBUG-143739](https://qt-project.atlassian.net/browse/QTBUG-143739) [REG 6.11.0->6.12.0]
tst_QWidget_window::tst_paintEventOnResize_QTBUG50796() is very flaky on
android-16-x86_64-on-linux
* [QTBUG-111229](https://qt-project.atlassian.net/browse/QTBUG-111229) Update 'More efficient string construction'
documentation
* [QTBUG-141083](https://qt-project.atlassian.net/browse/QTBUG-141083) WebEngine build fails with cmake / sbom related error
* [QTBUG-143708](https://qt-project.atlassian.net/browse/QTBUG-143708) Crash when moving undocked dockwidgets above each other
* [QTBUG-143753](https://qt-project.atlassian.net/browse/QTBUG-143753) Dockwidget transitioning from Floating Tabs to untabbed
floating changes position randomly
* [QTBUG-136710](https://qt-project.atlassian.net/browse/QTBUG-136710) QML Image object causes a crash when it gets deleted
while it's still loading
* [QTBUG-143762](https://qt-project.atlassian.net/browse/QTBUG-143762) radio button change does not work when parent widget is
enabled
* [QTBUG-141838](https://qt-project.atlassian.net/browse/QTBUG-141838) QODBC Oracle: “invalid username/password”
* [QTBUG-143710](https://qt-project.atlassian.net/browse/QTBUG-143710) Copy to clipboard removes newlines from text
* [QTBUG-135817](https://qt-project.atlassian.net/browse/QTBUG-135817) [REG 6.7.2 -> Qt 6.8.2] Windows:
QFontDatabase::families() does not list stylistic variants of families
* [QTBUG-143305](https://qt-project.atlassian.net/browse/QTBUG-143305) Wayland reconnect: QWaylandClientExtension will emit
activeChanged signal before event loop init.
* [QTBUG-143046](https://qt-project.atlassian.net/browse/QTBUG-143046) QTableWidget drop-and-drop indicator calculation is
always based on visualRect of the first column cell
* [QTBUG-143544](https://qt-project.atlassian.net/browse/QTBUG-143544) QDateTime editor shows local time while view shows UTC
* [QTBUG-143529](https://qt-project.atlassian.net/browse/QTBUG-143529) Qt Quick rendering (with D3D11 RHI) may cause NVidia GPU
device suspension
* [QTBUG-143607](https://qt-project.atlassian.net/browse/QTBUG-143607) Suspicious behavior of QUrl::toAce /
QString::normalized(NFC)
* [QTBUG-121987](https://qt-project.atlassian.net/browse/QTBUG-121987) Creating a new QMouseEvent can change globalPosition()
in other QMouseEvents
* [QTBUG-89486](https://qt-project.atlassian.net/browse/QTBUG-89486) Qt6 QMouseEvent invisibly overwrite last event global
position
* [QTBUG-143746](https://qt-project.atlassian.net/browse/QTBUG-143746) Specificity is lost with too many style rules
* [QTBUG-125197](https://qt-project.atlassian.net/browse/QTBUG-125197) QWidget multitouch sometimes drops touch points
* [QTBUG-67819](https://qt-project.atlassian.net/browse/QTBUG-67819) QGraphicsViewProxy does not propagate touch events to the
child of the widget
* [QTBUG-45737](https://qt-project.atlassian.net/browse/QTBUG-45737) No touch events handling (QGraphicsProxyWidget / QWidget)
* [QTBUG-144140](https://qt-project.atlassian.net/browse/QTBUG-144140) macdeployqt spends a lot of time updating install names
to the same value
* [QTBUG-144009](https://qt-project.atlassian.net/browse/QTBUG-144009) FAIL!  :
qmltestrunner::mouserelease::test_dragAxis(horizontal) Compared values
are not the same
* [QTBUG-143440](https://qt-project.atlassian.net/browse/QTBUG-143440) testlib crashes when encountering unknown test function
passed on command line
* [QTBUG-144142](https://qt-project.atlassian.net/browse/QTBUG-144142) copy_file_range may return ENOSYS inside some container
environments
* [QTBUG-136689](https://qt-project.atlassian.net/browse/QTBUG-136689) Crash in QImageData constructor due to a race condition
* [QTBUG-142029](https://qt-project.atlassian.net/browse/QTBUG-142029) QOpenGL crash with CGLFlushDrawable on Macos 26 (clang17
compiler)
* [QTBUG-143699](https://qt-project.atlassian.net/browse/QTBUG-143699) Crash in QOpenGLFunctions::glClear in various Controls
auto tests
* [QTBUG-143478](https://qt-project.atlassian.net/browse/QTBUG-143478) QT_QPA_DEFAULT_PLATFORM=wayland leads to broken binaries
in static build
* [QTBUG-125246](https://qt-project.atlassian.net/browse/QTBUG-125246) PNG with invalid colorSpace doesn't preserve ICC data
* [QTBUG-139957](https://qt-project.atlassian.net/browse/QTBUG-139957) QPushButton menu arrow shifts position/size when border
is applied via stylesheet
* [QTBUG-129099](https://qt-project.atlassian.net/browse/QTBUG-129099) tst_Q***AnimationGroup is flaky on webOS
* [QTBUG-135748](https://qt-project.atlassian.net/browse/QTBUG-135748) Mouse drag/gestures don't work on Android
* [QTBUG-138343](https://qt-project.atlassian.net/browse/QTBUG-138343) [Android][Mouse Input] Sliders and Dials Stop Responding
When Cursor Leaves Widget Bounds
* [QTBUG-143287](https://qt-project.atlassian.net/browse/QTBUG-143287) QNetworkInformation::loadBackendByFeatures crashes
sometimes
* [QTBUG-140872](https://qt-project.atlassian.net/browse/QTBUG-140872) Diagram not readable in black mode
* [QTBUG-144202](https://qt-project.atlassian.net/browse/QTBUG-144202) QTabBar/QTabWidget tab's close button is not animated
when the tab snaps to new position
* [QTBUG-143562](https://qt-project.atlassian.net/browse/QTBUG-143562) Assertion failure in
QSortFilterProxyModel::mapFromSource() after upgrading from Qt 6.8.3 to
Qt 6.8.6
* [QTBUG-132695](https://qt-project.atlassian.net/browse/QTBUG-132695) Crash in QGuiApplication::applicationStateChanged() when
quitting app
* [QTBUG-143204](https://qt-project.atlassian.net/browse/QTBUG-143204) Android GUI application crashes at the moment of
terminating
* [QTBUG-133404](https://qt-project.atlassian.net/browse/QTBUG-133404) Visual aliasing glitches when using scale other than
100% in Windows
* [QTBUG-144266](https://qt-project.atlassian.net/browse/QTBUG-144266) On Windows platform, visual artifacts remain on the
screen when moving a widget window within the main application window.
* [QTBUG-144526](https://qt-project.atlassian.net/browse/QTBUG-144526) QFontInfo does not return weight or style on Windows
* [QTBUG-131671](https://qt-project.atlassian.net/browse/QTBUG-131671) On iOS, CTR, ALT, SHIFT and COMMAND keys are not
detected
* [QTBUG-143969](https://qt-project.atlassian.net/browse/QTBUG-143969) Cannot select text in subwindow on Android
* [QTBUG-144549](https://qt-project.atlassian.net/browse/QTBUG-144549) When using QGraphicsGridLayout on Wayland, grid is
misaligned when rendered through QPicture
* [QTBUG-140507](https://qt-project.atlassian.net/browse/QTBUG-140507) Incorrect palette colors when enabling a contrast theme
while a hybrid widgets + quick application is running.
* [QTBUG-143208](https://qt-project.atlassian.net/browse/QTBUG-143208) Fix QTestAccessibility various problems
* [QTBUG-142915](https://qt-project.atlassian.net/browse/QTBUG-142915) crash because of wayland error "unknown object xxx,
message error(ous)"
* [QTBUG-137401](https://qt-project.atlassian.net/browse/QTBUG-137401) QScrollBar attached to QScrollArea visibility is not
updated correctly
* [QTBUG-46195](https://qt-project.atlassian.net/browse/QTBUG-46195) [Windows]: Swipe gesture is not always recognized and
sometimes in the wrong direction
* [QTBUG-138601](https://qt-project.atlassian.net/browse/QTBUG-138601) Swipe gesture does not work on Windows
* [QTBUG-14895](https://qt-project.atlassian.net/browse/QTBUG-14895) Qt Gestures - Pan and Swipe are not working
* [QTBUG-101426](https://qt-project.atlassian.net/browse/QTBUG-101426) QMetaObjectBuilder does not properly carry property
flags
* [QTBUG-141785](https://qt-project.atlassian.net/browse/QTBUG-141785) qtwebengine builds on windows don't /mostly/ use sccache
* [QTBUG-141803](https://qt-project.atlassian.net/browse/QTBUG-141803) Qt doesn't help debug "Unknown exception is thrown from
an Qt event handler"
* [QTBUG-143861](https://qt-project.atlassian.net/browse/QTBUG-143861) HTTP/2: Ensure that SETTINGS_MAX_FRAME_SIZE is respected
* [QTBUG-96239](https://qt-project.atlassian.net/browse/QTBUG-96239) Document CMake component in CMake function documentation
* [QTBUG-143608](https://qt-project.atlassian.net/browse/QTBUG-143608) QTableView/QTableWidget: scrolling issues when moving a
row/column header section outside the viewport
* [QTBUG-144206](https://qt-project.atlassian.net/browse/QTBUG-144206) Qt Designer: Item widgets' items lack fully-qualified
enums
* [PYSIDE-2492](https://qt-project.atlassian.net/browse/PYSIDE-2492) uic does not generate enumeration name into enum values
causing type checking warnings
* [PYSIDE-3278](https://qt-project.atlassian.net/browse/PYSIDE-3278) pyside6-uic: Item widgets' items have enum setters that
are inconsistent with those of other classes
* [QTBUG-135968](https://qt-project.atlassian.net/browse/QTBUG-135968) Top flaky test: tst_QFreeList::threadedTest
* [QTBUG-144462](https://qt-project.atlassian.net/browse/QTBUG-144462) AnnouncementPoliteness not respected on iOS
* [QTBUG-143054](https://qt-project.atlassian.net/browse/QTBUG-143054) meta-qt6 should support reproduce build
* [QTBUG-144257](https://qt-project.atlassian.net/browse/QTBUG-144257) Significant memory usage increase after upgrading from
Qt 6.6.1 to Qt 6.10.1 on Windows (10/11) and macOS

### qtsvg
* [QTBUG-143451](https://qt-project.atlassian.net/browse/QTBUG-143451) QSvgGenerator does not properly close path with "Z"

### qtdeclarative
* [QTBUG-139362](https://qt-project.atlassian.net/browse/QTBUG-139362) ColorDialog fails to display colors
* [QTBUG-141830](https://qt-project.atlassian.net/browse/QTBUG-141830) Sorted QSortFilterProxyModel crash in static builds
* [QTBUG-107028](https://qt-project.atlassian.net/browse/QTBUG-107028) tst_qquicktextfield and tst_qquicktextarea fail on
Android
* [QTBUG-142514](https://qt-project.atlassian.net/browse/QTBUG-142514) callArrowFunction / callObjectPropertyLookup randomly
crashing when receiving notifications
* [QTBUG-143374](https://qt-project.atlassian.net/browse/QTBUG-143374) [REG Qt 6.11.0 Beta 1] Missing
Qt6::QuickControls2FusionPrivate
* [QTBUG-142658](https://qt-project.atlassian.net/browse/QTBUG-142658) [Reg 6.5.10 -> 6.8.5] QQmlFileSelector's selection
inappropriately propagates to subsequent engines
* [QTBUG-143112](https://qt-project.atlassian.net/browse/QTBUG-143112) Fill not correctly rendered by curve renderer when pack
goes backwards
* [QTBUG-142577](https://qt-project.atlassian.net/browse/QTBUG-142577) Qt Designer on Mac OS fails to load a custom widget
plugin due to code signature issue
* [QTBUG-134502](https://qt-project.atlassian.net/browse/QTBUG-134502) The app crashes with ListView when using contentHeight
and fast scrolling with a mouse wheel.
* [QTBUG-121361](https://qt-project.atlassian.net/browse/QTBUG-121361) Document that QML_EXTENDED is *not* meant for extending
types you don't control
* [QTBUG-138193](https://qt-project.atlassian.net/browse/QTBUG-138193) QML menu set to visible on creation doesn't show
* [QTBUG-142574](https://qt-project.atlassian.net/browse/QTBUG-142574) qmlls crashes in QQmlJSScopesById::possibleIds
* [QTBUG-128664](https://qt-project.atlassian.net/browse/QTBUG-128664) Document that you need to declare DEPENDENCIES in order
to use other modules' C++ types in your module
* [QTBUG-143547](https://qt-project.atlassian.net/browse/QTBUG-143547) [Reg 6.10.1->6.10.2]: Application palette is reset after
loading a QQuickWidget
* [QTBUG-143479](https://qt-project.atlassian.net/browse/QTBUG-143479) [Reg 6.10.1 -> 6.11.0b2] macdeployqt fails on *.conf
files
* [QTBUG-143731](https://qt-project.atlassian.net/browse/QTBUG-143731) Qmlformat cannot format when existing properties are
used that are set further below
* [QTBUG-142074](https://qt-project.atlassian.net/browse/QTBUG-142074) readonly TextInput cause warning that application copied
from clipboard on Android
* [QTBUG-143554](https://qt-project.atlassian.net/browse/QTBUG-143554) "" == 0   returns false in the compiler
* [QTBUG-140507](https://qt-project.atlassian.net/browse/QTBUG-140507) Incorrect palette colors when enabling a contrast theme
while a hybrid widgets + quick application is running.
* [QTBUG-140155](https://qt-project.atlassian.net/browse/QTBUG-140155) Qmllint issue when using Controls.SpinBox.textFromValue
* [QTBUG-123141](https://qt-project.atlassian.net/browse/QTBUG-123141) A description about Loader is not clear enough
* [QTBUG-141246](https://qt-project.atlassian.net/browse/QTBUG-141246) qmlls fix for unqualified access is applied in the wrong
place
* [QTBUG-143823](https://qt-project.atlassian.net/browse/QTBUG-143823) qmllint suggests correct and wrong fix at the same time
* [QTBUG-64656](https://qt-project.atlassian.net/browse/QTBUG-64656) Wrong name for DragEvent.source propery
* [QTBUG-143857](https://qt-project.atlassian.net/browse/QTBUG-143857) QQuickWidget forgets its clearColor if its underlying
window changes
* [QTBUG-142511](https://qt-project.atlassian.net/browse/QTBUG-142511) FileDialog use with -no-feature-accessibility broken
* [QTBUG-143771](https://qt-project.atlassian.net/browse/QTBUG-143771) qmlcachegen crash with eval in if .. else when
generating cpp file
* [QTBUG-46434](https://qt-project.atlassian.net/browse/QTBUG-46434) QQuickPaintedItem crash when toggling antialiasing
* [QTBUG-132163](https://qt-project.atlassian.net/browse/QTBUG-132163) Animator crashes when paused is used
* [QTBUG-134749](https://qt-project.atlassian.net/browse/QTBUG-134749) Various ASAN crashes in QJSEngine
* [QTBUG-144092](https://qt-project.atlassian.net/browse/QTBUG-144092) Cannot assign to list of inline component type when
using multiple qml engines
* [QTBUG-144182](https://qt-project.atlassian.net/browse/QTBUG-144182) "ERROR: AddressSanitizer: stack-use-after-return" in
tst_qqmlnotifier destruction
* [QTBUG-139426](https://qt-project.atlassian.net/browse/QTBUG-139426) qmlformat adds extra newline for components only
containing id property
* [QTBUG-141347](https://qt-project.atlassian.net/browse/QTBUG-141347) [REG 6.10.X -> 6.11.0] Quick Gallery shows only blank
screen
* [QTBUG-139255](https://qt-project.atlassian.net/browse/QTBUG-139255) [Regr: 6.8.2->6.9.0] Focus restore problem on closing
popup
* [QTBUG-143473](https://qt-project.atlassian.net/browse/QTBUG-143473) Memory leak due to changes to garbage collection
introduced in 6.10.0
* [QTBUG-141729](https://qt-project.atlassian.net/browse/QTBUG-141729) QmlCompiler fail
* [QTBUG-137396](https://qt-project.atlassian.net/browse/QTBUG-137396) No documentation for why you shouldn't refer to an id in
the root object from other components
* [QTBUG-136650](https://qt-project.atlassian.net/browse/QTBUG-136650) Not possible to have a frameless QML ColorDialog
* [QTBUG-144327](https://qt-project.atlassian.net/browse/QTBUG-144327) [REG 6.9 → 6.10] Crash in
QQmlComponentAndAliasResolver<QQmlTypeCompiler>::resolveAliasesInObject
* [QTBUG-144137](https://qt-project.atlassian.net/browse/QTBUG-144137) D3D11 RHI crash with Qt 6.10.x
* [QTBUG-142369](https://qt-project.atlassian.net/browse/QTBUG-142369) Property bevel of RectangleShape is not working
* [QTBUG-143721](https://qt-project.atlassian.net/browse/QTBUG-143721) Behavior: False warning when targeting multiple grouped
properties
* [QTBUG-143582](https://qt-project.atlassian.net/browse/QTBUG-143582) SearchField.forceActiveFocus() doesn't work
* [QTBUG-141374](https://qt-project.atlassian.net/browse/QTBUG-141374) QML tools cannot see QAccessibilityHints
* [QTBUG-142723](https://qt-project.atlassian.net/browse/QTBUG-142723) Crash in QQuickWindowPrivate::polishItems
* [QTBUG-105906](https://qt-project.atlassian.net/browse/QTBUG-105906) [Reg 5.15.5->5.15.6] The fix for the QTBUG-89736 causes
a crash
* [QTBUG-72910](https://qt-project.atlassian.net/browse/QTBUG-72910) Running on a dangling pointer, when deleting the
activeFocusItem inside of QQuickItem::updatePolish
* [QTBUG-144701](https://qt-project.atlassian.net/browse/QTBUG-144701) [REG 6.10.2 → 6.10.3, 6.11] Valid QML code fails to load
with wrong error about property assignment
* [QTBUG-141913](https://qt-project.atlassian.net/browse/QTBUG-141913) SortFilterProxyModel: Not be able to run demo using
`qml` utility
* [QTBUG-30801](https://qt-project.atlassian.net/browse/QTBUG-30801) Button: tooltip not shown when the button is disabled
* [QTBUG-130899](https://qt-project.atlassian.net/browse/QTBUG-130899) Disabled item does not disable its HoverHandler
* [QTBUG-141963](https://qt-project.atlassian.net/browse/QTBUG-141963) GC Sweep logic is broken and masks life time bug in
QQmlDelegateModel
* [QTBUG-143282](https://qt-project.atlassian.net/browse/QTBUG-143282) qdoc: \summary directive apparently causes mixup in the
webxml  generator
* [QTBUG-143312](https://qt-project.atlassian.net/browse/QTBUG-143312) tst_qquickcanvasitem keeps failing on qnx with timeouts
* [QTBUG-143313](https://qt-project.atlassian.net/browse/QTBUG-143313) qmllint -  warnings about shadowing methods need to
silenced until they become actionable
* [QTBUG-143483](https://qt-project.atlassian.net/browse/QTBUG-143483) Document new qmllint warnings (qmlShadow,
qmlPropertyOverride, qmlIdShadowsMember, ...)
* [QTBUG-129176](https://qt-project.atlassian.net/browse/QTBUG-129176) [REG Qt 6.7.2-> 6.8.0-beta4] Crash in
QRawFont::pathForGlyph() / black screen
* [QTBUG-143071](https://qt-project.atlassian.net/browse/QTBUG-143071) Sporadic crashes on
QSGDistanceFieldGlyphCache::release()
* [QTBUG-129088](https://qt-project.atlassian.net/browse/QTBUG-129088) Support Contrast themes in FluentWinUI3
* [QTBUG-136120](https://qt-project.atlassian.net/browse/QTBUG-136120) Qml Runtime fails to correct escape -a after --
* [QTBUG-143361](https://qt-project.atlassian.net/browse/QTBUG-143361) QML Connections component crashes if creating many
Connections that target the same instance
* [QTBUG-142132](https://qt-project.atlassian.net/browse/QTBUG-142132) QML TextField advertises AT-SPI "editable text"
interface, but does not implement it, cannot set text
* [QTBUG-108005](https://qt-project.atlassian.net/browse/QTBUG-108005) PathView distorts TouchEvents
* [QTBUG-137823](https://qt-project.atlassian.net/browse/QTBUG-137823) Tab order does not follow visual order
* [QTBUG-143701](https://qt-project.atlassian.net/browse/QTBUG-143701) tst_QQuickContextMenu::textControlsMenuKey is flaky on
several platforms
* [QTBUG-131777](https://qt-project.atlassian.net/browse/QTBUG-131777) Required properties enforcement in qmltc is broken
* [QTBUG-144451](https://qt-project.atlassian.net/browse/QTBUG-144451) QDoc: \include snippet matching uses substring instead
of exact name
* [QTBUG-143978](https://qt-project.atlassian.net/browse/QTBUG-143978) [REG 6.8.3 - 6.10.1] Sporadic crashes at
QQuickBasicTheme::initialize()
* [QTBUG-
144397](https://qt-project.atlassian.net/browse/QTBUG-144397) tst_qquickstyle::defaultPaletteIsUpdatedWhenChangingColorScheme()
crashes on Ubuntu
* [QTBUG-142021](https://qt-project.atlassian.net/browse/QTBUG-142021) Child of FlexboxLayout with fillX is misaligned on
primary axis
* [QTBUG-141055](https://qt-project.atlassian.net/browse/QTBUG-141055) FlexboxLayout incorrectly calculates it's size

### qtactiveqt
* [QTBUG-144470](https://qt-project.atlassian.net/browse/QTBUG-144470) SBOM: SPDXRef-Package-qtactiveqt-qt-module-ActiveQt
declares wrong license

### qtmultimedia
* [QTBUG-143117](https://qt-project.atlassian.net/browse/QTBUG-143117) QtMultimedia QAudioBuffer typo in documentation
(unsiged, siged).
* [QTBUG-143116](https://qt-project.atlassian.net/browse/QTBUG-143116) Built-in example audiosource is unable to read audio on
macOS with specific USB devices
* [QTBUG-140424](https://qt-project.atlassian.net/browse/QTBUG-140424) QMediaRecorder::RecorderState is not recognized by QML
tools
* [QTBUG-143747](https://qt-project.atlassian.net/browse/QTBUG-143747) qtmultimedia fails to compile with FFMPEG 8.x on Android
* [QTBUG-139174](https://qt-project.atlassian.net/browse/QTBUG-139174) REG->6.9.1: Windows: Using QCamera with a QVideoSink
fails to stop video capture when used in a QQuickPaintedItem
* [QTBUG-122141](https://qt-project.atlassian.net/browse/QTBUG-122141) opus: Could not write header
* [QTBUG-144097](https://qt-project.atlassian.net/browse/QTBUG-144097) [Regression] iOS camera stops emitting frames after
short delay
* [QTBUG-131154](https://qt-project.atlassian.net/browse/QTBUG-131154) [Boot2Qt] Slow Video and Camera Rendering in Multimedia
Examples
* [QTBUG-144268](https://qt-project.atlassian.net/browse/QTBUG-144268) Incorrect behavior documented for QAudioSink::resume()
and related methods
* [QTBUG-143062](https://qt-project.atlassian.net/browse/QTBUG-143062) [darwin] Sporadic crashes on QMediaRecorder::record
(recording an audio)
* [QTBUG-137845](https://qt-project.atlassian.net/browse/QTBUG-137845) [Boot2Qt] The content of MPEG video file is corrupted
when playing on i.MX 8M Mini EVK
* [QTBUG-143570](https://qt-project.atlassian.net/browse/QTBUG-143570) Regression in Qt 6.10+: PipeWire backend has incomplete
support for virtual audio devices
* [QTBUG-143627](https://qt-project.atlassian.net/browse/QTBUG-143627) Incorrect usage of qFuzzyCompare() abounds in Qt source
[QtMulitmedia]
* [QTBUG-142939](https://qt-project.atlassian.net/browse/QTBUG-142939) [REG 6.8.3 - 6.10.1][macOS] Sporadic crashes related to
DeviceDisconnectMonitor
* [QTBUG-96239](https://qt-project.atlassian.net/browse/QTBUG-96239) Document CMake component in CMake function documentation

### qttools
* [QTBUG-143192](https://qt-project.atlassian.net/browse/QTBUG-143192) Documentation of overloaded signals/slots shows wrong
snippets
* [QTBUG-143212](https://qt-project.atlassian.net/browse/QTBUG-143212) QDoc: Empty link target causes crash
* [QTBUG-143311](https://qt-project.atlassian.net/browse/QTBUG-143311) Designer crashes when  double clicking widget to inline-
edit text while inline editor of another form is active
* [QTBUG-143475](https://qt-project.atlassian.net/browse/QTBUG-143475) Unnecessary warning when -no-feature-qdoc is used
* [QTBUG-143496](https://qt-project.atlassian.net/browse/QTBUG-143496) Plural TS files generated by qt_add_translations() have
incorrect source file paths
* [QTBUG-142808](https://qt-project.atlassian.net/browse/QTBUG-142808) \sa with link name part behaves differently to \l
* [QTBUG-109117](https://qt-project.atlassian.net/browse/QTBUG-109117) QDoc \qmldefault and \readonly commands are not
supported together
* [QTBUG-143375](https://qt-project.atlassian.net/browse/QTBUG-143375) Overloaded tr method triggers “Class 'MyNamespace' lacks
Q_OBJECT macro” error
* [QTBUG-143960](https://qt-project.atlassian.net/browse/QTBUG-143960) SBOM: Improve the content of the LibClang dependency
* [QTBUG-142742](https://qt-project.atlassian.net/browse/QTBUG-142742) QDoc core dumps when the include path is invalid
* [QTBUG-143893](https://qt-project.atlassian.net/browse/QTBUG-143893) qttools: lupdate Objective-C calls misinterpreted as C++
attributes

### qtdoc
* [QTBUG-143651](https://qt-project.atlassian.net/browse/QTBUG-143651) Do not translate proper nouns
* [QTBUG-144172](https://qt-project.atlassian.net/browse/QTBUG-144172) Doc: Qt Platform Integration project is not visible in
the TOC tree
* [QTBUG-142730](https://qt-project.atlassian.net/browse/QTBUG-142730) Demos contain orphaned references to unused custom QML
types generated by Qt Design Studio
* [QTBUG-143634](https://qt-project.atlassian.net/browse/QTBUG-143634) Qt Graphs CSV Demo does not validate input values before
rendering, causing integer overflow in texture size calculation
* [QTBUG-144477](https://qt-project.atlassian.net/browse/QTBUG-144477) Update list of GPL components in licenses.html

### qtlocation
* [QTBUG-144282](https://qt-project.atlassian.net/browse/QTBUG-144282) Incorrect usage of qFuzzyCompare() abounds in Qt source
[Qt Location]

### qtpositioning
* [QTBUG-142317](https://qt-project.atlassian.net/browse/QTBUG-142317) QGeoPath.contains() does not work correctly
* [QTBUG-142752](https://qt-project.atlassian.net/browse/QTBUG-142752) [Android] Keyboard reappears after tab switch when input
field remains focused in Satellite Info example app
* [QTBUG-143660](https://qt-project.atlassian.net/browse/QTBUG-143660) Incorrect usage of qFuzzyCompare() abounds in Qt source
[Qt Positioning]

### qtconnectivity
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtwebsockets
* [QTBUG-141396](https://qt-project.atlassian.net/browse/QTBUG-141396) Regarding Qt WebSocket, accessing the IP address and
port via wss fails.
* [QTBUG-135959](https://qt-project.atlassian.net/browse/QTBUG-135959) tst_QWebSocket::moveToThreadNoWarning is failing

### qtwebengine
* [QTBUG-142497](https://qt-project.atlassian.net/browse/QTBUG-142497) [REG 6.10.0->6.10.1] RKWard and slitherer crashed when
starting with Qt 6.10.1
* [QTBUG-142720](https://qt-project.atlassian.net/browse/QTBUG-142720) Crash in Qt6WebEngineCore during GPUInfo initialization
* [QTBUG-139335](https://qt-project.atlassian.net/browse/QTBUG-139335) QtWebEngine based browser shows nothing with MESA
LLVMpipe
* [QTBUG-142534](https://qt-project.atlassian.net/browse/QTBUG-142534) [REG 6.10.1-6.10.2] Broken rendering when reparenting
WebEngineView to another window (again)
* [QTBUG-141739](https://qt-project.atlassian.net/browse/QTBUG-141739) [REG 6.9.2-6.9.3] Sporadic deadlocks on WebEngineView
destruction
* [QTBUG-131304](https://qt-project.atlassian.net/browse/QTBUG-131304) Broken rendering when reparenting WebEngineView to
another window
* [QTBUG-141214](https://qt-project.atlassian.net/browse/QTBUG-141214) WebEngine freezes UI
* [QTBUG-142667](https://qt-project.atlassian.net/browse/QTBUG-142667) Building 6.5.11 WebEngine fails on Ubuntu 22.04
* [QTBUG-124576](https://qt-project.atlassian.net/browse/QTBUG-124576) Cannot build QtWebEngine
* [QTBUG-142323](https://qt-project.atlassian.net/browse/QTBUG-142323) QtWebEngine blocks building with MSVC Tooset 14.5 (VS2026)
* [QTBUG-143625](https://qt-project.atlassian.net/browse/QTBUG-143625) Incorrect usage of qFuzzyCompare() abounds in Qt source
[QtWebEngine]
* [QTBUG-131640](https://qt-project.atlassian.net/browse/QTBUG-131640) WebEngine not starting on properly when deployed with
specific structure on Windows
* [QTBUG-144270](https://qt-project.atlassian.net/browse/QTBUG-144270) QTWEBENGINE_RESOURCES_PATH does not work on Windows
* [QTBUG-80941](https://qt-project.atlassian.net/browse/QTBUG-80941) Chromium command line arguments for TLS versions/ciphers
don't work
* [QTBUG-141785](https://qt-project.atlassian.net/browse/QTBUG-141785) qtwebengine builds on windows don't /mostly/ use sccache
* [QTBUG-138734](https://qt-project.atlassian.net/browse/QTBUG-138734) webengine pdf example: runtime warnings
* [QTBUG-122655](https://qt-project.atlassian.net/browse/QTBUG-122655) 6.8.0 toplevel build fails on macOS, qtwebengine
* [QTBUG-142247](https://qt-project.atlassian.net/browse/QTBUG-142247) [REG 6.10.0 -> .1] SIGTRAP when accessing
QWebEngineExtensionManager of off-the-record profile

### qtdatavis3d
* [QTBUG-143622](https://qt-project.atlassian.net/browse/QTBUG-143622) Incorrect usage of qFuzzyCompare() abounds in Qt source
[QtGraphs and QtDatavis]

### qtnetworkauth
* [QTBUG-141774](https://qt-project.atlassian.net/browse/QTBUG-141774) openSUSE 16.0 qtnetworkauth -
tst_oauthurischemereplyhandler failed with timeout

### qtquicktimeline
* [QTBUG-131755](https://qt-project.atlassian.net/browse/QTBUG-131755) QML module QtQuick.Timeline.BlendTrees depend on non-
existing QML module QtQuickTimeline

### qtquick3d
* [QDS-12497](https://qt-project.atlassian.net/browse/QDS-12497) Emissive material RGB Factor slider control maxes out at 16.
* [QTBUG-143480](https://qt-project.atlassian.net/browse/QTBUG-143480) qtquick3d: Build failure on Linux with EGL + Vulkan -
missing EGL/egl.h include in qopenxrplatform_p.h
* [QTBUG-143629](https://qt-project.atlassian.net/browse/QTBUG-143629) Qt 6.11 Beta broken Shadows. The shadowMapFar is not any
effects.
* [QTBUG-144101](https://qt-project.atlassian.net/browse/QTBUG-144101) EmitMode is incorrectly EmitType in docs
* [QTBUG-143886](https://qt-project.atlassian.net/browse/QTBUG-143886) Unexpected behavior of Quaternion.lookAt (NaN output)
* [QTBUG-137143](https://qt-project.atlassian.net/browse/QTBUG-137143) RuntimeLoader example fails on Android because assimp
plugin is not deployed

### qthttpserver
* [QTBUG-143595](https://qt-project.atlassian.net/browse/QTBUG-143595) [Examples] 'Simple HTTP Server' example is not listed
under networking examples

### qtgrpc
* [QTBUG-142473](https://qt-project.atlassian.net/browse/QTBUG-142473) Linear memory growth observed with Qt GRPC during long
run
* [QTBUG-96239](https://qt-project.atlassian.net/browse/QTBUG-96239) Document CMake component in CMake function documentation

### qtquickeffectmaker
* [QTBUG-143111](https://qt-project.atlassian.net/browse/QTBUG-143111) 'Qt Quick Effect Maker' two-level entry in documentation
tree

### qtgraphs
* [QTBUG-142918](https://qt-project.atlassian.net/browse/QTBUG-142918) graph isnt updating when upper or lower series is
switched
* [QTBUG-142923](https://qt-project.atlassian.net/browse/QTBUG-142923) Adjusting barThickness or barSpacing does not trigger
redraw
* [QTBUG-143351](https://qt-project.atlassian.net/browse/QTBUG-143351) Axis labels do not get the correct label color in some
cases
* [QTBUG-142814](https://qt-project.atlassian.net/browse/QTBUG-142814) Theme updates do not take effect if the theme is shared
with several 3D graphs
* [QTBUG-138863](https://qt-project.atlassian.net/browse/QTBUG-138863) selectedPoint in Surface3DSeries does not work
* [QTBUG-143484](https://qt-project.atlassian.net/browse/QTBUG-143484) Floor size is not updated with margins in Bars3D
* [QTBUG-143548](https://qt-project.atlassian.net/browse/QTBUG-143548) LegendData doesn't update to reflect on explicit series
color if set on runtime
* [QTBUG-142944](https://qt-project.atlassian.net/browse/QTBUG-142944) Graphs3D.GridLineType.Shader renders incorrectly
* [QTBUG-143611](https://qt-project.atlassian.net/browse/QTBUG-143611) Weird behaviour in surface
* [QTBUG-143750](https://qt-project.atlassian.net/browse/QTBUG-143750) setRotation in QBarDataItem does not trigger a redraw
* [QTBUG-143741](https://qt-project.atlassian.net/browse/QTBUG-143741) tst_barstest Camera target sliders are not updating
graph position
* [QTBUG-143740](https://qt-project.atlassian.net/browse/QTBUG-143740) Floor grid is not updated when floor level is adjusted
in Bars3D
* [QTBUG-143751](https://qt-project.atlassian.net/browse/QTBUG-143751) setMeshAngle in QBar3DSeries causes rendering errors
* [QTBUG-137392](https://qt-project.atlassian.net/browse/QTBUG-137392) Update not taken in account on selected pie in PieChart
* [QTBUG-143622](https://qt-project.atlassian.net/browse/QTBUG-143622) Incorrect usage of qFuzzyCompare() abounds in Qt source
[QtGraphs and QtDatavis]

### qtapplicationmanager (Commercial only)
* [QTBUG-129127](https://qt-project.atlassian.net/browse/QTBUG-129127) Fix problems with the new am_package CMake macros

Known Issues
------------
* Check that your system meets Qt's requirements:
  https://doc-snapshots.qt.io/qt6-6.10/supported-platforms.html
* RTA reported issues from Qt 6.10
  https://qt-project.atlassian.net/issues/?filter=10825
* See Qt 6.10 known issues from:
  https://wiki.qt.io/Qt_6.10_Known_Issues
* Qt 6.10.3 Open issues in Jira:
  https://qt-project.atlassian.net/issues/?filter=21721

Credits for the release goes to:
---------------------------------

Eirik Aavitsland  
Laszlo Agocs  
Dilek Akcay  
Alexander Akulich  
Konsta Alajärvi  
Even Oscar Andersen  
Dimitrios Apostolou  
Albert Astals Cid  
Mate Barany  
Andreas Belke  
Vladimir Belyavsky  
Nicholas Bennett  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
David Boddie  
Tatiana Borisova  
Joerg Bornemann  
Rym Bouabid  
Assam Boudjelthia  
Marcell Brauner  
Aurélien Brooke  
Kai Uwe Broulik  
Alex Bu  
Eren Bursali  
Olivier De Cannière  
Alexei Cazacov  
Kaloyan Chehlarski  
Luqiao Chen  
Wang Chuan  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Pavel Dubsky  
David Edmundson  
Oliver Eftevaag  
Christian Ehrlicher  
Hatem ElKharashy  
Andreas Eliasson  
Fabio Falsini  
Joshua Goins  
Robert Griebl  
Jan Grulich  
Nicolas Guichard  
Mikko Hallamaa  
Jani Heikkinen  
Miikka Heikkinen  
Moss Heim  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Dominik Holland  
Mats Honkamaa  
Samuli Hölttä  
Masoud Jami  
Morteza Jamshidi  
Allan Sandfeld Jensen  
Jonas Karlsson  
Rainer Keller  
Igor Khanin  
Dennis Kim  
Friedemann Kleint  
Michal Klocek  
Jarek Kobus  
Sze Howe Koh  
Niko Korkala  
Tomi Korpipää  
Fabian Kosmale  
Mike Krus  
Santhosh Kumar  
Kai Köhne  
Inho Lee  
Frédéric Lefebvre  
Wladimir Leuschner  
Xiong LinLin  
Jie Liu  
David Loki  
Robert Löhning  
Thiago Macieira  
Marc Mutz  
Antti Määttä  
Andy Nichols  
Mårten Nordheim  
Dennis Oberst  
Frank Osterfeld  
Matti Paaso  
Kwanghyo Park  
Jerome Pasion  
Miika Pernu  
Samuli Piippo  
Timur Pocheptsov  
Lauri Pohjanheimo  
Rami Potinkara  
Lorn Potter  
Sakaria Pouke  
Dheerendra Purohit  
MohammadHossein Qanbari  
Topi Reinio  
Shawn Rutledge  
Ahmad Samir  
Lars Schmertmann  
Sami Shalayel  
Nils Petter Skålerud  
Ivan Solovev  
Axel Spoerl  
Christian Strømme  
Lars Sutterud  
Tasuku Suzuki  
Jan Arve Sæther  
Morten Sørvig  
Esa Törmänen  
Sami Varanka  
Peter Varga  
Doris Verria  
Tor Arne Vestbø  
Juha Vuolle  
Jannis Völker  
Miao Wang  
Yixue Wang  
Bernd Weimer  
Edward Welbourne  
Paul Wicking  
Piotr Wiercinski  
Oliver Wolff  
Semih Yavuz  
Zhao Yuhang  
Oleksii Zbykovskyi  
Wang Zichong  
