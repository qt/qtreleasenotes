Release note
============
Qt 6.10.2 release is a patch release made on the top of Qt 6.10.1.
As a patch release, Qt 6.10.2 does not add any new functionality but provides
bug fixes and other improvements and maintains both forward and backward
compatibility (source and binary) with the 6.10.x series.

For detailed information about Qt 6.10, refer to the online documentation
included in this distribution. The documentation is also available online:

https://doc.qt.io/qt-6/index.html

The Qt version 6.10 series is binary compatible with the 6.9.x series.
Applications compiled for 6.9 will continue to run with 6.10.

Some of the changes listed in this file include issue tracking numbers
corresponding to tasks in the Qt Bug Tracker:

https://bugreports.qt.io/

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
* [CVE-2025-14576](https://nvd.nist.gov/vuln/detail/CVE-2025-14576) in qtdeclarative

### qtbase
* 1222b7066f3 SQLite: Update SQLite to v3.51.0
Updated SQLite to v3.51.0

* e4082021f4c macOS: Disable window-modal native message boxes on Tahoe
Window-modal message boxes are no longer backed by native NSAlerts on
Tahoe, due to a bug that prevents the alert from responding to mouse
events for its buttons.

* 6e6f9a214e6 SHA3: Replace git SHA with tag
Replaced version information of 'Secure Hash Algorithm SHA-3' from a
git SHA to a semantic version. The content remained the same though.

* 3c7038fb2d0 wayland: Add color-management-v1 support
New protocol synced from wayland-protocols

* 29d68f23cb0 QRandomGenerator: remove direct use of HW instructions
This class no longer directly uses a hardware random number generator
on x86 systems, even if one is available. Instead, it will always use a
generator provided by the OS (so performance will be OS-specific),
though there should be no meaningful difference in the quality of the
samples generated.

* ac13a19afe4 CMake: Add initial Cyclone DX v1.6 SBOM generation support
A new -sbom-cyclonedx-v1_6 configure option can be used to generate and
install a CycloneDX v1.6 SBOM (Software Bill of Materials) file for each
built Qt repository.

* b6a126ee258 Update CLDR to v48
QLocale now uses v48 of the Unicode Consortium's Common Locale Data
Repository (CLDR).

* 50187e94332 CMake: Add emoji segmenter attribution to SBOM
Emoji Segmenter is now included in the SBOM dependencies of Qt GUI.

* 81416fce22a Upgrade Harfbuzz to 12.2.0
Upgraded Harfbuzz to version 12.2.0.

* 96c9766c04e Update bundled libpng to version 1.6.51
libpng was updated to version 1.6.51

* f3b6d336191 Add missing forwarding for channel signals in QLocalSocket
/ Unix
Fixed QLocalSocket not emitting channelReadyRead() and
channelBytesWritten() signals

* 2b839b350cc SQLite: Update SQLite to v3.51.1
Updated SQLite to v3.51.1

* 6a8067be450 QVectorND: do not assert when deserialization yields NaN
or ±∞
Fixed a bug in the QDataStream operator that could lead to an assertion
failure (program termination) on reading back previously streamed out
objects that contain NaN or infinity values.

* cbba3900679 Update bundled libpng to version 1.6.52
libpng was updated to version 1.6.52

* 1eae7ac88bd Update bundled libpng to version 1.6.53
libpng was updated to version 1.6.53

* 839b93270b4 QFont: fix operator<() pt.2: comparing QMaps
Fixed a Qt 6.7 regression in the stability of the less-than operator.
If you use QFont as keys in a QMap/std::map, or otherwise use QFont
ordering (equality is ok), then we strongly recommend to update.

* c3745d026b6 q23:expected: namespace TL_ macros with Q23_
Fixed potential compile errors in projects that use both the original
tl::expected and Qt private headers.

* a52e4d61b4e Update bundled libjpeg-turbo to version 3.1.3
libjpeg-turbo was updated to version 3.1.3

* c5e8b864239 Upgrade Harfbuzz to 12.3.0
Upgraded Harfbuzz to version 12.3.0.

* bec78b6ff61 Update bundled libpng to version 1.6.54
libpng was updated to version 1.6.54

### qtdeclarative
* af17d8437f Windows style: override the application palette when in
dark mode
The Windows native style will use a light palette as the application
global palette on Windows systems running in dark mode. The style cannot
render dark controls, and mixing a dark application palette with some UI
elements rendered in light mode using the Control style results in
inconsistent and unusable user interfaces. For Dark mode UIs, use a
style that supports dark mode, like the FluentWinUI3 or Fusion styles.

### qttools
* ebc8cf7b3 QDoc: HelpProjectWriter: Process \generatelist when building
a .qhp TOC
The \generatelist command now produces correct output when used in a
\list structure to build a Qt help project (qhp) TOC.

### qtquick3d
* 6503d6256 XR: OpenXR: OpenGL: desktop Linux support
Support desktop OpenGL on Linux

### qt5compat
* 5fc0e48 QLinkedList: fix range-erase() aliasing bug on shared
instances
Fixed a bug in range-erase() that would alter implicitly shared copies
of the list erase() was called on.

### qtgrpc
* 48a99f50 QGrpcHttp2Channel: Implement dataframe decompression
Added missing decompression handling for 'deflate' and 'gzip'.


Fixes
-----

### qtbase
* [QTBUG-141745](https://qt-project.atlassian.net/browse/QTBUG-141745) tst_http2.cpp:732:32: error: incomplete type
'QSslConfiguration'
* [QTBUG-141689](https://qt-project.atlassian.net/browse/QTBUG-141689) Qt6 on macOS Tahoe: Qt::WindowModal disables clicks on
QMessageBox
* [QTBUG-132522](https://qt-project.atlassian.net/browse/QTBUG-132522) Window title bar shrinks to few pixel height if
WindowStaysOnTopHint is toggled.
* [QTBUG-141475](https://qt-project.atlassian.net/browse/QTBUG-141475) Wayland: Warning spew related to QWaylandTextInputv3
under COSMIC
* [QTBUG-139227](https://qt-project.atlassian.net/browse/QTBUG-139227) [Windows] QMenuBar not displayed correctly with QDialog
* [QTBUG-139849](https://qt-project.atlassian.net/browse/QTBUG-139849) Windows11Style: Transparent combobox popups after
changing style from Windows11Style
* [QTBUG-117832](https://qt-project.atlassian.net/browse/QTBUG-117832) Qt-6.5 + iOS + QFileDialog::getOpenFileUrl(), unable to
read file content
* [QTBUG-141819](https://qt-project.atlassian.net/browse/QTBUG-141819) [Reg 6.8.4->6.8.5] Setting background-color in the
StyleSheet causes the QTextEdit border not to render properly with the
Windows 11 style.
* [QTBUG-140361](https://qt-project.atlassian.net/browse/QTBUG-140361) Standard theme menu icons on macOS Tahoe are too large
* [QTBUG-140897](https://qt-project.atlassian.net/browse/QTBUG-140897) [REG:6.8->6.9.3,6.10.0] QML TextField on Android 16
doesn't show keyboard on first tap.
* [QTBUG-141885](https://qt-project.atlassian.net/browse/QTBUG-141885) QRangeModel with tree of gadgets doesn't work
* [QTBUG-141899](https://qt-project.atlassian.net/browse/QTBUG-141899) QList::assign breaks basic exception guarantee
* [QTBUG-141994](https://qt-project.atlassian.net/browse/QTBUG-141994) Static build and disabling deprecated up to 6.6 results
in FTBS
* [QTBUG-141916](https://qt-project.atlassian.net/browse/QTBUG-141916) QSpinBox/QDoubleSpinBox does not factor in up/down
button size
* [QTBUG-133845](https://qt-project.atlassian.net/browse/QTBUG-133845)  QSpinBoxes take too much vertical space if an
application-wide style sheet is set since Qt 6.8.2
* [QTBUG-141895](https://qt-project.atlassian.net/browse/QTBUG-141895) Sorting indicator with windows11 style wrong in position
and direction
* [QTBUG-126345](https://qt-project.atlassian.net/browse/QTBUG-126345) QHeaderView sorting indicator is missing with windows11
style and dark themes
* [QTBUG-124920](https://qt-project.atlassian.net/browse/QTBUG-124920) Menubar press-drag-release gesture doesn't activate menu
items on some compositors
* [QTBUG-105476](https://qt-project.atlassian.net/browse/QTBUG-105476) QColorDialog wrongly exposes pickable region when
translated
* [QTBUG-141942](https://qt-project.atlassian.net/browse/QTBUG-141942) Crash in png lib
* [QTBUG-141918](https://qt-project.atlassian.net/browse/QTBUG-141918) QList asserts during assignment
* [QTBUG-142041](https://qt-project.atlassian.net/browse/QTBUG-142041) Starting a QProcess breaks std::cin (syscall not
restarted after SIGCHLD)
* [QTBUG-138513](https://qt-project.atlassian.net/browse/QTBUG-138513) QTableView setSpan + moveSection causes selection
mismatch
* [QTBUG-142092](https://qt-project.atlassian.net/browse/QTBUG-142092) emoji-segmenter dependency is missing from SBOM
* [QTBUG-142126](https://qt-project.atlassian.net/browse/QTBUG-142126) qt_generate_deploy_app_script deploys wrong architecture
in cross compile for WoA
* [QTBUG-141761](https://qt-project.atlassian.net/browse/QTBUG-141761) Crash when moving a dock of QDockWidget in and out of
the main window
* [QTBUG-138087](https://qt-project.atlassian.net/browse/QTBUG-138087) Qt wasm bug unexpected behaviour virtual keyboard
* [QTBUG-138821](https://qt-project.atlassian.net/browse/QTBUG-138821) Textfields properties not updates on editing at right
moment on mobile browser (Wasm)
* [QTBUG-142083](https://qt-project.atlassian.net/browse/QTBUG-142083) QPushButton icon windows 11 style
* [QTBUG-135381](https://qt-project.atlassian.net/browse/QTBUG-135381) QFileDialog's name filter case sensitivity is not clear
* [QTBUG-141833](https://qt-project.atlassian.net/browse/QTBUG-141833) QPainter::drawTiledPixmap() doesn't handle position
offset with HiDPI correctly
* [QTBUG-141912](https://qt-project.atlassian.net/browse/QTBUG-141912) QPicturePaintEngine crashes when its buffer runs full
* [QTBUG-138568](https://qt-project.atlassian.net/browse/QTBUG-138568) When <!-- %%INSERT_PERMISSIONS -> is removed it writes
nothing
* [QTBUG-140830](https://qt-project.atlassian.net/browse/QTBUG-140830) Settings Qt.ExpandedClientAreaHint in onCompleted
handler has no effect
* [QTBUG-142267](https://qt-project.atlassian.net/browse/QTBUG-142267) CMake configure fails if the target OS is already set to
TRUE
* [QTBUG-139425](https://qt-project.atlassian.net/browse/QTBUG-139425) Wayland: QEventLoop::ExcludeUserInputEvents doesn't work
* [QTBUG-141938](https://qt-project.atlassian.net/browse/QTBUG-141938) Wayland: custom event loop doesn't work since Qt6.10
* [QTBUG-142345](https://qt-project.atlassian.net/browse/QTBUG-142345) QList crashes if underlying malloc() returns 0
* [QTBUG-142182](https://qt-project.atlassian.net/browse/QTBUG-142182) FTBFS: unqualified QRangeModelDetails::wrapped_t uses
break unity-build
* [QTBUG-142184](https://qt-project.atlassian.net/browse/QTBUG-142184) QRangeModel should not refer to its private
implemantation unqualified
* [QTBUG-142336](https://qt-project.atlassian.net/browse/QTBUG-142336) No qtpaths executable found for deployment purposes
* [QTBUG-142324](https://qt-project.atlassian.net/browse/QTBUG-142324) Using client certificate without common name causes
crash (schannel backend)
* [QTBUG-142139](https://qt-project.atlassian.net/browse/QTBUG-142139) Fusion style has incorrect QDockWidget icon filenames
* [QTBUG-142129](https://qt-project.atlassian.net/browse/QTBUG-142129) Windows11Style: Adjust QLineEdit coloring
* [QTBUG-90897](https://qt-project.atlassian.net/browse/QTBUG-90897) Windows/Accessibility: Qt does not report correct focused
widget to screen readers on Windows
* [QTBUG-90899](https://qt-project.atlassian.net/browse/QTBUG-90899) Windows/Accessibility: NVDA sometimes reads out
information twice
* [QTBUG-142431](https://qt-project.atlassian.net/browse/QTBUG-142431) QVectorND QDataStream operators Q_ASSERT(qIsFinite())
instead of setting the stream state
* [QTBUG-140785](https://qt-project.atlassian.net/browse/QTBUG-140785) qt-cmake can't be used to run CMake `--build` or
`--install` modes, due to commandline injection of CMAKE_TOOLCHAIN_FILE
* [QTBUG-137435](https://qt-project.atlassian.net/browse/QTBUG-137435) macos: crash in Cocoa QPA when plugging in an external
screen
* [QTBUG-142400](https://qt-project.atlassian.net/browse/QTBUG-142400) QTreeWidget expand/collapse icons too small for windows
11 style
* [QTBUG-142463](https://qt-project.atlassian.net/browse/QTBUG-142463) state checks in tst_qaccessibility fail in Clang build
on Debian testing
* [QTBUG-141992](https://qt-project.atlassian.net/browse/QTBUG-141992) QMenu::exec returns Null for QWidgetAction , works for
QAction
* [QTBUG-142246](https://qt-project.atlassian.net/browse/QTBUG-142246) [REG 6.6 - 6.7] QFont::op< is no longer a strict weak
ordering, breaking map preconditions
* [QTBUG-141917](https://qt-project.atlassian.net/browse/QTBUG-141917) Severe Leak: User Handles ( Windows "_q_titlebar" won't
get closed )
* [QTBUG-142528](https://qt-project.atlassian.net/browse/QTBUG-142528) macOS: 10bit OpenGL context cannot be created
* [QTBUG-142232](https://qt-project.atlassian.net/browse/QTBUG-142232) q23::expected might break projects that use both Qt and
tl::expected
* [QTBUG-141532](https://qt-project.atlassian.net/browse/QTBUG-141532) configure is looking for waylandscanner even if it is
not needed
* [QTBUG-141579](https://qt-project.atlassian.net/browse/QTBUG-141579) android-9-x86-on-linux: Failed to acquire deadlock
protector for 'QAndroidPlatformOpenGLWindow::eglSurface()' while already
locked by 'QAndroidInputContext::runOnQtThread()'
* [QTBUG-141782](https://qt-project.atlassian.net/browse/QTBUG-141782) Top flaky test: tst_QColorDialog::hexColor
* [QTBUG-141357](https://qt-project.atlassian.net/browse/QTBUG-141357) Top flaky test:
tst_QCompleter::task253125_lineEditCompletion
* [QTBUG-139400](https://qt-project.atlassian.net/browse/QTBUG-139400) Properly manage QtEditText focus and InputConnection
callbacks
* [QTBUG-142460](https://qt-project.atlassian.net/browse/QTBUG-142460) App crashes when switching to other application
* [QTBUG-131650](https://qt-project.atlassian.net/browse/QTBUG-131650) qtwebengine does not compile under sccache, with note
note: please rebuild precompiled header
* [QTBUG-140863](https://qt-project.atlassian.net/browse/QTBUG-140863) Instructions output by qt-cmake-create /
QtInitProject.cmake are wrong
* [QTBUG-64446](https://qt-project.atlassian.net/browse/QTBUG-64446) tst_QWidget::multipleToplevelFocusCheck() on linux
* [QTBUG-84259](https://qt-project.atlassian.net/browse/QTBUG-84259) tst_QWidget::multipleToplevelFocusCheck fails with CentOS
8.1 x64 & SLES 15
* [QTBUG-100686](https://qt-project.atlassian.net/browse/QTBUG-100686) macdeployqt misses some libraries
* [QTBUG-142434](https://qt-project.atlassian.net/browse/QTBUG-142434) QStyleOptionViewItem::viewItemPosition is incorrect
* [QTBUG-140494](https://qt-project.atlassian.net/browse/QTBUG-140494) QAbstractItemView with AStyledItemDelegate and
Windows11Style
* [QTBUG-132882](https://qt-project.atlassian.net/browse/QTBUG-132882) StyleSheet in QHeaderView  Chops off first letter
* [QTBUG-142321](https://qt-project.atlassian.net/browse/QTBUG-142321) Potential Data Race in QReadWriteLock
* [QTBUG-141432](https://qt-project.atlassian.net/browse/QTBUG-141432) memory leak in QCoreApplication::requestPermissionImpl
* [QTBUG-133528](https://qt-project.atlassian.net/browse/QTBUG-133528) QLabel underline for accelerator doesn't update when Alt
is pressed
* [QTBUG-45253](https://qt-project.atlassian.net/browse/QTBUG-45253) [REG 4.X->5.X] Default QPushButton with QMenu loses arrow
with Windows 7 style
* [QTBUG-135333](https://qt-project.atlassian.net/browse/QTBUG-135333) Windows: Transparent frameless window has a frame with
titlebar
* [QTBUG-134701](https://qt-project.atlassian.net/browse/QTBUG-134701) QTableWidget stylesheet stays on headers after removal
* [QTBUG-
34103](https://qt-project.atlassian.net/browse/QTBUG-34103) QCommonStyle::subControlRect(CC_GroupBox,&option,QStyle::SC_GroupB
oxContents,...) gives wrong answer if option.rect.topLeft != (0,0)
* [QTBUG-143122](https://qt-project.atlassian.net/browse/QTBUG-143122) Paragraph &lt;&gt; is not indented in list item &lt;li&gt; when
-qt-list-indent is zero
* [QTBUG-143043](https://qt-project.atlassian.net/browse/QTBUG-143043) RightToLeft QCheckBox gets cropped with Win11 Style
* [QTBUG-140674](https://qt-project.atlassian.net/browse/QTBUG-140674) Crash failing to create eglSurface while UI thread
locked by QtAndroidAccessibility
* [QTBUG-140501](https://qt-project.atlassian.net/browse/QTBUG-140501) QDialog is broken on Android platform
* [QTBUG-102594](https://qt-project.atlassian.net/browse/QTBUG-102594) [REG 5.15.6 -> 5.15.9] Many ANR issues by
QtAccessibility
* [QTBUG-105958](https://qt-project.atlassian.net/browse/QTBUG-105958) [Android] Intent + Talkback leads to deadlock
* [QTBUG-112931](https://qt-project.atlassian.net/browse/QTBUG-112931) Android App crash in QtAndroidAccessibility
* [QTBUG-143175](https://qt-project.atlassian.net/browse/QTBUG-143175) [REG] Extreme freezing since 6.9
* [QTBUG-69423](https://qt-project.atlassian.net/browse/QTBUG-69423) QRandomGenerator not random on certain Windows
installations
* [QTBUG-129193](https://qt-project.atlassian.net/browse/QTBUG-129193) Qt compiled with gcc 13 and -march=bdver4/-mtune=bdver4
causes segfaults in tests, downstream applications
* [QTBUG-141663](https://qt-project.atlassian.net/browse/QTBUG-141663) Missing option to force VSync on VxWorks target
* [QTBUG-141803](https://qt-project.atlassian.net/browse/QTBUG-141803) Qt doesn't help debug "Unknown exception is thrown from
an Qt event handler"
* [QTBUG-131107](https://qt-project.atlassian.net/browse/QTBUG-131107) QVideoFrame::toImage / qImageFromVideoFrame not safe to
call from worker thread
* [QTBUG-141834](https://qt-project.atlassian.net/browse/QTBUG-141834) QNX: windows/widgets not scaled correctly when scale
factor is larger than 1
* [QTBUG-140073](https://qt-project.atlassian.net/browse/QTBUG-140073) Missing symbols in Java files in qtdeclarative
* [QTBUG-141949](https://qt-project.atlassian.net/browse/QTBUG-141949) Update CLDR to v48
* [QTBUG-138759](https://qt-project.atlassian.net/browse/QTBUG-138759) [VxWorks] some vxworks socket errorhandling is missing
from 6.x
* [QTBUG-142185](https://qt-project.atlassian.net/browse/QTBUG-142185) tst_qguieventdispatcher::postEventFromThread is flakey
on macOS 26
* [QTBUG-135049](https://qt-project.atlassian.net/browse/QTBUG-135049)  Connection error: GOAWAY invalid stream/error code (1)
* [QTBUG-139692](https://qt-project.atlassian.net/browse/QTBUG-139692) HTTP request results in NoError error on GOAWAY
* [QTBUG-139986](https://qt-project.atlassian.net/browse/QTBUG-139986) QStateMachine tests aren't running on the CI
* [QTBUG-142157](https://qt-project.atlassian.net/browse/QTBUG-142157) QCursor::pos() doesn't match enter event position
* [QTBUG-140667](https://qt-project.atlassian.net/browse/QTBUG-140667) Undocumented reimplemented public functions in snapshot
builds
* [QTBUG-138246](https://qt-project.atlassian.net/browse/QTBUG-138246) Q{Shared,Weak}Pointer::IfCompatible cause accidental
copy/move SMFs, causing FTBFS in qtdeclarative
* [QTBUG-140786](https://qt-project.atlassian.net/browse/QTBUG-140786) QFuture::cancelChain doesn't set the cancel info to all
chained futures/promises
* [QTBUG-142020](https://qt-project.atlassian.net/browse/QTBUG-142020) Incorrect usage of qFuzzyCompare() abounds in Qt source
[QtCore]
* [QTBUG-120396](https://qt-project.atlassian.net/browse/QTBUG-120396) `QUrl::resolved` gives wrong result when there are more
`..`s in relative reference
* [QTBUG-93625](https://qt-project.atlassian.net/browse/QTBUG-93625) qt_internal_add_test doesn't call qt_import_qml_plugins
* [QTBUG-142473](https://qt-project.atlassian.net/browse/QTBUG-142473) Linear memory growth observed with Qt GRPC during long
run
* [QTBUG-142713](https://qt-project.atlassian.net/browse/QTBUG-142713) SPDX Sbom document namespaces are not unique enough
* [QTBUG-140846](https://qt-project.atlassian.net/browse/QTBUG-140846) tst_Android::safeAreaWithWindowFlagsAndStates(Normal)
fails on Android 16
* [QTBUG-141712](https://qt-project.atlassian.net/browse/QTBUG-141712) tst_Android::testFullScreenDimensions() fails
* [QTBUG-141505](https://qt-project.atlassian.net/browse/QTBUG-141505) AOSP-based Android back gesture causes touch loss in Qt
for WebAssembly apps
* [QTBUG-142551](https://qt-project.atlassian.net/browse/QTBUG-142551) Crash in QRegularExpressionPrivate::optimizePattern()
* [QTBUG-143174](https://qt-project.atlassian.net/browse/QTBUG-143174) [REG 6.8.3-6.10.1] Sporadic crashes on application exit

### qtsvg
* [QTBUG-130140](https://qt-project.atlassian.net/browse/QTBUG-130140) SVG-font handling is unicode-oblivious and violates the
SVG specification
* [QTBUG-137773](https://qt-project.atlassian.net/browse/QTBUG-137773) Incorrect rendering of ligatures from <font> and <glyph>
elements
* [QTBUG-139446](https://qt-project.atlassian.net/browse/QTBUG-139446) Parsing text to font's glyphs happens to late and too
often

### qtdeclarative
* [QTBUG-141229](https://qt-project.atlassian.net/browse/QTBUG-141229) Built-in ScrollBars still visible when customising
ScrollView
* [QTBUG-141704](https://qt-project.atlassian.net/browse/QTBUG-141704) Crash when destroying QQmlPropertyMap
* [QTBUG-141849](https://qt-project.atlassian.net/browse/QTBUG-141849) Property binding generates incorrect JavaScript object
* [QTBUG-141893](https://qt-project.atlassian.net/browse/QTBUG-141893) QtQuick application with space in folder fails to
configure
* [QTBUG-140875](https://qt-project.atlassian.net/browse/QTBUG-140875) QML Text - multi-line text is not always elided
correctly when item is resized
* [QTBUG-141913](https://qt-project.atlassian.net/browse/QTBUG-141913) SortFilterProxyModel: Not be able to run demo using
`qml` utility
* [QTBUG-141242](https://qt-project.atlassian.net/browse/QTBUG-141242) QML file that imports the module it belongs to results
in "Failed to import" qmlls warning
* [QTBUG-137025](https://qt-project.atlassian.net/browse/QTBUG-137025) Early QML signals can be missed
* [QTBUG-139467](https://qt-project.atlassian.net/browse/QTBUG-139467) QtQ4A basic examples do not work starting from 6.9.2
* [QTBUG-141963](https://qt-project.atlassian.net/browse/QTBUG-141963) GC Sweep logic is broken and masks life time bug in
QQmlDelegateModel
* [QTBUG-140757](https://qt-project.atlassian.net/browse/QTBUG-140757) [Reg 6.9->6.10] Performance regression in
delegates_item_childrenRect QmlBench benchmark
* [QTBUG-142082](https://qt-project.atlassian.net/browse/QTBUG-142082) configuring a non-QtQuick build of qtdeclarative with
tests fails
* [QTBUG-141086](https://qt-project.atlassian.net/browse/QTBUG-141086) qmlls: Warnings about missing required property (that is
set)
* [QTBUG-142097](https://qt-project.atlassian.net/browse/QTBUG-142097) Freeze due to infinite loop in garbage collector
* [QTBUG-141883](https://qt-project.atlassian.net/browse/QTBUG-141883) CalendarModel cannot be updated properly
* [QTBUG-141920](https://qt-project.atlassian.net/browse/QTBUG-141920) Inconsistent behavior between QML compiler and
interpreter
* [QTBUG-141776](https://qt-project.atlassian.net/browse/QTBUG-141776) SearchField: the magnifying glass icon clipped at the
top in macOS style
* [QTBUG-142253](https://qt-project.atlassian.net/browse/QTBUG-142253) qmlsc fails to compile list<T>.splice()
* [QTBUG-141734](https://qt-project.atlassian.net/browse/QTBUG-141734) a11y: QML button box has unexpected "page tab list" a11y
role
* [QTBUG-142025](https://qt-project.atlassian.net/browse/QTBUG-142025) qmlls can't read from std::cin
* [QTBUG-142264](https://qt-project.atlassian.net/browse/QTBUG-142264) Top flaky test:
tst_qmlls_qqmlcodemodel::reloadLotsOfFiles
* [QTBUG-142331](https://qt-project.atlassian.net/browse/QTBUG-142331) Problem with FallbackAsVariant lookups in AOT adapter
code in qqml.cpp
* [QTBUG-142555](https://qt-project.atlassian.net/browse/QTBUG-142555) [Reg 6.5.10 -> 6.8.5] Qt.createQmlObject() causes memory
leak
* [QTBUG-141045](https://qt-project.atlassian.net/browse/QTBUG-141045) Remove stale version information from Qt Quick Controls
* [QTBUG-142208](https://qt-project.atlassian.net/browse/QTBUG-142208) Animating shape gradient color increasing memory usage
* [QTBUG-142550](https://qt-project.atlassian.net/browse/QTBUG-142550) AOT crash: SIGSEGV in QMetaObject::indexOfProperty when
QString used in short-circuit expression with derived value
* [QTBUG-142549](https://qt-project.atlassian.net/browse/QTBUG-142549) false warning: Accessible attached property must be
attached to an object deriving from Item or Action
* [QTBUG-142468](https://qt-project.atlassian.net/browse/QTBUG-142468) ASSERT: "!declarationsOverride" in qmllint
* [QTBUG-139362](https://qt-project.atlassian.net/browse/QTBUG-139362) ColorDialog fails to display colors
* [QTBUG-142407](https://qt-project.atlassian.net/browse/QTBUG-142407) [REG 6.2.13 → 6.3.0]  Import of QtQuick.Controls shadows
qualified import QML types
* [QTBUG-141882](https://qt-project.atlassian.net/browse/QTBUG-141882) macOS SearchField produces warnings
* [QTBUG-141729](https://qt-project.atlassian.net/browse/QTBUG-141729) QmlCompiler fail
* [QTBUG-143070](https://qt-project.atlassian.net/browse/QTBUG-143070) macOS SearchField has some styling issues
* [QTBUG-142820](https://qt-project.atlassian.net/browse/QTBUG-142820) Unexpanded QDoc macros in Qt Assistant index
* [QTBUG-141047](https://qt-project.atlassian.net/browse/QTBUG-141047) Screenshot not working in dark mode
* [QTBUG-143547](https://qt-project.atlassian.net/browse/QTBUG-143547) [Reg 6.10.1->6.10.2]: Application palette is reset after
loading a QQuickWidget
* [QTBUG-133449](https://qt-project.atlassian.net/browse/QTBUG-133449) VxWorks doesn't have JIT enabled
* [QTBUG-141543](https://qt-project.atlassian.net/browse/QTBUG-141543) Doc: Overhaul the Positioning with Anchors topic
* [QTBUG-133302](https://qt-project.atlassian.net/browse/QTBUG-133302) ContextMenu opened on TextField sometimes closes
immediately
* [QTBUG-137400](https://qt-project.atlassian.net/browse/QTBUG-137400) tst_qquickcontextmenu::menuItemShouldntTriggerOnRelease
is flaky
* [QTBUG-141398](https://qt-project.atlassian.net/browse/QTBUG-141398) FAIL!  :
tst_QQuickContextMenu::Basic::menuItemShouldntTriggerOnRelease()
Compared values are not the same
* [QTBUG-141406](https://qt-project.atlassian.net/browse/QTBUG-141406) tst_QQuickContextMenu::menuItemShouldntTriggerOnRelease()
is flaky
* [QTBUG-142186](https://qt-project.atlassian.net/browse/QTBUG-142186) MetaObject change in DelegateModel leads to crash in
Plasma
* [QTBUG-137440](https://qt-project.atlassian.net/browse/QTBUG-137440) qt6-declarative qmlcachegen non-determinism
* [QTBUG-142436](https://qt-project.atlassian.net/browse/QTBUG-142436) QmlPreview's window handling is unreliable
* [QTBUG-143071](https://qt-project.atlassian.net/browse/QTBUG-143071) Sporadic crashes on
QSGDistanceFieldGlyphCache::release()
* [QTBUG-129176](https://qt-project.atlassian.net/browse/QTBUG-129176) [REG Qt 6.7.2-> 6.8.0-beta4] Crash in
QRawFont::pathForGlyph() / black screen

### qtactiveqt
* [QTBUG-140884](https://qt-project.atlassian.net/browse/QTBUG-140884) dumpcpp generates incomplete .h and .cpp

### qtmultimedia
* [QTBUG-141840](https://qt-project.atlassian.net/browse/QTBUG-141840) QSoundEffect hangs when switching source url
* [QTBUG-141789](https://qt-project.atlassian.net/browse/QTBUG-141789) [reg 6.7.3->6.8/9/10] Audio Output Example freezes
* [QTBUG-141852](https://qt-project.atlassian.net/browse/QTBUG-141852) tst_qaudiosink: Cannot open int32 audio stream on CI
* [QTBUG-141787](https://qt-project.atlassian.net/browse/QTBUG-141787) QAudioOutput cannot recover from interrupted RDP session
* [QTBUG-141836](https://qt-project.atlassian.net/browse/QTBUG-141836) No audio device detected when using ffmpeg Qt6
multimedia backend
* [QTBUG-140938](https://qt-project.atlassian.net/browse/QTBUG-140938) Reg->6.10.0/Manjaro Linux: QtMultimedia shows no devices
apparently because pipewire-audio is not installed by default
* [QTBUG-142166](https://qt-project.atlassian.net/browse/QTBUG-142166) QAudio::convertVolume missing
* [QTBUG-135598](https://qt-project.atlassian.net/browse/QTBUG-135598) [Windows] Sporadic crashes when call
QVideoFrame::toImage() from working thread
* [QTBUG-131107](https://qt-project.atlassian.net/browse/QTBUG-131107) QVideoFrame::toImage / qImageFromVideoFrame not safe to
call from worker thread
* [QTBUG-142140](https://qt-project.atlassian.net/browse/QTBUG-142140) VideoOutput will report an error and be invisible when
MediaPlayer plays the video for the first time.
* [QTBUG-141662](https://qt-project.atlassian.net/browse/QTBUG-141662) qmlvideo example crashes on startup
* [QTBUG-142695](https://qt-project.atlassian.net/browse/QTBUG-142695) Current #import directives rely on case-insensitive
macOS file system
* [QTBUG-142694](https://qt-project.atlassian.net/browse/QTBUG-142694) [REG 6.8.3-6.10.1] Sporadic crashes on
QSoundEffectPrivateWithPlayer::play
* [QTBUG-142743](https://qt-project.atlassian.net/browse/QTBUG-142743) QtMultimediaPrivate::QRtAudioEngine::getEngineFor crash
with remote connection
* [QTBUG-142242](https://qt-project.atlassian.net/browse/QTBUG-142242) Crash in ffmpeg plugin: ASSERT: "context->free ==
deleteHwFrameContextData"
* [QTBUG-142480](https://qt-project.atlassian.net/browse/QTBUG-142480) Random assertion failure at QPlatformAudioIOStream
* [QTBUG-138223](https://qt-project.atlassian.net/browse/QTBUG-138223) QML Video doesn't autoPlay after source change
* [QTBUG-142939](https://qt-project.atlassian.net/browse/QTBUG-142939) [REG 6.8.3 - 6.10.1][macOS] Sporadic crashes related to
DeviceDisconnectMonitor
* [QTBUG-116767](https://qt-project.atlassian.net/browse/QTBUG-116767) [Boot2Qt] The screen becomes black when showing menu
while using camera in widgets application
* [QTBUG-142542](https://qt-project.atlassian.net/browse/QTBUG-142542) [Boot to Qt] "EGLFS: OpenGL windows cannot be mixed with
others"
* [QTBUG-143058](https://qt-project.atlassian.net/browse/QTBUG-143058) Capturing a still image from a camera to file in QML
crashes on iOS
* [QTBUG-142931](https://qt-project.atlassian.net/browse/QTBUG-142931) Android audio issue with 5.1 AAC: center channel missing
during downmix
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-135922](https://qt-project.atlassian.net/browse/QTBUG-135922) QMediaPlayer::mediaStatusChanged no longer emits
EndOfMedia on video completion
* [QTBUG-135618](https://qt-project.atlassian.net/browse/QTBUG-135618) [MacOS] Sporadic crashes when call
QVideoFrame::toImage()
* [QTBUG-143116](https://qt-project.atlassian.net/browse/QTBUG-143116) Built-in example audiosource is unable to read audio on
macOS with specific USB devices
* [QTBUG-143062](https://qt-project.atlassian.net/browse/QTBUG-143062) [darwin] Sporadic crashes on QMediaRecorder::record
(recording an audio)

### qttools
* [QTBUG-141631](https://qt-project.atlassian.net/browse/QTBUG-141631) [6.9.3 -> 6.10 regression] lupdate hangs when fourth
parameter of translate contains angle brackets and double colon
* [QTBUG-141632](https://qt-project.atlassian.net/browse/QTBUG-141632) lupdate discards string when fourth parameter of
`translate` is wrapped in parentheses
* [QTBUG-141954](https://qt-project.atlassian.net/browse/QTBUG-141954) Cannot inherit from QtQuick Templates in QDoc
* [QTBUG-140728](https://qt-project.atlassian.net/browse/QTBUG-140728) Should Qdoc generate anything when called with
--redirect-documentation-to-dev-null?
* [QTBUG-141642](https://qt-project.atlassian.net/browse/QTBUG-141642) QDoc: Possibility of infinite loops from circular class
relationships
* [QTBUG-137048](https://qt-project.atlassian.net/browse/QTBUG-137048) qdoc: Warn about self-link in \sa
* [QTBUG-142504](https://qt-project.atlassian.net/browse/QTBUG-142504) Fix doc links in qttools
* [QTBUG-142577](https://qt-project.atlassian.net/browse/QTBUG-142577) Qt Designer on Mac OS fails to load a custom widget
plugin due to code signature issue
* [QTBUG-143192](https://qt-project.atlassian.net/browse/QTBUG-143192) Documentation of overloaded signals/slots shows wrong
snippets
* [QTBUG-143212](https://qt-project.atlassian.net/browse/QTBUG-143212) QDoc: Empty link target causes crash
* [QTBUG-69423](https://qt-project.atlassian.net/browse/QTBUG-69423) QRandomGenerator not random on certain Windows
installations
* [QTBUG-129193](https://qt-project.atlassian.net/browse/QTBUG-129193) Qt compiled with gcc 13 and -march=bdver4/-mtune=bdver4
causes segfaults in tests, downstream applications
* [QTBUG-115448](https://qt-project.atlassian.net/browse/QTBUG-115448) qttools -unity-build-batch-size 100000 fails

### qtdoc
* [QTBUG-141358](https://qt-project.atlassian.net/browse/QTBUG-141358) Static build documentation out of date
* [QTBUG-138991](https://qt-project.atlassian.net/browse/QTBUG-138991) localization documentation shows wrong catalog name for
Qt WebSockets
* [QTBUG-142071](https://qt-project.atlassian.net/browse/QTBUG-142071) 5.15 is still listed as the supported versions
* [QTBUG-142245](https://qt-project.atlassian.net/browse/QTBUG-142245) [Boot2Qt] Cannot run lightning viewer example on the
device
* [QTBUG-141228](https://qt-project.atlassian.net/browse/QTBUG-141228) stocqt example: Live Data retrieval does not work
anymore for new keys
* [QTBUG-138148](https://qt-project.atlassian.net/browse/QTBUG-138148) photosurface example: CMake warning QTP0004
* [QTBUG-138147](https://qt-project.atlassian.net/browse/QTBUG-138147) stocqt example: CMake warning QTP0004
* [QTBUG-143100](https://qt-project.atlassian.net/browse/QTBUG-143100) QtJenny example won't compile due to fatal errors

### qtlocation
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtpositioning
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-142317](https://qt-project.atlassian.net/browse/QTBUG-142317) QGeoPath.contains() does not work correctly
* [QTBUG-142020](https://qt-project.atlassian.net/browse/QTBUG-142020) Incorrect usage of qFuzzyCompare() abounds in Qt source
[QtCore]

### qtsensors
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtwayland
* [QTBUG-142162](https://qt-project.atlassian.net/browse/QTBUG-142162) wl_output_send_done is not called when new client binds
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-138907](https://qt-project.atlassian.net/browse/QTBUG-138907) Probable Use after Free on
QtWaylandCompositor::onSurfaceDestroyed

### qt3d
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtimageformats
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtserialbus
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtserialport
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtwebsockets
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtwebchannel
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtwebengine
* [QTBUG-139461](https://qt-project.atlassian.net/browse/QTBUG-139461) Getting error "Cannot read property 'destroy' of
undefined" when trying to close the tab in Nano Browser example
* [QTBUG-141739](https://qt-project.atlassian.net/browse/QTBUG-141739) [REG 6.9.2-6.9.3] Sporadic deadlocks on WebEngineView
destruction
* [QTBUG-141214](https://qt-project.atlassian.net/browse/QTBUG-141214) WebEngine freezes UI
* [QTBUG-141476](https://qt-project.atlassian.net/browse/QTBUG-141476) &lt;select&gt; element does not work in Weston
* [QTBUG-140321](https://qt-project.atlassian.net/browse/QTBUG-140321) When QT_QPA_PLATFORM is set to wayland, QtWebEngine
cannot select items in a &lt;select&qt; element.
* [QTBUG-139709](https://qt-project.atlassian.net/browse/QTBUG-139709) Qt WebEngine: HTML "select" elements have excessive gap
* [QTBUG-135040](https://qt-project.atlassian.net/browse/QTBUG-135040) macos: Voice Over rect is wrongly calculated for
WebEngine
* [QTBUG-138747](https://qt-project.atlassian.net/browse/QTBUG-138747) Virtual Keyboard is not displayed after selecting the
pull-down menu of the Web with QtWebEngine + QVK + Wayland
* [QTBUG-131650](https://qt-project.atlassian.net/browse/QTBUG-131650) qtwebengine does not compile under sccache, with note
note: please rebuild precompiled header
* [QTBUG-142497](https://qt-project.atlassian.net/browse/QTBUG-142497) [REG 6.10.0->6.10.1] RKWard and slitherer crashed when
starting with Qt 6.10.1
* [QTBUG-142720](https://qt-project.atlassian.net/browse/QTBUG-142720) Crash in Qt6WebEngineCore during GPUInfo initialization
* [QTBUG-139335](https://qt-project.atlassian.net/browse/QTBUG-139335) QtWebEngine based browser shows nothing with MESA
LLVMpipe
* [QTBUG-142534](https://qt-project.atlassian.net/browse/QTBUG-142534) [REG 6.10.1-6.10.2] Broken rendering when reparenting
WebEngineView to another window (again)
* [QTBUG-131304](https://qt-project.atlassian.net/browse/QTBUG-131304) Broken rendering when reparenting WebEngineView to
another window
* [QTBUG-140444](https://qt-project.atlassian.net/browse/QTBUG-140444) Service workers do not honor
QWebEngineProfile::setHttpUserAgent
* [QTBUG-140232](https://qt-project.atlassian.net/browse/QTBUG-140232) Crash when removing QWebEngineView while printing a
document
* [QTBUG-137768](https://qt-project.atlassian.net/browse/QTBUG-137768) Crash in WebEngineQuick when rapidly switching between
multiple WebEngineView component
* [QTBUG-116619](https://qt-project.atlassian.net/browse/QTBUG-116619) Building under iOS produces hundreds of warnings related
to QtWebEngine and PDF
* [QTBUG-142320](https://qt-project.atlassian.net/browse/QTBUG-142320) [REG 6.10.0 -> .1] Frequent segfaults in QAccessible
* [QTBUG-142805](https://qt-project.atlassian.net/browse/QTBUG-142805) [REG 6.8.3-6.9.3] Crash if UpdateTooltip is called on
time while WebEngineView is being destroyed
* [QTBUG-96239](https://qt-project.atlassian.net/browse/QTBUG-96239) Document CMake component in CMake function documentation
* [QTBUG-141785](https://qt-project.atlassian.net/browse/QTBUG-141785) qtwebengine builds on windows don't /mostly/ use sccache

### qtwebview
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-75747](https://qt-project.atlassian.net/browse/QTBUG-75747) Windows: Support WebView2 backend on msvc

### qtcharts
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtdatavis3d
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtvirtualkeyboard
* [QTBUG-135140](https://qt-project.atlassian.net/browse/QTBUG-135140) Using a virtual keyboard with binding removal causes QML
output logging to throw binding removal errors.
* [QTBUG-137440](https://qt-project.atlassian.net/browse/QTBUG-137440) qt6-declarative qmlcachegen non-determinism

### qtscxml
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtnetworkauth
* [QTBUG-133086](https://qt-project.atlassian.net/browse/QTBUG-133086) Doc: Improve Networking and WebEngine security topics
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtremoteobjects
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtlottie
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtquicktimeline
* [QTBUG-142669](https://qt-project.atlassian.net/browse/QTBUG-142669) RuntimeLoader produces continuous debug output
(“QQuickVector3DValueType… QVariant(Invalid)”) when loading an animated
file
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtquick3d
* [QTBUG-142813](https://qt-project.atlassian.net/browse/QTBUG-142813) View3D of qtquick3d/hellocube does not produce visual
output, when building single threaded
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-143094](https://qt-project.atlassian.net/browse/QTBUG-143094) The StaticRigidBody  is not refreshed after changing
source geometry object.

### qtcoap
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtopcua
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qthttpserver
* [QTBUG-138410](https://qt-project.atlassian.net/browse/QTBUG-138410) QtHttpServer: The HTTP/1.0 support is incomplete

### qtquick3dphysics
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtgrpc
* [QTBUG-129286](https://qt-project.atlassian.net/browse/QTBUG-129286) GRPC: Implement HTTP/2 dataframe decompression
* [QTBUG-141780](https://qt-project.atlassian.net/browse/QTBUG-141780) Top flaky test:
QtGrpcClientEnd2EndTest::clientHandlesCompression
* [QTBUG-138179](https://qt-project.atlassian.net/browse/QTBUG-138179) Qt GRPC documentation: \gRPC macro doesnt' work
* [QTBUG-142759](https://qt-project.atlassian.net/browse/QTBUG-142759) Docs display unprocessed \gRPC qdoc macro
* [QTBUG-141872](https://qt-project.atlassian.net/browse/QTBUG-141872) QDoc: error: Documentation warnings (2) exceeded the
limit (0) for 'QtProtobuf'.
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtgraphs
* [QTBUG-141698](https://qt-project.atlassian.net/browse/QTBUG-141698) Generate OpenGL ES 3 shaders for qsb files in
graphs/2d/cockpit/
* [QTBUG-141927](https://qt-project.atlassian.net/browse/QTBUG-141927) GridLine.qml uses deprecated material type
* [QTBUG-142047](https://qt-project.atlassian.net/browse/QTBUG-142047) Render slice to image does not show labels correctly
* [QTBUG-142454](https://qt-project.atlassian.net/browse/QTBUG-142454) Surface Gallery oscilloscope demo slice view sometimes
stays incorrectly visible
* [QTBUG-142437](https://qt-project.atlassian.net/browse/QTBUG-142437) XYModelMapper produces unavoidable warning if
xSection/ySection uses property bindings
* [QTBUG-142418](https://qt-project.atlassian.net/browse/QTBUG-142418) Surface graph crash when trying to render a column slice
into image
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qmlcompilerplus (Commercial only)
* [QTBUG-143037](https://qt-project.atlassian.net/browse/QTBUG-143037) QML: Enum class properties cannot be compiled with
--direct-calls

Known Issues
------------
* Check that your system meets Qt's requirements:
  https://doc-snapshots.qt.io/qt6-6.10/supported-platforms.html
* RTA reported issues from Qt 6.10
  https://qt-project.atlassian.net/issues/?filter=10825
* See Qt 6.10 known issues from:
  https://wiki.qt.io/Qt_6.10_Known_Issues
* Qt 6.10.2 Open issues in Jira:
  https://qt-project.atlassian.net/issues/?filter=19482

Credits for the release goes to:
---------------------------------

Eirik Aavitsland  
Laszlo Agocs  
Dilek Akcay  
Alexander Akulich  
Konsta Alajärvi  
Stanislav Aleksandrov  
Even Oscar Andersen  
Dimitrios Apostolou  
Mate Barany  
Vladimir Belyavsky  
Kizito Birabwa  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
David Boddie  
Tatiana Borisova  
Joerg Bornemann  
Assam Boudjelthia  
Aurélien Brooke  
Oswald Buddenhagen  
Eren Bursali  
Olivier De Cannière  
Alexei Cazacov  
Kaloyan Chehlarski  
Michael Cho  
Paul Colby  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Szabolcs David  
Artem Dyomin  
Oliver Eftevaag  
Christian Ehrlicher  
Andreas Eliasson  
Nicolas Fella  
Marcus Gama  
John Paul Adrian Glaubitz  
Julian Greilich  
Robert Griebl  
Richard Moe Gustavsen  
Mikko Hallamaa  
Inkamari Harjula  
Andreas Hartmetz  
Jani Heikkinen  
Moss Heim  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Karl Ove Hufthammer  
Masoud Jami  
Morteza Jamshidi  
Allan Sandfeld Jensen  
Jonas Karlsson  
Friedemann Kleint  
Michal Klocek  
Ingo Klöcker  
Tomi Korpipää  
Jani Korteniemi  
Fabian Kosmale  
Mike Krus  
Kai Köhne  
Inho Lee  
Frédéric Lefebvre  
Wladimir Leuschner  
Robert Löhning  
Thiago Macieira  
Jan Moeller  
Sheree Morphett  
Kenji Mouri  
Marc Mutz  
Mårten Nordheim  
Daniel Nylander  
Dennis Oberst  
Kwanghyo Park  
Jerome Pasion  
Mauro Persano  
Samuli Piippo  
Karim Pinter  
Timur Pocheptsov  
Joni Poikelin  
Aleix Pol  
Rami Potinkara  
Lorn Potter  
Sakaria Pouke  
MohammadHossein Qanbari  
Liang Qi  
David Redondo  
Topi Reinio  
Konstantin Ritt  
Kaarle Ritvanen  
Shawn Rutledge  
Emir SARI  
Toni Saario  
Ahmad Samir  
Nick Shaforostov  
Sami Shalayel  
Nils Petter Skålerud  
Ivan Solovev  
Axel Spoerl  
Christian Strømme  
Tarja Sundqvist  
Lars Sutterud  
Michael Szczerba  
Błażej Szczygieł  
Morten Sørvig  
Elias Toivola  
Esa Törmänen  
Sami Varanka  
Peter Varga  
Bror Wetlesen Vedeld  
Tor Arne Vestbø  
Petri Virkkunen  
Ville Voutilainen  
Olli Vuolteenaho  
Jaishree Vyas  
Yixue Wang  
Miao Wang  
Michael Weghorn  
Edward Welbourne  
Paul Wicking  
Oliver Wolff  
Lu YaNing  
Erin of Yukis  
Vlad Zahorodnii  
Wang Zichong  
Johanna Äijälä  
