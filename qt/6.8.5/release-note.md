Release note
============
Qt 6.8.5 release is a patch release made on the top of Qt 6.8.4.
As a patch release, Qt 6.8.5 does not add any new functionality but provides
bug fixes and other improvements and maintains both forward and backward
compatibility (source and binary) with Qt 6.8.4.

For detailed information about Qt 6.8, refer to the online documentation
included in this distribution. The documentation is also available online:

https://doc.qt.io/qt-6/index.html

The Qt version 6.8 series is binary compatible with the 6.7.x series.
Applications compiled for 6.7 will continue to run with 6.8.

Some of the changes listed in this file include issue tracking numbers
corresponding to tasks in the Qt Bug Tracker:

https://qt-project.atlassian.net/

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

* [CVE-2025-10728](https://nvd.nist.gov/vuln/detail/CVE-2025-10728) in qtsvg
* [CVE-2025-10729](https://nvd.nist.gov/vuln/detail/CVE-2025-10729) in qtsvg

### qtbase
* 03404c4dbb7 QWeakPointer: don't let IfCompatible<X> make accidental
  SMFs
    * Fixed a regression whereby the QWeakPointer<T> copy or move
      constructors and/or assignment operators may fail to compile for
      forward-declared (incomplete) T.

* d63152f26de Update bundled libpng to version 1.6.50
    * libpng was updated to version 1.6.50

* faaa7491a41 QTextStream: cope with multi-code-point signs
    * Fixed QTextStream::FieldAlignment::AlignAccountingStyle for
      locales that have negativeSign/positiveSign (-/+) that take more
      than one UTF-16 code point (e.g. ar (Arabic)).

* 1d236b86674 QLocale: fix off-by-one error in codeToScript()
    * Fixed a bug where QLocale could not find the QLocale::Script with
      the highest value when looked up by string (codeToString() or
      QLocale(string) constructor).

* 3e1d40179bb SQLite: Update SQLite to v3.50.3
    * Updated SQLite to v3.50.3

* a1e2dbb5be3 Define macOS QOperatingSystemVersion constants using only
  major version
    * QOperatingSystemVersion constants for macOS 11 and up are now
      represented with their major version only, and minor and patch
      versions unspecified, as documented.

* efeadba3d58 SQLite: Update SQLite to v3.50.4
    * Updated SQLite to v3.50.4

* 91248b1a954 Fix the url construction in the requestUrl method
    * QNetworkRequestFactory::createRequest() doesn't decode the
      provided `path` anymore. If the path string was passed encoded by
      the user, it stays encoded in the particular way.

* fce59b7e05e QDirListing: check for '.' and '..' after the checking the
  name filters
    * Now listing '.' and '..' special entries respects any set name
      filters. Previously if IncludeDotAndDotDot was set, '.' and '..'
      would always be listed.

* 8b241508a22 Upgrade Harfbuzz to 11.3.3
    * Upgraded Harfbuzz to version 11.3.3.

* 22c585c8475 QTest::qWaitFor*: capture the widget/window using QPointer
    * Fixed a bug that would cause the qWaitForWindow* and
      qWaitForWidget* functions to crash or misbehave if the window or
      widget they were told to wait on was destroyed in the process of
      waiting for it to be shown/focused/activated/exposed.

* c74308d0f0a qvsnprintf: fail if the result size doesn't fit into an
  int
    * Fixed a bug that would cause q(v)snprintf() to report success on
      some platforms, even though the result was truncated.

* f8d51166092 Upgrade Harfbuzz to 11.4.1
    * Upgraded Harfbuzz to version 11.4.1.

* 48c97f1a67c Android: Set name-matched class names for Slider and
  ScrollBar for TalkBack
    * Use different Android class names for Slider and Scroller.

* 72d41f87818 Android: Use the TalkBack focus signal to trigger
  focusAction
    * Use TalkBack ACTION_ACCESSIBILITY_FOCUS to trigger focusAction.

* 9431f48e9a3 QJsonDocument/Value: fix integer truncation in
  fromJson(QByteArray)
    * Fixed a bug on 64-bit platforms where fromJson(QByteArray) could
      report one of the Unterminated errors for valid input whose size
      merely exceeded INT_MAX (2GiB).

* 349e5c29eb3 moveToTrash/XDG: allow $XDG_DATA_HOME/Trash to be a
  symlink
    * Fixed a bug that caused moveToTrash() to disallow trashing to
      trash bins using the XDG Trash Specification when the trash path
      was a symlink.

* 5afd6d35cbb Upgrade PCRE2 to 10.46
    * PCRE2 was updated to version 10.46.

* 3a008994249 Suppress construction of QTimeZone(Qt::TimeSpec)
    * Construction from a Qt::TimeSpec, which was never meant to be
      supported, is now rejected at compile time, where previously
      compilers (mis)interpreted the enum as an int so called the (int
      offsetSeconds) constructor, with results consistently at odds with
      what the user presumably expected.

* 6728b198d42 QFileSystemEngine/BSD: check UF_HIDDEN on the symlink only
    * Fixed a bug that caused isHidden() to return true on BSDs and
      Apple OSes for non-hidden symlinks that pointed to hidden targets.

* a6cf81f45b6 Respect QT_NO_INT128 in qtypes.cpp's #error
    * Made it possible to compile Qt with GCC in strict C++ mode (-ansi
      or -std=c++NN) again, provided QT_NO_INT128 is defined, too.

* 3f9ac1cbdb0 Add camel-case header for qtconcurrenttask.h
    * Added a camel-case QtConcurrentTask header, which is the same as
      QtConcurrent/qtconcurrenttask.h.

* 59ce1deaa18 Doc: Classify 3rd party code in cmake as tools
    * Reclassify third-party components "KWin" and "extra-cmake-modules"
      as tools related.

* 6b9e5e25ae0 Upgrade Harfbuzz to 11.4.5
    * Upgraded Harfbuzz to version 11.4.5.

* f202e2c9f62 Update bundled libjpeg-turbo to version 3.1.2
    * libjpeg-turbo was updated to version 3.1.1

* a360eb7664f QStringConverter: allow appendToBuffer() to write to the
  buffer
    * The appendToBuffer() functions in QStringEncoder and
      QStringDecoder may write to parts of the provided output beyond
      the returned pointer. Caller code must not assume the data beyond
      that remains unmodified.

* b4ad8c4b091 Update Freetype to 2.14.0
    * Updated bundled Freetype to 2.14.0.

* 863d40a9e95 Make QTEST_THROW_ON_FAIL work from within QtConcurrent
    * Fixed a bug which prevented QTEST_THROW_ON_FAIL and
      QTEST_THROW_ON_SKIP from working with QCOMPARE(), QVERIFY(), and
      QSKIP() invoked from within QtConcurrent functions.

* 10c4e056286 Upgrade Harfbuzz to 11.5.0
    * Upgraded Harfbuzz to version 11.5.0.

* b52dbf3e2b1 Update Freetype to 2.14.1
    * Updated bundled Freetype to 2.14.1.

* 7c185e7a17a Upgrade Harfbuzz to 11.5.1
    * Upgraded Harfbuzz to version 11.5.1.

* cb8d7269e88 Upgrade Harfbuzz to 12.1.0
    * Upgraded Harfbuzz to version 12.1.0.

### qtsvg
* ee5c5744 Replace check for endless recursion when loading
    * Fix stack overflow when an element references its child element
      using url()

### qt3d
* a554f6a18 Update assimp dependency
    * Update ASSIMP to 6.0.2

### qtimageformats
* d1347666 Update bundled libwebp to version 1.6.0
    * Update bundled libwebp to version 1.6.0

* 38ff5b61 Update bundled libtiff to version 4.7.1
    * Bundled libtiff was updated to version 4.7.1

### qtgrpc
* 9e1e19a8 Emit cancelled finished() in channel implementation
    * Cancellation logic should also emit finished now. Custom
      QAbstractGrpcChannel implementations should adapt their logic.

* 42259e5f QGrpcHttp2Channel: Guarantee transportation scheme
    * Requesting TLS or QLocalSocket now fails with a fatal error if the
      requested transport is unavailable.


Fixes
-----

### qtbase
* [QTBUG-137438](https://qt-project.atlassian.net/browse/QTBUG-137438) [REG 6.9.0 -> 6.9.1] QTemporaryFile
* [QTBUG-129242](https://qt-project.atlassian.net/browse/QTBUG-129242) QTableWidget selection issue
* [QTBUG-137776](https://qt-project.atlassian.net/browse/QTBUG-137776) Windows11 style, QTableView cell selection behavior
* [QTBUG-132590](https://qt-project.atlassian.net/browse/QTBUG-132590) Unclear relation between
QTemporaryFile::{autoRemove,rename}()
* [QTBUG-128794](https://qt-project.atlassian.net/browse/QTBUG-128794) QLineEdit in Android - no text visual
* [QTBUG-133549](https://qt-project.atlassian.net/browse/QTBUG-133549) Qt UI stops redrawing on Android
* [QTBUG-128457](https://qt-project.atlassian.net/browse/QTBUG-128457) QSpinBox does not respond correctly to Android keyboard
* [QTBUG-128422](https://qt-project.atlassian.net/browse/QTBUG-128422) [Android] Can't change selection in QComboBox with touch
input
* [QTBUG-121757](https://qt-project.atlassian.net/browse/QTBUG-121757) Entered text is invisible in QLineEdit until field focus
is changed
* [QTBUG-138261](https://qt-project.atlassian.net/browse/QTBUG-138261) QPlatformBackingStore doesn't handle QtGui-level
fractional scaling
* [QTBUG-138158](https://qt-project.atlassian.net/browse/QTBUG-138158) QT_DISCARD_FILE_CONTENTS does not work as expected
* [QTBUG-137120](https://qt-project.atlassian.net/browse/QTBUG-137120) [Regression] Right and top dockwidget area are not
resizable anymore
* [QTBUG-138183](https://qt-project.atlassian.net/browse/QTBUG-138183) The drop area for QToolBar gets triggered even when the
toolbar is not on the window.
* [QTBUG-133845](https://qt-project.atlassian.net/browse/QTBUG-133845)  QSpinBoxes take too much vertical space if an
application-wide style sheet is set since Qt 6.8.2
* [QTBUG-130642](https://qt-project.atlassian.net/browse/QTBUG-130642) Incorrect QAbstractSpinBox size hint in Windows 11 style
when style sheet is set
* [QTBUG-132431](https://qt-project.atlassian.net/browse/QTBUG-132431) Stylesheet Margin/Padding squashes QSpinBox
* [QTBUG-138428](https://qt-project.atlassian.net/browse/QTBUG-138428) tst_QTextStream::pos3LargeFile() takes an extraordinary
amount of time to execute
* [QTBUG-138435](https://qt-project.atlassian.net/browse/QTBUG-138435) QTextStream::pos() seems to be linear over QFile size
(or QFile::pos())
* [QTBUG-135928](https://qt-project.atlassian.net/browse/QTBUG-135928) Connection to D-Bus signals silently breaks if D-Bus was
used before creating QCoreApplication
* [QTBUG-138401](https://qt-project.atlassian.net/browse/QTBUG-138401) [REG dev] Windows11 Style: Check-boxes' drawing
regression
* [QTBUG-138094](https://qt-project.atlassian.net/browse/QTBUG-138094) Radiobuttons/Checkboxes in windows11 style do not follow
WinUI3 style
* [QTBUG-138238](https://qt-project.atlassian.net/browse/QTBUG-138238) NPE when calling QtNetwork.unregisterReceiver() at exit
* [QTBUG-137027](https://qt-project.atlassian.net/browse/QTBUG-137027) GetMethodID received NULL jclass
* [QTBUG-136130](https://qt-project.atlassian.net/browse/QTBUG-136130) background color of QTreeViewItems with windows 11 style
* [QTBUG-137986](https://qt-project.atlassian.net/browse/QTBUG-137986) rhi/vulkan: Do something about VUID-vkQueueSubmit-
pSignalSemaphores-00067
* [QTBUG-138484](https://qt-project.atlassian.net/browse/QTBUG-138484) QTextStream assumes single-character
QLocale::{positive,negative}Sign()
* [QTBUG-138206](https://qt-project.atlassian.net/browse/QTBUG-138206) a11y: Docked QDockWidget reports incorrect role and
window-relative position via AT-SPI
* [QTBUG-138566](https://qt-project.atlassian.net/browse/QTBUG-138566) QLocale::codeToScript() can't find QLocale::LastScript
* [QTBUG-137587](https://qt-project.atlassian.net/browse/QTBUG-137587) qtdeclarative: do_compile failed when building with high
parallelism.
* [QTBUG-133725](https://qt-project.atlassian.net/browse/QTBUG-133725) qml_tool_autogen target loses almost all dependencies on
other autogen and sync_headers targets
* [QTBUG-134757](https://qt-project.atlassian.net/browse/QTBUG-134757) [REG 6.7.3->6.8.0] QWidgetAction: No contextMenuEvent
* [QTBUG-136217](https://qt-project.atlassian.net/browse/QTBUG-136217) Windows11 style does not show underlying content of
index widget.
* [QTBUG-119501](https://qt-project.atlassian.net/browse/QTBUG-119501) Numbers colliding and not highlighted in Charts with
Widgets Gallery example
* [QTBUG-136163](https://qt-project.atlassian.net/browse/QTBUG-136163) sbom/spdx file not reproducible (contains build path)
* [QTBUG-138660](https://qt-project.atlassian.net/browse/QTBUG-138660) QHttp2Stream: dtor missing sendRST_STREAM for some
state(s)
* [QTBUG-138156](https://qt-project.atlassian.net/browse/QTBUG-138156) tst_QHttpServer::disconnectedInEventLoop leaves a bad
state making multipleRequests fail
* [QTBUG-138043](https://qt-project.atlassian.net/browse/QTBUG-138043) QMultiMap documentation error
* [QTBUG-134740](https://qt-project.atlassian.net/browse/QTBUG-134740) [REG 6.7.3 -> 6.8.0] QDir::entryInfoList slower
accessing SMB share from macOS
* [QTBUG-138374](https://qt-project.atlassian.net/browse/QTBUG-138374) QFileSystemWatcher::addPath() is slow on macos
* [QTBUG-137978](https://qt-project.atlassian.net/browse/QTBUG-137978) Qt.inputMethod.visible changes to true in orientation
change on iOS26 beta
* [QTBUG-136138](https://qt-project.atlassian.net/browse/QTBUG-136138) Blank screen in CarPlay Simulator with Qt-based iOS app
due to assertion: "[scene isKindOfClass:UIWindowScene.class]" in
qiosapplicationdelegate.mm
* [QTBUG-138032](https://qt-project.atlassian.net/browse/QTBUG-138032) calqlatr: Example prints 'stale focus object [...],
doing manual update' warnings
* [QTBUG-138256](https://qt-project.atlassian.net/browse/QTBUG-138256) QPlatformInputContext::update() called with stale focus
object
* [QTBUG-129027](https://qt-project.atlassian.net/browse/QTBUG-129027) tst_QStatusBar::QTBUG4334_hiddenOnMaximizedWindow()
failed on Ubuntu 24.04 GNOME X11
* [QTBUG-131448](https://qt-project.atlassian.net/browse/QTBUG-131448) Cannot QMovie::moveToThread
* [QTBUG-138230](https://qt-project.atlassian.net/browse/QTBUG-138230) QCheckBox used as editor in delegate does not display
checkmark when using Windows11 style and no text
* [QTBUG-135213](https://qt-project.atlassian.net/browse/QTBUG-135213) QTreeView creates ghost artifacts when scrolling
* [QTBUG-120254](https://qt-project.atlassian.net/browse/QTBUG-120254) Cell value leaking into other cells when entering new
value
* [QTBUG-106709](https://qt-project.atlassian.net/browse/QTBUG-106709) Application looks too small on an external display with
iPadOS 16.1 on M1 iPad
* [QTBUG-137544](https://qt-project.atlassian.net/browse/QTBUG-137544) QML iPad app window stays black when launched on
external display
* [QTBUG-68865](https://qt-project.atlassian.net/browse/QTBUG-68865) tst_QMenuBar::check_menuPosition autotest fails on Ubuntu
18.04
* [QTBUG-138372](https://qt-project.atlassian.net/browse/QTBUG-138372) QLocalSocket never emits ConnectedState in Linux
* [QTBUG-138864](https://qt-project.atlassian.net/browse/QTBUG-138864) qt-android-runner.py doesn't find package name
* [QTBUG-136629](https://qt-project.atlassian.net/browse/QTBUG-136629) QUnifiedTimer::updateAnimationTimers() crashes when
QApplication is recreated
* [QTBUG-135641](https://qt-project.atlassian.net/browse/QTBUG-135641) QNetworkDiskCache leaks file descriptors
* [QTBUG-138056](https://qt-project.atlassian.net/browse/QTBUG-138056) QSortFilterProxyModel: Crash when changing sourceModel
(QPropertyBindingData / QBindingStorage)
* [QTBUG-138488](https://qt-project.atlassian.net/browse/QTBUG-138488) [iOS] URL handler do not receive data from external apps
via Universal Link
* [QTBUG-138642](https://qt-project.atlassian.net/browse/QTBUG-138642) ODBC possible data loss with 'real' column
* [QTBUG-8963](https://qt-project.atlassian.net/browse/QTBUG-8963) Driver for ODBC - qsql_odbc.cpp should use the
QMetaType:float when sql type is SQL_FLOAT instead of QVariant::Double
* [QTBUG-138013](https://qt-project.atlassian.net/browse/QTBUG-138013) Content_uri test fails on Pixel6a Device
* [QTBUG-126531](https://qt-project.atlassian.net/browse/QTBUG-126531) Manual test android_content_uri fails
* [QTBUG-123319](https://qt-project.atlassian.net/browse/QTBUG-123319) android_content_uri test crashes when trying to get size
of nonexistent file.
* [QTBUG-134912](https://qt-project.atlassian.net/browse/QTBUG-134912) Manual test android_content_uri crash on exit
* [QTBUG-110240](https://qt-project.atlassian.net/browse/QTBUG-110240) "Use qtbase/tests/manual/android_content_uri" is not
found on the installation
* [QTBUG-132403](https://qt-project.atlassian.net/browse/QTBUG-132403) manual test android_content_uri fails.
* [QTBUG-129324](https://qt-project.atlassian.net/browse/QTBUG-129324) Don't print exceptions for content file operations that
are supposed to be done under the hood
* [QTBUG-137755](https://qt-project.atlassian.net/browse/QTBUG-137755) Regression: Segfault on closing a program using
QDockWidgets, introduced by ab6f1ad77852a427ae73172ca11dacf876a0cbf7
* [QTBUG-138250](https://qt-project.atlassian.net/browse/QTBUG-138250) Win11 23h2 ARM: QtBase -
tst_QRhi::storageBufferRuntimeSizeGraphics(OpenGL) 'pipeline->create()'
returned FALSE
* [QTBUG-93182](https://qt-project.atlassian.net/browse/QTBUG-93182) Occasional asserts when touch scroll NSEventPhaseEnded is
processed while event in queue indicates momentumPhase has begun
* [QTBUG-138922](https://qt-project.atlassian.net/browse/QTBUG-138922) Consistent Qt caused crash when navigating with Jetpack
Compose
* [QTBUG-124011](https://qt-project.atlassian.net/browse/QTBUG-124011) Android: QFileInfo::isWritable() returns false
erroneously and throws an exception
* [QTBUG-115143](https://qt-project.atlassian.net/browse/QTBUG-115143) Unable to open files under certain conditions on
Android.
* [QTBUG-114979](https://qt-project.atlassian.net/browse/QTBUG-114979) Two issues using content scheme to work with files
* [QTBUG-132490](https://qt-project.atlassian.net/browse/QTBUG-132490) Android and TestNamespace: errors in Qt JNI methods
* [QTBUG-135964](https://qt-project.atlassian.net/browse/QTBUG-135964) Windows theme uses wrong colors if high-contrast mode is
activated
* [QTBUG-138861](https://qt-project.atlassian.net/browse/QTBUG-138861) `QRhiResourceUpdateBatch` leaks memory if submitted via
`beginOffscreenFrame`
* [QTBUG-139211](https://qt-project.atlassian.net/browse/QTBUG-139211) tst_qquickpopup (Failed)
* [QTBUG-100991](https://qt-project.atlassian.net/browse/QTBUG-100991) Some tests crash on Android CI
* [QTBUG-131695](https://qt-project.atlassian.net/browse/QTBUG-131695) tst_qquickpopup tst_QQuickPopup::fadeDimmer is flaky
* [QTBUG-125083](https://qt-project.atlassian.net/browse/QTBUG-125083) [Android] ANRs related to QtNativeInputConnection
* [QTBUG-132695](https://qt-project.atlassian.net/browse/QTBUG-132695) Crash in QGuiApplication::applicationStateChanged() when
quitting app
* [QTBUG-139400](https://qt-project.atlassian.net/browse/QTBUG-139400) Properly manage QtEditText focus and InputConnection
callbacks
* [QTBUG-138982](https://qt-project.atlassian.net/browse/QTBUG-138982) qt-android-runner.py fails to start application
* [QTBUG-138622](https://qt-project.atlassian.net/browse/QTBUG-138622) Android launch wrapper script can conflict with qml
subdirectory name on case insensitive file systems
* [QTBUG-138561](https://qt-project.atlassian.net/browse/QTBUG-138561) QFont::exactMatch index out of bounds
* [QTBUG-137769](https://qt-project.atlassian.net/browse/QTBUG-137769) Keyboard is not closed when TextEdit loses focus while
using TalkBack
* [QTBUG-139128](https://qt-project.atlassian.net/browse/QTBUG-139128) QObject::connect(): clarify what a valid method is, in
the string-based overloads
* [QTBUG-119205](https://qt-project.atlassian.net/browse/QTBUG-119205) tst_Android::orientationChange is flaky on android
* [QTBUG-44569](https://qt-project.atlassian.net/browse/QTBUG-44569) QScreen::orientation() does not return actual screen
orientation on android
* [QTBUG-44554](https://qt-project.atlassian.net/browse/QTBUG-44554) QScreen::orientationChanged signal does not work
correctly on android
* [QTBUG-109127](https://qt-project.atlassian.net/browse/QTBUG-109127) QScreen::geometry() not always correct in
orientationChanged() slot
* [QTBUG-35237](https://qt-project.atlassian.net/browse/QTBUG-35237) Can't get "inverted" orientations while rotating android
device.
* [QTBUG-48549](https://qt-project.atlassian.net/browse/QTBUG-48549) Screen's orientation not updated when rotating by 180°
(in one movement) on Android
* [QTBUG-35428](https://qt-project.atlassian.net/browse/QTBUG-35428) In Screen.onOrientationChanged, the previous size is
reported instead of the new one
* [QTBUG-39401](https://qt-project.atlassian.net/browse/QTBUG-39401) QScreen::orientationChanged not fired on Android but
fired on iOS in the same conditions
* [QTBUG-94459](https://qt-project.atlassian.net/browse/QTBUG-94459) Android reports incorrect screen size after rotation
* [QTBUG-138984](https://qt-project.atlassian.net/browse/QTBUG-138984) Possible misinterpretation of
specifications.freedesktop.org/trash-spec
* [QTBUG-138904](https://qt-project.atlassian.net/browse/QTBUG-138904) QIBASE driver fails to build when linking against
Firebird v2.5
* [QTBUG-131513](https://qt-project.atlassian.net/browse/QTBUG-131513) [iOS] QSysInfo::productVersion() incomplete?
* [QTBUG-139600](https://qt-project.atlassian.net/browse/QTBUG-139600) Memory leak on macOS when adding application font from
data
* [QTBUG-139119](https://qt-project.atlassian.net/browse/QTBUG-139119) QFuture::takeResult asserts
* [QTBUG-138946](https://qt-project.atlassian.net/browse/QTBUG-138946) QSlider issues on macOS 26
* [QTBUG-138465](https://qt-project.atlassian.net/browse/QTBUG-138465) Line edits are not visible on macOS 26
* [QTBUG-139360](https://qt-project.atlassian.net/browse/QTBUG-139360) Editable combo box on macOS Tahoe
* [QTBUG-139051](https://qt-project.atlassian.net/browse/QTBUG-139051) Background color of QPlainTextEdit without border
cannont be set on Win11
* [QTBUG-139718](https://qt-project.atlassian.net/browse/QTBUG-139718) [Reg 6.8.3->6.8.4] Transparent windows are rendered with
a black background in full screen mode or while resizing.
* [QTBUG-139733](https://qt-project.atlassian.net/browse/QTBUG-139733) [Regression 6.8.3 -> 6.8.4] A transparent Window cannot
be rendered properly if backend is OpenGL
* [QTBUG-139291](https://qt-project.atlassian.net/browse/QTBUG-139291) showMaximized() does not maximize QDialog
* [QTBUG-138678](https://qt-project.atlassian.net/browse/QTBUG-138678) Crash in QTextEdit while inserting a column into a HTML
table
* [QTBUG-134896](https://qt-project.atlassian.net/browse/QTBUG-134896) QUrl's qHash() is inconsistent with its operator==
* [QTBUG-134900](https://qt-project.atlassian.net/browse/QTBUG-134900) QUrl's operator==() is taking bygone data into account
* [QTBUG-139439](https://qt-project.atlassian.net/browse/QTBUG-139439) CMake fails due to 'pthread_cancel' when configuring Qt
project for Android with CMake 4.x
* [QTBUG-86287](https://qt-project.atlassian.net/browse/QTBUG-86287) Static 5.15.0 compile results in "undefined reference to
xcb_aux_create_gc"
* [QTBUG-137004](https://qt-project.atlassian.net/browse/QTBUG-137004) xcb-image is missing dependency on xcb-aux
* [QTBUG-134082](https://qt-project.atlassian.net/browse/QTBUG-134082) Screen orientation change causes rendering issues on Qt
Quick Application (flicker related)
* [QTBUG-124140](https://qt-project.atlassian.net/browse/QTBUG-124140) [REG]: 6.7.0  full-screen app displays background window
(or splash-screen) graphics at top/bottom during multiwindow split
display
* [QTBUG-139983](https://qt-project.atlassian.net/browse/QTBUG-139983) macOS (Tahoe): assert in
tst_QStyleSheetStyle::complexWidgetFocus()
* [QTBUG-140064](https://qt-project.atlassian.net/browse/QTBUG-140064) error: array subscript 'QTransform[0]' is partly outside
array bounds of 'QVariant [1]'
* [QTBUG-136485](https://qt-project.atlassian.net/browse/QTBUG-136485) QDockWidgets sends visibilityChanged on destruction
* [QTBUG-102020](https://qt-project.atlassian.net/browse/QTBUG-102020) Incorrect layout in QTabBar when last tab is hidden
* [QTBUG-139791](https://qt-project.atlassian.net/browse/QTBUG-139791) Buttons don't work when the last tab is hidden
* [QTBUG-139989](https://qt-project.atlassian.net/browse/QTBUG-139989) FAIL!  : tst_QStateMachine::twoAnimations() Compared
values are not the same
* [QTBUG-138848](https://qt-project.atlassian.net/browse/QTBUG-138848) Content-Length header always sent in HTTP GET request
* [QTBUG-139040](https://qt-project.atlassian.net/browse/QTBUG-139040) Unreadable image on https://doc.qt.io/qt-6/animation-
overview.html
* [QTBUG-139944](https://qt-project.atlassian.net/browse/QTBUG-139944) macOS: title/text alignment on push buttons
* [QTBUG-140126](https://qt-project.atlassian.net/browse/QTBUG-140126) QNetworkReply::errorString shows misleading "server
replied:" with no reason phrase for HTTP/2/3 responses
* [QTBUG-139720](https://qt-project.atlassian.net/browse/QTBUG-139720) Tag errors in QtAbstractItemModel for Java
* [QTBUG-139688](https://qt-project.atlassian.net/browse/QTBUG-139688) [REG 6.9.3 -> 6.10.0] Public Java Classes Documentation
Bugs
* [QTBUG-139765](https://qt-project.atlassian.net/browse/QTBUG-139765) QTEST_THROW_ON_FAIL doesn't work from inside
QtConcurrent
* [QTBUG-139586](https://qt-project.atlassian.net/browse/QTBUG-139586) [Reg 6.9.1->6.9.2] Cannot send broadcast on macOS
anymore
* [QTBUG-138596](https://qt-project.atlassian.net/browse/QTBUG-138596) App fails to build with qmake with static Qt + static
FFmpeg, wrong linker flags
* [QTBUG-140203](https://qt-project.atlassian.net/browse/QTBUG-140203) [qtbase] Build failure with -no-ssl
* [QTBUG-139690](https://qt-project.atlassian.net/browse/QTBUG-139690) [REG 6.9.1 -> 6.9.2] SwipeView Android Expanded Client
Area hides NavigationBar
* [QTBUG-138246](https://qt-project.atlassian.net/browse/QTBUG-138246) Q{Shared,Weak}Pointer::IfCompatible cause accidental
copy/move SMFs, causing FTBFS in qtdeclarative
* [QTBUG-138155](https://qt-project.atlassian.net/browse/QTBUG-138155) qt_generate_deploy_qml_app_script: Error for space in
output name
* [QTBUG-138471](https://qt-project.atlassian.net/browse/QTBUG-138471) QString::arg() convert floating type to integer
* [QTBUG-138192](https://qt-project.atlassian.net/browse/QTBUG-138192) Android Templates, Manifest and CMake Properties
* [QTBUG-135413](https://qt-project.atlassian.net/browse/QTBUG-135413) Accessible.announce not working on iOS and Android
* [QTBUG-138562](https://qt-project.atlassian.net/browse/QTBUG-138562) QLocalePrivate::codeToLanguage() does not sanitize the
input before passing it to AlphaCode
* [QTCREATORBUG-32932](https://qt-project.atlassian.net/browse/QTCREATORBUG-32932) Automatic selection of too low Android SDK version
* [QTBUG-138610](https://qt-project.atlassian.net/browse/QTBUG-138610) QTemporaryFile::rename() overwrites existing file on
Android
* [QTBUG-132617](https://qt-project.atlassian.net/browse/QTBUG-132617) Unclear behaviour of QTemporaryFile::rename()
* [QTBUG-137130](https://qt-project.atlassian.net/browse/QTBUG-137130) Qt Creator crash on exit accessing destroyed event
dispatcher
* [QTBUG-135652](https://qt-project.atlassian.net/browse/QTBUG-135652) Using QIcon from png and svg file in a toolbar with
>100% scaler ratio causes wrong icon size to be picked elsewhere
* [QTBUG-137126](https://qt-project.atlassian.net/browse/QTBUG-137126) QAccessible::ActionChanged event not sent anywhere in Qt
* [QTBUG-138527](https://qt-project.atlassian.net/browse/QTBUG-138527) Replace direct links to https://doc.qt.io/qt-6/
* [QTBUG-136045](https://qt-project.atlassian.net/browse/QTBUG-136045) macOS: Window geometry is not updated correctly when the
OS rejects a change by setGeometry
* [QTBUG-107907](https://qt-project.atlassian.net/browse/QTBUG-107907) QOperatingSystemVersion::Windows10 <
QOperatingSystemVersion::Windows11 == false
* [QTBUG-132398](https://qt-project.atlassian.net/browse/QTBUG-132398) Unsupported linker script to make objective-c classnames
unique is broken since Xcode14
* [QTBUG-138831](https://qt-project.atlassian.net/browse/QTBUG-138831) [VxWorks] EDOOM handling is missing from 6.x
* [QTBUG-134546](https://qt-project.atlassian.net/browse/QTBUG-134546) [VxWorks] exit on poll error should be on by default
like in 5.15
* [QTBUG-138878](https://qt-project.atlassian.net/browse/QTBUG-138878) QNetworkRequestFactory creates an incorrect network
request
* [QTBUG-137860](https://qt-project.atlassian.net/browse/QTBUG-137860) [Windows][A11y] Text can not be selected by NVDA
* [QTBUG-135044](https://qt-project.atlassian.net/browse/QTBUG-135044) tst_QStringApiSymmetry fails under ASAN
(GenerationalCollator is leaked?)
* [QTBUG-134080](https://qt-project.atlassian.net/browse/QTBUG-134080) "QObject::~QObject: Timers cannot be stopped from
another thread" message in Qt 6.8.2 plugins
* [QTBUG-133861](https://qt-project.atlassian.net/browse/QTBUG-133861) [macOS] QML Preview: Closing the preview window produces
QObject::killTimer warning
* [QTBUG-132697](https://qt-project.atlassian.net/browse/QTBUG-132697) FAIL!  :
tst_QQmlDebugJS::setBreakpointInScriptThatQuits(custom)
'm_process->waitForFinished()' returned FALSE.
* [QTBUG-102984](https://qt-project.atlassian.net/browse/QTBUG-102984) QML debugger and profiler tests hangs on macOS/x86_64 in
CI
* [QTBUG-132381](https://qt-project.atlassian.net/browse/QTBUG-132381) [REG 6.8 -> 6.9] Crash when QGuiApplication is static
* [QTBUG-134093](https://qt-project.atlassian.net/browse/QTBUG-134093) Android application crashes on 16 KB page size
* [QTBUG-139055](https://qt-project.atlassian.net/browse/QTBUG-139055) CMake Error at tst_qstatemachineWrapperDebug
* [QTBUG-132211](https://qt-project.atlassian.net/browse/QTBUG-132211) [REG 6.7 -> 6.8][Android] UnsatisfiedLinkError onResume
and onNewIntent
* [QTBUG-120467](https://qt-project.atlassian.net/browse/QTBUG-120467) Link error from Google Play testing
* [QTBUG-70114](https://qt-project.atlassian.net/browse/QTBUG-70114) Java native functions registered with a delay
* [QTBUG-86314](https://qt-project.atlassian.net/browse/QTBUG-86314) Error in 64bit lib file path names
* [QTBUG-139139](https://qt-project.atlassian.net/browse/QTBUG-139139) ubuntu-24.04-x64-developer-build: Part of the build is
using qmake and ignores SCCACHE settings
* [QTBUG-37759](https://qt-project.atlassian.net/browse/QTBUG-37759) QWidget-gestures do not work
* [QTBUG-46195](https://qt-project.atlassian.net/browse/QTBUG-46195) [Windows]: Swipe gesture is not always recognized and
sometimes in the wrong direction
* [QTBUG-123585](https://qt-project.atlassian.net/browse/QTBUG-123585) Memory Leak: QGestureRecognizer::unregisterRecognizer()
* [QTBUG-112898](https://qt-project.atlassian.net/browse/QTBUG-112898) i letter should be İ in uppercase in Turkish
* [QTBUG-136653](https://qt-project.atlassian.net/browse/QTBUG-136653) tst_QAbstractItemView::testDialogAsEditor() crash on
Ubuntu 24.04 x11
* [QTBUG-138583](https://qt-project.atlassian.net/browse/QTBUG-138583) QLocale::toUpper() is not 64-bit-safe on ICU
* [QTBUG-2163](https://qt-project.atlassian.net/browse/QTBUG-2163) Support for conditions in special casing of unicode
characters is missing in Qt
* [QTBUG-139275](https://qt-project.atlassian.net/browse/QTBUG-139275) [a11y] Changes to Accessible.name for focused element
not announced to Screen Reader
* [QTBUG-107028](https://qt-project.atlassian.net/browse/QTBUG-107028) tst_qquicktextfield and tst_qquicktextarea fail on
Android
* [QTBUG-100259](https://qt-project.atlassian.net/browse/QTBUG-100259) tst_controls crash on Android
* [QTBUG-100258](https://qt-project.atlassian.net/browse/QTBUG-100258) tst_focus crashes on Android
* [QTBUG-139415](https://qt-project.atlassian.net/browse/QTBUG-139415) tst_controls has failing test cases
* [QTBUG-138705](https://qt-project.atlassian.net/browse/QTBUG-138705) Windows backend of QLocale::toLower() does not implement
Greek Final Sigma rule
* [QTBUG-138699](https://qt-project.atlassian.net/browse/QTBUG-138699) Square push buttons (macOS 26)
* [QTBUG-139283](https://qt-project.atlassian.net/browse/QTBUG-139283) QInputDevice::availableVirtualGeometry property
incomplete
* [QTBUG-138806](https://qt-project.atlassian.net/browse/QTBUG-138806) [VxWorks] Flickable doesn't work on VxWorks
* [QTBUG-138700](https://qt-project.atlassian.net/browse/QTBUG-138700) Tabs have wrong shape on macOS 26
* [QTBUG-138948](https://qt-project.atlassian.net/browse/QTBUG-138948) Radio button alignment issues on macOS 26
* [QTBUG-138738](https://qt-project.atlassian.net/browse/QTBUG-138738) Incorrect focus ring rendering
* [QTBUG-134627](https://qt-project.atlassian.net/browse/QTBUG-134627) [VxWorks] QTranslator load fails reading from SD card
* [QTBUG-138893](https://qt-project.atlassian.net/browse/QTBUG-138893) QTimeZone(Qt::UTC) returns incorrect UTC offset (+1
second)
* [QTBUG-137564](https://qt-project.atlassian.net/browse/QTBUG-137564) tst_qmovie fails
* [QTBUG-138403](https://qt-project.atlassian.net/browse/QTBUG-138403) QDirIterator → QDirListing should have some porting
documentation
* [QTBUG-139986](https://qt-project.atlassian.net/browse/QTBUG-139986) QStateMachine tests aren't running on the CI
* [QTBUG-139650](https://qt-project.atlassian.net/browse/QTBUG-139650) [VxWorks] touch evdev discovery is missing from 6.8
* [QTBUG-139951](https://qt-project.atlassian.net/browse/QTBUG-139951) [VxWorks] 6.8.4 -> 6.8.5 regression build failure with
VxWorks 24.03
* [QTBUG-139280](https://qt-project.atlassian.net/browse/QTBUG-139280) Cannot build QT 6.8 without GNU extensions
* [QTBUG-138659](https://qt-project.atlassian.net/browse/QTBUG-138659) QTextBoundaryFinder is copyable (deep-copies lookup
tables), but not movable
* [QTBUG-117447](https://qt-project.atlassian.net/browse/QTBUG-117447) Remove *-proxy.html pages in Qt Core
* [QTBUG-139994](https://qt-project.atlassian.net/browse/QTBUG-139994) Nullptr swapchain dereference in
QBackingStoreDefaultCompositor::flush
* [QTBUG-139007](https://qt-project.atlassian.net/browse/QTBUG-139007) QFileSystemEngine::fillMetaData fails on hostfs
* [COIN-1247](https://qt-project.atlassian.net/browse/COIN-1247) Build fails on dependency to qtattributionsscanner: not
found
* [QTBUG-66621](https://qt-project.atlassian.net/browse/QTBUG-66621) webassembly: strings with toUpper() not correct
* [QTBUG-69421](https://qt-project.atlassian.net/browse/QTBUG-69421) WebAssembly: characters are not displayed properly
* [QTBUG-74511](https://qt-project.atlassian.net/browse/QTBUG-74511) Possible REG: Wasm changes in qunicodetables will be lost
* [QTBUG-140211](https://qt-project.atlassian.net/browse/QTBUG-140211) WASM: libQt6Core.a is linked twice

### qtsvg
* [QTBUG-137553](https://qt-project.atlassian.net/browse/QTBUG-137553) [REG 6.8.2 -> 6.8.3] Significant performance regression
in SVG loading with PySide6 6.8.3

### qtdeclarative
* [QTBUG-138174](https://qt-project.atlassian.net/browse/QTBUG-138174) Lightning Viewer: runtime warnings
* [QTBUG-72208](https://qt-project.atlassian.net/browse/QTBUG-72208) Qt.labs.calendar onClicked date is one day off.
* [QTBUG-138200](https://qt-project.atlassian.net/browse/QTBUG-138200) iOS Style: Wrong palette colors when switching color
scheme from application
* [QTBUG-122436](https://qt-project.atlassian.net/browse/QTBUG-122436) Android a11y: Changes to Accessible.ignored and
Item.visible are not propagated to the screen reader
* [QTBUG-136959](https://qt-project.atlassian.net/browse/QTBUG-136959) Read-only TextEdit overrides all Shortcuts when it has
activeFocus
* [QTBUG-134936](https://qt-project.atlassian.net/browse/QTBUG-134936) Improve imperative Menu API documentation
* [QTBUG-138242](https://qt-project.atlassian.net/browse/QTBUG-138242) Crash when GC is triggered during script exception
handling in StateChangeScript or ScriptAction
* [QTBUG-138349](https://qt-project.atlassian.net/browse/QTBUG-138349) QmlPreview does not start with import QtQuick.Controls +
Style=Basic
* [QTBUG-132518](https://qt-project.atlassian.net/browse/QTBUG-132518) building with cmake 3.31 gives ODR violation warnings on
webassembly
* [QTBUG-127133](https://qt-project.atlassian.net/browse/QTBUG-127133) Why do I get warning "Multiple C++ types called xxx
found! This violates the One Definition Rule"
* [QTBUG-134292](https://qt-project.atlassian.net/browse/QTBUG-134292) ODR warnings with static build
* [QTBUG-126193](https://qt-project.atlassian.net/browse/QTBUG-126193) Crash in XR when clicking on Slider in Android Style
* [QTBUG-138559](https://qt-project.atlassian.net/browse/QTBUG-138559) qt_add_qml_module: TARGET dependency causes build
failure
* [QTBUG-136611](https://qt-project.atlassian.net/browse/QTBUG-136611) OpenGL: Layering breaks culling
* [QTBUG-127955](https://qt-project.atlassian.net/browse/QTBUG-127955) Repeater without parent reports its count but does not
create delegates
* [QTBUG-137029](https://qt-project.atlassian.net/browse/QTBUG-137029) Qmllint as process on Windows do not populate error
channel unless called in terminal.
* [QTBUG-138391](https://qt-project.atlassian.net/browse/QTBUG-138391) Deep-nested QML module containing *.mjs file can cause
ambiguous import
* [QTBUG-137860](https://qt-project.atlassian.net/browse/QTBUG-137860) [Windows][A11y] Text can not be selected by NVDA
* [QTBUG-133267](https://qt-project.atlassian.net/browse/QTBUG-133267) Curve renderer does not always show latest version of
path data
* [QTBUG-136355](https://qt-project.atlassian.net/browse/QTBUG-136355) Disabling qml-locale can segfault qmltc
* [QTBUG-136688](https://qt-project.atlassian.net/browse/QTBUG-136688) QJSEngine: call eval() directly from C++ crash
application
* [QTBUG-136566](https://qt-project.atlassian.net/browse/QTBUG-136566) Qml Structured Value does not work with qml arrays
* [QTBUG-138478](https://qt-project.atlassian.net/browse/QTBUG-138478) TapHandler doesn't react to touch input inside popup
background
* [QTBUG-133256](https://qt-project.atlassian.net/browse/QTBUG-133256) Crash on dynamically removing items from a custom
QtQuick.Controls.Container with transitions
* [QTBUG-46798](https://qt-project.atlassian.net/browse/QTBUG-46798) Destroying an item crashes ListView
* [QTBUG-138927](https://qt-project.atlassian.net/browse/QTBUG-138927) Incubator crashing when being destroyed
* [QTBUG-133247](https://qt-project.atlassian.net/browse/QTBUG-133247) Fill not correctly rendered by curve renderer
* [QTBUG-136598](https://qt-project.atlassian.net/browse/QTBUG-136598) Item::enabled behaves inconsistently with docs on Qt 6
* [QTBUG-30801](https://qt-project.atlassian.net/browse/QTBUG-30801) Button: tooltip not shown when the button is disabled
* [QTBUG-138490](https://qt-project.atlassian.net/browse/QTBUG-138490) Incorrect item ordering in QML container when the
ListView is nested within another Item.
* [QTBUG-123988](https://qt-project.atlassian.net/browse/QTBUG-123988) QSGGeometryData::hasDirtyIndexData() implementation uses
wrong member variable
* [QTBUG-138871](https://qt-project.atlassian.net/browse/QTBUG-138871) ASSERT: QColorOutput::colorify: "It makes no sense to
attempt to print an empty string."
* [QTBUG-138028](https://qt-project.atlassian.net/browse/QTBUG-138028) TextField with placeholder text strange behavior with
Binding
* [QTBUG-94251](https://qt-project.atlassian.net/browse/QTBUG-94251) tst_QQuickPopup fails with OpenSUSE 15.3
* [QTBUG-78261](https://qt-project.atlassian.net/browse/QTBUG-78261) tst_focus::policy is failing
* [QTBUG-78162](https://qt-project.atlassian.net/browse/QTBUG-78162) tst_qquicktextinput::mouseSelectionMode() is flaky on
OpenSuse 15.0
* [QTBUG-123985](https://qt-project.atlassian.net/browse/QTBUG-123985) PinchHandler works unreliably with Wayland
* [QTBUG-139309](https://qt-project.atlassian.net/browse/QTBUG-139309) REG: Material Slider's hovered effects visible when they
shouldn't be
* [QTBUG-137160](https://qt-project.atlassian.net/browse/QTBUG-137160) qt quick Loader active=false with unfinished Menu crash
* [QTBUG-139552](https://qt-project.atlassian.net/browse/QTBUG-139552) tst_qquickmenu: Test case loadMenuAsynchronously fails
due to warning
* [QTBUG-139626](https://qt-project.atlassian.net/browse/QTBUG-139626) AOT-compiled code crashes when accessing members of
QList<QVariantMap>
* [QTBUG-139306](https://qt-project.atlassian.net/browse/QTBUG-139306) Popup inside an async Loader crashes Qt Quick app if
there is direct property binding (possible racing condition)
* [QTBUG-135249](https://qt-project.atlassian.net/browse/QTBUG-135249) Popup: Some properties can not be bound
* [QTBUG-133424](https://qt-project.atlassian.net/browse/QTBUG-133424) Named platform icons are blurry on macOS when displayed
with IconImage/IconLabel
* [QTBUG-129972](https://qt-project.atlassian.net/browse/QTBUG-129972) [REG 6.6 → 6.7] Array returned to QML from CPP is not
retaining changes made in QML/JS
* [QTBUG-139025](https://qt-project.atlassian.net/browse/QTBUG-139025) [Reg 6.5.9 -> 6.8.4] Lists of objects with
JavaScriptOwnership, stored in var properties, are no longer destroyed
* [QTBUG-139059](https://qt-project.atlassian.net/browse/QTBUG-139059) Generated code does not track objects on JavaScript
stack
* [QTBUG-138919](https://qt-project.atlassian.net/browse/QTBUG-138919) [Reg 6.5.9 -> 6.8.4] Unreferenced objects with
JavaScriptOwnership are no longer destroyed
* [QTBUG-139764](https://qt-project.atlassian.net/browse/QTBUG-139764) Inconsistent conversions between QVariantList and
QList<T>
* [QTBUG-140057](https://qt-project.atlassian.net/browse/QTBUG-140057)  ASSERT: "locals" in file
/Users/qt/work/qt/qtdeclarative/src/qml/memory/qv4mm.cpp, line 1487
* [QTBUG-137172](https://qt-project.atlassian.net/browse/QTBUG-137172) "section" property in ListView behaviour is broken
(degradation)
* [QTBUG-136629](https://qt-project.atlassian.net/browse/QTBUG-136629) QUnifiedTimer::updateAnimationTimers() crashes when
QApplication is recreated
* [QTBUG-128483](https://qt-project.atlassian.net/browse/QTBUG-128483) ItemGrabResult garbage collected too early
* [QTBUG-133315](https://qt-project.atlassian.net/browse/QTBUG-133315) qmlformat can still insert extra spaces in user code
* [QTBUG-123386](https://qt-project.atlassian.net/browse/QTBUG-123386) QmlFormat. Incorrect handling of some comments
* [QTBUG-138565](https://qt-project.atlassian.net/browse/QTBUG-138565) "Cannot generate qmltypes file" when trying to run in-
app purchase demo app on Android
* [QTBUG-132108](https://qt-project.atlassian.net/browse/QTBUG-132108) addApplicationFontFromData behaves abnormally after
removeAllApplicationFonts.
* [QTBUG-138155](https://qt-project.atlassian.net/browse/QTBUG-138155) qt_generate_deploy_qml_app_script: Error for space in
output name
* [QTBUG-135407](https://qt-project.atlassian.net/browse/QTBUG-135407) [Scene Graph - Graph App] Segmentation Fault
* [QTBUG-139026](https://qt-project.atlassian.net/browse/QTBUG-139026) Scrollbar size jumps during drag due to dynamic item
heights
* [QTBUG-139211](https://qt-project.atlassian.net/browse/QTBUG-139211) tst_qquickpopup (Failed)
* [QTBUG-139320](https://qt-project.atlassian.net/browse/QTBUG-139320) QQ4A - Buffer Overflow crash in application project
* [QTBUG-139688](https://qt-project.atlassian.net/browse/QTBUG-139688) [REG 6.9.3 -> 6.10.0] Public Java Classes Documentation
Bugs
* [QTBUG-140181](https://qt-project.atlassian.net/browse/QTBUG-140181) Build failure in QtDeclarative with latest nightly
libc++
* [QTBUG-140041](https://qt-project.atlassian.net/browse/QTBUG-140041) ids are not properly resolved when using cachegen
* [QTBUG-114718](https://qt-project.atlassian.net/browse/QTBUG-114718) [Tests] tst_QQuickPopup fails

### qtmultimedia
* [QTBUG-130636](https://qt-project.atlassian.net/browse/QTBUG-130636) FFmpeg: QCamera::FlashOn is unreliable
* [QTBUG-134607](https://qt-project.atlassian.net/browse/QTBUG-134607) Video playback crash when setting QQuickWindow
GraphicsAPI to Vulkan
* [QTBUG-138414](https://qt-project.atlassian.net/browse/QTBUG-138414) FFmpeg Plugin: Improve usability on different RHI
backend configurations
* [QTBUG-138952](https://qt-project.atlassian.net/browse/QTBUG-138952) tst_qaudiosink: start_afterStopAndReset() crashes on
macOS
* [QTBUG-139549](https://qt-project.atlassian.net/browse/QTBUG-139549) Qt multimedia compilation error windows 32 bit
* [QTBUG-124562](https://qt-project.atlassian.net/browse/QTBUG-124562) Exposure compensation (setExposureCompensation) doesn't
work with the example app
* [QTBUG-139773](https://qt-project.atlassian.net/browse/QTBUG-139773) Crash in MediaPlayer in qtdice demo
* [QTBUG-139681](https://qt-project.atlassian.net/browse/QTBUG-139681) Camera widgets record button crashes application on
linux
* [QTBUG-140431](https://qt-project.atlassian.net/browse/QTBUG-140431) apalis-imx6: media Player example fails to play video
* [QTBUG-139660](https://qt-project.atlassian.net/browse/QTBUG-139660) QTextToSpeech WinRT backend stops speaking after the
first word in Qt 6.9.2
* [QTBUG-140122](https://qt-project.atlassian.net/browse/QTBUG-140122) Background Color Difference During Video Playback
Between Windows Media Player and Qt Media Player Example

### qttools
* [QTBUG-69756](https://qt-project.atlassian.net/browse/QTBUG-69756) QDoc: Parentheses in link text causes premature link end
anchor
* [QTBUG-137569](https://qt-project.atlassian.net/browse/QTBUG-137569) make qttools configure more user friendly on windows
* [QTBUG-139614](https://qt-project.atlassian.net/browse/QTBUG-139614) QDoc: Index files do not record the declared return type
* [QTBUG-139407](https://qt-project.atlassian.net/browse/QTBUG-139407) QDoc fails to build with LLVM >= 21
* [QTBUG-138870](https://qt-project.atlassian.net/browse/QTBUG-138870) QDoc fails to parse templated using statement with
default value for a template arg
* [QTBUG-86490](https://qt-project.atlassian.net/browse/QTBUG-86490) Generated documentation for change signals that represent
more than one property is hard to read
* [QTBUG-140378](https://qt-project.atlassian.net/browse/QTBUG-140378) lupdate fails to compile with LLVM 21 due to removed
FileManager::getFile() API
* [QTBUG-110696](https://qt-project.atlassian.net/browse/QTBUG-110696) Qt6CoreMacros.cmake should take AUTOGEN_BUILD_DIR into
account

### qtdoc
* [QTBUG-138169](https://qt-project.atlassian.net/browse/QTBUG-138169) Document Viewer: Runtime warnings
* [QTBUG-137296](https://qt-project.atlassian.net/browse/QTBUG-137296) Clarifications to "Qt for Android - Building from
Source" page based on customer feedback.
* [QTBUG-136065](https://qt-project.atlassian.net/browse/QTBUG-136065) Installer command does not work
* [QTBUG-138527](https://qt-project.atlassian.net/browse/QTBUG-138527) Replace direct links to https://doc.qt.io/qt-6/
* [QTBUG-138676](https://qt-project.atlassian.net/browse/QTBUG-138676) Coffee machine examples images not getting current
values fom slider

### qtlocation
* [QTBUG-138409](https://qt-project.atlassian.net/browse/QTBUG-138409) Incorrect qtlocation documentation
* [QTBUG-137557](https://qt-project.atlassian.net/browse/QTBUG-137557) QtLocation: Using GeocodeModel with OSM plugin in QML
causes app crash when canceling update

### qtpositioning
* [QTBUG-139654](https://qt-project.atlassian.net/browse/QTBUG-139654) Update QtPositioning documentation to use QDoc commands
* [QTBUG-139780](https://qt-project.atlassian.net/browse/QTBUG-139780) Qt Positioning: Discrepancy between documented type
names and actual type names
* [QTBUG-139560](https://qt-project.atlassian.net/browse/QTBUG-139560) Access functions are documented even when their
properties are not

### qtconnectivity
* [QTBUG-139280](https://qt-project.atlassian.net/browse/QTBUG-139280) Cannot build QT 6.8 without GNU extensions

### qtwayland
* [QTBUG-135341](https://qt-project.atlassian.net/browse/QTBUG-135341) text input v3: input method window is misplaced after
closing a popup
* [QTBUG-135921](https://qt-project.atlassian.net/browse/QTBUG-135921) text-input-v3 skips advertising capabilities
* [QTBUG-131983](https://qt-project.atlassian.net/browse/QTBUG-131983) text input v3: first character after refocus doesn't go
through the input method
* [QTBUG-137727](https://qt-project.atlassian.net/browse/QTBUG-137727) Crash in zwp_text_input_v3_set_surrounding_text when
selecting large text
* [QTBUG-139250](https://qt-project.atlassian.net/browse/QTBUG-139250) Top-level tool window doesnt oppen
* [QTBUG-135354](https://qt-project.atlassian.net/browse/QTBUG-135354) wayland\custom-extension and wayland\custom-shell
examples fails to build with Boot to Qt on Windows
* [QTBUG-130652](https://qt-project.atlassian.net/browse/QTBUG-130652) REG: Hiding and reshowing a sub-window crashes Wayland
client

### qt3d
* [QTBUG-138670](https://qt-project.atlassian.net/browse/QTBUG-138670) Doc: Scene3D QML type is missed at Qt 3D Scene3D Module

### qtserialport
* [QTBUG-133489](https://qt-project.atlassian.net/browse/QTBUG-133489) ResourceError does not fire on unplug for QtSerialPort
6.8.2
* [QTBUG-138643](https://qt-project.atlassian.net/browse/QTBUG-138643) Details missing for some USB serialport adapters

### qtwebsockets
* [QTBUG-81084](https://qt-project.atlassian.net/browse/QTBUG-81084) Websocket client creates TCP RST instead proper shutdown
on close()

### qtwebengine
* [QTBUG-123607](https://qt-project.atlassian.net/browse/QTBUG-123607) Vulkan backend rendering only black on X11
* [QTBUG-133608](https://qt-project.atlassian.net/browse/QTBUG-133608) Missing documentation on how to install Qt WebEngine
* [QTBUG-131897](https://qt-project.atlassian.net/browse/QTBUG-131897) pdf viewer is not working on nano browser and simple
browser sample apps
* [QTBUG-111907](https://qt-project.atlassian.net/browse/QTBUG-111907) Crash when touching text field inside WebEngineView
* [QTBUG-138641](https://qt-project.atlassian.net/browse/QTBUG-138641) QtWebEngine rendering glitches with `<select>` element
* [QTBUG-134055](https://qt-project.atlassian.net/browse/QTBUG-134055) Make Qt WebEngine expose accessibility content properly
* [QTBUG-138159](https://qt-project.atlassian.net/browse/QTBUG-138159) Build error:
QtWebEngineCore/private/qtwebenginecoreglobal_p.h: No such file or
directory
* [QTBUG-127109](https://qt-project.atlassian.net/browse/QTBUG-127109) trouble configuring QtPDF for iOS
* [QTBUG-138881](https://qt-project.atlassian.net/browse/QTBUG-138881) Windows Debug: QQuickWebEngineScriptCollection crashes
after adding custom library path
* [QTBUG-136622](https://qt-project.atlassian.net/browse/QTBUG-136622) Accessiblity:voice over can't read table content
* [QTBUG-135621](https://qt-project.atlassian.net/browse/QTBUG-135621) gn.py needs an -isysroot argument but configure doesn't
create it
* [QTBUG-137730](https://qt-project.atlassian.net/browse/QTBUG-137730) Failed to build sources on tqtc/lts-6.8:
XSLT_DEBUG_INIT’ conflicts with a previous declaration
* [COIN-1249](https://qt-project.atlassian.net/browse/COIN-1249) broken system header on rhel-8.10
* CVE-2025-6558: Incorrect validation of untrusted input in ANGLE and GPU
* CVE-2025-6965
* CVE-2025-7656: Integer overflow in V8
* CVE-2025-7657: Use after free in WebRTC
* CVE-2025-8576: Use after free in Extensions
* CVE-2025-8580: Inappropriate implementation in Filesystems
* CVE-2025-8582: Insufficient validation of untrusted input in DOM
* CVE-2025-8879: Heap buffer overflow in libaom
* CVE-2025-8880: Race in V8
* CVE-2025-8881: Inappropriate implementation in File Picker
* CVE-2025-8901: Out of bounds write in ANGLE
* CVE-2025-9866
* CVE-2025-10200: Use after free in Serviceworker
* CVE-2025-10201: Inappropriate implementation in Mojo
* CVE-2025-10500: Use after free in Dawn
* CVE-2025-10501: Use after free in WebRTC
* CVE-2025-10502: Heap buffer overflow in ANGLE
* CVE-2025-10890: Side-channel information leakage in V8
* CVE-2025-10891: Integer overflow in V8
* CVE-2025-10892: Integer overflow in V8
* CVE-2025-11458: Heap buffer overflow in Sync
* CVE-2025-11460: Use after free in Storage
* CVE-2025-11206: Heap buffer overflow in Video
* CVE-2025-11207: Side-channel information leakage in Storage
* CVE-2025-11216: Inappropriate implementation in Storage
* Security bug 43416197
* Security bug 421544815
* Security bug 427316421
* Security bug 428177287
* Security bug 428754691
* Security bug 431668129
* Security bug 431828026
* Security bug 432661300
* Security bug 435068768
* Security bug 435225528
* Security bug 439058241
* Security bug 440866282
* Security bug 441427753
* Security bug 445380761

### qtvirtualkeyboard
* [QTBUG-138693](https://qt-project.atlassian.net/browse/QTBUG-138693) Doc: VirtualKeyboardSetting QML Type is missed at Qt
Virtual Keyboard QML Types
* [QTBUG-139038](https://qt-project.atlassian.net/browse/QTBUG-139038) Overlay issue with Virtual Keyboard + Material Style
* [QTBUG-124178](https://qt-project.atlassian.net/browse/QTBUG-124178) Virtualkeyboard of Qt 5.15.15 crash on Ubuntu

### qtspeech
* [QTBUG-137855](https://qt-project.atlassian.net/browse/QTBUG-137855) QTextToSpeech: flite - sayingWord signals emitted
delayed
* [QTBUG-139660](https://qt-project.atlassian.net/browse/QTBUG-139660) QTextToSpeech WinRT backend stops speaking after the
first word in Qt 6.9.2
* [QTBUG-108205](https://qt-project.atlassian.net/browse/QTBUG-108205) tst_QTextToSpeech::pauseResume(darwin) fails on macOS 13
in CI

### qtremoteobjects
* [QTBUG-139754](https://qt-project.atlassian.net/browse/QTBUG-139754) FAIL!  : tst_clientSSL::testRun()
'socketClient->waitForEncrypted(-1)' returned FALSE

### qtquick3d
* [QTBUG-136137](https://qt-project.atlassian.net/browse/QTBUG-136137) License of
qtquick3d/src/runtimerender/res/effectlib/fog.glsllib: SPDX header
differs from qt_attribution
* [QTBUG-138245](https://qt-project.atlassian.net/browse/QTBUG-138245) FTBFS: qtquick3d's embree 3rd-party
* [QTBUG-139232](https://qt-project.atlassian.net/browse/QTBUG-139232) Crash when View3D is destroyed in a multiview case
* [QTBUG-136911](https://qt-project.atlassian.net/browse/QTBUG-136911) 2D items take transformation from random camera if there
are multiple View3Ds into a single scene
* [QTBUG-126098](https://qt-project.atlassian.net/browse/QTBUG-126098) Item2D uses wrong transformation in multiple views
* [QTBUG-139130](https://qt-project.atlassian.net/browse/QTBUG-139130) Nested View3D causes 2D content to not be rendered
* [QTBUG-139274](https://qt-project.atlassian.net/browse/QTBUG-139274) Loader3D and ComponentBehaviour Bound seem incompatible

### qtcoap
* [QTBUG-139697](https://qt-project.atlassian.net/browse/QTBUG-139697) Provide a public "bind" API for QCoapClient, or at least
filter out unexpected replies not from peer

### qthttpserver
* [QTBUG-137330](https://qt-project.atlassian.net/browse/QTBUG-137330) QtHttpServer: Writing from Sequential QIODevices to
HTTP(S)/1.1 Hangs the Client
* [QTBUG-138611](https://qt-project.atlassian.net/browse/QTBUG-138611) QtHttpServer has out of order writes because it starts
handling the next HTTP/1 request before it's done writing from QIODevice

### qtgrpc
* [QTBUG-138683](https://qt-project.atlassian.net/browse/QTBUG-138683) Protobuf: repeated enum fields are serialized
incorrectly
* [QTBUG-138494](https://qt-project.atlassian.net/browse/QTBUG-138494) GRPC, QHttp2Channel: Implement metadata handling
according to protocol
* [QTBUG-129160](https://qt-project.atlassian.net/browse/QTBUG-129160) QtGrpc: improve lifetime-management of Http2Handler
* [QTBUG-139597](https://qt-project.atlassian.net/browse/QTBUG-139597) QtGrpc: QGrpcHttp2Channel should guarantee
transportation scheme

### qtgraphs
* [QTBUG-137718](https://qt-project.atlassian.net/browse/QTBUG-137718) XYSeries: opacity property has no effect
* [QTBUG-133759](https://qt-project.atlassian.net/browse/QTBUG-133759) the Custom3DItem position is not correct when setting
"axisZ.reversed: true" in QtGraphs
* [QTBUG-138470](https://qt-project.atlassian.net/browse/QTBUG-138470) SurfaceGallery does not start properly
* [QTBUG-138462](https://qt-project.atlassian.net/browse/QTBUG-138462) QtGraphs pollutes the global namespace
* [QTBUG-138506](https://qt-project.atlassian.net/browse/QTBUG-138506) QtGraphs crash when GraphView is destroyed
* [QTBUG-134003](https://qt-project.atlassian.net/browse/QTBUG-134003) QtGraphs pieSize and holeSize validate and render
differently
* [QTBUG-138923](https://qt-project.atlassian.net/browse/QTBUG-138923) Gradient range doesn't update with aspectRatio
* [QTBUG-138924](https://qt-project.atlassian.net/browse/QTBUG-138924) Gradient does not work when starting up the app in some
cases
* [QTBUG-138822](https://qt-project.atlassian.net/browse/QTBUG-138822) Reusing same ValueAxis in multiple GraphViews results in
a crash
* [QTBUG-139112](https://qt-project.atlassian.net/browse/QTBUG-139112) QtGraphs AreaSeries inconsistent area filling
* [QTBUG-139568](https://qt-project.atlassian.net/browse/QTBUG-139568) Graph Gallery- App crashes when Clicking on Surface
graph
* [QTBUG-133921](https://qt-project.atlassian.net/browse/QTBUG-133921) The Graph Gallery example crashes when clicking on
surface graph
* [QTBUG-135818](https://qt-project.atlassian.net/browse/QTBUG-135818) OnHover/Enter/Exit is not Triggered
* [QTBUG-138456](https://qt-project.atlassian.net/browse/QTBUG-138456) Documentation contains references to "QGraphsView" which
is a private class
* [QTBUG-138797](https://qt-project.atlassian.net/browse/QTBUG-138797) Docs are messed up with * in some places

Known Issues
------------

* Check that your system meets Qt's requirements:
https://doc.qt.io/qt-6.8/supported-platforms.html
* The RTA (release test automation) reported issues in Qt 6.8.x:
https://qt-project.atlassian.net/issues/?filter=10287
* See Qt 6.8 known issues from:
https://wiki.qt.io/Qt_6.8_Known_Issues
* Qt 6.8.5 Open issues in Jira:
https://qt-project.atlassian.net/issues/?filter=10681

Credits for the release goes to:
---------------------------------

* Eirik Aavitsland
* Laszlo Agocs
* Dilek Akcay
* Konsta Alajärvi
* Anu Aliyas
* Even Oscar Andersen
* Soheil Armin
* Xavier BESSON
* Mate Barany
* Nicholas Bennett
* Tim Blechmann
* Eskil Abrahamsen Blomfeldt
* David Boddie
* Tatiana Borisova
* Joerg Bornemann
* Assam Boudjelthia
* Marcell Brauner
* Aurélien Brooke
* Kai Uwe Broulik
* Michael Brüning
* Olivier De Cannière
* Alexei Cazacov
* Kaloyan Chehlarski
* Albert Astals Cid
* Alexandru Croitor
* Mitch Curtis
* Giuseppe D'Angelo
* Pavel Dubsky
* Artem Dyomin
* Alexey Edelev
* Oliver Eftevaag
* Christian Ehrlicher
* Andreas Eliasson
* Ilya Fedin
* Joshua GPBeta
* Julian Greilich
* Robert Griebl
* Mikko Hallamaa
* Andre Hartmann
* Elias Hautala
* Moss Heim
* Ulf Hermann
* Øystein Heskestad
* Volker Hilsheimer
* Dominik Holland
* Benedikte Holm
* Samuli Hölttä
* Masoud Jami
* Morteza Jamshidi
* Allan Sandfeld Jensen
* Igor Khanin
* Ahmed El Khazari
* Ali Kianian
* Friedemann Kleint
* André Klitzing
* Michal Klocek
* Jarek Kobus
* Jarkko Koivikko
* Niko Korkala
* Tomi Korpipaa
* Fabian Kosmale
* Volker Krause
* Mike Krus
* Santhosh Kumar
* Kai Köhne
* Cristian Le
* Inho Lee
* Frédéric Lefebvre
* Robert Löhning
* Thiago Macieira
* Jan Moeller
* Safiyyah Moosa
* Sheree Morphett
* Marc Mutz
* Mårten Nordheim
* Dennis Oberst
* Matti Paaso
* Kwanghyo Park
* Samuli Piippo
* Karim Pinter
* Timur Pocheptsov
* Joni Poikelin
* Jacek Poplawski
* Rami Potinkara
* Sakaria Pouke
* Dheerendra Purohit
* MohammadHossein Qanbari
* Liang Qi
* Khem Raj
* Matthias Rauter
* Topi Reinio
* Bernhard Rosenkränzer
* Shawn Rutledge
* Ahmad Samir
* Timon Sassor
* Lars Schmertmann
* SanthoshKumar Selvaraj
* Luca Di Sera
* Sami Shalayel
* Nils Petter Skålerud
* Nils Peter Skålerud
* Ivan Solovev
* Axel Spoerl
* Christian Strømme
* Tarja Sundqvist
* Lars Sutterud
* Tasuku Suzuki
* Jan Arve Sæther
* Nodir Temirkhodjaev
* Jens Trillmann
* Paul Olav Tvete
* Sami Varanka
* Peter Varga
* BogDan Vatra
* Bror Wetlesen Vedeld
* Doris Verria
* Tor Arne Vestbø
* Petri Virkkunen
* Juha Vuolle
* Olli Vuolteenaho
* Jaishree Vyas
* Jannis Völker
* Michael Weghorn
* Edward Welbourne
* Paul Wicking
* Piotr Wiercinski
* Oliver Wolff
* Semih Yavuz
* Zhao Yuhang
* Vlad Zahorodnii
* Oleksii Zbykovskyi
