Release notes
=============
Qt 6.11 introduces many new features and improvements as well as bugfixes
over the 6.10.x series. For more details, refer to the online
documentation included in this distribution. The documentation is also
available online:

https://doc.qt.io/qt-6/whatsnew611.html

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
* [CVE-2025-5992](https://nvd.nist.gov/vuln/detail/CVE-2025-5992) in qtbase
* [CVE-2025-6338](https://nvd.nist.gov/vuln/detail/CVE-2025-6338) in qtbase
* [CVE-2025-12385](https://nvd.nist.gov/vuln/detail/CVE-2025-12385) in qtdeclarative
* [CVE-2025-14576](https://nvd.nist.gov/vuln/detail/CVE-2025-14576) in qtdeclarative

### qtbase
* 7bd7df5aa17 QFileSystemEngine::tempPath: bypass QDir and go straight
to QFSEngine
tempPath() may now return a non-canonical path. This means going up
from it (cdUp()) may result in different paths from string manipulation
(adding "/..").

* cc6d78325b0 SQLite: Update SQLite to v3.50.0
Updated SQLite to v3.50.0

* 5ee2737d916 qdbus: add call GetConnectionCredentials interface
Added method serviceCredentials(). See
<https://dbus.freedesktop.org/doc/dbus-specification.html> section:
'Method: org.freedesktop.DBus.GetConnectionCredentials' for more
information.

* a8dab6eb652 iOS: Report inverted screen orientations via windowScene
orientation
QScreen::orientation() now reflects the inverse portrait and landscape
orientations, as long as system allows rotating the UI to those
orientations.

* bac0226ac35 SQLite: Update SQLite to v3.50.1
Updated SQLite to v3.50.1

* f1c0bd2e06f QStringConverter: Introduce finalize()
Added finalize(), a function to force the converter to consider the
sequence of inputs as complete, flushing potential partial character
sequences.

* afdf37ad8f6 QMetaObject: deprecate the Qt 6 QVector -> QList porting
kludge
Fixed a bug that caused signals and slots with argument types matching
"QVector<" (e.g. "MyQVector<int>" or "NotQt::QVector<int>") to not be
found in QObject::connect() or QMetaObject::indexOfMethod().

* bb48dbb113a Add conversion from QUtf8StringView to std::u8string_view
Added std::u8string_view operator if compiled with C++20.

* 6600a332c69 QScopeGuard: only include what you need
The qscopeguard.h header no longer includes qglobal.h, but only what it
itself needs. A backwards-compatible fix is to not depend on transitive
includes and include all you need explicitly.

* 8fcc4596efc QDataStream: add operator bool()
Added implicit conversion to bool, returning `status() == Ok`.

* 46ad6121fde Bump double-conversion version
Updated double-conversion to v3.3.1.

* 98710e210f1 QDBusPendingCall: add move-constructor
Added move constructor.

* 522d505dd81 QScopeGuard: add commit()
Added commit() method.

* e97b9cd6710 QJsonObject/QCborMap: Add asKeyValueRange()
Added asKeyValueRange to iterate with a range-based for loop over key-
value pairs with support for structured bindings.

* 68210484d95 QDBusMessage: add move-constructor
Added move constructor.

* 238a4eb170d QUrl: fix comparisons of URLs with password but no
explicit username
Fixed a number of bugs in QUrl where a URL modified using the setXxx()
functions would fail to compare equal to itself after going through
toString() and setUrl() round-trip.

* 7176ca82bf5 Update CLDR to v47
Updated CLDR data, used by QLocale, to v47.

* eed5ce3d346 Deprecate QColormap
The QColormap class has been deprecated.

* 4ac4c9db14b Update bundled libjpeg-turbo to version 3.1.1
libjpeg-turbo was updated to version 3.1.1

* 3cb3e84843c Update TIKA mimetypes from upstream
Updated TIKA mimetypes from upstream

* 131da3b171a QMetaType: use nothrow operator new
create() will return a null pointer and not throw if a memory
allocation failure happens. It may still throw if the constructor of the
meta type in question throws.

* f6a0c8cf94b Update public suffix list
Updated the public suffix list to upstream version
2025-06-16_09-45-02_UTC.

* e4b3b9f501c QPainter: add brushOriginF()
QPainter got a new function brushOriginF().

* 91ef0705272 wayland: Add pointer warp support
New protocol synced from wayland-protocols

* d7a2e13df27 QLockFile: mark ctor explicit
The QLockFile(QString) constructor is now explicit, so implicit
conversion from QString to QLockFile, incl. `QLockFile f = str;`, no
longer works. Using explicit construction instead (`QLockFile f(str);`)
is a backwards-compatible fix.

* 7d5f447124e QLockFile: make d_ptr private
The protected QLockFile::d_ptr variable is now private. The class isn't
safe for subclassing, anyway (doesn't have a virtual destructor), so if
your code depends on this, you need to find a different design.

* 0094c73c3ce wayland: Add xx-session-management-v1 support
New protocol synced from wayland-protocols

* bb12c984b2c Android: update to Gradle 8.14.2 and AGP 8.10.1
Updated Gradle to 8.14.1 and AGP to 8.10.1.

* 9b9ebbc0c25 Update bundled libpng to version 1.6.49
libpng was updated to version 1.6.49

* ba863e0620a SQLite: Update SQLite to v3.50.2
Updated SQLite to v3.50.2

* e9f91f049cb QAnyStringView: support single wchar_t arguments also on
Unix
The unary arg() function now treats wchar_t as a character (string-
like; was: integer), so u"%1".arg(L'ø') will now return "ø" and not
'248". This makes the function consistent with both QString multi-arg()
and QLatin1StringView::arg().

* fd1915aba41 Android: Set proper A11y-element java class names to
support TalkBack
Provide actual Android UI class names for TalkBack to improve a11y
announcements.

* d65a45d2bcc Fail builds on Apple platforms with invalid Info.plist
Fail builds on Apple platforms if the Info.plist is invalid instead of
generating corrupt application bundles.

* 12285759263 QQuaternion: long live Axes / toAxes()
Added toAxes(), a getAxes() replacement.

* 31b846ffbf1 QPainter: overload setPen/setBrush for rvalue args
Added overloads of setPen() and setBrush() that take rvalues.

* 607772e250f Upgrade Valgrind third-party component to v3.25.1
Updated Valgrind support to v3.25.1; this adds support for RISCV 64-bit
Linux.

* 3e561c54a72 QAtomicScopedValueRollback: fix CTAD with with mixed
(atomic<T>, V) arguments
Added support for class template argument deduction (CTAD) when the
type of the atomic and the type of the new value differ, e.g. as in
`atomic<chrono::milliseconds> a; `QAtomicScopedValueRollback rb(a,
10s)`.

* 5e9efe45dfe QTest::failOnWarning now also fails for all message
types more severe than warning.

* ff045b60d93 QTest: provide overloads for the qWaitFor* functions
Added QDeadlineTimer overloads for the qWaitFor* functions.

* fe008ae667b Update bundled libpng to version 1.6.50
libpng was updated to version 1.6.50

* 3f953283687 QWeakPointer: don't let IfCompatible<X> make accidental
SMFs
Fixed a regression whereby the QWeakPointer<T> copy or move
constructors and/or assignment operators may fail to compile for
forward-declared (incomplete) T.

* 0184300bbaa QPainterPath: add missing move constructor
Added missing move constructor.

* b27e79ec0c4 qmatrix4x4.h: don't include qquaternion.h
The qmatrix4x4.h header no longer includes qquaternion.h. A backwards-
compatible fix is to not rely on transitive includes and include what
you need explicitly.

* 1ebc7380819 QTextStream: cope with multi-code-point signs
Fixed QTextStream::FieldAlignment::AlignAccountingStyle for locales
that have negativeSign/positiveSign (-/+) that take more than one UTF-16
code point (e.g. ar (Arabic)).

* 9b938823776 Make QTest::defaultTryTimeout public
Added QTest::defaultTryTimeout to allow configuring the default timeout
used by the QTRY_* functions.

* 1fe2adea79e a11y: Introduce RoleChanged event, bridge to AT-SPI, UIA
Added new RoleChanged enum value that can be used to send a
corresponding event when the role of an accessible object has changed.

* 9fd9845d1f6 QDBusPendingReply: add missing SMFs
Added move constructor.

* adcbac38cec QPainterPath: remove implicit sharing
QPainterPath is no longer implicitly shared. This is a necessary change
to support various caching optimizations. On the other hand,
QPainterPath is now fully reentrant (before, it was not thread-safe in
the general case).

* aea88d4106f QLocale: fix off-by-one error in codeToScript()
Fixed a bug where QLocale could not find the QLocale::Script with the
highest value when looked up by string (codeToString() or
QLocale(string) constructor).

* 54132e53180 src/gui: bump dependency version of xkbcommon
xkbcommon minimal required version now is 0.9.0.

* c22c344f2fb QTemporaryFile: add renameOverwrite()
Added renameOverwrite().

* 13088266c38 Static plugins - mangle entry point
In namespaced builds the entry function for static plugins now appends
the namespace via QT_MANGLE_NAMESPACE.

* 82eb0fc09e0 Q_IMPORT_PLUGIN: namespace RAII class
The Q_IMPORT_PLUGIN macro must be placed in file-scope. It cannot be
placed into function-scope any more, as it was never intended to be.

* cc246a67ca6 Allow disabling the single-argument qHash compatibility
overload
Added the QT_NO_SINGLE_ARGUMENT_QHASH_OVERLOAD macro.

* c925407c3ab SQLite: Update SQLite to v3.50.3
Updated SQLite to v3.50.3

* 8f344036d5d Make mapFromSource and mapToSource invokable
mapTo/FromSource are now marked as invokable and can be called from
QML.

* e1125c49657 Add missing changed signal to QML Window.flags
Added signal flagsChanged to QWindow.

* 57ada89c04d Define macOS QOperatingSystemVersion constants using only
major version
QOperatingSystemVersion constants for macOS 11 and up are now
represented with their major version only, and minor and patch versions
unspecified, as documented.

* c9539ba36e0 SQLite: Update SQLite to v3.50.4
Updated SQLite to v3.50.4

* 965638584a9 Fix the url construction in the requestUrl method
QNetworkRequestFactory::createRequest() doesn't decode the provided
`path` anymore. If the path string was passed encoded by the user, it
stays encoded in the particular way.

* 5f29ccd6bc4 QFileSystemEngine/BSD: check UF_HIDDEN on the symlink only
Fixed a bug that caused isHidden() to return true on BSDs and Apple
OSes for non-hidden symlinks that pointed to hidden targets.

* ba21e89c2f7 QQuaternion: long live EulerAngles / eulerAngles()
Added eulerAngles(), a getEulerAngles() replacement.

* 6706e565f97 QCoreApplication: namespace qt_startup_hook
qt_startup_hook is now name-mangled when building Qt in namespace.
Applications wishing to override it must use
QT_MANGLE_NAMESPACE(qt_startup_hook).

* 5f012d8b256 QDirListing: check for '.' and '..' after the checking the
name filters
Now listing '.' and '..' special entries respects any set name filters.
Previously if IncludeDotAndDotDot was set, '.' and '..' would always be
listed.

* 3cf10c70d9a QDirListing: add IncludeBrokenSymlinks flag
Added IncludeBrokenSymlinks flag which lists broken symbolic links
regardless of the state of the ResolveSymlinks flag. This provides
compatibility with the QDir::Filter::System flag in QDir.

* 1c0dc86fc74 QDir: deprecate QDir::Filter::Modified flag
Deprecated QDir::Filter::Modified flag.

* 70272ba992e Doc: Classify 3rd party code in cmake as tools
Reclassify third-party components "KWin" and "extra-cmake-modules" as
tools related.

* 145ffefc4c0 Upgrade Harfbuzz to 11.3.3
Upgraded Harfbuzz to version 11.3.3.

* acde39e1020 Make QtCore/QStringConverterBase header warn on use
Including the header QtCore/QStringConverterBase will produce a
warning. That class is not documented and must not be directly used. Use
only QStringConverter.

* 1493a6e8841 QSsl: Add support for the ML-DSA signature algorithm
Added support for the ML-DSA signature algorithm.

* 97eba34c65c Update byte-ordered QPixelFormats to be
QPixelFormat::BigEndian
QPixelFormats with typeInterpretation() QPixelFormat::UnsignedByte now
reflect a byteOrder of QPixelFormat::BigEndian, to highlight the fact
that these formats need to be read as such if not read in a byte-by-byte
manner.

* 9de2e727d95 windeployqt: Add parameter to extend timeout of
qmlimportscanner
Add option to control timeout for qmlimportscanner runs.

* ca01e54454c Teach QImage::toCGImage() how to propagate the image's
color space
QImage::toCGImage() now propagates the color space of the image to the
resulting CGImage.

* f0019c51397 QTest::qWaitFor*: capture the widget/window using QPointer
Fixed a bug that would cause the qWaitForWindow* and qWaitForWidget*
functions to crash or misbehave if the window or widget they were told
to wait on was destroyed in the process of waiting for it to be
shown/focused/activated/exposed.

* 184ec7cad28 QTextEngine: Pass expanded context to HarfBuzz for shaping
Improved text shaping with mnemonics in certain languages, such as
Arabic.

* ed358937452 qvsnprintf: fail if the result size doesn't fit into an
int
Fixed a bug that would cause q(v)snprintf() to report success on some
platforms, even though the result was truncated.

* 7a1e7c88f08 QQuaternion: fix SiC in fromEulerAngles() overload set
Added fromEulerAngles() overload taking the new EulerAngles struct as
an argument.

* 59929458695 Upgrade Harfbuzz to 11.4.1
Upgraded Harfbuzz to version 11.4.1.

* e7a211d702d Android: Use the TalkBack focus signal to trigger
focusAction
Use TalkBack ACTION_ACCESSIBILITY_FOCUS to trigger focusAction.

* b682d31d7e5 Android: Set name-matched class names for Slider and
ScrollBar for TalkBack
Use different Android class names for Slider and Scroller.

* 272a091d1cf Teach QImage::toCGImage() about most of our image formats
QImage::toCGImage() now supports most of the QImage formats. If a
format is not supported the function will return a null CGImageRef.

* cfb1596ef9e QJsonDocument/Value: fix integer truncation in
fromJson(QByteArray)
Fixed a bug on 64-bit platforms where fromJson(QByteArray) could report
one of the Unterminated errors for valid input whose size merely
exceeded INT_MAX (2GiB).

* c86a33db043 moveToTrash/XDG: allow $XDG_DATA_HOME/Trash to be a
symlink
Fixed a bug that caused moveToTrash() to disallow trashing to trash
bins using the XDG Trash Specification when the trash path was a
symlink.

* 93e2b44bc07 Teach qt_mac_toQImage about most of our image formats
Converting from CGImageRef, used for example in the HEIC/HEIF image
reader, now support a wider range of image formats, including
QImage::Format_RGB30 and the various floating point formats.

* b2197776c65 Upgrade PCRE2 to 10.46
PCRE2 was updated to version 10.46.

* 23ec36d1b23 QStringConverter: allow appendToBuffer() to write to the
buffer
The appendToBuffer() functions in QStringEncoder and QStringDecoder may
write to parts of the provided output beyond the returned pointer.
Caller code must not assume the data beyond that remains unmodified.

* 9da6fd4fab1 HTTP: remap Custom operations to known methods
Using CustomOperation with GET, PUT, POST, DELETE or HEAD will now be
remapped to the corresponding operation. This might affect caching and
redirection handling.

* 745d9683617 Add a clear method to QAuthenticator
Add a new method to clear all credentials.

* 76afe79daaa Suppress construction of QTimeZone(Qt::TimeSpec)
Construction from a Qt::TimeSpec, which was never meant to be
supported, is now rejected at compile time, where previously compilers
(mis)interpreted the enum as an int so called the (int offsetSeconds)
constructor, with results consistently at odds with what the user
presumably expected.

* d6054c5f414 Add camel-case header for qtconcurrenttask.h
Added a camel-case QtConcurrentTask header, which is the same as
QtConcurrent/qtconcurrenttask.h.

* e6ddf72279a Respect QT_NO_INT128 in qtypes.cpp's #error
Made it possible to compile Qt with GCC in strict C++ mode (-ansi or
-std=c++NN) again, provided QT_NO_INT128 is defined, too.

* 5b93573bb40 Update bundled libjpeg-turbo to version 3.1.2
libjpeg-turbo was updated to version 3.1.1

* 3b294d2d4f1 Upgrade Harfbuzz to 11.4.5
Upgraded Harfbuzz to version 11.4.5.

* 9cc32c24908 Update Freetype to 2.14.0
Updated bundled Freetype to 2.14.0.

* 5bde0225c81 Make QTEST_THROW_ON_FAIL work from within QtConcurrent
Fixed a bug which prevented QTEST_THROW_ON_FAIL and QTEST_THROW_ON_SKIP
from working with QCOMPARE(), QVERIFY(), and QSKIP() invoked from within
QtConcurrent functions.

* d9b675de61e QDate: make weakly incrementable
QDate now models the std::weakly_incrementable concept by implementing
pre- and postfix increment (and decrement) operators.

* b70bf618688 wayland: Implement server-side key repeat
Update wayland.xml to 1.24.0.

* f773dd0bf41 Update Freetype to 2.14.1
Updated bundled Freetype to 2.14.1.

* 5db6667780e Upgrade Harfbuzz to 11.5.0
Upgraded Harfbuzz to version 11.5.0.

* 5e4fedb906a QDBusReply: apply Rule Of Zero
Enabled move constructor and move assignment operator.

* fd46598a32e Add QRawFont::glyphCount()
Added QRawFont::glyphCount() for iterating the glyphs in a font.

* 840af27cc41 Add QRawFont::glyphName()
Added QRawFont::glyphName() for inspecting glyph names.

* 3ccf5e53d25 Remove seconds from C locale short time format
The C locale now, in line with all locales derived from CLDR data,
omits seconds from its short time format.

* ca07bcc9e9d Change C locale's short date format to use two-digit month
The C locale now, in line with all locales derived from CLDR data, uses
numeric month rather than the abbreviated month name.

* 24ccf8c5a0b QObject: warn about using SLOT macro with non-slot
functions
A warning will be shown if the SLOT() macro is used with a function not
marked as a slot, but it'll continue to work to keep backwards-
compatibility. However in Qt7 the SLOT() macro will be no-op for non-
slot functions.

* 3dca78332be Upgrade Harfbuzz to 11.5.1
Upgraded Harfbuzz to version 11.5.1.

* b910addacd9 Android: Update to Gradle 8.14.3
Updated Gradle to 8.14.3.

* 1a6316652aa Apple: Respect the painter's layout direction when
producing theme icons
The Apple icon engine now respects the layout direction of the painter,
producing RTL specific icons if available in the SF Symbols icon set.

* f8594a7ab6a Upgrade Harfbuzz to 12.1.0
Upgraded Harfbuzz to version 12.1.0.

* 947fd416e4e Add qTrId() alias for qtTrId()
Added qTrId() alias for qtTrId().

* d4ee0815891 macdeployqt: Make code signing with identity "-" the
default
macdeployqt does now do ad-hoc signing of its content by default. Use
the new option -no-codesign to disable that.

* 0a1c69bba5b QString: fix overly-eager arg(int-ish) overload
Fixed the integral arg() overload to reject types that merely
implicitly convert to an integral type. This was always the intent, but
6.9 and 6.10.0 incorrectly accepted types that implicitly convert to
float to match this overload, causing truncated results. We now reject
such types. A backwards-compatible fix is to cast such types to a C++
type whose displayed form matches your intent.

* fe3129ed411 Fix text offset when drawing a QPicture
Fixed an issue where text drawn into a QPicture might be offset
vertically when replayed.

* 08ebe3465cc qnumeric.h: add support for C23/C++26 <stdckdint.h>
qnumeric.h's qAddOverflow(), qSubOverFlow(), and qMulOverflow()
functions no longer accept char as a template parameter type. Use quint8
or qint8.

* 293032ab2f4 a11y: Add Switch role
Added new Switch role that can be used instead of CheckBox for more
accurately communicating the elements role to assistive technology.

* 18550cd9ad0 wayland: Convey preference for server side decorations
The Wayland XDG shell integration now requests server side decorations
with compositors supporting the zxdg_decoration_manager_v1 protocol.

* a6cc78f4e26 Teach QKeySequence::toString(Native) about C0 Control
Pictures
QKeySequence::toString() now maps the C0 control characters to their
equivialent in the Unicode Control Pictures block, if using
QKeySequence::SequenceFormat::NativeText.

* b2402684cc1 CMake: Relax handling of CMP0156 policy
CMake user projects will now use CMake's default value for the CMP0156
policy, except for Apple and Emscripten platforms which are forced to
NEW (when the policy is available).

* 0a0aed0fcd2 Long live Q_PRESUME
in the next commit so it won't be cherry-picked.

* 33b153c1042 QAbstractItemView: Make the keyboard search configurable
The new property keyboardSearchFlags was introduced, allowing client
code to do something other than a prefix search.

* 60b3466600b Document Q_PRESUME
and thus never evaluates the expression, replacing Q_ASSUME which could
evaluate it.

* 8f4adf09489 QByteArray: percentDecoded/fromPercentEncoding: add rvalue
overloads
Added rvalue overloads of percentDecoded() and fromPercentEncoding().

* b53656bfa70 a11y: Introduce accessible attribute for orientation
Added new Orientation enum value that can be used to specify the
orientation of an accessible object.

* 2808147b9ea SHA3: Replace git SHA with tag
Replaced version information of 'Secure Hash Algorithm SHA-3' from a
git SHA to a semantic version. The content remained the same though.

* e89fc23eb87 Upgrade PCRE2 to 10.47
PCRE2 was updated to version 10.47.

* 5e37cd4a5cf Don't claim that PCRE2 is optional
Don't claim that using PCRE2 is optional.

* 93fe512d053 XCB: Remove the native X11 painting engine
The experimental X11 Native Rendering engine has been removed. Use of
this engine required enabling it at compile time with a CMake option and
enabling at runtime with an environment variable.

* eebdc03a925 CMake: Add initial Cyclone DX v1.6 SBOM generation support
A new -sbom-cyclonedx-v1_6 configure option can be used to generate and
install a CycloneDX v1.6 SBOM (Software Bill of Materials) file for each
built Qt repository.

* 9805a4cba51 rhi: add support for depth clamping in
QRhiGraphicsPipeline
Added support for depth clamping in QRhiGraphicsPipeline.

* 878c451799a QUtcTimeZonePrivate: use OffsetName rather than ShortName
in fallback
Fixed-offset zones with non-standard offsets are now named more
compatibly with those with standard offsets.  This should only be
visible for whole-hour extreme offsets (over 14 hours, not used by any
real zone since the 1800s).

* 6466ed868ac Http: Set error to 'TimeoutError' for a transfer timeout
The error set when a request times out due to
QNetworkRequest::setTransferTimeout() has been changed to
QNetworkReply::TimeoutError, to disambiguate from the previously used
QNetworkReply::OperationCanceledError.

* 012cd9e4884 macOS: Disable window-modal native message boxes on Tahoe
Window-modal message boxes are no longer backed by native NSAlerts on
Tahoe, due to a bug that prevents the alert from responding to mouse
events for its buttons.

* 0c09d9483c4 SQLite: Update SQLite to v3.51.0
Updated SQLite to v3.51.0

* dfa8edf45c8 wayland: Add color-management-v1 support
New protocol synced from wayland-protocols

* f9bb6c8d900 QRangeModel: implement autoConnectPolicy
A range model operating on a range that holds identical QObject
sublasses for all items can now automatically connect the changed
signals of all properties mapped to item roles to the model's
corresponding dataChanged signal. This allows user code to change
properties of the item-object directly, and model clients (like item
views) will get updated.

* 5a685653b89 QRandomGenerator: remove direct use of HW instructions
This class no longer directly uses a hardware random number generator
on x86 systems, even if one is available. Instead, it will always use a
generator provided by the OS (so performance will be OS-specific),
though there should be no meaningful difference in the quality of the
samples generated.

* 50f3e2d39d0 Upgrade Harfbuzz to 12.2.0
Upgraded Harfbuzz to version 12.2.0.

* dcf4263dc41 QMake: Add support for MSVC's address sanitizer
QMake MSVC projects can now enable MSVC's address sanitizer with CONFIG
+= sanitizer sanitize_address

* 3a711ad6192 Update CLDR to v48
QLocale now uses v48 of the Unicode Consortium's Common Locale Data
Repository (CLDR). This includes two new languages, Ladin and Shan.

* b3918b13a92 iOS: Add support for QFileOpenEvent for external requests
to open files
QFileOpenEvent is now sent if the user requests that a supported file
type is to be opened in the application. This requires that the
application declares supported file types via CFBundleDocumentTypes.

* ed1d4a39814 CMake: Add emoji segmenter attribution to SBOM
Emoji Segmenter is now included in the SBOM dependencies of Qt GUI.

* 571c55dbcd6 QTabBar: Emit tabCloseRequested on middle click if
tabsClosable
Middle clicking tabs in QTabBar with tabsClosable set to true will now
emit tabCloseRequested.

* f1d0f5d7ee6c QTimeZone should now be able to parse numbers written
in non-BMP scripts - that is, where each digit is a surrogate pair.

* cc8415653fa Update bundled libpng to version 1.6.51
libpng was updated to version 1.6.51

* f216d13b67b Add TCP Keepalive options to QAbstractSocket
Added new socketoptions to QAbstractSocket: KeepAliveIdleOption,
KeepAliveIntervalOption and KeepAliveCountOption.

* 89bd95df5a0 Use environment variables to change TCP keepalive settings
in QNAM
Added new environment variables QT_QNAM_TCP_KEEPIDLE,
QT_QNAM_TCP_KEEPINTVL and QT_QNAM_TCP_KEEPCNT to change TCP keepalive
options. Set the values in QNAM so that it terminates an inactive
connection after 2 minutes.

* 0edcb27891e Add security scoped file engine for Apple operating
systems
Sandboxed applications on Apple platforms, (including macOS if opted in
to) can now access files outside of the application sandbox (so called
security scoped resources) for both reading and writing. Files or
folders chosen by the user via file dialogs or similar native mechanism
are automatically and transparently handled, including persistent access
across application and device restarts.

* 205e8ce387d iOS: Implement support for native save dialogs
Native file dialogs on iOS now support saving files.

* 8441b19e1ce CMake: Automatically generate a vcpkg manifest
Added a -generate-vcpkg-manifest configure option. This generates a
vcpkg.json file in the build directory. To just generate the manifest
without configuring Qt, run configure with -generate-vcpkg-manifest
-dry-run.

* 3714b7feabe Add missing forwarding for channel signals in QLocalSocket
/ Unix
Fixed QLocalSocket not emitting channelReadyRead() and
channelBytesWritten() signals

* f4be891ed74 SQLite: Update SQLite to v3.51.1
Updated SQLite to v3.51.1

* 135ffa252ee Specify TCP Keep Alive parameters via QNetworkRequest
Added new methods to specify and get the current TCP KeepAlive
parameters for the request.

* e22cd01076e Add QRangeModelAdapter: C++-style access to the range
while talking QAIM
Added QRangeModelAdapter for C++-style access to a range used in a
QRangeModel, while implementing QAbstractItemModel protocol.

* afd765ee590 QVectorND: do not assert when deserialization yields NaN
or ±∞
Fixed a bug in the QDataStream operator that could lead to an assertion
failure (program termination) on reading back previously streamed out
objects that contain NaN or infinity values.

* 450a1374f69 Update bundled libpng to version 1.6.52
libpng was updated to version 1.6.52

* e27d5fc6a6b QMetaProperty: Introduce VIRTUAL, OVERRIDE attributes
VIRTUAL and OVERRIDE attributes will be used for the expanded override
semantics in QML. See QTBUG-98320 for the details.

* b2cc2c2b7f6 QFont: fix operator<() pt.2: comparing QMaps
Fixed a Qt 6.7 regression in the stability of the less-than operator.
If you use QFont as keys in a QMap/std::map, or otherwise use QFont
ordering (equality is ok), then we strongly recommend to update.

* 305a018a041 Update bundled libpng to version 1.6.53
libpng was updated to version 1.6.53

* 6d2dbf45ba3 q23:expected: namespace TL_ macros with Q23_
Fixed potential compile errors in projects that use both the original
tl::expected and Qt private headers.

* 267571e3d5a Update bundled libjpeg-turbo to version 3.1.3
libjpeg-turbo was updated to version 3.1.3

* d3476d96eeb Core: Remove qmetacontainer.h include from qiterable.h
qiterable.h does not include qmetacontainer.h anymore.

* 3ceeb98f8de QThread/Unix: re-enable cancellation before the event
dispatcher
POSIX Thread cancellations are now enabled during the event
dispatcher's startingUp() call and when the QThread::started() signal is
emitted. This allows the thread to be terminated (e.g. via
QThread::terminate()) during those calls.

* cc57e71e944 qHash: don't hash the padding bytes of long double
Fixed a bug that caused the qHash() function to return non-
deterministic results for long double values on most x86 systems,
regardless of seed.

* a460702b6c9 CMake: Revisit target-based qt_wrap_cpp
When using the target-based signature of qt_wrap_cpp, qt_wrap_cpp(myapp
myobject.h) will now add the generated moc_myobject.cpp to the target.

* dccbfb1d4a8 Upgrade Harfbuzz to 12.3.0
Upgraded Harfbuzz to version 12.3.0.

* 9e00db429c8 CMake: Add means to configure the location of CMake config
files
The installation location of CMake config files can now be configured
by setting the CMake cache variable INSTALL_CMAKEDIR to a relative path.
The default is "lib/cmake". The public variable QT6_INSTALL_CMAKEDIR was
added to retrieve the path in user projects.

* 4e8f0a24bf9 macOS: Enable clipping of subviews when QWindow has child
windows
QWindows with child windows will now set the NSView.clipsToBounds
property to YES, to ensure that the child windows are clipped to their
parent.

* bd6714f2c75 Update tika-mimetypes.xml from upstream and improve
tooling
Updated TIKA mimetypes from upstream

* d694f887ee7 double-conversion: Update to 3.4.0
Updated double-conversion to v3.4.0.

* 730f3f99659 Update bundled libpng to version 1.6.54
libpng was updated to version 1.6.54

* 7c1075b7c3b CMake: Fix qt_wrap_cpp calls in subdirectories
In the variable-based signature of qt_wrap_cpp, we now add foo.moc
files to the output variable. This simplifies the code flow, and adding
.moc source files to a target doesn't have a negative effect.

* bbe21b30e7c QHash: add missing insert() overloads
Added the missing rvalue overloads of insert().

* 3ca90155e28 SQLite: Update SQLite to v3.51.2
Updated SQLite to v3.51.2

* d7d7b3f1df3 Update CLDR to v48.1
QLocale is updated to version 48.1.

* 479f636ed5a Update public suffix list
Updated the public suffix list to upstream version
2026-01-16_13-11-47_UTC.

* bc6d856c43c qfloat16: turn copySign() member into hidden friend
copysign()
Added copysign() with std::copysign()-compatible syntax, replacing the
copySign() member function.

* 713f0a5a4d5 QStringDecoder: handle errors when reading illegal UTF-32
Fixed a bug that caused QStringDecoder not to insert Unicode
replacement charaters when decoding malformed UTF-32 input data. The
same applies to QString::fromUcs4.

* bb0b0d0e8de Update UCD to Unicode 17.0.0 / revision 36
Updated the Unicode Character Database to UCD revision 36/Unicode 17.

* e1f39c7a32f QString::normalization: fix corrections shrinking the
string
Fixed a bug that caused normalization() to incorrectly apply some
Unicode 3.1 and 3.2 corrections, corrupting the string during the
operation. This affected QUrl::toAce().

* b83f06c5c97 QRM: respect MultiRoleItem override for container and
tuple rows
A QRangeModel::RowOptions override as MultiRoleItem is now respected
for containers and tuple types. The model will read and write the entire
container or tuple for calls to data and setData, and respect an
QRangeModel::ItemAccess specialization for role specific read/write
operations.

* 1489f59c8ea Upgrade Harfbuzz to 12.3.2
Upgraded Harfbuzz to version 12.3.2.

* 269a75dbd12 Android: bump to Gradle 9.3.1 and AGP 9.0.0
Updated Gradle to 9.3.1 and AGP to 9.0.0.

* f0eabce01d1 Update bundled libpng to version 1.6.55
libpng was updated to version 1.6.55

* d9e9efacc31 QAction: Strip elipsis unicode char from icon text
QAction now additionally strips the unicode elipsis character (…) from
the icon text.

* 7b8591ac572 QFileSystemEngine: handle copy_file_range() returning
ENOSYS error
Added a workaround to a compatibility issue of the copy()
implementation in some containerized Linux environments, which could
cause the file copy to fail with a "Function not implemented" error.
This is believed to be a bug in the container runtime, not Qt, in that
the container wrongly filtered the copy_file_range(2) system call that
the Linux kernel supports.

* d1751345bf9 qWaitFor: mark waitForMore/Succeeded as customization
points
The predicates passed to the qWaitFor* familiy of functions now need to
return a type that is implicitly convertible to bool (was: contextually
convertible to bool). An example of a type that is contextually-, but
not implicitly-convertible is one that has an explicit operator bool().
A backwards-compatible fix is to explicitly cast the return value to
bool.

* ba54db0ca4e Update zlib to 1.3.2
zlib was updated to version 1.3.2.

* f260db18c06 Update to TinyCBOR 7 with CMake support
TinyCBOR updated to version 7.0.

* 694b1a55619 Update Freetype to 2.14.2
Updated bundled Freetype to 2.14.2.

* 8ba7ea4b77a Upgrade Harfbuzz to 13.0.0
Upgraded Harfbuzz to version 13.0.0.

### qtsvg
* f9c27e60 QSvgGenerator: document the initPainter() override
This class now reimplements QPaintDevice:initPainter(). If you
subclassed QSvgGenerator and reimplemented initPainter(), you will need
to change your reimplementation to call the new QSvgGenerator override,
otherwise it won't be called.

### qtdeclarative
* c6351d481a Enable expanded client area by default in iOS style
The iOS style now enables expanded client areas by default. To override
this, set the ApplicationWindow's flags explicitly to e.g. Qt.Window.

* 681352aaeb QML: Turn warning into a syntax error
Using a bare function expression in eval() is now correctly recognized
as syntax error. You have to surround it in parentheses to make it a
statement. This has been generating warnings since Qt 5.11 and it should
have become an error already in 5.12.

* 893192a9f4 Clarify the exact commit of the yoga 3rd party dependency
Clarified that exact version of yoga library is v2.0.1.

* 92dceea85e CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

* 5068a675c4 QtQml: Do not store type references for properties
You can now have cyclic type references in QML documents. A QML type A
can have a property of type B while B has a property of type A. You can
still not cyclically inherit or instantiate types in QML documents, of
course

* 270bd4dc05 Don't delete component delegates
Old QQmlComponent delegates (not the item instances created by them)
are no longer destroyed when a new one is set, as they are technically
owned by user code. They will still eventually be garbage-collected as
expected, assuming there are no references to them.

* 5d3f3fdbdb Add easingCurve value type and Easing singleton
Added the easingCurve value type and Easing singleton.

* 8bc307e8ed API Review: Expose delegateModelAccess from
QQmlInstantiator
Instantiator now has a new property delegateModelAccess. Setting it to
DelegateModel.ReadWrite allows you to write values into the model via
required properties just as you could with context properties.

* eb9ab1b596 Replace btoa() and atob() with better implementations
The Qt.btoa() and Qt.atob() methods were subtly broken and produced
different output than the common Web APIs. They have been deprecated in
favor of overloads that take array-likes. Array-likes, especially
ArrayBuffer, are a better fit for expressing raw data than strings.

* 3ab60f40d5 qmllint: Avoid spurious warnings when file selectors are
used
qmllint and the LSP now no longer print warnings about ambiguous types
if file selectors are used, and instead use the "plain" version. The QML
script compiler will still conservatively reject such QML files. If
warnings about such cases are desired, the new "importFileSelector"
warning category can be enabled.

* 705c71b5f6 Remove support of manipulation of complex rows in
QQmlTableModel
Removed the support of manipulation of complex row structures from
QQmlTableModel.

* 78b23bda68 QQmlSslConfiguration: introduce sslOptionFlags property
Added an sslOptionFlags property. Use it instead of the sslOptions
property.

* cea8a1f8e1 Deprecate QQmlSslConfiguration::sslOptions property
Deprecated the sslOptions property of
sslConfiguration/sslDtlsConfiguration. Use the new sslOptionFlags
property instead.

* 018b10ff71 qt_target_qml_from_svg() command in cmake
Added a cmake api for automatically generating QML files from SVG files
in an application.

* 7fb0e744ff Compiler: Enable color output on supported consoles on
Windows
Color ouput for qmllint and qmlcachegen is now also enabled on Windows
on terminals that support it.

* 0d67aad01c QtQml: Return QVariant{Map|Hash} as-is when converting
QJSValue
QJSValue::toVariant() now returns a QVariantMap or QVariantHash for
JavaScript objects created from a QVariantMap or QVariantHash, even if
you tell it to RetainJSObjects via the "behavior" argument. There is no
conversion in this case, after all.

* 64b16cc111 QmlModels: Make QQmlInstantiator require QQmlDelegateModel
If you build with -no-feature-qml-delegate-model, along with most
functionality of QtQml.Models, Instantiator will also be missing now. It
makes no sense to provide an Instantiator that can't actually
instantiate anything.

* 3f89d9deb0 Add ShapePath.cosmeticStroke
ShapePath now has a cosmeticStroke property which causes strokeWidth to
be constant despite scaling. Set the environment variable
QT_QUICKSHAPES_STROKE_EXPANDING to 1 to enable an experimental method of
expanding strokes in the vertex shader, minimizing the need to re-
triangulate when strokeWidth changes.

* b300f909d7 Add EllipseShape to QtQuick.Shapes
Added EllipseShape.

* 13aa6fee41 Enable declared TextSelection instances to edit text
programmatically
In addition to TextEdit.cursorSelection, you can now create non-visual
instances of TextSelection and use them to modify rich text
programmatically.

* 7f5b602751 Make defaultDelegate compatible with TreeModel and
TableModel
Changed the order of the role and value parameters in setData to
resolve ambiguity.

* ed607c86a4 Initialize QQuickGradientStop position to zero
The position property is now always initialized to 0.0; previously it
was left uninitialized.

* 03cd2dea76 CMake: Add plugin options to
qt_generate_deploy_qml_app_script
Added NO_PLUGINS, EXCLUDE_PLUGINS, EXCLUDE_PLUGIN_TYPES,
INCLUDE_PLUGINS, and INCLUDE_PLUGIN_TYPES options to
qt_generate_deploy_qml_app_script.

* dff5931a40 Skip synthesis of QContextMenuEvent if eventpoint has a
grab
To fix QTBUG-134903, when the right mouse button is pressed, we don't
send a QContextMenuEvent if we can detect that a right-mouse click might
already be handled by a TapHandler or a MouseArea to open a Menu. But we
recommend that you stop opening menus that way: either rely on the
built-in menus provided by TextArea and TextField, or use the
ContextMenu attached property to replace or add menus to controls. In Qt
7 we plan to send the QContextMenuEvent without checking for handlers
first.

* a0a2a239dc qmllint: Also lint inner functions
qmllint will now lint inner functions, defined in javascript, in
addition to top-level functions and bindings.

* 4d1753b95f DialogButtonBox: add properties for setting a default
button
The DialogButtonBox now has two new properties, defaultButton and
defaultStandardButton. When one of these properties are being used, a
button set as default will be highlighted and receive activeFocus
whenever the DialogButtonBox gets focus. If a DialogButtonBox is
assigned as a Dialog's footer, it will also get focus when the Dialog is
opened. This means that a Dialog with a DialogButtonBox as its footer,
will give focus to a default button when opened. If both of these
properties are unset, the first button with the AcceptRole will get
focus, but it will not be highlighted.

* c0ede88036 Window: specify correct property type
Window and ApplicationWindow now enforce that the type of the property
passed to the screen property is ScreenInfo. It used to accept any
QObject, but would silently convert it to null if the type was not
correct.

* c056aaa055 StyleKit: add StyleKit to labs
Introduced new QML module 'StyleKit'. StyleKit provides a flexible
styling framework for Qt Quick Controls, enabling developers to define
reusable styles and themes using a simple key-value property format.

* 680c871fbf Qt Quick Controls: add DoubleSpinBox
Added DoubleSpinBox.

* 77b724bb85 Add StarShape to QtQuick.Shapes
Added StarShape.

* a783420505 Add RegularPolygonShape to QtQuick.Shapes
Added RegularPolygonShape

* 691ad1d9b2 qmlls: use 1 job for background builds
The number of CMake jobs can be set with a command line option, an
environment variables, and a .ini setting option. The default was
changed from using all available cores to 1. You can restore the
previous behavior by passing "max" as number of CMake jobs.

* 672ad85d94 Windows style: override the application palette when in
dark mode
The Windows native style will use a light palette as the application
global palette on Windows systems running in dark mode. The style cannot
render dark controls, and mixing a dark application palette with some UI
elements rendered in light mode using the Control style results in
inconsistent and unusable user interfaces. For Dark mode UIs, use a
style that supports dark mode, like the FluentWinUI3 or Fusion styles.

* c9ce38b9a6 Deprecate Qt Labs' Dialog
Dialog is now deprecated. Use QtQuick.Dialogs instead.

* c3ff198581 SpinBox: add text editing context menu
SpinBox now provides a ContextMenu by default. If you already have a
custom context menu for it, ContextMenu will not open its own on e.g.
right click.

* 05ad0b4e3c ComboBox: add text editing context menu
ComboBox now provides a ContextMenu by default. If you already have a
custom context menu for it, ContextMenu will not open its own on e.g.
right click.

* be192e17be SearchField: add text editing context menu
SearchField now provides a ContextMenu by default. If you already have
a custom context menu for it, ContextMenu will not open its own on e.g.
right click.

* 1f58283688 DoubleSpinBox: add text editing context menu
DoubleSpinBox now provides a ContextMenu by default. If you already
have a custom context menu for it, ContextMenu will not open its own on
e.g. right click.

* b5d11c1507 qmllint: Remove unused category
The restricted-type qmllint warning has been removed. It is now
possible to use all combinations of enum scoping and access scoping.

### qtmultimedia
* bc822b5d8 Build system: skip qtmultimedia if threading is disabled
QtMultimedia now requires Qt to be compiled with FEATURE_thread. This
implies it is not available in single-threaded webassembly

* 2f9a2771a CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

* f83c50d3d 3rdparty: import dr_wav to implement wav decoder
Added dr_wav as wave file decoder for QSoundEffect.

* 0599ece8d QCapturableWindow: Make constructible from QWindow
Introduced new constructor for QCapturableWindow, that allows
developers to create QCapturableWindow instances from QWindows. QML
Windows can now be implicitly constructed into QML CapturableWindow.

* 5f9237b2c 3rdparty: add tlsf arena allocator
Added tlsf for use in QSoundEffect player

* 1f335701d Audio: deprecate QWaveDecoder
QWaveDecoder has been deprecated. Users are advised to use
QAudioDecoder instead.

* 8ff8615fb QMediaFormat: align format/codec descriptions
Improve consistency of format and codec description strings

* 0806d7e30 Update FFmpeg version in documentation
Updated FFmpeg to n8.0.

* b38cc280b Update FFmpeg version in documentation
Updated FFmpeg to n7.1.2.

* ab4c0ec43 MultimediaQuick: use more expressive naming for preview
image provider
The internal image provider used by ImageCapture registers itself as
"QtMultimediaCameraPreviewImageProvider" instead of "camera". The last
frame will not be available under `image://camera/` anymore. Using
QtMultimedia::ImageCapture::preview will give the correct URI.

* 5ea59a7ce Audio: add new public APIs for callback-based Audio IO
Added a callback-based audio IO for QAudioSink/QAudioSource via a new
`start()` signature.

* b3042563f 3rdparty: update bundled Eigen to 5.0.1
Updating Eigen to 5.0.1

* 8385caaf3 Update FFmpeg version in documentation
Updated FFmpeg to n7.1.3.

* 6aed19d6d 3rdparty: dr_wav - update to 0.14.4
Update bundled dr_wav to 0.14.4

* 1554ffc31 GStreamer: Block switching camera or camera device while
recording
When using the GStreamer media backend, calls to
QCamera::setCameraDevice() and QMediaCaptureSession::setCamera() are
ignored during recording.

* 9d0f3cfae 3rdparty: update to dr_wav v0.14.5
update dr_wav to 0.14.5 due to heap buffer overflow

### qttools
* 79625eb96 qdoc: Allow generated lists in table of contents structure
Pages that contain table-of-contents \list structures can now also use
\generatelist and \annotatedlist commands for the same purpose.

* a8e4a4ed2 QDoc: Add an option to log warnings to a file
QDoc can now write warnings to a file. To enable this feature, set the
configuration variable `logwarnings` to `true`.

* 0378aa3da QDoc: Add `\overload primary` to set primary overload
You can now specify what the primary signature is for a set of
overloads with `\overload primary`. Refer to the QDoc manual for
detailed examples and documentation.

* b74f64a23 QDoc: Unify QML linking behavior
Documentation authors can now use QML import aliases in their  examples
and link commands. Types referenced through aliases (like TM.BaseType
after "import TestModule as TM") will be properly linked and highlighted
in the generated documentation.

* a5de61b7c QDoc: Unify HTML structure for QML/C++ members
QDoc no longer generates a table-based member layout for QML types, and
uses the same structure as for C++ types instead. New CSS classes (`qml-
member`, `qml-property`, `qml-method`, `qml-property-group`) allow for
specific styling of QML members.

* 5ca667543 QDoc: Unify HTML structure for QML/C++ members
QDoc no longer generates a table-based member layout for QML types, and
uses the same structure as for C++ types instead. New CSS classes (`qml-
member`, `qml-property`, `qml-method`, `qml-property-group`) allow for
specific styling of QML members.

* 5f184ccaa QDoc: Add \qmlsingletontype command
QDoc now has the \qmlsingletontype command, which you can use to
document a QML type as a QML singleton. Refer to the QDoc manual for
further details.

* 0d2f52a76 QDoc: Support QML pragma singleton
QDoc now recognizes 'pragma singleton' in QML files and automatically
marks the type as a QML singleton.

* 0c8860e98 QDoc: Detect QML_SINGLETON in C++
QDoc now detects QML_SINGLETON macros and marks the corresponding QML
type accordingly.

* bff61026f QDoc: Generate contextual snippets for overloaded signals
and slots
QDoc now generates contextual code snippets and configurable links for
overloaded signals and slots. When documenting overloaded signals or
slots, QDoc automatically creates practical connection examples using
the specific class and function signature, showing both qOverload() and
lambda approaches alongside links to comprehensive documentation.

* fc1bc78ca QDoc: Introduce \toc .. \endtoc, \tocentry commands
Added support for generating a table of contents in XML format for the
documentation project using \toc commands.

* d4d85cd4b QDoc: Always document pure virtual functions
QDoc now unconditionally documents pure virtual functions unless they
are documented as `\internal`.

* 5a0705d57 QDoc: Respect showinternal for \internal content
The 'showinternal' command line option and configuration setting now
correctly cause QDoc to generate documentation for '\internal'
comments.

* 5cde6536d lupdate: Add support for qTrId() function
Added support for qTrId() function calls.

* 003a78956 QDoc: Report unresolved \relates targets
QDoc now outputs a report if the \relates command refers to an unknown
target.

* ee5f834c8 QDoc: Introduce imagesoutputdir configuration variable
The output directory for images used in the documentation can now be
configured with 'imagesoutputdir' variable.

* 55c5c1f3d Linguist: Add auto-label placeholders for ID-based
translations
Added auto-label placeholders (<context>, <class>, <file>) for
automatic label generation in ID-based translations

* d3fb0ac1f QDoc: HelpProjectWriter: Process \generatelist when building
a .qhp TOC
The \generatelist command now produces correct output when used in a
\list structure to build a Qt help project (qhp) TOC.

* d3d4195a8 QDoc: Move \title parsing to DocParser
Formatting commands such as \notranslate are now supported within page
\title argument.

* 9ac1c95f4 Qt Widgets Designer: Extend the Help functionality to
support Web/Qt for Python
It is now possible to use Online web documentation or Qt for Python
documentation as per command line option.

* ef0510345 QDoc: Add an optional language argument to the code command
The \code command now accepts an optional argument to specify the
programming language for the code block.

* d4f550aae QDoc: Extract and render C++20 requires clauses
QDoc now extracts and displays C++20 requires clauses for function and
class templates. This works in both template-head and trailing
constraint positions.

* 28ed4babc QDoc: Render complex templates in multi-line format
Template declarations with more than two parameters are now rendered in
a multi-line format in function documentation. This improves readability
for complex template signatures.

* d2fe238e0 QDoc: Render multi-line templates using CSS white-space
preservation
Template declarations with more than two parameters are now rendered in
a multi-line format for improved readability in both HTML and DocBook
output. The HTML output uses the `template-block` CSS class, allowing
custom styling of multi-line template declarations.

* bb950c2af QFormBuilder::save(): Handle enumerations/flags
QFormBuilder now writes enumeration and flag properties.

* 1239b3261 QDoc: Make recognized code languages configurable
The programming languages that QDoc accepts in code blocks has been
made configurable, allowing code that will be marked up using online
tools to be included in documentation without warnings.

### qtpositioning
* aba34053 Make: Fix incorrect PURL version for clip2tri
Fixed incorrect PURL version for clip2tri in qt_attribution.json.

* f2db3f73 GeoClue2: Fix DesktopId property
The plugin now uses QGuiApplication::desktopFileName() if the desktopId
plugin parameter is not specified, and only falls back to
QCoreApplication::applicationName() if desktopFileName() is not defined.
The fall back path is scheduled to be dropped in the next major release
of Qt.

### qtconnectivity
* 965c5357 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtwayland
* 081436188 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qt3d
* 6164eed2a CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

* 58e347bde Update assimp dependency
Update ASSIMP to 6.0.2

* 9d25b2e13 Update Assimp
Updated Assimp to 6.0.4

### qtimageformats
* e987ad3b Update bundled libwebp to version 1.6.0
Update bundled libwebp to version 1.6.0

* 943f16f9 Update bundled libtiff to version 4.7.1
Bundled libtiff was updated to version 4.7.1

### qtwebengine
* 2ebb596b4 Add HTML inputmode global attribute support
Added HTML inputmode global attribute support

### qtvirtualkeyboard
* 7bdec84d CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

* f909c0d0 Dynamically enable/disable arrow key navigation
Added arrowKeyNavigationEnabled property to settings.

* 3390a38b Add keyboardDesignMaximumHeight to KeyboardStyle
Added keyboardDesignMaximumHeight property to style to prevent keyboard
overlapping most of the screen.

### qtnetworkauth
* 33c2f10 Reduce strictness of QOAuthUriSchemeReplyHandler path check
Treat empty path and '/' as equivalent when comparing redirect URL.

### qtlottie
* e592848 Doc: Fix module name in qt_attribution.json files
Fixed Qt Lottie Animation module name in license source files.

### qtquick3d
* 291d70aa1 Update Assimp to v6.0.2
Update ASSIMP to v6.0.2

* 546c7b641 Update OpenXR to v1.1.49
Update OpenXR to v1.1.49

* a8b2ef2fb Expose view matrix to post-processing effects
VIEW_MATRIX is now available in post-processing effects.

* cbc360e95 Add layering support
Added layering support

* 10386f657 Add support for normal-roughness texture
Added support for NORMAL_ROUGHNESS_TEXTURE in postprocessing effects
and custom materials.

* 4c2e685a4 Add SSGI effect
Added a screen-space global illumination solution to
ExtendedSceneEnvironment, providing ambient occlusion and real-time
indirect light.

* 5e7c98d74 Add View3D.closestPointPick()
Adding closestPointOnTriangle(), based on https://github.com/RenderKit/
embree/blob/master/tutorials/common/math/closest_point.h under the
Apache-2.0 license.

* 25f916068 XR: Add support for virtual touch on 3D surfaces
Extend XrItem touch event support to any Model with pickable: true.

* a9184325f XR: OpenXR: OpenGL: desktop Linux support
Support desktop OpenGL on Linux

* c66045397 Add blue noise randomness to PCF soft shadows
Add CC0-licensed blue noise texture

* 7d64f0b94 Add QML API for user-defined render passes
Added QML API to enable user-defined render passes.

* 7cd2bb990 Add SSR effect to ExtendedSceneEnvironment
Add screen-space reflections (SSR) support activated by the
'ssrEnabled' property.

* abceae28b Remove unusable enums from QSSGFrameData
Removed RenderResult enums in QFrameData that was only meant for
internal usage.

* 93c15cd2e Update OpenXR SDK to v1.1.54
Updated bundled OpenXR SDK to v1.1.54

* 24bd128e4 Update meshoptimizer to v1.0
Updated bundled meshoptimizer to v1.0

* c6cbe9702 Update Assimp to v6.0.4
Updated Assimp to v6.0.4

### qtshadertools
* 5ce3cba Update SPIRV-Cross
Geometry shaders can now be translated to HLSL automatically. Disabling
HLSL output and injecting handwritten HLSL geometry shaders is no longer
necessary.

* 6ed6a37 Update SPIRV-Cross
SPIRV-Cross has been updated to current HEAD.

* 01aeca4 Update glslang to 16.0.1
glslang has been updated to 16.1.0

### qt5compat
* 0bf495f CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

* 27e6a77 QLinkedList: fix range-erase() aliasing bug on shared
instances
Fixed a bug in range-erase() that would alter implicitly shared copies
of the list erase() was called on.

### qtcoap
* d28ae1f QCoapClient::post(): align the implementation with the docs
The post() overload that takes a QIODevice* now behaves according to
the documentation. Specifically, if the provided QIODevice* is null, it
will act as if an empty QByteArray was provided instead of simply
returning nullptr.

* 7aefb14 Allow binding QCoapClient to a network interface
Added a bindInterface property that can be used to bind the
communication to a specific network interface.

### qtopcua
* 30ac067b Fix authentication over a None policy secure channel
Using encrypted auth tokens over a None    security policy channel is
again possible after it was broken    with the update to open62541 1.4
in Qt 6.9.

* 1bb63a43 Fix error handling for security policy initialization
Fix a segfault if a client is initialized    with a corrupt certificate
file.

* 6389aaf2 Fix detach() for QOpcUaDataValue
QOpcUaDataValue now detaches its shared data    as expected when
timestamp picoseconds are set.

* 74cfcf64 Update bundled open62541 to v1.4.13
The bundled open62541 was updated to v1.4.13

* 8ea00388 Update bundled open62541 to v1.4.14
The bundled open62541 was updated to v1.4.14

### qthttpserver
* 7eda15d Allow routes to return QFuture<void> and write using responder
Added support for routes handlers that return QFuture<void> and respond
using QHttpServerResponder&& argument in another thread.

* 7dcfe24 Limit max size of incoming requests
Added configurable limitations to the size of incoming requests.

### qtgrpc
* bd86e2f9 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

* 814c0b6a Emit cancelled finished() in channel implementation
Cancellation logic should also emit finished now. Custom
QAbstractGrpcChannel implementations should adapt their logic.

* 0e280384 Deprecate serverMetadata for server{Initial,Trailing}Metadata
Deprecate the metadata()/serverMetadata()/setServerMetadata() methods
on QGrpcOperation and QGrpcOperationContext that use QHash in favor of
the new server{Initial,Trailing}Metadata interfaces, that use QMultiHash
and provide the correct handling of the received metadata in their
respective phase. This is a behavior change as the old metadata()
interface now only returns the initial metadata.

* 25782e88 QGrpc{Call,Channel}Options: add 'filterServerMetadata'
Added the filterServerMetadata property.

* 5bc854e9 QGrpcHttp2Channel: implement filterServerMetadata option
QGrpcOperation::serverInitialMetadata() and
QGrpcOperation::serverTrailingMetadata() no longer include any internal
gRPC or HTTP/2 pseudo‑headers by default.

* 15cef4fd QGrpcHttp2Channel: Guarantee transportation scheme
Requesting TLS or QLocalSocket now fails with a fatal error if the
requested transport is unavailable.

* 60446214 QGrpc{Call,Channel}Options: provide equality operators
Made the options classes equality comparable.

* be670fea QGrpcOperation: add serverInitialMetadataReceived signal
Added the serverInitialMetadataReceived signal.

* dbf2b504 QGrpcHttp2Channel: Report data loss for incomplete trailing
messages
finishes the communication with a non-ok QGrpcStatus (DataLoss) when
the stream is closed with unprocessed trailing data.

* efaba18e QGrpcHttp2Channel: Implement dataframe decompression
Added missing decompression handling for 'deflate' and 'gzip'.

* a0548009 Change arguments for the private channel-rpc interface
The abstract interface of private RPC functions has changed. Users of
this private, undocumented API must adapt their code.

* 94216252 Deprecate semi-private QGrpcOperationContext::argument
Deprecate the argument() method in favor of the new abstract rpc
interface.

* 6e07fd5a Enforce emission of QGrpcOperation::finished
RPC-handlers are now guaranteed to be constructed. The finished signal
will now be invoked at least once during the lifetime, as documented.

* fddc58d1 QGrpcHttp2Channel: configure h2 streams to omit the
downloadBuffer
Disabled unused HTTP/2 buffering, fixing a memory growth issue in long-
running streaming scenarios.

* f12a81f2 Revert "Add FINAL to generated properties"
revert to the previous behavior, then property were not final.

* e2d4e79b qtprotobufgen: Generate QtProtobuf messages as 'final' in
6.11
Generated QtProtobuf message classes are now final by default. A new
GENERATE_NON_FINAL_MESSAGES option was added to restore the previous
behavior for backwards compatibility.

* 65db4a58 QGrpc{Call,Channel}Options: qHash / QDS overload removal
amendments
Removed qHash and QDataStream overloads from
QGrpc{Call,Channel}Options, as these types do not qualify for
integration yet. Future Qt support may be provided as needed.

* dab0754e Add REMOVED_SINCE for QGrpcOperation related ctor changes
Restricted public construction of QGrpcCallReply and
QGrpc{Client,Server,Bidi}Stream due to unsafe usage patterns.

* 90ba5af9 QGrpcOperationContext: remove argument() instead of
deprecating
Removed QGrpcOperationContext::argument() in favor of the abstract RPC
interface. The class is only reachable through this interface, which is
undocumented and treated as private API.

### qtapplicationmanager (Commercial only)
* 14dca899 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtinterfaceframework (Commercial only)
* c6b7dc6c CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

* 49acad0c Update the bundled qface to the latest version (2.0.13)
The copy of qface in Qt was updated to 2.0.13

* 70a8507a Add deprecation handling to Jinja
Introduced deprecation primitives for templates.

* 11e080ca Compatibility layer for deprecated and commonly used Jinja
files
Renamed Jinja template files to use standard .jinja extensions,
deprecated old .tpl extensions.

### qtinsighttracker (Commercial only)
* ccc955c Add API for sending additional data
Additional data can now be tracked without attaching it to any other
event.


Fixes
-----

### qtbase
* [QTBUG-137277](https://qt-project.atlassian.net/browse/QTBUG-137277) Stack overflow in QFontEngine (due to infinite
recursion)
* [QTBUG-131655](https://qt-project.atlassian.net/browse/QTBUG-131655) Memory leak in QNSViewMenuHelper
* [QTBUG-137161](https://qt-project.atlassian.net/browse/QTBUG-137161) "Leaks" utility in the Instruments app report memory
leak.
* [QTBUG-137316](https://qt-project.atlassian.net/browse/QTBUG-137316) generateJavaQmlComponents will scan relevant import
directories twice
* [QTBUG-137297](https://qt-project.atlassian.net/browse/QTBUG-137297) qmake iOS target: fails to find (prebuilt) .prl
dependencies -> Xcode build fails
* [QTBUG-136346](https://qt-project.atlassian.net/browse/QTBUG-136346) build issue with `-DFEATURE_regularexpression=OFF`
* [QTBUG-137108](https://qt-project.atlassian.net/browse/QTBUG-137108) CE_ComboBoxLabel painting not called anymore on
QProxyStyle, due to QStyleSheetStyle
* [QTBUG-131761](https://qt-project.atlassian.net/browse/QTBUG-131761) Incorrect display of :selected state of QCombobox on
"windows" style plugin
* [QTBUG-136967](https://qt-project.atlassian.net/browse/QTBUG-136967) qjniarray.h:775:46: error: a template argument list is
expected
* [QTBUG-86287](https://qt-project.atlassian.net/browse/QTBUG-86287) Static 5.15.0 compile results in "undefined reference to
xcb_aux_create_gc"
* [QTBUG-137004](https://qt-project.atlassian.net/browse/QTBUG-137004) xcb-image is missing dependency on xcb-aux
* [QTBUG-135634](https://qt-project.atlassian.net/browse/QTBUG-135634) macOS: Deleted menu is not removed from native menu bar
* [QTBUG-136550](https://qt-project.atlassian.net/browse/QTBUG-136550) QMYSQL: QT application built with libmariadb3.4 won't
connect to MariaDB 10
* [QTBUG-136450](https://qt-project.atlassian.net/browse/QTBUG-136450) Top flaky test: tst_xdgshell::showMinimized
* [QTBUG-137398](https://qt-project.atlassian.net/browse/QTBUG-137398) A crash occurred in C:\Users\qt\work\qt\qtdeclarative_st
andalone_tests\tests\auto\quickdialogs\qquickfontdialogimpl\tst_qquickfo
ntdialogimpl.exe
* [QTBUG-137198](https://qt-project.atlassian.net/browse/QTBUG-137198) Configure fails with -DFEATURE_sanitize_thread=ON
-DFEATURE_sanitize_address=ON without a proper message
* [QTBUG-133687](https://qt-project.atlassian.net/browse/QTBUG-133687) Confusing instructions when atomicfptr config.test fails
* [QTBUG-136229](https://qt-project.atlassian.net/browse/QTBUG-136229) Fullscreen virtual keyboard: issue with selection and
delete
* [QTBUG-136074](https://qt-project.atlassian.net/browse/QTBUG-136074) QTreeView a11y: Frequent Qt Creator crashes when Orca
screen reader is active
* [QTBUG-133855](https://qt-project.atlassian.net/browse/QTBUG-133855)  QtreeView sporadic crash when setCurrentIndex is called
* [QTBUG-136960](https://qt-project.atlassian.net/browse/QTBUG-136960) Checkbox in QTreeview shows black outline in dark mode
* [QTBUG-137249](https://qt-project.atlassian.net/browse/QTBUG-137249) QML Screen.orientation on iOS does not provide all
directions
* [QTBUG-134602](https://qt-project.atlassian.net/browse/QTBUG-134602) Rendering of QQuickText slightly elevated.
* [QTBUG-134143](https://qt-project.atlassian.net/browse/QTBUG-134143) QColorDialog: Unable to pick color after switching
windows using  Windows Task View
* [QTBUG-136590](https://qt-project.atlassian.net/browse/QTBUG-136590) Regression in QTextTable: border-collapse cell border
rendering broken
* [QTBUG-137011](https://qt-project.atlassian.net/browse/QTBUG-137011) The icon of the QCommandLinkButton does not update when
the button's visibility is set to true.
* [QTBUG-137329](https://qt-project.atlassian.net/browse/QTBUG-137329) QFileDialog::getOpenFileContent opens a non-modal dialog
* [QTBUG-134060](https://qt-project.atlassian.net/browse/QTBUG-134060) QTextCharFormat::setFont() doesn’t set the font features
for OpenType fonts
* [QTBUG-133904](https://qt-project.atlassian.net/browse/QTBUG-133904) Corrupted qml rendering on some Android PowerVR devices
after the app is killed
* [QTBUG-134245](https://qt-project.atlassian.net/browse/QTBUG-134245) [Reg 6.8.0 -> 6.8.2] Strange 4-quadrant colouration of
Qt Quick items
* [QTBUG-134089](https://qt-project.atlassian.net/browse/QTBUG-134089) Power VR rendering failure on Qt 6.8.2
* [QTBUG-135411](https://qt-project.atlassian.net/browse/QTBUG-135411) Android visual Glitches on 6.8.2+
* [QTBUG-134496](https://qt-project.atlassian.net/browse/QTBUG-134496) Drawing errors on some Android devices
* [QTBUG-135810](https://qt-project.atlassian.net/browse/QTBUG-135810) [REG 6.8.1 -> 6.8.3] Crashes in QRhi::endFrame /
glDrawElements on Android
* [QTBUG-136487](https://qt-project.atlassian.net/browse/QTBUG-136487) Improve opening description of Qt's Paint System
* [QTBUG-128494](https://qt-project.atlassian.net/browse/QTBUG-128494) [Android] Accessible.description
* [QTBUG-137427](https://qt-project.atlassian.net/browse/QTBUG-137427) HTTP 2 request cancellation timing issue may lead to
severed connection
* [QTBUG-115293](https://qt-project.atlassian.net/browse/QTBUG-115293) tst_QGraphicsItem::itemUsesExtendedStyleOption() with
QtWayland failed on Ubuntu 22.04, GNOME
* [QTBUG-135844](https://qt-project.atlassian.net/browse/QTBUG-135844) Windows: QPainter errors when maximizing/resizing window
* [QTBUG-136990](https://qt-project.atlassian.net/browse/QTBUG-136990) QML property information rendered mangled (Assistant, Qt
Creator)
* [QTBUG-137041](https://qt-project.atlassian.net/browse/QTBUG-137041) Schannel plugin incorrectly verifies the
NetscapeCertType extension
* [QTBUG-126743](https://qt-project.atlassian.net/browse/QTBUG-126743) If QT_ANDROID_PACKAGE_SOURCE_DIR is set to a specific
path, a build folder is recursively created within the build folder.
* [QTBUG-137346](https://qt-project.atlassian.net/browse/QTBUG-137346) [Reg 6.8.0->6.8.1]QTableView ignores the stylesheet
background color when hovering over the items.
* [QTBUG-133656](https://qt-project.atlassian.net/browse/QTBUG-133656) During Transition from DST back to standard time. the
local clock time repeats an hour.
* [QTBUG-137556](https://qt-project.atlassian.net/browse/QTBUG-137556) [FTBFS] QtCore doc snippets link to QtWidgets
* [QTBUG-113401](https://qt-project.atlassian.net/browse/QTBUG-113401) QtConcurrent::run parameter order documentation wrong
* [QTBUG-135643](https://qt-project.atlassian.net/browse/QTBUG-135643) Window glitches when using Qt::ExpandedClientAreaHint
* [QTBUG-133943](https://qt-project.atlassian.net/browse/QTBUG-133943) Qt::ExpandedClientAreaHint results in different rounded
window corners on Windows
* [QTBUG-133946](https://qt-project.atlassian.net/browse/QTBUG-133946) Qt::ExpandedClientAreaHint breaks minimizing on Windows
* [QTBUG-137157](https://qt-project.atlassian.net/browse/QTBUG-137157) [macOS] QAccessibleInterface::window() is never called;
accessibility tools cannot see the top-level window that holds a
widget/Item
* [QTBUG-25938](https://qt-project.atlassian.net/browse/QTBUG-25938) Checkable QGroupBox doesn't keep "enabled" status of
children
* [QTBUG-136055](https://qt-project.atlassian.net/browse/QTBUG-136055) QWebSocketServer creates persistent files in
Microsoft/Crypto/RSA on each new client connection.
* [QTBUG-137027](https://qt-project.atlassian.net/browse/QTBUG-137027) GetMethodID received NULL jclass
* [QTBUG-136097](https://qt-project.atlassian.net/browse/QTBUG-136097) Can't use the properties and signals when definitions
such as them are enabled by `__has_include`
* [QTBUG-135337](https://qt-project.atlassian.net/browse/QTBUG-135337) crash when connecting with RDP
* [QTBUG-63252](https://qt-project.atlassian.net/browse/QTBUG-63252) QHostAddress::isInSubnet() parameter "netmask" is
misleading
* [QTBUG-136176](https://qt-project.atlassian.net/browse/QTBUG-136176) [Reg 6.8.3 -> 6.9.0]QIcon::ThemeIcon::DialogInformation
is missing pixels.
* [QTBUG-134604](https://qt-project.atlassian.net/browse/QTBUG-134604) edit-redo icon is clipped on Windows
* [QTBUG-109599](https://qt-project.atlassian.net/browse/QTBUG-109599) Password characters are not visible with a screenreader
* [QTBUG-137579](https://qt-project.atlassian.net/browse/QTBUG-137579) QDebugStateSaver not documented well
* [QTBUG-137452](https://qt-project.atlassian.net/browse/QTBUG-137452) compile error in moc-generated code if slot/property
name equals return type name
* [QTBUG-137467](https://qt-project.atlassian.net/browse/QTBUG-137467) qt.qpa.wayland: wrong transient parent of the popup
* [QTBUG-137727](https://qt-project.atlassian.net/browse/QTBUG-137727) Crash in zwp_text_input_v3_set_surrounding_text when
selecting large text
* [QTBUG-137755](https://qt-project.atlassian.net/browse/QTBUG-137755) Regression: Segfault on closing a program using
QDockWidgets, introduced by ab6f1ad77852a427ae73172ca11dacf876a0cbf7
* [QTBUG-137814](https://qt-project.atlassian.net/browse/QTBUG-137814) Build broken with -no-feature-sharedmemory
* [QTBUG-96379](https://qt-project.atlassian.net/browse/QTBUG-96379) Missing documentation for QMetaContainer
* [QTBUG-125319](https://qt-project.atlassian.net/browse/QTBUG-125319) Scaling issue occurs when the window is moved due to
disconnecting the screen.
* [QTBUG-137739](https://qt-project.atlassian.net/browse/QTBUG-137739) [REG 6.9.1-6.10.0 beta1] opengl/cube not launching on
Wayland
* [QTBUG-137850](https://qt-project.atlassian.net/browse/QTBUG-137850) moc_qwaylandxdgshell.cpp:625:60: error: template
argument 1 is invalid
* [QTBUG-137822](https://qt-project.atlassian.net/browse/QTBUG-137822) Qcocoa build is broken
* [QTBUG-134239](https://qt-project.atlassian.net/browse/QTBUG-134239) QAbstractFileIconProvider::icon() always returns null on
mobile platforms
* [QTBUG-134896](https://qt-project.atlassian.net/browse/QTBUG-134896) QUrl's qHash() is inconsistent with its operator==
* [QTBUG-134900](https://qt-project.atlassian.net/browse/QTBUG-134900) QUrl's operator==() is taking bygone data into account
* [QTBUG-137763](https://qt-project.atlassian.net/browse/QTBUG-137763) windeployqt crash when run through cmake
* [QTBUG-87180](https://qt-project.atlassian.net/browse/QTBUG-87180) Typo in the description of QGraphicsSimpleTextItem class
* [QTBUG-137870](https://qt-project.atlassian.net/browse/QTBUG-137870) cmake: qt can only be built once
* [QTBUG-120031](https://qt-project.atlassian.net/browse/QTBUG-120031) xcb: Modal state may get lost due to a race
* [QTBUG-133029](https://qt-project.atlassian.net/browse/QTBUG-133029) Documentation is inconsistent wrt QChronoTimer
* [QTBUG-123063](https://qt-project.atlassian.net/browse/QTBUG-123063) XCB flakiness in tst_qgraphicsscene (race condition
caused by the event dispatcher on Linux)
* [QTBUG-127705](https://qt-project.atlassian.net/browse/QTBUG-127705) Android splashscreen not removed
* [QTBUG-124140](https://qt-project.atlassian.net/browse/QTBUG-124140) [REG]: 6.7.0  full-screen app displays background window
(or splash-screen) graphics at top/bottom during multiwindow split
display
* [QTBUG-137838](https://qt-project.atlassian.net/browse/QTBUG-137838) QMultiHash has undocumented erase method
* [QTBUG-130978](https://qt-project.atlassian.net/browse/QTBUG-130978) Auto-scrolling breaks when dragging and dropping an item
in QTreeView.
* [QTBUG-137700](https://qt-project.atlassian.net/browse/QTBUG-137700) QIcon::pixmap selects wrong icon file from theme
* [QTBUG-90634](https://qt-project.atlassian.net/browse/QTBUG-90634) QIcon not preferring Hi DPI pixmaps when scaling
* [QTBUG-136130](https://qt-project.atlassian.net/browse/QTBUG-136130) background color of QTreeViewItems with windows 11 style
* [QTBUG-136060](https://qt-project.atlassian.net/browse/QTBUG-136060) Build leaks host kernel version into artifact
* [QTBUG-137882](https://qt-project.atlassian.net/browse/QTBUG-137882) top-level build, examples don't respect -linker
configure option
* [QTBUG-136009](https://qt-project.atlassian.net/browse/QTBUG-136009) Wayland: QGuiApplication::setOverrideCursor doesn't work
when app is freezed
* [QTBUG-95325](https://qt-project.atlassian.net/browse/QTBUG-95325) Removal of QTextStream::setCodec is not documented
* [QTBUG-137986](https://qt-project.atlassian.net/browse/QTBUG-137986) rhi/vulkan: Do something about VUID-vkQueueSubmit-
pSignalSemaphores-00067
* [QTBUG-138043](https://qt-project.atlassian.net/browse/QTBUG-138043) QMultiMap documentation error
* [QTBUG-133631](https://qt-project.atlassian.net/browse/QTBUG-133631) wasm: TextField with echo mode password should not try
to autocomplete
* [QTBUG-134795](https://qt-project.atlassian.net/browse/QTBUG-134795) Add note about HAVE_TICK_COUNTER dependency
* [QTBUG-113759](https://qt-project.atlassian.net/browse/QTBUG-113759) Sort alphabetically the list items on
https://doc.qt.io/qt-6/stylesheet-reference.html
* [QTBUG-127490](https://qt-project.atlassian.net/browse/QTBUG-127490) Doc for Q_DECLARE_OPERATORS_FOR_FLAGS only mentions
operator|()
* [QTBUG-130765](https://qt-project.atlassian.net/browse/QTBUG-130765) Fix excessive use of note sections in QDateTime
documentation
* [QTBUG-137702](https://qt-project.atlassian.net/browse/QTBUG-137702) [REG Qt 6.9.0 -> 6.9.1] Crash when completing code
* [QTBUG-137587](https://qt-project.atlassian.net/browse/QTBUG-137587) qtdeclarative: do_compile failed when building with high
parallelism.
* [QTBUG-133725](https://qt-project.atlassian.net/browse/QTBUG-133725) qml_tool_autogen target loses almost all dependencies on
other autogen and sync_headers targets
* [QTBUG-135785](https://qt-project.atlassian.net/browse/QTBUG-135785) Windows Vista/11 style does not use correct font for mdi
menu entries
* [QTBUG-78013](https://qt-project.atlassian.net/browse/QTBUG-78013) QIdentityProxyModel::match inappropriately mixes use of
proxy model index and source model data method
* [QTBUG-126054](https://qt-project.atlassian.net/browse/QTBUG-126054) QString::arg(wchar_t{}) prefers the integral overload
instead of the QChar one
* [QTBUG-138100](https://qt-project.atlassian.net/browse/QTBUG-138100) ios file icon provider missing QUrl include
* [QTBUG-102240](https://qt-project.atlassian.net/browse/QTBUG-102240) QStringList incorrect inheritance documentation
* [QTBUG-49564](https://qt-project.atlassian.net/browse/QTBUG-49564) QTextCharFormat fontPointSize() doesnt not return the
same as QTextCharFormat font().pointSize()
* [QTBUG-136217](https://qt-project.atlassian.net/browse/QTBUG-136217) Windows11 style does not show underlying content of
index widget.
* [QTBUG-119501](https://qt-project.atlassian.net/browse/QTBUG-119501) Numbers colliding and not highlighted in Charts with
Widgets Gallery example
* [QTBUG-138049](https://qt-project.atlassian.net/browse/QTBUG-138049) QScrollBar::createStandardContextMenu does not set QMenu
parent vs. QLineEdit, QPlainTextEdit, QTextEdit
* [QTBUG-138172](https://qt-project.atlassian.net/browse/QTBUG-138172) a11y: QToolButton menu not exposed on a11y layer when it
comes from default action
* [QTBUG-137344](https://qt-project.atlassian.net/browse/QTBUG-137344) a11y AT-SPI: org.freedesktop.DBus.Properties "GetAll"
queries trigger application crash
* [QTBUG-137806](https://qt-project.atlassian.net/browse/QTBUG-137806) [Android][A11y] Role of UI elements is missing
* [QTBUG-138201](https://qt-project.atlassian.net/browse/QTBUG-138201) Arranging QDockWidgets programatically causes
segmentation faults
* [QTBUG-129023](https://qt-project.atlassian.net/browse/QTBUG-129023) tst_QWindow::windowExposedAfterReparent() failed on
Ubuntu 24.04 GNOME X11
* [QTBUG-112692](https://qt-project.atlassian.net/browse/QTBUG-112692) QPropertyNotifier and related APIs have no \since
version
* [QTBUG-138158](https://qt-project.atlassian.net/browse/QTBUG-138158) QT_DISCARD_FILE_CONTENTS does not work as expected
* [QTBUG-136490](https://qt-project.atlassian.net/browse/QTBUG-136490) QSqlQueryModel::setLastError should be const
* [QTBUG-135238](https://qt-project.atlassian.net/browse/QTBUG-135238) QDateTime::toTimeZone doc's code snippet calls
deprecated ::toTimeSpec
* [QTBUG-138168](https://qt-project.atlassian.net/browse/QTBUG-138168) Fix a typo in the licenseRule.json file in qtbase
* [QTBUG-138226](https://qt-project.atlassian.net/browse/QTBUG-138226) QTranslator deadlocks trying to translate translation
file loading error
* [QTBUG-138196](https://qt-project.atlassian.net/browse/QTBUG-138196) [REG dev] Fusion: Buttons and comboboxes outlined
* [QTBUG-59186](https://qt-project.atlassian.net/browse/QTBUG-59186) Error in QIODevice::readLine() documentation about
handling newline char
* [QTBUG-137438](https://qt-project.atlassian.net/browse/QTBUG-137438) [REG 6.9.0 -> 6.9.1] QTemporaryFile
* [QTBUG-88466](https://qt-project.atlassian.net/browse/QTBUG-88466) Thread safety of QTranslator::translate
* [QTBUG-138130](https://qt-project.atlassian.net/browse/QTBUG-138130) QTableView misrendered since qt 6.9
* [QTBUG-132590](https://qt-project.atlassian.net/browse/QTBUG-132590) Unclear relation between
QTemporaryFile::{autoRemove,rename}()
* [QTBUG-137179](https://qt-project.atlassian.net/browse/QTBUG-137179) Crash in QTranslatorPrivate::do_translate (QQmlThread)
after QTranslator::load (main thread)
* [QTBUG-117414](https://qt-project.atlassian.net/browse/QTBUG-117414) Doc: Give hints how to get a QScreen object
* [QTBUG-127116](https://qt-project.atlassian.net/browse/QTBUG-127116) REG: QML Window Background Issue on Windows After
Minimizing and Restoring in Qt 6.5+
* [QTBUG-137120](https://qt-project.atlassian.net/browse/QTBUG-137120) [Regression] Right and top dockwidget area are not
resizable anymore
* [QTBUG-129242](https://qt-project.atlassian.net/browse/QTBUG-129242) QTableWidget selection issue
* [QTBUG-137776](https://qt-project.atlassian.net/browse/QTBUG-137776) Windows11 style, QTableView cell selection behavior
* [QTBUG-128794](https://qt-project.atlassian.net/browse/QTBUG-128794) QLineEdit in Android - no text visual
* [QTBUG-133549](https://qt-project.atlassian.net/browse/QTBUG-133549) Qt UI stops redrawing on Android
* [QTBUG-128457](https://qt-project.atlassian.net/browse/QTBUG-128457) QSpinBox does not respond correctly to Android keyboard
* [QTBUG-128422](https://qt-project.atlassian.net/browse/QTBUG-128422) [Android] Can't change selection in QComboBox with touch
input
* [QTBUG-121757](https://qt-project.atlassian.net/browse/QTBUG-121757) Entered text is invisible in QLineEdit until field focus
is changed
* [QTBUG-138261](https://qt-project.atlassian.net/browse/QTBUG-138261) QPlatformBackingStore doesn't handle QtGui-level
fractional scaling
* [QTBUG-134757](https://qt-project.atlassian.net/browse/QTBUG-134757) [REG 6.7.3->6.8.0] QWidgetAction: No contextMenuEvent
* [QTBUG-120167](https://qt-project.atlassian.net/browse/QTBUG-120167) Reg->6.7: QComboxbox hover is broken
* [QTBUG-60355](https://qt-project.atlassian.net/browse/QTBUG-60355) QMetaEnum docs have no code examples
* [QTBUG-136138](https://qt-project.atlassian.net/browse/QTBUG-136138) Blank screen in CarPlay Simulator with Qt-based iOS app
due to assertion: "[scene isKindOfClass:UIWindowScene.class]" in
qiosapplicationdelegate.mm
* [QTBUG-137978](https://qt-project.atlassian.net/browse/QTBUG-137978) Qt.inputMethod.visible changes to true in orientation
change on iOS26 beta
* [QTBUG-33977](https://qt-project.atlassian.net/browse/QTBUG-33977) Suggested change to QCoreApplication documentation
* [QTBUG-85428](https://qt-project.atlassian.net/browse/QTBUG-85428) Documentation for QScrollBar can be improved
* [QTBUG-137393](https://qt-project.atlassian.net/browse/QTBUG-137393) No drag cursor when dragging under wayland
* [QTBUG-138183](https://qt-project.atlassian.net/browse/QTBUG-138183) The drop area for QToolBar gets triggered even when the
toolbar is not on the window.
* [QTBUG-138032](https://qt-project.atlassian.net/browse/QTBUG-138032) calqlatr: Example prints 'stale focus object [...],
doing manual update' warnings
* [QTBUG-138256](https://qt-project.atlassian.net/browse/QTBUG-138256) QPlatformInputContext::update() called with stale focus
object
* [QTBUG-106709](https://qt-project.atlassian.net/browse/QTBUG-106709) Application looks too small on an external display with
iPadOS 16.1 on M1 iPad
* [QTBUG-137544](https://qt-project.atlassian.net/browse/QTBUG-137544) QML iPad app window stays black when launched on
external display
* [QTBUG-138230](https://qt-project.atlassian.net/browse/QTBUG-138230) QCheckBox used as editor in delegate does not display
checkmark when using Windows11 style and no text
* [QTBUG-135213](https://qt-project.atlassian.net/browse/QTBUG-135213) QTreeView creates ghost artifacts when scrolling
* [QTBUG-120254](https://qt-project.atlassian.net/browse/QTBUG-120254) Cell value leaking into other cells when entering new
value
* [QTBUG-133845](https://qt-project.atlassian.net/browse/QTBUG-133845)  QSpinBoxes take too much vertical space if an
application-wide style sheet is set since Qt 6.8.2
* [QTBUG-130642](https://qt-project.atlassian.net/browse/QTBUG-130642) Incorrect QAbstractSpinBox size hint in Windows 11 style
when style sheet is set
* [QTBUG-132431](https://qt-project.atlassian.net/browse/QTBUG-132431) Stylesheet Margin/Padding squashes QSpinBox
* [QTBUG-138428](https://qt-project.atlassian.net/browse/QTBUG-138428) tst_QTextStream::pos3LargeFile() takes an extraordinary
amount of time to execute
* [QTBUG-138435](https://qt-project.atlassian.net/browse/QTBUG-138435) QTextStream::pos() seems to be linear over QFile size
(or QFile::pos())
* [QTBUG-134740](https://qt-project.atlassian.net/browse/QTBUG-134740) [REG 6.7.3 -> 6.8.0] QDir::entryInfoList slower
accessing SMB share from macOS
* [QTBUG-138374](https://qt-project.atlassian.net/browse/QTBUG-138374) QFileSystemWatcher::addPath() is slow on macos
* [QTBUG-138238](https://qt-project.atlassian.net/browse/QTBUG-138238) NPE when calling QtNetwork.unregisterReceiver() at exit
* [QTBUG-135928](https://qt-project.atlassian.net/browse/QTBUG-135928) Connection to D-Bus signals silently breaks if D-Bus was
used before creating QCoreApplication
* [QTBUG-136231](https://qt-project.atlassian.net/browse/QTBUG-136231) Min c++ version required for QtWebengine
* [QTBUG-138401](https://qt-project.atlassian.net/browse/QTBUG-138401) [REG dev] Windows11 Style: Check-boxes' drawing
regression
* [QTBUG-138094](https://qt-project.atlassian.net/browse/QTBUG-138094) Radiobuttons/Checkboxes in windows11 style do not follow
WinUI3 style
* [QTBUG-125366](https://qt-project.atlassian.net/browse/QTBUG-125366) Selectable QLabel does not copy to clipboard as
QLineEdit does
* [QTBUG-138484](https://qt-project.atlassian.net/browse/QTBUG-138484) QTextStream assumes single-character
QLocale::{positive,negative}Sign()
* [QTBUG-138206](https://qt-project.atlassian.net/browse/QTBUG-138206) a11y: Docked QDockWidget reports incorrect role and
window-relative position via AT-SPI
* [QTBUG-138523](https://qt-project.atlassian.net/browse/QTBUG-138523) qtbase doesn't build with -no-feature-sessionmanager
-feature-wayland-client
* [QTBUG-137519](https://qt-project.atlassian.net/browse/QTBUG-137519) Memory corruption for tst_qsettings with JSPI
* [QTBUG-138008](https://qt-project.atlassian.net/browse/QTBUG-138008) Permissions test app crashes on emulator.
* [QTBUG-138372](https://qt-project.atlassian.net/browse/QTBUG-138372) QLocalSocket never emits ConnectedState in Linux
* [QTBUG-138566](https://qt-project.atlassian.net/browse/QTBUG-138566) QLocale::codeToScript() can't find QLocale::LastScript
* [QTBUG-138597](https://qt-project.atlassian.net/browse/QTBUG-138597) Grant Android runtime permissions to the android bundles
* [QTBUG-138565](https://qt-project.atlassian.net/browse/QTBUG-138565) "Cannot generate qmltypes file" when trying to run in-
app purchase demo app on Android
* [QTBUG-138585](https://qt-project.atlassian.net/browse/QTBUG-138585) tst_qxmlstream failed on webOS building
* [QTBUG-132617](https://qt-project.atlassian.net/browse/QTBUG-132617) Unclear behaviour of QTemporaryFile::rename()
* [QTBUG-132646](https://qt-project.atlassian.net/browse/QTBUG-132646) Add a variant of QTemporaryFile::rename() that
overwrites
* [QTBUG-136163](https://qt-project.atlassian.net/browse/QTBUG-136163) sbom/spdx file not reproducible (contains build path)
* [QTBUG-138660](https://qt-project.atlassian.net/browse/QTBUG-138660) QHttp2Stream: dtor missing sendRST_STREAM for some
state(s)
* [QTBUG-138156](https://qt-project.atlassian.net/browse/QTBUG-138156) tst_QHttpServer::disconnectedInEventLoop leaves a bad
state making multipleRequests fail
* [QTBUG-138603](https://qt-project.atlassian.net/browse/QTBUG-138603) [Reg 6.9.1 -> 6.10.0b2][CMake] Most private modules are
no longer accessible
* [QTBUG-123585](https://qt-project.atlassian.net/browse/QTBUG-123585) Memory Leak: QGestureRecognizer::unregisterRecognizer()
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
* [QTBUG-99277](https://qt-project.atlassian.net/browse/QTBUG-99277) QDBusContext does not work with property methods
* [QTBUG-138157](https://qt-project.atlassian.net/browse/QTBUG-138157) QWindow::safeAreaMargins() returns incorrect values when
virtual keyboard opens on Android (Qt 6.9)
* [QTBUG-131448](https://qt-project.atlassian.net/browse/QTBUG-131448) Cannot QMovie::moveToThread
* [QTBUG-131513](https://qt-project.atlassian.net/browse/QTBUG-131513) [iOS] QSysInfo::productVersion() incomplete?
* [QTBUG-129027](https://qt-project.atlassian.net/browse/QTBUG-129027) tst_QStatusBar::QTBUG4334_hiddenOnMaximizedWindow()
failed on Ubuntu 24.04 GNOME X11
* [QTBUG-135954](https://qt-project.atlassian.net/browse/QTBUG-135954) [REG] Wayland: Over 2x higher painting CPU usage when
display scaling is used
* [QTBUG-138642](https://qt-project.atlassian.net/browse/QTBUG-138642) ODBC possible data loss with 'real' column
* [QTBUG-8963](https://qt-project.atlassian.net/browse/QTBUG-8963) Driver for ODBC - qsql_odbc.cpp should use the
QMetaType:float when sql type is SQL_FLOAT instead of QVariant::Double
* [QTBUG-68865](https://qt-project.atlassian.net/browse/QTBUG-68865) tst_QMenuBar::check_menuPosition autotest fails on Ubuntu
18.04
* [QTBUG-136629](https://qt-project.atlassian.net/browse/QTBUG-136629) QUnifiedTimer::updateAnimationTimers() crashes when
QApplication is recreated
* [QTBUG-93182](https://qt-project.atlassian.net/browse/QTBUG-93182) Occasional asserts when touch scroll NSEventPhaseEnded is
processed while event in queue indicates momentumPhase has begun
* [QTBUG-138864](https://qt-project.atlassian.net/browse/QTBUG-138864) qt-android-runner.py doesn't find package name
* [QTBUG-135641](https://qt-project.atlassian.net/browse/QTBUG-135641) QNetworkDiskCache leaks file descriptors
* [QTBUG-138748](https://qt-project.atlassian.net/browse/QTBUG-138748) QContainerLayer is being erroneously passed to
vkCreateMetalSurfaceEXT, causing a crash
* [QTBUG-138824](https://qt-project.atlassian.net/browse/QTBUG-138824) Segmentation fault in tst_qquickaccessible
* [QTBUG-135964](https://qt-project.atlassian.net/browse/QTBUG-135964) Windows theme uses wrong colors if high-contrast mode is
activated
* [QTBUG-138648](https://qt-project.atlassian.net/browse/QTBUG-138648) QSettings (IniFormat) fails to find keys after
beginGroup() if subgroups exist
* [QTBUG-138474](https://qt-project.atlassian.net/browse/QTBUG-138474) windeployqt: Warning: module icuuc could not be found
* [QTBUG-138056](https://qt-project.atlassian.net/browse/QTBUG-138056) QSortFilterProxyModel: Crash when changing sourceModel
(QPropertyBindingData / QBindingStorage)
* [QTBUG-138488](https://qt-project.atlassian.net/browse/QTBUG-138488) [iOS] URL handler do not receive data from external apps
via Universal Link
* [QTBUG-138894](https://qt-project.atlassian.net/browse/QTBUG-138894) Android fails to start without accessibility
* [QTBUG-138904](https://qt-project.atlassian.net/browse/QTBUG-138904) QIBASE driver fails to build when linking against
Firebird v2.5
* [QTBUG-138922](https://qt-project.atlassian.net/browse/QTBUG-138922) Consistent Qt caused crash when navigating with Jetpack
Compose
* [QTBUG-138986](https://qt-project.atlassian.net/browse/QTBUG-138986) glFramebufferTexture2DMultisampleEXT() is called with a
wrong samples argument if the requested sample count is unsupported
* [QTBUG-138861](https://qt-project.atlassian.net/browse/QTBUG-138861) `QRhiResourceUpdateBatch` leaks memory if submitted via
`beginOffscreenFrame`
* [QTBUG-138250](https://qt-project.atlassian.net/browse/QTBUG-138250) Win11 23h2 ARM: QtBase -
tst_QRhi::storageBufferRuntimeSizeGraphics(OpenGL) 'pipeline->create()'
returned FALSE
* [QTBUG-138580](https://qt-project.atlassian.net/browse/QTBUG-138580) [REG 6.10.0 beta1 -> beta2] CMake test including all
modules fails
* [QTBUG-138542](https://qt-project.atlassian.net/browse/QTBUG-138542) [Wayland] Cursor changes to resize arrows in the area of
the app window
* [QTBUG-124011](https://qt-project.atlassian.net/browse/QTBUG-124011) Android: QFileInfo::isWritable() returns false
erroneously and throws an exception
* [QTBUG-115143](https://qt-project.atlassian.net/browse/QTBUG-115143) Unable to open files under certain conditions on
Android.
* [QTBUG-114979](https://qt-project.atlassian.net/browse/QTBUG-114979) Two issues using content scheme to work with files
* [QTBUG-139128](https://qt-project.atlassian.net/browse/QTBUG-139128) QObject::connect(): clarify what a valid method is, in
the string-based overloads
* [QTBUG-132490](https://qt-project.atlassian.net/browse/QTBUG-132490) Android and TestNamespace: errors in Qt JNI methods
* [QTBUG-139051](https://qt-project.atlassian.net/browse/QTBUG-139051) Background color of QPlainTextEdit without border
cannont be set on Win11
* [QTBUG-93371](https://qt-project.atlassian.net/browse/QTBUG-93371) arabic text shapes incorrectly when using accelerator
* [QTBUG-139250](https://qt-project.atlassian.net/browse/QTBUG-139250) Top-level tool window doesnt oppen
* [QTBUG-138947](https://qt-project.atlassian.net/browse/QTBUG-138947) QProgressBar completely blank on macOS 26
* [QTBUG-138942](https://qt-project.atlassian.net/browse/QTBUG-138942) Mac style (Widget and Quick) has issues on macOS 26
* [QTBUG-123404](https://qt-project.atlassian.net/browse/QTBUG-123404) QtWayland uses unexported QThreadPrivate, fails UBSan
build
* [QTBUG-139119](https://qt-project.atlassian.net/browse/QTBUG-139119) QFuture::takeResult asserts
* [QTBUG-139286](https://qt-project.atlassian.net/browse/QTBUG-139286) Make Platform Notes section optional in app-examples-
template
* [QTBUG-139292](https://qt-project.atlassian.net/browse/QTBUG-139292) Make section titles more language-neutral in app-
examples-template
* [QTBUG-138570](https://qt-project.atlassian.net/browse/QTBUG-138570) [REG 6.9.1 -> 6.10.0 Beta 2]
QFileSystemEngine::cloneFileTo hangs on FreeBSD 14.3
* [QTBUG-139106](https://qt-project.atlassian.net/browse/QTBUG-139106) REG: Variable fonts no longer works with Freetype
backend
* [QTBUG-137769](https://qt-project.atlassian.net/browse/QTBUG-137769) Keyboard is not closed when TextEdit loses focus while
using TalkBack
* [QTBUG-108329](https://qt-project.atlassian.net/browse/QTBUG-108329) tst_qfiledialog::completer() fails
* [QTBUG-101194](https://qt-project.atlassian.net/browse/QTBUG-101194) tst_QFileDialog has failing tests for Android
* [QTBUG-138982](https://qt-project.atlassian.net/browse/QTBUG-138982) qt-android-runner.py fails to start application
* [QTBUG-138622](https://qt-project.atlassian.net/browse/QTBUG-138622) Android launch wrapper script can conflict with qml
subdirectory name on case insensitive file systems
* [QTBUG-139211](https://qt-project.atlassian.net/browse/QTBUG-139211) tst_qquickpopup (Failed)
* [QTBUG-100991](https://qt-project.atlassian.net/browse/QTBUG-100991) Some tests crash on Android CI
* [QTBUG-131695](https://qt-project.atlassian.net/browse/QTBUG-131695) tst_qquickpopup tst_QQuickPopup::fadeDimmer is flaky
* [QTBUG-125083](https://qt-project.atlassian.net/browse/QTBUG-125083) [Android] ANRs related to QtNativeInputConnection
* [QTBUG-132695](https://qt-project.atlassian.net/browse/QTBUG-132695) Crash in QGuiApplication::applicationStateChanged() when
quitting app
* [QTBUG-139400](https://qt-project.atlassian.net/browse/QTBUG-139400) Properly manage QtEditText focus and InputConnection
callbacks
* [QTBUG-138561](https://qt-project.atlassian.net/browse/QTBUG-138561) QFont::exactMatch index out of bounds
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
* [QTBUG-139334](https://qt-project.atlassian.net/browse/QTBUG-139334) a11y: Qt doesn't support the AT-SPI Collection interface
* [QTBUG-139263](https://qt-project.atlassian.net/browse/QTBUG-139263) Missing operator documentation in QFont::Tag
* [QTBUG-139056](https://qt-project.atlassian.net/browse/QTBUG-139056) [Wayland] Crash on drag and drop cancel by escape
* [QTBUG-138984](https://qt-project.atlassian.net/browse/QTBUG-138984) Possible misinterpretation of
specifications.freedesktop.org/trash-spec
* [QTBUG-126134](https://qt-project.atlassian.net/browse/QTBUG-126134) Restarting multiple QThreads results in a crash
* [QTBUG-138504](https://qt-project.atlassian.net/browse/QTBUG-138504) Crash on Integer Overflow in QCheckedInt Operator+
(ASSERT in qcheckedint_impl.h:69)
* [QTBUG-139600](https://qt-project.atlassian.net/browse/QTBUG-139600) Memory leak on macOS when adding application font from
data
* [QTBUG-125138](https://qt-project.atlassian.net/browse/QTBUG-125138) QSqlDatabase::record() does not report generated columns
for SQlite
* [QTBUG-139591](https://qt-project.atlassian.net/browse/QTBUG-139591) tst_qtquickview_basic times out
* [QTBUG-139227](https://qt-project.atlassian.net/browse/QTBUG-139227) [Windows] QMenuBar not displayed correctly with QDialog
* [QTBUG-139615](https://qt-project.atlassian.net/browse/QTBUG-139615) [REG 6.10.0 Beta2 -> 6.10.0 Beta3] error: non-POD static
* [QTBUG-139284](https://qt-project.atlassian.net/browse/QTBUG-139284) Include squish-tested-example.qdocinc file to the app-
examples-template
* [QTBUG-139586](https://qt-project.atlassian.net/browse/QTBUG-139586) [Reg 6.9.1->6.9.2] Cannot send broadcast on macOS
anymore
* [QTBUG-138848](https://qt-project.atlassian.net/browse/QTBUG-138848) Content-Length header always sent in HTTP GET request
* [QTBUG-138465](https://qt-project.atlassian.net/browse/QTBUG-138465) Line edits are not visible on macOS 26
* [QTBUG-139360](https://qt-project.atlassian.net/browse/QTBUG-139360) Editable combo box on macOS Tahoe
* [QTBUG-138946](https://qt-project.atlassian.net/browse/QTBUG-138946) QSlider issues on macOS 26
* [QTBUG-139202](https://qt-project.atlassian.net/browse/QTBUG-139202) Button colors are wrong in dark mode on Windows 11
* [QTBUG-139439](https://qt-project.atlassian.net/browse/QTBUG-139439) CMake fails due to 'pthread_cancel' when configuring Qt
project for Android with CMake 4.x
* [QTBUG-139719](https://qt-project.atlassian.net/browse/QTBUG-139719) a11y: Label buddy misses labelled-by relation if it's
not a sibling
* [QTBUG-135808](https://qt-project.atlassian.net/browse/QTBUG-135808) Some problems with Expanded Client Areas on Android
* [QTBUG-139778](https://qt-project.atlassian.net/browse/QTBUG-139778) BIC: Changed QRhi::create() signature
* [QTBUG-139605](https://qt-project.atlassian.net/browse/QTBUG-139605) windows11style: crash when drawing slider due to failure
to check for null value
* [QTBUG-102020](https://qt-project.atlassian.net/browse/QTBUG-102020) Incorrect layout in QTabBar when last tab is hidden
* [QTBUG-139791](https://qt-project.atlassian.net/browse/QTBUG-139791) Buttons don't work when the last tab is hidden
* [QTBUG-139845](https://qt-project.atlassian.net/browse/QTBUG-139845) Reg->6.11: Assert when passing a too long-list to
QMetaMethodBuilder::setParameterNames()
* [QTBUG-138678](https://qt-project.atlassian.net/browse/QTBUG-138678) Crash in QTextEdit while inserting a column into a HTML
table
* [QTBUG-139425](https://qt-project.atlassian.net/browse/QTBUG-139425) Wayland: QEventLoop::ExcludeUserInputEvents doesn't work
* [PYSIDE-3173](https://qt-project.atlassian.net/browse/PYSIDE-3173) Emojis on Button Label Silently Crash PySide App
* [QTBUG-139291](https://qt-project.atlassian.net/browse/QTBUG-139291) showMaximized() does not maximize QDialog
* [QTBUG-139720](https://qt-project.atlassian.net/browse/QTBUG-139720) Tag errors in QtAbstractItemModel for Java
* [QTBUG-139688](https://qt-project.atlassian.net/browse/QTBUG-139688) Public Java Classes Documentation Bugs
* [QTBUG-134082](https://qt-project.atlassian.net/browse/QTBUG-134082) Screen orientation change causes rendering issues on Qt
Quick Application (flicker related)
* [QTBUG-139989](https://qt-project.atlassian.net/browse/QTBUG-139989) FAIL!  : tst_QStateMachine::twoAnimations() Compared
values are not the same
* [QTBUG-139944](https://qt-project.atlassian.net/browse/QTBUG-139944) macOS: title/text alignment on push buttons
* [QTBUG-135354](https://qt-project.atlassian.net/browse/QTBUG-135354) wayland\custom-extension and wayland\custom-shell
examples fails to build with Boot to Qt on Windows
* [QTBUG-139983](https://qt-project.atlassian.net/browse/QTBUG-139983) macOS (Tahoe): assert in
tst_QStyleSheetStyle::complexWidgetFocus()
* [QTBUG-139990](https://qt-project.atlassian.net/browse/QTBUG-139990) [REG 6.10.0 beta 3 -> beta 4] Building Qt examples for
WebAssembly fails
* [QTBUG-140064](https://qt-project.atlassian.net/browse/QTBUG-140064) error: array subscript 'QTransform[0]' is partly outside
array bounds of 'QVariant [1]'
* [QTBUG-140149](https://qt-project.atlassian.net/browse/QTBUG-140149) multimedia: unity builds broken on macos
* [QTBUG-140150](https://qt-project.atlassian.net/browse/QTBUG-140150) [cmake] qconfig.h and friends generated without
inclusion guards
* [QTBUG-140058](https://qt-project.atlassian.net/browse/QTBUG-140058) Tracepointgen doesn't generate metadata for enums
* [QTBUG-140172](https://qt-project.atlassian.net/browse/QTBUG-140172) [qtbase] Build failure in wayland plugin with -no-opengl
* [QTBUG-129735](https://qt-project.atlassian.net/browse/QTBUG-129735) Selenium tests flaky on CI
* [QTBUG-139617](https://qt-project.atlassian.net/browse/QTBUG-139617) Non-deterministic tst_QThread failures
* [QTBUG-140192](https://qt-project.atlassian.net/browse/QTBUG-140192) tst_qwidget (Failed) - tst_QWidget::resizeEvent()
Compared values are not the same
* [QTBUG-139765](https://qt-project.atlassian.net/browse/QTBUG-139765) QTEST_THROW_ON_FAIL doesn't work from inside
QtConcurrent
* [QTBUG-139040](https://qt-project.atlassian.net/browse/QTBUG-139040) Unreadable image on https://doc.qt.io/qt-6/animation-
overview.html
* [QTBUG-140126](https://qt-project.atlassian.net/browse/QTBUG-140126) QNetworkReply::errorString shows misleading "server
replied:" with no reason phrase for HTTP/2/3 responses
* [QTBUG-137927](https://qt-project.atlassian.net/browse/QTBUG-137927) Combining Qt::ExpandedClientAreaHint with
Qt::CustomizeWindowHint breaks mouse event handling
* [QTBUG-138659](https://qt-project.atlassian.net/browse/QTBUG-138659) QTextBoundaryFinder is copyable (deep-copies lookup
tables), but not movable
* [QTBUG-138596](https://qt-project.atlassian.net/browse/QTBUG-138596) App fails to build with qmake with static Qt + static
FFmpeg, wrong linker flags
* [QTBUG-140053](https://qt-project.atlassian.net/browse/QTBUG-140053) Suspect QLockFail::lock() may fail sporadically on
Windows
* [QTBUG-140203](https://qt-project.atlassian.net/browse/QTBUG-140203) [qtbase] Build failure with -no-ssl
* [QTBUG-139790](https://qt-project.atlassian.net/browse/QTBUG-139790) QFuture<T> cannot be passed to a method expecting
QFuture<void>
* [QTBUG-139690](https://qt-project.atlassian.net/browse/QTBUG-139690) SwipeView Android Expanded Client Area hides
NavigationBar
* [QTCREATORBUG-33525](https://qt-project.atlassian.net/browse/QTCREATORBUG-33525) Dockwidgets have app icons icons
* [QTBUG-139924](https://qt-project.atlassian.net/browse/QTBUG-139924) [REG Qt 6.9.2] Style Sheet is not always applied to
children
* [QTBUG-133332](https://qt-project.atlassian.net/browse/QTBUG-133332) possible stackoverflow calling setWindowFlag() in style
polish & unpolish
* [QTBUG-139653](https://qt-project.atlassian.net/browse/QTBUG-139653) Compile Error (GdiplusTypes.h(669): error C3861: 'max':
identifier not found)
* [QTBUG-138459](https://qt-project.atlassian.net/browse/QTBUG-138459) WindowStaysOnTopHint flag removes fullscreen on window
* [QTBUG-140509](https://qt-project.atlassian.net/browse/QTBUG-140509) Main ABI libs are littered by secondary ABI libs
* [QTBUG-136493](https://qt-project.atlassian.net/browse/QTBUG-136493) FFmpeg not properly configured with multi-abi builds
* [QTBUG-137248](https://qt-project.atlassian.net/browse/QTBUG-137248) color scheme issue on Android with expanded client area
* [QTBUG-124559](https://qt-project.atlassian.net/browse/QTBUG-124559) QWidgetPrivate::allWidgets contains stale artifact in
cleanup() slot of a test class
* [QTBUG-140516](https://qt-project.atlassian.net/browse/QTBUG-140516) qtbase/src/tools/bootstrap can't be built for Android
* [QTBUG-140643](https://qt-project.atlassian.net/browse/QTBUG-140643) QLocale::timeFormat(QLocale::NarrowFormat) returns
seconds for some locales
* [QTBUG-121879](https://qt-project.atlassian.net/browse/QTBUG-121879) QT_DEPLOY_QML_DIR example doesn't actually make use of
the value of QT_DEPLOY_QML_DIR
* [QTBUG-140649](https://qt-project.atlassian.net/browse/QTBUG-140649) Windows11Style: Fix QSlider layouting
* [QTBUG-140536](https://qt-project.atlassian.net/browse/QTBUG-140536) Android can't be built without EGL
* [QTBUG-136110](https://qt-project.atlassian.net/browse/QTBUG-136110) [Reg 6.8->6.9] Crash when opening popup (when creating
new C++ class) (Wayland protocol error)
* [QTBUG-139014](https://qt-project.atlassian.net/browse/QTBUG-139014) Odd update slowdowns on Windows with D3D and Quick
threaded render loop when continuously triggering window updates AND
starting it early
* [QTBUG-137219](https://qt-project.atlassian.net/browse/QTBUG-137219) Primitive restart does not work with D3D12
* [QTBUG-140784](https://qt-project.atlassian.net/browse/QTBUG-140784) /usr/include/c++/11/system_error:398
* [QTBUG-140443](https://qt-project.atlassian.net/browse/QTBUG-140443) tracepointgen:  Unable to find values for QEvent::Type
* [QTBUG-140207](https://qt-project.atlassian.net/browse/QTBUG-140207) Crash when rapidly moving a dock widget
* [QTBUG-140689](https://qt-project.atlassian.net/browse/QTBUG-140689) QToolBar Expansion Button Lacks Native Appearance on
macOS
* [QTBUG-139692](https://qt-project.atlassian.net/browse/QTBUG-139692) HTTP request results in NoError error on GOAWAY
* [QTBUG-140795](https://qt-project.atlassian.net/browse/QTBUG-140795) QRhi D3D11 backend bounds wrong buffers depending on
certain conditions
* [QTBUG-137936](https://qt-project.atlassian.net/browse/QTBUG-137936) Projects view displays files added by qt_add_resources()
in different subtrees
* [QTBUG-140694](https://qt-project.atlassian.net/browse/QTBUG-140694) Regression: Android: ImhNoPredictiveText on a text field
prevents text input completely
* [QTBUG-138858](https://qt-project.atlassian.net/browse/QTBUG-138858) Japanese input does not work well under landscape mode
on Android device
* [QTBUG-37980](https://qt-project.atlassian.net/browse/QTBUG-37980) Android: GET_EXTRACTED_TEXT_MONITOR flag not supported
* [QTBUG-138019](https://qt-project.atlassian.net/browse/QTBUG-138019) [Reg 6.7.3 -> 6.8.4][macOS][macos] Calqlatr: installed
example with qml modules doesn't launch due to code signing issues and
macdeployqt modifications
* [QTBUG-132285](https://qt-project.atlassian.net/browse/QTBUG-132285) [Windows] Flickering with high DPI scaling with native
Windows window
* [QTBUG-115992](https://qt-project.atlassian.net/browse/QTBUG-115992) Window containing native windows window is excessively
repainted on move
* [QTBUG-140847](https://qt-project.atlassian.net/browse/QTBUG-140847) Wayland: QMessageBox content clipped on COSMIC Desktop
* [QTBUG-138471](https://qt-project.atlassian.net/browse/QTBUG-138471) QString::arg() convert floating type to integer
* [QTBUG-131923](https://qt-project.atlassian.net/browse/QTBUG-131923) QPainter::drawImage with CompositionMode_Source into
non-alpha image format produces transparent pixels
* [QTBUG-140869](https://qt-project.atlassian.net/browse/QTBUG-140869) windows: use-after-free
* [QTBUG-140872](https://qt-project.atlassian.net/browse/QTBUG-140872) Diagram not readable in black mode
* [QTBUG-138807](https://qt-project.atlassian.net/browse/QTBUG-138807) [REG: 6.7 -> 6.8] win: QResource::registerResource
crashes if registering .rcc from inside the resource system
* [QTBUG-133410](https://qt-project.atlassian.net/browse/QTBUG-133410) Highlight faulty functionality of deprecated
QPrinter::PrinterResolution
* [QTBUG-139243](https://qt-project.atlassian.net/browse/QTBUG-139243) Font Substitution Causes Text Position Shift When
Drawing with QPicture in Qt
* [QTBUG-139610](https://qt-project.atlassian.net/browse/QTBUG-139610) Unwanted pixels are drawn during Japanese text rendering
* [QTBUG-138960](https://qt-project.atlassian.net/browse/QTBUG-138960) Fusion + stylesheet setting linear gradient as
background changes border color
* [QTBUG-139588](https://qt-project.atlassian.net/browse/QTBUG-139588) [REG: 5.10->5.11] SE_TabBarScrollLeft/RightButton have
no effect on stylesheet style anymore
* [QTBUG-138567](https://qt-project.atlassian.net/browse/QTBUG-138567) QUndoStack::redo() does not notify state change when
command becomes obsolete
* [QTBUG-140793](https://qt-project.atlassian.net/browse/QTBUG-140793) QToolButton::setPopupMode() has no effect if set before
setting the menu
* [QTBUG-140148](https://qt-project.atlassian.net/browse/QTBUG-140148) Windows11Style: adjust the QToolButton geometry
* [QTBUG-138419](https://qt-project.atlassian.net/browse/QTBUG-138419) [Reg 6.8.1->6.8.2] QMenu crash on QProcessEvent call
* [QTBUG-140132](https://qt-project.atlassian.net/browse/QTBUG-140132) Crash after deleting a popup menu in modal dialog event
processing
* [QTBUG-140856](https://qt-project.atlassian.net/browse/QTBUG-140856) Android software keyboard is not working in landscape
mode
* [QTBUG-139676](https://qt-project.atlassian.net/browse/QTBUG-139676) [a11y] "Switch" role is missing
* [QTBUG-135883](https://qt-project.atlassian.net/browse/QTBUG-135883) Submenus incorrectly bounded to main window on Wayland
* [QTBUG-99618](https://qt-project.atlassian.net/browse/QTBUG-99618) Expose XdgPositioner to QtBase
* [QTBUG-124810](https://qt-project.atlassian.net/browse/QTBUG-124810) nested menu is shown on top of its parent in wayland
* [QTBUG-72333](https://qt-project.atlassian.net/browse/QTBUG-72333) QAbstractItemView::isPersistentEditorOpen not checking
persistent editors
* [QTBUG-140929](https://qt-project.atlassian.net/browse/QTBUG-140929) QTextEdit/QTextDocument fail to render Emojis on
elements with id
* [QTBUG-138054](https://qt-project.atlassian.net/browse/QTBUG-138054) QProgressBar with text looks quite strange in Windows 11
style
* [QTBUG-140917](https://qt-project.atlassian.net/browse/QTBUG-140917) Update screenshot in "Document Layouts"
* [QTBUG-140923](https://qt-project.atlassian.net/browse/QTBUG-140923) Inaccurate QObject::startTimer documentation
* [QTBUG-141106](https://qt-project.atlassian.net/browse/QTBUG-141106) Wrong instructions on how to use GuiPrivate
* [QTBUG-135304](https://qt-project.atlassian.net/browse/QTBUG-135304) CMake CMP0177 on Android
* [QTBUG-130805](https://qt-project.atlassian.net/browse/QTBUG-130805) QTextFormat::FontSizeAdjustment documentation should
explain the value
* [QTBUG-141173](https://qt-project.atlassian.net/browse/QTBUG-141173) Wrong instructions on how to use CorePrivate
* [QTBUG-140134](https://qt-project.atlassian.net/browse/QTBUG-140134) Ugly spin boxes on macOS 26 (up/down buttons)
* [QTBUG-141181](https://qt-project.atlassian.net/browse/QTBUG-141181) What do with CMP0156 and CMake 4
* [QTBUG-135978](https://qt-project.atlassian.net/browse/QTBUG-135978) Adding -ObjC linking flag breaks iOS build
* [QTBUG-140211](https://qt-project.atlassian.net/browse/QTBUG-140211) WASM: libQt6Core.a is linked twice
* [QTBUG-141135](https://qt-project.atlassian.net/browse/QTBUG-141135) QMenu closes when clicking on a separator added by
addSeparator
* [QTBUG-140672](https://qt-project.atlassian.net/browse/QTBUG-140672) [VxWorks] 6.8.4 -> 6.8.5 build regression on Intel in
qfloat16.h
* [QTBUG-141061](https://qt-project.atlassian.net/browse/QTBUG-141061) TLS handshake fails for IDN hostnames (non-Punycode) on
Schannel backend
* [QTBUG-113028](https://qt-project.atlassian.net/browse/QTBUG-113028) QNetworkReply::RemoteHostClosedError error when using
Secure Channel library (configure option -schannel)
* [QTBUG-141128](https://qt-project.atlassian.net/browse/QTBUG-141128) FAIL!  :
tst_QQuickColorDialogImpl::dialogCanMoveBetweenWindows() Received a
fatal error
* [QTBUG-140830](https://qt-project.atlassian.net/browse/QTBUG-140830) Settings Qt.ExpandedClientAreaHint in onCompleted
handler has no effect
* [QTBUG-141100](https://qt-project.atlassian.net/browse/QTBUG-141100) WA_KeyboardFocusChange is not reset on focus change
through mouse
* [PYSIDE-3217](https://qt-project.atlassian.net/browse/PYSIDE-3217) Reg->6.10: C++ Enums in Python Qt Widgets designer
plugins no longer work
* [QTBUG-141255](https://qt-project.atlassian.net/browse/QTBUG-141255) Wrong conversion from ARGB with premultiplied alfa to
FP16
* [QTBUG-141074](https://qt-project.atlassian.net/browse/QTBUG-141074) C++23 [[assume]] added in 6.10.0 creates warnings when
compiling in C++20 mode with -Wextra -pedantic
* [QTBUG-141130](https://qt-project.atlassian.net/browse/QTBUG-141130) WASM: undefined QSemaphore method
* [QTBUG-138956](https://qt-project.atlassian.net/browse/QTBUG-138956) QMenu::activeAction() unexpectedly resets to nullptr
after setActiveAction()
* [QTBUG-139345](https://qt-project.atlassian.net/browse/QTBUG-139345) setWindowIcon(QIcon()) on QMdiSubWindow resets to the
default icon instead of removing the icon
* [QTBUG-140452](https://qt-project.atlassian.net/browse/QTBUG-140452) tst_json crashes under ASAN (MSVC) due to a stack
overflow
* [QTBUG-140449](https://qt-project.atlassian.net/browse/QTBUG-140449) disabled radio button that was checked but was set to
false while being disabled, still shows as checked until you hover your
mouse over it
* [QTBUG-141079](https://qt-project.atlassian.net/browse/QTBUG-141079) tst_QGraphicsProxyWidget::touchEventPropagation() does
not work with PM_DefaultFrameWidth > 1
* [QTBUG-141157](https://qt-project.atlassian.net/browse/QTBUG-141157) QStyleSheetStyle::drawComplexControl draws groove when
only Handle is asked for
* [QTBUG-141099](https://qt-project.atlassian.net/browse/QTBUG-141099) Regression in Qt 6.10: QWindow is placed at 0,0 by
default, frame is offscreen in Openbox
* [QTBUG-139964](https://qt-project.atlassian.net/browse/QTBUG-139964) Standard theme menu icons on macOS Tahoe do not match
Apple
* [QTBUG-141054](https://qt-project.atlassian.net/browse/QTBUG-141054) QML ScrollView with Text Inputs in WebAssembly shifts
after two left mouse clicks
* [QTBUG-134441](https://qt-project.atlassian.net/browse/QTBUG-134441) macOS: keyboard shortcut Meta+D results Ambiguous
shortcut
* [PYSIDE-3219](https://qt-project.atlassian.net/browse/PYSIDE-3219) QAbstractItemView.update shadows QWidget.update
* [QTBUG-140208](https://qt-project.atlassian.net/browse/QTBUG-140208) QAndroidApplication::context() doesn't have all methods
of QJniObject
* [QTBUG-141371](https://qt-project.atlassian.net/browse/QTBUG-141371) ::copy_file_range falsely(?) returns only
TriStateResult::Failed on failure
* [QTBUG-140145](https://qt-project.atlassian.net/browse/QTBUG-140145) Windows11Style: adjust the QPushButton geometry
* [QTBUG-139693](https://qt-project.atlassian.net/browse/QTBUG-139693) windows11 style: Checked menu items with icons look
strange
* [QTBUG-137203](https://qt-project.atlassian.net/browse/QTBUG-137203) Request to add an option for case sensitivity in
QNetworkRequest::setRawHeader().
* [QTBUG-135628](https://qt-project.atlassian.net/browse/QTBUG-135628) QCheckbox without text is right cropped
* [QTBUG-141433](https://qt-project.atlassian.net/browse/QTBUG-141433) QSaveFile has no std::filesystem::path support
* [QTBUG-140769](https://qt-project.atlassian.net/browse/QTBUG-140769) a11y: Scrollbar orientation not reported via AT-SPI (and
other a11y APIs)
* [QTBUG-139966](https://qt-project.atlassian.net/browse/QTBUG-139966) QScreen::refreshRateChanged signal is not fired when the
refresh rate changes
* [QTBUG-116886](https://qt-project.atlassian.net/browse/QTBUG-116886) Fix documentation for QDataStream::Version::6_6
* [QTBUG-141388](https://qt-project.atlassian.net/browse/QTBUG-141388) a11y: Freeze when querying QLineEdit word at offset
matching text length
* [QTBUG-139943](https://qt-project.atlassian.net/browse/QTBUG-139943) [iOS][Android] TextEdit or TextInput cannot be navigated
using A11y granularity
* [QTBUG-140467](https://qt-project.atlassian.net/browse/QTBUG-140467) a11y: Assert hit when using AT-SPI Text's
GetTextBeforeOffset in QLineEdit
* [QTBUG-140504](https://qt-project.atlassian.net/browse/QTBUG-140504) a11y: QAccessibleText::getTextAfterOffset implementation
for QTextEdit and QML TextEdit is incorrect
* [QTBUG-141499](https://qt-project.atlassian.net/browse/QTBUG-141499) windows11 style does not draw arrow for
QStyleOptionButton::HasMenu
* [QTBUG-134138](https://qt-project.atlassian.net/browse/QTBUG-134138) [A11y] ScreenReader reads QML StackView as "unknown" on
windows
* [QTBUG-141466](https://qt-project.atlassian.net/browse/QTBUG-141466) [FTBFS] include could not find requested file
"Qt6QmlToolsAdditionalTargetInfo.cmake"
* [QTBUG-140485](https://qt-project.atlassian.net/browse/QTBUG-140485) Missing documentation for QDate::startOfDay
* [QTBUG-139849](https://qt-project.atlassian.net/browse/QTBUG-139849) Windows11Style: Transparent combobox popups after
changing style from Windows11Style
* [QTBUG-141618](https://qt-project.atlassian.net/browse/QTBUG-141618) Windows 11 x64: MinGW build with GCC 15 fails in third
party error: 'decimal_point' may be used uninitialized
* [QTBUG-140789](https://qt-project.atlassian.net/browse/QTBUG-140789) Calqlatr: System Error
* [QTBUG-135038](https://qt-project.atlassian.net/browse/QTBUG-135038) QFileSystemModel is leaking nodes
* [QTBUG-141641](https://qt-project.atlassian.net/browse/QTBUG-141641) a11y: Missing labelled-by relations in QFileDialog
comboboxes
* [QTBUG-141187](https://qt-project.atlassian.net/browse/QTBUG-141187) Calling QTabBar::addTab/insertTab repeatedly is very
slow (O(N^2)) even if the parent QTabWidget is not visible
* [QTBUG-141666](https://qt-project.atlassian.net/browse/QTBUG-141666) a11y: Some QColorDialog widgets are not keyboard
accessible
* [QTBUG-141640](https://qt-project.atlassian.net/browse/QTBUG-141640) tst_QComboBox::virtualAutocompletion() is flaky since
2025-10-21
* [QTBUG-131115](https://qt-project.atlassian.net/browse/QTBUG-131115) [VxWorks] QTimezone is not enabled for VxWorks
* [QTBUG-141245](https://qt-project.atlassian.net/browse/QTBUG-141245) a11y: Orca screen reader often announces incorrect
QSpinBox value when changing it using arrow keys
* [QTBUG-132522](https://qt-project.atlassian.net/browse/QTBUG-132522) Window title bar shrinks to few pixel height if
WindowStaysOnTopHint is toggled.
* [QTBUG-141703](https://qt-project.atlassian.net/browse/QTBUG-141703) a11y: Lists in QFontDialog lack accessible names or
labelled-by relations
* [QTBUG-141745](https://qt-project.atlassian.net/browse/QTBUG-141745) tst_http2.cpp:732:32: error: incomplete type
'QSslConfiguration'
* [QTBUG-141475](https://qt-project.atlassian.net/browse/QTBUG-141475) Wayland: Warning spew related to QWaylandTextInputv3
under COSMIC
* [QTBUG-96165](https://qt-project.atlassian.net/browse/QTBUG-96165) OperationCanceledError instead of TimeoutError with
setTransferTimeout
* [QTBUG-141689](https://qt-project.atlassian.net/browse/QTBUG-141689) Qt6 on macOS Tahoe: Qt::WindowModal disables clicks on
QMessageBox
* [QTBUG-141644](https://qt-project.atlassian.net/browse/QTBUG-141644) a11y: Items in QFileDialog sidebar cannot be navigated
to using keyboard
* [QTBUG-141051](https://qt-project.atlassian.net/browse/QTBUG-141051) Item views report accessible name for any type of string
information except Description
* [QTBUG-140361](https://qt-project.atlassian.net/browse/QTBUG-140361) Standard theme menu icons on macOS Tahoe are too large
* [QTBUG-141819](https://qt-project.atlassian.net/browse/QTBUG-141819) [Reg 6.8.4->6.8.5] Setting background-color in the
StyleSheet causes the QTextEdit border not to render properly with the
Windows 11 style.
* [QTBUG-117832](https://qt-project.atlassian.net/browse/QTBUG-117832) Qt-6.5 + iOS + QFileDialog::getOpenFileUrl(), unable to
read file content
* [QTBUG-141553](https://qt-project.atlassian.net/browse/QTBUG-141553) Drop-down popups far from correct location
* [QTBUG-140073](https://qt-project.atlassian.net/browse/QTBUG-140073) Missing symbols in Java files in qtdeclarative
* [QTBUG-141366](https://qt-project.atlassian.net/browse/QTBUG-141366) Createbenchmark test crashed with a segmentation fault
* [QTBUG-140897](https://qt-project.atlassian.net/browse/QTBUG-140897) [REG:6.8->6.9.3,6.10.0] QML TextField on Android 16
doesn't show keyboard on first tap.
* [QTBUG-141571](https://qt-project.atlassian.net/browse/QTBUG-141571) a11y: Screen readers don't announce focused predefined
color in QColorDialog
* [QTBUG-141885](https://qt-project.atlassian.net/browse/QTBUG-141885) QRangeModel with tree of gadgets doesn't work
* [QTBUG-141994](https://qt-project.atlassian.net/browse/QTBUG-141994) Static build and disabling deprecated up to 6.6 results
in FTBS
* [QTBUG-124920](https://qt-project.atlassian.net/browse/QTBUG-124920) Menubar press-drag-release gesture doesn't activate menu
items on some compositors
* [QTBUG-141895](https://qt-project.atlassian.net/browse/QTBUG-141895) Sorting indicator with windows11 style wrong in position
and direction
* [QTBUG-126345](https://qt-project.atlassian.net/browse/QTBUG-126345) QHeaderView sorting indicator is missing with windows11
style and dark themes
* [QTBUG-141916](https://qt-project.atlassian.net/browse/QTBUG-141916) QSpinBox/QDoubleSpinBox does not factor in up/down
button size
* [QTBUG-142028](https://qt-project.atlassian.net/browse/QTBUG-142028) [regression] FTBFS: qnumeric.h overflow operations not
constexpr with C++26
* [QTBUG-141949](https://qt-project.atlassian.net/browse/QTBUG-141949) Update CLDR to v48
* [QTBUG-141918](https://qt-project.atlassian.net/browse/QTBUG-141918) QList asserts during assignment
* [QTBUG-109669](https://qt-project.atlassian.net/browse/QTBUG-109669) QStyleOptionMenuItem::Margin is not used by anything
* [QTBUG-105476](https://qt-project.atlassian.net/browse/QTBUG-105476) QColorDialog wrongly exposes pickable region when
translated
* [QTBUG-141730](https://qt-project.atlassian.net/browse/QTBUG-141730) Top flaky test:
tst_QRandomAccessAsyncFile::fileRemovedInProgress
* [QTBUG-141942](https://qt-project.atlassian.net/browse/QTBUG-141942) Crash in png lib
* [QTBUG-68947](https://qt-project.atlassian.net/browse/QTBUG-68947) QTreeView does not set QStyle::State_Editing
* [QTBUG-90897](https://qt-project.atlassian.net/browse/QTBUG-90897) Windows/Accessibility: Qt does not report correct focused
widget to screen readers on Windows
* [QTBUG-90899](https://qt-project.atlassian.net/browse/QTBUG-90899) Windows/Accessibility: NVDA sometimes reads out
information twice
* [QTBUG-142041](https://qt-project.atlassian.net/browse/QTBUG-142041) Starting a QProcess breaks std::cin (syscall not
restarted after SIGCHLD)
* [QTBUG-138513](https://qt-project.atlassian.net/browse/QTBUG-138513) QTableView setSpan + moveSection causes selection
mismatch
* [QTBUG-141899](https://qt-project.atlassian.net/browse/QTBUG-141899) QList::assign breaks basic exception guarantee
* [QTBUG-142092](https://qt-project.atlassian.net/browse/QTBUG-142092) emoji-segmenter dependency is missing from SBOM
* [QTBUG-135381](https://qt-project.atlassian.net/browse/QTBUG-135381) QFileDialog's name filter case sensitivity is not clear
* [QTBUG-142119](https://qt-project.atlassian.net/browse/QTBUG-142119) Can't use incomplete build of qtbase to build other Qt
repos anymore on macOS
* [QTBUG-142126](https://qt-project.atlassian.net/browse/QTBUG-142126) qt_generate_deploy_app_script deploys wrong architecture
in cross compile for WoA
* [QTBUG-141761](https://qt-project.atlassian.net/browse/QTBUG-141761) Crash when moving a dock of QDockWidget in and out of
the main window
* [QTBUG-138087](https://qt-project.atlassian.net/browse/QTBUG-138087) Qt wasm bug unexpected behaviour virtual keyboard
* [QTBUG-138821](https://qt-project.atlassian.net/browse/QTBUG-138821) Textfields properties not updates on editing at right
moment on mobile browser (Wasm)
* [QTBUG-142083](https://qt-project.atlassian.net/browse/QTBUG-142083) QPushButton icon windows 11 style
* [QTBUG-141833](https://qt-project.atlassian.net/browse/QTBUG-141833) QPainter::drawTiledPixmap() doesn't handle position
offset with HiDPI correctly
* [QTBUG-141912](https://qt-project.atlassian.net/browse/QTBUG-141912) QPicturePaintEngine crashes when its buffer runs full
* [QTBUG-141995](https://qt-project.atlassian.net/browse/QTBUG-141995) 16-bit PGM image data is truncated to 8-bits
* [QTBUG-138568](https://qt-project.atlassian.net/browse/QTBUG-138568) When <!-- %%INSERT_PERMISSIONS -> is removed it writes
nothing
* [QTBUG-93800](https://qt-project.atlassian.net/browse/QTBUG-93800) Add exception details to QJniObject
* [QTBUG-119791](https://qt-project.atlassian.net/browse/QTBUG-119791) Can no longer detect Java exceptions from C++ code with
Qt 6
* [QTBUG-142182](https://qt-project.atlassian.net/browse/QTBUG-142182) FTBFS: unqualified QRangeModelDetails::wrapped_t uses
break unity-build
* [QTBUG-142184](https://qt-project.atlassian.net/browse/QTBUG-142184) QRangeModel should not refer to its private
implemantation unqualified
* [QTBUG-142267](https://qt-project.atlassian.net/browse/QTBUG-142267) CMake configure fails if the target OS is already set to
TRUE
* [QTBUG-141938](https://qt-project.atlassian.net/browse/QTBUG-141938) Wayland: custom event loop doesn't work since Qt6.10
* [QTBUG-142345](https://qt-project.atlassian.net/browse/QTBUG-142345) QList crashes if underlying malloc() returns 0
* [QTBUG-142336](https://qt-project.atlassian.net/browse/QTBUG-142336) No qtpaths executable found for deployment purposes
* [QTBUG-142324](https://qt-project.atlassian.net/browse/QTBUG-142324) Using client certificate without common name causes
crash (schannel backend)
* [QTBUG-142139](https://qt-project.atlassian.net/browse/QTBUG-142139) Fusion style has incorrect QDockWidget icon filenames
* [QTBUG-142129](https://qt-project.atlassian.net/browse/QTBUG-142129) Windows11Style: Adjust QLineEdit coloring
* [QTBUG-140181](https://qt-project.atlassian.net/browse/QTBUG-140181) Build failure in QtDeclarative with latest nightly
libc++
* [QTBUG-142431](https://qt-project.atlassian.net/browse/QTBUG-142431) QVectorND QDataStream operators Q_ASSERT(qIsFinite())
instead of setting the stream state
* [QTBUG-140785](https://qt-project.atlassian.net/browse/QTBUG-140785) qt-cmake can't be used to run CMake `--build` or
`--install` modes, due to commandline injection of CMAKE_TOOLCHAIN_FILE
* [QTBUG-141856](https://qt-project.atlassian.net/browse/QTBUG-141856) Change of check state of list items is not announced by
screen readers
* [QTBUG-137435](https://qt-project.atlassian.net/browse/QTBUG-137435) macos: crash in Cocoa QPA when plugging in an external
screen
* [QTBUG-142400](https://qt-project.atlassian.net/browse/QTBUG-142400) QTreeWidget expand/collapse icons too small for windows
11 style
* [QTBUG-142512](https://qt-project.atlassian.net/browse/QTBUG-142512) WebAssembly - REG 6.10.x -> 6.11 - drag fails to move,
will only copy
* [QTBUG-141992](https://qt-project.atlassian.net/browse/QTBUG-141992) QMenu::exec returns Null for QWidgetAction , works for
QAction
* [QTBUG-142463](https://qt-project.atlassian.net/browse/QTBUG-142463) state checks in tst_qaccessibility fail in Clang build
on Debian testing
* [QTBUG-142246](https://qt-project.atlassian.net/browse/QTBUG-142246) [REG 6.6 - 6.7] QFont::op< is no longer a strict weak
ordering, breaking map preconditions
* [QTBUG-142528](https://qt-project.atlassian.net/browse/QTBUG-142528) macOS: 10bit OpenGL context cannot be created
* [QTBUG-141917](https://qt-project.atlassian.net/browse/QTBUG-141917) Severe Leak: User Handles ( Windows "_q_titlebar" won't
get closed )
* [QTBUG-142538](https://qt-project.atlassian.net/browse/QTBUG-142538) QWidget examples show "QRhiGles2: Failed to make context
current. Expect bad things to happen. Failed to create QRhi for
QBackingStoreRhiSupport" and nothing gets displayed on the screen
* [QTBUG-142232](https://qt-project.atlassian.net/browse/QTBUG-142232) q23::expected might break projects that use both Qt and
tl::expected
* [QTBUG-142552](https://qt-project.atlassian.net/browse/QTBUG-142552) CMake Error at tst_qquickaccessibleWrapperDebug.cmake
* [QTBUG-142089](https://qt-project.atlassian.net/browse/QTBUG-142089) Top flaky test:
tst_QRandomAccessAsyncFile::operationsDeletedInProgress
* [QTBUG-141579](https://qt-project.atlassian.net/browse/QTBUG-141579) android-9-x86-on-linux: Failed to acquire deadlock
protector for 'QAndroidPlatformOpenGLWindow::eglSurface()' while already
locked by 'QAndroidInputContext::runOnQtThread()'
* [QTBUG-141782](https://qt-project.atlassian.net/browse/QTBUG-141782) Top flaky test: tst_QColorDialog::hexColor
* [QTBUG-141357](https://qt-project.atlassian.net/browse/QTBUG-141357) Top flaky test:
tst_QCompleter::task253125_lineEditCompletion
* [QTBUG-142460](https://qt-project.atlassian.net/browse/QTBUG-142460) App crashes when switching to other application
* [QTBUG-141532](https://qt-project.atlassian.net/browse/QTBUG-141532) configure is looking for waylandscanner even if it is
not needed
* [QTBUG-131650](https://qt-project.atlassian.net/browse/QTBUG-131650) qtwebengine does not compile under sccache, with note
note: please rebuild precompiled header
* [QTBUG-140863](https://qt-project.atlassian.net/browse/QTBUG-140863) Instructions output by qt-cmake-create /
QtInitProject.cmake are wrong
* [QTBUG-64446](https://qt-project.atlassian.net/browse/QTBUG-64446) tst_QWidget::multipleToplevelFocusCheck() on linux
* [QTBUG-84259](https://qt-project.atlassian.net/browse/QTBUG-84259) tst_QWidget::multipleToplevelFocusCheck fails with CentOS
8.1 x64 & SLES 15
* [QTBUG-100686](https://qt-project.atlassian.net/browse/QTBUG-100686) macdeployqt misses some libraries
* [QTBUG-139635](https://qt-project.atlassian.net/browse/QTBUG-139635) Unexpected Result When QLCDNumber::display is Set to
INT_MIN
* [QTBUG-132882](https://qt-project.atlassian.net/browse/QTBUG-132882) StyleSheet in QHeaderView  Chops off first letter
* [QTBUG-142910](https://qt-project.atlassian.net/browse/QTBUG-142910) QSequentialIterable and QAssociativeIterable forwarding
headers are not installed
* [QTBUG-142434](https://qt-project.atlassian.net/browse/QTBUG-142434) QStyleOptionViewItem::viewItemPosition is incorrect
* [QTBUG-140494](https://qt-project.atlassian.net/browse/QTBUG-140494) QAbstractItemView with AStyledItemDelegate and
Windows11Style
* [QTBUG-132540](https://qt-project.atlassian.net/browse/QTBUG-132540) QMenu/QComboBox border-radius not properly rendered on
Windows
* [QTBUG-133116](https://qt-project.atlassian.net/browse/QTBUG-133116) Windows11Style: Menus look alien
* [QTBUG-141432](https://qt-project.atlassian.net/browse/QTBUG-141432) memory leak in QCoreApplication::requestPermissionImpl
* [QTBUG-133528](https://qt-project.atlassian.net/browse/QTBUG-133528) QLabel underline for accelerator doesn't update when Alt
is pressed
* [QTBUG-141803](https://qt-project.atlassian.net/browse/QTBUG-141803) Qt doesn't help debug "Unknown exception is thrown from
an Qt event handler"
* [QTBUG-45253](https://qt-project.atlassian.net/browse/QTBUG-45253) [REG 4.X->5.X] Default QPushButton with QMenu loses arrow
with Windows 7 style
* [QTBUG-88784](https://qt-project.atlassian.net/browse/QTBUG-88784) QFusionStyle does not support transparent buttons
* [QTBUG-
34103](https://qt-project.atlassian.net/browse/QTBUG-34103) QCommonStyle::subControlRect(CC_GroupBox,&option,QStyle::SC_GroupB
oxContents,...) gives wrong answer if option.rect.topLeft != (0,0)
* [QTBUG-134701](https://qt-project.atlassian.net/browse/QTBUG-134701) QTableWidget stylesheet stays on headers after removal
* [QTBUG-141637](https://qt-project.atlassian.net/browse/QTBUG-141637) Hash functions: unit test failures in repeated calls for
-0.0L and 0.0L
* [QTBUG-135333](https://qt-project.atlassian.net/browse/QTBUG-135333) Windows: Transparent frameless window has a frame with
titlebar
* [QTBUG-143122](https://qt-project.atlassian.net/browse/QTBUG-143122) Paragraph &lt;p&gt; is not indented in list item &lt;li&gt; when
-qt-list-indent is zero
* [QTBUG-143043](https://qt-project.atlassian.net/browse/QTBUG-143043) RightToLeft QCheckBox gets cropped with Win11 Style
* [QTBUG-143075](https://qt-project.atlassian.net/browse/QTBUG-143075) Tab's left/right (close button) widget didn't scroll
with tab in QTabbar if wheel event has PixelScroll capability
* [QTBUG-139212](https://qt-project.atlassian.net/browse/QTBUG-139212) New target form of qt6_wrap_cpp() doesn't work if given
header files
* [QTBUG-142121](https://qt-project.atlassian.net/browse/QTBUG-142121) Style Sheets: icon-size property does not scale
QPushButton Icon for :pressed pseudo-state
* [QTBUG-143059](https://qt-project.atlassian.net/browse/QTBUG-143059) qt_internal_find_apple_system_framework does not find
frameworks libraries
* [QTBUG-143060](https://qt-project.atlassian.net/browse/QTBUG-143060) Unable to find Qt...ToolsConfig.cmake although
QT_HOST_PATH_CMAKE_DIR and QT_HOST_PATH are set
* [QTBUG-141732](https://qt-project.atlassian.net/browse/QTBUG-141732) QLibraryInfo produces incorrect paths on Android.
* [QTBUG-70408](https://qt-project.atlassian.net/browse/QTBUG-70408) QPainter rotated by 180deg and drawing QPixmap on it,
picture comes out as not rotated when printing
* [QTBUG-143269](https://qt-project.atlassian.net/browse/QTBUG-143269) QStringView::operator std::u16string_view() not
constexpr
* [QTBUG-141769](https://qt-project.atlassian.net/browse/QTBUG-141769) openSUSE 16.0 qtbase -
tst_QRhi::renderToTextureArrayMultiView(OpenGL) 'ps->create()' returned
FALSE. ()
* [QTBUG-143183](https://qt-project.atlassian.net/browse/QTBUG-143183) Noto Color Emojies font is not handled correctly on
older Windows 10 (e.g. 1809, 1903, 2004, 21H2, 22H2...)
* [QTBUG-143174](https://qt-project.atlassian.net/browse/QTBUG-143174) [REG 6.8.3-6.10.1] Sporadic crashes on application exit
* [QTBUG-143352](https://qt-project.atlassian.net/browse/QTBUG-143352) [REG Qt 6.11.0 Beta 1] clang -  implicit conversion
changes signedness
* [QTBUG-112718](https://qt-project.atlassian.net/browse/QTBUG-112718) Q_INVOKABLE is not working with trailing return types,
QTBUG-93952 is still unresolved
* [QTBUG-143293](https://qt-project.atlassian.net/browse/QTBUG-143293) Random colors when drawing emojis with CBDT font +
assertion in debug
* [QTBUG-143336](https://qt-project.atlassian.net/browse/QTBUG-143336) [REG Qt 6.11.0 Beta 1] Missing Qt::WindowType::Desktop
* [QTBUG-142185](https://qt-project.atlassian.net/browse/QTBUG-142185) tst_qguieventdispatcher::postEventFromThread is flakey
on macOS 26
* [QTBUG-142664](https://qt-project.atlassian.net/browse/QTBUG-142664) macOS native drawing goes outside widget
* [QTBUG-143469](https://qt-project.atlassian.net/browse/QTBUG-143469) [REG 6.10.1] windows11 style on Windows 10 missing
interface icons
* [QTBUG-143405](https://qt-project.atlassian.net/browse/QTBUG-143405) [REG Qt 6.11.0 Beta 1] New CMake warning in
qtimageformats
* [QTBUG-143429](https://qt-project.atlassian.net/browse/QTBUG-143429) ninja clean fails
* [QTBUG-143294](https://qt-project.atlassian.net/browse/QTBUG-143294) WebAssembly: inputMethodHints not respected for mobile
virtual keyboard type
* [QTBUG-143119](https://qt-project.atlassian.net/browse/QTBUG-143119) QWidget handling QEvent::StyleChange during destruction
* [QTBUG-136485](https://qt-project.atlassian.net/browse/QTBUG-136485) QDockWidgets sends visibilityChanged on destruction
* [QTBUG-139218](https://qt-project.atlassian.net/browse/QTBUG-139218) Broken dependencies when qt6_wrap_cpp() is called in a
subdirectory
* [QTBUG-142822](https://qt-project.atlassian.net/browse/QTBUG-142822) [REG 6.9.1 -> 6.9.2] UnsatisfiedLinkError on Android:
dlopen failed: library "lib_arm64-v8a.so" not found
* [QTBUG-140674](https://qt-project.atlassian.net/browse/QTBUG-140674) Crash failing to create eglSurface while UI thread
locked by QtAndroidAccessibility
* [QTBUG-140501](https://qt-project.atlassian.net/browse/QTBUG-140501) QDialog is broken on Android platform
* [QTBUG-102594](https://qt-project.atlassian.net/browse/QTBUG-102594) [REG 5.15.6 -> 5.15.9] Many ANR issues by
QtAccessibility
* [QTBUG-105958](https://qt-project.atlassian.net/browse/QTBUG-105958) [Android] Intent + Talkback leads to deadlock
* [QTBUG-112931](https://qt-project.atlassian.net/browse/QTBUG-112931) Android App crash in QtAndroidAccessibility
* [QTBUG-143175](https://qt-project.atlassian.net/browse/QTBUG-143175) [REG] Extreme freezing since 6.9
* [QTBUG-143507](https://qt-project.atlassian.net/browse/QTBUG-143507) Qt 6.8 and higher won't build for x86_64 on macos
* [QTBUG-143587](https://qt-project.atlassian.net/browse/QTBUG-143587) Unexpected Vulkan validation errors in tst_qrhi autotest
* [QTBUG-142789](https://qt-project.atlassian.net/browse/QTBUG-142789) QFuture::result() crashes
* [QTBUG-143348](https://qt-project.atlassian.net/browse/QTBUG-143348) [REG Qt 6.11.0 Beta 1] Missing QFileSystemWatcher
* [QTBUG-143495](https://qt-project.atlassian.net/browse/QTBUG-143495) Segmentation fault in QEGLPlatformContext::hasExtension
* [QTBUG-142680](https://qt-project.atlassian.net/browse/QTBUG-142680) MERGE_QT_TRANSLATIONS results in duplicate qtdeclarative
lrelease arguments
* [QTBUG-141908](https://qt-project.atlassian.net/browse/QTBUG-141908) usage setOnApplyWindowInsetsListener kills QLineEdit
* [QTBUG-142020](https://qt-project.atlassian.net/browse/QTBUG-142020) Incorrect usage of qFuzzyCompare() abounds in Qt source
[QtCore]
* [QTBUG-143428](https://qt-project.atlassian.net/browse/QTBUG-143428) wasm: combobox on iOS does not unfocus
* [QTBUG-143452](https://qt-project.atlassian.net/browse/QTBUG-143452) Crash of TlsKeyOpenSSL::publicKeyFromX509 on Fedora
* [QTBUG-142938](https://qt-project.atlassian.net/browse/QTBUG-142938) Data Race in QProcessEnvironment
* [QTBUG-143739](https://qt-project.atlassian.net/browse/QTBUG-143739) tst_QWidget_window::tst_paintEventOnResize_QTBUG50796()
is very flaky on android-16-x86_64-on-linux
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
* [QTBUG-135817](https://qt-project.atlassian.net/browse/QTBUG-135817) [REG 6.7.2 -> Qt 6.8.2] Windows:
QFontDatabase::families() does not list stylistic variants of families
* [QTBUG-143710](https://qt-project.atlassian.net/browse/QTBUG-143710) Copy to clipboard removes newlines from text
* [QTBUG-143046](https://qt-project.atlassian.net/browse/QTBUG-143046) QTableWidget drop-and-drop indicator calculation is
always based on visualRect of the first column cell
* [QTBUG-143305](https://qt-project.atlassian.net/browse/QTBUG-143305) Wayland reconnect: QWaylandClientExtension will emit
activeChanged signal before event loop init.
* [QTBUG-143544](https://qt-project.atlassian.net/browse/QTBUG-143544) QDateTime editor shows local time while view shows UTC
* [QTBUG-140846](https://qt-project.atlassian.net/browse/QTBUG-140846) tst_Android::safeAreaWithWindowFlagsAndStates(Normal)
fails on Android 16
* [QTBUG-141712](https://qt-project.atlassian.net/browse/QTBUG-141712) tst_Android::testFullScreenDimensions() fails
* [QTBUG-143194](https://qt-project.atlassian.net/browse/QTBUG-143194) wasm: Drag does not work unless Drag.source is Window
* [QTBUG-143607](https://qt-project.atlassian.net/browse/QTBUG-143607) Suspicious behavior of QUrl::toAce /
QString::normalized(NFC)
* [QTBUG-143529](https://qt-project.atlassian.net/browse/QTBUG-143529) Qt Quick rendering (with D3D11 RHI) may cause NVidia GPU
device suspension
* [QTBUG-121987](https://qt-project.atlassian.net/browse/QTBUG-121987) Creating a new QMouseEvent can change globalPosition()
in other QMouseEvents
* [QTBUG-89486](https://qt-project.atlassian.net/browse/QTBUG-89486) Qt6 QMouseEvent invisibly overwrite last event global
position
* [QTBUG-143746](https://qt-project.atlassian.net/browse/QTBUG-143746) Specificity is lost with too many style rules
* [QTBUG-125197](https://qt-project.atlassian.net/browse/QTBUG-125197) QWidget multitouch sometimes drops touch points
* [QTBUG-67819](https://qt-project.atlassian.net/browse/QTBUG-67819) QGraphicsViewProxy does not propagate touch events to the
child of the widget
* [QTBUG-45737](https://qt-project.atlassian.net/browse/QTBUG-45737) No touch events handling (QGraphicsProxyWidget / QWidget)
* [QTBUG-144105](https://qt-project.atlassian.net/browse/QTBUG-144105) QtCorePrivate classes no longer displayed in Qt 6.11
* [QTBUG-144140](https://qt-project.atlassian.net/browse/QTBUG-144140) macdeployqt spends a lot of time updating install names
to the same value
* [QTBUG-144009](https://qt-project.atlassian.net/browse/QTBUG-144009) FAIL!  :
qmltestrunner::mouserelease::test_dragAxis(horizontal) Compared values
are not the same
* [QTBUG-142508](https://qt-project.atlassian.net/browse/QTBUG-142508) qmllint missing target dependencies when using Visual
Studio CMake generator
* [QTBUG-143440](https://qt-project.atlassian.net/browse/QTBUG-143440) testlib crashes when encountering unknown test function
passed on command line
* [QTBUG-143590](https://qt-project.atlassian.net/browse/QTBUG-143590) NoImplicitIncludes flag not working
* [QTBUG-138990](https://qt-project.atlassian.net/browse/QTBUG-138990) QToolButton action label trims "..." (periods) but not
"…" (ellipsis)
* [QTBUG-144142](https://qt-project.atlassian.net/browse/QTBUG-144142) copy_file_range may return ENOSYS inside some container
environments
* [QTBUG-142668](https://qt-project.atlassian.net/browse/QTBUG-142668) New example demos/android/feature-delivery configure
prints both 'FAILED' and 'BUILD SUCCESSFUL'
* [QTBUG-142029](https://qt-project.atlassian.net/browse/QTBUG-142029) QOpenGL crash with CGLFlushDrawable on Macos 26 (clang17
compiler)
* [QTBUG-136689](https://qt-project.atlassian.net/browse/QTBUG-136689) Crash in QImageData constructor due to a race condition
* [QTBUG-143699](https://qt-project.atlassian.net/browse/QTBUG-143699) Crash in QOpenGLFunctions::glClear in various Controls
auto tests
* [QTBUG-129099](https://qt-project.atlassian.net/browse/QTBUG-129099) tst_Q***AnimationGroup is flaky on webOS
* [QTBUG-125246](https://qt-project.atlassian.net/browse/QTBUG-125246) PNG with invalid colorSpace doesn't preserve ICC data
* [QTBUG-143478](https://qt-project.atlassian.net/browse/QTBUG-143478) QT_QPA_DEFAULT_PLATFORM=wayland leads to broken binaries
in static build
* [QTBUG-143781](https://qt-project.atlassian.net/browse/QTBUG-143781) Segmentation fault when model emits dataChanged() with
invalid index
* [QTBUG-142672](https://qt-project.atlassian.net/browse/QTBUG-142672) [REG 6.10.1->6.11.0] grpc/chat not configuring on
Android
* [QTBUG-141419](https://qt-project.atlassian.net/browse/QTBUG-141419) QNetworkAccessManager high CPU usage if outgoing packet
is rejected by nftables
* [QTBUG-139957](https://qt-project.atlassian.net/browse/QTBUG-139957) QPushButton menu arrow shifts position/size when border
is applied via stylesheet
* [QTBUG-135748](https://qt-project.atlassian.net/browse/QTBUG-135748) Mouse drag/gestures don't work on Android
* [QTBUG-138343](https://qt-project.atlassian.net/browse/QTBUG-138343) [Android][Mouse Input] Sliders and Dials Stop Responding
When Cursor Leaves Widget Bounds
* [QTBUG-143287](https://qt-project.atlassian.net/browse/QTBUG-143287) QNetworkInformation::loadBackendByFeatures crashes
sometimes
* [QTBUG-144288](https://qt-project.atlassian.net/browse/QTBUG-144288) QReadWriteLock gives thread sanitizer warning when used
with QReadLocker and QWriteLocker
* [QTBUG-144388](https://qt-project.atlassian.net/browse/QTBUG-144388) UB in QXcbVirtualDesktop
* [QTBUG-143204](https://qt-project.atlassian.net/browse/QTBUG-143204) Android GUI application crashes at the moment of
terminating
* [QTBUG-144444](https://qt-project.atlassian.net/browse/QTBUG-144444) Metal API validation: failed assertion `Depth Clip Mode
is not supported on this device' on iOS Simulator
* [QTBUG-144015](https://qt-project.atlassian.net/browse/QTBUG-144015) After attempting to change the color in the backlight
settings, the application crashes and produces a core dump.
* [QTBUG-144588](https://qt-project.atlassian.net/browse/QTBUG-144588) QRMA code snippet from blog post doesn't compile
* [QTBUG-144549](https://qt-project.atlassian.net/browse/QTBUG-144549) When using QGraphicsGridLayout on Wayland, grid is
misaligned when rendered through QPicture
* [QTBUG-137228](https://qt-project.atlassian.net/browse/QTBUG-137228) Cross-compiled ARM64 Windows binaries are not digitally
signed
* [QTBUG-122596](https://qt-project.atlassian.net/browse/QTBUG-122596) [REG 6.7.0->6.8.0] error in configure step, top level
build, MinGW
* [QTBUG-110758](https://qt-project.atlassian.net/browse/QTBUG-110758) Qt6/wayland QNativeInterface doesn't succeed in wrapping
existing EGL context
* [QTBUG-134921](https://qt-project.atlassian.net/browse/QTBUG-134921) Comparision of QVariantList and QProperty<QVariantList>
not working
* [QTBUG-119110](https://qt-project.atlassian.net/browse/QTBUG-119110) There are potential crash issues when some submenus are
expanded.
* [QTBUG-122642](https://qt-project.atlassian.net/browse/QTBUG-122642) The SQL QODBC driver implementation fails to escape
passwords set with setPassword(...) when using special characters.
* [QTBUG-55421](https://qt-project.atlassian.net/browse/QTBUG-55421) broken links to QBasicAtomic* in published docs
* [QTBUG-112355](https://qt-project.atlassian.net/browse/QTBUG-112355) ShaderEffectSource with recursive shader causes magenta
texture on Apple Silicon
* [QTBUG-132775](https://qt-project.atlassian.net/browse/QTBUG-132775) QSortFilterProxyModel fails to receive beginResetModel
* [QTBUG-120138](https://qt-project.atlassian.net/browse/QTBUG-120138) Showing a child Window more than once fails on
WebAssembly
* [QTBUG-134105](https://qt-project.atlassian.net/browse/QTBUG-134105) tst_qscroller::overshoot() is flaky on macOS
* [QTBUG-132435](https://qt-project.atlassian.net/browse/QTBUG-132435) QKeySequence doesn't encode and decode modifier only
shortcuts as expected
* [QTBUG-134208](https://qt-project.atlassian.net/browse/QTBUG-134208) Mnemonic annotation is passed to screen readers
* [QTBUG-137885](https://qt-project.atlassian.net/browse/QTBUG-137885) QPainter::brushOrigin() returns a QPoint instead QPointF
* [QTBUG-137942](https://qt-project.atlassian.net/browse/QTBUG-137942) test result file
tst_qmltc_examples-1750626901804.junit.xml is empty
* [COIN-1247](https://qt-project.atlassian.net/browse/COIN-1247) Build fails on dependency to qtattributionsscanner: not
found
* [QTBUG-137566](https://qt-project.atlassian.net/browse/QTBUG-137566) Make snippets in qtbase compilable and add to the build
system
* [QTBUG-137562](https://qt-project.atlassian.net/browse/QTBUG-137562) tst_qxmlstream timeout
* [QTBUG-135626](https://qt-project.atlassian.net/browse/QTBUG-135626) QPointer causes unneccessary (invalid) downcasts
* [QTCREATORBUG-32932](https://qt-project.atlassian.net/browse/QTCREATORBUG-32932) Automatic selection of too low Android SDK version
* [QTBUG-138155](https://qt-project.atlassian.net/browse/QTBUG-138155) qt_generate_deploy_qml_app_script: Error for space in
output name
* [QTBUG-98846](https://qt-project.atlassian.net/browse/QTBUG-98846) QMetaProperty: QMetaProperty::isRequired() does't work
* [QTBUG-115078](https://qt-project.atlassian.net/browse/QTBUG-115078) icx requires -mcx16 flag to compile
_InterlockedCompareExchange128 on windows
* [QTBUG-138246](https://qt-project.atlassian.net/browse/QTBUG-138246) Q{Shared,Weak}Pointer::IfCompatible cause accidental
copy/move SMFs, causing FTBFS in qtdeclarative
* [QTBUG-137130](https://qt-project.atlassian.net/browse/QTBUG-137130) Qt Creator crash on exit accessing destroyed event
dispatcher
* [QTBUG-137126](https://qt-project.atlassian.net/browse/QTBUG-137126) QAccessible::ActionChanged event not sent anywhere in Qt
* [QTBUG-138192](https://qt-project.atlassian.net/browse/QTBUG-138192) Android Templates, Manifest and CMake Properties
* [QTBUG-94777](https://qt-project.atlassian.net/browse/QTBUG-94777) running android unit tests requires about 3GB of disk
space per test
* [QTBUG-135413](https://qt-project.atlassian.net/browse/QTBUG-135413) Accessible.announce not working on iOS and Android
* [QTBUG-138562](https://qt-project.atlassian.net/browse/QTBUG-138562) QLocalePrivate::codeToLanguage() does not sanitize the
input before passing it to AlphaCode
* [QTBUG-138610](https://qt-project.atlassian.net/browse/QTBUG-138610) QTemporaryFile::rename() overwrites existing file on
Android
* [QTBUG-126659](https://qt-project.atlassian.net/browse/QTBUG-126659) New QMap.qHash leading to ambiguous calls
* [QTBUG-137564](https://qt-project.atlassian.net/browse/QTBUG-137564) tst_qmovie fails
* [QTBUG-138583](https://qt-project.atlassian.net/browse/QTBUG-138583) QLocale::toUpper() is not 64-bit-safe on ICU
* [QTBUG-135138](https://qt-project.atlassian.net/browse/QTBUG-135138) Investigate memory leaks on widget tests
* [QTBUG-2163](https://qt-project.atlassian.net/browse/QTBUG-2163) Support for conditions in special casing of unicode
characters is missing in Qt
* [QTBUG-138705](https://qt-project.atlassian.net/browse/QTBUG-138705) Windows backend of QLocale::toLower() does not implement
Greek Final Sigma rule
* [QTBUG-138527](https://qt-project.atlassian.net/browse/QTBUG-138527) Replace direct links to https://doc.qt.io/qt-6/
* [QTBUG-137933](https://qt-project.atlassian.net/browse/QTBUG-137933) stale-property-read for flags
* [QTBUG-107907](https://qt-project.atlassian.net/browse/QTBUG-107907) QOperatingSystemVersion::Windows10 <
QOperatingSystemVersion::Windows11 == false
* [QTBUG-136045](https://qt-project.atlassian.net/browse/QTBUG-136045) macOS: Window geometry is not updated correctly when the
OS rejects a change by setGeometry
* [QTBUG-138750](https://qt-project.atlassian.net/browse/QTBUG-138750) When compiling on windows, compile looks for `unistd.h`
* [QTBUG-132398](https://qt-project.atlassian.net/browse/QTBUG-132398) Unsupported linker script to make objective-c classnames
unique is broken since Xcode14
* [QTBUG-138823](https://qt-project.atlassian.net/browse/QTBUG-138823) Invalid JSON generated for *-deployment-settings.json
file
* [QTBUG-138829](https://qt-project.atlassian.net/browse/QTBUG-138829) Fix uses of deprecated
NSWindowStyleMaskTexturedBackground
* [QTBUG-37759](https://qt-project.atlassian.net/browse/QTBUG-37759) QWidget-gestures do not work
* [QTBUG-46195](https://qt-project.atlassian.net/browse/QTBUG-46195) [Windows]: Swipe gesture is not always recognized and
sometimes in the wrong direction
* [QTBUG-134546](https://qt-project.atlassian.net/browse/QTBUG-134546) [VxWorks] exit on poll error should be on by default
like in 5.15
* [QTBUG-138831](https://qt-project.atlassian.net/browse/QTBUG-138831) [VxWorks] EDOOM handling is missing from 6.x
* [QTBUG-138851](https://qt-project.atlassian.net/browse/QTBUG-138851) Quadratic behaviour in qlocale.cpp when building
uiLanguages
* [QTBUG-137860](https://qt-project.atlassian.net/browse/QTBUG-137860) [Windows][A11y] Text can not be selected by NVDA
* [QTBUG-138878](https://qt-project.atlassian.net/browse/QTBUG-138878) QNetworkRequestFactory creates an incorrect network
request
* [QTBUG-138706](https://qt-project.atlassian.net/browse/QTBUG-138706) [Wayland] Application freeze when mouse is doing UI-
blocking operations
* [QTBUG-138901](https://qt-project.atlassian.net/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-138403](https://qt-project.atlassian.net/browse/QTBUG-138403) QDirIterator → QDirListing should have some porting
documentation
* [QTBUG-136653](https://qt-project.atlassian.net/browse/QTBUG-136653) tst_QAbstractItemView::testDialogAsEditor() crash on
Ubuntu 24.04 x11
* [QTBUG-132211](https://qt-project.atlassian.net/browse/QTBUG-132211) [REG 6.7 -> 6.8][Android] UnsatisfiedLinkError onResume
and onNewIntent
* [QTBUG-120467](https://qt-project.atlassian.net/browse/QTBUG-120467) Link error from Google Play testing
* [QTBUG-70114](https://qt-project.atlassian.net/browse/QTBUG-70114) Java native functions registered with a delay
* [QTBUG-86314](https://qt-project.atlassian.net/browse/QTBUG-86314) Error in 64bit lib file path names
* [QTBUG-134093](https://qt-project.atlassian.net/browse/QTBUG-134093) Android application crashes on 16 KB page size
* [QTBUG-139055](https://qt-project.atlassian.net/browse/QTBUG-139055) CMake Error at tst_qstatemachineWrapperDebug
* [QTBUG-136076](https://qt-project.atlassian.net/browse/QTBUG-136076) QStringConverterBase points to qstringconverter.h, not
qstringconverter_base.h
* [QTBUG-138882](https://qt-project.atlassian.net/browse/QTBUG-138882) [Wayland] QWaylandShmBackingStore::scroll() is scrolling
the busy buffer
* [QTBUG-132108](https://qt-project.atlassian.net/browse/QTBUG-132108) addApplicationFontFromData behaves abnormally after
removeAllApplicationFonts.
* [QTBUG-139139](https://qt-project.atlassian.net/browse/QTBUG-139139) ubuntu-24.04-x64-developer-build: Part of the build is
using qmake and ignores SCCACHE settings
* [QTBUG-21468](https://qt-project.atlassian.net/browse/QTBUG-21468) tst_qstylesheetstyle is broken
* [QTCREATORBUG-33334](https://qt-project.atlassian.net/browse/QTCREATORBUG-33334) UI glitch with scrolling
* [QTBUG-138249](https://qt-project.atlassian.net/browse/QTBUG-138249) Win11 23h2 ARM: QtBase -
tst_QRhiWidget::grabFramebufferWhileStillInvisible fails
* [QTBUG-138252](https://qt-project.atlassian.net/browse/QTBUG-138252) Win11 23h2 ARM: QtBase -
tst_QRhiWidget::grabFramebufferWhileStillInvisible fails with cross-
compilation target
* [QTBUG-139283](https://qt-project.atlassian.net/browse/QTBUG-139283) QInputDevice::availableVirtualGeometry property
incomplete
* [QTBUG-139275](https://qt-project.atlassian.net/browse/QTBUG-139275) [a11y] Changes to Accessible.name for focused element
not announced to Screen Reader
* [QTBUG-138883](https://qt-project.atlassian.net/browse/QTBUG-138883) [Wayland] Missing enter event when modal windows is
closed and cursor is over parent window
* [QTBUG-138806](https://qt-project.atlassian.net/browse/QTBUG-138806) [VxWorks] Flickable doesn't work on VxWorks
* [QTBUG-107028](https://qt-project.atlassian.net/browse/QTBUG-107028) tst_qquicktextfield and tst_qquicktextarea fail on
Android
* [QTBUG-100259](https://qt-project.atlassian.net/browse/QTBUG-100259) tst_controls crash on Android
* [QTBUG-100258](https://qt-project.atlassian.net/browse/QTBUG-100258) tst_focus crashes on Android
* [QTBUG-139415](https://qt-project.atlassian.net/browse/QTBUG-139415) tst_controls has failing test cases
* [QTBUG-139405](https://qt-project.atlassian.net/browse/QTBUG-139405) QMatrix4x4 has an internal Flag enum that QDoc exposes
as flags
* [QTBUG-138699](https://qt-project.atlassian.net/browse/QTBUG-138699) Square push buttons (macOS 26)
* [QTBUG-133086](https://qt-project.atlassian.net/browse/QTBUG-133086) Doc: Improve Networking and WebEngine security topics
* [QTBUG-139606](https://qt-project.atlassian.net/browse/QTBUG-139606) [regression] App window blank when switching from
background to foreground
* [QTBUG-139659](https://qt-project.atlassian.net/browse/QTBUG-139659) Activity can stop reacting to touch events
* [QTBUG-138738](https://qt-project.atlassian.net/browse/QTBUG-138738) Incorrect focus ring rendering
* [QTBUG-138700](https://qt-project.atlassian.net/browse/QTBUG-138700) Tabs have wrong shape on macOS 26
* [QTBUG-138948](https://qt-project.atlassian.net/browse/QTBUG-138948) Radio button alignment issues on macOS 26
* [QTBUG-139950](https://qt-project.atlassian.net/browse/QTBUG-139950) tst_QGraphicsProxyWidget::windowOpacity is flaky and/or
failing on macOS
* [QTBUG-138893](https://qt-project.atlassian.net/browse/QTBUG-138893) QTimeZone(Qt::UTC) returns incorrect UTC offset (+1
second)
* [QTBUG-139986](https://qt-project.atlassian.net/browse/QTBUG-139986) QStateMachine tests aren't running on the CI
* [QTBUG-139951](https://qt-project.atlassian.net/browse/QTBUG-139951) [VxWorks] 6.8.4 -> 6.8.5 regression build failure with
VxWorks 24.03
* [QTBUG-139280](https://qt-project.atlassian.net/browse/QTBUG-139280) Cannot build QT 6.8 without GNU extensions
* [QTBUG-117447](https://qt-project.atlassian.net/browse/QTBUG-117447) Remove *-proxy.html pages in Qt Core
* [QTBUG-140038](https://qt-project.atlassian.net/browse/QTBUG-140038) tst_QGridLayout::spacingsAndMargins fails on Android 15
* [QTBUG-139565](https://qt-project.atlassian.net/browse/QTBUG-139565) Incorrect gl_InstanceIndex on D3D11 and D3D12
* [QTBUG-140133](https://qt-project.atlassian.net/browse/QTBUG-140133) tst_QGraphicsProxyWidget::createProxyForChildWidget
fails with non-zero safe area margins
* [QTBUG-140048](https://qt-project.atlassian.net/browse/QTBUG-140048) Tracepointgen doesn't seem  to support enum class
* [QTBUG-139007](https://qt-project.atlassian.net/browse/QTBUG-139007) QFileSystemEngine::fillMetaData fails on hostfs
* [QTBUG-139994](https://qt-project.atlassian.net/browse/QTBUG-139994) Nullptr swapchain dereference in
QBackingStoreDefaultCompositor::flush
* [QTBUG-140096](https://qt-project.atlassian.net/browse/QTBUG-140096) QDoc: \page command with file extensions other than
.html results in double extensions
* [QTBUG-66621](https://qt-project.atlassian.net/browse/QTBUG-66621) webassembly: strings with toUpper() not correct
* [QTBUG-69421](https://qt-project.atlassian.net/browse/QTBUG-69421) WebAssembly: characters are not displayed properly
* [QTBUG-74511](https://qt-project.atlassian.net/browse/QTBUG-74511) Possible REG: Wasm changes in qunicodetables will be lost
* [QTBUG-140413](https://qt-project.atlassian.net/browse/QTBUG-140413) heap-use-after-free when using a QSslCertificate in a
static QCoreApplication
* [QTBUG-140388](https://qt-project.atlassian.net/browse/QTBUG-140388) tst_QWindow::stateChangeSignal() is broken
* [QTBUG-139307](https://qt-project.atlassian.net/browse/QTBUG-139307) [REG 5.15.19->6.0.3] Windows: Widgets flicker/jitter
when hovering over them in 150% DPI scaling with 'windowsvista' style
* [QTIFW-3852](https://qt-project.atlassian.net/browse/QTIFW-3852) Banner Not Stretching When Using Installer Framework to
Create Custom Installer
* [QTBUG-140189](https://qt-project.atlassian.net/browse/QTBUG-140189) 347 - tst_qrhi (Failed)
* [QTBUG-137048](https://qt-project.atlassian.net/browse/QTBUG-137048) qdoc: Warn about self-link in \sa
* [QTBUG-29917](https://qt-project.atlassian.net/browse/QTBUG-29917) QDBusReply::error() should be const
* [QTBUG-140627](https://qt-project.atlassian.net/browse/QTBUG-140627) 499 - tst_qrhiwidget (Failed)
* [QTBUG-100377](https://qt-project.atlassian.net/browse/QTBUG-100377) [REG 5.15 -> 6.2] Date.parse() can't handle some dates
on Qt 6 but works in Qt 5
* [QTBUG-130278](https://qt-project.atlassian.net/browse/QTBUG-130278) [Reg 6.7.2 -> 6.8.0][macOS] QLocale::LongFormat no
longer produces reversible conversion between QDateTime and QString
* [QTBUG-130480](https://qt-project.atlassian.net/browse/QTBUG-130480) Windows 11 Style does not change the palette before
QEvent::PaletteChange
* [QTBUG-117904](https://qt-project.atlassian.net/browse/QTBUG-117904) QProgressBar High-DPI issues
* [QTBUG-120749](https://qt-project.atlassian.net/browse/QTBUG-120749) macOS: Mouse Up is not delivered correctly after drag
and drop
* [QTBUG-138381](https://qt-project.atlassian.net/browse/QTBUG-138381) Putting QTableWidget in a QGraphicsScene breaks
positioning of all widgets in cells
* [QTBUG-139697](https://qt-project.atlassian.net/browse/QTBUG-139697) Provide a public "bind" API for QCoapClient, or at least
filter out unexpected replies not from peer
* [QTBUG-139560](https://qt-project.atlassian.net/browse/QTBUG-139560) Access functions are documented even when their
properties are not
* [QTBUG-140738](https://qt-project.atlassian.net/browse/QTBUG-140738) Crash with cachegen compiled code
* [QTBUG-140725](https://qt-project.atlassian.net/browse/QTBUG-140725) QWinRegistryKey inconsistent handling of data members in
swap()/move-SMFs
* [QTBUG-139120](https://qt-project.atlassian.net/browse/QTBUG-139120) QSvgGenerator generates a different svg depending on the
Windows Display Scale Factor
* [QTBUG-141152](https://qt-project.atlassian.net/browse/QTBUG-141152) CMake: Update snippets for how to use private Qt API
* [QTBUG-136976](https://qt-project.atlassian.net/browse/QTBUG-136976) QHoverEvent::HoverMove Triggered Repeatedly on
Stationary Mouse When Unrelated QQuickItem Changes
* [QTBUG-141386](https://qt-project.atlassian.net/browse/QTBUG-141386) tst_QGraphicsProxyWidget::clickFocus fails on Windows 10
* [QTBUG-110696](https://qt-project.atlassian.net/browse/QTBUG-110696) Qt6CoreMacros.cmake should take AUTOGEN_BUILD_DIR into
account
* [QTBUG-140507](https://qt-project.atlassian.net/browse/QTBUG-140507) Incorrect palette colors when enabling a contrast theme
while a hybrid widgets + quick application is running.
* [QTBUG-141387](https://qt-project.atlassian.net/browse/QTBUG-141387) QGuiApplication should update lastCursorPosition on both
Enter and Leave events
* [QTBUG-141427](https://qt-project.atlassian.net/browse/QTBUG-141427) FAIL!  :
tst_controls::*::SwipeDelegate::test_removableDelegates(touch) Compared
values are not the same
* [QTBUG-140688](https://qt-project.atlassian.net/browse/QTBUG-140688) Standard icons from widgets/images don't have a dark
counterpart
* [QTBUG-115101](https://qt-project.atlassian.net/browse/QTBUG-115101) WaylandGlobalPrivate_sync_headers is not running if
nothing depends on WaylandGlobalPrivate
* [QTBUG-139336](https://qt-project.atlassian.net/browse/QTBUG-139336) Moving app window between to different DPR screens can
result in poor scaling
* [QTBUG-135418](https://qt-project.atlassian.net/browse/QTBUG-135418) REG->6.9.0: Windows 11 Style: Selection in Qt Designer
looks weird
* [QTBUG-122624](https://qt-project.atlassian.net/browse/QTBUG-122624) REG: QDirIterator unicode handling broke in Qt 6.8
* [QTBUG-141663](https://qt-project.atlassian.net/browse/QTBUG-141663) Missing option to force VSync on VxWorks target
* [QTBUG-69423](https://qt-project.atlassian.net/browse/QTBUG-69423) QRandomGenerator not random on certain Windows
installations
* [QTBUG-129193](https://qt-project.atlassian.net/browse/QTBUG-129193) Qt compiled with gcc 13 and -march=bdver4/-mtune=bdver4
causes segfaults in tests, downstream applications
* [QTBUG-131107](https://qt-project.atlassian.net/browse/QTBUG-131107) QVideoFrame::toImage / qImageFromVideoFrame not safe to
call from worker thread
* [QTBUG-141834](https://qt-project.atlassian.net/browse/QTBUG-141834) QNX: windows/widgets not scaled correctly when scale
factor is larger than 1
* [QTBUG-138455](https://qt-project.atlassian.net/browse/QTBUG-138455) Integer division by zero in QFontCache::decreaseCache()
* [QTBUG-141665](https://qt-project.atlassian.net/browse/QTBUG-141665) Doc: Suppress "No output generated for ..."
* [QTBUG-141412](https://qt-project.atlassian.net/browse/QTBUG-141412) QFont::toString() doesn't include font features and
variable axes
* [QTBUG-138759](https://qt-project.atlassian.net/browse/QTBUG-138759) [VxWorks] some vxworks socket errorhandling is missing
from 6.x
* [QTBUG-142157](https://qt-project.atlassian.net/browse/QTBUG-142157) QCursor::pos() doesn't match enter event position
* [QTBUG-135049](https://qt-project.atlassian.net/browse/QTBUG-135049)  Connection error: GOAWAY invalid stream/error code (1)
* [QTBUG-140667](https://qt-project.atlassian.net/browse/QTBUG-140667) Undocumented reimplemented public functions in snapshot
builds
* [QTBUG-140786](https://qt-project.atlassian.net/browse/QTBUG-140786) QFuture::cancelChain doesn't set the cancel info to all
chained futures/promises
* [QTBUG-120396](https://qt-project.atlassian.net/browse/QTBUG-120396) `QUrl::resolved` gives wrong result when there are more
`..`s in relative reference
* [QTBUG-142186](https://qt-project.atlassian.net/browse/QTBUG-142186) MetaObject change in DelegateModel leads to crash in
Plasma
* [QTBUG-93625](https://qt-project.atlassian.net/browse/QTBUG-93625) qt_internal_add_test doesn't call qt_import_qml_plugins
* [QTBUG-142473](https://qt-project.atlassian.net/browse/QTBUG-142473) Linear memory growth observed with Qt GRPC during long
run
* [QTBUG-142713](https://qt-project.atlassian.net/browse/QTBUG-142713) SPDX Sbom document namespaces are not unique enough
* [QTBUG-141505](https://qt-project.atlassian.net/browse/QTBUG-141505) AOSP-based Android back gesture causes touch loss in Qt
for WebAssembly apps
* [QTBUG-142551](https://qt-project.atlassian.net/browse/QTBUG-142551) Crash in QRegularExpressionPrivate::optimizePattern()
* [QTBUG-143208](https://qt-project.atlassian.net/browse/QTBUG-143208) Fix QTestAccessibility various problems
* [QTBUG-142915](https://qt-project.atlassian.net/browse/QTBUG-142915) crash because of wayland error "unknown object xxx,
message error(ous)"
* [QTBUG-137401](https://qt-project.atlassian.net/browse/QTBUG-137401) QScrollBar attached to QScrollArea visibility is not
updated correctly
* [QTCREATORBUG-33984](https://qt-project.atlassian.net/browse/QTCREATORBUG-33984) [cmake] custom target shows multiple identical
folders
* [QTBUG-142088](https://qt-project.atlassian.net/browse/QTBUG-142088) Doc: Clean \externalpage declarations
* [QTBUG-141773](https://qt-project.atlassian.net/browse/QTBUG-141773) openSUSE 16.0 qtbase - tst_seatv4::animatedCursor()
'!cursorSurface()->m_waitingFrameCallbacks.empty()' returned FALSE. ()
* [QTBUG-138601](https://qt-project.atlassian.net/browse/QTBUG-138601) Swipe gesture does not work on Windows
* [QTBUG-14895](https://qt-project.atlassian.net/browse/QTBUG-14895) Qt Gestures - Pan and Swipe are not working
* [QTBUG-141785](https://qt-project.atlassian.net/browse/QTBUG-141785) qtwebengine builds on windows don't /mostly/ use sccache
* [QTBUG-101426](https://qt-project.atlassian.net/browse/QTBUG-101426) QMetaObjectBuilder does not properly carry property
flags
* [QTBUG-143800](https://qt-project.atlassian.net/browse/QTBUG-143800) source value 8 is obsolete and will be removed in a
future release
* [QTBUG-143916](https://qt-project.atlassian.net/browse/QTBUG-143916) Fix QDoc warnings for Qt 6.11
* [QTBUG-143861](https://qt-project.atlassian.net/browse/QTBUG-143861) HTTP/2: Ensure that SETTINGS_MAX_FRAME_SIZE is respected
* [QTBUG-96239](https://qt-project.atlassian.net/browse/QTBUG-96239) Document CMake component in CMake function documentation
* [QTBUG-141701](https://qt-project.atlassian.net/browse/QTBUG-141701) [a11y] App language is not transparent to Screen Reader
* [QTBUG-143608](https://qt-project.atlassian.net/browse/QTBUG-143608) QTableView/QTableWidget: scrolling issues when moving a
row/column header section outside the viewport
* [QTBUG-144206](https://qt-project.atlassian.net/browse/QTBUG-144206) Qt Designer: Item widgets' items lack fully-qualified
enums
* [PYSIDE-2492](https://qt-project.atlassian.net/browse/PYSIDE-2492) uic does not generate enumeration name into enum values
causing type checking warnings
* [PYSIDE-3278](https://qt-project.atlassian.net/browse/PYSIDE-3278) pyside6-uic: Item widgets' items have enum setters that
are inconsistent with those of other classes

### qtsvg
* [QTBUG-139120](https://qt-project.atlassian.net/browse/QTBUG-139120) QSvgGenerator generates a different svg depending on the
Windows Display Scale Factor
* [QTBUG-142775](https://qt-project.atlassian.net/browse/QTBUG-142775) qtsvg/src/svg/qsvghandler_p.h:41:36: error:
‘QtSvg::Options’ has not been declared
* [QTBUG-142727](https://qt-project.atlassian.net/browse/QTBUG-142727) [REG 6.10.1 -> 6.11]] /Linux/Wayland: Differences in
rendering
* [QTBUG-139446](https://qt-project.atlassian.net/browse/QTBUG-139446) Parsing text to font's glyphs happens to late and too
often
* [QTBUG-138901](https://qt-project.atlassian.net/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist

### qtdeclarative
* [QTBUG-137256](https://qt-project.atlassian.net/browse/QTBUG-137256) qmllint warns about missing-type for properties of type
QVector<EnumClass>
* [QTBUG-116675](https://qt-project.atlassian.net/browse/QTBUG-116675) QQuickWindow::grabWindow renders too small on macOS
retina
* [QTBUG-135795](https://qt-project.atlassian.net/browse/QTBUG-135795) QML Locale cannot be compiled in Direct Mode
* [QTBUG-134403](https://qt-project.atlassian.net/browse/QTBUG-134403) QtQuick Rectangle: Gradient not displayed when the color
property is set to transparent.
* [QTBUG-137350](https://qt-project.atlassian.net/browse/QTBUG-137350) weatherforecast example crashes when clicking quickly
* [QTBUG-137035](https://qt-project.atlassian.net/browse/QTBUG-137035) qmllint gets stuck
* [QTBUG-134099](https://qt-project.atlassian.net/browse/QTBUG-134099) [REG 6.7.3->6.8]Global position for QHoverEvent issued
from a QQuickItem inside a QQuickWidget is wrong.
* [QTBUG-134635](https://qt-project.atlassian.net/browse/QTBUG-134635) A floating-point precision error with the slider value.
* [QTBUG-132703](https://qt-project.atlassian.net/browse/QTBUG-132703) Unify spelling of Qt Qml modules
* [QTBUG-136492](https://qt-project.atlassian.net/browse/QTBUG-136492) TreeView: Editable and non-editable items not working
correctly
* [QTBUG-137413](https://qt-project.atlassian.net/browse/QTBUG-137413) [REG 6.9.0 -> 6.9.1] qmlformat crashes on musl
* [QTBUG-137411](https://qt-project.atlassian.net/browse/QTBUG-137411) [REG 6.9.0 -> 6.9.1] Building for iOS failed:
qmlcachegen segmentation fault
* [QTBUG-137196](https://qt-project.atlassian.net/browse/QTBUG-137196) qmlcachegen crashes in QQmlJSScope::filePath
* [QTBUG-136998](https://qt-project.atlassian.net/browse/QTBUG-136998) qmllint crashes when checking  required properties
* [QTBUG-109085](https://qt-project.atlassian.net/browse/QTBUG-109085) Typo in QML ColumnLayout documentation
* [QTBUG-135295](https://qt-project.atlassian.net/browse/QTBUG-135295) [Reg 5.15 -> 6.8] Binding crashes when combined with
StackView and Loader
* [QTBUG-133924](https://qt-project.atlassian.net/browse/QTBUG-133924) IconLabel children are positioned under Icon & text
* [QTBUG-131886](https://qt-project.atlassian.net/browse/QTBUG-131886) Wrong delta threshold for MultiPointTouchArea using
scale
* [QTBUG-112355](https://qt-project.atlassian.net/browse/QTBUG-112355) ShaderEffectSource with recursive shader causes magenta
texture on Apple Silicon
* [QTBUG-135255](https://qt-project.atlassian.net/browse/QTBUG-135255) The type compiler incorrectly gives a warning about
insufficient annotation for enum types.
* [QTBUG-137416](https://qt-project.atlassian.net/browse/QTBUG-137416) FAIL!  : tst_QQuickFileDialogImpl::defaults() Compared
values are not the same
* [QTBUG-137054](https://qt-project.atlassian.net/browse/QTBUG-137054) qmlls: Invalid color "transparent"
* [QTBUG-137469](https://qt-project.atlassian.net/browse/QTBUG-137469) "Cannot assign object to list property" error message
isn't descriptive enough
* [QTBUG-130683](https://qt-project.atlassian.net/browse/QTBUG-130683) QtQuick.Controls: Native Tooltip size on macOS
* [QTBUG-122738](https://qt-project.atlassian.net/browse/QTBUG-122738) QtQuick.Dialogs FileDialog bad color with macOS dark
theme
* [QTBUG-137561](https://qt-project.atlassian.net/browse/QTBUG-137561) FAIL!  : tst_QQuickColorDialogImpl::defaults() Received
a warning that resulted in a failure
* [QTBUG-137705](https://qt-project.atlassian.net/browse/QTBUG-137705) qmlls: lazy QmlFile in DOM loads with incorrect import
path
* [QTBUG-94147](https://qt-project.atlassian.net/browse/QTBUG-94147) QSGGeometryNode docs snippet shows Qt 6 incompatible code
* [QTBUG-137703](https://qt-project.atlassian.net/browse/QTBUG-137703) Conflicts in grammar
* [QTBUG-19407](https://qt-project.atlassian.net/browse/QTBUG-19407) Loading remote workerscripts fails
* [QTBUG-132607](https://qt-project.atlassian.net/browse/QTBUG-132607) Unexpected text's rectangle behavior in a row
* [QTBUG-137577](https://qt-project.atlassian.net/browse/QTBUG-137577) CMake Configuration of user project fails
* [QTBUG-134704](https://qt-project.atlassian.net/browse/QTBUG-134704) tst_QQuickOverlay::pressedAndReleased is flaky on
opensuse
* [QTBUG-137005](https://qt-project.atlassian.net/browse/QTBUG-137005) Qt6::qmltestrunner target no longer available
* [COIN-1211](https://qt-project.atlassian.net/browse/COIN-1211) coin not able to build webengine winarm64 in reasonable
time
* [QTBUG-134600](https://qt-project.atlassian.net/browse/QTBUG-134600) FileDialog's currentFolder shows regression on Debian
* [QTBUG-137115](https://qt-project.atlassian.net/browse/QTBUG-137115) [REG 6.5 → 6.8] Issue with inline components and setData
* [QTBUG-104829](https://qt-project.atlassian.net/browse/QTBUG-104829) QML TextArea doesn't trigger onCursorPositionChanged
when deleting whole word
* [QTBUG-137877](https://qt-project.atlassian.net/browse/QTBUG-137877) PrototypeChainCycle confuses Qt Design Studio project
storage
* [QTBUG-137323](https://qt-project.atlassian.net/browse/QTBUG-137323) Flickable jump back when scrolling to the edge in KDE
* [QTBUG-81803](https://qt-project.atlassian.net/browse/QTBUG-81803) QML TextInput - Incorrect behavior when all text is
selected and ctrl+backspace is pressed
* [QTBUG-136235](https://qt-project.atlassian.net/browse/QTBUG-136235) Qt 6.8.3 A signal 11 (SIGSEGV) crash observed while
running qtquickview_kotlin sample application (Android 11 / API 30 )
* [QTBUG-137540](https://qt-project.atlassian.net/browse/QTBUG-137540) [Reg 6.5.0 -> 6.5.5] Compilation blog post example
doesn't work anymore
* [QTBUG-137848](https://qt-project.atlassian.net/browse/QTBUG-137848) Assertion failure in tst_qquickpixmapcache::lockingCrash
* [QTBUG-127863](https://qt-project.atlassian.net/browse/QTBUG-127863) DragHandler Activates When Dragging Starts Outside the
Item and Moves Inside
* [QTBUG-137328](https://qt-project.atlassian.net/browse/QTBUG-137328) [Reg 6.7 -> 6.9] QJSEngine: created JavaScript objects
does not have function hasOwnProperty
* [QTBUG-137777](https://qt-project.atlassian.net/browse/QTBUG-137777) ComboBox deletes delegate components
* [QTBUG-137270](https://qt-project.atlassian.net/browse/QTBUG-137270) QML: model-views: bindings evaluate after item/app
destruction -> crashes
* [QTBUG-134208](https://qt-project.atlassian.net/browse/QTBUG-134208) Mnemonic annotation is passed to screen readers
* [QTBUG-134936](https://qt-project.atlassian.net/browse/QTBUG-134936) Improve imperative Menu API documentation
* [QTBUG-137030](https://qt-project.atlassian.net/browse/QTBUG-137030) Assertion in qmllint
* [QTBUG-124157](https://qt-project.atlassian.net/browse/QTBUG-124157) QJSEngine crashes when evaluating arithmetic operation
on array with self referencing
* [QTBUG-138053](https://qt-project.atlassian.net/browse/QTBUG-138053) qqmlprivate compile issue with nvcc
* [QTBUG-137326](https://qt-project.atlassian.net/browse/QTBUG-137326) [Reg 5.15 -> 6.2] Crash in
QQmlAbstractBinding::removeFromObject()
* [QTBUG-72208](https://qt-project.atlassian.net/browse/QTBUG-72208) Qt.labs.calendar onClicked date is one day off.
* [QTBUG-137025](https://qt-project.atlassian.net/browse/QTBUG-137025) Early QML signals can be missed
* [QTBUG-116539](https://qt-project.atlassian.net/browse/QTBUG-116539) LoggingCategory object created after property * Changed
signal
* [QTBUG-137823](https://qt-project.atlassian.net/browse/QTBUG-137823) Tab order does not follow visual order
* [QTBUG-118188](https://qt-project.atlassian.net/browse/QTBUG-118188) QML evaluates bindings after destruction, possibly
resulting in segmentation faults
* [QTBUG-106900](https://qt-project.atlassian.net/browse/QTBUG-106900) QML Color type docs missing first few words
* [QTBUG-133256](https://qt-project.atlassian.net/browse/QTBUG-133256) Crash on dynamically removing items from a custom
QtQuick.Controls.Container with transitions
* [QTBUG-46798](https://qt-project.atlassian.net/browse/QTBUG-46798) Destroying an item crashes ListView
* [QTBUG-136455](https://qt-project.atlassian.net/browse/QTBUG-136455) Doc: Some QML methods are missing their return value
types
* [QTBUG-49481](https://qt-project.atlassian.net/browse/QTBUG-49481) Documentation about 'Attached properties' is confused
* [QTBUG-138195](https://qt-project.atlassian.net/browse/QTBUG-138195) Android deprecation failure
* [QTBUG-127329](https://qt-project.atlassian.net/browse/QTBUG-127329) missing explanation of sci file in borderimage
* [QTBUG-138216](https://qt-project.atlassian.net/browse/QTBUG-138216) Errors in English language QML TreeView documentation
* [QTBUG-94965](https://qt-project.atlassian.net/browse/QTBUG-94965) FontDialog documentation improvements
* [QTBUG-138174](https://qt-project.atlassian.net/browse/QTBUG-138174) Lightning Viewer: runtime warnings
* [QTBUG-115170](https://qt-project.atlassian.net/browse/QTBUG-115170) [Reg 5.15 -> 6.5] qmlimportscanner does not include
module versions
* [QTBUG-138357](https://qt-project.atlassian.net/browse/QTBUG-138357) Documentation for qt_add_qml_module misses information
about find_package
* [QTBUG-138233](https://qt-project.atlassian.net/browse/QTBUG-138233) declarative_ui::MapItems::test_drag() Compared values
are not the same
* [QTBUG-138200](https://qt-project.atlassian.net/browse/QTBUG-138200) iOS Style: Wrong palette colors when switching color
scheme from application
* [QTBUG-138346](https://qt-project.atlassian.net/browse/QTBUG-138346) qmllint: claims binding will not update on a signal
handler (i.e. not a binding)
* [QTBUG-122436](https://qt-project.atlassian.net/browse/QTBUG-122436) Android a11y: Changes to Accessible.ignored and
Item.visible are not propagated to the screen reader
* [QTBUG-132518](https://qt-project.atlassian.net/browse/QTBUG-132518) building with cmake 3.31 gives ODR violation warnings on
webassembly
* [QTBUG-127133](https://qt-project.atlassian.net/browse/QTBUG-127133) Why do I get warning "Multiple C++ types called xxx
found! This violates the One Definition Rule"
* [QTBUG-134292](https://qt-project.atlassian.net/browse/QTBUG-134292) ODR warnings with static build
* [QTBUG-54605](https://qt-project.atlassian.net/browse/QTBUG-54605) SignalSpy's clear() function is incorrectly documented as
causing valid to become false
* [QTBUG-120706](https://qt-project.atlassian.net/browse/QTBUG-120706) ScrollView::effectiveScrollBarHeight and
ScrollView::effectiveScrollbarWidth need elaboration on what exactly
"effective" mean
* [QTBUG-77201](https://qt-project.atlassian.net/browse/QTBUG-77201) Documentation of QQuickItem::stackAfter/stackBefore is
wrong
* [QTBUG-136147](https://qt-project.atlassian.net/browse/QTBUG-136147) Qt Labs Platforms: Add alt texts
* [QTBUG-127955](https://qt-project.atlassian.net/browse/QTBUG-127955) Repeater without parent reports its count but does not
create delegates
* [QTBUG-135329](https://qt-project.atlassian.net/browse/QTBUG-135329) Qt.btoa () return Base64 code for Uint8Array
* [QTBUG-138349](https://qt-project.atlassian.net/browse/QTBUG-138349) QmlPreview does not start with import QtQuick.Controls +
Style=Basic
* [QTBUG-138391](https://qt-project.atlassian.net/browse/QTBUG-138391) Deep-nested QML module containing *.mjs file can cause
ambiguous import
* [QTBUG-138242](https://qt-project.atlassian.net/browse/QTBUG-138242) Crash when GC is triggered during script exception
handling in StateChangeScript or ScriptAction
* [QTBUG-134652](https://qt-project.atlassian.net/browse/QTBUG-134652) Application in long folder name fails to load QML
plugins
* [QTBUG-136959](https://qt-project.atlassian.net/browse/QTBUG-136959) Read-only TextEdit overrides all Shortcuts when it has
activeFocus
* [QTBUG-138209](https://qt-project.atlassian.net/browse/QTBUG-138209) iOS: Two context menus appear for TextField
* [QTBUG-126193](https://qt-project.atlassian.net/browse/QTBUG-126193) Crash in XR when clicking on Slider in Android Style
* [QTBUG-88367](https://qt-project.atlassian.net/browse/QTBUG-88367) Gnome virtual keyboard does not open with echoMode:
TextInput.password
* [QTBUG-130801](https://qt-project.atlassian.net/browse/QTBUG-130801) qmlls: gotodefinition does not work on singletons
* [QTBUG-138171](https://qt-project.atlassian.net/browse/QTBUG-138171) File System Explorer: qmllint warnings
* [QTBUG-137939](https://qt-project.atlassian.net/browse/QTBUG-137939) New Qt 6.10 APIs in QSGGeometry show "since Qt 6.9"
* [QTBUG-137862](https://qt-project.atlassian.net/browse/QTBUG-137862) SearchField::currentIndex have dubious behavior
* [QTBUG-136611](https://qt-project.atlassian.net/browse/QTBUG-136611) OpenGL: Layering breaks culling
* [QTBUG-138559](https://qt-project.atlassian.net/browse/QTBUG-138559) qt_add_qml_module: TARGET dependency causes build
failure
* [QTBUG-138625](https://qt-project.atlassian.net/browse/QTBUG-138625) sucessful Variable Name Error
* [QTBUG-96350](https://qt-project.atlassian.net/browse/QTBUG-96350) QML: Shortcut: strange warning
* [QTBUG-138663](https://qt-project.atlassian.net/browse/QTBUG-138663) Comment error, unnecessary spelling error
* [QTBUG-138515](https://qt-project.atlassian.net/browse/QTBUG-138515) qmllint gets type of root id wrong
* [QTBUG-136566](https://qt-project.atlassian.net/browse/QTBUG-136566) Qml Structured Value does not work with qml arrays
* [QTBUG-137029](https://qt-project.atlassian.net/browse/QTBUG-137029) Qmllint as process on Windows do not populate error
channel unless called in terminal.
* [QTBUG-138358](https://qt-project.atlassian.net/browse/QTBUG-138358) QSGDefaultRectangleNode always returns invalid color
* [QTBUG-138532](https://qt-project.atlassian.net/browse/QTBUG-138532) qmllint: unterminated-case
* [QTBUG-133267](https://qt-project.atlassian.net/browse/QTBUG-133267) Curve renderer does not always show latest version of
path data
* [QTBUG-138602](https://qt-project.atlassian.net/browse/QTBUG-138602) Reg[6.9->6.10]Application toolbar turns black
* [QTBUG-137900](https://qt-project.atlassian.net/browse/QTBUG-137900) QML sslConfiguration has sslOptions propery out of sync
* [QTBUG-138749](https://qt-project.atlassian.net/browse/QTBUG-138749) Qt.uiLanguage is flagged by qmllint with [stale-
property-read] warning
* [QTBUG-138104](https://qt-project.atlassian.net/browse/QTBUG-138104) tst_qtquickview_signallistener crashes on Android
* [QTBUG-137860](https://qt-project.atlassian.net/browse/QTBUG-137860) [Windows][A11y] Text can not be selected by NVDA
* [QTBUG-138838](https://qt-project.atlassian.net/browse/QTBUG-138838) Compile failure due to QQmlSslConfiguration
* [QTBUG-138871](https://qt-project.atlassian.net/browse/QTBUG-138871) ASSERT: QColorOutput::colorify: "It makes no sense to
attempt to print an empty string."
* [QTBUG-136688](https://qt-project.atlassian.net/browse/QTBUG-136688) QJSEngine: call eval() directly from C++ crash
application
* [QTBUG-136355](https://qt-project.atlassian.net/browse/QTBUG-136355) Disabling qml-locale can segfault qmltc
* [QTBUG-136598](https://qt-project.atlassian.net/browse/QTBUG-136598) Item::enabled behaves inconsistently with docs on Qt 6
* [QTBUG-30801](https://qt-project.atlassian.net/browse/QTBUG-30801) Button: tooltip not shown when the button is disabled
* [QTBUG-138478](https://qt-project.atlassian.net/browse/QTBUG-138478) TapHandler doesn't react to touch input inside popup
background
* [QTBUG-138927](https://qt-project.atlassian.net/browse/QTBUG-138927) Incubator crashing when being destroyed
* [QTBUG-133247](https://qt-project.atlassian.net/browse/QTBUG-133247) Fill not correctly rendered by curve renderer
* [QTBUG-133313](https://qt-project.atlassian.net/browse/QTBUG-133313) "Invalid import qualifier ID" message doesn't say why
it's invalid
* [QTBUG-94251](https://qt-project.atlassian.net/browse/QTBUG-94251) tst_QQuickPopup fails with OpenSUSE 15.3
* [QTBUG-137733](https://qt-project.atlassian.net/browse/QTBUG-137733) quick/flexboxLayouts launch fails
* [QTBUG-138490](https://qt-project.atlassian.net/browse/QTBUG-138490) Incorrect item ordering in QML container when the
ListView is nested within another Item.
* [QTBUG-123988](https://qt-project.atlassian.net/browse/QTBUG-123988) QSGGeometryData::hasDirtyIndexData() implementation uses
wrong member variable
* [QTBUG-123985](https://qt-project.atlassian.net/browse/QTBUG-123985) PinchHandler works unreliably with Wayland
* [QTBUG-138028](https://qt-project.atlassian.net/browse/QTBUG-138028) TextField with placeholder text strange behavior with
Binding
* [QTBUG-139093](https://qt-project.atlassian.net/browse/QTBUG-139093) Lancelot baseline test fails for SearchField
* [QTBUG-138516](https://qt-project.atlassian.net/browse/QTBUG-138516) [Reg 6.8 -> 6.9] QML: compiler: methods crash in
(nested) QQmlPrivate::callArrowFunction
* [QTBUG-139104](https://qt-project.atlassian.net/browse/QTBUG-139104) qmlls crash when opening a qmltypes file
* [QTBUG-78162](https://qt-project.atlassian.net/browse/QTBUG-78162) tst_qquicktextinput::mouseSelectionMode() is flaky on
OpenSuse 15.0
* [QTBUG-139304](https://qt-project.atlassian.net/browse/QTBUG-139304) QML text with heading role is not read by screenreader
* [QTBUG-138001](https://qt-project.atlassian.net/browse/QTBUG-138001) Doc: Inconsistency in QML Layout inheritance tree
* [QTBUG-138219](https://qt-project.atlassian.net/browse/QTBUG-138219) Doc Issues with Qt Quick for Android Studio Projects
* [QTBUG-78261](https://qt-project.atlassian.net/browse/QTBUG-78261) tst_focus::policy is failing
* [QTBUG-137160](https://qt-project.atlassian.net/browse/QTBUG-137160) qt quick Loader active=false with unfinished Menu crash
* [QTBUG-137829](https://qt-project.atlassian.net/browse/QTBUG-137829) Don't allow yoga library symbols exposed from QT
libraries (either static / dynamic)
* [QTBUG-139583](https://qt-project.atlassian.net/browse/QTBUG-139583) FAIL!  : tst_QQuickApplicationWindow::layout()
* [QTBUG-139309](https://qt-project.atlassian.net/browse/QTBUG-139309) REG: Material Slider's hovered effects visible when they
shouldn't be
* [QTBUG-139626](https://qt-project.atlassian.net/browse/QTBUG-139626) AOT-compiled code crashes when accessing members of
QList<QVariantMap>
* [QTBUG-139633](https://qt-project.atlassian.net/browse/QTBUG-139633) Doc: Synchronizer should have \since 6.10
* [QTBUG-129972](https://qt-project.atlassian.net/browse/QTBUG-129972) [REG 6.6 → 6.7] Array returned to QML from CPP is not
retaining changes made in QML/JS
* [QTBUG-139025](https://qt-project.atlassian.net/browse/QTBUG-139025) [Reg 6.5.9 -> 6.8.4] Lists of objects with
JavaScriptOwnership, stored in var properties, are no longer destroyed
* [QTBUG-139059](https://qt-project.atlassian.net/browse/QTBUG-139059) Generated code does not track objects on JavaScript
stack
* [QTBUG-138919](https://qt-project.atlassian.net/browse/QTBUG-138919) [Reg 6.5.9 -> 6.8.4] Unreferenced objects with
JavaScriptOwnership are no longer destroyed
* [QTBUG-139306](https://qt-project.atlassian.net/browse/QTBUG-139306) Popup inside an async Loader crashes Qt Quick app if
there is direct property binding (possible racing condition)
* [QTBUG-135249](https://qt-project.atlassian.net/browse/QTBUG-135249) Popup: Some properties can not be bound
* [QTBUG-100259](https://qt-project.atlassian.net/browse/QTBUG-100259) tst_controls crash on Android
* [QTBUG-100258](https://qt-project.atlassian.net/browse/QTBUG-100258) tst_focus crashes on Android
* [QTBUG-139415](https://qt-project.atlassian.net/browse/QTBUG-139415) tst_controls has failing test cases
* [QTBUG-139781](https://qt-project.atlassian.net/browse/QTBUG-139781) Issues with SortFilterProxyModel docs
* [QTBUG-138886](https://qt-project.atlassian.net/browse/QTBUG-138886) Improve "once-off assignment" wording in QML
PropertyChanges documentation
* [QTBUG-123106](https://qt-project.atlassian.net/browse/QTBUG-123106) Documentation - Linking of QtQuickView STATUS_READY,
STATUS_NULL etc.. in docs
* [QTBUG-135474](https://qt-project.atlassian.net/browse/QTBUG-135474) QtQuickView Android class docs miss QtQmlStatus ?
* [QTBUG-139715](https://qt-project.atlassian.net/browse/QTBUG-139715) TextArea background invisible in Fusion style
* [QTBUG-139997](https://qt-project.atlassian.net/browse/QTBUG-139997) Curve renderer matrix scale detection fails when layer
is enabled
* [QTBUG-139764](https://qt-project.atlassian.net/browse/QTBUG-139764) Inconsistent conversions between QVariantList and
QList<T>
* [QTBUG-140057](https://qt-project.atlassian.net/browse/QTBUG-140057)  ASSERT: "locals" in file
/Users/qt/work/qt/qtdeclarative/src/qml/memory/qv4mm.cpp, line 1487
* [QTBUG-137172](https://qt-project.atlassian.net/browse/QTBUG-137172) "section" property in ListView behaviour is broken
(degradation)
* [QTBUG-140074](https://qt-project.atlassian.net/browse/QTBUG-140074) Crash in QQmlPrivate::callArrowFunctionAsVariant() when
using qmlcachegen
* [QTBUG-139342](https://qt-project.atlassian.net/browse/QTBUG-139342) [Windows] Context menu mouse event is propagated further
* [QTBUG-136629](https://qt-project.atlassian.net/browse/QTBUG-136629) QUnifiedTimer::updateAnimationTimers() crashes when
QApplication is recreated
* [QTBUG-140143](https://qt-project.atlassian.net/browse/QTBUG-140143) ValueFilter::value is documented as being a string when
it should be a variant
* [QTBUG-140161](https://qt-project.atlassian.net/browse/QTBUG-140161) FAIL!  : tst_QmlCppCodegen::callObjectLookupOnNull()
Compared values are not the same
* [QTBUG-139125](https://qt-project.atlassian.net/browse/QTBUG-139125) qmlformat: Documentation for CLI options and INI file
options are not sync'ed
* [QTBUG-126558](https://qt-project.atlassian.net/browse/QTBUG-126558) startSystemMove and startSystemResize don't have qml
documentation
* [QTBUG-128483](https://qt-project.atlassian.net/browse/QTBUG-128483) ItemGrabResult garbage collected too early
* [QTBUG-140415](https://qt-project.atlassian.net/browse/QTBUG-140415) qmlcachegen asserts in
QQmlJSRegisterContentPool::adjustType
* [QTBUG-139561](https://qt-project.atlassian.net/browse/QTBUG-139561) Crash when layer.enabled bound to MouseArea's
containsMouse
* [QTBUG-129088](https://qt-project.atlassian.net/browse/QTBUG-129088) Support Contrast themes in FluentWinUI3
* [QTBUG-139608](https://qt-project.atlassian.net/browse/QTBUG-139608) Synchronizer documentation could show how to use it with
singletons
* [QTBUG-139632](https://qt-project.atlassian.net/browse/QTBUG-139632) qmlls, qmllint, and qmlsc don't recognize required
properties set using "on" syntax
* [QTBUG-140026](https://qt-project.atlassian.net/browse/QTBUG-140026) TreeModel and TreeViewDelegate don't cooperate
* [QTBUG-140544](https://qt-project.atlassian.net/browse/QTBUG-140544) SceneGraph examples draws text under navigation bar.
* [QTBUG-138480](https://qt-project.atlassian.net/browse/QTBUG-138480) Top flaky test:
tst_qquickwidget::focusOnClickInProxyWidget
* [QTBUG-138518](https://qt-project.atlassian.net/browse/QTBUG-138518) [REG: 6.8.2 → 6.8.3] Inconsistent behavior of
QQmlEngine::clearComponentCache
* [QTBUG-140481](https://qt-project.atlassian.net/browse/QTBUG-140481) SpinBox up down indicators visually remain pressed
* [QTBUG-136958](https://qt-project.atlassian.net/browse/QTBUG-136958) [QuickControls] Highlight of the controls is square
instead of round
* [QTBUG-140018](https://qt-project.atlassian.net/browse/QTBUG-140018) [REG 6.9.1->6.9.2] QQuickStackElement::initialize null
dereference
* [QTBUG-140554](https://qt-project.atlassian.net/browse/QTBUG-140554) QQmlPropertyMap crash
* [QTBUG-138599](https://qt-project.atlassian.net/browse/QTBUG-138599) .qmlls.ini has wrong buildDir
* [QTBUG-140690](https://qt-project.atlassian.net/browse/QTBUG-140690) JavaScript function return type list<T> cannot be
correctly assigned to prop if annotated
* [QTBUG-139783](https://qt-project.atlassian.net/browse/QTBUG-139783) Filter's "invert" property doesn't follow QML naming
conventions
* [QTBUG-140400](https://qt-project.atlassian.net/browse/QTBUG-140400) Regression: QInputMethodEvent::Selection start does not
work anymore with commit string
* [QTBUG-94253](https://qt-project.atlassian.net/browse/QTBUG-94253) When an inputmask is set on a TextInput then it will
overwrite the first character if the cursor starts from position 0 after
typing the second character
* [QTBUG-123631](https://qt-project.atlassian.net/browse/QTBUG-123631) ScrollView Padding Property
* [QTBUG-139687](https://qt-project.atlassian.net/browse/QTBUG-139687) [REG 6.6 → 6.8] Broken list property update when the
setter delays modification
* [QTBUG-140665](https://qt-project.atlassian.net/browse/QTBUG-140665) qt_generate_deploy_qml_app is missing plugin deployment
options
* [QTBUG-140838](https://qt-project.atlassian.net/browse/QTBUG-140838) Top flaky test: tst_QQuickTextField::contextMenuDelete
* [QTBUG-138465](https://qt-project.atlassian.net/browse/QTBUG-138465) Line edits are not visible on macOS 26
* [QTBUG-140738](https://qt-project.atlassian.net/browse/QTBUG-140738) Crash with cachegen compiled code
* [QTBUG-140465](https://qt-project.atlassian.net/browse/QTBUG-140465) AOT compiled (cachegen) qml crashes program when
attempting to call a function on a destroyed context
* [QTBUG-134903](https://qt-project.atlassian.net/browse/QTBUG-134903) Duplicate context menus when using custom context Menus
in text controls
* [QTBUG-132384](https://qt-project.atlassian.net/browse/QTBUG-132384) TapHandler emits tapped after ContextMenu gets its
context menu event when running tst_QQuickContextMenu::eventOrder
* [QTBUG-140914](https://qt-project.atlassian.net/browse/QTBUG-140914) QML Preview: Updates to Singletons do not reflect in the
preview
* [QTBUG-119504](https://qt-project.atlassian.net/browse/QTBUG-119504) Inconsistent behavior of list property in QML
* [QTBUG-140922](https://qt-project.atlassian.net/browse/QTBUG-140922) SpinBox missing from Quick Controls Overview in
Documentation
* [QTBUG-139142](https://qt-project.atlassian.net/browse/QTBUG-139142) qmltc: Assertion when instantiating a "cross-nested"
class
* [QTBUG-32298](https://qt-project.atlassian.net/browse/QTBUG-32298) The canvas component method getImageData() will not
release the frame buffer from system memory.
* [QTBUG-85490](https://qt-project.atlassian.net/browse/QTBUG-85490) REG: Quick 2 TextField doesn't respect IntValidator top,
bottom
* [QTBUG-139699](https://qt-project.atlassian.net/browse/QTBUG-139699) Incorrect calculations involving Layout.preferredHeight
and Layout.fillHeight in nested layouts
* [QTBUG-138825](https://qt-project.atlassian.net/browse/QTBUG-138825) Attached properties through createObject with initial
parameters crash if done from a javascript file
* [QTBUG-141059](https://qt-project.atlassian.net/browse/QTBUG-141059) [Reg 6.8 -> 6.10] Assert in
QQmlPropertyCacheAliasCreator<QQmlTypeCompiler>::propertyDataForAlias
* [QTBUG-140915](https://qt-project.atlassian.net/browse/QTBUG-140915) qmlls: show import paths in import tooltip
* [QTBUG-141085](https://qt-project.atlassian.net/browse/QTBUG-141085) [qtdeclarative] Install failure
* [QTBUG-141063](https://qt-project.atlassian.net/browse/QTBUG-141063) Conflict (409) is not a network error so it should be
handled by status code
* [QTBUG-137404](https://qt-project.atlassian.net/browse/QTBUG-137404) Broken Text Outline Rendering with Text.Outline When
Using Software Graphics API
* [QTBUG-139344](https://qt-project.atlassian.net/browse/QTBUG-139344) call TreeView's expand in delegate will add extra items
* [QTBUG-136783](https://qt-project.atlassian.net/browse/QTBUG-136783) PathLine is not rendered when setting the display's
scale to 100%.
* [QTBUG-140068](https://qt-project.atlassian.net/browse/QTBUG-140068) Material background is black with color #FAFAFA
* [QTBUG-131895](https://qt-project.atlassian.net/browse/QTBUG-131895) cursor "stuck" in previous field with
nextItemInFocusChain().forceActiveFocus()
* [QTBUG-141161](https://qt-project.atlassian.net/browse/QTBUG-141161) FAIL!  : tst_qquickwidget::focusOnClickInProxyWidget()
Received a fatal error.
* [QTBUG-139400](https://qt-project.atlassian.net/browse/QTBUG-139400) Properly manage QtEditText focus and InputConnection
callbacks
* [QTBUG-
141060](https://qt-project.atlassian.net/browse/QTBUG-141060) tst_RenderControl::renderAndReadBackWithVulkanAndCustomDepthTextu
re fails on rx480
* [QTBUG-136943](https://qt-project.atlassian.net/browse/QTBUG-136943) Software renderer: Visual glitches when moving things
around a Flickable
* [QTBUG-140220](https://qt-project.atlassian.net/browse/QTBUG-140220) qml plugins are not re-instantiated if qapplication is
recreated
* [QTBUG-141194](https://qt-project.atlassian.net/browse/QTBUG-141194) qmllint - Warnings when setting FlexboxLayout.direction
in Visual Studio Code/VSCodium
* [QTBUG-132914](https://qt-project.atlassian.net/browse/QTBUG-132914) Qt Quick Drawer cannot be opened by touch when window is
rotated
* [QTBUG-141168](https://qt-project.atlassian.net/browse/QTBUG-141168) VectorImage: Masked items with transforms do not work
* [QTBUG-140533](https://qt-project.atlassian.net/browse/QTBUG-140533) Responsive layouts example does not lay out if shown
with a size bigger than NxM
* [QTBUG-141198](https://qt-project.atlassian.net/browse/QTBUG-141198) Doc: List of JavaScript functions topic is localized
incorrectly
* [QTBUG-141182](https://qt-project.atlassian.net/browse/QTBUG-141182) QML ProgressBar has broken layout on macOS 26
* [QTBUG-141219](https://qt-project.atlassian.net/browse/QTBUG-141219) qt_add_qml_module's relative IMPORT_PATH doesn't satisfy
qmlls
* [QTBUG-139679](https://qt-project.atlassian.net/browse/QTBUG-139679) Custom key handling in TextArea broken
* [QTBUG-133368](https://qt-project.atlassian.net/browse/QTBUG-133368) Qt Quick Software Renderer: Colour changes at fractional
coordinates produce a stray black line
* [QTBUG-141105](https://qt-project.atlassian.net/browse/QTBUG-141105) [REG] SIGSEGV in QQmlDelegateModelItem::destroyObject(),
accesses invalid QObjectData
* [QTBUG-140900](https://qt-project.atlassian.net/browse/QTBUG-140900) Crash when assigning a function declaration to a
ListElement(for nested lists)
* [QTBUG-141225](https://qt-project.atlassian.net/browse/QTBUG-141225) qmlls: don't warn about QT_QML_GENERATE_QMLLS_INI
anymore
* [QTBUG-141119](https://qt-project.atlassian.net/browse/QTBUG-141119) document how to make qmlls know about QML elements
defined in Qt Bridges projects
* [QTBUG-139603](https://qt-project.atlassian.net/browse/QTBUG-139603) Menu does not propagate Material style to submenus with
popupType: Popup.Window
* [QTBUG-141464](https://qt-project.atlassian.net/browse/QTBUG-141464) [FTBFS] AUTOMOC for target tst_qqmlimport_static_module:
The "moc" executable ... does not exist.
* [QTBUG-140414](https://qt-project.atlassian.net/browse/QTBUG-140414) Reg 6.9->6.10: color incorrectly changes to black and
crash if log
* [QTBUG-140487](https://qt-project.atlassian.net/browse/QTBUG-140487) Qt Quick States documentation shows old PropertyChanges
syntax
* [QTBUG-140441](https://qt-project.atlassian.net/browse/QTBUG-140441) a11y: QtQuick TextInput is inaccessible/missing in a11y
tree
* [QTBUG-139943](https://qt-project.atlassian.net/browse/QTBUG-139943) [iOS][Android] TextEdit or TextInput cannot be navigated
using A11y granularity
* [QTBUG-141420](https://qt-project.atlassian.net/browse/QTBUG-141420) qmlcachegen: calling func(obj) clones obj instead of
passing it by ref
* [QTBUG-141638](https://qt-project.atlassian.net/browse/QTBUG-141638) .qmlformat.ini "SemicolonRule=essential" is not
respected
* [QTBUG-140673](https://qt-project.atlassian.net/browse/QTBUG-140673) a11y: QML ScrollBar doesn't report current
position/value on accessibility layer
* [QTBUG-139833](https://qt-project.atlassian.net/browse/QTBUG-139833) [a11y] Auditive feedback during scroll missing
* [QTBUG-138845](https://qt-project.atlassian.net/browse/QTBUG-138845) [REG 6.2 → 6.3] qmllint ignores lambda
* [QTBUG-141448](https://qt-project.atlassian.net/browse/QTBUG-141448) Actual device pixel ratio inaccessible from QML under
Wayland
* [QTBUG-141646](https://qt-project.atlassian.net/browse/QTBUG-141646) Infinite loop in garbage collector, freezing Application
* [QTBUG-102811](https://qt-project.atlassian.net/browse/QTBUG-102811) "ScrollView + ListView + DelegateModel" crashes when
`reuseItems: true` and the size of ScrollView depends on delegate items
* [QTBUG-140858](https://qt-project.atlassian.net/browse/QTBUG-140858) [REG: 6.8 -> 6.9] QML Conditional Binding does not
restore original value
* [QTBUG-81884](https://qt-project.atlassian.net/browse/QTBUG-81884) qtdeclarative:
tst_HoverHandler::movingItemWithHoverHandler fails on macOS >= 10.14
because it uses QCursor::setPos()
* [QTBUG-103065](https://qt-project.atlassian.net/browse/QTBUG-103065) tst_HoverHandler::movingItemWithHoverHandler() fails on
Android
* [QTBUG-111294](https://qt-project.atlassian.net/browse/QTBUG-111294) tst_HoverHandler::movingItemWithHoverHandler fails with
SLES 15.4
* [QTBUG-141090](https://qt-project.atlassian.net/browse/QTBUG-141090) RangeSlider first.value/second.value error when should
be integer
* [QTBUG-141229](https://qt-project.atlassian.net/browse/QTBUG-141229) Built-in ScrollBars still visible when customising
ScrollView
* [QTBUG-141704](https://qt-project.atlassian.net/browse/QTBUG-141704) Crash when destroying QQmlPropertyMap
* [QTBUG-141849](https://qt-project.atlassian.net/browse/QTBUG-141849) Property binding generates incorrect JavaScript object
* [QTBUG-141893](https://qt-project.atlassian.net/browse/QTBUG-141893) QtQuick application with space in folder fails to
configure
* [QTBUG-140875](https://qt-project.atlassian.net/browse/QTBUG-140875) QML Text - multi-line text is not always elided
correctly when item is resized
* [QTBUG-140757](https://qt-project.atlassian.net/browse/QTBUG-140757) [Reg 6.9->6.10] Performance regression in
delegates_item_childrenRect QmlBench benchmark
* [QTBUG-141911](https://qt-project.atlassian.net/browse/QTBUG-141911) SIGSEGV in tst_palette
* [QTBUG-139352](https://qt-project.atlassian.net/browse/QTBUG-139352) Default button does not get focus when displaying dialog
* [QTBUG-141913](https://qt-project.atlassian.net/browse/QTBUG-141913) SortFilterProxyModel: Not be able to run demo using
`qml` utility
* [QTBUG-141242](https://qt-project.atlassian.net/browse/QTBUG-141242) QML file that imports the module it belongs to results
in "Failed to import" qmlls warning
* [QTBUG-141998](https://qt-project.atlassian.net/browse/QTBUG-141998)  FAIL!  :
inputpanelcontrols::tst_inputpanelcontrols::test_worksWithModal()
'verify()' returned FALSE. ()
* [QTBUG-141963](https://qt-project.atlassian.net/browse/QTBUG-141963) GC Sweep logic is broken and masks life time bug in
QQmlDelegateModel
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
* [QTBUG-142025](https://qt-project.atlassian.net/browse/QTBUG-142025) qmlls can't read from std::cin
* [QTBUG-123991](https://qt-project.atlassian.net/browse/QTBUG-123991) Masks inside <defs> ignored by Qt SVG parser
* [QTBUG-141734](https://qt-project.atlassian.net/browse/QTBUG-141734) a11y: QML button box has unexpected "page tab list" a11y
role
* [QTBUG-142264](https://qt-project.atlassian.net/browse/QTBUG-142264) Top flaky test:
tst_qmlls_qqmlcodemodel::reloadLotsOfFiles
* [QTBUG-141707](https://qt-project.atlassian.net/browse/QTBUG-141707) Given the same list of import paths, qmlls might load a
different module than qmllint/qmlsc
* [QTBUG-142472](https://qt-project.atlassian.net/browse/QTBUG-142472) FAIL!  : tst_VectorImage::parseFiles(skew_bothaxes.json)
'!item->childItems().first()->size().isNull()' returned FALSE
* [QTBUG-142331](https://qt-project.atlassian.net/browse/QTBUG-142331) Problem with FallbackAsVariant lookups in AOT adapter
code in qqml.cpp
* [QTBUG-142555](https://qt-project.atlassian.net/browse/QTBUG-142555) [Reg 6.5.10 -> 6.8.5] Qt.createQmlObject() causes memory
leak
* [QTBUG-141045](https://qt-project.atlassian.net/browse/QTBUG-141045) Remove stale version information from Qt Quick Controls
* [QTBUG-142529](https://qt-project.atlassian.net/browse/QTBUG-142529) tst_qmltyperegistrar::unconstructibleValueType()
'qmltypesData.contains
* [QTBUG-142208](https://qt-project.atlassian.net/browse/QTBUG-142208) Animating shape gradient color increasing memory usage
* [QTBUG-142550](https://qt-project.atlassian.net/browse/QTBUG-142550) AOT crash: SIGSEGV in QMetaObject::indexOfProperty when
QString used in short-circuit expression with derived value
* [QTBUG-142665](https://qt-project.atlassian.net/browse/QTBUG-142665) [REG 6.10.1->6.11.0] quick/quickshapes/weatherforecast
not configuring on Android
* [QTBUG-142658](https://qt-project.atlassian.net/browse/QTBUG-142658) [Reg 6.5.10 -> 6.8.5] QQmlFileSelector's selection
inappropriately propagates to subsequent engines
* [QTBUG-142574](https://qt-project.atlassian.net/browse/QTBUG-142574) qmlls crashes in QQmlJSScopesById::possibleIds
* [QTBUG-142549](https://qt-project.atlassian.net/browse/QTBUG-142549) false warning: Accessible attached property must be
attached to an object deriving from Item or Action
* [QTBUG-142468](https://qt-project.atlassian.net/browse/QTBUG-142468) ASSERT: "!declarationsOverride" in qmllint
* [QTBUG-139362](https://qt-project.atlassian.net/browse/QTBUG-139362) ColorDialog fails to display colors
* [QTBUG-141882](https://qt-project.atlassian.net/browse/QTBUG-141882) macOS SearchField produces warnings
* [QTBUG-142407](https://qt-project.atlassian.net/browse/QTBUG-142407) [REG 6.2.13 → 6.3.0]  Import of QtQuick.Controls shadows
qualified import QML types
* [QTBUG-138193](https://qt-project.atlassian.net/browse/QTBUG-138193) QML menu set to visible on creation doesn't show
* [QTBUG-141729](https://qt-project.atlassian.net/browse/QTBUG-141729) QmlCompiler fail
* [QTBUG-142366](https://qt-project.atlassian.net/browse/QTBUG-142366) Regression: Events not delivered to grandchild that
extends outside its grandparent
* [QTBUG-143108](https://qt-project.atlassian.net/browse/QTBUG-143108) error: undefined symbol:
QQuickAnimatedProperty::PropertyAnimation::simplified() const
* [QTBUG-141047](https://qt-project.atlassian.net/browse/QTBUG-141047) Screenshot not working in dark mode
* [QTBUG-143070](https://qt-project.atlassian.net/browse/QTBUG-143070) macOS SearchField has some styling issues
* [QTBUG-142820](https://qt-project.atlassian.net/browse/QTBUG-142820) Unexpanded QDoc macros in Qt Assistant index
* [QTBUG-141830](https://qt-project.atlassian.net/browse/QTBUG-141830) Sorted QSortFilterProxyModel crash in static builds
* [QTBUG-142577](https://qt-project.atlassian.net/browse/QTBUG-142577) Qt Designer on Mac OS fails to load a custom widget
plugin due to code signature issue
* [QTBUG-107028](https://qt-project.atlassian.net/browse/QTBUG-107028) tst_qquicktextfield and tst_qquicktextarea fail on
Android
* [QTBUG-142514](https://qt-project.atlassian.net/browse/QTBUG-142514) callArrowFunction / callObjectPropertyLookup randomly
crashing when receiving notifications
* [QTBUG-142440](https://qt-project.atlassian.net/browse/QTBUG-142440) ContextMenu position is wrong for TextInput
* [QTBUG-143374](https://qt-project.atlassian.net/browse/QTBUG-143374) [REG Qt 6.11.0 Beta 1] Missing
Qt6::QuickControls2FusionPrivate
* [QTBUG-143112](https://qt-project.atlassian.net/browse/QTBUG-143112) Fill not correctly rendered by curve renderer when pack
goes backwards
* [QTBUG-134502](https://qt-project.atlassian.net/browse/QTBUG-134502) The app crashes with ListView when using contentHeight
and fast scrolling with a mouse wheel.
* [QTBUG-138247](https://qt-project.atlassian.net/browse/QTBUG-138247) As a Qt user, I would like to know which version I need
to use a specific pragma
* [QTBUG-121361](https://qt-project.atlassian.net/browse/QTBUG-121361) Document that QML_EXTENDED is *not* meant for extending
types you don't control
* [QTBUG-143461](https://qt-project.atlassian.net/browse/QTBUG-143461) Having both cosmetic and non-cosmetic ShapePaths in the
same Shape does not work
* [QTBUG-142369](https://qt-project.atlassian.net/browse/QTBUG-142369) Property bevel of RectangleShape is not working
* [QTBUG-128664](https://qt-project.atlassian.net/browse/QTBUG-128664) Document that you need to declare DEPENDENCIES in order
to use other modules' C++ types in your module
* [QTBUG-143618](https://qt-project.atlassian.net/browse/QTBUG-143618) qmllint does not report parser warnings to the user
* [QTBUG-143547](https://qt-project.atlassian.net/browse/QTBUG-143547) [Reg 6.10.1->6.10.2]: Application palette is reset after
loading a QQuickWidget
* [QTBUG-143260](https://qt-project.atlassian.net/browse/QTBUG-143260) ASSERT: "scope->isFullyResolved()" in qmllint
* [QTBUG-143203](https://qt-project.atlassian.net/browse/QTBUG-143203) SearchField indicator docs need work
* [QTBUG-143479](https://qt-project.atlassian.net/browse/QTBUG-143479) [Reg 6.10.1 -> 6.11.0b2] macdeployqt fails on *.conf
files
* [QTBUG-143262](https://qt-project.atlassian.net/browse/QTBUG-143262) ASSERT: "m_objectStrongRef == 0" in Repeater with
DelegateChooser
* [QTBUG-142074](https://qt-project.atlassian.net/browse/QTBUG-142074) readonly TextInput cause warning that application copied
from clipboard on Android
* [QTBUG-140155](https://qt-project.atlassian.net/browse/QTBUG-140155) Qmllint issue when using Controls.SpinBox.textFromValue
* [QTBUG-143554](https://qt-project.atlassian.net/browse/QTBUG-143554) "" == 0   returns false in the compiler
* [QTBUG-143733](https://qt-project.atlassian.net/browse/QTBUG-143733) Crash in QQmlDelegateModel destructor
* [QTBUG-140507](https://qt-project.atlassian.net/browse/QTBUG-140507) Incorrect palette colors when enabling a contrast theme
while a hybrid widgets + quick application is running.
* [QTBUG-142511](https://qt-project.atlassian.net/browse/QTBUG-142511) FileDialog use with -no-feature-accessibility broken
* [QTBUG-123141](https://qt-project.atlassian.net/browse/QTBUG-123141) A description about Loader is not clear enough
* [QTBUG-141246](https://qt-project.atlassian.net/browse/QTBUG-141246) qmlls fix for unqualified access is applied in the wrong
place
* [QTBUG-143823](https://qt-project.atlassian.net/browse/QTBUG-143823) qmllint suggests correct and wrong fix at the same time
* [QTBUG-64656](https://qt-project.atlassian.net/browse/QTBUG-64656) Wrong name for DragEvent.source propery
* [QTBUG-143857](https://qt-project.atlassian.net/browse/QTBUG-143857) QQuickWidget forgets its clearColor if its underlying
window changes
* [QTBUG-142682](https://qt-project.atlassian.net/browse/QTBUG-142682) qmllint should warn when trying to override a
nonexistant property
* [QTBUG-142946](https://qt-project.atlassian.net/browse/QTBUG-142946) QML tools don't yet accept explicit overrides
* [QTBUG-143771](https://qt-project.atlassian.net/browse/QTBUG-143771) qmlcachegen crash with eval in if .. else when
generating cpp file
* [QTBUG-46434](https://qt-project.atlassian.net/browse/QTBUG-46434) QQuickPaintedItem crash when toggling antialiasing
* [QTBUG-132163](https://qt-project.atlassian.net/browse/QTBUG-132163) Animator crashes when paused is used
* [QTBUG-134749](https://qt-project.atlassian.net/browse/QTBUG-134749) Various ASAN crashes in QJSEngine
* [QTBUG-144092](https://qt-project.atlassian.net/browse/QTBUG-144092) Cannot assign to list of inline component type when
using multiple qml engines
* [QTBUG-139255](https://qt-project.atlassian.net/browse/QTBUG-139255) [Regr: 6.8.2->6.9.0] Focus restore problem on closing
popup
* [QTBUG-139426](https://qt-project.atlassian.net/browse/QTBUG-139426) qmlformat adds extra newline for components only
containing id property
* [QTBUG-144182](https://qt-project.atlassian.net/browse/QTBUG-144182) "ERROR: AddressSanitizer: stack-use-after-return" in
tst_qqmlnotifier destruction
* [QTBUG-141347](https://qt-project.atlassian.net/browse/QTBUG-141347) Quick Gallery shows only blank screen
* [QTBUG-132135](https://qt-project.atlassian.net/browse/QTBUG-132135) qt.qml.gc.allocatorStats is confused in incremental gc
mode
* [QTBUG-144143](https://qt-project.atlassian.net/browse/QTBUG-144143) [REG 6.10 -> 6.11] QtQuick: cursor shape is applied for
disabled and/or invisible items
* [QTBUG-144231](https://qt-project.atlassian.net/browse/QTBUG-144231) tst_qtquickview_basic (Failed)
* [QTBUG-136650](https://qt-project.atlassian.net/browse/QTBUG-136650) Not possible to have a frameless QML ColorDialog
* [QTBUG-142132](https://qt-project.atlassian.net/browse/QTBUG-142132) QML TextField advertises AT-SPI "editable text"
interface, but does not implement it, cannot set text
* [QTBUG-143473](https://qt-project.atlassian.net/browse/QTBUG-143473) Memory leak due to changes to garbage collection
introduced in 6.10.0
* [QTBUG-144446](https://qt-project.atlassian.net/browse/QTBUG-144446) QtQ4A Kotlin-based examples do not build with Gradle 9
* [QTBUG-142723](https://qt-project.atlassian.net/browse/QTBUG-142723) Crash in QQuickWindowPrivate::polishItems
* [QTBUG-105906](https://qt-project.atlassian.net/browse/QTBUG-105906) [Reg 5.15.5->5.15.6] The fix for the QTBUG-89736 causes
a crash
* [QTBUG-72910](https://qt-project.atlassian.net/browse/QTBUG-72910) Running on a dangling pointer, when deleting the
activeFocusItem inside of QQuickItem::updatePolish
* [QTBUG-115140](https://qt-project.atlassian.net/browse/QTBUG-115140) qtdeclarative -unity-build-batch-size 100000 fails
* [QTBUG-127605](https://qt-project.atlassian.net/browse/QTBUG-127605) [QtQuick.Dialogs/Wayland] Native FileDialog does not
respect Qt.ApplicationModal flag
* [QTBUG-136447](https://qt-project.atlassian.net/browse/QTBUG-136447) Blacklist tst_qquickiconimage tests for Windows 11 24h2
* [QTBUG-133586](https://qt-project.atlassian.net/browse/QTBUG-133586) F2 shortcut or Ctrl+Click in qml files sometimes leads
to build dir instead of source and sometimes does absolutly nothing
* [QTBUG-135286](https://qt-project.atlassian.net/browse/QTBUG-135286) Qml Property Cache heap-use-after-free
* [QTBUG-118610](https://qt-project.atlassian.net/browse/QTBUG-118610) ShaderEffectSource in recursive mode with multisampling
is broken
* [QTBUG-133858](https://qt-project.atlassian.net/browse/QTBUG-133858) tst_QQuickMenu::contextMenuKeyboard is flaky
* [QTBUG-137400](https://qt-project.atlassian.net/browse/QTBUG-137400) tst_qquickcontextmenu::menuItemShouldntTriggerOnRelease
is flaky
* [QTBUG-137144](https://qt-project.atlassian.net/browse/QTBUG-137144) a11y: AT-SPI "Locale" Accessible property not supported
* [QTBUG-132268](https://qt-project.atlassian.net/browse/QTBUG-132268) SelectionRectangle is fiddly to get working by default
* [QTBUG-117526](https://qt-project.atlassian.net/browse/QTBUG-117526) QQuickStylePrivate::fallbackStyle has the wrong value
when using run-time style selection and the fallback style is imported
via the style's qmldir
* [QTBUG-136709](https://qt-project.atlassian.net/browse/QTBUG-136709) Style import triggers style change
* [QTBUG-132108](https://qt-project.atlassian.net/browse/QTBUG-132108) addApplicationFontFromData behaves abnormally after
removeAllApplicationFonts.
* [QTBUG-109279](https://qt-project.atlassian.net/browse/QTBUG-109279) JS array vs QVariantList mixup
* [QTBUG-137554](https://qt-project.atlassian.net/browse/QTBUG-137554) qml: list qml --> c++ editing crashes/has no effect
* [QTBUG-133315](https://qt-project.atlassian.net/browse/QTBUG-133315) qmlformat can still insert extra spaces in user code
* [QTBUG-123386](https://qt-project.atlassian.net/browse/QTBUG-123386) QmlFormat. Incorrect handling of some comments
* [QTBUG-137116](https://qt-project.atlassian.net/browse/QTBUG-137116) Incorrect Semantic Highlighting for QML Property Chains
* [QTBUG-138155](https://qt-project.atlassian.net/browse/QTBUG-138155) qt_generate_deploy_qml_app_script: Error for space in
output name
* [QTBUG-87708](https://qt-project.atlassian.net/browse/QTBUG-87708) [Reg 5.15.0 -> 5.15.1] header's width isn't resized to
window's width when Layout is used
* [QTBUG-137946](https://qt-project.atlassian.net/browse/QTBUG-137946) qmllint: duplicate-property-binding
* [QTBUG-138164](https://qt-project.atlassian.net/browse/QTBUG-138164) Coffee Machine: qmllint warnings
* [QTBUG-138565](https://qt-project.atlassian.net/browse/QTBUG-138565) "Cannot generate qmltypes file" when trying to run in-
app purchase demo app on Android
* [QTBUG-138189](https://qt-project.atlassian.net/browse/QTBUG-138189) To Do List: qmllint warnings
* [QTBUG-138553](https://qt-project.atlassian.net/browse/QTBUG-138553) QmlTableModel complex types don't work as documented:
Remove setters
* [QTBUG-138173](https://qt-project.atlassian.net/browse/QTBUG-138173) Lightning Viewer: qmllint warnings
* [QTBUG-138703](https://qt-project.atlassian.net/browse/QTBUG-138703) QmlTableModel and QmlTreeModel should be merged where
possible.
* [QTBUG-138704](https://qt-project.atlassian.net/browse/QTBUG-138704) QmlTreeModel misses API for insertRow()
* [QTBUG-135407](https://qt-project.atlassian.net/browse/QTBUG-135407) [Scene Graph - Graph App] Segmentation Fault
* [QTBUG-138188](https://qt-project.atlassian.net/browse/QTBUG-138188) Thermostat: qmllint warnings
* [QTBUG-138901](https://qt-project.atlassian.net/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-139026](https://qt-project.atlassian.net/browse/QTBUG-139026) Scrollbar size jumps during drag due to dynamic item
heights
* [QTBUG-139240](https://qt-project.atlassian.net/browse/QTBUG-139240) qmllint should not warn about accessing properties from
QQmlPropertyMap
* [QTBUG-139211](https://qt-project.atlassian.net/browse/QTBUG-139211) tst_qquickpopup (Failed)
* [QTBUG-139552](https://qt-project.atlassian.net/browse/QTBUG-139552) tst_qquickmenu: Test case loadMenuAsynchronously fails
due to warning
* [QTBUG-131695](https://qt-project.atlassian.net/browse/QTBUG-131695) tst_qquickpopup tst_QQuickPopup::fadeDimmer is flaky
* [QTBUG-139560](https://qt-project.atlassian.net/browse/QTBUG-139560) Access functions are documented even when their
properties are not
* [QTBUG-118532](https://qt-project.atlassian.net/browse/QTBUG-118532) tst_qquickpopup::doubleClickInMouseArea and overlay are
flaky on android
* [QTBUG-121518](https://qt-project.atlassian.net/browse/QTBUG-121518) DOM refactoring p2
* [QTBUG-139688](https://qt-project.atlassian.net/browse/QTBUG-139688) Public Java Classes Documentation Bugs
* [QTBUG-114718](https://qt-project.atlassian.net/browse/QTBUG-114718) [Tests] tst_QQuickPopup fails
* [QTBUG-139941](https://qt-project.atlassian.net/browse/QTBUG-139941) DelegateModelAccess.ReadWrite should allow writing to
arrays and sequences as models
* [QTBUG-138947](https://qt-project.atlassian.net/browse/QTBUG-138947) QProgressBar completely blank on macOS 26
* [QTBUG-138942](https://qt-project.atlassian.net/browse/QTBUG-138942) Mac style (Widget and Quick) has issues on macOS 26
* [QTBUG-139320](https://qt-project.atlassian.net/browse/QTBUG-139320) QQ4A - Buffer Overflow crash in application project
* [QTBUG-139976](https://qt-project.atlassian.net/browse/QTBUG-139976) svgtoqml commandline tool requires window manager
* [QTBUG-140170](https://qt-project.atlassian.net/browse/QTBUG-140170) [6.10 REG] ASSERT failure in QQuickWindow: "Called
object is not of the correct type (class destructor may have already
run)"
* [QTBUG-140187](https://qt-project.atlassian.net/browse/QTBUG-140187) Missing dependencies for VectorImage when deploying on
Android
* [QTBUG-137944](https://qt-project.atlassian.net/browse/QTBUG-137944) qmlformat moves qmlint comments, removes function
argument annotations
* [QTBUG-140041](https://qt-project.atlassian.net/browse/QTBUG-140041) ids are not properly resolved when using cachegen
* [QTBUG-138946](https://qt-project.atlassian.net/browse/QTBUG-138946) QSlider issues on macOS 26
* [QTBUG-140364](https://qt-project.atlassian.net/browse/QTBUG-140364) QQuickGradientStop does not use default position when it
is not provided
* [QTBUG-139591](https://qt-project.atlassian.net/browse/QTBUG-139591) tst_qtquickview_basic times out
* [QTBUG-140242](https://qt-project.atlassian.net/browse/QTBUG-140242) QSGThreadedRenderLoop cleanup with QQuickWindow
swapchain still alive, this should not happen.
* [QTBUG-138022](https://qt-project.atlassian.net/browse/QTBUG-138022) Ui components behind top and bottom bar on Qt Examples
* [QTBUG-140851](https://qt-project.atlassian.net/browse/QTBUG-140851) Doc: Add Qt Academy course links to documentation
* [QTBUG-138471](https://qt-project.atlassian.net/browse/QTBUG-138471) QString::arg() convert floating type to integer
* [QTBUG-139269](https://qt-project.atlassian.net/browse/QTBUG-139269) REG[6.8.3->6.8.4] Nested Popup with an exit transition
causes crash on close
* [QTBUG-138918](https://qt-project.atlassian.net/browse/QTBUG-138918) Memory continuously increases when loading/unloading QML
components with Loader
* [QTBUG-138744](https://qt-project.atlassian.net/browse/QTBUG-138744) FluentWinUI3 ComboBox popup is not resized when
dynamically reloading the model
* [QTBUG-138545](https://qt-project.atlassian.net/browse/QTBUG-138545) QUrls passed from C++ to QML seem to be compared by
reference instead of value
* [QTBUG-140899](https://qt-project.atlassian.net/browse/QTBUG-140899) [REG 6.9.3 -> 6.10.0] Qt6Cored.dll Debug errors
(Microsoft Visual C++ Runetime Library)
* [QTBUG-133755](https://qt-project.atlassian.net/browse/QTBUG-133755) tst_customization has an unusually long runtime (several
hours)
* [QTBUG-140645](https://qt-project.atlassian.net/browse/QTBUG-140645) qmlls: provide fallback for semantic highlighting on
invalid files
* [QTBUG-137203](https://qt-project.atlassian.net/browse/QTBUG-137203) Request to add an option for case sensitivity in
QNetworkRequest::setRawHeader().
* [QTBUG-140675](https://qt-project.atlassian.net/browse/QTBUG-140675) svgtoqml commandline tool breaks compilation over ssh
* [QTBUG-100377](https://qt-project.atlassian.net/browse/QTBUG-100377) [REG 5.15 -> 6.2] Date.parse() can't handle some dates
on Qt 6 but works in Qt 5
* [QTBUG-40856](https://qt-project.atlassian.net/browse/QTBUG-40856) MouseArea containsMouse flag is not reset on Touch Screen
* [QTBUG-141430](https://qt-project.atlassian.net/browse/QTBUG-141430) tst_HoverHandler::twoHandlersTwoTouches is flaky
* [QTBUG-141110](https://qt-project.atlassian.net/browse/QTBUG-141110) RectangularShadow: be able to set individual radii
* [QTBUG-141365](https://qt-project.atlassian.net/browse/QTBUG-141365) android/QtQuickView.java:146: error: cannot find symbol
windowReference()
* [QTBUG-133302](https://qt-project.atlassian.net/browse/QTBUG-133302) ContextMenu opened on TextField sometimes closes
immediately
* [QTBUG-141398](https://qt-project.atlassian.net/browse/QTBUG-141398) FAIL!  :
tst_QQuickContextMenu::Basic::menuItemShouldntTriggerOnRelease()
Compared values are not the same
* [QTBUG-141406](https://qt-project.atlassian.net/browse/QTBUG-141406) tst_QQuickContextMenu::menuItemShouldntTriggerOnRelease()
is flaky
* [QTBUG-141385](https://qt-project.atlassian.net/browse/QTBUG-141385) qmllint: internal setting values only support single
paths
* [QTBUG-139676](https://qt-project.atlassian.net/browse/QTBUG-139676) [a11y] "Switch" role is missing
* [QTBUG-140134](https://qt-project.atlassian.net/browse/QTBUG-140134) Ugly spin boxes on macOS 26 (up/down buttons)
* [QTBUG-89033](https://qt-project.atlassian.net/browse/QTBUG-89033) Do not use versioned QML imports in Qt 6 documentation &
examples
* [QTBUG-141465](https://qt-project.atlassian.net/browse/QTBUG-141465) Reconfigure: CMake wants to use Linguist tools that
haven't been built yet
* [QTBUG-140504](https://qt-project.atlassian.net/browse/QTBUG-140504) a11y: QAccessibleText::getTextAfterOffset implementation
for QTextEdit and QML TextEdit is incorrect
* [QTBUG-140769](https://qt-project.atlassian.net/browse/QTBUG-140769) a11y: Scrollbar orientation not reported via AT-SPI (and
other a11y APIs)
* [QTBUG-140073](https://qt-project.atlassian.net/browse/QTBUG-140073) Missing symbols in Java files in qtdeclarative
* [QTBUG-95788](https://qt-project.atlassian.net/browse/QTBUG-95788) Singletons with clearComponentCache don't fully work
* [QTBUG-140340](https://qt-project.atlassian.net/browse/QTBUG-140340) [REG: 5->6] Input event delivery performance regression
in Qt 6
* [QTBUG-141665](https://qt-project.atlassian.net/browse/QTBUG-141665) Doc: Suppress "No output generated for ..."
* [QTBUG-130152](https://qt-project.atlassian.net/browse/QTBUG-130152) Documentation of QML elements does not show the complete
inheritance
* [QTBUG-133449](https://qt-project.atlassian.net/browse/QTBUG-133449) VxWorks doesn't have JIT enabled
* [QTBUG-53987](https://qt-project.atlassian.net/browse/QTBUG-53987) Cursor is not updated on mouse wheel over flickable
* [QTBUG-141543](https://qt-project.atlassian.net/browse/QTBUG-141543) Doc: Overhaul the Positioning with Anchors topic
* [QTBUG-139131](https://qt-project.atlassian.net/browse/QTBUG-139131) Reg->6.9.1: ASSERT failure in
QCoreApplication::sendEvent() (Debug build) when closing application in
Qt 6.9.1
* [QTBUG-
142016](https://qt-project.atlassian.net/browse/QTBUG-142016) tst_QQuickMessageDialogImpl::resultReflectsLastStandardButtonPres
sed blocking unrelated changes
* [QTBUG-115179](https://qt-project.atlassian.net/browse/QTBUG-115179) Clip optimization in
QQuickDeliveryAgentPrivate::pointerTargets is too aggressive
* [QTBUG-87459](https://qt-project.atlassian.net/browse/QTBUG-87459) Quick/Action: Cannot use an icon with the original colors
* [QTBUG-142189](https://qt-project.atlassian.net/browse/QTBUG-142189) QtQuick Switch mouse/touch tests fail related to center
point for macOS style
* [QTBUG-142186](https://qt-project.atlassian.net/browse/QTBUG-142186) MetaObject change in DelegateModel leads to crash in
Plasma
* [QTBUG-141854](https://qt-project.atlassian.net/browse/QTBUG-141854) qmllint: warn about defining properties that already
exist and shadowing
* [QTBUG-137440](https://qt-project.atlassian.net/browse/QTBUG-137440) qt6-declarative qmlcachegen non-determinism
* [QTBUG-142145](https://qt-project.atlassian.net/browse/QTBUG-142145) Menu and other Popup items do not work in XR
* [QTBUG-142203](https://qt-project.atlassian.net/browse/QTBUG-142203) QQuickRectangleShape doesn't update on size changes
* [QTBUG-140181](https://qt-project.atlassian.net/browse/QTBUG-140181) Build failure in QtDeclarative with latest nightly
libc++
* [QTBUG-142436](https://qt-project.atlassian.net/browse/QTBUG-142436) QmlPreview's window handling is unreliable
* [QTBUG-142792](https://qt-project.atlassian.net/browse/QTBUG-142792) svgtoqml-dependent examples fail to build on macOS in Qt
6.11 snapshot package
* [QTBUG-143071](https://qt-project.atlassian.net/browse/QTBUG-143071) Sporadic crashes on
QSGDistanceFieldGlyphCache::release()
* [QTBUG-129176](https://qt-project.atlassian.net/browse/QTBUG-129176) [REG Qt 6.7.2-> 6.8.0-beta4] Crash in
QRawFont::pathForGlyph() / black screen
* [QTBUG-67720](https://qt-project.atlassian.net/browse/QTBUG-67720) CMake: Avoid to deliver Qt Labs binarys in an apk
* [QTBUG-130899](https://qt-project.atlassian.net/browse/QTBUG-130899) Disabled item does not disable its HoverHandler
* [QTBUG-143208](https://qt-project.atlassian.net/browse/QTBUG-143208) Fix QTestAccessibility various problems
* [QTBUG-35598](https://qt-project.atlassian.net/browse/QTBUG-35598) QtQuick Controls TextField and TextArea miss mouse
context menu
* [QTBUG-143282](https://qt-project.atlassian.net/browse/QTBUG-143282) qdoc: \summary directive apparently causes mixup in the
webxml  generator
* [QTBUG-143312](https://qt-project.atlassian.net/browse/QTBUG-143312) tst_qquickcanvasitem keeps failing on qnx with timeouts
* [QTBUG-143313](https://qt-project.atlassian.net/browse/QTBUG-143313) qmllint -  warnings about shadowing methods need to
silenced until they become actionable
* [QTBUG-143483](https://qt-project.atlassian.net/browse/QTBUG-143483) Document new qmllint warnings (qmlShadow,
qmlPropertyOverride, qmlIdShadowsMember, ...)
* [QTBUG-140200](https://qt-project.atlassian.net/browse/QTBUG-140200) Modal QML Popup not modal to a11y layer
* [QTBUG-136120](https://qt-project.atlassian.net/browse/QTBUG-136120) Qml Runtime fails to correct escape -a after --
* [QTBUG-143361](https://qt-project.atlassian.net/browse/QTBUG-143361) QML Connections component crashes if creating many
Connections that target the same instance
* [QTBUG-142386](https://qt-project.atlassian.net/browse/QTBUG-142386) openSUSE 16.0 qtdeclarative -
tst_QQuickColorDialogImpl::moveColorPickerHandle()
'qAbs(colorPicker->color().green() - QColorConstants::Cyan.green()) < 3'
returned FALSE
* [QTBUG-143800](https://qt-project.atlassian.net/browse/QTBUG-143800) source value 8 is obsolete and will be removed in a
future release
* [QTBUG-143701](https://qt-project.atlassian.net/browse/QTBUG-143701) tst_QQuickContextMenu::textControlsMenuKey is flaky on
several platforms
* [QTBUG-142384](https://qt-project.atlassian.net/browse/QTBUG-142384) openSUSE 16.0 qtdeclarative -
tst_QQuickFontDialogImpl::clickAroundInTheFamilyListView()
'selectedFontSpyCount == 1' returned FALSE. (LOOP INDEX 5, EXPECTED 1,
ACTUAL 2, FONT Adwaita Mono)
* [QTBUG-143916](https://qt-project.atlassian.net/browse/QTBUG-143916) Fix QDoc warnings for Qt 6.11
* [QTBUG-108005](https://qt-project.atlassian.net/browse/QTBUG-108005) PathView distorts TouchEvents
* [QTBUG-141701](https://qt-project.atlassian.net/browse/QTBUG-141701) [a11y] App language is not transparent to Screen Reader
* [QTBUG-143675](https://qt-project.atlassian.net/browse/QTBUG-143675) Mismatch between logic and docs of
QtQuickViewContent.connectSignalListener
* [QTBUG-141950](https://qt-project.atlassian.net/browse/QTBUG-141950) make CompileError print character number
* [QTBUG-144451](https://qt-project.atlassian.net/browse/QTBUG-144451) QDoc: \include snippet matching uses substring instead
of exact name
* [QTBUG-143978](https://qt-project.atlassian.net/browse/QTBUG-143978) [REG 6.8.3 - 6.10.1] Sporadic crashes at
QQuickBasicTheme::initialize()
* [QTBUG-
144397](https://qt-project.atlassian.net/browse/QTBUG-144397) tst_qquickstyle::defaultPaletteIsUpdatedWhenChangingColorScheme()
crashes on Ubuntu

### qtactiveqt
* [QTBUG-134098](https://qt-project.atlassian.net/browse/QTBUG-134098) dumpcpp puts native Qt types inside a custom namespace
* [QTBUG-136512](https://qt-project.atlassian.net/browse/QTBUG-136512) [Reg 6.8.3 -> 6.9.0] dumpcpp's output is uncompilable
due to missing namespaces
* [QTBUG-137347](https://qt-project.atlassian.net/browse/QTBUG-137347) dumpcpp skips namespace and creates syntaxes errors
* [QTBUG-139731](https://qt-project.atlassian.net/browse/QTBUG-139731) Axserver crashes on exit if command line arguments
passed after standard Qt arguments (removed by QApp)
* [QTBUG-142519](https://qt-project.atlassian.net/browse/QTBUG-142519) error C2338: static_assert failed: 'dumpcpp should
generate the same version as moc'
* [QTBUG-140884](https://qt-project.atlassian.net/browse/QTBUG-140884) dumpcpp generates incomplete .h and .cpp
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtmultimedia
* [QTBUG-137150](https://qt-project.atlassian.net/browse/QTBUG-137150) Assertion hit when unplugging microphone device while
recording
* [QTBUG-137308](https://qt-project.atlassian.net/browse/QTBUG-137308) [Reg B2Qt 6.7.3 -> 6.8.3] glupload not supported in
GStreamer pipeline
* [QTBUG-137360](https://qt-project.atlassian.net/browse/QTBUG-137360) Qt multimedia compilation error windows 32 bit
* [QTBUG-120693](https://qt-project.atlassian.net/browse/QTBUG-120693) Corrupt JPEG data
* [QTBUG-127905](https://qt-project.atlassian.net/browse/QTBUG-127905) Changing SoundEffect source makes the app hang
* [QTBUG-126602](https://qt-project.atlassian.net/browse/QTBUG-126602) wasm: screenshot does not work
* [QTBUG-136145](https://qt-project.atlassian.net/browse/QTBUG-136145) Qt Spatial Audio: Add alt texts
* [QTBUG-137586](https://qt-project.atlassian.net/browse/QTBUG-137586) [pipewire] rare crashes on exit
* [QTBUG-137173](https://qt-project.atlassian.net/browse/QTBUG-137173) Windows native multimedia backend does not agree with
Windows Media Player when dealing with rotated video
* [QTBUG-136921](https://qt-project.atlassian.net/browse/QTBUG-136921) WebAssembly MediaPlayer no longer works with http urls
* [QTBUG-136676](https://qt-project.atlassian.net/browse/QTBUG-136676) Linking against static FFmpeg that is built with OpenSSL
support fails
* [QTBUG-136802](https://qt-project.atlassian.net/browse/QTBUG-136802) Linking against static FFmpeg that has VAAPI support
enabled causes build to fail
* [QTBUG-137973](https://qt-project.atlassian.net/browse/QTBUG-137973) QMediaPlayer example crashing while changing audio
device output
* [QTBUG-138060](https://qt-project.atlassian.net/browse/QTBUG-138060) Unable to build: no type named 'lock_guard' in namespace
'std' on macos ventura
* [QTBUG-98145](https://qt-project.atlassian.net/browse/QTBUG-98145) Android: Avoid empty file format on the AudioRecorder app
* [QTBUG-138059](https://qt-project.atlassian.net/browse/QTBUG-138059) [REG 6.9.0-6.9.1] [windows] Strange Qt warning on
QAudioSource::start() when non-default sample rate is used
* [QTBUG-138197](https://qt-project.atlassian.net/browse/QTBUG-138197) Crash in
QtPipeWire::QAudioContextManager::handleMetadata
* [QTBUG-104515](https://qt-project.atlassian.net/browse/QTBUG-104515) Documentation for QML's CaptureSession lacks
camera.start() entry
* [QTBUG-138248](https://qt-project.atlassian.net/browse/QTBUG-138248) Crash in QtPipeWire::SpaObjectAudioFormat::parse
* [QTBUG-130636](https://qt-project.atlassian.net/browse/QTBUG-130636) FFmpeg: QCamera::FlashOn is unreliable
* [QTBUG-134607](https://qt-project.atlassian.net/browse/QTBUG-134607) Video playback crash when setting QQuickWindow
GraphicsAPI to Vulkan
* [QTBUG-138414](https://qt-project.atlassian.net/browse/QTBUG-138414) FFmpeg Plugin: Improve usability on different RHI
backend configurations
* [QTBUG-136151](https://qt-project.atlassian.net/browse/QTBUG-136151) Qt Multimedia: Add alt texts
* [QTBUG-138952](https://qt-project.atlassian.net/browse/QTBUG-138952) tst_qaudiosink: start_afterStopAndReset() crashes on
macOS
* [QTBUG-139549](https://qt-project.atlassian.net/browse/QTBUG-139549) Qt multimedia compilation error windows 32 bit
* [QTBUG-138590](https://qt-project.atlassian.net/browse/QTBUG-138590) Incorrect Call to QAudioOutput::setVolume
* [QTBUG-124562](https://qt-project.atlassian.net/browse/QTBUG-124562) Exposure compensation (setExposureCompensation) doesn't
work with the example app
* [QTBUG-139773](https://qt-project.atlassian.net/browse/QTBUG-139773) Crash in MediaPlayer in qtdice demo
* [QTBUG-139993](https://qt-project.atlassian.net/browse/QTBUG-139993) ASSERT in QRtAudioEngine::runRtCommand
* [QTBUG-139681](https://qt-project.atlassian.net/browse/QTBUG-139681) Camera widgets record button crashes application on
linux
* [QTBUG-139210](https://qt-project.atlassian.net/browse/QTBUG-139210) No qtmultimedia.tags file generated
* [QTBUG-140431](https://qt-project.atlassian.net/browse/QTBUG-140431) apalis-imx6: media Player example fails to play video
* [QTBUG-140122](https://qt-project.atlassian.net/browse/QTBUG-140122) Background Color Difference During Video Playback
Between Windows Media Player and Qt Media Player Example
* [QTBUG-140451](https://qt-project.atlassian.net/browse/QTBUG-140451) TS video playback: no audio on Windows, corrupted audio
on macOS
* [QTBUG-138452](https://qt-project.atlassian.net/browse/QTBUG-138452) Misleading QML audioDevice.mode enum documentation.
* [QTBUG-140646](https://qt-project.atlassian.net/browse/QTBUG-140646) Error pops up at the end of playing audio file (mp4a
with ALAC codec) recorded with audio recorder example
* [QTBUG-140558](https://qt-project.atlassian.net/browse/QTBUG-140558) Pulseaudio leaks
* [QTBUG-140658](https://qt-project.atlassian.net/browse/QTBUG-140658) audio recorder example: AudioLevel element in gui does
nothing
* [QTBUG-124734](https://qt-project.atlassian.net/browse/QTBUG-124734) multimedia player example does not obey palette
* [QTBUG-126028](https://qt-project.atlassian.net/browse/QTBUG-126028) AudioSource example: changing source has no effect
* [QTBUG-140086](https://qt-project.atlassian.net/browse/QTBUG-140086) Streaming an IP camera over HTTP fails randomly
* [QTBUG-140462](https://qt-project.atlassian.net/browse/QTBUG-140462) QML Video Recorder example: qmllint warnings
* [QTBUG-141250](https://qt-project.atlassian.net/browse/QTBUG-141250) "Easy Effects Source" device doesn't show up
* [QTBUG-141376](https://qt-project.atlassian.net/browse/QTBUG-141376) declarative-camera, regression: Switching camera device
no longer keeps camera active
* [QTBUG-129152](https://qt-project.atlassian.net/browse/QTBUG-129152) Camera flash not working on iOS
* [QTBUG-137950](https://qt-project.atlassian.net/browse/QTBUG-137950) Application crash when loading a camera CaptureSession
on Windows
* [QTBUG-134554](https://qt-project.atlassian.net/browse/QTBUG-134554) gstreamer-pipeline does not work if source is set
initially
* [QTBUG-141615](https://qt-project.atlassian.net/browse/QTBUG-141615) Id conflict in QQuickImageProvider when Qt Multimedia
module is imported
* [QTBUG-141661](https://qt-project.atlassian.net/browse/QTBUG-141661) [macOS] Invalid preferredFormat is returned for iMac's
built-in audio device
* [QTBUG-141840](https://qt-project.atlassian.net/browse/QTBUG-141840) QSoundEffect hangs when switching source url
* [QTBUG-141789](https://qt-project.atlassian.net/browse/QTBUG-141789) [reg 6.7.3->6.8/9/10] Audio Output Example freezes
* [QTBUG-141852](https://qt-project.atlassian.net/browse/QTBUG-141852) tst_qaudiosink: Cannot open int32 audio stream on CI
* [QTBUG-141787](https://qt-project.atlassian.net/browse/QTBUG-141787) QAudioOutput cannot recover from interrupted RDP session
* [QTBUG-141836](https://qt-project.atlassian.net/browse/QTBUG-141836) No audio device detected when using ffmpeg Qt6
multimedia backend
* [QTBUG-140938](https://qt-project.atlassian.net/browse/QTBUG-140938) Reg->6.10.0/Manjaro Linux: QtMultimedia shows no devices
apparently because pipewire-audio is not installed by default
* [QTBUG-135598](https://qt-project.atlassian.net/browse/QTBUG-135598) [Windows] Sporadic crashes when call
QVideoFrame::toImage() from working thread
* [QTBUG-131107](https://qt-project.atlassian.net/browse/QTBUG-131107) QVideoFrame::toImage / qImageFromVideoFrame not safe to
call from worker thread
* [QTBUG-142166](https://qt-project.atlassian.net/browse/QTBUG-142166) QAudio::convertVolume missing
* [QTBUG-142140](https://qt-project.atlassian.net/browse/QTBUG-142140) VideoOutput will report an error and be invisible when
MediaPlayer plays the video for the first time.
* [QTBUG-141662](https://qt-project.atlassian.net/browse/QTBUG-141662) qmlvideo example crashes on startup
* [QTBUG-142503](https://qt-project.atlassian.net/browse/QTBUG-142503) Fix doc links in Qt Multimedia
* [QTBUG-142695](https://qt-project.atlassian.net/browse/QTBUG-142695) Current #import directives rely on case-insensitive
macOS file system
* [QTBUG-138223](https://qt-project.atlassian.net/browse/QTBUG-138223) QML Video doesn't autoPlay after source change
* [QTBUG-142242](https://qt-project.atlassian.net/browse/QTBUG-142242) Crash in ffmpeg plugin: ASSERT: "context->free ==
deleteHwFrameContextData"
* [QTBUG-142694](https://qt-project.atlassian.net/browse/QTBUG-142694) [REG 6.8.3-6.10.1] Sporadic crashes on
QSoundEffectPrivateWithPlayer::play
* [QTBUG-142743](https://qt-project.atlassian.net/browse/QTBUG-142743) QtMultimediaPrivate::QRtAudioEngine::getEngineFor crash
with remote connection
* [QTBUG-142480](https://qt-project.atlassian.net/browse/QTBUG-142480) Random assertion failure at QPlatformAudioIOStream
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
* [QTBUG-144222](https://qt-project.atlassian.net/browse/QTBUG-144222) QML MediaPlayer triggers property shadowing warning
* [QTBUG-144097](https://qt-project.atlassian.net/browse/QTBUG-144097) [Regression] iOS camera stops emitting frames after
short delay
* [QTBUG-131154](https://qt-project.atlassian.net/browse/QTBUG-131154) [Boot2Qt] Slow Video and Camera Rendering in Multimedia
Examples
* [QTBUG-135325](https://qt-project.atlassian.net/browse/QTBUG-135325) [Boot2Qt] The application freezes and eventually crashes
when video recording stops
* [QTBUG-127733](https://qt-project.atlassian.net/browse/QTBUG-127733) tst_QAudioSink::pullResumeFromUnderrun() failed on
Ubuntu 24.04 offscreen and X11
* [QTBUG-134645](https://qt-project.atlassian.net/browse/QTBUG-134645) SoundEffect decoding error
* [QTBUG-117099](https://qt-project.atlassian.net/browse/QTBUG-117099) Video jerks when playing (Windows backend)
* [QTBUG-130272](https://qt-project.atlassian.net/browse/QTBUG-130272) Failed to start pulseaudio sink and source on OpenSuse
CI
* [QTBUG-26504](https://qt-project.atlassian.net/browse/QTBUG-26504) QAudioOutput resume() fails regularly using pulseaudio
backend
* [QTBUG-133914](https://qt-project.atlassian.net/browse/QTBUG-133914) FFmpeg plugin tests may fail to build on Linux and
Android
* [QTBUG-138000](https://qt-project.atlassian.net/browse/QTBUG-138000) tst_QAudioSource::pull fails on ubuntu-22.04-x11-tests
* [QTBUG-137984](https://qt-project.atlassian.net/browse/QTBUG-137984) Unable to compile QtMultimedia Debug under PiOS
* [QTBUG-127560](https://qt-project.atlassian.net/browse/QTBUG-127560) maroon demo lags when enabling sounds
* [QTBUG-131912](https://qt-project.atlassian.net/browse/QTBUG-131912) [soundeffect] wrong playback on windows
* [QTBUG-
138507](https://qt-project.atlassian.net/browse/QTBUG-138507) qImageFromVideoFrame_doesNotCrash_whenCalledWithEvenAndOddSizedFr
ames fails on CI due to software conversion
* [QTBUG-138901](https://qt-project.atlassian.net/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-139660](https://qt-project.atlassian.net/browse/QTBUG-139660) QTextToSpeech WinRT backend stops speaking after the
first word in Qt 6.9.2
* [QTBUG-139560](https://qt-project.atlassian.net/browse/QTBUG-139560) Access functions are documented even when their
properties are not
* [QTBUG-140398](https://qt-project.atlassian.net/browse/QTBUG-140398) mediaplayerbackend
setActiveSubtitleTrack_switchesSubtitles fails on macOS 26
* [QTBUG-139767](https://qt-project.atlassian.net/browse/QTBUG-139767) AudioSource example crash
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-135922](https://qt-project.atlassian.net/browse/QTBUG-135922) QMediaPlayer::mediaStatusChanged no longer emits
EndOfMedia on video completion
* [QTBUG-135618](https://qt-project.atlassian.net/browse/QTBUG-135618) [MacOS] Sporadic crashes when call
QVideoFrame::toImage()
* [QTBUG-143062](https://qt-project.atlassian.net/browse/QTBUG-143062) [darwin] Sporadic crashes on QMediaRecorder::record
(recording an audio)
* [QTBUG-142762](https://qt-project.atlassian.net/browse/QTBUG-142762) Slow QSoundEffect initialization
* [QTBUG-137857](https://qt-project.atlassian.net/browse/QTBUG-137857) Regression in audio playback causing significant delay
at start and blocking main thread
* [QTBUG-137845](https://qt-project.atlassian.net/browse/QTBUG-137845) [Boot2Qt] The content of MPEG video file is corrupted
when playing on i.MX 8M Mini EVK
* [QTBUG-143570](https://qt-project.atlassian.net/browse/QTBUG-143570) Regression in Qt 6.10+: PipeWire backend has incomplete
support for virtual audio devices
* [QTBUG-143627](https://qt-project.atlassian.net/browse/QTBUG-143627) Incorrect usage of qFuzzyCompare() abounds in Qt source
[QtMulitmedia]
* [QTBUG-96239](https://qt-project.atlassian.net/browse/QTBUG-96239) Document CMake component in CMake function documentation

### qttools
* [QTBUG-135694](https://qt-project.atlassian.net/browse/QTBUG-135694) QDoc: no warning about missing \class documentation
* [QTBUG-96693](https://qt-project.atlassian.net/browse/QTBUG-96693) QUiLoader resolves  wrong buddy when UI is loaded twice
* [QTBUG-137019](https://qt-project.atlassian.net/browse/QTBUG-137019) QML type inheritance checks need warnings and
documentation
* [QTBUG-137458](https://qt-project.atlassian.net/browse/QTBUG-137458) Update 'QML Documentation Style" page for \qmlenum
* [QTBUG-138072](https://qt-project.atlassian.net/browse/QTBUG-138072) Remove traces of <type> argument to \page command from
documentation
* [QTBUG-136158](https://qt-project.atlassian.net/browse/QTBUG-136158) Qt UI Tools: Add alt texts
* [QTBUG-132832](https://qt-project.atlassian.net/browse/QTBUG-132832) lupdate generates errors for tr() marked strings in
template specializations
* [QTBUG-138557](https://qt-project.atlassian.net/browse/QTBUG-138557) [REG 6.10] qdoc cannot resolve link to deprecated
q[v]snprintf
* [QTBUG-138492](https://qt-project.atlassian.net/browse/QTBUG-138492) qdoc: Snippet indentation issues
* [QTBUG-137569](https://qt-project.atlassian.net/browse/QTBUG-137569) make qttools configure more user friendly on windows
* [QTBUG-138870](https://qt-project.atlassian.net/browse/QTBUG-138870) QDoc fails to parse templated using statement with
default value for a template arg
* [QTBUG-138887](https://qt-project.atlassian.net/browse/QTBUG-138887) [REG 5.13 → 5.14] \overload lastIndexOf() in qstring.cpp
renders lastIndexOf() as a non-link
* [QTBUG-138586](https://qt-project.atlassian.net/browse/QTBUG-138586) Clarify behavior of \overload if main method has
arguments
* [QTBUG-138910](https://qt-project.atlassian.net/browse/QTBUG-138910) Linguist: Assert in Navigation
* [QTBUG-48487](https://qt-project.atlassian.net/browse/QTBUG-48487) QDoc does not respect/show import ... as ... statements
in examples and code snippets
* [QTBUG-139057](https://qt-project.atlassian.net/browse/QTBUG-139057) Doc: Show correct signature for qDebug() , qInfo() ...
macros
* [QTBUG-138573](https://qt-project.atlassian.net/browse/QTBUG-138573) Selected text is shown with a black "highlight" when
opened from Visual Studio
* [QTBUG-138547](https://qt-project.atlassian.net/browse/QTBUG-138547) No disambiguation between types from same root module
* [QTBUG-139199](https://qt-project.atlassian.net/browse/QTBUG-139199) qttools configure error if llvm-provided packages are
used
* [QTBUG-138632](https://qt-project.atlassian.net/browse/QTBUG-138632) Document new label support in Qt Linguist documentation
* [QTBUG-51584](https://qt-project.atlassian.net/browse/QTBUG-51584) qdoc: There is no way to document singletons in QML
* [QTBUG-69756](https://qt-project.atlassian.net/browse/QTBUG-69756) QDoc: Parentheses in link text causes premature link end
anchor
* [QTBUG-86490](https://qt-project.atlassian.net/browse/QTBUG-86490) Generated documentation for change signals that represent
more than one property is hard to read
* [QTBUG-139614](https://qt-project.atlassian.net/browse/QTBUG-139614) QDoc: Index files do not record the declared return type
* [QTBUG-139407](https://qt-project.atlassian.net/browse/QTBUG-139407) QDoc fails to build with LLVM >= 21
* [QTBUG-138084](https://qt-project.atlassian.net/browse/QTBUG-138084) qdoc links return values of static functions to default
ctor of class, not class itself
* [QTBUG-137464](https://qt-project.atlassian.net/browse/QTBUG-137464) See also links (\sa) are not deduplicated
* [QTBUG-99553](https://qt-project.atlassian.net/browse/QTBUG-99553) qdoc: Hidden friends not visible if declared as private
* [QTBUG-114877](https://qt-project.atlassian.net/browse/QTBUG-114877) QDoc doesn't catch private pure virtual methods
* [QTBUG-139769](https://qt-project.atlassian.net/browse/QTBUG-139769) [Regr: 6.9.2 -> 6.10] Qt 6.10 BETA 3: lupdate does not
include context names in ts files
* [QTBUG-139405](https://qt-project.atlassian.net/browse/QTBUG-139405) QMatrix4x4 has an internal Flag enum that QDoc exposes
as flags
* [QTBUG-140105](https://qt-project.atlassian.net/browse/QTBUG-140105) QDoc: -showinternal command-line option should take
precedence over config file
* [QTBUG-140140](https://qt-project.atlassian.net/browse/QTBUG-140140) QDoc generates warnings for documentation typos in
\internal blocks when showinternal=false
* [QTBUG-140166](https://qt-project.atlassian.net/browse/QTBUG-140166) Order of member descriptions does not match order of
list
* [QTBUG-140223](https://qt-project.atlassian.net/browse/QTBUG-140223) Poor rendering of unnamed structs in documentation
* [QTBUG-140096](https://qt-project.atlassian.net/browse/QTBUG-140096) QDoc: \page command with file extensions other than
.html results in double extensions
* [QTBUG-140399](https://qt-project.atlassian.net/browse/QTBUG-140399) QDoc: Invalid HTML generated for breadcrumb elements
* [QTBUG-140539](https://qt-project.atlassian.net/browse/QTBUG-140539) Deprecated members can appear in inherited members list
instead
* [QTBUG-140676](https://qt-project.atlassian.net/browse/QTBUG-140676) Anonymous enum representation inconsistent in members
list
* [QTBUG-140920](https://qt-project.atlassian.net/browse/QTBUG-140920) Context filter in AI Translation dialog is sorted case
sensitively
* [QTBUG-139323](https://qt-project.atlassian.net/browse/QTBUG-139323) Empty deprecated items in Qt namespace
* [QTBUG-140205](https://qt-project.atlassian.net/browse/QTBUG-140205) Property group information is lost across module
boundaries
* [QTBUG-140409](https://qt-project.atlassian.net/browse/QTBUG-140409) QML base type not propagated in index files
* [QTBUG-134806](https://qt-project.atlassian.net/browse/QTBUG-134806) qdoc has no way to independently document QML
enumerations
* [QTBUG-141238](https://qt-project.atlassian.net/browse/QTBUG-141238) Version information refers to QML properties not
property groups
* [QTBUG-105172](https://qt-project.atlassian.net/browse/QTBUG-105172) qdoc creates proxy pages without any warning
* [QTBUG-140508](https://qt-project.atlassian.net/browse/QTBUG-140508) QDoc complains about undocumented parameters to
\overload fn()
* [QTBUG-140510](https://qt-project.atlassian.net/browse/QTBUG-140510) Empty-parameter \overload reference does not pick up
primary overload link
* [QTBUG-140728](https://qt-project.atlassian.net/browse/QTBUG-140728) Should Qdoc generate anything when called with
--redirect-documentation-to-dev-null?
* [QTBUG-141580](https://qt-project.atlassian.net/browse/QTBUG-141580) QDoc reports incorrect location for duplicate primary
overloads in shared comments
* [QTBUG-141581](https://qt-project.atlassian.net/browse/QTBUG-141581) QDoc doesn't respect \fn command order for primary
overload selection in shared comments
* [QTBUG-140686](https://qt-project.atlassian.net/browse/QTBUG-140686) Classes with attributes confuse lupdate
* [QTBUG-140636](https://qt-project.atlassian.net/browse/QTBUG-140636) Function return types with namespaces sometimes confuse
lupdate
* [QTBUG-72107](https://qt-project.atlassian.net/browse/QTBUG-72107) \l font in QToolButton's documentation results in a link
to the font row in the stylesheet reference documentation
* [QTBUG-61571](https://qt-project.atlassian.net/browse/QTBUG-61571) Improvements to doc handling of QML types with same name
and different imports
* [QTBUG-141642](https://qt-project.atlassian.net/browse/QTBUG-141642) QDoc: Possibility of infinite loops from circular class
relationships
* [QTBUG-140548](https://qt-project.atlassian.net/browse/QTBUG-140548) [Reg 6.9.1->6.9.2] Different misdetection of correct
namespace/class with tr
* [QTBUG-141741](https://qt-project.atlassian.net/browse/QTBUG-141741) QDoc reports false positive warnings for properties from
included dependency headers
* [QTBUG-141771](https://qt-project.atlassian.net/browse/QTBUG-141771) QDoc: Duplicate overload notes for signals/slots using
\overload command
* [QTBUG-140550](https://qt-project.atlassian.net/browse/QTBUG-140550) Class inside namespace with the same name confuses
lupdate
* [QTBUG-141155](https://qt-project.atlassian.net/browse/QTBUG-141155) Attached signal not marked as such
* [QTBUG-137048](https://qt-project.atlassian.net/browse/QTBUG-137048) qdoc: Warn about self-link in \sa
* [QTBUG-130152](https://qt-project.atlassian.net/browse/QTBUG-130152) Documentation of QML elements does not show the complete
inheritance
* [QTBUG-141631](https://qt-project.atlassian.net/browse/QTBUG-141631) [6.9.3 -> 6.10 regression] lupdate hangs when fourth
parameter of translate contains angle brackets and double colon
* [QTBUG-141632](https://qt-project.atlassian.net/browse/QTBUG-141632) lupdate discards string when fourth parameter of
`translate` is wrapped in parentheses
* [QTBUG-141954](https://qt-project.atlassian.net/browse/QTBUG-141954) Cannot inherit from QtQuick Templates in QDoc
* [QTBUG-134256](https://qt-project.atlassian.net/browse/QTBUG-134256) Coverity: Use after free in Qt Designer's property
editor
* [QTBUG-134195](https://qt-project.atlassian.net/browse/QTBUG-134195) Qt Widgets Designer/Property editor: theme icons
dropdown shown for  maximumSize Width property
* [QTBUG-141590](https://qt-project.atlassian.net/browse/QTBUG-141590) QDoc: ManifestWriter may silently fail when output
directory doesn't exist
* [QTBUG-141354](https://qt-project.atlassian.net/browse/QTBUG-141354) qmldir file markup is incorrect
* [QTBUG-142150](https://qt-project.atlassian.net/browse/QTBUG-142150) QDoc does not distinguish between links to QML
properties and QML attached properties
* [QTBUG-139449](https://qt-project.atlassian.net/browse/QTBUG-139449) Rename 'How to Resolve QDoc Warnings' page to
'Troubleshooting QDoc Warnings'
* [QTBUG-142351](https://qt-project.atlassian.net/browse/QTBUG-142351) Incorrect since text for QML property groups
* [QTBUG-142451](https://qt-project.atlassian.net/browse/QTBUG-142451) QDoc: segmentation fault when running with
--showinternal
* [QTBUG-142504](https://qt-project.atlassian.net/browse/QTBUG-142504) Fix doc links in qttools
* [QTBUG-141777](https://qt-project.atlassian.net/browse/QTBUG-141777) Documentation: Remove references to "Windows XP" preview
in Qt Widgets Designer
* [QTBUG-142530](https://qt-project.atlassian.net/browse/QTBUG-142530) qdoc: Allow to apply \notranslate to \title
* [QTBUG-140667](https://qt-project.atlassian.net/browse/QTBUG-140667) Undocumented reimplemented public functions in snapshot
builds
* [QTBUG-142427](https://qt-project.atlassian.net/browse/QTBUG-142427) Doc: Clarify which qdoc topic commands support
\deprecated , \preliminary, \internal
* [QTBUG-142577](https://qt-project.atlassian.net/browse/QTBUG-142577) Qt Designer on Mac OS fails to load a custom widget
plugin due to code signature issue
* [QTBUG-142527](https://qt-project.atlassian.net/browse/QTBUG-142527) Prevent qdoc commands to be translated in the
documentation
* [QTBUG-143192](https://qt-project.atlassian.net/browse/QTBUG-143192) Documentation of overloaded signals/slots shows wrong
snippets
* [QTBUG-143212](https://qt-project.atlassian.net/browse/QTBUG-143212) QDoc: Empty link target causes crash
* [QTBUG-143274](https://qt-project.atlassian.net/browse/QTBUG-143274) QDoc: DocBook output missing template declarations in
function signatures
* [QTBUG-143095](https://qt-project.atlassian.net/browse/QTBUG-143095) lupdate-pro is not installed
* [QTBUG-143311](https://qt-project.atlassian.net/browse/QTBUG-143311) Designer crashes when  double clicking widget to inline-
edit text while inline editor of another form is active
* [QTBUG-143475](https://qt-project.atlassian.net/browse/QTBUG-143475) Unnecessary warning when -no-feature-qdoc is used
* [QTBUG-142920](https://qt-project.atlassian.net/browse/QTBUG-142920) qdoc doesn't provide links for template parameters
* [QTBUG-142808](https://qt-project.atlassian.net/browse/QTBUG-142808) \sa with link name part behaves differently to \l
* [QTBUG-143496](https://qt-project.atlassian.net/browse/QTBUG-143496) Plural TS files generated by qt_add_translations() have
incorrect source file paths
* [QTBUG-109117](https://qt-project.atlassian.net/browse/QTBUG-109117) QDoc \qmldefault and \readonly commands are not
supported together
* [QTBUG-143375](https://qt-project.atlassian.net/browse/QTBUG-143375) Overloaded tr method triggers “Class 'MyNamespace' lacks
Q_OBJECT macro” error
* [QTBUG-143644](https://qt-project.atlassian.net/browse/QTBUG-143644) Qt Linguist AI translation crash
* [QTBUG-143645](https://qt-project.atlassian.net/browse/QTBUG-143645) Qt Linguist improvement to avoid partial AI translation
loss
* [QTBUG-143619](https://qt-project.atlassian.net/browse/QTBUG-143619) QDoc generates malformed .qhp syntax in some cases
* [QTBUG-143171](https://qt-project.atlassian.net/browse/QTBUG-143171) qdoc crashes below QDocDatabase::updateNavigation() when
building Squish docs
* [QTBUG-140343](https://qt-project.atlassian.net/browse/QTBUG-140343) Conversion operators get an extra return type
* [QTBUG-143893](https://qt-project.atlassian.net/browse/QTBUG-143893) qttools: lupdate Objective-C calls misinterpreted as C++
attributes
* [QTBUG-143960](https://qt-project.atlassian.net/browse/QTBUG-143960) SBOM: Improve the content of the LibClang dependency
* [QTBUG-142742](https://qt-project.atlassian.net/browse/QTBUG-142742) QDoc core dumps when the include path is invalid
* [QTBUG-136164](https://qt-project.atlassian.net/browse/QTBUG-136164) Saving UI-file using QFormBuilder missing properties
(unsupported?)
* [QTBUG-144451](https://qt-project.atlassian.net/browse/QTBUG-144451) QDoc: \include snippet matching uses substring instead
of exact name
* [QTBUG-130646](https://qt-project.atlassian.net/browse/QTBUG-130646) qdoc hangs when generating QML documentation
* [QTBUG-138901](https://qt-project.atlassian.net/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-110696](https://qt-project.atlassian.net/browse/QTBUG-110696) Qt6CoreMacros.cmake should take AUTOGEN_BUILD_DIR into
account
* [QTBUG-139193](https://qt-project.atlassian.net/browse/QTBUG-139193) Incomplete type information in all member pages
* [QTBUG-139262](https://qt-project.atlassian.net/browse/QTBUG-139262) Some links to non-overloaded functions contain overload
numbers
* [QTBUG-58805](https://qt-project.atlassian.net/browse/QTBUG-58805) Cannot document private virtual (abstract) methods with
QDoc
* [QTBUG-139560](https://qt-project.atlassian.net/browse/QTBUG-139560) Access functions are documented even when their
properties are not
* [QTBUG-136483](https://qt-project.atlassian.net/browse/QTBUG-136483) qdoc non-deterministic .index output
* [QTBUG-105097](https://qt-project.atlassian.net/browse/QTBUG-105097) \since says the macro is a function even if it isn't
* [QTBUG-135418](https://qt-project.atlassian.net/browse/QTBUG-135418) REG->6.9.0: Windows 11 Style: Selection in Qt Designer
looks weird
* [QTBUG-140729](https://qt-project.atlassian.net/browse/QTBUG-140729) QDoc generates duplicate entries in .index and .tags
output files
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-69423](https://qt-project.atlassian.net/browse/QTBUG-69423) QRandomGenerator not random on certain Windows
installations
* [QTBUG-129193](https://qt-project.atlassian.net/browse/QTBUG-129193) Qt compiled with gcc 13 and -march=bdver4/-mtune=bdver4
causes segfaults in tests, downstream applications
* [QTBUG-115448](https://qt-project.atlassian.net/browse/QTBUG-115448) qttools -unity-build-batch-size 100000 fails
* [QTBUG-141665](https://qt-project.atlassian.net/browse/QTBUG-141665) Doc: Suppress "No output generated for ..."
* [PYSIDE-3257](https://qt-project.atlassian.net/browse/PYSIDE-3257) Qt Widget Designer help links are broken

### qtdoc
* [QTBUG-135305](https://qt-project.atlassian.net/browse/QTBUG-135305) Calqlatr example has broken .qmlproject file
* [QTBUG-132833](https://qt-project.atlassian.net/browse/QTBUG-132833) QT_QPA_EGLFS_ROTATION rotates mouse events but not touch
events
* [QTBUG-133792](https://qt-project.atlassian.net/browse/QTBUG-133792) Compiling demos/maroon and demos/hangman on
Windows/MacOS fails
* [QTBUG-136649](https://qt-project.atlassian.net/browse/QTBUG-136649) Doc: Image update related to Qt Online Installer and Qt
Maintenance Tool changes
* [QTTA-401](https://qt-project.atlassian.net/browse/QTTA-401) Qt Jenny Demo: Gradle is not called during CMake configure
to generate code
* [QTBUG-138105](https://qt-project.atlassian.net/browse/QTBUG-138105) [Reg 6.5.9 -> 6.8.3] Alarms demo: TumberDelegate can no
longer read properties
* [QTBUG-137956](https://qt-project.atlassian.net/browse/QTBUG-137956) \generatelist with sorting based on title is buggy
* [QTBUG-138169](https://qt-project.atlassian.net/browse/QTBUG-138169) Document Viewer: Runtime warnings
* [QTBUG-95325](https://qt-project.atlassian.net/browse/QTBUG-95325) Removal of QTextStream::setCodec is not documented
* [QTBUG-118823](https://qt-project.atlassian.net/browse/QTBUG-118823) Debian repository setup suggests putting a password to a
plain text file that is worldreadable
* [QTBUG-138093](https://qt-project.atlassian.net/browse/QTBUG-138093) winrt::init_apartment(multithreaded) causes
QFileDialog::getOpenFileName to get stuck
* [QTBUG-138344](https://qt-project.atlassian.net/browse/QTBUG-138344) documentviewer: Language is not applied to plugin texts
* [QTBUG-91435](https://qt-project.atlassian.net/browse/QTBUG-91435) Debug instruction incorrect on
https://doc.qt.io/qt-5/inputs-linux-device.html
* [QTBUG-138476](https://qt-project.atlassian.net/browse/QTBUG-138476) documentviewer: Fix deployment on macOS, Windows, Linux
* [QTBUG-138176](https://qt-project.atlassian.net/browse/QTBUG-138176) Robot Arm: qmllint warnings
* [QTBUG-138177](https://qt-project.atlassian.net/browse/QTBUG-138177) Robot Arm: runtime warnings
* [QTBUG-138613](https://qt-project.atlassian.net/browse/QTBUG-138613) Remove links to 'Solutions for UI Design' page for 6.10
* [QTBUG-138587](https://qt-project.atlassian.net/browse/QTBUG-138587) Add information on how to subscribe to the mailing list
mentioned on "Security in Qt"
* [QTBUG-138165](https://qt-project.atlassian.net/browse/QTBUG-138165) Dice: qmllint warnings
* [QTBUG-138174](https://qt-project.atlassian.net/browse/QTBUG-138174) Lightning Viewer: runtime warnings
* [QTBUG-138175](https://qt-project.atlassian.net/browse/QTBUG-138175) Media Player example in qtdoc: qmllint warnings
* [QTBUG-135377](https://qt-project.atlassian.net/browse/QTBUG-135377) The Qt Wayland platform plugin is missing from the
documentation.
* [QTBUG-138676](https://qt-project.atlassian.net/browse/QTBUG-138676) Coffee machine examples images not getting current
values fom slider
* [QTBUG-137296](https://qt-project.atlassian.net/browse/QTBUG-137296) Clarifications to "Qt for Android - Building from
Source" page based on customer feedback.
* [QTBUG-117368](https://qt-project.atlassian.net/browse/QTBUG-117368) Thermostat: "Binding loops detected" runtime warnings
* [QTBUG-138188](https://qt-project.atlassian.net/browse/QTBUG-138188) Thermostat: qmllint warnings
* [QTBUG-139281](https://qt-project.atlassian.net/browse/QTBUG-139281) [REG 6.10.0 beta2 -> beta3] demos/coffee not launching
in qmake build on Windows
* [QTBUG-136065](https://qt-project.atlassian.net/browse/QTBUG-136065) Installer command does not work
* [QTBUG-137052](https://qt-project.atlassian.net/browse/QTBUG-137052) Document the new configure's output files in packages
* [QTBUG-138170](https://qt-project.atlassian.net/browse/QTBUG-138170) FX & Material Showroom: qmllint warnings
* [QTBUG-139996](https://qt-project.atlassian.net/browse/QTBUG-139996) lightningviewer fails to build with Boot to Qt on
Windows
* [QTBUG-139340](https://qt-project.atlassian.net/browse/QTBUG-139340) [new example] demos/graphs_csv not compiling on Wasm
multithread
* [QTBUG-138178](https://qt-project.atlassian.net/browse/QTBUG-138178) Same Game: qmllint warnings
* [QTBUG-140383](https://qt-project.atlassian.net/browse/QTBUG-140383) Coffee Machine: qmllint warnings
* [QTBUG-140387](https://qt-project.atlassian.net/browse/QTBUG-140387) Robot Arm: qmllint warnings
* [QTBUG-138795](https://qt-project.atlassian.net/browse/QTBUG-138795) When building from source "-debug-and-release" "cmake
--install ." isn't enough
* [QTBUG-115206](https://qt-project.atlassian.net/browse/QTBUG-115206) Document how to install debug-and-release builds to
avoid missing debug libraries (upstream cmake multi-config install
issue)
* [QTBUG-140395](https://qt-project.atlassian.net/browse/QTBUG-140395) Dice Example: Cannot Read property 'x' of null
* [QTBUG-140385](https://qt-project.atlassian.net/browse/QTBUG-140385) Dice Example: Cannot Read property 'x' of null
* [QTBUG-139937](https://qt-project.atlassian.net/browse/QTBUG-139937) Missing section in Android's getting started
documentation
* [QTBUG-140396](https://qt-project.atlassian.net/browse/QTBUG-140396) 'Thermostat' applications Control view not scaled
properly on 'smallDesktop'
* [QTBUG-140067](https://qt-project.atlassian.net/browse/QTBUG-140067) Clear up or remove 'Porting to iOS' documentation page
* [QTBUG-137076](https://qt-project.atlassian.net/browse/QTBUG-137076) Fix qmllint warnings for Calqlatr example
* [QTBUG-140113](https://qt-project.atlassian.net/browse/QTBUG-140113) Text Viewer Plugin Example does not compile
* [QTBUG-138173](https://qt-project.atlassian.net/browse/QTBUG-138173) Lightning Viewer: qmllint warnings
* [QTBUG-141358](https://qt-project.atlassian.net/browse/QTBUG-141358) Static build documentation out of date
* [QTBUG-138991](https://qt-project.atlassian.net/browse/QTBUG-138991) localization documentation shows wrong catalog name for
Qt WebSockets
* [QTBUG-142071](https://qt-project.atlassian.net/browse/QTBUG-142071) 5.15 is still listed as the supported versions
* [QTBUG-142190](https://qt-project.atlassian.net/browse/QTBUG-142190) Accessory selection reset logic regressed when changing
toys in ToyGalleryPage
* [QTBUG-142325](https://qt-project.atlassian.net/browse/QTBUG-142325) FAILED:
examples/demos/calqlatr/CMakeFiles/calqlatr_qmllint
* [QTBUG-142245](https://qt-project.atlassian.net/browse/QTBUG-142245) [Boot2Qt] Cannot run lightning viewer example on the
device
* [QTBUG-141228](https://qt-project.atlassian.net/browse/QTBUG-141228) stocqt example: Live Data retrieval does not work
anymore for new keys
* [QTBUG-138148](https://qt-project.atlassian.net/browse/QTBUG-138148) photosurface example: CMake warning QTP0004
* [QTBUG-138147](https://qt-project.atlassian.net/browse/QTBUG-138147) stocqt example: CMake warning QTP0004
* [QTBUG-143100](https://qt-project.atlassian.net/browse/QTBUG-143100) QtJenny example won't compile due to fatal errors
* [QTBUG-142693](https://qt-project.atlassian.net/browse/QTBUG-142693) ToyCustomizer: Text overlaps in OverviewPage
* [QTBUG-142580](https://qt-project.atlassian.net/browse/QTBUG-142580) [REG 6.10.1->6.11.0] car-configurator not launching
* [QTBUG-143651](https://qt-project.atlassian.net/browse/QTBUG-143651) Do not translate proper nouns
* [QTBUG-143863](https://qt-project.atlassian.net/browse/QTBUG-143863) error: ‘OnSuccess’ is not a member of
‘QtTaskTree::CallDone’ {aka ‘QFlags<QtTaskTree::CallDoneFlag>’}
* [QTBUG-143980](https://qt-project.atlassian.net/browse/QTBUG-143980) Feature Delivery: Bug fixing and updates.
* [QTBUG-144172](https://qt-project.atlassian.net/browse/QTBUG-144172) Doc: Qt Platform Integration project is not visible in
the TOC tree
* [QTBUG-144477](https://qt-project.atlassian.net/browse/QTBUG-144477) Update list of GPL components in licenses.html
* [QTBUG-136334](https://qt-project.atlassian.net/browse/QTBUG-136334) The documentation of qt6_add_lightprobe_images is
missing
* [QTBUG-138189](https://qt-project.atlassian.net/browse/QTBUG-138189) To Do List: qmllint warnings
* [QTBUG-138164](https://qt-project.atlassian.net/browse/QTBUG-138164) Coffee Machine: qmllint warnings
* [QTBUG-138632](https://qt-project.atlassian.net/browse/QTBUG-138632) Document new label support in Qt Linguist documentation
* [QTBUG-138527](https://qt-project.atlassian.net/browse/QTBUG-138527) Replace direct links to https://doc.qt.io/qt-6/
* [QTBUG-138898](https://qt-project.atlassian.net/browse/QTBUG-138898) [REG 6.10.0 beta2 -> beta3] demos/coffee not launching
* [QTBUG-138901](https://qt-project.atlassian.net/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-138124](https://qt-project.atlassian.net/browse/QTBUG-138124) Car Configurator: Runtime warnings
* [QTTA-450](https://qt-project.atlassian.net/browse/QTTA-450) QtJenny Example fails to build with
'QtCore/private/qandroidextras_p.h' file not found
* [QTBUG-136809](https://qt-project.atlassian.net/browse/QTBUG-136809) Specify that the Raspberry Pi 5 SoC is the tier 1
reference target
* [QTBUG-140051](https://qt-project.atlassian.net/browse/QTBUG-140051) Cosmetic facelift for QtJenny Demo
* [QTBUG-139769](https://qt-project.atlassian.net/browse/QTBUG-139769) [Regr: 6.9.2 -> 6.10] Qt 6.10 BETA 3: lupdate does not
include context names in ts files
* [QTTA-460](https://qt-project.atlassian.net/browse/QTTA-460) Documentation navigation is not functional
* [QTBUG-138019](https://qt-project.atlassian.net/browse/QTBUG-138019) [Reg 6.7.3 -> 6.8.4][macOS][macos] Calqlatr: installed
example with qml modules doesn't launch due to code signing issues and
macdeployqt modifications
* [QTBUG-89033](https://qt-project.atlassian.net/browse/QTBUG-89033) Do not use versioned QML imports in Qt 6 documentation &
examples
* [QTBUG-141086](https://qt-project.atlassian.net/browse/QTBUG-141086) qmlls: Warnings about missing required property (that is
set)
* [QTBUG-142012](https://qt-project.atlassian.net/browse/QTBUG-142012) String "6.10.0" found in 6.10.1 sources
* [QTBUG-142147](https://qt-project.atlassian.net/browse/QTBUG-142147) ToyCustomizer: wrong number of items on "Review Order"
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-142397](https://qt-project.atlassian.net/browse/QTBUG-142397) Document CMake qt_target_qml_from_lottie() function
* [QTBUG-142088](https://qt-project.atlassian.net/browse/QTBUG-142088) Doc: Clean \externalpage declarations
* [QTBUG-143206](https://qt-project.atlassian.net/browse/QTBUG-143206) String 6.10.2 in 6.11.0 sources
* [QTBUG-143309](https://qt-project.atlassian.net/browse/QTBUG-143309) qt_add_openapi_client() command is undocumented
* [QTBUG-143555](https://qt-project.atlassian.net/browse/QTBUG-143555) ToyCustomizer: UI improvements for WASM
* [QTBUG-142730](https://qt-project.atlassian.net/browse/QTBUG-142730) Demos contain orphaned references to unused custom QML
types generated by Qt Design Studio
* [QTBUG-143634](https://qt-project.atlassian.net/browse/QTBUG-143634) Qt Graphs CSV Demo does not validate input values before
rendering, causing integer overflow in texture size calculation
* [QTBUG-143916](https://qt-project.atlassian.net/browse/QTBUG-143916) Fix QDoc warnings for Qt 6.11
* [QTBUG-144451](https://qt-project.atlassian.net/browse/QTBUG-144451) QDoc: \include snippet matching uses substring instead
of exact name
* [QTBUG-144728](https://qt-project.atlassian.net/browse/QTBUG-144728) QtJenny example won't compile

### qtqa
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtlocation
* [QTBUG-138409](https://qt-project.atlassian.net/browse/QTBUG-138409) Incorrect qtlocation documentation
* [QTBUG-137557](https://qt-project.atlassian.net/browse/QTBUG-137557) QtLocation: Using GeocodeModel with OSM plugin in QML
causes app crash when canceling update
* [QTBUG-140841](https://qt-project.atlassian.net/browse/QTBUG-140841) Submodule update failure in Qt Location after Qt Qml
change
* [QTBUG-141671](https://qt-project.atlassian.net/browse/QTBUG-141671) Doc: Suppress "No output generated for" warnings
* [QTBUG-139941](https://qt-project.atlassian.net/browse/QTBUG-139941) DelegateModelAccess.ReadWrite should allow writing to
arrays and sequences as models
* [QTBUG-139560](https://qt-project.atlassian.net/browse/QTBUG-139560) Access functions are documented even when their
properties are not
* [QTBUG-139780](https://qt-project.atlassian.net/browse/QTBUG-139780) Qt Positioning: Discrepancy between documented type
names and actual type names
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtpositioning
* [QTBUG-136157](https://qt-project.atlassian.net/browse/QTBUG-136157) Qt Positioning: Add alt texts
* [QTBUG-138187](https://qt-project.atlassian.net/browse/QTBUG-138187) Satellite Info: qmllint warnings
* [QTBUG-141757](https://qt-project.atlassian.net/browse/QTBUG-141757) QT_UNITY_BUILD broken on windows
* [QTBUG-142317](https://qt-project.atlassian.net/browse/QTBUG-142317) QGeoPath.contains() does not work correctly
* [QTBUG-137764](https://qt-project.atlassian.net/browse/QTBUG-137764) QDoc uses incorrect image source
* [QTBUG-106049](https://qt-project.atlassian.net/browse/QTBUG-106049) Qt Android's QGeoCoordinate API returns altitude in
wrong reference frame
* [QTBUG-138174](https://qt-project.atlassian.net/browse/QTBUG-138174) Lightning Viewer: runtime warnings
* [QTBUG-139654](https://qt-project.atlassian.net/browse/QTBUG-139654) Update QtPositioning documentation to use QDoc commands
* [QTBUG-139780](https://qt-project.atlassian.net/browse/QTBUG-139780) Qt Positioning: Discrepancy between documented type
names and actual type names
* [QTBUG-139560](https://qt-project.atlassian.net/browse/QTBUG-139560) Access functions are documented even when their
properties are not
* [QTBUG-139782](https://qt-project.atlassian.net/browse/QTBUG-139782) Qt Positioning: Outdated documentation for value types
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-142020](https://qt-project.atlassian.net/browse/QTBUG-142020) Incorrect usage of qFuzzyCompare() abounds in Qt source
[QtCore]
* [QTBUG-143660](https://qt-project.atlassian.net/browse/QTBUG-143660) Incorrect usage of qFuzzyCompare() abounds in Qt source
[Qt Positioning]

### qtsensors
* [QTBUG-138901](https://qt-project.atlassian.net/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtconnectivity
* [QTBUG-136506](https://qt-project.atlassian.net/browse/QTBUG-136506) NFC target should be invalidated if Java function call
fails
* [QTBUG-136156](https://qt-project.atlassian.net/browse/QTBUG-136156) Qt Bluetooth: Add alt texts
* [QTBUG-136150](https://qt-project.atlassian.net/browse/QTBUG-136150) Qt NFC: Add alt texts
* [QTBUG-140697](https://qt-project.atlassian.net/browse/QTBUG-140697) Bluetooth Low Energy Scanner does not respect safe areas
* [QTBUG-140825](https://qt-project.atlassian.net/browse/QTBUG-140825) QBluetoothDeviceInfo::isCached() always returns true on
Windows
* [QTBUG-142334](https://qt-project.atlassian.net/browse/QTBUG-142334) error: variable has incomplete type 'const void'
* [QTBUG-136692](https://qt-project.atlassian.net/browse/QTBUG-136692) BLE devices can't be discovered after initial connection
on iOS 18+
* [QTBUG-138901](https://qt-project.atlassian.net/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-139280](https://qt-project.atlassian.net/browse/QTBUG-139280) Cannot build QT 6.8 without GNU extensions
* [QTBUG-141665](https://qt-project.atlassian.net/browse/QTBUG-141665) Doc: Suppress "No output generated for ..."
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtwayland
* [QTBUG-137333](https://qt-project.atlassian.net/browse/QTBUG-137333) Wayland Compositor + static build + LTO = crash
* [QTBUG-133866](https://qt-project.atlassian.net/browse/QTBUG-133866) Using qt-shell, if item in dialog is selected with
mouse, no further focus navigation via keyboard possible
* [QTBUG-115063](https://qt-project.atlassian.net/browse/QTBUG-115063) Crash in WaylandEglClientBuffer::WaylandEglClientBuffer
* [QTBUG-119259](https://qt-project.atlassian.net/browse/QTBUG-119259) Missing documentation of QT_IVI_SURFACE_ID
* [QTBUG-141147](https://qt-project.atlassian.net/browse/QTBUG-141147) [qtwayland] Manual tests build failure
* [QTBUG-141871](https://qt-project.atlassian.net/browse/QTBUG-141871) QDoc: error: Documentation warnings (51) exceeded the
limit (0) for 'QtWaylandCompositor'
* [QTBUG-142162](https://qt-project.atlassian.net/browse/QTBUG-142162) wl_output_send_done is not called when new client binds
* [QTBUG-138901](https://qt-project.atlassian.net/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-138907](https://qt-project.atlassian.net/browse/QTBUG-138907) Probable Use after Free on
QtWaylandCompositor::onSurfaceDestroyed

### qt3d
* [QTBUG-135394](https://qt-project.atlassian.net/browse/QTBUG-135394) MouseHandler may crash if it is destroyed while mouse is
being moved
* [QTBUG-137866](https://qt-project.atlassian.net/browse/QTBUG-137866) error: no member named 'getV4Engine' in
'QQmlEnginePrivate'
* [QTBUG-139978](https://qt-project.atlassian.net/browse/QTBUG-139978) qt3d fails on documentation-warnings
* [QTBUG-138670](https://qt-project.atlassian.net/browse/QTBUG-138670) Doc: Scene3D QML type is missed at Qt 3D Scene3D Module
* [QTBUG-141068](https://qt-project.atlassian.net/browse/QTBUG-141068) error: no matching function for call to
‘QString::arg(QRhiTexture::Flags)’
* [QTBUG-140939](https://qt-project.atlassian.net/browse/QTBUG-140939) Qt3DExtra after Qt 6.9
* [QTBUG-138901](https://qt-project.atlassian.net/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-140181](https://qt-project.atlassian.net/browse/QTBUG-140181) Build failure in QtDeclarative with latest nightly
libc++

### qtimageformats
* [QTBUG-138901](https://qt-project.atlassian.net/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtserialbus
* [QTBUG-107140](https://qt-project.atlassian.net/browse/QTBUG-107140) Typo in the document?
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtserialport
* [QTBUG-136154](https://qt-project.atlassian.net/browse/QTBUG-136154) Qt Serial Port: Add alt texts
* [QTBUG-133489](https://qt-project.atlassian.net/browse/QTBUG-133489) ResourceError does not fire on unplug for QtSerialPort
6.8.2
* [QTBUG-138643](https://qt-project.atlassian.net/browse/QTBUG-138643) Details missing for some USB serialport adapters
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtwebsockets
* [QTBUG-136153](https://qt-project.atlassian.net/browse/QTBUG-136153) Qt WebSockets: Add alt texts
* [QTBUG-130361](https://qt-project.atlassian.net/browse/QTBUG-130361) QWebSocketServer ssl errors handling not on part with
other classes
* [QTBUG-81084](https://qt-project.atlassian.net/browse/QTBUG-81084) Websocket client creates TCP RST instead proper shutdown
on close()
* [QTBUG-135959](https://qt-project.atlassian.net/browse/QTBUG-135959) tst_QWebSocket::moveToThreadNoWarning is failing
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-141665](https://qt-project.atlassian.net/browse/QTBUG-141665) Doc: Suppress "No output generated for ..."

### qtwebchannel
* [QTBUG-141648](https://qt-project.atlassian.net/browse/QTBUG-141648) Few WebChannel object registration crashes
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-140181](https://qt-project.atlassian.net/browse/QTBUG-140181) Build failure in QtDeclarative with latest nightly
libc++

### qtwebengine
* [QTBUG-135974](https://qt-project.atlassian.net/browse/QTBUG-135974) adding module pdfwidgets leads to a warning
* [QTBUG-136622](https://qt-project.atlassian.net/browse/QTBUG-136622) Accessiblity:voice over can't read table content
* [QTBUG-134055](https://qt-project.atlassian.net/browse/QTBUG-134055) Make Qt WebEngine expose accessibility content properly
* [QTBUG-133608](https://qt-project.atlassian.net/browse/QTBUG-133608) Missing documentation on how to install Qt WebEngine
* [QTBUG-137447](https://qt-project.atlassian.net/browse/QTBUG-137447) FAIL!  : tst_UIDelegates::javaScriptDialog(AlertDialog)
'(static_cast<QGuiApplication
*>(QCoreApplication::instance()))->focusObject()' returned FALSE.
* [QTBUG-137854](https://qt-project.atlassian.net/browse/QTBUG-137854) error: ‘getV4Engine’ is not a member of
‘QQmlEnginePrivate’
* [QTBUG-135100](https://qt-project.atlassian.net/browse/QTBUG-135100) QtPdf doc - broken link & missing information
* [QTBUG-111907](https://qt-project.atlassian.net/browse/QTBUG-111907) Crash when touching text field inside WebEngineView
* [QTBUG-136231](https://qt-project.atlassian.net/browse/QTBUG-136231) Min c++ version required for QtWebengine
* [QTBUG-138009](https://qt-project.atlassian.net/browse/QTBUG-138009) Correct suggestions for building Qt WebEngine
* [QTBUG-138159](https://qt-project.atlassian.net/browse/QTBUG-138159) Build error:
QtWebEngineCore/private/qtwebenginecoreglobal_p.h: No such file or
directory
* [QTBUG-138734](https://qt-project.atlassian.net/browse/QTBUG-138734) webengine pdf example: runtime warnings
* [QTBUG-138425](https://qt-project.atlassian.net/browse/QTBUG-138425) QtWebEngine no GPU acceleration on Nvidia RTX 4090
* [QTBUG-138736](https://qt-project.atlassian.net/browse/QTBUG-138736) FAIL!  :
tst_QWebEngineCookieStore::basicFilterOverHTTP() Compared values are not
the same
* [QTBUG-134762](https://qt-project.atlassian.net/browse/QTBUG-134762) [REG 6.6 → 6.8] HTML id attribute not coming through
unmodified when observing
* [QTBUG-138641](https://qt-project.atlassian.net/browse/QTBUG-138641) QtWebEngine rendering glitches with &lt;select&gt; element
* [QTBUG-138589](https://qt-project.atlassian.net/browse/QTBUG-138589) Quick Nano Browser has qmllint warnings
* [QTBUG-134637](https://qt-project.atlassian.net/browse/QTBUG-134637) QWebEngine does not respect iframe permissions
* [QTBUG-135787](https://qt-project.atlassian.net/browse/QTBUG-135787) HTML <permission> requests get ignored -> no
microphone/video on Zoom/Meet
* [QTBUG-139322](https://qt-project.atlassian.net/browse/QTBUG-139322) fail to install to staging dir
* [QTBUG-139327](https://qt-project.atlassian.net/browse/QTBUG-139327) webenginequick/quicknanobrowser: make install step does
not install the binary
* [QTBUG-138881](https://qt-project.atlassian.net/browse/QTBUG-138881) Windows Debug: QQuickWebEngineScriptCollection crashes
after adding custom library path
* [QTBUG-139624](https://qt-project.atlassian.net/browse/QTBUG-139624) Make qdoc to understand qml list types with lower case
* [QTBUG-139766](https://qt-project.atlassian.net/browse/QTBUG-139766) [Windows] Linker isn't able to create pdb file for
Qt6WebEngineCore
* [QTBUG-139710](https://qt-project.atlassian.net/browse/QTBUG-139710) [Reg 6.8 -> 6.9] qml web engine frame crashes on
assigment
* [QTBUG-139998](https://qt-project.atlassian.net/browse/QTBUG-139998) pdf\multipage and pdf\singlepage fails to build with
Boot to Qt 6.10.0 beta4 on Windows
* [QTBUG-122766](https://qt-project.atlassian.net/browse/QTBUG-122766) QPdfSearchModelPrivate::doSearch warning "not found in
context" happens sometimes
* [QTBUG-140515](https://qt-project.atlassian.net/browse/QTBUG-140515) User-Agent set via QWebEngineUrlRequestInterceptor is
ignored for reloads
* [QTBUG-140029](https://qt-project.atlassian.net/browse/QTBUG-140029) [macOS] Deployment target not detected for Qt Pdf
* [QTBUG-140032](https://qt-project.atlassian.net/browse/QTBUG-140032) [macOS] GnObject_Pdf linker error
* [QTBUG-140234](https://qt-project.atlassian.net/browse/QTBUG-140234) Memory leak on repeated setUrl() calls in QWebEnginePage
with QWebEngineView
* [QTBUG-131443](https://qt-project.atlassian.net/browse/QTBUG-131443) QPdfView mouseEvents don’t have correct position when
scrolled
* [QTBUG-141096](https://qt-project.atlassian.net/browse/QTBUG-141096) [REG 6.9 -> 6.10] Segfault when clicking
camera/microphone <permission> element
* [QTBUG-136160](https://qt-project.atlassian.net/browse/QTBUG-136160) QtWebEngine based browser shows nothing with legacy
NVIDIA driver
* [QTBUG-141112](https://qt-project.atlassian.net/browse/QTBUG-141112) Build fails with -disable-deprecated-up-to 0x060b00
* [QTBUG-141573](https://qt-project.atlassian.net/browse/QTBUG-141573) QtWebEngine does not forward Chromium inputmode hints
* [QTBUG-139461](https://qt-project.atlassian.net/browse/QTBUG-139461) Getting error "Cannot read property 'destroy' of
undefined" when trying to close the tab in Nano Browser example
* [QTBUG-141153](https://qt-project.atlassian.net/browse/QTBUG-141153) QtWebEngine fails to build: brotli/libcommon.a: error
adding symbols: archive has no index
* [QTBUG-141739](https://qt-project.atlassian.net/browse/QTBUG-141739) [REG 6.9.2-6.9.3] Sporadic deadlocks on WebEngineView
destruction
* [QTBUG-141214](https://qt-project.atlassian.net/browse/QTBUG-141214) WebEngine freezes UI
* [QTBUG-141476](https://qt-project.atlassian.net/browse/QTBUG-141476) &lt;select&gt; element does not work in Weston
* [QTBUG-140321](https://qt-project.atlassian.net/browse/QTBUG-140321) When QT_QPA_PLATFORM is set to wayland, QtWebEngine
cannot select items in a &lt;select&gt; element.
* [QTBUG-139709](https://qt-project.atlassian.net/browse/QTBUG-139709) Qt WebEngine: HTML "select" elements have excessive gap
* [QTBUG-135040](https://qt-project.atlassian.net/browse/QTBUG-135040) macos: Voice Over rect is wrongly calculated for
WebEngine
* [QTBUG-138747](https://qt-project.atlassian.net/browse/QTBUG-138747) Virtual Keyboard is not displayed after selecting the
pull-down menu of the Web with QtWebEngine + QVK + Wayland
* [QTBUG-116619](https://qt-project.atlassian.net/browse/QTBUG-116619) Building under iOS produces hundreds of warnings related
to QtWebEngine and PDF
* [QTBUG-143278](https://qt-project.atlassian.net/browse/QTBUG-143278) Accessibility observer after 138-based
* [QTBUG-143279](https://qt-project.atlassian.net/browse/QTBUG-143279) Update tst_Origins::jsUrlRelative
* [QTBUG-142323](https://qt-project.atlassian.net/browse/QTBUG-142323) QtWebEngine blocks building with MSVC Tooset 14.5
(VS 2026)
* [QTBUG-142534](https://qt-project.atlassian.net/browse/QTBUG-142534) [REG 6.10.1-6.10.2] Broken rendering when reparenting
WebEngineView to another window (again)
* [QTBUG-131304](https://qt-project.atlassian.net/browse/QTBUG-131304) Broken rendering when reparenting WebEngineView to
another window
* [QTBUG-142667](https://qt-project.atlassian.net/browse/QTBUG-142667) Building 6.5.11 WebEngine fails on Ubuntu 22.04
* [QTBUG-124576](https://qt-project.atlassian.net/browse/QTBUG-124576) Cannot build QtWebEngine
* [QTBUG-143467](https://qt-project.atlassian.net/browse/QTBUG-143467) qtwebengine/qtpdf cross-complations fail with bad
--sysroot= flag
* [QTBUG-143625](https://qt-project.atlassian.net/browse/QTBUG-143625) Incorrect usage of qFuzzyCompare() abounds in Qt source
[QtWebEngine]
* [QTBUG-141866](https://qt-project.atlassian.net/browse/QTBUG-141866) QTWebEngine renders incorrectly due to disabling GBM on
NVK
* [QTBUG-143725](https://qt-project.atlassian.net/browse/QTBUG-143725) webengine/chromium(140-based) fails build on apalis-imx6
* [QTBUG-143984](https://qt-project.atlassian.net/browse/QTBUG-143984) QtWebEngineQuick does not handle page's favicon URLs
which contains no extension
* [QTBUG-131640](https://qt-project.atlassian.net/browse/QTBUG-131640) WebEngine not starting on properly when deployed with
specific structure on Windows
* [QTBUG-144270](https://qt-project.atlassian.net/browse/QTBUG-144270) QTWEBENGINE_RESOURCES_PATH does not work on Windows
* [QTBUG-133086](https://qt-project.atlassian.net/browse/QTBUG-133086) Doc: Improve Networking and WebEngine security topics
* [QTBUG-136257](https://qt-project.atlassian.net/browse/QTBUG-136257) QtWebEngine based browser shows nothing with panthor
driver
* [QTBUG-136613](https://qt-project.atlassian.net/browse/QTBUG-136613) Top flaky test: tst_QWebEngineView::focusOnNavigation
* [QTBUG-139424](https://qt-project.atlassian.net/browse/QTBUG-139424) GPU rendering not working with mesa 25.2
* [QTBUG-139335](https://qt-project.atlassian.net/browse/QTBUG-139335) QtWebEngine based browser shows nothing with MESA
LLVMpipe
* [QTBUG-140889](https://qt-project.atlassian.net/browse/QTBUG-140889)  QWebEngineUrlRequestInfo::redirect() fails with No
'Access-Control-Allow-Origin' header is present on the requested
resource.
* [QTBUG-140444](https://qt-project.atlassian.net/browse/QTBUG-140444) Service workers do not honor
QWebEngineProfile::setHttpUserAgent
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-140232](https://qt-project.atlassian.net/browse/QTBUG-140232) Crash when removing QWebEngineView while printing a
document
* [QTBUG-137768](https://qt-project.atlassian.net/browse/QTBUG-137768) Crash in WebEngineQuick when rapidly switching between
multiple WebEngineView component
* [QTBUG-142320](https://qt-project.atlassian.net/browse/QTBUG-142320) [REG 6.10.0 -> .1] Frequent segfaults in QAccessible
* [QTBUG-142805](https://qt-project.atlassian.net/browse/QTBUG-142805) [REG 6.8.3-6.9.3] Crash if UpdateTooltip is called on
time while WebEngineView is being destroyed
* [QTBUG-96239](https://qt-project.atlassian.net/browse/QTBUG-96239) Document CMake component in CMake function documentation
* [QTBUG-80941](https://qt-project.atlassian.net/browse/QTBUG-80941) Chromium command line arguments for TLS versions/ciphers
don't work
* [QTBUG-141785](https://qt-project.atlassian.net/browse/QTBUG-141785) qtwebengine builds on windows don't /mostly/ use sccache
* [QTBUG-122655](https://qt-project.atlassian.net/browse/QTBUG-122655) 6.8.0 toplevel build fails on macOS, qtwebengine
* [QTBUG-141665](https://qt-project.atlassian.net/browse/QTBUG-141665) Doc: Suppress "No output generated for ..."
* [QTBUG-142247](https://qt-project.atlassian.net/browse/QTBUG-142247) [REG 6.10.0 -> .1] SIGTRAP when accessing
QWebEngineExtensionManager of off-the-record profile

### qtwebview
* [QTBUG-136082](https://qt-project.atlassian.net/browse/QTBUG-136082) Android Webview fails to load all html string because it
is percent-encoded
* [QTBUG-134723](https://qt-project.atlassian.net/browse/QTBUG-134723) [REG 6.8.0 -> 6.8.1] WebView's loadHtml() with BaseURL
has issues loading HTML content.
* [QTBUG-138555](https://qt-project.atlassian.net/browse/QTBUG-138555) webview2 can not create user data folder
* [QTBUG-139641](https://qt-project.atlassian.net/browse/QTBUG-139641) WebView2 plugin opens its own new windows Qt has no
control over
* [QTBUG-139717](https://qt-project.atlassian.net/browse/QTBUG-139717) qwebview loads webenginequick no matter if webview2
plugin backend selected
* [QTBUG-75747](https://qt-project.atlassian.net/browse/QTBUG-75747) Windows: Support WebView2 backend on msvc
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-46286](https://qt-project.atlassian.net/browse/QTBUG-46286) WebView object created and destroyed dynamically makes
android-app crash.

### qtcharts
* [QTBUG-136770](https://qt-project.atlassian.net/browse/QTBUG-136770) QLineSeries.clear() does not remove all lines from the
plot in that series
* [QTBUG-135240](https://qt-project.atlassian.net/browse/QTBUG-135240) Animation effects in ChartView makes PieSlice lose its
alpha channel
* [QTBUG-132790](https://qt-project.atlassian.net/browse/QTBUG-132790) Unexpected behaviour of QScatterSeries for
selectedPoints, replace and deselectAllPoints
* [QTBUG-132357](https://qt-project.atlassian.net/browse/QTBUG-132357) setSelectedColor doesn't work on barsets added to
QBarSeries with insert method
* [QTBUG-140545](https://qt-project.atlassian.net/browse/QTBUG-140545) Charts with QML Gallery example draws under system bars
(top and bottom)
* [QTBUG-136152](https://qt-project.atlassian.net/browse/QTBUG-136152) Qt Charts: Add alt texts
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtdatavis3d
* [QTBUG-138512](https://qt-project.atlassian.net/browse/QTBUG-138512) The classes in the Qt DataVisualization module do not
use the application's QLocale by default.
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-143622](https://qt-project.atlassian.net/browse/QTBUG-143622) Incorrect usage of qFuzzyCompare() abounds in Qt source
[QtGraphs and QtDatavis]

### qtvirtualkeyboard
* [QTBUG-136695](https://qt-project.atlassian.net/browse/QTBUG-136695) VKB: Entering English characters followed by Digits
automatically converts to chinese
* [QTBUG-134582](https://qt-project.atlassian.net/browse/QTBUG-134582) Languages dropdown appears blank when scrolling in Qt
Keyboard
* [QTBUG-137434](https://qt-project.atlassian.net/browse/QTBUG-137434) Inconsistent Keyboard Layout Country List Display
* [QTBUG-131374](https://qt-project.atlassian.net/browse/QTBUG-131374) The wordCandidateList field is not visible on the
virtual keyboard in a widget application.
* [QTBUG-133614](https://qt-project.atlassian.net/browse/QTBUG-133614) Caps Lock is not working properly in Qt Virtual
Keyboard.
* [QTBUG-138617](https://qt-project.atlassian.net/browse/QTBUG-138617)  chooceCandidate Variable Name Error
* [QTBUG-138624](https://qt-project.atlassian.net/browse/QTBUG-138624) handelGestureDetected Variable Name Error
* [QTBUG-138693](https://qt-project.atlassian.net/browse/QTBUG-138693) Doc: VirtualKeyboardSetting QML Type is missed at Qt
Virtual Keyboard QML Types
* [QTBUG-139038](https://qt-project.atlassian.net/browse/QTBUG-139038) Overlay issue with Virtual Keyboard + Material Style
* [QTBUG-124178](https://qt-project.atlassian.net/browse/QTBUG-124178) Virtualkeyboard of Qt 5.15.15 crash on Ubuntu
* [QTBUG-126402](https://qt-project.atlassian.net/browse/QTBUG-126402) QML virtual keyboard behavior regression between 5.x and
6.x
* [QTBUG-137731](https://qt-project.atlassian.net/browse/QTBUG-137731) Shadow Input is not properly displayed with
DesktopInputPanel with fullScreenMode = true
* [QTBUG-138921](https://qt-project.atlassian.net/browse/QTBUG-138921) Virtual Keyboard plugin missing or fails to load in Qt
6.9.1
* [QTBUG-137923](https://qt-project.atlassian.net/browse/QTBUG-137923) [Reg 6.8.3->6.9.0] Virtual keyboard is totally broken
because it depends on Qt MultiMedia
* [QTBUG-138888](https://qt-project.atlassian.net/browse/QTBUG-138888) Japanese layout cannot input Kanji characters in many
cases
* [QTBUG-137921](https://qt-project.atlassian.net/browse/QTBUG-137921) [Reg 6.8.3->6.9.0] Desktop virtual keyboard cannot find
InputPanel.qml and freezes the application
* [QTBUG-137250](https://qt-project.atlassian.net/browse/QTBUG-137250) REG->6.9.0: VirtualKeyboard not working (Linux)
* [QTBUG-140553](https://qt-project.atlassian.net/browse/QTBUG-140553) qmllint does not recognize
VirtualKeyboardSettings.wordCandidateList
* [QTBUG-140521](https://qt-project.atlassian.net/browse/QTBUG-140521) QML InputMethod crashes
* [QTBUG-135140](https://qt-project.atlassian.net/browse/QTBUG-135140) Using a virtual keyboard with binding removal causes QML
output logging to throw binding removal errors.
* [QTBUG-123415](https://qt-project.atlassian.net/browse/QTBUG-123415) [Qt Virtual Keyboard] Example produces lots of warnings
at startup
* [QTBUG-138901](https://qt-project.atlassian.net/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-136149](https://qt-project.atlassian.net/browse/QTBUG-136149) Qt Virtual Keyboard: Add alt texts
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-137440](https://qt-project.atlassian.net/browse/QTBUG-137440) qt6-declarative qmlcachegen non-determinism

### qtscxml
* [QTBUG-135827](https://qt-project.atlassian.net/browse/QTBUG-135827) foreach array is not evaluated
* [QTBUG-135906](https://qt-project.atlassian.net/browse/QTBUG-135906) Finalize step is not processed
* [QTBUG-135396](https://qt-project.atlassian.net/browse/QTBUG-135396) Errors point to initial scxml file instead of the
invoked where it happens
* [QTBUG-137851](https://qt-project.atlassian.net/browse/QTBUG-137851) error: cannot initialize a parameter of type
'QQmlTypeLoader *' with an rvalue of type 'QQmlEnginePrivate *'
* [QTBUG-144281](https://qt-project.atlassian.net/browse/QTBUG-144281) error: type 'unsigned int' cannot be used prior to '::'
because it has no members
* [QTBUG-138901](https://qt-project.atlassian.net/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-141665](https://qt-project.atlassian.net/browse/QTBUG-141665) Doc: Suppress "No output generated for ..."

### qtspeech
* [QTBUG-128818](https://qt-project.atlassian.net/browse/QTBUG-128818) QTextToSpeech with flite crashes saying ©
* [QTBUG-137735](https://qt-project.atlassian.net/browse/QTBUG-137735) Failing tests on tqtc/lts-6.8: tst_QTextToSpeech
* [QTBUG-137855](https://qt-project.atlassian.net/browse/QTBUG-137855) QTextToSpeech: flite - sayingWord signals emitted
delayed
* [QTBUG-138064](https://qt-project.atlassian.net/browse/QTBUG-138064) [flite] tst_QTextToSpeech fails on ubuntu/arm
* [QTBUG-139660](https://qt-project.atlassian.net/browse/QTBUG-139660) QTextToSpeech WinRT backend stops speaking after the
first word in Qt 6.9.2
* [QTBUG-137947](https://qt-project.atlassian.net/browse/QTBUG-137947) [flite] QTextToSpeech::pause(BoundaryHint::Word) not
implemented
* [QTBUG-138010](https://qt-project.atlassian.net/browse/QTBUG-138010) layout / palette glitches with quickspeech example
* [QTBUG-138901](https://qt-project.atlassian.net/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-108205](https://qt-project.atlassian.net/browse/QTBUG-108205) tst_QTextToSpeech::pauseResume(darwin) fails on macOS 13
in CI

### qtnetworkauth
* [QTBUG-141774](https://qt-project.atlassian.net/browse/QTBUG-141774) openSUSE 16.0 qtnetworkauth -
tst_oauthurischemereplyhandler failed with timeout
* [QTBUG-135353](https://qt-project.atlassian.net/browse/QTBUG-135353) Doc: Edit Qt Network Authorization documentation
* [QTBUG-133086](https://qt-project.atlassian.net/browse/QTBUG-133086) Doc: Improve Networking and WebEngine security topics
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtremoteobjects
* [QTBUG-130972](https://qt-project.atlassian.net/browse/QTBUG-130972) repc is not deterministic
* [QTBUG-113433](https://qt-project.atlassian.net/browse/QTBUG-113433) Typo in the document?
* [QTBUG-139754](https://qt-project.atlassian.net/browse/QTBUG-139754) FAIL!  : tst_clientSSL::testRun()
'socketClient->waitForEncrypted(-1)' returned FALSE
* [PYSIDE-3179](https://qt-project.atlassian.net/browse/PYSIDE-3179) REG->6.11.0: QtRemoteObjects/integration_test.py (and
other RO tests) assert/fail
* [QTBUG-139845](https://qt-project.atlassian.net/browse/QTBUG-139845) Reg->6.11: Assert when passing a too long-list to
QMetaMethodBuilder::setParameterNames()
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-140181](https://qt-project.atlassian.net/browse/QTBUG-140181) Build failure in QtDeclarative with latest nightly
libc++

### qtlottie
* [QTBUG-138213](https://qt-project.atlassian.net/browse/QTBUG-138213) Some easing curves are misinterpreted in Lottie
* [QTBUG-139975](https://qt-project.atlassian.net/browse/QTBUG-139975) New example lottie/qtlottieviewer fails to configure
* [QTBUG-140730](https://qt-project.atlassian.net/browse/QTBUG-140730) Qt Lottie Animation: Missing licensing pages
* [QTBUG-137912](https://qt-project.atlassian.net/browse/QTBUG-137912) Support path element combinations
* [QTBUG-140675](https://qt-project.atlassian.net/browse/QTBUG-140675) svgtoqml commandline tool breaks compilation over ssh
* [QTBUG-142319](https://qt-project.atlassian.net/browse/QTBUG-142319) lottietoqml: Fix timing issues
* [QTBUG-142547](https://qt-project.atlassian.net/browse/QTBUG-142547) lottietoqml: Support fill and stroke animations
* [QTBUG-143155](https://qt-project.atlassian.net/browse/QTBUG-143155) Deprecation warnings for qqmlfile
* [QTBUG-139976](https://qt-project.atlassian.net/browse/QTBUG-139976) svgtoqml commandline tool requires window manager
* [QTBUG-140187](https://qt-project.atlassian.net/browse/QTBUG-140187) Missing dependencies for VectorImage when deploying on
Android
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-142792](https://qt-project.atlassian.net/browse/QTBUG-142792) svgtoqml-dependent examples fail to build on macOS in Qt
6.11 snapshot package

### qtquicktimeline
* [QTBUG-136144](https://qt-project.atlassian.net/browse/QTBUG-136144) Qt Quick Timeline: Add alt texts
* [QTBUG-142669](https://qt-project.atlassian.net/browse/QTBUG-142669) RuntimeLoader produces continuous debug output
(“QQuickVector3DValueType… QVariant(Invalid)”) when loading an animated
file
* [QTBUG-131755](https://qt-project.atlassian.net/browse/QTBUG-131755) QML module QtQuick.Timeline.BlendTrees depend on non-
existing QML module QtQuickTimeline
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtquick3d
* [QTBUG-137182](https://qt-project.atlassian.net/browse/QTBUG-137182) Wrong shading rendered for 3D models imported by
RuntimeLoader
* [QTBUG-137445](https://qt-project.atlassian.net/browse/QTBUG-137445) Test #10: test_auto_geometry
......................***Failed    0.34 sec
* [QTBUG-137479](https://qt-project.atlassian.net/browse/QTBUG-137479) Possible null reference in qssgrendernode markdirty
* [QTBUG-136334](https://qt-project.atlassian.net/browse/QTBUG-136334) The documentation of qt6_add_lightprobe_images is
missing
* [QTBUG-137852](https://qt-project.atlassian.net/browse/QTBUG-137852) FAIL!  : qmltest::UnknownTestFunc() Received a fatal
error.
* [QTBUG-137979](https://qt-project.atlassian.net/browse/QTBUG-137979) REG->6.10: widgetgraphgallery produces warnings flood
"Vertex buffer empty"
* [QTBUG-138591](https://qt-project.atlassian.net/browse/QTBUG-138591) Broken font-weight tag
* [QTBUG-136137](https://qt-project.atlassian.net/browse/QTBUG-136137) License of
qtquick3d/src/runtimerender/res/effectlib/fog.glsllib: SPDX header
differs from qt_attribution
* [QTBUG-139033](https://qt-project.atlassian.net/browse/QTBUG-139033) [REG 6.9.2 -> 6.10.0] demos/stockqt and
quick3d/graphs/quick3dphysics examples not compiling on Wasm
singlethread
* [QTBUG-138245](https://qt-project.atlassian.net/browse/QTBUG-138245) FTBFS: qtquick3d's embree 3rd-party
* [QTBUG-139023](https://qt-project.atlassian.net/browse/QTBUG-139023) Having two View3D instances in same window with only one
having lightmaps makes lightmap rendering erratic
* [QTBUG-139232](https://qt-project.atlassian.net/browse/QTBUG-139232) Crash when View3D is destroyed in a multiview case
* [QTBUG-136911](https://qt-project.atlassian.net/browse/QTBUG-136911) 2D items take transformation from random camera if there
are multiple View3Ds into a single scene
* [QTBUG-126098](https://qt-project.atlassian.net/browse/QTBUG-126098) Item2D uses wrong transformation in multiple views
* [QTBUG-139130](https://qt-project.atlassian.net/browse/QTBUG-139130) Nested View3D causes 2D content to not be rendered
* [QTBUG-139175](https://qt-project.atlassian.net/browse/QTBUG-139175) Baking lights in CabinDemo gives a black scene on
Windows
* [QTBUG-139274](https://qt-project.atlassian.net/browse/QTBUG-139274) Loader3D and ComponentBehaviour Bound seem incompatible
* [QTBUG-140392](https://qt-project.atlassian.net/browse/QTBUG-140392) Material.OpaquePrePassDepthDraw Option Causing Graphical
Artifacts with Instancing and CustomMaterial
* [QTBUG-140670](https://qt-project.atlassian.net/browse/QTBUG-140670) Regression: Item2D not updated correctly
* [QTBUG-140662](https://qt-project.atlassian.net/browse/QTBUG-140662) Specular light calculation generates INF color values
* [QTBUG-140107](https://qt-project.atlassian.net/browse/QTBUG-140107) Postproc effects recreate intermediate buffers multiple
times with different sizes
* [QTBUG-139616](https://qt-project.atlassian.net/browse/QTBUG-139616) Setting ExtendedSceneEnvironment.adjustmentContrast
causes scene to go black
* [QTBUG-139324](https://qt-project.atlassian.net/browse/QTBUG-139324) Quick3D Frame view is empty in creator QML profiler
* [QTBUG-140780](https://qt-project.atlassian.net/browse/QTBUG-140780) Setting Sphere Geometry pickable: true, causes crash in
Quick 3D
* [QTBUG-140857](https://qt-project.atlassian.net/browse/QTBUG-140857) Qt Quick3d automatic LoD: Visual Artifacts with enabled
OpaquePrePassDepthDraw on any other object on same scene
* [QTBUG-140855](https://qt-project.atlassian.net/browse/QTBUG-140855) Qt Quick3d automatic LoD not working With CustomMaterial
* [QTBUG-138692](https://qt-project.atlassian.net/browse/QTBUG-138692) QML Quick3D Helper classes are not exported and cannot
be compiled in direct mode
* [QTBUG-140715](https://qt-project.atlassian.net/browse/QTBUG-140715) Qt Quick3d LoD with Instance dirty table is not updated
correctly.
* [QTBUG-140829](https://qt-project.atlassian.net/browse/QTBUG-140829) Touch events from XrView.setTouchpoint() do not work
with TapHandler
* [QTBUG-141224](https://qt-project.atlassian.net/browse/QTBUG-141224) OpenXR: OpenGL render wrong/dull colors
* [QTBUG-141222](https://qt-project.atlassian.net/browse/QTBUG-141222) OpenXR: xrWaitFrame() blocks the main thread
* [QTBUG-141617](https://qt-project.atlassian.net/browse/QTBUG-141617) SkyBoxCubeMap is not tonemapped
* [QTBUG-141876](https://qt-project.atlassian.net/browse/QTBUG-141876) QDoc: error: Documentation warnings (3) exceeded the
limit (1) for 'QtQuick3D'.
* [QTBUG-141921](https://qt-project.atlassian.net/browse/QTBUG-141921) particleshadergen "Failed to compile fragment shader"
during Qt compilation
* [QTBUG-141784](https://qt-project.atlassian.net/browse/QTBUG-141784) SSGI and normal map causes shader compilation failure
* [QTBUG-142145](https://qt-project.atlassian.net/browse/QTBUG-142145) Menu and other Popup items do not work in XR
* [QTBUG-142322](https://qt-project.atlassian.net/browse/QTBUG-142322) Qt Quick 3D: Add alt text
* [QTBUG-142746](https://qt-project.atlassian.net/browse/QTBUG-142746) [Boot to Qt 6.11.0 beta1] quick3d/userpasses example
fails to build
* [QTBUG-142813](https://qt-project.atlassian.net/browse/QTBUG-142813) View3D of qtquick3d/hellocube does not produce visual
output, when building single threaded
* [QTBUG-141960](https://qt-project.atlassian.net/browse/QTBUG-141960) Crash with LinkedList OIT method on macOS
* [QDS-12497](https://qt-project.atlassian.net/browse/QDS-12497) Emissive material RGB Factor slider control maxes out at 16.
* [QTBUG-143491](https://qt-project.atlassian.net/browse/QTBUG-143491) OverrideMaterial in RenderPass is not initialized
* [QTBUG-143106](https://qt-project.atlassian.net/browse/QTBUG-143106) balsam: Difficult to identify which MorphTargets refers
to which blend shape in the original file
* [QTBUG-143480](https://qt-project.atlassian.net/browse/QTBUG-143480) qtquick3d: Build failure on Linux with EGL + Vulkan -
missing EGL/egl.h include in qopenxrplatform_p.h
* [QTBUG-143629](https://qt-project.atlassian.net/browse/QTBUG-143629) Qt 6.11 Beta broken Shadows. The shadowMapFar is not any
effects.
* [QTBUG-144101](https://qt-project.atlassian.net/browse/QTBUG-144101) EmitMode is incorrectly EmitType in docs
* [QTBUG-143886](https://qt-project.atlassian.net/browse/QTBUG-143886) Unexpected behavior of Quaternion.lookAt (NaN output)
* [QTBUG-144116](https://qt-project.atlassian.net/browse/QTBUG-144116) Emit mode doesn't work correctly with particle scene
shape
* [QTBUG-144532](https://qt-project.atlassian.net/browse/QTBUG-144532) Misplaced Qt QUIck 3D example on Qt Creator welcome
screen
* [QTBUG-138170](https://qt-project.atlassian.net/browse/QTBUG-138170) FX & Material Showroom: qmllint warnings
* [QTBUG-138901](https://qt-project.atlassian.net/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-139941](https://qt-project.atlassian.net/browse/QTBUG-139941) DelegateModelAccess.ReadWrite should allow writing to
arrays and sequences as models
* [QTBUG-137048](https://qt-project.atlassian.net/browse/QTBUG-137048) qdoc: Warn about self-link in \sa
* [QTBUG-140023](https://qt-project.atlassian.net/browse/QTBUG-140023) Generated .mesh file does not preserve the original
filename of the input asset.
* [QTBUG-115450](https://qt-project.atlassian.net/browse/QTBUG-115450) qtquick3d -unity-build-batch-size 100000 fails
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-138065](https://qt-project.atlassian.net/browse/QTBUG-138065) Alpha blend render wrong with sourceItem
* [QTBUG-142917](https://qt-project.atlassian.net/browse/QTBUG-142917) Prepare Quad Renderer before using it
* [QTBUG-143094](https://qt-project.atlassian.net/browse/QTBUG-143094) The StaticRigidBody  is not refreshed after changing
source geometry object.
* [QTBUG-143916](https://qt-project.atlassian.net/browse/QTBUG-143916) Fix QDoc warnings for Qt 6.11

### qtshadertools
* [QTBUG-141348](https://qt-project.atlassian.net/browse/QTBUG-141348) ERROR: AddressSanitizer: stack-buffer-overflow
* [QTBUG-135281](https://qt-project.atlassian.net/browse/QTBUG-135281) Qml Camera not work on webassembly
* [QTBUG-138901](https://qt-project.atlassian.net/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qt5compat
* [QTBUG-71541](https://qt-project.atlassian.net/browse/QTBUG-71541) ColorOverlay documentation refers to wrong color format
* [QTBUG-136146](https://qt-project.atlassian.net/browse/QTBUG-136146) Qt 5 Core Compatibility: Add alt texts
* [QTBUG-138901](https://qt-project.atlassian.net/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist

### qtcoap
* [QTBUG-139697](https://qt-project.atlassian.net/browse/QTBUG-139697) Provide a public "bind" API for QCoapClient, or at least
filter out unexpected replies not from peer
* [QTBUG-138901](https://qt-project.atlassian.net/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtmqtt
* [QTBUG-135653](https://qt-project.atlassian.net/browse/QTBUG-135653) MessageReceived not fired when subscribing again to just
unsubscribed topic
* [QTBUG-137305](https://qt-project.atlassian.net/browse/QTBUG-137305) MQTT tests emits QSocketNotifier: Invalid socket
specified
* [QTBUG-138901](https://qt-project.atlassian.net/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtopcua
* [QTBUG-136141](https://qt-project.atlassian.net/browse/QTBUG-136141) Header files not listed in Qt OPC UA example
documentation
* [QTBUG-142401](https://qt-project.atlassian.net/browse/QTBUG-142401) Decide on
qt_opcua_disable_optimizations_in_current_dir()
* [QTBUG-85939](https://qt-project.atlassian.net/browse/QTBUG-85939) Qt Opcua failing tests on Windows MSVC when building with
CMake
* [QTBUG-142499](https://qt-project.atlassian.net/browse/QTBUG-142499) [FTBFS] Unknown CMake command
"qt_opcua_generate_datatypes"
* [QTBUG-137701](https://qt-project.atlassian.net/browse/QTBUG-137701) Connecting to unsecured endpoint results in
ClientError::UnknownError
* [QTBUG-138754](https://qt-project.atlassian.net/browse/QTBUG-138754) Build fails with Qt OPC UA when OpenSSL 1.1 is supported
* [QTBUG-138901](https://qt-project.atlassian.net/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-139354](https://qt-project.atlassian.net/browse/QTBUG-139354) OpcUA tests fail on macOS 26
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qthttpserver
* [QTBUG-137849](https://qt-project.atlassian.net/browse/QTBUG-137849) FAIL!  : tst_QHttpServerMultithreaded::initTestCase()
'localserver->listen(local)' returned FALSE. (Local server listen
failed)
* [QTBUG-136155](https://qt-project.atlassian.net/browse/QTBUG-136155) Qt HTTP Server: Add alt texts
* [QTBUG-137330](https://qt-project.atlassian.net/browse/QTBUG-137330) QtHttpServer: Writing from Sequential QIODevices to
HTTP(S)/1.1 Hangs the Client
* [QTBUG-108127](https://qt-project.atlassian.net/browse/QTBUG-108127) Handlers returning QFuture<void> should have access to
QHttpServerResponder, which should be made thread-safe
* [QTBUG-141875](https://qt-project.atlassian.net/browse/QTBUG-141875) FAIL!  : tst_QHttpServer::timeoutConnection(http/1.1)
Compared values are not the same
* [QTBUG-138410](https://qt-project.atlassian.net/browse/QTBUG-138410) QtHttpServer: The HTTP/1.0 support is incomplete
* [QTBUG-138611](https://qt-project.atlassian.net/browse/QTBUG-138611) QtHttpServer has out of order writes because it starts
handling the next HTTP/1 request before it's done writing from QIODevice
* [QTBUG-142127](https://qt-project.atlassian.net/browse/QTBUG-142127) QtHttpServer: Tests of size limiting of incoming
requests are flaky on Windows
* [QTBUG-143202](https://qt-project.atlassian.net/browse/QTBUG-143202) QtHttpServer: Fix remaining flaky tests
* [QTBUG-143595](https://qt-project.atlassian.net/browse/QTBUG-143595) [Examples] 'Simple HTTP Server' example is not listed
under networking examples

### qtquick3dphysics
* [QTBUG-139437](https://qt-project.atlassian.net/browse/QTBUG-139437) multiple definition of CapsuleGeometry
* [QTBUG-141066](https://qt-project.atlassian.net/browse/QTBUG-141066) test_auto_callback (Failed)
* [QTBUG-138901](https://qt-project.atlassian.net/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qtgrpc
* [QTBUG-137313](https://qt-project.atlassian.net/browse/QTBUG-137313) Build fails if using QML and GENERATE_PACKAGE_SUBFOLDERS
in qt_add_grpc
* [QTBUG-138179](https://qt-project.atlassian.net/browse/QTBUG-138179) Qt GRPC documentation: \gRPC macro doesnt' work
* [QTBUG-138180](https://qt-project.atlassian.net/browse/QTBUG-138180) Qt GRPC: Weird duplications in documentation tree
* [QTBUG-138494](https://qt-project.atlassian.net/browse/QTBUG-138494) GRPC, QHttp2Channel: Implement metadata handling
according to protocol
* [QTBUG-129160](https://qt-project.atlassian.net/browse/QTBUG-129160) QtGrpc: improve lifetime-management of Http2Handler
* [QTBUG-138039](https://qt-project.atlassian.net/browse/QTBUG-138039) QtGrpc: deprecate QHash server metadata interface
* [QTBUG-138683](https://qt-project.atlassian.net/browse/QTBUG-138683) Protobuf: repeated enum fields are serialized
incorrectly
* [QTBUG-139597](https://qt-project.atlassian.net/browse/QTBUG-139597) QtGrpc: QGrpcHttp2Channel should guarantee
transportation scheme
* [QTBUG-129286](https://qt-project.atlassian.net/browse/QTBUG-129286) GRPC: Implement HTTP/2 dataframe decompression
* [QTBUG-141780](https://qt-project.atlassian.net/browse/QTBUG-141780) Top flaky test:
QtGrpcClientEnd2EndTest::clientHandlesCompression
* [QTBUG-142670](https://qt-project.atlassian.net/browse/QTBUG-142670) QtGrpc: finalize Interceptor implementation
* [QTBUG-144204](https://qt-project.atlassian.net/browse/QTBUG-144204) QtGrpc API-Review 6.11: Resolve deprecation of
QGrpcOperationContext::argument()
* [QTBUG-138901](https://qt-project.atlassian.net/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-138812](https://qt-project.atlassian.net/browse/QTBUG-138812) Doc: Improve security documentation of Qt GRPC
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-141872](https://qt-project.atlassian.net/browse/QTBUG-141872) QDoc: error: Documentation warnings (2) exceeded the
limit (0) for 'QtProtobuf'.
* [QTBUG-142473](https://qt-project.atlassian.net/browse/QTBUG-142473) Linear memory growth observed with Qt GRPC during long
run
* [QTBUG-132876](https://qt-project.atlassian.net/browse/QTBUG-132876) Add the range and sign check for the
google.protobuf.Duration
* [QTBUG-96239](https://qt-project.atlassian.net/browse/QTBUG-96239) Document CMake component in CMake function documentation

### qtquickeffectmaker
* [QTBUG-143111](https://qt-project.atlassian.net/browse/QTBUG-143111) 'Qt Quick Effect Maker' two-level entry in documentation
tree
* [QTBUG-140905](https://qt-project.atlassian.net/browse/QTBUG-140905) [REG: 6.9.1 -> 6.10] Del key not usable in QQEM code
editor

### qtgraphs
* [QTBUG-137446](https://qt-project.atlassian.net/browse/QTBUG-137446) ERROR: AddressSanitizer: heap-use-after-free on address
0x611000024be8
* [QTBUG-138257](https://qt-project.atlassian.net/browse/QTBUG-138257) Code snippet for PieModelMapper uses undefined
properties
* [QTBUG-137718](https://qt-project.atlassian.net/browse/QTBUG-137718) XYSeries: opacity property has no effect
* [QTBUG-137716](https://qt-project.atlassian.net/browse/QTBUG-137716) QLineSeries: Property documentation is missing
* [QTBUG-133759](https://qt-project.atlassian.net/browse/QTBUG-133759) the Custom3DItem position is not correct when setting
"axisZ.reversed: true" in QtGraphs
* [QTBUG-136174](https://qt-project.atlassian.net/browse/QTBUG-136174) 3D bars graph endless sync loop
* [QTBUG-138470](https://qt-project.atlassian.net/browse/QTBUG-138470) SurfaceGallery does not start properly
* [QTBUG-138384](https://qt-project.atlassian.net/browse/QTBUG-138384) Incorrect documentation about one row surfaces
* [QTBUG-138492](https://qt-project.atlassian.net/browse/QTBUG-138492) qdoc: Snippet indentation issues
* [QTBUG-138462](https://qt-project.atlassian.net/browse/QTBUG-138462) QtGraphs pollutes the global namespace
* [QTBUG-138598](https://qt-project.atlassian.net/browse/QTBUG-138598) Setting series axis to null doesn't update the sizing
* [QTBUG-138810](https://qt-project.atlassian.net/browse/QTBUG-138810) Crash upon initialization in tst_surfacetest
* [QTBUG-138740](https://qt-project.atlassian.net/browse/QTBUG-138740) Only bar graph works correctly with horizontal graph
orientation
* [QTBUG-138827](https://qt-project.atlassian.net/browse/QTBUG-138827) OIT causes artefacts in text rendering
* [QTBUG-138797](https://qt-project.atlassian.net/browse/QTBUG-138797) Docs are messed up with * in some places
* [QTBUG-138506](https://qt-project.atlassian.net/browse/QTBUG-138506) QtGraphs crash when GraphView is destroyed
* [QTBUG-138923](https://qt-project.atlassian.net/browse/QTBUG-138923) Gradient range doesn't update with aspectRatio
* [QTBUG-138924](https://qt-project.atlassian.net/browse/QTBUG-138924) Gradient does not work when starting up the app in some
cases
* [QTBUG-134003](https://qt-project.atlassian.net/browse/QTBUG-134003) QtGraphs pieSize and holeSize validate and render
differently
* [QTBUG-137272](https://qt-project.atlassian.net/browse/QTBUG-137272) Bars example doesn't display column categories correctly
* [QTBUG-139112](https://qt-project.atlassian.net/browse/QTBUG-139112) QtGraphs AreaSeries inconsistent area filling
* [QTBUG-138822](https://qt-project.atlassian.net/browse/QTBUG-138822) Reusing same ValueAxis in multiple GraphViews results in
a crash
* [QTBUG-138755](https://qt-project.atlassian.net/browse/QTBUG-138755) Can't distinguish between multiple axis
* [QTBUG-140240](https://qt-project.atlassian.net/browse/QTBUG-140240) Rendering of Surface3DSeries crashes when the first row
is all NaN
* [QTBUG-140088](https://qt-project.atlassian.net/browse/QTBUG-140088) tst_qgqml2dtest (Failed)
* [QTBUG-140660](https://qt-project.atlassian.net/browse/QTBUG-140660) Transparency does not work in textureFile in
Surface3DSeries
* [QTBUG-140904](https://qt-project.atlassian.net/browse/QTBUG-140904) The QValue3DAxis::setReversed() function is not working
properly in the surface graph.
* [QTBUG-135931](https://qt-project.atlassian.net/browse/QTBUG-135931) Reg[6.8.2-6.9.0]ListView containing AbstractSeries does
not scroll on Drag
* [QTBUG-141067](https://qt-project.atlassian.net/browse/QTBUG-141067) tst_qgqmltest (Failed)
* [QTBUG-141186](https://qt-project.atlassian.net/browse/QTBUG-141186) Axis handling example keeps printing scale data warning
* [QTBUG-141370](https://qt-project.atlassian.net/browse/QTBUG-141370) Setting selection item label visibility to false does
not work for Scatter 3D
* [QTBUG-140202](https://qt-project.atlassian.net/browse/QTBUG-140202) Axis titles overlap axis lines with multiple axis
* [QTBUG-141518](https://qt-project.atlassian.net/browse/QTBUG-141518) [REG 6.10.0->6.10.1] graphs/graphprinting configure
fails
* [QTBUG-141687](https://qt-project.atlassian.net/browse/QTBUG-141687) Scatter instancing crash when selecting
* [QTBUG-141698](https://qt-project.atlassian.net/browse/QTBUG-141698) Generate OpenGL ES 3 shaders for qsb files in
graphs/2d/cockpit/
* [QTBUG-141927](https://qt-project.atlassian.net/browse/QTBUG-141927) GridLine.qml uses deprecated material type
* [QTBUG-142047](https://qt-project.atlassian.net/browse/QTBUG-142047) Render slice to image does not show labels correctly
* [QTBUG-134007](https://qt-project.atlassian.net/browse/QTBUG-134007) wrong X direction for Quaternion.lookAt
* [QTBUG-142454](https://qt-project.atlassian.net/browse/QTBUG-142454) Surface Gallery oscilloscope demo slice view sometimes
stays incorrectly visible
* [QTBUG-142437](https://qt-project.atlassian.net/browse/QTBUG-142437) XYModelMapper produces unavoidable warning if
xSection/ySection uses property bindings
* [QTBUG-142418](https://qt-project.atlassian.net/browse/QTBUG-142418) Surface graph crash when trying to render a column slice
into image
* [QTBUG-142696](https://qt-project.atlassian.net/browse/QTBUG-142696) Using 3D graphs in Qt Quick projects created with
QtCreator do not show even the Window
* [QTBUG-142918](https://qt-project.atlassian.net/browse/QTBUG-142918) graph isnt updating when upper or lower series is
switched
* [QTBUG-142923](https://qt-project.atlassian.net/browse/QTBUG-142923) Adjusting barThickness or barSpacing does not trigger
redraw
* [QTBUG-143351](https://qt-project.atlassian.net/browse/QTBUG-143351) Axis labels do not get the correct label color in some
cases
* [QTBUG-142814](https://qt-project.atlassian.net/browse/QTBUG-142814) Theme updates do not take effect if the theme is shared
with several 3D graphs
* [QTBUG-138863](https://qt-project.atlassian.net/browse/QTBUG-138863) selectedPoint in Surface3DSeries does not work
* [QTBUG-143358](https://qt-project.atlassian.net/browse/QTBUG-143358) Items are not always cropped if they are outside the
axis range
* [QTBUG-143484](https://qt-project.atlassian.net/browse/QTBUG-143484) Floor size is not updated with margins in Bars3D
* [QTBUG-143548](https://qt-project.atlassian.net/browse/QTBUG-143548) LegendData doesn't update to reflect on explicit series
color if set on runtime
* [QTBUG-142944](https://qt-project.atlassian.net/browse/QTBUG-142944) Graphs3D.GridLineType.Shader renders incorrectly
* [QTBUG-143481](https://qt-project.atlassian.net/browse/QTBUG-143481) Custom graph does not update when graph dimensions
change
* [QTBUG-143579](https://qt-project.atlassian.net/browse/QTBUG-143579) Custom graph prints out null errors during
initialization
* [QTBUG-143866](https://qt-project.atlassian.net/browse/QTBUG-143866) A crash in axisrenderer when switching between graphs
* [QTBUG-143611](https://qt-project.atlassian.net/browse/QTBUG-143611) Weird behaviour in surface
* [QTBUG-143741](https://qt-project.atlassian.net/browse/QTBUG-143741) tst_barstest Camera target sliders are not updating
graph position
* [QTBUG-143750](https://qt-project.atlassian.net/browse/QTBUG-143750) setRotation in QBarDataItem does not trigger a redraw
* [QTBUG-143740](https://qt-project.atlassian.net/browse/QTBUG-143740) Floor grid is not updated when floor level is adjusted
in Bars3D
* [QTBUG-143751](https://qt-project.atlassian.net/browse/QTBUG-143751) setMeshAngle in QBar3DSeries causes rendering errors
* [QTBUG-143865](https://qt-project.atlassian.net/browse/QTBUG-143865) Graphprinting and Aerospacehub examples are configured
incorrectly
* [QTBUG-135811](https://qt-project.atlassian.net/browse/QTBUG-135811) Graphs BarSeries only displays values does not show
labels
* [QTBUG-138456](https://qt-project.atlassian.net/browse/QTBUG-138456) Documentation contains references to "QGraphsView" which
is a private class
* [QTBUG-139560](https://qt-project.atlassian.net/browse/QTBUG-139560) Access functions are documented even when their
properties are not
* [QTBUG-138828](https://qt-project.atlassian.net/browse/QTBUG-138828) Programmatic slicing does not work
* [QTBUG-140843](https://qt-project.atlassian.net/browse/QTBUG-140843) PieSeries hoverable crashing
* [QTBUG-140174](https://qt-project.atlassian.net/browse/QTBUG-140174) Qt Graphs test errors resulting from TestNamespace
* [QTBUG-141560](https://qt-project.atlassian.net/browse/QTBUG-141560) qtgraphs: tracepoint build fails
* [QTBUG-134641](https://qt-project.atlassian.net/browse/QTBUG-134641) the Custom3DItem is still in Scatter3D after it is
deleted by removeCustomItem
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-143241](https://qt-project.atlassian.net/browse/QTBUG-143241) API review: QVector is just QList
* [QTBUG-143240](https://qt-project.atlassian.net/browse/QTBUG-143240) API review: Fix minor format issues
* [QTBUG-143244](https://qt-project.atlassian.net/browse/QTBUG-143244) API Review: optimized is an adjective
* [QTBUG-143242](https://qt-project.atlassian.net/browse/QTBUG-143242) API Review: Don't use private Q_SLOTS
* [QTBUG-143243](https://qt-project.atlassian.net/browse/QTBUG-143243) API review: What does release mean
* [QTBUG-137392](https://qt-project.atlassian.net/browse/QTBUG-137392) Update not taken in account on selected pie in PieChart
* [QTBUG-143251](https://qt-project.atlassian.net/browse/QTBUG-143251) API Review: Don't add operator<< directly to a class for
appending
* [QTBUG-143258](https://qt-project.atlassian.net/browse/QTBUG-143258) API Review: Should the timeZone be QTimeZone instead of
string
* [QTBUG-142020](https://qt-project.atlassian.net/browse/QTBUG-142020) Incorrect usage of qFuzzyCompare() abounds in Qt source
[QtCore]
* [QTBUG-143622](https://qt-project.atlassian.net/browse/QTBUG-143622) Incorrect usage of qFuzzyCompare() abounds in Qt source
[QtGraphs and QtDatavis]
* [QTBUG-143860](https://qt-project.atlassian.net/browse/QTBUG-143860) API Review: The changed signal argument cannot have the
same name as the property they are signaling for

### qttasktree
* [QTBUG-142004](https://qt-project.atlassian.net/browse/QTBUG-142004) TaskTree: Link to module in documentation
* [QTBUG-142003](https://qt-project.atlassian.net/browse/QTBUG-142003) TaskTree: Do not linkify all instances of TaskTree
* [QTBUG-142258](https://qt-project.atlassian.net/browse/QTBUG-142258) TaskTree: Add \since information
* [QTBUG-142259](https://qt-project.atlassian.net/browse/QTBUG-142259) TaskTree: Document module status
* [QTBUG-142262](https://qt-project.atlassian.net/browse/QTBUG-142262) sbom\qttasktree-6.11.0.source.spdx file missing

### qtopenapi
* [QTBUG-141898](https://qt-project.atlassian.net/browse/QTBUG-141898) FAIL!  : QtOpenAPI::StoreApiTests::timeoutTest()
'netError == QNetworkReply::OperationCanceledError' returned FALSE.
* [QTBUG-142149](https://qt-project.atlassian.net/browse/QTBUG-142149) .gitignore file in 6.11 qtopenapi src
* [QTBUG-142251](https://qt-project.atlassian.net/browse/QTBUG-142251) ninja: error: loading 'build.ninja': No such file or
directory
* [QTBUG-142540](https://qt-project.atlassian.net/browse/QTBUG-142540) Client is not regenerated when the spec file content
changes
* [QTWEBSITE-1264](https://qt-project.atlassian.net/browse/QTWEBSITE-1264) Qt Open API documentation is not generated
* [QTBUG-142907](https://qt-project.atlassian.net/browse/QTBUG-142907) Fix memleaks in the generated code
* [QTBUG-142545](https://qt-project.atlassian.net/browse/QTBUG-142545) Configuring qtopenapi does not find openapi-generator-
cli
* [QTBUG-143165](https://qt-project.atlassian.net/browse/QTBUG-143165) Add possibility to generate code from the large yaml
files by qt_add_openapi_client macro
* [QTBUG-141841](https://qt-project.atlassian.net/browse/QTBUG-141841) Investigate the test output problem on windows
* [QTBUG-141948](https://qt-project.atlassian.net/browse/QTBUG-141948) {{prefix}}ServerConfiguration::URL() is never used
* [QTBUG-142230](https://qt-project.atlassian.net/browse/QTBUG-142230) CMake Error at
src/openapi/Qt6OpenApiGeneratorMacros.cmake
* [QTBUG-142395](https://qt-project.atlassian.net/browse/QTBUG-142395) Common library should use {{commonPrefix}}, not
{{prefix}}
* [QTBUG-143168](https://qt-project.atlassian.net/browse/QTBUG-143168) Model property names collision
* [QTBUG-143180](https://qt-project.atlassian.net/browse/QTBUG-143180) FreeFormObject type should be taken into account for
bodyParams in function {{nickname}}WithDataImpl()
* [QTBUG-143176](https://qt-project.atlassian.net/browse/QTBUG-143176) Base Object class should not be abstract
* [QTBUG-143310](https://qt-project.atlassian.net/browse/QTBUG-143310) Document Qt OpenAPI as technical preview
* [QTBUG-143309](https://qt-project.atlassian.net/browse/QTBUG-143309) qt_add_openapi_client() command is undocumented
* [QTBUG-143683](https://qt-project.atlassian.net/browse/QTBUG-143683) A few Qt OpenAPI generator configuration options should
be fixed
* [QTBUG-143166](https://qt-project.atlassian.net/browse/QTBUG-143166) Add possibility to add a list of additional-properties
via qt_add_openapi_client macro

### qtcanvaspainter
* [QTBUG-142442](https://qt-project.atlassian.net/browse/QTBUG-142442) [REG 6.10.0->6.11.0]  -DFEATURE_gui=OFF build fails,
qtcanvaspainter
* [QTBUG-142458](https://qt-project.atlassian.net/browse/QTBUG-142458) Canvas Painter: Document CMake API in class
documentation
* [QTBUG-142457](https://qt-project.atlassian.net/browse/QTBUG-142457) Canvas Painter: Add \since information
* [QTBUG-143315](https://qt-project.atlassian.net/browse/QTBUG-143315) QCPainter: Broken text rendering in Windows CI VMs with
OpenGL
* [QTBUG-142461](https://qt-project.atlassian.net/browse/QTBUG-142461) Canvas Painter: Add overview
* [QTBUG-143843](https://qt-project.atlassian.net/browse/QTBUG-143843) addImage - removeImage - cacheMemoryUsage discrepancies

### qtapplicationmanager (Commercial only)
* [QTBUG-137056](https://qt-project.atlassian.net/browse/QTBUG-137056) Qt Application Manager - WindowObject Resizing Issue (Qt
6.8.3+)
* [QTBUG-138107](https://qt-project.atlassian.net/browse/QTBUG-138107) windowmanager.cpp:305:36: error: no member named
'setSlowModeEnabled' in 'TestNamespace::QUnifiedTimer'
* [QTBUG-130554](https://qt-project.atlassian.net/browse/QTBUG-130554) tst_Signature::check() fails on macOS 15
* [QTBUG-129127](https://qt-project.atlassian.net/browse/QTBUG-129127) Fix problems with the new am_package CMake macros
* [QTBUG-142798](https://qt-project.atlassian.net/browse/QTBUG-142798) error: no member named 'disableDeprecationWarnings' in
'QtAM::YamlParser'
* [QTBUG-136961](https://qt-project.atlassian.net/browse/QTBUG-136961) qtapplicationmanager: bubblewrap-example may need
bubblewarp
* [QTBUG-143054](https://qt-project.atlassian.net/browse/QTBUG-143054) meta-qt6 should support reproduce build

### qtinsighttracker (Commercial only)
* [QTBUG-140160](https://qt-project.atlassian.net/browse/QTBUG-140160) FAIL!  : tst_QInsightEventFilter::trackEvents(button.ui)
Compared values are not the same
* [QTBUG-141924](https://qt-project.atlassian.net/browse/QTBUG-141924) QDoc: error: Documentation warnings (19) exceeded the
limit (10) for 'QtInsightTracker'

### qtvncserver (Commercial only)
* [QTBUG-138461](https://qt-project.atlassian.net/browse/QTBUG-138461) Rotated VncItem input/visual mismatch in
GrabItemRectangle mode

### qmlcompilerplus (Commercial only)
* [QTBUG-139431](https://qt-project.atlassian.net/browse/QTBUG-139431) Miscompilation of lists of inline components
* [QTBUG-143037](https://qt-project.atlassian.net/browse/QTBUG-143037) QML: Enum class properties cannot be compiled with
--direct-calls
* [QTBUG-144300](https://qt-project.atlassian.net/browse/QTBUG-144300) tst_codegen_indirect (Failed)
* [QTBUG-135795](https://qt-project.atlassian.net/browse/QTBUG-135795) QML Locale cannot be compiled in Direct Mode

Known Issues
------------
* Check that your system meets Qt's requirements:
  https://doc-snapshots.qt.io/qt6-6.11/supported-platforms.html
* RTA reported issues from Qt 6.11
  https://qt-project.atlassian.net/issues?filter=21382
* See Qt 6.11 known issues from:
  https://wiki.qt.io/Qt_6.11_Known_Issues
* Qt 6.11.0 Open issues in Jira:
  https://qt-project.atlassian.net/issues?filter=21383

Credits for the release goes to:
---------------------------------

Eirik Aavitsland  
Cristian Adam  
Chris Adams  
Laszlo Agocs  
Owais Akhtar  
Dmitrii Akshintsev  
Alexander Akulich  
Konsta Alajärvi  
Stanislav Aleksandrov  
Anu Aliyas  
Even Oscar Andersen  
Purdea Andrei  
Dimitrios Apostolou  
Soheil Armin  
Albert Astals Cid  
Xavier BESSON  
Mate Barany  
Thierry Bastian  
Sebastian Beckmann  
Andreas Belke  
Vladimir Belyavsky  
Nicholas Bennett  
Lena Biliaieva  
Tim Blechmann  
Maximilian Blochberger  
Eskil Abrahamsen Blomfeldt  
David Boddie  
Tatiana Borisova  
Joerg Bornemann  
Rym Bouabid  
Assam Boudjelthia  
Marcell Brauner  
Aurélien Brooke  
Kai Uwe Broulik  
Michael Brüning  
Alex Bu  
Eren Bursali  
Olivier De Cannière  
Méven Car  
Alexei Cazacov  
Li Changze  
Kaloyan Chehlarski  
Luqiao Chen  
Michael Cho  
Wang Chuan  
Ece Cinucen  
Jonathan Clark  
Paul Colby  
Alexandru Croitor  
Mitch Curtis  
Thibaut Cuvelier  
Giuseppe D'Angelo  
Szabolcs David  
Pavel Dubsky  
Artem Dyomin  
Alexey Edelev  
David Edmundson  
Oliver Eftevaag  
Christian Ehrlicher  
Hatem ElKharashy  
Andreas Eliasson  
Fabio Falsini  
David Faure  
Ilya Fedin  
Nicolas Fella  
Tobias Fella  
Simo Fält  
Joshua GPBeta  
Samuel Gaist  
Zoltan Gera  
John Paul Adrian Glaubitz  
Joshua Goins  
Julian Greilich  
Robert Griebl  
Jan Grulich  
Johannes Grunenberg  
Kaj Grönholm  
Nicolas Guichard  
Richard Moe Gustavsen  
Lucie Gérard  
Mikko Hallamaa  
Inkamari Harjula  
Andre Hartmann  
Andreas Hartmetz  
Elias Hautala  
Jani Heikkinen  
Tero Heikkinen  
Miikka Heikkinen  
Moss Heim  
Christian Heimlich  
Liu Heng  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Dominik Holland  
Benedikte Holm  
Mats Honkamaa  
Xaver Hugl  
Jimi Huotari  
Samuli Hölttä  
Riccardo Ieva  
Thorbjørn Martsum / Mjølner Informatics  
Masoud Jami  
Morteza Jamshidi  
Johnny Jazeix  
Allan Sandfeld Jensen  
Jukka Jokiniva  
Jaeyoon Jung  
Christian Kandeler  
Jonas Karlsson  
Ilya Katsnelson  
Dmitry Kazakov  
Rainer Keller  
Igor Khanin  
Ahmed El Khazari  
Ali Kianian  
Dennis Kim  
Marius Kittler  
Friedemann Kleint  
André Klitzing  
Michal Klocek  
Ingo Klöcker  
Jarek Kobus  
Sze Howe Koh  
Jarkko Koivikko  
Antti Kokko  
Niko Korkala  
Tomi Korpipää  
Jani Korteniemi  
Fabian Kosmale  
Volker Krause  
Mike Krus  
Anton Kudryavtsev  
Kai Köhne  
Antonio Larrosa  
Cristian Le  
Inho Lee  
Frédéric Lefebvre  
Wladimir Leuschner  
Xiong LinLin  
Jie Liu  
David Loki  
Pawel Lopko  
Robert Löhning  
Thiago Macieira  
Marco Martin  
Sergio Martins  
Aaron McCarthy  
Shveta Mittal  
Jan Moeller  
Safiyyah Moosa  
Sheree Morphett  
Stan Morris  
Bartlomiej Moskal  
Kenji Mouri  
Marc Mutz  
Antti Määttä  
Martin Negyokru  
Andy Nichols  
Markku Nokkala  
Mårten Nordheim  
Dennis Oberst  
Matti Paaso  
Kwanghyo Park  
Jerome Pasion  
Miika Pernu  
Mauro Persano  
Samuli Piippo  
Karim Pinter  
Timur Pocheptsov  
Lauri Pohjanheimo  
Joni Poikelin  
Aleix Pol  
Jacek Poplawski  
Gleb Popov  
Alessandro Portale  
Rami Potinkara  
Lorn Potter  
Sakaria Pouke  
Shyamnath Premnadh  
Dheerendra Purohit  
MohammadHossein Qanbari  
Liang Qi  
Florian RICHER  
Khem Raj  
Matthias Rauter  
David Redondo  
Arno Rehn  
Topi Reinio  
Konstantin Ritt  
Kaarle Ritvanen  
David Rosca  
Bernhard Rosenkränzer  
Shawn Rutledge  
Otto Ryynänen  
Toni Saario  
Ahmad Samir  
Timon Sassor  
Lars Schmertmann  
Carl Schwan  
Michal Seben  
SanthoshKumar Selvaraj  
Mike Senter  
Thomas Senyk  
Luca Di Sera  
Nick Shaforostov  
Sami Shalayel  
Tian Shilin  
Venugopal Shivashankar  
Kristoffer Skau  
Nils Petter Skålerud  
Daniel Smith  
Ivan Solovev  
Axel Spoerl  
Stefan Steinwasser  
Magdalena Stojek  
Christian Strømme  
Tarja Sundqvist  
Lars Sutterud  
Tasuku Suzuki  
Michael Szczerba  
Błażej Szczygieł  
Jan Arve Sæther  
Morten Sørvig  
Sadegh Taghavi  
Nodir Temirkhodjaev  
Aleksandr Timofeev  
Elias Toivola  
Jens Trillmann  
Jere Tuliniemi  
Paul Olav Tvete  
Esa Törmänen  
Tuomas Vaarala  
Sami Varanka  
Peter Varga  
BogDan Vatra  
Bror Wetlesen Vedeld  
Doris Verria  
Tor Arne Vestbø  
Petri Virkkunen  
Ville Voutilainen  
Juha Vuolle  
Olli Vuolteenaho  
Jaishree Vyas  
Jannis Völker  
Miao Wang  
Yixue Wang  
Michael Weghorn  
Bernd Weimer  
Edward Welbourne  
Paul Wicking  
Piotr Wierciński  
Oliver Wolff  
Lu YaNing  
Andrei Yankovich  
Semih Yavuz  
Andri Yngvason  
Jasuhan Yoganathan  
Marianne Yrjänä  
He YuMing  
Zhao Yuhang  
Erin of Yukis  
Vlad Zahorodnii  
Oleksii Zbykovskyi  
Alexey Zerkin  
JiDe Zhang  
Liu Zheng  
Wang Zichong  
Nic Zonta  
hjk  
Johanna Äijälä  
Jouni Äijälä  
Dilek Akçay Öztüzün  
Daniel Čejchan  
