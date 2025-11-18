Release note
============
Qt 6.10.1 release is a patch release made on the top of Qt 6.10.0.
As a patch release, Qt 6.10.1 does not add any new functionality but provides
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
* [CVE-2025-12385](https://nvd.nist.gov/vuln/detail/CVE-2025-12385) in qtdeclarative

### qtbase
* 97790e91ae6 Add camel-case header for qtconcurrenttask.h
Added a camel-case QtConcurrentTask header, which is the same as
QtConcurrent/qtconcurrenttask.h.

* ddd5da17ebb Respect QT_NO_INT128 in qtypes.cpp's #error
Made it possible to compile Qt with GCC in strict C++ mode (-ansi or
-std=c++NN) again, provided QT_NO_INT128 is defined, too.

* 91ebf84d17b Upgrade Harfbuzz to 11.4.5
Upgraded Harfbuzz to version 11.4.5.

* c7574605254 Update bundled libjpeg-turbo to version 3.1.2
libjpeg-turbo was updated to version 3.1.1

* 95a267d8673 QStringConverter: allow appendToBuffer() to write to the
buffer
The appendToBuffer() functions in QStringEncoder and QStringDecoder may
write to parts of the provided output beyond the returned pointer.
Caller code must not assume the data beyond that remains unmodified.

* 05287da820e Update Freetype to 2.14.0
Updated bundled Freetype to 2.14.0.

* 6e6639d6693 Make QTEST_THROW_ON_FAIL work from within QtConcurrent
Fixed a bug which prevented QTEST_THROW_ON_FAIL and QTEST_THROW_ON_SKIP
from working with QCOMPARE(), QVERIFY(), and QSKIP() invoked from within
QtConcurrent functions.

* 486f712fc0d Upgrade Harfbuzz to 11.5.0
Upgraded Harfbuzz to version 11.5.0.

* 8e08522adc2 Update Freetype to 2.14.1
Updated bundled Freetype to 2.14.1.

* 9a8bf3b4bb0 QDBusReply: apply Rule Of Zero
Enabled move constructor and move assignment operator.

* 660bfd8415c Upgrade Harfbuzz to 11.5.1
Upgraded Harfbuzz to version 11.5.1.

* a51cfd7d85c Android: Update to Gradle 8.14.3
Updated Gradle to 8.14.3.

* 59d2f38c410 Upgrade Harfbuzz to 12.1.0
Upgraded Harfbuzz to version 12.1.0.

* 7196bb00ed7 QString: fix overly-eager arg(int-ish) overload
Fixed the integral arg() overload to reject types that merely
implicitly convert to an integral type. This was always the intent, but
6.9 and 6.10.0 incorrectly accepted types that implicitly convert to
float to match this overload, causing truncated results. We now reject
such types. A backwards-compatible fix is to cast such types to a C++
type whose displayed form matches your intent.

* 41c410f2125 CMake: Relax handling of CMP0156 policy
CMake user projects will now use CMake's default value for the CMP0156
policy, except for Apple and Emscripten platforms which are forced to
NEW (when the policy is available).

* aefee5fea5b Upgrade PCRE2 to 10.47
PCRE2 was updated to version 10.47.

* b7e7661a70d Don't claim that PCRE2 is optional
Don't claim that using PCRE2 is optional.

* 2f590dbcd66 Http: Set error to 'TimeoutError' for a transfer timeout
The error set when a request times out due to
QNetworkRequest::setTransferTimeout() has been changed to
QNetworkReply::TimeoutError, to disambiguate from the previously used
QNetworkReply::OperationCanceledError.

* 61f21a89d6e macOS: Disable window-modal native message boxes on Tahoe
Window-modal message boxes are no longer backed by native NSAlerts on
Tahoe, due to a bug that prevents the alert from responding to mouse
events for its buttons.

* 943262dce2b SQLite: Update SQLite to v3.51.0
Updated SQLite to v3.51.0

* 90b845d15ff Upgrade Harfbuzz to 12.2.0
Upgraded Harfbuzz to version 12.2.0.

### qtdeclarative
* 461b0df0b4 Make defaultDelegate compatible with TreeModel and
TableModel
Changed the order of the role and value parameters in setData to
resolve ambiguity.

* 600cb8d8dd Initialize QQuickGradientStop position to zero
The position property is now always initialized to 0.0; previously it
was left uninitialized.

* 9b86adf5dc CMake: Add plugin options to
qt_generate_deploy_qml_app_script
Added NO_PLUGINS, EXCLUDE_PLUGINS, EXCLUDE_PLUGIN_TYPES,
INCLUDE_PLUGINS, and INCLUDE_PLUGIN_TYPES options to
qt_generate_deploy_qml_app_script.

* 469c1e5ba0 qmllint: Also lint inner functions
qmllint will now lint inner functions, defined in javascript, in
addition to top-level functions and bindings.

* d50548e83 Update FFmpeg version in documentation
Updated FFmpeg to n7.1.2.

### qtimageformats
* f40dd4b Update bundled libtiff to version 4.7.1
Bundled libtiff was updated to version 4.7.1

### qtlottie
* 132982c Doc: Fix module name in qt_attribution.json files
Fixed Qt Lottie Animation module name in license source files.

### qtgrpc
* d93ce3b3 QGrpcHttp2Channel: Report data loss for incomplete trailing
messages
finishes the communication with a non-ok QGrpcStatus (DataLoss) when
the stream is closed with unprocessed trailing data.


Fixes
-----

### qtbase
* [QTBUG-139439](https://bugreports.qt.io/browse/QTBUG-139439) CMake fails due to 'pthread_cancel' when configuring Qt
project for Android with CMake 4.x
* [PYSIDE-3173](https://bugreports.qt.io/browse/PYSIDE-3173) Emojis on Button Label Silently Crash PySide App
* [QTBUG-138678](https://bugreports.qt.io/browse/QTBUG-138678) Crash in QTextEdit while inserting a column into a HTML
table
* [QTBUG-139291](https://bugreports.qt.io/browse/QTBUG-139291) showMaximized() does not maximize QDialog
* [QTBUG-139720](https://bugreports.qt.io/browse/QTBUG-139720) Tag errors in QtAbstractItemModel for Java
* [QTBUG-139688](https://bugreports.qt.io/browse/QTBUG-139688) Public Java Classes Documentation Bugs
* [QTBUG-134082](https://bugreports.qt.io/browse/QTBUG-134082) Screen orientation change causes rendering issues on Qt
Quick Application (flicker related)
* [QTBUG-124140](https://bugreports.qt.io/browse/QTBUG-124140) [REG]: 6.7.0  full-screen app displays background window
(or splash-screen) graphics at top/bottom during multiwindow split
display
* [QTBUG-102020](https://bugreports.qt.io/browse/QTBUG-102020) Incorrect layout in QTabBar when last tab is hidden
* [QTBUG-139791](https://bugreports.qt.io/browse/QTBUG-139791) Buttons don't work when the last tab is hidden
* [QTBUG-139983](https://bugreports.qt.io/browse/QTBUG-139983) macOS (Tahoe): assert in
tst_QStyleSheetStyle::complexWidgetFocus()
* [QTBUG-135354](https://bugreports.qt.io/browse/QTBUG-135354) wayland\custom-extension and wayland\custom-shell
examples fails to build with Boot to Qt on Windows
* [QTBUG-135808](https://bugreports.qt.io/browse/QTBUG-135808) Some problems with Expanded Client Areas on Android
* [QTBUG-140064](https://bugreports.qt.io/browse/QTBUG-140064) error: array subscript 'QTransform[0]' is partly outside
array bounds of 'QVariant [1]'
* [QTBUG-139990](https://bugreports.qt.io/browse/QTBUG-139990) [REG 6.10.0 beta 3 -> beta 4] Building Qt examples for
WebAssembly fails
* [QTBUG-140149](https://bugreports.qt.io/browse/QTBUG-140149) multimedia: unity builds broken on macos
* [QTBUG-140150](https://bugreports.qt.io/browse/QTBUG-140150) [cmake] qconfig.h and friends generated without
inclusion guards
* [QTBUG-139202](https://bugreports.qt.io/browse/QTBUG-139202) Button colors are wrong in dark mode on Windows 11
* [QTBUG-138094](https://bugreports.qt.io/browse/QTBUG-138094) Radiobuttons/Checkboxes in windows11 style do not follow
WinUI3 style
* [QTBUG-138848](https://bugreports.qt.io/browse/QTBUG-138848) Content-Length header always sent in HTTP GET request
* [QTBUG-140058](https://bugreports.qt.io/browse/QTBUG-140058) Tracepointgen doesn't generate metadata for enums
* [QTBUG-139989](https://bugreports.qt.io/browse/QTBUG-139989) FAIL!  : tst_QStateMachine::twoAnimations() Compared
values are not the same
* [QTBUG-139944](https://bugreports.qt.io/browse/QTBUG-139944) macOS: title/text alignment on push buttons
* [QTBUG-140172](https://bugreports.qt.io/browse/QTBUG-140172) [qtbase] Build failure in wayland plugin with -no-opengl
* [QTBUG-140192](https://bugreports.qt.io/browse/QTBUG-140192) tst_qwidget (Failed) - tst_QWidget::resizeEvent()
Compared values are not the same
* [QTBUG-139765](https://bugreports.qt.io/browse/QTBUG-139765) QTEST_THROW_ON_FAIL doesn't work from inside
QtConcurrent
* [QTBUG-139040](https://bugreports.qt.io/browse/QTBUG-139040) Unreadable image on https://doc.qt.io/qt-6/animation-
overview.html
* [QTBUG-140126](https://bugreports.qt.io/browse/QTBUG-140126) QNetworkReply::errorString shows misleading "server
replied:" with no reason phrase for HTTP/2/3 responses
* [QTBUG-137927](https://bugreports.qt.io/browse/QTBUG-137927) Combining Qt::ExpandedClientAreaHint with
Qt::CustomizeWindowHint breaks mouse event handling
* [QTBUG-139617](https://bugreports.qt.io/browse/QTBUG-139617) Non-deterministic tst_QThread failures
* [QTBUG-138596](https://bugreports.qt.io/browse/QTBUG-138596) App fails to build with qmake with static Qt + static
FFmpeg, wrong linker flags
* [QTBUG-140203](https://bugreports.qt.io/browse/QTBUG-140203) [qtbase] Build failure with -no-ssl
* [QTBUG-139790](https://bugreports.qt.io/browse/QTBUG-139790) QFuture<T> cannot be passed to a method expecting
QFuture<void>
* [QTBUG-139690](https://bugreports.qt.io/browse/QTBUG-139690) SwipeView Android Expanded Client Area hides
NavigationBar
* [QTBUG-140053](https://bugreports.qt.io/browse/QTBUG-140053) Suspect QLockFail::lock() may fail sporadically on
Windows
* [QTBUG-139425](https://bugreports.qt.io/browse/QTBUG-139425) Wayland: QEventLoop::ExcludeUserInputEvents doesn't work
* [QTCREATORBUG-33525](https://bugreports.qt.io/browse/QTCREATORBUG-33525) Dockwidgets have app icons icons
* [QTBUG-139924](https://bugreports.qt.io/browse/QTBUG-139924) [REG Qt 6.9.2] Style Sheet is not always applied to
children
* [QTBUG-133332](https://bugreports.qt.io/browse/QTBUG-133332) possible stackoverflow calling setWindowFlag() in style
polish & unpolish
* [QTBUG-139653](https://bugreports.qt.io/browse/QTBUG-139653) Compile Error (GdiplusTypes.h(669): error C3861: 'max':
identifier not found)
* [QTBUG-138459](https://bugreports.qt.io/browse/QTBUG-138459) WindowStaysOnTopHint flag removes fullscreen on window
* [QTBUG-139605](https://bugreports.qt.io/browse/QTBUG-139605) windows11style: crash when drawing slider due to failure
to check for null value
* [QTBUG-140516](https://bugreports.qt.io/browse/QTBUG-140516) qtbase/src/tools/bootstrap can't be built for Android
* [QTBUG-137248](https://bugreports.qt.io/browse/QTBUG-137248) color scheme issue on Android with expanded client area
* [QTBUG-140649](https://bugreports.qt.io/browse/QTBUG-140649) Windows11Style: Fix QSlider layouting
* [QTBUG-140536](https://bugreports.qt.io/browse/QTBUG-140536) Android can't be built without EGL
* [QTBUG-136110](https://bugreports.qt.io/browse/QTBUG-136110) [Reg 6.8->6.9] Crash when opening popup (when creating
new C++ class) (Wayland protocol error)
* [QTBUG-140509](https://bugreports.qt.io/browse/QTBUG-140509) Main ABI libs are littered by secondary ABI libs
* [QTBUG-136493](https://bugreports.qt.io/browse/QTBUG-136493) FFmpeg not properly configured with multi-abi builds
* [QTBUG-140784](https://bugreports.qt.io/browse/QTBUG-140784) /usr/include/c++/11/system_error:398
* [QTBUG-140443](https://bugreports.qt.io/browse/QTBUG-140443) tracepointgen:  Unable to find values for QEvent::Type
* [QTBUG-140207](https://bugreports.qt.io/browse/QTBUG-140207) Crash when rapidly moving a dock widget
* [QTBUG-121879](https://bugreports.qt.io/browse/QTBUG-121879) QT_DEPLOY_QML_DIR example doesn't actually make use of
the value of QT_DEPLOY_QML_DIR
* [QTBUG-139014](https://bugreports.qt.io/browse/QTBUG-139014) Odd update slowdowns on Windows with D3D and Quick
threaded render loop when continuously triggering window updates AND
starting it early
* [QTBUG-137219](https://bugreports.qt.io/browse/QTBUG-137219) Primitive restart does not work with D3D12
* [QTBUG-140689](https://bugreports.qt.io/browse/QTBUG-140689) QToolBar Expansion Button Lacks Native Appearance on
macOS
* [QTBUG-140847](https://bugreports.qt.io/browse/QTBUG-140847) Wayland: QMessageBox content clipped on COSMIC Desktop
* [QTBUG-132285](https://bugreports.qt.io/browse/QTBUG-132285) [Windows] Flickering with high DPI scaling with native
Windows window
* [QTBUG-115992](https://bugreports.qt.io/browse/QTBUG-115992) Window containing native windows window is excessively
repainted on move
* [QTBUG-138471](https://bugreports.qt.io/browse/QTBUG-138471) QString::arg() convert floating type to integer
* [QTBUG-140694](https://bugreports.qt.io/browse/QTBUG-140694) Regression: Android: ImhNoPredictiveText on a text field
prevents text input completely
* [QTBUG-138858](https://bugreports.qt.io/browse/QTBUG-138858) Japanese input does not work well under landscape mode
on Android device
* [QTBUG-37980](https://bugreports.qt.io/browse/QTBUG-37980) Android: GET_EXTRACTED_TEXT_MONITOR flag not supported
* [QTBUG-140795](https://bugreports.qt.io/browse/QTBUG-140795) QRhi D3D11 backend bounds wrong buffers depending on
certain conditions
* [QTBUG-137936](https://bugreports.qt.io/browse/QTBUG-137936) Projects view displays files added by qt_add_resources()
in different subtrees
* [QTBUG-131923](https://bugreports.qt.io/browse/QTBUG-131923) QPainter::drawImage with CompositionMode_Source into
non-alpha image format produces transparent pixels
* [QTBUG-140869](https://bugreports.qt.io/browse/QTBUG-140869) windows: use-after-free
* [QTBUG-139692](https://bugreports.qt.io/browse/QTBUG-139692) HTTP request results in NoError error on GOAWAY
* [QTBUG-138807](https://bugreports.qt.io/browse/QTBUG-138807) [REG: 6.7 -> 6.8] win: QResource::registerResource
crashes if registering .rcc from inside the resource system
* [QTBUG-133410](https://bugreports.qt.io/browse/QTBUG-133410) Highlight faulty functionality of deprecated
QPrinter::PrinterResolution
* [QTBUG-139610](https://bugreports.qt.io/browse/QTBUG-139610) Unwanted pixels are drawn during Japanese text rendering
* [QTBUG-139588](https://bugreports.qt.io/browse/QTBUG-139588) [REG: 5.10->5.11] SE_TabBarScrollLeft/RightButton have
no effect on stylesheet style anymore
* [QTBUG-138960](https://bugreports.qt.io/browse/QTBUG-138960) Fusion + stylesheet setting linear gradient as
background changes border color
* [QTBUG-138567](https://bugreports.qt.io/browse/QTBUG-138567) QUndoStack::redo() does not notify state change when
command becomes obsolete
* [QTBUG-140793](https://bugreports.qt.io/browse/QTBUG-140793) QToolButton::setPopupMode() has no effect if set before
setting the menu
* [QTBUG-140148](https://bugreports.qt.io/browse/QTBUG-140148) Windows11Style: adjust the QToolButton geometry
* [QTBUG-138419](https://bugreports.qt.io/browse/QTBUG-138419) [Reg 6.8.1->6.8.2] QMenu crash on QProcessEvent call
* [QTBUG-140132](https://bugreports.qt.io/browse/QTBUG-140132) Crash after deleting a popup menu in modal dialog event
processing
* [QTBUG-72333](https://bugreports.qt.io/browse/QTBUG-72333) QAbstractItemView::isPersistentEditorOpen not checking
persistent editors
* [QTBUG-140929](https://bugreports.qt.io/browse/QTBUG-140929) QTextEdit/QTextDocument fail to render Emojis on
elements with id
* [QTBUG-138054](https://bugreports.qt.io/browse/QTBUG-138054) QProgressBar with text looks quite strange in Windows 11
style
* [QTBUG-140856](https://bugreports.qt.io/browse/QTBUG-140856) Android software keyboard is not working in landscape
mode
* [QTBUG-141106](https://bugreports.qt.io/browse/QTBUG-141106) Wrong instructions on how to use GuiPrivate
* [QTBUG-140923](https://bugreports.qt.io/browse/QTBUG-140923) Inaccurate QObject::startTimer documentation
* [QTBUG-135304](https://bugreports.qt.io/browse/QTBUG-135304) CMake CMP0177 on Android
* [QTBUG-140917](https://bugreports.qt.io/browse/QTBUG-140917) Update screenshot in "Document Layouts"
* [QTBUG-130805](https://bugreports.qt.io/browse/QTBUG-130805) QTextFormat::FontSizeAdjustment documentation should
explain the value
* [QTBUG-141173](https://bugreports.qt.io/browse/QTBUG-141173) Wrong instructions on how to use CorePrivate
* [QTBUG-140134](https://bugreports.qt.io/browse/QTBUG-140134) Ugly spin boxes on macOS 26 (up/down buttons)
* [QTBUG-141181](https://bugreports.qt.io/browse/QTBUG-141181) What do with CMP0156 and CMake 4
* [QTBUG-135978](https://bugreports.qt.io/browse/QTBUG-135978) Adding -ObjC linking flag breaks iOS build
* [QTBUG-140211](https://bugreports.qt.io/browse/QTBUG-140211) WASM: libQt6Core.a is linked twice
* [QTBUG-141135](https://bugreports.qt.io/browse/QTBUG-141135) QMenu closes when clicking on a separator added by
addSeparator
* [QTBUG-140672](https://bugreports.qt.io/browse/QTBUG-140672) [VxWorks] 6.8.4 -> 6.8.5 build regression on Intel in
qfloat16.h
* [QTBUG-141061](https://bugreports.qt.io/browse/QTBUG-141061) TLS handshake fails for IDN hostnames (non-Punycode) on
Schannel backend
* [QTBUG-113028](https://bugreports.qt.io/browse/QTBUG-113028) QNetworkReply::RemoteHostClosedError error when using
Secure Channel library (configure option -schannel)
* [QTBUG-141128](https://bugreports.qt.io/browse/QTBUG-141128) FAIL!  :
tst_QQuickColorDialogImpl::dialogCanMoveBetweenWindows() Received a
fatal error
* [QTBUG-141100](https://bugreports.qt.io/browse/QTBUG-141100) WA_KeyboardFocusChange is not reset on focus change
through mouse
* [PYSIDE-3217](https://bugreports.qt.io/browse/PYSIDE-3217) Reg->6.10: C++ Enums in Python Qt Widgets designer
plugins no longer work
* [QTBUG-141255](https://bugreports.qt.io/browse/QTBUG-141255) Wrong conversion from ARGB with premultiplied alfa to
FP16
* [QTBUG-141130](https://bugreports.qt.io/browse/QTBUG-141130) WASM: undefined QSemaphore method
* [QTBUG-139345](https://bugreports.qt.io/browse/QTBUG-139345) setWindowIcon(QIcon()) on QMdiSubWindow resets to the
default icon instead of removing the icon
* [QTBUG-140449](https://bugreports.qt.io/browse/QTBUG-140449) disabled radio button that was checked but was set to
false while being disabled, still shows as checked until you hover your
mouse over it
* [QTBUG-141157](https://bugreports.qt.io/browse/QTBUG-141157) QStyleSheetStyle::drawComplexControl draws groove when
only Handle is asked for
* [QTBUG-140452](https://bugreports.qt.io/browse/QTBUG-140452) tst_json crashes under ASAN (MSVC) due to a stack
overflow
* [PYSIDE-3219](https://bugreports.qt.io/browse/PYSIDE-3219) QAbstractItemView.update shadows QWidget.update
* [QTBUG-140208](https://bugreports.qt.io/browse/QTBUG-140208) QAndroidApplication::context() doesn't have all methods
of QJniObject
* [QTBUG-141074](https://bugreports.qt.io/browse/QTBUG-141074) C++23 [[assume]] added in 6.10.0 creates warnings when
compiling in C++20 mode with -Wextra -pedantic
* [QTBUG-141054](https://bugreports.qt.io/browse/QTBUG-141054) QML ScrollView with Text Inputs in WebAssembly shifts
after two left mouse clicks
* [QTBUG-141371](https://bugreports.qt.io/browse/QTBUG-141371) ::copy_file_range falsely(?) returns only
TriStateResult::Failed on failure
* [QTBUG-134441](https://bugreports.qt.io/browse/QTBUG-134441) macOS: keyboard shortcut Meta+D results Ambiguous
shortcut
* [QTBUG-139964](https://bugreports.qt.io/browse/QTBUG-139964) Standard theme menu icons on macOS Tahoe do not match
Apple
* [QTBUG-141099](https://bugreports.qt.io/browse/QTBUG-141099) Regression in Qt 6.10: QWindow is placed at 0,0 by
default, frame is offscreen in Openbox
* [QTBUG-137203](https://bugreports.qt.io/browse/QTBUG-137203) Request to add an option for case sensitivity in
QNetworkRequest::setRawHeader().
* [QTBUG-141079](https://bugreports.qt.io/browse/QTBUG-141079) tst_QGraphicsProxyWidget::touchEventPropagation() does
not work with PM_DefaultFrameWidth > 1
* [QTBUG-140145](https://bugreports.qt.io/browse/QTBUG-140145) Windows11Style: adjust the QPushButton geometry
* [QTBUG-139693](https://bugreports.qt.io/browse/QTBUG-139693) windows11 style: Checked menu items with icons look
strange
* [QTBUG-135628](https://bugreports.qt.io/browse/QTBUG-135628) QCheckbox without text is right cropped
* [QTBUG-141499](https://bugreports.qt.io/browse/QTBUG-141499) windows11 style does not draw arrow for
QStyleOptionButton::HasMenu
* [QTBUG-140467](https://bugreports.qt.io/browse/QTBUG-140467) a11y: Assert hit when using AT-SPI Text's
GetTextBeforeOffset in QLineEdit
* [QTBUG-141388](https://bugreports.qt.io/browse/QTBUG-141388) a11y: Freeze when querying QLineEdit word at offset
matching text length
* [QTBUG-139943](https://bugreports.qt.io/browse/QTBUG-139943) [iOS][Android] TextEdit or TextInput cannot be navigated
using A11y granularity
* [QTBUG-134138](https://bugreports.qt.io/browse/QTBUG-134138) [A11y] ScreenReader reads QML StackView as "unknown" on
windows
* [QTBUG-116886](https://bugreports.qt.io/browse/QTBUG-116886) Fix documentation for QDataStream::Version::6_6
* [QTBUG-141466](https://bugreports.qt.io/browse/QTBUG-141466) [FTBFS] include could not find requested file
"Qt6QmlToolsAdditionalTargetInfo.cmake"
* [QTBUG-135038](https://bugreports.qt.io/browse/QTBUG-135038) QFileSystemModel is leaking nodes
* [QTBUG-141187](https://bugreports.qt.io/browse/QTBUG-141187) Calling QTabBar::addTab/insertTab repeatedly is very
slow (O(N^2)) even if the parent QTabWidget is not visible
* [QTBUG-140789](https://bugreports.qt.io/browse/QTBUG-140789) Calqlatr: System Error
* [QTBUG-141618](https://bugreports.qt.io/browse/QTBUG-141618) Windows 11 x64: MinGW build with GCC 15 fails in third
party error: 'decimal_point' may be used uninitialized
* [QTBUG-139966](https://bugreports.qt.io/browse/QTBUG-139966) QScreen::refreshRateChanged signal is not fired when the
refresh rate changes
* [QTBUG-141245](https://bugreports.qt.io/browse/QTBUG-141245) a11y: Orca screen reader often announces incorrect
QSpinBox value when changing it using arrow keys
* [QTBUG-131115](https://bugreports.qt.io/browse/QTBUG-131115) [VxWorks] QTimezone is not enabled for VxWorks
* [QTBUG-96165](https://bugreports.qt.io/browse/QTBUG-96165) OperationCanceledError instead of TimeoutError with
setTransferTimeout
* [QTBUG-141689](https://bugreports.qt.io/browse/QTBUG-141689) Qt6 on macOS Tahoe: Qt::WindowModal disables clicks on
QMessageBox
* [QTBUG-117832](https://bugreports.qt.io/browse/QTBUG-117832) Qt-6.5 + iOS + QFileDialog::getOpenFileUrl(), unable to
read file content
* [QTBUG-140897](https://bugreports.qt.io/browse/QTBUG-140897) [REG:6.8->6.9.3,6.10.0] QML TextField on Android 16
doesn't show keyboard on first tap.
* [QTBUG-137564](https://bugreports.qt.io/browse/QTBUG-137564) tst_qmovie fails
* [QTBUG-139986](https://bugreports.qt.io/browse/QTBUG-139986) QStateMachine tests aren't running on the CI
* [QTBUG-140038](https://bugreports.qt.io/browse/QTBUG-140038) tst_QGridLayout::spacingsAndMargins fails on Android 15
* [QTBUG-139951](https://bugreports.qt.io/browse/QTBUG-139951) [VxWorks] 6.8.4 -> 6.8.5 regression build failure with
VxWorks 24.03
* [QTBUG-139280](https://bugreports.qt.io/browse/QTBUG-139280) Cannot build QT 6.8 without GNU extensions
* [QTBUG-138580](https://bugreports.qt.io/browse/QTBUG-138580) [REG 6.10.0 beta1 -> beta2] CMake test including all
modules fails
* [QTBUG-140133](https://bugreports.qt.io/browse/QTBUG-140133) tst_QGraphicsProxyWidget::createProxyForChildWidget
fails with non-zero safe area margins
* [QTBUG-117447](https://bugreports.qt.io/browse/QTBUG-117447) Remove *-proxy.html pages in Qt Core
* [QTBUG-138659](https://bugreports.qt.io/browse/QTBUG-138659) QTextBoundaryFinder is copyable (deep-copies lookup
tables), but not movable
* [QTBUG-139676](https://bugreports.qt.io/browse/QTBUG-139676) [a11y] "Switch" role is missing
* [QTBUG-139007](https://bugreports.qt.io/browse/QTBUG-139007) QFileSystemEngine::fillMetaData fails on hostfs
* [QTBUG-139994](https://bugreports.qt.io/browse/QTBUG-139994) Nullptr swapchain dereference in
QBackingStoreDefaultCompositor::flush
* [QTBUG-139586](https://bugreports.qt.io/browse/QTBUG-139586) [Reg 6.9.1->6.9.2] Cannot send broadcast on macOS
anymore
* [QTBUG-66621](https://bugreports.qt.io/browse/QTBUG-66621) webassembly: strings with toUpper() not correct
* [QTBUG-69421](https://bugreports.qt.io/browse/QTBUG-69421) WebAssembly: characters are not displayed properly
* [QTBUG-74511](https://bugreports.qt.io/browse/QTBUG-74511) Possible REG: Wasm changes in qunicodetables will be lost
* [QTBUG-139307](https://bugreports.qt.io/browse/QTBUG-139307) [REG 5.15.19->6.0.3] Windows: Widgets flicker/jitter
when hovering over them in 150% DPI scaling with 'windowsvista' style
* [QTBUG-140189](https://bugreports.qt.io/browse/QTBUG-140189) 347 - tst_qrhi (Failed)
* [QTBUG-140181](https://bugreports.qt.io/browse/QTBUG-140181) Build failure in QtDeclarative with latest nightly
libc++
* [QTBUG-137048](https://bugreports.qt.io/browse/QTBUG-137048) qdoc: Warn about self-link in \sa
* [QTBUG-29917](https://bugreports.qt.io/browse/QTBUG-29917) QDBusReply::error() should be const
* [QTBUG-140627](https://bugreports.qt.io/browse/QTBUG-140627) 499 - tst_qrhiwidget (Failed)
* [QTBUG-140643](https://bugreports.qt.io/browse/QTBUG-140643) QLocale::timeFormat(QLocale::NarrowFormat) returns
seconds for some locales
* [QTBUG-139128](https://bugreports.qt.io/browse/QTBUG-139128) QObject::connect(): clarify what a valid method is, in
the string-based overloads
* [QTBUG-130278](https://bugreports.qt.io/browse/QTBUG-130278) [Reg 6.7.2 -> 6.8.0][macOS] QLocale::LongFormat no
longer produces reversible conversion between QDateTime and QString
* [QTBUG-140494](https://bugreports.qt.io/browse/QTBUG-140494) QAbstractItemView with AStyledItemDelegate and
Windows11Style
* [QTBUG-100377](https://bugreports.qt.io/browse/QTBUG-100377) [REG 5.15 -> 6.2] Date.parse() can't handle some dates
on Qt 6 but works in Qt 5
* [QTBUG-117904](https://bugreports.qt.io/browse/QTBUG-117904) QProgressBar High-DPI issues
* [QTBUG-130480](https://bugreports.qt.io/browse/QTBUG-130480) Windows 11 Style does not change the palette before
QEvent::PaletteChange
* [QTBUG-138201](https://bugreports.qt.io/browse/QTBUG-138201) Arranging QDockWidgets programatically causes
segmentation faults
* [QTBUG-138381](https://bugreports.qt.io/browse/QTBUG-138381) Putting QTableWidget in a QGraphicsScene breaks
positioning of all widgets in cells
* [QTBUG-139697](https://bugreports.qt.io/browse/QTBUG-139697) Provide a public "bind" API for QCoapClient, or at least
filter out unexpected replies not from peer
* [QTBUG-140725](https://bugreports.qt.io/browse/QTBUG-140725) QWinRegistryKey inconsistent handling of data members in
swap()/move-SMFs
* [QTBUG-141152](https://bugreports.qt.io/browse/QTBUG-141152) CMake: Update snippets for how to use private Qt API
* [QTBUG-110696](https://bugreports.qt.io/browse/QTBUG-110696) Qt6CoreMacros.cmake should take AUTOGEN_BUILD_DIR into
account
* [QTBUG-141366](https://bugreports.qt.io/browse/QTBUG-141366) Createbenchmark test crashed with a segmentation fault
* [QTBUG-140507](https://bugreports.qt.io/browse/QTBUG-140507) Incorrect palette colors when enabling a contrast theme
while a hybrid widgets + quick application is running.
* [QTBUG-135785](https://bugreports.qt.io/browse/QTBUG-135785) Windows Vista/11 style does not use correct font for mdi
menu entries
* [QTBUG-139336](https://bugreports.qt.io/browse/QTBUG-139336) Moving app window between to different DPR screens can
result in poor scaling
* [QTBUG-135418](https://bugreports.qt.io/browse/QTBUG-135418) REG->6.9.0: Windows 11 Style: Selection in Qt Designer
looks weird
* [QTBUG-122624](https://bugreports.qt.io/browse/QTBUG-122624) REG: QDirIterator unicode handling broke in Qt 6.8

### qtsvg
* [QTBUG-140951](https://bugreports.qt.io/browse/QTBUG-140951) [REG. 6.9.3 -> 6.10.0] SVG rendering broken
* [QTBUG-141102](https://bugreports.qt.io/browse/QTBUG-141102) [REG 6.9->6.10] SVG has wrong color
* [QTBUG-130140](https://bugreports.qt.io/browse/QTBUG-130140) SVG-font handling is unicode-oblivious and violates the
SVG specification

### qtdeclarative
* [QTBUG-123106](https://bugreports.qt.io/browse/QTBUG-123106) Documentation - Linking of QtQuickView STATUS_READY,
STATUS_NULL etc.. in docs
* [QTBUG-135474](https://bugreports.qt.io/browse/QTBUG-135474) QtQuickView Android class docs miss QtQmlStatus ?
* [QTBUG-139715](https://bugreports.qt.io/browse/QTBUG-139715) TextArea background invisible in Fusion style
* [QTBUG-139764](https://bugreports.qt.io/browse/QTBUG-139764) Inconsistent conversions between QVariantList and
QList<T>
* [QTBUG-140057](https://bugreports.qt.io/browse/QTBUG-140057)  ASSERT: "locals" in file
/Users/qt/work/qt/qtdeclarative/src/qml/memory/qv4mm.cpp, line 1487
* [QTBUG-137172](https://bugreports.qt.io/browse/QTBUG-137172) "section" property in ListView behaviour is broken
(degradation)
* [QTBUG-140074](https://bugreports.qt.io/browse/QTBUG-140074) Crash in QQmlPrivate::callArrowFunctionAsVariant() when
using qmlcachegen
* [QTBUG-138104](https://bugreports.qt.io/browse/QTBUG-138104) tst_qtquickview_signallistener crashes on Android
* [QTBUG-136629](https://bugreports.qt.io/browse/QTBUG-136629) QUnifiedTimer::updateAnimationTimers() crashes when
QApplication is recreated
* [QTBUG-140143](https://bugreports.qt.io/browse/QTBUG-140143) ValueFilter::value is documented as being a string when
it should be a variant
* [QTBUG-137829](https://bugreports.qt.io/browse/QTBUG-137829) Don't allow yoga library symbols exposed from QT
libraries (either static / dynamic)
* [QTBUG-126558](https://bugreports.qt.io/browse/QTBUG-126558) startSystemMove and startSystemResize don't have qml
documentation
* [QTBUG-128483](https://bugreports.qt.io/browse/QTBUG-128483) ItemGrabResult garbage collected too early
* [QTBUG-140415](https://bugreports.qt.io/browse/QTBUG-140415) qmlcachegen asserts in
QQmlJSRegisterContentPool::adjustType
* [QTBUG-129088](https://bugreports.qt.io/browse/QTBUG-129088) Support Contrast themes in FluentWinUI3
* [QTBUG-139608](https://bugreports.qt.io/browse/QTBUG-139608) Synchronizer documentation could show how to use it with
singletons
* [QTBUG-139632](https://bugreports.qt.io/browse/QTBUG-139632) qmlls, qmllint, and qmlsc don't recognize required
properties set using "on" syntax
* [QTBUG-140026](https://bugreports.qt.io/browse/QTBUG-140026) TreeModel and TreeViewDelegate don't cooperate
* [QTBUG-139561](https://bugreports.qt.io/browse/QTBUG-139561) Crash when layer.enabled bound to MouseArea's
containsMouse
* [QTBUG-138709](https://bugreports.qt.io/browse/QTBUG-138709) [Reg]Qmlformat indents functions incorrectly
* [QTBUG-138480](https://bugreports.qt.io/browse/QTBUG-138480) Top flaky test:
tst_qquickwidget::focusOnClickInProxyWidget
* [QTBUG-140544](https://bugreports.qt.io/browse/QTBUG-140544) SceneGraph examples draws text under navigation bar.
* [QTBUG-140481](https://bugreports.qt.io/browse/QTBUG-140481) SpinBox up down indicators visually remain pressed
* [QTBUG-138518](https://bugreports.qt.io/browse/QTBUG-138518) [REG: 6.8.2 → 6.8.3] Inconsistent behavior of
QQmlEngine::clearComponentCache
* [QTBUG-138599](https://bugreports.qt.io/browse/QTBUG-138599) .qmlls.ini has wrong buildDir
* [QTBUG-136958](https://bugreports.qt.io/browse/QTBUG-136958) [QuickControls] Highlight of the controls is square
instead of round
* [QTBUG-140400](https://bugreports.qt.io/browse/QTBUG-140400) Regression: QInputMethodEvent::Selection start does not
work anymore with commit string
* [QTBUG-94253](https://bugreports.qt.io/browse/QTBUG-94253) When an inputmask is set on a TextInput then it will
overwrite the first character if the cursor starts from position 0 after
typing the second character
* [QTBUG-140018](https://bugreports.qt.io/browse/QTBUG-140018) [REG 6.9.1->6.9.2] QQuickStackElement::initialize null
dereference
* [QTBUG-123631](https://bugreports.qt.io/browse/QTBUG-123631) ScrollView Padding Property
* [QTBUG-139687](https://bugreports.qt.io/browse/QTBUG-139687) [REG 6.6 → 6.8] Broken list property update when the
setter delays modification
* [QTBUG-140838](https://bugreports.qt.io/browse/QTBUG-140838) Top flaky test: tst_QQuickTextField::contextMenuDelete
* [QTBUG-139626](https://bugreports.qt.io/browse/QTBUG-139626) AOT-compiled code crashes when accessing members of
QList<QVariantMap>
* [QTBUG-138465](https://bugreports.qt.io/browse/QTBUG-138465) Line edits are not visible on macOS 26
* [QTBUG-140738](https://bugreports.qt.io/browse/QTBUG-140738) Crash with cachegen compiled code
* [QTBUG-140465](https://bugreports.qt.io/browse/QTBUG-140465) AOT compiled (cachegen) qml crashes program when
attempting to call a function on a destroyed context
* [QTBUG-140914](https://bugreports.qt.io/browse/QTBUG-140914) QML Preview: Updates to Singletons do not reflect in the
preview
* [QTBUG-140922](https://bugreports.qt.io/browse/QTBUG-140922) SpinBox missing from Quick Controls Overview in
Documentation
* [QTBUG-140690](https://bugreports.qt.io/browse/QTBUG-140690) JavaScript function return type list<T> cannot be
correctly assigned to prop if annotated
* [QTBUG-141059](https://bugreports.qt.io/browse/QTBUG-141059) [Reg 6.8 -> 6.10] Assert in
QQmlPropertyCacheAliasCreator<QQmlTypeCompiler>::propertyDataForAlias
* [QTBUG-119504](https://bugreports.qt.io/browse/QTBUG-119504) Inconsistent behavior of list property in QML
* [QTBUG-139142](https://bugreports.qt.io/browse/QTBUG-139142) qmltc: Assertion when instantiating a "cross-nested"
class
* [QTBUG-141085](https://bugreports.qt.io/browse/QTBUG-141085) [qtdeclarative] Install failure
* [QTBUG-137404](https://bugreports.qt.io/browse/QTBUG-137404) Broken Text Outline Rendering with Text.Outline When
Using Software Graphics API
* [QTBUG-141063](https://bugreports.qt.io/browse/QTBUG-141063) Conflict (409) is not a network error so it should be
handled by status code
* [QTBUG-140068](https://bugreports.qt.io/browse/QTBUG-140068) Material background is black with color #FAFAFA
* [QTBUG-136783](https://bugreports.qt.io/browse/QTBUG-136783) PathLine is not rendered when setting the display's
scale to 100%.
* [QTBUG-126193](https://bugreports.qt.io/browse/QTBUG-126193) Crash in XR when clicking on Slider in Android Style
* [QTBUG-139344](https://bugreports.qt.io/browse/QTBUG-139344) call TreeView's expand in delegate will add extra items
* [QTBUG-140665](https://bugreports.qt.io/browse/QTBUG-140665) qt_generate_deploy_qml_app is missing plugin deployment
options
* [QTBUG-85490](https://bugreports.qt.io/browse/QTBUG-85490) REG: Quick 2 TextField doesn't respect IntValidator top,
bottom
* [QTBUG-32298](https://bugreports.qt.io/browse/QTBUG-32298) The canvas component method getImageData() will not
release the frame buffer from system memory.
* [QTBUG-139699](https://bugreports.qt.io/browse/QTBUG-139699) Incorrect calculations involving Layout.preferredHeight
and Layout.fillHeight in nested layouts
* [QTBUG-131895](https://bugreports.qt.io/browse/QTBUG-131895) cursor "stuck" in previous field with
nextItemInFocusChain().forceActiveFocus()
* [QTBUG-141161](https://bugreports.qt.io/browse/QTBUG-141161) FAIL!  : tst_qquickwidget::focusOnClickInProxyWidget()
Received a fatal error.
* [QTBUG-139400](https://bugreports.qt.io/browse/QTBUG-139400) Properly manage QtEditText focus and InputConnection
callbacks
* [QTBUG-140220](https://bugreports.qt.io/browse/QTBUG-140220) qml plugins are not re-instantiated if qapplication is
recreated
* [QTBUG-136943](https://bugreports.qt.io/browse/QTBUG-136943) Software renderer: Visual glitches when moving things
around a Flickable
* [QTBUG-132914](https://bugreports.qt.io/browse/QTBUG-132914) Qt Quick Drawer cannot be opened by touch when window is
rotated
* [QTBUG-141194](https://bugreports.qt.io/browse/QTBUG-141194) qmllint - Warnings when setting FlexboxLayout.direction
in Visual Studio Code/VSCodium
* [QTBUG-140533](https://bugreports.qt.io/browse/QTBUG-140533) Responsive layouts example does not lay out if shown
with a size bigger than NxM
* [QTBUG-141198](https://bugreports.qt.io/browse/QTBUG-141198) Doc: List of JavaScript functions topic is localized
incorrectly
* [QTBUG-141182](https://bugreports.qt.io/browse/QTBUG-141182) QML ProgressBar has broken layout on macOS 26
* [QTBUG-133368](https://bugreports.qt.io/browse/QTBUG-133368) Qt Quick Software Renderer: Colour changes at fractional
coordinates produce a stray black line
* [QTBUG-141105](https://bugreports.qt.io/browse/QTBUG-141105) [REG] SIGSEGV in QQmlDelegateModelItem::destroyObject(),
accesses invalid QObjectData
* [QTBUG-140900](https://bugreports.qt.io/browse/QTBUG-140900) Crash when assigning a function declaration to a
ListElement(for nested lists)
* [QTBUG-
141060](https://bugreports.qt.io/browse/QTBUG-141060) tst_RenderControl::renderAndReadBackWithVulkanAndCustomDepthTextu
re fails on rx480
* [QTBUG-141219](https://bugreports.qt.io/browse/QTBUG-141219) qt_add_qml_module's relative IMPORT_PATH doesn't satisfy
qmlls
* [QTBUG-139679](https://bugreports.qt.io/browse/QTBUG-139679) Custom key handling in TextArea broken
* [QTBUG-136959](https://bugreports.qt.io/browse/QTBUG-136959) Read-only TextEdit overrides all Shortcuts when it has
activeFocus
* [QTBUG-141225](https://bugreports.qt.io/browse/QTBUG-141225) qmlls: don't warn about QT_QML_GENERATE_QMLLS_INI
anymore
* [QTBUG-139603](https://bugreports.qt.io/browse/QTBUG-139603) Menu does not propagate Material style to submenus with
popupType: Popup.Window
* [QTBUG-140414](https://bugreports.qt.io/browse/QTBUG-140414) Reg 6.9->6.10: color incorrectly changes to black and
crash if log
* [QTBUG-140487](https://bugreports.qt.io/browse/QTBUG-140487) Qt Quick States documentation shows old PropertyChanges
syntax
* [QTBUG-141420](https://bugreports.qt.io/browse/QTBUG-141420) qmlcachegen: calling func(obj) clones obj instead of
passing it by ref
* [QTBUG-141638](https://bugreports.qt.io/browse/QTBUG-141638) .qmlformat.ini "SemicolonRule=essential" is not
respected
* [QTBUG-138845](https://bugreports.qt.io/browse/QTBUG-138845) [REG 6.2 → 6.3] qmllint ignores lambda
* [QTBUG-141646](https://bugreports.qt.io/browse/QTBUG-141646) Infinite loop in garbage collector, freezing Application
* [QTBUG-102811](https://bugreports.qt.io/browse/QTBUG-102811) "ScrollView + ListView + DelegateModel" crashes when
`reuseItems: true` and the size of ScrollView depends on delegate items
* [QTBUG-141090](https://bugreports.qt.io/browse/QTBUG-141090) RangeSlider first.value/second.value error when should
be integer
* [QTBUG-140858](https://bugreports.qt.io/browse/QTBUG-140858) [REG: 6.8 -> 6.9] QML Conditional Binding does not
restore original value
* [QTBUG-139941](https://bugreports.qt.io/browse/QTBUG-139941) DelegateModelAccess.ReadWrite should allow writing to
arrays and sequences as models
* [QTBUG-138947](https://bugreports.qt.io/browse/QTBUG-138947) QProgressBar completely blank on macOS 26
* [QTBUG-138942](https://bugreports.qt.io/browse/QTBUG-138942) Mac style (Widget and Quick) has issues on macOS 26
* [QTBUG-139688](https://bugreports.qt.io/browse/QTBUG-139688) Public Java Classes Documentation Bugs
* [QTBUG-139320](https://bugreports.qt.io/browse/QTBUG-139320) QQ4A - Buffer Overflow crash in application project
* [QTBUG-114718](https://bugreports.qt.io/browse/QTBUG-114718) [Tests] tst_QQuickPopup fails
* [QTBUG-139025](https://bugreports.qt.io/browse/QTBUG-139025) [Reg 6.5.9 -> 6.8.4] Lists of objects with
JavaScriptOwnership, stored in var properties, are no longer destroyed
* [QTBUG-140170](https://bugreports.qt.io/browse/QTBUG-140170) [6.10 REG] ASSERT failure in QQuickWindow: "Called
object is not of the correct type (class destructor may have already
run)"
* [QTBUG-140187](https://bugreports.qt.io/browse/QTBUG-140187) Missing dependencies for VectorImage when deploying on
Android
* [QTBUG-137944](https://bugreports.qt.io/browse/QTBUG-137944) qmlformat moves qmlint comments, removes function
argument annotations
* [QTBUG-140041](https://bugreports.qt.io/browse/QTBUG-140041) ids are not properly resolved when using cachegen
* [QTBUG-123386](https://bugreports.qt.io/browse/QTBUG-123386) QmlFormat. Incorrect handling of some comments
* [QTBUG-138946](https://bugreports.qt.io/browse/QTBUG-138946) QSlider issues on macOS 26
* [QTBUG-140507](https://bugreports.qt.io/browse/QTBUG-140507) Incorrect palette colors when enabling a contrast theme
while a hybrid widgets + quick application is running.
* [QTBUG-140364](https://bugreports.qt.io/browse/QTBUG-140364) QQuickGradientStop does not use default position when it
is not provided
* [QTBUG-138022](https://bugreports.qt.io/browse/QTBUG-138022) Ui components behind top and bottom bar on Qt Examples
* [QTBUG-140851](https://bugreports.qt.io/browse/QTBUG-140851) Doc: Add Qt Academy course links to documentation
* [QTBUG-138471](https://bugreports.qt.io/browse/QTBUG-138471) QString::arg() convert floating type to integer
* [QTBUG-139269](https://bugreports.qt.io/browse/QTBUG-139269) REG[6.8.3->6.8.4] Nested Popup with an exit transition
causes crash on close
* [QTBUG-138918](https://bugreports.qt.io/browse/QTBUG-138918) Memory continuously increases when loading/unloading QML
components with Loader
* [QTBUG-138744](https://bugreports.qt.io/browse/QTBUG-138744) FluentWinUI3 ComboBox popup is not resized when
dynamically reloading the model
* [QTBUG-141162](https://bugreports.qt.io/browse/QTBUG-141162) tst_qquickColorDialogImpl::dialogCanMoveBetweenWindows
fails on windows
* [QTBUG-137203](https://bugreports.qt.io/browse/QTBUG-137203) Request to add an option for case sensitivity in
QNetworkRequest::setRawHeader().
* [QTBUG-140899](https://bugreports.qt.io/browse/QTBUG-140899) [REG 6.9.3 -> 6.10.0] Qt6Cored.dll Debug errors
(Microsoft Visual C++ Runetime Library)
* [QTBUG-133755](https://bugreports.qt.io/browse/QTBUG-133755) tst_customization has an unusually long runtime (several
hours)
* [QTBUG-138825](https://bugreports.qt.io/browse/QTBUG-138825) Attached properties through createObject with initial
parameters crash if done from a javascript file
* [QTBUG-140645](https://bugreports.qt.io/browse/QTBUG-140645) qmlls: provide fallback for semantic highlighting on
invalid files
* [QTBUG-100377](https://bugreports.qt.io/browse/QTBUG-100377) [REG 5.15 -> 6.2] Date.parse() can't handle some dates
on Qt 6 but works in Qt 5
* [QTBUG-141365](https://bugreports.qt.io/browse/QTBUG-141365) android/QtQuickView.java:146: error: cannot find symbol
windowReference()
* [QTBUG-140134](https://bugreports.qt.io/browse/QTBUG-140134) Ugly spin boxes on macOS 26 (up/down buttons)
* [QTBUG-141385](https://bugreports.qt.io/browse/QTBUG-141385) qmllint: internal setting values only support single
paths
* [QTBUG-89033](https://bugreports.qt.io/browse/QTBUG-89033) Do not use versioned QML imports in Qt 6 documentation &
examples
* [QTBUG-139943](https://bugreports.qt.io/browse/QTBUG-139943) [iOS][Android] TextEdit or TextInput cannot be navigated
using A11y granularity
* [QTBUG-141465](https://bugreports.qt.io/browse/QTBUG-141465) Reconfigure: CMake wants to use Linguist tools that
haven't been built yet
* [QTBUG-140073](https://bugreports.qt.io/browse/QTBUG-140073) Missing symbols in Java files in qtdeclarative
* [QTBUG-95788](https://bugreports.qt.io/browse/QTBUG-95788) Singletons with clearComponentCache don't fully work

### qtactiveqt
* [QTBUG-139731](https://bugreports.qt.io/browse/QTBUG-139731) Axserver crashes on exit if command line arguments
passed after standard Qt arguments (removed by QApp)

### qtmultimedia
* [QTBUG-139993](https://bugreports.qt.io/browse/QTBUG-139993) ASSERT in QRtAudioEngine::runRtCommand
* [QTBUG-139681](https://bugreports.qt.io/browse/QTBUG-139681) Camera widgets record button crashes application on
linux
* [QTBUG-139210](https://bugreports.qt.io/browse/QTBUG-139210) No qtmultimedia.tags file generated
* [QTBUG-140431](https://bugreports.qt.io/browse/QTBUG-140431) apalis-imx6: media Player example fails to play video
* [QTBUG-140451](https://bugreports.qt.io/browse/QTBUG-140451) TS video playback: no audio on Windows, corrupted audio
on macOS
* [QTBUG-140122](https://bugreports.qt.io/browse/QTBUG-140122) Background Color Difference During Video Playback
Between Windows Media Player and Qt Media Player Example
* [QTBUG-138452](https://bugreports.qt.io/browse/QTBUG-138452) Misleading QML audioDevice.mode enum documentation.
* [QTBUG-140646](https://bugreports.qt.io/browse/QTBUG-140646) Error pops up at the end of playing audio file (mp4a
with ALAC codec) recorded with audio recorder example
* [QTBUG-140558](https://bugreports.qt.io/browse/QTBUG-140558) Pulseaudio leaks
* [QTBUG-140658](https://bugreports.qt.io/browse/QTBUG-140658) audio recorder example: AudioLevel element in gui does
nothing
* [QTBUG-124734](https://bugreports.qt.io/browse/QTBUG-124734) multimedia player example does not obey palette
* [QTBUG-126028](https://bugreports.qt.io/browse/QTBUG-126028) AudioSource example: changing source has no effect
* [QTBUG-140086](https://bugreports.qt.io/browse/QTBUG-140086) Streaming an IP camera over HTTP fails randomly
* [QTBUG-140462](https://bugreports.qt.io/browse/QTBUG-140462) QML Video Recorder example: qmllint warnings
* [QTBUG-141250](https://bugreports.qt.io/browse/QTBUG-141250) "Easy Effects Source" device doesn't show up
* [QTBUG-129152](https://bugreports.qt.io/browse/QTBUG-129152) Camera flash not working on iOS
* [QTBUG-141376](https://bugreports.qt.io/browse/QTBUG-141376) declarative-camera, regression: Switching camera device
no longer keeps camera active
* [QTBUG-137950](https://bugreports.qt.io/browse/QTBUG-137950) Application crash when loading a camera CaptureSession
on Windows
* [QTBUG-134554](https://bugreports.qt.io/browse/QTBUG-134554) gstreamer-pipeline does not work if source is set
initially
* [QTBUG-141661](https://bugreports.qt.io/browse/QTBUG-141661) [macOS] Invalid preferredFormat is returned for iMac's
built-in audio device
* [QTBUG-141840](https://bugreports.qt.io/browse/QTBUG-141840) QSoundEffect hangs when switching source url
* [QTBUG-141789](https://bugreports.qt.io/browse/QTBUG-141789) [reg 6.7.3->6.8/9/10] Audio Output Example freezes
* [QTBUG-141787](https://bugreports.qt.io/browse/QTBUG-141787) QAudioOutput cannot recover from interrupted RDP session
* [QTBUG-139660](https://bugreports.qt.io/browse/QTBUG-139660) QTextToSpeech WinRT backend stops speaking after the
first word in Qt 6.9.2
* [QTBUG-139560](https://bugreports.qt.io/browse/QTBUG-139560) Access functions are documented even when their
properties are not
* [QTBUG-130272](https://bugreports.qt.io/browse/QTBUG-130272) Failed to start pulseaudio sink and source on OpenSuse
CI
* [QTBUG-26504](https://bugreports.qt.io/browse/QTBUG-26504) QAudioOutput resume() fails regularly using pulseaudio
backend
* [QTBUG-139767](https://bugreports.qt.io/browse/QTBUG-139767) AudioSource example crash

### qttools
* [QTBUG-139769](https://bugreports.qt.io/browse/QTBUG-139769) [Regr: 6.9.2 -> 6.10] Qt 6.10 BETA 3: lupdate does not
include context names in ts files
* [QTBUG-139405](https://bugreports.qt.io/browse/QTBUG-139405) QMatrix4x4 has an internal Flag enum that QDoc exposes
as flags
* [QTBUG-141238](https://bugreports.qt.io/browse/QTBUG-141238) Version information refers to QML properties not
property groups
* [QTBUG-140636](https://bugreports.qt.io/browse/QTBUG-140636) Function return types with namespaces sometimes confuse
lupdate
* [QTBUG-140686](https://bugreports.qt.io/browse/QTBUG-140686) Classes with attributes confuse lupdate
* [QTBUG-140548](https://bugreports.qt.io/browse/QTBUG-140548) [Reg 6.9.1->6.9.2] Different misdetection of correct
namespace/class with tr
* [QTBUG-140550](https://bugreports.qt.io/browse/QTBUG-140550) Class inside namespace with the same name confuses
lupdate
* [QTBUG-141771](https://bugreports.qt.io/browse/QTBUG-141771) QDoc: Duplicate overload notes for signals/slots using
\overload command
* [QTBUG-134806](https://bugreports.qt.io/browse/QTBUG-134806) qdoc has no way to independently document QML
enumerations
* [QTBUG-136483](https://bugreports.qt.io/browse/QTBUG-136483) qdoc non-deterministic .index output
* [QTBUG-105097](https://bugreports.qt.io/browse/QTBUG-105097) \since says the macro is a function even if it isn't
* [QTBUG-135418](https://bugreports.qt.io/browse/QTBUG-135418) REG->6.9.0: Windows 11 Style: Selection in Qt Designer
looks weird
* [QTBUG-141642](https://bugreports.qt.io/browse/QTBUG-141642) QDoc: Possibility of infinite loops from circular class
relationships

### qtdoc
* [QTBUG-139996](https://bugreports.qt.io/browse/QTBUG-139996) lightningviewer fails to build with Boot to Qt on
Windows
* [QTBUG-139340](https://bugreports.qt.io/browse/QTBUG-139340) [new example] demos/graphs_csv not compiling on Wasm
multithread
* [QTBUG-138178](https://bugreports.qt.io/browse/QTBUG-138178) Same Game: qmllint warnings
* [QTBUG-140383](https://bugreports.qt.io/browse/QTBUG-140383) Coffee Machine: qmllint warnings
* [QTBUG-140387](https://bugreports.qt.io/browse/QTBUG-140387) Robot Arm: qmllint warnings
* [QTBUG-138795](https://bugreports.qt.io/browse/QTBUG-138795) When building from source "-debug-and-release" "cmake
--install ." isn't enough
* [QTBUG-115206](https://bugreports.qt.io/browse/QTBUG-115206) Document how to install debug-and-release builds to
avoid missing debug libraries (upstream cmake multi-config install
issue)
* [QTBUG-140395](https://bugreports.qt.io/browse/QTBUG-140395) Dice Example: Cannot Read property 'x' of null
* [QTBUG-140385](https://bugreports.qt.io/browse/QTBUG-140385) Dice Example: Cannot Read property 'x' of null
* [QTBUG-139937](https://bugreports.qt.io/browse/QTBUG-139937) Missing section in Android's getting started
documentation
* [QTBUG-140396](https://bugreports.qt.io/browse/QTBUG-140396) 'Thermostat' applications Control view not scaled
properly on 'smallDesktop'
* [QTBUG-140067](https://bugreports.qt.io/browse/QTBUG-140067) Clear up or remove 'Porting to iOS' documentation page
* [QTBUG-137076](https://bugreports.qt.io/browse/QTBUG-137076) Fix qmllint warnings for Calqlatr example
* [QTBUG-140113](https://bugreports.qt.io/browse/QTBUG-140113) Text Viewer Plugin Example does not compile
* [QTBUG-138173](https://bugreports.qt.io/browse/QTBUG-138173) Lightning Viewer: qmllint warnings
* [QTBUG-140051](https://bugreports.qt.io/browse/QTBUG-140051) Cosmetic facelift for QtJenny Demo
* [QTBUG-139769](https://bugreports.qt.io/browse/QTBUG-139769) [Regr: 6.9.2 -> 6.10] Qt 6.10 BETA 3: lupdate does not
include context names in ts files
* [QTTA-460](https://bugreports.qt.io/browse/QTTA-460) Documentation navigation is not functional
* [QTBUG-89033](https://bugreports.qt.io/browse/QTBUG-89033) Do not use versioned QML imports in Qt 6 documentation &
examples

### qtlocation
* [QTBUG-140841](https://bugreports.qt.io/browse/QTBUG-140841) Submodule update failure in Qt Location after Qt Qml
change
* [QTBUG-139941](https://bugreports.qt.io/browse/QTBUG-139941) DelegateModelAccess.ReadWrite should allow writing to
arrays and sequences as models
* [QTBUG-139780](https://bugreports.qt.io/browse/QTBUG-139780) Qt Positioning: Discrepancy between documented type
names and actual type names

### qtpositioning
* [QTBUG-141757](https://bugreports.qt.io/browse/QTBUG-141757) QT_UNITY_BUILD broken on windows
* [QTBUG-139654](https://bugreports.qt.io/browse/QTBUG-139654) Update QtPositioning documentation to use QDoc commands
* [QTBUG-139780](https://bugreports.qt.io/browse/QTBUG-139780) Qt Positioning: Discrepancy between documented type
names and actual type names
* [QTBUG-139560](https://bugreports.qt.io/browse/QTBUG-139560) Access functions are documented even when their
properties are not

### qtconnectivity
* [QTBUG-140697](https://bugreports.qt.io/browse/QTBUG-140697) Bluetooth Low Energy Scanner does not respect safe areas
* [QTBUG-140825](https://bugreports.qt.io/browse/QTBUG-140825) QBluetoothDeviceInfo::isCached() always returns true on
Windows
* [QTBUG-139280](https://bugreports.qt.io/browse/QTBUG-139280) Cannot build QT 6.8 without GNU extensions

### qtwayland
* [QTBUG-115063](https://bugreports.qt.io/browse/QTBUG-115063) Crash in WaylandEglClientBuffer::WaylandEglClientBuffer
* [QTBUG-119259](https://bugreports.qt.io/browse/QTBUG-119259) Missing documentation of QT_IVI_SURFACE_ID
* [QTBUG-141147](https://bugreports.qt.io/browse/QTBUG-141147) [qtwayland] Manual tests build failure

### qt3d
* [QTBUG-139978](https://bugreports.qt.io/browse/QTBUG-139978) qt3d fails on documentation-warnings
* [QTBUG-138670](https://bugreports.qt.io/browse/QTBUG-138670) Doc: Scene3D QML type is missed at Qt 3D Scene3D Module
* [QTBUG-141068](https://bugreports.qt.io/browse/QTBUG-141068) error: no matching function for call to
‘QString::arg(QRhiTexture::Flags)’
* [QTBUG-140939](https://bugreports.qt.io/browse/QTBUG-140939) Qt3DExtra after Qt 6.9

### qtwebchannel
* [QTBUG-141648](https://bugreports.qt.io/browse/QTBUG-141648) Few WebChannel object registration crashes

### qtwebengine
* [QTBUG-139998](https://bugreports.qt.io/browse/QTBUG-139998) pdf\multipage and pdf\singlepage fails to build with
Boot to Qt 6.10.0 beta4 on Windows
* [QTBUG-122766](https://bugreports.qt.io/browse/QTBUG-122766) QPdfSearchModelPrivate::doSearch warning "not found in
context" happens sometimes
* [QTBUG-140515](https://bugreports.qt.io/browse/QTBUG-140515) User-Agent set via QWebEngineUrlRequestInterceptor is
ignored for reloads
* [QTBUG-140029](https://bugreports.qt.io/browse/QTBUG-140029) [macOS] Deployment target not detected for Qt Pdf
* [QTBUG-140032](https://bugreports.qt.io/browse/QTBUG-140032) [macOS] GnObject_Pdf linker error
* [QTBUG-140234](https://bugreports.qt.io/browse/QTBUG-140234) Memory leak on repeated setUrl() calls in QWebEnginePage
with QWebEngineView
* [QTBUG-131443](https://bugreports.qt.io/browse/QTBUG-131443) QPdfView mouseEvents don’t have correct position when
scrolled
* [QTBUG-141096](https://bugreports.qt.io/browse/QTBUG-141096) [REG 6.9 -> 6.10] Segfault when clicking
camera/microphone <permission> element
* [QTBUG-136160](https://bugreports.qt.io/browse/QTBUG-136160) QtWebEngine based browser shows nothing with legacy
NVIDIA driver
* [QTBUG-141112](https://bugreports.qt.io/browse/QTBUG-141112) Build fails with -disable-deprecated-up-to 0x060b00
* [QTBUG-141153](https://bugreports.qt.io/browse/QTBUG-141153) QtWebEngine fails to build: brotli/libcommon.a: error
adding symbols: archive has no index
* [QTBUG-136257](https://bugreports.qt.io/browse/QTBUG-136257) QtWebEngine based browser shows nothing with panthor
driver
* [QTBUG-139424](https://bugreports.qt.io/browse/QTBUG-139424) GPU rendering not working with mesa 25.2
* [QTBUG-139335](https://bugreports.qt.io/browse/QTBUG-139335) QtWebEngine based browser shows nothing with MESA
LLVMpipe
* [QTBUG-139710](https://bugreports.qt.io/browse/QTBUG-139710) [Reg 6.8 -> 6.9] qml web engine frame crashes on
assigment

### qtcharts
* [QTBUG-140545](https://bugreports.qt.io/browse/QTBUG-140545) Charts with QML Gallery example draws under system bars
(top and bottom)
* [QTBUG-136152](https://bugreports.qt.io/browse/QTBUG-136152) Qt Charts: Add alt texts

### qtdatavis3d
* [QTBUG-138512](https://bugreports.qt.io/browse/QTBUG-138512) The classes in the Qt DataVisualization module do not
use the application's QLocale by default.

### qtvirtualkeyboard
* [QTBUG-138693](https://bugreports.qt.io/browse/QTBUG-138693) Doc: VirtualKeyboardSetting QML Type is missed at Qt
Virtual Keyboard QML Types
* [QTBUG-139038](https://bugreports.qt.io/browse/QTBUG-139038) Overlay issue with Virtual Keyboard + Material Style
* [QTBUG-124178](https://bugreports.qt.io/browse/QTBUG-124178) Virtualkeyboard of Qt 5.15.15 crash on Ubuntu
* [QTBUG-138921](https://bugreports.qt.io/browse/QTBUG-138921) Virtual Keyboard plugin missing or fails to load in Qt
6.9.1
* [QTBUG-137923](https://bugreports.qt.io/browse/QTBUG-137923) [Reg 6.8.3->6.9.0] Virtual keyboard is totally broken
because it depends on Qt MultiMedia
* [QTBUG-138888](https://bugreports.qt.io/browse/QTBUG-138888) Japanese layout cannot input Kanji characters in many
cases
* [QTBUG-126402](https://bugreports.qt.io/browse/QTBUG-126402) QML virtual keyboard behavior regression between 5.x and
6.x
* [QTBUG-137731](https://bugreports.qt.io/browse/QTBUG-137731) Shadow Input is not properly displayed with
DesktopInputPanel with fullScreenMode = true
* [QTBUG-137921](https://bugreports.qt.io/browse/QTBUG-137921) [Reg 6.8.3->6.9.0] Desktop virtual keyboard cannot find
InputPanel.qml and freezes the application
* [QTBUG-137250](https://bugreports.qt.io/browse/QTBUG-137250) REG->6.9.0: VirtualKeyboard not working (Linux)
* [QTBUG-140553](https://bugreports.qt.io/browse/QTBUG-140553) qmllint does not recognize
VirtualKeyboardSettings.wordCandidateList
* [QTBUG-140521](https://bugreports.qt.io/browse/QTBUG-140521) QML InputMethod crashes
* [QTBUG-136149](https://bugreports.qt.io/browse/QTBUG-136149) Qt Virtual Keyboard: Add alt texts

### qtremoteobjects
* [PYSIDE-3179](https://bugreports.qt.io/browse/PYSIDE-3179) REG->6.11.0: QtRemoteObjects/integration_test.py (and
other RO tests) assert/fail
* [QTBUG-139845](https://bugreports.qt.io/browse/QTBUG-139845) Reg->6.11: Assert when passing a too long-list to
QMetaMethodBuilder::setParameterNames()

### qtlottie
* [QTBUG-139975](https://bugreports.qt.io/browse/QTBUG-139975) New example lottie/qtlottieviewer fails to configure
* [QTBUG-140730](https://bugreports.qt.io/browse/QTBUG-140730) Qt Lottie Animation: Missing licensing pages
* [QTBUG-140187](https://bugreports.qt.io/browse/QTBUG-140187) Missing dependencies for VectorImage when deploying on
Android

### qtquick3d
* [QTBUG-139175](https://bugreports.qt.io/browse/QTBUG-139175) Baking lights in CabinDemo gives a black scene on
Windows
* [QTBUG-139274](https://bugreports.qt.io/browse/QTBUG-139274) Loader3D and ComponentBehaviour Bound seem incompatible
* [QTBUG-140392](https://bugreports.qt.io/browse/QTBUG-140392) Material.OpaquePrePassDepthDraw Option Causing Graphical
Artifacts with Instancing and CustomMaterial
* [QTBUG-140670](https://bugreports.qt.io/browse/QTBUG-140670) Regression: Item2D not updated correctly
* [QTBUG-140662](https://bugreports.qt.io/browse/QTBUG-140662) Specular light calculation generates INF color values
* [QTBUG-140780](https://bugreports.qt.io/browse/QTBUG-140780) Setting Sphere Geometry pickable: true, causes crash in
Quick 3D
* [QTBUG-139616](https://bugreports.qt.io/browse/QTBUG-139616) Setting ExtendedSceneEnvironment.adjustmentContrast
causes scene to go black
* [QTBUG-139324](https://bugreports.qt.io/browse/QTBUG-139324) Quick3D Frame view is empty in creator QML profiler
* [QTBUG-140857](https://bugreports.qt.io/browse/QTBUG-140857) Qt Quick3d automatic LoD: Visual Artifacts with enabled
OpaquePrePassDepthDraw on any other object on same scene
* [QTBUG-140855](https://bugreports.qt.io/browse/QTBUG-140855) Qt Quick3d automatic LoD not working With CustomMaterial
* [QTBUG-140715](https://bugreports.qt.io/browse/QTBUG-140715) Qt Quick3d LoD with Instance dirty table is not updated
correctly.
* [QTBUG-140829](https://bugreports.qt.io/browse/QTBUG-140829) Touch events from XrView.setTouchpoint() do not work
with TapHandler
* [QTBUG-141222](https://bugreports.qt.io/browse/QTBUG-141222) OpenXR: xrWaitFrame() blocks the main thread
* [QTBUG-141617](https://bugreports.qt.io/browse/QTBUG-141617) SkyBoxCubeMap is not tonemapped
* [QTBUG-139941](https://bugreports.qt.io/browse/QTBUG-139941) DelegateModelAccess.ReadWrite should allow writing to
arrays and sequences as models

### qtshadertools
* [QTBUG-141348](https://bugreports.qt.io/browse/QTBUG-141348) ERROR: AddressSanitizer: stack-buffer-overflow
* [QTBUG-135281](https://bugreports.qt.io/browse/QTBUG-135281) Qml Camera not work on webassembly

### qtmqtt
* [QTBUG-137305](https://bugreports.qt.io/browse/QTBUG-137305) MQTT tests emits QSocketNotifier: Invalid socket
specified

### qthttpserver
* [QTBUG-138410](https://bugreports.qt.io/browse/QTBUG-138410) QtHttpServer: The HTTP/1.0 support is incomplete

### qtgrpc
* [QTBUG-129286](https://bugreports.qt.io/browse/QTBUG-129286) GRPC: Implement HTTP/2 dataframe decompression

### qtquickeffectmaker
* [QTBUG-140905](https://bugreports.qt.io/browse/QTBUG-140905) [REG: 6.9.1 -> 6.10] Del key not usable in QQEM code
editor

### qtgraphs
* [QTBUG-138822](https://bugreports.qt.io/browse/QTBUG-138822) Reusing same ValueAxis in multiple GraphViews results in
a crash
* [QTBUG-140240](https://bugreports.qt.io/browse/QTBUG-140240) Rendering of Surface3DSeries crashes when the first row
is all NaN
* [QTBUG-140088](https://bugreports.qt.io/browse/QTBUG-140088) tst_qgqml2dtest (Failed)
* [QTBUG-140660](https://bugreports.qt.io/browse/QTBUG-140660) Transparency does not work in textureFile in
Surface3DSeries
* [QTBUG-140904](https://bugreports.qt.io/browse/QTBUG-140904) The QValue3DAxis::setReversed() function is not working
properly in the surface graph.
* [QTBUG-135931](https://bugreports.qt.io/browse/QTBUG-135931) Reg[6.8.2-6.9.0]ListView containing AbstractSeries does
not scroll on Drag
* [QTBUG-140957](https://bugreports.qt.io/browse/QTBUG-140957) qtgraphs: tracepoint build fails
* [QTBUG-141186](https://bugreports.qt.io/browse/QTBUG-141186) Axis handling example keeps printing scale data warning
* [QTBUG-141370](https://bugreports.qt.io/browse/QTBUG-141370) Setting selection item label visibility to false does
not work for Scatter 3D
* [QTBUG-141687](https://bugreports.qt.io/browse/QTBUG-141687) Scatter instancing crash when selecting
* [QTBUG-141518](https://bugreports.qt.io/browse/QTBUG-141518) [REG 6.10.0->6.10.1] graphs/graphprinting configure
fails
* [QTBUG-138828](https://bugreports.qt.io/browse/QTBUG-138828) Programmatic slicing does not work
* [QTBUG-140843](https://bugreports.qt.io/browse/QTBUG-140843) PieSeries hoverable crashing
* [QTBUG-134641](https://bugreports.qt.io/browse/QTBUG-134641) the Custom3DItem is still in Scatter3D after it is
deleted by removeCustomItem

### qtinsighttracker (Commercial only)
* [QTBUG-140160](https://bugreports.qt.io/browse/QTBUG-140160) FAIL!  : tst_QInsightEventFilter::trackEvents(button.ui)
Compared values are not the same

### qtvncserver (Commercial only)
* [QTBUG-138461](https://bugreports.qt.io/browse/QTBUG-138461) Rotated VncItem input/visual mismatch in
GrabItemRectangle mode

Known Issues
------------
* Check that your system meets Qt's requirements:
  https://doc-snapshots.qt.io/qt6-6.10/supported-platforms.html
* RTA reported issues from Qt 6.10
  https://bugreports.qt.io/issues/?filter=27755
* See Qt 6.10 known issues from:
  https://wiki.qt.io/Qt_6.10_Known_Issues
* Qt 6.10.1 Open issues in Jira:
  https://bugreports.qt.io/issues/?filter=28123

Credits for the release goes to:
--------------------------------

Eirik Aavitsland  
Chris Adams  
Laszlo Agocs  
Dilek Akcay  
Konsta Alajärvi  
Stanislav Aleksandrov  
Even Oscar Andersen  
Dimitrios Apostolou  
Albert Astals Cid  
Mate Barany  
Thierry Bastian  
Nicholas Bennett  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
David Boddie  
Joerg Bornemann  
Assam Boudjelthia  
Marcell Brauner  
Aurélien Brooke  
Kai Uwe Broulik  
Michael Brüning  
Eren Bursali  
Olivier De Cannière  
Alexei Cazacov  
Kaloyan Chehlarski  
Wang Chuan  
Alexandru Croitor  
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
Ilya Fedin  
Julian Greilich  
Robert Griebl  
Jan Grulich  
Johannes Grunenberg  
Kaj Grönholm  
Richard Moe Gustavsen  
Lucie Gérard  
Mikko Hallamaa  
Inkamari Harjula  
Andre Hartmann  
Elias Hautala  
Jani Heikkinen  
Moss Heim  
Christian Heimlich  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Mats Honkamaa  
Xaver Hugl  
Samuli Hölttä  
Masoud Jami  
Morteza Jamshidi  
Johnny Jazeix  
Allan Sandfeld Jensen  
Jonas Karlsson  
Ilya Katsnelson  
Igor Khanin  
Ali Kianian  
Friedemann Kleint  
Michal Klocek  
Sze Howe Koh  
Jarkko Koivikko  
Tomi Korpipaa  
Jani Korteniemi  
Fabian Kosmale  
Santhosh Kumar  
Kai Köhne  
Inho Lee  
Frédéric Lefebvre  
Wladimir Leuschner  
Jie Liu  
Robert Löhning  
Thiago Macieira  
Safiyyah Moosa  
Marc Mutz  
Antti Määttä  
Martin Negyokru  
Andy Nichols  
Markku Nokkala  
Mårten Nordheim  
Dennis Oberst  
Jerome Pasion  
Samuli Piippo  
Karim Pinter  
Timur Pocheptsov  
Joni Poikelin  
Jacek Poplawski  
Gleb Popov  
Rami Potinkara  
Lorn Potter  
Sakaria Pouke  
Dheerendra Purohit  
MohammadHossein Qanbari  
Liang Qi  
Matthias Rauter  
David Redondo  
Topi Reinio  
Konstantin Ritt  
Kaarle Ritvanen  
Shawn Rutledge  
Toni Saario  
Ahmad Samir  
Timon Sassor  
Lars Schmertmann  
SanthoshKumar Selvaraj  
Mike Senter  
Luca Di Sera  
Sami Shalayel  
Kristoffer Skau  
Nils Petter Skålerud  
Ivan Solovev  
Axel Spoerl  
Stefan Steinwasser  
Christian Strømme  
Tarja Sundqvist  
Lars Sutterud  
Błażej Szczygieł  
Jan Arve Sæther  
Morten Sørvig  
Sadegh Taghavi  
Elias Toivola  
Jere Tuliniemi  
Paul Olav Tvete  
Sami Varanka  
Peter Varga  
Bror Wetlesen Vedeld  
Doris Verria  
Tor Arne Vestbø  
Petri Virkkunen  
Ville Voutilainen  
Olli Vuolteenaho  
Jaishree Vyas  
Jannis Völker  
Michael Weghorn  
Edward Welbourne  
Paul Wicking  
Piotr Wiercinski  
Oliver Wolff  
Semih Yavuz  
Wang Zichong  
Jouni Äijälä  
Daniel Čejchan  
