Release note  
============  

Qt 6.5 introduces many new features and improvements as well as bugfixes  
over the 6.4.x series. For more details, refer to the online  
documentation included in this distribution. The documentation is also  
available online:  
  
https://doc.qt.io/qt-6/index.html  
  
The Qt version 6.5 series is binary compatible with the 6.4.x series.  
Applications compiled for 6.4 will continue to run with 6.5.  
  
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
* eee9d25202 Use CSS classes on html list items for checkbox support  
Checkbox list items can now be read and written in both HTML and  
Markdown, including conversions.  
  
* 81fdfcfc4a Fix font rendering when Qt is configured with -no-harfbuzz  
Fixed font layouts when Qt was configured without Harfbuzz.  
  
* 992a318d39 CoreText: Fix fonts with synthetic stretch  
Fixed a bug where synthetically stretched fonts would get the wrong  
advances and sometimes glyphs would be clipped.  
  
* 79bead6c3b Add support for painting at integer DPR with downscale  
Added experimental support for always painting at an integer device  
pixel ratio (rounding the DPR up if necessary), followed by a downscale  
to the target DPR.Enable by setting QT_WIDGETS_HIGHDPI_DOWNSCALE=1 and  
QT_WIDGETS_RHI=1.  
  
* 122270d6be Long live the ICU-based QStringConverter interface!  
QStringConverter and API using it now supports more text codecs if Qt  
is compiled with ICU support.  
  
* 03e76ac23d xcb: fix missing initialization of m_cursor  
Fixed crash when no monitorInfo is available (e.g. VNC).  
  
* bf3fc5c95c QPromise: run continuation(s) on destruction  
QFuture now runs its continuations when its associated QPromise has  
been destroyed. Previously, if a QFuture was canceled because the  
associated QPromise has been destroyed, its continuations were skipped.  
  
* cb0b1ee441 moc: remove unnecessary emission of "#include  
<qbytearray.h>"  
moc no longer emits an #include for QByteArray in the output file. None  
of the content that moc generates needed that header, so this should not  
cause changes for most people. However, codebases that #include'd the  
moc output (something that is recommended) could be depending on this  
indirect include.  
  
* 2c0518eb62 moc: Allow reading property values through bindables  
You can now specify "READ default" in a Q_PROPERTY if you also specify  
a BINDABLE. moc will synthesize a READ accessor in that case.  
  
* 846b314aaf Emit autolinks in QTextMarkdownWriter  
QTextMarkdownWriter now writes an autolink whenever a hyperlink has no  
custom text and no tooltip, including when the document was parsed from  
Markdown containing a naked URL.  
  
* 7466422e9c Add a way to declare _exported_ logging categories  
Added the Q_DECLARE_EXPORTED_LOGGING_CATEGORY macro, in order to allow  
dynamic libraries to declare a logging category that can be then used by  
client code.  
  
* 9521a07af2 QKeySequenceEdit: add a maximumSquenceLength property  
Added a maximumSquenceLength property.  
  
* 217c47eac4 wasm: enable sql/sqlite for non threaded builds  
Enable sqlite for non threaded builds  
  
* c84897c137 QDebug: add op<< for std::initializer_list  
Can now stream std::initializer_list.  
  
* 1c0a56a2f3 Apply ScaleFactorRoundingPolicy to QT_SCREEN_SCALE_FACTORS  
The high-DPI scale factor rounding policy (settable with  
QGuiApplication::setHighDpiScaleFactorRoundingPolicy() or  
QT_SCALE_FACTOR_ROUNDING_POLICY) now applies to scale factors set with  
QT_SCREEN_SCALE_FACTORS.  
  
* cc70757964 qdbusxml2cpp: allow choosing <> over ""  
Added command line option -I/--global-include to include header files  
with <> in the generated files.  
  
* e1f25b1c8d Make it possible to check the accepted state of touch  
events in tests  
QTouchEventSequence::commit() now returns a bool so that tests can  
check whether the event was accepted during delivery.  
  
* 66a30b9a33 moc: Allow writing properties through bindables  
moc will now synthesize WRITE accessors for properties with BINDABLE if  
you specify "WRITE default".  
  
* 1d961491d8 Always update QPalette resolve mask, regardless of QBrush  
change  
Always update resolve mask in QPalette::setBrush, even if the value of  
brush has not changed.  
  
* 2cfabed1ff Long live QDebug op<< QMetaType!  
Can now stream QMetaType.  
  
* 1ea0d399b3 QKeySequenceEdit: Add a finishing key combinations property  
Added a property to allow defining the finishing key combinations.  
  
* 6bc227a06a Port QXmlStremReader to QAnyStringView  
Added constructor and addData() overloads taking QAnyStringView.  
  
* 43ef22045c Windows: Turn on dark mode support by default  
Dark mode, both for the window frames and for the palette, is now  
supported by default. It can be turned off (partially or entirely) by  
setting the QPA parameter "darkmode=0" (no dark mode support) or  
"darkmode=1" (darkmode support only for the window frames).  
  
* ccb2e4dbb1 QOpenGLBuffer: add move-SMFs and swap()s  
Added member-swap(), move constructor, move assignment operator.  
  
* 74fac865cf QMetaType: add registerType() and  
qRegisterMetaType(QMetaType)  
Added QMetaType::registerType() and an overload of qRegisterMetaType()  
taking QMetaType (the two functions do the same thing). These two  
functions ensure a given QMetaType is registered with the Qt global  
registry, so they can be found by name later. Using  
qRegisterMetaType<T>() also accomplishes the same thing, but is slightly  
better for completely generic code because it will avoid emitting the  
registration for built-in types.  
  
* 764d82ceb5 QMetaType: add is{Default,Copy,Move}Constructible and  
isDestructible  
Added isDefaultConstructible(), isCopyConstructible(),  
isMoveConstructible() and isDestructible().  
  
* 2d0c31e7d9 QMetaType: fix QMetaTypes for non-const references  
Made meta types for non-const references fail to compile. Previously,  
QMetaType::fromType allowed this to compile, but returned the meta type  
for the base type, which was incorrect. Const references are understood  
to be the same as the base type.  
  
* e540d4a864 QRegularExpression: introduce (global)matchView  
Added the matchView() and globalMatchView() functions that operate on  
string views. The match(QStringView) and globalMatch(QStringView)  
overloads have been deprecated.  
  
* 41c4f9a47a SQLite: Update SQLite to v3.39.2  
Updated SQLite to v3.39.2  
  
* 0a36a7c1db Make 'zz' format an alias for 'z' in time format strings  
Doubling the 'z' format in a date-time or time format string now  
produces the same output as a single 'z'. Previously, this would have  
produced two copies of the milliseconds field (eliding any trailing  
zeros in each). Contrast with 'zzz', which produces the full  
milliseconds field, including any trailing zeros.  
  
* 8cc389068b Improve QDomDocument::setContent() API  
Added new setContent() overloads that allow specifying different parse  
options through ParseOptions flags. These overloads use a new  
ParseResult struct for returning the information about an error, and  
QAnyStringView for passing string input.  
  
* 651092c218 Bump QVulkan(Device)Functions to Vulkan 1.3  
QVulkanFunctions and QVulkanDeviceFunctions are updated to expose the  
Vulkan 1.3 API as long as the build environment's vulkan.h is  
1.3-capable.  
  
* 26a73e1b31 QDomDocument: Add a way to enable spacing-only text nodes  
Spacing-only text nodes can now be preserved by passing the  
ParseOption::PreserveSpacingOnlyNodes option to setContent().  
  
* 9ce5709fb1 CMake: Support big resources in qt_add_resources  
The target-based variant of qt6_add_resource gained the option  
BIG_RESOURCES. This can be used instead of qt6_add_big_resources, which  
is not target-based.  
  
* 2ca3044083 Make QSqlQueryModel::query() return a reference to the  
const QSqlQuery  
QSqlQueryModel::query() now returns a reference to the const QSqlQuery  
object associated with the model.  
  
* c4fabe37b9 Remove QSqlTableModel::setQuery(const QSqlQuery &)  
The setQuery(const QSqlQuery &) method is removed, because QSqlQuery  
cannot be copied correctly. Use the public setQuery() overloads of the  
base QSqlQueryModel class instead. They allow passing of QSqlQuery by  
rvalue ref, or creation of the query by specifying query string and  
database object.  
  
* 042290d0fb CMake: Add QT_ANDROID_SIGN_AAB variable  
Added the QT_ANDROID_SIGN_AAB variable that can be set to ON to enable  
signing of .aab packages.  
  
* e163c49435 qdbusxml2cpp: remove the old "In"-for-signal compatibility  
code  
Removed the old compatibility code that accepted "In" annotations for  
signal argument names, introduced in Qt 5.8.  
  
* e684c25b85 QDomDocument: deprecate old setContent() overloads in favor  
of new ones  
Deprecated the old setContent() overloads in favor of the new ones that  
take ParseOptions and ParseError.  
  
* a6b55b3c46 Allow specify distance to plane for QTransform  
Added overloads to rotate() and rotateRadians() that allow specifying  
of the distance to the rotation plane.  
  
* 3226c82740 Rename QT_DISABLE_DEPRECATED_BEFORE ->  
QT_DISABLE_DEPRECATED_UP_TO  
The QT_DISABLE_DEPRECATED_BEFORE macro is renamed to  
QT_DISABLE_DEPRECATED_UP_TO. The old name is deprecated, but is still  
recognized if it is defined during configuration and the new name is not  
defined.  
  
* 18f0484a0e Rename QT_DEPRECATED_WARNINGS_SINCE ->  
QT_WARN_DEPRECATED_UP_TO  
The QT_DEPRECATED_WARNINGS_SINCE macro is renamed to  
QT_WARN_DEPRECATED_UP_TO. The old name is deprecated, but is still  
recognized if it is defined during configuration and the new name is not  
defined.  
  
* 2625a3a01a Add -disable-deprecated-up-to parameter to configure script  
The configure script now accepts a new parameter -disable-deprecated-  
up-to which is used to remove all deprecated code from API and ABI while  
building the libraries. The version number must be specified in a hex  
format. For example, it can be used like this:  /path/to/qt/configure  
-disable-deprecated-up-to 0x060500 to remove all code deprecated in Qt  
6.5.0 or earlier releases.  
  
* d8561b1dea QDebug: finish porting to qsizetype/size_t  
Fixed issues on 64-bit platforms when streaming containers (incl.  
strings) of more than 2Gi elements.  
  
* e1cf523354 QScopedArrayPointer: port to qsizetype  
Is no longer limited to 2Gi elements in size.  
  
* f5be5c6b14 Move qSharedBuild() from qglobal.h to qlibraryinfo.h  
qSharedBuild() is moved from qglobal.h to qlibraryinfo.h, '#include  
<QtCore/QLibraryInfo>' needs to be added where it's used.  
  
* 22662d7dba QLibraryInfo: Add isSharedBuild() function and deprecate  
qSharedBuild()  
Added QLibraryInfo::isSharedBuild() and deprecated qSharedBuild().  
  
* 9540a4eb90 QHttp2Configuration: in QNAM, use old, higher values in  
flow control  
Stream receive window that HTTP/2 protocol in QNAM is using increased  
to 214748364 octets (from the previous 64K) not to throttle download  
speed. Clients, working with servers, not accepting such parameters,  
must set HTTP/2 configuration on their requests accordingly.  
  
* 5c01cbfe76 Remove Q_DUMMY_COMPARISON_OPERATOR  
Removed the Q_DUMMY_COMPARISON_OPERATOR macro, which was needed to  
workaround outdated template instantiation rules on some outdated  
compilers.  
  
* c81d5ec19a QDBusTrayIcon: add xdg-activation support  
StatusNotifierItem tray implementation supports getting window focus  
token from desktop environments supporting the ProvideXdgActivationToken  
extension (e.g. KDE)  
  
* fe92b08065 QMetaObject: add a new, variadic  
invoke/invokeMethod/newInstance  
The QMetaObject::invokeMethod() taking a method name by string,  
QMetaObject::newInstance(), and QMetaMethod::invoke() now support more  
than 10 arguments.  
  
* f123212880 RCC: fix zlib compression when --no-zstd was specified  
Fixed a bug that caused rcc not to compress files with any compression  
algorithm if the --no-zstd option was present.  
  
* 50b05e3e2a Move qVersion() from qglobal.h to qlibraryinfo.h  
qVersion() is moved from qglobal.h to qlibraryinfo.h, '#include  
<QtCore/QLibraryInfo>' needs to be added where it's used.  
  
* 812a0d3125 QAnyStringView: construct from any T implicitly convertible  
to QString/QByteArray  
Can now be constructed from anything that implicitly converts to either  
QString or QByteArray.  
  
* 0380dd5051 QMetaObject: pass the QMetaTypes in variadic  
invoke/newInstance  
QMetaMethod::invoke(), QMetaObject::invokeMethod(), and  
QMetaObject::newInstance() are no longer limited to 10 arguments.  
  
* 9b6e79abbe Fix crash when setting override cursor on multiple clients  
Fixed a crash when setting an override cursor on multiple clients.  
  
* e6d3657f7f Update bundled libjpeg-turbo to version 2.1.4  
libjpeg-turbo was updated to version 2.1.4  
  
* 012132c60d xcb: use libxcb-cursor to replace Xlib/libXcursor  
Used libxcb-cursor to replace Xlib/libXcursor  
  
* aa99bf532d qdbusxml2cpp: modify the behavior of -m/--moc option  
The -m/--moc option now generates idiomatic moc file names  
(moc_base.cpp for headers, base.moc for implementation files)(was:  
always base.moc). Build systems using workarounds for the non-idiomatic  
naming of moc files used by qdbusxml2cpp in the past can now drop these  
workarounds for Qt versions >= 6.5.  
  
* 6abaff810a CMake: Collect IMPORTED library dependencies for android  
deployment  
Imported targets are now considered during Android deployment when  
using CMake 3.21+.  
  
* 66b633bbc1 Port QDir to qsizetype [3/3]: API  
The count() function now returns, and the indexing operator now takes,  
qsizetype (was: uint and int, respectively).  
  
* 542f837fa2 CMake: Clarify qt_deploy_runtime_dependencies' EXECUTABLE  
argument  
On non-macOS platforms, qt_deploy_runtime_dependencies' EXECUTABLE  
argument now expects the executable in the build directory instead of  
the installation directory.  
  
* 358248b495 Make QCryptographicHash move constructible  
Added move constructor, move assignment operator and swap() function.  
  
* cd37a773ca QCryptographicHash: Add getter for algorithm()  
Added getter algorithm().  
  
* 411b17150e Make time parsing accept zz as equivalent to z  
When parsing a datetime, the 'zz' format specifier is now equivalent to  
'z', as for serialization.  
  
* 27c91dbd36 macOS: Return false from set(Keyboard/Mouse)GrabEnabled  
QWindow::setKeyboardGrabEnabled() and QWindow::setMouseGrabEnabled()  
now returns false, as the feature is not implemented on macOS yet. If  
you were relying on these functions to make the window key (activate  
it), please use QWindow::requestActivate() instead.  
  
* 1b5462c2ac CMake: Introduce qt_deploy_translations  
Added qt_deploy_translations for deploying Qt translation catalogs in  
user projects.  
  
* 514027f43f CMake: Add NO_TRANSLATIONS option to deployment functions  
Added the NO_TRANSLATIONS option to qt_deploy_runtime_dependencies and  
qt_generate_deploy_app_script.  
  
* 22d4c67234 QObject: attempt to fix a deadlock introduced by an earlier  
fix  
Fixed a regression from 6.3 that caused QObject::isSignalConnected() to  
deadlock if called from inside disconnectNotify().  
  
* b62c3a8545 Document QAtomic testAndSet  
Documented new overloads of testAndSet() that were originally added for  
5.3.  
  
* 0462dba766 Skip early return from test loops during cleanup()  
During the cleanup() phase of a test, the QTRY_* macros and  
QTestEventLoop now ignore the test resolution, in contrast to when they  
are used from the test itself, which (since 6.3.0) exits the loops early  
if the test has failed.  
  
* 75d59c9502 Add QTest::currentTestResolved() and use in testlib  
Added QTest::currentTestResolved(), which is true if the test has  
failed or skipped. The QTRY_*() macros and QTestEventLoop now use this,  
rather than QTest::currentTestFailed(), to test whether they should stop  
looping, so that they also do so on a skip.  
  
* 633c136596 QCryptographicHash: implement OpenSSL 3.0 support  
Uses the OpenSSL 3.0 implementation now, where available.  
  
* e08f05ac6e QDebug: Support standard strings and string views directly  
QDebug now supports printing std::strings and std::string_views (and  
their wide, u16, and u32 variants) directly.  
  
* a51e7876b8 Revert "Keep original text for text/plain mime data"  
The fix to preserve special characters like &nbsp; the text/plain part  
of the clipboard when copied from a QTextEdit or QLineEdit had to be  
reverted (QTBUG-107004).  
  
* 0bc92c01e3 Support parsing time-zone specifiers more selectively  
hh:mm offset format (with colon), and 'tttt' matches an actual zone  
name. When used singly, 't' still matches anything the parser knows how  
to interpret as a zone specifier.  
  
* 18439a449f Support serializing time-zone fields in date-times more  
flexibly  
hh:mm, and 'tttt' gets the zone name. Previously, each 't' was replaced  
by another copy of the abbreviation.  
  
* 42b66bd809 QTaggedPointer: disable operator= with an empty initializer  
list  
The operator assignment taking a raw pointer has been reimplemented in  
order to avoid subtle issues when assigning `{}` to a QTaggedPointer.  
This will cause code that assigns a braced-init-list to a QTaggedPointer  
object to stop compiling (for instance, `tagPtr = {ptr}` is now ill-  
formed).  
  
* c9e19cf9d3 Move qurltlds_p.h out of src/network, and make it a .cpp  
file  
The Public Suffix List (PSL) data file got moved from  
src/network/kernel/qurltlds_p.h to src/3rdparty/libpsl/psl_data.cpp.  
  
* 30b881b394 qforeach.h: do not include qglobal.h  
The qforeach.h header no longer includes qglobal.h. If you relied on  
the transitive include, you may have to include qglobal.h explicitly.  
  
* fcd294a9ec QPrivateSignal: disable implicit conversions from  
initializer_list  
It is no longer possible to use `{}` to construct a QPrivateSignal  
object (specifically, QPrivateSignal's default constructor is now  
explicit). This means that emitting a signal that carries a  
QPrivateSignal argument (i.e. a "private signal") cannot any longer be  
done by using something like `emit aSignal({})`; instead, such usages  
must be ported to `emit aSignal(QPrivateSignal());` or equivalent.  
  
* fc76767692 Long live Q_UNREACHABLE_RETURN()!  
Added Q_UNREACHABLE_RETURN() macro.  
  
* 0f94430a0f testlib: make it possible to test double-clicks with  
discrete events  
QTest::mouseRelease() and mouseClick() can now be used to test double-  
clicks, by specifying a realistic timestamp delay.  
  
* 2742ceb1cd Update bundled libpng to version 1.6.38  
libpng was updated to version 1.6.38  
  
* 6ba003f732 Freetype: Fix transforming bitmap fonts  
Fixed an issue with the Freetype backend where rotations would not be  
applied correctly to bitmap fonts.  
  
* bb1f616ff1 Add flicking behavior hints to platform integration and  
theme  
Added platform FlickStartDistance, FlickMaximumVelocity and  
FlickDeceleration hints for the benefit of QtQuick Flickable  
  
* bbad6440ae Ensure proper format of Info.plist  
Fixed handling binary Info.plist files in generated Makefiles by always  
converting them to XML before substituting placeholders.  
  
* 3158068209 Fix generating PDFs with DirectWrite engine  
Fixed glitches in generated PDFs when the DirectWrite backend was in  
use, e.g. when high-dpi scaling was active.  
  
* cdd7163c60 macOS: Fix synthetic bold on scaled painters  
Fixed an issue with synthetic bold on fonts when the painter had a  
scale  
  
* 77eef32917 QLibrary: fix loading multiple versions of a library  
Fixed a bug that caused QLibrary to be unable to load two different  
versions of a library of a given name at the same time. Note that this  
is often inadviseable and loading the second library may cause a crash.  
  
* 65279d6e9d macOS: Fix less common writing systems on Catalina and  
later  
Fixed missing text with certain writing systems on macOS Catalina and  
later.  
  
* bb18767af1 Add QNativeInterface::QWaylandApplication  
Add QNativeInterface::QWaylandApplication that allows to access central  
native wayland objects.  
  
* 54c959643e Add Qt plugins to the dependency list with their  
dependencies  
All plugins that belong to the Qt modules that are linked to the  
Android application are now deployed with their dependencies.  
androiddeployqt tries to find and resolve plugin dependencies implicitly  
instead of skipping plugins with dependencies that are not resolved  
explicitly in the user project.  
  
* 2625e5f050 Make the `PREFIX` Parameter of the `qt_add_resources`  
Optional  
The `PREFIX` parameter of the `qt_add_resources` is now optional. If  
not passed, and `QT_RESOURCE_PREFIX` is not defined, `/` will be used as  
the path prefix.  
  
* e1089e0520 QBenchlib/Perf: don't try to benchmark the kernel  
Fixed support of Linux performance counters for QBENCHMARK, which used  
to fail with "Permission denied" errors in default configurations. Now,  
QtTest will automatically fall back to profiling only userspace, like  
the perf(1) tool does.  
  
* 209adad078 QBenchlib/Perf: remove the handling of attributes in  
-perfcounter  
Specifying attributes with the -perfcounter command- line option for  
Linux performance counters is deprecated. QtTest will ignore the colon  
and any attributes listed there, though future versions of QtTest may  
reintroduce attributes if needed.  
  
* 365904085e QFile: make constructors taking a path explicit  
The QFile constructors that take a path are going to become  
unconditionally `explicit` in Qt 6.9. Code like `QFile f = "/path";`  
will need to be ported to equivalent one (e.g. `QFile f{"/path/"}`).  
This has been done in order to prevent a category of mistakes when  
passing strings or paths to functions that actually take a QFile. Users  
can opt-in to this change even before Qt 6.9 by defining the  
QT_EXPLICIT_QFILE_CONSTRUCTION_FROM_PATH macro before including any Qt  
header.  
  
* fa4c8fa71a SQLite: enable default features for the built-in version  
SQLite shipped with Qt now supports FTS4, the mathematical functions  
and the Geopoly interface.  
  
* 703ac911f9 Make sure that the generated dbus sources get extra  
compiler flags  
The internal DBus source files that are generated, now are compiled  
with the same set of compilation flags and options as other source files  
of the Qt module.  
  
* fb4bc5fa26 QHash: tame HasQHashSingleArgOverload ODR violations  
Support for overloads of qHash with only one argument is going to be  
removed in Qt 7. Users are encouraged to upgrade to the two-arguments  
overload. Please refer to the QHash documentation for more information.  
  
* 971bd702ef Make QDialog respect Qt::AA_DontUseNativeDialogs  
QMessageBox now respects the Qt::AA_DontUseNativeDialogs application  
attribute to opt out of native message boxes on platforms where this is  
supported (iOS, Android).  
  
* 9d16d5e224 a11y: Add new QAccessibleSelectionInterface  
Added new preliminary QAccessibleSelectionInterface that can be used to  
expose selections to assistive technology.  
  
* a47c7a9826 macOS: Add dialog helper for native message boxes  
Message boxes such as QMessageBox now follow the platform look and feel  
by using native dialogs if possible.  
  
* 4d84843822 QString, QByteArray: add removeAt/First/Last() convenience  
methods  
Add removeAt/First/Last() convenience methods to QString and QByteArray  
  
* 649dccf57b Reintroduce converter APIs for supporting native clipboard  
formats  
Reintroduced to allow applications to add support for conversion from  
and to Windows-native clipboard formats to MIME-encoded data.  
  
* d9637d0781 QString: don't detach in removeStringImpl()  
Improved the performance of QString::remove() by avoiding unnecessary  
data copying. Now, if this string is (implicitly) shared with another,  
instead of copying everything and then removing what we don't want, the  
characters from this string are copied to the destination, except the  
ones that need to be removed.  
  
* f678893f8a Update bundled zlib to version 1.2.13  
zlib was updated to version 1.2.13.  
  
* ee2dbcada8 Add support for stereoscopic content in QOpenGLWidget  
Added support for stereoscopic rendering.  
  
* f6fefbc6ca Update bundled libpng to version 1.6.39  
libpng was updated to version 1.6.39  
  
* 715a6c3908 iOS plugin: Add native color dialog  
Added native color dialog support for iOS.  
  
* 4fb96669e3 QBindable: Make ordinary Q_PROPERTYs bindable  
Q_PROPERTYs without BINDABLE can be wrapped in QBindable to make them  
usable in bindings  
  
* 60968090ad Update -redo option such that it removes CMakeCache.txt and  
CMakeFiles/  
The -redo option now additionally removes existing CMakeCache.txt file,  
and CMakeFiles/ directory, and recreates them from scratch.  
  
* 84c76d6205 CMake: Make it possible to specify a debug MySQL client  
library  
If pkg-config is not used, a debug build of the MySQL client library  
can be specified with -DMySQL_LIBRARY_DEBUG=<path-to-library>. The debug  
and release variants of the library are automatically detected. Setting  
MySQL_ROOT and MySQL_LIBRARY_DIR is sufficient in most cases.  
  
* 5d41ec46e9 QString/QByteArray: de-pessimize op+ [1/2]: non-const  
return types  
operator+ no longer returns a const object, enabling move-semantics on  
the return value, but also hidden detaches.  
  
* c450f6d21c Support stereoscopic rendering with QGraphicsView  
Added support for stereoscopic rendering.  
  
* b977ae371a Add In-place utf-8 case-insensitive comparisons  
Added utf-8 case-insensitive comparisons  
  
* 443af8cd45 iOS plugin: Add native font dialog  
Added native font dialog support for iOS.  
  
* 7e4c7d50a7 Add QGuiApplication API to set a number-badge in the  
Dock/task bar  
Added QGuiApplication::setBadgeNumber() to inform the user about e.g.  
the number of unread e-mail or queued tasks. The badge will be overlaid  
on the application's icon in the Dock on macOS, the home screen icon on  
iOS, or the task bar on Windows.  
  
* d2e1d73bf1 QString: overload append to accept QUtf8StringView  
Added append(QUtf8StringView) overload.  
  
* 2ffdb3bcdd QString: overload the += operator to handle QUtf8StringView  
Added operator+=(QUtf8StringView) overload.  
  
* f046589e14 QString: overload insert with QUtf8StringView  
Added insert(QUtf8StringView) overload.  
  
* f192ddad8b QString: overload prepend with QUtf8StringView  
Added prepend(QUtf8StringView) overload.  
  
* eb63f2eb05 QMessageLogger: make qFatal categorized and streamable  
QMessageLogger::fatal now supports categorized logging, for instance  
using the qCFatal(category) macro. Moreover, qFatal() and qCFatal() now  
support streaming of values to be printed in the fatal message.  
  
* c9d991de1f Fix missing text when Harfbuzz fails to shape a substring  
Fixed a regression which would sometimes cause text to disappear if the  
string contained an unmatched variation selector character.  
  
* d77ce33082 Move Some of the Private CMake Helper Scripts from `bin/`  
to `libexec/`  
The private Qt CMake scripts, i.e., qt-configure-module, qt-cmake-  
private, qt-cmake-private-install.cmake, qt-cmake-standalone-test and  
qt-internal-configure-test were moved into $prefix/libexec on Unix  
platforms.  
  
* d8abcc969b Remove the deprecated TYPE option from qt_add_plugin  
The deprecated TYPE option of the qt_add_plugin() has been removed. You  
can specify the plugin type using the PLUGIN_TYPE option instead.  
  
* 6631444eb1 QString/QByteArray/QList: de-pessimize op+ [2/2]: overload  
on rvalue LHS  
Chained additions (a + b + c) now produce only one temporary buffer for  
the whole expression instead of one per addition. Using += or  
QStringBuilder is still faster, though.  
  
* e4851fedd4 Move qVersion() into it's own header  
Remove the entry for qVersion() being moved to qlibraryinfo.h.  
  
* 3fedcd4e4a Add Boyer-Moore Latin-1 string searcher with optional case  
sensitivity  
Added Boyer-Moore Latin-1 string searcher with optional case sensitivity  
  
* 46d1897267 CMake: Un-TP QT_RESOURCE_ALIAS  
The Core CMake QT_RESOURCE_ALIAS property is out of Technical Preview  
status.  
  
* a873979eb9 CMake: Un-TP most of the deployment API  
The Core CMake deployment API is out of Technical Preview status.  
  
* 41a994db06 QAnyStringView: add substringing operations  
Added substring functions sliced(), first(), last(), chop()/chopped(),  
truncate().  
  
* 536e173728 QNetworkRequest: Make header parsing locale-independent  
Fixed a bug where certain QNetworkRequest::KnownHeaders wouldn't be  
recognized as such in certain locales.  
  
* be05bb749e QNetworkAccessManager: Configurable number of HTTP1 TCP  
connections  
New class.  
  
* ae6186c7e8 Adapt QTimeZone to handle Qt::TimeSpec machinery  
QTimeZone is now always defined; feature timezone now controls most of  
its prior API and some new API is added, most of it always present, to  
enable QTimeZone to package a Qt::TimeSpec and, for Qt::OffsetFromUTC,  
its offset. Prior to this change, APIs using Qt::TimeSpec had to provide  
a separate function taking a QTimeZone alongside a function taking a  
Qt::TimeSpec and optional offset; it will now be possible to unify these  
into a single function taking a QTimeZone. Adaptation of other Qt  
classes to do so shall follow.  
  
* f46c18c627 Adapt QDateTime to route QTimeSpec uses via QTimeZone  
All QDateTime APIs involving a Qt::TimeSpec can now be routed via  
QTimeZone's lightweight time description support, saving the need to  
have different code paths for different time specs. In the process,  
QDateTime gains a timeRepresentation() method to return a QTimeZone  
reporting the (possibly lightweight) time description it uses. (The  
older timeZone() method always returns a non-lightweight QTimeZone,  
whose timeSpec() is Qt::TimeZone.)  
  
* e71099989e Add QDateTime::currentDateTime(const QTimeZone &)  
currentDateTime() now accepts a QTimeZone parameter to select the time  
representation to use for the result.  
  
* 585f2a31c6 QXmlStreamWriter: port API from QString to QAnyStringView  
Ported API to QAnyStringView (was: QString).  
  
* 074a4e16a3 Windows: Enable dark mode system palette by default  
Qt applications that use a style that supports dark mode rendering  
(such as the classic Windows or Fusion styles) will respect the dark  
appearance setting on Windows. Applications that use the Vista style,  
which doesn't support rendering in dark mode, will use the light system  
palette. On dark mode systems, the window frame will be dark if the  
palette is dark.  
  
* 58907dfa81 Try to match variant-selector font to preceding character  
Fix some cases where a variation-selector character would be ignored in  
font selection and the correct variant of a character would thus not be  
selected.  
  
* c3688e23a0 Return qt-configure-module to bin/  
Upon further consideration, qt-configure-module was deemed user-facing,  
and was thus moved back to ./bin on all platforms.  
  
* d37ef31674 Don't hide object replacement char except in rich text  
The object replacement character (U+FFFC) is now only filtered out in  
rich text controls, where they represent inline objects. In other  
controls, its glyphs will be shown as with other text.  
  
* 7f6e5d4748 SQLite: Update SQLite to v3.40.0  
Updated SQLite to v3.40.0  
  
* 7a850fc00c QT_INLINE_SINCE: never inline for static Qt builds  
Restored binary compatibility for static Qt builds broken by the  
QT_INLINE_SINCE mechanism. Qt still does not guarantee BC for static  
build configurations otherwise.  
  
* 1a4eca9e88 Add QCryptographicHash::supportsAlgorithm() to check  
supported algorithm  
Add supportsAlgorithm() method that can be used to query OpenSSL and  
check whether the selected algorithm is supported.  
  
* 124a8b6cdb windows: Fix vertical metrics with GDI engine  
Fixed an issue where the line gap of some fonts would be included twice  
in the font's leading.  
  
* 90384f4d86 QTest::WatchDog: fix missing timeout resets on test  
function change  
Fixed a bug which caused QTEST_FUNCTION_TIMEOUT to be applied to the  
whole test execution, as opposed to each test function.  
  
* 56ae42964e PCRE2: upgrade to 10.42  
PCRE2 has been updated to 10.42.  
  
* db61f95a31 SQLite: Update SQLite to v3.40.1  
Updated SQLite to v3.40.1  
  
* 65d011fe68 Move QTypeInfo<std::pair> from qpair.h to qtypeinfo.h to  
avoid ODR violation  
The QTypeInfo for std::pair/QPair will now be correct even if qpair.h  
hasn't been included, fixing an One-Definition-Rule (ODR) violation.  
  
* ed739a5c42 QUnicodeTools: Use thread-safe libthai API  
Correct line wrapping of Thai text now requires libthai version 0.1.25  
or above.  
  
* 3edf3d0730 Move QApplication::autoSipEnabled() to public scope  
bool QApplication::autoSipEnabled() is no longer a slot. Code such as  
using QObject::connect() to connect to it as a slot or accessing it  
through meta object system will have to be rewritten.  
  
* a0f953f019 Slow Deprecation of FILENAME_VARIABLE, replacement by  
OUTPUT_SCRIPT  
The FILENAME_VARIABLE option of qt_generate_deploy_script and  
qt_generate_deploy_app_script is now deprecated, use OUTPUT_SCRIPT  
option instead.  
  
* ddde19129c Object to creating duplicate entries in a test-data table  
Duplicate data tags are now warned about. Every call to QTest::newRow()  
or QTest::addRow() should result in a distinct data tag. If they do not,  
a warning is produced. Likewise, duplicate column names are forbidden;  
each call to QTest::addColumn() should use a distinct name.  
  
* 88689368d9 QMimeDatabase: don't stat() something that isn't a local  
file  
Fixed a regression from 6.4.0 that made certain QMimeDatabase functions  
that inspected file contents to fail on Unix systems, if the file was  
not a native file (e.g., a Qt resource).  
  
* 80a6048ab1 QStandardPaths/unix: ignore relative paths in all $XDG_*  
env vars  
Improved conformance to the Freedesktop basedir spec by ignoring any  
relative paths in XDG_* environment variables.  
  
* a44b695026 Don't do font merging for PUA characters  
Font merging (automatic assignment of alternative fonts) is no longer  
applied for characters in the Private Use Areas of Unicode.  
  
* 0cbc91d65d QVarLengthArray: clear() is not resize(0)  
clear() no longer requires the value_type to be default-constructible.  
  
* d656fde77e Update bundled libjpeg-turbo to version 2.1.5  
libjpeg-turbo was updated to version 2.1.5  
  
* 56909fb936 Windeployqt: add custom qml output directory command line  
option  
Windeployqt's default behavior is now to deploy qml imports to a "qml"  
directory inside the deploy directory, rather than directly to the  
deploy directory.  
  
* f594bc5afe qdoc: Add *.webp as an default image suffix  
*.webp has been added to the list of default image suffixes.  
  
* f59731b4fb qstrncpy: NUL-terminate even when src is nullptr  
Now NUL-terminates the target buffer even when the source pointer is  
nullptr, provided the target buffer has space for at least one byte.  
  
* b0d395e27c Text: fix Soft hyphen rendering in QTextLayout::glyphRuns()  
Fixed an issue where spaces would sometimes be shown in soft hyphen  
positions in a string.  
  
* 6d971d01b3 QFileSystemWatcher/Win: remove the pre-QFileInfo path  
normalization  
Fixed a bug that prevented removePaths() from removing the root of a  
drive on Windows.  
  
* dd7575b5f0 CMake: Fix position independent code linker flags not being  
set  
Qt tools are now built with position independent code even with Unix  
toolchains where this is not the default, for example clang.  
  
* d8a87b6942 Remove qmake files that provide support for building Qt  
modules  
Support for building Qt modules with qmake was removed.  
  
* 9a1a7e4965 SQLite: Update SQLite to v3.41.0  
Updated SQLite to v3.41.0  
  
* dcf7247e05 QErrorMessage: Reset 'again' check box between each error  
message  
QErrorMessage will now reset the check box for showing a message again  
for each new message shown, as each individual message has its own  
suppression state.  
  
* dbf4d319f0 SQLite: Update SQLite to v3.41.1  
Updated SQLite to v3.41.1  
  
### qtsvg  
* 5019037 QSvgGenerator: introduce a way to make it output SVG 1.1  
QSvgGenerator is now prepared to produce SVG 1.1 documents. This will  
enable QSvgGenerator to support more SVG features in the future, such as  
SVG clip paths. Please note that the actual feature set supported by  
QSvgGenerator is still very limited; extensive testing is recommended.  
  
### qtdeclarative  
* a72b4cd733 TestCase: add API for checking for polish at window level  
Added waitForPolish() and made isPolishScheduled() also take a Window,  
making it possible to verify that updatePolish() was called on one or  
more items managed by a window.  
  
* 8e0672da66 Add support for separate blending factors in  
QSGMaterialShader  
When a custom material declares its own blending factors, it is now  
possible to specify the source/destination alpha blending factors  
separate from the color blending factors. This is done by first setting  
the separateBlendFactors to true in  
QSGMaterialShader::GraphicsPipelineState, and then writing the desired  
values to srcAlpha and dstAlpha, in addition to srcColor and dstColor.  
  
* 175dfd25c2 Fix TextEdit/TextArea mouse cursor shape handling logic  
TextEdit and TextArea now set their own mouse cursors more  
consistently, but without regard for any external call to setCursor().  
  
* 6aad465f08 Introduce a sane resource path to qt_add_qml_module  
The AUTO_RESOURCE_PREFIX option was added to qt_add_qml_module(). It  
places your QML modules in the otherwise reserved resource directory  
/qt/qml. This directory is also added to the default QML import path. By  
using it you don't have to specify custom import paths anymore.  
Specifying neither AUTO_RESOURCE_PREFIX nor an explicit RESOURCE_PREFIX  
will generate a warning now because such QML modules are likely  
invisible in the resource file system.  
  
* 83a306f7d8 QQuickAbstractDialog: emit rejected() on mere close()  
QtQuick dialogs now emit rejected() on a mere close(), too.  
  
* cdcc41c8c1 Ensure QmlAttached attribute does not leak into derived  
types in C++  
Attached properties are only accessible from classes directly decorated  
with the QML_ATTACHED macro. Derived classes cannot inherit attached  
properties. Classes attached using the old way (via QQmlTypeInfo) are  
unchanged.  
  
* 42e3acaf9a Ensure QmlSingleton attribute does not leak into derived  
types in C++  
Classes decorated with the QML_SINGLETON macro will stop passing on the  
QML_SINGLETON functionality to their subclasses.  
  
* 3ab408da5d Ensure QmlForeign attribute does not leak into derived  
types in C++  
Classes decorated with the QML_FOREIGN macro will stop passing on the  
QML_FOREIGN functionality to their subclasses.  
  
* 80166d58a1 Fix SplitView containmentMask hit testing  
SplitView now correctly handles mouse events when using  
containmentMask.  
  
* 79f9e22ef7 Do not store instantiation errors in QQmlComponent  
Setting properties via createWithInitialProperties() and  
setInitialProperties() no longer affects the QQmlComponent's error state  
unless there are unset required properties. A warning is issued when a  
property could not be set.  
  
* 2483ffa011 Let Controls inherit palettes and fonts from parents  
Controls now inherit palette and font from parents.  
  
* 43b7daa1f7 qmldom: add support to dump a QML file's syntax tree  
Add support to dump AST of a QML file  
  
* 7e6db64d43 Deal with markdown fragments in TextEdit  
TextEdit.insert(), append(), copy(), paste() etc. are now working with  
MarkdownText.  
  
* 2cf1b290d7 CMake: Remove support for the deprecated CLASSNAME keyword  
The deprecated CLASSNAME argument of qt_add_qml_module has been removed  
in favor of CLASS_NAME.  
  
* 97cc7023ce Fix fractional scaling of text in Qt Quick  
Fixed a kerning issue with native-rendered text when there is a  
fractional system scale factor set.  
  
* 7e4b179430 Implement array methods for QQmlListProperty  
QQmlListProperty behaves like a JavaScript Array now. You can use  
map(), reduce(), forEach() etc on it. This also includes a slight change  
of behavior to the push() method. push() now returns the new list  
length, and it checks the length to not exceed UINT_MAX.  
  
* 650342de79 TextInput/Field: selectByMouse default=true, but not on  
touchscreens  
The selectByMouse property is now enabled by default, but no longer  
enables selecting by dragging your finger across text on a touchscreen.  
Platforms that are optimized for touchscreens normally use special text-  
selection handles, which interact with Qt via QInputMethod.  You can opt  
out of the behavior change by using an import version < 6.4.  
  
* e814ff1e86 QML: Support negative values in enums  
It is now possible to use negative integers as values for QML enum  
declarations.  
  
* 90d3fac73a TextEdit: selectByMouse default=true, but not on  
touchscreens  
The selectByMouse property is now enabled by default, but no longer  
enables selecting by dragging your finger across text on a touchscreen.  
Platforms that are optimized for touchscreens normally use special text-  
selection handles, which interact with Qt via QInputMethod.  You can opt  
out of the behavior change by using an import version < 6.4.  
  
* 34d52f8b2c qmllint: Implement module linting  
Individual modules can now be linted via the -M option  
  
* aa553318d4 Fix precedence between JS and QML scopes  
The precedence between imports and locally defined functions and  
variables in JavaScript files has been fixed. If you import a JavaScript  
file from a QML file, the functions inside the JavaScript file should  
obviously override anything imported from the QML context. This behavior  
has been restored.  
  
* dcbea32105 sg: Expose the projection matrix on the QSGRenderNode  
itself  
Added a projectionMatrix() accessor to QSGRenderNode.  This way a  
reimplemented prepare() can query both matrices and can load the final  
modelview-projection matrix into a uniform buffer for example.  
Previously this was only possible in render() because the projection  
matrix was only exposed in the RenderState. With QRhi, or modern APIs  
such as Vulkan, that is not quite sufficient since it is more than  
likely that one will want to calculate and store the matrix in  
prepare(), not in render().  
  
* b201b1d0b3 Fix error when calling byteLength on detached ArrayBuffer  
ArrayBuffer.byteLength() now returns 0 on detached ArrayBuffers,  
conforming to ECMAScript 2021.  
  
* 88aef52989 CMake: Place *_qmllint* targets into a separate FOLDER  
Introduced the QT_QMLLINTER_TARGETS_FOLDER global property to specify  
the name of the FOLDER for qmllint-related targets.  
  
* 3ebb3540df TextArea: selectByMouse default=true, but not on  
touchscreens  
The selectByMouse property is now enabled by default, but no longer  
enables selecting by dragging your finger across text on a touchscreen.  
Platforms that are optimized for touchscreens normally use special text-  
selection handles, which interact with Qt via QInputMethod. You can opt  
out of the behavior change by setting the environment variable  
QT_QUICK_CONTROLS_TEXT_SELECTION_BEHAVIOR=old.  
  
* 42848bda5c Fix TextInput and TextField mouse/touch selection fallback  
behavior  
The selectByMouse property is now enabled by default, but no longer  
enables selecting by dragging your finger across text on a touchscreen.  
Platforms that are optimized for touchscreens normally use special text-  
selection handles, which interact with Qt via QInputMethod.  You can opt  
out of the behavior change by setting the environment variable  
QT_QUICK_CONTROLS_TEXT_SELECTION_BEHAVIOR=old.  
  
* 7673a4d117 Add BoundaryRule.returnedToBounds signal  
BoundaryRule now has a returnedToBounds signal.  
  
* b6cf0672e6 Allow limited extensions to globals  
The JavaScript global objects are not frozen anymore in a QML engine.  
Instead, they are selectively locked. You can extend the objects with  
new members as long as you don't shadow any existing methods, and you  
can change or override data members. This also means that most methods  
of Object.prototype, which was previously exempt from the freezing,  
cannot be changed anymore. You can, however, change or override  
constructor, toString(), toLocaleString() and valueOf() on any  
prototype. Those are clearly meant to be overridden by user code.  
  
* 7fe4c9bb27 Add live property to QQuickItem layer  
Added live property to QQuickItem layer.  
  
* 205e31df16 DA: ignore disabled HoverHandlers when delivering hover  
events  
Disabled hover handlers will no longer receive hover events, or block  
siblings from being hovered.  
  
* 85ba26c644 QuickControls2: implement icons for submenus  
Now it's possible to set icon for Menu. This is useful for submenus, so  
icon will be displayed as for regular menu items.  
  
* 331e2effa7 Make basic render loop use a dedicated QRhi per window  
The 'basic' render loop has been changed to use a dedicated graphics  
context/device for each window. This is identical to the commonly used  
'threaded' render loop's behavior. This should not lead to any changes  
in rendering or visual appearance, but is expected to correct a number  
of lower level issues that tend to arise due to not having control over  
the context/device on a per-window basis.  
  
* 8ebdbf5c85 Avoid context truncation when filename has multiple dots  
The translation context in QML files has been changed to be in line  
with lupdate: Instead of using only the baseName(), completeBaseName()  
is now used.  
  
* d8066adc55 qml: deprecate top-level components  
QQmlComponents in qml document roots or in inline component roots are  
deprecated. Types defined in qml documents or in inline components are  
automatically wrapped into QQmlComponents when needed: those types  
really should not be inside a Component{}.  
  
* f3e72cfc0d QQuickTableView: add API to set section sizes explicitly  
Additional API for setting explicit row-, and column sizes has been  
made available.  
  
* 49b9f1f1e8 Make QQuickAttachedPropertyPropagator public  
Added QQuickAttachedPropertyPropagator, which provides a way to  
propagate attached properties from parent objects to children. This is  
especially useful when creating your own style.  
  
* d3f2c6ac42 Add TapHandler.exclusiveSignals to enable single/double tap  
exclusivity  
TapHandler.exclusiveSignals now lets you make the singleTapped and  
doubleTapped signals exclusive.  
  
* a824a6f060 Recursively write back value types and sequences  
You can now assign to properties of nested value types and to elements  
of containers from QML functions. You cannot, however, take references  
of such values and elements. This is in contrast to non-nested value  
types and the containers themselves. However, passing references of  
value types and containers around generally leads to very confusing  
effects. Don't do this.  
  
* 61a9612f5b MouseArea: don't get stuck in pressed state when disabling  
in press  
When a MouseArea becomes effectively disabled due to a parent's enabled  
property being set false while the mouse is pressed, the press will now  
be canceled.  
  
* ab52e47820 Locale: add toString functions  
Added toString() overloads.  
  
* 453469c9dc Maintain relative stacking order of popups  
When showing a popup that doesn't have an explicit z value set and is a  
child of the current top popup, then the popup's item's z value will be  
set to the z-value of the current top item.  
  
* 0bb7b2e932 Allow OS-synthesized right clicks to be delivered  
In case your operating system synthesizes a right-click from a  
touchscreen long-press, synthetic right-button mouse events are now  
delivered normally, so that e.g. TapHandler can react. You can opt out  
by setting QT_QUICK_ALLOW_SYNTHETIC_RIGHT_CLICK=0.  
  
* 649151bdcc QQuickNinePatchImage: fix aliasing by respecting the smooth  
property  
The Imagine style now supports smooth scaling for 9-patch images when  
the QT_QUICK_CONTROLS_IMAGINE_SMOOTH environment variable is set to 1.  
  
* a0290dcc53 QML: Fix precedence between imports  
The precedence of imports that expose different types for the same name  
has changed. Previously the algorithm was rather confused. Now, the rule  
of thumb is that more direct imports override more indirect ones. That  
means QtObject imported directly from QtQml is of higher precedence than  
QtObject imported from QtQml via QtQuick. Where that still leaves  
ambiguities, imports later in the document override imports earlier in  
the document. Any explicit imports and their dependencies always  
override the implicit import and its dependencies.  
  
* 8733b01ce3 QQuickTableView: implement support for letting the user  
resize rows and columns  
Added resizableColumns and resizableRows properties to enable resizing  
by dragging between cells.  
  
* 74873324bd QQuickItem: avoid emitting signals during destruction  
QQuickItem no longer emits change notifications for the parent,  
children, visible, and visibleChildren properties while it is being  
destroyed.  
  
* 17318c4805 QQuickDrag: correctly support text and image mime types  
The attaching type Drag supports more mime types in the mimeData  
property, which is now of type 'variantlist' instead of 'stringlist'. Qt  
Quick Drag validates the type of the data against supported mime types,  
and generates warnings in case of a mismatch. If the type of the data is  
ArrayBuffer (i.e. a QByteArray), then the data is accepted without any  
validation.  
  
* 1fc939a870 QML: Faithfully convert undefined and null to string  
qjsvalue_cast<QString>(x) now returns "undefined" for undefined JS  
values, and "null" for null JS values. This is in line with what  
QJSValue::toString() does, and also what JavaScript itself would produce  
when stringifying such values. Previously, qjsvalue_cast would return an  
empty string for both, undefined and null JS values.  
  
* 7fa4a53ebb QQuickTableView: add tab support  
Added support for navigating the current index using Tab and Backtab.  
  
* 9dc305379b Android: Set EnterKeyNext as default type for TextInput  
EnterKey type is now changed from EnterKeyDefault to EnterKeyNext for  
virtual keyboard in TextInput. It is done only if the focus can be moved  
to QQuickItem below, so the activeFocusOnTab need to be set.  
  
* 4ba7810a6a CMake: Add NO_TRANSLATIONS to  
qt_generate_deploy_qml_app_script  
Added the option NO_TRANSLATIONS to qt_generate_deploy_qml_app_script.  
  
* 2b0f5f9e61 Material: add roundedScale attached property  
Added roundedScale attached property, which can be used on certain  
controls to change the radius of their rounded corners.  
  
* 0925c51c59 QJSEngine: Optimize conversion from QObject* to QString  
You can implement custom toString() methods for your QML objects in  
JavaScript or in C++. Those methods don't actually have to return a  
string. Previously, whatever return value the method generated was  
forwarded as-is. Now it is coerced to a string.  
  
* 46429839fe QtQml: Restructure the module  
If you import QtQml you now need to make sure that QtQml is actually in  
the import path. Usually this is the case, but by manipulating the  
import path you can hide QtQml. In previous versions of Qt you could  
then still import QtQml because its types are present in the QtQml  
library. However, it would ignore its dependencies: QtQml.Models and  
QtQml.WorkerScript. If you really want to import only the builtins, you  
can always "import QML".  
  
* 6656567a40 Introduce type based overload of Qt.createComponent  
Qt.createComponent now supports creating a Component from its module  
and type name (passed as strings).  
  
* d1b9a4cacf QQuickItem: Fix effective visibility for items without  
parent  
The visible property of Items without a parent now always returns  
false, and the visibleChanged signal gets emitted when the parent item  
of a visible item becomes null.  
  
* ed83f0f795 QQuickTableView: implement TableView.editDelegate  
Added support for editing cells  
  
* 3f4856dbca Introduce QQmlApplicationEngine::loadFromModule  
It is now possible to load QML types via their module and type name.  
  
* e592a2ad31 Warn users when they customize native styles  
Customization of native styles will now result in warnings. Non-native  
styles (such as Basic) should be used for customization purposes, or a  
custom style. If you are aware of the risks and still want to customize  
these controls, you can ignore the warnings by setting  
QT_QUICK_CONTROLS_IGNORE_CUSTOMIZATION_WARNINGS to 1.  
  
* b12c7ca751 QQuickTableView: add layoutChanged() signal  
Added new signal 'layoutChanged()'  
  
* 373b6e54dd Add {horizontal,vertical}StretchFactor  
Added support for stretch factors  
  
* 52cbcd947d QQuickTableView: support multi-selection  
Added multi-selection support if using a SelectionRectangle and holding  
down the shift-modifier.  
  
* 21bf976a41 QQuickTreeViewDelegate: implement edit delegates  
TreeViewDelegate got support for editing nodes in the tree.  
  
* 4a11f077f0 CMake: Un-TP qt_generate_foreign_qml_type and  
qt_query_qml_module  
The qml CMake commands qt_generate_foreign_qml_type and  
qt_query_qml_module are out of Technical Preview status.  
  
* 7867a683fc Add PinchHandler.scaleAxis, rotationAxis; hold values in  
axes  
PinchHandler now has scaleAxis and rotationAxis grouped properties,  
alongside the existing xAxis and yAxis; and all of these now have  
activeValue and persistentValue properties. The activeValueChanged  
signal includes a delta value, giving the incremental change since the  
previous activeValue. The persistentValue is settable, in case some  
target item property can be adjusted in multiple ways: the handler's  
stored value can then be synced up with the item property value after  
each external change. These features are also added to DragHandler's  
xAxis and yAxis properties.  
  
* 745177133c CMake: Un-TP qml deployment API  
The qml CMake deployment API is out of Technical Preview status.  
  
* a432970b25 Standardize Drag/PinchHandler active/persistent scale,  
rotation, translation  
PinchHandler.activeTranslation now holds the amount of movement since  
the pinch gesture began. PinchHandler.persistentTranslation holds the  
accumulated sum of movement that has occurred during subsequent pinch  
gestures, and can be set to arbitrary values between gestures. Likewise,  
activeScale, persistentScale, activeRotation and persistentRotation  
follow the same pattern. The scaleChanged, rotationChanged, and  
translationChanged signals include delta arguments, which are useful for  
incrementally adjusting a non-default item property when the target is  
null.  
  
* 85fab4c5b4 Deprecate PinchAxis minimum/maximum scale and rotation  
properties  
PinchHandler.minimumScale, maximumScale, minimumRotation and  
maximumRotation are deprecated in favor of the minimum and maximum  
properties in the new scaleAxis and rotationAxis.  
  
* 0db201eb3b Add containerStyle property to Material attached object  
Added containerStyle attached property, which can be used on certain  
controls to change the style of the container that they are rendered in.  
  
* 2482a00596 PinchHandler: don't confine activeScale and activeRotation  
to min/max  
PinchHandler's activeScale (which was previously called scale) is no  
longer restricted to the range between minimumScale and maximumScale:  
these limits apply only to persistentScale. Likewise, activeRotation  
(previously rotation) is no longer restricted to the range between  
minimumRotation and maximumRotation.  
  
* 3708f5e5e6 Pointer handlers: don't emit canceled() when an extra  
button interrupts  
A Pointer Handler no longer emits the canceled() signal when it  
deactivates due to violating conditions (such as pressing the right  
button when acceptedButtons == LeftButton).  
  
* 4f86815d3f Fix missing glyphs when using NativeRendering  
Fixed an issue where text using NativeRendering would sometimes be  
missing glyphs.  
  
* 49cdc5c02b QQuickTableView: change the order of row and column to  
modelIndex()  
Because of a source incompatible change in Qt 6.4.0 and Qt 6.4.1,  
modelIndex(column, row) has been reverted back to modelIndex(row,  
column), equal to how it was in Qt 6.3. This also affects modelIndex()  
in TableView. If the order used in Qt 6.4.1 is needed, you can set the  
environment variable QT_QUICK_TABLEVIEW_COMPAT_VERSION=6.4  
  
* 9e62634bc0 Slow Deprecation of FILENAME_VARIABLE, replacement by  
OUTPUT_SCRIPT  
The FILENAME_VARIABLE option of qt6_generate_deploy_qml_app_script is  
now deprecated, use OUTPUT_SCRIPT option instead.  
  
* 1d090673bf CMake: Allow omitting the version of QML modules  
You can now omit the VERSION argument to qt_add_qml_module(). This will  
automatically generate the highest possible version.  
  
* e31abbf878 MultiPointTouchArea: rename signal arguments in Qt 7; test  
with formals  
As a reminder: you should always use formal parameters when writing a  
signal handler that depends on an argument, such as  
MultiPointTouchArea.onPressed, onUpdated, onReleased, or onCanceled. It  
gives you an opportunity to name the argument, to avoid confusion with  
the touchPoints property, and will avoid behavior changes if we rename  
the argument in a future version.  
  
* a8caf1f771 TableView: deprecate modelIndex(row, column) in favor of  
index(row, column)  
modelIndex(row, column) has been deprecated in favor of index(row,  
column).  
  
* 0e7f305667 TableView: deprecate itemAtCell(column, row) in favor of  
itemAtIndex(modelIndex)  
itemAtCell(column, row) has been deprecated in favor of  
itemAtIndex(modelIndex).  
  
* 0decb824c0 TableView: deprecate positionViewAtCell(column, row) in  
favor of positionViewAtIndex(modelIndex)  
positionViewAtCell(column, row) has been deprecated in favor of  
positionViewAtIndex(modelIndex).  
  
* c759966b89 Unexport QSGMaterialShader::GraphicsPipelineState  
The GraphicsPipelineState struct in QSGMaterialShader is no longer  
exported. This may present a binary compatibility break in theory, but  
unlikely to affect any applications in practice given that there is no  
use case for creating or copying an instance of this type in user code.  
This struct serves solely as input to the virtual  
updateGraphicsPipelineState() function, and instances are always created  
and initialized with default values by Qt.  
  
* ecf96e3388 QmlCompiler: Fix coercion of undefined to float and double  
Converting a JavaScript value to a double or float, for example by  
inserting it into a typed array, now assumes JavaScript type coercion  
semantics. In particular, converting a value that is not actually a  
number now results in NaN where it previously sometimes resulted in 0.  
  
* d7602cb315 Set correct `this` value in JSON.stringify replacer scope  
Set correct `this` value in JSON.stringify replacer scope, so that the  
value for current key in current object is no longer pre-stringified,  
and can actually be used to implement custom object serialization logic.  
  
* 2acf4db153 QML: Fix conflicts between QML_ANONYMOUS, QML_UNCREATABLE  
and namespaces  
You can no longer override the "uncreatable" message for QML-exposed  
namespaces using QML_UNCREATABLE. This would be incompatible with making  
the QML_UNCREATABLE macro safe from unintended inheritance. The latter  
is much more important.  
  
### qtmultimedia  
* 909fc7187 Fix behavior of QAudioSink::resume in push mode  
Calling QAudioSink::resume() now returns the sink to the state it had  
when QAudioSink::suspend() was called, no matter whether the sink  
operates in pull or push mode.  
  
### qttools  
* afbc20ed0 lupdate: Allow multiple specifiers after method signature  
lupdate does not trip anymore over tr() calls in methods with multiple  
specifiers. For example "QString MyClass::foo() const noexcept" now gets  
the correct context.  
  
* 1bc41bf8f QDoc: Add support for en-dash and em-dash  
  
  
* f97662104 Qt Designer: add QAction's menu role to action dialog  
The menu role has been added to the Action Editor dialog.  
  
* 9f52107c1 Qt Designer: Enable QQuickWidget for all Graphics APIs  
QQuickWidget is now available for all Graphics APIs.  
  
* 356531bab QDoc: Remove the "\newcode" and "\oldcode" command pair  
The deprecated \oldcode, \newcode commands were removed.  
  
* e2f237e74 qdoc: Enable correct linking to externally-built  
dependencies  
  
  
* f003dd86a qdoc: Unify handling of QML types and QML value types  
  
  
* 79370665b Update qlitehtml module  
Litehtml (used in Qt Assistant) was updated to upstream version v0.6.  
  
### qtdoc  
* 740dcc8f Document that macOS 10.14 and iOS 13 are no longer supported  
macOS 10.14 and iOS 13 are no longer supported deployment targets. If  
you have overridden the deployment target of your application, please  
update accordingly.  
  
### qtpositioning  
* f1316b77 Provide a QML binding for QGeoSatelliteInfo C++ class  
Convert QGeoSatelliteInfo to Q_GADGET and expose it to QML as  
geoSatelliteInfo value type. Also expose its nested enums in  
GeoSatelliteInfo namespace.  
  
* 1d040d9f Provide QML binding for QGeoSatelliteInfoSource C++ class  
Introduce SatelliteSource QML type, which provides QML API for  
QGeoSatelliteInfoSource C++ API.  
  
### qtconnectivity  
* f9adde45 Fix the return value for  
QBluetoothSocketPrivateDarwin::setSocketDescriptor  
QBluetoothSocket::setSocketDescriptor now always returns false on  
Darwin backend. That is the correct behavior because this method is not  
implemented.  
  
* 8fd38321 QtConnectivity/NFC: implement read/writeNdef for iOS  
Added support for writing and and reading NDEF messages on iOS devices.  
  
* c9d7b7c2 Add QLowEnergyController::readRssi()  
Added API for reading RSSI.  
  
* e7499c2c Add Bluez DBus peripheral role support  
Add support for Bluez DBus peripheral role  
  
* c46a3b15 SDP scanner: encode input URLs and escape XML-specific  
characters  
sdpscanner now %-encodes the URLs and escapes all XML-specific  
characters in them before adding the result to the generated XML output.  
  
### qtwayland  
* 35d82dca client: Allow resizing with touch input on client-side  
decorations  
Enable resizing windows using client-side decorations with touch input  
as well as mouse input.  
  
* 5bae5deb compositor: Support touch interaction with client decorations  
It is now possible to move windows using client-side decorations with  
touch input as well as mouse input.  
  
* 6e642a07 Client: Provide support for custom shells  
It is possible to run Qt applications using more than one shell surface  
protocol, e.g. xdg-shell + layer-shell.  
  
* ba39e7c6 client: Fix infinite recursion with text-input-v2  
Fixed a possible crash when editing a field in an item view.  
  
* 023b8981 compositor: Fix crash when raising shell surface item  
Fixed an issue where the compositor would sometimes crash if a shell  
surface item was brought to front.  
  
### qtimageformats  
* 91c2c38 Update bundled libwebp to version 1.2.4  
Update bundled libwebp to version 1.2.4  
  
* e911596 TGA Plugin: Fix reading of CMapDepth  
Fixed reading of TGA files with a non-zero X-origin  
  
* 077148c Update bundled libwebp to version 1.3.0  
Update bundled libwebp to version 1.3.0  
  
* 6f0e0c7 Update bundled libtiff to version 4.5.0  
Bundled libtiff was updated to version 4.5.0  
  
### qtserialbus  
* 048659a6 QModbusDevice: introduce an InvalidResponseError error code  
Introduce a new InvalidResponseError error code. Use this code instead  
of UnknownError when QModbusClient fails to parse the response.  
  
* e7ce9ac1 Make pduFromStream work on big endian (again)  
Fix reading from stream on big endian systems  
  
* 92b48dfb Introduce value classes for generic CAN bus parser  
Introduce QCanSignalDescription, QCanMessageDescription and  
QCanUniqueIdDescription classes. These classes are used to provide a set  
of rules to encode/decode the CAN bus messages.  
  
* fb5b1173 Long live QCanFrameProcessor  
Introduce the QCanFrameProcessor class. This class can be used to  
decode the received QCanBusFrame into a map of key-value pairs, and also  
compose a QCanBusFrame out of a map of key-value pairs. The class uses  
the information provided by QCanUniqueIdDescription object and a list of  
QCanMessageDescription objects as rules to do the encoding or decoding.  
  
* b0eede2d PeakCAN: Make compatible to latest MacCAN library  
The PeakCAN plugin is now compatible to the MacCAN library 0.9 or  
higher. On the other hand, older MacCAN libraries are no longer  
supported.  
  
* 186f34be Long live QCanDbcFileParser!  
Introduce a new QCanDbcFileParser class to parse DBC files. The DBC  
file parser will provide a list of QCanMessageDescriptions as a result.  
These can later be used in a QCanFrameProcessor to decode or encode  
QCanBusFrames.  
  
### qtwebsockets  
* d885e44 QWebSocketServer: update handshake timeout to keep up with  
QSslServer  
Due to the introduction of a standalone QSslServer, with its own  
timeout handling, the setHandshakeTimeout() function now applies the  
same timeout to both the TLS and WebSocket handshakes separately.  
  
### qtwebengine  
* 185a273ea Add Support for Client Hints Headers  
Client hint headers now added to HTTP requests  
  
* 8fd714008 Deprecate Quota Permission Request API  
Deprecate QWebEngineView.quoataRequested() signal. The signal is not  
emitted anymore.  
  
* 117ed7f5c Add touchSelectionMenu for widgets  
Added touch selection menu.  
  
* 7ff442bc6 Disable WebEngineContext dump by default  
Disabled WebEngineContext dump by default.  
  
### qtwebview  
* be675d3 Add settings API for QtWebView  
Added settings API to make it possible to modify some of the WebView's  
built-in functionality.  
  
### qtcharts  
* 189f798b Add ability to customize labels for specific points  
Add LabelFormat to PointConfiguration, allowing the user to set a  
custom label to specific points.  
  
### qtnetworkauth  
* db2f209 OAuth2: allow to specify TLS configuration  
Introduce a new sslConfiguration parameter which allows to specify a  
TLS configuration used during the authentication process.  
  
### qtremoteobjects  
* e96d2a9 Fix race condition when accessing invalid index  
Fix race condition when accessing invalid index  
  
### qtquick3d  
* 7c0bc9c8 Proper implementation of instanced picking  
Add support for picking of instanced models.  
  
* b5e3effd Add vertexColorsEnabled property to PrincipledMaterial  
Added a vertexColorsEnabled property to PrincipledMaterial that is  
identical to the one in DefaultMaterial.  
  
* 8372463d Add vertexColorsEnabled property to SpecularGlossyMaterial  
Added a vertexColorsEnabled property to SpecularGlossyMaterial that is  
identical to the one in DefaultMaterial.  
  
* 08717109 Add built-in simple fog  
Added support for a simple fog effect. This can be configured via the  
SceneEnvironment::fog property and the new Fog type.  
  
* 226aac61 Change API to follow QtQuick3DPhysics  
HeightFieldGeometry::heightMap is deprecated and replaced with  
HeightFieldGeometry::source.  
  
* d32625ab Mark types in QtQuick3D.Effects as deprecated  
The pre-made post-processing effects inherited from Qt 3D Studio and  
its predecessors are now marked as deprecated. They are still available  
for use, but new projects are encouraged to use the 3D post-processing  
facilities provided by ExtendedSceneEnvironment and SceneEnvironment.  
Whereas 2D effects that operate on and treat the output of the View3D as  
a simple 2D image, are recommended to be implemented via Qt Quick's  
facilities, such as the new MultiEffect type or the Qt Quick Effect  
Maker tool.  
  
### qt5compat  
* 153b799 Avoid recreating gaussian blur shader multiple times  
Improve creation time of Gaussian Blur-based effects.  
  
### qthttpserver  
* 55d1020 Add connection tracking  
Most public methods that accepted a QTcpSocket are now accepting  
QHttpServerResponder instead.  
  
* d38ffaa Remove QHttpServerResponse::write() and add  
QHttpServerResponder::writeResponse()  
QHttpServerResponse::write() method was removed in favor of new  
QHttpServerResponder::writeResponse().  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-104053 tst_QFile fails on webOS  
* QTBUG-103974 Wasm: unused functions in qtestcase.cpp, wasm framework  
doesn't build when cross-compiling on Mac  
* QTBUG-103455 Settings don't work with content:// URL on Android  
* QTBUG-103733 [Windows] setProcessDpiAwarenessContext(DPI_AWARENESS_CON  
TEXT_PER_MONITOR_AWARE_V2) failed on certain machines  
* QTBUG-98988 Qt bugs when portal implementation is not available  
* QTBUG-104123 "configure -no-pkg-config" doesn't turn off pkg-config  
* QTBUG-103894 Configuring fails on Manjaro Linux  
* QTBUG-96513 CI: qmake examples should not be built from tainted source  
tree  
* QTBUG-104056 Conan: qmlimportscanner: No such file or directory  
* QTBUG-88519 androiddeployqt doesn't know about Conan's build path  
* QTBUG-89588 androiddeployqt fails with error from qmlimportscanner if  
qtdeclarative is not installed  
* QTBUG-103922 Calling QThread::terminate() in destructor causes double  
object destruction  
* QTBUG-104050 The position of the submenu initiated by the tab key is  
incorrect  
* QTBUG-104003 QTabBar/QTabWidget crashes when closing last tab and  
there are hidden tabs  
* QTBUG-103568 Android 13: Warnings when starting qt apps  
* QTBUG-103836 Fusion menu text with mnemonic clipped on Windows  
* QTBUG-94481 [REG 5.15.2 -> 6.1.1] Ellipsis in the worst possible place  
* QTBUG-49704 QLoggingCategory::installFilter crashes with the code from  
documentation  
* QTBUG-100361 No font rendering at all when configured with -no-  
harfbuzz  
* QTBUG-103838 QFontMetrics::horizontalAdvance() does not seems to give  
correct value  
* QTBUG-98417 Bundling translation file of plist does not work with  
XCode 13  
* QTBUG-56893 Closing a dialog via mouse click on a button causes an XCB  
error  
* QTBUG-100093 Deployed third party library points to the original  
location  
* QTBUG-101161 Android Assets awfully slow to be loaded  
* QTBUG-88799 WASM - No hover on the whole GUI  
* QTBUG-104261 tst_qstringconverter::roundtrip() ASAN error stack-use-  
after-scope  
* QTBUG-102021 QCocoaScreen::UpdateScreens crash  
* QTBUG-84741 Crash on QCocoaScreen::isOnline() when calling  
CGDisplayIsOnline  
* QTBUG-101585 QMessageBox components get skipped by Windows Narrator  
* QTBUG-104231 tst_QVulkan fails with Ubuntu 22.04 due to broken Mesa  
lavapipe included in the distro  
* QTBUG-103007 Resetting a QComboBox custom model doesn't emit  
currentIndexChanged or currentTextChanged  
* QTBUG-104320 qt_add_big_resources does not list contents of the qrc  
file in Qt Creator  
* QTBUG-98845  .moc file is not included as dependency for .obj when  
digit separator is used  
* QTBUG-102768 Invalid warning message in debug builds when using  
QFont::setFamily() with comma split  
* QTBUG-103775 Downstream crash when bad index passed to insert methods  
of QBoxLayout  
* QTBUG-100188 Page layout settings are reset when QPrintDialog is shown  
if there is no printer installed on macOS  
* QTBUG-102395 QMainWindow::restoreState corrupts relation between  
toolbars layout item  
* QTBUG-104201 QWidget: resize() after showMaximized() causes strange  
behaviour  
* QTBUG-102595 Builds can't find the projects qml modules  
* QTBUG-78826 Cannot enter non ascii characters to the TextField and  
QLineEdit from browser(wasm)  
* QTBUG-102343 Windows: Only initial QScreen values are available if  
screen geometry changes between QApplication and before first window is  
open  
* QTBUG-103383 Windows: Qt doesn't respond to DPI changes if Qt window  
is having a non-Qt parent  
* QTBUG-79248 TrayIcons Menu does not scales its size when changing DPI  
* QTBUG-103375 [REG:5.15->6] Shift_JIS support for QDomDocument on Qt6  
* QTBUG-104421 tst_qthread terminateAndPrematureDestruction() ERROR:  
AddressSanitizer: stack-buffer-underflow  
* QTBUG-91896 QTableView span gets confused with logical indexes when  
columns are moved  
* QTBUG-104412 FAIL!  : tst_AndroidAssets during dependency update  
* QTBUG-85474 QGraphicsScene::clearSelection() may leave internal state  
inconsistent  
* QTBUG-103497 [iOS] CMake handling qt_add_big_resources() fails  
* QTBUG-104419 tst_qxp_function_ref::voidReturning() AddressSanitizer:  
stack-use-after-scope  
* QTBUG-104362 QDomImplementation::DropInvalidChars strips emoji and  
other non-BMP characters  
* QTBUG-86790 Mingw Qt provides debug libraries in the wrong folder  
* QTBUG-104443 xcb plugin crashes when running in vnc  
* PYSIDE-1750 QMouseEvent.pos marked as deprecated in source but not in  
docs  
* QTBUG-103992 QFuture::onCanceled is not called when promise is deleted  
* QTBUG-104083 tst_bench_shared_ptr does not compile on Ubuntu 22.04  
* QTBUG-104085 QJsonValue::toObject(const QJsonObject &defaultValue) and  
QJsonValue::toArray(const QJsonArray &defaultValue) parse empty default  
values incorrectly  
* QTBUG-102869 wasm: Resizing is still accessable under a modal dialog  
* QTBUG-53661 QDom internalSubset is never set  
* QTBUG-104396 qmake projects try to link to static qt libraries with  
hardcoded CI paths (no such file or directory)  
* QTBUG-93748 QT_DEPRECATED_X with Q_REQUIRED_RESULT causes warning  
C5240 in Visual Studio 16.9.5  
* QTBUG-104463 Generated qdoc sources from qtattributionscanner should  
have a different basedir so it is not appearing as version specific  
* QTBUG-94713 markdown writer: preserve auto-link URLs  
* QTBUG-85109 QPainter::drawImage draws images in different places  
depending on image format  
* QTBUG-104501 syntax error: identifier "VkFormat"  
* QTBUG-101615 QMLPATHS not documented  
* QTBUG-104132 [REG 6.2.4->6.3.0] HTTP-Redirect is broken  
(ManualRedirectPolicy)  
* QTBUG-104583 Buffer overrun and crash in  
QColorTransferTable::applyInverse()  
* QTBUG-103415 [Reg 6.1.3->6.2.0] Parallel Animation bug on macOS  
* QTBUG-95319 The cursor size is unstable when multiple QT_SCALE_FACTOR  
is used  
* QTBUG-92485 Q_ASSERT added in qrasterizer.cpp  
* QTBUG-24240 testlib: executing a test with an invalid data label  
doesn't count as a failure and doesn't return a non-zero exit code  
* QTBUG-104484 Missing documentation for QDropEvent methods: position,  
buttons, modifiers  
* QTBUG-95933 Using scanner input IRcode will result in an error when  
second character is uppercase  
* QTBUG-104383 QExpandingLineEdit::resizeToContents crashes  
conditionally in qBound (since Qt 6.3.0)  
* QTBUG-104565 QTableWidgets: crash when double click into table cell  
end that expands beyond   window  
* QTBUG-71900 Double tapping on a word does not show the selection  
handles in the right place after the initial selection  
* QTBUG-58503 Text Handle Cursor Position Offset Error  
* QTBUG-104205 QDockwidget screen change issue(s) more involved parts.  
* QTBUG-104527 iOS: Input panel opens when you click on a QPushButton  
* QTBUG-98651 [iOS 15] Application freezes when QDialog is executed by  
button clicked() signal  
* QTBUG-65559 Wacom tablet with pen, mouse tracking  
* QTBUG-104708 qmake projects try to link to static qt libraries with  
hardcoded CI paths part 2  
* QTBUG-104596 [reg->6.4] Qt Designer crashes when OpenGL widget is  
dragged to form  
* QTBUG-94066 Qt6 CMake targets for plugins missing in shared / official  
builds  
* QTBUG-104736 INCPATH is not correct when using "QMAKE_USE += gtk3" in  
a .pro file  
* QTBUG-104726 Build failure on x86  
* QTBUG-104232 tst_QSslKey::constructor fails with Ubuntu 22.04 and  
openssl 3  
* QTBUG-102825 Popping QML StackView Item makes a11y unusable  
* QTBUG-95930 QGuiApplication::setHighDpiScaleFactorRoundingPolicy()  
ignored on Linux, always acts like PassThrough  
* QTBUG-99546 QT_SCREEN_SCALE_FACTORS doesn't follow rounding policy  
* QTBUG-103794 B2qt fails with Ubuntu 22.04: undefined reference to  
`qt_resourceFeatureZstd'  
* QTBUG-104732 Need QFutureCallOutEvent to export symbols  
* QTBUG-96283 [REG 6.1.3->6.2.0] macOS: Can not configure qml / network  
example with statically compiled Qt  
* QTBUG-69354 QGtk3FileDialogHelper isn't modal  
* QTBUG-104734 Need several struct declarations remain in private header  
* QTBUG-103571 QWindowsContext::findPlatformWindowAt stuck in infinite  
loop  
* QTBUG-104809 Crash in QKmsDevice::createScreenForConnector  
* QTBUG-104696 QFontDialog:: selectedFont and fontSelected always  
returns one font  
* QTBUG-103988 State of QTreeWidgetItem not announce by screenreader  
* QTBUG-104740 Accessibility: NVDA not narrating full state of QTabBar  
* QTBUG-98762 REGRESSION: QPalette::setBrush does not reliably detach  
* QTBUG-104867 QtTest: QCOMPARE prints matching <null>s for mismatches  
when unable to convert to string  
* QTBUG-103940 Insufficient documentation in QRegularExpression variant  
of QString::indexOf(), results in random crash bug  
* QTBUG-104827 Huge APK sizes under Windows  
* QTBUG-99990 windows: Painting an image with DPR >1.0  to a QPrinter  
does not produce correct result  
* QTBUG-101058 Pixelated images on Windows  
* QTBUG-103892 Stop binding to iBridge interface when unit testing  
QTcpServer on macOS  
* QTBUG-103805 Linker error when configuring with "-sanitize fuzzer-no-  
link"  
* QTBUG-104851 qdoc: Ignore Q_WEAK_OVERLOAD  
* QTBUG-104877 wacom: QTabletEvent rotation goes to -180 when absent  
* QTBUG-46113 tst_qcompleter fails on Ubuntu  
* QTBUG-100982 tst_QStaticText fails on Wayland  
* QTBUG-104774 macOS: [Enter] key in TextField generates Qt.Key_Return  
instead of Qt.KeyEnter  
* QTBUG-103473 Regression: Pressing numeric keypad Enter doesn't dismiss  
QDialog containing QLineEdit  
* QTBUG-98921 tst_QGraphicsWidget::initialShow is uber flaky on OpenSUSE  
* QTBUG-104014 tst_QPointer::threadSafety crashed in CI  
(QBindingStorage::reinitAfterThreadMove)  
* QTBUG-104959 QT_NO_TRANSLATION define breaks QML build  
* QTBUG-49205 tst_qnetworkreply::ioGetFromBuiltinHttp  
* QTBUG-104493 Application performance drops if many threads are running  
while QProcess creates sub-processes on Unix  
* QTBUG-104718 fuzz: QCborValue::fromCbor out of memory error 32bit  
* QTBUG-102239 tst_QWidget::enterLeaveOnWindowShowHide is flaky  
* QTBUG-104213 Add \brief descriptions to Concurrent topics  
* QTBUG-104875 Wacom proximity events went missing on X11 in 6.3  
* QTBUG-105002 -mno-direct-extern-access fails clang  
* QTBUG-96702 Mandelbrot example not supporting zoom  
* QTBUG-104270 cmake loads native sysroot cmake config and tries to look  
for libs  
* QTBUG-82477 QClipboard doesn't support custom mimeTypes  
* QTBUG-104268  
tst_QTouchEvent::multiPointRawEventTranslationOnTouchPad() ASSERT  
failure in QList::at: "index out of range"  
* QTBUG-105079 XCB crash on plugin load when HighDPI and multiple  
monitors  
* QTBUG-105140 [REG] default constuctor requirement for meta type  
(QVariant) breaks webengine api  
* QTBUG-105078 QMYSQL: regression in formatValue of QByteArray  
* QTBUG-67254 tst_Gestures::customGesture is flaky  
* QTBUG-105177 Duplicate XCB_EXPOSE events create flakiness in many  
tests  
* QTBUG-105092 QDockWidget cannot be re-docked if floating  
* QTBUG-102879 Examples not linking to Qt::Core are installed in the  
wrong folder  
* QTBUG-104917 QStyleSheetStyle::drawPrimitive(QStyle::PE_PanelLineEdit)  
crashes with widget==nullptr  
* QTBUG-105242 [REGRESSION] After  
2f5f276b4a2a19b9f2669b84f28ce8e970aaa39f network printers are missing  
* QTBUG-104952 QT_WIDGETS_RHI/QOpenGLWidget lost transparency support on  
X11  
* QTBUG-104801 Crash with QPainter::drawText used on a QQuickView with a  
Text item  
* QTBUG-105049 Improper styling of placeholder text in Qt6  
* QTBUG-105204 QProperty: Notfication missing if binding no longer has  
any dependencies  
* QTBUG-104982 [Regression] binding stops being evaluated  
* QTBUG-104951 QT_WIDGETS_RHI/QOpenGLWidget lead to crash on Wayland  
* QTBUG-105234 MSVC 2022 fails to compile qtbase test  
tst_qxp_function_ref.cpp  
* QTBUG-105011 QtWidgets Vulkan RHI backend doesn't support translucency  
on Wayland  
* QTBUG-105264 Uncaught TypeError: self.module.qtAddCanvasElement is not  
a function  
* QTBUG-105310 Using deprecated keyword breaks the build  
* QTBUG-105041 openssl 3.x 32bit platform regression  
* QTBUG-104316 Qt 6.3.1 build for arm failed: selected processor does  
not support `yield' in ARM mode  
* QTBUG-105322 Reg->6.3.1: Passing a QDate to QDateEdit via constructor  
results in wrong date  
* QTBUG-104130 QDomDocument::setContent() with QXmlStreamReader discards  
whitespace-only Text nodes  
* QTBUG-89690 Functions and classes that allow to get whitespace-only  
text nodes are deprecated without any alternatives  
* QTBUG-104940 post in/decrements of QBEInteger and QLEInteger return  
reference according to documentation  
* QTBUG-105160 Bad access when destroying QComboBox immediately after  
selecting item  
* QTBUG-105302 qputenv sometimes puts garbage at the end of the value  
* QTBUG-105363 Opened dialog is not refreshed until mouse button click  
on it  
* QTBUG-105010 Font underline rendering bug  
* QTCREATORBUG-27634 Basic Layouts Example UI elemnets get squished  
* QTBUG-105323 [Regression] Keyboard is not properly hidden on ios  
* QTBUG-105341 QDoubleValidator can report "Intermediate" for inputs  
that are unambiguously out-of-range  
* QTBUG-105393 tst_QImage::exifReadComments fails on webOS  
* QTBUG-105339 Typo in since version for QStyledItemDelegate  
* QTBUG-105374 Modules in 5.15 branch missing MinGW debug files  
* QTBUG-105332  QCommonStyle Missing drawComplexControl() case  
implementation for CC_ComboBox  
* QTBUG-89762 RHI on Vulkan: VK_EXT_debug_report vs. VK_ext_debug_utils  
* QTBUG-105501 Qt6 build fails with system double-conversion  
* QTBUG-105517 Redundant "does" in QFrame  
* QTBUG-105213 Pressing space/enter on a button with focus doesn't  
trigger its action  
* QTBUG-70612 tst_QGraphicsEffect::prepareGeometryChangeInvalidateCache  
is flaky on openSUSE  
* QTBUG-70590 tst_qheaderview::stretchAndRestoreLastSection is flaky  
* QTBUG-93471 Darwin linker warns about global weak symbols when linking  
an executable against a static Qt  
* QTCREATORBUG-27685 Sliders Example not scaling well  
* QTBUG-104754 manual tests that use qt_internal_add_manual_test don't  
run on iOS  
* QTBUG-105527 Vulkan validation shows (useless but annoying) "errors"  
with vkkhrdisplay  
* QTBUG-86967 tst_qfont fails on Ubuntu20  
* QTBUG-105615 Update dependencies on '6.4' in qt/qttools fails  
* QTBUG-104948 QFileDialog::getOpenFileContent not honoring nameFilter  
* QTBUG-102053 Using QMAKE_ASSET_CATALOGS in .pro (qmake) fails with  
"Unknown platform: "ios-simulator""  
* QTBUG-105094 QDockWidget disappears when activating the main window  
behind it  
* QTBUG-104722 qdbusxml2cpp segfault on signal arg without annotation  
* QTBUG-105687 developer-build fails for QSemaphore  
* QTBUG-105221 tst_qgraphicsitem::sorting fails if testcase is executed  
individually  
* QTBUG-74760 Unstable autotest tst_QGraphicsItem::sorting()  
* QTBUG-105133 [REG 6.3.1] Androiddeployqt doesn't find rcc and  
qmlimportscanner  
* QTCREATORBUG-27868 Can't find qmlimportscanner when building examples  
for android  
* QTBUG-105031 a11y AT-SPI: Window-relative positions are incorrect  
* QTBUG-105042 a11y AT-SPI: Window-relative positions are wrong for  
dialogs, screen coordinates returned instead  
* QTBUG-105281 a11y AT-SPI: incorrect handling of window-relative coords  
for "GetOffsetAtPoint" (text interface)  
* QTBUG-105313 a11y AT-SPI: ATSPI_COORD_TYPE_PARENT is not supported  
* QTBUG-105520 a11y AT-SPI: "GetCaption" result (from AT-SPI table  
interface) has incorrect D-Bus type  
* QTBUG-102359  NTLM authentication crashes  
* QTBUG-105583 CMake deployment API generates faulty script if  
CMAKE_INSTALL_BINDIR is set to "." or ""  
* QTBUG-104793 a11y: AT-SPI TableCell interface not supported/exposed  
* QTBUG-105088 Can't rotate a QImage to 45 degrees by Y Axis  
* QTBUG-105810 iOS: TapHandler emits clicked, even if long pressed more  
than StyleHint::MousePressAndHoldInterval  
* QTBUG-105752 a11y AT-SPI: D-Bus reply for "GetAttributeValue" text  
method has incorrect format  
* QTBUG-104963 RMB on file dialog freezes the application  
* QTBUG-104944 QT_DISABLE_DEPRECATED_BEFORE hides wrong APIs  
* QTBUG-105709 Dragging large windows is slow on WASM  
* QTBUG-105286 Crash with UpdateWindowTitle event triggered by closing a  
dialog (mac)  
* QTBUG-105814 Accessibility tools cannot find tree items inside the  
app's UI on Windows  
* QTBUG-105474 Context menu does not close when minimizing window  
* QTBUG-42500 QProcess::start() secretly adds LD_LIBRARY_PATH on *nix  
* QTBUG-104925 [REG 6.4.0-beta1 -> 6.4.0-beta2] Qt no longer builds with  
-no-feature-highdpiscaling  
* QTBUG-105711 QDrag with invalid URLs in QMimeData crash on macOS  
* QTBUG-90504 Dark theme not respected by Fusion style  
* QTBUG-99276 Fusion style sets button text color to white automatically  
* QTBUG-105841 QtAndroid build failure with cmake 3.18.4 (qt 6.3)  
* QTBUG-104962 [REG 6.3.0 -> 6.3.1]QFileDialog does not allow changing  
column sizes nor sorting  
* QTBUG-104425 Crash when loading header state in QBittorent  
* QTBUG-97386 build dir is in QMAKE_PRL_BUILD_DIR → not reproducible  
* QTBUG-105017 Crash in QRhiGles2::ensureContext with  
QT_WIDGETS_RHI_BACKEND=vulkan and QOpenGLWidget  
* QTBUG-100888 tst_QWindow::modalWindowPosition() fails on Wayland  
* QTBUG-105231 reusing editor by reimplementing  
QAbstractItemDelegate::destroyEditor causes crashing  
* QTBUG-14460 QDesktopServices::openUrl() ignores anchor on local files.  
* QTBUG-102091 [Reg Qt 5->6] Disabled QCheckBoxes block scrolling of  
QScrollArea with mouse wheel  
* QTBUG-105832 String-based QObject::connect asserts when parameters are  
incomplete types  
* QTBUG-105621 Lingering bad cursor when dragging an undocked window  
over a textfield  
* QTBUG-105854 a11y AT-SPI: Method "ScrollSubstringTo" from AT-SPI text  
interface not supported  
* QTBUG-105811 a11y AT-SPI: "GetStringAtOffset" from AT-SPI text  
interface not supported  
* QTBUG-105988 a11y: Accessible interface can't be retrieved after  
calling QAccessibleEvent::setChild on event created using the  
constructor taking QAccessibleInterface*  
* QTBUG-105951 Crash when closing dialog directly after closing popup  
* QTBUG-106001 tst_QMap::beginEnd() triggers assertion failure on  
Windows  
* QTBUG-105043 HTTP2 downloads can be very slow  
* QTBUG-103093 Palette Change And Application PaletteChange Never Emited  
* QTBUG-105098 Purge Q_DUMMY_COMPARISON_OPERATOR  
* QTBUG-105932 [Reg in Qt 6] setProperty() fails for QFlags types  
* QTBUG-96185 Cannot use  "qproperty-" to set enum properties in qss  
* QTBUG-105620 Undocked dock widgets are all displayed as active  
* QTBUG-105591 Closing application with toolbar floating breaks toolbar  
the next time you start the application  
* QTBUG-105962 a11y AT-SPI: Qt sometimes uses same unique ID/object path  
for two different objects within a short time  
* QTBUG-106019 tst_QDtls::verifyClientCertificate fails with Ubuntu  
22.04 xorg and Windows 10 OpenSSL 3  
* QTBUG-105061 DirectFB platform plugin build fails  
* QTBUG-106017 tst_QSslCertificate fails with Ubuntu 22.04 xorg and  
Windows 10 21H2 OpenSSL 3  
* QTBUG-106012 tst_QResourceEngine::setLocale fails with Ubuntu 22.04  
xorg plus  
* QTBUG-106064 [REG] Undocking QDockWidget with drag misplaces it (a  
lot)  
* QTBUG-92964 Empty tree not spoken  
* QTBUG-105922 Can't compile examples with Emscripten 3.1.18  
* QTBUG-105004 Links to the code of examples for QCC2 were not updated  
at the move to QtDeclarative  
* QTBUG-106036 Tst_QSslKey fails with Windows 1021H2 and openssl 3  
* QTBUG-96276 _NET_STARTUP_ID not supported  
* QTBUG-87764 [REG 5.15.0 -> 5.15.1] macdeployqt produces  
QtWebEngineProcess.app package with empty folders  
* QTBUG-105735 Focus is not set to a child widget when a modal is open  
* QTBUG-104872 Calling QClipboard::image() corrupts image inside Win 11  
clipboard memory (from Windows Snipping Tool)  
* QTBUG-105338 lose alphachannel in imagedata from QClipboard  
* QTBUG-105923 WebAssembly loader broken when using the CMake  
RUNTIME_OUTPUT_DIRECTORY property  
* QTBUG-100889 tst_QWindow::requestUpdate() fails on Wayland  
* QTBUG-105057 vnc: Setting override cursor causes a crash on client  
disconnect  
* QTBUG-91774 QTextEdit::cursorForPosition() doesn't work with invisible  
blocks  
* QTBUG-94714 Qt's CMake seems to ignore dependencies when generating  
APK targets  
* QTBUG-105347 [Wasm] Stack example from documentation exits application  
* QTBUG-102004 [wasm] QML switch does not react on toggle  
* QTBUG-104518 Swipeview doesn't function correctly in Webassembly app  
* QTBUG-106153 wasm: Changing QTimer interval in multithreaded  
application breaks the timer  
* QTBUG-106223 assertion failed after Flickable takes grab from  
PinchHandler  
* QTBUG-104858 QT_DISABLE_DEPRECATED_BEFORE is not propagated to unit-  
tests  
* QTBUG-106279 I doubt if QTextStream setAutoDetectUnicode doesn't work  
* QTBUG-106000 tst_QLocale::fpExceptions() triggers assertion failure on  
Windows  
* QTBUG-104930 QLocale shows German text for "en_DE"  
* QTBUG-105102 qt_internal_add_tool and qt_internal_add_app does not get  
the value of QT_DISABLE_DEPRECATED_BEFORE  
* QTBUG-106374 Unable to build qtbase due to incomplete type in  
qtessellator.cpp  
* QTBUG-106159 wasm: Image downloading anything external does not work  
even though the request succeeds in multithreaded apps  
* QTBUG-106222 -junitxml produces invalid time in output log (seconds  
divided by 1000 instead of seconds)  
* QTBUG-105129 wasm: InstallTrigger is depreciated  
* QTBUG-106394 Android Multi ABI honors only for first abi the flag  
-DQT_NO_PACKAGE_VERSION_CHECK=TRUE  
* QTBUG-106462 /Users/qt/work/install/target/include/QtCore/6.5.0/QtCore  
/private/qsimd_p.h:216:12: fatal error: 'qsimd_x86_p.h' file not found  
* QTBUG-103196 syncqt does not reflect sources/headers known to CMake  
* QTBUG-106463 Make QT_HOST_PATH well visible and communicated clearly  
* QTBUG-104999 crash in QTextMarkdownWriter  
* QTBUG-106354 Last QNetworkReply::readyRead() is not always emitted  
* QTBUG-106016 tst_QNetworkReply::contentEncodingBigPayload fails with  
Ubuntu 22.04 xorg and Rhel 9  
* QTBUG-106560 WASM: Menus are resizable  
* QTBUG-106397 wasm: native keyboard does not popup on iOS  
* QTBUG-106472 macOS: Crash at exit on if QPixmap was copied to the  
clipboard  
* QTBUG-106610 gradlew is installed as not executable  
* QTBUG-23699 tst_QGraphicsWidget::updateFocusChainWhenChildDie() fails  
on Mac OS X  
* QTBUG-106573 QNetworkAccessManager can not get 404 reponse body.  
* QTBUG-42661 Wrong dialog activation  
* QTBUG-98048 Drag and drop with pixmap laggy on KDE  
* QTBUG-106571 qt_add_dbus_adaptor and qt_add_dbus_interface regression  
* QTBUG-106025 REG: isSignalConnected creates a dead lock.  
* QTBUG-106652 applicationName() default value broken on macOS  
* QTBUG-105618 QNetworkReplyFileImpl synchronously emits  
QNetworkReply::finished() from constructor in case of error  
* QTBUG-7211 QFile::permissions() returns old, cached value after call  
to QFile::setPermissions() on the same QFile object  
* QTBUG-101236 FAIL!  : tst_QPainter::hdrColors in Windows_11_21H2  
* QTBUG-106393 Mac OS: Dot and Comma key combinations not working for  
russian layout  
* QTBUG-36281 QKeyEvent regression in Qt5  
* QTBUG-35734 When pressing CTRL+SHIFT+number on a German keyboard then  
the key() you get in the key press is not always as expected  
* QTBUG-106668 Cannot paste content from external sources  
* QTBUG-87339 wasm: Emoji couldn't show while the text contains Chinese  
and emoji mix  
* QTBUG-71948  Containers with drag "rubber band effect" should react on  
pointer cancel  
* QTBUG-106436 Scene Graph - Direct3D 11 Under QML Example has wrong tag  
* QTBUG-106438 Scene Graph - Metal Texture Import Example has wrong tag  
* QTBUG-106439 Scene Graph - Metal Under QML Example has wrong tag  
* QTBUG-106469 QQuickRenderControl D3D11 Example has wrong tag  
* QTBUG-89557 QML Text's implicitWidth is wrong when wrapMode is set for  
multiline text.  
* QTBUG-104986 QTextLayout::maximumWidth() is not correct for multi-line  
text  
* QTBUG-104805 QColorDialog : Buttons are highlighted incorrectly  
* QTBUG-103503 Frameless window is resizable  
* QTBUG-106710 Regression: macOS windows with Qt::FramelessWindowHint  
are resizable  
* QTBUG-105182 Access violation / infinite loop in  
QFutureInterfaceBase::isChainCanceled()  
* QTBUG-106083 QFuture::then(QObject *context, Function &&function)  
throws "read access violation" when used in chained QFuture  
* QTBUG-106616 androiddeployqt not found on MultiABI android build with  
custom install dir  
* QTBUG-106672 [Reg: 6.3 -> 6.4] C3615: constexpr function  
'QtPrivate::QMetaTypeForType<T>::getName' cannot result in a constant  
expression  
* QTBUG-106531 QDockWidget Docking resizes (widens) the widget by a set  
number of pixels  
* QTBUG-104441 REG: No longer possible to use macros or functions that  
rely on an event loop in cleanup() after failed test function  
* QTBUG-106689 QNetworkReply: it is confusing whether the reply data has  
been decompressed or not.  
* QTBUG-106627 Stack overflow when trying to deactivate the active  
window-modal window  
* QTBUG-106387 Application crash when writing in textfield  
* QTBUG-106899 tst_qquicktext::dependentImplicitSizes() Compared doubles  
are not the same  
* QTBUG-106530 QDockWidget Undocking incorrectly offset from cursor  
(native titlebar) when dragging  
* QTBUG-101339 Hardware keyboard up/down keystrokes interpreted as  
home/end when interacting with a QML TextArea  
* QTBUG-106912 MoltenVK: Failed to create Vulkan instance when  
implementation supports is_portability_driver  
* QTBUG-106920 MOC cannot parse nested inline namespace (Parse error at  
"::")  
* QTBUG-100917 tst_QImageReader::setScaledClipRect() SVG/SVGZ fails on  
Wayland  
* QTBUG-81044 SVG: QImageReader::setScaledClipRect() uses wrong  
coordinate system  
* QTBUG-106978 Link failure with OpenSSL 3.0  
* QTBUG-92199 [REG] The color of QLineEdit and QPlainTextEdit  
placeholder text is not grayed-out if stylesheet was applied  
* QTBUG-93009 QPalette::PlaceholderText color is not followed after  
setting color in a style sheet  
* QTBUG-106980 dladdr() in qlogging.cpp - error: invalid conversion from  
'const void*' to 'void*'  
* QTBUG-90893 QNetworkRequest WASM implementation has no way of setting  
'withCredentials = true'  
* QTBUG-107004 Copying from QTextEdit to other program turns newline  
into paragraph separator (U+2029)  
* QTBUG-107043 Qt 6.4 QDateTime is broken with clang-cl when compiling  
with c++20  
* QTBUG-107072 build chooses unavailable hardware flags  
* QTBUG-107027 tst_QSslCertificate::subjectAndIssuerAttributes() failed  
on Ubuntu 22.04(GNOME on xorg)  
* QTBUG-106607 QODBC: QSqlQuery::isNull returns false for SELECT NULL  
* QTBUG-106984 Setting background brush in QTableWidgetItem used as  
header item is incorrectly cached leading to incorrect display colours  
* QTBUG-69608 cocoa: key press events for modifier keys do not have  
nativeVirtualKey  
* QTBUG-106353 Possibility of macOS build is not taken into account when  
building a project with CONFIG += simulator in mkspecs  
* PYSIDE-2069 pyside6-uic generates dynamic properties with C++ types  
* QTBUG-106947 QTextLayout::maximumWidth() doesn't handle spaces  
correctly  
* QTBUG-106219 [macOS] Typing accented/alternate characters doesn't work  
correctly  
* QTBUG-105984 windeployqt: Multimedia plugins missing  
* QTBUG-107178 plugins/platforms/libqminimal.so' is not a valid ELF  
object (file is for a different processor)  
* QTBUG-100891  
tst_QGuiApplication::genericPluginsAndWindowSystemEvents() fails on  
Wayland  
* QTBUG-100918 tst_QOpenGL::bufferMapRange() fails on Wayland  
* QTBUG-107249 [REG 6.4.0->6.5.0] Can not compile Qt examples with  
Android armv7 pre-build binaries on linux and macOS  
* QTBUG-107174 Units unclear for QWaitCondition::wait  
* QTBUG-107128 qtbase/src/dbus/dbus_minimal_p.h SPDX-License-Identifier  
misses AFL-2.1  
* QTBUG-107038 Non-aliased Text is rendered incorrectly using  
NativeRendering  
* QTBUG-97697 Missing documentation for GrabTransition enum in  
DragHandler  
* QTBUG-107246 QVariant.toList method not working properly  
* QTBUG-107188 Reg: Behavior Change: Modal dialogs seem to block events  
to other dialogs/widget  
* QTBUG-107155 tst_QWidget_window::resetFocusObjectOnDestruction() with  
QtWayland failed on Ubuntu 22.04, GNOME  
* QTBUG-107544 [Reg 6.3.2 -> 6.4.0] qsql_oci.cpp no longer compiles  
* QTBUG-107166 QQuickWidget causes crash when combined with dock and  
toolbar  
* QTBUG-107262 REG: Enter on r/o QComboBox does not close a dialog  
anymore  
* QTBUG-107569 Use of std::aligned_union and std::aligned_union_t  
deprecated in C++23  
* QTBUG-106542 qCompress()/qUncompress() cannot handle more than 4GiB of  
data on Win64  
* QTBUG-104831 windeployqt does not deploy Designer plugins for  
QUiLoader  
* QTBUG-70088 tst_QDoubleSpinBox::editingFinished() is flakey  
* QTBUG-100245 tst_qsqlquery should not create unique data tags when  
testing  
* QTBUG-81540 SFNT (OFT wrapped bitmap) font doesn't rotate  
* QTBUG-107719 Typo in the document?  
* QTBUG-107450 Reg[5->6]QSlider handle size is not correct  
* QTBUG-79977 QMessageBox does not work at  IOS 13  
* QTBUG-103387 QLibrary doesn't load() after a previously failed load()  
* QTBUG-77210  QML Image object causes a crash when it gets deleted  
while it's still loading  
* QTBUG-101000 macOS: QPushbutton text color changes  
* QTBUG-105292 Documented way of printing whole document produces  
warning  
* QTBUG-45357 Let qmake check whether Info.plist is in XML format  
* QTBUG-47979 QDesktopServices is unable to open a file on Android  
* QTBUG-107777 Typo in the document  
* QTBUG-102098 QPrinter::PdfFormat causes some fonts to be doubly-scaled  
when using DirectWrite font engine  
* QTBUG-107666 [REG 6.3.2 -> 6.4.0] Mac: QWindow blanks when resized by  
a custom window manager when it contains a QOpenGLWidget  
* QTBUG-103215 QTextDocument draws corrupted fonts on macOS in certain  
cases  
* QTBUG-85773 QML TextEdit copy() copies text twice on Android  
* QTBUG-106713 android.bundle.enableUncompressedNativeLibs=false  
deprecated in Android Gradle plug-in ver 8.0  
* QTBUG-107794 REG->dev (6.5)/Windows: Crash when playing message dialog  
sound with NoSound Scheme  
* QTBUG-85445 Qt for WebAssembly - QFileDialog doesn't show files in the  
MEMFS until we type the file name  
* QTBUG-107618 QFileDialog freeze when selecting large zip-file using  
the windows native dialog  
* QTBUG-96384 Tagalog cannot be displayed correctly  
* QTBUG-98920 Font fallback is not working properly on macOS  
* QTBUG-107814 Reg:[6.3->6.4]QOpenGLWidget tries to render duplicate  
controls  
* QTBUG-107627 AndroidAssetsFileEngineHandler is broken  
* QTBUG-107539 wasm: 2dpainting sample not working with  
webassembly/webgl  
* QTBUG-107197 [wasm] DropShadow breaks keyboard input  
* QTBUG-107629 [REG 6.3->6.4] WebEngineWidget OpenGL rendering is broken  
on Windows  
* QTBUG-107810 QImage::Format_Grayscale16 saved as 24bpp JPG  
* QTBUG-104709 [REG. 6.2->6.3] macOS: Default Edit menu entries shown  
twice  
* QTBUG-106227 Alternate row background color does not starts from  
beginning  
* QTBUG-107649 valgrind issue due to 9 bits in flags  
* QTBUG-80992 QT_SCALE_FACTOR don't work properly with WebAssembly  
* QTBUG-63324 iOS/macOS: system localization always returns english  
language  
* QTBUG-107575 Incorrect variable name in  
`_qt_internal_process_resource`  
* QTBUG-107054 Build with -no-feature-highdpiscaling is broken again on  
dev  
* QTBUG-98354 Windows 11: State of checkable QAction with icon is not  
shown  
* QTBUG-107589 QT_ANDROID_EXTRA_LIBS does not detect library  
dependencies  
* QTBUG-106035 Android: skipping *: it has unmet dependencies  
* QTBUG-107879 FAIL!  : tst_AndroidAssets::loadsFromAssetsPath  
* QTBUG-106277 QProperty fails to compile on MSVC in C++20 mode  
* QTBUG-107843 cmake: multi-ABI Android builds do not work in-tree  
* QTBUG-107926 Crash on accessing clipboard  
* QTBUG-107720 "This feature is not supported on the Windows platform."  
is a bit vague  
* QTBUG-104319 Program crash on exit after monitor disconnect  
* QTBUG-106927 On Mac OS 12.5.1, corner widget in QScrollArea is not  
drawn correctly  
* QTBUG-106368 Wrong Usage of DoDragDrop() Causes Drag and Drop via  
Touch to Hang  
* QTBUG-57577 Windows: Drag and drop through touch sometimes gets stuck  
with -platform windows:nomousefromtouch  
* QTBUG-100788 TapHandler tapped signal is emitted twice when using a  
stylus  
* QTBUG-77414 Drag and Drop with mimeData does not work properly on the  
touch screen  
* QTBUG-104594 qpushbutton: pressed signal not emitted until button is  
released, unsing touchscreen as input  
* QTBUG-91882 eglfs with a cloned screen cause app to flicker  
* QTBUG-107008 window list in macOS' dock icon context menu includes  
entry for QSystemTrayIcon  
* QTBUG-106108 REG/macOS:  context menu corners are not rounded  
* QTBUG-107991 QString asprintf behaves differently than printf with  
"%03.f" format for example  
* QTBUG-95585 Refused to set unsafe header  
* QTBUG-105707 EGLFS: Modal windows get stacked behind non-modal windows  
* QTBUG-103611 [Reg 5.15 -> 6.x] Re-initializing QGuiApplication causes  
QQmlApplicationEngine to crash  
* QTBUG-108039 Error with qproperty: expression  
‘std::source_location::current()’ is not a constant expression  
* QTBUG-108032 #including <QKeySequence> before <QSet> can silently  
break hashes used for set comparison  
* QTBUG-107033 qHash(Enum, size_t) may call an unexpected overload  
* QTBUG-105857 Qt application does not follow the DPI change when the  
DPI setting is changed before showing the first window  
* QTBUG-106983 Wrong description in documentation for  
QPartialOrdering::Greater  
* QTBUG-108128 Absolute coordinates used for pointer events on wasm  
* QTBUG-106031 Mouse cursor location offset if canvas doesn't start at  
0,0  
* QTBUG-108103 QHostAddress::isEqual() with IPv6 determines valid ip to  
be any  
* QTBUG-108151 WARNINGS_ARE_ERRORS not applied to repos other than  
qtbase  
* QTBUG-107687  [REG 6.3.1 -> 6.3.2] qt_add_resources with .qm  
translation files no longer rebuild generated .qrc when .qm files change  
* QTBUG-108113 "RCC: Cannot find file" in qt_add_translations  
* QTBUG-103470 [iOS] CMake translation handling fails  
* QTBUG-46681 [REG 4.x->5.x] QPainter in paintEvent() doesn't work with  
Qt::WA_PaintOnScreen  
* QTBUG-100085 xcb: Native window does not get paint event if another  
window on top of it is hidden unless there is a enter/leave event  
somewhere  
* QTBUG-108156 Unhandled exception on QNetworkInformation::load()  
* QTBUG-89156 [REG 5.15.0->5.15.1] Focus is limitted after reparenting  
and adding widgets  
* QTBUG-108186 Crash in qt_memrotate90 or qt_memrotate270  
* QTBUG-108196 SecKeychain is deprecated [-Wdeprecated-declarations]  
when compiling qnetworkaccessmanager.cpp  
* QTBUG-67579 QT5 apps running natively under Wayland do not respect  
cursor size setting  
* QTBUG-87778 wayland: cursor size wrong  
* QTBUG-108194 FAIL!  : data::tst_simulation-behavior::compile() module  
"Simu" is not installed  
* QTBUG-108270 Undefined symbols for architecture x86_64  
* QTBUG-108047 Setting macos style before creating a QApplication  
crashes  
* QTBUG-108218 [Win] Access violation in QNetworkListManagerEvents  
* QTBUG-37207 OSX: VoiceOver for QTableView doesn't work  
* QTBUG-107572 Expose QLineEdit focus for QComboBox editable  
* QTBUG-102478 xcb: QWidget::showMaximized and other functions cause  
QWindow::windowStateChanged signal to be fired twice  
* QTBUG-68175 tst_QWidget::raise is flaky  
* QTBUG-108136 QAnyStringView constraints are broken and cannot work  
* QTBUG-105909 a11y: AT-SPI selection interface not supported  
* QTBUG-83458 Internal links aren't preserved when exporting  
QTextDocument to PDF  
* QTBUG-108344 Something is rotten with texture-based widgets that are  
native child widgets or are children of a native child widget  
* QTBUG-108277 QWidget::setParent calls q_evaluateRhiRecursive which is  
slow  
* QTBUG-108121 Crash when using QQuickDefaultClipNode::setRadius() with  
Material style Button  
* QTBUG-106583 Windows and dialogs flashing white  
* QTBUG-108382 One more unhandled exception on  
QNetworkInformation::load()  
* QTBUG-108311 [REG: 6.3->6.4]: When moving a QDockWidget under certain  
environments it will trigger a warning message  
* QTBUG-108628 Dependency update on qt/qtdeclarative failed in dev  
* QTBUG-108764 tst_qwidgetrepaintmanager is flaky  
* QTBUG-108743 QColor - Undefined symbols QColor::QColor(char const*),  
QColor::QColor(QString const&)...  
* QTBUG-108742 macdeployqt: Multimedia plugins missing  
* QTBUG-107057 macdeployqt does not include libdarwinmediaplugin.dylib  
* QTBUG-108709 [REG 6.4.0 -> 6.4.1] Second ColorRole change via  
QPalette:setBrush() does not modify cacheKey  
* QTBUG-99471 macOS: modifier key does not switch between copy/move  
actions when dragging to file manager  
* QTBUG-46757 QGraphicsItem jumps when reaching the edge of the view  
* QTBUG-108300 Crash when setPersistentGraphics(false),  
setPersistentSceneGraph(false) and visible: true on wayland  
* QTBUG-108605 Unhandled WinRT exception at  
QSystemLocalePrivate::uiLanguages()  
* QTBUG-108617 CMake: headersclean broken on dev  
* QTBUG-108452 syncqt generates empty includes inside header file  
aliases if source and build directory are on a different Windows  
partitions  
* QTBUG-108840 Pasting a file into a text edit crashes the wasm module  
* QTBUG-108611 Developer build with -no-openssl failed  
* QTBUG-107806 Link is dead in the document  
* QTBUG-107675 Typo in the document?  
* QTBUG-108662 Can't build for Android  
* QTBUG-108815 Installing qtdeclarative fails  
* QTBUG-109004 qtbase configuration fails with cmake 3.16 on macos  
* QTBUG-109093 tst_QWidget::optimizedResizeMove flakes on openSuSE Leap  
15.4  
* QTBUG-109123 Vulkan memory gets flushed after unmap  
* QTBUG-105046 Linker failures when building with  
-DFEATURE_openssl_linked=ON  
* QTBUG-108747 QTabletEvent TabletMove not sent to a QWidget without any  
children  
* QTBUG-101680 MySQL plugin: QSqlQuery::prepare + exec no results when  
table contains JSON type  
* QTBUG-108799 [REG 6.2.4-6.3.2] Airplane emoji completely breaks text  
rendering  
* QTBUG-108908 closing QComboBox popup with Escape key also closes  
QDialog on macOS  
* QTBUG-109060 QAction() handling of text does not seem correctly  
documented  
* QTBUG-109061 QAction and ampersands in text  
* QTBUG-109024 incomplete handling of versioned links of tools in cross  
builds  
* QTBUG-109240 file INSTALL cannot find "/home/qt/work/qt/qtremoteobject  
s_build/mkspecs/modules/qt_lib_repparser_private.pri":  
* QTBUG-109239 file INSTALL cannot find "/home/qt/work/qt/qttools_build/  
mkspecs/modules/qt_lib_linguist_private.pri"  
* QTBUG-108677 macdeployqt tool does not copy networkinformation plugin  
* QTBUG-108841 Potential use-after-free in qClipboardPasteTo  
* QTBUG-108818 REG: qVersion() no longer included in <QtGlobal>  
* QTBUG-108641 system tray icons in Windows 10 goes blurry  
* QTBUG-109207 moc can't create output file when path is longer than 255  
characters  
* QTBUG-104895 Text rendering letter-spacing error  
* QTBUG-104916 QMYSQL Driver does not support MYSQL_OPT_LOCAL_INFILE  
* QTBUG-109169 Invalid QColorTrcLut use causes unreadable text with  
16-bit X11 visuals  
* QTBUG-25280 QNetworkAccessManager concurrent request limit not  
configurable  
* QTBUG-109271 Wasm: qmake.bat and qtpath.bat wrapper scripts call non-  
existent host tools  
* QTBUG-109287 [macOS] Crash in QNSOpenSavePanelDelegate  
* QTBUG-109090 QShortcutEvent requires id but id() is only deprecated in  
headers  
* QTBUG-107109 AUTOMOC warns about missing relevant classes after  
syncqt.cpp migration  
* QTBUG-106634 Android examples: cmake error with cmake 3.18  
* QTBUG-107560 QPointerEvent::clone does not do a deep copy, leaving the  
cloned object partially aliased  
* QTBUG-104776 AndroidContentFileEngineIterator hangs when listing  
shared content with nested dirs  
* QTBUG-109270 [REG 6.4.1->dev]: Qt does not build without Freetype  
* QTBUG-109226 Rare crashes in QXcbBackingStoreImage::flushPixmap  
* QTBUG-28853 QPainter's drawText method can't paint unicode characters  
with code values above 65535  
* QTBUG-103515 QSystemTrayIcon/macOS: Cannot quit the app when the  
context menu is opened by secondary click  
* QTBUG-108440 Wrong icon picked in QMenu in multi monitor multi DPI  
setup (Vista style)  
* QTBUG-82104 Qt Quick Live preview not working on Toradex Apalis i.MX 8  
with Yocto 2.7  
* QTBUG-108286  Guard against a non-visible Svg target when find_package  
is done in a nested subdirectory  
* QTBUG-101526 Special character "Object Replacement Character" does not  
show up visibly  
* QTBUG-109428 ABI broke for QJniObject::callVoidMethodV in 6.4  
* QTBUG-93624 nameFilters not working in FileDialog in iOS  
* QTBUG-106701 Crash with any QML app on external display with iPadOS  
16.1 on M1 iPad  
* QTBUG-109066 wasm: QDialog::exec() with asyncify hangs  
* QTBUG-109449 inlining QByteArray::isNull() causes BC break on static  
Qt builds  
* QTBUG-109165 No repaint when QGraphicsEffect gets destroyed  
* QTBUG-99601 ios: QMAKE_PRE_LINK Gives Error :Multiple commands produce  
* QTBUG-77385 QWidget::restoreGeometry does not work as documented.  
* QTBUG-4397 QWidget::RestoreGeometry does not work if saveGeometry() is  
called while a widget is maximized [regression]  
* QTBUG-109400 Windows: Font Line spacing differs between Qt 5 and 6  
* QTBUG-109466 QTEST_FUNCTION_TIMEOUT applies to the whole test, not per  
function  
* QTBUG-108848 iOS: Voice Control Accessibility feature breaks in iOS 16  
* QTBUG-108365 [REG 6.4.0 -> 6.5] Low contrast status bar in Android  
applications  
* QTBUG-107662 Android keyboard doesn't close when clicking on done  
* QTBUG-88652 QTEST_FUNCTION_TIMEOUT and test function limit (5 minutes)  
are not documented.  
* QTBUG-63700 QSharedPointer missing documentation for move operators  
* QTBUG-109436 Drag&Drop Memory leak  
* QTBUG-109329 tst_qprocess crash in OpenSUSE 15.4  
* QTBUG-109026 Android: UI is scaled smaller than before  
* QTBUG-109212 QLabel with embedded image using 'qrc:/' will no longer  
load  
* QTBUG-109214 Documentation for QtAndroidPrivate is still wrong for  
CMake  
* QTBUG-109559 tst_qmessagelogger::qMessagePattern(backtrace) is flaky  
on OpenSUSE 15.4  
* QTBUG-109586 QAndroidApplication::runOnAndroidMainThread() UB when  
timeout is set  
* QTBUG-109453 GDI fallback surface format for Win 11 (21H2)  
* QTBUG-109629 Occasional assertion fail when opening/closing devtools  
* QTBUG-109605 ABI breaks due to marking Qt_6_PRIVATE_API too widely  
* QTBUG-109604 ABI break in QCommonStyle  
* QTBUG-109594 QMetaType::NeedsConstruction might be wrongly set  
* QTBUG-107979 WebAssembly - callback is missing when WebAssembly module  
is ready to receive messages from Javascript  
* QTBUG-103393 IBus input method cannot set panel position correctly  
with DPI scaling  
* QTBUG-109746 tst_QWidget::optimizedResizeMove() and  
optimizedResize_topLevel() with QtWayland failed on Ubuntu 22.04, GNOME  
* QTBUG-109454 Black check/radio boxes and grey background with GTK  
Theme  
* QTBUG-109790 C++ syncqt ignores the wrong line with ELFVERSION:ignore-  
next  
* QTBUG-109619 Enabling 2 extra Android CMake options leads to a build  
error  
* QTBUG-108790 Crash on QFuture::cancel() with continuation and thread  
context  
* QTBUG-109477 QImageReader will cause heap corruption when load jpeg  
(width: 1px height:100px) on Apple M1  
* QTBUG-108639 Reg[6.2->6.4]WebAssembly: Tap is not working on mac with  
trackpad  
* QTBUG-109289 Documentation of QWidget::acceptDrops links to  
GraphicsView  
* QTBUG-109230 Crash in QFuture  
* QTBUG-109875 -Werror=type-limits for  
src/corelib/tools/qoffsetstringarray_p.h:85:27  
* QTBUG-109036 QXcbBackingStore::toImage() returns wrong image.  
* QTBUG-109754 QTextEdit::setTabChangesFocus has no effect  
* QTBUG-109738 Deploying a universal app for macOS fails  
* QTBUG-110002 FAILED:  
qtbase/src/xml/CMakeFiles/qattributionsscanner_XXX  
* QTBUG-109851 moc generates reserved identifiers for scoped classes  
* QTBUG-109610 developer-build fails for xcb  
* QTBUG-109958 tst_qalgorithms should not create unique datatags when  
testing  
* QTBUG-110058 QCryptographicHash is not re-entrant  
* QTBUG-109547 Unnecessary dependency to Qt6QmlTools / qtdeclarative-  
native  
* QTBUG-109159 Cross-compile Qt6. features: sse2  
* QTBUG-109474 6.5: Behavioral change in QTextLine  
* QTBUG-110068 qmake: Generated Visual Studio project defaults  
"GenerateDebugInformation" to "false"  
* QTBUG-109792 C++ syncqt tool should be built like moc  
* QTBUG-109237 [Reg-6.3.1->6.4.1] Calling formLayout->addRow can result  
in assert in Debug builds  
* QTBUG-105544 qunicodetools.cpp: libthai's th_brk is not thread-safe  
[2/2]: new API  
* QTBUG-109678 fatal error LNK1169: one or more multiply defined symbols  
found  
* QTBUG-109745 Static assertion failed with  
QVarLengthArray<std::vector<std::unique_ptr<int>>>  
* QTBUG-109967 Builds fail because of missing permissions libraries  
* QTBUG-84315 QUrl::setAuthority() behavior changes  
* QTBUG-54505 QString::compare( QString &other, ... ) treats Null and  
Empty QStrings as equivalent and returns zero.  
* QTBUG-110268 On macOS, Expose events cannot be filtered with  
QWindowSystemEventHandler  
* QTBUG-109840 QUrlQuery: operator== does not handle a case where  
exactly one object has null pimpl  
* QTBUG-109842 QUrlQuery: missing move constructor  
* QTBUG-110412 Crashes in many qml scenes when using vulkan  
* QTBUG-108183 Crash triggered by assertion in QTextDocumentLayout  
* QTBUG-110513 -no-rpath build fails with CMake 3.16  
* QTBUG-110434 [REG 6.4->6.5] Standard cursor shapes are not updated on  
a secondary screen  
* QTBUG-106533 Android: jar and src dirs are installed in /usr if  
CMAKE_INSTALL_PREFIX=/usr  
* QTBUG-107207 Add support for MultiABI with custom install dir of the  
android-build (patch included)  
* QTBUG-61042 A QML FileDialog shows a warning in a console after  
reseting the 'nameFilters' property  
* QTBUG-77211 Warning on nameFilters change in QML FileDialog  
* QTBUG-110627 Qt doesn't really follow Windows short time format  
* QTBUG-109798 Torrent Client example still broken in Qt6+!  
* QTBUG-64132 QToolButton should elide text when width constraints  
prevent from showing whole text  
* QTBUG-106659 QPrinter : Scaling factor applied wrongly  
* QTBUG-109838 QFontMetricsF::horizontalAdvance seems to do unnecessary  
scanning  
* QTBUG-107185 Some tests appear to be re-testing the exact same data  
tag  
* QTBUG-110744 qdbusxml2cpp generates files with invalid include name  
* QTBUG-108325 QuicControls2 documentations incorrectly suggests to link  
to the library  
* QTBUG-107026 http://matek.hu/xaos/doku.php is dead  
* QTBUG-110070 [REG]Qt crashes on all platforms when trying to paste  
using an empty clipboard  
* QTBUG-109375 [REG.]Widgets lose their focus frame when QProxyStyle is  
set  
* QTBUG-103720 Dragging toolbars across screens with higher scale  
factors has erratic behavior  
* QTBUG-110586 QRegularExpression wrong behavior (behaves differently  
from QRegExp)  
* QTBUG-104836 [Reg 6.3.1 -> 6.4.0b1] Unavoidable "unreachable code"  
warnings from qanystringview.h  
* QTBUG-110432 Checkbox label is white with darkmode on windows  
* QTBUG-110707 Optimization in QMimeDatabasePrivate::mimeTypeForFile  
does not work for Custom File Engines  
* QTBUG-109974 [Reg 6.3.2 -> 6.4] QML Date() does not update its time  
zone after OS time zone had been changed on Windows  
* QTBUG-56595 QXcbConnection::getTimestamp() returns old timestamp  
* QTBUG-109626 Potential race condition in clipboard paste & drop code  
* QTBUG-109518 QPdfWriter loses some of the content if it is positioned  
right  
* QTBUG-110735 Inconsistent QToolTip expire timeout when using rich text  
content  
* QTBUG-110271 Copyright year not updated to 2023 on documentation  
* QTBUG-108822 QDBus: unable to connect the InterfacesAdded signal of  
org.freedesktop.DBus.ObjectManager on the system bus (unless using  
QDBUS_DEBUG)  
* QTBUG-58043 XDG environment variables with relative paths should be  
ignored  
* QTBUG-110979 qdbusxml2cpp6 generates broken code for  
org.freedesktop.DBus.Deprecated  
* QTBUG-111010 Undefined symbols for architecture x86_64:  
"QNetworkProxyFactory::systemProxyForQuery(QNetworkProxyQuery const&)"  
* QTBUG-111007 QRhiGles2 contains non opengles2 call  
* QTBUG-109744 Wrong enum value from QString using Qt 6  
* QTBUG-110941 wasm: MultiPointTouchArea loses all touchpoints after  
just one is released  
* QTBUG-109741 Running qt_generate_deploy_app_script(tgt) must be run in  
the same directory scope as tgt  
* QTBUG-110459 FAILED: src/plugins/position/geoclue2/manager_interface.h  
src/plugins/position/geoclue2/manager_interface.cpp  
* QTBUG-110450 qtpositioning fails to build  
* QTBUG-109864 syncqt call fails  
* QTBUG-110810 Java Files missing from android project tree  
* QTBUG-110468 Qt uses deprecated Windows Layered Service Providers api  
resulting in wall of errors on Windows 11  
* QTBUG-110751 QTextEdit: textBackgroundColor() returns wrong color if  
no color is set  
* QTBUG-110785 QFbCursor memory leak  
* QTBUG-110502 Qt fills in private use unicode if a font is found using  
it  
* QTBUG-109206 QODBC: Reading Time fails when using ODBC Driver 17 for  
Sql Server  
* QTBUG-110967 MySQL Prepared Statement QDateTime: Not Working  
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
* QTBUG-108537 Pointer types in AutoConnections may fail to be queued at  
runtime, but work with QueuedConnection  
* QTBUG-107844 FileDialog: cannot open image picker dialog on iOS  
* QTBUG-107770 no member named 'init' in 'QStyleOption'  
* QTBUG-110816 qmlcachegen fails to find the qtdeclarative libraries  
* QTBUG-111131 setDragEnabled() is breaking interactive item selection  
in QTreeView  
* QTBUG-102010 QScroller prevents QAbstractItemView::DoubleClicked edit  
trigger  
* QTBUG-111268 three dependencies in binding of  
Q_OBJECT_BINDABLE_PROPERTY causes crash  
* QTBUG-111339 OCI plugin wrong query  
* QTBUG-46990 Soft hyphen rendered as space  
* QTBUG-62620 [QtQuick, TextEdit] Soft hypen and incorrectly drawn  
selection  
* QTBUG-67038 Soft hyphens are broken  
* QTBUG-102483 Soft hyphen rendered as space on macOS  
* QTBUG-111347 QMessageAuthenticationCode is not re-entrant  
* QTBUG-110986 QFileSystemWatcher::removePaths() Does not removes drive  
* QTBUG-111388 Crash in QCocoaMenuBar::merged  
* QTBUG-109178 Android Deploy Qt documentation is not up to date  
* QTBUG-98502 QDir::tempPath returns wrong path on Android  
* QTBUG-109511 QtConcurrent in 6.4.0 and later shows undesirable  
behaviour  
* QTBUG-63381 Transient scrollbars do not work when using style sheets  
* QTBUG-111426 iOS example project 'ToDo List' is incorrectly tagged as  
'Android'  
* QTBUG-111467 FTBFS: symbol clash in QCryptographicHash with OpenSSL:  
SHA1 "redeclared as different kind of entity"  
* QTBUG-111170 mouseMoveEvent fired without mouse being really moved  
(Mac only)  
* QTBUG-111275 Inserting a QDate into an Oracle DB with a prepared  
statements fails for timezones like CET  
* QTBUG-111382 Not possible to use TESTDATA for manual tests  
* QTBUG-111498 QPainter::drawImage() broken on big images when OpenGL is  
used  
* QTBUG-111491 Dark Title on Dark Windows 11 when running native Windows  
Style  
* QTBUG-111149 Reg->6.4.2: Windows: Qt Designer freezes when dragging  
actions in QMenu  
* QTBUG-110497 Qt's CMake Config files reset CMAKE_AUTOMOC_MACRO_NAMES  
* QTBUG-108013 QStandardPaths::PicturesLocation paths on Android  
* QTBUG-104892 QStandardPaths::DocumentsLocation on emulated android  
device returning the same directory twice  
* QTBUG-81860 Android: Add "content:" scheme paths to QStandardPaths  
* QTBUG-111416 [REG 6.3.2->6.4.2] Repeated QPainter::drawPixmapFragments  
calls draw images at wrong positions for QOpenGLWidget  
* QTBUG-111443 macOS/iOS: "Detected system locale encoding (US-ASCII,  
locale "C") is not UTF-8"  
* QTBUG-111698 Build fails with -march=amdfam10  
* QTBUG-111524 [REG 6.4 -> 6.5-beta3] Exec'd QMessageBoxes from QMenus  
return immediately on macOS  
* QTBUG-111774 FTBFS: qtbase -DQT_FORCE_FIND_TOOLS=ON fails on CMake:  
Some (but not all) targets in this export set were already defined.  
* QTBUG-111803 Native QMessageBox on macOS doesn't show check box  
* QTBUG-111267 markDirty() does not exist for Q_OBJECT_COMPUTED_PROPERTY  
* QTBUG-111867 QVariant::operator== between QVariant(0) and QString  
* QTBUG-111027 Adding asset pack to package crashes androiddeployqt  
* QTBUG-112016 [REG 6.5.0beta3 -> RC] namespace build fails on MSVC2019  
* QTBUG-111848 WASM: No text input possible  
* QTBUG-112205 QMetaType id of custom QObject subclass unknown prior to  
fetching id from QVariant  
* QTBUG-102041 Android multi-abi builds don't work if the Android  
ndk/sdk install path is different from the CI's one  
* QTBUG-104128 top-level configure is still verbose in a non-developer  
build  
* QTBUG-103714 cut & paste checkboxes: checkbox is lost  
* QTBUG-102771 macOS native style buttons changes implicit sizes even  
after they are completed  
* QTBUG-103923 GCC 12: failure to build from source [<QtBase>]  
* QTBUG-86088 QResource::unregisterResource() function does not remove  
the resource from memory  
* QTBUG-102862 Build failure with lttng enabled  
* QTBUG-104012 QDateTime constructor performance regression when year is  
below epoch  
* QTBUG-99545 App crashes in function QQmlPropertyCache::property(int)  
const on ARM 64bit  
* QTBUG-103753 incorrect document about QDomDocument::setContent()  
* QTBUG-103723 [iOS] CMake shader handling fails  
* QTBUG-68865 tst_QMenuBar::check_menuPosition autotest fails on Ubuntu  
18.04  
* QTBUG-87137 tst_QApplication::sendEventsOnProcessEvents() failed on  
Ubuntu 20.04/22.04 and RHEL 9  
* QTBUG-68860 tst_QGlyphRun::mixedScripts autotest fails on Ubuntu 18.04  
and QEMU builds  
* QTBUG-101177 QTimer random segmentation fault (SIGSEGV)  
* QTBUG-102403 QObject::objectName() leads to heap-use-after-free in  
tst_qquickanimations::cleanupWhenRenderThreadStops()  
* QTBUG-84248 tst_QFont::defaultFamily fails  
* QTBUG-103730 Qt Test tutorial is missing a clear entrypoint  
* QTBUG-103591 Windows: Comboboxes (Qml and QtWidgets) don't have the  
UIAutomation (UIA) ExpandCollapse pattern  
* QTBUG-104450 qmake: it's impossible to configure some compiler and  
linker options in the generated vcxproj  
* QTBUG-97249 Properly support properties with BINDABLE  
* QTBUG-103484 rich text gets converted to monospace in CI because  
QFontDatabase::GeneralFont is "Sans Serif" and is monospace  
* QTBUG-103281 androiddeployqt sets --release always when creating a  
signed package  
* QTBUG-101008 Using Text.NativeRendering results in characters drawn  
too close to each other with fractional scale factors  
* QTBUG-104508 qmlcachegen fails to compile PhotoCaptureControls.qml in  
multimedia  
* QTBUG-104580 androiddeployqt fails with "unknown argument '--libs'"  
when call llvm-readobj v14  
* QTBUG-103593 androiddeployqt doesn't work well with user's QML module  
in their subdirectories  
* QTBUG-102594 [REG 5.15.6 -> 5.15.9] Many ANR issues by QtAccessibility  
* QTBUG-99795 Mouse scroll wheel can't be used to interact with  
scrollable elements on iOS  
* QTBUG-104656 pointer events end up with accepted state == false after  
successful delivery  
* QTBUG-104857 QtBase does not compile with QT_DISABLE_DEPRECATED_BEFORE  
= 0x060000  
* QTBUG-103706 Synthesized touch event not recognized with Widgets  
* QTBUG-104878 xcb wacom support gets confused about device instances  
* QTBUG-104241 tst_QOpenGLWidget::stackWidgetOpaqueChildIsVisible fails  
with Ubuntu 22.04, openSUSE Leap 15.4 and RHEL 9  
* QTBUG-101932 two HoverHandlers with different  
acceptedDevices/acceptedPointerTypes: cursorShape doesn't change  
accordingly  
* QTBUG-97615 CMake cannot find packages when only Qt6_DIR and not  
CMAKE_PREFIX_PATH is set  
* QTBUG-105038 QCollator is limited to ≤ 2Gi characters  
* QTBUG-104787 Thread Sanitizer reports data races in QtConcurrent  
* QTBUG-89702 Improve the QRegExp->QRegularExpression docs  
* QTBUG-102764 [REG: 5->6] Pen / Pencil input devices not working  
* QTBUG-105051 pkg-config does not expose libexecdir for finding some  
tools  
* QTBUG-105201 tst_QWindow::positioning() fails on Android  
* QTBUG-104840 heap-use-after-free in QTest::ignoreMessage  
* QTBUG-105238 Cmake error with -DQT_BUILD_MANUAL_TESTS=ON  
* QTBUG-85248 Qt warning  
"QHttpNetworkConnectionPrivate::_q_hostLookupFinished could not de-queue  
request, failed to report HostNotFoundError"  
* QTBUG-105158 Initialize all Vulkan Device Properties  
* QTBUG-105388 qhash.h:553:17: warning: argument 1 value  
'18446744073709551615' exceeds maximum object size 9223372036854775807  
* QTBUG-66818 tst_QWindow::initialSize fails on Wayland  
* QTBUG-105360 warning C4996: 'QRegularExpression::match': Use matchView  
instead.  
* QTBUG-66371 tst_qmessagebox is flaky  
* COIN-892 Window activation failures on macOS in CI  
* QTBUG-105048 QSqlQuery is supposed to be move-only, however we copy it  
in our code  
* QTBUG-99808 CMake used on a Qt6 project generates a lot of extra  
targets  
* QTBUG-104730 androidtestrunner splits data row names by whitespace and  
treats them as test functions  
* QTBUG-63260 tst_QGraphicsScene::isActive is flaky on openSUSE 42.3  
* QTBUG-105249 tst_QGraphicsView::resizeAnchor() fails occasionally on  
RHEL  
* QTBUG-105247 tst_QGraphicsView::cursor2() is very flaky on macOS  
* QTBUG-62967 tst_QItemDelegate::enterKey(plaintextedit tab) fails on  
openSUSE 42.3  
* QTBUG-63262 tst_QItemDelegate::testLineEditValidation is flaky in  
openSUSE 42.3  
* QTBUG-105736 tst_qfile unixPipe and socketPair tests fail on Android  
12  
* QTBUG-105738 tst_qopengl:: fboRenderingRGB30() fails on Android 12  
* QTBUG-105739 tst_vulkan vulkan11() and vulkanWindowGrab() fail on  
Android 12  
* QTBUG-105596 FAIL!  : TestWebChannel::testPassWrappedObjectBack()  
Compared QObject pointers are not the same  
* QTBUG-103474 Floating dock widgets don't minimize with mainwindow if  
they have been floating initially  
* QTBUG-105469 QVariant::load: unknown user type with name QList<int>  
when running QtRO example  
* QTBUG-103513 A11Y: Flickable child item focus frame position not  
updated  
* QTBUG-103499 Android a11y: Flickable items outside of view are not  
selectable  
* QTBUG-87728 tst_QGraphicsAnchorLayout::layoutDirection() failed on  
Ubuntu 20.04 in CI  
* QTBUG-85912 CBOR API has no example documentation  
* QTBUG-105958 [Android] Intent + Talkback leads to deadlock  
* QTBUG-106018  tst_QSslSocket fails with Ubuntu 22.04 xorg and Windows  
10 21H2 plus OpenSSL 3  
* QTBUG-83185 [Android]: When using night or dark mode on a device, then  
the style extracted is still set as if it is light mode  
* QTBUG-99531 On Some Android device Default locale and System locale  
are different.  
* QTBUG-106389 QT MainWindow Example: context menu no show and All the  
UI has no response  
* QTBUG-90036 QFontMetrics horizontalAdvance has rounding error  
* QTBUG-106597 macOS: QWindow::set(Keyboard/Mouse)GrabEnabled() doesn't  
grab  
* QTBUG-101396 QOpenGLTextureBlitter support for GL_TEXTURE_RECTANGLE  
breaks on some Intel drivers  
* QTBUG-106020 tst_QSocks5SocketEngine::passwordAuth fails with Ubuntu  
22.04 xorg  
* QTBUG-41170 [Android]: When the window resizes then there it will  
cause flicker  
* QTBUG-66727 [Android]: When changing focus between TextInput fields  
there is a flicker of the QQuickWidget  
* QTBUG-84258 tst_Gestures::graphicsItemGesture fails  
* QTBUG-103054 FAIL!  : tst_Gestures::graphicsItemGesture in  
Ubuntu_20_04  
* QTBUG-106071 Example code in QPropertyAnimation documentation has  
memory leak  
* QTBUG-106479 androidtestrunner does not honour QTEST_FUNCTION_TIMEOUT  
* QTBUG-100242 Suspicious test condition for ecmascripttests  
* QTBUG-106154 QtGlobal: update docs after qglobal.h split  
* QTBUG-35409 MouseArea does not detect mouse pointer if it was already  
there on Mac OS X  
* QTBUG-100324 QHelpEvent::globalPos() returns frequently a wrong value.  
* QTBUG-106939 Error: "qmlimportscanner not found" while building  
examples while using cmake  
* QTBUG-96878 Add support for wstring{,_view} to QDebug  
* QTBUG-106233 Suggested fixes in qt_attributions.json for SPDX  
compliance & easier parsing  
* QTBUG-106712 HostPrefix & HostData reference incorrect dir in  
target_qt.conf (when cross compiling)  
* QTBUG-93948 obsolete note about linked openssl  
* QTBUG-106941 no-opengl build fails  
* QTBUG-106925 Context menus on mac os 12.5.1 are resizeable (and not  
native in appearance)  
* QTBUG-107538 OpenSUSE 15.3 developer build with OpenSSL 3 fails:  
‘QSslSocket’ has not been declared  
* QTBUG-107157 tst_QWidget with QtWayland failed on Ubuntu 22.04, GNOME  
* QTBUG-107184 tst_QGridLayout::setMinAndMaxSize() with QtWayland  
crashed on Ubuntu 22.04, GNOME  
* QTBUG-107154 tst_QWidget_window::mouseMoveWithPopup(Dialog) with  
QtWayland failed on Ubuntu 22.04 GNOME  
* QTBUG-107186 tst_QCompleter::showPopupInGraphicsView() with QtWayland  
failed on Ubuntu 22.04, GNOME  
* QTBUG-107158  
tst_QTouchEvent::multiPointRawEventTranslationOnTouchPad() with  
QtWayland failed on Ubuntu 22.04, GNOME  
* QTBUG-107578 tst_selftests failed with qtwayland qpa plugin on Ubuntu  
22.04 GNOME  
* QTBUG-107034 tst_QObjectRace::disconnectRace2 crashes in CI  
* QTBUG-106646 After dependency update to  
ac74b60c9c1101288eb2c558420ba69f675a2ee2,  
tst_qquicktextedit::pasteHtmlIntoMarkdown fails  
* QTBUG-35608 Flickable speed and deceleration does not scale with pixel  
density  
* QTBUG-35609 Flickable speed and deceleration are not easily  
customisable  
* QTBUG-52643 Dragging threshold on high DPI touch devices is too small  
* QTBUG-97055 QQC2 Flickable scrolling is not linear with clicky wheels  
on Qt 6.2.0  
* QTBUG-107167 Qt 6.4 not compatible with Mac App Store  
* QTBUG-106896 QDir::drive() does not shows DVD drive  
* QTBUG-106082 [Qt 3D] QSG_RHI_BACKEND : d3d11 produces unexpected  
results  
* QTBUG-102321 Qt application blocks macos shutdown, restart  
* QTBUG-107782 [Possible regression]: Text drawing errors using  
QPainterPath  
* QTBUG-73251 QTreeview stylesheet "show-decoration-selected" has no  
effect  
* QTBUG-102480 Build fails when examples enabled but Sql and/or Linguist  
are disabled  
* QTBUG-107801 Not all locales use single-character exponent separator  
* QTBUG-107907 QOperatingSystemVersion::Windows10 <  
QOperatingSystemVersion::Windows11 == false  
* QTBUG-107780 Rendering Texture in WebAssembly  
* QTBUG-105753 QDir is not re-entrant  
* QTBUG-91255 [Android] Add support for APK Signature Scheme v2  
* QTBUG-108175 [macOS] Qt warning: "macOS generated a color-profile Qt  
couldn't parse. This shouldn't happen."  
* QTBUG-107604 [Reg 5.15.10 -> 5.15.11] Incorrect fullscreen dimensions  
on some Android devices  
* QTBUG-107709 Android screen size mismatch [Reg 5.15.10 -> 5.15.11]  
* QTBUG-107523 [REG 5.15.10 -> 5.15.11] Android edge-to-edge layout  
broken  
* QTBUG-108188 Meta property writes fail to convert [u]longlong to enum  
* QTBUG-106703 tst_QQuickControl::Material::flickable units for arch  
'applegpu_g13g' are not packed  
* QTBUG-108216 Investigate the QRhi pipeline cache (MTLBinaryArchive  
usage) on macOS 13  
* QTBUG-92468 QTextEdit cursor is drawn incorrectly  
* QTBUG-86823 REG: Blinking cursor leaving an artifact in QTextEdit  
* QTBUG-96288 QTextEdit cursor postion error when QTextEdit has  
different pointsize  
* QTBUG-97125 Assistant is unusable on macOS Dark theme  
* QTBUG-108402 tst_Gestures failures on macOS 13  
* QTBUG-107727 QSystemTrayIcon does not emit the  
QSystemTrayIcon::activated signal on Ubuntu 20.04/22.04 for left click  
and right click.  
* QTBUG-4521 Custom events are processed only after the first  
::processEvents  
* QTBUG-104496 tst_Gestures failures with OpenSUSE Leap 15.4  
* QTBUG-106244 tst_Gestures failures with RHEL 9  
* COIN-966 gnome terminal running bootstrap-agent irritates tests  
* QTBUG-107923 Wrong height of the window on Android  
* QTBUG-108762 Action triggered signal seems to lack source for qmlsc  
* QTBUG-106906 tst_qtcuncurrentrun::pollForIsFinished occasionally  
crashes  
* QTBUG-45502 OSX: Many tests failing in CI for tst_qwidget  
* QTBUG-109135 Qt warning "Failed to create SecCertificate from  
QSslCertificate"  
* QTBUG-109235 Review toupper/tolower uses [Qt]  
* QTBUG-107893 cmake: multi-ABI Android builds do not forward cmake  
arguments  
* QTBUG-105820 windeployqt does not support Qt compiled with -libinfix  
option  
* QTBUG-80417 QDateTimeEdit cannot handle OffsetFromUTC or TimeZone as  
time-spec  
* QTBUG-25071 tst_QDom relies on specific QHash ordering  
* QTBUG-107808 Widget stops being updated when setUpdatesEnabled(false)  
is called before setUpdatesEnabled(true) is completed  
* QTBUG-103620 [Reg 5.15 -> 6.2] Flicking is inconsistent with touch  
screen  
* QTBUG-88506 tst_Android::assetsRead fails on Android  
* QTBUG-88840 No way to pass QT_ANDROID_PACKAGE_SOURCE_DIR for  
qt6_add_executable  
* QTBUG-109553 CMake deployment API creates too deep directory hierarchy  
when DESTDIR is set  
* QTBUG-93955 Material.System does not work on Ubuntu (Gnome)  
* QTBUG-97518 Mac, Metal RHI - runtime warnings "UI API called from  
background thread".  
* PYSIDE-2182 QTimer.singleShot example documentation does not work  
* QTBUG-109857 qt-configure-module not executable for android_armv7 on  
linux host  
* QTBUG-105804 The qt_ntfs_permission_lookup mechanism is prone to data  
races  
* PYSIDE-2191 pyside6-uic fails to correctly generate resource_rc  
location  
* QTBUG-109171 QOpenGLWidget inside QDockWidget produces segfault on  
undocking.  
* QTBUG-110703 tst_QFocusEvent::checkReason_ActiveWindow() fails on  
macOS 13.2  
* QTBUG-91627 [OpenGL] Crash when creating context with contextinfo  
example app on Android  
* QTBUG-110836 include could not find requested file: /home/qt/work/qt/q  
ttools/build/target/lib/cmake/Qt6Core/QtInstallPaths.cmake  
* QTBUG-110356 Building Permissions example for debug with qmake on  
macOS fails  
* QTBUG-109268 QWindow on Android doesn't use full area on some devices.  
* QTBUG-97503 Reg[5.15.2-5.15.6] Android: Keyboard covers the inputfield  
* QTBUG-109351 Bottom Navigation Bar overlaps app window  
* QTBUG-110501 Wrong calculation of display area on android when virtual  
keyboard is present before opening the app  
* QTBUG-109383 Re-enable building examples with qmake in non-qtbase  
repos  
* QTBUG-110952 uic-generated connnection to QLCDNumber::display() fails  
to compile due to overloads  
* QTBUG-110696 Qt6CoreMacros.cmake should take AUTOGEN_BUILD_DIR into  
account  
* QTBUG-110899 Incorrect warning about binding loop in  
QtQuick.Controls.Control  
* QTBUG-110270 Fix CTF backend metadata creation when cross compiling  
* QTBUG-103514 Possible crash in imagescaling example.  
* QTBUG-111140 cross-compilation failures for qtgrpc  
* QTBUG-102474 Sometime SSL leads to hang application on exit  
* QTBUG-109076 WebAssembly - QML - Text - Using Thai characters is  
causing a crash  
* QTBUG-108832 tst_QByteArrayLarge cases fail on Android 12 CI  
* QTBUG-108844 tst_QRhi test cases fail for Vulkan fails on Android 12  
CI  
* QTBUG-111235 tst_QOpenGLWidget::reparentHidden() fails on Android 12  
CI  
* QTBUG-111236 tst_qvulkan cases fail Android 12 CI  
* QTBUG-50278 "threadedqopenglwidget" sample fatal error when resizing.  
* QTBUG-110093 Threadedqopenglwidget example has blank screen  
* QTBUG-76054 android threadedqopenglwidget example blank and has error  
E OpenGLRenderer: void android::uirenderer::renderthread::CanvasContext:  
:setSurface(android::Surface *)  
* QTBUG-43209 Main GUI thread serialises QOpenGLWidget::frameSwapped per  
VSync for multiple application windows  
* QTBUG-111330 error: Not a signal or slot declaration in code generated  
by qt_add_dbus_interface  
  
### qtsvg  
* QTBUG-104203 QSvgGenerator does not sanitize string inputs  
* QTBUG-101698 [REG 6.2.2 -> 6.2.3] Integer overflow when loading svg  
image  
* QTBUG-100068 Colors of some SVG images are wrong  
* QTBUG-104944 QT_DISABLE_DEPRECATED_BEFORE hides wrong APIs  
  
### qtdeclarative  
* QTBUG-103250 Link to ScrollBar's size property is wrong  
* QTBUG-102136 QML Slider: (Lack of) implicitWidth affects background  
height when anchors are used  
* QTBUG-103956 [qmltc] property alias causes "unknown origin" error  
* QTBUG-104026 TypeError warnings from attached property usage in  
tst_qquicklistview  
* QTBUG-104129 qmllint: Type "QList<int>" of property "boo" not found  
* QTBUG-104092 qmlsc tries to look up lower case names as types  
* QTBUG-95993 QML Date operations are wrong when DST is active  
* QTBUG-102971 Something fishy going on on MinGW with QML Date  
* QTBUG-104051 FAIL!  : tst_qqmlnotifier::deleteFromHandler() Compared  
values are not the same  
* QTBUG-104010 qmlcachegen generates inefficient code for conversions to  
string  
* QTBUG-104124 QModelIndexList is declared in QtQml  
* QTBUG-101538 Pointless link to Qt Quick Text Validators page  
* QTBUG-100820 [REG 5.15.2-6.2.3] Wrong rendering of semi-transparent  
text if Text.NativeRendering is used  
* QTBUG-104089 TextEdit has wrong cursor shape on hover  
* QTBUG-101220 qmlsc does not set import paths for libraries  
* QTBUG-99057 Mismatched-new-delete warning when using qmltypes with  
mingw 9.0  
* QTBUG-100644 Document how to properly add javascript files with  
qt_add_qml_module  
* QTBUG-75109 tst_QQuickListView::currentIndex() is failing  
* QTBUG-100554 Qt Quick Calendar: 1st row sometimes contains only days  
from the previous month  
* QTBUG-103832 The delegate item of ListView is not pressed if the  
boundsBehavior is to set Flickable.StopAtBounds  
* QTBUG-103903 QMLLINT: warnings about missing imports with directory  
imports  
* QTBUG-104209 qmllint: Tumbler: attached properties of Tumbler must be  
accessed through a delegate item  
* QTBUG-86088 QResource::unregisterResource() function does not remove  
the resource from memory  
* QTBUG-98914 QML Test with grabImage() fails on iOS  
* QTBUG-101268 ListView does not preserve its relative scrollbar  
position when window is restored down on Windows if height of  
ListView.header changes dynamically  
* QTBUG-101266 Changing ListView.header height dynamically doesn't  
preserve relative scrollbar position when window is Maximized  
* QTBUG-102965 File order of CMake project can break compilation due to  
QMetaTypeId<T> specialization  
* QTBUG-104373 [REG: 6.2->6.3] qt_add_qml_module does not register  
QML_ELEMENT classes if version starts with 0  
* QTBUG-99947 Hidden TextEdit cursor blinking keeps triggering redraw  
when using QQuickWidget  
* QTBUG-103189 qmltyperegistrar: Warn about duplicate exports  
* QTBUG-104079 tst_qqmljsscope::qualifiedName() blocks integration  
* QTBUG-104197 qmllint: unknown attached property scope T.  
* QTBUG-104138 Doc: Wrong link to 'Squish'  
* QTBUG-104430 qmllint: Unexpected type for property  
"columnWidthProvider" expected function got function  
* QTBUG-38765 When propagateComposedEvents is set, drag does not always  
move the flickable  
* QTBUG-74842 Flickable behind MouseArea does not steal first drag event  
after creation  
* QTBUG-98964 No way to disable "Binding on contentItem is not deferred"  
warning when code deliberately doesn't care about deferred execution  
* QTBUG-104470 Text overlap in custom menu  
* QTBUG-104447 qmlsc miscompiles bindings that throw exceptions  
* QTBUG-104462 qmlsc miscompiles JavaScript functions with arguments  
* QTBUG-104523 error: no member named 'offsetsAndSize' in  
'qt_meta_stringdata_TestClass_t  
* QTBUG-101973 File Dialog does not re open in some situation.  
* QTBUG-60909 Unable to reset properties in gadgets  
* QTBUG-104544 When the repeater is used as the contentItem of the menu,  
all items are invisible  
* QTBUG-104366 SparseArray::pop_front() n is shadowed  
* QTBUG-102762 QML_ELEMENT is broken in Qt 6.3.0 on Android  
* QTBUG-104512 Invalid code generated  
* QTBUG-104258 tst_QQuickPopup::Material fails with Ubuntu 22.04  
* QTBUG-104555 Top level builds broken  
* QTBUG-104269 No word-wrap in fallback MessageDialog  
* QTBUG-104508 qmlcachegen fails to compile PhotoCaptureControls.qml in  
multimedia  
* QTBUG-104625 tst_Qmlls::testWorkspace fails  
* QTBUG-104603 Clarify the QML_EXTENDED documentation  
* QTBUG-104156 QML Type Compiler documentation formats unreasonably wide  
* QTBUG-104642 iOS: TextField has blinking cursor, but no input panel is  
showing  
* QTBUG-104094 qmltc could not correctly include QML files with  
QT_QMLTC_FILE_BASENAME specified  
* QTBUG-104257 tst_QQuickMenu(bar) tests are failing with Ubuntu 22.04  
* QTBUG-104242 tst_QQuickDrawer tests are failing with Ubuntu 22.04  
* QTBUG-104379 [REG 6.3.0 -> 6.3.1] Crash when trying to debug QML  
Application  
* QTBUG-104574 qmllint cannot cope with Qt.callLater  
* QTBUG-102559 macOS style focus frame incorrectly positioned  
* QTBUG-104573 DialogButtonBox enums are not known to qmllint  
* QTBUG-104471 tst_QQuickListView2::tapDelegateDuringFlicking fails on  
Android  
* QTBUG-87119 MouseArea inside SplitView item takes mouse events away  
from Splitview handle  
* QTBUG-97385 QtQuick SplitView with Flickable gets stuck  
* QTBUG-104442 QML Image does not rescale on setGeometry() when "layer"  
is enabled  
* QTBUG-104536 [Possible regression]: Rendering errors when using  
layer.enabled: true  
* QTBUG-101439 QQmlComponent is unusable after initial property errors  
* QTBUG-82301 No error when registering C++ singleton and QML singleton  
into the same module name  
* QTBUG-104665 Basic blocks pass wrongly optimizes indirect register  
reads out  
* QTBUG-82591 Object.getOwnPropertyNames() doesn't work with attached  
properties  
* QTBUG-104705 Controls, macOS: FocusRect for TextField is not aligned  
correctly  
* QTBUG-104743 qmlsc crashes  
* QTBUG-104491 mouse event broken after continuous transition animation  
in StackView.  
* QTBUG-104657 Custom ComboBox does not function properly with model  
passed from c++  
* QTBUG-104084 tst_qmldomitem ERROR: AddressSanitizer: alloc-dealloc-  
mismatch  
* QTBUG-104803 Crash when calling QJSValue::hasProperty("x") from Qml on  
a QVector3D received from a Q_PROPERTY  
* QTBUG-104683 qmlsc: Compilation errors with enums  
* QTBUG-101531 qmlsc issue with change signal handler  
* QTBUG-101480 The "Control" can't inherit the palette of  
"ApplicationWindow"  
* QTBUG-98494 tst_qmlformat::testExample times out on  the CI  
* QTBUG-88381 tst_qmltyperegistrar::pastMajorVersion fails on Windows  
MSVC 2019  
* QTBUG-94462 Qt Quick TextEdit.insert() does not process Markdown text  
* QTBUG-104795 SystemInformation singleton has few docs  
* QTBUG-104325 QQuickPointerHandler::currentEvent() exposes stale event  
* QTBUG-101008 Using Text.NativeRendering results in characters drawn  
too close to each other with fractional scale factors  
* QTBUG-99174 tst_qquickimageprovider Failed  
* QTBUG-99175 tst_QSequentialAnimationGroupJob::  
groupWithZeroDurationAnimations is flaky on macos ARM  
* QTBUG-99149 tst_qqmlxmlhttprequest::redirects failing on macOS arm in  
CI  
* QTBUG-100313 Support value type lists in qmltc  
* QTBUG-98769 QML StackView heap-use-after-free on pop()  
* QTBUG-104865 QQuickPaddedRectangle emits topPaddingChanged incorrectly  
* QTBUG-103746 QML javascript URL does not add a colon at the end of  
protocol field  
* QTBUG-98936 Can't use Apple Pencil with Qml controls  
* QTBUG-102764 [REG: 5->6] Pen / Pencil input devices not working  
* QTBUG-103937 QML WebEngineView - Wacom pen not works  
* QTBUG-104706 qmllint does not recognize JS array functions on  
QQmlListProperty  
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
* QTBUG-104780 Assertion failure when using "anchors.fill: parent" in  
tests/auto/qml/qmltc/QmltcTests/delegate_context.qml  
* QTBUG-104749 qmlsc: QQuickAnchors Q_PROPERTIES are not FINAL  
* QTBUG-105164 ScrollView consumes wheel events even when 'wheelEnabled'  
is set false  
* QTBUG-104468 [qmltc] -Waddress warnings  
* QTBUG-91687 QML fails to run benchmarks in qmlbench's v8bench  
directory  
* QTBUG-58559 Deletion of a dynamic properties to JSObject ends up using  
all memory  
* QTBUG-105252 [QML] Compiler does not accept boolean type cast  
* QTBUG-105188 Instruction "generate_BitOr" not implemented  
* QTBUG-94983 Crash when binding to aliased grouped property  
* QTBUG-92192 Issues calling JSON.stringify() on objects  
* QTBUG-105468 tst_rendernode autotest is useless  
* QTBUG-105361 qmlformat: Unnecessary replacement of 'let' with 'var',  
leading to inline write errors  
* QTBUG-105239 Split "Module Definition qmldir Files"'s table  
* QTBUG-105360 warning C4996: 'QRegularExpression::match': Use matchView  
instead.  
* QTBUG-105566 Touch panning a ListView in View3D broken  
* QTBUG-105058 PathView steals touch event of PinchArea delegate  
* QTBUG-104983 [REG] 908aa77d16e00f2bccc0ddae0f8b61955c56a6a1 breaks  
scrollbars if contentItem is accessed before it is set  
* QTBUG-105570 TreeViewDelegate: cannot perform selections  
* QTBUG-105682 [REG 6.4.0 beta1 -> beta3] quick3d/principledmaterial not  
compiling on iOS  
* QTBUG-105601 [REG 6.3.2->6.4.0] texteditor fails to compile on Wasm  
* QTBUG-105254 [QML] Compiler complains about namespaced QML_ELEMENTS -  
sometimes  
* QTBUG-95232 Qt Quick Local Storage does not work with absolute paths  
* QTBUG-105611 tst_cursor fails often on webOS  
* QTBUG-89567 [REG 5.15.0 -> 5.15.1] Qt.labs.platform.MenuItem is  
triggering shortcut even in disabled state  
* QTBUG-105572 Wrong image in documentation for eventcalendar example  
* QTBUG-104022 tst_SignalSpy::testCount fails in CI on macOS  
* QTBUG-98350 QuickTest runs test suites in parallel, causing crashes  
* QTBUG-105208 REG: Selecting text inside a TextEdit causes existing  
lines to disappear and empty lines to appear.  
* QTBUG-105555 REG: Text selection in the text editor example causes the  
text document to reposition the blocks after the selection  
* QTBUG-105728 REG: TextArea & TextEdit breaks when selecting text with  
mouse  
* QTBUG-103819 QML TextEdit memory usage is extreme and the memory is  
not freed  
* QTBUG-101932 two HoverHandlers with different  
acceptedDevices/acceptedPointerTypes: cursorShape doesn't change  
accordingly  
* QTBUG-103925 Accessing `byteLength` on an ArrayBuffer constructed from  
an empty QByteArray throws error  
* QTBUG-105907 Use the time stamp of the touch event when deliver touch  
as mouse  
* QTBUG-105812 Small typo in Accessible.description documentation  
* QTBUG-105899 ColorDialog: The text fields on ColorInputs.qml are buggy  
for the Fusion, Imagine and Universal styles.  
* QTBUG-104966 The Items in the ListView is not showing when the model  
is changed during dragging  
* QTBUG-105590 qmllint warns about enum values of ScrollBar  
* QTBUG-104928 qmlimportscanner: segfault on unexpected argument  
* QTBUG-95864 ListElement: cannot use script for property value  
* QTBUG-93603 Document that mixing old/new forms in QML Connections  
causes new form to not work  
* QTBUG-92068 Remote loading ui files in Qml fails to load from existing  
directory  
* QTBUG-96779 Overhaul basic type documentation  
* QTBUG-105992 Changing FontLoader font causes timer errors  
* QTBUG-96631 Unexpected syntax error when declaring a class inside  
another class  
* QTBUG-104556 Crash when accessing enum from QML  
* QTBUG-105608 Crash using enums  
* QTBUG-105535 When PropertyChanges transitions to a constant value with  
a PropertyAnimation, the binding from previous state is still active  
* QTBUG-105941 Failure to decode ETC2 texture (*.pkm file) if downloaded  
over HTTP  
* QTBUG-105860 REG: Dialog box and action bar buttons missing in  
texteditor example  
* QTBUG-104982 [Regression] binding stops being evaluated  
* QTBUG-106110 PinchHandler.minimum/maximumScale properties aren't  
enforced with native gestures  
* QTBUG-106098 ComboBox: The implicitContentWidthPolicy property doesn't  
work for the Imagine style  
* QTBUG-105901 QJSEngine::registerModule not respected under qml  
* QTBUG-106119 Crash when calling findChild from TestCase  
* QTBUG-103900 ColorDialog: Implement the ColorInputs.qml component in  
C++  
* QTBUG-104629 QML FolderDialog: CurrentFolder is not correctly  
* QTBUG-106256 qml crash when binding alias to property  
* QTBUG-106347 Build warns about QML code in C++ header with extension  
".hh"  
* QTBUG-104077 Build failure in 3rdparty/masm/assembler/ARM64Assembler.h  
* QTBUG-93188 tst_qqmlecmascript::gcCrashRegressionTest fails with ARM  
macOS 11 in Qt Declarative  
* QTBUG-98479 QObject that was previously exposed to QML as a const  
pointer remains frozen  
* QTBUG-101298 Extending the Error class errors when trying to overwrite  
the `name` property  
* QTBUG-84341 ECMAScript / Javascript Engine builtin objects are  
immutable (frozen)  
* QTBUG-106391 assertion failure in  
QQuickItemPrivate::localizedTouchEvent  
* QTBUG-104535 REG: Android's Back button does not close QQC2 Dialogs  
anymore  
* QTBUG-101488 tst_QQuickFileDialogImpl is flaky  
* QTBUG-106392 Alias is invalid when accessed from C++ via  
QObject::property()  
* QTBUG-106042 QtQuick.Controls creates delegates in separate contexts  
* QTBUG-105110 Android: FileDialog not working - unable to select file  
correctly  
* QTBUG-102339 Conan: multiple prefixes not supported when building e.g.  
examples  
* QTBUG-106457 Assert on invalid code  
* QTBUG-106357 crash in QIntrusiveListNode::remove() when pinch-zooming  
in QtPDF on iOS  
* QTBUG-106465 ToolTip::test_activateShortcutWhileToolTipVisible is  
flaky  
* QTBUG-106491 tst_QQuickMenu fails on webOS  
* QTBUG-106557 QuickControls Texteditor fails to launch on embedded  
devices  
* QTBUG-106553 Quick styled text processes HTML case sensitively (this  
is wrong)  
* QTBUG-106594 Text baseline anchor not updating properly  
* QTBUG-106566 qmllint crashes on invalid alias property  
* QTCREATORBUG-27655 Qt Quick Controls – Chat Tutorial not working  
* QTBUG-106604 Multiple Qt Quick Sliders repaint incorrectly in macOS  
* QTBUG-106548  [REG 6.2.4 - 6.3.2] HoverHandler "eats" all hover events  
even when disabled  
* QTBUG-106611 qml: signals cannot use inline components as argument  
type  
* QTBUG-106547 qml: deprecate top-level Components  
* QTBUG-95628 Question about the performance of method calls  
* QTBUG-35409 MouseArea does not detect mouse pointer if it was already  
there on Mac OS X  
* QTBUG-46460 MouseArea.containsMouse doesn't revert to false if enabled  
is set to false  
* QTBUG-106114 tst_qmltc_examples fails on webOS  
* QTBUG-106613 qmllint crash due to index out of range  
* QTBUG-106887 CMake does not pass --private-includes to  
qmltyperegistrar if the QML module target is the private library itself  
* QTBUG-106824 Bad casts in qquickshapegenericrenderer.cpp  
* QTBUG-106612 qmllint hits assert related to inline components  
* QTBUG-105192 Loader3D crashes when active property is dynamically  
changed  
* QTBUG-106704 HoverHandler and MouseArea: if hover is enabled/disabled  
but mouse does not move AND no item is marked dirty, state doesn't  
change immediately  
* QTBUG-80508 QSGGuiThreadRenderLoop uses single context for all windows  
* QTBUG-106705 qsTr context truncated on filename with multiple dots  
(ie. Foo.1.0.qml)  
* QTBUG-106690 FileDialog's selectedFile is wrong when going up a  
directory  
* QTBUG-107047 TypePropagator cannot handle optional chaining call  
* QTBUG-100242 Suspicious test condition for ecmascripttests  
* QTBUG-107014 [REG 6.2.4 -> 6.2.5] Items covered by Popup receive mouse  
events  
* QTBUG-107077  
tst_qquickdeliveryagent::undoDelegationWhenSubsceneFocusCleared fails  
* QTBUG-107078 qt_add_qml_module cannot exclude files from compilation  
* QTBUG-107080 qmlcachegen assertion failure  
* QTBUG-106864 Reg-5.15.9->5.15.10: Android crash on startup on armv7  
(32bit) devices  
* QTBUG-106269 Qt Quick apps immediately crash under Android 6  
* QTBUG-107091 [qmltc] repeater generates invalid code  
* QTBUG-107208 [Reg 5.15 -> 6.x] QQmlApplicationEngine::retranslate()  
doesn't work for ComboBox and ListView  
* QTBUG-107472 testhttpserver_p.h:18:10: fatal error: QTcpServer: No  
such file or directory  
* QTBUG-107038 Non-aliased Text is rendered incorrectly using  
NativeRendering  
* QTBUG-107533 [qmltc] live-lock when resolving multi-level alias  
properties  
* QTBUG-107534 [qmltc] cannot resolve alias into component  
* QTBUG-107176 cachegen eats all memory and fails  
* QTBUG-107542 qmlcachegen infinite loop with certain statements  
* QTBUG-107619 V4: Memory corruption due to unchecked length usage  
* QTBUG-107536 qsTranslate not working in ListElement  
* QTBUG-107250 qmllint crashes with fuzz input  
* QTBUG-106819 qmlcachegen miscompiles value type references  
* QTBUG-107264 TapHandler.singleTapped is emitted immediately before we  
know whether a double-tap will occur  
* QTBUG-65088 TapHandler: detecting double-clicks is not declarative  
enough  
* QTBUG-105055 -Wshorten-64-to-32 warnings in private headers  
* QTBUG-106645 "TypeError: Cannot read property of null" error in "QML  
Dynamic View Ordering Tutorial 1" example  
* QTEXT-7 TreeView: crash (as opposed to only runtime warning) if  
keyword "required" is not satisfied  
* QTBUG-107594 Crash when rendering emojis with NotoEmoji font  
* QTBUG-89933 tst_HoverHandler fails with macOS 10.15 and Xcode 12.3  
* QTBUG-99766 QML value type write-back support is inconsistent  
* QTBUG-107013 Wheel scroll event propagated from a modal dialog to the  
dialog below (Quick)  
* QTBUG-104960 DelegateModel is only 1 dimensional  
* QTBUG-78153 tst_qquickmousearea::nestedStopAtBounds() is flaky on  
OpenSuse 15.0  
* QTBUG-107772 Using ShaderEffect with inline-declared 'source' will  
crash on exit in dev  
* QTBUG-103939 Text editor example  Font bold/Italic etc. attributes not  
working  
* QTBUG-39806 MouseArea press is not canceled when enabled becomes false  
* QTBUG-103788 Disabling parent of MouseArea in onPressed gets stuck  
with mouse but not through touch  
* QTBUG-95225 When the D3D11 RHI backend is used then a white line can  
appear at the border when there is an odd number of pixels in either  
width or height  
* QTBUG-103877 TreeView from Qt 6.3 is not re-sorted when  
dynamicSortFilter is set in the QSortFilterProxyModel  
* QTBUG-104526 text in TextArea disappear when scrolling up large text  
by using scrollbar button "up"  
* QTBUG-106579 qmllint does not warn about duplicated properties and  
signals  
* QTBUG-106159 wasm: Image downloading anything external does not work  
even though the request succeeds in multithreaded apps  
* QTBUG-99887 TapHandler on TextField (for showing right click context  
menu) stops working in Qt6  
* QTBUG-105609 should be able to add a TapHandler to a Button to modify  
behavior  
* QTBUG-105610 should be able to add a DragHandler to a Button or other  
control  
* QTBUG-107837 HorizontalHeaderView has wrong column sizes  
* QTBUG-107691 ShaderEffectSource/layer always accounts for high DPI in  
textureSize, cannot work with pixels (Incorrect image when layer.enabled  
is true)  
* QTBUG-103620 [Reg 5.15 -> 6.2] Flicking is inconsistent with touch  
screen  
* QTBUG-106646 After dependency update to  
ac74b60c9c1101288eb2c558420ba69f675a2ee2,  
tst_qquicktextedit::pasteHtmlIntoMarkdown fails  
* QTBUG-105506 Inconsistent mix of numerals in calendar with Arabic  
* QTBUG-107685 qmlformat creates temp file with trailing "~" which is  
not removed  
* QTBUG-103268 QML item Menu doesn't close with touch screen on  
CloseOnPressOutside  
* QTBUG-99276 Fusion style sets button text color to white automatically  
* QTBUG-105741 Popups can be behind dialogs and other popups  
* QTBUG-107703 QML MenuBar : "Alt" does not activate/focus the first  
Menu  
* QTBUG-77902 MouseArea does not get fake right click on touchscreen  
* QTBUG-107867 QQuickSliderPrivate::handleUngrab() is called during  
multi-touch on QQuickSlider  
* QTBUG-106106 Crash in ~QQuickScrollBarAttached during rearrange of  
QQmlDelegateModel  
* QTBUG-108026 Memory leak when capturing a 3D scene using  
QQuickItem::grabImage  
* QTBUG-107254 Crash when assigning non existing properties  
* QTBUG-71922 Mime data is corrupted when using QQuickDragAttached and  
it's not UTF-8  
* QTBUG-107818 Sometimes ShaderEffect types are not be drawn correctly  
on 2 QQuickWindows  
* QTBUG-106940 "QML Import could not be resolved in any of the import  
paths: shared" when trying to QML debug example "emitters"  
* QTBUG-74496 Performance issue: rejected drag re-triggers drag enter  
event every frame while mouse moves  
* QTBUG-106708 Critical Javascript evaluation order error  
* QTBUG-106602 extending-qml example is missing QtQuick dependency in  
CMakeLists.txt  
* QTBUG-107989 Aliasing occurs at the image boundary if add Scale  
Animator to nine-patch image  
* QTBUG-98979 ListView scrolling is broken for ListView.SnapOneItem mode  
* QTBUG-108252 Crash occurs when GUI thread accesses QRhi objects  
created by Renderer Thread  
* QTBUG-107480 Typo in the document  
* QTBUG-107774 madvise() terminates application due to EBADF code  
* QTBUG-106884 Typo in the document  
* QTBUG-94619 Qt.labs.platform.Menu opens at the wrong location with  
scaling enabled  
* QTBUG-94783 Popup menu in incorrect position when using  
QT_SCALE_FACTOR=1.5 on Wayland Ubuntu  
* QTBUG-107171 qmlsc: Cannot resolve type annotations for args of type  
list<T>  
* QTBUG-107092 [qmltc] custom QQuickItem not found  
* QTBUG-108298 Crash using ConicalGradient in a ShapePath  
* QTBUG-106875 Segfault when Loader is trying to load a file that  
contains the Loader  
* QTBUG-108352 tst_touchmouse::strayTouchDoesntAutograb is flaky  
* QTBUG-77428 Block-scoped variable declaration is hoisted in QML  
* QTBUG-108362 DTZ checks are broken in QML  
* QTBUG-105226 GCC 13 produces -Wstringop-overflow= warning for  
qv4vme_moth.cpp  
* QTBUG-104047 Qt Quick: Drag event coordinates wrong in Release mode  
* QTBUG-104716 draganddrop example issues  
* QTBUG-61652 Android's virtual keyboard "OK" button must not accept the  
QDialog  
* QTBUG-108549 PinchHandler.scale loses the accumulated scaling if  
target == null  
* QTBUG-92064 PinchHandler target scale jumps when pinching a second  
time via native gesture  
* QTBUG-104890 PointHandler deactivated on touch screen  
* QTBUG-105479 [Reg 5.15 -> 6.x] qmlformat: Blank line between sections  
no longer enforced  
* QTBUG-108627 Assertion in QQmlPropertyData::setOverrideIndex  
* QTBUG-108441 Function call with destructured argument silently aborts  
compilation  
* QTBUG-108651 Property change detection for null values doesn't seem to  
be working  
* QTBUG-108646 Segmentation fault when inspecting QML objects without  
breaking  
* QTBUG-83890 [REG 5.14.1->5.14.2,5.15] Horizontal Scrollbars in  
ScrollView when Flickable fits  
* QTBUG-108634 Invalid code generated for comparison  
* QTBUG-108388 code snippet in the document is incomplete  
* QTBUG-108630 StandardButtons types  
* QTBUG-108704 QQmlGadgetPtrWrapper is dangerous  
* QTBUG-107607 Crash when trying to inspect "this.parent"  
* QTBUG-108913 ->6.4.1: Restore qmllint JSON Output Message  
* QTBUG-108684 Loader and ComponentBehaviour Bound seem incompatible  
* QTBUG-108291 `required property` fail only for last object  
* QTBUG-108697 Program can crash when Connections target is destroyed  
* QTBUG-26278 Need Qt.createComponent overload which takes a typename  
* QTBUG-108906 Update dependencies on 'dev' in qt/qtinterfaceframework  
failed  
* QTBUG-109010 top-level build: automoc broken yet again in 6.4 branch  
(depending on moc before it's built)  
* QTBUG-108851 qmlsc pastes whole file to stderr  
* QTBUG-109002 [PinchHandler] Dragging a target is not functional  
* QTBUG-108213 Unexpected visibleChanged signals on QQuickItem  
destruction  
* QTBUG-109005 argumentConversion.qml is subtly miscompiled  
* QTBUG-107079 [qmltc] dash in filename breaks compilatino  
* QTBUG-109048 qmlsc crashes with enum method parameters  
* QTBUG-108994 qml: signal handler crash on wrong arguments  
* QTBUG-109029 When an empty key is added to a QQmlPropertyMap then it  
will add a new entry even if there is an existing empty key entry  
* QTBUG-109200 Shape with QT_QUICK_BACKEND=software crashes sometimes  
* QTBUG-109007 [REG 6.3->6.4] lost the ability to test  
HandlerPoint.pressedButtons (flags) using & operator  
* QTBUG-109197 crash in qmlcachegen  
* QTBUG-108762 Action triggered signal seems to lack source for qmlsc  
* QTBUG-109109 Inconsistent behavior regarding C++-based types in the  
implicit import  
* QTBUG-108831 Some Rectangle borders are double the width with  
fractional scale ratios  
* QTBUG-108182 QML stack bounds checking is unreliable  
* QTBUG-109144 qmllint crashes with annotated function parameter  
* QTBUG-109164 [REG 6.2.5 -> 6.4.0] qmlcachegen crash when attempting a  
'Copy sequence'  
* QTBUG-107492 Typo in the document  
* QTBUG-109422 Wrong moduleheader for QuickControls  
* QTBUG-105312 REG: SplitView no longer works with touch  
* QTBUG-109196 Changes assigning into array property  
* QTBUG-109147 Methods returning lists of builtins cannot be used from  
C++  
* QTBUG-109021 Compiler warns about signal for properties starting with  
"on"  
* QTBUG-102201 DragHandler has unexpected behavior when unaccepted  
button is pressed during drag  
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
* QTBUG-98355 SpinBox text not clipped when larger than available width  
* QTBUG-108713 Native font rendering in some cases misses letters  
* QTBUG-109140 [REG: 5->6] Slowly dragging Tumbler causes numbers to  
jump around  
* QTBUG-105148 Rotated qml combobox popup placed incorrectly  
* QTBUG-109542 TreeView: TreeView.modelIndex() has the order of row and  
column swapped  
* QTBUG-98991 Add example to clear up common layout confusion  
* QTBUG-108798 Dynamically creation of MenuItem  
* QTBUG-101736 QQuickWidget: button in a popup doesn't receive touch end  
event  
* QTBUG-108102 Ensure the bindings in the base type are available  
* QTBUG-108024 [Non-qmlsc] `State.when` evaluation fails when an object  
is bound  
* QTBUG-104768 Overlay is not available when hardcoding the style  
* QTBUG-109299 Overlay seems to be unknown to the typesystem  
* QTBUG-109585 [Reg 6.4->6.5] Assertion when referring to C++ methods  
* QTBUG-109584 [Reg 6.3 -> 6.4] Cannot assign QVariantList to lists of  
other value types anymore in QML  
* QTBUG-109562 qmlplugindump (deprecated) crashes on dev build  
* QTBUG-109597 Seg fault in QQmlObjectCreator::finalize when creating  
QML object with initial bindings  
* QTBUG-96351 QML: strange "Binding loop detected" warning  
* QTBUG-108632 Cannot generate efficient code for equality comparison on  
non-primitive types  
* QTBUG-109854 [REG 6.2.4 -> 6.2.5] QQuickImageProvider doesn't scale  
properly if Image size is not set on High DPI displays  
* QTBUG-109377 Add equality comparison ability for QObject * vs null and  
undefined  
* QTBUG-100010 qtdeclarative/src/qml/jit/qv4assemblercommon_p.h needs  
Q_OS_SOLARIS support  
* QTBUG-102777 6.3: Warnings in examples/quickcontrols2/texteditor  
* QTBUG-96700 Strikethrough formatting changes to underline.  
* QTBUG-97594 Mac - Strikeout bugged in QML TextEdit for Japanese  
* QTBUG-108610 HorizontalHeaderView & VerticalHeaderView does not  
disconnect from QQmlTableModel::headerDataChanged and can crash app  
* QTBUG-106931 Windows: Dark Mode: Fusion style: Menu separator & check  
box  
* QTBUG-109739 QSGBatchRenderer calc for Z positioning results in  
negative value on Apple M1 chips clipping the top most element.  
* QTBUG-104643 qmlls leaks memory  
* QTBUG-109867 Divergent runtime behaviour of QJSPrimitiveValue when it  
is aot-compiled and when interpreted  
* QTBUG-90480 Not all overloads of Qt.matrix4x4 are listed  
* QTBUG-109760 qmlWarning is documented as being in qqmlengine.h, but  
it's actually in qqmlinfo.h  
* QTBUG-28981 Date.setDate does nothing  
* QTBUG-110023 Mouse Wheel broken inside Popup opened from a modal Popup  
* QTBUG-110242 tst_menu.qml is flaky on webOS  
* QTBUG-109882 ShapePath: Switching from a transparent colour to a non-  
transparent one causes the wrong colour to be displayed  
* QTBUG-109567 Masked MouseArea containsMouse value incorrect after  
visibility changes  
* QTBUG-104582 -1 * 0 is not -0  
* QTBUG-104576 qmllint does not like accessing other items from  
Repeaters  
* QTBUG-104632 qmllint gives "Unqualified access" warning without  
further explanation  
* QTBUG-106562 qmllint crashes derefencing a nullptr  
* QTBUG-108664 TableView positions incorrectly  
* QTBUG-110247 macOS: The macOS style falls back to the Basic style  
rather than the Fusion style  
* QTBUG-106869 QML_SEQUENTIAL_CONTAINER and QT_QMLCACHEGEN_DIRECT_CALLS  
are undocumented  
* QTBUG-109074 qmlformat removes (extra)comments  
* QTBUG-110112 Runtime qml won't load certain root elements  
* QTBUG-107797 linux: File selectors cannot be used  
* QTBUG-102344 PAST_MAJOR_VERSIONS doesn't work correctly  
* QTBUG-104899 QML(_NAMED)_ELEMENT should generate a clear error if the  
type in not default constructible  
* QTBUG-109221 Inconsistencies regarding list and value type property  
manipulations  
* QTBUG-95448 Re-add QQmlExtensionPlugin documentation  
* QTBUG-110585 Including QJSPrimitiveValue breaks consumer builds with  
-fno-operator-names  
* QTBUG-103044 tst_qmlcppcodegen on Android complains module  
"Qt.labs.folderlistmodel" is not installed  
* QTBUG-110438 QML_SEQUENTIAL_CONTAINERS and assignment to QML property  
does not work  
* QTBUG-110590 tst_qquickpixmapcache is unstable on linux  
* QTBUG-110628 [Reg 6.2 -> 6.4] Binding does not accept local signal  
handlers anymore  
* QTBUG-54860 When moving the mouse quickly over items that have a  
Behavior set on font size changing when the mouse is over it then it can  
get stuck in the mouse over position  
* QTBUG-108155 QmlEngine complains binding of QmlListProperty to QList  
<QObject *>  
* QTBUG-110117 Building tst_qmlsplitlib fails  
* QTBUG-110321 qmlformat runs into an issue with ES classes  
* QTBUG-110793 tst_qqmlvaluetypeproviders::date fails in CI  
* QTBUG-110697 Cannot use ListView.highlight when ComponentBehavior:  
Bound  
* QTBUG-110320 qmllint: Controls2.Action is not defined  
* QTBUG-91390 ListModel doesn't keep objects of JavaScriptOwnership  
alive  
* QTBUG-95895 REG 5.15 -> 6.2: destroy() does not destroy objects after  
appending listModel.  
* QTBUG-96167 Ownership of C++ owned object flips when added to  
ListModel  
* QTBUG-110769 REG: Compiled QML yields wrong result for undefined ==  
null  
* QTBUG-106074 Add and explain naming conventions and restrictions for  
files in QML  
* QTBUG-110882 QQmlApplicationEngine::loadFromModule does not handle  
pure QML modules  
* QTBUG-109204 Obsolete linter/compiler errors on Number.EPSILON  
* QTBUG-110906 MultiPointTouchArea signals have touchPoints arguments  
which conflict with touchPoints property  
* QTBUG-110831 Compile-time warnings in Qt Quick Controls - Attached  
Style Properties Example  
* QTBUG-105251 [QML] PropertyChanges can't resolve property types  
* QTBUG-75954 Flipable draws incorrectly when rotated and the angle is  
45°  
* QTBUG-110815 Internal types are both public and internal in generated  
qmldir file  
* QTBUG-110767 uint64_t and quint64 are treated differently in QML  
* QTBUG-110808 Cyclic dependency fails  
* QTBUG-110111 [Reg 6.3.2 -> 6.4.x] DropShadow: Changing radius to 0 at  
runtime causes a crash when attached to Canvas  
* QTBUG-106030 Updates docs to let people know if and when they should  
(not) use setContextProperty and what alternatives are  
* QTBUG-110833 qmlsc fails to detect import usage  
* QTBUG-111048 tst_qqmllocale::toString(locale.toString(new Date(2000,  
1, 1))) Compared values are not the same  
* QTBUG-110454 Javascript URLSearchParams does not encode query  
parameters  
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
* QTBUG-99355 tst_qmltc::listView() is flaky under qemu  
* QTBUG-101342 tst_qmltc::listView() is flaky under QNX qemu and Android  
* QTBUG-107902 "Defining QML Types from C++" lacks CMake documentation  
* QTBUG-111199 FAIL!  : tst_controls::iOS::SelectionRectangle  
* QTBUG-111210 Unblacklist tst_controls::iOS::SelectionRectangle test  
cases  
* QTBUG-111204 PinchHandler native-gesture scaling is no longer  
cumulative  
* QTBUG-111179 Incorrect coercion to number for undefined  
* QTBUG-111290 (qdoc) warning: Undocumented parameters in  
TableView::positionViewAtIndex()  
* QTBUG-111289 (qdoc) warning: Undocumented parameter 'resourceState' in  
QNativeInterface::QSGD3D12Texture::fromNative()  
* QTBUG-110914 Deprecated Qt.labs.settings do not link to new QtCore  
alternative  
* QTBUG-95324 JSON.stringify: replacer's `this` value is not conforming  
* QTBUG-111340 stdlib precondition violation in qmlcachegen  
* QTBUG-110594 containsMouse of MouseArea is always true after pressed  
with propagateComposedEvents  
* QTBUG-111381 QML plugins have wrong RUNPATH if CMake var  
INSTALL_QMLDIR is changed  
* QTBUG-105545 [QML] Property of QVariantMap cannot be found  
* QTBUG-111477 [REG 6.4->6.5] Purchasing Example will not compile on  
Windows: QQmlTypeNotAvailable breaks check for default constructor  
* QTBUG-111566 Docs: Faulty sample code in the documentation of  
SwipeDelegate QML Type  
* QTBUG-104761 acceptedButtons in DragHandler is apparently ignored  
* QTBUG-111470 Regression: cannot use QML_ANONYMOUS and QML_UNCREATABLE  
at the same time  
* QTBUG-111433 Pragma (pragma ComponentBehavior: Bound) doesn't allow  
ListView to be instantiated when section configured within it  
* QTBUG-111511 Object destructuring breaks qmlformat  
* QTBUG-111042 QML cache files are re-generated all the time when they  
contain inline components  
* QTBUG-111515 New Material 3 TextField placeholder text does not work  
with smaller heights  
* QTBUG-108896 [REG 6.2.4-6.3.2] Using PinchHandler for Flickable's  
child makes the Flickable transparent for touch events  
* QTBUG-111559 Loader with States creates 2 children instead of 1  
* QTBUG-111881 Incorrect example in  
QQmlApplicationEngine::objectCreationFailed documentation  
* QTBUG-111481 It is really hard to find the new Qt 6.5 qml MultiEffect  
in the docs  
* QTBUG-111986 qmlsc generates invalid code  
* QTBUG-74020 PointHandler documentation examples refer to TapHandler  
not PointHandler  
* QTBUG-106878 PointHandler documentation examples refer to TapHandler  
not PointHandler  
* QTBUG-102862 Build failure with lttng enabled  
* QTBUG-101440 QQmlComponent can't use JS types for initial properties  
* QTBUG-102595 Builds can't find the projects qml modules  
* QTBUG-103926 Undefined Qt.Key_* in javascript files if import or  
pragma  
* QTBUG-93766 Confusing omissions in docs about the QML Compiler  
* QTBUG-104157 Delegate Controls documentation: Introduction and details  
out of sync  
* QTBUG-97092 spelling errors reported by lintian  
* QTBUG-99578 Global Functions are Undocumented  
* QTBUG-86729 many Qt Quick test failures after input event refactoring  
* QTBUG-89927 tst_qquickfontloader::changeFontSourceViaState fails with  
macOS 10.15 and Xcode 12.3  
* QTBUG-104687 qmlsc miscompiles registers only set in in one of two  
alternative branches of execution  
* QTBUG-102984 tst_QQmlDebugJS hangs on macOS in CI  
* QTBUG-101678 tst_qqmlinspector (and other tests in  
tests/auto/qml/debugger/) times out on macOS 12 (x86_64) in CI  
* QTBUG-10684 Interaction between text input and flickable is lacking  
* QTBUG-97249 Properly support properties with BINDABLE  
* QTBUG-94919 Control changes hover state even though it is disabled  
* QTBUG-90494 TextField selectByMouse flag is by default set to false  
* QTBUG-105190 tst_QQuickListView2::flickDuringFlicking is flaky  
* QTBUG-105149 QML ComboBox displays an unwanted shadow effect on  
Android  
* QTBUG-105238 Cmake error with -DQT_BUILD_MANUAL_TESTS=ON  
* QTBUG-105277 Issues with changing mipmap for image elements  
* QTBUG-105354 QSGRenderNode / View3D's Inline mode has no way to gain  
access to the render target/pass descriptor when within an item layer  
* QTBUG-69883 Document default property values for QML  
* QTBUG-103513 A11Y: Flickable child item focus frame position not  
updated  
* QTBUG-104858 QT_DISABLE_DEPRECATED_BEFORE is not propagated to unit-  
tests  
* QTBUG-99808 CMake used on a Qt6 project generates a lot of extra  
targets  
* QTBUG-105937 ProgressBar draws progress incorrectly  
* QTBUG-105102 qt_internal_add_tool and qt_internal_add_app does not get  
the value of QT_DISABLE_DEPRECATED_BEFORE  
* QTBUG-101499 FAIL!  : tst_QQuickMultiPointTouchArea::nonOverlapping in  
Ubuntu_20_04  
* QTBUG-45655 Some remoting QQuickImage tests hang occasionally in the  
CI system  
* QTCREATORBUG-3708 Context sensitive help does not work for several QML  
properties  
* QTBUG-106365 qmlsc doesn't find modules from sysroot  
* COIN-870 MinGW Windows build exceeds timeout limit  
* QTBUG-106194 Error: idProperty.qml:42:30: Could not compile binding  
for family: Cannot access value for name root           font.family:  
root.fontName  
* QTBUG-106284 tst_QQuickColorDialogImpl::eyeDropper fails with RHEL 9  
* QTBUG-105697 linebyline lexer test fail on android  
* QTBUG-106545 Turning on the SpotLight for the first time blocks  
rendering  
* QTBUG-30801 Button: tooltip not shown when the button is disabled  
* QTBUG-106714 tst_qquickflickable fails on android  
* QTBUG-98130 QtQuick and controls examples use qt_add_resources to add  
QML files  
* QTBUG-55722 QQuickWindows::closing should be available with no  
parameter  
* QTBUG-103196 syncqt does not reflect sources/headers known to CMake  
* QTBUG-106941 no-opengl build fails  
* QTBUG-107028 tst_qquicktextfield and tst_qquicktextarea fail on  
Android  
* QTBUG-107253 qmldom standalone test fails to download archives  
* QTBUG-106520 FAIL!  :  
qtquickcontrols::Tests_StackLayout::test_addAndRemoveItems in  
Ubuntu_20_04  
* QTBUG-106521 FAIL!  :  
qtquickcontrols::Tests_StackLayout::test_addAndRemoveItems in MacOS_12  
* QTBUG-107143 qmllint ignore RegisterEnumClassesUnscoped  
* QTBUG-107591 TreeViewDelegate: selection via onClicked does not work  
* QTBUG-107763 tst_qquickhoverhandler::deviceCursor is flaky  
* QTBUG-106407 Signal connect warnings when opening ColorDialog  
* QTBUG-107168 [Reg 6.2.6 -> 6.4.0] qmlsc: Use of native JS console is  
now treated as an Error  
* QTBUG-64554 Menu does not close when MenuItem in a Loader is clicked  
* QTBUG-103096 tst_qquicktext fails on Android  
* QTBUG-107863 tst_QQuickMouseArea::disableParentOnPress is flaky on  
some platforms  
* QTBUG-107864 QTest::touchEvent needs to take a const QPointingDevice *  
* QTBUG-107844 FileDialog: cannot open image picker dialog on iOS  
* QTBUG-107795 Reg-5.15.10->5.15.11 Setting property on TextField  
crashes  
* QTBUG-107684 background of ToolTip template is ignored  
* QTBUG-106035 Android: skipping *: it has unmet dependencies  
* QTBUG-107589 QT_ANDROID_EXTRA_LIBS does not detect library  
dependencies  
* QTBUG-106703 tst_QQuickControl::Material::flickable units for arch  
'applegpu_g13g' are not packed  
* QTBUG-107850 Crash on QQuickItem destruction  
* QTBUG-108216 Investigate the QRhi pipeline cache (MTLBinaryArchive  
usage) on macOS 13  
* QTBUG-108217 QML Modules without plugin cannot be deployed  
* QTBUG-108657 IOS Vulnerabilities  
* QTCREATORBUG-27590 ValueAxis: Unknown component. (M300)  
* QTBUG-108883 Improve documentation on how to expose value types with  
enums to QML  
* QTBUG-108346 tst_qquicktextedit::pasteHtmlIntoMarkdown is flaky on  
Ubuntu 20.04  
* PYSIDE-1345 vertexDataAsPoint2D() in QSGGeometry returns only one  
point  
* QTBUG-108101 String "6.4.0" found in Qt6.4.1 sources  
* QTBUG-109383 Re-enable building examples with qmake in non-qtbase  
repos  
* QTBUG-108150 Adding qml files from the build folder to the QRC is  
creating filenames so long it breaks the build on Windows host  
* QTBUG-109111 qmlsc should support casting of various int types  
* QTBUG-109373 DragHandler and PinchHandler: meaning of axis  
persistentValue is wrong  
* QTBUG-109392 Deprecations in QQuickPinchHandler are done incorrectly  
* QTBUG-109488 tst_qquicktextedit FAIL  
* QTBUG-109506 QQuickItemLayer::updateOpacity can be called with no  
effect internally and assert/crash  
* QTBUG-109235 Review toupper/tolower uses [Qt]  
* QTBUG-107707 tst_qquickimageparticle fails with Ubuntu 22.04  
* QTBUG-109553 CMake deployment API creates too deep directory hierarchy  
when DESTDIR is set  
* QTBUG-109869 The INTEGRITY linker crashes on tst_qqmlfileselector  
* QTBUG-97518 Mac, Metal RHI - runtime warnings "UI API called from  
background thread".  
* QTBUG-109942 Crash when running the qtdeclarative gallery example  
* QTBUG-104679 [REG 6.2.4-6.3.1] ListView: ASSERT if PullBackHeader or  
PullBackFooter is used  
* QTBUG-106929 Qml Singletons do not work on Android  
* QTBUG-110009 Multi Languge related documents for Qt6 is not consistent  
* QTBUG-99146 URI and VERSION should be optional in qt_add_qml_module  
* QTBUG-84328 QML Animators with a weird start behavior  
* QTBUG-63381 Transient scrollbars do not work when using style sheets  
* QTBUG-104570 QQuickHandlerPoint has no QML_ELEMENT declaration  
* QTBUG-111187 QtQuick.Layouts not included during linking when using  
ColorDialog  
* QTBUG-70397 TapHandler fires for all overlapping items  
* QTBUG-73262 it's confusing that TapHandler.gesturePolicy affects event  
propagation  
* QTBUG-100534 TapHandler doesn't stop propagation  
* QTBUG-107239 DragHandler propagates tap event through Flickable to  
underlying TapHandler  
* QTBUG-111310 \image tag breaks \value block  
* QTBUG-111766 qml issues in Effect Maker  
* QTBUG-111857 tst_snippets verify:qtquickcontrols-material-attributes  
fails on macOS  
  
### qtactiveqt  
* QTBUG-99294 In ActiveQtServer derived from QMainWindow, when  
PushButton exists Lables in StatusBar can not be shown  
* QTBUG-100332 dumpcpp silently generates uncompilable files for some  
.NET libraries  
* QTBUG-100145 ActiveQt example "outlook" build fails with a wall of  
errors: MSOUTL.cpp(346616): error C2062: type 'unknown-type' unexpected  
* QTBUG-107089 [REG 6.4.0->6.5.0] ActiveQt/include missing the 'version  
number' dir  
* QTBUG-106014 ActiveQt fails to handle VT_UNKNOWN  
* QTBUG-106024 [QAxServerBase::Invoke] ActiveQt should only call the  
dispatch method if the types match  
* QTBUG-109235 Review toupper/tolower uses [Qt]  
* QTBUG-110158 Invalid QApplication construction with argc=0  
  
### qtmultimedia  
* QTBUG-103725 VideoOutput crash on iOS when using OpenGLRhi  
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
* QTBUG-104943 Multimedia examples not shown in Qt Creator although  
module installed from Installer  
* QTBUG-103729 [REG 5.15-6.2] App isn't able to start on Windows 10 N  
* QTBUG-106092 Binding to CaptureSession.imageCapture fails  
* QTBUG-103239 [macOS] Crash in AVFMediaPlayerObserver  
* QTBUG-106204 Multimedia framework requires "record audio"  
authorisation  
* QTBUG-106881 Camera with multiple streams cannot be detected for the  
second stream  
* QTBUG-106257 QtMultimedia segfault when gstreamer plugins are missing  
* QTBUG-107701 [REG 6.4.0->6.4.1] namespace build fails on Windows  
* QTBUG-104226 QmediaDevices::videoInputs() fails to find a camera if  
libcamera is installed.  
* QTBUG-107885 [Recorder Example] Not working mute for AudioInput  
* QTBUG-107205 Video with sound fails to play if sound device is  
unavailable  
* QTBUG-108009 QML Camera maximumZoomFactor in iPad  
* QTBUG-108027 Signal videoFrameChanged not emitted  
* QTBUG-95127 QMediaPlayer::setVideoOutput() no longer takes QList of  
outputs  
* QTBUG-103238 [macOS] Crash in qt_convert_NV12_to_ARGB32  
* QTBUG-107671 Using strcmp instead of gst's methods for classfying  
classes  
* QTBUG-108187 QAudioSink can not be moved to another thread  
* QTBUG-108898 [Windows] Crash on  
QWindowsMediaDevices::availableDevices()  
* QTBUG-109009 Ffmpeg: videotoolbox doesn't support some yuv 8bit  
formats  
* QTBUG-109070 [DOCS] QCameraDevice docs refers to missing orientation()  
* QTBUG-108668 QAudioDevice shows incorrect (old Qt5) QMediaDevices  
usage  
* QTBUG-109341 Dependency update on qt/qtmultimedia failed in dev  
* QTBUG-103567 QML MediaPlayer fails to playback rtsp media properly.  
* QTBUG-108995 Seeking on a paused audio file causes it to "play" it  
* QTBUG-109443 Android: tst_QVideoWidget timeout  
* QTBUG-59726 no access to second camera on android phones with dual  
front/back cameras  
* QTBUG-108221 QAudioOutput crashes on Qt 6  
* QTBUG-109583 Doc: Stale references in QAudioDevice docs  
* QTBUG-109535 infinite loop in ffmpeg camera check  
* QTBUG-97265 Qt6 mediarecorder QML has invalid syntax in example code  
* QTBUG-109539 Devices example crash  
* QTBUG-109415 Camera is automatically activated by CaptureSession  
* QTBUG-109613 duplicate symbols in gstreamer and ffmpeg backends  
* QTBUG-109561 QML Camera working on Android is random  
* QTBUG-109391 Camera goes black after turning off and on.  
* QTBUG-110131 QML Camera unloading crash on iOS  
* QTBUG-109956 Example manifest data for Spatial Audio Panning Example  
wrong  
* QTBUG-108676 Streaming audio from source to sink fails in Qt6,  
succeeds in Qt5  
* QTBUG-110797 On android devices, when a 'Video' object is destroyed,  
the screen does not detect mouse events any more  
* QTBUG-109659 Audio capturing and playing does not work on Android  
* QTBUG-110844 QMediaRecorder frequently returns unknown errors when  
trying to record on Mac  
* QTBUG-104849 audio input examples do not work on mac os  
* QTBUG-111269 QtMultimedia doesn't build with libva-devel  
* QTBUG-98373 QAudioOutput not working on WebAssembly  
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
* QTBUG-100079 Android: fix QAndroidAudioDecoder issues  
* QTBUG-97492 QAudioSink returns always UnderrunError on Android  
* QTBUG-103591 Windows: Comboboxes (Qml and QtWidgets) don't have the  
UIAutomation (UIA) ExpandCollapse pattern  
* QTBUG-102645 build errors in multimedia  
* QTBUG-98121 Android: Filters out unsupported audio codecs(flac) on  
AudioRecorder app  
* QTBUG-99022 Android: Changing a Audio sink on Audiooutput example  
issue  
* QTBUG-105169 videoFrame.toImage() does not work in a different thread  
than the video rendering thread  
* QTBUG-105619 FFMPEG: sound volume is not editable in Media Player  
* QTBUG-105521 Mediaplayer working with ffmpeg hangs on playback rate  
changing  
* QTBUG-105617 FFMPEG: Video and audio are not synchronized after  
changing playback rate  
* QTBUG-97814 QML MediaPlayer only reports position changes at 10hz  
* QTBUG-105372 QML Camera - setting zoomFactor does not work  
* QTBUG-107127 QtMultimedia 6.4 fails to build with 32 bit MinGW  
* QTBUG-107678 audio device has unknown channel  
* QTBUG-108020 QMediaDevices on MacOS needs additional listeners to  
correctly catch device changes  
* QTBUG-108018 Camera Example crashes on macOS 13 ventura  
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
  
### qttools  
* QTBUG-103863 \qtcmakepackage docs in qdoc manual are partially  
misplaced  
* QTBUG-104216 Order of "New Member Functions" is indeterministic  
* QTBUG-99421 Some Qt5 ui file does not compile with Qt6  
* QTBUG-100837 Assistant: PageUp/PageDown keys scrolls 2 pages not 1  
* QTBUG-104369 qdoc should prefer links to a type's own API rather than  
outside targets when encountering ambiguity  
* QTBUG-104490 qhelpgenerator can't find QSqlDatabase drivers in static  
builds  
* QTBUG-99415 lupdate ignores tr() call in a function with noexcept  
operator  
* QTBUG-104713 GCC 12: failure to build from source [<QtTools>]  
* QTBUG-104613 qdoc: Marking a \module with \since is not reflected in  
the module's member classes  
* QTBUG-105130 qttools: CMake failure if litehtml is found on the system  
* QTBUG-104633 'examplesinstallpath' configuration variable is not  
documented  
* QTBUG-105278 qdoc: WebXML generator drops some  text fragments  
* QTBUG-105097 \since says the macro is a function even if it isn't  
* QTBUG-105987 Make order of elements in .qhp deterministic  
* QTBUG-106552 qttools: Build failure if litehtml is found on the system  
* QTBUG-106209 qdoc: Breadcrumb menu bug if \module, \qmlmodule clash  
* QTBUG-106706 Non-retina artwork  
* QTBUG-102282 lupdate doesn't parse resource files if passed via json  
project's description file  
* QTBUG-106255 qdoc: \wrapper command is undocumented  
* QTBUG-107084 warning C4996: 'QStyleHints::keyboardAutoRepeatRate': Use  
keyboardAutoRepeatRateF() instead  
* QTBUG-107193 fatal error: 'QtDesigner/uilib_global.h' file not found  
* QTBUG-107602 qdoc: Links inside \section titles lead to broken table  
of contents  
* QTBUG-106898 Export of id-based ts files creates non-id-based qm files  
* QTBUG-107107 lupdate -locations absolute creates relatives and not  
absolute paths  
* QTBUG-107845 Can not disable Linguist in Qt 6.4.0 when qttools are  
enabled  
* QTBUG-107762 qdoc: Cannot link to externally-built projects via .index  
files  
* QTBUG-108299 QDoc: Formatting text passed to \caption may cause weird  
behavior on Windows  
* QTBUG-108219 qdoc: Arguments for format-specific macros are lost  
* QTBUG-108131 "Button" is found twice in Qt Quick Controls Help file  
(same title, same url)  
* QTBUG-108243 Naming menu separators in design view is broken  
* QTBUG-94365 QDoc: "error code: 4" from clang on macOS  
* QTBUG-109132 qdoc: QML value type documentation doesn't accept QML  
module information  
* QTBUG-109423 qttools DesignerComponentsPrivate headers are not synced  
* QTBUG-109456 /home/qt/work/qt/qttools/src/qdoc/qmlvisitor.cpp:593:  
undefined reference to `QString  
qualifiedIdToString<QQmlJS::AST::Type*>(QQmlJS::AST::Type*)'  
* QTBUG-109618 QtAttributionsScanner crashes frequently  
* QTBUG-110440 Qt Designer: Items just added to scratch pad are not  
visible on Windows  
* QTBUG-109614 QDoc creates truncated temporary header files  
* QTBUG-109316 lupdate produces identical rows  
* QTBUG-109735 \include docs should state snippet marker '//!' must be  
at the beginning on the line  
* QTBUG-110881 REG->6.5.0.B2: Qt Designer crashes when editing resources  
* QTBUG-110930 cross builds: designer examples installed incorrectly  
* QTBUG-110923 qdoc is unnecessarily verbose  
* QTBUG-110142 In qdoc manual, most examples have invalid comment  
start/end  
* QTBUG-109734 qdoc \include docs example has extra braces  
* QTBUG-111093 [QDoc] Fails for template instantiation with 2 types  
* QTBUG-111391 Fix documentation of \brief command to list all valid  
contexts  
* QTBUG-111603 Qt Designer crash with custom widget plugin derived from  
QMainWindow with no central widget  
* QTBUG-103791 With new documentation UI, many code examples lack links  
to Qt symbols  
* QTBUG-104377 Qt Designer: Alignment property moves to wrong place in  
property editor  
* QTBUG-91521 When calling lupdate on a file that uses QT_TR_NOOP in a  
constructor for a static QString it will fail to find the context  
* QTBUG-104426 lupdate uses return type as context for free functions  
* QTBUG-103470 [iOS] CMake translation handling fails  
* QTBUG-86507 ASSERT: "it.isUnused()" in file  
/home/qt/work/install/include/QtCore/qhash.h, line 525  
* QTBUG-103196 syncqt does not reflect sources/headers known to CMake  
* QTBUG-104903 Remove Cpp.ignore* qdocconf settings  
* QTBUG-104944 QT_DISABLE_DEPRECATED_BEFORE hides wrong APIs  
* QTBUG-105102 qt_internal_add_tool and qt_internal_add_app does not get  
the value of QT_DISABLE_DEPRECATED_BEFORE  
* QTBUG-98472 [REG 6.2.1->6.3.0] Designer not launching on macOS  
* QTBUG-107681 lupdate does not find *.ts files  
* QTBUG-105229 Qt QML documentation: clash on the "examples"  
* QTBUG-108353 qdoc: QHash related warnings with LLVM 15.0.0  
* QTBUG-96239 Document CMake component in CMake function documentation  
* PYSIDE-2191 pyside6-uic fails to correctly generate resource_rc  
location  
* QTBUG-110963 Q Designer: inactive QPalette color values not stored  
correctly  
  
### qttranslations  
* QTBUG-111748 [Turkish] Inconsistent translations  
  
### qtdoc  
* QTBUG-103468 Update or delete "Qt Commercial License" page  
* QTBUG-100690 WebAssembly (WASM) MEMORY Doc fixes  
* QTBUG-93471 Darwin linker warns about global weak symbols when linking  
an executable against a static Qt  
* QTBUG-105006 iOS archive builds fail with qt_add_qml_module()s in  
static libs  
* QTBUG-96151 QML deployment docs need to be rewritten  
* QTBUG-106556 Documentation states that painting outside GUI Thread to  
QPixmaps is not supported  
* QTBUG-107245 Typo in the document?  
* QTBUG-103856 Add replacement for some QX11Info alternatives to Qt6  
porting guide  
* QTBUG-103715 QNativeInterface::QX11Application::display() example  
missing  
* QTBUG-108513 Disappearing text on a Button on QtQuick Controls when  
the Dark theme is active on macOS  
* QTBUG-108101 String "6.4.0" found in Qt6.4.1 sources  
* QTBUG-108670 doc state, that QOpenGLWidget is not supported, but it  
was fixed in qt 6.4  
* QTBUG-107723 Ensure a good visibility of the "what's new" pages  
* QTBUG-109503 Qt GRPC and Protobuf are not linked correctly from module  
page  
* QTBUG-109324 Clarify the doc page about module changes in Qt6  
* QTBUG-105362 "Building a reusable QML module" refers to non-existent  
CMake code  
* QTBUG-110281 Link to current Apple documentation not archive for  
Info.plist  
* QTBUG-110768 Clean up 'What's new in Qt 6.5'  
* QTBUG-110668 wasm: WebSockets don't actually work from other threads  
* QTBUG-110984 QT_WASM_INITIAL_MEMORY documentation is incorrect  
* QTBUG-110950 WebAssembly websockets not supporting ping  
* QTBUG-110742 "Qt for macOS - Specific Issues": sample code is wrong  
* QTBUG-106682 Typo in the document  
* QTBUG-111271 Typo in the document?  
* QTBUG-111279 Typo in the document?  
* QTBUG-104937 Conflicting android-manifest-file-configuration.html  
files  
* QTBUG-111919 Bump the minimum Android api level to Android 8.0 api 26  
* QTBUG-111982 New example demos/documentviewer fails to compile  
* QTBUG-107849 Qt 6.4.0 Purchasing Hangman example does not start  
* QTBUG-104944 QT_DISABLE_DEPRECATED_BEFORE hides wrong APIs  
* QTBUG-99808 CMake used on a Qt6 project generates a lot of extra  
targets  
* QTBUG-106677 "Back" button breaks UI of Coffee Machine Example  
* QTBUG-107121 Hangman example doesn't build for android with build  
tools >= 31.0.0  
* QTBUG-108335 calqlatr demo buttons are broken  
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
  
### qtpositioning  
* QTBUG-103478 QGeoPositionInfoSource on Android always asks for  
location permission  
* QTBUG-107580 [REG 5.15.10 -> 5.15.11], PositionSource: last known  
position is never read  
* QTBUG-105551 Missing nmeaSource property in geoflickr example  
* QTBUG-105558 GeoFlickr example does not ask for permissions on Android  
* QTBUG-107584 [iOS] Missing plist/location properties in positioning  
examples  
* QTBUG-109303 Android: single updates for PositionSource and  
SatelliteSource take too long  
* QTBUG-110512 geoflickr example not working  
* QTBUG-110902 tst_qgeoareamonitor execution failed with exit code 3.  
* QTBUG-110931 tst_qgeoareamonitor::multipleThreads randomly hangs on  
macOS ARM  
* QTBUG-104448 Fix QtPositioning tests for static builds  
* QTBUG-104465 It is impossible to build tests with custom plugins in  
static build configurations  
* QTBUG-104858 QT_DISABLE_DEPRECATED_BEFORE is not propagated to unit-  
tests  
* QTBUG-106233 Suggested fixes in qt_attributions.json for SPDX  
compliance & easier parsing  
* QTBUG-106673 Remove top level .qmake.conf in qtpositioning, qt3d &  
qtlanguageserver  
* QTBUG-106533 Android: jar and src dirs are installed in /usr if  
CMAKE_INSTALL_PREFIX=/usr  
  
### qtsensors  
* QTBUG-105848 FAILED: src/plugins/sensors/iio-sensor-  
proxy/properties_interface.h  
* QTBUG-105173 AddressSanitizer: new-delete-type-mismatch in  
tst_QSensor::testReadingBC()  
* QTBUG-104858 QT_DISABLE_DEPRECATED_BEFORE is not propagated to unit-  
tests  
* QTBUG-103196 syncqt does not reflect sources/headers known to CMake  
  
### qtconnectivity  
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
* QTBUG-69747 Reading RSSI value of connected Bluetooth Low Energy  
device  
* QTBUG-106282 tst_QLowEnergyController::tst_emptyCtor fails with RHEL 9  
in QtConnectivity  
* QTBUG-104473 (Classic) Bluetooth discovery agents to clear previous  
errors  
* QTBUG-106654 Error Unable to handle unregistered datatype  
'std::shared_ptr<QWinRTBluetoothDeviceDiscoveryWorker>'  
* QTBUG-107170 fatal error: 'qtranslation.h' file not found  
* QTBUG-106039 [macOS Bluetooth LE] Assert if service discovery times  
out  
* QTBUG-107195 Typo in the document  
* QTBUG-107224 Typo in the document?  
* QTBUG-107192 Link is dead in the document  
* QTBUG-107196 Is Advertisement really unavailable on Qt Bluetooth?  
* QTBUG-109315 Implicit reconfigure causes error regarding missing  
target PkgConfig::BLUEZ  
* QTBUG-108461 Bluetooth blocks the main thread for a short time  
* QTBUG-106938 Unhandled exception on Android bluetooth  
* QTBUG-111242 sdpscanner strcpy()s sdp_data_t::val::str into a fixed-  
size 1KiB buffer  
* QTBUG-96530 MTU changed for wrong GATT session - warning on Windows BT  
LE  
* QTBUG-102442 Bluetooth hostmode change Discoverable=>Connectable  
doesn't work on Android  
* QTBUG-101066 QBluetoothServiceDiscoveryAgent::finished sometimes  
(spuriously) is not emmited on Android 10  
* QTBUG-97092 spelling errors reported by lintian  
* QTBUG-104914 tst_qbluetoothlocaldevice and tst_qbluetoothserver tests  
fail on Android 12 emulator in CI  
* QTBUG-94001 QtBluetooth uses deprecated Windows API  
* QTBUG-106614  
tst_QBluetoothDeviceDiscoveryAgent::tst_startStopDeviceDiscoveries fail  
on Android 12  
* QTBUG-106533 Android: jar and src dirs are installed in /usr if  
CMAKE_INSTALL_PREFIX=/usr  
* QTBUG-103611 [Reg 5.15 -> 6.x] Re-initializing QGuiApplication causes  
QQmlApplicationEngine to crash  
  
### qtwayland  
* QTBUG-97593 Qt with QtWayland doesn't build without QtQml  
* QTBUG-85297 Menu location is offset depending on  
xdg_output.logical_layout in sway  
* QTBUG-104227 QWaylandTextInput: Not possible to inject keys with  
Shift- or Ctrl-Modifiers  
* QTBUG-105308 ASSERT failure in QWindow: "Updates can only be scheduled  
from the GUI (main) thread"  
* QTBUG-106638 QtWayland tests crash on webOS  
* QTBUG-107076 Copying image data from Qt aplications is still broken on  
GNOME Wayland  
* QTBUG-104259 tst_seatv4 tests are failing with Ubuntu 22.04 Wayland  
* QTBUG-75919 Override cursor has no precedence on Wayland  
* QTBUG-108767 Examples don't shut down gracefully  
* QTBUG-108765 Frequent unsupported damage and damage_buffer warning  
* QTBUG-108690 Cannot move windows via touch  
* QTBUG-109302 Segmentation Fault with Wayland and QTreeWidget  
* QTBUG-109051 Crash in multi-screen example when moving window  
* QTBUG-111377 QtWayland requests window activation on every focus  
object change  
* QTBUG-111473 Dependency update on qt/qtapplicationmanager is failing  
in 6.5  
* QTBUG-110420 QtWayland fails to build  
* QTBUG-104435 Build failure in qtwayland with libcxx  
* QTBUG-66818 tst_QWindow::initialSize fails on Wayland  
* QTBUG-104903 Remove Cpp.ignore* qdocconf settings  
* QTBUG-103196 syncqt does not reflect sources/headers known to CMake  
* QTBUG-87303 Wayland context menus can go off the screen because Qt  
does not do set_constraint_adjustment  
  
### qt3d  
* QTBUG-102328 Qt3D.Core can't be imported from a static Qt build  
* QTBUG-104593 Qt3D Application Crashes when rendering first frame  
* QTCREATORBUG-27852 Audio visualizer example has blank white screen  
* QTBUG-109203 build fails when qtbase is configured without vulkan  
* QTBUG-108405 bounding volume results are not checked for validity in  
concurrent calcuation  
* QTBUG-99019 PhongMaterial does not work in GLES2  
* QTBUG-95650 Qt3D Light Module is not working.  
* QTBUG-100402 Light uniform is hardcoded to use PointLight only  
* QTBUG-101876 Qt3D Viewport documentation states wrong type for Gamma  
property  
* QTBUG-104534 QImage received from QRenderCapture using Qt3D RHI  
renderer causes crash.  
* QTBUG-104592 RHI Render Capture crashed with debug build  
* QTBUG-105102 qt_internal_add_tool and qt_internal_add_app does not get  
the value of QT_DISABLE_DEPRECATED_BEFORE  
* QTBUG-103196 syncqt does not reflect sources/headers known to CMake  
* QTBUG-106233 Suggested fixes in qt_attributions.json for SPDX  
compliance & easier parsing  
* QTBUG-106865 RHI RenderCapture capture results differ from OpenGL  
renderer  
* QTBUG-56368 Crash when using async NodeInstantiator within Scene3D  
* QTBUG-106972 QRenderCapture leaks memory with RHI renderer  
* QTBUG-107693 tst_QResourceManager received signal 11 (SIGSEGV) with  
Ubuntu 22.04 QEMU  
* QTBUG-107694 tst_RayCasting::shouldReturnAllResults fails with Ubuntu  
22.04 QNX  
* QTBUG-111980 [REG 6.5.0 RC->beta3] qt3d/wireframe, lights and pbr-  
materials fails on configure  
  
### qtimageformats  
* QTBUG-104398 Segmentation fault in Jpeg2000JasperReader when Jasper 3  
is used  
* QTBUG-104692 qtimageformats breaks top-level build  
* QTBUG-70245 AnimationImage cannot load Network picture download .webp  
format  
* QTBUG-107040 Tiff images with LZW compression do not work in debug  
builds  
* QTBUG-107223 Massive memory consumption when loading TIFF image  
* QTBUG-110720 qtimageformats: cmake fails if libwebp is built with  
cmake  
  
### qtserialbus  
* QTBUG-103879 [Reg 5.15.2 -> 5.15.9] QModbusClient:: sendRawRequest()  
produces ModbusDevice::UnknownError when there is no error  
* QTBUG-107132 Typo in the document?  
* QTBUG-107141 Typo in the document  
* QTBUG-109940 [REG 6.4.2->6.5/6.0] serialbus modbus examples not  
compiling on iOS  
* QTBUG-106524 Typo in the document  
* QTBUG-107137 CMake instruction is not written in the document; grammar  
  
### qtserialport  
* QTBUG-101444 QSerialPort: trouble with high baud rates /  
waitForReadyRead() stalls  
* QTBUG-103822 QSerialPort::waitForReadyRead always returns false on  
older Windows systems  
* QTBUG-91237 QSerialPort: moving / resizing / clicking window title bar  
blocks serial port read/write  
* QTBUG-87151 QSerialPort: synchronous read fails as waitForReadyRead()  
always times out.  
* QTBUG-109219 [SerialPort] bindable property tests fail  
* QTBUG-108450 REG: Qt 6.3.2 WinOverlappedNotifier possible crash  
  
### qtwebsockets  
* QTBUG-105851 tst_QWebSocketServer::tst_handshakeTimeout fails  
* QTBUG-106372 wasm: Using WebSockets from worker threads fail to work  
* QTBUG-106937 Since Qt 6.3 QWebSocket::errorString() displays random  
http status code if status != 400  
* QTBUG-108276 MQTT WebSocket doesn't connect  
* QTBUG-108996 wasm: Threaded build causes unaligned or out of bounds  
access after calling deleteLater() on a WebSocket  
* QTBUG-110150 QWebSocketProtocol header missing  
* QTBUG-110951 WebAssembly websockets bytes sent is 0 for  
sendTextMessage / sendBinaryMessage  
* QTBUG-111248 wasm: QWebSocket does not disconnect if deleted  
* QTBUG-105087 [REG: 6.3->6.4] wasm: Use after free due to pointer to  
temporary data being used  
* QTBUG-84315 QUrl::setAuthority() behavior changes  
  
### qtwebchannel  
* QTBUG-105596 FAIL!  : TestWebChannel::testPassWrappedObjectBack()  
Compared QObject pointers are not the same  
* QTBUG-98490 QWebChannel does not convert QDateTime to javascript date  
type  
* QTBUG-103196 syncqt does not reflect sources/headers known to CMake  
  
### qtwebengine  
* QTBUG-103579 Qt PDF: Static build fails on macOS  
* QTBUG-103735 QWebEnginePage::iconChanged() not emitted  
* QTBUG-103578 WebEngine: Error when linking gn  
* QTBUG-96377 Using QWebEngineView::setPage() on page already active  
* QTBUG-92932 [REG 5.12 -> 5.13] QWebEngineUrlRequestInterceptor doesn't  
get called for websocket connections  
* QTBUG-101769 Qt WebEngine reports wrong UIAutomation bounding rects  
with high DPI  
* QTBUG-54433 Support of datalist  
* QTBUG-103760 Conan: Qt WebEngine resources not found  
* QTBUG-104436 V8 error when using WebEngine with --single-process and  
proxy auto-config  
* QTBUG-105134 WebEngineView is crashing while loading the pdf file  
* QTBUG-105082 QtWebEngine freezes on specific Chromium debug command  
* QTBUG-86871 Qt WebEngine incompatible with Selenium's "sendKeys"  
method  
* QTBUG-105072 [REG 6.4] Initial widget focus is wrong  
* QTBUG-106210 Dependency update on qt/qtwebengine failed in dev  
* QTBUG-106090 moc_qquickwebenginesingleton_p.cpp:38:69: error: use of  
undeclared identifier 'QtMocHelpers'; did you mean  
'::TestNamespace::TestNamespace::QtMocHelpers'?  
* QTBUG-105955 [REGRESSION] Web Engine views are painted only partially  
* QTBUG-105960 QtQuick: WebEngineView scaling regression (Windows)  
* QTBUG-105168 Build of Qt Pdf for iOS fails  
* QTBUG-104769 pdfviewer example: Pinch zoom on laptop trackpad stops  
working if zoom way in  
* QTBUG-106355 QtPDF: crash when pinch-zooming on a PDF page with text  
on iOS  
* QTBUG-106358 QtPDF: hard to hide the keyboard on iOS  
* QTBUG-106361 duplicate symbol qLcNav  
* QTBUG-100391 Application built with Qt 6.2.2 fails to run because of  
missing mf.dll error  
* QTBUG-106461 QWebEngineUrlRequestJob::reply() does not support a  
QIODevice that cannot be read completely instantly  
* QTBUG-106254 Windows offline installer creation fails due to long path  
in QtWebEngine  
* QTBUG-106095 [REG] 5.15.8 -> 5.15.9 WebEngine crash with software  
OpenGL  
* QTBUG-106588 Accessibility in QWebEngine crashes application  
* QTBUG-97392 WebEngine fails to load urls from resources  
* QTBUG-106688 Loading html from qrc in QtWebEngine fails  
* QTBUG-106944 [REG 6.4.0rc->final] Can not compile examples on iOS if  
QfPDF is included in installation  
* QTBUG-86972 [REG] QtPDF isn't properly installed as a framework unless  
WebEngine is also installed  
* QTBUG-106967 email privacy: DNS prefetch still leak from local content  
* QTBUG-107144 WebEngine crashes on github.com  
* QTBUG-107113 Dependency update on qt/qtwebengine failed in dev  
* QTBUG-105953 QtQuick: WebEngineView resize regression  
* QTBUG-107502 [Reg 6.3.2 -> 6.4.0] Qt WebEngine --remote-debugging-port  
no longer works  
* QTBUG-106975 Qt webengineview Web page requestfullscreen invalid  
* QTBUG-107529 QWebEnginePage only uses part of QWebEngineView  
* QTBUG-103958 Unable to remove warning, "Qt WebEngine seems to be  
initialized from a plugin..."  
* QTBUG-108008 FAIL!  :  
tst_QWebEngineView::inputFieldOverridesShortcuts() 'actionTriggered'  
returned FALSE  
* QTBUG-108029 Can't build qtwebengine with MSVC2019  
* QTBUG-108265 Pasting plain text does not work on Discord web  
* QTBUG-107451 QT NanoBrowser not passing antibot checks  
* QTBUG-109179 auto test qwebengineclientcertificatestore fails to build  
* QTBUG-106816 quicknanobrowser's popup window can't be moved or closed  
* QTBUG-108993 Autotests unreasonably slow on qemu arm64  
* QTBUG-63174 Navigator.maxTouchPoints not working under Linux  
* QTBUG-109357 [REG 5.12 -> 5.15/6.x] QWebEngineUrlRequestInterceptor:  
Multiple redirects crashes the application  
* QTBUG-110272 webengine tries to use DRI on embedded builds  
* QTBUG-109040 QWebEngineView always prints context  
* QTBUG-109348 QtWebEngineView doesn't scroll word document  
* QTBUG-110873 error: ‘QtWebEngineProcess’ was not declared in this  
scope; did you mean ‘QtWebEngineCore’?  
* QTBUG-111585 REG: GL Errors with WebGL on macOS 13  
* QTBUG-106072 QtPdf can't open password-protected PDF files on  
Windows/Android  
* QTBUG-111784 Regression: macOS: Some video do not show pictures after  
WebGL fix  
* QTBUG-112007 Qt WebEngine 3rd party licensing documentation is  
generated but hidden  
* QTBUG-103354 Test #12: tst_uidelegates  
...........................***Failed  
* QTBUG-104057 Dependency update fails: error: no matching member  
function for call to 'addAction'  
* QTBUG-99445 quicknanobrowser crashes with --single-process  
* QTBUG-104238 [REG 5.15 -> 6.3] Widevine fails on specific sites  
* QTBUG-99207 [REG: 5.14.2->5.15.0] Redirection from file to custom url  
schemes does not work  
* QTBUG-102099 QWebEngineView ColorPicker  is not modal and freezes  
application  
* QTBUG-102633 [Windows] Linking errors in Blink  
* QTBUG-100630 PdfLinkModel don't give the right rect everytime  
* QTBUG-103221 QtPDF examples are not installed with 6.3.0 or 6.4.0  
* QTBUG-101744 tst_uidelegates most tests fail on macOS  
* QTBUG-105342 Test on qemu are very flacky  
* QTBUG-105818 gio is not detected correctly  
* QTBUG-106406 gn not build in host build when not building QtWebEngine  
or QtPdf at the same time  
* QTBUG-98904 Facebook notifications do not work with QtWebEngine  
* QTBUG-104224 QWebEngineView print() with copyCount multiplies number  
of copies  
* QTBUG-107778 Dependency update on qt/qtwebengine is failing in dev  
* QTBUG-107669 QtWebengine doesn't work with Vulkan  
* QTBUG-102058 #hashtag navigation does not work in custom url scheme  
* QTBUG-107442 The endpoint in QWebEnginePage works only with FCM  
* QTBUG-109235 Review toupper/tolower uses [Qt]  
* QTBUG-105124 qtwebengine crashes when `/usr/share/X11/xkb` is empty  
* QTBUG-110157 Incorrect command-line parsing if argc=0  
* QTBUG-96010 Issues with lifecycle example  
* QTBUG-110578 tst_QWebEngineView::horizontalScrollbarTest is flaky?  
* QTBUG-110749 Video decoding bug  
* QTBUG-63889 unbundle openjpeg  
* QTBUG-110504 Webengine extremely slow in loading webpage in debug  
build  
* QTBUG-105988 a11y: Accessible interface can't be retrieved after  
calling QAccessibleEvent::setChild on event created using the  
constructor taking QAccessibleInterface*  
* QTBUG-105053 qtwebengine 6.3.1 fails to link against system nss  
* QTBUG-111225 Host include paths from pkg-config not used when  
FEATURE_webengine_system_icu=On when cross-compiling  
  
### qtwebview  
* QTBUG-103196 syncqt does not reflect sources/headers known to CMake  
* QTBUG-104903 Remove Cpp.ignore* qdocconf settings  
* QTBUG-97487 [Android] WebView cannot open local file  
(net::ERR_ACCESS_DENIED)  
* QTBUG-98549 QML WebView does not store or read cookies  
* QTBUG-108752 tst_QQuickWebView::settings_JS fails on Android 12  
* QTBUG-109083 FAIL!  : tst_QWebView  
* QTBUG-106533 Android: jar and src dirs are installed in /usr if  
CMAKE_INSTALL_PREFIX=/usr  
  
### qtcharts  
* QTBUG-99190 Performance issue with VXYModelMapper  
* QTBUG-102392 X-axis vanishes when difference between min and max is  
less than two  
* QTCREATORBUG-27650 Pie Chart Customization Example doesn't scale  
properly  
* QTBUG-108090 Qt chart does not show best fit line correctly  
* QTBUG-107890 When changing the label of a legend marker it will not  
update until something else triggers an update  
* QTBUG-104903 Remove Cpp.ignore* qdocconf settings  
* QTBUG-108018 Camera Example crashes on macOS 13 ventura  
* PYSIDE-2179 QtCharts not available in PySide6 qml  
  
### qtdatavis3d  
* QTBUG-104714 Dependency cycle between QtDatavisualization and  
QtDatavisualizationQml  
* QTBUG-105398 Q3DScatter should fail gracefully when mesh is missing UV  
coordinates  
* QTBUG-106080 qmltest::Scene3D Initialized::test_initialized() Compared  
values are not the same  
* QTBUG-107505 Wasm build fails when linking both QtMultimedia and  
QtDataVisualization  
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
* QTBUG-104944 QT_DISABLE_DEPRECATED_BEFORE hides wrong APIs  
  
### qtvirtualkeyboard  
* QTBUG-102115 VirtualKeyboard manual tests have hard coded include  
paths which can lead to build error  
* QTBUG-94770 [Qt Virtual keyboard] Keyboards doesn't respond when  
QT_SCALE_FACTOR  is set to 1.5  
* QTBUG-105685 [REG 6.3.2->6.4.0] virtualkeyboard/basic not compiling on  
iOS  
* QTBUG-106894 QtVirtualKeyboard does not popup on static builds  
* QTBUG-106895 QtVirtualKeyboard on mac desktop wrong rotation  
* QTBUG-83217 rotation of virtualkeyboard does not work  
* QTBUG-98750 [VKB] AutoScroller does not work in the basic virtual  
keyboard example  
* QTBUG-105371 [Virtual keyboard] The fallback to layouts/fallback is  
not mentioned  
* QTBUG-108030 Virtual keyboard basic example freezes on Android  
* QTBUG-108396 The link in the document seems to be wrong  
* QTBUG-97901 tst_plugin::test_hangulInputMethod(row 24) fails  
* QTBUG-97830 Some Qt Virtual Keyboard tests checking the position of  
selection handles are failing  
* QTBUG-111928 [Reg 6.3.2 -> 6.4.x] Virtual keyboard layout is broken  
* QTBUG-104903 Remove Cpp.ignore* qdocconf settings  
* QTBUG-102152 qmlcachegen miscompiles something  
  
### qtscxml  
* QTBUG-98368 Dependency cycle in qtscxml  
* QTBUG-107209 Update documentation on how to integrate state machines  
into QML modules  
* QTBUG-80262 SCXML StateMachine state properties get incorrect values  
if History is used  
* QTBUG-109235 Review toupper/tolower uses [Qt]  
* QTBUG-110286 SignalTransition::triggered can cause Segfault  
  
### qtspeech  
* QTBUG-55274 [qtspeech] Re-enable blacklisted autotests  
* QTBUG-105477 Doc: TextToSpeech links to QML type  
* QTBUG-106286 tst_QTextToSpeech::sayWithVoices fails with RHEL 9 in  
QtSpeech  
* QTBUG-108381 qtspeech does not compile without qtqml  
* QTBUG-108773 Cannot compile qtexttospeech.h for C++ projects  
* QTBUG-108205 tst_QTextToSpeech::pauseResume(darwin) fails on macOS 13  
in CI  
* QTBUG-106533 Android: jar and src dirs are installed in /usr if  
CMAKE_INSTALL_PREFIX=/usr  
* QTBUG-103611 [Reg 5.15 -> 6.x] Re-initializing QGuiApplication causes  
QQmlApplicationEngine to crash  
  
### qtremoteobjects  
* QTBUG-104098 Update dependencies on '6.4' fails in qt/qtremoteobjects  
* QTBUG-74124 QAbstractItemModelReplica internal error crash  
* QTBUG-97790 Generated SourceAPI class can't be used without compiler  
warnings  
* QTBUG-105597 tst_Server_Process failed  
* QTBUG-106003 remoteobjects does not checks for Declarative's private  
headers existance, but makes use of them  
* QTBUG-105469 QVariant::load: unknown user type with name QList<int>  
when running QtRO example  
* QTBUG-104068 Fix qlalr warning when building qtremoteobjects  
* QTBUG-97092 spelling errors reported by lintian  
* QTBUG-105102 qt_internal_add_tool and qt_internal_add_app does not get  
the value of QT_DISABLE_DEPRECATED_BEFORE  
  
### qtlottie  
* QTBUG-107501 Lottie produces warnings  
* QTBUG-104944 QT_DISABLE_DEPRECATED_BEFORE hides wrong APIs  
  
### qtquicktimeline  
* QTBUG-104944 QT_DISABLE_DEPRECATED_BEFORE hides wrong APIs  
  
### qtquick3d  
* QTBUG-102193 Negative joint index leads to crashes  
* QTBUG-104118 [REG 6.3 -> 6.3.1] Global scaling does no longer work in  
3D asset imports  
* QTBUG-104885 Background color is not tonemapped  
* QTBUG-105131 QtQuick3D fails to build in C++20 mode  
* QTBUG-105293 Particles3D sortMode example crashes with distance mode  
* QTBUG-105354 QSGRenderNode / View3D's Inline mode has no way to gain  
access to the render target/pass descriptor when within an item layer  
* QTBUG-105549 customshaders example's Texture with Item option does  
nothing  
* QTBUG-103265 Shader compilation failure when setting height map  
* QTBUG-97692 Incorrect rendering when using external camera and  
Temporal AA  
* QTBUG-105565 [REG 6.3.2 -> 6.4.0] Highlighted example  
principledmaterial UI has a big empty space section  
* QTBUG-106037 issue when enabling Reflection Probe Debug View  
* QTBUG-105918 REG: Jittery skeletal animations  
* QTBUG-106544 Antialiasing example doesn't animate when progressive AA  
is enabled  
* QTBUG-102477 Adding the same effect twice to SceneEnviroment leads to  
a hanging application  
* QDS-7793 propertyGroups.json is not installed  
* QTBUG-107112 FAIL!  : tst_MultiWindow::cubeMultiViewportMultiWindow()  
'comparePixelNormPos  
* QTBUG-105458 Incorrect primitive position when skin property set to  
null  
* QTBUG-104843 QtQuick 3D leaks memory after destroying View3D  
* QDS-8014 Missing properties and types in qtquick3d property sheets  
* QTBUG-96339 Fails to build QtQuick3d on MSYS2/MinGW-w64 due to "The  
command line is too long"  
* QTBUG-98336 WIN10 Qt6 build error in qtquick3d module  
* QTBUG-107734 [REG 6.4.0->6.4.1 and 6.5.0] too long command on MinGW  
shadow build  
* QTBUG-105217 [REG: 6.3.2->6.4.0] Picking of 3D geometry works  
incorrectly (with BBox only)  
* QTBUG-108078 CustomMaterial texture min filter can't be changed  
* QTBUG-96302 3D scenes with 2D subtrees leak graphics resources upon  
destroying the scene  
* QTBUG-106032 If you start an application with View3D not visible from  
one state, it's impossible to get it visible then.  
* QTBUG-86716 Materials shared between views don't always render  
* QTBUG-108606 All View3D instances where material is used are not  
updated when material color changes  
* QTBUG-108811 Skinned mesh doesn't follow skeleton  
* QDS-8451 Adjusting horizon property value of sceneEnvironment does not  
work with drag  
* QTBUG-109249 Passing sourceItem-based texture to postprocessing effect  
uses the dummy texture  
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
* QTBUG-111929 QQuick3DLightmapBaker not exported for Design Studio  
* QDS-9507 Lightmapper issues  
* QTBUG-103196 syncqt does not reflect sources/headers known to CMake  
* QTBUG-105566 Touch panning a ListView in View3D broken  
* QTBUG-104944 QT_DISABLE_DEPRECATED_BEFORE hides wrong APIs  
* QTBUG-104903 Remove Cpp.ignore* qdocconf settings  
* QTBUG-104858 QT_DISABLE_DEPRECATED_BEFORE is not propagated to unit-  
tests  
* QTBUG-106481 PrincipledMaterial clearcoat shader error with no lights  
* QTBUG-107667 RobotArm example is disfunctional  
* QDS-7662 Drop-down menu for shaders in Properties&Material Editor  
lists irrelevant files from the project  
* QDS-8087 SpecularGlossyMaterial was added in Qt 6.4. It should be  
treated like one of the other basic material types  
* QTBUG-107780 Rendering Texture in WebAssembly  
* QDS-8024 Icons needed for new component library items  
* QTBUG-108758 documentation confuses aliasing and anti aliasing.  
* QTBUG-109088 Not skinned Mesh doesn't follow parent node  
* QDS-9055 3D import settings for Level of Detail are buggy in the UI  
with Qt 6.5 kit  
* QDS-8963 QtQuick3D types and properties missing in Designer  
* QTBUG-105609 should be able to add a TapHandler to a Button to modify  
behavior  
* QTBUG-111086 QuickBall example button white  
* QTBUG-111013 HorizontalHeaderView with resizableColums true eats input  
when visible (Quick 3D DebugView)  
* QTBUG-111709 FAIL!  : tst_Input::singleTap2D  
  
### qtshadertools  
* QTBUG-103723 [iOS] CMake shader handling fails  
* QTBUG-107483 Typo in the document?  
* QTBUG-110293 Apps crash on shader compile on INTEGRITY  
* QTBUG-103196 syncqt does not reflect sources/headers known to CMake  
* QTBUG-104903 Remove Cpp.ignore* qdocconf settings  
* QTBUG-106233 Suggested fixes in qt_attributions.json for SPDX  
compliance & easier parsing  
  
### qt5compat  
* QTBUG-103927 GCC 12: failure to build from source [<Qt5Compat>]  
* QTBUG-107468 [Regression] Creating DropShadow is almost 20x slower  
* QTBUG-105279 qmllint complains about Qt5Compat.GraphicalEffects  
imports  
* QTBUG-109747 Qt5Compat.GraphicalEffects is broken for static builds  
* QTBUG-105098 Purge Q_DUMMY_COMPARISON_OPERATOR  
* QTBUG-89702 Improve the QRegExp->QRegularExpression docs  
* QTBUG-104944 QT_DISABLE_DEPRECATED_BEFORE hides wrong APIs  
* QTBUG-103196 syncqt does not reflect sources/headers known to CMake  
  
### qtcoap  
* QTBUG-104944 QT_DISABLE_DEPRECATED_BEFORE hides wrong APIs  
* QTBUG-104903 Remove Cpp.ignore* qdocconf settings  
  
### qtmqtt  
* QTBUG-105873 QMqttClient documentation does not include the  
constructor  
* QTBUG-92817 QMqttTopicFilter also matches topics just starting with  
the filter name  
* QTBUG-106203 QMqttClient: Possible race condition on messageReceived  
signal  
* QTBUG-80440 MqttClient Invalid Property assignment: unsupported type  
"ushort"  
* QTBUG-104944 QT_DISABLE_DEPRECATED_BEFORE hides wrong APIs  
* QTBUG-104903 Remove Cpp.ignore* qdocconf settings  
* QTBUG-108276 MQTT WebSocket doesn't connect  
  
### qtopcua  
* QTBUG-104646 [C++20 FTBFS] open62541.h is running afoul of volatile  
compound statement deprecation in C++20  
* QTBUG-105593 Update dependencies on 'dev' in qt/qtopcua failed  
* QTBUG-109096 Installed version of OPC UA example cannot compile  
because it relies on the presence of Qt source code  
* QTBUG-110837 error: 'friend' used outside of class  
* QTBUG-109097 OPC UA examples use relative paths and assume in-source  
builds, thus do not work out-of-the-box when loaded in Qt Creator  
* QTBUG-96283 [REG 6.1.3->6.2.0] macOS: Can not configure qml / network  
example with statically compiled Qt  
* QTBUG-103905 No target "OpenSSL::SSL" failure on qtopcua dependency  
update  
* QTBUG-103196 syncqt does not reflect sources/headers known to CMake  
* QTBUG-104903 Remove Cpp.ignore* qdocconf settings  
* QTBUG-104418 tst_opcua:AbsoluteNodeTest is flaky on Mac  
* QTBUG-107161 Build failure with OpenSSL 3.0  
* QTBUG-108253  Tst_QOpcUaSecurity::keyPairs fails with OpenSSL 3  
* QTBUG-106285  
Tst_QOpcUaSecurity::connectAndDisconnectSecureUnencryptedKey fails with  
RHEL 9 in QtOpcua  
  
### qtlanguageserver  
* QTBUG-106673 Remove top level .qmake.conf in qtpositioning, qt3d &  
qtlanguageserver  
  
### qthttpserver  
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
* QTBUG-104348 .gitignore file present in qthttpserver and  
qtquick3dphysics  
* QTBUG-105329 QHttpServer: returning a value from a route handler  
should be an error when the function uses a QHttpServerResponder  
* QTBUG-106378 Qt HTTP Server examples do not show up under module name  
in 'All examples'  
* QTBUG-107854 HTTP server must handle Expect: 100-continue  
* QTBUG-107927 addressbookserver example uses very non standard  
"api_key" header  
* QTBUG-106160 tst_QAbstractHttpServer::fork() is flaky  
* QTBUG-105202 Route handlers returning QFuture are broken with  
pipelining  
  
### qtquick3dphysics  
* QTBUG-104348 .gitignore file present in qthttpserver and  
qtquick3dphysics  
* QTBUG-107007 Configuring Qt with -no-gui fails  
* QTBUG-108045 [FTBFS] iter.physx::PxContactStreamIterator::faceIndice’  
may be used uninitialized  
* QTBUG-108897 QFATAL : tst_physicsscene::UnknownTestFunc() ASSERT  
* QTBUG-109015 qtquick3dphysics PhysX build fails using oneapi icx on  
windows  
* QTBUG-110258 CharacterController doesn't trigger TriggerBody  
* QTBUG-110723 DynamicRigidBody axis lock properties have int type  
instead of enum  
* QTBUG-104903 Remove Cpp.ignore* qdocconf settings  
* QTBUG-108667 libcooker installed in PREFIX/bin  
  
Known Issues  
------------  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Amir Masoud Abdol  
Mike Achtelik  
Cristian Adam  
Chris Adams  
Laszlo Agocs  
Waqar Ahmed  
Martin Andersson  
Dimitrios Apostolou  
Albert Astals Cid  
YAMAMOTO Atsushi  
Xavier BESSON  
Mahmoud Badri  
Mate Barany  
Sebastian Beckmann  
Rolf Eike Beer  
Vladimir Belyavsky  
Nicholas Bennett  
Tobias C. Berner  
Chen Bin  
Alex Blasche  
Tim Blechmann  
Maximilian Blochberger  
Eskil Abrahamsen Blomfeldt  
Mikolaj Boc  
Tatiana Borisova  
Joerg Bornemann  
Jörg Bornemann  
Assam Boudjelthia  
Mathias Brevik  
Aurélien Brooke  
Michael Brüning  
Marco Bubke  
Igor Bugaev  
Andreas Buhr  
Robin Burchell  
Wojciech Błaszak  
Hxcan Cai  
Olivier De Cannière  
Luca Carlon  
Marcus Comstedt  
Creapermann  
Alexandru Croitor  
Mitch Curtis  
Thibaut Cuvelier  
Giuseppe D'Angelo  
Szabolcs David  
Noah Davis  
Oliver Dawes  
James DeLisle  
Knud Dollereder  
Evgeniy A. Dushistov  
Artem Dyomin  
Alexey Edelev  
David Edmundson  
Oliver Eftevaag  
Christian Ehrlicher  
Iikka Eklund  
Hatem ElKharashy  
Andreas Eliasson  
Balazs Erseki  
Lionel Fafchamps  
David Faure  
Ilya Fedin  
Wang Fei  
Nicolas Fella  
Ben Fletcher  
Alexandros Frantzis  
Simo Fält  
Samuel Gaist  
Pekka Gehör  
Roman Genkhel  
Christophe Giboudeaux  
Markus Goetz  
Maximilian Goldstein  
Andrei Golubev  
Julian Greilich  
Robert Griebl  
Mikko Gronoff  
Magnus Groß  
Jan Grulich  
Kaj Grönholm  
Richard Moe Gustavsen  
Lucie Gérard  
Tang Haixiang  
Heikki Halmet  
Thomas Hartmann  
Andre Hartmann  
Elias Hautala  
Jani Heikkinen  
Miikka Heikkinen  
Christian Heimlich  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Dominik Holland  
Mats Honkamaa  
Linus Jahn  
Sam James  
Nils Jeisecke  
Allan Sandfeld Jensen  
Tim Jenssen  
Janne Juntunen  
Taras Kachmaryk  
Maurice Kalinowski  
Jonas Karlsson  
Johannes Kauffmann  
Timothée Keller  
Ali Kianian  
Friedemann Kleint  
André Klitzing  
Michal Klocek  
Martin Klos  
Lars Knoll  
Seokha Ko  
Jarek Kobus  
Kai Koehne  
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
Jaroslaw Kubik  
Anton Kudryavtsev  
Konrad Kujawa  
Santhosh Kumar  
Marcel Kummer  
Sona Kurazyan  
Jonas Kvinge  
Keith Kyzivat  
Kai Köhne  
Lauri Laanmets  
Inho Lee  
Eric Lemanissier  
Paul Lemire  
Thorbjørn Lindeijer  
Celeste Liu  
Moody Liu  
Robert Loehning  
Jenny Lofthus  
Robert Löhning  
Thiago Macieira  
Sérgio Martins  
Sergio Martins  
Thorbjørn Lund Martsum  
Terry Meacham  
Frank Meerkötter  
Ievgenii Meshcheriakov  
Leena Miettinen  
Piotr Mikolajczyk  
Phan Quang Minh  
Samuel Mira  
Fawzi Mohamed  
Safiyyah Moosa  
Bartlomiej Moskal  
Marc Mutz  
Tommi Mänttäri  
Antti Määttä  
Martin Negyokru  
Guineng Ni  
Andy Nichols  
Yuya Nishihara  
Mårten Nordheim  
Dennis Oberst  
Kimmo Ollila  
Fredrik Orderud  
Roland Pallai  
Laszlo Papp  
Bumjoon Park  
Kwanghyo Park  
Ari Parkkila  
Shreya Pattani  
Evgen Pervenenko  
Thomas Piekarski  
Samuli Piippo  
Timur Pocheptsov  
Milla Pohjanheimo  
Joni Poikelin  
Aleix Pol  
Alessandro Portale  
Rami Potinkara  
Lorn Potter  
Shyamnath Premnadh  
Liang Qi  
Umair Raihan  
Matthias Rauter  
David Redondo  
Arno Rehn  
Topi Reinio  
Aleksandr Reviakin  
Rob De Reycke  
Alexander Rezepkin  
Christian Riggenbach  
André de la Rocha  
Alexey Rochev  
Rafael Roquetto  
Niclas Rosenvik  
Maxime Roussin-Bélanger  
Shawn Rutledge  
Toni Saario  
Sharad Sahu  
Ahmad Samir  
Michael Saxl  
Lars Schmertmann  
David Schulz  
Eli Schwartz  
Björn Schäpers  
Thomas Senyk  
Luca Di Sera  
Dmitry Shachnev  
Sami Shalayel  
Ye ShanShan  
Andy Shaw  
Venugopal Shivashankar  
Stefan Sichler  
Harald Sitter  
Kristoffer Skau  
David Skoland  
Daniel Smith  
Johan Solbakken  
Ivan Solovev  
Ziming Song  
Axel Spoerl  
Piotr Srebrny  
Christian Stenger  
Elias Steurer  
Patrick Stewart  
Martin Storsjö  
Brett Stottlemyer  
Christian Strømme  
Fab Stz  
Tarja Sundqvist  
Tasuku Suzuki  
Jan Arve Sæther  
Morten Sørvig  
Morten Johan Sørvig  
Benjamin Terrier  
Duan Ting  
Ivan Tkachenko  
Pino Toscano  
Mike Trahearn  
Jens Trillmann  
Jere Tuliniemi  
Paul Olav Tvete  
U-GER\tjmaciei  
Leticia Valladares  
Sami Varanka  
Peter Varga  
BogDan Vatra  
Louis du Verdier  
Doris Verria  
Tor Arne Vestbø  
Petri Virkkunen  
Jannis Voelker  
Alexander Volkov  
Ville Voutilainen  
Juha Vuolle  
Jaishree Vyas  
Martin Walch  
Ole Wegen  
Michael Weghorn  
Bernd Weimer  
Edward Welbourne  
Fushan Wen  
Paul Wicking  
Anna Wojciechowska  
Oliver Wolff  
Jiang Wu  
WANG Xuerui  
Weng Xuetian  
Lu YaNing  
Andrey Yaromenok  
Semih Yavuz  
Vlad Zahorodnii  
Sharaf Zaman  
Thomas Zander  
Leon Zhang  
JiDe Zhang  
Yuhang Zhao  
Eike Ziller  
hjk  
