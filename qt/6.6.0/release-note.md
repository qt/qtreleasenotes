Release note  
============  

Qt 6.6 introduces many new features and improvements as well as bugfixes  
over the 6.5.x series. For more details, refer to the online  
documentation included in this distribution. The documentation is also  
available online:  
  
https://doc.qt.io/qt-6/index.html  
  
The Qt version 6.6 series is binary compatible with the 6.5.x series.  
Applications compiled for 6.5 will continue to run with 6.6.  
  
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
* CVE-2023-38197 in qtbase  
* CVE-2023-43114 in qtbase  
* CVE-2023-32763 in qtbase  
* CVE-2023-37369 in qtbase  
* CVE-2023-34410 in qtbase  
* CVE-2023-33285 in qtbase  
* CVE-2023-32762 in qtbase  
  
### qtbase  
* 9773f0175c Return qt-configure-module to bin/  
Upon further consideration, qt-configure-module was deemed user-facing,  
and was thus moved back to ./bin on all platforms.  
  
* 05e72d53a6 PCRE2: upgrade to 10.42  
PCRE2 has been updated to 10.42.  
  
* ca64365e3a Don't hide object replacement char except in rich text  
The object replacement character (U+FFFC) is now only filtered out in  
rich text controls, where they represent inline objects. In other  
controls, its glyphs will be shown as with other text.  
  
* 8892819d0c windows: Fix vertical metrics with GDI engine  
Fixed an issue where the line gap of some fonts would be included twice  
in the font's leading.  
  
* 0657b0734e Add QCryptographicHash::supportsAlgorithm() to check  
supported algorithm  
Add supportsAlgorithm() method that can be used to query OpenSSL and  
check whether the selected algorithm is supported.  
  
* 8602a224b6 QT_INLINE_SINCE: never inline for static Qt builds  
Restored binary compatibility for static Qt builds broken by the  
QT_INLINE_SINCE mechanism. Qt still does not guarantee BC for static  
build configurations otherwise.  
  
* 8f2d5a5649 CMake: Enforce QT_RESOURCE_ALIAS for absolute paths in  
resources  
In Qt resources, files that are specified as absolute paths must have  
the property QT_RESOURCE_ALIAS set.  
  
* eac9f39517 SQLite: Update SQLite to v3.40.0  
Updated SQLite to v3.40.0  
  
* 26c190f57e QTest::WatchDog: fix missing timeout resets on test  
function change  
Fixed a bug which caused QTEST_FUNCTION_TIMEOUT to be applied to the  
whole test execution, as opposed to each test function.  
  
* 02f1e72d5a Android: Set EnterKeyNext as default type for QLineEdit  
EnterKey type is now changed from EnterKeyDefault to EnterKeyNext for  
virtual keyboard in QLineEdit. It is done only if the focus can be moved  
to widget below.  
  
* 936cae6b53 Add QFileInfo::readSymLink() to read the raw link path  
Added readSymLink() to read the symlink's raw target, without resolving  
to an absolute path.  
  
* b82c9d08f8 QFileInfo: overload file time related methods to take a  
QTimeZone arg  
Overload file time related methods to take QTimeZone argument; mainly  
useful if all you need is UTC time, e.g. to compare file timestamps,  
this is inherently faster as no conversions need to be performed.  
  
* f68a2316d8 Long live QPromise::addResults()!  
Added addResults() to report multiple results at once.  
  
* 2b2065bf35 Slow Deprecation of FILENAME_VARIABLE, replacement by  
OUTPUT_SCRIPT  
The FILENAME_VARIABLE option of qt_generate_deploy_script and  
qt_generate_deploy_app_script is now deprecated, use OUTPUT_SCRIPT  
option instead.  
  
* cac325fdc1 SQLite: Update SQLite to v3.40.1  
Updated SQLite to v3.40.1  
  
* fe7a0c19a6 QFileSystemModel: add lastModified() overload that takes a  
QTimeZone  
Added lastModified() overload that takes a QTimeZone, this is useful  
when e.g. comparing file timestamps and all that's needed is time in UTC  
(this is faster as no time zone conversions is required). QTimeZone::UTC  
is used internally when sorting by time (using the sort() function),  
which should ideally make it faster too.  
  
* f6b026eed1 Move QTypeInfo<std::pair> from qpair.h to qtypeinfo.h to  
avoid ODR violation  
The QTypeInfo for std::pair/QPair will now be correct even if qpair.h  
hasn't been included, fixing an One-Definition-Rule (ODR) violation.  
  
* 595360506d QSqlRecord: add missing C++11 move SMFs  
Added move constructor, -assignment operator, and swap().  
  
* 19ca03c21c QUnicodeTools: Use thread-safe libthai API  
Correct line wrapping of Thai text now requires libthai version 0.1.25  
or above.  
  
* 03ed57afa0 Move QApplication::autoSipEnabled() to public scope  
bool QApplication::autoSipEnabled() is no longer a slot. Code such as  
using QObject::connect() to connect to it as a slot or accessing it  
through meta object system will have to be rewritten.  
  
* 2d1fd400fc Object to creating duplicate entries in a test-data table  
Duplicate data tags are now warned about. Every call to QTest::newRow()  
or QTest::addRow() should result in a distinct data tag. If they do not,  
a warning is produced. Likewise, duplicate column names are forbidden;  
each call to QTest::addColumn() should use a distinct name.  
  
* 5e76a9569e xkbcommon: make shortcuts persistent across layouts  
make keys produce the same shortcuts independently of current layout  
  
* d4f72b4de6 QStandardPaths/unix: ignore relative paths in all $XDG_*  
env vars  
Improved conformance to the Freedesktop basedir spec by ignoring any  
relative paths in XDG_* environment variables.  
  
* 40dd38813c QMimeDatabase: don't stat() something that isn't a local  
file  
Fixed a regression from 6.4.0 that made certain QMimeDatabase functions  
that inspected file contents to fail on Unix systems, if the file was  
not a native file (e.g., a Qt resource).  
  
* 7cbdc8abbd QVarLengthArray: add STL-style assign()  
Added assign().  
  
* 26fec96a81 QString, QByteArray: don't detach in  
removeIf/erase/eraseif()  
Removing characters from a currently shared string or byte array is now  
done more efficiently  
  
* cc6324665e QString: don't detach in insert()  
Calling insert() on a currently shared string is now done more  
efficiently.  
  
* 3a3b76e040 QString: don't detach in insert(qsizetype, QUtf8StringView)  
Inserting Utf8 data (e.g. a QUtf8StringView) into a currently shared  
QString is now done more efficiently.  
  
* eb60e94020 QString: don't detach in replace_helper()  
Using replace() on a currently shared QString is now done more  
efficiently  
  
* fc33fea999 Don't do font merging for PUA characters  
Font merging (automatic assignment of alternative fonts) is no longer  
applied for characters in the Private Use Areas of Unicode.  
  
* 224930726b Long live QScopedPropertyUpdateGroup  
New RAII class wrapping Qt::beginPropertyUpdateGroup() and  
Qt::endPropertyUpdateGroup().  
  
* b73574c4a6 SQL/MySQL: add options to explicitly specify the protocol  
type  
Added the ability to specify the MySQL/MariaDB connection type using  
the "MYSQL_OPT_PROTOCOL" connection string option. In case the  
connection type is "MEMORY" for shared memory, applications can specify  
the shared memory segment name using the "MYSQL_SHARED_MEMORY_BASE_NAME"  
option.  
  
* fbfee2d7c5 QVarLengthArray: clear() is not resize(0)  
clear() no longer requires the value_type to be default-constructible.  
  
* 94efcf9be4 Update bundled libjpeg-turbo to version 2.1.5  
libjpeg-turbo was updated to version 2.1.5  
  
* 0b4286ff28 Windeployqt: add custom qml output directory command line  
option  
Windeployqt's default behavior is now to deploy qml imports to a "qml"  
directory inside the deploy directory, rather than directly to the  
deploy directory.  
  
* fd70555b33 Deprecate usage of qt_ntfs_permission_lookup  
Deprecated the variable qt_ntfs_permission_lookup to avoid race  
conditions while enabling or disabling permission checks. It can be  
replaced by the RAII class QNtfsPermissionCheckGuard or with the  
functions qEnableNtfsPermissionChecks(), qDisableNtfsPermissionChecks()  
and qAreNtfsPermissionChecksEnabled().  
  
* 6d17697913 QFileSystemWatcher/Win: remove the pre-QFileInfo path  
normalization  
Fixed a bug that prevented removePaths() from removing the root of a  
drive on Windows.  
  
* c889ffed9f QTextStream: make dtor non-virtual come Qt 7  
Inheriting QTextStream is deprecated. QTextStream will no longer have a  
virtual destructor in Qt 7. If your code inherits QTextStream, port to a  
design that doesn't require a polymorphic QTextStream. You may define  
the macro QT_NO_INHERITABLE_TEXT_STREAM to mark QTextStream as final to  
assist you in checking for such code. This is the default if you're  
compiling with QT_DISABLE_DEPRECATED_UP_TO set to Qt 6.9.  
  
* 610bafdfc5 qxkbcommon: Treat XKB_KEY_{Super,Hyper}_{L,R} as  
Qt::Key_Meta by default  
Super ("Win" key) and Hyper keys will no longer produce the  
corresponding Qt::Key_Super or Qt::Key_Hyper key events, but will  
instead be mapped to Qt::Key_Meta and result in Qt::MetaModifier being  
set.  
  
* 0efd8854c4 A QtSql driver for Mimer SQL  
Added a QtSql plugin to work with the Mimer SQL database  
  
* bb2ff8a69f qdoc: Add *.webp as an default image suffix  
*.webp has been added to the list of default image suffixes.  
  
* 0fe6f818d2 Text: fix Soft hyphen rendering in QTextLayout::glyphRuns()  
Fixed an issue where spaces would sometimes be shown in soft hyphen  
positions in a string.  
  
* 05f913d57d qstrncpy: NUL-terminate even when src is nullptr  
Now NUL-terminates the target buffer even when the source pointer is  
nullptr, provided the target buffer has space for at least one byte.  
  
* 4183768d9b CMake: Fix position independent code linker flags not being  
set  
Qt tools are now built with position independent code even with Unix  
toolchains where this is not the default, for example clang.  
  
* 2a2fc4d16d QMessageAuthenticationCode: remove lazy initialization of  
messageHash  
No longer delays processing of the key to the first setData() or  
result() call. While passing a default-constructed key to the  
constructor and then calling setKey() continues to work, for optimal  
performance, we suggest to pass the actual key as a constructor argument  
and call setKey() only to change the key.  
  
* 738c48244b Android: use FileProvider with QDesktopServices::openUrl()  
Add AndroidX dependency to Gradle builds by default since it's required  
by FileProvider.  
  
* 863eb576c8 Remove qmake files that provide support for building Qt  
modules  
Support for building Qt modules with qmake was removed.  
  
* 8f33a0424f SQLite: Update SQLite to v3.41.0  
Updated SQLite to v3.41.0  
  
* 6990f23813 Long live QMessageAuthenticationCode::resultView()!  
Added QCryptographicHash-style resultView().  
  
* f5358e5932 a11y: Add new relations DescriptionFor, Described,  
Flows{From,To}  
Added new relation flags DescriptionFor, Described, FlowsFrom and  
FlowsTo.  
  
* 4b197c3f52 QRegularExpression: add support for non-filepath  
wildcards/globbing  
Support for non-filepath wildcards has been added to  
wildcardToRegularExpression().  
  
* 4ec5c0efc7 SQL/ODBC: Return all native error codes  
QSqlError::errorCode() might return a semicolon separated list of  
native error codes.  
  
* f2fc2013de QErrorMessage: Reset 'again' check box between each error  
message  
QErrorMessage will now reset the check box for showing a message again  
for each new message shown, as each individual message has its own  
suppression state.  
  
* 7261a22987 QAbstractItemModel: fix match() with Qt::MatchWildcard  
QAbstractItemModel::match() now uses more generic wildcard matches  
rather than file path globbing. Please refer to the documentation of  
QRegularExpression::wildcardToRegularExpression() for more information  
about the differences.  
  
* f030037d24 Implement qstrncpy() in terms of std::strncat()  
On non-Windows platforms, no longer writes to all bytes of the target  
buffer, but stops after the terminating NUL. This was already the  
behavior on Windows.  
  
* 30de1f74de SQL/MySQL: Add support for Bit-Value Type - BIT  
Added handling for Bit-Value Type - BIT.  
  
* 0d29a406f7 QThread: add sleep(std::chrono::nanoseconds) overload  
Added sleep(std::chrono::nanoseconds) overload.  
  
* 5bffb47d6e QFSFileEngine: fix overflow bug when using lseek64  
Fixed a bug where opening a file in append mode may fail if the file  
size was bigger than INT_MAX.  
  
* e7b8b7bfbe CMake: Add NO_COMPILER_RUNTIME to deploy script macros  
Added the option NO_COMPILER_RUNTIME to qt_generate_deploy_app_script.  
  
* c5d4dde678 QMessageAuthenticationCode: add move SMFs and swap()  
Added move constructor, move assignment operator and swap() function.  
  
* c19f9716fb QMessageAuthenticationCode: port to QByteArrayView [3/3]:  
static hash()  
The constructor, setKey(), addData() methods as well as the static  
hash() function take arguments by QByteArrayView instead of QByteArray  
now.  
  
* 82b75570f0 QProcess/Linux: fix file descriptor leak in case of failed  
child start  
Fixed a file descriptor leak in QProcess when running on Linux 5.4 or  
later, if the executable being run failed to start (for example, the  
file for the executable didn't exist).  
  
* 17e4b2d8ed SQLite: Update SQLite to v3.41.1  
Updated SQLite to v3.41.1  
  
* 092563a3d0 Skip QTimeZone::isTimeZoneIdAvailable()'s validity check on  
Unix  
On Unix (other than macOS and Android), the TZ-DB backend has long  
accepted any well-formed POSIX zone description as a time-zone ID. This  
is now reflected in QTimeZone::isTimeZoneIdAvailable(), which previously  
claimed not to accept these IDs. However, avaliableTimeZoneIds() still  
does not attempt to construct all possible POSIX descriptors to include  
in its return.  
  
* 617165af6b QProcess: reimplement systemEnvironment() using  
QProcessEnvironment  
Fixed a bug that would cause systemEnvironment() to produce corrupted  
entries (mojibake) on Windows if the environment contains characters  
outside of the ANSI character set.  
  
* 3f40a8b5b1 Add QTextListFormat::start: html and markdown ordered list  
index offset  
QTextList now supports specifying a start index using the new  
QTextList::{setStart, start} functions. The HTML start attribute on  
ordered lists in rich text documents is now parsed and used when  
rendering a text list. Non-negative indices in markdown lists are now  
also parsed and written properly. This allows starting a list with a  
different number than 1.  
  
* eb9c8042cf Short live QT_ENABLE_P0846_SEMANTICS_FOR!  
Fixed manual get<I>() calls (Tuple Protocol) in C++17 mode.  
  
* a1889b2a67 Verify fix for manual get<I> calls for QVector<N>D  
Fixed manual get<I>() calls (Tuple Protocol) in C++17 mode.  
  
* 4d90c4e74a QTimer: fix new-style slot invocation for receiver in  
another thread  
Fixed a bug that caused slots connected to single-slot timers using the  
new-style connection mechanism to be delivered in the wrong thread.  
  
* a9e8034e8c Implement [variant.get] for QVariant [2/2]: get()  
Implemented the type-based std::variant access protocol  
(get<T>()/get_if<T>()) to allow easier access to the contained element  
than the previous solution of casting data(), as well as to allow  
generic code to treat QVariant and std::variant the same. The  
holds_alternative<T>() function is not provided, since it's the same as  
get_if<T> != nullptr. The index-based variant access functions  
(get<I>()/get_if<I>()) are also not provided, because, unlike  
std::variant, QVariant does not have a bounded number of alternative  
types, and QMetaType IDs are not (all) compile-time constants.  
  
* 5a182d35e2 Update license specification for PCRE2  
Clarifying license of PCRE2 to be BSD-3-Clause with advertisement  
exception for binary-like packages.  
  
* f8dba0395f QPromise: add support for addResult(braced-initializer)  
Added support for calls to addResult() with braced initializers.  
  
* 9a39b3c796 Apply ScaleFactorRoundingPolicy to QT_SCREEN_SCALE_FACTORS  
The high-DPI scale factor rounding policy (settable with  
QGuiApplication::setHighDpiScaleFactorRoundingPolicy() or  
QT_SCALE_FACTOR_ROUNDING_POLICY) now applies to scale factors set with  
QT_SCREEN_SCALE_FACTORS.  
  
* c4debab927 Introduce QTP0002 policy for android-specific target  
properties  
Target properties that specify android-specific paths now support  
generator expressions, but these generator expressions must be evaluated  
to valid JSON strings. The behavior is controlled by the policy QTP0002.  
The OLD policy behavior is deprecated and the NEW behavior is preferred  
for use.  
  
* b46a914bd7 SQLite: Update SQLite to v3.41.2  
Updated SQLite to v3.41.2  
  
* 2f709952cf QSqlError: also compare nativeErrorCode() in operator==() /  
operator!=()  
The comparison operators have been fixed to take both error type and  
error code into account.  
  
* c080d1e64d Create any callable using QRunnable::create  
QRunnable::create can now take non-copyable functions as argument.  
  
* 87103e04e9 QMultiHash: fix missing update to m_size  
to not be counted, resulting in a hash map with an incorrect element  
count and which could cause an assertion failure depending on how the  
hash was later mutated.  
  
* 2f226336a2 QPluginLoader: don't instantiante multiple, identical  
instances  
staticInstances() will not call duplicated registrations of the same  
instantiation function, which can only happen as a result of duplicated  
Q_IMPORT_PLUGIN for the same plugin name.  
  
* 7f38f9f394 Long live QtFuture::makeReadyRangeFuture()  
Introduce QtFuture::makeReadyRangeFuture(). This method takes a  
container which has input iterators and returns a multi-value  
QFuture<ValueType>, where ValueType is the underlying type of the input  
container.  
  
* 9b4b32ec98 Long live QtFuture::makeReadyVoidFuture() and  
QtFuture::makeReadyValueFuture()  
Added QtFuture::makeReadyVoidFuture() and  
QtFuture::makeReadyValueFuture().  
  
* 028c367f75 Deprecate QtFuture::makeReadyFuture()  
The QtFuture::makeReadyFuture() method and all its specializations are  
deprecated since Qt 6.10. The reason for the deprecation is that the  
method has a makeReadyFuture(const QList<T> &) overload, which behaves  
differently from all other overloads (including other non-const ref  
QList overloads). Use QtFuture::makeReadyVoidFuture() when you need a  
ready void QFuture, or QtFuture::makeReadyValueFuture() when you need to  
propagate the input type to the returned QFuture, or  
QtFuture::makeReadyRangeFuture() when you need to create a multi-value  
future based on an input container.  
  
* 39fab09aad SQL/MySQL: add option MYSQL_OPT_TLS_VERSION &  
MYSQL_OPT_SSL_MODE  
Added the two new connect options MYSQL_OPT_TLS_VERSION and  
MYSQL_OPT_SSL_MODE.  
  
* 3983babd71 QSqlQuery: add boundValueName()/boundValueNames()  
Added two new functions boundValueName()/boundValueNames() to return  
the names of the bound values.  
  
* 2f95cd8f8b Long live QPromise::emplaceResult/At()!  
Added emplaceResult() and emplaceResultAt() member functions.  
  
* db346e711c Fix accessibility on XCB when running as root  
On XCB applications running as root are now accessible.  
  
* 24fe86ebe7 CMake: Store unsanitized plugin type names in module .json  
files  
The module information JSON files now contain the unsanitized plugin  
types of a module, e.g. wayland-decoration-client instead of  
wayland_decoration_client. Consumers of the module information file must  
sanitize plugin types themselves if necessary.  
  
* 25530c7020 win: Fix default fallback font for some languages  
Fixed an issue querying a default font for certain languages not  
supported by the primary system font.  
  
* 3d0fb2cea9 Windeployqt: Add a check for LLVM-MinGW runtimes  
Windeployqt now supports LLVM-MingGW runtimes.  
  
* 87535e4e43 QTimer: optimize single shot timers that cross thread  
Single-shot timers with a string-based connection are now started in  
the receiver's thread, not in the thread that creates the timer.  
  
* e1818d9e9c QXmlStreamAttributes: port value()/hasAttribute() to  
QAnyStringView  
Ported value() and hasAttribute() to QAnyStringView.  
  
* 55a51e1909 Implement QXmlStreamReader::hasStandaloneDeclaration()  
added hasStandaloneDeclaration()  
  
* 5dabac2c9c Change QTimeZone's offset range into constants, not an enum  
The MinUtcOffsetSecs and MaxUtcOffsetSecs constants are now static  
constexpr members of QTimeZone, rather than members of an anonymous  
enum. Their values are now 16 hours either side of zero, to allow for  
some historical zones.  
  
* 968250ee14 QMetaProperty: add write() overload taking rvalue QVariant  
Added write() overload taking an rvalue QVariant.  
  
* 5f28d367d9 Make QPointer<T> constructible from QPointer<X>  
QPointer<T> can now be (move- and copy-)constructed from QPointer<X>.  
  
* 959800f6de Short live Q_NODISCARD_CTOR  
attribute for constructors on compilers that support it, and does  
nothing on other compilers.  
  
* 29b2506e8c Allow disable native messagebox dialog  
Added options functionality to QMessagebox. The currently only option  
available is DontUseNativeDialog.  
  
* b6d04c8a82 QMetaProperty: add writeOnGadget() overload taking rvalue  
QVariant  
Added writeOnGadget() overload taking an rvalue QVariant.  
  
* 0e7e1c3396 Take move-only functions for the threadpool  
Methods taking callable functions, can now take move-only lambdas.  
  
* 275e0e48a9 Deprecate Q_ASSUME  
The Q_ASSUME macro is now deprecated. Do not use it in new code and  
consider removing it from existing code.  
  
* 2162e0dfc4 Schannel: Add support for import of PKCS12/PFX files  
Add support for PKCS12 import with Schannel backend.  
  
* 3bf5b5f894 Use QSlotObject helpers in functor-cases of  
QMetaObject::invoke  
Using a functor with several operator() overloads in  
QMetaObject::invokeMethod now causes a compile time error. Qt would  
previously ignore const and noexcept overloads and always call the  
mutable version on a copy of the functor.  
  
* 1373a20f99 QTestEventLoop: don't stop the test fails outside the main  
thread  
The QTestEventLoop no longer attempts to exit its event loop if the  
failure was detected outside the main thread.  
  
* a2551c45d4 Move the formatting of <chrono> durations to QDebug &  
QtTest  
Added pretty formatting of C++ <chrono> durations.  
  
* 6160ea45b6 Implement API for enabling / disabling OpenType features  
Added an API to QFont which makes it possible to enable and disable  
specific typographic features in OpenType fonts.  
  
* 8c0153a526 Fix QMenu (+other theme) sizes on Windows multiscreen  
systems  
Fixed menu sizes on Windows systems with more screens.  
  
* 0306247f5a Remove Java iterator APIs for moving back if operator-- is  
not available  
QSetIterator no longer has a hasPrevious() member function. The  
underlying iterator doesn't implement operator--(), so couldn't be moved  
backwards anyway.  
  
* ec0e0d1e81 QDeadlineTimer: make it so any negative millisecond count  
is "forever"  
QDeadlineTimer will now interpret negative millisecond remaining times  
as "forever", instead of only the value -1. This brings the API closer  
in line with other API like QMutex. This change does not apply to the  
nanosecond counts in the API, nor to the API based on std::chrono.  
  
* 305f61a807 Remove the -sysroot option from configure  
The -sysroot option was removed. Use CMAKE_SYSROOT or  
CMAKE_TOOLCHAIN_FILE instead.  
  
* 7dba2c8761 QDnsLookup/Unix: make sure we don't overflow the buffer  
Fixed a bug that could cause a buffer overflow in Unix systems while  
parsing corrupt, malicious, or truncated replies.  
  
* 29b2fe40dc Revert commit "don't ever force fork() instead of forkfd()"  
Reverted a change from Qt 6.0 that made the childProcessModifier()  
callback be run in a child created by means other than a real fork()  
library call, a situation in which certain other library functions would  
be unusable, unreliable, or cause deadlocks. A flag to opt in to the  
solution with better performance will be added to Qt 6.6.  
  
* 9a73bc5f3d QDnsLookup/Windows: use DnsQueryEx so IPv6 servers are  
supported  
setNameserver() now supports IPv6 servers with on Apple systems, AIX,  
FreeBSD, NetBSD, Solaris, and Windows.  
  
* 48b6c8503a QProcess/Unix: enable setChildProcessModifier for  
startDetached  
The modifier function set with setChildProcessModifier() will now also  
be executed when the process is started with startDetached().  
  
* bbbe5f45c4 QList: add STL-style assign()  
Added assign().  
  
* 365af87f94 QDnsLookup/Windows: don't append domain search suffixes  
QDnsLookup on Windows will no longer append the system's configured  
domain name for look ups that contained only a single label (that is, no  
dots). This matches the Unix behavior.  
  
* b40ab2f8a6 SQLite: Update SQLite to v3.42.0  
Updated SQLite to v3.42.0  
  
* 8566c2db85 QUuid: add support for 128-bit integers  
Added support for converting between QUuid and quint128, on platforms  
that offer 128-bit integer types (all 64-bit ones supported by Qt,  
except MSVC).  
  
* f9c87cfd44 QProcess/Unix: add setUnixProcessParameters()  
Added setUnixProcessParameters() function that can be used to modify  
certain settings of the child process, without the need to provide a  
callback using setChildProcessModifier().  
  
* bce7009f55 QDnsLookup: add support for setting the port number of the  
server  
Added setNameserverPort().  
  
* c7af8d5808 Deprecate qAsConst()  
qAsConst() is now deprecated. You can simply globally search and  
replace "qAsConst" with "std::as_const" in your code-base.  
  
* 07d6d31a4c QFuture: Gracefully handle a destroyed context in  
continuations  
Added support for context objects of continuations being destroyed  
before the continuation finishes. In these cases the future is cancelled  
immediately.  
  
* 39cdf431f0 QObject: add setProperty() overload taking rvalue QVariant  
Added setProperty() overload taking an rvalue QVariant.  
  
* 6f529c38ce QVariant::fromStdVariant(): protect against accidental  
fromValue() ADL pick-ups  
The fromStdVariant() function used an unqualifed fromValue() call to  
convert each alternative type in the std::variant. It now uses qualified  
QVariant::fromValue() to avoid picking up unrelated fromValue()  
overloads whose return value just happens to implicitly convert to  
QVariant.  
  
* 18a2c62c07 QByteArray: add STL-style assign()  
Added assign().  
  
* f564e905c1 QVariant: Support emplace  
Implemented in-place construction for QVariant. The constructor taking  
std::in_place_type<Type> constructs an object of type Type directly  
inside QVariant's storage, without any further copy or move operations.  
QVariant::emplace() does the same when replacing the content of an  
existing QVariant and tries to reuse previously-allocated memory.  
  
* 1d3ae5f0e9 cmake: Add known translations to CFBundleLocalizations in  
Info.plist  
Translations added via qt_add_translations are now reflected as  
CFBundleLocalizations entries in the application's Info.plist file on  
Apple platforms. to disable this behavior, set  
QT_NO_SET_PLIST_LOCALIZATIONS.  
  
* 1eb4d17cb4 Generate and set a CFBundleIdentifier when none were  
provided on macOS  
When using Ninja generator, if neither  
`XCODE_ATTRIBUTE_PRODUCT_BUNDLE_IDENTIFIER` nor  
`MACOSX_BUNDLE_GUI_IDENTIFIER` is provided for a target, a bundle  
identifier, i.e., `com.yourcompany.<teamid>.<target>` will be generated  
and set as CFBundleIdentifier.  
  
* 79ae79d05c QVariant::fromValue: Add rvalue optimization  
Added fromValue() overload taking rvalues.  
  
* 8983225d3c QVariant: add rvalue overload of fromStdVariant()  
Added overload of fromStdVariant() taking rvalue std::variant<>s.  
  
* 8b6bd8ed99 QDnsLookup: allow looking up the root domain  
It is now possible to look up the root DNS domain, by setting the name  
property to an empty string. This query is usually done while setting  
the query type to NS.  
  
* ef1be84551 QStringDecoder: add a char16_t overload of  
appendToBuffer(QChar*, ~~~)  
Added appendToBuffer() overload for char16_t*, complementing the  
existing overload taking QChar*.  
  
* 54d8d8055e QString: add STL-style assign() [1/4]: non-(it,it)  
overloads  
Added assign().  
  
* e6fb3b4ea0 QPixmapCache: fix leaking of QStrings and Keys on clear()  
Fixed QString key data not being freed on clear().  
  
* 7a42679a98 Freetype: Don't do image transform for translations  
Fixed an issue where setting a translation matrix on text using a  
bitmap font would cause rendering artifacts.  
  
* 2948ab16ea QPixmapCache: deprecate replace()  
The `replace(key, pixmap)` function has been deprecated, because  
passing a `const Key` to it results in undefined behavior. Use  
`remove(key, pixmap)` followed by `key = insert(pixmap)` instead.  
  
* 56598b65fa Fix no-op emission of QComboBox::currentTextChanged  
emit currentTextChanged only, if currentText changes.  
  
* 211ff8ac53 QPixmapCache: Move qHash(Key) from _p.h to public header  
Made the qHash() overload for QPixmapCache::Key public (was: private)  
API.  
  
* f1adc51ca4 QFutureSynchronizer: fix aliasing problem in setFuture()  
Fixed a crash in setFuture() if the argument was already a member of  
QFutureSynchronizer::futures().  
  
* a9c29029d3 Consult QIcon::fallbackThemeName() even for themes with  
explicit parents  
QIcon::fallbackThemeName() will now be used as fallback even for themes  
that declare a parent theme.  
  
* c00d99d96e Consult QIcon::fallbackSearchPaths() even when theme name  
is empty  
QIcon::fallbackSearchPaths() will now be consulted for fallback icons  
even if the current theme name is empty.  
  
* abd60e9592 SSL: upgrade the default DH parameters  
The default Diffie-Hellman parameters are now using the 2048-bit MODP  
group from RFC 3526.  
  
* c131e159b0 Introduce QT_SYNC_HEADERS_AT_CONFIGURE_TIME flag  
When building Qt from sources, syncqt and Qt header files are now  
created at build time, not configure time. This should speed up the  
configuration step. You can set the CMake variable  
QT_CONFIGURE_TIME_SYNC_HEADERS to ON to use the previous behavior,  
though. The old behavior is also preserved if cmake/configure is run  
from inside an IDE - Qt Creator, Visual Studio Code, and CLion are  
currently detected.  
  
* f03c7e4a2d Introduce -no-vcpkg flag for disabling vcpkg  
detection/integration  
vcpkg detection, and integration can be disabled by passing the -no-  
vcpkg flag to the configure command, or by passing `-DQT_USE_VCPKG=OFF`  
to the cmake command.  
  
* 51dc94df9c QGtk3Theme: Do not default Active WindowText to button  
foreground  
Default to GTK Entry Text / Normal Text / qt_fusionPalette  
  
* d117cd5f3a QPixmapCache: ignore insertion or searches with empty key  
Trying to insert or find a pixmap with an empty key string now always  
fails immediately.  
  
* cb3416696f Update bundled libpng to version 1.6.40  
libpng was updated to version 1.6.40  
  
* 32f93394ef CMake: Don't use VCPKG_DEFAULT_TRIPLET for triplet  
deduction  
Qt no longer uses the VCPKG_DEFAULT_TRIPLET environment variable to  
deduce target triplet. By default we let vcpkg's toolchain file  
automatically deduce the triplet to use. The new QT_VCPKG_TARGET_TRIPLET  
environment variable can be used instead, or pass  
-DVCPKG_TARGET_TRIPLET=<triplet> to CMake.  
  
* 90d96766af QEventLoopLocker: defend against nullptr arguments  
Is now a no-op on nullptr QEventLoop*, QThread*,  
QCoreApplication::instance() (was: crash).  
  
* 3cc1885370 QEventLoopLocker: inline Private into public class  
No longer allocates; all operations are noexcept now.  
  
* a83d59b901 QLibrary: make isLoaded() report whether this object has  
load()ed  
QLibrary::isLoaded() now reports whether this instance of QLibrary has  
succeeded in loading the library, via direct or indirect call to load().  
Previously, it used to reported whether the actual library was loaded by  
any QLibrary instance.  
  
* e46c3c3e5a QCborValue: fix memleak on Array to Map coercion  
Fixed a memory leak when an array was coerced into a map.  
  
* 41388a7ce4 QSslDiffieHellmanParameters: fix mem-leak  
Fixed a memory leak in parsing of PEM-encoded Diffie-Hellman  
parameters.  
  
* aa2c0eb7eb CMake: Unify CMAKE_BUILD_TYPE behavior on all platforms  
When no explicit build type is specified, Windows will now default to  
building Release like the other platforms.  
  
* 7b6682cfbb QIcon::fromTheme(): Always consult "hicolor" theme last  
The 'hicolor' theme will now always be prioritized last when looking up  
fallback themes, even if explicitly declared as a theme parent in a  
theme.  
  
* 99d0f997aa iOS: Implement QPlatformWindow::setMask() for masking  
rendering and input  
QWindow::setMask() is now supported for masking the rendering and touch  
input of child windows.  
  
* 8d0833a81b Update bundled libjpeg-turbo to version 3.0.0  
libjpeg-turbo was updated to version 3.0.0  
  
* f974ea6f86 QDeadlineTimer: make the (Qt::TimerType) ctor explicit  
The QDeadlineTimer(Qt::TimerType) constructor is no longer implicit. To  
keep old source working, wrap the Qt::TimerType argument in  
QDeadlineTimer{}. This is backwards-compatible with older Qt versions.  
  
* 6f00da8489 SQL: add missing Q_DECLARE_SHARED to the value types  
QSqlField and QSqlRecord are now relocatable types.  
  
* cbea2f5705 QSqlIndex: implement member swap() and use a macro for  
move-assignment  
QSqlIndex is now a relocatable type.  
  
* bcbbafca88 QGuiApplication: Report default platform name before  
initialization  
QGuiApplication::platformName now reports the default platform name if  
QGuiApplication hasn't been instantiated yet. It used to return an empty  
string.  
  
* 6ec1766c5c Android: use all nameFilters at once for native file dialog  
use all nameFilters at once since Android file picker can't change  
nameFilters after being opened.  
  
* 35dda81f7a SQLite: Update SQLite to v3.43.0  
Updated SQLite to v3.43.0  
  
* 35ee5b4eb7 Set color scheme after handling theme change in windows  
Update colorScheme property after palette change.  
  
* 62e17eae88 Update bundled zlib to version 1.3  
zlib was updated to version 1.3.  
  
* 43326b3802 CMake: Recompute features when dependent features are  
marked dirty  
The build system will now try to recompute configure features when  
dependent feature values are toggled by the user.  
  
* e8fb761f75 Fix qHash(qfloat16) to match Qt 6.4 behavior  
Fixed qHash(qfloat16) which was broken from 6.5.0 to 6.5.3, inclusive.  
If you compiled against one of the affected Qt versions, you need to  
recompile against either Qt 6.4 or earlier or 6.5.4 or later, because  
the problematic code is inline.  
  
* 4dc4bf6cf1 Document q(u)int128 and QT_SUPPORTS_INT128  
Added qint128 and quint128 typedefs on platforms that support them.  
  
* e8514f771d Long live Q_(U)INT128_C()!  
Added Q_INT128_C() and Q_UINT128_C() macros to create qint128 and  
quint128 literals in a platform-independent way.  
  
* a66a3983f2 Fix crash when reading corrupt font data  
Fixed a possible crash that could happen when loading corrupted font  
data.  
  
* f504186992 SQLite: Update SQLite to v3.43.1  
Updated SQLite to v3.43.1  
  
* 096a112259 [docs] Fix \since for qHash(qfloat16)  
Delete the old entry for qHash(qfloat16), keep the one from this  
commit.  
  
### qtsvg  
* d130c74 Don't rasterize gigantic shapes  
Unreasonably large shapes are now ignored in SVG files to avoid  
stalling the application. The check can be disabled by setting  
QT_SVG_DISABLE_SIZE_LIMIT=1 in the environment.  
  
* ff22c3c QSvgFont: Initialize used member, remove unused  
Fixed undefined behavior from using uninitialized variable.  
  
### qtdeclarative  
* 83bf594fbd Pointer handlers: don't emit canceled() when an extra  
button interrupts  
A Pointer Handler no longer emits the canceled() signal when it  
deactivates due to violating conditions (such as pressing the right  
button when acceptedButtons == LeftButton).  
  
* 4bad329985 Fix missing glyphs when using NativeRendering  
Fixed an issue where text using NativeRendering would sometimes be  
missing glyphs.  
  
* 46fb848411 QQuickTableView: change the order of row and column to  
modelIndex()  
Because of a source incompatible change in Qt 6.4.0 and Qt 6.4.1,  
modelIndex(column, row) has been reverted back to modelIndex(row,  
column), equal to how it was in Qt 6.3. This also affects modelIndex()  
in TableView. If the order used in Qt 6.4.1 is needed, you can set the  
environment variable QT_QUICK_TABLEVIEW_COMPAT_VERSION=6.4  
  
* 3df8eba0f5 qmltc: generate code into namespaces  
The type compiler will generate C++-code into a namespace by default.  
The  new default namespace is inferred from the module's URI, where dots  
are interpreted as separating subnamespaces from each other, e.g., a  
type in module MyCompany.MyModule.Sub will be generated in the namespace  
MyCompany::MyModule::Sub.  
  
* b5eecccec8 Slow Deprecation of FILENAME_VARIABLE, replacement by  
OUTPUT_SCRIPT  
The FILENAME_VARIABLE option of qt6_generate_deploy_qml_app_script is  
now deprecated, use OUTPUT_SCRIPT option instead.  
  
* 5c496ad952 AnimatedImage: Add ability to configure sourceSize  
It's now possible to configure sourceSize property for AnimatedImage.  
This might be useful when you need e.g. to play hi-res GIF files in some  
smaller size.  
  
* 2d44365f69 CMake: Allow omitting the version of QML modules  
You can now omit the VERSION argument to qt_add_qml_module(). This will  
automatically generate the highest possible version.  
  
* 2b6eb1a51d MultiPointTouchArea: rename signal arguments in Qt 7; test  
with formals  
As a reminder: you should always use formal parameters when writing a  
signal handler that depends on an argument, such as  
MultiPointTouchArea.onPressed, onUpdated, onReleased, or onCanceled. It  
gives you an opportunity to name the argument, to avoid confusion with  
the touchPoints property, and will avoid behavior changes if we rename  
the argument in a future version.  
  
* aea8c9e093 TableView: deprecate modelIndex(row, column) in favor of  
index(row, column)  
modelIndex(row, column) has been deprecated in favor of index(row,  
column).  
  
* 3343c57b02 TableView: deprecate itemAtCell(column, row) in favor of  
itemAtIndex(modelIndex)  
itemAtCell(column, row) has been deprecated in favor of  
itemAtIndex(modelIndex).  
  
* 3773ad8534 TableView: deprecate positionViewAtCell(column, row) in  
favor of positionViewAtIndex(modelIndex)  
positionViewAtCell(column, row) has been deprecated in favor of  
positionViewAtIndex(modelIndex).  
  
* 3cc1e62157 Unexport QSGMaterialShader::GraphicsPipelineState  
The GraphicsPipelineState struct in QSGMaterialShader is no longer  
exported. This may present a binary compatibility break in theory, but  
unlikely to affect any applications in practice given that there is no  
use case for creating or copying an instance of this type in user code.  
This struct serves solely as input to the virtual  
updateGraphicsPipelineState() function, and instances are always created  
and initialized with default values by Qt.  
  
* b9834e0ee9 QmlCompiler: Fix coercion of undefined to float and double  
Converting a JavaScript value to a double or float, for example by  
inserting it into a typed array, now assumes JavaScript type coercion  
semantics. In particular, converting a value that is not actually a  
number now results in NaN where it previously sometimes resulted in 0.  
  
* 4c930247e6 Set correct `this` value in JSON.stringify replacer scope  
Set correct `this` value in JSON.stringify replacer scope, so that the  
value for current key in current object is no longer pre-stringified,  
and can actually be used to implement custom object serialization logic.  
  
* fd7fe4450b QSGDefaultPainterNode: Set format to RGBA8888_Premultiplied  
Changed image format to RGBA8888_Premultiplied in order to improve  
texture upload performance on OpenGL ES and WebGL.  
  
* a60968283b QML: Fix conflicts between QML_ANONYMOUS, QML_UNCREATABLE  
and namespaces  
You can no longer override the "uncreatable" message for QML-exposed  
namespaces using QML_UNCREATABLE. This would be incompatible with making  
the QML_UNCREATABLE macro safe from unintended inheritance. The latter  
is much more important.  
  
* 0a0f777821 CMake: Add NO_COMPILER_RUNTIME to  
qt_generate_deploy_qml_app_script  
Added the option NO_COMPILER_RUNTIME to  
qt_generate_deploy_qml_app_script.  
  
* d66db6c802 QSGDefaultPainterNode: Skip fillRect for invalid fill color  
Background filling can now be disabled by setting the fill color to an  
invalid color. This may improve performance, and is safe to do if the  
paint() function draws to all pixels on each frame.  
  
* efc037191a XHR: Add responseURL  
Added missing responseURL property. This returns the url that was used  
to retrieve the response data, after any redirects have occurred.  
  
* 37c25c6e74 QQuickItemView: Skip instantiating delegates if size is 0  
If a ListView has size zero, it won't instantiate any delegates until  
its size becomes non-zero.  
  
* 66f167aedc XMLHttpRequest: Implement XHR.overrideMimeType()  
Added missing overrideMimeType(mime) method. This function can be used  
to force the XHR object to parse the data in HTTP responses differently  
than what the server suggests.  
  
* 017bf54020 Hook up GPU frame timing to QQuickGraphicsConfig and the  
logs  
The scenegraph render loop timing logs can now show GPU-side times as  
well, as long as the application is launched with the env.var.  
QSG_RHI_PROFILE=1 or the feature is enabled via the new APIs in  
QQuickGraphicsConfiguration.  
  
* adc3d8b2e4 Fix StackLayout to keep the current visible item after  
insert/removal  
StackLayout will now update currentIndex if an Item is inserted or  
removed at an index less than or equal to the current index.  
  
* d93ca833f6 Add startAngle and endAngle properties to Dial  
The start and end angle of the dial element are made customizabe.  
  
* fcf3f5655b Add wrapped signal to Dial  
The dial element emits the wrapped() signal when it is wrapped around.  
  
* 5da4d5e808 Material: fix clipped floating placeholder text  
The outlined TextArea now sets topInset by default if it or its  
Flickable parent clips. This avoids the floating placeholder being  
clipped in those cases. The outlined TextField sets topInset by default  
only if the TextField itself clips.  
  
* 41f36038fb Remove the 'qml-devtools' feature  
The 'qml-devtools' feature is removed. All tools that depend on this  
feature are mandatory and need to be build unconditionally.  
  
* ce85cb1616 Update displayText and value of SpinBox (live)  
The value of a SpinBox can be updated automatically (live) when the  
user edits the text. The displayText of a SpinBox is updated and  
sanitized automatically.  
  
* f940f1b87e TreeView: add support for setting a root index  
You can now set a rootIndex in TreeView, to only show a branch of the  
tree model.  
  
* bdb7bc0543 QQuickScrollView and QQuickTextEdit: Fix binding loops  
Added effectiveScrollBarWidth and effectiveScrollBarHeight which hold  
the effective sizes of scrollbars.  
  
* 995a584c10 Add font.features API to match the one in QFont  
Added font.features property for fine-grained customization of the  
shaping process.  
  
* 9982f16ead Add uniformCellWidths and uniformCellHeights to QuickLayout  
Added uniformCellSizes properties to QuickLayout  
  
* 517d0efb7b TableView: implement SelectionMode  
You can now set a selectionMode in TableView, to control if the user  
should be allowed to select single or multiple cells.  
  
* 90a5e8d217 Introduction of LayoutItemProxy  
Added LayoutItemProxy, a helper item for writing responsive layouts.  
  
* 2eee3f5b69 Make properties in Qt Quick Controls FINAL  
The resizing property is now FINAL, meaning that it can no longer be  
shadowed by user declared properties.  
  
* ecfefd8b97 Make some properties in the effects module FINAL  
Properties for the type MultiEffect are now FINAL, meaning they can no  
longer be shadowed by declaring new properties with the same names in  
QML. A warning will be printed out to the console, when a FINAL property  
is being shadowed. We recommend that users rename those properties to  
avoid potential unexpected behavior changes.  
  
* a32e1543dd Make some properties in Qt Quick Shapes FINAL  
Properties for types in the Qt Quick Shapes module are now FINAL,  
meaning they can no longer be shadowed by declaring new properties with  
the same names in QML. A warning will be printed out to the console,  
when a FINAL property is being shadowed. We recommend that users rename  
those properties to avoid potential unexpected behavior changes.  
  
* f8befff6dc Make properties in Qt Quick Layouts FINAL  
Properties for types in the Qt Quick Layouts module are now FINAL,  
meaning they can no longer be shadowed by declaring new properties with  
the same names in QML. A warning will be printed out to the console,  
when a FINAL property is being shadowed. We recommend that users rename  
those properties to avoid potential unexpected behavior changes.  
  
* 16d822ff32 Make properties in the particles module FINAL  
Properties for types in the Qt Quick Particles module are now FINAL,  
meaning they can no longer be shadowed by declaring new properties with  
the same names in QML. A warning will be printed out to the console,  
when a FINAL property is being shadowed. We recommend that users rename  
those properties to avoid potential unexpected behavior changes.  
  
* 702c36dfc6 Make properties in Qt Quick FINAL to prevent shadowing  
Most properties for types in the QtQuick module are now FINAL, meaning  
that they can no longer be shadowed by declaring new properties with the  
same names. With few exceptions. A warning will be printed out to the  
console, when a FINAL property is shadowed. We recommend that users  
rename those properties to avoid potential unexpected behavior changes.  
  
* 06540cdb02 Flickable: Proportional wheel scrolling if deceleration is  
large  
When using a plain "clicky" mouse wheel, Flickable has historically  
applied acceleration: the faster you rotate the wheel, the faster it  
flicked. The default value of flickDeceleration was 5000, which felt  
hard to control, but changing it in QML affected touch-flicking and  
wheel behavior simultaneously. So now we decouple those:  
flickDeceleration only affects touchscreen flicking, and Flickable  
rather uses a new default value of 15000, which is defined to mean that  
scroll distance becomes directly proportional to  
QWheelEvent::angleDelta() * QStyleHints::wheelScrollLines() (where a  
"line" is 24 logical pixels, because Flickable does not have direct  
understanding of its contents). You can set the new environment var  
QT_QUICK_FLICKABLE_WHEEL_DECELERATION to a value from 1 to 14999 to  
restore wheel acceleration behavior from older versions; 5000 was the  
old value.  
  
* 2af5cc0a7f QML models: Make most properties FINAL to prevent  
accidental shadowing  
Most properties for types in the QtQml.Models module are now FINAL,  
meaning that they can no longer be shadowed by declaring new properties  
with the same names. A warning will be printed out to the console, when  
a FINAL property is shadowed. We recommend that users rename those  
properties to avoid potential unexpected behavior changes.  
  
* 1f6b5f1d43 Fix memory leak when invalidating NativeRendering fonts  
Fixed a controlled memory leak with Text.NativeRendering where loading  
and unloading the same application fonts could cause memory usage to  
increase indefinitely and not be regained until the window was closed.  
  
* f1a084c5e5 qmlls: fix the order in which the build directory is  
obtained  
Qmlls warns when inexisting build folder paths are passed to the  
--build-dir argument or the QMLLS_BUILD_DIRS environment variable. Also,  
it will inform the user if the build directory was set using the command  
line option, the environment variable or an .qmlls.ini settings file, if  
existent in the source folder.  
  
* aa603e1544 qmlformat: fix formatting of object destructuring  
qmlformat will no longer add "" characters automatically in the object  
keys unless the object key is actually a string literal. Also, using a  
scoped variable as the property key will no longer result in the  
duplication of the property name.  
  
### qtmultimedia  
* 0220951e7 Fix behavior of QAudioSink::resume in push mode  
Calling QAudioSink::resume() now returns the sink to the state it had  
when QAudioSink::suspend() was called, no matter whether the sink  
operates in pull or push mode.  
  
* bea75b36c Use new permissions API on Android  
The platform implementation no longer requests Camera and Microphone  
permissions, only checks if they are granted or not. The client  
application must request the permissions using the QPermission API.  
  
* ed04adaf7 Use new permissions API on macOS/iOS  
The platform implementation no longer requests Camera and Microphone  
permissions, only checks if they are granted or not. The client  
application must request the permissions using the QPermission API.  
  
### qttools  
* 86f290ee7 QDoc: Require clangcpp as a dependency  
QDoc will now require "clangcpp" to be available.  
  
* da526cfbf Update qlitehtml module  
Litehtml (used in Qt Assistant) was updated to upstream version v0.6.  
  
* 07efdc53c QDoc: Drop support for renaming commands via qdocconf files  
Support for the 'alias' variable in qdocconf-files is removed. Use  
QDoc's 'macro' construct instead.  
  
* f1f4cad99 QDoc: Always depend on QmlPrivate  
QDoc now requires the library QmlPrivate. Make sure the qtdeclarative  
module is available.  
  
* d5007c7a5 lupdate: Handle C++ string literals  
lupdate now supports prefixed string literals like u"foo".  
  
* c4b0be181 QDoc: Don't write default attributes to index files  
QDoc no longer writes the attributes virtual, const, static, final, or  
override, to the index files, unless the attribute is part of a function  
or method's signature. This reduces the file size of index files  
somewhat.  
  
* 7057d01fb QDoc: Append hash to canonical titles with non-alnum  
characters  
QDoc now appends a hash of the original title to the fragment  
identifier generated for that title if the title contains non-ascii  
characters. This means QDoc now generates fragment identifiers for  
titles that are written in non-latin characters.  
  
* 52c8f1dbd QDoc: Append hash when normalizing non-ascii file names  
QDoc now appends a hash of the original file name to the file name(s)  
of files where the name contains non-ascii characters. This means QDoc  
now generates files for pages with names written in non-latin  
characters.  
  
* 85f0b6ff4 Qt Designer: Add QFont::HintingPreference to property editor  
Support for the QFont::HintingPreference property has been added.  
  
* cd0b646e0 QDoc: Add support for platform dependent EOL chars  
You can now configure QDoc to generate platform dependent end-of-line  
characters in the files it generates. Set the new configuration variable  
`platformEOL = true` to enable this behavior. This can be useful on  
Windows, where the EOL sequence is `\r\n`. QDoc retains `\n` as default  
EOL character sequence.  
  
* c5f973ca9 Qt Designer: Add QFont::Weight to the property editor  
QFont::Weight is now available in the property editor, introducing a  
new "fontweight" .ui attribute. To preserve compatibility, the values  
"Normal"/"Bold" will result in the old "bold" attribute being used.  
  
* 3d691abe7 lconvert: Add -pluralonly command line argument  
Added a -pluralonly command line argument to drop non-plural form  
messages.  
  
### qtdoc  
* 1b416bc8 Bump CMake requirements on Apple platforms  
The minimum CMake version for Qt on Apple platforms is now 3.21.1.  
  
### qtlocation  
* 4b81f1a3 Remove all C++ event handling, prep for pointer handlers  
Map is now non-interactive, concerned only with rendering.  
  
* eaab4630 Add MapView  
MapView is the interactive replacement for the Map item in earlier  
releases. It wraps a Map instance with pointer handlers to make it  
interactive.  
  
### qtpositioning  
* 75c6e4e1 Allow to specify a baud rate for NMEA plugin  
Provide an 'nmea.baudrate' parameter for the NMEA plugin. The parameter  
takes any positive integer value and uses it as a baudrate for a  
serialport connection. If the value is not specified, or an incorrect  
value is specified, a default value of 4800 is used.  
  
* 4d02ca5c Use new permissions API on Android  
The platform implementation no longer requests location permissions,  
only checks if they are granted or not. The client application must  
request the permissions using the QPermission API.  
  
* a7b347aa Use new permissions API on macOS/iOS  
The platform implementation no longer requests location permissions,  
only checks if they are granted or not. The client application must  
request the permissions using the QPermission API.  
  
### qtconnectivity  
* 1e903be8 QBluetoothUuid: remove quint128 support  
The undocumented quint128 was removed from QtBluetooth. This affects  
the QBluetoothUuid constructor and the toUInt128() method. QUuid has  
support for an integer quint128 on certain 64-bit platforms (all except  
MSVC) with a constructor and a getter of the same name, so this change  
is mostly source-compatible, so long as the application code doesn't  
attempt to treat this type as a structure. For cross-platform support,  
use QUuid::Id128Bytes.  
  
* d195ae3a SDP scanner: encode input URLs and escape XML-specific  
characters  
sdpscanner now %-encodes the URLs and escapes all XML-specific  
characters in them before adding the result to the generated XML output.  
  
* ae1a1f5e QtBluetooth: port the code to the new permissions API  
(CoreBluetooth)  
Do not request permissions implicitly, only check them and leave it to  
applications to request permissions explicitly.  
  
* 55abcc47 QBluetoothUuid - add platform-specific conversion functions  
Add CoreBluetooth-specific conversion to QBluetoothUuid class, to get  
CBUUID out of QBluetoothUuid and convert CBUUID to QBluetoothUuid.  
  
* f5b08a18 QtNfc: Remove dependency on QtNetwork  
QtNfc no longer depends on QtNetwork.  
  
* 734638bc QBluetoothAddress: add qHash() as a proper hidden friend  
Added qHash().  
  
* 195f1baf QBluetoothUuid: remove default case labels and fix the  
fallout  
Fixed missing result of  
characteristicToString(CharacteristicType::WeightScaleFeature).  
  
* 246dfef3 QBluetoothUuid: inherit all ctors from QUuid  
QBluetoothUuid now provides all the constructors that QUuid also  
provides (incl. from GUID and QAnyStringView).  
  
### qtwayland  
* db4afd9c client: Fix infinite recursion with text-input-v2  
Fixed a possible crash when editing a field in an item view.  
  
* 0088b09e compositor: Fix crash when raising shell surface item  
Fixed an issue where the compositor would sometimes crash if a shell  
surface item was brought to front.  
  
### qt3d  
* b41f852e1 Create materials with normal textures in Assimp importer  
The scene importer now creates materials that support normal textures  
if the loaded scene has some.  
  
* 6fc59847c Texture array support for RHI renderer  
Enable texture array on the RHI render plugin  
  
### qtimageformats  
* feb7864 TGA Plugin: Fix reading of CMapDepth  
Fixed reading of TGA files with a non-zero X-origin  
  
* 3cba6d1 Update bundled libwebp to version 1.3.0  
Update bundled libwebp to version 1.3.0  
  
* da0158c Update bundled libtiff to version 4.5.0  
Bundled libtiff was updated to version 4.5.0  
  
* 5464b86 Update bundled libtiff to version 4.5.1  
Bundled libtiff was updated to version 4.5.1  
  
* 4496d03 Update bundled libwebp to version 1.3.1  
Update bundled libwebp to version 1.3.1  
  
* 4f638bc Update bundled libwebp to version 1.3.2  
Update bundled libwebp to version 1.3.2  
  
* db221e4 Update bundled libtiff to version 4.6.0  
Bundled libtiff was updated to version 4.6.0  
  
### qtwebsockets  
* da30f70 Support 401 response for websocket connections  
QWebSocket now supports 401 Unauthorized. Connect to the  
authenticationRequired signal to handle authentication challenges, or  
pass your credentials along with the URL.  
  
### qtwebchannel  
* 48d2066 Fix project structure and auto registry  
Created new QtWebChannelQuick which holds qml sources.  
  
### qtwebengine  
* 876f11854 Disable WebEngineContext dump by default  
Disabled WebEngineContext dump by default.  
  
* 000f31fb6 Add qWebEngineGetDomainAndRegistry()  
Add qWebEngineGetDomainAndRegistry()  
  
* 1aa2a71e3 Add QWebEnginePage::devToolsId()  
Add devToolsId property  
  
* 4a26a7b92 RenderWidgetHostViewQtDelegateItem: keep grabs  
WebEngineView (or WebView backed by Qt WebEngine) no longer allows  
components outside to take over the mouse or touch exclusive grab. For  
example if the user starts dragging a scrollbar inside the web view,  
that continues until release, regardless of any DragHandler, Flickable  
etc.  
  
### qtvirtualkeyboard  
* cfc77fbd Make qvirtualkeyboardnamespace.h private  
The qvirtualkeyboardnamespace.h header has been made private. None of  
the enum types declared in that header are used in public C++ APIs.  
  
* d435fdf2 Restore style path for backwards compatibility  
Restored style path /QtQuick/VirtualKeyboard/content/styles for  
backwards compatibility.  
  
### qtspeech  
* c03afcc Add QTextToSpeech::synthesize to produce PCM data rather than  
audio  
Added the ability to produce PCM data as a QByteArray. The  
QtTextToSpeech module now depends on QtMultimedia on all platforms.  
  
### qtnetworkauth  
* 32f29d3 Improve error handling and reporting in OAuth2  
Add token request error signal and improve related error handling  
  
### qtquick3d  
* 72f7a4fe Change API to follow QtQuick3DPhysics  
HeightFieldGeometry::heightMap is deprecated and replaced with  
HeightFieldGeometry::source.  
  
* 4f86bb24 Mark types in QtQuick3D.Effects as deprecated  
The pre-made post-processing effects inherited from Qt 3D Studio and  
its predecessors are now marked as deprecated. They are still available  
for use, but new projects are encouraged to use the 3D post-processing  
facilities provided by ExtendedSceneEnvironment and SceneEnvironment.  
Whereas 2D effects that operate on and treat the output of the View3D as  
a simple 2D image, are recommended to be implemented via Qt Quick's  
facilities, such as the new MultiEffect type or the Qt Quick Effect  
Maker tool.  
  
### qtgrpc  
* 2682cbb Reuse the existing message value when deserializing it second  
time from the wire  
Initialized message fields of the message type are reused when  
deserializinng the message. Previously message fields of the message  
type were deserialized to a freshly created message object. This change  
removes creating of the new message object at each deserialization cycle  
and reuses the exising field value if it's not 'null'. If fields of this  
message object are received from wire they will be overritten, if not  
they will store the previous value.  
  
* 3b8b24c Introduce QGrpcCallOptions and QGrpcChannelOptions  
Add QGrpcChannelOptions to store and process channel options and  
default call options.  
  
* dab5983 Remove QGrpcInsecureCredentials  
Removed QGrpcInsecureCredentials. Now insecure connection is default  
option for QGrpcChannelOptions and QGrpcCallOptions.  
  
* aed606e Remove QGrpcSslCredentials  
Removed QGrpcSslCredentials. Please use  
QGrpcChannelOptions::withSslConfiguration() to setup QSslConfiguration  
for the channel.  
  
* f57775c Remove QGrpcUserPasswordCredentials  
Removed QGrpcUserPasswordCredentials. Now user and password credentials  
can be added by using QGrpcMetadata.  
  
* e7da8ab Migrate to the implicitly shared data for protobuf messages  
Move-from protobuf messages now become invalid after the move  
operations and cannot continue to be used.  
  
* 96397a5 Remove silent reconnection to grpc server stream  
Client HTTP/2 channel doesn't retry to start server-stream  
automatically after connection is lost, since this contradicts gRPC  
streaming concepts. The error should be handled by business logic of an  
application instead.  
  
### qtvncserver (Commercial only)  
* c5319b2 Provide more information about connection state  
Replaced the connectionActive/isConnected properties with a serverState  
property that allow you to also track whether the server successfully  
initialized or not.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-107627 AndroidAssetsFileEngineHandler is broken  
* QTBUG-107662 Android keyboard doesn't close when clicking on done  
* QTBUG-109375 [REG.]Widgets lose their focus frame when QProxyStyle is  
set  
* QTBUG-101526 Special character "Object Replacement Character" does not  
show up visibly  
* QTBUG-109165 No repaint when QGraphicsEffect gets destroyed  
* QTBUG-109400 Windows: Font Line spacing differs between Qt 5 and 6  
* QTBUG-109428 ABI broke for QJniObject::callVoidMethodV in 6.4  
* QTBUG-108848 iOS: Voice Control Accessibility feature breaks in iOS 16  
* QTBUG-93624 nameFilters not working in FileDialog in iOS  
* QTBUG-99601 ios: QMAKE_PRE_LINK Gives Error :Multiple commands produce  
* QTBUG-109454 Black check/radio boxes and grey background with GTK  
Theme  
* QTBUG-109449 inlining QByteArray::isNull() causes BC break on static  
Qt builds  
* QTBUG-109329 tst_qprocess crash in OpenSUSE 15.4  
* QTBUG-106162 macOS VoiceOver has issues with QComboBox  
* QTBUG-109336 windeployqt does not deploy OPC UA plugins  
* QTBUG-106701 Crash with any QML app on external display with iPadOS  
16.1 on M1 iPad  
* QTBUG-109066 wasm: QDialog::exec() with asyncify hangs  
* QTBUG-109466 QTEST_FUNCTION_TIMEOUT applies to the whole test, not per  
function  
* QTBUG-77385 QWidget::restoreGeometry does not work as documented.  
* QTBUG-4397 QWidget::RestoreGeometry does not work if saveGeometry() is  
called while a widget is maximized [regression]  
* QTBUG-103481 qmlcachegen does not remove .qml and .js from resources  
* QTBUG-103720 Dragging toolbars across screens with higher scale  
factors has erratic behavior  
* QTCREATORBUG-28604 Code navigation: Opening resource files from URL  
literals does not work with CMake projects  
* QTBUG-108365 [REG 6.4.0 -> 6.5] Low contrast status bar in Android  
applications  
* QTBUG-61652 Android's virtual keyboard "OK" button must not accept the  
QDialog  
* QTBUG-88652 QTEST_FUNCTION_TIMEOUT and test function limit (5 minutes)  
are not documented.  
* QTBUG-109559 tst_qmessagelogger::qMessagePattern(backtrace) is flaky  
on OpenSUSE 15.4  
* QTBUG-63700 QSharedPointer missing documentation for move operators  
* QTBUG-109436 Drag&Drop Memory leak  
* QTBUG-109026 Android: UI is scaled smaller than before  
* QTBUG-109212 QLabel with embedded image using 'qrc:/' will no longer  
load  
* QTBUG-109214 Documentation for QtAndroidPrivate is still wrong for  
CMake  
* QTBUG-109586 QAndroidApplication::runOnAndroidMainThread() UB when  
timeout is set  
* QTBUG-109453 GDI fallback surface format for Win 11 (21H2)  
* QTBUG-109629 Occasional assertion fail when opening/closing devtools  
* QTBUG-106531 QDockWidget Docking resizes (widens) the widget by a set  
number of pixels  
* QTBUG-109605 ABI breaks due to marking Qt_6_PRIVATE_API too widely  
* QTBUG-109604 ABI break in QCommonStyle  
* QTBUG-109594 QMetaType::NeedsConstruction might be wrongly set  
* QTBUG-107979 WebAssembly - callback is missing when WebAssembly module  
is ready to receive messages from Javascript  
* QTBUG-109619 Enabling 2 extra Android CMake options leads to a build  
error  
* QTBUG-107026 http://matek.hu/xaos/doku.php is dead  
* QTBUG-103393 IBus input method cannot set panel position correctly  
with DPI scaling  
* QTBUG-109746 tst_QWidget::optimizedResizeMove() and  
optimizedResize_topLevel() with QtWayland failed on Ubuntu 22.04, GNOME  
* QTBUG-108183 Crash triggered by assertion in QTextDocumentLayout  
* QTBUG-109790 C++ syncqt ignores the wrong line with ELFVERSION:ignore-  
next  
* QTBUG-109590 styleHints()->setShowShortcutsInContextMenus(true) has no  
effect  
* QTBUG-69452 Shortcuts don't show up in context menus  
* QTBUG-109754 QTextEdit::setTabChangesFocus has no effect  
* QTBUG-106393 Mac OS: Dot and Comma key combinations not working for  
russian layout  
* QTBUG-109477 QImageReader will cause heap corruption when load jpeg  
(width: 1px height:100px) on Apple M1  
* QTBUG-106653 Crash on Accessibility interface  
* QTBUG-109853 Unit test for locale fails for some locales on macOS for  
negative dates  
* QTBUG-108790 Crash on QFuture::cancel() with continuation and thread  
context  
* QTBUG-108639 Reg[6.2->6.4]WebAssembly: Tap is not working on mac with  
trackpad  
* QTBUG-109289 Documentation of QWidget::acceptDrops links to  
GraphicsView  
* QTBUG-109230 Crash in QFuture  
* QTBUG-109851 moc generates reserved identifiers for scoped classes  
* QTBUG-109679 Qt Quick cannot keep up with high refresh rate monitors  
* QTBUG-109474 6.5: Behavioral change in QTextLine  
* QTBUG-109875 -Werror=type-limits for  
src/corelib/tools/qoffsetstringarray_p.h:85:27  
* QTBUG-109036 QXcbBackingStore::toImage() returns wrong image.  
* QTBUG-109738 Deploying a universal app for macOS fails  
* QTBUG-110002 FAILED:  
qtbase/src/xml/CMakeFiles/qattributionsscanner_XXX  
* QTBUG-109610 developer-build fails for xcb  
* QTBUG-109958 tst_qalgorithms should not create unique datatags when  
testing  
* QTBUG-110058 QCryptographicHash is not re-entrant  
* QTBUG-109547 Unnecessary dependency to Qt6QmlTools / qtdeclarative-  
native  
* QTBUG-109159 Cross-compile Qt6. features: sse2  
* QTBUG-110068 qmake: Generated Visual Studio project defaults  
"GenerateDebugInformation" to "false"  
* QTBUG-109792 C++ syncqt tool should be built like moc  
* QTBUG-109237 [Reg-6.3.1->6.4.1] Calling formLayout->addRow can result  
in assert in Debug builds  
* QTBUG-109864 syncqt call fails  
* QTBUG-110070 [REG]Qt crashes on all platforms when trying to paste  
using an empty clipboard  
* QTBUG-105544 qunicodetools.cpp: libthai's th_brk is not thread-safe  
[2/2]: new API  
* QTBUG-109678 fatal error LNK1169: one or more multiply defined symbols  
found  
* QTBUG-105753 QDir is not re-entrant  
* QTBUG-109745 Static assertion failed with  
QVarLengthArray<std::vector<std::unique_ptr<int>>>  
* QTBUG-109967 Builds fail because of missing permissions libraries  
* QTBUG-84315 QUrl::setAuthority() behavior changes  
* QTBUG-109626 Potential race condition in clipboard paste & drop code  
* QTBUG-54505 QString::compare( QString &other, ... ) treats Null and  
Empty QStrings as equivalent and returns zero.  
* QTBUG-107842 Style Plugin Example has no CMake docs  
* QTBUG-109227 Style Plugin Example is broken  
* QTBUG-110268 On macOS, Expose events cannot be filtered with  
QWindowSystemEventHandler  
* QTBUG-81756 QLocale's number parsing uses 'e' both as a digit and as  
exponent separator  
* QTBUG-109840 QUrlQuery: operator== does not handle a case where  
exactly one object has null pimpl  
* QTBUG-109842 QUrlQuery: missing move constructor  
* QTBUG-110412 Crashes in many qml scenes when using vulkan  
* QTBUG-110459 FAILED: src/plugins/position/geoclue2/manager_interface.h  
src/plugins/position/geoclue2/manager_interface.cpp  
* QTBUG-110450 qtpositioning fails to build  
* QTBUG-106659 QPrinter : Scaling factor applied wrongly  
* QTBUG-110513 -no-rpath build fails with CMake 3.16  
* QTBUG-110434 [REG 6.4->6.5] Standard cursor shapes are not updated on  
a secondary screen  
* QTBUG-61042 A QML FileDialog shows a warning in a console after  
reseting the 'nameFilters' property  
* QTBUG-77211 Warning on nameFilters change in QML FileDialog  
* QTBUG-106533 Android: jar and src dirs are installed in /usr if  
CMAKE_INSTALL_PREFIX=/usr  
* QTBUG-107207 Add support for MultiABI with custom install dir of the  
android-build (patch included)  
* QTBUG-110596 FAIL!  :  
tst_controls::Basic::SwipeDelegate::test_dragSideAction() Compared  
values are not the same  
* QTBUG-109798 Torrent Client example still broken in Qt6+!  
* QTBUG-110627 Qt doesn't really follow Windows short time format  
* QTBUG-64132 QToolButton should elide text when width constraints  
prevent from showing whole text  
* QTBUG-108325 QuicControls2 documentations incorrectly suggests to link  
to the library  
* QTBUG-109838 QFontMetricsF::horizontalAdvance seems to do unnecessary  
scanning  
* QTBUG-107185 Some tests appear to be re-testing the exact same data  
tag  
* QTBUG-109845 [REG 6.3.2 -> 6.4.0] toString() on valid QDateTime causes  
undefined behavior  
* QTBUG-108761 QXkbCommon::keysymToQtKey does not correctly handle  
punctuation with modifiers under some keyboard layouts  
* QTBUG-110586 QRegularExpression wrong behavior (behaves differently  
from QRegExp)  
* QTBUG-58043 XDG environment variables with relative paths should be  
ignored  
* QTBUG-104836 [Reg 6.3.1 -> 6.4.0b1] Unavoidable "unreachable code"  
warnings from qanystringview.h  
* QTBUG-110432 Checkbox label is white with darkmode on windows  
* QTBUG-108879 Constructing, copying and moving objects using  
QVariant/QMetaType/QMetaObject is incomplete  
* QTBUG-110707 Optimization in QMimeDatabasePrivate::mimeTypeForFile  
does not work for Custom File Engines  
* QTBUG-73260 webassembly: QDialog Transparent background  
* QTBUG-109974 [Reg 6.3.2 -> 6.4] QML Date() does not update its time  
zone after OS time zone had been changed on Windows  
* QTBUG-56595 QXcbConnection::getTimestamp() returns old timestamp  
* QTBUG-109518 QPdfWriter loses some of the content if it is positioned  
right  
* QTBUG-110735 Inconsistent QToolTip expire timeout when using rich text  
content  
* QTBUG-110271 Copyright year not updated to 2023 on documentation  
* QTBUG-108822 QDBus: unable to connect the InterfacesAdded signal of  
org.freedesktop.DBus.ObjectManager on the system bus (unless using  
QDBUS_DEBUG)  
* QTBUG-70362 QSqlQuery.value() with QString type  
* QTBUG-110803 ODBC SQL driver: UB in qGetStringData() in use of  
SQLGetData()  
* QTBUG-110979 qdbusxml2cpp6 generates broken code for  
org.freedesktop.DBus.Deprecated  
* QTBUG-111007 QRhiGles2 contains non opengles2 call  
* QTBUG-109744 Wrong enum value from QString using Qt 6  
* QTBUG-110941 wasm: MultiPointTouchArea loses all touchpoints after  
just one is released  
* QTBUG-109741 Running qt_generate_deploy_app_script(tgt) must be run in  
the same directory scope as tgt  
* QTBUG-110810 Java Files missing from android project tree  
* QTBUG-110468 Qt uses deprecated Windows Layered Service Providers api  
resulting in wall of errors on Windows 11  
* QTBUG-110751 QTextEdit: textBackgroundColor() returns wrong color if  
no color is set  
* QTBUG-110502 Qt fills in private use unicode if a font is found using  
it  
* QTBUG-110785 QFbCursor memory leak  
* QTBUG-109206 QODBC: Reading Time fails when using ODBC Driver 17 for  
Sql Server  
* QTBUG-110967 MySQL Prepared Statement QDateTime: Not Working  
* QTBUG-111049 WrapRt doesn't check for librt  
* QTBUG-111091 Top-level configure fails unless I have network  
* QTBUG-110595 [REG 5.15 -> 6.x] QSvgRenderer::render(QPainter*) is now  
~100x slower  
* QTBUG-105870 QListItemView with SingleSelection unselects item when  
clicking on empty area  
* QTBUG-107526 action Cmd+Return does not emit shortcut override event  
on macOS  
* QTBUG-109832 QMYSQL plugin no longer works with older supported  
versions of MySQL/MariaDB  
* QTBUG-106718 [REG] QCoreApplication::processEvents() processes  
deferred delete  
* QTBUG-106569 Ctrl-C in QTreeView passes invalid QModelIndex to model  
when model is empty  
* QTBUG-109178 Android Deploy Qt documentation is not up to date  
* QTBUG-105804 The qt_ntfs_permission_lookup mechanism is prone to data  
races  
* QTBUG-103498 wasm: touch app cannot move app with dialog titlebar  
* QTBUG-108537 Pointer types in AutoConnections may fail to be queued at  
runtime, but work with QueuedConnection  
* QTBUG-110986 QFileSystemWatcher::removePaths() Does not removes drive  
* QTBUG-86272 wasm: Dead keys don't work on Linux  
* QTBUG-107844 FileDialog: cannot open image picker dialog on iOS  
* QTBUG-111051 QTextStream shouldn't have been polymorphic  
* QTBUG-107770 no member named 'init' in 'QStyleOption'  
* QTBUG-110816 qmlcachegen fails to find the qtdeclarative libraries  
* QTBUG-111131 setDragEnabled() is breaking interactive item selection  
in QTreeView  
* QTBUG-62102 QKeySequenceEdit handles meta keys incorrectly on Wayland  
* QTBUG-102010 QScroller prevents QAbstractItemView::DoubleClicked edit  
trigger  
* QTBUG-111268 three dependencies in binding of  
Q_OBJECT_BINDABLE_PROPERTY causes crash  
* QTBUG-46990 Soft hyphen rendered as space  
* QTBUG-62620 [QtQuick, TextEdit] Soft hypen and incorrectly drawn  
selection  
* QTBUG-67038 Soft hyphens are broken  
* QTBUG-102483 Soft hyphen rendered as space on macOS  
* QTBUG-110098 When using the dialog function, the top setting function  
is invalid (Qt:: WindowStaysOnTopHint)  
* QTBUG-111339 OCI plugin wrong query  
* QTBUG-111388 Crash in QCocoaMenuBar::merged  
* QTBUG-111347 QMessageAuthenticationCode is not re-entrant  
* QTBUG-98502 QDir::tempPath returns wrong path on Android  
* QTBUG-109511 QtConcurrent in 6.4.0 and later shows undesirable  
behaviour  
* QTBUG-111275 Inserting a QDate into an Oracle DB with a prepared  
statements fails for timezones like CET  
* QTBUG-111149 Reg->6.4.2: Windows: Qt Designer freezes when dragging  
actions in QMenu  
* QTBUG-111467 FTBFS: symbol clash in QCryptographicHash with OpenSSL:  
SHA1 "redeclared as different kind of entity"  
* QTBUG-111426 iOS example project 'ToDo List' is incorrectly tagged as  
'Android'  
* QTBUG-111170 mouseMoveEvent fired without mouse being really moved  
(Mac only)  
* QTBUG-63381 Transient scrollbars do not work when using style sheets  
* QTBUG-111382 Not possible to use TESTDATA for manual tests  
* QTBUG-111498 QPainter::drawImage() broken on big images when OpenGL is  
used  
* QTBUG-110497 Qt's CMake Config files reset CMAKE_AUTOMOC_MACRO_NAMES  
* QTBUG-111491 Dark Title on Dark Windows 11 when running native Windows  
Style  
* QTBUG-107801 Not all locales use single-character exponent separator  
* QTBUG-105864 a11y: AT-SPI relations FLOWS_FROM and FLOWS_TO not  
supported  
* QTBUG-108013 QStandardPaths::PicturesLocation paths on Android  
* QTBUG-104892 QStandardPaths::DocumentsLocation on emulated android  
device returning the same directory twice  
* QTBUG-81860 Android: Add "content:" scheme paths to QStandardPaths  
* QTBUG-111416 [REG 6.3.2->6.4.2] Repeated QPainter::drawPixmapFragments  
calls draw images at wrong positions for QOpenGLWidget  
* QTBUG-111443 macOS/iOS: "Detected system locale encoding (US-ASCII,  
locale "C") is not UTF-8"  
* QTBUG-110898 Window disappears when monitor is disconnected  
* QTBUG-111698 Build fails with -march=amdfam10  
* QTBUG-111162 WASM: Platform minimum size only enforced on window  
initialization  
* QTBUG-111753 Manual tests try to use the auto test runner instead of  
wasm shell  
* QTBUG-111618 Resize cursor used even if window is not resizable  
* QTBUG-111524 [REG 6.4 -> 6.5-beta3] Exec'd QMessageBoxes from QMenus  
return immediately on macOS  
* QTBUG-111774 FTBFS: qtbase -DQT_FORCE_FIND_TOOLS=ON fails on CMake:  
Some (but not all) targets in this export set were already defined.  
* QTBUG-104585 Change in behaviour of QListWidget::findItems  
* QTBUG-111234 QRegularExpression::wildcardToRegularExpression is  
incorrect in corner cases  
* QTBUG-45087 ODBC: Native codes are lost when calling SQLGetDiagRec  
repeatedly  
* QTBUG-111267 markDirty() does not exist for Q_OBJECT_COMPUTED_PROPERTY  
* QTBUG-111803 Native QMessageBox on macOS doesn't show check box  
* QTBUG-111735 QPropertyAlias::addNotifier() is ill-formed  
* QTBUG-111397 QNetworkAccessManager hangs indefinitely when loading a  
corrupted cache file  
* QTBUG-111867 QVariant::operator== between QVariant(0) and QString  
* QTBUG-111617 Qt OpenGL: GL Widgets in Chrome duplicate view from first  
widget  
* QTBUG-96616 QODBC-DB2 Unicode support is not recognised  
* QTBUG-102958 ODBC Oracle wrong detection for unicode  
* QTBUG-111226 wasm: building individual tests is not possible  
* QTBUG-102107 [REG 5.15.2 => 6.2.3] QMenuBar can crash on Mac  
* QTBUG-106369 Crash when closing modal window with macOS on-screen  
keyboard  
* QTBUG-111183 Qt crash on macOS when using keyboard viewer  
* QTBUG-105250 Access NULL m_platformWindow in qnsview_complextext.mm  
* QTBUG-111884 FTBFS: qtbase can't be built in static mode  
* QTBUG-111869 irritating gotcha and crash in QCompleter popup()  
* QTBUG-111896 Accessibility button is visible if QWasmWindow canvas is  
transparent  
* QTBUG-111027 Adding asset pack to package crashes androiddeployqt  
* QTBUG-85544 androiddeployqt fails with message that neither  
libqtforandroid.so or libqtforandroidGL.so are included  
* QTBUG-97636 Qtbase for Android with examples fails to build  
* QTBUG-83997 Can't deploy a simple console application  
* QTBUG-93185 Android platform plugin not linked when using only QtCore  
* QTBUG-8682 QPlainTextEdit: When scrolling vertically using the arrow  
keys then the valueChanged() signal is not emitted from the vertical  
scrollbar  
* QTBUG-25365 ValueChanged() signal is not emitted by QScrollBar when  
Page Up/Dn is Hit in  QPlainTextEdit having scrollbar  
* QTBUG-108050 Depth Buffer not working in 5.15.2  
* QTBUG-110485 Empty ApplicationWindow prints a warning  
* QTBUG-111798 Crash on macOS when showing QMainWindow with  
"Preferences" menu item in "Edit" menu  
* QTBUG-111742 QColordialog - cannot input/paste values without #  
(pound) symbol  
* QTBUG-111916 Crash upon copy/paste on Mac in plugin situation  
* QTBUG-109971 Crash during window resize when using QQuickWidget  
* QTBUG-68884 Missing isNull check in QOpenGLTexture (crash in driver)  
* QTBUG-112174 QDebug operator<<(QDebug debug, const QInputDevice  
*device) crashes if device is null  
* QTBUG-56214 Qt Creator stops responding to mouse wheel scrolling  
* QTBUG-98720 Regression: Mouse wheel scrolling randomly stops working  
on Linux.  
* QTBUG-99331 Mouse-wheel scrolling stops working when mouse is  
disconnected and reconnected  
* QTBUG-112141 [Qt6 regression] Scrollwheel doesn't work after KVM  
switch  
* QTBUG-104878 xcb wacom support gets confused about device instances  
* QTBUG-30407 QTextList does not support the "start" attribute for  
ordered lists  
* QTBUG-102131 Update docs for QButtonGroup  
* QTBUG-111436 wasm: Dialog title does not cause popups to be dismissed  
* QTBUG-107139 Webassembly cannot input Chinese  
* QTBUG-104905 Window modal not blocking ancestor window interaction on  
Mac  
* QTBUG-112162 QTimer::singleShot() can call receiver in wrong thread  
* QTBUG-112205 QMetaType id of custom QObject subclass unknown prior to  
fetching id from QVariant  
* QTBUG-111598 Implement get/get_if for QVariant to make it nicer for  
non-default constructible types  
* QTBUG-112222 loss of data warnings compiling QTaggedPointer  
* QTBUG-107545 Taking a second future from QPromise overwrites the first  
one  
* QTBUG-106099 QCombobox dropdown not displayed on correct monitor in  
multimonitor setup  
* QTBUG-104781 Tooltip Example: Wrong object is moved when performing  
dragging on another one  
* QTBUG-111826 QPromise: Can't use addResult() with initializer list  
* QTBUG-111102 [REG 6.4.0 -> 6.4.1] QT_WIDGETS_HIGHDPI_DOWNSCALE is  
broken  
* QTBUG-107814 Reg:[6.3->6.4]QOpenGLWidget tries to render duplicate  
controls  
* QTBUG-95930 QGuiApplication::setHighDpiScaleFactorRoundingPolicy()  
ignored on Linux, always acts like PassThrough  
* QTBUG-99546 QT_SCREEN_SCALE_FACTORS doesn't follow rounding policy  
* QTBUG-74478 mouse flicking on qtabwidget non-current tab causes  
segfault  
* QTBUG-108614 QComboBox will emit currentIndexChanged when the index  
isn't changed  
* QTBUG-112289 Assertion fail for dialog repaint on window resize  
* QTBUG-107988 Can't use cmake generator expressions with  
QT_ANDROID_EXTRA_LIBS on macOS  
* QTBUG-111706 Keyboard Can not input when open into a page  
* QTBUG-100128 QListWidget/QListView: item widget disappears when item  
is dragged and dropped on itself  
* QTBUG-112458 Failed to generate docs  
* QTBUG-56064 QStandardItem:: setEnabled() has no effect on QComboBox  
items when SH_ComboBox_UseNativePopup is applied  
* QTBUG-105109 Example code related to QHash::erase() fails clazy  
* QTBUG-111417 HTTP/2 request does not finish until closed by remote  
host  
* QTBUG-109120 [iOS] Problems with Native Photo Picker  
* QTBUG-112478 WASM: default network connections broken due to changed  
default  
* QTBUG-112534 QMultiHash functions (size, isEmpty) return unexpected  
values  
* QTBUG-110019 Address Book example crashes on exit  
* QTBUG-97571 Text in column header is not elided for QHeaderView  
* QTBUG-112018 syncqt fails 6.5.0 build  
* QTBUG-111163 [6.5] Parallel builds failing in Docker container  
* QTBUG-102745 Static plugin loaded twice  
* QTBUG-112527 QPermission incorrectly checks and requests permissions  
on Android  
* QTBUG-109677 QtFuture::makeReadyFuture(mutable QList) creates wrong  
future  
* QTBUG-112465 androiddeployqt fail on Android build platform:  
android-33-ext5  
* QTBUG-112648 Extra semicolon warnings in qtablewidget.h, qimage.h and  
qdebug.h  
* QTBUG-96877 Qt6 won't render into cutout area (regression)  
* QTBUG-112656 qcocoanativeinterface.mm:4:10: fatal error:  
'QtGui/private/qopenglcontext_p.h' file not found  
* QTBUG-84797 QMYSQL: QT application running in Ubuntu 20.04 wont  
connect to MySQL 5.7.X servers  
* QTBUG-112204 windeployqt error when creating translations  
* QTBUG-111984 Connectivity dependency not installed in 6.4.3  
* QTBUG-112300 Shared plugin examples do not work  
* QTBUG-112667 qmake QMAKE_BUNDLE not work for mac  
* QTBUG-112668 qmake QMAKE_APPLICATION_BUNDLE_NAME not work for mac  
* QTBUG-97847 How to recreate full SQL query in Qt 6 (removed  
feature?!!!!)  
* QTBUG-110632 Assertion failure in qqmltreemodeltotablemodel.cpp when  
adding/removing files from directory watched by QFileSystemModel used by  
TreeView  
* QTBUG-112474 QNetworkAccessManager: CANNOT GET RETURN FROM HTTP POST  
* QTBUG-112257 QIcon::fromTheme very slow for repeated failed lookups  
* QTBUG-111538 QDockAreaLayout::updateSeparatorWidgets crash with null  
pointer dereference sometime after restoring state due to recursion into  
QMainWindowLayout::setGeometry causing corruption of separatorWidgets  
* QTBUG-109763 tst_QAccessibility::focusChild() with QtWayland failed on  
Ubuntu 22.04, GNOME  
* QTBUG-34337 Application hangs when enabling a11y for QTableView with  
large number (100k+) rows  
* QTBUG-103792 TextField inside a multi sampling layer breaks rendering  
with OpenGL RHI backend  
* QTBUG-112317 [REG 6.4.2 -> 6.5] can't NOT install qmltooling anymore  
* QTBUG-105921 Qt: OpenGL does not seem to work on Wayland? (NVIDIA  
515.65.01)  
* QTBUG-112756 GL_INVALID_OPERATION in unsupported function called  
(unsupported extension or deprecated function?)  
* QTBUG-112759 Application crashes on QAbstractButton::setChecked if  
button destroyed in toggled signal  
* QTBUG-112820 Undefined symbols for msgSend stubs when linking with  
Xcode < 14  
* QTBUG-104709 [REG. 6.2->6.3] macOS: Default Edit menu entries shown  
twice  
* QTBUG-79565 Mac: Emoji Picker shortcut (Ctrl + Cmd + Space) doesn't  
work in QML TextEdit  
* QTBUG-60505 Enhance the QSqlDatabase::cloneDatabase() help  
* QTBUG-110408 [Win] Yet another unhandled exception on  
QNetworkInformation::load()  
* QTBUG-43674 Accessibility is not enabled when running as root  
* QTBUG-112019 QSpinBox/QDoubleSpinBox up/down arrow size incorrect on  
screen with non-integer device pixel ratio  
* QTBUG-112861 Regression in spinbox PlusMinus symbol rendering  
* QTBUG-112448 windeployqt for mingw copies wrong mingw dlls  
* QTBUG-112743 Infinite warnings on failure to load .qrc resource file  
* QTBUG-112872 Module JSON files have wrong plugin_type entries for  
Wayland plugins  
* QTBUG-112822 QProperty crashes  
* QTBUG-112252 QSS: QSizeGrip { image: } shows image only when in  
bottom-right corner  
* QTBUG-112914 Qt3D/Windows[D3D11]: Crash at destruction  
* QTBUG-112735 Typo in QTextStream documentation ("ISO-5589-1")  
* QTBUG-112473 Background of splash screen of QtQuick example Window and  
Screen is not transparent  
* QTBUG-112537 A Window's background cannot be semitransparent anymore  
* QTBUG-111969 Qt6 semi transparent bug in Windows 11  
* QTBUG-112524 The Color Property of Window is no Effect  
* QTBUG-112953 QTextDocument::contentsChange is emitted several times  
when iBus is on  
* QTBUG-112326 [REG: 5->6] Cannot add items with user data to QComboBox  
that has QSortFilterProxyModel  
* QTBUG-111854 The order fonts are loaded in, can artificially reduce  
their style variants  
* QTBUG-99990 windows: Painting an image with DPR >1.0  to a QPrinter  
does not produce correct result  
* QTBUG-112277 Title text of stacked dock widgets shown in wrong  
location during drag  
* QTBUG-110080 Using FileDialog or FolderDialog makes the mouse cursor  
disappear  
* QTBUG-111978 Setting QComboBox tab order after setting setEditable  
results in incorrect behavior  
* QTBUG-111200 [REG: 5->6] QDomDocument now drops standalone attribute  
* QTBUG-112884 StringLiterals documentation references wrong header  
* QTBUG-109640 QFrame no physical pixel rounding for frame width on  
screen with non-integer device pixel ratio  
* QTBUG-113138 Copyright statements and license identifiers appear in  
the HTML  
* QTBUG-109429 Wrong window and/or content size after screen scaling  
change  
* QTBUG-113127 It is qt_gl_read_framebuffer_rgba8 that cause a crash  
which show info "nvoglv32!DrvPresentBuffers+0xf71ab" at the top of stack  
nvoglv32.dll  
* QTBUG-112881 QFileDialog::saveFileContent() not working on Chrome  
* QTBUG-113041 Loading a file asserts when the file is larger than chunk  
size  
* QTBUG-112814 The window restore geometry is not correct  
* QTBUG-112761 ctf_array produce an error while compiling with lttng  
enabled  
* QTBUG-113140 Resizing a QTabBar resets the scroll position  
* QTBUG-112816 REG [6.5.0->6.5.1] corelib/platform/androidnotifier not  
compiling on Android  
* QTBUG-103514 Possible crash in imagescaling example.  
* QTBUG-113147 Documentation of Q_ARG and Q_RETURN_ARG: return value  
* QTBUG-112899 QMacStyle setupSlider leaks memory painting QSlider  
* QTBUG-98093 QSlider is broken in MacOS Monterey  
* QTBUG-113216 The example for QT_DEPLOY_TRANSLATIONS_DIR doesn't  
actually mention that variable  
* QTBUG-112985 Access to GL_MAX_VARYING_COMPONENTS fails in macOS with  
core profile context  
* QTBUG-113227 ABI issue with QVariant and metatypes from Qt < 6.5  
* QTBUG-112922 Focus lost if mouse is hover over QGraphicsView  
* QTBUG-112762 QMetaProperty::write detaches value argument  
* QDS-9687 Examples cannot be downloaded  
* QTBUG-112334 False doc for void QList::resize(qsizetype size)  
* QTBUG-112697 QMessageBox return immediately on macOS if called from  
MenuBar and after a modal dialog [REG]  
* QTBUG-113238 Remove not needed android tag from Widget Camera Example  
* QTBUG-111509 WASM: recent accessibility work breaks -no-feature-  
accessibility build  
* QTBUG-113143 QGenericUnixServices::openDocument /  
xdgDesktopPortalOpenFile fails in flatpak  
* QTBUG-113289 Access to GL_POINT_SPRITE fails in GL core profile  
* QTBUG-112990 QProcess::startDetached() freezes threads on QNX?  
* QTBUG-112901 wasm: QCameraPermission does not work on Firefox  
* QTBUG-113315 Segmentation fault in a VirtualBox Linux guest with  
-march=native  
* QTBUG-113295 Failure to build Qt 6.5.0 from source on macOS  
* QTBUG-113311 [REG] Mac checkable menu stays on parent click (works in  
6.4.3 + 6.4.0b2)  
* QTBUG-113376 [REG 6.5.0 -> 6.5.1] QTabBar: Jumping non-expandable tabs  
* QTBUG-113209 Qt::ItemNeverHasChildren prevents itemChanged() from  
being fired  
* QTBUG-112663 QFile on Android unable to open file content:// with  
space in the name  
* QTBUG-107459 Qt produces warnings when QT_PLUGIN_PATH contains  
different major versions  
* QTBUG-101755 (glob|magic)-deleteall does not remove existing  
globs/magic with xml providers  
* QTBUG-113337 [REG 6.4.3 -> 6.5.0] Integer overflow in qfixed_p.h when  
rendering SVG image on the minimal plugin  
* QTBUG-109324 Clarify the doc page about module changes in Qt6  
* QTBUG-93768 Recursive loop with QCocoaAccessible::unignoredChildren  
causes crash  
* QTBUG-112911 QMenu has sizing issues on multi screen systems  
(again/regression)  
* QTBUG-113379 QSetIterator has hasPrevious, previous and peekPrevious  
but are unusable in Qt6  
* QTBUG-104785 [REGR:5->6] Performance regression in QLocale on macOS  
* QTBUG-112738 QDir::entryInfoList() broken on Android when nameFilters  
used  
* QTBUG-113500 Assert when using a QWidget inside NSSavePanel  
* QTBUG-112737 clang++: unknown argument: '-permissive-' and unsupported  
'-Zc:__cplusplus'  
* QTBUG-105457 Signals might be processed in wrong order in QtDBus  
* QTBUG-113351 qlogging.cpp: invalid return  
* QTBUG-112885 Qt6AndroidMacros generates invalid android's deployment-  
settings.json  
* QTBUG-111243 [REG: 5->6] pthread functions seem to refer to the parent  
process in QProcess child setup  
* QTBUG-111964 QProcess::start does not return if setChildModifier hangs  
* QTBUG-104493 Application performance drops if many threads are running  
while QProcess creates sub-processes on Unix  
* QTBUG-111582 QByteArray(int size, Qt::Initialization) is not  
documented  
* QTBUG-113443 QLocale::toDouble() fails to convert a string with Latin  
"e" or "E" as exponent separator in Ukrainian locale  
* QTBUG-113556 QWhatThis::showText() brings Mac Permission Dialog  
* QTBUG-36367 Misleading error output of moc on unknown symbols  
* QTBUG-45381 QTabWidget::setTabText() will cause the tab to shift the  
current position  
* QTBUG-113335 qhash.h:561:17: alloc-size-larger-than warning  
* QTBUG-113619 Incorrect moc file generated when using QOffscreenSurface  
* QTBUG-113676 NonPathWildcardConversion: * and ? do not match newline  
characters  
* QTBUG-113643 CMake: headersclean depends on way too much  
* QTBUG-111105 QT_WIDGETS_HIGHDPI_DOWNSCALE doesn't work with  
QOpenGLWidget  
* QTBUG-112921 Cannot create packages for Google PlayStore  
* QTBUG-108132 cannot set --release option to androiddeployqt when  
building app with cmake ?  
* QTBUG-112961 Opening QSqlDatabase in parallel causes endless loop at  
shutdown  
* QTBUG-33142 Inherited signals do not work via D-Bus  
* QTBUG-113244 Python not detected on reconfigure with the developer-  
build option  
* QTBUG-113771 Qt 6.5 Build from source issue - Can't find class headers  
like QFile  
* QTBUG-113787 error: 'IFF_UP' conflicts with a previous declaration  
* QTCREATORBUG-29216 indentifier for object is missing  
* QTCREATORBUG-29214 text repetition  
* QTBUG-112958 QFuture: gracefully handle a destroyed context in  
continuations  
* QTBUG-113281 QObject::setProperty() detaches value argument  
* QTBUG-113630 Windows build with LLVM fails with platform header  
missing after successfull configuration  
* QTBUG-113977 Crash on start with QT_SCREEN_SCALE_FACTORS set  
* QTBUG-113557 Raster native widget fail to draw when there is a quick  
widget sibling  
* QTBUG-113652 [REG 6.3.2 -> 6.4] Native QOpenGLWidget in QMainWindow  
breaks menu bar  
* QTBUG-108277 QWidget::setParent calls q_evaluateRhiRecursive which is  
slow  
* QTBUG-113694 Qt 6.5 build fails on macOS  
* QTBUG-36405 qdbusxml2cpp breaks with multiple interfaces and -c  
* QTBUG-110889 Missing default CFBundleIdentifier in CMake generated  
projects  
* QTBUG-87332 QDockWidget on Wayland is pretty bad: not redockable, does  
not visually move when moving  
* QTBUG-114064 QDialog always show minimize on macos  
* QTBUG-113990 QTextDocument should render <hr> in WindowText colour  
* QTBUG-106683 qt_add_qml_module: _automoc_json_extraction target and  
resources are rebuilding every time with Visual Studio Generator  
* QTBUG-114206 tst_qquick3dbuffermanager (Failed)  
* QTBUG-114238 API asymmetry in isEmpty / isNull between QByteArray and  
QString operator+=  
* QTBUG-114204 QTabBar tabs above current index not visible if current  
index is set before the tabbar is drawn  
* QTBUG-113591 Problem updating QDockWidget's title with translations  
* QTBUG-112829 QGuiApplication::screens() returns only the secondary  
screen  
* QTBUG-114085 qt-configure-module with parameters fail at run at root  
directory  
* QTBUG-113811 [REG: 6.2->6.5] windows: 16x multisampling produces a  
border (NVIDIA)  
* QTBUG-114229 Broken bitmap fonts when a non-rotating transform is set  
* QTBUG-112968 QTextEdit hangs when large text is copied  
* QTBUG-113438 AT-SPI: Wrong char reported by GetCharAtOffset when code  
point > 65535  
* QTBUG-112742 REG: QScreen physicalSize() return wrong results on  
Android / Qt 6.5 - returns pixels not millimeters  
* QTBUG-111901 Release build still puts debug info into .so files  
* QTBUG-93009 QPalette::PlaceholderText color is not followed after  
setting color in a style sheet  
* QTBUG-112513 QFuture continuation segfaults with move only datatypes  
* QTBUG-100094 iOS A11Y unexpected reset  
* QTBUG-114236 Any Drag and Drop crashes on 6.5  
* QTBUG-112217 setTearOffEnabled() leading to crash  
* QTBUG-109405 [Regression] 6.3.1 -> 6.4.1 Android - QSettings lost  
* QTBUG-109369 QSettings - default file location changed between Qt5 and  
Qt6 on Android  
* QTBUG-113717 QComboBox::removeItem is triggering  
QComboBox::currentTextChanged.  
* QTBUG-114199 macOS: Clicking on a menu item which opens a submenu  
erroneously closes menu  
* QTBUG-114078 wasm: NetworkReply with empty data generates runtimeError  
* QTBUG-108794 Building applications against static QNX build fails  
* QTBUG-113416 [Reg 6.4->6.5] Static build fails at PDF module  
* QTBUG-114530 Qt build in jenkins triggers message boxes with help  
messages from Qt tools  
* QTBUG-114431 FindEGL.cmake fails for static linking with Qt  
* QTBUG-114625 TRY_RUN failure on cross-compilation  
* QTBUG-114629 QJsonValueRef inherits non-exported class  
QJsonValueConstRef  
* QTBUG-111330 error: Not a signal or slot declaration in code generated  
by qt_add_dbus_interface  
* QTBUG-62912 Hover is not reset properly with touchscreens  
* QTBUG-114546 [Reg 6.2.8->6.5.1] [macOS] Prior modal dialog and manual  
event processing can break QMessageBox  
* QTBUG-113641 PlatformCommonInternal INTERFACE_LINK_OPTIONS property is  
propagated to user projects  
* QTBUG-114606 Cancelling a QPromise with a failure handler crashes  
* QTBUG-114073 qdoc resolves "QML Import Path" reference incorrectly  
* QTBUG-112200 Possible memory leak with Fusion style  
* QTBUG-114785 MinGW v13.1.0: errors in TinyCBOR (Windows 10 22H2  
x86_64)  
* QTBUG-110942 I see 2 icons showing up in our QTreeView since upgrading  
to Qt6  
* QTBUG-113573 When dragging a header section it will no longer scroll  
when at the edge  
* QTBUG-48161 QDockWidget emits visibilityChanged(false) when minimizing  
the window or switching virtual desktops  
* QTBUG-112491 examples/widgets/mainwindows/mainwindow crashes  
* QTBUG-114542 DockWidget Crashes when undocked and tabbified  
* QTBUG-108015 [CMake] [MSVC2022] TEST_separate_debug_info always fail  
* QTBUG-114537 linking of QtNetwork against GSSAPI fails on macOS with  
CMAKE_FIND_FRAMEWORK=LAST  
* QTBUG-114571 Incorrect colors after switching between light and dark  
modes  
* QTBUG-113169 QStyleHints::colorScheme reports incorrect value and  
breaks app palette  
* QTBUG-114191 [Dialog QML] Dialog becomes dark after putting the app in  
the background and resuming it back with iOS style  
* QTBUG-114313 [Reg: 5.15 -> 6.2/6.5?] QQuaternion::getAxisAndAngle()  
can produce NaN, even when normalized  
* QTBUG-112351 Incorrect description of QtConcurrent::run()  
* QTBUG-114115 Unable to run on Gitlab CI / Windows Server Core docker  
image  
* QTBUG-114416 iOS: Focussing on a read-only TextEdit can prevent Button  
from receiving further clicks  
* QTBUG-113975 [iOS] Button cannot be focused and take action if it is  
placed in text area  
* QTBUG-114781 Reg->6.6/MSVC: Compile warning about Unused  
SlotArgumentCount in lambda connect  
* QTBUG-114654 KeyRelease event not propagated to parent of QLineEdit  
* QTBUG-114826 multiwindow manual test does not work with D3D12 backend  
* QTBUG-114821 [Reg 6.4->6.5] QMenu no longer renders disabled text  
correctly  
* QTBUG-114865 macos: Building with sanitizer enabled fails  
* QTBUG-114583 Headers use things in <iterator> without including it  
* QTBUG-109781 QXmlStreamReader asserts trying to construct XmlStringRef  
of negative len on external input  
* QTBUG-114829 [REG 6.5.1 -> 6.5.2] Crash/failed assert by passing  
certain xml file to QXmlStreamReader  
* QTBUG-106483 Moving a window to another screen (different DPI) using  
keyboard shortcuts while a menu is open has unexpected behavior  
* QTBUG-114931 MSVC 2022 v17.6.4 causing build failure with Windows 10  
22H2  
* COIN-1059 windows-10_22h2-msvc2022 needs newever msvc 2022  
* QTBUG-114803 iOS Simulator build fails  
* QTBUG-114600 [REG 6.4.3 -> 6.5.0] Strange UI styles  
* QTBUG-68821 QNetworkAccessManager does not propagate proxy errors  
properly  
* QTBUG-113698 Nullptr dereference in qcoretextfontdatabase.mm  
* QTBUG-114605 [macOS] Hover events are not received if the parent of  
the QWindow is embedded  
* QTBUG-114783 RCC requires openssl  
* QTBUG-112995 Long press on touch screen breaks drag and drop  
* QTBUG-114470 Build failure for iOS  
* QTBUG-114925 Reg->6.6/MSVC/WIndows:  Cannot build with debug due to  
compiler flag clash in syncqt  
* QTBUG-114797 QVariant::convert may crash even if QVariant::canConvert  
returns true  
* QTBUG-114334 [REG 6.5.0 -> 6.5.1] Segfault in  
QXcbConnection::handleXcbEvent with touch(pad) gestures after  
disconnecting input device  
* QTBUG-114944 qtestcase.h may need a fix to avoid unreachable code  
warning.  
* QTBUG-112371 Unreachable code warning with MSVC2019 with QTestCase  
class  
* QTBUG-114919 QFileDialog spams users with permission requests  
* QTBUG-112893 WASM: exec() fails, even when ASYNCIFY is enabled  
* QTBUG-114576 QFileInfo("assets:/path/to/file").fileName() returns  
wrong name  
* QTBUG-114219 QFileInfo::fileName() does not strip assets prefix on  
Android  
* QTBUG-112261 [REGRESSION] QDir::entryList returns invalid names (6.4.2  
-> 6.4.3)  
* QTBUG-114918 qvulkanwindow.cpp:451:3: error: redefinition of  
'qvk_sampleCounts  
* QTBUG-112956 [REG 6.4] syncqt.cpp does not install headers marked with  
qt_deprecates pragma  
* QTBUG-115031 qtbase -unity-build-batch-size 103 fails  
* QTBUG-92464 QCompleter breaking use of keyboard accents  
* QTBUG-108522 [Regression: 4 - 5&6] QCompleter can not use input method  
when completer popup is visible on Linux  
* QTBUG-114225 QTableView create extra row  
* QTBUG-114683 Not null value is not enforced in SQL iBase plugin  
* QTBUG-115003 QPainter crash when drawing image  
* QTBUG-114991 QVariant<double> comparison uses <float> on  `-qreal  
float`  platforms  
* QTBUG-115002 Can't import MTLDevice with QRhi Metal.  
* QTBUG-115043 Minor source compatibility break in QLoggingCategory  
* QTBUG-114377 Broken focus when hiding a button of a QDialogButtonBox  
* QTBUG-115062 Incorrect handling of  
QT_FATAL_CRITICALS/QT_FATAL_WARNINGS (non-UB data race)  
* QTBUG-115101 WaylandGlobalPrivate_sync_headers is not running if  
nothing depends on WaylandGlobalPrivate  
* QTBUG-115124 qtpaths JSON output is invalid  
* QTBUG-114446 wasm: native keyboard does not popup on iOS  
* QTBUG-114825 Blacklisting of tst_qquickpopup::hover doesn't work  
* QTBUG-115135 a11y: Top-level item views don't have the application as  
accessible parent  
* QTBUG-95569 CMake infinite loop when configuring with Vulkan support  
in Conan  
* QTBUG-114847 QMAKE_APPLE_DEVICE_ARCHS not documented  
* QTBUG-114977 [REG: 5->6] QLibrary::unload unloads even if another  
QLibrary instance to it exists  
* QTBUG-92113 QXmlStreamReader freezes  
* QTBUG-95188 Out-of-memory in QXmlStreamReader  
* QTBUG-109326 QTableView and QTreeView with Fixed vertical size policy  
and AdjustToContents sizeAdjustPolicy always reserve space for  
horizontal scroll bar  
* QTBUG-113552 Wrong sizeHint for QTreeWidget having an AdjustToContents  
sizeAndAdjustPolicy  
* QTBUG-69120 QTreeView viewportSizeHint is wrong when called before  
showing the widget  
* QTBUG-115147 Title text of stacked dock widgets shown in wrong  
location during drag with stylesheet style  
* QTBUG-113319 ICOReader does not read AND mask for 16bpp/24bpp ico  
* QTBUG-114473 QPalette::cacheKey() is different for same object iff own  
style sheet is used  
* QTBUG-112895 bool ParseResult::operator bool() returns true if no  
error  
* QTBUG-115154 tst_QSocketNotifier::unexpectedDisconnection is flaky on  
macOS  
* QTBUG-114854 windeployqt deploys debug versions of QML plugins  
* QTBUG-115105 QAtomicScopedValueRollback: CTAD from  
Q(Basic)AtomicPointer fails  
* QTBUG-113461 QML TextField Popup  
* QTBUG-114069 qt_generate_deploy_app_script error when cross-compiling  
* QTBUG-97482 Android: QPushButton with QMenu does not work on Qt6  
* QTBUG-115229 Qt 6.5.1 MSVC 2019 fails to compile QtMqtt because of  
Chinese text encoding  
* QTBUG-115249 QCborValue mem leak in or near convertArrayToMap()  
* QTBUG-115243 qtbase 6.6.0-beta2 fails to build (linux-clang target) at  
cmake stage if -DQT_FEATURE_gc_binaries is used  
* QTBUG-115054 QWidget::createWindowContainer does not work on 6.5.1  
* QTBUG-54955 Mac: Wrong QDate string conversion with  
Qt::SystemLocaleLongDate on dates prior to 1893-04-02  
* QTBUG-114909 QLocale::toTime with ShortFormat returns invalid QTime  
for en_US "h:mm AP"  
* QTBUG-114559 SPNEGO/Negotiate:  Can't set spn Option - Signal not  
firing  
* QTBUG-115263 QHostInfo is leaking QSlotObjectBase in  
tst_QHostInfo::lookupConnectToFunctionPointerDeleted()  
* QTBUG-115318 QT_ANDROID_DEPLOY_RELEASE CMake variable has no effect  
* QTBUG-115324 Qt6 configured wrong when is placed inside "3rdparty"  
folder  
* QTBUG-115286 QFactoryLoader memory leak on follow-up setExtraPath()  
* QTBUG-114575 Value changes when cursor is moved in date/time field  
* QTBUG-115189 QColorDialog regression in 6.5.1  
* QTBUG-115473 Missing QSet::removeIf() method  
* QTBUG-114958 dev/6.7: Windows: qsb crashes in debug build, causing  
qtdeclarative build to fail  
* QTBUG-115516 QColorDialog: WA_Hover breaks color and luminance picker  
* QTBUG-115521 opengl can't upload R8 texture  
* QTBUG-114338 Qt Quick with metal crashes on older macOS 11  
* QTBUG-108216 Investigate the QRhi pipeline cache (MTLBinaryArchive  
usage) on macOS 13  
* QTBUG-115327 echoplugin uses an ambiguous project name  
* QTBUG-113685 macOS: QMessageBox does not emit the accepted signal when  
parented  
* QTBUG-115599 Possible SEGV (null pointer deref) in  
QXcbConnection::initializeAllAtoms()  
* QTBUG-115646 QTypeTraits::has_operator_less_than_v behaves  
surprisingly  
* QTBUG-115149  Unwanted highlight of arrows in tree view when hovering  
with mouse  
* QTBUG-115712 [REG 6.6.0 beta2->beta3] Qt source not compiling on  
macOS, declarative/webchannel?  
* QTBUG-112996 Moc error C2838: 'MyEnum': illegal qualified name in  
member declaration  
* QTBUG-115330 QCoreApplication::requestPermission() is leaking slot  
objects  
* QTBUG-115758 Tuio Fiducials always contain invalid UniqueIds  
* QTBUG-115732 Incorrect IANA ID detected for Windows timezone La Paz,  
Mazatlan  
* QTBUG-115740 QLocale for Spanish does not work correctly with  
thousands separators.  
* QTBUG-40315 doc: QFontMetrics::elidedText(...) does not work as  
expected for ElideNone  
* QTBUG-105007 On macOS, QMimeType::comment returns value for the  
secondary language  
* QTBUG-115756 Android: QLineEdit setText() from textEdited signal does  
not move cursor to the end  
* QTBUG-115597 QMenu crash if app loses focus immediately after  
selecting sub-menu item  
* QTBUG-115809 warning: ‘malloc’ may be used uninitialized [-Wmaybe-  
uninitialized]  
* QTBUG-116007 QT_ANDROID_PACKAGE_SOURCE_DIR not working  
* QTBUG-115831 REG 5->6: Setting property placeHolderText on  
QPlainTextEdit does not have any effect if the QPlainTextEdit does not  
have focus  
* QTBUG-115964 qdbuscpp2xml only exports methods/signals with  
QDBusVariant arguments if there's at least one method/signal with  
QVariant as argument  
* QTBUG-25944 QXmlStreamReader::readNextStartElement() works inelegantly  
with isEndDocument()  
* QTBUG-115058 QDockWidget group window still visible when empty  
(regression)  
* QTBUG-114435 Regression 5.15.14: Cannot open Files from Android  
FileDialog with spaces or umlauts  
* QTBUG-115652 Child quick widget fails to draw if it's child of raster  
native widget  
* QTBUG-108344 Something is rotten with texture-based widgets that are  
native child widgets or are children of a native child widget  
* QTBUG-115109 [REG] QTabWidget doesn't draw tabs on the left of the  
initially current tab  
* QTBUG-116137 Compile and install QtBase 6.5.2 does not provide header  
files in -prefix path  
* QTBUG-115853 There is NO method current() for QVulkanInstance  
* QTBUG-115507 qmake fails to provide correct preload list to shell html  
* QTBUG-115852 QCollator on ios doesn't support numeric mode  
* QTBUG-115632 Long press textfield popup teleports after being drawn  
for the first time  
* QTBUG-116224 Wrong QScrollBar with Qt6.5 + windows vista style in RTL  
mode  
* QTBUG-58732 Crash after destroying an unfinished QDBusPendingCall  
* QTBUG-116166 Network tests fail with OpenSSL 3.1.1  
* QTBUG-116287 [REG BiC 6.5.2 → 6.5.3] New QDialogButtonBox symbol  
* QTBUG-116351 QFileInfo::filesystemReadSymLink misses documentation  
* QTBUG-108402 tst_Gestures failures on macOS 13  
* QTBUG-115087 getOpenFileContent does not open the dialog  
* QTBUG-116231 wasm: on windows, shift key produces the word "Shift"  
* QTBUG-116499 Use of edid serial number in qwindowsscreen.cpp is broken  
* QTBUG-116496 icx on windows qvariant_p.h call to customConstructShared  
is ambiguous  
* QTBUG-116060 Reg 6.4.3->6.5.1 QTimer - signal/slot connection not  
working  
* QTBUG-116527 Regression; (QML) Locale enums no longer exist  
* QTBUG-83733 Don't use deprecated/removed functions and structs with  
OpenSSL v3  
* QTBUG-115801 Exception in NVDA screen reader when hovering over text  
edit (due to invalid return value)  
* QTBUG-114779 --no-feature-sharedmemory broken  
* QTBUG-116181 Android: QFile can't open file in directory which is  
chosen by QFileDialog::getExistingDirectory()  
* QTBUG-114423 [Reg 6.4.3->6.5] QTreeWidget crash inside QDialog on  
MacOS  
* QTBUG-116609 MinGW 13.1.0: Coin testing fails at qtbase  
* QTBUG-115461 [REG 6.5.1 -> 6.5.2] QT_WIDGETS_HIGHDPI_DOWNSCALE is  
broken again  
* QTBUG-113995 QDesktopServices::openUrl: Local files don't open anymore  
* QTBUG-115511 QToolTip StyleSheet Color Property Broken in 6.5.2  
* QTBUG-116696 Menus have window type _NET_WM_WINDOW_TYPE_NORMAL instead  
of _NET_WM_WINDOW_TYPE_POPUP_MENU  
* QTBUG-39887 Regression bug: QWidget::setAttribute() does not set  
Qt::WA_X11NetWmWindowType in Qt 5.  
* QTBUG-116729 BenchmarkDemoQt6 chokes the D3D12 backend with texture  
uploads  
* QTBUG-112653 Incorrect colour name returned when handling  
colorSchemeChanged  
* QTBUG-116758 Boot2Qt / Yocto build fails for qtbase in CI  
* QTBUG-116056 signal not found when deleting QAbstractItemModel  
* QTBUG-116788 Sporadic crash on  
QNetworkReplyHttpImplPrivate::loadFromCacheIfAllowed() with nullptr  
access  
* QTBUG-116695 Contradictory statements about signal's return type  
* QTBUG-116277 QFileDialog not cleaned up when parent deleted  
* QTBUG-116840  
/Users/qt/work/qt/qtbase/src/plugins/platforms/ios/qiostheme.mm:73:72:  
error: 'tintColor' is only available on iOS 15.0 or newer  
* QTBUG-96936 qt features do not re-evaluate correctly on re-configure  
* QTBUG-85962 Improve FEATURE_foo to QT_FEATURE_foo detection  
* QTBUG-112957 Toplevel developer build fails to link: undefined symbol:  
vtable for QNetworkAccessDebugPipeBackendFactory  
* QTBUG-116155 Crash with native QComboBox in refreshing QWidget  
* QTBUG-112525 macOS 6.5.0 native looking QMessageBox missing title and  
cannot change button texts  
* QTBUG-116876 Document QElapsedTimer::Duration,  
QElapsedTimer::TimePoint  
* QTBUG-3287 Reads a '\0'-terminated string from the QDataStream  
* QTBUG-116872 Mark QEvent::DevicePixelRatioChange enum as new in Qt 6.6  
* QTBUG-116870 Document QNativeIpcKey::QNativeIpcKey()  
* QTBUG-116330 wasm: Exit app with async main() results on runtime error  
* QTBUG-116937 Documentation for new api missing: QSqlField::swap  
* QTBUG-116732 ld: warning: -undefined error is deprecated  
* QTBUG-116777 Package created with windeployqt gives error when exe run  
* QTBUG-114720 QProcess::UnixProcessFlag::IgnoreSigpipe does not take  
effect on QNX  
* QTBUG-116930 Documentation for new api missing: QPalette::accent  
* QTBUG-115699 [REG 6.4.3-6.5] Changing the minimum size get the window  
out of maximized state  
* QTBUG-116338 Vulkan-based QQuickWidget or QRhiWidget is rendered  
incorrectly when in a QScrollArea  
* QTBUG-116517 Zero-width space in qaccessiblewidgets.cpp causing  
compilation error  
* QTBUG-116232 Regression 6.5.2 vs 6.6.0 beta: macOS DPI change  
detection fails with 6.6  
* QTBUG-114203 keyReleaseEvent not triggered on windows devices with  
touch display  
* QTBUG-113765 QComboBox: Wrong popup position when switching to Fusion  
style  
* QTBUG-116715 docs: qsettings path on embdded linux  
* QTBUG-116064 [REG SiC 6.4 -> 6.5] qHash(qfloat16(x)) is now ambiguous  
on GCC13  
* QTBUG-116076 qHash(qfloat16(x), seed) != qHash(float(x), seed) unless  
seed == 0  
* QTBUG-115752 stack-use-after-return in tst_assetimport  
* QTBUG-116929 Make a decision regarding QFont's feature API  
* QTBUG-116925 q(u)int128 are not documented  
* QTBUG-116731 QtFuture::whenAll() leaks when one of the futures is  
already finished  
* QTBUG-116920 FAIL!  : tst_QGeoAreaMonitorSource::tst_monitor() 'obj !=  
nullptr' returned FALSE.  
* QTBUG-116821 QNativeIpcKey: UB (inactive union member used)  
* QTBUG-117052 Condition of feature ipc_posix erroneously evaluates to  
FALSE  
* QTBUG-117200 Reg -> 6.6b4: Exit warning :"QItemSelectionModel:  
Selecting when no model has been set will result in a no-op" from apps  
with  sort proxy filter model  
* QTBUG-117109 QBindable example fails to configure  
* QTBUG-96374 Inactive Qt::Tool window with Qt::FramelessWindowHint flag  
does not show custom cursor  
* QTBUG-104776 AndroidContentFileEngineIterator hangs when listing  
shared content with nested dirs  
* QTBUG-88506 tst_Android::assetsRead fails on Android  
* QTBUG-88840 No way to pass QT_ANDROID_PACKAGE_SOURCE_DIR for  
qt6_add_executable  
* QTBUG-97518 Mac, Metal RHI - runtime warnings "UI API called from  
background thread".  
* QTBUG-103620 [Reg 5.15 -> 6.2] Flicking is inconsistent with touch  
screen  
* QTBUG-108150 Adding qml files from the build folder to the QRC is  
creating filenames so long it breaks the build on Windows host  
* QTBUG-109235 Review toupper/tolower uses [Qt]  
* QTBUG-105736 tst_qfile unixPipe and socketPair tests fail on Android  
12  
* QTBUG-106906 tst_qtcuncurrentrun::pollForIsFinished occasionally  
crashes  
* QTBUG-109553 CMake deployment API creates too deep directory hierarchy  
when DESTDIR is set  
* QTBUG-93955 Material.System does not work on Ubuntu (Gnome)  
* QTBUG-104354 Document QStringBuilder's auto gotcha  
* QTBUG-105958 [Android] Intent + Talkback leads to deadlock  
* QTBUG-100349 QFileInfo::fileTime() is slow  
* QTBUG-109857 qt-configure-module not executable for android_armv7 on  
linux host  
* QTBUG-99125 windeployqt does not deploy qml stuff in a call with  
multiple applications  
* PYSIDE-2182 QTimer.singleShot example documentation does not work  
* QTBUG-64940 QLocale country() tells "AnyCountry" even though country  
was provided  
* QTBUG-109383 Re-enable building examples with qmake in non-qtbase  
repos  
* QTBUG-74325 QByteArray::toDouble() and qstrtod() function does not  
correctly parse the uppercase NaN  
* QTBUG-110369 AUTOUIC can't handle relative paths referring to parent  
dirs with Ninja Multi-Config  
* QTBUG-109833 QEnterEvent does not have a valid timestamp due to QPA  
API quirks  
* QTBUG-110356 Building Permissions example for debug with qmake on  
macOS fails  
* PYSIDE-2191 pyside6-uic fails to correctly generate resource_rc  
location  
* QTBUG-109171 QOpenGLWidget inside QDockWidget produces segfault on  
undocking.  
* QTBUG-110585 Including QJSPrimitiveValue breaks consumer builds with  
-fno-operator-names  
* QTBUG-110703 tst_QFocusEvent::checkReason_ActiveWindow() fails on  
macOS 13.2  
* QTBUG-91627 [OpenGL] Crash when creating context with contextinfo  
example app on Android  
* QTBUG-110836 include could not find requested file: /home/qt/work/qt/q  
ttools/build/target/lib/cmake/Qt6Core/QtInstallPaths.cmake  
* QTBUG-107604 [Reg 5.15.10 -> 5.15.11] Incorrect fullscreen dimensions  
on some Android devices  
* QTBUG-109268 QWindow on Android doesn't use full area on some devices.  
* QTBUG-97503 Reg[5.15.2-5.15.6] Android: Keyboard covers the inputfield  
* QTBUG-107923 Wrong height of the window on Android  
* QTBUG-109351 Bottom Navigation Bar overlaps app window  
* QTBUG-110501 Wrong calculation of display area on android when virtual  
keyboard is present before opening the app  
* QTBUG-107696 tst_qtcpsocket timeouts with Ubuntu 22.04  
* QTBUG-110952 uic-generated connnection to QLCDNumber::display() fails  
to compile due to overloads  
* QTBUG-110696 Qt6CoreMacros.cmake should take AUTOGEN_BUILD_DIR into  
account  
* QTBUG-76587 wasm: keyboard mnemonics do not work correctly  
* QTBUG-110899 Incorrect warning about binding loop in  
QtQuick.Controls.Control  
* QTBUG-110270 Fix CTF backend metadata creation when cross compiling  
* QTBUG-109076 WebAssembly - QML - Text - Using Thai characters is  
causing a crash  
* QTBUG-111140 cross-compilation failures for qtgrpc  
* QTBUG-102474 Sometime SSL leads to hang application on exit  
* QTBUG-108832 tst_QByteArrayLarge cases fail on Android 12 CI  
* QTBUG-108844 tst_QRhi test cases fail for Vulkan fails on Android 12  
CI  
* QTBUG-111235 tst_QOpenGLWidget::reparentHidden() fails on Android 12  
CI  
* QTBUG-111236 tst_qvulkan cases fail Android 12 CI  
* QTBUG-111423 tst_WaylandCompositor::simpleKeyboard() failed when  
update dependencies  
* QTBUG-50278 "threadedqopenglwidget" sample fatal error when resizing.  
* QTBUG-110093 Threadedqopenglwidget example has blank screen  
* QTBUG-76054 android threadedqopenglwidget example blank and has error  
E OpenGLRenderer: void android::uirenderer::renderthread::CanvasContext:  
:setSurface(android::Surface *)  
* QTBUG-43209 Main GUI thread serialises QOpenGLWidget::frameSwapped per  
VSync for multiple application windows  
* QTBUG-108094 Image color changing while opening in QtQuick  
* QTBUG-104595 tst_QScreen::grabWindow XWAYLAND fails with Ubuntu 22.04  
* QTBUG-105140 [REG] default constuctor requirement for meta type  
(QVariant) breaks webengine api  
* QTBUG-111772 3D textures behave weird with some Vulkan implementations  
* QTBUG-110978 ZSTD: should the preference of the static version be  
kept?  
* QTBUG-111625 COM library crash exposed when using TBB scalable memory  
allocation  
* QTBUG-111741 qt_deploy_runtime_dependencies() doesn't install project  
linked libraries & adds undocumented vcredist installer  
* QTBUG-104752 No way to support both single and multi-role models in  
delegates that use required properties  
* QTBUG-111262 Review <ctype.h> uses [Qt]  
* QTBUG-104688 State variable in QCheckBox::stateChanged should be  
emitted as Qt::CheckState instead of int  
* QTBUG-107198 QML element resize cause flicker on MacOS  
* QTBUG-112275 tst_QImageReader::setClipRect() and setScaledClipRect()  
"SVG: rect" and "SVGZ: rect" with QtWayland failed on Ubuntu 22.04 GNOME  
* QTBUG-84055 Custom enumeration not supported by qt's signal system  
* QTBUG-112180 Properly support enums with underlying type != int  
* QTBUG-63481 tst_QSslSocket_onDemandCertificates_member::onDemandRootCe  
rtLoadingMemberMethods tests fail in the CI  
* QTBUG-112414 Damage rect is not respected for windows on WASM  
* QTBUG-112375 Error inserting value in field varchar(1) with prepared  
query with ODBC sql driver  
* QTBUG-94871 Qt should subscribe to dbus system tray and dbus menu  
service appearing/disappearing  
* QTBUG-94232 androiddeployqt is broken when manually defining  
dependencies  
* QTBUG-100563 Invalid style override breaks Qt Quick Control  
applications (incl. crash)  
* QTBUG-111514 QtCore fails to link with lld 16.0  
* QTBUG-103257 tst_qquickcanvasitem crashes on Android  
* QTBUG-41043 tst_qquickcanvasitem tends to fail on CI  
* QTBUG-78648 RHI: Does not work with Windows10 inside VMWare (Fusion)  
* QTBUG-97642 When a mask is set on a widget after being moved to a  
different display with a different DPR then it can end up not being set  
correctly because it is seen as the same as the previous one  
* QTBUG-109779 tst_QGraphicsEffect::draw() with QtWayland failed on  
Ubuntu 22.04, GNOME  
* QTBUG-111304 wasm: Cube example does not work  
* QTBUG-112227 qmlsc: QQmlProperlyLists assignment to QML lists cannot  
be compiled  
* QTBUG-111503 QXkbCommon: No Qt::KeypadModifier in QKeyEvents in  
QtWaylandCompositor  
* QTBUG-112896 gtk3 platformtheme returns the font of GtkFixed widget  
instead of monospace font  
* QTBUG-53085 Reg[5.6.0-5.6.1] "Start Dictation..." and "Emoji &  
Symbols" are missing in Edit menu in Application  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-104930 QLocale shows German text for "en_DE"  
* QTBUG-112965 Dark mode isn't applied  
* QTBUG-113036 Windows: Prevent Vistastyle from changing into darkmode  
at runtime  
* QTBUG-113116 Documentation typos, errors and improvements  
* QTBUG-113161 tracegen creates duplicate argument names for some types  
for lttng  
* QTBUG-112747 Unable to run configure.bat  
* QTBUG-35608 Flickable speed and deceleration does not scale with pixel  
density  
* QTBUG-35609 Flickable speed and deceleration are not easily  
customisable  
* QTBUG-97055 QQC2 Flickable scrolling is not linear with clicky wheels  
on Qt 6.2.0  
* QTBUG-112746 QAnyStringView missing implicit conversion from char[]  
with unknown size  
* QTBUG-31283 QByteArray::clear() should not free the reserved memory.  
* QTBUG-112892 tst_macdeployqt::basicapp is failing randomly in lts-6.2  
* QTBUG-112951 configure -sysroot is not enough for cross compilation,  
one must also define CMAKE_SYSROOT  
* QTBUG-68855 Overflow in QDateTime for extreme values of QDate  
* QTBUG-75521 Be precise in API dox of QGuiApplication::desktopFileName  
whether .desktop suffix is included  
* QTBUG-113613 [REG: 5->6] QMultiHash erase performance degraded from  
milliseconds to minutes  
* QTBUG-103093 Palette Change And Application PaletteChange Never Emited  
* QTBUG-101648 On Windows Touch device(Surface Pro) need to know if  
external keyboard is connected or not  
* QTBUG-101875 Properly register the input devices on Android  
* QTBUG-112432 wayland plugin should distinguish touchpads from mice,  
etc.  
* QTBUG-113706 WASM: QInputDevice::devices() erroneously reports that a  
touchscreen exists  
* QTBUG-113711 Windows: QInputDevice::devices() returns empty list  
* QTBUG-102239 tst_QWidget::enterLeaveOnWindowShowHide is flaky  
* QTCREATORBUG-29197 Examples page crashes when example has more than  
one category  
* QTBUG-113463 Build issues with symlinks  
* QTBUG-113371 locale and/or environment not being properly set for  
ptests  
* QTBUG-114167 A QString::prepend("data") loop never produces  
freeSpaceAtBegin().  
* QTBUG-113822 UB in QProcessPrivate::startDetached()  
* QTBUG-114243 Qt 6.5 regression with static cross-compiling for Windows  
* QTBUG-114624 QKeySequenceEdit doesn't detect CTRL+SHIFT+0 on a french  
keyboard  
* QTBUG-113690 Elements of QStringList property are not updatable for  
QGadgets  
* QTBUG-113679 When the letter J is at the start of a TextField then it  
will cut off the beginning of the letter due to the negative left  
bearing  
* QTBUG-110025 Android tests aren't bundling OpenSSL for any test  
* QTBUG-114175 QWizard default Style not drawn correctly when scaling  
other than 100%  
* QTBUG-112824 There is no way to get to the Open GL examples page from  
the Open GL Index  
* QTBUG-109776 tst_QAbstractItemView::selectionAutoScrolling() with  
QtWayland failed on Ubuntu 22.04, GNOME  
* QTBUG-101926 "AutoMoc subprocess error" when building in CI  
* QTBUG-114997 tst_QMenu::pushButtonPopulateOnAboutToShow() with  
QtWayland failed on Ubuntu 22.04, GNOME  
* QTBUG-115293 tst_QGraphicsItem::itemUsesExtendedStyleOption() with  
QtWayland failed on Ubuntu 22.04, GNOME  
* QTBUG-115447 QElapsedTimer::hasExpired should have chrono overload  
* QTBUG-114613 QWindow::winId() crashes when QWindowPrivate::create()  
fails  
* QTBUG-83160 moc stumbles on _GLIBCXX_VISIBILITY  
* QTBUG-99555 [RE: 6.2.1->6.2.2] macdeployqt fails to produce  
notarizable packages  
* QTBUG-115247 \target after \row generates invalid HTML  
* QTBUG-115691 [FTBFS w/-developer-build]  
QPlatformWindow::setBackingStore(QPlatformBackingStore*) was hidden  
warning  
* QTBUG-115598 tst_QWidget::render() with QtWayland failed on Ubuntu  
22.04, GNOME  
* QTBUG-113233 Need a way atomically adjust QWindow minimum and maximum  
sizes  
* QTBUG-93763 Systematic announcement of combobox selected element  
* QTBUG-116077 Inconsistent hashing between different FP types  
* QTBUG-116080 Inconsistent hashing between qint{32,64} on 32-bit  
platforms  
* QTBUG-111785 CMake warns about   accessible/qaccessible.h  
* QTBUG-116483 qttools' CMake test test_uiplugin_via_designer fails  
* COIN-1075 QEMU tests fail randomly on "Exec format error"  
* QTBUG-84234 Start new QCoreApplication after shutdown  
* QTBUG-116106 New accentColor role is missing from QQuickColorGroup  
* QTBUG-116689 Debugging qtbase with Creator on boot2qt because of "no-  
prefix" on a prefix build  
* QTBUG-116789 [REG] -platform linux-clang-libc++ -c++std c++2b fails to  
compile synctqt  
* QTBUG-115832 iOS: About Qt dialog displays incorrectly when launched  
from menu  
* QTBUG-116445 [REG][Windows] Crash on  
NativeSkiaOutputDevice::releaseTexture() with nullptr access  
* QTBUG-117120 Debian packages not installing  
  
### qtsvg  
* QTBUG-111850 [REG 6.2.2 -> 6.2.3] Loading particular svg file takes  
far too long  
* QTBUG-95237 [REG 6.0.4 -> 6.1.0] Integer-overflow in  
QFixed::operator+= through QImage::loadFromData(QByteArray)  
* QTBUG-114108 qtsvgglobal_p.h is not correctly installed  
* QTBUG-115648 QSvgRenderer::boundsOnElement() can return wrong results  
with multiple child <text> elements  
* QTBUG-113042 Loading particular svg file takes too long  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtdeclarative  
* QTBUG-107492 Typo in the document  
* QTBUG-105312 REG: SplitView no longer works with touch  
* QTBUG-109422 Wrong moduleheader for QuickControls  
* QTBUG-102201 DragHandler has unexpected behavior when unaccepted  
button is pressed during drag  
* QTBUG-109196 Changes assigning into array property  
* QTBUG-108102 Ensure the bindings in the base type are available  
* QTBUG-108024 [Non-qmlsc] `State.when` evaluation fails when an object  
is bound  
* QTBUG-109147 Methods returning lists of builtins cannot be used from  
C++  
* QTBUG-109021 Compiler warns about signal for properties starting with  
"on"  
* QTBUG-103811 Drawer: Different behavior with mouse & touch input  
* QTBUG-86744 ListView.isCurrentItem not available until model is  
refreshed  
* QTBUG-109417 binding to alias crashes qml  
* QTBUG-108600 [macOS] ListView's items get hover while scrolling in  
Inactive window and behaviour seems completely broken  
* QTBUG-108601 Hover handling is broken for ListView's items in specific  
scenario  
* QTBUG-109411 Quick Text's implicitWidth doesn't respect  
maximumLineCount  
* QTBUG-109140 [REG: 5->6] Slowly dragging Tumbler causes numbers to  
jump around  
* QTBUG-98355 SpinBox text not clipped when larger than available width  
* QTBUG-108266 Mention the fact that FolderListModel depends on  
QFileSystemWatcher for notifications  
* QTBUG-108713 Native font rendering in some cases misses letters  
* QTBUG-105148 Rotated qml combobox popup placed incorrectly  
* QTBUG-109542 TreeView: TreeView.modelIndex() has the order of row and  
column swapped  
* QTBUG-98991 Add example to clear up common layout confusion  
* QTBUG-108798 Dynamically creation of MenuItem  
* QTBUG-104768 Overlay is not available when hardcoding the style  
* QTBUG-109299 Overlay seems to be unknown to the typesystem  
* QTBUG-101736 QQuickWidget: button in a popup doesn't receive touch end  
event  
* QTBUG-98098 Error when Button has a custom background under macOS  
style  
* QTBUG-109585 [Reg 6.4->6.5] Assertion when referring to C++ methods  
* QTBUG-109584 [Reg 6.3 -> 6.4] Cannot assign QVariantList to lists of  
other value types anymore in QML  
* QTBUG-109562 qmlplugindump (deprecated) crashes on dev build  
* QTBUG-109597 Seg fault in QQmlObjectCreator::finalize when creating  
QML object with initial bindings  
* QTBUG-109473 qtdeclarative/dev does not build with manual tests  
enabled  
* QTBUG-96351 QML: strange "Binding loop detected" warning  
* QTBUG-109464 Drawer running exit transition during destruction causes  
crash  
* QTBUG-108632 Cannot generate efficient code for equality comparison on  
non-primitive types  
* QTBUG-106491 tst_QQuickMenu fails on webOS  
* QTBUG-109854 [REG 6.2.4 -> 6.2.5] QQuickImageProvider doesn't scale  
properly if Image size is not set on High DPI displays  
* QTBUG-109377 Add equality comparison ability for QObject * vs null and  
undefined  
* QTBUG-100010 qtdeclarative/src/qml/jit/qv4assemblercommon_p.h needs  
Q_OS_SOLARIS support  
* QTBUG-102777 6.3: Warnings in examples/quickcontrols2/texteditor  
* QTBUG-108610 HorizontalHeaderView & VerticalHeaderView does not  
disconnect from QQmlTableModel::headerDataChanged and can crash app  
* QTBUG-96700 Strikethrough formatting changes to underline.  
* QTBUG-97594 Mac - Strikeout bugged in QML TextEdit for Japanese  
* QTBUG-106931 Windows: Dark Mode: Fusion style: Menu separator & check  
box  
* QTBUG-109739 QSGBatchRenderer calc for Z positioning results in  
negative value on Apple M1 chips clipping the top most element.  
* QTBUG-104643 qmlls leaks memory  
* QTBUG-28981 Date.setDate does nothing  
* QTBUG-109760 qmlWarning is documented as being in qqmlengine.h, but  
it's actually in qqmlinfo.h  
* QTBUG-90480 Not all overloads of Qt.matrix4x4 are listed  
* QTBUG-109867 Divergent runtime behaviour of QJSPrimitiveValue when it  
is aot-compiled and when interpreted  
* QTBUG-110023 Mouse Wheel broken inside Popup opened from a modal Popup  
* QTBUG-110242 tst_menu.qml is flaky on webOS  
* QTBUG-109567 Masked MouseArea containsMouse value incorrect after  
visibility changes  
* QTBUG-104582 -1 * 0 is not -0  
* QTBUG-104576 qmllint does not like accessing other items from  
Repeaters  
* QTBUG-104632 qmllint gives "Unqualified access" warning without  
further explanation  
* QTBUG-109380 Function overloading  with date related methods fails  
* QTBUG-106562 qmllint crashes derefencing a nullptr  
* QTBUG-109882 ShapePath: Switching from a transparent colour to a non-  
transparent one causes the wrong colour to be displayed  
* QTBUG-108664 TableView positions incorrectly  
* QTBUG-109221 Inconsistencies regarding list and value type property  
manipulations  
* QTBUG-110247 macOS: The macOS style falls back to the Basic style  
rather than the Fusion style  
* QTBUG-110112 Runtime qml won't load certain root elements  
* QTBUG-106869 QML_SEQUENTIAL_CONTAINER and QT_QMLCACHEGEN_DIRECT_CALLS  
are undocumented  
* QTBUG-109074 qmlformat removes (extra)comments  
* QTBUG-107797 linux: File selectors cannot be used  
* QTBUG-102344 PAST_MAJOR_VERSIONS doesn't work correctly  
* QTBUG-104899 QML(_NAMED)_ELEMENT should generate a clear error if the  
type in not default constructible  
* QTBUG-95448 Re-add QQmlExtensionPlugin documentation  
* QTBUG-110585 Including QJSPrimitiveValue breaks consumer builds with  
-fno-operator-names  
* QTBUG-103044 tst_qmlcppcodegen on Android complains module  
"Qt.labs.folderlistmodel" is not installed  
* QTBUG-110438 QML_SEQUENTIAL_CONTAINERS and assignment to QML property  
does not work  
* QTBUG-110590 tst_qquickpixmapcache is unstable on linux  
* QTBUG-54860 When moving the mouse quickly over items that have a  
Behavior set on font size changing when the mouse is over it then it can  
get stuck in the mouse over position  
* QTBUG-110628 [Reg 6.2 -> 6.4] Binding does not accept local signal  
handlers anymore  
* QTBUG-108155 QmlEngine complains binding of QmlListProperty to QList  
<QObject *>  
* QTBUG-109204 Obsolete linter/compiler errors on Number.EPSILON  
* QTBUG-110117 Building tst_qmlsplitlib fails  
* QTBUG-110321 qmlformat runs into an issue with ES classes  
* QTBUG-91390 ListModel doesn't keep objects of JavaScriptOwnership  
alive  
* QTBUG-95895 REG 5.15 -> 6.2: destroy() does not destroy objects after  
appending listModel.  
* QTBUG-96167 Ownership of C++ owned object flips when added to  
ListModel  
* QTBUG-106074 Add and explain naming conventions and restrictions for  
files in QML  
* QTBUG-110320 qmllint: Controls2.Action is not defined  
* QTBUG-110793 tst_qqmlvaluetypeproviders::date fails in CI  
* QTBUG-110697 Cannot use ListView.highlight when ComponentBehavior:  
Bound  
* QTBUG-110769 REG: Compiled QML yields wrong result for undefined ==  
null  
* QTBUG-110882 QQmlApplicationEngine::loadFromModule does not handle  
pure QML modules  
* QTBUG-105251 [QML] PropertyChanges can't resolve property types  
* QTBUG-110831 Compile-time warnings in Qt Quick Controls - Attached  
Style Properties Example  
* QTBUG-110906 MultiPointTouchArea signals have touchPoints arguments  
which conflict with touchPoints property  
* QTBUG-110815 Internal types are both public and internal in generated  
qmldir file  
* QTBUG-110833 qmlsc fails to detect import usage  
* QTBUG-110808 Cyclic dependency fails  
* QTBUG-110767 uint64_t and quint64 are treated differently in QML  
* QTBUG-75954 Flipable draws incorrectly when rotated and the angle is  
45°  
* QTBUG-110111 [Reg 6.3.2 -> 6.4.x] DropShadow: Changing radius to 0 at  
runtime causes a crash when attached to Canvas  
* QTBUG-106030 Updates docs to let people know if and when they should  
(not) use setContextProperty and what alternatives are  
* QTBUG-110594 containsMouse of MouseArea is always true after pressed  
with propagateComposedEvents  
* QTBUG-110454 Javascript URLSearchParams does not encode query  
parameters  
* QTBUG-111048 tst_qqmllocale::toString(locale.toString(new Date(2000,  
1, 1))) Compared values are not the same  
* QTBUG-77629 QML Flickable stealing touch events from PinchArea  
* QTBUG-109655 Pinch gestures are broken in QML Photo Surface example  
* QTBUG-85278 PinchArea inside Flickable not working properly  
* QTBUG-106223 assertion failed after Flickable takes grab from  
PinchHandler  
* QTBUG-111078 ExecutableCompilationUnit::saveToDisk() does not  
invalidate the cache it uses for loadFromDisk()  
* QTBUG-109637 6.5beta1 & 6.6 regression breaks Qt5/Qt6 code portability  
with PinchHandler runtime error caused by "import QtQuick 2.12"  
* QTBUG-110776 missing palette documentation  
* QTBUG-111088 [REG: 6.4→6.5] First evaluation of nullish coalescing and  
optional chaining  
* QTBUG-110933 qmlsc mistakes Enum for Property  
* QTBUG-107902 "Defining QML Types from C++" lacks CMake documentation  
* QTBUG-99355 tst_qmltc::listView() is flaky under qemu  
* QTBUG-101342 tst_qmltc::listView() is flaky under QNX qemu and Android  
* QTBUG-111199 FAIL!  : tst_controls::iOS::SelectionRectangle  
* QTBUG-111210 Unblacklist tst_controls::iOS::SelectionRectangle test  
cases  
* QTBUG-111204 PinchHandler native-gesture scaling is no longer  
cumulative  
* QTBUG-111290 (qdoc) warning: Undocumented parameters in  
TableView::positionViewAtIndex()  
* QTBUG-111289 (qdoc) warning: Undocumented parameter 'resourceState' in  
QNativeInterface::QSGD3D12Texture::fromNative()  
* QTBUG-108896 [REG 6.2.4-6.3.2] Using PinchHandler for Flickable's  
child makes the Flickable transparent for touch events  
* QTBUG-111179 Incorrect coercion to number for undefined  
* QTBUG-110914 Deprecated Qt.labs.settings do not link to new QtCore  
alternative  
* QTBUG-95324 JSON.stringify: replacer's `this` value is not conforming  
* QTBUG-105545 [QML] Property of QVariantMap cannot be found  
* QTBUG-108741 Math.max / Math.min implementation incomplete  
* QTBUG-111340 stdlib precondition violation in qmlcachegen  
* QTBUG-111381 QML plugins have wrong RUNPATH if CMake var  
INSTALL_QMLDIR is changed  
* QTBUG-111566 Docs: Faulty sample code in the documentation of  
SwipeDelegate QML Type  
* QTBUG-104761 acceptedButtons in DragHandler is apparently ignored  
* QTBUG-111477 [REG 6.4->6.5] Purchasing Example will not compile on  
Windows: QQmlTypeNotAvailable breaks check for default constructor  
* QTBUG-111470 Regression: cannot use QML_ANONYMOUS and QML_UNCREATABLE  
at the same time  
* QTBUG-109816 Crash when accessing enums defined in QML_SINGLETON class  
* QTBUG-111433 Pragma (pragma ComponentBehavior: Bound) doesn't allow  
ListView to be instantiated when section configured within it  
* QTBUG-111042 QML cache files are re-generated all the time when they  
contain inline components  
* QTBUG-111491 Dark Title on Dark Windows 11 when running native Windows  
Style  
* QTBUG-111511 Object destructuring breaks qmlformat  
* QTBUG-111050 ListView: BottomToTop vertical direction removes the  
transition animation  
* QTBUG-111359 Removing a button from button group does not clear  
ButtonGroup.group  
* QTBUG-111515 New Material 3 TextField placeholder text does not work  
with smaller heights  
* QTBUG-73039 hide QQuickWindow on Ubutun 18.04LTS with NVIDIA  
proprietary driver would cause crash  
* QTBUG-111557 A left button click followed by a right button click  
triggers a  doubleTabbed event  
* QTBUG-95224 anchors.verticalCenter miscalculated with real height & y  
* QTBUG-111559 Loader with States creates 2 children instead of 1  
* QTBUG-111634 CalendarModel::indexOf() returns wrong value when model  
month starts from February  
* QTBUG-111230 missing export macro for QQuickWheelEvent  
* QTBUG-111227 WASM: 'Failed to build graphics pipeline state' error  
when using QtQuick Particles  
* QTBUG-74020 PointHandler documentation examples refer to TapHandler  
not PointHandler  
* QTBUG-106878 PointHandler documentation examples refer to TapHandler  
not PointHandler  
* QTBUG-111766 qml issues in Effect Maker  
* QTBUG-111857 tst_snippets verify:qtquickcontrols-material-attributes  
fails on macOS  
* QTBUG-106968 QSGSoftwareRenderContext textures leak  
* QTBUG-111892 wasm: asynchronous image loading never ends  
* QTBUG-111935 Qt V4 JIT engine generates bad JIT code on ARM64 (and  
potentially all arches)  
* QTBUG-102589  tst_SceneGraph::render fails on Android  
* QTBUG-97557 Qt Quick batch rendering issue when a batch contain nodes  
that have different index types  
* QTBUG-32132 Qml do not updates roles names on  
QAbstractItemModel::reset signal  
* QTBUG-103220 QQmlDelegateModel::_q_modelReset should handle roleNames  
changes  
* QTBUG-95807 QtQuick: Missing headers or documentation bug  
* QTBUG-111986 qmlsc generates invalid code  
* QTBUG-97589 QSGRenderNode::matrix() returns a dangling pointer in  
QSGRenderNode::render()  
* QTBUG-111881 Incorrect example in  
QQmlApplicationEngine::objectCreationFailed documentation  
* QTBUG-111481 It is really hard to find the new Qt 6.5 qml MultiEffect  
in the docs  
* QTBUG-112159 Drawing bug with Material 3 Drawer  
* QTBUG-111995 Crash in QRhiImplementation::textureFormatInfo when using  
ColorAnimation on text containing emojis  
* QTBUG-111792 Dynamically changing the Items in a ColumnLayout while  
resizing leads to crash  
* QTBUG-111809 Qml basic type string is not well documented  
* QTBUG-111918 Null Reference Errors on Deconstruction of nested QML  
QtObjects  
* QTBUG-112322 BorderImage docs: description of border property is in a  
confusing place  
* QTBUG-25244 SVG: Unsupported Image Format when using BorderImage  
* QTBUG-112354 AnchorChanges in states are not released  
* QTBUG-106677 "Back" button breaks UI of Coffee Machine Example  
* QTBUG-108390 Code snippet for custom Dial in the document is not  
working as expected  
* QTBUG-112151 QQmlInstantiator leaks memory  
* QTBUG-91425 DelegateModel: Crash when DelegateModelGroup is used for  
delegate geometry and model is cleared  
* QTBUG-98896 Double behaviors on same property crash  
* QTBUG-98402 tst_qquickimage::mirror() is failing on macOS 12  
* QTBUG-108596 [REG 6.3.2->6.4.0] TableView consumes mouse press/click  
events  
* QTBUG-111220 PinchHandler.persistentTranslation has inconsistent  
meaning with native pinch gesture  
* QTBUG-111800 TapHandler.exclusiveSignals: you can only tap once if  
m_doubleTapTimer is used  
* QTBUG-103257 tst_qquickcanvasitem crashes on Android  
* QTBUG-41043 tst_qquickcanvasitem tends to fail on CI  
* QTBUG-112683 On macOS, a QML module is not placed inside the bundle  
* QTBUG-112712 [6.5] "QtQuick" dependency on `QmlMeta`  
* QTBUG-95940 tst_qquicktextinput is flaky on OpenSUSE  
* QTBUG-111231 qmlformat does not preserve whitespace in comments and  
whitespace following header comments  
* QTBUG-111902 [Reg 5.15 -> 6.4.2] Loader with StackLayout and Repeater  
displays an incorrect index  
* QTBUG-107037 MultiPointTouchArea with enabled:false blocks events to  
MouseArea  
* QTBUG-108226 quickwidget example crash in QAccessibleQuickWindow /  
QMacAccessibilityElement  
* QTBUG-110592 [REG: 6.4->6.5.0-beta1] Quick tests now open a window  
* QTBUG-111504 Text loses selection when releasing long-press on Android  
text input  
* QTBUG-110850 selectAll does nothing in onFocusChanged triggered by  
touch input  
* QTBUG-112348 Make the options which can be used to control Qt Quick  
Compiler easier to find  
* QTBUG-112859 crash in tst_statemachineqml  
* QTBUG-109721 Non-Editable ComboBox wrongly propagates KeyEvent that  
has already been accepted  
* QTBUG-112838 'visible' of QQuickItem cannot be set to 'true' again  
after being set to 'false' once.  
* QTBUG-84920 StackView's depth is not updating after clear()  
* QTBUG-101985 ListView does not relayout its children when section  
delegate height changes  
* QTBUG-100002 QQuickListView: No layout update is triggered when a  
section delegate has its geometry changed.  
* QTBUG-112860 Binding doesn't seem to be released on changed 'when'  
property  
* QTBUG-106529 QtQuick.Shapes docs lacks mentionning how to make it  
smooth  
* QTBUG-112463 Very pixelated edges of text in PathText  
* QTBUG-110625 QML ListView creating delegate instances for ALL model  
entries  
* QTBUG-89568 Binding delegate height to ListView height causes  
delegates to be created unnecessarily  
* QTBUG-51773 When the height of a delegate is bound to the height of a  
ListView with a large model count, the application is blocked for  
several seconds  
* QTBUG-112434 [Regr: 6.3.1->6.3.2] MouseArea stays pressed after double  
click on touch screen  
* QTBUG-109393 [Regr: 6.3.1->6.3.2] iPad: DoubleClicking in MouseArea +  
Popup breaks  
* QTBUG-111322 HoverHandler example is broken in  
qtdeclarative/examples/quick/pointerhandlers  
* QTBUG-110114 Qt Quick Controls Button: Unable to override  
Accessible.role  
* QTBUG-112208 Assignment to a list property emits property change event  
for every item in the list  
* QTBUG-70939 QML ComboBox popup menu doesn't respect scaling  
* QTBUG-102393 QQmlEngine::retranslate no longer retranslates strings  
coming from C++  
* QTBUG-112227 qmlsc: QQmlProperlyLists assignment to QML lists cannot  
be compiled  
* QTBUG-110718 QML_ATTACHED in QQuickAttachedPropertyPropagator  
* QTBUG-112691 StackLayout Visible Item Does Not Update During Inserts  
* QTBUG-111439 qmlsc: Cannot compile function if this is passed as an  
argument to another  
* QTBUG-113226 Flickable emit flickStarted even though the child is  
processing the pinch gesture  
* QTBUG-112924 movementStarted/movementEnded signals are not emitted,  
the flickStarted/flickEnded signals with flick behavior still occur.  
* QTBUG-113265 Segmentation fault in  
examples/positioning/satelliteinfo/Main.qml  
* QTBUG-104987 REG: flicking TableView is broken  
* QTBUG-112945 QML RangeSlider does not work well on touch screen  
* QTBUG-113172 Qt 6.5 Material TextField placeholder breaks with  
alignment  
* QTBUG-112897 Can't build app when there is a function in QML Dialog  
* QTBUG-112837 QML fails to bind to QObject property (defined with  
Q_OBJECT_BINDABLE_PROPERTY and BINDABLE) that are a type Q_GADGET  
* QTBUG-112529 MultiPointTouchArea signals deliver QList<QObject*>  
* QTBUG-113353 Crash with qt.qml.binding.removal.info category enabled  
while breaking a binding  
* QTBUG-99363 [Reg 5.15 -> 6.2] Properties are not set on createObject  
* QTBUG-113312 grabToImage example fails  
* QTBUG-113321 Material TextArea and TextField placeholder text  
incorrectly clipped  
* QTBUG-112949 splice does not work on list properties  
* QTBUG-106266 [Reg 5.15 -> 6.x] Component.createObject() mangles passed  
properties  
* QTBUG-112291 QML_SEQUENTIAL_CONTAINERS affects isArray and breaks  
ComboBox  
* QTBUG-112946 amendException in QQmlJSAotContext can amend wrong stack  
frame  
* QTBUG-113221 -no-feature-qml-devtools does not build  
* QTBUG-113472 [REG 6.4.1->6.5.0] Qt.binding in initial properties  
silently fails for certain types  
* QTBUG-113474 REG: Material.background has no effect on flat buttons  
* QTBUG-113465 QQmlJSCodeGenerator::argumentsList() disregards most type  
wrappings  
* QTBUG-112740 SplitView: Incorrect Rendering Between Layouts and  
Transparent Items  
* QTBUG-113236 [REG] QQuickItem::ItemDevicePixelRatioHasChanged is  
triggered with a wrong value  
* QTBUG-113484 [REG] Unable to determine callable overload  
* QTBUG-106164 ListView doesn't render Text in delegates on dataChanged  
signal  
* QTBUG-106205 QML Text are not rendered if outside the screen at its  
creation  
* QTBUG-108803 Named import not recognized  
* QTBUG-64151 "Error: Locale: Number.fromLocaleString(): Invalid format"  
when erasing last digit of "2,000" in editable SpinBox  
* QTBUG-103205 SpinBox, no way to listen for text entered  
* QTBUG-113446 KTX, ASTC, PKM image not displayed using NinePatchImage  
* QTBUG-100678 QML Runtime Tool help all option is not working  
* QTBUG-113565 Enhance the warning about the vendor and platform  
specificness of compressed texture format support in the Image docs  
* QTBUG-88195 Change SplitView orientation  
* QTBUG-35244 QWindow visibility/visible property conflict  
* QTBUG-113673 ColorDialog don't resize correctly on small screens  
* QTBUG-112618 Wearable Example Home and Back Button Images Don't Load  
* QTBUG-108541 TreeView: cannot change root index  
* QTBUG-111679 Item or Rectangle not able to gain focus after Drawer is  
closed  
* QTBUG-97974 Using TextArea inside ScrollView produces binding loop  
warnings  
* QTBUG-113439 Specifying RESOURCES to qt6_target_qml_sources does not  
make file level dependency  
* QTBUG-113744 Misguiding error message  
* QTBUG-108689 TapHandler does not react to clicks when combined with  
PinchHandler  
* QTBUG-113005 Tap handlers are broken on Android.  
* QTBUG-113469 QML ComboBox breaks dark mode window styling  
* QTBUG-113852 [Reg Qt6.4->6.5] The contentWidth of QML TableView is 0  
* QTBUG-112840 Please write the realistic usecase of Qt Quick Test to  
the documentation  
* QTBUG-113853 [REG 5.15.x -> 6.3/6.4/6.5] Mouse Events not accepted on  
a MouseArea placed inside modal Popup::background  
* QTBUG-113725 Findings for qmlls  
* QTBUG-76830 QML ListView with variable sized delegates causes attached  
scroll bar to change sizes and skip around in an unwanted manner  
* QTBUG-108171 ScrollBar with sections is jumpy  
* QTBUG-112858 [Windows] Quick TextEdit with RTL text placed into a  
ColumnLayout has wrong alignment  
* QTBUG-112836 TableView multiple selection can't be disabled  
* QTBUG-112835 TableView selection Shift/Ctrl click behaviour absent  
* QTBUG-113584 Typo in the code snippet  
* QTBUG-114163 FAILED: qtdeclarative/src/qmlcompiler/CMakeFiles/qch_top_  
level_docs_QmlCompilerPrivate  
* QTBUG-112613 No way to navigate to a parent topic for Qt Quick  
Compiler doc pages  
* QTBUG-113454 Links for 'Qt Quick Effects', 'Qt Quick Particles'  
landing pages do not work  
* QTBUG-113743 QKeySequence cannot be sent to QML Shortcut from C++ side  
* QTBUG-114340 FAIL!  : tst_usertypes::watcherInQml()  
* QTBUG-113752 Warning when assigning to Map.visibleRegion  
* QTBUG-105862 [REG] Qt6.3.1 a MultiPointTouchArea inside another  
MultiPointTouchArea is reporting the wrong touch location  
* QTBUG-114364 qmlformat changes ComponentBehavior  
* QTBUG-114086 [Reg 6.4 -> 6.5] Historical NativeMethodBehavior is  
broken when a Q_INVOKABLE function is stored in a QML property  
* QTBUG-114358 ComponentBehavior: Bound causes 'QQmlContext: Cannot set  
property on internal context'  
* QTBUG-110589 Property bindings produce wrong values for Animation.to  
* QTBUG-61282 Changing an Animation duration has no effect  
* QTBUG-95840 QML Animations: not specified how they react to property  
changes while running  
* QTBUG-113497 QGuiApplication::setLayoutDirection does not change the  
window to RTL  
* QTBUG-114418 qmlsc: compile error with === or !== against undefined or  
null  
* QTBUG-113745 Qt Quick 2D Renderer: Partial scene update might erase  
items at fractional coordinates  
* QTBUG-97055 QQC2 Flickable scrolling is not linear with clicky wheels  
on Qt 6.2.0  
* QTBUG-106338 [5.15.7 -> 5.15.8] Change in Flickable acceleration  
* QTBUG-35609 Flickable speed and deceleration are not easily  
customisable  
* QTBUG-80720 More controls for touchpad scrolling. Stopping Flickable  
extra scrolling.  
* QTBUG-82565 Scrolling QML views with mouse wheel or touchpad is quite  
bad  
* QTBUG-113009 TextEdit: rendering issue when highlighting text  
* QTBUG-80788 [5.14 REG] New properties in ComboBox clash with custom  
properties (revision ignored)  
* QTBUG-100392 Animations crash at runtime because list properties do  
not emit onChanged signal when their items are destroyed  
* QTBUG-114407 [Boot2Qt] UI of imagine style example - automotive is  
distorted on B2Qt devices  
* QTBUG-114430 heap-use-after-free when assigning undefined to width and  
height of Control background item  
* QTBUG-114458 [Reg 6.2->6.3] Component.createObject() no longer copies  
QQmlListProperty values correctly  
* QTBUG-114421 Documentation error on ListView orientation table  
* QTBUG-114602 Documentation: LineShape is part of QtQuick.Particles?  
* QTBUG-113714 REG: Memory leak when loading/unloading application fonts  
* QTBUG-114494 QML rect property as a parameter causing a crash  
* QTBUG-109995 Can not interact with tumblers inside interactive  
flickable on touch  
* QTBUG-113653 [REG 5.15->6.2.3] MultiPointTouchArea doesn't receive  
gestureStarted signal when used inside PathView or Flickable  
* QTBUG-114329 [Reg 5.15 -> 6.2] QML Binding on new object not re-  
evaluated  
* QTBUG-113854 V4 Crashes when using Reflect.ownKeys(...)  
* QTBUG-114561 Material style highlighted & flat button shows no text  
* QTBUG-114492 Automotive example's Dial background image has  
downscaling artifacts  
* QTBUG-114691 Rectangle (with gradient) software backend does not match  
RHI backend  
* QTBUG-114476 qmlsc: crashes with let and control structs  
* QTBUG-98365 Memory leak with removed persisted items  
* QTBUG-114643 ResolveOverloaded: debug messages use QtInfoMsg  
* QTBUG-113495 Examples imageprovider and imageresponseprovider leave  
garbage files under the qt5 build directory  
* QTBUG-114483 Line number in warning is random and out of bounds  
* QTBUG-114815 qmlcachegen triggers AddressSanitizer stack-buffer-  
overflow error  
* QTBUG-114715 Doc: Stale info about QML module versioning  
* QTBUG-113855 qmlsc: unused import false positive for template strings  
* QTBUG-114186 QQC leaks attached objects  
* QTBUG-114874 REG [5.15 → 6.x]: With `height: implicitHeight` binding  
changes to implicitHeight won't trigger property interceptor (e.g.  
Behavior + Animation)  
* QTBUG-113738 [REG 6.4.3 -> 6.5.0] TableView positionViewAtCell crash  
* QTBUG-114808 Quick3d examples don't compile for QNX  
* QTBUG-114607 Flickable.StopAtBounds not working anymore with a wheel  
* QTBUG-110328 QEventPoint not being released correctly  
* QTBUG-114687 Qt.application.screens does not update if primary screen  
changes  
* QTBUG-114858 Dynamically adding State causes Segfault  
* QTBUG-114961 Regression: Keyboard input unusable with redirected Qt  
Quick scenes (QQuickRenderControl)  
* QTBUG-114986 Qml's typeregistrar is not parsing namespaces correctly  
* QTBUG-114897 Generated QML code doesn't compile with -Wshadow -Werror  
* QTBUG-114910 Missing constructor params crashes program  
* QTBUG-111013 HorizontalHeaderView with resizableColums true eats input  
when visible (Quick 3D DebugView)  
* QTBUG-113991 [Reg 6.4 -> 6.5] qmldir javascript library does not  
respect qualified import  
* QTBUG-114693 Galleryexample app Textarea and Drawer bug.  
* QTBUG-115106 State switched model crashes with ComponentBehaviour  
Bound  
* QTBUG-115179 Clip optimization in  
QQuickDeliveryAgentPrivate::pointerTargets is too aggressive  
* QTBUG-114978 Wearable example icons hard to distinguish from  
background and other cosmetic issues  
* QTBUG-110827 Qt's Gallery example producing tons of warning/errors  
* QTBUG-109306 Standard virtual keyboard typing does't generate standard  
QML events.  
* QTBUG-114166 resizing of ListView (possible Flickable) change in  
qt6.5.1  
* QTBUG-108144 Race condition when using QQuickMenu  
* QTBUG-95107 ListView item pooling breaks fetchMore  
* QTBUG-115159 QmlCache cpp files are always generated differently  
* QTBUG-115320 memcpy-param-overlap in qv4runtime.cpp  
* QTBUG-115115 [Reg 5.15 -> 6.2]  
QV4::Heap::QObjectMethod::ensureMethodsCache crash when calling a  
function in a js file  
* QTBUG-58718 Problems with JS array sorting after unshift  
* QTBUG-115278 [Reg 6.5 -> 6.6] qmlsc: accessing string list crashes  
* QTBUG-114596 Ownership of QObject* returned to qml by Q_INVOKABLE  
differs for const and non-const pointers  
* QTBUG-115523 [REG: 6.5.1->6.5.2] More complex javascript objects not  
converted to QVariantMap anymore  
* QTBUG-115557 Missing type "QQuickTapHandler::ExclusiveSignals" in  
property  
* QTBUG-114258 Cannot click on buttons inside Flickable in QQuickWidget  
with stylus  
* QTBUG-115251 Infinite loop in QPropertyObserverPointer::notify on  
startup  
* QTBUG-115319 Issue with number as a context property name  
* QTBUG-115322 Theme properties set on Item are not propagated to  
children  
* QTBUG-108275 Qmlformat issue with js objects keys  
* QTBUG-114839 qmlformat: Cannot format object destructuring  
* QTBUG-115537 [QML Docs] Image.fillMode enum documentation has a broken  
table formatting  
* QTBUG-104904 [REG 5.15.9 -> 6.3.1] SwipeDelegate does not forward  
mouse events to nested items in left, right, behind  
* QTBUG-115526 qmlcachegen fails to compile SetLookup for non-final  
properties  
* QTBUG-115733 [REG 6.5.1-6.5.2] Automatic conversion JS Array ->  
QByteArray is broken  
* QTBUG-113842 DropArea blocks scrollwheel of a mouse  
* QTBUG-115468 Dynamically adding items to SwipeView may add new items  
behind the current item  
* QTBUG-105090 tst_QQuickMenu AddressSanitizer: heap-use-after-free in  
QQmlData::signalHasEndpoint(int)  
* QTBUG-114801 qmlformat: two spaces in 'NumberAnimation on x  {'  
* QTBUG-115951 qml::UnknownTestFunc() QVERIFY()  
* QTBUG-116028 Material Switch doesn't respect Dense variant  
* QTBUG-115948 Calqlatr example - missing Qt Shader Tools module  
* QTBUG-115949 QML Gallery - missing Qt Shader Tools module  
* QTBUG-104469 Assertion failure when clearing model in  
Component.onCompleted of delegate in Repeater  
* QTBUG-115510 undefined reference to `QQuickTextLine::staticMetaObject'  
when using qmlsc in direct mode  
* QTBUG-113940 FileSelector doesn't work correctly  
* QTBUG-114655 heap-use-after-free when calling console.log() (and  
friends) from QML using cachegen  
* QTBUG-116148 A property alias for a property alias leads to a segfault  
in QQmlPropertyCacheAliasCreator<QV4::ExecutableCompilationUnit>::proper  
tyDataForAlias()  
* QTBUG-98859 Implicit conversion to Component doesn't work in inline  
components  
* QTBUG-116049 [Reg 6.2 -> 6.3] Segmentation fault when using attached  
`Component` property with `Binding`  
* QTBUG-116304 Missing code snippet in Scene Graph - Vulkan Under QML  
example  
* QTBUG-116228 Garbage collector can crash the QML Debugger  
* QTBUG-114482 [Boot2Qt] Cannot run Attached Style Properties example on  
Boot2Qt device  
* QTBUG-116390 Bad revision data in QtCore qmltypes  
* QTBUG-105745 QtQuick.Dialogs.quickimpl plugin not linked in static  
builds  
* QTBUG-115707 REG: Child popup inherits palette from parent popup  
rather than its associated window  
* QTBUG-116088 Infinite conversion chain in qmlcachegen [QPoint <->  
QPointF]  
* QTBUG-116571 Qt Quick render loop crashes when losing the graphics  
device  
* QTBUG-114326 [REG] Non-Singlebit Q_FLAGS not exposed correctly in  
property declarations  
* QTBUG-114467 qmllint does not warn about unqualified id lookup  
* QTBUG-116617 qmldom spelling error in tag attribute  
* QTBUG-116399 BorderImage produces warning  
* QTBUG-116749 missing right bracket  
* QTBUG-116587 If using QQuickRenderTarget and setMirrorVertically(true)  
will lead to the qml Item's clip area damage  
* QTBUG-116576 [REG 6.2 → 6.4]: Connections and signals whose names  
start with an underscore  
* QTBUG-116106 New accentColor role is missing from QQuickColorGroup  
* QTBUG-115328 Invalid qmllint_json target generated  
* QTBUG-114068 Top level items are not resized to the window size.  
* QTBUG-116753 qml - qmlscene root item sizing discrepancy  
* QTBUG-115687 Text loaded with Loader inside Flickable is not visible  
when scrolling  
* QTBUG-115004 [Android] TextEdit text selection works incorrect  
* QTBUG-115485 QtQuick shapes example has misleading file names  
* QTBUG-107707 tst_qquickimageparticle fails with Ubuntu 22.04  
* QTBUG-109383 Re-enable building examples with qmake in non-qtbase  
repos  
* QTBUG-108150 Adding qml files from the build folder to the QRC is  
creating filenames so long it breaks the build on Windows host  
* QTBUG-109111 qmlsc should support casting of various int types  
* QTBUG-109373 DragHandler and PinchHandler: meaning of axis  
persistentValue is wrong  
* QTBUG-109459 call to QQuickPopup::setVisible() from dtor bypasses  
virtual dispatch (ToolTip)  
* QTBUG-109392 Deprecations in QQuickPinchHandler are done incorrectly  
* QTBUG-109488 tst_qquicktextedit FAIL  
* QTBUG-109506 QQuickItemLayer::updateOpacity can be called with no  
effect internally and assert/crash  
* QTBUG-108820 Infinity - real vs int  
* QTBUG-109235 Review toupper/tolower uses [Qt]  
* QTBUG-109553 CMake deployment API creates too deep directory hierarchy  
when DESTDIR is set  
* QTBUG-109869 The INTEGRITY linker crashes on tst_qqmlfileselector  
* QTBUG-109942 Crash when running the qtdeclarative gallery example  
* QTBUG-97518 Mac, Metal RHI - runtime warnings "UI API called from  
background thread".  
* QTBUG-35608 Flickable speed and deceleration does not scale with pixel  
density  
* QTBUG-110009 Multi Languge related documents for Qt6 is not consistent  
* QTBUG-110029 [6.5] qmltc with signals does not compile  
MouseArea.onPressed  
* QTBUG-104679 [REG 6.2.4-6.3.1] ListView: ASSERT if PullBackHeader or  
PullBackFooter is used  
* QTBUG-106929 Qml Singletons do not work on Android  
* QTBUG-99146 URI and VERSION should be optional in qt_add_qml_module  
* QTBUG-84328 QML Animators with a weird start behavior  
* QTBUG-109314 Crash during QML item creation  
* QTBUG-111008 qtdeclarative flaky tst_qqmlprofilerservice test  
* QTBUG-63381 Transient scrollbars do not work when using style sheets  
* QTBUG-104570 QQuickHandlerPoint has no QML_ELEMENT declaration  
* QTBUG-111187 QtQuick.Layouts not included during linking when using  
ColorDialog  
* PYSIDE-903 QProgressDialog.setCancelButton() Is documented to accept  
0, but does not.  
* QTBUG-111564 FolderDialog won't open if its parent is an Item  
* QTBUG-95395 Code snippets for HoverHandler show TapHandler  
* QTBUG-70397 TapHandler fires for all overlapping items  
* QTBUG-73262 it's confusing that TapHandler.gesturePolicy affects event  
propagation  
* QTBUG-100534 TapHandler doesn't stop propagation  
* QTBUG-107239 DragHandler propagates tap event through Flickable to  
underlying TapHandler  
* QTBUG-111310 \image tag breaks \value block  
* QTBUG-111532 qmlsc when enabled gives many errors/warnings  
* QTBUG-65088 TapHandler: detecting double-clicks is not declarative  
enough  
* QTBUG-107264 TapHandler.singleTapped is emitted immediately before we  
know whether a double-tap will occur  
* QTBUG-111741 qt_deploy_runtime_dependencies() doesn't install project  
linked libraries & adds undocumented vcredist installer  
* QTBUG-111014 QTest backslash escape issue  
* QTBUG-111176 Views pass either "model" or "modelData" to delegates,  
depending on type of model  
* QTBUG-110980 ComponentBehavior: Bound and generic delegates don't mix  
well  
* QTBUG-104752 No way to support both single and multi-role models in  
delegates that use required properties  
* QTBUG-101488 tst_QQuickFileDialogImpl is flaky  
* QDS-8545 Buttons in default style do not have the correct implicit  
size in the form editor  
* QTBUG-111570 ASSERT: "newInstance != d->animationInstance" in file  
qquickbehavior.cpp  
* QTBUG-111595 Qml Menu, inherited property "opened" is not working  
* QTBUG-112696 QQuickWidget::focusPreserved test fails with RHI warnings  
* QTBUG-112180 Properly support enums with underlying type != int  
* QTBUG-106118 Changing contentItem to ScrollView breaks scrollbar  
visibility  
* QTBUG-111012 [Reg 5.15 -> 6.x] QSGGeometry::DrawLineLoop is no longer  
supported  
* QTBUG-112650 TextArea decorator not working as intended  
* QTBUG-53709 XMLHttpRequest missing overrideMimeType method  
* QTBUG-104323 Not possible to close a modal ComboBox popup by clicking  
on the ComboBox  
* QTBUG-113116 Documentation typos, errors and improvements  
* QTBUG-113138 Copyright statements and license identifiers appear in  
the HTML  
* QTBUG-113148 Build error in qqmllist.h on Windows  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-50161 ProgressBar and BusyIndicator are very CPU intensive  
* QTBUG-113227 ABI issue with QVariant and metatypes from Qt < 6.5  
* QTBUG-98790 ChangeListeners get called even after being semi-deleted  
* QTBUG-112762 QMetaProperty::write detaches value argument  
* QTBUG-112480 QmlCompiler does not care about shadowing of methods  
* QTBUG-113473 [REG 6.4.1->6.5.0] Assigning undefined to gadget qreal  
property doesn't reset  
* QTBUG-113230 Unexpected width behaviour when using  
Layout.horizontalStretchFactor  
* QTBUG-111946 How should QML modules be installed with cmake (with Qt  
6.4 or later)?  
* QTBUG-113015 [QDoc] Duplicate QML property name causes confusion:  
qml[attached]property QWindow::Visibility Window::visibility  
* QTBUG-104624 When a HoverHandler is placed inside an Item, the  
parent's children do not get the Hoverevent.  
* QTBUG-108739 Most properties in QtQuick are not FINAL and can be  
shadowed  
* QTBUG-114073 qdoc resolves "QML Import Path" reference incorrectly  
* QTBUG-113426 Crash in QtRhi with QQuickWidget  
* QTBUG-112306 Crash in QRhiResourceUpdateBatch::merge  
* QTBUG-111779  change signal of contentData and contentChildren in  
Dialog doesn't work  
* QTBUG-113228 Pane only stops some input events from propagating  
* QTBUG-106683 qt_add_qml_module: _automoc_json_extraction target and  
resources are rebuilding every time with Visual Studio Generator  
* QTBUG-89699 QQC2 SplitView does not honor size constraints when parent  
is resizing  
* QTBUG-107836 SplitView sizing issues  
* QTBUG-89023 tst_Animators::testTransitionsWithImplicitFrom is flaky on  
Ubuntu  
* QTBUG-114396 Change "OpenGL" to "Graphics API"  
* QTBUG-114571 Incorrect colors after switching between light and dark  
modes  
* QTBUG-114718 [Tests] tst_QQuickPopup fails  
* QTBUG-114845 qt6 qml documentation: "font.style" should be  
"font.styleName"  
* QTBUG-40856 MouseArea containsMouse flag is not reset on Touch Screen  
* QTBUG-86729 many Qt Quick test failures after input event refactoring  
* QTBUG-114959 Pushing Qt.binding to JS variable in StackView results in  
the pushed item's property not reacting to changes  
* QTBUG-114475 QML QQuickPointerHandler crashes  
* QTBUG-112537 A Window's background cannot be semitransparent anymore  
* QTBUG-113456 Window background cannot be transparent.  
* QTBUG-115015 [REG 5.15.14->6.5.1]: Qt6 QML component Window setting  
property color: "transparent" doesn't make the Window transparent for  
Windows 11 and MacOS  
* QTBUG-115140 qtdeclarative -unity-build-batch-size 100000 fails  
* QTBUG-68404 Using property values in QML animations triggers an  
assertion  
* QTBUG-84314 Fix QQuickPixmapCache to cache large images rendered by  
complex image plugins, and dispose via LRU algorithm  
* QTBUG-61783 SwipeDelegate left and right components not reacting on  
touchscreen press  
* QTBUG-114338 Qt Quick with metal crashes on older macOS 11  
* QTBUG-61646 Sample code for GridView.isCurrentItem is in the wrong  
place  
* QTBUG-115317 ListView can't reuse items when its integer model is  
modified  
* QTBUG-114688 QML application does not start if some QML modules are  
built static  
* QTBUG-115554 QQuickAttachedPropertyPropagator cannot propagate through  
popup and window  
* QTBUG-114953 PdfMultiPageView: Very poor memory performance when  
zooming in/out of long documents  
* QTBUG-107771 QML Native ScrollBar: Unable to assign [undefined] to int  
* QTBUG-116742 tst_qqmlbinding Failed  
* QTBUG-116537 Add \examplecategory to qtqml  
  
### qtactiveqt  
* QTBUG-111718 QAxScript: Changed value of ByRef parameter is not  
returned  
* QTBUG-56172 ActiveQt components are not well behaved when  
unloading/reloading  
* QTBUG-109235 Review toupper/tolower uses [Qt]  
* QTBUG-110158 Invalid QApplication construction with argc=0  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-111191 Qutlook Example (ActiveQt) crashes with Qt6.4.2  
  
### qtmultimedia  
* QTBUG-108995 Seeking on a paused audio file causes it to "play" it  
* QTBUG-103567 QML MediaPlayer fails to playback rtsp media properly.  
* QTBUG-108221 QAudioOutput crashes on Qt 6  
* QTBUG-109443 Android: tst_QVideoWidget timeout  
* QTBUG-59726 no access to second camera on android phones with dual  
front/back cameras  
* QTBUG-109583 Doc: Stale references in QAudioDevice docs  
* QTBUG-109535 infinite loop in ffmpeg camera check  
* QTBUG-108676 Streaming audio from source to sink fails in Qt6,  
succeeds in Qt5  
* QTBUG-97265 Qt6 mediarecorder QML has invalid syntax in example code  
* QTBUG-109539 Devices example crash  
* QTBUG-109415 Camera is automatically activated by CaptureSession  
* QTBUG-109613 duplicate symbols in gstreamer and ffmpeg backends  
* QTBUG-109561 QML Camera working on Android is random  
* QTBUG-109391 Camera goes black after turning off and on.  
* QTBUG-110285 Deadlock in QAndroidCamera destruction  
* QTBUG-110131 QML Camera unloading crash on iOS  
* QTBUG-109956 Example manifest data for Spatial Audio Panning Example  
wrong  
* QTBUG-110317 Camera active state does not work as expected  
* QTBUG-110797 On android devices, when a 'Video' object is destroyed,  
the screen does not detect mouse events any more  
* QTBUG-109659 Audio capturing and playing does not work on Android  
* QTBUG-110844 QMediaRecorder frequently returns unknown errors when  
trying to record on Mac  
* QTBUG-104849 audio input examples do not work on mac os  
* QTBUG-111269 QtMultimedia doesn't build with libva-devel  
* QTBUG-98373 QAudioOutput not working on WebAssembly  
* QTBUG-110995 Qt Multimedia Video not working on Nvidia Xavier and Orin  
platforms  
* QTBUG-110975 [Camera] Qt QML camera view on android is distorted in  
portrait view  
* QTBUG-111266 VideoOutput aspect ratio is not correct on Android in  
portrait view  
* QTBUG-111421 Camera preview ratio is not respected for portait  
orientation  
* QTBUG-107173 QML Camera is stretched the first time on Android  
* QTBUG-110868 QML Video crashes on macOS when lazy-loaded  
* QTBUG-110812 Camera not working when using OpenGL Renderer (macOS,  
iOS)  
* QTBUG-111900 FFMPEG library incompatibility on desktop builds  
* QTBUG-111944 wasm: QtMultimedia asks for mic and camera input for  
playing videos  
* QTBUG-98102 [macOS] Specific video can't be played  
* QTBUG-112315 wasm: multimedia examples do not build with qmake  
* QTBUG-110466 Combo Boxes in QML Video Recorder example don't populate  
* QTBUG-112352 Crash when destroying page with camera linked to  
VideoOutput  
* QTBUG-112679 Spectrum Example Doesn't Work  
* QTBUG-112847 player example fails to play any video on iOS  
* QTBUG-109167 QSoundEffect is stuck in Loading state  
* QTBUG-110005 windows: Crash if using asynchronous IO device as a media  
source  
* QTBUG-112601 Spatial Audio is marked as Tech Preview  
* QTBUG-108083 Video color change while playing in QML MediaPlayer  
* QTBUG-113008 REG [6.5.0->6.5.1] camera example not compiling on  
Android  
* QTBUG-112832 Building Qt 6.5.0 for Windows fails  
* QTBUG-113286 [REG 6.4.3-6.5.0] [darwin] QMediaPlayer produces invalid  
frames on custom QVideoSink  
* QTBUG-112973 MediaPlayer example cannot open any file  
* QTBUG-113386 MediaPlayer: error, errorString property changes are not  
notified  
* QTBUG-105372 QML Camera - setting zoomFactor does not work  
* QTBUG-113029 Android: declarative-camera example: Captured image is  
not rotated for landscape orientation  
* QTBUG-112454 Android-Multimedia know issue with pixel format need to  
be documented  
* QTBUG-113263 wasm: error when switching cameras  
* QTBUG-111912 The content in MediaPlayer is not cleared, when the next  
file has no video or cover art  
* QTBUG-114061 WebAssembly audio output not working  
* QTBUG-112226 android: Camera does not work  
* QTBUG-114889 Android: Camera does not work at all  
* QTBUG-114659 [DeclarativeCamera] Zoom control is incorrectly  
positioned and does not work on Android  
* QTBUG-114660 [DeclarativeCamera] Locking the phone causes the app to  
crash on Android  
* QTBUG-114039 App crash after changing Media Player source  
* QTBUG-113832 6.5.1 Qt MM crashes when playing a simple mp4 on AMD  
cards  
* QTBUG-111543 Heavy flickering with 60 fps videos  
* QTBUG-111911 Some videos has artifacts when playing in MediaPlayer.  
* QTBUG-111459 Heavy jittering in video playback if animations are  
active  
* QTBUG-109213 Video flickering when there is a ParticleSystem component  
or playing some animation at same time  
* QTBUG-114658 [DeclarativeCamera] The image is displayed upside down  
when using the front camera  
* QTBUG-99709 The size of the video missing in QMediaMetaData  
* QTBUG-115122 Documentation: PlaybackRate is not only about audio  
speed.  
* QTBUG-115360 QAudioDevice is exported twice  
* QTBUG-115563 QCameraDevice is declared twice in the qmltypes file  
* QTBUG-115564 QMediaFormat is declared twice in the qmltypes file  
* QTBUG-115566 QMediaMetaData is declared twice in the qmltypes file  
* QTBUG-115842 Android: Cannot take photo if CONTINUOUS_PICTURE  mode  
unavailable  
* QTBUG-109710 [EVR] Crash on readWglNvDxInteropProc() with nullptr  
access  
* QTBUG-115747 H264 MKV duration and position is zero  
* QTBUG-115843 Android:  Supported flashmodes not cleared in FFmpeg-  
backend  
* QTBUG-116451 QML Camera blank white screen (qmake)  
* QTBUG-116533 Sporadic crash on QSGVideoMaterial::updateTextures() with  
nullptr access  
* QTBUG-108412 Playing mjpeg streams through ffmpeg crashes  
* QTBUG-109491 Ffmpegdecoder fails in documentation build with Ubuntu  
22.04: invalid conversion  
* QTBUG-108176 [macOS] QAudioDevice "perferedFormat" warnings  
* QTBUG-109168 Unloading Camera (QML) item on Android hangs app.  
* QTBUG-97166 Qt6 Multimedia - Subtitle Language Metadata Detection  
Incorrect?  
* QTBUG-108403 FFmpeg backend doesn't work as expected  
* QTBUG-106533 Android: jar and src dirs are installed in /usr if  
CMAKE_INSTALL_PREFIX=/usr  
* QTBUG-110453  tst_QVideoWidget::fullScreen fails with Android target  
in RHEL-8.4  
* QTBUG-109149 [Windows] Crash on MFPlayerControl::handleStatusChanged()  
* QTBUG-103611 [Reg 5.15 -> 6.x] Re-initializing QGuiApplication causes  
QQmlApplicationEngine to crash  
* QTBUG-109731 6.4.2, 6.5beta1 & 6.6 regression QML MediaPlayer shows  
Corrupt/Blank Video If Playback Starts at Launch  
* QTBUG-108693 [EVR] Crash on D3DPresentEngine::makeVideoFrame  
* QTBUG-98506 QImageCapture not functioning properly on boot2qt embedded  
device  
* QTBUG-111567 masOS audio deadlock with AudioOutputUnitStart /  
AudioOutputUnitStop  
* QTBUG-111209 QML Multimedia looping broken  
* QTBUG-111744 QtMM macOS CI: mediaplayer crashes if playing long video  
of with high playback rate  
* QTBUG-110708 [REG: 6.4->6.5-beta2] ffmpeg cannot play http stream  
* QTBUG-99098 Android tst_QMediaCaptureSession test failed  
* QTBUG-108892 Preview of QScreenCapture with HDR display appears dark  
* QTBUG-109009 Ffmpeg: videotoolbox doesn't support some yuv 8bit  
formats  
* QTBUG-111213 FFmpeg: Audio stream from one device to another  
* QTBUG-112305 Ffmpeg looping is not seamless  
* QTBUG-112827 tst_QScreenCaptureIntegration::recordToFile  
* QTBUG-111951 [Reg 6.4->6.5] QMediaPlayer does not support video files  
with Chinese names  
* QTBUG-112714 Unable to access camera  
* QTBUG-112702 QMediaDevices::videoInputs returns empty list when used  
alone  
* QTBUG-112707 Qt6 Multimedia: cannot open file if file path contains  
non-ascii characters  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-113621 Missing method of setting (video)resolution for QML  
MediaRecorder  
* QTBUG-113782 error: no member named 'unary_function' in namespace  
'std'  
* QTBUG-112512 QSoundEffect cuts out on very short sounds ( ~ 0.2 - 0.3  
seconds )  
* QTBUG-112219 `QMediaDevices::defaultAudioInput()` wrong device  
* QTBUG-114202 QtMultimedia should not crash (qFatal) when using dummy  
implementation  
* QTBUG-110071 [REG 6.3.1->6.4.1]Problems with QMediaDevices  
'videoInputs' and 'videoInputsChanged'  
* QTBUG-114442 [REG 6.5.1->6.5.2] namespace build fails on Windows,  
Multimedia  
* QTBUG-113211 Windows: QMediaPlayer stuttering with some wave files  
* QTBUG-113481 MediaPlayer not reading video orientation metadata  
* QTBUG-115212 [Possible regression 5.15->6.4/6.5]Cannot load video from  
device on Windows Network in 6.4/6.5  
* QTBUG-111975 QVideoFrame::toImage has a memory leak at 3840 * 2160  
resolution  
* QTBUG-114174 Camera active property stays true when stopped  
* QTBUG-115763 CMake Error at /home/qt/work/install/lib/cmake/Qt6Multime  
dia/Qt6QFFmpegMediaPluginTargets.cmake  
* QTBUG-113247 Crash when recording wav audio  
* QTBUG-113020 [Regression] Android: declarative-camera example does not  
save picture/picture gets deleted on Qt 6.5  
* QTBUG-115471 FFmpeg video decoding not using hardware accleration.  
* QTBUG-108427 Hardware accelerated video decoding on Windows  
* QTBUG-113256 [macOS] Warnings when connecting/disconnecting AirPods  
* QTBUG-115575 Can not set camera pixel format on MacOS.  
* QTBUG-116393 MediaPlayer freezes if RTSP stream not found  
* QTBUG-115463 QCamera does not support hot plug in and out. Bug or how  
it is designed?  
* QTBUG-116467 [Reg 6.4->6.5] Stopping QCamera when it is not started  
properly causes crash  
* QTBUG-116671 Fix capture_capturesToFile_whenConnectedToMediaRecorder  
on linux CI  
* QTBUG-116075 [Windows] Audio recording starts not at once  
* QTBUG-116836 Android: MediaCodec encoder doesn't accept  
AV_PIX_FMT_MEDIACODEC  
  
### qttools  
* QTBUG-109423 qttools DesignerComponentsPrivate headers are not synced  
* QTBUG-109456 /home/qt/work/qt/qttools/src/qdoc/qmlvisitor.cpp:593:  
undefined reference to `QString  
qualifiedIdToString<QQmlJS::AST::Type*>(QQmlJS::AST::Type*)'  
* QTBUG-109618 QtAttributionsScanner crashes frequently  
* QTBUG-109734 qdoc \include docs example has extra braces  
* QTBUG-109735 \include docs should state snippet marker '//!' must be  
at the beginning on the line  
* QTBUG-110440 Qt Designer: Items just added to scratch pad are not  
visible on Windows  
* QTBUG-109614 QDoc creates truncated temporary header files  
* QTBUG-109316 lupdate produces identical rows  
* QTBUG-110881 REG->6.5.0.B2: Qt Designer crashes when editing resources  
* QTBUG-110930 cross builds: designer examples installed incorrectly  
* QTBUG-110923 qdoc is unnecessarily verbose  
* QTBUG-110142 In qdoc manual, most examples have invalid comment  
start/end  
* QTBUG-111093 [QDoc] Fails for template instantiation with 2 types  
* QTBUG-110630 lconvert do not keep beginning or ending spaces on plural  
form  
* QTBUG-111091 Top-level configure fails unless I have network  
* QTBUG-111391 Fix documentation of \brief command to list all valid  
contexts  
* QTBUG-111603 Qt Designer crash with custom widget plugin derived from  
QMainWindow with no central widget  
* QTBUG-58158 QDoc does not handle `using` declarations  
* QTBUG-111973 qdoc: Something is wrong with qdoc's handling of marked  
code  
* QTBUG-111310 \image tag breaks \value block  
* QTBUG-110781 List new C++ enum values in \sincelist  
* QTBUG-112256 qdoc should warn about documented global functions that  
do not use \relates  
* QTBUG-112220 Assistant starting with inappropriately small window  
* QTBUG-111775 Out-of-bounds string read in lupdate translationAttempt  
* QTBUG-112682 REG->6.5.0: Qt Designer does not handle horizontal  
alignment properties correctly  
* QTBUG-112641 6.5: qdoc crashes generating WebXML for Qt for Python in  
Qt 3D examples page  
* QTBUG-112841 [Possible regression 6.4.x->6.5.0] Cannot add translation  
to project from subdirectory (CMake)  
* QTBUG-70959 qdoc: \keyword sometimes eats up following paragraph  
* PYSIDE-2311 pyside6-lupdate blocks when the input file has no symbols  
in it.  
* QTBUG-113393 QDoc's "Example Manifest Files" page violates our  
Examples Guidelines  
* QTBUG-64506 QDoc section1 does not link in navigation panel when begin  
with non-latin character  
* QTBUG-113585 QDoc's \page command doesn't work with non-latin input  
* QTBUG-28618 qtdbusviewer prints warning "Connecting to deprecated  
signal  
QDBusConnectionInterface::serviceOwnerChanged(QString,QString,QString)"  
* QTBUG-113015 [QDoc] Duplicate QML property name causes confusion:  
qml[attached]property QWindow::Visibility Window::visibility  
* QTBUG-105754 QDoc's \sa command doesn't respect QDoc's //! comments  
* QTBUG-113152 [REG 5.15.8 -> 5.15.9] qt5_create_translation breaks  
projects with multiple same-named ts files  
* QTBUG-113864 \typealias doesn't expand with "This is a type alias for  
[...]"  
* QTBUG-113863 \typealias not highlighted with a clickable link on  
usages  
* QTBUG-107853 qt6_add_translations() deletes CMake-generated *.ts files  
when project is cleaned  
* QTBUG-110949 lupdate: trailing return type with template parameters  
* QTBUG-114151 QML Layout don't have a title  
* QTBUG-112677 Qt lingust, Translation file broken when qsTrId contain <  
* QTBUG-114956 \generatelist <groupname> does not sort the generated  
list  
* PYSIDE-2379 pyside6-lupdate names the context incorrectly when  
indentation detection is offset by oddly indented multiline string or  
similar  
* PYSIDE-2380 pyside6-lupdate ignores r-strings  
* QTBUG-95340 Linguist wrong warning about %n place markers  
* QTBUG-115465 Designer injects bogus "<normaloff>.</normaloff>." for  
icon properties  
* QTBUG-115602 A Minimal qdocconf File incorrect  
* QTBUG-115116 Doc: QObject overview documentation lists incomplete  
signatures of connect  
* QTBUG-116305 Qt Creator 11.0.2  layout alignment disable  
* QTBUG-116412 QDoc automatically adds links to deprecated methods in  
the see also section of docs  
* QTBUG-115958 Two runs of lupdate are required if -pluralonly is used  
for the native language  
* QTBUG-115578 Maybe TS file format documentation needs a correction?  
* QTBUG-116441 qdoc: Pages with multiple \ingroup commands lose  
navigation to parent \group  
* PYSIDE-2191 pyside6-uic fails to correctly generate resource_rc  
location  
* QTBUG-110963 Q Designer: inactive QPalette color values not stored  
correctly  
* QTBUG-110369 AUTOUIC can't handle relative paths referring to parent  
dirs with Ninja Multi-Config  
* QTBUG-113116 Documentation typos, errors and improvements  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-114707 Qdoc ignores the excludedirs config for example files  
list  
* QTBUG-114862 qdbusviewer shows tab for system bus although no system  
bus is present  
* QTBUG-106380 Hello tr() example exits immediately after being run  
* QTBUG-115448 qttools -unity-build-batch-size 100000 fails  
* QTBUG-114967 Issues in documentation of \details command  
* QTBUG-116534 Add \examplecategory to qthelp  
* QTBUG-116536 Add \examplecategory to qtassistant  
* QTBUG-111873 qt_attributions.json files should be valid JSON  
  
### qttranslations  
* QTBUG-111748 [Turkish] Inconsistent translations  
* QTBUG-114406 Update Turkish key label translations  
  
### qtdoc  
* QTBUG-109503 Qt GRPC and Protobuf are not linked correctly from module  
page  
* QTBUG-109324 Clarify the doc page about module changes in Qt6  
* QTBUG-105362 "Building a reusable QML module" refers to non-existent  
CMake code  
* QTBUG-110281 Link to current Apple documentation not archive for  
Info.plist  
* QTBUG-110768 Clean up 'What's new in Qt 6.5'  
* QTBUG-110984 QT_WASM_INITIAL_MEMORY documentation is incorrect  
* QTBUG-110668 wasm: WebSockets don't actually work from other threads  
* QTBUG-110950 WebAssembly websockets not supporting ping  
* QTBUG-110742 "Qt for macOS - Specific Issues": sample code is wrong  
* QTBUG-106682 Typo in the document  
* QTBUG-111271 Typo in the document?  
* QTBUG-111279 Typo in the document?  
* QTBUG-104937 Conflicting android-manifest-file-configuration.html  
files  
* QTBUG-110879 Error while using configure to build  
* QTBUG-85544 androiddeployqt fails with message that neither  
libqtforandroid.so or libqtforandroidGL.so are included  
* QTBUG-97636 Qtbase for Android with examples fails to build  
* QTBUG-83997 Can't deploy a simple console application  
* QTBUG-93185 Android platform plugin not linked when using only QtCore  
* QTBUG-111982 New example demos/documentviewer fails to compile  
* QTBUG-111751 Qt Print Support doesn't support ALL target.  
* QTBUG-111914 Docs:  Cannot configure Q4A kit for armv7 with the value  
given in docs  
* QTBUG-107849 Qt 6.4.0 Purchasing Hangman example does not start  
* QTBUG-112327 Typo in the document?  
* QTBUG-112416 Android docs: Update to correct platform/API version  
* QTBUG-113377 Failed to find required Qt component "PdfWidgets".  
* QTBUG-111586 Update OpenSSL for Android deployment docs for OpenSSL 3  
* QTBUG-113588 Check attribution details for opengl32sw.dll  
* QTBUG-114365 [REG 6.6.0->6.5.1] demos/documentviewer not compiling on  
macOS  
* QTBUG-114210 [REG 6.5.1->6.6.0] demos/photosurface not launching  
* QTBUG-99900 Leading zeroes for Android app "versionCode" are being  
removed  
* QTBUG-114529 ANDROID_NDK_ROOT example has wrong version  
* QTBUG-114370 documentviewer demo causes lots of warnings when building  
on iOS  
* QTBUG-114618 [DocumentViewer] Cannot view any document on macOS  
* QTBUG-114614 [DocumentViewer] Content of PDF file could not be viewed  
on Linux  
* QTBUG-114620 [DocumentViewer] Toolbar icons are not visible on macOS  
* QTBUG-114592 todolist demo fails to configure  
* QTBUG-114759 add_library cannot create target "CustomControls" because  
another target with the same name already exists  
* QTBUG-114615  [DocumentViewer] Edit menu gets multipled each time  
recent document is opened  
* QTBUG-114617 [DocumentViewer] Document specific handlers remain on the  
screen when changing document type  
* QTBUG-115343 Submodule update at 6.5 fails  
* QTBUG-115961 Documentation about building Qt for iOS from source  
requires corrections  
* QTBUG-115988 Doc: Lots of broken links to 'Plug & Paint example'  
* QTBUG-114998 Example can't run, missing module  
* QTBUG-113300 The documentation "How to Create Qt Plugins" seems to  
need a review and update  
* QTBUG-116149 Deploying QML Applications: wrongly instructs to use  
declarative instead of quick  
* QTBUG-116580 "Selected Material Icons" attribution shown twice  
* QTBUG-110921 Documentation for building iOS apps is plain wrong  
* QTBUG-116987 DocumentViewer example broken because QPdfPageSelector is  
no longer a QSpinBox subclass  
* QTBUG-117691 DocumentViewer example does not find plugins at runtime  
* PYSIDE-2191 pyside6-uic fails to correctly generate resource_rc  
location  
* QTBUG-102393 QQmlEngine::retranslate no longer retranslates strings  
coming from C++  
* QTBUG-111061 Windows Versions in Supported Platforms is ambiguous  
* QTBUG-111163 [6.5] Parallel builds failing in Docker container  
* QTBUG-111353 attached ToolTip moves around if its attachee is  
rotated/transformed; should be located near the mouse cursor instead  
* QTBUG-110914 Deprecated Qt.labs.settings do not link to new QtCore  
alternative  
* QTBUG-104930 QLocale shows German text for "en_DE"  
* QTBUG-113116 Documentation typos, errors and improvements  
* QTBUG-113257 Configure qt failed for arm64 architecture  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-110022 Docs missed for ANDROID_MIN_SDK_VERSION and  
ANDROID_TARGET_SDK_VERSION variables  
* QTBUG-114396 Change "OpenGL" to "Graphics API"  
* QTBUG-115108 FX_Material_Showroom fails to compile due to long paths  
* QTBUG-115247 \target after \row generates invalid HTML  
* QTBUG-115958 Two runs of lupdate are required if -pluralonly is used  
for the native language  
* QTBUG-114447 6.5.0 version string found in 6.6.0 sources  
  
### qtlocation  
* QTBUG-100333 MapQuickItem drawn at wrong location after vertical  
resize  
* QTBUG-110701 Holes in GeoPolygons are not rendered  
* QTBUG-110511 Rendering errors in QMapItems (Visible in GeoJSON Viewer  
example)  
* QTBUG-111005 [REG 6.5.0 beta2->beta3] location/mapviewer and places  
not launching  
* QTBUG-112477 configure -no-gui fails in qtlocation  
* QTBUG-115359 QGeoManeuver is exported twice  
* QTBUG-87646 WheelHandler doesn't work correctly with TouchPad  
* QTBUG-112394 Minimal map example - WheelHandler not working  
* QTBUG-112432 wayland plugin should distinguish touchpads from mice,  
etc.  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-114080 QML module documentation should move out of "List of  
types" page  
  
### qtpositioning  
* QTBUG-107584 [iOS] Missing plist/location properties in positioning  
examples  
* QTBUG-109303 Android: single updates for PositionSource and  
SatelliteSource take too long  
* QTBUG-110512 geoflickr example not working  
* QTBUG-110902 tst_qgeoareamonitor execution failed with exit code 3.  
* QTBUG-110931 tst_qgeoareamonitor::multipleThreads randomly hangs on  
macOS ARM  
* QTBUG-114657 [SatelliteInfo] The app stops responding after some time  
on macOS  
* QTBUG-115361 QGeoSatelliteInfo is exported twice  
* QTBUG-106533 Android: jar and src dirs are installed in /usr if  
CMAKE_INSTALL_PREFIX=/usr  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-113752 Warning when assigning to Map.visibleRegion  
* QTBUG-114080 QML module documentation should move out of "List of  
types" page  
* QTBUG-115217 NMEA SatelliteInfo Simulation mode stops providing  
updates  
  
### qtsensors  
* QTBUG-105173 AddressSanitizer: new-delete-type-mismatch in  
tst_QSensor::testReadingBC()  
* QTBUG-113435 dummy plugin gets built by default  
* QTBUG-113651 [REG 6.5.0->6.5.1] sensors/sensorsshowcase not compiling  
on Android  
* QTBUG-106533 Android: jar and src dirs are installed in /usr if  
CMAKE_INSTALL_PREFIX=/usr  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtconnectivity  
* QTBUG-109315 Implicit reconfigure causes error regarding missing  
target PkgConfig::BLUEZ  
* QTBUG-108461 Bluetooth blocks the main thread for a short time  
* QTBUG-106938 Unhandled exception on Android bluetooth  
* QTBUG-111242 sdpscanner strcpy()s sdp_data_t::val::str into a fixed-  
size 1KiB buffer  
* QTBUG-111116 QT BLE scanner example causes high cpu usage  
* QTBUG-112194 Error message with heartrate-game Bluetooth example  
* QTBUG-112303 QBluetoothUuid should offer fromCBUUID  
* QTBUG-112843 [REG 6.5.0->6.5.1] nfc/annotatedurl not compiling on  
Android  
* QTBUG-113318 QBluetoothLocalDevice::pairingStatus always returns  
status unpaired  
* QTBUG-116341 error C2475: 'qbswap': redefinition; 'constexpr'  
specifier mismatch  
* QTBUG-116563 [REG 6.4 -> 6.5] ISO7816 smart cards are considered to be  
NDEF tags  
* QTBUG-106408 Bluetooth Scanner Example has black bars  
* QTBUG-106533 Android: jar and src dirs are installed in /usr if  
CMAKE_INSTALL_PREFIX=/usr  
* QTBUG-103611 [Reg 5.15 -> 6.x] Re-initializing QGuiApplication causes  
QQmlApplicationEngine to crash  
* QTBUG-104754 manual tests that use qt_internal_add_manual_test don't  
run on iOS  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-116580 "Selected Material Icons" attribution shown twice  
  
### qtwayland  
* QTBUG-109302 Segmentation Fault with Wayland and QTreeWidget  
* QTBUG-109051 Crash in multi-screen example when moving window  
* QTBUG-95434 Bitmap cursors not supported on QtWayland  
* QTBUG-111377 QtWayland requests window activation on every focus  
object change  
* QTBUG-111473 Dependency update on qt/qtapplicationmanager is failing  
in 6.5  
* QTBUG-111130 Using a stylus to open a QMenu in a window before  
interacting with it using a mouse or touchpad causes the menu to open as  
a standalone window  
* QTBUG-110420 QtWayland fails to build  
* QTBUG-110623 Constrained menus activate items when cursor is not on  
them  
* QTBUG-87303 Wayland context menus can go off the screen because Qt  
does not do set_constraint_adjustment  
* QTBUG-108645 Focus not updated immediately and lost key press event  
* QTBUG-111423 tst_WaylandCompositor::simpleKeyboard() failed when  
update dependencies  
* QTBUG-110924 doc: Pure-QML example claims to only support one text-  
input protocol  
* QTBUG-102457 Qt may hit failed state if Wayland compositor provides no  
supported shell integrations  
* QTBUG-113022 wrong cmake module name  
* QTBUG-111503 QXkbCommon: No Qt::KeypadModifier in QKeyEvents in  
QtWaylandCompositor  
* QTBUG-113023 missing cmake module import documentation  
* QTBUG-113233 Need a way atomically adjust QWindow minimum and maximum  
sizes  
* QTBUG-113560 CMake error on static qtwayland build  
* QTBUG-97037 DragHandler / startSystemMove window move issue with QT6  
Webengine on Wayland  
* QTBUG-114671 Crash without input device connected  
* QTBUG-114995 tst_qgraphicsanchorlayout crash with QtWayland failed on  
Ubuntu 22.04, GNOME  
* QTBUG-115112 Key injection fails in QML test  
* QTBUG-115691 [FTBFS w/-developer-build]  
QPlatformWindow::setBackingStore(QPlatformBackingStore*) was hidden  
warning  
* QTBUG-97482 Android: QPushButton with QMenu does not work on Qt6  
* QTBUG-116051 QMenuBar doesn't open neighbouring menus on mouseover  
* QTBUG-115757 [REG: 6.5.1-6.5.2] Drag and Drop segfaults programs  
* QTBUG-116344 Segmentation fault on Wayland when enabling drag and drop  
on QListWidget  
* QTBUG-101656 Delayed rescaling when moving from 1x scale monitor to  
higher scale monitor  
* QTBUG-93380 Dialogs partly transparent on Sway/Wayland  
* QTBUG-112808 ERROR: cannot convert 'std::nullptr_t' to 'VkSurfaceKHR'  
{aka 'long long unsigned int'} in assignment  
* QTBUG-112853 Cannot send keys that need modifiers  
* QTBUG-101948 QWaylandWindow::doApplyConfigure called from the wrong  
thread  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-113145 Gesture handlers crash due to misbehaving compositors  
* QTBUG-115101 WaylandGlobalPrivate_sync_headers is not running if  
nothing depends on WaylandGlobalPrivate  
* QTBUG-116340 Add \examplecategory for Qt Wayland Compositor examples  
  
### qt3d  
* QTBUG-59468 Convert sceneparser plugins to load on demand  
* QTBUG-108405 bounding volume results are not checked for validity in  
concurrent calcuation  
* QTBUG-99019 PhongMaterial does not work in GLES2  
* QTBUG-111325 Crash at destruction when running Scene3D in QQuickView  
* QTBUG-110128 Gooch material does not work with Direct3D  
* QTBUG-113589 planets-qml example doesn't build anymore  
* QTBUG-113314 QSkyboxEntity does not render when using the (default)  
RHI backend  
* QTBUG-112739 Qt3DExtras::QSkyboxEntity is broken  
* QTBUG-97751 Crash when loading .obj files with empty lines - out of  
bounds array access in objgeometryloader.cpp  
* QTBUG-100386 Crash in GLTFImporter::commonMaterial  
* QTBUG-116229 Please fix Qt3DCore documentation  
* QTBUG-116354 Qt3D - Enable texture array  
* QTBUG-107693 tst_QResourceManager received signal 11 (SIGSEGV) with  
Ubuntu 22.04 QEMU  
* QTBUG-107694 tst_RayCasting::shouldReturnAllResults fails with Ubuntu  
22.04 QNX  
* QTBUG-111980 [REG 6.5.0 RC->beta3] qt3d/wireframe, lights and pbr-  
materials fails on configure  
* QTBUG-112914 Qt3D/Windows[D3D11]: Crash at destruction  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-116494 Documentation for QCylinderMesh misses Detailed  
Description  
  
### qtimageformats  
* QTBUG-110720 qtimageformats: cmake fails if libwebp is built with  
cmake  
* QTBUG-112947 QImageReader fails to read floating point TIFF images  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtserialbus  
* QTBUG-107141 Typo in the document  
* QTBUG-109940 [REG 6.4.2->6.5/6.0] serialbus modbus examples not  
compiling on iOS  
* QTBUG-114043 QCanDbcFileParser incorrectly parses 29-bit (extended)  
CAN IDs  
* QTBUG-113538 QCanBus not decoding CAN Frames correctly on Mac.  
* QTBUG-114619 QCanDbcFileParser fails to parse non-ASCII characters  
like '°'  
* QTBUG-107137 CMake instruction is not written in the document; grammar  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtserialport  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtwebsockets  
* QTBUG-92858 When connecting to a web socket server via a ngnix proxy  
then it will fail to connect since it is not requesting the  
authentication  
* QTBUG-108996 wasm: Threaded build causes unaligned or out of bounds  
access after calling deleteLater() on a WebSocket  
* QTBUG-110150 QWebSocketProtocol header missing  
* QTBUG-110951 WebAssembly websockets bytes sent is 0 for  
sendTextMessage / sendBinaryMessage  
* QTBUG-111248 wasm: QWebSocket does not disconnect if deleted  
* QTBUG-84315 QUrl::setAuthority() behavior changes  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtwebchannel  
* QTBUG-110795 [Reg? 6.2.7 -> 6.4.2] New warnings in QtWebEngineQuick  
* QTBUG-109677 QtFuture::makeReadyFuture(mutable QList) creates wrong  
future  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtwebengine  
* QTBUG-100417 [REG 5.15->6.3] Multiple context menus can be opened with  
synthetic touch events  
* QTBUG-109357 [REG 5.12 -> 5.15/6.x] QWebEngineUrlRequestInterceptor:  
Multiple redirects crashes the application  
* QTBUG-109243 [REG: 5->6] MouseArea under WebEngineView is getting  
emitting entered/exited signals even though mouse does not enter or  
leave it  
* QTBUG-109348 QtWebEngineView doesn't scroll word document  
* QTBUG-109040 QWebEngineView always prints context  
* QTBUG-110272 webengine tries to use DRI on embedded builds  
* QTBUG-110873 error: ‘QtWebEngineProcess’ was not declared in this  
scope; did you mean ‘QtWebEngineCore’?  
* QTWEBSITE-1083 Possible JS error in WebEngine Markdown Editor Example  
* QTBUG-104869 QWebEngineDownloadItem::totalBytes() always returns -1  
* QTBUG-111574 documentation is wrong for WebEngineCertificateError  
* QTBUG-106072 QtPdf can't open password-protected PDF files on  
Windows/Android  
* QTBUG-111585 REG: GL Errors with WebGL on macOS 13  
* QTBUG-111784 Regression: macOS: Some video do not show pictures after  
WebGL fix  
* QTBUG-106359 QtPDF multipage example should switch to search result  
tab during searching  
* QTBUG-112007 Qt WebEngine 3rd party licensing documentation is  
generated but hidden  
* QTBUG-87275 Incorrect parsing of local urls in qml  
* QTBUG-111939 Dependency update on qt/qtwebengine failed in 6.5.0  
* QTBUG-88482 License terms are missing for Qtpdf  
* QTBUG-111958 opus detection in QtWebEngine still needs perl  
* QTBUG-112282 Support Metal RHI  
* QTBUG-112280 Support Metal and D3D RHI backends  
* QTBUG-111067 Qt PDF Multipage example is crashing on desktop when  
loading pdf files  
* QTBUG-112772 Developer tools open with "screencast" enabled (again)  
* QTBUG-109401 Add DirectX support to QWebEngine  
* QTBUG-111909 QWebEngineView::print margin issues  
* QTBUG-112614 QPdfPageNavigator::backAvailableChanged and  
forwardAvailableChanged are not always emitted for jumps  
* QTBUG-111697 Build failure with GCC 13  
* QTBUG-112700 [REG] [macOS] Using getUserMedia() opens new window's tab  
in Dock  
* QTBUG-113109 [REG 6.4 -> 6.5] WebEngineScripts don't always run on  
pages containing iframes  
* QTBUG-113035 Under the current conditions specified in the  
documentation, it is not possible to build the module through cross-  
compilation  
* QTBUG-113350 FAIL!  :  
tst_QWebEngineGlobalSettings::dnsOverHttps(DnsMode::Secure (real DNS))  
'loadSpy.wait()' returned FALSE  
* QTBUG-112645 QWebEnginePage::WebWindowType not covered by tests  
* QTBUG-112483 Custom scheme handler can not handle content-type with  
value  "text/html ;charset=utf-8"  
* QTBUG-67716 Weird animation on WebView (WebEngine) on macOS when  
dragging pass boundaries  
* QTBUG-112466 libQt6Pdf.so is always built with an embedded copy of  
libpng  
* QTBUG-113400 If QWebEngineProcess is terminated and a JavaScript is  
being run that leads to crash  
* QTBUG-113270 Improve docs with details about the use of GPL components  
from Chromium  
* QTBUG-113524 WebEngine cannot use https after using -sign-for-  
notarization  
* QTBUG-113802 CrossBuilding QtPdf fails because of wrong path to  
qt.toolchain.cmake  
* QTBUG-113579 Clipboard write action doesn't work on 6.5.0  
* QTBUG-114045 error: expected constructor, destructor, or type  
conversion before ‘(’ token QT_FORWARD_DECLARE_CLASS(QThread)  
* QTBUG-113859 [REG 6.4->6.5] Accessibility crash when clicking on a  
link in a list on macOS  
* QTBUG-113806 Chromium attributions missing from 'Licences used in Qt'  
docs  
* QTBUG-114339 FAIL!  : qmltests::WebEngineViewSingleFileUpload::test_ac  
ceptSingleFileSelection(test.txt)  
* QTBUG-113704 Sending certain key events to QQuickView showing a  
focused QtWebEngine causes crash  
* QTBUG-114457 REG [6.5.2 & early 6.6.0 snapshot -> 6.6.0 beta1/FF]  
namespace build fails on linux, Webengine  
* QTBUG-113992 QTWebEngine crash when not working proxy is set  
* QTBUG-113981 QPdfView does not scroll reliably with mouse wheel event  
(two finger sliding on touchpad)  
* QTBUG-63021 add Window 10 compatible manifest to examples  
* QTBUG-113251 [REG 6.4 -> 6.5] Context menu functionality in devtools  
broken  
* QTBUG-103518 QML WebView scrolling events are picked up by DragHandler  
and Flickables behind it  
* QTBUG-115129 Backport Security patches from Chrome 113 to 112-based  
* QTBUG-115033 QtWebEngine uses invalid cmake arguments for file()  
* QTBUG-105053 qtwebengine 6.3.1 fails to link against system nss  
* QTBUG-111225 Host include paths from pkg-config not used when  
FEATURE_webengine_system_icu=On when cross-compiling  
* QTBUG-114939 Qt WebEngine Geolocation broken in 6.6  
* QTBUG-114953 PdfMultiPageView: Very poor memory performance when  
zooming in/out of long documents  
* QTBUG-113512  WebEngineView not visible in Designer on macOS  
* QTBUG-114471 Recipe browser starts in upside down mode  
* QTBUG-114875 Cannot detect Visual Studio when configuring QPdf and  
QWebEngine  
* QTBUG-115690  FAILED:  
qtwebengine/src/core/api/chromium_attributions.qdoc  
* QTBUG-115369 QWebEngine can not render page content and throw `Fatal  
error` in console  
* QTBUG-115713 [REG 6.6.0 beta2->beta3] QtPDF and QtWebengine not  
compiling from sources on MSVC2019  
* QTBUG-115476 QPdfPageSelector doesn't actually handle non-numeric page  
label input  
* QTBUG-115365 QWebEngineCertificateError is exported twice  
* QTBUG-99555 [RE: 6.2.1->6.2.2] macdeployqt fails to produce  
notarizable packages  
* QTBUG-115844 qtwebengine ignores some key remaps  
* QTBUG-115976 Dev tools not hidden with closing cross  
* QTBUG-115703 QtWebEngine 6.6.0 crashes on Windows  
* QTBUG-116278 [REG 6.6.0 beta2-> beta3] QtWebengine not compiling on  
macOS11  
* QTBUG-73994 Changing input method with shortcut key causes hang on  
WebEngine  
* QTBUG-116839 [B2Qt 6.6.0-beta4 snapshot] qtpdf and qtwebgine missing  
from imx8qmmek and jetson-agx-xavier-devkit  
* QTBUG-115722 [REG 6.6.0 beta2->beta3] QtWebengine not compiling from  
sources on SLES15_SP4  
* QTBUG-115753 ERROR: AddressSanitizer: heap-use-after-free  in  
tst_origins  
* QTBUG-116738 qtwebengine Address Sanitizer test run: stack-use-after-  
return in tst_QQuickWebEngineView::savePage(SingleHtmlSaveFormat)  
* QTBUG-116445 [REG][Windows] Crash on  
NativeSkiaOutputDevice::releaseTexture() with nullptr access  
* QTBUG-109235 Review toupper/tolower uses [Qt]  
* QTBUG-107442 The endpoint in QWebEnginePage works only with FCM  
* QTBUG-109179 auto test qwebengineclientcertificatestore fails to build  
* QTBUG-105124 qtwebengine crashes when `/usr/share/X11/xkb` is empty  
* QTBUG-110157 Incorrect command-line parsing if argc=0  
* QTBUG-96010 Issues with lifecycle example  
* QTBUG-110578 tst_QWebEngineView::horizontalScrollbarTest is flaky?  
* QTBUG-110749 Video decoding bug  
* QTBUG-110287 QWebEngineView does not load urls  
* QTBUG-63889 unbundle openjpeg  
* QTWB-67 Add support for changing text alignment  
* QTBUG-110504 Webengine extremely slow in loading webpage in debug  
build  
* QTBUG-111306 tst_MultiPageView::navigation uses fixed positions  
* QTBUG-105988 a11y: Accessible interface can't be retrieved after  
calling QAccessibleEvent::setChild on event created using the  
constructor taking QAccessibleInterface*  
* QTBUG-108154 Saving to MHTML while printing to PDF crashes with  
SIGSEGV  
* QTBUG-111852 Build failure of WebEngine (error when calling  
compress_files.js)  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-113413 LocalContentCanAccessFileUrls setting can prevent  
navigation between local files  
* QTBUG-113485 Navigation asserts when LocalContentCanAccessRemoteUrls  
is false  
* QTBUG-113551 Update documentation for limitation building QtPdf for  
Android with supported  LTS versions  
* QTBUG-114367 QtPdf API review  findings  
* QTBUG-113416 [Reg 6.4->6.5] Static build fails at PDF module  
* QTBUG-105342 Test on qemu are very flacky  
* QTBUG-113369 dark mode enabled causes crashes on specific sites  
* QTBUG-104610 Does WebEngine support document download and print  
operations in the document preview screen?  
* QTBUG-115188 QtWebEngine use after free in Extensions GetPreferences  
* QTBUG-113149 PDF download  from pdf viewer not working  
  
### qtwebview  
* QTBUG-82810 [Android] Deadlock for dynamically loading webview  
* QTBUG-106533 Android: jar and src dirs are installed in /usr if  
CMAKE_INSTALL_PREFIX=/usr  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-114495  FAIL!  : tst_QWebView::load()  
  
### qtcharts  
* QTBUG-107890 When changing the label of a legend marker it will not  
update until something else triggers an update  
* QTBUG-106404 Audio Example doesn't scale properly on android  
* QTBUG-109762 Setting plotArea makes the background to disappear  
* QTBUG-112917 sizeBy method of QScatterSeries is not behaving as  
expected.  
* QTBUG-112904 Scatter points become invisible or are plotted  
incorrectly while size configuration is applied.  
* QTBUG-114408 add_executable cannot create target "gallery" because  
another target with the same name already exists.  
* QTBUG-114221 Charts API Documentation Snippets broken, Examples  
broken.  
* QTBUG-113195 QtCharts/QXYSeries::colorBy method behave incorrectly  
after points are selected in QScatterSeries.  
* QTBUG-114943 Crash in Qt Audio Example on iPhone with Qt Kit 6.2.9 for  
iOS  
* QTBUG-115072 Crash while clicking on scatter points to perform  
selection  
* QTBUG-115977 QML Charts Galleryu example: Charts are hard to read on  
Android  
* QTBUG-116647 Application hangs on calling QXYSeries::sizeBy and  
QXYSeries::colorBy methods for a large number of scatter points.  
* PYSIDE-2179 QtCharts not available in PySide6 qml  
* QTBUG-112919 PointsConfiguration not cleared even when there are no  
points in QScatterSeries  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-94181 error: â€˜defaultInputDeviceâ€™ is not a member of  
â€˜QAudioDeviceInfoâ€™  
* QTBUG-114080 QML module documentation should move out of "List of  
types" page  
* QTBUG-116535 Add \examplecategory to qtcharts (1 update left)  
  
### qtdatavis3d  
* QTBUG-110036 Qml 3d oscilloscope example doesn't fit on screen  
* QTBUG-110042 Qml scatter example text on buttons not readable  
* QTBUG-110040 Qml custom input ui not mobile friendly  
* QTBUG-110041 Qml multigraph example buttons text not readable  
* QTBUG-110043 Qml spectogram example ui elements overlap  
* QTBUG-110037 Qml axis drag example text not readable  
* QTBUG-110038 Qml bars example graph is not centered  
* QTBUG-110044 Qml surface example text on buttons not readable  
* QTBUG-110045 Qml surface layers example controls not usable  
* QTBUG-110358 DrawMode is incorrect in Surface3D if resources are  
bundled  
* QTBUG-112813 Qt6::DataVisualization has a hard dependency on Qt6::Qml  
* QTBUG-112773 FAIL!  : qmltest::Bars3D  
Common::test_3_change_invalid_common() Uncaught exception: Value is null  
and could not be converted to an object  
* QTBUG-114178 Transparency in gradient results in weird stripes  
* QTBUG-114852 tst_qmltest_datavis test is flaky  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtvirtualkeyboard  
* QTBUG-97901 tst_plugin::test_hangulInputMethod(row 24) fails  
* QTBUG-97830 Some Qt Virtual Keyboard tests checking the position of  
selection handles are failing  
* QTBUG-111928 [Reg 6.3.2 -> 6.4.x] Virtual keyboard layout is broken  
* QTBUG-108536 Custom styles are not working  
* QTBUG-111154 [REG Qt 5 → Qt 6] qtvirtualkeyboard is unable to locate  
any custom stylings  
* QTBUG-113168 [VKB] fullScreenMode does not work when enabled with a  
Binding  
* QTBUG-116078 [REG] Behavior breakage in Qt 6.5: Virtual keyboard style  
qrc import path changed  
* QTBUG-108030 Virtual keyboard basic example freezes on Android  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-116432 Virtual keyboard import version number from Qt 5.15 does  
not work in Qt 6.5 version  
  
### qtscxml  
* QTBUG-109235 Review toupper/tolower uses [Qt]  
* QTBUG-110286 SignalTransition::triggered can cause Segfault  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtspeech  
* QTBUG-112607 [MSVC] Qt6 failed to build due to error C2695 on Windows  
x86 mode  
* QTBUG-113805 [Qt TextToSpeech] Resume function restarts the speech  
instead of resume it on Android  
* QTBUG-114099 Qt TextToSpeech landing page is missing 'Licenses and  
Attributions' section  
* QTBUG-115363 QVoice is exported twice  
* QTBUG-113820 Can't run Quick Speech Example on Android  
* QTBUG-106533 Android: jar and src dirs are installed in /usr if  
CMAKE_INSTALL_PREFIX=/usr  
* QTBUG-103611 [Reg 5.15 -> 6.x] Re-initializing QGuiApplication causes  
QQmlApplicationEngine to crash  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtnetworkauth  
* QTBUG-102279 ﻿QOAuth2AuthorizationCodeFlow::requestAccessToken() does  
not report HTTP errors?  
* QTBUG-106821 QOAuth2AuthorizationCodeFlow stuck in RefreshingToken  
state  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtremoteobjects  
* QTBUG-104068 Fix qlalr warning when building qtremoteobjects  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtlottie  
* QTBUG-97259 LottieAnimation start() and stop() not work as expected  
* QTBUG-102550 Bugs with lottie animations  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtquicktimeline  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtquick3d  
* QTBUG-109346 OrbitCameraControlle xSpeed/ySpeed value type incorrect  
in docs  
* QTBUG-109389 Crash if a Node with 2D item is deleted  
* QTBUG-109296 Clean up resources properly on scene manager destruction  
* QTBUG-108826 Quick3D particles model-blend particle example doesn't  
work  
* QTBUG-109564 Handle software backend more gracefully, not by crashing  
(Custominstancing, morphing & particles3d applications stopped  
unexpectedly, colibri-imx6ull)  
* QTBUG-109994 Runtime loader Example crash  
* QDS-8853 Adding Height Field Geometry component to scene in 3D freezes  
3D view  
* QDS-8862 Hidden components come visible after resetting view  
* QTBUG-110593 [REG 6.5.0 beta1->beta2] libassimp.a & libassimp.prl  
missing on Wasm  
* QDS-8865 Issues/emulation layer crash when hiding scene that has  
Quick3DEffect applied  
* QTBUG-110695 SkyBoxCubeMap does not work (regression from 6.4)  
* QTBUG-105318 Sharing material with non-instanced model breaks  
instancing  
* QTBUG-110580 Particles broken when using frustum culling  
* QTBUG-96184 Directional light shadow bounding box too small when using  
model blend particles  
* QTBUG-110870 no matching function for call to min  
* QTBUG-101671 QQuick3DGeometry should support up to 8 morphTargets as  
QtQuick3D build-in Model dose  
* QTBUG-109992 Lights example controls obstruct view  
* QTBUG-111031 DebugView's image asset estimation constantly grows in  
certain scenes  
* QTBUG-111026 sceneeffects example has no .pro  
* QTBUG-110962 CubemapTexture does not work with relative paths  
* QTBUG-107841 tst_Input crashes a lot  
* QTBUG-111135 tst_input crashes  
* QTBUG-110996 Instancing regression in runtimeloader example  
* QTBUG-111338 Material editor broken  
* QTBUG-111000 Global scale value doesn't have any effect on 3D import  
* QTBUG-111357 SCREEN_TEXTURE does not correctly contain the skybox in  
the first frame  
* QTBUG-110891 Zooming doesn't work with Qt Quick 3D  
OrbitCameraController when camera.z = 0  
* QTBUG-110918 Balsam Import Tool Generates Wrong Resource Paths  
* QTBUG-111715 infinite grid documentation has errors  
* QTBUG-110160 Continuous memory growth when the source of Loader 3D{}  
continues to change  
* QTBUG-111276 Poor instanced picking performance  
* QTBUG-111929 QQuick3DLightmapBaker not exported for Design Studio  
* QDS-9507 Lightmapper issues  
* QTBUG-111997 Picking a model with custom geometry with huge numbers of  
vertex  
* QTBUG-112928 FAIL!  : tst_MultiWindow::cubeMultiViewportMultiWindow()  
'comparePixelNormPos(result, 0.5, 0.5, QColor::fromRgb(59, 192, 77),  
FUZZ)' returned FALSE. ()  
* QTBUG-112178 Camera's scale affect the scene  
* QTBUG-112450 Shadows are incorrect when scene has no shadow-casting  
objects  
* QTBUG-110400 [macOS] Qt Quick 3D OrbitCameraController : Zooming is  
not working with native gesture  
* QTBUG-113043 Picking fails with imported scene  
* QDS-9667 Cannot choose lightmap for a model using combobox in  
Properties view  
* QTBUG-112389 FPS counter is not working  
* QTBUG-113044 No callback from QQuick3DLightmapBaker::bake() if there  
are no models set up for baking  
* QTBUG-92944 input problems in DynamicTexture example  
* QTBUG-113987 Typo in the document  
* QTBUG-113986 Typo in the document  
* QTBUG-113985 Data type of aoEnabled seems to be wrong.  
* QTBUG-114557  FAIL!  : tst_RotationDataClass::test_construct()  
Compared values are not the same  
* QTBUG-114313 [Reg: 5.15 -> 6.2/6.5?] QQuaternion::getAxisAndAngle()  
can produce NaN, even when normalized  
* QTBUG-105918 REG: Jittery skeletal animations  
* QTBUG-106371 CMake Build Fails with "Some targets in this export were  
already defined" when using system assimp draco  
* QTBUG-115064 'Some (but not all) targets in this export set were  
already defined' error during building from source process  
* QTBUG-115522 Unshaded CustomMaterial shader does not receive per-  
vertex COLOR attribute from custom QQuick3DGeometry  
* QTBUG-115362 ShaderBuildMessage is exported twice  
* QTBUG-114110 QtQuick3d scene freeze when deleting many nodes  
* QTBUG-116559 Quick3D doesn't compile with -trace lttng  
* QDS-9055 3D import settings for Level of Detail are buggy in the UI  
with Qt 6.5 kit  
* QDS-8963 QtQuick3D types and properties missing in Designer  
* QTBUG-105609 should be able to add a TapHandler to a Button to modify  
behavior  
* QTBUG-111086 QuickBall example button white  
* QTBUG-111013 HorizontalHeaderView with resizableColums true eats input  
when visible (Quick 3D DebugView)  
* QTBUG-111709 FAIL!  : tst_Input::singleTap2D  
* QTBUG-107990 item2D cannot be shared by importScene  
* QDS-9791 Two components named 'Attractor' in QtQuick3D Particles3D  
module components  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-101688 QtQuick3D: Fix compiler warnings for QNX  
* QTBUG-113982 fieldOfViewOrientation property is written twice in the  
PerspectiveCamera's documentation  
* QTBUG-115450 qtquick3d -unity-build-batch-size 100000 fails  
  
### qtshadertools  
* QTBUG-110293 Apps crash on shader compile on INTEGRITY  
* QTBUG-114113 qtshadertools contains two copies of spirv.hpp and  
they're different  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qt5compat  
* QTBUG-105279 qmllint complains about Qt5Compat.GraphicalEffects  
imports  
* QTBUG-109747 Qt5Compat.GraphicalEffects is broken for static builds  
* QTBUG-115467 Qt 6 QML Documentation: Wrong example for  
"verticalOffset"  
* QTBUG-112985 Access to GL_MAX_VARYING_COMPONENTS fails in macOS with  
core profile context  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtcoap  
* QTBUG-115501 [Qt CoAP] CI integrations pass even when the tests fail  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtmqtt  
* QTBUG-111846 MQTT Subscriptions Example Crashes  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtopcua  
* QTBUG-109096 Installed version of OPC UA example cannot compile  
because it relies on the presence of Qt source code  
* QTBUG-110837 error: 'friend' used outside of class  
* QTBUG-109097 OPC UA examples use relative paths and assume in-source  
builds, thus do not work out-of-the-box when loaded in Qt Creator  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-113504 [MSVC] Qt6 failed to build due to error C2362 on Windows  
with option /permissive-  
* QTBUG-116545 QOpcUaClient::connectionSettings getter and setter not  
documented  
  
### qtlanguageserver  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qthttpserver  
* QTBUG-107927 addressbookserver example uses very non standard  
"api_key" header  
* QTBUG-112484 QHttpServer: use function pointer as ViewHandler  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtquick3dphysics  
* QTBUG-108897 QFATAL : tst_physicsscene::UnknownTestFunc() ASSERT  
* QTBUG-110258 CharacterController doesn't trigger TriggerBody  
* QTBUG-110723 DynamicRigidBody axis lock properties have int type  
instead of enum  
* QTBUG-112819 Capsule geometry has invalid geometry bounds  
* QTBUG-111870 CharacterController: changing height or diameter is not  
working  
* QTBUG-111565 CharacterController does not receive Contact Reports  
* QTBUG-113597 ERROR building: Timeout after 15m0s: No output received  
* QTBUG-114111 Crash when destroying a body with scale  
* QTBUG-114183 Collision shape calculates orientation incorrectly when  
parent has scale  
* QTBUG-115539 Missing dependencies in qmldir  
* QTBUG-114114 PhysX has ODR violations  
* QTBUG-112846 Shadow artifacts  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtgrpc  
* QTBUG-109372 Updating qt/qt5 with a consistent set of submodules in  
dev failed  
* QTBUG-109016 .gitignore file present in qtgrpc  
* QTBUG-110704 WASM build broken on 6.5 (missing Qt6::qtprotobufgen)  
* QTBUG-111140 cross-compilation failures for qtgrpc  
* QTBUG-109130 Enable qtprotobufgen testing for Mac OS arm on CI  
* QTBUG-111318 [REG 6.5.0 beta2->6.5.0 beta3] qtgrpcgen.exe and  
qtprotobufgen.exe not present  
* QTBUG-111983 New examples grpc/magic8ball and chat not compiling on  
iOS or Android  
* QTBUG-112754 The qtprotobuf and qtgrpc example documentation doesn't  
link to the .proto files in the list of the example sources  
* QTBUG-113342 QtProtobufQtTypesQtCoreTest::qDateTime(LocalTime) fails  
* QTBUG-112421 QtProtobuf:  
Required.Proto3.ProtobufInput.RepeatedScalarMessageMerge.ProtobufOutput  
conformance test is failing  
* QTBUG-112422 QtProtobuf: Required.Proto3.ProtobufInput.ValidDataOneof.  
MESSAGE.Merge.ProtobufOutput conformance test is failing  
* QTBUG-112429 QtProtobuf: Recommended.Proto3.ProtobufInput.ValidDataOne  
ofBinary.MESSAGE.Merge.ProtobufOutput  
* QTBUG-113409 Yocto build fails for qtgrpc module  
* QTBUG-114237 undefined symbol: QGrpcChannelOptions::metadata() const  
* QTBUG-114409 FAIL!  : tst_qtprotobufgen::cmakeGeneratedFile(nopackage_  
protobuftyperegistrations.cpp) 'generatedFile.exists()' returned FALSE.  
()  
* QTBUG-114799 QtProtobuf::Any::fromMessage() does not compile  
* QTBUG-114816 serialization/deserialization of Any fails  
* QTBUG-114972 using google/protobuf/timestamp.proto fails to compile  
* QTBUG-115032 -platform linux-clang-libc++ fails to compile  
qtprotobufgen  
* QTBUG-115055 Qt6Grpc package depends on system WrapgRPC to be found  
and be compatible  
* QTBUG-110107 RTA CMake test fails on 6.5.0  
* QTBUG-115280 Docs should cover the server side even if it is not  
provided with Qt gRPC  
* QTBUG-114077 Package sub-folders generation doesn't work with QML  
argument  
* QTBUG-115499 moc: The metatypes.json file is generated with ambiguous  
"inputFile" records.  
* QTBUG-115057 when using qtgrpc, .proto files should appear in project  
hierarchy  
* QTBUG-115693 Boot2Qt / Yocto build fails for qtgrpc in CI  
* QTBUG-115582 Protobuf WellKnownTypes is missing in WASM builds  
* QTBUG-115175 QtProtobuf nested message generation error  
* QTBUG-116043 configure fails with "PROTO_FILES list is empty"  
* QTBUG-116160 GENERATE_PACKAGE_SUBFOLDERS and QML don't mix  
* QTBUG-116463 qt_add_protobuf() broken in 6.6.0-beta3 for VS2019 build  
system  
* QTBUG-116461 qt_add_protobuf() broken in 6.6.0-beta3 for WASM  
* QTBUG-115708 windows build failure when using protobuf  
GENERATE_PACKAGE_SUBFOLDERS  
* QTBUG-116679 -feature-protobuf-wellknowntypes not working for WASM  
* QTBUG-109503 Qt GRPC and Protobuf are not linked correctly from module  
page  
* QTBUG-111098 QtGRPC:  
QtGrpcClientTest::CallAndRecieveStringTest(Http2Client) fails with RHEL  
8.6  
* QTBUG-111485 failed to set dynamic section sizes: bad value  
* QTBUG-112762 QMetaProperty::write detaches value argument  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-114988 Duplicated message names of nested messages lead to QML  
warning  
* QTBUG-115180 QtProtobuf: Enum forward declaration is required  
  
### qtquickeffectmaker  
* QTBUG-109591 EffectMaker not finding default source images  
* QTBUG-109852 Image elements are created also for empty image  
properties  
* QTBUG-110047 Sometimes images exporting fails  
* QTBUG-110054 Issues with QQEM Thunder node  
* QTBUG-110945 AddNodeDialog not clipping/scrolling  
* QTBUG-111342 Fix QQEM with the updated Qt Controls material style  
* QTBUG-113021 Black areas in Water node  
* QTBUG-108171 ScrollBar with sections is jumpy  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-113531 EffectMaker not find resources on macOS  
* QTBUG-114561 Material style highlighted & flat button shows no text  
  
### qtapplicationmanager (Commercial only)  
* QTBUG-113297 Link is dead in the document  
* QTBUG-113501 error: no matching function for call to  
‘FunctorPrototype(<unresolved overloaded function type>)’  
* QTBUG-113423 "applicationAdded" signal needs update in the  
documentation  
* QTBUG-113302 Warning in the documentation is unclear in what it's  
talking about  
* QTBUG-113293 "names" is not documented about manifest  
* QTBUG-113291 Typo in the document and missing link in each section  
* QTBUG-113292 The link is dead in the document  
* QTBUG-113296 CMake solution is not written in the Container  
documentation  
* QTBUG-114355 Many qmllint warnings for Application Manager QML types  
* QTBUG-114356 AppMan: IntentServerHandler is not registered correctly  
* QTBUG-114755 AppMan: IntentModel cannot be compiled  
* QTBUG-116081 FAIL!  : appman-  
qmltestrunner::WindowMapping::test_amwin_advanced() property count  
* QTBUG-116627 FAIL!  : appman-  
qmltestrunner::BubbleWrap::test_bubblewrap() 'wait for signal  
windowAdded' returned FALSE.  
* QTBUG-109756 FAIL!  : tst_Signature::crossPlatform()  
's.verify(sigWinCrypt, m_verifyingPEM)' returned FALSE. (Failed to  
verify signature: error:10800069:PKCS7 routines::signature failure)  
* QTBUG-107886 Custom runtimes cannot be registered  
* QTBUG-113620 Errors in AppMan NotificationManager docs  
* QTBUG-105067 Different behavior in single- vs. multi-process mode  
* QTBUG-108855 Focus on click doesn't work in single-process mode  
  
### qtinterfaceframework (Commercial only)  
* QTBUG-109936 FAILED: qtinterfaceframework/src/tools/ifcodegen/.stamp-  
deploy_virtualenv  
* QTBUG-110298 Dependency update on qt/qtinterfaceframework is failing  
in dev  
* QTBUG-108640 [REG 6.4.1->6.5.0] interfaceframework\qface-  
tutorial\ch1-basics and ch2-enums-structs fails on configure  
* QTBUG-112684 GENERATED property is not set for the files generated by  
ifcodegen  
* QTBUG-110675 Qface-tutorial example not working  
* QTBUG-110674 Qface-climate example crash  
* QTBUG-110677 Window-qml example doesn't fit properly on screen  
* QTBUG-110678 Climate-qml example doesn't fit on screen  
* QTBUG-113429 Link is dead in the document  
* QTBUG-113431 Typo in the document  
* QTBUG-113430 Typo in the document  
* QTBUG-113459 Document error in Qt Interface Framework tutorial  
* QTBUG-114686 Locale Problem in Compiled Ifcodegen on M1  
* QTBUG-114940 Setting an env override for a simulationFile also affects  
the discoveryMode  
* QTBUG-115600 FAIL!  : BackendsTest::testInit(simulation-backend)  
* QTBUG-116662 Qt Interface Framework Generator doesn't work with cross-  
compiling kits  
* QTBUG-111898 Dependency update on qt/qtinterfaceframework is failing  
in dev  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
  
### qtvncserver (Commercial only)  
* QTBUG-109563 Qt VNC Server: Many files does not appear to contain a  
license header  
* QTBUG-110031 error: ‘qAsConst’ was not declared in this scope  
* QTBUG-108462 Share overlay through VncItem  
* QTBUG-110398 Mouse wheel does not work with VNC Server  
* QTBUG-113545 vncserver static build fails with libtomcrypt  
* QTBUG-108514 change the default port of the Qt VNC Server to 5901  
  
### qmlcompilerplus (Commercial only)  
* QTBUG-116741 Dependency update on qt/tqtc-qmlcompilerplus is failing  
in 6.6  
* QTBUG-106929 Qml Singletons do not work on Android  
* QTBUG-109221 Inconsistencies regarding list and value type property  
manipulations  
* QTBUG-111340 stdlib precondition violation in qmlcachegen  
* QTBUG-104508 qmlcachegen fails to compile PhotoCaptureControls.qml in  
multimedia  
* QTBUG-112480 QmlCompiler does not care about shadowing of methods  
  
### qtinsighttracker (Commercial only)  
* QTBUG-113766 [Insight Tracker] Click event without the category is not  
tracked  
* QTWEBSITE-1110 Missing redirects for Qt Insight Tracker documentation  
* QTBUG-116699 Data base cannot be opened in the subsequent launches  
* QTBUG-115601 FAIL!  : tst_QInsightEventFilter::trackEvents(text.ui)  
The computed value is expected to be greater than or equal to the  
baseline, but is not  
  
Known Issues  
------------  
  
* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-6.6/supported-platforms.html  
* RTA reported issues from Qt 6.6  
https://bugreports.qt.io/issues/?filter=25128  
* See Qt 6.6  known issues from:  
https://wiki.qt.io/Qt_6.6_Known_Issues  
* Qt 6.6.0 Open issues in Jira:  
https://bugreports.qt.io/issues/?filter=25286  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Amir Masoud Abdol  
Chris Adams  
Laszlo Agocs  
Yigit Akcay  
Anu Aliyas  
Martin Andersson  
Dimitrios Apostolou  
Albert Astals Cid  
YAMAMOTO Atsushi  
Xavier BESSON  
Andreas Bacher  
Mahmoud Badri  
Mate Barany  
Sebastian Beckmann  
Rolf Eike Beer  
Vladimir Belyavsky  
Nicholas Bennett  
Alex Blasche  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
Mikolaj Boc  
Tatiana Borisova  
Joerg Bornemann  
Jörg Bornemann  
Rym Bouabid  
Assam Boudjelthia  
Aurélien Brooke  
Kai Uwe Broulik  
Michael Brüning  
Igor Bugaev  
Andreas Buhr  
Andrey Butirsky  
Olivier De Cannière  
John Chadwick  
Mike Chen  
Wang Chuan  
Creapermann  
Alexandru Croitor  
Mitch Curtis  
Thibaut Cuvelier  
Giuseppe D'Angelo  
Pranta Dastider  
Szabolcs David  
Noah Davis  
Oliver Dawes  
James DeLisle  
Marius Dege  
Cédric Le Dillau  
Pavel Dubsky  
Artem Dyomin  
Alexey Edelev  
David Edmundson  
Oliver Eftevaag  
Christian Ehrlicher  
Iikka Eklund  
Hatem ElKharashy  
Andreas Eliasson  
Ahmed Essam  
Fabio Falsini  
David Faure  
Ilya Fedin  
Wang Fei  
Nicolas Fella  
Ben Fletcher  
Simo Fält  
Samuel Gaist  
Zoltan Gera  
Frederik Gladhorn  
Joshua Goins  
Julian Greilich  
Robert Griebl  
Mikko Gronoff  
Henning Gruendl  
Jan Grulich  
Kaj Grönholm  
Christoph Grüninger  
Richard Moe Gustavsen  
Lucie Gérard  
Ralf Habacker  
Tang Haixiang  
Kamil Hajdukiewicz  
Heikki Halmet  
Amanda Hamblin-Trué  
Jøger Hansegård  
Inkamari Harjula  
Andre Hartmann  
Thomas Hartmann  
Andreas Hartmetz  
Elias Hautala  
Jani Heikkinen  
Tero Heikkinen  
Miikka Heikkinen  
Christian Heimlich  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Dominik Holland  
Mats Honkamaa  
Jimi Huotari  
Sam James  
Martin Jansa  
Johnny Jazeix  
Allan Sandfeld Jensen  
Tim Jenssen  
Tim Jenßen  
Janne Juntunen  
Maurice Kalinowski  
Jonas Karlsson  
Johannes Kauffmann  
Timothée Keller  
Ali Kianian  
Marius Kittler  
Michael Klein  
Friedemann Kleint  
André Klitzing  
Michal Klocek  
Lars Knoll  
Seokha Ko  
Jarek Kobus  
Tobias Koenig  
Sze Howe Koh  
Jarkko Koivikko  
Antti Kokko  
Tomi Korpipaa  
Tomi Korpipää  
Jani Korteniemi  
Janne Koskinen  
Fabian Kosmale  
Volker Krause  
Mike Krus  
Konrad Kujawa  
Santhosh Kumar  
Sona Kurazyan  
Jonas Kvinge  
Kai Köhne  
Lauri Laanmets  
Inho Lee  
Jaehak Lee  
Paul Lemire  
Kimmo Leppälä  
Kimmo Leppälä  
Wladimir Leuschner  
Thorbjørn Lindeijer  
Robert Löhning  
Thiago Macieira  
Kuntal Majumder  
Olaf Mandel  
Christophe Marin  
Marco Martin  
Thorbjørn Lund Martsum  
Aaron McCarthy  
Terry Meacham  
Frank Meerkötter  
Ievgenii Meshcheriakov  
Lisandro Damián Nicanor Pérez Meyer  
Leena Miettinen  
Piotr Mikolajczyk  
Vladimir Minenko  
Phan Quang Minh  
Samuel Mira  
Jan Moeller  
Hamish Moffatt  
Safiyyah Moosa  
Bartlomiej Moskal  
Marc Mutz  
Tommi Mänttäri  
Antti Määttä  
Martin Negyokru  
Andy Nichols  
Mårten Nordheim  
Dennis Oberst  
Johannes Oikarinen  
Kimmo Ollila  
Fredrik Orderud  
Matti Paaso  
Roland Pallai  
Bumjoon Park  
Kwanghyo Park  
Ari Parkkila  
Shreya Pattani  
Pasi Petäjäjärvi  
Samuli Piippo  
Timur Pocheptsov  
Milla Pohjanheimo  
Joni Poikelin  
Aleix Pol  
Cajus Pollmeier  
Rami Potinkara  
Lorn Potter  
Shyamnath Premnadh  
MohammadHossein Qanbari  
Liang Qi  
Khem Raj  
Matthias Rauter  
David Redondo  
Arno Rehn  
Topi Reinio  
Hannah von Reth  
Christian Riggenbach  
Alexey Rochev  
Mario Roessel  
David Rosca  
Bernhard Rosenkränzer  
Shawn Rutledge  
Emir SARI  
Toni Saario  
Casimir Saastamoinen  
Sharad Sahu  
Ahmad Samir  
Philip Schuchardt  
David Schulz  
Carl Schwan  
Björn Schäpers  
L. E. Segovia  
Thomas Senyk  
Luca Di Sera  
Dmitry Shachnev  
Sami Shalayel  
Andy Shaw  
Venugopal Shivashankar  
Harald Sitter  
Kristoffer Skau  
David Skoland  
Daniel Smith  
Colin Snover  
Ivan Solovev  
Axel Spoerl  
Piotr Srebrny  
Brett Stottlemyer  
Christian Strømme  
Fab Stz  
Tarja Sundqvist  
Lars Sutterud  
Tasuku Suzuki  
Jan Arve Sæther  
Morten Sørvig  
Benjamin Terrier  
Samuel Thibault  
Henrik Thillman  
Ivan Tkachenko  
Orkun Tokdemir  
Pino Toscano  
Jens Trillmann  
Jere Tuliniemi  
Paul Olav Tvete  
Sami Varanka  
Peter Varga  
BogDan Vatra  
Doris Verria  
Tor Arne Vestbø  
Jannis Voelker  
Ville Voutilainen  
Juha Vuolle  
Jaishree Vyas  
Michael Weghorn  
Bernd Weimer  
Edward Welbourne  
Nicolas Werner  
Paul Wicking  
Piotr Wierciński  
Oliver Wolff  
Li Xinwei  
Jannis Xiong  
Lu YaNing  
Andrey Yaromenok  
Semih Yavuz  
Vlad Zahorodnii  
Sharaf Zaman  
Thomas Zander  
JiDe Zhang  
Leon Zhang  
Yuhang Zhao  
Shengfeng Zhou  
Eike Ziller  
hjk  
Fredrik Ålund  
Andrius Štikonas  
