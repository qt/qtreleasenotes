Release note
============
Qt 6.9.3 release is a patch release made on the top of Qt 6.9.2.
As a patch release, Qt 6.9.3 does not add any new functionality but provides
bug fixes and other improvements and maintains both forward and backward
compatibility (source and binary) with the 6.9.x series.

For detailed information about Qt 6.9, refer to the online documentation
included in this distribution. The documentation is also available online:

https://doc.qt.io/qt-6/index.html

The Qt version 6.9 series is binary compatible with the 6.8.x series.
Applications compiled for 6.8 will continue to run with 6.9.

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
* N/A

### qtbase
* 76502f946ce Fix the url construction in the requestUrl method
QNetworkRequestFactory::createRequest() doesn't decode the provided
`path` anymore. If the path string was passed encoded by the user, it
stays encoded in the particular way.

* 2847ec90d31 QFileSystemEngine/BSD: check UF_HIDDEN on the symlink only
Fixed a bug that caused isHidden() to return true on BSDs and Apple
OSes for non-hidden symlinks that pointed to hidden targets.

* 35a37bc2719 QDirListing: check for '.' and '..' after the checking the
name filters
Now listing '.' and '..' special entries respects any set name filters.
Previously if IncludeDotAndDotDot was set, '.' and '..' would always be
listed.

* 7361066eea2 Doc: Classify 3rd party code in cmake as tools
Reclassify third-party components "KWin" and "extra-cmake-modules" as
tools related.

* 3e07123c64f windeployqt: Add parameter to extend timeout of
qmlimportscanner
Add option to control timeout for qmlimportscanner runs.

* 3a545d75886 QTest::qWaitFor*: capture the widget/window using QPointer
Fixed a bug that would cause the qWaitForWindow* and qWaitForWidget*
functions to crash or misbehave if the window or widget they were told
to wait on was destroyed in the process of waiting for it to be
shown/focused/activated/exposed.

* 9ad39d7c9ac qvsnprintf: fail if the result size doesn't fit into an
int
Fixed a bug that would cause q(v)snprintf() to report success on some
platforms, even though the result was truncated.

* eff18b4690c Android: Set name-matched class names for Slider and
ScrollBar for TalkBack
Use different Android class names for Slider and Scroller.

* e4cd1648a94 Android: Use the TalkBack focus signal to trigger
focusAction
Use TalkBack ACTION_ACCESSIBILITY_FOCUS to trigger focusAction.

* 3782e6fb2ae QJsonDocument/Value: fix integer truncation in
fromJson(QByteArray)
Fixed a bug on 64-bit platforms where fromJson(QByteArray) could report
one of the Unterminated errors for valid input whose size merely
exceeded INT_MAX (2GiB).

* 04ae1919b05 moveToTrash/XDG: allow $XDG_DATA_HOME/Trash to be a
symlink
Fixed a bug that caused moveToTrash() to disallow trashing to trash
bins using the XDG Trash Specification when the trash path was a
symlink.

* 5ff534446a5 Upgrade PCRE2 to 10.46
PCRE2 was updated to version 10.46.

* ea658356d65 Suppress construction of QTimeZone(Qt::TimeSpec)
Construction from a Qt::TimeSpec, which was never meant to be
supported, is now rejected at compile time, where previously compilers
(mis)interpreted the enum as an int so called the (int offsetSeconds)
constructor, with results consistently at odds with what the user
presumably expected.

* 93c415b9e1e Respect QT_NO_INT128 in qtypes.cpp's #error
Made it possible to compile Qt with GCC in strict C++ mode (-ansi or
-std=c++NN) again, provided QT_NO_INT128 is defined, too.

* 0124969f62f Add camel-case header for qtconcurrenttask.h
Added a camel-case QtConcurrentTask header, which is the same as
QtConcurrent/qtconcurrenttask.h.

* 41eed0527f0 Update bundled libjpeg-turbo to version 3.1.2
libjpeg-turbo was updated to version 3.1.1

* 4ae32f5bdd7 QStringConverter: allow appendToBuffer() to write to the
buffer
The appendToBuffer() functions in QStringEncoder and QStringDecoder may
write to parts of the provided output beyond the returned pointer.
Caller code must not assume the data beyond that remains unmodified.

* 56a633041cd Make QTEST_THROW_ON_FAIL work from within QtConcurrent
Fixed a bug which prevented QTEST_THROW_ON_FAIL and QTEST_THROW_ON_SKIP
from working with QCOMPARE(), QVERIFY(), and QSKIP() invoked from within
QtConcurrent functions.

* 228370e3f8a Update Freetype to 2.14.1
Updated bundled Freetype to 2.14.1.

* be09b211db7 Upgrade Harfbuzz to 11.5.0
Upgraded Harfbuzz to version 11.5.0.

### qtsvg
* ea44b50c Replace check for endless recursion when loading
Fix stack overflow when an element references its child element using
url()

### qt3d
* 17bc9ad74 Update assimp dependency
Update ASSIMP to 6.0.2

### qtimageformats
* b873de3e Update bundled libtiff to version 4.7.1
Bundled libtiff was updated to version 4.7.1

### qtquick3d
* ebdd2806f Update Assimp to v6.0.2
Update ASSIMP to v6.0.2

### qtopcua
* 923ead9b Fix detach() for QOpcUaDataValue
QOpcUaDataValue now detaches its shared data    as expected when
timestamp picoseconds are set.

### qtgrpc
* bc7de6f4 Emit cancelled finished() in channel implementation
Cancellation logic should also emit finished now. Custom
QAbstractGrpcChannel implementations should adapt their logic.

* 607ab4ea QGrpcHttp2Channel: Guarantee transportation scheme
Requesting TLS or QLocalSocket now fails with a fatal error if the
requested transport is unavailable.


Fixes
-----

### qtbase
* [QTBUG-138056](https://bugreports.qt.io/browse/QTBUG-138056) QSortFilterProxyModel: Crash when changing sourceModel
(QPropertyBindingData / QBindingStorage)
* [QTBUG-138488](https://bugreports.qt.io/browse/QTBUG-138488) [iOS] URL handler do not receive data from external apps
via Universal Link
* [QTBUG-138374](https://bugreports.qt.io/browse/QTBUG-138374) QFileSystemWatcher::addPath() is slow on macos
* [QTBUG-138642](https://bugreports.qt.io/browse/QTBUG-138642) ODBC possible data loss with 'real' column
* [QTBUG-8963](https://bugreports.qt.io/browse/QTBUG-8963) Driver for ODBC - qsql_odbc.cpp should use the
QMetaType:float when sql type is SQL_FLOAT instead of QVariant::Double
* [QTBUG-138904](https://bugreports.qt.io/browse/QTBUG-138904) QIBASE driver fails to build when linking against
Firebird v2.5
* [QTBUG-138861](https://bugreports.qt.io/browse/QTBUG-138861) `QRhiResourceUpdateBatch` leaks memory if submitted via
`beginOffscreenFrame`
* [QTBUG-138250](https://bugreports.qt.io/browse/QTBUG-138250) Win11 23h2 ARM: QtBase -
tst_QRhi::storageBufferRuntimeSizeGraphics(OpenGL) 'pipeline->create()'
returned FALSE
* [QTBUG-93182](https://bugreports.qt.io/browse/QTBUG-93182) Occasional asserts when touch scroll NSEventPhaseEnded is
processed while event in queue indicates momentumPhase has begun
* [QTBUG-124011](https://bugreports.qt.io/browse/QTBUG-124011) Android: QFileInfo::isWritable() returns false
erroneously and throws an exception
* [QTBUG-115143](https://bugreports.qt.io/browse/QTBUG-115143) Unable to open files under certain conditions on
Android.
* [QTBUG-114979](https://bugreports.qt.io/browse/QTBUG-114979) Two issues using content scheme to work with files
* [QTBUG-138922](https://bugreports.qt.io/browse/QTBUG-138922) Consistent Qt caused crash when navigating with Jetpack
Compose
* [QTBUG-132490](https://bugreports.qt.io/browse/QTBUG-132490) Android and TestNamespace: errors in Qt JNI methods
* [QTBUG-139051](https://bugreports.qt.io/browse/QTBUG-139051) Background color of QPlainTextEdit without border
cannont be set on Win11
* [QTBUG-138401](https://bugreports.qt.io/browse/QTBUG-138401) [REG dev] Windows11 Style: Check-boxes' drawing
regression
* [QTBUG-139106](https://bugreports.qt.io/browse/QTBUG-139106) REG: Variable fonts no longer works with Freetype
backend
* [QTBUG-139211](https://bugreports.qt.io/browse/QTBUG-139211) tst_qquickpopup (Failed)
* [QTBUG-100991](https://bugreports.qt.io/browse/QTBUG-100991) Some tests crash on Android CI
* [QTBUG-131695](https://bugreports.qt.io/browse/QTBUG-131695) tst_qquickpopup tst_QQuickPopup::fadeDimmer is flaky
* [QTBUG-125083](https://bugreports.qt.io/browse/QTBUG-125083) [Android] ANRs related to QtNativeInputConnection
* [QTBUG-132695](https://bugreports.qt.io/browse/QTBUG-132695) Crash in QGuiApplication::applicationStateChanged() when
quitting app
* [QTBUG-139400](https://bugreports.qt.io/browse/QTBUG-139400) Properly manage QtEditText focus and InputConnection
callbacks
* [QTBUG-138982](https://bugreports.qt.io/browse/QTBUG-138982) qt-android-runner.py fails to start application
* [QTBUG-138622](https://bugreports.qt.io/browse/QTBUG-138622) Android launch wrapper script can conflict with qml
subdirectory name on case insensitive file systems
* [QTBUG-137769](https://bugreports.qt.io/browse/QTBUG-137769) Keyboard is not closed when TextEdit loses focus while
using TalkBack
* [QTBUG-138561](https://bugreports.qt.io/browse/QTBUG-138561) QFont::exactMatch index out of bounds
* [QTBUG-139128](https://bugreports.qt.io/browse/QTBUG-139128) QObject::connect(): clarify what a valid method is, in
the string-based overloads
* [QTBUG-138986](https://bugreports.qt.io/browse/QTBUG-138986) glFramebufferTexture2DMultisampleEXT() is called with a
wrong samples argument if the requested sample count is unsupported
* [QTBUG-119205](https://bugreports.qt.io/browse/QTBUG-119205) tst_Android::orientationChange is flaky on android
* [QTBUG-44569](https://bugreports.qt.io/browse/QTBUG-44569) QScreen::orientation() does not return actual screen
orientation on android
* [QTBUG-44554](https://bugreports.qt.io/browse/QTBUG-44554) QScreen::orientationChanged signal does not work
correctly on android
* [QTBUG-109127](https://bugreports.qt.io/browse/QTBUG-109127) QScreen::geometry() not always correct in
orientationChanged() slot
* [QTBUG-35237](https://bugreports.qt.io/browse/QTBUG-35237) Can't get "inverted" orientations while rotating android
device.
* [QTBUG-48549](https://bugreports.qt.io/browse/QTBUG-48549) Screen's orientation not updated when rotating by 180°
(in one movement) on Android
* [QTBUG-35428](https://bugreports.qt.io/browse/QTBUG-35428) In Screen.onOrientationChanged, the previous size is
reported instead of the new one
* [QTBUG-39401](https://bugreports.qt.io/browse/QTBUG-39401) QScreen::orientationChanged not fired on Android but
fired on iOS in the same conditions
* [QTBUG-94459](https://bugreports.qt.io/browse/QTBUG-94459) Android reports incorrect screen size after rotation
* [QTBUG-138984](https://bugreports.qt.io/browse/QTBUG-138984) Possible misinterpretation of
specifications.freedesktop.org/trash-spec
* [QTBUG-136629](https://bugreports.qt.io/browse/QTBUG-136629) QUnifiedTimer::updateAnimationTimers() crashes when
QApplication is recreated
* [QTBUG-125138](https://bugreports.qt.io/browse/QTBUG-125138) QSqlDatabase::record() does not report generated columns
for SQlite
* [QTBUG-139119](https://bugreports.qt.io/browse/QTBUG-139119) QFuture::takeResult asserts
* [QTBUG-139586](https://bugreports.qt.io/browse/QTBUG-139586) [Reg 6.9.1->6.9.2] Cannot send broadcast on macOS
anymore
* [QTBUG-139600](https://bugreports.qt.io/browse/QTBUG-139600) Memory leak on macOS when adding application font from
data
* [QTBUG-135643](https://bugreports.qt.io/browse/QTBUG-135643) Window glitches when using Qt::ExpandedClientAreaHint
* [QTBUG-133943](https://bugreports.qt.io/browse/QTBUG-133943) Qt::ExpandedClientAreaHint results in different rounded
window corners on Windows
* [QTBUG-133946](https://bugreports.qt.io/browse/QTBUG-133946) Qt::ExpandedClientAreaHint breaks minimizing on Windows
* [QTBUG-138465](https://bugreports.qt.io/browse/QTBUG-138465) Line edits are not visible on macOS 26
* [QTBUG-139360](https://bugreports.qt.io/browse/QTBUG-139360) Editable combo box on macOS Tahoe
* [QTBUG-138946](https://bugreports.qt.io/browse/QTBUG-138946) QSlider issues on macOS 26
* [QTBUG-139439](https://bugreports.qt.io/browse/QTBUG-139439) CMake fails due to 'pthread_cancel' when configuring Qt
project for Android with CMake 4.x
* [QTBUG-138678](https://bugreports.qt.io/browse/QTBUG-138678) Crash in QTextEdit while inserting a column into a HTML
table
* [QTBUG-139291](https://bugreports.qt.io/browse/QTBUG-139291) showMaximized() does not maximize QDialog
* [QTBUG-139720](https://bugreports.qt.io/browse/QTBUG-139720) Tag errors in QtAbstractItemModel for Java
* [QTBUG-139688](https://bugreports.qt.io/browse/QTBUG-139688) Public Java Classes Documentation Bugs
* [QTBUG-134896](https://bugreports.qt.io/browse/QTBUG-134896) QUrl's qHash() is inconsistent with its operator==
* [QTBUG-134900](https://bugreports.qt.io/browse/QTBUG-134900) QUrl's operator==() is taking bygone data into account
* [QTBUG-102020](https://bugreports.qt.io/browse/QTBUG-102020) Incorrect layout in QTabBar when last tab is hidden
* [QTBUG-139791](https://bugreports.qt.io/browse/QTBUG-139791) Buttons don't work when the last tab is hidden
* [QTBUG-139983](https://bugreports.qt.io/browse/QTBUG-139983) macOS (Tahoe): assert in
tst_QStyleSheetStyle::complexWidgetFocus()
* [QTBUG-134082](https://bugreports.qt.io/browse/QTBUG-134082) Screen orientation change causes rendering issues on Qt
Quick Application (flicker related)
* [QTBUG-124140](https://bugreports.qt.io/browse/QTBUG-124140) [REG]: 6.7.0  full-screen app displays background window
(or splash-screen) graphics at top/bottom during multiwindow split
display
* [QTBUG-140064](https://bugreports.qt.io/browse/QTBUG-140064) error: array subscript 'QTransform[0]' is partly outside
array bounds of 'QVariant [1]'
* [QTBUG-135808](https://bugreports.qt.io/browse/QTBUG-135808) Some problems with Expanded Client Areas on Android
* [PYSIDE-3173](https://bugreports.qt.io/browse/PYSIDE-3173) Emojis on Button Label Silently Crash PySide App
* [QTBUG-139990](https://bugreports.qt.io/browse/QTBUG-139990) [REG 6.10.0 beta 3 -> beta 4] Building Qt examples for
WebAssembly fails
* [QTBUG-138848](https://bugreports.qt.io/browse/QTBUG-138848) Content-Length header always sent in HTTP GET request
* [QTBUG-139944](https://bugreports.qt.io/browse/QTBUG-139944) macOS: title/text alignment on push buttons
* [QTBUG-139989](https://bugreports.qt.io/browse/QTBUG-139989) FAIL!  : tst_QStateMachine::twoAnimations() Compared
values are not the same
* [QTBUG-139765](https://bugreports.qt.io/browse/QTBUG-139765) QTEST_THROW_ON_FAIL doesn't work from inside
QtConcurrent
* [QTBUG-139040](https://bugreports.qt.io/browse/QTBUG-139040) Unreadable image on https://doc.qt.io/qt-6/animation-
overview.html
* [QTBUG-140192](https://bugreports.qt.io/browse/QTBUG-140192) tst_qwidget (Failed) - tst_QWidget::resizeEvent()
Compared values are not the same
* [QTBUG-139690](https://bugreports.qt.io/browse/QTBUG-139690) SwipeView Android Expanded Client Area hides
NavigationBar
* [QTBUG-138878](https://bugreports.qt.io/browse/QTBUG-138878) QNetworkRequestFactory creates an incorrect network
request
* [QTBUG-137860](https://bugreports.qt.io/browse/QTBUG-137860) [Windows][A11y] Text can not be selected by NVDA
* [QTBUG-135044](https://bugreports.qt.io/browse/QTBUG-135044) tst_QStringApiSymmetry fails under ASAN
(GenerationalCollator is leaked?)
* [QTBUG-134080](https://bugreports.qt.io/browse/QTBUG-134080) "QObject::~QObject: Timers cannot be stopped from
another thread" message in Qt 6.8.2 plugins
* [QTBUG-133861](https://bugreports.qt.io/browse/QTBUG-133861) [macOS] QML Preview: Closing the preview window produces
QObject::killTimer warning
* [QTBUG-132697](https://bugreports.qt.io/browse/QTBUG-132697) FAIL!  :
tst_QQmlDebugJS::setBreakpointInScriptThatQuits(custom)
'm_process->waitForFinished()' returned FALSE.
* [QTBUG-102984](https://bugreports.qt.io/browse/QTBUG-102984) QML debugger and profiler tests hangs on macOS/x86_64 in
CI
* [QTBUG-132381](https://bugreports.qt.io/browse/QTBUG-132381) [REG 6.8 -> 6.9] Crash when QGuiApplication is static
* [QTBUG-138829](https://bugreports.qt.io/browse/QTBUG-138829) Fix uses of deprecated
NSWindowStyleMaskTexturedBackground
* [QTBUG-37759](https://bugreports.qt.io/browse/QTBUG-37759) QWidget-gestures do not work
* [QTBUG-46195](https://bugreports.qt.io/browse/QTBUG-46195) [Windows]: Swipe gesture is not always recognized and
sometimes in the wrong direction
* [QTBUG-123585](https://bugreports.qt.io/browse/QTBUG-123585) Memory Leak: QGestureRecognizer::unregisterRecognizer()
* [QTBUG-138403](https://bugreports.qt.io/browse/QTBUG-138403) QDirIterator → QDirListing should have some porting
documentation
* [QTBUG-134093](https://bugreports.qt.io/browse/QTBUG-134093) Android application crashes on 16 KB page size
* [QTBUG-132211](https://bugreports.qt.io/browse/QTBUG-132211) [REG 6.7 -> 6.8][Android] UnsatisfiedLinkError onResume
and onNewIntent
* [QTBUG-120467](https://bugreports.qt.io/browse/QTBUG-120467) Link error from Google Play testing
* [QTBUG-70114](https://bugreports.qt.io/browse/QTBUG-70114) Java native functions registered with a delay
* [QTBUG-86314](https://bugreports.qt.io/browse/QTBUG-86314) Error in 64bit lib file path names
* [QTBUG-139055](https://bugreports.qt.io/browse/QTBUG-139055) CMake Error at tst_qstatemachineWrapperDebug
* [QTBUG-139139](https://bugreports.qt.io/browse/QTBUG-139139) ubuntu-24.04-x64-developer-build: Part of the build is
using qmake and ignores SCCACHE settings
* [QTBUG-136653](https://bugreports.qt.io/browse/QTBUG-136653) tst_QAbstractItemView::testDialogAsEditor() crash on
Ubuntu 24.04 x11
* [QTBUG-139275](https://bugreports.qt.io/browse/QTBUG-139275) [a11y] Changes to Accessible.name for focused element
not announced to Screen Reader
* [QTBUG-138249](https://bugreports.qt.io/browse/QTBUG-138249) Win11 23h2 ARM: QtBase -
tst_QRhiWidget::grabFramebufferWhileStillInvisible fails
* [QTBUG-138252](https://bugreports.qt.io/browse/QTBUG-138252) Win11 23h2 ARM: QtBase -
tst_QRhiWidget::grabFramebufferWhileStillInvisible fails with cross-
compilation target
* [QTBUG-138806](https://bugreports.qt.io/browse/QTBUG-138806) [VxWorks] Flickable doesn't work on VxWorks
* [QTBUG-107028](https://bugreports.qt.io/browse/QTBUG-107028) tst_qquicktextfield and tst_qquicktextarea fail on
Android
* [QTBUG-100259](https://bugreports.qt.io/browse/QTBUG-100259) tst_controls crash on Android
* [QTBUG-100258](https://bugreports.qt.io/browse/QTBUG-100258) tst_focus crashes on Android
* [QTBUG-139415](https://bugreports.qt.io/browse/QTBUG-139415) tst_controls has failing test cases
* [QTBUG-139283](https://bugreports.qt.io/browse/QTBUG-139283) QInputDevice::availableVirtualGeometry property
incomplete
* [QTBUG-138699](https://bugreports.qt.io/browse/QTBUG-138699) Square push buttons (macOS 26)
* [QTBUG-135964](https://bugreports.qt.io/browse/QTBUG-135964) Windows theme uses wrong colors if high-contrast mode is
activated
* [QTBUG-133086](https://bugreports.qt.io/browse/QTBUG-133086) Doc: Improve Networking and WebEngine security topics
* [QTBUG-138700](https://bugreports.qt.io/browse/QTBUG-138700) Tabs have wrong shape on macOS 26
* [QTBUG-127705](https://bugreports.qt.io/browse/QTBUG-127705) Android splashscreen not removed
* [QTBUG-139606](https://bugreports.qt.io/browse/QTBUG-139606) [regression] App window blank when switching from
background to foreground
* [QTBUG-139659](https://bugreports.qt.io/browse/QTBUG-139659) Activity can stop reacting to touch events
* [QTBUG-138948](https://bugreports.qt.io/browse/QTBUG-138948) Radio button alignment issues on macOS 26
* [QTBUG-138738](https://bugreports.qt.io/browse/QTBUG-138738) Incorrect focus ring rendering
* [QTBUG-138893](https://bugreports.qt.io/browse/QTBUG-138893) QTimeZone(Qt::UTC) returns incorrect UTC offset (+1
second)
* [QTBUG-137564](https://bugreports.qt.io/browse/QTBUG-137564) tst_qmovie fails
* [QTBUG-139986](https://bugreports.qt.io/browse/QTBUG-139986) QStateMachine tests aren't running on the CI
* [QTBUG-140038](https://bugreports.qt.io/browse/QTBUG-140038) tst_QGridLayout::spacingsAndMargins fails on Android 15
* [QTBUG-139951](https://bugreports.qt.io/browse/QTBUG-139951) [VxWorks] 6.8.4 -> 6.8.5 regression build failure with
VxWorks 24.03
* [QTBUG-139280](https://bugreports.qt.io/browse/QTBUG-139280) Cannot build QT 6.8 without GNU extensions
* [QTBUG-140133](https://bugreports.qt.io/browse/QTBUG-140133) tst_QGraphicsProxyWidget::createProxyForChildWidget
fails with non-zero safe area margins
* [QTBUG-117447](https://bugreports.qt.io/browse/QTBUG-117447) Remove *-proxy.html pages in Qt Core
* [QTBUG-138659](https://bugreports.qt.io/browse/QTBUG-138659) QTextBoundaryFinder is copyable (deep-copies lookup
tables), but not movable
* [QTBUG-139676](https://bugreports.qt.io/browse/QTBUG-139676) [a11y] "Switch" role is missing
* [QTBUG-139007](https://bugreports.qt.io/browse/QTBUG-139007) QFileSystemEngine::fillMetaData fails on hostfs
* [QTBUG-139994](https://bugreports.qt.io/browse/QTBUG-139994) Nullptr swapchain dereference in
QBackingStoreDefaultCompositor::flush

### qtsvg
* [QTBUG-137553](https://bugreports.qt.io/browse/QTBUG-137553) [REG 6.8.2 -> 6.8.3] Significant performance regression
in SVG loading with PySide6 6.8.3

### qtdeclarative
* [QTBUG-136688](https://bugreports.qt.io/browse/QTBUG-136688) QJSEngine: call eval() directly from C++ crash
application
* [QTBUG-136598](https://bugreports.qt.io/browse/QTBUG-136598) Item::enabled behaves inconsistently with docs on Qt 6
* [QTBUG-30801](https://bugreports.qt.io/browse/QTBUG-30801) Button: tooltip not shown when the button is disabled
* [QTBUG-138871](https://bugreports.qt.io/browse/QTBUG-138871) ASSERT: QColorOutput::colorify: "It makes no sense to
attempt to print an empty string."
* [QTBUG-136355](https://bugreports.qt.io/browse/QTBUG-136355) Disabling qml-locale can segfault qmltc
* [QTBUG-104829](https://bugreports.qt.io/browse/QTBUG-104829) QML TextArea doesn't trigger onCursorPositionChanged
when deleting whole word
* [QTBUG-136566](https://bugreports.qt.io/browse/QTBUG-136566) Qml Structured Value does not work with qml arrays
* [QTBUG-138478](https://bugreports.qt.io/browse/QTBUG-138478) TapHandler doesn't react to touch input inside popup
background
* [QTBUG-133247](https://bugreports.qt.io/browse/QTBUG-133247) Fill not correctly rendered by curve renderer
* [QTBUG-138927](https://bugreports.qt.io/browse/QTBUG-138927) Incubator crashing when being destroyed
* [QTBUG-138490](https://bugreports.qt.io/browse/QTBUG-138490) Incorrect item ordering in QML container when the
ListView is nested within another Item.
* [QTBUG-123988](https://bugreports.qt.io/browse/QTBUG-123988) QSGGeometryData::hasDirtyIndexData() implementation uses
wrong member variable
* [QTBUG-123985](https://bugreports.qt.io/browse/QTBUG-123985) PinchHandler works unreliably with Wayland
* [QTBUG-138516](https://bugreports.qt.io/browse/QTBUG-138516) [Reg 6.8 -> 6.9] QML: compiler: methods crash in
(nested) QQmlPrivate::callArrowFunction
* [QTBUG-138028](https://bugreports.qt.io/browse/QTBUG-138028) TextField with placeholder text strange behavior with
Binding
* [QTBUG-94251](https://bugreports.qt.io/browse/QTBUG-94251) tst_QQuickPopup fails with OpenSUSE 15.3
* [QTBUG-78261](https://bugreports.qt.io/browse/QTBUG-78261) tst_focus::policy is failing
* [QTBUG-139104](https://bugreports.qt.io/browse/QTBUG-139104) qmlls crash when opening a qmltypes file
* [QTBUG-78162](https://bugreports.qt.io/browse/QTBUG-78162) tst_qquicktextinput::mouseSelectionMode() is flaky on
OpenSuse 15.0
* [QTBUG-139304](https://bugreports.qt.io/browse/QTBUG-139304) QML text with heading role is not read by screenreader
* [QTBUG-139583](https://bugreports.qt.io/browse/QTBUG-139583) FAIL!  : tst_QQuickApplicationWindow::layout()
* [QTBUG-139309](https://bugreports.qt.io/browse/QTBUG-139309) REG: Material Slider's hovered effects visible when they
shouldn't be
* [QTBUG-137160](https://bugreports.qt.io/browse/QTBUG-137160) qt quick Loader active=false with unfinished Menu crash
* [QTBUG-139552](https://bugreports.qt.io/browse/QTBUG-139552) tst_qquickmenu: Test case loadMenuAsynchronously fails
due to warning
* [QTBUG-139306](https://bugreports.qt.io/browse/QTBUG-139306) Popup inside an async Loader crashes Qt Quick app if
there is direct property binding (possible racing condition)
* [QTBUG-139626](https://bugreports.qt.io/browse/QTBUG-139626) AOT-compiled code crashes when accessing members of
QList<QVariantMap>
* [QTBUG-129972](https://bugreports.qt.io/browse/QTBUG-129972) [REG 6.6 → 6.7] Array returned to QML from CPP is not
retaining changes made in QML/JS
* [QTBUG-139025](https://bugreports.qt.io/browse/QTBUG-139025) [Reg 6.5.9 -> 6.8.4] Lists of objects with
JavaScriptOwnership, stored in var properties, are no longer destroyed
* [QTBUG-139059](https://bugreports.qt.io/browse/QTBUG-139059) Generated code does not track objects on JavaScript
stack
* [QTBUG-138919](https://bugreports.qt.io/browse/QTBUG-138919) [Reg 6.5.9 -> 6.8.4] Unreferenced objects with
JavaScriptOwnership are no longer destroyed
* [QTBUG-138886](https://bugreports.qt.io/browse/QTBUG-138886) Improve "once-off assignment" wording in QML
PropertyChanges documentation
* [QTBUG-134292](https://bugreports.qt.io/browse/QTBUG-134292) ODR warnings with static build
* [QTBUG-135249](https://bugreports.qt.io/browse/QTBUG-135249) Popup: Some properties can not be bound
* [QTBUG-139715](https://bugreports.qt.io/browse/QTBUG-139715) TextArea background invisible in Fusion style
* [QTBUG-139764](https://bugreports.qt.io/browse/QTBUG-139764) Inconsistent conversions between QVariantList and
QList<T>
* [QTBUG-140057](https://bugreports.qt.io/browse/QTBUG-140057)  ASSERT: "locals" in file
/Users/qt/work/qt/qtdeclarative/src/qml/memory/qv4mm.cpp, line 1487
* [QTBUG-137172](https://bugreports.qt.io/browse/QTBUG-137172) "section" property in ListView behaviour is broken
(degradation)
* [QTBUG-138104](https://bugreports.qt.io/browse/QTBUG-138104) tst_qtquickview_signallistener crashes on Android
* [QTBUG-140074](https://bugreports.qt.io/browse/QTBUG-140074) Crash in QQmlPrivate::callArrowFunctionAsVariant() when
using qmlcachegen
* [QTBUG-136629](https://bugreports.qt.io/browse/QTBUG-136629) QUnifiedTimer::updateAnimationTimers() crashes when
QApplication is recreated
* [QTBUG-135407](https://bugreports.qt.io/browse/QTBUG-135407) [Scene Graph - Graph App] Segmentation Fault
* [QTBUG-139026](https://bugreports.qt.io/browse/QTBUG-139026) Scrollbar size jumps during drag due to dynamic item
heights
* [QTBUG-139211](https://bugreports.qt.io/browse/QTBUG-139211) tst_qquickpopup (Failed)
* [QTBUG-138947](https://bugreports.qt.io/browse/QTBUG-138947) QProgressBar completely blank on macOS 26
* [QTBUG-138942](https://bugreports.qt.io/browse/QTBUG-138942) Mac style (Widget and Quick) has issues on macOS 26
* [QTBUG-139688](https://bugreports.qt.io/browse/QTBUG-139688) Public Java Classes Documentation Bugs
* [QTBUG-139320](https://bugreports.qt.io/browse/QTBUG-139320) QQ4A - Buffer Overflow crash in application project
* [QTBUG-114718](https://bugreports.qt.io/browse/QTBUG-114718) [Tests] tst_QQuickPopup fails

### qtmultimedia
* [QTBUG-134607](https://bugreports.qt.io/browse/QTBUG-134607) Video playback crash when setting QQuickWindow
GraphicsAPI to Vulkan
* [QTBUG-138414](https://bugreports.qt.io/browse/QTBUG-138414) FFmpeg Plugin: Improve usability on different RHI
backend configurations
* [QTBUG-138952](https://bugreports.qt.io/browse/QTBUG-138952) tst_qaudiosink: start_afterStopAndReset() crashes on
macOS
* [QTBUG-136151](https://bugreports.qt.io/browse/QTBUG-136151) Qt Multimedia: Add alt texts
* [QTBUG-139549](https://bugreports.qt.io/browse/QTBUG-139549) Qt multimedia compilation error windows 32 bit
* [QTBUG-124562](https://bugreports.qt.io/browse/QTBUG-124562) Exposure compensation (setExposureCompensation) doesn't
work with the example app
* [QTBUG-138590](https://bugreports.qt.io/browse/QTBUG-138590) Incorrect Call to QAudioOutput::setVolume
* [QTBUG-139773](https://bugreports.qt.io/browse/QTBUG-139773) Crash in MediaPlayer in qtdice demo
* [QTBUG-139681](https://bugreports.qt.io/browse/QTBUG-139681) Camera widgets record button crashes application on
linux
* [QTBUG-140431](https://bugreports.qt.io/browse/QTBUG-140431) apalis-imx6: media Player example fails to play video
* [QTBUG-139660](https://bugreports.qt.io/browse/QTBUG-139660) QTextToSpeech WinRT backend stops speaking after the
first word in Qt 6.9.2
* [QTBUG-140122](https://bugreports.qt.io/browse/QTBUG-140122) Background Color Difference During Video Playback
Between Windows Media Player and Qt Media Player Example

### qttools
* [QTBUG-139057](https://bugreports.qt.io/browse/QTBUG-139057) Doc: Show correct signature for qDebug() , qInfo() ...
macros
* [QTBUG-138887](https://bugreports.qt.io/browse/QTBUG-138887) [REG 5.13 → 5.14] \overload lastIndexOf() in qstring.cpp
renders lastIndexOf() as a non-link
* [QTBUG-69756](https://bugreports.qt.io/browse/QTBUG-69756) QDoc: Parentheses in link text causes premature link end
anchor
* [QTBUG-86490](https://bugreports.qt.io/browse/QTBUG-86490) Generated documentation for change signals that represent
more than one property is hard to read
* [QTBUG-137569](https://bugreports.qt.io/browse/QTBUG-137569) make qttools configure more user friendly on windows
* [QTBUG-139614](https://bugreports.qt.io/browse/QTBUG-139614) QDoc: Index files do not record the declared return type
* [QTBUG-139407](https://bugreports.qt.io/browse/QTBUG-139407) QDoc fails to build with LLVM >= 21
* [QTBUG-140378](https://bugreports.qt.io/browse/QTBUG-140378) lupdate fails to compile with LLVM 21 due to removed
FileManager::getFile() API
* [QTBUG-110696](https://bugreports.qt.io/browse/QTBUG-110696) Qt6CoreMacros.cmake should take AUTOGEN_BUILD_DIR into
account

### qtdoc
* [QTBUG-135377](https://bugreports.qt.io/browse/QTBUG-135377) The Qt Wayland platform plugin is missing from the
documentation.
* [QTBUG-137296](https://bugreports.qt.io/browse/QTBUG-137296) Clarifications to "Qt for Android - Building from
Source" page based on customer feedback.
* [QTBUG-136065](https://bugreports.qt.io/browse/QTBUG-136065) Installer command does not work
* [QTBUG-138676](https://bugreports.qt.io/browse/QTBUG-138676) Coffee machine examples images not getting current
values fom slider
* [QTTA-450](https://bugreports.qt.io/browse/QTTA-450) QtJenny Example fails to build with
'QtCore/private/qandroidextras_p.h' file not found
* [QTBUG-136334](https://bugreports.qt.io/browse/QTBUG-136334) The documentation of qt6_add_lightprobe_images is
missing
* [QTBUG-140051](https://bugreports.qt.io/browse/QTBUG-140051) Cosmetic facelift for QtJenny Demo
* [QTBUG-137076](https://bugreports.qt.io/browse/QTBUG-137076) Fix qmllint warnings for Calqlatr example

### qtqa
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-134408](https://bugreports.qt.io/browse/QTBUG-134408) Update Vale linting config and vocabularies

### qtpositioning
* [QTBUG-139654](https://bugreports.qt.io/browse/QTBUG-139654) Update QtPositioning documentation to use QDoc commands
* [QTBUG-139780](https://bugreports.qt.io/browse/QTBUG-139780) Qt Positioning: Discrepancy between documented type
names and actual type names
* [QTBUG-139560](https://bugreports.qt.io/browse/QTBUG-139560) Access functions are documented even when their
properties are not

### qtconnectivity
* [QTBUG-139280](https://bugreports.qt.io/browse/QTBUG-139280) Cannot build QT 6.8 without GNU extensions

### qtwayland
* [QTBUG-139250](https://bugreports.qt.io/browse/QTBUG-139250) Top-level tool window doesnt oppen
* [QTBUG-135354](https://bugreports.qt.io/browse/QTBUG-135354) wayland\custom-extension and wayland\custom-shell
examples fails to build with Boot to Qt on Windows

### qt3d
* [QTBUG-139978](https://bugreports.qt.io/browse/QTBUG-139978) qt3d fails on documentation-warnings
* [QTBUG-138670](https://bugreports.qt.io/browse/QTBUG-138670) Doc: Scene3D QML type is missed at Qt 3D Scene3D Module

### qtserialport
* [QTBUG-138643](https://bugreports.qt.io/browse/QTBUG-138643) Details missing for some USB serialport adapters

### qtwebengine
* [QTBUG-138641](https://bugreports.qt.io/browse/QTBUG-138641) QtWebEngine rendering glitches with %lt;select%gt; element
* [QTBUG-135100](https://bugreports.qt.io/browse/QTBUG-135100) QtPdf doc - broken link & missing information
* [QTBUG-139322](https://bugreports.qt.io/browse/QTBUG-139322) fail to install to staging dir
* [QTBUG-138881](https://bugreports.qt.io/browse/QTBUG-138881) Windows Debug: QQuickWebEngineScriptCollection crashes
after adding custom library path
* [QTBUG-139624](https://bugreports.qt.io/browse/QTBUG-139624) Make qdoc to understand qml list types with lower case
* [QTBUG-139766](https://bugreports.qt.io/browse/QTBUG-139766) [Windows] Linker isn't able to create pdb file for
Qt6WebEngineCore
* [QTBUG-136257](https://bugreports.qt.io/browse/QTBUG-136257) QtWebEngine based browser shows nothing with panthor
driver
* [QTBUG-138589](https://bugreports.qt.io/browse/QTBUG-138589) Quick Nano Browser has qmllint warnings

### qtvirtualkeyboard
* [QTBUG-138693](https://bugreports.qt.io/browse/QTBUG-138693) Doc: VirtualKeyboardSetting QML Type is missed at Qt
Virtual Keyboard QML Types
* [QTBUG-138921](https://bugreports.qt.io/browse/QTBUG-138921) Virtual Keyboard plugin missing or fails to load in Qt
6.9.1
* [QTBUG-137923](https://bugreports.qt.io/browse/QTBUG-137923) [Reg 6.8.3->6.9.0] Virtual keyboard is totally broken
because it depends on Qt MultiMedia
* [QTBUG-124178](https://bugreports.qt.io/browse/QTBUG-124178) Virtualkeyboard of Qt 5.15.15 crash on Ubuntu
* [QTBUG-138888](https://bugreports.qt.io/browse/QTBUG-138888) Japanese layout cannot input Kanji characters in many
cases
* [QTBUG-126402](https://bugreports.qt.io/browse/QTBUG-126402) QML virtual keyboard behavior regression between 5.x and
6.x
* [QTBUG-137731](https://bugreports.qt.io/browse/QTBUG-137731) Shadow Input is not properly displayed with
DesktopInputPanel with fullScreenMode = true
* [QTBUG-135022](https://bugreports.qt.io/browse/QTBUG-135022) FAIL!  : inputpanel::tst_plugin::test_themeChange()
Received a fatal error
* [QTBUG-137921](https://bugreports.qt.io/browse/QTBUG-137921) [Reg 6.8.3->6.9.0] Desktop virtual keyboard cannot find
InputPanel.qml and freezes the application
* [QTBUG-137250](https://bugreports.qt.io/browse/QTBUG-137250) REG->6.9.0: VirtualKeyboard not working (Linux)

### qtspeech
* [QTBUG-139660](https://bugreports.qt.io/browse/QTBUG-139660) QTextToSpeech WinRT backend stops speaking after the
first word in Qt 6.9.2
* [QTBUG-108205](https://bugreports.qt.io/browse/QTBUG-108205) tst_QTextToSpeech::pauseResume(darwin) fails on macOS 13
in CI

### qtnetworkauth
* [QTBUG-135353](https://bugreports.qt.io/browse/QTBUG-135353) Doc: Edit Qt Network Authorization documentation

### qtremoteobjects
* [QTBUG-139754](https://bugreports.qt.io/browse/QTBUG-139754) FAIL!  : tst_clientSSL::testRun()
'socketClient->waitForEncrypted(-1)' returned FALSE
* [PYSIDE-3179](https://bugreports.qt.io/browse/PYSIDE-3179) REG->6.11.0: QtRemoteObjects/integration_test.py (and
other RO tests) assert/fail
* [QTBUG-139845](https://bugreports.qt.io/browse/QTBUG-139845) Reg->6.11: Assert when passing a too long-list to
QMetaMethodBuilder::setParameterNames()

### qtquick3d
* [QTBUG-136137](https://bugreports.qt.io/browse/QTBUG-136137) License of
qtquick3d/src/runtimerender/res/effectlib/fog.glsllib: SPDX header
differs from qt_attribution
* [QTBUG-138245](https://bugreports.qt.io/browse/QTBUG-138245) FTBFS: qtquick3d's embree 3rd-party
* [QTBUG-139232](https://bugreports.qt.io/browse/QTBUG-139232) Crash when View3D is destroyed in a multiview case
* [QTBUG-136911](https://bugreports.qt.io/browse/QTBUG-136911) 2D items take transformation from random camera if there
are multiple View3Ds into a single scene
* [QTBUG-126098](https://bugreports.qt.io/browse/QTBUG-126098) Item2D uses wrong transformation in multiple views
* [QTBUG-139130](https://bugreports.qt.io/browse/QTBUG-139130) Nested View3D causes 2D content to not be rendered
* [QTBUG-139274](https://bugreports.qt.io/browse/QTBUG-139274) Loader3D and ComponentBehaviour Bound seem incompatible

### qtcoap
* [QTBUG-139697](https://bugreports.qt.io/browse/QTBUG-139697) Provide a public "bind" API for QCoapClient, or at least
filter out unexpected replies not from peer

### qtgrpc
* [QTBUG-138494](https://bugreports.qt.io/browse/QTBUG-138494) GRPC, QHttp2Channel: Implement metadata handling
according to protocol
* [QTBUG-129160](https://bugreports.qt.io/browse/QTBUG-129160) QtGrpc: improve lifetime-management of Http2Handler
* [QTBUG-138683](https://bugreports.qt.io/browse/QTBUG-138683) Protobuf: repeated enum fields are serialized
incorrectly
* [QTBUG-139597](https://bugreports.qt.io/browse/QTBUG-139597) QtGrpc: QGrpcHttp2Channel should guarantee
transportation scheme
* [QTBUG-138812](https://bugreports.qt.io/browse/QTBUG-138812) Doc: Improve security documentation of Qt GRPC

### qtgraphs
* [QTBUG-138506](https://bugreports.qt.io/browse/QTBUG-138506) QtGraphs crash when GraphView is destroyed
* [QTBUG-134003](https://bugreports.qt.io/browse/QTBUG-134003) QtGraphs pieSize and holeSize validate and render
differently
* [QTBUG-138923](https://bugreports.qt.io/browse/QTBUG-138923) Gradient range doesn't update with aspectRatio
* [QTBUG-138924](https://bugreports.qt.io/browse/QTBUG-138924) Gradient does not work when starting up the app in some
cases
* [QTBUG-138822](https://bugreports.qt.io/browse/QTBUG-138822) Reusing same ValueAxis in multiple GraphViews results in
a crash
* [QTBUG-139112](https://bugreports.qt.io/browse/QTBUG-139112) QtGraphs AreaSeries inconsistent area filling
* [QTBUG-138797](https://bugreports.qt.io/browse/QTBUG-138797) Docs are messed up with * in some places

### qmlcompilerplus (Commercial only)
* [QTBUG-139431](https://bugreports.qt.io/browse/QTBUG-139431) Miscompilation of lists of inline components

### qtinsighttracker (Commercial only)
* [QTBUG-140160](https://bugreports.qt.io/browse/QTBUG-140160) FAIL!  : tst_QInsightEventFilter::trackEvents(button.ui)
Compared values are not the same

Known Issues
------------
* Check that your system meets Qt's requirements:
  https://doc.qt.io/qt-6.9/supported-platforms.html
* RTA reported issues from Qt 6.9
  https://bugreports.qt.io/issues/?filter=27175
* See Qt 6.9 known issues from:
  https://wiki.qt.io/Qt_6.9_Known_Issues
* Qt 6.9.3 Open issues in Jira:
  https://bugreports.qt.io/issues/?filter=27925

Credits for the  release goes to:
---------------------------------

Eirik Aavitsland  
Laszlo Agocs  
Konsta Alajärvi  
Even Oscar Andersen  
Soheil Armin  
Albert Astals Cid  
Nicholas Bennett  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
David Boddie  
Tatiana Borisova  
Assam Boudjelthia  
Marcell Brauner  
Aurélien Brooke  
Kai Uwe Broulik  
Michael Brüning  
Olivier De Cannière  
Alexei Cazacov  
Kaloyan Chehlarski  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Szabolcs David  
Pavel Dubsky  
Artem Dyomin  
Alexey Edelev  
Oliver Eftevaag  
Christian Ehrlicher  
Andreas Eliasson  
Nicolas Fella  
Joshua GPBeta  
Marcus Gama  
Julian Greilich  
Robert Griebl  
Richard Moe Gustavsen  
Lucie Gérard  
Mikko Hallamaa  
Jani Heikkinen  
Tero Heikkinen  
Moss Heim  
Ulf Hermann  
Volker Hilsheimer  
Dominik Holland  
Samuli Hölttä  
Morteza Jamshidi  
Allan Sandfeld Jensen  
Igor Khanin  
Ahmed El Khazari  
Ali Kianian  
Friedemann Kleint  
André Klitzing  
Michal Klocek  
Jarek Kobus  
Jarkko Koivikko  
Tomi Korpipaa  
Jani Korteniemi  
Fabian Kosmale  
Mike Krus  
Santhosh Kumar  
Kai Köhne  
Antonio Larrosa  
Inho Lee  
Frédéric Lefebvre  
Wladimir Leuschner  
Robert Löhning  
Thiago Macieira  
Leena Miettinen  
Jan Moeller  
Safiyyah Moosa  
Marc Mutz  
Andy Nichols  
Markku Nokkala  
Mårten Nordheim  
Dennis Oberst  
Kwanghyo Park  
Jerome Pasion  
Karim Pinter  
Timur Pocheptsov  
Joni Poikelin  
Jacek Poplawski  
Rami Potinkara  
Lorn Potter  
Sakaria Pouke  
Dheerendra Purohit  
Khem Raj  
Matthias Rauter  
Topi Reinio  
Bernhard Rosenkränzer  
Shawn Rutledge  
Ahmad Samir  
Timon Sassor  
Lars Schmertmann  
Sami Shalayel  
Nils Petter Skålerud  
Nils Peter Skålerud  
Ivan Solovev  
Christian Strømme  
Tarja Sundqvist  
Lars Sutterud  
Tasuku Suzuki  
Morten Sørvig  
Sami Varanka  
Peter Varga  
BogDan Vatra  
Bror Wetlesen Vedeld  
Doris Verria  
Tor Arne Vestbø  
Petri Virkkunen  
Ville Voutilainen  
Juha Vuolle  
Jaishree Vyas  
Jannis Völker  
Edward Welbourne  
Paul Wicking  
Piotr Wiercinski  
Oliver Wolff  
Semih Yavuz  
Zhao Yuhang  
