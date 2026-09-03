Release notes
=============

Qt 6.5.10 release is a patch release made on the top of Qt 6.5.9.
As a patch release, Qt 6.5.10 does not add any new functionality but provides
bug fixes and other improvements and maintains both forward and backward
compatibility (source and binary) with Qt 6.5.9.
For detailed information about Qt 6.5, refer to the online documentation
included in this distribution. The documentation is also available online:

https://doc.qt.io/qt-6/index.html

The Qt version 6.5 series is binary compatible with the 6.4.x series.
Applications compiled for 6.4 will continue to run with 6.5.

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

* [CVE-2025-6338](https://nvd.nist.gov/vuln/detail/CVE-2025-6338) in qtbase
* [CVE-2025-5683](https://nvd.nist.gov/vuln/detail/CVE-2025-5683) in qtimageformats

### qtbase
* 95990f148e2 QStringConverter: widen nameForEncoding()'s contract
  * The nameForEncoding() function now returns nullptr for an invalid
Encoding value. Before, such a call resulted in undefined behavior.

* a3a25443440 WASM builds now handle bitmap and pixmap cursors
  * Previously, bitmap and pixmap cursors were nonfunctional in wasm builds
and would trigger warnings.  These cursors now work as expected.

* bf7a0a234e6 Make F11 the fullscreen keyboard shortcut on Gnome (as on
KDE & Windows)
  * The fullscreen keyboard shortcut is now F11 on Gnome, not Ctrl-F11.

* 7e3a5edfce9 QAbstractSlider: fix missing "emission" of
SliderOrientationChange
  * Fixed the missing "emission" of protected
sliderChange(SliderOrientationChange).

* e5f9eb50432 QPointer: don't cause UB when checking for nullptr
  * For `QPointer<Derived> p`, `!p` and comparing `p` to nullptr no longer
perform invalid downcasts when the object held in `p` is in the process
of being destroyed and has already been demoted from Derived to one of
its base classes. Before, these expressions invoked data(), which casts
from QObject* to Derived*, a cast which is invalid.

* 53c73f8a40c Upgrade Harfbuzz to 11.1.0
  * Upgraded Harfbuzz to version 11.1.0.

* c2a90cfcd65 qDecodeDataUrl(): fix precondition violation in call to
QByteArrayView::at()
  * Fixed a bug in the handling of data: URLs that could lead to a crash if
Qt was built with assertions enabled. This affects QNetworkManager and
links in QTextDocument.

* af40da6f7b2 SQLite: Update SQLite to v3.49.2
  * Updated SQLite to v3.49.2

* 5eb36fd788c Update bundled libpng to version 1.6.48
  * libpng was updated to version 1.6.48

* e663df8a790 Upgrade Harfbuzz to 11.2.1
  * Upgraded Harfbuzz to version 11.2.1.

* f6b0130cbdb QSslCertificate: fromPath(): check the path arg isn't
empty
  * fromPath() no longer accepts an empty path, which would previously
result in searching the current directory.

* 554ccfa4b48 SQLite: Update SQLite to v3.50.0
  * Updated SQLite to v3.50.0

* b9fc0595a1a Update bundled libjpeg-turbo to version 3.1.1
  * libjpeg-turbo was updated to version 3.1.1

* b0f06cac5a8 Bump double-conversion version
  * Updated double-conversion to v3.3.1.

* 9569b16c202 Update public suffix list
  * Updated the public suffix list to upstream version
2025-06-16_09-45-02_UTC.

* 7a53f6af17f Update bundled libpng to version 1.6.49
  * libpng was updated to version 1.6.49

* ab04f3f8fcd SQLite: Update SQLite to v3.50.2
  * Updated SQLite to v3.50.2

* 1ab4ad03dd8 Fail builds on Apple platforms with invalid Info.plist
  * Fail builds on Apple platforms if the Info.plist is invalid instead of
generating corrupt application bundles.

* df904d9b044 QWeakPointer: don't let IfCompatible<X> make accidental
SMFs
  * Fixed a regression whereby the QWeakPointer<T> copy or move constructors
and/or assignment operators may fail to compile for forward-declared
(incomplete) T.

* ad91651ed08 QTextStream: cope with multi-code-point signs
  * Fixed QTextStream::FieldAlignment::AlignAccountingStyle for locales that
have negativeSign/positiveSign (-/+) that take more than one UTF-16 code
point (e.g. ar (Arabic)).

* f8c09cbe6b1 Update bundled libpng to version 1.6.50
  * libpng was updated to version 1.6.50

* bc0acff38e6 QLocale: fix off-by-one error in codeToScript()
  * Fixed a bug where QLocale could not find the QLocale::Script with the
highest value when looked up by string (codeToString() or
QLocale(string) constructor).

* a4e9aa0a073 SQLite: Update SQLite to v3.50.3
  * Updated SQLite to v3.50.3

* fca01841e62 SQLite: Update SQLite to v3.50.4
  * Updated SQLite to v3.50.4

* df06112d66e Upgrade Harfbuzz to 11.3.3
  * Upgraded Harfbuzz to version 11.3.3.

* bf44d44bd1e Upgrade Harfbuzz to 11.4.1
  * Upgraded Harfbuzz to version 11.4.1.

### qtsvg
* a7c6cfe5 CMake: Add PURL and CPE info to 3rd party attribution files
  * Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtdeclarative
* 15ff24d9d5 CMake: Add PURL and CPE info to 3rd party attribution files
  * Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtmultimedia
* 183de5d24 Update FFmpeg version in documentation
  * Updated FFmpeg to n7.1.1.

* 169963b2d CMake: Add PURL and CPE info to 3rd party attribution files
  * Added PURL and CPE information to the attribution files of 3rd party
sources.

### qttools
* f99c95e91 CMake: Add PURL and CPE info to 3rd party attribution files
  * Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtpositioning
* 5184363af CMake: Add PURL and CPE info to 3rd party attribution files
  * Added PURL and CPE information to the attribution files of 3rd party
sources.

* 115eed85a Make: Fix incorrect PURL version for clip2tri
  * Fixed incorrect PURL version for clip2tri in qt_attribution.json.

### qtsensors
* f6f3a012 CMake: Add PURL and CPE info to 3rd party attribution files
  * Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtconnectivity
* de4c12fe CMake: Add PURL and CPE info to 3rd party attribution files
  * Added PURL and CPE information to the attribution files of 3rd party
sources.

### qt3d
* 40084a201 CMake: Add PURL and CPE info to 3rd party attribution files
  * Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtimageformats
* 3fcb487a CMake: Add PURL and CPE info to 3rd party attribution files
  * Added PURL and CPE information to the attribution files of 3rd party
sources.

* 6ad06bb6 Update bundled libwebp to version 1.6.0
  * Update bundled libwebp to version 1.6.0

### qtvirtualkeyboard
* ca0e3324 CMake: Add PURL and CPE info to 3rd party attribution files
  * Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtquick3d
* d58eec787 Update TinyEXR to v1.0.12
  * Updated TinyEXR to v1.0.12

* b2e484810 CMake: Add PURL and CPE info to 3rd party attribution files
  * Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtshadertools
* 73b5da6 CMake: Add PURL and CPE info to 3rd party attribution files
  * Added PURL and CPE information to the attribution files of 3rd party
sources.

### qt5compat
* 5ec261c CMake: Add PURL and CPE info to 3rd party attribution files
  * Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtopcua
* 0e4555ea CMake: Add PURL and CPE info to 3rd party attribution files
  * Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtapplicationmanager (Commercial only)
* 9ca9aa78 CMake: Add PURL and CPE info to 3rd party attribution files
  * Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtinterfaceframework (Commercial only)
* 970cd27b Update the bundled qface to the latest version (2.0.13)
  * The copy of qface in Qt was updated to 2.0.13


Fixes
-----

### qtbase
* [QTBUG-135640](https://qt-project.atlassian.net/browse/QTBUG-135640) Data race in QPointer
(QtSharedPointer::ExternalRefCountData::getAndRef)
* [QTBUG-135854](https://qt-project.atlassian.net/browse/QTBUG-135854) Qt Keyboard Shortcut: Fullscreen incorrectly mapped in
GNOME
* [QTBUG-135597](https://qt-project.atlassian.net/browse/QTBUG-135597) QAbstractSlider is not using SliderOrientationChange
* [QTBUG-136019](https://qt-project.atlassian.net/browse/QTBUG-136019)  c1: fatal error C1083: Cannot open source file: 'C:\Use
rs\qt\work\qt\qt3d_build\src\plugins\renderers\opengl\debug\OpenGLRender
erPlugin_resource.rc': No such file or directory
* [QTBUG-120125](https://qt-project.atlassian.net/browse/QTBUG-120125) CMake subarch extraction does not always succeed
* [QTBUG-133841](https://qt-project.atlassian.net/browse/QTBUG-133841) 'Failed to initialize graphics backend for OpenGL'
causes the example apps to crash on launch
* [QTBUG-136442](https://qt-project.atlassian.net/browse/QTBUG-136442) NoSuchMethodError notifyObjectShow when using Appium
with Qt Accessibility component
* [QTBUG-134538](https://qt-project.atlassian.net/browse/QTBUG-134538) QRandomGenerator, QSimd: RDSEED should be checked for
validity
* [QTBUG-125436](https://qt-project.atlassian.net/browse/QTBUG-125436) Windows ARM: HealthCheck fails - QtBase tst_QProcess
* [QTBUG-136530](https://qt-project.atlassian.net/browse/QTBUG-136530) QFuture::isValid() without result
* [QTBUG-134419](https://qt-project.atlassian.net/browse/QTBUG-134419) systemCaCertificate() openssl backend walks current
working directory if system ca directory contains a broken symlink
* [QTBUG-136362](https://qt-project.atlassian.net/browse/QTBUG-136362) [REG 6.8 -> 6.9] QTableView: Header sections' incorrect
painting
* [QTBUG-136477](https://qt-project.atlassian.net/browse/QTBUG-136477) Header scrolls to opposite direction
* [QTBUG-93413](https://qt-project.atlassian.net/browse/QTBUG-93413) uic and overloaded slots
* [QTBUG-136812](https://qt-project.atlassian.net/browse/QTBUG-136812) Bug in http header handling on WASM
* [QTBUG-135489](https://qt-project.atlassian.net/browse/QTBUG-135489) [REG 6.8.2->6.8.3] Handling of custom scheme URL is
broken
* [QTBUG-136333](https://qt-project.atlassian.net/browse/QTBUG-136333)  Crash occurs upon opening QFileDialog from QDialog
* [QTBUG-136042](https://qt-project.atlassian.net/browse/QTBUG-136042) Qt MySQL driver does not add milliseconds for QDateTime
in formatValue()
* [QTBUG-95071](https://qt-project.atlassian.net/browse/QTBUG-95071) mysql client version detection broken with MariaDB 10.6
* [QTBUG-133746](https://qt-project.atlassian.net/browse/QTBUG-133746) QFileSystemModel with wrong path of top-directory of a
drive
* [QTBUG-132121](https://qt-project.atlassian.net/browse/QTBUG-132121) Bad signal restoration cause infinite loop in
FatalSignalHandler destructor
* [QTBUG-135442](https://qt-project.atlassian.net/browse/QTBUG-135442) QDockWidget/QMainWindow leak widgetItems from
QDockAreaLayoutItem on dragging and QDockWidget::close()
* [QTBUG-135634](https://qt-project.atlassian.net/browse/QTBUG-135634) macOS: Deleted menu is not removed from native menu bar
* [QTBUG-25938](https://qt-project.atlassian.net/browse/QTBUG-25938) Checkable QGroupBox doesn't keep "enabled" status of
children
* [QTBUG-128648](https://qt-project.atlassian.net/browse/QTBUG-128648) Update Android Gradle plugin to 8.6.0
* [QTBUG-137579](https://qt-project.atlassian.net/browse/QTBUG-137579) QDebugStateSaver not documented well
* [QTBUG-137861](https://qt-project.atlassian.net/browse/QTBUG-137861) fatal warning: parseLocationOrError returning a dangling
reference to a temporary
* [QTBUG-128337](https://qt-project.atlassian.net/browse/QTBUG-128337) configure does not properly parse sql options
* [QTBUG-126107](https://qt-project.atlassian.net/browse/QTBUG-126107) tst_QStingConverter::invalidConverter() triggers
valgrind
* [QTBUG-126743](https://qt-project.atlassian.net/browse/QTBUG-126743) If QT_ANDROID_PACKAGE_SOURCE_DIR is set to a specific
path, a build folder is recursively created within the build folder.
* [QTBUG-135481](https://qt-project.atlassian.net/browse/QTBUG-135481) Android TV system keyboard doesn't process input
correctly
* [QTBUG-136055](https://qt-project.atlassian.net/browse/QTBUG-136055) QWebSocketServer creates persistent files in
Microsoft/Crypto/RSA on each new client connection.
* [QTBUG-135337](https://qt-project.atlassian.net/browse/QTBUG-135337) crash when connecting with RDP
* [QTBUG-49564](https://qt-project.atlassian.net/browse/QTBUG-49564) QTextCharFormat fontPointSize() doesnt not return the
same as QTextCharFormat font().pointSize()
* [QTBUG-123063](https://qt-project.atlassian.net/browse/QTBUG-123063) XCB flakiness in tst_qgraphicsscene (race condition
caused by the event dispatcher on Linux)
* [QTBUG-138158](https://qt-project.atlassian.net/browse/QTBUG-138158) QT_DISCARD_FILE_CONTENTS does not work as expected
* [QTBUG-138428](https://qt-project.atlassian.net/browse/QTBUG-138428) tst_QTextStream::pos3LargeFile() takes an extraordinary
amount of time to execute
* [QTBUG-138435](https://qt-project.atlassian.net/browse/QTBUG-138435) QTextStream::pos() seems to be linear over QFile size
(or QFile::pos())
* [QTBUG-137277](https://qt-project.atlassian.net/browse/QTBUG-137277) Stack overflow in QFontEngine (due to infinite
recursion)
* [QTBUG-138238](https://qt-project.atlassian.net/browse/QTBUG-138238) NPE when calling QtNetwork.unregisterReceiver() at exit
* [QTBUG-138484](https://qt-project.atlassian.net/browse/QTBUG-138484) QTextStream assumes single-character
QLocale::{positive,negative}Sign()
* [QTBUG-125586](https://qt-project.atlassian.net/browse/QTBUG-125586) QVariantAnimation: currentValue should not change when
calling setStartValue() and setEndValue()
* [QTBUG-138566](https://qt-project.atlassian.net/browse/QTBUG-138566) QLocale::codeToScript() can't find QLocale::LastScript
* [QTBUG-137587](https://qt-project.atlassian.net/browse/QTBUG-137587) qtdeclarative: do_compile failed when building with high
parallelism.
* [QTBUG-133725](https://qt-project.atlassian.net/browse/QTBUG-133725) qml_tool_autogen target loses almost all dependencies on
other autogen and sync_headers targets
* [QTBUG-136083](https://qt-project.atlassian.net/browse/QTBUG-136083) qtypeinfo.h uses std::is_trivial_v which will be
deprecated in C++26
* [QTBUG-137978](https://qt-project.atlassian.net/browse/QTBUG-137978) Qt.inputMethod.visible changes to true in orientation
change on iOS26 beta
* [QTBUG-138056](https://qt-project.atlassian.net/browse/QTBUG-138056) QSortFilterProxyModel: Crash when changing sourceModel
(QPropertyBindingData / QBindingStorage)
* [QTBUG-135641](https://qt-project.atlassian.net/browse/QTBUG-135641) QNetworkDiskCache leaks file descriptors
* [QTBUG-137755](https://qt-project.atlassian.net/browse/QTBUG-137755) Regression: Segfault on closing a program using
QDockWidgets, introduced by ab6f1ad77852a427ae73172ca11dacf876a0cbf7
* [QTBUG-93182](https://qt-project.atlassian.net/browse/QTBUG-93182) Occasional asserts when touch scroll NSEventPhaseEnded is
processed while event in queue indicates momentumPhase has begun
* [QTBUG-135966](https://qt-project.atlassian.net/browse/QTBUG-135966) Blacklist tst_QFileDialog::clearLineEdit() on vxworks
* [QTBUG-135626](https://qt-project.atlassian.net/browse/QTBUG-135626) QPointer causes unneccessary (invalid) downcasts
* [QTBUG-10506](https://qt-project.atlassian.net/browse/QTBUG-10506) QCalendarWidget in Chinese locale shows wrong weekday
names
* [QTBUG-84877](https://qt-project.atlassian.net/browse/QTBUG-84877) QLocale::system() uses short names of days and months for
narrow formats
* [QTBUG-136716](https://qt-project.atlassian.net/browse/QTBUG-136716) QDockWidget glitches when moving/pushing unless undocked
and redocked
* [QTBUG-137069](https://qt-project.atlassian.net/browse/QTBUG-137069) tst_QWidget::palettePropagation3() runs into UB
* [QAA-2836](https://qt-project.atlassian.net/browse/QAA-2836) Make sure that all references to "Qt Android" are changed to
"Qt for Android"
* [QTBUG-134250](https://qt-project.atlassian.net/browse/QTBUG-134250) qdoc fails to report warnings for incorrect \fn
signatures
* [QTBUG-127012](https://qt-project.atlassian.net/browse/QTBUG-127012) iOS: ASSERT: "qmlType.metaObject()" in
fileqqmltypedata.cpp, line 1019
* [QTBUG-134883](https://qt-project.atlassian.net/browse/QTBUG-134883) QML on Windows: Unable to assign ClassA to ClassA
* [QTBUG-134208](https://qt-project.atlassian.net/browse/QTBUG-134208) Mnemonic annotation is passed to screen readers
* [QTBUG-138246](https://qt-project.atlassian.net/browse/QTBUG-138246) Q{Shared,Weak}Pointer::IfCompatible cause accidental
copy/move SMFs, causing FTBFS in qtdeclarative
* [QTBUG-138155](https://qt-project.atlassian.net/browse/QTBUG-138155) qt_generate_deploy_qml_app_script: Error for space in
output name
* [QTBUG-138471](https://qt-project.atlassian.net/browse/QTBUG-138471) QString::arg() convert floating type to integer
* [QTBUG-138562](https://qt-project.atlassian.net/browse/QTBUG-138562) QLocalePrivate::codeToLanguage() does not sanitize the
input before passing it to AlphaCode
* [QTBUG-138610](https://qt-project.atlassian.net/browse/QTBUG-138610) QTemporaryFile::rename() overwrites existing file on
Android
* [QTBUG-132617](https://qt-project.atlassian.net/browse/QTBUG-132617) Unclear behaviour of QTemporaryFile::rename()
* [QTBUG-138527](https://qt-project.atlassian.net/browse/QTBUG-138527) Replace direct links to https://doc.qt.io/qt-6/
* [QTBUG-135964](https://qt-project.atlassian.net/browse/QTBUG-135964) Windows theme uses wrong colors if high-contrast mode is
activated
* [QTBUG-134093](https://qt-project.atlassian.net/browse/QTBUG-134093) Android application crashes on 16 KB page size

### qtsvg
* [QTBUG-49160](https://qt-project.atlassian.net/browse/QTBUG-49160) Rendering SVG icon in QFileBox on Fedora22 crashes Qt

### qtdeclarative
* [QTBUG-135975](https://qt-project.atlassian.net/browse/QTBUG-135975) Hover event delivery causes memory leak
* [QTBUG-134772](https://qt-project.atlassian.net/browse/QTBUG-134772) Occasional crashs on debug service rampdowns
* [QTBUG-135367](https://qt-project.atlassian.net/browse/QTBUG-135367) Compiler warning in qmlcachegen generated code
* [QTBUG-135387](https://qt-project.atlassian.net/browse/QTBUG-135387) Division by zero when changing path elements of
ShapePath imperatively
* [QTBUG-136120](https://qt-project.atlassian.net/browse/QTBUG-136120) Qml Runtime fails to correct escape -a after --
* [QTBUG-122031](https://qt-project.atlassian.net/browse/QTBUG-122031) tst_qquickapplication::state() is flaky on opensuse
* [QTBUG-134606](https://qt-project.atlassian.net/browse/QTBUG-134606) eventPoint documentation is hard to read
* [QTBUG-135334](https://qt-project.atlassian.net/browse/QTBUG-135334) [Reg 6.4 -> 6.5] qmlRegisterSingletonInstance does not
work with importPath over http
* [QTBUG-136127](https://qt-project.atlassian.net/browse/QTBUG-136127) Crash when calling Object.value() on QQmlListModel
* [QTBUG-134887](https://qt-project.atlassian.net/browse/QTBUG-134887) [REG 6.9 -> 6.10] qmllint: bogus required property
warning with generalized grouped property
* [QTBUG-135965](https://qt-project.atlassian.net/browse/QTBUG-135965) Application freezes when trigger an Action's shortcut in
sub-sub Menu
* [QTBUG-135244](https://qt-project.atlassian.net/browse/QTBUG-135244) qmlcachegen takes a long time to compile
fluentwinui3/Slider.qml
* [QTBUG-136735](https://qt-project.atlassian.net/browse/QTBUG-136735) Line: 1: Internal process (QML Puppet) crashed.
* [QTBUG-128864](https://qt-project.atlassian.net/browse/QTBUG-128864) Vulkan RHI Renderer freezes on Windows sometimes after
pressing Win-D
* [QTBUG-53863](https://qt-project.atlassian.net/browse/QTBUG-53863) tst_QQuickListView::populateTransitions(static, no
populate) crashes randomly
* [QTBUG-136256](https://qt-project.atlassian.net/browse/QTBUG-136256) When menu items are dynamically added to Menu, it should
resize to fit
* [QTBUG-96580](https://qt-project.atlassian.net/browse/QTBUG-96580) Missing documentation for QSGRenderNode::RenderState
* [QTBUG-137086](https://qt-project.atlassian.net/browse/QTBUG-137086) [Reg 6.2 -> 6.5] Crashing QML code
* [QTBUG-135039](https://qt-project.atlassian.net/browse/QTBUG-135039) Import in one component affects type resolution in
another one
* [QTBUG-123341](https://qt-project.atlassian.net/browse/QTBUG-123341) QML JavaScript function annotations not supported
* [QTBUG-131961](https://qt-project.atlassian.net/browse/QTBUG-131961) Qml engine crashes when running SameValueZero
* [QTBUG-136439](https://qt-project.atlassian.net/browse/QTBUG-136439) No more possible to use a Loader for QML hot/live
reloading since Qt 6.8.3
* [QTBUG-132644](https://qt-project.atlassian.net/browse/QTBUG-132644) Cannot receive mouse move events when modal dialog is
open
* [QTBUG-134545](https://qt-project.atlassian.net/browse/QTBUG-134545) Mouse move and touch update events are not delivered
correctly when there are modal dialogs
* [QTBUG-136810](https://qt-project.atlassian.net/browse/QTBUG-136810) crash on qml cache checksum mismatch
* [QTBUG-116675](https://qt-project.atlassian.net/browse/QTBUG-116675) QQuickWindow::grabWindow renders too small on macOS
retina
* [QTBUG-136699](https://qt-project.atlassian.net/browse/QTBUG-136699) Unexpected removal of enabled binding when parent
enabled is toggled off
* [QTBUG-133924](https://qt-project.atlassian.net/browse/QTBUG-133924) IconLabel children are positioned under Icon & text
* [QTBUG-136492](https://qt-project.atlassian.net/browse/QTBUG-136492) TreeView: Editable and non-editable items not working
correctly
* [QTBUG-137035](https://qt-project.atlassian.net/browse/QTBUG-137035) qmllint gets stuck
* [QTBUG-137411](https://qt-project.atlassian.net/browse/QTBUG-137411) [REG 6.9.0 -> 6.9.1] Building for iOS failed:
qmlcachegen segmentation fault
* [QTBUG-137196](https://qt-project.atlassian.net/browse/QTBUG-137196) qmlcachegen crashes in QQmlJSScope::filePath
* [QTBUG-136998](https://qt-project.atlassian.net/browse/QTBUG-136998) qmllint crashes when checking  required properties
* [QTBUG-131886](https://qt-project.atlassian.net/browse/QTBUG-131886) Wrong delta threshold for MultiPointTouchArea using
scale
* [QTBUG-137561](https://qt-project.atlassian.net/browse/QTBUG-137561) FAIL!  : tst_QQuickColorDialogImpl::defaults() Received
a warning that resulted in a failure
* [QTBUG-135295](https://qt-project.atlassian.net/browse/QTBUG-135295) [Reg 5.15 -> 6.8] Binding crashes when combined with
StackView and Loader
* [QTBUG-137416](https://qt-project.atlassian.net/browse/QTBUG-137416) FAIL!  : tst_QQuickFileDialogImpl::defaults() Compared
values are not the same
* [QTBUG-137270](https://qt-project.atlassian.net/browse/QTBUG-137270) QML: model-views: bindings evaluate after item/app
destruction -> crashes
* [QTBUG-137540](https://qt-project.atlassian.net/browse/QTBUG-137540) [Reg 6.5.0 -> 6.5.5] Compilation blog post example
doesn't work anymore
* [QTBUG-124157](https://qt-project.atlassian.net/browse/QTBUG-124157) QJSEngine crashes when evaluating arithmetic operation
on array with self referencing
* [QTBUG-137326](https://qt-project.atlassian.net/browse/QTBUG-137326) [Reg 5.15 -> 6.2] Crash in
QQmlAbstractBinding::removeFromObject()
* [QTBUG-118188](https://qt-project.atlassian.net/browse/QTBUG-118188) QML evaluates bindings after destruction, possibly
resulting in segmentation faults
* [QTBUG-134208](https://qt-project.atlassian.net/browse/QTBUG-134208) Mnemonic annotation is passed to screen readers
* [QTBUG-136959](https://qt-project.atlassian.net/browse/QTBUG-136959) Read-only TextEdit overrides all Shortcuts when it has
activeFocus
* [QTBUG-138242](https://qt-project.atlassian.net/browse/QTBUG-138242) Crash when GC is triggered during script exception
handling in StateChangeScript or ScriptAction
* [QTBUG-122436](https://qt-project.atlassian.net/browse/QTBUG-122436) Android a11y: Changes to Accessible.ignored and
Item.visible are not propagated to the screen reader
* [QTBUG-136688](https://qt-project.atlassian.net/browse/QTBUG-136688) QJSEngine: call eval() directly from C++ crash
application
* [QTBUG-138478](https://qt-project.atlassian.net/browse/QTBUG-138478) TapHandler doesn't react to touch input inside popup
background
* [QTBUG-138927](https://qt-project.atlassian.net/browse/QTBUG-138927) Incubator crashing when being destroyed
* [QTBUG-135407](https://qt-project.atlassian.net/browse/QTBUG-135407) [Scene Graph - Graph App] Segmentation Fault
* [QTBUG-138490](https://qt-project.atlassian.net/browse/QTBUG-138490) Incorrect item ordering in QML container when the
ListView is nested within another Item.
* [QTBUG-105856](https://qt-project.atlassian.net/browse/QTBUG-105856) The Menu Item will continue to be highlighted after the
sub menu is closed
* [QTBUG-136031](https://qt-project.atlassian.net/browse/QTBUG-136031) MouseArea in a ApplicationWindow's background can not be
hovered since 6.9.0
* [QTBUG-136248](https://qt-project.atlassian.net/browse/QTBUG-136248) Crash in QQmlPrivate::callQObjectMethod
* [QTBUG-87708](https://qt-project.atlassian.net/browse/QTBUG-87708) [Reg 5.15.0 -> 5.15.1] header's width isn't resized to
window's width when Layout is used
* [QTBUG-51285](https://qt-project.atlassian.net/browse/QTBUG-51285) Using nested QtQuick Layouts with spacing generates
binding loops
* [QTBUG-137554](https://qt-project.atlassian.net/browse/QTBUG-137554) qml: list qml --> c++ editing crashes/has no effect
* [QTBUG-138155](https://qt-project.atlassian.net/browse/QTBUG-138155) qt_generate_deploy_qml_app_script: Error for space in
output name

### qtmultimedia
* [QTBUG-130898](https://qt-project.atlassian.net/browse/QTBUG-130898) Guard QML MediaRecorder videoResolution from accessing
invalid memory address
* [QTBUG-137875](https://qt-project.atlassian.net/browse/QTBUG-137875) GUI freeze in gstreamer when unloading Video element
* [QTBUG-134607](https://qt-project.atlassian.net/browse/QTBUG-134607) Video playback crash when setting QQuickWindow
GraphicsAPI to Vulkan
* [QTBUG-138414](https://qt-project.atlassian.net/browse/QTBUG-138414) FFmpeg Plugin: Improve usability on different RHI
backend configurations

### qttools
* [QTBUG-96693](https://qt-project.atlassian.net/browse/QTBUG-96693) QUiLoader resolves  wrong buddy when UI is loaded twice

### qtdoc
* [QTBUG-136036](https://qt-project.atlassian.net/browse/QTBUG-136036) colorpaletteclient doesn't compile if qml-network is
disabled
* [QAA-2836](https://qt-project.atlassian.net/browse/QAA-2836) Make sure that all references to "Qt Android" are changed to
"Qt for Android"
* [QTBUG-138527](https://qt-project.atlassian.net/browse/QTBUG-138527) Replace direct links to https://doc.qt.io/qt-6/

### qtlocation
* [QTBUG-137557](https://qt-project.atlassian.net/browse/QTBUG-137557) QtLocation: Using GeocodeModel with OSM plugin in QML
causes app crash when canceling update

### qtpositioning
* [QTBUG-137764](https://qt-project.atlassian.net/browse/QTBUG-137764) QDoc uses incorrect image source

### qtconnectivity
* [QTBUG-136576](https://qt-project.atlassian.net/browse/QTBUG-136576) QNdefNfcSmartPosterRecord might leak memory
* [QTBUG-124130](https://qt-project.atlassian.net/browse/QTBUG-124130) Bluetooth LE service data is trunctated at zero value
* [QTBUG-136692](https://qt-project.atlassian.net/browse/QTBUG-136692) BLE devices can't be discovered after initial connection
on iOS 18+

### qtwayland
* [QTBUG-137333](https://qt-project.atlassian.net/browse/QTBUG-137333) Wayland Compositor + static build + LTO = crash
* [QTBUG-139250](https://qt-project.atlassian.net/browse/QTBUG-139250) Top-level tool window doesnt oppen

### qt3d
* [QTBUG-135394](https://qt-project.atlassian.net/browse/QTBUG-135394) MouseHandler may crash if it is destroyed while mouse is
being moved

### qtserialbus
* [QTBUG-135791](https://qt-project.atlassian.net/browse/QTBUG-135791) QModbusClient: : sendRawRequest returns pointer, if
delete immediately, QModbusRtuSerialClientPrivate: : onReadyRead
function crash

### qtserialport
* [QTBUG-133489](https://qt-project.atlassian.net/browse/QTBUG-133489) ResourceError does not fire on unplug for QtSerialPort
6.8.2

### qtwebsockets
* [QTBUG-136216](https://qt-project.atlassian.net/browse/QTBUG-136216) QWebSocket "Invalid UTF-8 Code Encountered" Error in Qt6

### qtwebengine
* [QTBUG-128440](https://qt-project.atlassian.net/browse/QTBUG-128440) Top flaky test:
tst_qwebengineview::inputContextQueryInput
* [QTBUG-135620](https://qt-project.atlassian.net/browse/QTBUG-135620) Qt6WebEngineCoreDeploySupport fails when generating RPM
* [QTBUG-109553](https://qt-project.atlassian.net/browse/QTBUG-109553) CMake deployment API creates too deep directory
hierarchy when DESTDIR is set
* [QTBUG-119077](https://qt-project.atlassian.net/browse/QTBUG-119077) CMake deployment API does not deploy Qt Webengine
* [QTBUG-135047](https://qt-project.atlassian.net/browse/QTBUG-135047) Excessive X11 pixmap usage on 6.9
* [QTBUG-126722](https://qt-project.atlassian.net/browse/QTBUG-126722) WebEngine: GPU detection is missing "VmWare" in vendor
list
* [QTBUG-135032](https://qt-project.atlassian.net/browse/QTBUG-135032) Uncreatable value types behave erratically
* [QTBUG-123607](https://qt-project.atlassian.net/browse/QTBUG-123607) Vulkan backend rendering only black on X11
* [QTBUG-127758](https://qt-project.atlassian.net/browse/QTBUG-127758) tst_QWebEnginePage::dynamicFrame() failed on Ubuntu
24.04 offscreen(arm64) and X11(x64)
* [QTBUG-126049](https://qt-project.atlassian.net/browse/QTBUG-126049) text dump does not work realibly with 122-based
* [QTBUG-133608](https://qt-project.atlassian.net/browse/QTBUG-133608) Missing documentation on how to install Qt WebEngine
* [QTBUG-131897](https://qt-project.atlassian.net/browse/QTBUG-131897) pdf viewer is not working on nano browser and simple
browser sample apps
* [QTBUG-111907](https://qt-project.atlassian.net/browse/QTBUG-111907) Crash when touching text field inside WebEngineView
* [QTBUG-138641](https://qt-project.atlassian.net/browse/QTBUG-138641) QtWebEngine rendering glitches with `<select>` element
* [QTBUG-134055](https://qt-project.atlassian.net/browse/QTBUG-134055) Make Qt WebEngine expose accessibility content properly
* [QTBUG-129769](https://qt-project.atlassian.net/browse/QTBUG-129769) WebEngine ANGLE error: Failed to make current since
context is marked as lost
* [QTBUG-133570](https://qt-project.atlassian.net/browse/QTBUG-133570) 6.9beta2/Linux/XCB: WebEngine Simple Browser example
crashes
* [QTBUG-135621](https://qt-project.atlassian.net/browse/QTBUG-135621) gn.py needs an -isysroot argument but configure doesn't
create it
* [QTBUG-137730](https://qt-project.atlassian.net/browse/QTBUG-137730) Failed to build sources on tqtc/lts-6.8:
XSLT_DEBUG_INIT’ conflicts with a previous declaration
* [COIN-1249](https://qt-project.atlassian.net/browse/COIN-1249) broken system header on rhel-8.10

### qtcharts
* [QTBUG-136770](https://qt-project.atlassian.net/browse/QTBUG-136770) QLineSeries.clear() does not remove all lines from the
plot in that series
* [QTBUG-135240](https://qt-project.atlassian.net/browse/QTBUG-135240) Animation effects in ChartView makes PieSlice lose its
alpha channel
* [QTBUG-132790](https://qt-project.atlassian.net/browse/QTBUG-132790) Unexpected behaviour of QScatterSeries for
selectedPoints, replace and deselectAllPoints
* [QTBUG-132357](https://qt-project.atlassian.net/browse/QTBUG-132357) setSelectedColor doesn't work on barsets added to
QBarSeries with insert method

### qtvirtualkeyboard
* [QTBUG-134582](https://qt-project.atlassian.net/browse/QTBUG-134582) Languages dropdown appears blank when scrolling in Qt
Keyboard
* [QTBUG-137434](https://qt-project.atlassian.net/browse/QTBUG-137434) Inconsistent Keyboard Layout Country List Display
* [QTBUG-131374](https://qt-project.atlassian.net/browse/QTBUG-131374) The wordCandidateList field is not visible on the
virtual keyboard in a widget application.

### qtquicktimeline
* [QTBUG-133543](https://qt-project.atlassian.net/browse/QTBUG-133543) An invalid keyframe file can make the application crash.

### qtquick3d
* [QTBUG-136754](https://qt-project.atlassian.net/browse/QTBUG-136754) startTime doesn't work without affectors

### qtshadertools
* [QTBUG-138033](https://qt-project.atlassian.net/browse/QTBUG-138033) FAILED: qtshadertools/src/shadertools/CMakeFiles/qattrib
utionsscanner_ShaderTools Expected license file not found

### qthttpserver
* [QTBUG-138560](https://qt-project.atlassian.net/browse/QTBUG-138560) Websocket disconnect instantly from QHttpServer

Known Issues
------------

* Check that your system meets Qt's requirements:
https://doc.qt.io/qt-6.5/supported-platforms.html

* The RTA (release test automation) reported issues in Qt 6.5.x:
https://qt-project.atlassian.net/issues/?filter=15085

* See Qt 6.5 known issues from:
https://wiki.qt.io/Qt_6.5_Known_Issues

* Qt 6.5.10 Open issues in Jira:
https://qt-project.atlassian.net/issues/?filter=10699

Credits for the  release goes to:
---------------------------------

* Eirik Aavitsland
* Laszlo Agocs
* Anu Aliyas
* Mate Barany
* Nicholas Bennett
* Eric Beuque
* Tim Blechmann
* Maximilian Blochberger
* Eskil Abrahamsen Blomfeldt
* David Boddie
* Joerg Bornemann
* Assam Boudjelthia
* Aurélien Brooke
* Kai Uwe Broulik
* Michael Brüning
* Andreas Buhr
* Olivier De Cannière
* Alexei Cazacov
* Kaloyan Chehlarski
* Alexandru Croitor
* Mitch Curtis
* Thibaut Cuvelier
* Giuseppe D'Angelo
* Szabolcs David
* Pavel Dubsky
* Paul Dubsky
* Alexey Edelev
* Oliver Eftevaag
* Christian Ehrlicher
* Andreas Eliasson
* David Faure
* Ilya Fedin
* Nicolas Fella
* Samuel Gaist
* Robert Griebl
* Richard Moe Gustavsen
* Inkamari Harjula
* Moss Heim
* Ulf Hermann
* Øystein Heskestad
* Volker Hilsheimer
* Dominik Holland
* Samuli Hölttä
* Allan Sandfeld Jensen
* Jonas Karlsson
* Kevin Keating
* Michal Klocek
* Jarkko Koivikko
* Jani Korteniemi
* Fabian Kosmale
* Volker Krause
* Santhosh Kumar
* Kai Köhne
* Lauri Laanmets
* Inho Lee
* Frédéric Lefebvre
* Robert Löhning
* Thiago Macieira
* Christophe Marin
* Bartlomiej Moskal
* Marc Mutz
* Antti Määttä
* Andy Nichols
* Mårten Nordheim
* Mikhail Paulyshka
* Joni Poikelin
* Cajus Pollmeier
* Jacek Poplawski
* Rami Potinkara
* Dheerendra Purohit
* Liang Qi
* Topi Reinio
* Shawn Rutledge
* Otto Ryynänen
* Ahmad Samir
* Lars Schmertmann
* Luca Di Sera
* Sami Shalayel
* Ivan Solovev
* Axel Spoerl
* Tarja Sundqvist
* Lars Sutterud
* Jens Trillmann
* Peter Varga
* Tor Arne Vestbø
* Ville Voutilainen
* Juha Vuolle
* Jaishree Vyas
* Michael Weghorn
* Edward Welbourne
* Piotr Wiercinski
* Milian Wolff
* Oliver Wolff
* Semih Yavuz
* Oleksii Zbykovskyi
