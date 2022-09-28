Release note  
============  

Qt 6.4 introduces many new features and improvements as well as bugfixes  
over the 6.3.x series. For more details, refer to the online  
documentation included in this distribution. The documentation is also  
available online:  
  
https://doc.qt.io/qt-6/index.html  
  
The Qt version 6.4 series is binary compatible with the 6.3.x series.  
Applications compiled for 6.3 will continue to run with 6.4.  
  
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
* 2e2f1e2af7 Add css media rule support for QTextDocument::setHtml()  
Add css media rule support for QTextDocument::setHtml()  
  
* 19d231e47d QThread::idealThreadCount: use the thread affinity set  
idealThreadCount() will now return the number of logical processors  
that the current process (thread) has assigned in its affinity set,  
instead of the total number of processors in the system. These two  
numbers can be different if the process is launched by the parent with a  
different affinity set, with tools like Linux's taskset(1) or  
schedtool(1). This is currently implemented for Linux and FreeBSD.  
  
* 4631b61c81 Q_{APPLICATION,GLOBAL}_STATIC: use variadic macros  
The Q_GLOBAL_STATIC macro is now variadic. Any extra arguments are used  
as constructor arguments, obliterating the need to use  
Q_GLOBAL_STATIC_WITH_ARGS().  
  
* 46dc8e453a QVariant: use a typedef name when saving user types to  
QDataStream  
If QDataStream is used with a QDataStream::Version < Qt_6_0 to  
serialize a user type that was registered via a typedef with the  
metatype system, the typedef's name is used in the stream instead of the  
non-typedef name. This restores compatibility with Qt 5, allowing  
existing content to read the same QDataStreams; reading from older Qt 6  
versions should not be affected. (Note: if more than one typedef name is  
registered, it's indetermine which name gets used)  
  
* 9b320edb53 QStringBuilder: fix quadratic behavior in op+=  
Fixed quadratic behavior when repeatedly appending string-builder  
expressions (using operator+=) to QString/QByteArray objects.  
  
* c953e5c417 QByteArray: avoid detach() in a no-op replace()  
A replace(pos, n, after) call no longer detach()es when n ==  
after.size() == 0.  
  
* 7c8126d909 QTestData: fix streaming of u8 string literals in C++20  
mode  
Fixed streaming of u8 string literals in C++20 mode.  
  
* 9ea1f0f8b9 Fix qobject_cast on partially destroyed QWidget/QWindow  
Using qobject_cast on partially constructed or destroyed  
QWidget/QWindow instances now yields correct results. Similarly, using  
the convenience isWidgetType() / isWindowType() functions now correctly  
return false on such instances. Before, qobject_cast (and the  
convenience functions) would erroneously report that a given object was  
a QWidget (resp. QWindow) even during that object's construction (before  
QObject's constructor had completed) or destruction (after QWidget's  
(resp. QWindow's) destructors had been completed). This was semantically  
wrong and inconsistent with other ways of gathering runtime type  
information regarding such an object (e.g. dynamic_cast,  
obj->metaObject()->className() and so on).  
  
* 93c1f481ab Add QTextDocumentFragment::toRawText()  
Added QTextDocumentFragment::toRawText() function.  
  
* 17eb0f2d8a Keep original text for text/plain mime data  
Special characters like &nbsp; are now preserved in the text/plain part  
of the clipboard when copied from a QTextEdit or QLineEdit.  
  
* c20b213eab SQLite: Update SQLite to v3.37.0  
Updated SQLite to v3.37.0  
  
* e9fd1c6aab QScreen_win: retrieve user friendly monitor name  
QScreen::name() now returns the user friendly name instead of the GDI  
device name on Windows. This is consistent with other platforms and also  
obeys the documentation.  
  
* 11becbe910 QTzTimeZonePrivate: fix UB (data race on m_icu)  
Fixed a data race on Unix platforms when implicitly-shared copies of  
QTimeZone objects were used in certain ways (e.g. calling displayName())  
from different threads and Qt was configured with ICU support.  
  
* 197b5de0d8 qtpaths: Expose new PublicShareLocation, TemplatesLocation  
PublicShareLocation, TemplatesLocation got added as known locations to  
QStandardPaths.  
  
* 413cd06c88 Fix crash when text shaping fails  
Fixed a possible crash with certain fonts when shaping strings  
consisting only of control characters.  
  
* b387fbd122 QVersionNumber: change int to qsizetype for index and  
length  
Updated the QVersionNumber API to use qsizetype where length and index  
values were used. This change retains binary compatibility and the vast  
majority of users will not experience a source compatibility problem. It  
could occur with ambiguous overloads when passing results from  
QVersionNumber to other API not using either int or qsizetype. There  
could also be new warnings from compilers about converting 64-bit types  
to 32-bit ones.  
  
* e52d50a03d QLatin1String: perform the comparison to another QL1S using  
memcmp()  
Fixed a couple of bugs where two QLatin1Strings or two QUtf8StringViews  
would stop their comparisons at the first embedded null character,  
instead of comparing the full string. This issue affected both classes'  
relational operators (less than, greater than, etc.) and  
QUtf8StringView's operator== and operator!=.  
  
* 9ffcab6562 QVersionNumber: port fromString() to QAnyStringView  
fromString() now takes QAnyStringView (was: QString, QStringView,  
QLatin1String) and a qsizetype pointer (was: int pointer).  
  
* 6f6c8d0618 QVersionNumber: don't allocate in fromString() in the  
common case  
Can now be also be constructed from QVarLengthArray.  
  
* 1b4a5ecc91 JSON: When clearing duplicate object entries, also clear  
containers  
A memory leak in the JSON parser when reading objects with duplicate  
keys was fixed.  
  
* a59e736171 QMetaType: add a missing check for null d_ptr  
Fixed a bug that would cause QMetaType::compare() and  
QVariant::compare() to crash on invalid meta types and variants.  
  
* f0371487ce QTabBar: Improve scrolling with high resolution mouse  
wheels  
Scrolling with a high resolution mouse wheel changes the current index  
at a rate more like a normal mouse wheel.  
  
* 79aad61fc1 Enable all supported 1.0 device features in QVulkanWindow  
QVulkanWindow is now enabling all Vulkan 1.0 features reported as  
supported from the physical device.  
  
* b083c27d0a QVulkanWindow: make it possible to override the enabled  
features  
QVulkanWindow can now invoke a callback to alter the  
VkPhysicalDeviceFeatures object used to create the Vulkan device. This  
allows enabling 1.1, 1.2, and extension features.  
  
* b5d480d01d QHash: fix iteration of x86 AES hash code for len >= 32  
Fixed a bug in the qHashBits() function, which affected the hashing of  
QByteArray, QString (and their View classes), QLatin1String and  
QBitArray, which caused the hash to not include the final 32 bytes of  
the data source. As a result, QHash containers where the initial string  
was the same had a serious performance degradation on x86 CPUs with AES  
support.  
  
* 31a39bd55d QByteArrayList: simplify the join() overload set already  
now  
The join() overload set has changed. Code such as  
qOverload<>(&QByteArrayList::join) will have to be rewritten, e.g. using  
lambdas. We advise against taking addresses of library functions other  
than signals and slots.  
  
* 3d3558dc8f QStaticByteArrayMatcher: fix searching in 2+GiB haystacks  
Fixed searching in strings with size > 2GiB (on 64-bit platforms).  
  
* 2d95b75345 QByteArray: fix isUpper/isLower  
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
  
* 2e29a427ca Windows: Change default hinting preference for high-dpi  
When high-dpi scaling is active, the default text antialiasing has been  
set to symmetric for larger fonts (pixel size higher than 16 px). The  
old default can be selected manually as QFont::PreferVerticalHinting.  
  
* fb8bd02e63 rhi: d3d11: Switch the default swap effect and scaling mode  
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
  
* 9f31f579ec Sequential erase/_if: don't apply predicate twice to  
element  
A fix in the implementation of the erase-like algorithms of sequential  
Qt container may re-enable signed/unsigned comparison warnings  
previously suppressed by having occurred in std library code. To fix,  
cast the value to look for such that it has the same signedness as the  
container's elements.  
  
* 724e4646e2 Fix clipped glyphs in text rendering of QGraphicsTextItem  
Clipping of visible glyphs when doing partial updates of a graphics  
view was off by 1. Also fixed an issue that caused rounding errors when  
transforming the clip rect into the glyphs draw space which was caused  
by transforming a QRect instead of a QRectF.  
  
* b0e8ba783b DirectWrite: Turn off grid-fitting for unhinted text  
Automatic grid-fitting is now disabled for fonts that set  
QFont::PreferNoHinting.  
  
* 348f67d7ec qmetatype.h: remove unused includes  
The qmetatype.h header no longer includes qvarlengtharray. It might be  
necessary to include the header explicitly if code previously relied on  
it being implicitly included.  
  
* 1734c4ee98 qaccessible: Split QAccessible into own header  
<QAccessible> no longer includes <stdlib.h>. This might break code that  
relied on transitive includes.  
  
* ec03db7bb3 Fix C++20 ambiguous relational operators between  
QJsonValue{,Ref}  
Fixed relational operators to not cause warnings/ambiguities when  
compiling in C++20.  
  
* 29fceed2ff QProcess/Unix: ensure we don't accidentally execute  
something from CWD  
When passed a simple program name with no slashes, QProcess on Unix  
systems will now only search the current directory if "." is one of the  
entries in the PATH environment variable. This bug fix restores the  
behavior QProcess had before Qt 5.9. If launching an executable in the  
directory set by setWorkingDirectory() or inherited from the parent is  
intended, pass a program name starting with "./". For more information  
and best practices about finding an executable, see QProcess'  
documentation.  
  
* ae7799a924 qtextstream.h: streamline includes  
The qtextstream header no longer includes <QString>, <QStringEncoder>  
and <QStringDecoder>. Code which relied on the implicit inclusion of  
those classes might now need to include the headers explicitly.  
  
* f482e2a456 QDesktopServices: fix ABA problem in  
QOpenUrlHandlerRegistry  
Fixed a bug where destroying and re-creating a handler object in quick  
succession could cause the registration for the handler to be lost.  
  
* c6958cbbd6 Add new third party SHA-3 implementation to replace old  
obsolete one  
Added new SHA-3 implementation to Qt Core. The code is available under  
BSD 3-Clause "New" or "Revised" License.  
  
* 37a25fce94 QDesktopServices: deprecate destroying URL handlers w/o  
explicit unsetUrlHandler()  
URL handlers that have been passed to setUrlHandler() must now be  
removed by calling unsetUrlHandler() before they are destroyed. Relying  
on the handler's destructor to implicitly unset it is now deprecated,  
because it may already be in use by concurrent openUrl() calls. Support  
for implicit unsetting will be removed in 6.6 and, until then, a  
qWarning() is raised if it is exercised.  
  
* 04dc959d49 Introduce Q{Json,Cbor}ValueConstRef  
The iterator classes for Qt's JSON and CBOR containers (array and  
map/object) had a const correctness issue which allowed a const_iterator  
to mutate the container being iterated on, even if that container was  
itself const. Qt 6.4 has a fix for this, but will cause compilation  
issues where QCborValueRef and QJsonValueRef were used where the  
correctness could be violated. To keep code compiling with both 6.3 and  
6.4, either change to non-const iteration or replace the QxxxValueRef  
with a const QxxxValue reference. This change is binary-compatible.  
  
* 8de0493896 QMetaObjectBuilder: fix addProperty() recording of the  
property type  
Fixed a bug that would cause addProperty() to use the incorrect type  
for the property if the property's name matched a valid type registered  
with QMetaType.  
  
* 65a02da1b5 Make large inputs to qNextPowerOfTwo give undefined output  
The qNextPowerOfTwo() functions now have preconditions.  
  
* b2a9646be9 QIODevice::readAll: allow reading from a huge non-  
sequential devices  
Changed readAll() handling of large non-sequential devices like files  
that are bigger than the maximum QByteArray size (on 32-bit systems,  
just under 2 GB). Previously, readAll() always returned empty; now it  
will attempt to read from the device.  
  
* dcd87049bb Treat invalid Q(Date)?Time as null when used as an SQL  
value  
Handling of QDateTime and QTime values passed to SQL now consistently  
treats invalid as null. Some values of these types are neither valid nor  
null, which could lead to invalid data being given to the SQL database.  
Invalid values are now treated as null to prevent this.  
  
* 87c6e340a9 QStringConverter: fix move special member functions of  
State class  
Fixed a potential data corruption in the move constructor and move-  
assignment operator on 32-bit platforms.  
  
* 66203133e3 QStringConverter: make explicit what should never have been  
implicit  
All QStringEncoder/Decoder constructors are now explicit.  
  
* a87edb9ae9 QStringEncoder/Decoder: make base class ctors protected  
The destructors of the base classes of QStringEncoder and  
QStringDecoder are now protected, to prevent slicing.  
  
* a74cdf778c Implement QFormLayout::set/isRowVisible  
New APIs setRowVisible and isRowVisible to hide and show rows in a form  
layout.  
  
* 1058f053e5 MSVC: Raise minimum version of Visual Studio 2019 to 16.7  
The minimum MSVC version was raised to Visual Studio 2019 version 16.7  
(VC++ version 14.27). Trying to use an older version will now result in  
a compile time error.  
  
* cba40055b1 Network: Use public suffix database in DAFSA format  
Moved attribution of The Public Suffix List from Qt Core to Qt Network.  
  
* 4cca8ee527 QGuiApplication: use translation-based layout direction  
unless explicitly set  
Calling setLayoutDirection with a non- auto value now disables the  
auto-detection based on installed translators. Applications that  
explicitly set a layout direction and also want translators installed  
afterwards to take effect should reset the layout direction to Auto,  
which is now no longer a no-op.  
  
* 6e9a3d4209 QSettings: support reading UTF-8 keys in INI files  
The INI file reader now supports keys encoded with UTF-8, as well as  
the %-encoded format. Writing the keys back to the INI file is still  
done using %-encoded format. This change does not touch the way the  
*values* are handled - they are both read and written in UTF-8.  
  
* 03b9304703 Update bundled libjpeg-turbo to version 2.1.3  
libjpeg-turbo was updated to version 2.1.3  
  
* 736213bf66 QLatin1String: add missing APIs for compatibility with Qt  
string views  
Added QLatin1String(std::nullptr_t) constructor, which makes  
QLatin1String(0) call ambiguous. To fix the ambiguity, nullptr must be  
passed instead of 0.  
  
* 66a76a5def wasm: enable mobile native keyboarding  
Add support for native mobile keyboard  
  
* 16b614f2e1 Network: Use system publicsuffix database copy when  
available  
It is possible to use system's copy of publicsuffix database when it is  
available. This behavior is enabled by default on Linux and can be  
controlled using new command line switches -system-publicsuffix, -qt-  
publicsuffix, -no-publicsuffix, and -publicsuffix=all.  
  
* 0deff80eab Associative containers: add a way to obtain a key/value  
range  
Added asKeyValueRange().  
  
* e2a0ddbb69 CMake: Make configure less verbose by default  
The configure output verbosity of non developer-builds of Qt is now  
reduced by default. Pass "-- --log-level=STATUS" to configure to make it  
verbose again.  
  
* e440fec7fc Add literal operators for QLatin1String and QLatin1Char  
Added literal operator""_L1 that converts string literals and chars to  
QLatin1String and QLatin1Char.  
  
* f39f539858 Add numeric conversion methods to QLatin1String  
Added numeric conversion methods.  
  
* 78b6876974 Long live QColor::fromString()!  
Added fromString() and isValidColorName(), both taking QAnyStringView.  
  
* 30d28810ee Add QLatin1String::count(needle)  
Added QLatin1String::count(needle).  
  
* 82e12c79b2 Add an overload of QStringView::count() for QLatin1String  
Added an overload of QStringView::count() for QLatin1String.  
  
* abe3b4c9b9 Extract Header qstringfwd.h  
Added header qstringfwd.h containing forward-declarations of all Qt  
string classes.  
  
* d743fd0d0a qDecodeDataUrl(): treat ";base64" marker as case-  
insensitive  
Now recognizes the ";base64" marker in "data:" URLs case-insensitively.  
  
* 6585963583 Deprecate {QString, QByteArray}::count()  
Deprecated QString::count() and QByteArray::count() that take no  
parameters, to avoid confusion with the algorithm overloads of the same  
name. They can be replaced by size() or length() methods.  
  
* 67385c04ce QDataStream: make qfloat16 streaming a non-member  
The qfloat16 QDataStream operators are now hidden friends and only  
found by argument-dependent lookup. Previously, these were member  
functions on QDataStream.  
  
* 08d6bc2477 Prevent exclusion of percent character from percent-  
encoding  
When converting to percent-encoding, it was possible to exclude the  
percent character (or its replacement, unless this is one of the  
characters not normally encoded) from conversion.  Doing so would  
violate RFC 3986 Section 2.4 and break round-tripping of any string that  
contains the percent character. The percent character, or its  
replacement, is now always encoded, even if mentioned in the exclude  
list, as the documentation has always claimed.  
  
* 9b8015ed8d QMutexLocker: add isLocked()  
Added the isLocked() function.  
  
* ce83a03cfd QColor: deprecate isValidColor, setNamedColor, string-ish  
ctors  
The constructors from string-ish type, as well as the setNamedColor()  
and isValidColor() functions, have been deprecated effective Qt 6.6 in  
favor of fromString() and isValidColorName(), resp.  
  
* 9da4c6bfb7 QObject: port setObjectName() to QAnyStringView  
Added setObjectName() overload taking QAnyStringView.  
  
* f3c340c276 QStringTokenizer::toContainer(): allow more types of target  
containers  
toContainer() now works on containers whose value_type can be  
constructed from the tokenizer's value_type. It no longer requires an  
exact match.  
  
* cc5cc3225d QHash: Initialize the hash seed as soon as QtCore loads  
QtCore now initializes the QHash global seed before the main() function  
is run, so it is no longer possible to use qputenv() to affect the seed  
value for the current process. Disabling the random global seed for the  
current process should be done programmatically with by calling either  
the 6.2 function QHashSeed::setDeterministicGlobalSeed() or, if  
compatibility with Qt 5 is required, by calling qSetGlobalQHashSeed()  
with value 0.  
  
* 7d5604c194 Deprecate QElapsedTimer::TickCounter  
QElapsedTimer::TickCounter enum is now deprecated. Qt does not use the  
Windows API behind this enum already since Qt 5.9, so it's fair to  
assume that any code path relying on the enum is dead code.  
  
* 893dd5d7be Add QStringView::localeAwareCompare()  
Added QStringView::localeAwareCompare().  
  
* fb0c7a9956 QVariant: reduce transitive includes  
qvariant.h no longer includes <QList>, <QMap>, <QHash>,  
<QVarLengthArray>, <QSet> and <QObject>. Code that relied on transitive  
includes might need to explicitly include those headers now. Notably,  
including <QVariant> (or qvariant.h) is no longer sufficient when using  
QVariant(List|Map|Hash). Using them now requires including respectively  
<QVariantList>, <QVariantMap>, or <QVariantHash>. Alternatively,  
including <QVariant> and the <QList>, <QMap> or <QHash> header also  
works.  
  
* 20d0ff1a39 QMutexLocker: add move semantics  
The class is now movable.  
  
* e10d613509 Add QByteArray::percentDecoded() as an instance method  
percentDecoded() is now available as an instance method of the byte  
array to be decoded, equivalent to the static  
QByteArray::fromPercentEncoding().  
  
* 1b14569753 QMutexLocker: strenghten the locking operations  
QMutexLocker allowed relock() and unlock() on an already closed (resp.  
open) locker object. These semantics have always been undocumented and  
are now unsupported (in both cases they yield undefined behavior.)  
  
* 33d62de7c8 Enable move semantics for QTemporaryDir  
Enabled move semantics.  
  
* f97daab7a6 QObject: restore flags printing in dumpObjectTree()  
Restored printing of Qt3-style information from dumpObjectTree().  
  
* 2fb0135efa QSize/QPoint: add toSizeF/toPointF()  
Added toSizeF().  
  
* 5dc570f8b1 QLine/QMargins: add toLineF/toMarginsF()  
Added toLineF().  
  
* c52ebb3aba QRect: add toRectF()  
Added toRectF().  
  
* 94addad4dd Add QLatin1StringView as an alias for QLatin1String  
Added QLatin1StringView as an alias for QLatin1String.  
  
* 4cf299eb5b QSettings: port API from QString to QAnyStringView keys  
Keys can now be passed as QAnyStringView (was: QString). The most  
efficient way to pass literal keys is now "key"_L1, the backwards-  
compatible way is QStringLiteral("key").  
  
* 76db8a0b1b Use QLatin1StringView in QString/QLatin1String APIs and  
docs  
Made QLatin1StringView the recommended name for referring to a Latin-1  
string view (instead of QLatin1String).  
  
* af875e88f4 FreeType: Load multiple font faces from the same file on  
macOS  
Fixed a bug where the macOS FreeType backend would fail to load font  
faces from font files containing multiple faces.  
  
* 7d8150da4c QVariant: disable building from arbitrary pointers  
QVariant used to be constructible by raw pointers through a conversion  
towards bool. This is now illegal. If such a conversion is needed, users  
are advised to insert manual casts to bool.  
  
* 80b6bcc385 Short live Q_CONSTINIT!  
Added macro Q_CONSTINIT.  
  
* a0a2bf2d95 Update bundled zlib to version 1.2.12  
zlib was updated to version 1.2.12.  
  
* a3f7dd5260 Allow brace initialization for some of QLatin1StringView  
constructors  
The (const char *, qsizetype) and (const char *, const char *)  
constructors are no longer explicit.  
  
* 9e1a2b4603 We do in fact support 'F' format for floating-point values  
Documented existing support for 'F' format when converting floating-  
point numbers to strings in QLocale::toString(), hence equally for  
QString's floating-point formatting. Previously it was supported but the  
documentation neglected to mention it; it only differs from 'f' for  
infinities and NaN.  
  
* 61157c8354 QBuffer: fix writing more than two GiB of data  
Fixed silent data truncation when writing more than two GiB at once on  
64-bit platforms.  
  
* a6657bef40 QPropertyBindingSourceLocation: fix BiC in source_location  
ctors  
(Windows only) Fixed a binary-incompatibility where source_location  
constructors were missing in the ABI.  
  
* 4bc85b9850 QBuffer: fail early in seek() beyond QByteArray's max  
capacity  
Fixed silent data corruption on 32-bit platforms when seek() fails due  
to position > INT_MAX.  
  
* a00a1d8806 QByteArray/QVarLengthArray: add missing resize(n, v)  
overloads  
Added resize(n, ch) overload.  
  
* 8aa3cf21da Add literal operators for QString/QByteArray to  
StringLiterals namespace  
Added literal operators for _s and _ba for QString and QByteArray  
respectively in the Qt::Literals::StringLiterals namespace.  
  
* b2233f19c9 Annotate QMutex with TSAN annotations  
QMutex now has annotations for ThreadSanitizer.  
  
* 69555b364d QTimeZone: add construction from std::chrono::time_zone*  
QTimeZone can now be constructed from a std::chrono::time_zone pointer.  
  
* 9c028b0ff4 XmlStringRef: fix length truncation  
Fixed several bugs regarding handling of documents larger than 2Gi  
characters on 64-bit platforms.  
  
* 0a17a0da61 QDateTime: add support for std::chrono::duration arithmetic  
QDateTime now supports arithmetic between QDateTime objects and  
std::chrono::duration objects. A duration can be added to or subtracted  
from a QDateTime, yielding another QDateTime; and two QDateTime objects  
can be subtracted from each other, yielding the duration between them.  
  
* ef895869b4 QVarLengthArray: add missing (size, value) ctor  
Added (size, value) constructor.  
  
* 2e29f55f76 QDate: add conversions for std::chrono calendaring classes  
QDate (and therefore QDateTime) is now constructible using the  
year/month/day/week classes available in the std::chrono library.  
Moreover, it now features conversions from and to std::chrono::sys_days.  
  
* 7de83f06c1 QDateTime: add conversions for time_point and zoned_time  
QDateTime can now be constructed from std::chrono::time_point objects  
(including local_time), as well as from std::chrono::zoned_time objects.  
Moreover, they can be converted to std::chrono::time_point using  
system_clock as their clock.  
  
* da0f72ebb8 QEvent: start to de-inline copy ctor and clone() of all  
subclasses  
Fixed missing clone() reimplementations on QCloseEvent, QIconDragEvent,  
QShowEvent, QHideEvent, QDragEnterEvent, and QDragLeaveEvent.  
  
* 41a7546789 QDate(Time): add a addDuration method  
Added addDuration().  
  
* 86321a0deb Upgrade PCRE2 to 10.40  
PCRE2 has been updated to 10.40.  
  
* 9eb090d683 Add support for unwrapping QFuture<QFuture<T>>  
Added QFuture::unwrap() for unwrapping the future nested inside  
QFuture<QFuture<T>>.  
  
* 7fa2a1a479 Remove last traces of old Harfbuzz  
Fixed an issue where setting the legacy environment variable  
QT_HARFBUZZ=old would cause text to disappear from the application.  
  
* 3aef84d600 qhashfunctions.h: add std::hash specialization for  
QByteArrayView  
Added std::hash specialization.  
  
* 383368a321 Support test-case selection based on global data tag  
When specifying what tests to run on a QtTest command-line, it is now  
possible to include a global data tag in the same way as a function-  
specific data tag or in combination with it. Thus if the test reports  
itself as tst_Class::function(global:local), command-line option  
function:global:local will select that specific test and function:global  
will run all data-rows for the function on the given global data tag.  
  
* 7a7f2547f3 Return more specific entries before less in  
QLocale::uiLanguages()  
uiLanguages() now prefers more specific locale names over less specific  
ones, matching its own documentation, except where the system backend  
supplies them in some other order. This means a translation with the  
expected script and/or territory as well as language will be used in  
preference to a generic one for just the language, rather than only as a  
fall-back when the more generic one is missing.  
  
* e48b4d2b7c Implement support for '0b' prefix in toInt() etc  
The string-to-integer conversion functions (toInt() etc) now support  
the 0b prefix for binary literals. That means that base = 0 will  
recognize 0b to mean base = 2 and an explicit base = 2 argument will  
make toInt() (etc) skip an optional 0b.  
  
* 34242f843e Deprecate _qs and _qba literal operators in favor of _s and  
_ba  
Deprecated _qs and _qba literal operators for QString and QByteArray in  
favor of _s and _ba in the Qt::Literals::StringLiterals namespace.  
  
* 7905b624fd QTextStream: fix streaming of char16_t's  
Added op<<(char16_t).  
  
* 9b3885248b QTextStream: complete char16_t support  
Added op>>(char16_t&).  
  
* acfbe3b779 CMake: also allow building tools when found elsewhere in  
host builds  
QT_BUILD_TOOLS_WHEN_CROSSCOMPILING has been deprecated in favor of  
QT_FORCE_BUILD_TOOLS. The latter can be used in combination with  
QT_FORCE_FIND_TOOLS and QT_HOST_PATH to use tools from a host Qt even  
for a non-cross build and still build the tools.  
  
* a1903eb941 QPolygon: add toPolygonF()  
Added toPolygonF().  
  
* d9be9fedfb Add a clear action to QKeySequenceEdit  
Added a clear action to QKeySequenceEdit to be able to remove existing  
hotkey configurations.  
  
* ff053b39a3 Fix int/qsizetype mismatches in qstring.h  
Fixed result truncation mod INT_MAX in fromStdSstring(),  
fromStdU16string(), fromStdU32string(), and fromStdWstring().  
  
* 9af1f3557a Add option to not include native libraries in APK  
Adds option for Unbundled deployment, where native libraries are not  
packaged in the APK.  
  
* da4957c99b CMake: Pick first non-free team id for iOS Xcode projects  
A non-free Xcode team id is now preferred for project signing.  
  
* a3917126e8 CMake: Automatically use Xcode generator in qt-cmake + iOS  
qt-cmake now defaults to using the Xcode generator when targeting iOS  
projects.  
  
* a2255a3ab2 CMake: Ensure creation of a unique iOS bundle identifier  
The build system tries to create a unique bundle identifier based on  
the team id if no organization prefix can be retrieved from Xcode  
preferences.  
  
* 55a4d35dc3 FatalSignalHandler: remove call to qEnvironmentXxx from  
handler code  
QtTest will now check the value of the environment variable  
QTEST_PAUSE_ON_CRASH in QTest::qRun(), so if a test wants to modify this  
variable, it must do so from the main() or initMain() functions, not in  
the test itself (including initTestCase()).  
  
* 3d9e56aa6c FatalSignalHandler: chain back to the original crash  
handler  
On Unix, the QtTest code to handle Unix/POSIX fatal signals will now  
call back to the original handler that was installed, if there was one.  
This allows logging frameworks (such as Android ART's), for example, to  
log the crash too. Additionally, if there was no handler, the  
application should exit with the correct signal instead of SIGABRT.  
  
* d88da0b2b0 Update Harfbuzz to version 4.2.1  
Updated the Harfbuzz code included with Qt to version 4.2.1.  
  
* 9bad4be214 QStringConverter: use the QUtf8 codec when Windows is using  
UTF-8  
Fixed support for using Qt applications with UTF-8 as the system  
codepage or by enabling that in the application's manifest.  
  
* d83441340c QKeySequence: Add missing modifier names  
Added missing modifier names  
  
* 734c9f2df2 Expand QColorTransform  
Added QColorTransform::isIdentity() method. Added  
QImage::colorTransformed() transitive method.  
  
* d9b9cded92 Doc: Fix documentation for vulkan licenses  
Vulkan API Registry is available not only under MIT License, but also  
Apache License 2.0. Make this explicit in the license documentation.  
  
* 5adaa8d868 Add painter render hint for brush pattern transformation  
In Qt 5, the predefined brush patterns would always be transformed  
along with the object being painted. In Qt 6.0 onwards, they would or  
would not, depending on the SmoothPixmapTransformation render hint.  
Instead of this somewhat surprising behavior, make the default be  
untransformed (i.e. cosmetic), which makes sense when it comes to dpr  
scaling. For the cases where one wants scaling, a new render hint is  
introduced to enable that: NonCosmeticPatternBrushes.  
  
* 474792a751 QCOMPARE/QVERIFY: fix huge pessimisation in QTestResult  
Optimized successful QCOMPARE and QVERIFY for an up to 2x speedup.  
  
* 343e0ff485 Add QCOMPARE_{EQ,NE,LT,LE,GT,GE}()  
Add QCOMPARE_{EQ,NE,LT,LE,GT,GE}() macros. These new macros behave  
similarly to QVERIFY(a op b), where 'op' is ==, !=, <, <=, >, >=  
respectively, but print a formatted error message with argument values  
in case of failure. The formatting is done lazily, which means that the  
strings will be generated only when the comparison fails.  
  
* cc6d984390 Add QTRY_COMPARE_{EQ,NE,LT,LE,GT,GE}_WITH_TIMEOUT()  
Add QTRY_COMPARE_{EQ,NE,LT,LE,GT,GE}_WITH_TIMEOUT macros that  
repeatedly execute QCOMPARE_{EQ,NE,LT,LE,GT,GE} until either the  
comparison returns true or the timeout expires. Also add  
QTRY_COMPARE_{EQ,NE,LT,LE,GT,GE} macros that simply invoke the  
*_WITH_TIMEOUT versions with the usual timeout of five seconds.  
  
* 0681a2dd5a QTestLib: rework QTest::compare_helper()  
QCOMPARE now evaluates toString() on its arguments lazily, speeding up  
the general case where the comparison doesn't fail. This is true for the  
QCOMPARE functionality provided by Qt. If you specialized qCompare() for  
your own types, then you need to change its implementation in line with  
Qt's own qCompare() specializations in order to enable this feature.  
  
* 782fbe0f63 The new signal pendingConnectionAvailable is added to  
QTcpServer  
New signal pendingConnectionAvailable is emitted when a new connection  
is added  
  
* d631e581c0 Unify QSslServer from QtWebSockets and QtHttpServer into  
QtNetwork  
Unify QSslServer from QtWebSockets and QtHttpServer into QtNetwork  
  
* 8aacf83a76 Make Q_ASSUME() an expression (was: statement)  
Q_ASSUME() now expands to an expression (was: statement).  
  
* 97d7042c45 Fix font rendering when Qt is configured with -no-harfbuzz  
Fixed font layouts when Qt was configured without Harfbuzz.  
  
* 763fb35d9d CoreText: Fix fonts with synthetic stretch  
Fixed a bug where synthetically stretched fonts would get the wrong  
advances and sometimes glyphs would be clipped.  
  
* df1beb422a Add support for painting at integer DPR with downscale  
Added experimental support for always painting at an integer device  
pixel ratio (rounding the DPR up if necessary), followed by a downscale  
to the target DPR.Enable by setting QT_WIDGETS_HIGHDPI_DOWNSCALE=1 and  
QT_WIDGETS_RHI=1.  
  
* 980395c764 Long live the ICU-based QStringConverter interface!  
QStringConverter and API using it now supports more text codecs if Qt  
is compiled with ICU support.  
  
* 91cb059e3d xcb: fix missing initialization of m_cursor  
Fixed crash when no monitorInfo is available (e.g. VNC).  
  
* e58a29bdae Use CSS classes on html list items for checkbox support  
Checkbox list items can now be read and written in both HTML and  
Markdown, including conversions.  
  
* 841f04f309 QPromise: run continuation(s) on destruction  
QFuture now runs its continuations when its associated QPromise has  
been destroyed. Previously, if a QFuture was canceled because the  
associated QPromise has been destroyed, its continuations were skipped.  
  
* 00d8c8114f moc: remove unnecessary emission of "#include  
<qbytearray.h>"  
moc no longer emits an #include for QByteArray in the output file. None  
of the content that moc generates needed that header, so this should not  
cause changes for most people. However, codebases that #include'd the  
moc output (something that is recommended) could be depending on this  
indirect include.  
  
* d4db1ef7db Emit autolinks in QTextMarkdownWriter  
QTextMarkdownWriter now writes an autolink whenever a hyperlink has no  
custom text and no tooltip, including when the document was parsed from  
Markdown containing a naked URL.  
  
* 3757e14cfd wasm: enable sql/sqlite for non threaded builds  
Enable sqlite for non threaded builds  
  
* be3f589d17 Apply ScaleFactorRoundingPolicy to QT_SCREEN_SCALE_FACTORS  
The high-DPI scale factor rounding policy (settable with  
QGuiApplication::setHighDpiScaleFactorRoundingPolicy() or  
QT_SCALE_FACTOR_ROUNDING_POLICY) now applies to scale factors set with  
QT_SCREEN_SCALE_FACTORS.  
  
* 100c4cd130 Make it possible to check the accepted state of touch  
events in tests  
QTouchEventSequence::commit() now returns a bool so that tests can  
check whether the event was accepted during delivery.  
  
* b98b683bdc Always update QPalette resolve mask, regardless of QBrush  
change  
Always update resolve mask in QPalette::setBrush, even if the value of  
brush has not changed.  
  
* 591d8b4cc0 Windows: Turn on dark mode support by default  
Dark mode, both for the window frames and for the palette, is now  
supported by default. It can be turned off (partially or entirely) by  
setting the QPA parameter "darkmode=0" (no dark mode support) or  
"darkmode=1" (darkmode support only for the window frames).  
  
* 866d63f659 QMetaType: fix QMetaTypes for non-const references  
Made meta types for non-const references fail to compile. Previously,  
QMetaType::fromType allowed this to compile, but returned the meta type  
for the base type, which was incorrect. Const references are understood  
to be the same as the base type.  
  
* 513c8f63aa SQLite: Update SQLite to v3.39.2  
Updated SQLite to v3.39.2  
  
* d052236a2f CMake: Add QT_ANDROID_SIGN_AAB variable  
Added the QT_ANDROID_SIGN_AAB variable that can be set to ON to enable  
signing of .aab packages.  
  
* 17f0d47413 QDBusTrayIcon: add xdg-activation support  
StatusNotifierItem tray implementation supports getting window focus  
token from desktop environments supporting the ProvideXdgActivationToken  
extension (e.g. KDE)  
  
* 9fd40c04d1 QHttp2Configuration: in QNAM, use old, higher values in  
flow control  
Stream receive window that HTTP/2 protocol in QNAM is using increased  
to 214748364 octets (from the previous 64K) not to throttle download  
speed. Clients, working with servers, not accepting such parameters,  
must set HTTP/2 configuration on their requests accordingly.  
  
* 347c9e2b58 RCC: fix zlib compression when --no-zstd was specified  
Fixed a bug that caused rcc not to compress files with any compression  
algorithm if the --no-zstd option was present.  
  
* b0cadd5ed2 Fix crash when setting override cursor on multiple clients  
Fixed a crash when setting an override cursor on multiple clients.  
  
### qtdeclarative  
* 576fafd1e6 Pass qmldir to qmlcachegen, qmllint and qmltc, not the  
qmltypes file  
qmllint expects qmldir files, not qmltypes files to be passed via the  
-i option now. This enables it to see the imports and dependencies of  
the module being imported. For backwards compatibility it still accepts  
qmltypes files, with a warning.  
  
* 867698300a Make atlasing of compressed textures opt-in again  
Disable atlasing of compressed textures by default. Can be enabled with  
QSG_ENABLE_COMPRESSED_ATLAS=1  
  
* 13399bd54d Replace currentFile(s) with selectedFile(s)  
FileDialog's currentFile and currentFiles properties have been  
deprecated. The selectedFile and selectedFiles properties now refer to  
the currently selected file(s), as well as the final selection.  
  
* f73e294472 Remove the qml_sequence_object feature flag  
The qml_sequence_object feature flag has been removed. Omitting  
sequences from the QML language does not make much sense now that we use  
them for lists of value types. The original reason to allow it was that  
the sequence support took up a lot of space in the binary. This is not  
the case anymore since 6.0.  
  
* 2ffed97aac qmllint: Offer suggestions for typos  
qmllint will now automatically suggest fixes if it thinks a component,  
property or binding was not found due to a typo.  
  
* 8d93470858 Better handle requesting no-vsync and make this usable with  
threaded  
In addition to setting the swapInterval to 0 in the QQuickWindow's  
QSurfaceFormat, one can now also set the QSG_NO_VSYNC=1 environment  
variable to achieve the same (applies globally to all Quick windows in  
the application). The threaded render loop can now recognize that one or  
more windows have vsync-based throttling disabled explicitly, and if so,  
it will fall back automatically to using system timers to advance  
animations in order to prevent animations from running too fast when the  
presentation rate is not throttled by vsync.  
  
* 23249c6f51 sg: Add logic in threaded loop to recognize the lack of  
proper vsync  
The threaded render loop of Qt Quick can now potentially recognize that  
the graphics stack in a particular system is broken and does not provide  
vsync-based throttling. This can now automatically trigger falling back  
to using regular system timers to advance animations. (meaning one does  
not need to manually switch over to the 'basic' render loop or  
explicitly disable vsync on the window) Note however that this does not  
affect render thread animations (the so-called animators, such as  
XAnimator). Those will continue to advance based on the presentation  
rate no matter what.  
  
* 3fc68053db Use qt.qml.states logging category instead of  
STATECHANGE_DEBUG env  
The new qt.qml.states logging category is useful for debugging states  
and transitions. It replaces the STATECHANGE_DEBUG environment variable.  
  
* 5a908de8b7 Allow custom named value types in QML  
You can now add your own value types to QML modules. This works exactly  
like the registration of object types, just with Q_GADGET instead of  
QObject/Q_OBJECT. In turn, the QtQuick value types are only available  
from QtQuick now. Previously you could declare unusable properties of  
QtQuick value types when only importing QtQml. This is not possible  
anymore.  
  
* b0fc028cb5 QML: Allow named lists of value types  
You can now use lists of value types in QML. For example a property of  
type list<int> will hold a list of integers.  
  
* 7efcb0e349 Update and enhance the animation driving info in scenegraph  
docs  
The Qt Quick scenegraph documentation is now covering the topic of  
driving animations, how it is implemented in the different render loops,  
and what one needs to be aware when it comes to vsync and performance.  
  
* 5ca8cf28f9 QML: Soften the ctor check on type registration  
Registering types without suitable constructors or types with  
inaccessible attached objects is deprecated.  
  
* a0f5baad2a scenegraph: Enable arrays of combined image samplers  
Added support for arrays of combined image samplers per binding.  
  
* 0f0987c160 QtQuick: Add proper QInputMethod singleton  
Qt.inputMethod can now also be accessed via the InputMethod singleton.  
This allows you to use QInputMethod in a way supported by tooling and  
the compiler.  
  
* abe854b0cc QQuickTreeView: add expandRecursively()  
New function "expandRecursively()" has been added to TreeView.  
  
* 060e0b2cd1 QQuickTreeView: add collapseRecursively()  
New function "collapseRecursively()" has been added to TreeView.  
  
* 160190968d scenegraph: Add support for polygon fill mode  
Added support for polygon rasterization mode to graphics pipeline  
state.  
  
* c013439598 QQuickTreeView: add expandToIndex()  
New function "expandToIndex()" has been added to TreeView.  
  
* ee143fe27d qquickapplication: Add styleHints property  
Qt.styleHints should now be accessed as a property of QQuickApplication  
via Application.styleHints  
  
* b18fb72e7f QQuickTableView: refactor mapping functions from  
QQuickTreeView  
Added a set of functions to get the model index for a cell, and vice  
versa.  
  
* 7e1512c741 QQuickTableView: implement scrollToCell()  
Added a new property "animate" that can be set by the application to  
control if animations should be used for positioning the content item.  
  
* a398e06c61 qmllint: Support automatically applying suggestions  
Added the ability to automatically fix some warnings, use -f to  
automatically fix your files or add --dry-run to see what changes would  
be made first.  
  
* 38c09704e2 QQuickTableView: implement PositionMode, deprecate usage of  
Qt::Alignment  
The function positionViewAtCell() now takes TableView.PositionMode  
instead of Qt.Alignment as the second argument. For backwards  
compatibility, Qt.Alignment can still be used.  
  
* 8308f9f443 Port QQuickShaderEffectSource format to Qt 6  
ShaderEffect and Item layers can now request using a floating point  
texture format for their backing texture. ShaderEffectSource::format has  
been revised with values that have an actual effect on the underlying  
texture.  
  
* 43b7e1f745 QQuickTableView: add "Visible" and "Contain" to  
PositionMode  
Two new PositionModes added: "Visible" and "Contain". Those can be used  
in a call to positionViewAtCell() to ensure that a cell is visible in  
the view.  
  
* 3fd49c82cf Respect invokable toString() methods  
You can now override the JavaScript toString() method by providing a  
Q_INVOKABLE method of the same name in your QObject-based C++ classes.  
  
* de1672713a QQuickTableView: implement support for currentIndex  
Two new properties are added, keyNavigationEnabled and  
pointerNavigationEnabled, that lets the user navigate the current index  
around in the table. A 'required property bool current' can also be set  
in the delegate to style the item that is current.  
  
* 7c9276d38b qmllint: Integrate plugin infrastructure  
qmllint can now be extended via plugins. Use --plugins to get a list of  
available plugins.  
  
* 8e867653d8 QQmlApplicationEngine: Add a more convenient error signal  
Added objectCreationFailed signal as a more convenient way to check for  
errors than objectCreated.  
  
* 2fb43a35df Invalidate text when application fonts are added or removed  
Fix multiple issues with usage of application fonts when they are added  
or removed during the lifetime of the application.  
  
* 7e24db7464 QQuickTableView: add new function: cellAtPosition()  
cellAtPos(pos) is now deprecated in favor of cellAtPosition(pos). The  
latter will assume pos to be relative to the contentItem.  
  
* 10e359fa0b Improve layouts in terms of efficiency and stability  
Improved layouts in terms of efficiency and stability. Due to this,  
properties reflecting size hints, such as implicitWidth, implicitHeight  
and Layout.minimumWidth etc are not immediately updated anymore, they  
are postponed until the next polish event.  
  
* 5c04d17428 CMake: Add _qmllint_json target  
The --json option now has a mandatory file argument and writes its  
output there. You may also pass "-" to write it to stdout.  
  
* 43f705c3c0 Support to custom the render target on the software  
renderer  
Added QQuickRenderTarget::fromPaintDevice, Allowed to set the render  
target of QQuickWindow on the software renderer.  
  
* 39635d0254 QtQmlCore: Add SystemInformation singleton  
Add SystemInformation singleton.  
  
* 0b12dd572d QQuickTableView: add currentRow and currentColumn  
Two new properties are added: currentRow and currentColumn.  
  
* 44dd79eeda Allow modifying from, to, duration and easing properties  
during animation  
It is now possible to set the from, to, duration, and easing properties  
of a top-level animation while it is running. The animation will take  
the changes into account on the next loop.  
  
* bcc0f4fb1c Add setMirrorVertically for QQuickRenderTarget  
Added QQuickRenderTarget::setMirrorVertically, Allowed to control the  
mirror vertically of render target.  
  
* cfbc5ecf2a QML: Correctly detect extended types  
A derived type is no longer considered to be extended itself when only  
its base type is extended. Instead, the extension only exists on the  
base type.  
  
* 7fa03450cf QML: Add an option to bind components to files  
You can now bind components to a file scope. This way you can make sure  
IDs in the file are accessible to the components.  
  
* 7b535d22d6 Give Dialogs and Menus focus by default  
Dialogs and Menus now have their focus property set to true by default.  
Popups are unchanged, meaning that popups that should be interacted with  
via keyboard (including cancelling) should have focus set to true or  
forceActiveFocus() called on them after opening.  
  
* 1c680287ff Use regular key events for cancelling popups  
Popups no longer handle the Escape and Back keys by grabbing them as  
shortcuts, instead they are treated as regular events. This also means  
that popups that should be closable with the Escape or Back keys must  
have focus.  
  
* 8ef0407ddd QQuickTableView: add a new 'alternatingRows' property  
Added a new property 'alternatingRows', which is a hint to the delegate  
to alternate between rows.  
  
* 1df2cf6bad Allow specifies the native texture format on  
QQuickRenderTarget  
Added an overload for QQuickRenderTarget::fromOpenGLTexture to allow  
specifying the format of the OpenGL texture.  
  
* 065fb60786 QQuickTableView: add a 'subRect' argument to the  
positionViewAtCell() functions  
A new argument 'subRect' has been added to positionViewAtCell().  
  
* 1234a59a4d Add ColorDialog to QtQuick.Dialogs  
Added ColorDialog. This is a native dialog on platforms that support  
it, and a non-native Qt Quick ColorDialog on platforms that don't.  
  
* c98c2c08a5 QQmlDebug: reliably print the debugger warning  
The warning about enabled debuggers is now printed when at least one  
translation unit in the final executable requests it, independent of the  
order in which translation units are linked/initialized.  
  
* 86fae5664c Remove qmltc compilation command in favor of  
qt_add_qml_module()  
The qmltc compilation functionality provided by  
qt6_target_compile_qml_to_cpp() is merged into qt6_add_qml_module()  
command and is available through ENABLE_TYPE_COMPILER argument. The  
qt6_target_compile_qml_to_cpp() function does nothing and is left only  
to highlight that users must migrate away from it.  
  
* 36c6c1ea57 QtQuickTest: add API for checking for polish at window  
level  
Added QQuickTest::qIsPolishScheduled(QQuickWindow *) and  
QQuickTest::qWaitForPolish(QQuickWindow *) functions for verifying that  
updatePolish() was called on one or more items managed by a window.  
  
* 8353f84141 FileDialog: make selectedFile writable  
FileDialog's selectedFile property can now be set to an initially  
selected file.  
  
* 7dba66ab70 QQuickTableView: add new property 'selectionBehavior'  
A new property 'selectionBehavior' has been added that specifies if the  
user should be able to select rows, columns, or cells.  
  
* dda364c148 Canvas: Add support for specifying a size when saving to an  
image  
Canvas.save() now takes an optional size argument, which sets the size  
of the image to save, and sets DPR=1.  
  
* 6f6db238d4 Fix TextEdit/TextArea mouse cursor shape handling logic  
TextEdit and TextArea now set their own mouse cursors more  
consistently, but without regard for any external call to setCursor().  
  
* 79650395b0 QQuickAbstractDialog: emit rejected() on mere close()  
QtQuick dialogs now emit rejected() on a mere close(), too.  
  
* c9df284c19 Fix SplitView containmentMask hit testing  
SplitView now correctly handles mouse events when using  
containmentMask.  
  
* c135dbf522 Let Controls inherit palettes and fonts from parents  
Controls now inherit palette and font from parents.  
  
* 2118b7eb42 Deal with markdown fragments in TextEdit  
TextEdit.insert(), append(), copy(), paste() etc. are now working with  
MarkdownText.  
  
* f385c327ee Fix fractional scaling of text in Qt Quick  
Fixed a kerning issue with native-rendered text when there is a  
fractional system scale factor set.  
  
* baa3958645 TextInput/Field: selectByMouse default=true, but not on  
touchscreens  
The selectByMouse property is now enabled by default, but no longer  
enables selecting by dragging your finger across text on a touchscreen.  
Platforms that are optimized for touchscreens normally use special text-  
selection handles, which interact with Qt via QInputMethod.  You can opt  
out of the behavior change by using an import version < 6.4.  
  
* 0fa0fa27b8 TextEdit: selectByMouse default=true, but not on  
touchscreens  
The selectByMouse property is now enabled by default, but no longer  
enables selecting by dragging your finger across text on a touchscreen.  
Platforms that are optimized for touchscreens normally use special text-  
selection handles, which interact with Qt via QInputMethod.  You can opt  
out of the behavior change by using an import version < 6.4.  
  
* b7e84d06d8 Fix precedence between JS and QML scopes  
The precedence between imports and locally defined functions and  
variables in JavaScript files has been fixed. If you import a JavaScript  
file from a QML file, the functions inside the JavaScript file should  
obviously override anything imported from the QML context. This behavior  
has been restored.  
  
* dfd6170ebb TextArea: selectByMouse default=true, but not on  
touchscreens  
The selectByMouse property is now enabled by default, but no longer  
enables selecting by dragging your finger across text on a touchscreen.  
Platforms that are optimized for touchscreens normally use special text-  
selection handles, which interact with Qt via QInputMethod. You can opt  
out of the behavior change by setting the environment variable  
QT_QUICK_CONTROLS_TEXT_SELECTION_BEHAVIOR=old.  
  
* 2b42c90c37 Fix TextInput and TextField mouse/touch selection fallback  
behavior  
The selectByMouse property is now enabled by default, but no longer  
enables selecting by dragging your finger across text on a touchscreen.  
Platforms that are optimized for touchscreens normally use special text-  
selection handles, which interact with Qt via QInputMethod.  You can opt  
out of the behavior change by setting the environment variable  
QT_QUICK_CONTROLS_TEXT_SELECTION_BEHAVIOR=old.  
  
### qtmultimedia  
* b18358310 Doc: Mention third-party code  
Qt Multimedia now optionally contains code from Eigen 3.4.0, pfft, and  
Resonance Audio. Identified licenses of Eigen are Mozilla Public License  
2.0 and BSD 3-Clause "New" or "Revised" License. Pfft is available under  
a BSD 3-Clause "New" or "Revised" License. Finally Resonance Audio is  
available under Apache License 2.0.  
  
### qttools  
* b6db42d80 qdoc: Allow parameters for the \include command  
QDoc now allows extra parameters for the \include command to customize  
the quoted content.  
  
* f4c623deb Rename QML basic types to value types  
QML value types are now marked with the \qmlvaluetype directive, rather  
than \qmlbasictype. \qmlbasictype still works but is deprecated. So far,  
all value types are hardcoded into the QML engine, making the directive  
irrelevant for user projects. This will change.  
  
* 89fef3e06 Qt Designer: Enable the QWebEngineView, QQuickWidget plugins  
on Windows  
Qt Designer now sets the Graphics API to OpenGL in order to enable the  
QWebEngineView and QQuickWidget plugins.  
  
* c866539dd Qt Designer: Add abstract widget base classes  
The abstract base classes of Qt Widgets have been added for  
promotion/custom widget usage.  
  
* 8b4dab1e4 lupdate: Allow multiple specifiers after method signature  
lupdate does not trip anymore over tr() calls in methods with multiple  
specifiers. For example "QString MyClass::foo() const noexcept" now gets  
the correct context.  
  
### qtdoc  
* 5e8eaeb9 Remove "Generic Linux (x86, x64)" as supported desktop  
platform  
Linux x86 (Desktop) was removed from the list of officially supported  
platforms. We only provide binaries for Linux x64 since a while, and  
also do not actively test native builds on x86 Linux anymore.  
  
### qtsensors  
* 233475da Make geomagnetic mode the default magnetometer behavior  
The default magnetometer behavior is changed to be geomagnetic mode.  
  
### qtconnectivity  
* e91c7bc3 Don't stop BT LE server advertisement when first client  
connects  
Continue BT LE server advertisement after first client connects  
  
* 44d474a0 QtNFC: Add PSCSLite/winscard backend  
Added support for accessing smartcards using readers supporting PC/SC  
specification on Linux, macOS and Windows.  
  
* 99923601 Windows: implement the missing APIs for QBluetoothLocalDevice  
Add support for correctly emitting deviceConnected() and  
deviceDisconnected() signals, as well as return a valid list of  
connectedDevices().  
  
* d58d134d Introduce error codes for missing permissions  
Various error enums are extended with new error codes that represent  
missing permissions error. Error descriptions are also updated, when  
available.  
  
### qtwayland  
* dff57914 client: Fix crash on shutdown on Mesa driver  
Fixed a crash on shutdown that could happen with some graphics-heavy  
applications when running on Mesa drivers.  
  
* 00323844 Use opaque render list when client content is opaque  
The compositor now respects the opaque region set by the client and no  
longer applies blending or overdraw for fully opaque windows.  
  
* 64875f37 QWaylandBufferRef: fix relational operators  
Two const QWaylandBufferRefs can now be compared for equality (before,  
the LHS was not allowed to be const).  
  
* 6d8e7567 Allow multiple client buffer integrations to initialize  
Enabled support for multiple client buffer integrations without the  
need to set the QT_WAYLAND_IGNORE_BIND_DISPLAY environment variable.  
  
* 4910b7ad Clear keyboard modifier state when application deactivates  
Fixed a bug where keyboard modifiers would get stuck if the compositor  
was running nested inside e.g. X11 and then ALT-TAB was used to switch  
to a different application. This would cause shortcuts to misbehave.  
  
* 256c89e6 Compositor: Re-enable touch events for Wayland clients  
Fixed a bug where multi-touch would not work with Qt Wayland  
Compositor.  
  
* 487de472 client: Avoid protocol error with invalid min/max size  
Fixed an issue where setting an invalid minimum and maximum size on a  
window would cause some compositors to raise a protocol error.  
  
### qtimageformats  
* 0c8d5dc Update bundled libwebp to version 1.2.2  
Update bundled libwebp to version 1.2.2  
  
* 372ff59 Update bundled libtiff to version 4.4.0  
Bundled libtiff was updated to version 4.4.0  
  
* 3bd3228 Update bundled libwebp to version 1.2.4  
Update bundled libwebp to version 1.2.4  
  
### qtserialbus  
* 26062ef QModbusDevice: introduce an InvalidResponseError error code  
Introduce a new InvalidResponseError error code. Use this code instead  
of UnknownError when QModbusClient fails to parse the response.  
  
* 6620839 Make pduFromStream work on big endian (again)  
Fix reading from stream on big endian systems  
  
### qtwebsockets  
* cc4c24b Add support for WebSocket Sub-Protocols  
Add support for WebSocket Sub-Protocols  
  
* 5e94911 QWebSocketServer: update handshake timeout to keep up with  
QSslServer  
Due to the introduction of a standalone QSslServer, with its own  
timeout handling, the setHandshakeTimeout() function now applies the  
same timeout to both the TLS and WebSocket handshakes separately.  
  
### qtwebengine  
* c3ae834aa Add charset parsing to custom scheme handler's content type  
Charset is now explicitly parsed from provided contentType  
  
* 82357352b Introduce "--webEngineArgs" to prevent unexpected sub-  
process args  
Command line arguments meant for webengine has to be now stated after "  
--webEngineArgs" option.  
  
* 4c4ac0df9 Introduce http status code domain for loading info  
Added HttpStatusCodeDomain for http status code range of errors  
  
* 196ec015c Add NavigateOnDrop settings  
NavigateOnDropEnabled added, enabled by default.  
  
* 05d82c353 QPdfView: replace enums with enum classes  
All enums are replaced with enum classes.  
  
* 6769bd154 Move QPdf namespace enums into QPdfDocumentRenderOptions  
enum classes  
The QPdf namespace is removed.  
  
* 90f43fd25 Rename QPdfNavigationStack to QPdfPageNavigator; QML type  
too  
The PdfNavigationStack QML type has been renamed to PdfPageNavigator,  
matching the C++ type QPdfPageNavigator. These remember navigation  
history within a document, and are helpful to implement back/forward  
buttons similar to those on a web browser in both Qt Quick and widget-  
based viewer applications.  
  
* 0de16e9a2 Redefine PdfSearchModel.currentResult as document-based; use  
PdfLink  
PdfSearchModel.currentResult is now the result index within the whole  
set of search results rather than on currentPage; and changing  
currentPage no longer makes currentResult change. In the views, this  
means the current highlighted search result stays on the same page even  
when the user views a different page.  
  
* fd39e1eee Add link role to QPdfLinkModel, providing a QPdfLink  
instance  
PdfLinkModel now provides a QPdfLink object for each link. QPdfLink now  
contains everything necessary to render delegates for links and search  
results, and handle clicking links; and there is a copyToClipboard()  
method for use in context menus, which will copy the text returned trom  
toString(), which is also invokable.  
  
* 66aca3c84 Add PdfLinkDelegate instead of link decoration style  
properties  
A PdfLinkDelegate will now be instantiated on top of each hyperlink in  
the PdfMultiPageView, PdfScrollablePageView and PdfPageView components,  
for event handling and to provide tapped() and contextMenuRequested()  
signals. It is non-visual by default, but can be customized, for example  
to draw underlines under hyperlinks if the PDF documents are not  
expected to have them already.  
  
### qtvirtualkeyboard  
* 4395ca0f Port qtvirtualkeyboard to declarative type registration  
Virtual Keyboard extension mechanism was replaced with QML modules.  
Previously the virtual keyboard was using plugin mechanism with custom  
interface to load extensions. With the introduction of declarative type  
registration, this interface became obsolete. All of the existing  
virtual keyboard extensions are now registered as standard QML modules,  
loaded implicitly by the QtQuick.VirtualKeyboard module. This change  
does not impact the users of the virtual keyboard public API.  
  
### qtremoteobjects  
* e0269f5 Fix race condition when accessing invalid index  
Fix race condition when accessing invalid index  
  
### qtquick3d  
* f317a5ba Apply Occlusion map to global ambient light as well  
Occlusion maps now also affect the indirect lighting provided by  
punctual light's ambientColor  
  
* b0e71adb Adapt to moving of type registrations into the Qt namespace  
The QML type registrations for the QtQuick3D and QtQuick3D.Particles3D  
modules used to be public. This was an accident. As you cannot  
meaningfully call them anyway, they have been moved to private headers.  
  
* 8c6c6d20 Remove asset plugin for the UIP format  
Support for converting UIP files has been removed, as it has become  
less and less feasible to maintain a reasonable conversion path from the  
old 3D Studio format.  
  
* 5694a02b Add cubemap support for custom material/effect textures  
Added CubeMapTexture, a Texture subtype that allows exposing a cubemap  
from a KTX container to custom material and effect shaders.  
  
* 3656afdb Allow specifying the View3D backing texture format  
Added the renderFormat property that, as a counterpart to renderMode,  
allows specifying the backing texture's format when the View3D is  
rendering to a texture instead of directly targeting the window.  
  
### qt5compat  
* 0ba059c Port remaining graphical effects to Qt 6  
Added back missing Qt 5 effects: Blend, DirectionalBlur, DropShadow,  
GaussianBlur, Glow, InnerShadow, MaskedBlur, RadialBlur, RecursiveBlur,  
and ZoomBlur.  
  
### qtopcua  
* 0b657f3 OpcUA: Fix attribution of Open62541  
Complete list of licenses in opengl62541 files: MPL-2.0, CC0-1.0, CC-  
BY-SA-4.0, BSD-3-Clause, Apache-2.0, and MIT  
  
### qthttpserver  
* f04a680 HTTPS support  
Https support added to QAbstractHttpServer class  
  
* 52bce52 Fix memory leak in QHttpServerRequest  
Fixed: memory leak in QHttpServerRequest  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-98843 Qt 6.2.2 Windows build fail  
* QTBUG-96463 [REG 5.15.2-6.2.0] Text with BIDI controls is underlined  
incorrectly  
* QTBUG-86052 wasm: Calling setWindowIcon() has no effect on a QDialog  
* QTBUG-99165 cmake doesn't complain with android-30, but fails with  
unknown API S (ie android-31)  
* QTBUG-98408 QTextDocument is limited to `@media screen`when calling  
setHtml()  
* QTBUG-99223 CMake Error: File  
C:/Users/qt/work/install/lib/cmake/Qt6/qt_setup_tool_path.bat.in does  
not exist.  
* QTBUG-97752 QHash: non-readonly iteration access destroys iterator  
* QTBUG-96916 Qt 6 breaks compatibility of QVariant streaming into  
QDataStream  
* QTBUG-91739 Performance regression on QHash::insert() and  
QHash::remove()  
* QTBUG-81503 qtbase contains code that isn't allowed to be distributed  
* QTBUG-98901 QtConcurrent::run crashes on program exit  
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
* COIN-777 *** Could not find any device matching '--platform iOS  
--minimum-deployment-target  
* QTBUG-99413 QSysInfo::productType() incorrectly documented  
* QTBUG-85295 QSettings will still fall back onto any child groups  
specified in the fallback entries even if fallbacks are turned off  
* QTBUG-63695 QStandardPaths does not document locations for QNX  
* QTBUG-99316 Yocto build fails in CI for qtdeclarative-native dev/6.3  
branch  
* COIN-728 Logging categories no longer enabled when re-running failed  
tests  
* QTBUG-99416 QT6 qtbase build fails claiming symlinks are present  
* QTBUG-99148 Broken html list rendering because <code> element  
* QTBUG-99192 tst_qquickpixmapcache Failed  
* QTBUG-99572 Do not replace nbsp characters when creating text/plain  
mime data  
* QTBUG-92445 Markdown smashes nested formatting inside lists  
* QTBUG-97841 MacOS Monterey - scrolling issues with touch pad  
* QTBUG-99623 Dependency update on qt/qtopcua failed in 6.3  
* QTBUG-99633 [autotests] tst_QIcoImageFormat should be behind a feature  
flag  
* QTBUG-99522 qmake adds @ mark after then the output file name when it  
calls g++ on either Qt's MinGW or MSYS2 platform  
* QTBUG-99548 Qt6 CMake target compile options propagation (CUDA)  
* QTBUG-99676 markdown (and html) import/export should not rely on use  
of a fixed-pitched font to remember a `monospace` span  
* QTBUG-99640 Reg->6: QByteArray::append(const char *str, qsizetype len)  
crashes if len < 0  
* QTBUG-99111 wasm: cursor is wrong after resizing window  
* QTBUG-99605 XCB: QGuiApplication::primaryScreen() always last screen  
* QTBUG-99710 Regression: QCache crash  
* QTBUG-99224 Crash in QPixmapCache  
* QTBUG-99240 Crashing in trimming QPixmapCache  
* QTBUG-99408 [SQL] The SQL driver for Firebird/Interbase does not  
unpack the QVariant before null check  
* QTBUG-98471 [REG: 5->6.2.1] Null QDateTime is not stored as NULL  
anymore in Oracle OCI  
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
* QTBUG-95661 Test result counts are incorrect  
* QTBUG-99668 Using QDateTime with QTimeZone specified asserts in debug  
build  
* QTBUG-99630 tst_QShortcut::text is flaky in dev  
* QTBUG-99771 Porting guide does not mention binary JSON  
* QTBUG-92358 One More Crash in text shaping on special string with  
EmojiOneColor font.  
* QTBUG-89155 Assertion violation in text shaping on special string with  
EmojiOneColor font.  
* QTBUG-99472 "Pick Screen Color" button in QColorDialog doesn't scan  
secondary screen colors in Windows  
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
* QTBUG-99949 Cannot do unthrottled Present with D3D  
* QTBUG-99803 QVulkanWindow doesn't enable any device features (e.g.  
VkDeviceCreateInfo::pEnabledFeatures)  
* QTBUG-97950 Application slowly reads every file in /usr/bin before  
starting  
* QTBUG-96718 Crash in inBindingWrapper() (Creator built against Qt 6.2  
build)  
* QTBUG-99534 tst_qfuture memleaks  
* QTBUG-100067 network/torrent examples ProgressBar text should be  
layout with horizontal  
* QTBUG-95309 Compile fails with Qt in namespace and C++20  
* QTBUG-100118 QStaticByteArrayMatcher cannot match beyond INT_MAX  
* QTBUG-100072 Building Qt from source fails to compile with C++20  
standard enabled when using MSVC 2022  
* QTBUG-100144 Dependency update on qt/qtwebchannel failed in dev  
* QTBUG-98316 QTimer on Windows uses excessive power for timers  
* QTBUG-100107 QByteArray::isLower() is completely different from  
QString::isLower() , ditto isUpper()  
* QTBUG-100037 QSqlQuery: crash on executing query if connection is  
already closed  
* QTBUG-99066 Since QT6.2.1 Painted Widgets / Text is less "anti  
aliased"  
* QTBUG-100233 Android broken project/wrong libraries linked when adding  
UiTools  
* QTBUG-100074 Building QSharedMemory fails when bootstrapping  
* QTBUG-87136 Animations run twice as fast on a 120hz Android device  
* QTBUG-93823 Android QPlatformScreen does not expose the refresh rate:  
Animations (and timers) too fast on higher refresh rate monitors  
* QTBUG-94959 Timer and animations runs faster after screen touch event  
on Android 11  
* QTBUG-93393 Android A11Y TalkBack: Hidden onPressAction still called  
* QTBUG-62185 QVersionNumber seems broken on -O1 and higher with g++  
* QTBUG-69216 Android: tst_QFontDatabase::condensedFontMatching fails  
* QTBUG-89011 test runner is unable to run only initTestCase()  
* QTBUG-95842 testlib's autotest compilation fails with glibc 2.34  
* QTBUG-100071 QtFuture::connect fails to compile if the passed signal  
takes a std::tuple as argument  
* QTBUG-100294 RHI Direct3D11 fails to build with MinGW-w64 v8  
* QTBUG-100315 FEATURE_headersclean does not work with if  
CMAKE_CXX_FLAGS contains more than one option  
* QTBUG-99637 Windows with D3D or Vulkan: stretch effect is not ideal  
when resizing QQuickWindow  
* QTBUG-94608 Nonsensical full path to examples  
* QTBUG-100317 QMacStyle code references missing image resource  
* QTBUG-97929 CMake warnings in FindGLIB2.cmake  
* QTBUG-44096 QNetworkAuthenticationManager does not emit  
authenticationRequired when using NTLM  
* QTBUG-98253 Failed to build from source through clang-cl 13.0.0  
* QTBUG-93432 QGraphicsTextItem font gets incorrectly clipped when a  
clip rect is set on the painter.  
* QTBUG-34673 qmake prints 'Access is denied' when it actually can't  
find the .pro file  
* QTBUG-100416 QPluginLoader::loadHints return "no hints set" but by  
default PreventUnloadHint is set  
* QTBUG-100324 QHelpEvent::globalPos() returns frequently a wrong value.  
* QTBUG-99846 [autotests] tst_qlogging uses wrong helper path on webOS  
* QTBUG-99707 QML plugins have wrong RUNPATH  
* QTBUG-100432 [REG 6.2.3->6.3.0] QML/quick examples  not launching when  
compiled from command line  
* QTBUG-99954 [autotests] tst_QResourceEngine fails on webOS  
* QTBUG-97157 attempting to interact with any widget dialog on  
touchscreen fails; mouse causes crash after that  
* QTBUG-100290 Custom build fails with PCH  
* QTBUG-100493 QtFinishPrlFile.cmake: No such file or directory with  
multi-config build on Linux  
* QTBUG-100327 CompositionMode_Screen wrong with drawImage  
* QTBUG-100482 Network monitoring not working when ZScaler Internet  
Security is active  
* QTBUG-100441 [REG 6.2.1->6.3.0] Designer not launching on macOS x64  
* QTBUG-100518 Crash on iOS 13.3.1  
* QTBUG-100364 QStandardPaths GenericDataLocation for iOS seems to  
mention wrong path  
* QTBUG-93402 Android A11Y TalkBack: Focus Rect not updated on  
orientation Change  
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
* QTBUG-100654 tst_QRhi fails on webOS  
* QTBUG-88137 tst_QTimeLine fails on Android  
* QTBUG-96212 The visibility of placeHolderText of the QPlainTextEdit is  
not reevaluated in the setter  
* QTBUG-100494 QMdiSubWindow does not respect size constraints  
* QTBUG-100695 Document QProcessEnvironment::Initialization enum  
* QTBUG-100438 Incorrect rounding to ms in QTimer when clock too coarse  
* QTBUG-51327 [Windows 8.1]: After maximizing a window and toggling the  
frameless window hint and moving to another monitor then the window can  
be too big  
* QTBUG-100545 Nested QML items with Accessible properties set does not  
work on Android  
* QTBUG-100217 [REG 6.2.2  -> 6.2.3] Integer overflow when rendering svg  
image  
* QTBUG-87405 tst_QFontDatabase::systemFixedFont fails for Android  
* QTBUG-88136 tst_QFutureWatcher fails on Android  
* QTBUG-100775 Several data races around handlers of  
QDesktopServices::openUrl()  
* QTBUG-100546 QIODevice::readAll() Truncates Data To Max Int  
* QTBUG-100867 QFile::copy error string is uninformative  
* QTBUG-87400 tst_QAbstractItemView fails on Android  
* QTBUG-87408 tst_QTreeView has failing tests  
* QTBUG-100574 qtbase/src/gui/vulkan/qvulkanfunctions_p.cpp is missing  
dependency on qvkgen tool  
* QTBUG-100817 AVX build failure on intel skylake  
* QTBUG-100261 QPrinter property setup not effect  
* QTBUG-99504 Linux: QPrinter::setDuplex not effective ( Canon  
imageRUNNER 2520  )  
* QTBUG-100915 moc code generates warning [-Wredundant-parens]  
* QTBUG-100651 Unable to follow HTTP/2 redirects  
* QTBUG-100559 wasm: Linking commands too long for Windows  
* QTBUG-101065 fatal error: 'zconf.h' file not found  
* QTBUG-52472 Undefined Behaviour in qsimpledrag.cpp line 207  
* QTBUG-45045 SIGFPE in QQuickMenu  
* QTBUG-87404 tst_QGridLayout::minMaxSize fails on Android  
* QTBUG-100796 qt_internal_add_test calls don't handle extra properties  
for Android  
* QTBUG-84466 startSystemMove and startSystemResize does not enable aero  
snap on windows with frameless window.  
* QTBUG-100693 WebAssembly (WASM) MEMORY control fixes  
* QTBUG-101082 [REG 6.3 -> 6.4] Build error with UBSAN  
* QTBUG-101172 Android help from configure-cmake-mapping.md seems  
outdated (or wrong)?  
* QTBUG-100155 deprecated-declarations warning in  
examples/widgets/widgets/icons  
* QTBUG-87401 tst_QFormLayout::wrapping fails on Android  
* QTBUG-87674 qaccessibility fails on Android  
* QTBUG-101020 tst_QPlugin::scanInvalidPlugin fails on QNX  
* QTBUG-100802 [REG 6.2.2->6.2.3]Checkable QPushButton does not visually  
display checked state when toggled on macOS  
* QTBUG-101297 REG->6.3: Default-constructed QPrintPreviewDialog asserts  
"!(P(max) < P(min))"  
* QTBUG-100537 Can not build Qt 6 with cmake when preferring package  
configuration  
* QTBUG-69064 Android: tst_QFrame::testPainting fails  
* QTBUG-101300 QFlags: Missing some bitwise xor operators with  
QT_TYPESAFE_FLAGS  
* QTBUG-101294 tst_qflags doesn't compile with QT_TYPESAFE_FLAGS  
* QTBUG-101302 [REG 6.2.3 -> 6.3.0] QGuiApplication leaks memory  
* QTBUG-101306 enum-enum warning in qxcbwindow.cpp is genuiune  
* QTBUG-100299 Android: Unloaded multimedia plugins  
* QTBUG-87389 tst_QDialog::snapToDefaultButton fails on Android  
* QTBUG-95957 Scaled pixmap with ellipse clipping leaves lines in output  
* QTBUG-100329 Clipping glitches when painting with fractional scaling  
* QTBUG-100343 MDI subwindows leave artifacts when moving/resizing with  
fractional scaling  
* QTBUG-101299 QCOMPARE() doesn't compile for certain QFlags<T> with  
QT_TYPESAFE_FLAGS  
* QTBUG-90990 Drop down widget get left behind if dialog window is moved  
* QTBUG-88803 Native keyboard always popup on Android  
* QTBUG-101198 Build failure on qsimd.cpp  
* QTBUG-101399 QTest::toString() doesn't compile for certain QFlags<T>  
with QT_TYPESAFE_FLAGS  
* QTBUG-100873 REG->6.3b1/Windows with system clock offset: Assert when  
instantiating QDateTimeEdit  
* QTBUG-101028 argv passed to Android apps is not sufficiently  
terminated  
* QTBUG-93505 Unable to retrieve the swiped Filedialog  
* QTBUG-100795 QWeakPointer d pointer is private  
* QTBUG-101441 wasm: native keyboard not working on iOS  
* QTBUG-101286 [Regression] QNetworkReply::finished() is not emitted if  
an error occurs.  
* QTBUG-101411 QT_WARNING_DISABLE_* macros do not work under QCC (8.3.0)  
* QTBUG-101381 QtScxml: Fix compiler warnings for QNX  
* QTBUG-101415 QtPositioning: Fix compiler warnings for QNX  
* QTBUG-101384 QtRO: Fix compiler warnings for QNX  
* QTBUG-101382 QtBase: Fix compiler warnings for QNX  
* QTBUG-101304 Compile tst_qflags both with and w/o QT_TYPESAFE_FLAGS  
* QTBUG-28379 QFileDialog: aliases to folders disabled  
* QTBUG-67576 QAbstractSocket::setSocketOption() has no effect if called  
before QAbstractSocket::connectToHost()  
* QTBUG-101013 QQuickFileDialog does not work on Android  
* QTBUG-101581 Crash when zooming invalid image  
* QTBUG-101177 QTimer random segmentation fault (SIGSEGV)  
* QTBUG-101551 wasm multiple "use after free" in  
QNetworkReplyWasmImplPrivate::doSendRequest  
* QTBUG-100154 deprecated-declarations warning in  
examples/network/secureudpserver/server.cpp  
* QTBUG-94366 Backslash is converted to double forward slash in  
configure on Windows  
* QTBUG-100670 QDockWidgetGroupWindow effectively sets new dockarea  
permissions on qdockwidget  
* QTBUG-101592 Qt should load libvulkan.so.1, not libvulkan.so  
* QTBUG-100562 The characters ("_") in qtdbus-index.html links to  
qromancalendar.html  
* QTBUG-101609 Font "Bahnschrift" reports wrong style names  
* QTBUG-101610 Font "Alef" reports wrong style names and renders  
incorrectly  
* QTBUG-100790 tst_QInputDevice::multiSeatDevices() fails on Wayland  
* QTBUG-95067 WASM: Quick Window is bigger than browser frame on mobile  
browsers  
* QTBUG-98755 QIconEngine::IconNameHook disappeared  
* QTBUG-93499 Signal parameter MOC handling error with gcc 10  
* QTBUG-100770 Old Qt version mentioned in Qt6.3.0 qtbase documentation  
* QTBUG-101620 QOpenGLWidget does not update when content changed while  
its hidden  
* QTBUG-100870 QtTestLib's blacklisting doesn't take global data tags  
into account  
* QTBUG-101474 setClipRect() after setClipRegion() call doesn't change  
clipping region  
* QTBUG-87407 tst_QTableView has failing tests for Android  
* QTCREATORBUG-24600 some clicks in call stack don't register  
* QTBUG-101723 Configure failure with linux-clang-libc++  
* QTBUG-98369 [macOS] Qt internal warning when FontMetrics is used  
* QTBUG-99216 QMessageBox with Japanese characters gives "Missing font  
family" warning on macOS  
* QTBUG-101745 Running qmake on iOS build fails on macOS 12.3 Monterey  
* QTBUG-89545 CMake: on macOS (w/ framework build) the module includes  
the binary  
* QTBUG-101718 [REG 6.3.0beta2->beta3] quick3d/principledmaterial not  
launching on macOS  
* QTBUG-101775 Don't add framework directories as include paths  
* QTBUG-101869 tst_QOpenGL fails on webOS  
* QTBUG-101651 Random crashes in QGraphicsScene  
* QTBUG-101897 The 'movie' example should only build if  
'QT_FEATURE_movie' is available  
* QTBUG-101456 QTabBar::setTabTextColor does not change color when  
QPalette::Base background role is used  
* QTBUG-101916 Build Qt 6.3.0 beta2 / beta3 for Android fails only on  
Windows  
* QTBUG-101753 FTBFS because of -Werror=attribute and "retain attribute  
ignored" warning on rcc/uic/etc build  
* QTBUG-100821 tst_qimagereader fails on Windows 11 21H2  
* QTBUG-98477 tst_QWidget::enterLeaveOnWindowShowHide is flaky in QtBase  
with Windows 11  
* QTBUG-69242 Android: tst_QTextDocument::task240325 fails  
* QTBUG-100470 Undetected test crashes on Android  
* QTBUG-100666 FreeType font backend fails to select font style when a  
single font file contains multiple font faces  
* QTBUG-75172 Wrong documentation for Qt::ItemDataRole expected types  
* QTBUG-101647 Selected item in QTreeWidget cannot be dragged when CTRL-  
key is pressed  
* QTBUG-101145 Disable "Pick color" in QColorDialog when unavailable  
* QTBUG-101653 Windows/MinGW 9/Qt 6.2.3: Step into Qt source code does  
not work  
* QTBUG-88934 [Reg 5.15 -> 6] QFrame in the menu isn't drawing  
* QTBUG-101284 QPromise destructor doesn't transition to canceled state  
if it wasn't start()-ed  
* QTBUG-102041 Android multi-abi builds don't work if the Android  
ndk/sdk install path is different from the CI's one  
* QTBUG-101423 tst_QPlainTextEdit::ensureCursorVisibleOnInitialShow is  
crashing on Android  
* QTBUG-101321 tst_QDialog::dialogInGraphicsView crashes on Android  
* QTBUG-99747 QDate::startOfDay( ) leads to assert in debug build  
* QTBUG-101996 Android Qt file system fails to communicate with some  
content provider app (like Google Drive)  
* QTBUG-87422 tst_QAtomicInt::alignment fails on Android  
* QTBUG-87431 tst_QThreadStorage::crashOnExit fails on Android  
* QTBUG-87427 tst_QFileSystemModel::specialFiles fails on Android  
* QTBUG-101992 QDomDocument silently erases empty CDATA section  
* QTBUG-87418 tst_QStringConverter::convertUtf8 fails on Android  
* QTBUG-102064 binary_for_strip cannot be found on installed qtbase  
* QTBUG-87414 tst_QLocale::initTestCase fails on Android  
* QTBUG-99624 REG->6: Android: Fullscreen does not cover the navigation  
bar area  
* QTBUG-53290 QWindowsPrintDevice::defaultPrintDeviceId() may crash,  
when no printers are installed  
* QTBUG-102066 SDK version detection does not ignore stderr  
* QTBUG-70564 QT_NO_SIGNALS_SLOTS_KEYWORDS/QT_NO_KEYWORDS are  
undocumented  
* QTBUG-99020 -Wnull-pointer-subtraction when compiling  
qtdeclarative/src/qml/qml/ftw/qintrusivelist_p.h:244:69  
* QTBUG-87385 tst_QNetworkProxyFactory::genericSystemProxy fails on  
Android  
* QTBUG-87390 tst_QScreen has tests  failing for Android  
* QTBUG-97103 REG: 5.15.0->5.15.1: Under some circumstances the  
performance of an application on Windows when switching application  
focus  
* QTBUG-95114 When accessibility is made active after the start up of an  
application then it will trigger an update of all existing controls to  
update roles and names  
* QTBUG-100997 Regression and UI Freeze (5.15 -> 6.2) in QTableView with  
Accessibility  
* QTBUG-101283 QThread does not indicate that an event dispatcher is  
created in start()  
* QTBUG-101307 tst_qbytearrayview fails to compile with ubsan  
* QTBUG-102181 [Reg 6.2.3->6.2.4] Painting issues when scrolling in code  
editor  
* QTBUG-101758 REG[6.2.3->6.3] native QMessageBox crash on Android  
* QTBUG-97482 QPushButton with QMenu does not work on Qt6  
* QTBUG-102171 On 64-bit platforms, QBuffer::write(ptr, 2GiB + 1)  
incorrectly reports success  
* QTBUG-101038 Wrong physical DPI  
* QTBUG-99484 Android - QML Camera freezes app  
* QTBUG-102202 [REG:6.2.3->6.2.4]: Cannot use c++latest with qmake and  
MSVC  
* QTBUG-75386 QComboBox Selected Entry Color is incorrect on macOS  
* QTBUG-102249 QSplitter: Handle moves in non-pressed state too  
* QTBUG-87671 Android tests crashing with  
"java.lang.UnsatisfiedLinkError: dlopen failed: invalid ELF file"  
* QTBUG-101217 tst_qmessagebox has failing tests for Android  
* QTBUG-102157 QDateTime asserts on MSVC 2019 / C++20  
* QTBUG-102274 QBuffer silent data corruption on seek() past INT_MAX  
(32-bit only)  
* QTBUG-100312 androidtestrunner: A test with XPASS does not return  
error  
* QTBUG-102067 REG: QHash reserve endless loop with size < currently  
used one  
* QTBUG-96213 QProxyStyle::deleteLater() does not delete the QProxyStyle  
* QTBUG-101361 Mac: File Dialog filters different category than selected  
* QTBUG-102366 When filling a rect on a screen that has 150% scaling  
then it is possible that a line of pixels is not filled in  
* QTBUG-102199 QLocale::toDateTime asserts  
* QTBUG-101460 QTimeZone::displayName ignores locale on Android  
* QTBUG-102327 Address sanitizer caught heap-use-after-free in  
tst_QWidget::deleteWindowInCloseEvent  
* QTBUG-102358 Using system pcre2 fails when using pcre2 with cmake  
* QTBUG-100173 tst_qquickwidget fails on Android  
* QTBUG-100135 40000 chips example - zoom in/out buttons do not work  
* QTBUG-92269 Build claims to be done when it isn't, unnecessary  
rebuilds of Core after touching bootstrap source files  
* QTBUG-100297 QXdgDesktopPortalFileDialog::openPortal() does not set  
current_name  
* QTBUG-102246 windows arm64 broken QAtomicPointer ctor/copy/move  
* QTBUG-102431 QBENCHMARK triggers compiler warning  
* QTBUG-100039 QPlainTextEdit scrolls to cursor on alt-tab on ubuntu  
* QTCREATORBUG-26628 Switching from Creator to other window changes  
scroll position in editor  
* QTBUG-102484 Race condition in QSemaphore  
* QTBUG-102438 Drag/drop of "text/plain" does not work,  
QMimeData::text() returns an empty string  
* QTBUG-99136 QDockWidget not correctly parented/setup if dragged from  
another floating and tabified QDockWidget  
* QTBUG-101347 QMainWindow Menu / actions sometimes not displayed when  
performing long operations  
* QTBUG-99810 [REG: 5.15.5->5.15.6] xcb: Dock widgets disappear if  
trying to float them from QMainWindow that contains native window  
* QTBUG-69515 Linux, WindowStaysOnTopHint does not work.  
* QTBUG-73485 Issue with Qt::WindowStaysOnTopHint  
* QTBUG-81341 Window won't receive events above Gnome Dock despite  
X11ByPassWindowManager + WindowsStaysOnTop is set  
* QTBUG-102005 [wasm] Canvas not painted initially  
* QTBUG-102720 sha1.cpp is missing in the copy of bootstrap sources.  
* QTBUG-102744  QML items with Accessible properties set does not set  
properly for Android  
* QTBUG-102083 Switching between app windows breaks IME  
* QTBUG-101278 Chinese text input issues on macOS 12.x  
* QTBUG-102334 QSettings / QDateTime incompatible when switching from  
Qt6 -> Qt5  
* QTBUG-102495 Content-Length is always placed at the end of the Header  
part.  
* QTBUG-102592 Setting a common CMAKE_STAGING_PREFIX breaks build rpaths  
of non-qtbase repositories  
* QTBUG-98785 Button menu pops up at wrong position on a  
QGraphicsProxyWidget  
* QTBUG-102718 Crash when restoring a QDockAreaLayout  
* QTBUG-102541 crash when restoring QMainWindow state when screen scale  
has changed  
* QTBUG-101963 [Reg 5.15 -> 6.x] -platform linux-g++-32 now produces  
64-bit libraries  
* QTBUG-102269 Test cases can't be called with a global data tag  
* QTBUG-102584 Drag and drop always assumes to have [NSWindow  
contentView] with drag drop API  
* QTBUG-101320 Apps targeting Android 12 or higher must explicitly  
declare the android:exported attribute for app components  
* QTBUG-102607 macdeployqt: errors when producing a universal binary  
(universal binary)  
* QTBUG-101175 Can not build Qt 6.2.3 with cmake and ClangCl (clang-cl)  
due to missing `_mm_cvtps_ph`  
* QTBUG-102821 Global variable found in qeglfsx11integration.cpp  
* QTBUG-102750 Some highlighted examples are crashing at startup on  
embedded devices  
* QTBUG-102796 QLocale::uiLanguages() has wrong order  
* QTBUG-38971 QtActivity did not call through to  
super.onConfigurationChanged() on orientation change (crash)  
* QTBUG-102298 Android: Switching navigation bar between buttons /  
gestures hides qml elements  
* QTBUG-100950 wasm: enter and leave events do not happen  
* QTBUG-99691 Starting QtService causes black screen  
* QTBUG-102628 Application will crash if setWindowsIcon with a big ICON  
* QTBUG-102952 tst_QNetworkReply::autoDeleteReplies* tests are flaky  
* QTBUG-103000 [Reg: 5.15->6.3.0] Q_EMIT does not wait for slots to  
return on FreeBSD  
* QTBUG-101150 static initialisation fiasco with initializeWindowManager  
* QTBUG-102782 QPushButton setEnabled(false) doesn't grey out button  
* QTBUG-100059 Objective-C usage can result in undefined behavior  
* QTBUG-102717 [REG Qt 6 -> Qt 6] QGraphicsView Artifacts  
* QTBUG-103085 QVersionNumber doesn't indicate its type in QDebug output  
* QTBUG-97533 QMenu pops up on wrong screen  
* QTBUG-103003 [Windows] Warning - Unable to open default EUDC font:  
"EUDC.TTE"  
* QTBUG-103009 QML performance regression when accessibility is active  
* QTBUG-75106 Entries in the QAccessiblePluginsHash should be removed  
when a QQuickWindow is deleted  
* QTBUG-102820 [REG 5.15.2 => 6.2.4] Styled indicators not drawn in  
itemviews  
* QTBUG-102493 [REG 6.2.2 -> 6.2.3] Keyboard layout resets to English  
* QTBUG-102640 [REGRESSION] Keyboard layout not respected for *some* key  
combinations  
* QTBUG-95933 Using scanner input IRcode will result in an error when  
second character is uppercase  
* QTBUG-103084 Hover events are not receivable in embedded QWindow  
(macOS)  
* QTBUG-102190 Calling showNormal after show does not make windows  
normal in WebAssembly  
* QTBUG-102877 "-static" and "-feature-relocatable" cause extra 'bin'  
directory in various qmake paths  
* QTBUG-99335 Documentation for QtAndroidPrivate is wrong  
* QTBUG-102242 Wasm drag and drop support: asyncify: dropping results in  
browser getting drop event  
* QTBUG-103245 Configure fails when specifying -no-freetype  
* QTBUG-102960 iOS: input panel shows wrong suggestions  
* QTBUG-103370 REG: Qt does not build without Freetype  
* QTBUG-103356 [REG 6.3->6.4] Android arm64 and armv7 binary size  
increased  
* QTBUG-97813 Namespace with "enum" at its begining not being properly  
handled  
* QTBUG-102489 segfault in qsql_mysql.cpp cleanup with icx  
* QTBUG-103002 linker error with qmake projects on static linux Qt6  
build  
* QTBUG-95468 XCB: Memory leak of QXcbScrollingDevicePrivate for a  
device that is not a mouse  
* QTBUG-100351 [REG 5.12 -> 6.2] Pasting an image in Windows is not  
converted to a QImage correctly.  
* QTBUG-98003 InputMethod hides soon with ShiftModifier.  
* QTBUG-102866 [REG 5.12.3->6.2.1] Horizontal part of subcontrol-  
position of menu-indicator is ignored  
* QTBUG-102374 [REG:5.15.7->5.15.8]: repaint() on a widget makes  
QGraphicsOpacityEffect apply multiple times  
* QTBUG-102747 -DQT_GENERATE_WRAPPER_SCRIPTS_FOR_ALL_HOSTS=ON on windows  
generates windows line endings for unix script  
* QTBUG-99487 QHeaderView state incompatible between Qt5/6  
* QTBUG-100515 tst_qtextmarkdownwriter fails on QNX  
* QTBUG-100981 tst_QTextMarkdownWriter::fromHtml(preformats with  
embedded backticks) fails on Wayland  
* QTBUG-101031 markdown fenced code blocks end with unnecessary blank  
lines  
* QTBUG-94557 Menu causes touch failure  
* QTBUG-98519 [REG: 5.15.0->5.15.7] xcb: Synthesized mouse from touch  
gets stuck if receiving widget gets destroyed  
* QTBUG-102751 Can not receive touch event after the widget that  
WindowFlags is Qt::Popup is closed on ubuntu20.04  
* QTBUG-103706 Synthesized touch event not recognized with Widgets  
* QTBUG-100833 Default iOS project to both iPhone and iPad deployment  
* QTBUG-93268 target_link_libraries does not work with a target name on  
iOS  
* QTBUG-95381 CMake library install target does not copy binaries on iOS  
* QTBUG-87198 Configuring example targeting iOS with CMake + Xcode  
generator fails  
* QTBUG-103719 Crash in tst_qquicktext::implicitSize on macOS  
* QTBUG-102999 QtConcurrent::blockingMapped behavior changed since Qt5  
if the output container does have a non-explit size c'tor  
* QTBUG-102758 Application always starts on wrong screen  
* QTBUG-102637 [REG 6.2.4 -> 6.3.0] No fake screen created without  
xrandr, Qt aborts  
* QTBUG-103741 Signals carrying smart pointers to const QObject fail to  
compile  
* QTBUG-103576 [REG] Broken Qt::TextAlignmentRole  
* QTBUG-102134 QSplitter when hidden sets replaced widgets as hidden  
* QTBUG-103001 Implicit conversion loses integer  
* QTBUG-103603 [REG 5.15.2-6.2.4] Broken country flag emoji in RTL text  
* QTBUG-103742 QVectorIterator & QMutableVectorIterator CamelCase  
headers missing  
* QTBUG-88869 QAuthenticator hard-coded to HTTP in SPNEGO/Negotiate  
* QTBUG-101681 tst_QPointer::threadSafety() is flaky (probably race  
condition)  
* QTBUG-103745 QPainter::drawText method truncates inputs  
* QTBUG-103319 makeCurrent() needed inside of resizeGL()  
* QTBUG-97537 Fix failing line-break and word-break tests  
* QTBUG-69715 QKeySequence::toString() returns garbage strings for some  
simple QKeySequence  
* QTBUG-40030 Special keys like Shift are not named in  
QKeySequence::toString.  
* PYSIDE-1942 pyside6-uic python list support  
* QTBUG-103605 qfilesystemmodel.cpp fails to compile on Windows with  
oneAPI icx using c++20  
* QTBUG-103493 dev branch fails to build  
* QTBUG-103590 QKeySequenceEdit: not blocking quit on Mac  
* QTBUG-103852 QDir fails for paths of length over 260 characters  
* QTBUG-81674 Unexpected detach on setColorTable after  
QImage::QImage(const uchar *data, ...)  
* QTBUG-103740 QTemporaryFile::rename does not document that it can only  
rename, not copy+delete like QFile::rename  
* QTBUG-93298 Windows: Application hangs (or crashes) on quit while  
QtQuick FileDialog is open  
* QTBUG-102302 qprint_p.h defines file-static const arrays, but is  
included in many TUs  
* QTBUG-103984 QWindowsDialogHelperBase calls QThread::terminate()  
* QTBUG-104053 tst_QFile fails on webOS  
* QTBUG-103974 Wasm: unused functions in qtestcase.cpp, wasm framework  
doesn't build when cross-compiling on Mac  
* QTBUG-103733 [Windows] setProcessDpiAwarenessContext(DPI_AWARENESS_CON  
TEXT_PER_MONITOR_AWARE_V2) failed on certain machines  
* QTBUG-98988 Qt bugs when portal implementation is not available  
* QTBUG-103922 Calling QThread::terminate() in destructor causes double  
object destruction  
* QTBUG-103894 Configuring fails on Manjaro Linux  
* QTBUG-104123 "configure -no-pkg-config" doesn't turn off pkg-config  
* QTBUG-104056 Conan: qmlimportscanner: No such file or directory  
* QTBUG-88519 androiddeployqt doesn't know about Conan's build path  
* QTBUG-89588 androiddeployqt fails with error from qmlimportscanner if  
qtdeclarative is not installed  
* QTBUG-103836 Fusion menu text with mnemonic clipped on Windows  
* QTBUG-94481 [REG 5.15.2 -> 6.1.1] Ellipsis in the worst possible place  
* QTBUG-49704 QLoggingCategory::installFilter crashes with the code from  
documentation  
* QTBUG-100361 No font rendering at all when configured with -no-  
harfbuzz  
* QTBUG-103838 QFontMetrics::horizontalAdvance() does not seems to give  
correct value  
* QTBUG-56893 Closing a dialog via mouse click on a button causes an XCB  
error  
* QTBUG-98417 Bundling translation file of plist does not work with  
XCode 13  
* QTBUG-103455 Settings don't work with content:// URL on Android  
* QTBUG-100093 Deployed third party library points to the original  
location  
* QTBUG-101161 Android Assets awfully slow to be loaded  
* QTBUG-88799 WASM - No hover on the whole GUI  
* QTBUG-104261 tst_qstringconverter::roundtrip() ASAN error stack-use-  
after-scope  
* QTBUG-102021 QCocoaScreen::UpdateScreens crash  
* QTBUG-84741 Crash on QCocoaScreen::isOnline() when calling  
CGDisplayIsOnline  
* QTBUG-104231 tst_QVulkan fails with Ubuntu 22.04 due to broken Mesa  
lavapipe included in the distro  
* QTBUG-103007 Resetting a QComboBox custom model doesn't emit  
currentIndexChanged or currentTextChanged  
* QTBUG-104320 qt_add_big_resources does not list contents of the qrc  
file in Qt Creator  
* QTBUG-101585 QMessageBox components get skipped by Windows Narrator  
* QTBUG-102768 Invalid warning message in debug builds when using  
QFont::setFamily() with comma split  
* QTBUG-103775 Downstream crash when bad index passed to insert methods  
of QBoxLayout  
* QTBUG-100188 Page layout settings are reset when QPrintDialog is shown  
if there is no printer installed on macOS  
* QTBUG-104201 QWidget: resize() after showMaximized() causes strange  
behaviour  
* QTBUG-102595 Builds can't find the projects qml modules  
* QTBUG-102395 QMainWindow::restoreState corrupts relation between  
toolbars layout item  
* QTBUG-78826 Cannot enter non ascii characters to the TextField and  
QLineEdit from browser(wasm)  
* QTBUG-102343 Windows: Only initial QScreen values are available if  
screen geometry changes between QApplication and before first window is  
open  
* QTBUG-103383 Windows: Qt doesn't respond to DPI changes if Qt window  
is having a non-Qt parent  
* QTBUG-79248 TrayIcons Menu does not scales its size when changing DPI  
* QTBUG-103375 [REG:5.15->6] Shift_JIS support for QDomDocument on Qt6  
* QTBUG-91896 QTableView span gets confused with logical indexes when  
columns are moved  
* QTBUG-104412 FAIL!  : tst_AndroidAssets during dependency update  
* QTBUG-85474 QGraphicsScene::clearSelection() may leave internal state  
inconsistent  
* QTBUG-103497 [iOS] CMake handling qt_add_big_resources() fails  
* QTBUG-104443 xcb plugin crashes when running in vnc  
* QTBUG-104419 tst_qxp_function_ref::voidReturning() AddressSanitizer:  
stack-use-after-scope  
* PYSIDE-1750 QMouseEvent.pos marked as deprecated in source but not in  
docs  
* QTBUG-104083 tst_bench_shared_ptr does not compile on Ubuntu 22.04  
* QTBUG-103992 QFuture::onCanceled is not called when promise is deleted  
* QTBUG-86790 Mingw Qt provides debug libraries in the wrong folder  
* QTBUG-104085 QJsonValue::toObject(const QJsonObject &defaultValue) and  
QJsonValue::toArray(const QJsonArray &defaultValue) parse empty default  
values incorrectly  
* QTBUG-102869 wasm: Resizing is still accessable under a modal dialog  
* QTBUG-104003 QTabBar/QTabWidget crashes when closing last tab and  
there are hidden tabs  
* QTBUG-104362 QDomImplementation::DropInvalidChars strips emoji and  
other non-BMP characters  
* QTBUG-104463 Generated qdoc sources from qtattributionscanner should  
have a different basedir so it is not appearing as version specific  
* QTBUG-93748 QT_DEPRECATED_X with Q_REQUIRED_RESULT causes warning  
C5240 in Visual Studio 16.9.5  
* QTBUG-94713 markdown writer: preserve auto-link URLs  
* QTBUG-104421 tst_qthread terminateAndPrematureDestruction() ERROR:  
AddressSanitizer: stack-buffer-underflow  
* QTBUG-53661 QDom internalSubset is never set  
* QTBUG-104396 qmake projects try to link to static qt libraries with  
hardcoded CI paths (no such file or directory)  
* QTBUG-85109 QPainter::drawImage draws images in different places  
depending on image format  
* QTBUG-104583 Buffer overrun and crash in  
QColorTransferTable::applyInverse()  
* QTBUG-103568 Android 13: Warnings when starting qt apps  
* QTBUG-103415 [Reg 6.1.3->6.2.0] Parallel Animation bug on macOS  
* QTBUG-95319 The cursor size is unstable when multiple QT_SCALE_FACTOR  
is used  
* QTBUG-92485 Q_ASSERT added in qrasterizer.cpp  
* QTBUG-24240 testlib: executing a test with an invalid data label  
doesn't count as a failure and doesn't return a non-zero exit code  
* QTBUG-104132 [REG 6.2.4->6.3.0] HTTP-Redirect is broken  
(ManualRedirectPolicy)  
* QTBUG-104484 Missing documentation for QDropEvent methods: position,  
buttons, modifiers  
* QTBUG-71900 Double tapping on a word does not show the selection  
handles in the right place after the initial selection  
* QTBUG-58503 Text Handle Cursor Position Offset Error  
* QTBUG-104383 QExpandingLineEdit::resizeToContents crashes  
conditionally in qBound (since Qt 6.3.0)  
* QTBUG-104565 QTableWidgets: crash when double click into table cell  
end that expands beyond   window  
* QTBUG-101615 QMLPATHS not documented  
* QTBUG-104205 QDockwidget screen change issue(s) more involved parts.  
* QTBUG-104501 syntax error: identifier "VkFormat"  
* QTBUG-104527 iOS: Input panel opens when you click on a QPushButton  
* QTBUG-98651 [iOS 15] Application freezes when QDialog is executed by  
button clicked() signal  
* QTBUG-104708 qmake projects try to link to static qt libraries with  
hardcoded CI paths part 2  
* QTBUG-104596 [reg->6.4] Qt Designer crashes when OpenGL widget is  
dragged to form  
* QTBUG-94066 Qt6 CMake targets for plugins missing in shared / official  
builds  
* QTBUG-104726 Build failure on x86  
* QTBUG-104232 tst_QSslKey::constructor fails with Ubuntu 22.04 and  
openssl 3  
* QTBUG-95930 QGuiApplication::setHighDpiScaleFactorRoundingPolicy()  
ignored on Linux, always acts like PassThrough  
* QTBUG-99546 QT_SCREEN_SCALE_FACTORS doesn't follow rounding policy  
* QTBUG-96283 [REG 6.1.3->6.2.0] macOS: Can not configure qml / network  
example with statically compiled Qt  
* QTBUG-103794 B2qt fails with Ubuntu 22.04: undefined reference to  
`qt_resourceFeatureZstd'  
* QTBUG-104732 Need QFutureCallOutEvent to export symbols  
* QTBUG-69354 QGtk3FileDialogHelper isn't modal  
* QTBUG-102825 Popping QML StackView Item makes a11y unusable  
* QTBUG-104734 Need several struct declarations remain in private header  
* QTBUG-104809 Crash in QKmsDevice::createScreenForConnector  
* QTBUG-103988 State of QTreeWidgetItem not announce by screenreader  
* QTBUG-104696 QFontDialog:: selectedFont and fontSelected always  
returns one font  
* QTBUG-104740 Accessibility: NVDA not narrating full state of QTabBar  
* QTBUG-98762 REGRESSION: QPalette::setBrush does not reliably detach  
* QTBUG-104867 QtTest: QCOMPARE prints matching <null>s for mismatches  
when unable to convert to string  
* QTBUG-103940 Insufficient documentation in QRegularExpression variant  
of QString::indexOf(), results in random crash bug  
* QTBUG-99990 windows: Painting an image with DPR >1.0  to a QPrinter  
does not produce correct result  
* QTBUG-101058 Pixelated images on Windows  
* QTBUG-104827 Huge APK sizes under Windows  
* QTBUG-103805 Linker error when configuring with "-sanitize fuzzer-no-  
link"  
* QTBUG-104851 qdoc: Ignore Q_WEAK_OVERLOAD  
* QTBUG-104877 wacom: QTabletEvent rotation goes to -180 when absent  
* QTBUG-103892 Stop binding to iBridge interface when unit testing  
QTcpServer on macOS  
* QTBUG-46113 tst_qcompleter fails on Ubuntu  
* QTBUG-100982 tst_QStaticText fails on Wayland  
* QTBUG-49205 tst_qnetworkreply::ioGetFromBuiltinHttp  
* QTBUG-104014 tst_QPointer::threadSafety crashed in CI  
(QBindingStorage::reinitAfterThreadMove)  
* QTBUG-98921 tst_QGraphicsWidget::initialShow is uber flaky on OpenSUSE  
* QTBUG-104493 Application performance drops if many threads are running  
while QProcess creates sub-processes on Unix  
* QTBUG-104718 fuzz: QCborValue::fromCbor out of memory error 32bit  
* QTBUG-102239 tst_QWidget::enterLeaveOnWindowShowHide is flaky  
* QTBUG-104959 QT_NO_TRANSLATION define breaks QML build  
* QTBUG-104213 Add \brief descriptions to Concurrent topics  
* QTBUG-96702 Mandelbrot example not supporting zoom  
* QTBUG-104270 cmake loads native sysroot cmake config and tries to look  
for libs  
* QTBUG-82477 QClipboard doesn't support custom mimeTypes  
* QTBUG-104875 Wacom proximity events went missing on X11 in 6.3  
* QTBUG-105002 -mno-direct-extern-access fails clang  
* QTBUG-104268  
tst_QTouchEvent::multiPointRawEventTranslationOnTouchPad() ASSERT  
failure in QList::at: "index out of range"  
* QTBUG-105140 [REG] default constuctor requirement for meta type  
(QVariant) breaks webengine api  
* QTBUG-105079 XCB crash on plugin load when HighDPI and multiple  
monitors  
* QTBUG-105078 QMYSQL: regression in formatValue of QByteArray  
* QTBUG-102879 Examples not linking to Qt::Core are installed in the  
wrong folder  
* QTBUG-104917 QStyleSheetStyle::drawPrimitive(QStyle::PE_PanelLineEdit)  
crashes with widget==nullptr  
* QTBUG-105242 [REGRESSION] After  
2f5f276b4a2a19b9f2669b84f28ce8e970aaa39f network printers are missing  
* QTBUG-104801 Crash with QPainter::drawText used on a QQuickView with a  
Text item  
* QTBUG-104951 QT_WIDGETS_RHI/QOpenGLWidget lead to crash on Wayland  
* QTBUG-104952 QT_WIDGETS_RHI/QOpenGLWidget lost transparency support on  
X11  
* QTBUG-105234 MSVC 2022 fails to compile qtbase test  
tst_qxp_function_ref.cpp  
* QTBUG-105011 QtWidgets Vulkan RHI backend doesn't support translucency  
on Wayland  
* QTBUG-105310 Using deprecated keyword breaks the build  
* QTBUG-105041 openssl 3.x 32bit platform regression  
* QTBUG-104316 Qt 6.3.1 build for arm failed: selected processor does  
not support `yield' in ARM mode  
* QTBUG-104940 post in/decrements of QBEInteger and QLEInteger return  
reference according to documentation  
* QTBUG-105160 Bad access when destroying QComboBox immediately after  
selecting item  
* QTBUG-105302 qputenv sometimes puts garbage at the end of the value  
* QTBUG-105204 QProperty: Notfication missing if binding no longer has  
any dependencies  
* QTBUG-104982 [Regression] binding stops being evaluated  
* QTBUG-105010 Font underline rendering bug  
* QTCREATORBUG-27634 Basic Layouts Example UI elemnets get squished  
* QTBUG-105323 [Regression] Keyboard is not properly hidden on ios  
* QTBUG-105393 tst_QImage::exifReadComments fails on webOS  
* QTBUG-105341 QDoubleValidator can report "Intermediate" for inputs  
that are unambiguously out-of-range  
* QTBUG-105339 Typo in since version for QStyledItemDelegate  
* QTBUG-103571 QWindowsContext::findPlatformWindowAt stuck in infinite  
loop  
* QTBUG-104774 macOS: [Enter] key in TextField generates Qt.Key_Return  
instead of Qt.KeyEnter  
* QTBUG-103473 Regression: Pressing numeric keypad Enter doesn't dismiss  
QDialog containing QLineEdit  
* QTBUG-105501 Qt6 build fails with system double-conversion  
* QTBUG-105517 Redundant "does" in QFrame  
* QTBUG-93471 Darwin linker warns about global weak symbols when linking  
an executable against a static Qt  
* QTCREATORBUG-27685 Sliders Example not scaling well  
* QTBUG-104754 manual tests that use qt_internal_add_manual_test don't  
run on iOS  
* QTBUG-105322 Reg->6.3.1: Passing a QDate to QDateEdit via constructor  
results in wrong date  
* QTBUG-105527 Vulkan validation shows (useless but annoying) "errors"  
with vkkhrdisplay  
* QTBUG-86967 tst_qfont fails on Ubuntu20  
* QTBUG-105615 Update dependencies on '6.4' in qt/qttools fails  
* QTBUG-104948 QFileDialog::getOpenFileContent not honoring nameFilter  
* QTBUG-102053 Using QMAKE_ASSET_CATALOGS in .pro (qmake) fails with  
"Unknown platform: "ios-simulator""  
* QTBUG-105687 developer-build fails for QSemaphore  
* QTBUG-105133 [REG 6.3.1] Androiddeployqt doesn't find rcc and  
qmlimportscanner  
* QTCREATORBUG-27868 Can't find qmlimportscanner when building examples  
for android  
* QTBUG-105031 a11y AT-SPI: Window-relative positions are incorrect  
* QTBUG-105042 a11y AT-SPI: Window-relative positions are wrong for  
dialogs, screen coordinates returned instead  
* QTBUG-105281 a11y AT-SPI: incorrect handling of window-relative coords  
for "GetOffsetAtPoint" (text interface)  
* QTBUG-102359  NTLM authentication crashes  
* QTBUG-105520 a11y AT-SPI: "GetCaption" result (from AT-SPI table  
interface) has incorrect D-Bus type  
* QTBUG-105092 QDockWidget cannot be re-docked if floating  
* QTBUG-105752 a11y AT-SPI: D-Bus reply for "GetAttributeValue" text  
method has incorrect format  
* QTBUG-105709 Dragging large windows is slow on WASM  
* QTBUG-105286 Crash with UpdateWindowTitle event triggered by closing a  
dialog (mac)  
* QTBUG-105264 Uncaught TypeError: self.module.qtAddCanvasElement is not  
a function  
* QTBUG-105363 Opened dialog is not refreshed until mouse button click  
on it  
* QTBUG-105814 Accessibility tools cannot find tree items inside the  
app's UI on Windows  
* QTBUG-105213 Pressing space/enter on a button with focus doesn't  
trigger its action  
* QTBUG-104925 [REG 6.4.0-beta1 -> 6.4.0-beta2] Qt no longer builds with  
-no-feature-highdpiscaling  
* QTBUG-105474 Context menu does not close when minimizing window  
* QTBUG-105810 iOS: TapHandler emits clicked, even if long pressed more  
than StyleHint::MousePressAndHoldInterval  
* QTBUG-105374 Modules in 5.15 branch missing MinGW debug files  
* QTBUG-105583 CMake deployment API generates faulty script if  
CMAKE_INSTALL_BINDIR is set to "." or ""  
* QTBUG-90504 Dark theme not respected by Fusion style  
* QTBUG-99276 Fusion style sets button text color to white automatically  
* QTBUG-105841 QtAndroid build failure with cmake 3.18.4 (qt 6.3)  
* QTBUG-104962 [REG 6.3.0 -> 6.3.1]QFileDialog does not allow changing  
column sizes nor sorting  
* QTBUG-104425 Crash when loading header state in QBittorent  
* QTBUG-105017 Crash in QRhiGles2::ensureContext with  
QT_WIDGETS_RHI_BACKEND=vulkan and QOpenGLWidget  
* QTBUG-100888 tst_QWindow::modalWindowPosition() fails on Wayland  
* QTBUG-105231 reusing editor by reimplementing  
QAbstractItemDelegate::destroyEditor causes crashing  
* QTBUG-14460 QDesktopServices::openUrl() ignores anchor on local files.  
* QTBUG-102091 [Reg Qt 5->6] Disabled QCheckBoxes block scrolling of  
QScrollArea with mouse wheel  
* QTBUG-105951 Crash when closing dialog directly after closing popup  
* QTBUG-105621 Lingering bad cursor when dragging an undocked window  
over a textfield  
* QTBUG-105988 a11y: Accessible interface can't be retrieved after  
calling QAccessibleEvent::setChild on event created using the  
constructor taking QAccessibleInterface*  
* QTBUG-106001 tst_QMap::beginEnd() triggers assertion failure on  
Windows  
* QTBUG-105049 Improper styling of placeholder text in Qt6  
* QTBUG-105043 HTTP2 downloads can be very slow  
* QTBUG-105962 a11y AT-SPI: Qt sometimes uses same unique ID/object path  
for two different objects within a short time  
* QTBUG-106019 tst_QDtls::verifyClientCertificate fails with Ubuntu  
22.04 xorg and Windows 10 OpenSSL 3  
* QTBUG-103093 Palette Change And Application PaletteChange Never Emited  
* QTBUG-106012 tst_QResourceEngine::setLocale fails with Ubuntu 22.04  
xorg plus  
* QTBUG-106064 [REG] Undocking QDockWidget with drag misplaces it (a  
lot)  
* QTBUG-106017 tst_QSslCertificate fails with Ubuntu 22.04 xorg and  
Windows 10 21H2 OpenSSL 3  
* QTBUG-92964 Empty tree not spoken  
* QTBUG-105922 Can't compile examples with Emscripten 3.1.18  
* QTBUG-105004 Links to the code of examples for QCC2 were not updated  
at the move to QtDeclarative  
* QTBUG-105591 Closing application with toolbar floating breaks toolbar  
the next time you start the application  
* QTBUG-106036 Tst_QSslKey fails with Windows 1021H2 and openssl 3  
* QTBUG-105932 [Reg in Qt 6] setProperty() fails for QFlags types  
* QTBUG-96185 Cannot use  "qproperty-" to set enum properties in qss  
* QTBUG-96276 _NET_STARTUP_ID not supported  
* QTBUG-105735 Focus is not set to a child widget when a modal is open  
* QTBUG-104872 Calling QClipboard::image() corrupts image inside Win 11  
clipboard memory (from Windows Snipping Tool)  
* QTBUG-105338 lose alphachannel in imagedata from QClipboard  
* QTBUG-87764 [REG 5.15.0 -> 5.15.1] macdeployqt produces  
QtWebEngineProcess.app package with empty folders  
* QTBUG-105057 vnc: Setting override cursor causes a crash on client  
disconnect  
* QTBUG-106279 I doubt if QTextStream setAutoDetectUnicode doesn't work  
* QTBUG-105347 [Wasm] Stack example from documentation exits application  
* QTBUG-102004 [wasm] QML switch does not react on toggle  
* QTBUG-104518 Swipeview doesn't function correctly in Webassembly app  
* QTBUG-106153 wasm: Changing QTimer interval in multithreaded  
application breaks the timer  
* QTBUG-106223 assertion failed after Flickable takes grab from  
PinchHandler  
* QTBUG-104930 QLocale shows German text for "en_DE"  
* QTBUG-106222 -junitxml produces invalid time in output log (seconds  
divided by 1000 instead of seconds)  
* QTBUG-104999 crash in QTextMarkdownWriter  
* QTBUG-106354 Last QNetworkReply::readyRead() is not always emitted  
* QTBUG-104856 Non-Qt headers in 6.3.1\msvc2019_64\include  
* QTBUG-84234 Start new QCoreApplication after shutdown  
* QTBUG-98466 Misleading error messages when using macdeployqt on  
AppleSilicon Macs  
* QTBUG-89285 Document changes to State Machine Framework in Core  
Migration Guide  
* QTCREATORBUG-25594 Code model gets confused by qLastIndexOf in  
qstring.cpp  
* QTBUG-95237 [REG 6.0.4 -> 6.1.0] Integer-overflow in  
QFixed::operator+= through QImage::loadFromData(QByteArray)  
* QTBUG-96353 Test run procedure and flaky detection  
* QTBUG-98483 [macOS] QPushButton is broken in macOS Monterey  
* QTBUG-98937 KTX, ASTC image not displayed on Qt 6.2 and above  
* QTBUG-99489 tst_QTouchEvent::multiPointRawEventTranslationOnTouchPad  
is flaky on MacOS 10.15  
* QTBUG-81583 QTextMarkdownWriter: if a task list item's first line ends  
with monospace text, trailing backtick is omitted  
* QTBUG-81917 QtWidgets fails to build with clang 10.0-rc1 in C++20 mode  
* QTBUG-99009 QCursor::setPos X coordinates is wrong when DPI scaling is  
used  
* QTBUG-98350 QuickTest runs test suites in parallel, causing crashes  
* QTBUG-99368 TLS handshake fails due to incorrect cipher handling  
(Secure Transport macOS backend)  
* QTBUG-99775 Crash on QObject::objectName access when using QThreadPool  
from non-owning thread  
* QTBUG-20531 QLineEdit with a QCompleter: popup completion is drawn on  
the wrong location  
* QTBUG-99970 qt-testrunner.py    ERROR: Uncontrolled test CRASH!  
* QTBUG-92909 When following redirects, a PROPFIND request (and probably  
others) are converted to a GET  
* QTBUG-97844 Logitech mice and touchpads that send lots of events with  
small angleDelta cause overreaction  
* COIN-762 Coin's configure command gets warning about unused  
-DBUILD_EXAMPLES=OFF  
* QTBUG-99506 Loader with states and children loaders crashes on  
Integrity (release only)  
* QTBUG-95764 pure virtual call in QAccessibleQuickItem  
* QTBUG-98475 tst_QWindow::modalWindowEnterEventOnHide fails in QtBase  
with Windows 11  
* QTBUG-98478 tst_QFileSystemWatcher::signalsEmittedAfterFileMoved fails  
in QtBase with Windows 11  
* QTBUG-6905 font-weight: bold can truncate tab label  
* QTBUG-99791 Generated Makefile doesn't contain moc calls  
* QTBUG-100412 tst_qsrceen::grabWindow is flaky on Windows  
* QTBUG-99491 Windows - Android App, cmake build does not update  
correctly if app library is bigger than 2GB  
* QTBUG-93396 Android A11Y TalkBack: Slider does not announce value on  
change  
* QTBUG-100401 QToolbutton with popupMode QToolButton::InstantPopup and  
stylesheet have 2 arrows  
* QTBUG-100792 tst_QScreen::grabWindow() fails on Wayland  
* QTBUG-66818 tst_QWindow::initialSize fails on Wayland  
* QTBUG-100887 tst_QWindow::mouseToTouchTranslation() fails on Wayland  
* QTBUG-100889 tst_QWindow::requestUpdate() fails on Wayland  
* QTBUG-100891  
tst_QGuiApplication::genericPluginsAndWindowSystemEvents() fails on  
Wayland  
* QTBUG-100930 tst_QGraphicsWidget::updateFocusChainWhenChildDie fails  
on QNX  
* QTBUG-100929 tst_QImage::hugeQImage fails on platforms without  
adequate memory  
* QTBUG-87154 Add static dependencies from 3rdparty in qtbase  
* QTBUG-98489 tst_QTabBar::hoverTab fails in QtBase with Windows 11 and  
MSVC2022  
* QTBUG-99295 The tool "Qt6::sdpscanner" was not found  
* QTBUG-87397 tst_QGraphicsView fails on Android  
* QTBUG-101049 /permissive- not passed causes compiling errors  
* QTBUG-101332 FAIL!  : tst_QXmlStream::initTestCase in QNX_710  
* QTBUG-101194 tst_QFileDialog has failing tests for Android  
* QTBUG-87424 tst_QMenu fails on Android  
* QTBUG-99401 QSettings: support reading UTF-8 keys from INI files  
* QTBUG-100948 tst_QFontDatabase::systemFixedFont() fails on QNX  
* QTBUG-100917 tst_QImageReader::setScaledClipRect() SVG/SVGZ fails on  
Wayland  
* QTBUG-100918 tst_QOpenGL::bufferMapRange() fails on Wayland  
* QTBUG-101353 AUTORCC uses zstd even if Qt is build without rcc support  
* QTBUG-93955 Material.System does not work on Ubuntu (Gnome)  
* QTBUG-94459 Android reports incorrect screen size after rotation  
* QTBUG-87396 tst_toolsupport::offsets fails on Android  
* QTBUG-87423 tst_QPlainTextEdit fails on Android  
* QTBUG-89402 tst_QPlainTextEdit fails test cases on Android  
* QTBUG-97009 Broken rendering on Qt 6.2 Android arm64-v8a  
* QTBUG-101406 Add QT_TYPESAFE_FLAGS to headerclean and fix fallout  
* QTBUG-101519 FAIL!  :  
tst_QTouchEvent::multiPointRawEventTranslationOnTouchPad in  
Windows_11_21H2  
* QTBUG-101618 FAIL!  : tst_QSystemSemaphore::initialValue in QNX_710  
* QTBUG-101436 Font selection via styleName broken on Windows  
* QTBUG-99948 Fix enum/enum arithmetic in Qt  
* COIN-828 Fix build error message  
* QTBUG-101933 tst_quicktestmainwithsetup: QML module not found on webOS  
* QTBUG-101771 [Reg 5.15 -> 6.2] Item ignores the initial size from a  
binding when implicit size is used with Behavior  
* QTBUG-101888 tst_QGraphicsProxyWidget failing tests  
* QTBUG-87417 tst_QLineEdit fails on Android  
* QTBUG-100698 Fix BIC tests  
* QTBUG-99578 Global Functions are Undocumented  
* QTBUG-87438 corelib plugin tests fail on Android  
* QTBUG-102034 Merely subclassing QHeaderView causes it to lose built-in  
functionality  
* QTBUG-102095 tst_QFilesystemWatcher::watchDirectory() fails on macOS  
12 arm64  
* QTBUG-102096 tst_QFilesystemWatcher::signalsEmittedAfterFileMoved()  
fails on macOS  
* QTBUG-87668 tst_QWidget has many failing tests on Android  
* QTBUG-102030 Uncontrolled crash in tst_qwebenginepage  
* QTBUG-84349 QDateTimeParser wrongly accepts a sign in a month field MM  
* QTBUG-102043 tst_openglwidget has crashing cases  
* QTBUG-101346 Qt for Android has "weired" dependency on ICU, and deploy  
is slightly broken  
* QTBUG-102121 QT_FEATURE_tslib is On for INTEGRITY in case Desktop has  
tslib installed  
* QTBUG-101461 qdoc does not parse ref-qualified member functions  
* QTBUG-100697 Disappearing glyphs when application font reloaded  
* QTBUG-102258 tst_QCalendarWidget::showPrevNext() might crash on  
Android  
* QTBUG-100928 tst_QGlyphRun::mixedScripts fails on QNX  
* QTBUG-102253 tst_qwebengineview (Failed)  
* QTBUG-101274 QNX: Failing networks tests  
* QTBUG-102177 Regression: QProcess::readAllStandardError() crash on  
assert when MergedChannels is used  
* QTCREATORBUG-27196 Assert in qtcreator_processlauncher (On Windows,  
and Qt 6.3)  
* QTBUG-89400 tst_QCborStreamReader::hugeDeviceValidation two cases fail  
on Android  
* QTBUG-102447 tst_drawingmodes failed  
* QTBUG-100578 Heap-use-after-free is possible with  
QQuickPixmap::loadAsync()  
* QTBUG-78648 RHI: Does not work with Windows10 inside VMWare (Fusion)  
* QTBUG-102880 tst_QLocalSocket::threadedConnection is flaky on Windows  
* QTBUG-103055 FAIL!  : tst_QNetworkReply::ioGetFromHttpWithProxyAuth in  
QNX_710  
* QTBUG-103091 FAIL!  : tst_QDockWidget::floatingTabs in QNX_710  
* QTBUG-103056 FAIL!  : tst_QTcpServer::serverAddress in QNX_710  
* QTBUG-99545 App crashes in function QQmlPropertyCache::property(int)  
const on ARM 64bit  
* QTBUG-103196 syncqt does not reflect sources/headers known to CMake  
* QTBUG-99039 QVarLengthArray::push_back() is not strongly exception-  
safe  
* QTBUG-94462 Qt Quick TextEdit.insert() does not process Markdown text  
* QTBUG-103484 rich text gets converted to monospace in CI because  
QFontDatabase::GeneralFont is "Sans Serif" and is monospace  
* QTBUG-102594 [REG 5.15.6 -> 5.15.9] Many ANR issues by QtAccessibility  
* QTBUG-100145 ActiveQt example "outlook" build fails with a wall of  
errors: MSOUTL.cpp(346616): error C2062: type 'unknown-type' unexpected  
* QTBUG-89819 tst_qmarkdown tests fail on QEMU ARMv7  
* QTBUG-95993 QML Date operations are wrong when DST is active  
* QTBUG-103309 Menus can be truncated (REG from 5.15.2)  
* QTBUG-49663 menu position wrong on second monitor  
* QTBUG-101947 QMenu sizing issue on Windows with multiple monitors at  
different scaling [REG]  
* QTBUG-102982 QMenu appears at the wrong position without Per-Monitor  
DPI awareness  
* QTBUG-99663 Verify Qt Android build with NDK 24  
* QTBUG-97107 Add signing tests to unit test for Android  
* QTBUG-103923 GCC 12: failure to build from source [<QtBase>]  
* QTBUG-103470 [iOS] CMake translation handling fails  
* QTBUG-104128 top-level configure is still verbose in a non-developer  
build  
* QTBUG-104012 QDateTime constructor performance regression when year is  
below epoch  
* QTBUG-103753 incorrect document about QDomDocument::setContent()  
* QTBUG-103723 [iOS] CMake shader handling fails  
* QTBUG-102403 QObject::objectName() leads to heap-use-after-free in  
tst_qquickanimations::cleanupWhenRenderThreadStops()  
* QTBUG-87137 tst_QApplication::sendEventsOnProcessEvents() failed on  
Ubuntu 20.04/22.04 and RHEL 9  
* QTBUG-68860 tst_QGlyphRun::mixedScripts autotest fails on Ubuntu 18.04  
and QEMU builds  
* QTBUG-68865 tst_QMenuBar::check_menuPosition autotest fails on Ubuntu  
18.04  
* QTBUG-84248 tst_QFont::defaultFamily fails  
* QTBUG-103714 cut & paste checkboxes: checkbox is lost  
* QTBUG-103730 Qt Test tutorial is missing a clear entrypoint  
* QTBUG-103591 Windows: Comboboxes (Qml and QtWidgets) don't have the  
UIAutomation (UIA) ExpandCollapse pattern  
* QTBUG-104450 qmake: it's impossible to configure some compiler and  
linker options in the generated vcxproj  
* QTBUG-101008 Using Text.NativeRendering results in characters drawn  
too close to each other with fractional scale factors  
* QTBUG-104580 androiddeployqt fails with "unknown argument '--libs'"  
when call llvm-readobj v14  
* QTBUG-103593 androiddeployqt doesn't work well with user's QML module  
in their subdirectories  
* QTBUG-104656 pointer events end up with accepted state == false after  
successful delivery  
* QTBUG-104857 QtBase does not compile with QT_DISABLE_DEPRECATED_BEFORE  
= 0x060000  
* QTBUG-104241 tst_QOpenGLWidget::stackWidgetOpaqueChildIsVisible fails  
with Ubuntu 22.04, openSUSE Leap 15.4 and RHEL 9  
* QTBUG-104878 xcb wacom support gets confused about device instances  
* QTBUG-101932 two HoverHandlers with different  
acceptedDevices/acceptedPointerTypes: cursorShape doesn't change  
accordingly  
* QTBUG-89702 Improve the QRegExp->QRegularExpression docs  
* QTBUG-97615 CMake cannot find packages when only Qt6_DIR and not  
CMAKE_PREFIX_PATH is set  
* QTBUG-104787 Thread Sanitizer reports data races in QtConcurrent  
* QTBUG-102764 [REG: 5->6] Pen / Pencil input devices not working  
* QTBUG-105038 QCollator is limited to ≤ 2Gi characters  
* QTBUG-105051 pkg-config does not expose libexecdir for finding some  
tools  
* QTBUG-104840 heap-use-after-free in QTest::ignoreMessage  
* QTBUG-105238 Cmake error with -DQT_BUILD_MANUAL_TESTS=ON  
* QTBUG-85248 Qt warning  
"QHttpNetworkConnectionPrivate::_q_hostLookupFinished could not de-queue  
request, failed to report HostNotFoundError"  
* QTBUG-105158 Initialize all Vulkan Device Properties  
* QTBUG-104441 REG: No longer possible to use macros or functions that  
rely on an event loop in cleanup() after failed test function  
* QTBUG-105388 qhash.h:553:17: warning: argument 1 value  
'18446744073709551615' exceeds maximum object size 9223372036854775807  
* QTBUG-105048 QSqlQuery is supposed to be move-only, however we copy it  
in our code  
* QTBUG-104730 androidtestrunner splits data row names by whitespace and  
treats them as test functions  
* QTBUG-105736 tst_qfile unixPipe and socketPair tests fail on Android  
12  
* QTBUG-105738 tst_qopengl:: fboRenderingRGB30() fails on Android 12  
* QTBUG-105739 tst_vulkan vulkan11() and vulkanWindowGrab() fail on  
Android 12  
* QTBUG-104858 QT_DISABLE_DEPRECATED_BEFORE is not propagated to unit-  
tests  
* QTBUG-103474 Floating dock widgets don't minimize with mainwindow if  
they have been floating initially  
* QTBUG-105469 QVariant::load: unknown user type with name QList<int>  
when running QtRO example  
* QTBUG-103499 Android a11y: Flickable items outside of view are not  
selectable  
* QTBUG-103513 A11Y: Flickable child item focus frame position not  
updated  
* QTBUG-87728 tst_QGraphicsAnchorLayout::layoutDirection() failed on  
Ubuntu 20.04 in CI  
* QTBUG-85912 CBOR API has no example documentation  
* QTBUG-105958 [Android] Intent + Talkback leads to deadlock  
* QTBUG-106018  tst_QSslSocket fails with Ubuntu 22.04 xorg and Windows  
10 21H2 plus OpenSSL 3  
  
### qtsvg  
* QTBUG-99407 [REG 6.1.3  -> 6.2.0] Loading svg file takes too long  
* QTBUG-101698 [REG 6.2.2 -> 6.2.3] Integer overflow when loading svg  
image  
* QTBUG-100068 Colors of some SVG images are wrong  
* QTBUG-99642 Can't define CSS with properties for QToolButton with Qt 6  
  
### qtdeclarative  
* QTBUG-99113 qmlsc confuses ambiguous types in the same module  
* QTBUG-99043 The -i option to qmlcachegen, qmllint, qmlsc, etc. is  
wrong  
* QTBUG-99027 qmllint crashes in a combination with ListModel  
* QTBUG-75799 Strange flickering when restarting an animation with  
PauseAnimation and ScaleAnimator  
* QTBUG-99192 tst_qquickpixmapcache Failed  
* QTBUG-99229 "ninja: error: 'qrc_files-NOTFOUND', needed by  
'.qt_plugins/Qt6_QmlPlugins_Imports_untitled4.cmake', missing and no  
known rule to make it" when building "Qt Quick Application - Empty"  
project  
* QTBUG-99179 qmllint does not properly warn about duplictaed ids  
* QTBUG-98937 KTX, ASTC image not displayed on Qt 6.2 and above  
* QTBUG-96888 Not possible to quickly click buttons  
* QTBUG-99025 Property "hasOwnProperty" not found on type "Item"  
* QTBUG-99286  FAILED: src/quickcontrols2/material/impl/.rcc/qmlcache/qt  
quickcontrols2materialstyleimplplugin_RectangularGlow_qml.cpp  
* QTBUG-99275 agent:2021/12/16 18:36:00 build.go:394: FAILED:  
tests/auto/quickcontrols2/controls/basic/tst_basic  
* QTBUG-86533 Yocto and QNX builds are missing -rpath-link linker flag  
which causes non-prefix builds to fail  
* QTBUG-49049 arcTo doesn't always get drawn  
* QTBUG-99529 Touchpad scrolling list overshoot is buggy  
* QTBUG-99400 [Reg 5.2 -> 5.3] qmlplugindump: error details missing on  
linux  
* QTBUG-99477 Crash in QRhiD3D11::executeCommandBuffer with nullptr  
access  
* QTBUG-98116 Clean up qtdeclarative doc warnings and enable  
documentation testing in CI  
* QTBUG-99644 invalid access of indicator item inside switch type  
destructor  
* QTBUG-97081 qmllint should turn on compiler warnings on "pragma  
Strict"  
* QTBUG-99888 configure fails when only qtdeclarative and qtbase are  
checked out  
* QTBUG-81938 qtdeclarative:  
tst_QPauseAnimationJob::multipleSequentialGroups is flakey  
* QTBUG-94848 Missing element in drawer when used with ListView and  
Section  
* QTBUG-99273 QtDeclarative fails to configure when Python is not in  
PATH but is found via FindPython  
* QTBUG-99128 qmlsc does not see property revisions  
* QTBUG-100046 FAIL!  : tst_qquickborderimage::borderImageMesh()  
* QTBUG-99604 TextArea and TextField don't use IBeamCursor when readOnly  
and selectByMouse are both true  
* QTBUG-100110 switch handle goes out of bounds when size is increased  
(flatstyle example)  
* QTBUG-99608 tst_qmlcachegen (Failed)  
* QTBUG-100089 REG: QQuickDial with the Imagine style is displaying the  
handle at an incorrect position  
* QTBUG-99974 qt.labs.qmlmodels classes documented twice  
* QTBUG-99693 qmllint: aliased required property shouldn't be warned as  
missing  
* QTBUG-99311 QtQuick Window does not expose enum of visibility property  
of Window  
* QTBUG-100314 qmltc tests fail to compile with older CMake  
* QTBUG-100339 qmllint does not find ApplicationWindow.window  
* QTBUG-100326 *.mjs files not added to qmldir when added to  
qt_add_qml_module()  
* QTBUG-99124 Properly document ScrollBar in ScrollView  
* QTBUG-98039 QML javascript: "this" in class ctor becomes undefined  
during if(){...} in arrow functions  
* QTBUG-100260 Crash on access after using QML singleton as a model  
* QTBUG-100377 [REG 5.15 -> 6.2] Date.parse() can't handle some dates on  
Qt 6 but works in Qt 5  
* QTBUG-100366 tst_qmlcachegen tests using generateCache are valid only  
for host  
* QTBUG-100221 qtdeclarative compilation fails on arm64  
* QTBUG-100279 Building fails on Linux ARM64  
* QTBUG-97185 Quick DragHandler Reporting Wrong Coordinates using  
TouchScreen Input  
* QTBUG-98486 Touch points coordinates does not take into account the  
Device Pixel Ratio on Windows  
* QTBUG-98543 Invalid updates of contentY of Flickable on touch screen  
* QTBUG-95033 ButtonGroup does not work with Windows style Button  
* QTBUG-100480 QtQuick compiler generates bad code for "!=" operator  
* QTBUG-94161 "QTransform::translate with NaN called" when hovering over  
window containing Imagine style GroupBox containing a TextEdit  
* QTBUG-99547 PathView item does not appear in certain circumstance  
* QTBUG-51078 Use of Item obligatory in SwipeView?  
* QTBUG-51669 QQC2: SwipeView is not working as expected  
* QTBUG-100444 qmllint does not like variables in javascript  
files/modules  
* QTBUG-100469 Qml runtime resizeToItem configuration is not working  
* QTBUG-86695 [REG: 5.12 -> 5.14] Broken State::when behavior after  
suspicious change  
* QTBUG-95763 Configuring an executable with an attached qml module  
fails when using the Xcode generator  
* QTBUG-100380 valueAt(int index) method of ComboBox QML type (QQC2) is  
undocumented  
* QTBUG-100680 TableView: positionViewAtRow will in some cases move the  
viewport too far  
* QTBUG-100855 qmljs tool doesn't link on iOS build  
* QTBUG-95587 icon.source of Control is not resolved relative to user  
code  
* QTBUG-100947 Infinity not usable in QML  
* QTBUG-100978 A completely valid qml file with a block comment can  
result in a qmlcache compilation error  
* QTBUG-100980 Q_UNREACHABLE triggered in qmlcachegen  
* QTBUG-100883 qmlcachegen miscompiles QVariant of QObject* to bool  
conversion  
* QTBUG-101011 qmlsc goes into infinite loop  
* QTBUG-100338 qmllint warns about all members of model index  
* QTBUG-101074 Assert in qqmljstypepropagator.cpp  triggers and prevents  
compilation  
* QTBUG-101155 qml binding to a QML_EXTENDED property doesn't update  
when changed signal emitted  
* QTBUG-101206 tst_qquickwidget (Failed)  
* QTBUG-101285 error: use of undeclared identifier 'r9_1'; did you mean  
'r2_1'?  
* QTBUG-99436 Quick Drag and Drop Tiles example broken in Qt 6  
* QTBUG-98857 [REG 6.2.0->6.2.1] QML: Wrong item position after  
drag&drop  
* QTBUG-67950 Crash when changing Loader source inside a Repeater when  
the model changes  
* QTBUG-98181 Importing directory into namespace triggers assert  
* QTBUG-92006 Fractional font size is displayed incorrectly  
* QTBUG-77371 Accessibility: Multiple Text items with Accessible  
properties grouped together on Android  
* QTBUG-98011 qmltc crashes due to insufficient import locations in a  
specific Qt build configuration  
* QTBUG-101163 Qmltc error prevents qtdeclarative from compiling  
* QTBUG-101186 [REG 6.1.3 -> 6.2.0] AnchorAnimation causes Rectangle  
width and height to be zero  
* QTBUG-101349 qmlsc and qmlcachegen miscompile draganddrop/grid example  
* QTBUG-101383 QtDeclarative: Fix compiler warnings for QNX  
* QTBUG-101170 Regression: FileDialog.SaveFile fileMode doesn't work  
correctly in QML FileDialog  
* QTBUG-101402 There doesn't appear to be a list of text-field  
validators  
* QTBUG-61971 ComboBox wrong touch behavior  
* QTBUG-100508 SEGFAULT Crash on  
QQuickOpenGLShaderEffectMaterial::updateTextures()  
* QTBUG-101197 DragHandler.snapMode not listed in docs  
* QTBUG-100355 [REG 6.2.2 - 6.2.3] Custom image providers do not scale  
on High DPI displays  
* QTBUG-73271 QQmlComponent::setData crashes sporadically when called  
from multiple threads  
* QTBUG-101386 TableView: a TapHandler / PointerHandler doesn't always  
detect a tap  
* QTBUG-101617 [FTBFS] AUTOMOC for target tst-qmltyperegistrar-with-  
dashesplugin: The "moc" executable "...../qtbase/libexec/moc" does not  
exist.  
* QTBUG-101573 Popup is not closed when MouseArea on ToolTip is pressed  
* QTBUG-101034 Application not detecting submenu shortcuts  
* QTBUG-94391 FileDialog unwanted uri suffix for Android11 SAF  
* QTBUG-99449 qmlformat errors when JS array has trailing comma  
* QTBUG-101738 tst_QQmlDebugTranslationService::initTestCase fails on  
macOS 12/arm 64  
* QTBUG-101811 Import alias leads to 'Type not found'  
* QTBUG-101752 qmldir-import does not always work  
* QTBUG-101933 tst_quicktestmainwithsetup: QML module not found on webOS  
* QTBUG-101771 [Reg 5.15 -> 6.2] Item ignores the initial size from a  
binding when implicit size is used with Behavior  
* QTBUG-101700 DelegateModel: using for ... of loop in JS to iterate  
DelegateModel.groups attached property causes a crash  
* QTBUG-102018 tst_sanity cannot find test data on webOS  
* QTBUG-101884 Fix and enable tst_qquickwidget for  
QEMU/offscreen/software  
* QTBUG-102022 tst_codegen_direct fails  
* QTBUG-100431 Crash in libQt5Qml V4 engine caused by wrong memory  
access  
* QTBUG-95726 [REG 5.15.2-6.2.0] MouseArea loses hover when cursor is  
inside of nested MouseArea  
* QTBUG-95398 MouseArea inside of SpinBox contentItem is blocking  
hovered property  
* QTBUG-87697 QJSEngine replaces toString() method of QObject  
* QTBUG-90964 Examples missing cmake support (qml)  
* QTBUG-101394 ItemDelegate blocks ScrollView hovered  
* QTBUG-100543 [REG 5.15.2-6.2.2] Control doesn't propagate hover to his  
parent  
* QTBUG-100149 [Regression] Parent Button is not hovered if a child  
button is hovered  
* QTBUG-98940 Button inside MouseArea does not pass mouse hover events  
* QTBUG-98850 [REG 6.1->6.2] HoverHandler doesn't get hoverevents, when  
a button is on the parent  
* QTBUG-102138 QML ComboBox: Customization example is broken  
* QTBUG-102153 qmlcachegen does not properly handle ambiguous types  
* QTBUG-100018 tst_qmltc_manual fails on Android  
* QTBUG-102147 Declared alias import not found  
* QTBUG-102309 Typo in code generator leads to invalid code  
* QTBUG-102281 qmlcachegen generates invalid code  
* QTBUG-102424 Doc: FileDialog doesn't mention that the native Android  
file dialog is supported  
* QTBUG-100253 tst_qquickpopup fails on Android  
* QTBUG-91649 "Writing to "entity" broke the binding to the underlying  
model" warning when removing item from model  
* QTBUG-101655 [Reg 6.1 -> 6.2] Error creating inline component in Qt  
6.2  
* QTBUG-102415 tst_QQuickFolderDialogImpl::goUp() is flakey  
* QTBUG-101488 tst_QQuickFileDialogImpl is flaky  
* QTBUG-102446 tst_qquickfontloader_static Failed  
* QTBUG-102416 tst_qv4debugger fails on Android  
* QTBUG-102116 QML/C++ integration needs better cross-linking  
* QTBUG-100176 tst_qquickapplicationwindow crashes on Android  
* QTBUG-100991 Some tests crash on Android CI  
* QTBUG-100169 tst_qqmlextensionplugin fails on Android  
* QTBUG-99063 static top-level developer configuration fails in  
qtdeclarative doc snippet  
* QTBUG-100177 tst_qquickheaderview fails on Android  
* QTBUG-102646 QQuickFlickable wheel event not work correct for mouse  
device with pixel scroll wheel support for NoScrollPhase  
* QTBUG-102449 Native TextField: placeholderText does not respect  
horizontalAlignment  
* QTBUG-102644 qmldomlib breaks configure for top-level build: depends  
on moc before it's built  
* QTBUG-102724 Popup doesn't redraw if content exceeds window size  
* QTBUG-102339 Conan: multiple prefixes not supported when building e.g.  
examples  
* QTBUG-100257 tst_qquickdrawer fails on Android  
* QTBUG-102558 DialogButtonBox not regenerating layout on change of  
child Button width  
* QTBUG-102554 Segmentation fault when using QML_SINGLETON with  
QAbstractListModel  
* QTBUG-102776 JIT is disabled on Android  
* QTBUG-102085 Extending QML example has no CMake documentation  
* QTBUG-102729 Crash in QQmlBinding::evaluate()  
* QTBUG-100256 tst_qquickmenu fails on Android  
* QTBUG-102425 QML engine crashes if there are errors while setting up  
property bindings  
* QTBUG-102454 rootContext()->setContextProperty assertion with frozen  
`QQmlPropertyMap`  
* QTBUG-78648 RHI: Does not work with Windows10 inside VMWare (Fusion)  
* QTBUG-101005 tst_qquickmenu and tst_qquickpopup tests fail to return  
test result  
* QTBUG-100016 tst_qquickfolderlistmodel fails on Android  
* QTBUG-77335 tst_qquickfolderlistmodel::basicProperties fails on  
Android  
* QTBUG-102598 Build fails in qtdeclarative with  
localstorageexample_Header_qml.cpp  
* QTBUG-102719 [Reg 5.15 -> 6.1] Not possible to use Loader inside  
inline component  
* QTBUG-102857 [Reg 6.2 -> 6.3] QML MediaDevices elements not displayed  
in ListView  
* QTBUG-101401 Crash in QQmlObjectCreator::populateInstance  
* QTBUG-38932 PropertyAnimation ignores from/to changes  
* QTBUG-102765 qml type compiler: generated sources not unity buildable  
* QTBUG-102560 qml type compiler: codegen error with Gradients  
* QTBUG-95395 Code snippets for HoverHandler show TapHandler  
* QTBUG-101932 two HoverHandlers with different  
acceptedDevices/acceptedPointerTypes: cursorShape doesn't change  
accordingly  
* QTBUG-102953 ninja: error: 'src/remoteobjectsqml/CMakeFiles/RemoteObje  
ctsQml.dir/cmake_pch_arm64.hxx.pch'  
* QTBUG-102968 [Reg 6.2 -> 6.3] qmlcachegen failure suspecting for  
recognizing qml type  
* QTBUG-98964 No way to disable "Binding on contentItem is not deferred"  
warning when code deliberately doesn't care about deferred execution  
* QTBUG-100166 tst_qqmlenginedebugservice fails on Android  
* QTBUG-102996 QML MouseArea containsPress / containsMouse / pressed are  
stuck when using multitouch  
* QTBUG-35995 Clicked signal not emitted on MouseArea when changing  
visibility and listening for doubleClicked  
* QTBUG-102158 Click signal not emitted in MouseArea after DoubleClicked  
is emitted and tab changed  
* QTBUG-103017 Qt.labs.platform Menu does not show icons  
* QTBUG-103026 FAIL!  : tst_QQmlDebugTranslationService::verifyMissingAl  
lTranslationsForMissingLanguage()  
* QTBUG-74028 Text inside MultiPointTouchArea has invalid coordinates on  
touch events  
* QTBUG-84280 TextArea inside Flickable - cursor does not appear with  
LayoutMirroring.enabled  
* QTBUG-83662 For MultiPointTouchArea with a child PinchArea multiple  
pressed signals for multiple touch points on mouse press  
* QTBUG-77055 When pixelAligned is set to true in a Flickable, then it  
is possible that doing a flick away the boundaries (so you see a gap)  
will not cause it to snap back  
* QTBUG-100560 Crash when closing SwipeDelegate in onCompleted handler  
* QTBUG-103224 [read-only] marking is missing from acceptableInput  
property of TextInput QML type in the documentation  
* QTBUG-103081 QQmlComponent::create() crashes when creeating a  
QML_EXTENDED_NAMESPACE(Type) object when Type is a Q_OBJECT extending a  
property  
* QTBUG-102793 [REG: 5.13->5.14] Bindings in delegates get triggered  
multiple times if delegate and/or model is changed  
* QTBUG-99117 Custom style names not added to file selectors  
* QTBUG-101628 Pinch gestures are not cancelled when pinch.accepted  
property is set to false on macOS.  
* QTBUG-83413 Text rendering glitches in combination with loader and  
elide  
* QTBUG-67512 Dialog is closed when releasing a drag outside of it  
* QTBUG-78090 When active focus changes then it will set active focus on  
the new item first before it loses active focus on the other item  
* QTBUG-87190 Application freezes when there is no control to focus next  
* QTBUG-84375 Animation without 'from' value set and loops > 1 slows  
down at the end  
* QTBUG-102545 [REG 6.2 -> 6.3] Crash when appending a custom QObject to  
a ListModel  
* QTBUG-75197 Editable ComboBox doesn't clear the selection  
* QTBUG-100161 DelegateModelGroup crashes on insert  
* QTBUG-103203 [REG 5.15.9 -> 6.0.4] Crash when dynamically inserting  
Item's to DelegateModelGroup  
* QTBUG-30036 GridView considers items in its header as valid indexes in  
indexAt(int, int)  
* QTBUG-91461 GridView: resizing items causes view to reposition  
incorrectly  
* QTBUG-92868 GridView: the number of visible items is miscalculated  
* QTBUG-103361 qquickdeliveryagent.cpp error: unused parameter 'win'  
* QTBUG-102865 QML MessageDialog doesn't describe how to handle  
buttonClicked signal  
* QTBUG-99639 Rotated flickable decelerates in wrong direction  
* QTBUG-102117 "Integrating QML and C++" needs to be reworked or removed  
* QTBUG-101218 TableView: sync view ends up not in sync when using  
margins  
* QTBUG-102983 [Reg 6.2 -> 6.3] QML MediaDevices elements not displayed  
in ComboBox  
* QTBUG-98422 qmlformat incorrect formatting of several cases  
* QTBUG-102487 [REG 5.15.8 -> 5.15.9 + 6.2.3 -> 6.3.0] SwipeView shows  
last page on first page  
* QTBUG-101768 matrix4x4 doc sample code  
* QTBUG-103479 Required properties in inner elements of delegates cause  
views to omit model data from context  
* QTBUG-100014 tst_qqmlqt fails on Android  
* QTBUG-103101 qmllint: Produce better unqualified access warnings for  
models  
* QTBUG-93649 Regression 5.15.3->6.0.0: Mouse Events not accepted on a  
MouseArea placed inside Popup::background  
* QTBUG-103529 Support for value type lists is rather broken in  
qmlsc/qmlcachegen  
* QTBUG-103324 qmlls: assertion failed "ModuleIndex::qmldirsToLoad  
called twice" when editing a file  
* QTBUG-103560 qmlsc allows access to fractional indices of  
QQmlListProperty  
* QTBUG-103707 qmlcompiler: Script bindings with empty blocks hit an  
assert/crash  
* QTBUG-103522 The PreventStealing of mouseArea does not work properly  
in Flickable's(ListView) child item.  
* QTBUG-102120 tst_qquickmenubar fails on webOS  
* QTBUG-98387 ScrollBar not resizing to left correctly when window is  
extended left  
* QTBUG-102806 qmllint: access properties outside delegate without  
qmllint warnings  
* QTBUG-101012 qmllint: cannot reference id outside for a Component in  
the same file  
* QTBUG-103588 [Reg. 5.15-6.x] Returning empty QVariant from list model  
causes segfault  
* QTBUG-59141 Buttons / mouseArea doesn't works under Drawer's drag area  
* QTBUG-103216 Vulkan Validation Error in QQuickRenderTarget  
* QTBUG-102944 [Reg 5.15 -> 6.2] Relative QML import does not work from  
Android assets  
* QTBUG-103915 tst_snippets fails on webOS  
* QTBUG-101975 No longer possible to pre-select a file when fileMode is  
SaveFile  
* QTBUG-103897 QQmlJSImportVisitor: bindings on QQmlJSScopes are created  
when scopes are not yet fully resolved  
* QTWEBSITE-1051 Incorrect code snippet in QML inheritance and coercion  
example  
* QTBUG-103924 GCC 12: failure to build from source [<QtDeclarative>]  
* QTBUG-103920 qmlcachegen crashes when code uses list<...> qml type  
* QTBUG-102625 [REG 5.15 -> 6.0] Double click event does not fire when  
using DragHandler as a child of Window in Qt6  
* QTBUG-103187 Reconfiguration is slow due to qmlimportscanner  
* QTBUG-104051 FAIL!  : tst_qqmlnotifier::deleteFromHandler() Compared  
values are not the same  
* QTBUG-104026 TypeError warnings from attached property usage in  
tst_qquicklistview  
* QTBUG-104129 qmllint: Type "QList<int>" of property "boo" not found  
* QTBUG-104092 qmlsc tries to look up lower case names as types  
* QTBUG-95993 QML Date operations are wrong when DST is active  
* QTBUG-102971 Something fishy going on on MinGW with QML Date  
* QTBUG-103956 [qmltc] property alias causes "unknown origin" error  
* QTBUG-104010 qmlcachegen generates inefficient code for conversions to  
string  
* QTBUG-101538 Pointless link to Qt Quick Text Validators page  
* QTBUG-75109 tst_QQuickListView::currentIndex() is failing  
* QTBUG-104089 TextEdit has wrong cursor shape on hover  
* QTBUG-99057 Mismatched-new-delete warning when using qmltypes with  
mingw 9.0  
* QTBUG-103832 The delegate item of ListView is not pressed if the  
boundsBehavior is to set Flickable.StopAtBounds  
* QTBUG-86088 QResource::unregisterResource() function does not remove  
the resource from memory  
* QTBUG-99947 Hidden TextEdit cursor blinking keeps triggering redraw  
when using QQuickWidget  
* QTBUG-104373 [REG: 6.2->6.3] qt_add_qml_module does not register  
QML_ELEMENT classes if version starts with 0  
* QTBUG-100820 [REG 5.15.2-6.2.3] Wrong rendering of semi-transparent  
text if Text.NativeRendering is used  
* QTBUG-102965 File order of CMake project can break compilation due to  
QMetaTypeId<T> specialization  
* QTBUG-104197 qmllint: unknown attached property scope T.  
* QTBUG-104138 Doc: Wrong link to 'Squish'  
* QTBUG-98914 QML Test with grabImage() fails on iOS  
* QTBUG-100644 Document how to properly add javascript files with  
qt_add_qml_module  
* QTBUG-38765 When propagateComposedEvents is set, drag does not always  
move the flickable  
* QTBUG-74842 Flickable behind MouseArea does not steal first drag event  
after creation  
* QTBUG-104470 Text overlap in custom menu  
* QTBUG-101973 File Dialog does not re open in some situation.  
* QTBUG-104447 qmlsc miscompiles bindings that throw exceptions  
* QTBUG-104462 qmlsc miscompiles JavaScript functions with arguments  
* QTBUG-104523 error: no member named 'offsetsAndSize' in  
'qt_meta_stringdata_TestClass_t  
* QTBUG-104544 When the repeater is used as the contentItem of the menu,  
all items are invisible  
* QTBUG-101268 ListView does not preserve its relative scrollbar  
position when window is restored down on Windows if height of  
ListView.header changes dynamically  
* QTBUG-101266 Changing ListView.header height dynamically doesn't  
preserve relative scrollbar position when window is Maximized  
* QTBUG-102762 QML_ELEMENT is broken in Qt 6.3.0 on Android  
* QTBUG-104512 Invalid code generated  
* QTBUG-104258 tst_QQuickPopup::Material fails with Ubuntu 22.04  
* QTBUG-104094 qmltc could not correctly include QML files with  
QT_QMLTC_FILE_BASENAME specified  
* QTBUG-104156 QML Type Compiler documentation formats unreasonably wide  
* QTBUG-104603 Clarify the QML_EXTENDED documentation  
* QTBUG-104471 tst_QQuickListView2::tapDelegateDuringFlicking fails on  
Android  
* QTBUG-104379 [REG 6.3.0 -> 6.3.1] Crash when trying to debug QML  
Application  
* QTBUG-102559 macOS style focus frame incorrectly positioned  
* QTBUG-104573 DialogButtonBox enums are not known to qmllint  
* QTBUG-104442 QML Image does not rescale on setGeometry() when "layer"  
is enabled  
* QTBUG-104536 [Possible regression]: Rendering errors when using  
layer.enabled: true  
* QTBUG-87119 MouseArea inside SplitView item takes mouse events away  
from Splitview handle  
* QTBUG-97385 QtQuick SplitView with Flickable gets stuck  
* QTBUG-100554 Qt Quick Calendar: 1st row sometimes contains only days  
from the previous month  
* QTBUG-104642 iOS: TextField has blinking cursor, but no input panel is  
showing  
* QTBUG-104242 tst_QQuickDrawer tests are failing with Ubuntu 22.04  
* QTBUG-104257 tst_QQuickMenu(bar) tests are failing with Ubuntu 22.04  
* QTBUG-104508 qmlcachegen fails to compile PhotoCaptureControls.qml in  
multimedia  
* QTBUG-104625 tst_Qmlls::testWorkspace fails  
* QTBUG-104269 No word-wrap in fallback MessageDialog  
* QTBUG-104705 Controls, macOS: FocusRect for TextField is not aligned  
correctly  
* QTBUG-104491 mouse event broken after continuous transition animation  
in StackView.  
* QTBUG-104657 Custom ComboBox does not function properly with model  
passed from c++  
* QTBUG-104665 Basic blocks pass wrongly optimizes indirect register  
reads out  
* QTBUG-104084 tst_qmldomitem ERROR: AddressSanitizer: alloc-dealloc-  
mismatch  
* QTBUG-104803 Crash when calling QJSValue::hasProperty("x") from Qml on  
a QVector3D received from a Q_PROPERTY  
* QTBUG-101480 The "Control" can't inherit the palette of  
"ApplicationWindow"  
* QTBUG-104743 qmlsc crashes  
* QTBUG-104683 qmlsc: Compilation errors with enums  
* QTBUG-94462 Qt Quick TextEdit.insert() does not process Markdown text  
* QTBUG-104795 SystemInformation singleton has few docs  
* QTBUG-104325 QQuickPointerHandler::currentEvent() exposes stale event  
* QTBUG-101008 Using Text.NativeRendering results in characters drawn  
too close to each other with fractional scale factors  
* QTBUG-98769 QML StackView heap-use-after-free on pop()  
* QTBUG-104865 QQuickPaddedRectangle emits topPaddingChanged incorrectly  
* QTBUG-98936 Can't use Apple Pencil with Qml controls  
* QTBUG-102764 [REG: 5->6] Pen / Pencil input devices not working  
* QTBUG-103937 QML WebEngineView - Wacom pen not works  
* QTBUG-104537 [REG 6.2.4-6.3.1] HoverHandler do not propagate hover to  
TextEdit  
* QTBUG-104725 android: top level build failed with examples in tree  
* QTBUG-104884 Crash with ComponentBehavior: Bound and DelegateModel  
* QTBUG-105000 [REG: 5.15.2->5.15.10] State.when does not work for  
objects anymore  
* QTBUG-90466 Missing line number in tst_qquickloader error message on  
macOs  
* QTBUG-104702 qmllint does not understand implicit conversion between  
QString and QByteArray  
* QTBUG-104701 qmllint does not resolve imported .js file inside QML  
module  
* QTBUG-104658 macOS style lacks DialogButtonBox implementation  
* QTBUG-104749 qmlsc: QQuickAnchors Q_PROPERTIES are not FINAL  
* QTBUG-105164 ScrollView consumes wheel events even when 'wheelEnabled'  
is set false  
* QTBUG-104780 Assertion failure when using "anchors.fill: parent" in  
tests/auto/qml/qmltc/QmltcTests/delegate_context.qml  
* QTBUG-104468 [qmltc] -Waddress warnings  
* QTBUG-91687 QML fails to run benchmarks in qmlbench's v8bench  
directory  
* QTBUG-58559 Deletion of a dynamic properties to JSObject ends up using  
all memory  
* QTBUG-94983 Crash when binding to aliased grouped property  
* QTBUG-105252 [QML] Compiler does not accept boolean type cast  
* QTBUG-105188 Instruction "generate_BitOr" not implemented  
* QTBUG-102136 QML Slider: (Lack of) implicitWidth affects background  
height when anchors are used  
* QTBUG-105361 qmlformat: Unnecessary replacement of 'let' with 'var',  
leading to inline write errors  
* QTBUG-105239 Split "Module Definition qmldir Files"'s table  
* QTBUG-105566 Touch panning a ListView in View3D broken  
* QTBUG-105058 PathView steals touch event of PinchArea delegate  
* QTBUG-104983 [REG] 908aa77d16e00f2bccc0ddae0f8b61955c56a6a1 breaks  
scrollbars if contentItem is accessed before it is set  
* QTBUG-105570 TreeViewDelegate: cannot perform selections  
* QTBUG-105601 [REG 6.3.2->6.4.0] texteditor fails to compile on Wasm  
* QTBUG-105682 [REG 6.4.0 beta1 -> beta3] quick3d/principledmaterial not  
compiling on iOS  
* QTBUG-92192 Issues calling JSON.stringify() on objects  
* QTBUG-95232 Qt Quick Local Storage does not work with absolute paths  
* QTBUG-89567 [REG 5.15.0 -> 5.15.1] Qt.labs.platform.MenuItem is  
triggering shortcut even in disabled state  
* QTBUG-104022 tst_SignalSpy::testCount fails in CI on macOS  
* QTBUG-105611 tst_cursor fails often on webOS  
* QTBUG-105572 Wrong image in documentation for eventcalendar example  
* QTBUG-105208 REG: Selecting text inside a TextEdit causes existing  
lines to disappear and empty lines to appear.  
* QTBUG-105555 REG: Text selection in the text editor example causes the  
text document to reposition the blocks after the selection  
* QTBUG-105728 REG: TextArea & TextEdit breaks when selecting text with  
mouse  
* QTBUG-103819 QML TextEdit memory usage is extreme and the memory is  
not freed  
* QTBUG-105907 Use the time stamp of the touch event when deliver touch  
as mouse  
* QTBUG-105812 Small typo in Accessible.description documentation  
* QTBUG-105899 ColorDialog: The text fields on ColorInputs.qml are buggy  
for the Fusion, Imagine and Universal styles.  
* QTBUG-104966 The Items in the ListView is not showing when the model  
is changed during dragging  
* QTBUG-105254 [QML] Compiler complains about namespaced QML_ELEMENTS -  
sometimes  
* QTBUG-93603 Document that mixing old/new forms in QML Connections  
causes new form to not work  
* QTBUG-104928 qmlimportscanner: segfault on unexpected argument  
* QTBUG-92068 Remote loading ui files in Qml fails to load from existing  
directory  
* QTBUG-105590 qmllint warns about enum values of ScrollBar  
* QTBUG-95864 ListElement: cannot use script for property value  
* QTBUG-105937 ProgressBar draws progress incorrectly  
* QTBUG-105992 Changing FontLoader font causes timer errors  
* QTBUG-105535 When PropertyChanges transitions to a constant value with  
a PropertyAnimation, the binding from previous state is still active  
* QTBUG-96779 Overhaul basic type documentation  
* QTBUG-105860 REG: Dialog box and action bar buttons missing in  
texteditor example  
* QTBUG-96631 Unexpected syntax error when declaring a class inside  
another class  
* QTBUG-104556 Crash when accessing enum from QML  
* QTBUG-105608 Crash using enums  
* QTBUG-104982 [Regression] binding stops being evaluated  
* QTBUG-106110 PinchHandler.minimum/maximumScale properties aren't  
enforced with native gestures  
* QTBUG-106098 ComboBox: The implicitContentWidthPolicy property doesn't  
work for the Imagine style  
* QTBUG-106119 Crash when calling findChild from TestCase  
* QTBUG-103900 ColorDialog: Implement the ColorInputs.qml component in  
C++  
* QTBUG-106391 assertion failure in  
QQuickItemPrivate::localizedTouchEvent  
* QTBUG-104535 REG: Android's Back button does not close QQC2 Dialogs  
anymore  
* QTBUG-106357 crash in QIntrusiveListNode::remove() when pinch-zooming  
in QtPDF on iOS  
* QTBUG-99175 tst_QSequentialAnimationGroupJob::  
groupWithZeroDurationAnimations is flaky on macos ARM  
* QTBUG-99174 tst_qquickimageprovider Failed  
* QTBUG-99143 tst_qqmltimer is flaky on macOs  
* QTBUG-99214 Tests that rely on QProcess with the main app lib fail on  
Android  
* QTBUG-97579 When using DelegateChooser with a TreeView and then doing  
a sort on the model in a TreeView, the items are not correctly updated  
to reflect the chooser  
* QTBUG-57098 Popup's CloseOnEscape policy prevents escape key from  
being used without closing the popup  
* QTBUG-99355 tst_qmltc::listView() is flaky under qemu  
* QTBUG-89193 ListView delegate position resets after displaced  
transition  
* QTBUG-99367 Custom ScrollBar style not used after upgrade from 5.15 to  
6.2  
* QTBUG-83069 TextArea from Material theme is not properly clipped when  
used inside Flickable  
* QTBUG-99615 Most QMutableEventPoint usage depends on Undefined  
Behaviour  
* QTBUG-99582 crash in Controls Text Edit example when pasting in large  
amounts of text  
* QTBUG-98350 QuickTest runs test suites in parallel, causing crashes  
* QTBUG-91706 QML: Subclassing a QQuickItem that has revisioned  
properties fails  
* QTBUG-92591 QtDeclarative autotest configure fails on Android builds  
* QTBUG-100040 Configuring qtdeclarative fails for qmljs, qmljsrootgen  
and qjstest fails when cross-compiling  
* QTBUG-90898 Error compiling Qt with MSVC and c++2a  
* QTBUG-64470 tst_QQuickFramebufferObject::testInvalidate is failing on  
macOS  
* QTBUG-65614 tst_QQuickFramebufferObject failed on b2qt  
* QTBUG-76546 QML debugger tests that run a sub-process fail on QNX  
* QTBUG-100103 A mix of own qmldir and implicit import directory is  
badly broken in qmltc setup  
* QTBUG-100003 tst_qqmlmoduleplugin fails on Android  
* QTBUG-100020 tst_qqmljsscope fails on Android  
* QTBUG-100021 tst_qdebugmessageservice crashes on Android  
* QTBUG-100164 tst_qqmldebugtranslationservice fails on Android  
* QTBUG-100167 QML debugger tests fail on Android  
* QTBUG-100171 tst_qmldomitem fails on Android  
* QTBUG-100173 tst_qquickwidget fails on Android  
* QTBUG-100175 tst_testfiltering fails on Android  
* QTBUG-100191 tst_sanity and tst_snippets fail on Android  
* QTBUG-100254 tst_qquickmenubar fails on Android  
* QTBUG-100258 tst_focus crashes on Android  
* QTBUG-95750 RangeSlider::test_overlappingHandles test fails on  
LinuxUbuntu_20_04x86_64LinuxQEMUarmv7GCC  
* QTBUG-99198 QVariant::setValue() asserts when passing an object of  
qmltc-generated type wrapped in QT_NAMESPACE  
* QTBUG-45045 SIGFPE in QQuickMenu  
* QTBUG-52472 Undefined Behaviour in qsimpledrag.cpp line 207  
* QTBUG-100324 QHelpEvent::globalPos() returns frequently a wrong value.  
* QTBUG-75786 macOS 10.14 autotest failures  
* QTBUG-82015 qquickanimations::simplePath() is flakey on macOS  
* QTBUG-82043 tst_qquickmousearea::pressAndHold() is flakey on macOS  
* QTBUG-82404 tst_qquickbehaviors::currentValue is flaky on macos  
* QTBUG-85622 tst_qquickloader: urlToComponent is flaky on macos  
* QTBUG-85624 tst_qquickanimations: reparent is flaky on macos  
* QTBUG-88541 tst_qquickpointhander::tabletStylus doesn't work on hidpi  
* QTBUG-95863 tst_qquickpathview::snapOneItem() is flaky on macOS  
* QTBUG-98494 tst_qmlformat::testExample times out on  the CI  
* QTBUG-96574 Qt Quick API cannot render password protected PDF files  
* QTBUG-100839 qmllint guesses wrong about scope in so-called  
unqualified access  
* QTBUG-99103 QQuickMessageDialog: Remove binding loop in non-native  
implementation  
* QTBUG-101327 FAIL!  : qquicklayouts::tst_gridlayout::compile in  
QNX_710  
* QTBUG-101072 Choosing a project name with a dash inside creates a  
broken cmake configuration  
* QTBUG-101341 Some autotests cannot find libraries to which it is  
indirectly dependent (quicktest)  
* QTBUG-101174 Qt Design Studio crashes when built with Qt 6.3 Beta  
* QTBUG-101006 tst_qquickiconimage fails on Android  
* QTBUG-101342 tst_qmltc::listView() is flaky under QNX qemu and Android  
* QTBUG-101451 qtdeclarative/tests/manual/pointer lacks a CMakeLists.txt  
file  
* QTBUG-100938 MessageDialog layout is rather "spacy"  
* QTBUG-101193 Link to Transition QML type is wrong  
* QTBUG-83630 Qt Quick Control 2 Tooltip can be way too big when you  
have newlines  
* QTBUG-94764 REG: Attached ToolTips shrink  
* QTBUG-101704 Imagine style ToolTip calculates its width incorrectly  
* QTBUG-101678 tst_qqmlinspector (and other tests in  
tests/auto/qml/debugger/) times out on macOS 12 (x86_64) in CI  
* QTBUG-101662 Dialog Header/Footer cover over background instead of  
being inset  
* QTBUG-75202 tst_qquicklistview::contentHeightWithDelayRemove() is  
flaky on macOS 10.12  
* QTBUG-89456 QTypeTraits templates break existing code  
* QTBUG-95940 tst_qquicktextinput paste-related tests are flaky on  
OpenSUSE  
* QTBUG-102030 Uncontrolled crash in tst_qwebenginepage  
* QTBUG-96582 QtQC2 MacOS style theme switching not fully implemented  
* QTBUG-102345 QtQuick rectangle has one pixel spacing on Android  
* QTBUG-100697 Disappearing glyphs when application font reloaded  
* QTBUG-87250 When using RowLayout inside a Page which is inside an  
ApplicationWindow then it can cause a binding loop on implicitWidth  
* QTBUG-99104 QQuickMessageDialog: Footer has a larger boundingBox than  
it should on non-basic styles  
* QTBUG-77202 No touch release event for AbstractButton inside of  
ListView with pressDelay set  
* QTBUG-102447 tst_drawingmodes failed  
* QTBUG-102462 tst_qquickitem2 fails on Android  
* QTBUG-102036 Release and Clicked not fired for Buttons in ListView  
with pressDelay set with touch screen  
* QTBUG-102037 Invalid value of pressed property in ListView delegate  
* QTBUG-102384 JS Stack Overflow test fails on Android  
* QTBUG-96788 Javascript code causes segfault in iOS when using Qt debug  
library  
* QTBUG-102589  tst_SceneGraph::render fails on Android  
* QTBUG-102721 QQuickWindow::grabWindow() broken on Android  
* QTBUG-102833 tst_qqmlenginecleanup::test_customModuleCleanup() broken  
on Android  
* QTBUG-102780 Vulkan-based rendering test flaky on Android  
* QTBUG-102858 tst_quick_examples fails on Android  
* QTBUG-101972 "Killed process: No output received (timeout: 15m0s  
seconds)" when running tst_QQmlDebugJS  
* QTBUG-102984 tst_QQmlDebugJS hangs on macOS in CI  
* QTBUG-103099 tst_qquickcanvasitem fails on Android  
* QTBUG-103078 tst_qquickwindow fails on Android  
* QTBUG-103077 tst_qquickborderimage tests fail on Android  
* QTBUG-103076 tst_qquickanimatedimage::mirror_* tests fail on Android  
* QTBUG-103072 tst_TapHandler::gesturePolicyDragWithinBounds fails on  
Android  
* QTBUG-103068 tst_PointHandler::tabletStylus() fails on Android  
* QTBUG-103066 tst_QQuickPinchHandler::scaleNativeGesture() fails on  
Android  
* QTBUG-103065 tst_HoverHandler::movingItemWithHoverHandler() fails on  
Android  
* QTBUG-103080 tst_qquickdeliveryagent::passiveGrabberOrder() fails on  
Android  
* QTBUG-103082 tst_qquickdrag tests fail on Android  
* QTBUG-103083 tst_QQuickDropArea::signalOrder() fails on Android  
* QTBUG-103047 tst_qquickimageprovider::requestImage_sync fails on  
Android  
* QTBUG-103086 tst_qquickfocusscope::canvasFocus() fails on Android  
* QTBUG-103088 tst_qquickitemlayer tests fail on Android  
* QTBUG-103089  
tst_QQuickListView::QTBUG_48044_currentItemNotVisibleAfterTransition()  
fails on Android  
* QTBUG-103096 tst_qquicktext fails on Android  
* QTBUG-103094 tst_qquickshape tests fail on Android  
* QTBUG-103092 tests in tst_qquickmousearea fail on Android  
* QTBUG-103098 tst_qquicktextedit fails on Android  
* QTBUG-103064 tst_DragHandler::touchDragMulti fails on Android  
* QTBUG-103061 tst_FlickableInterop tests fail on Android  
* QTBUG-103044 tst_qmlcppcodegen on Android complains module  
"Qt.labs.folderlistmodel" is not installed  
* QTBUG-103060 tst_qquicklayouts::Tests_GridLayout::test_spacings fails  
on Android  
* QTBUG-91163 cannot build some modules with -developer-build on 32bit  
architectures without -no-warnings-are-errors  
* QTBUG-102330 "Creating C++ Plugins for QML" docs need to be updated  
with cmake use  
* QTBUG-103204 tst_cursor: webOS handles arrow cursor as bitmap cursor  
* QTBUG-103256 tst_qquicktextinput fails on Android  
* QTBUG-103257 tst_qquickcanvasitem crashes on Android  
* QTBUG-103258 tst_qquickrendercontrol fails on Android  
* QTBUG-103260 tst_qquickanimatedsprite fails on Android  
* QTBUG-103310 tst_qqmlbinding::delayed() crashes on Android  
* QTBUG-103280 tst_qquickpixmapcache: webOS always tries to load from  
cache  
* QTBUG-99545 App crashes in function QQmlPropertyCache::property(int)  
const on ARM 64bit  
* QTBUG-100073 Conan: leaf module options are missing -no-feature  
possibility  
* QTBUG-79280 Closing Popup with escape key does not close the expected  
popup  
* QTBUG-103766 MouseArea onRelease event is not triggered after second  
finger touch'n'release  
* QTBUG-103205 SpinBox, no way to listen for text entered  
* QTBUG-103881 FAIL!  : tst_RayCastingJob::worldSpaceRayCaster(short  
ray)  
* QTBUG-102403 QObject::objectName() leads to heap-use-after-free in  
tst_qquickanimations::cleanupWhenRenderThreadStops()  
* QTBUG-102862 Build failure with lttng enabled  
* QTBUG-102595 Builds can't find the projects qml modules  
* QTBUG-104157 Delegate Controls documentation: Introduction and details  
out of sync  
* QTBUG-97092 spelling errors reported by lintian  
* QTBUG-104671 qmllint does not see QColor and QQuickIcon  
* QTBUG-86729 many Qt Quick test failures after input event refactoring  
* QTBUG-101736 QQuickWidget: button in a popup doesn't receive touch end  
event  
* QTBUG-89927 tst_qquickfontloader::changeFontSourceViaState fails with  
macOS 10.15 and Xcode 12.3  
* QTBUG-89933 tst_HoverHandler fails with macOS 10.15 and Xcode 12.3  
* QTBUG-104687 qmlsc miscompiles registers only set in in one of two  
alternative branches of execution  
* QTBUG-10684 Interaction between text input and flickable is lacking  
* QTBUG-94919 Control changes hover state even though it is disabled  
* QTBUG-90494 TextField selectByMouse flag is by default set to false  
* QTBUG-105190 tst_QQuickListView2::flickDuringFlicking is flaky  
* QTBUG-105149 QML ComboBox displays an unwanted shadow effect on  
Android  
* QTBUG-105238 Cmake error with -DQT_BUILD_MANUAL_TESTS=ON  
* QTBUG-105277 Issues with changing mipmap for image elements  
* QTBUG-105354 QSGRenderNode / View3D's Inline mode has no way to gain  
access to the render target/pass descriptor when within an item layer  
* QTBUG-99578 Global Functions are Undocumented  
* QTBUG-103513 A11Y: Flickable child item focus frame position not  
updated  
* QTBUG-105610 should be able to add a DragHandler to a Button or other  
control  
* QTBUG-101499 FAIL!  : tst_QQuickMultiPointTouchArea::nonOverlapping in  
Ubuntu_20_04  
* QTBUG-106365 qmlsc doesn't find modules from sysroot  
  
### qtactiveqt  
* QTBUG-99294 In ActiveQtServer derived from QMainWindow, when  
PushButton exists Lables in StatusBar can not be shown  
* QTBUG-100332 dumpcpp silently generates uncompilable files for some  
.NET libraries  
* QTBUG-100145 ActiveQt example "outlook" build fails with a wall of  
errors: MSOUTL.cpp(346616): error C2062: type 'unknown-type' unexpected  
  
### qtmultimedia  
* QTBUG-97780 Video object does not throw an error when source path is  
not resolved  
* QTBUG-99142 QtMultimedia: Invalid target given to  
qt_is_imported_target: Qt6::QSGVivanteVideoNodeFactory  
* QTBUG-99129 Android media player isSeekable() always returns true  
* QTBUG-99183 Fix processEOS test in Android  
* QTBUG-99181 Fix loadMediaInLoadingState test  
* QTBUG-99182 Fix unloadMedia test  
* QTBUG-99134 Declarative Camera issues on video  
* QTBUG-99210 Fix playPauseStop test in Android  
* QTBUG-96985 Video and MediaPlayer don't allow to use relative URLs  
* QTBUG-99296 Crash when recording audio-only after video recording  
* QTBUG-99176 Recorder example: Crash when switching audio input off  
* QTBUG-97817 Camera example doesn't work  
* QTBUG-99564 QGstreamerMediaDevices::addDevice fails to detect device  
type  
* QTBUG-99358 Fix SurfaceTest Test in Android  
* QTBUG-99359 Fix Metadata Test in Android  
* QTBUG-99360 Fix audioVideoAvailable Test in Android  
* QTBUG-99661 audioDevice & cameraDevice list properties as methods  
* QTBUG-99650 QVideoSink unworkable on Android  
* QTBUG-97838 Recording broken on Apple Silicon / M1  
* QTBUG-99583 Default audio output device not listed as default in  
MediaDevices.audioOutputs  
* QTBUG-99357 Fix SeekPauseSeek Test in Android  
* QTBUG-99849 Doc refers to nonexistent QImageCapture::CaptureToBuffer  
setting.  
* QTBUG-100050 [REG 6.2.3(and 2)->6.2.1] namespace build fails on  
Windows, MinGW9.0 and MSVC2019  
* QTBUG-100106 Qml Video::seek() fails with TypeError  
* QTBUG-99643 Documentation shows use of deleted QImageCapture  
constructor  
* QTBUG-100283 "Video" keep sending positionChanged signal  
* QTBUG-100341 [REG 6.2.2 - 6.2.3] Memory leak on MediaPlayer  
destruction  
* QTBUG-100501 Typo in documentation of QMediaRecorder  
* QTBUG-100363 [REG 6.2.2 - 6.2.3] Video is always black with OpenGL RHI  
* QTBUG-100337 [Win] Vertically oriented video is upside down  
* QTBUG-100638 SoundEffect fails to load .wav files  
* QTBUG-100665 Crash in OpenGlVideoBuffer destructor  
* QTBUG-100181 QMediaPlayer::setPosition doesn't jump to precisely  
position while playing an FLAC file  
* QTBUG-100773 Android Multimedia arm64v8a target Huawei P40 Lite  
Android 10 QML Recorder example wont work  
* QTBUG-100299 Android: Unloaded multimedia plugins  
* QTBUG-99641 MacOS Monterey - QCamera stops render after a second  
* QTBUG-101518 Missing main.qml in Multimedia examples  
* QTBUG-100835 [WMF] Resuming a video after pause generates WMF error  
* QTBUG-100854 [WMF] Crash on resuming playback of specific video  
* QTBUG-101434 QMediaRecorder is stop write to file after bluetooth  
headset is reconnected  
* QTBUG-101591 MediaRecorder/CaptureSession doesn't release audio input  
(mic) on stop recording  
* QTBUG-101719 [REG6.3.0beta2->beta3] some multimedia examples not  
compiling on macOS  
* QTBUG-99361 Fix videoDimensions Test in Android  
* QTBUG-98262 Recording with audio fails on macOS 10.15 (Catalina)  
* QTBUG-99228 Qt-6.2.2 Example declarative-camera crash on Android 6.0.1  
* QTBUG-99093 Android tst_qvideoframe autotest failed  
* QTBUG-102962 Android: Update audio subsystem for SampleFormat::Float  
* QTBUG-102707 Several videos can't be played simultaneously with OpenGL  
RHI  
* QTBUG-102588 MediaMetaData.Duration not updated  
* QTBUG-102969 After changing the position QMediaPlayer::setPosition in  
the pause state, a sound is heard  
* QTBUG-103272 [Windows] Crash in MFPlayerSession::createSession()  
* QTBUG-102843 Audioinput example: [5.15 -> 6.3] a lot of noise for the  
volume level  
* QTBUG-60575 QtSpeech flite backend not working on Ubuntu Linux  
* QTBUG-103394 QMediaCaptureSession crashes with QCoreApplication  
* QTBUG-102645 build errors in multimedia  
* QTBUG-99094 Android tst_qaudiodecoderbackend test failed  
* QTBUG-103853 QMediaPlayer position error when rewind  
* QTBUG-99095 Android tst_QAudioSource test failed  
* QTBUG-104401 Typo in ffmpeg plugin name  
* QTBUG-104520 GDI leak in MediaPlayer  
* QTBUG-104433 Compile error GeneralBlockPanelKernel.h:27:56 in dev  
armeabi-v7a build  
* QTBUG-104483 ASSERT: "viewport.size() == size" in  
qquickvideooutput.cpp  
* QTBUG-104045 wasm: QSoundEffect no sound happens  
* QTBUG-104919 During update dependency Cmake generate failed at  
qtmultimedia repository  
* QTBUG-104133 QML animation overlaid on video becomes unusably slow &  
with increasing memory consumption over time  
* QTBUG-105001 Spatial audio example crash on Windows  
* QTBUG-102772 Declarative-camera preview freezes when takes photo  
* QTBUG-105381 Qt Multimedia fails to read crop info from a HEVC video  
stream's VPS.  
* QTBUG-105819 FTBFS with ffmpeg >= 5.1  
* QTBUG-105344 [Reg 5.15 -> 6.3] QMediaPlayer rewind  
(setPlaybackRate(-1.0) jumps to end-of-file  
* QTBUG-96599 No documentation for how to support different video  
formats  
* QTBUG-98419 [macOS] Audio Recorder example crashes on start on macOS  
10.15 (Catalina)  
* QTBUG-99038 Android:  Fix qmlvideo issues  
* QTBUG-96776 Rename/replace \qmlbacsictype with \qmlvaluetype  
* QTBUG-100079 Android: fix QAndroidAudioDecoder issues  
* QTBUG-99969 QVideoSink and QCamera very slow  
* QTBUG-102029 Android camera preview broken in Qt 6.2.4 (regression)  
* QTBUG-102306 Fix qdoc warnings in mediaplayer.qdoc  
* QTBUG-103567 QML MediaPlayer fails to playback rtsp media properly.  
* QTBUG-97492 QAudioSink returns always UnderrunError on Android  
* QTBUG-103591 Windows: Comboboxes (Qml and QtWidgets) don't have the  
UIAutomation (UIA) ExpandCollapse pattern  
* QTBUG-98121 Android: Filters out unsupported audio codecs(flac) on  
AudioRecorder app  
* QTBUG-99022 Android: Changing a Audio sink on Audiooutput example  
issue  
* QTBUG-105619 FFMPEG: sound volume is not editable in Media Player  
* QTBUG-105521 Mediaplayer working with ffmpeg hangs on playback rate  
changing  
* QTBUG-105617 FFMPEG: Video and audio are not synchronized after  
changing playback rate  
  
### qttools  
* QTBUG-99232 REG->6.3: Linguist occasionally asserts  
* QTBUG-99404 Qt Designer: Crash when editing spacer objectName in the  
Object Inspector Tab  
* QTBUG-99409 qdoc: Trailing newline in the master .qdocconf fails the  
build.  
* QTBUG-99740 qdoc: Automatic \inmodule resolution fails in some  
environments  
* QTBUG-100316 qdoc: ASSERT: "actualNode" in file  
qttools/src/qdoc/docbookgenerator.cpp, line 4246  
* QTBUG-100357 Dependency update on qt/qttools failed in dev  
* QTBUG-100308 Unable to build qttools with tests with the 'Ninja Multi-  
Config' generator  
* QTBUG-100310 lupdate does not support trailing commas in Python  
* QTBUG-95236 qttools fails configure with deactivated features.  
* QTBUG-96549 make clean removes ts file when using  
qt5_create_translation()  
* QTCREATORBUG-27087 Bad colors for Stylesheet editor in dark mode  
* QTBUG-101070 Qhelpgenerator endless loop with -c option  
* QTBUG-101893 The 'help' example should only build if 'Qt::Help' is  
built  
* QTBUG-93238 [REG 5.15.2 -> 6.0.3] Cannot build docs with static build  
of Qt  
* QTBUG-101319 Multiple qt_add_translations does not work in static  
projects  
* QTBUG-101461 qdoc does not parse ref-qualified member functions  
* QTBUG-101782 lrelease does not respect EXTRA_TRANSLATIONS in pro file.  
* QTBUG-102332 qdoc "documented multiple times" warning is bogus  
* QTBUG-101523 Linguist does not honor its input format specification  
* QTBUG-102179 QDoc does not find any header file when  
headers.fileextensions is not declared  
* QTBUG-102832 Qt Linguist incorrectly translates some language names  
* QTBUG-102387 qdoc: Fix inconsistency in breadcrump menu for sub-  
imports  
* QTBUG-48104 QUiLoader calls property setter twice while loading an ui-  
file  
* QTBUG-102088 Automatically generated "New QML Properties", "New QML  
Methods" miss type information  
* QTBUG-102342 List of all members misses inherited method with same  
name (but different signature)  
* QTBUG-103470 [iOS] CMake translation handling fails  
* QTBUG-103797 error C2220: the following warning is treated as an  
error: \Users\qt\work\qt\qttools\src\shared\qttoolbardialog\qttoolbardia  
log.cpp(1068): warning C4996: 'QTreeWidgetItem::setTextAlignment': Use  
the overload taking Qt::Alignment  
* QTBUG-103747 DocBook links to previous/next page are invalid  
* QTBUG-103749 DocBook examples: paragraphs outside  
* QTBUG-104216 Order of "New Member Functions" is indeterministic  
* QTBUG-99421 Some Qt5 ui file does not compile with Qt6  
* QTBUG-103863 \qtcmakepackage docs in qdoc manual are partially  
misplaced  
* QTBUG-100837 Assistant: PageUp/PageDown keys scrolls 2 pages not 1  
* QTBUG-104369 qdoc should prefer links to a type's own API rather than  
outside targets when encountering ambiguity  
* QTBUG-99415 lupdate ignores tr() call in a function with noexcept  
operator  
* QTBUG-104490 qhelpgenerator can't find QSqlDatabase drivers in static  
builds  
* QTBUG-104713 GCC 12: failure to build from source [<QtTools>]  
* QTBUG-105130 qttools: CMake failure if litehtml is found on the system  
* QTBUG-104633 'examplesinstallpath' configuration variable is not  
documented  
* QTBUG-105278 qdoc: WebXML generator drops some  text fragments  
* QTBUG-105097 \since says the macro is a function even if it isn't  
* QTBUG-105987 Make order of elements in .qhp deterministic  
* QTBUG-94345  Qt Designer crash in QQuickWidget plugin  
* QTBUG-100285 Windows: Qt Designer crash when selecting QWebEngineView  
* QTBUG-100073 Conan: leaf module options are missing -no-feature  
possibility  
* QTBUG-104377 Qt Designer: Alignment property moves to wrong place in  
property editor  
* QTBUG-91521 When calling lupdate on a file that uses QT_TR_NOOP in a  
constructor for a static QString it will fail to find the context  
* QTBUG-104426 lupdate uses return type as context for free functions  
* QTBUG-86507 ASSERT: "it.isUnused()" in file  
/home/qt/work/install/include/QtCore/qhash.h, line 525  
* QTBUG-104903 Remove Cpp.ignore* qdocconf settings  
  
### qtdoc  
* QTBUG-99167 XML support in Qt talks about XML Pattern  
* QTBUG-99847 Update Qt Creator info in Qt Quick tutorial  
* QTBUG-99967 List new modules in 6.3 overview documentation  
* QTBUG-100126 WebAssembly (WASM) Set Up Doc Updates  
* QTBUG-100434 Tutorials/alarms not launching on macOS  
* QTBUG-101652 MessageDialog and FolderDialog links are wrong in What's  
New docs  
* QTBUG-99667 Document CMake API changes in 6.3 Overview  
* QTBUG-103466 Update "Implementing Atomic Operations" section  
* QTBUG-103468 Update or delete "Qt Commercial License" page  
* QTBUG-100690 WebAssembly (WASM) MEMORY Doc fixes  
* QTBUG-93471 Darwin linker warns about global weak symbols when linking  
an executable against a static Qt  
* QTBUG-96151 QML deployment docs need to be rewritten  
* QTBUG-105006 iOS archive builds fail with qt_add_qml_module()s in  
static libs  
* QTBUG-97449 Clean Android build docs for Qt 6  
* QTBUG-98542 new purchasing is broken on Android when using public key  
verification  
* QTBUG-101267 Examples not running on browser on Windows: missing .js  
file  
* QTBUG-101370 Doc about Mac deployment lacks critical info for Qt 6  
* QTBUG-102268 There is no possibility to attach egl lib dependencies  
for Integrity  
* QTBUG-101320 Apps targeting Android 12 or higher must explicitly  
declare the android:exported attribute for app components  
* QTBUG-102304 Update documentation how to build iOS projects with cmake  
* QTBUG-103597 sgexamples qtdoc test fails on Android  
* QTBUG-102972 [REG 6.3.0 -> 6.4.0] apps crash on Android device  
* QTBUG-101323 Apps running on Android 12 and above must comply with the  
latest Unicode version  
  
### qtpositioning  
* QTBUG-99329  
org.qtproject.qt.android.positioning.QtPositioning.positionUpdated calls  
non-existent method  
* QTBUG-102836 Configure fails when trying to configure QtPositioning  
with -no-dbus  
* QTBUG-103807 QGeoAreaMonitorSource seg fault on exit on Android  
* QTBUG-103907 sccache: error: failed to store  
`mocs_compilation.cpp.obj` to cache  
* QTBUG-103478 QGeoPositionInfoSource on Android always asks for  
location permission  
* QTBUG-92967 Port addon-module cmake tests from Qt5 to Qt6  
* QTBUG-101345 FAIL!  :  
tst_DeclarativePositionSource::supportedMethodsBinding in QNX_710  
* QTBUG-96776 Rename/replace \qmlbacsictype with \qmlvaluetype  
* QTBUG-102994 Adding the Qt Bluetooth module produces a Makefile that  
looks for "user32.lib.lib" and "runtimeobject.lib.lib"  
* QTBUG-104448 Fix QtPositioning tests for static builds  
* QTBUG-104465 It is impossible to build tests with custom plugins in  
static build configurations  
  
### qtsensors  
* QTBUG-101931 error C2220: the following warning is treated as an  
error: warning C4996: 'QByteArray::count': Use size() or length()  
instead.  
* QTBUG-105848 FAILED: src/plugins/sensors/iio-sensor-  
proxy/properties_interface.h  
* QTBUG-102256 Some examples not compiling on iOS: "duplicate symbol for  
architecture arm64"  
* QTBUG-102994 Adding the Qt Bluetooth module produces a Makefile that  
looks for "user32.lib.lib" and "runtimeobject.lib.lib"  
  
### qtconnectivity  
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
* QTBUG-98973 BT LE Server to keep advertising also after its connected  
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
* QTBUG-101953 Windows BT COM initialization is incomplete  
* QTBUG-101984 Windows bluetooth socket not marked as unbuffered  
* QTBUG-102178 Test #10: tst_qbluetoothserver failed  
* QTBUG-102479 QBluetoothDeviceDiscoveryAgent should fail on macOS if  
provided with invalid address  
* QTBUG-102412 tst_qbluetoothlocaldevice::tst_pairDevice doesn't pass in  
manual mode on Windows  
* QTBUG-70222 Qt  Bluetooth LE doesn't detect Battery services  
* QTBUG-102442 Bluetooth hostmode change Discoverable=>Connectable  
doesn't work on Android  
* QTBUG-102319 Android BT service discovery agent crash when stopped  
* QTBUG-102874 Failing tst_qbluetoothlocaldevice (hostmode and manual  
pairing) on Android  
* QTBUG-102367 (potential BiC) Exported class QNdefMessage inherits from  
QList  
* QTBUG-103067 QBluetoothServer leaks RFCOMM and L2CAP Linux sockets  
* QTBUG-103826 Fix bluetooth deprecation warnings on macOS/iOS  
* QTBUG-103209 As a user who compiles Qt himself, I'm left in the dark  
regarding the configuration of QtConnectivity  
* QTBUG-104105 Bluez LE advertiser dispose crash when bluetooth off  
* QTBUG-104106 Android Bluetooth LE claims to advertise even if  
bluetooth off  
* QTBUG-104060 Bluez LE controller crash on too large advertisement data  
* QTBUG-104479 (Classic) bluetooth service scan sometimes hangs  
indefinitely on Android  
* QTBUG-97797 QBluetoothDeviceDiscoveryAgent take CPU/Ram usage to 100%  
* QTBUG-105556 BT LE repeated characteristic recurses into event loops  
until it crashes on Windows  
* QTBUG-105803 tst_qbluetoothdevicediscoveryagent and  
tst_qbluetoothservicediscoveryagent fail on Android 12 in CI  
* QTBUG-106029 Crash during device discovery in Qt RO bleclient example  
* QTBUG-105742 Memory leak in BLE discovery  
* QTBUG-98781 BT LE test case platform support enhancement  
* QTBUG-84234 Start new QCoreApplication after shutdown  
* QTBUG-98351 Thread-safe Android BT LE Java implementation  
* QTBUG-99222 Re-enable Bluetooth autotests on macOS  
* QTBUG-98955 tst_QBluetoothServiceInfo::tst_assignment fails on macOS  
12 ARM  
* QTBUG-98817 In QtConnectivity multiple QBluetooth autotest failures  
with macOS 12 ARM64  
* QTBUG-100042 Windows BT (server) pingpong service is not found  
* QTBUG-99685 Windows BT classic service scan doesn't always start  
* QTBUG-94001 QtBluetooth uses deprecated Windows API  
* QTBUG-101309 Bluez handle Enhanced LE connection complete  
* QTBUG-102256 Some examples not compiling on iOS: "duplicate symbol for  
architecture arm64"  
* QTBUG-99578 Global Functions are Undocumented  
* QTBUG-102994 Adding the Qt Bluetooth module produces a Makefile that  
looks for "user32.lib.lib" and "runtimeobject.lib.lib"  
* QTBUG-101066 QBluetoothServiceDiscoveryAgent::finished sometimes  
(spuriously) is not emmited on Android 10  
* QTBUG-97092 spelling errors reported by lintian  
* QTBUG-104914 tst_qbluetoothlocaldevice and tst_qbluetoothserver tests  
fail on Android 12 emulator in CI  
  
### qtwayland  
* QTBUG-90530 Low resolution title bar icon on Wayland on Hi DPI  
displays  
* QTBUG-92249 quick3d examples crashes or hangs on exit on wayland  
* QTBUG-95032 Dialogs on Wayland/Sway not drawn correctly when using  
client side decorations  
* QTBUG-96222 Some particular animations are too slow in vulkan backend.  
* QTBUG-99760 CMake warns about linking to plugins  
* QTBUG-99746 QtWayland fails to compile against recent EGL headers  
* QTBUG-97593 Qt with QtWayland doesn't build without QtQml  
* QTBUG-99802 qtwayland doesn't have all options in qt_cmdline.cmake  
* QTBUG-99965 Build with -no-feature-tabletevent fails for Linux/Wayland  
* QTBUG-100475 qtwayland features are misdetected  
* QTBUG-59627 Crash when window decorations are disabled (or switching  
to fullscreen)  
* QTBUG-100467 Window geometry is not updated when toggling the  
frameless window flag  
* QTBUG-100845 Cannot compare two const QWaylandBufferRefs  
* QTBUG-87303 Wayland context menus can go off the screen because Qt  
does not do set_constraint_adjustment  
* QTBUG-100942 Mouse button kept pressed state after closing the window  
in mouse press handler  
* QTBUG-101726 Main thread blocked after resizing window  
* QTBUG-102148 qtwayland contains invalid qt_attribution.json file  
* QTBUG-100148 Hover state of QCombobox has not been reset  
* QTBUG-102185 Fix remaining Qt Wayland Compositor documentation  
warnings  
* QTBUG-102601 Calculation of GlobalPos  
* QTBUG-102379 Fix PresentationTime qml module documentation  
* QTBUG-101366 Failure with more than one EGL-based client buffer  
integration  
* QTBUG-101862 [Wayland] Shortcut no longer activated after Alt+Tab when  
using WaylandCompositor/WaylandOutput in QML application  
* QTBUG-102829 [Wayland] Multitouch is not working in Qt6  
* QTBUG-103341 build fails without xkbcommon  
* QTBUG-103378 Some return values are ignored, causing warnings  
* QTBUG-102626 Crash with invalid min/max sizes  
* QTBUG-103391 crash on start: The Wayland connection experienced a  
fatal error: Protocol error  
* QTBUG-104227 QWaylandTextInput: Not possible to inject keys with  
Shift- or Ctrl-Modifiers  
* QTBUG-85297 Menu location is offset depending on  
xdg_output.logical_layout in sway  
* QTBUG-105308 ASSERT failure in QWindow: "Updates can only be scheduled  
from the GUI (main) thread"  
* QTBUG-100150 Touch event ignored when main GUI thread is slow  
* QTBUG-100792 tst_QScreen::grabWindow() fails on Wayland  
* QTBUG-101145 Disable "Pick color" in QColorDialog when unavailable  
* QTBUG-104435 Build failure in qtwayland with libcxx  
* QTBUG-66818 tst_QWindow::initialSize fails on Wayland  
  
### qt3d  
* QTBUG-101176 Linker error when AVX2 is disabled in core but enabled in  
Qt3D  
* QTBUG-102328 Qt3D.Core can't be imported from a static Qt build  
* QTBUG-104593 Qt3D Application Crashes when rendering first frame  
* QTBUG-99945 [REG 6.2.2-> 6.2.3] qt3d/audio-visualizer-qml fails to  
compile  
* QTBUG-100147 error: member reference base type 'char' is not a  
structure or union  
* QTBUG-100360 Crash in qt3d/src/render/jobs/renderviewjobutils.cpp  
(207)  
* QTBUG-100568 Crash in Renderer::cleanupShader  
* QTBUG-101949 A crash occurred in C:\Users\qt\work\qt\qt3d_standalone_t  
ests\tests\auto\render\scene2d\tst_scene2d.exe.  
* QTBUG-101595 [REG 6.2.4->6.3&4.0]qt3d/qardboard fails to compile  
* QTBUG-100073 Conan: leaf module options are missing -no-feature  
possibility  
* QTBUG-103218 [REG 6.3.0->6.3.1] qt3d examples not compiling on iOS  
* QTBUG-95650 Qt3D Light Module is not working.  
* QTBUG-100402 Light uniform is hardcoded to use PointLight only  
* QTBUG-104592 RHI Render Capture crashed with debug build  
* QTBUG-104534 QImage received from QRenderCapture using Qt3D RHI  
renderer causes crash.  
  
### qtimageformats  
* QTBUG-103454 Null-dereference read in QICNSHandler  
* QTBUG-103337 Vulnerabilities in bundled libtiff version  
* QTBUG-104398 Segmentation fault in Jpeg2000JasperReader when Jasper 3  
is used  
* QTBUG-104692 qtimageformats breaks top-level build  
  
### qtserialbus  
* QTBUG-96566 Serialbus can example fails to build  
* QTBUG-101689 QtSerialbus library linking is done using wrong Network  
library interface  
* QTBUG-101351 QModbusClient::processResponse() is never called  
* QTBUG-103879 [Reg 5.15.2 -> 5.15.9] QModbusClient:: sendRawRequest()  
produces ModbusDevice::UnknownError when there is no error  
* QTBUG-100073 Conan: leaf module options are missing -no-feature  
possibility  
  
### qtserialport  
* QTBUG-102001 error C2220: the following warning is treated as an error  
qserialportinfo.cpp(131): warning C4996: 'QScopedPointer<QSerialPortInfo  
Private,QSerialPortInfoPrivateDeleter>::swap': Use std::unique_ptr  
instead of QScopedPointer.  
* QTBUG-101444 QSerialPort: trouble with high baud rates /  
waitForReadyRead() stalls  
* QTBUG-103822 QSerialPort::waitForReadyRead always returns false on  
older Windows systems  
* QTBUG-91237 QSerialPort: moving / resizing / clicking window title bar  
blocks serial port read/write  
* QTBUG-87151 QSerialPort: synchronous read fails as waitForReadyRead()  
always times out.  
  
### qtwebsockets  
* QTBUG-100054 QWebSocket can emit binaryMessageReceived signal after  
being disconnected  
* QTBUG-102111 Custom http header on wss connection  
* QTBUG-101682 QtWebAssembly: Uncaught exception when using  
QWebSocket::sendBinaryMessage() with threaded application  
* QTBUG-105851 tst_QWebSocketServer::tst_handshakeTimeout fails  
* QTBUG-106372 wasm: Using WebSockets from worker threads fail to work  
* QTBUG-92967 Port addon-module cmake tests from Qt5 to Qt6  
* QTBUG-101333 FAIL!  : tst_QWebSocketServer::tst_handleConnection in  
QNX_710  
* QTBUG-102713 tst_QWebSocketServer has failing tests on Android  
* QTBUG-105087 [REG: 6.3->6.4] wasm: Use after free due to pointer to  
temporary data being used  
  
### qtwebchannel  
* QTBUG-92967 Port addon-module cmake tests from Qt5 to Qt6  
* QTBUG-101521 FAIL!  : qml::tst_bench::compile in QNX_710  
  
### qtwebengine  
* QTBUG-99282  
3rdparty/chromium/content/public/common/content_switches.h:13:10: fatal  
error: 'media/media_buildflags.h' file not found  
* QTBUG-95568 Possible deadlock at QtWebEngine Startup  
* QTBUG-99511 Top level cross build fails  
* QTBUG-99526 developer tools no longer highlights page elements when  
inspecting them  
* QTBUG-99485 Qt WebEngine AutomationId issue  
* QTBUG-99263 QProcess::finished not emitted  
* QTBUG-99215 Html popups do not work correctly.  
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
* QTBUG-68820 simplebrowser crashes when passing command line argument  
"-type=1"  
* QTBUG-101084 Test  #1: tst_qwebenginecookiestore  
.................***Failed  
* QTBUG-100996 WebEngine crashes in Accessibility  
* QTBUG-96574 Qt Quick API cannot render password protected PDF files  
* QTBUG-100672 Universal builds of WebEngine fail on M1 mac  
* QTBUG-101290 Unable to build examples when building as module with  
-DQT_BUILD_EXAMPLES=ON  
* QTBUG-96525 QWebEngineScript::setSourceUrl doesn't load scripts from  
qrc  
* QTBUG-94368 [QtPDF] bitcode bundle could not be generated because  
libQt5Pdf.a was built without full bitcode  
* QTBUG-94046 QtPDF: configuration with -static-runtime causes linker  
errors for projects  
* QTBUG-86948 When using QImageReader to load a PDF then the PDF images  
can be blurry and seem to be at half the size they should be  
* QTBUG-101706 [REG] ASSERT: "event->reason() != Qt::PopupFocusReason"  
in file \Users\qt\work\qt\qtwebengine\src\webenginewidgets\render_widget  
_host_view_qt_delegate_widget.cpp, line 79  
* QTBUG-101724 Application crash when trigger  
QWebEnginePage::triggerAction( QWebEnginePage::InspectElement )  
* QTBUG-101935 FAIL!  : tst_QWebEnginePage::pasteImage() Compared values  
are not the same  
* QTBUG-100839 qmllint guesses wrong about scope in so-called  
unqualified access  
* QTBUG-94963 QWebEngineLoadingInfo::errorDomain() returns  
WebEngineError::InternalErrorDomain when there is no error  
* QTBUG-100806 QMimeData::html() returns undesirable meta data  
* QTBUG-92539 Weird behavior when pasting certain HTML into element with  
contentEditable attribute set  
* QTBUG-101201 Failed to compile xkb_symbols with multiple layout  
* QTBUG-102303 QtPdf views: get Controls styling working better  
* QTBUG-102746 PdfMultiPageView: starts out with pages centered  
horizontally, switches to left-aligned after using the search results  
sidebar  
* QTBUG-102742 QtPDF MultiPageView: fix horizontal scrolling  
* QTBUG-102743 Version getters are undocumented  
* QTBUG-100799 Dictionaries not found in spellchecker bundle dir on  
macOS  
* QTBUG-100300 cups-config: No such file - build error in  
cups_config_helper.py  
* QTBUG-103217 QtWebEngineQuick form select field popups do not react on  
touch press  
* QTBUG-79254 QWebEngineView couldn't handle touch events for html  
select's popup menus  
* QTBUG-103372 [REG 6.2 -> 6.3] QT_QUICK_BACKEND=software segfaults with  
QtWebEngine in QSGSoftwareRenderableNode::update  
* QTBUG-101030 The zoom factor is reset every time QtWebEngine loads a  
new website  
* QTBUG-103778 [REG 5.15 -> 6.2] ERR_NETWORK_ACCESS_DENIED when clicking  
link from local page  
* QTBUG-102740 PdfMultiPageView: following search results scrolls around  
more than necessary  
* QTBUG-102394 Pdf rendering very slow using Qt Pdf module  
* QTBUG-102951 Qt PDF cannot coexist with TIFF Qt Image Formats plugin  
in statically-linked app  
* QTBUG-96377 Using QWebEngineView::setPage() on page already active  
* QTBUG-103735 QWebEnginePage::iconChanged() not emitted  
* QTBUG-103578 WebEngine: Error when linking gn  
* QTBUG-103579 Qt PDF: Static build fails on macOS  
* QTBUG-92932 [REG 5.12 -> 5.13] QWebEngineUrlRequestInterceptor doesn't  
get called for websocket connections  
* QTBUG-101769 Qt WebEngine reports wrong UIAutomation bounding rects  
with high DPI  
* QTBUG-54433 Support of datalist  
* QTBUG-105134 WebEngineView is crashing while loading the pdf file  
* QTBUG-105082 QtWebEngine freezes on specific Chromium debug command  
* QTBUG-86871 Qt WebEngine incompatible with Selenium's "sendKeys"  
method  
* QTBUG-103760 Conan: Qt WebEngine resources not found  
* QTBUG-104436 V8 error when using WebEngine with --single-process and  
proxy auto-config  
* QTBUG-105072 [REG 6.4] Initial widget focus is wrong  
* QTBUG-106090 moc_qquickwebenginesingleton_p.cpp:38:69: error: use of  
undeclared identifier 'QtMocHelpers'; did you mean  
'::TestNamespace::TestNamespace::QtMocHelpers'?  
* QTBUG-106210 Dependency update on qt/qtwebengine failed in dev  
* QTBUG-105955 [REGRESSION] Web Engine views are painted only partially  
* QTBUG-105960 QtQuick: WebEngineView scaling regression (Windows)  
* QTBUG-106355 QtPDF: crash when pinch-zooming on a PDF page with text  
on iOS  
* QTBUG-100391 Application built with Qt 6.2.2 fails to run because of  
missing mf.dll error  
* QTBUG-99119 [REG 5 -> 6] Segfault in  
QtWebEngineCore::WebContentsDelegateQt::webEngineSettings() on Google  
Meet  
* QTBUG-98941 [Qt5.15.4][QWebEngine]QWebEnginePage::print() function  
printing a grey paper while printing a PDF in Qt5.15.4  
* QTBUG-50686 QWebSettings::LocalContentCanAccessRemoteUrls not working  
with audio tags  
* QTBUG-82873 import QtQml in dependencies doesn't work on static builds  
if omitted from the main qml  
* QTBUG-101215 QML certifciate errror test is broken, but works on c++  
side  
* QTBUG-87154 Add static dependencies from 3rdparty in qtbase  
* QTBUG-100404 Changes around WebEngineScript are not documented  
* QTBUG-100713 Qt WebEngine: --disable-gpu does not disable GPU  
* QTBUG-100435 Cannot enable webrtc-pipewire feature  
* QTBUG-102253 tst_qwebengineview (Failed)  
* QTBUG-102156 QtPdf: stop using private API  
* QTBUG-102323 cmake seems to treat builddir as a regex and fails if  
builddir contains quantor characters (+)  
* QTBUG-102192 Navigation on drop broken  
* QTBUG-100073 Conan: leaf module options are missing -no-feature  
possibility  
* QTBUG-103859 qt-testrunner.py ERROR: exception:ParseError no element  
found  
* QTBUG-103354 Test #12: tst_uidelegates  
...........................***Failed  
* QTBUG-101744 tst_uidelegates most tests fail on macOS  
* QTBUG-104057 Dependency update fails: error: no matching member  
function for call to 'addAction'  
* QTBUG-99445 quicknanobrowser crashes with --single-process  
* QTBUG-99207 [REG: 5.14.2->5.15.0] Redirection from file to custom url  
schemes does not work  
* QTBUG-104238 [REG 5.15 -> 6.3] Widevine fails on specific sites  
* QTBUG-102099 QWebEngineView ColorPicker  is not modal and freezes  
application  
* QTBUG-102633 [Windows] Linking errors in Blink  
* QTBUG-103221 QtPDF examples are not installed with 6.3.0  
* QTBUG-105342 Test on qemu are very flacky  
* QTBUG-105818 gio is not detected correctly  
* QTBUG-106072 QtPdf can't open password-protected PDF files on Windows  
* QTBUG-106406 gn not build in host build when not building QtWebEngine  
or QtPdf at the same time  
* QTBUG-106461 QWebEngineUrlRequestJob::reply() does not support a  
QIODevice that cannot be read completely instantly  
  
### qtwebview  
* QTBUG-99372 FAILED: tests/auto/webview/qwebview/tst_qwebview  when  
builing for QNX  
* QTBUG-86533 Yocto and QNX builds are missing -rpath-link linker flag  
which causes non-prefix builds to fail  
* QTBUG-102801 qtwebview setAndDeleteCookie tests crash on Android  
* QTBUG-101487 FAIL!  : tst_QWebView::load in QNX_710  
* QTBUG-101520 FAIL!  : tst_QQuickWebView::stopEnabledAfterLoadStarted  
in QNX_710  
* QTBUG-102712 qtwebview tests fail on Android  
  
### qtcharts  
* QTBUG-100810 QML ChartView series color can get wrong on RHI if  
useOpenGL  
* QTBUG-102140 error C2220: the following warning is treated as an  
errorchartpresenter.cpp(141): warning C4996:  
'QScopedPointer<ChartAxisElement,QScopedPointerDeleter<T>>::take  
* QTBUG-102286 [REG 5.15 -> 6.2] QTChartView zoom area does not work in  
x direction  
* QTBUG-101945 Changing to QValueAxis::TicksDynamic on horizontal axes  
moves ticks to the opposite side  
* QTBUG-99190 Performance issue with VXYModelMapper  
* QTBUG-102392 X-axis vanishes when difference between min and max is  
less than two  
* QTCREATORBUG-27650 Pie Chart Customization Example doesn't scale  
properly  
* QTBUG-92967 Port addon-module cmake tests from Qt5 to Qt6  
* QTBUG-101517 FAIL!  : example::tst_barcategoryaxis::compile in QNX_710  
* QTBUG-102723 tst_qpieslice and tst_qpieseries fail on Android  
* QTBUG-102722 tst_QAreaSeries has test failures on Android  
* QTBUG-102725 charts_qml (tst_qml) fails on Android  
* QTBUG-100073 Conan: leaf module options are missing -no-feature  
possibility  
  
### qtdatavis3d  
* QTBUG-100400 API review Qt 6.2.0. -> Qt 6.3 issue  
* QTBUG-99724 qtnetwork examples fail on configure on Wasm: missing  
Qt6::DataVisualizationPrivate  
* QTBUG-102139 C4996 MSVC deprecation warnings are treated as an error  
* QTBUG-102735 ERROR: The test executable CRASHed uncontrollably!  
* QTBUG-104714 Dependency cycle between QtDatavisualization and  
QtDatavisualizationQml  
* QTBUG-105398 Q3DScatter should fail gracefully when mesh is missing UV  
coordinates  
* QTBUG-101513 FAIL!  : qmltest::tst_category::compile in QNX_710  
* QTBUG-102256 Some examples not compiling on iOS: "duplicate symbol for  
architecture arm64"  
  
### qtvirtualkeyboard  
* QTBUG-92212 QtVirtualKeyboard needs to use declarative type  
registration  
* QTBUG-95680 QtQuick.VirtualKeyboard versioning is broken  
* QTBUG-95660 qmllint complains a lot about Qt Virtual Keyboard  
* QTBUG-102737 ERROR: The test executable CRASHed uncontrollably!  
* QTBUG-94770 [Qt Virtual keyboard] Keyboards doesn't respond when  
QT_SCALE_FACTOR  is set to 1.5  
* QTBUG-105685 [REG 6.3.2->6.4.0] virtualkeyboard/basic not compiling on  
iOS  
* QTBUG-97439 [REG 5.15.2->6.2] Virtual Keyboard is hidden by QML dialog  
* QTBUG-97830 Some Qt Virtual Keyboard tests checking the position of  
selection handles are failing  
* QTBUG-101512 FAIL!  : inputpanel::tst_inputpanel::compile in QNX_710  
* QTBUG-101536 FAIL!  : styles::tst_styles::compile in QNX_710  
* QTBUG-100883 qmlcachegen miscompiles QVariant of QObject* to bool  
conversion  
* QTBUG-102152 qmlcachegen miscompiles something  
* QTBUG-102756 qtvirtualkeyboard tests fail on Android  
  
### qtscxml  
* QTBUG-102252 tst_qqmlstatemachine (Failed)  
* QTBUG-102284 Qt Scxml examples fail to link when using a static Qt  
* QTBUG-103396 error: reference to non-static member function must be  
called  
* QTBUG-99545 App crashes in function QQmlPropertyCache::property(int)  
const on ARM 64bit  
* QTBUG-98368 Dependency cycle in qtscxml  
* QTBUG-92967 Port addon-module cmake tests from Qt5 to Qt6  
* QTBUG-101343 FAIL!  : tst_statemachineqml::tst_anonymousstate::compile  
in QNX_710  
* QTBUG-100073 Conan: leaf module options are missing -no-feature  
possibility  
  
### qtspeech  
* QTBUG-84213 QTextToSpeech::availableVoices() does not list all voices  
* QTBUG-85019 Wrong math for QTextToSpeechEngineIos  
* QTBUG-82545 TextToSpeech say_hello fails on multiple platforms  
* QTBUG-55274 [qtspeech] Re-enable blacklisted autotests  
* QTBUG-105477 Doc: TextToSpeech links to QML type  
* QTBUG-82978 Allow "-Wextra-semi-stmt" on Q_UNUSED  
* QTBUG-86969 Rename org/qtproject/qt5 ?  
* QTBUG-103770 Doc: Re-add Qt Text to Speech module to All Qt Modules  
  
### qtremoteobjects  
* QTBUG-99269 tst_Integration_External test is failing on MacOS-arm64  
* QTBUG-100358 Dependency update on qt/qtremoteobjects failed in dev  
* QTBUG-85124 QRemoteObjectHost::hostUrl() crashes if no URL is set  
* QTBUG-102852 tst_usertypes::remoteCompositeType fails on Android  
* QTBUG-104098 Update dependencies on '6.4' fails in qt/qtremoteobjects  
* QTBUG-74124 QAbstractItemModelReplica internal error crash  
* QTBUG-97790 Generated SourceAPI class can't be used without compiler  
warnings  
* QTBUG-105597 tst_Server_Process failed  
* QTBUG-106003 remoteobjects does not checks for Declarative's private  
headers existance, but makes use of them  
* QTBUG-92967 Port addon-module cmake tests from Qt5 to Qt6  
* QTBUG-101336 FAIL!  : ModelreplicaTest::basicFunctions in QNX_710  
* QTBUG-101384 QtRO: Fix compiler warnings for QNX  
* QTBUG-97092 spelling errors reported by lintian  
  
### qtquick3d  
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
* QTBUG-100832 View3D.mapFrom3DScene crashes for large values  
* QTBUG-99759 Dynamically creating and destroying models causes  
assertion failure  
* QTBUG-100009  
qtquick3d/src/runtimerender/graphobjects/qssgrenderparticles.cpp:57:33:  
error: call of overloaded sqrt(int&) is ambiguous  
* QTBUG-101373 Item2D node rendered indefinitey on threaded render loop,  
blocks updates on basic render loop  
* QTBUG-101882 Particle shapes don't support reparenting  
* QTBUG-101638 GLSL version logic can use some improvements (was: Quick  
3D shader error on Linux)  
* QTBUG-102209 no-opengl build fails on quick3d  
* QTBUG-102305 [REG 6.3.0->6.4.0] quick3d/skinning not launching:  
"SimpleSkinningNew is not a type"  
* QTBUG-102293 QML profiler shows texture load for each frame for  
Quick3D  
* QTBUG-93883 Joint indexes is limited inside one skeleton element  
* QTBUG-102850 Parallax Correction issue when the probe is not  
positioned at the center  
* QTBUG-102023 Incorrect shadows from SpotLight and PointLight  
* QDS-6761 Model Picking is not working correctly  
* QTBUG-102193 Negative joint index leads to crashes  
* QTBUG-104118 [REG 6.3 -> 6.3.1] Global scaling does no longer work in  
3D asset imports  
* QTBUG-105131 QtQuick3D fails to build in C++20 mode  
* QTBUG-105293 Particles3D sortMode example crashes with distance mode  
* QTBUG-105354 QSGRenderNode / View3D's Inline mode has no way to gain  
access to the render target/pass descriptor when within an item layer  
* QTBUG-105549 customshaders example's Texture with Item option does  
nothing  
* QTBUG-103265 Shader compilation failure when setting height map  
* QTBUG-105565 [REG 6.3.2 -> 6.4.0] Highlighted example  
principledmaterial UI has a big empty space section  
* QTBUG-97692 Incorrect rendering when using external camera and  
Temporal AA  
* QTBUG-106037 issue when enabling Reflection Probe Debug View  
* QTBUG-105918 REG: Jittery skeletal animations  
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
* QTBUG-101718 [REG 6.3.0beta2->beta3] quick3d/principledmaterial not  
launching on macOS  
* QTBUG-102711 tst_MultiWindow crashes on Android  
* QTBUG-102710 tst_RenderControl fails on Android  
* QTBUG-99948 Fix enum/enum arithmetic in Qt  
* QTBUG-105566 Touch panning a ListView in View3D broken  
  
### qtshadertools  
* QTBUG-93101 qtdeclarative FTBFS on ppc64 & s390x  
* QTBUG-103723 [iOS] CMake shader handling fails  
  
### qt5compat  
* QTBUG-100024 qt5compat requires qtdeclarative despite it's not really  
required  
* QTBUG-100359 tst_qlinkedlist.cpp doesn't build: missing  
QLinkedListIterator  
* QTBUG-102254 tst_qtextcodec (Failed)  
* QTBUG-103927 GCC 12: failure to build from source [<Qt5Compat>]  
* QTBUG-99545 App crashes in function QQmlPropertyCache::property(int)  
const on ARM 64bit  
* QTBUG-89702 Improve the QRegExp->QRegularExpression docs  
  
### qtmqtt  
* QTBUG-105873 QMqttClient documentation does not include the  
constructor  
  
### qtopcua  
* QTBUG-102149 Invalid license file reference in  
./src/3rdparty/open62541/qt_attribution.json  
* QTBUG-104646 [C++20 FTBFS] open62541.h is running afoul of volatile  
compound statement deprecation in C++20  
* QTBUG-100007 qtopcua fails to integrate due to flaky  
opcua::SubscriptionsTest  
* QTBUG-96283 [REG 6.1.3->6.2.0] macOS: Can not configure qml / network  
example with statically compiled Qt  
* QTBUG-103905 No target "OpenSSL::SSL" failure on qtopcua dependency  
update  
  
### qtlanguageserver  
* QTBUG-99236 Qt Language server documentation missing  
* QTBUG-103924 GCC 12: failure to build from source [<QtDeclarative>]  
  
### qthttpserver  
* QTBUG-79345 QHttpServer doesn't compile with gcc4.8.3  
* QTBUG-79411 QHttpAbstractServer does not follow server listen()  
convention  
* QTBUG-89381 Can't Compile QtHttpServer with Qt 6.0.0  
* QTBUG-100479 QtHttpServer: Fix failing SSL auto tests  
* QTBUG-100476 QtHttpServer: fix QtConcurrent usage  
* QTBUG-100570 QtHttpServer: missing optional dependency on qtwebsockets  
* QTBUG-100533 QtHttpServer: Missing socket error handling in QSslServer  
* QTBUG-102000 error C2220: the following warning is treated as an error  
agent qhttpserverrequest_p.h(86): warning C4996: 'qGlobalQHashSeed': Use  
QHashSeed instead  
* QTBUG-103248 warning C4996: 'QtLiterals::operator ""_qs': Use _s from  
Qt::StringLiterals namespace instead  
* QTBUG-104097 error: no matching constructor for initialization of  
'QSslServer'  
* QTBUG-104538 tst_QAbstractHttpServer::websocket() memleak  
* QTBUG-104481 QtHttpServer::route()/afterRequest(): Compile errors when  
assigning the lambda to variable and passing that  
* QTBUG-104710 Windows: Enum naming QHttpServerRequest::DELETE clashes  
with winnt.h define of the same name  
* QTBUG-105330 QHttpServer statusString map is missing a few of status  
codes  
* QTBUG-105306 QHttpServerRequest::Method is undocumented  
* QTBUG-105723 QtHttpServer examples are not visible in QtCreator  
* QTBUG-74882 QHttpServer crashes when lambda catches `this`  
* QTBUG-76619 QHttpServerResponse is missing a QJsonArray constructor  
* QTBUG-82053 QtHttpServer crashes when CONNECT method is used  
* QTBUG-84617 QHttpServer crashes when disconnected from client before  
finishing reply  
* QTBUG-85191 QHttpServerFutureResponse.obj symbols already defined in  
qexception.obj  
* QTBUG-100478 QtHttpServer: reorganize branching and get rid of compat  
code in dev  
* QTBUG-103712 qhttpserver ssl tests fail on Android  
* QTBUG-106160 tst_QAbstractHttpServer::fork() is flaky  
  
### qtquick3dphysics  
* QTBUG-104903 Remove Cpp.ignore* qdocconf settings  
  
Known Issues  
------------  
  
* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-6.4/supported-platforms.html  
* RTA reported issues from Qt 6.4  
https://bugreports.qt.io/issues/?filter=24174  
* Supported development platforms are listed here:  
https://bugreports.qt.io/browse/QTBUG-102789  
* See Qt 6.4.0 Known Issues from:  
https://wiki.qt.io/Qt_6.4.0_Known_Issues  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Mike Achtelik  
Cristian Adam  
Chris Adams  
Laszlo Agocs  
Waqar Ahmed  
Dimitrios Apostolou  
Soheil Armin  
Viktor Arvidsson  
Albert Astals Cid  
YAMAMOTO Atsushi  
Mahmoud Badri  
Mate Barany  
Vladimir Belyavsky  
Nicholas Bennett  
Tobias C. Berner  
Chen Bin  
Alex Blasche  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
Mikolaj Boc  
Sören Bohn  
Francisco Boni  
Tatiana Borisova  
Joerg Bornemann  
Assam Boudjelthia  
Kai Uwe Broulik  
Florian Bruhin  
Jonah Brüchert  
Michael Brüning  
Marco Bubke  
Igor Bugaev  
Andreas Buhr  
Kirill Burtsev  
Jungi Byun  
Luca Carlon  
Ryan Chu  
Joel Clay  
Marcus Comstedt  
Alexandru Croitor  
Mitch Curtis  
Thibaut Cuvelier  
Giuseppe D'Angelo  
Szabolcs David  
Noah Davis  
Anton Demchenko  
Knud Dollereder  
Artem Dyomin  
Alexey Edelev  
David Edmundson  
Oliver Eftevaag  
Balazs Egedi  
Christian Ehrlicher  
Iikka Eklund  
Hatem ElKharashy  
Andreas Eliasson  
Mario Emmenlauer  
Tunahan Erkoyuncu  
Fabio Falsini  
David Faure  
Björn Feber  
Ilya Fedin  
Nicolas Fella  
Jesus Fernandez  
Ben Fletcher  
Kevin Funk  
Samuel Gaist  
Sylvain Garcia  
Pekka Gehör  
Roman Genkhel  
Christophe Giboudeaux  
Frederik Gladhorn  
Maximilian Goldstein  
Andrei Golubev  
Jeremie Graulle  
Robert Griebl  
Patrick Griffis  
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
Andre Hartmann  
Andreas Hartmetz  
Simon Hausmann  
Elias Hautala  
Jani Heikkinen  
Miikka Heikkinen  
Christian Heimlich  
Karsten Heimrich  
Chris Hennes  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Dominik Holland  
Mats Honkamaa  
Sam James  
Agnieszka Jaworska  
Nils Jeisecke  
Allan Sandfeld Jensen  
Tim Jenssen  
Hu Jialun  
Yin Jie  
William Jones  
Janne Juntunen  
Maurice Kalinowski  
Jonas Karlsson  
Johannes Kauffmann  
Youngjin Kim  
Friedemann Kleint  
André Klitzing  
Michal Klocek  
Lars Knoll  
Seokha Ko  
Jarek Kobus  
Kai Koehne  
Sze Howe Koh  
Jarkko Koivikko  
Antti Kokko  
Łukasz Korbel  
Tomi Korpipaa  
Jani Korteniemi  
Janne Koskinen  
Fabian Kosmale  
Volker Krause  
Mike Krus  
Jaroslaw Kubik  
Konrad Kujawa  
Marcel Kummer  
Simeon Kuran  
Sona Kurazyan  
Igor Kushnir  
Jonas Kvinge  
Kai Köhne  
Inho Lee  
Tony Leinonen  
Paul Lemire  
Qiang Li  
Jasper Limbago  
Moody Liu  
Jonathan Liu  
Robert Loehning  
Jenny Lofthus  
Robert Löhning  
Thiago Macieira  
Tamas Martinec  
Tamás Martinec  
Sérgio Martins  
Sergio Martins  
Thorbjørn Lund Martsum  
Ievgenii Meshcheriakov  
Leena Miettinen  
Samuel Mira  
Fawzi Mohamed  
Bartlomiej Moskal  
Andrey Mozzhuhin  
Marc Mutz  
Miklós Márton  
Tommi Mänttäri  
Antti Määttä  
Sivan Nanthiran  
Martin Negyokru  
Alexander Neumann  
Delf Neumärker  
Guineng Ni  
Andy Nichols  
Yuya Nishihara  
Mårten Nordheim  
Tadej Novak  
Sukyoung Oh  
Kimmo Ollila  
Tinja Paavoseppä  
Laszlo Papp  
Bumjoon Park  
Cathy Park  
Fan PengCheng  
Pasi Petäjäjärvi  
Thomas Piekarski  
Samuli Piippo  
Timur Pocheptsov  
Milla Pohjanheimo  
Joni Poikelin  
Aleix Pol  
Alessandro Portale  
Rami Potinkara  
Lorn Potter  
Liang Qi  
Umair Raihan  
Martin Reboredo  
David Redondo  
Arno Rehn  
Topi Reinio  
Aleksandr Reviakin  
André de la Rocha  
Rafael Roquetto  
Bernhard Rosenkraenzer  
Johannes Rosenqvist  
Niclas Rosenvik  
Elias Rudberg  
Shawn Rutledge  
Toni Saario  
Ahmad Samir  
Michael Saxl  
Lars Schmertmann  
Eli Schwartz  
Björn Schäpers  
Craig Scott  
Luca Di Sera  
Dmitry Shachnev  
Sami Shalayel  
Ye ShanShan  
Orgad Shaneh  
Tianlu Shao  
Andy Shaw  
Venugopal Shivashankar  
Kristoffer Skau  
David Skoland  
Ivan Solovev  
Axel Spoerl  
Michael Spork  
Piotr Srebrny  
Elias Steurer  
Patrick Stewart  
Martin Storsjö  
Brett Stottlemyer  
Christian Strømme  
Frank Su  
Tasuku Suzuki  
Mikhail Svetkin  
Jan Arve Sæther  
Morten Sørvig  
Morten Johan Sørvig  
Nodir Temirkhodjaev  
Benjamin Terrier  
Marcus Tillmanns  
Duan Ting  
Ivan Tkachenko  
Kenneth Topp  
Pino Toscano  
Mike Trahearn  
Jens Trillmann  
Alex Trotsenko  
Jere Tuliniemi  
Paul Olav Tvete  
Sami Varanka  
Peter Varga  
BogDan Vatra  
Louis du Verdier  
Doris Verria  
Tor Arne Vestbø  
Petri Virkkunen  
Harald Vistnes  
Jannis Voelker  
Alexander Volkov  
Ville Voutilainen  
Juha Vuolle  
Jaishree Vyas  
ChunLin Wang  
Stefan Wastl  
Michael Weghorn  
Bernd Weimer  
Edward Welbourne  
Fushan Wen  
Niklas Wenzel  
Clemens Werther  
Jeremy Whiting  
Paul Wicking  
Anna Wojciechowska  
Oliver Wolff  
Alvin Wong  
Jiang Wu  
Li Xinwei  
Weng Xuetian  
Lu YaNing  
Xiao YaoBing  
Zhang Yong  
Vlad Zahorodnii  
JiDe Zhang  
Yuhang Zhao  
Volodymyr Zibarov  
Eike Ziller  
hjk  
