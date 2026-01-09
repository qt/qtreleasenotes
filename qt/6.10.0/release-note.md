Release note
============
Qt 6.10 introduces many new features and improvements as well as bugfixes
over the 6.9.x series. For more details, refer to the online
documentation included in this distribution. The documentation is also
available online:

https://doc-snapshots.qt.io/qt6-6.10/

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
* [CVE-2025-3512](https://nvd.nist.gov/vuln/detail/CVE-2025-3512) in qtbase
* [CVE-2025-4211](https://nvd.nist.gov/vuln/detail/CVE-2025-4211) in qtbase
* [CVE-2025-5455](https://nvd.nist.gov/vuln/detail/CVE-2025-5455) in qtbase
* [CVE-2025-5992](https://nvd.nist.gov/vuln/detail/CVE-2025-5992) in qtbase
* [CVE-2025-6338](https://nvd.nist.gov/vuln/detail/CVE-2025-6838) in qtbase
* [CVE-2025-30348](https://nvd.nist.gov/vuln/detail/CVE-2025-30348) in qtbase
* [CVE-2025-23050](https://www.cve.org/CVERecord?id=CVE-2025-23050) in qtconnectivity
* [CVE-2025-5683](https://nvd.nist.gov/vuln/detail/CVE-2025-5683) in qtimageformats
* [CVE-2025-10728](https://nvd.nist.gov/vuln/detail/CVE-2025-10728) in qtsvg
* [CVE-2025-10729](https://nvd.nist.gov/vuln/detail/CVE-2025-10729) in qtsvg


### qtbase
* bde2292247b Add primary RGB color points getter
Added primary points getter and setter

* f3d5bdf4bcf SQLite: Update SQLite to v3.47.2
Updated SQLite to v3.47.2

* 357c64a9960 QWidgetWindow: send QContextMenuEvent even after accepted
mouse press
If your QWidget subclass depends on receiving QContextMenuEvent, and
also handles mouse events directly, we recommend that you call ignore()
on unhandled mouse events (such as right-button events). In Qt 7, we
plan to stop sending QContextMenuEvent if the triggering mouse event is
accepted.

* 56faffd92bf QStringView: fix construction from arrays of unknown size
Made construction from arrays of unknown size compile. Such arrays will
use the const Char* constructor, determining the size of the array at
runtime.

* 734bd05d0a6 Q{Any,Utf8}StringView: fix construction from arrays of
unknown size
Made construction from arrays of unknown size compile. Such arrays will
use the const Char* constructor, determining the size of the array at
runtime.

* 5def8ff180c qstringfwd.h: don't include qglobal.h
The qstringfwd.h header no longer includes qglobal.h. A backwards-
compatible fix is to include qglobal.h yourself instead of relying on
the transitive include.

* 11518e92c2b Provide D-Bus de-/marshalling operators for std::tuple
Added generic support for marshalling and demarshalling D-Bus STRUCTs
from/to std::tuple.

* 1299aaa231b QNCM[Mac]: Update from SCNetworkReachability to Network
framework
Replace deprecated SCNetworkReachability implementation with Network
framework (iOS, macOS)

* 54d47f8390c QByteArrayView: add a ctor for arrays of unknown bounds
Made construction from arrays of unknown size compile. Such arrays will
use the const Byte* constructor, determining the size of the array at
runtime.

* 7de17a91bcc Make dumpObjectTree() and dumpObjectInfo() invokable from
QML
QObject::dumpObjectTree() and QObject::dumpObjectInfo() are now
invokable, allowing them to be used from QML.

* 08320bfe2b7 QDebug: make std::optional stream operator SCARY
The std::optional streaming operator is now a member of QDebug, not a
free function. This breaks users that rely on the exact definition of
the operator (e.g. `operator<<(d, opt)`). A backwards-compatible fix is
to call the operator with infix notation (d << opt) only, and to avoid
const QDebug objects.

* fbbf4ace018 CMake: Split off private module config packages
Private Qt modules have been split off into separate Qt6FooPrivate
CMake config packages. A call to find_package(Qt6Foo) will now
implicitly find_package(Qt6FooPrivate). It's not an error if
Qt6FooPrivate isn't available as it may be the case on certain Linux
distros that split their Qt module packages into private and public
parts.

* 1a5afe625be Update bundled libjpeg-turbo to version 3.1.0
libjpeg-turbo was updated to version 3.1.0

* 8928b0fbb9c QCommandLineParser: include the positional arguments'
sizes in --help
Made it so the positional argument descriptions are taken into account
in the aligning of text for helpText().

* 5b07e3de3fe QSqlDriver: return the connection name of the assoicated
QSqlDatabase
Added connectionName() which returns the connection name of the
associated QSqlDatabase instance.

* 1bd883dbc15 QSqlQueryModel: add new function to refresh the model data
Added refresh() to refresh the model data from the database.

* 9f392c09a1d Apple: Use automatic rendering mode for icon engine
The Apple icon engine, used for theme icons on macOS and iOS, will now
use the default rendering mode for icons, typically monochrome, instead
of always using hierarchical icons.

* b884fbf1023 3rdparty: patch BLAKE2 sources to not export anything in
static builds
Fixed a bug that caused the BLAKE2 symbols to be visible from QtCore in
a static build. If you need to use the BLAKE2 hashing algorithm in your
own code, either use QCryptographicHash or import libb2 into your build
environment. Using libb2 remains the recommended solution for all
systems, especially those for which it has optimized (vectorized)
implementations.

* 92373d353cf QSaveFile: make it so flush() errors imply commit() failed
Fixed a bug that caused commit() to return true and overwrite its
intended target file even though it failed to flush buffered data to the
storage, which could cause data loss. This issue can be worked around by
calling flush() first and only calling commit() if that returns success.

* cfd3c84184c [QTextStream] Add operator bool() to QTextStream class
Added implicit conversion to bool, returning `status() == Ok`.

* 3cb87d891bb Do not duplicate JsonFormat enum
The QJsonDocument header no longer includes QJsonValue. The backward-
compatible fix is to include all needed headers explicitly and to not
rely on the transitive includes.

* f9163ae7a81 Remove QT_NO_CAST_FROM_ASCII from
QT_ENABLE_STRICT_MODE_UP_TO
No longer includes QT_NO_CAST_FROM_ASCII. If you wish to continue using
QT_NO_CAST_FROM_ASCII, you need to define it in addition to
QT_ENABLE_STRICT_MODE_UP_TO. The reason for this change is that, while
everything else in strict mode should eventually become the default,
we're not proposing to remove the ability to construct a QString from a
const char*. QT_NO_CAST_FROM_BYTEARRAY and QT_NO_CAST_TO_ASCII remain
enabled in strict mode, though.

* e18b0059338 QLogging: switch the systemd/journald sink to unformatted
mode
The Qt logging framework (qDebug/qWarning/etc) will now only send the
plain, unformatted message to systemd's journald, if this backend is
enabled. The category and other fields are sent via metadata to
journald, so they can be filtered on and retrieved using journalctl.
This matches what Qt does for the Apple Logging support and does not
apply when Qt is using syslog or stderr to communicate with journald.

* e316276b76b Update CLDR to v46
Updated CLDR data, used by QLocale, to v46.

* 287234704b5 QSpan: don't detach Qt containers
No longer detaches implicitly-shared Qt containers converted to
QSpan<const T, N>. Note that std::span<const T, N> will, however, detach
such containers, so we recommend to use std::as_const() with implcitly-
shared Qt containers, as always.

* 39df9e1858a Implement COLRv0 support in Freetype engine
Added support for COLRv0 format color fonts.

* fd6f593c7ff Update bundled libpng to version 1.6.45
libpng was updated to version 1.6.45

* 185cba6e95a Replace qdebug.h includes in public headers with forward-
declarations
Various Qt public headers don't include QDebug any more; if you need
QDebug's streaming you'll have to include it in your code.

* 952ec8db3a0 SQLite: Update SQLite to v3.48.0
Updated SQLite to v3.48.0

* be3bf632e1c QString: add {setUtf16,setUnicode}(const char16_t*)
overloads
Added setUtf16(const char16_t *) and setUnicode(const char16_t *)
overloads.

* 549bab4150b QtTest: Update valgrind (fatuously) to v3.24.0
Valgrind headers are up to date with Valgrind v3.24.0.

* 308ee2738f2 Update Harfbuzz to version 10.2.0
Upgraded Harfbuzz to version 10.2.0.

* 09fa335fb22 Update public suffix list
Updated the public suffix list to upstream SHA
47264b57765919188b9f4144de8d95cf77e1b6dc.

* 3b95bfe7c7b QString/QByteArray: add nullTerminate{,d}()
Added nullTerminate() and nullTerminated() methods (like chop() and
chopped()), which are useful for strings constructed with fromRawData()
when calling methods that expect \0-terminated strings.

* 2b451c81a36 rhi: Introduce a way to enumerate adapters/physical
devices
Introduced enumerateAdapters() in QRhi to provide a an abstraction for
enumerating adapters (physical devices) with Direct 3D and Vulkan.

* 918566aeddb Update CLDR to v46.1
Updated CLDR data, used by QLocale, to v46.1.

* ad7b94e163a CMake: Only load Qt6FooPrivate automatically when building
Qt
CMake packages of public Qt modules don't provide the targets of their
private counterparts anymore. User projects must now call
find_package(Qt6 COMPONENTS FooPrivate) to make use of the
Qt6::FooPrivate target. User projects that rely on the old behavior can
set the CMake variable QT_FIND_PRIVATE_MODULES to ON.

* 7cb90e15631 Make module ready for source SBOM checking
Renaming the license files with prefix LICENSE. to have them ignored by
reuse tool.

* 0e4f9ffa55c Android: update to Gradle 8.12 and AGP 8.8.0
Updated Gradle to 8.12 and AGP to 8.8.0.

* 1b85143d217 DirectWrite: Support embedded PNGs in color fonts
Added support for color font formats with embedded pixmaps in
DirectWrite backend.

* 034a2347967 QLine::translate: mark as constexpr
The translate() overloads are now constexpr.

* 45886e6a810 QFileSystemEngine/Darwin: remove use of clonefile() on
Apple systems
Fixed a bug on Apple systems that would cause copy() to copy a
directory if the QFile pointed to a directory and the destination was in
the same volume. Now copy()'s behavior is the same as in other OSes:
directories are never copied.

* 019d2e59743 Update testlib's copy of Linux's perf_event_p.h header
The perf_event_p.h from Linux is updated to match Linux kernel 6.13.

* cd442e439b7 Change handling of unspecified year in
QCalendar::daysInMonth()
The daysInMonth(month, Unspecified) corner case is now specified to
return the greatest number of days in that month across all years, where
previously it returned the usual number of days in the month. This means
QCalendar().daysInMonth(2) is now 29 rather than 28, with similar for
other calendars than the Gregorian default.

* 2c212e15f8b QObjectData: Return const QMetaObject* from
dynamicMetaObject() already now
This (undocumented) class' dynamicMetaObject() function now returns a
const QMetaObject* (was: non-const). The backwards-compatible fix is to
receive the result in a const QMetaObject* variable (or to use auto),
and applying a manual const_cast, if a non-const object pointer was
actually required. Modifying the meta object that was returned by this
function was never supported and may lead to problems elsewhere.

* 3a284dc19d1 QSet: don't detach in remove()/removeIf() if nothing is
being removed
remove() and removeIf() no longer unconditionally detach, but only if
something is actually being removed.

* a74d2832168 QNumeric: make the overflowing helpers constexpr
The q*Overflow family of functions are now callable from constant
expressions on certain compilers.

* 5d857ed3bce rhi: add QByteArray overloads avoiding copies to
QRhiResourceUpdateBatch
Added QByteArray overloads to
QRhiResourceUpdateBatch::updateDynamicBuffer and
QRhiResourceUpdateBatch::uploadStaticBuffer that allow passing large
buffers without copy to the RHI.

* f744cef06cf QSqlQuery: complete the deprecation/removal of its copies
Copying a QSqlQuery object via QMetaType now raises a runtime warning.
Note that copy operations for QSqlQuery objects have already been
deprecated since Qt 6.2, and are planned to be removed in Qt 7.

* b6f825a857d Long live qstdlibdetection.h!
Added Q_STL_ macros for stdlib detection (libc++, libstdc++, MSSTL,
Dinkumware, STLport, SGI, RogueWave). If your STL is lacking, please
file a bug report. Note that these macros are not considered public API
just yet.

* 2d1b3028673 Revert "Optimize QSet::unite"
Fixed a regression in unite() that caused equivalent elements of
`*this` to be overwritten by elements of `other` if `other.size()` was
larger than `this->size()`.

* 162015e9c6f Unbreak QSet::intersect()
Fixed a regression (introduced for Qt 5.2) in intersect() that caused
equivalent elements of `*this` to be overwritten by elements of `other`
if `other.size()` was larger than `this->size()`.

* 7d05f5ed7d3 QUrl: set the host to empty but present for "file" URLs
Fixed a bug (regression from 6.7) where QUrl::resolved() could create
invalid URLs when the relative URI being resolved contained a path with
double slashes (e.g., combining "scheme:a" with "..//b.txt")

* 340c9d88ab3 QUrl: avoid going up from the drive path on Windows file
URLs
Fixed a bug (regression from 6.7) where resolving a base URL of an
absolute file path containing a Windows drive could result in said drive
being removed (e.g., resolving "file:///c:/" with "../" would result in
"file:///").

* 3d007ff2e9c QProcess/Unix: don't close the childStartedPipe too soon
Fixed a bug that caused QProcess not to report start failures if the
UnixProcessFlag::CloseFileDescriptors flag was active.

* 68cac07d500 QSet: add an rvalue overload of unite()
Added unite(QSet&&) overload of unite(const QSet&). Ditto for the `+`
and `|` operators.

* eb03784510c SQLite: Update SQLite to v3.49.0
Updated SQLite to v3.49.0

* 407a98d94fb Improve hinted rendering quality on Windows
Improved hinted text rendering at font sizes larger than 16px.

* 16aae5a4b83 QSqlDatabase: fix historical mistake of defaultConnection
being non-const
The static QSqlDatabase::connectionName member variable has changed
from a non-const pointer to a constexpr array. Modifying the pointer was
most likely a mistake in code and would produce a misbehaving
application.

* f1f610bc67b Qt Timers: disallow setting negative intervals
Timers with negative intervals aren't allowed anymore, that is, if you
try to start a timer (or set the interval) with a negative value, that
interval will be set to 1ms. Previously Qt timers would let you set the
interval to a negative value, but behave in surprising ways (for example
stop the timer if it was running or not start it at all). This change
affects QTimer, QChronoTimer, QBasicTimer and QObject::startTimer().

* 85899ff1819 Update UCD to Unicode 16.0.0
Updated the Unicode Character Database to UCD revision 34/Unicode 16.

* cdc71532ec2 Add QFuture::cancelChain()
Added QFuture::cancelChain().

* bbdbcb2eba1 QJsonObject::iterator: add keyView()
Added keyView() methods to iterator and const_iterator, allowing zero-
copy inspection of the key().

* aad0ab897f6 QDesktopServices: don't use openDocument if the URL has a
query
Fixed a bug that caused QDesktopServices::openUrl() to discard a query
when opening a local file URL that contained a query but no fragment.

* d8b4eb1a175 Add a QMetaObject::connect function
Added a QMetaObject::connect function for connecting a signal's
QMetaMethod to a member function or a functor (lambdas, etc.)

* d25e5e2cb78 QByteArray(View)::lastIndexOf: Guard against needle >
haystack
Fixed a bug in lastIndexOf() that could lead to out-of-bounds access
when the needle is longer than the haystack.

* 54daec43a04 CBOR/JSON: fix crash when comparing strings with different
length
Fixed bug that could result in a crash or failing to find a entry in
the map/object with non- ASCII keys.

* 395d23fbb3f QTest::toString(): print FP with full precision and in
hexfloat
QtTest now prints floating point values in hexadecimal notation and has
increased the precision for the decimal format, so different values can
be observed in the output when QCOMPARE or QCOMPARE_xx fail.

* 83f2d1130aa qEnvironmentVariableIntValue: fix off-by-one with MSVC's
getenv_s
Fixed a bug that caused qEnvironmentVariableIntValue() to fail to parse
octal values from -020000000000 to -010000000000 with MSVC. Other
compilers were not affected.

* fd3c05cd073 Long live qEnvironmentVariableIntegerValue() returning
std::optional
Added qEnvironmentVariableIntegerValue(), which returns
std::optional<int>.

* 4b278fd9989 QString: add fromRawData with a char16_t pointer
Added fromRawData() overload taking char16_t* (was: only QChar*).

* 3cb58b053c2 Update PCRE2 to 10.45
PCRE2 was updated to version 10.45.

* 01fc6aeaff4 Add a generic container-joining algorithm qJoin()
Added qJoin().

* eb87b0444ac QVariant: don't use the static CanUseInternalSpace with
existing objects
Fixed a bug where QVariant could misbehave regarding types that changed
from non-relocatable to relocatable (or vice-versa) and not all uses of
it were recompiled. To benefit from this fix, applications must be
recompiled, but they will be safe going forward.

* 1d6f71779f0 Accept multiple fonts with the same family and style name
Fixed an issue with font families where only the last of multiple sub-
families sharing the same name would be registered.

* 3070efb64a6 QCbor/JsonValue: add toStringView()
Add toStringView() method.

* b93575de017 QLocale: fix UB (signed overflow) in formattedDataSize()
Fix issue when calling formattedDataSize() with
numeric_limits<qint64>::min().

* 75ecb176df8 QScrollBar: Add createStandardContextMenu
Added createStandardContextMenu() method to allow extending the built-
in context menu.

* bc06c7c61a4 SQLite: Update SQLite to v3.49.1
Updated SQLite to v3.49.1

* c553f39e3d3 QDirListing: add ExcludeOther
Add IteratorFlag::ExcludeOther enumerator. IteratorFlag::ExcludeSpecial
now becomes an, obsolete, alias for ExcludeOther (the name was changed
to "other" to match the wording used in std::filesystem::is_other()).

* 9a83c2b88c1 QFileInfo: add isOther()
Added isOther() method.

* 3fc00c4d5e3 qEnvironmentVariableIntegerValue: switch to 64-bit returns
Update previous statement on qEnvironmentVariableIntegerValue to
indicate it returns 64-bit.

* fb2ef7e2315 qEnvironmentVariableIntegerValue: remove arbitrary length
limit
qEnvironmentVariableIntValue() is no longer limited in the length of
the number.

* 6f1553774aa CMake: Remove deprecated deployment API argument
script, which was deprecated in 6.6.0, has been removed.

* 92b5980a7e3 Use ICU from Windows SDK for codec support
(QStringConverter)
Qt on Windows now uses the ICU API of the Windows SDK for text codec
support (if available and no 'full' ICU is configured). This greatly
enhances the list of supported text codecs available.

* 39e7946cb65 Bundle Kitware's RunCMake test module
Add upstream cmake's RunCMake test infrastructure module to
src/testinternal/3rdparty/cmake to aid in creation of cmake auto-tests.

* 8b75f4735b3 Update bundled libpng to version 1.6.47
libpng was updated to version 1.6.47

* 874be50e7b7 QStringView: introduce a user-defined literal operator
Is it now possible to create QStringView objects by using the u""_sv
user-defined literal.

* 383ed62676f rhi: add R8SI, R32SI, RG32SI, and RGBA32SI "exotic"
texture formats
QRhiTexture gained R8SI, R32SI, RG32SI, and RGBA32SI signed integer
formats.

* 4275dfb7bfa QDir: add mkpath/mkdir overloads taking
std::optional<Permissions>
Added mkdir() method that takes a std::optional<QFile::Permissions>;
the new method transparently replaces the older mkdir() overloads.

* d2efb6faba9 QAbstractItemDelegate: add handleEditorEvent()
The base class now provides a handleEditorEvent() method, which
provides the same event handling as in QItemDelegate and
QStyledItemDelegate, including Tab, Enter, Esc keys and focus out
handling.

* 70e02a4f870 protocol: update version info of wayland.xml in
qt_attribution.json
Update wayland.xml to 1.23.0.

* 82a3357d007 Update Harfbuzz to version 10.3.0
Upgraded Harfbuzz to version 10.3.0.

* 9a753fa656a QColorDialogOptions: delete QSettings code and stop saving
globally
The class no longer automatically saves settings such as the custom
colors to a global QSettings("QtProject") shared by all applications and
no longer restores custom colors from there. Applications that wish to
retain the custom color settings should use customColors() and
setCustomColor() with their own settings files.

* 5e936b60fc9 QUrl: decode square brackets in fromLocalFile()
' to their percent-encoded forms. This will be visible in calls to
toString(), toEncoded(), or the encoded form of path(). QUrl's
comparison operator will consider the old (created from an encoded URL
string) and new forms to be different.

* 351b7a31aa2 Add namespaces to qdbusxml2cpp
The Qt D-Bus XML compiler (qdbusxml2cpp) now supports the command-line
argument -namespace <namespace>, which encapsulates all generated
classes within the specified namespace to prevent class name conflicts.

* 550db195afb Upgrade Harfbuzz to 10.4.0
Upgraded Harfbuzz to version 10.4.0.

* dfaa43331af QPen: QDebug-stream Pen{,Join}Style etc as enums
The debug stream operator now prints the names of capStyle() and
joinStyle() (was: numerical values).

* 07a15916cc3 QThreadStorage: add a warning suggesting use of
thread_local
QThreadStorage will print a warning suggesting the use of thread_local
for use with primitive types that are not pointers. In fact, switching
to the C++11 functionality is advisable for all types, but some runtimes
have bugs concerning destruction order. This warning can be suppressed
by #define'ing the macro Q_NO_THREAD_STORAGE_TRIVIAL_WARNING.

* c17a934197a QCborStreamWriter: add append(QByteArrayView)
Added a QByteArrayView overload of append().

* 59a081dc7e0 QCborStreamWriter: add append(QUtf8StringView)
Added a QUtf8StringView overload of append().

* 1b3b62d1b9f CMake: add a DISCARD_FILE_CONTENTS option to
qt_add_resources
Added a DISCARD_FILE_CONTENTS option to qt_add_resources().

* e323d46cdae Distinguish system locale from corresponding CLDR-derived
one
Message logging now distinguishes the system locale from the
corresponding locale - generated from its language, script and territory
- based on CLDR data.

* ec2e3e7ac92 QMessagePattern: add the %{threadname} placeholder
QMessagePattern / QT_MESSAGE_PATTERN now support the %{threadname}
placeholder.

* 9c87c991805 QAIM: return false if nothing was (or could be) done in
setItemData
Calling setItemData with an invalid index or empty map of data returns
false.

* ff7dfd72162 Expose the Vulkan 1.4 core API
QVulkanFunctions and QVulkanDeviceFunctions are updated to expose the
Vulkan 1.4 API as long as Qt is built against Vulkan 1.4 headers.

* 57d91d80290 QByteArray: make replace() consistent with QString's
replace() is now consistent with QString::replace() in its treatment of
empty haystacks and needles.

* dc033758a30 rhi: support partial region readbacks in
QRhiReadbackDescription
Added support for specifying a sub-rectangle for readbacks in
QRhiReadbackDescription. This allows partial texture or backbuffer
readbacks.

* e67568706fc rhi: gl: allow readbacks for all texture formats
All readback texture formats supported by the OpenGL implementation can
now be used with the Qt RHI.

* 7df128675a2 3rdparty: update TinyCBOR to v0.6.1
The copy of TinyCBOR in Qt was updated to 0.6.1.

* 1a580ca2a90 qHashMulti*: use the seed argument in the template and
noexcept traits
Fixed an issue that caused qHashMulti() and qHashMultiCommutative() to
fail to compile if used with a type that provided the required
2-argument qHash() function without providing a default seed.

* 34f993b7f54 QByteArray: add conversion to std::string_view
Added an implicit conversion operator towards std::string_view.

* 16081f414d9 Only default top levels to
Qt::WA_ContentsMarginsRespectsSafeArea
The Qt::WA_ContentsMarginsRespectsSafeArea attribute is no longer set
by default for non-top-level widgets. Top level widgets still default to
Qt::WA_ContentsMarginsRespectsSafeArea=true, so children are laid out in
the safe areas, but overriding the attribute for the top level now
allows placing widgets in the non-safe areas without also setting the
Qt::WA_ContentsMarginsRespectsSafeArea attribute to false for every
descendant widget that overlaps the non-safe area.

* f3256e059f4 QConcatenateTablesProxyModel: cache roleNames()
The roleNames property is only updated (lazily) on addSourceModel() and
removeSourceModel() now (was: on every call of the function). If your
source models change their roleNames() dynamically, you need to call
invalidateRoleNamesCache() manually when they do.

* bb846a22c37 QUuid: fix qHash() on 64-bit platforms
Improved the performance of the qHash() function on 64-bit platforms by
populating all bits of the output (was: only lower 32 bits).

* 4c9a4ecd358 QNetworkAccessManager: don't resend non-idempotent
requests
Non-idempotent requests are no longer incorrectly re-sent if the
connection breaks down while reading the response.

* a4daf493964 QVariant/QMetaType: fix conversions to/from qfloat16
Implemented converting of qfloat16 to and from the other numeric types,
text conversions to and from QString and QByteArray, and conversions to
and from QJsonValue and QCborValue. This should make qfloat16 behave the
same as float and double.

* 895b1c0ab35 JSON/CBOR: fix conversions from QVariant containing longs
and qfloat16
Fixed conversions from QVariant when the variant contained long,
unsigned long, or qfloat16.

* 276ccda2f3e Pass VxWorks touch ranges via environment variable
The user can now override touch ranges that the driver returns, by
setting the new parameters "rangex" and "rangey" on the environment
variable QT_QPA_VXEVDEV_TOUCHSCREEN_PARAMETERS with comma-separated min
and max touch ranges for X and Y axis respectively. For example, add
rangex=10,815:rangey=15,1024

* f5115a91373 Long live QGenericItemModel for lists and tables
Added QGenericItemModel, a QAbstractItemModel implementation that make
any C++ range with a cbegin/cend iterator pair available to Qt's
model/view framework.

* 4b8659ebf68 QXmlStreamReader::addData: lock encoding for QLatin1 case
Fixed a bug when calling addData() with a Latin1-encoded string
containing a full XML document with an encoding attribute, could result
in incorrect parsing of this document.

* 3bfc5d0b3b9 Update VulkanMemoryAllocator to 3.2.1
Updated VulkanMemoryAllocator to 3.2.1

* 3728032e03b Account for rounding error when rounding height metrics
Fixed an issue where the line distance for hinted fonts would be off by
one for specific sizes of some fonts.

* 69633bcb58e QFileSystemEngine/Win: Use GetTempPath2 when available
On Windows, generating temporary directories for processes with
elevated privileges may now return a different path with a stricter set
of permissions. Please consult Microsoft's documentation from when they
made the same change for the .NET framework:
https://support.microsoft.com/en-us/topic/gettemppath-changes-in-
windows-february-cumulative-update-
preview-4cc631fb-9d97-4118-ab6d-f643cd0a7259

* 62153d6ce03 QLoggingRegistry: load all the qtlogging.ini files, not
just the first
Fixed a bug that caused the logging framework to not load all the
QtProject/qtlogging.ini files found in the user and system
configurations. Previously, it would stop parsing after finding the
first one; now, all files are processed and their rules are merged. See
the QStandardPaths documentation for more information on what file paths
are considered in each operating system.

* ed341fcdd18 Add QHttpHeaders convenience methods for converting to
known types
Added convenience methods for parsing header values to integers and
date-times.

* bf5fcd6ebe1 QHttpHeaders: Add setters for QDateTime
Added setDateTimeValue() methods for setting headers using QDateTime.

* eced22d7250 QTextMarkdownImporter: Fix heap-buffer-overflow
Fixed a heap buffer overflow in QTextMarkdownImporter. The first marker
for Front Matter must begin at the first character of a Markdown
document, and both markers must be exactly ---\n or ---\r\n.

* b6b725aef59 QXmlStreamReader: fix addData() unnecessary conversion to
UTF-8
Fixed a bug when addData(QAnyStringView) was incorrectly recoding
UTF-16 and Latin1 data to UTF-8, thus potentially mangling it.

* f3da9d3c858 QUrl: expand the square brackets encoding to decoded
setPath() calls
") are now transformed to their percent-encoded forms ("%5B" and "%5D")
when present as inputs to setPath(), setQuery(), and setFragment() if
the parsing mode is QUrl::DecodedMode (the default).

* 98e0a7e0a06 Upgrade Harfbuzz to 11.0.0
Upgraded Harfbuzz to version 11.0.0.

* 51cd57116b7 QPointer: don't cause UB when checking for nullptr
For `QPointer<Derived> p`, `!p` and comparing `p` to nullptr no longer
perform invalid downcasts when the object held in `p` is in the process
of being destroyed and has already been demoted from Derived to one of
its base classes. Before, these expressions invoked data(), which casts
from QObject* to Derived*, a cast which is invalid.

* 03d5daf9437 Add jemalloc support
Added optional support for the jemalloc allocator, and optimized memory
allocations and deallocations in core Qt classes to cooperate with it.

* 5766d74ee1f CMake: Add a way to turn off plugin deployment
Add the NO_PLUGINS argument to qt_deploy_runtime_dependencies. This
turns off plugin deployment altogether.

* 6014820fe5f CMake: Add options to select / exclude plugins for
deployment
Add the arguments INCLUDE_PLUGIN_TYPES, EXCLUDE_PLUGIN_TYPES,
INCLUDE_PLUGINS, and EXCLUDE_PLUGINS to qt_deploy_runtime_dependencies.

* f2ac985d2fc CMake: Add plugin-related arguments to
qt_generate_deploy_app_script
Added arguments for selecting Qt plugins to
qt_generate_deploy_app_script.

* 87f4f0af6e9 CMake: Rework deployment of Qt plugins
qt6_import_plugins doesn't have any effect anymore on plugin deployment
with the CMake deployment API on Linux.

* f017087214e windeployqt: Make "recursive plugin deployment" the
default
windeployqt now deploys plugins of all dependent Qt modules by default.
"--include-soft-plugins" became default and the command line option was
removed.

* 5ce44934b3c windeployqt: Deploy Qt dependencies of local non Qt
dependencies
windeployqt now takes local non Qt dependencies into consideration
during deployment.

* 48959f7e5b6 QStringConverter: widen nameForEncoding()'s contract
The nameForEncoding() function now returns nullptr for an invalid
Encoding value. Before, such a call resulted in undefined behavior.

* 68a9c5fe513 Remove QWindow argument from
QWindowSystemInterface::handleThemeChange
QWindowSystemInterface::handleThemeChange no longer takes an optional
QWindow.

* c35f6851bfe QAbstractSlider: fix missing "emission" of
SliderOrientationChange
Fixed the missing "emission" of protected
sliderChange(SliderOrientationChange).

* 54865833c53 QAbstractSlider: remove duplicate update() calls from
setOrientation()
setOrientation() now relies on sliderChange() to call update(). This
was already the case for setRange(), setSingleStep() and setPageStep(),
and setOrientation() was only handled specially because of QTBUG-135597.

* 30fd101b558 Make F11 the fullscreen keyboard shortcut on Gnome (as on
KDE & Windows)
The fullscreen keyboard shortcut is now F11 on Gnome, not Ctrl-F11.

* 59d77a0162d Disable {position,resize}Automatic on QPlatformWindow
creation
A destroyed and recreated QWindow will now maintain its position and
size, instead of allowing the platform window another chance at setting
a default position and size. Users of QWindow and its consumers that
reuses a single window for many "logical" windows need to explicitly
position and size the window for each "use".

* 395451e15f7 Upgrade Harfbuzz to 11.1.0
Upgraded Harfbuzz to version 11.1.0.

* 25ba5f57823 Bump macOS minimum deployment target to macOS 13
The minimum deployment target is now macOS 13.

* 9a06c8ae8c0 Bump iOS minimum deployment target to iOS 17
The minimum deployment target is now iOS 17.

* 0bdbf4688e4 macOS: Use dedicated content CALayer for Metal/Raster
content
Metal and Raster windows no longer render their content directly to the
root CALayer of the window's NSView, but to a sublayer of the root
layer. This is an implementation detail that should not be relied on,
but may affect client code that pokes into the NSView of the QWindow in
unsupported ways. To opt out of the new mode, set
QT_MAC_NO_CONTAINER_LAYER=1.

* 4d839093b48 qDecodeDataUrl(): fix precondition violation in call to
QByteArrayView::at()
Fixed a bug in the handling of data: URLs that could lead to a crash if
Qt was built with assertions enabled. This affects QNetworkManager and
links in QTextDocument.

* 776dbdce7b1 QXmlStreamReader: add support for retrieving raw inner XML
content
Added readRawInnerData() for retrieving the raw inner XML content of an
element.

* ef5d9702a97 Move system locale later in uiLanguages(), when adding it
as fallback
When the system locale itself is missing from what the system reports
as suitable languages into which to translate the UI, it is now inserted
later in the list, where previously it was added at the front.

* 2edd9286cf3 Fix long-form zone parts in date-time strings
The tttt format specifier now uses the full long name of the zone,
falling back to its IANA ID only if this cannot be determined. Both
forms are now recognized when reading a datetime from a string.

* 53622aca2ad QXmlStreamWriter: add error-handling API
Added error handling API with QXmlStreamWriter::Error enum, error(),
errorString(), and raiseError() functions.

* 095cacd668f Do not treat the installation of an empty QTranslator as
an error
QCoreApplication::installTranslator() will now return true even for
empty translators (QTranslator::isEmpty()). This makes it explicit that
empty QTranslator objects are registered and queried, and therefore
deleting the object prematurely might result in undefined behavior.

* d8ac4cd8692 Add constant property QStyleHints::accessibility
Added class QAccessibilityHints, which can be accessed from
QStyleHints. This singleton contains a single property
contrastPreference which can be used to determine if the platform has
enabled a high contrast setting or not. More accessibility settings
might be added to QAccessibilityHints in the future.

* 4599903eed3 SQLite: Update SQLite to v3.49.2
Updated SQLite to v3.49.2

* 2875c4358be QSslCertificate: fromPath(): check the path arg isn't
empty
fromPath() no longer accepts an empty path, which would previously
result in searching the current directory.

* 2be51c69230 QSslCertificate: add fromFile() method
Added fromFile() method.

* 883afddd1e8 QDockWidgetGroupWindow: Copy window icons to tabs
When grouping dock widgets in tabs, the dock widgets' window icons are
now used in the tab bar.

* 5b33c4e84ce QLayout - Introduce vertical and horizontal layout
constraints
Introduced a vertical and horizontal size constraint in layout as the
size constraint behavior can depend on the orientation.

* f17a8ac6fb9 Upgrade Harfbuzz to 11.2.1
Upgraded Harfbuzz to version 11.2.1.

* c9ab69d4e34 Update bundled libpng to version 1.6.48
libpng was updated to version 1.6.48

* 2a9444920bc macOS: Make NSServicesMenuRequestor implementation rich-
text aware
Text services via the Services menu now support rich text extraction
and insertion.

* a6070847f07 qlogging: Journal: Log thread id, suppress empty fields
Qt now logs the thread id (TID) in journal, allowing separation of
identical messages from multiple threads.

* a15639a3ab5 QByteArray: make replace(pos, len, view) consistent with
QString's
replace() is now consistent with QString::replace() in its treatment of
out-of-bounds indexes.

* 263f06ae8b5 QXmlStreamWriter: add option to stop writing after an
error
Added setStopWritingOnError() and stopWritingOnError() functions.

* cec5066f322 qdataurl: treat comma as mandatory in the data URL syntax
Changed parsing 'data:' URLs to report failure if the comma is missing,
this makes it more compliant with RFC 2397.

* 6f319847d01 Add q23::expected as a private type
Added Sy Brand's tl::expected as a third party dependency for use
internally in Qt implementation.

* da3422ca150 a11y: Introduce QAccessible::Attribute::Locale, bridge to
AT-SPI
Added new Locale enum value that can be used to specify the locale of
an accessible object.

* 61b17127ae5 QByteArray: make toDouble() reject space-only strings
Fixed an old regression that caused toDouble() and toFloat() to return
ok = true for a string containing only whitespaces.

* c2bdf7636eb Use WS_EX_NOACTIVATE to prevent window from getting
focused
Windows with flag Qt::WindowDoesNotAcceptFocus no longer have a taskbar
entry.

* 6854ea63365 dwrite: Support additional font names for system fonts
Fixed an issue where legacy names such as 'Arial Narrow' would no
longer be listed as separate font families.

* 2fb5bd96694 qdbus: add call GetConnectionCredentials interface
Added method serviceCredentials(). See
<https://dbus.freedesktop.org/doc/dbus-specification.html> section:
'Method: org.freedesktop.DBus.GetConnectionCredentials' for more
information.

* c617cc95934 QFileSystemEngine::tempPath: bypass QDir and go straight
to QFSEngine
tempPath() may now return a non-canonical path. This means going up
from it (cdUp()) may result in different paths from string manipulation
(adding "/..").

* 728daaf384e SQLite: Update SQLite to v3.50.0
Updated SQLite to v3.50.0

* b695743b7e6 iOS: Report inverted screen orientations via windowScene
orientation
QScreen::orientation() now reflects the inverse portrait and landscape
orientations, as long as system allows rotating the UI to those
orientations.

* b6a3f29c101 SQLite: Update SQLite to v3.50.1
Updated SQLite to v3.50.1

* 12b91f97e3d QMetaObject: deprecate the Qt 6 QVector -> QList porting
kludge
Fixed a bug that caused signals and slots with argument types matching
"QVector<" (e.g. "MyQVector<int>" or "NotQt::QVector<int>") to not be
found in QObject::connect() or QMetaObject::indexOfMethod().

* 2abd39c10c8 Add conversion from QUtf8StringView to std::u8string_view
Added std::u8string_view operator if compiled with C++20.

* 853658f537d QScopeGuard: only include what you need
The qscopeguard.h header no longer includes qglobal.h, but only what it
itself needs. A backwards-compatible fix is to not depend on transitive
includes and include all you need explicitly.

* 06c0ae9de36 QDataStream: add operator bool()
Added implicit conversion to bool, returning `status() == Ok`.

* 54f6da2d4c3 Bump double-conversion version
Updated double-conversion to v3.3.1.

* 973ae3e419c QJsonObject/QCborMap: Add asKeyValueRange()
Added asKeyValueRange to iterate with a range-based for loop over key-
value pairs with support for structured bindings.

* 8bc8f26e3c3 QUrl: fix comparisons of URLs with password but no
explicit username
Fixed a number of bugs in QUrl where a URL modified using the setXxx()
functions would fail to compare equal to itself after going through
toString() and setUrl() round-trip.

* b909757a29c Update CLDR to v47
Updated CLDR data, used by QLocale, to v47.

* 46cc56d828c Update bundled libjpeg-turbo to version 3.1.1
libjpeg-turbo was updated to version 3.1.1

* a572495f3bc Update TIKA mimetypes from upstream
Updated TIKA mimetypes from upstream

* 24b19d896d9 Update public suffix list
Updated the public suffix list to upstream version
2025-06-16_09-45-02_UTC.

* e4b1775861a wayland: Add pointer warp support
New protocol synced from wayland-protocols

* 89e52c93774 QLockFile: mark ctor explicit
The QLockFile(QString) constructor is now explicit, so implicit
conversion from QString to QLockFile, incl. `QLockFile f = str;`, no
longer works. Using explicit construction instead (`QLockFile f(str);`)
is a backwards-compatible fix.

* 5bc160bc838 Android: update to Gradle 8.14.2 and AGP 8.10.1
Updated Gradle to 8.14.1 and AGP to 8.10.1.

* 9a0e4d8fdc8 Update bundled libpng to version 1.6.49
libpng was updated to version 1.6.49

* 92f8e5fe481 SQLite: Update SQLite to v3.50.2
Updated SQLite to v3.50.2

* 5a8a4bb527a QAnyStringView: support single wchar_t arguments also on
Unix
The unary arg() function now treats wchar_t as a character (string-
like; was: integer), so u"%1".arg(L'ø') will now return "ø" and not
'248". This makes the function consistent with both QString multi-arg()
and QLatin1StringView::arg().

* 63bb40d3ed6 Android: Set proper A11y-element java class names to
support TalkBack
Provide actual Android UI class names for TalkBack to improve a11y
announcements.

* aadc9643902 Upgrade Valgrind third-party component to v3.25.1
Updated Valgrind support to v3.25.1; this adds support for RISCV 64-bit
Linux.

* 216782ba8a2 QAtomicScopedValueRollback: fix CTAD with with mixed
(atomic<T>, V) arguments
Added support for class template argument deduction (CTAD) when the
type of the atomic and the type of the new value differ, e.g. as in
`atomic<chrono::milliseconds> a; `QAtomicScopedValueRollback rb(a,
10s)`.

* 67fcaba326c QTest: provide overloads for the qWaitFor* functions
Added QDeadlineTimer overloads for the qWaitFor* functions.

* 12c6377cba4 Fail builds on Apple platforms with invalid Info.plist
Fail builds on Apple platforms if the Info.plist is invalid instead of
generating corrupt application bundles.

* 13e08422115 Update bundled libpng to version 1.6.50
libpng was updated to version 1.6.50

* 0d1b0c927ed QWeakPointer: don't let IfCompatible<X> make accidental
SMFs
Fixed a regression whereby the QWeakPointer<T> copy or move
constructors and/or assignment operators may fail to compile for
forward-declared (incomplete) T.

* f5aa159ca13 QPainterPath: add missing move constructor
Added missing move constructor.

* 8f3aa0a804d QDBusPendingCall: add move-constructor
Added move constructor.

* fe96605bd46 qmatrix4x4.h: don't include qquaternion.h
The qmatrix4x4.h header no longer includes qquaternion.h. A backwards-
compatible fix is to not rely on transitive includes and include what
you need explicitly.

* 1f801dd1462 QTextStream: cope with multi-code-point signs
Fixed QTextStream::FieldAlignment::AlignAccountingStyle for locales
that have negativeSign/positiveSign (-/+) that take more than one UTF-16
code point (e.g. ar (Arabic)).

* a5e804b643b QDBusPendingReply: add missing SMFs
Added move constructor.

* a1a25d1d01b QPainterPath: remove implicit sharing
QPainterPath is no longer implicitly shared. This is a necessary change
to support various caching optimizations. On the other hand,
QPainterPath is now fully reentrant (before, it was not thread-safe in
the general case).

* 838d543cd2a QLocale: fix off-by-one error in codeToScript()
Fixed a bug where QLocale could not find the QLocale::Script with the
highest value when looked up by string (codeToString() or
QLocale(string) constructor).

* 985fa26ba17 Static plugins - mangle entry point
In namespaced builds the entry function for static plugins now appends
the namespace via QT_MANGLE_NAMESPACE.

* 9284e76575f Q_IMPORT_PLUGIN: namespace RAII class
The Q_IMPORT_PLUGIN macro must be placed in file-scope. It cannot be
placed into function-scope any more, as it was never intended to be.

* 3492f1c5eec SQLite: Update SQLite to v3.50.3
Updated SQLite to v3.50.3

* 4036b7eaa1a Add missing changed signal to QML Window.flags
Added signal flagsChanged to QWindow.

* 1f46780405d Define macOS QOperatingSystemVersion constants using only
major version
QOperatingSystemVersion constants for macOS 11 and up are now
represented with their major version only, and minor and patch versions
unspecified, as documented.

* eb8048bcfcf SQLite: Update SQLite to v3.50.4
Updated SQLite to v3.50.4

* 6c4b0af0e33 src/gui: bump dependency version of xkbcommon
xkbcommon minimal required version now is 0.9.0.

* ada917e4ad1 Fix the url construction in the requestUrl method
QNetworkRequestFactory::createRequest() doesn't decode the provided
`path` anymore. If the path string was passed encoded by the user, it
stays encoded in the particular way.

* 325505018f7 QFileSystemEngine/BSD: check UF_HIDDEN on the symlink only
Fixed a bug that caused isHidden() to return true on BSDs and Apple
OSes for non-hidden symlinks that pointed to hidden targets.

* 6a7e8b913bf QCoreApplication: namespace qt_startup_hook
qt_startup_hook is now name-mangled when building Qt in namespace.
Applications wishing to override it must use
QT_MANGLE_NAMESPACE(qt_startup_hook).

* d070a72ec81 QDirListing: check for '.' and '..' after the checking the
name filters
Now listing '.' and '..' special entries respects any set name filters.
Previously if IncludeDotAndDotDot was set, '.' and '..' would always be
listed.

* ae8eb936887 Doc: Classify 3rd party code in cmake as tools
Reclassify third-party components "KWin" and "extra-cmake-modules" as
tools related.

* 725d7decc23 Upgrade Harfbuzz to 11.3.3
Upgraded Harfbuzz to version 11.3.3.

* baa7daec882 windeployqt: Add parameter to extend timeout of
qmlimportscanner
Add option to control timeout for qmlimportscanner runs.

* 62583dac9f3 QTest::qWaitFor*: capture the widget/window using QPointer
Fixed a bug that would cause the qWaitForWindow* and qWaitForWidget*
functions to crash or misbehave if the window or widget they were told
to wait on was destroyed in the process of waiting for it to be
shown/focused/activated/exposed.

* 37950e7d350 qvsnprintf: fail if the result size doesn't fit into an
int
Fixed a bug that would cause q(v)snprintf() to report success on some
platforms, even though the result was truncated.

* 13144f0b4ab Upgrade Harfbuzz to 11.4.1
Upgraded Harfbuzz to version 11.4.1.

* 9c7d479ca3f QTextEngine: Pass expanded context to HarfBuzz for shaping
Improved text shaping with mnemonics in certain languages, such as
Arabic.

* c9c2c70ea9c Teach QImage::toCGImage() how to propagate the image's
color space
QImage::toCGImage() now propagates the color space of the image to the
resulting CGImage.

* 5f488d4d50e Android: Set name-matched class names for Slider and
ScrollBar for TalkBack
Use different Android class names for Slider and Scroller.

* 07f3b9caf85 Android: Use the TalkBack focus signal to trigger
focusAction
Use TalkBack ACTION_ACCESSIBILITY_FOCUS to trigger focusAction.

* a145e12833e QJsonDocument/Value: fix integer truncation in
fromJson(QByteArray)
Fixed a bug on 64-bit platforms where fromJson(QByteArray) could report
one of the Unterminated errors for valid input whose size merely
exceeded INT_MAX (2GiB).

* 6fa36f0c862 moveToTrash/XDG: allow $XDG_DATA_HOME/Trash to be a
symlink
Fixed a bug that caused moveToTrash() to disallow trashing to trash
bins using the XDG Trash Specification when the trash path was a
symlink.

* b3da68f8edf Upgrade PCRE2 to 10.46
PCRE2 was updated to version 10.46.

* 3823d288fe7 Suppress construction of QTimeZone(Qt::TimeSpec)
Construction from a Qt::TimeSpec, which was never meant to be
supported, is now rejected at compile time, where previously compilers
(mis)interpreted the enum as an int so called the (int offsetSeconds)
constructor, with results consistently at odds with what the user
presumably expected.

* 4c644933860 Upgrade Harfbuzz to 11.4.5
Upgraded Harfbuzz to version 11.4.5.

* 28ef1f4c2f7 Upgrade Harfbuzz to 11.5.0
Upgraded Harfbuzz to version 11.5.0.

* 47975226ac0 Update Freetype to 2.14.0
Updated bundled Freetype to 2.14.0.

* 013085e51c7 Update Freetype to 2.14.1
Updated bundled Freetype to 2.14.1.

* cafd75c03f5 Update bundled libjpeg-turbo to version 3.1.2
libjpeg-turbo was updated to version 3.1.1

### qtsvg
* f507883c Make module ready for source SBOM checking
Renamed certain license files outside of LICENSES with `LICENSE.`
prefix such that reuse will correctly ignore them.

* 06829010 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

* 477bf764 Fix rendering opacity in text elements
Fixed rendering fill-opacity and stroke-opacity in text elements

### qtdeclarative
* 83d9084552 Teach ApplicationWindow about safe area margins
The contentItem of ApplicationWindow is now automatically padded to
account for safe area margins. To override the automatic padding, set
the padding explicitly, via e.g. `topPadding: 0`.

* b4b691b040 QtQml: Add some consistency to QV4::RegExp
The JavaScript regular expression engine now honors
QV4_JIT_CALL_THRESHOLD for its own JIT. If QV4_JIT_CALL_THRESHOLD is not
set, it uses the JIT after 3 interpreted matches for any regular
expression, rather than the previous 5. Matching a regular expression on
a string longer than 1024 bytes counts as 3 matches. This is to retain
the default behavior of JIT'ing regular expressions right away when
encountering long strings.

* 33c13102bf QtQml: Compare before assigning to var properties
Assigning to "var" properties now only triggers a change signal if the
value of the property actually changes. Change is determined using
JavaScript's "strictly equals" semantics (the "===" operator).

* bac4723a30 QtQml: Allow basic name quoting in qmldir files
You can now quote file names in qmldir files using '"'. This is so that
you can write file names with spaces in them. '\' functions as an escape
character, allowing you to escape quotes that are part of file names and
backslash itself.

* 23ed52c1c0 QQmlPropertyMap: add an example of two argument constructor
Added a code snippet to explain the use of protected two argument
constructor of QQmlPropertyMap.

* 0794a0e06e Add ContextMenu
Added ContextMenu. ContextMenu can be attached to any item in order to
show a context menu upon a platform-specific event, such as a right
click or the context menu key.

* 57b681eb51 qmlformat: Reorder imports alphabetically
qmlformat now supports sorting of imports, there is a new commandline
option -S that is used to sort imports.

* 6474c654eb IR Builder: Fix translation binding parsing
ListElement now supports disambiguation strings when QT_TR_NOOP is
used.

* 76359a60a5 FluentWinUI3: Move FocusFrame type to private impl module
FocusFrame.qml is deprecated in the module's public QML API and moved
to the private impl module instead.

* c6792959e6 FluentWinUI3: Move StyleImage to private impl module
StyleImage.qml is deprecated in the module's public QML API and moved
to the private impl module instead.

* 1b9d4c66ff Qml: Fix import order for certain name resolutions
When a type name is provided by two different imports, the type from
the last import takes precedence. This is now also the case when
resolving singletons, attached types, and types for as-casts. This
aligns with the behavior for regular type resolution.

* c9aa986ed1 Controls: Make ComboBox currentValue property writable
It is now possible to write to the ComboBox currentValue property as
way to set its current item.

* 3dda155085 qmlformat: Error out when no input files are provided
qmlformat will now error out if no files are provided as positional
arguments or via the -F option.

* 3b0dab39d0 CMake: Do not automatically link against Qt6::QmlPrivate
QML modules created by qt_add_qml_module no longer link against the
Qt6::QmlPrivate target by default. Modules that intentionally use
private API must now explicitly link against it.

* 26f7bf4f5c CMake: Remove deprecated deployment API argument
The FILENAME_VARIABLE option of qt6_generate_deploy_qml_app_script,
which was deprecated in 6.6.0, has been removed.

* fdb1db77a5 Overlay: ignore right button clicks
The pressed and released signals are no longer emitted for right
clicks. This is to allow ContextMenu to work when controls like Drawer
are used.

* 361f1f38e0 Make module ready for source SBOM checking
Renaming the license files with prefix LICENSE. to have them ignored by
reuse tool.

* a0bde44fef CMake: Enable building Qt and user projects without support
for aotstats
It is now possible to control whether QML Compiler statistics
(aotstats) get generated by setting the QT_QML_GENERATE_AOTSTATS CMake
variable to ON or OFF. The default value is ON.

* 3b598b6f75 ContextMenu: add to text editing controls
TextField and TextArea now provide a ContextMenu by default. If you
already have a custom context menu for these types, ContextMenu will not
open its own on e.g. right click.

* 4eaa8ff841 QQmlSA: Remove PassManager::{element|property}Passes() from
public API
PassManager will no longer expose the element and property passes that
it holds. They are only meant to be used inside the PassManager itself.
elementPasses() and propertyPasses() were removed.

* ede03ac61b Add QRhiAdapter support for QQuickGraphicsDevice
Added fromRhiAdapter() to QQuickGraphicsDevice.

* a9871233d0 StackView: Use PushTransition for pushItem(s)
The default operation for pushItem(s) is now PushTransition as
documented. Previously, Immediate was used.

* 065b784cab Auto-depend on QtQuick when linking against QtQuick
If a QML module target is linked against Qt6::Quick, QtQuick is
automatically added to its QML dependencies. This avoids tooling errors
when e.g. a QQuickItem derived type is exported by the module.

* e31befb14e PathRectangle: add bevel properties
Added bevel properties.

* e30b80657e Add RectangleShape to QtQuick.Shapes.DesignHelpers
Added RectangleShape.

* 9601b74dab QuickControls: Add vertical and horizontal header view
delegates
Add dedicated delegate components for vertical and horizontal header
views.

* 137cdc364d CMake: add a DISCARD_QML_CONTENTS option to
qt_add_qml_module
Added a DISCARD_QML_CONTENTS option to qt_add_qml_module(), that
removes original QML and JS file contents from the target's resource
system.

* 48cb120c5f TableView: emit commit on editor loss of focus, unless
Qt::Key_Escape
The edit delegate will now emit the onCommit signal when it loses
focus, unless it was closed from Qt::Key_Escape.

* 07f6e088c8 QML: Add ChangeLog for final property attribute
Properties in QML files can now be marked final. This is done the same
way as the default, readonly, and required property attributes. Marking
a property final in a QML file has the same effect as marking a
Q_PROPERTY() FINAL.

* 015ca951bc Expose QLocale::createSeparatedList to Qml
Added a createSeparatedList method that expose
QLocale::createSeparatedList to Qml.

* 4bd5b31279 Use sticky bindings to write the model through required
properties
DelegateModel now has a new property delegateModelAccess. Setting it to
DelegateModel.ReadWrite allows you to write values into the model via
required properties the way you can do the same with context properties.

* 42c4f40c0e QQuickPopupItem: Set tabFence to be true by default
The popupItem always acts as a tab fence, preventing tab focus
navigation in and out of the popup, except when the popup is a Drawer,
in which case this behavior depends on the drawer's modality.

* 390c78b394 QtQml: Drop checks for compile hash and Qt version from the
CUs
You can now use QML code compiled with Qt Quick Compiler across Qt
versions as long as the compilation unit format hasn't changed between
those versions. You cannot rely on the compilation unit format to stay
unchanged under any specific circumstances. However, we won't change it
unnecessarily.

* 3bc0a11401 Expose delegateModelAccess from QQuickItemView
ListView and GridView now have a new property delegateModelAccess.
Setting it to DelegateModel.ReadWrite allows you to write values into
the model via required properties just as you could with context
properties.

* 1cf72c90de Expose delegateModelAccess from QQuickRepeater
Repeater now has a new property delegateModelAccess. Setting it to
DelegateModel.ReadWrite allows you to write values into the model via
required properties just as you could with context properties.

* f469d538a7 Quick: Expose delegateModelAccess from QQuickTableView
TableView and TreeView now have a new property delegateModelAccess.
Setting it to DelegateModel.ReadWrite allows you to write values into
the model via required properties just as you could with context
properties.

* 5a05a2a04e Add trimming functionality to ShapePath
Add path trimming functionality

* 52141b34ec Basic Style: Add support for dark mode color scheme
Basic style supports dark mode now.

* 9ac0e70cdb Close all other Menus when showing non-sub-menu
All non-sub-menus are now closed when a menu is opened. This is to fix
an issue (QTBUG-134903) where duplicate menus are shown when opening a
custom non-ContextMenu on a text editing control like TextField or
TextArea. This means that rather than two context menus incorrectly
being opened, an extra one will briefly be visible before immediately
being closed. For information on how to avoid this, please see the
"Context menus" section of Menu's documentation.

* 6a84788297 QQmlBind: Only restore previous state if current state is
still active
The Binding element now only restores previous bindings or values if
its own binding is still active on destruction or changes to its "when"
property. If it has been overridden by another Binding element, it will
not disable that one anymore.

* 386e085114 QQuickTest: add and use active focus macros
Added QVERIFY_ACTIVE_FOCUS and QTRY_VERIFY_ACTIVE_FOCUS macros that can
be used to get detailed failure messages for when
QQuickItem::hasActiveFocus should be true but isn't.

* f52428e600 QtQml: Long live Qt.labs.synchronizer!
The new Synchronizer element allows you to synchronize values between
two or more properties without breaking their bindings. This is useful
for connecting user-editable controls to backend values.

* 06cd8c9843 QtQml: Do not check revisions when resolving aliases
You can now create aliases to revisioned properties that would be
unavailable when accessed without qualification. Aliases are always
qualified after all.

* 5a2a6a8d77 qmlformat: customizable semicolon
New option semicolon-rule is added and EmptyStatement formatting
behavior has changed.

* 0a848c1f26 Add API to VectorImage for controlling animations
Added some API to the VectorImage for looping, stopping, pausing and
resuming animations.

* d42bb3fdf7 QtQml: Reduce import and plugin paths for to plugin
applications
The default import and plugin paths for QML have been changed for
applications that set the Qt::AA_PluginApplication attribute. This
attribute is meant to isolate the plugin application from the host
application. To achieve this goal, it can't share plugin and import
paths with the host application.

* 6617c64b8f Support Flexbox layout in Qt Quick
Added MIT LICENSE from the third-party Facebook yoga source
(https://github.com/facebook/yoga/blob/main/LICENSE) to enable its usage
in Qt QuickLayouts.

* b0e38f6ace Introduce a TreeModel QML type
Added a new TreeModel QML type that allows the definition of a tree
structure in the QML file and works with TreeView.

* 2278556a69 Update license and external links in doc for quick flexbox
layout
The 'Version' and 'DownloadLocation' for the facebook yoga library are
mentioned in the qt_attribution.json file.

* a35b0e44ae Qml: Allow accessing unscoped enums values as
<Component>.<Enum>.<Key>
It is now possible to access unscoped enum values in a scoped way as
<component name>.<enum name>.<key>. Previously, it was only possible to
access them in an unscoped way.

* 5e312953f6 Qml: Add key <-> string helpers to Qml enums
It is now possible to map between the value of enum keys and their
string representations by calling the enumStringToValue,
enumValueToString, and enumValueToStrings methods on the Qt global
object.

* 4b22251e4d Enable expanded client area by default in iOS style
The iOS style now enables expanded client areas by default. To override
this, set the ApplicationWindow's flags explicitly to e.g. Qt.Window.

* 0e4a2e5152 Clarify the exact commit of the yoga 3rd party dependency
Clarified that exact version of yoga library is v2.0.1.

* b226d87937 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

* 335299d571 API Review: Expose delegateModelAccess from
QQmlInstantiator
Instantiator now has a new property delegateModelAccess. Setting it to
DelegateModel.ReadWrite allows you to write values into the model via
required properties just as you could with context properties.

* 76335ac111 qmllint: Avoid spurious warnings when file selectors are
used
qmllint and the LSP now no longer print warnings about ambiguous types
if file selectors are used, and instead use the "plain" version. The QML
script compiler will still conservatively reject such QML files. If
warnings about such cases are desired, the new "importFileSelector"
warning category can be enabled.

* 03a861c6c0 Remove support of manipulation of complex rows in
QQmlTableModel
Removed the support of manipulation of complex row structures from
QQmlTableModel.

* da7f7e19f8 Make defaultDelegate compatible with TreeModel and
TableModel
Changed the order of the role and value parameters in setData to
resolve ambiguity.

### qtactiveqt
* 6f495e7 Make QAxBase/QAxWidget QDataStream operators hidden friends
The QDataStream operators are now hidden friends, so they will only
match types which are QAxBase, or derived from it, not those that merely
implicitly convert to them. A backwards-compatible fix is to make the
conversion explicit and only call these operators on actual QAxBase
subclass objects.

### qtmultimedia
* 30f7fd263 3p: import signalsmith-stretch library
Import timestretching library from Signalsmith Audio to use in the
media player.

* 156db2b7e Add REUSE.toml files and missing licenses
Add path to license files within LicenseFiles field.
qtattributionscanner looks for the files associated with licenses listed
in the licenseId fiel within the LICENSES directory. To prevent reuse
from erroring out, the license files only mentioned in
qt_attribution.json need to be moved out of the LICENSES directory. For
the qtattributionscanner to find those files, they need to be listed in
LicenseFiles field.

* 6ff2bddd9 QAudioDevice: Make comparison only rely on id and mode
Comparison of QAudioDevice now only relies on .id() and .mode()
properties

* e37439670 Fix product name and ID for the pffft third party dependency
Update pffft product name and id.

* c3f8bbc66 Update pffft version to the latest version from upstream
Updated pffft to 02fe771.

* c8e6ca93c QImageCapture: Expose supportedFormats to QML
The supportedFormats property has been exposed to QML.

* a491cf35c Document where to find FFmpeg build scripts
Add link to where FFmpeg build scripts can be found.

* 1e17c8f18 QMediaPlayer: add API to expose pitch compensation
Added a new API to QMediaPlayer that enables pitch compensation,
providing greater customization options for the FFmpeg backend.

* 675ac18da Remove security critical label from pffft and Eigen
dependencies
Removed security critical label from pffft and Eigen third party
dependencies.

* 6c3e7a444 Document the native Windows media backend as deprecated as
of Qt 6.10


* 6fc0f34a3 QML, Camera: Expose RESET functions for device and format
QML property cameraFormat can now be reset in order to select the
default format.

* 24b9d2cdf QMake: Add possibility to link and embed FFmpeg frameworks
on iOS
Added the CONFIG value add_ios_ffmpeg_libraries that can be used in iOS
apps that need FFmpeg frameworks for QtMultimedia.

* f4398f4b5 QAudioSource/Sink: use preferred format by default
QAudioSource/Sink: use preferred device format when constructed with a
default-initialized QAudioFormat.

* 98d35f608 QWindowCapture: Make QML property 'window' resettable
The QML property 'window' can now be reset

* 60e6fd484 Update FFmpeg version in documentation
Updated FFmpeg to n7.1.1.

* 017fe70f6 Build system: skip qtmultimedia if threading is disabled
QtMultimedia now requires Qt to be compiled with FEATURE_thread. This
implies it is not available in single-threaded webassembly

* c720d74bc CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

* 07fe61bee 3rdparty: import dr_wav to implement wav decoder
Added dr_wav as wave file decoder for QSoundEffect.

* 25a2473ce QCapturableWindow: Make constructible from QWindow
Introduced new constructor for QCapturableWindow, that allows
developers to create QCapturableWindow instances from QWindows. QML
Windows can now be implicitly constructed into QML CapturableWindow.

* c5e323df4 3rdparty: add tlsf arena allocator
Added tlsf for use in QSoundEffect player

* 43aeb4afa QMediaFormat: align format/codec descriptions
Improve consistency of format and codec description strings

### qttools
* 4d1a8f944 QDoc: Write title attribute for images in HTML
QDoc can now generate a `title` attribute for your images. Set the
configuration variable `usealttextastitle = true` in your .qdocconf
file.

* 6a4f41e7f CMake: Add the QM_OUTPUT_DIRECTORY argument to
qt_add_lrelease
Added the QM_OUTPUT_DIRECTORY argument to qt_add_lrelease to specify
the directory where .qm files are generated. Using this argument is more
convenient than setting the OUTPUT_LOCATION source file property on
every corresponding .ts file.

* edd8ad8a7 CMake: Add QM_OUTPUT_DIRECTORY argument to
qt_add_translations
The qt_add_translations function gained the QM_OUTPUT_DIRECTORY
argument that can be used to specify the directory where .qm files are
generated.

* 923583303 CMake: Add TS_OUTPUT_DIRECTORY argument to
qt_add_translations
For consistency with qt_add_translations' argument QM_OUTPUT_DIRECTORY,
we introduced the argument TS_OUTPUT_DIRECTORY to specify where
automatically generated .ts files are placed. The old argument name,
TS_FILE_DIR, is still available as alias to keep older project files
working.

* 119802c61 Make module ready for source SBOM checking
Renaming the license files with prefix LICENSE. to have them ignored by
reuse tool.

* 98f2cfe37 qdoc: Improve handling and presentation of anonymous enums
QDoc now supports documenting anonymous C++ enums when
`documentationinheaders` feature is enabled.

* 2469e552a allow mixing id-based and text-based translation in a
document
The -idbased flag is not required anymore, and will be removed in
future version.

* 5478abc74 qdoc: Introduce \notranslate command
Added a \notranslate command to mark non-translatable words and
phrases.

* af507c08a QDoc: Drop 32-bit support in CodeMarker
- QDoc no longer supports 32-bit platforms.

* 4d9ce3d71 qdoc: Add support for generating links to source code in C++
reference
QDoc can now automatically generate links to the source code in C++
reference pages.

* 41d599f81 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

* 967078281 qdoc: Introduce \qmlenum command
QDoc now supports documenting enumerations in QML using the \qmlenum
command.

* 8bc64b1d2 qdoc: Allow generated lists in table of contents structure
Pages that contain table-of-contents \list structures can now also use
\generatelist and \annotatedlist commands for the same purpose.

* a0b0bfd7f QDoc: Generate contextual snippets for overloaded signals
and slots
QDoc now generates contextual code snippets and configurable links for
overloaded signals and slots. When documenting overloaded signals or
slots, QDoc automatically creates practical connection examples using
the specific class and function signature, showing both qOverload() and
lambda approaches alongside links to comprehensive documentation.

### qtlocation
* 58f50363b Expose delegateModelAccess from QDeclarativeGeoMapItemView
MapItemView now has a new property delegateModelAccess. Setting it to
DelegateModel.ReadWrite allows you to write values into the model via
required properties just as you could with context properties.

### qtpositioning
* da73ce94 Fix QGeoPolygon::toString() output
The output of the QGeoPolygon::toString() method is updated to be more
readable. Users who rely on the old format (e.g. in tests) need to
update their code.

* 1fcb7acc Add QDataStream serialization support for
QGeoPolygon::holePath()
Added support for serialization of QGeoPolygon::holePath() to/from
QDataStream. This changes the format of QGeoPolygon serialization, so
make sure to set QDataStream::version() < Qt_6_10 if you need the old
behavior.

* d48abeab CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

* 66d963ba Make: Fix incorrect PURL version for clip2tri
Fixed incorrect PURL version for clip2tri in qt_attribution.json.

* 720b0cdc GeoClue2: Fix DesktopId property
The plugin now uses QGuiApplication::desktopFileName() if the desktopId
plugin parameter is not specified, and only falls back to
QCoreApplication::applicationName() if desktopFileName() is not defined.
The fall back path is scheduled to be dropped in the next major release
of Qt.

### qtsensors
* 55c8bbf3 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtconnectivity
* 82bd4aa0 BlueZ: prefer powered on adapters when no address is
specified
If the local adapter address is not specified, the Linux backend now
tries to pick the first powered on adapter instead of simply picking the
first in the list.

* dc4e6842 Add NFC tag UID support with neard
The neard backend on Linux now returns the correct UID from
QNearFieldTarget::uid() with neard v0.19 or newer. It previously
returned an empty QByteArray.

* 5be7b3fd CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtwayland
* 70e02a4f protocol: update version info of wayland.xml in
qt_attribution.json
Update wayland.xml to 1.23.0.

* ee706b8f CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qt3d
* ebff9e759 QRay3D: fix transform
Fix QRay3D::transform

* 1d2b0f3a4 Make module ready for source SBOM checking
Renaming the license files with prefix LICENSE. to have them ignored by
reuse tool.

* dc32953dd CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

* e8e98b896 Update assimp dependency
Update ASSIMP to 6.0.2

### qtimageformats
* b36ff4a Update bundled libwebp to version 1.5.0
Update bundled libwebp to version 1.5.0

* 0a700dd CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

* dfc2687 Update bundled libwebp to version 1.6.0
Update bundled libwebp to version 1.6.0

* 8d80b76 Update bundled libtiff to version 4.7.1
Bundled libtiff was updated to version 4.7.1

### qtserialbus
* 90b4fe48 Add QCanBusDeviceInfo move-constructor
Added the  move-constructor.

* c8a4309a VirtualCAN: Add support for 10 channels
The VirtualCAN plugin now supports up to ten virtual CAN channels from
can0 to can9.

* 93444f47 SocketCAN: Avoid "cannot set the bitrate" warning
The socketcan plugin no longer sets a default bitrate of 500000. The
bitrate must either be set up by system means (ip link set ...) or by
using libsocketcan and
setConfigurationParameter(QCanBusDevice::BitRateKey, ...).

### qtserialport
* 3f05f97d Windows: fix readyRead() signal emission
Fixed a bug where the readyRead() signal did not follow the QIODevice
docs and could be emitted recursively.

* 07d21cb0 QSerialPort: add write buffer size limit
Added writeBufferSize()/setWriteBufferSize() to limit the size of the
write buffer.

### qtvirtualkeyboard
* a65aa1d6 Add Latvian layout
Added Latvian keyboard layout.

* 918692eb CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtnetworkauth
* 44576da Change QAbstractOAuth2::expirationAt also when invalidated
Change expirationAt also if expires_in wasn't provided, or has invalid
value, and becomes invalid.

* b05d99c Move tokenUrl property to QAbstractOAuth2
Added tokenUrl property that holds the token endpoint URL.

* 90c7e3d Deprecate QOAuth2AuthorizationCodeFlow::accessTokenUrl
property
Deprecated accessTokenUrl property and scheduled it for removal in Qt
7. Use QAbstractOAuth2::tokenUrl instead.

### qtremoteobjects
* c03d630e Expose (private) API for creating QtRO types
Add external/private interface to support bindings (specifically
Python) to generate dynamic classes from .rep files.

### qtlottie
* fe885d9 Doc: Fix module name in qt_attribution.json files
Fixed Qt Lottie Animation module name in license source files.

### qtquick3d
* 3fcad9b7a Add paths to the sub-project attributions for openxr
Added more specific paths to the sub-projects included with openxr.

* 66b9c1e25 Make module ready for source SBOM checking
Renamed certain license files outside of LICENSES with `LICENSE.`
prefix such that reuse will correctly ignore them.

* f339c33b0 Add CapsuleGeometry to Helpers
Add CapsuleGeometry to QtQuick3D.Helpers.

* c1ddec5de Assimp: baseColorFactor is linear and needs to be sRGB
glTF2 Models that use baseColorFactor now work according to spec, but
will be differnt than before.

* f02df7ff2 Update meshoptimizer to v0.23
Updated meshoptimizer to v0.23

* e913a6fd0 Update TinyEXR to v1.0.12
Updated TinyEXR to v1.0.12

* c7c0389c0 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

* 495de8d46 Expose delegateModelAccess from QQuick3DRepeater
Repeater3D now has a new property delegateModelAccess. Setting it to
DelegateModel.ReadWrite allows you to write values into the model via
required properties just as you could with context properties.

* edaef10f4 Lightmapping: Use new custom file format
Add source property to Lightmapper. Deprecated
BakedLightmap::loadPrefix.

* 202b89413 Lightmapping: Add NLM GPU denoising support
Add support for denoising of baked lightmaps. Add
Lightmapper::denoiseSigma property. Add 'Denoise lightmap' button to
DebugView.

* d45e71e9d Lightmapping: Use texels-per-unit based sizes
Add Model::texelsPerUnit and Lightmapper::texelsPerUnit. Deprecate
Model::lightmapBaseResolution.

* 37ae21421 Update OpenXR to v1.1.49
Update OpenXR to v1.1.49

* 83f1f14d6 Update Assimp to v6.0.2
Update ASSIMP to v6.0.2

### qtshadertools
* 0352d5b Update SPIRV-Cross
SPIRV-Cross was updated to match the bundled one in Vulkan SDK
1.4.304.0.

* 0f07627 Update to glslang 15.0.1
glslang was updated to 15.0.1.

* 31fdb26 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qt5compat
* 63add2f QStringRef: fix lost null-ness when converting to QStringView
Fixed a Qt 6 regression where conversion to QStringView would no longer
preserve nullness.

* 5f94627 QStringRef: preserve null-ness when converting to
QAnyStringView
Fixed missing conversion to QAnyStringView.

* f9576fa Make module ready for source SBOM checking
Renaming the license files with prefix LICENSE. to have them ignored by
reuse tool.

* 62d01b6 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtopcua
* 46c3d8a4 Update bundled open62541 to v1.4.9
The bundled open62541 was updated to v1.4.9

* 1f985995 Fix handling of ByteString node ids with null bytes
Fix a bug that prevented ByteString node ids    with null bytes from
being used.

* 78f49db2 Fix anonymous authentication for secure connections
Fix a bug where anonymous authentication over a secure connection was
broken

* a2afb729 Fix SimpleAttributeOperand conversion in the open62541 plugin
Fix an interoperability issue with the    Siemens OPC UA server where
the conditionId could not be selected    in an event filter.

* 5996e343 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

* 0e985c64 Fix authentication over a None policy secure channel
Using encrypted auth tokens over a None    security policy channel is
again possible after it was broken    with the update to open62541 1.4
in Qt 6.9.

* 757560f0 Fix error handling for security policy initialization
Fix a segfault if a client is initialized    with a corrupt certificate
file.

* 5821fa4f Fix detach() for QOpcUaDataValue
QOpcUaDataValue now detaches its shared data    as expected when
timestamp picoseconds are set.

* 3fec14b2 Update bundled open62541 to v1.4.13
The bundled open62541 was updated to v1.4.13

### qthttpserver
* fdc52d1 Split QHttpServerRequestPrivate into itself and
QHttpServerParser 4/4
Made QHttpServerRequest copyable

* c408098 Add keep-alive timeout for QHttpServer
Add methods to configure keep-alive timeout for QHttpServer.

### qtquick3dphysics
* e05ab04 PhysicsWorld: Simulate after frame render
Make simulation frames work in lockstep with rendered frames.

### qtgrpc
* 4b778a70 Avoid generating QList aliases for the protobuf messages
qtprotobufgen doesn't generate protobuf message QList aliases. All
usages of aliases should be replace by respective QList types. Aliases
are still generated and are guarded by the QT_USE_PROTOBUF_LIST_ALIASES
macro in the generated code. The macro is enabled by default and can be
disabled using QT_USE_PROTOBUF_LIST_ALIASES target property.

* 77fd3117 Add the early return from qt6_add_<protobuf|grpc>
The qt6_add_protobuf and qt6_add_grpc functions do not generate CMake
targets if provided in PROTO_FILES argument protobuf schemes do not
contain the corresponding for the generator definitions. qtprotobufgen
requires messages or enums, qtgrpcgen requires services. Functions now
make early return and warn about the missing definitions. Previosly the
functions generated unclear FATAL_ERROR. The
QT_SKIP_PROTOBUF_MISSING_DEFINITIONS_WARNING CMake variable suppresses
the warning.

* 65358c24 QGrpcHttp2Channel: Add user-agent header
Added a structured user-agent string to the request headers.

* 6a9810ed QGrpcHttp2Channel: Add QLocalSocket abstract namespace
support
Added abstract namespace support for QLocalSocket communication through
the "unix-abstract" scheme.

* d6586d97 Long live mutable getters
The generated messages now have the mutable getters for the fiels of
the message type. The getters have 'mut' prefix and implicily allocate
the respective fields if needed, so the use of intermediate message
objects is not required.

* 778371b8 Deprecate QHash<QBA,QBA> metadata in favor of QMultiHash
Deprecate the metadata()/setMetadata() methods on QGrpcCallOptions and
QGrpcChannelOptions that use QHash in favor of the new overloads that
use QMultiHash. This is more in line with the gRPC specification.

* 66984e6a QGrpc{Channel,Call}Options: Support incremental updates via
addMetadata
Added support for incrementally adding metadata via `addMetadata()`.

* 331c681f CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

* c1b74039 Emit cancelled finished() in channel implementation
Cancellation logic should also emit finished now. Custom
QAbstractGrpcChannel implementations should adapt their logic.

* c4eb1ea7 Deprecate serverMetadata for server{Initial,Trailing}Metadata
Deprecate the metadata()/serverMetadata()/setServerMetadata() methods
on QGrpcOperation and QGrpcOperationContext that use QHash in favor of
the new server{Initial,Trailing}Metadata interfaces, that use QMultiHash
and provide the correct handling of the received metadata in their
respective phase. This is a behavior change as the old metadata()
interface now only returns the initial metadata.

* c54cacce QGrpc{Call,Channel}Options: add 'filterServerMetadata'
Added the filterServerMetadata property.

* cd368c94 QGrpcHttp2Channel: implement filterServerMetadata option
QGrpcOperation::serverInitialMetadata() and
QGrpcOperation::serverTrailingMetadata() no longer include any internal
gRPC or HTTP/2 pseudo‑headers by default.

* 20a543c1 QGrpcHttp2Channel: Guarantee transportation scheme
Requesting TLS or QLocalSocket now fails with a fatal error if the
requested transport is unavailable.

### qtapplicationmanager (Commercial only)
* 7f6fe311 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

### qtinterfaceframework (Commercial only)
* 977b1ad1 Update license check
Rename license file with LICENSE. prefix. This way the file is ignored
by the reuse tool.

* d6883b61 CMake: Add PURL and CPE info to 3rd party attribution files
Added PURL and CPE information to the attribution files of 3rd party
sources.

* 6c30c4b7 Update the bundled qface to the latest version (2.0.13)
The copy of qface in Qt was updated to 2.0.13

### qtinsighttracker (Commercial only)
* 64d0cf1 Add API for sending additional data
Additional data can now be tracked without attaching it to any other
event.


Fixes
-----

### qtbase
* [QTBUG-130313](https://bugreports.qt.io/browse/QTBUG-130313) Garbage text output
* [QTBUG-131976](https://bugreports.qt.io/browse/QTBUG-131976) The alternateBase color in dark W11 style is wrong
* [QTBUG-131913](https://bugreports.qt.io/browse/QTBUG-131913) Incorrect QTimeZone documentation
* [QTBUG-45949](https://bugreports.qt.io/browse/QTBUG-45949) QToolBar icon-size can not be styled as documented
* [QTBUG-132066](https://bugreports.qt.io/browse/QTBUG-132066) contextMenuEvent no longer works
* [QTBUG-131983](https://bugreports.qt.io/browse/QTBUG-131983) text input v3: first character after refocus doesn't go
through the input method
* [QTBUG-132075](https://bugreports.qt.io/browse/QTBUG-132075) tst_qquicktext::multilengthStrings(Wrap) Compared
doubles are not the same (fuzzy compare)
* [QTBUG-132101](https://bugreports.qt.io/browse/QTBUG-132101) Extra semicolon warnings in qdirlisting.h, qaccessible.h
and qkeysequence.h
* [QTBUG-112746](https://bugreports.qt.io/browse/QTBUG-112746) QAnyStringView missing implicit conversion from char[]
with unknown size
* [QTBUG-132111](https://bugreports.qt.io/browse/QTBUG-132111) qtbase/fa4bd30caa079a3b1e5eac1bb4f17365f456b8f9 breaks
-unity-build
* [QTBUG-132115](https://bugreports.qt.io/browse/QTBUG-132115) QDateTimeParser::parse assertion triggered in case of
invalid date
* [QTBUG-132053](https://bugreports.qt.io/browse/QTBUG-132053) FTBFS: Compilation of qsharedmemory_p.h fails with
sysv_sem disabled
* [QTBUG-73390](https://bugreports.qt.io/browse/QTBUG-73390) QMenu Action is not triggered by numeric mnemonic entered
on keypad
* [QTBUG-127522](https://bugreports.qt.io/browse/QTBUG-127522) QBENCHMARK result does not output global data tag
* [QTBUG-132150](https://bugreports.qt.io/browse/QTBUG-132150) androiddeployqt does not strip quotation marks from
static namespace string retrieved from build.gradle
* [QTBUG-122797](https://bugreports.qt.io/browse/QTBUG-122797) QStringRef doesn't convert to QAnyStringView
* [QTBUG-139425](https://bugreports.qt.io/browse/QTBUG-139425) Wayland: QEventLoop::ExcludeUserInputEvents doesn't work
* [QTBUG-122798](https://bugreports.qt.io/browse/QTBUG-122798) [REG 5.15 -> 6.7 (or earlier)] QStringRef -> QStringView
conversion loses null-ness
* [QTBUG-131586](https://bugreports.qt.io/browse/QTBUG-131586)  QLineEdit's bottom edge is the wrong color when in Dark
mode.
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
* [QTBUG-132102](https://bugreports.qt.io/browse/QTBUG-132102) Windows: Fusion style: Combo-box list: Item with icon
and long text sometimes has elide
* [QTBUG-130992](https://bugreports.qt.io/browse/QTBUG-130992) Crash when rendering radialGradient
* [QTBUG-132104](https://bugreports.qt.io/browse/QTBUG-132104) QVariant::fromValue fails with std::unordered_map
* [QTBUG-87776](https://bugreports.qt.io/browse/QTBUG-87776) Move Qt::FooPrivate targets into separate CMake packages
* [QTBUG-131716](https://bugreports.qt.io/browse/QTBUG-131716) QCommandLineParser::helpText fails if no options are
added
* [QTBUG-132347](https://bugreports.qt.io/browse/QTBUG-132347) blake2b symbols exported in static builds
* [QTBUG-132332](https://bugreports.qt.io/browse/QTBUG-132332) QSaveFile will empty file if no space left on device
* [QTBUG-132431](https://bugreports.qt.io/browse/QTBUG-132431) Stylesheet Margin/Padding squashes QSpinBox
* [QTBUG-130642](https://bugreports.qt.io/browse/QTBUG-130642) Incorrect QAbstractSpinBox size hint in Windows 11 style
when style sheet is set
* [QTBUG-131959](https://bugreports.qt.io/browse/QTBUG-131959) Build failure on QtFuture::whenAll(QFuture<void>,
QFuture<void>)
* [QTBUG-132387](https://bugreports.qt.io/browse/QTBUG-132387) FAIL!  : tst_qqmlengine::uiLanguage() Not all expected
messages were received
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
* [QTBUG-131843](https://bugreports.qt.io/browse/QTBUG-131843) File/Folder link overlay is missing, or wrong
size/position
* [QTBUG-123843](https://bugreports.qt.io/browse/QTBUG-123843) Swipping with three finger between apps may cause a
crash after interacting with a text input field
* [QTBUG-132059](https://bugreports.qt.io/browse/QTBUG-132059) Crash when quickly invoking subsequent scrollAction
* [QTBUG-132281](https://bugreports.qt.io/browse/QTBUG-132281) Add change-notification signal to
QInputDevice::capabilities property
* [QTBUG-129242](https://bugreports.qt.io/browse/QTBUG-129242) QTableWidget selection issue
* [QTBUG-132381](https://bugreports.qt.io/browse/QTBUG-132381) [REG 6.8 -> 6.9] Crash when QGuiApplication is static
* [QTBUG-130895](https://bugreports.qt.io/browse/QTBUG-130895) Living QThread after termination
* [QTBUG-129927](https://bugreports.qt.io/browse/QTBUG-129927) [REG: 6.7 -> 6.8] Use after free in QTimeZone
* [QTBUG-129846](https://bugreports.qt.io/browse/QTBUG-129846) Quit in GUI application on linux in qt 6.8.0 does not
quit and process runs indefinitely
* [QTBUG-130341](https://bugreports.qt.io/browse/QTBUG-130341) Crash during QNetworkAccessManager destruction
* [QTBUG-117996](https://bugreports.qt.io/browse/QTBUG-117996) [REG 6.2 -> 6.5] QBasicTimer::stop: Failed. Possibly
trying to stop from a different thread
* [QTBUG-132410](https://bugreports.qt.io/browse/QTBUG-132410) Q_JNI_NATIVE_METHOD floating point argument corruption
on x86_64
* [QTBUG-132414](https://bugreports.qt.io/browse/QTBUG-132414) embedding a widget window in qml does not draw the
window
* [QTBUG-132581](https://bugreports.qt.io/browse/QTBUG-132581) QMake triggers abnormally many "zero as null pointer
constant" warnings on macOS
* [QTBUG-132622](https://bugreports.qt.io/browse/QTBUG-132622) Failed to find required Qt component "Protobuf"
* [QTBUG-132616](https://bugreports.qt.io/browse/QTBUG-132616) Failed to find the host tool "Qt6::qtwaylandscanner"
* [QTBUG-132597](https://bugreports.qt.io/browse/QTBUG-132597) Incorrect description of QTemporaryFile behavior when
two placeholders are present
* [QTBUG-132670](https://bugreports.qt.io/browse/QTBUG-132670) QTreeView does not always refresh on dataChanged
* [QTBUG-124173](https://bugreports.qt.io/browse/QTBUG-124173) QTreeView / QTableView dataChanged very slow when
topLeft and bottomRight span many items
* [QTBUG-131372](https://bugreports.qt.io/browse/QTBUG-131372) QStandardItem::appendRow does not update model
recursively
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
* [QTBUG-132255](https://bugreports.qt.io/browse/QTBUG-132255) Different emoji font resolution in Freetype on Windows
* [QTBUG-87417](https://bugreports.qt.io/browse/QTBUG-87417) tst_QLineEdit fails on Android
* [QTBUG-132841](https://bugreports.qt.io/browse/QTBUG-132841) Android QtAbstractItemModel wrong JNI call for sibling()
method
* [QTBUG-129698](https://bugreports.qt.io/browse/QTBUG-129698) Widget doesn't show after windowHandle()->destroy()
* [QTBUG-125892](https://bugreports.qt.io/browse/QTBUG-125892) QtDS compatibility - Improve qmldir path discovery
* [QTBUG-125970](https://bugreports.qt.io/browse/QTBUG-125970) QML components with the same name under a module
* [QTBUG-125971](https://bugreports.qt.io/browse/QTBUG-125971) Java QML codegen source file handling
* [QTBUG-132804](https://bugreports.qt.io/browse/QTBUG-132804) Debug build fails at qgenericunixthemes.cpp
* [QTBUG-125285](https://bugreports.qt.io/browse/QTBUG-125285) QKdeTheme falls back to Qt::ColorScheme::Unknown on
invalid desktop theme
* [QTBUG-132873](https://bugreports.qt.io/browse/QTBUG-132873) QtWidgets: QEvent::ContextMenu is not spontaneous in
6.9.0 beta 2 anymore
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
* [QTBUG-132911](https://bugreports.qt.io/browse/QTBUG-132911) Typo in QPermission docs
* [QTBUG-70798](https://bugreports.qt.io/browse/QTBUG-70798) Qfiledialog Does Not Correctly Restore the Directory
* [QTBUG-122381](https://bugreports.qt.io/browse/QTBUG-122381) Windows cursor changes not refreshing (excessive
caching)
* [QTBUG-130884](https://bugreports.qt.io/browse/QTBUG-130884) xdg-desktop-portal should be enabled only environments
that actually supports it
* [QTBUG-131894](https://bugreports.qt.io/browse/QTBUG-131894) qtranslator loads wrong locale
* [QTBUG-132575](https://bugreports.qt.io/browse/QTBUG-132575) QEasingCurve streaming operators (in/out a QDataStream)
will crash
* [QTBUG-132609](https://bugreports.qt.io/browse/QTBUG-132609) Configuring a single-config qtopcua might fail to build
tools when built against a multi-config Qt
* [QTBUG-132338](https://bugreports.qt.io/browse/QTBUG-132338) QtOpcUa Required QtVersion Wrong
* [QTBUG-122642](https://bugreports.qt.io/browse/QTBUG-122642) The SQL QODBC driver implementation fails to escape
passwords set with setPassword(...) when using special characters.
* [QTBUG-132801](https://bugreports.qt.io/browse/QTBUG-132801) Building Qt with separate debug info fails on QNX
* [QTBUG-128790](https://bugreports.qt.io/browse/QTBUG-128790) Adding a QQuickWidget at runtime changes window position
* [QTBUG-132173](https://bugreports.qt.io/browse/QTBUG-132173) The cell borders in QTextTableFormat are not being
painted.
* [QTBUG-132724](https://bugreports.qt.io/browse/QTBUG-132724) `qt_internal_generate_user_facing_tools_info` is not
relocatable
* [QTBUG-118176](https://bugreports.qt.io/browse/QTBUG-118176) qdoc: Generate \internal documentation correctly when
--showinternal is set
* [QTBUG-57209](https://bugreports.qt.io/browse/QTBUG-57209) Wrong documentation for QOpenGLTexture::setWrapMode
* [QTBUG-130912](https://bugreports.qt.io/browse/QTBUG-130912) [Windows] Child window with Qt.WindowDoesNotAcceptFocus
flag set still grabs focus
* [QTBUG-132356](https://bugreports.qt.io/browse/QTBUG-132356) Out-of-bounds read in
QRhiVulkan::endAndSubmitPrimaryCommandBuffer
* [QTBUG-133128](https://bugreports.qt.io/browse/QTBUG-133128) Windows11Style: QSlider min position off
* [QTBUG-132906](https://bugreports.qt.io/browse/QTBUG-132906) Reg[6.5->6.8]Windows11 style crashing with drawPrimitive
* [QTBUG-132952](https://bugreports.qt.io/browse/QTBUG-132952) Mouse messages for QDockWidget are incorrectly cast to
QMainWindow causing a crash
* [QTBUG-132808](https://bugreports.qt.io/browse/QTBUG-132808) Vulkan validation error on vkAcquireNextImageKHR (using
validation layer bundled with 1.4.304)
* [QTBUG-122819](https://bugreports.qt.io/browse/QTBUG-122819) QOpenGLWidget: error: GL_INVALID_OPERATION in
glDrawBuffers(unsupported buffer GL_BACK_LEFT)
* [QTBUG-132780](https://bugreports.qt.io/browse/QTBUG-132780) Faulty call to glDrawBuffers in RhiGles2 backend
* [QTBUG-112758](https://bugreports.qt.io/browse/QTBUG-112758) QMdiArea (in TabbedView mode): issues after moving tab
* [QTBUG-113458](https://bugreports.qt.io/browse/QTBUG-113458) DirectWrite don't handle CBDT, COLRv1, sbix, SVG color
fonts
* [QTBUG-132935](https://bugreports.qt.io/browse/QTBUG-132935) a11y: Qt application on Linux doesn't report accessible
parent
* [QTBUG-116016](https://bugreports.qt.io/browse/QTBUG-116016) QTextEdit clips placeholder text
* [QTBUG-133207](https://bugreports.qt.io/browse/QTBUG-133207) REG: Controls C++ tests not run with all styles
* [QTBUG-133289](https://bugreports.qt.io/browse/QTBUG-133289) Moving window container crashes if the window has been
destroyed
* [QTBUG-129233](https://bugreports.qt.io/browse/QTBUG-129233) tooltip will change focus on webassembly
* [QTBUG-133330](https://bugreports.qt.io/browse/QTBUG-133330) tst_qmenu crashes with MSVC in debug mode
* [QTBUG-132945](https://bugreports.qt.io/browse/QTBUG-132945) QDuplicateTracker::clear() leaks memory
* [QTBUG-132831](https://bugreports.qt.io/browse/QTBUG-132831) QSet::remove() unconditionally detaches
* [QTBUG-133336](https://bugreports.qt.io/browse/QTBUG-133336) FTBFS MinGW no matching function for call to
'IDWritePaintReader::MoveToFirstChild(DWRITE_PAINT_ELEMENT*)'
* [QTBUG-56952](https://bugreports.qt.io/browse/QTBUG-56952) [REG: 5.4.2->5.5.0] Duplicated hotkeys in menus not
working in some styles if first action is disabled
* [QTBUG-132752](https://bugreports.qt.io/browse/QTBUG-132752) QSqlQuery issues a deprecation warning in QMetaType
* [QTBUG-91766](https://bugreports.qt.io/browse/QTBUG-91766) Changing copy of QSqlQuery changes original.
* [QTBUG-133445](https://bugreports.qt.io/browse/QTBUG-133445) ibus x11 doesn't work in 6.9 and dev on Ubuntu 24.04
GNOME
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
* [QTBUG-133403](https://bugreports.qt.io/browse/QTBUG-133403) [REG 6.8.0 -> 6.8.1]
QUrl::adjusted(NormalizePathSegments) can produce an invalid URL
* [QTBUG-133402](https://bugreports.qt.io/browse/QTBUG-133402) [REG 6.8.0 -> 6.8.1] QUrl::resolved() can produce an
invalid path like "/../"
* [QTBUG-133032](https://bugreports.qt.io/browse/QTBUG-133032) Qt 6.8.1 "isRelocatable: undeclared identifier"
* [QTBUG-132490](https://bugreports.qt.io/browse/QTBUG-132490) Android and TestNamespace: errors in Qt JNI methods
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
* [QTBUG-133525](https://bugreports.qt.io/browse/QTBUG-133525) [REG] mac style: merged title bar and content area no
longer works
* [QTBUG-132589](https://bugreports.qt.io/browse/QTBUG-132589) Android Edit text context menu pointers are in wrong
place
* [QTBUG-133651](https://bugreports.qt.io/browse/QTBUG-133651) uic: Changing Palette in Designer breaks UI with Qt
5.15.2
* [QTBUG-118032](https://bugreports.qt.io/browse/QTBUG-118032) Application crash due to double invocation of
continuation in multithreaded QPromise and QFuture usage
* [QTBUG-130662](https://bugreports.qt.io/browse/QTBUG-130662) QFuture::cancel() is impractical on continuation chains
* [QTBUG-132249](https://bugreports.qt.io/browse/QTBUG-132249) AndroidTestRunner: allow to call additional/extra adb
call
* [QTBUG-118997](https://bugreports.qt.io/browse/QTBUG-118997) missing D-Bus Viewer manual
* [QTBUG-133376](https://bugreports.qt.io/browse/QTBUG-133376) #warning preprocessor macro is used in
qtdeprecationdefinitions.h
* [QTBUG-132314](https://bugreports.qt.io/browse/QTBUG-132314) GPU driver crash in iOS 18
* [QTBUG-133480](https://bugreports.qt.io/browse/QTBUG-133480) Combined flag emojis are not properly rendered
* [QTBUG-133456](https://bugreports.qt.io/browse/QTBUG-133456) Top flaky test: tst_Android::testFullScreenDimensions
* [QTBUG-133689](https://bugreports.qt.io/browse/QTBUG-133689) tst_qbytearrayview fails to compile with libc++ 19
* [QTBUG-133663](https://bugreports.qt.io/browse/QTBUG-133663) QDesktopServices::openUrl() misses query part
* [QTBUG-127528](https://bugreports.qt.io/browse/QTBUG-127528) QApplication::fontMetrics() deprecation message is too
vague
* [QTBUG-133644](https://bugreports.qt.io/browse/QTBUG-133644) [REG 6.6.3 -> 6.8.1] Assertion failure at QApplication
destruction
* [QTBUG-133744](https://bugreports.qt.io/browse/QTBUG-133744) QString assertion failure using UTF-16 character in
QJsonObject key
* [QTBUG-133725](https://bugreports.qt.io/browse/QTBUG-133725) qml_tool_autogen target loses almost all dependencies on
other autogen and sync_headers targets
* [QTBUG-133776](https://bugreports.qt.io/browse/QTBUG-133776) calling exit after constructing QApplication crash
* [QTBUG-133808](https://bugreports.qt.io/browse/QTBUG-133808) Including QFlag causes compilation failure with Clang
19, libcpp, and C++23
* [QTBUG-127116](https://bugreports.qt.io/browse/QTBUG-127116) REG: QML Window Background Issue on Windows After
Minimizing and Restoring in Qt 6.5+
* [QTBUG-133754](https://bugreports.qt.io/browse/QTBUG-133754) QtQuickView contents are sized too large
* [QTBUG-133810](https://bugreports.qt.io/browse/QTBUG-133810) CMake Multi-ABI builds not copying sub-ABIs libraries
* [QTBUG-131862](https://bugreports.qt.io/browse/QTBUG-131862) Android multi-ABI build stopped working
* [QTBUG-133500](https://bugreports.qt.io/browse/QTBUG-133500) [REG 6.8.1 -> 6.8.2] Crash on exit during logging of
thread destruction
* [QTBUG-133850](https://bugreports.qt.io/browse/QTBUG-133850) Using qt_wrap_ui causes build failure
* [QTBUG-133269](https://bugreports.qt.io/browse/QTBUG-133269) QTextStream: suspicious negation when streaming numbers
* [QTBUG-133118](https://bugreports.qt.io/browse/QTBUG-133118) Windows11Style: Item view selection hardly legible
* [QTBUG-132121](https://bugreports.qt.io/browse/QTBUG-132121) Bad signal restoration cause infinite loop in
FatalSignalHandler destructor
* [QTBUG-133825](https://bugreports.qt.io/browse/QTBUG-133825) tst_QDialog::keepPositionOnClose flaky on Opensuse
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
* [QTBUG-125225](https://bugreports.qt.io/browse/QTBUG-125225) RHI - Support for int texture formats
* [QTBUG-133954](https://bugreports.qt.io/browse/QTBUG-133954) Make sure that new 'Classes for string data' can be
found in TOC
* [QTBUG-129300](https://bugreports.qt.io/browse/QTBUG-129300) Cannot bind QRhi 3D texture to shader in DirectX 11 and
12 (with working workaround)
* [QTBUG-133407](https://bugreports.qt.io/browse/QTBUG-133407) Tools in qtbase fail to link to QtCore when Qt is
statically built
* [QTBUG-133261](https://bugreports.qt.io/browse/QTBUG-133261) qRound does not handle overflow
* [QTBUG-133834](https://bugreports.qt.io/browse/QTBUG-133834) Fusion Style: QMdiArea close button looks clipped with
fractional scaling
* [QTBUG-133940](https://bugreports.qt.io/browse/QTBUG-133940) Qt::CustomizeWindowHint has no effect on Windows
* [QTBUG-132705](https://bugreports.qt.io/browse/QTBUG-132705) Qt CMake content uses compiler config from qtbase,
instead the current modules
* [QTBUG-134073](https://bugreports.qt.io/browse/QTBUG-134073) QMimeData does not escape square brackets in text/uri-
list
* [QTBUG-134101](https://bugreports.qt.io/browse/QTBUG-134101) Qt 6.9.0 with uncompressed libraries doesn't work with
split APKs
* [QTBUG-115356](https://bugreports.qt.io/browse/QTBUG-115356) QMenu clips text for actions with icons with larger
fonts
* [QTBUG-131893](https://bugreports.qt.io/browse/QTBUG-131893) QToolButton menu selections fail to highlight when in
QMdiSubwindow
* [QTBUG-107904](https://bugreports.qt.io/browse/QTBUG-107904) Qt Designer crashes when set a negative value in border-
image
* [QTBUG-134210](https://bugreports.qt.io/browse/QTBUG-134210) Infinite recursion of a QSortFilterProxyModel with a
QConcatenateTablesProxyModel  as source
* [QTBUG-131256](https://bugreports.qt.io/browse/QTBUG-131256) QTextEdit will block and crash by
QEventLoop::WaitForMoreEvents when  pressing or dragging selected text
* [QTBUG-134235](https://bugreports.qt.io/browse/QTBUG-134235) Build failure of qtbase/src/widgets/styles/qdrawutil.cpp
with disabled features
* [QTBUG-132187](https://bugreports.qt.io/browse/QTBUG-132187) QDrawUtil: qDrawPlainRoundedRect does not work well for
high-dpi screens
* [QTBUG-133406](https://bugreports.qt.io/browse/QTBUG-133406) Unrechable code in MetaTypeQFutureHelper
* [QTBUG-134392](https://bugreports.qt.io/browse/QTBUG-134392) Copyright holder missing
qtbase/config.tests/armintrin/main.cpp
* [QTBUG-134316](https://bugreports.qt.io/browse/QTBUG-134316) [Reg] QFileOpenEvent isn't emitted for custom URI
* [QTBUG-133412](https://bugreports.qt.io/browse/QTBUG-133412) QFileDialog drive icons incorrect scaling on screen with
non-integer device pixel ratio
* [QTBUG-132929](https://bugreports.qt.io/browse/QTBUG-132929) QStyleHints::setColorScheme() doesn't affect the
application's theme on Ubuntu
* [QTBUG-125534](https://bugreports.qt.io/browse/QTBUG-125534) qt-internal-{ninja,strip}.bat.in are installed as
executable
* [QTBUG-134407](https://bugreports.qt.io/browse/QTBUG-134407) Using a -no-prefix macOS Qt that was built with CMake
3.24 is not possible
* [QTBUG-134425](https://bugreports.qt.io/browse/QTBUG-134425) Clarify the purpose of FEATURE_precompile_header
* [QTBUG-134393](https://bugreports.qt.io/browse/QTBUG-134393) qtwasmserver doesn't use the provided path parameter to
serve assets
* [QTBUG-133922](https://bugreports.qt.io/browse/QTBUG-133922) fr_CH is listed twice by QLocale::matchingLocales
* [QTBUG-134473](https://bugreports.qt.io/browse/QTBUG-134473) Font rendering of Qt Creators Text Editor is broken
* [QTBUG-134415](https://bugreports.qt.io/browse/QTBUG-134415) Qt FTBFS with GCC < 15 + TSAN + PCH + developer-build
* [QTBUG-134080](https://bugreports.qt.io/browse/QTBUG-134080) "QObject::~QObject: Timers cannot be stopped from
another thread" message in Qt 6.8.2 plugins
* [QTBUG-133861](https://bugreports.qt.io/browse/QTBUG-133861) [macOS] QML Preview: Closing the preview window produces
QObject::killTimer warning
* [QTBUG-134533](https://bugreports.qt.io/browse/QTBUG-134533) Fusion style: SH_EtchDisabledText in disable QMenu looks
blurry
* [QTBUG-127713](https://bugreports.qt.io/browse/QTBUG-127713) QProgressBar does not set a localisable label value by
default
* [QTBUG-134538](https://bugreports.qt.io/browse/QTBUG-134538) QRandomGenerator, QSimd: RDSEED should be checked for
validity
* [QTBUG-130063](https://bugreports.qt.io/browse/QTBUG-130063) QKeySequence(<QString>) doesn't parse correctly when we
have a space
* [QTBUG-133942](https://bugreports.qt.io/browse/QTBUG-133942) Qt::ExpandedClientAreaHint results in losing default
window title on Windows
* [QTBUG-133702](https://bugreports.qt.io/browse/QTBUG-133702) [Android] QDesktopServices::openUrl(): FileProvider
unable to get URI for sharing file
* [QTBUG-133710](https://bugreports.qt.io/browse/QTBUG-133710) Fix padding in tabs for pre elements
* [QTBUG-40283](https://bugreports.qt.io/browse/QTBUG-40283) QSettings: Documentation and implementation differ
* [QTBUG-134497](https://bugreports.qt.io/browse/QTBUG-134497) Mouse hover stylesheet does not renders correct color in
windows11
* [QTBUG-134727](https://bugreports.qt.io/browse/QTBUG-134727) QNetworkAccessManager cannot access IPv6 link-local
addresses having a zone id
* [QTBUG-134075](https://bugreports.qt.io/browse/QTBUG-134075) Windows Server 2016 is no longer working
* [QTBUG-134699](https://bugreports.qt.io/browse/QTBUG-134699) Performance regression in QDirIterator when going from
6.5.3 to 6.8.2 [REG 6.5.3->6.8.2]
* [QTBUG-134447](https://bugreports.qt.io/browse/QTBUG-134447) Modal dialog looks disabled
* [QTBUG-133945](https://bugreports.qt.io/browse/QTBUG-133945) Qt::ExpandedClientAreaHint results in wrong color for
close button on Windows
* [QTBUG-133941](https://bugreports.qt.io/browse/QTBUG-133941) Qt::ExpandedClientAreaHint results in losing window icon
on Windows
* [QTBUG-134718](https://bugreports.qt.io/browse/QTBUG-134718) FAIL!  : tst_controls::Basic::SwipeDelegate::test_remova
bleDelegates(touch_rotation_90) Received a fatal error
* [QTBUG-134313](https://bugreports.qt.io/browse/QTBUG-134313) can't drag application/x-color from one Qt application
to another (is it hex or raw?)
* [QTBUG-134683](https://bugreports.qt.io/browse/QTBUG-134683) Deprecated one argument version of qHash still required
in qHashMulti
* [QTBUG-126659](https://bugreports.qt.io/browse/QTBUG-126659) New QMap.qHash leading to ambiguous calls
* [QTBUG-134690](https://bugreports.qt.io/browse/QTBUG-134690) qHashMulti and qHashMultiCommutative use the slower
seed==0 algorithms for strings
* [QTBUG-132191](https://bugreports.qt.io/browse/QTBUG-132191) wasm: QTcpSocket signals connected rather errorOccurred
* [QTBUG-15125](https://bugreports.qt.io/browse/QTBUG-15125) QDomAttr QDomElement::setAttributeNode ( const QDomAttr &
newAttr ) does NOT replaces attribute with the same name as newAttr.
* [QTBUG-132430](https://bugreports.qt.io/browse/QTBUG-132430) Everything says "setHighDpiScaleFactorRoundingPolicy
must be called before creating the QGuiApplication instance"
* [QTBUG-28721](https://bugreports.qt.io/browse/QTBUG-28721) QXmlStreamWriter writes newline at beginning of stream if
auto formatting is enabled.
* [QTBUG-134424](https://bugreports.qt.io/browse/QTBUG-134424) Enable precompiled headers also when building submodules
stand-alone
* [QTBUG-134768](https://bugreports.qt.io/browse/QTBUG-134768) QLocale::toStrings uses E instead of e
* [QTBUG-134785](https://bugreports.qt.io/browse/QTBUG-134785) Provide QLocale::toString() floating-point formats for
locale-appropriate case of exponent
* [QTBUG-134930](https://bugreports.qt.io/browse/QTBUG-134930) [REG 6.9] QLabel scaled pixmap is broken
* [QTBUG-134694](https://bugreports.qt.io/browse/QTBUG-134694) QNetworkAccessManager re-sends destructive requests
(POST, possibly others) without user intervention
* [QTBUG-134756](https://bugreports.qt.io/browse/QTBUG-134756) QJsonValue::fromVariant converts integers incorrectly
* [QTBUG-133522](https://bugreports.qt.io/browse/QTBUG-133522) Continuation on 'mapped' yields single result only
* [QTBUG-134540](https://bugreports.qt.io/browse/QTBUG-134540) Windows 10 1809: ICU.dll is not available
* [QTBUG-134610](https://bugreports.qt.io/browse/QTBUG-134610) Disconnect all -> crash in QAccessibilityCache
* [QTBUG-132459](https://bugreports.qt.io/browse/QTBUG-132459) Windows11 style: QProgressBar needs some work
* [QTBUG-99957](https://bugreports.qt.io/browse/QTBUG-99957) No rule to make target 'qtbase/src/platformsupport/input/
CMakeFiles/InputSupportPrivate.dir/cmake_pch.hxx.gch
* [QTBUG-134626](https://bugreports.qt.io/browse/QTBUG-134626) [6.8.1 -> 6.8.2] Thicker text underline with certain
fonts (X11)
* [QTBUG-132310](https://bugreports.qt.io/browse/QTBUG-132310) Crash in QCocoaAccessible::shouldBeIgnored
* [QTBUG-135033](https://bugreports.qt.io/browse/QTBUG-135033) QXmlStreamReader::addData() can parse Latin1 data
incorrectly
* [QTBUG-134702](https://bugreports.qt.io/browse/QTBUG-134702) QT_QPA_PLATFORMTHEME=generic doesn't work on KDE and GTK
environments
* [QTBUG-134703](https://bugreports.qt.io/browse/QTBUG-134703) Setting XDG_CURRENT_DESKTOP to xdgdesktopportal, flatpak
or snap causes an instant crash
* [QTBUG-134602](https://bugreports.qt.io/browse/QTBUG-134602) Rendering of QQuickText slightly elevated.
* [QTBUG-135109](https://bugreports.qt.io/browse/QTBUG-135109) some POSIX-style TZ strings are not supported by Qt on
some Linux-based platform
* [QTBUG-135204](https://bugreports.qt.io/browse/QTBUG-135204) qgenericunixtheme.cpp: undefined reference to
`QKdeTheme::name'
* [QTBUG-130576](https://bugreports.qt.io/browse/QTBUG-130576) Touches Are Handled Incorrectly with QDialog on Qt 6.8.x
Android
* [QTBUG-127925](https://bugreports.qt.io/browse/QTBUG-127925) Touch events end up in wrong place with Widgets gallery
on Android
* [QTBUG-134788](https://bugreports.qt.io/browse/QTBUG-134788) Copyright footer shows previous year
* [QTBUG-134913](https://bugreports.qt.io/browse/QTBUG-134913) QLocale::toDouble() gives unexpected result for same
decimal and grouping symbol
* [QTBUG-135159](https://bugreports.qt.io/browse/QTBUG-135159) QIcon::fromTheme selects 32px icon instead of 16@2x with
devicePixelRatio 2
* [QTBUG-76976](https://bugreports.qt.io/browse/QTBUG-76976) QSortFilterProxyModel::mapFromSource returns a valid
QModelIndex for the filtered out item
* [QTBUG-127517](https://bugreports.qt.io/browse/QTBUG-127517) Reports of misaligned loads with asan on AArch64 / xcb
* [QTBUG-134784](https://bugreports.qt.io/browse/QTBUG-134784) macos: Crash in Voice Over/Accessiblity when resetting a
table model
* [QTBUG-135238](https://bugreports.qt.io/browse/QTBUG-135238) QDateTime::toTimeZone doc's code snippet calls
deprecated ::toTimeSpec
* [QTBUG-135163](https://bugreports.qt.io/browse/QTBUG-135163) QThread::isRunning returns false while the thread is
still running
* [QTBUG-135264](https://bugreports.qt.io/browse/QTBUG-135264) Error in qml qmake project with qt 6.8.3
* [QTBUG-135225](https://bugreports.qt.io/browse/QTBUG-135225) qtbase build fails without process(environment) feature
* [QTBUG-135230](https://bugreports.qt.io/browse/QTBUG-135230) Configuring xmlstreamreader out of the build fails
* [QTBUG-135152](https://bugreports.qt.io/browse/QTBUG-135152) qtbase build fails if configured with -no-feature-
desktopservices
* [QTBUG-134634](https://bugreports.qt.io/browse/QTBUG-134634) tst_QUuid::uint128 fails on big-endian
* [QTBUG-135287](https://bugreports.qt.io/browse/QTBUG-135287) QDirIterator::next no longer returns "" upon iterator
exhaustion
* [QTBUG-130142](https://bugreports.qt.io/browse/QTBUG-130142) 6.8 Regresssion:  QDirIterator::next segfaults
* [QTBUG-135338](https://bugreports.qt.io/browse/QTBUG-135338) Sorting indicator size not honored in itemview header
with windows11 style
* [QTBUG-135135](https://bugreports.qt.io/browse/QTBUG-135135) QMySqlDriver QDateTime is not consistant between
read/write
* [QTBUG-134807](https://bugreports.qt.io/browse/QTBUG-134807) macos: Voice Over/Accessiblity for tabs is lacking
* [QTBUG-135397](https://bugreports.qt.io/browse/QTBUG-135397) Cannot configure Qt with "-no-widgets"
* [QTBUG-135076](https://bugreports.qt.io/browse/QTBUG-135076) [QNX] Stale QNX Screen events under load
* [QTBUG-135471](https://bugreports.qt.io/browse/QTBUG-135471) tst_QXmlStream does not test non-wellformed documents
properly
* [QTBUG-135285](https://bugreports.qt.io/browse/QTBUG-135285) QVariant::toInt() asserts if the contained real number
exceeds integer limits
* [QTBUG-135578](https://bugreports.qt.io/browse/QTBUG-135578) Possible QTimer ABI break between Qt 6.7 and Qt 6.9
* [QTBUG-134902](https://bugreports.qt.io/browse/QTBUG-134902) Regression: QByteArray/string/string_view comparison
broken
* [QTBUG-135609](https://bugreports.qt.io/browse/QTBUG-135609) Build failure when building iOS on macOS
* [QTBUG-135129](https://bugreports.qt.io/browse/QTBUG-135129) QXmlStreamReader::addData(QASV) overload unconditionally
converts UTF-16 and L1 to UTF-8
* [QTBUG-135433](https://bugreports.qt.io/browse/QTBUG-135433) QUrl::setPath and QUrl::fromUserInput encodes local
paths differently from QUrl::fromLocalFile
* [QTBUG-135340](https://bugreports.qt.io/browse/QTBUG-135340) Regression: Stylesheet breaks QGraphicsProxyWidget
* [QTBUG-128916](https://bugreports.qt.io/browse/QTBUG-128916) QComboBox drop down is not visible on Windows11 in some
situation
* [QTBUG-128329](https://bugreports.qt.io/browse/QTBUG-128329) qt combobox 放入到QGraphicsProxyWidget下拉框不显示
* [QTBUG-135620](https://bugreports.qt.io/browse/QTBUG-135620) Qt6WebEngineCoreDeploySupport fails when generating RPM
* [QTBUG-109553](https://bugreports.qt.io/browse/QTBUG-109553) CMake deployment API creates too deep directory
hierarchy when DESTDIR is set
* [QTBUG-134881](https://bugreports.qt.io/browse/QTBUG-134881) android_content_uri test crashes during test process.
* [QTBUG-135648](https://bugreports.qt.io/browse/QTBUG-135648) [REG 6.7->6.8] macOS: FindWrapResolv.cmake fails
check_cxx_source_compiles with strict flags (-Werror -Wzero-as-null-
pointer-constant)
* [QTBUG-135650](https://bugreports.qt.io/browse/QTBUG-135650) [6.9.0] Build error during bootstrap
* [QTBUG-133963](https://bugreports.qt.io/browse/QTBUG-133963) [REG Qt 6.5 -> 6.7] Shortcuts on macOs using
Meta/Command require Shift as well
* [QTBUG-135378](https://bugreports.qt.io/browse/QTBUG-135378) Use after delete of QWasmSuspendResumeControl
* [QTBUG-135442](https://bugreports.qt.io/browse/QTBUG-135442) QDockWidget/QMainWindow leak widgetItems from
QDockAreaLayoutItem on dragging and QDockWidget::close()
* [QTBUG-135628](https://bugreports.qt.io/browse/QTBUG-135628) QCheckbox without text is right cropped
* [QTBUG-117731](https://bugreports.qt.io/browse/QTBUG-117731) CMake deploy api and QtMultimedia backend
* [QTBUG-135640](https://bugreports.qt.io/browse/QTBUG-135640) Data race in QPointer
(QtSharedPointer::ExternalRefCountData::getAndRef)
* [QTBUG-135079](https://bugreports.qt.io/browse/QTBUG-135079) windeployqt missing plugins
* [QTBUG-134395](https://bugreports.qt.io/browse/QTBUG-134395) QTest documentation seems to be old
* [QTBUG-135866](https://bugreports.qt.io/browse/QTBUG-135866) [REG dev] qnumeric.h: qBound() not found
* [QTBUG-135619](https://bugreports.qt.io/browse/QTBUG-135619) QVariant::canConvert behaves inconsistently with the
documentation
* [QTBUG-135806](https://bugreports.qt.io/browse/QTBUG-135806) qtbase autotests to compile without draganddrop
* [QTBUG-133923](https://bugreports.qt.io/browse/QTBUG-133923) Missing documentation for QFlags' equality operators
* [QTBUG-135636](https://bugreports.qt.io/browse/QTBUG-135636) tst_QTimer::crossThreadSingleShotToFunctor() leaks
(almost) all timers
* [QTBUG-134139](https://bugreports.qt.io/browse/QTBUG-134139) Windows: Qt::Popup window has wrong initial size on
system with displays with different DPI scales
* [QTBUG-135044](https://bugreports.qt.io/browse/QTBUG-135044) tst_QStringApiSymmetry fails under ASAN
(GenerationalCollator is leaked?)
* [QTBUG-54484](https://bugreports.qt.io/browse/QTBUG-54484) QSortFilterProxyModel crash on filter item out
* [QTBUG-50821](https://bugreports.qt.io/browse/QTBUG-50821) QSortFilterProxyModel crash when dataChanged during
setFilter*
* [QTBUG-135294](https://bugreports.qt.io/browse/QTBUG-135294) Duplicate data tags in tst_qgraphicslinearlayout
* [QTBUG-134721](https://bugreports.qt.io/browse/QTBUG-134721) Double click on QMenu item, widget behind the popup
received doubleclick
* [QTBUG-135933](https://bugreports.qt.io/browse/QTBUG-135933) QMenus with a layout and widgets are no longer shown
* [QTBUG-129108](https://bugreports.qt.io/browse/QTBUG-129108) Menus and action visibility
* [QTBUG-135326](https://bugreports.qt.io/browse/QTBUG-135326) Linux: QLoggingCategory::setFilterRules() with enabled
CTF tracing causes a crash
* [QTBUG-120924](https://bugreports.qt.io/browse/QTBUG-120924) Initializing a QList with iterators of a std::range
leads to warnings
* [QTBUG-135597](https://bugreports.qt.io/browse/QTBUG-135597) QAbstractSlider is not using SliderOrientationChange
* [QTBUG-135854](https://bugreports.qt.io/browse/QTBUG-135854) Qt Keyboard Shortcut: Fullscreen incorrectly mapped in
GNOME
* [QTBUG-136019](https://bugreports.qt.io/browse/QTBUG-136019)  c1: fatal error C1083: Cannot open source file: 'C:\Use
rs\qt\work\qt\qt3d_build\src\plugins\renderers\opengl\debug\OpenGLRender
erPlugin_resource.rc': No such file or directory
* [QTBUG-131955](https://bugreports.qt.io/browse/QTBUG-131955) SVG Icons strentched in QListViewWidget items
* [QTBUG-135875](https://bugreports.qt.io/browse/QTBUG-135875) Allow configuring wasm without clipboard feature
* [QTBUG-135874](https://bugreports.qt.io/browse/QTBUG-135874) Allow configuring wasm without draganddrop feature
* [QTBUG-135890](https://bugreports.qt.io/browse/QTBUG-135890) Allow configuring Windows without clipboard feature
* [QTBUG-135893](https://bugreports.qt.io/browse/QTBUG-135893) Allow configuring Windows without highdpiscaling feature
* [QTBUG-135024](https://bugreports.qt.io/browse/QTBUG-135024) Wasm Accessibility: Fix wasm accessibility element id
* [QTBUG-136079](https://bugreports.qt.io/browse/QTBUG-136079) error: 'QPixmapCache' has not been declared
* [QTBUG-135949](https://bugreports.qt.io/browse/QTBUG-135949) tst_QWebSocket - tests are failing
* [QTBUG-136024](https://bugreports.qt.io/browse/QTBUG-136024) The oracle OCI SQl Plugin is unusable
* [QTBUG-11967](https://bugreports.qt.io/browse/QTBUG-11967) QDateEdit/CalendarPopup(true) has incorrect sizing
* [QTBUG-136042](https://bugreports.qt.io/browse/QTBUG-136042) Qt MySQL driver does not add milliseconds for QDateTime
in formatValue()
* [QTBUG-95071](https://bugreports.qt.io/browse/QTBUG-95071) mysql client version detection broken with MariaDB 10.6
* [QTBUG-134695](https://bugreports.qt.io/browse/QTBUG-134695) [REG] QPdfWriter: embed font issue: generates very big
pdf file on windows : the workaround doesn't work anymore
* [QTBUG-135950](https://bugreports.qt.io/browse/QTBUG-135950) Cocoa window: Updates are not received
* [QTBUG-135860](https://bugreports.qt.io/browse/QTBUG-135860) qt_add_qml_module(): Reject invalid inputs
* [QTBUG-125586](https://bugreports.qt.io/browse/QTBUG-125586) QVariantAnimation: currentValue should not change when
calling setStartValue() and setEndValue()
* [QTBUG-133841](https://bugreports.qt.io/browse/QTBUG-133841) 'Failed to initialize graphics backend for OpenGL'
causes the example apps to crash on launch
* [QTBUG-135617](https://bugreports.qt.io/browse/QTBUG-135617) Compile Android without permissions -feature
* [QTBUG-135693](https://bugreports.qt.io/browse/QTBUG-135693) Compile Android without accessibility -feature
* [QTBUG-135675](https://bugreports.qt.io/browse/QTBUG-135675) Compile Android without clipboard -feature
* [QTBUG-134259](https://bugreports.qt.io/browse/QTBUG-134259) Update SSL overview with link to export control
documentation
* [QTBUG-136039](https://bugreports.qt.io/browse/QTBUG-136039) CMake build fail with axcontainer and infinite loop
* [QTBUG-136136](https://bugreports.qt.io/browse/QTBUG-136136) TestNamespace: 'tst_QGenericItemModel': ambiguous symbol
* [QTBUG-136050](https://bugreports.qt.io/browse/QTBUG-136050) Input text appears next to Qt window
* [QTBUG-130278](https://bugreports.qt.io/browse/QTBUG-130278) [Reg 6.7.2 -> 6.8.0][macOS] QLocale::LongFormat no
longer produces reversible conversion between QDateTime and QString
* [QTBUG-136241](https://bugreports.qt.io/browse/QTBUG-136241) wasm: standardContextMenu is not shown
* [QTBUG-135201](https://bugreports.qt.io/browse/QTBUG-135201) tst_QHeaderView is full of signed overflow (UB)
* [QTBUG-136341](https://bugreports.qt.io/browse/QTBUG-136341) Build fails without style_windows & style_stylesheet
features
* [QTBUG-135867](https://bugreports.qt.io/browse/QTBUG-135867) [REG 6.9] Linux/XCB: Possible holes in transparent
windows on HiDPI
* [QTBUG-130474](https://bugreports.qt.io/browse/QTBUG-130474) QLineEdit/QCompleter popup shows in top-level window
* [QTBUG-136233](https://bugreports.qt.io/browse/QTBUG-136233) [Webassembly] Ghost input field disrupts surface
geometry
* [QTBUG-135934](https://bugreports.qt.io/browse/QTBUG-135934) Mac-style QMenu icons never show Disabled mode
* [QTBUG-136348](https://bugreports.qt.io/browse/QTBUG-136348) Problem with macdeployqt not passing CN correctly
* [QTBUG-135800](https://bugreports.qt.io/browse/QTBUG-135800) [REG 6.8 → 6.9] XMLHttpRequest() errors from
qt.network.http2 and rest api data are not displaying to Multimedia
* [QTBUG-135655](https://bugreports.qt.io/browse/QTBUG-135655) Make Android configurable without 'process' support
* [QTBUG-136362](https://bugreports.qt.io/browse/QTBUG-136362) [REG 6.8 -> 6.9] QTableView: Header sections' incorrect
painting
* [QTBUG-136477](https://bugreports.qt.io/browse/QTBUG-136477) Header scrolls to opposite direction
* [QTBUG-136609](https://bugreports.qt.io/browse/QTBUG-136609) Can't run appex with 6.8.3 or later
* [QTBUG-136083](https://bugreports.qt.io/browse/QTBUG-136083) qtypeinfo.h uses std::is_trivial_v which will be
deprecated in C++26
* [QTBUG-136693](https://bugreports.qt.io/browse/QTBUG-136693) tst_qfile fails on VxWorks 25.03
* [QTBUG-136210](https://bugreports.qt.io/browse/QTBUG-136210) Qt installer .pc files unusable due to spurious prefix
* [QTBUG-134110](https://bugreports.qt.io/browse/QTBUG-134110) wasm mkspec distclean deleting all *.html and *.js files
* [QTBUG-126515](https://bugreports.qt.io/browse/QTBUG-126515) Buttons are too small, focus rectangle only seen at the
rounded corners
* [QTBUG-129568](https://bugreports.qt.io/browse/QTBUG-129568) tst_QWidget_window::mouseMoveWithPopup() failed on
Ubuntu 24.04 GNOME X11
* [QTBUG-129029](https://bugreports.qt.io/browse/QTBUG-129029) tst_QComboBox:popupPositionAfterStyleChange() failed on
Ubuntu 24.04 GNOME X11
* [QTBUG-136453](https://bugreports.qt.io/browse/QTBUG-136453) QTableView auto-section-resize broken since Qt 6.9
* [QTBUG-136497](https://bugreports.qt.io/browse/QTBUG-136497) Android app fails to restart when permission is revoked
* [QTBUG-136077](https://bugreports.qt.io/browse/QTBUG-136077) [Regression 6.8.2->6.8.3] Android apps hang with black
screen or splash screen
* [QTBUG-135961](https://bugreports.qt.io/browse/QTBUG-135961) Blank screen when app is woken up from background
* [QTBUG-134419](https://bugreports.qt.io/browse/QTBUG-134419) systemCaCertificate() openssl backend walks current
working directory if system ca directory contains a broken symlink
* [QTBUG-136530](https://bugreports.qt.io/browse/QTBUG-136530) QFuture::isValid() without result
* [QTBUG-135978](https://bugreports.qt.io/browse/QTBUG-135978) Adding -ObjC linking flag breaks iOS build
* [QTBUG-135945](https://bugreports.qt.io/browse/QTBUG-135945) QLatin1StringView documentation assumes knowledge of
string literals namespace
* [QTBUG-136678](https://bugreports.qt.io/browse/QTBUG-136678) Hardcoded paths used in
qt_generate_deploy_qml_app_script
* [QTBUG-136485](https://bugreports.qt.io/browse/QTBUG-136485) QDockWidgets sends visibilityChanged on destruction
* [QTBUG-125223](https://bugreports.qt.io/browse/QTBUG-125223)  Plugin's install_rpath error during deployment by
qt_generate_deploy_qml_app_script.
* [QTBUG-136723](https://bugreports.qt.io/browse/QTBUG-136723) set_window_geometry may be called repeatedly
* [QTBUG-135856](https://bugreports.qt.io/browse/QTBUG-135856) qDebug() << (QGesture*)nullptr; segfaults
* [QTBUG-135341](https://bugreports.qt.io/browse/QTBUG-135341) text input v3: input method window is misplaced after
closing a popup
* [QTBUG-135977](https://bugreports.qt.io/browse/QTBUG-135977) [REG 6.8.2 -> 6.8.3] WASM: Loaded Roboto Flex font
rendered as italic by default
* [QTBUG-135315](https://bugreports.qt.io/browse/QTBUG-135315) Possible regression in handling of special style names
* [QTBUG-135921](https://bugreports.qt.io/browse/QTBUG-135921) text-input-v3 skips advertising capabilities
* [QTBUG-136549](https://bugreports.qt.io/browse/QTBUG-136549) Race condition and crash when HTTP error received while
QHttp2Stream is uploading
* [QTBUG-136812](https://bugreports.qt.io/browse/QTBUG-136812) Bug in http header handling on WASM
* [QTBUG-136962](https://bugreports.qt.io/browse/QTBUG-136962) qstdweb::Promise does not handle exceptions
* [QTBUG-136799](https://bugreports.qt.io/browse/QTBUG-136799) wasm: unicode alt code processing error when NumLock is
activated
* [QTBUG-120048](https://bugreports.qt.io/browse/QTBUG-120048) "Empty" file/line/function fields should be omitted from
systemd-journal logs
* [QTBUG-136968](https://bugreports.qt.io/browse/QTBUG-136968) qstring.h:1125:40: error: '= delete' with a message is a
C++2c extension
* [QTBUG-135861](https://bugreports.qt.io/browse/QTBUG-135861) QXmlStreamWriter continues writing data after an error
is raised
* [QTBUG-133332](https://bugreports.qt.io/browse/QTBUG-133332) possible stackoverflow calling setWindowFlag() in style
polish & unpolish
* [QTBUG-135789](https://bugreports.qt.io/browse/QTBUG-135789) Build failure on macOS
* [QTBUG-133746](https://bugreports.qt.io/browse/QTBUG-133746) QFileSystemModel with wrong path of top-directory of a
drive
* [QTBUG-136493](https://bugreports.qt.io/browse/QTBUG-136493) FFmpeg not properly configured with multi-abi builds
* [QTBUG-135481](https://bugreports.qt.io/browse/QTBUG-135481) Android TV system keyboard doesn't process input
correctly
* [QTBUG-135283](https://bugreports.qt.io/browse/QTBUG-135283) SafeArea margins not populated
* [QTBUG-135227](https://bugreports.qt.io/browse/QTBUG-135227) QML SafeArea type only works if full screen is entered
first
* [QTBUG-135808](https://bugreports.qt.io/browse/QTBUG-135808) Some problems with Expanded Client Areas on Android
* [QTBUG-137104](https://bugreports.qt.io/browse/QTBUG-137104) Error: no member named 'qt_noop' in namespace
'TestNamespace'
* [QTBUG-137130](https://bugreports.qt.io/browse/QTBUG-137130) Qt Creator crash on exit accessing destroyed event
dispatcher
* [QTBUG-135722](https://bugreports.qt.io/browse/QTBUG-135722) Compile Android without desktopservices -feature
* [QTBUG-131699](https://bugreports.qt.io/browse/QTBUG-131699) QDialog with modal=false will be invisible or hidden
behind its parent when click other widgets
* [QTBUG-135376](https://bugreports.qt.io/browse/QTBUG-135376) Fullscreen virtual keyboard key handling
* [QTBUG-128745](https://bugreports.qt.io/browse/QTBUG-128745) [QuickControls] Text inputs displayed as extracted view
in landscape orientation
* [QTBUG-130058](https://bugreports.qt.io/browse/QTBUG-130058) Android Virtual keyboard is broken in landscape mode
* [QTBUG-137168](https://bugreports.qt.io/browse/QTBUG-137168) QtMultimedia fails to install: Cannot find
'plugins/multimedia/libmockmultimediaplugin.a' to compute its checksum
* [QTBUG-135938](https://bugreports.qt.io/browse/QTBUG-135938) Wayland: ToolTip resets the mouse cursor shape
* [QTBUG-137021](https://bugreports.qt.io/browse/QTBUG-137021) make QWindow::requestActivate() working in auto tests on
Wayland
* [QTBUG-136710](https://bugreports.qt.io/browse/QTBUG-136710) QML Image object causes a crash when it gets deleted
while it's still loading
* [QTBUG-137144](https://bugreports.qt.io/browse/QTBUG-137144) a11y: AT-SPI "Locale" Accessible property not supported
* [QTBUG-111993](https://bugreports.qt.io/browse/QTBUG-111993) QNetworkAccessManager docs: minor typo referencing non-
existent method
* [QTBUG-135489](https://bugreports.qt.io/browse/QTBUG-135489) [REG 6.8.2->6.8.3] Handling of custom scheme URL is
broken
* [QTBUG-137038](https://bugreports.qt.io/browse/QTBUG-137038) QByteArray::toDouble() behavior changed on whitespaces
only string
* [QTBUG-134921](https://bugreports.qt.io/browse/QTBUG-134921) Comparision of QVariantList and QProperty<QVariantList>
not working
* [QTBUG-131714](https://bugreports.qt.io/browse/QTBUG-131714) [Windows] Finishing system move activates the window
even if Qt.WindowDoesNotAcceptFocus is set
* [QTBUG-137201](https://bugreports.qt.io/browse/QTBUG-137201) tst_QScroller::overshoot() is flaky on Windows
* [QTBUG-110758](https://bugreports.qt.io/browse/QTBUG-110758) Qt6/wayland QNativeInterface doesn't succeed in wrapping
existing EGL context
* [QTBUG-135817](https://bugreports.qt.io/browse/QTBUG-135817) [REG 6.7.2 -> Qt 6.8.2] Windows:
QFontDatabase::families() does not list stylistic variants of families
* [QTBUG-137277](https://bugreports.qt.io/browse/QTBUG-137277) Stack overflow in QFontEngine (due to infinite
recursion)
* [QTBUG-131655](https://bugreports.qt.io/browse/QTBUG-131655) Memory leak in QNSViewMenuHelper
* [QTBUG-137161](https://bugreports.qt.io/browse/QTBUG-137161) "Leaks" utility in the Instruments app report memory
leak.
* [QTBUG-137316](https://bugreports.qt.io/browse/QTBUG-137316) generateJavaQmlComponents will scan relevant import
directories twice
* [QTBUG-136967](https://bugreports.qt.io/browse/QTBUG-136967) qjniarray.h:775:46: error: a template argument list is
expected
* [QTBUG-137297](https://bugreports.qt.io/browse/QTBUG-137297) qmake iOS target: fails to find (prebuilt) .prl
dependencies -> Xcode build fails
* [QTBUG-137108](https://bugreports.qt.io/browse/QTBUG-137108) CE_ComboBoxLabel painting not called anymore on
QProxyStyle, due to QStyleSheetStyle
* [QTBUG-131761](https://bugreports.qt.io/browse/QTBUG-131761) Incorrect display of :selected state of QCombobox on
"windows" style plugin
* [QTBUG-135634](https://bugreports.qt.io/browse/QTBUG-135634) macOS: Deleted menu is not removed from native menu bar
* [QTBUG-137398](https://bugreports.qt.io/browse/QTBUG-137398) A crash occurred in C:\Users\qt\work\qt\qtdeclarative_st
andalone_tests\tests\auto\quickdialogs\qquickfontdialogimpl\tst_qquickfo
ntdialogimpl.exe
* [QTBUG-136550](https://bugreports.qt.io/browse/QTBUG-136550) QMYSQL: QT application built with libmariadb3.4 won't
connect to MariaDB 10
* [QTBUG-137198](https://bugreports.qt.io/browse/QTBUG-137198) Configure fails with -DFEATURE_sanitize_thread=ON
-DFEATURE_sanitize_address=ON without a proper message
* [QTBUG-133687](https://bugreports.qt.io/browse/QTBUG-133687) Confusing instructions when atomicfptr config.test fails
* [QTBUG-135652](https://bugreports.qt.io/browse/QTBUG-135652) Using QIcon from png and svg file in a toolbar with
&gt;100% scaler ratio causes wrong icon size to be picked elsewhere
* [QTBUG-136229](https://bugreports.qt.io/browse/QTBUG-136229) Fullscreen virtual keyboard: issue with selection and
delete
* [QTBUG-136074](https://bugreports.qt.io/browse/QTBUG-136074) QTreeView a11y: Frequent Qt Creator crashes when Orca
screen reader is active
* [QTBUG-133855](https://bugreports.qt.io/browse/QTBUG-133855)  QtreeView sporadic crash when setCurrentIndex is called
* [QTBUG-136960](https://bugreports.qt.io/browse/QTBUG-136960) Checkbox in QTreeview shows black outline in dark mode
* [QTBUG-137249](https://bugreports.qt.io/browse/QTBUG-137249) QML Screen.orientation on iOS does not provide all
directions
* [QTBUG-136590](https://bugreports.qt.io/browse/QTBUG-136590) Regression in QTextTable: border-collapse cell border
rendering broken
* [QTBUG-133904](https://bugreports.qt.io/browse/QTBUG-133904) Corrupted qml rendering on some Android PowerVR devices
after the app is killed
* [QTBUG-134245](https://bugreports.qt.io/browse/QTBUG-134245) [Reg 6.8.0 -> 6.8.2] Strange 4-quadrant colouration of
Qt Quick items
* [QTBUG-134089](https://bugreports.qt.io/browse/QTBUG-134089) Power VR rendering failure on Qt 6.8.2
* [QTBUG-135411](https://bugreports.qt.io/browse/QTBUG-135411) Android visual Glitches on 6.8.2+
* [QTBUG-134496](https://bugreports.qt.io/browse/QTBUG-134496) Drawing errors on some Android devices
* [QTBUG-135810](https://bugreports.qt.io/browse/QTBUG-135810) [REG 6.8.1 -> 6.8.3] Crashes in QRhi::endFrame /
glDrawElements on Android
* [QTBUG-134143](https://bugreports.qt.io/browse/QTBUG-134143) QColorDialog: Unable to pick color after switching
windows using  Windows Task View
* [QTBUG-137011](https://bugreports.qt.io/browse/QTBUG-137011) The icon of the QCommandLinkButton does not update when
the button's visibility is set to true.
* [QTBUG-136450](https://bugreports.qt.io/browse/QTBUG-136450) Top flaky test: tst_xdgshell::showMinimized
* [QTBUG-137329](https://bugreports.qt.io/browse/QTBUG-137329) QFileDialog::getOpenFileContent opens a non-modal dialog
* [QTBUG-128494](https://bugreports.qt.io/browse/QTBUG-128494) [Android] Accessible.description
* [QTBUG-137427](https://bugreports.qt.io/browse/QTBUG-137427) HTTP 2 request cancellation timing issue may lead to
severed connection
* [QTBUG-115293](https://bugreports.qt.io/browse/QTBUG-115293) tst_QGraphicsItem::itemUsesExtendedStyleOption() with
QtWayland failed on Ubuntu 22.04, GNOME
* [QTBUG-135844](https://bugreports.qt.io/browse/QTBUG-135844) Windows: QPainter errors when maximizing/resizing window
* [QTBUG-137041](https://bugreports.qt.io/browse/QTBUG-137041) Schannel plugin incorrectly verifies the
NetscapeCertType extension
* [QTBUG-126743](https://bugreports.qt.io/browse/QTBUG-126743) If QT_ANDROID_PACKAGE_SOURCE_DIR is set to a specific
path, a build folder is recursively created within the build folder.
* [QTBUG-137346](https://bugreports.qt.io/browse/QTBUG-137346) [Reg 6.8.0->6.8.1]QTableView ignores the stylesheet
background color when hovering over the items.
* [QTBUG-133656](https://bugreports.qt.io/browse/QTBUG-133656) During Transition from DST back to standard time. the
local clock time repeats an hour.
* [QTBUG-137556](https://bugreports.qt.io/browse/QTBUG-137556) [FTBFS] QtCore doc snippets link to QtWidgets
* [QTBUG-135643](https://bugreports.qt.io/browse/QTBUG-135643) Window glitches when using Qt::ExpandedClientAreaHint
* [QTBUG-133943](https://bugreports.qt.io/browse/QTBUG-133943) Qt::ExpandedClientAreaHint results in different rounded
window corners on Windows
* [QTBUG-133946](https://bugreports.qt.io/browse/QTBUG-133946) Qt::ExpandedClientAreaHint breaks minimizing on Windows
* [QTBUG-113401](https://bugreports.qt.io/browse/QTBUG-113401) QtConcurrent::run parameter order documentation wrong
* [QTBUG-137157](https://bugreports.qt.io/browse/QTBUG-137157) [macOS] QAccessibleInterface::window() is never called;
accessibility tools cannot see the top-level window that holds a
widget/Item
* [QTBUG-25938](https://bugreports.qt.io/browse/QTBUG-25938) Checkable QGroupBox doesn't keep "enabled" status of
children
* [QTBUG-136055](https://bugreports.qt.io/browse/QTBUG-136055) QWebSocketServer creates persistent files in
Microsoft/Crypto/RSA on each new client connection.
* [QTBUG-137027](https://bugreports.qt.io/browse/QTBUG-137027) GetMethodID received NULL jclass
* [QTBUG-136097](https://bugreports.qt.io/browse/QTBUG-136097) Can't use the properties and signals when definitions
such as them are enabled by `__has_include`
* [QTBUG-135337](https://bugreports.qt.io/browse/QTBUG-135337) crash when connecting with RDP
* [QTBUG-133221](https://bugreports.qt.io/browse/QTBUG-133221) [REG: 6.7->6.8] SVG file mime type not recognized if the
file contains xml header
* [QTBUG-136990](https://bugreports.qt.io/browse/QTBUG-136990) QML property information rendered mangled (Assistant, Qt
Creator)
* [QTBUG-137452](https://bugreports.qt.io/browse/QTBUG-137452) compile error in moc-generated code if slot/property
name equals return type name
* [QTBUG-137467](https://bugreports.qt.io/browse/QTBUG-137467) qt.qpa.wayland: wrong transient parent of the popup
* [QTBUG-136176](https://bugreports.qt.io/browse/QTBUG-136176) [Reg 6.8.3 -> 6.9.0]QIcon::ThemeIcon::DialogInformation
is missing pixels.
* [QTBUG-134604](https://bugreports.qt.io/browse/QTBUG-134604) edit-redo icon is clipped on Windows
* [QTBUG-109599](https://bugreports.qt.io/browse/QTBUG-109599) Password characters are not visible with a screenreader
* [QTBUG-137579](https://bugreports.qt.io/browse/QTBUG-137579) QDebugStateSaver not documented well
* [QTBUG-137755](https://bugreports.qt.io/browse/QTBUG-137755) Regression: Segfault on closing a program using
QDockWidgets, introduced by ab6f1ad77852a427ae73172ca11dacf876a0cbf7
* [QTBUG-137814](https://bugreports.qt.io/browse/QTBUG-137814) Build broken with -no-feature-sharedmemory
* [QTBUG-137850](https://bugreports.qt.io/browse/QTBUG-137850) moc_qwaylandxdgshell.cpp:625:60: error: template
argument 1 is invalid
* [QTBUG-137822](https://bugreports.qt.io/browse/QTBUG-137822) Qcocoa build is broken
* [QTBUG-96379](https://bugreports.qt.io/browse/QTBUG-96379) Missing documentation for QMetaContainer
* [QTBUG-134896](https://bugreports.qt.io/browse/QTBUG-134896) QUrl's qHash() is inconsistent with its operator==
* [QTBUG-134900](https://bugreports.qt.io/browse/QTBUG-134900) QUrl's operator==() is taking bygone data into account
* [QTBUG-86287](https://bugreports.qt.io/browse/QTBUG-86287) Static 5.15.0 compile results in "undefined reference to
xcb_aux_create_gc"
* [QTBUG-137004](https://bugreports.qt.io/browse/QTBUG-137004) xcb-image is missing dependency on xcb-aux
* [QTBUG-137763](https://bugreports.qt.io/browse/QTBUG-137763) windeployqt crash when run through cmake
* [QTBUG-137739](https://bugreports.qt.io/browse/QTBUG-137739) [REG 6.9.1-6.10.0 beta1] opengl/cube not launching on
Wayland
* [QTBUG-87180](https://bugreports.qt.io/browse/QTBUG-87180) Typo in the description of QGraphicsSimpleTextItem class
* [QTBUG-137870](https://bugreports.qt.io/browse/QTBUG-137870) cmake: qt can only be built once
* [QTBUG-120031](https://bugreports.qt.io/browse/QTBUG-120031) xcb: Modal state may get lost due to a race
* [QTBUG-133029](https://bugreports.qt.io/browse/QTBUG-133029) Documentation is inconsistent wrt QChronoTimer
* [QTBUG-123063](https://bugreports.qt.io/browse/QTBUG-123063) XCB flakiness in tst_qgraphicsscene (race condition
caused by the event dispatcher on Linux)
* [QTBUG-137838](https://bugreports.qt.io/browse/QTBUG-137838) QMultiHash has undocumented erase method
* [QTBUG-130978](https://bugreports.qt.io/browse/QTBUG-130978) Auto-scrolling breaks when dragging and dropping an item
in QTreeView.
* [QTBUG-137700](https://bugreports.qt.io/browse/QTBUG-137700) QIcon::pixmap selects wrong icon file from theme
* [QTBUG-90634](https://bugreports.qt.io/browse/QTBUG-90634) QIcon not preferring Hi DPI pixmaps when scaling
* [QTBUG-127705](https://bugreports.qt.io/browse/QTBUG-127705) Android splashscreen not removed
* [QTBUG-124140](https://bugreports.qt.io/browse/QTBUG-124140) [REG]: 6.7.0  full-screen app displays background window
(or splash-screen) graphics at top/bottom during multiwindow split
display
* [QTBUG-137727](https://bugreports.qt.io/browse/QTBUG-137727) Crash in zwp_text_input_v3_set_surrounding_text when
selecting large text
* [QTBUG-136130](https://bugreports.qt.io/browse/QTBUG-136130) background color of QTreeViewItems with windows 11 style
* [QTBUG-137882](https://bugreports.qt.io/browse/QTBUG-137882) top-level build, examples don't respect -linker
configure option
* [QTBUG-136009](https://bugreports.qt.io/browse/QTBUG-136009) Wayland: QGuiApplication::setOverrideCursor doesn't work
when app is freezed
* [QTBUG-137986](https://bugreports.qt.io/browse/QTBUG-137986) rhi/vulkan: Do something about VUID-vkQueueSubmit-
pSignalSemaphores-00067
* [QTBUG-138043](https://bugreports.qt.io/browse/QTBUG-138043) QMultiMap documentation error
* [QTBUG-133631](https://bugreports.qt.io/browse/QTBUG-133631) wasm: TextField with echo mode password should not try
to autocomplete
* [QTBUG-134795](https://bugreports.qt.io/browse/QTBUG-134795) Add note about HAVE_TICK_COUNTER dependency
* [QTBUG-130765](https://bugreports.qt.io/browse/QTBUG-130765) Fix excessive use of note sections in QDateTime
documentation
* [QTBUG-113759](https://bugreports.qt.io/browse/QTBUG-113759) Sort alphabetically the list items on
https://doc.qt.io/qt-6/stylesheet-reference.html
* [QTBUG-137702](https://bugreports.qt.io/browse/QTBUG-137702) [REG Qt 6.9.0 -> 6.9.1] Crash when completing code
* [QTBUG-137587](https://bugreports.qt.io/browse/QTBUG-137587) qtdeclarative: do_compile failed when building with high
parallelism.
* [QTBUG-78013](https://bugreports.qt.io/browse/QTBUG-78013) QIdentityProxyModel::match inappropriately mixes use of
proxy model index and source model data method
* [QTBUG-126054](https://bugreports.qt.io/browse/QTBUG-126054) QString::arg(wchar_t{}) prefers the integral overload
instead of the QChar one
* [QTBUG-102240](https://bugreports.qt.io/browse/QTBUG-102240) QStringList incorrect inheritance documentation
* [QTBUG-125319](https://bugreports.qt.io/browse/QTBUG-125319) Scaling issue occurs when the window is moved due to
disconnecting the screen.
* [QTBUG-49564](https://bugreports.qt.io/browse/QTBUG-49564) QTextCharFormat fontPointSize() doesnt not return the
same as QTextCharFormat font().pointSize()
* [QTBUG-136217](https://bugreports.qt.io/browse/QTBUG-136217) Windows11 style does not show underlying content of
index widget.
* [QTBUG-119501](https://bugreports.qt.io/browse/QTBUG-119501) Numbers colliding and not highlighted in Charts with
Widgets Gallery example
* [QTBUG-95325](https://bugreports.qt.io/browse/QTBUG-95325) Removal of QTextStream::setCodec is not documented
* [QTBUG-138049](https://bugreports.qt.io/browse/QTBUG-138049) QScrollBar::createStandardContextMenu does not set QMenu
parent vs. QLineEdit, QPlainTextEdit, QTextEdit
* [QTBUG-138172](https://bugreports.qt.io/browse/QTBUG-138172) a11y: QToolButton menu not exposed on a11y layer when it
comes from default action
* [QTBUG-137344](https://bugreports.qt.io/browse/QTBUG-137344) a11y AT-SPI: org.freedesktop.DBus.Properties "GetAll"
queries trigger application crash
* [QTBUG-137806](https://bugreports.qt.io/browse/QTBUG-137806) [Android][A11y] Role of UI elements is missing
* [QTBUG-138201](https://bugreports.qt.io/browse/QTBUG-138201) Arranging QDockWidgets programatically causes
segmentation faults
* [QTBUG-138196](https://bugreports.qt.io/browse/QTBUG-138196) [REG dev] Fusion: Buttons and comboboxes outlined
* [QTBUG-59186](https://bugreports.qt.io/browse/QTBUG-59186) Error in QIODevice::readLine() documentation about
handling newline char
* [QTBUG-137438](https://bugreports.qt.io/browse/QTBUG-137438) [REG 6.9.0 -> 6.9.1] QTemporaryFile
* [QTBUG-112692](https://bugreports.qt.io/browse/QTBUG-112692) QPropertyNotifier and related APIs have no \since
version
* [QTBUG-88466](https://bugreports.qt.io/browse/QTBUG-88466) Thread safety of QTranslator::translate
* [QTBUG-138130](https://bugreports.qt.io/browse/QTBUG-138130) QTableView misrendered since qt 6.9
* [QTBUG-138158](https://bugreports.qt.io/browse/QTBUG-138158) QT_DISCARD_FILE_CONTENTS does not work as expected
* [QTBUG-138226](https://bugreports.qt.io/browse/QTBUG-138226) QTranslator deadlocks trying to translate translation
file loading error
* [QTBUG-137179](https://bugreports.qt.io/browse/QTBUG-137179) Crash in QTranslatorPrivate::do_translate (QQmlThread)
after QTranslator::load (main thread)
* [QTBUG-137776](https://bugreports.qt.io/browse/QTBUG-137776) Windows11 style, QTableView cell selection behavior
* [QTBUG-117414](https://bugreports.qt.io/browse/QTBUG-117414) Doc: Give hints how to get a QScreen object
* [QTBUG-132590](https://bugreports.qt.io/browse/QTBUG-132590) Unclear relation between
QTemporaryFile::{autoRemove,rename}()
* [QTBUG-128794](https://bugreports.qt.io/browse/QTBUG-128794) QLineEdit in Android - no text visual
* [QTBUG-133549](https://bugreports.qt.io/browse/QTBUG-133549) Qt UI stops redrawing on Android
* [QTBUG-128457](https://bugreports.qt.io/browse/QTBUG-128457) QSpinBox does not respond correctly to Android keyboard
* [QTBUG-128422](https://bugreports.qt.io/browse/QTBUG-128422) [Android] Can't change selection in QComboBox with touch
input
* [QTBUG-121757](https://bugreports.qt.io/browse/QTBUG-121757) Entered text is invisible in QLineEdit until field focus
is changed
* [QTBUG-138261](https://bugreports.qt.io/browse/QTBUG-138261) QPlatformBackingStore doesn't handle QtGui-level
fractional scaling
* [QTBUG-137120](https://bugreports.qt.io/browse/QTBUG-137120) [Regression] Right and top dockwidget area are not
resizable anymore
* [QTBUG-60355](https://bugreports.qt.io/browse/QTBUG-60355) QMetaEnum docs have no code examples
* [QTBUG-136138](https://bugreports.qt.io/browse/QTBUG-136138) Blank screen in CarPlay Simulator with Qt-based iOS app
due to assertion: "[scene isKindOfClass:UIWindowScene.class]" in
qiosapplicationdelegate.mm
* [QTBUG-137978](https://bugreports.qt.io/browse/QTBUG-137978) Qt.inputMethod.visible changes to true in orientation
change on iOS26 beta
* [QTBUG-85428](https://bugreports.qt.io/browse/QTBUG-85428) Documentation for QScrollBar can be improved
* [QTBUG-33977](https://bugreports.qt.io/browse/QTBUG-33977) Suggested change to QCoreApplication documentation
* [QTBUG-137393](https://bugreports.qt.io/browse/QTBUG-137393) No drag cursor when dragging under wayland
* [QTBUG-138032](https://bugreports.qt.io/browse/QTBUG-138032) calqlatr: Example prints 'stale focus object [...],
doing manual update' warnings
* [QTBUG-138256](https://bugreports.qt.io/browse/QTBUG-138256) QPlatformInputContext::update() called with stale focus
object
* [QTBUG-138183](https://bugreports.qt.io/browse/QTBUG-138183) The drop area for QToolBar gets triggered even when the
toolbar is not on the window.
* [QTBUG-106709](https://bugreports.qt.io/browse/QTBUG-106709) Application looks too small on an external display with
iPadOS 16.1 on M1 iPad
* [QTBUG-137544](https://bugreports.qt.io/browse/QTBUG-137544) QML iPad app window stays black when launched on
external display
* [QTBUG-138230](https://bugreports.qt.io/browse/QTBUG-138230) QCheckBox used as editor in delegate does not display
checkmark when using Windows11 style and no text
* [QTBUG-135213](https://bugreports.qt.io/browse/QTBUG-135213) QTreeView creates ghost artifacts when scrolling
* [QTBUG-120254](https://bugreports.qt.io/browse/QTBUG-120254) Cell value leaking into other cells when entering new
value
* [QTBUG-133845](https://bugreports.qt.io/browse/QTBUG-133845)  QSpinBoxes take too much vertical space if an
application-wide style sheet is set since Qt 6.8.2
* [QTBUG-134740](https://bugreports.qt.io/browse/QTBUG-134740) [REG 6.7.3 -> 6.8.0] QDir::entryInfoList slower
accessing SMB share from macOS
* [QTBUG-138374](https://bugreports.qt.io/browse/QTBUG-138374) QFileSystemWatcher::addPath() is slow on macos
* [QTBUG-138428](https://bugreports.qt.io/browse/QTBUG-138428) tst_QTextStream::pos3LargeFile() takes an extraordinary
amount of time to execute
* [QTBUG-138435](https://bugreports.qt.io/browse/QTBUG-138435) QTextStream::pos() seems to be linear over QFile size
(or QFile::pos())
* [QTBUG-138238](https://bugreports.qt.io/browse/QTBUG-138238) NPE when calling QtNetwork.unregisterReceiver() at exit
* [QTBUG-135928](https://bugreports.qt.io/browse/QTBUG-135928) Connection to D-Bus signals silently breaks if D-Bus was
used before creating QCoreApplication
* [QTBUG-138401](https://bugreports.qt.io/browse/QTBUG-138401) [REG dev] Windows11 Style: Check-boxes' drawing
regression
* [QTBUG-138094](https://bugreports.qt.io/browse/QTBUG-138094) Radiobuttons/Checkboxes in windows11 style do not follow
WinUI3 style
* [QTBUG-138484](https://bugreports.qt.io/browse/QTBUG-138484) QTextStream assumes single-character
QLocale::{positive,negative}Sign()
* [QTBUG-125366](https://bugreports.qt.io/browse/QTBUG-125366) Selectable QLabel does not copy to clipboard as
QLineEdit does
* [QTBUG-138206](https://bugreports.qt.io/browse/QTBUG-138206) a11y: Docked QDockWidget reports incorrect role and
window-relative position via AT-SPI
* [QTBUG-138168](https://bugreports.qt.io/browse/QTBUG-138168) Fix a typo in the licenseRule.json file in qtbase
* [QTBUG-137519](https://bugreports.qt.io/browse/QTBUG-137519) Memory corruption for tst_qsettings with JSPI
* [QTBUG-138008](https://bugreports.qt.io/browse/QTBUG-138008) Permissions test app crashes on emulator.
* [QTBUG-138372](https://bugreports.qt.io/browse/QTBUG-138372) QLocalSocket never emits ConnectedState in Linux
* [QTBUG-138566](https://bugreports.qt.io/browse/QTBUG-138566) QLocale::codeToScript() can't find QLocale::LastScript
* [QTBUG-138585](https://bugreports.qt.io/browse/QTBUG-138585) tst_qxmlstream failed on webOS building
* [QTBUG-138565](https://bugreports.qt.io/browse/QTBUG-138565) "Cannot generate qmltypes file" when trying to run in-
app purchase demo app on Android
* [QTBUG-134757](https://bugreports.qt.io/browse/QTBUG-134757) [REG 6.7.3->6.8.0] QWidgetAction: No contextMenuEvent
* [QTBUG-136163](https://bugreports.qt.io/browse/QTBUG-136163) sbom/spdx file not reproducible (contains build path)
* [QTBUG-138603](https://bugreports.qt.io/browse/QTBUG-138603) [Reg 6.9.1 -> 6.10.0b2][CMake] Most private modules are
no longer accessible
* [QTBUG-138660](https://bugreports.qt.io/browse/QTBUG-138660) QHttp2Stream: dtor missing sendRST_STREAM for some
state(s)
* [QTBUG-138156](https://bugreports.qt.io/browse/QTBUG-138156) tst_QHttpServer::disconnectedInEventLoop leaves a bad
state making multipleRequests fail
* [QTBUG-123585](https://bugreports.qt.io/browse/QTBUG-123585) Memory Leak: QGestureRecognizer::unregisterRecognizer()
* [QTBUG-138013](https://bugreports.qt.io/browse/QTBUG-138013) Content_uri test fails on Pixel6a Device
* [QTBUG-126531](https://bugreports.qt.io/browse/QTBUG-126531) Manual test android_content_uri fails
* [QTBUG-123319](https://bugreports.qt.io/browse/QTBUG-123319) android_content_uri test crashes when trying to get size
of nonexistent file.
* [QTBUG-134912](https://bugreports.qt.io/browse/QTBUG-134912) Manual test android_content_uri crash on exit
* [QTBUG-110240](https://bugreports.qt.io/browse/QTBUG-110240) "Use qtbase/tests/manual/android_content_uri" is not
found on the installation
* [QTBUG-132403](https://bugreports.qt.io/browse/QTBUG-132403) manual test android_content_uri fails.
* [QTBUG-129324](https://bugreports.qt.io/browse/QTBUG-129324) Don't print exceptions for content file operations that
are supposed to be done under the hood
* [QTBUG-138157](https://bugreports.qt.io/browse/QTBUG-138157) QWindow::safeAreaMargins() returns incorrect values when
virtual keyboard opens on Android (Qt 6.9)
* [QTBUG-131448](https://bugreports.qt.io/browse/QTBUG-131448) Cannot QMovie::moveToThread
* [QTBUG-131513](https://bugreports.qt.io/browse/QTBUG-131513) [iOS] QSysInfo::productVersion() incomplete?
* [QTBUG-129027](https://bugreports.qt.io/browse/QTBUG-129027) tst_QStatusBar::QTBUG4334_hiddenOnMaximizedWindow()
failed on Ubuntu 24.04 GNOME X11
* [QTBUG-135954](https://bugreports.qt.io/browse/QTBUG-135954) [REG] Wayland: Over 2x higher painting CPU usage when
display scaling is used
* [QTBUG-138642](https://bugreports.qt.io/browse/QTBUG-138642) ODBC possible data loss with 'real' column
* [QTBUG-8963](https://bugreports.qt.io/browse/QTBUG-8963) Driver for ODBC - qsql_odbc.cpp should use the
QMetaType:float when sql type is SQL_FLOAT instead of QVariant::Double
* [QTBUG-68865](https://bugreports.qt.io/browse/QTBUG-68865) tst_QMenuBar::check_menuPosition autotest fails on Ubuntu
18.04
* [QTBUG-136629](https://bugreports.qt.io/browse/QTBUG-136629) QUnifiedTimer::updateAnimationTimers() crashes when
QApplication is recreated
* [QTBUG-138864](https://bugreports.qt.io/browse/QTBUG-138864) qt-android-runner.py doesn't find package name
* [QTBUG-135641](https://bugreports.qt.io/browse/QTBUG-135641) QNetworkDiskCache leaks file descriptors
* [QTBUG-135964](https://bugreports.qt.io/browse/QTBUG-135964) Windows theme uses wrong colors if high-contrast mode is
activated
* [QTBUG-138474](https://bugreports.qt.io/browse/QTBUG-138474) windeployqt: Warning: module icuuc could not be found
* [QTBUG-138056](https://bugreports.qt.io/browse/QTBUG-138056) QSortFilterProxyModel: Crash when changing sourceModel
(QPropertyBindingData / QBindingStorage)
* [QTBUG-138488](https://bugreports.qt.io/browse/QTBUG-138488) [iOS] URL handler do not receive data from external apps
via Universal Link
* [QTBUG-138894](https://bugreports.qt.io/browse/QTBUG-138894) Android fails to start without accessibility
* [QTBUG-138904](https://bugreports.qt.io/browse/QTBUG-138904) QIBASE driver fails to build when linking against
Firebird v2.5
* [QTBUG-138861](https://bugreports.qt.io/browse/QTBUG-138861) `QRhiResourceUpdateBatch` leaks memory if submitted via
`beginOffscreenFrame`
* [QTBUG-138250](https://bugreports.qt.io/browse/QTBUG-138250) Win11 23h2 ARM: QtBase -
tst_QRhi::storageBufferRuntimeSizeGraphics(OpenGL) 'pipeline->create()'
returned FALSE
* [QTBUG-93182](https://bugreports.qt.io/browse/QTBUG-93182) Occasional asserts when touch scroll NSEventPhaseEnded is
processed while event in queue indicates momentumPhase has begun
* [QTBUG-138542](https://bugreports.qt.io/browse/QTBUG-138542) [Wayland] Cursor changes to resize arrows in the area of
the app window
* [QTBUG-124011](https://bugreports.qt.io/browse/QTBUG-124011) Android: QFileInfo::isWritable() returns false
erroneously and throws an exception
* [QTBUG-115143](https://bugreports.qt.io/browse/QTBUG-115143) Unable to open files under certain conditions on
Android.
* [QTBUG-114979](https://bugreports.qt.io/browse/QTBUG-114979) Two issues using content scheme to work with files
* [QTBUG-138922](https://bugreports.qt.io/browse/QTBUG-138922) Consistent Qt caused crash when navigating with Jetpack
Compose
* [QTBUG-138580](https://bugreports.qt.io/browse/QTBUG-138580) [REG 6.10.0 beta1 -> beta2] CMake test including all
modules fails
* [QTBUG-139250](https://bugreports.qt.io/browse/QTBUG-139250) Top-level tool window doesnt oppen
* [QTBUG-93371](https://bugreports.qt.io/browse/QTBUG-93371) arabic text shapes incorrectly when using accelerator
* [QTBUG-139119](https://bugreports.qt.io/browse/QTBUG-139119) QFuture::takeResult asserts
* [QTBUG-139286](https://bugreports.qt.io/browse/QTBUG-139286) Make Platform Notes section optional in app-examples-
template
* [QTBUG-139051](https://bugreports.qt.io/browse/QTBUG-139051) Background color of QPlainTextEdit without border
cannont be set on Win11
* [QTBUG-139106](https://bugreports.qt.io/browse/QTBUG-139106) REG: Variable fonts no longer works with Freetype
backend
* [QTBUG-108329](https://bugreports.qt.io/browse/QTBUG-108329) tst_qfiledialog::completer() fails
* [QTBUG-101194](https://bugreports.qt.io/browse/QTBUG-101194) tst_QFileDialog has failing tests for Android
* [QTBUG-138982](https://bugreports.qt.io/browse/QTBUG-138982) qt-android-runner.py fails to start application
* [QTBUG-138622](https://bugreports.qt.io/browse/QTBUG-138622) Android launch wrapper script can conflict with qml
subdirectory name on case insensitive file systems
* [QTBUG-139211](https://bugreports.qt.io/browse/QTBUG-139211) tst_qquickpopup (Failed)
* [QTBUG-100991](https://bugreports.qt.io/browse/QTBUG-100991) Some tests crash on Android CI
* [QTBUG-131695](https://bugreports.qt.io/browse/QTBUG-131695) tst_qquickpopup tst_QQuickPopup::fadeDimmer is flaky
* [QTBUG-125083](https://bugreports.qt.io/browse/QTBUG-125083) [Android] ANRs related to QtNativeInputConnection
* [QTBUG-132695](https://bugreports.qt.io/browse/QTBUG-132695) Crash in QGuiApplication::applicationStateChanged() when
quitting app
* [QTBUG-139400](https://bugreports.qt.io/browse/QTBUG-139400) Properly manage QtEditText focus and InputConnection
callbacks
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
* [QTBUG-138561](https://bugreports.qt.io/browse/QTBUG-138561) QFont::exactMatch index out of bounds
* [QTBUG-137769](https://bugreports.qt.io/browse/QTBUG-137769) Keyboard is not closed when TextEdit loses focus while
using TalkBack
* [QTBUG-138570](https://bugreports.qt.io/browse/QTBUG-138570) [REG 6.9.1 -> 6.10.0 Beta 2]
QFileSystemEngine::cloneFileTo hangs on FreeBSD 14.3
* [QTBUG-138947](https://bugreports.qt.io/browse/QTBUG-138947) QProgressBar completely blank on macOS 26
* [QTBUG-138942](https://bugreports.qt.io/browse/QTBUG-138942) Mac style (Widget and Quick) has issues on macOS 26
* [QTBUG-139292](https://bugreports.qt.io/browse/QTBUG-139292) Make section titles more language-neutral in app-
examples-template
* [QTBUG-138748](https://bugreports.qt.io/browse/QTBUG-138748) QContainerLayer is being erroneously passed to
vkCreateMetalSurfaceEXT, causing a crash
* [QTBUG-138986](https://bugreports.qt.io/browse/QTBUG-138986) glFramebufferTexture2DMultisampleEXT() is called with a
wrong samples argument if the requested sample count is unsupported
* [QTBUG-139128](https://bugreports.qt.io/browse/QTBUG-139128) QObject::connect(): clarify what a valid method is, in
the string-based overloads
* [QTBUG-139263](https://bugreports.qt.io/browse/QTBUG-139263) Missing operator documentation in QFont::Tag
* [QTBUG-139056](https://bugreports.qt.io/browse/QTBUG-139056) [Wayland] Crash on drag and drop cancel by escape
* [QTBUG-138984](https://bugreports.qt.io/browse/QTBUG-138984) Possible misinterpretation of
specifications.freedesktop.org/trash-spec
* [QTBUG-126134](https://bugreports.qt.io/browse/QTBUG-126134) Restarting multiple QThreads results in a crash
* [QTBUG-138504](https://bugreports.qt.io/browse/QTBUG-138504) Crash on Integer Overflow in QCheckedInt Operator+
(ASSERT in qcheckedint_impl.h:69)
* [QTBUG-139615](https://bugreports.qt.io/browse/QTBUG-139615) [REG 6.10.0 Beta2 -> 6.10.0 Beta3] error: non-POD static
* [QTBUG-139284](https://bugreports.qt.io/browse/QTBUG-139284) Include squish-tested-example.qdocinc file to the app-
examples-template
* [QTBUG-125138](https://bugreports.qt.io/browse/QTBUG-125138) QSqlDatabase::record() does not report generated columns
for SQlite
* [QTBUG-139586](https://bugreports.qt.io/browse/QTBUG-139586) [Reg 6.9.1->6.9.2] Cannot send broadcast on macOS
anymore
* [QTBUG-139600](https://bugreports.qt.io/browse/QTBUG-139600) Memory leak on macOS when adding application font from
data
* [QTBUG-138465](https://bugreports.qt.io/browse/QTBUG-138465) Line edits are not visible on macOS 26
* [QTBUG-139360](https://bugreports.qt.io/browse/QTBUG-139360) Editable combo box on macOS Tahoe
* [QTBUG-138946](https://bugreports.qt.io/browse/QTBUG-138946) QSlider issues on macOS 26
* [QTBUG-139778](https://bugreports.qt.io/browse/QTBUG-139778) BIC: Changed QRhi::create() signature
* [QTBUG-139845](https://bugreports.qt.io/browse/QTBUG-139845) Reg->6.11: Assert when passing a too long-list to
QMetaMethodBuilder::setParameterNames()
* [QTBUG-139720](https://bugreports.qt.io/browse/QTBUG-139720) Tag errors in QtAbstractItemModel for Java
* [QTBUG-139688](https://bugreports.qt.io/browse/QTBUG-139688) Public Java Classes Documentation Bugs
* [QTBUG-134082](https://bugreports.qt.io/browse/QTBUG-134082) Screen orientation change causes rendering issues on Qt
Quick Application (flicker related)
* [QTBUG-140064](https://bugreports.qt.io/browse/QTBUG-140064) error: array subscript 'QTransform[0]' is partly outside
array bounds of 'QVariant [1]'
* [QTBUG-139990](https://bugreports.qt.io/browse/QTBUG-139990) [REG 6.10.0 beta 3 -> beta 4] Building Qt examples for
WebAssembly fails
* [QTBUG-139989](https://bugreports.qt.io/browse/QTBUG-139989) FAIL!  : tst_QStateMachine::twoAnimations() Compared
values are not the same
* [QTBUG-140159](https://bugreports.qt.io/browse/QTBUG-140159) FAIL!  : tst_QStateMachine::twoAnimatedTransitions()
Compared values are not the same
* [QTBUG-140172](https://bugreports.qt.io/browse/QTBUG-140172) [qtbase] Build failure in wayland plugin with -no-opengl
* [QTCREATORBUG-33525](https://bugreports.qt.io/browse/QTCREATORBUG-33525) Dockwidgets have app icons icons
* [QTBUG-139425](https://bugreports.qt.io/browse/QTBUG-139425) Wayland: QEventLoop::ExcludeUserInputEvents doesn't work
* [QTBUG-140509](https://bugreports.qt.io/browse/QTBUG-140509) Main ABI libs are littered by secondary ABI libs
* [QTBUG-94708](https://bugreports.qt.io/browse/QTBUG-94708) qCDebug() and friends could pass the category as a tag in
Android
* [QTBUG-128900](https://bugreports.qt.io/browse/QTBUG-128900) macOS 15 deployment target build failure due to obsolete
API 'CGDisplayCreateImageForRect'
* [QTBUG-132072](https://bugreports.qt.io/browse/QTBUG-132072) QWidget::mapTo() crashed!
* [QTBUG-132114](https://bugreports.qt.io/browse/QTBUG-132114) qtbase/fe6dda9bb9310878b408b2421f60acb7135bd8ba breaks
-unity-build
* [QTBUG-131906](https://bugreports.qt.io/browse/QTBUG-131906) FAIL!  :
tst_qqmlecmascript::componentCreation(invalidMode) Not all expected
messages were received
* [QTBUG-131484](https://bugreports.qt.io/browse/QTBUG-131484) Fix links to QIODeviceBase::OpenMode flags
* [QTBUG-132051](https://bugreports.qt.io/browse/QTBUG-132051) Converting a QImage to an opaque format does not always
reset the alpha
* [QTBUG-131842](https://bugreports.qt.io/browse/QTBUG-131842) Qt's CSS parser doesn't eat unquoted URL strings with
query
* [QTBUG-130673](https://bugreports.qt.io/browse/QTBUG-130673) Windows11 Style : title bar doesn't highlight for active
mdisubwindow
* [QTBUG-132277](https://bugreports.qt.io/browse/QTBUG-132277) Qt fails to adhere to HTTP/2 HPACK dynamic table size
changes
* [QTBUG-132244](https://bugreports.qt.io/browse/QTBUG-132244) SQLite not found in qttools when building system SQLite
in Windows
* [QTBUG-132261](https://bugreports.qt.io/browse/QTBUG-132261) Many minor styling issues on windows 11
* [QTBUG-129754](https://bugreports.qt.io/browse/QTBUG-129754) Top flaky test: tst_qgesturerecognizer::touchReplay
* [QTBUG-131887](https://bugreports.qt.io/browse/QTBUG-131887) [Boot to Qt 6.9.0 snapshot] jetson-agx-orin cannot start
qtlauncher
* [QTBUG-129777](https://bugreports.qt.io/browse/QTBUG-129777) TOCTOU in QTranslator::load()'s helper
find_translation()
* [QTBUG-128420](https://bugreports.qt.io/browse/QTBUG-128420) Qt 6.8 does not support build paths with white spaces
anymore
* [QTBUG-132507](https://bugreports.qt.io/browse/QTBUG-132507) Fix review findings in QUniqueHandle
* [QTBUG-119490](https://bugreports.qt.io/browse/QTBUG-119490) qcocoaapplicationdelegate.mm:354:20: error: cannot
initialize return object of type 'BOOL'
* [QTBUG-131585](https://bugreports.qt.io/browse/QTBUG-131585) The QTreeWidget is painting poorly when the frame style
is set to QFrame::Plain | QFrame::Box when using Windows 11 style.
* [QTBUG-131377](https://bugreports.qt.io/browse/QTBUG-131377) Include Chromium in SBOM
* [QTBUG-128893](https://bugreports.qt.io/browse/QTBUG-128893) sbom for qtpdf gets lost , as it ends up as qtwebengine
sbom
* [QTBUG-12673](https://bugreports.qt.io/browse/QTBUG-12673) Crash in QWidgetPrivate::init on QApplication::quit()
using a modal dialog on Mac
* [QTBUG-132433](https://bugreports.qt.io/browse/QTBUG-132433) Windows 11 style - QToolButton/QPushButton quirks
* [QTBUG-132388](https://bugreports.qt.io/browse/QTBUG-132388) QChronoTimer::remainingTime() can not return anything
larger than ~24days on Windows
* [QTBUG-128466](https://bugreports.qt.io/browse/QTBUG-128466) Incorrect QInputDevice::capabilities() value for Apple
Pencil
* [QTBUG-123711](https://bugreports.qt.io/browse/QTBUG-123711) QtQuickView doesn't handle recreation of Activity
properly
* [QTBUG-127777](https://bugreports.qt.io/browse/QTBUG-127777) doc deprecates both ways to open a modal dialog
* [QTBUG-132785](https://bugreports.qt.io/browse/QTBUG-132785) QFile::rename() deletes file and fails to rename on
Windows/NFS
* [QTBUG-128467](https://bugreports.qt.io/browse/QTBUG-128467)  Incompatible QTabletEvent::rotation() value for Apple
Pencil
* [QTBUG-115717](https://bugreports.qt.io/browse/QTBUG-115717) QSortFilterProxyModel::invalidateFilter() sometimes does
not trigger a reevaluation of the model
* [QTBUG-132646](https://bugreports.qt.io/browse/QTBUG-132646) Add a variant of QTemporaryFile::rename() that
overwrites
* [QTBUG-131916](https://bugreports.qt.io/browse/QTBUG-131916) Quoting and QML files with white spaces in the path are
not supported in qmldir
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-133206](https://bugreports.qt.io/browse/QTBUG-133206) QThreadPrivate saying "QThreadStorage: Thread %p exited
after QThreadStorage %d destroyed"
* [QTBUG-133219](https://bugreports.qt.io/browse/QTBUG-133219) Adding more tests causes Emscripten compiler to run out
of memory on CI
* [QTBUG-129222](https://bugreports.qt.io/browse/QTBUG-129222) Sporadic segfault at getenv from pulseaudio during boot
* [QTBUG-114957](https://bugreports.qt.io/browse/QTBUG-114957) Clarify handling of FileDialog.nameFilter on Android
* [QTBUG-132070](https://bugreports.qt.io/browse/QTBUG-132070) Ubuntu 24.04 x64: Sometimes hundreds of tests failing
* [QTBUG-126827](https://bugreports.qt.io/browse/QTBUG-126827) Configuring a cmake-based Qt Quick project fails if the
path contains spaces
* [QTBUG-35598](https://bugreports.qt.io/browse/QTBUG-35598) QtQuick Controls TextField and TextArea miss mouse
context menu
* [QTBUG-133548](https://bugreports.qt.io/browse/QTBUG-133548) IMAP tests are consistently failing
* [QTBUG-127953](https://bugreports.qt.io/browse/QTBUG-127953) Basic support for CMake FetchContent
* [QTBUG-133293](https://bugreports.qt.io/browse/QTBUG-133293) QPicture overflows the bounding rect calculations
* [QTBUG-30133](https://bugreports.qt.io/browse/QTBUG-30133) QScroller auto-test is flakey
* [QTBUG-107893](https://bugreports.qt.io/browse/QTBUG-107893) cmake: multi-ABI Android builds do not forward cmake
arguments
* [QTBUG-132633](https://bugreports.qt.io/browse/QTBUG-132633) QDir::mkpath() is missing an overload with permissions
* [QTBUG-134105](https://bugreports.qt.io/browse/QTBUG-134105) tst_qscroller::overshoot() is flaky on macOS
* [QTBUG-106025](https://bugreports.qt.io/browse/QTBUG-106025) REG: isSignalConnected creates a dead lock.
* [QAA-2836](https://bugreports.qt.io/browse/QAA-2836) Make sure that all references to "Qt Android" are changed to
"Qt for Android"
* [QTBUG-133805](https://bugreports.qt.io/browse/QTBUG-133805) QFileDialog shouldn't write to QtProject.conf
* [QTBUG-132947](https://bugreports.qt.io/browse/QTBUG-132947) Geometry classes may have unsound `noexcept` on their
methods
* [QTBUG-133761](https://bugreports.qt.io/browse/QTBUG-133761) Update Qt Creator help mode colours to match the current
themes
* [QTBUG-134250](https://bugreports.qt.io/browse/QTBUG-134250) qdoc fails to report warnings for incorrect \fn
signatures
* [QTBUG-134148](https://bugreports.qt.io/browse/QTBUG-134148) When relying on implicit PCH, QML_ELEMENT is not
processed by qmltyperegistrar
* [QTBUG-133882](https://bugreports.qt.io/browse/QTBUG-133882) Polish string types overview
* [QTBUG-127549](https://bugreports.qt.io/browse/QTBUG-127549) QDomNode::save() takes huge amount of time. 10x worse
performance when compared to Qt 5
* [QTBUG-134557](https://bugreports.qt.io/browse/QTBUG-134557) QOpenGLFramebufferObject seems to leak
QOpenGLSharedResourceGuards
* [QTBUG-83817](https://bugreports.qt.io/browse/QTBUG-83817) potential out-of-bounds access in qcssparser
* [QTBUG-115926](https://bugreports.qt.io/browse/QTBUG-115926) WASM: In the QML Accessibility demo application, menu
items are not getting focus.
* [QTBUG-132526](https://bugreports.qt.io/browse/QTBUG-132526) Some CMake targets of private Qt modules reference non-
existent include dirs
* [QTBUG-86387](https://bugreports.qt.io/browse/QTBUG-86387) Support consuming XCFramework with qmake
* [QTBUG-118901](https://bugreports.qt.io/browse/QTBUG-118901) qt_feature for exceptions
* [QTBUG-133215](https://bugreports.qt.io/browse/QTBUG-133215) [Reg 6.6 -> 6.8] QMainWindow removes titlebar exception
* [QTBUG-134671](https://bugreports.qt.io/browse/QTBUG-134671) [VxWorks] QEGLPlatformContext::getProcAddress doesn't
work with static ogl libraries
* [QTBUG-127012](https://bugreports.qt.io/browse/QTBUG-127012) iOS: ASSERT: "qmlType.metaObject()" in
fileqqmltypedata.cpp, line 1019
* [QTBUG-134883](https://bugreports.qt.io/browse/QTBUG-134883) QML on Windows: Unable to assign ClassA to ClassA
* [QTBUG-130480](https://bugreports.qt.io/browse/QTBUG-130480) Windows 11 Style does not change the palette before
QEvent::PaletteChange
* [QTBUG-135037](https://bugreports.qt.io/browse/QTBUG-135037) QKdeTheme leaks QFont objects
* [QTBUG-135055](https://bugreports.qt.io/browse/QTBUG-135055) QScroller::grabGesture() appears to leak its
QFlickGestureRecognizer
* [QTBUG-122980](https://bugreports.qt.io/browse/QTBUG-122980) [REG -> dev] Unity Build broken
* [QTBUG-135134](https://bugreports.qt.io/browse/QTBUG-135134) [REG -> dev] Windows Network: Unity Build broken
* [QTBUG-134999](https://bugreports.qt.io/browse/QTBUG-134999) [Boot2Qt ] 'Failed to build graphics pipeline' when
running 'orderindependenttransparency' example
* [QTBUG-131459](https://bugreports.qt.io/browse/QTBUG-131459) QDoc: No warning if \qmltype contains \inherits with
non-existing type
* [QTBUG-135138](https://bugreports.qt.io/browse/QTBUG-135138) Investigate memory leaks on widget tests
* [QTBUG-135151](https://bugreports.qt.io/browse/QTBUG-135151) UB when active menu of a menu bar is being deleted
* [QTBUG-135146](https://bugreports.qt.io/browse/QTBUG-135146) [vxworks] not possible to build vkb with static build
and dlopen feature turned off
* [QTBUG-99563](https://bugreports.qt.io/browse/QTBUG-99563) The QMutable*Event construct is Undefined Behaviour
* [QTBUG-135382](https://bugreports.qt.io/browse/QTBUG-135382) Invalid year zero date asserts in
QDateTimeParser::parse()
* [QTBUG-135470](https://bugreports.qt.io/browse/QTBUG-135470) First access to
QSettings("HKEY_CLASSES_ROOT").childGroups() has "*" node
* [QTBUG-135410](https://bugreports.qt.io/browse/QTBUG-135410) tst_QDockWidget::titleBarDoubleClick() causes UB in
QDockWidget::event()
* [QTBUG-135626](https://bugreports.qt.io/browse/QTBUG-135626) QPointer causes unneccessary (invalid) downcasts
* [QTBUG-131650](https://bugreports.qt.io/browse/QTBUG-131650) qtwebengine does not compile under sccache, with note
note: please rebuild precompiled header
* [QTBUG-135621](https://bugreports.qt.io/browse/QTBUG-135621) gn.py needs an -isysroot argument but configure doesn't
create it
* [QTBUG-134627](https://bugreports.qt.io/browse/QTBUG-134627) [VxWorks] QTranslator load fails reading from SD card
* [QTBUG-135966](https://bugreports.qt.io/browse/QTBUG-135966) Blacklist tst_QFileDialog::clearLineEdit() on vxworks
* [QTBUG-135963](https://bugreports.qt.io/browse/QTBUG-135963) Blacklist tst_QFileDialog::completer on vxworks
* [QTBUG-135976](https://bugreports.qt.io/browse/QTBUG-135976) Memory leaks in QAlphaWidget and QRollEffect
* [QTBUG-136101](https://bugreports.qt.io/browse/QTBUG-136101) Minimal configuration compile with autotests
* [QTBUG-135612](https://bugreports.qt.io/browse/QTBUG-135612) QScreen::devicePixelRatio returns incorrect
values(integer value) on Wayland with fractional scaling in both Qt5 and
Qt6 (Manjaro).
* [QTBUG-136215](https://bugreports.qt.io/browse/QTBUG-136215) QComboBox list cannot display strikeOut text in its list
on mac
* [QTBUG-135967](https://bugreports.qt.io/browse/QTBUG-135967) QGeoPolygon does not serialize its holes
* [QTBUG-104930](https://bugreports.qt.io/browse/QTBUG-104930) QLocale shows German text for "en_DE"
* [QTBUG-10506](https://bugreports.qt.io/browse/QTBUG-10506) QCalendarWidget in Chinese locale shows wrong weekday
names
* [QTBUG-84877](https://bugreports.qt.io/browse/QTBUG-84877) QLocale::system() uses short names of days and months for
narrow formats
* [QTBUG-131897](https://bugreports.qt.io/browse/QTBUG-131897) pdf viewer is not working on nano browser and simple
browser sample apps
* [QTBUG-135947](https://bugreports.qt.io/browse/QTBUG-135947) No simple explanation (i.e. flow chart) for which string
to use in non-API use cases
* [QTBUG-135645](https://bugreports.qt.io/browse/QTBUG-135645) Issue in qvulkanwindow.cpp
* [QTBUG-136687](https://bugreports.qt.io/browse/QTBUG-136687) [regression 6.9.0] Wasm LibreOffice no longer gets
keyboard input events
* [QTBUG-136741](https://bugreports.qt.io/browse/QTBUG-136741) QWasmSuspendControl - missing signature for dynamic
linking
* [QTBUG-136722](https://bugreports.qt.io/browse/QTBUG-136722) [VxWorks] qthread_unix contains DKM related code
* [QTBUG-136716](https://bugreports.qt.io/browse/QTBUG-136716) QDockWidget glitches when moving/pushing unless undocked
and redocked
* [QTBUG-122590](https://bugreports.qt.io/browse/QTBUG-122590) Transparency not working correctly for Window Embedding
in QML
* [QTBUG-135859](https://bugreports.qt.io/browse/QTBUG-135859) WindowContainer cannot handle transparent Window
properly
* [QTBUG-136627](https://bugreports.qt.io/browse/QTBUG-136627) Blacklist tst_QDnsLookup::lookupNxDomain for Windows 11
* [QTBUG-135599](https://bugreports.qt.io/browse/QTBUG-135599) Network test failures in Windows 11 24h2
* [QTBUG-136628](https://bugreports.qt.io/browse/QTBUG-136628) Skip tst_qnetworkinformation_appless for Windows 11
* [QTBUG-136755](https://bugreports.qt.io/browse/QTBUG-136755) QQuickWindow::grabWindow() results in a black background
color instead of being transparent with the Offscreen platform.
* [QTBUG-121822](https://bugreports.qt.io/browse/QTBUG-121822) WASM Clang++ ignores EXCEPTIONS settings in asyncify
config
* [QTBUG-137069](https://bugreports.qt.io/browse/QTBUG-137069) tst_QWidget::palettePropagation3() runs into UB
* [QTBUG-137005](https://bugreports.qt.io/browse/QTBUG-137005) Qt6::qmltestrunner target no longer available
* [QTBUG-136337](https://bugreports.qt.io/browse/QTBUG-136337) [REG 6.8.3->6.9.0] ext-session-lock-v1 can no longer be
implemented with QtWayland due to forced null buffer attach
* [QTBUG-136110](https://bugreports.qt.io/browse/QTBUG-136110) [Reg 6.8->6.9] Crash when opening popup (when creating
new C++ class) (Wayland protocol error)
* [QTBUG-116197](https://bugreports.qt.io/browse/QTBUG-116197) org.freedesktop.appearance.color-scheme is supported in
a weird way
* [QTBUG-137228](https://bugreports.qt.io/browse/QTBUG-137228) Cross-compiled ARM64 Windows binaries are not digitally
signed
* [QTBUG-122596](https://bugreports.qt.io/browse/QTBUG-122596) [REG 6.7.0->6.8.0] error in configure step, top level
build, MinGW
* [QTBUG-55421](https://bugreports.qt.io/browse/QTBUG-55421) broken links to QBasicAtomic* in published docs
* [QTBUG-112355](https://bugreports.qt.io/browse/QTBUG-112355) ShaderEffectSource with recursive shader causes magenta
texture on Apple Silicon
* [QTBUG-132775](https://bugreports.qt.io/browse/QTBUG-132775) QSortFilterProxyModel fails to receive beginResetModel
* [QTBUG-120138](https://bugreports.qt.io/browse/QTBUG-120138) Showing a child Window more than once fails on
WebAssembly
* [QTBUG-134239](https://bugreports.qt.io/browse/QTBUG-134239) QAbstractFileIconProvider::icon() always returns null on
mobile platforms
* [QTBUG-134208](https://bugreports.qt.io/browse/QTBUG-134208) Mnemonic annotation is passed to screen readers
* [QTBUG-137885](https://bugreports.qt.io/browse/QTBUG-137885) QPainter::brushOrigin() returns a QPoint instead QPointF
* [QTBUG-137942](https://bugreports.qt.io/browse/QTBUG-137942) test result file
tst_qmltc_examples-1750626901804.junit.xml is empty
* [QTCREATORBUG-32932](https://bugreports.qt.io/browse/QTCREATORBUG-32932) Automatic selection of too low Android SDK version
* [QTBUG-115078](https://bugreports.qt.io/browse/QTBUG-115078) icx requires -mcx16 flag to compile
_InterlockedCompareExchange128 on windows
* [QTBUG-138246](https://bugreports.qt.io/browse/QTBUG-138246) Q{Shared,Weak}Pointer::IfCompatible cause accidental
copy/move SMFs, causing FTBFS in qtdeclarative
* [QTBUG-138155](https://bugreports.qt.io/browse/QTBUG-138155) qt_generate_deploy_qml_app_script: Error for space in
output name
* [QTBUG-138471](https://bugreports.qt.io/browse/QTBUG-138471) QString::arg() convert floating type to integer
* [QTBUG-137126](https://bugreports.qt.io/browse/QTBUG-137126) QAccessible::ActionChanged event not sent anywhere in Qt
* [QTBUG-138192](https://bugreports.qt.io/browse/QTBUG-138192) Android Templates, Manifest and CMake Properties
* [QTBUG-135413](https://bugreports.qt.io/browse/QTBUG-135413) Accessible.announce not working on iOS and Android
* [QTBUG-138562](https://bugreports.qt.io/browse/QTBUG-138562) QLocalePrivate::codeToLanguage() does not sanitize the
input before passing it to AlphaCode
* [QTBUG-138610](https://bugreports.qt.io/browse/QTBUG-138610) QTemporaryFile::rename() overwrites existing file on
Android
* [QTBUG-132617](https://bugreports.qt.io/browse/QTBUG-132617) Unclear behaviour of QTemporaryFile::rename()
* [QTBUG-138583](https://bugreports.qt.io/browse/QTBUG-138583) QLocale::toUpper() is not 64-bit-safe on ICU
* [QTBUG-2163](https://bugreports.qt.io/browse/QTBUG-2163) Support for conditions in special casing of unicode
characters is missing in Qt
* [QTBUG-138705](https://bugreports.qt.io/browse/QTBUG-138705) Windows backend of QLocale::toLower() does not implement
Greek Final Sigma rule
* [QTBUG-138527](https://bugreports.qt.io/browse/QTBUG-138527) Replace direct links to https://doc.qt.io/qt-6/
* [QTBUG-137933](https://bugreports.qt.io/browse/QTBUG-137933) stale-property-read for flags
* [QTBUG-107907](https://bugreports.qt.io/browse/QTBUG-107907) QOperatingSystemVersion::Windows10 <
QOperatingSystemVersion::Windows11 == false
* [QTBUG-136045](https://bugreports.qt.io/browse/QTBUG-136045) macOS: Window geometry is not updated correctly when the
OS rejects a change by setGeometry
* [QTBUG-134546](https://bugreports.qt.io/browse/QTBUG-134546) [VxWorks] exit on poll error should be on by default
like in 5.15
* [QTBUG-138829](https://bugreports.qt.io/browse/QTBUG-138829) Fix uses of deprecated
NSWindowStyleMaskTexturedBackground
* [QTBUG-37759](https://bugreports.qt.io/browse/QTBUG-37759) QWidget-gestures do not work
* [QTBUG-46195](https://bugreports.qt.io/browse/QTBUG-46195) [Windows]: Swipe gesture is not always recognized and
sometimes in the wrong direction
* [QTBUG-138831](https://bugreports.qt.io/browse/QTBUG-138831) [VxWorks] EDOOM handling is missing from 6.x
* [QTBUG-138851](https://bugreports.qt.io/browse/QTBUG-138851) Quadratic behaviour in qlocale.cpp when building
uiLanguages
* [QTBUG-137860](https://bugreports.qt.io/browse/QTBUG-137860) [Windows][A11y] Text can not be selected by NVDA
* [QTBUG-138878](https://bugreports.qt.io/browse/QTBUG-138878) QNetworkRequestFactory creates an incorrect network
request
* [QTBUG-138403](https://bugreports.qt.io/browse/QTBUG-138403) QDirIterator → QDirListing should have some porting
documentation
* [QTBUG-132211](https://bugreports.qt.io/browse/QTBUG-132211) [REG 6.7 -> 6.8][Android] UnsatisfiedLinkError onResume
and onNewIntent
* [QTBUG-120467](https://bugreports.qt.io/browse/QTBUG-120467) Link error from Google Play testing
* [QTBUG-70114](https://bugreports.qt.io/browse/QTBUG-70114) Java native functions registered with a delay
* [QTBUG-86314](https://bugreports.qt.io/browse/QTBUG-86314) Error in 64bit lib file path names
* [QTBUG-134093](https://bugreports.qt.io/browse/QTBUG-134093) Android application crashes on 16 KB page size
* [QTBUG-138882](https://bugreports.qt.io/browse/QTBUG-138882) [Wayland] QWaylandShmBackingStore::scroll() is scrolling
the busy buffer
* [QTBUG-139055](https://bugreports.qt.io/browse/QTBUG-139055) CMake Error at tst_qstatemachineWrapperDebug
* [QTBUG-139139](https://bugreports.qt.io/browse/QTBUG-139139) ubuntu-24.04-x64-developer-build: Part of the build is
using qmake and ignores SCCACHE settings
* [QTBUG-136653](https://bugreports.qt.io/browse/QTBUG-136653) tst_QAbstractItemView::testDialogAsEditor() crash on
Ubuntu 24.04 x11
* [QTCREATORBUG-33334](https://bugreports.qt.io/browse/QTCREATORBUG-33334) UI glitch with scrolling
* [QTBUG-132108](https://bugreports.qt.io/browse/QTBUG-132108) addApplicationFontFromData behaves abnormally after
removeAllApplicationFonts.
* [QTBUG-138249](https://bugreports.qt.io/browse/QTBUG-138249) Win11 23h2 ARM: QtBase -
tst_QRhiWidget::grabFramebufferWhileStillInvisible fails
* [QTBUG-138252](https://bugreports.qt.io/browse/QTBUG-138252) Win11 23h2 ARM: QtBase -
tst_QRhiWidget::grabFramebufferWhileStillInvisible fails with cross-
compilation target
* [QTBUG-139283](https://bugreports.qt.io/browse/QTBUG-139283) QInputDevice::availableVirtualGeometry property
incomplete
* [QTBUG-139275](https://bugreports.qt.io/browse/QTBUG-139275) [a11y] Changes to Accessible.name for focused element
not announced to Screen Reader
* [QTBUG-138883](https://bugreports.qt.io/browse/QTBUG-138883) [Wayland] Missing enter event when modal windows is
closed and cursor is over parent window
* [QTBUG-138901](https://bugreports.qt.io/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-138806](https://bugreports.qt.io/browse/QTBUG-138806) [VxWorks] Flickable doesn't work on VxWorks
* [QTBUG-107028](https://bugreports.qt.io/browse/QTBUG-107028) tst_qquicktextfield and tst_qquicktextarea fail on
Android
* [QTBUG-100259](https://bugreports.qt.io/browse/QTBUG-100259) tst_controls crash on Android
* [QTBUG-100258](https://bugreports.qt.io/browse/QTBUG-100258) tst_focus crashes on Android
* [QTBUG-139415](https://bugreports.qt.io/browse/QTBUG-139415) tst_controls has failing test cases
* [QTBUG-138699](https://bugreports.qt.io/browse/QTBUG-138699) Square push buttons (macOS 26)
* [QTBUG-139405](https://bugreports.qt.io/browse/QTBUG-139405) QMatrix4x4 has an internal Flag enum that QDoc exposes
as flags
* [QTBUG-133086](https://bugreports.qt.io/browse/QTBUG-133086) Doc: Improve Networking and WebEngine security topics
* [QTBUG-139606](https://bugreports.qt.io/browse/QTBUG-139606) [regression] App window blank when switching from
background to foreground
* [QTBUG-139659](https://bugreports.qt.io/browse/QTBUG-139659) Activity can stop reacting to touch events
* [QTBUG-138700](https://bugreports.qt.io/browse/QTBUG-138700) Tabs have wrong shape on macOS 26
* [QTBUG-138738](https://bugreports.qt.io/browse/QTBUG-138738) Incorrect focus ring rendering
* [QTBUG-138948](https://bugreports.qt.io/browse/QTBUG-138948) Radio button alignment issues on macOS 26
* [QTBUG-138893](https://bugreports.qt.io/browse/QTBUG-138893) QTimeZone(Qt::UTC) returns incorrect UTC offset (+1
second)
* [QTBUG-139950](https://bugreports.qt.io/browse/QTBUG-139950) tst_QGraphicsProxyWidget::windowOpacity is flaky and/or
failing on macOS
* [QTBUG-139986](https://bugreports.qt.io/browse/QTBUG-139986) QStateMachine tests aren't running on the CI
* [QTBUG-140038](https://bugreports.qt.io/browse/QTBUG-140038) tst_QGridLayout::spacingsAndMargins fails on Android 15
* [QTBUG-140133](https://bugreports.qt.io/browse/QTBUG-140133) tst_QGraphicsProxyWidget::createProxyForChildWidget
fails with non-zero safe area margins
* [QTBUG-117447](https://bugreports.qt.io/browse/QTBUG-117447) Remove *-proxy.html pages in Qt Core

### qtsvg
* [QTBUG-132468](https://bugreports.qt.io/browse/QTBUG-132468) Polyline with stroke displays nothing when all points
are the same
* [QTBUG-134044](https://bugreports.qt.io/browse/QTBUG-134044) SvgHandler might access out of bound
* [QTBUG-126487](https://bugreports.qt.io/browse/QTBUG-126487) image element is not properly tested in QtSvg
* [QTBUG-134735](https://bugreports.qt.io/browse/QTBUG-134735) Aliased rendering of resized, rotated png image
* [QTBUG-135596](https://bugreports.qt.io/browse/QTBUG-135596) SVG Stroke Animation Rendering Issue in Qt6.9.0
* [QTBUG-135363](https://bugreports.qt.io/browse/QTBUG-135363) REG: SVG shows up as black silhouette
* [QTBUG-126482](https://bugreports.qt.io/browse/QTBUG-126482) QtSvg ignores units
* [QTBUG-135483](https://bugreports.qt.io/browse/QTBUG-135483) [REG 6.7-> 6.8] Loading order affects QIcon state and
mode when adding svg images
* [QTBUG-123817](https://bugreports.qt.io/browse/QTBUG-123817) QTextLayout::draw() renders text as path and not text
* [QTBUG-126268](https://bugreports.qt.io/browse/QTBUG-126268) Text rendering does not handle fill and stroke opacities
correctly
* [QTBUG-137553](https://bugreports.qt.io/browse/QTBUG-137553) [REG 6.8.2 -> 6.8.3] Significant performance regression
in SVG loading with PySide6 6.8.3
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-132526](https://bugreports.qt.io/browse/QTBUG-132526) Some CMake targets of private Qt modules reference non-
existent include dirs
* [QTBUG-49160](https://bugreports.qt.io/browse/QTBUG-49160) Rendering SVG icon in QFileBox on Fedora22 crashes Qt
* [QTBUG-137700](https://bugreports.qt.io/browse/QTBUG-137700) QIcon::pixmap selects wrong icon file from theme
* [QTBUG-138901](https://bugreports.qt.io/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist

### qtdeclarative
* [QTBUG-131675](https://bugreports.qt.io/browse/QTBUG-131675) QML: Document "regexp" value type
* [QTBUG-131261](https://bugreports.qt.io/browse/QTBUG-131261) Use QML types Application QML Type documentation
* [QTBUG-132050](https://bugreports.qt.io/browse/QTBUG-132050) [Reg 6.8 -> 6.9] Different behavior in QML regex
compared to javascript
* [QTBUG-131958](https://bugreports.qt.io/browse/QTBUG-131958) qmlls: import warnings on wrong line
* [QTBUG-131296](https://bugreports.qt.io/browse/QTBUG-131296) qmlls fails to parse some QML modules and C++ types when
there is more than one QML module in a directory
* [QTBUG-132071](https://bugreports.qt.io/browse/QTBUG-132071) QML Window Container: Tab Focus between parent and
embedded window doesn't work
* [QTBUG-128462](https://bugreports.qt.io/browse/QTBUG-128462) Qt Quick Dialog colors are wrong when switching themes
* [QTBUG-131980](https://bugreports.qt.io/browse/QTBUG-131980) [REG 6.5.4-6.8.1] Crash on value type property
initialization
* [QTCREATORBUG-31881](https://bugreports.qt.io/browse/QTCREATORBUG-31881) QML Control + Click opens debug file
* [QTBUG-131920](https://bugreports.qt.io/browse/QTBUG-131920) F2 shortcut in qml files leads to build dir instead of
source
* [QTBUG-129231](https://bugreports.qt.io/browse/QTBUG-129231) Sporadic crash on QQuickListViewPrivate::fixup()
* [QTBUG-132192](https://bugreports.qt.io/browse/QTBUG-132192) Item is not updated if it would be invisible under
software render
* [QTBUG-131957](https://bugreports.qt.io/browse/QTBUG-131957) [REG 6.8.0 → 6.8.1] QML applications crash on macOS 12
(x86)
* [QTBUG-130328](https://bugreports.qt.io/browse/QTBUG-130328) the visual focus indicator of Button in FluentWinUI3
style doesn't work well with FocusScope
* [QTBUG-131961](https://bugreports.qt.io/browse/QTBUG-131961) Qml engine crashes when running SameValueZero
* [QTBUG-127691](https://bugreports.qt.io/browse/QTBUG-127691) qmllint: don't print duplicate warnings
* [QTBUG-131774](https://bugreports.qt.io/browse/QTBUG-131774) [REG 5.15 → 6] remove warning on signal connect with no
arguments
* [QTBUG-132329](https://bugreports.qt.io/browse/QTBUG-132329) [Reg 6.8 -> 6.9] qmlcachegen miscompiles number
coercions
* [QTBUG-131901](https://bugreports.qt.io/browse/QTBUG-131901) "var" and "variant" type properties emit valueChanged
signal even when value remains unchanged
* [QTBUG-132421](https://bugreports.qt.io/browse/QTBUG-132421) cmake: Specifying PROJECT_VERSION in a Quick project
fails generation
* [QTBUG-132528](https://bugreports.qt.io/browse/QTBUG-132528) qmlcompiler/qqmljscompilerstats_p.h", line 33: error
#276:  name followed by "::" must be a class or namespace name
* [QTBUG-132423](https://bugreports.qt.io/browse/QTBUG-132423) [Reg 6.2.13->6.5] qtquickcompiler.prf is missing from
cross-compiling kits, so "CONFIG += qtquickcompiler" no longer works
when cross-compiling
* [QTBUG-132380](https://bugreports.qt.io/browse/QTBUG-132380) QQmlTypeLoader::importAndDestroy() is flaky
* [QTBUG-128269](https://bugreports.qt.io/browse/QTBUG-128269) QQmlEngine destructor hangs on
QQmlTypeLoader::invalidate
* [QTBUG-129143](https://bugreports.qt.io/browse/QTBUG-129143) QML Text - Wrong implicitWidth
* [QTBUG-132118](https://bugreports.qt.io/browse/QTBUG-132118) Crash when adding JS resources to a QML document
directory
* [QTBUG-132499](https://bugreports.qt.io/browse/QTBUG-132499) assertion failure in callQObjectMethodAsVariant when
using qml cache
* [QTBUG-132355](https://bugreports.qt.io/browse/QTBUG-132355) Build failure with no-feature-quick-draganddrop option
* [QTBUG-132350](https://bugreports.qt.io/browse/QTBUG-132350) "QML debugging is enabled" warning is not guaranteed to
show at startup
* [QTBUG-132523](https://bugreports.qt.io/browse/QTBUG-132523) Null pointer dereference causing crash in QQuickPopup
* [QTBUG-132684](https://bugreports.qt.io/browse/QTBUG-132684) Using QT_TR_NOOP with disambiguation string in a
ListElement causes runtime error
* [QTBUG-132628](https://bugreports.qt.io/browse/QTBUG-132628) tst_taphandler::longPress is flaky on OpenSUSE
* [QTBUG-132100](https://bugreports.qt.io/browse/QTBUG-132100) Foreign QObject with an enum type cannot be registered
for Qml in a nested namespace
* [QTBUG-132737](https://bugreports.qt.io/browse/QTBUG-132737) Freeze when scrolling testbench
* [QTBUG-132134](https://bugreports.qt.io/browse/QTBUG-132134) qmlls crashed
* [QTBUG-131721](https://bugreports.qt.io/browse/QTBUG-131721) QML type loader thread has data races
* [QTBUG-132792](https://bugreports.qt.io/browse/QTBUG-132792) qtabstractitemmodel_java settings.gradle has duplicate
information
* [QTBUG-132408](https://bugreports.qt.io/browse/QTBUG-132408) VectorImage transform replace animations sometimes wrong
* [QTBUG-132805](https://bugreports.qt.io/browse/QTBUG-132805) qmllint: default property
* [QTBUG-132783](https://bugreports.qt.io/browse/QTBUG-132783) [Reg 6.8.1 -> 6.9] qmllint: exec of regex
* [QTBUG-132514](https://bugreports.qt.io/browse/QTBUG-132514) Fix navigation in Qml WorkerScript and XmlListModel
projects
* [QTBUG-132553](https://bugreports.qt.io/browse/QTBUG-132553) ContextMenu docs are incomplete
* [QTBUG-131576](https://bugreports.qt.io/browse/QTBUG-131576) Dialog of QtQuick.Dialogs not valid
* [QTBUG-128229](https://bugreports.qt.io/browse/QTBUG-128229) JavaScript library has cyclic dependeny on itself when
importing its own qml module
* [QTBUG-127294](https://bugreports.qt.io/browse/QTBUG-127294) qmllint: too many warnings when accessing an attached
type from a value type
* [QTBUG-128420](https://bugreports.qt.io/browse/QTBUG-128420) Qt 6.8 does not support build paths with white spaces
anymore
* [QTBUG-65463](https://bugreports.qt.io/browse/QTBUG-65463) ApplicationWindow.window attached property not available
due to component versioning
* [QTBUG-88626](https://bugreports.qt.io/browse/QTBUG-88626) tst_qqmltimer::restartWhenEventPosted() failed on
msvc2019 developer build in CI
* [QTBUG-132921](https://bugreports.qt.io/browse/QTBUG-132921) Crash in QmlCacheGeneratedCode
* [QTBUG-133047](https://bugreports.qt.io/browse/QTBUG-133047) [Reg 6.5 -> 6.8] qmlsc: list<QtObject> property-of-a-
property is not bound correctly
* [QTBUG-132280](https://bugreports.qt.io/browse/QTBUG-132280) qmlformat: The optional chaining operator (JavaScript)
is incorrectly removed when followed by an array access
* [QTBUG-133225](https://bugreports.qt.io/browse/QTBUG-133225) fix qmlformat cli option / settings file  precedence
* [QTBUG-133230](https://bugreports.qt.io/browse/QTBUG-133230) Removed ShapePaths are still rendered
* [QTBUG-133231](https://bugreports.qt.io/browse/QTBUG-133231) Removing ShapePaths from Shape results in properties for
other shapes being confused
* [QTBUG-131386](https://bugreports.qt.io/browse/QTBUG-131386) qmlformat inserts a new space after block comment on
file save
* [QTBUG-130570](https://bugreports.qt.io/browse/QTBUG-130570) "Scene Graph - RHI Under QML" documentation error
* [QTBUG-133323](https://bugreports.qt.io/browse/QTBUG-133323) gcc 15: build error with src/qmldom/qqmldomtop.cpp
* [QTBUG-132715](https://bugreports.qt.io/browse/QTBUG-132715) quickcontrols/gallery: double clicking item in drawer
opens view twice
* [QTBUG-133380](https://bugreports.qt.io/browse/QTBUG-133380) FAIL!  : tst_QQuickMenu::FluentWinUI3::mouse(Popup.Item)
Compared values are not the same
* [QTBUG-133398](https://bugreports.qt.io/browse/QTBUG-133398) qmlformat: Line-by-line formatter can't handle certain
property definitions
* [QTBUG-132065](https://bugreports.qt.io/browse/QTBUG-132065) qmlformat: 'From' properties confuses
IndentingLineWriter
* [QTBUG-133301](https://bugreports.qt.io/browse/QTBUG-133301) Crash when moving columns in an empty qml tableview
* [QTBUG-133052](https://bugreports.qt.io/browse/QTBUG-133052) modelData is lost when using a nested QML component
inside a Repeater
* [QTBUG-133129](https://bugreports.qt.io/browse/QTBUG-133129) DelegateModel can create delegates with unset required
properties in sub-objects
* [QTBUG-120951](https://bugreports.qt.io/browse/QTBUG-120951) connecting signal of aliased property in QML to C++ slot
doesn't work
* [QTBUG-131903](https://bugreports.qt.io/browse/QTBUG-131903) Item.transform is not readonly
* [QTBUG-118847](https://bugreports.qt.io/browse/QTBUG-118847) cpp object property getter is called too often for local
qml var access
* [QTBUG-127322](https://bugreports.qt.io/browse/QTBUG-127322) JSON.stringify() on property of type QVariantList reads
property for every list element
* [QTBUG-133053](https://bugreports.qt.io/browse/QTBUG-133053) [Reg 6.5 -> 6.8] Qt 6.8 silently removed sharing of
global variables between 2 typescript/javascript files
* [QTBUG-133526](https://bugreports.qt.io/browse/QTBUG-133526) Error: qmlcachegen inappropriately resolves file paths
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
* [QTBUG-133481](https://bugreports.qt.io/browse/QTBUG-133481) Top-level configure fails with neumorphicpanel example
* [QTBUG-133636](https://bugreports.qt.io/browse/QTBUG-133636) [Reg 6.7.3 -> 6.8.0] Qt StateMachine crashes during a
signal transition.
* [QTBUG-133276](https://bugreports.qt.io/browse/QTBUG-133276) qtquickview_kotlin doesn't compile
* [QTBUG-133645](https://bugreports.qt.io/browse/QTBUG-133645) Curve renderer stroke is blurry inside Qt Quick 3D scene
* [QTBUG-133461](https://bugreports.qt.io/browse/QTBUG-133461) [REG: 6.6.1 → 6.8.2] Change to singleton status of Qt
* [QTBUG-58643](https://bugreports.qt.io/browse/QTBUG-58643) QQmlListProperty has no examples of its usage
* [QTBUG-130705](https://bugreports.qt.io/browse/QTBUG-130705) QQmlListProperty is missing documentation for object /
data
* [QTBUG-133493](https://bugreports.qt.io/browse/QTBUG-133493) Extra space in qtquickview_java example
* [QTBUG-132802](https://bugreports.qt.io/browse/QTBUG-132802) qtquickview_kotlin example source value 8 is obsolete
and will be removed in a future release
* [QTBUG-119545](https://bugreports.qt.io/browse/QTBUG-119545) Document that the URL passed to Qt.createQmlObject() can
make it override existing components
* [QTBUG-123341](https://bugreports.qt.io/browse/QTBUG-123341) QML JavaScript function annotations not supported
* [QTBUG-89432](https://bugreports.qt.io/browse/QTBUG-89432) QML enum documentation should make a greater distinction
between using enums declared in C++ and declaring enums in QML
* [QTBUG-132409](https://bugreports.qt.io/browse/QTBUG-132409) QML registration macros are documented in QQmlEngine
* [QTBUG-133745](https://bugreports.qt.io/browse/QTBUG-133745) Link not shown correctly
* [QTBUG-133494](https://bugreports.qt.io/browse/QTBUG-133494) FTBFS: QtQuick DLL link error
* [QTBUG-120188](https://bugreports.qt.io/browse/QTBUG-120188) Don't use -1 to denote no individual corner radius
* [QTBUG-133460](https://bugreports.qt.io/browse/QTBUG-133460) [REG: 6.7.2 → 6.8.2] Change in binding resolution
behavior
* [QTBUG-132765](https://bugreports.qt.io/browse/QTBUG-132765) Controls Overlay item bypasses window event delivery;
Drawer bypasses ContextMenu
* [QTBUG-132461](https://bugreports.qt.io/browse/QTBUG-132461) [REG 6.8 -> 6.9] QtQmlStatusChangeListener is not a
functional interface
* [QTBUG-134035](https://bugreports.qt.io/browse/QTBUG-134035) tst_qquickdeferred crashing
* [QTBUG-131002](https://bugreports.qt.io/browse/QTBUG-131002) Add a way to disable aotstats statistics file
generations
* [QTBUG-130370](https://bugreports.qt.io/browse/QTBUG-130370) Missing docs for QML_NAMESPACE_EXTENDED()
* [QTBUG-132602](https://bugreports.qt.io/browse/QTBUG-132602) [REG 6.8 -> 6.9]Crash when invoking `destroy` on self
* [QTBUG-133587](https://bugreports.qt.io/browse/QTBUG-133587) Putting *.js file under QML_FILES and applying QTP0004
can break QML engine's ability to import module
* [QTBUG-133852](https://bugreports.qt.io/browse/QTBUG-133852) VectorImage: Scaled text elements have bad kerning
* [QTBUG-35598](https://bugreports.qt.io/browse/QTBUG-35598) QtQuick Controls TextField and TextArea miss mouse
context menu
* [QTBUG-133302](https://bugreports.qt.io/browse/QTBUG-133302) ContextMenu opened on TextField sometimes closes
immediately
* [QTBUG-133492](https://bugreports.qt.io/browse/QTBUG-133492) Issue found on Qt 6.8 variant that doesn't exist on 6.6
* [QTBUG-134053](https://bugreports.qt.io/browse/QTBUG-134053) Doc: Remove duplicate paragraph in 'Menu QML Type' and
add missing ')'
* [QTBUG-130764](https://bugreports.qt.io/browse/QTBUG-130764) Affector does not have property "velocity"?
* [QTBUG-130291](https://bugreports.qt.io/browse/QTBUG-130291) QML "instanceof" and "as" fail with "QtQuick.url" type
* [QTBUG-134043](https://bugreports.qt.io/browse/QTBUG-134043) tst_QQuickColorDialogImpl::dialogCanMoveBetweenWindows
is flaky
* [QTBUG-130791](https://bugreports.qt.io/browse/QTBUG-130791) qt_target_qml_sources cannot be subdir of
qt_add_qml_module
* [QTBUG-134087](https://bugreports.qt.io/browse/QTBUG-134087) qtquickview_java QML button signal not connected when
starting example
* [QTBUG-134274](https://bugreports.qt.io/browse/QTBUG-134274) QML LocationPermission is not a type
* [QTBUG-127098](https://bugreports.qt.io/browse/QTBUG-127098) qmllint: False positive for required property
* [QTBUG-134226](https://bugreports.qt.io/browse/QTBUG-134226) Warning about application/x-color in QtQuick Drag
* [QTBUG-134398](https://bugreports.qt.io/browse/QTBUG-134398) Qt Design Studio does not work with Qt 6.8 because of
QML caching
* [QTBUG-118454](https://bugreports.qt.io/browse/QTBUG-118454) Crash in QQuickTapHandler::setPressed() with nullptr
access
* [QTBUG-124777](https://bugreports.qt.io/browse/QTBUG-124777) QQuickTapHandler::setPressed() assumes non-null event if
not canceled
* [QTBUG-134037](https://bugreports.qt.io/browse/QTBUG-134037) FileDialog now always opens in a new window
* [QTBUG-132559](https://bugreports.qt.io/browse/QTBUG-132559) Top flaky test:
tst_qquickflickable::nestedSliderUsingTouch
* [QTBUG-
132631](https://bugreports.qt.io/browse/QTBUG-132631) tst_qquicklistview2::isCurrentItem_NoRegressionWithDelegateModelG
roups is flaky on opensuse
* [QTBUG-74050](https://bugreports.qt.io/browse/QTBUG-74050) tst_qquickshortcuts shortcuts and multiple are flaky
* [QTBUG-132647](https://bugreports.qt.io/browse/QTBUG-132647) tst_QQuickMultiPointTouchArea::nonOverlapping is flaky
on opensuse
* [QTBUG-78846](https://bugreports.qt.io/browse/QTBUG-78846) tst_qquicktextedit::mouseSelectionMode is flaky on
OpenSuse 15
* [QTBUG-118067](https://bugreports.qt.io/browse/QTBUG-118067) Flaky tests on opensuse 15.5: Parent task
* [QTBUG-132632](https://bugreports.qt.io/browse/QTBUG-132632) tst_qquicktextedit::cursorDelegate is flaky on opensuse
* [QTBUG-82282](https://bugreports.qt.io/browse/QTBUG-82282) tst_qquickmousearea::pressOneAndTapAnother is flaky on
OpenSuse 15
* [QTBUG-134247](https://bugreports.qt.io/browse/QTBUG-134247) TableView: edit delegate commit upon losing focus
* [QTBUG-134001](https://bugreports.qt.io/browse/QTBUG-134001) [iOS] The dial handle is misaligned with the circular
path of the dial
* [QTBUG-129424](https://bugreports.qt.io/browse/QTBUG-129424) iOS style: Dial handle doesn't follow groove
* [QTBUG-134442](https://bugreports.qt.io/browse/QTBUG-134442) tst_qqmlcomponent::loadFromQrc() randomly fails on QNX
* [QTBUG-134492](https://bugreports.qt.io/browse/QTBUG-134492) Thread sanitizer (TSAN) warns about data race with QSG
Scenegraph (qsgmaterial)
* [QTBUG-132931](https://bugreports.qt.io/browse/QTBUG-132931) QJSEngine leaks memory
* [QTBUG-133886](https://bugreports.qt.io/browse/QTBUG-133886) Regression in 6.9: Hover in ComboBox broken with
ApplicationWindow
* [QTBUG-67368](https://bugreports.qt.io/browse/QTBUG-67368) QJSValue::strictlyEquals documentation error
* [QTBUG-134688](https://bugreports.qt.io/browse/QTBUG-134688) Aliases of properties of bindables don't emit change
signals
* [QTBUG-134725](https://bugreports.qt.io/browse/QTBUG-134725) Mark QQC2 fusion style as a dependency for macos style
* [QTBUG-132763](https://bugreports.qt.io/browse/QTBUG-132763) Regression: keyboard navigation jumps to main view when
drawer is open
* [QTBUG-130116](https://bugreports.qt.io/browse/QTBUG-130116) Broken accessibility tree in (at least) certain lists
* [QTBUG-132886](https://bugreports.qt.io/browse/QTBUG-132886) qmlformat: The colon in the switch statement is in the
wrong position.
* [QTBUG-119404](https://bugreports.qt.io/browse/QTBUG-119404) QmlFormat: add spaces after js class methods
* [QTBUG-133316](https://bugreports.qt.io/browse/QTBUG-133316) qmldom/qmlformat: Comments are broken in certain
positions
* [QTBUG-123386](https://bugreports.qt.io/browse/QTBUG-123386) QmlFormat. Incorrect handling of some comments
* [QTBUG-134781](https://bugreports.qt.io/browse/QTBUG-134781) qmlls: lints out-of-date versions of files in the linter
* [QTBUG-134664](https://bugreports.qt.io/browse/QTBUG-134664) FAIL!  :
tst_examples::examples(examples/quick/multieffect/testbed/qml/main.qml)
Received a fatal error
* [QTBUG-127107](https://bugreports.qt.io/browse/QTBUG-127107) qmllint does not warn about redeclaration of JS
variables
* [QTBUG-122043](https://bugreports.qt.io/browse/QTBUG-122043) The button appears to be pressed twice, even if it's
pressed only once while you are pressing another button at the same time
on the Android app
* [QTBUG-133424](https://bugreports.qt.io/browse/QTBUG-133424) Named platform icons are blurry on macOS when displayed
with IconImage/IconLabel
* [QTBUG-135039](https://bugreports.qt.io/browse/QTBUG-135039) Import in one component affects type resolution in
another one
* [QTBUG-135091](https://bugreports.qt.io/browse/QTBUG-135091) [qtdeclarative] Cannot configure manual tests
* [QTBUG-133564](https://bugreports.qt.io/browse/QTBUG-133564) All QML Item properties named value inappropriately send
QAccessibleValueChangeEvent
* [QTBUG-95887](https://bugreports.qt.io/browse/QTBUG-95887) tst_FlickableInterop is flaky on opensuse
* [QTBUG-122405](https://bugreports.qt.io/browse/QTBUG-122405) tst_qquickhoverhandler::window is flaky on OpenSuse
* [QTBUG-75215](https://bugreports.qt.io/browse/QTBUG-75215) tst_qquickapplication::active() is flaky on opensuse
* [QTBUG-123550](https://bugreports.qt.io/browse/QTBUG-123550) Top flaky test: tst_qquickapplication::active on
openSUSE_15_5 X86_64.
* [QTBUG-122031](https://bugreports.qt.io/browse/QTBUG-122031) tst_qquickapplication::state() is flaky on opensuse
* [QTBUG-135288](https://bugreports.qt.io/browse/QTBUG-135288) qmlsc: crash on if + for
* [QTBUG-134887](https://bugreports.qt.io/browse/QTBUG-134887) [REG 6.9 -> 6.10] qmllint: bogus required property
warning with generalized grouped property
* [QTBUG-133832](https://bugreports.qt.io/browse/QTBUG-133832) QQuickWidget Segmentation Fault in setSource
* [QTBUG-135387](https://bugreports.qt.io/browse/QTBUG-135387) Division by zero when changing path elements of
ShapePath imperatively
* [QTBUG-134903](https://bugreports.qt.io/browse/QTBUG-134903) Duplicate context menus when using custom context Menus
in text controls
* [QTBUG-134215](https://bugreports.qt.io/browse/QTBUG-134215) [Reg 5 -> 6] Referencing `arguments` in arrow function
leads to segfault
* [QTBUG-135370](https://bugreports.qt.io/browse/QTBUG-135370) Replace QAbstractListModel with QQuickFolderListModel in
Component Casting
* [QTBUG-135740](https://bugreports.qt.io/browse/QTBUG-135740) Quick dialogs and templates to compile when draganddrop
feature is disabled
* [QTBUG-135649](https://bugreports.qt.io/browse/QTBUG-135649) qmlcachegen reaches Q_UNREACHABLE
* [QTBUG-129329](https://bugreports.qt.io/browse/QTBUG-129329) QML Preview doesn't update properly
* [QTBUG-135475](https://bugreports.qt.io/browse/QTBUG-135475) QML Plugin Example shows a blank window
* [QTBUG-135437](https://bugreports.qt.io/browse/QTBUG-135437) code snippet doesn't build due to a function reference
from inside Component
* [QTBUG-135279](https://bugreports.qt.io/browse/QTBUG-135279) FTBFS libc++abi: terminating due to uncaught exception
of type std::runtime_error: file is already signed. pass -f to sign
regardless
* [QTBUG-134911](https://bugreports.qt.io/browse/QTBUG-134911) Regression: C++ generated from QML throws compiler
warning (declaration of unit vs. global declaration)
* [QTBUG-134778](https://bugreports.qt.io/browse/QTBUG-134778) Binding: short syntax broken with ComponentBehavior:
Bound
* [QTBUG-135200](https://bugreports.qt.io/browse/QTBUG-135200) QQ4A example documentation does not point where to find
the examples
* [QTBUG-134726](https://bugreports.qt.io/browse/QTBUG-134726) line break is unspported
* [QTBUG-135815](https://bugreports.qt.io/browse/QTBUG-135815) QSG wrongly batches QSGGeometryNodes with different
lineWidth
* [QTBUG-134782](https://bugreports.qt.io/browse/QTBUG-134782) Binding: Documentation should point to multiple bindings
with new syntax
* [QTBUG-135342](https://bugreports.qt.io/browse/QTBUG-135342) qmlcachegen crashes in QQmlJSTypeResolver::genericType
* [QTBUG-134405](https://bugreports.qt.io/browse/QTBUG-134405) Fix QtQuickView multi-view examples
* [QTBUG-135980](https://bugreports.qt.io/browse/QTBUG-135980) error: 'O_RDONLY' was not declared in this scope
* [QTBUG-135367](https://bugreports.qt.io/browse/QTBUG-135367) Compiler warning in qmlcachegen generated code
* [QTBUG-134772](https://bugreports.qt.io/browse/QTBUG-134772) Occasional crashs on debug service rampdowns
* [QTBUG-134206](https://bugreports.qt.io/browse/QTBUG-134206) Using ListElement with QML Type Compiler leads to link
errors
* [QTBUG-134922](https://bugreports.qt.io/browse/QTBUG-134922) [REG 6.7 → 6.8] Regression with Qml Binding type
(destruction) in 6.8
* [QTBUG-135334](https://bugreports.qt.io/browse/QTBUG-135334) [Reg 6.4 -> 6.5] qmlRegisterSingletonInstance does not
work with importPath over http
* [QTBUG-135965](https://bugreports.qt.io/browse/QTBUG-135965) Application freezes when trigger an Action's shortcut in
sub-sub Menu
* [QTBUG-135975](https://bugreports.qt.io/browse/QTBUG-135975) Hover event delivery causes memory leak
* [QTBUG-134790](https://bugreports.qt.io/browse/QTBUG-134790) QML AnchorChanges do not compile in strict mode
* [QTBUG-135946](https://bugreports.qt.io/browse/QTBUG-135946) Allow configuring without quicktemplates2-hover feature
* [QTCREATORBUG-32634](https://bugreports.qt.io/browse/QTCREATORBUG-32634) Autocompletion for enum doesn't work without
restarting qml language server
* [QTBUG-136031](https://bugreports.qt.io/browse/QTBUG-136031) MouseArea in a ApplicationWindow's background can not be
hovered since 6.9.0
* [QTBUG-136120](https://bugreports.qt.io/browse/QTBUG-136120) Qml Runtime fails to correct escape -a after --
* [QTBUG-127913](https://bugreports.qt.io/browse/QTBUG-127913) QQuickTextNodeEngine renders
QChar::ObjectReplacementCharacter at low-DPI
* [QTBUG-136008](https://bugreports.qt.io/browse/QTBUG-136008) [REG: 6.8.2 -> 6.9] False warning about missing required
property when using inline component
* [QTBUG-135244](https://bugreports.qt.io/browse/QTBUG-135244) qmlcachegen takes a long time to compile
fluentwinui3/Slider.qml
* [QTBUG-136058](https://bugreports.qt.io/browse/QTBUG-136058) [Reg] qmllint: mix up between required properties
* [QTBUG-134606](https://bugreports.qt.io/browse/QTBUG-134606) eventPoint documentation is hard to read
* [QTBUG-136142](https://bugreports.qt.io/browse/QTBUG-136142) QQmlTableModel is not notifying about changes of its
data
* [QTBUG-136127](https://bugreports.qt.io/browse/QTBUG-136127) Crash when calling Object.value() on QQmlListModel
* [QTBUG-136250](https://bugreports.qt.io/browse/QTBUG-136250) TextEditor example: can't set multiple font attributes
at the same time
* [QTBUG-135457](https://bugreports.qt.io/browse/QTBUG-135457) [REG 6.8 → 6.9] ninja fails every time in every build
* [QTBUG-136253](https://bugreports.qt.io/browse/QTBUG-136253) Menu key on Windows doesn't open the context menu on the
focused item
* [QTBUG-136491](https://bugreports.qt.io/browse/QTBUG-136491) [Regression] Binary fails to link when using
qt_target_qml_sources
* [QTBUG-136248](https://bugreports.qt.io/browse/QTBUG-136248) Crash in QQmlPrivate::callQObjectMethod
* [QTBUG-53863](https://bugreports.qt.io/browse/QTBUG-53863) tst_QQuickListView::populateTransitions(static, no
populate) crashes randomly
* [QTBUG-136256](https://bugreports.qt.io/browse/QTBUG-136256) When menu items are dynamically added to Menu, it should
resize to fit
* [QTBUG-136735](https://bugreports.qt.io/browse/QTBUG-136735) Line: 1: Internal process (QML Puppet) crashed.
* [QTBUG-136552](https://bugreports.qt.io/browse/QTBUG-136552) QMLLS crashes
* [QTBUG-136192](https://bugreports.qt.io/browse/QTBUG-136192) qmlformat fails to write file
* [QTBUG-128864](https://bugreports.qt.io/browse/QTBUG-128864) Vulkan RHI Renderer freezes on Windows sometimes after
pressing Win-D
* [QTBUG-136672](https://bugreports.qt.io/browse/QTBUG-136672) QQuickComboBox::setModel() does an unguarded
qvariant_cast on the previous value
* [QTBUG-133858](https://bugreports.qt.io/browse/QTBUG-133858) tst_QQuickMenu::contextMenuKeyboard is flaky
* [QTBUG-136354](https://bugreports.qt.io/browse/QTBUG-136354) DragHandler doesn't account for scene changes when
calculating threshold
* [QTBUG-135286](https://bugreports.qt.io/browse/QTBUG-135286) Qml Property Cache heap-use-after-free
* [QTBUG-136797](https://bugreports.qt.io/browse/QTBUG-136797) QJSEngine::throwError(QJSValue) with a string value
becomes "undefined" in JS
* [QTBUG-132512](https://bugreports.qt.io/browse/QTBUG-132512) QtQuickView does not listen to Qt.quit() signal
* [QTBUG-136933](https://bugreports.qt.io/browse/QTBUG-136933) Can't build QtQ4A examples from command line
* [QTBUG-134880](https://bugreports.qt.io/browse/QTBUG-134880) Disable edge-to-edge feature of Android 15 on
qtquickview examples
* [QTBUG-117300](https://bugreports.qt.io/browse/QTBUG-117300) qmllint does not warn about enum with the same name as
their value
* [QTBUG-136581](https://bugreports.qt.io/browse/QTBUG-136581) [REG 6.5.3 -> 6.8.3] ListModel set() on existing index
fails if setting data retrieved from C++ QVariantMap containing a
QVariantList role
* [QTBUG-136969](https://bugreports.qt.io/browse/QTBUG-136969) qsvgvisitorimpl.cpp:1154:40: error: comparison of
integers of different signs
* [QTBUG-96580](https://bugreports.qt.io/browse/QTBUG-96580) Missing documentation for QSGRenderNode::RenderState
* [QTBUG-137072](https://bugreports.qt.io/browse/QTBUG-137072) [REG: 6.8 → 6.9] QMetaType::metaObject crashes the
program
* [QTBUG-133793](https://bugreports.qt.io/browse/QTBUG-133793) QT_QML_GENERATE_QMLLS_INI doesn't update file if build
directory changes
* [QTBUG-136947](https://bugreports.qt.io/browse/QTBUG-136947) EventModel::repopulate() missing endResetModel() on
early return in eventcalendar example
* [QTBUG-137086](https://bugreports.qt.io/browse/QTBUG-137086) [Reg 6.2 -> 6.5] Crashing QML code
* [QTBUG-135158](https://bugreports.qt.io/browse/QTBUG-135158) Quick Popup window can no longer have negative x on
Wayland
* [QTBUG-136439](https://bugreports.qt.io/browse/QTBUG-136439) No more possible to use a Loader for QML hot/live
reloading since Qt 6.8.3
* [QTBUG-137110](https://bugreports.qt.io/browse/QTBUG-137110) [Reg 6.8 -> 6.9] qmllint: Assert in type propagator
* [QTBUG-136810](https://bugreports.qt.io/browse/QTBUG-136810) crash on qml cache checksum mismatch
* [QTBUG-137124](https://bugreports.qt.io/browse/QTBUG-137124) Remove irrelevant images from Qt QML
* [QTBUG-133314](https://bugreports.qt.io/browse/QTBUG-133314) Artifacts in rounded rectangle corners with borders
using software backend
* [QTBUG-136738](https://bugreports.qt.io/browse/QTBUG-136738) [Software renderer] Rectangle with e.g. topLeftRadius
set corner drawn black
* [QTBUG-136699](https://bugreports.qt.io/browse/QTBUG-136699) Unexpected removal of enabled binding when parent
enabled is toggled off
* [QTBUG-132644](https://bugreports.qt.io/browse/QTBUG-132644) Cannot receive mouse move events when modal dialog is
open
* [QTBUG-134545](https://bugreports.qt.io/browse/QTBUG-134545) Mouse move and touch update events are not delivered
correctly when there are modal dialogs
* [QTBUG-137285](https://bugreports.qt.io/browse/QTBUG-137285) FAIL!  : tst_QQuickApplicationWindow::implicitFill()
Compared doubles are not the same (fuzzy compare)
* [QTBUG-137256](https://bugreports.qt.io/browse/QTBUG-137256) qmllint warns about missing-type for properties of type
QVector<EnumClass>
* [QTBUG-116675](https://bugreports.qt.io/browse/QTBUG-116675) QQuickWindow::grabWindow renders too small on macOS
retina
* [QTBUG-137350](https://bugreports.qt.io/browse/QTBUG-137350) weatherforecast example crashes when clicking quickly
* [QTBUG-137035](https://bugreports.qt.io/browse/QTBUG-137035) qmllint gets stuck
* [QTBUG-134403](https://bugreports.qt.io/browse/QTBUG-134403) QtQuick Rectangle: Gradient not displayed when the color
property is set to transparent.
* [QTBUG-135795](https://bugreports.qt.io/browse/QTBUG-135795) QML Locale cannot be compiled in Direct Mode
* [QTBUG-134099](https://bugreports.qt.io/browse/QTBUG-134099) [REG 6.7.3->6.8]Global position for QHoverEvent issued
from a QQuickItem inside a QQuickWidget is wrong.
* [QTBUG-134635](https://bugreports.qt.io/browse/QTBUG-134635) A floating-point precision error with the slider value.
* [QTBUG-137411](https://bugreports.qt.io/browse/QTBUG-137411) [REG 6.9.0 -> 6.9.1] Building for iOS failed:
qmlcachegen segmentation fault
* [QTBUG-137196](https://bugreports.qt.io/browse/QTBUG-137196) qmlcachegen crashes in QQmlJSScope::filePath
* [QTBUG-136998](https://bugreports.qt.io/browse/QTBUG-136998) qmllint crashes when checking  required properties
* [QTBUG-136492](https://bugreports.qt.io/browse/QTBUG-136492) TreeView: Editable and non-editable items not working
correctly
* [QTBUG-137413](https://bugreports.qt.io/browse/QTBUG-137413) [REG 6.9.0 -> 6.9.1] qmlformat crashes on musl
* [QTBUG-132703](https://bugreports.qt.io/browse/QTBUG-132703) Unify spelling of Qt Qml modules
* [QTBUG-133924](https://bugreports.qt.io/browse/QTBUG-133924) IconLabel children are positioned under Icon & text
* [QTBUG-135295](https://bugreports.qt.io/browse/QTBUG-135295) [Reg 5.15 -> 6.8] Binding crashes when combined with
StackView and Loader
* [QTBUG-131886](https://bugreports.qt.io/browse/QTBUG-131886) Wrong delta threshold for MultiPointTouchArea using
scale
* [QTBUG-112355](https://bugreports.qt.io/browse/QTBUG-112355) ShaderEffectSource with recursive shader causes magenta
texture on Apple Silicon
* [QTBUG-135255](https://bugreports.qt.io/browse/QTBUG-135255) The type compiler incorrectly gives a warning about
insufficient annotation for enum types.
* [QTBUG-137469](https://bugreports.qt.io/browse/QTBUG-137469) "Cannot assign object to list property" error message
isn't descriptive enough
* [QTBUG-137561](https://bugreports.qt.io/browse/QTBUG-137561) FAIL!  : tst_QQuickColorDialogImpl::defaults() Received
a warning that resulted in a failure
* [QTBUG-130683](https://bugreports.qt.io/browse/QTBUG-130683) QtQuick.Controls: Native Tooltip size on macOS
* [QTBUG-137705](https://bugreports.qt.io/browse/QTBUG-137705) qmlls: lazy QmlFile in DOM loads with incorrect import
path
* [QTBUG-94147](https://bugreports.qt.io/browse/QTBUG-94147) QSGGeometryNode docs snippet shows Qt 6 incompatible code
* [QTBUG-137416](https://bugreports.qt.io/browse/QTBUG-137416) FAIL!  : tst_QQuickFileDialogImpl::defaults() Compared
values are not the same
* [QTBUG-122738](https://bugreports.qt.io/browse/QTBUG-122738) QtQuick.Dialogs FileDialog bad color with macOS dark
theme
* [QTBUG-134704](https://bugreports.qt.io/browse/QTBUG-134704) tst_QQuickOverlay::pressedAndReleased is flaky on
opensuse
* [QTBUG-132607](https://bugreports.qt.io/browse/QTBUG-132607) Unexpected text's rectangle behavior in a row
* [QTBUG-137005](https://bugreports.qt.io/browse/QTBUG-137005) Qt6::qmltestrunner target no longer available
* [QTBUG-137577](https://bugreports.qt.io/browse/QTBUG-137577) CMake Configuration of user project fails
* [QTBUG-137115](https://bugreports.qt.io/browse/QTBUG-137115) [REG 6.5 → 6.8] Issue with inline components and setData
* [QTBUG-134600](https://bugreports.qt.io/browse/QTBUG-134600) FileDialog's currentFolder shows regression on Debian
* [QTBUG-137054](https://bugreports.qt.io/browse/QTBUG-137054) qmlls: Invalid color "transparent"
* [QTBUG-81803](https://bugreports.qt.io/browse/QTBUG-81803) QML TextInput - Incorrect behavior when all text is
selected and ctrl+backspace is pressed
* [QTBUG-137323](https://bugreports.qt.io/browse/QTBUG-137323) Flickable jump back when scrolling to the edge in KDE
* [QTBUG-136235](https://bugreports.qt.io/browse/QTBUG-136235) Qt 6.8.3 A signal 11 (SIGSEGV) crash observed while
running qtquickview_kotlin sample application (Android 11 / API 30 )
* [QTBUG-137540](https://bugreports.qt.io/browse/QTBUG-137540) [Reg 6.5.0 -> 6.5.5] Compilation blog post example
doesn't work anymore
* [QTBUG-137877](https://bugreports.qt.io/browse/QTBUG-137877) PrototypeChainCycle confuses Qt Design Studio project
storage
* [QTBUG-127863](https://bugreports.qt.io/browse/QTBUG-127863) DragHandler Activates When Dragging Starts Outside the
Item and Moves Inside
* [QTBUG-137328](https://bugreports.qt.io/browse/QTBUG-137328) [Reg 6.7 -> 6.9] QJSEngine: created JavaScript objects
does not have function hasOwnProperty
* [QTBUG-104829](https://bugreports.qt.io/browse/QTBUG-104829) QML TextArea doesn't trigger onCursorPositionChanged
when deleting whole word
* [QTBUG-137270](https://bugreports.qt.io/browse/QTBUG-137270) QML: model-views: bindings evaluate after item/app
destruction -> crashes
* [QTBUG-134208](https://bugreports.qt.io/browse/QTBUG-134208) Mnemonic annotation is passed to screen readers
* [QTBUG-137030](https://bugreports.qt.io/browse/QTBUG-137030) Assertion in qmllint
* [QTBUG-124157](https://bugreports.qt.io/browse/QTBUG-124157) QJSEngine crashes when evaluating arithmetic operation
on array with self referencing
* [QTBUG-138053](https://bugreports.qt.io/browse/QTBUG-138053) qqmlprivate compile issue with nvcc
* [QTBUG-137326](https://bugreports.qt.io/browse/QTBUG-137326) [Reg 5.15 -> 6.2] Crash in
QQmlAbstractBinding::removeFromObject()
* [QTBUG-116539](https://bugreports.qt.io/browse/QTBUG-116539) LoggingCategory object created after property * Changed
signal
* [QTBUG-137823](https://bugreports.qt.io/browse/QTBUG-137823) Tab order does not follow visual order
* [QTBUG-118188](https://bugreports.qt.io/browse/QTBUG-118188) QML evaluates bindings after destruction, possibly
resulting in segmentation faults
* [QTBUG-106900](https://bugreports.qt.io/browse/QTBUG-106900) QML Color type docs missing first few words
* [QTBUG-134936](https://bugreports.qt.io/browse/QTBUG-134936) Improve imperative Menu API documentation
* [QTBUG-133256](https://bugreports.qt.io/browse/QTBUG-133256) Crash on dynamically removing items from a custom
QtQuick.Controls.Container with transitions
* [QTBUG-46798](https://bugreports.qt.io/browse/QTBUG-46798) Destroying an item crashes ListView
* [QTBUG-136455](https://bugreports.qt.io/browse/QTBUG-136455) Doc: Some QML methods are missing their return value
types
* [QTBUG-49481](https://bugreports.qt.io/browse/QTBUG-49481) Documentation about 'Attached properties' is confused
* [QTBUG-138216](https://bugreports.qt.io/browse/QTBUG-138216) Errors in English language QML TreeView documentation
* [QTBUG-94965](https://bugreports.qt.io/browse/QTBUG-94965) FontDialog documentation improvements
* [QTBUG-138174](https://bugreports.qt.io/browse/QTBUG-138174) Lightning Viewer: runtime warnings
* [QTBUG-138357](https://bugreports.qt.io/browse/QTBUG-138357) Documentation for qt_add_qml_module misses information
about find_package
* [QTBUG-72208](https://bugreports.qt.io/browse/QTBUG-72208) Qt.labs.calendar onClicked date is one day off.
* [QTBUG-138233](https://bugreports.qt.io/browse/QTBUG-138233) declarative_ui::MapItems::test_drag() Compared values
are not the same
* [QTBUG-138200](https://bugreports.qt.io/browse/QTBUG-138200) iOS Style: Wrong palette colors when switching color
scheme from application
* [QTBUG-138346](https://bugreports.qt.io/browse/QTBUG-138346) qmllint: claims binding will not update on a signal
handler (i.e. not a binding)
* [QTBUG-122436](https://bugreports.qt.io/browse/QTBUG-122436) Android a11y: Changes to Accessible.ignored and
Item.visible are not propagated to the screen reader
* [QTBUG-136959](https://bugreports.qt.io/browse/QTBUG-136959) Read-only TextEdit overrides all Shortcuts when it has
activeFocus
* [QTBUG-138391](https://bugreports.qt.io/browse/QTBUG-138391) Deep-nested QML module containing *.mjs file can cause
ambiguous import
* [QTBUG-132518](https://bugreports.qt.io/browse/QTBUG-132518) building with cmake 3.31 gives ODR violation warnings on
webassembly
* [QTBUG-127133](https://bugreports.qt.io/browse/QTBUG-127133) Why do I get warning "Multiple C++ types called xxx
found! This violates the One Definition Rule"
* [QTBUG-134292](https://bugreports.qt.io/browse/QTBUG-134292) ODR warnings with static build
* [QTBUG-138242](https://bugreports.qt.io/browse/QTBUG-138242) Crash when GC is triggered during script exception
handling in StateChangeScript or ScriptAction
* [QTBUG-138349](https://bugreports.qt.io/browse/QTBUG-138349) QmlPreview does not start with import QtQuick.Controls +
Style=Basic
* [QTBUG-138171](https://bugreports.qt.io/browse/QTBUG-138171) File System Explorer: qmllint warnings
* [QTBUG-126193](https://bugreports.qt.io/browse/QTBUG-126193) Crash in XR when clicking on Slider in Android Style
* [QTBUG-137862](https://bugreports.qt.io/browse/QTBUG-137862) SearchField::currentIndex have dubious behavior
* [QTBUG-115170](https://bugreports.qt.io/browse/QTBUG-115170) [Reg 5.15 -> 6.5] qmlimportscanner does not include
module versions
* [QTBUG-54605](https://bugreports.qt.io/browse/QTBUG-54605) SignalSpy's clear() function is incorrectly documented as
causing valid to become false
* [QTBUG-77201](https://bugreports.qt.io/browse/QTBUG-77201) Documentation of QQuickItem::stackAfter/stackBefore is
wrong
* [QTBUG-120706](https://bugreports.qt.io/browse/QTBUG-120706) ScrollView::effectiveScrollBarHeight and
ScrollView::effectiveScrollbarWidth need elaboration on what exactly
"effective" mean
* [QTBUG-127955](https://bugreports.qt.io/browse/QTBUG-127955) Repeater without parent reports its count but does not
create delegates
* [QTBUG-136147](https://bugreports.qt.io/browse/QTBUG-136147) Qt Labs Platforms: Add alt texts
* [QTBUG-137939](https://bugreports.qt.io/browse/QTBUG-137939) New Qt 6.10 APIs in QSGGeometry show "since Qt 6.9"
* [QTBUG-136611](https://bugreports.qt.io/browse/QTBUG-136611) OpenGL: Layering breaks culling
* [QTBUG-138559](https://bugreports.qt.io/browse/QTBUG-138559) qt_add_qml_module: TARGET dependency causes build
failure
* [QTBUG-96350](https://bugreports.qt.io/browse/QTBUG-96350) QML: Shortcut: strange warning
* [QTBUG-136566](https://bugreports.qt.io/browse/QTBUG-136566) Qml Structured Value does not work with qml arrays
* [QTBUG-138358](https://bugreports.qt.io/browse/QTBUG-138358) QSGDefaultRectangleNode always returns invalid color
* [QTBUG-137029](https://bugreports.qt.io/browse/QTBUG-137029) Qmllint as process on Windows do not populate error
channel unless called in terminal.
* [QTBUG-138532](https://bugreports.qt.io/browse/QTBUG-138532) qmllint: unterminated-case
* [QTBUG-133267](https://bugreports.qt.io/browse/QTBUG-133267) Curve renderer does not always show latest version of
path data
* [QTBUG-138602](https://bugreports.qt.io/browse/QTBUG-138602) Reg[6.9->6.10]Application toolbar turns black
* [QTBUG-138749](https://bugreports.qt.io/browse/QTBUG-138749) Qt.uiLanguage is flagged by qmllint with [stale-
property-read] warning
* [QTBUG-137860](https://bugreports.qt.io/browse/QTBUG-137860) [Windows][A11y] Text can not be selected by NVDA
* [QTBUG-138515](https://bugreports.qt.io/browse/QTBUG-138515) qmllint gets type of root id wrong
* [QTBUG-136688](https://bugreports.qt.io/browse/QTBUG-136688) QJSEngine: call eval() directly from C++ crash
application
* [QTBUG-136355](https://bugreports.qt.io/browse/QTBUG-136355) Disabling qml-locale can segfault qmltc
* [QTBUG-138871](https://bugreports.qt.io/browse/QTBUG-138871) ASSERT: QColorOutput::colorify: "It makes no sense to
attempt to print an empty string."
* [QTBUG-136598](https://bugreports.qt.io/browse/QTBUG-136598) Item::enabled behaves inconsistently with docs on Qt 6
* [QTBUG-30801](https://bugreports.qt.io/browse/QTBUG-30801) Button: tooltip not shown when the button is disabled
* [QTBUG-138478](https://bugreports.qt.io/browse/QTBUG-138478) TapHandler doesn't react to touch input inside popup
background
* [QTBUG-138899](https://bugreports.qt.io/browse/QTBUG-138899) [REG 6.10.0 beta2 -> beta3] quickcontrols/spreadsheets
not compiling
* [QTBUG-138927](https://bugreports.qt.io/browse/QTBUG-138927) Incubator crashing when being destroyed
* [QTBUG-133247](https://bugreports.qt.io/browse/QTBUG-133247) Fill not correctly rendered by curve renderer
* [QTBUG-133313](https://bugreports.qt.io/browse/QTBUG-133313) "Invalid import qualifier ID" message doesn't say why
it's invalid
* [QTBUG-137733](https://bugreports.qt.io/browse/QTBUG-137733) quick/flexboxLayouts launch fails
* [QTBUG-138490](https://bugreports.qt.io/browse/QTBUG-138490) Incorrect item ordering in QML container when the
ListView is nested within another Item.
* [QTBUG-123988](https://bugreports.qt.io/browse/QTBUG-123988) QSGGeometryData::hasDirtyIndexData() implementation uses
wrong member variable
* [QTBUG-123985](https://bugreports.qt.io/browse/QTBUG-123985) PinchHandler works unreliably with Wayland
* [QTBUG-138516](https://bugreports.qt.io/browse/QTBUG-138516) [Reg 6.8 -> 6.9] QML: compiler: methods crash in
(nested) QQmlPrivate::callArrowFunction
* [QTBUG-139093](https://bugreports.qt.io/browse/QTBUG-139093) Lancelot baseline test fails for SearchField
* [QTBUG-138028](https://bugreports.qt.io/browse/QTBUG-138028) TextField with placeholder text strange behavior with
Binding
* [QTBUG-94251](https://bugreports.qt.io/browse/QTBUG-94251) tst_QQuickPopup fails with OpenSUSE 15.3
* [QTBUG-139104](https://bugreports.qt.io/browse/QTBUG-139104) qmlls crash when opening a qmltypes file
* [QTBUG-138001](https://bugreports.qt.io/browse/QTBUG-138001) Doc: Inconsistency in QML Layout inheritance tree
* [QTBUG-78162](https://bugreports.qt.io/browse/QTBUG-78162) tst_qquicktextinput::mouseSelectionMode() is flaky on
OpenSuse 15.0
* [QTBUG-139304](https://bugreports.qt.io/browse/QTBUG-139304) QML text with heading role is not read by screenreader
* [QTBUG-138219](https://bugreports.qt.io/browse/QTBUG-138219) Doc Issues with Qt Quick for Android Studio Projects
* [QTBUG-78261](https://bugreports.qt.io/browse/QTBUG-78261) tst_focus::policy is failing
* [QTBUG-139583](https://bugreports.qt.io/browse/QTBUG-139583) FAIL!  : tst_QQuickApplicationWindow::layout()
* [QTBUG-139309](https://bugreports.qt.io/browse/QTBUG-139309) REG: Material Slider's hovered effects visible when they
shouldn't be
* [QTBUG-137160](https://bugreports.qt.io/browse/QTBUG-137160) qt quick Loader active=false with unfinished Menu crash
* [QTBUG-139552](https://bugreports.qt.io/browse/QTBUG-139552) tst_qquickmenu: Test case loadMenuAsynchronously fails
due to warning
* [QTBUG-139626](https://bugreports.qt.io/browse/QTBUG-139626) AOT-compiled code crashes when accessing members of
QList<QVariantMap>
* [QTBUG-139633](https://bugreports.qt.io/browse/QTBUG-139633) Doc: Synchronizer should have \since 6.10
* [QTBUG-129972](https://bugreports.qt.io/browse/QTBUG-129972) [REG 6.6 → 6.7] Array returned to QML from CPP is not
retaining changes made in QML/JS
* [QTBUG-139025](https://bugreports.qt.io/browse/QTBUG-139025) [Reg 6.5.9 -> 6.8.4] Lists of objects with
JavaScriptOwnership, stored in var properties, are no longer destroyed
* [QTBUG-139059](https://bugreports.qt.io/browse/QTBUG-139059) Generated code does not track objects on JavaScript
stack
* [QTBUG-138919](https://bugreports.qt.io/browse/QTBUG-138919) [Reg 6.5.9 -> 6.8.4] Unreferenced objects with
JavaScriptOwnership are no longer destroyed
* [QTBUG-139306](https://bugreports.qt.io/browse/QTBUG-139306) Popup inside an async Loader crashes Qt Quick app if
there is direct property binding (possible racing condition)
* [QTBUG-135249](https://bugreports.qt.io/browse/QTBUG-135249) Popup: Some properties can not be bound
* [QTBUG-100259](https://bugreports.qt.io/browse/QTBUG-100259) tst_controls crash on Android
* [QTBUG-100258](https://bugreports.qt.io/browse/QTBUG-100258) tst_focus crashes on Android
* [QTBUG-139415](https://bugreports.qt.io/browse/QTBUG-139415) tst_controls has failing test cases
* [QTBUG-138886](https://bugreports.qt.io/browse/QTBUG-138886) Improve "once-off assignment" wording in QML
PropertyChanges documentation
* [QTBUG-139781](https://bugreports.qt.io/browse/QTBUG-139781) Issues with SortFilterProxyModel docs
* [QTBUG-123106](https://bugreports.qt.io/browse/QTBUG-123106) Documentation - Linking of QtQuickView STATUS_READY,
STATUS_NULL etc.. in docs
* [QTBUG-135474](https://bugreports.qt.io/browse/QTBUG-135474) QtQuickView Android class docs miss QtQmlStatus ?
* [QTBUG-140057](https://bugreports.qt.io/browse/QTBUG-140057)  ASSERT: "locals" in file
/Users/qt/work/qt/qtdeclarative/src/qml/memory/qv4mm.cpp, line 1487
* [QTBUG-137829](https://bugreports.qt.io/browse/QTBUG-137829) Don't allow yoga library symbols exposed from QT
libraries (either static / dynamic)
* [QTBUG-140026](https://bugreports.qt.io/browse/QTBUG-140026) TreeModel and TreeViewDelegate don't cooperate
* [QTBUG-136958](https://bugreports.qt.io/browse/QTBUG-136958) [QuickControls] Highlight of the controls is square
instead of round
* [QTBUG-131898](https://bugreports.qt.io/browse/QTBUG-131898) Moving the window sometimes crashes the application
* [QTCREATORBUG-31897](https://bugreports.qt.io/browse/QTCREATORBUG-31897) simplify qmlls setup / make it work out of the box
* [QTCREATORBUG-31823](https://bugreports.qt.io/browse/QTCREATORBUG-31823) Annotations and CodeCompletion is wrong or not
working
* [QTBUG-132075](https://bugreports.qt.io/browse/QTBUG-132075) tst_qquicktext::multilengthStrings(Wrap) Compared
doubles are not the same (fuzzy compare)
* [QTBUG-101704](https://bugreports.qt.io/browse/QTBUG-101704) ToolTip calculates its width incorrectly
* [QTBUG-131647](https://bugreports.qt.io/browse/QTBUG-131647) Q_PROPERTY REQUIRED has no effect on components loaded
directly from C++ API
* [QTBUG-132345](https://bugreports.qt.io/browse/QTBUG-132345) [Reg 6.5 -> 6.8] qmlcachegen miscompiles number
coercions
* [QTBUG-132275](https://bugreports.qt.io/browse/QTBUG-132275) timeout in tst_imagine
* [QTBUG-131916](https://bugreports.qt.io/browse/QTBUG-131916) Quoting and QML files with white spaces in the path are
not supported in qmldir
* [QTBUG-132387](https://bugreports.qt.io/browse/QTBUG-132387) FAIL!  : tst_qqmlengine::uiLanguage() Not all expected
messages were received
* [QTBUG-132436](https://bugreports.qt.io/browse/QTBUG-132436) Context menu fails to open on Windows in CI
* [QTBUG-130087](https://bugreports.qt.io/browse/QTBUG-130087) QML Compiler statistics doesn't shows all modules
* [QTBUG-132591](https://bugreports.qt.io/browse/QTBUG-132591) tst_QQmlInspector::connect(rectangle/unrestricted)
Received a fatal error
* [QTBUG-132650](https://bugreports.qt.io/browse/QTBUG-132650) tst_qquicktextedit::overwriteMode is flaky on opensuse
* [QTBUG-132651](https://bugreports.qt.io/browse/QTBUG-132651) tst_qquicktextedit::keyboardSelection is flaky on
opensuse
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
* [QTBUG-132073](https://bugreports.qt.io/browse/QTBUG-132073) Not possible to use ContextMenu on event-consuming types
like Pane
* [QTBUG-124913](https://bugreports.qt.io/browse/QTBUG-124913) Weird compiler warning message when using unresolved
function
* [QTBUG-130374](https://bugreports.qt.io/browse/QTBUG-130374) tst_qquicktextedit is flaky on Linux
* [QTBUG-131894](https://bugreports.qt.io/browse/QTBUG-131894) qtranslator loads wrong locale
* [QTCREATORBUG-32198](https://bugreports.qt.io/browse/QTCREATORBUG-32198) The wrong breakpoint source URL can be sent to the
QML debugger
* [QTBUG-132789](https://bugreports.qt.io/browse/QTBUG-132789)  Killed process: No output received (timeout: 15m0s
seconds)
* [QTBUG-133530](https://bugreports.qt.io/browse/QTBUG-133530) Several Controls tests failing after test coverage
restored
* [QTBUG-133725](https://bugreports.qt.io/browse/QTBUG-133725) qml_tool_autogen target loses almost all dependencies on
other autogen and sync_headers targets
* [QTBUG-87776](https://bugreports.qt.io/browse/QTBUG-87776) Move Qt::FooPrivate targets into separate CMake packages
* [QTBUG-130879](https://bugreports.qt.io/browse/QTBUG-130879) "Failed to build texture render target for layer" error
log when using Flickable, resizeContent and layer.enabled
* [QTBUG-133305](https://bugreports.qt.io/browse/QTBUG-133305) QDeclarative crashes with PARAM_RTP_MEM_FILL=FALSE on
VxWorks
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-133961](https://bugreports.qt.io/browse/QTBUG-133961) msvc LTO: compilation failure related to
QSafeQuickItemChangeListener
* [QTBUG-134009](https://bugreports.qt.io/browse/QTBUG-134009) warnings in offscreen plugin, inherited from
QPlatformWindow
* [QTBUG-134269](https://bugreports.qt.io/browse/QTBUG-134269) Attached properties using REVISION produce error
* [QTBUG-128649](https://bugreports.qt.io/browse/QTBUG-128649) Document that files belonging to a QML module have to be
in that QML module's directory.
* [QTBUG-115926](https://bugreports.qt.io/browse/QTBUG-115926) WASM: In the QML Accessibility demo application, menu
items are not getting focus.
* [QTBUG-110243](https://bugreports.qt.io/browse/QTBUG-110243) Resources are lost when linking static libraries using
CMake build system in a separate project
* [QTBUG-134250](https://bugreports.qt.io/browse/QTBUG-134250) qdoc fails to report warnings for incorrect \fn
signatures
* [QTBUG-129947](https://bugreports.qt.io/browse/QTBUG-129947) tst_QQuickTextEdit::mouseSelection() is flaky on macOS
arm 12/13
* [QTCREATORBUG-32591](https://bugreports.qt.io/browse/QTCREATORBUG-32591) qmlls still not work in qt creator
* [QTBUG-132526](https://bugreports.qt.io/browse/QTBUG-132526) Some CMake targets of private Qt modules reference non-
existent include dirs
* [QTBUG-134648](https://bugreports.qt.io/browse/QTBUG-134648) QQmlTableInstanceModel allows access to context
properties even if required properties are present
* [QTBUG-134251](https://bugreports.qt.io/browse/QTBUG-134251) Qt Quick for Android is hard to find
* [QTBUG-
134878](https://bugreports.qt.io/browse/QTBUG-134878) tst_controls::Basic::SwipeDelegate::test_removableDelegates(touch
) Received signal 10 (SIGBUS), code 1
* [QTBUG-134718](https://bugreports.qt.io/browse/QTBUG-134718) FAIL!  : tst_controls::Basic::SwipeDelegate::test_remova
bleDelegates(touch_rotation_90) Received a fatal error
* [QTBUG-125906](https://bugreports.qt.io/browse/QTBUG-125906) Flicking needs to be done horizontally to delete items
in apps that have been rotated 90°.
* [QTBUG-135020](https://bugreports.qt.io/browse/QTBUG-135020) qmllint: clean up linting categories
* [QTBUG-55000](https://bugreports.qt.io/browse/QTBUG-55000) QtQuick tests fail on highdpi screen
* [QTBUG-134768](https://bugreports.qt.io/browse/QTBUG-134768) QLocale::toStrings uses E instead of e
* [QTBUG-131478](https://bugreports.qt.io/browse/QTBUG-131478) Inconsistent behavior when changing Flickable margins
* [QTBUG-133755](https://bugreports.qt.io/browse/QTBUG-133755) tst_customization has an unusually long runtime (several
hours)
* [QTBUG-109553](https://bugreports.qt.io/browse/QTBUG-109553) CMake deployment API creates too deep directory
hierarchy when DESTDIR is set
* [QTBUG-117948](https://bugreports.qt.io/browse/QTBUG-117948) qt_generate_deploy_qml_app_script() deploys QML plugin
target but not the corresponding backing target
* [QTBUG-135164](https://bugreports.qt.io/browse/QTBUG-135164) TextArea with description and no name results in empty
a11y description
* [QTBUG-135032](https://bugreports.qt.io/browse/QTBUG-135032) Uncreatable value types behave erratically
* [QTBUG-105856](https://bugreports.qt.io/browse/QTBUG-105856) The Menu Item will continue to be highlighted after the
sub menu is closed
* [QTBUG-135944](https://bugreports.qt.io/browse/QTBUG-135944) Version string '6.9.0' found in 6.10.0 sources
* [QTBUG-136101](https://bugreports.qt.io/browse/QTBUG-136101) Minimal configuration compile with autotests
* [QTBUG-136251](https://bugreports.qt.io/browse/QTBUG-136251) TextEditor example: selection is lost when you open the
Font or Color dialog from the context menu
* [QTBUG-133752](https://bugreports.qt.io/browse/QTBUG-133752) tst_QJSEngine fails when statically linking
* [QTBUG-136447](https://bugreports.qt.io/browse/QTBUG-136447) Blacklist tst_qquickiconimage tests for Windows 11 24h2
* [QTBUG-136755](https://bugreports.qt.io/browse/QTBUG-136755) QQuickWindow::grabWindow() results in a black background
color instead of being transparent with the Offscreen platform.
* [QTBUG-136806](https://bugreports.qt.io/browse/QTBUG-136806) QtQml restores QmlIR from CompilationUnits when loading
AOT-compiled artefacts
* [QTBUG-133312](https://bugreports.qt.io/browse/QTBUG-133312) Default QML import paths conflict and can result in
crashes
* [QTBUG-135789](https://bugreports.qt.io/browse/QTBUG-135789) Build failure on macOS
* [QTBUG-87708](https://bugreports.qt.io/browse/QTBUG-87708) [Reg 5.15.0 -> 5.15.1] header's width isn't resized to
window's width when Layout is used
* [QTBUG-134800](https://bugreports.qt.io/browse/QTBUG-134800) Window.window cannot work as a target of Connections QML
in GridView/RowLayout
* [QTBUG-51285](https://bugreports.qt.io/browse/QTBUG-51285) Using nested QtQuick Layouts with spacing generates
binding loops
* [QTBUG-115140](https://bugreports.qt.io/browse/QTBUG-115140) qtdeclarative -unity-build-batch-size 100000 fails
* [QTBUG-127605](https://bugreports.qt.io/browse/QTBUG-127605) [QtQuick.Dialogs/Wayland] Native FileDialog does not
respect Qt.ApplicationModal flag
* [QTBUG-133586](https://bugreports.qt.io/browse/QTBUG-133586) F2 shortcut or Ctrl+Click in qml files sometimes leads
to build dir instead of source and sometimes does absolutly nothing
* [QTBUG-118610](https://bugreports.qt.io/browse/QTBUG-118610) ShaderEffectSource in recursive mode with multisampling
is broken
* [QTBUG-129088](https://bugreports.qt.io/browse/QTBUG-129088) Support Contrast themes in FluentWinUI3
* [QTBUG-137144](https://bugreports.qt.io/browse/QTBUG-137144) a11y: AT-SPI "Locale" Accessible property not supported
* [QTBUG-132268](https://bugreports.qt.io/browse/QTBUG-132268) SelectionRectangle is fiddly to get working by default
* [QTBUG-117526](https://bugreports.qt.io/browse/QTBUG-117526) QQuickStylePrivate::fallbackStyle has the wrong value
when using run-time style selection and the fallback style is imported
via the style's qmldir
* [QTBUG-136709](https://bugreports.qt.io/browse/QTBUG-136709) Style import triggers style change
* [QTBUG-137900](https://bugreports.qt.io/browse/QTBUG-137900) QML sslConfiguration has sslOptions propery out of sync
* [QTBUG-109279](https://bugreports.qt.io/browse/QTBUG-109279) JS array vs QVariantList mixup
* [QTBUG-137554](https://bugreports.qt.io/browse/QTBUG-137554) qml: list qml --> c++ editing crashes/has no effect
* [QTBUG-138104](https://bugreports.qt.io/browse/QTBUG-138104) tst_qtquickview_signallistener crashes on Android
* [QTBUG-133315](https://bugreports.qt.io/browse/QTBUG-133315) qmlformat can still insert extra spaces in user code
* [QTBUG-137116](https://bugreports.qt.io/browse/QTBUG-137116) Incorrect Semantic Highlighting for QML Property Chains
* [QTBUG-132108](https://bugreports.qt.io/browse/QTBUG-132108) addApplicationFontFromData behaves abnormally after
removeAllApplicationFonts.
* [QTBUG-138155](https://bugreports.qt.io/browse/QTBUG-138155) qt_generate_deploy_qml_app_script: Error for space in
output name
* [QTBUG-137946](https://bugreports.qt.io/browse/QTBUG-137946) qmllint: duplicate-property-binding
* [QTBUG-138164](https://bugreports.qt.io/browse/QTBUG-138164) Coffee Machine: qmllint warnings
* [QTBUG-138565](https://bugreports.qt.io/browse/QTBUG-138565) "Cannot generate qmltypes file" when trying to run in-
app purchase demo app on Android
* [QTBUG-138189](https://bugreports.qt.io/browse/QTBUG-138189) To Do List: qmllint warnings
* [QTBUG-138553](https://bugreports.qt.io/browse/QTBUG-138553) QmlTableModel complex types don't work as documented:
Remove setters
* [QTBUG-138703](https://bugreports.qt.io/browse/QTBUG-138703) QmlTableModel and QmlTreeModel should be merged where
possible.
* [QTBUG-138173](https://bugreports.qt.io/browse/QTBUG-138173) Lightning Viewer: qmllint warnings
* [QTBUG-138704](https://bugreports.qt.io/browse/QTBUG-138704) QmlTreeModel misses API for insertRow()
* [QTBUG-135407](https://bugreports.qt.io/browse/QTBUG-135407) [Scene Graph - Graph App] Segmentation Fault
* [QTBUG-138188](https://bugreports.qt.io/browse/QTBUG-138188) Thermostat: qmllint warnings
* [QTBUG-138901](https://bugreports.qt.io/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-139026](https://bugreports.qt.io/browse/QTBUG-139026) Scrollbar size jumps during drag due to dynamic item
heights
* [QTBUG-139211](https://bugreports.qt.io/browse/QTBUG-139211) tst_qquickpopup (Failed)
* [QTBUG-139240](https://bugreports.qt.io/browse/QTBUG-139240) qmllint should not warn about accessing properties from
QQmlPropertyMap
* [QTBUG-118532](https://bugreports.qt.io/browse/QTBUG-118532) tst_qquickpopup::doubleClickInMouseArea and overlay are
flaky on android
* [QTBUG-139688](https://bugreports.qt.io/browse/QTBUG-139688) Public Java Classes Documentation Bugs
* [QTBUG-139320](https://bugreports.qt.io/browse/QTBUG-139320) QQ4A - Buffer Overflow crash in application project
* [QTBUG-140170](https://bugreports.qt.io/browse/QTBUG-140170) [6.10 REG] ASSERT failure in QQuickWindow: "Called
object is not of the correct type (class destructor may have already
run)"

### qtactiveqt
* [QTBUG-132205](https://bugreports.qt.io/browse/QTBUG-132205) warning C4834: discarding return value of function with
[[nodiscard]] attribute
* [QTBUG-132488](https://bugreports.qt.io/browse/QTBUG-132488) TestNamespace error at Active Qt
* [QTBUG-123520](https://bugreports.qt.io/browse/QTBUG-123520) QAxObject has invalid properties that can not be set
either
* [QTBUG-134098](https://bugreports.qt.io/browse/QTBUG-134098) dumpcpp puts native Qt types inside a custom namespace
* [QTBUG-136512](https://bugreports.qt.io/browse/QTBUG-136512) [Reg 6.8.3 -> 6.9.0] dumpcpp's output is uncompilable
due to missing namespaces
* [QTBUG-137347](https://bugreports.qt.io/browse/QTBUG-137347) dumpcpp skips namespace and creates syntaxes errors
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-134902](https://bugreports.qt.io/browse/QTBUG-134902) Regression: QByteArray/string/string_view comparison
broken

### qtmultimedia
* [QTBUG-128253](https://bugreports.qt.io/browse/QTBUG-128253) List of camera devices does not update on runtime
* [QTBUG-130901](https://bugreports.qt.io/browse/QTBUG-130901) Crash on Some Android Device when using Multimedia
* [QTBUG-131785](https://bugreports.qt.io/browse/QTBUG-131785) [Boot2Qt] The media player detects 2 video tracks for
the m2v file
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
* [QTBUG-131688](https://bugreports.qt.io/browse/QTBUG-131688) Ffmpeg backend build fails if openssl 1.1 is used
* [QTBUG-128908](https://bugreports.qt.io/browse/QTBUG-128908) HLS video stream (m3u8) has glitches and delay in the
first segment
* [QTBUG-133813](https://bugreports.qt.io/browse/QTBUG-133813) Document that QML VideoOutput is a subclass of Item
* [QTBUG-133033](https://bugreports.qt.io/browse/QTBUG-133033) QMediaPlayer may crash during shutdown
* [QTBUG-134085](https://bugreports.qt.io/browse/QTBUG-134085) Cannot play recorded video on declarative-example
* [QTBUG-134090](https://bugreports.qt.io/browse/QTBUG-134090) [REG 6.9.0beta3 snapshot->6.9.0 beta3] the
-DFEATURE_gui=OFF build fails
* [QTBUG-133773](https://bugreports.qt.io/browse/QTBUG-133773) Cannot record a video with QML camera
* [QTBUG-134135](https://bugreports.qt.io/browse/QTBUG-134135) qandroidvideoframebuffer.cpp gives "error: variable
length arrays in C++ are a Clang extension" errors with NDK r27c
* [QTBUG-125238](https://bugreports.qt.io/browse/QTBUG-125238) QVideoFrame::toImage fails on Android with 16 bit per
component planar YUV formats
* [QTBUG-134046](https://bugreports.qt.io/browse/QTBUG-134046) [Android] The audiorecorder example app is crashing when
trying to record anything with disallowed permissions
* [QTBUG-134412](https://bugreports.qt.io/browse/QTBUG-134412) Fix copyAllFiles in multimediatestlib to copy
recursively
* [QTBUG-131711](https://bugreports.qt.io/browse/QTBUG-131711) QML video example: Center Box that renders camera feed
Misalign on Maximizing/Minimizing
* [QTBUG-132755](https://bugreports.qt.io/browse/QTBUG-132755) External USB webcam has incorrect rotation applied
* [QTBUG-132754](https://bugreports.qt.io/browse/QTBUG-132754) List of cameras not getting updated
* [QTBUG-133135](https://bugreports.qt.io/browse/QTBUG-133135) Paused or completed video playback freezes application
using MediaPlayer (gstreamer backend)
* [QTBUG-134937](https://bugreports.qt.io/browse/QTBUG-134937) error: no match for ‘operator==’ (operand types are
‘const std::optional<QByteArray>’ and
‘std::optional<std::basic_string_view<char> >’)
* [QTBUG-134902](https://bugreports.qt.io/browse/QTBUG-134902) Regression: QByteArray/string/string_view comparison
broken
* [QTBUG-119141](https://bugreports.qt.io/browse/QTBUG-119141) MediaPlayer-example The data of the files is editable,
but cannot be saved
* [QTBUG-135021](https://bugreports.qt.io/browse/QTBUG-135021) docs link to QVideoFrameFormat::PixelFormat goes to
wikipedia instead
* [QTBUG-135235](https://bugreports.qt.io/browse/QTBUG-135235) screencapture doesn't work any more on wayland
* [QTBUG-135043](https://bugreports.qt.io/browse/QTBUG-135043) qtmultimedia FTBFS due to a CMake error in
QtFFmpegMediaPluginImpl
* [QTBUG-123104](https://bugreports.qt.io/browse/QTBUG-123104) QAudioSource without explicitly specified QAudioFormat
is not functional
* [QTBUG-135172](https://bugreports.qt.io/browse/QTBUG-135172) FindFFmpeg.cmake doesn't look for correct libraries on
iOS
* [QTBUG-134882](https://bugreports.qt.io/browse/QTBUG-134882) QAudioDevice::isFormatSupported() not working on Android
* [QTBUG-135312](https://bugreports.qt.io/browse/QTBUG-135312) Crash in QtMultimedia pipewire
* [QTBUG-135307](https://bugreports.qt.io/browse/QTBUG-135307) Regression 6.8.2 > 6.8.3: Media player does not play mp3
* [QTBUG-122754](https://bugreports.qt.io/browse/QTBUG-122754) [windows] QML media player always uses audio stream,
even when there is no media playing
* [QTBUG-135939](https://bugreports.qt.io/browse/QTBUG-135939) qgstreameraudiooutput.cpp is missing the inclusion of
header files
* [QTBUG-135256](https://bugreports.qt.io/browse/QTBUG-135256) Camera not functioning if permission granted later
* [QTBUG-132167](https://bugreports.qt.io/browse/QTBUG-132167) QCamera: Handle AVCaptureDevice being in suspended state
* [QTBUG-128418](https://bugreports.qt.io/browse/QTBUG-128418) AudioOutput example toggles between push and pull modes
when switching device
* [QTBUG-136003](https://bugreports.qt.io/browse/QTBUG-136003) QVideoSink documentation mentions nonexistent paint()
function
* [QTBUG-129626](https://bugreports.qt.io/browse/QTBUG-129626) [ffmpeg] pc files not found when building against a
system ffmpeg
* [QTBUG-136052](https://bugreports.qt.io/browse/QTBUG-136052) VideoOutput crash with opacity animation
* [QTBUG-135360](https://bugreports.qt.io/browse/QTBUG-135360) Unexpected Qt Multimedia warning message
* [QTBUG-135911](https://bugreports.qt.io/browse/QTBUG-135911) QRhi claims to not support a working texture format.
* [QTBUG-136191](https://bugreports.qt.io/browse/QTBUG-136191) Screencapture example crashes on permission granted
* [QTBUG-136475](https://bugreports.qt.io/browse/QTBUG-136475) Maroon example crashes in Linux
* [QTBUG-136680](https://bugreports.qt.io/browse/QTBUG-136680) qt_add_ios_ffmpeg_libraries() not working with 6.9
* [QTBUG-132458](https://bugreports.qt.io/browse/QTBUG-132458) [static linking] undefined symbols for ffmpeg plugin
* [QTBUG-134196](https://bugreports.qt.io/browse/QTBUG-134196) R16 video texture formats don't have a working fallback
for GLES 2.0
* [QTBUG-137070](https://bugreports.qt.io/browse/QTBUG-137070) [REG 6.9.1 prev snapshot->6.9.1] Multimedia examples not
compiling, Wasm
* [QTBUG-136227](https://bugreports.qt.io/browse/QTBUG-136227) Crash in camera rundown
* [QTBUG-136920](https://bugreports.qt.io/browse/QTBUG-136920) Access violation on QWindowsFormatInfo construction
* [QTBUG-102716](https://bugreports.qt.io/browse/QTBUG-102716) [Windows] Access violation in QWindowsFormatInfo
* [QTBUG-137150](https://bugreports.qt.io/browse/QTBUG-137150) Assertion hit when unplugging microphone device while
recording
* [QTBUG-137308](https://bugreports.qt.io/browse/QTBUG-137308) [Reg B2Qt 6.7.3 -> 6.8.3] glupload not supported in
GStreamer pipeline
* [QTBUG-137360](https://bugreports.qt.io/browse/QTBUG-137360) Qt multimedia compilation error windows 32 bit
* [QTBUG-120693](https://bugreports.qt.io/browse/QTBUG-120693) Corrupt JPEG data
* [QTBUG-127905](https://bugreports.qt.io/browse/QTBUG-127905) Changing SoundEffect source makes the app hang
* [QTBUG-136145](https://bugreports.qt.io/browse/QTBUG-136145) Qt Spatial Audio: Add alt texts
* [QTBUG-137586](https://bugreports.qt.io/browse/QTBUG-137586) [pipewire] rare crashes on exit
* [QTBUG-137173](https://bugreports.qt.io/browse/QTBUG-137173) Windows native multimedia backend does not agree with
Windows Media Player when dealing with rotated video
* [QTBUG-136676](https://bugreports.qt.io/browse/QTBUG-136676) Linking against static FFmpeg that is built with OpenSSL
support fails
* [QTBUG-136802](https://bugreports.qt.io/browse/QTBUG-136802) Linking against static FFmpeg that has VAAPI support
enabled causes build to fail
* [QTBUG-137973](https://bugreports.qt.io/browse/QTBUG-137973) QMediaPlayer example crashing while changing audio
device output
* [QTBUG-138060](https://bugreports.qt.io/browse/QTBUG-138060) Unable to build: no type named 'lock_guard' in namespace
'std' on macos ventura
* [QTBUG-98145](https://bugreports.qt.io/browse/QTBUG-98145) Android: Avoid empty file format on the AudioRecorder app
* [QTBUG-138059](https://bugreports.qt.io/browse/QTBUG-138059) [REG 6.9.0-6.9.1] [windows] Strange Qt warning on
QAudioSource::start() when non-default sample rate is used
* [QTBUG-138197](https://bugreports.qt.io/browse/QTBUG-138197) Crash in
QtPipeWire::QAudioContextManager::handleMetadata
* [QTBUG-104515](https://bugreports.qt.io/browse/QTBUG-104515) Documentation for QML's CaptureSession lacks
camera.start() entry
* [QTBUG-138248](https://bugreports.qt.io/browse/QTBUG-138248) Crash in QtPipeWire::SpaObjectAudioFormat::parse
* [QTBUG-130636](https://bugreports.qt.io/browse/QTBUG-130636) FFmpeg: QCamera::FlashOn is unreliable
* [QTBUG-134607](https://bugreports.qt.io/browse/QTBUG-134607) Video playback crash when setting QQuickWindow
GraphicsAPI to Vulkan
* [QTBUG-138414](https://bugreports.qt.io/browse/QTBUG-138414) FFmpeg Plugin: Improve usability on different RHI
backend configurations
* [QTBUG-136151](https://bugreports.qt.io/browse/QTBUG-136151) Qt Multimedia: Add alt texts
* [QTBUG-138952](https://bugreports.qt.io/browse/QTBUG-138952) tst_qaudiosink: start_afterStopAndReset() crashes on
macOS
* [QTBUG-139549](https://bugreports.qt.io/browse/QTBUG-139549) Qt multimedia compilation error windows 32 bit
* [QTBUG-138590](https://bugreports.qt.io/browse/QTBUG-138590) Incorrect Call to QAudioOutput::setVolume
* [QTBUG-124562](https://bugreports.qt.io/browse/QTBUG-124562) Exposure compensation (setExposureCompensation) doesn't
work with the example app
* [QTBUG-139773](https://bugreports.qt.io/browse/QTBUG-139773) Crash in MediaPlayer in qtdice demo
* [QTBUG-140431](https://bugreports.qt.io/browse/QTBUG-140431) apalis-imx6: media Player example fails to play video
* [QTBUG-125956](https://bugreports.qt.io/browse/QTBUG-125956) Unit testing of new APIs
* [QTBUG-130089](https://bugreports.qt.io/browse/QTBUG-130089) Encoding to H264 fails on macOS ARM in Qt CI
* [QTBUG-132778](https://bugreports.qt.io/browse/QTBUG-132778) Error compiling multimedia examples on iOS
* [QTBUG-132087](https://bugreports.qt.io/browse/QTBUG-132087) QCamera::cameraFormat does not update correctly
* [QTBUG-127000](https://bugreports.qt.io/browse/QTBUG-127000) Incorrect frame rate when starting H264 video. Incorrect
playback stop.
* [QTBUG-133563](https://bugreports.qt.io/browse/QTBUG-133563) Omit from showing media backend info in the console
* [QTBUG-116782](https://bugreports.qt.io/browse/QTBUG-116782) FFmpeg backend: RTSP stream is very choppy in Qt,
compared to FFplay
* [QTBUG-127137](https://bugreports.qt.io/browse/QTBUG-127137) [ffmpeg, macos]
tst_QMediaPlayerBackend::stressTest_setupAndTeardown crashes on CI
* [QTBUG-133538](https://bugreports.qt.io/browse/QTBUG-133538) Qt 6.8.2 limited supported audio formats
* [QTBUG-133914](https://bugreports.qt.io/browse/QTBUG-133914) FFmpeg plugin tests may fail to build on Linux and
Android
* [QTBUG-116015](https://bugreports.qt.io/browse/QTBUG-116015) REG: Qt6 Audio device enumeration fails on Linux system
without pulseaudio or with pulseaudio disabled.
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-134248](https://bugreports.qt.io/browse/QTBUG-134248) QDoc: error: Documentation warnings (6) exceeded the
limit (2) for 'QtWebEngine'.
* [QTBUG-129758](https://bugreports.qt.io/browse/QTBUG-129758) Audio playback does not work on linux/aarch64 (sailfish
os)
* [QTBUG-135239](https://bugreports.qt.io/browse/QTBUG-135239) external QAudioDevice no longer provides sample rates
* [QTBUG-134229](https://bugreports.qt.io/browse/QTBUG-134229) Changing playback speed results in cracking and out-of-
sync sound when playing audio/video on Android
* [QTBUG-134430](https://bugreports.qt.io/browse/QTBUG-134430) QCamera stops working entirely if device is disconnected
* [QTBUG-135618](https://bugreports.qt.io/browse/QTBUG-135618) [MacOS] Sporadic crashes when call
QVideoFrame::toImage()
* [QTBUG-135951](https://bugreports.qt.io/browse/QTBUG-135951) QMediaRecorder captures video at a much worse quality on
Linux
* [QTBUG-135873](https://bugreports.qt.io/browse/QTBUG-135873) Crash when trying to play video
* [QTBUG-135601](https://bugreports.qt.io/browse/QTBUG-135601) tst_QWindowCaptureBackend failures in Windows 11 24h2
* [QTBUG-123073](https://bugreports.qt.io/browse/QTBUG-123073) [macOS] QMediaRecorder failed to record an audio after
reconnecting AirPods
* [QTBUG-136632](https://bugreports.qt.io/browse/QTBUG-136632) There is no sound when playing videos (REGRESSION)
* [QTBUG-135281](https://bugreports.qt.io/browse/QTBUG-135281) Qml Camera not work on webassembly
* [QTBUG-
133652](https://bugreports.qt.io/browse/QTBUG-133652) tst_QMediaPlayerBackend::play_playbackLastsForTheExpectedTime is
flaky on Linux
* [QTBUG-136124](https://bugreports.qt.io/browse/QTBUG-136124) tst_qwindowcapturebackend: flaky deadlocks on
opensuse-15.6
* [QTBUG-135614](https://bugreports.qt.io/browse/QTBUG-135614) recorder_encodesFrames_toValidMediaFile_whenWindowResizes
fails on opensuse/asan
* [QTBUG-129713](https://bugreports.qt.io/browse/QTBUG-129713) Test times out: tst_QMediaFrameInputsBackend::mediaRecor
derWritesVideo_whenInputFrameGrowsOverTime
* [QTBUG-127733](https://bugreports.qt.io/browse/QTBUG-127733) tst_QAudioSink::pullResumeFromUnderrun() failed on
Ubuntu 24.04 offscreen and X11
* [QTBUG-134645](https://bugreports.qt.io/browse/QTBUG-134645) SoundEffect decoding error
* [QTBUG-117099](https://bugreports.qt.io/browse/QTBUG-117099) Video jerks when playing (Windows backend)
* [QTBUG-138000](https://bugreports.qt.io/browse/QTBUG-138000) tst_QAudioSource::pull fails on ubuntu-22.04-x11-tests
* [QTBUG-137984](https://bugreports.qt.io/browse/QTBUG-137984) Unable to compile QtMultimedia Debug under PiOS
* [QTBUG-127560](https://bugreports.qt.io/browse/QTBUG-127560) maroon demo lags when enabling sounds
* [QTBUG-131912](https://bugreports.qt.io/browse/QTBUG-131912) [soundeffect] wrong playback on windows
* [QTBUG-138901](https://bugreports.qt.io/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-139660](https://bugreports.qt.io/browse/QTBUG-139660) QTextToSpeech WinRT backend stops speaking after the
first word in Qt 6.9.2

### qttools
* [QTBUG-128326](https://bugreports.qt.io/browse/QTBUG-128326) Can't document list<T> properties in QML
* [QTBUG-132278](https://bugreports.qt.io/browse/QTBUG-132278) lupdate does not see translate macros in inherited
classes template parameter list
* [QTBUG-120508](https://bugreports.qt.io/browse/QTBUG-120508) Qt Linguist: Unreadable HTML tags in dark mode
* [QTBUG-127452](https://bugreports.qt.io/browse/QTBUG-127452) Linguist unreadable after switching to dark theme
* [QTBUG-80574](https://bugreports.qt.io/browse/QTBUG-80574) lupdate -location relative doesn't work for XLIFF
* [QTBUG-101196](https://bugreports.qt.io/browse/QTBUG-101196) lupdate parser fumbles with inline namespaces
* [QTBUG-33978](https://bugreports.qt.io/browse/QTBUG-33978) lupdate segfault on \0 in Java
* [QTBUG-98919](https://bugreports.qt.io/browse/QTBUG-98919) static_cast<> throws off lupdate's parsing of
QCoreApplication::translate()
* [QTBUG-132151](https://bugreports.qt.io/browse/QTBUG-132151) QDoc doesn't support grouped properties when parsing a
.qml file
* [QTBUG-132953](https://bugreports.qt.io/browse/QTBUG-132953) tst_helpengineplugin.cpp:41:9: error: unknown type name
'DomCreationOptions
* [QTBUG-131931](https://bugreports.qt.io/browse/QTBUG-131931) Fix incorrect documentation for \reimp
* [QTBUG-57734](https://bugreports.qt.io/browse/QTBUG-57734) Blinking cursor does not always have focus
* [QTBUG-132707](https://bugreports.qt.io/browse/QTBUG-132707) Missing links in Qt Linguist Manual: Text ID based
translations doc
* [QTBUG-132557](https://bugreports.qt.io/browse/QTBUG-132557) "Updating '%1'..." not translatable in lrelease
* [QTBUG-87872](https://bugreports.qt.io/browse/QTBUG-87872) qsTranslate is not picked up by lupdate/lrelease in
template literal string in qml
* [QTBUG-128603](https://bugreports.qt.io/browse/QTBUG-128603) The content in Qt Linguist UI doesn't get updated when
opening an updated .ts file while the previous .ts is opened
* [QTBUG-128604](https://bugreports.qt.io/browse/QTBUG-128604) Qt Linguist requires to be restarted to correctly
display the updated source code information
* [QTBUG-32216](https://bugreports.qt.io/browse/QTBUG-32216) Ctrl+B works only when the focus is in "Source text"
* [QTBUG-54203](https://bugreports.qt.io/browse/QTBUG-54203) Linguist hardcoded background colors when working with >1
language
* [QTBUG-131158](https://bugreports.qt.io/browse/QTBUG-131158) Qdoc mangles link targets that contain trademark symbols
* [QTBUG-132881](https://bugreports.qt.io/browse/QTBUG-132881) qdoc fails to document private signals
* [QTBUG-68098](https://bugreports.qt.io/browse/QTBUG-68098) QT linguist expands XML entities in XLIFF ids
* [QTBUG-132613](https://bugreports.qt.io/browse/QTBUG-132613) lrelease: OUTPUT_LOCATION is ignored for auto-generated
*.ts files
* [QTBUG-798](https://bugreports.qt.io/browse/QTBUG-798) lupdate finds tr() too aggressively
* [QTBUG-36443](https://bugreports.qt.io/browse/QTBUG-36443) lconvert could offer option to sort translation messages
in ts file
* [QTBUG-89128](https://bugreports.qt.io/browse/QTBUG-89128) QtLinguist shows language names in native language
* [QTBUG-131459](https://bugreports.qt.io/browse/QTBUG-131459) QDoc: No warning if \qmltype contains \inherits with
non-existing type
* [QTBUG-10581](https://bugreports.qt.io/browse/QTBUG-10581) Linguists "Statistics" menu item should not be checkable
* [QTBUG-95236](https://bugreports.qt.io/browse/QTBUG-95236) qttools fails configure with deactivated features.
* [QTBUG-52661](https://bugreports.qt.io/browse/QTBUG-52661) Validation only applies to first length variant
* [QTBUG-130096](https://bugreports.qt.io/browse/QTBUG-130096) clang-based lupdate fails on macOS 15
* [QTBUG-131481](https://bugreports.qt.io/browse/QTBUG-131481) Qt Linguist: Runtime warnings about
QAccessibleTree::indexFromLogical: invalid index:  7 0
* [QTBUG-130006](https://bugreports.qt.io/browse/QTBUG-130006) lupdate: -mno-sse not recognized if binary linked
against Clang libraries built on ARM-based Mac
* [QTBUG-133320](https://bugreports.qt.io/browse/QTBUG-133320) The translate dialog is not working correctly
* [QTBUG-52180](https://bugreports.qt.io/browse/QTBUG-52180) lupdate should complain about re-use of IDs for different
(context,source,disambiguation) tuples
* [QTBUG-134250](https://bugreports.qt.io/browse/QTBUG-134250) qdoc fails to report warnings for incorrect \fn
signatures
* [QTBUG-134520](https://bugreports.qt.io/browse/QTBUG-134520) qdoc: delimiters surrounding alt text are in the
generated HTML attribs.
* [QTBUG-134693](https://bugreports.qt.io/browse/QTBUG-134693) [REG 6.8 -> 6.9] qt_add_translations creates QM files in
PROJECT_BINARY_DIR instead of CMAKE_CURRENT_BINARY_DIR
* [QTBUG-124852](https://bugreports.qt.io/browse/QTBUG-124852) Linguist tool bar looks funny
* [QTBUG-131856](https://bugreports.qt.io/browse/QTBUG-131856) \qmlproperty docs don't mention how to document enum
type
* [QTBUG-134458](https://bugreports.qt.io/browse/QTBUG-134458) qdoc: Command for marking non-translatable strings
* [QTBUG-136115](https://bugreports.qt.io/browse/QTBUG-136115) REG: QDoc never links using relative hrefs when running
in single-exec mode
* [QTBUG-135398](https://bugreports.qt.io/browse/QTBUG-135398) [REG 6.8.3->6.9.0] MSVC2022 x64: Widget Designer crash
when QWebEngineView is dragged to canvas
* [QTBUG-94345](https://bugreports.qt.io/browse/QTBUG-94345)  Qt Designer crash in QQuickWidget plugin
* [QTBUG-100285](https://bugreports.qt.io/browse/QTBUG-100285) Windows: Qt Designer crash when selecting QWebEngineView
* [QTBUG-136164](https://bugreports.qt.io/browse/QTBUG-136164) Saving UI-file using QFormBuilder missing properties
(unsupported?)
* [QTBUG-136436](https://bugreports.qt.io/browse/QTBUG-136436) qdoc doesn't warn about missing alt text for
\inlineimage
* [QTBUG-133739](https://bugreports.qt.io/browse/QTBUG-133739) Update qdoc manual for \deprecated and \moduleState
* [QTBUG-136342](https://bugreports.qt.io/browse/QTBUG-136342) Build fails wihtout style_stylesheet feature
* [QTBUG-135692](https://bugreports.qt.io/browse/QTBUG-135692) lupdate orders messages differently depending on
"-locations" argument
* [QTBUG-136532](https://bugreports.qt.io/browse/QTBUG-136532) QRegularExpression::matchView is not indexed by Qt
Assistant
* [QTBUG-136768](https://bugreports.qt.io/browse/QTBUG-136768) Mis-detection of namespaces
* [QTBUG-136736](https://bugreports.qt.io/browse/QTBUG-136736) [REG: 6.5->6.8] ios: Fails if main app target is in a
subdirectory
* [QTBUG-103470](https://bugreports.qt.io/browse/QTBUG-103470) [iOS] CMake translation handling fails
* [QTBUG-117406](https://bugreports.qt.io/browse/QTBUG-117406) [REG 6.6.0beta4->6.7.0] linguist/i18n and qml/qml-i18n
not compiling on iOS
* [QTBUG-130646](https://bugreports.qt.io/browse/QTBUG-130646) qdoc hangs when generating QML documentation
* [QTBUG-136805](https://bugreports.qt.io/browse/QTBUG-136805) Fix typo in the \modulestate description
* [QTBUG-137147](https://bugreports.qt.io/browse/QTBUG-137147) Auto-links to deprecated functions fail when
alternatives exist
* [QTBUG-96693](https://bugreports.qt.io/browse/QTBUG-96693) QUiLoader resolves  wrong buddy when UI is loaded twice
* [QTBUG-138072](https://bugreports.qt.io/browse/QTBUG-138072) Remove traces of <type> argument to \page command from
documentation
* [QTBUG-136158](https://bugreports.qt.io/browse/QTBUG-136158) Qt UI Tools: Add alt texts
* [QTBUG-138557](https://bugreports.qt.io/browse/QTBUG-138557) [REG 6.10] qdoc cannot resolve link to deprecated
q[v]snprintf
* [QTBUG-138492](https://bugreports.qt.io/browse/QTBUG-138492) qdoc: Snippet indentation issues
* [QTBUG-137569](https://bugreports.qt.io/browse/QTBUG-137569) make qttools configure more user friendly on windows
* [QTBUG-138870](https://bugreports.qt.io/browse/QTBUG-138870) QDoc fails to parse templated using statement with
default value for a template arg
* [QTBUG-139057](https://bugreports.qt.io/browse/QTBUG-139057) Doc: Show correct signature for qDebug() , qInfo() ...
macros
* [QTBUG-138887](https://bugreports.qt.io/browse/QTBUG-138887) [REG 5.13 → 5.14] \overload lastIndexOf() in qstring.cpp
renders lastIndexOf() as a non-link
* [QTBUG-138547](https://bugreports.qt.io/browse/QTBUG-138547) No disambiguation between types from same root module
* [QTBUG-139199](https://bugreports.qt.io/browse/QTBUG-139199) qttools configure error if llvm-provided packages are
used
* [QTBUG-138632](https://bugreports.qt.io/browse/QTBUG-138632) Document new label support in Qt Linguist documentation
* [QTBUG-69756](https://bugreports.qt.io/browse/QTBUG-69756) QDoc: Parentheses in link text causes premature link end
anchor
* [QTBUG-86490](https://bugreports.qt.io/browse/QTBUG-86490) Generated documentation for change signals that represent
more than one property is hard to read
* [QTBUG-139407](https://bugreports.qt.io/browse/QTBUG-139407) QDoc fails to build with LLVM >= 21
* [QTBUG-139614](https://bugreports.qt.io/browse/QTBUG-139614) QDoc: Index files do not record the declared return type
* [QTBUG-138084](https://bugreports.qt.io/browse/QTBUG-138084) qdoc links return values of static functions to default
ctor of class, not class itself
* [QTBUG-139769](https://bugreports.qt.io/browse/QTBUG-139769) [Regr: 6.9.2 -> 6.10] Qt 6.10 BETA 3: lupdate does not
include context names in ts files
* [QTBUG-97125](https://bugreports.qt.io/browse/QTBUG-97125) Assistant is unusable on macOS Dark theme
* [QTBUG-133106](https://bugreports.qt.io/browse/QTBUG-133106) qmlls: linking help plugin makes binary size too big
* [QTBUG-127789](https://bugreports.qt.io/browse/QTBUG-127789) Generated TS files are missing the language and
sourcelanguage attributes
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-126546](https://bugreports.qt.io/browse/QTBUG-126546) Attribution documentation processed twice in CI
* [QTBUG-134195](https://bugreports.qt.io/browse/QTBUG-134195) Qt Widgets Designer/Property editor: theme icons
dropdown shown for  maximumSize Width property
* [QTBUG-134256](https://bugreports.qt.io/browse/QTBUG-134256) Coverity: Use after free in Qt Designer's property
editor
* [QTBUG-134595](https://bugreports.qt.io/browse/QTBUG-134595) Build of qttools/linguist fails with features mdiarea,
fontcombobox or syntaxhighlighting disabled
* [QTBUG-130888](https://bugreports.qt.io/browse/QTBUG-130888) Incorrect formulation of conditonal noexcept \note's
* [QTBUG-136963](https://bugreports.qt.io/browse/QTBUG-136963) qdoc/qmlmarkupvisitor.h:78:16: error:
‘QQmlJS::AST::Expression’ has not been declared
* [QTBUG-136247](https://bugreports.qt.io/browse/QTBUG-136247) QDoc doesn´t resolve \externalpage title correctly
* [QTBUG-134806](https://bugreports.qt.io/browse/QTBUG-134806) qdoc has no way to independently document QML
enumerations
* [QTBUG-136483](https://bugreports.qt.io/browse/QTBUG-136483) qdoc non-deterministic .index output
* [QTBUG-138901](https://bugreports.qt.io/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-110696](https://bugreports.qt.io/browse/QTBUG-110696) Qt6CoreMacros.cmake should take AUTOGEN_BUILD_DIR into
account
* [QTBUG-139193](https://bugreports.qt.io/browse/QTBUG-139193) Incomplete type information in all member pages
* [QTBUG-139262](https://bugreports.qt.io/browse/QTBUG-139262) Some links to non-overloaded functions contain overload
numbers

### qtdoc
* [QTBUG-130567](https://bugreports.qt.io/browse/QTBUG-130567) Doc: wrong link to XWayland
* [QTBUG-132348](https://bugreports.qt.io/browse/QTBUG-132348) Add missing best practices topics to the qtdoc project
tree
* [QTBUG-132551](https://bugreports.qt.io/browse/QTBUG-132551) Cannot build Car Configurator demo
* [QTWEBSITE-1200](https://bugreports.qt.io/browse/QTWEBSITE-1200) Protect macOS specific file paths from translation
* [QTBUG-132360](https://bugreports.qt.io/browse/QTBUG-132360) On QtDice example top and bottom bar are partially
visible.
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
* [QTBUG-133957](https://bugreports.qt.io/browse/QTBUG-133957) Add information about source SBOM in SBOM page
* [QTBUG-127953](https://bugreports.qt.io/browse/QTBUG-127953) Basic support for CMake FetchContent
* [QTBUG-135250](https://bugreports.qt.io/browse/QTBUG-135250) Editorial notes on `Qt for Wayland Requirements` page
* [QTBUG-135289](https://bugreports.qt.io/browse/QTBUG-135289) [Examples] Lightning Viewer app misses tags
* [QTBUG-134789](https://bugreports.qt.io/browse/QTBUG-134789) "Contents" menu hidden behind images
* [QTBUG-100340](https://bugreports.qt.io/browse/QTBUG-100340) Remove documentation of QPF2 fonts
* [QTBUG-136036](https://bugreports.qt.io/browse/QTBUG-136036) colorpaletteclient doesn't compile if qml-network is
disabled
* [QTBUG-133462](https://bugreports.qt.io/browse/QTBUG-133462) QNAM cannot get response from Qt HTTP Server due to WASM
app not being allowed to perform Cross-Origin Resource Sharing
* [QTBUG-136482](https://bugreports.qt.io/browse/QTBUG-136482) REG [6.9.0->6.9.1] demos/hangman not compiling on
Android
* [QTBUG-135801](https://bugreports.qt.io/browse/QTBUG-135801) windeployqt: Help output listed for an old version
* [QTBUG-135840](https://bugreports.qt.io/browse/QTBUG-135840) the doc only contains qmake but not cmake
* [QTBUG-136974](https://bugreports.qt.io/browse/QTBUG-136974) Qt Licensing page does not list Qt Graphs under GPL
licensed modules
* [QTBUG-132833](https://bugreports.qt.io/browse/QTBUG-132833) QT_QPA_EGLFS_ROTATION rotates mouse events but not touch
events
* [QTBUG-133792](https://bugreports.qt.io/browse/QTBUG-133792) Compiling demos/maroon and demos/hangman on
Windows/MacOS fails
* [QTTA-401](https://bugreports.qt.io/browse/QTTA-401) Qt Jenny Demo: Gradle is not called during CMake configure
to generate code
* [QTBUG-138105](https://bugreports.qt.io/browse/QTBUG-138105) [Reg 6.5.9 -> 6.8.3] Alarms demo: TumberDelegate can no
longer read properties
* [QTBUG-138169](https://bugreports.qt.io/browse/QTBUG-138169) Document Viewer: Runtime warnings
* [QTBUG-95325](https://bugreports.qt.io/browse/QTBUG-95325) Removal of QTextStream::setCodec is not documented
* [QTBUG-118823](https://bugreports.qt.io/browse/QTBUG-118823) Debian repository setup suggests putting a password to a
plain text file that is worldreadable
* [QTBUG-138093](https://bugreports.qt.io/browse/QTBUG-138093) winrt::init_apartment(multithreaded) causes
QFileDialog::getOpenFileName to get stuck
* [QTBUG-138344](https://bugreports.qt.io/browse/QTBUG-138344) documentviewer: Language is not applied to plugin texts
* [QTBUG-138476](https://bugreports.qt.io/browse/QTBUG-138476) documentviewer: Fix deployment on macOS, Windows, Linux
* [QTBUG-138176](https://bugreports.qt.io/browse/QTBUG-138176) Robot Arm: qmllint warnings
* [QTBUG-138177](https://bugreports.qt.io/browse/QTBUG-138177) Robot Arm: runtime warnings
* [QTBUG-138613](https://bugreports.qt.io/browse/QTBUG-138613) Remove links to 'Solutions for UI Design' page for 6.10
* [QTBUG-138587](https://bugreports.qt.io/browse/QTBUG-138587) Add information on how to subscribe to the mailing list
mentioned on "Security in Qt"
* [QTBUG-138165](https://bugreports.qt.io/browse/QTBUG-138165) Dice: qmllint warnings
* [QTBUG-137956](https://bugreports.qt.io/browse/QTBUG-137956) \generatelist with sorting based on title is buggy
* [QTBUG-138174](https://bugreports.qt.io/browse/QTBUG-138174) Lightning Viewer: runtime warnings
* [QTBUG-138898](https://bugreports.qt.io/browse/QTBUG-138898) [REG 6.10.0 beta2 -> beta3] demos/coffee not launching
* [QTBUG-138175](https://bugreports.qt.io/browse/QTBUG-138175) Media Player example in qtdoc: qmllint warnings
* [QTBUG-135377](https://bugreports.qt.io/browse/QTBUG-135377) The Qt Wayland platform plugin is missing from the
documentation.
* [QTBUG-138676](https://bugreports.qt.io/browse/QTBUG-138676) Coffee machine examples images not getting current
values fom slider
* [QTBUG-137296](https://bugreports.qt.io/browse/QTBUG-137296) Clarifications to "Qt for Android - Building from
Source" page based on customer feedback.
* [QTBUG-117368](https://bugreports.qt.io/browse/QTBUG-117368) Thermostat: "Binding loops detected" runtime warnings
* [QTBUG-138188](https://bugreports.qt.io/browse/QTBUG-138188) Thermostat: qmllint warnings
* [QTBUG-139281](https://bugreports.qt.io/browse/QTBUG-139281) [REG 6.10.0 beta2 -> beta3] demos/coffee not launching
in qmake build on Windows
* [QTBUG-136065](https://bugreports.qt.io/browse/QTBUG-136065) Installer command does not work
* [QTBUG-137052](https://bugreports.qt.io/browse/QTBUG-137052) Document the new configure's output files in packages
* [QTBUG-138170](https://bugreports.qt.io/browse/QTBUG-138170) FX & Material Showroom: qmllint warnings
* [QTBUG-139996](https://bugreports.qt.io/browse/QTBUG-139996) lightningviewer fails to build with Boot to Qt on
Windows
* [QTBUG-139340](https://bugreports.qt.io/browse/QTBUG-139340) [new example] demos/graphs_csv not compiling on Wasm
multithread
* [QTBUG-140383](https://bugreports.qt.io/browse/QTBUG-140383) Coffee Machine: qmllint warnings
* [QTBUG-140387](https://bugreports.qt.io/browse/QTBUG-140387) Robot Arm: qmllint warnings
* [QTBUG-131769](https://bugreports.qt.io/browse/QTBUG-131769) Remove traces of VS 2019 in documentation
* [QTBUG-132046](https://bugreports.qt.io/browse/QTBUG-132046) Remove AGX Xavier and add AGX Orin in Tier table
* [QTBUG-132738](https://bugreports.qt.io/browse/QTBUG-132738) Errors in some examples
* [QTBUG-133305](https://bugreports.qt.io/browse/QTBUG-133305) QDeclarative crashes with PARAM_RTP_MEM_FILL=FALSE on
VxWorks
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-134220](https://bugreports.qt.io/browse/QTBUG-134220) The xcb-xinerama is missing from table listing Qt
requirements on X11
* [QTBUG-134104](https://bugreports.qt.io/browse/QTBUG-134104) Specific Options for Platforms documentation should have
VxWorks
* [QTBUG-35598](https://bugreports.qt.io/browse/QTBUG-35598) QtQuick Controls TextField and TextArea miss mouse
context menu
* [QTBUG-134251](https://bugreports.qt.io/browse/QTBUG-134251) Qt Quick for Android is hard to find
* [QTBUG-133574](https://bugreports.qt.io/browse/QTBUG-133574) Setting QT_DEFAULT_MAJOR_VERSION to 6 doesn't select Qt6
over Qt5
* [QTBUG-135944](https://bugreports.qt.io/browse/QTBUG-135944) Version string '6.9.0' found in 6.10.0 sources
* [QTBUG-129105](https://bugreports.qt.io/browse/QTBUG-129105) Car configurator can't download assets from
download.qt.io
* [QTBUG-136683](https://bugreports.qt.io/browse/QTBUG-136683) Update TI SK-AM62 Supported Platforms entry in doc for
6.10
* [QTBUG-136794](https://bugreports.qt.io/browse/QTBUG-136794) QML debugging is excluded in some of the Android
examples and demos
* [QTBUG-136334](https://bugreports.qt.io/browse/QTBUG-136334) The documentation of qt6_add_lightprobe_images is
missing
* [QTBUG-134903](https://bugreports.qt.io/browse/QTBUG-134903) Duplicate context menus when using custom context Menus
in text controls
* [QTBUG-138189](https://bugreports.qt.io/browse/QTBUG-138189) To Do List: qmllint warnings
* [QTBUG-138164](https://bugreports.qt.io/browse/QTBUG-138164) Coffee Machine: qmllint warnings
* [QTBUG-138632](https://bugreports.qt.io/browse/QTBUG-138632) Document new label support in Qt Linguist documentation
* [QTBUG-138527](https://bugreports.qt.io/browse/QTBUG-138527) Replace direct links to https://doc.qt.io/qt-6/
* [QTBUG-138901](https://bugreports.qt.io/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-138124](https://bugreports.qt.io/browse/QTBUG-138124) Car Configurator: Runtime warnings
* [QTTA-450](https://bugreports.qt.io/browse/QTTA-450) QtJenny Example fails to build with
'QtCore/private/qandroidextras_p.h' file not found
* [QTBUG-136809](https://bugreports.qt.io/browse/QTBUG-136809) Specify that the Raspberry Pi 5 SoC is the tier 1
reference target
* [QTBUG-140051](https://bugreports.qt.io/browse/QTBUG-140051) Cosmetic facelift for QtJenny Demo
* [QTTA-460](https://bugreports.qt.io/browse/QTTA-460) Documentation navigation is not functional

### qtqa
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-130992](https://bugreports.qt.io/browse/QTBUG-130992) Crash when rendering radialGradient
* [QTBUG-134408](https://bugreports.qt.io/browse/QTBUG-134408) Update Vale linting config and vocabularies

### qtlocation
* [QTBUG-128901](https://bugreports.qt.io/browse/QTBUG-128901) MapPolyline cannot tolerate empty QGeoPath when
referenceSurface is set to Globe
* [QTBUG-134438](https://bugreports.qt.io/browse/QTBUG-134438) MapQuickItem HoverHandler or MouseArea incorrect if
zoomLevel set
* [QTBUG-134097](https://bugreports.qt.io/browse/QTBUG-134097) TapHandler with a MapPolyline is not getting tapped
events when the Map is rotated
* [QTBUG-138409](https://bugreports.qt.io/browse/QTBUG-138409) Incorrect qtlocation documentation
* [QTBUG-137557](https://bugreports.qt.io/browse/QTBUG-137557) QtLocation: Using GeocodeModel with OSM plugin in QML
causes app crash when canceling update
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtpositioning
* [QTBUG-133935](https://bugreports.qt.io/browse/QTBUG-133935) QML Qt Positioning memory use after free() / double
free()
* [QTBUG-135967](https://bugreports.qt.io/browse/QTBUG-135967) QGeoPolygon does not serialize its holes
* [QTBUG-136157](https://bugreports.qt.io/browse/QTBUG-136157) Qt Positioning: Add alt texts
* [QTBUG-138187](https://bugreports.qt.io/browse/QTBUG-138187) Satellite Info: qmllint warnings
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-137764](https://bugreports.qt.io/browse/QTBUG-137764) QDoc uses incorrect image source
* [QTBUG-106049](https://bugreports.qt.io/browse/QTBUG-106049) Qt Android's QGeoCoordinate API returns altitude in
wrong reference frame
* [QTBUG-138174](https://bugreports.qt.io/browse/QTBUG-138174) Lightning Viewer: runtime warnings
* [QTBUG-139654](https://bugreports.qt.io/browse/QTBUG-139654) Update QtPositioning documentation to use QDoc commands
* [QTBUG-139780](https://bugreports.qt.io/browse/QTBUG-139780) Qt Positioning: Discrepancy between documented type
names and actual type names
* [QTBUG-139560](https://bugreports.qt.io/browse/QTBUG-139560) Access functions are documented even when their
properties are not

### qtsensors
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-138901](https://bugreports.qt.io/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist

### qtconnectivity
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
* [QTBUG-99410](https://bugreports.qt.io/browse/QTBUG-99410) [macOS 12.1] Bluetooth data stream blocked when main menu
opened
* [QTBUG-136576](https://bugreports.qt.io/browse/QTBUG-136576) QNdefNfcSmartPosterRecord might leak memory
* [QTBUG-136506](https://bugreports.qt.io/browse/QTBUG-136506) NFC target should be invalidated if Java function call
fails
* [QTBUG-136150](https://bugreports.qt.io/browse/QTBUG-136150) Qt NFC: Add alt texts
* [QTBUG-136156](https://bugreports.qt.io/browse/QTBUG-136156) Qt Bluetooth: Add alt texts
* [QTBUG-132455](https://bugreports.qt.io/browse/QTBUG-132455) [Android] Lots of deprecated API is used
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-136692](https://bugreports.qt.io/browse/QTBUG-136692) BLE devices can't be discovered after initial connection
on iOS 18+
* [QTBUG-138901](https://bugreports.qt.io/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist

### qtwayland
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
* [QTBUG-132642](https://bugreports.qt.io/browse/QTBUG-132642) custom-extension example broken
* [QTBUG-132196](https://bugreports.qt.io/browse/QTBUG-132196) text input v3: input method active with popup menu
* [QTBUG-120384](https://bugreports.qt.io/browse/QTBUG-120384) Define "manufacturer" in WaylandOutput documentation
* [QTBUG-134071](https://bugreports.qt.io/browse/QTBUG-134071) [qtwayland] Manual tests fail to compile
* [QTBUG-134205](https://bugreports.qt.io/browse/QTBUG-134205) cmake execution failed
* [QTBUG-134264](https://bugreports.qt.io/browse/QTBUG-134264) "QtShell Compositor" -example install instructions
missing
* [QTBUG-134126](https://bugreports.qt.io/browse/QTBUG-134126) bakedlightmap example: wayland assertion error
* [QTBUG-134939](https://bugreports.qt.io/browse/QTBUG-134939) FAIL!  : tst_WaylandCompositor::simpleKeyboard()
Received a fatal error.
* [QTBUG-136494](https://bugreports.qt.io/browse/QTBUG-136494) FAIL!  : tst_xdgshell::popup() 'popup->isExposed()'
returned FALSE. ()
* [QTBUG-132208](https://bugreports.qt.io/browse/QTBUG-132208) Small memory deficiency in wl_buffer in linux-dmabuf
* [QTBUG-137333](https://bugreports.qt.io/browse/QTBUG-137333) Wayland Compositor + static build + LTO = crash
* [QTBUG-133866](https://bugreports.qt.io/browse/QTBUG-133866) Using qt-shell, if item in dialog is selected with
mouse, no further focus navigation via keyboard possible
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-63039](https://bugreports.qt.io/browse/QTBUG-63039) Threaded scenegraph crash with Nvidia drivers in wayland
* [QTBUG-132699](https://bugreports.qt.io/browse/QTBUG-132699) tst_WaylandReconnect::multipleScreens is flaky on Ubuntu
22.04
* [QTBUG-134234](https://bugreports.qt.io/browse/QTBUG-134234) rare crashes in QWaylandShmBackingStore::flush
* [QTBUG-136343](https://bugreports.qt.io/browse/QTBUG-136343) [REG Qt 6.9] Wayland: QCompleter popup closes
application with protocol error
* [QTBUG-138901](https://bugreports.qt.io/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist

### qt3d
* [QTBUG-133931](https://bugreports.qt.io/browse/QTBUG-133931) QDoc: error: Documentation warnings (48) exceeded the
limit (0) for 'Qt3D'.
* [QTBUG-123885](https://bugreports.qt.io/browse/QTBUG-123885) [cmake] name clash between qt3d and qtquick3d - assimp
target
* [QTBUG-106079](https://bugreports.qt.io/browse/QTBUG-106079) qmllint produces warnings from Qt3D imports and
components
* [QTBUG-135394](https://bugreports.qt.io/browse/QTBUG-135394) MouseHandler may crash if it is destroyed while mouse is
being moved
* [QTBUG-139978](https://bugreports.qt.io/browse/QTBUG-139978) qt3d fails on documentation-warnings
* [QTBUG-132092](https://bugreports.qt.io/browse/QTBUG-132092) RayCasting failing sometimes
* [QTBUG-130470](https://bugreports.qt.io/browse/QTBUG-130470) Issues with BlitFramebuffer::interpolationMethod
* [QTBUG-130490](https://bugreports.qt.io/browse/QTBUG-130490) Unprotected access in animation handler
* [QTBUG-131459](https://bugreports.qt.io/browse/QTBUG-131459) QDoc: No warning if \qmltype contains \inherits with
non-existing type
* [QTBUG-124708](https://bugreports.qt.io/browse/QTBUG-124708) QText2DEntity jagged text when using RHI OpenGL backend
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-138901](https://bugreports.qt.io/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist

### qtimageformats
* [QTBUG-134112](https://bugreports.qt.io/browse/QTBUG-134112) 16-bit Grayscale TIFF is not loaded correctly
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-138901](https://bugreports.qt.io/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist

### qtserialbus
* [QTBUG-135299](https://bugreports.qt.io/browse/QTBUG-135299) error: ‘QElapsedTimer’ was not declared in this scope
* [QTBUG-135791](https://bugreports.qt.io/browse/QTBUG-135791) QModbusClient: : sendRawRequest returns pointer, if
delete immediately, QModbusRtuSerialClientPrivate: : onReadyRead
function crash
* [QTBUG-135132](https://bugreports.qt.io/browse/QTBUG-135132) [qtserialbus] Cannot build manual tests
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-89066](https://bugreports.qt.io/browse/QTBUG-89066) Setting CAN bus bitrate with socketcan returns error
* [QTBUG-107140](https://bugreports.qt.io/browse/QTBUG-107140) Typo in the document?

### qtserialport
* [QTBUG-105561](https://bugreports.qt.io/browse/QTBUG-105561) QSerialPort Mark/Space Emulation causes recursion and
crash
* [QTBUG-131679](https://bugreports.qt.io/browse/QTBUG-131679) QSerialPort does not have Mark/Space parity emulation
for reading the data
* [QTBUG-84689](https://bugreports.qt.io/browse/QTBUG-84689) readyRead() signal will be reemitted even I have called
waitForReadyRead()
* [QTBUG-67544](https://bugreports.qt.io/browse/QTBUG-67544) QSerialPort emits errorOccurred with NoError
* [QTBUG-136154](https://bugreports.qt.io/browse/QTBUG-136154) Qt Serial Port: Add alt texts
* [QTBUG-133489](https://bugreports.qt.io/browse/QTBUG-133489) ResourceError does not fire on unplug for QtSerialPort
6.8.2
* [QTBUG-138643](https://bugreports.qt.io/browse/QTBUG-138643) Details missing for some USB serialport adapters
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-135905](https://bugreports.qt.io/browse/QTBUG-135905) QSerialPortPrivate::writeData function may cause memory
exhaustion.

### qtwebsockets
* [QTBUG-133557](https://bugreports.qt.io/browse/QTBUG-133557) Unable to connect to a server using an URL containing a
ipv6 link local address with a zone-id
* [QTBUG-135959](https://bugreports.qt.io/browse/QTBUG-135959) tst_QWebSocket::moveToThreadNoWarning is failing
* [QTBUG-136216](https://bugreports.qt.io/browse/QTBUG-136216) QWebSocket "Invalid UTF-8 Code Encountered" Error in Qt6
* [QTBUG-136153](https://bugreports.qt.io/browse/QTBUG-136153) Qt WebSockets: Add alt texts
* [QTBUG-81084](https://bugreports.qt.io/browse/QTBUG-81084) Websocket client creates TCP RST instead proper shutdown
on close()
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtwebchannel
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtwebengine
* [QTBUG-131972](https://bugreports.qt.io/browse/QTBUG-131972) error: no matching function for call to
‘TestNamespace::QString::arg(const char [], TestNamespace::QString)
* [QTBUG-112746](https://bugreports.qt.io/browse/QTBUG-112746) QAnyStringView missing implicit conversion from char[]
with unknown size
* [QTBUG-131896](https://bugreports.qt.io/browse/QTBUG-131896) A sentence is cut in the middle in the Native Dialogs
section in Qt WebEngine features
* [QTBUG-131969](https://bugreports.qt.io/browse/QTBUG-131969) "Spellchecking can not be enabled" error logged when
disabling spell checking
* [QTBUG-132564](https://bugreports.qt.io/browse/QTBUG-132564) qwebengine-convert-dict fails on .dic wordlist
* [QTBUG-128893](https://bugreports.qt.io/browse/QTBUG-128893) sbom for qtpdf gets lost , as it ends up as qtwebengine
sbom
* [QTBUG-130608](https://bugreports.qt.io/browse/QTBUG-130608) Dropdown in WebEngineView are not zoomed and aligned
properly when parent of WebEngineView is zoomed.
* [QTBUG-132608](https://bugreports.qt.io/browse/QTBUG-132608) WebEngine assert with Wayland
* [QTBUG-132411](https://bugreports.qt.io/browse/QTBUG-132411) Chromium version isn't reduced in user-agent string
* [QTBUG-132682](https://bugreports.qt.io/browse/QTBUG-132682) [REG 6.9] Segfault in
{{QtWebEngineCore::NativeSkiaOutputDeviceOpenGL::texture()}} with
offscreen platform
* [QTBUG-127109](https://bugreports.qt.io/browse/QTBUG-127109) trouble configuring QtPDF for iOS
* [QTBUG-133558](https://bugreports.qt.io/browse/QTBUG-133558) DRM video fails to play on macOS
* [QTBUG-128222](https://bugreports.qt.io/browse/QTBUG-128222) Migrate away from Chromium legacy IPC
* [QTBUG-133590](https://bugreports.qt.io/browse/QTBUG-133590) tst_qwebengineview::keyboardFocusAfterPopup on macos
* [QTBUG-133649](https://bugreports.qt.io/browse/QTBUG-133649) When calling QWebEngineView::setFocus after calling
QWebEngineView::setFocus for the second time, focus is given to another
widget
* [QTBUG-131841](https://bugreports.qt.io/browse/QTBUG-131841) PdfScrollablePageView does not work in the app
* [QTBUG-133495](https://bugreports.qt.io/browse/QTBUG-133495) Missing Documentation of 3rd party component usage
* [QTBUG-133977](https://bugreports.qt.io/browse/QTBUG-133977) Undefined coin sanity check for offline-documentation
platform
* [QTBUG-134209](https://bugreports.qt.io/browse/QTBUG-134209) Deadlock on NVidia GPU or Vulkan rendeirng
* [QTBUG-134416](https://bugreports.qt.io/browse/QTBUG-134416) Log noise when building Qt WebEngine documentation
* [QTBUG-134107](https://bugreports.qt.io/browse/QTBUG-134107) Qt WebEngine NumLock detection broken using
KeyboardDriver::Xkb
* [QTBUG-135047](https://bugreports.qt.io/browse/QTBUG-135047) Excessive X11 pixmap usage on 6.9
* [QTBUG-128440](https://bugreports.qt.io/browse/QTBUG-128440) Top flaky test:
tst_qwebengineview::inputContextQueryInput
* [QTBUG-134481](https://bugreports.qt.io/browse/QTBUG-134481) qwebengine_convert_dict Cannot encode command 'TRY ...'
to utf8.
* [QTBUG-135620](https://bugreports.qt.io/browse/QTBUG-135620) Qt6WebEngineCoreDeploySupport fails when generating RPM
* [QTBUG-109553](https://bugreports.qt.io/browse/QTBUG-109553) CMake deployment API creates too deep directory
hierarchy when DESTDIR is set
* [QTBUG-119077](https://bugreports.qt.io/browse/QTBUG-119077) CMake deployment API does not deploy Qt Webengine
* [QTBUG-126722](https://bugreports.qt.io/browse/QTBUG-126722) WebEngine: GPU detection is missing "VmWare" in vendor
list
* [QTBUG-135647](https://bugreports.qt.io/browse/QTBUG-135647) WebEngine fatal error in XWayland at startup -> GLX:
Failed to find frame buffer configuration.
* [QTBUG-135032](https://bugreports.qt.io/browse/QTBUG-135032) Uncreatable value types behave erratically
* [QTBUG-123607](https://bugreports.qt.io/browse/QTBUG-123607) Vulkan backend rendering only black on X11
* [QTBUG-136533](https://bugreports.qt.io/browse/QTBUG-136533) Developer tools open with "screencast" enabled (again,
chapter 2)
* [QTBUG-131897](https://bugreports.qt.io/browse/QTBUG-131897) pdf viewer is not working on nano browser and simple
browser sample apps
* [QTBUG-136481](https://bugreports.qt.io/browse/QTBUG-136481) QtWebEngine crashes when screen is removed
* [QTBUG-133593](https://bugreports.qt.io/browse/QTBUG-133593) Qt Webengine debug symbols (dSYM) have incorrect install
location on macOS
* [QTBUG-136637](https://bugreports.qt.io/browse/QTBUG-136637) Missing libxml2.so.2 with libxml2 2.14
* [QTBUG-136257](https://bugreports.qt.io/browse/QTBUG-136257) QtWebEngine based browser shows nothing with panthor
driver
* [QTBUG-135974](https://bugreports.qt.io/browse/QTBUG-135974) adding module pdfwidgets leads to a warning
* [QTBUG-136622](https://bugreports.qt.io/browse/QTBUG-136622) Accessiblity:voice over can't read table content
* [QTBUG-134055](https://bugreports.qt.io/browse/QTBUG-134055) Make Qt WebEngine expose accessibility content properly
* [QTBUG-133608](https://bugreports.qt.io/browse/QTBUG-133608) Missing documentation on how to install Qt WebEngine
* [QTBUG-137447](https://bugreports.qt.io/browse/QTBUG-137447) FAIL!  : tst_UIDelegates::javaScriptDialog(AlertDialog)
'(static_cast<QGuiApplication
*>(QCoreApplication::instance()))->focusObject()' returned FALSE.
* [QTBUG-137854](https://bugreports.qt.io/browse/QTBUG-137854) error: ‘getV4Engine’ is not a member of
‘QQmlEnginePrivate’
* [QTBUG-111907](https://bugreports.qt.io/browse/QTBUG-111907) Crash when touching text field inside WebEngineView
* [QTBUG-136231](https://bugreports.qt.io/browse/QTBUG-136231) Min c++ version required for QtWebengine
* [QTBUG-138009](https://bugreports.qt.io/browse/QTBUG-138009) Correct suggestions for building Qt WebEngine
* [QTBUG-135100](https://bugreports.qt.io/browse/QTBUG-135100) QtPdf doc - broken link & missing information
* [QTBUG-138736](https://bugreports.qt.io/browse/QTBUG-138736) FAIL!  :
tst_QWebEngineCookieStore::basicFilterOverHTTP() Compared values are not
the same
* [QTBUG-138159](https://bugreports.qt.io/browse/QTBUG-138159) Build error:
QtWebEngineCore/private/qtwebenginecoreglobal_p.h: No such file or
directory
* [QTBUG-138425](https://bugreports.qt.io/browse/QTBUG-138425) QtWebEngine no GPU acceleration on Nvidia RTX 4090
* [QTBUG-138734](https://bugreports.qt.io/browse/QTBUG-138734) webengine pdf example: runtime warnings
* [QTBUG-138641](https://bugreports.qt.io/browse/QTBUG-138641) QtWebEngine rendering glitches with &lt;select&gt; element
* [QTBUG-134637](https://bugreports.qt.io/browse/QTBUG-134637) QWebEngine does not respect iframe permissions
* [QTBUG-135787](https://bugreports.qt.io/browse/QTBUG-135787) HTML <permission> requests get ignored -> no
microphone/video on Zoom/Meet
* [QTBUG-139322](https://bugreports.qt.io/browse/QTBUG-139322) fail to install to staging dir
* [QTBUG-139327](https://bugreports.qt.io/browse/QTBUG-139327) webenginequick/quicknanobrowser: make install step does
not install the binary
* [QTBUG-138881](https://bugreports.qt.io/browse/QTBUG-138881) Windows Debug: QQuickWebEngineScriptCollection crashes
after adding custom library path
* [QTBUG-139624](https://bugreports.qt.io/browse/QTBUG-139624) Make qdoc to understand qml list types with lower case
* [QTBUG-139766](https://bugreports.qt.io/browse/QTBUG-139766) [Windows] Linker isn't able to create pdb file for
Qt6WebEngineCore
* [QTBUG-139710](https://bugreports.qt.io/browse/QTBUG-139710) [Reg 6.8 -> 6.9] qml web engine frame crashes on
assigment
* [QTBUG-139998](https://bugreports.qt.io/browse/QTBUG-139998) pdf\multipage and pdf\singlepage fails to build with
Boot to Qt 6.10.0 beta4 on Windows
* [QTBUG-112281](https://bugreports.qt.io/browse/QTBUG-112281) Support ANGLE on Linux
* [QTBUG-132331](https://bugreports.qt.io/browse/QTBUG-132331) missing udev documentation
* [QTBUG-129970](https://bugreports.qt.io/browse/QTBUG-129970) WebEngine Windows ARM support
* [QTBUG-117478](https://bugreports.qt.io/browse/QTBUG-117478) qtwebengine h264 broken on Windows
* [QTBUG-131377](https://bugreports.qt.io/browse/QTBUG-131377) Include Chromium in SBOM
* [QTBUG-132479](https://bugreports.qt.io/browse/QTBUG-132479) [Windows] After download is interrupted,
QWebEngineDownloadRequest::resume() crashes with "Observers can only be
added once!"
* [QTBUG-132473](https://bugreports.qt.io/browse/QTBUG-132473) QWebEngineDownloadRequest::DownloadInterrupted creates
multiple, inconsistent QWebEngineDownloadRequest objects
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-133970](https://bugreports.qt.io/browse/QTBUG-133970) QtPDF spdx files not included in MinGW content
* [QTBUG-134938](https://bugreports.qt.io/browse/QTBUG-134938) FAIL!  : tst_MultiPageView::pinchDragPinch() Compared
doubles are not the same (fuzzy compare)
* [QTBUG-135040](https://bugreports.qt.io/browse/QTBUG-135040) macos: Voice Over rect is wrongly calculated for
WebEngine
* [QTBUG-129769](https://bugreports.qt.io/browse/QTBUG-129769) WebEngine ANGLE error: Failed to make current since
context is marked as lost
* [QTBUG-133570](https://bugreports.qt.io/browse/QTBUG-133570) 6.9beta2/Linux/XCB: WebEngine Simple Browser example
crashes
* [QTBUG-134064](https://bugreports.qt.io/browse/QTBUG-134064) WebEngine build fails with GCC 11.5
* [QTBUG-135621](https://bugreports.qt.io/browse/QTBUG-135621) gn.py needs an -isysroot argument but configure doesn't
create it
* [QTBUG-135786](https://bugreports.qt.io/browse/QTBUG-135786) WebEngine in 6.9.0 with an AMD GPU and on both
Wayland/X11 renders gltiches instead of text
* [QTBUG-133711](https://bugreports.qt.io/browse/QTBUG-133711) QWebEngineClientHints::fullVersionList is not extended
as documented
* [QTBUG-133799](https://bugreports.qt.io/browse/QTBUG-133799) QWebEngineClientHints::fullVersionList changes the order
of the versions
* [QTBUG-134746](https://bugreports.qt.io/browse/QTBUG-134746) [REG 6.8.2 → 6.9] simplebrowser example crashes during
startup on Windows
* [QTBUG-133086](https://bugreports.qt.io/browse/QTBUG-133086) Doc: Improve Networking and WebEngine security topics
* [QTBUG-138589](https://bugreports.qt.io/browse/QTBUG-138589) Quick Nano Browser has qmllint warnings
* [QTBUG-136613](https://bugreports.qt.io/browse/QTBUG-136613) Top flaky test: tst_QWebEngineView::focusOnNavigation
* [QTBUG-139424](https://bugreports.qt.io/browse/QTBUG-139424) GPU rendering not working with mesa 25.2

### qtwebview
* [QTBUG-136082](https://bugreports.qt.io/browse/QTBUG-136082) Android Webview fails to load all html string because it
is percent-encoded
* [QTBUG-134723](https://bugreports.qt.io/browse/QTBUG-134723) [REG 6.8.0 -> 6.8.1] WebView's loadHtml() with BaseURL
has issues loading HTML content.
* [QTBUG-138555](https://bugreports.qt.io/browse/QTBUG-138555) webview2 can not create user data folder
* [QTBUG-139641](https://bugreports.qt.io/browse/QTBUG-139641) WebView2 plugin opens its own new windows Qt has no
control over
* [QTBUG-139717](https://bugreports.qt.io/browse/QTBUG-139717) qwebview loads webenginequick no matter if webview2
plugin backend selected
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-75747](https://bugreports.qt.io/browse/QTBUG-75747) Windows: Support WebView2 backend on msvc

### qtcharts
* [QTBUG-115358](https://bugreports.qt.io/browse/QTBUG-115358) QBarCategoryAxis is exported twice
* [QTBUG-135691](https://bugreports.qt.io/browse/QTBUG-135691) Wasm build fails when linking both QtCharts and QtGraphs
* [QTBUG-136770](https://bugreports.qt.io/browse/QTBUG-136770) QLineSeries.clear() does not remove all lines from the
plot in that series
* [QTBUG-135240](https://bugreports.qt.io/browse/QTBUG-135240) Animation effects in ChartView makes PieSlice lose its
alpha channel
* [QTBUG-132790](https://bugreports.qt.io/browse/QTBUG-132790) Unexpected behaviour of QScatterSeries for
selectedPoints, replace and deselectAllPoints
* [QTBUG-132357](https://bugreports.qt.io/browse/QTBUG-132357) setSelectedColor doesn't work on barsets added to
QBarSeries with insert method
* [QTBUG-140545](https://bugreports.qt.io/browse/QTBUG-140545) Charts with QML Gallery example draws under system bars
(top and bottom)
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-134519](https://bugreports.qt.io/browse/QTBUG-134519) tst_QBarSeries::mousehovered() is flaky on Ubuntu 24.04
X11(GNOME)

### qtdatavis3d
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtvirtualkeyboard
* [QTBUG-135022](https://bugreports.qt.io/browse/QTBUG-135022) FAIL!  : inputpanel::tst_plugin::test_themeChange()
Received a fatal error
* [QTBUG-133400](https://bugreports.qt.io/browse/QTBUG-133400) Mouse/Touch hover propagates to item under VKB
* [QTBUG-137250](https://bugreports.qt.io/browse/QTBUG-137250) REG->6.9.0: VirtualKeyboard not working (Linux)
* [QTBUG-136695](https://bugreports.qt.io/browse/QTBUG-136695) VKB: Entering English characters followed by Digits
automatically converts to chinese
* [QTBUG-134582](https://bugreports.qt.io/browse/QTBUG-134582) Languages dropdown appears blank when scrolling in Qt
Keyboard
* [QTBUG-137434](https://bugreports.qt.io/browse/QTBUG-137434) Inconsistent Keyboard Layout Country List Display
* [QTBUG-131374](https://bugreports.qt.io/browse/QTBUG-131374) The wordCandidateList field is not visible on the
virtual keyboard in a widget application.
* [QTBUG-133614](https://bugreports.qt.io/browse/QTBUG-133614) Caps Lock is not working properly in Qt Virtual
Keyboard.
* [QTBUG-127557](https://bugreports.qt.io/browse/QTBUG-127557) QtVirtualKeyboard crash introduced in 6.5.4
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-133241](https://bugreports.qt.io/browse/QTBUG-133241) VKB basic example's doc is missing cmake explanation
* [QTBUG-123415](https://bugreports.qt.io/browse/QTBUG-123415) [Qt Virtual Keyboard] Example produces lots of warnings
at startup
* [QTBUG-138901](https://bugreports.qt.io/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist

### qtscxml
* [QTBUG-132565](https://bugreports.qt.io/browse/QTBUG-132565) Questions about feature statemachine
* [QTBUG-134901](https://bugreports.qt.io/browse/QTBUG-134901) [REG 6.8.2 -> 6.9.0-RC] QStateMachine and QScxml qmake
projects do not compile
* [QTBUG-135396](https://bugreports.qt.io/browse/QTBUG-135396) Errors point to initial scxml file instead of the
invoked where it happens
* [QTBUG-132510](https://bugreports.qt.io/browse/QTBUG-132510) Superfluous optional components
* [QTBUG-126419](https://bugreports.qt.io/browse/QTBUG-126419) QState::finished not emitted for parallel QStateMachines
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-138901](https://bugreports.qt.io/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist

### qtspeech
* [QTBUG-135969](https://bugreports.qt.io/browse/QTBUG-135969) Top flaky test: tst_QTextToSpeech::synthesize
* [QTBUG-128818](https://bugreports.qt.io/browse/QTBUG-128818) QTextToSpeech with flite crashes saying ©
* [QTBUG-137735](https://bugreports.qt.io/browse/QTBUG-137735) Failing tests on tqtc/lts-6.8: tst_QTextToSpeech
* [QTBUG-137855](https://bugreports.qt.io/browse/QTBUG-137855) QTextToSpeech: flite - sayingWord signals emitted
delayed
* [QTBUG-138064](https://bugreports.qt.io/browse/QTBUG-138064) [flite] tst_QTextToSpeech fails on ubuntu/arm
* [QTBUG-139660](https://bugreports.qt.io/browse/QTBUG-139660) QTextToSpeech WinRT backend stops speaking after the
first word in Qt 6.9.2
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-137947](https://bugreports.qt.io/browse/QTBUG-137947) [flite] QTextToSpeech::pause(BoundaryHint::Word) not
implemented
* [QTBUG-138010](https://bugreports.qt.io/browse/QTBUG-138010) layout / palette glitches with quickspeech example
* [QTBUG-138901](https://bugreports.qt.io/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-108205](https://bugreports.qt.io/browse/QTBUG-108205) tst_QTextToSpeech::pauseResume(darwin) fails on macOS 13
in CI

### qtnetworkauth
* [QTBUG-131948](https://bugreports.qt.io/browse/QTBUG-131948) OAuth2 expirationAt doest not change when invalidated
* [QTBUG-131949](https://bugreports.qt.io/browse/QTBUG-131949) Use UTC instead of local time for internal expiresAt
representation
* [QTBUG-135257](https://bugreports.qt.io/browse/QTBUG-135257) NetworkAuth Coverity findings
* [QTBUG-132710](https://bugreports.qt.io/browse/QTBUG-132710) QtNetworkAuth's use of QStringList for scopes is not
matching RFC6749 Section 3.3 semantics
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-135353](https://bugreports.qt.io/browse/QTBUG-135353) Doc: Edit Qt Network Authorization documentation

### qtremoteobjects
* [QTBUG-131016](https://bugreports.qt.io/browse/QTBUG-131016) Unexpected warning generated by repc
* [QTBUG-136671](https://bugreports.qt.io/browse/QTBUG-136671) Skip remoteobjectsqml build if remoteobjects library
isn't built
* [QTBUG-130972](https://bugreports.qt.io/browse/QTBUG-130972) repc is not deterministic
* [QTBUG-139754](https://bugreports.qt.io/browse/QTBUG-139754) FAIL!  : tst_clientSSL::testRun()
'socketClient->waitForEncrypted(-1)' returned FALSE
* [PYSIDE-3179](https://bugreports.qt.io/browse/PYSIDE-3179) REG->6.11.0: QtRemoteObjects/integration_test.py (and
other RO tests) assert/fail
* [QTBUG-139845](https://bugreports.qt.io/browse/QTBUG-139845) Reg->6.11: Assert when passing a too long-list to
QMetaMethodBuilder::setParameterNames()
* [QTBUG-132738](https://bugreports.qt.io/browse/QTBUG-132738) Errors in some examples
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-132526](https://bugreports.qt.io/browse/QTBUG-132526) Some CMake targets of private Qt modules reference non-
existent include dirs

### qtlottie
* [QTBUG-132404](https://bugreports.qt.io/browse/QTBUG-132404) Cannot build LottieAnimation with qmlsc
* [QTBUG-138213](https://bugreports.qt.io/browse/QTBUG-138213) Some easing curves are misinterpreted in Lottie
* [QTBUG-139975](https://bugreports.qt.io/browse/QTBUG-139975) New example lottie/qtlottieviewer fails to configure
* [QTBUG-140730](https://bugreports.qt.io/browse/QTBUG-140730) Qt Lottie Animation: Missing licensing pages
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtquicktimeline
* [QTBUG-132502](https://bugreports.qt.io/browse/QTBUG-132502) No way to switch to timeline editor
* [QTBUG-133543](https://bugreports.qt.io/browse/QTBUG-133543) An invalid keyframe file can make the application crash.
* [QTBUG-136144](https://bugreports.qt.io/browse/QTBUG-136144) Qt Quick Timeline: Add alt texts
* [QTBUG-131459](https://bugreports.qt.io/browse/QTBUG-131459) QDoc: No warning if \qmltype contains \inherits with
non-existing type
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtquick3d
* [QTBUG-131966](https://bugreports.qt.io/browse/QTBUG-131966) Default dimension for primitive geometry in
documentation
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
* [QTBUG-135115](https://bugreports.qt.io/browse/QTBUG-135115) Oit doesn't work with custom materials
* [QTBUG-135125](https://bugreports.qt.io/browse/QTBUG-135125) OIT alpha is applied twice making rendering darker
* [QTBUG-134999](https://bugreports.qt.io/browse/QTBUG-134999) [Boot2Qt ] 'Failed to build graphics pipeline' when
running 'orderindependenttransparency' example
* [QTBUG-136240](https://bugreports.qt.io/browse/QTBUG-136240) RuntimeLoader example fails on QNX
* [QTBUG-136754](https://bugreports.qt.io/browse/QTBUG-136754) startTime doesn't work without affectors
* [QTBUG-137182](https://bugreports.qt.io/browse/QTBUG-137182) Wrong shading rendered for 3D models imported by
RuntimeLoader
* [QTBUG-137445](https://bugreports.qt.io/browse/QTBUG-137445) Test #10: test_auto_geometry
......................***Failed    0.34 sec
* [QTBUG-137479](https://bugreports.qt.io/browse/QTBUG-137479) Possible null reference in qssgrendernode markdirty
* [QTBUG-136334](https://bugreports.qt.io/browse/QTBUG-136334) The documentation of qt6_add_lightprobe_images is
missing
* [QTBUG-137979](https://bugreports.qt.io/browse/QTBUG-137979) REG->6.10: widgetgraphgallery produces warnings flood
"Vertex buffer empty"
* [QTBUG-138591](https://bugreports.qt.io/browse/QTBUG-138591) Broken font-weight tag
* [QTBUG-136137](https://bugreports.qt.io/browse/QTBUG-136137) License of
qtquick3d/src/runtimerender/res/effectlib/fog.glsllib: SPDX header
differs from qt_attribution
* [QTBUG-139033](https://bugreports.qt.io/browse/QTBUG-139033) [REG 6.9.2 -> 6.10.0] demos/stockqt and
quick3d/graphs/quick3dphysics examples not compiling on Wasm
singlethread
* [QTBUG-138245](https://bugreports.qt.io/browse/QTBUG-138245) FTBFS: qtquick3d's embree 3rd-party
* [QTBUG-139023](https://bugreports.qt.io/browse/QTBUG-139023) Having two View3D instances in same window with only one
having lightmaps makes lightmap rendering erratic
* [QTBUG-139232](https://bugreports.qt.io/browse/QTBUG-139232) Crash when View3D is destroyed in a multiview case
* [QTBUG-136911](https://bugreports.qt.io/browse/QTBUG-136911) 2D items take transformation from random camera if there
are multiple View3Ds into a single scene
* [QTBUG-126098](https://bugreports.qt.io/browse/QTBUG-126098) Item2D uses wrong transformation in multiple views
* [QTBUG-139130](https://bugreports.qt.io/browse/QTBUG-139130) Nested View3D causes 2D content to not be rendered
* [QTBUG-130962](https://bugreports.qt.io/browse/QTBUG-130962) View3D inside XrItem's contentItem is not rendered
* [QTBUG-133645](https://bugreports.qt.io/browse/QTBUG-133645) Curve renderer stroke is blurry inside Qt Quick 3D scene
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-96159](https://bugreports.qt.io/browse/QTBUG-96159) Qt5.git integration fails in '6.2':  The "moc" executable
"/Users/qt/work/qt/qt5/qtbase/libexec/moc" does not exist
* [QTBUG-132526](https://bugreports.qt.io/browse/QTBUG-132526) Some CMake targets of private Qt modules reference non-
existent include dirs
* [QTBUG-135052](https://bugreports.qt.io/browse/QTBUG-135052) [QtQuick3dXr]  Vulkan performance much worse compared to
OpenGLES on Quest 3
* [QTBUG-135823](https://bugreports.qt.io/browse/QTBUG-135823) Qt Quick 3D: OITWeightedBlended silently fails in
WebAssembly
* [QTBUG-138170](https://bugreports.qt.io/browse/QTBUG-138170) FX & Material Showroom: qmllint warnings
* [QTBUG-138901](https://bugreports.qt.io/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist

### qtshadertools
* [QTBUG-131336](https://bugreports.qt.io/browse/QTBUG-131336) Hardcoded shader version prevent creating higher level
shaders with MULTIVIEW
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-138901](https://bugreports.qt.io/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist

### qt5compat
* [QTBUG-132209](https://bugreports.qt.io/browse/QTBUG-132209) Missing information on 'Qt 5 Compatibility APIs:
Graphical Effects' landing page
* [QTBUG-136673](https://bugreports.qt.io/browse/QTBUG-136673) Skip sax autotests if XML is disabled
* [QTBUG-71541](https://bugreports.qt.io/browse/QTBUG-71541) ColorOverlay documentation refers to wrong color format
* [QTBUG-136146](https://bugreports.qt.io/browse/QTBUG-136146) Qt 5 Core Compatibility: Add alt texts
* [QTBUG-122798](https://bugreports.qt.io/browse/QTBUG-122798) [REG 5.15 -> 6.7 (or earlier)] QStringRef -> QStringView
conversion loses null-ness
* [QTBUG-122797](https://bugreports.qt.io/browse/QTBUG-122797) QStringRef doesn't convert to QAnyStringView
* [QTBUG-133892](https://bugreports.qt.io/browse/QTBUG-133892) QDoc: error: Documentation warnings (6) exceeded the
limit (0) for 'QtCore5Compat'.
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-138901](https://bugreports.qt.io/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist

### qtcoap
* [QTBUG-136669](https://bugreports.qt.io/browse/QTBUG-136669) Skip QtCoap build if udpsocket is disabled
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-138901](https://bugreports.qt.io/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-139697](https://bugreports.qt.io/browse/QTBUG-139697) Provide a public "bind" API for QCoapClient, or at least
filter out unexpected replies not from peer

### qtmqtt
* [QTBUG-132164](https://bugreports.qt.io/browse/QTBUG-132164) Qt 6.9 API Review/MQTT/COAP: Logging categories in
public headers
* [QTBUG-135653](https://bugreports.qt.io/browse/QTBUG-135653) MessageReceived not fired when subscribing again to just
unsubscribed topic
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-138901](https://bugreports.qt.io/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist

### qtopcua
* [QTBUG-134674](https://bugreports.qt.io/browse/QTBUG-134674) opcua/waterpump/simulationserver example does not build
with Boot to Qt
* [QTBUG-109096](https://bugreports.qt.io/browse/QTBUG-109096) Installed version of OPC UA example cannot compile
because it relies on the presence of Qt source code
* [QTBUG-136141](https://bugreports.qt.io/browse/QTBUG-136141) Header files not listed in Qt OPC UA example
documentation
* [QTBUG-122005](https://bugreports.qt.io/browse/QTBUG-122005) qtopcua is not building against OpenSSL-1.1.1
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-133890](https://bugreports.qt.io/browse/QTBUG-133890) wrong licensing in
/Users/qt/work/install/sbom/qtopcua-6.10.0.source.spdx
* [QTBUG-133704](https://bugreports.qt.io/browse/QTBUG-133704) REG->6.9b3: OpcUA/Windows: Link error for QMetaObject in
namespace
* [QTBUG-131516](https://bugreports.qt.io/browse/QTBUG-131516) [reg] Fatal error C1067 when building qtopcua with
latest moc changes
* [QTBUG-134944](https://bugreports.qt.io/browse/QTBUG-134944) Issue with Alarm Acknowledgement - BadNodeIdUnknown with
ByteString NodeId
* [QTBUG-135674](https://bugreports.qt.io/browse/QTBUG-135674) SimpleAttributeOperand for condtionId generated with
BrowsePath of arraySize -1
* [QTBUG-135130](https://bugreports.qt.io/browse/QTBUG-135130) [qtopcua] Cannot build manual tests
* [QTBUG-137701](https://bugreports.qt.io/browse/QTBUG-137701) Connecting to unsecured endpoint results in
ClientError::UnknownError
* [QTBUG-138754](https://bugreports.qt.io/browse/QTBUG-138754) Build fails with Qt OPC UA when OpenSSL 1.1 is supported
* [QTBUG-138901](https://bugreports.qt.io/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist

### qtlanguageserver
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qthttpserver
* [QTBUG-132517](https://bugreports.qt.io/browse/QTBUG-132517) qthttpserver build fails when qlocalsockets are disabled
* [QTBUG-132748](https://bugreports.qt.io/browse/QTBUG-132748) Random assert fail in  tst_qhttpserverrequestfilter
* [QTBUG-136675](https://bugreports.qt.io/browse/QTBUG-136675) Skip QHttpServer build if mimetype support is disabled
* [QTBUG-137849](https://bugreports.qt.io/browse/QTBUG-137849) FAIL!  : tst_QHttpServerMultithreaded::initTestCase()
'localserver->listen(local)' returned FALSE. (Local server listen
failed)
* [QTBUG-136155](https://bugreports.qt.io/browse/QTBUG-136155) Qt HTTP Server: Add alt texts
* [QTBUG-137330](https://bugreports.qt.io/browse/QTBUG-137330) QtHttpServer: Writing from Sequential QIODevices to
HTTP(S)/1.1 Hangs the Client
* [QTBUG-130500](https://bugreports.qt.io/browse/QTBUG-130500) Various network tests are failing on macOS 15
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-134250](https://bugreports.qt.io/browse/QTBUG-134250) qdoc fails to report warnings for incorrect \fn
signatures
* [QTBUG-129103](https://bugreports.qt.io/browse/QTBUG-129103) HttpServer documentation needs an overhaul
* [QTBUG-138611](https://bugreports.qt.io/browse/QTBUG-138611) QtHttpServer has out of order writes because it starts
handling the next HTTP/1 request before it's done writing from QIODevice

### qtquick3dphysics
* [QTBUG-131965](https://bugreports.qt.io/browse/QTBUG-131965) Use built-in primitives as CollisionShapes
* [QTBUG-134277](https://bugreports.qt.io/browse/QTBUG-134277) [clang-cl] PhysX build failure
* [QTBUG-139437](https://bugreports.qt.io/browse/QTBUG-139437) multiple definition of CapsuleGeometry
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-138901](https://bugreports.qt.io/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist

### qtgrpc
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
of integers of different signs with x86 and armeabi-v7a developer builds
for Android
* [QTBUG-134273](https://bugreports.qt.io/browse/QTBUG-134273) QtGrpc: Abstract namespaces are not working with
QLocalSocket
* [QTBUG-134647](https://bugreports.qt.io/browse/QTBUG-134647) Cannot cross-compile grpc examples
* [QTBUG-134885](https://bugreports.qt.io/browse/QTBUG-134885) Fail to build with protobuf-30
* [QTBUG-136471](https://bugreports.qt.io/browse/QTBUG-136471) QtGrpc: Deprecate QHash metadata interface in favor of
QMultiHash
* [QTBUG-130113](https://bugreports.qt.io/browse/QTBUG-130113) build time paths used in
Qt6ProtobufWellKnownTypesTargets.cmake
* [QTBUG-137313](https://bugreports.qt.io/browse/QTBUG-137313) Build fails if using QML and GENERATE_PACKAGE_SUBFOLDERS
in qt_add_grpc
* [QTBUG-138180](https://bugreports.qt.io/browse/QTBUG-138180) Qt GRPC: Weird duplications in documentation tree
* [QTBUG-138494](https://bugreports.qt.io/browse/QTBUG-138494) GRPC, QHttp2Channel: Implement metadata handling
according to protocol
* [QTBUG-129160](https://bugreports.qt.io/browse/QTBUG-129160) QtGrpc: improve lifetime-management of Http2Handler
* [QTBUG-138039](https://bugreports.qt.io/browse/QTBUG-138039) QtGrpc: deprecate QHash server metadata interface
* [QTBUG-138683](https://bugreports.qt.io/browse/QTBUG-138683) Protobuf: repeated enum fields are serialized
incorrectly
* [QTBUG-139597](https://bugreports.qt.io/browse/QTBUG-139597) QtGrpc: QGrpcHttp2Channel should guarantee
transportation scheme
* [QTBUG-129918](https://bugreports.qt.io/browse/QTBUG-129918) [FTBFS] gtgrpc: CMake Error: AUTOMOC for target
protocplugintestcommon: The "moc" executable "xxxx" does not exist.
* [QTBUG-120214](https://bugreports.qt.io/browse/QTBUG-120214) Add the support of implicit convertion of protobuf well-
known types from JSON input
* [QTBUG-132125](https://bugreports.qt.io/browse/QTBUG-132125) Clashing of Quick Components and Protobuf QML messages
* [QTBUG-132738](https://bugreports.qt.io/browse/QTBUG-132738) Errors in some examples
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-134250](https://bugreports.qt.io/browse/QTBUG-134250) qdoc fails to report warnings for incorrect \fn
signatures
* [QTBUG-119913](https://bugreports.qt.io/browse/QTBUG-119913) When accessing protobuf message properties, propety
values always detaches the internal shared data
* [QTBUG-138901](https://bugreports.qt.io/browse/QTBUG-138901) Doc: Usage of incorrect argument to \generatelist
* [QTBUG-138812](https://bugreports.qt.io/browse/QTBUG-138812) Doc: Improve security documentation of Qt GRPC

### qtquickeffectmaker
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-121928](https://bugreports.qt.io/browse/QTBUG-121928) Remove Copyright year from About Qt & command line tools

### qtgraphs
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
* [QTBUG-133921](https://bugreports.qt.io/browse/QTBUG-133921) The Graph Gallery example crashes when clicking on
surface graph
* [QTBUG-134002](https://bugreports.qt.io/browse/QTBUG-134002) QBarCategoryAxis::setCategories only works once.
* [QTBUG-134641](https://bugreports.qt.io/browse/QTBUG-134641) the Custom3DItem is still in Scatter3D after it is
deleted by removeCustomItem
* [QTBUG-134997](https://bugreports.qt.io/browse/QTBUG-134997) Crash with hoverable lineseries
* [QTBUG-134598](https://bugreports.qt.io/browse/QTBUG-134598) Qt Graphs Module documentation misses title
* [QTBUG-135388](https://bugreports.qt.io/browse/QTBUG-135388) Axis titles don't align correctly
* [QTBUG-135492](https://bugreports.qt.io/browse/QTBUG-135492) 2d fails compile line graph disabled
* [QTBUG-136631](https://bugreports.qt.io/browse/QTBUG-136631) Surface Graph has draws extra unused triangles
* [QTBUG-136654](https://bugreports.qt.io/browse/QTBUG-136654) Building qtgraphs on mac fails with due to -Wcast-
function-type-mismatch
* [QTBUG-135384](https://bugreports.qt.io/browse/QTBUG-135384) Printing the 3D graph causes the Graph Printing example
to crash
* [QTBUG-135386](https://bugreports.qt.io/browse/QTBUG-135386) [Boot2Qt] Cannot save 3D graph to PDF
* [QTBUG-136725](https://bugreports.qt.io/browse/QTBUG-136725) Graph Node names are different to qml names
* [QTBUG-136942](https://bugreports.qt.io/browse/QTBUG-136942) removeMultiple fails to remove the last item in the
series
* [QTBUG-135929](https://bugreports.qt.io/browse/QTBUG-135929) Labels overlaps when pie slice are small
* [QTBUG-134592](https://bugreports.qt.io/browse/QTBUG-134592) Dragging points in 2D spline graphs is not working
* [QTBUG-136950](https://bugreports.qt.io/browse/QTBUG-136950) tst_qmlbarscatter trying to use non-existent property
* [QTBUG-138257](https://bugreports.qt.io/browse/QTBUG-138257) Code snippet for PieModelMapper uses undefined
properties
* [QTBUG-137718](https://bugreports.qt.io/browse/QTBUG-137718) XYSeries: opacity property has no effect
* [QTBUG-133759](https://bugreports.qt.io/browse/QTBUG-133759) the Custom3DItem position is not correct when setting
"axisZ.reversed: true" in QtGraphs
* [QTBUG-136174](https://bugreports.qt.io/browse/QTBUG-136174) 3D bars graph endless sync loop
* [QTBUG-138470](https://bugreports.qt.io/browse/QTBUG-138470) SurfaceGallery does not start properly
* [QTBUG-138384](https://bugreports.qt.io/browse/QTBUG-138384) Incorrect documentation about one row surfaces
* [QTBUG-138492](https://bugreports.qt.io/browse/QTBUG-138492) qdoc: Snippet indentation issues
* [QTBUG-138462](https://bugreports.qt.io/browse/QTBUG-138462) QtGraphs pollutes the global namespace
* [QTBUG-138598](https://bugreports.qt.io/browse/QTBUG-138598) Setting series axis to null doesn't update the sizing
* [QTBUG-138740](https://bugreports.qt.io/browse/QTBUG-138740) Only bar graph works correctly with horizontal graph
orientation
* [QTBUG-138827](https://bugreports.qt.io/browse/QTBUG-138827) OIT causes artefacts in text rendering
* [QTBUG-138506](https://bugreports.qt.io/browse/QTBUG-138506) QtGraphs crash when GraphView is destroyed
* [QTBUG-138923](https://bugreports.qt.io/browse/QTBUG-138923) Gradient range doesn't update with aspectRatio
* [QTBUG-138924](https://bugreports.qt.io/browse/QTBUG-138924) Gradient does not work when starting up the app in some
cases
* [QTBUG-134003](https://bugreports.qt.io/browse/QTBUG-134003) QtGraphs pieSize and holeSize validate and render
differently
* [QTBUG-138797](https://bugreports.qt.io/browse/QTBUG-138797) Docs are messed up with * in some places
* [QTBUG-139112](https://bugreports.qt.io/browse/QTBUG-139112) QtGraphs AreaSeries inconsistent area filling
* [QTBUG-132009](https://bugreports.qt.io/browse/QTBUG-132009) LegendData cannot be instantiated
* [QTBUG-131117](https://bugreports.qt.io/browse/QTBUG-131117) Pie graph bugs
* [QTBUG-131111](https://bugreports.qt.io/browse/QTBUG-131111) LineSeries bugs
* [QTBUG-132107](https://bugreports.qt.io/browse/QTBUG-132107) 3D surface graph bugs
* [QTBUG-119683](https://bugreports.qt.io/browse/QTBUG-119683) Surface Graph Gallery example not fully responsive
* [QTBUG-132401](https://bugreports.qt.io/browse/QTBUG-132401) SplineSeries removeMultiple() malfunctioning and
incorrectly documented
* [QTBUG-133359](https://bugreports.qt.io/browse/QTBUG-133359) qtGraphs ValueAxis labelFormat does not support the same
formatting options that the qtCharts one
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-113837](https://bugreports.qt.io/browse/QTBUG-113837) Volume texture formats not handled
* [QTBUG-135930](https://bugreports.qt.io/browse/QTBUG-135930) multiple categories for the BarCategoryAxis overlaps
* [QTBUG-135887](https://bugreports.qt.io/browse/QTBUG-135887) points near the min/max of each axis get clipped
* [QTBUG-135691](https://bugreports.qt.io/browse/QTBUG-135691) Wasm build fails when linking both QtCharts and QtGraphs
* [QTBUG-138456](https://bugreports.qt.io/browse/QTBUG-138456) Documentation contains references to "QGraphsView" which
is a private class

### qtapplicationmanager (Commercial only)
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
* [QTBUG-136234](https://bugreports.qt.io/browse/QTBUG-136234) FAIL!  :
qml::ApplicationManager::test_applicationInterface() 'function returned
false' returned FALSE. ()
* [QTBUG-137008](https://bugreports.qt.io/browse/QTBUG-137008) FAILED: tests/data/packages C:/Users/qt/work/qt/qtapplic
ationmanager_standalone_tests/tests/data/packages
* [QTBUG-137056](https://bugreports.qt.io/browse/QTBUG-137056) Qt Application Manager - WindowObject Resizing Issue (Qt
6.8.3+)
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-135860](https://bugreports.qt.io/browse/QTBUG-135860) qt_add_qml_module(): Reject invalid inputs
* [QTBUG-99702](https://bugreports.qt.io/browse/QTBUG-99702) Qt module -tools package has both compile time and
runtime tools
* [QTBUG-136961](https://bugreports.qt.io/browse/QTBUG-136961) qtapplicationmanager: bubblewrap-example may need
bubblewarp

### qtinterfaceframework (Commercial only)
* [QTBUG-131579](https://bugreports.qt.io/browse/QTBUG-131579) [REG 6.8.0->6.8.1] building interfaceframework/remote
has FAILED and SUCCESFULL statements in output
* [QTBUG-132791](https://bugreports.qt.io/browse/QTBUG-132791) Attempt to promote imported target
"Python3::Interpreter" to global scope
* [QTBUG-133958](https://bugreports.qt.io/browse/QTBUG-133958) QDoc: error: Documentation warnings (9) exceeded the
limit (0) for 'QtInterfaceFramework'.
* [QTBUG-134742](https://bugreports.qt.io/browse/QTBUG-134742) The documentation and the snippet seem to be
contradicting
* [QTBUG-135435](https://bugreports.qt.io/browse/QTBUG-135435) interfaceframework/qifservicemanager.cpp:212:5: error:
unknown type name 'QElapsedTimer'
* [QTBUG-134684](https://bugreports.qt.io/browse/QTBUG-134684) A crash occurred in C:\Users\qt\work\qt\qtinterfaceframe
work_standalone_tests\tests\auto\core\qifabstractfeature\tst_qifabstract
feature.exe.
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qmlcompilerplus (Commercial only)
* [QTBUG-136126](https://bugreports.qt.io/browse/QTBUG-136126) error: no member named 'errorMessage' in
'QQmlJS::AotStatsEntry'
* [QTBUG-134790](https://bugreports.qt.io/browse/QTBUG-134790) QML AnchorChanges do not compile in strict mode
* [QTBUG-139431](https://bugreports.qt.io/browse/QTBUG-139431) Miscompilation of lists of inline components
* [QTBUG-124913](https://bugreports.qt.io/browse/QTBUG-124913) Weird compiler warning message when using unresolved
function
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-135795](https://bugreports.qt.io/browse/QTBUG-135795) QML Locale cannot be compiled in Direct Mode

### qtinsighttracker (Commercial only)
* [QTBUG-131763](https://bugreports.qt.io/browse/QTBUG-131763) DOC: Wrong link in to example sources
* [QTBUG-128736](https://bugreports.qt.io/browse/QTBUG-128736) DOC: Add missing configuration value
* [QTBUG-132587](https://bugreports.qt.io/browse/QTBUG-132587) error: ignoring return value of function declared with
'nodiscard' attribute [-Werror,-Wunused-result]
* [QTBUG-140160](https://bugreports.qt.io/browse/QTBUG-140160) FAIL!  : tst_QInsightEventFilter::trackEvents(button.ui)
Compared values are not the same

### qtvncserver (Commercial only)
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

Known Issues
------------
* Check that your system meets Qt's requirements:
  https://doc-snapshots.qt.io/qt6-6.10/supported-platforms.html
* RTA reported issues from Qt 6.10
  https://qt-project.atlassian.net/issues/?filter=10825
* See Qt 6.10 known issues from:
  https://wiki.qt.io/Qt_6.10_Known_Issues
* Qt 6.10.0 Open issues in Jira:
  https://qt-project.atlassian.net/issues/?filter=10708

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
Soheil Armin  
YAMAMOTO Atsushi  
Xavier BESSON  
Mahmoud Badri  
Mate Barany  
Thierry Bastian  
Valentin Batz  
Sebastian Beckmann  
Vladimir Belyavsky  
Nicholas Bennett  
Jules Bertholet  
Eric Beuque  
Lena Biliaieva  
Wang Bin  
Tim Blechmann  
Maximilian Blochberger  
Eskil Abrahamsen Blomfeldt  
David Boddie  
Tatiana Borisova  
Joerg Bornemann  
Rym Bouabid  
Assam Boudjelthia  
Carlo Bramini  
Aurélien Brooke  
Kai Uwe Broulik  
Michael Brüning  
Alex Bu  
Benjamin Buch  
Olivier De Cannière  
Méven Car  
Alexei Cazacov  
Li Changze  
Kaloyan Chehlarski  
Mike Chen  
Michael Cho  
Wang Chuan  
Albert Astals Cid  
Ece Cinucen  
Jonathan Clark  
Ed Cooke  
Alexandru Croitor  
Mitch Curtis  
Thibaut Cuvelier  
Giuseppe D'Angelo  
Szabolcs David  
Quentin Deldycke  
Ali Can Demiralp  
Pavel Dubsky  
Paul Dubsky  
Artem Dyomin  
Alexey Edelev  
David Edmundson  
Oliver Eftevaag  
Christian Ehrlicher  
Hatem ElKharashy  
Andreas Eliasson  
Amr Essam  
David Faure  
Ilya Fedin  
Nicolas Fella  
Tobias Fella  
Ilya Flikov  
Andrew Forrest  
Isak Fyksen  
Joshua GPBeta  
Samuel Gaist  
Zoltan Gera  
Christophe Giboudeaux  
Frederik Gladhorn  
Joshua Goins  
Julian Greilich  
Robert Griebl  
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
Andreas Hartmetz  
Elias Hautala  
Tero Heikkinen  
Jani Heikkinen  
Miikka Heikkinen  
Moss Heim  
Jari Helaakoski  
Johan Klokkhammer Helsing  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Dominik Holland  
Benedikte Holm  
Zhang Hongyuan  
Mats Honkamaa  
Xaver Hugl  
Jimi Huotari  
Samuli Hölttä  
Thorbjørn Martsum / Mjølner Informatics  
Masoud Jami  
Morteza Jamshidi  
Allan Sandfeld Jensen  
Tim Jenßen  
Liu Jinchang  
Jukka Jokiniva  
Teemu Jokitulppo  
Jonas Karlsson  
Igor Khanin  
Ahmed El Khazari  
Ali Kianian  
Marius Kittler  
Friedemann Kleint  
Peter Kling  
André Klitzing  
Michal Klocek  
Jarek Kobus  
Tobias Koenig  
Sze Howe Koh  
Jarkko Koivikko  
Niko Korkala  
Tomi Korpipää  
Jani Korteniemi  
Fabian Kosmale  
Volker Krause  
Mike Krus  
Anton Kudryavtsev  
Santhosh Kumar  
Jonas Kvinge  
Kai Köhne  
Antonio Larrosa  
Cristian Le  
Inho Lee  
Elvis Lee  
Frédéric Lefebvre  
Paul Lemire  
Wladimir Leuschner  
Jørgen Lind  
Felix Lionardo  
Jie Liu  
Pawel Lopko  
Jarno Lämsä  
Robert Löhning  
Thiago Macieira  
Christophe Marin  
Thorbjørn Lund Martsum  
Leena Miettinen  
Shveta Mittal  
Jan Moeller  
Thomas Moerschell  
Safiyyah Moosa  
Sheree Morphett  
Stan Morris  
Bartlomiej Moskal  
Marc Mutz  
Tommi Mänttäri  
Antti Määttä  
Martin Negyokru  
Andy Nichols  
Mårten Nordheim  
Dennis Oberst  
Matti Paaso  
Tinja Paavoseppä  
Kwanghyo Park  
Jerome Pasion  
Mikhail Paulyshka  
Jose Dapena Paz  
Miika Pernu  
Mauro Persano  
Evgen Pervenenko  
Samuli Piippo  
Karim Pinter  
Timur Pocheptsov  
Lauri Pohjanheimo  
Milla Pohjanheimo  
Joni Poikelin  
Jacek Poplawski  
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
Jaime Resano  
Konstantin Ritt  
David Rosca  
Bernhard Rosenkränzer  
Shawn Rutledge  
Otto Ryynänen  
Emir SARI  
Toni Saario  
Casimir Saastamoinen  
Ahmad Samir  
Timon Sassor  
Lars Schmertmann  
Carl Schwan  
Michal Seben  
SanthoshKumar Selvaraj  
Andrii Semkiv  
Luca Di Sera  
Sami Shalayel  
Raman Shamotsin  
Andy Shaw  
Tian Shilin  
Xu Shitong  
Venugopal Shivashankar  
Pierre-Yves Siret  
Harald Sitter  
Kristoffer Skau  
Nils Peter Skålerud  
Nils Petter Skålerud  
Daniel Smith  
Ivan Solovev  
Axel Spoerl  
Patrick Stewart  
Alexander Stippich  
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
Ovidiu Tepescu  
Marcus Tillmanns  
Aleksandr Timofeev  
Elias Toivola  
Daniel Trevitz  
Jens Trillmann  
Jere Tuliniemi  
Shantanu Tushar  
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
Stefan Wastl  
Ole Wegen  
Michael Weghorn  
Bernd Weimer  
Edward Welbourne  
Paul Wicking  
Piotr Wierciński  
Oliver Wolff  
Milian Wolff  
Shitong Xu  
Semih Yavuz  
Marianne Yrjänä  
Zhao Yuhang  
Vlad Zahorodnii  
Oleksii Zbykovskyi  
Alexey Zerkin  
Yuhang Zhao  
Yifan Zhu  
Eike Ziller  
Nic Zonta  
Dilek Akçay Öztüzün  
Michał Łoś  
