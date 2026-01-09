Release note
============
Qt 6.8.3 release is a patch release made on the top of Qt 6.8.2.
As a patch release, Qt 6.8.3 does not add any new functionality but provides
bug fixes and other improvements and maintains both forward and backward
compatibility (source and binary) with Qt 6.8.2.

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
* b7cd4409218 Update Harfbuzz to version 10.2.0
Upgraded Harfbuzz to version 10.2.0.

* eff8f1c0501 QtTest: Update valgrind (fatuously) to v3.24.0
Valgrind headers are up to date with Valgrind v3.24.0.

* b086e31bbdf Update public suffix list
Updated the public suffix list to upstream SHA
47264b57765919188b9f4144de8d95cf77e1b6dc.

* 7bb97b13c5e Update CLDR to v46.1
Updated CLDR data, used by QLocale, to v46.1.

* a4ab1ceb161 Update testlib's copy of Linux's perf_event_p.h header
The perf_event_p.h from Linux is updated to match Linux kernel 6.13.

* 4299115fe62 QSet: don't detach in remove()/removeIf() if nothing is
being removed
remove() and removeIf() no longer unconditionally detach, but only if
something is actually being removed.

* e8555c18c95 Long live qstdlibdetection.h!
Added Q_STL_ macros for stdlib detection (libc++, libstdc++, MSSTL,
Dinkumware, STLport, SGI, RogueWave). If your STL is lacking, please
file a bug report. Note that these macros are not considered public API
just yet.

* 0e17856f635 Revert "Optimize QSet::unite"
Fixed a regression in unite() that caused equivalent elements of
`*this` to be overwritten by elements of `other` if `other.size()` was
larger than `this->size()`.

* eb10876c7dd Unbreak QSet::intersect()
Fixed a regression (introduced for Qt 5.2) in intersect() that caused
equivalent elements of `*this` to be overwritten by elements of `other`
if `other.size()` was larger than `this->size()`.

* 4a935a192ef Improve hinted rendering quality on Windows
Improved hinted text rendering at font sizes larger than 16px.

* 129e8b429b4 SQLite: Update SQLite to v3.49.0
Updated SQLite to v3.49.0

* 95e071255d8 QDir: change qt_normalizePathSegments to preserve trailing
'/'s
Aligned how QDir and QUrl normalize paths with respect to preserving a
trailing slash. That is, QDir::cleanPath("/b/.") and
QUrl("file:///b/.).toString(QUrl::NormalizePathSegments) will return
"/b/" and "file:///b/" respectively. For more details see:
https://www.ietf.org/rfc/rfc3986.html#section-5.2.4

* 09f0470790c QUrl: set the host to empty but present for "file" URLs
Fixed a bug (regression from 6.7) where QUrl::resolved() could create
invalid URLs when the relative URI being resolved contained a path with
double slashes (e.g., combining "scheme:a" with "..//b.txt")

* d4ceec964b1 QUrl: avoid going up from the drive path on Windows file
URLs
Fixed a bug (regression from 6.7) where resolving a base URL of an
absolute file path containing a Windows drive could result in said drive
being removed (e.g., resolving "file:///c:/" with "../" would result in
"file:///").

* cbb45175deb QDesktopServices: don't use openDocument if the URL has a
query
Fixed a bug that caused QDesktopServices::openUrl() to discard a query
when opening a local file URL that contained a query but no fragment.

* b93ec378c34 QByteArray(View)::lastIndexOf: Guard against needle >
haystack
Fixed a bug in lastIndexOf() that could lead to out-of-bounds access
when the needle is longer than the haystack.

* d9d7b14f09a qEnvironmentVariableIntValue: fix off-by-one with MSVC's
getenv_s
Fixed a bug that caused qEnvironmentVariableIntValue() to fail to parse
octal values from -020000000000 to -010000000000 with MSVC. Other
compilers were not affected.

* 9fbf346c59e Update license rule to Unicode-3.0
UCD-generated data files now come under Unicode-3.0

* dbff2edaa16 Update UCD to Unicode 16.0.0
Updated the Unicode Character Database to UCD revision 34/Unicode 16.

* 7b129e56689 Update PCRE2 to 10.45
PCRE2 was updated to version 10.45.

* 9760d842624 QVariant: don't use the static CanUseInternalSpace with
existing objects
Fixed a bug where QVariant could misbehave regarding types that changed
from non-relocatable to relocatable (or vice-versa) and not all uses of
it were recompiled. To benefit from this fix, applications must be
recompiled, but they will be safe going forward.

* c3148c3081b Accept multiple fonts with the same family and style name
Fixed an issue with font families where only the last of multiple sub-
families sharing the same name would be registered.

* 73c44c83814 QLocale: fix UB (signed overflow) in formattedDataSize()
Fix issue when calling formattedDataSize() with
numeric_limits<qint64>::min().

* ee068f2ec52 QProcess/Unix: don't close the childStartedPipe too soon
Fixed a bug that caused QProcess not to report start failures if the
UnixProcessFlag::CloseFileDescriptors flag was active.

* 36be23364f6 SQLite: Update SQLite to v3.49.1
Updated SQLite to v3.49.1

* cd04bfe905f Update bundled libpng to version 1.6.47
libpng was updated to version 1.6.47

* de0b702d31c Bundle Kitware's RunCMake test module
Add upstream cmake's RunCMake test infrastructure module to
src/testinternal/3rdparty/cmake to aid in creation of cmake auto-tests.

* 52a5ac76909 QUrl: decode square brackets in fromLocalFile()
' to their percent-encoded forms. This will be visible in calls to
toString(), toEncoded(), or the encoded form of path(). QUrl's
comparison operator will consider the old (created from an encoded URL
string) and new forms to be different.

* 9d9ca53b895 Update Harfbuzz to version 10.3.0
Upgraded Harfbuzz to version 10.3.0.

* 357eafdffad Upgrade Harfbuzz to 10.4.0
Upgraded Harfbuzz to version 10.4.0.

* 9c8525ff1db 3rdparty: update TinyCBOR to v0.6.1
The copy of TinyCBOR in Qt was updated to 0.6.1.

* c07c2d5a527 CBOR/JSON: fix crash when comparing strings with different
length
Fixed bug that could result in a crash or failing to find a entry in
the map/object with non- ASCII keys.

### qtdeclarative
* 7d56cf0e98 IR Builder: Fix translation binding parsing
ListElement now supports disambiguation strings when QT_TR_NOOP is
used.

* 00f3da62f9 Qml: Fix import order for certain name resolutions
When a type name is provided by two different imports, the type from
the last import takes precedence. This is now also the case when
resolving singletons, attached types, and types for as-casts. This
aligns with the behavior for regular type resolution.

* 3b60715ca5 qmlformat: Error out when no input files are provided
qmlformat will now error out if no files are provided as positional
arguments or via the -F option.

* 773e1b2cc6 CMake: Enable building Qt and user projects without support
for aotstats
It is now possible to control whether QML Compiler statistics
(aotstats) get generated by setting the QT_QML_GENERATE_AOTSTATS CMake
variable to ON or OFF. The default value is ON.

* 7dccf86437 Make module ready for source SBOM checking
Renaming the license files with prefix LICENSE. to have them ignored by
reuse tool.

* 6e5a7384ca Auto-depend on QtQuick when linking against QtQuick
If a QML module target is linked against Qt6::Quick, QtQuick is
automatically added to its QML dependencies. This avoids tooling errors
when e.g. a QQuickItem derived type is exported by the module.

### qtmultimedia
* 96b6d5aa7 Emit each individual settings signals from
QMediaRecorder::record()
Emit specific setting signal from QMediaRecorder::record() if a
corresponding setting changed.

* 25df9e8d4 Update pffft version to the latest version from upstream
Updated pffft to 02fe771.

* 25cd2447e Fix product name and ID for the pffft third party dependency
Update pffft product name and id.

* 91455ca75 Document where to find FFmpeg build scripts
Add link to where FFmpeg build scripts can be found.

* d8d7f8945 Remove security critical label from pffft and Eigen
dependencies
Removed security critical label from pffft and Eigen third party
dependencies.

### qtconnectivity
* 4374841c BlueZ: prefer powered on adapters when no address is
specified
If the local adapter address is not specified, the Linux backend now
tries to pick the first powered on adapter instead of simply picking the
first in the list.

### qtquick3d
* f920268a5 Make module ready for source SBOM checking
Renamed certain license files outside of LICENSES with `LICENSE.`
prefix such that reuse will correctly ignore them.

### qt5compat
* fb864d3 Make module ready for source SBOM checking
Renaming the license files with prefix LICENSE. to have them ignored by
reuse tool.

### qtgrpc
* a8ca2982 Add the early return from qt6_add_<protobuf|grpc>
The qt6_add_protobuf and qt6_add_grpc functions do not generate CMake
targets if provided in PROTO_FILES argument protobuf schemes do not
contain the corresponding for the generator definitions. qtprotobufgen
requires messages or enums, qtgrpcgen requires services. Functions now
make early return and warn about the missing definitions. Previosly the
functions generated unclear FATAL_ERROR. The
QT_SKIP_PROTOBUF_MISSING_DEFINITIONS_WARNING CMake variable suppresses
the warning.


Fixes
-----

### qtbase
* [QTBUG-132891](https://bugreports.qt.io/browse/QTBUG-132891) Whitespace in projectPath fails
* [QTBUG-132398](https://bugreports.qt.io/browse/QTBUG-132398) Unsupported linker script to make objective-c classnames
unique is broken since Xcode14
* [QTBUG-131631](https://bugreports.qt.io/browse/QTBUG-131631) widgets/itemviews/simpletreemodel not configuring on iOS
* [QTBUG-132575](https://bugreports.qt.io/browse/QTBUG-132575) QEasingCurve streaming operators (in/out a QDataStream)
will crash
* [QTBUG-132609](https://bugreports.qt.io/browse/QTBUG-132609) Configuring a single-config qtopcua might fail to build
tools when built against a multi-config Qt
* [QTBUG-132338](https://bugreports.qt.io/browse/QTBUG-132338) QtOpcUa Required QtVersion Wrong
* [QTBUG-70798](https://bugreports.qt.io/browse/QTBUG-70798) Qfiledialog Does Not Correctly Restore the Directory
* [QTBUG-130884](https://bugreports.qt.io/browse/QTBUG-130884) xdg-desktop-portal should be enabled only environments
that actually supports it
* [QTBUG-132801](https://bugreports.qt.io/browse/QTBUG-132801) Building Qt with separate debug info fails on QNX
* [QTBUG-122642](https://bugreports.qt.io/browse/QTBUG-122642) The SQL QODBC driver implementation fails to escape
passwords set with setPassword(...) when using special characters.
* [QTBUG-118176](https://bugreports.qt.io/browse/QTBUG-118176) qdoc: Generate \internal documentation correctly when
--showinternal is set
* [QTBUG-132724](https://bugreports.qt.io/browse/QTBUG-132724) `qt_internal_generate_user_facing_tools_info` is not
relocatable
* [QTBUG-57209](https://bugreports.qt.io/browse/QTBUG-57209) Wrong documentation for QOpenGLTexture::setWrapMode
* [QTBUG-133128](https://bugreports.qt.io/browse/QTBUG-133128) Windows11Style: QSlider min position off
* [QTBUG-132906](https://bugreports.qt.io/browse/QTBUG-132906) Reg[6.5->6.8]Windows11 style crashing with drawPrimitive
* [QTBUG-87417](https://bugreports.qt.io/browse/QTBUG-87417) tst_QLineEdit fails on Android
* [QTBUG-132173](https://bugreports.qt.io/browse/QTBUG-132173) The cell borders in QTextTableFormat are not being
painted.
* [QTBUG-132952](https://bugreports.qt.io/browse/QTBUG-132952) Mouse messages for QDockWidget are incorrectly cast to
QMainWindow causing a crash
* [QTBUG-112758](https://bugreports.qt.io/browse/QTBUG-112758) QMdiArea (in TabbedView mode): issues after moving tab
* [QTBUG-132808](https://bugreports.qt.io/browse/QTBUG-132808) Vulkan validation error on vkAcquireNextImageKHR (using
validation layer bundled with 1.4.304)
* [QTBUG-122819](https://bugreports.qt.io/browse/QTBUG-122819) QOpenGLWidget: error: GL_INVALID_OPERATION in
glDrawBuffers(unsupported buffer GL_BACK_LEFT)
* [QTBUG-132780](https://bugreports.qt.io/browse/QTBUG-132780) Faulty call to glDrawBuffers in RhiGles2 backend
* [QTBUG-133289](https://bugreports.qt.io/browse/QTBUG-133289) Moving window container crashes if the window has been
destroyed
* [QTBUG-133207](https://bugreports.qt.io/browse/QTBUG-133207) REG: Controls C++ tests not run with all styles
* [QTBUG-132831](https://bugreports.qt.io/browse/QTBUG-132831) QSet::remove() unconditionally detaches
* [QTBUG-132945](https://bugreports.qt.io/browse/QTBUG-132945) QDuplicateTracker::clear() leaks memory
* [QTBUG-132911](https://bugreports.qt.io/browse/QTBUG-132911) Typo in QPermission docs
* [QTBUG-56952](https://bugreports.qt.io/browse/QTBUG-56952) [REG: 5.4.2->5.5.0] Duplicated hotkeys in menus not
working in some styles if first action is disabled
* [QTBUG-133430](https://bugreports.qt.io/browse/QTBUG-133430) Qt fails to build on certain Intel CPUs due to
avx512_fp16 with GCC14 (src/gui/painting/qrgbafloat.h)
* [QTBUG-133297](https://bugreports.qt.io/browse/QTBUG-133297) [macOS] Some emojis are rendering incorrect in some
sizes
* [QTBUG-132500](https://bugreports.qt.io/browse/QTBUG-132500) [REG 6.7 -> 6.8] QSet::unite() no longer consistently
picks equivalent elements from `other`
* [QTBUG-132536](https://bugreports.qt.io/browse/QTBUG-132536) QSet::intersect() picks equivalent elements
inconsistently  from `other` or *this
* [QTBUG-133101](https://bugreports.qt.io/browse/QTBUG-133101) GCC defines __PIC__ with -fPIE (was: Weird
QObject::findChild() behavior)
* [QTBUG-133032](https://bugreports.qt.io/browse/QTBUG-133032) Qt 6.8.1 "isRelocatable: undeclared identifier"
* [QTBUG-133330](https://bugreports.qt.io/browse/QTBUG-133330) tst_qmenu crashes with MSVC in debug mode
* [QTBUG-132700](https://bugreports.qt.io/browse/QTBUG-132700) [REG 6.6 -> 6.7] Click event handling not working using
mouse/trackpad on Android
* [QTBUG-130297](https://bugreports.qt.io/browse/QTBUG-130297) Cannot click buttons in ChromeOS
* [QTBUG-133405](https://bugreports.qt.io/browse/QTBUG-133405) Repeated texture readbacks crash
* [QTBUG-133516](https://bugreports.qt.io/browse/QTBUG-133516) Windows MinGW: TestNamespace errors in qcomobject
* [QTBUG-132516](https://bugreports.qt.io/browse/QTBUG-132516) Broken link to Qt Creator: Build Systems
* [QTBUG-132490](https://bugreports.qt.io/browse/QTBUG-132490) Android and TestNamespace: errors in Qt JNI methods
* [QTBUG-129233](https://bugreports.qt.io/browse/QTBUG-129233) tooltip will change focus on webassembly
* [QTBUG-131946](https://bugreports.qt.io/browse/QTBUG-131946) The quality of font rendering has dropped dramatically
since version 6.8
* [QTBUG-132057](https://bugreports.qt.io/browse/QTBUG-132057) WebAssembly - App "Window" moves outside of visible area
* [QTWEBSITE-1202](https://bugreports.qt.io/browse/QTWEBSITE-1202) Broken tabs in translated docs
* [QTBUG-133117](https://bugreports.qt.io/browse/QTBUG-133117) Windows11Style: Check boxes and radio buttons slightly
cropped at 150%
* [QTBUG-132589](https://bugreports.qt.io/browse/QTBUG-132589) Android Edit text context menu pointers are in wrong
place
* [QTBUG-133651](https://bugreports.qt.io/browse/QTBUG-133651) uic: Changing Palette in Designer breaks UI with Qt
5.15.2
* [QTBUG-132249](https://bugreports.qt.io/browse/QTBUG-132249) AndroidTestRunner: allow to call additional/extra adb
call
* [QTBUG-118032](https://bugreports.qt.io/browse/QTBUG-118032) Application crash due to double invocation of
continuation in multithreaded QPromise and QFuture usage
* [QTBUG-133403](https://bugreports.qt.io/browse/QTBUG-133403) [REG 6.8.0 -> 6.8.1]
QUrl::adjusted(NormalizePathSegments) can produce an invalid URL
* [QTBUG-133402](https://bugreports.qt.io/browse/QTBUG-133402) [REG 6.8.0 -> 6.8.1] QUrl::resolved() can produce an
invalid path like "/../"
* [QTBUG-132314](https://bugreports.qt.io/browse/QTBUG-132314) GPU driver crash in iOS 18
* [QTBUG-133663](https://bugreports.qt.io/browse/QTBUG-133663) QDesktopServices::openUrl() misses query part
* [QTBUG-133689](https://bugreports.qt.io/browse/QTBUG-133689) tst_qbytearrayview fails to compile with libc++ 19
* [QTBUG-133644](https://bugreports.qt.io/browse/QTBUG-133644) [REG 6.6.3 -> 6.8.1] Assertion failure at QApplication
destruction
* [QTBUG-133776](https://bugreports.qt.io/browse/QTBUG-133776) calling exit after constructing QApplication crash
* [QTBUG-133725](https://bugreports.qt.io/browse/QTBUG-133725) qml_tool_autogen target loses almost all dependencies on
other autogen and sync_headers targets
* [QTBUG-133808](https://bugreports.qt.io/browse/QTBUG-133808) Including QFlag causes compilation failure with Clang
19, libcpp, and C++23
* [QTBUG-133500](https://bugreports.qt.io/browse/QTBUG-133500) [REG 6.8.1 -> 6.8.2] Crash on exit during logging of
thread destruction
* [QTBUG-133810](https://bugreports.qt.io/browse/QTBUG-133810) CMake Multi-ABI builds not copying sub-ABIs libraries
* [QTBUG-131862](https://bugreports.qt.io/browse/QTBUG-131862) Android multi-ABI build stopped working
* [QTBUG-133782](https://bugreports.qt.io/browse/QTBUG-133782) Mistakenly rounding down "bytesPerLine" for QPixmap
* [QTBUG-133577](https://bugreports.qt.io/browse/QTBUG-133577) [iOS] [REG] Including a Swift file leads to a startup
error
* [QTBUG-128458](https://bugreports.qt.io/browse/QTBUG-128458) ui文件中创建了QProgressBar对象，运行出来的结果为啥是一条横线，和设计ui界面上的显示不一致
* [QTBUG-131574](https://bugreports.qt.io/browse/QTBUG-131574) Qt 6.8 displays some font families in DemiBold much
thicker than with Qt6.7
* [QTBUG-133781](https://bugreports.qt.io/browse/QTBUG-133781) Regression - Button clicks open keyboard in WebAssembly
on Android
* [QTBUG-130458](https://bugreports.qt.io/browse/QTBUG-130458) Fusion theme doesn't use accent color in Windows light
mode
* [QTBUG-129300](https://bugreports.qt.io/browse/QTBUG-129300) Cannot bind QRhi 3D texture to shader in DirectX 11 and
12 (with working workaround)
* [QTBUG-115356](https://bugreports.qt.io/browse/QTBUG-115356) QMenu clips text for actions with icons with larger
fonts
* [QTBUG-131893](https://bugreports.qt.io/browse/QTBUG-131893) QToolButton menu selections fail to highlight when in
QMdiSubwindow
* [QTBUG-107904](https://bugreports.qt.io/browse/QTBUG-107904) Qt Designer crashes when set a negative value in border-
image
* [QTBUG-134073](https://bugreports.qt.io/browse/QTBUG-134073) QMimeData does not escape square brackets in text/uri-
list
* [QTBUG-134316](https://bugreports.qt.io/browse/QTBUG-134316) [Reg] QFileOpenEvent isn't emitted for custom URI
* [QTBUG-133744](https://bugreports.qt.io/browse/QTBUG-133744) QString assertion failure using UTF-16 character in
QJsonObject key
* [QTBUG-123711](https://bugreports.qt.io/browse/QTBUG-123711) QtQuickView doesn't handle recreation of Activity
properly
* [QTBUG-132785](https://bugreports.qt.io/browse/QTBUG-132785) QFile::rename() deletes file and fails to rename on
Windows/NFS
* [QTBUG-12673](https://bugreports.qt.io/browse/QTBUG-12673) Crash in QWidgetPrivate::init on QApplication::quit()
using a modal dialog on Mac
* [QTBUG-132507](https://bugreports.qt.io/browse/QTBUG-132507) Fix review findings in QUniqueHandle
* [QTBUG-132646](https://bugreports.qt.io/browse/QTBUG-132646) Add a variant of QTemporaryFile::rename() that
overwrites
* [QTBUG-131916](https://bugreports.qt.io/browse/QTBUG-131916) Quoting and QML files with white spaces in the path are
not supported in qmldir
* [QTBUG-133206](https://bugreports.qt.io/browse/QTBUG-133206) QThreadPrivate saying "QThreadStorage: Thread %p exited
after QThreadStorage %d destroyed"
* [QTBUG-131894](https://bugreports.qt.io/browse/QTBUG-131894) qtranslator loads wrong locale
* [QTBUG-129222](https://bugreports.qt.io/browse/QTBUG-129222) Sporadic segfault at getenv from pulseaudio during boot
* [QTBUG-114957](https://bugreports.qt.io/browse/QTBUG-114957) Clarify handling of FileDialog.nameFilter on Android
* [QTBUG-132070](https://bugreports.qt.io/browse/QTBUG-132070) Ubuntu 24.04 x64: Sometimes hundreds of tests failing
* [QTBUG-126827](https://bugreports.qt.io/browse/QTBUG-126827) Configuring a cmake-based Qt Quick project fails if the
path contains spaces
* [QTBUG-125569](https://bugreports.qt.io/browse/QTBUG-125569) Make sure licensing in file matches that in
qt_attribution.json
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-133269](https://bugreports.qt.io/browse/QTBUG-133269) QTextStream: suspicious negation when streaming numbers
* [QTBUG-126054](https://bugreports.qt.io/browse/QTBUG-126054) QString::arg(wchar_t{}) prefers the integral overload
instead of the QChar one
* [QTBUG-129108](https://bugreports.qt.io/browse/QTBUG-129108) Menus and action visibility
* [QTBUG-128940](https://bugreports.qt.io/browse/QTBUG-128940) FAIL!  :
qmltestrunner::AnimatedImage::test_imageSource(local not found) Not all
expected messages were received
* [QTBUG-127953](https://bugreports.qt.io/browse/QTBUG-127953) Basic support for CMake FetchContent
* [QTBUG-132433](https://bugreports.qt.io/browse/QTBUG-132433) Windows 11 style - QToolButton/QPushButton quirks
* [QTBUG-30133](https://bugreports.qt.io/browse/QTBUG-30133) QScroller auto-test is flakey
* [QTBUG-107893](https://bugreports.qt.io/browse/QTBUG-107893) cmake: multi-ABI Android builds do not forward cmake
arguments
* [QTBUG-132633](https://bugreports.qt.io/browse/QTBUG-132633) QDir::mkpath() is missing an overload with permissions
* [QTBUG-106025](https://bugreports.qt.io/browse/QTBUG-106025) REG: isSignalConnected creates a dead lock.
* [QTBUG-133761](https://bugreports.qt.io/browse/QTBUG-133761) Update Qt Creator help mode colours to match the current
themes
* [QTBUG-134250](https://bugreports.qt.io/browse/QTBUG-134250) qdoc fails to report warnings for incorrect \fn
signatures

### qtsvg
* [QTBUG-132468](https://bugreports.qt.io/browse/QTBUG-132468) Polyline with stroke displays nothing when all points
are the same

### qtdeclarative
* [QTBUG-132805](https://bugreports.qt.io/browse/QTBUG-132805) qmllint: default property
* [QTBUG-132792](https://bugreports.qt.io/browse/QTBUG-132792) qtabstractitemmodel_java settings.gradle has duplicate
information
* [QTBUG-128229](https://bugreports.qt.io/browse/QTBUG-128229) JavaScript library has cyclic dependeny on itself when
importing its own qml module
* [QTBUG-127294](https://bugreports.qt.io/browse/QTBUG-127294) qmllint: too many warnings when accessing an attached
type from a value type
* [QTBUG-132684](https://bugreports.qt.io/browse/QTBUG-132684) Using QT_TR_NOOP with disambiguation string in a
ListElement causes runtime error
* [QTBUG-132134](https://bugreports.qt.io/browse/QTBUG-132134) qmlls crashed
* [QTBUG-133047](https://bugreports.qt.io/browse/QTBUG-133047) [Reg 6.5 -> 6.8] qmlsc: list<QtObject> property-of-a-
property is not bound correctly
* [QTBUG-132921](https://bugreports.qt.io/browse/QTBUG-132921) Crash in QmlCacheGeneratedCode
* [QTBUG-128420](https://bugreports.qt.io/browse/QTBUG-128420) Qt 6.8 does not support build paths with white spaces
anymore
* [QTBUG-133230](https://bugreports.qt.io/browse/QTBUG-133230) Removed ShapePaths are still rendered
* [QTBUG-133231](https://bugreports.qt.io/browse/QTBUG-133231) Removing ShapePaths from Shape results in properties for
other shapes being confused
* [QTBUG-132280](https://bugreports.qt.io/browse/QTBUG-132280) qmlformat: The optional chaining operator (JavaScript)
is incorrectly removed when followed by an array access
* [QTBUG-131386](https://bugreports.qt.io/browse/QTBUG-131386) qmlformat inserts a new space after block comment on
file save
* [QTBUG-133323](https://bugreports.qt.io/browse/QTBUG-133323) gcc 15: build error with src/qmldom/qqmldomtop.cpp
* [QTBUG-133052](https://bugreports.qt.io/browse/QTBUG-133052) modelData is lost when using a nested QML component
inside a Repeater
* [QTBUG-133129](https://bugreports.qt.io/browse/QTBUG-133129) DelegateModel can create delegates with unset required
properties in sub-objects
* [QTBUG-131903](https://bugreports.qt.io/browse/QTBUG-131903) Item.transform is not readonly
* [QTBUG-133526](https://bugreports.qt.io/browse/QTBUG-133526) Error: qmlcachegen inappropriately resolves file paths
* [QTBUG-132065](https://bugreports.qt.io/browse/QTBUG-132065) qmlformat: 'From' properties confuses
IndentingLineWriter
* [QTBUG-133053](https://bugreports.qt.io/browse/QTBUG-133053) [Reg 6.5 -> 6.8] Qt 6.8 silently removed sharing of
global variables between 2 typescript/javascript files
* [QTBUG-130570](https://bugreports.qt.io/browse/QTBUG-130570) "Scene Graph - RHI Under QML" documentation error
* [QTBUG-133301](https://bugreports.qt.io/browse/QTBUG-133301) Crash when moving columns in an empty qml tableview
* [QTBUG-133566](https://bugreports.qt.io/browse/QTBUG-133566) tst_qquickmenu::popup() is flaky
* [QTBUG-132263](https://bugreports.qt.io/browse/QTBUG-132263) qmlls can find a module but not its types
* [QTBUG-133380](https://bugreports.qt.io/browse/QTBUG-133380) FAIL!  : tst_QQuickMenu::FluentWinUI3::mouse(Popup.Item)
Compared values are not the same
* [QTBUG-133341](https://bugreports.qt.io/browse/QTBUG-133341) flaky test
Tst_touchMouse::touchCancelWillCancelMousePress
* [QTBUG-132648](https://bugreports.qt.io/browse/QTBUG-132648) tst_TouchMouse::touchButtonOnFlickable is flaky on
opensuse
* [QTBUG-132630](https://bugreports.qt.io/browse/QTBUG-132630) tst_qquickmousearea::doubleTap is flaky on opensuse
* [QTBUG-133342](https://bugreports.qt.io/browse/QTBUG-133342) Tst_QQuickMultiPointTouchArea::inFlickable2 is flaky on
Opensuse
* [QTBUG-133343](https://bugreports.qt.io/browse/QTBUG-133343) Tst_qquickmousearea::doubleTap flaky on Opensuse
* [QTBUG-132941](https://bugreports.qt.io/browse/QTBUG-132941) Top flaky test:
tst_QQuickMouseArea::nestedFlickableStopAtBounds
* [QTBUG-133344](https://bugreports.qt.io/browse/QTBUG-133344) Tst_qquickpinchhandler::scale is flaky on Opensuse
* [QTBUG-123341](https://bugreports.qt.io/browse/QTBUG-123341) QML JavaScript function annotations not supported
* [QTBUG-132802](https://bugreports.qt.io/browse/QTBUG-132802) qtquickview_kotlin example source value 8 is obsolete
and will be removed in a future release
* [QTBUG-133461](https://bugreports.qt.io/browse/QTBUG-133461) [REG: 6.6.1 → 6.8.2] Change to singleton status of Qt
* [QTBUG-58643](https://bugreports.qt.io/browse/QTBUG-58643) QQmlListProperty has no examples of its usage
* [QTBUG-130705](https://bugreports.qt.io/browse/QTBUG-130705) QQmlListProperty is missing documentation for object /
data
* [QTBUG-119545](https://bugreports.qt.io/browse/QTBUG-119545) Document that the URL passed to Qt.createQmlObject() can
make it override existing components
* [QTBUG-133636](https://bugreports.qt.io/browse/QTBUG-133636) [Reg 6.7.3 -> 6.8.0] Qt StateMachine crashes during a
signal transition.
* [QTBUG-133745](https://bugreports.qt.io/browse/QTBUG-133745) Link not shown correctly
* [QTBUG-132409](https://bugreports.qt.io/browse/QTBUG-132409) QML registration macros are documented in QQmlEngine
* [QTBUG-89432](https://bugreports.qt.io/browse/QTBUG-89432) QML enum documentation should make a greater distinction
between using enums declared in C++ and declaring enums in QML
* [QTBUG-133460](https://bugreports.qt.io/browse/QTBUG-133460) [REG: 6.7.2 → 6.8.2] Change in binding resolution
behavior
* [QTBUG-130370](https://bugreports.qt.io/browse/QTBUG-130370) Missing docs for QML_NAMESPACE_EXTENDED()
* [QTBUG-131002](https://bugreports.qt.io/browse/QTBUG-131002) Add a way to disable aotstats statistics file
generations
* [QTBUG-134053](https://bugreports.qt.io/browse/QTBUG-134053) Doc: Remove duplicate paragraph in 'Menu QML Type' and
add missing ')'
* [QTBUG-133852](https://bugreports.qt.io/browse/QTBUG-133852) VectorImage: Scaled text elements have bad kerning
* [QTBUG-133492](https://bugreports.qt.io/browse/QTBUG-133492) Issue found on Qt 6.8 variant that doesn't exist on 6.6
* [QTBUG-130764](https://bugreports.qt.io/browse/QTBUG-130764) Affector does not have property "velocity"?
* [QTBUG-134043](https://bugreports.qt.io/browse/QTBUG-134043) tst_QQuickColorDialogImpl::dialogCanMoveBetweenWindows
is flaky
* [QTBUG-133587](https://bugreports.qt.io/browse/QTBUG-133587) Putting *.js file under QML_FILES and applying QTP0004
can break QML engine's ability to import module
* [QTBUG-134398](https://bugreports.qt.io/browse/QTBUG-134398) Qt Design Studio does not work with Qt 6.8 because of
QML caching
* [QTBUG-134320](https://bugreports.qt.io/browse/QTBUG-134320) memory leak in listview usage (QQuickItemView)
* [QTBUG-124913](https://bugreports.qt.io/browse/QTBUG-124913) Weird compiler warning message when using unresolved
function
* [QTBUG-131961](https://bugreports.qt.io/browse/QTBUG-131961) Qml engine crashes when running SameValueZero
* [QTBUG-125289](https://bugreports.qt.io/browse/QTBUG-125289) Add an overload of toScriptValue that only produces
vanilla JavaScript types
* [QTBUG-132931](https://bugreports.qt.io/browse/QTBUG-132931) QJSEngine leaks memory
* [QTBUG-130374](https://bugreports.qt.io/browse/QTBUG-130374) tst_qquicktextedit is flaky on Linux
* [QTBUG-131894](https://bugreports.qt.io/browse/QTBUG-131894) qtranslator loads wrong locale
* [QTBUG-133530](https://bugreports.qt.io/browse/QTBUG-133530) Several Controls tests failing after test coverage
restored
* [QTBUG-133305](https://bugreports.qt.io/browse/QTBUG-133305) QDeclarative crashes with PARAM_RTP_MEM_FILL=FALSE on
VxWorks
* [QTBUG-130879](https://bugreports.qt.io/browse/QTBUG-130879) "Failed to build texture render target for layer" error
log when using Flickable, resizeContent and layer.enabled
* [QTBUG-87776](https://bugreports.qt.io/browse/QTBUG-87776) Move Qt::FooPrivate targets into separate CMake packages
* [QTBUG-133858](https://bugreports.qt.io/browse/QTBUG-133858) tst_QQuickMenu::contextMenuKeyboard is flaky under
stress
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-134269](https://bugreports.qt.io/browse/QTBUG-134269) Attached properties using REVISION produce error
* [QTCREATORBUG-32591](https://bugreports.qt.io/browse/QTCREATORBUG-32591) qmlls still not work in qt creator
* [QTBUG-134250](https://bugreports.qt.io/browse/QTBUG-134250) qdoc fails to report warnings for incorrect \fn
signatures

### qtactiveqt
* [QTBUG-123520](https://bugreports.qt.io/browse/QTBUG-123520) QAxObject has invalid properties that can not be set
either
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtmultimedia
* [QTBUG-132463](https://bugreports.qt.io/browse/QTBUG-132463) Recording video and audio with AAC audio codec don't
play back correctly in Windows Media Player or Quicktime on macOS
* [QTBUG-126276](https://bugreports.qt.io/browse/QTBUG-126276) QMediaRecorder fails to encode to Matroska file format
with some codecs
* [QTBUG-119355](https://bugreports.qt.io/browse/QTBUG-119355) MediaPlayerApp-Desktop-example Unplugging the audio
output freezes the media and prevent it from being played
* [QTBUG-132525](https://bugreports.qt.io/browse/QTBUG-132525) [CoreAudio] sampling rate ranges are wrong
* [QTBUG-130299](https://bugreports.qt.io/browse/QTBUG-130299) [windows] Sporadic ASSERT on QMediaPlayer destruction
* [QTBUG-133201](https://bugreports.qt.io/browse/QTBUG-133201) Recording audio can crash if audio was previously
recorded with a codec with a bigger buffer size
* [QTBUG-113247](https://bugreports.qt.io/browse/QTBUG-113247) Crash when recording wav audio
* [QTBUG-132532](https://bugreports.qt.io/browse/QTBUG-132532) Audiorecoder example bugs
* [QTBUG-133250](https://bugreports.qt.io/browse/QTBUG-133250) QImageCapture::fileFormatChanged signal fires when value
is unchanged
* [QTBUG-131114](https://bugreports.qt.io/browse/QTBUG-131114) Workaround needed for video pixel formats that use RG8
textures on GLES2
* [QTBUG-133096](https://bugreports.qt.io/browse/QTBUG-133096) QML ImageCapture property fileFormat is read-only
* [QTBUG-124131](https://bugreports.qt.io/browse/QTBUG-124131) Recording MP3 fails on Windows with Intel Microphone
Array
* [QTBUG-131286](https://bugreports.qt.io/browse/QTBUG-131286) Cannot use QML video example on MacOS
* [QTBUG-128802](https://bugreports.qt.io/browse/QTBUG-128802) [ffmpeg] QMediaPlayer::isSeekable returns true for
sequential QIODevice
* [QTBUG-126259](https://bugreports.qt.io/browse/QTBUG-126259) Encoding odd-sized custom frames causes ASAN crash in
sws_rescale
* [QTBUG-130386](https://bugreports.qt.io/browse/QTBUG-130386) [QML] MediaPlayer{}/Video{} crashes when changing the
media source right after calling play()
* [QTBUG-128908](https://bugreports.qt.io/browse/QTBUG-128908) HLS video stream (m3u8) has glitches and delay in the
first segment
* [QTBUG-131688](https://bugreports.qt.io/browse/QTBUG-131688) Ffmpeg backend build fails if openssl 1.1 is used
* [QTBUG-133813](https://bugreports.qt.io/browse/QTBUG-133813) Document that QML VideoOutput is a subclass of Item
* [QTBUG-134090](https://bugreports.qt.io/browse/QTBUG-134090) [REG 6.9.0beta3 snapshot->6.9.0 beta3] the
-DFEATURE_gui=OFF build fails
* [QTBUG-133033](https://bugreports.qt.io/browse/QTBUG-133033) QMediaPlayer may crash during shutdown
* [QTBUG-134085](https://bugreports.qt.io/browse/QTBUG-134085) Cannot play recorded video on declarative-example
* [QTBUG-133773](https://bugreports.qt.io/browse/QTBUG-133773) Cannot record a video with QML camera
* [QTBUG-134135](https://bugreports.qt.io/browse/QTBUG-134135) qandroidvideoframebuffer.cpp gives "error: variable
length arrays in C++ are a Clang extension" errors with NDK r27c
* [QTBUG-125238](https://bugreports.qt.io/browse/QTBUG-125238) QVideoFrame::toImage fails on Android with 16 bit per
component planar YUV formats
* [QTBUG-125956](https://bugreports.qt.io/browse/QTBUG-125956) Unit testing of new APIs
* [QTBUG-130089](https://bugreports.qt.io/browse/QTBUG-130089) Encoding to H264 fails on macOS ARM in Qt CI
* [QTBUG-132778](https://bugreports.qt.io/browse/QTBUG-132778) Error compiling multimedia examples on iOS
* [QTBUG-132087](https://bugreports.qt.io/browse/QTBUG-132087) QCamera::cameraFormat does not update correctly
* [QTBUG-127000](https://bugreports.qt.io/browse/QTBUG-127000) Incorrect frame rate when starting H264 video. Incorrect
playback stop.
* [QTBUG-133563](https://bugreports.qt.io/browse/QTBUG-133563) Omit from showing debug output for QtMultimedia
* [QTBUG-116782](https://bugreports.qt.io/browse/QTBUG-116782) FFmpeg backend: RTSP stream is very choppy in Qt,
compared to FFplay
* [QTBUG-133538](https://bugreports.qt.io/browse/QTBUG-133538) Qt 6.8.2 limited supported audio formats
* [QTBUG-116015](https://bugreports.qt.io/browse/QTBUG-116015) REG: Qt6 Audio device enumeration fails on Linux system
without pulseaudio or with pulseaudio disabled.
* [QTBUG-133914](https://bugreports.qt.io/browse/QTBUG-133914) FFmpeg plugin tests may fail to build on Linux and
Android
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qttools
* [QTBUG-131931](https://bugreports.qt.io/browse/QTBUG-131931) Fix incorrect documentation for \reimp
* [QTBUG-132953](https://bugreports.qt.io/browse/QTBUG-132953) tst_helpengineplugin.cpp:41:9: error: unknown type name
'DomCreationOptions
* [QTBUG-132613](https://bugreports.qt.io/browse/QTBUG-132613) lrelease: OUTPUT_LOCATION is ignored for auto-generated
*.ts files
* [QTBUG-126546](https://bugreports.qt.io/browse/QTBUG-126546) Attribution documentation processed twice in CI
* [QTBUG-95236](https://bugreports.qt.io/browse/QTBUG-95236) qttools fails configure with deactivated features.
* [QTBUG-127789](https://bugreports.qt.io/browse/QTBUG-127789) Generated TS files are missing the language and
sourcelanguage attributes
* [QTBUG-134195](https://bugreports.qt.io/browse/QTBUG-134195) Qt Widgets Designer/Property editor: theme icons
dropdown shown for  maximumSize Width property
* [QTBUG-134256](https://bugreports.qt.io/browse/QTBUG-134256) Coverity: Use after free in Qt Designer's property
editor

### qtdoc
* [QTBUG-132360](https://bugreports.qt.io/browse/QTBUG-132360) On QtDice example top and bottom bar are partially
visible.
* [QTBUG-133503](https://bugreports.qt.io/browse/QTBUG-133503) Add Qt list of vulnerabilities in Security overview
* [QTBUG-116765](https://bugreports.qt.io/browse/QTBUG-116765) qmlformat: unnecessarily formats single line to multiple
lines
* [QTBUG-107030](https://bugreports.qt.io/browse/QTBUG-107030) Update documentation of QML
* [QTBUG-132704](https://bugreports.qt.io/browse/QTBUG-132704)  Car Configurator demo crashes on startup
* [QTBUG-132738](https://bugreports.qt.io/browse/QTBUG-132738) Errors in some examples
* [QTBUG-133305](https://bugreports.qt.io/browse/QTBUG-133305) QDeclarative crashes with PARAM_RTP_MEM_FILL=FALSE on
VxWorks
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-134220](https://bugreports.qt.io/browse/QTBUG-134220) The xcb-xinerama is missing from table listing Qt
requirements on X11
* [QTBUG-134251](https://bugreports.qt.io/browse/QTBUG-134251) Qt Quick for Android is hard to find

### qtlocation
* [QTBUG-128901](https://bugreports.qt.io/browse/QTBUG-128901) MapPolyline cannot tolerate empty QGeoPath when
referenceSurface is set to Globe
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtpositioning
* [QTBUG-133935](https://bugreports.qt.io/browse/QTBUG-133935) QML Qt Positioning memory use after free() / double
free()
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtsensors
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtconnectivity
* [QTBUG-116664](https://bugreports.qt.io/browse/QTBUG-116664) Bluetooth (linux) non-functional if 2 hci devices
present and hci0 is disabled
* [QTBUG-133534](https://bugreports.qt.io/browse/QTBUG-133534) Warn user that too large data can make
QLowEnergyAdvertisingData::setManufacturerData fail in error
* [QTBUG-133553](https://bugreports.qt.io/browse/QTBUG-133553) [REG: 6.8.0->6.8.1] Duplicated symbol
OrgFreedesktopDBusPropertiesInterface::staticMetaObject' between QtGui
and QtConnectivity
* [QTBUG-133975](https://bugreports.qt.io/browse/QTBUG-133975) BLUETOOTH_SCAN permission in Split APK / AAB
(QtBluetoothUtility.java)
* [QTBUG-133788](https://bugreports.qt.io/browse/QTBUG-133788) Ndef editor example cross-compiling on Windows to
Boot2Qt fails
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtwayland
* [QTBUG-133204](https://bugreports.qt.io/browse/QTBUG-133204) QCursor::pos stuck at (0, 0) until mouse click/move
(wayland, kwin)
* [QTBUG-132196](https://bugreports.qt.io/browse/QTBUG-132196) text input v3: input method active with popup menu
* [QTBUG-120384](https://bugreports.qt.io/browse/QTBUG-120384) Define "manufacturer" in WaylandOutput documentation
* [QTBUG-132642](https://bugreports.qt.io/browse/QTBUG-132642) custom-extension example broken
* [QTBUG-134071](https://bugreports.qt.io/browse/QTBUG-134071) [qtwayland] Manual tests fail to compile
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qt3d
* [QTBUG-133931](https://bugreports.qt.io/browse/QTBUG-133931) QDoc: error: Documentation warnings (48) exceeded the
limit (0) for 'Qt3D'.

### qtimageformats
* [QTBUG-134112](https://bugreports.qt.io/browse/QTBUG-134112) 16-bit Grayscale TIFF is not loaded correctly
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtserialbus
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtserialport
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtwebsockets
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtwebchannel
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtwebengine
* [QTBUG-130608](https://bugreports.qt.io/browse/QTBUG-130608) Dropdown in WebEngineView are not zoomed and aligned
properly when parent of WebEngineView is zoomed.
* [QTBUG-128893](https://bugreports.qt.io/browse/QTBUG-128893) sbom for qtpdf gets lost , as it ends up as qtwebengine
sbom
* [QTBUG-132411](https://bugreports.qt.io/browse/QTBUG-132411) Chromium version isn't reduced in user-agent string
* [QTBUG-131969](https://bugreports.qt.io/browse/QTBUG-131969) "Spellchecking can not be enabled" error logged when
disabling spell checking
* [QTBUG-132682](https://bugreports.qt.io/browse/QTBUG-132682) [REG 6.9] Segfault in
{{QtWebEngineCore::NativeSkiaOutputDeviceOpenGL::texture()}} with
offscreen platform
* [QTBUG-133558](https://bugreports.qt.io/browse/QTBUG-133558) DRM video fails to play on macOS
* [QTBUG-133590](https://bugreports.qt.io/browse/QTBUG-133590) tst_qwebengineview::keyboardFocusAfterPopup on macos
* [QTBUG-133649](https://bugreports.qt.io/browse/QTBUG-133649) When calling QWebEngineView::setFocus after calling
QWebEngineView::setFocus for the second time, focus is given to another
widget
* [QTBUG-131841](https://bugreports.qt.io/browse/QTBUG-131841) PdfScrollablePageView does not work in the app
* [QTBUG-134248](https://bugreports.qt.io/browse/QTBUG-134248) QDoc: error: Documentation warnings (6) exceeded the
limit (2) for 'QtWebEngine'.
* [QTBUG-117478](https://bugreports.qt.io/browse/QTBUG-117478) qtwebengine h264 broken on Windows
* [QTBUG-132479](https://bugreports.qt.io/browse/QTBUG-132479) [Windows] After download is interrupted,
QWebEngineDownloadRequest::resume() crashes with "Observers can only be
added once!"
* [QTBUG-132473](https://bugreports.qt.io/browse/QTBUG-132473) QWebEngineDownloadRequest::DownloadInterrupted creates
multiple, inconsistent QWebEngineDownloadRequest objects
* [QTBUG-133970](https://bugreports.qt.io/browse/QTBUG-133970) QtPDF spdx files not included in MinGW content
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtwebview
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtcharts
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtdatavis3d
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtvirtualkeyboard
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-127557](https://bugreports.qt.io/browse/QTBUG-127557) QtVirtualKeyboard crash introduced in 6.5.4
* [QTBUG-133241](https://bugreports.qt.io/browse/QTBUG-133241) VKB basic example's doc is missing cmake explanation

### qtscxml
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtspeech
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtnetworkauth
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtremoteobjects
* [QTBUG-132738](https://bugreports.qt.io/browse/QTBUG-132738) Errors in some examples
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtlottie
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtquicktimeline
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtquick3d
* [QTBUG-132811](https://bugreports.qt.io/browse/QTBUG-132811) ExtendedSceneEnvironment does not work with multiview
* [QTBUG-133367](https://bugreports.qt.io/browse/QTBUG-133367) PointLight with shadows crashes XR application when
using vulkan backend
* [QTBUG-132042](https://bugreports.qt.io/browse/QTBUG-132042) Qt6Quick3DRuntimeRender crashes on Android
* [QTBUG-132838](https://bugreports.qt.io/browse/QTBUG-132838) Debug build fails at rendererimpl
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtshadertools
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qt5compat
* [QTBUG-132209](https://bugreports.qt.io/browse/QTBUG-132209) Missing information on 'Qt 5 Compatibility APIs:
Graphical Effects' landing page
* [QTBUG-133892](https://bugreports.qt.io/browse/QTBUG-133892) QDoc: error: Documentation warnings (6) exceeded the
limit (0) for 'QtCore5Compat'.
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtopcua
* [QTBUG-133890](https://bugreports.qt.io/browse/QTBUG-133890) wrong licensing in
/Users/qt/work/install/sbom/qtopcua-6.10.0.source.spdx
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtlanguageserver
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qthttpserver
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtquick3dphysics
* [QTBUG-134277](https://bugreports.qt.io/browse/QTBUG-134277) [clang-cl] PhysX build failure
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtgrpc
* [QTBUG-132907](https://bugreports.qt.io/browse/QTBUG-132907) QtCore.proto and QtGui.proto are missing in developer
builds
* [QTBUG-132954](https://bugreports.qt.io/browse/QTBUG-132954) QDoc: error: Documentation warnings (2) exceeded the
limit (0) for 'QtProtobuf'
* [QTBUG-132848](https://bugreports.qt.io/browse/QTBUG-132848) qt_add_protobuf and qt_add_grpc should print a warning
if .proto files miss respective definitions
* [QTBUG-133937](https://bugreports.qt.io/browse/QTBUG-133937) Grpc: harden channel against error state reconnections
* [QTBUG-134266](https://bugreports.qt.io/browse/QTBUG-134266) grpc chat example doesn't install all libraries
* [QTBUG-120214](https://bugreports.qt.io/browse/QTBUG-120214) Add the support of implicit convertion of protobuf well-
known types from JSON input
* [QTBUG-125406](https://bugreports.qt.io/browse/QTBUG-125406) QtGrpc: rework documentation
* [QTBUG-130555](https://bugreports.qt.io/browse/QTBUG-130555) JSON serialization of google.protobuf.Timestamp seems to
be off
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-134250](https://bugreports.qt.io/browse/QTBUG-134250) qdoc fails to report warnings for incorrect \fn
signatures
* [QTBUG-134273](https://bugreports.qt.io/browse/QTBUG-134273) QtGrpc: Abstract namespaces are not working with
QLocalSocket

### qtquickeffectmaker
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtgraphs
* [QTBUG-132753](https://bugreports.qt.io/browse/QTBUG-132753) GraphAnimation crashes eventually with out of range
* [QTBUG-132611](https://bugreports.qt.io/browse/QTBUG-132611) can't remove margin of GraphsView
* [QTBUG-131111](https://bugreports.qt.io/browse/QTBUG-131111) LineSeries bugs
* [QTBUG-133359](https://bugreports.qt.io/browse/QTBUG-133359) qtGraphs ValueAxis labelFormat does not support the same
formatting options that the qtCharts one
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtapplicationmanager (Commercial only)
* [QTBUG-133605](https://bugreports.qt.io/browse/QTBUG-133605) Bubblewrap plugin is not handling bwrap option order
correctly
* [QTBUG-134214](https://bugreports.qt.io/browse/QTBUG-134214) [WARN | am.system] when running 'hello-world' on Boot to
Qt
* [QTBUG-134539](https://bugreports.qt.io/browse/QTBUG-134539) Failed to verify signature (no chain of trust)

### qtinterfaceframework (Commercial only)
* [QTBUG-133958](https://bugreports.qt.io/browse/QTBUG-133958) QDoc: error: Documentation warnings (9) exceeded the
limit (0) for 'QtInterfaceFramework'.
* [QTBUG-134684](https://bugreports.qt.io/browse/QTBUG-134684) A crash occurred in C:\Users\qt\work\qt\qtinterfaceframe
work_standalone_tests\tests\auto\core\qifabstractfeature\tst_qifabstract
feature.exe.

### qmlcompilerplus (Commercial only)
* [QTBUG-124913](https://bugreports.qt.io/browse/QTBUG-124913) Weird compiler warning message when using unresolved
function

Known Issues
------------

* Check that your system meets Qt's requirements:
https://doc.qt.io/qt-6.8/supported-platforms.html
* RTA reported issues from Qt 6.8
https://qt-project.atlassian.net/issues/?filter=10287
* See Qt 6.8 known issues from:
https://wiki.qt.io/Qt_6.8_Known_Issues
* Qt 6.8.3 Open issues in Jira:
https://qt-project.atlassian.net/issues/?filter=10647

Credits for the  release goes to:
---------------------------------

Eirik Aavitsland  
Laszlo Agocs  
Owais Akhtar  
Konsta Alajärvi  
Anu Aliyas  
Even Oscar Andersen  
Soheil Armin  
Mate Barany  
Vladimir Belyavsky  
Nicholas Bennett  
Kizito Birabwa  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
David Boddie  
Joerg Bornemann  
Assam Boudjelthia  
Aurélien Brooke  
Kai Uwe Broulik  
Michael Brüning  
Benjamin Buch  
Oswald Buddenhagen  
Olivier De Cannière  
Alexei Cazacov  
Kaloyan Chehlarski  
Albert Astals Cid  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Szabolcs David  
Pavel Dubsky  
Artem Dyomin  
Alexey Edelev  
Oliver Eftevaag  
Christian Ehrlicher  
Hatem ElKharashy  
Andreas Eliasson  
David Faure  
Ilya Fedin  
Ilya Flikov  
Andrew Forrest  
Joshua Goins  
Robert Griebl  
Jan Grulich  
Richard Moe Gustavsen  
Lucie Gérard  
Mikko Hallamaa  
Jøger Hansegård  
Inkamari Harjula  
Jani Heikkinen  
Moss Heim  
Jari Helaakoski  
Ulf Hermann  
Volker Hilsheimer  
Morteza Jamshidi  
Allan Sandfeld Jensen  
Teemu Jokitulppo  
Jonas Karlsson  
Friedemann Kleint  
Michal Klocek  
Sze Howe Koh  
Niko Korkala  
Fabian Kosmale  
Santhosh Kumar  
Jonas Kvinge  
Kai Köhne  
Cristian Le  
Inho Lee  
Frédéric Lefebvre  
Wladimir Leuschner  
Felix Lionardo  
Robert Löhning  
Thiago Macieira  
Leena Miettinen  
Thomas Moerschell  
Safiyyah Moosa  
Bartlomiej Moskal  
Marc Mutz  
Andy Nichols  
Mårten Nordheim  
Dennis Oberst  
Tinja Paavoseppä  
Jerome Pasion  
Karim Pinter  
Timur Pocheptsov  
Lauri Pohjanheimo  
Joni Poikelin  
Rami Potinkara  
Lorn Potter  
Dheerendra Purohit  
Liang Qi  
Matthias Rauter  
David Redondo  
Topi Reinio  
Shawn Rutledge  
Ahmad Samir  
Lars Schmertmann  
Luca Di Sera  
Sami Shalayel  
Tian Shilin  
Harald Sitter  
Nils Petter Skålerud  
Ivan Solovev  
Axel Spoerl  
Patrick Stewart  
Christian Strømme  
Audun Sutterud  
Lars Sutterud  
Tasuku Suzuki  
Jan Arve Sæther  
Morten Sørvig  
Esa Törmänen  
Tuomas Vaarala  
Sami Varanka  
Peter Varga  
Doris Verria  
Tor Arne Vestbø  
Juha Vuolle  
Olli Vuolteenaho  
Jaishree Vyas  
Michael Weghorn  
Edward Welbourne  
Paul Wicking  
Milian Wolff  
Oliver Wolff  
Shitong Xu  
Semih Yavuz  
Marianne Yrjänä  
Yifan Zhu  
Michał Łoś  
