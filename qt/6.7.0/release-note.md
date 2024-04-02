Release note  
============  

Qt 6.7 introduces many new features and improvements as well as bugfixes  
over the 6.6.x series. For more details, refer to the online  
documentation included in this distribution. The documentation is also  
available online:  
  
https://doc.qt.io/qt-6/index.html  
  
The Qt version 6.7 series is binary compatible with the 6.6.x series.  
Applications compiled for 6.6 will continue to run with 6.7.  
  
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
  
### qtbase  
* 6ab0d25a09 QPixmapCache: fix leaking of QStrings and Keys on clear()  
Fixed QString key data not being freed on clear().  
  
* 211b54ea47 Add flag to hide eye dropper button from QColorDialog  
Added a NoEyeDropperButton option to hide the eye dropper button.  
  
* aa481854a9 QUrl: Add QUrl::fromEncoded(QByteArrayView) overload  
Added QUrl::fromEncoded(QByteArrayView) overload.  
  
* 90e3f0bd73 Freetype: Don't do image transform for translations  
Fixed an issue where setting a translation matrix on text using a  
bitmap font would cause rendering artifacts.  
  
* 48841c34d2 CMake: Unify CMAKE_BUILD_TYPE behavior on all platforms  
When no explicit build type is specified, Windows will now default to  
building Release like the other platforms.  
  
* f341f75c8c Align QKeySequence behavior between macOS and iOS  
Keyboard shortcuts now follow the same scheme as on macOS, with their  
native representation expressed via the ⌘, ⌥, and ⌃ modifiers. Use  
Qt::AA_MacDontSwapCtrlAndMeta to override this.  
  
* 78cdd9a64d QPixmapCache: deprecate replace()  
The `replace(key, pixmap)` function has been deprecated, because  
passing a `const Key` to it results in undefined behavior. Use  
`remove(key, pixmap)` followed by `key = insert(pixmap)` instead.  
  
* 90bc0ad41f QProcess/Unix: add failChildProcessModifier()  
Added failChildProcessModifier().  
  
* dcf7604230 QVariant::value/qvariant_cast: add rvalue optimization  
Added rvalue QVariant overloads of qvariant_cast<T>() and  
QVariant::value<T>().  
  
* 9195438a5f Fix no-op emission of QComboBox::currentTextChanged  
emit currentTextChanged only, if currentText changes.  
  
* 72d660843b QCoreApplication: port processEvents() to QDeadlineTimer  
Added processEvents() overload that takes a QDeadlineTimer.  
  
* f7792d2b6d Schannel: Add support for proper listing of ciphers  
Add support for listing supported ciphers with Schannel backend.  
  
* f4dca7c512 Consult QIcon::fallbackThemeName() even for themes with  
explicit parents  
QIcon::fallbackThemeName() will now be used as fallback even for themes  
that declare a parent theme.  
  
* dde45bcefb Consult QIcon::fallbackSearchPaths() even when theme name  
is empty  
QIcon::fallbackSearchPaths() will now be consulted for fallback icons  
even if the current theme name is empty.  
  
* e603661c48 QIcon::fromTheme(): Always consult "hicolor" theme last  
The 'hicolor' theme will now always be prioritized last when looking up  
fallback themes, even if explicitly declared as a theme parent in a  
theme.  
  
* 7fa3267fda QPixmapCache: Move qHash(Key) from _p.h to public header  
Made the qHash() overload for QPixmapCache::Key public (was: private)  
API.  
  
* e8dcbaaaf6 QFutureSynchronizer: fix aliasing problem in setFuture()  
Fixed a crash in setFuture() if the argument was already a member of  
QFutureSynchronizer::futures().  
  
* 39882a1354 Set color scheme after handling theme change in windows  
Update colorScheme property after palette change.  
  
* 38cd3cb126 Short live Q_NODISCARD_(CTOR_)X!  
.  
  
* 842cfcec80 QObject: introduce QT_NO_CONTEXTLESS_CONNECT  
Added the QT_NO_CONTEXTLESS_CONNECT macro. Defining the macro before  
including any Qt header will disable the overload of QObject::connect  
that does not take a receiver/context argument.  
  
* 3ec24e329c SSL: upgrade the default DH parameters  
The default Diffie-Hellman parameters are now using the 2048-bit MODP  
group from RFC 3526.  
  
* b3f27f75b6 Introduce -no-vcpkg flag for disabling vcpkg  
detection/integration  
vcpkg detection, and integration can be disabled by passing the -no-  
vcpkg flag to the configure command, or by passing `-DQT_USE_VCPKG=OFF`  
to the cmake command.  
  
* a8cf976ce6 Introduce QT_SYNC_HEADERS_AT_CONFIGURE_TIME flag  
When building Qt from sources, syncqt and Qt header files are now  
created at build time, not configure time. This should speed up the  
configuration step. You can set the CMake variable  
QT_CONFIGURE_TIME_SYNC_HEADERS to ON to use the previous behavior,  
though. The old behavior is also preserved if cmake/configure is run  
from inside an IDE - Qt Creator, Visual Studio Code, and CLion are  
currently detected.  
  
* 574a47dd5a QGtk3Theme: Do not default Active WindowText to button  
foreground  
Default to GTK Entry Text / Normal Text / qt_fusionPalette  
  
* c580a7b0fa QTest: add qSleep(std::chrono::milliseconds) overload  
Added qSleep(std::chrono::milliseconds) overload.  
  
* 57712e1160 QTest: add qWait(chrono::milliseconds) overload  
Added qWait(chrono::milliseconds) overload.  
  
* fa296ee1dc QTest: add QDeadlineTimer qWaitFor() overload  
Added QDeadlineTimer qWaitFor() overload.  
  
* 4f618bde08 QEventLoop: port processEvents() to QDeadlineTimer  
Added a processEvents() overload that takes a QDeadlineTimer.  
  
* e84dc809e2 Say hello to QtVFS for SQLite3  
QtVFS for SQLite3 allows to open databases using QFile. This way it can  
open databases from RW locations such as android shared storage, or even  
from read-only resources e.g. qrc or android assets.  
  
* 79abdd3cd4 QPixmapCache: ignore insertion or searches with empty key  
Trying to insert or find a pixmap with an empty key string now always  
fails immediately.  
  
* 8aa0d71d06 Update bundled libpng to version 1.6.40  
libpng was updated to version 1.6.40  
  
* 3748b194d4 QEventLoopLocker: defend against nullptr arguments  
Is now a no-op on nullptr QEventLoop*, QThread*,  
QCoreApplication::instance() (was: crash).  
  
* ee736717d3 CMake: Don't use VCPKG_DEFAULT_TRIPLET for triplet  
deduction  
Qt no longer uses the VCPKG_DEFAULT_TRIPLET environment variable to  
deduce target triplet. By default we let vcpkg's toolchain file  
automatically deduce the triplet to use. The new QT_VCPKG_TARGET_TRIPLET  
environment variable can be used instead, or pass  
-DVCPKG_TARGET_TRIPLET=<triplet> to CMake.  
  
* af32768f18 QDebug: add getter/setter for noQuotes  
Added setQuoteStrings()/quoteStrings() to access and manipulate the  
quote()/noquote() state.  
  
* b2b5862479 QAnyStringView: add QDebug stream operator  
Can now stream QAnyStringView into QDebug.  
  
* d8a8a3a5dc QEventLoopLocker: inline Private into public class  
No longer allocates; all operations are noexcept now.  
  
* c2956f8f76 QEventLoopLocker: add move SMFs and swap()  
Added move special-member-functions and swap().  
  
* 4b7b5edf26 SQL/SQLite: add case folding for non-ascii characters  
Add new option QSQLITE_ENABLE_NON_ASCII_CASE_FOLDING for correct case  
folding of non-ascii characters.  
  
* 1ca71cbff0 QLibrary: make isLoaded() report whether this object has  
load()ed  
QLibrary::isLoaded() now reports whether this instance of QLibrary has  
succeeded in loading the library, via direct or indirect call to load().  
Previously, it used to reported whether the actual library was loaded by  
any QLibrary instance.  
  
* 70fc6b4581 Disable vcpkg detection/integration by default  
Vcpkg detection/integration is now disabled by default, and it can be  
enabled by either passing `-vcpkg` to the configure script, or by  
passing `-DQT_USE_VCPKG=ON` to cmake.  
  
* 929d9a4ca5 Allow OpenGL to be found on X11-less Linux systems (using  
libOpenGL)  
Allow OpenGL to be found on X11-less Linux systems (using libOpenGL)  
  
* 96d67da420 String-like containers: add implicit conversions towards  
std:: string views  
Added an implicit conversion operator towards std::string_view.  
  
* ecab68989e QCborValue: fix memleak on Array to Map coercion  
Fixed a memory leak when an array was coerced into a map.  
  
* 676087ef1f QSslDiffieHellmanParameters: fix mem-leak  
Fixed a memory leak in parsing of PEM-encoded Diffie-Hellman  
parameters.  
  
* e532933a2a SQL/PSQL: Handle jsonb operators in prepared queries  
Add setEnablePositionalBinding() to be able to disable positional  
binding.  
  
* a1451bbb57 QEventDispatcherUNIX: convert "eventfd" feature to proper  
QT_CONFIG  
Qt no longer sets the QT_NO_EVENTFD feature macro on systems without  
eventfd.  
  
* a7f227f56c Make qYieldCpu() public API  
Added qYieldCpu() function.  
  
* 674134f08d Consider BUILD_SHARED_LIBS when adding libraries using  
_qt_internal_add_library  
qt6_add_library now considers the value of the BUILD_SHARED_LIBS  
variable. If the variable is DEFINED it has higher priority than the  
library type detecting logic in qt6_add_library when adding the library  
targets.  
  
* ed7c7a1458 iOS: Implement QPlatformWindow::setMask() for masking  
rendering and input  
QWindow::setMask() is now supported for masking the rendering and touch  
input of child windows.  
  
* 3498baef76 Update bundled libjpeg-turbo to version 3.0.0  
libjpeg-turbo was updated to version 3.0.0  
  
* 297fe90329 Allow to override build date with SOURCE_DATE_EPOCH  
Allows to override _DATE_ with SOURCE_DATE_EPOCH to make builds  
reproducible.  
  
* 14d1108d35 Deprecate Q_ASSUME()  
attribute.  
  
* 91e70f239e Give QLocale::uiLanguages() a separator parameter  
QLocale::uiLanguages() now lets the caller choose what separator to use  
between the tags that make up each locale-identifier in the list  
returned.  
  
* 15cfdab514 Give QLocale's name() and bcp47Name() separator parameters  
QLocale's name() and bcp47Name() now let the caller chose what  
separator to use between the tags making up the name, where there is  
more than one.  
  
* 17f2b6d2e9 QDeadlineTimer: make the (Qt::TimerType) ctor explicit  
The QDeadlineTimer(Qt::TimerType) constructor is no longer implicit. To  
keep old source working, wrap the Qt::TimerType argument in  
QDeadlineTimer{}. This is backwards-compatible with older Qt versions.  
  
* 2f87711913 SQL: add missing Q_DECLARE_SHARED to the value types  
QSqlField and QSqlRecord are now relocatable types.  
  
* f081578ce0 QSqlIndex: implement member swap() and use a macro for  
move-assignment  
QSqlIndex is now a relocatable type.  
  
* a7d2855b3c invokeMethod: enable passing parameters to overload taking  
functors  
Added support for passing parameters to the overload of  
QMetaObject::invokeMethod that takes a functor. These new overloads must  
have the return-value passed through qReturnArg().  
  
* 828acefc8a Rename Qt::Key_mu to Qt::Key_micro  
Qt::Key_mu is now renamed Key_micro, since it is, in fact, the micro  
sign, not the Greek letter mu. The old name is retained as an alias for  
the time being.  
  
* dd3840a1a2 QGuiApplication: Report default platform name before  
initialization  
QGuiApplication::platformName now reports the default platform name if  
QGuiApplication hasn't been instantiated yet. It used to return an empty  
string.  
  
* 0f41819196 Android: use all nameFilters at once for native file dialog  
use all nameFilters at once since Android file picker can't change  
nameFilters after being opened.  
  
* 49e52e8dd6 SQLite: Update SQLite to v3.43.0  
Updated SQLite to v3.43.0  
  
* fcb548878b CMake/Network: limit the testing for some network iface  
features  
The QT_NO_GETIFADDRS and QT_NO_IPV6IFNAME macros are deprecated. On a  
standard Linux build, they will be defined to 1, even if the system does  
support getifaddrs() and ifnametoindex().  
  
* 946f15efb7 CMake/ELF: hide all Standard Library symbols  
On ELF-based platforms (e.g., Linux, FreeBSD), the linking process has  
been updated to exclude Standard Library symbols from getting the "Qt_6"  
ELF version. This solves the problem of applications and libraries  
breaking arbitrarily after Qt updates, but will cause such breakages  
right now. Content built with older versions of Qt may need to be  
relinked.  
  
* 3652cdf6c7 Update bundled zlib to version 1.3  
zlib was updated to version 1.3.  
  
* 5a96d13bb5 QCheckBox: add new checkStateChanged(Qt::CheckState) signal  
Added new checkStateChanged(Qt::CheckState) signal, obsoleting  
stateChanged(int).  
  
* 65e04162d1 CMake: Recompute features when dependent features are  
marked dirty  
The build system will now try to recompute configure features when  
dependent feature values are toggled by the user.  
  
* 55f0738f16 Add StateLocation & GenericStateLocation to  
StandardLocation  
Added StateLocation & GenericStateLocation to StandardLocation  
  
* d83aabad0f Add static constexpr Boyer-Moore Latin-1 string matcher  
Added QStaticLatin1StringMatcher, which can be used to create a static  
constexpr string matcher for Latin-1 content.  
  
* 6da6a17de9 Fix qHash(qfloat16) to match Qt 6.4 behavior  
Fixed qHash(qfloat16) which was broken from 6.5.0 to 6.5.3, inclusive.  
If you compiled against one of the affected Qt versions, you need to  
recompile against either Qt 6.4 or earlier or 6.5.4 or later, because  
the problematic code is inline.  
  
* 454636afec Document q(u)int128 and QT_SUPPORTS_INT128  
Added qint128 and quint128 typedefs on platforms that support them.  
  
* b2aeac9891 QTextFormat: Allow merging unset properties  
QTextFormat now allows setting properties to an invalid QVariant to  
allow clearing properties via a merge. This changes behavior slightly  
where code iterating over a QTextFormats properties would never  
encounter invalid variants, which is now possible if setProperty with an  
invalid variant was used instead of using the clearProperty function to  
remove properties.  
  
* 16433a4a6e Long live Q_(U)INT128_C()!  
Added Q_INT128_C() and Q_UINT128_C() macros to create qint128 and  
quint128 literals in a platform-independent way.  
  
* 9fe47cf2e1 Fix crash when reading corrupt font data  
Fixed a possible crash that could happen when loading corrupted font  
data.  
  
* 9c0def81e4 Warn on failure to construct valid system time zone object  
If systemTimeZone() is unable to identify a valid system time zone, it  
now produces a warning the first time it encounters the problem.  
  
* 2fd4a86dc5 QDataStream: prevent accidental streaming of pointers  
Streaming of arbitrary pointers using QDataStream has been disabled.  
Note that such streaming happened through the streaming operator for  
bool.  
  
* 4583d808ea SQLite: Update SQLite to v3.43.1  
Updated SQLite to v3.43.1  
  
* 6f5136ef66 QMessageBox::about / aboutQt - use native modal dialog on  
iOS  
QMessageBox::about(Qt) now shows native, modal dialog.  
  
* 0f19cafc3c [docs] Fix \since for qHash(qfloat16)  
Delete the old entry for qHash(qfloat16), keep the one from this  
commit.  
  
* fe182c1541 CMake: Add I18N_LANGUAGES keyword to  
qt_standard_project_setup  
Added variable QT_I18N_LANGUAGES to specify the languages that are used  
for i18n in the project.  
  
* 4a6cbfbe5c QVariant: add fromMetaType  
Added the QVariant::fromMetaType named constructor, that builds a  
QVariant of a given QMetaType.  
  
* 13f673939d Fix renamed and duplicated namespaces in QXmlStreamWriter  
Fix renamed and duplicated namespaces in QXmlStreamWriter.  
  
* 5469d6a6cc Support loading variable fonts as application fonts in  
Freetype  
Added support for selecting named instances in variable application  
fonts when using the Freetype backend.  
  
* 2496882ea7 a11y: No longer mark QAccessibleSelectionInterface as  
preliminary  
The QAccessibleSelectionInterface that was added as preliminary in Qt  
6.5 is no longer preliminary. Exposing selection to assistive technology  
can be achieved by implementing this interface.  
  
* ff6eca0087 CMake: Add I18N_NATIVE_LANGUAGE keyword to  
qt_standard_project_setup  
Added variable QT_I18N_NATIVE_LANGUAGE to specify the native language  
that is used in the source code for translatable strings.  
  
* 6c90aa029b QDockWidget: ignore close event if DockWidgetClosable is  
not set  
A floating dockwidget that doesn't have the DockWidgetClosable feature  
flag set can no longer be closed by a call to QWidget::close or a  
corresponding keyboard shortcut (such as Alt+F4).  
  
* 42d2944191 Add coverage and coverage-gcov features  
Added the coverage configuration argument. The only supported coverage  
tool at the moment is gcov. The argument requires Qt is built in Debug  
otherwise setting the argument leads to the configuration error. Typical  
usage:   <...>/configure -developer-build -coverage gcov  
  
* aa19704bbc Un-deprecate qSwap()  
Un-deprecated qSwap().  
  
* bfe62b0224 Remove framework-related functionality from syncqt  
'-framework' and '-frameworkIncludeDir' arguments were removed. The  
related logic is moved to cmake scripts.  
  
* 9349e463d4 Use the actual target name as base name for android  
deployment settings  
The target name is used as a base name of android deployment settings,  
but not the OUTPUT_NAME property.  
  
* ad692a1fbb Doc: update future direction of QCoreApplication::notify()  
In Qt 7, QCoreApplication::notify() will not be called for events being  
delivered to objects outside the main thread. The reason for that is  
that the main application object may begin destruction while those  
threads are still delivering events, which is undefined behavior.  
Applications that currently override notify() and use that function  
outside the main thread are advised to find other solutions in the mean  
time.  
  
* 016addc201 QString: assign() [4/4]: (it,it) overload for UTF-8 data  
types  
Enabled assign() for UTF-8 data types.  
  
* 9800c63533 revert "xkbcommon: make shortcuts persistent across  
layouts"  
A change in 6.6.0 that resulted in keyboard shortcuts not respecting  
the user's active layout has been reverted.  
  
* 500be123f4 Support variable applications fonts with DirectWrite  
Added support for selecting named instances in variable application  
fonts when using the DirectWrite backend.  
  
* b6c7335635 QPointer: fix missing converting move-assignment operator  
Added missing converting move-assignment operator. This is forwards-  
compatible with Qt 6.6.0: compiling against 6.6.0 will just use the  
lvalue overload.  
  
* 0fa4af060e QTemporaryFile: Add support for std::filesystem::path  
Added support for passing std::filesystem::path to rename and  
createNativeFile.  
  
* ebf1538fa6 Qt::mightBeRichText: port to QAnyStringView  
Ported Qt::mightBeRichText() to QAnyStringView (was: QString).  
  
* 6b363556b8 QByteArray: Remove unnecessary <stdarg.h> header  
The header qbytearray.h no longer includes the header stdarg.h.  
  
* ffe8932ef3 Make systemTimeZone() and systemTimeZoneId() consistent  
When unable to determine the IANA ID of the system's local time zone,  
QTimeZone::systemTimeZoneId() now returns empty instead of the "UTC" it  
formerly, and misleadingly, returned. Passing the return to the  
QTimeZone constructor now consistently produces the same as calling  
QTimeZone::systemTimeZone(), whose id() now matches the return from  
QTimeZone::systemTimeZoneId(). This is independent of whether  
QTimeZone::systemTimeZone() is valid.  
  
* a20a6ae7ea cmake: simplify exceptions handling code  
Qt explicitly pass -fexceptions now on non-MSVC toolchains, if exception  
handling is not disabled in CMake configure.  
  
* 4aba97e062 Adjust msecs instead of offset for spring-forward  
resolution times  
When QDateTime is instantiated for a combination of date and time that  
was skipped, by local time or a time-zone, for example during a spring-  
forward DST transition, the invalid result's time() - and, in rare  
cases, date() - no longer match what was asked for. Instead, these  
values and offsetFromUtc() now match the point in time identified by  
toMSecsSinceEpoch().  
  
* 3b6d288e3b Android: Simplify Qt for Android hierarchy, less Java  
reflection!  
Simplify Qt for Android public bindings (QActivity, QtService and  
QtApplication) by implementing base classes which use the delegate  
implementions directly and avoid reflection.  
  
* 05888490db QSet: de-pessimize binary operators  
The binary operators &, |, + and - are now hidden friends, and chaining  
them has been made a lot more efficient.  
  
* f2c2242c74 SQLite: Update SQLite to v3.43.2  
Updated SQLite to v3.43.2  
  
* 381d6210c2 qevent.h: don't include <QPointer>, fwd-declare it  
The headers qevent.h and qfuture.h no longer include the header  
qpointer.h.  
  
* a49ccc08c3 QDateTime: disambiguate times in a zone transition  
Added a TransitionResolution parameter to various QDateTime methods to  
enable the caller to indicate, when the indicated datetime falls in a  
time-zone transition, which side of the transition to fall or whether to  
produce an invalid result.  
  
* 1e7fa7dbe8 androiddeployqt: Copy templates and stdcpp lib in auxillary  
mode  
Now the auxillary mode of androiddeployqt also copies the templates  
and the stdcpp lib file without building the APK.  
  
* 071291a0d4 Update bundled libjpeg-turbo to version 3.0.1  
libjpeg-turbo was updated to version 3.0.1  
  
* a6ad755734 QStringList: add filter(QStringMatcher) overload  
Added filter(const QStringMatcher &) overload, which may be faster for  
large lists and/or lists with very long strings.  
  
* 3dffd5aa0b QStringList: add indexOf() QString/QStringView/QL1SV  
overloads  
Added indexOf() overloads that take  
QString/QStringView/QLatin1StringView, and a Qt::CaseSensitivity  
parameter. Prior to this using QStringList::indexOf() called the methods  
inherited from the base class.  
  
* c205f05128 QStringList: add filter(QL1SV) overload  
Added filter(QLatin1StringView) overload, which is more optimized when  
searching for a Latin-1 string literal as no conversion to QString is  
necessary.  
  
* f2e19d37de QStringList: add lastIndexOf() overloads  
Added lastIndexOf() overloads that take a  
QString/QStringView/QLatin1StringView and a Qt::CaseSenitivity  
parameters. Prior to this calling lastIndexOf() would call the methods  
inherited from the base class. This change is source compatible and  
existing code should continue to work.  
  
* bb23a05905 QWeakPointer: deprecate its relational operators  
The (in)equality operators of QWeakPointer have been deprecated. Always  
upgrade a QWeakPointer to a QSharedPointer (for instance, via lock())  
before doing a comparison.  
  
* 51cfc973b3 Add a QDateTimeEdit::timeZone property  
Added timeZone property to enable a datetime edit widget to control the  
timezone used. This makes the timeSpec property redundant; this old  
property shall be deprecated from 6.10.  
  
* 6a93ec2435 QAtomic: remove the copy ctor and assignment operator  
The copy constructor and assignment operators of Qt atomic classes  
(QAtomicInteger, QAtomicPointer) have been removed. Their usage in user  
code should be considered a programming error, as no memory ordering  
semantics were ever documented for these operations (and therefore  
relying on any specific semantic would be relying on undocumented,  
unportable behavior). This matches the API of the std::atomic class in  
C++. Note that you can still use explicit load/store operations to  
transfer a value across two Qt atomic objects, and therefore use the  
memory ordering specified for the load/store operations.  
  
* fd9c567156 Use SSL_CTX_set_dh_auto if DHparam is empty  
An empty Diffie-Hellmann parameter enables auto selection of openssl  
backend.  
  
* 358745d7de QSP/QWP: introduce owner_before, owner_equal, owner_hash  
Added owner_before, owner_equal, owner_hash.  
  
* 935562a77b QTemporaryFile(Name): don't make the path absolute on  
generation  
This class will now return relative file paths in fileName() if the  
file template was also a relative path (it used to always return an  
absolute path). The temporary files are still created in the same  
directory; this change only affects the length of the path the function  
returns.  
  
* 58fd829cdf Use localized time-zone abbreviations or offset  
When a datetime format includes the timezone (or offset), the  
appropriately localised form is (to the extent the timezone backend in  
use supports this) used where, previously, a haphazard choice of system  
and C locale was used. This applies to both serialization and parsing.  
  
* 4ecbe42ff4 QMetaObject: add indexOfEnumerator(QBAV) overload  
Added indexOfEnumerator(QByteArrayView) overload. And deprecated  
indexOfEnumerator(const char *) overload.  
  
* 65d58e6c41 Introduce new empty Windows 11 style  
Renaming of QWindowsVistaStylePlugin to QModernWindowsStylePlugin  
  
* c27baa6aac Update menu behavior to mimick Windows 11 style on  
QWindows11Style  
On Windows 11, hovered menu and menuitems are now highlighted with  
darker rounded rect.  
  
* 56bb4ac484 qnetworkrequest, qnetworkreply: port some methods to QBAV  
Ported hasRawHeader and rawHeader of QNetworkReply and QNetworkRequest  
to QByteArrayView.  
  
* ce4531a490 QNetworkInfo: if no builtin defaults are found, load  
anything  
QNetworkInformation::defaultBackend() will now load any available  
backend with Reachability support if the default ones are not available.  
If none are available it will create a backend that always returns the  
default values for each property.  
  
* d53c0d721f Windeployqt: add options to deploy/block plugins  
Windeployqt now has options that allow for custom plugin deployment.  
Users can include or exclude them, either individually, or by type.  
  
* 4fad57e750 QStringView: add isLower and isUpper  
Added isLower() and isUpper()  
  
* df73672f97 QTimeZone(qint32 offsetSeconds): use IANA ID when one is  
available  
one which would omit trailing :00 for minutes or seconds, which the  
IANA ID may well include.  
  
* c63a21ae5c SQLite: Update SQLite to v3.44.0  
Updated SQLite to v3.44.0  
  
* 8753bb3045 Cocoa MessageBox: don't use native message box if detailed  
text is set  
On Apple platforms, the native message box is no longer used when  
detailed text is set.  
  
* 54656da9ac QMimeDatabase: handle buggy type definitions with circular  
inheritance  
Added code to detect and break circular inheritance loops in the MIME  
data, which were causing infinite loops  
  
* 3c9017b0e2 iOS: Use 160x160 as default normal window size, like on  
other platforms  
The default normalGeometry() of a window is now 160x160, instead of  
following the screen geometry. Top level windows are still maximized by  
default, as before.  
  
* bdd41f491c Rename Q*Ordering to Qt::*_ordering  
Added Qt::{partial,weak,strong}_ordering as drop-in C++17 stand-ins for  
C++20's std::{partial,weak,strong}_ordering.  
  
* e608bc0192 QObject: port findChild/ren() to QAnyStringView  
Ported QObject::findChild/ren() and their helper functions to  
QAnyStringView.  
  
* 2dc0c01449 configure: Make sure the configure script exits with  
cmake's exit code  
The configure script on UNIX systems will now exit with the same exit  
code that the underlying cmake process exited with.  
  
* b7657ddccb qDebug: add support for std::optional and std::nullopt_t  
Added support for std::optional and std::nullopt_t  
  
* bf946e8e3b QObject: allow calling findChild() without a name  
Added findChild() overload taking no name.  
  
* 11d8200249 SQLite: Update SQLite to v3.44.1  
Updated SQLite to v3.44.1  
  
* d201c0a218 OpenSSL: remove support for 1.1  
Support for OpenSSL 1.1 has been dropped. Qt now only supports OpenSSL  
3.  
  
* 8e8815b688 QCborStreamReader: fix API mistake: lastError() wasn't  
const  
Fixed lastError() not being declared as a const member.  
  
* 8af346c1f6 QCborStreamReader: add toString() and toByteArray()  
Added toString() and toByteArray(), which read a full string whether it  
is chunked or not. They also guard against attempting to allocate more  
memory than the underlying stream could provide.  
  
* 9590ed6ba6 macOS: Implement QPlatformServiceColorPicker via  
NSColorSampler  
Non native color dialogs now use native color picking when picking  
colors from the screen.  
  
* 8220173b02 SQLite: Update SQLite to v3.44.2  
Updated SQLite to v3.44.2  
  
* 25d1db424e QUtf8StringView: make data() constexpr  
data() is now constexpr, too.  
  
* 5f775e6719 Fix QStringConverter::encodingForName() for trailing `-`,  
`_`  
Fixed a bug where encodingForName() failed due to trailing characters  
(`_`, `-`) that ought to have been ignored.  
  
* ff7d69dafd Refuse to relocate non-copy/move-constructible types  
No longer allows marking as Q_RELOCATABLE_TYPE a type that is neither  
movable nor copyable.  
  
* 8988c92b98 QIcon: fall back to QPA engine if themes don't provide the  
icon  
If neither theme nor fallback theme provide the requested icon, we fall  
back to the QPA plugin implementation. On platforms where an  
implementation exists, this will override the explicitly provided  
fallback (second parameter to QIcon::fromTheme).  
  
* 9bbfdd6844 QIcon: turn platform engines on by default  
Qt now has implementations of native icon engines for macOS, iOS,  
Windows 10, Windows 11, and Android. These engines provide access to the  
native icon libraries and fonts, mapping standard icons to the  
corresponding native icon asset. Icons from application-defined themes  
take precedence, but the last-resort fallback icon passed as the second  
parameter into the QIcon::fromTheme(QString, QIcon) overload is only  
used if the icon is not available from the native library. See the QIcon  
documentation for details.  
  
* a0c9fc6758 CMake: Add a way to pass additional arguments to  
win/macdeployqt  
Added the DEPLOY_TOOL_OPTIONS argument to the functions  
qt_generate_deploy_app_script and qt_deploy_runtime_dependencies.  
  
* 3d231e27a8 Long live qCompareThreeWay()  
Added qCompareThreeWay() as a public API for three-way comparison.  
  
* ccd0dc7f6d QPartialOrdering: add lower-case flags for std/Qt::  
compatibility  
Added a set of lower-case flags (::less, ::greater, etc) to improve  
source-compatibility with {Qt,std}::partial_ordering.  
  
* c39fff0da5 Add missing <=> 0 operator to Qt ordering types  
Added three-way comparison operator (<=>) against literal zero,  
available when compiling in C++20 mode.  
  
* 03e78e5d62 Long live QSpan as public API!  
New Qt equivalent of std::span.  
  
* db991cb4e1 QBitArray: replace the member operator~ with a hidden  
friend  
The bitwise AND, OR, XOR, and NOT operator functions on QBitArray are  
now hidden friends. This may cause source-incompatibility in unusual  
coding styles (like 'array.operator~()') or with classes that have a  
casting 'operator QBitArray()'.  
  
* 4fa9f13397 Make QAtomicScopedValueRollback public API  
New class.  
  
* e240f559e4 QUrlQuery: drop the qpair.h include  
qurlquery.h no longer includes qpair.h (for qMakePair).  
  
* b8fac53803 Add QCalendar::matchCenturyToWeekday()  
Added a matchCenturyToWeekday() method for use when resolving dates  
given day, month and last two digits of the year, along with day of the  
week. Any custom calendar backend plugins shall need a recompile and  
may, optionally, implement the new virtual method behind this.  
  
* 41f84f3ddb Give the caller control over the century used for two-digit  
dates  
When fromString() has only a two-digit year to go on, it is now  
possible to set the start-year of the century within which this selects.  
  
* 925ce9e908 Add QHttpHeaders class  
New QHttpHeaders class  
  
* f587ba1036 QNetworkRequestFactory convenience class  
Added a new convenience class to help with the needs of repeating  
network request details imposed by the server-side service endpoints,  
which is common with RESTful applications.  
  
* e560adef21 Add REST client convenience wrappers  
Added new convenience classes QRestAccessManager and QRestReply for  
typical RESTful client application usage  
  
* 090991123d Support for std::chrono as transferTimeout type  
Add std::chrono support for transfer timeout.  
  
* 706dafe347 Make some QScreen native interfaces public  
The QAndroidScreen, QWaylandScreen and QWaylandWindow native interfaces  
are now available on QScreen to provide a handle to the underlying  
platform screen.  
  
* 68898f6fa0 Use Ctrl+Shift+S for Save As... shortcut on every platform  
Ctrl+Shift+S is now the standard shortcut for Save As... on every  
platform.  
  
* 377066e407 Fix return value of qbswap(qint128)  
Fixed return type of qbswap(qint128) (was: quint128).  
  
* 5419df55f3 Use Qt::WindowNoState for child windows/widgets shown via  
show()  
Child windows and widgets are now always shown in their normal state by  
show().  
  
* d62b4d84c1 CMake: Add QT_DEPLOY_LIBEXEC_DIR  
Added the deployment variable QT_DEPLOY_LIBEXEC_DIR.  
  
* e4697acbc8 CMake: Add LIBEXEC_DIR argument to  
qt_deploy_runtime_dependencies  
The qt_deploy_runtime_dependencies function gained the LIBEXEC_DIR  
argument to set the directory for deploying helper executables on Unix  
derivatives.  
  
* 3b3960c9b4 QWidget: deliver DragLeave events symmetrically  
DragLeave events are now always sent to the widget the mouse is  
leaving, even if it didn't accept the DragEnter event.  
  
* 2b18f6c7b8 Fix Maximized frameless window painting wrong with  
WS_THICKFRAME  
Adding a check for the maximized state of the window during the  
calculation of margins. Margins calculation will not be skipped for  
maximized windows.  
  
* c6219ebfb5 QWindowContainer: Don't embed a QWidget  
If createWindowContainer() is called with a QWidgetWindow argument,  
return pointer to the widget instead of new container.  
  
* 253957b940 Add parent arg to QFileDialog::getOpenFileContent and  
saveFileContent  
Adds an overload to the static methods getOpenFileContent and  
saveFileContent with a new parent argument which always no-ops in the  
WASM environment.  
  
* 4bc230ad05 SQL: rename enablePositionalBinding() to  
setPositionalBindingEnabled()  
Add setPositionalBindingEnabled() to be able to disable positional  
binding.  
  
* 2634ad2e6c QShader: add move constructor, move-assignment operator and  
swap  
Added move constructor, move-assignment operator and swap member  
function.  
  
* 1f3f99f673 Don't include windows.h in the public qopengl.h header  
On Windows, the public qopengl.h header no longer includes windows.h.  
  
* 6224c3b0dc SQLite: Update SQLite to v3.45.0  
Updated SQLite to v3.45.0  
  
* 8902ed8f89 QUuid: Fix Id128Bytes alignment on some architectures  
The QUuid::Id128Bytes type had a loose definition that could cause it  
be passed incompatibly between functions, in some architectures,  
depending on whether GNU extensions were allowed. This is now fixed, but  
may cause code compiled with Qt 6.6.0 and 6.6.1 to fail when recompiled  
with 6.6.2 or later.  
  
* 02ba4b14dc QCheckBox: deprecate stateChanged()  
stateChanged(int) has been deprecated in favor of  
checkStateChanged(Qt:CheckState).  
  
* 4f1752a6b9 Increase precision for QGraphicsView::AnchorUnderMouse  
Increase precision for QGraphicsView::AnchorUnderMouse and  
QGraphicsView::centerOn  
  
* b9bcaae226 SQL/MySQL: Fix compilation with MySQL 8.3  
Fixed compilation with MySQL 8.3.  
  
* a3b4b060cf QHostInfo: fix lookupHost() signature immediately  
The lookupHost() static function now takes const QObject* receivers  
(was: (non-const) QObject*).  
  
* 6a5b47ecac QSsl: QMetaObject is defined in qobjectdefs.h  
The enums in namespace QSsl are now Q_ENUMs.  
  
* f14f12c2e1 QObject: Let moveToThread return succcess state  
QObject::moveToThread() now returns a boolean success state.  
  
* af9bf8712e Update Zlib to 1.3.1  
zlib was updated to version 1.3.1.  
  
* 5b2f352042 windows: Avoid infinite recursion with certain fonts  
Fixed an issue where an infinite recursion could occur if the system  
had a font with multiple preferred names in non-English languages.  
  
* 55b2011bcd Fix clipped text when combining multiple writing systems  
Fixed an issue where drawing text from different writing systems in the  
same line and including a background could cause parts of the text to be  
clipped.  
  
* 73cf291849 Doc: Update Copyright in md4c license text  
Updated md4c (optional part of Qt Gui) to version 0.5.1.  
  
* 036e9811d2 Update public suffix list  
Updated the public suffix list to upstream SHA  
883ced078a83f9d79a98933145425c221a5e51f0.  
  
* f477c78577 QDialogButtonBox: Fix focus chain and default button  
assignment  
Default button becomes focus proxy of a QDialogButtonBox. This ensures  
that Enter triggers the default button, instead of the first button in  
the layout.  
  
* 327dcc078d QPainterPath: Fix boundingRect and controlPointRect  
ignoring start point  
boundingRect() and controlPointRect() now use the start point from  
QPainterPath(const QPointF &startPoint).  
  
* 3d182679b4 QBitArray: avoid overflow in size-to-storage calculations  
Fixed a bug with QBitArrays whose size() came within 7 of the  
size_type's maximum.  
  
* 1b90474986 Support the named instances of Variable Fonts  
Added support for the named instances from the variable fonts.  
  
* 03bf71b7ff Update bundled libpng to version 1.6.41  
libpng was updated to version 1.6.41  
  
* d61a333705 QBitArray: fix potential truncation in QDataStream op>>()  
Fixed undetected overflows in the deserialisation (opertor>>()) from  
QDataStream.  
  
* 2c53d990f7 SQLite: Update SQLite to v3.45.1  
Updated SQLite to v3.45.1  
  
* ff8928d3cb Update md4c to 0.5.2  
md4c was updated to 0.5.2.  
  
* 7fa10ab76e QMovie non-anim: use QImageReader::imageCount but not  
nextImageDelay  
QMovie now handles non-animated multi-frame image formats (such as  
tiff): QImageIOHandler::imageCount() is observed, and the default frame  
rate is 1 FPS.  
  
* 41c786781a Update QLocale and calendar data to CLDR v44.1  
Updated QLocale's data extracted from the Unicode Common Locale Data  
Repository (CLDR) to v44.1. The license changed to Unicode License V3.  
  
* 27625a33c5 Update bundled libjpeg-turbo to version 3.0.2  
libjpeg-turbo was updated to version 3.0.2  
  
* c2400042ba Update Valgrind to version 3.22.0  
Updated Valgrind header used by QtTest. The change only affects  
portability of s390 inline assembler.  
  
* cd59980f72 Update bundled libpng to version 1.6.42  
libpng was updated to version 1.6.42  
  
* 2cf327be82 CMake: Fix undefined symbol: qt_resourceFeatureZstd issue  
Targets created with qt_add_executable and qt_add_library will now add  
the --no-zstd option to AUTORCC_OPTIONS when the target platform does  
not support zstd decompression. You can opt out via the  
QT_NO_AUTORCC_ZSTD cmake variable.  
  
* 0985c707a9 QBitArray: don't create invalid Qt 5 streams  
Now refuses to stream a QBitArray with size() > INT_MAX to a  
Qt-5-compatible QDataStream.  
  
* e69a151573 QBitArray: use QDataStream::SizeLimitExeeded where  
applicable  
Uses new QDataStream::Status::SizeLimitExceeded now, where applicable  
(was: WriteFailed, ReadCorruptData).  
  
* 737dbc8c78 WASM builds now handle bitmap and pixmap cursors  
Previously, bitmap and pixmap cursors were nonfunctional in wasm builds  
and would trigger warnings.  These cursors now work as expected.  
  
* 2cfe7199a2 QGtk3Theme: Fix QGtk3Interface::fileIcon  
Fixed file icons provided by QFileIconProvider when using the gtk3  
platform theme.  
  
* 18d15404cb PCRE2: upgrade to 10.43  
PCRE2 was updated to version 10.43.  
  
* 93f8c8f3e6 wasm: make opengles3 (webgl2) default surface format  
Default OpenGL ES version raised to 3.0  
  
* 5403bfedc8 RHI: fix Vulkan layout for PreserveDepthStencilContents  
depth textures  
QRhiTextureRenderTarget::PreserveDepthStencilContents now works  
properly on Vulkan  
  
* 03514d8f2c SQL/SQLite: handle option SQLITE_OPEN_NOFOLLOW  
Add new option QSQLITE_OPEN_NOFOLLOW to expose open mode  
SQLITE_OPEN_NOFOLLOW.  
  
* 3bbe5641b0 QString: document isSimpleText() removal  
Removed undocumented internal, yet public, isSimpleText() member  
function. If you still use it, you'll have to write your own version  
outside of QString.  
  
* 33336ef2ee QNetworkInformation: document a potential SiC  
The enums in QNetworkInformation must now be scoped when used from QML.  
The scope is no longer optional. Adding the scope is a backwards-  
compatible fix.  
  
* 2f50deafbf Revert "Fix export of QDeferredDeleteEvent, should be  
Q_CORE_EXPORT"  
Made this undocumented class private and unexported. You will still be  
able to see the definition in qcoreevent_p.h, but you won't be able to  
create objects of the class anymore.  
  
* 9d791aabad Update bundled libpng to version 1.6.43  
libpng was updated to version 1.6.43  
  
* 9888d8ee22 SQLite: Update SQLite to v3.45.2  
Updated SQLite to v3.45.2  
  
### qtsvg  
* b7ca594 Fix crash when reading text with line breaks  
Fixed a regression where the application would crash on certain SVG  
files.  
  
* 33f3425 QSvgWidget: only start the animation timer when visible  
Add animationEnabled property to QSvgRenderer, and use it from  
QSvgWidget to stop animations when hidden.  
  
* 534d072 Add symbol and marker to QSvg  
Added <symbol> and <marker> to the supported elements of QtSvg.  
  
* e4b4153 Add filter attribute/element and various filter primitives  
Added support for the <filter> element to QtSvg. The most important but  
not all filter primitves are supported: feMerge, feColorMatrix,  
feGaussianBlur, feOffset, feComposite, feFlood.  
  
### qtdeclarative  
* b7813fc5ea Make some properties in the effects module FINAL  
Properties for the type MultiEffect are now FINAL, meaning they can no  
longer be shadowed by declaring new properties with the same names in  
QML. A warning will be printed out to the console, when a FINAL property  
is being shadowed. We recommend that users rename those properties to  
avoid potential unexpected behavior changes.  
  
* e31821795e Make some properties in Qt Quick Shapes FINAL  
Properties for types in the Qt Quick Shapes module are now FINAL,  
meaning they can no longer be shadowed by declaring new properties with  
the same names in QML. A warning will be printed out to the console,  
when a FINAL property is being shadowed. We recommend that users rename  
those properties to avoid potential unexpected behavior changes.  
  
* b949315427 Make properties in Qt Quick Layouts FINAL  
Properties for types in the Qt Quick Layouts module are now FINAL,  
meaning they can no longer be shadowed by declaring new properties with  
the same names in QML. A warning will be printed out to the console,  
when a FINAL property is being shadowed. We recommend that users rename  
those properties to avoid potential unexpected behavior changes.  
  
* cb82b9f2ad Make properties in the particles module FINAL  
Properties for types in the Qt Quick Particles module are now FINAL,  
meaning they can no longer be shadowed by declaring new properties with  
the same names in QML. A warning will be printed out to the console,  
when a FINAL property is being shadowed. We recommend that users rename  
those properties to avoid potential unexpected behavior changes.  
  
* 351979e05a Make properties in Qt Quick FINAL to prevent shadowing  
Most properties for types in the QtQuick module are now FINAL, meaning  
that they can no longer be shadowed by declaring new properties with the  
same names. With few exceptions. A warning will be printed out to the  
console, when a FINAL property is shadowed. We recommend that users  
rename those properties to avoid potential unexpected behavior changes.  
  
* b1766d9d62 Flickable: Proportional wheel scrolling if deceleration is  
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
  
* 7d426b6226 Introduce sourceSize parameter to Canvas::loadImage()  
Optional size parameter added to Canvas::loadImage(). Useful to improve  
visual quality by rendering scalable formats like SVG closer to the  
intended display size.  
  
* 9355b7173c QML models: Make most properties FINAL to prevent  
accidental shadowing  
Most properties for types in the QtQml.Models module are now FINAL,  
meaning that they can no longer be shadowed by declaring new properties  
with the same names. A warning will be printed out to the console, when  
a FINAL property is shadowed. We recommend that users rename those  
properties to avoid potential unexpected behavior changes.  
  
* eed2ee69ac Fix memory leak when invalidating NativeRendering fonts  
Fixed a controlled memory leak with Text.NativeRendering where loading  
and unloading the same application fonts could cause memory usage to  
increase indefinitely and not be regained until the window was closed.  
  
* 13dc5b3c9d qmlls: fix the order in which the build directory is  
obtained  
Qmlls warns when inexisting build folder paths are passed to the  
--build-dir argument or the QMLLS_BUILD_DIRS environment variable. Also,  
it will inform the user if the build directory was set using the command  
line option, the environment variable or an .qmlls.ini settings file, if  
existent in the source folder.  
  
* 2e44d316c8 Add flag to hide eye dropper button from qml ColorDialog  
Added a NoEyeDropperButton option to hide the eye dropper button  
  
* b4cf8c1f1a QML: Revert the default for enforcing function signatures  
Type annotations on function signatures are now enforced, no matter if  
the code in question is interpreted, JIT-compiled, or AOT-compiled.  
Previously, only AOT-compiled code enforced the signatures. Therefore  
you could produce divergent behavior by passing or returning values that  
violated the type annotations.  
  
* b9bfdea0e2 QML: Un-specialcase QStringList and QVariantList conversion  
Converting a QVariantList to a QJSValue via, for example  
QJSEngine::toScriptValue() does not produce a JavaScript array anymore,  
but rather a better suited sequence object that behaves almost like a  
JavaScript array. The only difference is that its QJSValue::isArray()  
will return false now.  
  
* 3e619367b1 StackView: add strongly-typed push functions  
Added strongly-typed pushItem and pushItems functions. These can be  
compiled to C++ by the QML Compiler.  
  
* 7d0ec8910f StackView: add strongly-typed pop functions  
Added strongly-typed popToItem popToIndex, and popCurrentItem  
functions. These can be compiled to C++ by the QML Compiler.  
  
* 1baa7fc3e7 StackView: add strongly-typed replace functions  
Added strongly-typed replaceCurrentItem functions. These can be  
compiled to C++ by the QML Compiler.  
  
* 514fa7e284 Remove redundant warning  
Assigning null to a property of incompatible type is now an error  
instead of a warning.  
  
* 115916f217 qmlformat: fix formatting of object destructuring  
qmlformat will no longer add "" characters automatically in the object  
keys unless the object key is actually a string literal. Also, using a  
scoped variable as the property key will no longer result in the  
duplication of the property name.  
  
* 62014e9cec Remove bounding behavior of popup for negative margins  
The popup default margins (-1) earlier was constrained on left and top  
edges, but allowed to move beyond right and bottom edges. The behavior  
changed now to relax this constraint and move beyond all edges. Also to  
be noted, edge constraints has been relaxed only for Popup and controls  
inheriting from popup (such as drawer, menu) still follows earlier  
behavior.  
  
* ca20f7e82f Add a radius property for each corner of a Rectangle  
Rectangle can now render individual radii on each corner.  
  
* 71e6a60a3d Remove QML_LEAK_CHECK  
The environment variable QML_LEAK_CHECK is replaced by the logging  
category qt.scenegraph.leaks.  
  
* 4cdf0643b4 QtQml: Key singletons by singleton instance info  
The QML engine will now refrain from creating separate instances of a  
singleton type for each version it is registered for if the singleton is  
registered declaratively (using QML_SINGLETON). The behavior of  
procedurally registered singletons (using the qmlRegisterSingletonType()  
family of functions) remains the same: For each registration call, a  
separate singleton instance is created.  
  
* 8e7572ac63 Make text node scenegraph API public  
Added QSGTextNode and QQuickWindow::createTextNode() for creating scene  
graph nodes containing text. This can be useful when building custom Qt  
Quick items with text.  
  
* 9427ee785c Fix Material dark theme not being respected when used as a  
fallback  
The fallback style's theme is now initialized, allowing e.g. the  
Material style's dark theme setting to be respected when it's set as the  
fallback style and the user is using run-time style selection. Compile-  
time style selection is unaffected and continues to work correctly.  
  
* bb8fb504fe Fix translucent NativeRendering text on transparent window  
Fixed an issue where NativeRendering text with a translucent color  
combined with a transparent window would cause unexpected translucency  
effects on opaque parts of the scene.  
  
* 16023fc77c Defer automatic Window transient parent until component  
completion  
Declaring Windows via dedicated properties of another Window or Item  
will result in an automatic transient parent relationship to the parent  
Window or Item, just like declaring it as part of the default data  
property.  
  
* d6e0d5630a Add pragma syntax to support translation context  
The context for the translation can now be controled in a given file  
using pragma Translator.  
  
* 1052fb195f Set implicit size for QQuickShape  
The Shape item now implements implicitWidth and implicitHeight, so it  
will get a non-empty size by default, and be appropriately placed in  
layouts.  
  
* a927fcd4ac Fix missing paragraph containing object replacement char  
Fixed an issue where a paragraph containing the Object Replacement  
Character (U+FFFC) would be invisible.  
  
* f5aecbde91 QtQml: Allow multiple names for C++-based QML types  
You can now have multiple QML_NAMED_ELEMENT macros in the same C++  
class to make one C++ type available with more than one QML name.  
  
* 8f6809681e Disable TapHandler.longPressed signal if longPressThreshold  
== 0  
TapHandler.longPressThreshold can now be set to 0 to disable its press-  
and-hold feature, and can be reset to undefined to restore the platform  
default.  
  
* 79474b087a Drawer: adjust opening edge to the rotation of the window's  
content item  
If the window's content item is rotated, then the drawer will adapt the  
edge from which it can be drawn out accordingly. Only multiple of 90  
degrees are supported.  
  
* d0fcada55f Popup: keep popup and overlay centered for all orientations  
Changing the contentOrientation of the window no longer repositions the  
overlay and popup items. They now stay centered over the window's  
contentItem. To rotate the entire UI in a window, set the rotation  
property of the contentItem.  
  
* 84d950bc32 QML: Let IDs in outer context override bound components'  
properties  
In QML documents with bound components, IDs defined in outer contexts  
override properties defined in inner contexts now. This is how  
qmlcachegen has always interpreted bound components when generating C++  
code, and it is required to make access to outer IDs actually safe. The  
interpreter and JIT have previously preferred inner properties over  
outer IDs.  
  
* 91e75fc347 QQuickItemGrabResult: Grab with window devicePixelRatio  
grabToImage now grabs the item taking into account its  
devicePixelRatio.  
  
* a63fe035e3 Implement variable axes API in QML  
Added font.variableAxes property.  
  
* b46d6a75ac Add load/save functionality to QQuickTextDocument (Tech  
Preview)  
TextEdit.textDocument now has a source property for loading files;  
save() and saveAs() functions for writing; a modified property which  
tracks QTextDocument::modified; and an error signal in case any of these  
operations fail. Setting the source property is allowed only if the  
document is in unmodified state. This API is in Tech Preview.  
  
* b00798df9d MessageDialog: Dont rely on accept or reject signal  
emissions from QPA  
The MessageDialog will now close when a button is pressed, regardless  
of the button's role.  
  
* 1ca9928856 Move focusReason from QQuickControl to QQuickItem  
The focusReason property has now moved from QQuickControl to  
QQuickItem.  
  
* 64234dfc70 Move focusPolicy from QQuickControl to QQuickItem  
The focusPolicy property has now moved from QQuickControl to  
QQuickItem.  
  
* 43625c7140 QQuickItem: Make focusReason property read-only from QML  
focusReason property is read-only.  
  
* 045f9ce192 Add TextSelection (Tech Preview)  
TextEdit.cursorSelection is a TextSelection object, which provides  
properties to inspect and modify the formatting of the single selection  
that is currently supported. This API is in Tech Preview.  
  
* 8dd6878364 MessageDialog: make QQuickAbstractDialog::result return  
button pressed  
The MessageDialog will no longer emit rejected when the user presses a  
button that doesn't have the role NoRole or RejectedRole.  
  
* f926f7acf6 CMake: Fix the all_qmllint* targets for VS generators, take  
II  
When using CMake's Visual Studio project generator, the creation of the  
targets all_qmllint, all_qmllint_json and all_qmllint_module requires  
now CMake 3.19 or newer. A warning is printed for older CMake versions.  
This warning can be disabled by setting QT_NO_QMLLINT_CREATION_WARNING.  
  
* 1495051e07 CMake: Add a way to pass additional arguments to  
win/macdeployqt  
Added the DEPLOY_TOOL_OPTIONS argument to the function  
qt_generate_deploy_qml_app_script.  
  
* ea9c46ed26 API Cleanup: QQuickItem: Add parameter to  
focusPolicyChanged signal  
focusPolicyChanged signal now takes a Qt::FocusPolicy parameter.  
  
* 41d9d86f6e Set default layout size policies for quick items  
The QtQuick items now set their default size policy and it would be  
effective when used within QtQuick Layouts.  
  
* 32b4d8bb16 Fall back to retrying with "software" when swapchain fails  
The fallback to a software rasterizer, if applicable to the platform  
and 3D API, is now performed also upon the first swapchain creation  
failure. Previously this was only done if the QRhi initialization  
failed. Relevant in particular on Windows, potentially allowing  
functioning on systems that are incapable of proper accelerated D3D  
rendering, but, for whatever reason, do not fail early on upon the  
device/context creation, only later at swapchain creation.  
  
* e824eaf86d doc: Clarify that automatic transient parent relies on  
visual parent  
Windows that automatically pick up a transient parent window from its  
Item parent will not be shown unless the item is part of a scene.  
  
### qtmultimedia  
* edb6324fb Update doc and attributions with new FFmpeg version in  
Multimedia  
Updated FFmpeg to n6.1.  
  
* 24bb44389 Rename QAudio namespace to QtAudio  
The QAudio namespace has been renamed to QtAudio, with QAudio still  
being available as an alias. String based connections to  
QAudioSink/Source::stateChanged need to continue to use QAudio::State as  
the parameter.  
  
### qttools  
* 43114e955 Qt Designer: Add QFont::Weight to the property editor  
QFont::Weight is now available in the property editor, introducing a  
new "fontweight" .ui attribute. To preserve compatibility, the values  
"Normal"/"Bold" will result in the old "bold" attribute being used.  
  
* 9d3891fcd Qt Designer: Add a way of specifying plugin paths  
Added API and command line options for modifying the plugin paths.  
  
* 685037c07 lconvert: Add -pluralonly command line argument  
Added a -pluralonly command line argument to drop non-plural form  
messages.  
  
* 94bb328a1 CMake: Make the target argument of qt_add_lrelease optional  
Passing a target as the first argument to qt_add_lrelease was  
deprecated.  
  
* 3c5603a77 CMake: Allow specifying multiple targets in qt_add_lupdate  
Added the TARGETS option to qt_add_lupdate to handle multiple targets.  
  
* 8a0adfa78 CMake: Support project-wide i18n with qt_add_translations  
qt_add_translations gained the TARGETS argument to specify multiple  
targets that intend to load .qm files.  
  
* 8b664bcfb CMake: Allow excluding target sources from i18n  
The target property QT_EXCLUDE_SOURCES_FROM_TRANSLATION was added to  
exclude source files of a target from handling with lupdate.  
  
* cda38d3d0 lupdate: remove number heuristics  
Removed the number heuristics feature. Users are advised to avoid hard-  
coded numbers in translatable strings and use QString::arg instead.  
  
* f93028758 CMake: Automatically determine .ts file names in  
qt_add_translations  
The TS_FILES argument of qt_add_translations is optional now, and .ts  
file paths can be automatically determined after setting the  
QT_I18N_LANGUAGES variable.  
  
* 17680273b CMake: Add a way to specify the native language for i18n  
qt_add_lupdate gained the NATIVE_TS_FILE argument that denotes the .ts  
file for the native language of the application. This .ts file will  
contain only plural forms.  
  
* ffe105e1a CMake: Automatically determine the path of the native .ts  
file  
If the TS_FILES argument is not passed to qt_add_translations, the path  
to the native .ts file is automatically determined if  
QT_I18N_NATIVE_LANGUAGE is set.  
  
* a52c1be27 Qt Designer: Write fully qualified enumerations  
Qt Designer will output fully qualified enumeration values in .ui files  
to accommodate for scoped enums and Qt for Python.  
  
* e12950c83 QDoc: Require libclang >= 15  
QDoc now requires LLVM 15 or newer.  
  
* 6942bc0ee qdoc: Introduce \generatelist qmlvaluetypesbymodule  
The \generatelist QDoc command now supports listing    QML value types  
explicitly by passing qmlvaluetypesbymodule as    the first argument.  
  
* aef0c3cf3 CMake: Fix qt_add_translations in different subdirs for VS  
generators  
When using CMake's Visual Studio project generator, the creation of the  
update_translations target requires now CMake 3.19 or newer. A warning  
is printed for older CMake versions. This warning can be disabled by  
setting QT_NO_GLOBAL_LUPDATE_TARGET_CREATION_WARNING to ON.  
  
* a6007f58f Update qlitehtml submodule  
Litehtml (used in Qt Assistant) was    updated to upstream version v0.9.  
  
### qtdoc  
* 1cf3295c Bump CMake requirements on Apple platforms  
The minimum CMake version for Qt on Apple platforms is now 3.21.1.  
  
### qtsensors  
* f5eae761 QtSensors: Expose QSensor::isFeatureSupported to QML  
Add QmlSensor::isFeatureSupported().  
  
### qtconnectivity  
* 4d5da3f5 QBluetoothAddress: add qHash() as a proper hidden friend  
Added qHash().  
  
* 439e818f QBluetoothUuid: remove default case labels and fix the  
fallout  
Fixed missing result of  
characteristicToString(CharacteristicType::WeightScaleFeature).  
  
* aff0acde QBluetoothUuid: inherit all ctors from QUuid  
QBluetoothUuid now provides all the constructors that QUuid also  
provides (incl. from GUID and QAnyStringView).  
  
* 9db4dd9f Make BlueZ DBus peripheral the default backend on Linux  
The default Linux peripheral implementation was changed from the kernel  
interface to the BlueZ DBus interface. The old implementation remains  
available by defining QT_BLUETOOTH_USE_KERNEL_PERIPHERAL as environment  
variable.  
  
* 6a2c6e31 PCSC: Make polling interval adjustable via environment  
The polling interval is now configurable using QT_NFC_POLL_INTERVAL_MS  
environment variable. The default polling interval was reduced to 100ms.  
  
### qt3d  
* 781c07e2a Texture array support for RHI renderer  
Enable texture array on the RHI render plugin  
  
* e275b1c28 Fix Race Condition in NodePostConstructorInit::processNodes  
Fix Race Condition in NodePostConstructorInit::processNodes  
  
* 9cc525731 Fix ambient color contribution in Phong shader  
Fix ambient color contribution  
  
* 51cfb893c Enable uniform buffer for RHI compute shaders  
Enable uniform buffer for RHI compute shaders  
  
### qtimageformats  
* 32d5b3d Update bundled libwebp to version 1.3.1  
Update bundled libwebp to version 1.3.1  
  
* 5428d25 Update bundled libtiff to version 4.5.1  
Bundled libtiff was updated to version 4.5.1  
  
* 4cfdd47 Update bundled libwebp to version 1.3.2  
Update bundled libwebp to version 1.3.2  
  
* 4feed66 Update bundled libtiff to version 4.6.0  
Bundled libtiff was updated to version 4.6.0  
  
### qtserialbus  
* 5cf1eb9f QModbusPdu: remove Q_DECLARE_TYPEINFOs  
The class and its subclasses are no longer marked as  
Q_RELOCATABLE_TYPE.  
  
* 8f1167b9 QCanDbcFileParser: add parseData(QStringView)  
Added method parseData(QStringView), which takes the contents of a DBC  
file as an input parameter. Use this method if the DBC file has an  
encoding different from UTF-8. In such cases the file contents should be  
first properly converted to QStringView, and then passed to this method.  
  
### qtserialport  
* 3bdac61 Fix QSerialPort::bindableStopBits return value type  
QSerialPort::bindableStopBits() now returns  
QBindable<QSerialPort::StopBits> instead of QBindable<bool>.  
  
### qtwebengine  
* 3feab861f RenderWidgetHostViewQtDelegateItem: keep grabs  
WebEngineView (or WebView backed by Qt WebEngine) no longer allows  
components outside to take over the mouse or touch exclusive grab. For  
example if the user starts dragging a scrollbar inside the web view,  
that continues until release, regardless of any DragHandler, Flickable  
etc.  
  
* 37430020d Add clearHttpCacheCompleted signal to profile  
Added clearHttpCacheCompleted signal.  
  
* bd8572420 Add QWebEngineSettings::ForceDarkMode  
ForceDarkMode added, disabled by default.  
  
* f46e2f2d6 Fix corrupted load/fetch state on start up in case of  
NoCache  
Switching profile to NoCache do not longer implicitly removes cache  
from old data store.  
  
* a82e90223 Add new API for screen capturing  
Add QQuickWebEngineView::desktopMediaRequested() signal  
  
* 613be810d Add WebEngineDriver  
Added WebEngineDriver  
  
### qtvirtualkeyboard  
* 5445b917 Make qvirtualkeyboardnamespace.h private  
The qvirtualkeyboardnamespace.h header has been made private. None of  
the enum types declared in that header are used in public C++ APIs.  
  
* e5bf53cc Restore style path for backwards compatibility  
Restored style path /QtQuick/VirtualKeyboard/content/styles for  
backwards compatibility.  
  
### qtremoteobjects  
* a495a5c9 QNX QIODevice subclasses: remove Q_DECLARE_TYPEINFOs  
These classes are no longer marked as Q_RELOCATABLE_TYPE.  
  
### qtquick3d  
* 28839c49 Support HDR (linear) images as base color maps  
Using HDR images (loaded from .hdr or .exr files) as base color maps  
are now supported correctly. Previously the image data was incorrectly  
going through sRGB->linear conversion which is incorrect for HDR image  
data as they are not sRGB (or any other color space for that matter).  
  
* 1633d6c1 Add separate controls for RGB and Alpha blending in custom  
materials  
Added separate controls for alpha blend factors.  
  
* be16b0ae Add a way to override the backing texture size with the  
Offscreen mode  
Added View3D properties to override the backing texture's size when  
using the default Offscreen render mode. This allows the application to  
specify its own render target resolution (for example because the  
developer knows that the content is fine with a lower resolution instead  
of following the windowing system dictated geometry and high DPI scale  
factor). For easy experimenting, the properties are also exposed in the  
DebugView item.  
  
### qt5compat  
* 5420ed0 SAX: Remove unused QtXml/qtxmlglobal.h header inclusion  
The QtCore5Compat/qxml.h header no longer includes QtXml/qtxmlglobal.h.  
  
### qtopcua  
* d624a8f2 Encode 0 node id for empty string  
Encoding empty strings as    node id is now permitted.  
  
* 03fcb5c3 open62541: Re-encode unhandled types to QOpcUaExtensionObject  
Unknown types that are decoded by the stack    and have no Qt OPC UA  
data classes will now be re-encoded and returned    as extension object  
instead of an empty QVariant.  
  
* 699de8e3 Add support for the DataTypeDefinition attribute  
The DataTypeDefinition attribute of DataType nodes can now    be read.  
This allows manual decoding of generic structured and enum types.  
  
* e324f887 Add the DiagnosticInfo data type  
The DiagnosticInfo data type is now available    for reading and  
writing.  
  
* 4992ea8d Add generic struct handler  
Qt OPC UA has been extended with a generic struct    handler which  
enables the user to automatically decode structured types    having the  
DataTypeDefintion attribute set.  
  
* e4e0731a Add read and write support for EventFilter and types it  
depends on  
The open62541 plugin is now capable of    reading and writing  
EventFilter and its dependency types.  
  
* 947dda8b Add API for the RegisterNodes and UnregisterNodes services  
QOpcUaClient now supports registerNodes()  and unregisterNodes() with  
the open62541 plugin.  
  
* 4a2b804e Remove the UACPP plugin  
The Unified Automation backend has been removed.    The open62541  
backend will be able to act as a drop-in replacement for    everything  
except the connectError() signal.  
  
* 925ea2ed Add historical events read support  
Qt OPC UA is now capable of    reading historical events with the  
open62541 plugin  
  
* c23cccdd Implement triggering for monitored items  
QOpcUaNode now supports SetTriggering  to set up a triggering link  
between two monitored items.  
  
* 245951a3 Replace incorrect license attribution for 3rdparty/open62541  
Correctly refer to the CC-BY-SA0 license as "Creative Commons  
Attribution Share Alike 4.0 International".  
  
### qthttpserver  
* 4a8cd55 Access to the ssl config in QHttpServerRequest  
Added sslConfiguration().  
  
### qtquick3dphysics  
* 476efc4 Support disabling simulation of a body  
Add support for disabling simulation of a body through the  
PhysicsBody::simulationEnabled property.  
  
* 71b26a5 Support setting simulation thread count  
Support setting simulation thread count.  
  
* 3012a8a Support collision filtering  
Add support for collision filtering. It is now possible to specify  
groups IDs for nodes and ignore collisions between them.  
  
* 31e2d0b Add collision report properties  
Add reportKinematicKinematicCollisions and  
reportStaticKinematicCollisions properties that will enable kinematic-  
kinematic and static-kinematic collision reporting respectively.  
  
* c71bc44 Support using QQ3DGeometries as mesh sources  
Support using QQuick3DGeometry as source through the  
TriangleMeshShape::geometry property.  
  
* 7a2852e Support using Image as source to heightfield shape  
Support using QML Image type as source through the  
HeightFieldShape::image property.  
  
### qtgrpc  
* 453d694 Remove silent reconnection to grpc server stream  
Client HTTP/2 channel doesn't retry to start server-stream  
automatically after connection is lost, since this contradicts gRPC  
streaming concepts. The error should be handled by business logic of an  
application instead.  
  
* 59f3429 Add enum size spec  
Generated enums now have int32_t type spec according to protobuf  
specification.  
  
* b089a77 Move enums to the nested namespace out of class  
Nested enums moved out of message classes to the nested namespace, same  
as the nested messages.  
  
* 3f51504 Split QGrpcOperation into Client and Channel parts  
QGrpcOperation::abort function is replaced by QGrpcOperation::cancel  
function. The logic of new function is generic for all gRPC operations.  
All grpc operations(calls and streams) now emit errorOccurred signal  
when cancelling.  
  
* fcb87b4 Emit the finished signal for grpc calls even if error occurred  
Unary gRPC calls now emit both 'errorOccurred' and 'finished' signals  
if the call is finished with error. Previously only the 'finished'  
signal was emitted.  
  
* b1a78d7 Do not capitalize the enum field names  
Enum fields now preserve the case of first letter. Previosly generator  
capitalized the generated enum field names.  
  
* 913aef6 Implement support of 'optional' fields  
All message fieds now have 'has' methods that indicate if message was  
initialized and contain value or not.  
  
* 845b7f2 Delete generation of duplicating qt-properties with standard  
types  
remove generation of additional Message properties that were used in  
QML. Since Qt Protobuf type converters are created and work correctly,  
we can just directly use QtProtobuf::int32/QtProtobuf::int64/etc types  
in Q_PROPERTY().  
  
* 3937931 Introduce QGrpcClientInterceptor  
Added QGrpcOperation::waitForFinished() method.  
  
* 703f2e3 Rid of synchronous gRPC API  
The synchronous gRPC calls are not generated anymore. All related API  
is removed.  
  
* ef91694 Rename QML URI of the QtGrpcQuick module  
The QML URI of the QtGrpcQuick module is changed to QtGrpc. All  
occurrences of module imports should be changed to 'import QtGrpc'.  
  
* 435d475 Add the missing Licenses and Attributions sections  
qtprotobufgen, qtgrpcgen tools link against protobuf libraries,  
licensed under BSD 3-clause "New" or "Revised" License. This is now  
documented.  
  
* 74b45fd Add the missing _p suffix for protobuf messages that are oneof  
members  
Properties of protobuf message types that are oneof members now have  
'_p' suffix, since they are formally private.  
  
* b86990f Add public API to get unknown fields from deserialized  
QProtobufMessage  
Added the public unknownFieldNumbers() and unknownFieldData()  
functions.  
  
* fbf877c Add JSON serialization and deserialization for Qt Protobuf  
Edit existing QProtobufSerializer API, also move  
serialization/deserialization methods from QProtobufSerializer class  
into QProtobufBaseSerializer interface, since all of them shall be re-  
usable for new Json-serializer.  
  
* 8ac1b26 Make QProtobufSerializer and QProtobufJsonSerializer non-  
stateless  
Any type API is changed. 'as' and 'fromMessage' functions not accept  
the pointer to a serializer.  
  
* 0812595 Make the both QProtobufSerializer and QProtobufJsonSerializer  
final  
Both QProtobufSerializer and QProtobufJsonSerializer are final now.  
  
* 4243dfb Implement JSON (de)serialization of enums  
Changed the following interfaces:  - serializeEnum  - serializeEnumList  
- deserializeEnum  - deserializeEnumList All interfaces now have the  
mandatory const QMetaEnum &metaEnum argument. The argument is needed to  
convert the enum value to its string representation.  
  
* fa30200 Add the pre-generated map pair property ordering  
Removed infoForMapKey and infoForMapValue methods from the  
QtProtobufPrivate::QProtobufPropertyOrderingInfo structure.  
  
* cdaf519 Use the QML_NAMED_ELEMENT for the gRPC client in QML context  
gRPC clients now are registered as <ServiceName>Client in QML context.  
  
* 6671df0 Fix the generation of the export macro  
New option extras allow setting the generated export filename and  
control if it should be generated at the generator run.  
  
### qtinsighttracker (Commercial only)  
* 8e89373 Support remote configurations  
Application's insight tracker configuration can be changed at runtime  
from the Qt Insight Console.  
  
* 08f5c97 Support compressed sqlite databases  
The SQLite event storage can now be compressed with either zlib or zstd  
algorithms.  
  
* 655ea8a Add context data to event API  
New API: Context data can now be included in the interaction and  
transition events.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-114206 tst_qquick3dbuffermanager (Failed)  
* QTBUG-114238 API asymmetry in isEmpty / isNull between QByteArray and  
QString operator+=  
* QTBUG-108794 Building applications against static QNX build fails  
* QTBUG-114204 QTabBar tabs above current index not visible if current  
index is set before the tabbar is drawn  
* QTBUG-113811 [REG: 6.2->6.5] windows: 16x multisampling produces a  
border (NVIDIA)  
* QTBUG-100094 iOS A11Y unexpected reset  
* QTBUG-114236 Any Drag and Drop crashes on 6.5  
* QTBUG-113591 Problem updating QDockWidget's title with translations  
* QTBUG-112829 QGuiApplication::screens() returns only the secondary  
screen  
* QTBUG-114085 qt-configure-module with parameters fail at run at root  
directory  
* QTBUG-114229 Broken bitmap fonts when a non-rotating transform is set  
* QTBUG-112968 QTextEdit hangs when large text is copied  
* QTBUG-112742 REG: QScreen physicalSize() return wrong results on  
Android / Qt 6.5 - returns pixels not millimeters  
* QTBUG-112246 ios: Assert if closing keyboard and touching the screen  
with another finger  
* QTBUG-113165 Native text on macOS and iOS is not the same.  
* QTBUG-111901 Release build still puts debug info into .so files  
* QTBUG-110942 I see 2 icons showing up in our QTreeView since upgrading  
to Qt6  
* QTBUG-112217 setTearOffEnabled() leading to crash  
* QTBUG-113438 AT-SPI: Wrong char reported by GetCharAtOffset when code  
point > 65535  
* QTBUG-73834 No data signature found  
* QTBUG-79934 WASM - Qt Quick application does not have keyboard focus  
after loading  
* QTBUG-113416 [Reg 6.4->6.5] Static build fails at PDF module  
* QTBUG-54955 Mac: Wrong QDate string conversion with  
Qt::SystemLocaleLongDate on dates prior to 1893-04-02  
* QTBUG-93009 QPalette::PlaceholderText color is not followed after  
setting color in a style sheet  
* QTBUG-112513 QFuture continuation segfaults with move only datatypes  
* QTBUG-114313 [Reg: 5.15 -> 6.2/6.5?] QQuaternion::getAxisAndAngle()  
can produce NaN, even when normalized  
* QTBUG-114431 FindEGL.cmake fails for static linking with Qt  
* QTBUG-114446 wasm: native keyboard does not popup on iOS  
* QTBUG-113717 QComboBox::removeItem is triggering  
QComboBox::currentTextChanged.  
* QTBUG-109405 [Regression] 6.3.1 -> 6.4.1 Android - QSettings lost  
* QTBUG-109369 QSettings - default file location changed between Qt5 and  
Qt6 on Android  
* QTBUG-87603 Crash when concatenating two strings using  
QT_USE_QSTRINGBUILDER  
* QTBUG-47066 Segmentation fault with QStringBuilder  
* QTBUG-104354 Document QStringBuilder's auto gotcha  
* QTBUG-114199 macOS: Clicking on a menu item which opens a submenu  
erroneously closes menu  
* QTBUG-114078 wasm: NetworkReply with empty data generates runtimeError  
* QTBUG-113573 When dragging a header section it will no longer scroll  
when at the edge  
* QTBUG-113765 QComboBox: Wrong popup position when switching to Fusion  
style  
* QTBUG-114530 Qt build in jenkins triggers message boxes with help  
messages from Qt tools  
* QTBUG-111330 error: Not a signal or slot declaration in code generated  
by qt_add_dbus_interface  
* QTBUG-48161 QDockWidget emits visibilityChanged(false) when minimizing  
the window or switching virtual desktops  
* QTBUG-62912 Hover is not reset properly with touchscreens  
* QTBUG-113641 PlatformCommonInternal INTERFACE_LINK_OPTIONS property is  
propagated to user projects  
* QTBUG-114576 QFileInfo("assets:/path/to/file").fileName() returns  
wrong name  
* QTBUG-114219 QFileInfo::fileName() does not strip assets prefix on  
Android  
* QTBUG-112261 [REGRESSION] QDir::entryList returns invalid names (6.4.2  
-> 6.4.3)  
* QTBUG-88316 [REG] Testcocoon support is totally broken. Consider  
removing it.  
* QTBUG-114625 TRY_RUN failure on cross-compilation  
* QTBUG-108015 [CMake] [MSVC2022] TEST_separate_debug_info always fail  
* QTBUG-112996 Moc error C2838: 'MyEnum': illegal qualified name in  
member declaration  
* QTBUG-114629 QJsonValueRef inherits non-exported class  
QJsonValueConstRef  
* QTBUG-114334 [REG 6.5.0 -> 6.5.1] Segfault in  
QXcbConnection::handleXcbEvent with touch(pad) gestures after  
disconnecting input device  
* QTBUG-114537 linking of QtNetwork against GSSAPI fails on macOS with  
CMAKE_FIND_FRAMEWORK=LAST  
* QTBUG-114546 [Reg 6.2.8->6.5.1] [macOS] Prior modal dialog and manual  
event processing can break QMessageBox  
* QTBUG-112491 examples/widgets/mainwindows/mainwindow crashes  
* QTBUG-114542 DockWidget Crashes when undocked and tabbified  
* QTBUG-114606 Cancelling a QPromise with a failure handler crashes  
* QTBUG-112351 Incorrect description of QtConcurrent::run()  
* QTBUG-114654 KeyRelease event not propagated to parent of QLineEdit  
* QTBUG-112200 Possible memory leak with Fusion style  
* QTBUG-114480 Plugins available via multiple paths are loaded without  
RTLD_NODELETE  
* QTBUG-71674 Registering an object to dbus without interface can lead  
to invalid dbus interface getting registered  
* QTBUG-113975 [iOS] Button cannot be focused and take action if it is  
placed in text area  
* QTBUG-114416 iOS: Focussing on a read-only TextEdit can prevent Button  
from receiving further clicks  
* QTBUG-92464 QCompleter breaking use of keyboard accents  
* QTBUG-108522 [Regression: 4 - 5&6] QCompleter can not use input method  
when completer popup is visible on Linux  
* QTBUG-114073 qdoc resolves "QML Import Path" reference incorrectly  
* QTBUG-112653 Incorrect colour name returned when handling  
colorSchemeChanged  
* QTBUG-114785 MinGW v13.1.0: errors in TinyCBOR (Windows 10 22H2  
x86_64)  
* QTBUG-114781 Reg->6.6/MSVC: Compile warning about Unused  
SlotArgumentCount in lambda connect  
* QTBUG-114115 Unable to run on Gitlab CI / Windows Server Core docker  
image  
* QTBUG-114571 Incorrect colors after switching between light and dark  
modes  
* QTBUG-113169 QStyleHints::colorScheme reports incorrect value and  
breaks app palette  
* QTBUG-114191 [Dialog QML] Dialog becomes dark after putting the app in  
the background and resuming it back with iOS style  
* QTBUG-114225 QTableView create extra row  
* QTBUG-108482 Mention more clearly that only a subset of features of  
supported HTML tags are implemented  
* QTBUG-114826 multiwindow manual test does not work with D3D12 backend  
* QTBUG-114821 [Reg 6.4->6.5] QMenu no longer renders disabled text  
correctly  
* QTBUG-114865 macos: Building QtWebEngine  with sanitizer enabled fails  
* QTBUG-114605 [macOS] Hover events are not received if the parent of  
the QWindow is embedded  
* QTBUG-114583 Headers use things in <iterator> without including it  
* QTBUG-77059 QStorageInfo::mountedVolumes() doesn't list volumes  
mounted after "docker overlay volumes"  
* QTBUG-114760 tst_QComboBox::popupPositionAfterStyleChange is flaky  
* QTBUG-68821 QNetworkAccessManager does not propagate proxy errors  
properly  
* QTBUG-106483 Moving a window to another screen (different DPI) using  
keyboard shortcuts while a menu is open has unexpected behavior  
* QTBUG-114847 QMAKE_APPLE_DEVICE_ARCHS not documented  
* QTBUG-109781 QXmlStreamReader asserts trying to construct XmlStringRef  
of negative len on external input  
* QTBUG-114829 [REG 6.5.1 -> 6.5.2] Crash/failed assert by passing  
certain xml file to QXmlStreamReader  
* QTBUG-114931 MSVC 2022 v17.6.4 causing build failure with Windows 10  
22H2  
* COIN-1059 windows-10_22h2-msvc2022 needs newever msvc 2022  
* QTBUG-114803 iOS Simulator build fails  
* QTBUG-114600 [REG 6.4.3 -> 6.5.0] Strange UI styles  
* QTBUG-113698 Nullptr dereference in qcoretextfontdatabase.mm  
* QTBUG-114783 RCC requires openssl  
* QTBUG-114470 Build failure for iOS  
* QTBUG-114925 Reg->6.6/MSVC/WIndows:  Cannot build with debug due to  
compiler flag clash in syncqt  
* QTBUG-113685 macOS: QMessageBox does not emit the accepted signal when  
parented  
* QTBUG-112995 Long press on touch screen breaks drag and drop  
* QTBUG-114919 QFileDialog spams users with permission requests  
* QTBUG-114944 qtestcase.h may need a fix to avoid unreachable code  
warning.  
* QTBUG-112371 Unreachable code warning with MSVC2019 with QTestCase  
class  
* QTBUG-114797 QVariant::convert may crash even if QVariant::canConvert  
returns true  
* QTBUG-107120 QSqlDatabase not working with SQLite files from  
QFileDialog  
* QTBUG-112893 WASM: exec() fails, even when ASYNCIFY is enabled  
* QTBUG-114918 qvulkanwindow.cpp:451:3: error: redefinition of  
'qvk_sampleCounts  
* QTBUG-115031 qtbase -unity-build-batch-size 103 fails  
* QTBUG-112956 [REG 6.4] syncqt.cpp does not install headers marked with  
qt_deprecates pragma  
* QTBUG-114683 Not null value is not enforced in SQL iBase plugin  
* QTBUG-115003 QPainter crash when drawing image  
* QTBUG-114991 QVariant<double> comparison uses <float> on  `-qreal  
float`  platforms  
* QTBUG-115002 Can't import MTLDevice with QRhi Metal.  
* QTBUG-115043 Minor source compatibility break in QLoggingCategory  
* QTBUG-114377 Broken focus when hiding a button of a QDialogButtonBox  
* QTBUG-115062 Incorrect handling of  
QT_FATAL_CRITICALS/QT_FATAL_WARNINGS (non-UB data race)  
* QTBUG-2597 [PATCH] Improved error output for qdbusxml2cpp  
* QTBUG-115101 WaylandGlobalPrivate_sync_headers is not running if  
nothing depends on WaylandGlobalPrivate  
* QTBUG-113110 a11y: AT-SPI TableCell methods GetRowHeaderCells and  
GetColumnHeaderCells not implemented  
* QTBUG-115124 qtpaths JSON output is invalid  
* QTBUG-114825 Blacklisting of tst_qquickpopup::hover doesn't work  
* QTBUG-115135 a11y: Top-level item views don't have the application as  
accessible parent  
* QTBUG-95569 CMake infinite loop when configuring with Vulkan support  
in Conan  
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
* QTBUG-115160 Typo in QWidget::backgroundRole() doc  
* QTBUG-114473 QPalette::cacheKey() is different for same object iff own  
style sheet is used  
* QTBUG-115147 Title text of stacked dock widgets shown in wrong  
location during drag with stylesheet style  
* QTBUG-113319 ICOReader does not read AND mask for 16bpp/24bpp ico  
* QTBUG-115154 tst_QSocketNotifier::unexpectedDisconnection is flaky on  
macOS  
* QTBUG-113461 QML TextField Popup  
* QTBUG-115105 QAtomicScopedValueRollback: CTAD from  
Q(Basic)AtomicPointer fails  
* QTBUG-114854 windeployqt deploys debug versions of QML plugins  
* QTBUG-112895 bool ParseResult::operator bool() returns true if no  
error  
* QTBUG-114069 qt_generate_deploy_app_script error when cross-compiling  
* QTBUG-115229 Qt 6.5.1 MSVC 2019 fails to compile QtMqtt because of  
Chinese text encoding  
* QTBUG-97482 Android: QPushButton with QMenu does not work on Qt6  
* QTBUG-115243 qtbase 6.6.0-beta2 fails to build (linux-clang target) at  
cmake stage if -DQT_FEATURE_gc_binaries is used  
* QTBUG-115249 QCborValue mem leak in or near convertArrayToMap()  
* QTBUG-115054 QWidget::createWindowContainer does not work on 6.5.1  
* QTBUG-114909 QLocale::toTime with ShortFormat returns invalid QTime  
for en_US "h:mm AP"  
* QTBUG-109104 Provide QStringConverter alternative to  
QTextCodec::availableCodecs  
* QTBUG-114559 SPNEGO/Negotiate:  Can't set spn Option - Signal not  
firing  
* QTBUG-115263 QHostInfo is leaking QSlotObjectBase in  
tst_QHostInfo::lookupConnectToFunctionPointerDeleted()  
* QTBUG-115318 QT_ANDROID_DEPLOY_RELEASE CMake variable has no effect  
* QTBUG-112921 Cannot create packages for Google PlayStore  
* QTBUG-108132 cannot set --release option to androiddeployqt when  
building app with cmake ?  
* QTBUG-111959 (potential BiC) Exported class QTimerList inherits from  
QList  
* QTBUG-115324 Qt6 configured wrong when is placed inside "3rdparty"  
folder  
* QTBUG-115286 QFactoryLoader memory leak on follow-up setExtraPath()  
* QTBUG-114575 Value changes when cursor is moved in date/time field  
* QTBUG-96636 Some Postgresql jsonb operators mistaken for prepared  
statement placeholders.  
* QTBUG-115189 QColorDialog regression in 6.5.1  
* QTBUG-115473 Missing QSet::removeIf() method  
* QTBUG-114958 dev/6.7: Windows: qsb crashes in debug build, causing  
qtdeclarative build to fail  
* QTBUG-115506 qmake fails to provide correct export name to shell html  
* QTBUG-115505 Shared build doesn't succeed due to missing JSPI function  
definitions  
* QTBUG-115507 qmake fails to provide correct preload list to shell html  
* QTBUG-115516 QColorDialog: WA_Hover breaks color and luminance picker  
* QTBUG-115521 opengl can't upload R8 texture  
* QTBUG-114338 Qt Quick with metal crashes on older macOS 11  
* QTBUG-108216 Investigate the QRhi pipeline cache (MTLBinaryArchive  
usage) on macOS 13  
* QTBUG-115327 echoplugin uses an ambiguous project name  
* QTBUG-115599 Possible SEGV (null pointer deref) in  
QXcbConnection::initializeAllAtoms()  
* QTBUG-115646 QTypeTraits::has_operator_less_than_v behaves  
surprisingly  
* QTBUG-115149  Unwanted highlight of arrows in tree view when hovering  
with mouse  
* QTBUG-115596 qdbusxml2cpp errors with valid DBus XML - causes  
compilation failures  
* QTBUG-115045 Don't overwrite my CMAKE_<Config>_POSTFIX  
* QTBUG-115037 WASM: Settings issue when removing a group of keys  
* QTBUG-115509 tst_qsettings doesn't pass on WASM  
* QTBUG-115712 [REG 6.6.0 beta2->beta3] Qt source not compiling on  
macOS, declarative/webchannel?  
* QTBUG-115330 QCoreApplication::requestPermission() is leaking slot  
objects  
* QTBUG-91448 Undefined resource symbols when linking app with a static  
Qt without qmake and CMake  
* QTBUG-110243 Resources are lost when linking static libraries using  
CMake build system in a separate project  
* QTBUG-115758 Tuio Fiducials always contain invalid UniqueIds  
* QTBUG-115732 Incorrect IANA ID detected for Windows timezone La Paz,  
Mazatlan  
* QTBUG-115740 QLocale for Spanish does not work correctly with  
thousands separators.  
* QTBUG-115737 qmake should allow to override _DATE_  
* QTBUG-40315 doc: QFontMetrics::elidedText(...) does not work as  
expected for ElideNone  
* QTBUG-105007 On macOS, QMimeType::comment returns value for the  
secondary language  
* QTBUG-94460 QLocale's names for languages, scripts and territories  
don't match CLDR's en.xml's proper names  
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
* QTBUG-113557 Raster native widget fail to draw when there is a quick  
widget sibling  
* QTBUG-115959 Stack corruption when using JSPI from within a posted  
event  
* QTBUG-115852 QCollator on ios doesn't support numeric mode  
* QTBUG-115109 [REG] QTabWidget doesn't draw tabs on the left of the  
initially current tab  
* QTBUG-113140 Resizing a QTabBar resets the scroll position  
* QTBUG-116137 Compile and install QtBase 6.5.2 does not provide header  
files in -prefix path  
* QTBUG-115853 There is NO method current() for QVulkanInstance  
* QTBUG-115632 Long press textfield popup teleports after being drawn  
for the first time  
* QTBUG-116224 Wrong QScrollBar with Qt6.5 + windows vista style in RTL  
mode  
* QTBUG-58732 Crash after destroying an unfinished QDBusPendingCall  
* QTBUG-115752 stack-use-after-return in tst_assetimport  
* QTBUG-116166 Network tests fail with OpenSSL 3.1.1  
* QTBUG-108402 tst_Gestures failures on macOS 13  
* QTBUG-116060 Reg 6.4.3->6.5.1 QTimer - signal/slot connection not  
working  
* QTBUG-116287 [REG BiC 6.5.2 → 6.5.3] New QDialogButtonBox symbol  
* QTBUG-116351 QFileInfo::filesystemReadSymLink misses documentation  
* QTBUG-115087 getOpenFileContent does not open the dialog  
* QTBUG-116231 wasm: on windows, shift key produces the word "Shift"  
* QTBUG-116499 Use of edid serial number in qwindowsscreen.cpp is broken  
* QTBUG-116496 icx on windows qvariant_p.h call to customConstructShared  
is ambiguous  
* QTBUG-116527 Regression; (QML) Locale enums no longer exist  
* QTBUG-116517 Zero-width space in qaccessiblewidgets.cpp causing  
compilation error  
* QTBUG-115801 Exception in NVDA screen reader when hovering over text  
edit (due to invalid return value)  
* QTBUG-83733 Don't use deprecated/removed functions and structs with  
OpenSSL v3  
* QTBUG-114779 --no-feature-sharedmemory broken  
* QTBUG-116572 build failure about ‘sqlite3_filename’ has not been  
declared  
* QTBUG-116181 Android: QFile can't open file in directory which is  
chosen by QFileDialog::getExistingDirectory()  
* QTBUG-116056 signal not found when deleting QAbstractItemModel  
* QTBUG-115730 Qt uses Macros and config files from install tree when  
building qtdeclarative "again"  
* QTBUG-114423 [Reg 6.4.3->6.5] QTreeWidget crash inside QDialog on  
MacOS  
* QTBUG-116609 MinGW 13.1.0: Coin testing fails at qtbase  
* QTBUG-115461 [REG 6.5.1 -> 6.5.2] QT_WIDGETS_HIGHDPI_DOWNSCALE is  
broken again  
* QTBUG-113995 QDesktopServices::openUrl: Local files don't open anymore  
* QTBUG-115511 QToolTip StyleSheet Color Property Broken in 6.5.2  
* QTBUG-104688 State variable in QCheckBox::stateChanged should be  
emitted as Qt::CheckState instead of int  
* QTBUG-83881 dateTime != dateTime.addMSecs(0) after time zone change  
* QTBUG-116465 QVulkanFunctions & QVulkanDeviceFunctions actually  
support Vulkan 1.3  
* QTBUG-116696 Menus have window type _NET_WM_WINDOW_TYPE_NORMAL instead  
of _NET_WM_WINDOW_TYPE_POPUP_MENU  
* QTBUG-39887 Regression bug: QWidget::setAttribute() does not set  
Qt::WA_X11NetWmWindowType in Qt 5.  
* QTBUG-116729 BenchmarkDemoQt6 chokes the D3D12 backend with texture  
uploads  
* QTBUG-116338 Vulkan-based QQuickWidget or QRhiWidget is rendered  
incorrectly when in a QScrollArea  
* QTBUG-96936 qt features do not re-evaluate correctly on re-configure  
* QTBUG-85962 Improve FEATURE_foo to QT_FEATURE_foo detection  
* QTBUG-112957 Toplevel developer build fails to link: undefined symbol:  
vtable for QNetworkAccessDebugPipeBackendFactory  
* QTBUG-116758 Boot2Qt / Yocto build fails for qtbase in CI  
* QTBUG-116788 Sporadic crash on  
QNetworkReplyHttpImplPrivate::loadFromCacheIfAllowed() with nullptr  
access  
* QTBUG-116695 Contradictory statements about signal's return type  
* QTBUG-116277 QFileDialog not cleaned up when parent deleted  
* QTBUG-116715 docs: qsettings path on embdded linux  
* QTBUG-116330 wasm: Exit app with async main() results on runtime error  
* QTBUG-116232 Regression 6.5.2 vs 6.6.0 beta: macOS DPI change  
detection fails with 6.6  
* QTBUG-116757 QMessageBox does not show hyperlinks on macOS  
* QTBUG-116155 Crash with native QComboBox in refreshing QWidget  
* QTBUG-112525 macOS 6.5.0 native looking QMessageBox missing title and  
cannot change button texts  
* QTBUG-114720 QProcess::UnixProcessFlag::IgnoreSigpipe does not take  
effect on QNX  
* QTBUG-116876 Document QElapsedTimer::Duration,  
QElapsedTimer::TimePoint  
* QTBUG-3287 Reads a '\0'-terminated string from the QDataStream  
* QTBUG-116870 Document QNativeIpcKey::QNativeIpcKey()  
* QTBUG-116872 Mark QEvent::DevicePixelRatioChange enum as new in Qt 6.6  
* QTBUG-114203 keyReleaseEvent not triggered on windows devices with  
touch display  
* QTBUG-116937 Documentation for new api missing: QSqlField::swap  
* QTBUG-116732 ld: warning: -undefined error is deprecated  
* QTBUG-116777 Package created with windeployqt gives error when exe run  
* QTBUG-115699 [REG 6.4.3-6.5] Changing the minimum size get the window  
out of maximized state  
* QTBUG-116930 Documentation for new api missing: QPalette::accent  
* QTBUG-109874 q20algorithm triggers -Werror,-Wunused-template  
* QTBUG-116064 [REG SiC 6.4 -> 6.5] qHash(qfloat16(x)) is now ambiguous  
on GCC13  
* QTBUG-116076 qHash(qfloat16(x), seed) != qHash(float(x), seed) unless  
seed == 0  
* QTBUG-116357 Build fails with -march=native  
* QTBUG-111698 Build fails with -march=amdfam10  
* QTBUG-107072 build chooses unavailable hardware flags  
* QTBUG-116925 q(u)int128 are not documented  
* QTBUG-116929 Make a decision regarding QFont's feature API  
* QTBUG-115196 QMenubar only works once  
* QTBUG-116769 [Boot2Qt] QMenu not re-appearing after closing in widgets  
app  
* QTBUG-116973 [REG 6.5 -> dev] CMakeList: Can't rebuild after changes  
with -no-opengl  
* QTBUG-117021 ASSERT: "self.window" in file qiosviewcontroller.mm, line  
110  
* QTBUG-116903 [REG 6.5.0-6.5.2][macOS] Emoji edit menu items are not  
visible in a specific case  
* QTBUG-116756 Map DXGI_ADAPTER_FLAG_SOFTWARE to CpuDevice in  
QRhiDriverInfo  
* QTBUG-116773 Adding "Fuzzed" .otf font files causes access violation  
exception  
* QTBUG-116920 FAIL!  : tst_QGeoAreaMonitorSource::tst_monitor() 'obj !=  
nullptr' returned FALSE.  
* QTBUG-117052 Condition of feature ipc_posix erroneously evaluates to  
FALSE  
* QTBUG-116731 QtFuture::whenAll() leaks when one of the futures is  
already finished  
* QTBUG-116890 Typo in the document  
* PYSIDE-2460 QOpenGLContext is not valid when aboutToBeDestroyed is run  
* QTBUG-116821 QNativeIpcKey: UB (inactive union member used)  
* QTBUG-117097 [Windows] Sporadic crash on  
QNetworkConnectionEvents::getNetworkConnectionFromAdapterGuid()  
* QTBUG-115832 iOS: About Qt dialog displays incorrectly when launched  
from menu  
* QTBUG-116763 out-of-bounds operator+  
* QTBUG-116716 qt_add_translations: CFBundleLocalizations might not be  
added to Info.plist  
* QTBUG-75456 Streaming XMLs from reader to writer changes namespace  
name  
* QTBUG-116349 Doc: Documentation of qAsConst missing  
* QTBUG-116752 Floatable non-closable dock widget can be closed when  
floating, but cannot be reopened  
* QTBUG-117215 "A minimal RSS listing application" example has wrong  
metadata  
* QTBUG-117053 NOT ( x AND y ) feature condition incorrectly evaluated  
* QTBUG-117200 Reg -> 6.6b4: Exit warning :"QItemSelectionModel:  
Selecting when no model has been set will result in a no-op" from apps  
with  sort proxy filter model  
* QTBUG-117109 QBindable example fails to configure  
* QTBUG-117204 using debug_script ends in type error  
* QTBUG-117383 QFile::moveToTrash does nothing but returns true  
* QTBUG-117412 Vulkan instance validation error on Raspberry Pi 4  
* QTBUG-117416 RPi4 with Vulkan: choosing the output screen does not  
work  
* QTBUG-116926 Table view delegate(derived from QStyledItemDelegate) can  
not get new value when Spinbox loses focus and  
spinbox->setKeyboardTracking(false)  
* QTBUG-115486 Item view headers with stylesheets include space for sort  
indicator on all sections  
* QTBUG-117483 QWeakPointer's converting move constructor is not  
threadsafe  
* QTBUG-117482 should be "external" instead of  'exernal'  
* QTBUG-109465 [REG: 5.15 → 6.2] binding doesn't update when it should  
* QTBUG-115161 Crash in QAccessibleComboBox::focusChild()  
* QTBUG-117509 Examples that set OUTPUT_NAME will not build for Android  
* QTBUG-117518 syncqt: qt_sync_skip_header_check header not skipped  
* QTBUG-117644 Orca screen reader doesn't announce combobox value when  
focused  
* QTBUG-117674 [Reg 5.15->6.x] CONFIG += qt causes failure to link to  
WinMain  
* QTBUG-107598 HorizontalHeaderView crashes the app if it's synced to  
model changed from bg thread  
* QTBUG-109718 QWebSocket cannot handle HTTP 407 response ("Proxy  
Authentication Required")  
* QTBUG-102196 QDockWidget: wrong mouse cursor icon used when dock  
widget floating, has custom title bar & contains window container  
* QTBUG-115233 OpenSSL-3 QCryptographicHash leaks  
OSSL_PROVIDER_load()'ed objects  
* QTBUG-89904 Possible error in Qt 6 "Container Classes" documentation  
* QTBUG-114437 REG: Android: Layout in display cut mode being overridden  
to short edges always  
* QTBUG-96877 Qt6 won't render into cutout area (regression)  
* QTBUG-117745 Warning message from app compiled with XCode 15  
* QTBUG-94250 tst_QListView::internalDragDropMove fails with OpenSUSE  
15.3 and RHEL 9  
* QTBUG-117817 Windeployqt --qpaths  
* QTBUG-117787 Cached network requests leak memory  
* QTBUG-117705 Incorrect documentation for QStringEncoder and  
QStringDecoder  
* QTBUG-117764 [REG 6.5.1->6.5.2] Setting a DockWidget title when the  
DockWidget is closed causes windowTitle to be null or desync  
* QTBUG-117820 xcb: Adding and removing devices while the application is  
running may spam the application output with unregistered device  
messages  
* QTBUG-117473 crash occuring at shutdown  
* QTBUG-113486 Inactive components not correcly rendered in dark-mode  
environments in Qt 6.5.0  
* QTBUG-117740  Insufficient qreal validation in  
./src/gui/painting/qpdf.cpp produces broken PDF with large coordinates  
* QTBUG-117779 [Reg 6.5.3->6.5.2] Showing a secondary Window is broken:  
the second Window unexpectedly depends on the main Window position  
* QTBUG-86297 Qt does not handle the ACTION_POINTER_UP  event on android  
* QTBUG-117459 windeployqt: Explicitly disabled plugins are still  
deployed  
* QTBUG-109025 High DPI scaling breaks Mouse/Stylus on Android  
* QTBUG-117950 qxkbcommon.cpp:242:16: error: 'XKB_KEY_dead_lowline' was  
not declared in this scope  
* QTBUG-117870 icx on windows has an issue with int128 6.6.0 rc  
* QTBUG-117153 lastest commit for QLoggingCategory trigger compile error  
in other impotant project  
* QTBUG-116221 QShortcut does not work with QWindow  
* QTBUG-112879 [QT6.5] gtk3 theme glitches when moving the window  
* QTBUG-117514 QFuture::then marked as private  
* QTBUG-117621 Reg->6.7: QSqlDatabase::drivers() requires a  
QCoreApplication to work  
* QTBUG-116826 Windows inactive accent colour changes when window loses  
focus  
* QTBUG-117490 QNetworkInformation:loadBackendByFeatures(QNetworkInforma  
tion::Feature::Reachability) doesn't work in snap  
* QTBUG-117904 QProgressBar High-DPI issues  
* QTBUG-118041 selftests don't appear to respect ASAN_OPTIONS  
environment variable  
* QTBUG-116167 Duplicate requests of QNetworkAccessManager do not work  
* QTBUG-115446 qcocoanativeinterface.mm:4:10: fatal error:  
'QtGui/private/qopenglcontext_p.h' file not found  
* QTBUG-117709 Protobuf CMakefiles don't work when protobuf libraries  
aren't installed  
* QTBUG-96371 QAction doesn't work with cyrillic keyboard  layout  
* QTBUG-79493 Mac: QML Shortcut with StandardKey.Copy sequence is not  
activated in russian (any non-latin?) locale  
* QTBUG-117242 QtStartUpFunction is written as QtCleanUpFunction  
* QTBUG-118075 macdeployqt does not sign any libraries when the  
-exectuable parameter is used  
* QTBUG-115992 Window containing native windows window is excessively  
repainted on move  
* QTBUG-117606 QLineEdit loses its frames when hovering  
* QTBUG-118117 [REG 6.4.3->6.5.3] Opening a modeless QDialog removes a  
previously set taskbar icon overlay from native API on Windows 11  
* QTBUG-117905  Imported target "WrapHarfbuzz::WrapHarfbuzz" includes  
non-existent path  
* QTBUG-108323 qt-cmake.bat configures invalid compiler  
* QTBUG-118192 QNetworkAccessManager hang with low integrity level (low  
IL) sandboxing  
* QTBUG-5903 When a QCOMPARE of two lengthy values fails, the debugging  
output is incomplete  
* QTBUG-115241 Android Deploy Qt tool does not copy templates and  
libc++_shared library in aux mode  
* QTBUG-118170 QRhi static constants causing missing symbols  
* QTBUG-118229 QNetworkDatagram destructor uses private API  
* QTBUG-118199 Flaky tst_QEventLoop::processEvents on QNX  
* QTBUG-117804 Incomplete JPEG writing after libjpeg-turbo 3.0.0 upgrade  
* QTBUG-118220 tst_qrhi (Failed) on Android 14 emulator when running  
within a CI VM  
* QTBUG-105034 QDataStream cannot serialize containers > 2Gi elements  
* QTBUG-80417 QDateTimeEdit cannot handle OffsetFromUTC or TimeZone as  
time-spec  
* QTBUG-117367 [Reg 5.15 ->6.x] Android: Unable to dismiss "teardrop"  
cursor from text inputs  
* QTBUG-118419 [Reg 6.4->6.5] Cannot create button with menu in message  
box  
* QTBUG-118320 [Reg 6.4.3->6.5] Application window not active after  
closing message box  
* QTBUG-104905 Window modal not blocking ancestor window interaction on  
Mac  
* QTBUG-118462 Qt6Core_INCLUDE_DIRS cmake variable contains suspicious  
stuff on Windows  
* QTBUG-106527 AT-SPI2: Incorrect sizes returned for WINDOW and PARENT  
coordinates  
* QTBUG-118308 [Reg 6.4->6.5] QMessageBox::set(Default|Escape)Button  
does not work  
* QTBUG-117713 [REG: 5->6] Scaling images with Qt::SmoothTransformation  
breaks them if scaled to smaller than 50% size  
* QTBUG-118135 VxWorks error: use of undeclared identifier 'PN_XNUM'  
* QTBUG-118191 iOS LaunchScreen DarkMode support  
* QTBUG-117997 WASM: generated index.html lacks exit code details  
* QTBUG-118244 QVulkanWindow::grab() assumes RGBA which leads to  
inverted R and B channels  
* QTBUG-118234 tst_qvulkan (Failed) on Android 14  
* QTBUG-118586 QTimeZone::isTimeZoneIdAvailable is giving wrong result.  
* QTBUG-118315 Misleading documentation of QWaylandApplication  
* QTBUG-118221 QDate construction from std chrono types is inefficient  
* QTBUG-118318 QStringConverter/Win doesn't handle resumption for  
encodings with more than 2 octets per character for convertToUnicode  
* QTBUG-117428 [Reg 6.4->6.5] QWizard does not draw the buttons  
* QTBUG-117910 [windeployqt] The QtPDF module will always be deployed if  
it's installed  
* QTBUG-118553 Incorrect composition when place a software-rendered  
widget over a OpenGL-based widget  
* QTBUG-118612 Large size cursor overlaps tooltips on linux  
* QTBUG-115005 [Android] Text cursor handle visible out of the TextEdit  
clip region  
* QTBUG-118649 tst_QGlyphRun fails with Linux on ARM  
* QTBUG-111855 QSharedMemory no longer works using the old constructor  
after recent changes in dev  
* QTBUG-117533 QProcess does not work with thread sanitizer  
* QTBUG-114971 QAndroidBinder: implementation for native methods missing  
* QTBUG-118070 When configuring with debug info, installed libraries  
shoudn't be stripped  
* QTBUG-118703 Crash (divison by zero) in  
QLocaleData::applyIntegerFormatting()  
* QTBUG-118643 REG->6.7 : Fusion style QDockWidget buttons are too large  
* QTBUG-118122 QCommonStyle::standardIcon/Pixmap does not use the  
correct icons for high-dpi  
* QTBUG-117966 QVulkanWindow::setEnabledFeaturesModifier does not allow  
to enable device features other than Vulkan 1.0 features  
* QTBUG-118741 Windows: QNetworkInformation does not report "metered"  
feaature  
* QTBUG-116550 [schannel] Qt warning "QIODevice::write (QTcpSocket):  
device not open"  
* QTBUG-118227 QCryptographicHash broken with OpenSSL 3 (feature  
"openssl_hash")  
* QTBUG-118194 Adding QOpenGLWidget to FullScreen window breaks Full  
Screen  
* QTBUG-118759 [Regr:6.5->6.6] QDateTime comparison performance  
regression on macOS  
* QTBUG-118627 Build error for QNX, incomplete type QQnxWindowMapper  
* QTBUG-118851 qtbase: LTO disabled with GCC  
* QTBUG-118716 [REG: 6.5 -> 6.6] windows: Cyclical QCheckBox setChecked  
leads to stack overflow  
* QTBUG-106262 Mouse events use rounded float local pos  
* QTBUG-118667 QIcon::addFile() with an invalid filename results in  
QFile::isNull() == false  
* QTBUG-111952 tslib input plugin broken  
* QTBUG-113307 tslib input not working  
* QTBUG-93368 Windows: QGuiApplication::primaryScreenChanged is not  
emitted when changing primary screen  
* QTBUG-116295 Qt build with SSL3, is not picking up SSL3  
* QTBUG-118899 REG: QPrintDialog no longer opens on Windows  
* QTBUG-116013 QHeaderView::resetDefaultSectionSize doesn't invalidate  
cached size hints / update view  
* QTBUG-118695 popup menu on QToolButton displays at wrong screen  
* QTBUG-118814 [OpenSSL 3.0] QCryptographicHash::Keccak_256 produces the  
same output as Sha3_256  
* QTBUG-118631 QBitArray::testBit with unsigned enum fails to build with  
gcc13  
* QTBUG-117499 Mouse scroll events stop working with `-platform  
windows:reverse`  
* QTBUG-28463 Unable to use Arabic right to left (RTL) layout in the  
title bar of own custom dialog.  
* QTBUG-117494 QSvgRenderer produces different results randomly when it  
is run the same way  many times  
* QTBUG-118580 QPrinter::setPageLayout does behaves different on windows  
and Linux  
* QTBUG-118912 [example hellovulkancubes] crash on addNew()  
* QTBUG-118986 [Crash] The hellovulkancubes example app is crashing when  
tapping Add New button on Android  
* QTBUG-101219 Hidden tabs via QTabWidget::setTabVisible are still  
available  
* QTBUG-117206 QT_ANDROID_EXTRA_LIBS ignored for secondary ABIs  
* QTBUG-118992 Reg6.4->6.5 QMessageBox Hide/Show detailed section is  
gone  
* QTBUG-118993 MSVC warns as error on stdext::checked_array_iterator in  
QtCore/qvector.h  
* QTBUG-118870 Icon of a cell with a background color disappears if a  
stylesheet is used for QTreeView::indicator  
* QTBUG-114075 PrivateApi in QtActivityLoader  
* QTBUG-117900 [REG 5.15.2->6.5.1] Behavioural inconsistency when  
reparenting QStandardItems  
* QTBUG-89145 QStandardItemModel takeItem / takeChild does not emit the  
right signals  
* QTBUG-116532 tst_QStandardItemModel leaks memory in multiple test  
cases  
* QTBUG-119053 macOS: QSystemTrayIcon::activated signal slot is called  
multiple times if QSystemTrayIcon::setContextMenu is called from it  
* QTBUG-119068 QSystemTrayIcon - unable to reset context menu  
* QTBUG-104641 QDial: division by zero while changing minimal or maximum  
value  
* QTBUG-117111 QProperty's documentation has a Note section which seems  
to be displayed in an unintended way  
* QTBUG-78737 Windows: Two menus instead of one appear by clicking on  
the QSystemTrayIcon  
* QTBUG-119044 CXXFLAGS='-D_GLIBCXX_DEBUG' build crashes (e.g. in  
sharedmemory example)  
* QTBUG-118133 Windows QPA:  QSystemIconTrayIcon::show() not working  
after calling hide()  
* QTBUG-105150 QStandardItem is using un-documented value of  
Qt::ItemDataRole  
* QTBUG-111527 SEGFAULT in QGuiApplication ctor after setting  
DesktopSettingsAware to false  
* QTBUG-113507 macOS: Popups opening on wrong screen  
* QTBUG-118106 a11y: Strikethrough not reported as AT-SPI text attribute  
* QTBUG-102831 QCompleter's suggestion list hides native Chinese Input  
method  
* QTBUG-118458 TLS Invalid Token  
* QTBUG-41696 QApplication::widgetAt() doesn't work with widgets with  
Qt::WA_TransparentForMouseEvents on Mac  
* QTBUG-119092 [REG: 6.5.2->6.5.3] macOS: topLevelAt/widgetAt cannot  
find something under a window with setIgnoresMouseEvents set  
* PYSIDE-2525 Segfaults related to QMenu on macOS  
* QTBUG-119007 Android: QtDisplayManager.onDisplayChanged() can lead to  
a null pointer exception  
* QTBUG-119134 Rotating the Android device causes any Qt application to  
crash  
* QTBUG-105395 WM_TRANSIENT_FOR is not kept in sync  
* QTBUG-104602 QTabWidget does not set the selected state on AT-SPI2  
* QTBUG-116400 Fusion style Scrollbar cutoff  
* QTBUG-112479 Touch Drag doesn't cause mousePressEvent after Touch  
Press  
* QTBUG-119032 Mouse Release is not fired with touch screen  
* QTBUG-100688 TapHandler doesn't emit  onDoubleTapped when using a  
touchscreen  
* QTBUG-114188 QMdiArea::TabbedView not honored with single subwindow  
* QTBUG-117762 "The cached device pixel ratio value was stale on window  
expose" when closing window on Wayland  
* QTBUG-118223 QDockWidget generates leftover containers + crash  
* QTBUG-99136 QDockWidget not correctly parented/setup if dragged from  
another floating and tabified QDockWidget  
* QTBUG-118578 Undocking tabbed widget from floating window creates  
empty redundant window  
* QTBUG-118579 Undocking tabbed widget from main window onto the  
floating window crashes app  
* QTBUG-56799 [QDockWidget - Crash] Double Clicking to re-parent docks  
can cause a crash.  
* QTBUG-35736 "Index out of range" situation in QMainWindowLayout class  
* QTBUG-63448 Undocking window does not send topLevelChanged signal  
* QTBUG-88329 Delete a QDockWidget while drag in progress causes crash  
* QTBUG-88157 tabPosition called with out-of-bounds when closing an  
undocked QDockWidget  
* QTBUG-94097 creating QDockWidget after application startup prevents  
correct termination on Ubuntu  
* QTBUG-44540 QDockAreaLayoutInfo crashes in restoreState (l. 1978-9)  
when restoring closed, floating QDockWidget  
* QTBUG-53808 QDockWidget losing decoration on undocking when  
GroupedDragging is enabled  
* QTBUG-72915 QDockWidget doesn't properly dock anymore after it was  
undocked (regression)  
* QTBUG-53438 QMainWindow: tabbed QDockWidgets leave invisible QTabBar  
* QTBUG-119219 macOS: NPE in QNSWindow applicationActivationChanged  
* QTBUG-64373 QPushButton with RightToLeft layoutDirection and an icon  
crops text in Fusion style  
* QTBUG-98525 QTreeView inline text editor doesn't not sized properly  
* QTBUG-118225 QtQuick Loader doesn't load over http(s)  
* QTBUG-118605 CTRL+Tab don't work in combobox  
* QTBUG-119366 QTabBar is incorrectly offset when changing the  
TabPosition  
* QTBUG-115156 Last character missing with JAWS  
* QTBUG-106695 QScroller doesn't send mouse press events if on primary  
display  
* QTBUG-111787 devicePixelRatio / zoom rescale error  
* QTBUG-111528 Android font does not depend on locale/OS preference but  
is hardcoded  
* QTBUG-117765 moc chokes on <concepts> from xcode13  
* QTBUG-22424 Inappropriate use of #if 0 in QStaticText autotest  
* QTBUG-114539 QToolButton arrow clipped on screen with non-integer  
device pixel ratio  
* QTBUG-119338 Objective-C usage can result in undefined behavior (part  
2)  
* QTBUG-87334 Graphical issue on some Android smartphones: white line at  
the top and the right side of the screen  
* QTBUG-119239 Incorrect reading of Plain PBM images  
* QTBUG-118416 [wasm] Signal from another thread is discarded while the  
thread is temporarily blocking  
* QTBUG-106928 QObject: Cannot create children for a parent that is in a  
different thread when exiting Android app  
* QTBUG-118421 TextField logs "Cannot create children for a parent that  
is in a different thread" when closing virtual keyboard  
* QTBUG-88508 some tests are not saving result output to file on Android  
* QTBUG-114253 [REG: 5.11->6] Performance issue with loading images in  
static build  
* QTBUG-34550 QDBusObjectPath property is sometimes ignored by  
qdbuscpp2xml  
* QTBUG-119306 drawPoints and drawPolygon don't match  
* QTBUG-119424 windows: Too long tooltip crashes  
* QTBUG-119511 windeployqt -v has no effect  
* QTBUG-18525 Registering object with no parent crashes Qt  
* QTBUG-115298 Androidtestrunner freezes after obtaining SDK version  
* QTBUG-106479 androidtestrunner does not honour QTEST_FUNCTION_TIMEOUT  
* QTBUG-119517 Segfault in tst_qquickmaterialstyle  
Material::test_background:drawer  
* QTBUG-118907 Not correct QDataStream version  
* QTBUG-69919 Large D-Bus messages sometimes trigger assertion failure  
in qDBusToggleWatch  
* QTBUG-119602 PainterPaths-Graphic&Multimedia-Example typo in the  
documentation  
* QTBUG-116898 Change deprecation information for  
QtFuture::makeReadyFuture  
* QTBUG-119499 Document QMessageAuthenticationCode  using HMAC  
* QTBUG-118568 qvulkanwindow  repeatedly recreate swapchain  
* QTBUG-24318 tst_QApplication::testDeleteLater() fails on Mac OS X  
* QTBUG-119430 Top flaky test: tst_android::orientationChange on  
Android_ANY X86_64.  
* QTBUG-94459 Android reports incorrect screen size after rotation  
* QTBUG-119464 QSslSocket::setCiphers() documentation uses weak cyphers  
* QTBUG-119148 layer.samples value not clipped in Qt6  
* QTBUG-119444 [REG 6.5.1 -> 6.5.2] QOpenGLWidget with  
QT_WIDGETS_HIGHDPI_DOWNSCALE uses nearest filter  
* QTBUG-116350 Fix documentation to refer to QNtfsPermissionCheckGuard  
instead of qt_ntfs_permission_lookup  
* QTBUG-119792 Objects of target "lib1" referenced but is not one of the  
allowed target   types (EXECUTABLE, SHARED, MODULE)  
* QTBUG-114849 Big icons in QTabWidget are badly aligned (regression  
from Qt5 to Qt6)  
* QTBUG-34613 QDBusConnection::connectToBus fails dbus API check when  
q_dbus_bus_register fails  
* QTBUG-101404 wasm: mobile keyboard keeps popping on on android  
* QTBUG-116262 QRestAccessManager custom method request support  
* QTBUG-117637 qfloat16 comparison with integral types is ambiguous  
* QTBUG-119650 Model adapter/replica incompatible across different Qt  
versions and platforms  
* QTBUG-72916 QKeySequence::keyBindings() for StandardKey(SaveAs) do not  
return any key sequences  
* QTBUG-119526 [Reg 6.6.0->6.6.1]QCocoaAccessibility Crash with Mac  
VoiceOver enabled  
* QTBUG-118585 "Crash" in QMacAccessibilityElement initWithId:role:  
* QTBUG-119797 [Reg 6.5.3 -> 6.6.1]QFileIconProvider.icon of a file only  
give general file icon  
* QTBUG-119371 [macOS] (File|Folder)Dialog.currentFolder holds stale  
data  
* QTBUG-118800 Programmatically selecting item view item breaks a11y  
focus  
* QTBUG-119881 Windows ARM qtbase fails with unresolved external symbol  
asm referenced in function tst_qYieldCpu  
* QTBUG-119054 Mac: Focus issues when embedding into non-Qt apps  
* QTBUG-119155 [REG: 6.5.2->6.5.3] headerDataChanged is now queued and  
parameters may be out of sync  
* QTBUG-120025 The QMainWindowLayout::restoreState causes a crash  
* QTBUG-118642 [Reg6.4->6.5]WebAssembly - QML - failing to use Noto  
Color Emoji font  
* QTBUG-49720 Documentation for QFileDialog::DontConfirmOverwrite should  
mention QFileDialog::AcceptMode  
* QTBUG-18057 QPixmap::toWinHBITMAP(): 2 Bugs when running out of memory  
(Access violation or lost HBITMAP handle)  
* QTBUG-119406 QFuture::then() with context object deadlocks  
* QTBUG-119103 QFuture hangs when continuation uses a context object and  
is resolved from the same thread  
* QTBUG-117918 Debug builds with QFuture::waitForFinished and same-  
thread continuations may deadlock  
* QTBUG-119579 [Reg 6.5 -> 6.6] Calling QPromise::finish() from the same  
thread deadlocks i  
* QTBUG-119810 QFuture continuation with deleted context  
* QTBUG-119309 Qt fails to flush to Mac native sub window when tlw is  
RHI  
* QTBUG-120050 Configuring a CMake-based Qt WASM project fails if emsdk  
path has spaces  
* QTBUG-115260 Hang during drag and drop [REG]  
* QTBUG-120036 DFEATURE_libjpeg CMake option not working  
* QTBUG-120006 DeleteStartOfWord with a selection in QLineEdit has  
unexpected behavior  
* QTBUG-119225 [Reg 6.2 -> 6.5] QSplashScreen no longer shows on Linux  
with a single call to QCoreApplication::processEvents()  
* QTBUG-120054 Reg6.4->6.5 Stylesheet has no Effect on QMessageBox  
* QTBUG-119972 Clang-tidy reports possible memory leak with  
QMetaObject::invokeMethod  
* QTBUG-119995 QML - Text - Font weight - macOS/Windows difference  
* QTBUG-119902 Crash in QImage::scaled  
* QTBUG-117903 WM_CHAR creates unwanted keyboard event - activating  
shortcut  
* QTBUG-115765 QAbstractItemView::EditingState: state stale when editing  
with a proxy model  
* QTBUG-92016 High DPI, bad SVG quality, wrong screen selected for  
current window  
* QTBUG-94203 Icon drawing bug of  StyleSheetStyle in a mixed-dpi  
environment  
* QTBUG-110266 affine example crashes when moving the center hoverpoint  
* QTBUG-119167 Atspi.Table.get_row_column_extents_at_index can cause  
segfault in tree  
* QTBUG-119708 VS2022 simple program fails to link in Release mode with  
ProtobufWellKnownTypes  
* QTBUG-119752 Customized QToolTip with padding or margin displays  
incorrectly  
* QTBUG-112920 FTBFS qt 6.5.0 on gcc 9  
* QTBUG-120062 Non-native QFileDialog gets frozen on destruction if  
remote mapped drive is disconnected  
* QTBUG-47159 QFileDialog::selectFile does not keep native separators  
* QTBUG-120055 When dragging QTableView columns scrolling behaves oddly  
* QTBUG-120141 cmake build of a Qt project with static Qt linkage fails  
due to error in qtbase/cmake/FindWrapResolv.cmake  
* QTBUG-119619 CMake deploy script finds x64 libraries for WoA  
application.  
* QTBUG-117704 Dragging Window handling WM_NCCALCSIZE and WM_NCHITTEST  
squishes contents  
* QTBUG-120121 a11y QComboBox: Problematic signal/slot activation order  
* QTBUG-120125 CMake subarch extraction does not always succeed  
* QTBUG-116989 wasm:  pen pointerhandler example does not work as  
expected  
* QTBUG-120257 widgets/itemviews/editabletreemodel not compiling on  
Android  
* QTBUG-120167 Reg->6.7: QComboxbox hover is broken  
* QTBUG-50403 QDrag conflict with hover of widgets  
* QTBUG-120012 Limiting maximum allocation size for QDataStream  
* QTBUG-119178 Crash after registering an invalid resource file  
* QTBUG-113865 [Text Editor]Using undo function causes the app to crash  
* QTBUG-120107 PDF view gets render mistakes on Android 10  
* QTCREATORBUG-30117 Help viewer: "[read-only]" tags have unreadably low  
contrast in dark mode  
* QTBUG-119113 windows: Stack overflow when dragging to/from embedded  
native window  
* QTBUG-120309 Public ABI break in 6.7 beta 1  
* QTBUG-119808 [REG 6.1 -> 6.6] QPlainTextEdit: Placeholder is not  
hidden on input  
* QTBUG-52622 Not highdpi icons in standart message dialogs  
* QTBUG-120379 The `QStringLiterals` header is lost  
* QTBUG-120327 Pen PointerEvents not handled in WebAssembly (fix  
attached)  
* QTBUG-118161 QFileDialog::getOpenFileContent not working in sometimes  
* QTBUG-22544 tst_qmdisubwindow::setFont() autotest is unstable  
* QTBUG-67708 QGroupBox title does not follow vertical alignment with  
fusion style  
* QTBUG-120624 UB when passing null string to QString::arg()  
* QTBUG-103825 Wrong resolution of Icon in Windows (Toast) Notifications  
* QTBUG-120548 QSqlQuery::positionalBindingEnabled improvements  
* QTBUG-120302 AddressSanitizer: heap-use-after-free in  
tst_QFuture::continuationsWithContext()  
* QTBUG-120335 On certain machines QtConcurrent crashes if no free  
threads on thread pool  
* QTBUG-119501 Numbers colliding and not highlighted in Charts with  
Widgets Gallery example  
* QTBUG-120614 QImage::convertToFormat: wrong conversion from RGBA64 to  
RGBA16FPx4  
* QTBUG-120574 QComboBox popup high decreases when hiding view items  
* QTBUG-83604 QSlider with ticks is glitchy with QFusionStyle  
* QTBUG-120762 Use after free  
* QTBUG-111314 Adding padding to QSlider does not work on Fusion style  
* QTBUG-120758 qtdeclarative fails to build with conan 2 on windows:  
include path too long  
* QTBUG-120572 [QDoc] Redundant text in QTabBar detailed description  
* QTBUG-120297 Q_GADGET forces following elements to be private  
* QTBUG-117954 QProcess::startDetached quits application when running  
with ASAN  
* QTBUG-104493 Application performance drops if many threads are running  
while QProcess creates sub-processes on Unix  
* QTBUG-120332 [REG 6.6.1 -> 6.7] rendering svg causes division by zero  
in getRadialGradientValues  
* QTBUG-120474 4xMSAA doesn't work with Mali400 using Lima driver  
* QTBUG-120350 QOffScreenSurface::isValid always returns false on  
WebAssembly  
* QTBUG-120766 qstorageinfo.cpp compile error 6.7.0-beta1  
* QTBUG-118503 WASM: arrow keys and select-all not working for  
QPlainTextEdit on touchscreen  
* QTBUG-120687 6.7/API review: QIcon theme API clashes with <windows.h>  
* QTBUG-58005 ibus: commit does not properly reset the preedit string  
* QTBUG-120487 Symlinks generated in user_facing_tool_links.txt during  
configuration are incorrect for MacOS  
* QTBUG-120748 Win11 Style: QMessageBox text invisible when using dark  
theme on Windows  
* QTBUG-120732 Qimagereader manual test - Image file is missing  
* QTBUG-121041 Fusion style: add clip region for groupbox title  
* QTBUG-121030 QIconLoader failed to find icon in hicolor  
* QTBUG-121015 tst_QGuiApplication::topLevelAt() failed on Wayland  
* QTBUG-120485 QT_INSTALL_DOCS configured with wrong path  
* QTBUG-118867 Render thread can delete font engines still in use  
* QTBUG-121135 QNetworkRequest::setTransferTimeout linkage on MinGW  
* QTBUG-120619 QHttpServer with QtConcurrent blocks until the very first  
request has finished before being able to process in parallel  
* QTBUG-119248 The result of calling serviceUUID is different in Q5 and  
Qt6  
* QTBUG-120961 QLocale::monthName() doesn't work correctly on Windows  
* QTBUG-120909 Improve SQL Browser Example - Coding style  
* QTBUG-120577 qt6.5.3 QTextEdit can't display image ! but qt5.15 is ok  
。  
* QTBUG-120968 QProcess::start(): Fix docs about Starting state on  
Windows  
* QTCREATORBUG-30066 Git commands fail on windows when using the  
QProcess backend  
* QTBUG-121140 [REG 6.6 → 6.7] QStorageInfo isn't functional for btrfs  
setups  
* QTBUG-121204 ~unique_ptr() static assertion failure due to incomplete  
type T (C++23)  
* QTBUG-120976 REG: QPushButton of a menu will still appear pressed even  
after you click somewhere outside the button area.  
* QTBUG-121232 tst_QQuickWebView crash  
* QTBUG-121183 [QMYSQL] The mysql_list_fields() was removed in MySQL  
v8.3  
* QTBUG-120962 QTextCursor::removeSelectedText leads to crash  
* QTBUG-120509 Crash when Qt re-create native windows if  
WA_DontCreateNativeAncestors is set  
* QTBUG-120436 sqldrivers always build in release  
* QTBUG-114941 Qt 6.6 Beta 1 and Qt Creator 11.0.0-beta2 - Test  
permissions - Bluetooth fails on Android 14  
* QTBUG-120317 qt6<target_name>_debug_metatypes.json: illegal value  
* QTBUG-121472 qmltyperegistrar.exe fails to parse metatypes.json file  
* QTBUG-121498 tst_QAbstractItemView::removeIndexWhileEditing() failed  
on Wayland  
* QTBUG-120469 Crash in QCocoaSystemTrayIcon::emitActivated() when  
calling QComboBox clear() then addItem()  
* QTBUG-121008 Crash in QMacAccessibilityElement when using  
QTreeView/QCombobox  
* QTBUG-121515 [Reg 6.6.1 -> 6.6.2] QNetworkAccessManager never finishes  
request if server sends status code 401 without a challenge  
* QTBUG-120264 Inactive radio buttons partially respond to click  
* QTBUG-118238 【Windows】stack overflow after launch Any Qt Application  
(or Official Demo)  
* QTBUG-121040 [Reg 5.1 -> 5.15 and all 6.*] QTextDocumentation does not  
handle background of HTML string correctly  
* QTBUG-115989 Shadowed Q_PROPERTY with non-empty params NOTIFY breaks  
compilation  
* QTBUG-74471 QFileSystemModel shows directories with  
setFilter(QDir::Files)  
* QTBUG-115459 Possible infinite loop triggered by unmaximizing the  
window in 6.5.0+  
* QTBUG-118489 Can't tab to last button in QDialogButtonBox  
* QTBUG-111994 Deal with a font face at index 0 as Regular for Variable  
fonts  
* QTBUG-112136 Unable to pick up styles properly from Variable fonts  
* QTBUG-121729 error: Multiple commands produce same *_metatypes.json  
* QTBUG-119532 Starting Android app fails with AST  
* QTBUG-120907 FE_INVALID in tst_QPainter::fpe_radialGradients()  
* QTBUG-121557 [Reg 6.4.3->6.6] Application unusable after closing  
nested message boxes  
* QTBUG-121713 QXkbCommon::keysymToQtKey does not map XF86Calculator  
* QTBUG-117429 TIFF AnimatedImage memory leak  
* QTBUG-120633 REG->6.7: Windows11/Vista palette issues (bright)  
* QTBUG-121485 QLocale method nativeCountryName returns wrong values.  
* QTBUG-120369 iOS: Crash after changing screen orientation  
* QTBUG-120530 QDomDocument doc refers to QXmlQuery which doesn't exist  
in Qt6  
* QTBUG-109073 [REG] Memory leak in QJsonObject  
* QTBUG-99178 QFileSystemModel should have an option to disable icon  
loading; crashes if the icon provider is null  
* QTBUG-121873 The description and the snippet don't match in  
QDBusAbstractInterface::asyncCall  
* QTBUG-121697 Critical crash when creating QPlainTextEdit when using  
styles/stylesheets.  
* QTBUG-121790 QApplication::setStyleSheet crashes QTextEdit  
* QTBUG-108068 QNetworkAccessManager should handle all informational  
HTTP replies  
* QTBUG-121667 Qt Notifier app is crashing immediately after being  
launched for the first time after deployment  
* QTBUG-121668 Qt Notifier example - notifications do not work on  
Android 13  
* QTBUG-121947 qDebug() output is missing newline on Windows  
* QTBUG-121948 RCC compression is broken when deploying to Android from  
a Linux host using CMake  
* QTBUG-106466 build android app with Debian host fails on undefined  
symbol qt_resourceFeatureZstd  
* QTBUG-101353 AUTORCC uses zstd even if Qt is build without rcc support  
* QTBUG-103476 Custom`Delegate::destroyEditor()` is not called for some  
editor when removing a tree branch  
* QTBUG-122054 Massive performance loss of QTreeView::expandAll  
* QTBUG-121875 Typo in the document  
* QTBUG-120688 Explicitly document behavior for QFileInfo if file is  
directory  
* QTBUG-85425 Fusion style adds unneeded space for QGroupBoxes without a  
title on Linux  
* QTBUG-95472 CLONE - Fusion style adds unneeded space for QGroupBoxes  
without a title  
* QTBUG-119795 Adding QOpenGLWidget to a QDialog in a maximized  
QMainWindow maximizes the QDialog  
* QTBUG-120316 Cannot close window after hiding and showing again  
* QTBUG-73021 Regression: [5.11.0 -> 5.11.1] QGLWidget paintEvent is not  
called if a QGLWidget is contained in a dialog that is closed and then  
reopened  
* QTBUG-122210 [REG 6.6.1->6.6.2] widgets/itemviews/editabletreemodel  
not compiling on iOS  
* QTBUG-122200 Header files are not being copied into the Qt* frameworks  
in custom build  
* QTBUG-119447 RHI - QRhiResourceUpdateBatch::readBackBuffer() fails to  
read compute buffer on Metal  
* QTBUG-122087 QTimer::isActive returns true if interval is Invalid  
* QTBUG-116927 markdown writer omits trailing ** if a bold span exceeds  
the wrap limit  
* QTBUG-106526 markdown writer should never wrap headings, but wraps  
them if they are too long  
* QTBUG-121881 QT_DEPLOY_QML_DIR: Custom value causes empty "qml" folder  
to be created  
* QTBUG-121880 QT_DEPLOY_TRANSLATIONS_DIR is ignored  
* QTBUG-121764 [Reg 6.6->6.7] Funny theme icon  
* QTBUG-122139 DirectWrite's default hinting looks off  
* QTBUG-122167 REG: Kerning errors with DirectWrite font backend  
* QTBUG-122266 property "AUTORCC_OPTIONS" is not allowed  
* QTBUG-114608 Programmatically setting focus does not move VoiceOver  
* QTBUG-122254 Documentation example of  
QCborStreamReader::readString()/QCborStreamReader::readByteArray is  
wrong  
* QTBUG-122214 REG->6.7: Windows 11,Linux: Dock icons blurry (w/o High  
DPI scaling (all styles)  
* QTBUG-122272 Some buttons from QStyle::StandardPixmap have artifacts  
in the background in the dark mode  
* QTBUG-119864 QPushButton or QToolButton does not receive mouse events  
after calling setMenu().  
* QTBUG-121906 Copyright year in so files not updated to 2024  
* QTBUG-121928 Remove Copyright year from About Qt & command line tools  
* QTBUG-122138 QTzTimeZoneCache::findEntry() parses files while holding  
QTzTimeZoneCache::m_mutex  
* QTBUG-122192 CONFIG *= silent fails at linking  
* QTBUG-122398 6.7/Windows 11/Modern style: Crash with  
QGraphicsProxyWidget  
* QTBUG-121380 No info after setting the QT_LOGGING_DEBUG env var  
* QTBUG-122451 Floating point in raster drawBitmap together with strict  
QImage::scanLine causes assertion "i >= 0 && i < height()"  
* QTBUG-110686 wasm: declarative apps on Android appear black  
* QTBUG-122648 Crash when moving application to background and bring it  
back  
* QTBUG-122622 configure on Windows can't handle unquoted -DFOO=0  
arguments  
* QTBUG-113255 QML view doesn't update properly when device is rotated  
with permission dialog.  
* QTBUG-88721 QTextDocument::find() does not work well with  
QRegularExpressions  
* QTBUG-122168 REG: Monochrome emojis with DirectWrite font backend  
* QTBUG-118983 CTest prints output from a failed test twice  
* QTBUG-121389 tst_qmessagehandler::qMessagePattern(backtrace  
depth,separator) fails on qemu-armv7-developer-build  
* QTBUG-122637 qmessagebox.h: extra ';' after member function definition  
[-Wextra-semi]  
* QTBUG-122109 QTreeWidget's columns do not seem to resize properly  
after upgrading from Qt6.5.3 to Qt6.1.1  
* QTBUG-120699 QHeaderView in QTableView doesn't restore geometry  
* QTBUG-107486 Typo in the document  
* QTBUG-122674 Build failure on x32 ABI  
* QTBUG-96348 QWindowsSystemTrayIcon::showMessage: Windows Handle leak  
* QTBUG-62945 Windows: QSystemTrayIcon::showMessage causes GDI-Object  
leak  
* QTBUG-122739 qtpaths/qmake don't honor qtconf in some cases with LTO  
enabled  
* QTBUG-122456 Support of NFC for Services when QtNative.onNewIntent()  
is private  
* QTBUG-119080 a11y: Checkbox lacks AT-SPI "checkable" state  
* QTBUG-122073 If SQL Engine does not support lastInsertId QList will  
assert  
* QTBUG-121126 Crash when restoring maximized window of application with  
tabified dock widgets  
* QTBUG-122001 QMainWindow::tabifiedDockWidgets() - Not accurate  
* QTBUG-119611 QPlainTextEdit access violation crash when inserting  
136,348,169 latin characters  
* QTBUG-120571 QGuiApplication::palette() returns incorrect values on  
Windows 11  
* QTBUG-81662 Indentation in QML RichText after list is wrong  
* QTBUG-120254 Cell value leaking into other cells when entering new  
value  
* QTBUG-122749 [Crash] WebEngine Print Me example app crashes when  
changing the page orientation  
* QTBUG-122642 The SQL QODBC driver implementation fails to escape  
passwords set with setPassword(...) when using special characters.  
* QTBUG-105871 QUdpSocket stop emitting ReadyRead signal in  
QueuedConnection  
* QTBUG-120694 QDockWidget resize issue with Qt 6.6.1  
* QTBUG-115598 tst_QWidget::render() with QtWayland failed on Ubuntu  
22.04, GNOME  
* QTBUG-40561 QDomText::splitText leaks memory  
* QTBUG-96051 markdown writer: in a table cell ending with backslash,  
it's not escaped  
* QTBUG-122083 Markdown writer fails to escape special characters  
* QTBUG-121561 Android: in TextField: cannot edit inside of words, only  
at the end [regression]  
* QTBUG-122663 Live Preview doesn't work on Boot2Qt  
* QTBUG-122720 tst_toolsupport::offsets(QFilePrivate::fileName) fails on  
x32 ABI  
* QTBUG-122687 libraries contain wrong runpath  
* QTBUG-122949 Toplevel drag only works on left monitor  
* QTBUG-122944 Dragged toplevel is re-attached even after  
wl_data_device.leave  
* QTBUG-120639 [REG 6.6.1 -> 6.7.0-beta1] Menu items too wide on 4K  
* QTBUG-123083 tst_QProcess::setChildProcessModifier fails in dev  
* QTCREATORBUG-30425 Android C++ breakpoints does not work with Qt  
Creator  
* QTBUG-123059 "package android.location.altitude does not exist" when  
building qtpositioning for Android on Linux  
* QTBUG-123286 'load_local_libs' and 'bunlded_libs' libraries in  
libs.xml are always prefixed with "lib"  
* QTBUG-122893 Sending QNetworkRequest fails on singlethreaded WASM  
* QTBUG-122747 Reparenting QTabWidget with a native window tab can cause  
crash  
* QTBUG-111514 QtCore fails to link with lld 16.0  
* QTBUG-114152 QTimer: Make timers' timeouts ordered  
* QTBUG-113371 locale and/or environment not being properly set for  
ptests  
* QTBUG-114167 A QString::prepend("data") loop never produces  
freeSpaceAtBegin().  
* QTBUG-112814 The window restore geometry is not correct  
* QTBUG-113463 Build issues with symlinks  
* QTBUG-113822 UB in QProcessPrivate::startDetached()  
* QTBUG-112896 gtk3 platformtheme returns the font of GtkFixed widget  
instead of monospace font  
* QTBUG-114243 Qt 6.5 regression with static cross-compiling for Windows  
* QTBUG-113848 Displaying \x3 to QTextEdit leads to warning and later to  
crash  
* QTBUG-114624 QKeySequenceEdit doesn't detect CTRL+SHIFT+0 on a french  
keyboard  
* QTBUG-104878 xcb wacom support gets confused about device instances  
* QTBUG-76587 wasm: keyboard mnemonics do not work correctly  
* QTBUG-113679 When the letter J is at the start of a TextField then it  
will cut off the beginning of the letter due to the negative left  
bearing  
* QTBUG-113690 Elements of QStringList property are not updatable for  
QGadgets  
* QTBUG-110025 Android tests aren't bundling OpenSSL for any test  
* QTBUG-114175 QWizard default Style not drawn correctly when scaling  
other than 100%  
* QTBUG-113233 Need a way atomically adjust QWindow minimum and maximum  
sizes  
* QTBUG-111163 [6.5] Parallel builds failing in Docker container  
* QTBUG-109792 C++ syncqt tool should be built like moc  
* QTBUG-112824 There is no way to get to the Open GL examples page from  
the Open GL Index  
* QTBUG-114997 tst_QMenu::pushButtonPopulateOnAboutToShow() with  
QtWayland failed on Ubuntu 22.04, GNOME  
* QTBUG-109776 tst_QAbstractItemView::selectionAutoScrolling() with  
QtWayland failed on Ubuntu 22.04, GNOME  
* QTBUG-106228 errors reported by "reuse lint"  
* QTBUG-112870 clang-tidy warnings on static global variables in moc  
generated code  
* QTBUG-115152 qmltyperegistrar cannot see the base class of a  
QML_ELEMENT from a different module  
* QTBUG-101926 "AutoMoc subprocess error" when building in CI  
* QTBUG-105864 a11y: AT-SPI relations FLOWS_FROM and FLOWS_TO not  
supported  
* QTBUG-115293 tst_QGraphicsItem::itemUsesExtendedStyleOption() with  
QtWayland failed on Ubuntu 22.04, GNOME  
* QTBUG-68855 Overflow in QDateTime for extreme values of QDate  
* QTBUG-111371 QIntValidator::validate() deems a trailing grouping  
character Acceptable  
* QTBUG-115447 QElapsedTimer::hasExpired should have chrono overload  
* QTBUG-104012 QDateTime constructor performance regression when year is  
below epoch  
* QTBUG-114613 QWindow::winId() crashes when QWindowPrivate::create()  
fails  
* QTBUG-83160 moc stumbles on _GLIBCXX_VISIBILITY  
* QTBUG-99555 [RE: 6.2.1->6.2.2] macdeployqt fails to produce  
notarizable packages  
* QTBUG-115691 [FTBFS w/-developer-build]  
QPlatformWindow::setBackingStore(QPlatformBackingStore*) was hidden  
warning  
* QTBUG-115247 \target after \row generates invalid HTML  
* QTBUG-116077 Inconsistent hashing between different FP types  
* QTBUG-116080 Inconsistent hashing between qint{32,64} on 32-bit  
platforms  
* QTBUG-93763 Systematic announcement of combobox selected element  
* QTBUG-88264 [REG v6.0.0-beta3 -> dev] Top-level configure fails if  
told to build tests  
* QTBUG-111785 CMake warns about   accessible/qaccessible.h  
* QTBUG-116503 tst_QUdpSocket failing on some IPv6 multicast tests on  
QNX  
* QTBUG-116483 qttools' CMake test test_uiplugin_via_designer fails  
* COIN-1075 QEMU tests fail randomly on "Exec format error"  
* QTBUG-116106 New accentColor role is missing from QQuickColorGroup  
* QTBUG-84234 Start new QCoreApplication after shutdown  
* QTBUG-116621 tst_qdbusconnection: Test crashes sometimes in CI  
* QTBUG-116689 Debugging qtbase with Creator on boot2qt because of "no-  
prefix" on a prefix build  
* QTBUG-116789 [REG] -platform linux-clang-libc++ -c++std c++2b fails to  
compile synctqt  
* QTBUG-116297 QPainter::drawPixmap showing seams  
* QTBUG-116905 QMimeDatabase doesn't return all glob patterns for mime  
types specified in multiple locations  
* QTBUG-116017 [REG] tst_QDate::startOfDay_endOfDay_bounds() test  
failure  
* QTBUG-108796 Some examples crash when running with Qt 6.5 kit  
* QTBUG-116445 [REG][Windows] Crash on  
NativeSkiaOutputDevice::releaseTexture() with nullptr access  
* QTBUG-113645 QWindowsTheme::queryHighContrast: incorrect parameters  
passed to SystemParametersInfo for SPI_GETHIGHCONTRAST  
* QTBUG-117098 qt_internal_add_test's non builtin_testdata mode can't be  
relied upon for QFINDTESTDATA  
* QTBUG-117120 Debian packages not installing  
* QTBUG-86223 Add gcov support to the CMake build  
* QTBUG-110921 Documentation for building iOS apps is plain wrong  
* QTBUG-116784 iOS built with CMAKE is not uploadable on Appstore  
(Transporter)  
* QTBUG-109444 Qt's CMake deployment API Error: Extra libraries copied  
* QTBUG-113123 Mixed indexes in QListWidget when setSortingEnabled is  
True  
* QTBUG-108761 QXkbCommon::keysymToQtKey does not correctly handle  
punctuation with modifiers under some keyboard layouts  
* QTBUG-27681 [regression] KeyboardLayoutChange is not detected  
* QTBUG-87973 Overload resolution noise from global operators and  
functions  
* QTBUG-109708 Startup crash in QRhiD3D11::endFrame() with nullptr  
access  
* QTBUG-117757 QMultiHash::insert() does not return a correct iterator  
to the inserted element  
* QTBUG-117535 Cannot enable at-spi bridge with wayland  
* QTBUG-118116 QRhiWidget has no way to set flags on the top-level's  
QRhi  
* QTBUG-67200 Windows: Alt + Shift +9 and '(' results Ambiguous shortcut  
overload  
* QTBUG-38137 Some keyboard shortcuts don't work.  
* QTBUG-80953 Test failures on sparc  
* QTBUG-115199 Improve errno handling in Qt  
* QTBUG-111873 qt_attributions.json files should be valid JSON  
* QTBUG-115158 Time zone names and abbreviations are not localised  
* QTBUG-113513 Modernized look for comboboxes on Windows 11  
* QTBUG-95217 Modernized look for context menus on Windows 11  
* QTBUG-113511 Modernized look for sliders on Windows 11  
* QTBUG-113617 Modernized look for spinboxes on Windows 11  
* QTBUG-116613 Qt for webassembly doesn't use browser's locale for its  
QLocale::system()  
* PYSIDE-2492 uic does not generate enumeration name into enum values  
causing type checking warnings  
* QTBUG-118211 Generation of alias targets for executable needs to be  
guarded  
* QTBUG-118569 crash in qschannelbackend  
QTlsPrivate::X509CertificateSchannel::QSslCertificate_from_CERT_CONTEXT  
* QTBUG-118909 Touches cancelled when interacting with multiple windows  
* QTBUG-118080 QDoc cannot distinguish between template function  
overloads differing only  in template arguments  
* QTBUG-87438 corelib plugin tests fail on Android  
* QTBUG-110681 QCheckbox, QRadioButton wrong size when moving app  
between different DPI screens  
* QTBUG-118984 tst_qwidget::render() is flaky-crashing a lot on Android  
* QTBUG-119205 tst_Android::orientationChange is flaky on android  
* QTBUG-117702 qbittorrent dumped core  
* QTBUG-119081 QProcessPrivate::waitForDeadChild() doesn't check  
forkfd_wait's return code  
* QTBUG-114604 Setting initial page orientation for QPrintDialog does  
not work in Windows 11  
* QTBUG-119216 macOS: REG->6.5: DnD with custom text MIME type got  
broken/crashes  
* QTBUG-119359 tst_QGuiEventLoop::processEvents is flaky on QNX  
* QTBUG-119328 [FTBFS w/-unity-build] Linux build runs into sys/mount.h  
vs. linux/fs.h incompatibility  
* QTBUG-86035 Split QtBuild.cmake into smaller files  
* QTBUG-119490 qcocoaapplicationdelegate.mm:354:20: error: cannot  
initialize return object of type 'BOOL'  
* QTBUG-119616 tst_Http2::duplicateRequestsWithAborts fails in CI  
* QTBUG-66223 tst_QDBusAbstractAdaptor is very flaky  
* QTBUG-59336 tst_QDBusAbstractAdaptor::methodCallsPeer() crashes  
occasionally in the CI on OpenSUSE 42.1  
* QTBUG-117948 qt_generate_deploy_qml_app_script() deploys QML plugin  
target but not the corresponding backing target  
* QTBUG-118849 Android: QScreen grabWindow() returns null pixmap  
* QTBUG-119574 Android: request to show SW keyboard not cleared up when  
view destroyed  
* QTBUG-92107 QDBusAbstractInterface::asyncCall() not really async when  
service runs in the same process  
* QTBUG-116551 qt_generate_deploy_app_script doesn't support all  
windeployqt arguments  
* QTBUG-101141 moc: namespaced base class not properly resolved in  
cpp.json file  
* QTBUG-82434 Incorrect Appearance QCursor with AA_EnableHighDpiScaling  
* QTBUG-119998 CMake errors out with recursion in latest dev when using  
qt-cmake-standalone-test on in-source auto test  
* QTBUG-111443 macOS/iOS: "Detected system locale encoding (US-ASCII,  
locale "C") is not UTF-8"  
* QTBUG-119077 CMake deployment API does not deploy Qt Webengine  
* QTBUG-116577 ASSERT: "sumFactors > 0.0"  in qgridlayoutengine.cpp  
* QTBUG-120196 Maximized frameless window painting wrong view region  
with Qt::FramelessWindowHint and Windows api WS_THICKFRAME  
* QTBUG-115125 QObject::connect warns, but also fails to connect to  
lambdas with Qt::UniqueConnection  
* QTBUG-117443 Two Android executables mix their build artifacts if  
targets are added in a single CMakeLists.txt  
* QTBUG-118829 androiddeployqt with --release includes various  
qmltooling libs  
* QTBUG-119915 QIcon::availableSizes() return duplicates  
* QTBUG-106907 "package" attribute in AndroidManifest is deprecated  
* QTBUG-120334 tst_qshortcut_kernel in gui failed on Wayland  
* QTBUG-120078 QOpenGLCompositorBackingStore::resize crashes due to null  
context  
* QTBUG-120460 tst_QHostInfo::reverseLookup() fails on qemu and blocks  
CI  
* QTBUG-109877 macOS: QFileDialog::getSaveFileName() truncates a  
compound extension  
* QTBUG-99750 cannot activate file system watcher in QFileSystemModel  
* QTBUG-118619 Poor QTest::addRow() and QTest::newRow() performance in  
Qt >= 6.5.0  
* QTBUG-113498 QVideoWidget in QDialog does not show / crashes (macOS)  
when shown twice  
* QTBUG-120191 Unable to restore visibility state of the QDockWidget  
* QTBUG-119601 iOS: Sometimes soft keyboard can't be closed  
* QTBUG-96879 QGraphicsView::setTransformationAnchor(AnchorUnderMouse)  
drifts when zooming with trackpad  
* QTBUG-121457 Amend qt_internal_add_docs to accept INDEX_DIRECTORIES  
argument  
* QTBUG-120602 Cannot build Qt modules standalone for iOS  
* QTBUG-120682 Creating QSslSocket when schannel is in use takes too  
long time  
* QTBUG-52021 Blink timer for QLineEdit not killed after QMenu spawn  
* QTBUG-122042 Shortcut icons for the delete and backspace keys seem to  
be wrong  
* QDS-11733 Delete icon points in wrong direction on macOS  
* QTBUG-104997 markdown writer doesn't correctly write blockquotes  
containing lists  
* QTBUG-109367 Android native ExtractEditText does not receive text  
updates from qml TextEdit in fullscreen mode and landscape orientation  
* QTBUG-54623 Linux/xcb/KDE 5.18:  
QFontDatabase::systemFont(QFontDatabase::FixedFont) returns proportional  
font  
* QTBUG-75648 WinRT: QFontDatabase::systemFont(QFontDatabase::FixedFont)  
returns proportional font  
* QTBUG-75649 Boot2Qt (QEMU):  
QFontDatabase::systemFont(QFontDatabase::FixedFont) returns proportional  
font  
* QTBUG-79900 QFontDatabase::systemFont(QFontDatabase::FixedFont)  
returns proportional font  
* QTBUG-99676 markdown (and html) import/export should not rely on use  
of a fixed-pitched font to remember a `monospace` span  
* QTBUG-103484 rich text gets converted to monospace in CI because  
QFontDatabase::GeneralFont is "Sans Serif" and is monospace  
* QTBUG-118139 Fix keyboard input not working for child windows  
* QTBUG-120276 Crash when reparent a native child to a different tlw if  
QT_WIDGETS_RHI=1 is set on Windows  
* QTBUG-122596 [REG 6.7.0->6.8.0] error in configure step, top level  
build, MinGW  
* QTBUG-122693 tst_QApplication::abortQuitOnShow fails frequently on  
Android  
* QTBUG-122137 REG: QtWebEngine / Pdfwidgets no longer supports plugins  
* QTBUG-122704 QPainterPath de-serialisation from QDataStream fails if  
item isn't empty  
* QTBUG-31283 QByteArray::clear() should not free the reserved memory.  
* QTBUG-122838 Android multi-abi builds broken if depfiles are used  
* QTBUG-105009 [REG 5.15.2->6.3.1/6.4.0 Beta2] You can still insert  
Chinese text into a QTextEdit when "readOnly" property is enabled.  
* QTBUG-110838 edit components ReadOnly invalid via some input method  
* QTBUG-119182 Readonly QLineEdit writable using input method  
* QTBUG-122827 Android: Accessibility not working  
* QTBUG-119918 Possible/likely data race in QObjectData bit-field access  
* QTBUG-122420 meta-qt6 incorrectly packages x86_64 qmake on aarch64  
cross-compile target  
* QTBUG-122980 [REG -> dev] Unity Build broken  
* QTBUG-122235 The image gestures app crashes when opening image file on  
Android  
* QTBUG-123115 Finalize 6.7 API review of QCborStreamReader  
* QTBUG-123339 Critical QTextEngine regression in Qt 6.7.0 RC1.  
  
### qtsvg  
* QTBUG-95237 [REG 6.0.4 -> 6.1.0] Integer-overflow in  
QFixed::operator+= through QImage::loadFromData(QByteArray)  
* QTBUG-114108 qtsvgglobal_p.h is not correctly installed  
* QTBUG-115648 QSvgRenderer::boundsOnElement() can return wrong results  
with multiple child <text> elements  
* QTBUG-113042 Loading particular svg file takes too long  
* QTBUG-117944 [Qt SVG] QML Image bad source crashes application instead  
of error status (QSvgHandler::parse)  
* QTBUG-120708 Fluidlauncher manual testing -  Error message on launch  
* QTBUG-120233 QtSvg does not ignore desc and title tag contents when  
child of text tag  
* QTBUG-120653 All SVGs with paths with more than 32768 points render  
incorrectly  
* QTBUG-123010 SVG supported by 6.6 but not by 6.7  
  
### qtdeclarative  
* QTBUG-113745 Qt Quick 2D Renderer: Partial scene update might erase  
items at fractional coordinates  
* QTBUG-113743 QKeySequence cannot be sent to QML Shortcut from C++ side  
* QTBUG-114340 FAIL!  : tst_usertypes::watcherInQml()  
* QTBUG-113752 Warning when assigning to Map.visibleRegion  
* QTBUG-105862 [REG] Qt6.3.1 a MultiPointTouchArea inside another  
MultiPointTouchArea is reporting the wrong touch location  
* QTBUG-114364 qmlformat changes ComponentBehavior  
* QTBUG-114086 [Reg 6.4 -> 6.5] Historical NativeMethodBehavior is  
broken when a Q_INVOKABLE function is stored in a QML property  
* QTBUG-113875 [qmltc] build error with QT_NO_URL_CAST_FROM_STRING  
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
* QTBUG-59878 SVG rasterization issue in QML Canvas  
* QTBUG-80788 [5.14 REG] New properties in ComboBox clash with custom  
properties (revision ignored)  
* QTBUG-100392 Animations crash at runtime because list properties do  
not emit onChanged signal when their items are destroyed  
* QTBUG-114407 [Boot2Qt] UI of imagine style example - automotive is  
distorted on B2Qt devices  
* QTBUG-114467 qmllint does not warn about unqualified id lookup  
* QTBUG-114430 heap-use-after-free when assigning undefined to width and  
height of Control background item  
* QTBUG-114458 [Reg 6.2->6.3] Component.createObject() no longer copies  
QQmlListProperty values correctly  
* QTBUG-114494 QML rect property as a parameter causing a crash  
* QTBUG-114421 Documentation error on ListView orientation table  
* QTBUG-114602 Documentation: LineShape is part of QtQuick.Particles?  
* QTBUG-113714 REG: Memory leak when loading/unloading application fonts  
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
* QTBUG-112434 [Regr: 6.3.1->6.3.2] MouseArea stays pressed after double  
click on touch screen  
* QTBUG-109393 [Regr: 6.3.1->6.3.2] iPad: DoubleClicking in MouseArea +  
Popup breaks  
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
* QTBUG-113527 qmlcachegen does narrowing type coercions when calling  
functions  
* QTBUG-109221 Inconsistencies regarding list and value type property  
manipulations  
* QTBUG-113738 [REG 6.4.3 -> 6.5.0] TableView positionViewAtCell crash  
* QTBUG-114874 REG [5.15 → 6.x]: With `height: implicitHeight` binding  
changes to implicitHeight won't trigger property interceptor (e.g.  
Behavior + Animation)  
* QTBUG-114326 [REG] Non-Singlebit Q_FLAGS not exposed correctly in  
property declarations  
* QTBUG-114808 Quick3d examples don't compile for QNX  
* QTBUG-114607 Flickable.StopAtBounds not working anymore with a wheel  
* QTBUG-113690 Elements of QStringList property are not updatable for  
QGadgets  
* QTBUG-114966 QML Registration wrong warning  
* QTBUG-110328 QEventPoint not being released correctly  
* QTBUG-114687 Qt.application.screens does not update if primary screen  
changes  
* QTBUG-114986 Qml's typeregistrar is not parsing namespaces correctly  
* QTBUG-114858 Dynamically adding State causes Segfault  
* QTBUG-114961 Regression: Keyboard input unusable with redirected Qt  
Quick scenes (QQuickRenderControl)  
* QTBUG-102980 anchors: null warnings are redundant  
* QTBUG-114897 Generated QML code doesn't compile with -Wshadow -Werror  
* QTBUG-114910 Missing constructor params crashes program  
* QTBUG-111013 HorizontalHeaderView with resizableColums true eats input  
when visible (Quick 3D DebugView)  
* QTBUG-104469 Assertion failure when clearing model in  
Component.onCompleted of delegate in Repeater  
* QTBUG-113991 [Reg 6.4 -> 6.5] qmldir javascript library does not  
respect qualified import  
* QTBUG-104008 Can't restore the disabled group object of QQuickPalette  
* QTBUG-114693 Galleryexample app Textarea and Drawer bug.  
* QTBUG-115106 State switched model crashes with ComponentBehaviour  
Bound  
* QTBUG-115179 Clip optimization in  
QQuickDeliveryAgentPrivate::pointerTargets is too aggressive  
* QTBUG-110827 Qt's Gallery example producing tons of warning/errors  
* QTBUG-114978 Wearable example icons hard to distinguish from  
background and other cosmetic issues  
* QTBUG-115115 [Reg 5.15 -> 6.2]  
QV4::Heap::QObjectMethod::ensureMethodsCache crash when calling a  
function in a js file  
* QTBUG-109306 Standard virtual keyboard typing does't generate standard  
QML events.  
* QTBUG-114166 resizing of ListView (possible Flickable) change in  
qt6.5.1  
* QTBUG-108144 Race condition when using QQuickMenu  
* QTBUG-95107 ListView item pooling breaks fetchMore  
* QTBUG-115159 QmlCache cpp files are always generated differently  
* QTBUG-115320 memcpy-param-overlap in qv4runtime.cpp  
* QTBUG-58718 Problems with JS array sorting after unshift  
* QTBUG-115278 [Reg 6.5 -> 6.6] qmlsc: accessing string list crashes  
* QTBUG-114596 Ownership of QObject* returned to qml by Q_INVOKABLE  
differs for const and non-const pointers  
* QTBUG-115523 [REG: 6.5.1->6.5.2] More complex javascript objects not  
converted to QVariantMap anymore  
* QTBUG-115557 Missing type "QQuickTapHandler::ExclusiveSignals" in  
property  
* QTBUG-115251 Infinite loop in QPropertyObserverPointer::notify on  
startup  
* QTBUG-114258 Cannot click on buttons inside Flickable in QQuickWidget  
with stylus  
* QTBUG-115319 Issue with number as a context property name  
* QTBUG-115322 Theme properties set on Item are not propagated to  
children  
* QTBUG-108275 Qmlformat issue with js objects keys  
* QTBUG-114839 qmlformat: Cannot format object destructuring  
* QTBUG-115537 [QML Docs] Image.fillMode enum documentation has a broken  
table formatting  
* QTBUG-104904 [REG 5.15.9 -> 6.3.1] SwipeDelegate does not forward  
mouse events to nested items in left, right, behind  
* QTBUG-115152 qmltyperegistrar cannot see the base class of a  
QML_ELEMENT from a different module  
* QTBUG-115526 qmlcachegen fails to compile SetLookup for non-final  
properties  
* QTBUG-115733 [REG 6.5.1-6.5.2] Automatic conversion JS Array ->  
QByteArray is broken  
* QTBUG-113842 DropArea blocks scrollwheel of a mouse  
* QTBUG-115468 Dynamically adding items to SwipeView may add new items  
behind the current item  
* QTBUG-105090 tst_QQuickMenu AddressSanitizer: heap-use-after-free in  
QQmlData::signalHasEndpoint(int)  
* QTBUG-107473 Infinite loop while trying to open a popup  
* QTBUG-77647 Problems with positioning of Popup with default margins  
* QTBUG-114801 qmlformat: two spaces in 'NumberAnimation on x  {'  
* QTBUG-115951 qml::UnknownTestFunc() QVERIFY()  
* QTBUG-116028 Material Switch doesn't respect Dense variant  
* QTBUG-115948 Calqlatr example - missing Qt Shader Tools module  
* QTBUG-115949 QML Gallery - missing Qt Shader Tools module  
* QTBUG-113940 FileSelector doesn't work correctly  
* QTBUG-115510 undefined reference to `QQuickTextLine::staticMetaObject'  
when using qmlsc in direct mode  
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
* QTCREATORBUG-29419 qmlls cannot find the build directory  
* QTBUG-116179 MinGW 13.1.0: error: array subscript 0 is outside array  
bounds of 'long long unsigned int [0]'  
* QTBUG-116088 Infinite conversion chain in qmlcachegen [QPoint <->  
QPointF]  
* QTBUG-105745 QtQuick.Dialogs.quickimpl plugin not linked in static  
builds  
* QTBUG-115707 REG: Child popup inherits palette from parent popup  
rather than its associated window  
* QTBUG-110243 Resources are lost when linking static libraries using  
CMake build system in a separate project  
* QTBUG-116571 Qt Quick render loop crashes when losing the graphics  
device  
* QTBUG-116617 qmldom spelling error in tag attribute  
* QTBUG-116399 BorderImage produces warning  
* QTBUG-114688 QML application does not start if some QML modules are  
built static  
* QTBUG-116576 [REG 6.2 → 6.4]: Connections and signals whose names  
start with an underscore  
* QTBUG-103310 tst_qqmlbinding::delayed() crashes on Android  
* QTBUG-116749 missing right bracket  
* QTBUG-116587 If using QQuickRenderTarget and setMirrorVertically(true)  
will lead to the qml Item's clip area damage  
* QTBUG-116739 Material.roundedScale has no effect on Frame  
* QTBUG-116106 New accentColor role is missing from QQuickColorGroup  
* QTBUG-116764 Add more fine grained logging category for "used before  
declaration" warning  
* QTBUG-115687 Text loaded with Loader inside Flickable is not visible  
when scrolling  
* QTBUG-115328 Invalid qmllint_json target generated  
* QTBUG-114068 Top level items are not resized to the window size.  
* QTBUG-116753 qml - qmlscene root item sizing discrepancy  
* QTBUG-114144 qmllint: false positive [read-only-property] with  
QQmlListProperty  
* QTBUG-116795 QQuickBasicProgressBar::setColor() does nothing after  
initialization?  
* QTBUG-115004 [Android] TextEdit text selection works incorrect  
* QTBUG-116289 Placing a HoverHandler on a Button makes it respond to a  
right-click.  
* QTBUG-116164 [Regr: 6.5.0->6.5.1] Broken "implicitWidth",  
"implicitHeight" bindings  
* QTBUG-116672 Application crashes when MenuItem text contains img tag  
* QTBUG-116828 Aborting incubation may lead to a crash with some  
controls  
* QTBUG-116681 QtCore Settings does not support ini files located in  
resources  
* QTBUG-116748 HorizontalHeaderView does not use  
QAbstractItemModel::roleNames()  
* QTBUG-117140 gcc 13.2.1  -Werror=maybe-uninitialized in  
qqmldomexternalitems.cpp  
* QTBUG-117062 DelegatePage in Qt Quick Controls - Gallery example is  
broken  
* QTBUG-115227 VerticalHeaderView/TableView required properties go all  
over the place when using syncView  
* QTBUG-105080 FileDialog ignores fileMode : FileDialog.Save  
* QTBUG-116566 QML TableView: resizableColumns/resizableRows breaks the  
default interactive behavior  
* QTBUG-109444 Qt's CMake deployment API Error: Extra libraries copied  
* QTBUG-107214 QML Text Memory leak  
* QTBUG-115485 QtQuick shapes example has misleading file names  
* QTBUG-117361 qmlcachegen crashes in  
QQmlJSTypeResolver::adjustTrackedType  
* QTBUG-113258 Calling QObject methods from QML (still) incurs useless  
overhead  
* QTBUG-117077 qmllint does not allow 'print' as invokable method name  
* QTBUG-117642 Crash when trying to trick property bindings  
* QTBUG-117513 Restore pthread_attr_init() to stackPropertiesGeneric()  
for FreeBSD  
* QTBUG-105839 Commercial license files in opensource archive  
* QTBUG-117672 crash in tst_codegen_indirect_static  
* QTBUG-62954 Pressing escape with a Menu (within a MenuBar) open  
doesn't prevent mouse hovers from opening adjacent menus  
* QTBUG-117130 crash in tryLoadFromDiskCache with corrupted cache  
* QTBUG-117789 QmlCompiler generates invalid code for unary operator+  
* QTBUG-117829 QML engine mis-converts QQmlListProperty  
* QTBUG-117891 [REG 6.5.2 → 6.5.3] Unable to determine callable overload  
with QVariantMap  
* QTBUG-102468 Document that mixing array syntax with other forms of  
populating default properties produces undefined ordering  
* QTBUG-117384 [REG 6.4 → 6.5] Calling a Q_INVOKABLE function with a  
std::vector<long> parameter zeroes the vector  
* QTBUG-116804 QML incubation documentation issues  
* QTBUG-114194 "Connecting signals to methods and signals" documentation  
should mention lifetime of connections  
* QTBUG-113785 Warn about  setContextProperty() in documentation  
* QTBUG-117880 Material 3 misaligns Button icon  
* QTBUG-108883 Improve documentation on how to expose value types with  
enums to QML  
* QTBUG-118132 Failed to compile QML app with VS2019  
* QTBUG-116895 Missing docs for QML_ADDED_IN_VERSION,  
QML_REMOVED_IN_VERSION  
* QTBUG-101991 QML ListModel should document that it's a QAIM  
* QTBUG-118052 Text.NativeRendering causes text to show through.  
* QTBUG-118100 readonly property can be written via unqualified access  
* QTBUG-117451 private/qquickevents_p_p.h: No such file or directory  
when compiling a new Qt Quick Project with QML to C++ Compilation  
* QTBUG-117788 Assert due to cyclic dependencies  
* QTBUG-93780 QML type versioning mechanism needs better documentation  
* QTBUG-87833 qqmlfile.h is marked as internal but is used in examples  
* QTBUG-118091 qmltc includes a non-existent qquickcheckbox_p_p.h  
* QTBUG-118089 Enums exposed to QML seem only working when the QML code  
gets compiled by qmlsc  
* QTBUG-117703 Unclear/missing documentation on using  
QML_FOREIGN_NAMESPACE  
* QTBUG-117922 Unexpected and inconsistent overload resolution when  
calling C++ from QML  
* QTBUG-118469 [REG 6.3.2 → 6.5.0] qsTranslate function no longer  
translates if directly bound to property  
* QTBUG-117793 QML-managed objects are garbage collected when stored in  
QML-declared list properties  
* QTBUG-117479 Segmentation fault in qml debugger  
* QTBUG-117866 Accessing destroyed value in a method connected to a  
Signal results in a crash.  
* QTBUG-117160 touchUngrabEvent is not implemented for qquickflickable  
* QTBUG-117969 Fix 'About Qt' dialog in File System Explorer  
* QTBUG-118222 tst_nodestest (failed) on Android 14 emulator when  
running in a CI VM  
* QTBUG-118514 [Reg 6.5 -> 6.6] Miscompilation of arithmetic operators  
* QTBUG-118591 Regression: QQmlScriptString::operator==() crashes  
* QTBUG-118237 Documentation of QML font weights is incorrect  
* QTBUG-108449 Virtual keyboard does not appears until window focus  
changed to another application  
* QTBUG-118069 Wrong position reported uppon touch release  
* QTBUG-118397 ~QQuickContainer() Crash when calling  
QQmlIncubator::abort  
* QTBUG-118633 Popup stretches outside window boundary when anchored  
with overlay centerIn  
* QTBUG-117800 QmlCompiler generates bogus warning about internal  
conversion  
* QTBUG-118748 In the .cpp generated by qml, include qcoreapplication.h  
without module dir variant  
* QTBUG-118738 Not possible to exclude qtquicktimeline and qtquick  
control styles from the build  
* QTBUG-118744 Flaky crash (segfault) when running tst_inputpanel  
tst_plugin::test_fullScreenModeWordReselection  
* QTBUG-118163 Flaky race-condition in QuickTest when running  
tst_inputpanel built with ASAN  
* QTBUG-118525 Crash if popping a StackView causes a nested event loop  
to run  
* QTBUG-78441 Text disappears when using a U+FFFC unicode character  
* QTBUG-118460 Overlay.rotation gets discarded when window is resized  
* QTBUG-116606 unable to deselect text in text input using touch  
* QTBUG-117831 [REG: 6.5.2->6.5.3] Destroying active popup with dim  
layer leaves the dimming layer behind  
* QTBUG-118461 Overlay's opacity is ignored  
* QTBUG-118897 Qt Quick TableView performance issue when updating  
ContentY in onModelChanged  
* QTBUG-115579 Rebinding of property alias does not work for some  
aliases that refer to certain (grouped) properties  
* QTBUG-117799 QmlCompiler unnecessarily generates QJSValue from list  
operation  
* QTBUG-115166 qt_add_qml_module() causes non-Ninja generators to think  
that projects are never up-to-date  
* QTBUG-117958 qt_add_qml_module does not register QML_SINGLETON classes  
if version starts with 0  
* QTBUG-118856 Placeholder text does not follow the set  
horizontalAlignment in Material style.  
* QTBUG-119065 Unable to reset tray icon menu for QML SystemTrayIcon  
* QTBUG-119024 Window position is bypassed by Wayland.  
* QTBUG-117795 Bogus compile warning  
* QTBUG-117917 HorizontalHeaderView with plain JavaScript array model  
crashes on flick  
* QTBUG-118760 Misplaced letter in the Qt Quick Controls example  
ComboBox text  
* QTBUG-86977 Qml Text underline changes on resize with fractional  
display scale factors  
* QTBUG-29676 Signals not disconnected when target object is destroyed  
* QTBUG-75483 QML Tooltip visibility is set to false but should not  
* QTBUG-93856 Menus with a certain fixed height, element height and  
window height not scrolled when they should  
* QTBUG-119122 Using a specific as-cast asserts and fails compilation  
* QTBUG-119132 it should be possible to disable the  
TapHandler.longPressed signal  
* QTBUG-105810 iOS: TapHandler emits clicked, even if long pressed more  
than StyleHint::MousePressAndHoldInterval  
* QTBUG-119091 QmlCacheGen crashes on QML-file, but won't disclose  
where/why it cashes  
* QTBUG-119090 QmlCacheGen miscompiles Enum constant reference, yielding  
"undefined"  
* QTBUG-53987 Cursor is not updated on mouse wheel over flickable  
* QTBUG-90457 HoverHandler.cursorShape doesn't change dynamically within  
same bounds  
* QTBUG-54019 regression in certain MouseArea hover use cases  
* QTBUG-115696 Delegates are not re-positioned when ListView orientation  
is changed runtime  
* QTBUG-117892 Radius not working from QSGDefaultInternalRectangleNode  
* QTBUG-112673 Drag.imageSource example - no image on first drag  
* QTBUG-115491 Drag.imageSource Only Works On Second try  
* QTBUG-118779 QT quick control-wearable demo-example Issue with the  
background when switching light/dark mode  
* QTBUG-119298 [macOS] Using Imagine style controls provokes Qt warning  
* QTBUG-83155 Roboto font used in Material style slows down startup time  
* QTBUG-119181 Crash in QQmlDelegateModelGroup::insert  
* QTBUG-119165 qmlsc: QUrl does not compile in console.log()  
* QTBUG-119216 macOS: REG->6.5: DnD with custom text MIME type got  
broken/crashes  
* QTBUG-80910 Drawer item does not support rotation  
* QTBUG-71117 When the contentOrientation is changed for the  
ApplicationWindow, then the Drawer does not drag out as expected  
* QTBUG-115536 Setting Window.contentOrientation breaks Popup on regular  
desktop  
* QTBUG-115121 PathView can be clicked through if it is flicking and  
delegate has MouseArea  
* QTBUG-119160 Graphics corruption when toggling depth-aware rendering  
* QTBUG-119005 QML FileDialog file size overflow  
* QTBUG-108261 "Required property foo was not initialized" when using JS  
array as model with required properties in delegate  
* QTBUG-118902 Qmltyperegistrar doesn't escape "-" in "#ifdef" generated  
code  
* QTBUG-115710 [Windows and WSL2] QML module that only contains C++ code  
breaks `all_qmllint` target  
* QTBUG-119147 Invalid input not handled in Qt Quick Controls - Contact  
List example  
* QTBUG-118828 CloseEvent QML Type is anonymous type  
* QTBUG-119084 Connections type doesn't work in qmltc'ed app  
* QTBUG-119451 the document is incorrect about the data type in the code  
snippet  
* QTBUG-119162 Qml: Behaviour differs between interpreted/compiled code  
* QTBUG-119531 [Reg 6.6.0 -> 6.6.1] TypeError: Type error with aliases  
* QTBUG-99266 [Qt Quick 2D Renderer] Text underlines rendering is broken  
on fractional screen's scale factors  
* QTBUG-119838 [REG] qt_add_qml_module broken for the VS generator when  
called in different subdirectories  
* QTBUG-117948 qt_generate_deploy_qml_app_script() deploys QML plugin  
target but not the corresponding backing target  
* QTBUG-118445 Native macOS MessageDialog doesn't reopen  
* QTBUG-118212 [Reg 5.15->6.x][Android] MessageDialog's standard buttons  
do not accept/reject the dialog  
* QTBUG-119395 crash on QML property bindings  
* QTBUG-81022 Text editor example contradicts QQuickTextDocument's  
documentation  
* QTBUG-120005 Native TextArea: placeholderText does not respect  
horizontalAlignment  
* QTBUG-108807 QQC2 TabBar first TabButton visual state incorrect when  
deselected  
* QTBUG-109488 tst_qquicktextedit::largeTextObservesViewport fails / is  
flaky  
* QTBUG-119715 REG: ScrollView content size broken  
* QTBUG-119675 [qmllint ] Enabling the qmllint for a lot of QML files  
exceeds the command line limitation on Windows host  
* QTBUG-117827 [Reg 6.6 -> 6.7] Bogus cyclic dependency warnings between  
singletons  
* QTBUG-117387 TapHandler and DragHandler interoperability breaks  
* QTBUG-66360 PointHandler goes inactive releasing mouse button when  
multiple pressed  
* QTBUG-83980 HoverHandler: sometimes point.position returns (0, 0)  
* QTBUG-119363 UniformAnimator makes app crash when being destroyed by  
other component  
* QTBUG-119793 QML Button (Material 3) contents truncated  
* QTBUG-119640 Typo in the document  
* QTBUG-119794 QJSValue: url does not convert to QUrl  
* QTBUG-119963 [Reg 6.5.1->6.5.3] QJSEngine no longer converts new'ed JS  
object to QVariantMap  
* QTBUG-120084 [REG 6.6 → 6.7] bogus "TypeError: Cannot read property  
'Foo' of undefined" error when using enums  
* QTBUG-120168 [Reg 6.6 → 6.7] Cannot launch minidesk appman example  
* QTBUG-120279 Cyclic dependency error in qtquick3d  
* QTBUG-120282 Configuring qtcharts from sources fails because of  
dependency cycle  
* QTBUG-120205 [REG: 6.5->6.6] Image implicitWidth/Height no longer  
available in onStatusChanged  
* QTBUG-119916 Non-native FileDialog does not prompt about overwriting  
an existing file  
* QTBUG-117899 [REG 6.4->6.5] Binding Loops -> Wrong layout because of  
interruption  
* QTBUG-118511 Binding loop if ColumnLayout implicitWidth is changed  
* QTBUG-120113 [Reg 6.6 -> 6.7] Bluetooth QML examples start crashing  
after recent additions to QtDeclarative  
* QTBUG-120322 qmlsc: crash on assigning int property  
* QTBUG-119760 Crash when dereferencing a deleted QRhi after native  
window is re-created  
* QTBUG-120349 Window Qml Type doc is missing the default visible  
property value  
* QTBUG-116306 Mention indeterminate state for Qt Quick Controls 2  
ProgressBar customization  
* QTBUG-120346  hovered property of HoverHandler stays true when sliding  
by touch outside of hover area  
* QTBUG-120100 qmlls: completion inserts colons in bindings  
* QTBUG-120102 qmlls: completion mismatch for qualified expressions  
* QTBUG-120111 qmlls: missing completion for qualified types  
* QTBUG-120137 qmlls: completion inserts extra semicolon in for loops  
* QTBUG-119842 qmlls: crash when autocompleting return statements  
* QTBUG-120296 Qt Quick Widgets Example  -  Grab Framebuffer is  
susceptible to crash  
* QTBUG-120504 REG: Call on null object in optional chain throws an  
error  
* QTBUG-120169 qmlls: no completion in attached/grouped properties  
because of parser  
* QTBUG-119917 Non-native FileDialog loses current filename when  
changing folders  
* QTBUG-120052 TextArea/TextField: placeholderText does not respect  
horizontalAlignment after the component creation  
* QTBUG-120065 Non-native FileDialog loses URL schema when filename is  
manually entered  
* QTBUG-120592 tst_inputpanel (Failed)  
* QTBUG-120628 TableView: cannot select cells when using mouse press +  
shift  
* QTBUG-119646 [Tests] Warnings in  
qtdeclarative/tests/auto/quickcontrols/controls/data/tst_textfield.qml  
* QTBUG-119645 [Tests] Warnings in  
qtdeclarative/tests/auto/quickcontrols/controls/data/tst_textarea.qml  
* QTBUG-99231 "Could not set initial property horizontalAlignment" when  
trying to set resettable property  
* QTBUG-119372 build fails with Q_IMPORT_QML_PLUGIN macro  
* QTBUG-120189 [Reg 6.6 -> 6.7] Cannot assign object of type  
"IconPropertiesGroup" to property of type  
"IconPropertiesGroup_QMLTYPE_1*" as the former is neither the same as  
the latter nor a sub-class of it  
* QTBUG-120336 [Reg 6.6 -> 6.7] Qt Quick Examples - Pointer Handlers  
example crashes  
* QTBUG-120473 [Reg 6.6 -> 6.7] qmlsc: type mismatch generates  
uncompilable code  
* QTBUG-113776 qmlformat fails to format if there is a escape char in  
the key string  
* QTBUG-106598 MessageDialog won't open if its parent is a plain item  
* QTBUG-120479 qmldir file not placed with library with CMake Xcode  
generator  
* QTBUG-120555 AnimatedImage: issues with loading web source  
* QTBUG-120484 qmlls: formatting removes some comments  
* QTBUG-120677 tst_qmlls_utils: adapt tests to changes in qmlls  
* QTBUG-119839 qmlls: invalid completions after dots  
* QTBUG-121014 [REG 6.6 → 6.7] Faulty behavior of instanceof when  
multipe QML engines are used  
* QTBUG-121022 Miscompilation of condition  
* QTBUG-119992 qt5 code is used for the qt6.6 documentation  
* QTBUG-121206 NO_LINT has not effect in qt_add_qml_module  
* QTBUG-121132 TableView: overlapping selections are cleared  
* QTBUG-121035 QSettings::value("Theme") returns an empty QByteArray if  
beginGroup has been called  
* QTBUG-113558 QQuickWidget does not handle touch event via QML  
TapHandler correctly  
* QTBUG-121139 qmlcachegen locks up in some situations  
* QTBUG-120568 "Using the Configuration File in a Project" only covers  
qmake way and not cmake  
* QTBUG-119994 the documentation seems to be contradictory to the code  
snippet  
* QTBUG-119903 the link to elevated card cannot be found  
* QTBUG-115953 Interactive Flickable with pressDelay makes  
childMouseEventFilter to lose MouseButtonPress event  
* QTBUG-118857 Virtual Keyboard is hidden by QtQuick.Dialogs' dialogs  
* QTBUG-121216 Drawer item does not support rotation for touch input  
* QTBUG-121393 Q_UNREACHABLE was reached while compiling some files  
* QTBUG-120512 Inconsistent behaviour between qmlsc and JIT compiler  
when setting a property to "undefined"  
* QTBUG-116426 crash in QQuickItemPrivate::derefWindow  
* QTBUG-120450 Allocating or deallocating a QJSEngine object causes a  
crash if the application has called mlockall(MCL_CURRENT|MCL_FUTURE)  
* QTBUG-121588 [REG 6.6 → 6.7] Crash in  
VDMListDelegateDataType::createMissingProperties  
* QTBUG-118710 [REG 6.5.2 → 6.5.3] QQmlProperty: wrong warning about  
signal handler capitalization  
* QTBUG-111729 Assertion failed in QJSEngine when repeatedly deleting &  
adding property getters on an object  
* QTBUG-120301 QQuickStateGroup taking null pointers leads to crash  
* QTBUG-113695 qmllint: property-changes-parsed suggests can code that  
don't understand  
* QTBUG-121734 SetLookup crashes on hierarchy of shadowable properties  
* QTBUG-119326 application crash when using QML-Debugger: Component vs  
.qml  
* QTBUG-109261 qmlsc dead code analysis is incomplete  
* QTBUG-121710 [Reg 6.6.0 -> 6.6.1] Aliasing to enums does not work as  
in Qt 6.6.0 an earlier anymore  
* QTBUG-119984 old way of exposing c++ class to qml is written  
* QTBUG-121909 [Reg 6.6 -> 6.7] Optional chaining+ nullish coalescing  
leads to uncompilable code  
* QTBUG-120008 tst_QJSEngine::valueConversion_QVariant is flaky  
* QTBUG-119459 [Reg 5.15 -> 6.2] the line number output by  
console.trace() is too big  
* QTBUG-113039 Crash when accessing properties of line parameter in  
Text.onLineLaidOut  
* QTBUG-120499 [REG 6.5.3 - 6.6.1] QML warning "Final member modelData  
is overridden in class QQmlDMAbstractItemModelData. The override won't  
be used."  
* QTBUG-120506 [Reg 6.5 -> 6.6] Using `CameraLens.ProjectionType` as  
type hinting cause runtime error  
* QTBUG-122108 Crash while attempting to load rich text resource from an  
invalid scheme  
* QTBUG-120573 [REG 6.6->6.7] TypeError: Property 'onDownPressed' of  
object QQuickKeysAttached(...) is not a function  
* QTBUG-118750 REG: QQuickItem::setParentItem to null triggers  
tst_qmltests crash  
* QTBUG-122173 tst_qquickanimatedimage::currentFrame() is flaky on  
windows  
* QTBUG-122106 QList<int> is converted to int by qmlsc  
* QTBUG-118889 Assert when changing focus fast of  
qquickmaterialplaceholdertext  
* QTBUG-119829 [Reg 6.5 -> 6.6] Shadowing default property crashes QML  
* QTBUG-122004 Generated code of qt_add_qml_module fails to build  
* QTBUG-120105 Unreliable QML Timer / qmltest wait() / QTest:qWait()  
with offscreen platform  
* QTBUG-121840 Cannot format the text and the 'Touch User Interface' is  
not available in text editor example on Qt 6.7.0  
* QTBUG-121946 scoped enum values cannot be used as keys in a JS object  
* QTBUG-121349 Flickable: strange defaults for mouse wheel triggered  
boundsMovement  
* QTBUG-121592 Attached ScrollBar and ScrollIndicator fail when using  
QML Type Compiler  
* QTBUG-118982 qmllint multiple pragma ComponentBehavior in same file  
* QTBUG-119448 Fix documentation: initializing a property of aliased  
property won't actually cause an error  
* QTBUG-120526 qmllint complains wrongly when changing Layout attached  
properties in a PropertyChanges  
* QTBUG-116994 qt_add_add_qml_module runs into command line length  
limits on Windows  
* QTBUG-119911 Incubated object is garbage collected before a reference  
to it can be created  
* QTBUG-120200 [REG 6.6.1->6.7.0] static build fails on MSVC2019 x64,  
qtquick3d  
* QTBUG-118497 REG [6.6.1->6.7.0] static build fails on MSVC2019 x64  
* QTBUG-116006 QtQuickTimeline build fails in Visual Studio static  
builds  
* QTBUG-122024 Advertised and documented property of Layouts does not  
work.  
* QTBUG-122454 Gallery example radio buttons not working as expected  
* QTBUG-110772 qmlsc/cachegen can trigger -Wtrigraphs  
* QTBUG-117798 QmlCompiler generates bogus warning about writing back  
object types  
* QTBUG-116505 HoverHandler is broken when using a stylus  
* QTBUG-101932 two HoverHandlers with different  
acceptedDevices/acceptedPointerTypes: cursorShape doesn't change  
accordingly  
* QTBUG-101364 qmllint spurious error: QML State AnchorChanges: with  
type QQuickAnchorLine to QQmlScriptString of QQmlScriptString  
* QTBUG-120772 TextEdit.textDocument loads according to mime type  
regardless of TextEdit.textFormat  
* QTBUG-120620 6.7.0.beta1 Calqltr app fails to start with single  
threaded WASM  
* QTBUG-122676 weatherforecast example: ASSERT crash when running on  
Raspberry Pi OS (debian 11 derivative), arm64  
* QTBUG-108673 QJSEngine use wrong logging category "default" for  
console.trace()  
* QTBUG-115478 Qmllint interferes with qmldir file in source directory  
if present  
* QTBUG-115439 Qmllint throws warnings at TapHandler's signals  
* QTBUG-121134 doc: fix QML tools links  
* QTBUG-122251 qmltc crashes with Qt.point as a return type  
* QTBUG-120760 Unloading TableView headers via Loaders causes crash  
* QTBUG-118804 The link is looping for Qt Quick Effect Maker  
* QTBUG-122686 Crash when processing hover events modifies object tree  
* QTBUG-109708 Startup crash in QRhiD3D11::endFrame() with nullptr  
access  
* QTBUG-101200 Qt crash/freeze when doing a graphics driver update on  
Windows  
* QTBUG-120007 QtQuick text rendering performance regression Qt5->Qt6  
* QTBUG-116057 Enums annotated as scoped-only match unscoped with  
QML_SINGLETON  
* QTBUG-107143 qmllint ignore RegisterEnumClassesUnscoped  
* QTBUG-122707 [Reg 5.15 -> 6.4] Binding QML type does not restore  
original value in some cases  
* QTBUG-122790 Child window is not closed upon closing the main window  
in Qt Quick Widgets Example  
* QTBUG-120433 AnimationController segfaults on exit  
* QTBUG-91272 [Regression]On Mouse Area press, deleting other  
overlapping mouse area crashes the Application  
* QTBUG-113384 QQuickWidget - touchpad click not working after scrolling  
* QTBUG-122915 [REG 6.6.1-6.6.2] Overlay remains visible when a Popup is  
destroyed via Loader  
* QTBUG-123014 tst_qquicktextdocument (Failed)  
* QTBUG-121197  [REG 6.6 → 6.7] Opening window from Loader does not work  
* QTBUG-122230 Broken links in qtdeclarative docs  
* QTBUG-122008 The child window does not get the style of the parent in  
the attached style properties example (QQuickAttachedPropertyPropagator)  
* QTBUG-122985 toggling TextEdit.format back and forth between AutoText  
and PlainText loses markdown after a couple of times  
* QTBUG-123225 REG[6.6 → 6.7]: QML: unscoped enums stopped working  
* QTBUG-123307 build fails "qtdeclarative/src/quick/platform/android/qan  
droidquickviewembedding.cpp"  
* QTBUG-123428 [REG 6.6 → 6.7 ]Using QML_DISABLE_DISK_CACHE breaks QML  
code  
* QTBUG-123332 Install dir is incorrect for Qt6AndroidQuick.jar  
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
* QTBUG-114718 [Tests] tst_QQuickPopup fails  
* QTBUG-114396 Change "OpenGL" to "Graphics API"  
* QTBUG-114825 Blacklisting of tst_qquickpopup::hover doesn't work  
* QTBUG-114571 Incorrect colors after switching between light and dark  
modes  
* QTBUG-40856 MouseArea containsMouse flag is not reset on Touch Screen  
* QTBUG-86729 many Qt Quick test failures after input event refactoring  
* QTBUG-114845 qt6 qml documentation: "font.style" should be  
"font.styleName"  
* QTBUG-114959 Pushing Qt.binding to JS variable in StackView results in  
the pushed item's property not reacting to changes  
* QTBUG-114475 QML QQuickPointerHandler crashes  
* QTBUG-112537 A Window's background cannot be semitransparent anymore  
* QTBUG-113456 Window background cannot be transparent.  
* QTBUG-115015 [REG 5.15.14->6.5.1]: Qt6 QML component Window setting  
property color: "transparent" doesn't make the Window transparent for  
Windows 11 and MacOS  
* QTBUG-107771 QML Native ScrollBar: Unable to assign [undefined] to int  
* QTBUG-48018 QML Flickable truncates contentX to signed 32-bits  
(0x80000000)  
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
* QTBUG-109542 TreeView: TreeView.modelIndex() has the order of row and  
column swapped  
* QTBUG-115110 .rcc/qmlcache/ generated code is too liberal in its use  
of std::move()  
* QTBUG-115554 QQuickAttachedPropertyPropagator cannot propagate through  
popup and window  
* QTBUG-114953 PdfMultiPageView: Very poor memory performance when  
zooming in/out of long documents  
* QTBUG-116432 Virtual keyboard import version number from Qt 5.15 does  
not work in Qt 6.5 version  
* QTBUG-116742 tst_qqmlbinding Failed  
* QTBUG-116537 Add \examplecategory to qtqml  
* QTBUG-111570 ASSERT: "newInstance != d->animationInstance" in file  
qquickbehavior.cpp  
* QTBUG-31492 ListView creates and destroys delegates infinitely under  
certain conditions  
* QTBUG-101552 FileDialog(SaveFile) doesn't work correctly on KDE  
* QTBUG-108455 FileDialog.SaveFile mode is unusable  
* QTBUG-117403 Material dark theme not used when using runtime style  
selection  
* QTBUG-117700 StackView's enter transitions are broken when  
pushing/replacing onto an empty stack  
* QTBUG-117526 QQuickStylePrivate::fallbackStyle has the wrong value  
when using run-time style selection and the fallback style is imported  
via the style's qmldir  
* QTBUG-117830 Crash on QQuickMultiEffectPrivate::updateEffectShaders()  
with nullptr access  
* QTBUG-117806 QQmlApplicationEngine::loadFromModule() not working on  
Android  
* QTBUG-116660 doc: move qmlls and qmllint out ot "Qt Quick"  
* QTBUG-98734 FAIL!  : tst_qqmlcomponent::qmlCreateWindow() Received a  
fatal error.  
* QTBUG-116589 Dynamic translations seem not working with  
QQmlApplicationEngine::loadFromModule()  
* QTBUG-118532 tst_qquickpopup::doubleClickInMouseArea and overlay are  
flaky on android  
* QTBUG-118067 Flaky tests on opensuse 15.5: Parent task  
* QTBUG-117968 Initialization behavior difference between precompiled  
and not compiled QML component  
* QTBUG-118431 inline component seems can not support cast feature(Type  
assertions)  
* QTBUG-118624 [WASM] Qt's internal shaders can easily conflict with  
user shaders  
* QTBUG-118636 Some missing content of the rich text table while  
displaying HTML file with TextArea  
* QTBUG-101143 QML_FOREIGN refering to a class in another library leaves  
the type empty in qmltypes file  
* QTBUG-65012 TapHandler: should not emit longPressed if the point is  
dragged  
* QTBUG-115237 Dragging PathView beyond the end of the path and  
releasing outside of it starts a flick  
* QTBUG-102846 [Windows] Restoring OpenGL context logic doesn't seem  
valid  
* QTBUG-118074 qmllint does not complain about invalid import URL  
* QTBUG-118080 QDoc cannot distinguish between template function  
overloads differing only  in template arguments  
* QTBUG-111873 qt_attributions.json files should be valid JSON  
* QTBUG-50693 QQuickItem::grabToImage ignores scale factor  
* QTBUG-119663 extending qml tutorial cannot be found in the examples  
available in the qt creator  
* QTBUG-36521 Basic TextArea functionality depends on C++  
* QTBUG-38830 Meta task for examples/quick/controls/texteditor  
* QTBUG-117667 REG: TextEdit height gets stuck due to binding loops  
(forever) or anchor changes (temporarily until further resize event)  
* QTBUG-25489 QtQuick2 TextEdit emits unnecessary cursorRectangleChanged  
on all kinds of modifications  
* QTBUG-116551 qt_generate_deploy_app_script doesn't support all  
windeployqt arguments  
* QTBUG-108808 QQC2 BusyIndicator does not inherit visibility from  
parent consistently  
* QTBUG-120262 Use SPDX-License-Ref in 3rdparty directories  
* QTBUG-121192 _qt_internal_collect_buildsystem_targets does not handle  
multiple build directories of the same source directory  
* QTBUG-118867 Render thread can delete font engines still in use  
* QTBUG-120356 padding not applied to header and footer for  
QuickControls.Dialog  
* QTBUG-117654 TextArea multi-line placeholder text overlaps the  
TextEdit area  
* QTBUG-121643 qt6-declarative: possible build-time race condition  
around qmlcachegen  
* QTBUG-122256 Crash on  
QQuickMultiEffectPrivate::updateBlurItemsAmount() with nullptr access  
* QTBUG-62111 Docs: Fixed day/year format in QDateTime  
* QTBUG-122405 tst_qquickhoverhandler::window is flaky on OpenSuse  
* QTBUG-63363 QPointingDevices for the trackpad and mouse are  
dynamically instantiated on macOS  
* QTBUG-112432 wayland plugin should distinguish touchpads from mice,  
etc.  
* QTBUG-109548 Find a signal-specific replacement for PropertyChanges  
* QTBUG-122679 tst_how-to-qml timePicker is flaky  
* QTBUG-122653 6.8.0 toplevel build fails on MSVC2019 x64, qtdeclarative  
* QTBUG-78846 tst_qquicktextedit::mouseSelectionMode is flaky on  
OpenSuse 15  
* QTBUG-74342 QML RichText hr element doesn't work  
* QTBUG-123160 crash in qquickspinbox  
  
### qtactiveqt  
* QTBUG-56172 ActiveQt components are not well behaved when  
unloading/reloading  
* QTBUG-100657 Crash while receiving COM IDispatch events when  
initializing  
* QTBUG-96871 Crash on calling connect on   QAxObject source instance  
* QTBUG-119064 Build fail on Windows (reg 6.5.3 -> 6.6.0)  
* QTBUG-111191 Qutlook Example (ActiveQt) crashes with Qt6.4.2  
  
### qtmultimedia  
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
* QTBUG-113742 Camera/VideoOuput possible memory leak on Android.  
* QTBUG-115275 VideoOutput - Memory leak with Android Camera source  
* QTBUG-116533 Sporadic crash on QSGVideoMaterial::updateTextures() with  
nullptr access  
* QTBUG-115935 REG: FFMPEG backend causes Android 13 crash on Launch  
* QTBUG-116901 QAudioSink: incorrect example code for stopping the  
device  
* QTBUG-115460 Camera crash on image acquire on Android  
* QTBUG-116526 Android camera crash in example project  
* QTBUG-114932 [DeclarativeCamera] Capture crashes the example  
* QTBUG-117086 [WMF] Excessive Qt warning "No audio output"  
* QTBUG-116991 QVideoFrame allocation broken for YUV422P  
* QTBUG-117056 ERROR: AddressSanitizer: heap-use-after-free in  
tst_QAudioSink::pullResumeFromUnderrun()  
* QTBUG-114083 [QtDeclarativeCamera] Popup list of available cameras is  
not available after changing the orientation  
* QTBUG-116688  QVideoFrame::toImage: failed to get textures for frame;  
format: 172 textureConverter null  
* QTBUG-117421 Compilation failes for Android with FFmpeg  
* QTBUG-116801 Path with space leads to crash Qmultimedia example  
* QTBUG-117599 Compilation error for FFmpeg with dynamically linked  
OpenSSL  
* QTBUG-117656 Compilation failes for Android with FFmpeg  
* QTBUG-115568 Missing type "QScreen" is referenced in qmltypes  
* QTBUG-115444 MediaPlayer has no sound on Android  
* QTBUG-116779 FFmpeg backend: GUI thread freezes when initializing an  
network source  
* QTBUG-118706 Crash on QWindowsMediaDevices::availableDevices() with  
nullptr access  
* QTBUG-118749 tst_qtexttospeech_qml (Failed)  
* QTBUG-117006 MediaPlayer::playing isn't always true when it should be  
* QTBUG-118624 [WASM] Qt's internal shaders can easily conflict with  
user shaders  
* QTBUG-117744 Bluish hue in video  
* QTBUG-115075 WebAssembly audio input not working  
* QTBUG-119087 MediaPlayer-Graphic&Multimedia-example Volume slider is  
being compressed and becomes unusable  
* QTBUG-119083 MediaPlayer-Graphic&Multimedia There exists an empty  
selection when going through next and previous media  
* QTBUG-118777 Emulation layer crash / cannot run project after adding  
two Audio Listeners  
* QTBUG-118699 The video playback is corrupted with Android native  
backend  
* QTBUG-118309 QML Camera - Zoom not observed in Preview  
* QTBUG-116324 Request to implement thumbnail realization for multimedia  
FFMPEG backend  
* QTBUG-119089 QML Camera crashing on some devices  
* QTBUG-119445 Camera crash on image acquire on Android  
* QTBUG-117099 Video jerks when playing (Windows backend)  
* QTBUG-118734 Attribution scanner can not refer to files downloaded  
during provisioning  
* QTBUG-119693 [REG] 6.7.0 namespace build fails on Windows  
(MSVC&MinGW), multimedia  
* QTBUG-119236 Unexpected value for QML Camera.error enum  
* QTBUG-119909 qffmpegscreencapture_dxgi.cpp(288): error C2039:  
'QWindowsScreen': is not a member of 'QNativeInterface::Private'  
* QTBUG-118573 Android tests on CI part 3/3 (screen/window capture)  
* QTBUG-118839 [DeclarativeCamera] The app crashes when unlocking the  
screen on Android  
* QTBUG-116519 [Reg 6.2 -> 6.5] Repeated QSoundEffect is broken on  
PulseAudio  
* QTBUG-113616 Android: Crash when mapping QVideoFrame object  
(minimize/restore)  
* QTBUG-118127 QMediaPlayer can not play sound again after the sound  
finished.  
* QTBUG-120449 Qt6 Multimedia WebAssembly Docs reference nonexistent  
method  
* QTBUG-113498 QVideoWidget in QDialog does not show / crashes (macOS)  
when shown twice  
* QTBUG-118593 QML Camera ImageCapture Parameter not declared  
* QTBUG-118572 Android tests on CI part 2/3 (audio)  
* QTBUG-118587 [WMF] Video position may exceed it's duration  
* QTBUG-120198 Process abruptly terminates while executing static  
destructor in Qt6Multimedia.dll  
* QTBUG-121455 QtMultimedia module fails Yocto CI build  
* QTBUG-121200 QML Video Recorder - Missing Text in Buttons on Android  
* QTBUG-121495 COM is uninitialized too many times with FFmpeg and  
QWindowsResampler  
* QTBUG-121187  Spectrum App Crashes after recording sound in "Record  
and Playback" Mode  
* QTBUG-119737 MediaRecorder.isAvailable not defined  
* QTBUG-120465 QML Camera unloading crash on iOS  
* QTBUG-119746 Audio recording volume extremely low  
* QTBUG-114900 alsa backend causes warning messages  
* QTBUG-122096 Wrong colors are displayed when playing videos with IMC2  
color format  
* QTBUG-122053 Qt continues to occupy the microphone unless you call  
QMediaCaptureSession::setAudioInput() with a null pointer after  
recording is complete  
* QTBUG-121714 Camera preview stops working when recording on Android-  
backend  
* QTBUG-122045 [MediaPlayerExample] The timeline is not reset when the  
loop mode for single file is turned on  
* QTBUG-120026 Retrieving videoDevices blocks main event loop  
* QTBUG-121221  Camera Example - Recording Denied with "Invalid  
Argument" Error  
* QTBUG-113317 QVideoWidget rendering video incorrectly on macOS  
Monterey  
* QTBUG-121943 QPlatformMediaDevices is accessed before main on Android  
* QTBUG-122640 QtMultimedia plugins are not deployed to Android .apks  
* QTBUG-122638 [gstreamer] deadlock when switching camera  
* QTBUG-122706 onBufferProgressChanged not emited at all  
* QTBUG-121678 eglfs: Capturing the screen crashes on a Qt Quick  
application  
* QTBUG-122750 [Regression] QSoundEffect cuts audio with FFmpeg backend  
* QTBUG-122753 Qt Multimedia: implicit instantiation of undefined  
template 'std::char_traits<unsigned char>' (libc++ 19 / musl libc /  
amd64)  
* QTBUG-122193 QSoundEffect hangs on Loading  
* QTBUG-121182 QML Video Example: Simultaneous videos playback crashes  
the App on Android  
* QTBUG-122649  Playing multiple videos simultaneously fails for the  
second video with the FFMPEG backend on Android.  
* QTBUG-122199 [ffmpeg] player crash in libavcodec if libnvidia-decode  
is not installed  
* QTBUG-122608 [REG 6.6.1-6.6.2] [windows] QMediaPlayer failed to set  
topology on custom QVideoSink  
* QTBUG-122817 [REG 6.6.1-6.6.2] [windows] QML MediaPlayer unable to  
play a video when 'audioOutput' is not specified  
* QTBUG-98437 QMediaPlayer does not emit destroyed signal  
* QTBUG-122887 Android: MediaPlayer: AudioOutput via HDMI not possible  
* QTBUG-123105 ror: no matching conversion for functional-style cast  
from 'const char[5]' to 'QStringView'  
* QTBUG-123312 [gstreamer] video playback broken with gstreamer older  
than 1.20  
* QTBUG-123597 QAudioDecoder crashes on files without audio track  
* QTBUG-109537 Spectrum example build fails  
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
* QTBUG-111567 masOS audio deadlock with AudioOutputUnitStart /  
AudioOutputUnitStop  
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
* QTBUG-116979 VideoOutput implicit size doesn't update until playback  
begins  
* QTBUG-116444 [Windows] Qt warning "Failed to retrieve default audio  
endpoint -2147023728"  
* QTBUG-116978 MediaPlayer::position cannot be declared in QML  
* QTBUG-107563 QMediaPlayer can't play AVI with Apple codecs  
* QTBUG-108403 FFmpeg backend doesn't work as expected  
* QTBUG-110498 QtMultimedia leaks a lot of memory on Windows when opengl  
contexts are shared  
* QTBUG-110012 QML Video Example: example not displaying video  
* QTBUG-116782 FFmpeg backend: RTSP stream is very choppy in Qt,  
compared to FFplay  
* QTBUG-114954 Media Player Example: Default video does not play on  
Android  
* QTBUG-113980 Playing videos over network still an issue on Android  
* QTBUG-117528 [REG 6.3.2->6.5.2] QMediaPlayer always captures the audio  
device what blocks sleep mode on Windows  
* QTBUG-117612 [REG 6.3.2->6.5.2] Windows 10: CPU core stucks at minimum  
friequency  
* QTBUG-117919 REG: Qt6.7 QML MediaPlayer duration property doesn't  
update declaratively  
* QTBUG-111045 QSoundEffect not playing  
* QTBUG-101364 qmllint spurious error: QML State AnchorChanges: with  
type QQuickAnchorLine to QQmlScriptString of QQmlScriptString  
* QTBUG-118654 QMediaPlayer does not allow negative playback rate hence  
no rewinding possible  
* QTBUG-118510 Errors when building Qt with FFMpeg/vaapi on Ubuntu 20.04  
* QTBUG-108754 Video not stretched properly  
* QTBUG-116020 Audio from QMediaPlayer crackles and stutters on pause  
and resume  
* QTBUG-118080 QDoc cannot distinguish between template function  
overloads differing only  in template arguments  
* QTBUG-117407 Document limitations of QScreenCapture  
* QTBUG-110312 AutoPlay property is missing from QMediaPlayer  
* QTBUG-118668 QTextToSpeech::synthesize under window does not get data  
* QTBUG-118571 Android tests on CI part 1/3 (camera & media  
capture/player)  
* QTBUG-117746 eglfs: Capturing the screen crashes  
* QTBUG-117878 Cannot capture screen from QQuickWidget  
* QTBUG-118099 Volume Discrepancies Between QMediaPlayer and  
QSoundEffect with ffmpeg  
* QTBUG-111815 Bumpy rendering of D3D11 textures  
* QTBUG-121750 QCameraImageProcessing fails to set settings on linux  
v4l2 camera  
* QTBUG-122577 QScreenCapture tests are flaky on OpenSuse 15.5  
* QTBUG-111190 V4L2m2m encoder gets failed on linux  
* QTBUG-122224 [Crash] The audiorecorder example crashes when selecting  
output and start recording  
  
### qttools  
* QTBUG-113863 \typealias not highlighted with a clickable link on  
usages  
* QTBUG-107853 qt6_add_translations() deletes CMake-generated *.ts files  
when project is cleaned  
* QTBUG-114057 QDoc not parsing files with same name  
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
* QTBUG-115720 \value followed by \table merges contents and breaks  
table  
* QTBUG-115537 [QML Docs] Image.fillMode enum documentation has a broken  
table formatting  
* QTBUG-115116 Doc: QObject overview documentation lists incomplete  
signatures of connect  
* QTBUG-114937 Space in \printuntil regex needs to be protected  
* QTBUG-116305 Qt Creator 11.0.2  layout alignment disable  
* QTBUG-116412 QDoc automatically adds links to deprecated methods in  
the see also section of docs  
* QTBUG-115958 Two runs of lupdate are required if -pluralonly is used  
for the native language  
* QTBUG-115578 Maybe TS file format documentation needs a correction?  
* QTBUG-116599 qttools: race condition in test_translation_api CMake  
test  
* QTBUG-116441 qdoc: Pages with multiple \ingroup commands lose  
navigation to parent \group  
* QTBUG-116880 qdoc generates weird info for noexcept() methods  
* QTBUG-117145 Designer FTBFS  
* QTBUG-116335 QMessageBox::options not correctly linked to  
* QTBUG-117214 "Multiple Inheritance" example - medata broken  
* QTBUG-117406 [REG 6.6.0beta4->6.7.0] linguist/i18n and qml/qml-i18n  
not compiling on iOS  
* QTBUG-117510 qdoc: Incorrect links to qhash-proxy.html page  
* QTBUG-116483 qttools' CMake test test_uiplugin_via_designer fails  
* QTBUG-117974 CMake Error at  
qttools/src/assistant/qhelpgenerator/CMakeLists.txt:66  
(add_dependencies)  
* QTBUG-117970 Dependency update on qt/qttools failed in dev  
* QTBUG-117778 QDoc: section commands shadows inherited module state  
* QTBUG-118558 QDoc: DocParser::getRestOfLine no longer strips trailing  
backslashes and whitespace properly  
* QTBUG-118769 lupdate leaves behind .json files if it fails to load pro  
file  
* QTBUG-115166 qt_add_qml_module() causes non-Ninja generators to think  
that projects are never up-to-date  
* QTBUG-116833 QDoc generates .sha1 files for each qhp file, but they  
all contain wrong hash  
* PYSIDE-2492 uic does not generate enumeration name into enum values  
causing type checking warnings  
* QTBUG-119502 Doc - Update required clang version for QDoc  
* QTBUG-119610 QDoc: DocParser::getRestOfLine() doesn't chop trailing  
backslash on Windows  
* QTBUG-119146 qdoc: \relates command is unable to correctly handle  
function overloads  
* QTBUG-119555 [REG] Qt 6.6.1 breaks qt_add_translations  
* QTBUG-120265 QDoc incorrectly generates list of types for  
\compareswith  
* QTBUG-121226 qdoc extraimages.HTML not supported  
* QTBUG-121377 Dependency update on qt/qttools failed  
* QTBUG-118808 qt_add_translations with source autodetection mishandles  
id-based generated UI headers  
* QTBUG-121186 New QSharedPointer methods do not show up under "New  
Classes and Functions"  
* QTBUG-121563 bad license identifier in qttools/src/qdoc/qdoc/tests/gen  
eratedoutput/testdata/templatedcallables/templated_callables.*  
* QTBUG-121850 QDoc: SHA1-files generated for QHP files differ across  
platforms  
* QTBUG-118990 assistant.exe index navigation fails  
* QTBUG-122418 qdoc: validatedqdocoutputfiles test fails address  
sanitizer check  
* QTBUG-123011 wrong xxx_lupdate_project.json is generated when no  
targets are specified in qt6_add_lupdate  
* QTBUG-123109 qdoc fails to compile with clang 18  
* QTBUG-123338 cmake translation handling not backwards compatible  
* QTBUG-123405 [REG 6.6 -> 6.7.0 RC] Translations were generated in the  
wrong folder  
* QTBUG-114707 Qdoc ignores the excludedirs config for example files  
list  
* QTBUG-114862 qdbusviewer shows tab for system bus although no system  
bus is present  
* QTBUG-106380 Hello tr() example exits immediately after being run  
* QTBUG-115448 qttools -unity-build-batch-size 100000 fails  
* QTBUG-115247 \target after \row generates invalid HTML  
* QTBUG-114967 Issues in documentation of \details command  
* QTBUG-116534 Add \examplecategory to qthelp  
* QTBUG-116536 Add \examplecategory to qtassistant  
* QTBUG-111873 qt_attributions.json files should be valid JSON  
* QTBUG-115686 qt5.git build of qttools/examples places .ts files in  
SRCDIR, not BUILDDIR  
* QTBUG-115962 lupdate generates invalid translation  
* QTBUG-111970 qdoc renders fixed-size array parameters incorrectly  
* QTBUG-100374 private pri files are installed for headerless libraries  
* QTBUG-118080 QDoc cannot distinguish between template function  
overloads differing only  in template arguments  
* QTBUG-62697 qhc files cannot be created in a reproducible way  
* QTBUG-120236 macOS: Qt Designer appears on a start on macOS as if it  
was broken  
* QTBUG-120633 REG->6.7: Windows11/Vista palette issues (bright)  
* QTBUG-119051 With Linguist it seems only the last segment from the  
XLIFF is used as translated string.  
* QTBUG-120531 lupdate doesn't understand template literals  
* QTBUG-121906 Copyright year in so files not updated to 2024  
* QTBUG-122616 Qt Designer: Invalid path:  
'/.designer/backup\backup2.bak.' when saving the backup file.  
* QTBUG-122691 Dependency update on qt/qttools failed in 6.7  
* QTCREATORBUG-30427 Crash in help  
* QTCREATORBUG-30459 [REG 12.0.2 -> 13.0] Help mode resizes incorrectly  
  
### qttranslations  
* QTBUG-115634 qttranslations configure takes ages on CMake 3.27  
  
### qtdoc  
* QTBUG-113588 Check attribution details for opengl32sw.dll  
* QTBUG-114210 [REG 6.5.1->6.6.0] demos/photosurface not launching  
* QTBUG-114365 [REG 6.6.0->6.5.1] demos/documentviewer not compiling on  
macOS  
* QTBUG-99900 Leading zeroes for Android app "versionCode" are being  
removed  
* QTBUG-114529 ANDROID_NDK_ROOT example has wrong version  
* QTBUG-114592 todolist demo fails to configure  
* QTBUG-114370 documentviewer demo causes lots of warnings when building  
on iOS  
* QTBUG-114618 [DocumentViewer] Cannot view any document on macOS  
* QTBUG-114614 [DocumentViewer] Content of PDF file could not be viewed  
on Linux  
* QTBUG-114620 [DocumentViewer] Toolbar icons are not visible on macOS  
* QTBUG-114615  [DocumentViewer] Edit menu gets multipled each time  
recent document is opened  
* QTBUG-114617 [DocumentViewer] Document specific handlers remain on the  
screen when changing document type  
* QTBUG-114759 add_library cannot create target "CustomControls" because  
another target with the same name already exists  
* QTBUG-115961 Documentation about building Qt for iOS from source  
requires corrections  
* QTBUG-115988 Doc: Lots of broken links to 'Plug & Paint example'  
* QTBUG-114998 Example can't run, missing module  
* QTBUG-113300 The documentation "How to Create Qt Plugins" seems to  
need a review and update  
* QTBUG-116149 Deploying QML Applications: wrongly instructs to use  
declarative instead of quick  
* QTBUG-116580 "Selected Material Icons" attribution shown twice  
* QTBUG-110846 Internationalization with Qt: Mention retranslateUi  
* QTBUG-110921 Documentation for building iOS apps is plain wrong  
* QTBUG-116987 DocumentViewer example broken because QPdfPageSelector is  
no longer a QSpinBox subclass  
* QTBUG-117691 DocumentViewer example does not find plugins at runtime  
* QTBUG-117694 Document Viewer example could not be build on Qt 6.7.0  
* QTBUG-54267 Qt Quick Calqlatr example does not properly reflect the  
current way of using Qt Quick  
* QTBUG-111272 "Porting to Android" only covers qmake  
* QTBUG-117089 qt_add_qml_module - what has changed between versions?  
* QTBUG-118104 Typo in the document  
* QTBUG-118577 Android Docs has non-compiling code-snippet.  
* QTBUG-118211 Generation of alias targets for executable needs to be  
guarded  
* QTBUG-118043 QML Media Player doesn't fit on smaller screens  
* QTBUG-118754 assertObjectType is triggered with a correct signal/slot  
connection on macOS  
* QTBUG-118672 [DocumentViewer] Cannot open PDF files using the app.  
* QTBUG-119286 Typos in Thermostat example  
* QTBUG-119297 Room icons in Thermostat example not correct  
* QTBUG-119320 Thermostat example buttons inactive  
* QTBUG-119294 Settings tab in Thermostat example behaves oddly  
* QTBUG-119290 Icon highlighting in Thermostat example is barely visible  
* QTBUG-117647 Audio track is not played when opening audio file after  
playing video file in media player example  
* QTBUG-119996 Demo hangman don't work on Qt6.7  
* QTBUG-117090 CMake docs: incorrect code example for  
qt_generate_qml_app_script  
* QTBUG-119175 [DocumentViewer] The app crashes when opening 3d model  
file (obj)  
* QTBUG-120372 Typo in the document  
* QTBUG-119458 Initializing with QQuickView is missing cmake instruction  
* QTBUG-120364 [6.7 beta1] Qt Dice demo crashes on Android devices  
* QTBUG-120471 Fix minor issues in stocqt  
* QTBUG-121165 Error in WebAssembly documentation  
* QTBUG-120230 'coffee' fails when cross-compiling on Windows  
* QTBUG-112024 Robotarm fails to launch on embedded devices  
* QTBUG-121044 Calqlatr example not scaling properly in landscape mode  
* QTBUG-121524 [REG 6.6.1 -> 6.6.2] StocQt CMake error for Android  
* QTBUG-121660 Calqlatr example missing naming for Android package  
* QTBUG-119285 MediaPlayerApp-Desktop-Example Scrolling issues when  
using the mousewheel  
* QTBUG-121940 [DocumentViewer] The app crashes when clicking print  
button after opening several various files  
* QTBUG-121578 demos/hangman fails to build on Android and macOS  
* QTBUG-120643 [REG 6.2.4 -> 6.5.3] "Classes" page is empty  
* QTBUG-122258 [REG 6.6.1->6.7.0] demos/stocqt not compiling  
* QTBUG-122657 Demos/StocQt has runtime QML import errors  
* QTBUG-122299 Calqlatr application fails to run on Boot2Qt devices  
* QTBUG-122178 [Media Player Example] App hangs when previous track is  
clicked  
* QTBUG-122767 QTP0001 warning for FX & Material Showroom example  
* QTBUG-122569 Calqlatr example package name not unique  
* QTBUG-122444 Qt Dice Example: The control menu's lower half is cut off  
in landscape mode  
* QTBUG-123164 New example demos/osmbuildings not compiling on Android  
* QTBUG-114396 Change "OpenGL" to "Graphics API"  
* QTBUG-115108 FX_Material_Showroom fails to compile due to long paths  
* QTBUG-115247 \target after \row generates invalid HTML  
* QTBUG-115958 Two runs of lupdate are required if -pluralonly is used  
for the native language  
* QTBUG-88264 [REG v6.0.0-beta3 -> dev] Top-level configure fails if  
told to build tests  
* QTBUG-114447 6.5.0 version string found in 6.6.0 sources  
* QTBUG-79353 qtbase and qtxmlpatterns do not build if GUI module  
disabled  
* QTBUG-116784 iOS built with CMAKE is not uploadable on Appstore  
(Transporter)  
* QTBUG-114437 REG: Android: Layout in display cut mode being overridden  
to short edges always  
* QTBUG-96877 Qt6 won't render into cutout area (regression)  
* QTIFW-3139 Online Installer 4.6.1 : Command Line Interface "-default-  
answer" "--accept-messages" doesn't work together  
* QTBUG-114375 User got stuck and is not taken back to the home in  
coffee example  
* QTBUG-117651 The Webassembly documentation has an incorrect  
target_link_options  
* QTBUG-118181 Version 6.6.0 in 6.7.0 documentation  
* QTBUG-114713 Enhancements in the Color Palette REST API example  
* QTBUG-118789 Target Devices used in Automated Testing is out-dated  
* QTBUG-116489 tutorials/alarms not compiling  
* QTBUG-115373 Hangman Demo uses unsupported version of Google Play  
Billing Library  
* QTCREATORBUG-30077 TodoList example app does not work out of the box  
* QTBUG-120014 Dependency for libxcb-cursor0 since Qt 6.5 is not  
mentioned in the documentation.  
* QTBUG-119176 [DocumentViewer] Content of model file could not be  
viewed in the app  
* QTBUG-121412 Make sure that QtLocation examples use new QPermissions  
API  
* QTBUG-122041 [DocumentViewer] The app is crashing when opening the  
file on Android device  
* QTBUG-123543 Incomplete docs about the status of Linux on ARM desktops  
in 6.7  
  
### qtlocation  
* QTBUG-115359 QGeoManeuver is exported twice  
* QTBUG-117404 [REG 6.6.0beta4->6.7.0] location\geojson_viewer not  
compiling on Android  
* QTBUG-118447 Here plugin does not support authentication via apiKey  
* QTBUG-121766 GeoJsonViewer example cannot open files.  
* QTBUG-123112 GeoJson Viewer example doesn't show maps on Android  
* QTBUG-114080 QML module documentation should move out of "List of  
types" page  
* QTBUG-121412 Make sure that QtLocation examples use new QPermissions  
API  
  
### qtpositioning  
* QTBUG-114657 [SatelliteInfo] The app stops responding after some time  
on macOS  
* QTBUG-115361 QGeoSatelliteInfo is exported twice  
* QTBUG-116645 [Android] providerList() returns NULL list  
* QTBUG-118739 The SatelliteInfo demo app is constantly crashing  
* QTBUG-113752 Warning when assigning to Map.visibleRegion  
* QTBUG-114080 QML module documentation should move out of "List of  
types" page  
* QTBUG-115217 NMEA SatelliteInfo Simulation mode stops providing  
updates  
* QTBUG-116920 FAIL!  : tst_QGeoAreaMonitorSource::tst_monitor() 'obj !=  
nullptr' returned FALSE.  
  
### qtconnectivity  
* QTBUG-113318 QBluetoothLocalDevice::pairingStatus always returns  
status unpaired  
* QTBUG-116341 error C2475: 'qbswap': redefinition; 'constexpr'  
specifier mismatch  
* QTBUG-116563 [REG 6.4 -> 6.5] ISO7816 smart cards are considered to be  
NDEF tags  
* QTBUG-115370 Android device (Android12 Go Edition) cannot reconnect  
to BLE peripheral device  
* QTBUG-118895 No signals are emmited after error Failed to create  
pairing "org.bluez.Error.AuthenticationCanceled"  
* QTBUG-105526 NFC polling interval  
* QTBUG-119060 Read access violation when calling stop() during  
Bluetooth service discovery  
* QTBUG-119063 Segfault in Bluetooth module's Windows COM de-init  
* QTBUG-120410 NDEF Editor Example - Clicking on 'read tag' will erase  
existing records  
* QTBUG-116580 "Selected Material Icons" attribution shown twice  
* QTBUG-118080 QDoc cannot distinguish between template function  
overloads differing only  in template arguments  
  
### qtwayland  
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
* QTBUG-117069 ERROR: AddressSanitizer: stack-use-after-scope in  
tst_WaylandCompositor::emitsErrorOnSameIviId()  
* QTBUG-117067 ERROR: AddressSanitizer: heap-use-after-free in  
tst_seatv4::animatedCursor()  
* QTBUG-117068 ERROR: AddressSanitizer: heap-use-after-free in  
tst_primaryselectionv1  
* QTBUG-117932 Crash in texture orphanage  
* QTBUG-112161 Drag and drop with wayland display error  
* QTBUG-118042 cannot forward key event from compositor to client  
* QTBUG-111022 Custom Extension example not working on NVIDIA  
* QTBUG-118650 Qt wayland may freeze with no available buffer in  
QWaylandShmBackingStore if window show/hide very fast  
* QTBUG-119110 There are potential crash issues when some submenus are  
expanded.  
* QTBUG-119177 The app exits abnormally (exit code 255) when dragging  
the toolbar in widgets app  
* QTBUG-118612 Large size cursor overlaps tooltips on linux  
* QTBUG-119882 tst_QWindow::setVisibleThenCreate() failed on Wayland  
* QTBUG-119883 tst_QWindow::windowExposedAfterReparent() failed on  
Wayland  
* QTBUG-119136 qt creator does not restore to maximized state when  
minimized from maximized state  
* QTBUG-118890 QWaylandWindow::reset() mutex race/deadlock with  
QWaylandWindow::beginFrame()  
* QTBUG-120171 Inactionable warning: QWaylandTextInputV3: Input protocol  
"text-input-unstable-v3" does not support querying input direction. Use  
qt-text-input-method-unstable-v1 instead for full support of Qt input  
method events.  
* QTBUG-120393 The link is ill formed in the document  
* QTBUG-120392 QWayland CSD window has unclickable area  
* QTBUG-120397 "output" property seems to be missing in WaylandQuickItem  
QML type documentation  
* QTBUG-120477 Overriding swap interval for Wayland EGL windows doesn't  
work  
* QTBUG-105703 QWaylandWindow::createDecoration() is called from  
multiple threads  
* QTBUG-120533 Various runtime warnings about Wayland text input  
* QTBUG-121399 tst_QWizard::task177022_setFixedSize() failed on Wayland  
* QTBUG-116600 The Virtual keyboard is not hidden when the TextField  
loses focus on the Wayland client.  
* QTBUG-122965 Qt 6.5.4 don't generate XDG_RUNTIME_DIR  
* QTBUG-113145 Gesture handlers crash due to misbehaving compositors  
* QTBUG-115101 WaylandGlobalPrivate_sync_headers is not running if  
nothing depends on WaylandGlobalPrivate  
* QTBUG-116340 Add \examplecategory for Qt Wayland Compositor examples  
* QTBUG-120035 [weston] Setting fixed size for the main level widget  
crashes the application when maximized  
* QTBUG-95817 Quick windows break  on nvidia wayland when resized  
  
### qt3d  
* QTBUG-113314 QSkyboxEntity does not render when using the (default)  
RHI backend  
* QTBUG-112739 Qt3DExtras::QSkyboxEntity is broken  
* QTBUG-97751 Crash when loading .obj files with empty lines - out of  
bounds array access in objgeometryloader.cpp  
* QTBUG-100386 Crash in GLTFImporter::commonMaterial  
* QTBUG-112706 skinningPalette uniform is not uploaded to shaders in the  
Qt 3D RHI backend  
* QTBUG-116229 Please fix Qt3DCore documentation  
* QTBUG-116354 Qt3D - Enable texture array  
* QTBUG-114037 [Android] Could not launch any app with Qt 3D module on  
Android 12  
* QTBUG-114036 [Android] Qt3D.Renderer.RHI.Backend: : Failed to build  
graphics pipeline: Creation Failed  
* QTBUG-116770 Race Condition or Crash in Qt3D due to Thread Affinity of  
NodePostConstructorInit::processNodes()  
* QTBUG-118399 https://doc.qt.io/qt-6/qt3drender-qmaterial.html example  
code misses parentheses  
* QTBUG-116494 Documentation for QCylinderMesh misses Detailed  
Description  
* QTBUG-77665 Phong fragment shader does not account correctly for  
ambient color  
* QTBUG-120241 Incorrect handling of ambient color in phong shaders in  
qt3d (Regression)  
* QTBUG-119657 Double free with RHI resources while using Qt3D compute  
* QTBUG-115025 QPerVertexColorMaterial does not work with Direct3D  
* QTBUG-77139 QText2DEntity isn't working with parent entity in  
constructor  
* QTBUG-100387 QText2DEntity does not create any geometry in certain  
cases  
* QTBUG-120964 delayed creation of QAttribute with parent in constructor  
causes crash  
* QTBUG-119659 Qt3D RHI - Uniform buffers not bound for compute shaders  
* QTBUG-111427 Race condition in UniformBlockValueBuilder  
* QTBUG-122613 QPaintedTextureImage in a Texture2D crashes with size  
256x256  
* QTBUG-121702 Manual testing - buffercapture-qml crashes immediately  
upon start  
* QTBUG-117065 ERROR: AddressSanitizer: memcpy-param-overlap in  
tst_AspectCommandDebugger::checkBufferTrim()  
* QTBUG-119137 ERROR: AddressSanitizer: heap-use-after-free in  
tst_qmesh::checkSourceUpdate() in qt3d  
* QTBUG-118080 QDoc cannot distinguish between template function  
overloads differing only  in template arguments  
* QTBUG-69463 Camera view matrix computation unstable (regression)  
* QTBUG-123483 Qt3D: Fix Stereo back buffer selection  
  
### qtimageformats  
* QTBUG-118797 ICNS format: QImageReader::setAllocationLimit() bug  
  
### qtserialbus  
* QTBUG-114043 QCanDbcFileParser incorrectly parses 29-bit (extended)  
CAN IDs  
* QTBUG-113538 QCanBus not decoding CAN Frames correctly on Mac.  
* QTBUG-114619 QCanDbcFileParser fails to parse non-ASCII characters  
like '°'  
* QTBUG-99259 vectorcan can not receive and send CAN-FD message  
* QTBUG-114397 QCanDbcFileParser will not parse signals with certain  
valid utf-8 encoded characters  
  
### qtserialport  
* QTBUG-117887 QSerialPort::bindableStopBits has a wrong return value  
* QTBUG-120412 Blocking receiver example - Will crash when clicking  
'start' if no Serial port is selected  
* QTBUG-115205 QSerialPort does not properly set baud rate  
  
### qtwebsockets  
* QTBUG-92858 When connecting to a web socket server via a ngnix proxy  
then it will fail to connect since it is not requesting the  
authentication  
  
### qtwebchannel  
* QTBUG-115738 FAIL!  :  
qml::WebChannelSeparation::test_signalSeparation() Compared values are  
not the same  
* QTBUG-115779 Webchannel's standalone example doesn't work when opened  
with CMake  
  
### qtwebengine  
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
* QTBUG-115369 QWebEngine can not render page content and throw `Fatal  
error` in console  
* QTBUG-114875 Cannot detect Visual Studio when configuring QPdf and  
QWebEngine  
* QTBUG-115476 QPdfPageSelector doesn't actually handle non-numeric page  
label input  
* QTBUG-115713 [REG 6.6.0 beta2->beta3] QtPDF and QtWebengine not  
compiling from sources on MSVC2019  
* QTBUG-115365 QWebEngineCertificateError is exported twice  
* QTBUG-115844 qtwebengine ignores some key remaps  
* QTBUG-115976 Dev tools not hidden with closing cross  
* QTBUG-111541 QWebEngineProfile::clearHttpCache() can subsequently  
cause QWebEnginePage::load() to hang  
* QTBUG-99555 [RE: 6.2.1->6.2.2] macdeployqt fails to produce  
notarizable packages  
* QTBUG-115703 QtWebEngine 6.6.0 crashes on Windows  
* QTBUG-116042 configure fails when BUILDDIR path contains "++"  
* QTBUG-116278 [REG 6.6.0 beta2-> beta3] QtWebengine not compiling on  
macOS11  
* QTBUG-73994 Changing input method with shortcut key causes hang on  
WebEngine  
* QTBUG-116839 [B2Qt 6.6.0-beta4 snapshot] qtpdf and qtwebgine missing  
from imx8qmmek and jetson-agx-xavier-devkit  
* QTBUG-116159 Reg 6.4->6.5 QWebView with Q3DSurfaces does not renders  
* QTBUG-115722 [REG 6.6.0 beta2->beta3] QtWebengine not compiling from  
sources on SLES15_SP4  
* QTBUG-116738 qtwebengine Address Sanitizer test run: stack-use-after-  
return in tst_QQuickWebEngineView::savePage(SingleHtmlSaveFormat)  
* QTBUG-116445 [REG][Windows] Crash on  
NativeSkiaOutputDevice::releaseTexture() with nullptr access  
* QTBUG-115994 Duplicate character when long-pressing for accented char  
on macOS/webengine  
* QTBUG-115753 ERROR: AddressSanitizer: heap-use-after-free  in  
tst_origins  
* QTBUG-117119 Some Qt WebEngine documentation issues  
* QTBUG-117489 [REG 6.4 -> 6.5] Invalid QDataStream data when  
serializing uninited QWebEngineHistory  
* QTBUG-117031 qmllint: Missing type information for WebEngine  
* QTBUG-117658 QWebEnginePage property url is missing NOTIFY, not-usable  
from QML  
* QTBUG-118505 REG: Qt WebEngine debug-and-release builds broken on  
macOS.  
* QTBUG-117751 building with -no-opengl produces errors in  
web_engine_context.cpp  
* QTBUG-117867 QWebEngineNewWindowRequest::openIn() breaks page  
interceptor  
* QTBUG-117741 libvpx is not used  
* QTBUG-118455 Crash in Compositor::Observer::compositor() with nullptr  
access  
* QTBUG-118655 Manual Deployment document of QtWebengine needs little  
update.  
* QTBUG-119023 WebEngine accessibility crash when clicking on a link in  
a list on macOS  
* QTBUG-113859 [REG 6.4->6.5] Accessibility crash when clicking on a  
link in a list on macOS  
* QTBUG-119525 error: field ‘responseHeaders’ has incomplete type  
‘QMultiMap<QByteArray, QByteArray>’  
* QTBUG-115357 qt 6.5.2 fails to build from source with system libpng  
(regression from 6.5.1)  
* QTBUG-119536 Lack of documentation regarding QPdfBookmarkModel's  
document property  
* QTBUG-118995 Dev tools not working  
* QTBUG-119789 [Accessibility] Qt 6.5.3 cannot be built with the option  
' -no-feature-accessibility''.  
* QTBUG-112142 [Qt WebEngine] ScreenCapture should provide a way to  
select window/screen to capture  
* QTBUG-86869 Unrecognized Chrome version when using Selenium and  
Chromedriver  
* QTBUG-118398 QWebEngineView in QScrollArea is not scrollable  
* QTBUG-118120 qtwebengine: build failure with x86_64h  
* QTBUG-119776 PDF Multipage viewer example - Clicking on previous  
(upward arrow) will crash the example  
* QTBUG-120446 Alternated item color in list is not always alternated  
* QTBUG-119722 [REG 5 → 6] Default context menu is missing icons  
* QTBUG-104766 QtQuick.Pdf PdfDocument gets  
"QCoreApplication::postEvent: Unexpected null receiver" warning when  
instantiated standalone  
* QTBUG-120245 A crash occurred in C:\Users\qt\work\qt\qtwebengine_stand  
alone_tests\tests\auto\pdfquick\multipageview\tst_multipageview.exe  
* QTBUG-104767 Using PdfPageImage instead of Image on PDF file results  
in EXC_BAD_ACCESS (SIGSEGV)  
* QTBUG-119245 Qt Web Engine alert quotes not working  
* QTBUG-83338 Default implementations of javaScriptAlert/Confirm/Prompt  
treat message as rich text  
* QTBUG-119991 Unable to print at all if the first page of multi page  
document is not printed  
* QTBUG-118746 Japanese input on macOS regressed in Qt 6.5.3  
* QTBUG-120218 QML WebEngineView.printToPdf(): paper formats are wrong  
in the resulting document  
* QTBUG-115502 PdfMultiPageView: repeated pinch-zooming jumps to wrong  
zoom level  
* QTBUG-121564 tst_MultiPageView::pinchDragPinch is flaky  
* QTBUG-121502 crash in QPdfIOHandler if document is deleted too early  
* QTBUG-119416 Loading a specific page in a PDF document does not always  
show the correct page  
* QTBUG-120689  
tst_qwebenginepage::getUserMediaRequestDesktopVideoManyPages is flaky  
* QTBUG-120273 QWebEngineView shows blank content on initial show when  
page bg set to transparent  
* QTBUG-121227 QWebEngineView shows blank content on initial show when  
page bg set to transparent  
* QTBUG-112013 QWebEnginePage.setBackground(Qt::black) doesn't work for  
page loading.  
* QTBUG-120926 QWebEnginePage::setBackgroundColor doesn't work properly  
* QTBUG-122153 QWebEngineView::setFocus() doesn't give focus to the view  
after calling QWebEngineView::load() for the second time  
* QTBUG-122137 REG: QtWebEngine / Pdfwidgets no longer supports plugins  
* QTBUG-121589 Can't build qt6 due to failed ozone platform assertion  
* QTBUG-118035 QtWebengine build fails on pure wayland  
* QTBUG-113416 [Reg 6.4->6.5] Static build fails at PDF module  
* QTBUG-113551 Update documentation for limitation building QtPdf for  
Android with supported  LTS versions  
* QTBUG-114367 QtPdf API review  findings  
* QTBUG-105342 Test on qemu are very flacky  
* QTBUG-85731 Screen sharing does not work on Google Meet  
* QTBUG-113369 dark mode enabled causes crashes on specific sites  
* QTBUG-104610 Does WebEngine support document download and print  
operations in the document preview screen?  
* QTBUG-115188 QtWebEngine use after free in Extensions GetPreferences  
* QTBUG-113149 PDF download  from pdf viewer not working  
* QTBUG-116165 FAIL!  :  
tst_QWebEnginePage::acceptNavigationRequestNavigationType()  
'expectedList.size() == page.navigations.size()' returned FALSE.  
* QTBUG-100417 [REG 5.15->6.3] Multiple context menus can be opened with  
synthetic touch events  
* QTBUG-113463 Build issues with symlinks  
* QTBUG-114859 When saving an mhtml page  
QWebEngineDownloadRequest::isSavePageDownload() returns false  
* QTBUG-116478 [Reg 5.14.2 -> 5.15.0] Significant performance decrease  
when loading QtWebEngine pages simultaneously in many windows  
* QTBUG-117624 Minor issues of QWebEngineDownloadRequest  
* QTBUG-116565 Cannot sign a WebEngine-based application with Qt 6.5.2  
(but OK with Qt 6.4.3, 6.3.2, 5.15.2)  
* QTBUG-117752 QWebEngineUrlRequestInterceptor not called on page, if  
the one set on the profile changed the info  
* QTBUG-118750 REG: QQuickItem::setParentItem to null triggers  
tst_qmltests crash  
* QTBUG-114865 macos: Building QtWebEngine  with sanitizer enabled fails  
* QTBUG-111873 qt_attributions.json files should be valid JSON  
* QTBUG-117707 MinGW 13.1.0: FAILED:  
obj/third_party/icu/bundled_icuuc_private/putil.o  
* QTBUG-116595 QtPfd build failure on 32-bit arm  
* QTBUG-119763 [REG 6.5.2?] Rare segfaults in  
QWebEngineDownloadItem::page()  
* QTBUG-119878 [Reg 5.15->6.x] Crash and/or bad output when printing via  
Qt WebEngine's PDF plugin  
* QTBUG-119077 CMake deployment API does not deploy Qt Webengine  
* QTBUG-120692 Cannot cross-compile webengine for x86_64  
* QTBUG-86948 When using QImageReader to load a PDF then the PDF images  
can be blurry and seem to be at half the size they should be  
* QTBUG-120420 QtWebEngine inspector crashes  
* QTBUG-120764 PDF Viewer Widget example search error  
* QTCREATORBUG-30308 QtCreator is not able to debug pdb files when lib  
linked with pdbpagesize  
* QTBUG-120414 Recipe Browser example crashes  
* QTBUG-122699 Failed DCHECK in v8 when watching livestream  
  
### qtwebview  
* QTBUG-69801 Qml WebView on Android eats touch events  
* QTBUG-119356 WebViewSettings QML Type documentation of  
javaScriptEnabled property has a spelling mistake  
* QTBUG-112346 qmllint fails when WebView is used  
* QTBUG-114495  FAIL!  : tst_QWebView::load()  
  
### qtcharts  
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
* QTBUG-113437 QML XYSeries bestFitLineColor doc type  
* QTBUG-118322 Fix licensing of Qt Charts examples  
* QTBUG-115274 "Qml Wheather" example causes 'Too many arguments'  
runtime error  
* QTBUG-118669 Qt chart crash on showing context menu  
* QTBUG-114814 QColorAxis::setVisible method is not behaving as  
expected.  
* QTBUG-119712 QChartView prevents parent QScrollView from receiving  
touch screen scroll events.  
* QTBUG-77403 Scrolling via trackpad does not work on Chart  
* QTBUG-119900 Deleting a visible QAbstractSeries with OpenGL enabled  
causes an error  
* QTBUG-114080 QML module documentation should move out of "List of  
types" page  
* QTBUG-116535 Add \examplecategory to qtcharts (1 update left)  
* QTBUG-120282 Configuring qtcharts from sources fails because of  
dependency cycle  
  
### qtdatavis3d  
* QTBUG-114178 Transparency in gradient results in weird stripes  
* QTBUG-114852 tst_qmltest_datavis test is flaky  
* QTBUG-122185 Manual testing - itemmodeltest crashes  
  
### qtvirtualkeyboard  
* QTBUG-116078 [REG] Behavior breakage in Qt 6.5: Virtual keyboard style  
qrc import path changed  
* QTBUG-108030 Virtual keyboard basic example freezes on Android  
* QTBUG-118324 Fix licensing of Qt VirtualKeyboard basic example  
* QTBUG-116432 Virtual keyboard import version number from Qt 5.15 does  
not work in Qt 6.5 version  
* QTBUG-118565 VirtualKeyboard documentation incorrect  
* QTBUG-121658 Virtual keyboard example crashes after startup on Android  
* QTBUG-111873 qt_attributions.json files should be valid JSON  
* QTBUG-120262 Use SPDX-License-Ref in 3rdparty directories  
* QTBUG-121643 qt6-declarative: possible build-time race condition  
around qmlcachegen  
  
### qtscxml  
* QTBUG-118050 Empty script element ends up invoking Q_UNREACHABLE()  
* QTBUG-119562 StateMachine Documentation wrong  
* QTBUG-120576 The Note is duplicated for EventConnection::occurred  
* QTBUG-120578 The date type of "event" in occurred should be specified  
* QTBUG-120262 Use SPDX-License-Ref in 3rdparty directories  
  
### qtspeech  
* QTBUG-115363 QVoice is exported twice  
* QTBUG-113820 Can't run Quick Speech Example on Android  
* QTBUG-117516 [Qt TextToSpeech] Cannot get the list of languages on  
android device  
* QTBUG-117824 configure -no-gui fails to build  
* QTBUG-118668 QTextToSpeech::synthesize under window does not get data  
* QTBUG-120655 tst_qtexttospeech (Failed)  
* QTBUG-122950  FAIL!  :  
tst_qtexttospeech_qml::Voice::test_default_voice() Compared values are  
not the same  
* QTBUG-122884 QML TextToSpeech enqueue does not work with Darwin engine  
* QTBUG-122900 Android App dies immediately if I add TextToSpeech to the  
project  
  
### qtnetworkauth  
* QTBUG-117680 NetworkAuth examples do not show up in Qt Creator  
  
### qtremoteobjects  
* QTBUG-114664 QRemoteObjectReplica::state() has incorrect description  
* QTBUG-115458 QRemoteObjectRegistry has incorrect info about  
QRemoteObjectSourceLocation(s)  
* QTBUG-116151 Replica can crash with QHostAddress being called with a  
<null reference>  
* QTBUG-117379 [REG: 5->6] Enums with ENUM in the type name cause error  
in repc  
* QTBUG-119870 verror: static assertion failed: QQnxNativeIo is neither  
copy- nor move-constructible  
* QTBUG-120242 SubClassReplicaTest crashes  
* QTBUG-118080 QDoc cannot distinguish between template function  
overloads differing only  in template arguments  
  
### qtquicktimeline  
* QTBUG-119204 Not possible to exclude qtquicktimeline from the build  
* QTBUG-119673 6.7.0 static build fails on MSVC2019, timeline  
  
### qtquick3d  
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
* QTBUG-113164 Crash when you have two models with same mesh in the  
scene, one with BakedLightmap and one without  
* QTBUG-116136 Memory leaks in Loader qml component  
* QTBUG-117619 [REG] Frustum culling broken in 6.6  
* QTBUG-117023 Picking and rotating don't work on bars after clicking  
buttons  
* QTBUG-118404 Unable to replicate PrincipledMaterial Behaviour with  
CustomMaterial (no way to specify separate blend factors)  
* QTBUG-118659 [REG 6.6.1 previous snapshot->6.6.1] example  
quick3d/proceduraltexture not launching  
* QTBUG-118806 Exporting functionality in the material editor is broken  
* QTBUG-118773 Baking emissive materials without shadow  
* QTBUG-119373 typo in the document  
* QTBUG-120579 The link to the Fog QML type is not correct  
* QTBUG-120431 QQ3DPhysics customshapes example looks different on  
opengl vs d3d11  
* QTBUG-120629 Baking Lightmap fails with msvc2019 kit  
* QTBUG-120424 Segmentation fault in the process of loading/unloading 3D  
objects  
* QTBUG-121390 Live Preview with a 3D project crashes on with Qt 6.6.1  
* QTBUG-121568 quick3d/extensions/stenciloutline not launching on linux  
& windows  
* QDS-11396 Node QML type from QtQuick3D is not available in Components  
* QTBUG-122143 balsam ktx build error with ASAN build  
* QTBUG-108755 [REGRESSION] number of drawcalls don't show up in QML  
profiler  
* QTBUG-123015 When configuring with -no-qml-debug then it will fail to  
build QtQuick3D  
* QTBUG-113982 fieldOfViewOrientation property is written twice in the  
PerspectiveCamera's documentation  
* QTBUG-115450 qtquick3d -unity-build-batch-size 100000 fails  
* QTBUG-116911 tst_surfacetest massive data test crash  
* QTBUG-111873 qt_attributions.json files should be valid JSON  
* QTBUG-120279 Cyclic dependency error in qtquick3d  
* QTBUG-120109 WasdController: Models stutter in Qt Quick 3D Physics  
example  
  
### qtshadertools  
* QTBUG-114113 qtshadertools contains two copies of spirv.hpp and  
they're different  
* QTBUG-117780 qt_add_shaders is not executed if the target does not  
exist  
* QTBUG-120513 Apps crash on shader compile on INTEGRITY (6.7 beta 1)  
  
### qt5compat  
* QTBUG-115467 Qt 6 QML Documentation: Wrong example for  
"verticalOffset"  
* QTBUG-117825 [REG 6.6.0 RC->6.6.0] static build on macOS fails,  
qt5compat(?)  
* QTBUG-116981 QTextCodec::toUnicode() behavior changed  
* QTBUG-118080 QDoc cannot distinguish between template function  
overloads differing only  in template arguments  
  
### qtcoap  
* QTBUG-115501 [Qt CoAP] CI integrations pass even when the tests fail  
  
### qtmqtt  
* QTBUG-104478 Mqtt topic wildcard failure  
  
### qtopcua  
* QTBUG-117681 qtopcua is confused about SSL and OpenSSL  
* QTBUG-120911 Qt OPC UA landing page misses license information  
* QTBUG-122277 QtOpcUa does not compile using VS2022 17.9.0 on "subst"  
drive  
* QTBUG-106285  
Tst_QOpcUaSecurity::connectAndDisconnectSecureUnencryptedKey fails with  
RHEL 9 in QtOpcua  
* QTBUG-113504 [MSVC] Qt6 failed to build due to error C2362 on Windows  
with option /permissive-  
* QTBUG-75555 Missing test for event filters  
* QTBUG-116545 QOpcUaClient::connectionSettings getter and setter not  
documented  
* QTBUG-111602 OpenSSL 3.0 use-of-deprecated-function warnings  
* QTBUG-120960 "Backend support" table in QOpcUaMonitoringParameters is  
confusing  
* QTBUG-123094 Dependency update on qt/qtopcua failed in 6.7.0  
  
### qtlanguageserver  
* QTBUG-118201 namespace "std" has no member "exception_ptr"  
  
### qthttpserver  
* QTBUG-119405 QHttpServer terribly slow file transfer  
* QTBUG-121219 QtHttpServer crashes when during GET of a larger content  
remote closes connection  
* QTBUG-120746 QWebSocket immediately disconnects after without  
receiving anything  
* QTBUG-114713 Enhancements in the Color Palette REST API example  
  
### qtquick3dphysics  
* QTBUG-114183 Collision shape calculates orientation incorrectly when  
parent has scale  
* QTBUG-114111 Crash when destroying a body with scale  
* QTBUG-115539 Missing dependencies in qmldir  
* QTBUG-114114 PhysX has ODR violations  
* QTBUG-117058 ERROR: AddressSanitizer: heap-use-after-free in  
tst_callback  
* QTBUG-111922 Support specifying number of threads used for simulation  
* QTBUG-120045 Application crashes in Qt Quick 3D Physics  
* QTBUG-120569 TriangleMeshShape geometry does not cook good, when  
TexCoordSemantic used.  
* QTBUG-121033 onBodyContact being called after object is deleted  
* QTBUG-111565 CharacterController does not receive Contact Reports  
  
### qtgrpc  
* QTBUG-114237 undefined symbol: QGrpcChannelOptions::metadata() const  
* QTBUG-114409 FAIL!  : tst_qtprotobufgen::cmakeGeneratedFile(nopackage_  
protobuftyperegistrations.cpp) 'generatedFile.exists()' returned FALSE.  
()  
* QTBUG-114799 QtProtobuf::Any::fromMessage() does not compile  
* QTBUG-114816 serialization/deserialization of Any fails  
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
* QTBUG-116258 magic8ball example need documentation adjustments  
* QTBUG-116463 qt_add_protobuf() broken in 6.6.0-beta3 for VS2019 build  
system  
* QTBUG-116461 qt_add_protobuf() broken in 6.6.0-beta3 for WASM  
* QTBUG-115708 windows build failure when using protobuf  
GENERATE_PACKAGE_SUBFOLDERS  
* QTBUG-116631 FAILED:  
qtgrpc/src/grpcquick/CMakeFiles/qch_top_level_docs_GrpcQuick  
* QTBUG-116679 -feature-protobuf-wellknowntypes not working for WASM  
* QTBUG-109332 qtprotobufgen generated invalid include when generating  
code from .proto file with no package  
* QTBUG-117066 ERROR: AddressSanitizer: heap-use-after-free in  
QtGrpcClientServerStreamTest::Deadline()  
* QTBUG-116640 Protobuf generator doesn't support C++ keywords field  
names  
* QTBUG-118321 GRPC Chat example fails to build  
* QTBUG-118996 Memory leak in qprotobufserializer.h  
* QTBUG-118097 Port away from nested event loops  
* QTBUG-119227 Segfault assigning to a moved-out protobuf message  
* QTBUG-119013 Oneof properties are duplicated by QML aliases  
* QTBUG-119244 Non-packed repeated fields do not preserve the order when  
making roundtrip as unknown fields  
* QTBUG-120227 AddressSanitizer: heap-use-after-free in QtProtobufRepeat  
edTypesJsonDeserializationTest::RepeatedComplexMessageTest()  
* QTBUG-120432 Protobuf: Nested enums lack their protobuf and metatype  
regestering  
* QTBUG-120426 Document QGrpcRpcInfo::ReplyType  
* QTBUG-120945 QGrpcChannelOptions::withMetadata  
* QTBUG-121507 Qt GRPC in  "All Modules" does not link to landing page  
* QTBUG-121429 qtprotobuf.html:  Clash between C++ namespace and group  
documentation  
* QTBUG-121544 qtprotobufgen generates the corrupted  
protobufwellknowntypes_exports.qpb.h  
* QTBUG-121585 wrong license filename in LICENSES folder ?  
* QTBUG-121865 Qt GRPC module documentation link is broken  
* QTBUG-121862 optional fields are not copied in messages  
* QTBUG-121854 EXPORT_MACRO option has no effect in qt_add_protobuf call  
* QTBUG-121856 qtgrpcgen do not generate C++ export files  
* QTBUG-122700 qt_add_protobuf doesn't set neither OUTPUT_HEADERS nor  
OUTPUT_TARGETS  
* QTBUG-122677 magic8ball doesn't receive errorOccurred() if server is  
not started  
* QTBUG-122816 QtGrpc generator asserts when no messages defined in  
.proto file  
* QTBUG-121560 JSON serializer adds an object when deserializing empty  
JSON arrays  
* QTBUG-122908 Qt Chat example crashes  
* QTBUG-123345 Qt GRPC HTTP2 regression  
* QTBUG-114972 using google/protobuf/timestamp.proto fails to compile  
* QTBUG-114988 Duplicated message names of nested messages lead to QML  
warning  
* QTBUG-115180 QtProtobuf: Enum forward declaration is required  
* QTBUG-113516 int64, fixed64, sfixed64 not recognized as numbers in QML  
* QTBUG-116045 Move C++ definitions to a common header file  
* QTBUG-118080 QDoc cannot distinguish between template function  
overloads differing only  in template arguments  
* QTBUG-114079 qt_add_protobuf() macro should warn a user in case of  
adding proto files with the same name  
* QTBUG-120946 QGrpcHttp2Channel description refers to deprecated  
call/channel credentials  
* QTBUG-121813 qt_attribution.json issues  
* QTBUG-123400 QtProtobuf: cannot use Qt reserved names as fields  
  
### qtquickeffectmaker  
* QTBUG-114561 Material style highlighted & flat button shows no text  
  
### qtgraphs  
* QTBUG-114054 Selectionlabel keeps shrinking in slice view  
* QTBUG-114121 tst_custominput does not work  
* QTBUG-113677 Slice view with orthographic camera shows the main graph  
incorrectly  
* QTBUG-114180 Incomplete gradients cause incorrect rendering result  
* QTBUG-113525 Selection label gets occluded by graph items  
* QTBUG-115270 widgetgraphgallery: itemLabel remains on the graph even  
though data has changed  
* QTBUG-112244 Windowcolor does not always work correctly  
* QTBUG-114129 tst_qmlheightmap: changing the map image does not work  
* QTBUG-114867 Crash on Surfacegallery oscilloscope  
* QTBUG-114123 tst_minimalbars crashes at start  
* QTBUG-114132 tst_volumetrictest crashes  
* QTBUG-115681 Axis range adjustment does not trigger redraw for scatter  
* QTBUG-115685 Fix grid in scatter graph  
* QTBUG-112441 Surface3D: Multiseries selection mode is on by default  
* QTBUG-114490 Views do not resize when in slice view  
* QTBUG-114125 tst_barasrowcolors: row colors do not work  
* QTBUG-115774 Crash when trying to adjust axis range in tst_barstest  
* QTBUG-112241 Graphgallery graph window sizes are off  
* QTBUG-114124 tst_multigraphs crashes when changing graph type to  
Scatter  
* QTBUG-114060 Crash on AxisHandling example  
* QTBUG-115940 Surfacegraph picking resample crash  
* QTBUG-115684 Texture is gone when axis range is changed  
* QTBUG-115986 Grid lines might not be updated after line count change  
* QTBUG-115683 Title labels are not updated for surface graph  
* QTBUG-115694 Axis range crashes the topology example  
* QTBUG-116005 Toggling surface texture not working  
* QTBUG-114120 Slice view is too small  
* QTBUG-116108 Zoom on topography example shows wrong graph  
* QTBUG-116177 Update grid and labels when aspect ratio changes  
* QTBUG-114491 Labels disappear when changing data proxy in  
widgetgraphgallery  
* QTBUG-116207 Ambient light is ignored if specular is set to 0.0  
* QTBUG-116140 Surface3DSeries ignores itemLabelFormat  
* QTBUG-113272 Theme light properties are not passed through to gradient  
materials  
* QTBUG-116169 Shows incorrect highlight on topography example  
* QTBUG-116201 Background and grid ignore theme's light properties  
* QTBUG-111059 Surface Widget: Updating the heightmap model ranges is  
too slow  
* QTBUG-116317 Surface grid looks aliased  
* QTBUG-116272 'Adjust sample count' sliders do not work in barstest  
* QTBUG-116398 widget gallery crashes with surfacegraph  
* QTBUG-116336 Texture is flipped in textured topography example  
* QTBUG-116233 Slices in surface graph do not update correctly when  
using ranges  
* QTBUG-116269 Huge label visible in AxisHandling and crash after that  
if so that the labels get flipped  
* QTBUG-116200 Highlight gradients are sometimes incorrect  
* QTBUG-116313 Flat shading does not work on opengl backend  
* QTBUG-116487 Surfacegraph does not exit picking when out of range  
* QTBUG-116471 Bars3D leaks memory when changing color style  
* QTBUG-116485 Crash on picking in oscilliscope demo  
* QTBUG-116438 Surface graphs camera can not be rotated after switching  
to slice view  
* QTBUG-116525 Custom labels do not show up  
* QTBUG-116486 Labels re-align after rotating a bar graph and then  
selecting something  
* QTBUG-116514 A black triangle appears in the slice view  
* QTBUG-116601 Surface3D Topography crash on picking edge  
* QTBUG-116435 Surface3D crashes in textured topography example if slice  
view is used  
* QTBUG-116310 Camera rotation should be disabled in surfacegallery  
spectrogram example in ortho mode  
* QTBUG-116604 Grid lines are drawn on top of slice and labels in slice  
view  
* QTBUG-116033 The original graph enlarges in slice view when resizing  
window  
* QTBUG-116629 Label background color is not correct in Axis Formatting  
example  
* QTBUG-116561 Alignment of labels is wrong  
* QTBUG-116659 Toggling Hide Shadows in scatter example cause the series  
to disappear  
* QTBUG-116479 Highlighting the selection does not work correctly in  
texture topography example  
* QTBUG-117024 Labels cast shadows, but they should not  
* QTBUG-117213 Fix example category for qtgraph examples  
* QTBUG-115772 Graph goes to empty slice view automatically  
* QTBUG-113675 Slice view is sometimes empty in Bars3D  
* QTBUG-116911 tst_surfacetest massive data test crash  
* QTBUG-117627 Surface graph polar view is too narrow  
* QTBUG-116743 Mesh.Point does not get rotated to face camera in  
Optimization.Default  
* QTBUG-117676 Surface Graph Gallery example crashes when picking  
* QTBUG-116823 Picking the surface graphs after changing ranges is  
inaccurate  
* QTBUG-117738 Slice view material is not rendered correctly  
* QTBUG-117734 Scatter highlight flickers / disappears when rotating  
after selection  
* QTBUG-113650 Selection is sometimes incorrect in Bars3D  
* QTBUG-117685 Scatter doesn't change highlight for the selected point  
* QTBUG-117821 A lot of warnings in Bars3D  
* QTBUG-117848 Slice view opens unexpectedly  
* QTBUG-117767 Selected point does not face camera if scene is rotated  
with Mesh::Point  
* QTBUG-117769 Selected bars do not use the correct mesh  
* QTBUG-117961 tst_itemmodeltest: Labels are not drawn at the beginning  
* QTBUG-116785 Topography example shows highlight series in slice view  
* QTBUG-117957 tst_itemmodeltest: Surface Graph is not drawn  
* QTBUG-118079 Slice view grid color is incorrect  
* QTBUG-114122 tst_itemmodel: selection from table does not work  
* QTBUG-117842 Bars: slice view empty  
* QTBUG-117989 Toggling smooth mesh for one series sets it for all in  
scatter example  
* QTBUG-118039 Zoom to selected bar does not animate the graph in  
widgetgraphgallery  
* QTBUG-114411 Axis label selection does not work  
* QTBUG-118395 Toggling smooth mesh in scatter example causes meshes to  
disappear  
* QTBUG-117875 Slice view labels are placed incorrectly  
* QTBUG-117823 Labels are distorted in slice view  
* QTBUG-99816 Reflection support does not work - remove references to it  
* QTBUG-118582 Scatter item mesh type is not always updated correctly  
* QTBUG-118144 measureFps does not force continuous rendering  
* QTBUG-116745 Adjusting highlight light strength in theme does not have  
an effect  
* QTBUG-118554 Ambiguous API in renderToImage feature  
* QTBUG-117938 Scatter point gradients are not updated correctly  
* QTBUG-117784 Selecting another bar from the same row in optimization  
default doesn't work  
* QTBUG-116602 Item label is shown as an empty label in surface graph  
gallery example  
* QTBUG-118644 Create slice bar models with instancing  
* QTBUG-118660 Slice view shows Item selection even when selectionmode  
does not have it set  
* QTBUG-118812 Crash on tst_barstest  
* QTBUG-118528 Floor and floor grid may be out of sync  
* QTBUG-116429 widgetgraphgallery: surfacegraph should open slice view  
immediately  
* QTBUG-119376 Slice graph stays open in test_qmlheightmap  
* QTBUG-119662 Remove AxisHelper  
* QTBUG-120255 Surface gallery spectrogram demo polar graph has a gap at  
the edge  
* QTBUG-120310 Cannot exit surface slice graph view  
* QTBUG-120292 'Change' buttons don't work in tst_surfacetest  
* QTBUG-119661 tst_barstest crashes when trying the 'Swap value axis'  
button  
* QTBUG-119686 Height Map's slice graph does not update correctly  
* QTBUG-120562 QtGraphs: Examples don't show in Qt Creator for Qt 6.7  
* QTBUG-119695 Bars are too close to the floor  
* QTBUG-120209 Clearing a selected point does not work on the surface  
* QTBUG-120664 Changing theme doesn't update LineSeries  
* QTBUG-120701 Surface graph is visible when the whole array is out of  
bounds on the row axis  
* QTBUG-120744 Surface is not rendered after selecting ascending data in  
tst_surfacetest  
* QTBUG-120128 Uniform color does not work in selected bars  
* QTBUG-120480 Graph jumps to slice view when changing other properties  
* QTBUG-120743 LineSeries doesn't respect minimum axis values  
* QTBUG-120400 SliceItemLabel appears even if the hide label button is  
pressed  
* QTBUG-120552 Wireframe can be toggled on when series is not visible  
* QTBUG-121391 Shader errors with 2D grid lines if both 2D and 3D  
features are on  
* QTBUG-121208 Line widths not updating  
* QTBUG-121372 Theme3D::baseColors is written as Theme3D::baseColor in  
the document  
* QTBUG-120731 Surface slice rendering is black when data is descending  
* QTBUG-121474 setSeriesGradient and connectSeriesGradient are  
duplicated in 3 places  
* QTBUG-121476 Unity build fails with duplicated noRoleIndex definition  
* QTBUG-121520 QtGraphs fails to configure manual tests without  
multimedia  
* QTBUG-120977 Texture appears the wrong way round with descending data  
* QTBUG-121655 Q missing in front of SeriesTheme and GraphTheme  
* QTBUG-121686 Callout example doesn't show lines  
* QTBUG-121905 A lot of warnings from public headers  
* QTBUG-122068 Some vertical and only some horizontal gridlines visible  
in spectogram  
* QTBUG-122071 data point polar position not calculated in scatter  
* QTBUG-117936 Polar axis support for Scatter3D does not work  
* QTBUG-121695 Setting selectedColor in XYSeries does not work  
* QTBUG-121680 Crash if axisX or axisY is set to null after being first  
set  
* QTBUG-121687 It should not be possible to enter negative width  
* QTBUG-121688 It should not be possible to set an invalid value to  
capStyle  
* QTBUG-121998 Q3DSurface/Q3DBars opens up as white screen by default  
* QTBUG-122172 Manual testing - tst_barstest crashes  
* QTBUG-122169 Custom pointMarker can't access outside the component  
* QTBUG-122182 Surface graph selected point is incorrect in polar mode  
* QTBUG-122247 Surface oscilloscope example labels show wrong numbers  
* QTBUG-121770 QXYSeries select and deselect functions do not seem to  
work  
* QTBUG-121739 QBarSet selectBars and selectAllBars do not work  
* QTBUG-121720 BarSeries axisX and axisY can be given invalid axes  
* QTBUG-121209 Line Properties example crashes  
* QTBUG-122450 Sometimes crashes in testbed  
* QTBUG-122445 SettingsView causes artifacts when hidden  
* QTBUG-122446 GraphsView accepts events it doesn't handle  
* QTBUG-122443 Lines and PointMarkers aren't clipped by GraphsView  
* QTBUG-122688 Bars gradient does not update  
* QTBUG-113833 Fix orthographic camera setup for volumes  
* QTBUG-114692 Only relative scaling works  
* QTBUG-113834 Area selection doesn't work correctly for volumes  
* QTBUG-113646 Shadows are sometimes messed up with OptimizationDefault  
* QTBUG-113839 Slice frames go behind the volume  
* QTBUG-108129 Rendering performance of Surface3D is poor  
* QTBUG-114980 Volumes have distorted perspective  
* QTBUG-114105 Custom item selection does not work  
* QTBUG-116473 Graph is not deleted on exit in widgetvolumetric  
* QTBUG-116472 Orthographic camera doesn't scale with window size  
* QTBUG-114981 Orthographic camera starts too close in the volumetric  
example  
* QTBUG-111712 renderToImage does nothing  
* QTBUG-120152 Back and side vertical gridlines visible in polar graph  
* QTBUG-121212 Axis grid clipped from top & bottom  
* QTBUG-121211 Grid lines visibility not updating correctly  
* QTBUG-121207 Polish & Rendering synchronization needs update  
* QTBUG-121719 BarSeries barWidth can be given invalid values  
* QTBUG-121721 AbstractSeries valuesMultiplier can be given invalid  
values  
* QTBUG-121805 QGraphTheme ColorTheme enums do not work  
* QTBUG-121806 QGraphTheme setColorTheme does not override individually  
set colors  
* QTBUG-122050 Polar grid too big in spectogram  
* QTBUG-122112 Setting polar axis on for Bars3D causes a crash on  
Windows  
  
### qtapplicationmanager (Commercial only)  
* QTBUG-114355 Many qmllint warnings for Application Manager QML types  
* QTBUG-114356 AppMan: IntentServerHandler is not registered correctly  
* QTBUG-114755 AppMan: IntentModel cannot be compiled  
* QTBUG-116081 FAIL!  : appman-  
qmltestrunner::WindowMapping::test_amwin_advanced() property count  
* QTBUG-116627 FAIL!  : appman-  
qmltestrunner::BubbleWrap::test_bubblewrap() 'wait for signal  
windowAdded' returned FALSE.  
* QTBUG-117980 CMake install fails on appman for Qt/QNX windows build  
* QTBUG-118603 FAIL!  : tst_Yaml::mergedCache() Compared values are not  
the same  
* QTBUG-118524 Crash in wayland when using Bubblewrap container plugin  
* QTBUG-119241 Context properties broken when named specifically  
* QTBUG-119476 qtapplicationmanager/src/main-lib/main.cpp:16:12: fatal  
error: packagemanagerdbuscontextadaptor.h: No such file or directory  
* QTBUG-118743 Notification not dismissing when dismissOnAction is true  
* QTBUG-120326 SEGV when testing of appman-qmltestrunner  
* QTBUG-122425 AppMan: Documented logging category for QML logging is  
incorrect  
* QTBUG-122721 [AppMan] Discrepancies in documented types of Application  
+ Package Categories  
* QTBUG-117010 [Boot2Qt] Cannot run any application that uses Qt  
Application Manager  
* QTBUG-122951 "#pragma once" is not allowed in installed header files:  
* QTBUG-105067 Different behavior in single- vs. multi-process mode  
* QTBUG-108855 Focus on click doesn't work in single-process mode  
  
### qtinterfaceframework (Commercial only)  
* QTBUG-114686 Locale Problem in Compiled Ifcodegen on M1  
* QTBUG-114940 Setting an env override for a simulationFile also affects  
the discoveryMode  
* QTBUG-115600 FAIL!  : BackendsTest::testInit(simulation-backend)  
* QTBUG-116662 Qt Interface Framework Generator doesn't work with cross-  
compiling kits  
* QTBUG-119428 Enums in simulationData cannot be parsed correctly  
* QTBUG-121575 Interface files are generated in configuration time, not  
compilation time  
* QTBUG-122036 ModuleNotFoundError: No module named 'dataclasses'  
* QTBUG-121740 The page about Jinja Template Syntax has its link  
malformed  
* QTBUG-121778 QIfAbstractFeature::connectToServiceObject()'s code  
snippet is ill-formed  
* QTBUG-121696 This page about QtIf is only talking about qmake, not  
cmake  
* QTBUG-121800 IfSimulator QML type's doc doesn't specify the return  
types of methods  
* QTBUG-112685 CMake policies are not in sync between qt repos and  
macros included in top-level CMakeLists.txt  
* QTBUG-115221 Add support for WebAssembly in the autotests  
  
### qmlcompilerplus (Commercial only)  
* QTBUG-116741 Dependency update on qt/tqtc-qmlcompilerplus is failing  
in 6.6  
* QTBUG-120039 fatal error: 'private/qquickabstractdialog_p.h' file not  
found  
* QTBUG-122035 FAILED:  
tests/auto/codegen/.rcc/qmlcache/tst_codegen_direct_writeback_qml.cpp  
* QTBUG-121734 SetLookup crashes on hierarchy of shadowable properties  
* QTBUG-122726 Dependency update on qt/tqtc-qmlcompilerplus is failing  
* QTBUG-119162 Qml: Behaviour differs between interpreted/compiled code  
  
### qtinsighttracker (Commercial only)  
* QTBUG-113766 [Insight Tracker] Click event without the category is not  
tracked  
* QTWEBSITE-1110 Missing redirects for Qt Insight Tracker documentation  
* QTBUG-116699 Data base cannot be opened in the subsequent launches  
* QTBUG-117916 Only enabling QtInsightTracker in C++ side only works for  
MSVC  
* QTBUG-112415 QtInsighttracker component not sending data to QtInsight  
server on Android platforms  
* QTBUG-119043 Events are not sent in the sync value set in  
qtinsight.conf  
* QTBUG-115601 FAIL!  : tst_QInsightEventFilter::trackEvents(text.ui)  
The computed value is expected to be greater than or equal to the  
baseline, but is not  
  
### qtvncserver (Commercial only)  
* QTBUG-113545 vncserver static build fails with libtomcrypt  
* QTBUG-119312 Cannot input text to an input field in a dialog  
* QTBUG-115515 Compiling Qt top level does not compiles Qt Vncserver  
* QTBUG-115835 Dependencies.yaml should mention Qt Shader Tools  
  
Known Issues  
------------  
  
* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-6.7/supported-platforms.html  
* RTA reported issues from Qt 6.7  
https://bugreports.qt.io/issues/?filter=25756  
* See Qt 6.7 known issues from:  
https://wiki.qt.io/Qt_6.7_Known_Issues  
* Qt 6.7.0 Open issues in Jira:  
https://bugreports.qt.io/issues/?filter=25773  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Amir Masoud Abdol  
Matt Aber  
Cristian Adam  
James Addison  
Laszlo Agocs  
Yigit Akcay  
Dilek Akcay  
Owais Akhtar  
Dmitrii Akshintsev  
Konsta Alajärvi  
Anu Aliyas  
Tim Angus  
Dimitrios Apostolou  
Soheil Armin  
Nikunj Arora  
Viktor Arvidsson  
Albert Astals Cid  
Mahmoud Badri  
Karolina Sofia Bang  
Mate Barany  
Chris Von Bargen  
Vladimir Belyavsky  
Nicholas Bennett  
Lena Biliaieva  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
Mikolaj Boc  
Tatiana Borisova  
Joerg Bornemann  
Rym Bouabid  
Assam Boudjelthia  
Aurélien Brooke  
Kai Uwe Broulik  
Michael Brüning  
Alex Bu  
Alexander Busse  
Olivier De Cannière  
John Chadwick  
Kaloyan Chehlarski  
Mike Chen  
Ed Cooke  
Andreas Cord-Landwehr  
Alexandru Croitor  
Mitch Curtis  
Thibaut Cuvelier  
Giuseppe D'Angelo  
Pranta Dastider  
Szabolcs David  
Noah Davis  
Oliver Dawes  
Marius Dege  
Ilya Doroshenko  
Pavel Dubsky  
Artem Dyomin  
Alexey Edelev  
David Edmundson  
Oliver Eftevaag  
Christian Ehrlicher  
Hatem ElKharashy  
Andreas Eliasson  
Ahmed Essam  
Fabio Falsini  
David Faure  
Ilya Fedin  
Nicolas Fella  
Josep M. Ferrer  
Renato Araujo Oliveira Filho  
Isak Fyksen  
Simo Fält  
GHENADY  
Samuel Gaist  
Florian de Gaulejac  
Zoltan Gera  
Joshua Goins  
Aleix Pol Gonzalez  
Julian Greilich  
Robert Griebl  
Mikko Gronoff  
Jan Grulich  
Johannes Grunenberg  
Kaj Grönholm  
Richard Moe Gustavsen  
Lucie Gérard  
Ralf Habacker  
Kamil Hajdukiewicz  
Rob Hall  
Mikko Hallamaa  
Heikki Halmet  
Amanda Hamblin-Trué  
Jøger Hansegård  
Inkamari Harjula  
Thomas Hartmann  
Andre Hartmann  
Elias Hautala  
Tero Heikkinen  
Jani Heikkinen  
Miikka Heikkinen  
Moss Heim  
Paul Heimann  
Christian Heimlich  
Jari Helaakoski  
Alex Henrie  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Dominik Holland  
Andreas Holzammer  
Mats Honkamaa  
Alexander Hulander  
Samuli Hölttä  
Yaroslav Isakov  
Martin Jansa  
Allan Sandfeld Jensen  
Tim Jenssen  
Maurice Kalinowski  
Jonas Karlsson  
Kevin Keating  
Timothée Keller  
Ahmed Kerimov  
Jonathan Ketchker  
Kurt Kiefer  
Kristof Kiszel  
Michael Klein  
Friedemann Kleint  
André Klitzing  
Michal Klocek  
Martin Klos  
Lars Knoll  
Jarek Kobus  
Tobias Koenig  
Sze Howe Koh  
Jarkko Koivikko  
Tomi Korpipaa  
Tomi Korpipää  
Jani Korteniemi  
Fabian Kosmale  
Tomasz Kozlowski  
Tomasz Kozłowski  
Volker Krause  
Mike Krus  
Serg Kryvonos  
Anton Kudryavtsev  
Konrad Kujawa  
Santhosh Kumar  
Ghenady Kuznetsov  
Jonas Kvinge  
Keith Kyzivat  
Kai Köhne  
Lauri Laanmets  
Inho Lee  
Paul Lemire  
Kimmo Leppälä  
Chris Lerner  
Wladimir Leuschner  
Thorbjørn Lindeijer  
Lorenzo Lucignano  
Thiago Macieira  
Olaf Mandel  
Tamas Martinec  
Sergio Martins  
Sérgio Martins  
Łukasz Matysiak  
Aaron McCarthy  
Frank Meerkötter  
Ievgenii Meshcheriakov  
Lisandro Damián Nicanor Pérez Meyer  
Leena Miettinen  
Vladimir Minenko  
Samuel Mira  
Jan Moeller  
Safiyyah Moosa  
Bartlomiej Moskal  
Marc Mutz  
Tommi Mänttäri  
Antti Määttä  
Antonio Napolitano  
Martin Negyokru  
Nicekwell Ni  
Andy Nichols  
Mårten Nordheim  
Dennis Oberst  
Kimmo Ollila  
Matti Paaso  
Tinja Paavoseppä  
Kwanghyo Park  
Shreya Pattani  
Pasi Petäjäjärvi  
Samuli Piippo  
Rayam Pinto  
Timur Pocheptsov  
Lauri Pohjanheimo  
Milla Pohjanheimo  
Joni Poikelin  
Aleix Pol  
Cajus Pollmeier  
Jacek Poplawski  
Gleb Popov  
Alessandro Portale  
Rami Potinkara  
Lorn Potter  
Sakaria Pouke  
Shyamnath Premnadh  
MohammadHossein Qanbari  
Liang Qi  
Khem Raj  
Matthias Rauter  
David Redondo  
Arno Rehn  
Topi Reinio  
Huang Rui  
Shawn Rutledge  
Toni Saario  
Casimir Saastamoinen  
Sharad Sahu  
Ahmad Samir  
Lars Schmertmann  
Philip Schuchardt  
Carl Schwan  
Thomas Senyk  
Luca Di Sera  
Dmitry Shachnev  
Sami Shalayel  
Orgad Shaneh  
Andy Shaw  
Ws ShawnWoo  
Venugopal Shivashankar  
Harald Sitter  
Kristoffer Skau  
Colin Snover  
Ivan Solovev  
Tomas Soltys  
Krzysztof Sommerfeld  
Axel Spoerl  
Patryk Stachniak  
Stefan Steinwasser  
Christian Strømme  
Po-Hao Su  
Frank Su  
Tarja Sundqvist  
Audun Sutterud  
Lars Sutterud  
Tasuku Suzuki  
Jan Arve Sæther  
Morten Sørvig  
Akira TAGOH  
Sadegh Taghavi  
Nodir Temirkhodjaev  
Marcus Tillmanns  
Ivan Tkachenko  
Orkun Tokdemir  
Jens Trillmann  
Jere Tuliniemi  
Tuukka Turunen  
Paul Olav Tvete  
Esa Törmänen  
Sami Varanka  
Peter Varga  
BogDan Vatra  
Doris Verria  
Tor Arne Vestbø  
Kalle Viironen  
Gerber Lóránt Viktor  
Petri Virkkunen  
Jannis Voelker  
Fabian Vogt  
Alexander Volkov  
Ville Voutilainen  
Juha Vuolle  
Olli Vuolteenaho  
Sune Vuorela  
Jaishree Vyas  
Michael Weghorn  
Bernd Weimer  
Edward Welbourne  
Paul Wicking  
Bernhard M. Wiedemann  
Piotr Wiercinski  
Piotr Wierciński  
Jakub Wincenciak  
Milian Wolff  
Oliver Wolff  
Li Xinwei  
Weng Xuetian  
Lu YaNing  
Semih Yavuz  
Li Yefeng  
Marianne Yrjänä  
Zhao Yuhang  
Vlad Zahorodnii  
Marcin Zdunek  
Feifei Zhan  
JiDe Zhang  
Yuhang Zhao  
Yansheng Zhu  
Yifan Zhu  
Eike Ziller  
hjk  
shjiu  
Fredrik Ålund  
Michał Łoś  
Andrius Štikonas  
