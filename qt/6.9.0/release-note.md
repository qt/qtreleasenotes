Release note
============
Qt 6.9 introduces many new features and improvements as well as bugfixes
over the 6.8.x series. For more details, refer to the online
documentation included in this distribution. The documentation is also
available online:

https://doc.qt.io/qt-6/

The Qt version 6.9 series is binary compatible with the 6.8.x series.
Applications compiled for 6.8 will continue to run with 6.9.

Some of the changes listed in this file include issue tracking numbers
corresponding to tasks in the Qt Bug Tracker:

https://bugreports.qt.io/

Each of these identifiers can be entered in the bug tracker to obtain
more information about a particular change.

To make it easier to port to Qt 6, we have created a porting guide to
summarize the changes since Qt 5 and provide guidance to handle them. In
the guide, you can find links to articles about changes that may affect
your application and help you transition from Qt 5.15 to Qt 6:

https://doc.qt.io/qt-6/portingguide.html


Important Changes
-----------------

### Security fixes
* CVE-2025-30348 in qtbase
* CVE-2025-23050 in qtconnectivity
* CVE-2024-39936 in qtbase
* CVE-2025-3512 in qtbase

### qtbase
* 993b197d9c9 Entrypoint/Win32: just use __argc and __argv if available
Fixed a bug that caused Qt applications to disregard Unicode command-
lines on Windows even when argc and argv were passed un- modified to
QGuiApplication or QApplication. This happened only for builds with
Visual Studio and in the "windows" subsystem (not "console").

* b2eb4226991 qtypeinfo.h: move QTypeTraits part to qttypetraits.h
The qtypeinfo.h header no longer transitively includes <optional>,
<tuple> and <variant>.

* 6b096271cf0 QSqlRecord/QSqlQuery: Use QAnyStringView instead
QStringView
All functions taking a QString were changed to take a QAnyStringView.

* ffac33964d5 Add std::format support for qfloat16
Added std::format support for qfloat16. The supported formatting
options are similar to those of std::formatter for float.

* 23a83d6dcee Remove QNetworkRequestFactory TP marking
This class is no longer "under development and subject to change".

* 20b85ea8bfe Remove QRestAccessManager TP marking
This class is no longer "under development and subject to change".

* f39ce44c733 Remove QRestReply TP marking
This class is no longer "under development and subject to change".

* 648e3c730af [docs] Document QDBusObjectPath QDebug stream operator
Added QDebug stream operator.

* d6e1df3513c Add Qt::compareThreeWay() overloads for
Qt::totally_ordered_wrapper
Added Qt::compareThreeWay() overloads for Qt::totally_ordered_wrapper.
These overloads do the comparison using strict total ordering.

* b1ae4334ea1 Deprecate Qt::compareThreeWay() overload for pointers
Deprecate Qt::compareThreeWay() overload for pointers.

* c0d5c1b2fef Update public suffix list
Updated the public suffix list to upstream SHA
903a83ff7bfc3148e3692e09396f9f3bdc9462ef.

* 33387ed25f3 PCRE: upgrade to 10.44
PCRE2 was updated to version 10.44.

* b3edce58e5a QStringConverter: port encodingForName() to QAnyStringView
The encodingForName() function now takes QAnyStringView (was: const
char*).

* d4c4e6b876b QStringEn/Decoder: port (name, Flags) ctors to
QAnyStringView
The (name, flags) constructor now takes QAnyStringView (was: const
char*).

* b17703171cc QWidget: do not send hide events to hidden children
Widgets which are already hidden no longer receive hide events if
they're made hidden again (for instance because an ancestor gets
hidden).

* 0ed039fd134 QESDP: deprecate
QT_ENABLE_QEXPLICITLYSHAREDDATAPOINTER_STATICCAST
Support for QT_ENABLE_QEXPLICITLYSHAREDDATAPOINTER_STATICCAST has been
deprecated, and will get removed in a future version of Qt.

* d73a2bf0fb3 QThread: mark is(Main|Current)Thread() noexcept
Added isMainThread() static member function.

* 3a38de71da1 Windows: Remove legacy mouse handling
Legacy mouse handling has been removed. It is no longer possible to
enforce legacy mouse handling by passing "-nowmpointer".

* 5bbf4b40624 Remove QT_ENABLE_QEXPLICITLYSHAREDDATAPOINTER_STATICCAST
Support for QT_ENABLE_QEXPLICITLYSHAREDDATAPOINTER_STATICCAST has been
removed.

* d671e1af3b7 Determine Qt::AA_DontShowIconsInMenus default value based
on platform
The default value of Qt::AA_DontShowIconsInMenus is now determined
based on the platform. On macOS icons will not show by default. To
override, use QAction.iconVisibleInMenu for individual menu actions, or
set Qt::AA_DontShowIconsInMenus to false.

* 37a5e001277 CMake: Generate an SPDX v2.3 SBOM file for each built
repository
A new -sbom configure option can be used to generate and install a SPDX
SBOM (Software Bill of Materials) file for each built Qt repository.

* f39b39b8c72 Relax QHttpHeaders value field checks to allow UTF-8
Allows UTF-8 in header values now.

* 8ac57ff6bc7 QBitArray: fix read of uninitialized terminating null
Fixed a regression introduced in 6.7.0 that could cause QBitArray to
report wrong bit counts after a bitwise operation.

* 08c6de0c5d6 CMake: Add a way to use system/bundled 3rdparty libs in
bulk
Added the configure feature 'force-system-libs'. Enabling this feature
enables every 'system-foolib' feature, and the system-provided 3rdparty
library foo will be used. If the library is not found, an error is
yielded. Also added the analogous 'force-bundled-libs' feature that
enforces the usage of bundled 3rdparty libs.

* 2fbece8a73c PDF: add support for PDF/X-4
Support for PDF/X-4 has been added.

* e8fcdf9bb63 PDF: add a way to customize the output intent
New class.

* da2d3e914c1 Core: Move SipHash implementation into separate file
Adapted copyright information for the SipHash Algorithm (used in Qt
Core).

* 01d4be4a832 QThread/Unix: fix normal exit/terminate() race
On Unix, fixed a race of QThread::terminate() with normal thread exit
(running off the end of run()) which could corrupt QThread's internal
cleanup code. The fix involves disabling thread cancellation for the
remainder of the thread's lifetime once control reaches QThread's
cleanup code. If you rely on a PTHREAD_CANCELED return status, be aware
that this change may mask late cancellations. Likewise, slots connected
to QThread::finished() using Qt::DirectConnection are now run in a
regime where thread cancellation is already disabled. If you need
cancellation in that situation to work, you need to define your own
finished()-like signal and emit that at the end of run().

* efab6e69831 QtTest 3rdparty: update valgrind headers to v23.0
Updated QtTest's Valgrind headers to version 3.23.

* f79548e268a Update CLDR to v45, adding language Kuvi
Updated CLDR data, used by QLocale, to v45.

* 74ad4cbeef4 Change the mimetype database embedded into QtCore
For licensing reasons, QtCore no longer ships a copy of the MIME
database from freedesktop.org's shared-mime-info project, but the one
from the Apache Tika project. The tika definitions don't have icons or
translated descriptions, but are sufficient for matching file types.

* b12542c964c QMimeDatabase: pick up XML mimetypes from :/qt-
project.org/mime/packages
QMimeDatabase can now pick up XML mimetype definitions from :/qt-
project.org/mime/packages. GPL-compatible projects which provide self-
contained binaries can use this to provide a copy of freedesktop.org.xml
that will be used instead of the TIKA mimetypes.

* b294927a127 QDebug: add support for std::array
Can now output std::array

* 3ab18f40216 qcompilerdetection.h: Introduce Q_DECL_CONSTEXPR_DTOR
macro
Introduced Q_DECL_CONSTEXPR_DTOR which resolves to constexpr when
__cpp_constexpr >= 201907L, otherwise it resolves to inline.

* 7ccf30ae462 CMake: Add partial fixes for archiving dSYMs with an Xcode
project
CMake-generated Xcode projects will now include debugging symbols by
default, regardless of configuration type, and Release-like
configurations will default to using dSYM bundles instead of keeping the
debug symbols in object files, to match Xcode project defaults.

* 766d95edb3e Add Files field
Specify the source file that the "Mipmap generator for D3D12" component
consists of.

* 6e7c158152c Update benchlib's 3rdparty cycle counter to FFTW v3.3.10
QtTest's benchlib now uses FFTW v3.3.10's version of the clock-cycle
counter, Cycle.

* b8b7c584027 a11y: Add property for QWidget's accessible ID
Add an accessibleId property that allows to easily set a particular
accessible identifier for QWidgets that can be used by assistive
technologies to identify the widget.

* 7ffb4c16955 Remove GTK3 native menu
Due to deprecation of the gtk_menu_popup() function, we no longer use
GTK menus on Gnome: they are now rendered by Qt.

* 13244eef6c9 Fix signature of QDebug::toString() (again)
The toString() static function no longer allows the called operator<<()
to modify the argument. No Qt-provided operator<<() does that, and
operators that do are probably buggy.

* b57fac818b7 Long live QDebug::toBytes()!
Added ctor from QByteArray* and a static toBytes() function.

* c70fd79a178 XCB: set devicePixelRatio on backing store QImages
The images grabbed from a window (via e.g. QQuickWindow::grabWindow) on
XCB will now respect the window's devicePixelRatio.

* cb3faeba3d9 QArrayDataOps: fix FP equality comparison
Fixed a bug when two QLists holding NaN values were considered to be
equal.

* 2aa39be4c23 Add QDebug printing for the std/Qt::<name>_ordering types
Added possibility to print {std/Qt} weak/partial/strong_ordering values
with QDebug << operator.

* 02bf4d06b24 rhi: d3d11: Wait in beginFrame with a max latency of 2
The D3D11 backend creates swapchains from now on with
DXGI_SWAP_CHAIN_FLAG_FRAME_LATENCY_WAITABLE_OBJECT by default, with a
max frame latency of 2.

* 91cae3f9cc9 rhi: d3d12: Also default to max frame latency 2
The D3D12 backend creates swapchains from now on with
DXGI_SWAP_CHAIN_FLAG_FRAME_LATENCY_WAITABLE_OBJECT by default, with a
max frame latency of 2.

* d897e6a5f37 QAnyStringView: fix (char) ctor producing an invalid UTF-8
sequence
Fixed a bug where a QAnyStringView constructed from `char` would
produce an invalid UTF-8 sequence instead of a valid Latin-1 one, as
expected from the equivalent QChar constructor.

* 64416d3cf64 Add __attribute__((format(printf()))) to q(v)nprintf()
Added attributes for GCC-compatible compilers to detect format/argument
mismatches. If this throws warnings for your calls now, don't ignore
them. printf() format mistakes could be security-relevant. You may also
find that you relied on undocumented behavior, such as that certain
implementations (Windows, Android, WASM) of qsnprintf() support
char16_t* instead of wchar_t* for %ls. In that case, you should port to
qUtf16Printable() and QString::asprintf(), or suppress the warning and
port away from the platform dependence at your earliest convenience.

* bd7d54249e3 Introduce QT_NO_QSNPRINTF and mark QtCore as qsnprintf-
free
Added the QT_NO_QSNPRINTF macro to disable qsnprintf() and
qvsnprintf(), which will also be deprecated in 6.9. See the
documentation for details why we take this step.

* f3d29dfb89f CMake: Add new signature to qt6_wrap_cpp
A new target-based signature was added for qt_wrap_cpp. The usage of
the previous output-variable signature is deprecated and will issue a
warning.

* afd0bb28fba Deprecate q(v)snprintf()
As warned in advance in the 6.8 change-log, these functions have now
been deprecated with immediate effect. Due to an unfortunate fallback to
QString::asprintf().toLocal8Bit(), these functions introduce strictly
more platform dependencies than C++11's std::(v)snprintf(), which is the
suggested replacement.

* fe34ea9c88b QStringList: add filter(QLatin1StringMatcher) overload
Added filter(QLatin1StringMatcher) overload, which may be faster when
searching in large lists or lists with longer strings.

* 17d1d577c99 QFile: add supportsMoveToTrash()
Added supportsMoveToTrash() to check if Qt supports moving files to
trash in the current OS.

* 1b1ae345025 Long live Q_DECL_EQ_DELETE_X
Added the Q_DECL_EQ_DELETE_X macro.

* 7b707610629 QByteArray: add operator+(QByteArray, QByteArrayView)
Added operator+(const QByteArray &, QByteArrayView) overloads, so that
concatenation works without QStringBuilder too.

* 0774d5cc900 QString: add operator+(QString, QStringView) overloads
Added operator+(const QString&, QStringView) overloads, so that
concatenation continues to work even when QStringBuilder is disabled.

* 8fa8c574c04 qcompilerdetection.h: Introduce Q_CONSTEXPR_DTOR macro for
variables
Introduced Q_CONSTEXPR_DTOR for variables, which resolves to constexpr
when __cpp_constexpr >= 201907L, otherwise it resolves to const.

* bac583d0902 Long live Q_DISABLE_COPY(_MOVE)_X
Added the Q_DISABLE_COPY_X and Q_DISABLE_COPY_MOVE_X macros.

* d0bf0660b17 Update license rule to Unicode-3.0
UCD-generated data files now come under Unicode-3.0

* d39441a2eb5 Fix partial_ordering::unordered != 0 comparison
Fixed a bug where partial_ordering::unordered != 0 comparison produced
an incorrect result.

* 5a31800d412 QIdentityProxyModel: add setHandleSourceDataChanges(bool)
Added setHandleSourceDataChanges(bool) method to allow sub-classes to
indicate to QIdentityProxyModel that they will handle source model data
changes on their own. Also added a getter, isHandleSourceDataChanges().

* a2a315eaa28 Remove inline downscaling in png reader
The PNG handler no longer implements progressive downscaling during
decoding when scaled image reading is requested.

* dcc49d20a86 SQLite: Update SQLite to v3.46.1
Updated SQLite to v3.46.1

* 77a9a208227 Respect QTextDocument::defaultFont() in ODF writer
The ODF backend to QTextDocumentWriter will now respect the default
font set on the QTextDocument.

* 9bb2ab59786 Only define QT_SUPPORTS_INT128 if type_traits work for
them
Qt's support for 128-bit integers (qint128/quint128) is now conditional
on support for these types from the Standard Library, in particular
<type_traits> and <limits>. Qt no longer tries to work around missing
Standard Library support. As a consequence, e.g. GCC -ansi and GCC
-std=c++NN (instead of -std=gnu++NN, the default) builds will now no
longer support these types.

* 7c7b34f76a7 Update Freetype to 2.13.3
Updated bundled Freetype to version 2.13.3.

* f951c115860 Implement QTableModel::moveRows
Implemented moveRows in model. When sorting is enabled, setItem() now
moves the row to its sorted position, emitting rowsMoved rather than
layoutChanged.

* bb8cf72233e Decouple location and bluetooth permissions if API level
>= 31
ACCESS_FINE_LOCATION is no longer requested if API-level >= 31

* 521e091bca1 Convert a Qt ordering type to the weaker std ordering type
Added missing conversions from Qt ordering types to std ordering types.

* b5d8552f2ba Android: upgrade to Gradle 8.10 and AGP 8.5.2
Updated Gradle to 8.10 and AGP to 8.5.2.

* 221d8fdfb14 String Views: optimize the QByteArray/QString constructors
Creation of QLatin1StringView from QByteArray or QByteArrayView now
preserves the origin's isNull() status. This matches the behavior of
creating a QUtf8StringView from those types.

* a0a08285665 PDF: add support for the Author field
It is now possible to set the Author information for a PDF file.

* 9b70a895540 QTabBar: distinguish minimum from not-minimum size queries
from QStyle
QStyleOptionTab::MinimumSizeHint is added, allowing styles to
distinguish between queries for the minimum size vs the non-minimal size
of a tab.

* ecc13e3d41a QIcon::pixmap() add a note about the changed behavior
QIcon::pixmap() is fixed to no longer scale the size, passed to
QIconEngine::scaledPixmap(), by the devicePixelRatio.

* 0c010cd9c79 QDataStream: allow streaming of enums backed by long and
unsigned long
QDataStream now supports streaming enumerations whose underlying type
is long or unsigned long (like std::int64_t, std::uint64_t, ptrdiff_t,
size_t on 64-bit Unix platforms).

* dea91dbb505 Implement feature timezone_locale's CLDR half
The data extracted from the Unicode Consortium's Common Locale Data
Repository (CLDR) now includes, on platforms where this is otherwise
unavailable, data on how different locales name the world's various
time-zones.

* cc128d802c6 Add API to get variable axis information from font
Added API to get variable axis information for a font.

* 00ce45efe16 QSortFilterProxyModel: add a protected beginFilterChange
Added a new protected function beginFilterChange() that subclasses
overriding filterAcceptsRow or filterAcceptsColumn should call before
the filter parameter is changed. This makes sure that the signals
informing about rows or columns changing get correctly emitted.

* 8f68bd9e635 String Views: add slice() methods
Added slice() methods to
Q{String,ByteArray,Latin1String,Utf8String,AnyString}View which work
like sliced() but modify the view they are called on.

* 7fb3a182822 QNetworkRequest::transferTimeout: saturate int return
value
The transferTimeout() function now returns INT_MIN or INT_MAX when
transferTimeoutAsDuration().count() cannot be represented in an int.

* 6a3a28236c6 qFuzzy(Compare|IsNull)(): mark as noexcept
All qFuzzyCompare() and qFuzzyIsNull() overloads are now noexcept.

* 799e16149ce QStringTokenizer: clean up Q_STRINGTOKENIZER_USE_SENTINEL
The undocumented Q_STRINGTOKENIZER_USE_SENTINEL macro was removed. It
was unconditionally defined since Qt 6.0.

* 5774aa2560b Update tika-mimetypes.xml from upstream
Updated TIKA MIME types definition file to add the audio/aac and
application/x-java-keystore MIME types.

* e0d93ed4908 QStringTokenizer: remove unused op==(it, it)
The relational operators between QStringTokenizer::iterators have been
removed. Correct code didn't need them since Qt 6.0, when
QStringTokenizer::end() started returning ::sentinel instead of
::iterator unconditionally. You can still compare iterator and sentinel,
just not iterator and iterator.

* 4e911bda295 QTimer: make singleShot() have nanoseconds resolution
[1/2]: old-style
The singleShot() static methods now operate with nanoseconds
resolution, like QChronoTimer. The rest of QTimer remains milliseconds;
use QChronoTimer if you need a QTimer with nanoseconds resolution of
more than INT_MAX milliseconds range. Beware overflow that may occur
when passing large milliseconds objects that may overflow
nanoseconds::rep when converted.

* 2382bfb5b03 Add max_size() and maxSize() to view types
Added max_size() to all string-view types.

* f02402044e5 Pass QSslError::SslError by value
Made the QSslError::SslError QDebug operator<< a hidden friend of
QSslError. This means the operator is no longer a match for arguments
implicitly converting to SslError, only for SslError itself. A
backwards-compatible fix is to make the conversion explicit: debug <<
QSslError::SslError(arg).

* 29b98eabf07 QTimerEvent: port to Qt::TimerId
Added constructor taking a Qt::TimerId. Also added a getter for
Qt::TimerId.

* 751cbbd6b13 QBasicTimer: port to Qt::TimerId
Added id() method returning Qt::TimerId.

* 215c2d65b22 QBasicTimer: port to std::chrono::nanoseconds
Added start() overloads taking std::chrono::nanoseconds, and deprecated
the start() overloads taking chrono::milliseconds. This change is
backward compatible.

* 265187518d1 Update tika-mimetypes.xml from upstream
Updated TIKA MIME types definition file to add the audio/flac MIME type
as an alias for audio/x-flac MIME type.

* e95fb04202b QSharedPointer: optimize casts on rvalue shared pointers
Optimized casts on rvalue shared pointers.

* 9e3a96189d9 QHeaderView - Avoid memory usage until it is required
Introduced support for huge models by not using any memory per section
until a section has been hidden, moved or resized.

* 202dd3cb39a rhi: vulkan: Allow passing in wait/signal semaphores to
vkQueueSubmit/Present
Added support for specifying application-provided Vulkan semaphores to
wait and signal in queue submission and present calls. Relevant for
applications that integrate custom Vulkan rendering involving certain
forms of synchronization.

* c9ff625865c QUrl::toString: fix using of NormalizePathSegments and
RemoveFilename
Fixed a bug that caused QUrl::toString(), QUrl::toEncoded() and
QUrl::adjusted() to ignore QUrl::NormalizePathSegments if
QUrl::RemoveFilename was set.

* 0d83d8bbb15 Update to Harfbuzz 9.0.0
Updated Harfbuzz to 9.0.0.

* c76c888556d Introduce qt_add_android_permission CMake function
Added qt_add_android_permission function for setting Android
permissions from application CMake

* 69e6ae1670f QIODevice: Add QIODevice::readLineInto()
Added readLineInto() an alternative to readLine() that utilizes pre-
allocated memory.

* e2290b104fc moc & QMetaObject: move the QMetaMethod revision
information
With Qt 6.9, the layout of the meta object data table changed
incompatibly for classes containing meta methods (signals, slots) marked
with Q_REVISION. This is marked by the presence of revision 13 or later.
Code that reads or writes the meta object's raw data directly instead of
using QMetaMethod must detect the new layout.

* 3b9f5c82f52 QFileSystemEngine/Unix: implement getting the size of
block devices
For open block devices on Unix systems, size() now returns the size of
the underlying device. Previously, it would always return 0.

* ec894d69450 QDir: change qt_normalizePathSegments to preserve trailing
'/'s
Aligned how QDir and QUrl normalize paths with respect to preserving a
trailing slash. That is, QDir::cleanPath("/b/.") and
QUrl("file:///b/.).toString(QUrl::NormalizePathSegments) will return
"/b/" and "file:///b/" respectively. For more details see:
https://www.ietf.org/rfc/rfc3986.html#section-5.2.4

* 2effeb25c04 Long live 64-bit QFlags
Now supports 64-bit enumerations, with the same syntax, including
extraction into QMetaObject using the Q_FLAG and Q_DECLARE_FLAGS
markers. Note the QFlag helper class remains 32-bit wide. Creation of a
64-bit QFlags from a generic integer can be achieved by passing a
std::in_place first argument.

* 0db5b424cda Android: support uncompressed native libs within APKs
Add support for uncompressed native libraries within APKs.

* 069858008c8 QTestLib: increment timestamp by specified delay before
each event
QTest::mouseClick() and mouseDClick() now apply the given delay to the
timestamps of each event in the sequence, as it has been documented all
along. As before, the delay is never allowed to be less than 1 ms.

* b09fb51e7bb Windows: Use correct default font when
desktopSettingsAware is false
Fixed a regression where the default font on Windows would be larger
than before if desktopSettingsAware had been set to false.

* 247cd80abdd Windows: Fix memory leak in DirectWrite font database
Fixed a memory leak when repopulating the DirectWrite font database.

* 889bdf1de48 QTextOption: Add flag for showing default ignorable
characters
Added QTextOption::ShowDefaultIgnorables flag.

* 9ef4c123c39 QChar: disable implicit conversions on most ctor arguments
QChar constructors no longer perform implicit conversions. They only
accept the exact types listed in the documentation. A backwards-
compatible fix is to explicitly cast to one of the explicitly-supported
argument types.

* 06615a7cb87 QJniArray: add API to create an empty array and change
values
QJniArray now provides a mutable iterator and API to create an empty
Java array of a specified size, and to set individual values in the
array. QJniArray::reference is now an alias to a wrapper type that holds
a value.

* 9df6e8ad3b3 QProcess/Unix: add a flag to disable core dumps
Added UnixProcessFlag::DisableCoreDumps.

* 846b84ff305 QLatin1StringView: add toUtf8()
Added toUtf8(), which can convert without going through QString first.

* 6b598235b7b d3d: Drive window updates from a vblank watcher thread
By default, windows that get rendered to with QRhi using either the
D3D11 or D3D12 backend base their update request deliveries on
notifications from dedicated vblank waiting threads. This affects both
direct users of QWindow::requestUpdate() and also Qt Quick, since
QQuickWindow uses the same mechanism internally. This is expected to
provide smoother presentation, in particular a reduced display - mouse
cursor lag when dragging items in a Qt Quick scene for example, and
potentially reduced CPU load. Note that this is not applicable when
using an adapter such as WARP. For development and testing purposes, it
is possible to request the old behavior by setting the environment
variable QT_D3D_NO_VBLANK_THREAD to a non-zero value.

* a905d26f14d CMake:Android: add wrapper scripts to easily run apps
Add wrapper scripts to run Android apps and tests with ease from the
host.

* cc8a71e211f Update to Harfbuzz 10.0.1
Updated Harfbuzz to 10.0.1.

* c7691842f74 QDirIterator: don't crash with next() after hasNext()
returned false
Fixed a crash that happened if you called next() after hasNext() had
already returned false. Ideally you should never call next() without
first calling hasNext() as that could lead to unexpected results (for
example, infinite loops).

* 0b5874bc96f a11y: Add new BlockQuote role
Added new BlockQuote role that can be used to report quoted content as
such to assistive technology.

* 96c5e55c111 CMake: Change SBOM generation to be enabled by default
(mostly)
SBOM generation is now enabled by default, when building Qt, except for
developer builds and no-prefix builds. JSON SBOM generation is enabled
by default if the required Python dependencies are available.

* a9412bca7f9 macOS: Don't stop display-link once started and window is
exposed
Display-links are now kept running, even when windows are not
animating, as long as they are visible on screen. This improves the
responsiveness in fulfilling updateRequest with a corresponding
UpdateRequest event, which affects how fast a Qt Quick window can render
the result of a property change.

* 222891d0b6b QUuid: restore sorting order of Qt < 6.8
Fixed a regression that caused QUuid sorting order to change for some
UUIDs, compared to Qt 6.7 and earlier versions.

* 84afaafc9c6 Add truncated entries to QLocale::uiLanguages()
QLocale::uiLanguages() now includes, after the entries it previously
had (that accurately match what the relevant locale calls for, including
when it's a system locale reflecting user configuration), the fall-back
entries it may be reasonable to try if none of these is matched by a
suitable resource. The fall-backs are less-specific and result from
truncating the prior entries, omitting some trailing tags. Client code
that has been attempting to do such fallbacks for itself should instead
now just trust the list provided by uiLanguages().

* e7c8c2ccc85 macOS: Add support for context menu keyboard hotkey
The context menu keyboard hotkey available on macOS 15 is now
propagated as a QContextMenuEvent if the corresponding QKeyEvent is not
accepted.

* f430db18c97 SQLite: Update SQLite to v3.47.0
Updated SQLite to v3.47.0

* c1cb30f85b3 QDebug: normalize std::pair output separator
The output of a streamed std::pair has now a space after the separating
comma, like for other containers.

* b8c879f2735 QList: fix std::to_address(QList::iterator) on older
compilers
Fixed std::to_address() on QList::iterator on older compilers.

* 4fabde349f1 QThread/Unix: refactor to split QThreadPrivate::finish()
in two phases
Restored the Qt 6.7 timing of when the finished() signal is emitted
relative to the destruction of thread_local variables. Qt 6.8.0
contained a change that moved this signal to a later time on most Unix
systems, which has caused problems with the order in which those
variables were accessed. The destruction of the event dispatcher is kept
at this late stage, wherever possible.

* db8230715aa Freetype: Fix artificial oblique combined with other
transforms
Fixed an issue where artificially obliquened text would look incorrect
when other transformations were also applied and the Freetype backend
was in use.

* 32578a088db QHeaderView: update the view correctly in
resetDefaultSectionSize
Changing the defaultSectionSize no longer affects sections that don't
have the old default size.

* a5ddcbb76b6 Windows: Fix missing glyphs for very large font
Fixed an issue where glyphs might be missing for very large fonts.

* 4e4eef175bc moc: handle nested structs with meta content
Fixed a bug that caused moc to attempt to parse a nested struct (not
class) with meta keywords and this produced code that wouldn't compile.
Nested classes and structures are permitted, but must be defined outside
of the declaration of the outer class.

* 0576c2b7266 Make QSpan::isEmpty() constexpr
Fixed isEmpty() to be constexpr (empty() already was).

* 12b41c33326 QDebug: add streaming operators for std::tuple
Can now stream std::tuple.

* ad568b859a6 Revert "QTest: add -[no]throwon{fail,skip} command line
arguments"
The command-line options and environment variables that changed the
defaults for QTest::setThrowOn{Fail,Skip}() have been removed due to a
design flaw. To set the default, either place a call to the required
function in the test's initTestCase() function or define the C++ macro.

* fd75a66f3f6 Remove assert in QImageTextureGlyphCache::fillTexture()
Fixed possible assert when transforming bitmap fonts.

* 180f72d1002 Fix disappearing text with large bitmap fonts
Fixed an issue where text in bitmap fonts would disappear when scaled
up to very large sizes.

* b8500f3efc1 QString: toward UTF-8 arg() support [3/4]: add
Q{Any,Utf8}StringView::arg()
Added (multi-)arg() support a la QStringView/QLatin1StringView.

* d3eca687445 Deprecate Qt::MacWindowToolBarButtonHint
The Qt::MacWindowToolBarButtonHint flag has been deprecated, as it has
been a no-op since Qt 5.

* 454f010e58b Create a QCOMPARE_3WAY macro to test the C++20 spaceship
operator <=>
Added the QCOMPARE_3WAY macro. The macro tests the C++20 spaceship
operator <=>

* 6f25a583a6b CMake: Rework the module JSON files
The structure of the module JSON files, e.g. modules/Core.json has been
reworked. Consumers of these files need to be updated. A
'schema_version' key was added and set to 2 to ease reading different
versions of these files.

* 88cf9668009 Upgrade to Harfbuzz 10.1.0
Upgraded Harfbuzz to version 10.1.0.

* 36dca3c04f7 CMake: Add PURL and CPE info to 3rd party attribution
files
Added PURL and CPE information to the attribution files of 3rd party
sources.

* aa7d479be0d Introduce emoji-segmenter to 3rdparty code
Added the emoji-segmenter to third party code, for supporting complex
emoji sequences. This can be configured using the -emojisegmenter
option.

* 7b024cc1749 Don't count overflowing inline image height to previous
line
Fixed an issue which could cause the height of a word-wrapped text line
to grow if the immediate line after it began with an inline image.

* a9fe57fefaa QDebug: add streaming operators for std::unordered_map
Added support for std::unordered_map.

* 7ae959e00ae QCupsPrintEngine::setProperty(): defend against malformed
PPK_CupsOptions values
Fixed a bug where setting a value string-list with an odd number of
elements as the PPK_CupsOptions value would read uninitialized data.

* 18ec9c7b62f QSqlQueryModel: New method to re-execute the current query
Added refreshQuery() and refreshQuery(const QSqlDatabase &db) to
refresh the model data.

* a8c9a5617c7 QDebug: add streaming operators for std::unordered_set
Added support for std::unordered_set.

* 0c96528e8d4 QDebug: add streaming operators for std::set
Added support for std::set.

* 65fda988e92 QJson: Allow parsing any JSON value to QJsonValue
QJsonValue now follows RFC 8259 and is thus able to parse any JSON
value, not just arrays and objects. QJsonDocument remains at the level
of RFC 4627 in that only arrays and objects can be parsed.

* 850d4895be5 QDebug: add streaming operators for std::multiset
Added support for std::multiset.

* 51b584e6062 Windows: Fix arbitrary outline on emojis
Fixed an issue where emojis would sometimes get an outline.

* a0a9ec5674f SQLite: Update SQLite to v3.47.1
Updated SQLite to v3.47.1

* 80acbbc4571 Use and recognize en-POSIX as BCP47 name of the C locale
Changed the QLocale::bcp47Name() of the C locale to "en-POSIX" to
distinguish it from plain "en" (from which it differs materially). This
name is now also recognized as a name for the C locale.

* bc807073871 Fusion style: adjust sizeFromContents() for CT_PushButton
PM_ButtonMargin is now respected for QPushButton in fusion style.

* d14addfd451 CMake: Increase minimum required CMake version to 3.22
Building and using Qt now requires at least CMake version 3.22.

* 2ebca8cde1b Add widgetAdded signal for QStackedWidget and
QStackedLayout
The widgetAdded() signal emits whenever a widget is added or inserted
into QStackedWidget or QStackedLayout.

* e23dc7c4202 Correct handling of World in mapping MS's zone IDs to IANA
ones
Corrected handling of QLocale::World and clarified in docs how
QLocale::AnyTerritory is handled when QTimeZone selects zones by
territory.

* c39c3fe0cb1 QIODevice: Add overloads of QIODevice::readLineInto() that
takes QSpan
Added overloads of QIODevice::readLineInto() taking QSpan and returnig
a QByteArrayView.

* cbd2f56c141 QDockWidget: add Q_PROPERTY dockWidgetArea
Added dockLocation Q_PROPERTY with new dockLocation() and
setDockLocation() API.

* f401142d321 QIcon: document the support for icon fonts
QIcon can now generate icons from the named glyphs of an icon font.

* d9ad2251d9f Add QHash::tryEmplace/try_emplace
Added tryEmplace().

* 563ed822f86 QString: toward UTF-8 arg() support [3½/4]: port unary
arg() to QAnyStringView
The QString::arg() overloads have been redesigned. Character-like types
(char, char16_t, char8_t, wchar_t (still subject to QTBUG-126054 at the
time of writing), char32_t) now always output the character, not its
numeric value. In particular, char16_t and char arguments now match the
string-ish arg() overload (and therefore don't provide a `base` argument
anymore. A backwards-compatible fix is to cast char, char16_t, and
wchar_t arguments to uint. This also fixes the ambiguity errors you may
have seen when using a char16_t as `fillChar`.

* f7e8e54d7e6 QString: toward UTF-8 arg() support [4/4]: accept
QAnyStringViews (incl. UTF-8 ones)
Added (multi-)arg() support for UTF-8 (QUtf8StringView) and
QAnyStringView arguments. Passing C string literals or QByteArrays to
arg() now no longer implicitly converts to QString first.

* 3bed6f4e86e Introduce FFmpeg-related configure options
`-DFFMPEG_DIR=<dir>` and `-DQT_DEPLOY_FFMPEG=ON` can now be set via
`-ffmpeg-dir <dir>` and `-ffmpeg-deploy` respectively.

* b63e274a8a7 QSpan: add missing chopped()
Added chopped().

* 2d53ef6c6b3 Add QHash::tryInsert
Added tryInsert.

* 08c6cc62c74 QList: rework comparison operators
QList now implements operator<=>() in C++20 mode.

* 9cbfa8cb4c6 QVarLengthArray: rework comparison operators
QVarLengthArray now implements operator<=>() in C++20 mode.

* 7b009756035 QSpan: add missing slice() and chop()
Added slice() and chop(), being in-place versions of sliced() and
chopped(), resp.

* 387633a6069 QDomDocument::toByteArray() crashed in case of high XML
nesting level
QDomDocument::toByteArray() now iterates the nodes of the document
instead of recursing into subnodes. This avoids a stack-overflow crash
that used to arise with deeply-nested document structures.

* 056e78f456f Add iterator, begin() and end() for QDomNodeList
Added iterator support.

* f81fd7bd9f8 QHash: add insertOrAssign / insert_or_assign
Added insertOrAssign.

* d89cef439f5 QUuid: add support for creating UUID v7
Added support for creating UUID v7 as described in
https://datatracker.ietf.org/doc/html/rfc9562#name-uuid-version-7

* 901731ad780 Add primary RGB color points getter
Added primary points getter and setter

* 75cb14deb89 SQLite: Update SQLite to v3.47.2
Updated SQLite to v3.47.2

* f329dd4e16c QWidgetWindow: send QContextMenuEvent even after accepted
mouse press
If your QWidget subclass depends on receiving QContextMenuEvent, and
also handles mouse events directly, we recommend that you call ignore()
on unhandled mouse events (such as right-button events). In Qt 7, we
plan to stop sending QContextMenuEvent if the triggering mouse event is
accepted.

* 2dfc0cb6f6f QStringView: fix construction from arrays of unknown size
Made construction from arrays of unknown size compile. Such arrays will
use the const Char* constructor, determining the size of the array at
runtime.

* e076767bfd1 qstringfwd.h: don't include qglobal.h
The qstringfwd.h header no longer includes qglobal.h. A backwards-
compatible fix is to include qglobal.h yourself instead of relying on
the transitive include.

* 51bfc9da41f Q{Any,Utf8}StringView: fix construction from arrays of
unknown size
Made construction from arrays of unknown size compile. Such arrays will
use the const Char* constructor, determining the size of the array at
runtime.

* 94928669c12 QByteArrayView: add a ctor for arrays of unknown bounds
Made construction from arrays of unknown size compile. Such arrays will
use the const Byte* constructor, determining the size of the array at
runtime.

* aac98b795d0 QDebug: make std::optional stream operator SCARY
The std::optional streaming operator is now a member of QDebug, not a
free function. This breaks users that rely on the exact definition of
the operator (e.g. `operator<<(d, opt)`). A backwards-compatible fix is
to call the operator with infix notation (d << opt) only, and to avoid
const QDebug objects.

* 9834571282d CMake: Split off private module config packages
Private Qt modules have been split off into separate Qt6FooPrivate
CMake config packages. A call to find_package(Qt6Foo) will now
implicitly find_package(Qt6FooPrivate). It's not an error if
Qt6FooPrivate isn't available as it may be the case on certain Linux
distros that split their Qt module packages into private and public
parts.

* a994bc80fe6 Update bundled libjpeg-turbo to version 3.1.0
libjpeg-turbo was updated to version 3.1.0

* 55a46ec0058 QCommandLineParser: include the positional arguments'
sizes in --help
Made it so the positional argument descriptions are taken into account
in the aligning of text for helpText().

* fc29afbe1a2 QSqlDriver: return the connection name of the assoicated
QSqlDatabase
Added connectionName() which returns the connection name of the
associated QSqlDatabase instance.

* 7ab28855940 QSqlQueryModel: add new function to refresh the model data
Added refresh() to refresh the model data from the database.

* e2669499796 Apple: Use automatic rendering mode for icon engine
The Apple icon engine, used for theme icons on macOS and iOS, will now
use the default rendering mode for icons, typically monochrome, instead
of always using hierarchical icons.

* 09d44fdef3a QSaveFile: make it so flush() errors imply commit() failed
Fixed a bug that caused commit() to return true and overwrite its
intended target file even though it failed to flush buffered data to the
storage, which could cause data loss. This issue can be worked around by
calling flush() first and only calling commit() if that returns success.

* d39c4933902 3rdparty: patch BLAKE2 sources to not export anything in
static builds
Fixed a bug that caused the BLAKE2 symbols to be visible from QtCore in
a static build. If you need to use the BLAKE2 hashing algorithm in your
own code, either use QCryptographicHash or import libb2 into your build
environment. Using libb2 remains the recommended solution for all
systems, especially those for which it has optimized (vectorized)
implementations.

* 73b8c83ec72 Do not duplicate JsonFormat enum
The QJsonDocument header no longer includes QJsonValue. The backward-
compatible fix is to include all needed headers explicitly and to not
rely on the transitive includes.

* 77de3d45d3a Remove QT_NO_CAST_FROM_ASCII from
QT_ENABLE_STRICT_MODE_UP_TO
No longer includes QT_NO_CAST_FROM_ASCII. If you wish to continue using
QT_NO_CAST_FROM_ASCII, you need to define it in addition to
QT_ENABLE_STRICT_MODE_UP_TO. The reason for this change is that, while
everything else in strict mode should eventually become the default,
we're not proposing to remove the ability to construct a QString from a
const char*. QT_NO_CAST_FROM_BYTEARRAY and QT_NO_CAST_TO_ASCII remain
enabled in strict mode, though.

* 9413c19cc1f Update CLDR to v46
Updated CLDR data, used by QLocale, to v46.

* cddddd753c3 QSpan: don't detach Qt containers
No longer detaches implicitly-shared Qt containers converted to
QSpan<const T, N>. Note that std::span<const T, N> will, however, detach
such containers, so we recommend to use std::as_const() with implcitly-
shared Qt containers, as always.

* 37c389c7791 Implement COLRv0 support in Freetype engine
Added support for COLRv0 format color fonts.

* 11f94598dac Replace qdebug.h includes in public headers with forward-
declarations
Various Qt public headers don't include QDebug any more; if you need
QDebug's streaming you'll have to include it in your code.

* d5c3460b412 SQLite: Update SQLite to v3.48.0
Updated SQLite to v3.48.0

* c2e528ef425 Update Harfbuzz to version 10.2.0
Upgraded Harfbuzz to version 10.2.0.

* 9ed5d93c77f QtTest: Update valgrind (fatuously) to v3.24.0
Valgrind headers are up to date with Valgrind v3.24.0.

* faf10af206c Update public suffix list
Updated the public suffix list to upstream SHA
47264b57765919188b9f4144de8d95cf77e1b6dc.

* eac8f360808 Update CLDR to v46.1
Updated CLDR data, used by QLocale, to v46.1.

* e120fb78c94 CMake: Only load Qt6FooPrivate automatically when building
Qt
CMake packages of public Qt modules don't provide the targets of their
private counterparts anymore. User projects must now call
find_package(Qt6 COMPONENTS FooPrivate) to make use of the
Qt6::FooPrivate target. User projects that rely on the old behavior can
set the CMake variable QT_FIND_PRIVATE_MODULES to ON.

* 7782f2ad149 CMake: Don't enforce find_package(Qt6FooPrivate) for Qt
6.9
The requirement to do find_package(Qt6FooPrivate) in user projects was
postponed to a later Qt version.

* e60b493c2e5 Android: update to Gradle 8.12 and AGP 8.8.0
Updated Gradle to 8.12 and AGP to 8.8.0.

* 3e0276990de Make module ready for source SBOM checking
Renaming the license files with prefix LICENSE. to have them ignored by
reuse tool.

* 4bff9e35822 DirectWrite: Support embedded PNGs in color fonts
Added support for color font formats with embedded pixmaps in
DirectWrite backend.

* c4eacb70fde QFileSystemEngine/Darwin: remove use of clonefile() on
Apple systems
Fixed a bug on Apple systems that would cause copy() to copy a
directory if the QFile pointed to a directory and the destination was in
the same volume. Now copy()'s behavior is the same as in other OSes:
directories are never copied.

* 9df94123350 Update testlib's copy of Linux's perf_event_p.h header
The perf_event_p.h from Linux is updated to match Linux kernel 6.13.

* 605a20b2624 QSet: don't detach in remove()/removeIf() if nothing is
being removed
remove() and removeIf() no longer unconditionally detach, but only if
something is actually being removed.

* 7dca077bb6e QObjectData: Return const QMetaObject* from
dynamicMetaObject() already now
This (undocumented) class' dynamicMetaObject() function now returns a
const QMetaObject* (was: non-const). The backwards-compatible fix is to
receive the result in a const QMetaObject* variable (or to use auto),
and applying a manual const_cast, if a non-const object pointer was
actually required. Modifying the meta object that was returned by this
function was never supported and may lead to problems elsewhere.

* 97880102dc2 QSqlQuery: complete the deprecation/removal of its copies
Copying a QSqlQuery object via QMetaType now raises a runtime warning.
Note that copy operations for QSqlQuery objects have already been
deprecated since Qt 6.2, and are planned to be removed in Qt 7.

* 71979923413 Long live qstdlibdetection.h!
Added Q_STL_ macros for stdlib detection (libc++, libstdc++, MSSTL,
Dinkumware, STLport, SGI, RogueWave). If your STL is lacking, please
file a bug report. Note that these macros are not considered public API
just yet.

* 86597d28911 QUrl: set the host to empty but present for "file" URLs
Fixed a bug (regression from 6.7) where QUrl::resolved() could create
invalid URLs when the relative URI being resolved contained a path with
double slashes (e.g., combining "scheme:a" with "..//b.txt")

* 8c5736e68f9 QUrl: avoid going up from the drive path on Windows file
URLs
Fixed a bug (regression from 6.7) where resolving a base URL of an
absolute file path containing a Windows drive could result in said drive
being removed (e.g., resolving "file:///c:/" with "../" would result in
"file:///").

* 3dff1a3f7b2 Revert "Optimize QSet::unite"
Fixed a regression in unite() that caused equivalent elements of
`*this` to be overwritten by elements of `other` if `other.size()` was
larger than `this->size()`.

* eb13efc4a60 Unbreak QSet::intersect()
Fixed a regression (introduced for Qt 5.2) in intersect() that caused
equivalent elements of `*this` to be overwritten by elements of `other`
if `other.size()` was larger than `this->size()`.

* e5936267888 Improve hinted rendering quality on Windows
Improved hinted text rendering at font sizes larger than 16px.

* b2191e44501 SQLite: Update SQLite to v3.49.0
Updated SQLite to v3.49.0

* 01010851cb6 QProcess/Unix: don't close the childStartedPipe too soon
Fixed a bug that caused QProcess not to report start failures if the
UnixProcessFlag::CloseFileDescriptors flag was active.

* db1ed43050e QString: add {setUtf16,setUnicode}(const char16_t*)
overloads
Added setUtf16(const char16_t *) and setUnicode(const char16_t *)
overloads.

* 5985c90d37a Update UCD to Unicode 16.0.0
Updated the Unicode Character Database to UCD revision 34/Unicode 16.

* 9a634a5c4b7 QByteArray(View)::lastIndexOf: Guard against needle >
haystack
Fixed a bug in lastIndexOf() that could lead to out-of-bounds access
when the needle is longer than the haystack.

* edb8d08e468 QDesktopServices: don't use openDocument if the URL has a
query
Fixed a bug that caused QDesktopServices::openUrl() to discard a query
when opening a local file URL that contained a query but no fragment.

* ff7675817d9 qEnvironmentVariableIntValue: fix off-by-one with MSVC's
getenv_s
Fixed a bug that caused qEnvironmentVariableIntValue() to fail to parse
octal values from -020000000000 to -010000000000 with MSVC. Other
compilers were not affected.

* 0730c7ea55b Update PCRE2 to 10.45
PCRE2 was updated to version 10.45.

* c1bb08ab269 QVariant: don't use the static CanUseInternalSpace with
existing objects
Fixed a bug where QVariant could misbehave regarding types that changed
from non-relocatable to relocatable (or vice-versa) and not all uses of
it were recompiled. To benefit from this fix, applications must be
recompiled, but they will be safe going forward.

* e7562a50b98 Accept multiple fonts with the same family and style name
Fixed an issue with font families where only the last of multiple sub-
families sharing the same name would be registered.

* 6cefb8be965 QLocale: fix UB (signed overflow) in formattedDataSize()
Fix issue when calling formattedDataSize() with
numeric_limits<qint64>::min().

* 5518a384b2d SQLite: Update SQLite to v3.49.1
Updated SQLite to v3.49.1

* 5f3708e1901 Update bundled libpng to version 1.6.47
libpng was updated to version 1.6.47

* 926abdce783 Bundle Kitware's RunCMake test module
Add upstream cmake's RunCMake test infrastructure module to
src/testinternal/3rdparty/cmake to aid in creation of cmake auto-tests.

* 0777144b454 QColorDialogOptions: delete QSettings code and stop saving
globally
The class no longer automatically saves settings such as the custom
colors to a global QSettings("QtProject") shared by all applications and
no longer restores custom colors from there. Applications that wish to
retain the custom color settings should use customColors() and
setCustomColor() with their own settings files.

* 1a4e2e869f7 Update Harfbuzz to version 10.3.0
Upgraded Harfbuzz to version 10.3.0.

* ecc8ca605c3 Upgrade Harfbuzz to 10.4.0
Upgraded Harfbuzz to version 10.4.0.

* 457a8631546 3rdparty: update TinyCBOR to v0.6.1
The copy of TinyCBOR in Qt was updated to 0.6.1.

* 25986746947 QTextMarkdownImporter: Fix heap-buffer-overflow
Fixed a heap buffer overflow in QTextMarkdownImporter. The first marker
for Front Matter must begin at the first character of a Markdown
document, and both markers must be exactly ---\n or ---\r\n.

### qtsvg
* 425366a7 Add filter primitive "feBlend" to QtSVG
Added support for the "feBlend" filter primitive to QtSvg. The most
important but not all filter primitves are supported: feMerge,
feColorMatrix, feGaussianBlur, feOffset, feComposite, feFlood, feBlend.

* 0191fed2 Make module ready for source SBOM checking
Renamed certain license files outside of LICENSES with `LICENSE.`
prefix such that reuse will correctly ignore them.

### qtdeclarative
* 365cb95a75 Remove the Window.parent and Window.z properties
The Window.parent and Window.z properties added as tech preview in Qt
6.7 have been removed due to known failure scenarios that are still
being investigated. To embed a Window, use the explicit WindowContainer
item, which does not have any of the known issues.

* 92b919aff7 Warn about unset required properties on composite
singletons
Instantiating singletons with unset required properties will now fail
and print a warning instead of creating the singleton with the
properties unset.

* 74ec76d5ed qmllint: don't set error exit code if there are warnings
qmllint no longer exits with an error code if there are warnings by
default. Actual errors will still cause the exit code to be set.

* df684931c9 QJSEngine: Treat empty string literals as non-null, empty
QStrings
Assigning an empty JavaScript string to a property of type QString now
produces only an empty QString, not a null QString.

* cbc694491b Add Flickable.acceptedButtons property
Flickable.acceptedButtons has been added with default Qt.LeftButton;
set it to Qt.NoButton to disallow scrolling by dragging the mouse.

* 18c4bf827d Enable popup windows for QtQuick.Dialogs
All dialogs in QtQuick.Dialogs will now use popup windows, if able.

* b45629207e Material Style: update style theme when system theme is
changed
If the Material.theme is set to Material.System, the application theme
changes when the system theme is changed. This also works for the child
attached styles. If its theme is set to Material.System, regardless of
its attached parent style, it will follow the system theme changes.

* 51de3b6806 QQmlComponent: Reject nested properties in
setInitialProperties
The undocumented ability to set properties of subobjects when setting
initial properties will now fail.

* 862d229666 Fix rendering errors with Calibri Light and curve renderer
text
Fixed an issue where some fonts would exhibit artifacts when renderered
with the CurveRendering render type.

* aeabdb9388 QML: Type-check objects passed to QmlListWrapper
Assignments to list properties in QML are now type-checked. Before you
could, for example, insert a plain QObject into list<Item>, producing
undefined behavior. Now it instead inserts null and warns. In
particular, if you assign a JavaScript array of random objects to a list
property, QML will check each individual element, and insert null as
well as warn when encountering type incompatibilities.

* 6ae36202fd qmlcachegen: Reject using --only-bytecode with compiler-
only options
qmlcachegen will now exit with a failure state if --only-bytecode is
set as the same time as Script Compiler exclusive options. The only-
bytecode flag skips the compilation altogether. Remove one of the
conflicting flag to solve the issue.

* e40e9cbbf7 QQmlObjectModel: Mark elements when marking the object
model
ObjectModel will not let the garbage collector destroy any JavaScript-
owned objects it holds anymore. It now properly references them.
C++-owned objects still behave the same.

* fd1f8ea4e0 QQuickWidget: Assign focus to offscreen window when focus
chain wraps
The first/last item must be focused when QQuickWidget receives a focus-
in event due to tab/backtab reasons. In other cases, such as
ActiveWindowFocusReason, the item that was focused before will be
refocused.

* dfab766a8f Add a flickDeceleration property to Tumbler
Added flickDeceleration property.

* 1f618ee52a QQuickItem: Correct coordinate conversion to QPointF
The function mapToItem(item, real x, real y) now returns a point with
real values instead of rounding to an integer.

* 87b7a9b738 PointHandler: don't deactivate because of synth-mouse
events
If PointHandler is declared with acceptedButtons: Qt.NoButton it now
means that the PointHandler does not care which buttons are pressed or
not pressed: but it ignores synth-mouse events and responds only to
events that come from the appropriate kind of device. If specific
acceptedButtons are set, synthetic mouse-moves can deactivate it
temporarily.

* 14299fef5e Introduce FontMetrics.capitalHeight property
Added FontMetrics.capitalHeight property to match the
QFontMetricsF::capHeight() property.

* 92fe495d47 Re-enable Fbo mode in QQuickPaintedItem with OpenGL only
QQuickPaintedItem is made to behave identically to Qt 5 when the
application is rendering with OpenGL and the renderTarget property is
set to FramebufferObject or InvertedYFramebufferObject.

* fbc473d22a Close Dialog when a DestructiveRole button is clicked
Dialog is now closed when a button with the DestructiveRole is clicked.
Currently the only button with this role is Discard.

* 35630eef3d QtQml: Unify detaching behavior for all reference objects
Writing a list or value type to a QML-declared property now always
detaches this same list or value from any locals or other properties you
may have read it from. Therefore, subsequent changes to its "source"
will not affect it anymore. This is in line with what we do to
C++-declared properties.

* 0675615024 QQuickMenu: dissolve QQmlV4Function version of Menu::open
The undocumented behavior of resetting a menu's parent item when
explicitly passing undefined as the parent to Menu's open method has
been removed; instead, a type error is now thrown.

* 69254dfc91 CMake: Add a global QT_QML_NO_CACHEGEN cmake variable
A new QT_QML_NO_CACHEGEN cmake variable can be set to disable
compilation of qml files for all project qml files.

* c4455f1771 qmllint plugins: prefix settingsname with plugin name
Qmllint prefixes logging categories from plugins with the plugin name
in .qmllint.ini files. For example, PropertyChangesParsed=disable
becomes Quick.PropertyChangesParsed=disable.

* b772c53f52 Turn Qt::QuickEffects into a regular Qt module
QuickEffects is now an actual Qt module that you can findPackage()
without further gymnastics.

* 595abf24a2 QQmlComponent: Fix ordering of callbacks on
loadFromModule()
The QQmlParserStatus callbacks are invoked on objects loaded using
QQmlComponent::loadFromModule() at appropriate times now. You can rely
on any initial properties having been set before componentComplete() is
called and you can rely on the object having a valid QML context.

* 55c3b94035 Move DelegateChooser from Qt.labs.models to QtQml.Models
DelegateChooser has been moved from Qt.labs.models to QtQml.Models.

* 0edf656a2e Controls: Add TableViewDelegate
New delegate added: TableViewDelegate

* ebb30f71d0 Add textEdited() signal to TextEdit
Added textEdited() signal.

* 9a6d405cd6 Deprecate the dialogs in Qt.labs.platform
FileDialog, FontDialog, FolderDialog, MessageDialog and ColorDialog are
now deprecated. Use QtQuick.Dialogs instead.

* 3a050a7c65 Add Shear transform type
Added Shear transform types for shearing an item by a factor or angle
along the x- and y-axes.

* 2369543641 qmlls: fix compatibility issue due to removal of "p" flag
qmlls tool can take both -p and -d flag to pass documentation path.

* b9400f0aa6 Teach ApplicationWindow about safe area margins
The contentItem of ApplicationWindow is now automatically padded to
account for safe area margins. To override the automatic padding, set
the padding explicitly, via e.g. `topPadding: 0`.

* 383173616a Add ContextMenu
Added ContextMenu. ContextMenu can be attached to any item in order to
show a context menu upon a platform-specific event, such as a right
click or the context menu key.

* 7cbb3c18b9 QQmlPropertyMap: add an example of two argument constructor
Added a code snippet to explain the use of protected two argument
constructor of QQmlPropertyMap.

* 4ba99033bd IR Builder: Fix translation binding parsing
ListElement now supports disambiguation strings when QT_TR_NOOP is
used.

* 8340c55bbe FluentWinUI3: Move FocusFrame type to private impl module
FocusFrame.qml is deprecated in the module's public QML API and moved
to the private impl module instead.

* fe5bb33ed1 FluentWinUI3: Move StyleImage to private impl module
StyleImage.qml is deprecated in the module's public QML API and moved
to the private impl module instead.

* a280575919 Qml: Fix import order for certain name resolutions
When a type name is provided by two different imports, the type from
the last import takes precedence. This is now also the case when
resolving singletons, attached types, and types for as-casts. This
aligns with the behavior for regular type resolution.

* 4e9c8cb4b2 qmlformat: Error out when no input files are provided
qmlformat will now error out if no files are provided as positional
arguments or via the -F option.

* 2d354c85cb Overlay: ignore right button clicks
The pressed and released signals are no longer emitted for right
clicks. This is to allow ContextMenu to work when controls like Drawer
are used.

* 2561aedd99 Make module ready for source SBOM checking
Renaming the license files with prefix LICENSE. to have them ignored by
reuse tool.

* 27df31e579 CMake: Enable building Qt and user projects without support
for aotstats
It is now possible to control whether QML Compiler statistics
(aotstats) get generated by setting the QT_QML_GENERATE_AOTSTATS CMake
variable to ON or OFF. The default value is ON.

* dfcde3ea4d ContextMenu: add to text editing controls
TextField and TextArea now provide a ContextMenu by default. If you
already have a custom context menu for these types, ContextMenu will not
open its own on e.g. right click.

* 516b464c8e QQmlSA: Remove PassManager::{element|property}Passes() from
public API
PassManager will no longer expose the element and property passes that
it holds. They are only meant to be used inside the PassManager itself.
elementPasses() and propertyPasses() were removed.

### qtactiveqt
* d37e41f Make QAxBase/QAxWidget QDataStream operators hidden friends
The QDataStream operators are now hidden friends, so they will only
match types which are QAxBase, or derived from it, not those that merely
implicitly convert to them. A backwards-compatible fix is to make the
conversion explicit and only call these operators on actual QAxBase
subclass objects.

### qtmultimedia
* d79819e8b Update doc and attributions with new FFmpeg version in
Multimedia
Updated FFmpeg to n7.0.

* 217df8f83 Add pipewire screen capture on Wayland
Added screen capture function on Wayland via pipewire.

* 00558a91b Override the signal 'videoFrameChanged' in qml video sink
Removed QVideoFrame parameter from the not documented qml signal
VideoSink.videoFrameChanged.

* 24fb15e81 Update FFmpeg version in documentation
Updated FFmpeg to n7.0.1.

* 3e31ac9f0 Update FFmpeg version in documentation
Updated FFmpeg to n7.0.2.

* b8c581a06 GStreamer: increase the minimum required version to 1.20
Minimum required GStreamer version is raised to 1.20

* e829737e6 Don't add file extension when the filename already has an
extension
QMediaRecorder::setOutputLocation and QImageCapture::captureToFile will
no longer alter the suffix/extension if the provided path already
includes an extension, even if this extension does not align with the
recommended extensions for the MIME type.

* 03e32a342 Update FFmpeg version in documentation
Updated FFmpeg to n7.1.

* 643aa6dcd Make backend selection case insensitive
Backend selection using the QT_MEDIA_BACKEND environment variable is
now case insensitive.

* c28ff07a9 Disable HW textures conversion by default on native Windows
backend
HW texture conversion (zero copy texture transfer) is disabled by
default with the native Windows media backend. Set the
QT_DISABLE_HW_TEXTURES_CONVERSION environment variable to '0' to re-
enable it.

* 084a55aae QCamera: Change QML manualExposureTime property type to
float
QML binding for QCamera::manualExposureTime has changed from type int
to float.

* 2e3f558bd QCamera, docs: Update focusMode and focusDistance
documentation
focusDistance can now be applied without focusMode already being set to
FocusModeManual.

* 7b0434df8 Add qml property VideoOutput.mirrored
Add the qml property VideoOutput.mirrored. The property allows
mirroring the video stream according to the application's requirements.

* 0f7aa65ce Add qml property Video.mirrored
Add the qml property Video.mirrored.

* 960c48848 GStreamer - implement custom gstreamer bin
QMediaPlayer: GStreamer - support custom pipeline as source

* 2ef3f6939 Emit each individual settings signals from
QMediaRecorder::record()
Emit specific setting signal from QMediaRecorder::record() if a
corresponding setting changed.

* a80fd4a0a Add the endOfStreamPolicy property to VideoOutput
Added the qml property VideoOutput.endOfStreamPolicy allowing users to
keep the last frame at the end of the stream. Added the qml method
VideoOutput.clearOutput() allowing users to manually clear the last kept
frame.

* ffd7b0890 Add the endOfStreamPolicy property to the Video qml element
Added the qml property Video.endOfStreamPolicy allowing users to keep
the last frame at the end of the stream. Added the qml method
Video.clearOutput() allowing users to manually remove the last kept
frame.

* e3226852d Deprecate QMediaRecorder::encoderSettingsChanged() signal
from Qt 6.9
Deprecate QMediaRecorder::encoderSettingsChanged() because more
specific signals should be used instead.

* c76485c05 3p: import signalsmith-stretch library
Import timestretching library from Signalsmith Audio to use in the
media player.

* f69eb6622 Add REUSE.toml files and missing licenses
Add path to license files within LicenseFiles field.
qtattributionscanner looks for the files associated with licenses listed
in the licenseId fiel within the LICENSES directory. To prevent reuse
from erroring out, the license files only mentioned in
qt_attribution.json need to be moved out of the LICENSES directory. For
the qtattributionscanner to find those files, they need to be listed in
LicenseFiles field.

* 1ff4415d7 QAudioDevice: Make comparison only rely on id and mode
Comparison of QAudioDevice now only relies on .id() and .mode()
properties

* a04551ec1 Update pffft version to the latest version from upstream
Updated pffft to 02fe771.

* 3697a5cb4 Fix product name and ID for the pffft third party dependency
Update pffft product name and id.

* 9a6f30d85 Document where to find FFmpeg build scripts
Add link to where FFmpeg build scripts can be found.

* 98810b8f0 Remove security critical label from pffft and Eigen
dependencies
Removed security critical label from pffft and Eigen third party
dependencies.

### qttools
* 49d9fc926 qdoc: Allow custom sorting of generated group lists
\generatelist and \annotatedlist commands now support custom sort order
for the generated lists.

* f7e80349a qdoc: Require libclang >= 17
QDoc now requires LLVM 17 or newer.

* a6c76bac0 QtHelp API review: Make QHelpContentItem non copyable /
movable
The QHelpContentItem class is not longer copyable, because copying
results in double-deletion errors.

* 80480b06e CMake: Add TS_FILES_OUTPUT_VARIABLE argument to
qt_add_translations
Added the TS_FILES_OUTPUT_VARIABLE argument to qt_add_translations. Use
this to get the .ts files that have been automatically determined by
qt_add_translations.

* 34ce4eccb Change the shared Qt solutions headers to be proper private
headers
The headers of the shared Qt solutions have been renamed to be private
headers using the _p.h suffix.

* c87e631ce QtHelp API review: Make QHelpContentItem final
The QHelpContentItem class is now final (it lacks a virtual
destructor).

* d31d4735e QDoc: Allow author to specify `auto` as return type in `\fn`
command
QDoc now respects the author's intent better, in that it outputs `auto`
as the return type of functions that are documented with `auto` as their
return type.

* 435029af3 Qt Designer: Add qtVersion property to
QDesignerIntegrationInterface
QDesignerIntegrationInterface now has a qtVersion property, allowing
integrations to specify the Qt version they are targeting.

* 77a13c158 QDoc: Long live \cmakepackage, \cmakecomponent, and
\cmaketargetitem!
QDoc now supports adjusting the CMake requisites for third-party
projects

* d14eda472 Qt Designer: Change the default mode to docked for macOS,
too
Qt Designer now starts in docked mode by default on macOS, too.

* afa9c763b QDoc: Make the productname in \since command configurable
You can now configure the product name that's used with QDoc's `\since`
command with the new configuration variable `productname`. This
constitutes behavior change, as the command previously would inject
`Qt`.

* 4d59b4ca8 QDoc: Make example-related warnings configurable
Two new configuration variables have been introduced to QDoc to control
whether QDoc emits warnings about missing images or missing project
files, specific to example documentation. These warnings can now be
disabled by setting `examples.warnaboutmissingimages = false` and
`examples.warnaboutmissingprojectfiles = false` in the QDoc
configuration file(s).

* 63ee65d4e qdoc: Improve generation of versioned page titles
QDoc now uses the 'productname' configuration variable in the generated
.html &lt;title&gt; elements.

* 6e7a77330 CMake: Add a way to merge Qt translations at build time
qt_add_translations and qt_add_lrelease gained the
MERGE_QT_TRANSLATIONS argument for merging the Qt-provided translations
into the project's .qm files. Qt's translation catalogs are
automatically determined or may be passed explicitly via the newly
introduced QT_TRANSLATION_CATALOGS argument.

* d3cff9974 QDoc: Allow processing documentation comments in headers
QDoc can generate documentation from comments in header files. This
feature is provided as technology preview in this release. We appreciate
any feedback you may have!

* bdee3fb98 qdoc: QML Visitor: Handle namespaced imports
QDoc now resolves the correct QML base type imported under a namespace
ID.

* 156aec720 QDoc: Stop passing $CLANG_RESOURCE_DIR to Clang
QDoc no longer passes the contents of the `CLANG_RESOURCE_DIR`
environment variable as an include path when interfacing with Clang.

* 554277f21 QDoc: Write title attribute for images in HTML
QDoc can now generate a `title` attribute for your images. Set the
configuration variable `usealttextastitle = true` in your .qdocconf
file.

* efcf32f3c CMake: Add the QM_OUTPUT_DIRECTORY argument to
qt_add_lrelease
Added the QM_OUTPUT_DIRECTORY argument to qt_add_lrelease to specify
the directory where .qm files are generated. Using this argument is more
convenient than setting the OUTPUT_LOCATION source file property on
every corresponding .ts file.

* f6d4e8e17 CMake: Add QM_OUTPUT_DIRECTORY argument to
qt_add_translations
The qt_add_translations function gained the QM_OUTPUT_DIRECTORY
argument that can be used to specify the directory where .qm files are
generated.

* 89904d70b CMake: Add TS_OUTPUT_DIRECTORY argument to
qt_add_translations
For consistency with qt_add_translations' argument QM_OUTPUT_DIRECTORY,
we introduced the argument TS_OUTPUT_DIRECTORY to specify where
automatically generated .ts files are placed. The old argument name,
TS_FILE_DIR, is still available as alias to keep older project files
working.

* 022712768 Make module ready for source SBOM checking
Renaming the license files with prefix LICENSE. to have them ignored by
reuse tool.

### qtconnectivity
* fcee2074 sdpscanner: fix format strings for (u)int64_t
Fixed a bug involving broken serialization of SDP_(U)INT64 DTDs on Big-
Endian machines.

* dca2eb93 Check if location checks can be skipped with bluetooth scan
Android implementation now allows starting scan even if Location is
switched off and location permissions aren't granted. This requires that
API level is 31+ and that BLUETOOTH_SCAN asserts 'neverForLocation'.

* 8a2c5926 BlueZ: prefer powered on adapters when no address is
specified
If the local adapter address is not specified, the Linux backend now
tries to pick the first powered on adapter instead of simply picking the
first in the list.

### qtwayland
* 718ee85b Client: Split requests to set window and content geometry
The QWaylandShellSurface::setWindowGeometry() function is no longer
suitable for communicating the bounds of client side decorated content.
Custom shell implementations should use
QWaylandShellSurface::setContentGeometry() instead.

* 55e03d99 CMake: Move each wayland protocol into a separate
subdirectory
Split the single qtwayland 3rd party qt_attribution.json file into
multiple ones, per protocol, to ease maintenance.

* d362fc72 compositor: Implement drag and drop for touch events
Fixed an issue where drag operations could be initiated by touch
events, but it would not be possible to drop the contents.

* 8ad868df client: Implement xdg_system_bell_v1
New protocol synced from wayland-protocols

* aabc0f44 Implement support for attaching dbus menu bar to a window
Adds the implemented appmenu protocol

* ed1fd7f1 Client: implement toplevel icon protocol
New protocol synced from wayland-protocols

* f0acf489 Add support for wlr-data-control-unstable-v1 protocol
New protocol synced from wlroots.

* 8952cc71 protocol: update version info of wayland.xml in
qt_attribution.json
Update wayland.xml to 1.23.0.

### qt3d
* 01b416a07 Update imgui to latest version
Updated imgui to version 1.91.0

* 58df6033c Update assimp to 5.4.3
Update ASSIMP to v5.4.3

* 6533c6253 QRay3D: fix transform
Fix QRay3D::transform

### qtimageformats
* 8a9e941 Update bundled libtiff to version 4.7.0
Bundled libtiff was updated to version 4.7.0

* 99dfc51 Update bundled libwebp to version 1.5.0
Update bundled libwebp to version 1.5.0

### qtserialbus
* 553ed89c Fix virtual can backend usage in multithreaded environment
Fixed a race condition during creation of the VirtualCanServer when two
QCanBusDevices are instantiated in the same process in different threads

* a9e8ea7f Fix virtual can backend usage in multithreaded environment
Fixed a race condition during start of the VirtualCanServer in
multithreaded environment

* c6202b07 Doc: Fix nullptr access to QCanBusDevice in snippet
Fixed that the example snippet was wrongly operating on nullptr instead
a valid QCanBusDevice.

### qtserialport
* 9437a8a Windows use iManufacturer/iProduct for
manufacturer/description
Make Windows use USB iManufacturer for the returned Manufacturer in
QSerialPortInfo::availablePorts() and USB iProduct for the the returned
description also in availablePorts(). This makes Windows and Linux
report the same information for both fields.

* adb03af Linux: add an option to skip udev when enumerating serial
ports
Added the possibility to skip the libudev lookup by setting the
QT_SERIALPORT_SKIP_UDEV_LOOKUP environment variable. In such case, the
information from /sys/class/tty is used to enumerate the available
ports.

* 1dae292 Resurrect QSerialPort::restoreParametersOnClose property
Restored the QSerialPort::settingsRestoredOnClose property.

* 746a243 Windows: fix readyRead() signal emission
Fixed a bug where the readyRead() signal did not follow the QIODevice
docs and could be emitted recursively.

### qtwebengine
* 00d7de830 Add QWebEnginePermission and rewrite permissions API
Added new API for querying and modifying website permissions.

* 0cba9db58 Add PreferCSSMarginsForPrinting to QWebEngineSettings
New API added to QWebEngineSettings to optionally prefer CSS margin
rules over QPageLayout for printing results.

* 21ce22977 Make download API asynchronous
QWebEngineProfile::downloadRequested() is not limited to synchronous
usage anymore. QWebEngineDownloadRequest can be accepted or rejected
later without blocking the browsing session.

* 843d7f9b7 Add setting for JS touch events API
Added JSTouchEventsEnabled setting

* ecf3a7af6 Add QWebEngineUrlRequestInfo::isDownload()
Added isDownload() getter

### qtwebview
* b069ab8 macOS: Flip the switch and make the native back-end the
default
macOS will now use the native WebView backend by default, meaning
QtWebEngine is no longer required on macOS.

### qtspeech
* bb4d0b4 Remove the "macos" plugin
The "macos" engine plugin has been removed. The "darwin" engine has
been the default for supported Apple platforms and should be used
instead.

### qtnetworkauth
* 42732d7 Emit callbackDataReceived signal
Replyhandlers emit the callbackDataReceived() signal prior to parsing
the data, as documented.

* d867b77 Don't clear QAbstractOAuth2::scope upon empty server response
If the authorization server returns an empty 'scope' response, the
requested scope is not cleared anymore. Instead, it is assumed that the
requested 'scope' was granted.

* 571b717 Add QAbstractOAuth2::grantedScope and requestedScope
properties
Added new 'grantedScope' and 'requestedScope' properties to provide
clean separation between requested and granted scopes.

* 17333e7 Validate 'state' property when set
The 'state' property is checked for validity and setting a 'state' that
contains illegal characters will not be allowed.

* 62feb2e Add 'nonce' support for OAuth2
Added 'nonce' property and 'NonceMode' enum for using nonce in the
flows.

* 4209ced Add OIDC ID token acquisition convenience support
Added new 'idToken' property for accessing OIDC ID tokens

* 235f475 Add token request modification possibility
Added new function setter for modifying token network requests

* 5b2fca1 Add errorOccurred and deprecate error signal
The error signal is now deprecated and replaced by errorOccurred. This
will make the code handling errors clearer to write and read.

* 741fd2b Add https support to QOAuthHttpServerReplyHandler
Added support for https localhost server

* 97b0865 Remove 'state' parameter from extraTokens
received state parameter is no longer provided in extraTokens property.

* 164e2d8 Add Device Authorization Grant / Flow
Added new QOAuth2DeviceAuthorizationFlow class that implements support
for OAuth2 device authorization grant.

* ed5e676 Rename errorOccured signal to serverReportedErrorOccurred
The error signal is now deprecated and replaced by
serverReportedErrorOccurred.

* 58c92af Add access token expiration convenience functionality
Added new accessTokenAboutToExpire() signal, and autorefresh and
refreshThreshold properties.

* 08f3037 Fix and improve token request error reporting
Make a better distinction between NetworkErrors and ServerErrors with
token requests.

* b1e6744 Improve callback/redirect_uri hostname setting
Changed and clarified callback hostname handling (especially localhost
vs. 127.0.0.1)

* 6e08270 Add a method to manually define http callback hostname
Added new API for manually specifying the callback/redirect_uri
hostname

* 3807bb4 Change QAbstractOAuth2::expirationAt also when invalidated
Change expirationAt also if expires_in wasn't provided, or has invalid
value, and becomes invalid.

* 2034cfd Move tokenUrl property to QAbstractOAuth2
Added tokenUrl property that holds the token endpoint URL.

* 5933508 Deprecate QOAuth2AuthorizationCodeFlow::accessTokenUrl
property
Deprecated accessTokenUrl property and scheduled it for removal in Qt
7. Use QAbstractOAuth2::tokenUrl instead.

### qtremoteobjects
* aaeabff4 Expose (private) API for creating QtRO types
Add external/private interface to support bindings (specifically
Python) to generate dynamic classes from .rep files.

### qtquick3d
* 6b5c11725 Update Assimp to v5.4.2
Updated Assimp to v5.4.2

* 6fcd1b525 Update TinyEXR to v1.0.9
Updated TinyEXR to v1.0.9

* c9611c1e4 Update Assimp to v5.4.3
Updated Assimp to v5.4.3

* 0bd78ad6d Allow forcing mediump precision for floats in ES
frag.shaders
Added the option of forcing medium precision for floats in GLSL ES
fragment shaders. Provided mainly as a tool for performance tuning. Set
the environment variable QT_QUICK3D_MEDIUM_PRECISION to a non-zero
value. Has no effect on other kinds of shaders (and that includes non-ES
GLSL too).

* 50212fa8e Add 4K ultra shadow map resolution
Add 'Ultra' (4K) shadow map resolution.

* 8e96663a2 Change csmSplit1 default value
Default value of csmSplit1 is now 0.1.

* ba87ccc09 XR: Make multiview rendering the default
Multiview rendering is now enabled by default on platforms that
supports it.

* a9db04ced XR: Make the property multiViewRenderingEnabled read-only
The multiViewRenderingEnabled property is now read-only and toggeling
multiview rendering is no longer possible at run-time.

* 7c18923ee OrbitCameraController: Add automaticClipping
Add automaticClipping property

* 15032139d Reapply "Fix incorrect instancing model shadows"
Add shadowBoundsMinimum and shadowBoundsMaximum properties.

* 8738fd391 DebugView: Enable drawing of point light bounds
add drawPointLightShadowBoxes property

* fcce01e4b OpenXR: Update bundled version of OpenXR to 1.1.42
Update OpenXR to v1.1.42

* d12c49cba Add support for 32 bit shadowmaps
Add use32bitShadowmap property

* c8a7acb48 DirectionalLight: Add lockShadowmapTexels property
Add lockShadowmapTexels property

* cbc1cc8c9 Add Order Independent Transparency API
Add oitMethod property.

* 9feeb88f3 Add paths to the sub-project attributions for openxr
Added more specific paths to the sub-projects included with openxr.

* b776e8300 Make module ready for source SBOM checking
Renamed certain license files outside of LICENSES with `LICENSE.`
prefix such that reuse will correctly ignore them.

### qtshadertools
* fc91074 Update identifier and name for Khronos license
Change name of Khronos license to 'MIT Khronos - old variant', as it is
now called in SPDX: https://spdx.org/licenses/MIT-Khronos-old.html .

* 052ffb1 Allow requesting medium default float precision for GLSL ES
Added the ability for request medium precision for floats in the
generated GLSL ES fragment shaders.

* c586cb1 Update SPIRV-Cross
SPIRV-Cross was updated to match the bundled one in Vulkan SDK
1.4.304.0.

* e268295 Update to glslang 15.0.1
glslang was updated to 15.0.1.

### qt5compat
* 69a761a QTextCodec: use DefaultConversion too
Fixed a bug that caused QTextCodec not to write the Byte Order Mark for
UTF codecs. QTextCodec now has the same behavior as Qt 5.x.

* 92094c9 QStringRef: fix lost null-ness when converting to QStringView
Fixed a Qt 6 regression where conversion to QStringView would no longer
preserve nullness.

* 2df7508 QStringRef: preserve null-ness when converting to
QAnyStringView
Fixed missing conversion to QAnyStringView.

* 27edbd6 Make module ready for source SBOM checking
Renaming the license files with prefix LICENSE. to have them ignored by
reuse tool.

### qtopcua
* 247b3bae Fix race condition between backend shutdown and main thread
The connection property of OpcUaConnection now    takes ownership of the
QOpcUaClient as described in the docs

* 6342f6c8 Enable session locale ids update for the current connection
Updating session locale ids for the    current connection is now
supported.

* f8869459 Implement certificate authentication
The open62541 plugin now supports  certificate authentication.

* 9dbd9948 Add support for private key passwords
The open62541 plugin now supports  PEM encoded private keys with
password protection.

* d9d70191 Update OPC UA enums and add AccessLevelExBit
Qt OPC UA now supports the AccessLevelEx attribute

* 7fbda83d Disable the namespace 0 NodeId Q_NAMESPACE support with MSVC
Support for the meta object containing all the OPCUA namespace 0
NodeIDs (namespace QOpcUa::NodeIds) was disabled when using the
Microsoft Visual Studio C++ compiler, due to reaching compiler-imposed
limitations.

* 9ecc26fd Add node ids to qopcuaxmldatatypes2cpp and add CMake
integration
Qt OPC UA now exposes the CMake function
qt_opcua_generate_datatypes() to generate data types at build time.

* 2dc8599d Mark the QML API as deprecated
The QML API is now deprecated and will be  removed in a future version

* ee509565 Update bundled open62541 to v1.4.9
The bundled open62541 was updated to v1.4.9

### qtlanguageserver
* 1a9a75c JSON-RPC/QtLanguageServer: Enforce static builds
The (private) JsonRpc and LanguageServer modules are now always build
as static libraries.

### qtquick3dphysics
* ca61c4b Expose PxRigidDynamic::isSleeping() as QML API
Add isSleeping property

### qtgrpc
* 5b977693 Remove the QtProtobuf::repeatedValueCompare function
The QtProtobuf::repeatedValueCompare function was removed. Using op==
is a backwards-compatible fix.

* 61ccc3f8 Make the protobuf serializer registry private
Added QProtobufRepeatedIterator. QVariant that contain repeated or map
protobuf values can be converted to this class using QVariant::view
method.

* 271764cd Assert if QGrpcOperationContext::serializer returns null
QAbstractGrpcChannel implementations now are obliged to supply
QGrpcContext with the valid serializer. Any attempt to deserialize the
returned message with null serializer now will lead to assert or SEGV.

* e7ef620d Remove QGrpcOperation::deserializationError(String) methods
QGrpcOperation::deserializationError and
QGrpcOperation::deserializationErrorString methods are removed.

* 119add5f Make error handling in QAbstractProtobufSerializer generic
QAbstractProtobufSerializer::DeserializationError is renamed to
QAbstractProtobufSerializer::Error and now contains list of both
possible serialization and deserialization errors.

* a1b5a6dd Migrate to std::unique_ptr return value for all RPCs
All generated RPC methods now return std::unique_ptr instead of
std::shared_ptr. This change explicitly defines that caller takes the
ownership of the returned pointers.

* 7203da26 Avoid generating QList aliases for the protobuf messages
qtprotobufgen doesn't generate protobuf message QList aliases. All
usages of aliases should be replace by respective QList types. Aliases
are still generated and are guarded by the QT_USE_PROTOBUF_LIST_ALIASES
macro in the generated code. The macro is enabled by default and can be
disabled using QT_USE_PROTOBUF_LIST_ALIASES target property.

* a600e1c5 Add the early return from qt6_add_<protobuf|grpc>
The qt6_add_protobuf and qt6_add_grpc functions do not generate CMake
targets if provided in PROTO_FILES argument protobuf schemes do not
contain the corresponding for the generator definitions. qtprotobufgen
requires messages or enums, qtgrpcgen requires services. Functions now
make early return and warn about the missing definitions. Previosly the
functions generated unclear FATAL_ERROR. The
QT_SKIP_PROTOBUF_MISSING_DEFINITIONS_WARNING CMake variable suppresses
the warning.

### qtinterfaceframework (Commercial only)
* 1fa3a3a2 Update qface version in the license attribution
Update qface to 2.0.11


Fixes
-----

### qtbase
* [QTBUG-125380](https://bugreports.qt.io/browse/QTBUG-125380) Windows command line arguments mangled by double prime
character
* [QTBUG-125436](https://bugreports.qt.io/browse/QTBUG-125436) Windows ARM: HealthCheck fails - QtBase tst_QProcess
* [QTBUG-125958](https://bugreports.qt.io/browse/QTBUG-125958) Numpad 5 is not mapped to Qt::Key_Clear
* [QTBUG-126012](https://bugreports.qt.io/browse/QTBUG-126012) [patch] bindTextureImage: clearing GL error: 0x500
* [QTBUG-125513](https://bugreports.qt.io/browse/QTBUG-125513) crash when mixing QWidget style and styleSheet
* [QTBUG-126056](https://bugreports.qt.io/browse/QTBUG-126056) Camelcase forwarding headers missing in macOS/iOS builds
* [QTBUG-125858](https://bugreports.qt.io/browse/QTBUG-125858) REG: Wrong result value in QMessageBox::warning detected
in version 6.7.1
* [QTBUG-126084](https://bugreports.qt.io/browse/QTBUG-126084) QDockWidget unplugged from floating tab is in the wrong
position
* [QTBUG-125479](https://bugreports.qt.io/browse/QTBUG-125479) iOS - The cached device pixel ratio value was stale on
window expose
* [QTBUG-126107](https://bugreports.qt.io/browse/QTBUG-126107) tst_QStingConverter::invalidConverter() triggers
valgrind
* [QTBUG-126122](https://bugreports.qt.io/browse/QTBUG-126122) [Reg 6.6 -> 6.7] Window resizing on Android is broken
* [QTBUG-126052](https://bugreports.qt.io/browse/QTBUG-126052) submenu overlaps in qWdiget on iOS
* [QTBUG-126044](https://bugreports.qt.io/browse/QTBUG-126044) QMenu: Submenu partially hidden by main menu
* [QTBUG-125993](https://bugreports.qt.io/browse/QTBUG-125993) Double tap on touch screen not provoking
mouseDoubleClickEvent - patch included
* [QTBUG-126115](https://bugreports.qt.io/browse/QTBUG-126115) tst_qdbuscpp2xml doesn't appear to list qdbuscpp2xml as
a dependency
* [QTBUG-53974](https://bugreports.qt.io/browse/QTBUG-53974) QGraphicsScene always in inactive state if placed in a
QTabWidget
* [QTBUG-125410](https://bugreports.qt.io/browse/QTBUG-125410) TextField.inputMethodHints flags are ignored on Android
for Qt 6.7.0
* [QTBUG-126144](https://bugreports.qt.io/browse/QTBUG-126144) "configure -system-libb2" does not error if libb2 is
unavailable
* [QTBUG-121586](https://bugreports.qt.io/browse/QTBUG-121586) [Reg 5.15->6.x] QActionGroup signals missing from
documentation
* [QTBUG-125015](https://bugreports.qt.io/browse/QTBUG-125015) [REG] configure -c++std c++17 no longer works
* [QTBUG-59621](https://bugreports.qt.io/browse/QTBUG-59621) QIcon has increased memory usage because pixmaps are not
loaded on demand
* [QTBUG-124786](https://bugreports.qt.io/browse/QTBUG-124786) [Android] NullPointerException at
QtActivityDelegate.java:83
* [QTBUG-126221](https://bugreports.qt.io/browse/QTBUG-126221) B2Qt Application crashes
* [QTBUG-126265](https://bugreports.qt.io/browse/QTBUG-126265) uic: Code Injection to Potential Code Execution
* [QTBUG-124573](https://bugreports.qt.io/browse/QTBUG-124573) Windows Icon Engine: QIcon::pixmap() scales size by
devicePixelRatio twice, not once
* [QTBUG-126374](https://bugreports.qt.io/browse/QTBUG-126374) ABI break in 6.8 beta 1:
QPageLayout::setBottomMargin(double)
* [QTBUG-126386](https://bugreports.qt.io/browse/QTBUG-126386) qcompare.h build error on MSVC
* [QTBUG-126393](https://bugreports.qt.io/browse/QTBUG-126393) Can't build gallery example with qmake because it tries
to link to non-existent libqtesticonplugin.a
* [QTBUG-124829](https://bugreports.qt.io/browse/QTBUG-124829) The appearance of icons in QFileSystemModel is
simplified and differs from the typical Windows icons.
* [QTBUG-126343](https://bugreports.qt.io/browse/QTBUG-126343) QBitArray::count breaks after bitwise opererations
* [QTBUG-123018](https://bugreports.qt.io/browse/QTBUG-123018) Crash on closing an ios application
* [QTBUG-126388](https://bugreports.qt.io/browse/QTBUG-126388) [REG 6.8.0 -> 6.9.0] QTableView: Icons are incorrectly
scaled
* [QTBUG-126303](https://bugreports.qt.io/browse/QTBUG-126303) QWidget::createWindowContainer() managed window deleted
when new widget added due to QRhi
* [QTBUG-119076](https://bugreports.qt.io/browse/QTBUG-119076) Selecting multiple rows is sluggish if there are column
spans
* [QTBUG-126394](https://bugreports.qt.io/browse/QTBUG-126394) [Regression] Decreased performance in timerEvent
* [QTBUG-44643](https://bugreports.qt.io/browse/QTBUG-44643) QOCI: error accessing oracle ref_cursors
* [QTBUG-123886](https://bugreports.qt.io/browse/QTBUG-123886) [REG 6.5.2->6.5.3] QAbstractScrollArea::sizeHint does
not include the horizontal scrollbar's size
* [QTBUG-23470](https://bugreports.qt.io/browse/QTBUG-23470) QLibrary does not add 'lib' prefix if file name starts
with 'lib' (unix)
* [QTBUG-67692](https://bugreports.qt.io/browse/QTBUG-67692) Clash with Qt's internal logging categories when building
project with a static build of Qt
* [QTBUG-126349](https://bugreports.qt.io/browse/QTBUG-126349) Windows ARM: HealthCheck fails - QtBase tst_QFuture
* [QTBUG-124898](https://bugreports.qt.io/browse/QTBUG-124898) [Reg 6.2 -> 6.5] Qt.uiLanguage does not work for locale
changes
* [QTBUG-123298](https://bugreports.qt.io/browse/QTBUG-123298) Qt 6.5 on MacOS - In full screen, topmost QMenu action
doesn't fire
* [QTBUG-39403](https://bugreports.qt.io/browse/QTBUG-39403) QDesktopWidget::availableGeometry() returns wrong values
in Mac fullscreen mode
* [QTBUG-126381](https://bugreports.qt.io/browse/QTBUG-126381) qcssparser.cpp ASSERT: "d->parsed.metaType() ==
QMetaType::fromType<QList<QVariant>>()"
* [QTBUG-126214](https://bugreports.qt.io/browse/QTBUG-126214) QtCore: implicit instantiation of undefined template
'std::char_traits<unsigned char>' (libc++ 19 / musl libc / amd64)
* [QTBUG-122753](https://bugreports.qt.io/browse/QTBUG-122753) Qt Multimedia: implicit instantiation of undefined
template 'std::char_traits<unsigned char>' (libc++ 19 / musl libc /
amd64)
* [QTBUG-122778](https://bugreports.qt.io/browse/QTBUG-122778) QTreeView stylesheet does apply the border and the
background color to the branches
* [QTBUG-124481](https://bugreports.qt.io/browse/QTBUG-124481) KDE theme plugin always assumes single click activation
on KDE Plasma 6
* [QTBUG-126594](https://bugreports.qt.io/browse/QTBUG-126594) 6.7.2 qtbase: missing cups dependency in
Qt6PrintSupport.pc and Qt6PrintSupport cmake modules
* [QTBUG-89484](https://bugreports.qt.io/browse/QTBUG-89484) macdeployqt not deploying QSerialBus (canbus) plugins
* [QTBUG-126622](https://bugreports.qt.io/browse/QTBUG-126622) [iOS] Screen Reader focus gets stuck
* [QTBUG-126621](https://bugreports.qt.io/browse/QTBUG-126621) moveToTrash fails to remove a symlink to a directory
after trashing
* [QTBUG-126596](https://bugreports.qt.io/browse/QTBUG-126596) QListWidgetItem::setForeground() does not work
* [QTBUG-126543](https://bugreports.qt.io/browse/QTBUG-126543) windows11 style has QTableView ignoring
Qt::ForegroundRole
* [QTBUG-63485](https://bugreports.qt.io/browse/QTBUG-63485) Documentation for QStringList::replaceInStrings
* [QTBUG-56590](https://bugreports.qt.io/browse/QTBUG-56590) macdeployqt copying dSYM bundles
* [QTBUG-126502](https://bugreports.qt.io/browse/QTBUG-126502) Link broken on Qt Test Overview page in docs.qt.io
* [QTBUG-126678](https://bugreports.qt.io/browse/QTBUG-126678) CMake flag QT_USE_TARGET_ANDROID_BUILD_DIR does not work
with QT_ANDROID_BUILD_ALL_ABIS
* [QTBUG-33786](https://bugreports.qt.io/browse/QTBUG-33786) Orca reads model columns instead of rows when navigating
through items in QListView
* [QTBUG-125504](https://bugreports.qt.io/browse/QTBUG-125504) QDirListing includes '.' and '..'
* [QTBUG-27205](https://bugreports.qt.io/browse/QTBUG-27205) QFileSystemModel::filename() uses wrong role value for
call to data() method
* [QTBUG-126659](https://bugreports.qt.io/browse/QTBUG-126659) New QMap.qHash leading to ambiguous calls
* [QTBUG-126530](https://bugreports.qt.io/browse/QTBUG-126530) Qt app memory keeps growing with accessibility enabled
* [QTBUG-126348](https://bugreports.qt.io/browse/QTBUG-126348) QToolButton widgets have wrong background colors with
windows11 style and dark themes
* [QTBUG-126345](https://bugreports.qt.io/browse/QTBUG-126345) QHeaderView sorting indicator is missing with windows11
style and dark themes
* [QTBUG-68465](https://bugreports.qt.io/browse/QTBUG-68465) macOS: Accessibility: MenuItems are not accessible
* [QTBUG-126456](https://bugreports.qt.io/browse/QTBUG-126456) QWidgetWindow: Use of object after destruction
* [QTBUG-126503](https://bugreports.qt.io/browse/QTBUG-126503) No graphic change on Hover for QPushButton and
QToolbutton
* [QTBUG-125781](https://bugreports.qt.io/browse/QTBUG-125781) Cannot distinguish disabled or hovered buttons on
Windows 11
* [QTBUG-126043](https://bugreports.qt.io/browse/QTBUG-126043) macOS: Double clicking an appliaction in finder opens it
without the window becoming active
* [QTBUG-122755](https://bugreports.qt.io/browse/QTBUG-122755) Dragging text on HighDPI screen results in a warning
"QPixmap::scaled: Pixmap is a null pixmap"
* [QTBUG-123449](https://bugreports.qt.io/browse/QTBUG-123449) [Reg 6.4->6.5] Quick MenuItems do not appear greyed out
when disabled under GTK
* [QTBUG-126775](https://bugreports.qt.io/browse/QTBUG-126775) windeployqt does not provide MinGW's libraries
* [QTBUG-62970](https://bugreports.qt.io/browse/QTBUG-62970) tst_QComboBox::autoCompletionCaseSensitivity is flaky on
openSUSE 42.3
* [QTBUG-126773](https://bugreports.qt.io/browse/QTBUG-126773) iOS - library not found for -llibavformat
* [QTBUG-126845](https://bugreports.qt.io/browse/QTBUG-126845) QOpenGLWindow use after destruct
* [QTBUG-126575](https://bugreports.qt.io/browse/QTBUG-126575) QImage / QImageReader: lost QColorSpace during rotation
* [QTBUG-126335](https://bugreports.qt.io/browse/QTBUG-126335) QtQuick Window instances have blank title bars under
WebAssembly
* [QTBUG-126721](https://bugreports.qt.io/browse/QTBUG-126721) [REG 6.6->6.7] Overriden setVisible() no longer gets
called when parent widget is shown
* [QTBUG-126218](https://bugreports.qt.io/browse/QTBUG-126218) Preview is not generated when QPrintPreviewWidget is
shown
* [QTBUG-107139](https://bugreports.qt.io/browse/QTBUG-107139) Webassembly cannot input Chinese
* [QTBUG-124932](https://bugreports.qt.io/browse/QTBUG-124932) Incorrect keyboard functionality in a QML 3D scene on
the WebAssembly platform.
* [QTBUG-117096](https://bugreports.qt.io/browse/QTBUG-117096) Input fields (QWidgets and QML) don't register dead keys
accents when using a Linux desktop
* [QTBUG-126822](https://bugreports.qt.io/browse/QTBUG-126822) Windows accessibility crash/assert in Gallery example
* [QTBUG-126872](https://bugreports.qt.io/browse/QTBUG-126872) Double dash configure options with an equal sign broken
* [QTBUG-126391](https://bugreports.qt.io/browse/QTBUG-126391) tst_QDateTime::timeZones() fail on macOS 15
* [QTBUG-126390](https://bugreports.qt.io/browse/QTBUG-126390) ASSERT: "sameLocale(locale.d->m_data, monthly)"
* [QTBUG-127044](https://bugreports.qt.io/browse/QTBUG-127044) qmake reports wrong mkspec on Windows Arm64
* [QTBUG-127008](https://bugreports.qt.io/browse/QTBUG-127008) QThread::terminate() vs. normal exit race
* [QTBUG-112287](https://bugreports.qt.io/browse/QTBUG-112287) android: Input does not work with QQuickWidget
* [QTBUG-124564](https://bugreports.qt.io/browse/QTBUG-124564) Windows 11: Alternating row colors doesn't work in
windows11 style
* [QTBUG-126674](https://bugreports.qt.io/browse/QTBUG-126674) Inconsistent hashing between bool and integral overloads
* [QTBUG-89204](https://bugreports.qt.io/browse/QTBUG-89204) qtimageformats fails to configure during a static Windows
build with target global promotion failures
* [QTBUG-94356](https://bugreports.qt.io/browse/QTBUG-94356) fail to configure qt 6.1.1 on macos (with conan) due to
ZLIB global promotion not happening
* [QTBUG-95052](https://bugreports.qt.io/browse/QTBUG-95052) qtimageformats global promotion issues in static builds.
* [QTBUG-98807](https://bugreports.qt.io/browse/QTBUG-98807) build failure (with conan)when odbc and vulkan are
enabled (due to global promotion)
* [QTBUG-125371](https://bugreports.qt.io/browse/QTBUG-125371) Problematic calling of qt_find_package(Qt6) in
qt_internal_project_setup
* [QTBUG-52292](https://bugreports.qt.io/browse/QTBUG-52292) Pantheon desktop is not recognized as Gtk desktop
* [QTBUG-126533](https://bugreports.qt.io/browse/QTBUG-126533) Expand/collaps icon in QTreeView is not correctly scaled
when multi monitors have different scale settings
* [QTBUG-127112](https://bugreports.qt.io/browse/QTBUG-127112) QProgressBar with Windows 11 style is using far too much
cpu
* [QTBUG-127168](https://bugreports.qt.io/browse/QTBUG-127168) Memory Leak: Windows: Result of SetupDiGetClassDevs() is
not freed
* [QTBUG-126435](https://bugreports.qt.io/browse/QTBUG-126435) Document QT_NO_UTF8_SOURCE
* [QTBUG-126479](https://bugreports.qt.io/browse/QTBUG-126479) show()+showMaximized()+activating a layout de-maximizes
the window
* [QTBUG-104201](https://bugreports.qt.io/browse/QTBUG-104201) QWidget: resize() after showMaximized() causes strange
behaviour
* [QTBUG-127055](https://bugreports.qt.io/browse/QTBUG-127055) QThread::terminate() ABA problem
* [QTBUG-125589](https://bugreports.qt.io/browse/QTBUG-125589) weired console message with simple application
* [QTBUG-127129](https://bugreports.qt.io/browse/QTBUG-127129) Default column value misses database name in WHERE
* [QTBUG-122723](https://bugreports.qt.io/browse/QTBUG-122723) MySql and ODBC QSqlField.defaultValue() always get
invalid QVariant
* [QTBUG-127175](https://bugreports.qt.io/browse/QTBUG-127175) ibase driver returns stale error condition
* [QTBUG-125467](https://bugreports.qt.io/browse/QTBUG-125467) QIBASE can't connect to pre-Firebird 4 database
* [QTBUG-126151](https://bugreports.qt.io/browse/QTBUG-126151) QJniArray should not require contiguous containers as
input or output
* [QTBUG-124561](https://bugreports.qt.io/browse/QTBUG-124561) Qt.labs.platform context Menu appears out of the app
window on Gnome/wayland
* [QTBUG-126598](https://bugreports.qt.io/browse/QTBUG-126598) Qt.labs.platform Menu broken content positioning on
linux
* [QTBUG-127152](https://bugreports.qt.io/browse/QTBUG-127152) Document QDirListing::DirEntry
* [QTBUG-60674](https://bugreports.qt.io/browse/QTBUG-60674) QSqlRelationalTableModel - relation refresh crash
* [QTBUG-126541](https://bugreports.qt.io/browse/QTBUG-126541) Qt FTBFS on clang when C++20 is enabled
* [QTBUG-127414](https://bugreports.qt.io/browse/QTBUG-127414) Random configure/build error for android multiabi
* [QTBUG-127510](https://bugreports.qt.io/browse/QTBUG-127510) SCARY QDebug::toString() terrifies tests that compare
Microsoft::WRL::ComPtr
* [QTBUG-127507](https://bugreports.qt.io/browse/QTBUG-127507) "trivial-auto-var-init=pattern" causes crashes when
using MinGW
* [QTBUG-127473](https://bugreports.qt.io/browse/QTBUG-127473) [REG 5.15 -> 6] QList::op==() is broken for FP types
* [QTBUG-127616](https://bugreports.qt.io/browse/QTBUG-127616) examples/corelib/time/calendarbackendplugin fails to
build on msvc2022
* [QTBUG-125496](https://bugreports.qt.io/browse/QTBUG-125496) Apps continue running in the background.
* [QTBUG-126820](https://bugreports.qt.io/browse/QTBUG-126820) Move all QKeyCombination-returning operators into the
namespace Qt
* [QTBUG-125778](https://bugreports.qt.io/browse/QTBUG-125778) QMdiSubWindow does not refresh when the Maximize button
is hidden after being created.
* [QTBUG-127668](https://bugreports.qt.io/browse/QTBUG-127668) A standalone test can't be configure with a cross-
compiled Qt
* [QTBUG-125730](https://bugreports.qt.io/browse/QTBUG-125730) QAnyStringView('\xE4') creates an invalid UTF-8 string
(expected: valid L1)
* [QTBUG-127614](https://bugreports.qt.io/browse/QTBUG-127614) [macOS] [labs.platform] Menu stuck on opening when
standard icons are used
* [QTBUG-127551](https://bugreports.qt.io/browse/QTBUG-127551) [win] [labs.platform] Standard menu icons looks wrong on
DPR > 1
* [QTBUG-120396](https://bugreports.qt.io/browse/QTBUG-120396) `QUrl::resolved` gives wrong result when there are more
`..`s in relative reference
* [QTBUG-127641](https://bugreports.qt.io/browse/QTBUG-127641) QComboBox popup position changes after widget
reparenting
* [QTBUG-125149](https://bugreports.qt.io/browse/QTBUG-125149) Misplaced popup menu for reparented combo box
* [QTBUG-122747](https://bugreports.qt.io/browse/QTBUG-122747) Reparenting QTabWidget with a native window tab can
cause crash
* [QTBUG-127342](https://bugreports.qt.io/browse/QTBUG-127342) OCI plugin does not build for ARM
* [QTBUG-127512](https://bugreports.qt.io/browse/QTBUG-127512) tst_QTextLayout::softHyphens(16) failed on Ubuntu
24.04(both x64 and arm64) GNOME
* [QTBUG-127110](https://bugreports.qt.io/browse/QTBUG-127110) Platforms still use the inefficient qvsnprintf() fall-
back
* [QTBUG-126350](https://bugreports.qt.io/browse/QTBUG-126350) Windows ARM: HealthCheck fails - QtBase module_includes
* [QTBUG-126351](https://bugreports.qt.io/browse/QTBUG-126351) Windows ARM: HealthCheck fails - QtBase test_opengl_lib
* [QTBUG-127114](https://bugreports.qt.io/browse/QTBUG-127114) QPainter::drawText(QRectF, QString) has inconsistent
behavior when QRectF is null
* [QTBUG-127672](https://bugreports.qt.io/browse/QTBUG-127672) Consecutive stars in wildcardToRegularExpression cause
regex catastrophic backtracking
* [QTBUG-116083](https://bugreports.qt.io/browse/QTBUG-116083) Build failure related to fontdatabase / fontconfig
* [QTBUG-127799](https://bugreports.qt.io/browse/QTBUG-127799) repc: /home/qt/work/qt/qtremoteobjects_standalone_tests/
tests/auto/pods/rep_pods_replica.h: No such file.
* [QTBUG-127723](https://bugreports.qt.io/browse/QTBUG-127723) tst_QSvgRenderer::testFeFlood() failed on Ubuntu 24.04
X11 and offscreen
* [QTBUG-126415](https://bugreports.qt.io/browse/QTBUG-126415) Unknown CMake command "qt_internal_add_test" while
trying to open permissions manual test and selecting configuration
* [QTBUG-127104](https://bugreports.qt.io/browse/QTBUG-127104) Misplaced pushbuttons in QScrollBar
* [QTBUG-119753](https://bugreports.qt.io/browse/QTBUG-119753) QSqlRecord access causes hang/memory leak and crash
using QODBC driver
* [QTBUG-124173](https://bugreports.qt.io/browse/QTBUG-124173) QTreeView / QTableView dataChanged very slow when
topLeft and bottomRight span many items
* [QTBUG-127392](https://bugreports.qt.io/browse/QTBUG-127392) Avoid warning: Ignoring window icon xxx exceeds maximum
xcb request length 65535
* [QTBUG-127646](https://bugreports.qt.io/browse/QTBUG-127646) Windows ARM: HealthCheck fails - QtBase tst_qcolorspace
* [QTBUG-127759](https://bugreports.qt.io/browse/QTBUG-127759) Qt::partial_ordering::unordered implements op!=()
incorrectly
* [QTBUG-127781](https://bugreports.qt.io/browse/QTBUG-127781) Qt6::MockMultimediaPlugin is duplicated when building
qtmultimedia tests against pre-built qtmultimedia
* [QTBUG-127857](https://bugreports.qt.io/browse/QTBUG-127857) -skip-tests and -skip-examples are case sensitive
* [QTBUG-127403](https://bugreports.qt.io/browse/QTBUG-127403) Typo in QRhiTextureRenderTargetDescription
* [QTBUG-121855](https://bugreports.qt.io/browse/QTBUG-121855) missing RHI related headers (class documentation is
wrong)
* [QTBUG-125994](https://bugreports.qt.io/browse/QTBUG-125994) All RHI class documentations shows Qt6::Gui as the link
target for CMake
* [QTBUG-122774](https://bugreports.qt.io/browse/QTBUG-122774) "--no-qmltoolingsettingsInternal" gives error 'Unknown
option 'no-qmltoolingsettingsInternal''
* [QTBUG-124310](https://bugreports.qt.io/browse/QTBUG-124310) QT_DISTANCEFIELD_DEFAULT_BASEFONTSIZE=128 causes a
QDistanceField crash
* [QTBUG-127981](https://bugreports.qt.io/browse/QTBUG-127981) [cmake] stenciloutline name clash
* [QTBUG-127296](https://bugreports.qt.io/browse/QTBUG-127296) The return values of QMimeData::hasFormat() and
QMimeData::data() are inconsistent with the documentation.
* [QTBUG-124302](https://bugreports.qt.io/browse/QTBUG-124302) QOpenGLWindow Crashes on GPU-less Windows VM
* [QTBUG-126572](https://bugreports.qt.io/browse/QTBUG-126572) Default qt_generate_deploy_qml_app_script does not
deploy QtWebEngineProcess(d).exe to where it should be
* [QTBUG-121724](https://bugreports.qt.io/browse/QTBUG-121724) Image scaling produces an artifact around translucent
areas
* [QTBUG-127732](https://bugreports.qt.io/browse/QTBUG-127732) QT_WIN_DEBUG_CONSOLE breaks windeployqt in CMake install
* [QTBUG-128122](https://bugreports.qt.io/browse/QTBUG-128122) FAIL!  : declarative_positioning_core::PositionSource::t
est_bindPositionSourceProperties() Compared values are not the same
* [QTBUG-128137](https://bugreports.qt.io/browse/QTBUG-128137) qt-configure-module does not consider choosen
INSTALL_LIBEXECDIR
* [QTBUG-124570](https://bugreports.qt.io/browse/QTBUG-124570) Font is rendered differently in html and in ODT
* [QTBUG-126752](https://bugreports.qt.io/browse/QTBUG-126752) Calling popup() on QCompleter causes an abnormal
behavior of the Qt virtual keyboard.
* [QTBUG-119901](https://bugreports.qt.io/browse/QTBUG-119901) Basic <type_traits> not working for q*int128 in QtCore
TUs
* [QTBUG-127552](https://bugreports.qt.io/browse/QTBUG-127552) a11y: QFrame reports incorrect top-level role on Linux
(AT-SPI2)
* [QTBUG-126013](https://bugreports.qt.io/browse/QTBUG-126013) heap-use-after-free in from
QtPrivate::watchContinuationImpl
* [QTBUG-127880](https://bugreports.qt.io/browse/QTBUG-127880) Race condition in QFuture implementation
* [QTBUG-128102](https://bugreports.qt.io/browse/QTBUG-128102) Hash constructor with iterators does not work with
ranges::views
* [QTBUG-127549](https://bugreports.qt.io/browse/QTBUG-127549) QDomNode::save() takes huge amount of time. 10x worse
performance when compared to Qt 5
* [QTBUG-128199](https://bugreports.qt.io/browse/QTBUG-128199) [Reg 6.7.2->6.8.0b3] QByteArray::lastIndexOf fails to
find char
* [QTBUG-127926](https://bugreports.qt.io/browse/QTBUG-127926) Outdated Android docs still refer to
QtAndroid::androidActivity()
* [QTBUG-127288](https://bugreports.qt.io/browse/QTBUG-127288) Windows: MDI subwindow icons have low resolution and an
unattractive appearance when the window is displayed in maximized mode.
* [QTBUG-127381](https://bugreports.qt.io/browse/QTBUG-127381) Unexpected shift-selection in QTreeView.
* [QTBUG-128205](https://bugreports.qt.io/browse/QTBUG-128205) Qt documentation's offline.css defines weird background
for the print media type
* [QTBUG-124162](https://bugreports.qt.io/browse/QTBUG-124162) Qt Assistant Print Preview is not working
* [QTBUG-128254](https://bugreports.qt.io/browse/QTBUG-128254) Cannot build signed AAB with verbose deployment
* [QTBUG-109619](https://bugreports.qt.io/browse/QTBUG-109619) Enabling 2 extra Android CMake options leads to a build
error
* [QTBUG-122967](https://bugreports.qt.io/browse/QTBUG-122967) [macOS]Calling winId() renders additional undesired
pixmap if scaling factor is not 1
* [QTBUG-122751](https://bugreports.qt.io/browse/QTBUG-122751) Top flaky test: tst_qaccessibilitymac::treeViewTest on
MacOS_14 ARM64, MacOS_13, MacOS_12
* [QTBUG-127563](https://bugreports.qt.io/browse/QTBUG-127563) a11y: Window name reported to assistive technology
doesn't match what's displayed when app name is set
* [QTBUG-117417](https://bugreports.qt.io/browse/QTBUG-117417) Regression 5.15: Sharing Files w FileProvider fails
* [QTBUG-123752](https://bugreports.qt.io/browse/QTBUG-123752) Unexpected offset of fixed-height top-level window when
Windows Taskbar is on top
* [QTBUG-124733](https://bugreports.qt.io/browse/QTBUG-124733) Tool bar loose focus over mouse hovering
* [QTBUG-128298](https://bugreports.qt.io/browse/QTBUG-128298) QT_ANDROID_DEBUGGER_MAIN_THREAD_SLEEP_MS doesn't work
* [QTBUG-127670](https://bugreports.qt.io/browse/QTBUG-127670) Conversions from Qt::<name>_ ordering type to the weaker
std types are missing
* [QTBUG-121322](https://bugreports.qt.io/browse/QTBUG-121322) Cannot cross compile Qt for arm64 macOS on x86_64 macOS
* [QTBUG-128296](https://bugreports.qt.io/browse/QTBUG-128296) a11y: Missing NameChanged event when setting
windowModified property
* [QTBUG-128290](https://bugreports.qt.io/browse/QTBUG-128290) QT_THREAD_PARALLEL_FILLS macro causes
semaphore_wait_trap on iOS
* [QTBUG-125975](https://bugreports.qt.io/browse/QTBUG-125975)  QT_DISABLE_DEPRECATED_UP_TO 0x060400 gives link error
with static build
* [QTBUG-110841](https://bugreports.qt.io/browse/QTBUG-110841)  [REG: 5.10.1->5.11.0-alpha] Mouse events not observed
when Super (Windows) key is held down.
* [QTBUG-125756](https://bugreports.qt.io/browse/QTBUG-125756) Rename misleading variable QT_ANDROID_API_VERSION in
CMake and qmake
* [QTBUG-94956](https://bugreports.qt.io/browse/QTBUG-94956) "Invalid revision: zipalign" when building for android
* [QTBUG-124465](https://bugreports.qt.io/browse/QTBUG-124465) QDate::fromString very slow in 6.7.0
* [QTBUG-127788](https://bugreports.qt.io/browse/QTBUG-127788) QSlider's ticks are blurry when using Windows 11 style
* [QTBUG-128337](https://bugreports.qt.io/browse/QTBUG-128337) configure does not properly parse sql options
* [QTBUG-128325](https://bugreports.qt.io/browse/QTBUG-128325) tst_qbytearrayview test gives deprecated warnings at
compilation
* [QTBUG-86424](https://bugreports.qt.io/browse/QTBUG-86424) Can not use enum (class) as slot argument with underlying
type (unsigned) long, e.g. std::uint64_t
* [QTBUG-124252](https://bugreports.qt.io/browse/QTBUG-124252) Qt for WebAssembly multi-config generator support
* [QTBUG-115158](https://bugreports.qt.io/browse/QTBUG-115158) Time zone names and abbreviations are not localised
* [QTBUG-124118](https://bugreports.qt.io/browse/QTBUG-124118) QColorDialog on Windows 11: layout is broken
* [QTBUG-115717](https://bugreports.qt.io/browse/QTBUG-115717) QSortFilterProxyModel::invalidateFilter() sometimes does
not trigger a reevaluation of the model
* [QTBUG-127924](https://bugreports.qt.io/browse/QTBUG-127924) QFileDialog::selectNameFilter() does not work with the
filter returned by QFileDialog::selectedtNameFilter() of a previous
dialog
* [QTBUG-127987](https://bugreports.qt.io/browse/QTBUG-127987) Error copying directory: .syncqt_staging
* [QTBUG-127536](https://bugreports.qt.io/browse/QTBUG-127536) When styling a QComboBox, it always has a check-box icon
even after setting the icon to none.
* [QTBUG-84297](https://bugreports.qt.io/browse/QTBUG-84297) QTimeZone::NameType doesn't work as documentated
* [QTBUG-127090](https://bugreports.qt.io/browse/QTBUG-127090) In QTextEdit, switching the text color back to the
original color in dark mode with textColor() results in an incorrect
color being applied.
* [QTBUG-128391](https://bugreports.qt.io/browse/QTBUG-128391) QWidget inside a QMenu using QWidgetAction does not
always receive enterEvent and leaveEvent
* [QTBUG-128144](https://bugreports.qt.io/browse/QTBUG-128144) Complete addition of Qt::TimerId
* [QTBUG-125239](https://bugreports.qt.io/browse/QTBUG-125239) ERROR: AddressSanitizer: heap-use-after-free WRITE of
size 1 in tst_QGuiApplication::modalWindow()
* [QTBUG-128548](https://bugreports.qt.io/browse/QTBUG-128548) atal error: QRhiTexture: No such file or directory
* [QTBUG-128390](https://bugreports.qt.io/browse/QTBUG-128390) Crash on QWindowPrivate::updateDevicePixelRatio() with
nullptr access
* [QTBUG-128516](https://bugreports.qt.io/browse/QTBUG-128516) [macOS] Sporadic crash on
QCocoaScreen::deliverUpdateRequests()
* [QTBUG-123551](https://bugreports.qt.io/browse/QTBUG-123551) [Boot2Qt] A windows is blacked out in QQuickWidget
Example application
* [QTBUG-124235](https://bugreports.qt.io/browse/QTBUG-124235) Too small minimumSizeHint for QDateEdit/QDateTimeEdit
with windows11-style
* [QTBUG-118794](https://bugreports.qt.io/browse/QTBUG-118794) "The cached device pixel ratio value was stale on window
expose" when opening context menu on macOS with external display
* [QTBUG-120925](https://bugreports.qt.io/browse/QTBUG-120925) Right mouse click on QSpinBox makes Qt webassembly crash
* [QTBUG-128586](https://bugreports.qt.io/browse/QTBUG-128586) Signals without arguments give false warnings in QML in
Android
* [QTBUG-128678](https://bugreports.qt.io/browse/QTBUG-128678) Reintroduce support of iOS 16
* [QTBUG-128470](https://bugreports.qt.io/browse/QTBUG-128470) QHash heterogeneous lookup depends on C++20 concepts
* [QTBUG-128667](https://bugreports.qt.io/browse/QTBUG-128667) qdrawhelper crash rendering with ARM NEON
* [QTBUG-128675](https://bugreports.qt.io/browse/QTBUG-128675) q(u)int128 isn't supported with clang using MSVC's STL
* [QTBUG-128434](https://bugreports.qt.io/browse/QTBUG-128434) Master Details- Album added in the list is not
displayed.
* [QTBUG-32325](https://bugreports.qt.io/browse/QTBUG-32325) Qt5 Eats Your Memory
* [QTBUG-31215](https://bugreports.qt.io/browse/QTBUG-31215) QHeaderView/QVector memory management bug causes
unexpected out of memory exception
* [QTBUG-116042](https://bugreports.qt.io/browse/QTBUG-116042) configure fails when BUILDDIR path contains "++"
* [QTBUG-87982](https://bugreports.qt.io/browse/QTBUG-87982) Android INSERT_APP_NAME should be defined in project file
* [QTCREATORBUG-17863](https://bugreports.qt.io/browse/QTCREATORBUG-17863) Android: add variables for APP_NAME, APP_PACKAGE,
EXECUTION_TARGET
* [QTBUG-92013](https://bugreports.qt.io/browse/QTBUG-92013) Allow setting the Android icon from the project file
* [QTBUG-128648](https://bugreports.qt.io/browse/QTBUG-128648) Update Android Gradle plugin to 8.6.0
* [QTBUG-128364](https://bugreports.qt.io/browse/QTBUG-128364) Add CMake property to set androidCompileSdkVersion or
--android-platform used by androiddeployqt
* [QTBUG-127711](https://bugreports.qt.io/browse/QTBUG-127711) QUrl.adjusted doesn't work with QUrl::RemoveFilename |
QUrl::NormalizePathSegments
* [QTBUG-123219](https://bugreports.qt.io/browse/QTBUG-123219) android: Intents sent to the app while the screen is off
cause application to freeze for some time on wake up
* [QTBUG-127852](https://bugreports.qt.io/browse/QTBUG-127852) [REG: 5->6] Crash when using QSortFilterProxyModel if
the source model has a buddy() and does layout change
* [QTBUG-128742](https://bugreports.qt.io/browse/QTBUG-128742) QConcatenateTablesProxyModel does not react to
rowsAboutToBeMoved/rowsMoved
* [QTBUG-128800](https://bugreports.qt.io/browse/QTBUG-128800) QFileInfo::isSymLink() returns true with wrong path
* [QTBUG-128848](https://bugreports.qt.io/browse/QTBUG-128848) QTypeRevision::fromVersion fails ( in debug mode ), when
being fed with characters
* [QTBUG-113137](https://bugreports.qt.io/browse/QTBUG-113137) Performance problem about QItemSelectionModel
* [QTBUG-128929](https://bugreports.qt.io/browse/QTBUG-128929) Potential integer overflow in QNetworkReplyWasmImpl
* [QTBUG-128558](https://bugreports.qt.io/browse/QTBUG-128558) QTreeWidget creates new accessible QTreeWidgetItems each
time the child at index is retrieved
* [QTBUG-128903](https://bugreports.qt.io/browse/QTBUG-128903) [REG dev] QTableView: Hidden cells with headers
* [QTBUG-128499](https://bugreports.qt.io/browse/QTBUG-128499) Disabled components are not grayed in Light mode
* [QTBUG-128940](https://bugreports.qt.io/browse/QTBUG-128940) FAIL!  :
qmltestrunner::AnimatedImage::test_imageSource(local not found) Not all
expected messages were received
* [QTBUG-129128](https://bugreports.qt.io/browse/QTBUG-129128) QTableWidget: moving rows deletes rows
* [QTBUG-128906](https://bugreports.qt.io/browse/QTBUG-128906) Konsole crashes with SIGSEGV
* [QTBUG-120151](https://bugreports.qt.io/browse/QTBUG-120151) Two simultaneously opened onscreen keyboards could work
incorrectly
* [QTBUG-127701](https://bugreports.qt.io/browse/QTBUG-127701) ASSERT: "index >= 0 && index < m_adaptorModel.count()"
in file /home/...qqmltableinstancemodel.cpp, line 124
* [QTBUG-128517](https://bugreports.qt.io/browse/QTBUG-128517) [REG 6.6.3->6.7.2] Some cells in QTableViews do not show
text unless the cell is selected
* [QTBUG-126953](https://bugreports.qt.io/browse/QTBUG-126953) Wrong documentation for compression tag in a qrc file
* [QTBUG-128322](https://bugreports.qt.io/browse/QTBUG-128322) tst_qstringapisymmetry fails to GPU init and message
reject
* [QTBUG-129193](https://bugreports.qt.io/browse/QTBUG-129193) Qt compiled with gcc 13 and -march=bdver4/-mtune=bdver4
causes segfaults in tests, downstream applications
* [QTBUG-129258](https://bugreports.qt.io/browse/QTBUG-129258) Key and pointer events delivered to popups are synthetic
* [QTBUG-129147](https://bugreports.qt.io/browse/QTBUG-129147) [Windows] Crash on QRhiD3D::output6ForWindow() with
nullptr access
* [QTBUG-127767](https://bugreports.qt.io/browse/QTBUG-127767) QDir::mkpath("/") fails
* [QTBUG-129178](https://bugreports.qt.io/browse/QTBUG-129178) Broken layout on landing page (offline style)
* [QTBUG-129349](https://bugreports.qt.io/browse/QTBUG-129349) Re-enable tst_qhostinfo on macOS
* [QTBUG-129362](https://bugreports.qt.io/browse/QTBUG-129362) tst_QDockWidget::setFloating() failed on GNOME
Wayland(Ubuntu 24.04 and 22.04
* [QTBUG-129434](https://bugreports.qt.io/browse/QTBUG-129434) [[Regr: 6.7.2 -> 6.7.3]] QTranslator::load finds
languages in wrong order
* [QTBUG-36831](https://bugreports.qt.io/browse/QTBUG-36831) Drop indicator painted as single pixel when not shown
* [QTBUG-129375](https://bugreports.qt.io/browse/QTBUG-129375) [REG 6.5.1 -> 6.7.2|6.8.0-rc1] Common Trace Format (CTF)
backend causes application crash
* [QTBUG-129509](https://bugreports.qt.io/browse/QTBUG-129509) (Regression) Erratic scrolling behavior using the mouse
in 6.7.3
* [QTBUG-129514](https://bugreports.qt.io/browse/QTBUG-129514) Reversed mouse buttons don't work properly on 6.7.3
* [QTBUG-129335](https://bugreports.qt.io/browse/QTBUG-129335) DNS lookup on Apple platforms doesn't go through system
machinery
* [QTBUG-129201](https://bugreports.qt.io/browse/QTBUG-129201) tst_qwidget_window crashes on Android in nightly health
check
* [QTBUG-129213](https://bugreports.qt.io/browse/QTBUG-129213) Multipe log writings "QQnx: Failed to get screen for
window, errno=22" when starting Qt application
* [QTBUG-129358](https://bugreports.qt.io/browse/QTBUG-129358) Multi-abi build does not rebuild other targets when
there is a change
* [QTBUG-129299](https://bugreports.qt.io/browse/QTBUG-129299) [Widget] The view becomes black when docking back the
window in Hellp GL2 example
* [QTBUG-129436](https://bugreports.qt.io/browse/QTBUG-129436) Virtual keyboard example doesn't work on QNX800
* [QTBUG-129524](https://bugreports.qt.io/browse/QTBUG-129524) Android crash on Widget QMenu shortcut (when keyboard
open)
* [QTBUG-128359](https://bugreports.qt.io/browse/QTBUG-128359) Right-click menu logic error
* [QTBUG-111926](https://bugreports.qt.io/browse/QTBUG-111926) QFlags doesn't support large (>  sizeof(int)) enums
* [QTBUG-129290](https://bugreports.qt.io/browse/QTBUG-129290)          [REG 5.15->6.7.2] QTableView with stylesheet -
indicators overlap text
* [QTBUG-129689](https://bugreports.qt.io/browse/QTBUG-129689) QStorageInfo valid information not reset after path is
cleared on Linux
* [QTBUG-129386](https://bugreports.qt.io/browse/QTBUG-129386) QProgressBar Windows style has changed for the chunks.
* [QTBUG-129398](https://bugreports.qt.io/browse/QTBUG-129398) QButtonGroup::addButton() doesn't guarantee negative ids
(as promised in docs)
* [QTBUG-129399](https://bugreports.qt.io/browse/QTBUG-129399) Widgets gallery example color scheme does not work
* [QTBUG-127596](https://bugreports.qt.io/browse/QTBUG-127596) Application crash on opening in ~QBindingObserverPtr()
* [QTBUG-91262](https://bugreports.qt.io/browse/QTBUG-91262) Qpainter draws text with gray edge on qimage
* [QTBUG-129794](https://bugreports.qt.io/browse/QTBUG-129794) QTest::mouseClick() and mouseDClick() don't actually
apply the delay to each event in the sequence
* [QTBUG-127135](https://bugreports.qt.io/browse/QTBUG-127135) [Reg 6.5->6.7] Menu display problem Windows 11 dark
mode.
* [QTBUG-129085](https://bugreports.qt.io/browse/QTBUG-129085) Build on Solaris fails as -fstack-protector-strong is
used without -lssp
* [QTBUG-125474](https://bugreports.qt.io/browse/QTBUG-125474) windowsvista style: menus are broken
* [QTBUG-129545](https://bugreports.qt.io/browse/QTBUG-129545) tst_qgraphicswidget doesn't work on MacOS
* [QTBUG-129697](https://bugreports.qt.io/browse/QTBUG-129697) QT stopped understanding HTTP response compressed with
gzip.
* [QTBUG-129770](https://bugreports.qt.io/browse/QTBUG-129770) Android crash on Widget QMenu shortcut
* [QTBUG-124360](https://bugreports.qt.io/browse/QTBUG-124360) Android TV system keyboard no long opens on text fields
in 6.7
* [QTBUG-129405](https://bugreports.qt.io/browse/QTBUG-129405) Maximizing and restoring a window gradually moves it
downwards
* [QTBUG-129679](https://bugreports.qt.io/browse/QTBUG-129679) Windows 10: Maximized fixed-height window exceeds screen
to the right when task bar is left
* [QTCREATORBUG-31769](https://bugreports.qt.io/browse/QTCREATORBUG-31769) Passing 'settings set target.load-script-from-
symbol-file true' to lldb on macOS breaks debug dumpers when multiple
Creators are installed on the system
* [QTBUG-129832](https://bugreports.qt.io/browse/QTBUG-129832) Default font is way bigger in 6.8
* [QTBUG-129149](https://bugreports.qt.io/browse/QTBUG-129149) missing wasm ondragleave handler for drag and drop
* [QTBUG-129896](https://bugreports.qt.io/browse/QTBUG-129896) Qt 6.8.0 build with ICU enabled fails on Windows
* [QTBUG-44692](https://bugreports.qt.io/browse/QTBUG-44692) QWindowsCursor::mousePosition / QCursor::pos may return
garbage
* [QTBUG-129914](https://bugreports.qt.io/browse/QTBUG-129914) QPainter drawText(int x, int y, int width, int height,
...) doesn't work if width or height is zero
* [QTBUG-124496](https://bugreports.qt.io/browse/QTBUG-124496) QObject::timerEvent may be called before the timer
elapsed
* [QTBUG-129979](https://bugreports.qt.io/browse/QTBUG-129979) QGroupBox title looks enabled while group box is
disabled
* [QTBUG-129920](https://bugreports.qt.io/browse/QTBUG-129920) QMetaProperty::revision() always returns a fixed value
fixed number 0xFF00 + number
* [QTBUG-129471](https://bugreports.qt.io/browse/QTBUG-129471) [CMake] Unable to configure qtbase due to
$<LINK_ONLY:EXPAT::EXPAT>
* [QTBUG-129898](https://bugreports.qt.io/browse/QTBUG-129898) Pot. regression 6.7 -> 6.8 QThreadPool too many thread
IDs
* [QTBUG-129999](https://bugreports.qt.io/browse/QTBUG-129999) QTextTableCell::setFormat example code layout is broken
* [QTBUG-129234](https://bugreports.qt.io/browse/QTBUG-129234) tooltip only works once
* [QTBUG-129472](https://bugreports.qt.io/browse/QTBUG-129472) Regression: QMainWindow is invisible in Qt6.8beta for
iOS
* [QTBUG-129716](https://bugreports.qt.io/browse/QTBUG-129716) Submenu item not correctly aligned in rtl mode (gap to
main menu)
* [QTBUG-130119](https://bugreports.qt.io/browse/QTBUG-130119) configure with -disable-deprecated-up-to does not allow
5.15
* [QTBUG-127111](https://bugreports.qt.io/browse/QTBUG-127111) QRhi::nextResourceUpdateBatch() documentation error
* [QTBUG-129481](https://bugreports.qt.io/browse/QTBUG-129481) [Reg 6.8.0-beta4->6.8.0-rc][Reg 6.7.2->6.7.3] Build
break
* [QTBUG-103898](https://bugreports.qt.io/browse/QTBUG-103898) QListWidget::dropEvent processes already accepted events
* [QTBUG-130045](https://bugreports.qt.io/browse/QTBUG-130045) QTableView: there's a single pixel line between cells
where dropping is handled as if on viewport
* [QTBUG-129287](https://bugreports.qt.io/browse/QTBUG-129287) QDateTime fails to parse some dates
* [QTBUG-129504](https://bugreports.qt.io/browse/QTBUG-129504) Regenerate certificates for qsslserver auto-test
* [QTBUG-130109](https://bugreports.qt.io/browse/QTBUG-130109) Qt plugins not loaded through symlinks
* [QTBUG-129983](https://bugreports.qt.io/browse/QTBUG-129983) QSqlQuery Postgres and timestamp => QDateTime(Invalid)
* [QTBUG-130142](https://bugreports.qt.io/browse/QTBUG-130142) 6.8 Regresssion:  QDirIterator::next segfaults
* [QTBUG-128731](https://bugreports.qt.io/browse/QTBUG-128731) macOS: Crash when disconnecting screen when app is in
fullscreen
* [QTBUG-130133](https://bugreports.qt.io/browse/QTBUG-130133) ios QFileDialog crash
* [QTBUG-128870](https://bugreports.qt.io/browse/QTBUG-128870) Qt lacks an accessible role for block quotes
* [QTBUG-130294](https://bugreports.qt.io/browse/QTBUG-130294) FEATURE_cxx20 flag does not cause the code to be
compiled with C++20
* [QTBUG-130155](https://bugreports.qt.io/browse/QTBUG-130155) QUuid sorting order was changed in Qt 6.8.0
* [QTBUG-129596](https://bugreports.qt.io/browse/QTBUG-129596) Crash when closing inactive tab in tabbar for MDI window
* [QTBUG-130304](https://bugreports.qt.io/browse/QTBUG-130304) QDBusMessage::createMethodCall with a bad "service"
argument crashes in libdbus-1
* [QTBUG-128295](https://bugreports.qt.io/browse/QTBUG-128295) QTextImageHandler findAtNxFileOrResource() strips file:
scheme
* [QTBUG-125874](https://bugreports.qt.io/browse/QTBUG-125874) QTcpSocket readyRead not emitted for first received data
* [QTBUG-129330](https://bugreports.qt.io/browse/QTBUG-129330) Qt6 loads all imageformat plugins during startup
* [QTBUG-130288](https://bugreports.qt.io/browse/QTBUG-130288) QDoubleSpinBox layout still broken in Windows 11
* [QTBUG-128938](https://bugreports.qt.io/browse/QTBUG-128938) wasm: qtwasmserver.py does not work with python 3.12
* [QTBUG-129818](https://bugreports.qt.io/browse/QTBUG-129818) Organize the tutorials in Qt Widgets so they are visible
and reachable
* [PYSIDE-2897](https://bugreports.qt.io/browse/PYSIDE-2897) QCombobox Checkstates collide with text on Windows
* [PYSIDE-2906](https://bugreports.qt.io/browse/PYSIDE-2906) In Qt 6.7.x+ with the windows11 style, checkboxes and
items in a custom QComboBox overlap, breaking the UI. This issue is
absent in Qt 6.6.3 and earlier, suggesting a regression related to the
style changes introduced in newer Qt versions.
* [QTBUG-116511](https://bugreports.qt.io/browse/QTBUG-116511) Android 11 and above setNativeLocks failed: "Function
not implemented"
* [QTBUG-130125](https://bugreports.qt.io/browse/QTBUG-130125) Windows11 style padding for QComboBox
* [QTBUG-130123](https://bugreports.qt.io/browse/QTBUG-130123) Windows11 style same text color for
active/inactive/disabled widgets
* [QTBUG-130122](https://bugreports.qt.io/browse/QTBUG-130122) Windows11 style missing menu indicator for QPushButton
menu
* [QTBUG-127488](https://bugreports.qt.io/browse/QTBUG-127488) qtbase tests crashing on Android
* [QTBUG-130476](https://bugreports.qt.io/browse/QTBUG-130476) 6.8.0 openssl deployment
* [QTBUG-130002](https://bugreports.qt.io/browse/QTBUG-130002) The documentation of QIcon::State is wrong
* [QTBUG-129092](https://bugreports.qt.io/browse/QTBUG-129092) "OpenType support missing for..." Qt warnings
* [QTBUG-129113](https://bugreports.qt.io/browse/QTBUG-129113) VxWorks undefined references due to link line
* [QTBUG-83498](https://bugreports.qt.io/browse/QTBUG-83498) Fix handling of plugins in static builds (and the
dependency cycles it creates)
* [QTBUG-129704](https://bugreports.qt.io/browse/QTBUG-129704) Guard against potential NullPointerException for
QtActivityDelegate
* [QTBUG-130399](https://bugreports.qt.io/browse/QTBUG-130399) windows11 style: QTabWidget with QMenu as corner widget
* [QTBUG-130643](https://bugreports.qt.io/browse/QTBUG-130643) std::to_address doesn't work for QList::iterator
* [QTBUG-129927](https://bugreports.qt.io/browse/QTBUG-129927) [REG: 6.7 -> 6.8] Use after free in QTimeZone
* [QTBUG-129846](https://bugreports.qt.io/browse/QTBUG-129846) Quit in GUI application on linux in qt 6.8.0 does not
quit and process runs indefinitely
* [QTBUG-130341](https://bugreports.qt.io/browse/QTBUG-130341) Crash during QNetworkAccessManager destruction
* [QTBUG-117996](https://bugreports.qt.io/browse/QTBUG-117996) [REG 6.2 -> 6.5] QBasicTimer::stop: Failed. Possibly
trying to stop from a different thread
* [QTBUG-130621](https://bugreports.qt.io/browse/QTBUG-130621) tst_QPromise incorrectly disabled tests
* [QTBUG-129696](https://bugreports.qt.io/browse/QTBUG-129696) Crash in QCalendarBackend::dateTimeToString when
timezone is invalid
* [QTBUG-128488](https://bugreports.qt.io/browse/QTBUG-128488) QPainterPath some time gives incorrect value
* [QTBUG-129028](https://bugreports.qt.io/browse/QTBUG-129028) [Windows] Non-native QFileDialog behaves strangely when
creating a folder with a trailing space
* [QTBUG-130309](https://bugreports.qt.io/browse/QTBUG-130309) QSortFilterProxyModel invalidate is slow when there's a
large number of persistent indicies
* [QTBUG-130565](https://bugreports.qt.io/browse/QTBUG-130565) QString::slice uses the wrong snippet
* [QTBUG-97436](https://bugreports.qt.io/browse/QTBUG-97436) Italic rotated text on Linux renders incorrectly
* [QTBUG-86104](https://bugreports.qt.io/browse/QTBUG-86104) [evdev] The first event coordinates are incorrect when
absolute coordinates used for mouse handling.
* [QTBUG-108015](https://bugreports.qt.io/browse/QTBUG-108015) [CMake] [MSVC2022] TEST_separate_debug_info always fail
* [QTBUG-129095](https://bugreports.qt.io/browse/QTBUG-129095) [REG Qt 6.3.2 -> 6.4.0] Default button is not triggered
when widget in a sub-layout has focus
* [QTBUG-13404](https://bugreports.qt.io/browse/QTBUG-13404) QMenu does not take into account the width of separators
with text
* [QTBUG-130056](https://bugreports.qt.io/browse/QTBUG-130056) Fail to link after qt_add_translations added to
CMakeLists.txt
* [QTBUG-128912](https://bugreports.qt.io/browse/QTBUG-128912) QTreeView Header splitter cursor is not shown with
QGraphicsProxyWidget
* [QTBUG-128484](https://bugreports.qt.io/browse/QTBUG-128484) HTTP cache:  max-age value is ignored by must-revalidate
* [QTBUG-130720](https://bugreports.qt.io/browse/QTBUG-130720) Typo on enum QStyle::StyleHint
* [QTBUG-130717](https://bugreports.qt.io/browse/QTBUG-130717) file INSTALL cannot find
"/home/qt/work/qt/qttools_build/target/bin/pixeltool.wasm"
* [QTBUG-130704](https://bugreports.qt.io/browse/QTBUG-130704) [Regr:6.3.2->6.8.0] QMenu text alignment missing when
mixing actions with and without icons
* [QTBUG-128478](https://bugreports.qt.io/browse/QTBUG-128478) tst_qcompleter crashes on Linux, mostly on RHEL
* [QTBUG-129582](https://bugreports.qt.io/browse/QTBUG-129582) QComboBox with null view crashing application
* [QTBUG-116013](https://bugreports.qt.io/browse/QTBUG-116013) QHeaderView::resetDefaultSectionSize doesn't invalidate
cached size hints / update view
* [QTBUG-128913](https://bugreports.qt.io/browse/QTBUG-128913) QGraphicsItem::ItemIgnoresTransformations leads to show
popup at far off position
* [QTBUG-130642](https://bugreports.qt.io/browse/QTBUG-130642) Incorrect QAbstractSpinBox size hint in Windows 11 style
when style sheet is set
* [QTBUG-126671](https://bugreports.qt.io/browse/QTBUG-126671) NativeRendering renders nothing on Windows on ARM in
VMWare Fusion on Mac
* [QTBUG-130498](https://bugreports.qt.io/browse/QTBUG-130498) Q_ENUM for sub classes does not work
* [QTBUG-128781](https://bugreports.qt.io/browse/QTBUG-128781) Setting flat button background colors does not work
correctly on Win11
* [QTBUG-128518](https://bugreports.qt.io/browse/QTBUG-128518) [REG 6.6.3->6.7.2] Vertical scrollbar can appear
unpainted until window is resized
* [QTBUG-130739](https://bugreports.qt.io/browse/QTBUG-130739) tst_QImageIOHandler tests fail CI on VxWorks
* [QTBUG-128302](https://bugreports.qt.io/browse/QTBUG-128302) [macOS] Closing window while modal dialog is open
crashes the application
* [QTBUG-114873](https://bugreports.qt.io/browse/QTBUG-114873) Rendering is broken when moving window between monitors
with OpenGL on macOS
* [QTBUG-130824](https://bugreports.qt.io/browse/QTBUG-130824) Windows11 style: wrong size hint for (editable)
QComboBox
* [QTBUG-11967](https://bugreports.qt.io/browse/QTBUG-11967) QDateEdit/CalendarPopup(true) has incorrect sizing
* [QTBUG-130586](https://bugreports.qt.io/browse/QTBUG-130586) [Reg] The font "Terminus" is not rendered
* [QTBUG-129946](https://bugreports.qt.io/browse/QTBUG-129946)  Android QtQuickApp Not Work with Qt 6.8.0 ARM64-v8a
* [QTBUG-129512](https://bugreports.qt.io/browse/QTBUG-129512) [Boot2Qt] QMenu does not reappear after closing in
widgets app
* [QTBUG-130737](https://bugreports.qt.io/browse/QTBUG-130737) tst_QDir::mkdirWithPermissions fails on CI with VxWorks
* [QTBUG-129981](https://bugreports.qt.io/browse/QTBUG-129981) quiview.mm uses deprecated QPointingDevice method,
breaking 6.8 compilation from Src on iOS
* [QTBUG-130138](https://bugreports.qt.io/browse/QTBUG-130138) Context Menu does not open on right click outside of
opened context menu
* [QTBUG-123632](https://bugreports.qt.io/browse/QTBUG-123632) Regression: Setting background-color style of
QTreeView::item breaks alternatingRowColors
* [QTBUG-128405](https://bugreports.qt.io/browse/QTBUG-128405) Unavoidable race condition when using
QPromise::setException()?
* [QTBUG-130843](https://bugreports.qt.io/browse/QTBUG-130843) a11y: Qt sends AT-SPI signals with wrong DBus signature
* [QTBUG-129791](https://bugreports.qt.io/browse/QTBUG-129791) Issue with Showmaximized function in case of QMainWindow
with Qt::FramelessWindowHint flag
* [QTBUG-130865](https://bugreports.qt.io/browse/QTBUG-130865) [Windows] QWidget::showMaximized() does not follow
SPI_SETWORKAREA correctly when Qt::FramelessWindowHint is set
* [QTBUG-130828](https://bugreports.qt.io/browse/QTBUG-130828) windows11 style: radio buttons painted incorrectly
inside scroll area
* [QTBUG-77939](https://bugreports.qt.io/browse/QTBUG-77939) QDoubleSpinBox dot(.) decimal separator disappears for
values >= 1000
* [QTBUG-128916](https://bugreports.qt.io/browse/QTBUG-128916) QComboBox drop down is not visible on Windows11 in some
situation
* [QTBUG-128329](https://bugreports.qt.io/browse/QTBUG-128329) qt combobox 放入到QGraphicsProxyWidget下拉框不显示
* [QTBUG-116554](https://bugreports.qt.io/browse/QTBUG-116554) [macOS] Crash on QCocoaDrag::maybeDragMultipleItems()
* [QTBUG-130916](https://bugreports.qt.io/browse/QTBUG-130916) QCheckBox documentation mentions non-exising accessors
* [QTBUG-115451](https://bugreports.qt.io/browse/QTBUG-115451) QSpinBox, QComboBox visual Clipping / incorrect Size
Hint
* [QTBUG-111796](https://bugreports.qt.io/browse/QTBUG-111796) Qt Font Scaling for bitmap fonts is broken in Wayland
* [QTBUG-130930](https://bugreports.qt.io/browse/QTBUG-130930) Freetype: Assert when rotating drawing bitmap font with
rotated painter
* [QTBUG-130977](https://bugreports.qt.io/browse/QTBUG-130977) Freetype: Scaling bitmap fonts can cause missing glyphs
* [QTBUG-131009](https://bugreports.qt.io/browse/QTBUG-131009) FAIL!  : tst_focus::navigation(tab-all-controls)
Received a warning that resulted in a failure
* [QTBUG-130973](https://bugreports.qt.io/browse/QTBUG-130973) [iOS] Native image picker dialog freezes when asking for
permission
* [QTBUG-131001](https://bugreports.qt.io/browse/QTBUG-131001) QWidget::childAt returns empty children
* [QTBUG-129684](https://bugreports.qt.io/browse/QTBUG-129684) Potential crash when calling QInputDialogue::getText()
* [QTBUG-131093](https://bugreports.qt.io/browse/QTBUG-131093) [REG 6.5.3 - 6.7.3] [macOS] Global scale factor has no
effect on platform's window size anymore
* [QTBUG-130832](https://bugreports.qt.io/browse/QTBUG-130832) [REG 6.8.0 -> dev] Windows System Tray Icon: Context
menu's incorrect position
* [QTBUG-126698](https://bugreports.qt.io/browse/QTBUG-126698) [REG 5->6] QDateEdit defaults to 20th century
* [QTBUG-129570](https://bugreports.qt.io/browse/QTBUG-129570) moc can no longer create meta objects for private
classes (that aren't Q_OBJECT themselves)
* [QTBUG-129108](https://bugreports.qt.io/browse/QTBUG-129108) Menus and action visibility
* [QTBUG-130895](https://bugreports.qt.io/browse/QTBUG-130895) Living QThread after termination
* [QTBUG-129302](https://bugreports.qt.io/browse/QTBUG-129302) AndroidDeployQt does not seems to work with cmake
generator expression
* [QTBUG-131253](https://bugreports.qt.io/browse/QTBUG-131253) onDataChanged callback of QtAbstractItemModel fails on
tests
* [QTBUG-131127](https://bugreports.qt.io/browse/QTBUG-131127) QLocale: Assert in QLocale::uiLanguages() on wasm
* [QTBUG-129996](https://bugreports.qt.io/browse/QTBUG-129996) modules/Core.json target information incomplete for
macOS universal builds
* [QTBUG-130811](https://bugreports.qt.io/browse/QTBUG-130811) XCB: Async operations between XCB and X11 cause
flakiness in QXcbScreen::topLevelAt()
* [QTBUG-84258](https://bugreports.qt.io/browse/QTBUG-84258) tst_Gestures::graphicsItemGesture fails
* [QTBUG-69648](https://bugreports.qt.io/browse/QTBUG-69648) tst_Gestures::graphicsItemTreeGesture fails on Ubuntu
18.04.
* [QTBUG-67393](https://bugreports.qt.io/browse/QTBUG-67393) tst_Gestures::explicitGraphicsObjectTarget fails on
Ubuntu 17.10.
* [QTBUG-67392](https://bugreports.qt.io/browse/QTBUG-67392) tst_Gestures::graphicsItemTreeGesture fails on Ubuntu
17.10.
* [QTBUG-67389](https://bugreports.qt.io/browse/QTBUG-67389) tst_Gestures::graphicsView fails on Ubuntu 17.10.
* [QTBUG-68861](https://bugreports.qt.io/browse/QTBUG-68861) tst_Gestures::graphicsItemGesture autotest fails on
Ubuntu 18.04
* [QTBUG-70224](https://bugreports.qt.io/browse/QTBUG-70224) tst_Gestures::testReuseCanceledGestures autotest fails on
Ubuntu 18.04 & SLES 15
* [QTBUG-70223](https://bugreports.qt.io/browse/QTBUG-70223) tst_Gestures::partialGesturePropagation autotest fails on
Ubuntu 18.04 & SLES 15
* [QTBUG-67395](https://bugreports.qt.io/browse/QTBUG-67395) tst_Gestures::autoCancelGestures2 fails on Ubuntu 17.10
* [QTBUG-70227](https://bugreports.qt.io/browse/QTBUG-70227) tst_Gestures::panelStacksBehindParent autotest fails on
Ubuntu 18.04
* [QTBUG-70226](https://bugreports.qt.io/browse/QTBUG-70226) tst_Gestures::panelPropagation autotest fails on Ubuntu
18.04
* [QTBUG-70209](https://bugreports.qt.io/browse/QTBUG-70209) tst_Gestures::graphicsViewParentPropagation autotest
fails on Ubuntu 18.04
* [QTBUG-70153](https://bugreports.qt.io/browse/QTBUG-70153) tst_Gestures::autoCancelGestures2 autotest fails on
Ubuntu 18.04
* [QTBUG-45048](https://bugreports.qt.io/browse/QTBUG-45048) 2 QProgressBar's have differing behaviour, if one has
setTextVisible(true)
* [QTBUG-131108](https://bugreports.qt.io/browse/QTBUG-131108) tst_QFont::italicOblique CI test fails on Android 15
* [QTBUG-131262](https://bugreports.qt.io/browse/QTBUG-131262) Freetype: Variable font named instances with slant not
detected as oblique
* [QTBUG-18068](https://bugreports.qt.io/browse/QTBUG-18068) When a corner widget in a QTabWidget is hidden then the
space is not reclaimed for the tabs
* [QTBUG-130980](https://bugreports.qt.io/browse/QTBUG-130980) There is a bug with line spacing when QLabel displays
rich text.
* [QTBUG-130590](https://bugreports.qt.io/browse/QTBUG-130590) Winsock being initialized with "DRAFT" version of 2.0
* [QTBUG-130552](https://bugreports.qt.io/browse/QTBUG-130552) QNetworkConnectionMonitorPrivate::updateState crash
* [QTBUG-131008](https://bugreports.qt.io/browse/QTBUG-131008) QZipReader::extractAll wrongly creates directories for
entries in zip root dir
* [QTBUG-130799](https://bugreports.qt.io/browse/QTBUG-130799) Remove or fix Q_OBJECT qdoc macro
* [QTBUG-129576](https://bugreports.qt.io/browse/QTBUG-129576) [Boot2Qt] Running "QQuickRenderControl RHI Example" app
with OpenGL graphic api causes the view to become black
* [QTBUG-130887](https://bugreports.qt.io/browse/QTBUG-130887) compose handling is broken
* [QTBUG-62502](https://bugreports.qt.io/browse/QTBUG-62502) QJsonDocument only supports arrays and objects
* [QTBUG-130673](https://bugreports.qt.io/browse/QTBUG-130673) Windows11 Style : title bar doesn't highlight for active
mdisubwindow
* [QTBUG-130000](https://bugreports.qt.io/browse/QTBUG-130000) Keyboard does not get focus on Android TV
* [QTBUG-131368](https://bugreports.qt.io/browse/QTBUG-131368) tst_QWindow::framePositioning() is flaky on Linux
* [QTBUG-130371](https://bugreports.qt.io/browse/QTBUG-130371) Keyboard navigation focus in WebAssembly is half broken
* [QTBUG-131587](https://bugreports.qt.io/browse/QTBUG-131587) Flaky emoji rendering on Windows
* [QTBUG-131632](https://bugreports.qt.io/browse/QTBUG-131632) REG: Bengali text missing
* [QTBUG-131446](https://bugreports.qt.io/browse/QTBUG-131446) QMetaProperty documentation references deprecated
"type()" function
* [QTBUG-131491](https://bugreports.qt.io/browse/QTBUG-131491) QDateTime comparision is slow even the same timezone is
set
* [QTBUG-131487](https://bugreports.qt.io/browse/QTBUG-131487) QFileSystemModel does not work with QML DelegateModel
* [QTBUG-129575](https://bugreports.qt.io/browse/QTBUG-129575)  Fix API flaw for QImage::mirror and QImage::mirrored
* [QTBUG-122609](https://bugreports.qt.io/browse/QTBUG-122609) moc takes 'constexpr' as function return type
* [QTBUG-129439](https://bugreports.qt.io/browse/QTBUG-129439) QToolBar incorrect display on Windows 11
* [QTBUG-129700](https://bugreports.qt.io/browse/QTBUG-129700) Windows 11 modern style | Toolbar buttons state not
legible
* [QTBUG-130822](https://bugreports.qt.io/browse/QTBUG-130822) Windows 11 style does not render ON status of toggle
button in toolbar
* [QTBUG-131664](https://bugreports.qt.io/browse/QTBUG-131664) QApplication in inPopupMode bug popupWindow is not a
widget window will cause a coredump
* [QTBUG-94860](https://bugreports.qt.io/browse/QTBUG-94860) Pushbuttons in Fusion widget style could use a bit more
padding.
* [QTBUG-131731](https://bugreports.qt.io/browse/QTBUG-131731) REG: Possible crash on macOS when disabling emoji
parsing
* [QTBUG-131782](https://bugreports.qt.io/browse/QTBUG-131782) [REG 6.8.0 -> 6.8.1] Cannot configure qtbase if
directory contains "++"
* [QTBUG-130557](https://bugreports.qt.io/browse/QTBUG-130557) SBOM has references to build time paths
* [QTBUG-131505](https://bugreports.qt.io/browse/QTBUG-131505) Unable to create multisampled depth-only pipeline
* [QTBUG-131338](https://bugreports.qt.io/browse/QTBUG-131338) qtbase tst_android testFullScreenDimensions is flaky
* [QTBUG-96105](https://bugreports.qt.io/browse/QTBUG-96105) When a window is switched to be FullScreen then it will
end up keeping a bar at the bottom of the window which should not be
visible
* [QTBUG-101968](https://bugreports.qt.io/browse/QTBUG-101968) Android: a widget is shown incorrectly in fullscreen
mode for the first time
* [QTBUG-127394](https://bugreports.qt.io/browse/QTBUG-127394) Window not drawn to full screen in immersive mode after
orientation change.
* [QTBUG-121820](https://bugreports.qt.io/browse/QTBUG-121820) Android: Mainwindow has black border in the bottom when
set to full screen
* [QTBUG-109878](https://bugreports.qt.io/browse/QTBUG-109878) Qt 6.4.1 - Android - White rectangle at the bottom of
the screen
* [QTBUG-119594](https://bugreports.qt.io/browse/QTBUG-119594) Android: Layout in display cut mode being overridden to
default edges always
* [QTBUG-131474](https://bugreports.qt.io/browse/QTBUG-131474) QNetworkRequest::setRawHeader puts header name in
lowercase
* [QTBUG-131799](https://bugreports.qt.io/browse/QTBUG-131799) SQL drivers cannot be configured due to an SBOM error.
* [QTBUG-125588](https://bugreports.qt.io/browse/QTBUG-125588) QString::arg(char16_t{}) prefers the integral, not the
QChar overload
* [QTBUG-126053](https://bugreports.qt.io/browse/QTBUG-126053) QString::arg(u8' ') prefers the integral, not the QChar
overload, when built in C++20
* [QTBUG-126055](https://bugreports.qt.io/browse/QTBUG-126055) [REG SiC 6.4 -> 6.5] QString::arg(qfloat16{}) is
ambiguous if QFLOAT16_IS_NATIVE
* [QTBUG-126054](https://bugreports.qt.io/browse/QTBUG-126054) QString::arg(wchar_t{}) prefers the integral overload
instead of the QChar one
* [QTBUG-131801](https://bugreports.qt.io/browse/QTBUG-131801) QHttpNetworkRequestPrivate copy constructor does not
copy fullLocalServerName
* [QTBUG-110898](https://bugreports.qt.io/browse/QTBUG-110898) Window disappears when monitor is disconnected
* [QTBUG-130714](https://bugreports.qt.io/browse/QTBUG-130714) Qt applications crash when dragging to a different X11
Screen
* [QTBUG-131741](https://bugreports.qt.io/browse/QTBUG-131741) [Reg 6.5.7 -> 6.8.0][iOS] QDesktopServices URL Handler
(custom scheme) no longer receives data from external apps
* [QTBUG-112346](https://bugreports.qt.io/browse/QTBUG-112346) qmllint fails when WebView is used
* [QTBUG-129722](https://bugreports.qt.io/browse/QTBUG-129722) [asan] use-after-free in pulseaudio logger
* [QTBUG-130630](https://bugreports.qt.io/browse/QTBUG-130630) AddressSanitizer: heap-use-after-free on
tst_qopcuaclient
* [QTBUG-131880](https://bugreports.qt.io/browse/QTBUG-131880) [macOS] Crash on [NSSavePanel
didEndPanelWithReturnCode:]
* [QTBUG-131883](https://bugreports.qt.io/browse/QTBUG-131883) SBOM prevent installing modules in different directory
* [QTBUG-131151](https://bugreports.qt.io/browse/QTBUG-131151) QDomDocument::toByteArray() crashes when parsing svg
file.
* [QTBUG-131906](https://bugreports.qt.io/browse/QTBUG-131906) FAIL!  :
tst_qqmlecmascript::componentCreation(invalidMode) Not all expected
messages were received
* [QTBUG-131950](https://bugreports.qt.io/browse/QTBUG-131950) Creator help mode: footer for main index.html is in
middle of page
* [QTBUG-131761](https://bugreports.qt.io/browse/QTBUG-131761) Incorrect display of :selected state of QCombobox on
"windows" style plugin
* [QTBUG-131976](https://bugreports.qt.io/browse/QTBUG-131976) The alternateBase color in dark W11 style is wrong
* [QTBUG-131913](https://bugreports.qt.io/browse/QTBUG-131913) Incorrect QTimeZone documentation
* [QTBUG-45949](https://bugreports.qt.io/browse/QTBUG-45949) QToolBar icon-size can not be styled as documented
* [QTBUG-132066](https://bugreports.qt.io/browse/QTBUG-132066) contextMenuEvent no longer works
* [QTBUG-132101](https://bugreports.qt.io/browse/QTBUG-132101) Extra semicolon warnings in qdirlisting.h, qaccessible.h
and qkeysequence.h
* [QTBUG-132111](https://bugreports.qt.io/browse/QTBUG-132111) qtbase/fa4bd30caa079a3b1e5eac1bb4f17365f456b8f9 breaks
-unity-build
* [QTBUG-112746](https://bugreports.qt.io/browse/QTBUG-112746) QAnyStringView missing implicit conversion from char[]
with unknown size
* [QTBUG-132115](https://bugreports.qt.io/browse/QTBUG-132115) QDateTimeParser::parse assertion triggered in case of
invalid date
* [QTBUG-132053](https://bugreports.qt.io/browse/QTBUG-132053) FTBFS: Compilation of qsharedmemory_p.h fails with
sysv_sem disabled
* [QTBUG-73390](https://bugreports.qt.io/browse/QTBUG-73390) QMenu Action is not triggered by numeric mnemonic entered
on keypad
* [QTBUG-127522](https://bugreports.qt.io/browse/QTBUG-127522) QBENCHMARK result does not output global data tag
* [QTBUG-132150](https://bugreports.qt.io/browse/QTBUG-132150) androiddeployqt does not strip quotation marks from
static namespace string retrieved from build.gradle
* [QTBUG-131586](https://bugreports.qt.io/browse/QTBUG-131586)  QLineEdit's bottom edge is the wrong color when in Dark
mode.
* [QTBUG-122797](https://bugreports.qt.io/browse/QTBUG-122797) QStringRef doesn't convert to QAnyStringView
* [QTBUG-122798](https://bugreports.qt.io/browse/QTBUG-122798) [REG 5.15 -> 6.7 (or earlier)] QStringRef -> QStringView
conversion loses null-ness
* [QTBUG-132256](https://bugreports.qt.io/browse/QTBUG-132256) Drag and drop not working
* [QTBUG-131707](https://bugreports.qt.io/browse/QTBUG-131707) Multi-ABI Android builds only work on base kit arch
* [QTBUG-132091](https://bugreports.qt.io/browse/QTBUG-132091) macOS: Key modifiers aren't ignored when dragging
'within the application'
* [QTBUG-131685](https://bugreports.qt.io/browse/QTBUG-131685) QDoubleSpinBox: Style sheet Property Selector doesn't
reset font back to original style
* [QTBUG-132124](https://bugreports.qt.io/browse/QTBUG-132124) stream 1 finished with error: ""
* [QTBUG-132073](https://bugreports.qt.io/browse/QTBUG-132073) Not possible to use ContextMenu on event-consuming types
like Pane
* [QTBUG-130275](https://bugreports.qt.io/browse/QTBUG-130275) Segmentation Fault when using InsertWidget with too-
large index
* [QTBUG-130992](https://bugreports.qt.io/browse/QTBUG-130992) Crash when rendering radialGradient
* [QTBUG-87776](https://bugreports.qt.io/browse/QTBUG-87776) Move Qt::FooPrivate targets into separate CMake packages
* [QTBUG-131716](https://bugreports.qt.io/browse/QTBUG-131716) QCommandLineParser::helpText fails if no options are
added
* [QTBUG-132075](https://bugreports.qt.io/browse/QTBUG-132075) tst_qquicktext::multilengthStrings(Wrap) Compared
doubles are not the same (fuzzy compare)
* [QTBUG-132104](https://bugreports.qt.io/browse/QTBUG-132104) QVariant::fromValue fails with std::unordered_map
* [QTBUG-132332](https://bugreports.qt.io/browse/QTBUG-132332) QSaveFile will empty file if no space left on device
* [QTBUG-132431](https://bugreports.qt.io/browse/QTBUG-132431) Stylesheet Margin/Padding squashes QSpinBox
* [QTBUG-132347](https://bugreports.qt.io/browse/QTBUG-132347) blake2b symbols exported in static builds
* [QTBUG-131959](https://bugreports.qt.io/browse/QTBUG-131959) Build failure on QtFuture::whenAll(QFuture<void>,
QFuture<void>)
* [QTBUG-21329](https://bugreports.qt.io/browse/QTBUG-21329) QTransform::quadToQuad() doesn't work, when passed
QRectFs
* [QTBUG-132258](https://bugreports.qt.io/browse/QTBUG-132258) _qt_internal_create_command_script fails on windows if
spaces present
* [QTBUG-132340](https://bugreports.qt.io/browse/QTBUG-132340) QmlTools not automatically found
* [QTBUG-132085](https://bugreports.qt.io/browse/QTBUG-132085) [REG 6.7 -> 6.8][Android] Stuck in SplashScreen on
Restart
* [QTBUG-130766](https://bugreports.qt.io/browse/QTBUG-130766) QtConcurrent::blockingMapped has incorrect argument
deduction for generic lambdas
* [QTBUG-132188](https://bugreports.qt.io/browse/QTBUG-132188) Could not find external SBOM document
* [QTBUG-94890](https://bugreports.qt.io/browse/QTBUG-94890) Shortcut with "Backtab" does not work for Windows
* [QTBUG-123843](https://bugreports.qt.io/browse/QTBUG-123843) Swipping with three finger between apps may cause a
crash after interacting with a text input field
* [QTBUG-131843](https://bugreports.qt.io/browse/QTBUG-131843) File/Folder link overlay is missing, or wrong
size/position
* [QTBUG-132059](https://bugreports.qt.io/browse/QTBUG-132059) Crash when quickly invoking subsequent scrollAction
* [QTBUG-132381](https://bugreports.qt.io/browse/QTBUG-132381) [REG 6.8 -> 6.9] Crash when QGuiApplication is static
* [QTBUG-129242](https://bugreports.qt.io/browse/QTBUG-129242) QTableWidget selection issue
* [QTBUG-132281](https://bugreports.qt.io/browse/QTBUG-132281) Add change-notification signal to
QInputDevice::capabilities property
* [QTBUG-132410](https://bugreports.qt.io/browse/QTBUG-132410) Q_JNI_NATIVE_METHOD floating point argument corruption
on x86_64
* [QTBUG-132581](https://bugreports.qt.io/browse/QTBUG-132581) QMake triggers abnormally many "zero as null pointer
constant" warnings on macOS
* [QTBUG-132414](https://bugreports.qt.io/browse/QTBUG-132414) embedding a widget window in qml does not draw the
window
* [QTBUG-132622](https://bugreports.qt.io/browse/QTBUG-132622) Failed to find required Qt component "Protobuf"
* [QTBUG-132616](https://bugreports.qt.io/browse/QTBUG-132616) Failed to find the host tool "Qt6::qtwaylandscanner"
* [QTBUG-132670](https://bugreports.qt.io/browse/QTBUG-132670) QTreeView does not always refresh on dataChanged
* [QTBUG-131372](https://bugreports.qt.io/browse/QTBUG-131372) QStandardItem::appendRow does not update model
recursively
* [QTBUG-132597](https://bugreports.qt.io/browse/QTBUG-132597) Incorrect description of QTemporaryFile behavior when
two placeholders are present
* [QTBUG-132697](https://bugreports.qt.io/browse/QTBUG-132697) FAIL!  :
tst_QQmlDebugJS::setBreakpointInScriptThatQuits(custom)
'm_process->waitForFinished()' returned FALSE.
* [QTBUG-102984](https://bugreports.qt.io/browse/QTBUG-102984) QML debugger and profiler tests hangs on macOS/x86_64 in
CI
* [QTBUG-132133](https://bugreports.qt.io/browse/QTBUG-132133) QSpan<const T> causes Qt container to detach
* [QTBUG-127467](https://bugreports.qt.io/browse/QTBUG-127467) QtAbstractItemModel asserts when being rapidly modified
* [QTBUG-132698](https://bugreports.qt.io/browse/QTBUG-132698) Debug build fails at qtimezonelocale.cpp
* [QTBUG-121418](https://bugreports.qt.io/browse/QTBUG-121418) [Regr: 5.x -> 6.x] QTranslator loads zh instead of zh_TW
translation
* [QTBUG-132155](https://bugreports.qt.io/browse/QTBUG-132155) Android apps with armeabi-v7a architecture crash after
startup
* [QTBUG-130909](https://bugreports.qt.io/browse/QTBUG-130909) Color Emojis don't render at all on Android 15
* [QTBUG-131116](https://bugreports.qt.io/browse/QTBUG-131116) Freetype: Support COLR format color fonts
* [QTBUG-129698](https://bugreports.qt.io/browse/QTBUG-129698) Widget doesn't show after windowHandle()->destroy()
* [QTBUG-132841](https://bugreports.qt.io/browse/QTBUG-132841) Android QtAbstractItemModel wrong JNI call for sibling()
method
* [QTBUG-132255](https://bugreports.qt.io/browse/QTBUG-132255) Different emoji font resolution in Freetype on Windows
* [QTBUG-87417](https://bugreports.qt.io/browse/QTBUG-87417) tst_QLineEdit fails on Android
* [QTBUG-132873](https://bugreports.qt.io/browse/QTBUG-132873) QtWidgets: QEvent::ContextMenu is not spontaneous in
6.9.0 beta 2 anymore
* [QTBUG-125892](https://bugreports.qt.io/browse/QTBUG-125892) QtDS compatibility - Improve qmldir path discovery
* [QTBUG-125970](https://bugreports.qt.io/browse/QTBUG-125970) QML components with the same name under a module
* [QTBUG-125971](https://bugreports.qt.io/browse/QTBUG-125971) Java QML codegen source file handling
* [QTBUG-132804](https://bugreports.qt.io/browse/QTBUG-132804) Debug build fails at qgenericunixthemes.cpp
* [QTBUG-125285](https://bugreports.qt.io/browse/QTBUG-125285) QKdeTheme falls back to Qt::ColorScheme::Unknown on
invalid desktop theme
* [QTBUG-132875](https://bugreports.qt.io/browse/QTBUG-132875) CMYK to RGB conversion on big endian produces
significantly wrong colors
* [QTBUG-132377](https://bugreports.qt.io/browse/QTBUG-132377) Broken country flags emoji rendering in KDE
* [QTBUG-132891](https://bugreports.qt.io/browse/QTBUG-132891) Whitespace in projectPath fails
* [QTBUG-131631](https://bugreports.qt.io/browse/QTBUG-131631) widgets/itemviews/simpletreemodel not configuring on iOS
* [QTBUG-132398](https://bugreports.qt.io/browse/QTBUG-132398) Unsupported linker script to make objective-c classnames
unique is broken since Xcode14
* [QTBUG-132912](https://bugreports.qt.io/browse/QTBUG-132912) [REG 6.8.1->6.9.0 beta1&2](Windows/Linux X11) Designer
crashes when dragging OpenGLWidget, QQuickWidget or QWebEngineView to
canvas
* [QTBUG-132609](https://bugreports.qt.io/browse/QTBUG-132609) Configuring a single-config qtopcua might fail to build
tools when built against a multi-config Qt
* [QTBUG-132338](https://bugreports.qt.io/browse/QTBUG-132338) QtOpcUa Required QtVersion Wrong
* [QTBUG-132575](https://bugreports.qt.io/browse/QTBUG-132575) QEasingCurve streaming operators (in/out a QDataStream)
will crash
* [QTBUG-130884](https://bugreports.qt.io/browse/QTBUG-130884) xdg-desktop-portal should be enabled only environments
that actually supports it
* [QTBUG-70798](https://bugreports.qt.io/browse/QTBUG-70798) Qfiledialog Does Not Correctly Restore the Directory
* [QTBUG-132801](https://bugreports.qt.io/browse/QTBUG-132801) Building Qt with separate debug info fails on QNX
* [QTBUG-122642](https://bugreports.qt.io/browse/QTBUG-122642) The SQL QODBC driver implementation fails to escape
passwords set with setPassword(...) when using special characters.
* [QTBUG-132173](https://bugreports.qt.io/browse/QTBUG-132173) The cell borders in QTextTableFormat are not being
painted.
* [QTBUG-131894](https://bugreports.qt.io/browse/QTBUG-131894) qtranslator loads wrong locale
* [QTBUG-132724](https://bugreports.qt.io/browse/QTBUG-132724) `qt_internal_generate_user_facing_tools_info` is not
relocatable
* [QTBUG-118176](https://bugreports.qt.io/browse/QTBUG-118176) qdoc: Generate \internal documentation correctly when
--showinternal is set
* [QTBUG-132906](https://bugreports.qt.io/browse/QTBUG-132906) Reg[6.5->6.8]Windows11 style crashing with drawPrimitive
* [QTBUG-132356](https://bugreports.qt.io/browse/QTBUG-132356) Out-of-bounds read in
QRhiVulkan::endAndSubmitPrimaryCommandBuffer
* [QTBUG-133128](https://bugreports.qt.io/browse/QTBUG-133128) Windows11Style: QSlider min position off
* [QTBUG-57209](https://bugreports.qt.io/browse/QTBUG-57209) Wrong documentation for QOpenGLTexture::setWrapMode
* [QTBUG-132952](https://bugreports.qt.io/browse/QTBUG-132952) Mouse messages for QDockWidget are incorrectly cast to
QMainWindow causing a crash
* [QTBUG-112758](https://bugreports.qt.io/browse/QTBUG-112758) QMdiArea (in TabbedView mode): issues after moving tab
* [QTBUG-113458](https://bugreports.qt.io/browse/QTBUG-113458) DirectWrite don't handle CBDT, COLRv1, sbix, SVG color
fonts
* [QTBUG-132808](https://bugreports.qt.io/browse/QTBUG-132808) Vulkan validation error on vkAcquireNextImageKHR (using
validation layer bundled with 1.4.304)
* [QTBUG-122819](https://bugreports.qt.io/browse/QTBUG-122819) QOpenGLWidget: error: GL_INVALID_OPERATION in
glDrawBuffers(unsupported buffer GL_BACK_LEFT)
* [QTBUG-132780](https://bugreports.qt.io/browse/QTBUG-132780) Faulty call to glDrawBuffers in RhiGles2 backend
* [QTBUG-132935](https://bugreports.qt.io/browse/QTBUG-132935) a11y: Qt application on Linux doesn't report accessible
parent
* [QTBUG-133207](https://bugreports.qt.io/browse/QTBUG-133207) REG: Controls C++ tests not run with all styles
* [QTBUG-133289](https://bugreports.qt.io/browse/QTBUG-133289) Moving window container crashes if the window has been
destroyed
* [QTBUG-129233](https://bugreports.qt.io/browse/QTBUG-129233) tooltip will change focus on webassembly
* [QTBUG-133330](https://bugreports.qt.io/browse/QTBUG-133330) tst_qmenu crashes with MSVC in debug mode
* [QTBUG-132831](https://bugreports.qt.io/browse/QTBUG-132831) QSet::remove() unconditionally detaches
* [QTBUG-132945](https://bugreports.qt.io/browse/QTBUG-132945) QDuplicateTracker::clear() leaks memory
* [QTBUG-56952](https://bugreports.qt.io/browse/QTBUG-56952) [REG: 5.4.2->5.5.0] Duplicated hotkeys in menus not
working in some styles if first action is disabled
* [QTBUG-132911](https://bugreports.qt.io/browse/QTBUG-132911) Typo in QPermission docs
* [QTBUG-133336](https://bugreports.qt.io/browse/QTBUG-133336) FTBFS MinGW no matching function for call to
'IDWritePaintReader::MoveToFirstChild(DWRITE_PAINT_ELEMENT*)'
* [QTBUG-132752](https://bugreports.qt.io/browse/QTBUG-132752) QSqlQuery issues a deprecation warning in QMetaType
* [QTBUG-91766](https://bugreports.qt.io/browse/QTBUG-91766) Changing copy of QSqlQuery changes original.
* [QTBUG-133445](https://bugreports.qt.io/browse/QTBUG-133445) ibus x11 doesn't work in 6.9 and dev on Ubuntu 24.04
GNOME
* [QTBUG-133101](https://bugreports.qt.io/browse/QTBUG-133101) GCC defines __PIC__ with -fPIE (was: Weird
QObject::findChild() behavior)
* [QTBUG-133430](https://bugreports.qt.io/browse/QTBUG-133430) Qt fails to build on certain Intel CPUs due to
avx512_fp16 with GCC14 (src/gui/painting/qrgbafloat.h)
* [QTBUG-133297](https://bugreports.qt.io/browse/QTBUG-133297) [macOS] Some emojis are rendering incorrect in some
sizes
* [QTBUG-133032](https://bugreports.qt.io/browse/QTBUG-133032) Qt 6.8.1 "isRelocatable: undeclared identifier"
* [QTBUG-133403](https://bugreports.qt.io/browse/QTBUG-133403) [REG 6.8.0 -> 6.8.1]
QUrl::adjusted(NormalizePathSegments) can produce an invalid URL
* [QTBUG-133402](https://bugreports.qt.io/browse/QTBUG-133402) [REG 6.8.0 -> 6.8.1] QUrl::resolved() can produce an
invalid path like "/../"
* [QTBUG-132490](https://bugreports.qt.io/browse/QTBUG-132490) Android and TestNamespace: errors in Qt JNI methods
* [QTBUG-132500](https://bugreports.qt.io/browse/QTBUG-132500) [REG 6.7 -> 6.8] QSet::unite() no longer consistently
picks equivalent elements from `other`
* [QTBUG-132536](https://bugreports.qt.io/browse/QTBUG-132536) QSet::intersect() picks equivalent elements
inconsistently  from `other` or *this
* [QTBUG-132700](https://bugreports.qt.io/browse/QTBUG-132700) [REG 6.6 -> 6.7] Click event handling not working using
mouse/trackpad on Android
* [QTBUG-130297](https://bugreports.qt.io/browse/QTBUG-130297) Cannot click buttons in ChromeOS
* [QTBUG-131946](https://bugreports.qt.io/browse/QTBUG-131946) The quality of font rendering has dropped dramatically
since version 6.8
* [QTBUG-133405](https://bugreports.qt.io/browse/QTBUG-133405) Repeated texture readbacks crash
* [QTBUG-133454](https://bugreports.qt.io/browse/QTBUG-133454) QRhi: finish() with D3D12 not fully functional when
called outside begin/endFrame()
* [QTBUG-133516](https://bugreports.qt.io/browse/QTBUG-133516) Windows MinGW: TestNamespace errors in qcomobject
* [QTWEBSITE-1202](https://bugreports.qt.io/browse/QTWEBSITE-1202) Broken tabs in translated docs
* [QTBUG-133117](https://bugreports.qt.io/browse/QTBUG-133117) Windows11Style: Check boxes and radio buttons slightly
cropped at 150%
* [QTBUG-132057](https://bugreports.qt.io/browse/QTBUG-132057) WebAssembly - App "Window" moves outside of visible area
* [QTBUG-132589](https://bugreports.qt.io/browse/QTBUG-132589) Android Edit text context menu pointers are in wrong
place
* [QTBUG-133525](https://bugreports.qt.io/browse/QTBUG-133525) [REG] mac style: merged title bar and content area no
longer works
* [QTBUG-133651](https://bugreports.qt.io/browse/QTBUG-133651) uic: Changing Palette in Designer breaks UI with Qt
5.15.2
* [QTBUG-118032](https://bugreports.qt.io/browse/QTBUG-118032) Application crash due to double invocation of
continuation in multithreaded QPromise and QFuture usage
* [QTBUG-132249](https://bugreports.qt.io/browse/QTBUG-132249) AndroidTestRunner: allow to call additional/extra adb
call
* [QTBUG-118997](https://bugreports.qt.io/browse/QTBUG-118997) missing D-Bus Viewer manual
* [QTBUG-133376](https://bugreports.qt.io/browse/QTBUG-133376) #warning preprocessor macro is used in
qtdeprecationdefinitions.h
* [QTBUG-132314](https://bugreports.qt.io/browse/QTBUG-132314) GPU driver crash in iOS 18
* [QTBUG-133644](https://bugreports.qt.io/browse/QTBUG-133644) [REG 6.6.3 -> 6.8.1] Assertion failure at QApplication
destruction
* [QTBUG-133663](https://bugreports.qt.io/browse/QTBUG-133663) QDesktopServices::openUrl() misses query part
* [QTBUG-133689](https://bugreports.qt.io/browse/QTBUG-133689) tst_qbytearrayview fails to compile with libc++ 19
* [QTBUG-133725](https://bugreports.qt.io/browse/QTBUG-133725) qml_tool_autogen target loses almost all dependencies on
other autogen and sync_headers targets
* [QTBUG-133776](https://bugreports.qt.io/browse/QTBUG-133776) calling exit after constructing QApplication crash
* [QTBUG-133808](https://bugreports.qt.io/browse/QTBUG-133808) Including QFlag causes compilation failure with Clang
19, libcpp, and C++23
* [QTBUG-133480](https://bugreports.qt.io/browse/QTBUG-133480) Combined flag emojis are not properly rendered
* [QTBUG-133500](https://bugreports.qt.io/browse/QTBUG-133500) [REG 6.8.1 -> 6.8.2] Crash on exit during logging of
thread destruction
* [QTBUG-133810](https://bugreports.qt.io/browse/QTBUG-133810) CMake Multi-ABI builds not copying sub-ABIs libraries
* [QTBUG-131862](https://bugreports.qt.io/browse/QTBUG-131862) Android multi-ABI build stopped working
* [QTBUG-133850](https://bugreports.qt.io/browse/QTBUG-133850) Using qt_wrap_ui causes build failure
* [QTBUG-133269](https://bugreports.qt.io/browse/QTBUG-133269) QTextStream: suspicious negation when streaming numbers
* [QTBUG-133118](https://bugreports.qt.io/browse/QTBUG-133118) Windows11Style: Item view selection hardly legible
* [QTBUG-132121](https://bugreports.qt.io/browse/QTBUG-132121) Bad signal restoration cause infinite loop in
FatalSignalHandler destructor
* [QTBUG-131574](https://bugreports.qt.io/browse/QTBUG-131574) Qt 6.8 displays some font families in DemiBold much
thicker than with Qt6.7
* [QTBUG-133782](https://bugreports.qt.io/browse/QTBUG-133782) Mistakenly rounding down "bytesPerLine" for QPixmap
* [QTBUG-128458](https://bugreports.qt.io/browse/QTBUG-128458) ui文件中创建了QProgressBar对象，运行出来的结果为啥是一条横线，和设计ui界面上的显示不一致
* [QTBUG-133577](https://bugreports.qt.io/browse/QTBUG-133577) [iOS] [REG] Including a Swift file leads to a startup
error
* [QTBUG-133781](https://bugreports.qt.io/browse/QTBUG-133781) Regression - Button clicks open keyboard in WebAssembly
on Android
* [QTBUG-130458](https://bugreports.qt.io/browse/QTBUG-130458) Fusion theme doesn't use accent color in Windows light
mode
* [QTBUG-133954](https://bugreports.qt.io/browse/QTBUG-133954) Make sure that new 'Classes for string data' can be
found in TOC
* [QTBUG-129300](https://bugreports.qt.io/browse/QTBUG-129300) Cannot bind QRhi 3D texture to shader in DirectX 11 and
12 (with working workaround)
* [QTBUG-127528](https://bugreports.qt.io/browse/QTBUG-127528) QApplication::fontMetrics() deprecation message is too
vague
* [QTBUG-134101](https://bugreports.qt.io/browse/QTBUG-134101) Qt 6.9.0 with uncompressed libraries doesn't work with
split APKs
* [QTBUG-134235](https://bugreports.qt.io/browse/QTBUG-134235) Build failure of qtbase/src/widgets/styles/qdrawutil.cpp
with disabled features
* [QTBUG-133406](https://bugreports.qt.io/browse/QTBUG-133406) Unrechable code in MetaTypeQFutureHelper
* [QTBUG-134447](https://bugreports.qt.io/browse/QTBUG-134447) Modal dialog looks disabled
* [QTBUG-134316](https://bugreports.qt.io/browse/QTBUG-134316) [Reg] QFileOpenEvent isn't emitted for custom URI
* [QTBUG-134473](https://bugreports.qt.io/browse/QTBUG-134473) Font rendering of Qt Creators Text Editor is broken
* [QTBUG-134080](https://bugreports.qt.io/browse/QTBUG-134080) "QObject::~QObject: Timers cannot be stopped from
another thread" message in Qt 6.8.2 plugins
* [QTBUG-133861](https://bugreports.qt.io/browse/QTBUG-133861) [macOS] QML Preview: Closing the preview window produces
QObject::killTimer warning
* [QTBUG-134930](https://bugreports.qt.io/browse/QTBUG-134930) [REG 6.9] QLabel scaled pixmap is broken
* [QTBUG-94871](https://bugreports.qt.io/browse/QTBUG-94871) Qt should subscribe to dbus system tray and dbus menu
service appearing/disappearing
* [PYSIDE-2772](https://bugreports.qt.io/browse/PYSIDE-2772) QTreeView is not displaying the data even though
QAbstractItemModel has an item.
* [QTBUG-125097](https://bugreports.qt.io/browse/QTBUG-125097) Q_APPLICATION_STATIC needs to say that it's in #include
<QtCore/QApplicationStatic>
* [QTBUG-117321](https://bugreports.qt.io/browse/QTBUG-117321) Inconsistent treatment of char[] with embedded NULs when
target is QString vs. QByteArray
* [QTBUG-126248](https://bugreports.qt.io/browse/QTBUG-126248) macOS: widget UI flashes when overriding color scheme
during UI construction
* [QTBUG-125446](https://bugreports.qt.io/browse/QTBUG-125446) Ubuntu 24.04 ARM64: HealthCheck qtbase failings
* [QTBUG-126200](https://bugreports.qt.io/browse/QTBUG-126200) tst_QFloat16Format::format() failed on linux arm64
* [QTBUG-126178](https://bugreports.qt.io/browse/QTBUG-126178) QtQuickView does not handle user input in a LinearLayout
* [QTBUG-119321](https://bugreports.qt.io/browse/QTBUG-119321) FAIL!  : tst_QSharedMemory::useTooMuchMemory(POSIX) in
Debian - Linux on ARM
* [QTBUG-126225](https://bugreports.qt.io/browse/QTBUG-126225) tst_QSharedMemory::useTooMuchMemory(POSIX) timeout on
linux arm64 in CI
* [QTBUG-126278](https://bugreports.qt.io/browse/QTBUG-126278) QNetworkReply::attribute(HttpReasonPhraseAttribute)
returns empty value when Http2 is used
* [QTBUG-126177](https://bugreports.qt.io/browse/QTBUG-126177) Crash when adding a QtQuickView before loading the
component
* [QTBUG-126395](https://bugreports.qt.io/browse/QTBUG-126395) moc fails to parse around QT_WARNING macros in Q_SIGNALS
sections
* [QTBUG-124572](https://bugreports.qt.io/browse/QTBUG-124572) Program crash when using a specific glyph from a popular
font file on Linux
* [QTBUG-126385](https://bugreports.qt.io/browse/QTBUG-126385)  tst_lupdate ...............................***Failed
* [QTBUG-126546](https://bugreports.qt.io/browse/QTBUG-126546) Attribution documentation processed twice in CI
* [QTBUG-114812](https://bugreports.qt.io/browse/QTBUG-114812) No HTTP status code when HTTP reply received during body
upload
* [QTBUG-126008](https://bugreports.qt.io/browse/QTBUG-126008) tst_QSettings::testErrorHandling() is silently passing
because of broken #if logic
* [QTBUG-113404](https://bugreports.qt.io/browse/QTBUG-113404) Wayland: Gestures are not delivered to correct top level
widget
* [QTBUG-125878](https://bugreports.qt.io/browse/QTBUG-125878) Cannot pinch-to-zoom after the qt 6.7.1 upgrade
[regression]
* [QTBUG-126313](https://bugreports.qt.io/browse/QTBUG-126313) QScroller gesture blocks mouse clicks
* [QTBUG-106653](https://bugreports.qt.io/browse/QTBUG-106653) Crash on Accessibility interface
* [QTBUG-126727](https://bugreports.qt.io/browse/QTBUG-126727) [QNX 7.1, Qt 6.7.2] Linking errors when building graphs
and quickcontrols examples with installed QNX binary
* [QTBUG-125772](https://bugreports.qt.io/browse/QTBUG-125772) The loading order affects QIcon and makes it show the
wrong source image.
* [QTBUG-126426](https://bugreports.qt.io/browse/QTBUG-126426) QStyleOptionProgressBar is not properly rendered by a
delegate
* [QTBUG-124919](https://bugreports.qt.io/browse/QTBUG-124919) QDBusSignature considers an empty string to be an
invalid signature
* [QTBUG-124653](https://bugreports.qt.io/browse/QTBUG-124653) Regression in QTemporaryFile::fileName()
* [QTBUG-125405](https://bugreports.qt.io/browse/QTBUG-125405) QPdfWriter must use a cmap table for embedded TrueType
fonts
* [QTBUG-126150](https://bugreports.qt.io/browse/QTBUG-126150) QJniArray::const_iterator should be random-access, not
just bidirectional
* [QTBUG-126729](https://bugreports.qt.io/browse/QTBUG-126729) [AutoTests] breaks target_precompile_headers(REUSE_FROM)
* [QTBUG-119616](https://bugreports.qt.io/browse/QTBUG-119616) tst_Http2::duplicateRequestsWithAborts fails in CI
* [QTBUG-125569](https://bugreports.qt.io/browse/QTBUG-125569) Make sure licensing in file matches that in
qt_attribution.json
* [QTBUG-127052](https://bugreports.qt.io/browse/QTBUG-127052) qt_add_translations does not add the generated .ts files
to the source list of the target
* [QTBUG-84628](https://bugreports.qt.io/browse/QTBUG-84628) Unneeded private .pri files are generated/installed
* [QTBUG-126866](https://bugreports.qt.io/browse/QTBUG-126866) Archiving the application does not have debug info files
(dSYM) included as expected
* [QTBUG-127073](https://bugreports.qt.io/browse/QTBUG-127073) tst_QDnsLookup failures
* [QTBUG-127404](https://bugreports.qt.io/browse/QTBUG-127404) CMake deployment API doesn't allow deploying into bin
subdirectories
* [QTBUG-120138](https://bugreports.qt.io/browse/QTBUG-120138) Showing a child Window more than once fails on
WebAssembly
* [QTBUG-127464](https://bugreports.qt.io/browse/QTBUG-127464) Intel CET hardening needs an opt-out for WebEngine
* [QTBUG-123172](https://bugreports.qt.io/browse/QTBUG-123172) tst_QApplication::abortQuitOnShow() crash on
Wayland(GNOME, Ubuntu 22.04)
* [QTBUG-87728](https://bugreports.qt.io/browse/QTBUG-87728) tst_QGraphicsAnchorLayout::layoutDirection() failed on
Ubuntu 20.04 in CI
* [QTBUG-107157](https://bugreports.qt.io/browse/QTBUG-107157) tst_QWidget with QtWayland failed on Ubuntu 22.04, GNOME
* [QTBUG-127085](https://bugreports.qt.io/browse/QTBUG-127085) Crash when re-opening laptop lid
* [QTBUG-126187](https://bugreports.qt.io/browse/QTBUG-126187) HW Keyboard input is broken after touching UI
* [QTBUG-109081](https://bugreports.qt.io/browse/QTBUG-109081) Not all string concatenation operations are possible
when QStringBuilder is disabled
* [QTBUG-68865](https://bugreports.qt.io/browse/QTBUG-68865) tst_QMenuBar::check_menuPosition autotest fails on Ubuntu
18.04
* [QTBUG-118901](https://bugreports.qt.io/browse/QTBUG-118901) qt_feature for exceptions
* [QTBUG-127928](https://bugreports.qt.io/browse/QTBUG-127928) tst_bmtrimpath.cpp:243:59: error: use of overloaded
operator '+' is ambiguous
* [QTBUG-127931](https://bugreports.qt.io/browse/QTBUG-127931) error: ambiguous overload for ‘operator+’
* [QTBUG-127806](https://bugreports.qt.io/browse/QTBUG-127806) QLineEdit selects all text when receiving focus.
* [QTBUG-127959](https://bugreports.qt.io/browse/QTBUG-127959) QIdentityProxyModel needs a way to disable builting
handling of layoutChanged and dataChanged
* [QTBUG-109214](https://bugreports.qt.io/browse/QTBUG-109214) Documentation for QtAndroidPrivate is still wrong for
CMake
* [QTBUG-127966](https://bugreports.qt.io/browse/QTBUG-127966) Error formating number with locale es_ES
* [QTBUG-117637](https://bugreports.qt.io/browse/QTBUG-117637) qfloat16 comparison with integral types is ambiguous
* [QTBUG-120637](https://bugreports.qt.io/browse/QTBUG-120637) QUuid::Id128Bytes UB when accessing members
* [QTBUG-127468](https://bugreports.qt.io/browse/QTBUG-127468) Building against Android NDK r27 fails
* [QTBUG-127457](https://bugreports.qt.io/browse/QTBUG-127457) Qt support for <span> + CSS property <margin> is broken
* [QTBUG-124011](https://bugreports.qt.io/browse/QTBUG-124011) Android: QFileInfo::isWritable() returns false
erroneously and throws an exception
* [QTBUG-127953](https://bugreports.qt.io/browse/QTBUG-127953) Basic support for CMake FetchContent
* [QTBUG-127442](https://bugreports.qt.io/browse/QTBUG-127442) REG[6.7 → 6.8]: generated qml type registration contains
invalid include paths
* [QTBUG-117358](https://bugreports.qt.io/browse/QTBUG-117358) BLUETOOTH_SCAN permission flag neverForLocation
* [QTBUG-112164](https://bugreports.qt.io/browse/QTBUG-112164) Check ACCESS_FINE_LOCATION is no longer needed in recent
Android Sdk
* [QTBUG-118877](https://bugreports.qt.io/browse/QTBUG-118877) -qreal float configuration option does not compile
* [QTBUG-126632](https://bugreports.qt.io/browse/QTBUG-126632) qmlimportscanner does not properly handle ../ in path
imports
* [QTBUG-127568](https://bugreports.qt.io/browse/QTBUG-127568) Top flaky test: tst_qtcpserver::qtbug6305
* [QTBUG-114914](https://bugreports.qt.io/browse/QTBUG-114914) Using QLocale to set it to English will also display
Chinese
* [QTBUG-122448](https://bugreports.qt.io/browse/QTBUG-122448) Date().toLoacleTimeString() doesn't respect the locale
* [QTBUG-128173](https://bugreports.qt.io/browse/QTBUG-128173) Doc: Remove use of defunct QDoc command
"\tableofcontents"
* [QTBUG-101475](https://bugreports.qt.io/browse/QTBUG-101475) QTableWidget cannot internal move item
* [QTBUG-125610](https://bugreports.qt.io/browse/QTBUG-125610) Constructing a QDate from std::chrono::year_month_day
results in link error
* [QTBUG-126672](https://bugreports.qt.io/browse/QTBUG-126672) [Regr: 6.6.3->6.7.0] Additional initial a11y element
* [QTBUG-128371](https://bugreports.qt.io/browse/QTBUG-128371) Windows ARM: Fix blacklisted
tst_qwidget::render_windowOpacity()
* [QTBUG-128372](https://bugreports.qt.io/browse/QTBUG-128372) Windows ARM: Fix blacklisted
tst_qwidget::enterLeaveOnWindowShowHide(dialog)
* [QTBUG-121653](https://bugreports.qt.io/browse/QTBUG-121653) License clarification for unicode & unicode-cldr related
files
* [QTBUG-128456](https://bugreports.qt.io/browse/QTBUG-128456) A method registered with registerNativeMethods() does
not work when the method has a jobjectArray parameter
* [QTBUG-128498](https://bugreports.qt.io/browse/QTBUG-128498) tst_qcompare fails to compile on MSVC 2022 c++20
* [QTBUG-128424](https://bugreports.qt.io/browse/QTBUG-128424) Warning messages during configure are not helpful
* [QTBUG-118851](https://bugreports.qt.io/browse/QTBUG-118851) qtbase: LTO disabled with GCC
* [QTBUG-125512](https://bugreports.qt.io/browse/QTBUG-125512) QDirListing::const_iterator copy semantics
* [QTBUG-128029](https://bugreports.qt.io/browse/QTBUG-128029) wayland: Window container in QMdiArea does not work
* [QTBUG-47713](https://bugreports.qt.io/browse/QTBUG-47713) QSqlRelationalTableModel does not allow to unset a
foreign key selection
* [QTBUG-90634](https://bugreports.qt.io/browse/QTBUG-90634) QIcon not preferring Hi DPI pixmaps when scaling
* [QTBUG-128656](https://bugreports.qt.io/browse/QTBUG-128656) Unclear usage of
QT_DECLARE_QESDP_SPECIALIZATION_DTOR_WITH_EXPORT
* [QTBUG-117514](https://bugreports.qt.io/browse/QTBUG-117514) QFuture::then marked as private
* [QTBUG-128455](https://bugreports.qt.io/browse/QTBUG-128455) [VxWorks] configure doesn't recognize graphics settings
* [QTBUG-128796](https://bugreports.qt.io/browse/QTBUG-128796) Move QAndroidApplication native interface to virtual
functions instead of static methods
* [QTBUG-128493](https://bugreports.qt.io/browse/QTBUG-128493) QIBASE Driver: Timestamps with timezones are not stored
as UTC
* [QTBUG-54693](https://bugreports.qt.io/browse/QTBUG-54693) QFileDialog::getOpenFileName crashes when parent is
deleted while dialog is open
* [QTBUG-127675](https://bugreports.qt.io/browse/QTBUG-127675) Spurious assertion failure in
tst_QSoundEffect::testSetSourceWhilePlaying
* [QTBUG-128420](https://bugreports.qt.io/browse/QTBUG-128420) Qt 6.8 does not support build paths with white spaces
anymore
* [QTBUG-77059](https://bugreports.qt.io/browse/QTBUG-77059) QStorageInfo::mountedVolumes() doesn't list volumes
mounted after "docker overlay volumes"
* [QTBUG-128855](https://bugreports.qt.io/browse/QTBUG-128855) Wasam drag and drop of a smaller file gives zero byte
* [QTBUG-129118](https://bugreports.qt.io/browse/QTBUG-129118) "DirectWrite: CreateFontFaceFromHDC() failed" Qt
warnigns
* [QTBUG-129023](https://bugreports.qt.io/browse/QTBUG-129023) tst_QWindow::windowExposedAfterReparent() failed on
Ubuntu 24.04 GNOME X11
* [QTBUG-129029](https://bugreports.qt.io/browse/QTBUG-129029) tst_QComboBox:popupPositionAfterStyleChange() failed on
Ubuntu 24.04 GNOME X11
* [QTBUG-129026](https://bugreports.qt.io/browse/QTBUG-129026) tst_QWidget_window::setWindowState(Qt::WindowMaximized)
failed on Ubuntu 24.04 GNOME X11
* [QTBUG-129027](https://bugreports.qt.io/browse/QTBUG-129027) tst_QStatusBar::QTBUG4334_hiddenOnMaximizedWindow()
failed on Ubuntu 24.04 GNOME X11
* [QTBUG-125323](https://bugreports.qt.io/browse/QTBUG-125323) Android Keyboard hides QML Text Edit Box
* [QTBUG-125053](https://bugreports.qt.io/browse/QTBUG-125053) QAbstractListModel fails to populate QML model
* [QTBUG-127340](https://bugreports.qt.io/browse/QTBUG-127340) [Reg 6.7->6.8] Wrong item count in ListView/Repeater
* [QTBUG-128660](https://bugreports.qt.io/browse/QTBUG-128660) QScreen::availableGeometry().topLeft() is wrong for
high-DPI displays
* [QTBUG-129567](https://bugreports.qt.io/browse/QTBUG-129567) tst_QWidget_window::tst_dnd_events() timeout on Ubuntu
24.04 GNOME X11
* [QTBUG-129568](https://bugreports.qt.io/browse/QTBUG-129568) tst_QWidget_window::mouseMoveWithPopup() failed on
Ubuntu 24.04 GNOME X11
* [QTBUG-129292](https://bugreports.qt.io/browse/QTBUG-129292) tst_QWindowContainer::testFocus() failed on GNOME
Wayland(Ubuntu 24.04 and 22.04)
* [QTBUG-129361](https://bugreports.qt.io/browse/QTBUG-129361) tst_QSizeGrip::hideAndShowOnWindowStateChange() failed
on Ubuntu 24.04 GNOME Wayland
* [QTBUG-118231](https://bugreports.qt.io/browse/QTBUG-118231) Android app 'pause' or 'screen-off' causes
'eglSwapBuffers failed' and various logcat errors
* [QTBUG-120238](https://bugreports.qt.io/browse/QTBUG-120238) Android 14 predictive text is broken for Gboard (on
target)
* [QTBUG-107185](https://bugreports.qt.io/browse/QTBUG-107185) Some tests appear to be re-testing the exact same data
tag
* [QTBUG-28246](https://bugreports.qt.io/browse/QTBUG-28246) QFileSystemEngine::isCaseSensitive() is hardcoded to
return false on Windows and true on Unix
* [QTBUG-31103](https://bugreports.qt.io/browse/QTBUG-31103) QFileSystemModel need to better case insensitivity
support
* [QTBUG-129516](https://bugreports.qt.io/browse/QTBUG-129516) tst_QAIV::testDialogAsEditor is flaky on Linux/X11
* [QTBUG-69423](https://bugreports.qt.io/browse/QTBUG-69423) QRandomGenerator not random on certain Windows
installations
* [QTBUG-129735](https://bugreports.qt.io/browse/QTBUG-129735) Selenium tests flaky on CI
* [QTBUG-96513](https://bugreports.qt.io/browse/QTBUG-96513) CI: qmake examples should not be built from tainted
source tree
* [QTBUG-128510](https://bugreports.qt.io/browse/QTBUG-128510) qtest: watchdog doesn't catch timeouts in initTestCase
and friends
* [QTBUG-129849](https://bugreports.qt.io/browse/QTBUG-129849) REG: Possible memory leak in DirectWrite font database
* [QTBUG-121822](https://bugreports.qt.io/browse/QTBUG-121822) WASM Clang++ ignores EXCEPTIONS settings in asyncify
config
* [QTBUG-123711](https://bugreports.qt.io/browse/QTBUG-123711) QtQuickView doesn't handle recreation of Activity
properly
* [QTBUG-111336](https://bugreports.qt.io/browse/QTBUG-111336) [REG 6.3->6.4]
qtdeclarative/examples/quick/pointerhandlers/tabletCanvasDrawing.qml got
broken again
* [QTBUG-129998](https://bugreports.qt.io/browse/QTBUG-129998) synthesis of mouse events after unaccepted QTabletEvents
doesn't work on some platforms
* [QTBUG-129839](https://bugreports.qt.io/browse/QTBUG-129839) 6.8: Programmatically resized window stalls for initial
part of resize animation
* [QTBUG-114987](https://bugreports.qt.io/browse/QTBUG-114987) tst_QGraphicsView::scrollBarRanges(motif, 3 x2) and many
others with QtWayland failed on Ubuntu 22.04, GNOME
* [QTBUG-130038](https://bugreports.qt.io/browse/QTBUG-130038) DBus: Sending a QVariantMap with null QVariant can crash
the application
* [QTCREATORBUG-28838](https://bugreports.qt.io/browse/QTCREATORBUG-28838) QtC indentation hickup on enable_if_t<LHS < RHS>
in template-initializer
* [QTBUG-130613](https://bugreports.qt.io/browse/QTBUG-130613) Documentation of Q_GLOBAL_STATIC(MyType, staticType) is
confusing
* [QTBUG-93625](https://bugreports.qt.io/browse/QTBUG-93625) qt_internal_add_test doesn't call qt_import_qml_plugins
* [QTBUG-122109](https://bugreports.qt.io/browse/QTBUG-122109) QTreeWidget's columns do not seem to resize properly
after upgrading from Qt6.5.3 to Qt6.1.1
* [QTBUG-123154](https://bugreports.qt.io/browse/QTBUG-123154) Applying stylesheet resets column and row size
configurations on Qt 6.5.4
* [QTBUG-52507](https://bugreports.qt.io/browse/QTBUG-52507) Wrong menu position for QToolButton placed on a scene
* [QTBUG-130500](https://bugreports.qt.io/browse/QTBUG-130500) Various network tests are failing on macOS 15
* [QTBUG-129944](https://bugreports.qt.io/browse/QTBUG-129944) A "strong assertion" does not help safely exclude
android.permission.ACCESS_FINE_LOCATION from manifest
* [QTBUG-126608](https://bugreports.qt.io/browse/QTBUG-126608) QRhi pipeline cache is never written for applications
terminated forcibly without running cleanup for Quick/QWindow/QGuiApp
* [QTBUG-130932](https://bugreports.qt.io/browse/QTBUG-130932) Top flaky test:
tst_QAbstractItemView::testDialogAsEditor
* [QTBUG-130743](https://bugreports.qt.io/browse/QTBUG-130743) tst_QTreeView::taskQTBUG_8376 tests fails CI on VxWorks
* [QTBUG-130742](https://bugreports.qt.io/browse/QTBUG-130742) tst_QPrinter::taskQTBUG4497_reusePrinterOnDifferentFiles
fails CI on VxWorks
* [QTBUG-130738](https://bugreports.qt.io/browse/QTBUG-130738) tst_QFont::familyNameWithCommaQuote fails CI on VxWorks
* [QTBUG-130740](https://bugreports.qt.io/browse/QTBUG-130740) tst_QNetworkReply tests fail CI on VxWorks
* [QTBUG-99563](https://bugreports.qt.io/browse/QTBUG-99563) The QMutable*Event construct is Undefined Behaviour
* [QTBUG-130118](https://bugreports.qt.io/browse/QTBUG-130118) [REG: 6.7 -> 6.8] psql: querying pg_timezone_names now
gives 00:00:00 offsets
* [QTBUG-127174](https://bugreports.qt.io/browse/QTBUG-127174) protobuf scalar types stop working if registered using
QML_USING
* [QTBUG-130736](https://bugreports.qt.io/browse/QTBUG-130736) tst_QApplication fails on CI with VxWorks
* [QTBUG-131343](https://bugreports.qt.io/browse/QTBUG-131343) Crash in QXcbScreen::setMonitor() via KDE/xembed-sni-
proxy
* [QTBUG-131362](https://bugreports.qt.io/browse/QTBUG-131362) tst_QLineEdit::testQuickSelectionWithMouse test fails
due to XPASS on VxWorks
* [QTBUG-99063](https://bugreports.qt.io/browse/QTBUG-99063) static top-level developer configuration fails in
qtdeclarative doc snippet
* [QTBUG-131484](https://bugreports.qt.io/browse/QTBUG-131484) Fix links to QIODeviceBase::OpenMode flags
* [QTBUG-128914](https://bugreports.qt.io/browse/QTBUG-128914) Many examples fail to build when "Build via Junction
Points" is enabled in Qt Creator
* [QTBUG-94708](https://bugreports.qt.io/browse/QTBUG-94708) qCDebug() and friends could pass the category as a tag in
Android
* [QTBUG-131653](https://bugreports.qt.io/browse/QTBUG-131653) Race condition between androiddeployqt runs for apk and
aab package builds
* [QTBUG-131477](https://bugreports.qt.io/browse/QTBUG-131477) Review SBOM generation and documentation to include
third party components
* [QTBUG-120604](https://bugreports.qt.io/browse/QTBUG-120604) Custom sort/filter model example - The arrow on the
magnifying glass is too high
* [QTBUG-64941](https://bugreports.qt.io/browse/QTBUG-64941) QTimeZone parses zone.tab, which is for backwards
compatibility
* [QTBUG-112898](https://bugreports.qt.io/browse/QTBUG-112898) i letter should be İ in uppercase in Turkish
* [QTBUG-131745](https://bugreports.qt.io/browse/QTBUG-131745) Emscripten 3.1.70 linker runs out of memory in CI
* [QTBUG-131842](https://bugreports.qt.io/browse/QTBUG-131842) Qt's CSS parser doesn't eat unquoted URL strings with
query
* [QTBUG-128893](https://bugreports.qt.io/browse/QTBUG-128893) sbom for qtpdf gets lost , as it ends up as qtwebengine
sbom
* [QTBUG-132072](https://bugreports.qt.io/browse/QTBUG-132072) QWidget::mapTo() crashed!
* [QTBUG-132114](https://bugreports.qt.io/browse/QTBUG-132114) qtbase/fe6dda9bb9310878b408b2421f60acb7135bd8ba breaks
-unity-build
* [QTBUG-132051](https://bugreports.qt.io/browse/QTBUG-132051) Converting a QImage to an opaque format does not always
reset the alpha
* [QTBUG-130313](https://bugreports.qt.io/browse/QTBUG-130313) Garbage text output
* [QTBUG-128900](https://bugreports.qt.io/browse/QTBUG-128900) macOS 15 deployment target build failure due to obsolete
API 'CGDisplayCreateImageForRect'
* [QTBUG-132102](https://bugreports.qt.io/browse/QTBUG-132102) Windows: Fusion style: Combo-box list: Item with icon
and long text sometimes has elide
* [QTBUG-132187](https://bugreports.qt.io/browse/QTBUG-132187) QDrawUtil: qDrawPlainRoundedRect does not work well for
high-dpi screens
* [QTBUG-132277](https://bugreports.qt.io/browse/QTBUG-132277) Qt fails to adhere to HTTP/2 HPACK dynamic table size
changes
* [QTBUG-132244](https://bugreports.qt.io/browse/QTBUG-132244) SQLite not found in qttools when building system SQLite
in Windows
* [QTBUG-132261](https://bugreports.qt.io/browse/QTBUG-132261) Many minor styling issues on windows 11
* [QTBUG-131887](https://bugreports.qt.io/browse/QTBUG-131887) [Boot to Qt 6.9.0 snapshot] jetson-agx-orin cannot start
qtlauncher
* [QTBUG-132507](https://bugreports.qt.io/browse/QTBUG-132507) Fix review findings in QUniqueHandle
* [QTBUG-119490](https://bugreports.qt.io/browse/QTBUG-119490) qcocoaapplicationdelegate.mm:354:20: error: cannot
initialize return object of type 'BOOL'
* [QTBUG-132459](https://bugreports.qt.io/browse/QTBUG-132459) Windows11 style: QProgressBar needs some work
* [QTBUG-131585](https://bugreports.qt.io/browse/QTBUG-131585) The QTreeWidget is painting poorly when the frame style
is set to QFrame::Plain | QFrame::Box when using Windows 11 style.
* [QTBUG-131377](https://bugreports.qt.io/browse/QTBUG-131377) Include Chromium in SBOM
* [QTBUG-12673](https://bugreports.qt.io/browse/QTBUG-12673) Crash in QWidgetPrivate::init on QApplication::quit()
using a modal dialog on Mac
* [QTBUG-132433](https://bugreports.qt.io/browse/QTBUG-132433) Windows 11 style - QToolButton/QPushButton quirks
* [QTBUG-127777](https://bugreports.qt.io/browse/QTBUG-127777) doc deprecates both ways to open a modal dialog
* [QTBUG-132785](https://bugreports.qt.io/browse/QTBUG-132785) QFile::rename() deletes file and fails to rename on
Windows/NFS
* [QTBUG-132646](https://bugreports.qt.io/browse/QTBUG-132646) Add a variant of QTemporaryFile::rename() that
overwrites
* [QTBUG-131916](https://bugreports.qt.io/browse/QTBUG-131916) Quoting and QML files with white spaces in the path are
not supported in qmldir
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-133206](https://bugreports.qt.io/browse/QTBUG-133206) QThreadPrivate saying "QThreadStorage: Thread %p exited
after QThreadStorage %d destroyed"
* [QTBUG-129222](https://bugreports.qt.io/browse/QTBUG-129222) Sporadic segfault at getenv from pulseaudio during boot
* [QTBUG-114957](https://bugreports.qt.io/browse/QTBUG-114957) Clarify handling of FileDialog.nameFilter on Android
* [QTBUG-132070](https://bugreports.qt.io/browse/QTBUG-132070) Ubuntu 24.04 x64: Sometimes hundreds of tests failing
* [QTBUG-126827](https://bugreports.qt.io/browse/QTBUG-126827) Configuring a cmake-based Qt Quick project fails if the
path contains spaces
* [QTBUG-35598](https://bugreports.qt.io/browse/QTBUG-35598) QtQuick Controls TextField and TextArea miss mouse
context menu
* [QTBUG-30133](https://bugreports.qt.io/browse/QTBUG-30133) QScroller auto-test is flakey
* [QTBUG-107893](https://bugreports.qt.io/browse/QTBUG-107893) cmake: multi-ABI Android builds do not forward cmake
arguments
* [QTBUG-132633](https://bugreports.qt.io/browse/QTBUG-132633) QDir::mkpath() is missing an overload with permissions
* [QTBUG-106025](https://bugreports.qt.io/browse/QTBUG-106025) REG: isSignalConnected creates a dead lock.
* [QTBUG-133805](https://bugreports.qt.io/browse/QTBUG-133805) QFileDialog shouldn't write to QtProject.conf
* [QAA-2836](https://bugreports.qt.io/browse/QAA-2836) Make sure that all references to "Qt Android" are changed to
"Qt for Android"
* [QTBUG-134105](https://bugreports.qt.io/browse/QTBUG-134105) tst_qscroller::overshoot() is flaky on macOS
* [QTBUG-133761](https://bugreports.qt.io/browse/QTBUG-133761) Update Qt Creator help mode colours to match the current
themes
* [QTBUG-133882](https://bugreports.qt.io/browse/QTBUG-133882) Polish string types overview
* [QTBUG-134250](https://bugreports.qt.io/browse/QTBUG-134250) qdoc fails to report warnings for incorrect \fn
signatures
* [QTBUG-135044](https://bugreports.qt.io/browse/QTBUG-135044) tst_QStringApiSymmetry fails under ASAN
(GenerationalCollator is leaked?)

### qtsvg
* [QTBUG-128583](https://bugreports.qt.io/browse/QTBUG-128583) Regression in QtSvgTinyDocument: Runtime warnings logged
to the console
* [QTBUG-53759](https://bugreports.qt.io/browse/QTBUG-53759) Qt svg icon engine does not support multiple png icons
* [QTBUG-122310](https://bugreports.qt.io/browse/QTBUG-122310) SVG Rendering with opacity on group not consistent with
other viewers
* [QTBUG-88265](https://bugreports.qt.io/browse/QTBUG-88265) QSvgGenerator QImage QBrush Not Work
* [QTBUG-131335](https://bugreports.qt.io/browse/QTBUG-131335) ubuntu-24.04-x86-static-qtlite build fails with Qt SVG
* [QTBUG-132468](https://bugreports.qt.io/browse/QTBUG-132468) Polyline with stroke displays nothing when all points
are the same
* [QTBUG-67692](https://bugreports.qt.io/browse/QTBUG-67692) Clash with Qt's internal logging categories when building
project with a static build of Qt
* [QTBUG-126486](https://bugreports.qt.io/browse/QTBUG-126486) Multiple Issues with bounding box in QtSvg
* [QTBUG-118877](https://bugreports.qt.io/browse/QTBUG-118877) -qreal float configuration option does not compile
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtdeclarative
* [QTBUG-125961](https://bugreports.qt.io/browse/QTBUG-125961) Built AAR has SDK version mismatch with Embedded QML
example
* [QTBUG-126011](https://bugreports.qt.io/browse/QTBUG-126011) shared_qml_module (Failed)
* [QTBUG-125765](https://bugreports.qt.io/browse/QTBUG-125765) QML builtins are linked into user binaries
* [QTBUG-125879](https://bugreports.qt.io/browse/QTBUG-125879) ASSERT in qmlls
* [QTBUG-124461](https://bugreports.qt.io/browse/QTBUG-124461) qmlls does not exit after receiving an exit request
* [QTBUG-123361](https://bugreports.qt.io/browse/QTBUG-123361) Providing stable A11y identifier for reliable UI tests
* [QTBUG-76809](https://bugreports.qt.io/browse/QTBUG-76809) QML accessibility does not take into account the Item's
scale property
* [QTBUG-125864](https://bugreports.qt.io/browse/QTBUG-125864) Broken rendering with curve renderer in Shapes example
* [QTBUG-125914](https://bugreports.qt.io/browse/QTBUG-125914) Formatting qml code containing an enum with qmlformat
removes enum values
* [QTBUG-125529](https://bugreports.qt.io/browse/QTBUG-125529) Lancelot baseline mismatch in Qt Quick's ComboBox using
Basic style
* [QTBUG-125495](https://bugreports.qt.io/browse/QTBUG-125495) Can't read styleName property from font singleton
* [QTBUG-122658](https://bugreports.qt.io/browse/QTBUG-122658) ListView crashes when `reuseitems` is set after
`positionViewAtIndex`
* [QTBUG-124624](https://bugreports.qt.io/browse/QTBUG-124624) Online documentation doesn't explain how to set dark
theme of Fusion style
* [QTBUG-125720](https://bugreports.qt.io/browse/QTBUG-125720) Typo in example code in QQuickRhiItem documentation
* [QTBUG-119647](https://bugreports.qt.io/browse/QTBUG-119647) [Tests] Warnings in
qtdeclarative/tests/auto/quickcontrols/controls/data/tst_tumbler.qml
* [QTBUG-125725](https://bugreports.qt.io/browse/QTBUG-125725) QQuickControl::focusReasonChanged does not work properly
* [QTBUG-126094](https://bugreports.qt.io/browse/QTBUG-126094) Spelling of Qt Qml/QML very inconsistent
* [QTBUG-126267](https://bugreports.qt.io/browse/QTBUG-126267) QQuickTextDocument::setTextDocument disables TextEdit
* [QTBUG-125157](https://bugreports.qt.io/browse/QTBUG-125157) Clarify the snippet about Editing Cells in a TableView
* [QTBUG-126124](https://bugreports.qt.io/browse/QTBUG-126124) Material style Button has extra padding when text
property has a value but display is IconOnly
* [QTBUG-126039](https://bugreports.qt.io/browse/QTBUG-126039) Dragging HeaderView works even when the mouse event is
accepted by a MouseArea inside an (header) cell
* [QTBUG-112320](https://bugreports.qt.io/browse/QTBUG-112320) javascript engine:  Proxy handler.get() doesn't work on
field 'name'
* [QTBUG-126127](https://bugreports.qt.io/browse/QTBUG-126127) Same file twice in sources, lower and upper case first
letter
* [QTBUG-115856](https://bugreports.qt.io/browse/QTBUG-115856) Don't let qmllint warnings fail the build
* [QTBUG-118165](https://bugreports.qt.io/browse/QTBUG-118165) qmlTypeId() causes QML_ELEMENTs to not be registered
* [QTBUG-124744](https://bugreports.qt.io/browse/QTBUG-124744) [Reg 6.7.0 -> dev] Bindings on width/height of
ApplicationWindow.background are not respected
* [QTBUG-
126375](https://bugreports.qt.io/browse/QTBUG-126375) tst_QQuickFontDialogImpl::settingUnderlineAndStrikeoutEffects is
flaky
* [QTBUG-122998](https://bugreports.qt.io/browse/QTBUG-122998) Crash in QQuickItemView through recursive item release
* [QTBUG-123527](https://bugreports.qt.io/browse/QTBUG-123527) Unchecked Fusion style RadioButtons / CheckBoxes are
barely visible in dark mode
* [QTBUG-125481](https://bugreports.qt.io/browse/QTBUG-125481) [Reg 6.7.0->6.7.1] Combination of Quick Layouts broken
* [QTBUG-126136](https://bugreports.qt.io/browse/QTBUG-126136) QML signal to C++ slot connection nonfunctional if
declared within the C++ object with the slot
* [QTBUG-125224](https://bugreports.qt.io/browse/QTBUG-125224) Cannot stop animation if it was restarted before the
last loop completed
* [QTBUG-126175](https://bugreports.qt.io/browse/QTBUG-126175) tst_QQuickPopup::popupWindowChangingParent is flaky
* [QTBUG-124572](https://bugreports.qt.io/browse/QTBUG-124572) Program crash when using a specific glyph from a popular
font file on Linux
* [QTBUG-119866](https://bugreports.qt.io/browse/QTBUG-119866) TapHandler is used in most of the code snippet of
DragHandler
* [QTBUG-120216](https://bugreports.qt.io/browse/QTBUG-120216) QQmlThread causes linker errors with USBan by using
unexported class QThreadPrivate
* [QTBUG-126057](https://bugreports.qt.io/browse/QTBUG-126057) Item state change reverts item's scaled size
* [QTBUG-126512](https://bugreports.qt.io/browse/QTBUG-126512) Controls styles use Qt.styleHints even though
documentation advises against it
* [QTBUG-126539](https://bugreports.qt.io/browse/QTBUG-126539) Native context menu shows every second time
* [QTBUG-126042](https://bugreports.qt.io/browse/QTBUG-126042) Nested ListView of orthogonal orientation gets stuck
without snapping using touchpad
* [QTBUG-126563](https://bugreports.qt.io/browse/QTBUG-126563) [Reg 6.5 -> 6.7] Anonymous function on a signal results
in QML Linter error when compiler warnings are enabled
* [QTBUG-126510](https://bugreports.qt.io/browse/QTBUG-126510) [REG 6.6 -> 6.7] Type error due to clash between JS and
Qml type names
* [QTBUG-126504](https://bugreports.qt.io/browse/QTBUG-126504) QML Nested Imports - some problems
* [QTBUG-126330](https://bugreports.qt.io/browse/QTBUG-126330) Crash when resizing ListView with reuseItems: true and
custom QQuickAsyncImageProvider
* [QTBUG-126628](https://bugreports.qt.io/browse/QTBUG-126628) QQuickAsyncImageProvider causes crash without Qt Network
(qml_network)
* [QTBUG-125906](https://bugreports.qt.io/browse/QTBUG-125906) Flicking needs to be done horizontally to delete items
in apps that have been rotated 90°.
* [QTBUG-30768](https://bugreports.qt.io/browse/QTBUG-30768) When an item in a ListView is snapped into place then it
does not take account for the section header
* [QTBUG-125611](https://bugreports.qt.io/browse/QTBUG-125611) Inconsistent QString::isNull behavior in
QJSEngine::evaluate result and QJSValue constructed from QString
* [QTBUG-126626](https://bugreports.qt.io/browse/QTBUG-126626) Hovered property stays when popup is opened from drawer
* [QTBUG-123894](https://bugreports.qt.io/browse/QTBUG-123894) Top flaky test: tst_qquicklistview::multipleTransitions
on MacOS_14 ARM64, MacOS_12 and MacOS_13
* [QTBUG-118903](https://bugreports.qt.io/browse/QTBUG-118903) Dragging ListView with Apple Pencil keeps items in
highlighted state
* [QTBUG-125526](https://bugreports.qt.io/browse/QTBUG-125526) [REG 6.6.3-6.7.0] TextEdit - warnings on loading
embedded QRC images
* [QTBUG-126396](https://bugreports.qt.io/browse/QTBUG-126396) Illegal memory access in QQuickShaderEffectPrivate
* [QTBUG-126673](https://bugreports.qt.io/browse/QTBUG-126673) [Regression 6.6 -> 6.7] Higher CPU utilization in large
QML applications
* [QTBUG-81231](https://bugreports.qt.io/browse/QTBUG-81231) QJSEngine and QStringList properties handling, a
potential performance issue
* [QTBUG-125095](https://bugreports.qt.io/browse/QTBUG-125095) [REG 6.2 → 6.5] Qt.binding fails with QtQObject inside
createObject
* [QTBUG-126834](https://bugreports.qt.io/browse/QTBUG-126834) [Reg 6.5 -> 6.6] Qml: Compiler generates wrong code for
Array.prototype.join invocation
* [QTBUG-125959](https://bugreports.qt.io/browse/QTBUG-125959) Cannot compile with qmltc when the type to compile
include a QML module that contains .hpp files
* [QTBUG-126398](https://bugreports.qt.io/browse/QTBUG-126398) Decide whether QV4::Sequence should be implicitly
convertable to QStringList
* [QTBUG-126676](https://bugreports.qt.io/browse/QTBUG-126676) qml lexer creates function tokens with wrong length
* [QTBUG-126712](https://bugreports.qt.io/browse/QTBUG-126712) qmlls: missing completions on QML module imports
* [QTBUG-126723](https://bugreports.qt.io/browse/QTBUG-126723) [REG 6.6 → 6.7] TableModel appendRow() no longer works.
* [QTBUG-123987](https://bugreports.qt.io/browse/QTBUG-123987) QML Popup "palette" property is not linking forward to
the proper palette docs
* [QTBUG-122963](https://bugreports.qt.io/browse/QTBUG-122963) Inconsistency in popup positioning logic
* [QTBUG-116442](https://bugreports.qt.io/browse/QTBUG-116442) Doubleclick sent to first item when single-clicking
alternating items
* [QTBUG-125053](https://bugreports.qt.io/browse/QTBUG-125053) QAbstractListModel fails to populate QML model
* [QTBUG-126711](https://bugreports.qt.io/browse/QTBUG-126711) qmlls: go to definition does not work on
ApplicationWindow
* [QTBUG-126714](https://bugreports.qt.io/browse/QTBUG-126714) qmlls: avoid psychedelic highlighting mode on invalid
code
* [QTBUG-125296](https://bugreports.qt.io/browse/QTBUG-125296) background color of TreeViewDelegate
* [QTBUG-127072](https://bugreports.qt.io/browse/QTBUG-127072) Timer QML type missing from documentation snapshots
* [QTBUG-126690](https://bugreports.qt.io/browse/QTBUG-126690) Creating dynamic properties and reparenting a Control
break bindings on Singletons
* [QTBUG-126819](https://bugreports.qt.io/browse/QTBUG-126819) Stroke width 0 is interpreted differently by the
QuickShape renderers
* [QTBUG-126782](https://bugreports.qt.io/browse/QTBUG-126782) Android build fails on
'qtdeclarative/src/quick/platform/android/qandroidviewsignalmanager.cpp'
* [QTBUG-126474](https://bugreports.qt.io/browse/QTBUG-126474) QQuickLayout Recursive Rearrange Locks Application
* [QTBUG-127166](https://bugreports.qt.io/browse/QTBUG-127166) Dimmer trying to be stacked before a top level popup
window
* [QTBUG-127009](https://bugreports.qt.io/browse/QTBUG-127009) Assert in QVariant possibly caused by mis-compilation
by qmlsc/qmlcachegen
* [QTBUG-127292](https://bugreports.qt.io/browse/QTBUG-127292) Failures on tst_qquicktextdocument
* [QTBUG-109880](https://bugreports.qt.io/browse/QTBUG-109880) Wrapper method that should create and return a
Javascript Generator object returns undefined
* [QTBUG-127092](https://bugreports.qt.io/browse/QTBUG-127092) When the URI starts with a numeric string,
qt_add_qml_module will generate erroneous code.
* [QTBUG-124412](https://bugreports.qt.io/browse/QTBUG-124412) qmllint warns about accessing highlightResizeDuration
etc from ListView attached property
* [QTBUG-127328](https://bugreports.qt.io/browse/QTBUG-127328) NinePatchImageSelector cannot use relative path for
source
* [QTBUG-127379](https://bugreports.qt.io/browse/QTBUG-127379) Service Embedding manual test doesn't build
* [QTBUG-106103](https://bugreports.qt.io/browse/QTBUG-106103) Deleting a Binding doesn't restore
* [QTBUG-127399](https://bugreports.qt.io/browse/QTBUG-127399) LayoutMirroring warning has typo
* [QTBUG-123191](https://bugreports.qt.io/browse/QTBUG-123191) Scenegraph nodes batching broken beginning with Qt 6.5.3
* [QTBUG-127169](https://bugreports.qt.io/browse/QTBUG-127169) Material style theme does not change when the system
theme changes
* [QTBUG-123861](https://bugreports.qt.io/browse/QTBUG-123861) Passing a string that contains a dot to
`QQmlComponent::createWithInitialProperties` will crash the application
* [QTBUG-126886](https://bugreports.qt.io/browse/QTBUG-126886) Setting format in QQuickTextDocument (TextArea) crashes
* [QTBUG-127273](https://bugreports.qt.io/browse/QTBUG-127273) [QNX 6.8.0 beta2] Do not try to use clipboard in
quickcontrols/spreadsheets on QNX - no support for it on the platform
* [QTBUG-127474](https://bugreports.qt.io/browse/QTBUG-127474) qmlls erases user code when updating implicitly defined
signal handlers
* [QTBUG-124498](https://bugreports.qt.io/browse/QTBUG-124498) qmltyperesolver can't handle ECMAScript resources
* [QTBUG-127067](https://bugreports.qt.io/browse/QTBUG-127067)  qml_in_android_view example project build error
* [QTBUG-125146](https://bugreports.qt.io/browse/QTBUG-125146) qmllint highlights wrong part in warning message
* [QTBUG-127309](https://bugreports.qt.io/browse/QTBUG-127309) qmllint: uses wrong category for  Property "xxx" has
incomplete type "Unregistered". You may be missing an import. [missing-
property]
* [QTBUG-127602](https://bugreports.qt.io/browse/QTBUG-127602) qmlls does not read .qmllint.ini
* [QTBUG-127619](https://bugreports.qt.io/browse/QTBUG-127619) FileDialog prints binding loop warning when opened.
* [QTBUG-127572](https://bugreports.qt.io/browse/QTBUG-127572) qtdeclarative/gallery example does not run for
webassembly
* [QTBUG-97557](https://bugreports.qt.io/browse/QTBUG-97557) Qt Quick batch rendering issue when a batch contain nodes
that have different index types
* [QTBUG-127703](https://bugreports.qt.io/browse/QTBUG-127703) tst_controls::RangeSlider::test_overlappingHandles()
failed on Ubuntu 24.04 offscreen
* [QTBUG-127700](https://bugreports.qt.io/browse/QTBUG-127700) tst_popup.qml::test_popupWithOverlayInLoader() crash
* [QTBUG-126616](https://bugreports.qt.io/browse/QTBUG-126616) CurveRendering artifacts drawing fonts
* [QTBUG-127016](https://bugreports.qt.io/browse/QTBUG-127016) Improve documentation for using a TreeModel in a Qt
Quick UI
* [QTBUG-127315](https://bugreports.qt.io/browse/QTBUG-127315) Tumbler's currentIndex is not the same as the initial
value
* [QTBUG-127727](https://bugreports.qt.io/browse/QTBUG-127727) tst_SoftwareRenderer::renderTarget fails
* [QTBUG-127330](https://bugreports.qt.io/browse/QTBUG-127330) QtCharts\plugins.qmltypes: Property object is missing a
name or type script binding.
* [QTBUG-124921](https://bugreports.qt.io/browse/QTBUG-124921) Tumbler's currentIndex is not working when the model is
changed at runtime
* [QTBUG-127687](https://bugreports.qt.io/browse/QTBUG-127687) qmlls does not print warning categories on warnings
* [QTBUG-127704](https://bugreports.qt.io/browse/QTBUG-127704) [REG: 6.6.2 → 6.7.2] QList<QObject *> argument causes
TypeError
* [QTBUG-124553](https://bugreports.qt.io/browse/QTBUG-124553) [Reg 5.15 -> 6.2] QML Binding is overwritten after
initialization
* [QTBUG-127458](https://bugreports.qt.io/browse/QTBUG-127458) qmlls fails to provide auto-completion for formal
parameters in signal handlers
* [QTBUG-127586](https://bugreports.qt.io/browse/QTBUG-127586) qmlls: wrong autocompletion on attached types
* [QTBUG-127609](https://bugreports.qt.io/browse/QTBUG-127609) qmlls: completion wrong for qualified imports
* [QTBUG-127519](https://bugreports.qt.io/browse/QTBUG-127519) CurveRenderer leaks SGNodes
* [QTBUG-118024](https://bugreports.qt.io/browse/QTBUG-118024) Still referenced objects are deleted during swap
operation between two ListModel instances
* [QTBUG-112638](https://bugreports.qt.io/browse/QTBUG-112638) Conflicting error message on compiling javascript
functions
* [QTBUG-124847](https://bugreports.qt.io/browse/QTBUG-124847) qsTr() documentation could also show how to use
disambiguation and plural forms
* [QTBUG-127782](https://bugreports.qt.io/browse/QTBUG-127782) Crash on Dragging Sections by Start Dragging Close to
the Border
* [QTBUG-124124](https://bugreports.qt.io/browse/QTBUG-124124) QtQuick MessageDialog: Fails on macOS when using
richtext
* [QTBUG-127865](https://bugreports.qt.io/browse/QTBUG-127865) Crash When Dragging Sections Between Different Header
Views
* [QTBUG-127650](https://bugreports.qt.io/browse/QTBUG-127650) Strange behaviours in QML warning, "Using attached type
<TYPE> already initialized in a parent scope"
* [QTBUG-125580](https://bugreports.qt.io/browse/QTBUG-125580) [Tests] Warnings in
tst_controls::Material::ComboBox::test_comboBoxWithShaderEffect()
* [QTBUG-126981](https://bugreports.qt.io/browse/QTBUG-126981) Application crashes with assert when closing the window
with TableView
* [QTBUG-127034](https://bugreports.qt.io/browse/QTBUG-127034) Qcolor Class / color QML value type cannot be copied via
HSL values
* [QTBUG-121449](https://bugreports.qt.io/browse/QTBUG-121449) The emojis are pixelated
* [QTBUG-123636](https://bugreports.qt.io/browse/QTBUG-123636) Crash when calling QWidget::setFixedSize with larger
values
* [QTBUG-124764](https://bugreports.qt.io/browse/QTBUG-124764) qt_add_lupdate adds extra location for QML files
* [QTBUG-127809](https://bugreports.qt.io/browse/QTBUG-127809) TableView forceLayout does not correct contentX/contentY
after columnWidth/rowHeight changed
* [QTBUG-125416](https://bugreports.qt.io/browse/QTBUG-125416) SwipeView shows all elements at once if it is 0x0 in
size
* [QTBUG-125630](https://bugreports.qt.io/browse/QTBUG-125630) TextInput.passwordMaskDelay does nothing if echoMode is
PasswordEchoOnEdit
* [QTBUG-127906](https://bugreports.qt.io/browse/QTBUG-127906) Qt.labs.platform.Menu opens at the wrong location with
scaling enabled
* [QTBUG-115759](https://bugreports.qt.io/browse/QTBUG-115759) Centering an element in Overlay results in visual
inconsistencies
* [QTBUG-126576](https://bugreports.qt.io/browse/QTBUG-126576) qmlls: automatic qmltypes generation is slowing
completions and highlighting down
* [QTBUG-127343](https://bugreports.qt.io/browse/QTBUG-127343) Incomplete and inconsistent type checking for QML lists
* [QTBUG-126514](https://bugreports.qt.io/browse/QTBUG-126514) [Regr: 6.5.0->6.7.1] Mouse wheel scrolling in nested
list views broken
* [QTBUG-114984](https://bugreports.qt.io/browse/QTBUG-114984) Software Renderer: Updating a layer-enabled subtree
while it is invisible produces wrong outcomes
* [QTBUG-128283](https://bugreports.qt.io/browse/QTBUG-128283) Memory leak after calling QQuickItem::grabToImage
* [QTBUG-127455](https://bugreports.qt.io/browse/QTBUG-127455) QML ListView crashes in
QQuickItemViewPrivate::itemGeometryChanged
* [QTBUG-127846](https://bugreports.qt.io/browse/QTBUG-127846) quickcontrols/spreadsheets not launching when installed
outside of build dir
* [QTBUG-127624](https://bugreports.qt.io/browse/QTBUG-127624) QML tools stop reporting unqualified access after the
first occurrence in a block
* [QTBUG-127613](https://bugreports.qt.io/browse/QTBUG-127613) Tumbler breaks when wrap value changes
* [QTBUG-120011](https://bugreports.qt.io/browse/QTBUG-120011) Qt Quick Controls Menu can appear at the wrong position
when DPI Awareness is enabled
* [QTBUG-128128](https://bugreports.qt.io/browse/QTBUG-128128) QML_ELEMENT exposes types of arguments of all slots in
.qmltypes-file
* [QTBUG-127442](https://bugreports.qt.io/browse/QTBUG-127442) REG[6.7 → 6.8]: generated qml type registration contains
invalid include paths
* [QTBUG-127440](https://bugreports.qt.io/browse/QTBUG-127440) QML TextField can't deselect by clicking on the text
field
* [QTBUG-10684](https://bugreports.qt.io/browse/QTBUG-10684) Interaction between text input and flickable is lacking
* [QTBUG-111504](https://bugreports.qt.io/browse/QTBUG-111504) Text loses selection when releasing long-press on
Android text input
* [QTBUG-116606](https://bugreports.qt.io/browse/QTBUG-116606) unable to deselect text in text input using touch
* [QTBUG-127049](https://bugreports.qt.io/browse/QTBUG-127049) Infinitely Recursvie Iterators Segfault process
* [QTBUG-126632](https://bugreports.qt.io/browse/QTBUG-126632) qmlimportscanner does not properly handle ../ in path
imports
* [QTBUG-80344](https://bugreports.qt.io/browse/QTBUG-80344) Button's icon blurry because of non-integer position
* [QTBUG-128344](https://bugreports.qt.io/browse/QTBUG-128344) ASSERT: "(populates && changedIndex == Accumulator &&
m_state.accumulatorOut().isValid()) || (!populates && changedIndex !=
Accumulator)"
* [QTBUG-110451](https://bugreports.qt.io/browse/QTBUG-110451) emitting dataChanged trips on freed delegate memory
* [QTBUG-123377](https://bugreports.qt.io/browse/QTBUG-123377) JS Set iteration does not follow spec
* [QTBUG-124731](https://bugreports.qt.io/browse/QTBUG-124731) grabPermissions: PointerHandler.TakeOverForbidden
conflicts with contentItem (or ItemDelegate) on iOS
* [QTBUG-123595](https://bugreports.qt.io/browse/QTBUG-123595) VerticalHeaderView / HorizontalHeaderView should always
use headerData() -- stale docs?
* [QTBUG-125995](https://bugreports.qt.io/browse/QTBUG-125995) Fix aotstats cmake support on Xcode
* [QTBUG-126858](https://bugreports.qt.io/browse/QTBUG-126858) Closing a popup with popupType set to PopupWindow calls
exit transition twice
* [QTBUG-128525](https://bugreports.qt.io/browse/QTBUG-128525) QML ComboBox closes on escape/back key release, not
press
* [QTBUG-126987](https://bugreports.qt.io/browse/QTBUG-126987) Setting combobox focus to false doesn't close it when
popupType is set to popupWindow
* [QTBUG-128605](https://bugreports.qt.io/browse/QTBUG-128605) The dependency target
"qtgraphicaleffectsplugin_qmltyperegistration" of target
"module_qtgraphicaleffectsplugin_aotstats_targets" does not exist.
* [QTBUG-128561](https://bugreports.qt.io/browse/QTBUG-128561) Crash when re-showing shape using CurveRenderer
* [QTCREATORBUG-31526](https://bugreports.qt.io/browse/QTCREATORBUG-31526) Missing QML dependency not included in qmllint
output in Issues pane
* [QTBUG-120061](https://bugreports.qt.io/browse/QTBUG-120061) Invalid QSGAbstractRenderer::setClearMode
* [QTBUG-126815](https://bugreports.qt.io/browse/QTBUG-126815) Action triggered callback has incorrect source when
popupType is set to PopupWindow
* [QTBUG-128611](https://bugreports.qt.io/browse/QTBUG-128611) Service Embedding manual test doesn't compile / crashes
* [QTBUG-126713](https://bugreports.qt.io/browse/QTBUG-126713) Attached style properties not propagating when popupType
is set to popup window
* [QTBUG-128645](https://bugreports.qt.io/browse/QTBUG-128645) Fix Windows ARM: QtDeclarative -
TestLinkStaticQmlModule::canRun
* [QTBUG-128586](https://bugreports.qt.io/browse/QTBUG-128586) Signals without arguments give false warnings in QML in
Android
* [QTBUG-127661](https://bugreports.qt.io/browse/QTBUG-127661) Creator jumps to auto generated file instead of the real
one
* [QTBUG-128272](https://bugreports.qt.io/browse/QTBUG-128272) New example quickcontrols\spreadsheets fails to compile
on MSVC2022 x64
* [QTBUG-128638](https://bugreports.qt.io/browse/QTBUG-128638) [Reg 6.7 -> 6.8] Crash when using live preview
* [QTBUG-128782](https://bugreports.qt.io/browse/QTBUG-128782) [Reg 6.7 -> 6.8] Crash when using live preview
* [QTBUG-128789](https://bugreports.qt.io/browse/QTBUG-128789) [Reg 6.6 -> 6.7] QML confuses types between engines
* [QTBUG-128931](https://bugreports.qt.io/browse/QTBUG-128931) Focus frame is never drawn inside QQuickWidget
* [QTBUG-128420](https://bugreports.qt.io/browse/QTBUG-128420) Qt 6.8 does not support build paths with white spaces
anymore
* [QTBUG-128860](https://bugreports.qt.io/browse/QTBUG-128860) Qt6QmlMacros doesn't handle build directories with
spaces in the path
* [QTBUG-128934](https://bugreports.qt.io/browse/QTBUG-128934) tst_qquicktableview::checkColumnRowResizeAfterReorder is
flaky
* [QTBUG-127308](https://bugreports.qt.io/browse/QTBUG-127308) [REG 6.6 → 6.8] qmlRestrictedType warning errorneously
triggers for enum class
* [QTBUG-118588](https://bugreports.qt.io/browse/QTBUG-118588) qmllint: Nondeterministic output when multiple files are
linted in one invocation
* [QTBUG-128444](https://bugreports.qt.io/browse/QTBUG-128444) Universal style theme does not change when the system
theme changes
* [QTBUG-129052](https://bugreports.qt.io/browse/QTBUG-129052) controls tests are flaky since https://codereview.qt-
project.org/c/qt/qtdeclarative/+/589582
* [QTBUG-129214](https://bugreports.qt.io/browse/QTBUG-129214) quick/quickwidgets/qmlpreviewer not compiling on Android
* [QTBUG-118898](https://bugreports.qt.io/browse/QTBUG-118898) Qmltyperegistrar ignores --namespace in --extract mode.
* [QTBUG-129194](https://bugreports.qt.io/browse/QTBUG-129194) qmllint segmentation fault in
QQmlSA::Element::internalId
* [QTBUG-129202](https://bugreports.qt.io/browse/QTBUG-129202) FAIL!  :
inputpanelcontrols::tst_inputpanelcontrols::test_worksWithModal()
* [QTBUG-128868](https://bugreports.qt.io/browse/QTBUG-128868) qmllint prints Warning: Ambiguous type detected.
XxxDialog is defined multiple times.
* [QTBUG-129281](https://bugreports.qt.io/browse/QTBUG-129281) Assert when trying to access SplitView handle from the
outside
* [QTBUG-124345](https://bugreports.qt.io/browse/QTBUG-124345) QML ObjectModel: Following the documentation for append
will lead to app crash
* [QTBUG-129323](https://bugreports.qt.io/browse/QTBUG-129323) QtQuickDialogs won't reopen when closed
* [QTBUG-123829](https://bugreports.qt.io/browse/QTBUG-123829) TreeView Documentation Code Example Displays Nothing
* [QTBUG-129329](https://bugreports.qt.io/browse/QTBUG-129329) QML Preview doesn't update properly
* [QTBUG-128637](https://bugreports.qt.io/browse/QTBUG-128637) race condition with async Shape(Path)
* [QTBUG-128445](https://bugreports.qt.io/browse/QTBUG-128445) anchors.mirrored is still documented
* [QTBUG-128500](https://bugreports.qt.io/browse/QTBUG-128500) The snippet in "Separating Tests from Application Logic"
leads to an error
* [QTBUG-129310](https://bugreports.qt.io/browse/QTBUG-129310) Possible garbage collector bug
* [QTBUG-85860](https://bugreports.qt.io/browse/QTBUG-85860) BusyIndicator in inconsistent state when running property
changed too fast
* [QTBUG-127340](https://bugreports.qt.io/browse/QTBUG-127340) [Reg 6.7->6.8] Wrong item count in ListView/Repeater
* [QTBUG-129500](https://bugreports.qt.io/browse/QTBUG-129500) QQuickItem::mapToItem() can segfault during
initalization
* [QTBUG-126784](https://bugreports.qt.io/browse/QTBUG-126784)  QQuickWindow::graphicsConfiguration() documentation
wrong
* [QTBUG-128875](https://bugreports.qt.io/browse/QTBUG-128875) [PDF] Zooming in and out the pdf file then opening
another one causes to app to crash
* [QTBUG-128158](https://bugreports.qt.io/browse/QTBUG-128158) Native Quick Menu emits signals in wrong order
* [QTBUG-119034](https://bugreports.qt.io/browse/QTBUG-119034) result of Item.mapToItem call is round to integer
* [QTBUG-129165](https://bugreports.qt.io/browse/QTBUG-129165) regression ListView not updating count
* [QTBUG-111336](https://bugreports.qt.io/browse/QTBUG-111336) [REG 6.3->6.4]
qtdeclarative/examples/quick/pointerhandlers/tabletCanvasDrawing.qml got
broken again
* [QTBUG-129196](https://bugreports.qt.io/browse/QTBUG-129196) QtQuick.tooling Module wants QtQml's Component instead
of QtQuick.tooling's
* [QTBUG-128895](https://bugreports.qt.io/browse/QTBUG-128895) [Reg 6.2 -> 6.5] QtQuick.Templates causes crashes if
QtQuick types are not registered
* [QTBUG-127833](https://bugreports.qt.io/browse/QTBUG-127833) Sign mismatches in QML language server
* [QTBUG-129797](https://bugreports.qt.io/browse/QTBUG-129797) qmlcachegen generates code that is incompatible with
QT_NO_CAST_FROM_ASCII
* [QTBUG-129766](https://bugreports.qt.io/browse/QTBUG-129766) Qt build fails with XCode 15.3 and 16
* [QTBUG-129182](https://bugreports.qt.io/browse/QTBUG-129182) tst_qquickwidget::tabKey() is flaky on dev
* [QTBUG-129599](https://bugreports.qt.io/browse/QTBUG-129599) ListView: ListView sometimes lags / pauses when dragging
it
* [QTBUG-129799](https://bugreports.qt.io/browse/QTBUG-129799) qmllint: typechecking 'Overlay' attached property fails
* [QTBUG-111770](https://bugreports.qt.io/browse/QTBUG-111770) Gauge control
* [QTBUG-129515](https://bugreports.qt.io/browse/QTBUG-129515) Double wrapped QML Settings don't save or load
* [QTBUG-129941](https://bugreports.qt.io/browse/QTBUG-129941) tst_declarative_ui (Failed)
* [QTBUG-129926](https://bugreports.qt.io/browse/QTBUG-129926) The documentation says "two properteis" but there are
four of them
* [QTBUG-129699](https://bugreports.qt.io/browse/QTBUG-129699) Crash in void
QQuickDeliveryAgentPrivate::clearFocusInScope when closing Application
* [QTBUG-128843](https://bugreports.qt.io/browse/QTBUG-128843) Crash when Qt QML is built with -ltcg flag
* [QTBUG-130080](https://bugreports.qt.io/browse/QTBUG-130080) "SourceProxy is not a type" when Qt is build statically
* [QTBUG-67168](https://bugreports.qt.io/browse/QTBUG-67168) DialogButtonBox.DestructiveRole doesn't close the dialog
* [QTBUG-130143](https://bugreports.qt.io/browse/QTBUG-130143) Crash in QQmlAbstractBinding::removeFromObject()
* [QTBUG-128820](https://bugreports.qt.io/browse/QTBUG-128820) qmllint doesn't see properties from base classes
* [QTBUG-129943](https://bugreports.qt.io/browse/QTBUG-129943) tst_PointHandler::tabletStylus is flaky
* [QTBUG-129947](https://bugreports.qt.io/browse/QTBUG-129947) tst_QQuickTextEdit::mouseSelection() is flaky on macOS
arm 12/13
* [QTBUG-129759](https://bugreports.qt.io/browse/QTBUG-129759) Document delegateModel of ComboBox
* [QTBUG-118691](https://bugreports.qt.io/browse/QTBUG-118691) tst_qquickpixmapcache::slowDevice is flaky
* [QTBUG-126090](https://bugreports.qt.io/browse/QTBUG-126090) tst_qquickpixmapcache::slowDeviceInterrupted fails on
macOS and qemu at least
* [QTBUG-130095](https://bugreports.qt.io/browse/QTBUG-130095) qmlprofiler doc is empty
* [QTBUG-130081](https://bugreports.qt.io/browse/QTBUG-130081) qmlcompiler generated code not compatible with
QT_NO_CAST_FROM_ASCII
* [QTBUG-130088](https://bugreports.qt.io/browse/QTBUG-130088) Crash in QQuickDeliveryAgentPrivate::clearHover
* [QTBUG-129681](https://bugreports.qt.io/browse/QTBUG-129681) QML imports break on UNC paths that contain `%` chars
* [QTBUG-129839](https://bugreports.qt.io/browse/QTBUG-129839) 6.8: Programmatically resized window stalls for initial
part of resize animation
* [QTBUG-124478](https://bugreports.qt.io/browse/QTBUG-124478) Qt6.5.1 QML - Scrolling issue when using a trackpad on
macOS when there are nested scroll areas
* [QTBUG-127776](https://bugreports.qt.io/browse/QTBUG-127776) Code completion for return types doesn't work
* [QTBUG-128932](https://bugreports.qt.io/browse/QTBUG-128932) qmllint disable does not work for missing-type?
* [QTBUG-118879](https://bugreports.qt.io/browse/QTBUG-118879) QML ListElement does not work with enums when "as"
import is used
* [QTBUG-104404](https://bugreports.qt.io/browse/QTBUG-104404) QQmlContext::nameForObject() with ApplicationWindow
causes creation of many QQuickScreenInfo objects
* [QTBUG-127065](https://bugreports.qt.io/browse/QTBUG-127065) Memory leak in Loader during debugging via QML debugger
* [QTBUG-128805](https://bugreports.qt.io/browse/QTBUG-128805) qmllint always deduces type of "this" to be "QObject"
* [QTBUG-127957](https://bugreports.qt.io/browse/QTBUG-127957) [Reg 6.5 -> 6.7] Reference/Value nature of lists is
inconsistent
* [QTBUG-129388](https://bugreports.qt.io/browse/QTBUG-129388) Compilation Units are not completely released on engine
destruction
* [QTBUG-122102](https://bugreports.qt.io/browse/QTBUG-122102) mprotect repeatedly fails and triggers SELinux AVC
alerts
* [QTBUG-129622](https://bugreports.qt.io/browse/QTBUG-129622) [Reg 6.7.2 -> 6.7.3] Crash in QQuickItem::setX
* [QTBUG-130360](https://bugreports.qt.io/browse/QTBUG-130360) [Reg] Button with action doesn't have accessible name if
the action doesn't set Accessible.name
* [QTBUG-130511](https://bugreports.qt.io/browse/QTBUG-130511) Xcode build fails: is attached to multiple targets
* [QTBUG-130358](https://bugreports.qt.io/browse/QTBUG-130358) qmllint: load plugins before processing commandline
parameters
* [QTBUG-130517](https://bugreports.qt.io/browse/QTBUG-130517) PinchHandler unexpectedly resets target's rotation even
if rotationAxis.enabled is false
* [QTBUG-130534](https://bugreports.qt.io/browse/QTBUG-130534)  libQt6QmlToolingSettings.a is required for user app
configure step
* [QTBUG-105488](https://bugreports.qt.io/browse/QTBUG-105488) ptest build to fail when QmlCompiler is used
* [QTBUG-120082](https://bugreports.qt.io/browse/QTBUG-120082) ListView: documentation of property `count` is unclear
* [QTBUG-119530](https://bugreports.qt.io/browse/QTBUG-119530) QML - screen reader reads twice the title of the
application
* [QTBUG-130331](https://bugreports.qt.io/browse/QTBUG-130331) Cannot use VirtualKeyboard when using several modal
Popup
* [QTBUG-129520](https://bugreports.qt.io/browse/QTBUG-129520) Click/mouseRelease signals are not received by a button
in a Popup if the InputPanel is placed in front of the Popup
* [QTBUG-130620](https://bugreports.qt.io/browse/QTBUG-130620) Drag: shows warning about sourceSize when using with
grabToImage()
* [QTBUG-130681](https://bugreports.qt.io/browse/QTBUG-130681) FAIL!  : tst_QQmlDebugTranslationService::verifyMissingA
llTranslationsForMissingLanguage() Compared values are not the same
* [QTBUG-130689](https://bugreports.qt.io/browse/QTBUG-130689) There are no  any QML Screen change notifications when
you change the MacBook display resolution
* [QTBUG-129939](https://bugreports.qt.io/browse/QTBUG-129939) [REG: 6.5->6.6] Validator fixup() is now always called
for every key press in SpinBox
* [QTBUG-130349](https://bugreports.qt.io/browse/QTBUG-130349) dom crashes when using nested functions
* [QTBUG-130522](https://bugreports.qt.io/browse/QTBUG-130522) QML_CONSTRUCTIBLE_VALUE misbehaves on constructors
taking QJSValue
* [QTBUG-128269](https://bugreports.qt.io/browse/QTBUG-128269) QQmlEngine destructor hangs on
QQmlTypeLoader::invalidate
* [QTBUG-122784](https://bugreports.qt.io/browse/QTBUG-122784) QtQuick: Unset required property in Singleton is not an
error?
* [QTBUG-113576](https://bugreports.qt.io/browse/QTBUG-113576) The wording in the documentation makes it confusing
* [QTBUG-130575](https://bugreports.qt.io/browse/QTBUG-130575) Javascript closure in QML does not directly capture
imported modules
* [QTBUG-122249](https://bugreports.qt.io/browse/QTBUG-122249) Remove transition with reuseItems leaves random gaps
* [QTBUG-107458](https://bugreports.qt.io/browse/QTBUG-107458) Reused items in GridView wrongly inherit properties
changed in remove transition
* [QTBUG-130087](https://bugreports.qt.io/browse/QTBUG-130087) QML Compiler statistics doesn't shows all modules
* [QTBUG-130084](https://bugreports.qt.io/browse/QTBUG-130084) QML Compiler statistics fail once a single module uses "
--only-bytecode"
* [QTBUG-130536](https://bugreports.qt.io/browse/QTBUG-130536) Disabled MenuItem propagates clicks to underlying mouse
area in drawer
* [QTBUG-130357](https://bugreports.qt.io/browse/QTBUG-130357) qmllint plugins: missing prefix in setting file keys
* [QTBUG-130820](https://bugreports.qt.io/browse/QTBUG-130820) Documentation for ComboBox find() Method has wrong
enumeration value MatchEndsWidth
* [QTBUG-128632](https://bugreports.qt.io/browse/QTBUG-128632) Incorrect qmllint warning about unresolved type
* [QTBUG-128577](https://bugreports.qt.io/browse/QTBUG-128577) Property "visible" of QML Item seems to affect how mouse
event is delivered
* [QTBUG-124634](https://bugreports.qt.io/browse/QTBUG-124634) QML Strict mode fails to compile inline object for
Qt.font call
* [QTBUG-130718](https://bugreports.qt.io/browse/QTBUG-130718) ERROR: The test executable probably crashed
* [QTBUG-130623](https://bugreports.qt.io/browse/QTBUG-130623) Windows: Resizing dialog with popupType: Popup.Window
shows weird behavior when resizing.
* [QTBUG-130880](https://bugreports.qt.io/browse/QTBUG-130880) QMLLS crashes repeatedly
* [QTBUG-130588](https://bugreports.qt.io/browse/QTBUG-130588) QuickEffectsPrivate should be discoverable with
find_package(Qt6 COMPONENTS QuickEffects REQUIRED) in CMakeLists.txt
* [QTBUG-130676](https://bugreports.qt.io/browse/QTBUG-130676) [Reg 6.7.2 -> 6.8.0] TextEdit.textChanged() signal is
emitted too frequently
* [QTBUG-130856](https://bugreports.qt.io/browse/QTBUG-130856) Calling replace() on QQuickWindow::data causes a crash
* [QTBUG-130867](https://bugreports.qt.io/browse/QTBUG-130867) QQmlComponent::loadFromModule() bug
* [QTBUG-130928](https://bugreports.qt.io/browse/QTBUG-130928) Spreadsheet example hangs when select and drag header
along with cell data
* [QTBUG-130900](https://bugreports.qt.io/browse/QTBUG-130900) Typo in Quick docs since 6.8
* [QTBUG-82058](https://bugreports.qt.io/browse/QTBUG-82058) tst_QQuickTextInput::setInputMask() is flaky on macOS
* [QTBUG-130839](https://bugreports.qt.io/browse/QTBUG-130839) [qmltc] Customizing Overlay.modal attached property
causes compilation errors
* [QTBUG-130838](https://bugreports.qt.io/browse/QTBUG-130838) [qmltc] Compilation errors when building a QML component
with aliased attached property
* [QTBUG-128935](https://bugreports.qt.io/browse/QTBUG-128935) Cannot dismiss QtQuick popups in QQuickWidget, misplaced
QQuickOverlay
* [QTBUG-130694](https://bugreports.qt.io/browse/QTBUG-130694) qmlls: code completion doesn't respect comments
* [QTBUG-130524](https://bugreports.qt.io/browse/QTBUG-130524) Error in qmldir file of Controls.Windows.imp
* [QTBUG-127538](https://bugreports.qt.io/browse/QTBUG-127538) Crash with Imagine style
* [QTBUG-126667](https://bugreports.qt.io/browse/QTBUG-126667) tst_QQuickPopup::popupWindowPositioning is flaky
* [QTBUG-130767](https://bugreports.qt.io/browse/QTBUG-130767) Incremental QML gc deletes context property
* [QTBUG-130974](https://bugreports.qt.io/browse/QTBUG-130974) A regular expression pattern gives unexpected results in
QML and QJSEngine.
* [QTBUG-127122](https://bugreports.qt.io/browse/QTBUG-127122) some MouseArea's signals are weirdly triggered
* [QTBUG-131263](https://bugreports.qt.io/browse/QTBUG-131263) FAIL!  : tst_qqmllanguage::retrieveQmlTypeId()
'qmlTypeId("testhelper", 1, 0, "PurelyDeclarativeSingleton") >= 0'
returned FALSE
* [QTBUG-34881](https://bugreports.qt.io/browse/QTBUG-34881) Flickable can have its flick incorrectly stolen
* [QTBUG-131291](https://bugreports.qt.io/browse/QTBUG-131291) heap-use-after-free in tst_qqmlenginedebugservice
* [QTBUG-131359](https://bugreports.qt.io/browse/QTBUG-131359) error: no template named 'qt_call_create_metaobjectdata'
in the global namespace
* [QTBUG-100069](https://bugreports.qt.io/browse/QTBUG-100069) TableView's 'Selecting items' doesn't support
DelegateChooser
* [QTBUG-125135](https://bugreports.qt.io/browse/QTBUG-125135) [Reg 6.5.3->6.5.4]Qml Popup component is not closing
anymore when instantiated via QQuickWidget.
* [QTBUG-112898](https://bugreports.qt.io/browse/QTBUG-112898) i letter should be İ in uppercase in Turkish
* [QTBUG-131594](https://bugreports.qt.io/browse/QTBUG-131594) qt/android/QtQuickView.java:23: error: unexpected end
tag
* [QTBUG-131394](https://bugreports.qt.io/browse/QTBUG-131394) Type assertions don't work properly for inline
components
* [QTBUG-101159](https://bugreports.qt.io/browse/QTBUG-101159) SelectionRectangle does work with TableView in Android
* [QTBUG-131633](https://bugreports.qt.io/browse/QTBUG-131633) QML Palette documentation is incomplete
* [QTBUG-120064](https://bugreports.qt.io/browse/QTBUG-120064) Clicking even on TextField vs Mousearea
* [QTBUG-129972](https://bugreports.qt.io/browse/QTBUG-129972) [REG 6.6 → 6.7] Array returned to QML from CPP is not
retaining changes made in QML/JS
* [QTBUG-130807](https://bugreports.qt.io/browse/QTBUG-130807) MouseArea::hoverEnabled property unexpectedly propagated
to child Controls.
* [QTBUG-93754](https://bugreports.qt.io/browse/QTBUG-93754) Qt Quick Controls Switch documentation does not state
clearly how to use the checked / not checked state
* [QTBUG-131098](https://bugreports.qt.io/browse/QTBUG-131098) TopLevel Dialogs can be obscured because they are
dynamically centered under their parent Window
* [QTBUG-131776](https://bugreports.qt.io/browse/QTBUG-131776) TableView: calling positionWithAtColumn when a syncView
is set, fails
* [QTBUG-129427](https://bugreports.qt.io/browse/QTBUG-129427) Focus frame causes items in a RowLayout to change
position when focus navigating
* [QTBUG-130266](https://bugreports.qt.io/browse/QTBUG-130266) WheelHandler documentation examples are written for tap
handler
* [QTBUG-131442](https://bugreports.qt.io/browse/QTBUG-131442) quickBeginDeferred: crash in combination with inline
components
* [QTBUG-131749](https://bugreports.qt.io/browse/QTBUG-131749) Incorrect strokeColor behaviour using property bindings
and CurveRenderer
* [QTBUG-131807](https://bugreports.qt.io/browse/QTBUG-131807) qmlls options incompatibility from 6.8 to 6.9
* [QTBUG-132050](https://bugreports.qt.io/browse/QTBUG-132050) [Reg 6.8 -> 6.9] Different behavior in QML regex
compared to javascript
* [QTBUG-131296](https://bugreports.qt.io/browse/QTBUG-131296) qmlls fails to parse some QML modules and C++ types when
there is more than one QML module in a directory
* [QTBUG-131958](https://bugreports.qt.io/browse/QTBUG-131958) qmlls: import warnings on wrong line
* [QTBUG-131980](https://bugreports.qt.io/browse/QTBUG-131980) [REG 6.5.4-6.8.1] Crash on value type property
initialization
* [QTCREATORBUG-31881](https://bugreports.qt.io/browse/QTCREATORBUG-31881) QML Control + Click opens debug file
* [QTBUG-131920](https://bugreports.qt.io/browse/QTBUG-131920) F2 shortcut in qml files leads to build dir instead of
source
* [QTBUG-128462](https://bugreports.qt.io/browse/QTBUG-128462) Qt Quick Dialog colors are wrong when switching themes
* [QTBUG-132071](https://bugreports.qt.io/browse/QTBUG-132071) QML Window Container: Tab Focus between parent and
embedded window doesn't work
* [QTBUG-129231](https://bugreports.qt.io/browse/QTBUG-129231) Sporadic crash on QQuickListViewPrivate::fixup()
* [QTBUG-131675](https://bugreports.qt.io/browse/QTBUG-131675) QML: Document "regexp" value type
* [QTBUG-131261](https://bugreports.qt.io/browse/QTBUG-131261) Use QML types Application QML Type documentation
* [QTBUG-132192](https://bugreports.qt.io/browse/QTBUG-132192) Item is not updated if it would be invisible under
software render
* [QTBUG-130328](https://bugreports.qt.io/browse/QTBUG-130328) the visual focus indicator of Button in FluentWinUI3
style doesn't work well with FocusScope
* [QTBUG-131961](https://bugreports.qt.io/browse/QTBUG-131961) Qml engine crashes when running SameValueZero
* [QTBUG-131957](https://bugreports.qt.io/browse/QTBUG-131957) [REG 6.8.0 → 6.8.1] QML applications crash on macOS 12
(x86)
* [QTBUG-132329](https://bugreports.qt.io/browse/QTBUG-132329) [Reg 6.8 -> 6.9] qmlcachegen miscompiles number
coercions
* [QTBUG-131774](https://bugreports.qt.io/browse/QTBUG-131774) [REG 5.15 → 6] remove warning on signal connect with no
arguments
* [QTBUG-127691](https://bugreports.qt.io/browse/QTBUG-127691) qmllint: don't print duplicate warnings
* [QTBUG-132421](https://bugreports.qt.io/browse/QTBUG-132421) cmake: Specifying PROJECT_VERSION in a Quick project
fails generation
* [QTBUG-132423](https://bugreports.qt.io/browse/QTBUG-132423) [Reg 6.2.13->6.5] qtquickcompiler.prf is missing from
cross-compiling kits, so "CONFIG += qtquickcompiler" no longer works
when cross-compiling
* [QTBUG-132355](https://bugreports.qt.io/browse/QTBUG-132355) Build failure with no-feature-quick-draganddrop option
* [QTBUG-129143](https://bugreports.qt.io/browse/QTBUG-129143) QML Text - Wrong implicitWidth
* [QTBUG-132499](https://bugreports.qt.io/browse/QTBUG-132499) assertion failure in callQObjectMethodAsVariant when
using qml cache
* [QTBUG-132528](https://bugreports.qt.io/browse/QTBUG-132528) qmlcompiler/qqmljscompilerstats_p.h", line 33: error
#276:  name followed by "::" must be a class or namespace name
* [QTBUG-132118](https://bugreports.qt.io/browse/QTBUG-132118) Crash when adding JS resources to a QML document
directory
* [QTBUG-132350](https://bugreports.qt.io/browse/QTBUG-132350) "QML debugging is enabled" warning is not guaranteed to
show at startup
* [QTBUG-132523](https://bugreports.qt.io/browse/QTBUG-132523) Null pointer dereference causing crash in QQuickPopup
* [QTBUG-132100](https://bugreports.qt.io/browse/QTBUG-132100) Foreign QObject with an enum type cannot be registered
for Qml in a nested namespace
* [QTBUG-132737](https://bugreports.qt.io/browse/QTBUG-132737) Freeze when scrolling testbench
* [QTBUG-132134](https://bugreports.qt.io/browse/QTBUG-132134) qmlls crashed
* [QTBUG-132792](https://bugreports.qt.io/browse/QTBUG-132792) qtabstractitemmodel_java settings.gradle has duplicate
information
* [QTBUG-132684](https://bugreports.qt.io/browse/QTBUG-132684) Using QT_TR_NOOP with disambiguation string in a
ListElement causes runtime error
* [QTBUG-132408](https://bugreports.qt.io/browse/QTBUG-132408) VectorImage transform replace animations sometimes wrong
* [QTBUG-132514](https://bugreports.qt.io/browse/QTBUG-132514) Fix navigation in Qml WorkerScript and XmlListModel
projects
* [QTBUG-132805](https://bugreports.qt.io/browse/QTBUG-132805) qmllint: default property
* [QTBUG-132783](https://bugreports.qt.io/browse/QTBUG-132783) [Reg 6.8.1 -> 6.9] qmllint: exec of regex
* [QTBUG-132553](https://bugreports.qt.io/browse/QTBUG-132553) ContextMenu docs are incomplete
* [QTBUG-131576](https://bugreports.qt.io/browse/QTBUG-131576) Dialog of QtQuick.Dialogs not valid
* [QTBUG-127294](https://bugreports.qt.io/browse/QTBUG-127294) qmllint: too many warnings when accessing an attached
type from a value type
* [QTBUG-128229](https://bugreports.qt.io/browse/QTBUG-128229) JavaScript library has cyclic dependeny on itself when
importing its own qml module
* [QTBUG-65463](https://bugreports.qt.io/browse/QTBUG-65463) ApplicationWindow.window attached property not available
due to component versioning
* [QTBUG-132921](https://bugreports.qt.io/browse/QTBUG-132921) Crash in QmlCacheGeneratedCode
* [QTBUG-133047](https://bugreports.qt.io/browse/QTBUG-133047) [Reg 6.5 -> 6.8] qmlsc: list<QtObject> property-of-a-
property is not bound correctly
* [QTBUG-132280](https://bugreports.qt.io/browse/QTBUG-132280) qmlformat: The optional chaining operator (JavaScript)
is incorrectly removed when followed by an array access
* [QTBUG-133230](https://bugreports.qt.io/browse/QTBUG-133230) Removed ShapePaths are still rendered
* [QTBUG-133231](https://bugreports.qt.io/browse/QTBUG-133231) Removing ShapePaths from Shape results in properties for
other shapes being confused
* [QTBUG-131386](https://bugreports.qt.io/browse/QTBUG-131386) qmlformat inserts a new space after block comment on
file save
* [QTBUG-133323](https://bugreports.qt.io/browse/QTBUG-133323) gcc 15: build error with src/qmldom/qqmldomtop.cpp
* [QTBUG-133398](https://bugreports.qt.io/browse/QTBUG-133398) qmlformat: Line-by-line formatter can't handle certain
property definitions
* [QTBUG-132065](https://bugreports.qt.io/browse/QTBUG-132065) qmlformat: 'From' properties confuses
IndentingLineWriter
* [QTBUG-133301](https://bugreports.qt.io/browse/QTBUG-133301) Crash when moving columns in an empty qml tableview
* [QTBUG-133052](https://bugreports.qt.io/browse/QTBUG-133052) modelData is lost when using a nested QML component
inside a Repeater
* [QTBUG-133129](https://bugreports.qt.io/browse/QTBUG-133129) DelegateModel can create delegates with unset required
properties in sub-objects
* [QTBUG-131903](https://bugreports.qt.io/browse/QTBUG-131903) Item.transform is not readonly
* [QTBUG-133053](https://bugreports.qt.io/browse/QTBUG-133053) [Reg 6.5 -> 6.8] Qt 6.8 silently removed sharing of
global variables between 2 typescript/javascript files
* [QTBUG-133526](https://bugreports.qt.io/browse/QTBUG-133526) Error: qmlcachegen inappropriately resolves file paths
* [QTBUG-130570](https://bugreports.qt.io/browse/QTBUG-130570) "Scene Graph - RHI Under QML" documentation error
* [QTBUG-133225](https://bugreports.qt.io/browse/QTBUG-133225) fix qmlformat cli option / settings file  precedence
* [QTBUG-133475](https://bugreports.qt.io/browse/QTBUG-133475) FAIL!  : tst_QQuickContextMenu::FluentWinUI3
* [QTBUG-133566](https://bugreports.qt.io/browse/QTBUG-133566) tst_qquickmenu::popup() is flaky
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
* [QTBUG-133380](https://bugreports.qt.io/browse/QTBUG-133380) FAIL!  : tst_QQuickMenu::FluentWinUI3::mouse(Popup.Item)
Compared values are not the same
* [QTBUG-133636](https://bugreports.qt.io/browse/QTBUG-133636) [Reg 6.7.3 -> 6.8.0] Qt StateMachine crashes during a
signal transition.
* [QTBUG-133481](https://bugreports.qt.io/browse/QTBUG-133481) Top-level configure fails with neumorphicpanel example
* [QTBUG-133483](https://bugreports.qt.io/browse/QTBUG-133483) qtquickview_java and _kotlin example QML Button signal
disconnect doesn't work
* [QTBUG-133276](https://bugreports.qt.io/browse/QTBUG-133276) qtquickview_kotlin doesn't compile
* [QTBUG-133493](https://bugreports.qt.io/browse/QTBUG-133493) Extra space in qtquickview_java example
* [QTBUG-123341](https://bugreports.qt.io/browse/QTBUG-123341) QML JavaScript function annotations not supported
* [QTBUG-132802](https://bugreports.qt.io/browse/QTBUG-132802) qtquickview_kotlin example source value 8 is obsolete
and will be removed in a future release
* [QTBUG-58643](https://bugreports.qt.io/browse/QTBUG-58643) QQmlListProperty has no examples of its usage
* [QTBUG-130705](https://bugreports.qt.io/browse/QTBUG-130705) QQmlListProperty is missing documentation for object /
data
* [QTBUG-119545](https://bugreports.qt.io/browse/QTBUG-119545) Document that the URL passed to Qt.createQmlObject() can
make it override existing components
* [QTBUG-133461](https://bugreports.qt.io/browse/QTBUG-133461) [REG: 6.6.1 → 6.8.2] Change to singleton status of Qt
* [QTBUG-133745](https://bugreports.qt.io/browse/QTBUG-133745) Link not shown correctly
* [QTBUG-89432](https://bugreports.qt.io/browse/QTBUG-89432) QML enum documentation should make a greater distinction
between using enums declared in C++ and declaring enums in QML
* [QTBUG-132409](https://bugreports.qt.io/browse/QTBUG-132409) QML registration macros are documented in QQmlEngine
* [QTBUG-133494](https://bugreports.qt.io/browse/QTBUG-133494) FTBFS: QtQuick DLL link error
* [QTBUG-133645](https://bugreports.qt.io/browse/QTBUG-133645) Curve renderer stroke is blurry inside Qt Quick 3D scene
* [QTBUG-133460](https://bugreports.qt.io/browse/QTBUG-133460) [REG: 6.7.2 → 6.8.2] Change in binding resolution
behavior
* [QTBUG-132765](https://bugreports.qt.io/browse/QTBUG-132765) Controls Overlay item bypasses window event delivery;
Drawer bypasses ContextMenu
* [QTBUG-132461](https://bugreports.qt.io/browse/QTBUG-132461) [REG 6.8 -> 6.9] QtQmlStatusChangeListener is not a
functional interface
* [QTBUG-134035](https://bugreports.qt.io/browse/QTBUG-134035) tst_qquickdeferred crashing
* [QTBUG-130370](https://bugreports.qt.io/browse/QTBUG-130370) Missing docs for QML_NAMESPACE_EXTENDED()
* [QTBUG-131002](https://bugreports.qt.io/browse/QTBUG-131002) Add a way to disable aotstats statistics file
generations
* [QTBUG-132602](https://bugreports.qt.io/browse/QTBUG-132602) [REG 6.8 -> 6.9]Crash when invoking `destroy` on self
* [QTBUG-133852](https://bugreports.qt.io/browse/QTBUG-133852) VectorImage: Scaled text elements have bad kerning
* [QTBUG-133587](https://bugreports.qt.io/browse/QTBUG-133587) Putting *.js file under QML_FILES and applying QTP0004
can break QML engine's ability to import module
* [QTBUG-35598](https://bugreports.qt.io/browse/QTBUG-35598) QtQuick Controls TextField and TextArea miss mouse
context menu
* [QTBUG-133302](https://bugreports.qt.io/browse/QTBUG-133302) ContextMenu opened on TextField sometimes closes
immediately
* [QTBUG-133492](https://bugreports.qt.io/browse/QTBUG-133492) Issue found on Qt 6.8 variant that doesn't exist on 6.6
* [QTBUG-134053](https://bugreports.qt.io/browse/QTBUG-134053) Doc: Remove duplicate paragraph in 'Menu QML Type' and
add missing ')'
* [QTBUG-130764](https://bugreports.qt.io/browse/QTBUG-130764) Affector does not have property "velocity"?
* [QTBUG-134043](https://bugreports.qt.io/browse/QTBUG-134043) tst_QQuickColorDialogImpl::dialogCanMoveBetweenWindows
is flaky
* [QTBUG-130291](https://bugreports.qt.io/browse/QTBUG-130291) QML "instanceof" and "as" fail with "QtQuick.url" type
* [QTBUG-134087](https://bugreports.qt.io/browse/QTBUG-134087) qtquickview_java QML button signal not connected when
starting example
* [QTBUG-133886](https://bugreports.qt.io/browse/QTBUG-133886) Regression in 6.9: Hover in ComboBox broken with
ApplicationWindow
* [QTBUG-134398](https://bugreports.qt.io/browse/QTBUG-134398) Qt Design Studio does not work with Qt 6.8 because of
QML caching
* [QTBUG-125585](https://bugreports.qt.io/browse/QTBUG-125585) Line spacing of many fonts is dramatically different
between Qt5 and Qt6
* [QTBUG-122031](https://bugreports.qt.io/browse/QTBUG-122031) tst_qquickapplication::state() is flaky on opensuse
* [QTBUG-75215](https://bugreports.qt.io/browse/QTBUG-75215) tst_qquickapplication::active() is flaky on opensuse
* [QTBUG-126184](https://bugreports.qt.io/browse/QTBUG-126184) tst_qquickwindow::visibilityDoesntClobberWindowState is
flaky
* [QTBUG-126047](https://bugreports.qt.io/browse/QTBUG-126047) tst_qquickpixmapcache::slowDevice crashes sporadically
* [QTBUG-88646](https://bugreports.qt.io/browse/QTBUG-88646) tst_qquicktext::contentSize() failed on msvc2019
developer build in CI
* [QTBUG-111766](https://bugreports.qt.io/browse/QTBUG-111766) qml issues in Effect Maker
* [QTBUG-124756](https://bugreports.qt.io/browse/QTBUG-124756) QQuickWindowContainer is not in the right child order
* [QTBUG-122415](https://bugreports.qt.io/browse/QTBUG-122415) Flickering when dragging a sub window
* [QTBUG-126222](https://bugreports.qt.io/browse/QTBUG-126222) tst_how_to_qml::activeFocusDebugging() fails often
* [QTBUG-125867](https://bugreports.qt.io/browse/QTBUG-125867) SelectionRectangle in Drag mode intercepts events even
when it should not
* [QTBUG-117526](https://bugreports.qt.io/browse/QTBUG-117526) QQuickStylePrivate::fallbackStyle has the wrong value
when using run-time style selection and the fallback style is imported
via the style's qmldir
* [QTBUG-126236](https://bugreports.qt.io/browse/QTBUG-126236) tst_controls::Basic::Action::test_repeater() fails on
linux and macos
* [QTBUG-67692](https://bugreports.qt.io/browse/QTBUG-67692) Clash with Qt's internal logging categories when building
project with a static build of Qt
* [QTBUG-125753](https://bugreports.qt.io/browse/QTBUG-125753) Fix PointRenderer series add/remove/visibility
* [QTBUG-68465](https://bugreports.qt.io/browse/QTBUG-68465) macOS: Accessibility: MenuItems are not accessible
* [QTBUG-112870](https://bugreports.qt.io/browse/QTBUG-112870) clang-tidy warnings on static global variables in moc
generated code
* [QTBUG-33017](https://bugreports.qt.io/browse/QTBUG-33017) [autotest] tst_qquickgridview tends to fail on win and
osx
* [QTBUG-88644](https://bugreports.qt.io/browse/QTBUG-88644) tst_QQuickGridView::snapToRow() failed on msvc2019
developer build in CI
* [QTBUG-126201](https://bugreports.qt.io/browse/QTBUG-126201) Qt examples output CMake warning about Qt policy QTP0004
* [QTBUG-124468](https://bugreports.qt.io/browse/QTBUG-124468) qmlpreview fails to load libworkerscriptplugin.so
* [QTBUG-126662](https://bugreports.qt.io/browse/QTBUG-126662) 2D Graphs: low performance on scrolling axis
* [QTBUG-126863](https://bugreports.qt.io/browse/QTBUG-126863) [REG 6.7->6.8]: Cannot read from attached
'Accessible.name' property
* [QTBUG-100020](https://bugreports.qt.io/browse/QTBUG-100020) tst_qqmljsscope fails on Android
* [QTBUG-126560](https://bugreports.qt.io/browse/QTBUG-126560) ListView's count property not updating when the ListView
is inside a Drawer and the model gets its data from a network request
* [QTBUG-89889](https://bugreports.qt.io/browse/QTBUG-89889) tst_QDateTime::systemTimeZoneChange fails on 32bit
systems
* [QTBUG-118109](https://bugreports.qt.io/browse/QTBUG-118109) qmllint: deferred-property-id logging category is muted
* [QTBUG-125589](https://bugreports.qt.io/browse/QTBUG-125589) weired console message with simple application
* [QTBUG-125571](https://bugreports.qt.io/browse/QTBUG-125571) YAnimator onRunningChanged can Qt.callLater(jsFunc) with
invalid scope object
* [QTBUG-125341](https://bugreports.qt.io/browse/QTBUG-125341) QML_CONSTRUCTIBLE_VALUE has a strange strategy to select
the right constructor
* [QTCREATORBUG-31102](https://bugreports.qt.io/browse/QTCREATORBUG-31102) qmlls syntax highlighting differs from the built
in one
* [QTBUG-127467](https://bugreports.qt.io/browse/QTBUG-127467) QtAbstractItemModel asserts when being rapidly modified
* [QTBUG-127756](https://bugreports.qt.io/browse/QTBUG-127756) Add support for popup window types in the how-to-qml
test
* [PYSIDE-2803](https://bugreports.qt.io/browse/PYSIDE-2803) pyside6-deploy throws a "command line is too long" error.
* [QTBUG-127562](https://bugreports.qt.io/browse/QTBUG-127562) qmllint wrongfully complains about tumbler attached
property
* [QTBUG-123491](https://bugreports.qt.io/browse/QTBUG-123491) qmlls memory leak
* [QTBUG-127848](https://bugreports.qt.io/browse/QTBUG-127848) QML embedding: qtabstractlistmodel_kotlin &
qtabstractitemmodel_java look off on low and high pixel density displays
* [QTBUG-124175](https://bugreports.qt.io/browse/QTBUG-124175) ListView sections don't work with a dot syntax (e.g.
"gadget.size") if using Q_GADGETs
* [QTBUG-124280](https://bugreports.qt.io/browse/QTBUG-124280) QML embedding example Java part doesn't look good on low
pixel densities
* [QTBUG-107493](https://bugreports.qt.io/browse/QTBUG-107493) Reword debug log messages for QML import statements
* [QTBUG-124922](https://bugreports.qt.io/browse/QTBUG-124922) The text in a TextEdit is not updated when
LayoutMirroring is enabled
* [QTBUG-128321](https://bugreports.qt.io/browse/QTBUG-128321) tst_QQuickPopup::Basic::popupWindowFocus() failed on
Ubuntu 24.04 arm64 offscreen
* [QTBUG-128173](https://bugreports.qt.io/browse/QTBUG-128173) Doc: Remove use of defunct QDoc command
"\tableofcontents"
* [QTBUG-96630](https://bugreports.qt.io/browse/QTBUG-96630) MenuItem mnemonic shortcut not triggered
* [QTBUG-128368](https://bugreports.qt.io/browse/QTBUG-128368) Make sure that also qt6_ CMake commands are in the help
index
* [QTBUG-127950](https://bugreports.qt.io/browse/QTBUG-127950) Qt policy QTP0004 is not set: You need qmldir files for
each extra  directory that contains .qml files for your module
* [QTBUG-127133](https://bugreports.qt.io/browse/QTBUG-127133) Why do I get warning "Multiple C++ types called xxx
found! This violates the One Definition Rule"
* [QTBUG-36525](https://bugreports.qt.io/browse/QTBUG-36525) Binding loop warning message does not give sufficient
information in order to fix it
* [QTBUG-122679](https://bugreports.qt.io/browse/QTBUG-122679) tst_how-to-qml timePicker is flaky
* [QTBUG-128606](https://bugreports.qt.io/browse/QTBUG-128606) CMake Error: The inter-target dependency graph contains
the following strongly connected component (cycle)
* [QTBUG-123396](https://bugreports.qt.io/browse/QTBUG-123396) MultiEffect shadowColor cannot be used for glow
* [QTBUG-126680](https://bugreports.qt.io/browse/QTBUG-126680) qmlls should know about implicit imports of nested QML
* [QTBUG-128417](https://bugreports.qt.io/browse/QTBUG-128417) Update QtGP version in examples & QtTAS
* [QTBUG-115140](https://bugreports.qt.io/browse/QTBUG-115140) qtdeclarative -unity-build-batch-size 100000 fails
* [QTBUG-129030](https://bugreports.qt.io/browse/QTBUG-129030) tst_qquickwindow::visibilityDoesntClobberWindowState()
failed on Ubuntu 24.04 GNOME X11
* [QTBUG-129032](https://bugreports.qt.io/browse/QTBUG-129032) tst_QQuickMultiPointTouchArea::nonOverlapping() and
nested() failed on Ubuntu 24.04 GNOME X11
* [QTBUG-82052](https://bugreports.qt.io/browse/QTBUG-82052) tst_QQuickTextEdit::linkHover() is flaky on macOS 10.14
* [QTBUG-128914](https://bugreports.qt.io/browse/QTBUG-128914) Many examples fail to build when "Build via Junction
Points" is enabled in Qt Creator
* [QTBUG-38004](https://bugreports.qt.io/browse/QTBUG-38004) Mac: When you have some TextInput fields in QML with
activeFocusOnTab set then it is not possible to tab to them
* [QTBUG-128126](https://bugreports.qt.io/browse/QTBUG-128126) Native Quick Menu opens in wrong location (Win)
* [QTBUG-129241](https://bugreports.qt.io/browse/QTBUG-129241) Crash at QV4::Value::as<T>
* [QTBUG-129301](https://bugreports.qt.io/browse/QTBUG-129301) QQmlMetaType::prettyTypeName sometimes returns non-
pretty name
* [QTBUG-127051](https://bugreports.qt.io/browse/QTBUG-127051) Language server doesn't provide hover documentation for
WebEngineView.url
* [QTBUG-128933](https://bugreports.qt.io/browse/QTBUG-128933) Allow to disable mouse panning in ScrollView
* [QTBUG-127422](https://bugreports.qt.io/browse/QTBUG-127422) Second QtQuickView doesn't work
* [QTBUG-123499](https://bugreports.qt.io/browse/QTBUG-123499) tst_MptaInterop::touchesThenPinch fails in Qt 6
* [QTBUG-129113](https://bugreports.qt.io/browse/QTBUG-129113) VxWorks undefined references due to link line
* [QTBUG-129737](https://bugreports.qt.io/browse/QTBUG-129737) Crash in tst_qqmlincubator
* [QTBUG-130582](https://bugreports.qt.io/browse/QTBUG-130582) [REG 6.7.3-6.8.0] MultiEffect with shadowOpacity looks
different than before
* [QTBUG-125631](https://bugreports.qt.io/browse/QTBUG-125631) [ios] Regression QMake -> CMake: slow build time due to
file copying and qmlcachegen
* [QTBUG-126205](https://bugreports.qt.io/browse/QTBUG-126205) CMake build takes 5x as long to build as qmake build
* [QTBUG-126671](https://bugreports.qt.io/browse/QTBUG-126671) NativeRendering renders nothing on Windows on ARM in
VMWare Fusion on Mac
* [QTBUG-130589](https://bugreports.qt.io/browse/QTBUG-130589) [Reg] TreeView editDelegate doesn't get positioned
correctly
* [QTCREATORBUG-31897](https://bugreports.qt.io/browse/QTCREATORBUG-31897) simplify qmlls setup / make it work out of the box
* [QTBUG-128221](https://bugreports.qt.io/browse/QTBUG-128221) [Reg 6.7.2->6.8.0b3] qmllint no longer fails when
warnings are found
* [QTBUG-127174](https://bugreports.qt.io/browse/QTBUG-127174) protobuf scalar types stop working if registered using
QML_USING
* [QTBUG-93625](https://bugreports.qt.io/browse/QTBUG-93625) qt_internal_add_test doesn't call qt_import_qml_plugins
* [QTBUG-130833](https://bugreports.qt.io/browse/QTBUG-130833) String '6.8.0' found in 6.9.0 sources
* [QTBUG-130991](https://bugreports.qt.io/browse/QTBUG-130991) 6.8.0: qtdeclarative examples build fail
* [QTBUG-123764](https://bugreports.qt.io/browse/QTBUG-123764) MessageDialog detailed text does not show in Fusion
style on dark mode
* [QTBUG-130893](https://bugreports.qt.io/browse/QTBUG-130893) ShapePath.fillItem doesn't work with all items; doesn't
scale correctly with QT_SCALE_FACTOR
* [QTBUG-126794](https://bugreports.qt.io/browse/QTBUG-126794) Crash with ListView of LayoutItemProxy
* [QTBUG-131487](https://bugreports.qt.io/browse/QTBUG-131487) QFileSystemModel does not work with QML DelegateModel
* [QTBUG-131288](https://bugreports.qt.io/browse/QTBUG-131288) Refine FileLocations::addRegion and make it reliable
* [QTBUG-98790](https://bugreports.qt.io/browse/QTBUG-98790) ChangeListeners get called even after being semi-deleted
* [QTBUG-129575](https://bugreports.qt.io/browse/QTBUG-129575)  Fix API flaw for QImage::mirror and QImage::mirrored
* [QTBUG-131702](https://bugreports.qt.io/browse/QTBUG-131702) qmlls sends an error when trying to stop on startup
* [QTBUG-131721](https://bugreports.qt.io/browse/QTBUG-131721) QML type loader thread has data races
* [QTBUG-95887](https://bugreports.qt.io/browse/QTBUG-95887) tst_FlickableInterop is flaky on opensuse
* [QTBUG-131906](https://bugreports.qt.io/browse/QTBUG-131906) FAIL!  :
tst_qqmlecmascript::componentCreation(invalidMode) Not all expected
messages were received
* [QTBUG-131898](https://bugreports.qt.io/browse/QTBUG-131898) Moving the window sometimes crashes the application
* [QTBUG-132075](https://bugreports.qt.io/browse/QTBUG-132075) tst_qquicktext::multilengthStrings(Wrap) Compared
doubles are not the same (fuzzy compare)
* [QTCREATORBUG-31823](https://bugreports.qt.io/browse/QTCREATORBUG-31823) Annotations and CodeCompletion is wrong or not
working
* [QTBUG-132345](https://bugreports.qt.io/browse/QTBUG-132345) [Reg 6.5 -> 6.8] qmlcachegen miscompiles number
coercions
* [QTBUG-132387](https://bugreports.qt.io/browse/QTBUG-132387) FAIL!  : tst_qqmlengine::uiLanguage() Not all expected
messages were received
* [QTBUG-132436](https://bugreports.qt.io/browse/QTBUG-132436) Context menu fails to open on Windows in CI
* [QTBUG-101704](https://bugreports.qt.io/browse/QTBUG-101704) ToolTip calculates its width incorrectly
* [QTBUG-132591](https://bugreports.qt.io/browse/QTBUG-132591) tst_QQmlInspector::connect(rectangle/unrestricted)
Received a fatal error
* [QTBUG-101678](https://bugreports.qt.io/browse/QTBUG-101678) tst_qqmlinspector (and other tests in
tests/auto/qml/debugger/) times out on macOS 12 (x86_64) in CI
* [QTBUG-101972](https://bugreports.qt.io/browse/QTBUG-101972) "Killed process: No output received (timeout: 15m0s
seconds)" when running tst_QQmlDebugJS
* [QTBUG-102984](https://bugreports.qt.io/browse/QTBUG-102984) QML debugger and profiler tests hangs on macOS/x86_64 in
CI
* [QTBUG-132697](https://bugreports.qt.io/browse/QTBUG-132697) FAIL!  :
tst_QQmlDebugJS::setBreakpointInScriptThatQuits(custom)
'm_process->waitForFinished()' returned FALSE.
* [QTBUG-125289](https://bugreports.qt.io/browse/QTBUG-125289) Add an overload of toScriptValue that only produces
vanilla JavaScript types
* [QTBUG-
132631](https://bugreports.qt.io/browse/QTBUG-132631) tst_qquicklistview2::isCurrentItem_NoRegressionWithDelegateModelG
roups is flaky on opensuse
* [QTBUG-132632](https://bugreports.qt.io/browse/QTBUG-132632) tst_qquicktextedit::cursorDelegate is flaky on opensuse
* [QTBUG-132647](https://bugreports.qt.io/browse/QTBUG-132647) tst_QQuickMultiPointTouchArea::nonOverlapping is flaky
on opensuse
* [QTBUG-132559](https://bugreports.qt.io/browse/QTBUG-132559) Top flaky test:
tst_qquickflickable::nestedSliderUsingTouch
* [QTBUG-132628](https://bugreports.qt.io/browse/QTBUG-132628) tst_taphandler::longPress is flaky on OpenSUSE
* [QTBUG-132650](https://bugreports.qt.io/browse/QTBUG-132650) tst_qquicktextedit::overwriteMode is flaky on opensuse
* [QTBUG-132651](https://bugreports.qt.io/browse/QTBUG-132651) tst_qquicktextedit::keyboardSelection is flaky on
opensuse
* [QTBUG-132073](https://bugreports.qt.io/browse/QTBUG-132073) Not possible to use ContextMenu on event-consuming types
like Pane
* [QTBUG-124913](https://bugreports.qt.io/browse/QTBUG-124913) Weird compiler warning message when using unresolved
function
* [QTBUG-132931](https://bugreports.qt.io/browse/QTBUG-132931) QJSEngine leaks memory
* [QTBUG-131894](https://bugreports.qt.io/browse/QTBUG-131894) qtranslator loads wrong locale
* [QTBUG-130374](https://bugreports.qt.io/browse/QTBUG-130374) tst_qquicktextedit is flaky on Linux
* [QTBUG-133530](https://bugreports.qt.io/browse/QTBUG-133530) Several Controls tests failing after test coverage
restored
* [QTBUG-133725](https://bugreports.qt.io/browse/QTBUG-133725) qml_tool_autogen target loses almost all dependencies on
other autogen and sync_headers targets
* [QTBUG-133305](https://bugreports.qt.io/browse/QTBUG-133305) QDeclarative crashes with PARAM_RTP_MEM_FILL=FALSE on
VxWorks
* [QTBUG-130879](https://bugreports.qt.io/browse/QTBUG-130879) "Failed to build texture render target for layer" error
log when using Flickable, resizeContent and layer.enabled
* [QTBUG-87776](https://bugreports.qt.io/browse/QTBUG-87776) Move Qt::FooPrivate targets into separate CMake packages
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-133858](https://bugreports.qt.io/browse/QTBUG-133858) tst_QQuickMenu::contextMenuKeyboard is flaky under
stress
* [QTBUG-134009](https://bugreports.qt.io/browse/QTBUG-134009) warnings in offscreen plugin, inherited from
QPlatformWindow
* [QTBUG-134269](https://bugreports.qt.io/browse/QTBUG-134269) Attached properties using REVISION produce error
* [QTCREATORBUG-32591](https://bugreports.qt.io/browse/QTCREATORBUG-32591) qmlls still not work in qt creator
* [QTBUG-134251](https://bugreports.qt.io/browse/QTBUG-134251) Qt Quick for Android is hard to find
* [QTBUG-134250](https://bugreports.qt.io/browse/QTBUG-134250) qdoc fails to report warnings for incorrect \fn
signatures

### qtactiveqt
* [QTBUG-126518](https://bugreports.qt.io/browse/QTBUG-126518) Qt 6.8 qutlook example does not build with 6.8.0 Beta1
* [QTBUG-123533](https://bugreports.qt.io/browse/QTBUG-123533) dumpcpp generates code that does not compile
* [QTBUG-123498](https://bugreports.qt.io/browse/QTBUG-123498) [Reg 6.2.0 -> 6.2.11 (possibly 6.2.3->6.2.4)][ActiveQt]
Resizing QTableView header inside a QAXCLASS freezes COM application
* [QTBUG-129724](https://bugreports.qt.io/browse/QTBUG-129724) error C2065: 'CommandStateChangeConstants': undeclared
identifier
* [QTBUG-127510](https://bugreports.qt.io/browse/QTBUG-127510) SCARY QDebug::toString() terrifies tests that compare
Microsoft::WRL::ComPtr
* [QTBUG-128173](https://bugreports.qt.io/browse/QTBUG-128173) Doc: Remove use of defunct QDoc command
"\tableofcontents"
* [QTBUG-127947](https://bugreports.qt.io/browse/QTBUG-127947) Active Qt landing page is missing license text
* [QTBUG-111760](https://bugreports.qt.io/browse/QTBUG-111760) target_link_libraries(foo INTERFACE Qt::Core) fails for
interface libs with CMake < 3.19 on Windows
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtmultimedia
* [QTBUG-125213](https://bugreports.qt.io/browse/QTBUG-125213) Flaky crashes on ASAN-compiled tst_qsoundeffect
* [QTBUG-119102](https://bugreports.qt.io/browse/QTBUG-119102) Cannot record video using QML or widgets camera example
on macOS with built-in camera or iOS device continuity camera
* [QTBUG-125957](https://bugreports.qt.io/browse/QTBUG-125957) Lost last frame when encoding custom video frames
* [QTBUG-125389](https://bugreports.qt.io/browse/QTBUG-125389) Deadlock during destruction in
tst_QMediaCaptureSession::testAudioMute
* [QTBUG-126119](https://bugreports.qt.io/browse/QTBUG-126119) Test #43: tst_qmediacapturesession .........***Failed
* [QTBUG-126203](https://bugreports.qt.io/browse/QTBUG-126203) [darwin] MediaPlayer does not always take into account
the selected audio output device
* [QTBUG-123220](https://bugreports.qt.io/browse/QTBUG-123220) Green Line Artifact in QML VideoOutput component
* [QTBUG-118571](https://bugreports.qt.io/browse/QTBUG-118571) Android tests on CI part 1/3 (camera & media
capture/player)
* [QTBUG-126449](https://bugreports.qt.io/browse/QTBUG-126449) qmltyperegistrar: Build time warnings for qtmultimedia
* [QTBUG-113399](https://bugreports.qt.io/browse/QTBUG-113399) QVideoSink with Qt 6 on Android ignores requested camera
settings
* [QTBUG-121452](https://bugreports.qt.io/browse/QTBUG-121452) Qt ScreenCapture Example Fails to Capture Screen Content
* [QTBUG-114674](https://bugreports.qt.io/browse/QTBUG-114674) Audio fails silently on iOS 16 following app suspended
* [QTBUG-124396](https://bugreports.qt.io/browse/QTBUG-124396) [Boot2Qt] "The wayland connection broke" when running
audioooutput example app
* [QTBUG-122635](https://bugreports.qt.io/browse/QTBUG-122635) QML video example crashes immediately after launch,
because of missing qmlvideo module
* [QTBUG-124925](https://bugreports.qt.io/browse/QTBUG-124925) [REG 6.5.5 -> 6.5.6] Spectrum App Crashes after
recording sound in "Record and Playback" Mode
* [QTBUG-126254](https://bugreports.qt.io/browse/QTBUG-126254) [darwin] Camera example crashes when recording with
webcam, "AudioChannelLayout is invalid"
* [QTBUG-126958](https://bugreports.qt.io/browse/QTBUG-126958) avfvideorenderer control - don't use invalid pointers
* [QTBUG-126988](https://bugreports.qt.io/browse/QTBUG-126988) [macOS] QAudioSource::start returns invalid pointer if
start failed
* [QTBUG-122104](https://bugreports.qt.io/browse/QTBUG-122104) Missing Info.plist in audio devices example does not
allow using the application on macOS
* [QTBUG-126968](https://bugreports.qt.io/browse/QTBUG-126968) wasm: MediaPlayer won't work if source is set at
creation
* [QTBUG-124615](https://bugreports.qt.io/browse/QTBUG-124615) Top flaky test: tst_qmediaplayerbackend::play_createsFra
mesWithExpectedContentAndIncreasingFrameTime_whenPlayingRtspMediaStream
on MacOS_14 ARM64, MacOS_12, MacOS_13, Ubuntu_22_04, openSUSE_15_5.
* [QTBUG-126192](https://bugreports.qt.io/browse/QTBUG-126192) ios: Zoom factor does not notify changes and cannot zoom
back to 1.0
* [QTBUG-126817](https://bugreports.qt.io/browse/QTBUG-126817) Qt6MultimediaConfig.cmake fails due to missing FFmpeg
* [QTBUG-126428](https://bugreports.qt.io/browse/QTBUG-126428) Android: Regression with playing video (H.264)
* [QTBUG-116766](https://bugreports.qt.io/browse/QTBUG-116766) [Boot2Qt] List of cameras should contain only available
(connected) ones
* [QTBUG-124206](https://bugreports.qt.io/browse/QTBUG-124206) [GStreamer]
tst_QAudioDecoderBackend::play_emitsFormatError_whenMediaHasNoAudioTrack
does not report errors
* [QTBUG-127453](https://bugreports.qt.io/browse/QTBUG-127453) WASM: seekableChanged is not firing
* [QTBUG-127745](https://bugreports.qt.io/browse/QTBUG-127745) tst_qvideoframecolormanagement failed on Ubuntu 24.04
offscreen(arm64)
* [QTBUG-127744](https://bugreports.qt.io/browse/QTBUG-127744) tst_qvideoframe failed on Ubuntu 24.04 offscreen(arm64)
* [QTBUG-127746](https://bugreports.qt.io/browse/QTBUG-127746) tst_qmediaplayerbackend failed on Ubuntu 24.04
offscreen(arm64)
* [QTBUG-127784](https://bugreports.qt.io/browse/QTBUG-127784) Inaccurate color handling when no RHI backend is
available
* [QTBUG-127675](https://bugreports.qt.io/browse/QTBUG-127675) Spurious assertion failure in
tst_QSoundEffect::testSetSourceWhilePlaying
* [QTBUG-127320](https://bugreports.qt.io/browse/QTBUG-127320) QMediaPlayer unable to open files with absolute paths
without scheme
* [QTBUG-127533](https://bugreports.qt.io/browse/QTBUG-127533) Android front face camera upside down / not mirrored
* [QTBUG-125901](https://bugreports.qt.io/browse/QTBUG-125901) IOCTL  call on VIDIOC_ENUM_FRAMEINTERVALS fails to
enumarate frame interval/rate for FFmpeg V4L2 cameras
* [QTBUG-127836](https://bugreports.qt.io/browse/QTBUG-127836) Windows ARM: Multimedia -
tst_QMediaFormat::testResolveForEncoding fails
* [QTBUG-128150](https://bugreports.qt.io/browse/QTBUG-128150) Fix Windows ARM: Multimedia -
tst_QMediaFormat::testResolveForEncoding
* [QTBUG-127838](https://bugreports.qt.io/browse/QTBUG-127838) Windows ARM: Multimedia -
tst_QQuickVideoOutput::initTestCase fails
* [QTBUG-128151](https://bugreports.qt.io/browse/QTBUG-128151) Fix Windows ARM: Multimedia -
tst_QQuickVideoOutput::initTestCase
* [QTBUG-128264](https://bugreports.qt.io/browse/QTBUG-128264) (No such file or directory):
/home/qt/work/qt/3rdparty/ffmpeg/qt_attribution.json
* [QTBUG-127494](https://bugreports.qt.io/browse/QTBUG-127494) [WASM] Multiple VideoOutputs cannot play independently
* [QTBUG-128246](https://bugreports.qt.io/browse/QTBUG-128246) QMultimedia UYVY rendering is in lower image quality
* [QTBUG-127681](https://bugreports.qt.io/browse/QTBUG-127681) Spurious crash in
stressTest_setupAndTeardown_keepAudioOutput on android
* [QTBUG-128759](https://bugreports.qt.io/browse/QTBUG-128759) [REG 6.7.2->6.7.3] change in configure options,
gstreamer on LoA
* [QTBUG-128335](https://bugreports.qt.io/browse/QTBUG-128335) Error messages are invisible in media player error
dialog on Windows
* [QTBUG-125356](https://bugreports.qt.io/browse/QTBUG-125356) multimedia/screencapture/CMakeLists.txt is missing
INSTALL_EXAMPLEDIR
* [QTBUG-128374](https://bugreports.qt.io/browse/QTBUG-128374) Sporadic crash on QRhiMetal::enqueueSubresUpload()
* [QTBUG-110131](https://bugreports.qt.io/browse/QTBUG-110131) QML Camera unloading crash on iOS
* [QTBUG-120465](https://bugreports.qt.io/browse/QTBUG-120465) QML Camera unloading crash on iOS
* [QTBUG-126592](https://bugreports.qt.io/browse/QTBUG-126592) MediaPlayer never stops on some audio - ffmpeg
* [QTBUG-128482](https://bugreports.qt.io/browse/QTBUG-128482) QMediaRecorder::setAutoStop crashes if no media backend
is found
* [QTBUG-127853](https://bugreports.qt.io/browse/QTBUG-127853) Use cmake's ability to embed frameworks/dylibs (ffmpeg
on iOS)
* [QTBUG-128159](https://bugreports.qt.io/browse/QTBUG-128159) QFFmpegMediaPlayer setMedia assert failure
* [QTBUG-129021](https://bugreports.qt.io/browse/QTBUG-129021) Replace usage of deprecated
av_fmt_ctx_get_duration_estimation_method
* [QTBUG-112259](https://bugreports.qt.io/browse/QTBUG-112259) QCameraFocus doesn't work properly on iOS
* [QTBUG-129232](https://bugreports.qt.io/browse/QTBUG-129232) Fix misleading diagnostics in CMake output when FFmpeg
is not found
* [QTBUG-129184](https://bugreports.qt.io/browse/QTBUG-129184) Bad type for GstURIDecodeBin property
* [QTBUG-126211](https://bugreports.qt.io/browse/QTBUG-126211) Multiple CMake warnings about missing 'pc' files on
Windows
* [QTBUG-129053](https://bugreports.qt.io/browse/QTBUG-129053) Deadlock in tst_qsoundeffect
* [QTBUG-129502](https://bugreports.qt.io/browse/QTBUG-129502) Regression in QtMultimedia [6.7->6.8]
* [QTBUG-129469](https://bugreports.qt.io/browse/QTBUG-129469) Test #42: tst_qmediaplayerbackend ..........***Failed
* [QTBUG-129501](https://bugreports.qt.io/browse/QTBUG-129501) [REG 6.7.2-6.7.3] QMediaRecorder doesn't respect the
output file extension
* [QTBUG-129521](https://bugreports.qt.io/browse/QTBUG-129521) QFFmpeg::EncoderThread: use-after-free in unit tests
* [QTBUG-129587](https://bugreports.qt.io/browse/QTBUG-129587) Build failure: -Werror in pipewire/spa header
* [QTBUG-129712](https://bugreports.qt.io/browse/QTBUG-129712) Test timed out:
makeCustomGStreamerCamera_fromPipelineDescription_userProvidedGstElement
* [QTBUG-129714](https://bugreports.qt.io/browse/QTBUG-129714) Document programmatic IO APIs as only supported with
FFmpeg media backend
* [QTBUG-129825](https://bugreports.qt.io/browse/QTBUG-129825) qplatformaudiobufferinput_p.h(41): error C2332:
'struct': missing tag name
* [QTBUG-129597](https://bugreports.qt.io/browse/QTBUG-129597) Assertion error, QSoundEffect object creation on worker
thread using QtConcurrent
* [QTBUG-116671](https://bugreports.qt.io/browse/QTBUG-116671) Fix capture_capturesToFile_whenConnectedToMediaRecorder
on linux CI
* [QTBUG-46409](https://bugreports.qt.io/browse/QTBUG-46409) tst_qaudiodeviceinfo fails in RHEL
* [QTBUG-128421](https://bugreports.qt.io/browse/QTBUG-128421) [Android] Recorder example is not able to record video
* [QTBUG-130348](https://bugreports.qt.io/browse/QTBUG-130348) Update documentation for QMediaRecorder::actualLocation
and outputLoction
* [QTBUG-112512](https://bugreports.qt.io/browse/QTBUG-112512) QSoundEffect cuts out on very short sounds ( ~ 0.2 - 0.3
seconds )
* [QTBUG-128738](https://bugreports.qt.io/browse/QTBUG-128738) MediaPlayer on android device can't find default audio
output
* [QTBUG-126567](https://bugreports.qt.io/browse/QTBUG-126567) Android 14 QMediaPlayer plays sound using speakers
instead of headphones
* [QTBUG-130441](https://bugreports.qt.io/browse/QTBUG-130441) Configuring Qt Multimedia fails even if -no-feature-
ffmpeg is specified
* [QTBUG-128369](https://bugreports.qt.io/browse/QTBUG-128369) [EVR] Access violation on
EVRCustomPresenter::processOutput()
* [QTBUG-130488](https://bugreports.qt.io/browse/QTBUG-130488) qt6_add_ios_ffmpeg_libraries wrongly uses APPEND on a
flag CMake var
* [QTBUG-130600](https://bugreports.qt.io/browse/QTBUG-130600) [gstreamer] Intel IPU6 camera shows up as multiple
devices
* [QTBUG-130387](https://bugreports.qt.io/browse/QTBUG-130387) [gstreamer] QMediaRecorder - recorder broken when audio
input present
* [QTBUG-130668](https://bugreports.qt.io/browse/QTBUG-130668) QSoundEffect::setSource does not change audio source
* [QTBUG-128412](https://bugreports.qt.io/browse/QTBUG-128412) [WASM] declarative-camera example does not allow
capturing images, viewing captured photos, and playing back video
* [QTBUG-128413](https://bugreports.qt.io/browse/QTBUG-128413) [WASM] Changing camera in declarative-camera example
does not work
* [QTBUG-118594](https://bugreports.qt.io/browse/QTBUG-118594)  QML Camera wrong Orientation on iOS
* [QTBUG-130719](https://bugreports.qt.io/browse/QTBUG-130719) FAIL!  :
tst_QWindowCaptureBackend::capturedImage_equals_imageFromGrab(single-
pixel-window)
* [QTBUG-127543](https://bugreports.qt.io/browse/QTBUG-127543) QSoundEffect/SoundEffect audioDevice property has no
effect when device is changed
* [QTBUG-124350](https://bugreports.qt.io/browse/QTBUG-124350) [Boot2Qt] Switching the cameras in QML camera app causes
the app to crash
* [QTBUG-129351](https://bugreports.qt.io/browse/QTBUG-129351) [Boot2Qt][Camera] The QML camera app crashed when
swtiching the camera from USB to CSI
* [QTBUG-130478](https://bugreports.qt.io/browse/QTBUG-130478) QVideoFormat::isSupported returns false with supported
video codecs if audio codec is not specified
* [QTBUG-119506](https://bugreports.qt.io/browse/QTBUG-119506) AudioOutputExample-Graphic&Multimedia-Example Unplugging
& plugging headphones don't work as expected
* [QTBUG-128869](https://bugreports.qt.io/browse/QTBUG-128869) declarative-camera capture-button stops responding under
very specific conditions
* [QTBUG-118827](https://bugreports.qt.io/browse/QTBUG-118827) [REG 6.2..11 -> 6.2.13] Qt Widget Spectrum Example
UnderrunError.
* [QTBUG-119766](https://bugreports.qt.io/browse/QTBUG-119766) Spectrum Example - The sound is not redirected when
output is changed
* [QTBUG-119767](https://bugreports.qt.io/browse/QTBUG-119767) Spectrum Example - Mode - Generated Tone does not work
* [QTBUG-114104](https://bugreports.qt.io/browse/QTBUG-114104) R8 is not supported on GLES 2.0 only systems
* [QTBUG-130911](https://bugreports.qt.io/browse/QTBUG-130911) Android: Regression for recording after ffmpeg update to
7.1
* [QTBUG-129379](https://bugreports.qt.io/browse/QTBUG-129379) Declarative camera example: video recording stutters.
* [QTBUG-130813](https://bugreports.qt.io/browse/QTBUG-130813) qt_add_ios_ffmpeg_libraries does not generate
SwiftSupport folder so AppStore rejects!
* [QTBUG-131300](https://bugreports.qt.io/browse/QTBUG-131300) QMultimedia module build fails in Boot2Qt / Yocto
* [QTBUG-131495](https://bugreports.qt.io/browse/QTBUG-131495) GStreamer media player example does not automatically
start playing media
* [QTBUG-130970](https://bugreports.qt.io/browse/QTBUG-130970) [wayland] qtmm examples crash on rockchip when using
wayland
* [QTBUG-131284](https://bugreports.qt.io/browse/QTBUG-131284) The QML video example crashes when running fullscreen
mode for the video and getting back to the main app view
* [QTBUG-124351](https://bugreports.qt.io/browse/QTBUG-124351) [Boot2Qt][Wayland] The widgets camera app crashes when
taking the picture in the full screen
* [QTBUG-131107](https://bugreports.qt.io/browse/QTBUG-131107) QVideoFrame::toImage / qImageFromVideoFrame not safe to
call from worker thread
* [QTBUG-131567](https://bugreports.qt.io/browse/QTBUG-131567) Incorrect images are used for QML Media Player
documentation on the web
* [QTBUG-131715](https://bugreports.qt.io/browse/QTBUG-131715) QML VideoOutput.orientation is broken
* [QTBUG-131530](https://bugreports.qt.io/browse/QTBUG-131530) declarative-camera crashes on startup under iOS 18.1
* [QTBUG-119355](https://bugreports.qt.io/browse/QTBUG-119355) MediaPlayerApp-Desktop-example Unplugging the audio
output freezes the media and prevent it from being played
* [QTBUG-130340](https://bugreports.qt.io/browse/QTBUG-130340) MediaPlayer sound is muted when iPhone hardware sound
switch is off
* [QTBUG-129692](https://bugreports.qt.io/browse/QTBUG-129692) [darwin] Sporadic crashes on QMediaPlayer destuction
* [QTBUG-131882](https://bugreports.qt.io/browse/QTBUG-131882) QtMultimedia - crashes with 'darwin' plugin (iOS)
* [QTBUG-130898](https://bugreports.qt.io/browse/QTBUG-130898) Guard QML MediaRecorder videoResolution from accessing
invalid memory address
* [QTBUG-115023](https://bugreports.qt.io/browse/QTBUG-115023) Video QML widget does not reset errorString after
assigning source and always resets after play
* [QTBUG-131753](https://bugreports.qt.io/browse/QTBUG-131753) QML module QtQuick3D.SpatialAudio depend on nonexisting
QML module QtQuick3DPrivate
* [QTBUG-131286](https://bugreports.qt.io/browse/QTBUG-131286) Cannot use QML video example on MacOS
* [QTBUG-128253](https://bugreports.qt.io/browse/QTBUG-128253) List of camera devices does not update on runtime
* [QTBUG-130901](https://bugreports.qt.io/browse/QTBUG-130901) Crash on Some Android Device when using Multimedia
* [QTBUG-126305](https://bugreports.qt.io/browse/QTBUG-126305) Setting camera pixel format and resolution is failed.
* [QTBUG-123023](https://bugreports.qt.io/browse/QTBUG-123023) [Examples] Audio input devices list is not updated when
connecting new device
* [QTBUG-132478](https://bugreports.qt.io/browse/QTBUG-132478) Memory leak in video playback
* [QTBUG-132463](https://bugreports.qt.io/browse/QTBUG-132463) Recording video and audio with AAC audio codec don't
play back correctly in Windows Media Player or Quicktime on macOS
* [QTBUG-129394](https://bugreports.qt.io/browse/QTBUG-129394) Qt Dice freeze (not hang, just jerky)
* [QTBUG-132266](https://bugreports.qt.io/browse/QTBUG-132266) QSoundEffect plays choppy WAV sound effects on macOS
* [QTBUG-132779](https://bugreports.qt.io/browse/QTBUG-132779) Regression: Captured images have no rotation data
applied
* [QTBUG-131785](https://bugreports.qt.io/browse/QTBUG-131785) [Boot2Qt] The media player detects 2 video tracks for
the m2v file
* [QTBUG-112952](https://bugreports.qt.io/browse/QTBUG-112952) Camera (Widgets) Example missing buttons in topbar
* [QTBUG-126276](https://bugreports.qt.io/browse/QTBUG-126276) QMediaRecorder fails to encode to Matroska file format
with some codecs
* [QTBUG-131270](https://bugreports.qt.io/browse/QTBUG-131270) Improve QMediaFormat::isSupported to support more codecs
* [QTBUG-129708](https://bugreports.qt.io/browse/QTBUG-129708) Wrong aspect ratio with rotated screen using
QScreenCapture and QMediaRecorder
* [QTBUG-108680](https://bugreports.qt.io/browse/QTBUG-108680) QAudioDeviceInfo does not report 176.4kHz sample rates
* [QTBUG-129915](https://bugreports.qt.io/browse/QTBUG-129915) Qt + VB-CABLE : 8 channels on macOS / 2 channels only on
Windows
* [QTBUG-108681](https://bugreports.qt.io/browse/QTBUG-108681) QAudioDevice min/max sample rate API is inappropriate
and also incorrect
* [QTBUG-132525](https://bugreports.qt.io/browse/QTBUG-132525) [CoreAudio] sampling rate ranges are wrong
* [QTBUG-130299](https://bugreports.qt.io/browse/QTBUG-130299) [windows] Sporadic ASSERT on QMediaPlayer destruction
* [QTBUG-133201](https://bugreports.qt.io/browse/QTBUG-133201) Recording audio can crash if audio was previously
recorded with a codec with a bigger buffer size
* [QTBUG-113247](https://bugreports.qt.io/browse/QTBUG-113247) Crash when recording wav audio
* [QTBUG-132532](https://bugreports.qt.io/browse/QTBUG-132532) Audiorecoder example bugs
* [QTBUG-131114](https://bugreports.qt.io/browse/QTBUG-131114) Workaround needed for video pixel formats that use RG8
textures on GLES2
* [QTBUG-133096](https://bugreports.qt.io/browse/QTBUG-133096) QML ImageCapture property fileFormat is read-only
* [QTBUG-133250](https://bugreports.qt.io/browse/QTBUG-133250) QImageCapture::fileFormatChanged signal fires when value
is unchanged
* [QTBUG-124131](https://bugreports.qt.io/browse/QTBUG-124131) Recording MP3 fails on Windows with Intel Microphone
Array
* [QTBUG-130386](https://bugreports.qt.io/browse/QTBUG-130386) [QML] MediaPlayer{}/Video{} crashes when changing the
media source right after calling play()
* [QTBUG-128802](https://bugreports.qt.io/browse/QTBUG-128802) [ffmpeg] QMediaPlayer::isSeekable returns true for
sequential QIODevice
* [QTBUG-126259](https://bugreports.qt.io/browse/QTBUG-126259) Encoding odd-sized custom frames causes ASAN crash in
sws_rescale
* [QTBUG-128908](https://bugreports.qt.io/browse/QTBUG-128908) HLS video stream (m3u8) has glitches and delay in the
first segment
* [QTBUG-131688](https://bugreports.qt.io/browse/QTBUG-131688) Ffmpeg backend build fails if openssl 1.1 is used
* [QTBUG-133813](https://bugreports.qt.io/browse/QTBUG-133813) Document that QML VideoOutput is a subclass of Item
* [QTBUG-133033](https://bugreports.qt.io/browse/QTBUG-133033) QMediaPlayer may crash during shutdown
* [QTBUG-134090](https://bugreports.qt.io/browse/QTBUG-134090) [REG 6.9.0beta3 snapshot->6.9.0 beta3] the
-DFEATURE_gui=OFF build fails
* [QTBUG-134085](https://bugreports.qt.io/browse/QTBUG-134085) Cannot play recorded video on declarative-example
* [QTBUG-133773](https://bugreports.qt.io/browse/QTBUG-133773) Cannot record a video with QML camera
* [QTBUG-134135](https://bugreports.qt.io/browse/QTBUG-134135) qandroidvideoframebuffer.cpp gives "error: variable
length arrays in C++ are a Clang extension" errors with NDK r27c
* [QTBUG-125238](https://bugreports.qt.io/browse/QTBUG-125238) QVideoFrame::toImage fails on Android with 16 bit per
component planar YUV formats
* [QTBUG-125956](https://bugreports.qt.io/browse/QTBUG-125956) Unit testing of new APIs
* [QTBUG-124725](https://bugreports.qt.io/browse/QTBUG-124725) [Camera] The video recorded with webcam on macOS is
corrupted - it only displays green flashing noise
* [QTBUG-125613](https://bugreports.qt.io/browse/QTBUG-125613) Investigate lacking video format support on Android 14
with FFmpeg media player
* [QTBUG-67692](https://bugreports.qt.io/browse/QTBUG-67692) Clash with Qt's internal logging categories when building
project with a static build of Qt
* [QTBUG-117888](https://bugreports.qt.io/browse/QTBUG-117888) Wide camera is not supported?
* [QTBUG-122757](https://bugreports.qt.io/browse/QTBUG-122757) FFmpeg+Intel VAAPI decoding of certain h264/mp4 videos
fails in 6.6.x+
* [QTBUG-126106](https://bugreports.qt.io/browse/QTBUG-126106) QVideoFrames sent to QML as signal arguments are
deallocated too late
* [QTBUG-126143](https://bugreports.qt.io/browse/QTBUG-126143) QMediaFormat on Linux does not show MP3
* [QTBUG-126799](https://bugreports.qt.io/browse/QTBUG-126799) [gstreamer] playback rate / seeking unreliable
* [QTBUG-123056](https://bugreports.qt.io/browse/QTBUG-123056) GStreamer: `setLoops` sometimes not working
* [QTBUG-127031](https://bugreports.qt.io/browse/QTBUG-127031) [QMediaPlayer] switching video output while playback is
paused does not update new sink
* [QTBUG-126014](https://bugreports.qt.io/browse/QTBUG-126014) [ffmpeg] setVideoOutput/setAudioOutput while playing
seems broken
* [QTBUG-127346](https://bugreports.qt.io/browse/QTBUG-127346) [gstreamer] QMediaPlayer: subsequent playback broken
* [QTBUG-127484](https://bugreports.qt.io/browse/QTBUG-127484) CMake Error if gstreamer_gl_wayland (or gl_x11) feature
is enabled
* [QTBUG-127137](https://bugreports.qt.io/browse/QTBUG-127137) [ffmpeg, macos]
tst_QMediaPlayerBackend::stressTest_setupAndTeardown crashes on CI
* [QTBUG-95952](https://bugreports.qt.io/browse/QTBUG-95952) Seemingly unnecessary check for pulse-mainloop-glib
* [QTBUG-127733](https://bugreports.qt.io/browse/QTBUG-127733) tst_QAudioSink::pullResumeFromUnderrun() failed on
Ubuntu 24.04 offscreen and X11
* [QTBUG-127927](https://bugreports.qt.io/browse/QTBUG-127927) [gstreamer] record_video_without_preview assertion
failure on CI
* [QTBUG-128161](https://bugreports.qt.io/browse/QTBUG-128161) Fix Windows ARM: Multimedia - crash in
tst_QVideoFrameBackend
* [QTBUG-127837](https://bugreports.qt.io/browse/QTBUG-127837) Windows ARM: Multimedia - Two crashes in
tst_qvideoframebackend and tst_qmediaframeinputsbackend
* [QTBUG-128162](https://bugreports.qt.io/browse/QTBUG-128162) Fix Windows ARM: Multimedia - crash in
tst_qmediaframeinputsbackend
* [QTBUG-127781](https://bugreports.qt.io/browse/QTBUG-127781) Qt6::MockMultimediaPlugin is duplicated when building
qtmultimedia tests against pre-built qtmultimedia
* [QTBUG-128336](https://bugreports.qt.io/browse/QTBUG-128336) Camera widget example does not record audio with default
AAC format
* [QTBUG-118877](https://bugreports.qt.io/browse/QTBUG-118877) -qreal float configuration option does not compile
* [QTBUG-112014](https://bugreports.qt.io/browse/QTBUG-112014) QMediaPlayer hangs up on setPosition(...) when using
gstreamer backend
* [QTBUG-124372](https://bugreports.qt.io/browse/QTBUG-124372) After seeking using the GStreamer backend, the stream
goes into a paused state.
* [QTBUG-129078](https://bugreports.qt.io/browse/QTBUG-129078) Unit test failures on Android Samsung Galaxy S6 Lite
* [QTBUG-128838](https://bugreports.qt.io/browse/QTBUG-128838) Regression after unification of video frame
transformations
* [QTBUG-127565](https://bugreports.qt.io/browse/QTBUG-127565) Top flaky test: tst_qmediaplayerbackend::finiteLoops
* [QTBUG-111926](https://bugreports.qt.io/browse/QTBUG-111926) QFlags doesn't support large (>  sizeof(int)) enums
* [QTBUG-129570](https://bugreports.qt.io/browse/QTBUG-129570) moc can no longer create meta objects for private
classes (that aren't Q_OBJECT themselves)
* [QTBUG-129486](https://bugreports.qt.io/browse/QTBUG-129486) re-enable test for gstreamer without blocking the
dependency updater
* [QTBUG-128515](https://bugreports.qt.io/browse/QTBUG-128515) tst_QScreenCaptureBackend failed on Ubuntu 24.04 GNOME
X11
* [QTBUG-121542](https://bugreports.qt.io/browse/QTBUG-121542) Video playback with QtMultimedia stutters when using
d3d11 backend, WindowsMediaFoundation, and having an animation on the
scene.
* [QTBUG-117099](https://bugreports.qt.io/browse/QTBUG-117099) Video jerks when playing (Windows backend)
* [QTBUG-110453](https://bugreports.qt.io/browse/QTBUG-110453)  tst_QVideoWidget::fullScreen fails with Android target
in RHEL-8.4
* [QTBUG-126816](https://bugreports.qt.io/browse/QTBUG-126816) Deadlock in QDarwinAudioSource while stopping
disconnected device
* [QTBUG-118310](https://bugreports.qt.io/browse/QTBUG-118310) QML Camera - setting WhiteBalance, Exposure, ISO doesn't
work as expected
* [QTBUG-129831](https://bugreports.qt.io/browse/QTBUG-129831) QCamera::setCameraDevice has unclear behavior
* [QTBUG-124517](https://bugreports.qt.io/browse/QTBUG-124517) [gstreamer] GST_MESSAGE_BUFFERING not delivered if
(uri)decodebin doesn't contain a queue
* [QTBUG-125251](https://bugreports.qt.io/browse/QTBUG-125251) [gstreamer] spurious assertion failure on shutdown
* [QTBUG-123073](https://bugreports.qt.io/browse/QTBUG-123073) [macOS] QMediaRecorder failed to record an audio after
reconnecting AirPods
* [QTBUG-131759](https://bugreports.qt.io/browse/QTBUG-131759) Log FFmpeg version and license during startup
* [QTBUG-127000](https://bugreports.qt.io/browse/QTBUG-127000) Incorrect frame rate when starting H264 video. Incorrect
playback stop.
* [QTBUG-110310](https://bugreports.qt.io/browse/QTBUG-110310) FlushMode property missing from VideoOutput
* [QTBUG-130089](https://bugreports.qt.io/browse/QTBUG-130089) Encoding to H264 fails on macOS ARM in Qt CI
* [QTBUG-132778](https://bugreports.qt.io/browse/QTBUG-132778) Error compiling multimedia examples on iOS
* [QTBUG-132087](https://bugreports.qt.io/browse/QTBUG-132087) QCamera::cameraFormat does not update correctly
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
* [QTBUG-126116](https://bugreports.qt.io/browse/QTBUG-126116) tst_validateQdocOutputFiles fails on AddressSanitizer
* [QTBUG-126182](https://bugreports.qt.io/browse/QTBUG-126182) Qt Designer  on archlinux always crash when edit an *.ui
file
* [QTBUG-126189](https://bugreports.qt.io/browse/QTBUG-126189) [REG 6.7.1->6.7.2&6.8.0] lconvert, lrelease, lupdate and
few others not combiled in no-gui build
* [QTBUG-125066](https://bugreports.qt.io/browse/QTBUG-125066) Configure fails in qttools if PrintSupport is disabled
* [QTBUG-126167](https://bugreports.qt.io/browse/QTBUG-126167) CMake fails to configure simple project
* [QTBUG-126139](https://bugreports.qt.io/browse/QTBUG-126139) Linguist shipped with Qt6 breaks how language tag is
handled
* [QTBUG-126088](https://bugreports.qt.io/browse/QTBUG-126088) qdoc: Protect \trademark from translations
* [QTBUG-126152](https://bugreports.qt.io/browse/QTBUG-126152) qdoc: Macro arguments cannot contain formatting commands
* [QTBUG-126274](https://bugreports.qt.io/browse/QTBUG-126274) [REG: 6.7.1->6.7.2] Windows/Win11/Vista styles:
designer: Spinbox values are shown doubled
* [QTBUG-61277](https://bugreports.qt.io/browse/QTBUG-61277) Doc: Some modules missing from "All QML Modules" page
* [QTBUG-125310](https://bugreports.qt.io/browse/QTBUG-125310) tst_lupdate asserts on mingw13
* [QTBUG-126546](https://bugreports.qt.io/browse/QTBUG-126546) Attribution documentation processed twice in CI
* [QTBUG-101446](https://bugreports.qt.io/browse/QTBUG-101446) QT/LLVM RTTI settings - Undefined reference to
`typeinfo' when compiling Qt Everywhere from source
* [QTBUG-126960](https://bugreports.qt.io/browse/QTBUG-126960) qdoc: No warning generated for a missing qhp subproject
index title
* [QTBUG-127052](https://bugreports.qt.io/browse/QTBUG-127052) qt_add_translations does not add the generated .ts files
to the source list of the target
* [QTBUG-127056](https://bugreports.qt.io/browse/QTBUG-127056) qt_add_translations has no way of returning the
automatically determined .ts file paths
* [QTBUG-127146](https://bugreports.qt.io/browse/QTBUG-127146) [REG 5.15 -> 6.0] TR_EXCLUDE became too strict
* [QTBUG-27936](https://bugreports.qt.io/browse/QTBUG-27936) Regression: lupdate is very very slow
* [QTBUG-124200](https://bugreports.qt.io/browse/QTBUG-124200) Linguist 'does not know the plural rules for Luganda'
* [QTBUG-127513](https://bugreports.qt.io/browse/QTBUG-127513) qttool: depends on network-support, but should only be
optional
* [QTBUG-127564](https://bugreports.qt.io/browse/QTBUG-127564) qdoc: qhp group: selector does not work for groups
without a \group page
* [QTBUG-127630](https://bugreports.qt.io/browse/QTBUG-127630) qdoc crashes when building Qt Creator developer
documentation
* [QTBUG-127789](https://bugreports.qt.io/browse/QTBUG-127789) Generated TS files are missing the language and
sourcelanguage attributes
* [QTBUG-127792](https://bugreports.qt.io/browse/QTBUG-127792)  Generated TS file with plural forms contain incorrect
<numerusform> entry count
* [QTBUG-127828](https://bugreports.qt.io/browse/QTBUG-127828) qt_add_translations: TS_FILE_DIR is ignored when
PLURALS_TS_FILE set
* [QTBUG-127841](https://bugreports.qt.io/browse/QTBUG-127841) Windows ARM: qttools - tst_lconvert::initTestCase()
fails
* [QTBUG-128186](https://bugreports.qt.io/browse/QTBUG-128186) qlitehtml is built in a directory called "value-
NOTFOUND"
* [QTBUG-126994](https://bugreports.qt.io/browse/QTBUG-126994) [DocBook] Too much escaping in code
* [QTBUG-128301](https://bugreports.qt.io/browse/QTBUG-128301) Custom CMake usage information for non-Qt projects
* [QTBUG-128411](https://bugreports.qt.io/browse/QTBUG-128411) Remove 'corefeatures.html' from qdoc manual
* [QTBUG-52024](https://bugreports.qt.io/browse/QTBUG-52024) contrary to documentation, lupdate does destroy data
* [QTBUG-124709](https://bugreports.qt.io/browse/QTBUG-124709) Linguist examples pollute the source tree with *_en.ts
files
* [QTBUG-128356](https://bugreports.qt.io/browse/QTBUG-128356) https://doc.qt.io/qt-
6/qscreen.html#physicalDotsPerInchChanged missing an entry?
* [QTBUG-127011](https://bugreports.qt.io/browse/QTBUG-127011) Attribution scanner error messages are unhelpful
* [PYSIDE-2863](https://bugreports.qt.io/browse/PYSIDE-2863) pyside6-lupdate do not attribute comment to corresponding
text
* [QTBUG-120186](https://bugreports.qt.io/browse/QTBUG-120186) qFpClassify function appears twice (for each overload)
in the docs
* [QTBUG-128926](https://bugreports.qt.io/browse/QTBUG-128926) QDoc: When linked against clang from LLVM 19, QDoc
segfaults when generating qt3d documentation
* [QTBUG-128644](https://bugreports.qt.io/browse/QTBUG-128644) QDoc fails to compile against Clang-19 RC1-RC4, Clang 20
* [QTBUG-128668](https://bugreports.qt.io/browse/QTBUG-128668) Incomplete html title generated for qt cmake manual
* [QTBUG-124255](https://bugreports.qt.io/browse/QTBUG-124255) libclang is supposed to be optional dependency, but I
can't turn it off
* [QTBUG-129503](https://bugreports.qt.io/browse/QTBUG-129503) Reg->6.7.3: In Qt Designer, the widgets' Layout
Alignment option is ineffective (unable to generate corresponding code)
* [PYSIDE-2492](https://bugreports.qt.io/browse/PYSIDE-2492) uic does not generate enumeration name into enum values
causing type checking warnings
* [QTBUG-127179](https://bugreports.qt.io/browse/QTBUG-127179) Qt Creator puts wrong fields for spacer objects
* [QTBUG-128365](https://bugreports.qt.io/browse/QTBUG-128365) Wrong "Line"  (QFrame) orientation
* [QTBUG-127051](https://bugreports.qt.io/browse/QTBUG-127051) Language server doesn't provide hover documentation for
WebEngineView.url
* [QTBUG-129833](https://bugreports.qt.io/browse/QTBUG-129833) The Context Sensitive Help example is not working
correctly
* [QTBUG-123819](https://bugreports.qt.io/browse/QTBUG-123819) LUpdate does not parse "*.mjs" files properly.
* [QTBUG-67964](https://bugreports.qt.io/browse/QTBUG-67964) lupdate: Treat warnings as errors
* [QTBUG-130502](https://bugreports.qt.io/browse/QTBUG-130502) Qt6LinguistTool CMake Policy CMP0007 not met
* [QTBUG-129709](https://bugreports.qt.io/browse/QTBUG-129709) Display of namespaced classes in documentation
* [QTBUG-128904](https://bugreports.qt.io/browse/QTBUG-128904) lupdate: Using enum class with underlying type specified
triggers "tr() cannot be called without context"
* [QTBUG-130147](https://bugreports.qt.io/browse/QTBUG-130147) lupdate warning with std::enable_if and MS STL
* [QTBUG-127527](https://bugreports.qt.io/browse/QTBUG-127527) lupdate truncates JavaScript template literal strings
* [QTBUG-23140](https://bugreports.qt.io/browse/QTBUG-23140) linguist loses origin attribute in xliff files
* [QTBUG-17307](https://bugreports.qt.io/browse/QTBUG-17307) Incorrect processing of xliff file format with multiple
<file> entries
* [QTBUG-130734](https://bugreports.qt.io/browse/QTBUG-130734) QDoc doesn't recognize namespaced QML imports
* [QTBUG-130674](https://bugreports.qt.io/browse/QTBUG-130674) Control over which page a namespaced function appears in
* [QTBUG-130873](https://bugreports.qt.io/browse/QTBUG-130873) WIndows/Windows11 Style: Designer signal slot editor
item view drawing artifacts
* [QTBUG-128949](https://bugreports.qt.io/browse/QTBUG-128949) [REG: 5->6] Help file not searchable if body tag is
followed by another tag
* [QTBUG-55480](https://bugreports.qt.io/browse/QTBUG-55480) Extra namespace qualification confuses lupdate
* [QTBUG-131014](https://bugreports.qt.io/browse/QTBUG-131014) Qt Widgets Designer: Grid not visible in dark mode
* [QTBUG-110936](https://bugreports.qt.io/browse/QTBUG-110936) lupdate can not update empty strings in .ts file
* [QTBUG-131282](https://bugreports.qt.io/browse/QTBUG-131282) Wrong Context in Function Definitions with Prepended
"::"
* [QTBUG-129392](https://bugreports.qt.io/browse/QTBUG-129392) Linguist doesn't display id for id-based translations
* [QTBUG-131480](https://bugreports.qt.io/browse/QTBUG-131480) Reg->6.8.1/Linux: Qt Linguist exit warning "Timers
cannot be stopped from another thread"
* [QTBUG-105573](https://bugreports.qt.io/browse/QTBUG-105573) lupdate produces wrong output for strings with escaped
unicode characters in some cases
* [QTBUG-131565](https://bugreports.qt.io/browse/QTBUG-131565) Remove \footnote documentation from QDoc manual
* [QTBUG-131572](https://bugreports.qt.io/browse/QTBUG-131572) qdoc: Overrides a previous doc for two QML types with
identical name in different modules
* [QTBUG-117493](https://bugreports.qt.io/browse/QTBUG-117493) lupdate's complaint about ts file's missing language
attribute is unhelpful
* [QTBUG-125951](https://bugreports.qt.io/browse/QTBUG-125951) lconvert input file ordering confusion
* [QTBUG-128617](https://bugreports.qt.io/browse/QTBUG-128617) lupdate doesn't generate the context data in .ts file
for id-based translation project
* [QTBUG-131375](https://bugreports.qt.io/browse/QTBUG-131375) QDoc generates "List of all members" tree items for
classes without public members.
* [QTBUG-130888](https://bugreports.qt.io/browse/QTBUG-130888) Incorrect formulation of conditonal noexcept \note's
* [QTBUG-130609](https://bugreports.qt.io/browse/QTBUG-130609) Zero width space in translations
* [QTBUG-131951](https://bugreports.qt.io/browse/QTBUG-131951) Linguist: Writing Translations with "&#" Causes a
Warning
* [QTBUG-128326](https://bugreports.qt.io/browse/QTBUG-128326) Can't document list<T> properties in QML
* [QTBUG-132151](https://bugreports.qt.io/browse/QTBUG-132151) QDoc doesn't support grouped properties when parsing a
.qml file
* [QTBUG-132953](https://bugreports.qt.io/browse/QTBUG-132953) tst_helpengineplugin.cpp:41:9: error: unknown type name
'DomCreationOptions
* [QTBUG-131931](https://bugreports.qt.io/browse/QTBUG-131931) Fix incorrect documentation for \reimp
* [QTBUG-131158](https://bugreports.qt.io/browse/QTBUG-131158) Qdoc mangles link targets that contain trademark symbols
* [QTBUG-132881](https://bugreports.qt.io/browse/QTBUG-132881) qdoc fails to document private signals
* [QTBUG-132613](https://bugreports.qt.io/browse/QTBUG-132613) lrelease: OUTPUT_LOCATION is ignored for auto-generated
*.ts files
* [QTBUG-131459](https://bugreports.qt.io/browse/QTBUG-131459) QDoc: No warning if \qmltype contains \inherits with
non-existing type
* [QTBUG-95236](https://bugreports.qt.io/browse/QTBUG-95236) qttools fails configure with deactivated features.
* [QTBUG-134693](https://bugreports.qt.io/browse/QTBUG-134693) [REG 6.8 -> 6.9] qt_add_translations creates QM files in
PROJECT_BINARY_DIR instead of CMAKE_CURRENT_BINARY_DIR
* [QTBUG-123130](https://bugreports.qt.io/browse/QTBUG-123130) QDoc with Clang 18 drops `noexcept` specifier from
compiler generated methods documented with \fn
* [QTBUG-67692](https://bugreports.qt.io/browse/QTBUG-67692) Clash with Qt's internal logging categories when building
project with a static build of Qt
* [QTBUG-127352](https://bugreports.qt.io/browse/QTBUG-127352) lupdate's -extension option doesn't work
* [QTBUG-80417](https://bugreports.qt.io/browse/QTBUG-80417) QDateTimeEdit cannot handle OffsetFromUTC or TimeZone as
time-spec
* [QTBUG-119429](https://bugreports.qt.io/browse/QTBUG-119429) Top flaky test: tst_lupdate::good on Windows_11_22H2,
Windows_11_23H2, and Windows_10_22H2.
* [QTBUG-127751](https://bugreports.qt.io/browse/QTBUG-127751) tst_lupdate failed on Ubuntu 24.04 offscreen(arm64)
* [PYSIDE-2840](https://bugreports.qt.io/browse/PYSIDE-2840) Enum properties unsupported in Qt Designer custom widgets
* [QTBUG-124162](https://bugreports.qt.io/browse/QTBUG-124162) Qt Assistant Print Preview is not working
* [QTBUG-128173](https://bugreports.qt.io/browse/QTBUG-128173) Doc: Remove use of defunct QDoc command
"\tableofcontents"
* [QTBUG-128368](https://bugreports.qt.io/browse/QTBUG-128368) Make sure that also qt6_ CMake commands are in the help
index
* [QTBUG-128424](https://bugreports.qt.io/browse/QTBUG-128424) Warning messages during configure are not helpful
* [QTBUG-130006](https://bugreports.qt.io/browse/QTBUG-130006) lupdate: -mno-sse not recognized if binary linked
against Clang libraries built on ARM-based Mac
* [QTBUG-130096](https://bugreports.qt.io/browse/QTBUG-130096) clang-based lupdate fails on macOS 15
* [QTBUG-130646](https://bugreports.qt.io/browse/QTBUG-130646) qdoc hangs when generating QML documentation
* [QTBUG-130282](https://bugreports.qt.io/browse/QTBUG-130282) build time path used in qdoc binary
* [QTBUG-130799](https://bugreports.qt.io/browse/QTBUG-130799) Remove or fix Q_OBJECT qdoc macro
* [QTBUG-118728](https://bugreports.qt.io/browse/QTBUG-118728) SimpleTextViewer-example The name of the file being
viewed is not shown
* [QTBUG-131884](https://bugreports.qt.io/browse/QTBUG-131884) qdoc: Segmentation fault when generating .qhp
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtdoc
* [QTBUG-126104](https://bugreports.qt.io/browse/QTBUG-126104) Android mobile examples link redirects to WASM page
* [QTBUG-126019](https://bugreports.qt.io/browse/QTBUG-126019) Clean up What's new in Qt 6.8 page
* [QTBUG-124144](https://bugreports.qt.io/browse/QTBUG-124144) No buildings in osmbuildings - example
* [QTBUG-126273](https://bugreports.qt.io/browse/QTBUG-126273) Two conflicting pages for 'Inter-process Communication'
* [QTBUG-55199](https://bugreports.qt.io/browse/QTBUG-55199) macdeployqt does not copy SVG image format plugins
* [QTBUG-126517](https://bugreports.qt.io/browse/QTBUG-126517) Qt 6.8 stocqt example does not show its content
* [QTBUG-126578](https://bugreports.qt.io/browse/QTBUG-126578) Fix warnings of StocQt
* [QTBUG-122683](https://bugreports.qt.io/browse/QTBUG-122683) Update trademark information
* [QTBUG-127060](https://bugreports.qt.io/browse/QTBUG-127060) Header column spanning more columns than expected
* [QTBUG-127547](https://bugreports.qt.io/browse/QTBUG-127547) The link in INTEGRITY doc leads to Qt for wasm doc
* [QTBUG-126866](https://bugreports.qt.io/browse/QTBUG-126866) Archiving the application does not have debug info files
(dSYM) included as expected
* [QTBUG-123164](https://bugreports.qt.io/browse/QTBUG-123164) New example demos/osmbuildings not compiling on Android
* [QTBUG-127814](https://bugreports.qt.io/browse/QTBUG-127814) Calqlatr fails to remove the unary minus character
* [QTBUG-127835](https://bugreports.qt.io/browse/QTBUG-127835) demos/lightningviewer not launching when installed
outside of build dir
* [QTBUG-128225](https://bugreports.qt.io/browse/QTBUG-128225) Failing to deploy examples that link to dynamic lib qml
modules, but don't explicitly import them
* [QTBUG-127989](https://bugreports.qt.io/browse/QTBUG-127989) [Regr: 6.7.2 -> 6.8.0-beta2] Build fails with MinGW
* [QTBUG-128231](https://bugreports.qt.io/browse/QTBUG-128231) WebAssembly: No mention that WebSocket servers are not
supported
* [QTBUG-128399](https://bugreports.qt.io/browse/QTBUG-128399) Add a link to What's New at the top of a landing page of
a Qt release
* [QTBUG-118038](https://bugreports.qt.io/browse/QTBUG-118038) Qt6WaylandCompositor could not be found because
dependency Wayland could   not be found
* [QTBUG-122041](https://bugreports.qt.io/browse/QTBUG-122041) [DocumentViewer] The app is crashing when opening the
file on Android device
* [QTBUG-122285](https://bugreports.qt.io/browse/QTBUG-122285)  The documentation doesn't specify the required versions
of the Windows SDK.
* [QTBUG-128351](https://bugreports.qt.io/browse/QTBUG-128351) car-configurator: Runtime warnings
* [QTBUG-127851](https://bugreports.qt.io/browse/QTBUG-127851) Car rendering example breaks qtdoc builds with examples,
if CMake version is below 3.21.1
* [QTBUG-128729](https://bugreports.qt.io/browse/QTBUG-128729) qtdoc module fails yocto build
* [QTBUG-128436](https://bugreports.qt.io/browse/QTBUG-128436) new ARM-based desktop platforms are not mentioned in
What's New
* [QTBUG-128673](https://bugreports.qt.io/browse/QTBUG-128673) [DocumentViewer] The app crashes on Linux when asserting
an instance of RuntimeLoader QML Type
* [QTBUG-129105](https://bugreports.qt.io/browse/QTBUG-129105) Car configurator can't download assets from
download.qt.io
* [QTBUG-129080](https://bugreports.qt.io/browse/QTBUG-129080) CMake / ninja doesn't build plugins by default
* [QTBUG-114998](https://bugreports.qt.io/browse/QTBUG-114998) Example can't run, missing module
* [QTBUG-129444](https://bugreports.qt.io/browse/QTBUG-129444) Wrong image shown in Qt Multimedia "Media Player"
examples
* [QTBUG-129569](https://bugreports.qt.io/browse/QTBUG-129569) Documentation linking to 'Qt Quick', 'Qt Widgets' now
incorrectly point to example sections
* [QTBUG-129449](https://bugreports.qt.io/browse/QTBUG-129449) Diagram in Documentation for "Threading" Basics looks
bad
* [QTBUG-129390](https://bugreports.qt.io/browse/QTBUG-129390) PaddedRectangle is not exposed from QtQuick.Controls
anymore
* [QTBUG-129773](https://bugreports.qt.io/browse/QTBUG-129773) Mark Qt HTTP Server, Qt Protobuf, and Qt GRPC as
supported Add-On modules
* [QTBUG-129559](https://bugreports.qt.io/browse/QTBUG-129559) Links to "The Qt Resource System" points to the Android
docs
* [QTBUG-123219](https://bugreports.qt.io/browse/QTBUG-123219) android: Intents sent to the app while the screen is off
cause application to freeze for some time on wake up
* [QTBUG-127527](https://bugreports.qt.io/browse/QTBUG-127527) lupdate truncates JavaScript template literal strings
* [QTBUG-119282](https://bugreports.qt.io/browse/QTBUG-119282) MediaPlayerApp-Example Issue with the audio output
* [QTBUG-128576](https://bugreports.qt.io/browse/QTBUG-128576) //~ extra-Context in .ts file doesn't show up in Qt
Linguist and it's not documented
* [QTBUG-130567](https://bugreports.qt.io/browse/QTBUG-130567) Doc: wrong link to XWayland
* [QTBUG-132348](https://bugreports.qt.io/browse/QTBUG-132348) Add missing best practices topics to the qtdoc project
tree
* [QTWEBSITE-1200](https://bugreports.qt.io/browse/QTWEBSITE-1200) Protect macOS specific file paths from translation
* [QTBUG-132360](https://bugreports.qt.io/browse/QTBUG-132360) On QtDice example top and bottom bar are partially
visible.
* [QTBUG-132551](https://bugreports.qt.io/browse/QTBUG-132551) Cannot build Car Configurator demo
* [QTBUG-133503](https://bugreports.qt.io/browse/QTBUG-133503) Add Qt list of vulnerabilities in Security overview
* [QTWEBSITE-1196](https://bugreports.qt.io/browse/QTWEBSITE-1196) Prevent CMake module name to be translated
* [QTBUG-132936](https://bugreports.qt.io/browse/QTBUG-132936) Align Overview pages with the sidebar
* [QTBUG-116765](https://bugreports.qt.io/browse/QTBUG-116765) qmlformat: unnecessarily formats single line to multiple
lines
* [QTBUG-107030](https://bugreports.qt.io/browse/QTBUG-107030) Update documentation of QML
* [QTBUG-133971](https://bugreports.qt.io/browse/QTBUG-133971) Replace "QML for Android" with "Qt Quick for Android" in
What's new 6.9
* [QTBUG-133954](https://bugreports.qt.io/browse/QTBUG-133954) Make sure that new 'Classes for string data' can be
found in TOC
* [QAA-2836](https://bugreports.qt.io/browse/QAA-2836) Make sure that all references to "Qt Android" are changed to
"Qt for Android"
* [QTBUG-132704](https://bugreports.qt.io/browse/QTBUG-132704)  Car Configurator demo crashes on startup
* [QTBUG-126094](https://bugreports.qt.io/browse/QTBUG-126094) Spelling of Qt Qml/QML very inconsistent
* [QTBUG-125329](https://bugreports.qt.io/browse/QTBUG-125329) Grpc generators: fix Policy CMP0071
* [QTBUG-100100](https://bugreports.qt.io/browse/QTBUG-100100) Demos should use `qt6_add_qml_module` instead of
`qt6_add_resources`
* [QTBUG-124657](https://bugreports.qt.io/browse/QTBUG-124657) qsTrNoOp() is not defined in QML
* [QTBUG-126201](https://bugreports.qt.io/browse/QTBUG-126201) Qt examples output CMake warning about Qt policy QTP0004
* [QTBUG-127560](https://bugreports.qt.io/browse/QTBUG-127560) maroon demo lags when enabling sounds
* [QTBUG-127736](https://bugreports.qt.io/browse/QTBUG-127736) 6.8.0 sources having 6.7.0 version strings (debian-
packages.qdoc)
* [QTBUG-127926](https://bugreports.qt.io/browse/QTBUG-127926) Outdated Android docs still refer to
QtAndroid::androidActivity()
* [QTBUG-123315](https://bugreports.qt.io/browse/QTBUG-123315) [REG 6.6.1 -> 6.6.2] Run time errors from coffee demo
* [QTBUG-128278](https://bugreports.qt.io/browse/QTBUG-128278) Incorrent and incomplete statements about using compiled
QML
* [QTBUG-128173](https://bugreports.qt.io/browse/QTBUG-128173) Doc: Remove use of defunct QDoc command
"\tableofcontents"
* [QTBUG-128678](https://bugreports.qt.io/browse/QTBUG-128678) Reintroduce support of iOS 16
* [QTBUG-92811](https://bugreports.qt.io/browse/QTBUG-92811) Misleading identification of third party tool
* [QTBUG-128455](https://bugreports.qt.io/browse/QTBUG-128455) [VxWorks] configure doesn't recognize graphics settings
* [QTBUG-129220](https://bugreports.qt.io/browse/QTBUG-129220) Wrong breadcrumb in Qt Edu for Qt for MCU docs
* [QDS-13600](https://bugreports.qt.io/browse/QDS-13600) Replace deprecated FetchContent_Populate
* [QTBUG-129628](https://bugreports.qt.io/browse/QTBUG-129628) Building Qt6 from Git for Windows fails when following
the available documentation
* [QTBUG-125322](https://bugreports.qt.io/browse/QTBUG-125322) INSTALL_EXAMPLESDIR is missing from demos/todolist's
CMakeLists.txt
* [QTBUG-130352](https://bugreports.qt.io/browse/QTBUG-130352) Update webOS page with current webOS and Qt version
* [QTBUG-130499](https://bugreports.qt.io/browse/QTBUG-130499) Add VxWorks Debugging information to Qt Documentation
* [QTBUG-130467](https://bugreports.qt.io/browse/QTBUG-130467) Qt for Android build instructions are confusing when it
comes to -developer-build
* [QTBUG-130833](https://bugreports.qt.io/browse/QTBUG-130833) String '6.8.0' found in 6.9.0 sources
* [QTBUG-130129](https://bugreports.qt.io/browse/QTBUG-130129) Docs: instruct user to put TQTC keyring in systemwide
folder, not ~
* [QTBUG-131025](https://bugreports.qt.io/browse/QTBUG-131025) Doc: Change documentation for 5 year LTS
* [QTBUG-130307](https://bugreports.qt.io/browse/QTBUG-130307) RobotArmApp example demo is visibly moving frame by
frame at the end of each movement
* [QTBUG-131486](https://bugreports.qt.io/browse/QTBUG-131486) Wrong licensing of "Qt 5 Core Compatibility APIs"
* [QTBUG-131769](https://bugreports.qt.io/browse/QTBUG-131769) Remove traces of VS 2019 in documentation
* [QTBUG-132046](https://bugreports.qt.io/browse/QTBUG-132046) Remove AGX Xavier and add AGX Orin in Tier table
* [QTBUG-132738](https://bugreports.qt.io/browse/QTBUG-132738) Errors in some examples
* [QTBUG-133305](https://bugreports.qt.io/browse/QTBUG-133305) QDeclarative crashes with PARAM_RTP_MEM_FILL=FALSE on
VxWorks
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-35598](https://bugreports.qt.io/browse/QTBUG-35598) QtQuick Controls TextField and TextArea miss mouse
context menu
* [QTBUG-134251](https://bugreports.qt.io/browse/QTBUG-134251) Qt Quick for Android is hard to find

### qtlocation
* [QTBUG-128806](https://bugreports.qt.io/browse/QTBUG-128806) Wrong instructions for adding QGeoJson to project
* [QTBUG-128901](https://bugreports.qt.io/browse/QTBUG-128901) MapPolyline cannot tolerate empty QGeoPath when
referenceSurface is set to Globe
* [QTBUG-128173](https://bugreports.qt.io/browse/QTBUG-128173) Doc: Remove use of defunct QDoc command
"\tableofcontents"
* [QTBUG-130139](https://bugreports.qt.io/browse/QTBUG-130139) Flickable: an outer flickable can sometimes be stuck in
dragging mode when dragging on an inner flickable
* [QTBUG-34881](https://bugreports.qt.io/browse/QTBUG-34881) Flickable can have its flick incorrectly stolen
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtpositioning
* [QTBUG-127847](https://bugreports.qt.io/browse/QTBUG-127847) QtPositioning Android backend always checks for precise
location
* [QTBUG-133935](https://bugreports.qt.io/browse/QTBUG-133935) QML Qt Positioning memory use after free() / double
free()
* [QTBUG-115717](https://bugreports.qt.io/browse/QTBUG-115717) QSortFilterProxyModel::invalidateFilter() sometimes does
not trigger a reevaluation of the model
* [QTBUG-130559](https://bugreports.qt.io/browse/QTBUG-130559) Enable documentation testing in the CI for all Qt
submodules containing docs
* [QTBUG-131484](https://bugreports.qt.io/browse/QTBUG-131484) Fix links to QIODeviceBase::OpenMode flags
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtsensors
* [QTBUG-128167](https://bugreports.qt.io/browse/QTBUG-128167) The android implementation is using an
obsolete/deprecated/removed function ALooper_pollAll
* [QTBUG-131578](https://bugreports.qt.io/browse/QTBUG-131578) CMake Error at
src/sensors/doc/snippets/sensors/CMakeLists.txt:13 (find_package)
* [QTBUG-128173](https://bugreports.qt.io/browse/QTBUG-128173) Doc: Remove use of defunct QDoc command
"\tableofcontents"
* [QTBUG-130799](https://bugreports.qt.io/browse/QTBUG-130799) Remove or fix Q_OBJECT qdoc macro
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtconnectivity
* [QTBUG-124650](https://bugreports.qt.io/browse/QTBUG-124650) Missing BLE 5.x Extended Advertisements for Windows
* [QTBUG-127407](https://bugreports.qt.io/browse/QTBUG-127407) annotatedurl example build failing
* [QTBUG-128465](https://bugreports.qt.io/browse/QTBUG-128465) [REG 6.8.0->6.9.0] toplevel namespace build fails on
MSVC2022 x64 & arm64, qtconnectivity/bluetooth
* [QTBUG-129763](https://bugreports.qt.io/browse/QTBUG-129763) qapduutils.cpp fails to compile on mingw developer build
with -force-asserts
* [QTBUG-129977](https://bugreports.qt.io/browse/QTBUG-129977)  Reading or writing to NFC tag gives an exception on
iPhone
* [QTBUG-124130](https://bugreports.qt.io/browse/QTBUG-124130) Bluetooth LE service data is trunctated at zero value
* [QTBUG-131940](https://bugreports.qt.io/browse/QTBUG-131940) Bluetooth examples does not work on iOS
* [QTBUG-132202](https://bugreports.qt.io/browse/QTBUG-132202) Qt bluetooth qlowenergycontroller_winrt.cpp incorrectly
assumes CharacteristicUserDescription returns UTF16 when it actually
returns UTF8
* [QTBUG-132510](https://bugreports.qt.io/browse/QTBUG-132510) Superfluous optional components
* [QTBUG-132571](https://bugreports.qt.io/browse/QTBUG-132571) Unable to build QtConnectivity without DBus
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
* [QTBUG-127110](https://bugreports.qt.io/browse/QTBUG-127110) Platforms still use the inefficient qvsnprintf() fall-
back
* [QTBUG-123430](https://bugreports.qt.io/browse/QTBUG-123430) QBluetoothSocket::errorOccured is not emitted in certain
circumstances
* [QTBUG-128173](https://bugreports.qt.io/browse/QTBUG-128173) Doc: Remove use of defunct QDoc command
"\tableofcontents"
* [QTBUG-117358](https://bugreports.qt.io/browse/QTBUG-117358) BLUETOOTH_SCAN permission flag neverForLocation
* [QTBUG-112164](https://bugreports.qt.io/browse/QTBUG-112164) Check ACCESS_FINE_LOCATION is no longer needed in recent
Android Sdk
* [QTBUG-132455](https://bugreports.qt.io/browse/QTBUG-132455) [Android] Lots of deprecated API is used
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtwayland
* [QTBUG-68756](https://bugreports.qt.io/browse/QTBUG-68756) tst_WaylandClient::dontCrashOnMultipleCommits is flaky
* [QTBUG-124502](https://bugreports.qt.io/browse/QTBUG-124502) Drag and drop operation can crash the compositor
* [QTBUG-126275](https://bugreports.qt.io/browse/QTBUG-126275) [REG Qt 6.6.3 -> 6.7.0] Wayland: Can't scroll with
mousewheel in editor
* [QTBUG-126262](https://bugreports.qt.io/browse/QTBUG-126262) ERROR: AddressSanitizer:  tst_surface heap-use-after-
free
* [QTBUG-118640](https://bugreports.qt.io/browse/QTBUG-118640) Qt sends the pointer event serial instead of the tablet
event serial in data_device:start_drag or xdg_toplevel::move.
* [QTBUG-125878](https://bugreports.qt.io/browse/QTBUG-125878) Cannot pinch-to-zoom after the qt 6.7.1 upgrade
[regression]
* [QTBUG-126313](https://bugreports.qt.io/browse/QTBUG-126313) QScroller gesture blocks mouse clicks
* [QTBUG-113404](https://bugreports.qt.io/browse/QTBUG-113404) Wayland: Gestures are not delivered to correct top level
widget
* [QTBUG-122197](https://bugreports.qt.io/browse/QTBUG-122197) QScreen::size is wrong on GNOME Wayland with 200%
scaling
* [QTBUG-127487](https://bugreports.qt.io/browse/QTBUG-127487) Touch Dragging on minimal-qml wayland compositor does
not work
* [QTBUG-117920](https://bugreports.qt.io/browse/QTBUG-117920) Unable to move/resize/close Qt Application using a wacom
tablet stylus in GNOME Environment
* [QTBUG-127301](https://bugreports.qt.io/browse/QTBUG-127301) Clipboard cannot be changed from compositor if client
has copied something
* [QTBUG-105843](https://bugreports.qt.io/browse/QTBUG-105843) Broken cursor changing on Wayland with tablet input
* [QTBUG-123776](https://bugreports.qt.io/browse/QTBUG-123776) Missing tablet cursor. Set tablet cursor on Wayland with
zwp_tablet_tool.set_cursor
* [QTBUG-128350](https://bugreports.qt.io/browse/QTBUG-128350) QWaylandBufferRef::toOpenGLTexture leaks textures
* [QTBUG-127980](https://bugreports.qt.io/browse/QTBUG-127980) Segmentation fault after Qt.quit()
* [QTBUG-129203](https://bugreports.qt.io/browse/QTBUG-129203) FAIL!  : qml::WindowItem::test_childrenZOrder()
'function returned false' returned FALSE
* [QTBUG-67919](https://bugreports.qt.io/browse/QTBUG-67919) Wayland: custom-extension example depends on private APIs
* [QTBUG-129630](https://bugreports.qt.io/browse/QTBUG-129630) QRhiWidget not shown on Wayland
* [QTBUG-129403](https://bugreports.qt.io/browse/QTBUG-129403) [Boot2Qt][Wayland] Getting "eglSwapBuffers failed with
0x300d" error when trying to run RHI widget example
* [QTBUG-129584](https://bugreports.qt.io/browse/QTBUG-129584) [REG 6.7.3] Wayland text input v3: input method window
no longer updates its positions
* [QTBUG-127821](https://bugreports.qt.io/browse/QTBUG-127821) DragHandler and DropArea interaction might cause a stuck
mousegrab
* [QTBUG-117762](https://bugreports.qt.io/browse/QTBUG-117762) "The cached device pixel ratio value was stale on window
expose" when closing window on Wayland
* [QTBUG-119112](https://bugreports.qt.io/browse/QTBUG-119112) QtQuick may render a frame after wl_surface has been
destroyed
* [QTBUG-130652](https://bugreports.qt.io/browse/QTBUG-130652) REG: Hiding and reshowing a sub-window crashes Wayland
client
* [QTBUG-130581](https://bugreports.qt.io/browse/QTBUG-130581) Virtual Keyboard Hints are not reported for the second
top level wayland window
* [QTBUG-130128](https://bugreports.qt.io/browse/QTBUG-130128) Wayland: Crash when nesting popups / (custom editor
provided by an item delegate)
* [QTBUG-128937](https://bugreports.qt.io/browse/QTBUG-128937) Wayland: Submenu popup in the wrong place instead of
adjacent to its parent menu.
* [QTBUG-130627](https://bugreports.qt.io/browse/QTBUG-130627) AddressSanitizer: heap-use-after-free on
tst_WaylandClient::mouseDrag
* [QTBUG-129331](https://bugreports.qt.io/browse/QTBUG-129331) text input v3 preedit_string's cursor position isn't
honored
* [QTBUG-131983](https://bugreports.qt.io/browse/QTBUG-131983) text input v3: first character after refocus doesn't go
through the input method
* [QTBUG-132274](https://bugreports.qt.io/browse/QTBUG-132274) Fix the module documentation structure for Qt Wayland
Client
* [QTBUG-132727](https://bugreports.qt.io/browse/QTBUG-132727) Several apps crash on Wayland with Qt 6.9
* [QTBUG-132195](https://bugreports.qt.io/browse/QTBUG-132195) text input v3: disable() request isn't committed
* [QTBUG-133204](https://bugreports.qt.io/browse/QTBUG-133204) QCursor::pos stuck at (0, 0) until mouse click/move
(wayland, kwin)
* [QTBUG-132196](https://bugreports.qt.io/browse/QTBUG-132196) text input v3: input method active with popup menu
* [QTBUG-132642](https://bugreports.qt.io/browse/QTBUG-132642) custom-extension example broken
* [QTBUG-120384](https://bugreports.qt.io/browse/QTBUG-120384) Define "manufacturer" in WaylandOutput documentation
* [QTBUG-134071](https://bugreports.qt.io/browse/QTBUG-134071) [qtwayland] Manual tests fail to compile
* [QTBUG-134126](https://bugreports.qt.io/browse/QTBUG-134126) bakedlightmap example: wayland assertion error
* [QTBUG-67692](https://bugreports.qt.io/browse/QTBUG-67692) Clash with Qt's internal logging categories when building
project with a static build of Qt
* [QTBUG-125589](https://bugreports.qt.io/browse/QTBUG-125589) weired console message with simple application
* [QTBUG-118877](https://bugreports.qt.io/browse/QTBUG-118877) -qreal float configuration option does not compile
* [QTBUG-127563](https://bugreports.qt.io/browse/QTBUG-127563) a11y: Window name reported to assistive technology
doesn't match what's displayed when app name is set
* [QTBUG-112432](https://bugreports.qt.io/browse/QTBUG-112432) wayland plugin should distinguish touchpads from mice,
etc.
* [QTBUG-125592](https://bugreports.qt.io/browse/QTBUG-125592) Crash when hiding windows on Wayland with Vulkan
* [QTBUG-128029](https://bugreports.qt.io/browse/QTBUG-128029) wayland: Window container in QMdiArea does not work
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qt3d
* [QTBUG-129701](https://bugreports.qt.io/browse/QTBUG-129701) [Qt3D] Loading of builtin shaders broken
* [QTBUG-124891](https://bugreports.qt.io/browse/QTBUG-124891) Unredistributable files in qt3d / qtquick3d
* [QTBUG-126251](https://bugreports.qt.io/browse/QTBUG-126251) Render to Texture broken following stereo rendering
fixes
* [QTBUG-106079](https://bugreports.qt.io/browse/QTBUG-106079) qmllint produces warnings from Qt3D imports and
components
* [QTBUG-128939](https://bugreports.qt.io/browse/QTBUG-128939) [REG 6.8.0 RC snapshot -> 6.8.0 RC snapshot]
Unredistributable files in qt3d
* [QTBUG-130559](https://bugreports.qt.io/browse/QTBUG-130559) Enable documentation testing in the CI for all Qt
submodules containing docs
* [QTBUG-131477](https://bugreports.qt.io/browse/QTBUG-131477) Review SBOM generation and documentation to include
third party components
* [QTBUG-129575](https://bugreports.qt.io/browse/QTBUG-129575)  Fix API flaw for QImage::mirror and QImage::mirrored
* [QTBUG-132092](https://bugreports.qt.io/browse/QTBUG-132092) RayCasting failing sometimes
* [QTBUG-130470](https://bugreports.qt.io/browse/QTBUG-130470) Issues with BlitFramebuffer::interpolationMethod
* [QTBUG-130490](https://bugreports.qt.io/browse/QTBUG-130490) Unprotected access in animation handler
* [QTBUG-131459](https://bugreports.qt.io/browse/QTBUG-131459) QDoc: No warning if \qmltype contains \inherits with
non-existing type

### qtimageformats
* [QTBUG-127540](https://bugreports.qt.io/browse/QTBUG-127540) WebP: QImage detach in WebPPictureImportRGB(A) can cause
a crash
* [QTBUG-127965](https://bugreports.qt.io/browse/QTBUG-127965) QImage not loading simple heic file
* [QTBUG-134112](https://bugreports.qt.io/browse/QTBUG-134112) 16-bit Grayscale TIFF is not loaded correctly
* [QTBUG-130617](https://bugreports.qt.io/browse/QTBUG-130617) FAIL!  : tst_qwebp::writeImage(kollada_noalpha-100)
'!reread.isNull()' returned FALSE. ()
* [QTBUG-130559](https://bugreports.qt.io/browse/QTBUG-130559) Enable documentation testing in the CI for all Qt
submodules containing docs
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtserialbus
* [QTBUG-130559](https://bugreports.qt.io/browse/QTBUG-130559) Enable documentation testing in the CI for all Qt
submodules containing docs
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtserialport
* [QTBUG-128748](https://bugreports.qt.io/browse/QTBUG-128748) Unused static functions in qserialport_p.h
* [QTBUG-128487](https://bugreports.qt.io/browse/QTBUG-128487) Difference between QSerialPortInfo on Windows and Linux
* [QTBUG-115292](https://bugreports.qt.io/browse/QTBUG-115292) QSerialPortInfo Provides USBHUB Info instead of Port
Info
* [QTBUG-109455](https://bugreports.qt.io/browse/QTBUG-109455) read() returns qint64 not int
* [QTBUG-120221](https://bugreports.qt.io/browse/QTBUG-120221) clang-tidy, and probably clang complains about dllimport
vs. inline in qtserialportinfo.h
* [QTBUG-129756](https://bugreports.qt.io/browse/QTBUG-129756) settingsRestoredOnClose() deprected from interface, but
not removed from implementation
* [QTBUG-107440](https://bugreports.qt.io/browse/QTBUG-107440) QSerial property settingsRestoredOnClose to control the
RTS line
* [QTBUG-105561](https://bugreports.qt.io/browse/QTBUG-105561) QSerialPort Mark/Space Emulation causes recursion and
crash
* [QTBUG-131679](https://bugreports.qt.io/browse/QTBUG-131679) QSerialPort does not have Mark/Space parity emulation
for reading the data
* [QTBUG-84689](https://bugreports.qt.io/browse/QTBUG-84689) readyRead() signal will be reemitted even I have called
waitForReadyRead()
* [QTBUG-67544](https://bugreports.qt.io/browse/QTBUG-67544) QSerialPort emits errorOccurred with NoError
* [QTBUG-130559](https://bugreports.qt.io/browse/QTBUG-130559) Enable documentation testing in the CI for all Qt
submodules containing docs
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtwebsockets
* [QTBUG-120492](https://bugreports.qt.io/browse/QTBUG-120492) QWebSocket connecting to an URL without a path sends GET
request without leading /
* [QTBUG-130500](https://bugreports.qt.io/browse/QTBUG-130500) Various network tests are failing on macOS 15
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtwebchannel
* [QTBUG-119303](https://bugreports.qt.io/browse/QTBUG-119303) WebChannel 'standalone' application does not build with
non-shadow build dir
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtwebengine
* [QTBUG-125035](https://bugreports.qt.io/browse/QTBUG-125035) Webengine: issues compiling with ninja 1.12
* [QTBUG-125452](https://bugreports.qt.io/browse/QTBUG-125452) QT_FEATURE_webengine_system_icu=ON results in broken
runtime
* [QTBUG-126138](https://bugreports.qt.io/browse/QTBUG-126138) Correct QML PdfSelection documentation
* [QTBUG-126401](https://bugreports.qt.io/browse/QTBUG-126401) Qt webengine leaks its WebEngineQuickWidget
* [QTBUG-113574](https://bugreports.qt.io/browse/QTBUG-113574) Incorrect sizing and bad text rendering with WebEngine
using fractional scaling on Wayland
* [QTBUG-125096](https://bugreports.qt.io/browse/QTBUG-125096) Print button WebEngine PDF viewer works only once
* [QTBUG-126722](https://bugreports.qt.io/browse/QTBUG-126722) WebEngine: GPU detection is missing "VmWare" in vendor
list
* [QTBUG-124878](https://bugreports.qt.io/browse/QTBUG-124878) --no-sandbox through command line does not seem to have
any effect
* [QTBUG-124110](https://bugreports.qt.io/browse/QTBUG-124110) [REG] Warning on WebEngineView creation
* [QTBUG-124172](https://bugreports.qt.io/browse/QTBUG-124172) FindGn: fix search path to find Gn when installed on the
host with custom install dirs
* [QTBUG-113636](https://bugreports.qt.io/browse/QTBUG-113636) qtwebengine: add option to build gn only
* [QTBUG-127318](https://bugreports.qt.io/browse/QTBUG-127318) QWebEngineView findText does not clear previous
findText's highlight results at certain conditions
* [QTBUG-111927](https://bugreports.qt.io/browse/QTBUG-111927) Link hovering may not change cursor shape in web view
* [QTBUG-123889](https://bugreports.qt.io/browse/QTBUG-123889) Qt webengine doesn't update cursor properly when
entering/leaving widgets
* [QTBUG-115929](https://bugreports.qt.io/browse/QTBUG-115929) [REG 6.3 -> 6.4/.5] Mouse cursor is pointer-only when
leaving window at bottom edge
* [QTBUG-127544](https://bugreports.qt.io/browse/QTBUG-127544) qtwebengine/examples/webenginewidgets/permissionbrowser
fail to compile with -Werror=format-security
* [QTBUG-126256](https://bugreports.qt.io/browse/QTBUG-126256) [REG 6.6 -> 6.7] WebOTP crashes renderer process
* [QTBUG-127611](https://bugreports.qt.io/browse/QTBUG-127611) [macOS] Crash on WebEngineView destruction
* [QTBUG-127758](https://bugreports.qt.io/browse/QTBUG-127758) tst_QWebEnginePage::dynamicFrame() failed on Ubuntu
24.04 offscreen(arm64) and X11(x64)
* [QTBUG-126049](https://bugreports.qt.io/browse/QTBUG-126049) text dump does not work realibly with 122-based
* [QTBUG-125300](https://bugreports.qt.io/browse/QTBUG-125300) Potential requirement on C runtime version for Qt 6.5.5
(and newer)?
* [QTBUG-124274](https://bugreports.qt.io/browse/QTBUG-124274) WebEngine build fails on openSUSE 15 due to libre2
* [QTBUG-126312](https://bugreports.qt.io/browse/QTBUG-126312) Persistent QML WebEngineProfile causes crash upon
loading a new website
* [QTBUG-120248](https://bugreports.qt.io/browse/QTBUG-120248) [Qt WebEngine] More configure-time checks and
documentation for required libraries
* [QTBUG-122407](https://bugreports.qt.io/browse/QTBUG-122407) bitbake meta-toolchain-qt6 fails with missing cups-
config
* [QTBUG-127464](https://bugreports.qt.io/browse/QTBUG-127464) Intel CET hardening needs an opt-out for WebEngine
* [QTBUG-120370](https://bugreports.qt.io/browse/QTBUG-120370) QQuickWebEngineDownloadItem is not public
* [QTBUG-128140](https://bugreports.qt.io/browse/QTBUG-128140) Dead link for QWebEngineScript::sourceUrl
* [QTBUG-127951](https://bugreports.qt.io/browse/QTBUG-127951) navigator.mediaDevices.enumerateDevices not returning
granted devices with PersistentPermissionsPolicy::AskEveryTime
* [QTBUG-127797](https://bugreports.qt.io/browse/QTBUG-127797) screen sharing capabilities over WebRTC is not working
* [QTBUG-127975](https://bugreports.qt.io/browse/QTBUG-127975) qtwebengine fails to build on msvc2022 (c++20)
* [QTBUG-119908](https://bugreports.qt.io/browse/QTBUG-119908) HTML &lt;select&gt; Element Triggers Program Crash in QT on
EGLFS/KMS Platforms
* [QTBUG-128381](https://bugreports.qt.io/browse/QTBUG-128381) [REG 6.8.0-> 6.9.0] toplevel no-gui build fails,
qtwebengine
* [QTBUG-127726](https://bugreports.qt.io/browse/QTBUG-127726) Screen sharing crashes in DesktopCapturer
* [QTBUG-128784](https://bugreports.qt.io/browse/QTBUG-128784) OpenGL context creation issues when D3D11 RHI is used
(sic)
* [QTBUG-108763](https://bugreports.qt.io/browse/QTBUG-108763) Incorrect documentation for
QWebEngineUrlRequestInterceptor.interceptRequest
* [QTBUG-128241](https://bugreports.qt.io/browse/QTBUG-128241) HTML selection tag crashes app when clicked on
* [QTBUG-128897](https://bugreports.qt.io/browse/QTBUG-128897) Pure virtual function call on
NativeSkiaOutputDevice::Present()
* [QTBUG-128846](https://bugreports.qt.io/browse/QTBUG-128846) [126-based][macOS]Failed assertion "A command encoder is
already encoding to this command buffer"
* [QTBUG-129826](https://bugreports.qt.io/browse/QTBUG-129826) [6.8] Minimum python version isn't correct anymore
* [QTBUG-129884](https://bugreports.qt.io/browse/QTBUG-129884) Webengine tests hang after
qmltests::GetUserMedia::test_getUserMedia(desktop video) on Windows 11
* [QTBUG-130034](https://bugreports.qt.io/browse/QTBUG-130034) Top flaky test:
tst_qwebenginepage::getUserMediaRequestDesktopVideoManyPages
* [QTBUG-130035](https://bugreports.qt.io/browse/QTBUG-130035) Top flaky test: tst_qwebenginepage::getUserMediaRequest
* [QTBUG-130327](https://bugreports.qt.io/browse/QTBUG-130327) Missing closing bracket in QWebEngineUrlSchemeHandler
documentation
* [QTBUG-129796](https://bugreports.qt.io/browse/QTBUG-129796) Blocking main frame request from a Google Search crashes
the process
* [QTBUG-130500](https://bugreports.qt.io/browse/QTBUG-130500) Various network tests are failing on macOS 15
* [QTBUG-130633](https://bugreports.qt.io/browse/QTBUG-130633) IDE source scanning cannot be disabled with qt-
configure-module
* [QTBUG-130599](https://bugreports.qt.io/browse/QTBUG-130599) [Regr: 6.7->6.8]JavascriptCanAccessClipboard doesn't
allowing copying to clipboard on 6.8
* [QTBUG-130790](https://bugreports.qt.io/browse/QTBUG-130790) error: 'cortex-a53' does not support feature 'crc'
* [QTBUG-131397](https://bugreports.qt.io/browse/QTBUG-131397) WebEngineProfile doesn't instantiate in QML if property
declarations are in a specific order
* [QTBUG-123095](https://bugreports.qt.io/browse/QTBUG-123095) Wheel scrolling issues in WebEngine
* [QTBUG-
131342](https://bugreports.qt.io/browse/QTBUG-131342) qtwebengine/src/core/compositor/native_skia_output_device_vulkan.
cpp:252:34: error: use of undeclared identifier 'importMemoryHandleInfo'
* [QTBUG-129153](https://bugreports.qt.io/browse/QTBUG-129153) Sporadic crash on NativeSkiaOutputDevice::BeginPaint()
* [QTBUG-131156](https://bugreports.qt.io/browse/QTBUG-131156) Scripts injected on DocumentReady and Deferred are not
always executed on google.com
* [QTBUG-
131794](https://bugreports.qt.io/browse/QTBUG-131794) qmltests::WebViewFindText::test_findTextInterruptedByLoad()
'function returned false' returned FALSE.
* [QTBUG-131304](https://bugreports.qt.io/browse/QTBUG-131304) Broken rendering when reparenting WebEngineView to
another window
* [QTBUG-131972](https://bugreports.qt.io/browse/QTBUG-131972) error: no matching function for call to
‘TestNamespace::QString::arg(const char [], TestNamespace::QString)
* [QTBUG-112746](https://bugreports.qt.io/browse/QTBUG-112746) QAnyStringView missing implicit conversion from char[]
with unknown size
* [QTBUG-131896](https://bugreports.qt.io/browse/QTBUG-131896) A sentence is cut in the middle in the Native Dialogs
section in Qt WebEngine features
* [QTBUG-131969](https://bugreports.qt.io/browse/QTBUG-131969) "Spellchecking can not be enabled" error logged when
disabling spell checking
* [QTBUG-132564](https://bugreports.qt.io/browse/QTBUG-132564) qwebengine-convert-dict fails on .dic wordlist
* [QTBUG-130608](https://bugreports.qt.io/browse/QTBUG-130608) Dropdown in WebEngineView are not zoomed and aligned
properly when parent of WebEngineView is zoomed.
* [QTBUG-128893](https://bugreports.qt.io/browse/QTBUG-128893) sbom for qtpdf gets lost , as it ends up as qtwebengine
sbom
* [QTBUG-132608](https://bugreports.qt.io/browse/QTBUG-132608) WebEngine assert with Wayland
* [QTBUG-132411](https://bugreports.qt.io/browse/QTBUG-132411) Chromium version isn't reduced in user-agent string
* [QTBUG-132682](https://bugreports.qt.io/browse/QTBUG-132682) [REG 6.9] Segfault in
{{QtWebEngineCore::NativeSkiaOutputDeviceOpenGL::texture()}} with
offscreen platform
* [QTBUG-127109](https://bugreports.qt.io/browse/QTBUG-127109) trouble configuring QtPDF for iOS
* [QTBUG-133558](https://bugreports.qt.io/browse/QTBUG-133558) DRM video fails to play on macOS
* [QTBUG-133590](https://bugreports.qt.io/browse/QTBUG-133590) tst_qwebengineview::keyboardFocusAfterPopup on macos
* [QTBUG-133649](https://bugreports.qt.io/browse/QTBUG-133649) When calling QWebEngineView::setFocus after calling
QWebEngineView::setFocus for the second time, focus is given to another
widget
* [QTBUG-131841](https://bugreports.qt.io/browse/QTBUG-131841) PdfScrollablePageView does not work in the app
* [QTBUG-133495](https://bugreports.qt.io/browse/QTBUG-133495) Missing Documentation of 3rd party component usage
* [QTBUG-133977](https://bugreports.qt.io/browse/QTBUG-133977) Undefined coin sanity check for offline-documentation
platform
* [QTBUG-134209](https://bugreports.qt.io/browse/QTBUG-134209) Deadlock on NVidia GPU or Vulkan rendeirng
* [QTBUG-123500](https://bugreports.qt.io/browse/QTBUG-123500) Unable to read out javascript engine version
* [QTBUG-126085](https://bugreports.qt.io/browse/QTBUG-126085) QQuickWebEngineProfile::defaultProfile() doesn't produce
a working profile
* [QTBUG-126546](https://bugreports.qt.io/browse/QTBUG-126546) Attribution documentation processed twice in CI
* [QTBUG-112281](https://bugreports.qt.io/browse/QTBUG-112281) Support ANGLE on Linux
* [QTBUG-127110](https://bugreports.qt.io/browse/QTBUG-127110) Platforms still use the inefficient qvsnprintf() fall-
back
* [QTBUG-126655](https://bugreports.qt.io/browse/QTBUG-126655) QtWebEngine fails Yocto CI build
* [QTBUG-119367](https://bugreports.qt.io/browse/QTBUG-119367) Downloading a PDF changes the current page icon
* [QTBUG-128308](https://bugreports.qt.io/browse/QTBUG-128308) [Windows] Startup crash in
gl::GLContextEGL::Initialize() on AMD GPUs
* [QTBUG-128653](https://bugreports.qt.io/browse/QTBUG-128653) tst_qquickwebengineview failed on
ubuntu-24.04-arm64-offscreen-tests
* [QTBUG-128652](https://bugreports.qt.io/browse/QTBUG-128652) tst_qmltests crashed on ubuntu-24.04-arm64-offscreen-
tests
* [QTBUG-126317](https://bugreports.qt.io/browse/QTBUG-126317) libexec/gn on MacOS is not universal
* [QTBUG-58669](https://bugreports.qt.io/browse/QTBUG-58669) printToPdf, QPageLayout margins overwrite CSS specified
margins
* [QTBUG-115764](https://bugreports.qt.io/browse/QTBUG-115764) [REG 5 -> 6] Hovering does not trigger elements on
websites with Wayland
* [QTBUG-131607](https://bugreports.qt.io/browse/QTBUG-131607) Crash on NativeSkiaOutputDeviceDirect3D11::texture()
with nullptr access
* [QTBUG-128875](https://bugreports.qt.io/browse/QTBUG-128875) [PDF] Zooming in and out the pdf file then opening
another one causes to app to crash
* [QTBUG-132331](https://bugreports.qt.io/browse/QTBUG-132331) missing udev documentation
* [QTBUG-129970](https://bugreports.qt.io/browse/QTBUG-129970) WebEngine Windows ARM support
* [COIN-1211](https://bugreports.qt.io/browse/COIN-1211) coin not able to build webengine winarm64 in reasonable
time
* [QTBUG-117478](https://bugreports.qt.io/browse/QTBUG-117478) qtwebengine h264 broken on Windows
* [QTBUG-131377](https://bugreports.qt.io/browse/QTBUG-131377) Include Chromium in SBOM
* [QTBUG-132479](https://bugreports.qt.io/browse/QTBUG-132479) [Windows] After download is interrupted,
QWebEngineDownloadRequest::resume() crashes with "Observers can only be
added once!"
* [QTBUG-132473](https://bugreports.qt.io/browse/QTBUG-132473) QWebEngineDownloadRequest::DownloadInterrupted creates
multiple, inconsistent QWebEngineDownloadRequest objects
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-133970](https://bugreports.qt.io/browse/QTBUG-133970) QtPDF spdx files not included in MinGW content

### qtwebview
* [QTBUG-70166](https://bugreports.qt.io/browse/QTBUG-70166) iOS Webview not able to return an object
* [QTBUG-102712](https://bugreports.qt.io/browse/QTBUG-102712) qtwebview tests fail on Android
* [QTBUG-108752](https://bugreports.qt.io/browse/QTBUG-108752) tst_QQuickWebView::settings_JS fails on Android 12
* [QTBUG-129303](https://bugreports.qt.io/browse/QTBUG-129303) [Android] WebView.loadHtml() fails to correctly encode
certain strings?
* [QTBUG-130559](https://bugreports.qt.io/browse/QTBUG-130559) Enable documentation testing in the CI for all Qt
submodules containing docs
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtcharts
* [QTBUG-127434](https://bugreports.qt.io/browse/QTBUG-127434) The labelsVisible property affects the titleVisible
property behavior if labelsVisible is set to false and titleVisible is
set to true.
* [QTBUG-127982](https://bugreports.qt.io/browse/QTBUG-127982) The QLineSeries hovered signal is only re-emitted when
the mouse leaves the hover area.
* [QTBUG-126452](https://bugreports.qt.io/browse/QTBUG-126452) qmltyperegistrar: Build warnings in qtcharts
* [QTBUG-130559](https://bugreports.qt.io/browse/QTBUG-130559) Enable documentation testing in the CI for all Qt
submodules containing docs
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtdatavis3d
* [QTBUG-127724](https://bugreports.qt.io/browse/QTBUG-127724) tst_qmltest_datavis crash on Ubuntu 24.04 offscreen
* [QTBUG-128460](https://bugreports.qt.io/browse/QTBUG-128460) Main window crashes/black out when QtDataVisualization
3D chart in QMdiSubWindow destroyed
* [QTBUG-118877](https://bugreports.qt.io/browse/QTBUG-118877) -qreal float configuration option does not compile
* [QTBUG-130559](https://bugreports.qt.io/browse/QTBUG-130559) Enable documentation testing in the CI for all Qt
submodules containing docs
* [QTBUG-129575](https://bugreports.qt.io/browse/QTBUG-129575)  Fix API flaw for QImage::mirror and QImage::mirrored
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtvirtualkeyboard
* [QTBUG-127120](https://bugreports.qt.io/browse/QTBUG-127120) CMake error in qtvirtualkeyboard: CMake Error: The
inter-target dependency graph contains the following strongly connected
component (cycle)
* [QTBUG-126842](https://bugreports.qt.io/browse/QTBUG-126842) VirtualKeyboard is always shown on primary screen
* [QTBUG-123416](https://bugreports.qt.io/browse/QTBUG-123416) [Qt Virtual Keyboard] Built-in style uses font family
that doesn't exist on all platforms
* [QTBUG-114551](https://bugreports.qt.io/browse/QTBUG-114551) [VKB] Selection handle coordinates fail to take
InputPanel's parent's transformation into account
* [QTBUG-128606](https://bugreports.qt.io/browse/QTBUG-128606) CMake Error: The inter-target dependency graph contains
the following strongly connected component (cycle)
* [QTBUG-130382](https://bugreports.qt.io/browse/QTBUG-130382) Can't disable Korean layout in yocto recipe
* [QTBUG-123415](https://bugreports.qt.io/browse/QTBUG-123415) [Qt Virtual Keyboard] Example produces lots of warnings
at startup
* [QTBUG-131347](https://bugreports.qt.io/browse/QTBUG-131347) Incorrect decimal point for German keyboard
* [QTBUG-127557](https://bugreports.qt.io/browse/QTBUG-127557) QtVirtualKeyboard crash introduced in 6.5.4
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-133241](https://bugreports.qt.io/browse/QTBUG-133241) VKB basic example's doc is missing cmake explanation

### qtscxml
* [QTBUG-131265](https://bugreports.qt.io/browse/QTBUG-131265) qtscxml fails after moc changes
* [QTBUG-132565](https://bugreports.qt.io/browse/QTBUG-132565) Questions about feature statemachine
* [QTBUG-134901](https://bugreports.qt.io/browse/QTBUG-134901) [REG 6.8.2 -> 6.9.0-RC] QStateMachine and QScxml qmake
projects do not compile
* [QTBUG-128173](https://bugreports.qt.io/browse/QTBUG-128173) Doc: Remove use of defunct QDoc command
"\tableofcontents"
* [QTBUG-128368](https://bugreports.qt.io/browse/QTBUG-128368) Make sure that also qt6_ CMake commands are in the help
index
* [QTBUG-130799](https://bugreports.qt.io/browse/QTBUG-130799) Remove or fix Q_OBJECT qdoc macro
* [QTBUG-132510](https://bugreports.qt.io/browse/QTBUG-132510) Superfluous optional components
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtspeech
* [QTBUG-108205](https://bugreports.qt.io/browse/QTBUG-108205) tst_QTextToSpeech::pauseResume(darwin) fails on macOS 13
in CI
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtnetworkauth
* [QTBUG-85377](https://bugreports.qt.io/browse/QTBUG-85377) callbackDataReceived is never emitted in
QOAuthHttpServerReplyHandler
* [QTBUG-66415](https://bugreports.qt.io/browse/QTBUG-66415) Access token callback clears scope
* [QTBUG-104655](https://bugreports.qt.io/browse/QTBUG-104655) QAbstractOAuth2::setState doesn't work as expected
* [QTBUG-128739](https://bugreports.qt.io/browse/QTBUG-128739) qtnetworkauth fail to build on MSVC C++20
* [QTBUG-129590](https://bugreports.qt.io/browse/QTBUG-129590) tst_oauth2 SSL certificate usage fails
* [QTBUG-129591](https://bugreports.qt.io/browse/QTBUG-129591) Remove QtWebEngine  hard dependency from OAuth2 doc
snippets application
* [QTBUG-65309](https://bugreports.qt.io/browse/QTBUG-65309) set header for Authorization when doing
QOAuth2AuthorizationCodeFlow::requestAccessToken()
* [QTBUG-129291](https://bugreports.qt.io/browse/QTBUG-129291) Use 127.0.0.1 instead of localhost as default in
QOAuth2AuthorizationCodeFlow
* [QTBUG-130159](https://bugreports.qt.io/browse/QTBUG-130159) [Reg 6.6.3 -> 6.7] QOAuth2AuthorizationCodeFlow uses
"localhost" as the redirect URI when it should be "127.0.0.1"
* [QTBUG-131948](https://bugreports.qt.io/browse/QTBUG-131948) OAuth2 expirationAt doest not change when invalidated
* [QTBUG-131949](https://bugreports.qt.io/browse/QTBUG-131949) Use UTC instead of local time for internal expiresAt
representation
* [QTBUG-132710](https://bugreports.qt.io/browse/QTBUG-132710) QtNetworkAuth's use of QStringList for scopes is not
matching RFC6749 Section 3.3 semantics
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtremoteobjects
* [QTBUG-128368](https://bugreports.qt.io/browse/QTBUG-128368) Make sure that also qt6_ CMake commands are in the help
index
* [QTBUG-130628](https://bugreports.qt.io/browse/QTBUG-130628) Assert fail in tst_usertypes::complexInQml
* [QTBUG-132738](https://bugreports.qt.io/browse/QTBUG-132738) Errors in some examples
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtlottie
* [QTBUG-127928](https://bugreports.qt.io/browse/QTBUG-127928) tst_bmtrimpath.cpp:243:59: error: use of overloaded
operator '+' is ambiguous
* [QTBUG-118877](https://bugreports.qt.io/browse/QTBUG-118877) -qreal float configuration option does not compile
* [QTBUG-130559](https://bugreports.qt.io/browse/QTBUG-130559) Enable documentation testing in the CI for all Qt
submodules containing docs
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtquicktimeline
* [QTBUG-122812](https://bugreports.qt.io/browse/QTBUG-122812) Binding is not restored for Timeline component
* [QTBUG-130559](https://bugreports.qt.io/browse/QTBUG-130559) Enable documentation testing in the CI for all Qt
submodules containing docs
* [QTBUG-131459](https://bugreports.qt.io/browse/QTBUG-131459) QDoc: No warning if \qmltype contains \inherits with
non-existing type
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtquick3d
* [QTBUG-125875](https://bugreports.qt.io/browse/QTBUG-125875) Manual test modelblendparticles segfaults on startup
* [QTBUG-125876](https://bugreports.qt.io/browse/QTBUG-125876) Instanced models are not taken into account in shadow
mapping bounds
* [QTBUG-125987](https://bugreports.qt.io/browse/QTBUG-125987) PickResult QML Type documentation no longer generated
* [QTBUG-126440](https://bugreports.qt.io/browse/QTBUG-126440) Bone texture not set for depth pre-pass (and possibly
other passes)
* [QTBUG-126657](https://bugreports.qt.io/browse/QTBUG-126657) Car configurator demo: shadow mapping glitches
* [QTBUG-127326](https://bugreports.qt.io/browse/QTBUG-127326) materialeditor binaries missing
* [QTBUG-127688](https://bugreports.qt.io/browse/QTBUG-127688) Remove obsolete Android Manifest Entries from examples
* [QTBUG-120001](https://bugreports.qt.io/browse/QTBUG-120001) Game can be played in the results screen in Qt Quick 3D
- Quick Ball example
* [QTBUG-127413](https://bugreports.qt.io/browse/QTBUG-127413) Building failure with FEATURE_quick_shadereffect=OFF
* [QTBUG-119888](https://bugreports.qt.io/browse/QTBUG-119888) Texts overlap with each other in Qt Quick3D
* [QTBUG-128370](https://bugreports.qt.io/browse/QTBUG-128370) Instance table cache not invalidated when instance table
is deleted
* [QTBUG-127878](https://bugreports.qt.io/browse/QTBUG-127878) XrVirtualMouse clicks not received by ListView delegates
* [QTBUG-128922](https://bugreports.qt.io/browse/QTBUG-128922) Invalid frustum dimensions in shadowmap shader
* [QTBUG-129140](https://bugreports.qt.io/browse/QTBUG-129140) [REG] Lightprobe using texture data causes crash
* [QTBUG-127760](https://bugreports.qt.io/browse/QTBUG-127760) qtdoc dice example debug assertion failure
* [QTBUG-129990](https://bugreports.qt.io/browse/QTBUG-129990) QtQuick3D.Xr crashes if the runtime doesn't support
depth swapchains
* [QTBUG-129807](https://bugreports.qt.io/browse/QTBUG-129807) qtquick3d doc generation fails without system OpenXR
* [QTBUG-129230](https://bugreports.qt.io/browse/QTBUG-129230) OrbitCameraController does not respect the camera
clipFar distance
* [QTBUG-130680](https://bugreports.qt.io/browse/QTBUG-130680) Building instructions visionOS
* [QTBUG-130398](https://bugreports.qt.io/browse/QTBUG-130398) volumeraycaster example can fail to start on Android
* [QTBUG-130381](https://bugreports.qt.io/browse/QTBUG-130381) quick3d/embree: AVX code paths not disabled with GCC 14
* [QTBUG-128352](https://bugreports.qt.io/browse/QTBUG-128352) Potential thread safety issue in many Qt Quick 3D
examples
* [QTBUG-129395](https://bugreports.qt.io/browse/QTBUG-129395) Qt Dice on mobile is "jumpy" while zooming
* [QTBUG-126316](https://bugreports.qt.io/browse/QTBUG-126316) Wrong timing for animations in XR
* [QTBUG-130647](https://bugreports.qt.io/browse/QTBUG-130647) hand property is missing in XrInputAction doc
* [QTBUG-126650](https://bugreports.qt.io/browse/QTBUG-126650) Directional light causes flickering with shadows.
* [QTBUG-128512](https://bugreports.qt.io/browse/QTBUG-128512) XrSpatialAnchorListModel filter properties do not work
* [QTBUG-131361](https://bugreports.qt.io/browse/QTBUG-131361) Intel skylake fails to build for Boot2Qt lts-6.5(.8)
* [QTBUG-128560](https://bugreports.qt.io/browse/QTBUG-128560) Lancelot test custom material error
* [QTBUG-132273](https://bugreports.qt.io/browse/QTBUG-132273) Quick3D runtime error with gcc >=12.1
* [QTBUG-127406](https://bugreports.qt.io/browse/QTBUG-127406) Add Path to entries of
qtquick3d/src/3rdparty/openxr/qt_attribution.json
* [QTBUG-132080](https://bugreports.qt.io/browse/QTBUG-132080) Directional light order influences shadow mapping
* [QTBUG-132081](https://bugreports.qt.io/browse/QTBUG-132081) Shadow mapping broken with orthographic camera
* [QTBUG-132838](https://bugreports.qt.io/browse/QTBUG-132838) Debug build fails at rendererimpl
* [QTBUG-132811](https://bugreports.qt.io/browse/QTBUG-132811) ExtendedSceneEnvironment does not work with multiview
* [QTBUG-133367](https://bugreports.qt.io/browse/QTBUG-133367) PointLight with shadows crashes XR application when
using vulkan backend
* [QTBUG-132042](https://bugreports.qt.io/browse/QTBUG-132042) Qt6Quick3DRuntimeRender crashes on Android
* [QTBUG-134291](https://bugreports.qt.io/browse/QTBUG-134291) ExtendedSceneEnvironment crash with multiview on HTC
Vive
* [QTBUG-124891](https://bugreports.qt.io/browse/QTBUG-124891) Unredistributable files in qt3d / qtquick3d
* [QTBUG-126193](https://bugreports.qt.io/browse/QTBUG-126193) Crash in XR when clicking on Slider in Android Style
* [QTBUG-67692](https://bugreports.qt.io/browse/QTBUG-67692) Clash with Qt's internal logging categories when building
project with a static build of Qt
* [QTBUG-125371](https://bugreports.qt.io/browse/QTBUG-125371) Problematic calling of qt_find_package(Qt6) in
qt_internal_project_setup
* [QTBUG-127110](https://bugreports.qt.io/browse/QTBUG-127110) Platforms still use the inefficient qvsnprintf() fall-
back
* [QTBUG-115450](https://bugreports.qt.io/browse/QTBUG-115450) qtquick3d -unity-build-batch-size 100000 fails
* [QTBUG-129575](https://bugreports.qt.io/browse/QTBUG-129575)  Fix API flaw for QImage::mirror and QImage::mirrored
* [QTBUG-130962](https://bugreports.qt.io/browse/QTBUG-130962) View3D inside XrItem's contentItem is not rendered
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtshadertools
* [QTBUG-126634](https://bugreports.qt.io/browse/QTBUG-126634) cmake/qsb fails to create the .qsb subdirectory
* [QTBUG-130559](https://bugreports.qt.io/browse/QTBUG-130559) Enable documentation testing in the CI for all Qt
submodules containing docs
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qt5compat
* [QTBUG-130392](https://bugreports.qt.io/browse/QTBUG-130392) Error: no matching function for call to
‘QChar::QChar(const qle_ushort&)
* [QTBUG-132209](https://bugreports.qt.io/browse/QTBUG-132209) Missing information on 'Qt 5 Compatibility APIs:
Graphical Effects' landing page
* [QTBUG-128173](https://bugreports.qt.io/browse/QTBUG-128173) Doc: Remove use of defunct QDoc command
"\tableofcontents"
* [QTBUG-122795](https://bugreports.qt.io/browse/QTBUG-122795) Incompatibility in QTextCodec between Qt5 and Qt6 (lack
of BOM)
* [QTBUG-130559](https://bugreports.qt.io/browse/QTBUG-130559) Enable documentation testing in the CI for all Qt
submodules containing docs
* [QTBUG-122798](https://bugreports.qt.io/browse/QTBUG-122798) [REG 5.15 -> 6.7 (or earlier)] QStringRef -> QStringView
conversion loses null-ness
* [QTBUG-122797](https://bugreports.qt.io/browse/QTBUG-122797) QStringRef doesn't convert to QAnyStringView
* [QTBUG-133892](https://bugreports.qt.io/browse/QTBUG-133892) QDoc: error: Documentation warnings (6) exceeded the
limit (0) for 'QtCore5Compat'.
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtcoap
* [QTBUG-130559](https://bugreports.qt.io/browse/QTBUG-130559) Enable documentation testing in the CI for all Qt
submodules containing docs
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtmqtt
* [QTBUG-132164](https://bugreports.qt.io/browse/QTBUG-132164) Qt 6.9 API Review/MQTT/COAP: Logging categories in
public headers
* [QTBUG-130559](https://bugreports.qt.io/browse/QTBUG-130559) Enable documentation testing in the CI for all Qt
submodules containing docs
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtopcua
* [QTBUG-131516](https://bugreports.qt.io/browse/QTBUG-131516) [reg] Fatal error C1067 when building qtopcua with
latest moc changes
* [QTBUG-127840](https://bugreports.qt.io/browse/QTBUG-127840) Windows ARM: qtopcua -
Tst_QOpcUaSecurity::keyPairs(open62541) fails
* [QTBUG-127931](https://bugreports.qt.io/browse/QTBUG-127931) error: ambiguous overload for ‘operator+’
* [QTBUG-127974](https://bugreports.qt.io/browse/QTBUG-127974) qtopcua fails to build on msvc2022 (c++20)
* [QTBUG-128749](https://bugreports.qt.io/browse/QTBUG-128749) qtopcua generates warnings about using
OpenSSL3-deprecated API
* [QTBUG-126631](https://bugreports.qt.io/browse/QTBUG-126631) AddressSanitizer: heap-use-after-free in tst_opcua
* [QTBUG-122005](https://bugreports.qt.io/browse/QTBUG-122005) qtopcua is not building against OpenSSL-1.1.1
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-133890](https://bugreports.qt.io/browse/QTBUG-133890) wrong licensing in
/Users/qt/work/install/sbom/qtopcua-6.10.0.source.spdx
* [QTBUG-133704](https://bugreports.qt.io/browse/QTBUG-133704) REG->6.9b3: OpcUA/Windows: Link error for QMetaObject in
namespace

### qtlanguageserver
* [QTBUG-128574](https://bugreports.qt.io/browse/QTBUG-128574) FTBFS with GCC 14: tReq may be used uninitialized
[-Werror=maybe-uninitialized]
* [QTBUG-67692](https://bugreports.qt.io/browse/QTBUG-67692) Clash with Qt's internal logging categories when building
project with a static build of Qt
* [QTBUG-115140](https://bugreports.qt.io/browse/QTBUG-115140) qtdeclarative -unity-build-batch-size 100000 fails
* [QTBUG-130559](https://bugreports.qt.io/browse/QTBUG-130559) Enable documentation testing in the CI for all Qt
submodules containing docs
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qthttpserver
* [QTBUG-127333](https://bugreports.qt.io/browse/QTBUG-127333) FAIL! :
tst_QHttpServerResponse::mimeTypeDetection(image/svg+xml) Compared
values are not the same
* [QTBUG-129798](https://bugreports.qt.io/browse/QTBUG-129798) Two-way communication for QWebSockets created in
QHttpServer does not work
* [QTBUG-132517](https://bugreports.qt.io/browse/QTBUG-132517) qthttpserver build fails when qlocalsockets are disabled
* [QTBUG-132748](https://bugreports.qt.io/browse/QTBUG-132748) Random assert fail in  tst_qhttpserverrequestfilter
* [QTBUG-105892](https://bugreports.qt.io/browse/QTBUG-105892) QHttpServer: afterRequest handlers are not executed
after each request
* [QTBUG-128113](https://bugreports.qt.io/browse/QTBUG-128113) API Review for qthttpserver module
* [QTBUG-129773](https://bugreports.qt.io/browse/QTBUG-129773) Mark Qt HTTP Server, Qt Protobuf, and Qt GRPC as
supported Add-On modules
* [QTBUG-130500](https://bugreports.qt.io/browse/QTBUG-130500) Various network tests are failing on macOS 15
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-129103](https://bugreports.qt.io/browse/QTBUG-129103) HttpServer documentation needs an overhaul
* [QTBUG-134250](https://bugreports.qt.io/browse/QTBUG-134250) qdoc fails to report warnings for incorrect \fn
signatures

### qtquick3dphysics
* [QTBUG-124796](https://bugreports.qt.io/browse/QTBUG-124796) QT quick 3d physics- Cannon example- shadow flickering
* [QTBUG-127319](https://bugreports.qt.io/browse/QTBUG-127319) Add command line help for cooker
* [QTBUG-127748](https://bugreports.qt.io/browse/QTBUG-127748) geometry_update crashed on Ubuntu 24.04 offscreen(arm64)
* [QTBUG-100100](https://bugreports.qt.io/browse/QTBUG-100100) Demos should use `qt6_add_qml_module` instead of
`qt6_add_resources`
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtgrpc
* [QTBUG-125375](https://bugreports.qt.io/browse/QTBUG-125375) QtGrpc: deadline doesn't respect server response
* [QTBUG-126480](https://bugreports.qt.io/browse/QTBUG-126480) ASAN: tst_grpc_client_unarycall SEGV on unknown address
0x000000000000
* [QTBUG-126451](https://bugreports.qt.io/browse/QTBUG-126451) gRPC: client-side streaming is throttling under high
load
* [QTBUG-124594](https://bugreports.qt.io/browse/QTBUG-124594) Protobuf deserialization is slow and the bottleneck for
a vectormap application
* [QTBUG-126383](https://bugreports.qt.io/browse/QTBUG-126383) CMake: Failed to find required Qt component
"ProtobufQuick".
* [QTBUG-127341](https://bugreports.qt.io/browse/QTBUG-127341) Error when building for Android:
qqmlgrpchttp2channel.cpp
* [QTBUG-126126](https://bugreports.qt.io/browse/QTBUG-126126) qtgrpc build fails on qemu-armv7-developer-build in dev
branch
* [QTBUG-127857](https://bugreports.qt.io/browse/QTBUG-127857) -skip-tests and -skip-examples are case sensitive
* [QTBUG-128174](https://bugreports.qt.io/browse/QTBUG-128174) magic8 SimpleGrpcServer.exe build failed with MinGW
* [QTBUG-119913](https://bugreports.qt.io/browse/QTBUG-119913) When accessing protobuf message properties, propety
values always detaches the internal shared data
* [QTBUG-127945](https://bugreports.qt.io/browse/QTBUG-127945) New example grpc/vehicle not compiling on iOS
* [QTBUG-129204](https://bugreports.qt.io/browse/QTBUG-129204) qgrpchttp2channel.cpp:19:10: fatal error:
'QtNetwork/qlocalsocket.h' file not found
* [QTBUG-129918](https://bugreports.qt.io/browse/QTBUG-129918) [FTBFS] gtgrpc: CMake Error: AUTOMOC for target
protocplugintestcommon: The "moc" executable "xxxx" does not exist.
* [QTBUG-131134](https://bugreports.qt.io/browse/QTBUG-131134) Compilation error: ‘class QGrpcChannelOptions’ has no
member named ‘sslConfiguration’
* [QTBUG-131577](https://bugreports.qt.io/browse/QTBUG-131577) FAIL!  :
tst_protobuf_repeated_qml::qtprotobufRepeatedTest::initTestCase()
Uncaught exception
* [QTBUG-131415](https://bugreports.qt.io/browse/QTBUG-131415) qtprotobufgen crashes on Any inside a oneof field
* [QTBUG-131417](https://bugreports.qt.io/browse/QTBUG-131417) qtprotobufgen: header guards with invalid C-identifier
* [QTBUG-129652](https://bugreports.qt.io/browse/QTBUG-129652) Messages that have the 'Repeated' suffix lead to name
clashing with the generated Repeated aliases
* [QTBUG-112423](https://bugreports.qt.io/browse/QTBUG-112423) QtProtobuf: Required.Proto3.ProtobufInput.ValidDataRepea
ted.ENUM.UnpackedInput.ProtobufOutput is failing
* [QTBUG-112425](https://bugreports.qt.io/browse/QTBUG-112425) QtProtobuf:  Recommended.Proto3.ProtobufInput.ValidDataR
epeated.ENUM.UnpackedInput.PackedOutput.ProtobufOutput test is failing
* [QTBUG-112424](https://bugreports.qt.io/browse/QTBUG-112424) QtProtobuf: Recommended.Proto3.ProtobufInput.ValidDataRe
peated.ENUM.UnpackedInput.DefaultOutput.ProtobufOutput test is failing
* [QTBUG-129588](https://bugreports.qt.io/browse/QTBUG-129588) QtGRPC: create a minimal overview example
* [QTBUG-125406](https://bugreports.qt.io/browse/QTBUG-125406) QtGrpc: rework documentation
* [QTBUG-132182](https://bugreports.qt.io/browse/QTBUG-132182) ProtobufQtCoreTypes: missing Qt includes for mapped
messages
* [QTBUG-130555](https://bugreports.qt.io/browse/QTBUG-130555) JSON serialization of google.protobuf.Timestamp seems to
be off
* [QTBUG-131780](https://bugreports.qt.io/browse/QTBUG-131780) GrpcQuick and ProtobufQuick are missing as necessary
dependencies for QML parameter for qt_add_protobuf and qt_add_grpc
* [QTBUG-131689](https://bugreports.qt.io/browse/QTBUG-131689) protobuf and grpc installation example should be clearer
* [QTBUG-132907](https://bugreports.qt.io/browse/QTBUG-132907) QtCore.proto and QtGui.proto are missing in developer
builds
* [QTBUG-132954](https://bugreports.qt.io/browse/QTBUG-132954) QDoc: error: Documentation warnings (2) exceeded the
limit (0) for 'QtProtobuf'
* [QTBUG-132848](https://bugreports.qt.io/browse/QTBUG-132848) qt_add_protobuf and qt_add_grpc should print a warning
if .proto files miss respective definitions
* [QTBUG-133937](https://bugreports.qt.io/browse/QTBUG-133937) Grpc: harden channel against error state reconnections
* [QTBUG-134266](https://bugreports.qt.io/browse/QTBUG-134266) grpc chat example doesn't install all libraries
* [QTBUG-134309](https://bugreports.qt.io/browse/QTBUG-134309) qgrpchttp2channel.cpp:121:25: error: unused variable
'HttpScheme' with developer build for Android
* [QTBUG-134439](https://bugreports.qt.io/browse/QTBUG-134439) qprotobufpropertyordering.cpp:313:47: error: comparison
of integers of different signs with x86 developer build for Android
* [QTBUG-67692](https://bugreports.qt.io/browse/QTBUG-67692) Clash with Qt's internal logging categories when building
project with a static build of Qt
* [QTBUG-125328](https://bugreports.qt.io/browse/QTBUG-125328) Grpc genenerators: implicitly created export.qpb.h is
broken
* [QTBUG-127174](https://bugreports.qt.io/browse/QTBUG-127174) protobuf scalar types stop working if registered using
QML_USING
* [QTBUG-128196](https://bugreports.qt.io/browse/QTBUG-128196) Make the move ctor default inlined in the generated code
* [QTBUG-128368](https://bugreports.qt.io/browse/QTBUG-128368) Make sure that also qt6_ CMake commands are in the help
index
* [QTBUG-123643](https://bugreports.qt.io/browse/QTBUG-123643) QtProtobuf: Extra Namespace option does not work
* [QTBUG-128753](https://bugreports.qt.io/browse/QTBUG-128753) Protobufgen/grpcgen tests override their results
* [QTBUG-129571](https://bugreports.qt.io/browse/QTBUG-129571) QtGRPC: verify examples
* [QTBUG-128468](https://bugreports.qt.io/browse/QTBUG-128468) Vehicle client example asserts on exit
* [QTBUG-132125](https://bugreports.qt.io/browse/QTBUG-132125) Clashing of Quick Components and Protobuf QML messages
* [QTBUG-120214](https://bugreports.qt.io/browse/QTBUG-120214) Add the support of implicit convertion of protobuf well-
known types from JSON input
* [QTBUG-132738](https://bugreports.qt.io/browse/QTBUG-132738) Errors in some examples
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-134273](https://bugreports.qt.io/browse/QTBUG-134273) QtGrpc: Abstract namespaces are not working with
QLocalSocket
* [QTBUG-134250](https://bugreports.qt.io/browse/QTBUG-134250) qdoc fails to report warnings for incorrect \fn
signatures

### qtquickeffectmaker
* [QTBUG-126255](https://bugreports.qt.io/browse/QTBUG-126255) Qt Quick Effect Maker ships copyrighted Rawpixel-sourced
images in violation of Rawpixel's Business License
* [QTBUG-111760](https://bugreports.qt.io/browse/QTBUG-111760) target_link_libraries(foo INTERFACE Qt::Core) fails for
interface libs with CMake < 3.19 on Windows
* [QTBUG-131809](https://bugreports.qt.io/browse/QTBUG-131809) cannot open Qt Quick Effect Maker in QDS
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtgraphs
* [QTBUG-126102](https://bugreports.qt.io/browse/QTBUG-126102) Grid on surface is not changing color
* [QTBUG-126269](https://bugreports.qt.io/browse/QTBUG-126269) Toggling labels off and on shows a empty label
* [QTBUG-125907](https://bugreports.qt.io/browse/QTBUG-125907) Autotest crashes at QBarSet::replace
* [QTBUG-126811](https://bugreports.qt.io/browse/QTBUG-126811) Crash in AreaSeries when no axis are defined
* [QTBUG-125470](https://bugreports.qt.io/browse/QTBUG-125470) Default series theme should be valid
* [QTBUG-126875](https://bugreports.qt.io/browse/QTBUG-126875) AreaSeries does not update if upper/lowerSeries is
manipulated in QML
* [QTBUG-127066](https://bugreports.qt.io/browse/QTBUG-127066) Surface gallery hide background toggle seems to do
nothing
* [QTBUG-125550](https://bugreports.qt.io/browse/QTBUG-125550) Incorrect interpretation of index 255 color in
QCustom3DVolume's colorTable
* [QTBUG-126506](https://bugreports.qt.io/browse/QTBUG-126506) Main view is rendered on top of slice view on resize
with widget apps
* [QTBUG-116628](https://bugreports.qt.io/browse/QTBUG-116628) Main graph enlarges on  top of slice view for a one
frame
* [QTBUG-119273](https://bugreports.qt.io/browse/QTBUG-119273) Qt Graphs axishandling example fails to build with
Boot2Qt
* [QTBUG-127348](https://bugreports.qt.io/browse/QTBUG-127348) Crash in widgetgraphgallery
* [QTBUG-127180](https://bugreports.qt.io/browse/QTBUG-127180) Color in slice view does not follow the background color
* [QTBUG-125782](https://bugreports.qt.io/browse/QTBUG-125782) Color scheme is not automatically updated if platform
color sceheme changes
* [QTBUG-126829](https://bugreports.qt.io/browse/QTBUG-126829) Docs for theme are incorrect
* [QTBUG-127500](https://bugreports.qt.io/browse/QTBUG-127500) Occasional crash when doing slice selection in surface
* [QTBUG-127498](https://bugreports.qt.io/browse/QTBUG-127498) Shadows do not work
* [QTBUG-127253](https://bugreports.qt.io/browse/QTBUG-127253) PointGroup pointer not deleted
* [QTBUG-127593](https://bugreports.qt.io/browse/QTBUG-127593) Docs for min & max camera zoom levels is incorrect
* [QTBUG-127105](https://bugreports.qt.io/browse/QTBUG-127105) PieSeries draws extra lines when moved to second monitor
* [QTBUG-127391](https://bugreports.qt.io/browse/QTBUG-127391) testbed pie graph stops responding when resized
* [QTBUG-127631](https://bugreports.qt.io/browse/QTBUG-127631) PieSeries labels don't hide when labelVisible set to
false
* [QTBUG-127502](https://bugreports.qt.io/browse/QTBUG-127502) Main view is wrong after return from slice view in
oscilloscope example
* [QTBUG-126830](https://bugreports.qt.io/browse/QTBUG-126830) C++ docs are incorrect after the widget & composition
change
* [QTBUG-126627](https://bugreports.qt.io/browse/QTBUG-126627) QtGraphs/6.8: Many uninitialized class member variables
* [QTBUG-127728](https://bugreports.qt.io/browse/QTBUG-127728) XYSeries is not removed from graph after clear() is
called
* [QTBUG-122267](https://bugreports.qt.io/browse/QTBUG-122267) Manual testing - data points in tst_minimalscatter stay
hidden
* [QTBUG-127743](https://bugreports.qt.io/browse/QTBUG-127743) Selecting a point with the same index from another
series does not work
* [QTBUG-127763](https://bugreports.qt.io/browse/QTBUG-127763) Selecting a point from another series leaves selected
point in previous series hidden
* [QTBUG-127734](https://bugreports.qt.io/browse/QTBUG-127734) tst_itemmodel crash
* [QTBUG-127765](https://bugreports.qt.io/browse/QTBUG-127765) PieSeries is not centered in view
* [QTBUG-127831](https://bugreports.qt.io/browse/QTBUG-127831) Build fails if one graphtype is disabled
* [QTBUG-127808](https://bugreports.qt.io/browse/QTBUG-127808) Slice view gets messed up with Legacy optimization
* [QTBUG-127877](https://bugreports.qt.io/browse/QTBUG-127877) Scatter graph item size does not update instantly
* [QTBUG-127879](https://bugreports.qt.io/browse/QTBUG-127879) A rectangle is visible in slice view if selectionMode
does not contain Item
* [QTBUG-127922](https://bugreports.qt.io/browse/QTBUG-127922) Triggers is valuetype assertion with gradients
* [QTBUG-127923](https://bugreports.qt.io/browse/QTBUG-127923) Warning in bars example
* [QTBUG-127932](https://bugreports.qt.io/browse/QTBUG-127932) Clear control points if points are 0
* [QTBUG-127801](https://bugreports.qt.io/browse/QTBUG-127801) Slice view is broken in QML for Bars3D
* [QTBUG-127497](https://bugreports.qt.io/browse/QTBUG-127497) Wrong bar mesh used after data range change
* [QTBUG-127496](https://bugreports.qt.io/browse/QTBUG-127496) Wrong axis label style after label style change
* [QTBUG-128213](https://bugreports.qt.io/browse/QTBUG-128213) Rendering issues with pie chart
* [QTBUG-128432](https://bugreports.qt.io/browse/QTBUG-128432) Graph Gallery example shows broken UI when resizing the
window
* [QTBUG-127769](https://bugreports.qt.io/browse/QTBUG-127769) Animation does not work in tst_directional
* [QTBUG-128799](https://bugreports.qt.io/browse/QTBUG-128799) The Graph Gallery crashes on launch on Android device
* [QTBUG-128490](https://bugreports.qt.io/browse/QTBUG-128490) Flickering when a single pie slice is shown in PieSeries
* [QTBUG-128889](https://bugreports.qt.io/browse/QTBUG-128889) WASM examples for 3D crash at start
* [QTBUG-128661](https://bugreports.qt.io/browse/QTBUG-128661) Barseries visibility signal called twice when changing
labels visibility
* [QTBUG-128863](https://bugreports.qt.io/browse/QTBUG-128863) connection issues when replacing barsets
* [QTBUG-129162](https://bugreports.qt.io/browse/QTBUG-129162) Add bound checks to QXYSeries
* [QTBUG-129138](https://bugreports.qt.io/browse/QTBUG-129138) tst_valueaxis::addAndDelete() crashes
* [QTBUG-129272](https://bugreports.qt.io/browse/QTBUG-129272) XYSeries count is an invokable function instead of a
property
* [QTBUG-129336](https://bugreports.qt.io/browse/QTBUG-129336) XYSeries pointsReplaced signal is not connected to
update
* [QTBUG-129054](https://bugreports.qt.io/browse/QTBUG-129054) [Boot2Qt] Surface of the graph is black when running the
example app on RPi device
* [QTBUG-129357](https://bugreports.qt.io/browse/QTBUG-129357) Multiple crashes while animating series
* [QTBUG-129381](https://bugreports.qt.io/browse/QTBUG-129381) Double signaling in DateTimeAxis
* [QTBUG-129352](https://bugreports.qt.io/browse/QTBUG-129352) [Boot2Qt] Cannot build "Cockpit" example app for Boot2Qt
device on Windows machine
* [QTBUG-129497](https://bugreports.qt.io/browse/QTBUG-129497) Linker error with QGraphsLine::swap: unresolved external
symbol
* [QTBUG-130507](https://bugreports.qt.io/browse/QTBUG-130507) Crash when mouse pressing PointRenderer graphs
* [QTBUG-126611](https://bugreports.qt.io/browse/QTBUG-126611) QCustom3DItem not scaled properly
* [QTBUG-130013](https://bugreports.qt.io/browse/QTBUG-130013) Setting selection item label visibility to false does
not work
* [QTBUG-130722](https://bugreports.qt.io/browse/QTBUG-130722) Bar3DSeries columnLabels and rowLabels not working.
* [QTBUG-130010](https://bugreports.qt.io/browse/QTBUG-130010) userDefinedMesh is ignored
* [QTBUG-130011](https://bugreports.qt.io/browse/QTBUG-130011) Changing selection pointer mesh with Surface3D does not
work
* [QTBUG-130870](https://bugreports.qt.io/browse/QTBUG-130870) Selection pointer does not follow highlight color
immediately
* [QTBUG-127800](https://bugreports.qt.io/browse/QTBUG-127800) Graphs3D namespace docs are missing from QML
* [QTBUG-131123](https://bugreports.qt.io/browse/QTBUG-131123) Docs mention non-existent Graphs3D.CameraPreset.None
enum value
* [QTBUG-131124](https://bugreports.qt.io/browse/QTBUG-131124) GraphsTheme documentation ambiguities
* [QTBUG-131140](https://bugreports.qt.io/browse/QTBUG-131140) LogValue3DAxisFormatter "edgeLabelsVisible" or
"showEdgeLabels" bug
* [QTBUG-131138](https://bugreports.qt.io/browse/QTBUG-131138) Custom3DLabel absolute position and scaling bugs
* [QTBUG-131121](https://bugreports.qt.io/browse/QTBUG-131121) GraphTransition description example unorthodox
indentation
* [QTBUG-131278](https://bugreports.qt.io/browse/QTBUG-131278) Qt cockpit example .qrc file missing
* [QTBUG-131366](https://bugreports.qt.io/browse/QTBUG-131366) Incorrect import and linking target hint for
Q3DSurfaceWidgetItem
* [QTBUG-129824](https://bugreports.qt.io/browse/QTBUG-129824) heightMapFile fails silently if the filename is
incorrect or cannot be found
* [QTBUG-131118](https://bugreports.qt.io/browse/QTBUG-131118) SplineSeries inherits XYSeries, but the documentation
indicates otherwise
* [QTBUG-131423](https://bugreports.qt.io/browse/QTBUG-131423) QBarDataItem::setRotation does not work as expected
* [QTBUG-131119](https://bugreports.qt.io/browse/QTBUG-131119) GraphPointAnimation and SplineControlAnimation have no
properties at all according to the docs
* [QTBUG-131473](https://bugreports.qt.io/browse/QTBUG-131473) Q3DGraphsWidgetItem::customItems() always returns empty
list
* [QTBUG-129767](https://bugreports.qt.io/browse/QTBUG-129767) Axis titleColor doesn't follow theming
* [QTBUG-129109](https://bugreports.qt.io/browse/QTBUG-129109) Unused signals in Q3DGraphsWidgetItem
* [QTBUG-127689](https://bugreports.qt.io/browse/QTBUG-127689) DirectToBackground and qDefaultSurfaceFormat are
probably incorrect
* [QTBUG-131730](https://bugreports.qt.io/browse/QTBUG-131730) aspectRatio and horizontalAspectRatio can be assigned
negative values
* [QTBUG-131120](https://bugreports.qt.io/browse/QTBUG-131120) GraphPointAnimation doesn't work with ScatterSeries
* [QTBUG-131735](https://bugreports.qt.io/browse/QTBUG-131735) Invalid value can be set to barThickness
* [QTBUG-131733](https://bugreports.qt.io/browse/QTBUG-131733) Invalid preset can be assigned to theme
* [QTBUG-131734](https://bugreports.qt.io/browse/QTBUG-131734) Invalid value can be assigned to renderingMode
* [QTBUG-131736](https://bugreports.qt.io/browse/QTBUG-131736) Graphs update even if nothing has changed
* [QTBUG-131796](https://bugreports.qt.io/browse/QTBUG-131796) qgraphstheme.cpp:5:10: fatal error: utils_p.h: No such
file or directory
* [QTBUG-131635](https://bugreports.qt.io/browse/QTBUG-131635) Selected points label flips when adjusting font size
* [QTBUG-131872](https://bugreports.qt.io/browse/QTBUG-131872) Docs missing for labelSize and scaleLabelsByCount
* [QTBUG-131853](https://bugreports.qt.io/browse/QTBUG-131853) Shadow-like artefacts on surface graph
* [QTBUG-128235](https://bugreports.qt.io/browse/QTBUG-128235)  QAbstract3DSeries::setBaseColor does not support
transparent colors
* [QTBUG-131112](https://bugreports.qt.io/browse/QTBUG-131112) Vertical ValueAxis title with labels overlap
* [QTBUG-131890](https://bugreports.qt.io/browse/QTBUG-131890) Q3DBarsWidgetItem - documentation does not match snippet
* [QTBUG-131854](https://bugreports.qt.io/browse/QTBUG-131854) Documentation is missing from some GraphsWidgets methods
* [QTBUG-132084](https://bugreports.qt.io/browse/QTBUG-132084) Legend data returns wrong colors for XYSeries
* [QTBUG-132082](https://bugreports.qt.io/browse/QTBUG-132082) Points can be dragged away from line even if series not
draggable
* [QTBUG-132083](https://bugreports.qt.io/browse/QTBUG-132083) Bar series rendering broken
* [QTBUG-132159](https://bugreports.qt.io/browse/QTBUG-132159) Surface3D requires 2 clicks to display selection pointer
* [QTBUG-132335](https://bugreports.qt.io/browse/QTBUG-132335) API comparison issues in QGraphsWidget
* [QTBUG-132336](https://bugreports.qt.io/browse/QTBUG-132336) API comparison issues in Graphs
* [QTBUG-132396](https://bugreports.qt.io/browse/QTBUG-132396) API comparison findings: transparencyTechnique is not
documented in Q3DGraphsWidgetItem
* [QTBUG-132402](https://bugreports.qt.io/browse/QTBUG-132402) SplineSeries remove() malfunctions when used with
GraphPointAnimation
* [QTBUG-129425](https://bugreports.qt.io/browse/QTBUG-129425) Unused signals in 2D side
* [QTBUG-132745](https://bugreports.qt.io/browse/QTBUG-132745) borderVisible property not working in Custom3DLabel in
QtGraphs.
* [QTBUG-132596](https://bugreports.qt.io/browse/QTBUG-132596) plotAreaBackgroundVisible of GraphsTheme not work
* [QTBUG-132132](https://bugreports.qt.io/browse/QTBUG-132132) Panning with left mouse button doesn't work
* [QTBUG-132766](https://bugreports.qt.io/browse/QTBUG-132766) Camera cannot be rotated below a graph with negative
bars
* [QTBUG-132753](https://bugreports.qt.io/browse/QTBUG-132753) GraphAnimation crashes eventually with out of range
* [QTBUG-132611](https://bugreports.qt.io/browse/QTBUG-132611) can't remove margin of GraphsView
* [QTBUG-128656](https://bugreports.qt.io/browse/QTBUG-128656) Unclear usage of
QT_DECLARE_QESDP_SPECIALIZATION_DTOR_WITH_EXPORT
* [QTBUG-133479](https://bugreports.qt.io/browse/QTBUG-133479) Surface Graphs show z-fighting
* [QTBUG-125753](https://bugreports.qt.io/browse/QTBUG-125753) Fix PointRenderer series add/remove/visibility
* [QTBUG-125752](https://bugreports.qt.io/browse/QTBUG-125752) Fix AreaRenderer series add/remove/visibility
* [QTBUG-125886](https://bugreports.qt.io/browse/QTBUG-125886) QtGraphs namespace should be QtGraphs3D instead of
QGraphs3D
* [QTBUG-125754](https://bugreports.qt.io/browse/QTBUG-125754) Fix PieRenderer series add/remove/visibility
* [QTBUG-126653](https://bugreports.qt.io/browse/QTBUG-126653) Weird implementation in QBarSet
* [QTBUG-127043](https://bugreports.qt.io/browse/QTBUG-127043) Add missing FINAL in QDateTimeAxis
* [QTBUG-127045](https://bugreports.qt.io/browse/QTBUG-127045) Pass QString by const ref in QDateTimeAxis
* [QTBUG-126662](https://bugreports.qt.io/browse/QTBUG-126662) 2D Graphs: low performance on scrolling axis
* [QTBUG-127270](https://bugreports.qt.io/browse/QTBUG-127270) Spline hover positioning not correct
* [QTBUG-127118](https://bugreports.qt.io/browse/QTBUG-127118) Check qsizetype validity across classes
* [QTBUG-127719](https://bugreports.qt.io/browse/QTBUG-127719) Check examples for memory issues
* [QTBUG-118877](https://bugreports.qt.io/browse/QTBUG-118877) -qreal float configuration option does not compile
* [QTBUG-128251](https://bugreports.qt.io/browse/QTBUG-128251) QBarSeries clicked Signal Not Emitted in Qt 6.8.0 Beta3
(Graphs: 2D)
* [QTBUG-125480](https://bugreports.qt.io/browse/QTBUG-125480) Issues on 3d widget graph examples
* [QTBUG-128898](https://bugreports.qt.io/browse/QTBUG-128898) qmlTestBed barModelMapping not working correctly
* [QTBUG-130306](https://bugreports.qt.io/browse/QTBUG-130306) Documentation with source code mismatch
* [QTBUG-130649](https://bugreports.qt.io/browse/QTBUG-130649) Invalid GraphTheme code snippet in QtGraphs
Documentation
* [QTBUG-130655](https://bugreports.qt.io/browse/QTBUG-130655) Qt Graphs GraphsTheme gridVisible: false does not hide
the grid
* [QTBUG-131131](https://bugreports.qt.io/browse/QTBUG-131131) Graphs3D related documentation bugs
* [QTBUG-131136](https://bugreports.qt.io/browse/QTBUG-131136) 3D scatter graph bugs
* [QTBUG-122089](https://bugreports.qt.io/browse/QTBUG-122089) Graphs3D.RenderingMode.DirectToBackground causes crashes
in autotests
* [QTBUG-129575](https://bugreports.qt.io/browse/QTBUG-129575)  Fix API flaw for QImage::mirror and QImage::mirrored
* [QTBUG-131117](https://bugreports.qt.io/browse/QTBUG-131117) Pie graph bugs
* [QTBUG-131846](https://bugreports.qt.io/browse/QTBUG-131846) GraphsView missing plot area and ticks inside dialog
* [QTBUG-132009](https://bugreports.qt.io/browse/QTBUG-132009) LegendData cannot be instantiated
* [QTBUG-131111](https://bugreports.qt.io/browse/QTBUG-131111) LineSeries bugs
* [QTBUG-132107](https://bugreports.qt.io/browse/QTBUG-132107) 3D surface graph bugs
* [QTBUG-119683](https://bugreports.qt.io/browse/QTBUG-119683) Surface Graph Gallery example not fully responsive
* [QTBUG-132401](https://bugreports.qt.io/browse/QTBUG-132401) SplineSeries removeMultiple() malfunctioning and
incorrectly documented
* [QTBUG-133359](https://bugreports.qt.io/browse/QTBUG-133359) qtGraphs ValueAxis labelFormat does not support the same
formatting options that the qtCharts one
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtapplicationmanager (Commercial only)
* [QTBUG-127679](https://bugreports.qt.io/browse/QTBUG-127679) error: no member named 'listen' in 'QHttpServer'
* [QTBUG-128107](https://bugreports.qt.io/browse/QTBUG-128107) error: use of undeclared identifier 'qsnprintf'; did you
mean 'vsnprintf'?
* [QTBUG-127933](https://bugreports.qt.io/browse/QTBUG-127933) [REG 6.8.0 beta2->beta3] applicationmanager examples not
compiling on iOS
* [QTBUG-128212](https://bugreports.qt.io/browse/QTBUG-128212) FAIL!  : qml::ApplicationManager::test_startAndStopAllAp
plications(StopAllApplications) Uncaught exception: Cannot read property
'modelData' of null
* [QTBUG-129814](https://bugreports.qt.io/browse/QTBUG-129814) applicationmanager\application-
features\apps\Glitches\Glitches\glitches.cpp(4): fatal error C1083:
Cannot open include file: 'unistd.h': No such file or directory
* [QTBUG-130117](https://bugreports.qt.io/browse/QTBUG-130117) build time paths used in appman binaries
* [QTBUG-130388](https://bugreports.qt.io/browse/QTBUG-130388) application-features example has broken
* [QTBUG-132585](https://bugreports.qt.io/browse/QTBUG-132585) error: ignoring return value of function declared with
'nodiscard' attribute [-Werror,-Wunused-result]
* [QTBUG-132649](https://bugreports.qt.io/browse/QTBUG-132649) qtapplicationmanager fails yocto / meta-qt6 CI with
CMake errors
* [QTBUG-132693](https://bugreports.qt.io/browse/QTBUG-132693) error: ignoring return value of function declared with
'nodiscard' attribute [-Werror,-Wunused-result]
* [QTBUG-133208](https://bugreports.qt.io/browse/QTBUG-133208) warning C4996:
'QSortFilterProxyModel::invalidateFilter': Use begin/endFilterChange()
instead
* [QTBUG-133605](https://bugreports.qt.io/browse/QTBUG-133605) Bubblewrap plugin is not handling bwrap option order
correctly
* [QTBUG-134214](https://bugreports.qt.io/browse/QTBUG-134214) [WARN | am.system] when running 'hello-world' on Boot to
Qt
* [QTBUG-134539](https://bugreports.qt.io/browse/QTBUG-134539) Failed to verify signature (no chain of trust)
* [QTBUG-99702](https://bugreports.qt.io/browse/QTBUG-99702) Qt module -tools package has both compile time and
runtime tools
* [QTBUG-129488](https://bugreports.qt.io/browse/QTBUG-129488) FAIL!  : qml::BubbleWrap::test_bubblewrap() 'wait for
signal windowAdded' returned FALSE. ()
* [QTBUG-130554](https://bugreports.qt.io/browse/QTBUG-130554) tst_Signature::check() fails on macOS 15
* [QTBUG-130869](https://bugreports.qt.io/browse/QTBUG-130869) tst_applicationmanager_multi-process (Failed)

### qtinterfaceframework (Commercial only)
* [QTBUG-127627](https://bugreports.qt.io/browse/QTBUG-127627) AttributeError: type object 'Path' has no attribute
'getcwd'
* [QTBUG-128501](https://bugreports.qt.io/browse/QTBUG-128501) [Boot to Qt 6.8.0 beta4] "module
"Example.If.RemoteModule" is not installed" when running 'remote'
application on a Boot to Qt device
* [QTBUG-128117](https://bugreports.qt.io/browse/QTBUG-128117) [REG Qt 6.7.2-> 6.8.0 beta1-3] interfaceframework/remote
not compiling with Android binaries
* [QTBUG-130868](https://bugreports.qt.io/browse/QTBUG-130868) tst_simulation_backend_static (Failed)
* [QTBUG-131579](https://bugreports.qt.io/browse/QTBUG-131579) [REG 6.8.0->6.8.1] building interfaceframework/remote
has FAILED and SUCCESFULL statements in output
* [QTBUG-132791](https://bugreports.qt.io/browse/QTBUG-132791) Attempt to promote imported target
"Python3::Interpreter" to global scope
* [QTBUG-133958](https://bugreports.qt.io/browse/QTBUG-133958) QDoc: error: Documentation warnings (9) exceeded the
limit (0) for 'QtInterfaceFramework'.
* [QTBUG-124279](https://bugreports.qt.io/browse/QTBUG-124279) Interfaceframework examples don't get deployed to
embedded devices
* [QTBUG-130082](https://bugreports.qt.io/browse/QTBUG-130082) Doc: wrong annotation name for defaultServerMode
* [QTBUG-134684](https://bugreports.qt.io/browse/QTBUG-134684) A crash occurred in C:\Users\qt\work\qt\qtinterfaceframe
work_standalone_tests\tests\auto\core\qifabstractfeature\tst_qifabstract
feature.exe.

### qmlcompilerplus (Commercial only)
* [QTBUG-127469](https://bugreports.qt.io/browse/QTBUG-127469) [Reg 6.7 -> 6.8.0b2] IconLabel fails to compile with
qmlsc Direct Mode
* [QTBUG-127930](https://bugreports.qt.io/browse/QTBUG-127930) FAIL!  : tst_CodeGen::enums() Not all expected messages
were received
* [QTBUG-128262](https://bugreports.qt.io/browse/QTBUG-128262) error: invalid covariant return type for â€˜virtual
std::variant<QQmlJSAotFunction
* [QTBUG-124913](https://bugreports.qt.io/browse/QTBUG-124913) Weird compiler warning message when using unresolved
function

### qtinsighttracker (Commercial only)
* [QTBUG-128116](https://bugreports.qt.io/browse/QTBUG-128116) [REG 6.7.2->6.8.0beta1-3] insighttracker/coffee not
compiling with Android binaries
* [QTBUG-132041](https://bugreports.qt.io/browse/QTBUG-132041) FAIL!  : tst_QInsightEventFilter::trackEvents(empty.qml)
Compared values are not the same
* [QTBUG-128736](https://bugreports.qt.io/browse/QTBUG-128736) DOC: Add missing configuration value
* [QTBUG-132587](https://bugreports.qt.io/browse/QTBUG-132587) error: ignoring return value of function declared with
'nodiscard' attribute [-Werror,-Wunused-result]
* [QTBUG-126979](https://bugreports.qt.io/browse/QTBUG-126979) CMake error in dev' branch dependency update round:
package "Qt6InsightTracker"  is considered to be NOT FOUND
* [QTBUG-127678](https://bugreports.qt.io/browse/QTBUG-127678) error: no member named 'sslSetup' in 'QHttpServer'
* [QTBUG-67692](https://bugreports.qt.io/browse/QTBUG-67692) Clash with Qt's internal logging categories when building
project with a static build of Qt

### qtvncserver (Commercial only)
* [QTBUG-126399](https://bugreports.qt.io/browse/QTBUG-126399) Dependency update on qt/qtdeviceutilities is failing in
6.8 .
* [QTBUG-130436](https://bugreports.qt.io/browse/QTBUG-130436) warning C4996: 'lcVncVerbose': Use
Q_STATIC_LOGGING_CATEGORY or add either Q_DECLARE_LOGGING_CATEGORY or
QT_DECLARE_EXPORTED_QT_LOGGING_CATEGORY in a header
* [QTBUG-67692](https://bugreports.qt.io/browse/QTBUG-67692) Clash with Qt's internal logging categories when building
project with a static build of Qt
* [QTBUG-128535](https://bugreports.qt.io/browse/QTBUG-128535) QVncServer documentation is missing some signals

Known Issues
------------
* Check that your system meets Qt's requirements:
https://doc.qt.io/qt-6.9/supported-platforms.html
* RTA reported issues from Qt 6.9
https://qt-project.atlassian.net/issues/?filter=10496
* See Qt 6.9 known issues from:
https://wiki.qt.io/Qt_6.9_Known_Issues
* Qt 6.9.0 Open issues in Jira:
https://qt-project.atlassian.net/issues/?filter=10527

Credits for the  release goes to:
---------------------------------

Eirik Aavitsland  
Laszlo Agocs  
Dilek Akcay  
Owais Akhtar  
Dmitrii Akshintsev  
Konsta Alajärvi  
Anu Aliyas  
Even Oscar Andersen  
Tim Angus  
Dimitrios Apostolou  
Soheil Armin  
Viktor Arvidsson  
Albert Astals Cid  
Alessandro Astone  
YAMAMOTO Atsushi  
Xavier BESSON  
Andreas Bacher  
Mate Barany  
Thierry Bastian  
Matthias Behr  
Vladimir Belyavsky  
Nicholas Bennett  
Stephan Bergmann  
Eric Beuque  
Lena Biliaieva  
Janet Blackquill  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
David Boddie  
Tatiana Borisova  
Joerg Bornemann  
Rym Bouabid  
Assam Boudjelthia  
Sven Brauch  
Aurélien Brooke  
Kai Uwe Broulik  
Michael Brüning  
Alex Bu  
Olivier De Cannière  
Alexei Cazacov  
Brian Chan  
Kaloyan Chehlarski  
Mike Chen  
Michael Cho  
Wang Chuan   
Ed Cooke  
Miguel Costa  
Alexandru Croitor  
Christoph Cullmann  
Kenneth Culver  
Mitch Curtis  
Thibaut Cuvelier  
Giuseppe D'Angelo  
Szabolcs David  
Ali Can Demiralp  
Pieter Dewachter  
Pavel Dubsky  
Artem Dyomin  
Alexey Edelev  
David Edmundson  
Oliver Eftevaag  
Christian Ehrlicher  
Nikolaus Einhauser  
Hatem ElKharashy  
Andreas Eliasson  
Amr Essam  
David Faure  
Ilya Fedin  
Nicolas Fella  
Ilya Flikov  
Andrew Forrest  
Dheerendra FullName  
Isak Fyksen  
Simo Fält  
Samuel Gaist  
Zoltan Gera  
Nazar Gerasymchuk  
Federico Giovanardi  
Joshua Goins  
Alexander Golubev  
Julian Greilich  
Robert Griebl  
Magnus Groß  
Jan Grulich  
Johannes Grunenberg  
Kaj Grönholm  
Richard Moe Gustavsen  
Balló György  
Lucie Gérard  
Mikko Hallamaa  
Jøger Hansegård  
Inkamari Harjula  
Andre Hartmann  
Elias Hautala  
Jani Heikkinen  
Tero Heikkinen  
Miikka Heikkinen  
Moss Heim  
Christian Heimlich  
Jari Helaakoski  
Liu Heng  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Dominik Holland  
Zhang Hongyuan  
Mats Honkamaa  
Botond István Horváth  
Samuli Hölttä  
Sam James  
Masoud Jami  
Morteza Jamshidi  
Johnny Jazeix  
Allan Sandfeld Jensen  
Jukka Jokiniva  
Teemu Jokitulppo  
Tomasz Kalisiak  
Jonas Karlsson  
Timothée Keller  
Igor Khanin  
Ahmed El Khazari  
Ali Kianian  
Marius Kittler  
Friedemann Kleint  
Peter Kling  
André Klitzing  
Michal Klocek  
Ingo Klöcker  
Yuri Knigavko  
Jarek Kobus  
Tobias Koenig  
Sze Howe Koh  
Jarkko Koivikko  
Niko Korkala  
Tomi Korpipää  
Fabian Kosmale  
Volker Krause  
Mike Krus  
Santhosh Kumar  
Jonas Kvinge  
Kai Köhne  
Lauri Laanmets  
Cristian Le  
Cage Lee  
Inho Lee  
Frédéric Lefebvre  
Paul Lemire  
Chris Lerner  
Wladimir Leuschner  
Qiang Li  
Liu Linsong  
Felix Lionardo  
Jie Liu  
Heng Liu  
Jarno Lämsä  
Robert Löhning  
Thiago Macieira  
Andras Mantia  
Christophe Marin  
Jonathan Marten  
Thorbjørn Lund Martsum  
Łukasz Matysiak  
Leena Miettinen  
Shveta Mittal  
Jan Moeller  
Thomas Moerschell  
Safiyyah Moosa  
Bartlomiej Moskal  
Marc Mutz  
Tommi Mänttäri  
Antti Määttä  
Martin Negyokru  
Andy Nichols  
Mårten Nordheim  
Dennis Oberst  
Daniel Opitz  
Eimen Oueslati  
Matti Paaso  
Tinja Paavoseppä  
Kwanghyo Park  
Ari Parkkila  
David C. Partridge  
Jerome Pasion  
Evgen Pervenenko  
Samuli Piippo  
Karim Pinter  
Timur Pocheptsov  
Lauri Pohjanheimo  
Milla Pohjanheimo  
Joni Poikelin  
Aleix Pol  
Rami Potinkara  
Lorn Potter  
Sakaria Pouke  
Shyamnath Premnadh  
Dheerendra Purohit  
MohammadHossein Qanbari  
Liang Qi  
Khem Raj  
Matthias Rauter  
David Redondo  
Arno Rehn  
Topi Reinio  
Jaime Resano  
Shawn Rutledge  
Toni Saario  
Filip Sajdak  
Ahmad Samir  
Timon Sassor  
Lars Schmertmann  
Philip Schuchardt  
David Schulz  
Carl Schwan  
Luca Di Sera  
Dmitry Shachnev  
Sami Shalayel  
Jiu Shanheng  
Andy Shaw  
Tian Shilin  
Venugopal Shivashankar  
Pierre-Yves Siret  
Harald Sitter  
Nils Petter Skålerud  
Nils Petter Skålerud  
Daniel Smith  
Ivan Solovev  
Thomas Sondergaard  
Axel Spoerl  
Patryk Stachniak  
Patrick Stewart  
Magdalena Stojek  
Martin Storsjö  
Brett Stottlemyer  
Christian Strømme  
Tarja Sundqvist  
Audun Sutterud  
Lars Sutterud  
Tasuku Suzuki  
Jan Arve Sæther  
Morten Sørvig  
Sadegh Taghavi  
HIDAKA Takahiro  
Vladislav Tarakanov  
Nodir Temirkhodjaev  
Benjamin Terrier  
Samuel Thibault  
Phil Thompson  
Christian Tismer  
Ivan Tkachenko  
Elias Toivola  
Orkun Tokdemir  
Pino Toscano  
Jens Trillmann  
Jere Tuliniemi  
Shantanu Tushar  
Paul Olav Tvete  
Esa Törmänen  
Fatih Uzunoglu  
Tuomas Vaarala  
Sami Varanka  
Peter Varga  
Niccolò Venerandi  
Doris Verria  
Tor Arne Vestbø  
Petri Virkkunen  
Jannis Voelker  
Ville Voutilainen  
Juha Vuolle  
Olli Vuolteenaho  
Jaishree Vyas  
Jannis Völker  
Dongmei Wang  
Gary Wang  
David Warner  
Ole Wegen  
Michael Weghorn  
Bernd Weimer  
Edward Welbourne  
Fushan Wen  
Paul Wicking  
Piotr Wierciński  
Milian Wolff  
Oliver Wolff  
YaoBing Xiao  
Li Xinwei  
Shitong Xu  
Lu YaNing  
Semih Yavuz  
Marianne Yrjänä  
Wang Yu  
Zhao Yuhang  
Vlad Zahorodnii  
Alexey Zerkin  
JiDe Zhang  
Chen Zhanwang  
Yuhang Zhao  
Liu Zheng  
Yifan Zhu  
Wang Zichong  
Eike Ziller  
hjk  
Michał Łoś  
