Release notes
=============
Qt 6.11.1 release is a patch release made on the top of Qt 6.11.0.
As a patch release, Qt 6.11.1 does not add any new functionality but provides
bug fixes and other improvements and maintains both forward and backward
compatibility (source and binary) with the 6.11.x series.

For detailed information about Qt 6.11, refer to the online documentation
included in this distribution. The documentation is also available online:

https://doc.qt.io/qt-6/index.html

The Qt version 6.11 series is binary compatible with the 6.10.x series.
Applications compiled for 6.10 will continue to run with 6.11.

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
* [CVE-2026-6210](https://nvd.nist.gov/vuln/detail/CVE-2026-6210) in qtsvg

### qtbase
* ee98fb90e60 Run valid tests specified on a command-line, even if mixed
with invalid<br>
When non-existent functions are given on a test's command-line, or a
function is paired with a non-existent data-tag, QtTest previously only
reported these invalid arguments. It now also runs the tests for any
valid arguments they were mixed with.

* 75bef94c41c QVariant: fix comparison of unsigned enums to integers<br>
Fixed a bug that caused compare() to return wrong results when
comparing an unsigned enumerator to an integer.

* 2382f3f65bf QAtomicPointer: add missing docs for 3-arg overload<br>
Documented new overloads of testAndSet() that were originally added for
5.3.

* ae86e48b425 QDoubleSpinBox: fix rounding errors<br>
The calculated value after stepping up/down is now rounded to avoid
discrepancies between the displayed and internal value.

* b913cfdb541 Update Freetype to 2.14.2<br>
Updated bundled Freetype to 2.14.2.

* 44c842612e0 Upgrade Harfbuzz to 13.0.0<br>
Upgraded Harfbuzz to version 13.0.0.

* be168cf3466 Do not persist unicode error state across dirents<br>
Fixed a bug on Unix systems that caused a file name that failed to
decode as UTF-8 to cause decoding errors in other file names. This also
affected QDirIterator and QDir.

* b4f85ee31ec SQLite: Update SQLite to v3.52.0<br>
Updated SQLite to v3.52.0

* d06e2f845d4 SQLite: Update SQLite to v3.51.3<br>
Updated SQLite to v3.51.3, 3.52.0 was withdrawn.

* 3bd5495bbc0 QVarLengthArray: fix memleak in move-assignment<br>
Fixed a memory leak in the move-assignment operator.

* ae239d0f655 windeployqt: Skip system libraries during deployment<br>
windeplyqt now skips Qt dependencies originating from %SystemRoot%

* a7b56f4263d Update bundled libpng to version 1.6.56<br>
libpng was updated to version 1.6.56

* b3c463c8d70 Update bundled libjpeg-turbo to version 3.1.4<br>
libjpeg-turbo was updated to version 3.1.4

* 6dc4d66acce Upgrade Harfbuzz to 13.2.1<br>
Upgraded Harfbuzz to version 13.2.1.

* fddd9e9f942 Update Freetype to 2.14.3<br>
Updated bundled Freetype to 2.14.3.

* 8b54513cdcf QDBusMetaObject: ensure custom types are normalized<br>
Fixed a bug that would cause the tool to crash on exit when querying
remote objects containing complex arguments.

* 185cab53a38 QSharedMemory/POSIX: remove use of O_CLOEXEC<br>
Fixed a bug that caused this class to fail to create() or attach() to
POSIX shared memory segments on macOS 26. The issue did not affect
System V segments.

* 5b40e50f1b3 QObject: mark QMetaObject::Connection::d_ptr temporarily
mutable<br>
Fixed a source of undefined behavior when a const
QMetaObject::Connection object is passed to disconnect(). If you cannot
upgrade your Qt version, a workaround is to not declare your
QMetaObject::Connection objects as const.

* cc01bf95dd0 QUdpSocket/Win: handle WSAEMSGSIZE with write()<br>
Fixed a bug on Windows to set the DatagramTooLargeError condition when
attempting to send a datagram that is too big when using write(), as
writeDatagram() already did. Note that write() causes the socket to
close on this error; use writeDatagram() to avoid that.

* 14001438b71 QCoreApplication/Darwin: canonicalize the application file
path<br>
Fixed a regression from 6.9 that caused applicationFilePath() to return
absolute but not canonical paths on Apple operating systems. This
affects applications whose executable is symlinked to another location
in the system.

* d9019b527ea QMultiMap: fix remove(key, value) incorrect assumption on
std::multimap<br>
Fixed a bug that caused remove() to fail to find key-value pair passed
as parameters, with some implementations of the Standard Library. This
was observed with libc++ from LLVM 22.

* cd7c72446d8 SQLite: Update SQLite to v3.53.0<br>
Updated SQLite to v3.53.0

* 4f5109d8a4b Update bundled libpng to version 1.6.57<br>
libpng was updated to version 1.6.57

* 7965ffe5695 Update bundled libpng to version 1.6.58<br>
libpng was updated to version 1.6.58

* 8ed875c356c Make QT_NO_SINGLE_ARGUMENT_QHASH_OVERLOAD safer to use<br>
Fixed an issue where defining QT_NO_SINGLE_ARGUMENT_QHASH_OVERLOAD
could, instead of complaining about the missing seed argument of user-
defined qHash() functions, silently call a different qHash() overload
(one that has a seed argument, and whose key type implicitly converts
from the original qHash()'s key type.

* a43dab95d6c Upgrade Harfbuzz to 14.2.0<br>
Upgraded Harfbuzz to version 14.2.0

### qtmultimedia
* 231a3ece7 3rdparty: update to dr_wav v0.14.5<br>
update dr_wav to 0.14.5 due to heap buffer overflow

* 272e02b47 CMake, qt_add_ios_ffmpeg_libraries: Fatal error on incorrect
target<br>
The CMake function 'qt_add_ios_ffmpeg_libraries' now produces a fatal
error if the target argument is not an executable. This change was made
to prevent incorrect usage of the function.

* 4d992dd74 WMF: Fix video preview not showing first frame when paused
before load<br>
Fixed video preview not showing first frame when pause() is called
before media loads. The WMF backend now behaves consistently with the
FFmpeg backend.

### qttools
* 2866cfd42 QDoc: Make recognized code languages configurable<br>
The programming languages that QDoc accepts in code blocks has been
made configurable, allowing code that will be marked up using online
tools to be included in documentation without warnings.

### qt3d
* cafe5f849 Update Assimp<br>
Updated Assimp to 6.0.4

### qtserialbus
* 4e62afc7 PeakCAN: Fix error string with trailing null bytes<br>
Fixed that the error string returned by systemErrorString() contained
trailing null bytes.

* 58c45b69 VectorCAN: Fix receiving echo frames with CAN-FD<br>
Fixed that no echo frames were received when both
QCanBusDevice::CanFdKey and QCanBusDevice::ReceiveOwnKey were set to
true.

### qtquick3d
* f700fb695 Update TinyEXR to v1.0.13<br>
Updated TinyEXR to v1.0.13

### qt5compat
* 9b00920 QTextCodec: avoid read-past-buffer in codecForName()<br>
Fixed an out-of-bounds read in codecForName(). which could read past
the end of the QByteArray argument if the argument was created
fromRawData() with no NUL-termination.


Fixes
-----

### qtbase
* [QTBUG-132695](https://qt-project.atlassian.net/browse/QTBUG-132695) Crash in QGuiApplication::applicationStateChanged() when
quitting app
* [QTBUG-143204](https://qt-project.atlassian.net/browse/QTBUG-143204) Android GUI application crashes at the moment of
terminating
* [QTBUG-143562](https://qt-project.atlassian.net/browse/QTBUG-143562) Assertion failure in
QSortFilterProxyModel::mapFromSource() after upgrading from Qt 6.8.3 to
Qt 6.8.6
* [QTBUG-144202](https://qt-project.atlassian.net/browse/QTBUG-144202) QTabBar/QTabWidget tab's close button is not animated
when the tab snaps to new position
* [QTBUG-144015](https://qt-project.atlassian.net/browse/QTBUG-144015) After attempting to change the color in the backlight
settings, the application crashes and produces a core dump.
* [QTBUG-144444](https://qt-project.atlassian.net/browse/QTBUG-144444) Metal API validation: failed assertion `Depth Clip Mode
is not supported on this device' on iOS Simulator
* [QTBUG-133404](https://qt-project.atlassian.net/browse/QTBUG-133404) Visual aliasing glitches when using scale other than
100% in Windows
* [QTBUG-141613](https://qt-project.atlassian.net/browse/QTBUG-141613) I18N_SOURCE_LANGUAGE does not change
CFBundleDevelopmentRegion
* [QTBUG-144266](https://qt-project.atlassian.net/browse/QTBUG-144266) On Windows platform, visual artifacts remain on the
screen when moving a widget window within the main application window.
* [QTBUG-144450](https://qt-project.atlassian.net/browse/QTBUG-144450) CMake spams output with "Line 'QT_LINT_EXAMPLES=ON' does
not match regex."
* [QTBUG-144526](https://qt-project.atlassian.net/browse/QTBUG-144526) QFontInfo does not return weight or style on Windows
* [QTBUG-144485](https://qt-project.atlassian.net/browse/QTBUG-144485) Visual Studio 2026 / MSVC2026 header check failed:
qrangemodel.h
* [QTBUG-131671](https://qt-project.atlassian.net/browse/QTBUG-131671) On iOS, CTR, ALT, SHIFT and COMMAND keys are not
detected
* [QTBUG-143969](https://qt-project.atlassian.net/browse/QTBUG-143969) Cannot select text in subwindow on Android
* [QTBUG-136011](https://qt-project.atlassian.net/browse/QTBUG-136011) Floating QDockWidget cannot be dragged on Wayland
* [QTBUG-20544](https://qt-project.atlassian.net/browse/QTBUG-20544) QDoubleSpinBox incorrectly shows -0.0 after small
increments
* [QTBUG-114414](https://qt-project.atlassian.net/browse/QTBUG-114414) QDoubleSpinbox::valueChanged not emitted after step
* [QTBUG-144521](https://qt-project.atlassian.net/browse/QTBUG-144521) QDoubleSpinBox does not display specialValueText() when
stepping to minimum
* [QTBUG-144549](https://qt-project.atlassian.net/browse/QTBUG-144549) When using QGraphicsGridLayout on Wayland, grid is
misaligned when rendered through QPicture
* [QTBUG-115172](https://qt-project.atlassian.net/browse/QTBUG-115172) [reg 6.3.2 -> 6.5.1] TextEdit wrong wrapping with
wrapMode: TextEdit.Wrap in some cases
* [QTBUG-144166](https://qt-project.atlassian.net/browse/QTBUG-144166) Qt 6.10.2 QMake debug builds cause warning of 16 KB
error
* [QTBUG-143663](https://qt-project.atlassian.net/browse/QTBUG-143663) Incorrect positioning of child windows
* [QTBUG-144805](https://qt-project.atlassian.net/browse/QTBUG-144805) [Qt 6.10.2 -> 6.10.3] Regression? Unexpected hover
effect on QScrollBar groove
* [QTBUG-126009](https://qt-project.atlassian.net/browse/QTBUG-126009) Fusion style: QFrame::StyledPanel with wrong offset in
High DPI scaling
* [QTBUG-142576](https://qt-project.atlassian.net/browse/QTBUG-142576) wasm: setting QT_WASM_SOURCE_MAP_BASE does not work for
app
* [QTBUG-144807](https://qt-project.atlassian.net/browse/QTBUG-144807) FTBFS: CMake on Windows fails with "CMake Error: File
/app.exe.manifest.in does not exist."
* [QTBUG-144862](https://qt-project.atlassian.net/browse/QTBUG-144862) Qt applications emit errors on exit: QThreadStorage:
entry 8 destroyed before end of thread
* [QTBUG-144845](https://qt-project.atlassian.net/browse/QTBUG-144845) QFileDialog::getOpenFileName(...) does not handle file
dialog cancel
* [QTBUG-144622](https://qt-project.atlassian.net/browse/QTBUG-144622) The Size of QToolButton with popup menu is too large
* [QTBUG-144777](https://qt-project.atlassian.net/browse/QTBUG-144777) [REG: 6.7.3 -> 6.8.0] Application hanging with focus
event bouncing between windows in end-less loop
* [QTBUG-136165](https://qt-project.atlassian.net/browse/QTBUG-136165) OBS Studio flashing/hanging due to changed window focus
behavior
* [QTBUG-142913](https://qt-project.atlassian.net/browse/QTBUG-142913) QFileDialog prematurely stops listing directory contents
when it encounters invalid unicode in a filename.
* [QTBUG-144736](https://qt-project.atlassian.net/browse/QTBUG-144736) Addressbook example freezes on QNX
* [QTBUG-144216](https://qt-project.atlassian.net/browse/QTBUG-144216) REG: Qt 6.9.3 -> 6.10.2 -qt-list-indent remains in
effect after list
* [QTBUG-143122](https://qt-project.atlassian.net/browse/QTBUG-143122) Paragraph &lt;p&gt; is not indented in list item &lt;li&gt; when
-qt-list-indent is zero
* [QTBUG-142087](https://qt-project.atlassian.net/browse/QTBUG-142087) SVGs in rich-text (HTML) QTooltips not rendered smoothly
at all device pixel ratios (Windows)
* [QTBUG-143114](https://qt-project.atlassian.net/browse/QTBUG-143114) Reg->6.10: QLineEdit placeholder text no longer showing
(light themes)
* [QTBUG-140684](https://qt-project.atlassian.net/browse/QTBUG-140684) Top flaky test: tst_QWindow::eventOrderOnShow
* [QTBUG-145004](https://qt-project.atlassian.net/browse/QTBUG-145004) QVarLengthArray::operator=(QVarLengthArray&&) leaks heap
buffer when both sides use heap storage
* [QTBUG-144790](https://qt-project.atlassian.net/browse/QTBUG-144790) "C" linkage warning on Clang 21 builds of tst_qvariant
* [QTBUG-115751](https://qt-project.atlassian.net/browse/QTBUG-115751) Odd Qt warning: "Unable to open monitor interface to
\\\\.\\DISPLAY1:" "The operation completed successfully."
* [QTBUG-133050](https://qt-project.atlassian.net/browse/QTBUG-133050) Run the Qt application with the interface, turn off the
monitor, and then report an error when turning on the monitor
* [QTBUG-144931](https://qt-project.atlassian.net/browse/QTBUG-144931) QTransposeProxyModel uses QList<Connection>; check
whether it can use std::array<Connection, MaxPossible>
* [QTBUG-144930](https://qt-project.atlassian.net/browse/QTBUG-144930) QIdentityProxyModel uses QVLA<Connection> when it could
use std::array<>
* [QTBUG-143754](https://qt-project.atlassian.net/browse/QTBUG-143754) QMainWindowLayout is leaking a
QDockWidgetGroupWindowItem when two floating dock widgets are hovering
over each other.
* [QTBUG-142080](https://qt-project.atlassian.net/browse/QTBUG-142080) Qtbase build fails with MinGW-W64 update to 15.1.0 /
12.0.0
* [QTBUG-140473](https://qt-project.atlassian.net/browse/QTBUG-140473) Window restored from the taskbar appears on the wrong
screen
* [QTBUG-145009](https://qt-project.atlassian.net/browse/QTBUG-145009) [REG] Blurry inline image in QTextDocument
* [QTBUG-142131](https://qt-project.atlassian.net/browse/QTBUG-142131) ICU lib deploy confusion
* [QTBUG-143252](https://qt-project.atlassian.net/browse/QTBUG-143252) QTabBar::setTabTextColor is ignored in Dark Mode on
macOS
* [QTBUG-144329](https://qt-project.atlassian.net/browse/QTBUG-144329) ASSERT: "value - FP(minimal) > FP(-1)" in
QtQuick.Shapes/QPainterPath
* [QTBUG-143965](https://qt-project.atlassian.net/browse/QTBUG-143965) QLabel::linkHovered signal not emitted when mouse enters
link area via vertical movement
* [QTBUG-121794](https://qt-project.atlassian.net/browse/QTBUG-121794) Undo/redo shortcuts do not work with Hebrew keyboard
layout
* [QTBUG-69288](https://qt-project.atlassian.net/browse/QTBUG-69288) Ctrl+L is not handled as keyboard shortcut on Hebrew
keyboard on Windows
* [QTBUG-145104](https://qt-project.atlassian.net/browse/QTBUG-145104) QWhatsThis::showText will misplace popup at the edge of
secondary monitor
* [QTBUG-145058](https://qt-project.atlassian.net/browse/QTBUG-145058) Frameless window still shows border on Windows 11 (DWM
rounded corners)
* [QTBUG-144944](https://qt-project.atlassian.net/browse/QTBUG-144944) [REG 6.9->6.10] Geometry of embedded Qt widgets in
AppKit goes haywire under Auto Layout
* [QTBUG-145239](https://qt-project.atlassian.net/browse/QTBUG-145239) qyieldcpu.h fails to compile on dev with macOS 26.4 SDK
on Apple Silicon
* [QTBUG-145359](https://qt-project.atlassian.net/browse/QTBUG-145359) qdbus command crashes on exit in
QMetaType::unregisterMetaType
* [QTBUG-145008](https://qt-project.atlassian.net/browse/QTBUG-145008) wasm: eventloop/main_exec manual test crash
* [QTBUG-145403](https://qt-project.atlassian.net/browse/QTBUG-145403) QToolButton autoraise rendered in Hover sate in windows
11 style
* [QTBUG-140148](https://qt-project.atlassian.net/browse/QTBUG-140148) Windows11Style: adjust the QToolButton geometry
* [QTBUG-143457](https://qt-project.atlassian.net/browse/QTBUG-143457) Warnings in Qtbase with MinGW-W64 update to 15.1.0 /
12.0.0
* [QTBUG-145435](https://qt-project.atlassian.net/browse/QTBUG-145435) qhash.cpp:1400:57 error 'memset' will set 0 bytes
* [QTBUG-144922](https://qt-project.atlassian.net/browse/QTBUG-144922) Turning VSync off in DirectX 11 + 12 no longer works as
intended without setting undocumented env.var.
* [QTBUG-145256](https://qt-project.atlassian.net/browse/QTBUG-145256) QRhiD3D11::endFrame() call swapChainD->swapChain touch
nullptr crash when display driver removed.
* [QTBUG-145358](https://qt-project.atlassian.net/browse/QTBUG-145358) unity build fails - duplicate define openModeToOpenFlags
* [QTBUG-145563](https://qt-project.atlassian.net/browse/QTBUG-145563) Can not configure sql plugins as standalone build
anymore
* [QTBUG-113749](https://qt-project.atlassian.net/browse/QTBUG-113749) QNetworkReply stops emiting readyRead when using proxy
* [QTBUG-145402](https://qt-project.atlassian.net/browse/QTBUG-145402) QNetworkAccessManager::sendCustomRequest("DELETE", ...)
does not send the body request
* [QTBUG-141547](https://qt-project.atlassian.net/browse/QTBUG-141547) UIC: qclass_lib_map.h maps to obsolete class
* [QTBUG-139109](https://qt-project.atlassian.net/browse/QTBUG-139109) Creating QQuickWidget on dialog within QDialog::exec()
causes early exit
* [QTBUG-145310](https://qt-project.atlassian.net/browse/QTBUG-145310) QFontEngineFT::loadGlyph crashes with SIGSEGV when
FT_Render_Glyph returns FT_Err_Invalid_Pixel_Size
* [QTBUG-136786](https://qt-project.atlassian.net/browse/QTBUG-136786) [REG] Textrendering, Windows: Fonts looking too bold in
DirectWrite mode
* [QTBUG-130131](https://qt-project.atlassian.net/browse/QTBUG-130131) windeployqt warnings
* [QTBUG-145731](https://qt-project.atlassian.net/browse/QTBUG-145731) QFontMetrics integer rounding causes 1px positioning
error for AlignBaseline inline objects
* [QTBUG-143608](https://qt-project.atlassian.net/browse/QTBUG-143608) QTableView/QTableWidget: scrolling issues when moving a
row/column header section outside the viewport
* [QTBUG-145206](https://qt-project.atlassian.net/browse/QTBUG-145206) QTreeView: auto-scroll does not stop when mouse button
released outside viewport
* [QTBUG-145422](https://qt-project.atlassian.net/browse/QTBUG-145422) QSharedMemory fails on macOS 26.4
* [QTBUG-141450](https://qt-project.atlassian.net/browse/QTBUG-141450) Qt 6.10 QML WebView denying focus to other elements even
when invisible
* [QTBUG-145393](https://qt-project.atlassian.net/browse/QTBUG-145393) eglSwapBuffers() is called on every touch move event on
an empty Window {} in Qt Quick on QNX
* [QTBUG-140898](https://qt-project.atlassian.net/browse/QTBUG-140898) [REG 6.9.1->6.9.2] Wrong menu icons size with Windows
Vista style
* [QTBUG-144978](https://qt-project.atlassian.net/browse/QTBUG-144978) QUrlQuery::addQueryItem documentation needs improvement
* [QTBUG-145787](https://qt-project.atlassian.net/browse/QTBUG-145787) QCoreApplication::applicationDirPath() no longer
supports symlinks
* [QTBUG-145378](https://qt-project.atlassian.net/browse/QTBUG-145378) Qt 6.11.0 cannot be built on Linux with OpenGL disabled
* [QTBUG-140172](https://qt-project.atlassian.net/browse/QTBUG-140172) [qtbase] Build failure in wayland plugin with -no-opengl
* [QTBUG-145222](https://qt-project.atlassian.net/browse/QTBUG-145222) QTaggedIterator<QTaggedIterator<QSequentialIterator,
void>, std::random_access_iterator_tag>' does not provide a subscript
operator
* [QTBUG-142757](https://qt-project.atlassian.net/browse/QTBUG-142757) QToolBar expansion button color does not update when the
Appearance setting is changed
* [QTBUG-124617](https://qt-project.atlassian.net/browse/QTBUG-124617) AUTOINCREMENT column is not auto-incremented when being
modified by QSqlTableModel
* [QTBUG-133220](https://qt-project.atlassian.net/browse/QTBUG-133220) [Reg 6.8->6.9.0] Stylesheet on QPushButton makes spacing
smaller
* [QTBUG-145621](https://qt-project.atlassian.net/browse/QTBUG-145621) QMultiMap::remove(key, value) fails to remove entry
* [QTBUG-145810](https://qt-project.atlassian.net/browse/QTBUG-145810) QWizard: The bottom border line above the Next/Cancel
buttons flickers when resizing while using the "windowsvista" style at
150% DPI scaling.
* [QTBUG-142797](https://qt-project.atlassian.net/browse/QTBUG-142797) QMainWindow: inconsistent behavior when saving and
restoring geometry with dock widgets
* [QTBUG-145874](https://qt-project.atlassian.net/browse/QTBUG-145874) _qt_internal_plugin_file_path_match() is called with
wrong parameter in Qt6CoreDeploySupport.cmake
* [QTBUG-117731](https://qt-project.atlassian.net/browse/QTBUG-117731) CMake deploy api and QtMultimedia backend
* [QTBUG-136758](https://qt-project.atlassian.net/browse/QTBUG-136758) [Reg 6.8->6.9] iOS NFC dialog stops QML/UI execution
* [QTBUG-132314](https://qt-project.atlassian.net/browse/QTBUG-132314) GPU driver crash in iOS 18
* [QTBUG-140491](https://qt-project.atlassian.net/browse/QTBUG-140491) [Reg 6.5.3->6.5.5] QMessageBox subclass loses its native
look on iOS devices
* [QTBUG-143779](https://qt-project.atlassian.net/browse/QTBUG-143779) [REG 6.2.13 -> 6.5.1][macOS] OpenGL backend with custom
surface format crashes QQuickWidget when resizing
* [QTBUG-142745](https://qt-project.atlassian.net/browse/QTBUG-142745) [REG: 5->6] Large page size without margins doesn't work
anymore
* [QTBUG-145813](https://qt-project.atlassian.net/browse/QTBUG-145813) windeployqt ignores skip plugin options if verbose level
is 0
* [QTBUG-140413](https://qt-project.atlassian.net/browse/QTBUG-140413) heap-use-after-free when using a QSslCertificate in a
static QCoreApplication
* [QTBUG-145857](https://qt-project.atlassian.net/browse/QTBUG-145857) REG: Several new debugger panes not present in the
context menu
* [QTBUG-145849](https://qt-project.atlassian.net/browse/QTBUG-145849) iOS: Accessibility issues with CheckBox
* [QTBUG-142807](https://qt-project.atlassian.net/browse/QTBUG-142807) Discrepancy between platforms with queued one-to-many
connections with processEvents()
* [QTBUG-143485](https://qt-project.atlassian.net/browse/QTBUG-143485) [Reg 6.9.3 -> 6.10.1][Apple Pencil] Scrolling/dragging
gets cancelled when Apple Pencil's "Hover" mode is enabled
* [QTBUG-139006](https://qt-project.atlassian.net/browse/QTBUG-139006) QtMainLoopThread crashes on x86_64 android emulator due
to graphics backend initialization fail
* [QTBUG-145771](https://qt-project.atlassian.net/browse/QTBUG-145771) QOpenGLContext::makeCurrent() leaves stale
GL_INVALID_ENUM on shared context (macOS, Core Profile)
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.
* [QTBUG-145904](https://qt-project.atlassian.net/browse/QTBUG-145904) QAbstractItemView::inputMethodQuery() returns
inconsistent coordinate system for ImCursorRectangle
* [QTBUG-130754](https://qt-project.atlassian.net/browse/QTBUG-130754) [Windows] Issues with keyboard focus when embedding
window
* [QTBUG-145776](https://qt-project.atlassian.net/browse/QTBUG-145776) On some widgets, must set both background role and
Button role to set background
* [QTBUG-145799](https://qt-project.atlassian.net/browse/QTBUG-145799) qmlpreview doesn't work with loadFromModule()
* [QTBUG-145468](https://qt-project.atlassian.net/browse/QTBUG-145468) QDBusContext::setDelayedReply(true) doesn't work for
property getters
* [QTBUG-138914](https://qt-project.atlassian.net/browse/QTBUG-138914) Top flaky test: tst_QWidget::synthMouseDoubleClick
* [QTBUG-142100](https://qt-project.atlassian.net/browse/QTBUG-142100) the Timers doc page needs a bit more work
* [QTBUG-144914](https://qt-project.atlassian.net/browse/QTBUG-144914) Reg [6.5-6.8]/macOS: QMenu submenu arrow grows when
padding is set with non-native style
* [QTBUG-145853](https://qt-project.atlassian.net/browse/QTBUG-145853) [qtbase] Wayland plugin build fails with -no-feature-egl
* [QTBUG-144939](https://qt-project.atlassian.net/browse/QTBUG-144939) Scissor rectangle stays set with some rhi backends after
resetClipping()
* [QTBUG-141405](https://qt-project.atlassian.net/browse/QTBUG-141405) QSystemTrayIcon::showMessage doesn't show custom icon in
KDE
* [QTBUG-109152](https://qt-project.atlassian.net/browse/QTBUG-109152) QOpenGLContext::getProcAdress is not guaranteed to
return nullptr on all platforms
* [QTBUG-146145](https://qt-project.atlassian.net/browse/QTBUG-146145) [REG 6.11.0->6.11.1] can not compile examples with qmake
on Android armv7 and x86 targets
* [QTBUG-146636](https://qt-project.atlassian.net/browse/QTBUG-146636) [REG 6.11.0->6.11.1] Dragging QQuickWidget or
QWebEngineView on top of OpenGL Widget crashes Qt Widget Designer on
Windows
* [QTBUG-145383](https://qt-project.atlassian.net/browse/QTBUG-145383) crash when two QQuickWidget instances are initialized
before show
* [QTBUG-146574](https://qt-project.atlassian.net/browse/QTBUG-146574) QMainWindow does not show all dock widgets in Projects
mode ("projects mode" lacks kit selection / projects settings)
* [QTBUG-143440](https://qt-project.atlassian.net/browse/QTBUG-143440) testlib crashes when encountering unknown test function
passed on command line
* [QTBUG-135968](https://qt-project.atlassian.net/browse/QTBUG-135968) Top flaky test: tst_QFreeList::threadedTest
* [QTBUG-144462](https://qt-project.atlassian.net/browse/QTBUG-144462) AnnouncementPoliteness not respected on iOS
* [QTBUG-143054](https://qt-project.atlassian.net/browse/QTBUG-143054) meta-qt6 should support reproduce build
* [QTBUG-144257](https://qt-project.atlassian.net/browse/QTBUG-144257) Significant memory usage increase after upgrading from
Qt 6.6.1 to Qt 6.10.1 on Windows (10/11) and macOS
* [QTBUG-117832](https://qt-project.atlassian.net/browse/QTBUG-117832) Qt-6.5 + iOS + QFileDialog::getOpenFileUrl(), unable to
read file content
* [QTBUG-144825](https://qt-project.atlassian.net/browse/QTBUG-144825) qcore_unix_p.h defines lots of names that lack the
Q/qt_/q namespace
* [QTBUG-144929](https://qt-project.atlassian.net/browse/QTBUG-144929) QObject::disconnect(const Connection &) const_cast<>s
its argument
* [QTBUG-116821](https://qt-project.atlassian.net/browse/QTBUG-116821) QNativeIpcKey: UB (inactive union member used)
* [QTBUG-131933](https://qt-project.atlassian.net/browse/QTBUG-131933) std::reverse_iterator<QDomNodeList::It>::operator->
fails on clang c++17
* [QTBUG-101426](https://qt-project.atlassian.net/browse/QTBUG-101426) QMetaObjectBuilder does not properly carry property
flags
* [QTBUG-143245](https://qt-project.atlassian.net/browse/QTBUG-143245) Qt.ImhSensitiveData input method hint forces QWERTY
keyboard for Japanese and Chinese text input
* [QTBUG-144581](https://qt-project.atlassian.net/browse/QTBUG-144581) tst_QAbstractNetworkCache::etag is flaky
* [QTBUG-71947](https://qt-project.atlassian.net/browse/QTBUG-71947) Unsigned C++ enum values are converted to signed when
exported to QML
* [QTBUG-111926](https://qt-project.atlassian.net/browse/QTBUG-111926) QFlags doesn't support large (>  sizeof(int)) enums
* [QTBUG-141837](https://qt-project.atlassian.net/browse/QTBUG-141837) QMenu tooltip not redrawn when moving between disabled
actions, and not shown after hovering enabled submenu
* [QTBUG-142906](https://qt-project.atlassian.net/browse/QTBUG-142906) Moving window across displays stops animations
* [QTBUG-110448](https://qt-project.atlassian.net/browse/QTBUG-110448) Cannot remove window min/max buttons Ubuntu Wayland
* [QTBUG-144492](https://qt-project.atlassian.net/browse/QTBUG-144492) [REG] HTTP/2 timeouts
* [QTBUG-145234](https://qt-project.atlassian.net/browse/QTBUG-145234) Korean text rendered as squares on Windows with Korean
locale settings
* [QTBUG-116986](https://qt-project.atlassian.net/browse/QTBUG-116986) T* and const T* hash to different values
* [QTCREATORBUG-34287](https://qt-project.atlassian.net/browse/QTCREATORBUG-34287) Crash when closing the "Debug Qt Creator > Show
Logs" dialog
* [QTBUG-145565](https://qt-project.atlassian.net/browse/QTBUG-145565) a11y focus frame is in the wrong place when the built-in
keyboard is opened
* [QTBUG-138495](https://qt-project.atlassian.net/browse/QTBUG-138495) QCommonStyle subElementRect HeaderLabel QRect size
* [QTBUG-144565](https://qt-project.atlassian.net/browse/QTBUG-144565) QJsonDocument move ctor and swap() are out-of-line
(should be inline)
* [QTBUG-96974](https://qt-project.atlassian.net/browse/QTBUG-96974) QNetworkInterface::Unknown for all interfaces on Android
11
* [QTBUG-145975](https://qt-project.atlassian.net/browse/QTBUG-145975) tst_selftests fails on QNX 8.0: libc++ newlocale stub
crashes sub-binaries with LC_ALL=en_US.UTF-8
* [QTBUG-143161](https://qt-project.atlassian.net/browse/QTBUG-143161) Keyboard takes full screen on android and there is no
way to hide the extra features

### qtsvg
* [QTBUG-144383](https://qt-project.atlassian.net/browse/QTBUG-144383) [REG 6.10.2 -> 6.11] Incorrect SVG Rendering
* [QTBUG-140827](https://qt-project.atlassian.net/browse/QTBUG-140827) [REG. 6.8.3 -> 6.9.3] SVG rendering broken
* [QTBUG-145372](https://qt-project.atlassian.net/browse/QTBUG-145372) QPainterPath assertion failure in
QSvgPaintEngine::drawPath when path contains CurveToElement
* [QTBUG-145797](https://qt-project.atlassian.net/browse/QTBUG-145797) QSvgGenerator only outputs a single font family

### qtdeclarative
* [QTBUG-137396](https://qt-project.atlassian.net/browse/QTBUG-137396) No documentation for why you shouldn't refer to an id in
the root object from other components
* [QTBUG-144327](https://qt-project.atlassian.net/browse/QTBUG-144327) [REG 6.9 → 6.10] Crash in
QQmlComponentAndAliasResolver<QQmlTypeCompiler>::resolveAliasesInObject
* [QTBUG-144446](https://qt-project.atlassian.net/browse/QTBUG-144446) QtQ4A Kotlin-based examples do not build with Gradle 9
* [QTBUG-144137](https://qt-project.atlassian.net/browse/QTBUG-144137) D3D11 RHI crash with Qt 6.10.x
* [QTBUG-143721](https://qt-project.atlassian.net/browse/QTBUG-143721) Behavior: False warning when targeting multiple grouped
properties
* [QTBUG-143582](https://qt-project.atlassian.net/browse/QTBUG-143582) SearchField.forceActiveFocus() doesn't work
* [QTBUG-143450](https://qt-project.atlassian.net/browse/QTBUG-143450) QML app crash on memory allocation
* [QTBUG-141374](https://qt-project.atlassian.net/browse/QTBUG-141374) QML tools cannot see QAccessibilityHints
* [QTBUG-142723](https://qt-project.atlassian.net/browse/QTBUG-142723) Crash in QQuickWindowPrivate::polishItems
* [QTBUG-105906](https://qt-project.atlassian.net/browse/QTBUG-105906) [Reg 5.15.5->5.15.6] The fix for the QTBUG-89736 causes
a crash
* [QTBUG-72910](https://qt-project.atlassian.net/browse/QTBUG-72910) Running on a dangling pointer, when deleting the
activeFocusItem inside of QQuickItem::updatePolish
* [QTBUG-142151](https://qt-project.atlassian.net/browse/QTBUG-142151) qmllint wrong positive with attached property
* [QTBUG-141151](https://qt-project.atlassian.net/browse/QTBUG-141151) SortFilterProxyModel snippet contains wrong syntax
* [QTCREATORBUG-31078](https://qt-project.atlassian.net/browse/QTCREATORBUG-31078) Bogus warning in Qt Creator / TableModel /
Delegate
* [QTBUG-144209](https://qt-project.atlassian.net/browse/QTBUG-144209) "ERROR: AddressSanitizer: stack-use-after-return" in
tst_FlickableInterop::nativeGesturePinchOnFlickableWithParentTapHandler
* [QTBUG-144701](https://qt-project.atlassian.net/browse/QTBUG-144701) [REG 6.10.2 → 6.10.3, 6.11] Valid QML code fails to load
with wrong error about property assignment
* [QTBUG-124476](https://qt-project.atlassian.net/browse/QTBUG-124476) QML alias triggers ASSERT coreIndex >= 0
* [QTBUG-144237](https://qt-project.atlassian.net/browse/QTBUG-144237) textEditingContextMenuUndoRedo:SearchField fails on
Wayland
* [QTBUG-144365](https://qt-project.atlassian.net/browse/QTBUG-144365) textEditingContextMenuUndoRedo:SearchField fails on
ubuntu-22.04-x11-tests
* [QTBUG-142469](https://qt-project.atlassian.net/browse/QTBUG-142469) qmllint: Cannot assign to read-only property data [read-
only-property]
* [QTBUG-144556](https://qt-project.atlassian.net/browse/QTBUG-144556) [REG] QQuickMenu::contentItemChange has an obvious bug
leading to crash in some scenarious
* [QTBUG-144811](https://qt-project.atlassian.net/browse/QTBUG-144811) error: cannot cast 'QQuickColorValueType' to its private
base class 'QColor'
* [QTBUG-144146](https://qt-project.atlassian.net/browse/QTBUG-144146) FluentWinUI3 Combobox background doesn't fit the size.
* [QTBUG-144908](https://qt-project.atlassian.net/browse/QTBUG-144908) Crash at QQuickWidget::setSource, if qml root object is
QtObject
* [QTBUG-139544](https://qt-project.atlassian.net/browse/QTBUG-139544) DelegateChooser doesn't update when DelegateChoice
criteria are modified(TreeView)
* [QTCREATORBUG-34161](https://qt-project.atlassian.net/browse/QTCREATORBUG-34161) Bogus warning when using a signal with an argument
in QML
* [QTBUG-144915](https://qt-project.atlassian.net/browse/QTBUG-144915) error: invalid cast of an rvalue expression of type
'QQuickColorValueType' to type 'QColor&&'
* [QTBUG-144814](https://qt-project.atlassian.net/browse/QTBUG-144814) SearchField accepted signal is not emitted
* [QTBUG-144907](https://qt-project.atlassian.net/browse/QTBUG-144907) Updating path with stroke gradient is broken in Qt Quick
* [QTBUG-144812](https://qt-project.atlassian.net/browse/QTBUG-144812) qmlformat removes comments in object lists
* [QTBUG-123386](https://qt-project.atlassian.net/browse/QTBUG-123386) QmlFormat. Incorrect handling of some comments
* [QTBUG-144917](https://qt-project.atlassian.net/browse/QTBUG-144917) QML Import couldn't be resolved
* [QTBUG-142249](https://qt-project.atlassian.net/browse/QTBUG-142249) FluentWinUI3 BusyIndicator is visible when running is
false
* [QTBUG-144810](https://qt-project.atlassian.net/browse/QTBUG-144810) qmlsc: Runtime crash when Repeater's model is a list of
an inline component
* [QTBUG-144585](https://qt-project.atlassian.net/browse/QTBUG-144585) qmllint/qmlls don't recognize "pragma ValueTypeBehavior:
Assertable"
* [QTBUG-140506](https://qt-project.atlassian.net/browse/QTBUG-140506) qmlformat: Proper indentation after () => {...}
* [QTBUG-144977](https://qt-project.atlassian.net/browse/QTBUG-144977) QQuickTextNodeEngine: AlignBaseline positioning
incorrect for inline objects
* [QTBUG-144933](https://qt-project.atlassian.net/browse/QTBUG-144933) QML-to-C++ compilation produces C4702 (unreachable code)
warnings on MSVC with /W4
* [QTBUG-144999](https://qt-project.atlassian.net/browse/QTBUG-144999) Build Failure with easingCurve Value Type in Direct Mode
* [QTBUG-144691](https://qt-project.atlassian.net/browse/QTBUG-144691) Bogus error "Token '}' expected" when using `interface`
as property name
* [QTBUG-132452](https://qt-project.atlassian.net/browse/QTBUG-132452) qmllint issues
* [QTBUG-144836](https://qt-project.atlassian.net/browse/QTBUG-144836) anchors.centerIn does not vertical align
* [QTBUG-144803](https://qt-project.atlassian.net/browse/QTBUG-144803) Contact List example: List not short edited contact to
alphabetical order
* [QTBUG-145143](https://qt-project.atlassian.net/browse/QTBUG-145143) tst_qtdeclarative_qwasmwindow_harness (Failed)
* [QTBUG-145094](https://qt-project.atlassian.net/browse/QTBUG-145094) Same Game: 'qt.qml.propertyCache.append' runtime
warnings in Qt 6.11.0
* [QTBUG-145112](https://qt-project.atlassian.net/browse/QTBUG-145112)  [Reg 6.10 -> 6.11] qmlls: No code completion or syntax
highlighting for QML Singletons
* [QTBUG-142101](https://qt-project.atlassian.net/browse/QTBUG-142101) FluentWinUI3 TabButton's text is invisible on Ubuntu
* [QTBUG-145434](https://qt-project.atlassian.net/browse/QTBUG-145434) Crash calling function in qmltc generated type
* [QTBUG-143577](https://qt-project.atlassian.net/browse/QTBUG-143577) Documentation of qml font type is in the wrong place
* [QTBUG-131441](https://qt-project.atlassian.net/browse/QTBUG-131441) Qml Text HoverHandler ColumnLayout hover area is not
detected correctly
* [QTBUG-45200](https://qt-project.atlassian.net/browse/QTBUG-45200) Text.StyledText doesn't handle onLinkActivated correctly
* [QTBUG-145074](https://qt-project.atlassian.net/browse/QTBUG-145074) Ambiguous type detected. App 254.0 is defined multiple
times
* [QTBUG-133859](https://qt-project.atlassian.net/browse/QTBUG-133859) tst_QQuickMenu::mousePropagationWithinPopup is flaky
under stress
* [QTBUG-145731](https://qt-project.atlassian.net/browse/QTBUG-145731) QFontMetrics integer rounding causes 1px positioning
error for AlignBaseline inline objects
* [QTBUG-139469](https://qt-project.atlassian.net/browse/QTBUG-139469) SelectedTextColor ignored for &lt;ol&gt; content in TextEdit
* [QTBUG-141870](https://qt-project.atlassian.net/browse/QTBUG-141870) HoverHandler ignores cursorShape parameter
* [QTBUG-145204](https://qt-project.atlassian.net/browse/QTBUG-145204) Crash in QQuickTableViewPrivate::dataChangedCallback
* [QTBUG-136580](https://qt-project.atlassian.net/browse/QTBUG-136580) [REG 6.5.3 -> 6.8.3] ItemParticle no longer works if
contained in a parent item with enabled: false
* [QTBUG-117923](https://qt-project.atlassian.net/browse/QTBUG-117923) ItemParticle causes constant CPU usage and rerenders
* [QTBUG-145226](https://qt-project.atlassian.net/browse/QTBUG-145226) Binding loop when binding StyleKit ScrollView's
contentWidth to its width
* [QTBUG-135624](https://qt-project.atlassian.net/browse/QTBUG-135624) TextInput doesn't work if contentItem of the Window it
is created in was disabled
* [QTBUG-145070](https://qt-project.atlassian.net/browse/QTBUG-145070) QML ItemSelectionModel::selection does not function as
expected
* [QTBUG-139107](https://qt-project.atlassian.net/browse/QTBUG-139107) Crash in QQuickItem::~QQuickItem
* [QTBUG-143361](https://qt-project.atlassian.net/browse/QTBUG-143361) QML Connections component crashes if creating many
Connections that target the same instance
* [QTBUG-135879](https://qt-project.atlassian.net/browse/QTBUG-135879) TapHandler receives events in the background when a pop-
up window is active when using an active stylus.
* [QTBUG-142700](https://qt-project.atlassian.net/browse/QTBUG-142700) QtQuick: native Tooltip text update causes wrong
placement
* [QTBUG-144583](https://qt-project.atlassian.net/browse/QTBUG-144583) Qt Quick Examples - Drag and Drop, not launching on
Android
* [QTBUG-145611](https://qt-project.atlassian.net/browse/QTBUG-145611) "Go To C++ Definition" does not find file
* [QTBUG-140781](https://qt-project.atlassian.net/browse/QTBUG-140781) Reg 6.9->6.10: Crash with Worker
* [QTBUG-117786](https://qt-project.atlassian.net/browse/QTBUG-117786) QmlCompiler does not recognize a component within itself
* [QTBUG-145826](https://qt-project.atlassian.net/browse/QTBUG-145826) Qt Quick Compiler cannot properly handle conversion from
QJSPrimitiveValue to float
* [QTBUG-145139](https://qt-project.atlassian.net/browse/QTBUG-145139) doc: qmlformat's --group-attributes-together has same
documentation as --normalize
* [QTBUG-98872](https://qt-project.atlassian.net/browse/QTBUG-98872) Modal windows accept mouse / drag events
* [QTBUG-75074](https://qt-project.atlassian.net/browse/QTBUG-75074) Flickable over DragHandler doesn't allow to scroll in the
touch screen
* [QTBUG-126812](https://qt-project.atlassian.net/browse/QTBUG-126812) TapHandler over Flickable blocks interaction with
Flickable by mouse but not by touch
* [QTBUG-143872](https://qt-project.atlassian.net/browse/QTBUG-143872) Quick Text control: Truncated status is not cleared when
text is cleared
* [QTBUG-144447](https://qt-project.atlassian.net/browse/QTBUG-144447) QML InputMethod documentation doesn't show properties
etc
* [QTBUG-145762](https://qt-project.atlassian.net/browse/QTBUG-145762) rendercontrol_opengl example creates new textures
infinitely
* [QTBUG-141127](https://qt-project.atlassian.net/browse/QTBUG-141127) Differentiate a QtQbject, i.e. a C++ QObject, and a JS
object
* [QTBUG-144331](https://qt-project.atlassian.net/browse/QTBUG-144331) iOS: Crash when destroying Controls.Control with
VoiceOver enabled
* [QTBUG-145896](https://qt-project.atlassian.net/browse/QTBUG-145896) FAIL!  : declarative_ui::MapItems::test_items_on_map()
Compared values are not the same
* [QTBUG-145740](https://qt-project.atlassian.net/browse/QTBUG-145740) A frame appears when double-clicking a menu bar item
while using the FluentWinUI3 style.
* [QTBUG-145897](https://qt-project.atlassian.net/browse/QTBUG-145897) error: unknown type name 'QtObject'; did you mean
'QObject'?
* [QTBUG-138207](https://qt-project.atlassian.net/browse/QTBUG-138207) Releasing QQuickItemGrabResult before ready signal was
sent can lead to crashes
* [QTBUG-140138](https://qt-project.atlassian.net/browse/QTBUG-140138) qmllint doesn't understand object list bindings to
attached and grouped properties
* [QTBUG-90451](https://qt-project.atlassian.net/browse/QTBUG-90451) ShapePath.closed returns true when empty
* [QTBUG-145016](https://qt-project.atlassian.net/browse/QTBUG-145016) QAbstractItemModel::data: Returning invalid QVariant
breaks "required property string" binding
* [QTBUG-142933](https://qt-project.atlassian.net/browse/QTBUG-142933) Layout.fillWidth does not work correctly with the Text
element.
* [QTBUG-145981](https://qt-project.atlassian.net/browse/QTBUG-145981) error: use of undeclared identifier
'QQuickFontValueType'
* [QTBUG-138101](https://qt-project.atlassian.net/browse/QTBUG-138101) QQC2 Dialog inside QQuickWidget has broken keyboard
navigation
* [QTBUG-144241](https://qt-project.atlassian.net/browse/QTBUG-144241) SearchField text reset / binding loop when currentIndex
stays -1
* [QTBUG-116650](https://qt-project.atlassian.net/browse/QTBUG-116650) TableView rebuilds the entire table when a single row is
added/removed
* [QTBUG-134741](https://qt-project.atlassian.net/browse/QTBUG-134741) Redundant TableView updates.
* [QTBUG-131777](https://qt-project.atlassian.net/browse/QTBUG-131777) Required properties enforcement in qmltc is broken
* [QTBUG-144451](https://qt-project.atlassian.net/browse/QTBUG-144451) QDoc: \include snippet matching uses substring instead
of exact name
* [QTBUG-143978](https://qt-project.atlassian.net/browse/QTBUG-143978) [REG 6.8.3 - 6.10.1] Sporadic crashes at
QQuickBasicTheme::initialize()
* [QTBUG-
144397](https://qt-project.atlassian.net/browse/QTBUG-144397) tst_qquickstyle::defaultPaletteIsUpdatedWhenChangingColorScheme()
crashes on Ubuntu
* [QTBUG-143245](https://qt-project.atlassian.net/browse/QTBUG-143245) Qt.ImhSensitiveData input method hint forces QWERTY
keyboard for Japanese and Chinese text input
* [QTBUG-141251](https://qt-project.atlassian.net/browse/QTBUG-141251) TextInput and Text vertical alignment does not match
when using multiple fonts
* [QTBUG-115140](https://qt-project.atlassian.net/browse/QTBUG-115140) qtdeclarative -unity-build-batch-size 100000 fails
* [QTBUG-145062](https://qt-project.atlassian.net/browse/QTBUG-145062) qmlls 6.11: lots of import path warnings on project
created with qt creator's wizard
* [QTBUG-145131](https://qt-project.atlassian.net/browse/QTBUG-145131) Slowness while waiting for popups to close on macOS
* [QTBUG-144929](https://qt-project.atlassian.net/browse/QTBUG-144929) QObject::disconnect(const Connection &) const_cast<>s
its argument
* [QTBUG-142021](https://qt-project.atlassian.net/browse/QTBUG-142021) Child of FlexboxLayout with fillX is misaligned on
primary axis
* [QTBUG-141055](https://qt-project.atlassian.net/browse/QTBUG-141055) FlexboxLayout incorrectly calculates it's size
* [QTBUG-141514](https://qt-project.atlassian.net/browse/QTBUG-141514) TestCase keyClick/Press/Release should mention they also
can take a string
* [QTBUG-143477](https://qt-project.atlassian.net/browse/QTBUG-143477) Material styled Quick Controls: do not hardcode size and
expose more customizable components
* [QTBUG-131790](https://qt-project.atlassian.net/browse/QTBUG-131790) FileDialog: "arrow up" background overlaps with base
component
* [QTBUG-131786](https://qt-project.atlassian.net/browse/QTBUG-131786) popupType "Popup.Window" propagates events
* [QTBUG-145585](https://qt-project.atlassian.net/browse/QTBUG-145585) `modal: true` does not block input to the parent window
when using `popupType: Popup.Window`
* [QTBUG-141362](https://qt-project.atlassian.net/browse/QTBUG-141362) Popup allows mouse fallthrough regardless of mode
* [QTCREATORBUG-32759](https://qt-project.atlassian.net/browse/QTCREATORBUG-32759) [Reg 14.0.2 -> 16.0.0] Application Output pane no
longer prints stdout/stderr messages when debugging
* [QTBUG-145721](https://qt-project.atlassian.net/browse/QTBUG-145721) qmlls: completions wrong when shadowing
* [QTBUG-141450](https://qt-project.atlassian.net/browse/QTBUG-141450) Qt 6.10 QML WebView denying focus to other elements even
when invisible
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.
* [QTBUG-88646](https://qt-project.atlassian.net/browse/QTBUG-88646) tst_qquicktext::contentSize() failed on msvc2019
developer build in CI

### qtactiveqt
* [QTBUG-144470](https://qt-project.atlassian.net/browse/QTBUG-144470) SBOM: SPDXRef-Package-qtactiveqt-qt-module-ActiveQt
declares wrong license
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtmultimedia
* [QTBUG-144268](https://qt-project.atlassian.net/browse/QTBUG-144268) Incorrect behavior documented for QAudioSink::resume()
and related methods
* [QTBUG-140092](https://qt-project.atlassian.net/browse/QTBUG-140092) GStreamer errors in the multimedia examples on
imx93-11x11-lpddr4x
* [QTBUG-144712](https://qt-project.atlassian.net/browse/QTBUG-144712) pipewire: wrong use of multi-result promises
* [QTBUG-144809](https://qt-project.atlassian.net/browse/QTBUG-144809) assertion failure in tst_QVideoFrame::constructor_create
sFrameWithCorrectFormat_whenCalledWithSupportedImageFormats
* [QTBUG-144842](https://qt-project.atlassian.net/browse/QTBUG-144842) android: heap corruption in tst_multiapp
* [QTBUG-145175](https://qt-project.atlassian.net/browse/QTBUG-145175) MediaPlayer QML app crashes on Linux when playing remote
video: undefined symbol: vaMapBuffer2 in Qt’s libavutil
* [QTBUG-143801](https://qt-project.atlassian.net/browse/QTBUG-143801) GStreamer 1.24+ GST_VIDEO_FORMAT_DMA_DRM GstVideoFormat
not supported.
* [QTBUG-145144](https://qt-project.atlassian.net/browse/QTBUG-145144) CMake: qt_add_ios_ffmpeg_libraries fails when used on
libraries
* [QTBUG-127444](https://qt-project.atlassian.net/browse/QTBUG-127444) QMediaRecorder does not start recording on darwin
backend
* [QTBUG-143062](https://qt-project.atlassian.net/browse/QTBUG-143062) [darwin] Sporadic crashes on QMediaRecorder::record
(recording an audio)
* [QTBUG-123073](https://qt-project.atlassian.net/browse/QTBUG-123073) [macOS] QMediaRecorder failed to record an audio after
reconnecting AirPods
* [QTBUG-109960](https://qt-project.atlassian.net/browse/QTBUG-109960) [WMF] Unable to show video preview (first frame)
* [QTBUG-145590](https://qt-project.atlassian.net/browse/QTBUG-145590) QMediaPlayer with FFmpeg backed doesn't supports HLS
with AES-128 encryption
* [QTBUG-145704](https://qt-project.atlassian.net/browse/QTBUG-145704) [macOS] DeviceDisconnectMonitor crashes when removing an
audio device
* [QTBUG-135951](https://qt-project.atlassian.net/browse/QTBUG-135951) QMediaRecorder captures video at a much worse quality on
Linux
* [QTBUG-144996](https://qt-project.atlassian.net/browse/QTBUG-144996) QtMultiMedia cannot handle RTMP protocol correctly
* [QTBUG-145793](https://qt-project.atlassian.net/browse/QTBUG-145793) QMediaPlayer changes output device sample rate
unexpectedly on MacOS
* [QTBUG-145816](https://qt-project.atlassian.net/browse/QTBUG-145816) [darwin] Sporadic crashes when running
tst_QMediaPlayerBackend in CI
* [QTBUG-145753](https://qt-project.atlassian.net/browse/QTBUG-145753)  Continuously changing eulerRotation through gestures in
a multi-threaded build will cause Tried to spawn a new thread, but the
thread pool is exhausted.
* [QTBUG-144518](https://qt-project.atlassian.net/browse/QTBUG-144518) QQuickSoundEffect has a property whose name is the same
as that of base class property
* [QTBUG-144719](https://qt-project.atlassian.net/browse/QTBUG-144719) msvc2026: compile error at multimedia removed_api.cpp
* [QTBUG-144918](https://qt-project.atlassian.net/browse/QTBUG-144918) [darwin] Sporadic crashes in
MediaToolbox/AudioToolbox/CoreMedia (unknown reason)
* [QTBUG-144711](https://qt-project.atlassian.net/browse/QTBUG-144711) QSoundEffect sporadically triggers a QSocketNotifier
error and loops endlessly
* [QTBUG-128515](https://qt-project.atlassian.net/browse/QTBUG-128515) tst_QScreenCaptureBackend failed on Ubuntu 24.04 GNOME
X11
* [QTBUG-145178](https://qt-project.atlassian.net/browse/QTBUG-145178) FAIL!  :
tst_QMediaPlayerBackend::play_threeMediaPlayers() Compared values are
not the same
* [QTBUG-142694](https://qt-project.atlassian.net/browse/QTBUG-142694) [REG 6.8.3-6.10.1] Sporadic crashes on
QSoundEffectPrivateWithPlayer::play
* [QTBUG-143627](https://qt-project.atlassian.net/browse/QTBUG-143627) Incorrect usage of qFuzzyCompare() abounds in Qt source
[QtMulitmedia]

### qttools
* [QTBUG-144451](https://qt-project.atlassian.net/browse/QTBUG-144451) QDoc: \include snippet matching uses substring instead
of exact name
* [QTBUG-144563](https://qt-project.atlassian.net/browse/QTBUG-144563) Update '\modulestate' example in QDoc manual
* [QTBUG-119307](https://qt-project.atlassian.net/browse/QTBUG-119307) Qdoc table width argument doesn't work
* [QTBUG-145179](https://qt-project.atlassian.net/browse/QTBUG-145179) update_translations target creating duplicate location
entries
* [QTBUG-145230](https://qt-project.atlassian.net/browse/QTBUG-145230) qhelpenginecore.cpp:11:10: fatal error:
'QtConcurrent/qtconcurrentrun.h' file not found
* [QTBUG-145608](https://qt-project.atlassian.net/browse/QTBUG-145608) QDoc: Fix dangling pointers in Clang argument vector
* [QTBUG-145617](https://qt-project.atlassian.net/browse/QTBUG-145617) Regression: Can't set negative minimum on QDoubleSpinBox
in Designer property editor
* [QTBUG-145755](https://qt-project.atlassian.net/browse/QTBUG-145755) qdoc: improve \note in \enum \value block

### qtdoc
* [QTBUG-144477](https://qt-project.atlassian.net/browse/QTBUG-144477) Update list of GPL components in licenses.html
* [QTBUG-142580](https://qt-project.atlassian.net/browse/QTBUG-142580) [REG 6.10.1->6.11.0] car-configurator not launching
* [QTBUG-144835](https://qt-project.atlassian.net/browse/QTBUG-144835) ToyCustomizer: fix 3D rendering on Showcase view
* [QTBUG-144980](https://qt-project.atlassian.net/browse/QTBUG-144980) Car Configurator: CMake warnings about non-existent
target 'Qt6::Quick3DParticles'
* [QTBUG-143980](https://qt-project.atlassian.net/browse/QTBUG-143980) Feature Delivery: Bug fixing and updates.
* [QTBUG-144916](https://qt-project.atlassian.net/browse/QTBUG-144916) Id for object PaginatedResource shadows property
"colors"
* [QTBUG-142732](https://qt-project.atlassian.net/browse/QTBUG-142732) [Reg 6.8.5 -> 6.10.1] FX & Material Showroom demo:
Camera controls no longer work
* [QTBUG-144451](https://qt-project.atlassian.net/browse/QTBUG-144451) QDoc: \include snippet matching uses substring instead
of exact name
* [QTBUG-142730](https://qt-project.atlassian.net/browse/QTBUG-142730) Demos contain orphaned references to unused custom QML
types generated by Qt Design Studio
* [QTBUG-144728](https://qt-project.atlassian.net/browse/QTBUG-144728) QtJenny example won't compile
* [QTBUG-142131](https://qt-project.atlassian.net/browse/QTBUG-142131) ICU lib deploy confusion
* [QTBUG-145099](https://qt-project.atlassian.net/browse/QTBUG-145099) Document new --appx and --appx-certificate arguments of
windeployqt
* [QTBUG-143161](https://qt-project.atlassian.net/browse/QTBUG-143161) Keyboard takes full screen on android and there is no
way to hide the extra features

### qtqa
* [QTBUG-143566](https://qt-project.atlassian.net/browse/QTBUG-143566) RHEL-9.6: tst_Bic::sizesAndVTables(qt:6.10) Test failed

### qtlocation
* [QTBUG-144282](https://qt-project.atlassian.net/browse/QTBUG-144282) Incorrect usage of qFuzzyCompare() abounds in Qt source
[Qt Location]
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtpositioning
* [QTBUG-142752](https://qt-project.atlassian.net/browse/QTBUG-142752) [Android] Keyboard reappears after tab switch when input
field remains focused in Satellite Info example app
* [QTBUG-144952](https://qt-project.atlassian.net/browse/QTBUG-144952) Fix UB in Q{GeoPath,Polygon}Private

### qtconnectivity
* [QTBUG-123430](https://qt-project.atlassian.net/browse/QTBUG-123430) QBluetoothSocket::errorOccured is not emitted in certain
circumstances
* [QTBUG-99701](https://qt-project.atlassian.net/browse/QTBUG-99701) Bluetooth RFComm [Inbound] connection issue with Monterey
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtwayland
* [QTBUG-138907](https://qt-project.atlassian.net/browse/QTBUG-138907) Probable Use after Free on
QtWaylandCompositor::onSurfaceDestroyed
* [QTBUG-144929](https://qt-project.atlassian.net/browse/QTBUG-144929) QObject::disconnect(const Connection &) const_cast<>s
its argument

### qt3d
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtimageformats
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtserialbus
* [QTBUG-145569](https://qt-project.atlassian.net/browse/QTBUG-145569) [PeakCAN] systemErrorString returns trailing null
characters in QCanBusDevice::errorString
* [QTBUG-145556](https://qt-project.atlassian.net/browse/QTBUG-145556) vectorcan - no transmit echo when using CAN-FD
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtserialport
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtwebsockets
* [QTBUG-141396](https://qt-project.atlassian.net/browse/QTBUG-141396) Regarding Qt WebSocket, accessing the IP address and
port via wss fails.
* [QTBUG-63312](https://qt-project.atlassian.net/browse/QTBUG-63312) No timeout in QWebSocketServer/QSslServer during
handshake
* [QTBUG-57026](https://qt-project.atlassian.net/browse/QTBUG-57026) ssl websocketserver stops accepting new connections

### qtwebchannel
* [QTBUG-144929](https://qt-project.atlassian.net/browse/QTBUG-144929) QObject::disconnect(const Connection &) const_cast<>s
its argument

### qtwebengine
* [QTBUG-131640](https://qt-project.atlassian.net/browse/QTBUG-131640) WebEngine not starting on properly when deployed with
specific structure on Windows
* [QTBUG-144270](https://qt-project.atlassian.net/browse/QTBUG-144270) QTWEBENGINE_RESOURCES_PATH does not work on Windows
* [QTBUG-136257](https://qt-project.atlassian.net/browse/QTBUG-136257) QtWebEngine based browser shows nothing with panthor
driver
* [QTBUG-144438](https://qt-project.atlassian.net/browse/QTBUG-144438) Quick: <select> dropdown menus don't receive keyboard
input
* [QTBUG-144824](https://qt-project.atlassian.net/browse/QTBUG-144824) tst_touchinput (Failed)
* [QTBUG-144818](https://qt-project.atlassian.net/browse/QTBUG-144818) [REG 6.9.3 -> 6.11.0-rc] QWebEngineView <select>
dropdown grows indefinitely on non-integer DPI scaling (125%, 150%) on
Windows
* [QTBUG-144608](https://qt-project.atlassian.net/browse/QTBUG-144608) videoplayer example not loading video
* [QTBUG-144595](https://qt-project.atlassian.net/browse/QTBUG-144595) Warning on startup: "Failed to load keymap file, falling
back to StubKeyboardLayoutEngine"
* [QTBUG-142936](https://qt-project.atlassian.net/browse/QTBUG-142936) System openh264 is not used
* [QTBUG-144398](https://qt-project.atlassian.net/browse/QTBUG-144398) Quick Nano Browser: "Open in new window" option doesn't
load page
* [QTBUG-145382](https://qt-project.atlassian.net/browse/QTBUG-145382) [REG 6.10 -> 6.11] QtWebEngine FindRust.cmake conflicts
with Corrosion
* [QTBUG-145188](https://qt-project.atlassian.net/browse/QTBUG-145188) Reported event code in Javascript for numpad enter is
wrong on Windows
* [QTBUG-85661](https://qt-project.atlassian.net/browse/QTBUG-85661) On Windows QtWebEngine, right ctrl/alt sends left
ctrl/alt KeyboardEvent.code
* [QTBUG-135615](https://qt-project.atlassian.net/browse/QTBUG-135615) Version check is needed for libopenjp2
* [QTBUG-141126](https://qt-project.atlassian.net/browse/QTBUG-141126) QPdfView: bounding box of search result highlight covers
part of text.
* [QTBUG-144144](https://qt-project.atlassian.net/browse/QTBUG-144144) QPdfPageSelector allows selecting page n+1 of n total
pages
* [QTBUG-132681](https://qt-project.atlassian.net/browse/QTBUG-132681) [REG 6.7] UB: DocumentPictureInPicture API results in
QWebEngineNewWindowRequest::DestinationType with uninitialized value
* [QTBUG-142806](https://qt-project.atlassian.net/browse/QTBUG-142806) Pdfviewer example highlights wrong part of word if word
contains multiple instances of searched text
* [QTBUG-139689](https://qt-project.atlassian.net/browse/QTBUG-139689) Using Loader for WebEngineView with Devtools causes
crash
* [QTBUG-136619](https://qt-project.atlassian.net/browse/QTBUG-136619) scroll via the scrollbar is not smooth when using
viewing a PDF inside a QWebEngineView
* [QTBUG-145878](https://qt-project.atlassian.net/browse/QTBUG-145878) Scrolling by dragging the thumb of a scrollbar on an
inner div is not working on touchscreens
* [QTBUG-145980](https://qt-project.atlassian.net/browse/QTBUG-145980) QtWebEngine: getUserMedia with chromeMediaSourceId
rejects valid DesktopMediaID strings not registered in
DesktopStreamsRegistry
* [QTBUG-144352](https://qt-project.atlassian.net/browse/QTBUG-144352) Yocto 5.0.8 ARM 64/32bit qtwebengine build error:
vp9_parser
* [QTBUG-144007](https://qt-project.atlassian.net/browse/QTBUG-144007) Yocto 5.0.8 ARM 64/32bit qtwebengine build error:
base_jumbo_19.o
* [QTBUG-141693](https://qt-project.atlassian.net/browse/QTBUG-141693) Upcoming Yocto 5.0.8 bfd linker not fit to link
WebEngine on ci node
* [QTBUG-145054](https://qt-project.atlassian.net/browse/QTBUG-145054) arm32 debug builds no longer possible with 140-based
with yocto 5.0
* [QTBUG-136109](https://qt-project.atlassian.net/browse/QTBUG-136109) Qt WebEngine is very unresponsive when resizing
* [QTBUG-137715](https://qt-project.atlassian.net/browse/QTBUG-137715) Yocto 5.0.8 ARMv7 WebEngine build error:
QWebEngineDownloadRequest::setDownloadDirectory
* [QTBUG-145902](https://qt-project.atlassian.net/browse/QTBUG-145902) [qtwebengine] Crash during Skia/EGL initialization

### qtwebview
* [QTBUG-145858](https://qt-project.atlassian.net/browse/QTBUG-145858) WebView.onUrlChanged event not firing on Android

### qtvirtualkeyboard
* [QTBUG-143749](https://qt-project.atlassian.net/browse/QTBUG-143749) Virtual Keyboard(Greek): "ABC" key label is not
localized to Greek alphabet
* [QTBUG-145711](https://qt-project.atlassian.net/browse/QTBUG-145711) QML tools do not recognize
VirtualKeyboardSettings.visibleFunctionKeys
* [QTBUG-145418](https://qt-project.atlassian.net/browse/QTBUG-145418) When an item in the Selection List on the far right is
highlighted and I use the arrow keys to navigate, the highlighted
position does not match the item's position in the Selection List.
* [QTBUG-145861](https://qt-project.atlassian.net/browse/QTBUG-145861) tst_inputpanelcontrols (failed)

### qtscxml
* [QTBUG-144929](https://qt-project.atlassian.net/browse/QTBUG-144929) QObject::disconnect(const Connection &) const_cast<>s
its argument

### qtspeech
* [QTBUG-138127](https://qt-project.atlassian.net/browse/QTBUG-138127) Top flaky test: tst_QTextToSpeech::synthesize
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtnetworkauth
* [QTBUG-145561](https://qt-project.atlassian.net/browse/QTBUG-145561) OAuth2 fails with Microsoft
* [QTBUG-145705](https://qt-project.atlassian.net/browse/QTBUG-145705) OAuth2 flows shouldn't require id_token when refreshing
tokens
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtquick3d
* [QTBUG-137143](https://qt-project.atlassian.net/browse/QTBUG-137143) RuntimeLoader example fails on Android because assimp
plugin is not deployed
* [QTBUG-144532](https://qt-project.atlassian.net/browse/QTBUG-144532) Misplaced Qt QUIck 3D example on Qt Creator welcome
screen
* [QTBUG-144509](https://qt-project.atlassian.net/browse/QTBUG-144509) [QNX] qtquick3d: scenegrabber_xr baseline test
unconditionally links Qt::Quick3DXrPrivate, breaking configure on
platforms without OpenXR
* [QTBUG-144523](https://qt-project.atlassian.net/browse/QTBUG-144523) [frustumCullingEnabled] The camera cuts off all objects
working through instancing
* [QTBUG-144277](https://qt-project.atlassian.net/browse/QTBUG-144277) DebugView is not update state in underlay renderMode of
View3D
* [QTBUG-144998](https://qt-project.atlassian.net/browse/QTBUG-144998) View3D renderOverrides property is not documented
* [QTBUG-141244](https://qt-project.atlassian.net/browse/QTBUG-141244) Instance Culling for LoD Does Not Offload the GPU
* [QTBUG-142937](https://qt-project.atlassian.net/browse/QTBUG-142937) Failed to compile PrincipledMaterial For Model with
SphereGeometry
* [QTBUG-145137](https://qt-project.atlassian.net/browse/QTBUG-145137) Enums for renderTargetBlend are not usable from QML
* [QTBUG-145057](https://qt-project.atlassian.net/browse/QTBUG-145057) PrincipledMaterial: Crash when enabling Normal Map
display in Debug Mode
* [QTBUG-145056](https://qt-project.atlassian.net/browse/QTBUG-145056) REG: The NORMAL variable is not working to set a normal
map in the CustomMaterial.
* [QTBUG-142477](https://qt-project.atlassian.net/browse/QTBUG-142477) SIGFPE on Intel Mesa Vulkan
* [QTBUG-142175](https://qt-project.atlassian.net/browse/QTBUG-142175) Baking lights for two or more View3Ds in the same
document causes warnings
* [QTBUG-143697](https://qt-project.atlassian.net/browse/QTBUG-143697) CubeMapTexture broken on OpenGL
* [QTBUG-144516](https://qt-project.atlassian.net/browse/QTBUG-144516) Improve the default behavior of qt6_add_materials
* [QTBUG-137996](https://qt-project.atlassian.net/browse/QTBUG-137996) `WrapQuick3DAssimp::WrapQuick3DAssimp` target not found
* [QTBUG-145819](https://qt-project.atlassian.net/browse/QTBUG-145819) Qt Quick 3D on Android: mesh resources collapse
(meshDataSize → 0) after long runtime without sceneGraphInvalidated,
reproducible on both OpenGL and Vulkan (regression from 6.9.0)
* [QTBUG-145753](https://qt-project.atlassian.net/browse/QTBUG-145753)  Continuously changing eulerRotation through gestures in
a multi-threaded build will cause Tried to spawn a new thread, but the
thread pool is exhausted.
* [QTBUG-143048](https://qt-project.atlassian.net/browse/QTBUG-143048) RenderHelpers::rhiRenderRenderable emit warnings per
frame "Texture 0x7d1853005510 () used with different accesses within the
same pass, this is not allowed"
* [QTBUG-145014](https://qt-project.atlassian.net/browse/QTBUG-145014) [Frustum Culling] Shadows disappear when caster is
culled but its shadow remains in view.
* [QTBUG-140820](https://qt-project.atlassian.net/browse/QTBUG-140820) Lancelot lightmap tests failing on Windows
* [QTBUG-143916](https://qt-project.atlassian.net/browse/QTBUG-143916) Fix QDoc warnings for Qt 6.11
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtshadertools
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.
* [QTBUG-145988](https://qt-project.atlassian.net/browse/QTBUG-145988) QtShaderTools: investigate op==/qHash() asymmetries
* [QTBUG-145990](https://qt-project.atlassian.net/browse/QTBUG-145990) QShaderVersion is only qHash-able on INTEGRITY

### qt5compat
* [QTBUG-145180](https://qt-project.atlassian.net/browse/QTBUG-145180) QTextCodec::codecForName() reads past the end of
QByteArray::fromRawData()
* [QTBUG-85227](https://qt-project.atlassian.net/browse/QTBUG-85227) Qt's deprecation warnings are not on by default for MSVC

### qtcoap
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtopcua
* [QTBUG-142475](https://qt-project.atlassian.net/browse/QTBUG-142475) Multiple-Definition Symbol Errors in Qt Build with SSL
and QtOpcUa
* [QTBUG-145171](https://qt-project.atlassian.net/browse/QTBUG-145171) Slew of warnings when building opcua
* [QTBUG-143626](https://qt-project.atlassian.net/browse/QTBUG-143626) Incorrect usage of qFuzzyCompare() abounds in Qt source
[<rest of Qt>]

### qtlanguageserver
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qthttpserver
* [QTBUG-144173](https://qt-project.atlassian.net/browse/QTBUG-144173) QtHttpServer: useSemaphores(SSL) test fails with OpenSSL
3.5.4
* [QTBUG-144929](https://qt-project.atlassian.net/browse/QTBUG-144929) QObject::disconnect(const Connection &) const_cast<>s
its argument

### qtgrpc
* [QTBUG-135074](https://qt-project.atlassian.net/browse/QTBUG-135074) grpc/clientguide example uses built time path
* [QTBUG-144179](https://qt-project.atlassian.net/browse/QTBUG-144179) "ERROR: AddressSanitizer: use-after-poison" in qtgrpc

### qtgraphs
* [QTBUG-144851](https://qt-project.atlassian.net/browse/QTBUG-144851) Resetting pan and zoom in aerospacehub example's bar
graph does not work
* [QTBUG-144872](https://qt-project.atlassian.net/browse/QTBUG-144872) 2D Bar Graphs do not handle diverged stacks with
negative values in same BarSet
* [QTBUG-144579](https://qt-project.atlassian.net/browse/QTBUG-144579) When GraphsView displays multiple series sharing
additional axis the margins are incorrectly calculated
* [QTBUG-145001](https://qt-project.atlassian.net/browse/QTBUG-145001) Crash when axis removed from GraphsView
* [QTBUG-143916](https://qt-project.atlassian.net/browse/QTBUG-143916) Fix QDoc warnings for Qt 6.11

### qttasktree
* [QTBUG-144927](https://qt-project.atlassian.net/browse/QTBUG-144927) TaskTree examples do not show up in Qt Creator welcome
screen
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.

### qtopenapi
* [QTBUG-145097](https://qt-project.atlassian.net/browse/QTBUG-145097) qtopenapi: Replace 'Technical Preview' with 'Technology
Preview'
* [QTBUG-145568](https://qt-project.atlassian.net/browse/QTBUG-145568) [OAS] Nested models should be serialized correctly
* [QTBUG-145410](https://qt-project.atlassian.net/browse/QTBUG-145410) [OAS] CommonLib::fromJsonValue(<ints> &value, const
QJsonValue &jval) should not return "TRUE" in case QJsonValue is not
Integer type
* [QTBUG-145423](https://qt-project.atlassian.net/browse/QTBUG-145423) [OAS] bool CommonLib::fromJsonValue(QString &value,
const QJsonValue &jval) should not convert non string json values to
string
* [QTBUG-145413](https://qt-project.atlassian.net/browse/QTBUG-145413) [OAS] There is no concept of partial validity or auto-
correction in the spec, invalid schema should be dropped
* [QTBUG-145412](https://qt-project.atlassian.net/browse/QTBUG-145412) [OAS] It should be possible to set an empty array to the
model
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtcanvaspainter
* [QTBUG-144859](https://qt-project.atlassian.net/browse/QTBUG-144859) Doc: CanvasPainter duplicates things in TOC
* [QTBUG-142521](https://qt-project.atlassian.net/browse/QTBUG-142521) sbom\qtcanvaspainter-6.11.0.source.spdx file missing
* [QTBUG-144831](https://qt-project.atlassian.net/browse/QTBUG-144831) Path caching not working as expected with certain
settings
* [QTBUG-145406](https://qt-project.atlassian.net/browse/QTBUG-145406) API issue with QCanvasPainterItemRenderer::synchronize()

### qtapplicationmanager (Commercial only)
* [QTBUG-137117](https://qt-project.atlassian.net/browse/QTBUG-137117) applicationmanager\custom-appman not launching on
Windows
* [QTBUG-144122](https://qt-project.atlassian.net/browse/QTBUG-144122) [qtapplicationmanager] do_install_ptest_base fails due
to duplicate copy target race condition in bubblewrap test
* [QTBUG-145392](https://qt-project.atlassian.net/browse/QTBUG-145392) applicationmanager fails yocto/meta-qt6 build
* [QTBUG-129127](https://qt-project.atlassian.net/browse/QTBUG-129127) Fix problems with the new am_package CMake macros

### qtinsighttracker (Commercial only)
* [QTBUG-145073](https://qt-project.atlassian.net/browse/QTBUG-145073) CMake error at tqtc-
qtinsighttracker/src/insighttracker/configure.cmake

Known Issues
------------
* Check that your system meets Qt's requirements:
  https://doc-snapshots.qt.io/qt6-6.11/supported-platforms.html
* RTA reported issues from Qt 6.11
  https://qt-project.atlassian.net/issues?filter=21382
* See Qt 6.11 known issues from:
  https://wiki.qt.io/Qt_6.11_Known_Issues
* Qt 6.11.1 Open issues in Jira:
  https://qt-project.atlassian.net/issues/?filter=22936

Credits for the release goes to:
---------------------------------

Eirik Aavitsland<br>
Cristian Adam<br>
Laszlo Agocs<br>
Dilek Akcay<br>
Dmitrii Akshintsev<br>
Konsta Alajärvi<br>
Stanislav Aleksandrov<br>
Even Oscar Andersen<br>
Dimitrios Apostolou<br>
Xavier BESSON<br>
Mate Barany<br>
Thierry Bastian<br>
Rogelio J. Baucells<br>
Andreas Belke<br>
Vladimir Belyavsky<br>
Nicholas Bennett<br>
Tim Blechmann<br>
Eskil Abrahamsen Blomfeldt<br>
David Boddie<br>
Tatiana Borisova<br>
Joerg Bornemann<br>
Rym Bouabid<br>
Assam Boudjelthia<br>
Aurélien Brooke<br>
Kai Uwe Broulik<br>
Michael Brüning<br>
Eren Bursali<br>
Olivier De Cannière<br>
Alexei Cazacov<br>
Jean-Michaël Celerier<br>
Kaloyan Chehlarski<br>
Wang Chuan<br>
Alexandru Croitor<br>
Mitch Curtis<br>
Giuseppe D'Angelo<br>
Jake Drahos<br>
Artem Dyomin<br>
David Edmundson<br>
Oliver Eftevaag<br>
Christian Ehrlicher<br>
Hatem ElKharashy<br>
Andreas Eliasson<br>
Susumu Endo<br>
Nicolas Fella<br>
Joshua Goins<br>
Robert Griebl<br>
Kaj Grönholm<br>
Nicolas Guichard<br>
Richard Moe Gustavsen<br>
Mikko Hallamaa<br>
Inkamari Harjula<br>
Andre Hartmann<br>
Andreas Hartmetz<br>
Jani Heikkinen<br>
Tero Heikkinen<br>
Moss Heim<br>
Ulf Hermann<br>
Øystein Heskestad<br>
Volker Hilsheimer<br>
Dominik Holland<br>
Mats Honkamaa<br>
Samuli Hölttä<br>
Masoud Jami<br>
Morteza Jamshidi<br>
Allan Sandfeld Jensen<br>
Lau Jespersen<br>
Jonas Karlsson<br>
Igor Khanin<br>
Ali Kianian<br>
Friedemann Kleint<br>
André Klitzing<br>
Michal Klocek<br>
Seokha Ko<br>
Jarek Kobus<br>
Sze Howe Koh<br>
Jarkko Koivikko<br>
Tomi Korpipaa<br>
Fabian Kosmale<br>
Volker Krause<br>
Mike Krus<br>
Anton Kudryavtsev<br>
Santhosh Kumar<br>
Kai Köhne<br>
Cristian Le<br>
Inho Lee<br>
Frédéric Lefebvre<br>
Wladimir Leuschner<br>
Felix Lionardo<br>
David Loki<br>
Robert Löhning<br>
Thiago Macieira<br>
Shveta Mittal<br>
Safiyyah Moosa<br>
Marc Mutz<br>
Antti Määttä<br>
Andy Nichols<br>
Mårten Nordheim<br>
Daniel Nylander<br>
Dennis Oberst<br>
Sukyoung Oh<br>
Kimmo Ollila<br>
Frank Osterfeld<br>
Matti Paaso<br>
Jerome Pasion<br>
Miika Pernu<br>
Yauheni Pervenenka<br>
Evgen Pervenenka<br>
Samuli Piippo<br>
Lauri Pohjanheimo<br>
Joni Poikelin<br>
Gleb Popov<br>
Rami Potinkara<br>
Lorn Potter<br>
Shyamnath Premnadh<br>
Dheerendra Purohit<br>
MohammadHossein Qanbari<br>
Liang Qi<br>
Darshan Ramesh<br>
David Redondo<br>
Topi Reinio<br>
Konstantin Ritt<br>
Shawn Rutledge<br>
Toni Saario<br>
Ahmad Samir<br>
Nick Shaforostov<br>
Sami Shalayel<br>
Eugene Shalygin<br>
Andy Shaw<br>
Venugopal Shivashankar<br>
Nils Petter Skålerud<br>
Ivan Solovev<br>
Axel Spoerl<br>
Ratchanan Srirattanamet<br>
Patrick Stewart<br>
Christian Strømme<br>
Tarja Sundqvist<br>
Lars Sutterud<br>
Tasuku Suzuki<br>
Jan Arve Sæther<br>
Morten Sørvig<br>
Sadegh Taghavi<br>
Patrik Teivonen<br>
Marcus Tillmanns<br>
Elias Toivola<br>
Jere Tuliniemi<br>
Paul Olav Tvete<br>
Tuomas Vaarala<br>
Peter Varga<br>
Doris Verria<br>
Tor Arne Vestbø<br>
Ville Voutilainen<br>
Juha Vuolle<br>
Olli Vuolteenaho<br>
Jannis Völker<br>
Michael Weghorn<br>
Bernd Weimer<br>
Edward Welbourne<br>
Paul Wicking<br>
Piotr Wiercinski<br>
Anna Wojciechowska<br>
Oliver Wolff<br>
Andrei Yankovich<br>
Semih Yavuz<br>
Zhao Yuhang<br>
Vlad Zahorodnii<br>
Yingzhen Zhao<br>
Eike Ziller<br>
Johanna Äijälä<br>
