Release note
============
Qt 6.8.1 release is a patch release made on the top of Qt 6.8.0.
As a patch release, Qt 6.8.1 does not add any new functionality but provides
bug fixes and other improvements and maintains both forward and backward
compatibility (source and binary) with Qt 6.8.0.

For detailed information about Qt 6.8, refer to the online documentation
included in this distribution. The documentation is also available online:

https://doc.qt.io/qt-6/index.html

The Qt version 6.8 series is binary compatible with the 6.7.x series.
Applications compiled for 6.7 will continue to run with 6.8.

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
N/A

### qtbase
* fee6283b85d QUrl::toString: fix using of NormalizePathSegments and
RemoveFilename
Fixed a bug that caused QUrl::toString(), QUrl::toEncoded() and
QUrl::adjusted() to ignore QUrl::NormalizePathSegments if
QUrl::RemoveFilename was set.

* c36b24b0873 Update bundled libpng to version 1.6.44
libpng was updated to version 1.6.44

* d2b98a11470 Update bundled libjpeg-turbo to version 3.0.4
libjpeg-turbo was updated to version 3.0.4

* 5c675fb2988 Windows: Use correct default font when
desktopSettingsAware is false
Fixed a regression where the default font on Windows would be larger
than before if desktopSettingsAware had been set to false.

* 6dfe5c847e0 Windows: Fix memory leak in DirectWrite font database
Fixed a memory leak when repopulating the DirectWrite font database.

* fdaf9c1a2e5 Update to Harfbuzz 10.0.1
Updated Harfbuzz to 10.0.1.

* 55a8050d1e7 QDirIterator: don't crash with next() after hasNext()
returned false
Fixed a crash that happened if you called next() after hasNext() had
already returned false. Ideally you should never call next() without
first calling hasNext() as that could lead to unexpected results (for
example, infinite loops).

* 57caaff5fc4 CMake: Change SBOM generation to be enabled by default
(mostly)
SBOM generation is now enabled by default, when building Qt, except for
developer builds and no-prefix builds. JSON SBOM generation is enabled
by default if the required Python dependencies are available.

* 76da2f74d4e QUuid: restore sorting order of Qt < 6.8
Fixed a regression that caused QUuid sorting order to change for some
UUIDs, compared to Qt 6.7 and earlier versions.

* 037e14dd07a macOS: Add support for context menu keyboard hotkey
The context menu keyboard hotkey available on macOS 15 is now
propagated as a QContextMenuEvent if the corresponding QKeyEvent is not
accepted.

* 1fac1117315 SQLite: Update SQLite to v3.47.0
Updated SQLite to v3.47.0

* 6535b6d5f3d QList: fix std::to_address(QList::iterator) on older
compilers
Fixed std::to_address() on QList::iterator on older compilers.

* e28adc19ed5 Decouple location and bluetooth permissions if API level
>= 31
ACCESS_FINE_LOCATION is no longer requested if API-level >= 31

* 98d03964ac4 Windows: Fix missing glyphs for very large font
Fixed an issue where glyphs might be missing for very large fonts.

* 20fbd344005 QHeaderView: update the view correctly in
resetDefaultSectionSize
Changing the defaultSectionSize no longer affects sections that don't
have the old default size.

* 44bf5566cb0 moc: handle nested structs with meta content
Fixed a bug that caused moc to attempt to parse a nested struct (not
class) with meta keywords and this produced code that wouldn't compile.
Nested classes and structures are permitted, but must be defined outside
of the declaration of the outer class.

* 3b9f2025392 Freetype: Fix artificial oblique combined with other
transforms
Fixed an issue where artificially obliquened text would look incorrect
when other transformations were also applied and the Freetype backend
was in use.

* 6aca2efd621 CMake:Android: add wrapper scripts to easily run apps
Add wrapper scripts to run Android apps and tests with ease from the
host.

* d4801777890 Make QSpan::isEmpty() constexpr
Fixed isEmpty() to be constexpr (empty() already was).

* 334a3922c0b QThread/Unix: refactor to split QThreadPrivate::finish()
in two phases
Restored the Qt 6.7 timing of when the finished() signal is emitted
relative to the destruction of thread_local variables. Qt 6.8.0
contained a change that moved this signal to a later time on most Unix
systems, which has caused problems with the order in which those
variables were accessed. The destruction of the event dispatcher is kept
at this late stage, wherever possible.

* 4f4c07e94d9 Upgrade to Harfbuzz 10.1.0
Upgraded Harfbuzz to version 10.1.0.

### qtdeclarative
* 55c93d6a5b QQuickWidget: Assign focus to offscreen window when focus
chain wraps
The first/last item must be focused when QQuickWidget receives a focus-
in event due to tab/backtab reasons. In other cases, such as
ActiveWindowFocusReason, the item that was focused before will be
refocused.

* 549f4f6f47 QQuickItem: Correct coordinate conversion to QPointF
The function mapToItem(item, real x, real y) now returns a point with
real values instead of rounding to an integer.

* ff177a379c Close Dialog when a DestructiveRole button is clicked
Dialog is now closed when a button with the DestructiveRole is clicked.
Currently the only button with this role is Discard.

* 3d3e32447e PointHandler: don't deactivate because of synth-mouse
events
If PointHandler is declared with acceptedButtons: Qt.NoButton it now
means that the PointHandler does not care which buttons are pressed or
not pressed: but it ignores synth-mouse events and responds only to
events that come from the appropriate kind of device. If specific
acceptedButtons are set, synthetic mouse-moves can deactivate it
temporarily.

* 8d93ef6220 CMake: Add a global QT_QML_NO_CACHEGEN cmake variable
A new QT_QML_NO_CACHEGEN cmake variable can be set to disable
compilation of qml files for all project qml files.

* 3c162c592a QQmlComponent: Fix ordering of callbacks on
loadFromModule()
The QQmlParserStatus callbacks are invoked on objects loaded using
QQmlComponent::loadFromModule() at appropriate times now. You can rely
on any initial properties having been set before componentComplete() is
called and you can rely on the object having a valid QML context.

### qtmultimedia
* 067dcda60 Don't add file extension when the filename already has an
extension
QMediaRecorder::setOutputLocation and QImageCapture::captureToFile will
no longer alter the suffix/extension if the provided path already
includes an extension, even if this extension does not align with the
recommended extensions for the MIME type.

* 48c05c3fb Update FFmpeg version in documentation
Updated FFmpeg to n7.1.

* a4734a3d3 Make backend selection case insensitive
Backend selection using the QT_MEDIA_BACKEND environment variable is
now case insensitive.

* dbc1482d3 Disable HW textures conversion by default on native Windows
backend
HW texture conversion (zero copy texture transfer) is disabled by
default with the native Windows media backend. Set the
QT_DISABLE_HW_TEXTURES_CONVERSION environment variable to '0' to re-
enable it.

* 0968a212e QCamera: Change QML manualExposureTime property type to
float
QML binding for QCamera::manualExposureTime has changed from type int
to float.

* f05302d78 QCamera, docs: Update focusMode and focusDistance
documentation
focusDistance can now be applied without focusMode already being set to
FocusModeManual.

* d5a4cf9bf Revert "Update FFmpeg version in documentation"
Reverted FFmpeg to n7.0.2.

### qttools
* 0aac4ddbb qdoc: Allow custom sorting of generated group lists
\generatelist and \annotatedlist commands now support custom sort order
for the generated lists.

### qtconnectivity
* 785e56f6 Check if location checks can be skipped with bluetooth scan
Android implementation now allows starting scan even if Location is
switched off and location permissions aren't granted. This requires that
API level is 31+ and that BLUETOOTH_SCAN asserts 'neverForLocation'.

### qtimageformats
* 082d494 Update bundled libtiff to version 4.7.0
Bundled libtiff was updated to version 4.7.0

### qtserialport
* 3ac6261 Windows use iManufacturer/iProduct for
manufacturer/description
Make Windows use USB iManufacturer for the returned Manufacturer in
QSerialPortInfo::availablePorts() and USB iProduct for the the returned
description also in availablePorts(). This makes Windows and Linux
report the same information for both fields.

### qtquick3d
* 6e4222ea8 XR: Make multiview rendering the default
Multiview rendering is now enabled by default on platforms that
supports it.

### qt5compat
* 5234c2b QTextCodec: use DefaultConversion too
Fixed a bug that caused QTextCodec not to write the Byte Order Mark for
UTF codecs. QTextCodec now has the same behavior as Qt 5.x.

### qtopcua
* 8616972b Fix race condition between backend shutdown and main thread
The connection property of OpcUaConnection now    takes ownership of the
QOpcUaClient as described in the docs


Fixes
-----

### qtbase
* QTBUG-127711 QUrl.adjusted doesn't work with QUrl::RemoveFilename |
QUrl::NormalizePathSegments
* QTBUG-117096 Input fields (QWidgets and QML) don't register dead keys
accents when using a Linux desktop
* QTBUG-128742 QConcatenateTablesProxyModel does not react to
rowsAboutToBeMoved/rowsMoved
* QTBUG-127852 [REG: 5->6] Crash when using QSortFilterProxyModel if the
source model has a buddy() and does layout change
* QTBUG-128800 QFileInfo::isSymLink() returns true with wrong path
* QTBUG-128848 QTypeRevision::fromVersion fails ( in debug mode ), when
being fed with characters
* QTBUG-128929 Potential integer overflow in QNetworkReplyWasmImpl
* QTBUG-128558 QTreeWidget creates new accessible QTreeWidgetItems each
time the child at index is retrieved
* QTBUG-128499 Disabled components are not grayed in Light mode
* QTBUG-128940 FAIL!  :
qmltestrunner::AnimatedImage::test_imageSource(local not found) Not all
expected messages were received
* QTBUG-121855 missing RHI related headers (class documentation is
wrong)
* QTBUG-125994 All RHI class documentations shows Qt6::Gui as the link
target for CMake
* QTBUG-129128 QTableWidget: moving rows deletes rows
* QTBUG-128906 Konsole crashes with SIGSEGV
* QTBUG-120151 Two simultaneously opened onscreen keyboards could work
incorrectly
* QTBUG-127701 ASSERT: "index >= 0 && index < m_adaptorModel.count()" in
file /home/...qqmltableinstancemodel.cpp, line 124
* QTBUG-128517 [REG 6.6.3->6.7.2] Some cells in QTableViews do not show
text unless the cell is selected
* QTBUG-126953 Wrong documentation for compression tag in a qrc file
* QTBUG-129193 Qt compiled with gcc 13 and -march=bdver4/-mtune=bdver4
causes segfaults in tests, downstream applications
* QTBUG-129147 [Windows] Crash on QRhiD3D::output6ForWindow() with
nullptr access
* QTBUG-129258 Key and pointer events delivered to popups are synthetic
* QTBUG-129178 Broken layout on landing page (offline style)
* QTBUG-129349 Re-enable tst_qhostinfo on macOS
* QTBUG-129362 tst_QDockWidget::setFloating() failed on GNOME
Wayland(Ubuntu 24.04 and 22.04
* QTBUG-129434 [[Regr: 6.7.2 -> 6.7.3]] QTranslator::load finds
languages in wrong order
* QTBUG-129201 tst_qwidget_window crashes on Android in nightly health
check
* QTBUG-129375 [REG 6.5.1 -> 6.7.2|6.8.0-rc1] Common Trace Format (CTF)
backend causes application crash
* QTBUG-129412 Service Embedding manual test crashes
* QTBUG-127422 Second QtQuickView doesn't work
* QTBUG-36831 Drop indicator painted as single pixel when not shown
* QTBUG-129299 [Widget] The view becomes black when docking back the
window in Hellp GL2 example
* QTBUG-129335 DNS lookup on Apple platforms doesn't go through system
machinery
* QTBUG-129509 (Regression) Erratic scrolling behavior using the mouse
in 6.7.3
* QTBUG-129514 Reversed mouse buttons don't work properly on 6.7.3
* QTBUG-110841  [REG: 5.10.1->5.11.0-alpha] Mouse events not observed
when Super (Windows) key is held down.
* QTBUG-129213 Multipe log writings "QQnx: Failed to get screen for
window, errno=22" when starting Qt application
* QTBUG-129436 Virtual keyboard example doesn't work on QNX800
* QTBUG-129358 Multi-abi build does not rebuild other targets when there
is a change
* QTBUG-129524 Android crash on Widget QMenu shortcut (when keyboard
open)
* QTBUG-128359 Right-click menu logic error
* QTBUG-129689 QStorageInfo valid information not reset after path is
cleared on Linux
* QTBUG-129398 QButtonGroup::addButton() doesn't guarantee negative ids
(as promised in docs)
* QTBUG-129386 QProgressBar Windows style has changed for the chunks.
* QTBUG-129399 Widgets gallery example color scheme does not work
* QTBUG-127596 Application crash on opening in ~QBindingObserverPtr()
* QTBUG-129085 Build on Solaris fails as -fstack-protector-strong is
used without -lssp
* QTBUG-125474 windowsvista style: menus are broken
* QTBUG-127135 [Reg 6.5->6.7] Menu display problem Windows 11 dark mode.
* QTBUG-129697 QT stopped understanding HTTP response compressed with
gzip.
* QTBUG-129770 Android crash on Widget QMenu shortcut
* QTBUG-124360 Android TV system keyboard no long opens on text fields
in 6.7
* QTCREATORBUG-31769 Passing 'settings set target.load-script-from-
symbol-file true' to lldb on macOS breaks debug dumpers when multiple
Creators are installed on the system
* QTBUG-91262 Qpainter draws text with gray edge on qimage
* QTBUG-129149 missing wasm ondragleave handler for drag and drop
* QTBUG-129832 Default font is way bigger in 6.8
* QTBUG-129914 QPainter drawText(int x, int y, int width, int height,
...) doesn't work if width or height is zero
* QTBUG-129896 Qt 6.8.0 build with ICU enabled fails on Windows
* QTBUG-129920 QMetaProperty::revision() always returns a fixed value
fixed number 0xFF00 + number
* QTBUG-129979 QGroupBox title looks enabled while group box is disabled
* QTBUG-129898 Pot. regression 6.7 -> 6.8 QThreadPool too many thread
IDs
* QTBUG-129716 Submenu item not correctly aligned in rtl mode (gap to
main menu)
* QTBUG-103898 QListWidget::dropEvent processes already accepted events
* QTBUG-129471 [CMake] Unable to configure qtbase due to
$<LINK_ONLY:EXPAT::EXPAT>
* QTBUG-130045 QTableView: there's a single pixel line between cells
where dropping is handled as if on viewport
* QTBUG-129504 Regenerate certificates for qsslserver auto-test
* QTBUG-129983 QSqlQuery Postgres and timestamp => QDateTime(Invalid)
* QTBUG-129472 Regression: QMainWindow is invisible in Qt6.8beta for iOS
* QTBUG-130109 Qt plugins not loaded through symlinks
* QTBUG-130142 6.8 Regresssion:  QDirIterator::next segfaults
* QTBUG-129234 tooltip only works once
* QTBUG-130133 ios QFileDialog crash
* QTBUG-128731 macOS: Crash when disconnecting screen when app is in
fullscreen
* QTBUG-129481 [Reg 6.8.0-beta4->6.8.0-rc][Reg 6.7.2->6.7.3] Build break
* QTBUG-127111 QRhi::nextResourceUpdateBatch() documentation error
* QTBUG-129999 QTextTableCell::setFormat example code layout is broken
* QTBUG-124496 QObject::timerEvent may be called before the timer
elapsed
* QTBUG-129405 Maximizing and restoring a window gradually moves it
downwards
* QTBUG-129679 Windows 10: Maximized fixed-height window exceeds screen
to the right when task bar is left
* QTBUG-123752 Unexpected offset of fixed-height top-level window when
Windows Taskbar is on top
* QTBUG-130304 QDBusMessage::createMethodCall with a bad "service"
argument crashes in libdbus-1
* QTBUG-129596 Crash when closing inactive tab in tabbar for MDI window
* QTBUG-130155 QUuid sorting order was changed in Qt 6.8.0
* QTBUG-130294 FEATURE_cxx20 flag does not cause the code to be compiled
with C++20
* QTBUG-129287 QDateTime fails to parse some dates
* PYSIDE-2897 QCombobox Checkstates collide with text on Windows
* PYSIDE-2906 In Qt 6.7.x+ with the windows11 style, checkboxes and
items in a custom QComboBox overlap, breaking the UI. This issue is
absent in Qt 6.6.3 and earlier, suggesting a regression related to the
style changes introduced in newer Qt versions.
* QTBUG-116511 Android 11 and above setNativeLocks failed: "Function not
implemented"
* QTBUG-130122 Windows11 style missing menu indicator for QPushButton
menu
* QTBUG-130123 Windows11 style same text color for
active/inactive/disabled widgets
* QTBUG-130125 Windows11 style padding for QComboBox
* QTBUG-130288 QDoubleSpinBox layout still broken in Windows 11
* QTBUG-129092 "OpenType support missing for..." Qt warnings
* QTBUG-130476 6.8.0 openssl deployment
* QTBUG-127488 qtbase tests crashing on Android
* QTBUG-125874 QTcpSocket readyRead not emitted for first received data
* QTBUG-129113 VxWorks undefined references due to link line
* QTBUG-83498 Fix handling of plugins in static builds (and the
dependency cycles it creates)
* QTBUG-129704 Guard against potential NullPointerException for
QtActivityDelegate
* QTBUG-130399 windows11 style: QTabWidget with QMenu as corner widget
* QTBUG-130643 std::to_address doesn't work for QList::iterator
* QTBUG-128488 QPainterPath some time gives incorrect value
* QTBUG-129028 [Windows] Non-native QFileDialog behaves strangely when
creating a folder with a trailing space
* QTBUG-130119 configure with -disable-deprecated-up-to does not allow
5.15
* QTBUG-130309 QSortFilterProxyModel invalidate is slow when there's a
large number of persistent indicies
* QTBUG-129696 Crash in QCalendarBackend::dateTimeToString when timezone
is invalid
* QTBUG-86104 [evdev] The first event coordinates are incorrect when
absolute coordinates used for mouse handling.
* QTBUG-13404 QMenu does not take into account the width of separators
with text
* QTBUG-128912 QTreeView Header splitter cursor is not shown with
QGraphicsProxyWidget
* QTBUG-130056 Fail to link after qt_add_translations added to
CMakeLists.txt
* QTBUG-128484 HTTP cache:  max-age value is ignored by must-revalidate
* QTBUG-130720 Typo on enum QStyle::StyleHint
* QTBUG-124898 [Reg 6.2 -> 6.5] Qt.uiLanguage does not work for locale
changes
* QTBUG-128478 tst_qcompleter crashes on Linux, mostly on RHEL
* QTBUG-130704 [Regr:6.3.2->6.8.0] QMenu text alignment missing when
mixing actions with and without icons
* QTBUG-127536 When styling a QComboBox, it always has a check-box icon
even after setting the icon to none.
* QTBUG-129582 QComboBox with null view crashing application
* QTBUG-130621 tst_QPromise incorrectly disabled tests
* QTBUG-128913 QGraphicsItem::ItemIgnoresTransformations leads to show
popup at far off position
* QTBUG-126671 NativeRendering renders nothing on Windows on ARM in
VMWare Fusion on Mac
* QTBUG-116013 QHeaderView::resetDefaultSectionSize doesn't invalidate
cached size hints / update view
* QTBUG-130498 Q_ENUM for sub classes does not work
* QTBUG-130642 Incorrect QAbstractSpinBox size hint in Windows 11 style
when style sheet is set
* QTBUG-108015 [CMake] [MSVC2022] TEST_separate_debug_info always fail
* QTBUG-97436 Italic rotated text on Linux renders incorrectly
* QTBUG-130565 QString::slice uses the wrong snippet
* QTBUG-128518 [REG 6.6.3->6.7.2] Vertical scrollbar can appear
unpainted until window is resized
* QTBUG-128781 Setting flat button background colors does not work
correctly on Win11
* QTBUG-130739 tst_QImageIOHandler tests fail CI on VxWorks
* QTBUG-128302 [macOS] Closing window while modal dialog is open crashes
the application
* QTBUG-114873 Rendering is broken when moving window between monitors
with OpenGL on macOS
* QTBUG-130824 Windows11 style: wrong size hint for (editable) QComboBox
* QTBUG-11967 QDateEdit/CalendarPopup(true) has incorrect sizing
* QTBUG-130586 [Reg] The font "Terminus" is not rendered
* QTBUG-129946  Android QtQuickApp Not Work with Qt 6.8.0 ARM64-v8a
* QTBUG-129512 [Boot2Qt] QMenu does not reappear after closing in
widgets app
* QTBUG-129981 quiview.mm uses deprecated QPointingDevice method,
breaking 6.8 compilation from Src on iOS
* QTBUG-130138 Context Menu does not open on right click outside of
opened context menu
* QTBUG-123632 Regression: Setting background-color style of
QTreeView::item breaks alternatingRowColors
* QTBUG-126345 QHeaderView sorting indicator is missing with windows11
style and dark themes
* QTBUG-129791 Issue with Showmaximized function in case of QMainWindow
with Qt::FramelessWindowHint flag
* QTBUG-130865 [Windows] QWidget::showMaximized() does not follow
SPI_SETWORKAREA correctly when Qt::FramelessWindowHint is set
* QTBUG-129927 [REG: 6.7 -> 6.8] Use after free in QTimeZone
* QTBUG-129846 Quit in GUI application on linux in qt 6.8.0 does not
quit and process runs indefinitely
* QTBUG-130341 Crash during QNetworkAccessManager destruction
* QTBUG-117996 [REG 6.2 -> 6.5] QBasicTimer::stop: Failed. Possibly
trying to stop from a different thread
* QTBUG-130843 a11y: Qt sends AT-SPI signals with wrong DBus signature
* QTBUG-130828 windows11 style: radio buttons painted incorrectly inside
scroll area
* QTBUG-77939 QDoubleSpinBox dot(.) decimal separator disappears for
values >= 1000
* QTBUG-128916 QComboBox drop down is not visible on Windows11 in some
situation
* QTBUG-128329 qt combobox 放入到QGraphicsProxyWidget下拉框不显示
* QTBUG-116554 [macOS] Crash on QCocoaDrag::maybeDragMultipleItems()
* QTBUG-128405 Unavoidable race condition when using
QPromise::setException()?
* QTBUG-115451 QSpinBox, QComboBox visual Clipping / incorrect Size Hint
* QTBUG-130916 QCheckBox documentation mentions non-exising accessors
* QTBUG-131001 QWidget::childAt returns empty children
* QTBUG-131009 FAIL!  : tst_focus::navigation(tab-all-controls) Received
a warning that resulted in a failure
* QTBUG-128493 QIBASE Driver: Timestamps with timezones are not stored
as UTC
* QTBUG-128455 [VxWorks] configure doesn't recognize graphics settings
* QTBUG-120396 `QUrl::resolved` gives wrong result when there are more
`..`s in relative reference
* QTBUG-54693 QFileDialog::getOpenFileName crashes when parent is
deleted while dialog is open
* QTBUG-107157 tst_QWidget with QtWayland failed on Ubuntu 22.04, GNOME
* QTBUG-128855 Wasam drag and drop of a smaller file gives zero byte
* QTBUG-128371 Windows ARM: Fix blacklisted
tst_qwidget::render_windowOpacity()
* QTBUG-128372 Windows ARM: Fix blacklisted
tst_qwidget::enterLeaveOnWindowShowHide(dialog)
* QTBUG-129118 "DirectWrite: CreateFontFaceFromHDC() failed" Qt warnigns
* QTBUG-129023 tst_QWindow::windowExposedAfterReparent() failed on
Ubuntu 24.04 GNOME X11
* QTBUG-129029 tst_QComboBox:popupPositionAfterStyleChange() failed on
Ubuntu 24.04 GNOME X11
* QTBUG-129026 tst_QWidget_window::setWindowState(Qt::WindowMaximized)
failed on Ubuntu 24.04 GNOME X11
* QTBUG-127675 Spurious assertion failure in
tst_QSoundEffect::testSetSourceWhilePlaying
* QTBUG-129027 tst_QStatusBar::QTBUG4334_hiddenOnMaximizedWindow()
failed on Ubuntu 24.04 GNOME X11
* QTBUG-125323 Android Keyboard hides QML Text Edit Box
* QTBUG-125053 QAbstractListModel fails to populate QML model
* QTBUG-127340 [Reg 6.7->6.8] Wrong item count in ListView/Repeater
* QTBUG-119616 tst_Http2::duplicateRequestsWithAborts fails in CI
* QTBUG-77059 QStorageInfo::mountedVolumes() doesn't list volumes
mounted after "docker overlay volumes"
* QTBUG-118231 Android app 'pause' or 'screen-off' causes
'eglSwapBuffers failed' and various logcat errors
* QTBUG-28246 QFileSystemEngine::isCaseSensitive() is hardcoded to
return false on Windows and true on Unix
* QTBUG-31103 QFileSystemModel need to better case insensitivity support
* QTBUG-129516 tst_QAIV::testDialogAsEditor is flaky on Linux/X11
* QTBUG-129568 tst_QWidget_window::mouseMoveWithPopup() failed on Ubuntu
24.04 GNOME X11
* QTBUG-129567 tst_QWidget_window::tst_dnd_events() timeout on Ubuntu
24.04 GNOME X11
* QTBUG-129292 tst_QWindowContainer::testFocus() failed on GNOME
Wayland(Ubuntu 24.04 and 22.04)
* QTBUG-125446 Ubuntu 24.04 ARM64: HealthCheck qtbase failings
* QTBUG-129361 tst_QSizeGrip::hideAndShowOnWindowStateChange() failed on
Ubuntu 24.04 GNOME Wayland
* QTBUG-69423 QRandomGenerator not random on certain Windows
installations
* QTBUG-120238 Android 14 predictive text is broken for Gboard (on
target)
* QTBUG-96513 CI: qmake examples should not be built from tainted source
tree
* QTBUG-129849 REG: Possible memory leak in DirectWrite font database
* QTBUG-128420 Qt 6.8 does not support build paths with white spaces
anymore
* QTBUG-123711 QtQuickView doesn't handle recreation of Activity
properly
* QTBUG-128510 qtest: watchdog doesn't catch timeouts in initTestCase
and friends
* QTBUG-129839 6.8: Programmatically resized window stalls for initial
part of resize animation
* QTBUG-114987 tst_QGraphicsView::scrollBarRanges(motif, 3 x2) and many
others with QtWayland failed on Ubuntu 22.04, GNOME
* QTCREATORBUG-28838 QtC indentation hickup on enable_if_t<LHS < RHS> in
template-initializer
* QTBUG-130557 SBOM has references to build time paths
* QTBUG-125569 Make sure licensing in file matches that in
qt_attribution.json
* QTBUG-130613 Documentation of Q_GLOBAL_STATIC(MyType, staticType) is
confusing
* QTBUG-129944 A "strong assertion" does not help safely exclude
android.permission.ACCESS_FINE_LOCATION from manifest
* QTBUG-117358 BLUETOOTH_SCAN permission flag neverForLocation
* QTBUG-112164 Check ACCESS_FINE_LOCATION is no longer needed in recent
Android Sdk
* QTBUG-52507 Wrong menu position for QToolButton placed on a scene
* QTBUG-122109 QTreeWidget's columns do not seem to resize properly
after upgrading from Qt6.5.3 to Qt6.1.1
* QTBUG-123154 Applying stylesheet resets column and row size
configurations on Qt 6.5.4
* QTBUG-93625 qt_internal_add_test doesn't call qt_import_qml_plugins
* QTBUG-130500 Various network tests are failing on macOS 15
* QTBUG-130932 Top flaky test: tst_QAbstractItemView::testDialogAsEditor

### qtsvg
* QTBUG-128485 Crash on reading specific SVG file
* QTBUG-122310 SVG Rendering with opacity on group not consistent with
other viewers
* QTBUG-88265 QSvgGenerator QImage QBrush Not Work

### qtdeclarative
* QTBUG-128638 [Reg 6.7 -> 6.8] Crash when using live preview
* QTBUG-128782 [Reg 6.7 -> 6.8] Crash when using live preview
* QTBUG-128272 New example quickcontrols\spreadsheets fails to compile
on MSVC2022 x64
* QTBUG-126858 Closing a popup with popupType set to PopupWindow calls
exit transition twice
* QTBUG-127661 Creator jumps to auto generated file instead of the real
one
* QTBUG-128789 [Reg 6.6 -> 6.7] QML confuses types between engines
* QTBUG-128525 QML ComboBox closes on escape/back key release, not press
* QTBUG-128645 Fix Windows ARM: QtDeclarative -
TestLinkStaticQmlModule::canRun
* QTBUG-128931 Focus frame is never drawn inside QQuickWidget
* QTBUG-128420 Qt 6.8 does not support build paths with white spaces
anymore
* QTBUG-128860 Qt6QmlMacros doesn't handle build directories with spaces
in the path
* QTBUG-128934 tst_qquicktableview::checkColumnRowResizeAfterReorder is
flaky
* QTBUG-128444 Universal style theme does not change when the system
theme changes
* QTBUG-118588 qmllint: Nondeterministic output when multiple files are
linted in one invocation
* QTBUG-127308 [REG 6.6 → 6.8] qmlRestrictedType warning errorneously
triggers for enum class
* QTBUG-129052 controls tests are flaky since https://codereview.qt-
project.org/c/qt/qtdeclarative/+/589582
* QTBUG-129214 quick/quickwidgets/qmlpreviewer not compiling on Android
* QTBUG-129194 qmllint segmentation fault in QQmlSA::Element::internalId
* QTBUG-118898 Qmltyperegistrar ignores --namespace in --extract mode.
* QTBUG-128868 qmllint prints Warning: Ambiguous type detected.
XxxDialog is defined multiple times.
* QTBUG-129281 Assert when trying to access SplitView handle from the
outside
* QTBUG-129323 QtQuickDialogs won't reopen when closed
* QTBUG-128637 race condition with async Shape(Path)
* QTBUG-129329 QML Preview doesn't update properly
* QTBUG-123829 TreeView Documentation Code Example Displays Nothing
* QTBUG-128445 anchors.mirrored is still documented
* QTBUG-128500 The snippet in "Separating Tests from Application Logic"
leads to an error
* QTBUG-129310 Possible garbage collector bug
* QTBUG-85860 BusyIndicator in inconsistent state when running property
changed too fast
* QTBUG-127340 [Reg 6.7->6.8] Wrong item count in ListView/Repeater
* QTBUG-125053 QAbstractListModel fails to populate QML model
* QTBUG-129500 QQuickItem::mapToItem() can segfault during initalization
* QTBUG-126784  QQuickWindow::graphicsConfiguration() documentation
wrong
* QTBUG-128875 [PDF] Zooming in and out the pdf file then opening
another one causes to app to crash
* QTBUG-119034 result of Item.mapToItem call is round to integer
* QTBUG-128895 [Reg 6.2 -> 6.5] QtQuick.Templates causes crashes if
QtQuick types are not registered
* QTBUG-129182 tst_qquickwidget::tabKey() is flaky on dev
* QTBUG-129797 qmlcachegen generates code that is incompatible with
QT_NO_CAST_FROM_ASCII
* QTBUG-129599 ListView: ListView sometimes lags / pauses when dragging
it
* QTBUG-129766 Qt build fails with XCode 15.3 and 16
* QTBUG-129799 qmllint: typechecking 'Overlay' attached property fails
* QTBUG-129165 regression ListView not updating count
* QTBUG-129941 tst_declarative_ui (Failed)
* QTBUG-129699 Crash in void
QQuickDeliveryAgentPrivate::clearFocusInScope when closing Application
* QTBUG-129926 The documentation says "two properteis" but there are
four of them
* QTBUG-128843 Crash when Qt QML is built with -ltcg flag
* QTBUG-130080 "SourceProxy is not a type" when Qt is build statically
* QTBUG-67168 DialogButtonBox.DestructiveRole doesn't close the dialog
* QTBUG-129759 Document delegateModel of ComboBox
* QTBUG-111336 [REG 6.3->6.4]
qtdeclarative/examples/quick/pointerhandlers/tabletCanvasDrawing.qml got
broken again
* QTBUG-130143 Crash in QQmlAbstractBinding::removeFromObject()
* QTBUG-128820 qmllint doesn't see properties from base classes
* QTBUG-118691 tst_qquickpixmapcache::slowDevice is flaky
* QTBUG-126090 tst_qquickpixmapcache::slowDeviceInterrupted fails on
macOS and qemu at least
* QTBUG-129943 tst_PointHandler::tabletStylus is flaky
* QTBUG-130095 qmlprofiler doc is empty
* QTBUG-130081 qmlcompiler generated code not compatible with
QT_NO_CAST_FROM_ASCII
* QTBUG-130088 Crash in QQuickDeliveryAgentPrivate::clearHover
* QTBUG-129681 QML imports break on UNC paths that contain `%` chars
* QTBUG-129839 6.8: Programmatically resized window stalls for initial
part of resize animation
* QTBUG-124478 Qt6.5.1 QML - Scrolling issue when using a trackpad on
macOS when there are nested scroll areas
* QTBUG-128932 qmllint disable does not work for missing-type?
* QTBUG-129622 [Reg 6.7.2 -> 6.7.3] Crash in QQuickItem::setX
* QTBUG-122102 mprotect repeatedly fails and triggers SELinux AVC alerts
* QTBUG-128805 qmllint always deduces type of "this" to be "QObject"
* QTBUG-127776 Code completion for return types doesn't work
* QTBUG-130360 [Reg] Button with action doesn't have accessible name if
the action doesn't set Accessible.name
* QTBUG-130511 Xcode build fails: is attached to multiple targets
* QTBUG-125995 Fix aotstats cmake support on Xcode
* QTBUG-130517 PinchHandler unexpectedly resets target's rotation even
if rotationAxis.enabled is false
* QTBUG-130534  libQt6QmlToolingSettings.a is required for user app
configure step
* QTBUG-105488 ptest build to fail when QmlCompiler is used
* QTBUG-120082 ListView: documentation of property `count` is unclear
* QTBUG-119530 QML - screen reader reads twice the title of the
application
* QTBUG-130331 Cannot use VirtualKeyboard when using several modal Popup
* QTBUG-129520 Click/mouseRelease signals are not received by a button
in a Popup if the InputPanel is placed in front of the Popup
* QTBUG-130620 Drag: shows warning about sourceSize when using with
grabToImage()
* QTBUG-130358 qmllint: load plugins before processing commandline
parameters
* QTBUG-130689 There are no  any QML Screen change notifications when
you change the MacBook display resolution
* QTBUG-130349 dom crashes when using nested functions
* QTBUG-129939 [REG: 6.5->6.6] Validator fixup() is now always called
for every key press in SpinBox
* QTBUG-118879 QML ListElement does not work with enums when "as" import
is used
* QTBUG-128269 QQmlEngine destructor hangs on QQmlTypeLoader::invalidate
* QTBUG-129947 tst_QQuickTextEdit::mouseSelection() is flaky on macOS
arm 12/13
* QTBUG-130575 Javascript closure in QML does not directly capture
imported modules
* QTBUG-130087 QML Compiler statistics doesn't shows all modules
* QTBUG-128632 Incorrect qmllint warning about unresolved type
* QTBUG-130536 Disabled MenuItem propagates clicks to underlying mouse
area in drawer
* QTBUG-130820 Documentation for ComboBox find() Method has wrong
enumeration value MatchEndsWidth
* QTBUG-128577 Property "visible" of QML Item seems to affect how mouse
event is delivered
* QTBUG-130522 QML_CONSTRUCTIBLE_VALUE misbehaves on constructors taking
QJSValue
* QTBUG-130084 QML Compiler statistics fail once a single module uses "
--only-bytecode"
* QTBUG-130623 Windows: Resizing dialog with popupType: Popup.Window
shows weird behavior when resizing.
* QTBUG-130880 QMLLS crashes repeatedly
* QTBUG-130900 Typo in Quick docs since 6.8
* QTBUG-130928 Spreadsheet example hangs when select and drag header
along with cell data
* QTBUG-130676 [Reg 6.7.2 -> 6.8.0] TextEdit.textChanged() signal is
emitted too frequently
* QTBUG-130856 Calling replace() on QQuickWindow::data causes a crash
* QTBUG-130867 QQmlComponent::loadFromModule() bug
* QTBUG-82058 tst_QQuickTextInput::setInputMask() is flaky on macOS
* QTBUG-130839 [qmltc] Customizing Overlay.modal attached property
causes compilation errors
* QTBUG-130838 [qmltc] Compilation errors when building a QML component
with aliased attached property
* QTBUG-128935 Cannot dismiss QtQuick popups in QQuickWidget, misplaced
QQuickOverlay
* QTBUG-130767 Incremental QML gc deletes context property
* QTBUG-126680 qmlls should know about implicit imports of nested QML
* QTBUG-127133 Why do I get warning "Multiple C++ types called xxx
found! This violates the One Definition Rule"
* QTBUG-115140 qtdeclarative -unity-build-batch-size 100000 fails
* QTBUG-129030 tst_qquickwindow::visibilityDoesntClobberWindowState()
failed on Ubuntu 24.04 GNOME X11
* QTBUG-129032 tst_QQuickMultiPointTouchArea::nonOverlapping() and
nested() failed on Ubuntu 24.04 GNOME X11
* QTBUG-82052 tst_QQuickTextEdit::linkHover() is flaky on macOS 10.14
* QTBUG-38004 Mac: When you have some TextInput fields in QML with
activeFocusOnTab set then it is not possible to tab to them
* QTBUG-128914 Many examples fail to build when "Build via Junction
Points" is enabled in Qt Creator
* QTBUG-127906 Qt.labs.platform.Menu opens at the wrong location with
scaling enabled
* QTBUG-128126 Native Quick Menu opens in wrong location (Win)
* QTBUG-129241 Crash at QV4::Value::as<T>
* QTBUG-129388 Compilation Units are not completely released on engine
destruction
* QTBUG-129202 FAIL!  :
inputpanelcontrols::tst_inputpanelcontrols::test_worksWithModal()
* QTBUG-129301 QQmlMetaType::prettyTypeName sometimes returns non-pretty
name
* QTBUG-127051 Language server doesn't provide hover documentation for
WebEngineView.url
* QTBUG-128933 Allow to disable mouse panning in ScrollView
* QTBUG-127422 Second QtQuickView doesn't work
* QTBUG-123499 tst_MptaInterop::touchesThenPinch fails in Qt 6
* QTBUG-130582 [REG 6.7.3-6.8.0] MultiEffect with shadowOpacity looks
different than before
* QTBUG-125631 [ios] Regression QMake -> CMake: slow build time due to
file copying and qmlcachegen
* QTBUG-126205 CMake build takes 5x as long to build as qmake build
* QTBUG-130589 [Reg] TreeView editDelegate doesn't get positioned
correctly
* QTBUG-128221 [Reg 6.7.2->6.8.0b3] qmllint no longer fails when
warnings are found
* QTCREATORBUG-31897 simplify qmlls setup
* QTBUG-130991 6.8.0: qtdeclarative examples build fail

### qtactiveqt
* QTBUG-123498 [Reg 6.2.0 -> 6.2.11 (possibly 6.2.3->6.2.4)][ActiveQt]
Resizing QTableView header inside a QAXCLASS freezes COM application
* QTBUG-111760 target_link_libraries(foo INTERFACE Qt::Core) fails for
interface libs with CMake < 3.19 on Windows

### qtmultimedia
* QTBUG-128374 Sporadic crash on QRhiMetal::enqueueSubresUpload()
* QTBUG-110131 QML Camera unloading crash on iOS
* QTBUG-120465 QML Camera unloading crash on iOS
* QTBUG-126592 MediaPlayer never stops on some audio - ffmpeg
* QTBUG-127853 Use cmake's ability to embed frameworks/dylibs (ffmpeg on
iOS)
* QTBUG-128482 QMediaRecorder::setAutoStop crashes if no media backend
is found
* QTBUG-128159 QFFmpegMediaPlayer setMedia assert failure
* QTBUG-129021 Replace usage of deprecated
av_fmt_ctx_get_duration_estimation_method
* QTBUG-112259 QCameraFocus doesn't work properly on iOS
* QTBUG-129232 Fix misleading diagnostics in CMake output when FFmpeg is
not found
* QTBUG-129184 Bad type for GstURIDecodeBin property
* QTBUG-126211 Multiple CMake warnings about missing 'pc' files on
Windows
* QTBUG-129053 Deadlock in tst_qsoundeffect
* QTBUG-129502 Regression in QtMultimedia [6.7->6.8]
* QTBUG-114674 Audio fails silently on iOS 16 following app suspended
* QTBUG-129469 Test #42: tst_qmediaplayerbackend ..........***Failed
* QTBUG-129501 [REG 6.7.2-6.7.3] QMediaRecorder doesn't respect the
output file extension
* QTBUG-129521 QFFmpeg::EncoderThread: use-after-free in unit tests
* QTBUG-129587 Build failure: -Werror in pipewire/spa header
* QTBUG-129714 Document programmatic IO APIs as only supported with
FFmpeg media backend
* QTBUG-129712 Test timed out:
makeCustomGStreamerCamera_fromPipelineDescription_userProvidedGstElement
* QTBUG-129825 qplatformaudiobufferinput_p.h(41): error C2332: 'struct':
missing tag name
* QTBUG-129597 Assertion error, QSoundEffect object creation on worker
thread using QtConcurrent
* QTBUG-116671 Fix capture_capturesToFile_whenConnectedToMediaRecorder
on linux CI
* QTBUG-46409 tst_qaudiodeviceinfo fails in RHEL
* QTBUG-128421 [Android] Recorder example is not able to record video
* QTBUG-130348 Update documentation for QMediaRecorder::actualLocation
and outputLoction
* QTBUG-112512 QSoundEffect cuts out on very short sounds ( ~ 0.2 - 0.3
seconds )
* QTBUG-130441 Configuring Qt Multimedia fails even if -no-feature-
ffmpeg is specified
* QTBUG-130488 qt6_add_ios_ffmpeg_libraries wrongly uses APPEND on a
flag CMake var
* QTBUG-128369 [EVR] Access violation on
EVRCustomPresenter::processOutput()
* QTBUG-130600 [gstreamer] Intel IPU6 camera shows up as multiple
devices
* QTBUG-130387 [gstreamer] QMediaRecorder - recorder broken when audio
input present
* QTBUG-130668 QSoundEffect::setSource does not change audio source
* QTBUG-128738 MediaPlayer on android device can't find default audio
output
* QTBUG-126567 Android 14 QMediaPlayer plays sound using speakers
instead of headphones
* QTBUG-128412 [WASM] declarative-camera example does not allow
capturing images, viewing captured photos, and playing back video
* QTBUG-128413 [WASM] Changing camera in declarative-camera example does
not work
* QTBUG-118594  QML Camera wrong Orientation on iOS
* QTBUG-130719 FAIL!  :
tst_QWindowCaptureBackend::capturedImage_equals_imageFromGrab(single-
pixel-window)
* QTBUG-127543 QSoundEffect/SoundEffect audioDevice property has no
effect when device is changed
* QTBUG-130813 qt_add_ios_ffmpeg_libraries does not generate
SwiftSupport folder so AppStore rejects!
* QTBUG-131300 QMultimedia module build fails in Boot2Qt / Yocto
* QTBUG-112014 QMediaPlayer hangs up on setPosition(...) when using
gstreamer backend
* QTBUG-124372 After seeking using the GStreamer backend, the stream
goes into a paused state.
* QTBUG-126799 [gstreamer] playback rate / seeking unreliable
* QTBUG-129078 Unit test failures on Android Samsung Galaxy S6 Lite
* QTBUG-127565 Top flaky test: tst_qmediaplayerbackend::finiteLoops
* QTBUG-128838 Regression after unification of video frame
transformations
* QTBUG-111926 QFlags doesn't support large (>  sizeof(int)) enums
* QTBUG-129570 moc can no longer create meta objects for private classes
(that aren't Q_OBJECT themselves)
* QTBUG-126276 QMediaRecorder fails to encode to Matroska file format
with some codecs
* QTBUG-129486 re-enable test for gstreamer without blocking the
dependency updater
* QTBUG-129692 [darwin] Sporadic crashes on QMediaPlayer destuction
* QTBUG-121542 Video playback with QtMultimedia stutters when using
d3d11 backend, WindowsMediaFoundation, and having an animation on the
scene.
* QTBUG-117099 Video jerks when playing (Windows backend)
* QTBUG-110453  tst_QVideoWidget::fullScreen fails with Android target
in RHEL-8.4
* QTBUG-126816 Deadlock in QDarwinAudioSource while stopping
disconnected device
* QTBUG-118310 QML Camera - setting WhiteBalance, Exposure, ISO doesn't
work as expected
* QTBUG-129831 QCamera::setCameraDevice has unclear behavior
* QTBUG-124517 [gstreamer] GST_MESSAGE_BUFFERING not delivered if
(uri)decodebin doesn't contain a queue
* QTBUG-125251 [gstreamer] spurious assertion failure on shutdown

### qttools
* PYSIDE-2863 pyside6-lupdate do not attribute comment to corresponding
text
* QTBUG-120186 qFpClassify function appears twice (for each overload) in
the docs
* QTBUG-128926 QDoc: When linked against clang from LLVM 19, QDoc
segfaults when generating qt3d documentation
* QTBUG-128644 QDoc fails to compile against Clang-19 RC1-RC4, Clang 20
* QTBUG-129503 Reg->6.7.3: In Qt Designer, the widgets' Layout Alignment
option is ineffective (unable to generate corresponding code)
* PYSIDE-2492 uic does not generate enumeration name into enum values
causing type checking warnings
* QTBUG-127179 Qt Creator puts wrong fields for spacer objects
* QTBUG-128365 Wrong "Line"  (QFrame) orientation
* QTBUG-127051 Language server doesn't provide hover documentation for
WebEngineView.url
* QTBUG-129833 The Context Sensitive Help example is not working
correctly
* QTBUG-130502 Qt6LinguistTool CMake Policy CMP0007 not met
* QTBUG-23140 linguist loses origin attribute in xliff files
* QTBUG-17307 Incorrect processing of xliff file format with multiple
<file> entries

### qtdoc
* QTBUG-127851 Car rendering example breaks qtdoc builds with examples,
if CMake version is below 3.21.1
* QTBUG-128729 qtdoc module fails yocto build
* QTBUG-128436 new ARM-based desktop platforms are not mentioned in
What's New
* QTBUG-128673 [DocumentViewer] The app crashes on Linux when asserting
an instance of RuntimeLoader QML Type
* QTBUG-129080 CMake / ninja doesn't build plugins by default
* QTBUG-114998 Example can't run, missing module
* QTBUG-129444 Wrong image shown in Qt Multimedia "Media Player"
examples
* QTBUG-129569 Documentation linking to 'Qt Quick', 'Qt Widgets' now
incorrectly point to example sections
* QTBUG-129390 PaddedRectangle is not exposed from QtQuick.Controls
anymore
* QTBUG-129773 Mark Qt HTTP Server, Qt Protobuf, and Qt GRPC as
supported Add-On modules
* QTBUG-129559 Links to "The Qt Resource System" points to the Android
docs
* QTBUG-128455 [VxWorks] configure doesn't recognize graphics settings
* QTBUG-100100 Demos should use `qt6_add_qml_module` instead of
`qt6_add_resources`
* QDS-13600 Replace deprecated FetchContent_Populate
* QTBUG-129628 Building Qt6 from Git for Windows fails when following
the available documentation
* QTBUG-125322 INSTALL_EXAMPLESDIR is missing from demos/todolist's
CMakeLists.txt
* QTBUG-130352 Update webOS page with current webOS and Qt version

### qtlocation
* QTBUG-128806 Wrong instructions for adding QGeoJson to project
* QTBUG-130139 Flickable: an outer flickable can sometimes be stuck in
dragging mode when dragging on an inner flickable

### qtsensors
* QTBUG-128167 The android implementation is using an
obsolete/deprecated/removed function ALooper_pollAll

### qtconnectivity
* QTBUG-129763 qapduutils.cpp fails to compile on mingw developer build
with -force-asserts
* QTBUG-129977  Reading or writing to NFC tag gives an exception on
iPhone
* QTBUG-129944 A "strong assertion" does not help safely exclude
android.permission.ACCESS_FINE_LOCATION from manifest
* QTBUG-117358 BLUETOOTH_SCAN permission flag neverForLocation
* QTBUG-112164 Check ACCESS_FINE_LOCATION is no longer needed in recent
Android Sdk

### qtwayland
* QTBUG-105843 Broken cursor changing on Wayland with tablet input
* QTBUG-123776 Missing tablet cursor. Set tablet cursor on Wayland with
zwp_tablet_tool.set_cursor
* QTBUG-128350 QWaylandBufferRef::toOpenGLTexture leaks textures
* QTBUG-127980 Segmentation fault after Qt.quit()
* QTBUG-129203 FAIL!  : qml::WindowItem::test_childrenZOrder() 'function
returned false' returned FALSE
* QTBUG-129630 QRhiWidget not shown on Wayland
* QTBUG-129403 [Boot2Qt][Wayland] Getting "eglSwapBuffers failed with
0x300d" error when trying to run RHI widget example
* QTBUG-129584 [REG 6.7.3] Wayland text input v3: input method window no
longer updates its positions
* QTBUG-126275 [REG Qt 6.6.3 -> 6.7.0] Wayland: Can't scroll with
mousewheel in editor
* QTBUG-127821 DragHandler and DropArea interaction might cause a stuck
mousegrab
* QTBUG-130581 Virtual Keyboard Hints are not reported for the second
top level wayland window
* QTBUG-130128 Wayland: Crash when nesting popups / (custom editor
provided by an item delegate)
* QTBUG-128029 wayland: Window container in QMdiArea does not work

### qt3d
* QTBUG-129701 [Qt3D] Loading of builtin shaders broken
* QTBUG-128939 [REG 6.8.0 RC snapshot -> 6.8.0 RC snapshot]
Unredistributable files in qt3d
* QTBUG-106079 qmllint produces warnings from Qt3D imports and
components

### qtserialport
* QTBUG-128487 Difference between QSerialPortInfo on Windows and Linux

### qtwebsockets
* QTBUG-130500 Various network tests are failing on macOS 15

### qtwebengine
* QTBUG-128784 OpenGL context creation issues when D3D11 RHI is used
(sic)
* QTBUG-108763 Incorrect documentation for
QWebEngineUrlRequestInterceptor.interceptRequest
* QTBUG-128241 HTML selection tag crashes app when clicked on
* QTBUG-128897 Pure virtual function call on
NativeSkiaOutputDevice::Present()
* QTBUG-120248 [Qt WebEngine] More configure-time checks and
documentation for required libraries
* QTBUG-128857 Qt WebEngine underperforms compared to Google Chrome by
factor of  2 ~ 3
* QTBUG-104065 [REG 6.2->6.3] QtWebEngine font color issue
* QTBUG-129884 Webengine tests hang after
qmltests::GetUserMedia::test_getUserMedia(desktop video) on Windows 11
* QTBUG-130034 Top flaky test:
tst_qwebenginepage::getUserMediaRequestDesktopVideoManyPages
* QTBUG-130035 Top flaky test: tst_qwebenginepage::getUserMediaRequest
* QTBUG-127726 Screen sharing crashes in DesktopCapturer
* QTBUG-130327 Missing closing bracket in QWebEngineUrlSchemeHandler
documentation
* QTBUG-129796 Blocking main frame request from a Google Search crashes
the process
* QTBUG-130500 Various network tests are failing on macOS 15
* QTBUG-129826 [6.8] Minimum python version isn't correct anymore
* QTBUG-130599 [Regr: 6.7->6.8]JavascriptCanAccessClipboard doesn't
allowing copying to clipboard on 6.8
* QTBUG-130790 error: 'cortex-a53' does not support feature 'crc'
* QTBUG-131397 WebEngineProfile doesn't instantiate in QML if property
declarations are in a specific order
* QTBUG-128653 tst_qquickwebengineview failed on
ubuntu-24.04-arm64-offscreen-tests
* QTBUG-128652 tst_qmltests crashed on ubuntu-24.04-arm64-offscreen-
tests
* QTBUG-126317 libexec/gn on MacOS is not universal

### qtwebview
* QTBUG-102712 qtwebview tests fail on Android
* QTBUG-108752 tst_QQuickWebView::settings_JS fails on Android 12
* QTBUG-129303 [Android] WebView.loadHtml() fails to correctly encode
certain strings?

### qtdatavis3d
* QTBUG-128460 Main window crashes/black out when QtDataVisualization 3D
chart in QMdiSubWindow destroyed

### qtvirtualkeyboard
* QTBUG-130382 Can't disable Korean layout in yocto recipe
* QTBUG-123415 [Qt Virtual Keyboard] Example produces lots of warnings
at startup

### qtspeech
* QTBUG-108205 tst_QTextToSpeech::pauseResume(darwin) fails on macOS 13
in CI

### qtnetworkauth
* QTBUG-129590 tst_oauth2 SSL certificate usage fails
* QTBUG-129291 Use 127.0.0.1 instead of localhost as default in
QOAuth2AuthorizationCodeFlow

### qtremoteobjects
* QTBUG-130628 Assert fail in tst_usertypes::complexInQml

### qtlottie
* QTBUG-118877 -qreal float configuration option does not compile

### qtquicktimeline
* QTBUG-122812 Binding is not restored for Timeline component

### qtquick3d
* QTBUG-128922 Invalid frustum dimensions in shadowmap shader
* QTBUG-129140 [REG] Lightprobe using texture data causes crash
* QTBUG-127760 qtdoc dice example debug assertion failure
* QTBUG-129990 QtQuick3D.Xr crashes if the runtime doesn't support depth
swapchains
* QTBUG-129807 qtquick3d doc generation fails without system OpenXR
* QTBUG-130398 volumeraycaster example can fail to start on Android
* QTBUG-130680 Building instructions visionOS
* QTBUG-130381 quick3d/embree: AVX code paths not disabled with GCC 14
* QTBUG-128352 Potential thread safety issue in many Qt Quick 3D
examples
* QTBUG-129395 Qt Dice on mobile is "jumpy" while zooming
* QTBUG-126316 Wrong timing for animations in XR
* QTBUG-130647 hand property is missing in XrInputAction doc
* QTBUG-131361 Intel skylake fails to build for Boot2Qt lts-6.5(.8)

### qt5compat
* QTBUG-130392 Error: no matching function for call to
‘QChar::QChar(const qle_ushort&)
* QTBUG-122795 Incompatibility in QTextCodec between Qt5 and Qt6 (lack
of BOM)

### qtopcua
* QTBUG-128749 qtopcua generates warnings about using
OpenSSL3-deprecated API
* QTBUG-126631 AddressSanitizer: heap-use-after-free in tst_opcua

### qtlanguageserver
* QTBUG-115140 qtdeclarative -unity-build-batch-size 100000 fails

### qthttpserver
* QTBUG-129798 Two-way communication for QWebSockets created in
QHttpServer does not work
* QTBUG-129773 Mark Qt HTTP Server, Qt Protobuf, and Qt GRPC as
supported Add-On modules
* QTBUG-130500 Various network tests are failing on macOS 15

### qtgrpc
* QTBUG-129204 qgrpchttp2channel.cpp:19:10: fatal error:
'QtNetwork/qlocalsocket.h' file not found
* QTBUG-129918 [FTBFS] gtgrpc: CMake Error: AUTOMOC for target
protocplugintestcommon: The "moc" executable "xxxx" does not exist.
* QTBUG-125406 QtGrpc: rework documentation
* QTBUG-128753 Protobufgen/grpcgen tests override their results

### qtgraphs
* QTBUG-128432 Graph Gallery example shows broken UI when resizing the
window
* QTBUG-127769 Animation does not work in tst_directional
* QTBUG-128799 The Graph Gallery crashes on launch on Android device
* QTBUG-128490 Flickering when a single pie slice is shown in PieSeries
* QTBUG-128889 WASM examples for 3D crash at start
* QTBUG-128661 Barseries visibility signal called twice when changing
labels visibility
* QTBUG-128863 connection issues when replacing barsets
* QTBUG-129162 Add bound checks to QXYSeries
* QTBUG-129272 XYSeries count is an invokable function instead of a
property
* QTBUG-129336 XYSeries pointsReplaced signal is not connected to update
* QTBUG-129054 [Boot2Qt] Surface of the graph is black when running the
example app on RPi device
* QTBUG-129357 Multiple crashes while animating series
* QTBUG-129352 [Boot2Qt] Cannot build "Cockpit" example app for Boot2Qt
device on Windows machine
* QTBUG-129497 Linker error with QGraphsLine::swap: unresolved external
symbol
* QTBUG-129381 Double signaling in DateTimeAxis
* QTBUG-130507 Crash when mouse pressing PointRenderer graphs
* QTBUG-130013 Setting selection item label visibility to false does not
work
* QTBUG-130722 Bar3DSeries columnLabels and rowLabels not working.
* QTBUG-130010 userDefinedMesh is ignored
* QTBUG-130011 Changing selection pointer mesh with Surface3D does not
work
* QTBUG-130870 Selection pointer does not follow highlight color
immediately
* QTBUG-127800 Graphs3D namespace docs are missing from QML
* QTBUG-131123 Docs mention non-existent Graphs3D.CameraPreset.None enum
value
* QTBUG-131124 GraphsTheme documentation ambiguities
* QTBUG-131366 Incorrect import and linking target hint for
Q3DSurfaceWidgetItem
* QTBUG-128898 qmlTestBed barModelMapping not working correctly
* QTBUG-130306 Documentation with source code mismatch
* QTBUG-130649 Invalid GraphTheme code snippet in QtGraphs Documentation
* QTBUG-130655 Qt Graphs GraphsTheme gridVisible: false does not hide
the grid
* QTBUG-131131 Graphs3D related documentation bugs

### qtapplicationmanager (Commercial only)
* QTBUG-129814 applicationmanager\application-
features\apps\Glitches\Glitches\glitches.cpp(4): fatal error C1083:
Cannot open include file: 'unistd.h': No such file or directory
* QTBUG-130117 build time paths used in appman binaries
* QTBUG-130388 application-features example has broken
* QTBUG-129488 FAIL!  : qml::BubbleWrap::test_bubblewrap() 'wait for
signal windowAdded' returned FALSE. ()
* QTBUG-130554 tst_Signature::check() fails on macOS 15

### qtinterfaceframework (Commercial only)
* QTBUG-130868 tst_simulation_backend_static (Failed)
* QTBUG-130082 Doc: wrong annotation name for defaultServerMode

### qtvncserver (Commercial only)
* QTBUG-128535 QVncServer documentation is missing some signals

Known Issues
------------

* Check that your system meets Qt's requirements:
https://doc.qt.io/qt-6.8/supported-platforms.html
* RTA reported issues from Qt 6.8
https://bugreports.qt.io/issues/?filter=26458
* See Qt 6.8 known issues from:
https://wiki.qt.io/Qt_6.8_Known_Issues
* Qt 6.8.1 Open issues in Jira:
https://bugreports.qt.io/issues/?filter=26843

Credits for the  release goes to:
---------------------------------

Eirik Aavitsland  
Laszlo Agocs  
Dilek Akcay  
Owais Akhtar  
Konsta Alajärvi  
Anu Aliyas  
Even Oscar Andersen  
Soheil Armin  
Alessandro Astone  
Andreas Bacher  
Mate Barany  
Vladimir Belyavsky  
Nicholas Bennett  
Lena Biliaieva  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
Tatiana Borisova  
Joerg Bornemann  
Rym Bouabid  
Assam Boudjelthia  
Sven Brauch  
Kai Uwe Broulik  
Michael Brüning  
Olivier De Cannière  
Alexei Cazacov  
Brian Chan  
Kaloyan Chehlarski  
Wang Chuan  
Ed Cooke  
Alexandru Croitor  
Kenneth Culver  
Mitch Curtis  
Giuseppe D'Angelo  
Pavel Dubsky  
Artem Dyomin  
Alexey Edelev  
David Edmundson  
Oliver Eftevaag  
Christian Ehrlicher  
Hatem ElKharashy  
Andreas Eliasson  
David Faure  
Nicolas Fella  
Andrew Forrest  
Dheerendra FullName  
Simo Fält  
Zoltan Gera  
Robert Griebl  
Johannes Grunenberg  
Kaj Grönholm  
Richard Moe Gustavsen  
Lucie Gérard  
Mikko Hallamaa  
Jøger Hansegård  
Inkamari Harjula  
Elias Hautala  
Tero Heikkinen  
Jani Heikkinen  
Moss Heim  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Dominik Holland  
Zhang Hongyuan  
Mats Honkamaa  
Samuli Hölttä  
Masoud Jami  
Morteza Jamshidi  
Allan Sandfeld Jensen  
Jonas Karlsson  
Ahmed El Khazari  
Ali Kianian  
Friedemann Kleint  
André Klitzing  
Michal Klocek  
Jarek Kobus  
Niko Korkala  
Tomi Korpipaa  
Fabian Kosmale  
Volker Krause  
Mike Krus  
Santhosh Kumar  
Jonas Kvinge  
Kai Köhne  
Inho Lee  
Paul Lemire  
Wladimir Leuschner  
Thiago Macieira  
Łukasz Matysiak  
Shveta Mittal  
Safiyyah Moosa  
Bartlomiej Moskal  
Marc Mutz  
Tommi Mänttäri  
Antti Määttä  
Andy Nichols  
Mårten Nordheim  
Dennis Oberst  
Tinja Paavoseppä  
Jerome Pasion  
Samuli Piippo  
Karim Pinter  
Timur Pocheptsov  
Milla Pohjanheimo  
Joni Poikelin  
Aleix Pol  
Rami Potinkara  
Lorn Potter  
Sakaria Pouke  
Dheerendra Purohit  
MohammadHossein Qanbari  
Liang Qi  
Khem Raj  
Matthias Rauter  
David Redondo  
Topi Reinio  
Shawn Rutledge  
Toni Saario  
Ahmad Samir  
Lars Schmertmann  
Carl Schwan  
Luca Di Sera  
Sami Shalayel  
Jiu Shanheng  
Nils Petter Skålerud  
Ivan Solovev  
Axel Spoerl  
Christian Strømme  
Tarja Sundqvist  
Lars Sutterud  
Tasuku Suzuki  
Morten Sørvig  
Sadegh Taghavi  
HIDAKA Takahiro  
Samuel Thibault  
Phil Thompson  
Elias Toivola  
Orkun Tokdemir  
Jere Tuliniemi  
Paul Olav Tvete  
Esa Törmänen  
Tuomas Vaarala  
Sami Varanka  
Peter Varga  
Doris Verria  
Tor Arne Vestbø  
Petri Virkkunen  
Juha Vuolle  
Olli Vuolteenaho  
Jaishree Vyas  
Jannis Völker  
Michael Weghorn  
Edward Welbourne  
Paul Wicking  
Piotr Wierciński  
Oliver Wolff  
Semih Yavuz  
Marianne Yrjänä  
Zhao Yuhang  
Michał Łoś  
