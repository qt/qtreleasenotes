Release note  
============  

Qt 6.2 introduces many new features and improvements as well as bugfixes  
over the 6.1.x series. For more details, refer to the online  
documentation included in this distribution. The documentation is also  
available online:  
  
https://doc.qt.io/qt-6/index.html  
  
The Qt version 6.2 series is binary compatible with the 6.1.x series.  
Applications compiled for 6.1 will continue to run with 6.2.  
  
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
* fccd419dd6 Remove false Q_UNREACHABLE from shaping code  
Fixed a possible crash with certain fonts when shaping strings  
consisting only of control characters.  
  
* ef763e1958 Fix crash when requesting A32 glyph on Wayland  
Fixed crash when calling QRawFont::alphaMapForGlyph() with subpixel  
antialiasing on Wayland.  
  
* faebfdea1b Long live VK_KHR_display platform plugin!  
Introduced a vkkhrdisplay platform plugin to run Vulkan-based  
applications in fullscreen, without a windowing system, on systems where  
VK_KHR_display and VK_KHR_display_swapchain are supported by the Vulkan  
implementation.  
  
* 9d84bafeba Make it possible to disable the PrintSupport module  
Building of QtPrintSupport can be disabled by passing -no-feature-  
printsupport to configure.  
  
* 6512a7fc64 Restore pre-Qt6 QList::fill() behavior  
Fixed QList::fill() regression introduced in 6.0: calling fill() with  
size < current list size wouldn't truncate the list  
  
* d8158c6c93 macOS: Be honest about the system locale  
QLocale::system() on macOS no longer pretends to support LANG or other  
environment variables as overrides, as this is not a feature that the  
system locale on macOS supports. To override the locale of an  
application, use QLocale::setDefault(), or pass -AppleLocale en_US.  
  
* 6862ce3d77 QMatrix4x4: deprecate operator*(QMatrix4x4,  
QVector3D/QPoint(F))  
operator* between a QMatrix4x4 and a QVector3D, QPoint, or QPointF has  
been deprecated in favor of map() and mapVector().  
  
* 654a216499 QMatrix4x4: deprecate operator*(QVector3D, QMatrix4x4)  
The multiplication operator (operator*) between a QVector3D and a  
QMatrix4x4 has been deprecated. User code needs to extend the QVector3D  
to a QVector4D first (by specifying the intended w coordinate), and then  
multiply the QVector4D by the matrix.  
  
* 3cf84287e7 Prepare TextDate to use UTC-offset rather than GMT-offset  
zone suffixes  
The Qt::TextDate format now recognizes UTC-based offset suffixes in  
addition to suffixes based on the deprecated alias GMT. This prepares  
for toString() to use such UTC-based suffixes for time-zones  
(fromString() cannot parse the present abbreviation suffix). A future  
release of Qt shall use UTC-based suffixes in place of the present GMT-  
based suffixes (which conflict with GMT-based IANA zone names) for  
Qt::LocalTime and Qt::OffsetFromUTC time-specs. Client code is  
encouraged to use and recognize UTC-based zone suffixes in preparation  
for that transition, unless compatibility with versions before 6.2 is  
required.  
  
* 517578e071 QDateTime::toString(): use UTC-offset as time-zone suffix  
When spec is Qt::TimeZone, the offset-suffix now used for the  
toString(Qt::TextDate) format is now a UTC-based offset string,  
compatible with the parsing (now) supported by fromString(). The zone-  
abbreviation suffix in use since 5.9 was not parseable.  
  
* c462793d67 Drop parsing of antique TextDate format  
The parsing of Qt::TextDate in QDateTime::fromString() no longer  
supports the old TextDate format used (only) on Windows by Qt < 5.2  
("ddd d. MMM yyyy" with an "HH:mm:ss" time either appended or inserted  
before "yyyy").  
  
* 73a04edce1 QProcess::startDetached: set the error condition on failure  
to start  
If a startDetached() fails to start the target application, the  
QProcess object should now have a proper error string in errorString().  
  
* 1f30bcf336 Move build tools to libexec instead of the bin dir  
Tools that are called by the build system and are unlikely to be called  
by the user are now installed to the libexec directory.  
  
* 0e22001a3b Add more support for structured bindings  
QSize is now usable in a structured binding declaration.  
  
* fe9d7bf759 QScopedPointer: deprecate swap  
QScopedPointer swapping functions have been deprecated, as they would  
allow the managed pointer to escape the scope. If you need those  
semantics, use std::unique_ptr instead.  
  
* ede0082f86 Update bundled libjpeg-turbo to version 2.0.6  
libjpeg-turbo was updated to version 2.0.6  
  
* 224c638f78 QProcess/Unix: use a common function to find the target  
executable  
startDetached() now supports launching .app executable bundles on macOS  
/ iOS systems, like start() already did.  
  
* 83876c0256 QNetworkInterface/Unix: fix DNS eligibility of global  
addresses  
Fixed the reporting the "DNS eligibility" factor  
(QNetworkAddressEntry::dnsEligibility) for global IP addresses.  
Previously, QNetworkInterface interface erroneously reported all global  
addresses as eligible, regardless of whether they had already been  
deprecated by the OS or were temporary in the first place.  
  
* 7fd9ed3201 Support family names that end/start with space  
Fixed matching against fonts which has a family name that ends or  
starts with a space.  
  
* 022fd8e79c SQLite: Update to 3.35.2  
Updated SQLite to v3.35.2  
  
* 14f9f00fdb QSqlQuery: make it a move only type  
QSqlQuery copy operations have been deprecated. QSqlQuery copy  
semantics cannot be implemented correctly, as it's not generally  
possible to copy a result set of a query when copying the corresponding  
QSqlQuery object. This resulted in modifications on a QSqlQuery having  
visible (and unintended) side effects on its copies. Instead, treat  
QSqlQuery as a move-only type.  
  
* fef850c51a Extend qtpaths functionally to replicate the 'qmake -query'  
behavior  
qtpaths got new --qt-query argument that can be used instead of qmake  
-query. The new --qtconf, --query-format arguments allow you to further  
tweak its output.  
  
* b1377ed02d Add literal operators for QString and QByteArray  
Added literal operator u"..."_qs that converts a char16_t string  
literal to QString  
  
* bc00daae71 Add support to set thread priority to QThreadPool  
QThreadPool can now be configured to use a different thread priority  
when creating new threads than the one it inherits from the thread it  
was created in. This will only apply to the threads started after the  
property is changed.  
  
* 7473317b52 QTextHtmlParserNode: Limit colspan to avoid segfault  
QTextDocument::setHtml: column spans are limited to 20480, an  
arbitrarily high but reasonable value.  
  
* 2e6c37fe51 QCoreApplication::exit: make it a slot  
exit() is now a slot, like quit().  
  
* 86ad338aa4 Q{*String,ByteArray}View::length(): use qsizetype, not int  
The length() function now returns `qsizetype`, not `int`, for  
consistency with the other string and container classes in Qt. Following  
this change, it has been un-deprecated.  
  
* 50a7eb8cf7 Add the "Territory" enumerated type for QLocale  
QLocale now has Territory as an alias for its Country enumeration, and  
associated territory-based names to match its country-named methods, to  
better match the usage in relevant standards. The country-based names  
shall in due course be deprecated in favor of the territory-based names.  
  
* b322bfcc14 QString: add missing char8_t* constructor / fromUtf8  
overloads  
Added a constructor and a fromUtf8() overload taking a `const char8_t  
*` argument.  
  
* cf42a0fe5e Remove lazy binding evaluation  
QProperty uses always eager evaluation now when a dependency in a  
binding changes.  
  
* 7709463b55 QHash: allow an empty QT_HASH_SEED env variable to reset  
Previously, if the QT_HASH_SEED environment variable was set but empty,  
Qt would interpret that as if it had been set to 0, thus disabling the  
hash salting functionality. Since this makes setting and unsetting this  
variable difficult in scripts, it has been changed: if the variable is  
set but empty, it is interpreted now as if it had not been set and the  
hash salting functionality is enabled.  
  
* 6560778616 Read DPI from X Settings initially as well  
Qt now reads Xft/DPI from X settings at startup, and will prefer this  
value over Xft.dpi from X resources.  
  
* 284d4e7125 QLayout: mark unsetContentsMargins as the RESET function  
The unsetContentsMargins() function now acts as the RESET function for  
the contentsMargins property.  
  
* bcbbbdb2d6 Fix case sensitivity handling QSFPM  
Case sensitivity as well as regular expression options handling have  
been fixed. The original value is properly kept when using  
setFilterWildCard and setFilterFixedString. The regular expression  
options are now also properly kept when changing the case senstitivity  
through setFilterCaseSensitivity.  
  
* d385158d52 Move plugin code from QtNetwork to qtbase/plugins  
QSslSocket by default prefers 'openssl' backend if it is available.  
  
* 5fabad9a61 Long live PRI*Qdatatypes  
A series of PRIxQTDATATYPE macros have been added. They make it  
possible to print some Qt type aliases (qsizetype, qintptr, etc.) via a  
formatted output facility such as printf() or qDebug() without raising  
formatting warnings and without the need of a type cast.  
  
* 9bad096c09 Use a more forgiving threshold for qFuzzyIsNull(qfloat16)  
The qfloat16 threshold value for qFuzzyIsNull() has changed from 1e-3  
to 9.76e-3, almost a factor of ten increase, for consistency with  
qFuzzyCompare()'s tolerance. Values between these would previously have  
had qFuzzyIsNull(f) false despite qFuzzyCompre(f, 1+f) being true.  
  
* 0d76a5cd2c QSFPM: fix filterCaseSensitivityChanged signal emission  
logic  
A call to QRegularExpression overload of setFilterRegularExpression now  
emits a filterCaseSensitivityChanged signal, if required.  
  
* 808a6dedcb ItemViews: don't delete dragged items when a subclass  
accepted the move  
Classes overriding dropEvent for MoveAction events to move data can  
call accept() on the event before calling the superclass to prevent  
QAbstractItemView from deleting the source item.  
  
* 5e89c1406e Delete less-than operator for QKeyCombination  
Potentially source-incompatible change: the less-than operator for  
QKeyCombination has been deleted. Code relying on the deprecated  
implicit conversion to int will no longer compile. Use  
QKeyCombination::toCombined explicitly.  
  
* afd7460aff Add new app permissions API under QCoreApplication  
Add new API for handling app permissions with an initial implementation  
for Android.  
  
* 72a5151403 Write out the HTML correctly for nested lists  
The output of toHtml() now handles nested lists correctly.  
  
* 127f617387 Update bundled libjpeg-turbo to version 2.1.0  
libjpeg-turbo was updated to version 2.1.0  
  
* a1e405ce11 Windows: Work-around misreporting of Script and Roman  
Fixed text in "Roman" and "Script" bitmap fonts not showing in Qt Quick  
applications.  
  
* 76d3cda884 macOS: Fix synthesized bold  
Fixed an issue where boldness would not be correctly synthesized for  
families with no bold variant.  
  
* ca14ed494c QLocalSocket/Win: implement duplex communication in  
blocking mode  
The waitFor*() functions on Windows now support duplex operation, as  
they already did on Unix.  
  
* 688602704d Support CSS text-decoration-color in underlines, overlines,  
strikethrough  
The CSS text-decoration-color attribute is now supported in rich text  
spans with underlines, overlines and strikethrough.  
  
* d5c3e1336b Allow to load -developer-build without configurations into  
an IDE  
configure -developer-build now sets up the CMake File API query, so  
that a build can be loaded without reconfiguration into Qt Creator and  
other IDE's. Pass -developer-build -no-cmake-file-api to configure to  
disable this.  
  
* 300dec66ce QMetaMethod: Store method constness in metaobject system  
It is now possible to query the constness of a method with  
QMetaMethod::isConst.  
  
* 75d8623752 SQLite: Update SQLite to v3.35.5  
Updated SQLite to v3.35.5  
  
* 1a63217021 rhi: Fix memory leak  
Fixed a memory leak in QRhiGles2  
  
* f385b8827a Windows: Add synthesized fonts also when there is a style  
name  
Fixed an issue where bold/italic would not be synthesized for fonts if  
QFont::NoFontMerging was set.  
  
* e906bb84fb QFlags: add (named) explicit conversion from/to int  
Added the fromInt() and toInt() functions for explicit conversions  
from/to a plain integer.  
  
* ddee595d58 QFlags: add qHash overload  
QFlags now has a qHash() overload.  
  
* d2759e0e32 QFlags: add operator& / &= overloads taking a QFlags object  
The operator& and operator&= now accept a QFlags object.  
  
* 2be9e6cc26 Q_DECLARE_OPERATORS_FOR_FLAGS: also define operator&  
Bitwise AND-ing two values of an enum type for which flag operations  
have been declared now produces a QFlags object. Similarly, AND-ing a  
value of enum type and one of type QFlags now produces a QFlags object.  
Before, it produced an integer in both cases. This may introduce a  
slight incompatibility in user code; it is possible to keep the code  
working in Qt versions before and after this change by inserting enough  
conversions to QFlags, and/or by changing expressions such as `enum &  
flag` to `flag & enum` (the latter has always produced a QFlags object).  
  
* aafea67cf6 QFlags: add operator== and !=  
Added overloads of operator== and operator!= between QFlags objects,  
and between a QFlags object and an object of the flag's enumeration.  
  
* c8f380bd13 QPageSize: make PageSizeId ctor non-explicit  
Conversion from a QPageSize::PageSizeId is now implicit.  
  
* c4947c1c4c QFlags: add test(Any)Flag(s)  
The testFlags, testAnyFlag and testAnyFlags functions have been added.  
  
* 50c838d4b5 Make the exit() methods in QEventLoop and QThread be slots  
exit() is now a slot, like quit().  
  
* 9a94c4a415 Long live qToUnderlying  
The qToUnderlying function has been added, to convert an value of  
enumeration type to its underlying value.  
  
* 8278879c19 Fix QItemSelectionModel::selectionChanged emission  
QItemSelectionModel now emits the selectionChanged signal if only the  
indexes of the selected items change.  
  
* a5dc381b4c QByteArrayView: add compare  
Added compare(), enabling case sensitive and insensitive comparison  
with other QByteArrayViews.  
  
* 11a40defff Fix memory leak when using small caps font  
Fixed a memory leak when initializing a small caps font.  
  
* f1983dcdf6 Correct RGB to Grayscale conversion  
RGB conversions to grayscale formats are now gamma-corrected and  
produce color-space luminance values  
  
* 715041b663 Enable UNICODE for all Qt targets and Qt consumers by  
default  
Enables the UNICODE and _UNICODE definitions on WIN32 platforms by  
default for all cmake projects to reflect the qmake behavior. Use  
qt6_disable_unicode_defines function to disable the default unicode  
definitions.  
  
* 4b60cea602 Farewell Q_DISABLE_MOVE  
The Q_DISABLE_MOVE macro has been removed. Code that was using it can  
be ported to Q_DISABLE_COPY_MOVE instead.  
  
* ae02188233 QTestlib: Add formatting for QObject * in QCOMPARE  
QCOMPARE() now reports QObject * values by class and objectName().  
  
* 35412acd88 Use time-zone transition data before 1970 as well as after  
Available time-zone information is now used to its full extent, where  
previously QDateTime used LocalTime's current standard time for all  
dates before 1970. Where we have time-zone information, it is considered  
reliable, so we use it.  This changes the "best efforts" used for times  
outside the range supported by the system APIs, in most cases giving  
less misleading results.  
  
* 467b39d52c Fix license information for libjpeg-turbo  
Clarified that libjpeg-turbo is actually covered by three licenses, not  
only IJG.  
  
* 6829719575 macOS: allow Qt::AA_DontShowShortcutsInContextMenus  
overrides  
The shortcutVisibleInContextMenu property defaults to the value of the  
Qt::AA_DontShowShortcutsInContextMenus attribute, which in turn defaults  
to the platform integration. To override the default, set the  
application attribute after instantiating QApplication, or override the  
default for each QAction instance.  
  
* 3f8e0c3107 QVarLengthArray: fix aliasing error in insert(it, n, v)  
Fixed an aliasing bug affecting insertions of objects aliasing existing  
elements.  
  
* 7dfa2b68cd Revert "Windows: Add synthesized fonts also when there is a  
style name"  
Fixed a regression where different font styles and/or weights would not  
be available.  
  
* 70b3e6937b Remove ministro code  
Remove ministro code since it's been unmaintained and not working with  
recent Android versions.  
  
* 898bb35f84 Android: Make the manifest less to scary to read and edit  
Remove some elements from the manifest file that are internal, to make  
it easier to deal with the manifest.  
  
* 68f7aae466 QCryptographicHash: don't present the same data over and  
over again  
Fixed a bug where presenting more than 4GiB in a single addData() call  
would calculate the wrong result().  
  
* 528a0a03f1 Restore default installation prefix from Qt 5  
The installation prefix now defaults to /usr/local/Qt-${version} and  
C:/Qt/Qt-${version} like it did in Qt 5.  
  
* 045804c45d QLineEdit: don't change layout direction on keyboard input  
QLineEdit used to change the layout direction on each key press, based  
on the text content. This feature resulted in an inconsistent and  
erratic user experience, and has been removed.  
  
* 4b0cf03651 QLocalSocket/Win: destroy the pipe before emitting final  
signals  
QLocalSocket on Windows now emits both readChannelFinished() and  
disconnected() signals after closing the pipe and emitting  
stateChanged(UnconnectedState), which is consistent with the behavior on  
Unix.  
  
* b953b7440f Change QCollator's default locale to QLocale().collation()  
The default locale used by QCollator is now the collation locale of the  
default QLocale. This restores the ability (lost at 5.14) to control the  
locale used by QString::localeAwareCompare(), while retaining the use of  
a collation locale when the default is the system locale.  
  
* 8eda2c4c57 Consistent handling of disabled items in  
QItemSelectionModel  
All methods in QItemSelectionModel now consider only items which are  
marked as enabled and selectable as part of the selection.  
  
* f20f5b722f Make QFutureWatcher::isFinished() consistent with the  
watched QFuture  
The QFutureWatcher::isFinished() method now indicates if the related  
QFuture is finished, instead of indicating if the finished() signal was  
delivered. This makes it consistent with the future that is being  
watched.  
  
* 57015d8551 Remove special casing of HSL QColor comparison  
Equality on HSL colors is now raw value based like other color-formats,  
instead of being partially interpretation based.  
  
* 212954be8b CMake: Bump min required CMake version for shared Qt builds  
to 3.16  
Building Qt as shared libraries now requires CMake version 3.16 or  
later. Building user projects with CMake using that Qt installation also  
requires a CMake version of 3.16 or later.  
  
* 4b3ed8aa32 QByteArray: don't coerce negative to unsigned for any base  
QByteArray's formatting of negative whole numbers to bases other than  
ten now, like QString's (since Qt 6.0), formats the absolute value and  
prepends a minus sign.  
  
* 4a1618ab9d testlib: Deprecate QWARN() in favor of qWarning()  
QWARN() has been deprecated in favor of qWarning()  
  
* 851b6e9d10 QXpmHandler: fix re-entrancy bug in xpm_color_name  
Fixed a race condition when concurrently writing .xpm files.  
  
* 12917537fe QXpmHandler: actually limit characters-per-pixel to four  
Instead of writing a corrupt file, rejects to write XPM files with more  
than 64^4 colors (more than four characters per pixel) now.  
  
* 003fa58eef QListView: fix AdjustToContents (sizeAdjustPolicy)  
A more correct implementation of QListView::viewportSizeHint has been  
made. That implies that setting the sizeAdjustPolicy to AdjustToContent  
on QListView and QListWidget will now cause the view to size after the  
contents and avoid scrollbars.  
  
* c11a4d3432 MySQL: remove the version number checks in favor of actual  
functionality  
Fixed the detection of whether the client and server support prepared  
statements. This was caused by the mariadb connector library reporting  
its own version numbers (starting in version 3.2) instead of the server  
version.  
  
* 02bed8c646 Fix memory leak if eXIf has incorrect crc  
Fix for possible memory leak in libpng was backported.  
  
* f1641ed814 CMake: Bump min required CMake version for static Qt builds  
to 3.21  
Building Qt as static libraries now requires CMake version 3.21 or  
later. Building user projects with CMake using that Qt installation also  
requires a CMake version of 3.21 or later.  
  
* b4a1265b15 Fix printing with unhinted fonts  
Fixed an issue where the characters in printed text would look too  
small.  
  
* a7fa5b4b76 CMake: Don't install metatypes files for user projects  
qt6_extract_metatypes does not install metatypes files anymore. Instead  
the OUTPUT_FILES option can be provided to get the list of extracted  
files for further processing.  
  
* 432acc2794 Fix bug with NoFontMerging when font does not support  
script  
Fixed an issue with NoFontMerging and changing font families  
dynamically, where boxes would be seen in place of the correct text.  
  
* 75d699e1cd QS(V)/QBA(V)/QL1S::lastIndexOf: fix the offset calculations  
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
  
* 8890ca3d97 Update Harfbuzz to version 2.9.0  
Updated bundled Harfbuzz to version 2.9.0.  
  
* e18831961c Fix default line thickness for fonts  
Fixes an issue where underlines and other decorations would be too  
thick for some fonts.  
  
* 7eaa9942f6 NetworkAccessBackend: Remove the backend part of the name  
The NetworkAccessBackend plugin-type is renamed to NetworkAccess, if  
you have a plugin marked NetworkAccessBackend you need to change it to  
NetworkAccess.  
  
* b01986df91 Update bundled libjpeg-turbo to version 2.1.1  
libjpeg-turbo was updated to version 2.1.1  
  
* 4375a94b21 SQLite: Update SQLite to v3.36.0  
Updated SQLite to v3.36.0  
  
### qtsvg  
* f9ac5f3 Limit font size to avoid numerous overflows  
Avoid numerous overflows by limiting font size to 0xffff. This fixes  
oss-fuzz issue 31701.  
  
### qtdeclarative  
* 9ca63fbd0b Introduce a 'System' theme to the styles.  
Added Universal.System theme enum value, that can be used to let the  
Universal style choose either the light or dark theme based on the  
system theme colors.  
  
* 51c181776f SwipeView: add isNextItem and isPreviousItem attached  
properties  
Added isNextItem and isPreviousItem attached properties to make it  
straight-forward to use Loader for unloading pages that are outside the  
reach.  
  
* 3ec6f508aa StackView: add attached activated() etc. signals  
Added attached activated(), deactivated(), activating(), and  
deactivating() signals that are convenient for initializing and cleaning  
up item-specific resources.  
  
* d0a48ae26a Add ButtonGroup::clicked(AbstractButton) signal  
Added clicked(AbstractButton) signal for centralized click handling for  
grouped buttons.  
  
* 221c3ce846 Slider: expose valueAt(pos) for getting continuous value  
updates  
Added valueAt() method for getting continuous value updates.  
  
* 3e40325d44 Material: fix elevation effect for Frame, GroupBox, Pane &  
TabBar  
Fixed (optional) elevation effects for Frame, GroupBox, Pane, and  
TabBar.  
  
* bfb0a9ebe3 Add DialogButtonBox  
Added DialogButtonBox to provide convenience for handling dialog  
buttons. DialogButtonBox is able to create a set of standard buttons  
with a single line of QML code, and provides convenient accepted() and  
rejected() signals.  
  
* 6a8f7b88a7 Add QQuickContainer::increment|decrementCurrentIndex()  
Added incrementCurrentIndex() and decrementCurrentIndex() methods for  
changing the current index without losing its property binding.  
  
* 1e8e214805 Add SwipeView::interactive  
Added interactive property for controlling whether swipe interaction is  
enabled.  
  
* 4a92e38303 Tumbler: add wrap property  
Added wrap property to control whether or not tumbler wraps when it  
reaches the top and bottom.  
  
* fff036ab4d SpinBox: add up.hovered and down.hovered properties  
Added up.hovered and down.hovered properties that hold whether the  
respective buttons are hovered.  
  
* 97c88459d8 RangeSlider: add first.hovered and second.hovered  
properties  
Added first.hovered and second.hovered properties that hold whether the  
respective handles are hovered.  
  
* fa8cccf479 Tumbler: change default visibleItemCount to 5  
Changed the default value of visibleItemCount to 5 to make it visually  
clearer that it's a Tumbler.  
  
* 8ed484329f Universal: implement hover effects  
Implemented hover effects  
  
* 2c4b2d4882 Tumbler: make wrap property depend on count by default  
Changed the default value of wrap to be false when count is less than  
visibleItemCount. Explicitly setting wrap overrides this behavior.  
  
* 99c170e3fc Add pressed() and released() signals to TextField and  
TextArea  
Added pressed() and released() signals.  
  
* 1badc06b81 Be consistent with naming of event argument in  
pressAndHold() signals  
Aligned the name of the pressAndHold() argument with TextArea  
  
* 09706e8f9f Popup: expose flip API  
Added allowVerticalFlip and allowHorizontalFlip properties to control  
whether flipping is allowed to fit a popup inside the window.  
  
* 546544b347 SwipeDelegate: add swipe.close()  
Added swipe.close() for setting swipe.position to 0.  
  
* a26244b5c3 SwipeDelegate: add swipe.completed() signal  
Added swipe.completed() for responding to completion of swipes.  
  
* bc86a96c56 StackView: allow choosing which transition to run  
Made it possible to choose the visual transition type for any  
operation. This allows using for example push and pop transitions with  
replace(), which allows implementing an "infinite" back and forward  
navigation pattern while keeping the amount of instantiated items  
constant.  
  
* 4ac9693ef8 SwipeDelegate: add swipe.pressed and swipe.clicked()  
Added swipe.pressed and swipe.clicked() for detecting when non-  
interactive left/right/behind items are pressed and clicked.  
  
* 7a835a4b4e Add Dialog  
Added Dialog to provide convenience for handling dialog popups. Dialog  
integrates with DialogButtonBox, and provides convenient accepted() and  
rejected() signals.  
  
* 508bb6ddde Add MenuSeparator  
Added MenuSeparator to visually distinguish between groups of items in  
a menu.  
  
* 0bf6a3f425 Add ComboBox::flat  
Added a flat property that provides more suitable looks for using  
ComboBox in a ToolBar.  
  
* 87b21a5702 Make a plain Control calculate suitable implicit size  
A plain Control now calculates its implicit size based on the implicit  
size of the content item plus paddings, and the implicit size of the  
background item.  
  
* 0e01d1d979 Make a plain Container calculate suitable implicit size  
A plain Container now calculates its implicit size based on the  
implicit size of the content item plus paddings, and the implicit size  
of the background item.  
  
* 58326f2bc3 StackView: add removed() attached signal  
Added StackView.removed() attached signal to provide a way to delete  
items that StackView won't.  
  
* f6c3ecdb06 Add RoundButton  
Added RoundButton.  
  
* fbe806c544 Fix Popup to respect explicit size  
Fixed to respect explicitly set width and height.  
  
* 244356ba18 QQuickDrawer: allow resizing and positioning  
Made it possible to control the vertical position of a horizontal  
drawer, and vice versa. This allows placing a drawer below a  
header/toolbar, for instance.  
  
* fda44e6fed Make a plain AbstractButton calculate suitable implicit  
size  
A plain AbstractButton now calculates its implicit size based on the  
implicit size of the content item plus paddings, and the implicit size  
of the background item.  
  
* ae3e7f0799 Add QQuickTumbler::moving  
Added a moving-property that describes whether the tumbler is currently  
moving, due to the user either dragging or flicking the tumbler.  
  
* 47736b3510 Add QQuickSlider::live  
Added a live-property that determines whether the slider provides live  
updates for the value-property while the handle is dragged.  
  
* 405ef2c052 Add QQuickRangeSlider::live  
Added a live-property that determines whether the range slider provides  
live updates for the first.value and second.value properties while the  
respective handle is dragged.  
  
* d03c8de38f Add QQuickDial::live  
Added a live-property that determines whether the dial provides live  
updates for the value-property while the handle is dragged.  
  
* bd5e078e5b Make hoverEnabled propagate to children  
Control::hoverEnabled has been made to inherit to children, to make it  
possible to disable hover effects for a tree of controls in one place.  
  
* 32810acaa1 Let specifying the fallback style for custom styles  
Added support for specifying the fallback style for custom styles via  
:/qtquickcontrols2.conf, QT_QUICK_CONTROLS_FALLBACK_STYLE or  
QQuickStyle::setFallbackStyle().  
  
* cb80c055e7 Page: provide implicit size  
Page has been made to calculate its implicit size based on the implicit  
size of the header, content, and footer plus paddings, and the implicit  
size of the background item.  
  
* 4ce80b299c Fix Shortcut to respect modal popups  
The QML Shortcut type from QtQuick has been fixed to respect modal  
popups from QtQuick Controls 2.  
  
* b552676670 QQuickComboBox: handle Home and End keys  
Added handling for Home and End keys.  
  
* 6f95a086b4 QQuickComboBox: key search  
Added missing keyboard search functionality.  
  
* f5467114b7 QQuickStyle::availableStyles()  
Added availableStyles() method that returns the list of available  
built-in styles.  
  
* 48731e5c2e Dialog: emit rejected() when closed interactively  
Dialog now emits rejected() when closed interactively.  
  
* c69c1f32b0 Restore AbstractButton::checkable  
The checkable property has been made accessible from QML. Previously it  
was only exposed for Button and MenuItem, but it is now available for  
any AbstractButton to make it possible to create custom QML-based  
checkable buttons.  
  
* 94d98bdb63 Add support for a QT_QUICK_CONTROLS_STYLE_PATH environment  
variable  
Added support for a QT_QUICK_CONTROLS_STYLE_PATH environment variable,  
which can be used to specify lookup paths for Qt Quick Controls 2  
styles. This allows device manufacturers and Linux distributions to  
specify a system-wide style installation folder that may be located  
outside the Qt installation tree.  
  
* eba5b547e7 Add ComboBox::editable  
Added editable property  
  
* d705558a28 SwipeDelegate: Add swipe.enabled property  
Added swipe.enabled property to allow disabling of swiping.  
  
* e33443d9b8 Add SwipeDelegate::swipe.open()  
Added swipe.open(side) method that can be used to programmatically open  
the side item on the specified side, which can be either  
SwipeDelegate.Left or SwipeDelegate.Right.  
  
* b0fd258cbb Add Drawer::interactive  
Added interactive property that specifies whether the drawer reacts to  
swipes. This can be used to make drawer a non-closable persistent side-  
bar.  
  
* da0570d1dd Dial: add missing wheel handling  
Added support for wheel handling when wheelEnabled is set to true.  
  
* 0b189ba2ea SpinBox: add inputMethodHints and inputMethodComposing  
Added inputMethodHints and inputMethodComposing properties for  
controlling the input method when using editable spin boxes.  
  
* 3f2cb85ac1 Add Slider::moved() signal  
Added a moved() signal that is emitted whenever the slider is  
interactively moved by the user by using either touch, mouse, wheel, or  
keys.  
  
* 948932c9c6 Add Dial::moved() signal  
Added a moved() signal that is emitted whenever the dial is  
interactively moved by the user by using either touch, mouse, or keys.  
  
* 0a37852dd8 Add AbstractButton::toggled() signal  
Added a toggled() signal that is emitted whenever a checkable button is  
interactively toggled by the user by using either touch, mouse, or keys.  
  
* 2a2a58a061 Add QQuickSpinBox::valueModified()  
Added a valueModified() signal that is emitted whenever the value of a  
spin box has been interactively modified by the user by using either  
touch, mouse, wheel, or keys.  
  
* 66cca16867 Doc: SwipeDelegate: document grouped signals with  
\qmlsignal  
Added swipe.opened() and swipe.closed() signals, which are emitted when  
the delegate has been opened or closed by swipe, and the respective  
transition has finished.  
  
* 5be4488fb1 SwipeDelegate: rename swipe.rebound to swipe.transition  
Added a swipe.transition property that holds the transition that is  
applied when a swipe is released, or swipe.open() or swipe.close() is  
called.  
  
* f15468cf9e Add DelayButton  
Added DelayButton.  
  
* 24acfcafdf QQuickTabBar: fix implicit size calculation  
Added contentWidth and contentHeight properties that are automatically  
calculated based on the total size of the tab items, but can be manually  
overridden if desired. This fixes an issue that TabBar was not able to  
reliably calculate an implicit size, and could in certain scenarios  
enter an infinite loop due to a circular dependency between the items'  
sizes and the tabbar's size.  
  
* 0450296455 Add ScrollBar::snapMode  
Added snapMode property incremental or discrete scrolling.  
  
* 0a86cab635 Editors: fix placeholder text alignment  
Fixed the horizontal alignment of the placeholder text in right-to-left  
UIs.  
  
* 4a97498f4c Add SwipeView::orientation  
Added orientation property.  
  
* def88e0185 Add attached StackView.visible property  
Added attached StackView.visible property that can be used to control  
whether items below the top- most item are kept visible.  
  
* fdd4131711 Add ScrollBar::interactive  
Added an interactive-property. A non-interactive ScrollBar is visually  
and behaviorally similar to ScrollIndicator. This property is useful for  
switching between typical mouse- and touch-orientated UIs with  
interactive and non- interactive scroll bars, respectively.  
  
* 6c0ee76c64 Add ScrollBar::policy  
Added a policy-property, which holds whether the scroll bar is shown  
always/never/as needed (default).  
  
* a9aa500a68 Add ScrollView  
Added ScrollView.  
  
* b026ebf67a Default QQuickSlider::live to true  
On a popular demand, Slider has been changed to report live value  
updates. This can be disabled by setting Slider::live to false.  
  
* 4aadcdae61 Default QQuickDial::live to true  
On a popular demand, Dial has been changed to report live value  
updates. This can be disabled by setting Dial::live to false.  
  
* fc54107f0b Default QQuickRangeSlider::live to true  
On a popular demand, RangeSlider has been changed to report live value  
updates. This can be disabled by setting RangeSlider::live to false.  
  
* 9351df782b Make TextArea work out of the box inside ScrollView  
TextArea has been made to work inside ScrollView, providing necessary  
scroll bars out of the box.  
  
* 94e5393455 ApplicationWindow: fix typo  
The data-property has been renamed to contentData, as it was  
documented. Notice that a data-property still exists in QML Window, but  
is no longer overshadowed in ApplicationWindow.  
  
* b0d2e6d133 AbstractButton: add support for icons  
Added support for icons. The following properties are now available for  
derived types to use: icon.name, icon.source, icon.width, icon.height,  
icon.color.  
  
* b44048ae27 AbstractButton: add display property  
Added display property to allow control over how icons and text are  
displayed within buttons, without having to implement custom delegates.  
  
* 72e12f8e5e Slider: add horizontal and vertical properties for  
convenience  
Added horizontal and vertical properties to make it more convenient to  
create orientation-dependent bindings in styles.  
  
* befa702ce7 RangeSlider: add horizontal and vertical properties for  
convenience  
Added horizontal and vertical properties to make it more convenient to  
create orientation-dependent bindings in styles.  
  
* 113d6f0670 ScrollBar: add horizontal and vertical properties for  
convenience  
Added horizontal and vertical properties to make it more convenient to  
create orientation-dependent bindings in styles.  
  
* 4ff021d3cb ScrollIndicator: add horizontal and vertical properties for  
convenience  
Added horizontal and vertical properties to make it more convenient to  
create orientation-dependent bindings in styles.  
  
* 2e0cded947 SwipeView: add horizontal and vertical properties for  
convenience  
Added horizontal and vertical properties to make it more convenient to  
create orientation-dependent bindings in styles.  
  
* 1cf6abc8ba Slider: react immediately when using a mouse  
Sliders and Dials now react immediately when using a mouse. Now the  
initial drag threshold applies only on touch, to avoid conflicting with  
flickables.  
  
* f0eed56490 ScrollBar: react immediately when using a mouse  
ScrollBar now reacts immediately when using a mouse.  
  
* 27850633dc Add Action  
Introduced Action, an abstract user interface action that can have  
shortcuts and be assigned to buttons.  
  
* 06672a7a45 Add AbstractButton::action  
Added AbstractButton::action property.  
  
* 03607d6d3c Add ActionGroup  
Introduced ActionGroup, a non-visual group of actions that is mutually  
exclusive by default.  
  
* 5479c13959 Add SpinBox::wrap  
Added wrap-property to allow wrapping circular spinboxes.  
  
* 8b9f4364ba Material: use Android button layout for dialogs  
DialogButtonBox with Material theme now uses Android button layout.  
  
* 7fe5e4c685 Add ButtonGroup::exclusive  
Added exclusive property to allow creating non-exclusive button groups.  
  
* 6bd301a56a QQuickTabBar: introduce index/tabBar/position attached  
properties  
Added index/tabBar/position attached properties.  
  
* 26bfe7cb1a Incorporate QQuickDialog::result from QQuickPlatformDialog  
Added "result" property that holds whether the dialog was previously  
accepted or rejected.  
  
* 13452a48c8 QQuickDialogButtonBox: add missing signals  
Added missing applied(), reset(), and discarded() signals.  
  
* fd4d347b0c Add missing QQuickDialog::standardButton() invokable method  
Added a standardButton() method for accessing the standard buttons in  
the dialog's button box.  
  
* 2b20122b22 QQuickDialog: add missing standard button signals  
Added missing applied(), discarded(), helpRequested(), and reset()  
signals that are emitted when the respective standard buttons are  
clicked.  
  
* ea043d5d83 QQuickStyleSelector: fix built-in file selectors  
Fixed the style selection mechanism so that now it is possible to  
organize platform and locale-specific files into sub-directories, such  
as "+linux", "+macos", and "+windows".  
  
* 83a91bc073 StackView::clear() allow specifying a transition  
Allowed specifying a transition when clearing the stack view.  
  
* f57f2d9e45 Say hello to the Fusion style  
Introduced a Fusion style that offers a platform agnostic desktop-  
oriented look'n'feel.  
  
* f2264e2684 Add support for configurable fonts  
Added support for specifying the default font for different styles in  
qtquickcontrols2.conf.  
  
* 1b98cac7c0 Add QQuickMenu::popup()  
Added a popup() method that opens a menu at the mouse cursor on desktop  
platforms that have a mouse cursor available, and otherwise centers the  
menu over its parent item.  
  
* ecef73ddb0 QQuickMenu: add support for declaring Actions  
Added support for declaring Actions. The new "delegate" property is  
used to define a Component that is used to create menu items that  
present the actions.  
  
* 1981ed233f Add QQuickMenuItem::menu  
Added a "menu" property that provides access to the menu that contains  
the menu item.  
  
* 4339a686c1 Add Popup::opened  
Added an "opened" boolean property that holds whether a popup is fully  
open. That is, the popup is visible and neither the enter nor exit  
transitions are running.  
  
* 00594b6e05 QQuickContainer: removeItem(Item) and takeItem(int)  
Deprecated removeItem(int) in favor of removeItem(Item) and  
takeItem(int) with clearer semantics. The former destroys the item,  
whereas the latter transfers ownership to the caller.  
  
* 841e4355d3 QQuickMenu: removeItem(Item) and takeItem(int)  
Deprecated removeItem(int) in favor of removeItem(Item) and  
takeItem(int) with clearer semantics. The former destroys the item,  
whereas the latter transfers ownership to the caller.  
  
* 0d59bff892 QQuickMenu: update the highlighted item on mouse hover  
Menu has been fixed to highlight its items while key navigating and  
mouse hovering to ensure seamless item highlight between mouse hover and  
key navigation. In order to provide appropriate highlighting that works  
for key navigation and mouse hover, styles should bind their visual  
highlight to MenuItem::highlighted instead of Control::activeFocus or  
Control::hovered.  
  
* 038d565194 Let users disable the multi-touch support  
Added a configure feature for disabling multi- touch support (configure  
-no-feature-quicktemplates2-multitouch).  
  
* af96b35bf4 QQuickMenu: fix key navigation  
Fixed key navigation to skip separators.  
  
* 92fcd0a3fb Add support for cascading sub-menus  
Added support for cascading sub-menus.  
  
* 474ded7679 Add QQuickMenu::add/insert/remove/takeMenu()  
Added addMenu(), insertMenu(), removeMenu(), and takeMenu() methods for  
adding and removing sub-menus programmatically.  
  
* 0ef18b4cb2 Add QQuickMenu::add/insert/remove/takeAction()  
Added addAction(), insertAction(), removeAction(), and takeAction()  
methods for adding and removing actions programmatically.  
  
* 1ffede10a0 Add Menu::currentIndex  
Added currentIndex property for styling purposes.  
  
* 697658ab9a Add Popup::enabled  
Added "enabled" property.  
  
* 5dfa85e68c Make ApplicationWindow::activeFocusControl work with plain  
Window  
The attached activeFocusControl property has been made functional with  
a plain QML Window to make the functionality available when using  
QQuickWindow/View/Widget instead of ApplicationWindow.  
  
* d0fdebbc37 Add Overlay attached properties and signals  
Deprecated the overlay grouped property in favor of the newly  
introduced Overlay attached properties.  
  
* 014466f46a QQuickMenu: add actionAt() and menuAt() accessors  
Added actionAt() and menuAt() accessors.  
  
* 1642a45fed Add QQuickPopup::mirrored  
Added a read-only "mirrored" property that is true when the popup's  
locale is right-to-left.  
  
* b9637d71b3 Add QQuickMenu::dismiss()  
Added a dismiss() method. Unlike close() that only closes a menu and  
its sub-menus, dismiss() closes the whole hierarchy of menus, including  
the parent menus.  
  
* 141fdff2c5 Add QQuickMenu::count  
Added "count" property.  
  
* 66faa149db Introduce MenuBar  
Introduced a MenuBar control.  
  
* 846a908b73 Add Imagine style  
Added the Imagine style, which is based on image assets that can be  
provided using a predefined naming convention.  
  
* 2de38813d7 QQuickButton: promote autoRepeat back to  
QQuickAbstractButton  
The autoRepeat property was promoted from Button to AbstractButton.  
  
* 90659c9bed Add QQuickAbstractButton::autoRepeatDelay and  
autoRepeatInterval  
Added autoRepeatDelay and autoRepeatInterval properties.  
  
* 339ddd4fc7 QQuickCheckBox: don't force tristate when partially checked  
CheckBox no longer forces tristate to true when setting checkState to  
Qt.PartiallyChecked. This allows a checkbox to present a partially  
checked state without being interactively a tri-state checkbox.  
  
* fbcdccc4e2 QQuickCheckBox: don't consider partially checked as checked  
CheckBox no longer considers the partially checked state as a checked  
state. This fixes check state cycling for a non-tri-state checkbox so  
that it goes from partially checked to fully checked state.  
  
* 960798f911 Add ButtonGroup::checkState  
Added checkState property that indicates the combined check state of  
the entire group.  
  
* 6115585477 QQuickAbstractButton: expose the press point  
Added pressX and pressY properties.  
  
* 043e3d24f9 Expose QQuickCheckBox::nextCheckState() to QML  
Made it possible to implement nextCheckState() in QML.  
  
* 9e1b044afa ScrollBar: allow configuring the minimum size  
Added minimumSize, visualSize, and visualPosition properties.  
  
* f246314b21 ScrollIndicator: allow configuring the minimum size  
Added minimumSize, visualSize, and visualPosition properties.  
  
* 03155ec2e2 Expose QQuickCheckDelegate::nextCheckState() to QML  
Made it possible to implement nextCheckState() in QML.  
  
* 8e4b91030f Tumbler: ensure that currentIndex animations aren't too  
slow  
Made currentIndex animations take a constant amount of time (1 second)  
regardless of how many items are in the model. This prevents Tumblers  
with large amounts of items from scrolling too slowly when changing the  
currentIndex.  
  
* f2696acaf7 Document license and attribute third party code  
Document constants from AngularJS in  
src/imports/controls/material/ElevationEffect.qml  
  
* 7eb5f8a54b QQuickControl: respect click focus policy for focus scopes  
Fixed focus scope controls, such as Frame, GroupBox, Page, and Pane, to  
respect click focus policy by clearing a potential sub-focus child. This  
makes it possible to close the virtual keyboard by clicking the  
background of a Pane that has Qt.ClickFocus set as its focusPolicy, for  
example.  
  
* 63899f3185 QQuickToolTip: add non-attached show() and hide() methods  
Added non-attached show() and hide() methods to make it more flexible  
to meet certain requirements.  
  
* cf71905368 QQuickControl: respect wheel focus policy for focus scopes  
Fixed focus scope controls to respect wheel focus policy.  
  
* 4ff95c1ffa QQuickCheckDelegate: don't force tristate when partially  
checked  
CheckDelegate no longer forces tristate to true when setting checkState  
to Qt.PartiallyChecked. This allows a delegate to present a partially  
checked state without being interactively a tri-state check delegate.  
  
* e318a1690e QQuickCheckDelegate: don't consider partially checked as  
checked  
CheckDelegate no longer considers the partially checked state as a  
checked state. This fixes check state cycling for a non-tri-state check  
delegate so that it goes from partially checked to fully checked state.  
  
* 0b8160a26b Add Control::horizontal|verticalPadding  
Added horizontalPadding and verticalPadding properties as a convenient  
way to set both left and right, or top and bottom paddings in one go.  
  
* 71d5afa10c Add Popup::horizontal|verticalPadding  
Added horizontalPadding and verticalPadding properties as a convenient  
way to set both left and right, or top and bottom paddings in one go.  
  
* 77a693cb41 QQuickTextField: add placeholderTextColor property  
Added placeholderTextColor property for user convenience to customize  
the placeholderText color to fit the backgrounds.  
  
* f6eb6a3661 Tumbler: add positionViewAtIndex() function  
Added positionViewAtIndex() function that calls the respective  
PathView/ListView function, depending on the value of wrap. This allows  
changing currentIndex without animations.  
  
* 5313a2b3fd Add DialogButtonBox::buttonLayout  
Added buttonLayout property that can be used to arrange the buttons.  
  
* 55fa922b4f Add Dense Material style variant for desktop  
Added Dense variant of the Material style for use on desktop platforms.  
Some controls are slightly smaller in height and use smaller font sizes.  
The variant can be enabled by setting QT_QUICK_CONTROLS_MATERIAL_VARIANT  
to Dense or setting Variant=Dense in the qtquickcontrols.conf file.  
  
* 6b28a01d3f QQuickTextArea: add placeholderTextColor property  
Added placeholderTextColor property for user convenience to customize  
the placeholderText color to fit the backgrounds.  
  
* b6dbfe623a QQuickSlider: add touchDragThreshold property  
Added touchDragThreshold property for configuring the threshold to  
initiate the touch 'drag' of the handle of the slider. The mouse 'drag'  
won't be affected by the property.  
  
* 3650590177 QQuickRangeSlider: add touchDragThreshold property  
Added touchDragThreshold property for configuring the threshold to  
initiate the touch 'drag' of the handle of the slider. The mouse 'drag'  
won't be affected by the property.  
  
* 7dbe1348cc QQuickStyle: add API for managing style paths  
Added stylePathList() and addStylePath() methods for managing the list  
of directories where Qt Quick Controls 2 searches for available styles.  
  
* 1abc7fcbab Add anchors property to Popup to allow centering in  
parent/window  
Added anchors.centerIn to Popup to allow a covenient way of centering a  
popup.  
  
* 449ebc4fbc QQuickControl: update baseline offset automatically  
Unless explicitly specified, baselineOffset is now automatically  
updated based on the top padding of the control and the baselineOffset  
of the contentItem. Styles no longer need to specify the baselineOffset  
in QML.  
  
* 583b7b0324 RangeSlider: add first.moved() and second.moved() signals  
Added a moved() signal to each handle (similar to the Slider's moved()  
signal) to react to the values being interactively changed by the user.  
  
* 98a65a9c74 RangeSlider: add valueAt() function  
Added a valueAt() function to allow accessing each handle's value when  
the live property is set to false.  
  
* c2fd8f7d00 DialogButtonBox: add contentWidth and contentHeight  
Added contentWidth and contentHeight properties.  
  
* cea175fca9 SwipeView: add contentWidth and contentHeight  
Added contentWidth and contentHeight properties.  
  
* 5bd9d44bc7 Control: add implicitBackgroundWidth|Height properties  
Added implicitBackgroundWidth and implicitBackgroundHeight properties  
that can be used to simplify complex implicit size bindings.  
  
* ec6cc9921f Control: add implicitContentWidth|Height properties  
Added implicitContentWidth and implicitContentHeight properties that  
can be used to simplify complex implicit size bindings.  
  
* 704625a034 AbstractButton: add implicitIndicatorWidth|Height  
Added implicitIndicatorWidth and implicitIndicatorHeight properties.  
  
* d2496a68bb Popup: add implicitBackground|ContentWidth|Height  
properties  
Added implicitBackgroundWidth, implicitBackgroundHeight,  
implicitContentWidth, and implicitContentHeight properties.  
  
* 616e86dcb2 ComboBox: add implicitIndicatorWidth|Height  
Added implicitIndicatorWidth and implicitIndicatorHeight properties.  
  
* c8e4c78ec7 Slider: add implicitHandleWidth|Height  
Added implicitHandleWidth and implicitHandleHeight properties.  
  
* 00664e8b59 RangeSlider: add first|second.implicitHandleWidth|Height  
Added first.implicitHandleWidth, first.implicitHandleHeight,  
second.implicitHandleWidth, and second.implicitHandleHeight properties.  
  
* 1a7be21541 SpinBox: add up|down.implicitIndicatorWidth|Height  
Added up.implicitIndicatorWidth, up.implicitIndicatorHeight,  
down.implicitIndicatorWidth, and down.implicitIndicatorHeight  
properties.  
  
* c2768f0f2a Page: add implicit header and footer size properties  
Added implicitHeaderWidth, implicitHeaderHeight, implicitFooterWidth,  
and implicitFooterHeight properties.  
  
* 37ef78bef2 Dialog: add implicit header and footer size properties  
Added implicitHeaderWidth, implicitHeaderHeight, implicitFooterWidth,  
and implicitFooterHeight properties.  
  
* 06071fd14d GroupBox: add implicitLabelWidth|Height  
Added implicitLabelWidth and implicitLabelHeight properties.  
  
* b16f0030f3 Platform: make icon a grouped property  
Deprecated iconName and iconSource properties in favor of icon.name and  
icon.source grouped properties.  
  
* a27c3913c9 Platform: add icon.mask  
Added icon.mask grouped property.  
  
* 5adce042aa Control: add support for background insets  
Added topInset, bottomInset, leftInset, and rightInset properties to  
control the geometry of the background similarly to how paddings control  
the geometry of the contentItem.  
  
* 31998a21d1 Popup: add support for background insets  
Added topInset, bottomInset, leftInset, and rightInset properties to  
control the geometry of the background similarly to how paddings control  
the geometry of the contentItem.  
  
* fac7e9e87c Add missing implicitBackground{Width|Height} to non-  
QQuickControls  
Added implicitBackgroundWidth and implicitBackgroundHeight properties  
that can be used to simplify complex implicit size bindings.  
  
* 89495f409f Label: add support for background insets  
Added topInset, bottomInset, leftInset, and rightInset properties to  
control the geometry of the background similarly to how paddings control  
the geometry of the contentItem.  
  
* 6858d4e987 TextField: add support for background insets  
Added topInset, bottomInset, leftInset, and rightInset properties to  
control the geometry of the background similarly to how paddings control  
the geometry of the contentItem.  
  
* 5ef9d74f83 TextArea: add support for background insets  
Added topInset, bottomInset, leftInset, and rightInset properties to  
control the geometry of the background similarly to how paddings control  
the geometry of the contentItem.  
  
* 9e1a353a86 Dial: add inputMode property  
Added the inputMode property. This property controls how the dial is  
interacted with. The circular input mode (default, old behavior)  
operates on an absolute input system, whereas the horizontal and  
vertical input modes use a relative input system.  
  
* 3c7bfc1567 Tie minor version of all imports to Qt's minor version  
From Qt 5.12 onwards, all import versions in Qt Quick Controls 2 follow  
the same minor version as Qt's minor version number. For example, the  
import version for Qt 5.12 is: "import QtQuick.Controls 2.12".  
  
* ed87e837ff Add SplitView  
Introduced SplitView, a control that lays out items horizontally or  
vertically with a draggable splitter between each item.  
  
* 033564edf5 QQuickIcon: Add support to cache a pixmap  
Added cache property to icon.  
  
* f462312365 Add valueRole API to ComboBox  
Added valueRole, currentValue and indexOfValue(). These allow  
convenient management of data for a role associated with the text role.  
  
* 83813e4340 QQuickComboBox: emit countChanged signal when model is  
updated  
countChanged signal now will be emitted when a new model is set to the  
ComboBox  
  
* da06da5700 QQuickTextArea: prevent changing size of background  
recursively  
defer adding change listener and prevent changing size of background  
recursively in construction  
  
* 6815f353e5 TextArea: prevent changing size of background recursively  
prevent changing size of background recursively in construction  
  
* 2da83b321f Universal: disable wrapping for TabBar  
Disabled wrapping. The Universal style TabBar now behaves like TabBar  
from other styles.  
  
* 66de71b26a QQuickMenuBar: let MenuBarItem lose highlight when Menu is  
dismissed  
Fixed issue with dynamically menu bar items not losing their highlight  
when their menu was dismissed.  
  
* 21e3c3eff2 QQuickPopup: try to grab shortcut when component completed  
Fixed the issue that Popup doesn't respond to CloseOnEscape if the  
initial value of visible is true  
  
* 80f1186338 Don't delete items we didn't create  
Old delegate items (background, contentItem, etc.) are no longer  
destroyed, as they are technically owned by user code. Instead, they are  
hidden, unparented from the control (QQuickItem parent, not QObject),  
and Accessible.ignored is set to true. This prevents them from being  
unintentionally visible and interfering with the accessibility tree when  
a new delegate item is set.  
  
* 0425562e14 ComboBox: add selectTextByMouse property  
Added selectTextByMouse property.  
  
* 0b607bfe14 Add HorizontalHeaderView and VerticalHeaderView  
Add HorizontalHeaderView and VerticalHeaderView. They are controls  
associated with TableView. Support flicking synchronization Support  
default, fusion, imagine, material and universal delegate styles.  
  
* 0d5a43fa84 Material: Change slider's color to grey when not enabled  
Add visual distinction between an enabled and not enabled slider.  
  
* 31f5c21ddb Remove old QQuickPalette implementation  
the palette API is a part of QQuickItem now.  
  
* 67792feba0 Fix Qt 6 to-do comments in QML files  
implicitWidth and implicitHeight must now be provided for Tumbler's  
contentItem, as with all other controls.  
  
* e16408a193 ComboBox: make pressed read-only  
The pressed property is now read-only. The down property can be used  
instead.  
  
* 7c873b0a58 Container: remove deprecated removeItem(var) overload  
The deprecated removeItem(var) function was removed. removeItem(Item)  
or takeItem(int) can be used instead.  
  
* e0b356af9e Menu: remove deprecated removeItem(var) overload  
The deprecated removeItem(var) function was removed. removeItem(Item)  
or takeItem(int) can be used instead.  
  
* 8fdcde54e6 Fix Qt.labs.platform/MenuItem 1.1: expose icon  
Expose MenuItem.icon.* property when imported as revision 1, which was  
erroneously not exposed at all.  
  
* de867d2370 Platform: remove deprecated iconName, iconSource API  
The deprecated iconName and iconSource properties were removed. Use the  
icon property instead.  
  
* ed1ec14b6a QQuickStackView: deprecate Transition enum value  
The StackView.Transition enum value was deprecated. The operation  
argument can be omitted in order to use the default transition for any  
given operation.  
  
* 31fbd97b0e ApplicationWindow: remove deprecated overlay API  
The deprecated overlay properties and attached API were removed. Use  
the Overlay attached type instead.  
  
* 49ffc6e6af ComboBox: add implicitContentWidthPolicy  
Added implicitContentWidthPolicy, which controls how the  
implicitContentWidth of the ComboBox is calculated. This can be used to  
automatically ensure that text is not elided.  
  
* 501bc44bb0 Use qmlRegisterModuleImport() to register styles  
Custom styles must now have a qmldir that lists the files that the  
style implements. For example, for a style that only implements Button:  
--- module MyStyle Button 1.0 Button.qml --- In addition, there is now  
only one valid, case-sensitive form for style names: "Material",  
"MyStyle", etc. These changes are done to help enable the compilation of  
QML code to C++, as well as improve tooling capabilities.  
  
* 0e516bc963 ToolTip: only begin timeout when opened  
ToolTip's timeout now begins only after opened() has been emitted. This  
bug fix results in tooltips with enter transitions being visible for the  
entire duration of the timeout property. This means that they are  
visible slightly longer than they were before, so it may be worthwhile  
to visually check tooltips in your application and adjust timeouts if  
necessary.  
  
* 0d3b8f832a Dialog: emit accepted()/rejected() before closed()  
Dialog's accepted() and rejected() signals are now emitted before  
closed() when calling done(), accept() and reject().  
  
* bb33370005 Fix examples' usages of styles  
Due to the recent type registration changes, importing a style  
explicitly (e.g. "import QtQuick.Controls.Material") now registers that  
style's QML types in addition to making its API (attached, singleton,  
etc.) available. For this reason, it is now advised to have style-  
specific code in a separate QML file and use file selectors if your  
application supports more than one style. If your style only supports  
one style, importing that style explicitly will work as expected. For  
example, if you use Material.foreground in your QML code and your  
application supports more than one style, you should refactor the code  
that uses the binding into its own file; e.g. +Material/MyComponent.qml.  
  
* 9219e86aa5 Rename "Default" style to "Basic"  
The Default style was renamed to Basic to account for the introduction  
of the platform styles (macOS, Windows), which will be used by default  
(where possible) when no style is specified.  
  
* a0f0b4f65e Support compile-time style selection  
It's now possible to select a style at compile-time by importing that  
style explicitly instead of QtQuick.Controls. This avoids the need to do  
run-time style selection and hence deploy the QtQuick.Controls plugin  
with the application.  
  
* 8b53448704 Default to the most appropriate built-in style if none is  
specified  
An appropriate built-in style is now used as the default style if one  
is available for the target platform. For example, when running a Qt  
Quick Controls application on macOS, the macOS style will be used. On  
Android, the Material style will be used. When running on e.g. an  
embedded device, where no native style is available, use the Basic  
(formerly "Default") style.  
  
* 0a48787cef ScrollView: always clip implicitly created Flickable  
ScrollView now clips its contents by default.  
  
* 4a718113ab Allow style to be set to "Default" for compatibility  
Setting the style to "Default" now behaves the same way as not  
specifying a style; a relevant style will be chosen based on the  
platform. To use the style previously known as "Default", use "Basic".  
  
* df33c79fb6 Reset the opacity and scale properties after the exit  
transition  
After the exit transition is finished, then the opacity and scale  
properties will be reset to their values before the enter transition is  
started.  
  
* ab71cdafca QML: Warn about variables being used before their  
declaration  
QML warns about JavaScript variables being used before their  
declaration now. This is almost always a mistake. It is particularly  
dangerous in the presence of injected signal parameters because  
qmlcachegen cannot identify a name collision between an injected signal  
parameter and a variable being used before its declaration. It therefore  
miscompiles such code. You can turn off the deprecation warning using  
the "qt.qml.compiler" logging category.  
  
* 953ea29328 Deprecate qmlplugindump  
qmlplugindump is deprecated. Instead of using qmlplugindump to generate  
qmltypes files by loading and analyzing the pre-built plugins, you  
should declare your QML types using QML_ELEMENT and friends. Then you  
can automatically generate the qmltypes files at compile time using  
qmltyperegistrar.  
  
* df70d4f76f QML: Warn about usage of injected signal parameters  
The automatic injection of signal parameters into signal handlers is  
deprecated. This is because we cannot determine the names of the signal  
parameters at compile time. Furthermore, also for human readers it is  
difficult to discern between arguments, context properties, properties  
of the current object, and properties of the root object of the  
component. Requiring the signal parameters to be explicitly named  
resolves some of this confusion. You can turn the deprecation warning  
off using the "qt.qml.compiler" and "qt.qml.context" logging categories.  
  
* 8e904d9c8b QML engine: Handle const QObject pointer correctly  
If a QObject pointer is passed to the QML engine and subsequently  
frozen with Object.freeze, modifying its QObject properties now fails  
and throws a TypeError. The TypeError is thrown even in non-strict mode.  
  
* ce52c245aa Add a "prefer" directive to qmldir  
You can now specify that QML files in a QML module should be loaded  
from a different place than the directory where the qmldir file is  
found. To do this, add a "prefer" directive to the qmldir file. The most  
useful application of this is adding the QML files as resources to a  
plugin, and using qmlcachegen to pre-compile them. You can then add  
their path inside the resource file system as "prefer" path in order to  
make the engine load the pre-compiled files. The plain files should  
still be installed next to the qmldir file so that they remain visible  
to tooling.  
  
* bbba1e5614 qmllint: Implement deprecation warnings  
Add support for deprecation annotations.  
  
* 602982993c qmllint: check default properties  
Add support for default properties  
  
* ea8f8e0900 Introduce XmlListModel to QtDeclarative  
Introduce an XmlListModel QML model to create read-only models from XML  
data. This is a simplified version of a model from QtXmlPatterns, which  
would no longer be a part of Qt 6. This model supports only simple  
slash-separated paths and, optionally, one attribute for each element.  
  
* a9c93e2716 qmlscene: Show deprecation warning  
qmlscene is deprecated, please use qml instead  
  
* eb2386a042 Optimize ExecutionEngine::metaTypeToJS()  
If you create a QJSValue from a nested QVariant (that is, a QVariant  
containing another QVariant), then, when retrieving its contents again,  
the outer variant is not unwrapped anymore. Rather, you get exactly the  
value you've passed in.  
  
* d61ececdb8 Expose formattedDataSize() in QML Locale type  
Added formattedDataSize() for formatting quantities of bytes as kB, MB,  
GB etc.  
  
* 93984dfc86 qmllint: Only exclude default QML import dirs when  
explicitly requested  
Using -I no longer excludes default QML import directories. Use --bare  
to get the old behavior.  
  
* 5f7ecce233 Implement optional chaining  
Added support for optional chaining (https://github.com/tc39/proposal-  
optional-chaining)  
  
* b15d300fd1 QQuickTableView: add isColumnLoaded() and isRowLoaded()  
Added API to query if a row or column is loaded and available for  
iteration: isRowLoaded(row) and isColumnLoaded(column).  
  
* c7f9d1525e QQuickTableView: add API to get column widths and row  
heights  
Added API to query row heights and column widths: columnWidth(col),  
rowHeight(row), implicitColumnWidth(col), implicitRowHeight(row).  
  
* 9cd1e7902c Fix QQmlContext::nameForObject()  
QQmlContext::nameForObject() now finds properties of context objects,  
but it does not search unrelated other ("linked") contexts anymore.  
  
* 93bd34b78f Add QtCore module  
Added QtCore QML module. Currently this only contains the StandardPaths  
singleton, but in the future could expose lots of useful types from Qt  
Core to QML.  
  
* 3464655f5e Add QJSEngine::registerModule  
Adds the ability to register QJSValues in C++ as modules for importing  
in MJS files.  
  
* 0fef848468 qv4engine: Fix enums getting turned into objects when  
passed in lists  
A QList containing enums will now result in an array of numbers instead  
of an array of objects.  
  
* 55fafd6915 Fix regression where qtquickcompiler cannot find rcc  
Fixed regression in Qt 6.1.0 which broke 'QT += qtquickcompiler' on  
Linux, macOS.  
  
* 1d44ddf576 Add support for QTextCharFormat::underlineColor in  
highlighers and CSS  
When a QSyntaxHighlighter calls QTextFormat::setUnderlineColor(), or  
CSS style contains text-decoration-color, Text and TextEdit will now use  
that color for underline, overline and strikeout rendering.  
  
* c442542627 Move tools to libexec  
qmlimportscanner, qmltyperegistrar, qmljsrootgen, qmlcachegen tools got  
moved from QTDIR/bin into QTDIR/libexec directory.  
  
* a063cd0be5 ToolTip: use contentWidth of Text contentItem to account  
for newlines  
The implicit width of ToolTips now accounts for newlines in the text.  
If you want to use the old behavior, set ToolTip's contentWidth to  
implicitContentWidth.  
  
* 0a673d257a Make QDate handling consistent in its use of UTC  
Where a QDate is represented in QML's JavaScript as a Date, it is now  
more consistently associated with the start of the UTC day it describes.  
Previously cases where it was represented as the start of local time's  
day could lead to a Date turning into a QDate for the preceding day.  
Inconsistencies in the specified behavior of Date preclude eliminating  
such problems entirely, but they should now be limited to cases where  
(perversely for a date property or parameter) the date is specified with  
a local time late enough to make it coincide with the start of the next  
UTC day (in which case that next day's QDate will be its C++  
representation).  
  
* 6b687ad7ec Fix layout is always RTL when locale is RTL  
Control's locale property no longer affects layout direction. Use  
LayoutMirroring instead.  
  
* 4f73c07b52 Revert "AbstractButton: set automatically as checkable when  
being checked"  
Setting the AbstractButton's 'checked' property to 'true' does not  
automatically set its 'checkable' to true anymore.  
  
* 0472a7a432 Evaluate type assertions in QML  
You can use TypeScript-like type assertions using "as" now. In contrast  
to TypeScript, QML's type assertions are enforced at runtime. If the  
type doesn't match, null is returned for object types. Also, type  
assertions can only cast to object types. There is no way to create a  
value type or primitive type reference. As value types and primitives  
cannot be polymorphic, this doesn't matter, though. There are other ways  
of converting those.  
  
* 73d51eed2f qmllint: Add support for loading options from settings  
Adds the ability to set linting options via a settings file rather than  
using command line parameters. Use --write-defaults to generate a  
template with default values for editing. Use --ignore-settings to  
disable this feature  
  
* f9421abbdf Add QtQuick.Dialogs  
Added FileDialog. This is a native FileDialog on platforms that support  
it, and a non-native Qt Quick FileDialog on platforms that don't.  
  
* 17babc38b4 Add the possibility of flipping vertically to Image  
Added mirrorVertically to Image to allow vertically mirroring an image.  
This complements the existing mirror property that performs a horizontal  
flip.  
  
* f625afb9f3 Add placeholderText to SystemPalette and ColorGroup  
Added placeholderText to SystemPalette and ColorGroup to keep it in  
sync with QPalette  
  
* d2bb3513b4 qmllint: Add support for outputting warnings as JSON  
Add the ability to output warnings as JSON for use in tooling.  
  
* c6c31740a7 Selection support: support setting a QItemSelectionModel on  
TableView  
TableView now supports selections by using an ItemSelectionModel.  
  
* ba2928c787 Reject overrides of final properties (and potentially  
methods)  
C++ properties declared FINAL now refuse to be overridden by other C++  
properties. This mirrors the treatment of QML properties trying to  
override FINAL properties. As we cannot reject the C++ types the way we  
can reject QML types, the overrides are ignored and a warning is issued.  
It is also impossible to override final properties with functions now.  
This used to be possible in the past.  
  
* 9f389ee75d qmllint: Add ability to ignore individual warnings  
You can now ignore individual warnings by adding "// qmllint disable"  
in the line causing it. You may also specify one or more warning type to  
ignore ("// qmllint disable warningtype1 warningtype2...") which is  
preferable. This can also be done for entire blocks of code by using "//  
qmllint disable" in an empty line and ending it with "// qmllint enable"  
  
* 4017505cbc QQuickItem: Make x/y/width/height bindable  
The x, y, width and height properties of QQuickItem are now bindable.  
This enables modifying their bindings from C++. One could for instance  
swap the width of two items, preserving the bindings: // QML Item {  
Rectangle { id: a; width: parent.width / 2 }   Rectangle { id: b; width:  
parent.width / 3; anchors.right: a.left } } // C++ auto rootCtxt =  
engine.rootContext(); auto a =  
qobject_cast<QQuickItem*>(rootCtxt->objectForName(u"a"_qs)); auto b =  
qobject_cast<QQuickItem*>(rootCtxt->objectForName(u"b"_qs)); auto  
aBinding = a->bindableWidth().takeBinding(); auto bBinding =  
b->bindableWidth().takeBinding();  
a->bindableWidth()->setBinding(bBinding);  
b->bindableWidth()->setBinding(aBinding); Afterwards, if the root item  
gets resized, the width of the rectangles will still be adjusted.  
  
* f5258c3682 Fix FINAL warning  
QML code that imported version 2.4 or earlier will no longer be able to  
access contentWidth and contentHeight in types derived from Container  
(i.e. MenuBar, etc.).  
  
* 1c4ba17015 Refactor and update qml CMake API  
The qml CMake API has changed from 6.1 and is now out of Technical  
Preview status. The most notable change is that .qml files should no  
longer be specified as resources, there is dedicated handling for them  
in the qt6_add_qml_module(). A related change is that the  
qt6_target_qml_files() command has been replaced by  
qt6_target_qml_sources(). More complete integration with qmlcachegen,  
qmllint and qmldir generation is also part of the CMake API.  
  
* 60d11e1f69 Add DragHandler.activeTranslation and persistentTranslation  
DragHandler.activeTranslation now holds the amount of movement since  
the drag gesture began. DragHandler.persistentTranslation holds the  
accumulated sum of movement that has occurred during subsequent drag  
gestures, and can be set to arbitrary values between gestures.  
  
* c52710c10c Add new control: SelectionRectangle  
A SelectionRectangle has been added to Controls. A SelectionRectangle  
can be used to make selections in TableView.  
  
* d30fad2a71 qqmllistmodel: Fix QObjects getting garbage collected  
ListModels now take ownership of the objects added to them, only  
releasing them after the object has been removed again. This may break  
existing solutions which rely on the object not being owned by the  
model.  
  
* c024daf331 QQuickItem change contains function behavior  
Item.contains() now checks for coordinates less than the width and  
height, for consistency with childAt(), and because the item is drawn  
from (0,0) to (width-1, height-1).  
  
* 6d332987ef Change QQuickItem childAt bounds check behavior  
QQuickItem::itemAt() now uses contains() for hit testing, so it is  
affected by containmentMask() if set.  
  
* fb09279c01 Make QQuickItem containmentMask be dependent on position  
Previously, containmentMask's position was ignored. If containmentMask  
parent inherit from QQuickItem, then position will take into account. In  
some cases, this is useful, for example, to make click on button larger  
than the size of the button itself, in all directions, not just to the  
right and bottom.  
  
* d728049372 Fix Flickable wheel velocity calculation  
Flickable no longer tries to detect whether you're using a "clicky"  
wheel or a touchpad, but rather does the velocity calculation more  
correctly with elapsed time (dθ / dt). A single rotation of a "clicky"  
wheel also moves a fixed distance, which is now adjustable via  
QStyleHints::wheelScrollLines(). Animation is restored, but should now  
stay in control on touchpads; and it will once again transition the  
"moving" properties correctly when scrolling ends.  
  
* 3eece79ddb Avoid querying the file system for qmldir files for locked  
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
  
* 1a29e946ee Add button argument to the  
TapHandler.[single|double|]tapped signals  
TapHandler's tapped(), singleTapped() and doubleTapped() signals now  
have two arguments: the QEventPoint instance, and the button being  
tapped. If you need it, you should write an explicit function for the  
signal handler: onTapped: function(point, button) { ... } or  
onDoubleTapped: (point, button)=> ...  
  
### qttools  
* b7fd470a QDoc: Let default be qmldefault  
QDoc's \default command should specify a default value. To document a  
default QML property, use the new \qmlproperty command.  
  
* 7f3bcf85 macdeployqt: Fix bug parsing otool output when deploying  
plugins  
Fix plugin deployment bug caused by otool parsing  
  
* 03abcbab macdeployqt: Fix plugin resolution bugs for non-standard  
installs  
Uses QLibraryInfo to resolve plugins at install locations.  
  
* 1637d91e QDoc: Add \deprecatedsince command  
QDoc now lets you record the version something is deprecated in with  
the new \deprecatedsince command.  
  
* ae369522 qdoc: Remove Node::Obsolete status  
Replaced \obsolete command in favor of \deprecated as it's a more  
accurate description of the intended status.  
  
* c3660873 Doc: Improve \deprecated command  
QDoc now lets you record the version something is deprecated and  
suggest replacements with the \deprecated command.  
  
* d6bc6581 lupdate: Support Python  
lupdate now supports Python.  
  
### qtdoc  
* 2a59fb29 Move Qt Shader Tools, Qt Quick 3D, Qt Quick Timeline to GPL  
section  
Mark Qt Shader Tools, Qt Quick 3D, and Qt Quick Timeline in the module  
overview as available under Commercial/GPLv3 only.  
  
### qtwayland  
* e08b25ef Fix race condition when attaching client to text input  
Fixed a problem where a virtual keyboard would not be updated correctly  
if two clients were started at almost the same time.  
  
* 93058de8 client: Fix frame callback leak when window unexposed  
Fixed a bug where Wayland clients would continuously request frame  
callbacks while unexposed, which potentially caused crashes on some  
compositors.  
  
* b19b0fba client: Gracefully handle shutdown and window hiding  
Fixed a crash that could happen when hiding or closing windows while Qt  
Quick was actively rendering on a different thread.  
  
* 1a4545f9 Ignore viewporter buffer size when buffer is null  
Fixed an issue in the wp_viewporter extension, where it would emit a  
protocol error if the viewport was configured before attaching a buffer  
to the surface.  
  
* 386a4cd5 Implement wp_viewporter support for video buffer formats  
Support for wp_viewporter extended to cover less common buffer formats.  
  
### qt3d  
* 4886caf4b Fix multi-view picking  
Non rendered entities (due to layer filtering) are no longer pickable  
  
* 61058758a Disable RHI Renderer by default  
RHI Backend is not longer built by default  
  
### qtimageformats  
* 8796018 Update bundled libtiff to version 4.2.0  
Bundled libtiff was updated to version 4.2.0  
  
* 59aaed8 Update bundled libwebp to version 1.2.0  
Update bundled libwebp to version 1.2.0  
  
* 2d8573f Update bundled libtiff to version 4.3.0  
Bundled libtiff was updated to version 4.3.0  
  
* 95f02ee Add floating point read and write to TIFF handler  
Read/write support for floating point image formats added.  
  
* 31f752a Update bundled libwebp to version 1.2.1  
Update bundled libwebp to version 1.2.1  
  
### qtvirtualkeyboard  
* 50173b8 Add Stroke and Romaji values to the InputMode enumeration  
Added Stroke and Romaji values to the InputMode enumeration.  
  
* 2e4201f CMake: Fix pinyin and tcime resource bundling  
Added vkb- prefix to no-bundle-pinyin no-bundle-tcime command line  
options (e.g. vkb-no-bundle-pinyin) and restored them as part of  
configuration.  
  
* ff2d652 Change long press delay from 800 ms to 500 ms  
Change long press delay from 800 ms to 500 ms.  
  
* adeb526 Refresh keyboard layouts and style  
Refresh keyboard layouts and style.  
  
* 916bf30 Decrease the z-value of the InputPanel to 10000  
The default z-value of the InputPanel item has been decreased to 10000.  
  
* f59e59b Fix high CPU utilization caused by key repeat timer  
Fixed high CPU utilization caused by key repeat timer.  
  
* a393c7e Disable Windows IME when Qt Virtual Keyboard plugin is loaded  
Disable Windows IME when Qt Virtual Keyboard plugin is loaded  
  
* f273b5b Fix processing of hard Qt::Key_Backspace and Qt::Key_Delete  
Fix processing of hard backspace and delete keys.  
  
### qtscxml  
* 0f733c0 Name and mark the scxml datamodel plugin headers as private  
The QScxmlEcmaScriptDataModel class is no longer part of the public  
API. This relates to moving the ecmascript datamodel's QML dependency  
from build time to runtime.  
  
* 6a2ed39 Rename qscxmlc CMake options  
Rename QSCXMLC_ARGUMENTS and OUTPUT_DIR CMake variables to be better  
aligned with other CMake APIs (OPTIONS and OUTPUT_DIRECTORY  
respectively).  
  
### qtquick3d  
* 06c66e24 Fix to deal with emissive properties  
This patch changes how to handle emissive terms in all materials.  
Following lancelot tests are influenced by this patch.  
custommaterial/customsimpletexture.qml instancing/customsimple.qml  
layers/Light_probe.qml Previously the emissive term is multimpled by the  
diffuse term, but now it is added to the final color.  In  
customsimpletexture, the final color will be close to "white" since the  
emissive value is too big.  
  
* ef768aa9 Fix the occlusionMap to be compatible with GLTF2  
This patch changes how occlusionMap works in QQuick3DMaterial.  
Previously occlusionMap influences on all the diffuse colors and  
emissive colors. Now it will not affect punctual lightings.(For now it  
will affect only IBL.) The result of a lancelot test,  
principled/occlusion.qml, will be changed because it does not have  
IBL.(The occlusionMap will be ignored.) There will be 4 rows in the new  
test. Top 2 rows are without IBL, and others are with IBL in their  
materials.  
  
* 4bb19c6e Auto-invert flipV for QTextureFileReader formats  
Compressed textures (more precisely, any texture loaded from a .ktx,  
.pkm, or .astc file) now get an implicit vertical flip when used in  
combination with a DefaultMaterial or PrincipledMaterial. This is the  
same implicit behavior as one gets when using Qt Quick to render the  
contents of the texture by using the sourceItem property. In addition, a  
new property has been introduced: Texture.autoOrientation. By default  
this is set to true. Setting to false disables the implicit flipping  
behavior. The behavior of the existing flipV property is not affected.  
It will apply after any implicit flipping.  
  
* ac9aaccc Enhance add_lightprobe_images file name handling  
The qt6_add_lightprobe_images CMake function, which is the new name of  
qt6_quick3d_bake_lightprobe_hdri has been changed to match  
qt6_add_resources when it comes to the handling of PREFIX, BASE, and  
FILES. It no longer strips the directories from the entries in the FILES  
list. This means that invocations that previously catered for the  
special behavior by listing the necessary extra directories in PREFIX  
must now be changed to not do that anymore. In addition, support for the  
OUTPUTS keyword has been introduced, in order to have API symmetry with  
qt6_add_shaders.  
  
### qtshadertools  
* f3a446a Change PREFIX and FILES path handling to match add_resources  
The qt6_add_shaders CMake function has been changed to match  
qt6_add_resources when it comes to the handling of PREFIX, BASE, and  
FILES. qt6_add_shaders no longer strips the directories from the entries  
in the FILES list. This means that invocations that previously catered  
for the special behavior by listing the necessary extra directories in  
PREFIX must now be changed to not do that anymore.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-90582 Building qtbase statically with tests fails  
* QTBUG-89155 Assertion violation in text shaping on special string with  
EmojiOneColor font.  
* QTBUG-90033 iOS: unable to click on a QWidget  
* QTBUG-90860 [iOS] The edit menu doesn't hide when typing on the input  
panel  
* QTBUG-84616  Mac Checkbox Accessibility does not returns mixed State  
* QTBUG-63018 [iOS]: When moving the selection handles in a TextEdit the  
cursorRectChanged signal is emitted even if the cursor rect is not  
actually changed  
* QTBUG-89086 tst_QGlyphRun::drawRightToLeft() failed on openSUSE 15.2  
* QTBUG-90683 Some keyboard shortcuts will crash Qt when matching is  
attempted on macOS 10.15 or higher  
* QTBUG-90236 QRawFont::alphaMapForGlyph() shows garbage and eventually  
leads to crash  
* QTBUG-90937 [iOS] edit menu stays open after changing focus  
* QTBUG-90933 Update dependencies on 'dev' in qt/qtdeclarative failed  
* QTBUG-90698 tst_QTextLayout::softHyphens() failed on macos 11 in CI  
* QTBUG-90946 Qt configure option is translated to the incorrect cmake  
variable  
* QTBUG-90801 QMake: if you #include a C file from another C file, the  
original file no make target is created  
* QTBUG-90778 [Reg 5.15 -> 6] CMake: Can't skip PrintSupport.  
* QTBUG-90963 QDoc manual has overlapping captions with images  
* QTBUG-77937 Extra whitespace accessible with scroll-bars at the end of  
QPlainTextEdit widget  
* QTBUG-91033 Multiple extra compilers with same input are broken for VS  
projects  
* QTBUG-90850 MinGW static build: fail to build PostgreSQL driver  
* QTBUG-91042 REG Qt 6.0: QList/QVector::fill does not support shrinking  
list  
* QTBUG-88579 CMake testing expect a fake_prefix folder resembling the  
installation prefix  
* QTBUG-91038 tst_QTextLayout::longText failures  
* QTBUG-75630 QPainter drops e.g. lines using small (< 1e-12) user world  
coords  
* QTBUG-90925 Cannot specify link libraries for target "OpenSSL::Crypto"  
* QTBUG-90914 configure can't find compiler although CC/CXX are given  
* QTBUG-90870 Add Qt::Gui dependency by default to Android tests  
* QTBUG-90971 macOS system locale isn't consistent with itself  
* QTBUG-89735 MultiPointTouchArea delays release on three finger tap  
* QTBUG-91061 [REG 6.0.1->6.1.0] qml/quick examples not compiling on iOS  
(Undefined symbols for architecture arm64)  
* QTBUG-90961 Recent tidy-up broke builds with system double-conversion  
library  
* QTBUG-89889 tst_QDateTime::systemTimeZoneChange fails on 32bit systems  
* QTBUG-91102 failed to detect Wacom Art Pen rotation capability  
* QTBUG-90625 subset of downloads stall and die with connection closed  
on some systems  
* QTBUG-90699 tst_QApplication::focusWidget() and focusMouseClick()  
failed on macos 10.15 in CI  
* QTBUG-87457 Example not compiling due 'AutoUic error'  
* QTBUG-89952 [Reg 5.15 -> 6] Windows, MSVC: DLL-s are bigger with  
CMake, than QMake.  
* QTBUG-90969 Cannot build qtquickcontrols2 examples on Qt6  
* QTBUG-87078 xcb: showMaximized() in full screen only restores the  
window with some WMs  
* QTBUG-85287 Hanging tst_qprocess test on qemu armv7 CMake builds  
* QTBUG-88031 iOS: quickcontrols2/gallery fails to build in release mode  
(Failed to parse qmlimportscanner output)  
* QTBUG-91158 INPUT_ variables having a corresponding feature are  
converted to "ON/OFF"  
* QTBUG-69129 Android: QTimeZone::specificTransition fails  
* QTBUG-86733 [Android] NoSuchMethodException when using QtMultimedia  
* QTBUG-87871 QMdiSubWindow's window icon size is incorrect for system  
scaling 150% or more  
* QTBUG-91194 Android Service - Exception on startup  
* QTBUG-32778 Documentation colors conflicting with system theme make  
text unreadable  
* QTBUG-83632 In top level frameless window Qt.CrossCursor does not  
comes in effect  
* QTBUG-91224 BIC breakage in QStyleOptionHeader  
* QTBUG-83295 QLineEdit::editingFinished() not emitted when pressing the  
clear button and moving focus away  
* QTBUG-91223 qt_memrotate270, qt_memrotate180 , qt_memrotate90,  
segfaults  
* QTBUG-69131 Android: tst_QTimeZone::transitionEachZone fails  
* QTBUG-91155 QNetworkManagerNetworkInformationBackend without DBus  
* QTBUG-90949 UI rendering and interaction dead lock when used as an  
window embedded application  
* QTBUG-91401 Error loading PNG: Unsupported ICC profile class 70727472  
* QTBUG-81316 QGraphicsItem::setZValue not working  
* QTBUG-91430 QCommandLineParser crashes when helpText/showHelp is  
called without a QCoreApplication  
* QTBUG-90396 QFontDialog highlights default value for the font style  
list  
* QTBUG-64443 QWindowsPipeReader/Writer notification stops when dragging  
the window  
* QTBUG-91431 CommpareNotEqual misspelled  
* QTBUG-91500 There is no file 'QWGLContext'  
* QTBUG-91076 syncqt.pl is in bin and libexec  
* QTBUG-91496 Cross Compilation of Android from Windows fails after  
libexec changes  
* QTBUG-91532 tst_QMenu::QTBUG_89082_actionTipsHide() failing on Windows  
* QTBUG-91073 Android:  cursor movement in TextEdit is not tracked, so  
it can go behind the soft-keyboard  
* QTBUG-91620 QFuture documentation incorrectly linked  
* QTBUG-91531 Inconsistent use of Qt_6_PRIVATE_API breaks BC between Qt  
6.0 and Qt 6.1  
* QTBUG-63275 Android QScreen::grabWindow(0) & sample code  
Screenshot::shootScreen() fails on Android  
* QTBUG-42469 QTreeWidget animated crashes when QTreeWidgetItems are set  
hidden to true  
* QTBUG-91402 [REG: 5.15 - 6.x] Wheel events get lost when connecting  
from macOS via ssh  
* QTBUG-91630 Rendering error with OpenGL in Lancelot test case  
involving Item2D  
* QTBUG-88305 [REG v6.0.0-beta3 -> dev] Asking configure for an  
unavailable feature causes obscure crash instead of informative error  
message (version 2)  
* QTBUG-91056 [Android]: When a  large TextEdit is clicked, it  changes  
its size with every click  
* QTBUG-91438 iOS enormous leak ends with "Terminated due to memory  
issue"  
* QTBUG-91539 QThread::quit() is unreliable on Windows  
* QTBUG-84342 QTuioTouchPlugin fails to build with "Unix Makefiles"  
generator on macOS  
* QTBUG-90449 Wrong CMAKE_INSTALL_PREFIX when building a module against  
an installer-provided Qt  
* QTBUG-91141 qdoc/WebXML (Qt 6): Invalid links to "Changes to Qt  
<Module>" are inserted into \brief of classes and other places  
* QTBUG-88286 The -cmake configure option seems redundant now  
* QTBUG-86857 QPushButton style "text-align: bottom" not working in Qt  
5.15.1  
* QTBUG-91704 QMultiHash::count(key) crashes on empty container  
* QTBUG-91455 Qt.ImhFormattedNumbersOnly flag does not show minus sign  
in iOS keyboard  
* QTBUG-90812 androiddeployqt doesn't bundle JARs or include permissions  
set on a plugin  
* QTBUG-91511 Can't build user project with qmake with a Qt6 built with  
-qtlibinfix XX  
* QTBUG-91538 qtshadertools/qtools require cmake wrappers from  
qtimageformats (WebP/Jasper) in static builds  
* QTBUG-91909 QtConcurrenceThreadEngine > ThreadEngineStarter<VOID>?  
* QTBUG-91916 [REG 6.1 -> 6.2] Memory leak in QPainterPath  
* QTBUG-55444 Documentation doesn't explain that login and password  
provided to MySQL plugin (QSqlDatabase::setUserName and  
QSqlDatabase::setPassword) must be in latin1 encoding  
* QTBUG-91866 MSVC warns about C4250 in network/openssl  
* QTBUG-91766 Changing copy of QSqlQuery changes original.  
* QTBUG-91261 Invalid pointer return with QGridLayout::itemAt(-1)  
* QTBUG-91117 Build error in Windows Visual Studio 2019,  c++20  
referring to std::popcount  
* QTBUG-91915 Gui applications that are built as part of a static Qt  
build miss the default QPA plugin  
* QTBUG-87326 Removal of "old time-zone lookup fallbacks" breaks TZ  
handling on Gentoo  
* QTBUG-92046 Description of Julian calendar is wrong  
* QTBUG-91714 QSizeGrip can not continue resize on the second screen  
* QTBUG-92011 Qt 6.1.0 betas fail to compile:  
qpaintengine_x11.cpp:2457:43: error: no matching member function for  
call to 'loadGlyph'  
* QTBUG-91788 Assert when removing a model from  
QConcatenateTablesProxyModel that is bound to a QSortFilterProxyModel  
* QTBUG-91029 Windows/Accessibility: Focused QListWidget is not  
announced by screen readers  
* QTBUG-89456 QTypeTraits templates break existing code  
* QTBUG-92087 No shortcuts possible with SysReq key  
* QTBUG-92051 The keyboard does not appear after changing the focus  
* QTBUG-91362 Cursor handle in wrong place when app is launched i split  
screen  
* QTBUG-86670 Fix qtwayland / qtquickcontrols2 static builds failing to  
reconfigure in a non-prefix build  
* QTBUG-92178 Editable Tree Model fails QAbstractItemModelTester  
* QTBUG-92173 [iOS]: Crash occurs when showing a new QQuickWindow after  
the first one is deleted  
* QTBUG-92220 QAbstractItemModelTester false positive  
* QTBUG-65927 Shift the coordinates under Android when I use QML + c++.  
* QTBUG-92235 Update dependencies failed on 'dev' in qt/qtsvg  
* QTBUG-69214 Android: tst_QFont::resetFont fails  
* QTBUG-86134 [Reg 5.9 -> 5.12] QPushButton: icon not aligned when menu-  
indicator is removed  
* QTBUG-90250 QPushButton: menu indicator with stylesheet not drawn  
correctly  
* QTBUG-92460 [Reg -> 6.2 24226bb5f595581a239356c18a338783a85349ca]:  
QLineEdit clear button and embedded icons are way too large  
* QTBUG-92245 androiddeployqt: Do not expect rcc in /bin  
* QTBUG-91878 Assert in QConcatenateTablesProxyModel::index if models  
are added while filtering QSortFilterProxyModel is used  
* QTBUG-92148 QSemaphore::acquire is not woken when release is called()  
* QTBUG-92275 Slow and memory intensive handling of input to  
QDateTime::fromString  
* QTBUG-90611 Shortcut Alt+` is not working with non US layout  
* QTBUG-92239 Incorporate Android's MediaStore into Qt for Android  
* QTBUG-92079 QFINDTESTDATA does not find data relative to test source  
* QTBUG-92490 Stylesheet with pseudo state on QPlainTextEdit  
* QTBUG-92451 Static build fails on MinGW and MSVC2019, shadertools?  
* QTBUG-87861 Handle PLUGIN_EXTENDS = - in qmake plugin projects and in  
pro2cmake  
* QTBUG-92459 "set_property can not be used on an ALIAS target" when  
building qttools dev  
* QTBUG-92040 [macOS] Labs platform context menu items are disabled on  
modal window  
* QTBUG-92096 QMenu Scrollable  will  reset Active Action  
* QTBUG-89508 Qt::makePropertyBinding does not work with read-only  
bindables  
* QTBUG-92568 Using QNetworkInformation will cause application crash  
when exit  
* QTBUG-91957 Assert while trying to load SVG  
* QTBUG-92205 TextEdit show tab character  error when tabStopDistance  
less than tab width  
* QTBUG-89467 .prl file generation is dependent on add_subdirectory  
order  
* QTBUG-91686 The use of "QLocale::Country" means that countries and  
regions are prone toambiguity  
* QTBUG-90962 QLocale constructor docs don't accurately describe the  
fall-back process  
* QTBUG-91676 Some tst_QProcess's don't need to link to Qt  
* QTBUG-73225 QT DST beyond 2037  
* QTBUG-92838 Redownloading same file in parallel produces a warning  
about removal of cache file  
* QTBUG-89108 cmake mime database compression with zstd fails  
* QTBUG-88093 qtbase unable to build with system jpeg  
* QTBUG-89844 QProperty's eager evaluation leads to inconsistent states  
* QTBUG-19983 Setting a cancel button on QProgressDialog more than once  
causes layout to be invalid  
* QTBUG-92908 gradients widget example crashes  
* QTBUG-92886 QAbstractItemModelTester false positive removing rows with  
no columns  
* QTBUG-83911 Proxy models maintaining the tree structure are impossible  
* QTBUG-92890 Qt 6.1.0 Android binary size on Windows host increased  
significantly  
* QTBUG-86847 QXmlStreamReader.prefix() cannot return EndElement's  
prefix  
* QTBUG-86823 REG: Blinking cursor leaving an artifact in QTextEdit  
* QTBUG-92962 tst_qproperty fails to compile with C++20 standard enabled  
* QTBUG-92963 tst_qpromise fails to compile with C++20 standard enabled  
* QTBUG-92260 QSortFilterProxyModel::setFilterRegularExpression(const  
QString &) preserves all pattern options  
* QTBUG-91885 QSqlTableModel support column names with dots  
* QTCREATORBUG-25389 Can't use manual tests from Creator  
* QTBUG-87579 Qt Android 6 with CMake is relying on deprecated ndk-  
bundle  
* QTBUG-93002 CMake: linker error with Linux Static Libraries while  
using QtQuick.Controls  
* QTBUG-93007 QThreadPool should make sure maxThreadCount is > 0 as < 1  
breaks it even though the docs say otherwise.  
* QTBUG-85136 "qmake -qtconf foo.conf -query" does not work  
* QTBUG-90030 Persistent index handling in QAbstractItemModel is wrong  
* QTBUG-93021 Qt6 Static build for macOS problem: Undefined symbols for  
architecture x86_64 and issues with libraries linking.  
* QTBUG-91405 qt-configure-module does not work as expected with multi  
config ninja generator  
* QTBUG-56322 Qt for Android source package build error in examples  
* QTBUG-92885 W System.err: java.lang.NoSuchMethodException:  
isKeyboardVisible []  
* QTBUG-87429 tst_QRhi::renderToTextureArrayOfTexturedQuad fails on  
Android Emulator in CI  
* QTBUG-87449 Example not compiling due '/usr/bin/ld: cannot find  
-lpnp_basictools'  
* QTBUG-92826 JSON documentation needs updating for deprecations  
* QTBUG-77427 setDropAction() is not respected in ItemViews during move  
operation on MAC  
* QTBUG-93270 QPropertyBindingSourceLocation won't compile bacause of  
wrong source_location selection  
* QTBUG-91284 Http2: authenticationRequired is not emitted  
* QTBUG-88441 No longer possible to build docs with an already installed  
qdoc  
* PYSIDE-1404 Incompatible import of "Object" in compiled UI  
* QTBUG-91770 qvnc: Arbitrary memory read vulnerability  
* QTBUG-67944 If user pressed back button during application startup.  
Application becomes unresponsive.  
* QTBUG-92940 MSVC: warning C4723: potential divide by 0 in Qt Gui  
* QTBUG-90945 SizeGrip missing  
* QTBUG-92584 QSqlTableModel ORDER BY doesn't quote table name [with  
spaces]  
* QTBUG-92579 Different Screen.pixelDensity and Screen.devicePixelRatio  
* QTBUG-71123 "moc" failed to parse auto in trailing-return-type signals  
and slots  
* QTBUG-93416 Sample code doesn't compile  
* QTBUG-61652 Android's virtual keyboard "OK" button must not accept the  
QDialog  
* QTBUG-63393 [iOS]: When typing in a TextEdit and then using Undo, it  
is only possible to undo the very last change  
* QTBUG-91171 QTextCharFormat setFontUnderline does not sets the  
attribute to document  
* QTBUG-88374 QTextDocument::toHtml: nested lists (ul, ol) not nested in  
output  
* QTBUG-91758 [REG 5.13.2->5.14.0]: QPainter renders <Spaces> in Text  
wrong when units  set to micrometers  
* QTBUG-92240 MDI Sub window title remains in main window title when  
DontMaximizeSubWindowOnActivation option used  
* QTBUG-85826 Some Windows fonts don't work in Text  
* QTBUG-85634 Japanese and Chinese characters have no effect by bold  
enabled  
* QTBUG-92988 if font size is set via stylesheet for QTab, it chops off  
text  
* QTBUG-84664 When QLineEdit is in password mode then it will still  
allow characters to be composed but it will lose what the intended  
character is  
* QTBUG-90840 QSyntaxHighlighter does not apply capitalization with  
QTextCharFormat::setFontCapitalization  
* QTBUG-91396 _NET_SUPPORTED not updated  
* QTBUG-93032 Reg:5.15.2->5.15.3 QPushButton Focus rect is change of  
behavior  
* QTBUG-39617 QML TextArea doesn't support  
QTextCharFormat::SpellCheckUnderline  
* QTBUG-91236 background-color does not propagate beyond first child  
element  
* QTBUG-93475 QPainter rotate causes pixmap rendering issues  
* QTBUG-92599 QLabel with word wrap makes unable to decrease parent  
items size  
* QTBUG-93620 W System.err: java.lang.NoSuchMethodException:  
notifyQtAndroidPluginRunning  
* QTBUG-93295 Session Resumption with Session ID - IPv6 -  
ephemeralServerKey is missing  
* QTBUG-74291 QTemporaryFile does not work for Windows network paths  
* QTBUG-91398 When QFont::NoFontMerging is set then if bold or italics  
is requested that is not provided by the font then it will end up not  
synthesizing this  
* QTBUG-92366 QListView has abnormal spacing when setWordWrap is true  
* QTBUG-93635 Reg->6.0: Windows vista style: placeholderText has wrong  
color  
* QTBUG-87334 Graphical issue on some Android smartphones: white line at  
the top and the right side of the screen  
* QTBUG-93387 Versionless targets hide finalizers set on versioned  
targets  
* QTBUG-89145 QStandardItemModel takeItem / takeChild does not emit the  
right signals  
* QTBUG-84494 Keyboard layout not managed on Keys.event  
* QTBUG-88989 Build errors on Android with latest gradle  
* QTBUG-70137 Dockwidgets - Placing QDockWidget is almost impossible  
* QTBUG-93636 Unnecessary hard link from qmake.exe to qmake6.exe  
* QTBUG-93713 Trivial WASM example crashes when running for a minute  
* QTBUG-93494 iOS A11Y VoiceOver: QAccessible::EditableText not  
implemented as "TextField" and value is missing last character  
* QTBUG-93739 QT 6.1.0 does not compile with -DQT_NO_EXCEPTIONS=1  
* QTBUG-92182 Qt Dock Widgets super slow to dock  
* QTBUG-93431 Android: build system dependencies are wrong  
* QTBUG-93305 QItemSelectionModel does not emit selectionChanged on row  
removal (under conditions)  
* QTBUG-93707 QT_HOST_BINS and -LIBS path incorrect on qmake -query  
* QTBUG-93779 [elxr] (error #412) unresolved symbols: 1  
* QTBUG-93750 Updating dependencies in qtdeclarative fails  
* QTBUG-93831 [REG 5.15.2->5.15.4]: Android: Copy-pasting text is not  
possible after pasting  
* QTBUG-92188 Stack smashing detected using QImage::scaled  
* QTBUG-71701 QFileSystemModel fails to locate a host from the root  
node's visible children  
* QTBUG-85051 CMake doesn't support big resources  
* QTBUG-93770 Wrong pixel ratio when using OpenGL in an embedded window  
context  
* QTBUG-89951 Why does Qt 6 cmake add `UNICODE` to public definitions on  
Windows?  
* QTBUG-93072 Invalid enum value in  
QTextHtmlParser::tableCellBorderStyle  
* QTBUG-93895 Error C2440: 'initializing': cannot convert from 'const  
TCHAR *' to 'const wchar_t *  
* QTBUG-93760 tst_macdeployqt::basicapp fails with macOS 11 ARM  
* QTBUG-91095 wasm: app loses focus as mouse moves around widgets  
* QTBUG-93943 target "Qt::ZlibPrivate" but the target was not  
* QTBUG-93230 Conflict name for qt_add_resources  
* QTBUG-69555 QHash freezes due to call to getrandom() via glibc 's  
getentropy()  
* QTBUG-92910 Hashing for nested QPair is broken in Qt 6  
* QTBUG-93858 Some XKB letter keysyms are not properly converted to  
corresponding Qt keys  
* QTBUG-49771 Backspace key is not working when CapsLock is on  
* QTBUG-93852 QLoggingCategory documentation doesn't state under which  
conditions it is enabled by default  
* QTBUG-88651 Can't Hide Menu Separator  
* QTBUG-93736 QCombobox last item become inaccessible when a listview is  
used in popup  
* QTBUG-92488 When a QComboBox is set to use Fusion style after changing  
the size adjust policy to AdjustToContents then it will cut off the last  
item in a list and force it to be scrollable  
* QTBUG-94073 Comment error  
* QTBUG-92583 QListVIew page turning error  
* QTBUG-94077 qmlimportscanner is missing, making all Android packages  
unusable  
* QTBUG-93504 Running automoc with --collect-json stalls during cmake  
build with Makefiles  
* QTBUG-36565 Some key symbols generated by xkb level 3 shift don't work  
in QTextBrowser, QTextEdit, QLineEdit  
* QTBUG-93841 Superfluous calls to int qRegisterMetaType(const char  
*typeName)  
* QTBUG-94064 D3D11 debug layer warning is printed when having a vertex  
shader with no inputs  
* QTBUG-94070 Memory corruption in sqlite plugin  
* QTBUG-93600 90° X rotation as quaternion produces NaN on euler angle  
* QTBUG-93995 Doc: Clean up warnings in qtbase  
* QTBUG-93174 QtDeviceUtilities doc build doesn't produce .qch file  
* QTBUG-93839 QtQuick not included when cross-compiling in a top-level  
build due to missing qsb  
* QTBUG-89754 Reg->6.0/Linux/CMake build : QtGui has dependency on  
libopengl0  
* QTBUG-83089 NameFilters not working in FileDialog in Android 10  
* QTBUG-94143 QProperty: tst_qsequentialanimationgroup crashes  
* QTBUG-89273 Building almost any Qt example for iOS throws a big list  
of warnings  
* QTBUG-73990 Context Menu Items Fonts and Hotkeys Not Displaying  
* QTBUG-90442 QFileDialog::saveFileContent crashes on accept  
* QTBUG-94178 QNativeGestureEvent with gestureType EndNativeGesture  
should have QEventPoint::state == Released  
* QTBUG-77771 A Double click on QtreeView/QTreeWidget index is emitting  
two clicked() and one doubleClicked() signal  
* QTBUG-92250 Change the order of libraries and object files in the  
generated .prl files  
* QTBUG-93742 Error in public function "setclearbuttonenabled" of  
"QLineEdit" control  
* QTBUG-94156 Unknown CMake command "qt_finalize_executable"  
* QTBUG-94108 [REG 6.1.0 -> 6.2] No TLS backend available in statically  
built project  
* QTBUG-92266 vertical space before video on  
https://doc.qt.io/qt-6/gettingstarted.html  
* QTBUG-94220 Update dependencies on 'dev' in qt/qtquickcontrols2 fails  
* QTBUG-87813 WASM: App sometimes crashes on aborting NetworkRequest  
* QTBUG-93868 Fix unnoticed regression after merging the fix for UNC  
path handling  
* QTBUG-94057 QLineEdit should be enter editing status when FocusIn  
* QTBUG-94124 Update dependencies on 'dev' in qt/qtlocation fails  
* QTBUG-94211 Windows Long Path issue for RelWithDebInfo config  
* QTBUG-92234 QTranslator.load problem by skipping some  
* QTBUG-89588 androiddeployqt fails with error from qmlimportscanner if  
qtdeclarative is not installed  
* QTBUG-59888 UX Issue: Drag & Drop does not work well with  
MultiSelection/ExtendedSelection  
* QTBUG-94226 QListView - broken drag-n-drop items movement  
* QTBUG-86754 [Reg 5.12.4-> 5.12.5]Action text overlaps the shortcut in  
menu when padding is used  
* QTBUG-94213 Type normalization of QMetaType does not match runtime  
type normalization  
* QTBUG-94264 When building for Android, instead of an apk, just .so is  
built  
* QTBUG-94269 QIntValidator: integer values exceeding top "intermediate"  
according to validate() func  
* QTBUG-92232 [REG] Option Clicking Window Close Button Crashes App  
* QTBUG-65637 Window minimizing broken after building QT app with Mac OS  
High Sierra SDK  
* QTBUG-91025 Should mention that QPrint Support is not available for  
iOS  
* QTBUG-64543 When starting a drag scroll via QScroller in a listview  
there will be a slight jump right before the scrolling starts  
* QTBUG-50866 QTabBar scroll buttons overlap tabs  
* QTBUG-70498 Cannot scroll first tab right, using scroll button in  
QTabBar, when tab size do not fit into visible rect.  
* QTBUG-94248 Check scrollbar ScrollBarOverlap when computing QListView  
margins  
* QTBUG-27640 QToolButton::menu-arrow{image:none;} does not work in  
Custom TitleBar  
* QTBUG-84117 QHeaderView sort indicator and text overlap if both  
aligned right  
* QTBUG-86362 [Reg 5.14 to 5.15.0] macOS: Tabbed QDockWidgets not  
properly drawing the tabs  
* QTBUG-71894 Hangul composition bug  
* QTBUG-94400 /EHsc flag removal wrong  
* QTBUG-91120 QDate::fromString() fails on isolated dates on macOS with  
TZ=Europe/Lisbon  
* QTBUG-94347 QRandomGenerator64 refers to functions as static, aren't.  
* QTBUG-20456 QAbstractItemView: When clicking on an item that is being  
edited and the edit trigger is SelectedClicked it should just stop  
editing  
* QTBUG-94470 Incorrect parsing of HTTP2 frame headers.  
* QTBUG-94032 Command line is too long when building large projects  
* QTBUG-92878 [qt6/cmake] Qt Resource object libraries not found in  
sibling scopes due to not being global  
* QTBUG-94532 Markdown checkboxes are clipped when text range selected  
* QTBUG-93764 QPrintPreviewDialog: printer orientation not updated by  
QPageSetupDialog  
* QTBUG-94568 Build error when depending on internal module in qtbase  
* QTBUG-94448 QtWidgets: Some stylesheets explode Designer and the whole  
linux terminal (recursion crash)  
* QTBUG-94501 GStreamer::Gl dependency is not recorded correctly in a  
static build  
* QTBUG-89379 QQuickWindow::QtTextRendering cause font problem on Apple  
M1  
* QTBUG-85714 QOpenGLWidget with NativeWindow QDockWidget does not  
render when undocked  
* QTBUG-94069 MacOS ComboBox Focus Ring is Too Tall  
* QTBUG-82835 Stale socket notifications can be emitted to new sockets  
* QTBUG-91130 SIGSYS error in QSystemSemaphore for iOS  
* QTBUG-94175 QGraphicsProxyWidget: rendered Arabic text incomplete in  
large font sizes when OpenGL is used  
* QTBUG-85529 Polytonic Greek characters cannot be composed both ways  
* QTBUG-94246 Memory leak in qsql_oci plugin  
* QTBUG-94706 missing documentaiton details about QFile::copy()  
* QTBUG-94591 qmake doesn't search mkspecs files in the right location  
* QTBUG-94538 Change cursor theme is not applied immediately . The Qt5  
app needs to be restarted.  
* QTBUG-92083 Building console project fails with linker errors  
* QTBUG-91919 Qt will crash if changing screen resolution on Mac  
* QTBUG-83869 Correction to the documentation:  
https://doc.qt.io/qt-5/qtransform.html#basic-matrix-operations  
* QTBUG-81251 _debug libraries are missing from pre build Qt on Mac  
* QTBUG-94708 qCDebug() and friends could pass the category as a tag in  
Android  
* QTBUG-94527 Building Android QML projects with qmake is broken  
* QTBUG-94839 QSystemTrayIcon::isSystemTrayAvailable() opens a new file  
descriptor on each call which isn't closed  
* QTBUG-92477 Memory leak in QFontDatabase  
* QTBUG-88508 some tests are not saving result output to file on Android  
* QTBUG-92157 Qt configured without Vulkan support in 6.1 Android  
packages [Vulkan crashes on SA8155 (Qualcomm)]  
* QTBUG-93890 Crash in webOS emulator with recent meta-qt6  
* QTBUG-94944 qt6_qml_type_registration with VS19 cmake generator  
outputs error: "The dependency target "qt6-test_autogen" of  
target"qt6-test_automoc_json_extraction" does not exist.  
* QTBUG-38776 QDockWidget titlebar icons are not drawn with high DPI  
* QTBUG-94802 [Reg-5.15.4->5.15.5]Menu separator is not visible  
* QTBUG-94973 Build fails when configuring twice with CMake and with  
both INSTALL_MKSPECSDIR and QT_QMAKE_TARGET_MKSPEC set  
* QTBUG-95005 Typo in QOpenGLPaintDevice::dotsPerMeterY  
* QTBUG-91632 Make /usr/local/Qt-6.x the default install folder instead  
of /usr/local  
* QTBUG-94824 In qlinedit, icon and text overlap  
* QTBUG-95027 Building a DEBUG CMake project against a -debug-and-  
release Qt fails  
* QTBUG-95039 String translations cancelled in qsystemerror.cpp  
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
* QTBUG-92561 Strange selection behavior of with ExtendedSelection +  
SelectRows  
* QTBUG-95011 QLineEdit inconsistently changes layout direction when  
text changes  
* QTBUG-95077 [5.15/6.1->6.2] Some library names now have a "Private"  
suffix  
* QTBUG-73966 When using QMenu::icon:checked inside a stylesheet it is  
being ignored and has no effect  
* QTBUG-83619 Stylesheet: QAbstractItemView::indicator changes selected  
item text color  
* QTBUG-94981 QTreeView: expandToDepth() and expandAll() ends  
prematurely for asynchronous models  
* QTBUG-89022 QImageWriter insufficiently supports QSaveFile  
* QTBUG-95013 pt_BR translations not loaded  
* QTBUG-94788 QListView will be reset when setSelectionMode  is  
MultiSelection  
* QTBUG-94942 QML type registration emits "qt6quick_metatypes.json:  
illegal value"  
* QTBUG-95198 Building QtMultimedia qmake projects is broken on Windows  
* QTBUG-86846 the password box not refreshed under Chinese input method  
* QTBUG-93829 QItemSelectionModel::hasSelection is inconsistent  
* QTBUG-94737 Crash in QThreadOnce test  
* QTBUG-95009 QNetworkDiskCache::cacheSize() returns a size twice as  
large as the real one.  
* QTBUG-95277 HTTP2: QNetworkReply::encrypted not emitted  
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
* QTBUG-91459 When using Speech Recognition on a multiple monitor setup  
telling it to click a button does not always work on the secondary  
monitor  
* QTBUG-95334 QMap<QString,QString>::const_iterator cannot do "it+1" any  
more  
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
* QTBUG-20894 QCompleter unexpectedly changes QLineEdit text  
* QTBUG-56595 QXcbConnection::getTimestamp() returns old timestamp  
* QTBUG-69515 Linux, WindowStaysOnTopHint does not work.  
* QTBUG-95635 qtbase fails to configure on Linux with CMake 3.21.1 and  
policy CMP00126 enabled  
* QTBUG-95655 CMake couldn't find "FindWMF.cmake" in top-level builds  
* QTBUG-95071 mysql client version detection broken with MariaDB 10.6  
* QTBUG-8096 icon-size stylesheet property is defined as length but only  
lengths in px can be used  
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
* QTBUG-95441 6.2: The basic QFont constructor deprecated?  
* QTBUG-69975 Cocoa NSFullSizeContentViewWindowMask was wiped when  
toggling fullscreen  
* QTBUG-95639 MariaDB 10.6 prepared queries metadata cache causes  
breakage in mysql driver  
* QTBUG-95214 QtConcurrent::run requires the return type to be default-  
constructible  
* QTBUG-95602 App wizard QtQuick Empty with language failed to find Qt  
component "LinguisticTools"  
* QTBUG-95841 [REG-5.15->6.2]QMainWindow::VerticalTabs is broken in Qt6  
* QTBUG-95389 link in QSet documentation missing  
* QTBUG-95806 Qt6WasmMacros.cmake uses wrong paths for wasm_shell.html,  
qtloader.js and qtlogo.svg  
* QTBUG-95795 Crash when running a qt quick app on iOS simulator  
* QTBUG-81770 Garbled character is displayed when switching Arabic to  
another language  
* QTBUG-30522 macOS: Closing application window while context menu is  
open leaves menu open  
* QTBUG-94215 [Reg 5.15.2->5.15.3/6] QString::lastIndexOf is broken  
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
* QTBUG-94091 Nested Graphicsview does not works as expected  
* QTBUG-94951 Qt 6.2 alpha assertion failed in qunicodetools.cpp  
* QTBUG-87128 In the help pages: The QFileInfo::setFile() example is  
really the QDir::setCurrent() one  
* QTBUG-45737 No touch events handling (QGraphicsProxyWidget / QWidget)  
* QTBUG-96009 tst_QGraphicsProxyWidget::mouseDoubleClickEvent fails  
* QTBUG-89549 Linker error when building Qt 6 statically with cmake +  
clang on Windows  
* QTBUG-46300 Qt's application ignore some input method behavior  
* QTBUG-72744 macOS: Qt does not hide cursor when entering text  
* QTBUG-88774 QNetworkAccessBackend documentation is missing a class  
entry  
* QTBUG-96101 QPMCache deleted from another thread  
* QTBUG-92018 QLocale date toString uses standalone name where plain  
name should be used  
* QTBUG-95463 QListView in view mode QListView::IconMode crashes when  
the last row is moved  
* QTBUG-96067 Build failure with riscv32  
* QTBUG-46701 Closing a full screen window via Qt APIs leaves the screen  
black on macOS  
* QTBUG-89562 qt_lib_network_private.pri contains  
QMAKE_LIBS_OPENSSL/NOLINK entry  
* QTBUG-52450 macOS: Closing a window that's in fullscreen removes the  
window, but doesn't exit fullscreen  
* QTBUG-68069 Exiting fullscreen window leaves the application in  
fullscreen mode on macOS  
* QTBUG-81552 macOS: Wrong cursor shown when the mouse is moved slowly  
into window  
* QTBUG-95358 Possible null pointer dereference in qpixmap.cpp  
* QTBUG-96197 Yocto build fails in CI for 6.2.0-beta4 qtbase  
* QTBUG-96170 WASM: data URI scheme does not work  
* QTBUG-91707 [Reg 5.15->6.0] Recursive QMap as MetaType cannot have key  
with custom operator==  
* QTBUG-91059 Mac: Multiple modal dialogs block all input  
* QTBUG-95565 Qt Creator cannot build Qt 6 for iOS from the start  
* QTBUG-96062 Integrity linker can't cope with duplicate object files on  
command line  
* QTBUG-96285 QProcess can't be restarted  
* QTBUG-96619 QRhi declares types with non-relocatable QVLA in them as  
relocatable which can lead to crashes  
* QTBUG-96606 CA certificates not fetched on Android  
* QTBUG-96690 Qt6. Build failed when use std::optional as a signal  
argument  
* QTBUG-54848 Problem with QAbstractItemDelegate and IME (chinese Input  
Method) with edit trigger QAbstractItemView::AnyKeyPressed  
* QTBUG-96838 signing Android app bundles fails with 6.2.0-rc  
* QTBUG-89423 QAbstractItemModel::multiData SC/BC fallout  
* QTBUG-84906 qt6_qml_type_registration requires automoc  
* QTBUG-90980 CMake configure failure with given multiline toolchain  
file  
* QTBUG-20984 tst_macgui autotest is unstable  
* QTBUG-90943 Qt 6.0.0 ignores ANDROID_PACKAGE_SOURCE_DIR  
* QTBUG-91052 qmlcachegen adds Windows paths when cross-compiling on  
Linux  
* QTBUG-90483 Revert deletion of qmake project files for snippets  
compilation  
* QTBUG-56552 QDateTime/QTime truncates milliseconds when converting to  
Qt::ISODate string  
* QTBUG-88728 80M of rows crash QTableView while 70M do not  
* QTBUG-90662 Fix CI warnings qtbase  
* QTBUG-91180 Cant' start Android emulator with Ubuntu 18.04  
* QTBUG-91147 Correct wrong snippet paths reported by CI  
* QTBUG-91104 REG->6.0/Windows : QFileSystemModel no longer displays  
file icons  
* QTBUG-86013 [evdev] protocol b touch device doesn't get release event  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
* QTBUG-89082 The previous tips is still displayed when mouse move to  
another Action without tips.  
* QTBUG-89948 [HiDpi] Qt renders incorrectly if user's scaling factor is  
less than 1  
* QTBUG-82617 Crash on exit via back button on Huawei Mate 20 Pro  
* QTBUG-83932 Port configure.cmake missing libraries that are marked  
with FIXME  
* QTBUG-91423 tst_QGlobalStatic gets stuck after "realloc(): invalid  
next size" message  
* QTBUG-91392 ProtocolFailure with certain HTTP requests to  
transmission-daemon  
* QTBUG-91253 QConcatenateTablesProxyModel crushes being sourceModel in  
QSortFilterProxyModel  
* QTCREATORBUG-23574 cmake support for iOS  
* QTBUG-79140 [REG 5.13.0 -> 5.14.0]OTF fonts don't work correctly  
* QTBUG-91888 Item2D + importScene = crash due to the well-known dead-  
rhi-objects-in-cache-key problem  
* QTBUG-91782 clang compiler crashes in CI  
* QTBUG-87580 Add minimal set of tests to build for static Qt configs in  
Coin  
* QTBUG-92211 Android emulator VM fails to run  
tst_QRhi::renderPassDescriptorCompatibility once OpenGL ES 3.0 is  
enabled  
* QTBUG-91417 Selection does not work in read-only text editing controls  
- QtWidgets  
* QTBUG-92163 top-level configure returns with exit code != 0 if qt3d is  
checked out  
* QTBUG-52523 tst_gestures event counts fail on RHEL 7.x  
* QTBUG-92861 QtQml does not provide version 6.2  
* QTBUG-92947 QPalette doesn't return the correct color when querying  
QPalette::PlaceholderText  
* QTBUG-91911 Qt combines values from unrelated enum types  
* QTBUG-58013 Cursor position changes not properly passed to input  
method  
* QTBUG-93033 Deprecated Function "isTopLevel" in qwidget.h defined  
* QTBUG-90341 The QtStartUpFunction function may be called repeatedly  
* QTBUG-93069 QSettings leads to deadlock  
* QTBUG-93037 Conan builds are unable to run tst_qmake  
* QTBUG-86033 Update QtPlatformAndroid.cmake to include features in the  
old Qt5AndroidSupport.cmake  
* QTBUG-93093 The tests for QSharedPointer are disabled  
* QTBUG-91801 Potential memory leak in sending queued signals?  
* QTBUG-93019 [REG 5.15-6.0] QList/QVector regressions  
* QTBUG-93176 Data race in tst_qurl::testThreading() detected by Thread  
Sanitizer  
* QTBUG-92930 QRawFont::advancesForGlyphIndexes seems to ignore  
KernedAdvances  
* QTBUG-92944 input problems in DynamicTexture example  
* QTBUG-87057 QListView item looses items from models that don't  
override moveRows during internal drag'n'drop  
* QTBUG-92500 When using a ShaderEffect which has been compiled with the  
qsb tool, it does not apply the effect at all  
* QTBUG-89512 binding a computed property to another property should  
give an error  
* QTBUG-86677 QToolBar button resize chops text  
* QTBUG-93565 Unnecessary dependency to host Tools package in cross-  
builds  
* QTBUG-63557 Showing / hiding QML Dialog type keeps allocating memory  
without releasing it  
* QTBUG-71900 Double tapping on a word does not show the selection  
handles in the right place after the initial selection  
* QTBUG-80863 [cmake] excessive compilation of Import.cpp files for  
static plugins  
* QTBUG-88414 CMake multi-config build still build some debug tools  
* QTBUG-64446 tst_QWidget::multipleToplevelFocusCheck() on linux  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
* QTBUG-92905 QFile/pipe reading blocks when using a file descriptor  
instead of a handle  
* QTBUG-93838 Consider SHA-1 algorithm deprecated  
* QTBUG-90799 Select handles Left- and RightPoint goes to the wrong  
place when double tapping on a word on the widget dialog  
* QTBUG-62102 QKeySequenceEdit handles meta keys incorrectly on Wayland  
* QTBUG-93360 Compile Qt with gcc 11  
* QTBUG-87775 Passing INTERNAL_MODULE to qt_internal_add_module should  
only create a single Qt::FooPrivate target  
* QTBUG-94043 MSVC warning C4996: 'ID2D1Factory::GetDesktopDpi':  
Deprecated. Use DisplayInformation::LogicalDpi for Windows Store Apps or  
GetDpiForWindow for desktop apps.  
* QTBUG-94127 Testing in android emulator hangs  
* QTBUG-85879 Print Preview inconsistent icons  
* QTBUG-94194 Qt 6.1/6.1.1 compilation fails after MSVC 2019 16.10  
update with "/std:c++latest" compiler flag  
* QTBUG-93752 When setting the inactive colorgroup in the palette and  
then making the window inactive it will not trigger an update on any  
colors bound to the palette  
* QTBUG-87263 QMap<QVariant, QVariant> compilation error  
* QTBUG-60822 [REG: 4->5] WA_TranslucentBackground cannot be changed  
after widget has been shown  
* QTBUG-88248 QObject orphaned connections soft-leak  
* QTBUG-88081 Failed to build Qt from source through clang-cl  
* QTBUG-92941 REG 5->6: QVector size() does not reach capacity() before  
reallocating  
* QTBUG-89536 Remove configure.json files for building Qt 6  
* QTBUG-94613 [FTFBS] qttools does not compile: QtTools/private/qttools-  
config_p.h: No such file or directory  
* QTBUG-94753 QtFlagHandlingHelpers.cmake overrides flags -On from the  
user  
* QTBUG-87989 "ASan runtime does not come first in initial library list"  
when building Qt Quick application with Qt configured with -sanitize  
address  
* QTBUG-94355 Revice changes in configure summary options, 6.1.1 ->  
6.2.0  
* QTBUG-85201 Deprecate Ministro in Qt for Android  
* QTBUG-94971 QHoverEvent::scenePosition() is actually local position  
* QTBUG-91713 QtBase benchmarks fail for qtimezone, qdiriterator, and  
qfile  
* QTBUG-95004 XCB: Qt packages are built without session management  
support  
* QTBUG-88090 Installed CMake files reference the SOURCE TREE  
* QTBUG-94463 QThreadPool creates one thread more than maxThreadCount  
* QTBUG-95199 Incorrect propagation of iOS bitcode and -fapplication-  
extension flags to user projects  
* QTBUG-95208 Linker error regarding bitcode when linking CMake app  
targeting iOS  
* QTBUG-95268 test_QT_TESTCASE_BUILDDIR fails when built with CMake 3.21  
* QTBUG-95303 Internal module pri files are missing public include  
header locations  
* QTBUG-85839 Documentation: wrong default value for Layout Direction  
* QTBUG-80957 QFutureInterface: reportResults with an empty vector  
breaks results  
* QTBUG-95394 Crash in RHI when exiting a QtWaylandCompositor with  
active clients.  
* QTBUG-53706 QString::number(-17, 16) should return "-11" not  
"0xffffffffffffffef"  
* QTBUG-94831 Crash on MSVC in ~QMetaTypeFunctionRegistry() on program  
end with dynamically loaded Qt  
* QTBUG-95314 WASM: Diverging timezones in C++/QML  
* QTBUG-95532 Can't build qtquickcalendar due to missing SQL dependency  
* QTBUG-58749 QListView AdjustToContents not working  
* QTBUG-95072 Menu is shown at displaced position on enable/disable  
* QTBUG-71590 Qt is using "Non-SDK" interfaces, will be blocked by  
Android  
* QTBUG-95453 Mouse move pointer does not reflect when drag will move -  
eglfs  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-95845 qt_add_qml_module unconditionally installs metatypes.json  
files into "arbitrary" directory  
* QTBUG-93340 trafficlight_qml_dynamic crashes on Android device  
* QTBUG-89122 Building Qt with cmake needs 15% more space than with  
qmake  
* QTBUG-95668 Webengine widget not visible in Designer UI  
* QTBUG-35700 single punctuation input via CJK input method doesn't work  
* QTBUG-95921 scxml examples fail to build for iOS target  
* QTBUG-89296 No way to specify C standard for Visual Studio 2019 in  
qmake project  
* QTBUG-95661 Test result counts are incorrect  
* QTBUG-94451 Switch Android target SDK to 30 for Qt 6.2  
* QTBUG-39125 Cocoa: When typing in a Korean character and then press  
enter, it will take two presses before the enter key is actually invoked  
* QTBUG-96121 Versionless CMake commands prevent setting variables in  
calling scope  
* QTBUG-88535 List of modules in configure output is incomplete  
* QTBUG-96219 Conversion of versionless wrapper functions to macros  
needs to be reverted  
* QTBUG-84877 QLocale::system() uses short names of days and months for  
narrow formats  
* QTBUG-96303 Review (again) CodeChecker issues for Qt Core  
* QTBUG-95832 QtRemoteObjects CMake API is using the internal  
qt_manual_moc API  
* QTBUG-96127 Broken external links in Qt docs  
* QTBUG-96441  [REG 6.1.0 - 6.2.0] Windows: QWindow doesn't respect  
minimumWidth/minimumHeight  
* QTBUG-96790 crash in QWindowsFileSystemWatcherEngine::addPaths  
* QTBUG-96718 Crash in inBindingWrapper() (Creator built against Qt 6.2  
build)  
  
### qtsvg  
* QTBUG-91507 Out of bounds read in function  
`QRadialFetchSimd<QSimdSse2>::fetch` when input craft svg file  
* QTBUG-90744 [REG: 5.13 -> 5.14] QPixmap::load returns false for svg  
files if file encoding not utf-8 & format not specified  
* QTBUG-32405 QSvgRenderer::boundsOnElement broken for text nodes  
* QTBUG-94878 QSvgRenderer crash  
* QTBUG-92184 QtSVG cannot understand minified SVGs if they contain arcs  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
* QTBUG-94030 Minimal plugin not found in static build although  
explicitly imported  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
  
### qtdeclarative  
* QTBUG-70141 Warnings when using DialogButtonBox  
* QTBUG-70729 heap-use-after-free when running qmlbench with Menu as  
delegate  
* QTBUG-70064 tst_QQuickApplicationWindow::font() crash on macOS 10.13  
* QTBUG-71066 QML MenuItem disappear after highlighting using  
Instantiator  
* QTBUG-71444 [REG: 5.11-5.12] Segfault on any 5.12.0 version  
* QTBUG-71583 MenuItem state with checkable MenuItem faulty  
* QTBUG-71770 Regression in QQC2 Menu destruction  
* QTBUG-71952 Quick Controls 2 fixes for building with qreal=float  
* QTBUG-71974 TableView: does not work together with ScrollView  
* QTBUG-63834 Missing Qt module requirement in QQuickStyle class  
description  
* QTBUG-71554 QQuickIconLabel reports an incorrect baselineOffset  
* QTBUG-71875 Background of Material style TextField doesn't respect  
control width  
* QTBUG-71902 REG->5.12 RC: QQC2: Incorrect font size  
* QTBUG-72372 Button outside dialog if there is only one standardButton  
defined  
* QTBUG-72746 QQuickWindow segfault on destruction  
* QTBUG-72811 [Reg 5.11 -> 5.12] QQC2 buttons not react to click when  
holding for about a second  
* QTBUG-73179 qt.labs.platform.FileDialog folder property doesn't work  
* QTBUG-72786 ComboBox: can't customize popup palette  
* QTBUG-73412 Dial.inputMode property not recognized by Qt Creator  
* QTBUG-72023 Fusion Qt Quick Controls style no longer honors  
palette/font settings from qtquickcontrols2.conf  
* QTBUG-69540 QtQuickControls 2 Menu highlights disabled item on click  
* QTBUG-70181 QtQuickControls 2 disabled MenuItems take part in arrow  
key navigation  
* QTBUG-73447 Changing QtQuick Controls 2 Menu enabled State Breaks  
Coloring  
* QTBUG-66494 Dialog with only title set causes binding loop on  
implicitWidth  
* QTBUG-73754  
tst_controls::Default::TextField::test_ignorePressRelease() and  
test_pressedReleased() failed  
* QTBUG-73354 QtQuickControls 2 menus don't handle Enter key  
* QTBUG-74130 tst_cursor::controls(containers) failed on win7  
* QTBUG-72536 [REG 5.11.2 -> 5.12] TextArea's initialization with long  
text bug  
* QTBUG-74276 Segfault with basic SplitView example  
* QTBUG-72886 [REG 5.11.2-5.12 ] DialogButtonBox breaks when button text  
is changed  
* QTBUG-74512 tst_sanity.cpp:186:23: error: variable type  
'FunctionValidator' is an abstract class  
* QTBUG-70161 iOS: editable QML combobox menu does not open  
* QTBUG-70451 DialogButtonBox to order buttons as defined when absent of  
buttonRole  
* QTBUG-74711  
DialogButtonBox::test_oneButtonAlignedRightInImplicitWidthBox is flaky  
* QTBUG-74688 SpinBox indicators stay hovered after being pressed and  
moving the mouse away  
* QTBUG-69096 Pane's documentation doesn't fully explain  
contentWidth/Height behaviour  
* QTBUG-74661 ComboBox popup cannot have focus  
* QTBUG-75072 Accessibility: ScrollBar does not scroll when increasing  
value  
* QTBUG-73604 tst_accessibility in QtQuickControls2 fails on Android  
* QTBUG-75051 When calling QQmlEngine::retranslate() it will cause the  
background of a highlighted MenuItem to be smaller than the Menu width  
* QTBUG-75844 iOS: Text cursor hides while showing magnifier glass  
* QTBUG-75572 Enum type conversion issue  
* QTBUG-76356 Incorrect accessibleRole for 'Switch' QML  
* QTBUG-76077 SplitView documentation says "import QtQuick.Controls 2.5"  
but was added later  
* QTBUG-76378 Error copying C:\Users\qt\work\qt\qtquickcontrols2\src\imp  
orts\controls\designer\images*.png to  
..\..\..\qml\QtQuick\Controls.2*.png: Cannot open C:\Users\qt\work\qt\qt  
quickcontrols2\src\imports\controls\designer\images*.png for input  
* QTBUG-76164 tst_controls crash on macOS 10.12  
* QTBUG-75972 ComboBox count isn't updated on model change  
* QTBUG-73128 tst_qquickmenubar::Default::mouse() is flaky  
* QTBUG-76369 TextArea draw something strange when use "Material Style"  
* QTBUG-77840 TabBar links to wrong page  
* QTBUG-77909 tst_revisions::window() failed  
* QTBUG-77946 tst_QQuickDrawer::Universal::position(right) failed on  
Linux openSUSE_15_0 (gcc-x86_64)  
* QTBUG-75338 Editable ComboBox: currentIndex is not set to -1 and  
currentText not cleared after confirming non-existent value  
* QTBUG-77734 tst_Snippets::verify(qtquickcontrols2-combobox-custom)  
'warnings.isEmpty()' returned FALSE. ()  
* QTBUG-75085 When calling QQmlEngine::retranslate() then it will not  
have any effect on the buttons in a DialogButtonBox  
* QTBUG-78252 qquickstackelement.cpp:213:82: error: too few arguments to  
function call, expected 6, have 4  
* QTBUG-78470 tst_calendar::MonthGrid::test_range() and  
WeekNumberColumn::test_range() failed  
* QTBUG-66799 Tumbler: displacement calculation goes wrong if wrap is  
disabled and tumbler gets resized  
* QTBUG-73243 ToolTip will crash application  
* QTBUG-76029 REG: Performance regression in Quick Controls 2 Combo Box  
* QTBUG-78790 NinePatchImage crashed when source changed  
* QTBUG-50027 Behaviour and styling of TabBar and TabButtons in  
Universal style  
* QTBUG-79150  
tst_controls::Default::Tumbler::test_currentIndexAtCreation() failed on  
all places  
* QTBUG-79270 Crash, if SplitView have only 1 item and changing  
visibility  
* QTBUG-79370 tst_QQuickPopup::Default::cursorShape() is failing in CI  
* QTBUG-77306 MenuBarItem does not lose highlight when a Menu is added  
using MenuBar.addMenu  
* QTBUG-79302 New SplitView ignores children generated by Repeater  
* QTBUG-79326 Dialog is not getting closed with Esc key press even with  
closePolicy set to Popup.CloseOnEscape  
* QTBUG-79501 When a Drawer isn't modal, isTabFence should be false  
* QTBUG-78858 Editable ComboBox is very slow  
* QTBUG-79275 QQC2: libqtquickcontrols2imaginestyleplugin should be much  
smaller  
* QTBUG-79790  
tst_controls::Default::Control::test_font_explicit_attributes(family)  
failed  
* QTBUG-79929 tst_qquickmaterialstyleconf::conf() failed  
* QTBUG-62401 Items derived from Container does not deliver key events  
to children  
* QTBUG-62350 ToolTip control's text does not automatically wrap  
* QTBUG-79952 Material style doesn't work with Qt 5.14.0 Beta 2  
* QTBUG-80164  
tst_QQuickPopup::Universal::closeOnEscapeWithVisiblePopup() is flaky on  
openSUSE  
* QTBUG-80153 tst_controls::Default::Dial::test_dragging(live) failed  
* QTBUG-79464 Focus is lost when Dialog is closed during another Dialog  
exit transition  
* QTBUG-66583 Accessible.name for Qt Controls 2 Button cannot be set  
* QTBUG-79846 Custom QtQuick with hover events breaks an splitview  
* QTBUG-80353 Crash in StackView by triggering consecutive calls to  
clear method  
* QTBUG-78885 ComboBox does not select currently suggested item when  
pressing tab  
* QTBUG-57267 StackView: pushing an item again before its exiting  
animation ends visually clears the stack  
* QTBUG-71406 Editable ComboBox text is not selectable with the mouse.  
* QTBUG-78202 QML ToolTip is closed unexpectedly  
* QTBUG-81216 [REG?] QQuickStyle::setFallbackStyle() not working any  
more in 5.14 on Android  
* QTBUG-80970 Failing to run QML RangeSlider customization example  
* QTBUG-75682 (plugins.qmltypes and) designer/* don't get copied anymore  
during build  
* QTBUG-81796 Text of explicitly declared Buttons in DialogButtonBox not  
rendering  
* QTBUG-77202 No touch release event for AbstractButton inside of  
ListView with pressDelay set  
* QTBUG-81935 Tooltip not closing properly with custom animation if  
open() is called during exit transition.  
* QTBUG-82032 Double click on QML Button is considered as two single  
clicks  
* QTBUG-82463 Dial in automotive example is a bit squished  
* QTBUG-82643  
tst_controls::Default::ToolTip::test_openDuringExitTransitionWithTimeout  
is flaky  
* QTBUG-82020 Displayed text in ComboBox cannot be translated  
* QTBUG-82774 qtquickcontrols2 doesn't build with latest  
qtdeclarative/qtbase dev  
* QTBUG-82811 tst_customization::creation(incomplete:*) tests are  
failing  
* QTBUG-81867 QQC2 SplitView doesn't work if an item is invisible  
* QTBUG-70768 Disabled Slider should be gray (Material Style)  
* QTBUG-73687 When specifying a scale for a Menu it will be positioned  
as if the scale was not set, and therefore can be placed unexpectedly  
* QTBUG-82473 Menu does not take padding properly into account  
* QTBUG-83554 currentValue not updated after model change in ComboBox if  
currentIndex does not change  
* QTBUG-84443 'std::bad_alloc' when  
tst_QQuickApplicationWindow::clearFocusOnDestruction()  
* QTBUG-84381 AddressSanitizer: heap-use-after-free in StackView  
* QTBUG-84579 Popup with parent in StackView centered in overlay causes  
crash at exit  
* QTBUG-78281 QML ComboBox is eliding when it shouldn't  
* QTBUG-86012 qtquickcontrols2 cross compile fails to configure  
* QTBUG-84488 Qml ComboBox list jumps on open  
* QTBUG-85884 When a Dialog is hidden then it is possible that it does  
not reset the focus correctly if when it loses active focus it does the  
process again to hide the dialog  
* QTBUG-85806 Calling swipe.close() on already closed SwipeDelegate  
triggers onClosed  
* QTBUG-85804 SwipeDelegate triggers swipe.closed even when it didn't  
actually close  
* QTBUG-86212  tst_QQuickPopup::setOverlayParentToNull fails in with  
macOS 10.14  
* QTBUG-86280 Crash when importing style without first importing  
Controls  
* QTBUG-86276 QtQuick.Controls 2 Menu does not override other &mnemonic  
key shortcuts  
* QTBUG-85748 Dialog's accepted() signal emitted before closed() when  
using non-zero-duration transitions  
* QTBUG-86263 Gallery example no longer respects the style that was set  
* QTBUG-85719 SpinBox fails to validate the entry after it failed  
already  
* QTBUG-86303 Fallback styles overwrite themes  
* QTBUG-86851 QQC2 Menu contentModel not deleted  
* QTBUG-83698 Using Keys.onReturnPressed from Button to open Menu causes  
the first MenuItem to get triggered on show  
* QTBUG-87848 Cannot run flat style example - missing resources  
* QTBUG-88170 tst_QQuickDrawer::Basic::slider fails after making  
Flickable handle touch events directly  
* QTBUG-88184 property count of SplitView is not documented  
* QTBUG-88141 qdoc warnings in Qt Quick Controls 2 for 6.0  
* QTBUG-88158 Finish 'Porting to Qt 6 - Qt Quick Controls 2' Page  
* QTBUG-88222 Property: Assignment of inherited object regression  
* QTBUG-88362 qtquickcontrols2 dependency update failed on 'dev'  
* QTBUG-87658 QtQuick.Controls version number fails on import  
* QTBUG-88038 FAIL!  :  
tst_QQuickDrawer::Universal::flickable(touch,diagonal)  
'flickable->isDragging()' returned FALSE. ()  
* QTBUG-88463 static build not executing the initialisation code of qml  
plugins  
* QTBUG-88492 QmlComponent: Component is not ready error with static  
compiled Controls 2  
* QTBUG-88955 [REG 5.15.2 -> 6.0.0] Cannot change style of  
quickcontrols2 gallery example using the menu  
* QTBUG-89006 Native style: running controls on Windows with a dpr =  
1.25 has drawing glitches  
* QTBUG-89290 "Target "gallery_controls2" links to target  
"Qt::QuickTemplates2" but the  target was not found" when building  
gallery example  
* QTBUG-87283 REG: Popup position changes after opening once  
* QTBUG-89673 Destroying a modal Dialog with exit transition blocks all  
mouse input to other dialogs  
* QTBUG-88162 Crash when NinePatchImage's source is changed  
* QTBUG-85770 SwipeDelegate resizes incorrectly while it is open  
* QTBUG-89909 tst_controls Dialog tests fail on offscreen platform  
* QTBUG-84426 Tumbler without wrap ignores initial currentIndex  
* QTBUG-90580 tst_QQuickMenu::Material::subMenuDisabledMouse(non-  
cascading) fails on Ubuntu 20.04  
* QTBUG-75042 [Accesssibility] Qt Quick Control 2 Dialog parts (title,  
body, footer) are read in wrong order  
* QTBUG-72757 iOS: Text input cursor moving incorrect with using  
magnifying glass  
* QTBUG-90928 Update dependencies on '6.1' in qt/qtquickcontrols2 failed  
* QTBUG-89956 Documentation for QJSEngine::toScriptValue() and  
QJSEngine::fromScriptValue() doesn't say which types can be converted  
* QTBUG-89955 Ambiguous string comparison in QML Plugin Dumper  
* QTBUG-90038 Crash in QQmlObjectCreator::setupBindings  
* QTBUG-86595 QML uses qPrintable() instead of qUtf8Printable() to  
display errors  
* QTBUG-86482 Missing string conversion in QJSValue parameter in a c++  
signal  connected to QML  
* QTBUG-84906 qt6_qml_type_registration requires automoc  
* QTBUG-91089 qmlplugindump does not dump plain qml files in qmldir and  
needs to be deprecated  
* QTBUG-86946 tst_qqmlpropertycache: derivedGadgetMethod fails if run  
after metaObjectsForRootElements  
* QTBUG-87197 MouseArea containsMouse value incorrect after visibility  
changes  
* QTBUG-40851 Contradiction in Animation and Transitions documentation  
* QTBUG-61021 Autocomplete of editable ComboBox not working on Android  
* QTBUG-91196 Locale QML documetnation lists misspelled property  
* QTBUG-90239 TextField with regex clears text if unmatched char is  
typed  
* QTBUG-85615 qmlRegisterSingletonType (QJSValue) only works for Objects  
* QTBUG-86669 Investigate automatic calling of qt6_import_qml_plugins  
for examples using a static Qt build  
* QTBUG-90632 Particles are causing unnecessary batch uploads  
* QTBUG-88643 tst_QQmlImport::importPathOrder() failed on msvc2019  
developer build in CI  
* QTBUG-84060 qmllint: warning when accessing JS array declared as a var  
* QTBUG-91519 [REG 5.14.2 -> 5.15.0] Call QQmlIncubator::clear() inside  
QQmlIncubator::setInitialState() crashes afterward  
* QTBUG-83980 HoverHandler: sometimes point.position returns (0, 0)  
* QTBUG-90362 The first character in text input fields appears last on  
Android 10/11  
* QTBUG-91491 Crash in Generator::method_next when creating new  
properties on Generator  
* QTBUG-91694 Colors comparison with QML fuzzyCompare() always results  
in 'equal'  
* QTBUG-91717 QJSPrimitiveValue must not use std::variant  
* QTBUG-91727 qt6_target_enable_qmllint() never adds -I flags for import  
path  
* QTBUG-83762 qmllint: Warning: Property "T" not found on type  
"Rectangle" [...]  
* QTBUG-85107 qml runtime tool have no option to share opengl context  
* QTBUG-91182 Atlas textures with size not greater than  
QSG_ATLAS_TRANSIENT_IMAGE_THRESHOLD are not visible with ShaderEffect  
* QTBUG-87018 Touch/mouse-related test failures in qtquickcontrols2  
* QTBUG-92076 TableView: forceLayout() fails when all columns are hidden  
* QTBUG-91989 Default theme in Gallery on Windows is 'Basic' (expecting  
the 'Windows')  
* QTBUG-92064 PinchHandler target scale jumps when pinching a second  
time via native gesture  
* QTBUG-92165 REG 5.15->6.0: when PinchHandler and DragHandler are used  
together, trackpad pinch gesture causes a jump  
* QTBUG-92000 tst_qquickitem::hoverEvent is flaky on Ubuntu 20.04  
* QTBUG-92099 TableView: content height doesn't change when adding new  
rows  
* QTBUG-92078 qmleasing uses removed API  
* QTBUG-92207 Qmllint does not warn about use of deprecated property in  
binding  
* QTBUG-92026 qt6_qml_type_registration() generates CMP0116 warnings  
with CMake 3.20  
* QTBUG-87236 NinePatchImage causes crash due to repeated presses.  
* QTBUG-75556 Selection in TextEdit not working for Readonly text  
* QTBUG-91143 QML inline components cannot reference alias properties  
* QTBUG-92447 [Reg 5.15 -> 6.0] qmllint: Property "length" not found on  
type "QString"  
* QTBUG-92236 When the cache for a QML file is generated and then loaded  
it will cause a crash  
* QTBUG-92562 qtdeclarative build error on x86-windows  
* QTBUG-91749 Incorrect batching using overlapping QSGGeometry with  
lines having a width > 1  
* QTBUG-92449 qmllint: "unused import" lint don't care about "required"  
types  
* QTBUG-92571 qmllint: Cannot assign to default property of incompatible  
type  
* QTBUG-92566 builtins.qmltypes: double is not real?  
* QTBUG-92372 QtQuick's qmltypes misses signals  
* QTBUG-89736 focusable item becomes impossible to focus after  
reparenting to a newly loaded item  
* QTBUG-91867 TextInput cursorDelegate position not updated after left  
padding change  
* QTBUG-84895 QML annotations should be actively supported in tooling  
* QTBUG-92966 MSVC compiler warning C4267 in qqmlirbuilder.cpp  
* QTBUG-92883 [qt6] duplicate symbols in mac style plugin  
* QTBUG-93039 Crash when scrolling ScrollView with zero-sized item  
* QTBUG-93048 Signal and Handler Event System   demo Grammatical errors  
* QTBUG-93027 states + PropertyChanges = qmllint no property exists in  
the current element  
* QTBUG-93172 Duplicate symbol qInitResources_qmake_immediate when  
building qtquickcontrols2 gallery example against static macOS Qt  
* QTBUG-88220 Add documentation pages for the new native styles  
* QTBUG-93189 qmllint does not handle Behavior correctly  
* QTBUG-93241 qmllint plus mysterious window  
* QTBUG-93231 qmllint: unknown attached property scope ScrollBar  
* QTBUG-92214 QML Dial with stepsize set gives unexpected result  
* QTBUG-93083 setSceneGraphBackend(const QString &backend): where is the  
list of possible strings?  
* QTBUG-93404 QML Debugging : Breakpoints' internal ID is not assigned  
properly  
* QTBUG-93430 macOS: sliders should not get focus from clicking on them  
* QTBUG-92224 Show let type variable in Locals  
* QTBUG-63673 PinchArea uses wrong coordinate system when inside a  
rotated container item  
* QTBUG-91549 WheelHandler enables itself although deactivated  
* QTBUG-93423 macOS: slider handle focus ring is too big  
* QTBUG-91783 Gadget object returned from property is not modified  
* QTBUG-91924 With the Imagine style then it is possible that the  
background of a GroupBox is clipped by two pixels  
* QTBUG-93175  tst_EcmaScriptTests::runInterpreted fails with Windows 10  
developer build  
* QTBUG-85861 When passing a QList of enum values to QML then they are  
passed as objects  
* QTBUG-93264 TableView: first column does not unhide when changing  
column width  
* QTBUG-74572 When using a syntax highligher on the QQuickTextDocument,  
then triggering a rehighlight does not automatically update the text  
control using it  
* QTBUG-93436 ASTC images are mirrored  
* QTBUG-69577 while using both qml and JavaScriptCore.framwork, iOS app  
got a non-public api references error  
* QTBUG-93563 [REG] qmake: Cannot locate rcc when using Qt Quick  
Compiler  
* QTBUG-76136 Slider always snaps if stepSize is set regardless which  
snapMode is used  
* QTBUG-93480 tst_qquickuniversalstyle::Universal::test_inheritance  
failed  
* QTBUG-83630 Qt Quick Control 2 Tooltip can be way too big when you  
have newlines  
* QTBUG-91716 TapHandler works only in the upper left corner of the  
screen when QQuickView given another window as parent  
* QTBUG-92158 [REG 5->6]QML Customised scrollbar has incorrect size and  
scrolling behaviour  
* QTBUG-92466 Recommend that instead of passing a QTime directly from  
C++ to QML, that it is passed as a QDateTime instead so that the  
timezone can be explicitly set to UTC to avoid any problems with  
conversion  
* QTBUG-89126 REG: ScrollView doesn't remove ScrollBar after settinging  
the new one  
* QTBUG-92839 QQuickRenderControl D3D11 should be made working with  
MinGW too  
* QTBUG-93886 PinchHandler's centroid.velocity is wrong (regression  
5.15->6.0)  
* QTBUG-79163 DragHandler steals events from a MouseArea with  
preventStealing = true  
* QTBUG-93958 Crash with ScrollView + TextArea + Item when the app is  
closing  
* QTBUG-91227 Layout is always RTL when locale is RTL  
* QTBUG-93807 Forced 'checkable' property of ItemDelegate interferes  
with editable models  
* QTBUG-94022 Visiting FolderListModel's Qt 6 documentation results in  
404  
* QTBUG-94005 dynamically-created pointer handlers aren't added to  
Item.resources property  
* QTBUG-93994 QML ComboBox hide error  
* QTBUG-93880 MultiPointHandlers (DragHandler, PinchHandler) don't emit  
the grabChanged signal  
* QTBUG-93959 Qt Quick should request Vulkan API 1.1 on the VkInstance,  
when available  
* QTBUG-94067 Runtime error in qv4stackframe  
* QTBUG-93746 There's no PlaceholderText property in ColorGroup  
* QTBUG-92944 input problems in DynamicTexture example  
* QTBUG-67290 Accessibility is broken when using QQuickWidget  
* QTBUG-94099 qmltyperegistrar doesn't explicitly export the  
qml_register_types_...() function  
* QTBUG-93857 Mac Link Accessibility, Link cannot be triggered by  
VoiceOver  
* QTBUG-94180 Update dependencies on 'dev' in qt/qtquickcontrols2  
* QTBUG-93652 qmllint: Missing support for inline components  
* QTBUG-93752 When setting the inactive colorgroup in the palette and  
then making the window inactive it will not trigger an update on any  
colors bound to the palette  
* QTBUG-93489 Not obvious how to generate key events for QML when using  
QQuickRenderControl  
* QTBUG-64128 When dragging an item that is the parent of the DropArea  
then it will call onEntered for that DropArea  
* QTBUG-94533 Update dependencies on '6.2' in qt/qtquickcontrols2 fails  
* QTBUG-94519 Install rules for .qml files should use source dir as  
their source, not build dir copies  
* QTBUG-94553 Update dependencies on '6.2' in qt/qtquickcontrols2 fails  
* QTBUG-94559 Update dependencies on '6.2' in qt/qtquickcontrols2 fails  
* QTBUG-91365 Can't set palette for Window  
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
* QTBUG-93041 If Button is used as delegate of ListView then application  
fails  
* QTBUG-91390 ListModel doesn't keep objects of JavaScriptOwnership  
alive  
* QTBUG-94833 Wayland compositor crash when client window closes  
* QTBUG-94703 REG: Binding to var properties that are undefined is  
broken in 6.2.0  
* QTBUG-55958 QQuickItem::contains return true even for points outside  
the item rect  
* QTBUG-89376 QQuickItem API that involves item-at/bounds checks doesn't  
respect containmentMask  
* QTBUG-34882 Multiple hovers are incorrect when children are outside  
parent  
* QTBUG-94455 tst_QQuickFileDialogImpl::defaults() leaks memory  
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
* QTBUG-89375 No C++ documentation for containmentMask  
* QTBUG-72843 HoverHandler is unreliable  
* QTBUG-95162 Qt config with some modules disabled causes compile error  
(Qt 6.2.0 beta1)  
* QTBUG-94622 svg Image is  Pixelated when windows is scaled  
* QTBUG-95139 Using backticks for ListElement value results in "cannot  
use script for property value"  
* QTBUG-81037 Array.concat does not verify length against allocated  
space  
* QTBUG-95132 Memory Leak when using QQuickPaintedItem with RHI  
* QTBUG-95365 QML module files copied to build dir have nothing  
depending on them  
* QTBUG-95417 Regression 5.15.4: gc() within generator functions crash  
* QTBUG-95095 Inline QML component can't use named import of JavaScript  
module from enclosing scope  
* QTBUG-95532 Can't build qtquickcalendar due to missing SQL dependency  
* QTBUG-91165 QtQuick compiler and QML States/AnchorChanges at loading  
prevents component to be displayed  
* QTBUG-95622 SelectionRectangle: selection is removed when dragging on  
the bottom-right handle  
* QTBUG-95575 Build fails with clang-cl 12.0.0  
* QTBUG-95314 WASM: Diverging timezones in C++/QML  
* QTBUG-95591 QtQuick documentation references private class  
"QQuickColorGroup"  
* QTBUG-94964 Create QtQuick.Dialogs module overview page  
* QTBUG-95656 qmllint does not handle implicit import correctly  
* QTBUG-94558 The handle hovered state of RangeSlider is wrong when  
first and second overlapped  
* QTBUG-95811 KeyNavigation: all properties should be marked as attached  
* QTBUG-95393 QQuickView::grab segfaults at times  
* QTBUG-95259 After closing modal menu, non-modal menus can't be  
dismissed by clicking  
* QTBUG-95825 Live preview not starting  
* QTBUG-95659 Assertion error by accessing this from onSignal arrow  
function  
* QTBUG-85591 qmlProtectModule() claims it "allows the engine to skip  
checking for a plugin when that uri is imported", but that might not be  
true  
* QTBUG-95593 Customised SpinBox buttons don't work with macOS style  
* QTBUG-89409 Unable to scroll listview by dragging / swiping if header  
is used  
* QTBUG-95461 QQuickTextInput doesn't manage pre-edit text correctly  
* QTBUG-95937 Native windows style is incompatible with QQuickWidget or  
other means of offscreen rendering  
* QTBUG-94456 Alias properties incorrectly allow duplicating property  
names  
* QTBUG-95944 ButtonGroup.buttons is not a default property as it claims  
to be  
* QTBUG-92840 FolderListModel docs have gone missing  
* QTBUG-95895 REG 5.15 -> 6.2: destroy() does not destroy objects after  
appending listModel.  
* QTBUG-95562 Warnings about deprecated usage  
* QDS-4390 Live preview crashes at shutdown  
* QTBUG-96126 Compositor crashes when client is closed  
* QTBUG-96118 FTBFS top-level: The "moc" executable  
"BUÏLDDIR/qtbase/libexec/moc" does not exist.  
* QTBUG-96167 Ownership of C++ owned object flips when added to  
ListModel  
* QTBUG-96150 QML best practices docs are outdated  
* QTBUG-96190 Rendering glitches when resizing window containing  
QQuickPaintedItem  
* QTBUG-96099 Drag and Drop example crashes on KDE Plasma  
* QTBUG-88414 CMake multi-config build still build some debug tools  
* QTBUG-93050 Memory leak in qiconhelper.cpp when loading icon by name  
* QTBUG-64847 TapHandler does not tell us which button was tapped (and  
this breaks the manual test)  
* QTBUG-96301 qmldir files generated by CMake do not respect .ui.qml  
suffix  
* QTBUG-47963 TextField auto tests fail  
* QTBUG-47317 StackView: pushed items still show up after being popped  
* QTBUG-47949 StackView: transitions are broken  
* QTBUG-47318 ApplicationWindow: item within a StackView that fills the  
window doesn't get correct initial size  
* QTBUG-48086 SwipeView: can't set initial currentIndex  
* QTBUG-48072 ApplicationWindow doesn't respect its maximumWidth/Height  
* QTBUG-47754 Duplicate "count" property in documentation for Tumbler in  
QtQuick.Controls 2  
* QTBUG-48624 TabBar reset current index to -1 on completion  
* QTBUG-48651 Crash in theme code when loading engines in succession  
* QTBUG-48721 tst_pageindicator warnings  
* QTBUG-48808 'make qmltypes' fails  
* QTBUG-48993 TabBar set wrong width for tabs dynamically created by  
Repeater  
* QTBUG-48718 Mis-aligned text in tabs  
* QTBUG-48989 SpinBox always converts value in contentItem as int  
* QTBUG-48720 Stack before/after warnings in auto tests  
* QTBUG-49338 tst_applicationwindow crash  
* QTBUG-49361 Test qtquickcontrols2\tests\auto\accessibility frequently  
fails on Windows  
* QTBUG-49551 Material Button highlighted state  
* QTBUG-49468 Missing baseline offsets  
* QTBUG-49891 Use qputenv instead of (not existing) qsetenv in  
outcommented code  
* QTBUG-49924 ComboBox produces warning about incorrect sRGB profile  
with default style  
* QTBUG-50018 ToolButton can't be highlighted  
* QTBUG-50008 Button: disabled state is not visualized clearly enough  
* QTCREATORBUG-15137 metainfo file for Qt.labs.controls 1.0 doesn't work  
while in Qt Creator 3.5.0  
* QTBUG-49941 Qt5.6 offline: qtlabscontrols (qtquickcontrols2) examples  
missing  
* QTBUG-50048 Build fails on ARM with -qreal float in qtquickcontrols2  
* QTBUG-50045 Drawer is too eager to steal touch  
* QTBUG-50033 SpinBox nearly unusable on touch-based devices  
* QTBUG-50143 ComboBox display empty  when model is  ListModel  
* QTBUG-50025 Toolbar or ApplicationWindow header/footer transparent in  
Material style  
* QTBUG-49958 Stretched Dial  
* QTBUG-50274 StackView: replacing of the topmost item clears the whole  
stack  
* QTBUG-50203 Menu object doesn't have a title property  
* QTBUG-50332 ToolBar switch crashes in  
QQmlJavaScriptExpression::hasError()  
* QTBUG-50347 Material style: checkable MenuItem doesn't use user  
defined accent color  
* QTBUG-50404 [Universal Style] Can't use SwipeView in conjunction with  
ComboBox or TextArea  
* QTBUG-50385 ComboBox crashes on click after model change in  
QQuickListViewPrivate::lastPosition()  
* QTBUG-50470 Universal Style: ComboBox and ListView don't use user  
defined accent color  
* QTBUG-50412 TextArea placeholder text does not disappear on Android  
until word is committed  
* QTBUG-50329 Material: primary color is missing  
* QTBUG-50330 Material: wrong toolbar color  
* QTBUG-50327 Default style Button & TextField look too similar  
* QTBUG-50577 Using scrollwheel on a (modal) Popup moves application  
content  
* QTBUG-50305 StackView: push new item over double-clicked item breaks  
mouse events  
* QTBUG-50141 ComboBox does not support object array  
* QTBUG-50161 ProgressBar and BusyIndicator are very CPU intensive  
* QTBUG-50043 Tab position  
* QTBUG-50757 ComboBox has no scrollbar for menu  
* QTBUG-49961 Partially checked CheckBox  
* QTBUG-49921 Popups don't work without ApplicationWindow  
* QTBUG-50815 Flickable clips too much content of a Quick Control 2  
Label on iOS  
* QTBUG-50575 Using ComboBox makes SwipeView animation unsmooth  
* QTBUG-50933 Review Qt Labs Controls doc  
* QTBUG-50972 Range Slider qt.labs.controls not usable (Material,  
Universal)  
* QTBUG-50971 Text too small (material design) qt.labs.controls Gallery  
* QTBUG-50937 Error when accessing StackView attached properties via  
popped item  
* QTBUG-51114 SpinBox resets to "from" value when loses focus  
* QTBUG-51118 ComboBox doesn't show/select currentIndex  
* QTBUG-50295 tst_activeFocusOnTab crashes randomly on Ubuntu 14.04  
* QTBUG-51278 QQC2: plugins.qmltypes is quite outdated, please  
regenerate  
* QTBUG-51257 Material: Controls that don't have focused highlight  
(there is no difference between normal & focused states)  
* QTBUG-51108 Invalid month index returned by model  
* QTBUG-51312 [REG Qt 5.6.0 Beta -> Qt 5.6.0 RC] ProgressBar  
indeterminate property results in a displaced progress bar with Material  
style  
* QTBUG-50220 SpinBox can't be inc/dec using mouse wheel  
* QTBUG-50221 Slider can't be inc/dec using mouse wheel  
* QTBUG-51322 Popup doesn't respect height  
* QTBUG-51316 Windows: Accessibility warnings from Labs controls gallery  
example  
* QTBUG-41432 Hard to choose the right text rendering type  
* QTBUG-51645 QQC2: Combobox reacts strangely on return key pressed  
* QTBUG-51078 Use of Item obligatory in SwipeView?  
* QTBUG-51708 Static builds fail  
* QTBUG-51616 Complete documentation Control QML Type  
* QTBUG-51916 Background color does not change if closing one popup and  
opening another in javascript  
* QTBUG-51918 qtgamepad examples have broken install targets  
* QTBUG-51990 Popup margins are ignored or broken  
* QTBUG-51991 ApplicationWindow attached property not available in Popup  
* QTBUG-51989 Popup cannot be created with enabled visible property  
* QTBUG-52003 Velocity-related tests in tst_swipedelegate and tst_drawer  
are unstable  
* QTBUG-50993 The default style doesn't have focused highlight  
* QTBUG-51972 Qt Controls 2.0: ComboBox doesn't load properly with async  
set to true  
* QTBUG-52233 ScrollBar behaves weirdly with certain paddings  
* QTBUG-52156 ToolTip typo  
* QTBUG-51796 Controls focus handling is not consistent when using a  
mouse  
* QTBUG-52448 QQuickAbstractButton: clicked() called before  
nextCheckState()  
* QTBUG-52358 ButtonGroup doesn't work with a Repeater that's within a  
Column  
* QTBUG-52146 ButtonGroup's "current" property documentation disagrees  
with code  
* QTBUG-52615 [REG] StackView.initialitem is not equivalent to push() in  
Component.onCompleted  
* QTBUG-51254 Material: SpinBox doesn't respect the minimum touch target  
size  
* QTBUG-52631 Material: changing primary/accent colors doesn't update  
dependent colors in popup and it's children  
* QTBUG-52730 QQC2: There is no way to turn off the Drawer touch support  
* QTBUG-52738 Input text not visible with Universal's dark theme  
* QTBUG-52919 Wrong link on page: Material Style documentation  
* QTBUG-52608 Popup cannot properly reposition from right and bottom  
window borders  
* QTBUG-52979 Regression: Material combobox menu cannot be scrolled  
* QTBUG-51677 QQC2: TextArea can't be used to show long very long texts  
* QTBUG-51785 Need a "HOWTO create/include/build/maintain your  
qt56controls style"  
* QTBUG-52731 tst_material keeps crashing in the CI (win 10)  
* QTBUG-49371 signal implicitWidthChanged() from QQuickTextEdit  
redefined in QQuickTextArea  
* QTBUG-53061 Regression: First item in Tumbler disapperas  
* QTBUG-53066 Regression: After Popup open, drawer shadowed by an  
overlay  
* QTBUG-53157  tst_accessibility fails in Ubuntu 16.04  
* QTBUG-52558 Behavioral incompatibility between QQuick* checkables and  
QWidget/Quick.Controls checkables  
* QTBUG-53208 Statically compiled QQC2 and QQC1 cannot find plugins  
* QTBUG-53120 Tumbler's displacement is incorrect when model has 2 items  
* QTBUG-53203 Style-specific file selectors fail if the first letter  
isn't uppercased  
* QTBUG-53274 QQuickMenu does not add menu item signal handlers when  
adding item via addItem()  
* QTBUG-53275 Popups should restore focus to the contentItem of  
ApplicationWindow upon closing  
* QTBUG-53262 overlapping text (Popup - Menu - MenuItem)  
* QTBUG-53309 Setting dim to false on a modal Popup doesn't work  
* QTBUG-52953 Examples are not  installed in the correct directory  
* QTBUG-53348 Material Button missing checked state visuals  
* QTBUG-53350 Default Button colors  
* QTBUG-52729 Popup resizes to improper height on window size change  
* QTBUG-53067 After replacing out item from StackView it has wrong  
dimensions on orientation change  
* QTBUG-53377 Theme font ignored in QQC2 due to not exact match  
* QTBUG-53420 Non-modal popups shouldn't affect focus  
* QTBUG-53519 API review findings to be fixed before the release  
* QTBUG-53556 tst_material fails on numerous locations  
* QTCREATORBUG-16371 Qt Quick Designer does not work for a newly created  
Qt Quick Controls 2 application  
* QTBUG-33179 QML revisioning does not work for grouped properties  
* QTBUG-53846 Slider is not set if only clicked  
* QTBUG-51527 Material: ScrollBar doesn't respect the minimum touch  
target size  
* QTBUG-54140 Improper use of stepSize property (probably off-by-1 bug  
in step division)  
* QTBUG-54173 Document the equivalent of MenuBar  
* QTBUG-54207 Material SpinBox label doesn't respect enabled state  
* QTBUG-54573 ComboBox popup listview draws overlapping text when model  
changes  
* QTBUG-54578 Hidden Drawer visible in window after increasing window  
size if docked at right or bottom edge  
* QTBUG-54648 SwipeDelegate: clicked() and released() never emitted for  
button delegates  
* QTBUG-53929 Button press in ListView is canceled after moving a tiny  
bit  
* QTBUG-54615 Double-clicking text in a TextArea selects the whole  
paragraph  
* QTBUG-54629 Drawer can not disabled with dragMargin  
* QTBUG-54658 SwipeDelegate not always emits swipe.complete  
* QTBUG-54660 SwipeDelegate Layouting problem if orientation changes  
* QTBUG-54764 Material: Buttons (and the other controls) have no ripple  
effect  
* QTBUG-54780 SwipeDelegate's contentItem is not resized automatically  
when the control's height changes  
* QTBUG-54552 Settings (Qt.labs.settings) cannot be used inside  
Component  
* QTBUG-53419 hovered property is true even when under a popup  
* QTBUG-54897 TextArea in Flickable handles mouse input outside  
flickable area making elements underneath unusable  
* QTBUG-55040 SwipeDelegate does not swiping out contentItem if anchored  
to parent  
* QTBUG-54269 Material colors don't work as documented  
* QTBUG-55174 Doc: SwipeDelegate missing from "Delegate Controls"  
* QTBUG-55143 ApplicationWindow contents is not relayouted when  
header.visibility or footer.visibility changes  
* QTBUG-55118 ComboBox text errors after modifications of underlying  
list model  
* QTBUG-54935 Material style ComboBox has white text (on a white  
background) when put in a ToolBar  
* QTBUG-55179 tst_controls::Tumbler::test_displacementListView() fails  
on Red Hat 4.9.1-10  
* QTBUG-55004 ComboBox into Dialog doesn't show value list on Android  
* QTBUG-54472 BusyIndicator in material style goes nuts when scrolling  
through ListView  
* QTBUG-55015 RangeSlider stepSize does not properly take into account  
"from"  
* QTBUG-55228 Dial's stepSize handling is broken  
* QTBUG-55129 TabButton always squeezed to fit in TabBar  
* QTBUG-54917 Material style ToolButton's checked state is only visible  
when hovered  
* QTBUG-55050 ComboBox popup does not exploit available space  
* QTBUG-55347 QtQuick Controls 2 ToolTip crashes when previous parent  
Item is destroyed before new ToolTip is displayed  
* QTBUG-55366 Specifying foreground and background in  
qtquickcontrols2.conf has no effect  
* QTBUG-54995 TextInput crashes qml2puppet if QtQuick Controls 2 are  
imported  
* QTBUG-55620 ScrollIndicator overshoot doesn't respect paddings  
* QTBUG-54797 Property dim doesn't work properly on Windows  
* QTBUG-55647 Switch is not focused by mouse clicking on indicator.  
* QTBUG-55405 StackView: destroyOnPop functionality needs to be restored  
* QTBUG-55684 TextField size must be explicitly set when customizing the  
background property  
* QTBUG-55729 Popups don't close on touch events without  
ApplicationWindow  
* QTBUG-54913 hovered property is true even when under a popup in a  
Window  
* QTBUG-55687 Some Material controls do not respect Material.background  
* QTBUG-54794 Drawer bad behavior after close a popup menu  
* QTBUG-50992 QQC2: Object destroyed during incubation  
* QTBUG-55769 Modal popups and drawers leak wheel events through  
* QTBUG-55995 Drawer flickers on release when closing  
* QTBUG-56007 MenuItem press/hover state remains after selecting an item  
and reopening the menu  
* QTBUG-56010 Drawer: cannot drag to close from the outside on touch  
* QTBUG-56025 Popup does not respect explicit size  
* QTBUG-55686 SwitchDelegate's handle is not draggable  
* QTBUG-53168 Drawer has wrong height and position if ApplicationWindow  
or page has header/footer  
* QTBUG-55360 QtQuick.Controls Drawer component ignores "y" parametr  
* QTBUG-56131 Other popups do not close after closing a drawer  
* QTBUG-56136 A modeless popup inside a modal popup doesn't close when  
clicking the background of the modal popup  
* QTBUG-56158 Crash in StackView::pop()  
* QTBUG-54347 Runtime error when used custom popup based on QQuickPopup  
from Quick Controls 2  
* QTBUG-56215 If the SpinBox is not editable, valueFromText should never  
be called  
* QTBUG-56243 Crash when showing tooltip in an ApplicationWindow via  
attached show() function  
* QTBUG-56265 TabBar: cannot mix fixed and implicitly resized tabs  
* QTBUG-55520 Material ripple effect must be activated on press not on  
release  
* QTBUG-54206 Material ToolTip quickly disappears when hovering from one  
control to another  
* QTBUG-56297 Cannot override popup.contentItem on ComboBox  
* QTBUG-53266 Material Popup color wrong on dark theme  
* QTBUG-55572 Child ToolTip ignores delay and timeout properties  
* QTBUG-55749 StackView (Controls 2.0) doesn't work with http url on  
first try  
* QTBUG-56556 Button stays hovered while pressed  
* QTBUG-55652 Material style ToolButton's ripple/hover effect breaks  
when text is cleared on click  
* QTBUG-56709 Page doesn't calculate implicit size  
* QTBUG-56697 [REG 5.7.0 -> 5.7.1] Popups don't close on click outside  
* QTBUG-56698 Default style: disabled controls nearly impossible to see  
* QTBUG-56562 Shortcut does not play well with Qt Quick Controls 2  
popups  
* QTBUG-56755 Popup: binding loops with size-dependent positioning  
* QTBUG-56884 ComboBox missing home/end & key search  
* QTBUG-56061 tst_Drawer::touch() fails  
* QTBUG-57167 ComboBox: binding loop for Material.foreground  
* QTBUG-57069 QQC2 Slider's documentation should say "ratio", not  
"percentage"  
* QTBUG-57085 autorepeat stops in SpinBox stops when mouse or touch  
moved  
* QTBUG-57243 SwipeDelegate: calling swipe.close() breaks the internal  
state  
* QTBUG-57258 tst_controls::Default::ToolTip::test_makeVisibleWhileExitT  
ransitionRunning fails occasionally  
* QTBUG-56312 SwipeDelegate does not lose focus if  
Flickable.StopAtBounds  
* QTBUG-57297 Build fails with incomplete type QColor  
* QTBUG-57271 Beginning a swipe over a Label in SwipeDelegate's right  
item causes wrong item to be exposed  
* QTBUG-57350 SwipeDelegate: animations gone missing  
* QTBUG-57266 StackView: pushing the already topmost item visually  
clears the stack  
* QTBUG-57256 ComboBox::test_modelReset() fails occasionally in the CI  
* QTBUG-57242 SwipeDelegate::position value jumps abruptly  
* QTBUG-57618 Qt Quick Controls crash on Android 6 and 7  
* QTBUG-57800 Android: Qt Quick Controls 2 Combobox  background arrow is  
much bigger than it should be  
* QTBUG-57858 Hang due to infinite loop when removing tabs from TabBar  
* QTBUG-55999 TextField's placeholder is aligned to right while it is a  
LTR text  
* QTBUG-57944 [REG 5.7.1->5.8.0 RC] Switch control released at middle  
state it stays there  
* QTBUG-58217 SpinBox: when range is changed the buttons won't get  
enabled/disabled accordingly  
* QTBUG-58343 Description of PageIndicator is incorrect  
* QTBUG-57846 Using fastblur and crashing when closing  
* QTBUG-58810 Menu uses a wrong cursor shape.  
* QTBUG-59026 Qt Quick Materials Controls crash on Android  
* QTBUG-59034 tst_controls::Default::StackView crashes  
* QTBUG-59098 StackView Blocking UngrabMouse  
* QTBUG-58828 Unwanted animation when toggling Material controls between  
various states  
* QTBUG-58932 ApplicationWindow documentation contains contentData  
property which does not exist  
* QTBUG-59233 Update Button's GIF in the documentation  
* QTBUG-58060 Wrong dialog buttons order with Material  
* QTBUG-59536  
tst_controls::Default::SwipeDelegate::test_horizontalAnchors() failed  
* QTBUG-57650 "SignalSpy.qml:253: TypeError: Cannot read property of  
null" when running Controls 2 auto tests  
* QTBUG-59661 Incorrect binding for implicitHeight in Popup  
* QTBUG-59532 Crash in QQmlDebugService  
* QTBUG-59634 StackView replace SIGSEGV  
* QTBUG-58606 tst_Snippets::screenshots tests fail occasionally  
* QTBUG-59911 Material BusyIndicator is invisible  
* QTBUG-59629 Scrollbar has no implicit setted cursor  
* QTBUG-59309 StackView resolves relative path is incorrect.  
* QTBUG-59920 Sliders and Dials do not immediately move when dragged  
* QTBUG-58105 [Android] Back key terminates QtQuickControls2 gallery  
example  
* QTBUG-58667 Set position of Scrollbar at mousePressEvent  
* QTBUG-59746 Performance regression for Button creation benchmark  
* QTBUG-58925 QQC2: Combobox *checked* image is weird on Android  
emulator  
* QTBUG-60200 QPainter warnings when running Gallery example with  
Material style  
* QTBUG-60356 Editable SpinBox's text input doesn't have focus when the  
SpinBox is focused  
* QTBUG-60405 Presses and releases leak through modal Menu  
* QTBUG-60358 Popup's modal documentation is too brief  
* QTBUG-58797 Material TextField / TextArea: cursorVisible ignores  
readOnly state  
* QTBUG-60493 Gallery drawer flickers when opening for the first time  
* QTBUG-60521 Drawer interferes with flicking on touch  
* QTBUG-60528 Changing IconImage's iconColor also affects its size  
* QTBUG-60598 [REG] Drawer: can't close by dragging over the drawer on  
touch  
* QTBUG-60602 [REG] Popup shadow leaks events through on touch  
* QTBUG-60807 Icon not colourised after becoming enabled  
* QTBUG-60893 Assigning screens in ApplicationWindow possible only AFTER  
they have been created  
* QTBUG-59423 Dialog reacts only to the accepting and rejecting roles of  
the standard buttons  
* QTBUG-58646 Artifacts in the Material style ItemDelegate  
* QTBUG-61109 [Reg 5.8 -> 5.9 RC] Qt Quick Controls 2: Page content  
whith anchor.fill: parent can appear below header and footer  
* QTBUG-60684 Empty dropdown list shown on ComboBox after clear  
* QTBUG-61225 Many ComboBox auto tests are flaky  
* QTBUG-60973 Qt5.9.0 macOS: Qtquickcontrols2 gallery app has extra  
items on drop-down menu  
* QTBUG-61144 Taps don't occur for Buttons in ListView with pressDelay  
set  
* QTBUG-61114 Changing font properties of tooltip breaks font  
* QTBUG-60995 Qt Quick Controls 2 help has misplaced images and text  
* QTCREATORBUG-18321 ButtonGroup is marked as Unknown Component. (M300),  
but code runs fine  
* QTBUG-61310 Container crashes with Repeater  
* QTBUG-61426 SpinBox press and hold + or - does not trigger  
valueModified  
* QTBUG-61336 ApplicationWindow can't be used with  
QQuickView/QQuickWidget  
* QTBUG-61585 Qt 5.9 MonthGrid gets no clicked signal on touch  
* QTBUG-61535 tst_calendar::MonthGrid::test_locale  
* QTBUG-60492 ToolTip blocks Shortcut  
* QTBUG-61647 Incorrect description for RangeSlider first & second  
values  
* QTBUG-61608 Default value of Menu's closePolicy differs from the  
description in docs and conflicts with onPressAndHold events  
* QTBUG-61785 Non-interactive controls are blocking touch  
* QTBUG-61698 Modal Overlay don't block multi touch  
* QTBUG-61374 "TypeError: Cannot read property 'text' of null" with  
Tumbler.currentItem  
* QTBUG-61843 Assertion failure when setting incorrect edge value on  
Drawer  
* QTBUG-61581 QtQuickControls2 Drawer doesn't close if tapped outside  
* QTBUG-61950 Regression: unused parameter warnings in  
qwidgetplatform_p.h under some build configurations  
* QTBUG-62153 StackView.Immediate transition leads to crash when used in  
StackView.onRemoved  
* QTBUG-62158 [QQC2] orientation change breaks the position and size of  
the Popup  
* QTBUG-62241 tst_switch fails  
* QTBUG-62363 tst_qquickmenubar::mouse() fails for all styles on Ubuntu  
16.04 CI machines  
* QTBUG-62289 Compilation error in qtquickcontrols2 (during qt5.git  
integration in 'dev')  
* QTBUG-62383 tst_menu::mouse fails on Ubuntu 16.04 CI machine  
* QTBUG-62412 SwipeDelegate tests fail  
* QTBUG-62549 tst_controls::Default::Dialog::test_reject() fails during  
qt5.git integration in 'dev'  
* QTBUG-62628 tst_Drawer::multiple() fails during qt5.git integration in  
'dev'  
* QTBUG-62292 [Windows] Crash with ScrollView + TextArea  
* QTBUG-62508 SpinBox value can be outside of from-to range  
* QTBUG-62926 Crash in qtquickcontrols2 tests during qt5.git integration  
in 'dev'  
* QTBUG-59652 Non-modal Drawer does not drag/swipe open  
* QTBUG-63037 tst_controls::Material::UnknownTestFunc() fails during  
qt5.git integration in '5.10'  
* QTBUG-63119 windowText palette colour role not inherited by controls  
within ListView  
* QTBUG-61135 Attached Keys signal handlers don't work for an editable  
ComboBox  
* QTBUG-63149 module "QtQuick.Controls.Fusion" version 2.3 is not  
installed  
* QTBUG-62854 QuickControls 2 TextField and TextArea background styling  
problem when disabled  
* QTBUG-62946 Crash in ButtonGroup when removing items from a model  
using beginRemoveRows()/endRemoveRows()  
* QTBUG-62325 QML ScrollView + TextArea causes binding loop  
* QTBUG-60480 tst_controls::Default::ComboBox::test_mouse() fails  
occasionally in the CI  
* QTBUG-63674 Qt Quick Controls 2 ActionGroup is not working  
* QTBUG-63618 No customisation documentation for GroupBox's title  
* QTBUG-63672 Modal popup causes crash when used in StackView  
* QTBUG-63626 'Environment variable 'PWD' undefined' error for QtQuick:  
Controls docs build on Windows  
* QTBUG-63644 QML ToolTip impossible to rely on  
* QTBUG-63898 DialogButtonBox leads to segfault when being styled  
* QTBUG-63895 5.10: Broken image links in QQC2 imagine style  
documentation  
* QTBUG-62668 tst_popup:xxx tests fail during qt5.git integration in  
'dev'  
* QTBUG-63959 QQC2 ItemDelegate icon source crashes with custom image  
provider  
* QTBUG-64075 Arguments in QQuickSpinbox swapped  
* QTBUG-63238 Add ability provide next state for tristate CheckBox  
* QTBUG-64048 TextField clears text selection on mouse right click  
* QTBUG-64065 The error in Slider.Value with stepSize and "snapMode:  
Slider.SnapAlways"  
* QTBUG-56557 ScrollBar handle minimum length  
* QTBUG-64259 Qt.labs.platform SystemTrayIcon activated signal missing  
reason argument  
* QTBUG-64430 [REG 5.10] gallery (delegates) shows wrong checkboxes in  
default style  
* QTBUG-64492 [REG 5.10] Button's text is no-longer center-aligned  
* QTBUG-64548 Shortcut doesn't work in QQuickWidget  
* QTBUG-64761 qtquickcontrols2/examples/quickcontrols2/flatstyle  
configure/compile failure with disabled widgets module  
* QTBUG-62874 [REG: 5.8->5.9]: Controls 2 BusyIndicator animation does  
not update if it is inside QQuickWidget  
* QTBUG-65108 'checkable' feature of a Button doesn't work if the Button  
has an action connected to it  
* QTBUG-65165 Tumbler's animation accelerates slowly with large  
scrolling distances  
* QTBUG-65016 QQuickStyle::setFallbackStyle is broken on iOS  
* QTBUG-62110 Slow swipe on HighDPI android device  
* QTBUG-65084 QtQuickControls2: StackView eats all touch events  
* QTBUG-65341 Broken customization  
* QTBUG-57147 License files LGPLv2 is still present  
* QTBUG-65052 Hovering bug for ToolButton in Listview with less than 3  
character text  
* QTBUG-60550 Drawer has no documentation for adding content to it  
* QTBUG-65500 Cannot configure Font property for Imagine style  
* QTBUG-65445 Improve Style/FallbackStyle documentation  
* QTBUG-65880 [REG 5.9.3 => 5.9.4] Popup opened at 0, 0 has no  
background  
* QTBUG-65889 Shortcut stops triggering Action when the Action is  
assigned to a Button in a Repeater  
* QTBUG-65784 [Reg 5.10 -> 5.11] Stack overflow crash caused by 9e1b044  
(QTBUG-56557)  
* QTBUG-65962 [REG: 5.9.3->5.9.4] ComboBox popup doesn't show up  
* QTBUG-63185 grabImage() doesn't work on software renderer  
* QTBUG-55251 Context menu opens further away from the cursor the  
further the mouse is clicked from the top-left edge of the window  
* QTBUG-66176 QML TextField QuickControls2 - placeholderText is almost  
transparent when background is black  
* QTBUG-65193 When having multiple Actions with same icon set, first  
Action's image is drawn as a black box in Quick Controls 2  
* QTBUG-66113 Nested popups cause Keys.onBackPressed event handler to  
not be executed  
* QTBUG-51321 StackView should clear focus when a new item is pushed  
* QTBUG-51921 Mixing QtQuickControls2 and QtQuickControls breaks menu  
fonts  
* QTBUG-66358 Tumbler has no means of setting currentIndex without  
animation  
* QTBUG-59719 DialogButtonBox don't create a button when there is only  
one button.  
* QTBUG-66669 Segfault when running qmlplugindump on Qt Quick Templates  
* QTBUG-66752 QtQuickControls2 BusyIndicator not showing with fusion  
style  
* QTBUG-66658 StackView documentation don't explain memory management  
and is confusing  
* QTBUG-66430 QML font size changes after calling QApplication::font()  
* QTBUG-66386 Checkable Platform MenuItem can't be used like Controls  
MenuItem  
* QTBUG-66874 No documentation for managing a dynamically generated list  
of platform menu items  
* QTBUG-66876 Can't use qsTr() in submenu titles on macOS  
* QTBUG-66889 Crash when closing application that uses nested native  
menus on Windows  
* QTBUG-66637 When a Slider resides on a Drawer then the slider handle  
is not updating when dragging correctly  
* QTBUG-66995 FAIL!  : tst_controls::Default::Button::test_checkable()  
'verify()' returned FALSE. ()  
* QTBUG-67118 QQuickStackView::initialItem gets deleted, leaving a  
dangling pointer  
* QTBUG-66044 SpinBox wheel event propagation  
* QTBUG-67152 Assert when using Material or Universal Style in Qt Quick  
Designer  
* QT3DS-1363 Color Dialog doesn't show current color at first launch  
* QTBUG-66625 QQuickIcon not properly registered  
* QTBUG-67317 RangeSlider lacks a valueAt() function  
* QTBUG-67334 Regression: ScrollView+TextArea do not scroll correctly  
* QTBUG-67442 Incorrect color for disabled status in check indicator and  
radio indicator  
* QTBUG-66276 QtQuick Controls2 Fusion style plugin doesn't have a  
plugins.qmltypes  
* QTBUG-67501 qtquickcontrols2 module compiled with option CONFIG +=  
qtquickcompiler' doesn't work  
* QTBUG-67573 CheckIndicator does not have a color for the disabled  
status in Material Style  
* QTBUG-67574 RadioIndicator does not have a color for the disabled  
status in Material Style  
* QTBUG-60156 Padding for background in Control  
* QTBUG-67478 Slider's snapMode docs don't mention stepSize  
* QTBUG-67684 If QML ComboBox is closed through a timer (visible =  
false), the open popup is not closed  
* QTBUG-66455 When specifying the implicitWidth for a background item on  
a Button, the implicitWidth is not propagated to the Button correctly  
* QTBUG-67930 tst_controls::Material::ComboBox::test_keyClose(Escape)  
and test_keyClose(Back) failed  
* QTBUG-68665 tst_controls::Default::AbstractButton::test_trigger(click  
disabled button) failed  
* QTBUG-68556 Last tab in TabBar not shown correctly with Fusion style  
* QTBUG-66834 Missing docs for exporting Imagine assets  
* QTBUG-68769 Setting RenderType on Controls 2 Textfield results in cut-  
off text on high-dpi displays  
* QTBUG-68618 QtQuickControls2 won't build  
* QTBUG-68737 Tumbler resets currentIndex after modelChanged was emitted  
* QTBUG-68222 QQuickStyle::addStylePath does not work with qrc:/ paths  
* QTBUG-68858 QtQuickControls 2 Menu does not scroll if height is larger  
than screen  
* QTBUG-69141 TabButton missing documentation on web  
* QTBUG-69286 Regression in DialogButtonBox attached properties (5.11 =>  
dev)  
* QTBUG-68298 Lack of "AbstractButton.TextUnderIcon" in documentation  
* QTBUG-69376 ScrollView will not scroll for particular content items  
* QTBUG-68219 Style path through environment variable does not work for  
locations in resources  
* QTBUG-66483 Qml ShaderEffectSource/ShaderEffect crashes on exit  
* QTBUG-69551 ItemDelegate "padding" property doesn't set top/bottom  
padding any more  
* QTBUG-69506 Resizing IconImage changes it's actual color if `color` is  
translucent  
* QTBUG-69839 [REG: 5.10.1->5.11.0] QML ColorDialog  in "texteditor"  
sample crashes on MacOS 10.13.6 (HighSierra)  
* QTBUG-69897 Unstyled StackView from Templates crashes on push()  
* QTBUG-69916 qtquickcontrols2/src/imports/platform/qquickplatformmessag  
edialog.cpp:379:51: error: use of overloaded operator '<<' is ambiguous  
* QTBUG-70065 tst_QQuickStyle::qrcInQtQuickControlsStylePathEnvVar()  
failed on macOS 10.13  
* QTBUG-67559 Setting a reusable delegate for a Menu (QML type) doesn't  
work  
* QTBUG-70413 tst_controls::Default::Popup::test_shortcut is flaky  
* QTBUG-70063 tst_font::font(Control) crash on macOS 10.13  
* QTBUG-71387 Crash after calling qmlClearTypeRegistrations()  
* QTBUG-71694 Qt Quick Controls (former Qt Quick Controls 2)  
documentation not found from Qt Creator's Help  
* QTBUG-70652 Fusion palette regression in 5.12 (macOS)  
* QTBUG-71735 Pane/Page with Layout steals all events of parent  
MouseArea  
* QTBUG-71942 Qt Quick controls 2 SpinBox crashes the qml2puppet  
* QTBUG-72539 QRegularExpression:: wildcardToRegularExpression does not  
work as expected  
* QTBUG-72750 Slider wheel event propagation  
* QTBUG-73202 Can't tab out from QtQuick.Controls.TextArea cotrol  
* QTBUG-69682 QtQuickControls 2 Menu does not close if Action becomes  
disabled  
* QTBUG-73849 Documentation: wrong link for Number.toLocaleString  
* QTBUG-71290 QML Drawer lockup when attached to top edge which does not  
coincide with screen top edge  
* QTBUG-74226 Attached ToolTip timeout copied across to other attached  
ToolTips  
* QTBUG-70597 Tumbler::test_itemsCorrectlyPositioned() is flaky  
* QTBUG-74919 qquickcombobox.cpp:187:13: error: ‘QString  
QQuickComboBoxDelegateModel::stringValue(int, const QString&)’ marked  
‘override’, but does not override  
* QTBUG-74902 StackView doesn't fit its content  
* QTBUG-75546 QML Menu documentation is not mentioning default value of  
focus property  
* QTBUG-75558 Non-existing property is used in code snippet for QML  
Action shortcut documentation  
* QTBUG-67343 Windows: dynamically creating a ComboBox with a  
ShaderEffect delegate triggers an assert  
* QTBUG-76608 Unblacklisting passing tests  
* QTBUG-77815 agent:2019/08/23 13:47:41 build.go:215: Error in line 3:  
Namespace "" has invalid syntax in file:  
"/home/qt/work/build/qtbase/doc/qtquickcontrols/qtquickcontrols.qhp"  
* QTBUG-78261 tst_focus::policy is failing on OpenSUSE  
* QTBUG-78799 Docs link to Qt Quick Controls 1 StackView  
* QTBUG-78690 QML API Review for 5.14  
* QTBUG-59330 Content of a QRC-file conflicting with the Material style  
* QTBUG-83172 tst_QQuickHeaderView::listModel() 'vhvCell2' returned  
FALSE. ()  
* QTBUG-82279 NumberAnimation on enter/exit of Menu is not working with  
negative starting value  
* QTBUG-82954 QTextDocument height includes leading of last line  
* QTBUG-81976 ListView delegates produces "TypeError: Cannot read  
property 'width' of null" when removing item from QAbstractItemModel  
* QTBUG-84102 Qt.labs.platform/MenuItem 1.1  
* QDS-2278 Dial specifics snap mode not working  
* QTBUG-82978 Allow "-Wextra-semi-stmt" on Q_UNUSED  
* QTBUG-82989 Decide upon and document our stance on binding to parent  
in delegates  
* QTBUG-85903 StackView: calling pop() with one item does nothing  
* QTBUG-64151 "Error: Locale: Number.fromLocaleString(): Invalid format"  
when erasing last digit of "2,000" in editable SpinBox  
* QTBUG-85151 "module "QtQuick.Templates" is not installed" when some  
files' QML imports specify version and some don't  
* QTBUG-85699 Material ToolBar: "QML Material: Binding loop detected for  
property "foreground""  
* QTBUG-86399 Windows: add remaining native style patches for Windows  
* QTBUG-86815 Rename all internal CMake functions to start with  
qt_internal  
* QTBUG-87164 qmllint library search regression  
* QTBUG-87661 Rename add_qt_gui_executable in examples to  
qt_add_executable across all repos  
* QTBUG-86053 Figure out and add missing CI CMake configs that mirror  
qmake non-Packaging ones  
* QTBUG-87664 Adjust behavior of add_qt_gui_executable /  
qt_add_executable as per API review  
* QTBUG-88114 Make sure QFontDatabase methods are used as static methods  
* QTBUG-88343 Mirror -no-gui qmake configuration in CMake  
* QTBUG-88372 Rewrite of Qt object breaks QtQuickControls2 tests  
* QTBUG-87818 AUX_QML_FILES Designer files are missing from cmake build  
* QTBUG-88533 qdoc errors in QtCore  
* QTBUG-88553 "invalid nullptr parameter" when running Qt Quick Controls  
- Contact List example  
* QTBUG-52466 Styles need to be explicitly imported to work with static  
builds  
* QTBUG-90401 Heap-use-after-free in QAbstractAnimationJob  
* QTBUG-86567 When destroying an item in a model that has an animation  
running as part of its delegate then it can cause a crash to occur  
* QTBUG-90869 tst_qquickdesignersupport: tests segfault when running on  
QEMU and Windows MinGW developer build  
* QTBUG-90439 Doc: Fix CI warnings qtdeclarative  
* QTBUG-41867 disabled particle Emitter still causes QSG renderer  
uploads  
* QTBUG-89943 Deprecate injected arguments for signal handlers  
* QTBUG-91116 tst_qquickflickable is unstable on macOS 11  
* QTBUG-89938 tst_QQuickPopup::macOS fails with macOS 10.15 and 11.1 and  
with Xcode 12.3  
* QTBUG-46350 Crash when deleting item currently set in PropertyChanges  
target  
* QTBUG-88263 [REG v6.0.0-beta3 -> dev] cmake-based configure pollutes  
the source tree  
* QTBUG-91141 qdoc/WebXML (Qt 6): Invalid links to "Changes to Qt  
<Module>" are inserted into \brief of classes and other places  
* QTBUG-91276 DelegateModel can crash with retranslate()  
* QTBUG-86708 When using DelegateModelGroup to group items then when a  
created item which is set to not be included will trigger an assert  
* QTBUG-86729 many Qt Quick test failures after input event refactoring  
* QTBUG-92861 QtQml does not provide version 6.2  
* QDS-4212 Changing Range Slider snap mode changes it's orientation  
* QTBUG-72906 ListView rejects QList models  
* QTBUG-93358 qmllint: Add support for UiArrayBindings  
* QTBUG-92500 When using a ShaderEffect which has been compiled with the  
qsb tool, it does not apply the effect at all  
* QTBUG-80415 segfault in software renderer inside  
QSGSoftwareInternalImageNode  
* QTBUG-87260 TextArea with QSyntaxHighlighter : setUnderlineColor and  
setUnderlineStyle not working  
* QTBUG-88644 tst_QQuickGridView::snapToRow() failed on msvc2019  
developer build in CI  
* QTBUG-92984 Image is painted with wrong Z order  
* QTBUG-78996 JavaScript getDay() regression on MinGW  
* QTBUG-93841 Superfluous calls to int qRegisterMetaType(const char  
*typeName)  
* QTBUG-27671 QMLTest: Some subtests of  
tests/auto/qmltest/events/tst_events.qml are flaky  
* QTBUG-88672 REG: Performance regression in Qt Quick Controls 2  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
* QTBUG-93983 GeoLocation::test_Location_complete fails  
* QTBUG-94030 Minimal plugin not found in static build although  
explicitly imported  
* QTBUG-93972 ASTC compressed textures rendering orientation not  
consistent  
* QTBUG-87775 Passing INTERNAL_MODULE to qt_internal_add_module should  
only create a single Qt::FooPrivate target  
* QTBUG-94068 Undefined behavior  
* QTBUG-87708 [Reg 5.15.0 -> 5.15.1] header's width isn't resized to  
window's width when Layout is used  
* QTBUG-94251 tst_QQuickPopup fails with OpenSUSE 15.3  
* QTBUG-89536 Remove configure.json files for building Qt 6  
* QTBUG-93257 qt6_import_qml_plugins does not compose  
* QTBUG-77417 qmllint: need to handle SignalTransition guard properties  
* QTBUG-54267 Qt Quick Calqlatr example does not properly reflect the  
current way of using Qt Quick  
* QTBUG-94798 crash in QQuickDesignerSupport with gcc at ubuntu  
* QTBUG-94971 QHoverEvent::scenePosition() is actually local position  
* QTBUG-93890 Crash in webOS emulator with recent meta-qt6  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
* QTBUG-95208 Linker error regarding bitcode when linking CMake app  
targeting iOS  
* QTBUG-94928 loop QQuickDesignerSupport with simple example  
* QTBUG-75862 FocusReason is broken in Controls 2  
* QTBUG-89380 Cannot use QtObject as containmentMask  
* QTBUG-95152 A QtWebEngine build fails on dev on M1 MacBook  
* QTBUG-94844 Rendering errors with ShaderEffect after hiding and  
reshowing a window  
* QTBUG-95567 Failure in TestQmllint when merging qtquickcontrols2 into  
qtdeclarative  
* QTBUG-87580 Add minimal set of tests to build for static Qt configs in  
Coin  
* QTBUG-88138 tst_QQuickDrawer::macOS::slider is failing  
* QTBUG-95756 tst_QQmlImport::removeDynamicPlugin() is flaky on macOS  
* QTBUG-95609 cmake names for qml plugins  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-95763 Configuring an executable with an attached qml module  
fails when using the Xcode generator  
* QTBUG-95845 qt_add_qml_module unconditionally installs metatypes.json  
files into "arbitrary" directory  
* QTBUG-95788 Singletons with clearComponentCache don't fully work  
* QTBUG-93340 trafficlight_qml_dynamic crashes on Android device  
* QTBUG-96121 Versionless CMake commands prevent setting variables in  
calling scope  
* QTBUG-96159 Qt5.git integration fails in '6.2':  The "moc" executable  
"/Users/qt/work/qt/qt5/qtbase/libexec/moc" does not exist  
* QTBUG-96219 Conversion of versionless wrapper functions to macros  
needs to be reverted  
* QTBUG-96144 qmlsc generates bad code for assigning strings to colors  
* QTBUG-81302 WheelHandler wheel signal is not documented  
* QTBUG-95587 icon.source of Control is not resolved relative to user  
code  
* QTBUG-96127 Broken external links in Qt docs  
  
### qtactiveqt  
* QTBUG-92351 Update dependencies on 'dev' in qt/qtactiveqt fails  
* QTBUG-92237 Document the qaxserver_no_register configuration  
* QTBUG-93446 MingGW: activeqt/qutlook configure fails  
* QTBUG-93944 error: "NOMINMAX" redefined  
* QTBUG-95407 activeqt/qutlook fails to configure  
* QTBUG-95406 activeqt examples fails to build, MinGW  
* QTBUG-91743 The new /readded 6.1 modules are missing from doc snapshot  
server  
* QTBUG-88414 CMake multi-config build still build some debug tools  
* QTBUG-96121 Versionless CMake commands prevent setting variables in  
calling scope  
* QTBUG-96219 Conversion of versionless wrapper functions to macros  
needs to be reverted  
  
### qttools  
* QTBUG-89980 Tools (Assistant, Designer, Linguist) copyright still 2020  
* QTBUG-90867 qdoc: Warning limit has no effect in single-exec mode  
* QTBUG-91088 QFormBuilder does not save 'name' attribute on 'widget'  
elements in UI-file  
* QTBUG-91244 [REG] qdoc fails to find overloaded functions from the  
global namespace  
* QTBUG-91558 [REG 6.0/5.15.4] lconvert can not read .qm files  
* QTBUG-91746 Incomplete statement in QDoc documentation on  
\instantiates  
* QTBUG-91753 Designer cannot change font  
* QTBUG-91754 qdoc crash when generic documents of qtbase  
* QTBUG-91990 qdoc: \property command fails with a const property type  
* QTBUG-92458 Fix potential memory leak in QHelpContentProvider  
* QTBUG-92590 qdoc generates 'quick3', 'qt3' tags for qtquick3d, qt3d  
* QTBUG-92478 [QDoc] Links for obsolete methods point to the wrong page  
* QTBUG-92355 scoped enum values can't be linked in documentation  
* QTBUG-65810 Outdated copyright notes  
* QTBUG-91644 macdeployqt doesn't deploy plugins when build qt with  
custom -plugindir and frameworks in app bundle cannot resolve rpath  
* QTBUG-92386 [QDoc]  \omitvalue does not omit the enum's description  
* QTBUG-93422 qlitehtml library is not installed  
* QTBUG-49591 Qt Designer: QTableWidget : Horizontal labels are not  
visible (horizontalHeaderVisible property is not saved correctly) when  
in page-based container  
* QTBUG-93265 qdoc: Handle versionless imports for Qt Quick 3D  
gracefully  
* QTBUG-85513 QTableWidget header item alignment defaults to  
Qt::AlignHCenter|Qt::AlignVCenter visually but Designer shows AlignLeft  
* QTBUG-93646 .gitignore files in qttools  
* QTBUG-94034 qlitehtml: compiler warning C4530  
* QTBUG-94395 qdoc: Incorrect signature generated for QML signals  
* QTBUG-74353 Qt Assistant doesn't take stylesheet into account with  
search result view  
* QTBUG-90540 Incomplete documentation of namespace "Qt"  
* QTBUG-94480 qdoc:  Broken links to a non-existing module pages  
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
* QTBUG-95948 qdoc: Tagging an \fn does not work for \fn commands that  
share a doc comment  
* QTBUG-94796 macdeployqt does not deploy  
/Contents/PlugIns/sqldrivers/libqsqlite.dylib anymore  
* QTBUG-96096 translations are not installed anymore  
* QTBUG-95981 qdoc is ignoring the full path of identical source file  
names  
* QTBUG-95125 [REG 6.1.0 -> 6.2] Assistant shows blank page  
* QTBUG-96220 qt6_create_translation() mishandles -extensions due to  
malformed regex  
* QTBUG-95247 windeployqt does not copy tls plugins  
* QTBUG-96694 broken "Contents" links in assistant  
* QTBUG-91141 qdoc/WebXML (Qt 6): Invalid links to "Changes to Qt  
<Module>" are inserted into \brief of classes and other places  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
* QTBUG-89860 Document QDoc warnings  
* QTBUG-91521 When calling lupdate on a file that uses QT_TR_NOOP in a  
constructor for a static QString it will fail to find the context  
* QTBUG-87090 Several lupdate tests are failing with clang-based lupdate  
* QTBUG-89536 Remove configure.json files for building Qt 6  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
* QTBUG-88090 Installed CMake files reference the SOURCE TREE  
* QTBUG-95305 ninja dependency error when configuring a project that  
uses AUTOUIC and CMake 3.21.0  
* QTBUG-96121 Versionless CMake commands prevent setting variables in  
calling scope  
* QTBUG-96219 Conversion of versionless wrapper functions to macros  
needs to be reverted  
  
### qttranslations  
* QTBUG-93280 [Reg 5.15.3->6.0] Dialog buttons translated even though  
they shouldn't be  
* QTBUG-94370 .qm files should be put into qtbase/translations for non-  
installable builds  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
  
### qtdoc  
* QTBUG-86614 When a service is set to be started at boot time it is not  
being started after a reboot of the device  
* QTBUG-92047 Configure "-help" does not mention "-xplatform"  
* QTBUG-91239 Porting to Qt6: high dpi scale factor default rounding  
policy not documented  
* QTBUG-56322 Qt for Android source package build error in examples  
* QTBUG-90510 libqmacstyle.dylib should be mentioned in the document  
* QTBUG-92848 Update Documentation of Qt6: Deploying QML Applications -  
Ahead-of-Time Compilation  
* QTBUG-93245 Documentation: New 6.1 modules missing from overview  
* QTBUG-94903 Add new 6.2 modules to "All Modules"  
* QTBUG-95990 Add support for multi-abi application builds for Android  
with qmake  
* QTBUG-93895 Error C2440: 'initializing': cannot convert from 'const  
TCHAR *' to 'const wchar_t *  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
* QTBUG-94183 build failure: LINK : fatal error LNK1181: cannot open  
input file 'propsys.obj'  
* QTBUG-95271 Document "qt-cmake" or add an example which folder in the  
Qt installation should be listed in CMAKE_PREFIX_PATH  
* QTBUG-95748 QtSensors:  update qtdoc module listing  
* QTBUG-96150 QML best practices docs are outdated  
* QTBUG-96127 Broken external links in Qt docs  
  
### qtwayland  
* QTBUG-91206 Input hints not delivered to virtual keyboard with new  
text input protocol  
* QTBUG-86177 Some subsurfaces change but are never committed  
* QTBUG-91096 >1 Programs on QtWayland causes QtVirtualKeyboard to not  
work  
* QTBUG-89680 Touch is ignored if up and down arrives in the same  
wl_touch.frame  
* QTBUG-92925 configure message: no wayland-egl support detected  
* QTBUG-81504 QWaylandWindow::handleUpdate creates thousands of pending  
frame callbacks, causing wayland connection termination  
* QTBUG-93751 Update dependencies on 'dev' in qt/qtwayland  
* QTBUG-92249 quick3d examples crashes or hangs on exit on wayland  
* QTBUG-94085 cmake automoc error when configuring qtwayland (in  
autotests)  
* QTBUG-94602 Releasing wayland buffer from Qt compositor side  
* QTBUG-95394 Crash in RHI when exiting a QtWaylandCompositor with  
active clients.  
* QTBUG-64652 TextInputManager lacks documentation  
* QTBUG-95464 Qt wayland surface is empty when gst-launch client is  
playing video  
* QTBUG-88263 [REG v6.0.0-beta3 -> dev] cmake-based configure pollutes  
the source tree  
* QTBUG-92861 QtQml does not provide version 6.2  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
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
  
### qt3d  
* QTBUG-92163 top-level configure returns with exit code != 0 if qt3d is  
checked out  
* QTBUG-92259 Missing qmltypes support for quick3dcoreplugin  
* QTBUG-93240 Configure error in qt3d for -developer-build -release  
* QTBUG-93428 Examples not finding QtConcurrent  
* QTBUG-90243 Unable to build Qt3D Add-On with Conan, Qt6.0.1,  
Qt6.1.0Alpha,6.0.2, 6.0.3, 6.0.4  
* QTBUG-92861 QtQml does not provide version 6.2  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
* QTBUG-93035 Adding a disable entity to the scene and enabling it later  
isn't properly picked up  
* QTBUG-95130 Qt3D ShaderProgram sources cannot compile on iOS (RHI)  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
* QTBUG-90321 QT_BEGIN_LICENSE:LGPL3 references non-existing file  
LICENSE.GPL  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
  
### qtimageformats  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
* QTBUG-89536 Remove configure.json files for building Qt 6  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
  
### qtcharts  
* QTBUG-59040 QtCharts performance bad when min/max values changed  
* QTBUG-79218 When zooming out enough then the labels on the axes will  
end up showing drawing errors  
* QTBUG-94084 Update dependencies on 'dev' in qt/qtcharts  
* QTBUG-94469 Doc: Wrong return type for QValueAxis::labelFormat qml  
property  
* QTBUG-94472 [REG 6.2 snapshot->6.2 current] qml/QtCharts/designer -dir  
missing  
* QTBUG-95307 Qt Charts is missing in module upgrade documentation  
* QTBUG-90583 conanfile.py: Accept QTDIR in addition to QT_PATH  
* QTBUG-92861 QtQml does not provide version 6.2  
* QTBUG-93672 zooming infinitely causes infinite allocating loop  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
* QTBUG-94025 All points after selected point are marked as selected  
* QTBUG-94181 error: â€˜defaultInputDeviceâ€™ is not a member of  
â€˜QAudioDeviceInfoâ€™  
* QTBUG-89536 Remove configure.json files for building Qt 6  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
  
### qtdatavis3d  
* QTBUG-91032 Some autotests fail on Qt 6.1  
* QTBUG-90710 Some tests fail  
* QTBUG-91053 macOS coin build fails  
* QTBUG-91347 tst_proxy::multiMatch() Received a fatal error  
* QTBUG-90663 RHI backend selection is not documented  
* QTBUG-92167 Adding additional libraries to qt5.git fails  
* QTBUG-93263 QtDatavisualization examples not compiling on Android  
* QTBUG-91103 QML theme shows as totally dark when specified during  
creation  
* QTBUG-93506 Gradients don't show.  
* QTBUG-93676 Itemmodel example draws text as garbage  
* QTBUG-92995 Some datavisualization examples run with warnings  
* QTBUG-94182 error: no member named 'setCodec' in  
'TestNamespace::QAudioFormat'  
* QTBUG-90665 RenderingMode changing does not work correctly  
* QTBUG-80194 Q3DScatter Memory Leak  
* QTBUG-94256 Manual tests do not compile  
* QTBUG-94331 Some examples do not work correctly on macOS  
* QTBUG-94364 Rotate and zoom do not work on Android  
* QTBUG-96206 Graph's orthoprojection property doesn't work like  
documentation says  
* QTBUG-90583 conanfile.py: Accept QTDIR in addition to QT_PATH  
* QTBUG-91381 tst_qmltestWrapperRelWithDebInfo is failing in 6.1  
* QTBUG-90664 Some examples do not work correctly  
* PYSIDE-1438 Using QBar3DSeries.dataProvider().addRow() segfaults  
* QTBUG-92861 QtQml does not provide version 6.2  
* QTBUG-86815 Rename all internal CMake functions to start with  
qt_internal  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
  
### qtvirtualkeyboard  
* QTBUG-90809 Inconsistent behavior of InputPanel between release and  
debug config on Windows  
* QTBUG-92881 InputPanels defaults z value should be lower than max  
value for overlays  
* QTBUG-93459 [Highlighted example] virtualkeyboard/static fails to  
compile on iOS  
* QTBUG-93997 Warnings with virtual keyboard in Qt 6  
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
* QTBUG-92861 QtQml does not provide version 6.2  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
* QTBUG-89536 Remove configure.json files for building Qt 6  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
  
### qtscxml  
* QTBUG-93444 [Highlighted example] qtscxml/trafficlights-qml-dynamic  
crashes on Android hw  
* QTBUG-93727 CMake Error with -developer-build due to target name  
conflict  
* QTBUG-94125 Update dependencies on 'dev' in qt/qtscxml fails  
* QTBUG-94386 Update dependencies on '6.2' in qt/qtscxml fails  
* QTBUG-95208 Linker error regarding bitcode when linking CMake app  
targeting iOS  
* QTBUG-60045 SCXML examples fail to compile with -no-gui  
* QTBUG-92494 Ability to use STATECHARTS with qmake in Qt6  
* QTBUG-92861 QtQml does not provide version 6.2  
* QTBUG-92541 statemachine/padnavigator, build fails: QOpenGLWidget: No  
such file or directory  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
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
  
### qtnetworkauth  
* QTBUG-93243 QtNetworkAuth fails to build when Qt is configured with  
FEATURE_thread=OFF  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-96127 Broken external links in Qt docs  
  
### qtlottie  
* QTBUG-92861 QtQml does not provide version 6.2  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
  
### qtquicktimeline  
* QTBUG-88263 [REG v6.0.0-beta3 -> dev] cmake-based configure pollutes  
the source tree  
* QTBUG-89467 .prl file generation is dependent on add_subdirectory  
order  
* QTBUG-92861 QtQml does not provide version 6.2  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
* QDS-3216 Flickering when using default value as implcit first keyframe  
  
### qtquick3d  
* QTBUG-89886 assert/segfault on exit in MultipleViews.qml  
* QTBUG-90514 Loader with View3D crashes  
* QTBUG-89433 Unredistributable files in qt3d and qtquick3d  
* QTBUG-89872 Error with instancing in depth pre-pass and shadows  
* QTBUG-91118 Texture.indexUV is unstable  
* QTBUG-91412 Texture.sourceItem does not handle all textureProvider  
items correctly  
* QTBUG-91879 Invisible but item layer View3D with Inline render mode  
crashes  
* QTBUG-91871 View3D with no size specified crashes with OpenGL only  
* QTBUG-88320 Dynamically creating a View3D second time crashes  
* QTBUG-91888 Item2D + importScene = crash due to the well-known dead-  
rhi-objects-in-cache-key problem  
* QTBUG-89946 SpotLight doesn't work properly with PBR materials  
* QTBUG-92215 custom shaders example: no ui elements interacatable  
* QTBUG-92389 QQuick3DInstancing not clearing m_instanceDataChanged  
* QTBUG-92917 Changing instanceCountOverride has no effect  
* QTBUG-92959 QtQuick3D fails to compile targeting WebAssembly  
* QTBUG-93097 Quick3D Texture might not capture the latest state of  
sourceItem  
* QTBUG-90564 Crash if some importer plugin can't be loaded  
* QTBUG-93266 The new QML types in Qt Quick 3D for the particle system  
miss  a \since  
* QTBUG-93429 QtQuick3D fails to compile targeting WebAssembly part 2  
* QTBUG-93605 PointLight is not properly projected on skinned meshes  
* QTBUG-92953 Mesh rotation is not correct if it is not in Skeleton node  
* QTBUG-92944 input problems in DynamicTexture example  
* QTBUG-93095 View3D picking breaks if 2D Quick Item added to scene  
* QTBUG-93972 ASTC compressed textures rendering orientation not  
consistent  
* QTBUG-94185 Misplaced Joint{} element may crash application  
* QTBUG-94230 Node method map***() causes crash if node if null  
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
* QTBUG-95586 Z-Prepass doesn't render correctly if scene has only  
transparent objects with depth write  
* QTBUG-95743 TransformSpace property of Node item can't be read/changed  
* QDS-4841 Remove import versions from quick3D designer source templates  
for Cube, View3D etc.  
* QTBUG-95616 Incorrect shadowmap bounds calculated from camera frustum  
* QTBUG-95583 Incorrect shadowmap bounds when referencing camera from  
different node  
* QDS-4853 Picking 3D objects is completely broken in 3D editor  
* QDS-4873 Designer specifics have errors for quick3d property sheets  
* QTBUG-94829 Directional light casts too wide shadows  
* QTBUG-94830 Rotation of skeleton root node rotates the skeleton but  
not the skinned meshes  
* QDS-4859 Item could not be created -error when adding a Qt 3D Studio  
component to Navigator (Qt6 project)  
* QTBUG-95620 QuickBall example crashes after hitting the first target  
* QTBUG-91271 useRandomSeed alone doesn't make particles deterministic  
* QTBUG-88263 [REG v6.0.0-beta3 -> dev] cmake-based configure pollutes  
the source tree  
* QTBUG-91195 Emitters do not work correctly when in node hierarchy  
* QTBUG-90788 Fix eulerRotation etc. with particles  
* QTBUG-91730 Fix affector extra updates  
* QTBUG-91729 Fix velocity with rotated emitter  
* QTBUG-91681 Consistant rendering order for particles  
* QTBUG-92019 Fix Attractor3D on node tree  
* QTBUG-92028 Particles rotating too fast on android  
* QTBUG-92104 Quick3D QuickBall example crashing on dev  
* QTBUG-92203 Snowing example crashes with big intensity values  
* QTBUG-92255 ParticleSystem trail ghost emits when restarted  
* QTBUG-92169 Asset handling: Qml write for the intermediate scene  
format needs to output resources correctly  
* QTBUG-89175 quick3d: set property 'parent' of Node not work  
* QTBUG-92831 Particles testbed Animated Sprite not working with qmake  
* QTBUG-92171 Asset handling: Complete the assimp importer for the new  
intermediate format  
* QTBUG-92861 QtQml does not provide version 6.2  
* QTBUG-93034 No changed signals from particlesystem time  
* QTBUG-92892 Rotated emitter velocity not always correct  
* QTBUG-90817 Quick3D Model bounds not set in an imported scene  
* QTBUG-93648 Crash when going back in particles example after viewing  
Fire And Smoke  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
* QDS-4399 Properties missing for some components  
* QDS-4477 Imported Qt3DStudio project looks different in DS built with  
Qt6.1 compared to QDS 2.1  
* QTBUG-94453 Rectangles can't be used for light probs in View3D  
* QTBUG-89536 Remove configure.json files for building Qt 6  
* QTBUG-94548 Multimeshes not working with model-blend particles  
* QDS-4509 Cannot run a project that has QtQuick3D Effects module added  
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
  
### qtshadertools  
* QTBUG-92882 qtshadertools and qtdeclarative Quick not built for QNX  
* QTBUG-95048 Linkage error during building any qt quick3D application  
for Integrity based on Qt6  
* QTBUG-96618 qtquick3d examples fail to build for QNX  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
* QTBUG-96121 Versionless CMake commands prevent setting variables in  
calling scope  
* QTBUG-96219 Conversion of versionless wrapper functions to macros  
needs to be reverted  
  
### qt5compat  
* QTBUG-92861 QtQml does not provide version 6.2  
* QTBUG-93015 ColorOverlay color property documentation wrong  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
* QTBUG-89536 Remove configure.json files for building Qt 6  
* QTBUG-90819 Linking relationships to plugins are incorrectly specified  
* QTBUG-95636 Update cmake_minimum_required to 3.16 in all CMake Qt  
example projects  
* QTBUG-83081 QTextCodec::canEncode does not work for ICU conversions  
  
Known Issues  
------------  
  
* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-6/gettingstarted.html#platform-requirements  
* RTA reported issues from Qt 6.2  
https://bugreports.qt.io/issues/?filter=23315  
* Supported development platforms are listed here:  
https://bugreports.qt.io/browse/QTBUG-90021  
* See Qt 6.2.0 Known Issues from:  
https://wiki.qt.io/Qt_6.2.0_Known_Issues  

Credits for the  release goes to:  
---------------------------------  
  
Aavitsland Eirik  
Achtelik Mike  
Adam Cristian  
Agocs Laszlo  
Akulich Alexander  
Akulich Alexandr  
Angelelli Paolo  
Apostolou Dimitrios  
Avtomonov Nikolay  
Bai Yulong  
Baijot Vincent  
Beernaert Leander  
Beldi Luca  
Benelli Marco  
Bennett Nicholas  
Bin Chen  
Binner Stephan  
Blasche Alex  
Blechmann Tim  
Blomfeldt Eskil Abrahamsen  
Borisova Tatiana  
Bornemann Joerg  
Bot Qt CI  
Bot Qt Forward Merge  
Boudjelthia Assam  
Brasser Michael  
Broulik Kai Uwe  
Buddenhagen Oswald  
Bugaev Igor  
Buhr Andreas  
Burchell Robin  
Butirsky Andrey  
Byun Jungi  
Callegari Massimo  
Chao Caroline  
Chuan Wang  
Cid Albert Astals  
Croitor Alexandru  
Curtis Mitch  
D'Angelo Giuseppe  
David Szabolcs  
Dhumal Shrikant  
Dietrich Gabriel de  
Dietz Pascal  
Dippold Michael  
Dushistov Evgeniy A.  
Edelev Alexey  
Edmundson David  
Eftevaag Oliver  
Ehrlicher Christian  
Eklund Iikka  
ElKharashy Hatem  
Erb Jason  
Falsini Fabio  
Fanaskov Vitaly  
Faure David  
Fedin Ilya  
Fella Nicolas  
Fernandez Jesus  
Fokin Valentin  
Fontaine Fabrice  
Frantzis Alexandros  
Funk Kevin  
Fält Simo  
Gaist Samuel  
Gehör Pekka  
Genkhel Roman  
Gerard Lucie  
German Aleksei  
Gladhorn Frederik  
Goldstein Maximilian  
Golubev Andrei  
Griebl Robert  
Gronowski Paweł  
Gruendl Henning  
Grulich Jan  
Grönholm Kaj  
Guichard Nicolas  
Gustavsen Richard Moe  
Gérard Lucie  
Haixiang Tang  
Halmet Heikki  
Hao Zhang  
Hartmann Thomas  
Hartmetz Andreas  
Hausmann Simon  
Heikkinen Jani  
Heikkinen Miikka  
Heimrich Karsten  
Heng Gong  
Hermann Ulf  
Heskestad Øystein  
Hilsheimer Volker  
Holland Dominik  
Jeisecke Nils  
Jensen Allan Sandfeld  
Jenssen Tim  
Jie Huang  
Jung Jaeyoon  
Kalinowski Maurice  
Kanapickas Povilas  
Karlsson Jonas  
Katz Jeremy  
Keller Christoph  
Khang Hyunkook  
Kim Hyungchan  
Kim Youngjin  
Kittler Marius  
Kleint Friedemann  
Klocek Michal  
Knoll Lars  
Kobus Jarek  
Koehne Kai  
Koh Sze Howe  
Koivikko Jarkko  
Kokko Antti  
Korpipaa Tomi  
Koscheev Vyacheslav  
Kosinski Lukas  
Koskinen Janne  
Kosmale Fabian  
Krause Volker  
Krupenko Nikita  
Krus Mike  
Kudryavtsev Anton  
Kurazyan Sona  
Kushnir Igor  
Kvinge Jonas  
Kyzivat Keith  
Köhne Kai  
Lee Elvis  
Lee Inho  
Lei Hou  
Leinonen Tony  
Lemire Paul  
Li Qiang  
LinKun Xing  
Liu Haoyu  
Löhning Robert  
Macieira Thiago  
Mardegan Alberto  
Martin Marco  
Martinec Tamas  
Martinec Tamás  
Martins Sérgio  
Martsum Thorbjørn Lund  
Meerkoetter Frank  
Meshcheriakov Ievgenii  
Miettinen Leena  
Mikolajczyk Piotr  
MingYang He  
Mohamed Fawzi  
Moiseev Boris  
Moskal Bartlomiej  
Mutz Marc  
Määttä Antti  
Nichols Andy  
Nikiforov Aleksei  
Nishihara Yuya  
Nordheim Mårten  
Nurmenniemi Sami  
Nurmi J-P  
Oikarinen Kari  
Oksa Tapio  
Ollila Kimmo  
Paeglis Gatis  
Palaraja Kavindra  
Park Cathy  
Parker Seth  
Pasion Jerome  
Passi Jukka  
Pelkonen Tuomo  
Peng Tang  
PengCheng Fan  
Persano Mauro  
Petroules Jake  
Petäjäjärvi Pasi  
Piccolino-Boniforti Marco A.  
Piippo Samuli  
Pocheptsov Timur  
Pohjanheimo Milla  
Poikelin Joni  
Pokrzywka Romain  
Pol Aleix  
Polak Karol  
Policht Michal  
Portale Alessandro  
Potter Lorn  
Powell Jeremy  
Project The Qt  
Qi Liang  
RIM Yuntaek  
Redondo David  
Reinio Topi  
Richter Florian  
Ritt Konstantin  
Rocha Andre de la  
Rocha André de la  
Rojas Antonio  
Rosenvik Niclas  
Rui Dong  
RuiJie Fan  
Rutledge Shawn  
Saario Toni  
Saether Jan Arve  
Sarajärvi Tony  
Schmertmann Lars  
Schwarzer Frederik  
Scott Craig  
Seemann Jochen  
Seiderer Peter  
Seo Siyeon  
Sera Luca Di  
Shachnev Dmitry  
Shaforostoff Nick  
Shaforostov Nick  
Shao Tianlu  
Shaw Alex  
Shaw Andy  
Shivashankar Venugopal  
Skoland David  
Smith Daniel  
Solovev Ivan  
Song WenTao  
Spencer Michael  
Srebrny Piotr  
Staikov Andrii  
Storsjö Martin  
Strømme Christian  
Suzuki Tasuku  
Svetkin Mikhail  
Sæther Jan Arve  
Sørvig Morten  
Sørvig Morten Johan  
Temirkhodjaev Nodir  
Tkachenko Ivan  
Trotsenko Alex  
Tuliniemi Jere  
Tushar Shantanu  
Tvete Paul Olav  
Uzumcu Furkan  
Valdmann Jüri  
Varanka Sami  
Varga Peter  
Vatra BogDan  
Vejdarski Martin  
Verbruggen Erik  
Verria Doris  
Vertriest Nico  
Vestbø Tor Arne  
Voelker Jannis  
Volgutov Valery  
Volkov Alexander  
Voutilainen Ville  
Vuolle Juha  
Wang ChunLin  
Wang Dongmei  
Welbourne Edward  
Wenhao Peng  
Wicking Paul  
Wolff Milian  
Wolff Oliver  
Wójcik Kama  
Xiang Zhang  
Xinwei Li  
Xuetian Weng  
Ya Zou  
YaoBing Xiao  
Yicun Wang  
Yong Zhang  
Yrjänä Marianne  
Yu Wang  
Yu Zhang  
Yuyin Yang  
Zahorodnii Vlad  
Zhang JiDe  
Zhao Yuhang  
Ziller Eike  
Zimmermann John  
hjk hjk  
