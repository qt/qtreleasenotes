Release note  
============  

Qt 6.3 introduces many new features and improvements as well as bugfixes  
over the 6.2.x series. For more details, refer to the online  
documentation included in this distribution. The documentation is also  
available online:  
  
https://doc.qt.io/qt-6/index.html  
  
The Qt version 6.3 series is binary compatible with the 6.2.x series.  
Applications compiled for 6.2 will continue to run with 6.3.  
  
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
* f9b867216b String API Symmetry: test for indexOf with large negative  
offset  
QString::indexOf(QChar) and QString::indexOf(char16_t) now treat a  
negative start-position, from, bigger than the string's size as invalid.  
It previously clipped such start-positions to the start of the string,  
inconsistently with other QString indexOf overloads.  
  
* 734429f4a3 QDebug: add support for QVarLengthArray  
Can now stream QVarLengthArray objects.  
  
* a93a9ea915 Fix QFAIL() to interract correctly with QEXPECT_FAIL()  
QEXPECT_FAIL() now correctly anticipates a subsequent QFAIL().  
Previously QFAIL() counted as a fail regardless.  
  
* d093ec8d03 Fix handling of day-of-week in QDateTimeParser and  
QDateTimeEdit  
Corrected handling of weekdays. Previously, changes to the week-day  
were simply changes to the day of the month. Weekday fields are now  
handled as such: changes to them do change the day of the month, but a  
change that would step past the end (or start) of the month is adjusted  
to the relevant day of the nearest week within the month. When wrapping  
is disabled, the locale-specific first and last days of the week are the  
bounds. Formats which specify day of week but not day of month will now  
preserve day of week when changing month or year, selecting the nearest  
day of month that matches.  
  
* c00ee2f310 Use UTC when parsing only a date or only a time, not a  
date-time  
QDateEdit and QTimeEdit now operate in UTC, to avoid spurious  
complications arising from time-zone transitions (e.g. DST) causing the  
implicit other half to combine with the part being edited to make an  
invalid result. Returns from their dateTime() and other methods  
returning QDateTime (max/min) shall thus be in UTC where previously they  
were in local time. QDateTimeEdit continues using local time. The  
default can be over-ridden by setTimeSpec(), as ever.  
  
* bb93c641a2 TLS: Mark TLS 1.0, 1.1 and DTLS 1.0 deprecated  
TLS 1.0, 1.1 and DTLS 1.0 are now deprecated, as recommended by  
RFC-8996.  
  
* 6e57e41f9a QVarLengthArray: fix aliasing error in insert(it, n, v)  
Fixed an aliasing bug affecting insertions of objects aliasing existing  
elements.  
  
* d16ee17a39 Revert "Windows: Add synthesized fonts also when there is a  
style name"  
Fixed a regression where different font styles and/or weights would not  
be available.  
  
* 38448b19a1 QSemaphore: add <chrono> overload of tryAcquire()  
tryAcquire() now optionally takes a <chrono> duration as timeout, not  
just int milliseconds.  
  
* af6bc5a21b Remove ministro code  
Remove ministro code since it's been unmaintained and not working with  
recent Android versions.  
  
* 963a31c0f4 Android: Make the manifest less to scary to read and edit  
Remove some elements from the manifest file that are internal, to make  
it easier to deal with the manifest.  
  
* 35453446a5 QCryptographicHash: don't present the same data over and  
over again  
Fixed a bug where presenting more than 4GiB in a single addData() call  
would calculate the wrong result().  
  
* de18b3ff37 QCryptographicHash: port addData() to QByteArrayView  
Replaced QByteArray with QByteArrayView in addData() and static hash()  
functions.  
  
* 46d2ba1ea4 Restore default installation prefix from Qt 5  
The installation prefix now defaults to /usr/local/Qt-${version} and  
C:/Qt/Qt-${version} like it did in Qt 5.  
  
* ff77930c25 QJsonValue: add rvalue overloads for QJsonArray and  
QJsonObject ctors  
Added constructors taking rvalue QJsonArray and rvalue QJsonObject.  
  
* 6b14ea1ba4 qSwap: make it constexpr  
qSwap is now constexpr.  
  
* 3552821551 QObject: make new-style-connects SFINAE-friendly  
, SLOT(~~~)) is now SFINAEd out instead of triggering a static_assert().  
That means it is now possible to use Expression SFINAE  
(decltype(QObject::connect(<sender>, <signal>, std::declval<Args>()...)  
to properly wrap new-style QObject::connect() calls with a single  
wrapper function, greatly simplifying the implementation, incl. passing  
Qt::ConnectionType arguments. For more information on how to use this in  
your own code, see the sources of QWidget::addAction().  
  
* 2b50c8bec0 QObject: optimize the common case of  
findChildren(QString())  
Added findChildren() overload taking no name (thus optimizing this  
common case).  
  
* e08f6d601d QLineEdit: don't change layout direction on keyboard input  
QLineEdit used to change the layout direction on each key press, based  
on the text content. This feature resulted in an inconsistent and  
erratic user experience, and has been removed.  
  
* 08e4d2db08 QWidget: copy Q{Menu,ToolBar}::addActions() functions  
Added the same addAction(text) overloads that previously existed only  
on QMenu and QToolBar, with the following two differences: First, the  
QKeySequence object, if any, is now available on all overloads, not just  
the ones taking a slot, but has changed position to allow, secondly,  
passing an optional Qt::ConnectionType parameter which will be passed to  
the QObject::connect() call. In addition, the function template  
overloads are now properly constrained so that they exist if and only if  
the corresponding QObject::connect() call does, too.  
  
* 09d1196281 QMenu/QToolBar: remove addAction() functions  
The addAction() functions have been moved down into QWidget.  
  
* 6c1bc7798b QLocalSocket/Win: destroy the pipe before emitting final  
signals  
QLocalSocket on Windows now emits both readChannelFinished() and  
disconnected() signals after closing the pipe and emitting  
stateChanged(UnconnectedState), which is consistent with the behavior on  
Unix.  
  
* 973ca1fac6 Change QCollator's default locale to QLocale().collation()  
The default locale used by QCollator is now the collation locale of the  
default QLocale. This restores the ability (lost at 5.14) to control the  
locale used by QString::localeAwareCompare(), while retaining the use of  
a collation locale when the default is the system locale.  
  
* 90d9a86c2e QMetaType: Support converting any QFuture<T> to  
QFuture<void>  
QMetaType now supports converting any QFuture<T> to QFuture<void>.  
  
* 27d6314b95 QCryptographicHash: use a std::array to hold result (was:  
QByteArray)  
Changed to use a statically-sized buffer internally. Added resultView()  
to access it.  
  
* 0c2125458a Consistent handling of disabled items in  
QItemSelectionModel  
All methods in QItemSelectionModel now consider only items which are  
marked as enabled and selectable as part of the selection.  
  
* e095fa7f9c Allow to set TCP network listen(2) backlog  
Added QTcpServer::setListenBacklog() to be able to have control over  
the listen backlog feature.  
  
* 53e4a50c6b Make QFutureWatcher::isFinished() consistent with the  
watched QFuture  
The QFutureWatcher::isFinished() method now indicates if the related  
QFuture is finished, instead of indicating if the finished() signal was  
delivered. This makes it consistent with the future that is being  
watched.  
  
* 162d486c0d Remove special casing of HSL QColor comparison  
Equality on HSL colors is now raw value based like other color-formats,  
instead of being partially interpretation based.  
  
* f18d8fd1fb QLocalSocket/Win: do not close the device on  
disconnectFromServer()  
The Windows implementation of QLocalSocket::disconnectFromServer() no  
longer calls close(), which is consistent with the behavior on Unix.  
  
* 921ff400bb QLocalSocket/Win: allow delayed close to work  
QLocalSocket on Windows now implements delayed closing, which is  
consistent with the behavior on Unix.  
  
* 8f75ab231f Allow to set Local Socket listen(2) backlog  
Added setListenBacklogSize() to be able to have control over the listen  
backlog feature.  
  
* d3ecc6db29 QMenuBar: remove addAction() functions  
The addAction() functions have been moved down into QWidget.  
  
* 25fff849e8 QDirIterator: add nextFileInfo()  
Added nextFileInfo(), which is like next(), but returns fileInfo()  
instead of filePath().  
  
* 42970e490a CMake: Bump min required CMake version for shared Qt builds  
to 3.16  
Building Qt as shared libraries now requires CMake version 3.16 or  
later. Building user projects with CMake using that Qt installation also  
requires a CMake version of 3.16 or later.  
  
* 615a9cf991 QUuid: port to QAnyStringView  
The from-string constructor and the fromString() function now take  
QAnyStringView (was: overload set with a subset of QString, QByteArray,  
const char*, QLatin1String, QStringView each).  
  
* 260168d9d7 QByteArray: don't coerce negative to unsigned for any base  
QByteArray's formatting of negative whole numbers to bases other than  
ten now, like QString's (since Qt 6.0), formats the absolute value and  
prepends a minus sign.  
  
* bef57b317f testlib: Deprecate QWARN() in favor of qWarning()  
QWARN() has been deprecated in favor of qWarning()  
  
* 115f828ae4 QTestEventLoop: stop when the test fails  
The QTestEventLoop new exits its event loop as soon as the test is  
known to be failing.  
  
* 73fabadcee QXpmHandler: fix re-entrancy bug in xpm_color_name  
Fixed a race condition when concurrently writing .xpm files.  
  
* 71334c324e QXpmHandler: actually limit characters-per-pixel to four  
Instead of writing a corrupt file, rejects to write XPM files with more  
than 64^4 colors (more than four characters per pixel) now.  
  
* 7502598ef5 QListView: fix AdjustToContents (sizeAdjustPolicy)  
A more correct implementation of QListView::viewportSizeHint has been  
made. That implies that setting the sizeAdjustPolicy to AdjustToContent  
on QListView and QListWidget will now cause the view to size after the  
contents and avoid scrollbars.  
  
* f95a446641 CMake: Bump min required CMake version for static Qt builds  
to 3.21  
Building Qt as static libraries now requires CMake version 3.21 or  
later. Building user projects with CMake using that Qt installation also  
requires a CMake version of 3.21 or later.  
  
* 211369133c MySQL: remove the version number checks in favor of actual  
functionality  
Fixed the detection of whether the client and server support prepared  
statements. This was caused by the mariadb connector library reporting  
its own version numbers (starting in version 3.2) instead of the server  
version.  
  
* 76e2409cc9 Fix memory leak if eXIf has incorrect crc  
Fix for possible memory leak in libpng was backported.  
  
* 6f833eff92 Add QByteArrayView::trimmed()  
Added trimmed().  
  
* 29cfea3e82 QVarLengthArray: add support for emplacement  
Added emplace(), emplace_back().  
  
* 2f5695bed5 Fix printing with unhinted fonts  
Fixed an issue where the characters in printed text would look too  
small.  
  
* 6cee204d56 QS(V)/QBA(V)/QL1S::lastIndexOf: fix the offset calculations  
A regression in the behavior of the lastIndexOf() function on text-  
related containers and views (QString, QStringView, QByteArray,  
QByteArrayView, QLatin1String) has been fixed, and the behavior made  
consistent and more in line with user expectations. When lastIndexOf()  
is invoked with a negative `from` position, the last match has now to  
start at the last character in the container/view (before, it was at the  
position *past* the last character). This makes a difference when using  
lastIndexOf() with a needle that has 0 length (for instance an empty  
string, a regular expression that can match 0 characters, and so on);  
any other case is unaffected. To retrieve the "truly last" match, one  
can pass a positive `from` offset to lastIndexOf() (basically, pass  
`size()` as the `from` parameter). To make calls such as  
`text.lastIndexOf(~~~);`, that do not pass any `from` parameter, behave  
properly, a new lastIndexOf() overload has been added to all the text  
containers/views. This overload does not take a `from` parameter at all,  
and will search starting from one character past the end of the text,  
therefore returning a correct result when used with needles that may  
yield 0-length matches. Client code may need to be recompiled in order  
to use this new overload. Conversely, client code that needs to skip the  
"truly last" match now needs to pass -1 as the `from` parameter instead  
of relying on the default.  
  
* e7455644a2 CMake: Don't install metatypes files for user projects  
qt6_extract_metatypes does not install metatypes files anymore. Instead  
the OUTPUT_FILES option can be provided to get the list of extracted  
files for further processing.  
  
* 43a63901f4 Fix bug with NoFontMerging when font does not support  
script  
Fixed an issue with NoFontMerging and changing font families  
dynamically, where boxes would be seen in place of the correct text.  
  
* d8f815db7f Update Harfbuzz to version 2.9.0  
Updated bundled Harfbuzz to version 2.9.0.  
  
* 1971250de5 Fix default line thickness for fonts  
Fixes an issue where underlines and other decorations would be too  
thick for some fonts.  
  
* bac329a28b QRegularExpressionMatch: add a way to know if a capturing  
group captured  
Added the hasCaptured() family of functions to know if a given  
capturing group has captured something.  
  
* 531b913f61 qdbuscpp2xml: add support for custom types with a new -t  
option  
Added a -t option to specify how to handle custom types.  
  
* 842ece2117 NetworkAccessBackend: Remove the backend part of the name  
The NetworkAccessBackend plugin-type is renamed to NetworkAccess, if  
you have a plugin marked NetworkAccessBackend you need to change it to  
NetworkAccess.  
  
* 4bf3010378 QUrl: Implement UTS #46  
ACE processing is now performed according to the UTS #46 standard based  
on IDNA 2008 instead of IDNA 2003.  
  
* 7d4d47de70 QObject::connect(): fail to connect to a functor if  
UniqueConnection is passed  
QObject::connect() now will refuse to connect a signal to a free  
function / function object if UniqueConnection is passed. Note that  
UniqueConnection has never worked for such connections -- the flag was  
simply ignored, and they were established multiple times. Now, the flag  
is not ignored and results in a connection failure (as well as a runtime  
warning by Qt).  
  
* 4e9efb0b60 Teach QByteArrayView how to parse numbers  
Added numeric parsing methods.  
  
* a6a3b1e79c Update bundled libjpeg-turbo to version 2.1.1  
libjpeg-turbo was updated to version 2.1.1  
  
* 6da648ad83 Add a QLocale(QStringView) constructor  
Added QLocale(QStringView) constructor.  
  
* 9a4c98e556 xcb: support xrandr(1.5) monitor setup  
Qt screen info will get from xrandr monitor object if 1.5 is installed.  
  
* da2fd6a903 Q_DECLARE_INTERFACE: add missing const to const  
qobject_cast  
The macro Q_DECLARE_INTERFACE used to cast away the constness of the  
QObject parameter. That is now fixed in this release, but may cause  
failure to build source code that depended on this incorrect behavior.  
If fixing the const correctness in your code is not an option, insert an  
explicit const_cast<IFace *> of the object prior to the qobject_cast  
call.  
  
* b919fc8fd0 SQLite: Update SQLite to v3.36.0  
Updated SQLite to v3.36.0  
  
* 4641ff0f6a Add new am/pm format-specifier that preserves locale's case  
Time formats used by QLocale, QTime and QDateTime's parsing and  
serialization now recognize 'aP' and 'Ap' format specifiers to obtain an  
AM/PM indicator, using the locale-appropriate case for the indicator,  
where previously the author of a time format had to pick a case that  
might conflict with the user's locale. For QTime and QDateTime the  
locale is always C, whose indicators are uppercase. For QLocale, the  
case will now match that of amText() or pmText(). Previously, 'aP' would  
have been read as a lower-case indicator followed by a 'P' and 'Ap' as  
an upper-case indicator followed by a 'p'. The 'P' or 'p' will now be  
treated as part of the format specifier: if the prior behavior is  
desired, either use 'APp' or 'apP' as format specifier or quote the 'p'  
or 'P' in the format. The prior 'a', 'ap', 'A' and 'AP' specifiers are  
otherwise unaffected.  
  
* 2e520f29a7 OpenSSL: Let people opt-in to use TLS 1.3 PSK callback  
When using TLS 1.3 we suppress the first callback from OpenSSL about  
pre-shared keys, as it doesn't conform to the past behavior which  
preSharedKeyAuthenticationRequired provided. With this update you can  
opt-out of that workaround by setting the QT_USE_TLS_1_3_PSK environment  
variable  
  
* e0ad2cee55 Fix querying font aliases that share name with other fonts  
Fixed an issue where some font styles and weights would not be  
selectable. This was especially noticeable on Windows.  
  
* 53d1e26ff5 High resolution wheel-event support from libinput  
Can now use the hires scrolling API from libinput 1.19, adding this  
feature to QPAs using libinput directly  
  
* b4bb3a5415 Introduce QDoubleValidator::setRange overload with two  
parameters  
The QDoubleValidator::setRange() method now has two overloads. The  
first overload takes 3 parameters, but does not support a default value  
for decimals. The second overload takes only two parameters, not  
changing the number of decimals at all. Hence, the number of decimals  
will only be changed if the user explicitly specifies it. To maintain  
the old behavior of setRange(), pass 0 as the 3rd argument explicitly.  
  
* fe46cd59ce Add isValidUtf8() methods to QUtf8StringView and  
QByteArray{,View}  
Added isValidUtf8() method.  
  
* 416fbfa5a0 Use Yu Gothic UI as the main fallback font for Japanese  
Made the primary fallback font on Japanese locale "Yu Gothic UI" (the  
default system font).  
  
* 4e71603412 Implement preview support for GTK file dialog  
A native GTK file dialog (created via QFileDialog or QtQuick.Dialogs)  
now shows an image preview pane.  
  
* 0dc6cc0551 MSVC: enforce that we are under /permissive-  
When using MSVC Qt now requires standards compliance mode. This  
requires passing the /permissive- command line switch. Note that when  
using C++20 or above, the /permissive- switch is implied by default.  
  
* b4e290a9ab Update PCRE2 to 10.38  
PCRE2 has been updated to version 10.38.  
  
* 0a02d84555 Add basic android multi-abi support for CMake projects  
Added basic support for multi-abi builds of user projects.  
  
* fab1debb74 QTest: support initMain() in QTEST_APPLESS_MAIN  
initMain() is now also supported when using QTEST_APPLESS_MAIN.  
  
* cb651f81de Update Harfbuzz to version 3.0.0  
Updated bundled Harfbuzz to version 3.0.0.  
  
* 4d47b18c81 Revert "Support family names that end/start with space"  
Fixed an assert that happened when the system had a font with a  
trailing or leading space in its name.  
  
* e0b6b27d39 Add style hint for preventing spin box selection on up/down  
A new style hint, SH_SpinBox_SelectOnStep, specifies whether pressing  
the up/down buttons or keys in a spinbox will automatically select the  
text.  
  
* e05e3c7762 freetype/no-fc: Disambiguate fonts with different widths  
Fixed a bug where fonts of different width within the same family would  
be unselectable if the Freetype font database (no-fontconfig  
configuration) was in use.  
  
* 5c436365f5 Support background-color CSS styling on <hr/>  
The background-color style can now be applied to <hr/> to set the rule  
color.  
  
* b6cbd9c43a QList: deprecate iterator<->pointer implicit conversions  
(2/3)  
Converting a QList's iterator from and to a raw pointer is deprecated,  
and will get removed in Qt 6.6. User code can prepare for the change by  
defining QT_STRICT_QLIST_ITERATORS.  
  
* f9139b19bf QLatin1String: harmonize null byte handling with the rest  
of QString  
Since Qt 6.0, all QString and QLatin1String methods consuming  
QByteArray and QByteArrayView objects will include any embedded null  
bytes and treat them as U+0000 Unicode characters, whereas in Qt 4.x and  
5.x, they would stop at the first null byte like bare C strings. Qt 6.3  
contains a fix for a couple of the methods that mistakenly persisted the  
old behavior in 6.0-6.2, namely the QLatin1String constructor from  
QByteArray and the equality and inequality operators between QByteArray  
and QString.  
  
* a7d1c48ca3 QVarLengthArray: Reduce memory allocations in emplace()  
Reduced number of memory allocations in emplace() by allocating more  
memory at once.  
  
* e3f05981cb QHash: use the shadow seed  
The qHash functions operating on string-like types and the qHashBits  
function will now mix in a shadow seed (not available in any API) if the  
provided main seed is not 0. This means the hashing value for any  
particular input has an almost zero chance of being equal in two  
different processes, even if processes of the same application. This  
unpredictability makes QHash more strongly resist denial-of-service  
attacks through degenerate hashing tables.  
  
* bbfd625b63 qglobal.h: Do not include <algorithm>  
The <algorithm> header is no longer transitively included with  
qglobal.h. If you used functionality from that header and relied on the  
transitive include, you will now need to explicitly add the header.  
  
* e2e5f448ca Implement QTest:mouseMove widget overload to send event  
QTest::mouseMove no longer moves the mouse cursor via QCursor::setPos,  
but instead generates a QEvent::MouseMove. Testing of code that relies  
on QCursor::pos needs to be done with explicit calls to QCursor::setPos.  
  
* efc1cd5799 PCRE2: upgrade to 10.39  
PCRE2 has been updated to version 10.39.  
  
* f5fbad669d QByteArrayList: add join(QByteArrayView)  
Added join(QByteArrayView) overload.  
  
* c1c15abc8d QByteArrayList: fix narrowing in join() implementations  
[1/2]  
Fixed a bug when calling join() on lists with more than INTMAX  
elements.  
  
* faa854ffeb QByteArrayList: fix narrowing in join() implementations  
[2/2]  
Fixed a bug when calling join() with separators of length > INTMAX.  
  
* c5409964b0 configure: Allow specifying arbitrary variable assignments  
Users can directly assign CMake variables with configure, for example  
"configure CMAKE_CXX_COMPILE=clang++-11".  
  
* 5fc9c02a69 QProcess: Distinguish between null and empty  
QProcessEnvironment  
An additional constructor was added to explicitly create an object that  
when set on QProcess would cause it to inherit the environment from  
parent (this was formerly the behavior of a default-constructed  
QProcessEnvironment, which will now (as documented) actually give a  
process an environment with no variables set). A new method  
inheritsFromParent() was added to test for such objects.  
  
* 1c880752eb qmake: Support Visual Studio 2022  
Added support for Visual Studio 2022.  
  
* eab40726be QFuture: support cancellation of continuation chain through  
parent  
The chain of continuations attached to a future now can be cancelled  
through cancelling the future itself at any point of the execution of  
the chain, as it was documented. Previously canceling the future would  
cancel the chain only if it was done before the chain starts executing,  
otherwise the cancellation would be ignored. Now the part of the chain  
that wasn't started at the moment of cancellation will be canceled.  
  
* 61aa482241 QTabBar: Support scrolling with a kinetic wheel  
Scrolling with a kinetic wheel or touch pad scrolls the entire tab bar,  
without changing the current index.  
  
* 9879d41d05 xcb: Implement support for touchpad gestures  
Touchpads can now detect multi-finger gestures and send  
RotateNativeGesture, ZoomNativeGesture and PanNativeGesture events,  
since XInput 2.4 and X Server 21.1.  
  
* b99adf7a81 Do not include qloggingcategory.h in public headers  
The qguiapplication.h header no longer implicitly includes  
qloggingcategory.h. If your code depends on the transitive include,  
explicitly include <QLoggingCategory> where needed.  
  
* b00fe3c9aa CMake: Enable -bundled-xcb-xinput by default  
The xcb plugin is now compiled with the bundled xcb-xinput library by  
default, in order to enable support for touchpad gestures.  
  
* dca63b6ef6 QIODeviceBase: make dtor protected  
The QIODeviceBase destructor is now protected to avoid deleting objects  
of classes derived from it through a QIODeviceBase pointer, which would  
be undefined behavior.  
  
* fb33e2a8e8 Add missing QT_TRID_N_NOOP definition  
Added missing QT_TRID_N_NOOP() macro. Lupdate actually recognizes it  
since Qt 5.12.  
  
* 71faedc5b4 Fix deserializing Qt 5.x fonts through QDataStream  
Fixed a problem deserializing the family of fonts that had been  
serialized using QDataStream in Qt 5.  
  
* b7f4041669 QAnyStringView: fix broken implicit conversion from  
QStringBuilder  
Implicit conversion from QStringBuilder to QAnyStringView now works as  
advertised.  
  
* 7fe5611365 QHash: optimize value(key) and key(value) callers  
The value(key) and key(value) functions are now overloaded on presence  
of the defaultValue (was: defaulted argument) to avoid injecting  
temporary objects into the caller's stack frame.  
  
* 04ec14105e Change qt.conf key Qml2Imports to QmlImports  
The key Paths/Qml2Imports has been renamed to Paths/QmlImports. For  
backwards-compatibility, Paths/Qml2Imports is still accepted and acts as  
default value for when Paths/QmlImports is not present.  
  
* 102f7d31c4 Add support for combining multiple QFutures  
Added QtFuture::whenAll() and QtFuture::whenAny() functions, returning  
a QFuture that becomes ready when all or any of the supplied futures  
complete.  
  
* 8ce3693856 QImageReader: check allocation limit for minimum 32 bpp  
When checking allocation limit during image reading, the memory  
requirements are now calculated for a minimum of 32 bits per pixel,  
since Qt will typically convert an image to that depth when it is used  
in GUI. This means that the effective allocation limit is significantly  
smaller when reading 1 bpp and 8 bpp images.  
  
* f5f7f78766 QObject: don't #include qproperty.h  
The qobject.h header no longer implicitly includes qproperty.h. If your  
code depends on the transitive include, explicitly include <QProperty>  
where needed.  
  
* f4e89d58da QVERIFY_EXCEPTION_THROWN: re-throw unknown exceptions  
Now re-throws unknown exceptions (= not derived from std::exception)  
(was: swallowed them and returned from the test function), in order to  
play nice with pthread cancellation.  
  
* 174af05400 QDir: Add support for setting directory permissions to  
mkdir()  
Added QDir::mdkir() overload that accepts permissions argument.  
  
* 1edf153a6b Long live QVERIFY_THROWS_EXCEPTION!  
Added QVERIFY_THROWS_EXCEPTION, replacing QVERIFY_EXCEPTION_THROWN,  
which has therefore been deprecated.  
  
* efb283fb7f Add QTest::failOnWarning  
Added QTest::failOnWarning. When called in a test function, any warning  
that matches the given pattern will cause a test failure. The test will  
continue execution when a failure is added. All patterns are cleared at  
the end of each test function.  
  
* c27d2a57a4 Make QAbstractProxyModel itemData() behave like data()  
The itemData() and setItemData() functions will now call the respective  
implementations in the source model (after mapping the index to a source  
index), matching what data() and setData() already did. Before, the  
proxy model simply called the default implementations of  
itemData()/setItemData() in its own base class (QAbstractItemModel).  
  
* ed343669f7 Long live QVERIFY_THROWS_NO_EXCEPTION!  
Added QVERIFY_THROWS_NO_EXCEPTION macro.  
  
* a0f9aef11b Long live Q_GADGET_EXPORT!  
Added the Q_GADGET_EXPORT macro, which is like Q_GADGET, but allows  
passing an export macro (like Q_NAMESPACE_EXPORT for Q_NAMESPACE).  
  
* 23f980799d QSharedPointer: fix counter-productive QT_PREPEND_NAMESPACE  
use in qHash() impl  
The qHash(QSharedPointer<X>) overload can now use qHash(X*) overloads  
found (only) through ADL (was: ADL was disabled due to qualified lookup  
of qHash(X*)).  
  
* 793417ce75 Fix gaps between lines of selection  
Fixed an issue where there would sometimes be visible gaps in  
selections spanning multiple lines.  
  
* 4c930e9d13 QNAM: Disable h2c by default  
Support for clear-text http/2 was disabled due to incompatibility with  
certain servers. If you were relying on this feature you must re-enable  
it by setting the QT_NETWORK_ALLOW_H2C environment variable. For a later  
version of Qt it will get a dedicated attribute.  
  
* 54536bb5ae QString::arg: deprecate use of arbitrary Unicode digits as  
replacements  
The arg() functions featured in Qt string classes have always been  
documented to require replacements tokens to be sequences of ASCII  
digits (like %1, %2, %34, and so on). A coding oversight made it accept  
sequences of arbitrary characters with a Unicode digit value instead.  
For instance, "%2੩" is interpreted as the 23rd substitution; and "%1²"  
is interpreted as the 12th substitution. This behavior is deprecated,  
and will result in runtime warnings. Starting from Qt 6.6, arg()'s  
behavior will be changed to accept only ASCII digits by default. That  
means that "%1²" is going to be interpreted as substitution number 1  
followed by the "²" character (which does not get substituted, so it  
gets left as-is in the result). Users can restore the previous semantics  
(accept Unicode digits) by setting the  
QT_USE_UNICODE_DIGIT_VALUES_IN_STRING_ARG environment variable to a non-  
zero value. In Qt 7, arg() will only support sequences of ASCII digits.  
Note that from Qt 6.3 users can also set  
QT_USE_UNICODE_DIGIT_VALUES_IN_STRING_ARG to zero; this will make arg()  
use ASCII digits only, in preparation for the future change of defaults.  
  
* d162ce3732 Add _make_aab target  
Add the extra _make_aab targets for each executable target, that can be  
used to generate android app bundles. Also add aab metatarget to build  
all _make_aab targets that are created in the project.  
  
* bda75c81f5 Fix missing characters or assert with certain font sizes  
Fixed an issue where characters would in some rare cases be missing  
from text, depending on font metrics, font size and system scale factor.  
  
* 6b02473e1e Fix overlapping text for Osaka font on macOS  
Fixed a problem where using the Osaka font would lead to overlapping  
text.  
  
* ebac49dd45 android:qmake: Fix static libraries to include the QT_ARCH  
suffix  
Static libraries targeting Android will now include an arch suffix when  
built using qmake.  
  
* dbb9579566 Text editing: smart block and char format after newline  
Hitting enter at the end of a line with a special block format  
(horizontal rule, heading, checklist item) now makes some "smart"  
adjustments to avoid retaining properties that are unlikely to be  
continued on the next line. Hitting enter twice now resets block and  
char formats to default.  
  
* 2d2104da7c QSizePolicy: make qHash() a hidden friend  
qHash() is now a hidden friend and can only be called by unqualified  
(qHash(sp)), not by qualified lookup (as in, say, ::qHash(sp) or  
QT_PREPEND_NAMESPACE(qHash)(sp)).  
  
* 63c0a1bd23 Add QFontComboBox::setSampleText  
Added the setSampleText() function, in order to be able to control the  
sample text displayed by the combobox (when previewing the fonts).  
  
* 98c2260c3b Add QFontComboBox::setDisplayFont  
Added the setDisplayFont() function, in order to be able to control the  
font used to render the font name and sample text (when previewing the  
fonts).  
  
* 56bd1b76d2 Don't change resolve mask when setting brush doesn't change  
palette  
Setting a brush on a palette that is identical to the current brush no  
longer sets the resolve mask bit for that particular role, so items  
using the palette will continue to inherit changes from parent items.  
  
* 83f2f27bb6 QFile: Add open() overload that accepts permissions  
argument  
Added QDir::open() overload that accepts permissions argument.  
  
* 9909ec0bc6 QNAM: Reintroduce h2c with an attribute  
Added QNetworkRequest::Http2CleartextAllowedAttribute which controls  
whether HTTP/2 cleartext (h2c) is allowed or not. The default is false.  
This replaces the QT_NETWORK_H2C_ALLOWED environment variable.  
  
* cdc3de6c84 QStringBuilder: Add support for QByteArrayView  
Added support for QByteArrayView.  
  
* 84fba93ebb QThread::create(): request interruption and join on  
destruction  
Destroying a QThread object created by QThread::create() while the  
thread that it manages is still running will now automatically ask that  
thread to quit, and will wait until the thread has finished. Before,  
this resulted in a program crash. See the documentation of  
QThread::~QThread() for more details.  
  
* c7248a3879 Implement fetching physical QStorageInfo::blockSize() under  
Windows  
The QStorageInfo::blockSize() will now report the physical block size  
of a storage device under Windows. Network mapped drives are not  
supported.  
  
* d4a88e4ea4 QVarLengthArray: fix size update on failed append()  
Fixed a bug whereby a failed append() would leave the container with an  
inconsistent size().  
  
* 3bbbd4ae12 wasm: update recommended emscripten to 3.0.0  
Recommended emscripten version is now 3.0.0  
  
* 4f53c703e4 QLocale: Extend support for language codes  
Added overloads for codeToLanguage() and languageToCode() that support  
specifying which ISO 639 codes to consider.  
  
* e297e80fd0 QVarLengthArray: make reallocation strongly exception safe  
The append()-like functions are now strongly exception safe. This means  
reallocation will now use copies instead of moves, unless the value_type  
has a noexcept move constructor.  
  
* 0800947d7d QVarLengthArray: fix UB (precondition violation) in range-  
erase()  
Fixed a bug where range-erase() could invoke undefined behavior when  
called with an empty range.  
  
* 48b75def5d QList: fix typo in QList(It, It)  
Fixed a regression that caused the range constructor to fail for pure  
input_iterator's.  
  
* 6a42363feb QVarLengthArray: widen append(p, n)'s contract  
The counted-range-append() function (append(ptr, n)) now accepts ptr ==  
nullptr, provided n == 0, too (was: triggered assertion).  
  
* b00404abff Trust CoreText-provided vertical metrics on macOS  
Fixed an issue where certain fonts, such as Monaco, would have a  
different line spacing than expected.  
  
* 85e92f2e5f QVarLengthArray: deprecate prepend()  
Deprecated prepend() because QVarLengthArray is the only Qt container  
without a "fast" prepend. If you require that functionality, even though  
it's a linear operation, then use insert(cbegin(), ~~~) instead.  
  
* 699e661b2b Add css media rule support for QTextDocument::setHtml()  
Add css media rule support for QTextDocument::setHtml()  
  
* f9b52f1958 Q_{APPLICATION,GLOBAL}_STATIC: use variadic macros  
The Q_GLOBAL_STATIC macro is now variadic. Any extra arguments are used  
as constructor arguments, obliterating the need to use  
Q_GLOBAL_STATIC_WITH_ARGS().  
  
* 4263ea6169 QVariant: use a typedef name when saving user types to  
QDataStream  
If QDataStream is used with a QDataStream::Version < Qt_6_0 to  
serialize a user type that was registered via a typedef with the  
metatype system, the typedef's name is used in the stream instead of the  
non-typedef name. This restores compatibility with Qt 5, allowing  
existing content to read the same QDataStreams; reading from older Qt 6  
versions should not be affected. (Note: if more than one typedef name is  
registered, it's indetermine which name gets used)  
  
* 02c8a20642 QStringBuilder: fix quadratic behavior in op+=  
Fixed quadratic behavior when repeatedly appending string-builder  
expressions (using operator+=) to QString/QByteArray objects.  
  
* 7e2860d415 QTestData: fix streaming of u8 string literals in C++20  
mode  
Fixed streaming of u8 string literals in C++20 mode.  
  
* 3666dad5e0 QByteArray: avoid detach() in a no-op replace()  
A replace(pos, n, after) call no longer detach()es when n ==  
after.size() == 0.  
  
* 41607ac85d SQLite: Update SQLite to v3.37.0  
Updated SQLite to v3.37.0  
  
* 2045d02393 QScreen_win: retrieve user friendly monitor name  
QScreen::name() now returns the user friendly name instead of the GDI  
device name on Windows. This is consistent with other platforms and also  
obeys the documentation.  
  
* 2dc04cf854 QTzTimeZonePrivate: fix UB (data race on m_icu)  
Fixed a data race on Unix platforms when implicitly-shared copies of  
QTimeZone objects were used in certain ways (e.g. calling displayName())  
from different threads and Qt was configured with ICU support.  
  
* 30cefa1c79 Fix crash when text shaping fails  
Fixed a possible crash with certain fonts when shaping strings  
consisting only of control characters.  
  
* 11d84fd5db QLatin1String: perform the comparison to another QL1S using  
memcmp()  
Fixed a couple of bugs where two QLatin1Strings or two QUtf8StringViews  
would stop their comparisons at the first embedded null character,  
instead of comparing the full string. This issue affected both classes'  
relational operators (less than, greater than, etc.) and  
QUtf8StringView's operator== and operator!=.  
  
* 2ed7c64dd9 JSON: When clearing duplicate object entries, also clear  
containers  
A memory leak in the JSON parser when reading objects with duplicate  
keys was fixed.  
  
* b02508c98a QMetaType: add a missing check for null d_ptr  
Fixed a bug that would cause QMetaType::compare() and  
QVariant::compare() to crash on invalid meta types and variants.  
  
* 3b83168eb8 QTabBar: Improve scrolling with high resolution mouse  
wheels  
Scrolling with a high resolution mouse wheel changes the current index  
at a rate more like a normal mouse wheel.  
  
* 4d273ab0d3 Enable all supported 1.0 device features in QVulkanWindow  
QVulkanWindow is now enabling all Vulkan 1.0 features reported as  
supported from the physical device.  
  
* c255d2ca7d QByteArrayList: simplify the join() overload set already  
now  
The join() overload set has changed. Code such as  
qOverload<>(&QByteArrayList::join) will have to be rewritten, e.g. using  
lambdas. We advise against taking addresses of library functions other  
than signals and slots.  
  
* 69e15a7f26 QStaticByteArrayMatcher: fix searching in 2+GiB haystacks  
Fixed searching in strings with size > 2GiB (on 64-bit platforms).  
  
* 388b418e36 QHash: fix iteration of x86 AES hash code for len >= 32  
Fixed a bug in the qHashBits() function, which affected the hashing of  
QByteArray, QString (and their View classes), QLatin1String and  
QBitArray, which caused the hash to not include the final 32 bytes of  
the data source. As a result, QHash containers where the initial string  
was the same had a serious performance degradation on x86 CPUs with AES  
support.  
  
* ea158430d5 rhi: d3d11: Switch the default swap effect and scaling mode  
With Direct3D 11 the default swap effect is now  
DXGI_SWAP_EFFECT_FLIP_SEQUENTIAL combined with DXGI_SCALING_NONE. This  
should provide a better (less "jumpy") resizing experience for Qt Quick  
content in particular, because the stretch effect for size-mismatched  
present is not ideal for user interfaces. We'd rather want to keep the  
size as-is and have the white border on the right/bottom (which we will  
have anyway, inevitably). This is also closer to what one gets with  
OpenGL (though that may depend on the driver as well). For Vulkan on  
Windows, the behavior will remain very similar to what  
DXGI_SCALING_STRETCH does, depending on the implementation probably,  
because the Vulkan spec fails to address the handling of scaling modes  
for size-mismatched presents. To get the old D3D behavior, i.e.  
FLIP_DISCARD+SCALING_STRETCH, set the environment variable  
QT_D3D_FLIP_DISCARD to a non-zero value.  
  
* b0b88f3420 Fix clipped glyphs in text rendering of QGraphicsTextItem  
Clipping of visible glyphs when doing partial updates of a graphics  
view was off by 1. Also fixed an issue that caused rounding errors when  
transforming the clip rect into the glyphs draw space which was caused  
by transforming a QRect instead of a QRectF.  
  
* e3eea5b2a9 Sequential erase/_if: don't apply predicate twice to  
element  
A fix in the implementation of the erase-like algorithms of sequential  
Qt container may re-enable signed/unsigned comparison warnings  
previously suppressed by having occurred in std library code. To fix,  
cast the value to look for such that it has the same signedness as the  
container's elements.  
  
* ac73f1ad90 QProcess/Unix: ensure we don't accidentally execute  
something from CWD  
When passed a simple program name with no slashes, QProcess on Unix  
systems will now only search the current directory if "." is one of the  
entries in the PATH environment variable. This bug fix restores the  
behavior QProcess had before Qt 5.9. If launching an executable in the  
directory set by setWorkingDirectory() or inherited from the parent is  
intended, pass a program name starting with "./". For more information  
and best practices about finding an executable, see QProcess'  
documentation.  
  
* 913915da08 Fix C++20 ambiguous relational operators between  
QJsonValue{,Ref}  
Fixed relational operators to not cause warnings/ambiguities when  
compiling in C++20.  
  
* e0babf6c2d QDesktopServices: fix ABA problem in  
QOpenUrlHandlerRegistry  
Fixed a bug where destroying and re-creating a handler object in quick  
succession could cause the registration for the handler to be lost.  
  
* 7a98858ff0 QDesktopServices: deprecate destroying URL handlers w/o  
explicit unsetUrlHandler()  
URL handlers that have been passed to setUrlHandler() must now be  
removed by calling unsetUrlHandler() before they are destroyed. Relying  
on the handler's destructor to implicitly unset it is now deprecated,  
because it may already be in use by concurrent openUrl() calls. Support  
for implicit unsetting will be removed in 6.6 and, until then, a  
qWarning() is raised if it is exercised.  
  
* b57de770ca QMetaObjectBuilder: fix addProperty() recording of the  
property type  
Fixed a bug that would cause addProperty() to use the incorrect type  
for the property if the property's name matched a valid type registered  
with QMetaType.  
  
* 1307bf2bbf QIODevice::readAll: allow reading from a huge non-  
sequential devices  
Changed readAll() handling of large non-sequential devices like files  
that are bigger than the maximum QByteArray size (on 32-bit systems,  
just under 2 GB). Previously, readAll() always returned empty; now it  
will attempt to read from the device.  
  
* 76f1bb3096 Treat invalid Q(Date)?Time as null when used as an SQL  
value  
Handling of QDateTime and QTime values passed to SQL now consistently  
treats invalid as null. Some values of these types are neither valid nor  
null, which could lead to invalid data being given to the SQL database.  
Invalid values are now treated as null to prevent this.  
  
* 45370ab793 QStringConverter: fix move special member functions of  
State class  
Fixed a potential data corruption in the move constructor and move-  
assignment operator on 32-bit platforms.  
  
* 741b367d6b MSVC: Raise minimum version of Visual Studio 2019 to 16.7  
The minimum MSVC version was raised to Visual Studio 2019 version 16.7  
(VC++ version 14.27). Trying to use an older version will now result in  
a compile time error.  
  
* 70828223f3 QGuiApplication: use translation-based layout direction  
unless explicitly set  
Calling setLayoutDirection with a non- auto value now disables the  
auto-detection based on installed translators. Applications that  
explicitly set a layout direction and also want translators installed  
afterwards to take effect should reset the layout direction to Auto,  
which is now no longer a no-op.  
  
* a7ab6235f7 Update bundled libjpeg-turbo to version 2.1.3  
libjpeg-turbo was updated to version 2.1.3  
  
* 9cbb14f25d CMake: Make configure less verbose by default  
The configure output verbosity of non developer-builds of Qt is now  
reduced by default. Pass "-- --log-level=STATUS" to configure to make it  
verbose again.  
  
* aae6eb8f6d QDataStream: make qfloat16 streaming a non-member  
The qfloat16 QDataStream operators are now hidden friends and only  
found by argument-dependent lookup. Previously, these were member  
functions on QDataStream.  
  
* 2c780c4398 qDecodeDataUrl(): treat ";base64" marker as case-  
insensitive  
Now recognizes the ";base64" marker in "data:" URLs case-insensitively.  
  
* b26b25bfaa QByteArray: fix isUpper/isLower  
The semantics of QByteArray::isLower() and QByteArray::isUpper() have  
been changed. Now lowercase (resp. uppercase) byte arrays are allowed to  
contain any character; a byte array is considered lowercase (resp.  
uppercase) if it's equal to its own toLower() (resp. toUpper()) folding.  
For instance, the "abc123" byte array is now considered to be lowercase.  
Previously, the isLower() (resp. isUpper()) functions checked whether  
the byte array only contained ASCII lowercase (resp. uppercase)  
characters, and was at least 1 character long. This had the side effect  
that byte array containing ASCII non-letters (e.g. numbers, symbols,  
etc.) were not lowercase nor uppercase.  
  
### qtsvg  
* 76eeb07 Limit font size to avoid numerous overflows  
Avoid numerous overflows by limiting font size to 0xffff. This fixes  
oss-fuzz issue 31701.  
  
### qtdeclarative  
* fb6baf03fa AbstractButton: emit doubleClicked() for touch events  
doubleClicked() is now also emitted for touch events.  
  
* 16fc4cf366 qqmllistmodel: Fix QObjects getting garbage collected  
ListModels now take ownership of the objects added to them, only  
releasing them after the object has been removed again. This may break  
existing solutions which rely on the object not being owned by the  
model.  
  
* 988d9dfe85 Allow registration of enums from related types to be  
switched off  
You can now suppress the registration of enums of "related" C++ types  
in a QML type. Such registration is often unintended and rather  
unpredictable. Set the "RegisterEnumsFromRelatedTypes" Q_CLASSINFO to  
"false" in order to suppress the registration.  
  
* a5404b2cb6 Deprecate QQmlExtensionPlugin::baseUrl()  
The internal function QQmlExtensionPlugin::baseUrl() has been  
deprecated. You don't need it if you properly specify your module in the  
qmldir file.  
  
* 37540467ca QQuickItem change contains function behavior  
Item.contains() now checks for coordinates less than the width and  
height, for consistency with childAt(), and because the item is drawn  
from (0,0) to (width-1, height-1).  
  
* 10e4dcc0cf Change QQuickItem childAt bounds check behavior  
QQuickItem::itemAt() now uses contains() for hit testing, so it is  
affected by containmentMask() if set.  
  
* c7297de660 Make QQuickItem containmentMask be dependent on position  
Previously, containmentMask's position was ignored. If containmentMask  
parent inherit from QQuickItem, then position will take into account. In  
some cases, this is useful, for example, to make click on button larger  
than the size of the button itself, in all directions, not just to the  
right and bottom.  
  
* b4cc56e6bf qmllint: Remove deprecated options  
options from Qt 6.1 are now fully removed, use the new style of options  
as outlined in --help.  
  
* a8fbd86514 Fix Flickable wheel velocity calculation  
Flickable no longer tries to detect whether you're using a "clicky"  
wheel or a touchpad, but rather does the velocity calculation more  
correctly with elapsed time (dθ / dt). A single rotation of a "clicky"  
wheel also moves a fixed distance, which is now adjustable via  
QStyleHints::wheelScrollLines(). Animation is restored, but should now  
stay in control on touchpads; and it will once again transition the  
"moving" properties correctly when scrolling ends.  
  
* d0dc91158d Avoid querying the file system for qmldir files for locked  
modules  
The pre-5.15 behavior of qmlProtectModule() has mostly been restored:  
If you explicitly protect a module, the QML engine will never look for  
any qmldir files or plugins for that module again. This severely limits  
what you can do with such a module. However, once all affected engines  
have loaded the module, protecting it can be a useful optimization. In  
contrast to pre-5.15, the qmldir cache for such modules continues to be  
re-used even after they are locked. Therefore, in QML engines that have  
loaded the module before, you can expect any "prefer" or "import"  
directives and any composite types to still be available after  
protecting the module.  
  
* 5864644ac8 Add button argument to the  
TapHandler.[single|double|]tapped signals  
TapHandler's tapped(), singleTapped() and doubleTapped() signals now  
have two arguments: the QEventPoint instance, and the button being  
tapped. If you need it, you should write an explicit function for the  
signal handler: onTapped: function(point, button) { ... } or  
onDoubleTapped: (point, button)=> ...  
  
* 0a3270f2da Add invokable QQuickItem::dumpItemTree()  
dumpItemTree() has been added; it can be called from C++ (similar to  
QObject::dumpObjectTree()) or from QML, to show the qDebug-operator  
output for an item and all its children, indented to show the tree  
structure.  
  
* c249edb83f disconnectNotifiers() more aggressively during object  
deletion  
When an object is queued for deletion, for example because its parent  
object is being deleted, then all of its change notifiers are dropped.  
This means no binding or signal handler that depends on properties of  
such an object will be triggered anymore. As you cannot read properties  
from such half-deleted objects anyway, there was never a point in being  
notified about further property changes. There may be corner cases where  
the notifications are used for some unrelated processing, though.  
  
* a15472716d Teach the qml runtime to load config files by basename  
The QML Runtime tool's -c / --config option now can find a directory  
containing a file called configuration.qml under  
QStandardPaths::AppConfigLocation, in addition to being able to give the  
full path to the configuration file, as before. I.e. on Linux you could  
write a custom configuration into ~/.config/QtProject/Qml  
Runtime/myconfig/configuration.qml and then use it via qml -c myconfig  
somefile.qml. The --list-conf option will list the configurations that  
can be found in this way.  
  
* 08ee029ed8 qml: Deprecate the --dummy-data option  
The QML Runtime tool's --dummy-data option is now deprecated, because  
context properties are deprecated. This option will be removed in a  
future version of Qt.  
  
* d4039298e7 QQmlEngine: Fine grained translation binding tracking  
QQmlEngine::retranslate no longer refreshes all bindings, but only  
translation bindings.  
  
* c71d1c363e QQmlDelegateModelAttached: Make static properties  
statically known  
DelegateModel's attached properties are now valid everywhere in its  
delegate, not only in the toplevel object.  
  
* f2a15482dd Add a Pragma for list assign behavior  
You can now specify the list property assignment behavior in QML using  
the "ListPropertyAssignBehavior" pragma. This is analogous to the macros  
you can use in C++.  
  
* b21948f5e8 Fix distorted text with subpixel matrix translation  
Fixed an issue where text using NativeRendering would look slightly  
skewed if it was inside a parent that had been positioned at a subpixel  
offset.  
  
* eca6bd4854 Implement horizontal rule rendering in text  
Horizontal rules (thematic breaks in markdown) are now rendered as  
simple horizontal lines, either in the same color as the text, or as  
specified via CSS background-color.  
  
* e14d13bea6 qmlformat: Implement settings file  
Adds the ability to set linting options via a settings file rather than  
using command line parameters. Use --write-defaults to generate a  
template with default values for editing. Use --ignore-settings to  
disable this feature.  
  
* 36e9a36b0d Use correct plugin name for Android QML plugins  
Starting with Qt 6.4, QML import mechanism won't add URI-based prefixes  
when looking for QML plugins for Android applications. For forward  
compatibility, the 'plugin' record of the qmldir files should contain  
the full file name of the plugin without abi-specific suffixes and the  
file extension. When using the CMake API to create the qmldir, no  
further action is necessary.  
  
* dbf7048ae2 Add calendar types  
Added types from Qt.labs.calendar/QtQuick.Calendar.  
  
* 3ccba598bc Calculate text metrics using design metrics  
renderType property added to specify if the metrics should match Qt or  
Native rendering.  
  
* 9b62f4c27a Allow any Item to act as a viewport for any of its children  
QQuickItem::clipRect() now provides the region visible in the viewport,  
and can be used to limit SG node vertices as an optimization in custom  
items, at the cost of having updatePaintNode() called more often. See  
docs about the new ItemObservesViewport and ItemIsViewport flags.  
  
* 063c5c7fae Fix missing glyphs when changing distance field parameters  
Fixed an issue where glyphs would sometimes be missing when changing  
the environment variables that define how distance fields are generated  
to certain values.  
  
* e17bfffc07 Add TapHandler.gesturePolicy: DragWithinBounds enum value;  
examples  
TapHandler now has one more gesturePolicy value: DragWithinBounds; it  
is similar to WithinBounds, except that timeHeld is not reset during  
dragging, and the longPressed signal can be emitted regardless of the  
drag threshold. This is useful for implementing press-drag-release  
components such as menus, while using timeHeld to directly drive an  
"opening" animation.  
  
* 4a5b0ad84f qquickdeliveryagent: Fix drag events being sent in the  
wrong order  
Now sends DragArea leave events before enter events when appropriate  
(QTBUG-82263)  
  
* 9db23e0e04 TextEdit large text: don't populate blocks outside the  
viewport into SG  
When given large text documents (QString::size() > 10000), Text and  
TextEdit now try to avoid populating scene graph nodes for ranges of  
text that fall outside the viewport, which could be a parent item having  
the ItemIsViewport flag set (such as a Flickable), or the window's  
content item. If the viewport is smaller than the window, you might see  
lines of text disappearing when they are scrolled out of the viewport;  
if that's undesired, either design your UI so that other items obscure  
the area beyond the viewport, or set the clip property to make clipping  
exact.  
  
* 58ff7aa4fe Compile QML files ahead of time with qmlcachegen  
QML bindings and functions are now compiled to C++ by qmlcachegen, if  
possible. Use the qt.qml.compiler.aot logging category to receive  
diagnostics about the compilation.  
  
* ab287508d5 QML test lib: propagate failOnWarning() feature to QML  
Added failOnWarning() for allowing to fail a test if a particular  
warning is output during that test execution  
  
* 18da655b77 quick: add qquicktreeview  
A new view is added: TreeView  
  
* 8c0b1e06d9 Fix focus for items inside a QQuickWidget in a  
QGraphicsProxyWidget  
  
  
* 93bdedc155 Add WheelHandler.blocking property  
WheelHandler now has a property called blocking, which is true by  
default; but if set to false, it allows wheel events to propagate to  
items "under" this handler's parent, and their WheelHandlers.  
  
* 2b50181be8 Add HoverHandler.blocking property  
HoverHandler now has a property called blocking, which is false by  
default; but if set to true, it prevents hover events from propagating  
to items "under" this handler's parent, and their HoverHandlers.  
  
* 1b4800e7c0 Add MessageDialog to QtQuick.Dialogs  
Added MessageDialog. This is a native MessageDialog on platforms that  
support it, and a non-native Qt Quick MessageDialog on platforms that  
don't.  
  
* 0ddb0d4b9b controls: add TreeViewDelegate  
New delegate added: TreeViewDelegate  
  
* e58cb58b44 Allow reparenting Pointer Handlers  
The parent property of any Pointer Handler is now settable.  
  
* 8326ff2ac1 Instantiator: don't interfere with delegates that assign  
parents  
Instantiator now avoids re-assigning a delegate object's parent to  
itself if it was already set; thus, you can now declare a parent  
assignment.  
  
* d4d56b519d Deprecate QQuickFontDialog::currentFont  
To make the font dialog's API consistent with the file and folder  
dialog, we're deprecating the "currentFont" property and replacing it  
with the "selectedFont" property, which previously was used as the final  
selection made by the user. By the time the user accepts the dialog, the  
currentFont and selectedFont had the same value anyways. So if the  
application needs to react "live" to which font the user is selecting,  
they can now simply bind to the selectedFont property, and if the  
application only wants to update a font when the user accepts the  
dialog, they can handle the accepted signal, and read from the  
selectedFont property in the signal handler.  
  
* 5ba0e82297 Add FolderDialog  
Added FolderDialog. This is a native FolderDialog on platforms that  
support it, and a non-native Qt Quick FolderDialog on platforms that  
don't.  
  
* 17feb77536 Pass qmldir to qmlcachegen, qmllint and qmltc, not the  
qmltypes file  
qmllint expects qmldir files, not qmltypes files to be passed via the  
-i option now. This enables it to see the imports and dependencies of  
the module being imported. For backwards compatibility it still accepts  
qmltypes files, with a warning.  
  
* a461d16a70 Make atlasing of compressed textures opt-in again  
Disable atlasing of compressed textures by default. Can be enabled with  
QSG_ENABLE_COMPRESSED_ATLAS=1  
  
* a318e6f354 Replace currentFile(s) with selectedFile(s)  
FileDialog's currentFile and currentFiles properties have been  
deprecated. The selectedFile and selectedFiles properties now refer to  
the currently selected file(s), as well as the final selection.  
  
* d39a0fbf26 Use qt.qml.states logging category instead of  
STATECHANGE_DEBUG env  
The new qt.qml.states logging category is useful for debugging states  
and transitions. It replaces the STATECHANGE_DEBUG environment variable.  
  
### qttools  
* 7bd1a834e lupdate: Support Python  
lupdate now supports Python.  
  
* aed245b1b windeployqt: Replace qmake querying with qtpaths  
windeployqt now uses qtpaths.exe instead of qmake.exe to query paths  
related to the Qt installation. This is also reflected in a new -qtpaths  
command line argument, which replaces the -query argument.  
  
* 50724a307 qdoc: Allow parameters for the \include command  
QDoc now allows extra parameters for the \include command to customize  
the quoted content.  
  
* cafdb2dbc Qt Designer: Enable the QWebEngineView, QQuickWidget plugins  
on Windows  
Qt Designer now sets the Graphics API to OpenGL in order to enable the  
QWebEngineView and QQuickWidget plugins.  
  
### qtpositioning  
* d454e613 QGeoAreaMonitorSource: add virtual methods to toggle custom  
properties  
Add virtual methods to set and get custom parameters. Helps to  
configure and control backend-specific behavior at runtime.  
  
* 965c80c5 CoordinateAnimation: fix direction interpolation  
The value of direction property for CoordinateAnimation is now handled  
correctly. Previously the values were confused, so specifying  
CoordinateAnimation.East direction was actually leading to moving West  
and vice versa.  
  
* 0fe43dd0 Fix positioning must be enabled and authorized at startup to  
work on iOS  
Fix positioning must be enabled and authorized on startup to work on iOS  
  
* 7c7eeee8 QGeoPositionInfo: add DirectionAccuracy attribute  
Added new DirectionAccuracy attribute. This attribute is available only  
on Android (API level 26 or above) and macOS/iOS. To represent the new  
attribute in QML, two new properties are added to Position QML object:  
directionAccuracy and directionAccuracyValid.  
  
### qtsensors  
* 175a5ab3 QtSensors Qt6 documentation base update  
sensorfw removed from docs for now  
  
* d40c4d0b Update QtSensors platform- and sensor support in Qt6  
Disable documentation  
  
* acd80292 Remove TI Sensor tag support  
Remove support  
  
* 9de2b478 Make geomagnetic mode the default magnetometer behavior  
The default magnetometer behavior is changed to be geomagnetic mode.  
  
### qtconnectivity  
* 43c01fbe Windows: extend QBluetoothLocalDevice implementation  
The implementation of QBluetoothLocalDevice on Windows is extended to  
support almost all features. The only missing parts are the  
connectedDevices() method and the deviceConnected()/deviceDisconnected()  
signals.  
  
### qtwayland  
* 639bd926 Ignore viewporter buffer size when buffer is null  
Fixed an issue in the wp_viewporter extension, where it would emit a  
protocol error if the viewport was configured before attaching a buffer  
to the surface.  
  
* 060024e2 Implement wp_viewporter support for video buffer formats  
Support for wp_viewporter extended to cover less common buffer formats.  
  
* baa7ef51 Fix the logic for decoding modifiers map in Wayland text  
input protocol  
Fix modifiers map decoding logic when receiving the map from the  
compositor.  
  
* d4a7faff Don't build XComposite buffer integration by default  
  
  
* f8b59e8c Remove the XComposite buffer sharing extension  
  
  
* b529ae8b client: Fix crash on shutdown on Mesa driver  
Fixed a crash on shutdown that could happen with some graphics-heavy  
applications when running on Mesa drivers.  
  
* f6c767b8 QWaylandBufferRef: fix relational operators  
Two const QWaylandBufferRefs can now be compared for equality (before,  
the LHS was not allowed to be const).  
  
### qt3d  
* d79376732 Fix multi-view picking  
Non rendered entities (due to layer filtering) are no longer pickable  
  
* 3964b2734 Disable RHI Renderer by default  
RHI Backend is not longer built by default  
  
### qtimageformats  
* 80786b7 Update bundled libwebp to version 1.2.1  
Update bundled libwebp to version 1.2.1  
  
* 7964a3d Update bundled libwebp to version 1.2.2  
Update bundled libwebp to version 1.2.2  
  
### qtserialbus  
* 8eaa91e CAN: Fix overreading QByteArray buffer  
Fixed potential read buffer overflows when sending CAN frames in  
diverse CAN backends which were detected by Address Sanitizer.  
  
* b0a6187 QCanBusFrame: Add constexpr where applicable  
Made more member functions constexpr.  
  
* 3b2ce7c QCanBusDeviceInfo: Add method to obtain the plugin name  
Added the CAN bus plugin name to QCanBusDeviceInfo.  
  
### qtwebsockets  
* d196801 Clear frame before emitting signals to prevent duplicating  
messages  
Clear frame before emitting signals to prevent duplicating messages  
  
### qtwebchannel  
* d711fc8 Transparently handle QFuture<T> method return types  
Transparently handle QFuture<T> method return types  
  
### qtwebengine  
* 5f723fe74 Fix QWebEngineQuick namespace for webenginequick module  
Use namespace QtWebEngineQuick QtWebEngine::initialize() is now  
QtWebEnigneQuick::initialize()  
  
* 2ad450018 Add API for favicon database  
image:/favicon/ URLs now can be used to access icon database.  
  
* d0ff107c0 Make default profile off the record  
Default profile is off-the-record Off-the-record profile can have  
registered protocol handlers.  
  
* 8f7a386a5 Remove deprecated useforglobalcertificateverification  
(Q)WebEngineSettings::useForGlobalCertificateVerification has been  
removed.  
  
* 13254e795 WebEngineNavigationRequest: add accept/reject and deprecate  
setAction  
setAction(action) is deprecated in favor of new accept/reject methods  
  
* b7634f470 Disable kAllowContentInitiatedDataUrlNavigations  
Page content may no longer navigate to data-urls, if this is needed we  
recommend using custom-url schemes instead or force old behavior using  
--enable-features=AllowContentInitiatedDataUrlNavigations, though the  
feature switch may be removed in any later update.  
  
* e90ed198b Add charset parsing to custom scheme handler's content type  
Charset is now explicitly parsed from provided contentType  
  
### qtvirtualkeyboard  
* 63a944ff Fix high CPU utilization caused by key repeat timer  
Fixed high CPU utilization caused by key repeat timer.  
  
* 71d67571 Disable Windows IME when Qt Virtual Keyboard plugin is loaded  
Disable Windows IME when Qt Virtual Keyboard plugin is loaded  
  
* ca5b712d Fix processing of hard Qt::Key_Backspace and Qt::Key_Delete  
Fix processing of hard backspace and delete keys.  
  
* a9da9816 cerence-hwr: Fix compilation with the latest Cerence SDK (v9)  
Added support for the latest Cerence SDK (9.x).  
  
* 1129af13 Use a containment mask to keep input panel working during  
modal session  
Since Qt 5.15, the virtual keyboard's input panel has automatically  
been reparented to prevent the keyboard UI from being blocked by modal  
dialogs. This is no longer done; the input panel instead uses a  
containment mask on the dimmer item that blocks input during modal  
sessions, allowing clicks through to the keyboard UI.  
  
### qtscxml  
* 3baa625 Rename qscxmlc CMake options  
Rename QSCXMLC_ARGUMENTS and OUTPUT_DIR CMake variables to be better  
aligned with other CMake APIs (OPTIONS and OUTPUT_DIRECTORY  
respectively).  
  
### qtlottie  
* 3399742 Fix loading of LottieAnimation::source  
Fixed bug that prevented LottieAnimation from loading its source from a  
relative URL.  
  
### qtquick3d  
* ae0e65e5 Enhance add_lightprobe_images file name handling  
The qt6_add_lightprobe_images CMake function, which is the new name of  
qt6_quick3d_bake_lightprobe_hdri has been changed to match  
qt6_add_resources when it comes to the handling of PREFIX, BASE, and  
FILES. It no longer strips the directories from the entries in the FILES  
list. This means that invocations that previously catered for the  
special behavior by listing the necessary extra directories in PREFIX  
must now be changed to not do that anymore. In addition, support for the  
OUTPUTS keyword has been introduced, in order to have API symmetry with  
qt6_add_shaders.  
  
* 85099d70 Improve handling of materials that depend on the screen  
texture  
This patch changes the content of the screen texture. The intention of  
the screen texture is to enable a material to bind the contents of the  
framebuffer currently being rendered to, and that should include the  
background as well. Previously the background of the screen texture was  
always transparent (alpha = 0.0), but now this will depend on the  
backgroundMode set in SceneEnvironment.  
  
* 2b4b038a Add support for KHR_materials_ior to PrincipledMaterial  
This patch changes the default value of specularAmount to 1.0. This  
property as documented should only modify the amount of the specular  
contribution. A value of 1.0 means that full specular contribution,  
where a value less than 1.0 mean less than the full specular  
contribution. Previously the value of 0.5 was halfing the specular  
contribution leading to much less impressive reflections. This was  
because the value of specularAmount was also being used under the hood  
to calculate the dielectric specular value used for the F term. It is  
much more accurate to use the index of refraction instead for this.  
  
* 30cb6ac4 Apply Occlusion map to global ambient light as well  
Occlusion maps now also affect the indirect lighting provided by  
punctual light's ambientColor  
  
### qtshadertools  
* b4394f2 Change PREFIX and FILES path handling to match add_resources  
The qt6_add_shaders CMake function has been changed to match  
qt6_add_resources when it comes to the handling of PREFIX, BASE, and  
FILES. qt6_add_shaders no longer strips the directories from the entries  
in the FILES list. This means that invocations that previously catered  
for the special behavior by listing the necessary extra directories in  
PREFIX must now be changed to not do that anymore.  
  
### qtopcua  
* 629a080 OpcUA: Fix attribution of Open62541  
Complete list of licenses in opengl62541 files: MPL-2.0, CC0-1.0, CC-  
BY-SA-4.0, BSD-3-Clause, Apache-2.0, and MIT  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-92232 [REG] Option Clicking Window Close Button Crashes App  
* QTBUG-65637 Window minimizing broken after building QT app with Mac OS  
High Sierra SDK  
* QTBUG-91025 Should mention that QPrint Support is not available for  
iOS  
* QTBUG-70498 Cannot scroll first tab right, using scroll button in  
QTabBar, when tab size do not fit into visible rect.  
* QTBUG-64543 When starting a drag scroll via QScroller in a listview  
there will be a slight jump right before the scrolling starts  
* QTBUG-50866 QTabBar scroll buttons overlap tabs  
* QTBUG-94248 Check scrollbar ScrollBarOverlap when computing QListView  
margins  
* QTBUG-84117 QHeaderView sort indicator and text overlap if both  
aligned right  
* QTBUG-27640 QToolButton::menu-arrow{image:none;} does not work in  
Custom TitleBar  
* QTBUG-86362 [Reg 5.14 to 5.15.0] macOS: Tabbed QDockWidgets not  
properly drawing the tabs  
* QTBUG-71894 Hangul composition bug  
* QTBUG-94442 Update dependencies on '6.1' in qt/qttools fails  
* QTBUG-94264 When building for Android, instead of an apk, just .so is  
built  
* QTBUG-91120 QDate::fromString() fails on isolated dates on macOS with  
TZ=Europe/Lisbon  
* QTBUG-94400 /EHsc flag removal wrong  
* QTBUG-94347 QRandomGenerator64 refers to functions as static, aren't.  
* QTBUG-20456 QAbstractItemView: When clicking on an item that is being  
edited and the edit trigger is SelectedClicked it should just stop  
editing  
* QTBUG-94470 Incorrect parsing of HTTP2 frame headers.  
* QTBUG-94032 Command line is too long when building large projects  
* QTBUG-68936 tst_QDateTime::daylightTransitions() makes invalid  
assumptions  
* QTBUG-94532 Markdown checkboxes are clipped when text range selected  
* QTBUG-76948 IOS: disconnect second screen while app in b/g, it crashes  
when app goes into foreground  
* QTBUG-92878 [qt6/cmake] Qt Resource object libraries not found in  
sibling scopes due to not being global  
* QTBUG-85523 When there is no header then is no border for the cell on  
the side without the header  
* QTBUG-93764 QPrintPreviewDialog: printer orientation not updated by  
QPageSetupDialog  
* QTBUG-91130 SIGSYS error in QSystemSemaphore for iOS  
* QTBUG-94568 Build error when depending on internal module in qtbase  
* QTBUG-94501 GStreamer::Gl dependency is not recorded correctly in a  
static build  
* QTBUG-94448 QtWidgets: Some stylesheets explode Designer and the whole  
linux terminal (recursion crash)  
* QTBUG-94175 QGraphicsProxyWidget: rendered Arabic text incomplete in  
large font sizes when OpenGL is used  
* QTBUG-85714 QOpenGLWidget with NativeWindow QDockWidget does not  
render when undocked  
* QTBUG-89379 QQuickWindow::QtTextRendering cause font problem on Apple  
M1  
* QTBUG-94069 MacOS ComboBox Focus Ring is Too Tall  
* QTBUG-82835 Stale socket notifications can be emitted to new sockets  
* QTBUG-85529 Polytonic Greek characters cannot be composed both ways  
* QTBUG-94246 Memory leak in qsql_oci plugin  
* QTBUG-91919 Qt will crash if changing screen resolution on Mac  
* QTBUG-94706 missing documentaiton details about QFile::copy()  
* QTBUG-94591 qmake doesn't search mkspecs files in the right location  
* QTBUG-94538 Change cursor theme is not applied immediately . The Qt5  
app needs to be restarted.  
* QTBUG-87989 "ASan runtime does not come first in initial library list"  
when building Qt Quick application with Qt configured with -sanitize  
address  
* QTBUG-92083 Building console project fails with linker errors  
* QTBUG-83869 Correction to the documentation:  
https://doc.qt.io/qt-5/qtransform.html#basic-matrix-operations  
* QTBUG-81251 _debug libraries are missing from pre build Qt on Mac  
* QTBUG-94708 qCDebug() and friends could pass the category as a tag in  
Android  
* QTBUG-94527 Building Android QML projects with qmake is broken  
* QTBUG-94839 QSystemTrayIcon::isSystemTrayAvailable() opens a new file  
descriptor on each call which isn't closed  
* QTBUG-92477 Memory leak in QFontDatabase  
* QTBUG-94781 [Reg-5.15.4->5.15.5] Bold font is not picked up when  
QFontDatabase is used  
* QTBUG-91398 When QFont::NoFontMerging is set then if bold or italics  
is requested that is not provided by the font then it will end up not  
synthesizing this  
* QTBUG-94445 Android unit test runner does not report failures, always  
Success  
* QTBUG-88508 some tests are not saving result output to file on Android  
* QTBUG-92122 QEvent::Quit missing from QEvent type documentation  
* QTBUG-92157 Qt configured without Vulkan support in 6.1 Android  
packages [Vulkan crashes on SA8155 (Qualcomm)]  
* QTBUG-91619 QCFSocketNotifier does not handle connect  
* QTBUG-93890 Crash in webOS emulator with recent meta-qt6  
* QTBUG-94944 qt6_qml_type_registration with VS19 cmake generator  
outputs error: "The dependency target "qt6-test_autogen" of  
target"qt6-test_automoc_json_extraction" does not exist.  
* QTBUG-38776 QDockWidget titlebar icons are not drawn with high DPI  
* QTBUG-76945 macOS: When providing your own icons for a dock widget  
titlebar in a stylesheet, the old one can be drawn on top  
* QTBUG-39427 Repeatedly setting a widget style sheets has issues  
* QTBUG-18958 setting stylesheet more than once before showing the  
widget causes resetting stylesheet doesn't work  
* QTBUG-94973 Build fails when configuring twice with CMake and with  
both INSTALL_MKSPECSDIR and QT_QMAKE_TARGET_MKSPEC set  
* QTBUG-94802 [Reg-5.15.4->5.15.5]Menu separator is not visible  
* QTBUG-95005 Typo in QOpenGLPaintDevice::dotsPerMeterY  
* QTBUG-91632 Make /usr/local/Qt-6.x the default install folder instead  
of /usr/local  
* QTBUG-94824 In qlinedit, icon and text overlap  
* QTBUG-95027 Building a DEBUG CMake project against a -debug-and-  
release Qt fails  
* QTBUG-95039 String translations cancelled in qsystemerror.cpp  
* QTBUG-94799 QFileDialog file name completer doesn't work with Proxy  
Model  
* QTBUG-78043 non-native QFileDialog displaying incorrect mapped network  
drive names  
* QTBUG-95028 Apps created by qt_internal_add_app are placed in a  
bin/Release subfolder in a -debug-and-release build  
* QTBUG-95043 QDebugMessageServiceFactoryPlugin_init.cpp.obj is  
incorrectly dynamically linked instead of statically linked to runtime  
library  
* QTBUG-94921 Feature poll_select is already defined to be "ON" and  
should now be set to  "OFF" when importing features from Qt6::Core.  
* QTBUG-85972 [REG: 5.9->5.12]: When the height of a button goes below  
31px then it will start to shift the button down instead of making it a  
square button so it can be made smaller  
* QTBUG-91125 QTextFormat::FullWidthSelection does not work with right-  
to-left text layout  
* QTBUG-95042 QFrame Qt::WA_TranslucentBackground is broken with  
specific window flags and drawable child item  
* QTBUG-92561 Strange selection behavior of with ExtendedSelection +  
SelectRows  
* QTBUG-95011 QLineEdit inconsistently changes layout direction when  
text changes  
* QTBUG-95077 [5.15/6.1->6.2] Some library names now have a "Private"  
suffix  
* QTBUG-89022 QImageWriter insufficiently supports QSaveFile  
* QTBUG-83619 Stylesheet: QAbstractItemView::indicator changes selected  
item text color  
* QTBUG-73966 When using QMenu::icon:checked inside a stylesheet it is  
being ignored and has no effect  
* QTBUG-94981 QTreeView: expandToDepth() and expandAll() ends  
prematurely for asynchronous models  
* QTBUG-95013 pt_BR translations not loaded  
* QTBUG-93829 QItemSelectionModel::hasSelection is inconsistent  
* QTBUG-95223 Remove the QClipboard class's warning info  
* QTBUG-94788 QListView will be reset when setSelectionMode  is  
MultiSelection  
* QTBUG-94942 QML type registration emits "qt6quick_metatypes.json:  
illegal value"  
* QTBUG-95198 Building QtMultimedia qmake projects is broken on Windows  
* QTBUG-86846 the password box not refreshed under Chinese input method  
* QTBUG-94737 Crash in QThreadOnce test  
* QTBUG-95277 HTTP2: QNetworkReply::encrypted not emitted  
* QTBUG-95009 QNetworkDiskCache::cacheSize() returns a size twice as  
large as the real one.  
* QTBUG-94733 When the display is set to 150% and a QMdiSubWindow is  
maximized then the icons can be incorrectly displayed  
* QTBUG-93466 QTransposeProxyModel. LayoutChanged bug  
* QTBUG-95293 QCocoaAccessibilityElement incorrect selector for  
"enabled": should be isAccessibilityEnabled not  
accessibilityEnabledAttribute  
* QTBUG-85410 [Reg 5.9 -> 5.12] Cannot open filesystem root with  
Qt.openUrlExternally  
* QTBUG-95283 No TLS backend available in statically built project  
* QTBUG-95229 Qt for Windows configured with -debug-and-release fails to  
build with CMake 3.21.0  
* QTBUG-95255 After setDefaultAction for a QToolButton and call  
setChecked, then checked status wrong  
* QTBUG-91048 QFutureWatcher::isFinished() stays false after  
waitForFinished()  
* QTBUG-95310 QMouseEvent methods marked as deprecated in code aren't  
marked as such in docs  
* QTBUG-91459 When using Speech Recognition on a multiple monitor setup  
telling it to click a button does not always work on the secondary  
monitor  
* QTBUG-20726 QNetworkAccessManager connection cache timeout should be  
configurable  
* QTBUG-91440 Very high CPU on socket timeouts when QNAM has lots of  
connections  
* QTBUG-95239 Massive memory consumption when rendering small svg  
* QTBUG-12055 Segfault in QTextStream  
* QTBUG-95254 When passing a string that has a % inside it to  
QUrlQuery::addQueryItem then it will not escape the % if it is followed  
with 2 hexadecimal characters  
* QTBUG-95334 QMap<QString,QString>::const_iterator cannot do "it+1" any  
more  
* QTBUG-90662 Fix CI warnings qtbase  
* QTBUG-80576 CMake build doesn't find MoltenVK  
* QTBUG-95391 [REG] WrapVulkanHeaders::WrapVulkanHeaders not found on  
system without Vulkan development package  
* QTBUG-95454 Version 6.1.2 found in Qt6.2 sources  
* QTBUG-77656 Crash when waking up with multiple displays in clamshell  
mode  
* QTBUG-95050 [REG: 5.2->5.14] Locale used by  
QString::localeAwareCompare() no longer changeable  
* QTBUG-95383 QFileSystemModel sort extremely inefficient with wildcards  
* QTBUG-89294 QScrollArea fails to re-layout widgets correctly in high  
DPI environments  
* QTBUG-94790 moc fails to parse include inside enum  
* QTBUG-95429 Expired certificates in tst_QSslCertificate  
* QTBUG-93004 Assert and crash in qcalendar.cpp when the first call to  
QDateTime::toString is done from two simultaneous threads  
* QTBUG-95619 [Mac] Memory leak in  
QNSWindow::applicationActivationChanged  
* QTBUG-86227 Implement or drop the -coverage configure argument for the  
CMake build  
* QTBUG-95273 QFuture::then() documentation about threading is unclear  
* QTBUG-95577 Incorrect punycode encoding and decoding for non-BMP  
codepoints  
* QTBUG-56595 QXcbConnection::getTimestamp() returns old timestamp  
* QTBUG-69515 Linux, WindowStaysOnTopHint does not work.  
* QTBUG-20894 QCompleter unexpectedly changes QLineEdit text  
* QTBUG-95635 qtbase fails to configure on Linux with CMake 3.21.1 and  
policy CMP00126 enabled  
* QTBUG-95655 CMake couldn't find "FindWMF.cmake" in top-level builds  
* QTBUG-8096 icon-size stylesheet property is defined as length but only  
lengths in px can be used  
* QTBUG-95071 mysql client version detection broken with MariaDB 10.6  
* QTBUG-95441 6.2: The basic QFont constructor deprecated?  
* QTBUG-95607 Screen rotation causes wrong menu position  
* QTBUG-95631 Stylesheet issue when try to change background color with  
a editable combobox on hover  
* QTBUG-95552 Reproducible crash from wheelEvent in QGraphicsScene  
containing a QWidget with a Q*BoxLayout  
* QTBUG-95471 Unable to compose characters on Mac OS in text edits  
* QTBUG-95720 REG: 5.15->6.1: Drawing text on a printer will end up  
having badly rendered text  
* QTBUG-95689 Missing overflow handling allows alternative Punycode-  
encoded domain name representations  
* QTBUG-93999 CMake Install fails with -debug-and-release and -separate-  
debug-info  
* QTBUG-95652 Revice changes in configure summary options, 6.2.0  
* QTBUG-95732 The build system does not work correctly with  
-DFEATURE_developer_build:BOOL=TRUE  
* QTBUG-69975 Cocoa NSFullSizeContentViewWindowMask was wiped when  
toggling fullscreen  
* QTBUG-2390 Generated .la files are not correct for frameworks  
* QTBUG-94031 FILE_ID_INFO is redefined when using MinGW-w64 version  
9.0.0  
* QTBUG-95639 MariaDB 10.6 prepared queries metadata cache causes  
breakage in mysql driver  
* QTBUG-95214 QtConcurrent::run requires the return type to be default-  
constructible  
* QTBUG-95827 qmake CONFIG+=Debug leads to release builds  
* QTBUG-95602 App wizard QtQuick Empty with language failed to find Qt  
component "LinguisticTools"  
* QTBUG-95841 [REG-5.15->6.2]QMainWindow::VerticalTabs is broken in Qt6  
* QTBUG-95389 link in QSet documentation missing  
* QTBUG-95795 Crash when running a qt quick app on iOS simulator  
* QTBUG-95806 Qt6WasmMacros.cmake uses wrong paths for wasm_shell.html,  
qtloader.js and qtlogo.svg  
* QTBUG-94215 [Reg 5.15.2->5.15.3/6] QString::lastIndexOf is broken  
* QTBUG-81770 Garbled character is displayed when switching Arabic to  
another language  
* QTBUG-30522 macOS: Closing application window while context menu is  
open leaves menu open  
* QTBUG-89472 Building Qt for Android with -ltcg fails to compile  
* QTBUG-89177 MacOS Dark Mode button text is not contrast enough to be  
readable  
* QTBUG-70255 QScroller::scrollTo fails in QGraphicsView with movable  
item  
* QTBUG-95943 qt-configure-module -help is not implemented  
* QTBUG-95716 qlistview select box residual thin line  
* QTBUG-95846 QPropertyAlias crashes in all situations  
* QTBUG-95341 QLineEdit lineRect should use boundingRect height  
* QTBUG-94529 Using Titillium Web on Windows creates rendering artefacts  
* QTBUG-94951 Qt 6.2 alpha assertion failed in qunicodetools.cpp  
* QTBUG-94091 Nested Graphicsview does not works as expected  
* QTBUG-95950 QNetworkAccessCache crash  
* QTBUG-87128 In the help pages: The QFileInfo::setFile() example is  
really the QDir::setCurrent() one  
* QTBUG-67819 QGraphicsViewProxy does not propagate touch events to the  
child of the widget  
* QTBUG-45737 No touch events handling (QGraphicsProxyWidget / QWidget)  
* QTBUG-96009 tst_QGraphicsProxyWidget::mouseDoubleClickEvent fails  
* QTBUG-89549 Linker error when building Qt 6 statically with cmake +  
clang on Windows  
* QTBUG-46300 Qt's application ignore some input method behavior  
* QTBUG-71394 Long-press to show popover for accented/alternate  
characters does not work correctly on macOS  
* QTBUG-72744 macOS: Qt does not hide cursor when entering text  
* QTBUG-95942 The elidedtext() function cannot realize text ellipsis in  
Tibetan  
* QTBUG-88774 QNetworkAccessBackend documentation is missing a class  
entry  
* QTBUG-96101 QPMCache deleted from another thread  
* QTBUG-92018 QLocale date toString uses standalone name where plain  
name should be used  
* QTBUG-86279 QLocale::system()'s standaloneDayName() and dayName() use  
the same back-end  
* QTBUG-95463 QListView in view mode QListView::IconMode crashes when  
the last row is moved  
* QTBUG-95959 Extend qnetworkaccesscache testing  
* QTBUG-65457 Improper handling of TILED displays (4K / 5K / 8K etc.) /  
support for RandR v1.5  
* QTBUG-96067 Build failure with riscv32  
* QTBUG-96123 Wrong character  
* QTBUG-46701 Closing a full screen window via Qt APIs leaves the screen  
black on macOS  
* QTBUG-88088 variable QTSYNC_QT cannot be set by the user  
* QTBUG-89562 qt_lib_network_private.pri contains  
QMAKE_LIBS_OPENSSL/NOLINK entry  
* QTBUG-52450 macOS: Closing a window that's in fullscreen removes the  
window, but doesn't exit fullscreen  
* QTBUG-68069 Exiting fullscreen window leaves the application in  
fullscreen mode on macOS  
* QTBUG-81552 macOS: Wrong cursor shown when the mouse is moved slowly  
into window  
* QTBUG-96003 [Reg Qt5.9.9 -> Qt5.15] setCursor() does not work on  
QWidget inside QWidget  
* QTBUG-95358 Possible null pointer dereference in qpixmap.cpp  
* QTBUG-96197 Yocto build fails in CI for 6.2.0-beta4 qtbase  
* QTBUG-96170 WASM: data URI scheme does not work  
* QTBUG-91707 [Reg 5.15->6.0] Recursive QMap as MetaType cannot have key  
with custom operator==  
* QTBUG-91059 Mac: Multiple modal dialogs block all input  
* QTBUG-96268 qurlrecode memcpy triggering a fatal warning  
* QTBUG-30617 QtConcurrentMap does not map QJsonArray  
* QTBUG-96062 Integrity linker can't cope with duplicate object files on  
command line  
* QTBUG-95565 Qt Creator cannot build Qt 6 for iOS from the start  
* QTBUG-96103 Memory corruption in  
tst_qreadwritelock::multipleReadersLoop()  
* QTBUG-96305 [REG 5.15.5 -> 5.15.6] xcode builds broken if OBJECTS_DIR  
set  
* QTBUG-96285 QProcess can't be restarted  
* QTBUG-96359 QProcess related crash (purely on Windows)  
* QTBUG-79016 Processing qm file name error when using config  
embed_translations  
* QTBUG-94835 Font Weight not properly reflected  
* QTBUG-72872 Nested QtConcurrent::map cause deadlock  
* QTBUG-96543 tst_shadersource fails  
* COIN-755 Integration is blocked in dev  
* QTBUG-59394 Q_INIT_RESOURCE cannot be called from main to initialize  
resources in a shared library  
* QTBUG-96085 Cannot configure qtdeclarative with tests on Android  
* QTBUG-96208 macOS: Crash on application exit due to unloading library  
with objc class  
* QTBUG-83908 Material.System does not work on Windows 10 in Dark Mode  
* QTBUG-95108 Reg[Qt 5.15.4->Qt5.15.5] Qt::MetaModifier and  
Qt::GroupSwitchModifier is always set  
* QTBUG-95289 GroupSwitchModifier always present in event.modifiers()  
* QTBUG-49771 Backspace key is not working when CapsLock is on  
* QTBUG-96600 Some QGuiApplication command line options have incorrect  
descriptions  
* QTBUG-96345 tst_QSocks5SocketEngine::simpleConnectToIMAP() is flaky on  
Ubuntu  
* QTBUG-89765 Vulkan: view3d example occasionally(?) has broken indexed  
drawing  
* QTBUG-96288 QTextEdit cursor postion error when QTextEdit has  
different pointsize  
* QTBUG-96247 QScreen crash on Linux/X11  
* QTBUG-42985 Qt GUI application disappear or crash when no screens are  
available  
* QTBUG-96594 qt_add_dbus_adaptor behaves different than  
qt6_add_dbus_adaptor  
* QTBUG-96619 QRhi declares types with non-relocatable QVLA in them as  
relocatable which can lead to crashes  
* QTBUG-91090 CPU feature detection broken with CMake  
* QTBUG-87669 few gui tests fail to build on Android  
* QTBUG-95202 Auto-generated android-*-deployment-settings.json contains  
wrong path to immediate qrc file on Qt 6  
* QTBUG-95235 Building Quick Controls 2 examples with Qt 6.1.1 for  
Android fails  
* QTBUG-96511 MacOS iframework paths missing when using  
QT_ADDITIONAL_PACKAGES_PREFIX_PATH  
* QTBUG-96513 CI: qmake examples should not be built from tainted source  
tree  
* QTBUG-96659 Compiler error in qproperty_p.h  
* QTBUG-96300 The build system does not work accept  
-DFEATURE_cxx20:BOOL=TRUE  
* QTBUG-96392 HAVE_egl_x11 test fails with libglvnd 1.3.4  
* QTBUG-96690 Qt6. Build failed when use std::optional as a signal  
argument  
* QTBUG-96726 [Reg: 6.2 beta3->6.2 beta4] Key event is wrongly passed on  
* QTBUG-54848 Problem with QAbstractItemDelegate and IME (chinese Input  
Method) with edit trigger QAbstractItemView::AnyKeyPressed  
* QTBUG-96606 CA certificates not fetched on Android  
* QTBUG-36926 Mac OS: Mouse hover events are sometimes ignored  
* QTBUG-42661 Wrong dialog activation  
* QTBUG-96639 QMainWindow crash during "closeEvent"  
* QTBUG-67702 QTest::ignoreMessage() fails to match regex against  
warning string  
* QTBUG-96838 signing Android app bundles fails with 6.2.0-rc  
* QTBUG-78970 REG 5.9.4 => 5.12.4 setAutoRaise not working on Mac  
* QTBUG-96926 QImage::convertToFormat(format, colorTable) doesn't  
preserve devicePixelRatio  
* QTBUG-96798 Separate debug info builds are broken when cross-  
compiling, wrong objcopy is used  
* QTBUG-96322 Crash on RHI with Opacity Mask effect  
* QTBUG-96906 iOS / Android / WebAssembly have invalid [DevicePaths]  
Prefix in target_qt.conf when installing Qt from online installer  
* QTBUG-96846 Many messages "QThread::wait: Thread tried to wait on  
itself" when Creator starts new threads  
* QTBUG-94882 Building qtbase unit tests for Android fails  
* QTBUG-86094 Generating large pdf files when using pen with zero width  
* QTBUG-96466 [REG 5.15.2-6.2.0] Runtime crash on changing screen's  
scale factor  
* QTBUG-96701 android-build projects cannot be used in Android Studio  
* QTBUG-66513 qApp activeWindow wrong after button menu popup  
* QTBUG-69710 QLineEdit can't be used for keyboard input after popup  
menu from another QDialog  
* QTBUG-78750 macOS: Context menus become unusable  
* QTBUG-85058 Windows: QDir::entryList doesn't work for directories that  
end with '.lnk'  
* QTBUG-96621 Missing QHash include in qcocoawindow.h  
* QTBUG-97023 Fix invalid Qt6::ATSPI2_nolink target  
* QTBUG-94341 Windows: Let QLocale::uiLanguages() return all preferred  
languages  
* QTBUG-13965 QPainterPath::addText() does not respect QFont::SmallCaps  
* QTBUG-77854 QFont::setStretch ignored after calling  
QFont::setStyleName  
* QTBUG-96998 CMake: UNIX is not set for INTEGRITY builds  
* QTBUG-96978 Brush transformations are not supported by the PDF engine  
* QTBUG-97119 Escape doesn't close popups anymore  
* QTBUG-97085 Crash while JITting QRegularExpression in multiple threads  
(Rosetta)  
* QTBUG-93885 ASSERT failure in void __cdecl  
QtFontFamily::ensurePopulated(void) on system registed font  
* QTBUG-79140 [REG 5.13.0 -> 5.14.0]OTF fonts don't work correctly  
* QTBUG-96286 [Reg 5.9.8 -> ] QWidget loosing contents when using  
winId() and re-opened  
* QTBUG-79012 [regression 5.9.8 - > 5.11.x] QWidget loosing content when  
using winId() in embedded QWidget  
* QTBUG-71519 Inconsistent handling of "close" w/QWindows  
* QTBUG-96734 QDoubleSpinBox asserts in validate with default properties  
* QTBUG-85574 No focus on window after showing and hiding a modal dialog  
* QTBUG-97241 Qt no longer compiles when configured with -trace  
* QTBUG-97146 QRhiMetal asserts when a given sampleCount is not  
supported by a device  
* QTBUG-96789 Shader cache not able to write out compiled shaders  
* QTBUG-97098 Documentation: building sql drivers following the  
instructions in the docs fails with "CMake Error: Unknown argument  
--build"  
* QTBUG-96267 ...QtQml/private/qqmljsparser_p.h contains full path to  
build dir  
* QTBUG-94352 QTabBar's SelectionBehavior QTabBar::SelectPreviousTab  
does not work as expected  
* QTBUG-97179 Assertion failure inside of QNetworkAccessManager thread  
* QTBUG-92958 Blinking scrollbar with QScrollArea and edge cases.  
* QTBUG-97109 Use of uninitialized value in qfilesystemengine_unix.cpp  
* QTBUG-8857 Qt::WA_ShowWithoutActivating causes a situation where a  
QLineEdit cursor is blinking but not active  
* QTBUG-93955 Material.System does not work on Ubuntu (Gnome)  
* QTBUG-97122 Regression: UTF-32 codec fails on assert when  
fromUnicode() is called  
* QTBUG-97425 Build from sources fails in Qt 6.2.0 with MSVC 2019 in  
c++20 mode  
* QTBUG-84310 CMake: qt_lib_XXX.pri files don't contain run_depends  
entries  
* QTBUG-255 QTableWidget setSpan + selectedRanges  
* QTBUG-97409 QNetworkInformation::TransportMedium enum undocumented  
* QTBUG-89640 font.styleName depends on font loading order  
* QTBUG-94979 Misleading example for QPoint[F]::dotProduct()  
* QTBUG-97441 Doc: generated lists show only the first word of the  
\brief statement  
* QTBUG-97384 [REG 5.15.2-6.2.0] "Flow control error" while loading web  
image  
* QTBUG-96128 Compile error when adding QList::const_iterator and  
std::ptrdiff_t  
* QTBUG-96603 QTextDocument: stylesheet border-color for td applied only  
to first td  
* QTBUG-96861 Geoflickr example dstStep assert crash on mac and iOS  
* QTBUG-79081 Nested foreach generate warnings  
* QTBUG-97095 Mouse clicks are not delivered to the QWidget beneath  
container QWidget in QOpenGLWIndow on Windows  
* QTBUG-94769 QComboBoxListView display misalignment after sliding  
* QTBUG-91391 androiddeployqt uses deprecated ndk.dir property  
* QTBUG-60257 [XCB]: QXcbClipboard: SelectionRequest too old messages  
can appear  
* QTBUG-96869 GTK file dialog is invisible if there is QTimer with 0  
interval in the main thread  
* QTBUG-97475 Crash in QItemSelectionModel  
* QTBUG-97486 Crash in TimeZone ICU backend  
* QTBUG-96560 Android: Keyboard does not show up again if it has been  
closed with back button in some devices  
* QTBUG-97443 Crash - DpiAdjustmentPolicy resolved from wrong  
environment  
* QTBUG-97491 Android: in TextField: cannot edit inside of words, only  
at the end  
* QTBUG-97133 Cannot configure qtbase for Android  
* QTBUG-97116 OpenSSL TLS plugin is not loaded for OpenSSLv3  
* QTBUG-96870 qt_internal_generate_tool_command_wrapper might fail to  
generate wrapper script due to unrelated configuration failure  
* QTBUG-96558 RTA CMake test fails on macOS10.15 and macOS11.0  
* QTBUG-97478 Configuring CMake based application with QtQuick fails  
* QTBUG-95609 cmake names for qml plugins  
* QTBUG-97099 [cmake] dependent qml plugins not auto-loaded with  
statically linked qt  
* QTBUG-96114 [Reg : 5.12.4 -> ] ActiveX widget not rendering on  
secondary screen when System-DPI Aware is combined with high DPI scaling  
* QTBUG-46620 QMainWindow:restoreState doesnt restore width of  
QDockWidgets in maximized QMainWindow  
* QTBUG-97493 Change of QDateTimeEdit::setDateTime not documented in  
"Changes to Qt Modules in Qt 6"  
* QTBUG-57347 [macOS] button doesn't click when having preedit string in  
line edit and text edit  
* QTBUG-91222 Markdown parser improperly handles certain HTML payloads  
* QTBUG-94245 Markdown unexpected render result  
* QTBUG-89101 QPainter::fillRect broken with QBrush containing DPR > 1  
pixmap  
* QTBUG-96327 qt5.15 examples on qnx710 display "is an invalid ELF  
object (shstrtab section header seems to be at 0)“  
* QTBUG-88529 wrong symbol is getting deleted  when tap on clear button  
* QTBUG-94768 Qt::Tool window has no title bar  
* QTBUG-96240 Views are not blurred  
* QTBUG-97054 QSqlDatabase.open() warning  
* QTBUG-86533 Yocto and QNX builds are missing -rpath-link linker flag  
which causes non-prefix builds to fail  
* QTBUG-97629 Building qtbase for Android with examples fails to  
configure  
* QTBUG-85997 QDir::mkpath() does not return true for existing drive  
* QTBUG-97110 QDir::mkpath() fails on MACOS given the root path  
* QTBUG-96256 Cannot declare MetaType for a QHash/QMultiHash with key  
type without custom operator==  
* QTBUG-97532 Mention how to properly deploy and use TLS plugins  
* QTBUG-97489 [REG 6.2 -> 6.3.0] QDateTime::fromString slow at handling  
large input  
* QTBUG-7768 fontMetrics.boundingRect() and drawText(boundingRect)  
disagree about text width metrics  
* QTBUG-70184 QFontMetrics::tightBoundingRect doesn’t return correct  
width somtimes  
* QTBUG-85936 TextMetrics.width does not always give a correct width for  
the given text and is sometimes too short depending on the font used  
* QTBUG-94023 TextMetrics width is not same as Text.implicitWidth  
* QTBUG-83733 Don't use deprecated/removed functions and structs with  
OpenSSL v3  
* QTBUG-97009 Broken rendering on Qt 6.2 Android arm64-v8a  
* QTBUG-79565 Mac: Emoji Picker shortcut (Ctrl + Cmd + Space) doesn't  
work in QML TextEdit  
* QTBUG-97673 Update dependencies in qt/qtshadertools fails  
* QTBUG-93810 warnings due to enums in QSize  
* QTBUG-97451 QString(QByteArray) constructor behavior change between  
Qt5 and Qt6  
* QTBUG-96124 QListview automatic scrolling should consider when the  
item is not selected  
* QTBUG-97002 Building for android fail  
* QTBUG-97713 [Reg 6.1->6.2] Unexpected value for QKeyEvent::key() if  
Ctrl+letter is pressed  
* QTBUG-97246 Qt fails to compile with both tracing and QT_NAMESPACE  
enabled  
* QTBUG-94806 Having Qmltypes in CONFIG leads to faulty vcxproj file  
* QTBUG-25743 QAction triggered in QMenu within QMenuBar even though the  
QMenu's menuAction is hidden/disabled.  
* QTBUG-90990 Drop down widget get left behind if dialog window is moved  
* QTBUG-6905 font-weight: bold can truncate tab label  
* QTBUG-8209 QTabBar: Tab size incorrect when using bold font in a style  
sheet  
* QTBUG-94918 QWidget::show triggers windows activation  
* QTBUG-97269 Antialiasing is disabled when the painter's antialiasing  
attribute is set behind the clipping funcion.  
* QTBUG-97727 Tree Model Completer Example: tree model is broken due to  
bugs in MainWindow::modelFromFile  
* QTBUG-96458 Make it possible to build newer Qt modules against older  
Qt  
* QTBUG-94481 [REG 5.15.2 -> 6.1.1] Ellipsis in the worst possible place  
* QTBUG-93671 Undefined reference to WinMain with MinGW  
* QTBUG-96178 [wasm] Cursor shape does not work  
* QTBUG-97811 QScrollArea performance regression  
* QTBUG-97599 Internal Qt builds prefer target Tools packages over host  
packages  
* QTBUG-95099 [FTBFS] Qt6CoreToolsTargets.cmake not found with  
-DQT_FORCE_FIND_TOOLS=ON  
* QTBUG-97831 Fix "does not include QT_BEGIN_NAMESPACE" CMake warnings  
* QTBUG-97257 QVideoWidget not showing after minimizing  
* QTBUG-97896 Qt CMake packages should not create targets if  
dependencies are not met  
* QTBUG-97908 Regression: PageUp and PageDown don't work in QScrollArea.  
* QTBUG-90352 Page Up/Page Down do not work in QTextBrowser  
* QTBUG-97738 Crash on Nvidia with GLES  
* QTBUG-97919 include could not find requested file:  C:/Users/qt/work/q  
t/qt5/qtbase/lib/cmake/Qt6EntryPointPrivate/Qt6EntryPointMinGW32Target.c  
make  
* QTBUG-81842 Puzzle example looses pieces  
* QTBUG-97945 assert in qnsview_mouse.mm  
* QTBUG-97457 Highlighted example quick3d/morphing not compiling on  
Wasm, "wasm-ld: error: initial memory too small, 17835968 bytes needed"  
* QTBUG-97941 Plugin parsing/loading issues under clang build (with  
ASan)  
* QTBUG-97729 Please suppress the annoying logo message from rc.exe  
* QTBUG-97853 Tablewidget_cellClicked not working after opening Dialog  
with cellDoubleClicked  
* QTBUG-94028 Cursor not displayed at right margin of QPlainTextEdit  
* QTBUG-97698 Mac: QHeaderView ignores vertical alignment  
* QTBUG-97984 HttpStatusCodeAttribute gives 0 in case of success  
* QTBUG-83503 wasm: dialogs wrong size when opened  
* QTBUG-58053 Impossible to run a QProcess with an empty environment  
* QTBUG-93412 Problem with drawing progressbar as QTreeView delegate  
* QTBUG-98087 top-level in-source build detected as prefix build  
pointing to build dir and removes moc upon install  
* QTBUG-98088 [Regression, macOS] quit() before exec() quits instantly.  
* QTBUG-98026 Nested QGraphicsViews do not clip some items when printing  
* QTBUG-97747 [REG: 5->6] QDomDocument::setContent now requires  
QIODevice to be open  
* QTBUG-93438 Android unit tests capture C++ logs, not Java logs  
* QTBUG-97937 QPushButton does not emit signal released() when releasing  
the button outside of the button  
* QTBUG-98085 qthreadstorage.h fails to compile with namespaces enabled  
* QTBUG-97382 qt.conf not reladed properly after  
QCoreApplication::instance()  
* QTBUG-97383 [REG 5.15 -> 6.2] QtWebEngineProcess + change resources  
location with qt.conf  
* QTBUG-97947 [REG 5.15 -> 6.2] QtWebEngine resources + translations  
location no longer affected by qt.conf  
* QTBUG-91545 [iOS] Selection in TextEdit not working for Readonly text  
* QTBUG-97774 Win32: Window contents flicker a lot when resizing  
* QTBUG-59401 QFileDialog::setDefaultSuffix doesn't work when file path  
contains a dot  
* QTBUG-98265 QMultiHash::operator== is broken  
* QTBUG-98247 qobject_cast pointer conversion crashed  
* QTBUG-26269 QScrollArea: The viewport bleeds through another widget  
when the scroll bar is reset.  
* QTBUG-96069 Qt 6.2.0 Beta3 runtime link error when run  
multimediawidgets sample on android arm  
* QTBUG-98099 Crash on exit with Application font and QFontComboBox  
* QTBUG-98277 QT_TRID_N_NOOP is missing  
* QTBUG-3945 QT_TRANSLATE_NOOP does not cover plurals  
* QTBUG-98377 QImage::reinterpretAsFormat wrong reference counting when  
out of memory  
* QTBUG-98093 QSlider is broken in MacOS Monterey  
* QTBUG-97995 Error deserializing QFont (from 5.15 to 6.2)  
* QTBUG-98138 QAnyStringView argument doesn't accept QStringBuilder  
* QTBUG-98403 tst_QPainter fails with macOS 12 x86 in developer build  
tests  
* QTBUG-98388 Vertical QPainter::drawLine() result on QWidget is skewed  
* QTBUG-98335 qt.conf still expects entries called "Qml2Imports" rather  
than "QmlImports"  
* QTBUG-97490 Static Build is unable to find QPrinter::NativeFormat  
* QTBUG-98137 Disabled button in QDialogButtonBox gets focus by Tab  
* QTBUG-59433 Qt5 no longer shows window list in macOS dock  
* QTBUG-98480 qhashseed is flaky in QtBase with Windows 11  
* QTBUG-98280 QAuthenticator doesn't check if algorithm is supported  
* QTBUG-98286 Reg->Qt 6: QToolButton with style sheet : There are two  
Tool button arrows rendered  (all styles)  
* QTBUG-95933 Using scanner input IRcode will result in an error when  
second character is uppercase  
* QTBUG-94036 tst_QAccessibilityMac::notificationsTest() fails  
* QTBUG-96405 setGraphicsApi :OpenGLRhi.  QML application resizing  
flickers and is sometimes blank  
* QTBUG-55458 Q_GADGET should not require the whole class to be exported  
* QTBUG-98544 Combination of 'HangulInputMethod' and 'QGraphicsTextItem'  
does not work as expected.  
* QTBUG-97431 WASM - Tumbler does not work good/at all  
* QTBUG-33908 With the PMF connect syntax, slots are invoked on  
partially destroyed objects  
* QTBUG-82455 QTextDocument::contentsChange(int,int,int) values are  
incompatible with QTextCursor  
* QTBUG-98289 QTableView : The last column/row is hidden by scrollbar  
when stylesheet is used.  
* QTBUG-98372 Regression Qt5 > Qt6: Visible gaps between selected lines  
* QTBUG-98726 CMake code for locating latest android.jar in Android SDK  
is incorrect  
* QTBUG-98770 QList<T>::count(const T&) triggers undefined behavior  
sanitizer when list is empty  
* QTBUG-97833 Elf.h not found when compiling a test case on QNX CI  
* QTBUG-96710 CMake isn't exposing an aab target for Android projects  
* QTBUG-98493 Using copy-restricted class in lambda for QFuture's  
then(), does not build  
* QTBUG-92521 WASM: QToolTips occasionally makes app exception  
* QTBUG-98803 Applications are upside-down in WebAssembly  
* QTBUG-91691 [REG: 5.15.0->5.15.1] QTextDocument tables with colspan  
collapses the starting column to minimum size  
* QTBUG-95240 QTextTabel: column width changes when merging other rows  
* QTBUG-86633 QML - letters randomly disappear when resizing label  
* QTBUG-92037 QMdiArea  setActiveSubWindow sublist.at(0) failed if  
setViewMode(QMdiArea::TabbedView);  
* QTBUG-96880 New line is ignored with Osaka font  
* QTBUG-97699 Building projects with static Qt (debug):  
qrc_openglblacklists.cpp.obj : warning LNK4099: PDB 'vc140.pdb' was not  
found with 'qrc_openglblacklists.cpp.obj'  
* QTBUG-62602 Underline is displayed outside the text box  
* QTBUG-86671 Table cells overlap with image and relative width  
* QTBUG-97463 Showing Large image in QTextBrowser table overlaps  
* QTBUG-98444 QTableView, Deselecting column by [ctrl + click] on  
horizontal header only works when the first row is visible  
* QTBUG-98532 CMake - _qmltyperegistration.cpp do not get updated  
* QTBUG-83165 Android .aab bundle fails to link static library in subdir  
* QTBUG-48815 QTextEdit: When pressing enter at the end of last item in  
an ordered list...  
* QTBUG-97459 when hitting enter in QTextEdit at the end of a line with  
a checked checkbox, next line is also checked  
* QTBUG-80473 Inserting an <HR> tag into QTextDocument does Bad Things  
* QTBUG-86372 [xcb] WindowTransparentForInput causing problems with  
resizing  
* QTBUG-98578 Documentation of qabstractnativeeventfilter  
* QTBUG-98752 QFontDatabase::addApplicationFontFromData does not mention  
OpenType being supported  
* QTBUG-97649 androiddeployqt exits with signing if the path contains  
spaces  
* QTBUG-98504 QSystemTrayIcon example: selecting Quit from context menu  
shows unnecessary message  
* QTBUG-98762 REGRESSION: QPalette::setBrush does not reliably detach  
* QTBUG-65475 Application palette changes at runtime do not work for all  
widgets  
* QTBUG-98654 QX11Application: No such file  
* QTBUG-98875 QMouseEvent source() vs pointingDevice() unclear in  
documentation  
* QTBUG-86052 wasm: Calling setWindowIcon() has no effect on a QDialog  
* QTBUG-72776 QKeyEvent key() only returns value of first surrogate for  
characters in Supplementary Planes  
* QTBUG-58995 [REG 5.7->5.8][Windows]: When using Courier with a large  
pixel size then it will show up as 13 points regardless  
* PYSIDE-1720 piside6-uic convert signal clicked(bool) to clicked  
* QTBUG-95192 Segmentation fault at application closing  
* QTBUG-74504 wasm: clipboard use not working as expected on chrome  
* QTBUG-93619 Clipboard does not work in WASM build of Qt application  
* QTBUG-79365 Webassembly: rich text paste not supported  
* QTBUG-86169 Web Assembly Copy Paste Enhancements  
* QTBUG-93976 QStorageInfo delivers -1 for blockSize() under Windows 10  
* QTBUG-80653 Keyboard LED states do not change with evdev keyboard  
* QTBUG-68636 Some popups (i.e.) menus are misplaced on gnome-shell  
* QTBUG-98856 Wrong cursor showing when restoreOverrideCursor in  
QDockWidget  
* QTBUG-95096 Qt 6's new and improved QList fails its removeAll  
benchmarks  
* QTBUG-94995 Changed QML files do not updated on device  
* QTBUG-99039 QVarLengthArray::push_back() is not strongly exception-  
safe  
* QTBUG-99036 [REG 5.15 → 6.3] QList(It, It) no longer works with pure  
input_iterators  
* QTBUG-97818 Huge line spacing when font is Monaco  
* QTBUG-98961 abstractitemview drag item can not autoscroll  
* QTBUG-92501 QtFuture::connect includes Q*::QPrivateSignal as one of  
the arguments  
* QTBUG-98843 Qt 6.2.2 Windows build fail  
* QTBUG-99165 cmake doesn't complain with android-30, but fails with  
unknown API S (ie android-31)  
* QTBUG-98408 QTextDocument is limited to `@media screen`when calling  
setHtml()  
* QTBUG-99223 CMake Error: File  
C:/Users/qt/work/install/lib/cmake/Qt6/qt_setup_tool_path.bat.in does  
not exist.  
* QTBUG-97752 QHash: non-readonly iteration access destroys iterator  
* QTBUG-96463 [REG 5.15.2-6.2.0] Text with BIDI controls is underlined  
incorrectly  
* QTBUG-96916 Qt 6 breaks compatibility of QVariant streaming into  
QDataStream  
* QTBUG-81503 qtbase contains code that isn't allowed to be distributed  
* QTBUG-99163 QTransform rotate big image will crash  
* QTBUG-99280 Splash screen appears on top model dialog with dynamic vs  
behind with static  
* QTBUG-99330 qdoc: Crash at QString::operator+=()  
* QTBUG-99186 uncaught exeption takes down app  
* QTBUG-99319 QApplication crash on second run when mouse roll over  
window  
* QTBUG-99371 QWidget::customContextMenuRequested coordinates are off  
for widgets in a QMenu  
* QTBUG-99147 <!---->  
* QTBUG-99413 QSysInfo::productType() incorrectly documented  
* COIN-777 *** Could not find any device matching '--platform iOS  
--minimum-deployment-target  
* QTBUG-98901 QtConcurrent::run crashes on program exit  
* QTBUG-63695 QStandardPaths does not document locations for QNX  
* QTBUG-99316 Yocto build fails in CI for qtdeclarative-native dev/6.3  
branch  
* QTBUG-99416 QT6 qtbase build fails claiming symlinks are present  
* QTBUG-99192 tst_qquickpixmapcache Failed  
* QTBUG-97841 MacOS Monterey - scrolling issues with touch pad  
* QTBUG-99623 Dependency update on qt/qtopcua failed in 6.3  
* QTBUG-99633 [autotests] tst_QIcoImageFormat should be behind a feature  
flag  
* QTBUG-99548 Qt6 CMake target compile options propagation (CUDA)  
* QTBUG-99522 qmake adds @ mark after then the output file name when it  
calls g++ on either Qt's MinGW or MSYS2 platform  
* QTBUG-99111 wasm: cursor is wrong after resizing window  
* QTBUG-99605 XCB: QGuiApplication::primaryScreen() always last screen  
* QTBUG-99676 markdown (and html) import/export should not rely on use  
of a fixed-pitched font to remember a `monospace` span  
* QTBUG-92445 Markdown smashes nested formatting inside lists  
* QTBUG-99148 Broken html list rendering because <code> element  
* QTBUG-99408 [SQL] The SQL driver for Firebird/Interbase does not  
unpack the QVariant before null check  
* QTBUG-98471 [REG: 5->6.2.1] Null QDateTime is not stored as NULL  
anymore in Oracle OCI  
* QTBUG-99710 Regression: QCache crash  
* QTBUG-99224 Crash in QPixmapCache  
* QTBUG-99240 Crashing in trimming QPixmapCache  
* QTBUG-99656 [REG] QT_HOST_BINS, QT_HOST_LIBEXECS and QT_HOST_LIBS have  
extra 'bin' in path  
* QTBUG-99620 QMetaType: type QMap<int,QFlags<Qt::AlignmentFlag>> has  
more than one typedef alias: ColumnAlignmentMap, ColumnAlignmentMap  
* QTBUG-99743 QTabWidget rendering broken on macOS 12  
* QTBUG-99717 [autotests] text reading in tst_QImageReader should be  
behind a feature flag  
* PYSIDE-1773 uic doesn't import QAbstractItemView for  
QTableView/QTreeView EditTriggers  
* PYSIDE-1404 Incompatible import of "Object" in compiled UI  
* QTBUG-99668 Using QDateTime with QTimeZone specified asserts in debug  
build  
* QTBUG-99630 tst_QShortcut::text is flaky in dev  
* QTBUG-99771 Porting guide does not mention binary JSON  
* QTBUG-92358 One More Crash in text shaping on special string with  
EmojiOneColor font.  
* QTBUG-89155 Assertion violation in text shaping on special string with  
EmojiOneColor font.  
* QTBUG-99642 Can't define CSS with properties for QToolButton with Qt 6  
* QTBUG-99615 Most QMutableEventPoint usage depends on Undefined  
Behaviour  
* QTBUG-72103 Conversion between QQuaternion and Euler angles has issues  
in special cases  
* QTBUG-97535 Bug in examples for QListIterator Class  
* QTBUG-99486 Extra dot appears in top left corner of Fusion style spin  
box frames with no buttons  
* QTBUG-80666 QNetworkRequest::setHeader(IfModifiedSince) treats local  
time as UTC  
* QTBUG-99666 Qt module builds mix install and staging prefixes  
* QTBUG-99799 Memory leak in QJsonDocument::fromJson()  
* QTBUG-99960 A crash when comparing two null QVariants  
* QTBUG-99323 [REG: 5.14.2 -> 5.15.0] Posted events get stuck when  
QCoreApplication::processEvents with QEventLoop::WaitForMoreEvents is  
used  
* QTBUG-99472 "Pick Screen Color" button in QColorDialog doesn't scan  
secondary screen colors in Windows  
* QTBUG-100026 [REG 6.2  -> 6.3] Crash in QSslCertificate  
* QTBUG-96718 Crash in inBindingWrapper() (Creator built against Qt 6.2  
build)  
* QTBUG-97950 Application slowly reads every file in /usr/bin before  
starting  
* QTBUG-99534 tst_qfuture memleaks  
* QTBUG-100067 network/torrent examples ProgressBar text should be  
layout with horizontal  
* QTBUG-95309 Compile fails with Qt in namespace and C++20  
* QTBUG-100118 QStaticByteArrayMatcher cannot match beyond INT_MAX  
* QTBUG-100072 Building Qt from source fails to compile with C++20  
standard enabled when using MSVC 2022  
* QTBUG-99949 Cannot do unthrottled Present with D3D  
* QTBUG-91739 Performance regression on QHash::insert() and  
QHash::remove()  
* QTBUG-100144 Dependency update on qt/qtwebchannel failed in dev  
* QTBUG-100233 Android broken project/wrong libraries linked when adding  
UiTools  
* QTBUG-100074 Building QSharedMemory fails when bootstrapping  
* QTBUG-87136 Animations run twice as fast on a 120hz Android device  
* QTBUG-93823 Android QPlatformScreen does not expose the refresh rate:  
Animations (and timers) too fast on higher refresh rate monitors  
* QTBUG-94959 Timer and animations runs faster after screen touch event  
on Android 11  
* QTBUG-93393 Android A11Y TalkBack: Hidden onPressAction still called  
* QTBUG-100294 RHI Direct3D11 fails to build with MinGW-w64 v8  
* QTBUG-100315 FEATURE_headersclean does not work with if  
CMAKE_CXX_FLAGS contains more than one option  
* QTBUG-100071 QtFuture::connect fails to compile if the passed signal  
takes a std::tuple as argument  
* QTBUG-95842 testlib's autotest compilation fails with glibc 2.34  
* QTBUG-99637 Windows with D3D or Vulkan: stretch effect is not ideal  
when resizing QQuickWindow  
* QTBUG-100416 QPluginLoader::loadHints return "no hints set" but by  
default PreventUnloadHint is set  
* QTBUG-97929 CMake warnings in FindGLIB2.cmake  
* QTBUG-100324 QHelpEvent::globalPos() returns frequently a wrong value.  
* QTBUG-93432 QGraphicsTextItem font gets incorrectly clipped when a  
clip rect is set on the painter.  
* QTBUG-99846 [autotests] tst_qlogging uses wrong helper path on webOS  
* QTBUG-98253 Failed to build from source through clang-cl 13.0.0  
* QTBUG-99707 QML plugins have wrong RUNPATH  
* QTBUG-100432 [REG 6.2.3->6.3.0] QML/quick examples  not launching when  
compiled from command line  
* QTBUG-97157 attempting to interact with any widget dialog on  
touchscreen fails; mouse causes crash after that  
* QTBUG-99954 [autotests] tst_QResourceEngine fails on webOS  
* QTBUG-94608 Nonsensical full path to examples  
* QTBUG-100317 QMacStyle code references missing image resource  
* QTBUG-100290 Custom build fails with PCH  
* QTBUG-100327 CompositionMode_Screen wrong with drawImage  
* QTBUG-100493 QtFinishPrlFile.cmake: No such file or directory with  
multi-config build on Linux  
* QTBUG-100482 Network monitoring not working when ZScaler Internet  
Security is active  
* QTBUG-100441 [REG 6.2.1->6.3.0] Designer not launching on macOS x64  
* QTBUG-100364 QStandardPaths GenericDataLocation for iOS seems to  
mention wrong path  
* QTBUG-100518 Crash on iOS 13.3.1  
* QTBUG-100362  
tst_QNetworkReply::putWithServerClosingConnectionImmediately is flaky  
* QTBUG-63196 QNetworkReply::putWithServerClosingConnectionImmediately  
fails on Windows  
* QTBUG-98476  
tst_QNetworkReply::putWithServerClosingConnectionImmediately fails in  
QtBase with Windows 11  
* QTBUG-78797 Shift-select drag distance is zero in QTreeView  
* QTBUG-81542 QListView range selection changes after 1 pixel move  
* QTBUG-99512 QListview  selectcount  error with items of differing  
sizes  
* QTBUG-100420 QPicture doesn't respect Qt::IntersectClip when used with  
setClipPath  
* QTBUG-93402 Android A11Y TalkBack: Focus Rect not updated on  
orientation Change  
* QTBUG-100654 tst_QRhi fails on webOS  
* QTBUG-100695 Document QProcessEnvironment::Initialization enum  
* QTBUG-100438 Incorrect rounding to ms in QTimer when clock too coarse  
* QTBUG-51327 [Windows 8.1]: After maximizing a window and toggling the  
frameless window hint and moving to another monitor then the window can  
be too big  
* QTBUG-100545 Nested QML items with Accessible properties set does not  
work on Android  
* QTBUG-100217 [REG 6.2.2  -> 6.2.3] Integer overflow when rendering svg  
image  
* QTBUG-88136 tst_QFutureWatcher fails on Android  
* QTBUG-100775 Several data races around handlers of  
QDesktopServices::openUrl()  
* QTBUG-100546 QIODevice::readAll() Truncates Data To Max Int  
* QTBUG-100867 QFile::copy error string is uninformative  
* QTBUG-87400 tst_QAbstractItemView fails on Android  
* QTBUG-87408 tst_QTreeView has failing tests  
* QTBUG-100574 qtbase/src/gui/vulkan/qvulkanfunctions_p.cpp is missing  
dependency on qvkgen tool  
* QTBUG-100261 QPrinter property setup not effect  
* QTBUG-99504 Linux: QPrinter::setDuplex not effective ( Canon  
imageRUNNER 2520  )  
* QTBUG-100915 moc code generates warning [-Wredundant-parens]  
* QTBUG-100651 Unable to follow HTTP/2 redirects  
* QTBUG-88137 tst_QTimeLine fails on Android  
* QTBUG-87405 tst_QFontDatabase::systemFixedFont fails for Android  
* QTBUG-52472 Undefined Behaviour in qsimpledrag.cpp line 207  
* QTBUG-45045 SIGFPE in QQuickMenu  
* QTBUG-100693 WebAssembly (WASM) MEMORY control fixes  
* QTBUG-100559 wasm: Linking commands too long for Windows  
* QTBUG-100796 qt_internal_add_test calls don't handle extra properties  
for Android  
* QTBUG-101172 Android help from configure-cmake-mapping.md seems  
outdated (or wrong)?  
* QTBUG-84466 startSystemMove and startSystemResize does not enable aero  
snap on windows with frameless window.  
* QTBUG-87674 qaccessibility fails on Android  
* QTBUG-101020 tst_QPlugin::scanInvalidPlugin fails on QNX  
* QTBUG-87401 tst_QFormLayout::wrapping fails on Android  
* QTBUG-100802 [REG 6.2.2->6.2.3]Checkable QPushButton does not visually  
display checked state when toggled on macOS  
* QTBUG-100037 QSqlQuery: crash on executing query if connection is  
already closed  
* QTBUG-101297 REG->6.3: Default-constructed QPrintPreviewDialog asserts  
"!(P(max) < P(min))"  
* QTBUG-101302 [REG 6.2.3 -> 6.3.0] QGuiApplication leaks memory  
* QTBUG-100299 Android: Unloaded multimedia plugins  
* QTBUG-100537 Can not build Qt 6 with cmake when preferring package  
configuration  
* QTBUG-101306 enum-enum warning in qxcbwindow.cpp is genuiune  
* QTBUG-69064 Android: tst_QFrame::testPainting fails  
* QTBUG-87389 tst_QDialog::snapToDefaultButton fails on Android  
* QTBUG-101299 QCOMPARE() doesn't compile for certain QFlags<T> with  
QT_TYPESAFE_FLAGS  
* QTBUG-101300 QFlags: Missing some bitwise xor operators with  
QT_TYPESAFE_FLAGS  
* QTBUG-101294 tst_qflags doesn't compile with QT_TYPESAFE_FLAGS  
* QTBUG-95957 Scaled pixmap with ellipse clipping leaves lines in output  
* QTBUG-100329 Clipping glitches when painting with fractional scaling  
* QTBUG-100343 MDI subwindows leave artifacts when moving/resizing with  
fractional scaling  
* QTBUG-101399 QTest::toString() doesn't compile for certain QFlags<T>  
with QT_TYPESAFE_FLAGS  
* QTBUG-100795 QWeakPointer d pointer is private  
* QTBUG-101028 argv passed to Android apps is not sufficiently  
terminated  
* QTBUG-93505 Unable to retrieve the swiped Filedialog  
* QTBUG-101286 [Regression] QNetworkReply::finished() is not emitted if  
an error occurs.  
* QTBUG-101411 QT_WARNING_DISABLE_* macros do not work under QCC (8.3.0)  
* QTBUG-101381 QtScxml: Fix compiler warnings for QNX  
* QTBUG-101415 QtPositioning: Fix compiler warnings for QNX  
* QTBUG-101384 QtRO: Fix compiler warnings for QNX  
* QTBUG-101382 QtBase: Fix compiler warnings for QNX  
* QTBUG-101304 Compile tst_qflags both with and w/o QT_TYPESAFE_FLAGS  
* QTBUG-28379 QFileDialog: aliases to folders disabled  
* QTBUG-101551 wasm multiple "use after free" in  
QNetworkReplyWasmImplPrivate::doSendRequest  
* QTBUG-100154 deprecated-declarations warning in  
examples/network/secureudpserver/server.cpp  
* QTBUG-67576 QAbstractSocket::setSocketOption() has no effect if called  
before QAbstractSocket::connectToHost()  
* QTBUG-101581 Crash when zooming invalid image  
* QTBUG-101609 Font "Bahnschrift" reports wrong style names  
* QTBUG-101610 Font "Alef" reports wrong style names and renders  
incorrectly  
* QTBUG-100790 tst_QInputDevice::multiSeatDevices() fails on Wayland  
* QTBUG-98755 QIconEngine::IconNameHook disappeared  
* QTBUG-101013 QQuickFileDialog does not work on Android  
* QTBUG-95067 WASM: Quick Window is bigger than browser frame on mobile  
browsers  
* QTBUG-100562 The characters ("_") in qtdbus-index.html links to  
qromancalendar.html  
* QTBUG-100873 REG->6.3b1/Windows with system clock offset: Assert when  
instantiating QDateTimeEdit  
* QTBUG-94366 Backslash is converted to double forward slash in  
configure on Windows  
* QTBUG-101592 Qt should load libvulkan.so.1, not libvulkan.so  
* QTBUG-93499 Signal parameter MOC handling error with gcc 10  
* QTBUG-100770 Old Qt version mentioned in Qt6.3.0 qtbase documentation  
* QTBUG-101620 QOpenGLWidget does not update when content changed while  
its hidden  
* QTBUG-101474 setClipRect() after setClipRegion() call doesn't change  
clipping region  
* QTBUG-87407 tst_QTableView has failing tests for Android  
* QTCREATORBUG-24600 some clicks in call stack don't register  
* QTBUG-99640 Reg->6: QByteArray::append(const char *str, qsizetype len)  
crashes if len < 0  
* QTBUG-100107 QByteArray::isLower() is completely different from  
QString::isLower() , ditto isUpper()  
* QTBUG-98369 [macOS] Qt internal warning when FontMetrics is used  
* QTBUG-99216 QMessageBox with Japanese characters gives "Missing font  
family" warning on macOS  
* QTBUG-101745 Running qmake on iOS build fails on macOS 12.3 Monterey  
* QTBUG-89545 CMake: on macOS (w/ framework build) the module includes  
the binary  
* QTBUG-101718 [REG 6.3.0beta2->beta3] quick3d/principledmaterial not  
launching on macOS  
* QTBUG-101775 Don't add framework directories as include paths  
* QTBUG-101651 Random crashes in QGraphicsScene  
* QTBUG-101897 The 'movie' example should only build if  
'QT_FEATURE_movie' is available  
* QTBUG-101916 Build Qt 6.3.0 beta2 / beta3 for Android fails only on  
Windows  
* COIN-689 Android test VMs lack locales  
* QTBUG-93752 When setting the inactive colorgroup in the palette and  
then making the window inactive it will not trigger an update on any  
colors bound to the palette  
* QTBUG-87263 QMap<QVariant, QVariant> compilation error  
* QTBUG-94059 Stop using mixed enum arithmetic  
* QTBUG-60822 [REG: 4->5] WA_TranslucentBackground cannot be changed  
after widget has been shown  
* QTBUG-59126 clear WA_TranslucentBackground  
* QTBUG-87775 Passing INTERNAL_MODULE to qt_internal_add_module should  
only create a single Qt::FooPrivate target  
* QTBUG-94450 tst_QString::setRawData() indicates problems with Qt 6's  
reworking of raw data handling  
* QTBUG-91077 startSystemMove/startSystemResize causing mouse events to  
be lost on X11(MATE)  
* QTBUG-93002 CMake: linker error with Linux Static Libraries while  
using QtQuick.Controls  
* QTBUG-88248 QObject orphaned connections soft-leak  
* QTBUG-87774 QToolBar::clear() leaks memory  
* QTBUG-88081 Failed to build Qt from source through clang-cl  
* QTBUG-88434 Qt6 Beta4 fails to compile with Clang - SIMD issues  
* QTBUG-92941 REG 5->6: QVector size() does not reach capacity() before  
reallocating  
* QTBUG-89536 Remove configure.json files for building Qt 6  
* QTBUG-93360 Compile Qt with gcc 11  
* QTBUG-94250 tst_QListView::internalDragDropMove fails with OpenSUSE  
15.3  
* QTBUG-94613 [FTFBS] qttools does not compile: QtTools/private/qttools-  
config_p.h: No such file or directory  
* QTBUG-94753 QtFlagHandlingHelpers.cmake overrides flags -On from the  
user  
* QTBUG-94355 Revice changes in configure summary options, 6.1.1 ->  
6.2.0  
* QTBUG-85201 Deprecate Ministro in Qt for Android  
* QTBUG-94971 QHoverEvent::scenePosition() is actually local position  
* QTBUG-91713 QtBase benchmarks fail for qtimezone, qdiriterator, and  
qfile  
* QTBUG-95004 XCB: Qt packages are built without session management  
support  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
* QTBUG-94546 QTreeModel::index changes model despite being const  
* QTBUG-94463 QThreadPool creates one thread more than maxThreadCount  
* QTBUG-88090 Installed CMake files reference the SOURCE TREE  
* QTBUG-95136 QLocalServer provides no way to know how to clean up if  
its listen() fails  
* QTBUG-95199 Incorrect propagation of iOS bitcode and -fapplication-  
extension flags to user projects  
* QTBUG-95208 Linker error regarding bitcode when linking CMake app  
targeting iOS  
* QTBUG-88448 QtConcurrent filter/map does not work with reductor object  
* QTBUG-95268 test_QT_TESTCASE_BUILDDIR fails when built with CMake 3.21  
* QTBUG-95303 Internal module pri files are missing public include  
header locations  
* QTBUG-85839 Documentation: wrong default value for Layout Direction  
* QTBUG-80957 QFutureInterface: reportResults with an empty vector  
breaks results  
* QTBUG-63363 QPointingDevices for the trackpad and mouse are  
dynamically instantiated on macOS  
* QTBUG-95394 Crash in RHI when exiting a QtWaylandCompositor with  
active clients.  
* QTBUG-70137 Dockwidgets - Placing QDockWidget is almost impossible  
* QTBUG-53706 QString::number(-17, 16) should return "-11" not  
"0xffffffffffffffef"  
* QTBUG-94831 Crash on MSVC in ~QMetaTypeFunctionRegistry() on program  
end with dynamically loaded Qt  
* QTBUG-95314 WASM: Diverging timezones in C++/QML  
* QTBUG-95532 Can't build qtquickcalendar due to missing SQL dependency  
* QTBUG-58749 QListView AdjustToContents not working  
* QTBUG-95072 Menu is shown at displaced position on enable/disable  
* QTBUG-55444 Documentation doesn't explain that login and password  
provided to MySQL plugin (QSqlDatabase::setUserName and  
QSqlDatabase::setPassword) must be in latin1 encoding  
* QTBUG-95453 Mouse move pointer does not reflect when drag will move -  
eglfs  
* QTBUG-71590 Qt is using "Non-SDK" interfaces, will be blocked by  
Android  
* QTBUG-79102 Scrolling via trackpad does not when a widget is inside a  
QScrollArea  
* QTBUG-67032 Mouse Wheel event gets propagated even when event filter  
should stop it  
* QTBUG-87580 Add minimal set of tests to build for static Qt configs in  
Coin  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-95845 qt_add_qml_module unconditionally installs metatypes.json  
files into "arbitrary" directory  
* QTBUG-93340 trafficlight_qml_dynamic crashes on Android device  
* QTBUG-95969 module "QtMultimedia" plugin "qtmultimediaplugin" not  
found  
* QTBUG-89122 Building Qt with cmake needs 15% more space than with  
qmake  
* QTBUG-80863 [cmake] excessive compilation of Import.cpp files for  
static plugins  
* QTBUG-95668 Webengine widget not visible in Designer UI  
* QTBUG-95921 scxml examples fail to build for iOS target  
* QTBUG-89296 No way to specify C standard for Visual Studio 2019 in  
qmake project  
* QTBUG-35700 single punctuation input via CJK input method doesn't work  
* QTBUG-88308 [REG v6.0.0-beta3 -> dev] configure tries to use ccache  
when it is not installed  
* QTBUG-39125 Cocoa: When typing in a Korean character and then press  
enter, it will take two presses before the enter key is actually invoked  
* QTBUG-95661 Test result counts are incorrect  
* QTBUG-94451 Switch Android target SDK to 30 for Qt 6.2  
* QTBUG-96121 Versionless CMake commands prevent setting variables in  
calling scope  
* QTBUG-88535 List of modules in configure output is incomplete  
* QTBUG-87646 WheelHandler doesn't work correctly with TouchPad  
* QTBUG-96219 Conversion of versionless wrapper functions to macros  
needs to be reverted  
* QTCREATORBUG-26168 No run targets for examples  
* QTBUG-84877 QLocale::system() uses short names of days and months for  
narrow formats  
* QTBUG-80347 Forward headers are not generated for deprecated classes  
* QTBUG-89141 QStatusBar without a parent crashes XFCE4 toolbars  
* QTBUG-95200 qt6_add_qml_module only works when used in same folder  
than the backing library  
* QTBUG-95670 PSK doesn't work when both the client and server use TLS  
1.3  
* QTBUG-30040 tst_qtooltip::task183679 is unstable in Mac CI  
* QTBUG-94714 Qt's CMake seems to ignore dependencies when generating  
APK targets  
* QTBUG-96127 Broken external links in Qt docs  
* QTBUG-96303 Review (again) CodeChecker issues for Qt Core  
* QTBUG-55523 Windows: Application does not quit if tooltip was visible  
when last window was closed  
* QTBUG-96290 qmlimportscanner: "qmldir file not found at" when  
configuring quickwidget example with static Qt  
* QTBUG-77833 Mac: context menu not closed when minimizing window  
* QTBUG-82626 Cmd-H Doesn't Hide App When Tooltip Displayed  
* QTBUG-58727 [macOS]: Command+H with Qt::Popup window open leads to  
inconsistent internal state  
* QTBUG-94770 [Qt Virtual keyboard] Keyboards doesn't respond when  
QT_SCALE_FACTOR  is set to 1.5  
* QTBUG-96253 Unable to build qtscxml tests after building with  
components with Conan  
* QTBUG-95249 OpenSSL TLS backend plugin missing in macOS installation  
from official binary  
* QTBUG-95832 QtRemoteObjects CMake API is using the internal  
qt_manual_moc API  
* QTBUG-90719 QDoubleValidator unexpected behaviour using different  
locale  
* QTBUG-96441  [REG 6.1.0 - 6.2.0] Windows: QWindow doesn't respect  
minimumWidth/minimumHeight  
* QTBUG-96786 QPainter::drawRect fills OpenGL window background when  
pen's alpha != 1.0  
* QTBUG-96790 crash in QWindowsFileSystemWatcherEngine::addPaths  
* QTBUG-46882 REG [5.4.2-5.5.0] Floating QDockWidget cannot be resized  
* QTBUG-64994 CLONE - frameless window can't minimize or maximize on mac  
* QTBUG-85084 Skip executing unnecessary commands when building tools  
during cross-compilation  
* QTBUG-80766 Android app installed from Google  Play store crashes  
* QTBUG-94344 High CPU load in WASM threaded application  
* QTBUG-73117 QTableView is very laggy on scroll  
* QTBUG-96654 REG[5.15-6.1]QTreeView crash when checkbox triggers reset  
* QTBUG-97028 \relates documentation should mention how it interacts  
with templated classes  
* QTBUG-96057 Bluetooth crash when connectToPairedDevice on windows  
* QTBUG-95285 Create documentation page for Qt for Android Manifest  
* QTBUG-96239 Document CMake component in CMake function documentation  
* QTBUG-96575 Merge "DTLS Client"and "DTLS Server" examples  
* QTBUG-83939 QGenericUnixServices::openDocument /  
xdgDesktopPortalOpenFile uses wrong fd mode, breaking snaps  
* QTBUG-26424 fix disabled test cases of tst_qwidget  
* QTBUG-97076 QT3D fails to compile on macos when system assimp is  
installed  
* QTBUG-95763 Configuring an executable with an attached qml module  
fails when using the Xcode generator  
* QTBUG-58013 Cursor position changes not properly passed to input  
method  
* QTBUG-93414 Qt Quick application stuck in a cursor update loop  
* QTBUG-95669 Clicking enter on some text fields it might freeze UI  
* QTBUG-96671 Android: Keyboard sometimes stuck and replacing previous  
letter  
* QTBUG-96675 Android: Cursor is shown in wrong place  
* QTBUG-96769 Android: keyboard input can get lost  
* QTBUG-74606 floating QDockWidget with native child widget fails to  
show() after closing it  
* QTBUG-74342 QML RichText hr element doesn't work  
* QTBUG-97247 Fix docs for comparison and debug/data stream operators of  
Qt containers  
* QTBUG-96257 Cannot declare MetaType for a recursive QSet with deleted  
operator==  
* QTBUG-97601 Compilation speed decrease with Qt 6.2 compared to Qt  
5.15.2  
* QTBUG-96399 Crash with SIGSEGV in QXcbConnection::getSelectionOwner  
* QTBUG-97656 The article explaining bindable properties is not linked  
in other related parts of the docs  
* QTBUG-95300 [Regression] TextField goes behind soft keyboard on  
android  
* QTBUG-96117 Android soft keyboard no longer pans the screen  
* QTBUG-97503 Reg[5.15.2-5.15.6] Android: Keyboard covers the inputfield  
* QTBUG-72110 MouseArea stops responding  
* QTBUG-74872 Qt/QMake includes the deprecated 'CFBundleGetInfoString'  
key into the Info.plist on macOS  
* QTBUG-96898 Sub-project created with qt_add_qml_module doesn't work on  
Android  
* QTBUG-94530 Disconnecting HDMI output causes application to crash  
* QTBUG-97903 Sporadic crash on QPMCache::flushDetachedPixmaps  
* QTBUG-91445 Crash in QPixmapCache::setCacheLimit in Windows  
* QTCREATORBUG-26473 Crash inside pixmap cache while RMB inside cpp  
editor  
* QTBUG-97715 Quick3D examples fail on imx6  
* QTBUG-96975 Qurl fails with MSVC 2022 target in windows 10 & 11  
* QTBUG-97808 QOperatingSystemVersion: Adding new const entries in patch  
releases breaks our BC guarantees  
* QTBUG-97582 QFuture::cancel through then()/onCanceled/onFailed  
* QTCREATORBUG-26581 Multicursor mode enables during the selection  
without pressing "Alt"  
* QTBUG-84234 Start new QCoreApplication after shutdown  
* QTBUG-97842 Move Android tools docs from qtdoc to qtbase  
* QTBUG-97115 When an application that is using a background service is  
closed then it will cause an ANR after hanging for about 30 seconds  
* QTBUG-98650 Drop Qt 3/4 support  
* QTBUG-98653 QStringView::split returns invalid data  
* QTBUG-98569 Error in meta-b2qt for Windows Toolchain  
* QTBUG-98642 Qml/QmlScene : malformed http request when opening a qml  
file over http with qml/qmlscene  
* QTBUG-93037 Conan builds are unable to run tst_qmake  
* QTBUG-98649 Qt Android creates View IDs in a way potentially leading  
to a collision  
* QTBUG-92231 SSL handshake failure after ignoreSslErrors  
* QTBUG-75862 FocusReason is broken in Controls 2  
* QTBUG-96957 Created output file is in inncorrect type and in different  
location  
* QTBUG-98151 Widgets over a QMdiArea are not repainted correctly  
* QTBUG-92249 quick3d examples crashes or hangs on exit on wayland  
* QTBUG-59096 tst_qqmlsettings.cpp(415): error C2065: 'boldFont':  
undeclared identifier  
* QTBUG-98561 Creating directory using symbolic link in path fails on  
QNX  
* QTBUG-98466 Misleading error messages when using macdeployqt on  
AppleSilicon Macs  
* QTBUG-89285 Document changes to State Machine Framework in Core  
Migration Guide  
* QTCREATORBUG-25594 Code model gets confused by qLastIndexOf in  
qstring.cpp  
* QTBUG-95237 [REG 6.0.4 -> 6.1.0] Integer-overflow in  
QFixed::operator+= through QImage::loadFromData(QByteArray)  
* QTBUG-45582 Duplicated vtables due to inline virtual functions  
(probably all dtors)  
* QTBUG-98483 [macOS] QPushButton is broken in macOS Monterey  
* QTBUG-98937 KTX, ASTC image not displayed on Qt 6.2 and above  
* QTBUG-99009 QCursor::setPos X coordinates is wrong when DPI scaling is  
used  
* QTBUG-81917 QtWidgets fails to build with clang 10.0-rc1 in C++20 mode  
* QTBUG-81583 QTextMarkdownWriter: if a task list item's first line ends  
with monospace text, trailing backtick is omitted  
* QTBUG-99368 TLS handshake fails due to incorrect cipher handling  
(Secure Transport macOS backend)  
* QTBUG-99775 Crash on QObject::objectName access when using QThreadPool  
from non-owning thread  
* QTBUG-20531 QLineEdit with a QCompleter: popup completion is drawn on  
the wrong location  
* QTBUG-92909 When following redirects, a PROPFIND request (and probably  
others) are converted to a GET  
* QTBUG-97844 Logitech mice and touchpads that send lots of events with  
small angleDelta cause overreaction  
* QTBUG-99803 QVulkanWindow doesn't enable any device features (e.g.  
VkDeviceCreateInfo::pEnabledFeatures)  
* COIN-762 Coin's configure command gets warning about unused  
-DBUILD_EXAMPLES=OFF  
* QTBUG-99506 Loader with states and children loaders crashes on  
Integrity (release only)  
* QTBUG-95764 pure virtual call in QAccessibleQuickItem  
* QTBUG-99747 QDate::startOfDay( ) leads to assert in debug build  
* QTBUG-98475 tst_QWindow::modalWindowEnterEventOnHide fails in QtBase  
with Windows 11  
* QTBUG-98478 tst_QFileSystemWatcher::signalsEmittedAfterFileMoved fails  
in QtBase with Windows 11  
* QTBUG-100412 tst_qsrceen::grabWindow is flaky on Windows  
* QTBUG-99491 Windows - Android App, cmake build does not update  
correctly if app library is bigger than 2GB  
* QTBUG-62185 QVersionNumber seems broken on -O1 and higher with g++  
* QTBUG-93396 Android A11Y TalkBack: Slider does not announce value on  
change  
* QTBUG-100401 QToolbutton with popupMode QToolButton::InstantPopup and  
stylesheet have 2 arrows  
* QTBUG-100792 tst_QScreen::grabWindow() fails on Wayland  
* QTBUG-100891  
tst_QGuiApplication::genericPluginsAndWindowSystemEvents() fails on  
Wayland  
* QTBUG-66818 tst_QWindow::initialSize fails on Wayland  
* QTBUG-100887 tst_QWindow::mouseToTouchTranslation() fails on Wayland  
* QTBUG-100888 tst_QWindow::modalWindowPosition() fails on Wayland  
* QTBUG-100889 tst_QWindow::requestUpdate() fails on Wayland  
* QTBUG-100929 tst_QImage::hugeQImage fails on platforms without  
adequate memory  
* QTBUG-100930 tst_QGraphicsWidget::updateFocusChainWhenChildDie fails  
on QNX  
* QTBUG-98489 tst_QTabBar::hoverTab fails in QtBase with Windows 11 and  
MSVC2022  
* QTBUG-87154 Add static dependencies from 3rdparty in qtbase  
* QTBUG-99295 The tool "Qt6::sdpscanner" was not found  
* QTBUG-87671 Android tests crashing with  
"java.lang.UnsatisfiedLinkError: dlopen failed: invalid ELF file"  
* QTBUG-87397 tst_QGraphicsView fails on Android  
* QTBUG-101049 /permissive- not passed causes compiling errors  
* QTBUG-101328 FAIL!  : tst_QLockFile::lockUnlock in QNX_710  
* QTBUG-101332 FAIL!  : tst_QXmlStream::initTestCase in QNX_710  
* QTBUG-87424 tst_QMenu fails on Android  
* QTBUG-101321 tst_QDialog::dialogInGraphicsView crashes on Android  
* QTBUG-100948 tst_QFontDatabase::systemFixedFont() fails on QNX  
* QTBUG-87396 tst_toolsupport::offsets fails on Android  
* QTBUG-94459 Android reports incorrect screen size after rotation  
* QTBUG-100917 tst_QImageReader::setScaledClipRect() SVG/SVGZ fails on  
Wayland  
* QTBUG-100918 tst_QOpenGL::bufferMapRange() fails on Wayland  
* QTBUG-100982 tst_QStaticText fails on Wayland  
* QTBUG-101519 FAIL!  :  
tst_QTouchEvent::multiPointRawEventTranslationOnTouchPad in  
Windows_11_21H2  
* QTBUG-101406 Add QT_TYPESAFE_FLAGS to headerclean and fix fallout  
* QTBUG-101567 FAIL!  : tst_QWindow::spuriousMouseMove in  
Windows_11_21H2  
* QTBUG-101618 FAIL!  : tst_QSystemSemaphore::initialValue in QNX_710  
* QTBUG-101436 Font selection via styleName broken on Windows  
* QTBUG-89402 tst_QPlainTextEdit fails test cases on Android  
* QTBUG-99948 Fix enum/enum arithmetic in Qt  
* QTBUG-100470 Undetected test crashes on Android  
* QTBUG-101194 tst_QFileDialog has failing tests for Android  
  
### qtsvg  
* QTBUG-94878 QSvgRenderer crash  
* QTBUG-92184 QtSVG cannot understand minified SVGs if they contain arcs  
* QTBUG-97421 text x,y positions are always parsed as pixels  
* QTBUG-97422 font-size is always parsed as pixels  
* QTBUG-96044 High memory consumption when rendering svg image  
* QTBUG-95891 svg file freezes QImage  
* QTBUG-98139 QSvgRenderer::boundsOnElement does not properly calculate  
the bounding box of a text when it has a transformation  
* QTBUG-99407 [REG 6.1.3  -> 6.2.0] Loading svg file takes too long  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-99642 Can't define CSS with properties for QToolButton with Qt 6  
  
### qtdeclarative  
* QTBUG-82146 doubleClicked() not emitted for Button on touch devices  
* QTBUG-94360 QmlRegisterType object's signal slot connections crashes  
when giving more than 2 argguments with signal.  
* QTBUG-94455 tst_QQuickFileDialogImpl::defaults() leaks memory  
* QTBUG-93652 qmllint: Missing support for inline components  
* QTBUG-93752 When setting the inactive colorgroup in the palette and  
then making the window inactive it will not trigger an update on any  
colors bound to the palette  
* QTBUG-94456 Alias properties incorrectly allow duplicating property  
names  
* QTBUG-91390 ListModel doesn't keep objects of JavaScriptOwnership  
alive  
* QTBUG-91365 Can't set palette for Window  
* QTBUG-93489 Not obvious how to generate key events for QML when using  
QQuickRenderControl  
* QTBUG-64128 When dragging an item that is the parent of the DropArea  
then it will call onEntered for that DropArea  
* QTBUG-94533 Update dependencies on '6.2' in qt/qtquickcontrols2 fails  
* QTBUG-55705 SwipeDelegate is not swiping inside SwipeView  
* QTBUG-94519 Install rules for .qml files should use source dir as  
their source, not build dir copies  
* QTBUG-94520 Install destinations for .qml files do not account for  
resource paths  
* QTBUG-94553 Update dependencies on '6.2' in qt/qtquickcontrols2 fails  
* QTBUG-94559 Update dependencies on '6.2' in qt/qtquickcontrols2 fails  
* QTBUG-94502 Crash on Android caused by automatic type conversion  
between JS array and QVariantList (SIGBUS)  
* QTBUG-86755 no required property support in tools  
* QTBUG-94307 ComboBox: without a validator bindings to acceptableInput  
don't work  
* QTBUG-94575 Update dependencies on 'dev' in qt/qtqc2 fails  
* QTBUG-94576 Debug output flooded with "detected interleaved frame-sync  
and actual events"  
* QTBUG-92824 QtQuick.Controls Button.qml wrong parent used for  
transitionDuration (line 77)  
* QTBUG-94223 Regression[5.14->5.15] 'model' is no longer an implicit  
data role in delegates in Custom delegate  
* QTBUG-92840 FolderListModel docs have gone missing  
* QTBUG-93041 If Button is used as delegate of ListView then application  
fails  
* QTBUG-94833 Wayland compositor crash when client window closes  
* QTBUG-94703 REG: Binding to var properties that are undefined is  
broken in 6.2.0  
* QTBUG-55958 QQuickItem::contains return true even for points outside  
the item rect  
* QTBUG-89376 QQuickItem API that involves item-at/bounds checks doesn't  
respect containmentMask  
* QTBUG-34882 Multiple hovers are incorrect when children are outside  
parent  
* QTBUG-63670 Disabled MouseArea stealing hover events  
* QTBUG-94970 tst_QQuickFileDialogImpl crashes  
* QTBUG-92563 Extra, incorrect HoverMove sent after MouseButtonRelease  
* QTBUG-95070 PinchHandler doesn't filter by number of fingers when  
receiving QNativeGestureEvents  
* QTBUG-56075 QML Flickable: high-precision trackpad scrolling is too  
fast  
* QTBUG-75239 When the locale is changed then it should be propagated to  
the the controls in the ApplicationWindow, but Label and TextField are  
not seen as controls  
* QTBUG-95073 TextEdit inconsistency with some key events (modifiers)  
* QTBUG-75553 QML Canvas, reset line dash failed  
* QTBUG-77528 Conflicting includes from 3rdparty/masm/stubs/wtf and icu  
* QTBUG-89375 No C++ documentation for containmentMask  
* QTBUG-72843 HoverHandler is unreliable  
* QTBUG-95162 Qt config with some modules disabled causes compile error  
(Qt 6.2.0 beta1)  
* QTBUG-94622 svg Image is  Pixelated when windows is scaled  
* QTBUG-95139 Using backticks for ListElement value results in "cannot  
use script for property value"  
* QTBUG-90456 Array manipulation destroys objects in array  
* QTBUG-81037 Array.concat does not verify length against allocated  
space  
* QTBUG-95365 QML module files copied to build dir have nothing  
depending on them  
* QTBUG-95132 Memory Leak when using QQuickPaintedItem with RHI  
* QTBUG-95417 Regression 5.15.4: gc() within generator functions crash  
* QTBUG-95532 Can't build qtquickcalendar due to missing SQL dependency  
* QTBUG-95562 Warnings about deprecated usage  
* QTBUG-94021 groupBoxPadding not defined for GroupBox on MacOS  
* QTBUG-95095 Inline QML component can't use named import of JavaScript  
module from enclosing scope  
* QTBUG-95622 SelectionRectangle: selection is removed when dragging on  
the bottom-right handle  
* QTBUG-91165 QtQuick compiler and QML States/AnchorChanges at loading  
prevents component to be displayed  
* QTBUG-95575 Build fails with clang-cl 12.0.0  
* QTBUG-95314 WASM: Diverging timezones in C++/QML  
* QTBUG-95629 SelectionRectangle: Long press on top of a handle clears  
the current selection  
* QTBUG-95591 QtQuick documentation references private class  
"QQuickColorGroup"  
* QTBUG-94964 Create QtQuick.Dialogs module overview page  
* QTBUG-95656 qmllint does not handle implicit import correctly  
* QTBUG-95544 Regression: buttons invisible when using non-sized custom  
backgrounds  
* QTBUG-94558 The handle hovered state of RangeSlider is wrong when  
first and second overlapped  
* QTBUG-95811 KeyNavigation: all properties should be marked as attached  
* QTBUG-95393 QQuickView::grab segfaults at times  
* QTBUG-95259 After closing modal menu, non-modal menus can't be  
dismissed by clicking  
* QTBUG-95825 Live preview not starting  
* QTBUG-85591 qmlProtectModule() claims it "allows the engine to skip  
checking for a plugin when that uri is imported", but that might not be  
true  
* QTBUG-95659 Assertion error by accessing this from onSignal arrow  
function  
* QTBUG-95593 Customised SpinBox buttons don't work with macOS style  
* QTBUG-89409 Unable to scroll listview by dragging / swiping if header  
is used  
* QTBUG-92844 qmllint should warn about assigning to readonly property  
* QTBUG-95937 Native windows style is incompatible with QQuickWidget or  
other means of offscreen rendering  
* QTBUG-95461 QQuickTextInput doesn't manage pre-edit text correctly  
* QTBUG-95944 ButtonGroup.buttons is not a default property as it claims  
to be  
* QTBUG-95895 REG 5.15 -> 6.2: destroy() does not destroy objects after  
appending listModel.  
* QTBUG-95373 Component is missing required property index from here  
* QDS-4390 Live preview crashes at shutdown  
* QTBUG-96126 Compositor crashes when client is closed  
* QTBUG-96118 FTBFS top-level: The "moc" executable  
"BUÏLDDIR/qtbase/libexec/moc" does not exist.  
* QTBUG-96167 Ownership of C++ owned object flips when added to  
ListModel  
* QTBUG-96150 QML best practices docs are outdated  
* QTBUG-96159 Qt5.git integration fails in '6.2':  The "moc" executable  
"/Users/qt/work/qt/qt5/qtbase/libexec/moc" does not exist  
* QTBUG-96190 Rendering glitches when resizing window containing  
QQuickPaintedItem  
* QTBUG-96099 Drag and Drop example crashes on KDE Plasma  
* QTBUG-88414 CMake multi-config build still build some debug tools  
* QTBUG-93050 Memory leak in qiconhelper.cpp when loading icon by name  
* QTBUG-91350 [REG 5.15->6.0] TapHandler.onTapped: device and button are  
no longer available  
* QTBUG-64847 TapHandler does not tell us which button was tapped (and  
this breaks the manual test)  
* QTBUG-96301 qmldir files generated by CMake do not respect .ui.qml  
suffix  
* QTBUG-95589 Customizing checkbox does not fully work when using  
example from documentation  
* QTBUG-87402 Error when using ShaderEffect doesn't tell the user how to  
fix it  
* QTBUG-96130 srbCache exhibits unreasonable, semi-continuous growth  
with dynamic scenes  
* QTBUG-91109 Inconsistent behaviour of TextArea with horizontalCenter  
between different platforms (Gallery example)  
* QTBUG-65853 QML ScrollBar Quick Controls 2 - policy:  
ScrollBar.AsNeeded not working when scrollbar is customized  
* QTBUG-96290 qmlimportscanner: "qmldir file not found at" when  
configuring quickwidget example with static Qt  
* QTBUG-96275 Crash while loading QML type data from disk cache  
* QTBUG-96405 setGraphicsApi :OpenGLRhi.  QML application resizing  
flickers and is sometimes blank  
* QTBUG-96147 qmlsc does not understand curly braced grouped properties  
* QTBUG-96587 qmlsc ignores return type of CallPropertyLookup  
* QTBUG-96343 inheritance cycle not detected correctly  
* QTBUG-96200 Only the first Q_PROPERTY marked as REQUIRED is required  
in reality  
* QTBUG-96551 Crash while processing a shortcut key  
* QTBUG-96561 MenuItem does not clear shortcuts from GUI kernel  
* QTBUG-96902 Import of JS module to QML does not work  
* QTBUG-96358 ShaderTools package not found when building qtdeclarative  
examples in-tree in a prefix build (not as ExternalProjects)  
* QTBUG-96909 ListView/Flickable: when releasing multitouch, list stays  
in dragging state  
* QTBUG-96625 Unable to declare variable with identifier equal to  
function name inside getter  
* QTBUG-86744 ListView.isCurrentItem not available until model is  
refreshed  
* QTBUG-96805 quick examples not compiling on Wasm: CMake Error at  
.../wasm_32/lib/cmake/Qt6/QtPublicPluginHelpers.cmake  
* QTBUG-92841 Offscreen Surfaces should not receive input events in 3D  
scenes  
* QTBUG-96668 [Reg 6.1 -> 6.2] Cannot overwrite property bindings in  
aliased elements  
* QTBUG-97099 [cmake] dependent qml plugins not auto-loaded with  
statically linked qt  
* QTBUG-96192 Performance concerns for a qmlengine->retranslate() call  
* QTBUG-96876 Error initializing PageIndicator with Material style  
* QTBUG-94975 [ASAN] Heap-use-after-free in QOpenGLFramebufferObject  
* QTBUG-93642 list<QtObject> appends new elements when redefined in  
component instances  
* QTBUG-96112 Text tearing on text element when set inside parent  
element with noninteger y value  
* QTBUG-83626 When a Popup has an odd number for the width and/or height  
then texts inside it can be rendered badly  
* QTBUG-55638 garbled font after scrolling with mouse wheel  
* QTBUG-97467 [REG 6.2.0->6.2.1] cmake test fails on RHEL  
* QTBUG-90869 tst_qquickdesignersupport: tests segfault when running on  
QEMU and Windows MinGW developer build  
* QTBUG-94253 When an inputmask is set on a TextInput then it will  
overwrite the first character if the cursor starts from position 0 after  
typing the second character  
* QTBUG-96966 Using stackView.pop(StackView.Immediate) after  
stackView.push(item, StackView.Transition) causes Item to be placed  
unexpectedly  
* QTBUG-61496 StackView: pop() with StackView.Immediate leads to blank  
StackView  
* QTBUG-74342 QML RichText hr element doesn't work  
* QTBUG-81306 qml Markdown format not working as expected  
* QTBUG-85956 QQuickPopupPrivate::finalizeExitTransition() not giving  
focus to the highest-z Dialog with focus = true  
* QTBUG-85918 Focus set to wrong dialog in case of enter transition  
* QTBUG-96929 ToolTip: Make it clearer that ESC is a shortcut used by  
the default closePolicy  
* QTBUG-86854 When a Tooltip is visible then it is possible to interact  
with a window that is underneath a modal dialog although it should be  
blocking the input to it  
* QTBUG-97480 ParentChange crash  
* QTBUG-58416 QtQuick Image: SVG Images are not properly scaled with  
High DPI Scaling  
* QTBUG-81018 Image sourceSize binding causes the size to become smaller  
unexpectedly  
* QTBUG-97605 tst_qqmlmoduleplugin::incorrectPluginCase() Received a  
fatal error.  
* QTBUG-74335 QML RichText table border is misaligned  
* QTBUG-97600 qmllint segfaults on Connections  
* QTBUG-97462 Qt Quick "Text editor" example uses deprecated code  
* QTBUG-84269 StackView doesn't work with required properties  
* QTBUG-93988 Regression 5.15.1->5.15.2 : Loader's item width is not set  
even when its status is Loader.Ready  
* QTBUG-97466 quick/pointerhandlers example fails to configure  
* QTBUG-97465 [REG 6.2.0->6.2.1] quickcontrols2/texteditor not compiling  
on Wasm  
* QTBUG-91706 QML: Subclassing a QQuickItem that has revisioned  
properties fails  
* QTBUG-86202 DelegateChooser stopped working with enums in QVariants  
* QTBUG-97488 [REG 5.15.2->6.2] DelegateChooser not finding choice  
* QTBUG-96898 Sub-project created with qt_add_qml_module doesn't work on  
Android  
* QTBUG-96458 Make it possible to build newer Qt modules against older  
Qt  
* QTBUG-96934 QQuickFontDialogImpl: update listview indexes when calling  
setCurrentFont()  
* QTBUG-85936 TextMetrics.width does not always give a correct width for  
the given text and is sometimes too short depending on the font used  
* QTBUG-94023 TextMetrics width is not same as Text.implicitWidth  
* QTBUG-96796 qmlcache causes loading problem if the qml filename  
matches the name of some qml file from Qt package and has inline  
component  
* QTBUG-73633 QML FileDialog sort names by capitalised name first  
* QTBUG-97859 QQuickWindow::tabletEvent() broken in Qt 6.2.1  
* QTBUG-98015 qml tool fails to build when targeting iOS  
* QTBUG-98058 Static Qt plugins not always linked into Qt apps in a top-  
level build  
* QTBUG-98109 Update dependencies on '6.2' in qt/qtdeclarative fails  
* QTBUG-98115 qmllint crashes when id is assigned to string  
* QTBUG-98125 qmllint crashes when there is an animation on a grouped  
property  
* QTBUG-98032 QML/Javascript: Using an anonymous function as a default  
parameter in a function signature crashes the application.  
* QTBUG-98150 Designer puppet keeps crashing at startup in batch  
renderer  
* QDS-5481 Animation looping is not properly set when it is in component  
* QTBUG-91886 Inconsistence in material style checked highlighted button  
* QTBUG-86453 Instantiator creates delegates when active is false if  
items are dynamically added to a ListModel  
* QTBUG-88331 Instantiator creates delegate when active is false and  
delegate is updated  
* QTBUG-98356 JIT crash on invalid yield syntax  
* QTBUG-97927 Focus frame placed in the wrong position after window  
resize  
* QTBUG-97914 Broken test tst_QQuickListView2::dragDelegateWithMouseArea  
* QTBUG-98140 TextInput with cursorDelegate and clipping: custom cursor  
gets clipped  
* QTBUG-35646 Setting clip property true on TextInput hides cursor on an  
empty input.  
* QTBUG-98440 TableView selectionModel property is not available in  
Quick 2.2  
* QTBUG-98248 SEGFAULT Crash in QQmlAnimationTimer::registerAnimation  
* QTBUG-98541 qmlsc generates bad code when comparing numbers to  
undefined  
* QTBUG-93358 qmllint: Add support for UiArrayBindings  
* QTBUG-95633 QQmlEngine::offlineStoragePath() documentation needs link  
to openDatabase()  
* QTBUG-98311 QML bitwise 'or' operator is not evaluated correctly when  
initializing C++ property and both operands are enum values  
* QTBUG-59223 tst_qqmlxmlhttprequest::send_options fails with  
LANG=de_DE.UTF-8  
* QTBUG-97782 Material SpinBox QML TypeErrors  
* QTBUG-98299 qmllint debug code cause qmllint skip problems  
* QTBUG-98017 QSGRhiTextureGlyphCache::createEmptyTexture() nullptr  
access crash  
* QTBUG-98727 tst_DragHandler::touchDragMultiSliders is flaky / failing  
on macOS  
* QTBUG-37364 Missing documentation for QQuickItem's boundingRect(),  
clipRect()  
* QTBUG-60491 When TextEdit show the file more than 1mb, the soft will  
use many memory  
* QTBUG-65741 Invalid event clipping  
* QTBUG-98742 qt6_target_qml_sources() doesn't ensure PREFIX argument  
starts with "/"  
* QTBUG-98439 "Binding on contentItem is not deferred as requested by  
the DeferredPropertyNames class info because it constitutes a group  
property" when instantiating ScrollBar  
* QTBUG-98792 Crash when using as-cast  
* QTBUG-84196 Crash when calling QQmlEngine::retranslate  
* QTBUG-98482 RangeSlider does not update position/visualPosition based  
on from/to changes  
* QTBUG-97461 [REG 5.15.2->6.2] DragHandler does not work when there's a  
Drawer in the application  
* QTBUG-98811 FAIL!  :  
tst_qqmlxmlhttprequest::setRequestHeader_illegalName(Referer) Received a  
fatal error.  
* QTBUG-82263 [REG: 5.13->5.14]: QML DropArea wrong signals order  
* QTBUG-97541 qt_add_qml_module does not properly handle singleton qml  
files  
* QTBUG-98830 qmlsc confuses precedence between properties and IDs  
* QTBUG-98717 Setting HoverHandler cursorShape in a Window crashes  
* QTBUG-92998 Items in GridView shifts to the right when using RTL  
layoutDirection  
* QTBUG-75862 FocusReason is broken in Controls 2  
* QTBUG-71723 When showing a context menu for a TextField then it will  
lose the selection instead of keeping it  
* QTBUG-36332 QtQuick Controls: actions which depend on activeFocusItem  
are disabled when a menu is shown  
* QTBUG-98468 CMake Error: AUTOMOC for target affectors_shared: The  
"moc" executable "/Users/qt/work/qt/qt5/qtbase/libexec/moc" does not  
exist  
* QTBUG-91479 When a TextField is inside a QQuickWidget that is in a  
QGraphicsProxyWidget then clicking the TextField will not give it focus  
and as such it is not possible to type in it  
* QTBUG-98924 Cannot assign binding of type Button to QQuickItem  
* QTBUG-98127 Weighted layout behavior is not documented  
* QTBUG-98960 warning C4573: the usage of 'QJSNumberCoercion::toInteger'  
requires the compiler to capture 'this'  
* QTBUG-98730 Slider with negative width crash the application  
* QTBUG-99027 qmllint crashes in a combination with ListModel  
* QTBUG-99025 Property "hasOwnProperty" not found on type "Item"  
* QTBUG-94765 AnimatedSprite has glitches  
* QTBUG-98747 close.accepted behavior  
* QTBUG-84730 Allow to reassign PointerHandler.parent  
* QTBUG-98367 Segmentation fault with Binding on font.bold  
* QTBUG-99113 qmlsc confuses ambiguous types in the same module  
* QTBUG-99043 The -i option to qmlcachegen, qmllint, qmlsc, etc. is  
wrong  
* QTBUG-75799 Strange flickering when restarting an animation with  
PauseAnimation and ScaleAnimator  
* QTBUG-99192 tst_qquickpixmapcache Failed  
* QTBUG-98937 KTX, ASTC image not displayed on Qt 6.2 and above  
* QTBUG-99229 "ninja: error: 'qrc_files-NOTFOUND', needed by  
'.qt_plugins/Qt6_QmlPlugins_Imports_untitled4.cmake', missing and no  
known rule to make it" when building "Qt Quick Application - Empty"  
project  
* QTBUG-99286  FAILED: src/quickcontrols2/material/impl/.rcc/qmlcache/qt  
quickcontrols2materialstyleimplplugin_RectangularGlow_qml.cpp  
* QTBUG-99275 agent:2021/12/16 18:36:00 build.go:394: FAILED:  
tests/auto/quickcontrols2/controls/basic/tst_basic  
* QTBUG-86533 Yocto and QNX builds are missing -rpath-link linker flag  
which causes non-prefix builds to fail  
* QTBUG-96888 Not possible to quickly click buttons  
* QTBUG-49049 arcTo doesn't always get drawn  
* QTBUG-99529 Touchpad scrolling list overshoot is buggy  
* QTBUG-99400 [Reg 5.2 -> 5.3] qmlplugindump: error details missing on  
linux  
* QTBUG-99477 Crash in QRhiD3D11::executeCommandBuffer with nullptr  
access  
* QTBUG-99644 invalid access of indicator item inside switch type  
destructor  
* QTBUG-98116 Clean up qtdeclarative doc warnings and enable  
documentation testing in CI  
* QTBUG-99888 configure fails when only qtdeclarative and qtbase are  
checked out  
* QTBUG-94848 Missing element in drawer when used with ListView and  
Section  
* QTBUG-99128 qmlsc does not see property revisions  
* QTBUG-100046 FAIL!  : tst_qquickborderimage::borderImageMesh()  
* QTBUG-99273 QtDeclarative fails to configure when Python is not in  
PATH but is found via FindPython  
* QTBUG-100110 switch handle goes out of bounds when size is increased  
(flatstyle example)  
* QTBUG-99608 tst_qmlcachegen (Failed)  
* QTBUG-100089 REG: QQuickDial with the Imagine style is displaying the  
handle at an incorrect position  
* QTBUG-99974 qt.labs.qmlmodels classes documented twice  
* QTBUG-99311 QtQuick Window does not expose enum of visibility property  
of Window  
* QTBUG-100314 qmltc tests fail to compile with older CMake  
* QTBUG-99124 Properly document ScrollBar in ScrollView  
* QTBUG-100326 *.mjs files not added to qmldir when added to  
qt_add_qml_module()  
* QTBUG-98039 QML javascript: "this" in class ctor becomes undefined  
during if(){...} in arrow functions  
* QTBUG-100366 tst_qmlcachegen tests using generateCache are valid only  
for host  
* QTBUG-100221 qtdeclarative compilation fails on arm64  
* QTBUG-100279 Building fails on Linux ARM64  
* QTBUG-100377 [REG 5.15 -> 6.2] Date.parse() can't handle some dates on  
Qt 6 but works in Qt 5  
* QTBUG-100260 Crash on access after using QML singleton as a model  
* QTBUG-97185 Quick DragHandler Reporting Wrong Coordinates using  
TouchScreen Input  
* QTBUG-98486 Touch points coordinates does not take into account the  
Device Pixel Ratio on Windows  
* QTBUG-98543 Invalid updates of contentY of Flickable on touch screen  
* QTBUG-95033 ButtonGroup does not work with Windows style Button  
* QTBUG-100480 QtQuick compiler generates bad code for "!=" operator  
* QTBUG-99547 PathView item does not appear in certain circumstance  
* QTBUG-51078 Use of Item obligatory in SwipeView?  
* QTBUG-51669 QQC2: SwipeView is not working as expected  
* QTBUG-100469 Qml runtime resizeToItem configuration is not working  
* QTBUG-94161 "QTransform::translate with NaN called" when hovering over  
window containing Imagine style GroupBox containing a TextEdit  
* QTBUG-86695 [REG: 5.12 -> 5.14] Broken State::when behavior after  
suspicious change  
* QTBUG-95763 Configuring an executable with an attached qml module  
fails when using the Xcode generator  
* QTBUG-100380 valueAt(int index) method of ComboBox QML type (QQC2) is  
undocumented  
* QTBUG-100680 TableView: positionViewAtRow will in some cases move the  
viewport too far  
* QTBUG-100855 qmljs tool doesn't link on iOS build  
* QTBUG-100947 Infinity not usable in QML  
* QTBUG-95587 icon.source of Control is not resolved relative to user  
code  
* QTBUG-101011 qmlsc goes into infinite loop  
* QTBUG-100978 A completely valid qml file with a block comment can  
result in a qmlcache compilation error  
* QTBUG-100980 Q_UNREACHABLE triggered in qmlcachegen  
* QTBUG-100883 qmlcachegen miscompiles QVariant of QObject* to bool  
conversion  
* QTBUG-100338 qmllint warns about all members of model index  
* QTBUG-101074 Assert in qqmljstypepropagator.cpp  triggers and prevents  
compilation  
* QTBUG-101155 qml binding to a QML_EXTENDED property doesn't update  
when changed signal emitted  
* QTBUG-67950 Crash when changing Loader source inside a Repeater when  
the model changes  
* QTBUG-99436 Quick Drag and Drop Tiles example broken in Qt 6  
* QTBUG-98857 [REG 6.2.0->6.2.1] QML: Wrong item position after  
drag&drop  
* QTBUG-98011 qmltc crashes due to insufficient import locations in a  
specific Qt build configuration  
* QTBUG-101163 Qmltc error prevents qtdeclarative from compiling  
* QTBUG-92006 Fractional font size is displayed incorrectly  
* QTBUG-77371 Accessibility: Multiple Text items with Accessible  
properties grouped together on Android  
* QTBUG-98181 Importing directory into namespace triggers assert  
* QTBUG-101186 [REG 6.1.3 -> 6.2.0] AnchorAnimation causes Rectangle  
width and height to be zero  
* QTBUG-101285 error: use of undeclared identifier 'r9_1'; did you mean  
'r2_1'?  
* QTBUG-101349 qmlsc and qmlcachegen miscompile draganddrop/grid example  
* QTBUG-101383 QtDeclarative: Fix compiler warnings for QNX  
* QTBUG-101170 Regression: FileDialog.SaveFile fileMode doesn't work  
correctly in QML FileDialog  
* QTBUG-101402 There doesn't appear to be a list of text-field  
validators  
* QTBUG-101197 DragHandler.snapMode not listed in docs  
* QTBUG-100355 [REG 6.2.2 - 6.2.3] Custom image providers do not scale  
on High DPI displays  
* QTBUG-101617 [FTBFS] AUTOMOC for target tst-qmltyperegistrar-with-  
dashesplugin: The "moc" executable "...../qtbase/libexec/moc" does not  
exist.  
* QTBUG-73271 QQmlComponent::setData crashes sporadically when called  
from multiple threads  
* QTBUG-101573 Popup is not closed when MouseArea on ToolTip is pressed  
* QTBUG-101034 Application not detecting submenu shortcuts  
* QTBUG-61971 ComboBox wrong touch behavior  
* QTBUG-94391 FileDialog unwanted uri suffix for Android11 SAF  
* QTBUG-101738 tst_QQmlDebugTranslationService::initTestCase fails on  
macOS 12/arm 64  
* QTBUG-94251 tst_QQuickPopup fails with OpenSUSE 15.3  
* QTBUG-87775 Passing INTERNAL_MODULE to qt_internal_add_module should  
only create a single Qt::FooPrivate target  
* QTBUG-83703 Enums leak from properties to parent objects  
* QTBUG-94068 Undefined behavior  
* QTBUG-77946 tst_QQuickDrawer::Universal::position(right) failed on  
Linux openSUSE_15_0 (gcc-x86_64)  
* QTBUG-87708 [Reg 5.15.0 -> 5.15.1] header's width isn't resized to  
window's width when Layout is used  
* QTBUG-93746 There's no PlaceholderText property in ColorGroup  
* QTBUG-89536 Remove configure.json files for building Qt 6  
* QTBUG-93257 qt6_import_qml_plugins does not compose  
* QTBUG-77417 qmllint: need to handle SignalTransition guard properties  
* QTBUG-76310 Dragging (QDrag) triggered by touch event requires an  
additional press to move drag target  
* QTBUG-54267 Qt Quick Calqlatr example does not properly reflect the  
current way of using Qt Quick  
* QTBUG-94798 crash in QQuickDesignerSupport with gcc at ubuntu  
* QTBUG-94971 QHoverEvent::scenePosition() is actually local position  
* QTBUG-93890 Crash in webOS emulator with recent meta-qt6  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
* QTBUG-93987 Parameter injection warning no longer printed  
* QTBUG-95208 Linker error regarding bitcode when linking CMake app  
targeting iOS  
* QTBUG-94928 loop QQuickDesignerSupport with simple example  
* QTBUG-89380 Cannot use QtObject as containmentMask  
* QTBUG-95152 A QtWebEngine build fails on dev on M1 MacBook  
* QTBUG-94922 base/logging_buildflags.h may not be generated in time  
with top-level build  
* QTBUG-94844 Rendering errors with ShaderEffect after hiding and  
reshowing a window  
* QTBUG-95567 Failure in TestQmllint when merging qtquickcontrols2 into  
qtdeclarative  
* QTBUG-87580 Add minimal set of tests to build for static Qt configs in  
Coin  
* QTBUG-83630 Qt Quick Control 2 Tooltip can be way too big when you  
have newlines  
* QTBUG-94764 REG: Attached ToolTips shrink  
* QTBUG-88138 tst_QQuickDrawer::macOS::slider is failing  
* QTBUG-89938 tst_QQuickPopup::macOS fails with macOS 10.15 and 11.1 and  
with Xcode 12.3  
* QTBUG-95756 tst_QQmlImport::removeDynamicPlugin() is flaky on macOS  
* QTBUG-95609 cmake names for qml plugins  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-95863 tst_qquickpathview::snapOneItem() is flaky on macOS  
* QTBUG-76652 tst_qquicklistview::currentItem() turned flaky on linux  
around june 8th 2019  
* QTBUG-95845 qt_add_qml_module unconditionally installs metatypes.json  
files into "arbitrary" directory  
* QTBUG-95887 tst_FlickableInterop is flaky on opensuse  
* QTBUG-95939 tst_taphandler is flaky on OpenSUSE  
* QTBUG-95938 tst_mousearea_interop is flaky on OpenSUSE  
* QTBUG-95788 Singletons with clearComponentCache don't fully work  
* QTBUG-95740 Property "freqModel" not found on type "Item"  
* QTBUG-93340 trafficlight_qml_dynamic crashes on Android device  
* QTBUG-96121 Versionless CMake commands prevent setting variables in  
calling scope  
* QTBUG-96219 Conversion of versionless wrapper functions to macros  
needs to be reverted  
* QTBUG-96144 qmlsc generates bad code for assigning strings to colors  
* QTBUG-81302 WheelHandler wheel signal is not documented  
* QTBUG-95200 qt6_add_qml_module only works when used in same folder  
than the backing library  
* QTBUG-96261 QtQuickControls2 based application fails to run on macOS  
after using macdeployqt on it  
* QTBUG-83908 Material.System does not work on Windows 10 in Dark Mode  
* QTBUG-93955 Material.System does not work on Ubuntu (Gnome)  
* QTBUG-95262 TypeErrors in tests  
* QTBUG-96127 Broken external links in Qt docs  
* QTBUG-85151 "module "QtQuick.Templates" is not installed" when some  
files' QML imports specify version and some don't  
* QTBUG-91163 cannot build some modules with -developer-build on 32bit  
architectures without -no-warnings-are-errors  
* QTBUG-97055 QQC2 Flickable scrolling is not linear with clicky wheels  
on Qt 6.2.0  
* QTBUG-97092 spelling errors reported by lintian  
* QTBUG-96964 Changing the ShaderEffect shader crashes  
* QTBUG-96454 QT6.2.0 cross compile failed on QNX7.1 Version  
* QTBUG-85084 Skip executing unnecessary commands when building tools  
during cross-compilation  
* QTBUG-86045 Make it possible to set the attached properties for  
DelegateModel declaratively  
* QTBUG-92591 QtDeclarative autotest configure fails on Android builds  
* QTBUG-97075 [REG: 5.14.2->5.15.0] Anchors don't work with InputPanel  
anymore  
* QTBUG-56918 When the keyboard is shown for a text field in a modal  
popup then it will not be usable  
* QTBUG-92881 InputPanels defaults z value should be lower than max  
value for overlays  
* QTBUG-89513 Generating JIT code crashes QML app  
* QTBUG-94806 Having Qmltypes in CONFIG leads to faulty vcxproj file  
* QTBUG-93956 The QSGBatchRenderer::Renderer's m_vertexUploadPool and  
m_indexUploadPool buffers never shrink  
* QTBUG-72110 MouseArea stops responding  
* QTBUG-91545 [iOS] Selection in TextEdit not working for Readonly text  
* QTBUG-75556 Selection in TextEdit not working for Readonly text  
* QTBUG-92809 ListView can go out of sync with the model if item is  
removed and inserted outside of the view before the current item  
* QTBUG-97986 build problem with qmltc test  
* QTBUG-98130 QtQuick and controls examples use qt_add_resources to add  
QML files  
* QTBUG-96806 quick/customitems/painteditem/TextBalloon/qmltextballoon  
not compiling:  
* QTBUG-91033 Multiple extra compilers with same input are broken for VS  
projects  
* QTBUG-98402 tst_qquickimage::mirror() is failing on macOS 12  
* QTBUG-86044 When a ListView is removing items with a transition and  
there is delay remove used then when the last item is removed the footer  
does not go to the top of the view  
* QTBUG-98404  tst_qmlcachegen (Failed)  
* QTBUG-98516 tst_qquickanimations::pathTransition and  
opacityAnimationFromZero are flaky on macos  
* QTBUG-98492 tst_HoverHandler::mouseAreaAndUnderlyingHoverHandler and  
tst_HoverHandler::hoverHandlerAndUnderlyingMouseArea are flaky on macos  
* QTBUG-98491 Flaky tst_qquickmenu tests on macOS  
* QTBUG-98494 tst_qmlformat::testExample times out on  the CI  
* QTBUG-97423 heap-use-after-free in SwipeView::test_orientation  
* QTBUG-98650 Drop Qt 3/4 support  
* QTBUG-98734 FAIL!  : tst_qqmlcomponent::qmlCreateWindow() Received a  
fatal error.  
* QTBUG-98790 ChangeListeners get called even after being semi-deleted  
* QTBUG-98722 SignalSpy.qml triggers a memory leak in the QML engine  
* QTBUG-86633 QML - letters randomly disappear when resizing label  
* QTBUG-95558 Warning on specifying the point size of TextField  
* QTBUG-91691 [REG: 5.15.0->5.15.1] QTextDocument tables with colspan  
collapses the starting column to minimum size  
* QTBUG-99042 qmlsc generates bad code for CallPropertyLookup  
* QTBUG-81938 qtdeclarative:  
tst_QPauseAnimationJob::multipleSequentialGroups is flakey  
* QTBUG-99149 tst_qqmlxmlhttprequest::redirects failing on macOS arm in  
CI  
* QTBUG-99175 tst_QSequentialAnimationGroupJob::  
groupWithZeroDurationAnimations is flaky on macos ARM  
* QTBUG-99174 tst_qquickimageprovider Failed  
* QTBUG-99143 tst_qqmltimer is flaky on macOs  
* QTBUG-97579 When using DelegateChooser with a TreeView and then doing  
a sort on the model in a TreeView, the items are not correctly updated  
to reflect the chooser  
* QTBUG-57098 Popup's CloseOnEscape policy prevents escape key from  
being used without closing the popup  
* QTBUG-99214 Tests that rely on QProcess with the main app lib fail on  
Android  
* QTBUG-99355 tst_qmltc::listView() is flaky under qemu  
* QTBUG-99367 Custom ScrollBar style not used after upgrade from 5.15 to  
6.2  
* QTBUG-83069 TextArea from Material theme is not properly clipped when  
used inside Flickable  
* QTBUG-99615 Most QMutableEventPoint usage depends on Undefined  
Behaviour  
* QTBUG-99582 crash in Controls Text Edit example when pasting in large  
amounts of text  
* QTBUG-100040 Configuring qtdeclarative fails for qmljs, qmljsrootgen  
and qjstest fails when cross-compiling  
* QTBUG-64470 tst_QQuickFramebufferObject::testInvalidate is failing on  
macOS  
* QTBUG-65614 tst_QQuickFramebufferObject failed on b2qt  
* QTBUG-76546 QML debugger tests that run a sub-process fail on QNX  
* QTBUG-100103 A mix of own qmldir and implicit import directory is  
badly broken in qmltc setup  
* QTBUG-95750 RangeSlider::test_overlappingHandles test fails on  
LinuxUbuntu_20_04x86_64LinuxQEMUarmv7GCC  
* QTBUG-99198 QVariant::setValue() asserts when passing an object of  
qmltc-generated type wrapped in QT_NAMESPACE  
* QTBUG-100431 Crash in libQt5Qml V4 engine caused by wrong memory  
access  
* QTBUG-45045 SIGFPE in QQuickMenu  
* QTBUG-52472 Undefined Behaviour in qsimpledrag.cpp line 207  
* QTBUG-75786 macOS 10.14 autotest failures  
* QTBUG-82015 qquickanimations::simplePath() is flakey on macOS  
* QTBUG-82043 tst_qquickmousearea::pressAndHold() is flakey on macOS  
* QTBUG-82404 tst_qquickbehaviors::currentValue is flaky on macos  
* QTBUG-85622 tst_qquickloader: urlToComponent is flaky on macos  
* QTBUG-85624 tst_qquickanimations: reparent is flaky on macos  
* QTBUG-88541 tst_qquickpointhander::tabletStylus doesn't work on hidpi  
* QTBUG-100324 QHelpEvent::globalPos() returns frequently a wrong value.  
* QTBUG-100003 tst_qqmlmoduleplugin fails on Android  
* QTBUG-100014 tst_qqmlqt fails on Android  
* QTBUG-100016 tst_qquickfolderlistmodel fails on Android  
* QTBUG-100018 tst_qmltc_manual fails on Android  
* QTBUG-100020 tst_qqmljsscope fails on Android  
* QTBUG-100021 tst_qdebugmessageservice crashes on Android  
* QTBUG-100164 tst_qqmldebugtranslationservice fails on Android  
* QTBUG-100166 tst_qqmlenginedebugservice fails on Android  
* QTBUG-100167 QML debugger tests fail on Android  
* QTBUG-100169 tst_qqmlextensionplugin fails on Android  
* QTBUG-100171 tst_qmldomitem fails on Android  
* QTBUG-100173 tst_qquickwidget fails on Android  
* QTBUG-100175 tst_testfiltering fails on Android  
* QTBUG-100176 tst_qquickapplicationwindow crashes on Android  
* QTBUG-100177 tst_qquickheaderview fails on Android  
* QTBUG-100191 tst_sanity and tst_snippets fail on Android  
* QTBUG-100253 tst_qquickpopup fails on Android  
* QTBUG-100254 tst_qquickmenubar fails on Android  
* QTBUG-100256 tst_qquickmenu fails on Android  
* QTBUG-100257 tst_qquickdrawer fails on Android  
* QTBUG-100258 tst_focus crashes on Android  
* QTBUG-99103 QQuickMessageDialog: Remove binding loop in non-native  
implementation  
* QTBUG-100839 qmllint guesses wrong about scope in so-called  
unqualified access  
* QTBUG-101329 FAIL!  : tst_QQuickFileDialogImpl::goUp in QNX_710  
* QTBUG-101327 FAIL!  : qquicklayouts::tst_gridlayout::compile in  
QNX_710  
* QTBUG-99761 CMake warns that INSTALL_SOURCE_QMLTYPES is deprecated  
* QTBUG-101174 Qt Design Studio crashes when built with Qt 6.3 Beta  
* QTBUG-101342 tst_qmltc::listView() is flaky under QNX qemu  
* QTBUG-101341 Some autotests cannot find libraries to which it is  
indirectly dependent (quicktest)  
* QTBUG-100991 Some tests crash on Android CI  
* QTBUG-101005 tst_qquickmenu and tst_qquickpopup tests fail to return  
test result  
* QTBUG-101006 tst_qquickiconimage fails on Android  
* QTBUG-101072 Choosing a project name with a dash inside creates a  
broken cmake configuration  
* QTBUG-101451 qtdeclarative/tests/manual/pointer lacks a CMakeLists.txt  
file  
* QTBUG-100938 MessageDialog layout is rather "spacy"  
* QTBUG-101193 Link to Transition QML type is wrong  
* QTBUG-101704 Imagine style ToolTip calculates its width incorrectly  
  
### qtactiveqt  
* QTBUG-95407 activeqt/qutlook fails to configure  
* QTBUG-95406 activeqt examples fails to build, MinGW  
* QTBUG-88414 CMake multi-config build still build some debug tools  
* QTBUG-96121 Versionless CMake commands prevent setting variables in  
calling scope  
* QTBUG-96219 Conversion of versionless wrapper functions to macros  
needs to be reverted  
* QTBUG-85084 Skip executing unnecessary commands when building tools  
during cross-compilation  
  
### qtmultimedia  
* QTBUG-95627 [REG] Unable to mute sound before playing a video  
* QTBUG-95154 no method for getting dimensions of video  
* QTBUG-95641 ImageCapture not working  
* QTBUG-95185 "camera" sample project crashes switching devices  
* QTBUG-95133 Type Multimedia.Video unavailable  
* QTBUG-95766 in QAudioDecoder, provide 'setAudioFormat()' method  
* QTBUG-96251 Multimedia configure fails for targets with no opengl  
* QTBUG-94845 autoOrientation in QML VideoOutput doesn't work  
* QTBUG-95626 [REG] Audio playback is not stopped on MediaPlayer  
destruction  
* QTBUG-95576 [REG] MediaPlayer position property is not updated while  
playing a video  
* QTBUG-96376 Recording fails when encoding audio to other codecs other  
than AAC, WAV, or ALAC  
* QTBUG-96368 Mediaplayer's video output doesn't update when changing  
video source on macOS/iOS  
* QTBUG-96089 Multiply defined symbols found for  
QWindowsIntegration::~QWindowsIntegration(void)  
* QTBUG-96609 Outdated code snippet in QMultimediaPlayer documentation  
* QTBUG-96402 QMediaPlayer position inconsistent  
* QTBUG-96652 QML VideoOuput cannot be used directly with QML Camera  
* QTBUG-96641 Missing properties in MediaPlayer QML type  
* QTBUG-96653 QML MediaPlayer documentation incorrectly uses VideoOutput  
* QTBUG-95066 Multimedia: Missing documentation for QML types  
* QTBUG-96705 The preview parameter from imageCaptured() can no longer  
be used as image source (QML)  
* QTBUG-96642 Loading multiple SoundEffects in QML randomly crashes the  
application  
* QTBUG-96704 In QML, using capture*() after switching between camera  
devices crashes the application  
* QTBUG-95234 MingW build does not find WMF, and builds without a valid  
backend  
* QTBUG-96944 Recorder app crashes while switching between apps  
* QTBUG-96943 Incorrect video orientation for recorded video - recorder  
example  
* QTBUG-95063 audiosource example asserts on startup  
* QTBUG-96984 MediaPlayer example in Detailed Description is missing id  
* QTBUG-96719 Update resolution list by data from the  
QList<QCameraFormat> on QCameraFormat  
* QTBUG-96955 Spectrum app crashes once user try to edit settings  
* QTBUG-97069 [Windows] Crash (use-after-free) on (Q)MediaPlayer  
destruction  
* QTBUG-97152 QMediaPlayer 'play' jumps to wrong position after seek  
* QTBUG-97121 RTSP stream crash Video player  
* QTBUG-96750 Incorrect return from full screen mode for player example  
* QTBUG-96747 Black rectangle visible on the initial screen for player  
example  
* QTBUG-97166 Qt6 Multimedia - Subtitle Language Metadata Detection  
Incorrect?  
* QTBUG-97391 Qt6 QML Multimedia camera example code invalid syntax  
* QTBUG-95369 multimedia/video/android/gstreamer fails on configure  
(typo in CMakeLists.txt?)  
* QTBUG-97091 Disable ALSA and pulse audio by default in the build  
system  
* QTBUG-96985 Video and MediaPlayer don't allow to use relative URLs  
* QTBUG-96956 List of available devices not refreshed while plug in/  
plug out wired headset  
* QTBUG-97485 Build from source of qt multimedia fails on MacOS with  
opengl disabled  
* QTBUG-97622 QML ImageCapture preview property does nothing?  
* QTBUG-97379 [Boot2Qt] Declarative-camera example does not work with  
Toradex Apalis i.MX6  
* QTBUG-97584 qmllint error on VideoOutput: "QQuickItem was not found.  
Did you add all import paths?"  
* QTBUG-97646 Crash on QMediaRecorder when running test  
* QTBUG-97647 Crash on QAudioDecoder when running test  
* QTBUG-97408 multimediawidgets/camera example crashes when launched  
from Finder  
* QTBUG-96899 QAudioDecoder fails on windows  
* QTBUG-97610 Android - QML Camera does not work at first after granting  
permission  
* QTBUG-97402 Qt6 Multimedia: Signals not fired on change of Audio Track  
* QTBUG-97440 Qt Multimedia does not compile without EGL 1.5 on Linux  
platform  
* QTBUG-97730 Wrong QMediaPlayer::position when  
QMediaPlayer::videoOutput==NULL  
* QTBUG-96447 Subtitles do not work on iOS  
* QTBUG-97895 fullscreen does not work in the player example on macOS  
* QTBUG-97839 Listes handling on the Audiorecoder example  
* QTBUG-97832 [Windows] MediaRecorder is not functional for local file  
output locations  
* QTBUG-97911 QVideoWidget stopped working as QCamera viewfinder after  
Qt upgrade 6.2.0->6.2.1  
* QTBUG-97952 Qt6 QML MediaRecorder outputs FormatError when output  
location is incorrect  
* QTBUG-98023 Return value of mimeTypeForFormat  is incorrect on  
QMediaFormat  
* QTBUG-97415 Qt6 Multimedia: Imprecise Seek Behavior for a Local Video  
* QTBUG-96957 Created output file is in inncorrect type and in different  
location  
* QTBUG-96953 Spectrum app crashes once user play button after sound  
ended  
* QTBUG-97992 Stopping QMediaPlayer and starting it again may crash on  
Windows  
* QTBUG-97587 int QAndroidImageCapture::captureToBuffer() // ###  
implement me!  
* QTBUG-97758 QAudioOutput::setDevice doesn't work in Linux  
* QTBUG-98124 Qt Multimedia has an unnecessary dependency to libwayland-  
dev when Qt is configured without Wayland.  
* QTBUG-97080 Wrong video preview orientation on landscape  
* QTBUG-97861 QSoundEffect stop not working  
* QTBUG-98131 Invalid QMediaMetaData::VideoFrameRate  
* QTBUG-97828 Add support for gapless/seamless playback in Qt6  
* QTBUG-97815 QCamera ::setVideoOutput is removed but documentation  
still refers it  
* QTBUG-98559 QtMultimedia Camera Not View on Android 10  
* QTBUG-97909 Implement MediaPlayer Buffering Listener  
* QTBUG-98262 Recording with audio fails on macOS 10.15 (Catalina)  
* QTBUG-98860 Crash during media capture with OpenGL-based rhi  
* QTBUG-98191 QMediaPlayer position reported incorrectly for flac files  
after a seek  
* QTBUG-98306 [REG][macOS] Video orientation is broken  
* QTBUG-99011 QMediaFormat::supportedFileFormats return value is  
incomplete  
* QTBUG-96946 Part of the app greyed out while recording is on  
* QTBUG-99142 QtMultimedia: Invalid target given to  
qt_is_imported_target: Qt6::QSGVivanteVideoNodeFactory  
* QTBUG-99129 Android media player isSeekable() always returns true  
* QTBUG-99181 Fix loadMediaInLoadingState test  
* QTBUG-99183 Fix processEOS test in Android  
* QTBUG-99182 Fix unloadMedia test  
* QTBUG-99134 Declarative Camera issues on video  
* QTBUG-99210 Fix playPauseStop test in Android  
* QTBUG-97780 Video object does not throw an error when source path is  
not resolved  
* QTBUG-99296 Crash when recording audio-only after video recording  
* QTBUG-99176 Recorder example: Crash when switching audio input off  
* QTBUG-97817 Camera example doesn't work  
* QTBUG-99358 Fix SurfaceTest Test in Android  
* QTBUG-99359 Fix Metadata Test in Android  
* QTBUG-99360 Fix audioVideoAvailable Test in Android  
* QTBUG-99661 audioDevice & cameraDevice list properties as methods  
* QTBUG-97838 Recording broken on Apple Silicon / M1  
* QTBUG-99583 Default audio output device not listed as default in  
MediaDevices.audioOutputs  
* QTBUG-99357 Fix SeekPauseSeek Test in Android  
* QTBUG-99849 Doc refers to nonexistent QImageCapture::CaptureToBuffer  
setting.  
* QTBUG-99650 QVideoSink unworkable on Android  
* QTBUG-100050 [REG 6.2.3(and 2)->6.2.1] namespace build fails on  
Windows, MinGW9.0 and MSVC2019  
* QTBUG-100106 Qml Video::seek() fails with TypeError  
* QTBUG-99643 Documentation shows use of deleted QImageCapture  
constructor  
* QTBUG-100341 [REG 6.2.2 - 6.2.3] Memory leak on MediaPlayer  
destruction  
* QTBUG-100283 "Video" keep sending positionChanged signal  
* QTBUG-100501 Typo in documentation of QMediaRecorder  
* QTBUG-100363 [REG 6.2.2 - 6.2.3] Video is always black with OpenGL RHI  
* QTBUG-100638 SoundEffect fails to load .wav files  
* QTBUG-100337 [Win] Vertically oriented video is upside down  
* QTBUG-100665 Crash in OpenGlVideoBuffer destructor  
* QTBUG-100181 QMediaPlayer::setPosition doesn't jump to precisely  
position while playing an FLAC file  
* QTBUG-100773 Android Multimedia arm64v8a target Huawei P40 Lite  
Android 10 QML Recorder example wont work  
* QTBUG-101518 Missing main.qml in Multimedia examples  
* QTBUG-100835 [WMF] Resuming a video after pause generates WMF error  
* QTBUG-100854 [WMF] Crash on resuming playback of specific video  
* QTBUG-101434 QMediaRecorder is stop write to file after bluetooth  
headset is reconnected  
* QTBUG-101591 MediaRecorder/CaptureSession doesn't release audio input  
(mic) on stop recording  
* QTBUG-101719 [REG6.3.0beta2->beta3] some multimedia examples not  
compiling on macOS  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-94895 Clean up Qt Multimedia documentation for Qt 6.2  
* QTBUG-96401 qtmultimedia fails to configure due to not finding GObject  
due to typo.  
* QTBUG-96406 MM Video playback fails completely when using (linking)  
WebEngine  
* QTBUG-96202 SoundEffect does not work in Qt6.2 beta3 in Windows and  
Linux  
* QTBUG-95883 QtMultimedia tests fail on Android  
* QTBUG-96952 Android MediaPlayer not sending onInfo updates  
* QTBUG-95010 Missing loops property  
* QTBUG-96947 Cannot go back from multi option for qmlvideo example  
* QTBUG-97076 QT3D fails to compile on macos when system assimp is  
installed  
* QTBUG-96945 WebM file format not supported for recorder  
* QTBUG-95186 snapCamera fails to show frames  
* COIN-762 Coin's configure command gets warning about unused  
-DBUILD_EXAMPLES=OFF  
* QTBUG-96599 No documentation for how to support different video  
formats  
* QTBUG-98419 [macOS] Audio Recorder example crashes on start on macOS  
10.15 (Catalina)  
* QTBUG-99038 Android:  Fix qmlvideo issues  
  
### qttools  
* QTBUG-93646 .gitignore files in qttools  
* QTBUG-94395 qdoc: Incorrect signature generated for QML signals  
* QTBUG-74353 Qt Assistant doesn't take stylesheet into account with  
search result view  
* QTBUG-90540 Incomplete documentation of namespace "Qt"  
* QTBUG-94480 qdoc:  Broken links to a non-existing module pages  
* QTBUG-94365 QDoc: "error code: 4" from clang on macOS  
* QTBUG-94555 qdoc: Broken links to \internal or \dontdocument nodes  
* QTBUG-94612 qttools' litehtml should be compiled with all warnings  
turned off  
* QTBUG-94613 [FTFBS] qttools does not compile: QtTools/private/qttools-  
config_p.h: No such file or directory  
* QTBUG-91082 [REG: 5.12->5.13] Assistant does not support custom  
filters anymore  
* QTBUG-95561 Typo in the "Introduction To QDoc" manual page.  
* QTBUG-87677 windeployqt locates a release version of icudtXX.dll for a  
debug binary  
* QTBUG-65810 Outdated copyright notes  
* QTBUG-95948 qdoc: Tagging an \fn does not work for \fn commands that  
share a doc comment  
* QTBUG-94796 macdeployqt does not deploy  
/Contents/PlugIns/sqldrivers/libqsqlite.dylib anymore  
* QTBUG-96096 translations are not installed anymore  
* PYSIDE-1376 Translator comments and meta-strings support for pyside-  
lupdate  
* QTBUG-95981 qdoc is ignoring the full path of identical source file  
names  
* QTBUG-95125 [REG 6.1.0 -> 6.2] Assistant shows blank page  
* QTBUG-96220 qt6_create_translation() mishandles -extensions due to  
malformed regex  
* QTBUG-95247 windeployqt does not copy tls plugins  
* QTBUG-95975 [REG Qt 6.2.0 beta1 -> beta2] Rebuilding unchanged sources  
results in build error  
* QTBUG-96837 qdoc: warnings about generatelist incorrectly formatted  
* QTBUG-96694 broken "Contents" links in assistant  
* QTBUG-97028 \relates documentation should mention how it interacts  
with templated classes  
* QTBUG-96521 Windeployqt does not deploy Qt6ShaderTools lib with Rhi  
Renderer  
* QTBUG-97034 qdoc: relative paths in 'includepaths' variable are  
resolved too late  
* QTBUG-96408 QDoc crashed while parsing the index file in Qt5.15  
* QTBUG-97453 qdoc: Unnecessary warnings when running in testing mode  
* QTBUG-97389 'lupdate_sources' variable empty in cmake file generated  
by qt_add_lupdate  
* QTBUG-97562 qdoc: Assert when there's an empty link target  
* PYSIDE-1687 lupdate -tr-function-alias option doesn't work with custom  
function  
* QTBUG-97125 Assistant is unusable on macOS Dark theme  
* QTBUG-97516 Qt Assistant - Background color missing in embedded  
browser  
* QTBUG-97189 Assistant: some keys not working  
* QTBUG-97517 Qt Designer - Command line option "--help-all" has no  
effect  
* QTBUG-97104 macdeployqt fails when qmlimportscanner takes longer than  
30s  
* QTBUG-97627 heap-use-after-free when running ninja html_docs in qtbase  
* QTBUG-98472 [REG 6.2.1->6.3.0] Designer not launching on macOS  
* QTBUG-97380 tst_lupdate fails with Windows 10 21H1 and Windows 11 21H2  
* QTBUG-98517 qdoc: \instantiates causes unnecessary warnings when  
testing in CI  
* QTBUG-98916 Qt Designer sets font family which was set to something  
else in ui file to Segeo UI  
* QTBUG-46322 When setting a family name that has a comma in the name it  
will not match the font correctly  
* QTBUG-91521 When calling lupdate on a file that uses QT_TR_NOOP in a  
constructor for a static QString it will fail to find the context  
* QTBUG-98277 QT_TRID_N_NOOP is missing  
* QTBUG-99232 REG->6.3: Linguist occasionally asserts  
* QTBUG-99404 Qt Designer: Crash when editing spacer objectName in the  
Object Inspector Tab  
* QTBUG-99409 qdoc: Trailing newline in the master .qdocconf fails the  
build.  
* QTBUG-100316 qdoc: ASSERT: "actualNode" in file  
qttools/src/qdoc/docbookgenerator.cpp, line 4246  
* QTBUG-100357 Dependency update on qt/qttools failed in dev  
* QTBUG-100308 Unable to build qttools with tests with the 'Ninja Multi-  
Config' generator  
* QTBUG-99740 qdoc: Automatic \inmodule resolution fails in some  
environments  
* QTBUG-96549 make clean removes ts file when using  
qt5_create_translation()  
* QTCREATORBUG-27087 Bad colors for Stylesheet editor in dark mode  
* QTBUG-101070 Qhelpgenerator endless loop with -c option  
* QTBUG-101893 The 'help' example should only build if 'Qt::Help' is  
built  
* QTBUG-87090 Several lupdate tests are failing with clang-based lupdate  
* QTBUG-89536 Remove configure.json files for building Qt 6  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
* QTBUG-88090 Installed CMake files reference the SOURCE TREE  
* QTBUG-95305 ninja dependency error when configuring a project that  
uses AUTOUIC and CMake 3.21.0  
* QTBUG-95529 bookmark menu don't jump to the viewer when clicked the  
bookmark item  
* QTBUG-96121 Versionless CMake commands prevent setting variables in  
calling scope  
* QTBUG-96219 Conversion of versionless wrapper functions to macros  
needs to be reverted  
* QTBUG-53533 macdeployqt otool parsing broken  
* QTBUG-90982 macdeployqt mistakenly detect my library as debug libs  
* QTBUG-85084 Skip executing unnecessary commands when building tools  
during cross-compilation  
* QTBUG-97765 FTBFS qttools  
* QTBUG-97174 QDoc: \page command translates underscores to hyphens  
* QTBUG-97949 qdoc: erratic behavior on link text formatting  
* QTBUG-98335 qt.conf still expects entries called "Qml2Imports" rather  
than "QmlImports"  
* QTBUG-94345  Qt Designer crash in QQuickWidget plugin  
* QTBUG-100285 Windows: Qt Designer crash when selecting QWebEngineView  
  
### qttranslations  
* QTBUG-94370 .qm files should be put into qtbase/translations for non-  
installable builds  
* QTBUG-94803 Qt 6.2 can't build from source : canbusutil linguist_pl.qm  
No such file or directory  
* QTBUG-96038 qttranslation updateqm target always out of date  
* QTBUG-95975 [REG Qt 6.2.0 beta1 -> beta2] Rebuilding unchanged sources  
results in build error  
  
### qtdoc  
* QTBUG-90510 libqmacstyle.dylib should be mentioned in the document  
* QTBUG-92848 Update Documentation of Qt6: Deploying QML Applications -  
Ahead-of-Time Compilation  
* QTBUG-94903 Add new 6.2 modules to "All Modules"  
* QTBUG-93245 Documentation: New 6.1 modules missing from overview  
* QTBUG-95990 Add support for multi-abi application builds for Android  
with qmake  
* QTBUG-95285 Create documentation page for Qt for Android Manifest  
* QTBUG-97052 Typo in Qt for Windows - Graphics Acceleration  
documentation  
* QTBUG-97438 Compiling universal binaries in Qt Creator error  
* QTBUG-98000 Incorrect header path in the docs  
* QTBUG-98110 Doc defines 5.13 and 5.14 without Extended Support, not  
true  
* QTBUG-98327 qt6 doc error  
* QTBUG-98773 Documented default for libexec in qt.conf is wrong for  
Windows  
* QTBUG-99167 XML support in Qt talks about XML Pattern  
* QTBUG-99847 Update Qt Creator info in Qt Quick tutorial  
* QTBUG-99967 List new modules in 6.3 overview documentation  
* QTBUG-100126 WebAssembly (WASM) Set Up Doc Updates  
* QTBUG-100434 Tutorials/alarms not launching on macOS  
* QTBUG-101652 MessageDialog and FolderDialog links are wrong in What's  
New docs  
* QTBUG-95271 Document "qt-cmake" or add an example which folder in the  
Qt installation should be listed in CMAKE_PREFIX_PATH  
* QTBUG-95748 QtSensors:  update qtdoc module listing  
* QTBUG-96150 QML best practices docs are outdated  
* QTBUG-96127 Broken external links in Qt docs  
* QTBUG-96151 QML deployment docs need to be rewritten  
* QTBUG-87805 Port mkspec QT_QPA_DEFAULT_PLATFORM mechanism to CMake  
* QTBUG-96590 Qt for Android documentation refers to gcc.exe instead of  
clang.exe  
* QTBUG-97842 Move Android tools docs from qtdoc to qtbase  
* QTBUG-96785 "Getting Started with Qt for Android" documentation needs  
an update  
* QTBUG-98335 qt.conf still expects entries called "Qml2Imports" rather  
than "QmlImports"  
* QTBUG-98542 new purchasing is broken on Android when using public key  
verification  
* QTBUG-97449 Clean Android build docs for Qt 6  
* QTBUG-101267 Examples not running on browser on Windows: missing .js  
file  
* QTBUG-101370 Doc about Mac deployment lacks critical info for Qt 6  
  
### qtpositioning  
* QTBUG-57678  
tst_QNmeaPositionInfoSource_RealTime::setUpdateInterval_delayedUpdate()  
fails occasionally in the CI  
* QTBUG-83077 Q12020 Flaky failing autotest function  
setUpdateInterval_delayedUpdate in qnmeapositioninfosource_realtime  
* QTBUG-47503 Output of QGeoSatelliteInfo::satelliteIdentifier() does  
not match documentation  
* QTBUG-36854 Missing updateTimeout() signal when regular update fails  
on Android  
* QTBUG-95221 QGeoCoordinate::toString() sometimes return wrong values  
* QTBUG-94898 Add CMake info to the QtPositioning C++ class  
documentation  
* QTBUG-95582 Qt6::Bundled_Clip2Tri not found  
* QTBUG-91377 [iOS] User is not asked about location permission when  
opening the app  
* QTBUG-78705 No position updates occur if not permitted at startup on  
iOS, even if permissions change later  
* QTBUG-97722 Geoclue-2 plugin fails to report speed and direction  
* QTBUG-97705 PositionSource doesn't stay active nor start on initial  
property values  
* QTBUG-98780 error: use of undeclared identifier 'lcPositioning'  
* QTBUG-99329  
org.qtproject.qt.android.positioning.QtPositioning.positionUpdated calls  
non-existent method  
* QTBUG-71396 QGeoPositionInfoSource does not work from Android service  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
* QTBUG-73055 QGeoRectangle unification doesn't always results in the  
smallest possible rectangle  
* QTBUG-64694 Add QGeoPositionInfo::PositionAccuracy  
* QTBUG-74995 Add documentation for positioning plugins  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-60467 weatherinfo application appid blocked - example not  
working anymore  
* QTBUG-96127 Broken external links in Qt docs  
* QTBUG-97187 Request new repo for QtPositioning  
* QTBUG-97076 QT3D fails to compile on macos when system assimp is  
installed  
* QTBUG-92967 Port addon-module cmake tests from Qt5 to Qt6  
* QTBUG-101345 FAIL!  :  
tst_DeclarativePositionSource::supportedMethodsBinding in QNX_710  
  
### qtsensors  
* QTBUG-96914 Configuring top-level build on Ubuntu 18.04 without pkg-  
config fails in qtsensors  
* QTBUG-98737 Dependency update to qt/qtsensors failed  
* QTBUG-70770 Proximity Sensor Double emits onActiveChanged  
* QTBUG-80755 QSensor::active handling is buggy.  
* QTBUG-73618 tst_sensorgestures_gestures in QtSensors fails on Android  
* QTBUG-72328 Improve sensor examples  
* QTBUG-66318 QTiltReading docs do not specify value units  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
* QTBUG-68383 QCoreApplicationPrivate::theMainThread initialization  
before main()  
* QTBUG-95784 QtSensors:  windows backend specific notes  
* QTBUG-97076 QT3D fails to compile on macos when system assimp is  
installed  
  
### qtconnectivity  
* QTBUG-94392 BTLE: Android->Linux scan finds other side only sometimes  
* QTBUG-55734 NFC Empty Tag causes Error  
* QTBUG-90760 BT discovery stopped working after moving to Qt 5.15.2  
* QTBUG-95349 Typo in Bluetooth Low Energy Overview documentation  
* QTBUG-94897 Add CMake to C++ NFC class documentation  
* QTBUG-94905 Add Qt 6 Porting Guide to Qt Bluetooth  
* QTBUG-94894 Clean up Qt Bluetooth documentation for 6.2  
* QTBUG-93991 Run example Heartrate monitor server on iOS and on Windows  
* QTBUG-95960 IOBluetoothDeviceInquiry never ends  
* QTBUG-95686 Multiple Bluetooth tests fail on macOS  
* QTBUG-80719 connectToDevice() hangs when trying to connect to faulty  
Bluetooth device  
* QTBUG-89149 QLowEnergyController::connectToDevice  
* QTBUG-97242 Windows: 100% CPU load when reading services and  
characteristics  
* QTBUG-96996 BT LE Android Large descriptor write support  
* QTBUG-97691 lowenergyscanner yields 'width' of 'null' QML warnings  
* QTBUG-96997 BT LE Android min/max characteristic size checks  
* QTBUG-97576 BT LE Android server connectivity status with multiple  
connections  
* QTBUG-97900 Crash when connecting to Bluetooth device on macOS 12  
* QTBUG-98073 cork board example crashes on android 12 device when  
targetSDK set to 31  
* QTBUG-98323 Assertion failure when running bluetooth/btchat example  
* QTBUG-98353 QBluetoothSocket.connectToService failing on Android  
devices with a java error  
* QTBUG-96742 Timing issues in BTLE peripheral on Android  
* QTBUG-96743 BTLE on Android: Characteristic supposed to support both  
Notification and Indication supports neither  
* QTBUG-98719 QBluetoothSocket deletion occasionally crashes on Windows  
* QTBUG-98582 QT Bluetooth LE crashed when connect/disconnect to a  
device  
* QTBUG-98878 Bluetooth LE characteristic Indication manual test fails  
on darwin server  
* QTBUG-82685 QBluetoothDeviceDiscoveryAgent::error not emitted in  
Windows when the Bluetooth is turned off in Windows Bluetooth settings  
* QTBUG-99288 BT LE client on macOS doesn't recover if the bluetooth was  
initially OFF  
* QTBUG-99617 SDP attribute write fail  
* QTBUG-99673 Service discovery with UUID filter doesn't work on macOS  
Monterey  
* QTBUG-99687 Windows BT service scan scans just one device  
* QTBUG-99410 [macOS 12.1] Bluetooth data stream blocked when main menu  
opened  
* QTBUG-100445 macOS bluetooth SDP records contain anomalies  
* QTBUG-99689 Windows BT service scan filter fails against Linux server  
* QTBUG-100289 pingpong Linux => Windows doesn't work  
* QTBUG-100819 Bluez lowenergy peripheral incomplete initialization  
* QTBUG-99295 The tool "Qt6::sdpscanner" was not found  
* QTBUG-100303 Bluetooth RFComm [Outbound] connection issue with  
Monterey  
* QTBUG-100894 Linux bluetooth crash when multiple services found  
* QTBUG-101018 Bluez backend doesnt extract socket protocol information  
from service info  
* QTBUG-101071 Bluez dbus socket gives different error codes than other  
platforms  
* QTBUG-101586 Bluetooth Android server asserts if disposed too quickly  
after listen()  
* QTBUG-101690 QBluetoothSocket::canReadLine can sometimes return false  
negative  
* QTBUG-101721 QBluetoothSocket double-emits connected() on macOS  
* QTBUG-101720 [REG 6.3.0beta2->beta3] bluetooth/heartrate-server not  
compiling on iOS  
* QTBUG-93595 BTLE advertising on Android does not work with  
setLocalName set  
* QTBUG-89536 Remove configure.json files for building Qt 6  
* QTBUG-94449 Problem with build system dependencies regarding Java code  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-96057 Bluetooth crash when connectToPairedDevice on windows  
* QTBUG-83633 Bluetooth Discovery device crash  
* QTBUG-85084 Skip executing unnecessary commands when building tools  
during cross-compilation  
* QTBUG-96688 BT LE Android large characteristic write support  
* QTBUG-86796 Documentation should mention that qt bluetooth and audio  
requires QGuiApplication  
* QTBUG-96995 BT LE Android mtu() method error on peripheral side  
* QTBUG-97076 QT3D fails to compile on macos when system assimp is  
installed  
* QTBUG-98090 macOS examples that need special plist keys need their own  
plist files  
* QTBUG-96557 Qt bluetooth can not scan device on Mac 12 beta  
* QTBUG-97578 QT Bluetooth hang when scan services/characterictics  
* QTBUG-75100 There is no way to know if a bluetooth adapter is  
available  
* QTBUG-98781 BT LE test case platform support enhancement  
* QTBUG-98955 tst_QBluetoothServiceInfo::tst_assignment fails on macOS  
12 ARM  
* QTBUG-98351 Thread-safe Android BT LE Java implementation  
* QTBUG-99222 Re-enable Bluetooth autotests on macOS  
* QTBUG-84234 Start new QCoreApplication after shutdown  
* QTBUG-98817 In QtConnectivity multiple QBluetooth autotest failures  
with macOS 12 ARM64  
* QTBUG-100042 Windows BT (server) pingpong service is not found  
* QTBUG-99685 Windows BT classic service scan doesn't always start  
* QTBUG-94001 QtBluetooth uses deprecated Windows API  
* QTBUG-101309 Bluez handle Enhanced LE connection complete  
  
### qtwayland  
* QTBUG-64652 TextInputManager lacks documentation  
* QTBUG-62786 Missing QPlatformIntegration::queryKeyboardModifiers()  
implementation in Wayland QPA  
* QTBUG-88261 Spurious duplicate output from cmake-based configure  
* QTBUG-94602 Releasing wayland buffer from Qt compositor side  
* QTBUG-95394 Crash in RHI when exiting a QtWaylandCompositor with  
active clients.  
* QTBUG-95388 [REG] Qt6WaylandGlobalPrivate package not found by  
Qt6WaylandClient  
* QTBUG-95464 Qt wayland surface is empty when gst-launch client is  
playing video  
* QTBUG-87624 Wayland client crash when QDrag is used  
* QTBUG-96464 Wayland client race condition in applyConfigure  
* QTBUG-96845 Failed to build FEATURE_wayland_dmabuf_client_buffer  
* QTBUG-93474 Gnome on Wayland: Right click empties the clipboard  
* QTBUG-97245 Wayland compositor crash when creating and destroying  
windows  
* QTBUG-97094 Wayland modifiers map decoding has flawed logic  
* QTBUG-97394 Crash when using zwp_text_input_v2  
* QTBUG-96298 QInputMethod::visibleChanged was not send when keyboard is  
open and close with QtTextInputMethodManager  
* QTBUG-98010 Screen information unavailable on Wayland  
* QTBUG-98897  error: ‘QWaylandOutput* QWaylandOutputPrivate::q_func()’  
is private within this context  
* QTBUG-95962 Wayland: Crash in XDG Shell when resizing window with  
mouse  
* QTBUG-90530 Low resolution title bar icon on Wayland on Hi DPI  
displays  
* QTBUG-92249 quick3d examples crashes or hangs on exit on wayland  
* QTBUG-95032 Dialogs on Wayland/Sway not drawn correctly when using  
client side decorations  
* QTBUG-99760 CMake warns about linking to plugins  
* QTBUG-99746 QtWayland fails to compile against recent EGL headers  
* QTBUG-97593 Qt with QtWayland doesn't build without QtQml  
* QTBUG-99802 qtwayland doesn't have all options in qt_cmdline.cmake  
* QTBUG-99965 Build with -no-feature-tabletevent fails for Linux/Wayland  
* QTBUG-100475 qtwayland features are misdetected  
* QTBUG-100845 Cannot compare two const QWaylandBufferRefs  
* QTBUG-87303 Wayland context menus can go off the screen because Qt  
does not do set_constraint_adjustment  
* QTBUG-100942 Mouse button kept pressed state after closing the window  
in mouse press handler  
* QTBUG-89536 Remove configure.json files for building Qt 6  
* QTBUG-94580 Hover enter/leave events regression  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-95715 Incorrect texture handling in multi-screen wayland  
compositor  
* QTBUG-96121 Versionless CMake commands prevent setting variables in  
calling scope  
* QTBUG-96219 Conversion of versionless wrapper functions to macros  
needs to be reverted  
* QTBUG-96259 Support wl_seat v7  
* QTBUG-81504 QWaylandWindow::handleUpdate creates thousands of pending  
frame callbacks, causing wayland connection termination  
* QTBUG-85084 Skip executing unnecessary commands when building tools  
during cross-compilation  
* QTBUG-66075 Wayland event dispatcher multi-threading support  
* QTBUG-97076 QT3D fails to compile on macos when system assimp is  
installed  
* QTBUG-97985 Wayland: XComposite backend does not update surfaces  
properly  
* QTBUG-97950 Application slowly reads every file in /usr/bin before  
starting  
* QTBUG-96258 Support wl_seat v6  
* QTBUG-100150 Touch event ignored when main GUI thread is slow  
  
### qt3d  
* QTBUG-93428 Examples not finding QtConcurrent  
* QTBUG-97708 Error when compiling qanimationclipdata.cpp against  
qtbase/dev  
* QTBUG-95439 Qt 3D Planets arm64-v8a example  "Invalid minSdkVersion  
version, minSdkVersion must be >= 23"  
* QTBUG-97254 Pugixml workaround for QTBUG-11923 causes C1001 in  
MSVC2019 with PCH  
* QTBUG-101176 Linker error when AVX2 is disabled in core but enabled in  
Qt3D  
* QTBUG-93035 Adding a disable entity to the scene and enabling it later  
isn't properly picked up  
* QTBUG-95130 Qt3D ShaderProgram sources cannot compile on iOS (RHI)  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
* QTBUG-90321 QT_BEGIN_LICENSE:LGPL3 references non-existing file  
LICENSE.GPL  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-97076 QT3D fails to compile on macos when system assimp is  
installed  
* QTBUG-86493 ComputeCommand.trigger(1) executes compute shader more  
than 1 time  
* QTBUG-98097 Qt3D license only GPL or Commercial?  
* QTBUG-97950 Application slowly reads every file in /usr/bin before  
starting  
* QTBUG-98420 Configure failure with system assimp  
* QTBUG-99945 [REG 6.2.2-> 6.2.3] qt3d/audio-visualizer-qml fails to  
compile  
* QTBUG-100568 Crash in Renderer::cleanupShader  
  
### qtimageformats  
* QTBUG-89536 Remove configure.json files for building Qt 6  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
  
### qtserialbus  
* QTBUG-94838 QCanBus passthrucan  
* QTBUG-94695 Buffer overflow when using systeccan plugin for  
QtSerialBus  
* QTBUG-95040 [Reg 5.15 -> 6.2] New incoming CAN frames not read into  
QCanBusDevice  
* QTBUG-95387 [REG beta1->beta2] Serialbus examples fail to build  
* QTBUG-86533 Yocto and QNX builds are missing -rpath-link linker flag  
which causes non-prefix builds to fail  
* QTBUG-97685 Qt SerialBus Qt 6 change documentation replaced SerialPort  
documentation  
* QTBUG-98800 [PeakCAN] Incorrect QCanBusFrame::TimeStamp conversion  
* QTBUG-96566 Serialbus can example fails to build  
* QTBUG-101689 QtSerialbus library linking is done using wrong Network  
library interface  
* QTBUG-89536 Remove configure.json files for building Qt 6  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-85084 Skip executing unnecessary commands when building tools  
during cross-compilation  
* QTBUG-97076 QT3D fails to compile on macos when system assimp is  
installed  
  
### qtserialport  
* QTBUG-98735 C:/Users/qt/work/install/include/QtCore/6.3.0/QtCore\priva  
te/qobject_p.h:497:78: error: 'q_func' is a private member of  
'QSerialPortPrivate'  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-89536 Remove configure.json files for building Qt 6  
  
### qtwebsockets  
* QTBUG-87279 [REG: 5.13.2-5.14.0] When interacting with a webpage that  
will trigger a signal via QWebChannel then if the slot is still running  
it can cause it to resend the same message rather than a new one  
* QTBUG-94932 Add Qt 6 Porting Guide to Qt WebSockets  
* QTBUG-97681 C++ classes of the QtWebSockets module have misspelled  
package names in the instructions for CMake  
* QTBUG-100054 QWebSocket can emit binaryMessageReceived signal after  
being disconnected  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-96127 Broken external links in Qt docs  
* QTBUG-92967 Port addon-module cmake tests from Qt5 to Qt6  
* QTBUG-101333 FAIL!  : tst_QWebSocketServer::tst_handleConnection in  
QNX_710  
  
### qtwebchannel  
* QTBUG-89536 Remove configure.json files for building Qt 6  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
* QTBUG-94931 Add Qt 6 Porting Guide to Qt WebChannel  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-92967 Port addon-module cmake tests from Qt5 to Qt6  
* QTBUG-101521 FAIL!  : qml::tst_bench::compile in QNX_710  
  
### qtwebengine  
* QTBUG-94333 Examples can't be configured due to target name conflict  
* QTBUG-94572 Update dependencies on '6.2' in qt/qtwebengine fails  
* QTBUG-88105 Windows fails sandboxed on the CIs  
* QTBUG-94759 webengine needs more dependencies checks  
* QTBUG-94343 QtWebEngineCore include paths sometimes missing when  
building core files  
* QTBUG-94709 6.2.0 Qt src package, webengine not compiling  
* QTBUG-94702 Doc: Qt WebEngine docs aren't getting built in dev/6.2  
* QTBUG-95153 6.2 QtWebEngineProcess is also in /bin  
* QTBUG-94757 Incorrect CMAKE_TOOLCHAIN_FILE check  
* QTBUG-94804 QtWebEngine install doesn't honor DESTDIR  
* QTBUG-95051 qtwebengine not forwarding CMAKE_BUILD_TYPE correctly.  
* QTBUG-94997 qtwebengine not respecting CMAKE_INSTALL_PREFIX  
* QTBUG-95473 Qt WebEngine build fails to locate the xkbcommon include  
* QTBUG-95367 Webengine examples fails to build: undefined reference to  
`QApplication::QApplication(int&, char**, int)'  
* QTBUG-95571 Console window for QtWebengineProcess.exe is displayed on  
initialization QML WebEngineView  
* QTBUG-95614 Google looks weird with QtWebEngine built with cmake  
* QTBUG-95331 QWebEnginePage::view() disappeared without a trace  
* QTBUG-94937 Clean up Qt WebEngine documentation for Qt 6.2  
* QTBUG-95564 Minimum ICU version is too low  
* QTBUG-94933 Add Qt 6 Porting Guide to Qt WebEngine  
* QTBUG-94349 cmake cannot find Qt6Targets.cmake and  
Qt6VersionlessTargets.cmake when configuring prefix build  
* QTBUG-94922 base/logging_buildflags.h may not be generated in time  
with top-level build  
* QTBUG-95152 A QtWebEngine build fails on dev on M1 MacBook  
* QTBUG-95158 Insource/Namespace/Shadow build fails.  
* QTBUG-95972 CMake build tries to link after compile error  
* QTBUG-95231 qtwebengine translations and resources installed to wrong  
path  
* QTBUG-95590 Rewrite cmake-gn intergration  
* QTBUG-96093 QtWebEngineProcess cannot start  
* QTBUG-95668 Webengine widget not visible in Designer UI  
* QTBUG-94772 Crash in Page's test: openLinkInNewPage:OverridePopup  
* QTBUG-76249 [Reg 5.9->5.11]Custom UserAgent ignored if page opened  
with window.open or _blank  
* QTBUG-96196 configure -list-features does not list webengine features  
* QTBUG-95717  Configuring: Qt 6.2 " Unknown command line option  
'-webengine-proprietary-codecs'."  
* QTBUG-96266 webengine not building (linking): LINK : fatal error  
LNK1104: cannot open file  
'CMakeFiles_QtWebEngineCore_Release_objects.rsp'  
* QTBUG-96308 Drag and drop does not work on macOS  
* QTBUG-95770 Cannot open recently saved file  
* QTBUG-95580 Crash on GetFaviconsForURL  
* QTBUG-96398 Build fails on arm  
* QTBUG-96539 WebEngineView: QtWebEngineProcess cannot start.  
* QTBUG-96002 The document QtWebengine is self-contradictory  
* QTBUG-96771 Webengine/quicknanobrowser fails to build: undefined  
reference to `QApplication::QApplication(int&, char**, int)'  
* QTBUG-96375 Build failure with webengine  
* QTBUG-96930 REG:5.15.3->5.15.4 - When doing a pinch gesture inside a  
WebEngineView then it has no effect  
* QTBUG-96855 QWebEngineDownloadItem::setDownloadFileName failed in disk  
root  
* QTBUG-97598 [Windows] Deadlock on WebEngineView rendering  
* QTBUG-94604 QtWebEngineProcess and resource paths are wrong with  
-developer-build -framework on macOS  
* QTBUG-97897 Tooltips hide by themselves almost immediatelly when  
launched from QWebEngineView  
* QTBUG-97926 QWebengine can not play the  embeded vimeo video  
* QTBUG-97836 QtWebEngineCore still not compiling from source  
* QTBUG-84105 Out-of-proc networking causes firewall confusion  
* QTBUG-92539 Weird behavior when pasting certain HTML into element with  
contentEditable attribute set  
* QTBUG-90904 Crash on calling QAccessible::registerAccessibleInterface  
* QTBUG-97472 [REG] Crash/segfault in ozone implementation when calling  
XkbGetState  
* QTBUG-98400 CVE-2021-3541 in chromium  
* QTBUG-98401 CVE-2021-3517 in chromium  
* QTBUG-71277 Nanobrowser example has confusing project layout  
* QTBUG-97414 tst_CertificateError::fatalError()  
'!page.error->isOverridable()' returned FALSE.  
* QTBUG-45582 Duplicated vtables due to inline virtual functions  
(probably all dtors)  
* QTBUG-98918 [REG] recentlyAudible does not implement 2s cooldown  
anymore  
* QTBUG-99511 Top level cross build fails  
* QTBUG-99526 developer tools no longer highlights page elements when  
inspecting them  
* QTBUG-99485 Qt WebEngine AutomationId issue  
* QTBUG-99215 Html popups do not work correctly.  
* QTBUG-99263 QProcess::finished not emitted  
* QTBUG-99669 Glib network plugins doesn't configure or build  
* QTBUG-99890 QtWebEngine ozone platform needs pkgconfig check for  
xkbfile include  
* QTBUG-86972 [REG] QtPDF isn't properly installed as a framework unless  
WebEngine is also installed  
* QTBUG-100023 Cannot use Qt6::Pdf Module (Not Found)  
* QTBUG-94924 Load signals not emitted when opening a google result  
* QTBUG-100032 tst_qquickwebview: malloc_consolidate(): invalid chunk  
size  
* QTBUG-100285 Windows: Qt Designer crash when selecting QWebEngineView  
* QTBUG-100293 spellcheck error: session_bridge_ was not declared  
* QTBUG-100291 abort early on missing dependency: gssapi.h for kerberos  
* QTBUG-96597 Crash on WebEngine(View|Profile).userScripts.collection  
property get  
* QTBUG-100500 System libxslt is not used  
* QTBUG-101084 Test  #1: tst_qwebenginecookiestore  
.................***Failed  
* QTBUG-100996 WebEngine crashes in Accessibility  
* QTBUG-100672 Universal builds of WebEngine fail on M1 mac  
* QTBUG-101290 Unable to build examples when building as module with  
-DQT_BUILD_EXAMPLES=ON  
* QTBUG-101706 [REG] ASSERT: "event->reason() != Qt::PopupFocusReason"  
in file \Users\qt\work\qt\qtwebengine\src\webenginewidgets\render_widget  
_host_view_qt_delegate_widget.cpp, line 79  
* QTBUG-94368 [QtPDF] bitcode bundle could not be generated because  
libQt5Pdf.a was built without full bitcode  
* QTBUG-86948 When using QImageReader to load a PDF then the PDF images  
can be blurry and seem to be at half the size they should be  
* QTBUG-94046 QtPDF: configuration with -static-runtime causes linker  
errors for projects  
* QTBUG-96525 QWebEngineScript::setSourceUrl doesn't load scripts from  
qrc  
* QTBUG-101935 FAIL!  : tst_QWebEnginePage::pasteImage() Compared values  
are not the same  
* QTBUG-101697 QtPDF's plugins.qmltypes is not installed  
* QTBUG-92519 [REG 5.15.2 -> 5.15.3] Can't upload files on Photopea  
* QTBUG-91467 [REG 5.15.0 -> 5.15.2] OCSP is used even if not enabled  
* QTBUG-86021 WebEngineView "backgroundColor" has no documentation  
* QTBUG-94911 change locale does not work on embedded(QEMU)  
* QTBUG-95924 Touch events are not accepted in webenginequick by default  
* COIN-699 add ulimit for linux nodes  
* QTBUG-86533 Yocto and QNX builds are missing -rpath-link linker flag  
which causes non-prefix builds to fail  
* QTBUG-95269 Clicking on a link in the PDF viewer crashes with SIGSEGV  
* QTBUG-95339 QPrintPreviewDialog crash  
* QTBUG-88875 WebChannel is broken in ApplicationWorld with javascript  
disabled in MainWorld  
* QTBUG-96127 Broken external links in Qt docs  
* QTBUG-96928 QtWebEngine continuously allocates memory until it get  
killed  
* QTBUG-85084 Skip executing unnecessary commands when building tools  
during cross-compilation  
* QTBUG-96942 Developer tools open with "toogle screencast" enabled  
* QTBUG-97188 Make sure that all bots know about the new repo  
* QTBUG-99119 [REG 5 -> 6] Segfault in  
QtWebEngineCore::WebContentsDelegateQt::webEngineSettings() on Google  
Meet  
* QTBUG-98941 [Qt5.15.4][QWebEngine]QWebEnginePage::print() function  
printing a grey paper while printing a PDF in Qt5.15.4  
* QTBUG-101215 QML certifciate errror test is broken, but works on c++  
side  
* QTBUG-50686 QWebSettings::LocalContentCanAccessRemoteUrls not working  
with audio tags  
* QTBUG-87154 Add static dependencies from 3rdparty in qtbase  
* QTBUG-100404 Changes around WebEngineScript are not documented  
* QTBUG-100713 Qt WebEngine: --disable-gpu does not disable GPU  
  
### qtwebview  
* QTBUG-94381 .gitignore files in qtwebview  
* QTBUG-94475 [6.2.0] 'Qml' is missing from CMakeLists.txt from  
QtWebView, building from sources fails  
* QTBUG-94376 Update dependencies on '6.2' in qt/qtwebview fails  
* QTBUG-94934 Add Qt 6 Porting Guide to Qt WebView  
* QTBUG-94935 Clean up Qt WebView documentation for Qt 6.2  
* QTBUG-99372 FAILED: tests/auto/webview/qwebview/tst_qwebview  when  
builing for QNX  
* QTBUG-86533 Yocto and QNX builds are missing -rpath-link linker flag  
which causes non-prefix builds to fail  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-101487 FAIL!  : tst_QWebView::load in QNX_710  
* QTBUG-101520 FAIL!  : tst_QQuickWebView::stopEnabledAfterLoadStarted  
in QNX_710  
  
### qtcharts  
* QTBUG-94469 Doc: Wrong return type for QValueAxis::labelFormat qml  
property  
* QTBUG-94472 [REG 6.2 snapshot->6.2 current] qml/QtCharts/designer -dir  
missing  
* QTBUG-95307 Qt Charts is missing in module upgrade documentation  
* QTBUG-94998 5.15.4 -> 5.15.5, some labels disappeared from axes  
* QTBUG-79218 When zooming out enough then the labels on the axes will  
end up showing drawing errors  
* QTBUG-92544 charts/audio has dependency to non-existent module  
Multimedia  
* QTBUG-60529 Chart doesn't resize after hiding axis labels  
* QTBUG-95870 Setting plotArea for a ChartView in a layout is not  
respected  
* QTBUG-81278 Switching axis that is shared by multiple series to  
another doesn't work  
* QTBUG-98282 QPieSlice label does not indicate it takes html formatted  
text  
* QTBUG-99044 [REG Qt5 -> Qt6.2]: Chart with QLineSeries and  
QScatterSeries does not receive mouse events  
* QTBUG-100810 QML ChartView series color can get wrong on RHI if  
useOpenGL  
* QTBUG-89536 Remove configure.json files for building Qt 6  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-92967 Port addon-module cmake tests from Qt5 to Qt6  
* QTBUG-101517 FAIL!  : example::tst_barcategoryaxis::compile in QNX_710  
  
### qtdatavis3d  
* QTBUG-90371 The labels for the bars are not displayed when property  
"Rotate horizontally" set max to the right  
* QTBUG-94441 Axis title labels do not respect the Abstract3DAxis's  
titleFixed property  
* QTBUG-78767 baseGradient for Surface3DSeries is applied incorrectly  
when the trailing line(s) of the QSurfaceDataArray contain NaN only  
* QTBUG-95270 Can't link to 'Qt Data Visualization' from qdoc  
* QTBUG-94364 Rotate and zoom do not work on Android  
* QTBUG-94331 Some examples do not work correctly on macOS  
* QTBUG-95923 WireFrameColor in datavisualisation needs revisioning  
* QTBUG-95941 Currently signals take argument as value instead of const  
ref  
* QTBUG-96206 Graph's orthoprojection property doesn't work like  
documentation says  
* QTBUG-97683 [REG 6.2.0.6.2.1] examples-manifest has wrong paths,  
examples not visible in Creator UI  
* QTBUG-97931 CMake warning about linked plugins in Qt Data  
Visualization  
* QTBUG-100400 API review Qt 6.2.0. -> Qt 6.3 issue  
* QTBUG-99724 qtnetwork examples fail on configure on Wasm: missing  
Qt6::DataVisualizationPrivate  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-101513 FAIL!  : qmltest::tst_category::compile in QNX_710  
  
### qtvirtualkeyboard  
* QTBUG-94259 High CPU load on embedded targets caused by timers  
* QTBUG-93042 Program crashed when type with keyboard  
* QTBUG-94560 The first item of selection list sometimes get highlight  
* QTBUG-94017 Cursor position moves when un-converted Japanese is  
deleted  
* QTBUG-68412 tst_plugin::test_pinyinInputMethod crashes on arm  
* QTBUG-94715 Qt Virtualkeyboards support for Chinese language doesn't  
work properly  
* QTBUG-95664 VirtualKeyboardSettings: Readonly property is not marked  
as such  
* QTBUG-95893 Missing documentation for dictionary API  
* QTBUG-95996 Segmentation fault on exit caused by virtual keyboard  
* QTBUG-97075 [REG: 5.14.2->5.15.0] Anchors don't work with InputPanel  
anymore  
* QTBUG-56918 When the keyboard is shown for a text field in a modal  
popup then it will not be usable  
* QTBUG-92881 InputPanels defaults z value should be lower than max  
value for overlays  
* QTBUG-97983 Highlighted example virtualkeyboard/basic not configuring  
on Wasm  
* QTBUG-96578 Virtual Keyboard Deployment guide does not cover widget  
applications  
* QTBUG-89536 Remove configure.json files for building Qt 6  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-97076 QT3D fails to compile on macos when system assimp is  
installed  
* QTBUG-97830 Some Qt Virtual Keyboard tests checking the position of  
selection handles are failing  
* QTBUG-97901 tst_plugin::test_hangulInputMethod(row 24) fails  
* QTBUG-97439 [REG 5.15.2->6.2] Virtual Keyboard is hidden by QML dialog  
* QTBUG-101512 FAIL!  : inputpanel::tst_inputpanel::compile in QNX_710  
* QTBUG-101536 FAIL!  : styles::tst_styles::compile in QNX_710  
  
### qtscxml  
* QTBUG-94386 Update dependencies on '6.2' in qt/qtscxml fails  
* QTBUG-95921 scxml examples fail to build for iOS target  
* QTBUG-95208 Linker error regarding bitcode when linking CMake app  
targeting iOS  
* QTBUG-98738  
/Users/qt/work/qt/qtscxml/src/statemachineqml/state_p.h:92:66: error:  
unknown type name 'm_childrenComputedProperty'  
* QTBUG-89536 Remove configure.json files for building Qt 6  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
* QTBUG-95305 ninja dependency error when configuring a project that  
uses AUTOUIC and CMake 3.21.0  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-96121 Versionless CMake commands prevent setting variables in  
calling scope  
* QTBUG-96219 Conversion of versionless wrapper functions to macros  
needs to be reverted  
* QTBUG-96253 Unable to build qtscxml tests after building with  
components with Conan  
* QTBUG-85084 Skip executing unnecessary commands when building tools  
during cross-compilation  
* QTBUG-92967 Port addon-module cmake tests from Qt5 to Qt6  
* QTBUG-101343 FAIL!  : tst_statemachineqml::tst_anonymousstate::compile  
in QNX_710  
  
### qtnetworkauth  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-96127 Broken external links in Qt docs  
  
### qtremoteobjects  
* QTBUG-94513 RemoteObjects/modelviewclient crashes  
* QTBUG-94570 QEventDispatcherWin32::registerTimer: Failed to create a  
timer  
* QTBUG-87672 Adjust qtremoteobjects public CMake API  
* QTBUG-94899 Clean up Qt RemoteObjects documentation for Qt 6.2  
* QTBUG-95832 QtRemoteObjects CMake API is using the internal  
qt_manual_moc API  
* QTBUG-91041 Remote Objects: Model headers are not updated  
* QTBUG-97688 Clients don't reconnect to replaced nodes over TCP  
* QTBUG-97704 POD type replication issue  
* QTBUG-99269 tst_Integration_External test is failing on MacOS-arm64  
* QTBUG-85124 QRemoteObjectHost::hostUrl() crashes if no URL is set  
* QTBUG-89536 Remove configure.json files for building Qt 6  
* QTBUG-94904 Update "Changes to Qt Modules" for Qt 6.2  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-96121 Versionless CMake commands prevent setting variables in  
calling scope  
* QTBUG-96219 Conversion of versionless wrapper functions to macros  
needs to be reverted  
* QTBUG-91163 cannot build some modules with -developer-build on 32bit  
architectures without -no-warnings-are-errors  
* QTBUG-85084 Skip executing unnecessary commands when building tools  
during cross-compilation  
* QTBUG-92967 Port addon-module cmake tests from Qt5 to Qt6  
* QTBUG-101336 FAIL!  : ModelreplicaTest::basicFunctions in QNX_710  
  
### qtlottie  
* QTBUG-98794 LottieAnimation::source not loaded in Qt 6  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
  
### qtquicktimeline  
* QDS-3216 Flickering when using default value as implcit first keyframe  
* QTBUG-97043 qtquicktimeline: commercial only license ?  
  
### qtquick3d  
* QTBUG-94263 Balsam seems to interpret a sphere parented under leaf  
joint as joint  
* QTBUG-94337 Model-blend particles rendered incorrectly when endNode  
has rotation  
* QTBUG-94479 Suzanne mesh doesn't work with model-blend particles  
* QDS-4536 3D editor broken in latest snapshot, sometimes crashes Design  
Studio  
* QDS-4574 3D node navigator preview crashes puppet  
* QTBUG-94589 Crash if model-blend particle is not properly initialized  
* QTBUG-95212 Error when empty scene is loaded  
* QTBUG-95535 CMake functions for offline shader and light probe  
generation do not work on Android  
* QTBUG-90409 quick3d: consume 4x memory for custom geometry and memory  
leak  
* QTBUG-95534 Rename depthSorting property in Instancing  
* QTBUG-95616 Incorrect shadowmap bounds calculated from camera frustum  
* QTBUG-95583 Incorrect shadowmap bounds when referencing camera from  
different node  
* QTBUG-95586 Z-Prepass doesn't render correctly if scene has only  
transparent objects with depth write  
* QTBUG-95743 TransformSpace property of Node item can't be read/changed  
* QDS-4841 Remove import versions from quick3D designer source templates  
for Cube, View3D etc.  
* QDS-4853 Picking 3D objects is completely broken in 3D editor  
* QDS-4873 Designer specifics have errors for quick3d property sheets  
* QTBUG-94830 Rotation of skeleton root node rotates the skeleton but  
not the skinned meshes  
* QTBUG-94829 Directional light casts too wide shadows  
* QTBUG-94828 Shadows don't work if there is a #Rectangle model inside  
imported scene  
* QDS-4859 Item could not be created -error when adding a Qt 3D Studio  
component to Navigator (Qt6 project)  
* QTBUG-95620 QuickBall example crashes after hitting the first target  
* QTBUG-96163 ModelParticle3D instanceTable property not documented  
* QDS-5004 FBX imported models broken in 3D Editor  
* QDS-5103 Issues with QtQuick3D.Particles3D module designer specifics  
* QDS-5098 QtQuick3D.FileInstancing component is shown in library as  
"Instancing"  
* QDS-5096 Fix property specifics for QtQuick3D.Repeater3D  
* QTBUG-96730 Custom Material fragment shader sometimes does not have  
access to special variables  
* QTBUG-79026 WasdController can't get control of keyboard back after  
using UI element  
* QTBUG-97260 Model blend particle spatial node is not always  
initialized  
* QTBUG-97676 SSAA expands orthographic camera view  
* QTBUG-96736 Insert #line directives to custom material and effect  
shaders in order to print useful line numbers in error messages  
* QTBUG-98342 View3D mapping functions do not work correctly with  
orthographic camera and 2x pixel ratio  
* QTBUG-98448 A map used in two passes will not have its UV Coords  
generated in the second one  
* QTBUG-98330 Particlesystem keeps updating particles even when not  
visible  
* QTBUG-98579 Particles example crashes in  
QSSGBufferManager::cleanupUnreferencedBuffers  
* QTBUG-98583 R32F QQuick3DTextureData does not work  
* QDS-3025 Adding a spotlight under another node that is not in global  
origin places the light gizmo to global origin in 3D view  
* QTBUG-96184 Directional light shadow bounding box too small when using  
model blend particles  
* QTBUG-99012 Scene rendering getting slower per QQuick3DGeometry  
updates  
* QTBUG-97254 Pugixml workaround for QTBUG-11923 causes C1001 in  
MSVC2019 with PCH  
* QTBUG-99112 IOR support causes gltf crashes on i.MX8  
* QDS-5064 Instances created by using XML files are not visible in Form  
Editor  
* QTBUG-98749 Application crashes if there are more then 8 light sources  
* QTBUG-97925 ProgressiveAA does not work if there are  
PrincipledMaterials in scene  
* QTBUG-98748 TriangleFan primitive type can't be used [should handle  
this more gracefully and print a warning]  
* QTBUG-98756 U16Type doesn't work for joint indexes  
* QTBUG-99738 Reflection probe crashes if backgroundMode is not SkyBox  
* QTBUG-99430 Crash if a Model is created via Repeater3D  
* QTBUG-94616 Low saturation of sky texture  
* QTBUG-99992 AssetUtils.RuntimeLoader requires absolute file path for  
source  
* QTBUG-100831 Model spams with Vertex buffer empty warning  
* QTBUG-100572 Quick 3D: Shadow maps aren't working correctly  
* QTBUG-99759 Dynamically creating and destroying models causes  
assertion failure  
* QTBUG-100009  
qtquick3d/src/runtimerender/graphobjects/qssgrenderparticles.cpp:57:33:  
error: call of overloaded sqrt(int&) is ambiguous  
* QTBUG-100832 View3D.mapFrom3DScene crashes for large values  
* QTBUG-94453 Rectangles can't be used for light probs in View3D  
* QTBUG-89536 Remove configure.json files for building Qt 6  
* QTBUG-94548 Multimeshes not working with model-blend particles  
* QDS-4509 Cannot run a project that has QtQuick3D Effects module added  
* QDS-4399 Properties missing for some components  
* QDS-4471 Adding 2D content to a 3D scene breaks 3D Editor  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
* QTBUG-95284 QtQuick3D fails to build in CI when targeting WebAssembly  
+ CMake 3.21.0 + Ninja due to command line length limit  
* QTBUG-94539 mapTo3DScene() will fail when a camera is not explicit  
assigned  
* QTBUG-94693 Scenes with two View3D are not properly updated  
* QTBUG-95634 Property "forward" of Node is non-NOTIFYable  
* QDS-4801 3D Particle system running on QDS stops running after ~20  
seconds  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-94969 Sharing a scene with embedded 2D content between two  
windows crashes  
* QTBUG-96121 Versionless CMake commands prevent setting variables in  
calling scope  
* QDS-4967 Wander3D uniqueAmount property is missing  
* QDS-4981 Wrong default value of SpriteSequence3D randomStart  
* QTBUG-96219 Conversion of versionless wrapper functions to macros  
needs to be reverted  
* QDS-4978 Wrong default value of property editor Model pickable  
property  
* QTBUG-96307 Issue with stopped particle system and startTime  
* QTBUG-96457 "infinite plane" Item2D prevents event propagation to 2D  
content behind it  
* QTBUG-96514 Item declared in a Node or Model creates an Item2D  
immediately; reparenting leaves behind an empty 2D subscene  
* QTBUG-85084 Skip executing unnecessary commands when building tools  
during cross-compilation  
* QTBUG-92841 Offscreen Surfaces should not receive input events in 3D  
scenes  
* QTBUG-96558 RTA CMake test fails on macOS10.15 and macOS11.0  
* QTBUG-97076 QT3D fails to compile on macos when system assimp is  
installed  
* QTBUG-97920 Designer editor view has shadow image with model-blend  
particles  
* QTBUG-97586 Setting delegate dynamically before model is set breaks  
Repeater3D  
* QTBUG-97950 Application slowly reads every file in /usr/bin before  
starting  
* QTBUG-98007 Designer puppet crashes at startup  
* QTBUG-98111 Particle emitter bursts do not work with animated emitter  
* QDS-5552 Long delay before emitting after particle system is rewinded  
* QTBUG-98420 Configure failure with system assimp  
* QTBUG-97857 Item2D shouldn't be always pickable  
* QTBUG-97715 Quick3D examples fail on imx6  
* QTBUG-99615 Most QMutableEventPoint usage depends on Undefined  
Behaviour  
* QTBUG-100019 TemporalAA not working while animating the scene  
* QDS-6081 Changing camera on View3D doesn't change the view in form  
editor  
* QDS-4966 Editing Model source with property editor fails  
* QTBUG-96624 Lightprobe/skybox exposure and tonemapping issues  
* QTBUG-101354 Particles not taking into account global opacity  
* QTBUG-101371 Node.sceneRotation may get wrong if parent node is scaled  
non-uniformly  
* QTBUG-101373 Item2D node rendered indefinitey on threaded render loop,  
blocks updates on basic render loop  
* QTBUG-101718 [REG 6.3.0beta2->beta3] quick3d/principledmaterial not  
launching on macOS  
  
### qtshadertools  
* QTBUG-95048 Linkage error during building any qt quick3D application  
for Integrity based on Qt6  
* QTBUG-96618 qtquick3d examples fail to build for QNX  
* QTBUG-96524 Qsb tool output (errors) not visible when called From  
visual studio / cmake  
* QTBUG-96912 No documented way to build GLES shader using  
samplerExternalOES with qsb  
* QTBUG-96121 Versionless CMake commands prevent setting variables in  
calling scope  
* QTBUG-96219 Conversion of versionless wrapper functions to macros  
needs to be reverted  
* QTBUG-85084 Skip executing unnecessary commands when building tools  
during cross-compilation  
  
### qt5compat  
* QTBUG-98656 QXmlInputSource (Qt5 Core compatibility) does not properly  
read encoding instruction  
* QTBUG-100024 qt5compat requires qtdeclarative despite it's not really  
required  
* QTBUG-100359 tst_qlinkedlist.cpp doesn't build: missing  
QLinkedListIterator  
* QTBUG-89536 Remove configure.json files for building Qt 6  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-83081 QTextCodec::canEncode does not work for ICU conversions  
* QTBUG-97122 Regression: UTF-32 codec fails on assert when  
fromUnicode() is called  
* QTBUG-96127 Broken external links in Qt docs  
  
### qtcoap  
* QTBUG-94610 [FTBFS] qtcoap and qtdeclarative have a conflicting target  
name  
* QTBUG-94763 [CoAP] When resource is observed the QT CoAP client sends  
an acknowledgement packet which is not empty.  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-96127 Broken external links in Qt docs  
* QTBUG-91163 cannot build some modules with -developer-build on 32bit  
architectures without -no-warnings-are-errors  
  
### qtmqtt  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
  
### qtopcua  
* QTBUG-89536 Remove configure.json files for building Qt 6  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-91163 cannot build some modules with -developer-build on 32bit  
architectures without -no-warnings-are-errors  
* QTBUG-85084 Skip executing unnecessary commands when building tools  
during cross-compilation  
* QTBUG-96228 [OPCUA] Qt Opc UA client crashes after disconnect /  
reconnect  
  
Known Issues  
------------  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Mike Achtelik  
Dan Ackers  
Laszlo Agocs  
Waqar Ahmed  
Alexander Akulich  
Dimitrios Apostolou  
Viktor Arvidsson  
Luca Beldi  
Vladimir Belyavsky  
Nicholas Bennett  
Chen Bin  
Jan Blackquill  
Alex Blasche  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
Francisco Boni  
Tatiana Borisova  
Joerg Bornemann  
Assam Boudjelthia  
Michael Brasser  
Kai Uwe Broulik  
Michael Brüning  
Oswald Buddenhagen  
Igor Bugaev  
Andreas Buhr  
Kirill Burtsev  
Jungi Byun  
Giulio Camuffo  
Méven Car  
Juan Casafranca  
Wang Chuan  
Albert Astals Cid  
Michał Cieślak  
Raphael Cotty  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Szabolcs David  
Noah Davis  
Rodney Dawes  
Pascal Dietz  
Alexey Edelev  
David Edmundson  
Oliver Eftevaag  
Balazs Egedi  
Christian Ehrlicher  
Iikka Eklund  
Hatem ElKharashy  
Andreas Eliasson  
Fabio Falsini  
David Faure  
Ilya Fedin  
Wang Fei  
Nicolas Fella  
Fabrice Fontaine  
Alexandros Frantzis  
Kevin Funk  
Simo Fält  
Samuel Gaist  
Talent Gc  
Pekka Gehör  
Lucie Gerard  
Christophe Giboudeaux  
Markus Goetz  
Maximilian Goldstein  
Andrei Golubev  
Robert Griebl  
Magnus Groß  
Henning Gruendl  
Jan Grulich  
Kaj Grönholm  
Richard Moe Gustavsen  
Lucie Gérard  
Ralf Habacker  
Tang Haixiang  
Heikki Halmet  
Zhang Hao  
Thomas Hartmann  
Andre Hartmann  
Andreas Hartmetz  
Jani Heikkinen  
Miikka Heikkinen  
Christian Heimlich  
Karsten Heimrich  
Ulf Hermann  
Øystein Heskestad  
Arjen Hiemstra  
Volker Hilsheimer  
Dominik Holland  
Agnieszka Jaworska  
Allan Sandfeld Jensen  
Tim Jenssen  
Yin Jie  
William Jones  
Jaeyoon Jung  
Janne Juntunen  
Povilas Kanapickas  
Jonas Karlsson  
Jeremy Katz  
Youngjin Kim  
Marius Kittler  
Friedemann Kleint  
Michal Klocek  
Lars Knoll  
Seokha Ko  
Jarek Kobus  
Kai Koehne  
Sze Howe Koh  
Jarkko Koivikko  
Tomi Korpipaa  
Jani Korteniemi  
Lukas Kosinski  
Janne Koskinen  
Fabian Kosmale  
Volker Krause  
Mike Krus  
Simeon Kuran  
Sona Kurazyan  
Igor Kushnir  
Jonas Kvinge  
Kai Köhne  
Inho Lee  
Elvis Lee  
Tony Leinonen  
Eric Lemanissier  
Paul Lemire  
Qiang Li  
Robert Löhning  
Thiago Macieira  
Pavol Markovic  
Tamas Martinec  
Tamás Martinec  
Thorbjørn Lund Martsum  
Cristian Maureira-Fredes  
Ievgenii Meshcheriakov  
Leena Miettinen  
Samuel Mira  
Fawzi Mohamed  
Bartlomiej Moskal  
Andrey Mozzhuhin  
Marc Mutz  
Tommi Mänttäri  
Antti Määttä  
Sivan Nanthiran  
Biswapriyo Nath  
Georges Basile Stavracas Neto  
Alexander Neumann  
Delf Neumärker  
Andy Nichols  
Daniel Nicoletti  
Yuya Nishihara  
Mårten Nordheim  
Kimmo Ollila  
Tinja Paavoseppä  
Gatis Paeglis  
Cathy Park  
Tuomo Pelkonen  
Wang Peng  
Mauro Persano  
Raffaele Pertile  
Pasi Petäjäjärvi  
Samuli Piippo  
Timur Pocheptsov  
Milla Pohjanheimo  
Joni Poikelin  
Aleix Pol  
Alessandro Portale  
Rami Potinkara  
Lorn Potter  
Liang Qi  
Zhang Qipeng  
Yuntaek RIM  
David Redondo  
Arno Rehn  
Topi Reinio  
Hannah von Reth  
Aleksandr Reviakin  
Florian Richter  
André de la Rocha  
David Rosca  
Bernhard Rosenkraenzer  
Fan RuiJie  
Peter Rustler  
Shawn Rutledge  
Toni Saario  
Timofey Sartakov  
Lars Schmertmann  
David Schulz  
Björn Schäpers  
Craig Scott  
Luca Di Sera  
Dmitry Shachnev  
Ye ShanShan  
Orgad Shaneh  
Tianlu Shao  
Andy Shaw  
Venugopal Shivashankar  
Evgeny Shtanov  
Pierre-Yves Siret  
David Skoland  
Daniel Smith  
Ivan Solovev  
WenTao Song  
Axel Spoerl  
Piotr Srebrny  
Andrii Staikov  
Patrick Stewart  
Martin Storsjö  
Brett Stottlemyer  
Christian Strømme  
Frank Su  
Tasuku Suzuki  
Jan Arve Sæther  
Morten Johan Sørvig  
Morten Sørvig  
Nodir Temirkhodjaev  
Benjamin Terrier  
Samuel Thibault  
Ivan Tkachenko  
Pino Toscano  
Jens Trillmann  
Alex Trotsenko  
Jere Tuliniemi  
Paul Olav Tvete  
Jüri Valdmann  
Sami Varanka  
Peter Varga  
BogDan Vatra  
Martin Vejdarski  
Doris Verria  
Nico Vertriest  
Tor Arne Vestbø  
Harald Vistnes  
Jannis Voelker  
Alexander Volkov  
Ville Voutilainen  
Juha Vuolle  
Jaishree Vyas  
ChunLin Wang  
Chen Wei  
Gong Weia  
Bernd Weimer  
Edward Welbourne  
Peng Wenhao  
Niklas Wenzel  
Clemens Werther  
Paul Wicking  
Oliver Wolff  
Milian Wolff  
Kama Wójcik  
Li Xi  
Li Xinwei  
Weng Xuetian  
Zhang Yong  
Marianne Yrjänä  
Zhang Yu  
Yang Yuyin  
Vlad Zahorodnii  
JiDe Zhang  
Yuhang Zhao  
Evan Zhou  
Eike Ziller  
chenbin  
hjk  
