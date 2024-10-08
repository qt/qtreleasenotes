Release note
============
Qt 6.8 introduces many new features and improvements as well as bugfixes
over the 6.7.x series. For more details, refer to the online
documentation included in this distribution. The documentation is also
available online:

https://doc.qt.io/qt-6/

The Qt version 6.8 series is binary compatible with the 6.7.x series.
Applications compiled for 6.7 will continue to run with 6.8.

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
* CVE-2024-39936 in qtbase
* CVE-2024-36048 in qtnetworkauth
* CVE-2024-33861 in qtbase
* CVE-2024-30161 in qtbase
* CVE-2024-25580 in qtbase
* CVE-2023-51714 in qtbase

### qtbase
* 7a829eaf518 Fix return value of qbswap(qint128) to qint128 (was: quint128).

* 3472aa6e284 Use Qt::WindowNoState for child windows/widgets shown via
show()
Child windows and widgets are now always shown in their normal state by
show().

* 675b4f63fea QIdentityProxyModel: add
setHandleSourceLayoutChanges(bool)
Added setHandleSourceLayoutChanges(bool) method to allow sub-classes to
indicate to QIdentityProxyModel that they will handle source model
layout changes on their own. Also added a getter,
isHandleSourceLayoutChanges().

* 12b4085f453 CMake: Added the deployment variable
QT_DEPLOY_LIBEXEC_DIR.

* f355f4fe7ea CMake: Add LIBEXEC_DIR argument to
qt_deploy_runtime_dependencies
The qt_deploy_runtime_dependencies function gained the LIBEXEC_DIR
argument to set the directory for deploying helper executables on Unix
derivatives.

* d4f38a36325 QDialogButtonBox: Fix focus chain and default button
assignment
Default button becomes focus proxy of a QDialogButtonBox. This ensures
that Enter triggers the default button, instead of the first button in
the layout.

* 4f95e66f940 QWidget: deliver DragLeave events symmetrically
DragLeave events are now always sent to the widget the mouse is
leaving, even if it didn't accept the DragEnter event.

* 5f7b4c045f4 Fix Maximized frameless window painting wrong with
WS_THICKFRAME
Adding a check for the maximized state of the window during the
calculation of margins. Margins calculation will not be skipped for
maximized windows.

* b9ee6d3b2e4 QWindowContainer: Don't embed a QWidget
If createWindowContainer() is called with a QWidgetWindow argument,
return pointer to the widget instead of new container.

* a116b2ddfc9 QByteArray: allow begin() to return nullptr, like QString
Calling begin() or end() in a const QByteArray will return a null
pointer if isNull() is true. This is the same behavior as QString. This
is important for code attempting to iterate from data() to end() instead
of begin() to end().

* 7c5cf8cae05 Add parent arg to QFileDialog::getOpenFileContent and
saveFileContent
Adds an overload to the static methods getOpenFileContent and
saveFileContent with a new parent argument which always no-ops in the
WASM environment.

* 993f3180144 QSqlRecord: All functions taking a QString got an overload
taking a QStringView.

* f2dba191942 QSqlQuery: isNull() and value() each gained a new overload
taking a QStringView.

* b1e5d9275d4 SQL: rename enablePositionalBinding() to
setPositionalBindingEnabled()
Add setPositionalBindingEnabled() to be able to disable positional
binding.

* 89d89f99a79 QShader: Added move constructor, move-assignment operator
and swap member function.

* b13c610f50c On Windows, the public qopengl.h header no longer includes
windows.h.

* 24a95c22fc9 SQLite: Updated SQLite to v3.45.0

* 6f9db711546 QUuid: Fix Id128Bytes alignment on some architectures
The QUuid::Id128Bytes type had a loose definition that could cause it
be passed incompatibly between functions, in some architectures,
depending on whether GNU extensions were allowed. This is now fixed, but
may cause code compiled with Qt 6.6.0 and 6.6.1 to fail when recompiled
with 6.6.2 or later.

* dc4159286b8 qt6_wrap_cpp: Add .moc generation
qt_wrap_cpp will accept .cpp files from now on. When a .cpp file is
passed to qt_wrap_cpp, the TARGET parameter is now required. Generated
.moc files are added to target's sources inside qt_wrap_cpp. This avoids
the need to add the generated .moc files to the output parameter.

* 3512fb1ec5f QCheckBox: deprecate stateChanged()
stateChanged(int) has been deprecated in favor of
checkStateChanged(Qt:CheckState).

* d99b0cfed21 Increase precision for QGraphicsView::AnchorUnderMouse
Increase precision for QGraphicsView::AnchorUnderMouse and
QGraphicsView::centerOn

* 41c842d3f7e SQL/MySQL: Fixed compilation with MySQL 8.3

* 4b3d6be5f5a QHostInfo: fix lookupHost() signature immediately
The lookupHost() static function now takes const QObject* receivers
(was: (non-const) QObject*).

* 93a4478c5f7 QSsl: The enums in namespace QSsl are now Q_ENUMs.

* e752c77b351 QObject::moveToThread() now returns a boolean success state.

* 8be3c9f4867 Fix clipped text when combining multiple writing systems
Fixed an issue where drawing text from different writing systems in the
same line and including a background could cause parts of the text to be
clipped.

* 1579f19cf71 Updated Zlib to 1.3.1

* 11344f57235 windows: Avoid infinite recursion with certain fonts
Fixed an issue where an infinite recursion could occur if the system
had a font with multiple preferred names in non-English languages.

* e769cf026e3 QTest: add opt-in changing QCOMPARE etc to exit with
throw, not return
Added QTEST_THROW_ON_FAIL and QTEST_THROW_ON_SKIP C++ macros and
environment variables that, when defined, change how
QCOMPARE/QVERIFY/QSKIP etc exit the test function on failure. Instead of
a return, exiting only the immediately-surrounding function, they throw
a special exception instead, thereby exiting from subfunctions of the
test function, all the way to QtTestLib.

* a17c10a63b3 Update public suffix list
Updated the public suffix list to upstream SHA
883ced078a83f9d79a98933145425c221a5e51f0.

* 185add27b2f Added support for the named instances from the variable
fonts.

* c6aa399d062 QBitArray: avoid overflow in size-to-storage calculations
Fixed a bug with QBitArrays whose size() came within 7 of the
size_type's maximum.

* a4f44e06988 QPainterPath: Fix boundingRect and controlPointRect
ignoring start point
boundingRect() and controlPointRect() now use the start point from
QPainterPath(const QPointF &startPoint).

* 40a87ca1b42 SQLite: Updated SQLite to v3.45.1

* 0808beace33 QBitArray: fix potential truncation in QDataStream op>>()
Fixed undetected overflows in the deserialisation (opertor>>()) from
QDataStream.

* 2188ca2c5df QVersionNumber: make iterable
Added (const) iterators over segments (begin()/end(), incl. c- and r-
variants).

* 62b3720a207 Remove system locale dependency from timezone code that
doesn't need it
Some features are now available whenever feature timezone is enabled,
that were previously dependent on system locale support.

* 063026cc503 Update QLocale and calendar data to CLDR v44.1
Updated QLocale's data extracted from the Unicode Common Locale Data
Repository (CLDR) to v44.1. The license changed to Unicode License V3.

* 9219e8ff1d1 QBitArray: don't create invalid Qt 5 streams
Now refuses to stream a QBitArray with size() > INT_MAX to a
Qt-5-compatible QDataStream.

* 0092f06a648 Add CMYK support for pens/fills in the PDF engine
QPdfWriter can now use CMYK colors directly, without converting them
into RGB colors.

* 7c313f18654 QMovie non-anim: use QImageReader::imageCount but not
nextImageDelay
QMovie now handles non-animated multi-frame image formats (such as
tiff): QImageIOHandler::imageCount() is observed, and the default frame
rate is 1 FPS.

* 16bcdba8e7a Updated md4c to 0.5.2

* 3a7cda715a9 QPdfWriter: switch the default color model to Auto
QPdfWriter by default will now save CMYK colors in CMYK, instead of
converting them to RGB. You can use the setColorModel() function to
restore the previous behavior.

* bffddc6a993 Extract and re-write "front matter" in markdown documents
Markdown "front matter" (usually YAML) is now extracted during parsing
(GitHub dialect) and can be retrieved from
QTextDocument::metaInformation(FrontMatter). QTextMarkdownWriter also
writes front matter (if any) to the output.

* 6504496c646 QBitArray: use QDataStream::SizeLimitExeeded where
applicable
Uses new QDataStream::Status::SizeLimitExceeded now, where applicable
(was: WriteFailed, ReadCorruptData).

* 366657b9511 Remove QT_READDIR_R macro from qplatformdefs.h
Removed QT_READDIR_R macro; readdir_r() has been deprecated since
glibc-2.24 and it's recommended to use readdir() instead. For more
details see: https://man7.org/linux/man-pages/man3/readdir_r.3.html

* 79badf1b2c9 Update Valgrind to version 3.22.0
Updated Valgrind header used by QtTest. The change only affects
portability of s390 inline assembler.

* d4bb448cddc QTest: allow passing chrono literal as QTRY_ timeout
The QTRY_*_WITH_TIMEOUT macros now also accept chrono literals (was:
int milliseconds).

* 329dbfcc78d CMake: Fix undefined symbol: qt_resourceFeatureZstd issue
Targets created with qt_add_executable and qt_add_library will now add
the --no-zstd option to AUTORCC_OPTIONS when the target platform does
not support zstd decompression. You can opt out via the
QT_NO_AUTORCC_ZSTD cmake variable.

* 38c62c58514 WASM builds now handle bitmap and pixmap cursors
Previously, bitmap and pixmap cursors were nonfunctional in wasm builds
and would trigger warnings.These cursors now work as expected.

* e1f45ad8187 QMap: added missing qHash() overload

* 1d7950c9467 Added qHash() overloads for quint128 and qint128.

* af051f9be23 QVarLengthArray: re-publish Prealloc as a nested
PreallocatedSize
Added PreallocatedSize nested constant, equal to the Prealloc template
argument.

* 277d77029d7 QGtk3Theme: Fix QGtk3Interface::fileIcon
Fixed file icons provided by QFileIconProvider when using the gtk3
platform theme.

* 73bf1c1a9bc QList: Added support for uninitialized construction and resizing.

* cfaed648738 QByteArray/QString: Added resizeForOverwrite().

* 909d881e753 PCRE2: upgraded to 10.43

* ee25bde3edf wasm: make opengles3 (webgl2) default surface format
Default OpenGL ES version raised to 3.0

* 9904686cf3e RHI: fix Vulkan layout for PreserveDepthStencilContents
depth textures
QRhiTextureRenderTarget::PreserveDepthStencilContents now works
properly on Vulkan

* bfc7535a10f QSingleShotTimer: use nanoseconds precision
Added startTimer() nanoseconds overload and removed the milliseconds
overload. This change is backwards compatible.

* 3379fd2322d SQL/SQLite: handle option SQLITE_OPEN_NOFOLLOW
Add new option QSQLITE_OPEN_NOFOLLOW to expose open mode
SQLITE_OPEN_NOFOLLOW.

* 7ce6920aacf Containers: add max_size()

* 0119f0a43bf Add QNetworkRequest attribute support to
QNetworkRequestFactory
Add QNetworkRequest attribute support to QNetworkRequestFactory

* 9bf68a47e1b QString/QByteArray: add slice() methods
Added slice() methods that work like sliced(), but modify the
string/byte-array they are called on.

* fb5ffe86268 a11y: Add new QAccessibleAttributesInterface
Added new QAccessibleAttributesInterface that can be used to expose
object attributes/properties to assistive technology.

* f9653c4ff25 QNetworkInformation: document a potential SiC
The enums in QNetworkInformation must now be scoped when used from QML.
The scope is no longer optional. Adding the scope is a backwards-
compatible fix.

* 803abb6323c rhi: Added support for short and ushort vertex attributes

* 735d2d41c38 QString: document isSimpleText() removal
Removed undocumented internal, yet public, isSimpleText() member
function. If you still use it, you'll have to write your own version
outside of QString.

* bd764cc1ca5 Add QChronoTimer, a timer with nanoseconds precision
Added QChronoTimer, which uses a std::chrono::nanoseconds intervals, as
a replacement for QTimer.

* 4bc0834bc18 Timers: Added Qt::TimerId enum class, that is used to
represent timer IDs.

* 94dfcaac8aa QDirIterator: port to QDirListing internally
This class has been deprecated and may be removed in a future Qt
release. Use QDirListing instead.

* e06c67d448a Revert "Fix export of QDeferredDeleteEvent, should be
Q_CORE_EXPORT"
Made this undocumented class private and unexported. You will still be
able to see the definition in qcoreevent_p.h, but you won't be able to
create objects of the class anymore.

* d8f6425fef1 Add a QHttpHeaders convenience method for unique header
name setting
Added replaceOrAppend() convenience method, which either replaces
previous entries with a single entry, or appends a new one if no entries
existed

* 8a6d9ac7bcd Add A2B tables, and PCSLab support to QIcc
ICC profiles that are not three-component matrix based are now
supported.

* 652065b06b3 Honor QPrinter::setFullPage(true) on Windows too (no
margins)
setFullPage(true) now behaves as expected, i.e. the QPrinter margins
are ignored and the drawing's (0, 0) is the topleft corner of the page.
This is what setFullPage(true) is documented to do, and how it was
already working on other operating systems. If this causes regressions
in your application, consider removing the call to setFullPage(true) so
that the painting honors the margins again.

* 21dfb0ebcc6 QString/QByteArray: add explicit constructors for
Q{String,ByteArray}View
Added a constructor to create a QByteArray from QByteArrayView.

* 3a6c8e02b6d Long live QT_ENABLE_STRICT_MODE_UP_TO
Added the QT_ENABLE_STRICT_MODE_UP_TO macro.

* 2781c3b6248 SQL/MySQL: pass UTC date/time stamps to the server
Fixed a bug in passing QDateTime to be passed as local time to the
server, regardless of the QDateTime's time zone setting. This would
cause certain timestamps to be rejected by the server, such as a UTC
time stamp whose time numerically matched the local timezone's spring
forward gap in the transition into Daylight Savings Time.

* f1bb9cfbf65 Add AA_DontUseNativeMenuWindows
Added AA_DontUseNativeMenuWindows application attribute. Menu popup
windows (e.g. context menus, combo box menus, and non-native menubar
menus) created while this attribute is set to true will not be
represented as native top level windows, unless required by the
implementation.

* 91f8d1de37a SQLite: Updated SQLite to v3.45.2

* ed66cf8a045 Revert default FlickDeceleration to 1500
The default value for the platform FlickDeceleration hint is reverted
to 1500 (rather than 5000 as in Qt 6.6). This sets the default value for
Flickable.flickDeceleration, which can be overridden directly; and the
default can also be overridden in any QPlatformTheme subclass.

* b71f185ffc5 SQL/PostgreSQL: Make sure the server returns datetime in
UTC
Fixed a bug where a wrong QDateTime might be returned when the
PostgreSQL server and the Qt client had different time zones configured.

* d04cf2c58b4 cmake: Rename QT_UIKIT_SDK to QT_APPLE_SDK
The -sdk configure argument now maps to the QT_APPLE_SDK CMake
variable. QT_UIKIT_SDK is still supported for iOS builds for
compatibility.

* 70e69f334e3 cmake: Don't set CMAKE_SYSTEM_NAME=iOS when configuring
with -sdk
The -sdk argument no longer auto-enables the macx-ios-clang makespec.
Pass -xplatform macx-ios-clang to explicitly build Qt for iOS.

* 9ff1e6d80bb Add hardening build options
Qt builds by default in "hardened mode", meaning that a series of
security-related compiler options are automatically enabled. In the
unlikely case in which these options constitute an unacceptable
performance hit, it is possible to disable individual hardening options
when configuring Qt.

* 4c21f728374 QImageReader: allow only one dimension to be used for
scaledSize
Allow only one dimension (width or height) to be set for the scaled
size. In this case, the other will be calculated automatically based on
the original image size and maintaining the aspect ratio.

* 3924c945d17 QMovie: allow only one dimension to be used for scaledSize
Allow only one dimension (width or height) to be set for the scaled
size. In this case, the other will be calculated automatically based on
the original movie size and maintaining the aspect ratio.

* 0cdeecf4150 Make deployment of openssl plugin optional
Deployment of openssl plugins is now optional. For proper deployment of
openssl related functionality pass in --openssl-root to make sure that
openssl libraries are also deployed.

* ecdbc40d404 CMake: Consider NO_UNSUPPORTED_PLATFORM_ERROR for non-
bundle mac apps
The qt6_generate_deploy_app_script NO_UNSUPPORTED_PLATFORM_ERROR option
will now have an effect when calling the API on non-bundle macOS
executable targets.

* b84e7a6bb09 CMake: Move various rcc generated files into .qt
subdirectory
Generated resource files (and supporting files) will now be placed into
the .qt/rcc subdirectory of a project build dir. The location is an
implementation detail that might still change in the future, so it
should not be relied upon.

* fdac1e22053 Add support for using an inline namespaces for
-qtnamespace
It is now possible to use an inline namespace for -qtnamespace (option
-qtinlinenamespace).

* 2a54229f90b GUI: Added support for 8-bit CMYK images.

* 3fb3d95c335 Add support for CMYK file I/O in JPEG
Added support for loading and saving of JPEG files in 8-bit CMYK
format. When loading a CMYK JPEG file, Qt used to convert it
automatically to a RGB image; now instead it's kept as-is.

* ce2585d0e95 QObject: add check for Q_OBJECT macro to findChild(ren)
The class template parameter passed to QObject::findChild() or
findChildren() is now required to have the Q_OBJECT macro. Forgetting to
add it could result in finding children of the nearest ancestor class
that has the macro.

* 3c6598c359a Add CMYK image output support to QPdfWriter
QPdfWriter can now save images in CMYK format directly.

* 5a03e5c51b4 SQL/ODBC: don't create temporary QStrings
All options must now be upper-cased as documented. Lower-cased options
are no longer supported.

* 394788c68ef QCborValue: fix sorting of UTF8-to-UTF16 strings
Fixed a bug that caused certain non-US-ASCII string comparisons to
produce results not in line with the CBOR specifications.

* 3941fe697b9 libinput: Allow setting touchscreen matrix via env var
The environment variable QT_QPA_LIBINPUT_TOUCH_MATRIX now can be set
with a string of 6 space-separated numbers to set the touchscreen
transformation matrix. See docs for
libinput_device_config_calibration_set_matrix()

* ca851b33171 Unify behavior of QSystemTrayIcon::geometry for hidden
icons on Windows
The geometry of a hidden QSystemTrayIcon was unified over different
Windows versions. It will always return QRect() now.

* 421e7621faa Implement aliased text rendering with DirectWrite
Support QFont::NoAntialias with the DirectWrite font engine.

* 25c96d547b4 Add CMYK support to QColorSpace

* 359df32300f Android: don't call JNI_OnLoad for libraries opened with
QLibrary
Loading a shared library with QLibrary no longer implicily calls a
JNI_OnLoad implementation.

* b6624877c61 SQLite: Updated SQLite to v3.45.3

* 0f5f1bfeffc Extract metatype information as part of library
finalization
With CMake 3.19 or later qt_extract_metatypes() is automatically called
during target finalization for libraries that use automoc now. This has
no effect if you've already manually called qt_extract_metatypes()
before, but it does make sure that the metatypes are also generated if
you haven't.

* 7466831509f Long live [[nodiscard]] QFile::open
The open() functions of file-related I/O classes (such as QFile,
QSaveFile, QTemporaryFile) can now be marked with the "nodiscard"
attribute, in order to prevent a category of bugs where the return value
of open() is not checked and the file is then used. In order to avoid
warnings in existing code, the marking can be opted in or out, by
defining QT_USE_NODISCARD_FILE_OPEN or the QT_NO_USE_NODISCARD_FILE_OPEN
macros. By default, Qt will automatically enable nodiscard on these
functions starting from Qt 6.10.

* 7cf57cffbc9 QByteArrayView: make starts/endsWith(char) constexpr
The startsWith(char) and endsWith(char) functions are now constexpr.

* 3afcfbc4005 Port QVersionNumber to QSpan
We have begun to port APIs to QSpan, replacing overload sets of
concrete container classes. This breaks code that relied on concrete
container class overloads and passed types that implicitly convert to
such a container, but not to QSpan. The backwards-compatible fix is to
make the conversion explicit.

* cba15d99f0c Add API to provide user-defined fallback fonts
Added API to override default fallback font families for specific
scripts.

* 1025ff1bf4f QLogging: enable %{backtrace} support via <stacktrace>
Support for the %{backtrace} expansion has been extended to the
platforms supporting C++23's <stacktrace> header (such as MSVC 2022 >=
17.4).

* c0f6d10bc29 iOS: Remove plumbing for
QWindow::reportContentOrientationChange. It no longer has any effect on
iOS, as the APIs used to implement this on iOS are no longer available.

* bc014d5fc70 iOS: Don't report UIDevice.currentDevice.orientation
through QScreen
QScreen::orientation() will no longer report the device's physical
orientation when orientation has been locked to a subset of the
available orientations, but will instead match the primary orientation.

* 94c62e32226 QXmlStreamWriter: decode UTF-8 into code points
Fixed a bug that caused the class to fail to write UTF-8 strings with
non-US-ASCII content when passed as a QUtf8StringView.

* c25541e9ac4 QXmlStreamWriter: fix attempts to write bad QStrings
The class now rejects writing UTF-8 and UTF-16 invalid input (improper
code unit sequences).

* 39bbfce9b67 QStringConverterICU: Pass correct pointer to callback
Fixed a bug involving moved QStringEncoder/QStringDecoder objects
accessing invalid state.

* d0b4e8a601b QGtk3Theme: Add support for xdg-desktop-portal to get
color scheme in QGtk3Theme.

* d778d17b9f0 Cope with CLDR's "day period" format specifiers
CLDR's 'B' (flexible day period, e.g. "at night" &c.) field, not
currently supported, is now handled as a synonym for the AM/PM field
'a', instead of leaving the B as literal text. Only affects zh_TW at
present.

* 42e4e1816ab Fix handling of am/pm indicators in mapping from CLDR to
Qt formats
Where CLDR specifies an am/pm indicator, the case of the CLDR-supplied
indicator is used, where previously QLocale forced it to upper-case.

* 60bdf2b2201 QProcess: fix startCommand() with whitespace-only strings
Fixed a bug that would cause startCommand() to crash if passed a string
that was empty or contained only whitespace characters.

* f0f2a9ef260 QString: ensure multi-arg arg() parses replacement like
single-arg arg()
The QString::arg() overload taking multiple QString-like arguments is
now fixed to interpret placeholders like the other arg() overloads: it
will find at most two digits after the '%' character. That is, the
sequence "%123" is now interpreted as placeholder #12 followed by
character '3' (verbatim).

* dd56558ecde Date-time formats now more faithfully follow the CLDR data
in handling timezones. In most cases where this changes data, it uses
the IANA ID in place of the abbreviation.

* f20be43b827 Set focus to the window container when contained window
gains focus
The window container will become focused if the contained window
becomes focused. This implies that the QApplication::focusWidget() will
be the window container if the contained window is the focus window.

* ef2b55ee65a QXmlStreamEntityResolver: disable copying
Disabled the copy and move constructors and assignment operators. You
can still provide them for your own subclasses, but you must do so
explicitly.

* b4c63b89dfe QSqlDatabase: add moveToThread()/currentThread()
QSqlDatabase gained two new functions moveToThread() and
currentThread() to be able to use it in another thread than the one it
was created in.

* 0756cc1eae5 QTest: rip out qxp::function_ref from compare_helper()
The QCOMPARE_xx macros can now only find QTest::toString() expansions
that are either found via Argument Dependent Lookup on the type in
question or are an instatiation of the QTest::toString<T>() template.
This matches the behavior of the QCOMPARE() macro.

* ba2f7945965 QSaveFile: don't reset fileEngine after commit()
Member functions such as fileTime() and size() now continue to work
after commit().

* f0633e82379 SQLite: Update identified license
Change identified license for SQLite from 'Public Domain' to more
accurate 'SQLite Blessing': https://spdx.org/licenses/blessing.html

* ab0b2a490eb QSignalSpy: fix -Wweak-vtable by removing the QObject
inheritance
QSignalSpy no longer inherits from QObject. If your code uses the fact
that QSignalSpy is-a QObject, you need to redesign around this now.

* 737c6680b48 QRegularExpressionMatch: port API from QString to
QAnyStringView keys
Keys can now be passed as QAnyStringView (was QStringView).

* 0b494c47d36 Don't quit automatically via QEventLoopLocker if there are
open windows
Fixed a regression where the last QEventLoopLocker going out of scope
would quit the app, even if there were open windows, if
quitOnLastWindowClosed was false.

* fa456ad5501 Add QHttpHeaders to QNetworkRequest
Added headers() and setHeaders() methods to QNetworkRequest, which
provide an interface to work with QHttpHeaders.

* 148add03f3b Enable resetting a sort model by descending order
QSortFilterProxyModel.sort sorts the proxy by the source model index
descending if the sort column is less than zero and the order is
descending.

* c6438054b91 Add QHttpHeaders to QNetworkReply
Added headers(), setHeaders() and setWellKnownHeader() methods to
QNetworkRequest to provide an interface to work with QHttpHeaders.

* 09ea47f8113 Improve default style of QTextTable
QTextTableFormat now defaults to collapsed tables with no spacing
between cells.

* 78b0d507ce8 Add QHttpHeaders methods to QNetworkCacheMetaData
Added headers() and setHeaders() methods to QNetworkCacheMetaData to
provide an interface to work with QHttpHeaders.

* e8e881ba35f macOS: Added support for universal links / https uri
scheme handling

* 664c7ffb212 macOS: Added support for custom uri scheme handling

* 65fef44ddf1 Added headers() and setHeaders() methods to QNetworkProxy
to provide an interface to work with QHttpHeaders.

* a2566e139f8 Extend QTest::failOnWarning() to a no-parameter
fail-on-any-warning.  This support a common case, without needing to
construct a match-everything regular expression.

* 0fef8f53c3e Use QHttpHeaders: Update internal users of QNRequest,
QNReply, QNProxy
Header value added by QNetworkRequest::setRawHeader() method is trimmed
now.

* ab2f4ef8fad QTextDocument: Add support for responsive images
The max-width style can now be applied to <img/> to set the maximum
width in pixels or percentage.

* ed70faf87af QCoreApplication: make removeNativeEventFilter() remove
from main thread
Fixed a mismatch on which event dispatcher was modified between
installNativeEventFilter() and removeNativeEventFilter(). Now both
functions in QCoreApplication access the main thread's event dispatcher.
To access the current thread's dispatcher, use
QAbstractEventDispatcher's functions.

* c878a51509d QLatin1StringMatcher: add indexIn(QStringView) overload

* 9724b039cac QDnsLookup: add initial support for DNS-over-TLS (DoT)
The class now supports DNS-over-TLS and some other DNSSEC experimental
features, on some platforms. Use QDnsLookup::isProtocolSupported to know
if the protocol is supported on a given platform.

* 4503dabfbd1 QDnsLookup: add support for TLSA records
Added support for querying records of type TLSA, which are useful in
DNS-based Authentication of Named Entities (DANE).

* 179e79b18d1 QThreadPool: add waitForDone() based on QDeadlineTimer
Added an overload of waitForDone() based on QDeadlineTimer.

* fa0d77e290f Added qFuzzyCompare() and qFuzzyIsNull() overloads for
QPointF

* 7072030d933 Fixed a bug when QLineF::isNull() returned incorrect
result if the start or end point had a zero component.

* 9bedf8a53c8 QLineF: added qFuzzyCompare and qFuzzyIsNull overloads

* 9d4e1b9f8d3 QRectF: added qFuzzyCompare and qFuzzyIsNull overloads

* 8a54d25a467 Fix QMarginsF::operator==() for zero margins
Fixed a bug when equality comparison returned incorrect results if one
of the margins was zero.

* 473d06970d2 QMarginsF: added qFuzzyCompare and qFuzzyIsNull overloads

* ed6d1fa71a7 QDBusSignature: accept empty strings as valid
Fixed a bug that caused the class not to accept an empty string as a
valid D-Bus SIGNATURE value.

* 010952a55ee a11y: Added new QAccessibleAnnouncementEvent that can be
used to request the announcement of a message by assistive technologies.

* 3ca9877f8ca QSizeF: add qFuzzyCompare and qFuzzyIsNull overloads

* 90c2cde6916 Change the -qpa configure argument logic
Added '-default-qpa' argument which replaces the '-qpa' one. The
argument is translated to the QT_DEFAULT_QPA_PLATFORM CMake variable and
selects the default platform that should be used by GUI application if
QT_QPA_PLATFORM environment variable is not set.

* b740cd1f38e Android: account for namespace in build.gradle instead of
manifest
Add support for namespace in build.gradle instead of the package
attribute in the manifest.

* 72c6fcafdd7 Updatee bundled libjpeg-turbo to version 3.0.4

* cb8e5e0dd96 Http: Support unix+http: scheme in http backend
QNetworkAccessManager now supports local connections using the uri
schemes unix+http: or local+http:.

* 672afb13ca5 QSignalSpy: make sig member const
The signal() method no longer necessarily returns an empty byte array
when the connection failed. Use the existing isValid() method to
determine whether a given QSignalSpy object listens to a valid signal on
a valid object.

* 26a81bd4fb1 QVariant: do reset is_null after setValue()
Fixed a bug that would allow the class to keep returning isNull() =
true even after calling setValue().

* 462c958a924 QSpan: add as_(writable_)bytes
Added std::span-style as_bytes() and as_writable_bytes() functions.

* 00769990310 QRegion: re-add rects() and port setRects() to QSpan
Added QSpan overload of setRects(); re-added Qt5's rects(), but
returning QSpan instead of QVector now.

* ece36a73945 Port QModelIndex to new comparison helper macros
Added a Qt::totally_ordered_wrapper class whose relational operators
use the std ordering types. Use it to wrap the pointers when doing the
comparison to avoid UB.

* cbda9583521 Port QPersistentModelIndex to new comparison helper macros
Made several operators (relational, QDebug streaming, etc) hidden
friends. This may break code that calls these operators a) with types
that require implicit conversion on the arguments, or b) using member-
function syntax (lhs.operator<(rhs)). The backwards-compatible fix for
(a) is to make at least one of the argument's implicit conversions
explicit. For (b), use infix notation (lhs < rhs).

* 48aad482a87 Http: Add support for full localsocket paths
QNetworkAccessManager now supports using full local server name, as in,
named pipes on Windows or path to socket objects on Unix.

* 373ae6cbd24 SQL/IBase: add partial support for SQL_INT128 datatype

* ef2912334cc QLibraryInfo: Introduce paths
qt.conf now allows providing mutliple paths, and QLibraryInfo has a new
paths method to fetch all of them.

* 8931f2c8365 SQLite: Updated SQLite to v3.46.0

* 54f22297143 QChar: remove QT_IMPLICIT_QCHAR_CONSTRUCTION opt-in
Removed the QT_IMPLICIT_QCHAR_CONSTRUCTION opt-in. The respective QChar
constructors (`(int)`, `(uint)`, `(uchar)`, `(uchar, uchar)`) are now
always explicit.

* a92f0e1a843 qmake: Do not disable deprecation warnings for MSVC
(C4996)
qmake does not disable the MSVC compiler warning about deprecated API by
default anymore (C4996). This means the compiler will now warn about use
of deprecated API, be it from Qt or from other headers. You can manually
revert this by adding QMAKE_CXX_FLAGS_WARN_ON += -wd4996 to your .pro
file.

* c70c81b3719 Long live QCryptographicHash::hashInto()!
Added hashInto().

* d8131960d89 QUuid: Ported createUuidV3() and createUuidV5() from
QByteArray to QByteArrayView, made them noexcept, and fixed various
ambiguities in the overload set.

* 88b1c962390 QAnyStringView: fix char-ish ctors to not allocate memory
Fixed a regression where constructing a QAnyStringView from a char-like
type (QChar, QLatin1Char, ...) would first construct a QString and only
then convert that to QAnyStringView.

* 87896c03c1b QIcon: enable icon engine plugins to implement themes
The keys registered by an QIconEnginePlugin implementation are now also
matched against the current theme (system or user theme), allowing
engine providers to implement entire themes through a plugin.

* 2b6a77cd150 QMessageAuthenticationCode: add hashInto() overloads
Added hashInto() methods, see QCryptographicHash for more information.

* a5953d20e27 Add QPaintDevice metric query to get precise fractional
DPR value
Added new QPaintDevice metrics for querying fractional device pixel
ratios with high precision. Custom paintdevice classes that support
fractional DPRs are recommended to implement support for these queries
in metric(). Others can ignore them.

* 32610561e3e Add new convenience class QFormDataBuilder to help
constructing multipart/form-data QHttpMultiPart messagess.

* ce33e476670 Add Bt2020 and Bt2100 color spaces
Bt.2020 and Bt.2100 (aka HDR10) formats have been added.

* 1bc78f7739c Introduce flag to use typographical line metrics for fonts
Added QFont::PreferTypoLineMetrics for using the recommended line
spacing metrics of the font, even if the font has not explicitly set its
USE_TYPO_METRICS flag.

* 9122d826d25 macOS: Present Metal layer with transaction during display
cycle
Metal layers are now presented with transactions during the display-
cycle, which should fix issues with the layer's content being out of
sync with the layer bounds or scale. If this causes issues, set the
QT_MTL_NO_TRANSACTION environment variable to opt out.

* d5dd7da3eef rcc: add the ability to output copyrights in the output
The Qt Resource Compiler now accepts a <legal> XML tag inside the main
<RCC> entry, which can be used to document the copyright of the resource
file itself and other terms of use (even though the file is probably
created by a tool like Qt Creator's resource editor). The text of this
copyright will be emitted in the generated C++ or Python source code.

* 70dd53e3d30 uic: recognize <legal> tag as an alias for <comment>
The Qt UI Compiler now accepts a <legal> XML tag to indicate the
copyright of the UI file and other legal terms of use. The text of this
tag will be emitted in the generated code. This tag is an alias to
<comment>.

* 9ec1de2528b Add Identifier role to QAccessible and use it in OS
interfaces
Add possibility to add unique identifier to QAccessibleInterface to
give a11y elements consistent identifiers.

* 5f63885e84e Update CLDR Windows timezone data to v44.1
Updated timezone data from the Unicode Common Locale Data Repository
(CLDR) to v44.1 to match QLocale's data.

* aec1edfe40f qtypeinfo.h: move QTypeTraits part to qttypetraits.h
The qtypeinfo.h header no longer transitively includes <optional>,
<tuple> and <variant>.

* 34533705b27 Entrypoint/Win32: just use __argc and __argv if available
Fixed a bug that caused Qt applications to disregard Unicode command-
lines on Windows even when argc and argv were passed unmodified to
QGuiApplication or QApplication. This happened only for builds with
Visual Studio and in the "windows" subsystem (not "console").

* 47353821221 QSqlRecord/QSqlQuery: Use QAnyStringView instead
QStringView
All functions taking a QString were changed to take a QAnyStringView.

* dc8c8b5fc9f Remove QNetworkRequestFactory TP marking
This class is no longer "under development and subject to change".

* 56019f4d49d Remove QRestAccessManager TP marking
This class is no longer "under development and subject to change".

* 9b1e98a14e0 Remove QRestReply TP marking
This class is no longer "under development and subject to change".

* 1a833d82f48 [docs] Document QDBusObjectPath QDebug stream operator
Added QDebug stream operator.

* e24f931b9f5 Added Qt::compareThreeWay() overloads for
Qt::totally_ordered_wrapper.
These overloads do the comparison using strict total ordering.

* e37c0a33a40 Deprecate Qt::compareThreeWay() overload for pointers

* dbb945fd432 Update public suffix list
Updated the public suffix list to upstream SHA
903a83ff7bfc3148e3692e09396f9f3bdc9462ef.

* 3b1d3432157 PCRE: upgraded to 10.44

* 70dcbb4f171 QESDP: deprecate
QT_ENABLE_QEXPLICITLYSHAREDDATAPOINTER_STATICCAST
Support for QT_ENABLE_QEXPLICITLYSHAREDDATAPOINTER_STATICCAST has been
deprecated, and will get removed in a future version of Qt.

* 09c3e9da1ff QStringConverter: port encodingForName() to QAnyStringView
The encodingForName() function now takes QAnyStringView (was: const
char*).

* 23013db675b QStringEn/Decoder: port (name, Flags) ctors to
QAnyStringView
The (name, flags) constructor now takes QAnyStringView (was: const
char*).

* e5890084dcc QThread: mark is(Main|Current)Thread() noexcept
Added isMainThread() static member function.

* 33b3054da17 Windows: Remove legacy mouse handling
Legacy mouse handling has been removed. It is no longer possible to
enforce legacy mouse handling by passing "-nowmpointer".

* 65bf57ce7ca CMake: Generate an SPDX v2.3 SBOM file for each built
repository
A new -sbom configure option can be used to generate and install a SPDX
SBOM (Software Bill of Materials) file for each built Qt repository.

* 3a70e669ef1 Determine Qt::AA_DontShowIconsInMenus default value based
on platform
The default value of Qt::AA_DontShowIconsInMenus is now determined
based on the platform. On macOS icons will not show by default. To
override, use QAction.iconVisibleInMenu for individual menu actions, or
set Qt::AA_DontShowIconsInMenus to false.

* cb517bd2e5e QBitArray: fix read of uninitialized terminating null
Fixed a regression introduced in 6.7.0 that could cause QBitArray to
report wrong bit counts after a bitwise operation.

* 34f6210bb6e Relax QHttpHeaders value field checks to allow UTF-8
Allows UTF-8 in header values now.

* a30591603b5 PDF: add support for PDF/X-4
Support for PDF/X-4 has been added.

* e309f0b0139 Core: Move SipHash implementation into separate file
Adapted copyright information for the SipHash Algorithm (used in Qt
Core).

* 159d63edb5f PDF: add a way to customize the output intent
New class QPdfOutputIntent.

* 894837577d8 QThread/Unix: fix normal exit/terminate() race
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

* 03a95f5f209 QtTest 3rdparty: updated Valgrind headers to version 3.23.

* 2d2975bd9fb Change the mimetype database embedded into QtCore
For licensing reasons, QtCore no longer ships a copy of the MIME
database from freedesktop.org's shared-mime-info project, but the one
from the Apache Tika project. The tika definitions don't have icons or
translated descriptions, but are sufficient for matching file types.

* ed2f80b75db QMimeDatabase: pick up XML mimetypes from :/qt-
project.org/mime/packages
QMimeDatabase can now pick up XML mimetype definitions from :/qt-
project.org/mime/packages. GPL-compatible projects which provide self-
contained binaries can use this to provide a copy of freedesktop.org.xml
that will be used instead of the TIKA mimetypes.

* 2347afc4197 CMake: Add partial fixes for archiving dSYMs with an Xcode
project
CMake-generated Xcode projects will now include debugging symbols by
default, regardless of configuration type, and Release-like
configurations will default to using dSYM bundles instead of keeping the
debug symbols in object files, to match Xcode project defaults.

* 4091f4ede0b Add Files field
Specify the source file that the "Mipmap generator for D3D12" component
consists of.

* b68eaebc86e Update benchlib's 3rdparty cycle counter to FFTW v3.3.10
QtTest's benchlib now uses FFTW v3.3.10's version of the clock-cycle
counter, Cycle.

* 6a0f00ac4e2 Updated CLDR data, used by QLocale, QCalendar and
QTimeZone, to v45, adding language Kuvi.

* b572a85b68a Remove GTK3 native menu
Due to deprecation of the gtk_menu_popup() function, we no longer use
GTK menus on Gnome: they are now rendered by Qt.

* ae515c3f2eb Fix signature of QDebug::toString() (again)
The toString() static function no longer allows the called operator<<()
to modify the argument. No Qt-provided operator<<() does that, and
operators that do are probably buggy.

* f53074c7470 QArrayDataOps: fix FP equality comparison
Fixed a bug when two QLists holding NaN values were considered to be
equal.

* 92006060683 rhi: d3d11: Wait in beginFrame with a max latency of 2
The D3D11 backend creates swapchains from now on with
DXGI_SWAP_CHAIN_FLAG_FRAME_LATENCY_WAITABLE_OBJECT by default, with a
max frame latency of 2.

* 1e6950fd77a rhi: d3d12: Also default to max frame latency 2
The D3D12 backend creates swapchains from now on with
DXGI_SWAP_CHAIN_FLAG_FRAME_LATENCY_WAITABLE_OBJECT by default, with a
max frame latency of 2.

* 42c467a11d5 Add __attribute__((format(printf()))) to q(v)nprintf()
Added attributes for GCC-compatible compilers to detect format/argument
mismatches. If this throws warnings for your calls now, don't ignore
them. printf() format mistakes could be security-relevant. You may also
find that you relied on undocumented behavior, such as that certain
implementations (Windows, Android, WASM) of qsnprintf() support
char16_t* instead of wchar_t* for %ls. In that case, you should port to
qUtf16Printable() and QString::asprintf(), or suppress the warning and
port away from the platform dependence at your earliest convenience.

* a9dbdcd9865 CMake: Add new signature to qt6_wrap_cpp
A new target-based signature was added for qt_wrap_cpp. The usage of
the previous output-variable signature is deprecated and will issue a
warning.

* 0eab6aac051 Introduce QT_NO_QSNPRINTF and mark QtCore as qsnprintf-
free
Added the QT_NO_QSNPRINTF macro to disable qsnprintf() and
qvsnprintf(), which will also be deprecated in 6.9. See the
documentation for details why we take this step.

* a83d113f663 Fixed a bug where partial_ordering::unordered != 0
comparison produced an incorrect result.

* 2b505519238 QIdentityProxyModel: add setHandleSourceDataChanges(bool)
Added setHandleSourceDataChanges(bool) method to allow sub-classes to
indicate to QIdentityProxyModel that they will handle source model data
changes on their own. Also added a getter, isHandleSourceDataChanges().

* 12bca469969 Remove inline downscaling in png reader
The PNG handler no longer implements progressive downscaling during
decoding when scaled image reading is requested.

* ae7ca75995f SQLite: Updated SQLite to v3.46.1

* 7805b3c32f8 Only define QT_SUPPORTS_INT128 if type_traits work for
them
Qt's support for 128-bit integers (qint128/quint128) is now conditional
on support for these types from the Standard Library, in particular
<type_traits> and <limits>. Qt no longer tries to work around missing
Standard Library support. As a consequence, e.g. GCC -ansi and GCC
-std=c++NN (instead of -std=gnu++NN, the default) builds will now no
longer support these types.

* aa9a9911698 Respect QTextDocument::defaultFont() in ODF writer
The ODF backend to QTextDocumentWriter will now respect the default
font set on the QTextDocument.

* 9993c1d13e6 Updated bundled Freetype to version 2.13.3.

* b88adc11886 Android: Updated Gradle to 8.10 and AGP to 8.5.2.

* eae3d0807a0 Convert a Qt ordering type to the weaker std ordering type
Added missing conversions from Qt ordering types to std ordering types.

* f1e15832ddc String Views: optimize the QByteArray/QString constructors
Creation of QLatin1StringView from QByteArray or QByteArrayView now
preserves the origin's isNull() status. This matches the behavior of
creating a QUtf8StringView from those types.

* 61b9195fc27 QIcon::pixmap() add a note about the changed behavior
QIcon::pixmap() is fixed to no longer scale the size, passed to
QIconEngine::scaledPixmap(), by the devicePixelRatio.

* e1f4f2ef47c String Views: add slice() methods
Added slice() methods to
Q{String,ByteArray,Latin1String,Utf8String,AnyString}View which work
like sliced() but modify the view they are called on.

* 1714af17217 QNetworkRequest::transferTimeout: saturate int return
value
The transferTimeout() function now returns INT_MIN or INT_MAX when
transferTimeoutAsDuration().count() cannot be represented in an int.

* 2f7d52a9ba1 Update tika-mimetypes.xml from upstream
Updated TIKA MIME types definition file to add the audio/aac and
application/x-java-keystore MIME types.

* 99f8efd0ef1 QStringTokenizer: Remove the undocumented
Q_STRINGTOKENIZER_USE_SENTINEL macro. It has been unconditionally
defined since Qt 6.0.

* d5109e4a88e Implement QTableModel::moveRows
Implemented moveRows in model. When sorting is enabled, setItem() now
moves the row to its sorted position, emitting rowsMoved rather than
layoutChanged.

* 514e2449133 All qFuzzyCompare() and qFuzzyIsNull() overloads are now
noexcept.

* e6ab7847a76 QTimer: make singleShot() have nanoseconds resolution
[1/2]: old-style
The singleShot() static methods now operate with nanoseconds
resolution, like QChronoTimer. The rest of QTimer remains milliseconds;
use QChronoTimer if you need a QTimer with nanoseconds resolution of
more than INT_MAX milliseconds range. Beware overflow that may occur
when passing large milliseconds objects that may overflow
nanoseconds::rep when converted.

* 6065ed99486 Pass QSslError::SslError by value
Made the QSslError::SslError QDebug operator<< a hidden friend of
QSslError. This means the operator is no longer a match for arguments
implicitly converting to SslError, only for SslError itself. A
backwards-compatible fix is to make the conversion explicit: debug <<
QSslError::SslError(arg).

* 60ed64e1d60 QTimerEvent: port to Qt::TimerId
Added constructor taking a Qt::TimerId. Also added a getter for
Qt::TimerId.

* f5a2d34da83 Add max_size() and maxSize() to view types
Added max_size() to all string-view types.

* c9fe636dfc3 QBasicTimer: port to Qt::TimerId
Added id() method returning Qt::TimerId.

* f2a5284d941 Update tika-mimetypes.xml from upstream
Updated TIKA MIME types definition file to add the audio/flac MIME type
as an alias for audio/x-flac MIME type.

* bc59c88186e Updated Harfbuzz to 9.0.0

* e4b298316dd QUrl::toString: fix using of NormalizePathSegments and
RemoveFilename
Fixed a bug that caused QUrl::toString(), QUrl::toEncoded() and
QUrl::adjusted() to ignore QUrl::NormalizePathSegments if
QUrl::RemoveFilename was set.

* 339feefc5c8 Update bundled libpng to version 1.6.44

### qtsvg
* 7e8298f Add QSvgRenderer default options setting
Added default options setting to QSvgRenderer

### qtdeclarative
* d4ca70eaa4 CMake: Fix the all_qmllint* targets for VS generators, take
II
When using CMake's Visual Studio project generator, the creation of the
targets all_qmllint, all_qmllint_json and all_qmllint_module requires
now CMake 3.19 or newer. A warning is printed for older CMake versions.
This warning can be disabled by setting QT_NO_QMLLINT_CREATION_WARNING.

* 5722c67490 CMake: Add a way to pass additional arguments to
win/macdeployqt
Added the DEPLOY_TOOL_OPTIONS argument to the function
qt_generate_deploy_qml_app_script.

* 107c5da80c Add --warnings-are-errors option to qmlcachegen
Added the --warnings-are-errors option that treats warnings as errors
when generating C++ code.

* 98c45e5344 API Cleanup: QQuickItem: Add parameter to
focusPolicyChanged signal
focusPolicyChanged signal now takes a Qt::FocusPolicy parameter.

* 2451ff25a5 Set default layout size policies for quick items
The QtQuick items now set their default size policy and it would be
effective when used within QtQuick Layouts.

* 0290e0fd52 Add imageSourceSize property to QQuickDrag
The attaching type Drag has a new imageSourceSize property, which can
be used like Image.sourceSize to scale the drag image during loading.

* 96299182fb Fall back to retrying with "software" when swapchain fails
The fallback to a software rasterizer, if applicable to the platform
and 3D API, is now performed also upon the first swapchain creation
failure. Previously this was only done if the QRhi initialization
failed. Relevant in particular on Windows, potentially allowing
functioning on systems that are incapable of proper accelerated D3D
rendering, but, for whatever reason, do not fail early on upon the
device/context creation, only later at swapchain creation.

* 6db942a87d doc: Clarify that automatic transient parent relies on
visual parent
Windows that automatically pick up a transient parent window from its
Item parent will not be shown unless the item is part of a scene.

* 4c355bf34e Material: remove ComboBox's insets
ComboBox's insets were removed. This may cause visual changes to UIs.

* 4a2466ea07 ApplicationWindow: explicitly set background size if not
explicitly set
ApplicationWindow now explicitly sets the width and height of its
background if no size was explicitly set by the user. This matches the
behavior of Control, and ensures that if e.g. an Image is used as a
window's background, any changes in its implicit size (e.g. after a
source change) won't affect its actual size.

* 25099f84c5 Flickable: don't allow dragging with mouse buttons other
than left
Flickable is meant to be dragged (flicked) by touch events; and as a
matter of legacy support, for now it can also be dragged by the left
mouse button. Dragging with other mouse buttons, such as the right and
middle buttons, is not allowed.

* 6777c19e39 CMake: Move generated qmltypes file into .qt subdirectory
of build dir
Generated .qmltypes files will now be placed into the .qt/qmltypes
subdirectory of a target build directory. The location is an
implementation detail that might still change in the future, so it
should not be relied upon.

* 57bc466592 CMake: Consider NO_UNSUPPORTED_PLATFORM_ERROR for non-
bundle mac apps
The qt6_generate_deploy_qml_app_script NO_UNSUPPORTED_PLATFORM_ERROR
option will now have an effect when calling the API on non-bundle macOS
executable targets.

* 60194389cd ItemView: Avoid undesired repositioning in updateCurrent
If highlightFollowsCurrentItem is set to false, and highlightRangeMode
is set to NoHighlightRange, then programatically setting the
currentIndex of the list will no longer scroll the view to that item.

* 822db20f84 Menu, MenuBar: remove requestNative and rely solely on app
attributes
Menu and MenuBar now use native menus by default on platforms where
they're supported.

* 8bf5aae19b QtQml: Properly enforce signatures of AOT-compiled
functions
The AOT compiled code for type-annotated JavaScript functions does not
let you pass or return values of the wrong type anymore.

* b41e8dc848 Allow specifying a custom blend operation in materials
QSGMaterialShader subclasses can now specify a blend operation
different from Add using the new GraphicsPipelineState members opColor
and opAlpha.

* 71e2598379 QML: Deprecate coercion on type assertions
A new attribute "Assertable" has been added to the "ValueTypeBehavior"
pragma. You should always use it if you want to type-check value types
using "as". If you don't use it, an instance of the type is created as
result of the "as" if the type doesn't match.

* 22272aefeb Add PathRectangle, a PathElement for optionally rounded
rectangles
Add PathRectangle, a PathElement for optionally rounded rectangles

* 237bdcd310 Support drag and drop section reordering in the table view
Added new property 'containsDrag' for the delegate, and it is set when
a user drags a column or row on top of another delegate. This property
is applicable only for HorizontalHeaderView and VerticalHeaderView.

* 7729ed61a6 Support targets for DEPENDENCIES/IMPORTS in
qt_add_qml_module
qt_add_qml_module now supports passing targets to the DEPENDENCIES and
IMPORT keywords when prefixed with TARGET. This requires opting into
Qt's CMake policy QTP0005.

* 333dd9e276 Android: Add Java QtAbstractItemModel as a QAIM wrapper
Added new public Java classes, QtAbstractItemModel and QtModelIndex to
wrap a subset of their C++ counterpart functionalities, through internal
proxies.

* a5b306650b QQuickMenuItem: add implicitTextPadding and textPadding
A MenuItem now has two new properties (implicitTextPadding and
textPadding) that can be used for aligning the text across all MenuItems
inside a Menu.

* bb370edeba AbstractButton: Add click() and animateClick()
Added click() and animateClick() functions to allow programmatically
clicking a button with or without visual changes.

* b8213a2322 Add new Fluent style for Qt Quick Controls
Introduction of Windows11 style for Qt Quick Controls.

* d807fb5078 qt_add_qml_module: Create qt.conf in build dir
When using CMake >= 3.19, qt_add_qml_module now creates a qt.conf file
in the build directory next to each binary. This sets up import paths
for targets passed to DEPENDENCIES and IMPORTS with the new TARGET
option.

* 1d5476fb24 a11y: Add a method for issuing a
QAccessibleAnnouncementEvent
Add support for sending announcement events to QtQuick apps.

* 612c00a0b6 Warn about unset required properties on composite
singletons
Instantiating singletons with unset required properties will now fail
and print a warning instead of creating the singleton with the
properties unset.

* 25a8845a7a qmllint: don't set error exit code if there are warnings
qmllint no longer exits with an error code if there are warnings by
default. Actual errors will still cause the exit code to be set.

* 14bb25f69c QJSEngine: Treat empty string literals as non-null, empty
QStrings
Assigning an empty JavaScript string to a property of type QString now
produces only an empty QString, not a null QString.

* 7629067009 Remove the Window.parent and Window.z properties
The Window.parent and Window.z properties added as tech preview in Qt
6.7 have been removed due to known failure scenarios that are still
being investigated. To embed a Window, use the explicit WindowContainer
item, which does not have any of the known issues.

* 1d5dda7ebe Material Style: update style theme when system theme is
changed
If the Material.theme is set to Material.System, the application theme
changes when the system theme is changed. This also works for the child
attached styles. If its theme is set to Material.System, regardless of
its attached parent style, it will follow the system theme changes.

* 21230d6028 QQmlComponent: Reject nested properties in
setInitialProperties
The undocumented ability to set properties of subobjects when setting
initial properties will now fail.

* 3481cbc3ab Enable popup windows for QtQuick.Dialogs
All dialogs in QtQuick.Dialogs will now use popup windows, if able.

* 1a0d477fb0 Fix rendering errors with Calibri Light and curve renderer
text
Fixed an issue where some fonts would exhibit artifacts when renderered
with the CurveRendering render type.

* c9c1a08409 QML: Type-check objects passed to QmlListWrapper
Assignments to list properties in QML are now type-checked. Before you
could, for example, insert a plain QObject into list<Item>, producing
undefined behavior. Now it instead inserts null and warns. In
particular, if you assign a JavaScript array of random objects to a list
property, QML will check each individual element, and insert null as
well as warn when encountering type incompatibilities.

### qtmultimedia
* edaec2bf7 Rename QAudio namespace to QtAudio
The QAudio namespace has been renamed to QtAudio, with QAudio still
being available as an alias. String based connections to
QAudioSink/Source::stateChanged need to continue to use QAudio::State as
the parameter.

* 6f590d44b Fix ABI breakage wrt QAudioSink/Source::stateChanged signals
Qt 6.7.0 broke binary compatibility by renaming the QAudio namespace to
QtAudio. Qt 6.7.1 restores compatibility with previous Qt 6 versions
again by making QtAudio an alias for the QAudio namespace, but breaks BC
with 6.7.0. Code previously built against 6.7.0 needs to be recompiled.

* 5673c4ed4 Add QVideoFrame constructor that converts from QImage
Added QVideoFrame constructor that converts from QImage

* 2a217aba3 Manage media backend lifetime using Q_APPLICATION_STATIC


* 7a3b2ff73 Update pffft version to the latest version from upstream
Updated pffft to fbc4058.

* d27311be4 GStreamer: add private API to access pipeline for capture
session
QMediaCaptureSession: GStreamer - private interface to access
underlying GstPipeline of QMediaCaptureSession

* 2937fe559 ALSA: use first device as default
ALSA: use first device as default, if ALSA doesn't report a default
device.

* 948ce7b3d Rename QVideoFrameFormat::frameRate => streamFrameRate
Renamed the property QVideoFrameFormat::frameRate to
QVideoFrameFormat::streamFrameRate.

* f6f7b38e7 Use correct stride factor with YUV420P10 pixel format
Fix display of videos using YUV420P10 pixel format

* 075da34d9 Add rotation property to QVideoFrameFormat
Added the property 'rotation' to QVideoFrameFormat.

* 49d1fb36a Add methods QVideoFrame::streamFrameRate and
setStreamFrameRate
Added the property 'streamFrameRate' to QVideoFrame.

* a42df322e GStreamer: custom audio io - introduce factory functions
QAudioInput/QAudioOutput: GStreamer - add private API to customize
audio input/output via a pipeline string.

* 134c74f13 Document dynamic linking of FFmpeg on macOS
Document that FFmpeg media backend links dynamically to FFmpeg
libraries on both Windows and macOS, and that applications using Qt
Multimedia with the FFmpeg media backend must deploy shared FFmpeg
libraries as part of their installers.

* cae22b1b6 Implement QAudioBufferInput and QVideoFrameInput
Added classes QAudioBufferInput and QVideoFrameInput allowing to send
custom media data to QMediaRecorder.

* 0fbdd3f57 Add QtVideo::MapMode, deprecate QVideoFrame::MapMode
Added the namespace QtVideo::MapMode, deprecated QVideoFrame::MapMode.

* ec69c074d Android: doc update of deprecating the Android back-end
Deprecated MediaCodec Android back-end

* 95ba80139 GStreamer: QGstreamerVideoSink - improve conversion element
override
QVideoSink: GStreamer - allow override of conversion element via
environment variable

* 14f6acdbe Expose QAbstractVideoBuffer in public API
Added QAbstractVideoBuffer that allows to provide custom data to
QVideoFrame. Added a QVideoFrame's constructor taking
QAbstractVideoBuffer.

* a96d1bf66 Add the property QMediaRecorder::autoStop
Added the property QMediaRecorder::autoStop making the media recorder to
stop at the and of input streams.

* 55069941c Implement QAudioBufferOutput, as a custom output for
QMediaPlayer
Added QAudioBufferOutput allowing to get the decoded audio data from
QMediaPlayer

* 7a805b99f Add pipewire screen capture on Wayland
Added screen capture function on Wayland via pipewire.

* 78d2f104a Override the signal 'videoFrameChanged' in qml video sink
Removed QVideoFrame parameter from the not documented qml signal
VideoSink.videoFrameChanged.

* c8e658e2f Update FFmpeg version in documentation
Updated FFmpeg to n7.0.2.

* 4c3810cf3 GStreamer: increase the minimum required version to 1.20
Minimum required GStreamer version is raised to 1.20

### qttools
* 66aebd35a CMake: Fix qt_add_translations in different subdirs for VS
generators
When using CMake's Visual Studio project generator, the creation of the
update_translations target requires now CMake 3.19 or newer. A warning
is printed for older CMake versions. This warning can be disabled by
setting QT_NO_GLOBAL_LUPDATE_TARGET_CREATION_WARNING to ON.

* 1d22163ad qdoc: Make -outputdir cmd line option relative to current
working dir
The path provided with the -outputdir command line option is now
relative to the current working directory when running QDoc.

* c51980bb0 QDoc: Ensure `nosubdirs` doesn't mangle `outputdir`
The `nosubdirs` configuration variable no longer removes the last
segment in the `outputdir` path. To retain previous behavior for
projects that define `outputsubdir` and `nosubdirs`, prepend
`outputsubdir` with `../`.

* ffd3d0c70 QDoc: Stop generating .qhp.sha1 files
QDoc no longer generates .qhp.sha1 hash files.

* 1d4d82e64 Update qlitehtml submodule
Litehtml (used in Qt Assistant) wasupdated to upstream version v0.9.

* 0532419f7 qdoc: Handle future versions in \deprecated [<version>]
command
The \deprecated command now correctly handles deprecations in a future
version.

* 5aaa1b0b2 QHelpEngineCore: Remove the old hack for dynamic readonly
property
Remove the old hack with setting the dynamic "_q_readonly" property to
change the read only mode. Use QHelpEngineCore::setReadOnly() instead.

* 10a1d2658 qdoc: Introduce the \tm command for handling trademarks
A new command, \tm, was introduced to manage trademarks in the
documentation.

* 5001aead1 QDoc: Introduce '\nativetype' command
The new 'nativetype' command supercedes the 'instantiates' command. New
documentation should use the new command.

* cd03ff5e7 QDoc: Deprecate '\instantiates' command
The '\instantiates' command is deprecated and will be removed in a
future version of QDoc. Use the new '\nativetype' command instead.

* 2a47e26e4 qdoc: Require libclang >= 17
QDoc now requires LLVM 17 or newer.

* 3d2d8c375 QtHelp API review: Make QHelpContentItem non copyable /
movable
The QHelpContentItem class is not longer copyable, because copying
results in double-deletion errors.

* d27b63e48 CMake: Add TS_FILES_OUTPUT_VARIABLE argument to
qt_add_translations
Added the TS_FILES_OUTPUT_VARIABLE argument to qt_add_translations. Use
this to get the .ts files that have been automatically determined by
qt_add_translations.

* 2533a207b Change the shared Qt solutions headers to be proper private
headers
The headers of the shared Qt solutions have been renamed to be private
headers using the _p.h suffix.

* 21d7ad352 QtHelp API review: Make QHelpContentItem final
The QHelpContentItem class is now final (it lacks a virtual
destructor).

* dbfd273cb QDoc: Allow author to specify `auto` as return type in `\fn`
command
QDoc now respects the author's intent better, in that it outputs `auto`
as the return type of functions that are documented with `auto` as their
return type.

* a76b6ddc3 Qt Designer: Change the default mode to docked for macOS,
too
Qt Designer now starts in docked mode by default on macOS, too.

### qtdoc
* 9ffd52c5 Update documentation for QHash's heterogeneous lookup feature
.

### qtpositioning
* 0f3efd9b Android: allow to convert altitude to MSL on Android 14 and
later
Intoroduce a plugin parameter that allows to convert the altitude from
WGS84 to MSL. This parameter works only on Android 14 and later. By
default the altitude is still returned in WGS84 format for backwards
compatibility.

### qtsensors
* 5c5b0baa Attribute Third-Party Code in Android Sensors Plugin
Add attribution for Android getRotationMatrix and getOrientation code,
copied from Android sources under Apache-2.0. This code is only used on
Android, as part of the Android Sensor plugin.

### qtconnectivity
* be1a9e8d Unregister Bluetooth profile UUID after connection
Unregister Bluetooth profile UUID after connection, so it can be
registered for connecting to new devices.

* 9163f008 iOS: Distinguish security violations from other connection
errors
Add a new UnsupportedTargetError error code.

* 39e673bb sdpscanner: fix format strings for (u)int64_t
Fixed a bug involving broken serialization of SDP_(U)INT64 DTDs on Big-
Endian machines.

### qtwayland
* 9db8724e Client: Emit wlSurfaceDestroyed after actually destroying
wl_surface
The QWaylandWindow::surfaceDestroyed() signal is emitted after actually
destroying the wl_surface object.

* 12608dfd qtwaylandscanner: Send null for a null QString with allow-
null
String arguments in a request will now send null rather than empty
string for a null QString if the argument is declared with "allow-null".

* 40116ae3 Add GNOME-like client-side decoration plugin


* f6c4b2f0 ShellSurfaceItem: Make sure modal dialogs stay on top
ShellSurfaceItem will keep modal dialogs on top of other surfaces when
using XdgShell.

* f67962df CMake: Move each wayland protocol into a separate
subdirectory
Split the single qtwayland 3rd party qt_attribution.json file into
multiple ones, per protocol, to ease maintenance.

* 98456a97 compositor: Implement drag and drop for touch events
Fixed an issue where drag operations could be initiated by touch
events, but it would not be possible to drop the contents.

### qt3d
* 491e25e10 Fix ambient color contribution in Phong shader
Fix ambient color contribution

* 7dd1fe963 Enable uniform buffer for RHI compute shaders
Enable uniform buffer for RHI compute shaders

* d772f48e8 RHI: add support for Int and HalfFloat attributes
Add support for Int and HalfFloat attributes

* f4f3c945a Update imgui to latest version
Updated imgui to version 1.91.0

* d55c9c7b2 Update assimp to 5.4.3
Update ASSIMP to v5.4.3

### qtimageformats
* 3cf1295 TIFF: add support for CMYK image load/save
Added support for loading and saving of 8-bit CMYK TIFF files.

* a5e0b01 Update bundled libwebp to version 1.4.0
Update bundled libwebp to version 1.4.0

* 349833fca48 Update bundled libtiff to version 4.7.0
Bundled libtiff was updated to version 4.7.0

### qtserialbus
* 0eab51e1 CAN: Allow querying all available devices at once
The new overload QCanBus::availableDevices(QStringList *) can be used
to query all available CAN interfaces in the system at once.

* 9d8501e9 VectorCAN: Set CAN-FD configuration only for uninitialized
channels
Fixed XL_ERROR when try to set CAN-FD configuration for a virtual
channel which was already opened by another application.

* 689c02d5 Fix virtual can backend usage in multithreaded environment
Fixed a race condition during creation of the VirtualCanServer when two
QCanBusDevices are instantiated in the same process in different threads

* 865e15a0 Fix virtual can backend usage in multithreaded environment
Fixed a race condition during start of the VirtualCanServer in
multithreaded environment

### qtwebengine
* de57e1b0b Add new API for screen capturing
Add QQuickWebEngineView::desktopMediaRequested() signal

* dbfa94722 Add WebEngineDriver
Added WebEngineDriver

* 56a4d784e Add hasPostData to QWebEngineNavigationRequest
hasFormData has been added to indicate navigations request (re)posting
form data.

* 7302e3eb4 Allow succeeding URLRequestJobs without actual content
loading
QWebEngineUrlRequestJob::NoError is deprecated

* 02b8b5afb Implement optional website permission persistence
Added new API to control permission persistence.

* 3df5f39db Add QWebEnginePermission and rewrite permissions API
Added new API for querying and modifying website permissions.

### qtwebview
* 3ceb65d windows: Fix freeze when loading Qt Web Engine plugin
Fixed a freeze on startup on Windows. As part of the solution for this,
the Qt Web View library now depends directly on Qt Web Engine on
Windows, instead of indirectly via the plugin library.

### qtnetworkauth
* 2a4c897 Ensure the code is not encoded a second time if already
percent encoded
OAuth2 providers might be sending the authentication code already
percent encoded. This is the case of Google. This now a supported use
case and the code is not systematically encoded anymore.

* a2e2292 Document QOAuthUriSchemeReplyHandler
Added QOAuthUriSchemeReplyHandler class

* 6823351 Add support for PKCE
Added PKCE support and turned it on by default

* 0425611 Remove redirect_uri parameter usage with token refresh
redirect_uri parameter is no longer included in access token refresh
request

* f7a6cdf Don't clear QAbstractOAuth2::scope upon empty server response
If the authorization server returns an empty 'scope' response, the
requested scope is not cleared anymore. Instead, it is assumed that the
requested 'scope' was granted.

### qtquick3d
* d3f6fe0b3 Add more QQuick3dViewport picking alternatives with mouse
coords
Added additional picking alternatives that allows for dynamically
checking against a subset of the models in a scene.

* c3dbb5b6f Add support for flat varyings
Custom materials and postprocessing effects can now support passing
data without interpolation between the vertex and fragment stages. This
is achieved by prefixing the type with the 'flat' keyword in the VARYING
declaration.

* 7b4fa9c3e Make instances the default property of InstanceList
The default property is now instances.

* 0c85d183b Implement Cascading Shadow Maps (CSM)
Add support for Cascading Shadow Maps in DirectionalLight.

* b20fd4dcc Add PCF soft shadows support
Add PCF soft shadows support. This change will affect the appearance of
all shadows and might require manual updating of the shadow mapping
settings in your app.

* f202f199c Update Assimp to v5.4.2
Updated Assimp to v5.4.2

* 914114f00 Update TinyEXR to v1.0.9
Updated TinyEXR to v1.0.9

* b3925be03 Update Assimp to v5.4.3
Updated Assimp to v5.4.3

### qtshadertools
* 998086b Change classification of NVIDIA license
Re-classify previous custom nvidia license as AML-glslang, as
introduced by the newest SPDX version.

* fa6a085 Update identifier and name for Khronos license
Change name of Khronos license to 'MIT Khronos - old variant', as it is
now called in SPDX: https://spdx.org/licenses/MIT-Khronos-old.html .

### qt5compat
* dd0ddad QText{En,De}coder: use DefaultConversion
Fixed a bug that caused QTextEncoder not to write the Byte Order Mark
for UTF codecs when the constructor without explicit flags was used.

### qtopcua
* 43cb4360 Replace incorrect license attribution for 3rdparty/open62541
Correctly refer to the CC-BY-SA0 license as "Creative Commons
Attribution Share Alike 4.0 International".

* b1f8405a Fix status code handling for monitored items
Report the right status code for monitored item updates

### qtlanguageserver
* 7784458 JSON-RPC/QtLanguageServer: Enforce static builds
The (private) JsonRpc and LanguageServer modules are now always build
as static libraries.

### qthttpserver
* 3bd2834 Add function to register functions that verifies WebSocket
upgrades
Add function to register callback functions that verifies WebSocket
upgrades

### qtgrpc
* e3abfef0 Make QProtobufSerializer and QProtobufJsonSerializer non-
stateless
Any type API is changed. 'as' and 'fromMessage' functions not accept
the pointer to a serializer.

* ac4a2fc7 Make the both QProtobufSerializer and QProtobufJsonSerializer
final
Both QProtobufSerializer and QProtobufJsonSerializer are final now.

* 001bcf2f Use the QML_NAMED_ELEMENT for the gRPC client in QML context
gRPC clients now are registered as <ServiceName>Client in QML context.

* de50547f Rename 'propertyOrdering' static member of protobuf messages
to 'staticPropertyOrdering'
The 'propertyOrdering' static member is renamed to
'staticPropertyOrdering'.

* 39d27ad7 Add the QProtobufMessage::propertyOrdering method
Added the ordering argument to the QProtobufMessage constructor.

* 2d0897ce Extend interface of gRPC operation with methods supporting
QProtobufMessage
Added the following interfaces to gRPC operation classes:-
QGrpcOperation::read(QProtobufMessage *message) const-
QGrpcClientStream::sendMessage(const QProtobufMessage *message)-
QGrpcBidirStream::sendMessage(const QProtobufMessage *message)

* d737f7a5 Remove the Q_DECLARE_PROTOBUF_SERIALIZERS macro
The Q_DECLARE_PROTOBUF_SERIALIZERS macro is removed from the API and is
not generated anymore.

* ae2f1ed3 Fix the generation of the export macro
New option extras allow setting the generated export filename and
control if it should be generated at the generator run.

* 5dfafece Generate the explicit presence flag for protobuf message
fields
All fields that have explcit presence now set the 'ExplicitPresence'
flag in their property ordering structures.

* d69bc697 Remove the 'stream' prefix from all streaming methods
The 'stream' prefix is removed for all generated streaming methods.

* ec8a3fec Remove errorOccurred interface signal from grpc operations
The QGrpcOperation::errorOccurred and
QGrpcChannelOperation::errorOccurred signals are removed.

* 21ceb0f3 Remove the QtProtobuf::repeatedValueCompare function
The QtProtobuf::repeatedValueCompare function was removed. Using op==
is a backwards-compatible fix.

* 4cfc2688 Make the protobuf serializer registry private
Added QProtobufRepeatedIterator. QVariant that contain repeated or map
protobuf values can be converted to this class using QVariant::view
method.

* a433f657 Assert if QGrpcOperationContext::serializer returns null
QAbstractGrpcChannel implementations now are obliged to supply
QGrpcContext with the valid serializer. Any attempt to deserialize the
returned message with null serializer now will lead to assert or SEGV.

* b84b7054 Remove QGrpcOperation::deserializationError(String) methods
QGrpcOperation::deserializationError and
QGrpcOperation::deserializationErrorString methods are removed.

* aab32a01 Make error handling in QAbstractProtobufSerializer generic
QAbstractProtobufSerializer::DeserializationError is renamed to
QAbstractProtobufSerializer::Error and now contains list of both
possible serialization and deserialization errors.

* c195c56b Migrate to std::unique_ptr return value for all RPCs
All generated RPC methods now return std::unique_ptr instead of
std::shared_ptr. This change explicitly defines that caller takes the
ownership of the returned pointers.


Fixes
-----

### qtbase
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
* QTBUG-18057 QPixmap::toWinHBITMAP(): 2 Bugs when running out of memory
(Access violation or lost HBITMAP handle)
* QTBUG-49720 Documentation for QFileDialog::DontConfirmOverwrite should
mention QFileDialog::AcceptMode
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
* QTBUG-119225 [Reg 6.2 -> 6.5] QSplashScreen no longer shows on Linux
with a single call to QCoreApplication::processEvents()
* QTBUG-120006 DeleteStartOfWord with a selection in QLineEdit has
unexpected behavior
* QTBUG-119972 Clang-tidy reports possible memory leak with
QMetaObject::invokeMethod
* QTBUG-120054 Reg6.4->6.5 Stylesheet has no Effect on QMessageBox
* QTBUG-115765 QAbstractItemView::EditingState: state stale when editing
with a proxy model
* QTBUG-119902 Crash in QImage::scaled
* QTBUG-119995 QML - Text - Font weight - macOS/Windows difference
* QTBUG-117903 WM_CHAR creates unwanted keyboard event - activating
shortcut
* QTBUG-92016 High DPI, bad SVG quality, wrong screen selected for
current window
* QTBUG-94203 Icon drawing bug ofStyleSheetStyle in a mixed-dpi
environment
* QTBUG-119708 VS2022 simple program fails to link in Release mode with
ProtobufWellKnownTypes
* QTBUG-119167 Atspi.Table.get_row_column_extents_at_index can cause
segfault in tree
* QTBUG-110266 affine example crashes when moving the center hoverpoint
* QTBUG-119752 Customized QToolTip with padding or margin displays
incorrectly
* QTBUG-112920 FTBFS qt 6.5.0 on gcc 9
* QTBUG-120062 Non-native QFileDialog gets frozen on destruction if
remote mapped drive is disconnected
* QTBUG-47159 QFileDialog::selectFile does not keep native separators
* QTBUG-120055 When dragging QTableView columns scrolling behaves oddly
* QTBUG-113573 When dragging a header section it will no longer scroll
when at the edge
* QTBUG-120141 cmake build of a Qt project with static Qt linkage fails
due to error in qtbase/cmake/FindWrapResolv.cmake
* QTBUG-119619 CMake deploy script finds x64 libraries for WoA
application.
* QTBUG-117704 Dragging Window handling WM_NCCALCSIZE and WM_NCHITTEST
squishes contents
* QTBUG-120121 a11y QComboBox: Problematic signal/slot activation order
* QTBUG-119526 [Reg 6.6.0->6.6.1]QCocoaAccessibility Crash with Mac
VoiceOver enabled
* QTBUG-120125 CMake subarch extraction does not always succeed
* QTBUG-117975 Memory leaks when QObject::deleteLater is used without
QApplication runloop
* QTBUG-116989 wasm:pen pointerhandler example does not work as
expected
* QTBUG-113865 [Text Editor]Using undo function causes the app to crash
* QTBUG-120257 widgets/itemviews/editabletreemodel not compiling on
Android
* QTBUG-118489 Can't tab to last button in QDialogButtonBox
* QTBUG-50403 QDrag conflict with hover of widgets
* QTBUG-120167 Reg->6.7: QComboxbox hover is broken
* QTBUG-120012 Limiting maximum allocation size for QDataStream
* QTBUG-119178 Crash after registering an invalid resource file
* QTCREATORBUG-30117 Help viewer: "[read-only]" tags have unreadably low
contrast in dark mode
* QTBUG-120107 PDF view gets render mistakes on Android 10
* QTBUG-119113 windows: Stack overflow when dragging to/from embedded
native window
* QTBUG-120309 Public ABI break in 6.7 beta 1
* QTBUG-119750 QByteArray::indexOf(char) faster than
QByteArrayView(QByteArray)::indexOf(char)
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
* QTBUG-120474 4xMSAA doesn't work with Mali400 using Lima driver
* QTBUG-120332 [REG 6.6.1 -> 6.7] rendering svg causes division by zero
in getRadialGradientValues
* QTBUG-120335 On certain machines QtConcurrent crashes if no free
threads on thread pool
* QTBUG-120302 AddressSanitizer: heap-use-after-free in
tst_QFuture::continuationsWithContext()
* QTBUG-120572 [QDoc] Redundant text in QTabBar detailed description
* QTBUG-103825 Wrong resolution of Icon in Windows (Toast) Notifications
* QTBUG-120350 QOffScreenSurface::isValid always returns false on
WebAssembly
* QTBUG-118503 WASM: arrow keys and select-all not working for
QPlainTextEdit on touchscreen
* QTBUG-119501 Numbers colliding and not highlighted in Charts with
Widgets Gallery example
* QTBUG-86792 Port tests/auto/corelib/plugin/qpluginloader/machtest
projects to CMake
* QTBUG-120548 QSqlQuery::positionalBindingEnabled improvements
* QTBUG-120487 Symlinks generated in user_facing_tool_links.txt during
configuration are incorrect for MacOS
* QTBUG-120624 UB when passing null string to QString::arg()
* QTBUG-120614 QImage::convertToFormat: wrong conversion from RGBA64 to
RGBA16FPx4
* QTBUG-120758 qtdeclarative fails to build with conan 2 on windows:
include path too long
* QTBUG-120574 QComboBox popup high decreases when hiding view items
* QTBUG-90876 QShGetFileInfoThread never gets destroyed
* QTBUG-83604 QSlider with ticks is glitchy with QFusionStyle
* QTBUG-111314 Adding padding to QSlider does not work on Fusion style
* QTBUG-120762 Use after free
* QTBUG-120297 Q_GADGET forces following elements to be private
* QTBUG-117533 QProcess does not work with thread sanitizer
* QTBUG-117954 QProcess::startDetached quits application when running
with ASAN
* QTBUG-104493 Application performance drops if many threads are running
while QProcess creates sub-processes on Unix
* QTBUG-120766 qstorageinfo.cpp compile error 6.7.0-beta1
* QTBUG-120317 qt6<target_name>_debug_metatypes.json: illegal value
* QTBUG-120687 6.7/API review: QIcon theme API clashes with <windows.h>
* QTBUG-58005 ibus: commit does not properly reset the preedit string
* QTBUG-120748 Win11 Style: QMessageBox text invisible when using dark
theme on Windows
* QTBUG-120732 Qimagereader manual test - Image file is missing
* QTBUG-121041 Fusion style: add clip region for groupbox title
* QTBUG-121030 QIconLoader failed to find icon in hicolor
* QTBUG-120485 QT_INSTALL_DOCS configured with wrong path
* QTBUG-121015 tst_QGuiApplication::topLevelAt() failed on Wayland
* QTBUG-118867 Render thread can delete font engines still in use
* QTBUG-121135 QNetworkRequest::setTransferTimeout linkage on MinGW
* QTBUG-120619 QHttpServer with QtConcurrent blocks until the very first
request has finished before being able to process in parallel
* QTBUG-119248 The result of calling serviceUUID is different in Q5 and
Qt6
* QTBUG-120961 QLocale::monthName() doesn't work correctly on Windows
* QTBUG-113402 qt6_wrap_cpp doesn't work for C++ source files
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
* QTBUG-120907 FE_INVALID in tst_QPainter::fpe_radialGradients()
* QTBUG-120962 QTextCursor::removeSelectedText leads to crash
* QTBUG-120509 Crash when Qt re-create native windows if
WA_DontCreateNativeAncestors is set
* QTBUG-120436 sqldrivers always build in release
* QTBUG-114958 dev/6.7: Windows: qsb crashes in debug build, causing
qtdeclarative build to fail
* QTBUG-114941 Qt 6.6 Beta 1 and Qt Creator 11.0.0-beta2 - Test
permissions - Bluetooth fails on Android 14
* QTBUG-121498 tst_QAbstractItemView::removeIndexWhileEditing() failed
on Wayland
* QTBUG-120469 Crash in QCocoaSystemTrayIcon::emitActivated() when
calling QComboBox clear() then addItem()
* QTBUG-121008 Crash in QMacAccessibilityElement when using
QTreeView/QCombobox
* QTBUG-121040 [Reg 5.1 -> 5.15 and all 6.*] QTextDocumentation does not
handle background of HTML string correctly
* QTBUG-118238 【Windows】stack overflow after launch Any Qt Application
(or Official Demo)
* QTBUG-121515 [Reg 6.6.1 -> 6.6.2] QNetworkAccessManager never finishes
request if server sends status code 401 without a challenge
* QTBUG-120264 Inactive radio buttons partially respond to click
* QTBUG-121403 embedded window invisible with transparent window
* QTBUG-115989 Shadowed Q_PROPERTY with non-empty params NOTIFY breaks
compilation
* QTBUG-74471 QFileSystemModel shows directories with
setFilter(QDir::Files)
* QTBUG-115459 Possible infinite loop triggered by unmaximizing the
window in 6.5.0+
* QTBUG-121557 [Reg 6.4.3->6.6] Application unusable after closing
nested message boxes
* QTBUG-111994 Deal with a font face at index 0 as Regular for Variable
fonts
* QTBUG-112136 Unable to pick up styles properly from Variable fonts
* QTBUG-111796 Qt Font Scaling for bitmap fonts is broken in Wayland
* QTBUG-119532 Starting Android app fails with AST
* QTBUG-121468 QDomDocument missing parameter names in `toString()` and
`toByteArray()`
* QTBUG-121713 QXkbCommon::keysymToQtKey does not map XF86Calculator
* QTBUG-121729 error: Multiple commands produce same *_metatypes.json
* QTBUG-120688 Explicitly document behavior for QFileInfo if file is
directory
* QTBUG-99178 QFileSystemModel should have an option to disable icon
loading; crashes if the icon provider is null
* QTBUG-121485 QLocale method nativeCountryName returns wrong values.
* QTBUG-117429 TIFF AnimatedImage memory leak
* QTBUG-120633 REG->6.7: Windows11/Vista palette issues (bright)
* QTBUG-120722 markdown with yaml front matter is parsed wrong
* QTBUG-120369 iOS: Crash after changing screen orientation
* QTBUG-120530 QDomDocument doc refers to QXmlQuery which doesn't exist
in Qt6
* QTBUG-109073 [REG] Memory leak in QJsonObject
* QTBUG-121873 The description and the snippet don't match in
QDBusAbstractInterface::asyncCall
* QTBUG-121947 qDebug() output is missing newline on Windows
* QTBUG-121667 Qt Notifier app is crashing immediately after being
launched for the first time after deployment
* QTBUG-121668 Qt Notifier example - notifications do not work on
Android 13
* QTBUG-108068 QNetworkAccessManager should handle all informational
HTTP replies
* QTBUG-121697 Critical crash when creating QPlainTextEdit when using
styles/stylesheets.
* QTBUG-121790 QApplication::setStyleSheet crashes QTextEdit
* QTBUG-121948 RCC compression is broken when deploying to Android from
a Linux host using CMake
* QTBUG-106466 build android app with Debian host fails on undefined
symbol qt_resourceFeatureZstd
* QTBUG-101353 AUTORCC uses zstd even if Qt is build without rcc support
* QTBUG-121670 QDom related classes with anonymous parameters make
PySide 6 bindings awkward to use
* QTBUG-122037 error: ambiguous template instantiation for ‘struct
std::indirectly_readable_traits<QVersionNumber::It>’
* QTBUG-103476 Custom`Delegate::destroyEditor()` is not called for some
editor when removing a tree branch
* QTBUG-122054 Massive performance loss of QTreeView::expandAll
* QTBUG-121875 Typo in the document
* QTBUG-119795 Adding QOpenGLWidget to a QDialog in a maximized
QMainWindow maximizes the QDialog
* QTBUG-120316 Cannot close window after hiding and showing again
* QTBUG-73021 Regression: [5.11.0 -> 5.11.1] QGLWidget paintEvent is not
called if a QGLWidget is contained in a dialog that is closed and then
reopened
* QTBUG-122087 QTimer::isActive returns true if interval is Invalid
* QTBUG-85425 Fusion style adds unneeded space for QGroupBoxes without a
title on Linux
* QTBUG-95472 CLONE - Fusion style adds unneeded space for QGroupBoxes
without a title
* QTBUG-116080 Inconsistent hashing between qint{32,64} on 32-bit
platforms
* QTBUG-122210 [REG 6.6.1->6.6.2] widgets/itemviews/editabletreemodel
not compiling on iOS
* QTBUG-121996 Not possible to run unit tests with ctest on windows
* QTBUG-116927 markdown writer omits trailing ** if a bold span exceeds
the wrap limit
* QTBUG-106526 markdown writer should never wrap headings, but wraps
them if they are too long
* QTBUG-121906 Copyright year in so files not updated to 2024
* QTBUG-121928 Remove Copyright year from About Qt & command line tools
* QTBUG-122200 Header files are not being copied into the Qt* frameworks
in custom build
* QTBUG-119447 RHI - QRhiResourceUpdateBatch::readBackBuffer() fails to
read compute buffer on Metal
* QTBUG-121881 QT_DEPLOY_QML_DIR: Custom value causes empty "qml" folder
to be created
* QTBUG-121880 QT_DEPLOY_TRANSLATIONS_DIR is ignored
* QTBUG-121764 [Reg 6.6->6.7] Funny theme icon
* QTBUG-122266 property "AUTORCC_OPTIONS" is not allowed
* QTBUG-122139 DirectWrite's default hinting looks off
* QTBUG-122167 REG: Kerning errors with DirectWrite font backend
* QTBUG-114608 Programmatically setting focus does not move VoiceOver
* QTBUG-122254 Documentation example of
QCborStreamReader::readString()/QCborStreamReader::readByteArray is
wrong
* QTBUG-122214 REG->6.7: Windows 11,Linux: Dock icons blurry (w/o High
DPI scaling (all styles)
* QTBUG-118643 REG->6.7 : Fusion style QDockWidget buttons are too large
* QTBUG-122138 QTzTimeZoneCache::findEntry() parses files while holding
QTzTimeZoneCache::m_mutex
* QTBUG-122272 Some buttons from QStyle::StandardPixmap have artifacts
in the background in the dark mode
* QTBUG-119864 QPushButton or QToolButton does not receive mouse events
after calling setMenu().
* QTBUG-122192 CONFIG *= silent fails at linking
* QTBUG-114706 exported cmake targets link versionless targets when they
shouldn't
* QTBUG-122398 6.7/Windows 11/Modern style: Crash with
QGraphicsProxyWidget
* QTBUG-122176 RCC should generate warning-free code.
* QTBUG-121380 No info after setting the QT_LOGGING_DEBUG env var
* QTBUG-122451 Floating point in raster drawBitmap together with strict
QImage::scanLine causes assertion "i >= 0 && i < height()"
* QTBUG-110686 wasm: declarative apps on Android appear black
* QTBUG-122648 Crash when moving application to background and bring it
back
* QTBUG-122624 REG: QDirIterator unicode handling broke in Qt 6.8
* QTBUG-122622 configure on Windows can't handle unquoted -DFOO=0
arguments
* QTBUG-122691 Dependency update on qt/qttools failed in 6.7
* QTBUG-122674 Build failure on x32 ABI
* QTBUG-88721 QTextDocument::find() does not work well with
QRegularExpressions
* QTBUG-113255 QML view doesn't update properly when device is rotated
with permission dialog.
* QTBUG-122168 REG: Monochrome emojis with DirectWrite font backend
* QTBUG-118983 CTest prints output from a failed test twice
* QTBUG-122109 QTreeWidget's columns do not seem to resize properly
after upgrading from Qt6.5.3 to Qt6.1.1
* QTBUG-120699 QHeaderView in QTableView doesn't restore geometry
* QTBUG-121389 tst_qmessagehandler::qMessagePattern(backtrace
depth,separator) fails on qemu-armv7-developer-build
* QTBUG-122637 qmessagebox.h: extra ';' after member function definition
[-Wextra-semi]
* QTBUG-121822 WASM Clang++ ignores EXCEPTIONS settings in asyncify
config
* QTBUG-116550 [schannel] Qt warning "QIODevice::write (QTcpSocket):
device not open"
* QTBUG-121126 Crash when restoring maximized window of application with
tabified dock widgets
* QTBUG-122300 Fix conversion warnings in tst_qstring
* QTBUG-122301 Fix conversion warning in tst_qresultstore
* QTBUG-107486 Typo in the document
* QTBUG-96348 QWindowsSystemTrayIcon::showMessage: Windows Handle leak
* QTBUG-62945 Windows: QSystemTrayIcon::showMessage causes GDI-Object
leak
* QTBUG-122739 qtpaths/qmake don't honor qtconf in some cases with LTO
enabled
* QTBUG-119080 a11y: Checkbox lacks AT-SPI "checkable" state
* QTBUG-122073 If SQL Engine does not support lastInsertId QList will
assert
* QTBUG-122001 QMainWindow::tabifiedDockWidgets() - Not accurate
* QTBUG-120571 QGuiApplication::palette() returns incorrect values on
Windows 11
* QTBUG-81662 Indentation in QML RichText after list is wrong
* QTBUG-120254 Cell value leaking into other cells when entering new
value
* QTBUG-119611 QPlainTextEdit access violation crash when inserting
136,348,169 latin characters
* QTBUG-122749 [Crash] WebEngine Print Me example app crashes when
changing the page orientation
* QTBUG-121755 Handle information HTTP replies (1xx) for HTTP/2
* QTBUG-122642 The SQL QODBC driver implementation fails to escape
passwords set with setPassword(...) when using special characters.
* QTBUG-120694 QDockWidget resize issue with Qt 6.6.1
* QTBUG-102196 QDockWidget: wrong mouse cursor icon used when dock
widget floating, has custom title bar & contains window container
* QTBUG-40561 QDomText::splitText leaks memory
* QTBUG-105871 QUdpSocket stop emitting ReadyRead signal in
QueuedConnection
* QTBUG-115598 tst_QWidget::render() with QtWayland failed on Ubuntu
22.04, GNOME
* QTBUG-96051 markdown writer: in a table cell ending with backslash,
it's not escaped
* QTBUG-122083 Markdown writer fails to escape special characters
* QTBUG-122914 "OpenGL functionality tests failed" despite configuring
with "-no-opengl"
* QTBUG-122687 libraries contain wrong runpath
* QTBUG-121561 Android: in TextField: cannot edit inside of words, only
at the end [regression]
* QTBUG-122663 Live Preview doesn't work on Boot2Qt
* QTBUG-122944 Dragged toplevel is re-attached even after
wl_data_device.leave
* QTBUG-122949 Toplevel drag only works on left monitor
* QTBUG-122982 assertion failure while reading markdown file that
contains front matter but is otherwise empty
* QTBUG-122720 tst_toolsupport::offsets(QFilePrivate::fileName) fails on
x32 ABI
* QTBUG-120639 [REG 6.6.1 -> 6.7.0-beta1] Menu items too wide on 4K
* QTBUG-118434 [Reg Qt5->Qt6] QMenu cannot arrange menu entries
correctly when there are large quantity of them
* QTBUG-123005 [Reg 6.2->6.5+] Qt::AA_ShareOpenGLContexts has stopped
working for offscreen rendering
* QTCREATORBUG-30425 Android C++ breakpoints does not work with Qt
Creator
* QTBUG-121514 [Reg 6.6.0->6.6.2] Focus wrong in dialog with
QDialogButtonBox
* QTBUG-120049 [REG 6.6.0 --> 6.6.1] Incorrect child widget has focus in
dialog by default
* QTBUG-119003 QPrinter fullPage mode behaves differently on Windows
than on Mac and Linux
* QTBUG-95927 QPrinter::setFullPage does not set margins to zero
* QTBUG-123059 "package android.location.altitude does not exist" when
building qtpositioning for Android on Linux
* QTBUG-122973 QDateTime::operator== documentation is wrong
* QTBUG-113432 RubberBand update area is too small in QListView
* QTBUG-122821 QListView with checkable items duplicates checkbox
* QTBUG-122825 QAbstractItemView::indicator not working properly
* QTBUG-102820 [REG 5.15.2 => 6.2.4] Styled indicators not drawn in
itemviews
* QTBUG-86407 Accelerators in QDockWidget titles are displayed
incorrectly in some styles
* QTBUG-122723 MySql and ODBC QSqlField.defaultValue() always get
invalid QVariant
* QTBUG-123083 tst_QProcess::setChildProcessModifier fails in dev
* QTBUG-118209 Several issues when aborting network request
* QTBUG-36127 Internal warning when aborting a QNetworkReply
* QTBUG-123186 "Target "tst_qsvgdevice" links to:
Qt6::QSvgIconPlugin_init but the target was not found" when building
qtsvg for iOS
* QTBUG-122181 Allow finding qtmultimedia mock plugin in manual tests
* QTBUG-123151 tst_QStorageInfo::caching is flaky on RHEL
* QTBUG-122729 tst_qwasmwindow_harness fails after fixing Env in CI
* QTBUG-122205 OpenXR feature breaks test builds
* QTBUG-123286 'load_local_libs' and 'bunlded_libs' libraries in
libs.xml are always prefixed with "lib"
* QTBUG-122996 Delegate definition should be in front of QGuiApplication
but doing so sometimes makes reflection delegate unusable
* QTBUG-118226 Rejected QMessageBox emits Accepted Signal
* QTBUG-122747 Reparenting QTabWidget with a native window tab can cause
crash
* QTBUG-123211 Metal backend:
QRhiTextureRenderTarget::PreserveColorContents doesn't work with render
buffers
* QTBUG-122838 Android multi-abi builds broken if depfiles are used
* QTBUG-122893 Sending QNetworkRequest fails on singlethreaded WASM
* QTBUG-119169 QFutureWatcher::resultReadyAt() signals sent in random
order
* QTBUG-122257 windeployqt --list option prints status messages
* QTBUG-123339 Critical QTextEngine regression in Qt 6.7.0 RC1.
* QTBUG-122664 windeployqt can not find qtpaths executable
* QTBUG-121500 Default flick deceleration is far too high for
touchscreens, can't be customized through platform theme
* QTBUG-35608 Flickable speed and deceleration does not scale with pixel
density
* QTBUG-35609 Flickable speed and deceleration are not easily
customisable
* QTBUG-52643 Dragging threshold on high DPI touch devices is too small
* QTBUG-97055 QQC2 Flickable scrolling is not linear with clicky wheels
on Qt 6.2.0
* QTBUG-123324 dSYM warning: skipping debug map object with duplicate
name and timestamp
* QTBUG-117410 The QQuickRenderControl Example renders a black cube
* QTBUG-115960 QSqlQuery (QPSQL) inserts QDateTime in UTC format but
retrives it as local timezone
* QTBUG-122304 Fix overflow warnings in tst_qnumeric
* QTBUG-122303 Fix truncation warnings in tst_qnumeric
* QTBUG-122588 AA_UseStyleSheetPropagationInWidgetStyles does not work
if parent widget is already shown
* QTBUG-122910 Hinting is bad with fractional scaling, Wayland and
hintfull
* QTBUG-116086 tst_qqmlbinding::restoreBindingWithoutCrash leaks memory
* QTBUG-122302 Fix truncation warning in generation_helpers
* QTBUG-123374 Linux on Arm fails with '-headersclean' in
global/qfloat16.h
* QTBUG-123401 Ambigious overload of operator<<(QDBusArgument &arg,
const Container<Key, T> &map) for QMap with nested pairs
* QTBUG-123486 qcontainertools_impl.h:383:14: error: ‘D.279326’ is used
uninitialized [-Werror=uninitialized]
* QTBUG-106709 Application looks too small on an external display with
iPadOS 16.1 on M1 iPad
* QTBUG-123032 [REG: 6.6.1->6.6.2] Override cursor changes together with
window creation and destruction crashes on KDE
* QTBUG-115039 AnimatedImage: setting sourceSize.width or height alone
doesn't work
* QTBUG-123410
QtInterfaceFramework/private/qifabstractfeature_p.h:20:10: fatal error:
private/qobject_p.h: No such file or directory
* QTBUG-122776 Qt for webassembly doesn't respect
Qt::WA_ShowWithoutActivating for QDialog
* QTBUG-120768 Non-Native Dialog opens file when attempting to open
invalid file
* QTBUG-123554 xcb: Enabling touch device while application is running
causes a crash on first touch
* QTBUG-123092 Explain the order and the logic of using various SSL
backends
* QTBUG-123588 Compiler warnings in generated code of user project
* QTBUG-123310 [Regression] Squish build failure with QMap/qHash
* QTBUG-123353 building androidnotifier example with qmake fails
* QTBUG-123722 QComboBox shown with black popup background
* QTBUG-122684 Inconsistent QPolygonF serialization
* QTBUG-122704 QPainterPath de-serialisation from QDataStream fails if
item isn't empty
* QTBUG-123334 QMessageBox wrong icons displayed on Android
* QTBUG-123875 QRestAccessManager include documentation is incorrect
* QTBUG-123937 Wrong preprocessor conditional in qspan.h
* QTBUG-123959 qApp crashes after being deleted when hosted as a plugin
and when focus application is changed
* QTBUG-123927 Three-way comparison operators in QJsonValueRef result in
ambiguities and break build
* QTBUG-123932 qstorageinfo_linux.cpp:15:10: fatal error: linux/mount.h:
No such file or directory
* QTBUG-80167 QOpenGLWidget no longer repaint if a paint-on-screen
widget is updated
* QTBUG-73386 Serializing Qt Data Types Documentation not up to date
* QTBUG-123798 tst_QComboBox::popupPositionAfterStyleChange() flaky on
QNX
* QTBUG-123326 Style Violation: warning: Qt-RuleOfThree: Class with move
assignment operator is missing move constructor. [QCollatorSortKey]
* QTBUG-123989 Building Qt for Android with examples fails with missing
QObject:connect() overload
* QTBUG-122135 uri manual test fail
* QTBUG-120276 Crash when reparent a native child to a different tlw if
QT_WIDGETS_RHI=1 is set on Windows
* QTBUG-123444 regression: ODBC connection strings no longer work with
QSqlDatabase::setDatabaseName()
* QTBUG-123478 regression:ODBC QSqlDatase::record() broken
* QTBUG-114243 Qt 6.5 regression with static cross-compiling for Windows
* QTBUG-111235 tst_QOpenGLWidget::reparentHidden() fails on Android 12
CI
* QTBUG-111236 tst_qvulkan cases fail Android 12 CI
* QTBUG-123848 Short cuts involving 2 (or more) modifier keys are not
longer handled by the Input Methods on macos.
* QTBUG-106516 Multi-modifier key events not correctly handled on macOS
* QTBUG-124164 QFileSystemModel delete takes 1s
* QTBUG-118985 The screen becomes blank after unlocking the screen in
the app with Vulkan content rendered under a Qt Quick scene
* QTBUG-118840 [Crash] Vulkan examples crash on Android when unlocking
the screen
* QTBUG-123791 Crash in qwindows11style with null widget
* QTBUG-124003 xcb: Mouse enter event is no longer delivered when mouse
leaves windows with pressed button
* QTBUG-123632 Regression: Setting background-color style of
QTreeView::item breaks alternatingRowColors
* QTBUG-124151 Layout Item Is Not Properly Deleted if Layout Is Disabled
* QTBUG-124254 Names can start with a non-letter char in Address Book
example
* QTBUG-103019 MinGW Qt6Platform.pc has an extra '>' after '-D_UNICODE'
* QTBUG-124186 syncqt is not found when building qt submodules using
cmake >= 3.29
* QTBUG-123162 macOS: QMdiSubWindow title bar gradient stands out too
much in dark mode
* QTBUG-122180 When changing the stylesheet for a selected, checked
QHeaderView section then it disregards the font weight setting
* QTBUG-124191 [REG: 6.6->6.7] QComboBox custom view is destroyed if
style changes
* QTBUG-92855 Dock widgets' title bars on macOS dark mode do not fit in
* QTBUG-97645 QWindowsFontEngineDirectWrite ignores QFont::NoAntialias
flag
* QTBUG-118887 Screen.orientation broken on android 14
* QTBUG-118236 Declarative Camera Example orientation errors on Android
13 / Android 14
* QTBUG-93413 uic and overloaded slots
* QTBUG-122208 Randomly getting "Access is denied" errorwhen saving
files with QSaveFile.
* QTBUG-123054 Reg[5->6] QSvgRenderer generated images are not identical
* QTBUG-124085 Incorrect icon used for "document-properties" on Windows
* QTBUG-113492 META + Tab and CTRL + Tab shortcuts do not function on
macOS
* QTBUG-8596 Mac cocoa only: QKeyEvent Qt::Key_Tab not accessible to
event or eventFilter
* QTBUG-124267 QTableView's corner button documentation is inconsistent
with its implementation
* QTBUG-92007 [REG: 5.13->5.14] QLibrary is now automatically calling
JNI_OnLoad of loaded library
* QTBUG-124349 Duplicate data tags in tst_QVariant::compareNumerics()
* QTBUG-67807 QOpenGLFunctions_4_5_Core has wrong prototypes for
*NamedBuffer* functions
* QTBUG-121046 Some dependencies are always considered not up to date.
* QTBUG-123962 [regression] QMenu crashes on eglfs
* QTBUG-124343 QMenu documentation points to deprecated
QMouseEvent::globalPos()
* QTBUG-87219 MOC's preprocessing is not conformant
* QTBUG-124288 Moc compile error when using enums
* QTBUG-124301 QTableView resize causes infinite loop if signal is
connected before model is set
* QTBUG-101143 QML_FOREIGN refering to a class in another library leaves
the type empty in qmltypes file
* QTBUG-99051 qt_add_library should generate metatypes.json files by
default
* QTBUG-121199 QML_FOREIGN of objects in an inheritance tree does not
work with qmllint
* QTBUG-123102 [hiDPI] QSystemTrayIcon wrong context menu position
* QTBUG-121722 headersclean does not pass the /utf-8 compiler flag by
default for MSVC
* QTBUG-120331 rendering svg causes int overflows in
blend_vertical_gradient_argb
* QTBUG-123167 QTextBrowser.toHtml is not rendering supported CSS border
property for html table tag.
* QTBUG-124366 wasm: keyboard input on linux touchscreen device not
working
* QTBUG-122740 Android Embedded QML View: App crashes when selecting
text
* QTBUG-123839 useless file accesses in qt_findAtNxFile() originating
from QStyleSheetStyle::loadPixmap()
* QTBUG-122241 QXmlStreamWriter::writeCharacters fails to write UTF-8
encoded QAnyStringView
* QTBUG-124221 [Doc] QStringConverter lacks ICU support information
* QTBUG-124117 Compiling code based on Qt 6.7.0 with MSVC compiler vc16
(14.29.30133) causes compile error "unreachable code"
* QTBUG-116197 org.freedesktop.appearance.color-scheme is supported in a
weird way
* QTBUG-2188 QTextDocument: Bullets in bullet lists are not affected by
text color
* QTBUG-213 Error in drawing of bullets in QTextDocument
* QTBUG-57833 QTextEdit list number/bullets inherit the following text
style
* QTBUG-123872 time wrongly displayed in zh_TW locale
* QTBUG-123579 QLocale::toDatetime does not always work when it should?
* QTBUG-124160 [Reg] NSSearchField no longer visible after hide/show
QDialog
* QTBUG-43745 Qt5 still ignores fontconfig on some Linux desktops
* QTBUG-124512 QProcess::startCommand crash if empty string is passed
* QTBUG-123891 HTTP2: finished and errorOccurred signals never emitted
when auth fails with code 401
* QTBUG-118581 QString multi-arg wrong behaviors: percent(%) eats all
numbers
* QTBUG-121653 License clarification for unicode & unicode-cldr related
files
* QTBUG-113404 Wayland: Gestures are not delivered to correct top level
widget
* QTBUG-124554 QPushButton menu dropdown arrow looks odd on 100% DPI at
HD (1920x1080) resolution
* QTBUG-114539 QToolButton arrow clipped on screen with non-integer
device pixel ratio
* QTBUG-124580 QMimeData::setData("text/uri-list",…) loses last url
* QTBUG-99106 QMouseEvent always generates Qt::LeftButton events on
Android, even on right mouse click
* QTBUG-124538 ~QGuiGLThreadContext leaks memory
* PYSIDE-2492 uic does not generate enumeration name into enum values
causing type checking warnings
* QTBUG-123035 QDataStream docs give wrong examples
* QTBUG-124227 Reg[6.5.4->6.5.5] looks like Gif Frame duration is
changed
* QTBUG-122436 Android a11y: Changes to Accessible.ignored and
Item.visible are not propagated to the screen reader
* QTBUG-124642 qtbase/src/corelib/io/qprocess_unix.cpp:860:31: error:
'TIOCNOTTY' was not declared in this scope
* QTBUG-123928 Not all widgets follow mode switching at runtime in the
Widget Gallery example
* QTBUG-124551 [macOS] App crashes on quit if the Quick Platform menu is
open
* QTBUG-117091 Crash during updateApplicationBadge
* QTBUG-124719 windeployqt picks some host arch dlls
* QTBUG-124376 Slow UI build in Release mode with MSVC
* QTBUG-66605 QSaveFile::fileTime() fails after QSaveFile::commit()
* QTBUG-77039 QSaveFile::size() reports 0 after writing a file
* QTBUG-124666 Performance regression after "Abstract QWidget focus
chain management"
* QTBUG-123919 Inconsistent api in QStringEncoder vs QStringConverter
* QTBUG-124386 [Regression] QEventLoopLocker causes application to quit
even with open windows
* QTBUG-122166 Qt Test tutorials missing a link to the source code
* QTBUG-124447 Doing style->drawControl(QStyle::CE_ProgressBar) inside
QStyledItemDelegate causes a crash
* QTBUG-124863 It's not possible to have the reversed unordered model in
QSortFilterProxyModel
* QTBUG-124475 tst_QWidget::tabOrderWithProxyDisabled() crash on
Wayland(GNOME, Ubuntu 22.04)
* QTBUG-124286 New native style for Windows 11 ignores stylesheet in
some cases
* QTBUG-124861 HistoryCompleter popup stays on top when changing mode
* QTBUG-124908 QtView does not destroy the foreign parent window it is
wrapped by
* QTBUG-115583 Redundant declaration of QPageSize equality operator
* QTBUG-124262 [Reg] Crash when calling QMainWindow:.tabifiedDockWidgets
after QMainWindow::removeDockWidget
* QTBUG-124869 qtconfigmacros.h is missing an include
* QTBUG-124608 QResource file engine returns read-only memory for some
resources even with MapPrivateOption
* QTBUG-123939 tst_qdialogbuttonbox non-deterministic failure
* QTBUG-125089 crash: notepad example from qtbase on ios
* QTBUG-112721 QLineEdit standard menu actions do not have object names
* QTBUG-124135 qtbase/cmake produced pkg-config .pc files no longer emit
dependencies
* QTBUG-110369 AUTOUIC can't handle relative paths referring to parent
dirs with Ninja Multi-Config
* QTBUG-124783 QCoreApplication::removeNativeEventFilter does not use
MainThread eventDispatcher
* QTBUG-109512 Documentation of QThread::setStackSize() wrong (on Unix)
* QTBUG-117996 [REG 6.2 -> 6.5] QBasicTimer::stop: Failed. Possibly
trying to stop from a different thread
* QTBUG-125079 removed_api.cpp compile error
* QTBUG-111988 qtdiag cannot be executed in static builds
* QTBUG-125142 [REG 6.7.0->6.7.1] Can't deploy to iOS/iOS simulator:
ASSERT: "m_view.window" in file qioswindow.mm
* QTBUG-124931 Wrong aligenment for right to left languages in the main
menu with Windows 11
* QTBUG-124111 Fix QNetworkReply on WASM
* QTBUG-124919 QDBusSignature considers an empty string to be an invalid
signature
* QTBUG-96120 zstd both found and not found
* QTBUG-96394 Misleading cmake output about missing optional packages
* QTBUG-111216 CMake configuration summary is wrong about "wrapped" zstd
(and others)
* QTBUG-125154 Left-clicking in QSlider in modern Windows 11 style uses
old Windows XP/Vista slider stepping behavior
* QTBUG-125058 QtTest log QCRITICAL due to QApplication::regClass:
Registering window class 'Qt662dScreenChangeObserverWindow' failed.
(Class already exists.)
* QTBUG-125241 fromIccProfile fails with "failed minimal tag size
sanity"
* QTBUG-114938 2dpainting example crashes on QNX
* QTBUG-115462 QT_WIDGETS_HIGHDPI_DOWNSCALE is broken on Wayland
* QTBUG-123998 Top flaky test: tst_qwidget::hoverPosition on
openSUSE_15_5 X86_64, Ubuntu_22_04, QNX_710
* QTBUG-124197 a11y: Report QAccessible::Help as HelpText AT-SPI
property
* QTBUG-125506 [Reg 6.7.0->6.7.1] Build break with -no-feature-mdiarea
* QTBUG-73655 QTableView Not Rendering Icons Correctly
* QTBUG-125285 QKdeTheme falls back to Qt::ColorScheme::Unknown on
invalid desktop theme
* QTBUG-124524 QMenuBar with style override submenu all white in dark
mode and crash
* QTBUG-125472 [Reg 5.15->6.x] QVariant::isNull() can return true for
non-null values
* QTBUG-124192 a11y: Missing NameChanged event for updated window title
* QTBUG-125257 CLONE - [REG 6.7.1->6.8] QTabWidget: Tab focus does not
work for children
* QTBUG-119057 a11y: Qt lacks possibility to set many a11y
attributes/properties
* QTBUG-125222 isAutoRepeat not working for WASAM
* QTBUG-123838 QFile::moveToTrash() description incorrect
* QTBUG-125467 QIBASE can't connect to pre-Firebird 4 database
* QTBUG-86203 Documentation on QtAndroid:androidService(),
QtAndroid:androidContext() unclear
* QTBUG-125627 code_injection.mojom-shared.h:332:5: error: there are no
arguments to ‘CHECK’ that depend on a template parameter,
* QTBUG-125610 Constructing a QDate from std::chrono::year_month_day
results in link error
* QTBUG-120415 Unable to close Window when changing hide taskbar toggle
* QTBUG-122456 Support of NFC for Services when QtNative.onNewIntent()
is private
* QTBUG-125306 Wrong alpha on format convertioncolor space transform
* QTBUG-122394 Crash when using QDockWidget
* QTBUG-85227 Qt's deprecation warnings are not on by default for MSVC
* QTBUG-125531 Unable to drag files into the xwayland widget of
QTextEdit
* QTBUG-102347 Qt documentation doesn't specify log level severity order
* QTBUG-125735 [REG 6.4→6.5] QAnyStringView(char-ish) has become slow
* QTBUG-124235 Too small minimumSizeHint for QDateEdit/QDateTimeEdit
with windows11-style
* QTBUG-124150 QAbstractSpinBox size hint miscalculated for Windows 11
style
* QTBUG-125776 The Q_OBJECT macro documentation mentions obsolete
requirements
* QTBUG-124342 Gap at edge of windows using fractional scaling
* QTBUG-125889 tst_qfloat16::ordering - conversion of floating to
integral exercise undefined behaviour
* QTBUG-125623 DBusConnection name clash
* QTBUG-125302 QColorSpace::iccProfile asserts
* QTBUG-125585 Line spacing of many fonts is dramatically different
between Qt5 and Qt6
* QTBUG-119221 The mainwindow will be recreated when add a
QWebEngineView to it
* QTBUG-121181 Main window blinks when adding QWebEngineView into a
layout
* QTBUG-120096 Rendering seems interupted when switching webengine view
to QWidget
* QTBUG-115652 Child quick widget fails to draw if it's child of raster
native widget
* QTBUG-108344 Something is rotten with texture-based widgets that are
native child widgets or are children of a native child widget
* QTBUG-113557 Raster native widget fail to draw when there is a quick
widget sibling
* QTBUG-107198 QML element resize cause flicker on MacOS
* QTBUG-114439 No such signal
QPlatformNativeInterface::systemTrayWindowChanged(QScreen*) on Wayland
* QTBUG-94871 Qt should subscribe to dbus system tray and dbus menu
service appearing/disappearing
* QTBUG-125721 QStorageInfo::mountedDrives() not reporting mounted btrfs
subvolumes on same device as root
* QTBUG-125303 QColorTransform asserts
* QTBUG-125120 wasm: qtvirtualkeyboard crashes on startup
* QTBUG-125381 wasm: microphone permissions on firefox dont work
* QTBUG-125958 Numpad 5 is not mapped to Qt::Key_Clear
* QTBUG-125436 Windows ARM: HealthCheck fails - QtBase tst_QProcess
* QTBUG-125380 Windows command line arguments mangled by double prime
character
* QTBUG-126012 [patch] bindTextureImage: clearing GL error: 0x500
* QTBUG-125513 crash when mixing QWidget style and styleSheet
* QTBUG-125858 REG: Wrong result value in QMessageBox::warning detected
in version 6.7.1
* QTBUG-126056 Camelcase forwarding headers missing in macOS/iOS builds
* QTBUG-126084 QDockWidget unplugged from floating tab is in the wrong
position
* QTBUG-125479 iOS - The cached device pixel ratio value was stale on
window expose
* QTBUG-126107 tst_QStingConverter::invalidConverter() triggers valgrind
* QTBUG-126052 submenu overlaps in qWdiget on iOS
* QTBUG-126044 QMenu: Submenu partially hidden by main menu
* QTBUG-126122 [Reg 6.6 -> 6.7] Window resizing on Android is broken
* QTBUG-125993 Double tap on touch screen not provoking
mouseDoubleClickEvent - patch included
* QTBUG-126115 tst_qdbuscpp2xml doesn't appear to list qdbuscpp2xml as a
dependency
* QTBUG-125410 TextField.inputMethodHints flags are ignored on Android
for Qt 6.7.0
* QTBUG-126144 "configure -system-libb2" does not error if libb2 is
unavailable
* QTBUG-124786 [Android] NullPointerException at
QtActivityDelegate.java:83
* QTBUG-59621 QIcon has increased memory usage because pixmaps are not
loaded on demand
* QTBUG-126221 B2Qt Application crashes
* QTBUG-126265 uic: Code Injection to Potential Code Execution
* QTBUG-125015 [REG] configure -c++std c++17 no longer works
* QTBUG-121586 [Reg 5.15->6.x] QActionGroup signals missing from
documentation
* QTBUG-126374 ABI break in 6.8 beta 1:
QPageLayout::setBottomMargin(double)
* QTBUG-126386 qcompare.h build error on MSVC
* QTBUG-126343 QBitArray::count breaks after bitwise opererations
* QTBUG-124829 The appearance of icons in QFileSystemModel is simplified
and differs from the typical Windows icons.
* QTBUG-123018 Crash on closing an ios application
* QTBUG-119076 Selecting multiple rows is sluggish if there are column
spans
* QTBUG-126394 [Regression] Decreased performance in timerEvent
* QTBUG-123886 [REG 6.5.2->6.5.3] QAbstractScrollArea::sizeHint does not
include the horizontal scrollbar's size
* QTBUG-23470 QLibrary does not add 'lib' prefix if file name starts
with 'lib' (unix)
* QTBUG-123298 Qt 6.5 on MacOS - In full screen, topmost QMenu action
doesn't fire
* QTBUG-39403 QDesktopWidget::availableGeometry() returns wrong values
in Mac fullscreen mode
* QTBUG-126349 Windows ARM: HealthCheck fails - QtBase tst_QFuture
* QTBUG-124898 [Reg 6.2 -> 6.5] Qt.uiLanguage does not work for locale
changes
* QTBUG-126303 QWidget::createWindowContainer() managed window deleted
when new widget added due to QRhi
* QTBUG-126381 qcssparser.cpp ASSERT: "d->parsed.metaType() ==
QMetaType::fromType<QList<QVariant>>()"
* QTBUG-126214 QtCore: implicit instantiation of undefined template
'std::char_traits<unsigned char>' (libc++ 19 / musl libc / amd64)
* QTBUG-122753 Qt Multimedia: implicit instantiation of undefined
template 'std::char_traits<unsigned char>' (libc++ 19 / musl libc /
amd64)
* QTBUG-124573 Windows Icon Engine: QIcon::pixmap() scales size by
devicePixelRatio twice, not once
* QTBUG-126388 [REG 6.8.0 -> 6.9.0] QTableView: Icons are incorrectly
scaled
* QTBUG-122778 QTreeView stylesheet does apply the border and the
background color to the branches
* QTBUG-124481 KDE theme plugin always assumes single click activation
on KDE Plasma 6
* QTBUG-126594 6.7.2 qtbase: missing cups dependency in
Qt6PrintSupport.pc and Qt6PrintSupport cmake modules
* QTBUG-126621 moveToTrash fails to remove a symlink to a directory
after trashing
* QTBUG-56590 macdeployqt copying dSYM bundles
* QTBUG-89484 macdeployqt not deploying QSerialBus (canbus) plugins
* QTBUG-126502 Link broken on Qt Test Overview page in docs.qt.io
* QTBUG-126678 CMake flag QT_USE_TARGET_ANDROID_BUILD_DIR does not work
with QT_ANDROID_BUILD_ALL_ABIS
* QTBUG-33786 Orca reads model columns instead of rows when navigating
through items in QListView
* QTBUG-125504 QDirListing includes '.' and '..'
* QTBUG-27205 QFileSystemModel::filename() uses wrong role value for
call to data() method
* QTBUG-126659 New QMap.qHash leading to ambiguous calls
* QTBUG-126348 QToolButton widgets have wrong background colors with
windows11 style and dark themes
* QTBUG-126530 Qt app memory keeps growing with accessibility enabled
* QTBUG-126596 QListWidgetItem::setForeground() does not work
* QTBUG-126543 windows11 style has QTableView ignoring
Qt::ForegroundRole
* QTBUG-63485 Documentation for QStringList::replaceInStrings
* QTBUG-68465 macOS: Accessibility: MenuItems are not accessible
* QTBUG-126456 QWidgetWindow: Use of object after destruction
* QTBUG-126043 macOS: Double clicking an appliaction in finder opens it
without the window becoming active
* QTBUG-122755 Dragging text on HighDPI screen results in a warning
"QPixmap::scaled: Pixmap is a null pixmap"
* QTBUG-123449 [Reg 6.4->6.5] Quick MenuItems do not appear greyed out
when disabled under GTK
* QTBUG-126503 No graphic change on Hover for QPushButton and
QToolbutton
* QTBUG-125781 Cannot distinguish disabled or hovered buttons on Windows
11
* QTBUG-126622 [iOS] Screen Reader focus gets stuck
* QTBUG-126775 windeployqt does not provide MinGW's libraries
* QTBUG-62970 tst_QComboBox::autoCompletionCaseSensitivity is flaky on
openSUSE 42.3
* QTBUG-126773 iOS - library not found for -llibavformat
* QTBUG-126575 QImage / QImageReader: lost QColorSpace during rotation
* QTBUG-107139 Webassembly cannot input Chinese
* QTBUG-124932 Incorrect keyboard functionality in a QML 3D scene on the
WebAssembly platform.
* QTBUG-117096 Input fields (QWidgets and QML) don't register dead keys
accents when using a Linux desktop
* QTBUG-126822 Windows accessibility crash/assert in Gallery example
* QTBUG-126721 [REG 6.6->6.7] Overriden setVisible() no longer gets
called when parent widget is shown
* QTBUG-126218 Preview is not generated when QPrintPreviewWidget is
shown
* QTBUG-126872 Double dash configure options with an equal sign broken
* QTBUG-126391 tst_QDateTime::timeZones() fail on macOS 15
* QTBUG-126390 ASSERT: "sameLocale(locale.d->m_data, monthly)"
* QTBUG-127044 qmake reports wrong mkspec on Windows Arm64
* QTBUG-127008 QThread::terminate() vs. normal exit race
* QTBUG-112287 android: Input does not work with QQuickWidget
* QTBUG-124564 Windows 11: Alternating row colors doesn't work in
windows11 style
* QTBUG-89204 qtimageformats fails to configure during a static Windows
build with target global promotion failures
* QTBUG-94356 fail to configure qt 6.1.1 on macos (with conan) due to
ZLIB global promotion not happening
* QTBUG-95052 qtimageformats global promotion issues in static builds.
* QTBUG-98807 build failure (with conan)when odbc and vulkan are enabled
(due to global promotion)
* QTBUG-125371 Problematic calling of qt_find_package(Qt6) in
qt_internal_project_setup
* QTBUG-52292 Pantheon desktop is not recognized as Gtk desktop
* QTBUG-126533 Expand/collaps icon in QTreeView is not correctly scaled
when multi monitors have different scale settings
* QTBUG-127168 Memory Leak: Windows: Result of SetupDiGetClassDevs() is
not freed
* QTBUG-126479 show()+showMaximized()+activating a layout de-maximizes
the window
* QTBUG-104201 QWidget: resize() after showMaximized() causes strange
behaviour
* QTBUG-127055 QThread::terminate() ABA problem
* QTBUG-125589 weired console message with simple application
* QTBUG-126435 Document QT_NO_UTF8_SOURCE
* QTBUG-127129 Default column value misses database name in WHERE
* QTBUG-127175 ibase driver returns stale error condition
* QTBUG-127112 QProgressBar with Windows 11 style is using far too much
cpu
* QTBUG-126845 QOpenGLWindow use after destruct
* QTBUG-126151 QJniArray should not require contiguous containers as
input or output
* QTBUG-124561 Qt.labs.platform context Menu appears out of the app
window on Gnome/wayland
* QTBUG-126598 Qt.labs.platform Menu broken content positioning on linux
* QTBUG-127152 Document QDirListing::DirEntry
* QTBUG-60674 QSqlRelationalTableModel - relation refresh crash
* QTBUG-126541 Qt FTBFS on clang when C++20 is enabled
* QTBUG-127414 Random configure/build error for android multiabi
* QTBUG-127510 SCARY QDebug::toString() terrifies tests that compare
Microsoft::WRL::ComPtr
* QTBUG-127507 "trivial-auto-var-init=pattern" causes crashes when using
MinGW
* QTBUG-127473 [REG 5.15 -> 6] QList::op==() is broken for FP types
* QTBUG-126820 Move all QKeyCombination-returning operators into the
namespace Qt
* QTBUG-125778 QMdiSubWindow does not refresh when the Maximize button
is hidden after being created.
* QTBUG-125496 Apps continue running in the background.
* QTBUG-127668 A standalone test can't be configure with a cross-
compiled Qt
* QTBUG-120396 `QUrl::resolved` gives wrong result when there are more
`..`s in relative reference
* QTBUG-127614 [macOS] [labs.platform] Menu stuck on opening when
standard icons are used
* QTBUG-127551 [win] [labs.platform] Standard menu icons looks wrong on
DPR > 1
* QTBUG-127342 OCI plugin does not build for ARM
* QTBUG-127512 tst_QTextLayout::softHyphens(16) failed on Ubuntu
24.04(both x64 and arm64) GNOME
* QTBUG-126350 Windows ARM: HealthCheck fails - QtBase module_includes
* QTBUG-126351 Windows ARM: HealthCheck fails - QtBase test_opengl_lib
* QTBUG-127114 QPainter::drawText(QRectF, QString) has inconsistent
behavior when QRectF is null
* QTBUG-127641 QComboBox popup position changes after widget reparenting
* QTBUG-125149 Misplaced popup menu for reparented combo box
* QTBUG-127672 Consecutive stars in wildcardToRegularExpression cause
regex catastrophic backtracking
* QTBUG-127799 repc: /home/qt/work/qt/qtremoteobjects_standalone_tests/t
ests/auto/pods/rep_pods_replica.h: No such file.
* QTBUG-126415 Unknown CMake command "qt_internal_add_test" while trying
to open permissions manual test and selecting configuration
* QTBUG-127392 Avoid warning: Ignoring window icon xxx exceeds maximum
xcb request length 65535
* QTBUG-127646 Windows ARM: HealthCheck fails - QtBase tst_qcolorspace
* QTBUG-127403 Typo in QRhiTextureRenderTargetDescription
* QTBUG-127857 -skip-tests and -skip-examples are case sensitive
* QTBUG-116083 Build failure related to fontdatabase / fontconfig
* QTBUG-127759 Qt::partial_ordering::unordered implements op!=()
incorrectly
* QTBUG-119753 QSqlRecord access causes hang/memory leak and crash using
QODBC driver
* QTBUG-122774 "--no-qmltoolingsettingsInternal" gives error 'Unknown
option 'no-qmltoolingsettingsInternal''
* QTBUG-124310 QT_DISTANCEFIELD_DEFAULT_BASEFONTSIZE=128 causes a
QDistanceField crash
* QTBUG-127981 [cmake] stenciloutline name clash
* QTBUG-121724 Image scaling produces an artifact around translucent
areas
* QTBUG-126572 Default qt_generate_deploy_qml_app_script does not deploy
QtWebEngineProcess(d).exe to where it should be
* QTBUG-127732 QT_WIN_DEBUG_CONSOLE breaks windeployqt in CMake install
* QTBUG-119901 Basic <type_traits> not working for q*int128 in QtCore
TUs
* QTBUG-127552 a11y: QFrame reports incorrect top-level role on Linux
(AT-SPI2)
* QTBUG-127296 The return values of QMimeData::hasFormat() and
QMimeData::data() are inconsistent with the documentation.
* QTBUG-124570 Font is rendered differently in html and in ODT
* QTBUG-126013 heap-use-after-free in from
QtPrivate::watchContinuationImpl
* QTBUG-127880 Race condition in QFuture implementation
* QTBUG-128102 Hash constructor with iterators does not work with
ranges::views
* QTBUG-127549 [6.5->6.7 regression] QString::replace() takes huge
amount of time. 10x worse performance
* QTBUG-128199 [Reg 6.7.2->6.8.0b3] QByteArray::lastIndexOf fails to
find char
* QTBUG-128137 qt-configure-module does not consider choosen
INSTALL_LIBEXECDIR
* QTBUG-127288 Windows: MDI subwindow icons have low resolution and an
unattractive appearance when the window is displayed in maximized mode.
* QTBUG-127926 Outdated Android docs still refer to
QtAndroid::androidActivity()
* QTBUG-127381 Unexpected shift-selection in QTreeView.
* QTBUG-128205 Qt documentation's offline.css defines weird background
for the print media type
* QTBUG-124162 Qt Assistant Print Preview is not working
* QTBUG-128254 Cannot build signed AAB with verbose deployment
* QTBUG-109619 Enabling 2 extra Android CMake options leads to a build
error
* QTBUG-122967 [macOS]Calling winId() renders additional undesired
pixmap if scaling factor is not 1
* QTBUG-122751 Top flaky test: tst_qaccessibilitymac::treeViewTest on
MacOS_14 ARM64, MacOS_13, MacOS_12
* QTBUG-117417 Regression 5.15: Sharing Files w FileProvider fails
* QTBUG-123752 Unexpected offset of fixed-height top-level window when
Windows Taskbar is on top
* QTBUG-128298 QT_ANDROID_DEBUGGER_MAIN_THREAD_SLEEP_MS doesn't work
* QTBUG-128290 QT_THREAD_PARALLEL_FILLS macro causes semaphore_wait_trap
on iOS
* QTBUG-125975QT_DISABLE_DEPRECATED_UP_TO 0x060400 gives link error
with static build
* QTBUG-127723 tst_QSvgRenderer::testFeFlood() failed on Ubuntu 24.04
X11 and offscreen
* QTBUG-126752 Calling popup() on QCompleter causes an abnormal behavior
of the Qt virtual keyboard.
* QTBUG-124733 Tool bar loose focus over mouse hovering
* QTBUG-127670 Conversions from Qt::<name>_ ordering type to the weaker
std types are missing
* QTBUG-121322 Cannot cross compile Qt for arm64 macOS on x86_64 macOS
* QTBUG-110841[REG: 5.10.1->5.11.0-alpha] Mouse events not observed
when Super (Windows) key is held down.
* QTBUG-128325 tst_qbytearrayview test gives deprecated warnings at
compilation
* QTBUG-124465 QDate::fromString very slow in 6.7.0
* QTBUG-128337 configure does not properly parse sql options
* QTBUG-94956 "Invalid revision: zipalign" when building for android
* QTBUG-127788 QSlider's ticks are blurry when using Windows 11 style
* QTBUG-124118 QColorDialog on Windows 11: layout is broken
* QTBUG-127924 QFileDialog::selectNameFilter() does not work with the
filter returned by QFileDialog::selectedtNameFilter() of a previous
dialog
* QTBUG-127987 Error copying directory: .syncqt_staging
* QTBUG-127536 When styling a QComboBox, it always has a check-box icon
even after setting the icon to none.
* QTBUG-128391 QWidget inside a QMenu using QWidgetAction does not
always receive enterEvent and leaveEvent
* QTBUG-84297 QTimeZone::NameType doesn't work as documentated
* QTBUG-125239 ERROR: AddressSanitizer: heap-use-after-free WRITE of
size 1 in tst_QGuiApplication::modalWindow()
* QTBUG-128144 Complete addition of Qt::TimerId
* QTBUG-128390 Crash on QWindowPrivate::updateDevicePixelRatio() with
nullptr access
* QTBUG-128516 [macOS] Sporadic crash on
QCocoaScreen::deliverUpdateRequests()
* QTBUG-123551 [Boot2Qt] A windows is blacked out in QQuickWidget
Example application
* QTBUG-128548 atal error: QRhiTexture: No such file or directory
* QTBUG-128586 Signals without arguments give false warnings in QML in
Android
* QTBUG-128678 Reintroduce support of iOS 16
* QTBUG-128470 QHash heterogeneous lookup depends on C++20 concepts
* QTBUG-118794 "The cached device pixel ratio value was stale on window
expose" when opening context menu on macOS with external display
* QTBUG-128667 qdrawhelper crash rendering with ARM NEON
* QTBUG-128675 q(u)int128 isn't supported with clang using MSVC's STL
* QTBUG-128434 Master Details- Album added in the list is not displayed.
* QTBUG-128648 Update Android Gradle plugin to 8.6.0
* QTBUG-127711 QUrl.adjusted doesn't work with QUrl::RemoveFilename |
QUrl::NormalizePathSegments
* QTBUG-121855 missing RHI related headers (class documentation is
wrong)
* QTBUG-125994 All RHI class documentations shows Qt6::Gui as the link
target for CMake
* QTBUG-128940 FAIL!:
qmltestrunner::AnimatedImage::test_imageSource(local not found) Not all
expected messages were received
* QTBUG-116763 out-of-bounds operator+
* QTBUG-90634 QIcon not preferring Hi DPI pixmaps when scaling
* QTBUG-106479 androidtestrunner does not honour QTEST_FUNCTION_TIMEOUT
* QTBUG-101141 moc: namespaced base class not properly resolved in
cpp.json file
* QTBUG-82434 Incorrect Appearance QCursor with AA_EnableHighDpiScaling
* QTBUG-119998 CMake errors out with recursion in latest dev when using
qt-cmake-standalone-test on in-source auto test
* QTBUG-111443 macOS/iOS: "Detected system locale encoding (US-ASCII,
locale "C") is not UTF-8"
* QTBUG-119918 Possible/likely data race in QObjectData bit-field access
* QTBUG-119077 CMake deployment API does not deploy Qt Webengine
* QTBUG-119359 tst_QGuiEventLoop::processEvents is flaky on QNX
* QTBUG-117739 Fix qdoc can't link to warnings to removed or renamed
Examples
* QTBUG-118225 QtQuick Loader doesn't load over http(s)
* QTBUG-116577 ASSERT: "sumFactors > 0.0"in qgridlayoutengine.cpp
* QTBUG-120196 Maximized frameless window painting wrong view region
with Qt::FramelessWindowHint and Windows api WS_THICKFRAME
* QTBUG-119321 FAIL!: tst_QSharedMemory::useTooMuchMemory(POSIX) in
Debian - Linux on ARM
* QTBUG-115125 QObject::connect warns, but also fails to connect to
lambdas with Qt::UniqueConnection
* QTBUG-106907 "package" attribute in AndroidManifest is deprecated
* QTBUG-99750 cannot activate file system watcher in QFileSystemModel
* QTBUG-109877 macOS: QFileDialog::getSaveFileName() truncates a
compound extension
* QTBUG-120078 QOpenGLCompositorBackingStore::resize crashes due to null
context
* QTBUG-120334 tst_qshortcut_kernel in gui failed on Wayland
* QTBUG-114583 Headers use things in <iterator> without including it
* QTBUG-120460 tst_QHostInfo::reverseLookup() fails on qemu and blocks
CI
* QTBUG-119601 iOS: Sometimes soft keyboard can't be closed
* QTBUG-118829 androiddeployqt with --release includes various
qmltooling libs
* QTBUG-117443 Two Android executables mix their build artifacts if
targets are added in a single CMakeLists.txt
* QTBUG-119915 QIcon::availableSizes() return duplicates
* QTBUG-117910 [windeployqt] The QtPDF module will always be deployed if
it's installed
* QTBUG-118619 Poor QTest::addRow() and QTest::newRow() performance in
Qt >= 6.5.0
* QTBUG-113498 QVideoWidget in QDialog does not show / crashes (macOS)
when shown twice
* QTBUG-120191 Unable to restore visibility state of the QDockWidget
* QTBUG-96879 QGraphicsView::setTransformationAnchor(AnchorUnderMouse)
drifts when zooming with trackpad
* QTBUG-121348 Cannot run syncqt with Threadsanitizer
* QTBUG-119216 macOS: REG->6.5: DnD with custom text MIME type got
broken/crashes
* QTBUG-121457 Amend qt_internal_add_docs to accept INDEX_DIRECTORIES
argument
* QTBUG-120682 Creating QSslSocket when schannel is in use takes too
long time
* QTBUG-120602 Cannot build Qt modules standalone for iOS
* QTBUG-115158 Time zone names and abbreviations are not localised
* QTBUG-119490 qcocoaapplicationdelegate.mm:354:20: error: cannot
initialize return object of type 'BOOL'
* QTBUG-52021 Blink timer for QLineEdit not killed after QMenu spawn
* QTBUG-103484 rich text gets converted to monospace in CI because
QFontDatabase::GeneralFont is "Sans Serif" and is monospace
* QTBUG-122042 Shortcut icons for the delete and backspace keys seem to
be wrong
* QDS-11733 Delete icon points in wrong direction on macOS
* QTBUG-118834 QStringConverter/Win might throw away some valid
characters when restoring state during decode
* QTBUG-116077 Inconsistent hashing between different FP types
* QTBUG-120529 configure feature calculation is needlessly complicated
* QTBUG-104997 markdown writer doesn't correctly write blockquotes
containing lists
* QTBUG-118318 QStringConverter/Win doesn't handle resumption for
encodings with more than 2 octets per character for convertToUnicode
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
* QTBUG-118139 Fix keyboard input not working for child windows
* QTBUG-122596 [REG 6.7.0->6.8.0] error in configure step, top level
build, MinGW
* QTBUG-121495 COM is uninitialized too many times with FFmpeg and
QWindowsResampler
* QTBUG-122693 tst_QApplication::abortQuitOnShow fails frequently on
Android
* QTBUG-122137 REG: QtWebEngine / Pdfwidgets no longer supports plugins
* QTBUG-109708 Startup crash in QRhiD3D11::endFrame() with nullptr
access
* QTBUG-31283 QByteArray::clear() should not free the reserved memory.
* QTBUG-105009 [REG 5.15.2->6.3.1/6.4.0 Beta2] You can still insert
Chinese text into a QTextEdit when "readOnly" property is enabled.
* QTBUG-110838 edit components ReadOnly invalid via some input method
* QTBUG-119182 Readonly QLineEdit writable using input method
* QTBUG-122827 Android: Accessibility not working
* QTBUG-122420 meta-qt6 incorrectly packages x86_64 qmake on aarch64
cross-compile target
* QTBUG-122980 [REG -> dev] Unity Build broken
* QTBUG-122235 The image gestures app crashes when opening image file on
Android
* QTBUG-121583 Windeployqt does not take into account all dependencies
and exits with failure due to missing platform plugin
* QTBUG-108175 [macOS] Qt warning: "macOS generated a color-profile Qt
couldn't parse. This shouldn't happen."
* QTBUG-123115 Finalize 6.7 API review of QCborStreamReader
* QTBUG-115166 qt_add_qml_module() causes non-Ninja generators to think
that projects are never up-to-date
* QTBUG-123130 QDoc with Clang 18 drops `noexcept` specifier from
compiler generated methods documented with \fn
* QTBUG-122712 QMessageBox: setTextFormat() won't apply to informative
text
* QTBUG-110502 Qt fills in private use unicode if a font is found using
it
* QTBUG-123357 Some properties not included in QTextDocument::toHtml()
* QTBUG-117948 qt_generate_deploy_qml_app_script() deploys QML plugin
target but not the corresponding backing target
* QTBUG-100336 QObject::connect using loadRelaxed to synchronize non-
atomic writes
* QTBUG-123229 Q_OBJECT in multi-line(?) C comment triggers automoc (but
not qmake)
* QTBUG-123438 syncqt fails on MSVC build
* QTBUG-123172 tst_QApplication::abortQuitOnShow() crash on
Wayland(GNOME, Ubuntu 22.04)
* QTBUG-122580 Screenshorts for "Qt Widget Gallery" are cut off
* QTBUG-123715 qtdeclarative build fails on VxWorks (missing
__stack_chk_guard)
* QTBUG-73231 When a menubar spans across displays using different DPIs
then opening menus on either display can show the menu in the wrong
place
* QTBUG-117598 macdeploytqt: could not parse otool output; fails to
deploy Qt frameworks and dependencies
* QTBUG-48488 Cancelling Print to File Crashes Application
* QTBUG-123942 WASM tests failing
* QTBUG-109833 QEnterEvent does not have a valid timestamp due to QPA
API quirks
* QTBUG-123306 Orientation issues with embedding QML to Android Java
application
* QTBUG-118234 tst_qvulkan (Failed) on Android 14
* QTBUG-118220 tst_qrhi (Failed) on Android 14 emulator when running
within a CI VM
* QTBUG-124291tst_QWidget::setParentChangesFocus(make dialog
parentless, after) fails on Android 8 in CI
* QTBUG-123623 tst_qstandardpaths::testCustomRuntimeDirectory_data
doesn't check for failures
* QTBUG-117500 Sporadic crash onQFontEngineMulti::ensureEngineAt()
* QTBUG-124346 qt-everywhere-
src-6.7.0/qtbase/src/corelib/global/qglobal.h:70:10: fatal error:
QtCore/qversiontagging.h: No such file or directory
* QTBUG-121131 QML - Text - Font weight - macOS/Windows difference -
episode 2
* QTBUG-107185 Some tests appear to be re-testing the exact same data
tag
* QTBUG-123900 error: cannot pass object of non-trivial type
'QtJniTypes::Context' through variadic function; call will abort at
runtime
* PYSIDE-2648 Both sample/widget bindings examples fail in CMake on
configure
* QTBUG-122410 For some paper size setting margin has no effect
* QTBUG-124723 QThread::start(Priority) should be
QThread::start(QThread::Priority)
* QTBUG-124200 Linguist 'does not know the plural rules for Luganda'
* QTBUG-124272 QT_TEST_ALL_COMPARISON_OPS & QT_TEST_EQUALITY_OPS cause
massive code bloat
* QTBUG-123711 QtQuickView doesn't handle recreation of Activity
properly
* QTBUG-120565 Bottlenecks when compositing widgets with RHI
* QTBUG-12283 QTextDocument: HTML image width tag is not handled
correctly when the width is supplied as a percentage
* QTBUG-124771 MACOS_BUNDLE_POST_BUILD generates a symlink to a non-
existent dylib for static QML plugin, fails AppStore validation
* QTBUG-124265 configure -qpa "wayland;xcb"
* QTBUG-87805 Port mkspec QT_QPA_DEFAULT_PLATFORM mechanism to CMake
* QTBUG-124449 test_widgets_app_deployment failed on
debian-11.6-arm64-offscreen-tests
* QTBUG-125287 Android: Template args don't work for String[] using
jobjectArray
* QTBUG-114914 Using QLocale to set it to English will also display
Chinese
* QTBUG-122448 Date().toLoacleTimeString() doesn't respect the locale
* QTBUG-125283 std::ranges::search is faster than
QByteArrayView::contains
* QTBUG-118080 QDoc cannot distinguish between template function
overloads differing onlyin template arguments
* QTBUG-125097 Q_APPLICATION_STATIC needs to say that it's in #include
<QtCore/QApplicationStatic>
* QTBUG-101307 tst_qbytearrayview fails to compile with ubsan
* QTBUG-124575 Firebird 5 empty result with decimal value
* QTBUG-119469 Targets not yet defined: zstd::libzstd_static
* QTBUG-125588 QString::arg(char16_t{}) prefers the integral, not the
QChar overload
* QTBUG-125587 Cannot create DateTime from StdTimePoint
* QTBUG-124173 QTreeView / QTableView dataChanged very slow when topLeft
and bottomRight span many items
* QTBUG-69777 QML Window with Qt::Popup flag not behaving correctly
(mouse not grabbed)
* QTBUG-123361 Providing stable A11y identifier for reliable UI tests
* PYSIDE-2772 QTreeView is not displaying the data even though
QAbstractItemModel has an item.
* QTBUG-126053 QString::arg(u8' ') prefers the integral, not the QChar
overload, when built in C++20
* QTBUG-126054 QString::arg(wchar_t{}) prefers the integral overload
instead of the QChar one
* QTBUG-126055 [REG SiC 6.4 -> 6.5] QString::arg(qfloat16{}) is
ambiguous if QFLOAT16_IS_NATIVE
* QTBUG-53974 QGraphicsScene always in inactive state if placed in a
QTabWidget
* QTBUG-126248 macOS: widget UI flashes when overriding color scheme
during UI construction
* QTBUG-117321 Inconsistent treatment of char[] with embedded NULs when
target is QString vs. QByteArray
* QTBUG-126178 QtQuickView does not handle user input in a LinearLayout
* QTBUG-126225 tst_QSharedMemory::useTooMuchMemory(POSIX) timeout on
linux arm64 in CI
* QTBUG-125446 Ubuntu 24.04 ARM64: HealthCheck qtbase failings
* QTBUG-126278 QNetworkReply::attribute(HttpReasonPhraseAttribute)
returns empty value when Http2 is used
* QTBUG-126177 Crash when adding a QtQuickView before loading the
component
* QTBUG-126395 moc fails to parse around QT_WARNING macros in Q_SIGNALS
sections
* QTBUG-126546 Attribution documentation processed twice in CI
* QTBUG-124572 Program crash when using a specific glyph from a popular
font file on Linux
* QTBUG-126393 Can't build gallery example with qmake because it tries
to link to non-existent libqtesticonplugin.a
* QTBUG-126727 [QNX 7.1, Qt 6.7.2] Linking errors when building graphs
and quickcontrols examples with installed QNX binary
* QTBUG-106653 Crash on Accessibility interface
* QTBUG-125772 The loading order affects QIcon and makes it show the
wrong source image.
* QTBUG-125878 Cannot pinch-to-zoom after the qt 6.7.1 upgrade
[regression]
* QTBUG-126313 QScroller gesture blocks mouse clicks
* QTBUG-126426 QStyleOptionProgressBar is not properly rendered by a
delegate
* QTBUG-126150 QJniArray::const_iterator should be random-access, not
just bidirectional
* QTBUG-119616 tst_Http2::duplicateRequestsWithAborts fails in CI
* QTBUG-125405 QPdfWriter must use a cmap table for embedded TrueType
fonts
* QTBUG-126674 Inconsistent hashing between bool and integral overloads
* QTBUG-124653 Regression in QTemporaryFile::fileName()
* QTBUG-126866 Archiving the application does not have debug info files
(dSYM) included as expected
* QTBUG-127052 qt_add_translations does not add the generated .ts files
to the source list of the target
* QTBUG-125730 QAnyStringView('\xE4') creates an invalid UTF-8 string
(expected: valid L1)
* QTBUG-127110 Platforms still use the inefficient qvsnprintf() fall-
back
* QTBUG-127073 tst_QDnsLookup failures
* QTBUG-127404 CMake deployment API doesn't allow deploying into bin
subdirectories
* QTBUG-127464 Intel CET hardening needs an opt-out for WebEngine
* QTBUG-87728 tst_QGraphicsAnchorLayout::layoutDirection() failed on
Ubuntu 20.04 in CI
* QTBUG-125569 Make sure licensing in file matches that in
qt_attribution.json
* QTBUG-127085 Crash when re-opening laptop lid
* QTBUG-126187 HW Keyboard input is broken after touching UI
* QTBUG-68865 tst_QMenuBar::check_menuPosition autotest fails on Ubuntu
18.04
* QTBUG-127806 QLineEdit selects all text when receiving focus.
* QTBUG-127959 QIdentityProxyModel needs a way to disable builting
handling of layoutChanged and dataChanged
* QTBUG-127104 Misplaced pushbuttons in QScrollBar
* QTBUG-117637 qfloat16 comparison with integral types is ambiguous
* QTBUG-120637 QUuid::Id128Bytes UB when accessing members
* QTBUG-127468 Building against Android NDK r27 fails
* QTBUG-124011 Android: QFileInfo::isWritable() returns false
erroneously and throws an exception
* QTBUG-127953 Basic support for CMake FetchContent
* QTBUG-127442 REG[6.7 → 6.8]: generated qml type registration contains
invalid include paths
* QTBUG-127568 Top flaky test: tst_qtcpserver::qtbug6305
* QTBUG-126632 qmlimportscanner does not properly handle ../ in path
imports
* QTBUG-128322 tst_qstringapisymmetry fails to GPU init and message
reject
* QTBUG-118877 -qreal float configuration option does not compile
* QTBUG-109214 Documentation for QtAndroidPrivate is still wrong for
CMake
* QTBUG-128173 Doc: Remove use of defunct QDoc command
"\tableofcontents"
* QTBUG-101475 QTableWidget cannot internal move item
* QTBUG-126672 [Regr: 6.6.3->6.7.0] Additional initial a11y element
* QTBUG-128456 A method registered with registerNativeMethods() does not
work when the method has a jobjectArray parameter
* QTBUG-128424 Warning messages during configure are not helpful
* QTBUG-128498 tst_qcompare fails to compile on MSVC 2022 c++20
* QTBUG-125512 QDirListing::const_iterator copy semantics
* QTBUG-128029 wayland: Window container in QMdiArea does not work
* QTBUG-128656 Unclear usage of
QT_DECLARE_QESDP_SPECIALIZATION_DTOR_WITH_EXPORT
* QTBUG-117514 QFuture::then marked as private
* QTBUG-128796 Move QAndroidApplication native interface to virtual
functions instead of static methods

### qtsvg
* QTBUG-120708 Fluidlauncher manual testing -Error message on launch
* QTBUG-120233 QtSvg does not ignore desc and title tag contents when
child of text tag
* QTBUG-120695 Svgweatherinfo manual test -Stuck on loading
* QTBUG-121981 QtSvg parser does not handle nested svg elements
correctly
* QTBUG-120653 All SVGs with paths with more than 32768 points render
incorrectly
* QTBUG-123010 SVG supported by 6.6 but not by 6.7
* QTBUG-122752 [Reg: 6.4.2 -> 6.5.3] QFont::setPixelSize warning when
rendering svg files with painter font size set in pixels
* QTBUG-123178 SVG rendering of strokes with stroke-dasharray="0"
renders no line instead of a solid line
* QTBUG-119910 SVG image plugin collides with other image plugins
reading gzip compressed data
* QTBUG-12635 QImageReader::imageFormat returns "svg" for any XML
documents
* QTBUG-16804 When using QImageReader::imageFormat() with a XML file
then it will indicate that it is a SVG file
* QTBUG-63873 XML file mistakenly identified as SVG by QImageReader
* QTBUG-124287 QtSvg allocation too large memory when load the svg image
* QTBUG-123994 [REG 6.5->6.7] QML SVG rendering in 6.7 can't render file
properly (regression)
* QTBUG-125065 [REG 6.5.3 -> 6.6.0] Null-pointer deref when loading svg
file
* QTBUG-123138 QtSvg doesn't support feGaussianBlur
* QTBUG-128583 Regression in QtSvgTinyDocument: Runtime warnings logged
to the console
* QTBUG-82779 Several SVG are not drawn or animated correctly
* QTBUG-122310 SVG Rendering with opacity on group not consistent with
other viewers
* QTBUG-126486 Multiple Issues with bounding box in QtSvg
* QTBUG-118877 -qreal float configuration option does not compile

### qtdeclarative
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
* QTBUG-115166 qt_add_qml_module() causes non-Ninja generators to think
that projects are never up-to-date
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
* QTBUG-120100 qmlls: completion inserts colons in bindings
* QTBUG-120102 qmlls: completion mismatch for qualified expressions
* QTBUG-120111 qmlls: missing completion for qualified types
* QTBUG-120137 qmlls: completion inserts extra semicolon in for loops
* QTBUG-119842 qmlls: crash when autocompleting return statements
* QTBUG-120168 [Reg 6.6 → 6.7] Cannot launch minidesk appman example
* QTBUG-120084 [REG 6.6 → 6.7] bogus "TypeError: Cannot read property
'Foo' of undefined" error when using enums
* QTBUG-120279 Cyclic dependency error in qtquick3d
* QTBUG-120282 Configuring qtcharts from sources fails because of
dependency cycle
* QTBUG-117899 [REG 6.4->6.5] Binding Loops -> Wrong layout because of
interruption
* QTBUG-118511 Binding loop if ColumnLayout implicitWidth is changed
* QTBUG-120205 [REG: 6.5->6.6] Image implicitWidth/Height no longer
available in onStatusChanged
* QTBUG-119916 Non-native FileDialog does not prompt about overwriting
an existing file
* QTBUG-120322 qmlsc: crash on assigning int property
* QTBUG-120113 [Reg 6.6 -> 6.7] Bluetooth QML examples start crashing
after recent additions to QtDeclarative
* QTBUG-119760 Crash when dereferencing a deleted QRhi after native
window is re-created
* QTBUG-120349 Window Qml Type doc is missing the default visible
property value
* QTBUG-116306 Mention indeterminate state for Qt Quick Controls 2
ProgressBar customization
* QTBUG-120346hovered property of HoverHandler stays true when sliding
by touch outside of hover area
* QTBUG-120169 qmlls: no completion in attached/grouped properties
because of parser
* QTBUG-120296 Qt Quick Widgets Example-Grab Framebuffer is
susceptible to crash
* QTBUG-120489 Drag.imageSource property should work with other images,
not just screen grabs
* QTBUG-120504 REG: Call on null object in optional chain throws an
error
* QTBUG-119917 Non-native FileDialog loses current filename when
changing folders
* QTBUG-119903 the link to elevated card cannot be found
* QTBUG-120052 TextArea/TextField: placeholderText does not respect
horizontalAlignment after the component creation
* QTBUG-120336 [Reg 6.6 -> 6.7] Qt Quick Examples - Pointer Handlers
example crashes
* QTBUG-120473 [Reg 6.6 -> 6.7] qmlsc: type mismatch generates
uncompilable code
* QTBUG-119994 the documentation seems to be contradictory to the code
snippet
* QTBUG-120628 TableView: cannot select cells when using mouse press +
shift
* QTBUG-120065 Non-native FileDialog loses URL schema when filename is
manually entered
* QTBUG-120592 tst_inputpanel (Failed)
* QTBUG-113776 qmlformat fails to format if there is a escape char in
the key string
* QTBUG-119645 [Tests] Warnings in
qtdeclarative/tests/auto/quickcontrols/controls/data/tst_textarea.qml
* QTBUG-99231 "Could not set initial property horizontalAlignment" when
trying to set resettable property
* QTBUG-119646 [Tests] Warnings in
qtdeclarative/tests/auto/quickcontrols/controls/data/tst_textfield.qml
* QTBUG-120189 [Reg 6.6 -> 6.7] Cannot assign object of type
"IconPropertiesGroup" to property of type
"IconPropertiesGroup_QMLTYPE_1*" as the former is neither the same as
the latter nor a sub-class of it
* QTBUG-119372 build fails with Q_IMPORT_QML_PLUGIN macro
* QTBUG-120568 "Using the Configuration File in a Project" only covers
qmake way and not cmake
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
* QTBUG-121132 TableView: overlapping selections are cleared
* QTBUG-121206 NO_LINT has not effect in qt_add_qml_module
* QTBUG-121035 QSettings::value("Theme") returns an empty QByteArray if
beginGroup has been called
* QTBUG-113558 QQuickWidget does not handle touch event via QML
TapHandler correctly
* QTBUG-121139 qmlcachegen locks up in some situations
* QTBUG-115953 Interactive Flickable with pressDelay makes
childMouseEventFilter to lose MouseButtonPress event
* QTBUG-121436 FAIL!:
inputpanel::tst_plugin::test_pinyinInputMethod(row 1) Received a fatal
error.
* QTBUG-120512 Inconsistent behaviour between qmlsc and JIT compiler
when setting a property to "undefined"
* QTBUG-118857 Virtual Keyboard is hidden by QtQuick.Dialogs' dialogs
* QTBUG-121535 FAIL!:
qmltests::WebEngineViewSingleFileUpload::test_acceptDirectory() Received
a fatal error.
* QTBUG-113039 Crash when accessing properties of line parameter in
Text.onLineLaidOut
* QTBUG-121216 Drawer item does not support rotation for touch input
* QTBUG-80910 Drawer item does not support rotation
* QTBUG-71117 When the contentOrientation is changed for the
ApplicationWindow, then the Drawer does not drag out as expected
* QTBUG-115536 Setting Window.contentOrientation breaks Popup on regular
desktop
* QTBUG-121393 Q_UNREACHABLE was reached while compiling some files
* QTBUG-116426 crash in QQuickItemPrivate::derefWindow
* QTBUG-120450 Allocating or deallocating a QJSEngine object causes a
crash if the application has called mlockall(MCL_CURRENT|MCL_FUTURE)
* QTBUG-111729 Assertion failed in QJSEngine when repeatedly deleting &
adding property getters on an object
* QTBUG-121588 [REG 6.6 → 6.7] Crash in
VDMListDelegateDataType::createMissingProperties
* QTBUG-118710 [REG 6.5.2 → 6.5.3] QQmlProperty: wrong warning about
signal handler capitalization
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
* QTBUG-121728 FAIL!: tst_qqmlxmlhttprequest::open(Absolute network
url)) 'object->property("dataOK").toBool()' returned FALSE.
* QTBUG-122027 Baseline alignment offset when text has fallback fonts
* QTBUG-121909 [Reg 6.6 -> 6.7] Optional chaining+ nullish coalescing
leads to uncompilable code
* QTBUG-120506 [Reg 6.5 -> 6.6] Using `CameraLens.ProjectionType` as
type hinting cause runtime error
* QTBUG-120008 tst_QJSEngine::valueConversion_QVariant is flaky
* QTBUG-119459 [Reg 5.15 -> 6.2] the line number output by
console.trace() is too big
* QTBUG-120499 [REG 6.5.3 - 6.6.1] QML warning "Final member modelData
is overridden in class QQmlDMAbstractItemModelData. The override won't
be used."
* QTBUG-122108 Crash while attempting to load rich text resource from an
invalid scheme
* QTBUG-122173 tst_qquickanimatedimage::currentFrame() is flaky on
windows
* QTBUG-120573 [REG 6.6->6.7] TypeError: Property 'onDownPressed' of
object QQuickKeysAttached(...) is not a function
* QTBUG-122106 QList<int> is converted to int by qmlsc
* QTBUG-118750 REG: QQuickItem::setParentItem to null triggers
tst_qmltests crash
* QTBUG-118889 Assert when changing focus fast of
qquickmaterialplaceholdertext
* QTBUG-121840 Cannot format the text and the 'Touch User Interface' is
not available in text editor example on Qt 6.7.0
* QTBUG-121946 scoped enum values cannot be used as keys in a JS object
* QTBUG-122004 Generated code of qt_add_qml_module fails to build
* QTBUG-119829 [Reg 6.5 -> 6.6] Shadowing default property crashes QML
* QTBUG-121509 UTF support is broken in regular expressions of Qt's JS
engine
* QTBUG-120105 Unreliable QML Timer / qmltest wait() / QTest:qWait()
with offscreen platform
* QTBUG-121592 Attached ScrollBar and ScrollIndicator fail when using
QML Type Compiler
* QTBUG-121349 Flickable: strange defaults for mouse wheel triggered
boundsMovement
* QTBUG-107779 Regression: QQuickControlsTestUtils does not compile for
WebAssembly shared libraries build
* QTBUG-121594 Paste Action can't be disabled in context menu of
TextField
* QTBUG-118982 qmllint multiple pragma ComponentBehavior in same file
* QTBUG-116994 qt_add_add_qml_module runs into command line length
limits on Windows
* QTBUG-120526 qmllint complains wrongly when changing Layout attached
properties in a PropertyChanges
* QTBUG-120620 6.7.0.beta1 Calqltr app fails to start with single
threaded WASM
* QTBUG-119911 Incubated object is garbage collected before a reference
to it can be created
* QTBUG-119448 Fix documentation: initializing a property of aliased
property won't actually cause an error
* QTBUG-122024 Advertised and documented property of Layouts does not
work.
* QTBUG-122008 The child window does not get the style of the parent in
the attached style properties example (QQuickAttachedPropertyPropagator)
* QTBUG-122454 Gallery example radio buttons not working as expected
* QTBUG-110772 qmlsc/cachegen can trigger -Wtrigraphs
* QTBUG-117798 QmlCompiler generates bogus warning about writing back
object types
* QTBUG-116505 HoverHandler is broken when using a stylus
* QTBUG-101932 two HoverHandlers with different
acceptedDevices/acceptedPointerTypes: cursorShape doesn't change
accordingly
* QTBUG-120772 TextEdit.textDocument loads according to mime type
regardless of TextEdit.textFormat
* QTBUG-101364 qmllint spurious error: QML State AnchorChanges: with
type QQuickAnchorLine to QQmlScriptString of QQmlScriptString
* QTBUG-108673 QJSEngine use wrong logging category "default" for
console.trace()
* QTBUG-115478 Qmllint interferes with qmldir file in source directory
if present
* QTBUG-115439 Qmllint throws warnings at TapHandler's signals
* QTBUG-122230 Broken links in qtdeclarative docs
* QTBUG-122676 weatherforecast example: ASSERT crash when running on
Raspberry Pi OS (debian 11 derivative), arm64
* QTBUG-122705 Drag.imageSource property should have hi-dpi support
* QTBUG-33179 QML revisioning does not work for grouped properties
* QTBUG-121134 doc: fix QML tools links
* QTBUG-120007 QtQuick text rendering performance regression Qt5->Qt6
* QTBUG-122031 tst_qquickapplication::state() is flaky on opensuse
* QTBUG-75215 tst_qquickapplication::active() is flaky on opensuse
* QTBUG-120760 Unloading TableView headers via Loaders causes crash
* QTBUG-122251 qmltc crashes with Qt.point as a return type
* QTBUG-118804 The link is looping for Qt Quick Effect Maker
* QTBUG-107143 qmllint ignore RegisterEnumClassesUnscoped
* QTBUG-116057 Enums annotated as scoped-only match unscoped with
QML_SINGLETON
* QTBUG-109708 Startup crash in QRhiD3D11::endFrame() with nullptr
access
* QTBUG-101200 Qt crash/freeze when doing a graphics driver update on
Windows
* QTBUG-122686 Crash when processing hover events modifies object tree
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
* QTBUG-122232 Signed/unsigned mismatch in tst_qjsmanagedvalue
* QTBUG-121197[REG 6.6 → 6.7] Opening window from Loader does not work
* QTBUG-123014 tst_qquicktextdocument (Failed)
* QTBUG-113532 Animate RadioButton in the Material style
* QTBUG-120149 Material 3 - TextField placeholder issues when padding
changed
* QTBUG-122894 Crash when QQuickView loads QML document that binds
Overlay.overlay.[property]
* QTBUG-117923 ItemParticle causes constant CPU usage and rerenders
* QTBUG-122985 toggling TextEdit.format back and forth between AutoText
and PlainText loses markdown after a couple of times
* QTBUG-108019 QSGTexture::nativeInterface() doesn't work for
QSGMetalTexture
* QTBUG-121388 Qt Quick Controls: Palette role values don't get live
updates
* QTBUG-119812 QML Advanced Tutorial 4-Example -Highscores are
doubled
* QTBUG-121466 ApplicationWindow background Image does not resize when
source changed
* QTBUG-122340 MultiEffect - Wrong initial position of the shadow
(MultiEffect)
* QTBUG-122746 Quick controls Popup - shadow is rendered incorrectly
* QTBUG-123118 QQuickShaderEffect missing property updates
* QTBUG-123171 QmlFormat Semicolon is missing at the end of some default
exports
* QTBUG-122665 [Reg 6.6.1 → 6.6.2] ListView footer item cannot be
vertically placed
* QTBUG-122076 QQuickItem::classBegin()/componentComplete() never
invoked when using QQmlComponent::loadFromModule()
* QTBUG-123307 build fails "qtdeclarative/src/quick/platform/android/qan
droidquickviewembedding.cpp"
* QTBUG-123225 REG[6.6 → 6.7]: QML: unscoped enums stopped working
* QTBUG-123111 Particle System Application stuck on GUI thread
* QTBUG-121500 Default flick deceleration is far too high for
touchscreens, can't be customized through platform theme
* QTBUG-35608 Flickable speed and deceleration does not scale with pixel
density
* QTBUG-35609 Flickable speed and deceleration are not easily
customisable
* QTBUG-120542 Editable SpinBox crashes Quick3d application
* QTBUG-119765 [Reg 6.5.2 -> 6.6.1]default roles are not available in
abstract table model headerdata
* QTBUG-123428 [REG 6.6 → 6.7 ]Using QML_DISABLE_DISK_CACHE breaks QML
code
* QTBUG-123421 Documentation wrong for QML_CONSTRUCTIBLE_VALUE
* QTBUG-97252 Swipeview stops responding after right-clicking
* QTBUG-95939 tst_taphandler is flaky on OpenSUSE
* QTBUG-123413 qmltypes warning when using const in Q_INVOKABLE
* QTBUG-123332 Install dir is incorrect for Qt6AndroidQuick.jar
* QTBUG-123394 [REG 6.5.5 -> 6.6.2] Dial control looks wrong
* QTBUG-114694 [Tests]
tst_controls::Basic::SpinBox::test_editable_doubleSpinBox fails on macOS
* QTBUG-123490 Flickable doesn't react to second touchpoint while first
touchpoint is dragging DragHandler
* QTBUG-86729 many Qt Quick test failures after input event refactoring
* QTBUG-113226 Flickable emit flickStarted even though the child is
processing the pinch gesture
* QTBUG-120267 qmllint: Member "destroy" not found on type "Popup"
* QTBUG-123395 QML EXC_BAD_ACCESS crash
* QTBUG-116589 Dynamic translations seem not working with
QQmlApplicationEngine::loadFromModule()
* QTBUG-123588 Compiler warnings in generated code of user project
* QTBUG-123089 qmltyperegistrar: missing "isConstructible" for
QQuickStackViewArg
* QTBUG-123484 [Reg 6.7 > 6.6.2] Crash in QJSValue copy constructor
* QTBUG-123613 qmlcachegen crashing with Qt 6.7.0-rc2
* QTBUG-123541 QmlFormat. MethodDefinition is not supported
* QTBUG-123499 tst_MptaInterop::touchesThenPinch fails in Qt 6
* QTBUG-123594 Missing dependency in QtQuick/Controls/Material/impl
* QTBUG-123591 qmlls crashes when opening more than one file
* QTBUG-122564 Contactlist example not opening (CMake)
* QTBUG-123535 qt_generate_foreign_qml_types fails with Q_ENUM_NS
* QTBUG-118076 pragma FunctionSignatureBehavior: Enforced is broken for
object lists
* QTBUG-100866 Grid accessible fails to delete accessible items with
reuseItems set
* QTBUG-123837 QQmlJSScope fails to correctly recognize required aliases
to non required property when marked as required outside the
declaration.
* QTBUG-123805 CurveRenderer crashes when calculating dash pattern
* QTBUG-123114 QQuickPopupPositioner uses wrong bounds when
Window.contentOrientation == Screen.orientation
* QTBUG-123920 qtdeclarative build break when texthtmlparser - feature
is turned off
* QTBUG-120033 Binding not evaluated
* QTBUG-119756 [Tests] Warnings in tst_controls::macOS::SpinBox
* QTBUG-123596 Crash JS for x in o{ delete o[x] } if o is a
sparsearray
* QTBUG-122925 QQmlComponentPrivate::doBeginCreate can crash in some
scenarios
* QTBUG-123871 qmlls crashes
* QTBUG-120551 qmllint: incorrectly warns when using a function in a
javascript library
* QTBUG-123865 [Reg 6.2 -> 6.5] Crash when using PropertyChanges with
multiple inline components
* QTBUG-123050 Crash when trying to build QML files (qmlcachegen)
* QTBUG-118636 Some missing content of the rich text table while
displaying HTML file with TextArea
* QTBUG-119572 [Tests] Warnings in
tst_controls::Imagine::RangeSlider::test_nullHandles()
* QTBUG-119633 [Tests] Warnings in
qtdeclarative/tests/auto/quickcontrols/controls/data/tst_slider.qml
* QTBUG-120097 Screen Reader reads password in Password TextField
* QTBUG-124084 [Reg 6.5.3->6.7.0] Nested ListModel set from c++ is not
working any more
* QTBUG-123547 qmldom: cannot create dom if script expression contains
comment
* QTBUG-123645 CollectedComments data in AstComment is invalidated
* QTBUG-124163 With SW backend, QQuickPaintedItems show aliasing when
transformed
* QTBUG-124170 QQuickPaintedItem: antialiasing property has no effect
* QTBUG-123864 qmlformat: does not preserve empty lines
* QTBUG-124226 Confusing example code for Qt.createComponent
* QTBUG-123196the Shape object doesn't display ShapePath objects
injected by Shape.data.push() function.
* QTBUG-119482 QML Strict mode refuses to compile console.log for
QStringList
* QTBUG-43842 Scanning for QML imports of projects fails
* QTBUG-123378 QML TextInput makes the application unresponsive if made
invisible when it has keyboard focus on Android
* QTBUG-68527 Automatic ListView content positioning while disabled
* QTBUG-124201 [Tests] Warnings in tst_controls::Windows::SpinBox
* QTBUG-124275 [Tests] Warnings in tst_controls::iOS::RangeSlider
* QTBUG-117641 Loader and loaded item sizes can get unsynchronized
* QTBUG-120670 TextField causing activeFocus of the calling item to be
triggered multiple times.
* QTBUG-84976 When Window has no activeFocus, activeFocus lost after
transitioning back from Dialog to Window
* QTBUG-124281 MultiEffect doesn't seem to free resources at its
destruction
* QTCREATORBUG-30627 Follow symbol for QML imported modules does not
function with QML LSP enabled
* QTBUG-124290 [Tests] Warnings in tst_controls::iOS::Slider
* QTBUG-83408 Text disappears with ElideRight.
* QTBUG-33608 Elide property of Text breaks component resizing
* QTBUG-46487 PathView. DelegateModel::item: index out range error when
model is reset with less number of items
* QTBUG-122250 GridView is missing documentation for reuseItems
* QTBUG-123773 [Contact List Example] Example not running on MacOS
* QTBUG-123227 Qt Quick Test missing cmake support
* QTBUG-124359 Cannot use variableAxes due to wrong component versioning
* QTBUG-111337 Text incorrectly renders bullet list points after a link
* QTBUG-123855 Inconsistent RichText Formatting of "&lt;ol&gt;" and "&lt;ul&gt;" in
Text QML type
* QTBUG-63741 Subsequent bullet points incorrectly colored by hyperlink
* QTBUG-57833 QTextEdit list number/bullets inherit the following text
style
* QTBUG-26612 QTextDocument doesn't render code in list items properly
* QTBUG-73859 HTML font attributes override styling, rather than add to
it
* QTBUG-75887 The delegate object in the Listview for DelegateModel with
DelegateChoice is not being updated on role value change in the model
* QTBUG-123528 macOS: Hard to tell if a Switch is in checked state in an
inactive window
* QTBUG-124428 Customisation documentation includes deprecated
DropShadow example
* QTBUG-124225 [REG 6.7 → dev] Assert: start > 0 in
QQmlComponentPrivate::beginCreate
* QTBUG-124229 FAILED:
src/qmltest/CMakeFiles/QuickTest.dir/quicktest.cpp.o
* QTBUG-94100 TreeView: adding columns not handled
* QTBUG-121143 SelectionRectangle does not work correctly when de-
selecting
* QTBUG-98958 Image sourceClipRect has no visual effect on an image from
QQuickImageProvider
* QTBUG-86316 Image sourceClipRect ignored for textures, "image:" urls
* QTBUG-122783 Material.theme doesn't propagate to ListView header when
elevation animated
* QTBUG-123763 MessageDialog detailed text goes out of bounds in
Material style
* QTBUG-124459 qmlls: no completions after "id." when components are not
bound
* QTBUG-123593 qsb generates shader that webassembly does not accept
* QTBUG-123993 [Reg 6.6 -> 6.7] QVariantList conversion from/to QML
broken in Qt 6.7
* QTBUG-124220 Weird compiler warning for functions without return type
annotation
* QTBUG-124622 [Tests] Warning in
tst_controls::Material::Popup::test_size()
* QTBUG-122990 tst_qmlformat::testExample issues: slow + triggers
warnings
* QTBUG-124521 QT_QML_GENERATE_QMLLS_INI generates wrong buildDir
* QTBUG-124730 MultiEffects Shadow in repeater causes application to
crash
* QTBUG-108696 [TapHandler] Internal warning "QObject::disconnect:
Unexpected nullptr parameter"
* QTBUG-122582 qmlcachegen generates code with int/qsizetype confusion
* QTBUG-119885 Function signatures are insufficiently enforced
* QTBUG-124363 [6.7 REG] Changing QML Window visible property clobbers
window state
* QTBUG-124456 [6.4.2] Margins in QuickLayouts causing a QList exception
(index out of range)
* QTBUG-124569 Qt Quick rendering of html table borders is inconsistent
with widgets
* QTBUG-120986 QML Type TextArea or TextEdit doesn't render CSS table
and table cell border correctly
* QTBUG-113040 Quick Text: SVG inline images have poor quality on High-
DPI displays
* QTBUG-124474 The text of QML ComboBox in a Window turns invisible in
dark mode
* QTBUG-125049 SplitView jumps to an incorrect width when resizing if
another object in SplitView is not visible.
* QTBUG-125076 [Reg 6.5->6.7.0] Doc for QQuickItem no longer says
"Instantiated by: Item"
* QTBUG-124771 MACOS_BUNDLE_POST_BUILD generates a symlink to a non-
existent dylib for static QML plugin, fails AppStore validation
* QTBUG-125153 cmake: Deployment of shared module fails with Xcode (non-
ninja) generator during the post build step (not during installation)
* QTBUG-124230 tst_focus::reason is failing
* QTBUG-125214 There is no equivalent to glBlendEquation in
QSGMaterialShader
* QTBUG-124657 qsTrNoOp() is not defined in QML
* QTBUG-125393 qmllint fails when given files names with backslashes on
Windows
* QTBUG-125228 Customizing Quick Controls Documentation should use
Templates instead
* QTBUG-124357 Quick Controls are not rendered correctly when changing
OS theme
* QTBUG-105697 linebyline lexer test fail on android
* QTBUG-123436 tst_linebylinelex failed on webOS
* QTBUG-119644 [Tests] Warnings in
qtdeclarative/tests/auto/quickcontrols/controls/data/tst_combobox.qml
* QTBUG-56921 Imperatively setting TextEdit's alignment results in
incorrectly aligned text
* QTBUG-125580 [Tests] Warnings in
tst_controls::Material::ComboBox::test_comboBoxWithShaderEffect()
* QTBUG-124799 qmlls crashes on autocompletion
* QTBUG-125576 Qml Compiler: unresolved QStringBuilder results might
cause problems
* QTBUG-74331 beyond living (aka not really dead) link in colors docs
* QTBUG-125429 send array from qml to c++
* QTBUG-123882 QML list of length N emits (N+1) value change signals
when shift() is called
* QTBUG-125723 Android type converters is missing Java Long type
* QTBUG-125127 Documentation of the QML singleton: correct the snippet
for pragma Singleton
* QTBUG-126011 shared_qml_module (Failed)
* QTBUG-125961 Built AAR has SDK version mismatch with Embedded QML
example
* QTBUG-125765 QML builtins are linked into user binaries
* QTBUG-125864 Broken rendering with curve renderer in Shapes example
* QTBUG-123361 Providing stable A11y identifier for reliable UI tests
* QTBUG-125914 Formatting qml code containing an enum with qmlformat
removes enum values
* QTBUG-122658 ListView crashes when `reuseitems` is set after
`positionViewAtIndex`
* QTBUG-124624 Online documentation doesn't explain how to set dark
theme of Fusion style
* QTBUG-125720 Typo in example code in QQuickRhiItem documentation
* QTBUG-119647 [Tests] Warnings in
qtdeclarative/tests/auto/quickcontrols/controls/data/tst_tumbler.qml
* QTBUG-124461 qmlls does not exit after receiving an exit request
* QTBUG-125879 ASSERT in qmlls
* QTBUG-125529 Lancelot baseline mismatch in Qt Quick's ComboBox using
Basic style
* QTBUG-126267 QQuickTextDocument::setTextDocument disables TextEdit
* QTBUG-125725 QQuickControl::focusReasonChanged does not work properly
* QTBUG-126124 Material style Button has extra padding when text
property has a value but display is IconOnly
* QTBUG-125157 Clarify the snippet about Editing Cells in a TableView
* QTBUG-126039 Dragging HeaderView works even when the mouse event is
accepted by a MouseArea inside an (header) cell
* QTBUG-124744 [Reg 6.7.0 -> dev] Bindings on width/height of
ApplicationWindow.background are not respected
* QTBUG-126094 Spelling of Qt Qml/QML very inconsistent
* QTBUG-115856 Don't let qmllint warnings fail the build
* QTBUG-112320 javascript engine:Proxy handler.get() doesn't work on
field 'name'
* QTBUG-118165 qmlTypeId() causes QML_ELEMENTs to not be registered
* QTBUG-122998 Crash in QQuickItemView through recursive item release
* QTBUG-123527 Unchecked Fusion style RadioButtons / CheckBoxes are
barely visible in dark mode
* QTBUG-125481 [Reg 6.7.0->6.7.1] Combination of Quick Layouts broken
* QTBUG-126136 QML signal to C++ slot connection nonfunctional if
declared within the C++ object with the slot
* QTBUG-125224 Cannot stop animation if it was restarted before the last
loop completed
* QTBUG-126175 tst_QQuickPopup::popupWindowChangingParent is flaky
* QTBUG-119866 TapHandler is used in most of the code snippet of
DragHandler
* QTBUG-126057 Item state change reverts item's scaled size
* QTBUG-120216 QQmlThread causes linker errors with USBan by using
unexported class QThreadPrivate
* QTBUG-126512 Controls styles use Qt.styleHints even though
documentation advises against it
* QTBUG-126539 Native context menu shows every second time
* QTBUG-126042 Nested ListView of orthogonal orientation gets stuck
without snapping using touchpad
* QTBUG-126330 Crash when resizing ListView with reuseItems: true and
custom QQuickAsyncImageProvider
* QTBUG-126510 [REG 6.6 -> 6.7] Type error due to clash between JS and
Qml type names
* QTBUG-126504 QML Nested Imports - some problems
* QTBUG-126628 QQuickAsyncImageProvider causes crash without Qt Network
(qml_network)
* QTBUG-125906 Flicking needs to be done horizontally to delete items in
apps that have been rotated 90°.
* QTBUG-126563 [Reg 6.5 -> 6.7] Anonymous function on a signal results
in QML Linter error when compiler warnings are enabled
* QTBUG-124572 Program crash when using a specific glyph from a popular
font file on Linux
* QTBUG-30768 When an item in a ListView is snapped into place then it
does not take account for the section header
* QTBUG-126626 Hovered property stays when popup is opened from drawer
* QTBUG-118903 Dragging ListView with Apple Pencil keeps items in
highlighted state
* QTBUG-125526 [REG 6.6.3-6.7.0] TextEdit - warnings on loading embedded
QRC images
* QTBUG-126396 Illegal memory access in QQuickShaderEffectPrivate
* QTBUG-126673 [Regression 6.6 -> 6.7] Higher CPU utilization in large
QML applications
* QTBUG-123894 Top flaky test: tst_qquicklistview::multipleTransitions
on MacOS_14 ARM64, MacOS_12 and MacOS_13
* QTBUG-125611 Inconsistent QString::isNull behavior in
QJSEngine::evaluate result and QJSValue constructed from QString
* QTBUG-125095 [REG 6.2 → 6.5] Qt.binding fails with QtQObject inside
createObject
* QTBUG-126834 [Reg 6.5 -> 6.6] Qml: Compiler generates wrong code for
Array.prototype.join invocation
* QTBUG-81231 QJSEngine and QStringList properties handling, a potential
performance issue
* QTBUG-125959 Cannot compile with qmltc when the type to compile
include a QML module that contains .hpp files
* QTBUG-126723 [REG 6.6 → 6.7] TableModel appendRow() no longer works.
* QTBUG-126712 qmlls: missing completions on QML module imports
* QTBUG-126676 qml lexer creates function tokens with wrong length
* QTBUG-123987 QML Popup "palette" property is not linking forward to
the proper palette docs
* QTBUG-122963 Inconsistency in popup positioning logic
* QTBUG-116442 Doubleclick sent to first item when single-clicking
alternating items
* QTBUG-125053 QAbstractListModel fails to populate QML model
* QTBUG-126714 qmlls: avoid psychedelic highlighting mode on invalid
code
* QTBUG-125296 background color of TreeViewDelegate
* QTBUG-126690 Creating dynamic properties and reparenting a Control
break bindings on Singletons
* QTBUG-127072 Timer QML type missing from documentation snapshots
* QTBUG-126819 Stroke width 0 is interpreted differently by the
QuickShape renderers
* QTBUG-126782 Android build fails on
'qtdeclarative/src/quick/platform/android/qandroidviewsignalmanager.cpp'
* QTBUG-126474 QQuickLayout Recursive Rearrange Locks Application
* QTBUG-127166 Dimmer trying to be stacked before a top level popup
window
* QTBUG-127292 Failures on tst_qquicktextdocument
* QTBUG-109880 Wrapper method that should create and return a Javascript
Generator object returns undefined
* QTBUG-124412 qmllint warns about accessing highlightResizeDuration etc
from ListView attached property
* QTBUG-127092 When the URI starts with a numeric string,
qt_add_qml_module will generate erroneous code.
* QTBUG-127009 Assert in QVariant possibly caused by mis-compilationby
qmlsc/qmlcachegen
* QTBUG-126398 Decide whether QV4::Sequence should be implicitly
convertable to QStringList
* QTBUG-127328 NinePatchImageSelector cannot use relative path for
source
* QTBUG-127379 Service Embedding manual test doesn't build
* QTBUG-106103 Deleting a Binding doesn't restore
* QTBUG-126711 qmlls: go to definition does not work on
ApplicationWindow
* QTBUG-127399 LayoutMirroring warning has typo
* QTBUG-123191 Scenegraph nodes batching broken beginning with Qt 6.5.3
* QTBUG-127169 Material style theme does not change when the system
theme changes
* QTBUG-127273 [QNX 6.8.0 beta2] Do not try to use clipboard in
quickcontrols/spreadsheets on QNX - no support for it on the platform
* QTBUG-123861 Passing a string that contains a dot to
`QQmlComponent::createWithInitialProperties` will crash the application
* QTBUG-126886 Setting format in QQuickTextDocument (TextArea) crashes
* QTBUG-127532 Using JS template literals breaks qmlls' auto-completion
list
* QTBUG-127474 qmlls erases user code when updating implicitly defined
signal handlers
* QTBUG-124498 qmltyperesolver can't handle ECMAScript resources
* QTBUG-127067  qml_in_android_view example project build error
* QTBUG-125146 qmllint highlights wrong part in warning message
* QTBUG-127309 qmllint: uses wrong category forProperty "xxx" has
incomplete type "Unregistered". You may be missing an import. [missing-
property]
* QTBUG-127602 qmlls does not read .qmllint.ini
* QTBUG-127572 qtdeclarative/gallery example does not run for
webassembly
* QTBUG-97557 Qt Quick batch rendering issue when a batch contain nodes
that have different index types
* QTBUG-127619 FileDialog prints binding loop warning when opened.
* QTBUG-126127 Same file twice in sources, lower and upper case first
letter
* QTBUG-127703 tst_controls::RangeSlider::test_overlappingHandles()
failed on Ubuntu 24.04 offscreen
* QTBUG-126616 CurveRendering artifacts drawing fonts
* QTBUG-127315 Tumbler's currentIndex is not the same as the initial
value
* QTBUG-127016 Improve documentation for using a TreeModel in a Qt Quick
UI
* QTBUG-127700 tst_popup.qml::test_popupWithOverlayInLoader() crash
* QTBUG-124921 Tumbler's currentIndex is not working when the model is
changed at runtime
* QTBUG-127330 QtCharts\plugins.qmltypes: Property object is missing a
name or type script binding.
* QTBUG-127687 qmlls does not print warning categories on warnings
* QTBUG-127704 [REG: 6.6.2 → 6.7.2] QList<QObject *> argument causes
TypeError
* QTBUG-124553 [Reg 5.15 -> 6.2] QML Binding is overwritten after
initialization
* QTBUG-127519 CurveRenderer leaks SGNodes
* QTBUG-118024 Still referenced objects are deleted during swap
operation between two ListModel instances
* QTBUG-124847 qsTr() documentation could also show how to use
disambiguation and plural forms
* QTBUG-127782 Crash on Dragging Sections by Start Dragging Close to the
Border
* QTBUG-124124 QtQuick MessageDialog: Fails on macOS when using richtext
* QTBUG-127458 qmlls fails to provide auto-completion for formal
parameters in signal handlers
* QTBUG-127586 qmlls: wrong autocompletion on attached types
* QTBUG-127609 qmlls: completion wrong for qualified imports
* QTBUG-127865 Crash When Dragging Sections Between Different Header
Views
* QTBUG-127650 Strange behaviours in QML warning, "Using attached type
<TYPE> already initialized in a parent scope"
* QTBUG-126981 Application crashes with assert when closing the window
with TableView
* QTBUG-123636 Crash when calling QWidget::setFixedSize with larger
values
* QTBUG-121449 The emojis are pixelated
* QTBUG-124764 qt_add_lupdate adds extra location for QML files
* QTBUG-127034 Qcolor Class / color QML value type cannot be copied via
HSL values
* QTBUG-127809 TableView forceLayout does not correct contentX/contentY
after columnWidth/rowHeight changed
* QTBUG-125416 SwipeView shows all elements at once if it is 0x0 in size
* QTBUG-125630 TextInput.passwordMaskDelay does nothing if echoMode is
PasswordEchoOnEdit
* QTBUG-115759 Centering an element in Overlay results in visual
inconsistencies
* QTBUG-126514 [Regr: 6.5.0->6.7.1] Mouse wheel scrolling in nested list
views broken
* QTBUG-127343 Incomplete and inconsistent type checking for QML lists
* QTBUG-126576 qmlls: automatic qmltypes generation is slowing
completions and highlighting down
* QTBUG-127846 quickcontrols/spreadsheets not launching when installed
outside of build dir
* QTBUG-114984 Software Renderer: Updating a layer-enabled subtree while
it is invisible produces wrong outcomes
* QTBUG-127455 QML ListView crashes in
QQuickItemViewPrivate::itemGeometryChanged
* QTBUG-128283 Memory leak after calling QQuickItem::grabToImage
* QTBUG-127906 Qt.labs.platform.Menu opens at the wrong location with
scaling enabled
* QTBUG-120011 Qt Quick Controls Menu can appear at the wrong position
when DPI Awareness is enabled
* QTBUG-127440 QML TextField can't deselect by clicking on the text
field
* QTBUG-10684 Interaction between text input and flickable is lacking
* QTBUG-111504 Text loses selection when releasing long-press on Android
text input
* QTBUG-116606 unable to deselect text in text input using touch
* QTBUG-127049 Infinitely Recursvie Iterators Segfault process
* QTBUG-128128 QML_ELEMENT exposes types of arguments of all slots in
.qmltypes-file
* QTBUG-127442 REG[6.7 → 6.8]: generated qml type registration contains
invalid include paths
* QTBUG-126632 qmlimportscanner does not properly handle ../ in path
imports
* QTBUG-80344 Button's icon blurry because of non-integer position
* QTBUG-110451 emitting dataChanged trips on freed delegate memory
* QTBUG-123377 JS Set iteration does not follow spec
* QTBUG-124731 grabPermissions: PointerHandler.TakeOverForbidden
conflicts with contentItem (or ItemDelegate) on iOS
* QTBUG-123595 VerticalHeaderView / HorizontalHeaderView should always
use headerData() -- stale docs?
* QTBUG-127727 tst_SoftwareRenderer::renderTarget fails
* QTBUG-125995 Fix aotstats cmake support on Xcode
* QTBUG-126987 Setting combobox focus to false doesn't close it when
popupType is set to popupWindow
* QTBUG-128605 The dependency target
"qtgraphicaleffectsplugin_qmltyperegistration" of target
"module_qtgraphicaleffectsplugin_aotstats_targets" does not exist.
* QTBUG-128561 Crash when re-showing shape using CurveRenderer
* QTBUG-126815 Action triggered callback has incorrect source when
popupType is set to PopupWindow
* QTBUG-126713 Attached style properties not propagating when popupType
is set to popup window
* QTBUG-128611 Service Embedding manual test doesn't compile / crashes
* QTBUG-128586 Signals without arguments give false warnings in QML in
Android
* QTBUG-128638 [Reg 6.7 -> 6.8] Crash when using live preview
* QTBUG-128782 [Reg 6.7 -> 6.8] Crash when using live preview
* QTBUG-128420 Qt 6.8 does not support build paths with white spaces
anymore
* QTBUG-128860 Qt6QmlMacros doesn't handle build directories with spaces
in the path
* QTBUG-116106 New accentColor role is missing from QQuickColorGroup
* QTBUG-117667 REG: TextEdit height gets stuck due to binding loops
(forever) or anchor changes (temporarily until further resize event)
* QTBUG-25489 QtQuick2 TextEdit emits unnecessary cursorRectangleChanged
on all kinds of modifications
* QTBUG-116551 qt_generate_deploy_app_script doesn't support all
windeployqt arguments
* QTBUG-108808 QQC2 BusyIndicator does not inherit visibility from
parent consistently
* QTBUG-117654 TextArea multi-line placeholder text overlaps the
TextEdit area
* QTBUG-120262 Use SPDX-License-Ref in 3rdparty directories
* QTBUG-119550 Refactor DOMenvironment loading & parsing files
* QTBUG-121192 _qt_internal_collect_buildsystem_targets does not handle
multiple build directories of the same source directory
* QTBUG-118867 Render thread can delete font engines still in use
* QTBUG-120356 padding not applied to header and footer for
QuickControls.Dialog
* QTBUG-99178 QFileSystemModel should have an option to disable icon
loading; crashes if the icon provider is null
* QTBUG-121643 qt6-declarative: possible build-time race condition
around qmlcachegen
* QTBUG-122067 Material ToolTip::test_attached and
ToolTip::test_attachedSizeBug are flaky on macOS
* QTBUG-122256 Crash on
QQuickMultiEffectPrivate::updateBlurItemsAmount() with nullptr access
* QTBUG-62111 Docs: Fixed day/year format in QDateTime
* QTBUG-119437 Drop optional when nullish coalescing an optionalT with
a rhs of type T
* QTBUG-122380 QML cannot handle "as string"
* QTBUG-122405 tst_qquickhoverhandler::window is flaky on OpenSuse
* QTBUG-63363 QPointingDevices for the trackpad and mouse are
dynamically instantiated on macOS
* QTBUG-112432 wayland plugin should distinguish touchpads from mice,
etc.
* QTBUG-122653 6.8.0 toplevel build fails on MSVC2019 x64, qtdeclarative
* QTBUG-122679 tst_how-to-qml timePicker is flaky
* QTBUG-109548 Find a signal-specific replacement for PropertyChanges
* QTBUG-78846 tst_qquicktextedit::mouseSelectionMode is flaky on
OpenSuse 15
* QTBUG-122956 QQmlObjectCreator::beginPopulateDeferred: Incorrct usage
of scope
* QTBUG-74342 QML RichText hr element doesn't work
* QTBUG-120067 Material 3 - Controls height issues
* QTBUG-115438 [REG: 5->6] MouseArea onEnter triggers before onExit on
the previous item
* QTBUG-123160 crash in qquickspinbox
* QTBUG-110475 [REG 6.4.1 → 6.4.2] Interactive elements in SwipeDelegate
receive no events
* QTBUG-122260 IndentingLineWriter not always correctly indent when
carryover
* QTBUG-104768 Overlay is not available when hardcoding the style
* QTBUG-123103 Naming conflict with QtQuick.Controls and IconImage
* QTBUG-119689 Qt Quick Examples Views - Typo in "ObjectModel"
* QTBUG-123210 QML: Rectangle with rounded corners and border width = 1
shows not good anti-aliasing
* QTBUG-108831 Some Rectangle borders are double the width with
fractional scale ratios
* QTBUG-123386 QmlFormat. Incorrect handling of some comments
* QTBUG-123318 QT Quick controls - Wearable Demo example: Notifications
in the demo mode is skipped
* QTBUG-122321 qmltc: WebEngineView with anchors causes assertion at
component creation
* QTBUG-123592 Foreign generation fails with namespace
* QTBUG-123999 Heap buffer overflow in JS Set.delete
* QTBUG-124145 FAILED:
tests/auto/benchmark/.rcc/qmlcache/benchmark_direct_Test_qml.cpp
* QTBUG-118222 tst_nodestest (failed) on Android 14 emulator when
running in a CI VM
* QTBUG-123162 macOS: QMdiSubWindow title bar gradient stands out too
much in dark mode
* QTBUG-92855 Dock widgets' title bars on macOS dark mode do not fit in
* QTBUG-101143 QML_FOREIGN refering to a class in another library leaves
the type empty in qmltypes file
* QTBUG-90479 [Reg 5.13.2->5.14.0] PathView's strange behaviour with
model having 19 items
* QTBUG-42504 QML PathView cacheItemCount does not work, crashes
* QTBUG-59108 PathView enters in to loop of Creation/Destruction of
delegates
* QTBUG-50540 Pathview delegates not created correctly with caching
enabled
* QTBUG-124129 qmlls crashes
* QTBUG-112840 Please write the realistic usecase of Qt Quick Test to
the documentation
* QTBUG-114969 qmllint should consider QML2_IMPORT_PATH for import paths
* QTBUG-123908 '6.7.0' versions found in 6.8.0 sources
* QTBUG-65461 Qt Quick Controls 2 Menu::visible does not work when
inside MenuBar
* QTBUG-115140 qtdeclarative -unity-build-batch-size 100000 fails
* QTBUG-116577 ASSERT: "sumFactors > 0.0"in qgridlayoutengine.cpp
* QTBUG-124294 Unresolved type even it is listed
* QTBUG-121131 QML - Text - Font weight - macOS/Windows difference -
episode 2
* QTBUG-71497 [REG: 5.11->5.12] Qt.include() does not import functions
when the included script is using strict mode
* QTBUG-125240 Core Protobuf types need QML registration
* QTBUG-70063 tst_font::font(Control) crash on macOS 10.13
* QTBUG-122986 Document recommended project structure for projects that
have a QML module used by two or more executables
* QTBUG-125585 Line spacing of many fonts is dramatically different
between Qt5 and Qt6
* QTBUG-88646 tst_qquicktext::contentSize() failed on msvc2019 developer
build in CI
* QTBUG-126047 tst_qquickpixmapcache::slowDevice crashes sporadically
* QTBUG-126184 tst_qquickwindow::visibilityDoesntClobberWindowState is
flaky
* QTBUG-122784 QtQuick: Unset required property in Singleton is not an
error?
* QTBUG-111766 qml issues in Effect Maker
* QTBUG-126222 tst_how_to_qml::activeFocusDebugging() fails often
* QTBUG-117526 QQuickStylePrivate::fallbackStyle has the wrong value
when using run-time style selection and the fallback style is imported
via the style's qmldir
* QTBUG-125867 SelectionRectangle in Drag mode intercepts events even
when it should not
* QTBUG-125753 Fix PointRenderer series add/remove/visibility
* QTBUG-126667 tst_QQuickPopup::popupWindowPositioning is flaky
* QTBUG-68465 macOS: Accessibility: MenuItems are not accessible
* QTBUG-112870 clang-tidy warnings on static global variables in moc
generated code
* QTBUG-33017 [autotest] tst_qquickgridview tends to fail on win and osx
* QTBUG-88644 tst_QQuickGridView::snapToRow() failed on msvc2019
developer build in CI
* QTBUG-126201 Qt examples output CMake warning about Qt policy QTP0004
* QTBUG-126662 2D Graphs: low performance on scrolling axis
* QTBUG-126863 [REG 6.7->6.8]: Cannot read from attached
'Accessible.name' property
* QTBUG-126560 ListView's count property not updating when the ListView
is inside a Drawer and the model gets its data from a network request
* QTBUG-124756 QQuickWindowContainer is not in the right child order
* QTBUG-122415 Flickering when dragging a sub window
* QTBUG-125589 weired console message with simple application
* QTBUG-118109 qmllint: deferred-property-id logging category is muted
* QTBUG-124468 qmlpreview fails to load libworkerscriptplugin.so
* QTBUG-125571 YAnimator onRunningChanged can Qt.callLater(jsFunc) with
invalid scope object
* QTBUG-125341 QML_CONSTRUCTIBLE_VALUE has a strange strategy to select
the right constructor
* QTCREATORBUG-31102 qmlls syntax highlighting differs from the built in
one
* QTBUG-127467 QtAbstractItemModel asserts when being rapidly modified
* PYSIDE-2803 pyside6-deploy throws a "command line is too long" error.
* QTBUG-127756 Add support for popup window types in the how-to-qml test
* QTBUG-127691 qmllint: don't print duplicate warnings
* QTBUG-124345 QML ObjectModel: Following the documentation for append
will lead to app crash
* QTBUG-127562 qmllint wrongfully complains about tumbler attached
property
* QTBUG-123491 qmlls memory leak
* QTBUG-127848 QML embedding: qtabstractlistmodel_kotlin &
qtabstractitemmodel_java look off on low and high pixel density displays
* QTBUG-124280 QML embedding example Java part doesn't look good on low
pixel densities
* QTBUG-124922 The text in a TextEdit is not updated when
LayoutMirroring is enabled
* QTBUG-107493 Reword debug log messages for QML import statements
* QTBUG-128321 tst_QQuickPopup::Basic::popupWindowFocus() failed on
Ubuntu 24.04 arm64 offscreen
* QTBUG-128173 Doc: Remove use of defunct QDoc command
"\tableofcontents"
* QTBUG-96630 MenuItem mnemonic shortcut not triggered
* QTBUG-128368 Make sure that also qt6_ CMake commands are in the help
index
* QTBUG-127950 Qt policy QTP0004 is not set: You need qmldir files for
each extradirectory that contains .qml files for your module
* QTBUG-128606 CMake Error: The inter-target dependency graph contains
the following strongly connected component (cycle)
* QTBUG-36525 Binding loop warning message does not give sufficient
information in order to fix it
* QTBUG-127661 Creator jumps to auto generated file instead of the real
one
* QTBUG-123396 MultiEffect shadowColor cannot be used for glow
* QTBUG-128417 Update QtGP version in examples & QtTAS

### qtactiveqt
* QTBUG-122762 [Reg 5.15 -> 6.5] ActiveQt server does not return
QVariantList properly
* QTBUG-126518 Qt 6.8 qutlook example does not build with 6.8.0 Beta1
* QTBUG-123533 dumpcpp generates code that does not compile
* QTBUG-127510 SCARY QDebug::toString() terrifies tests that compare
Microsoft::WRL::ComPtr
* QTBUG-128173 Doc: Remove use of defunct QDoc command
"\tableofcontents"
* QTBUG-127947 Active Qt landing page is missing license text
* QTBUG-111760 target_link_libraries(foo INTERFACE Qt::Core) fails for
interface libs with CMake < 3.19 on Windows

### qtmultimedia
* QTBUG-118573 Android tests on CI part 3/3 (screen/window capture)
* QTBUG-118839 [DeclarativeCamera] The app crashes when unlocking the
screen on Android
* QTBUG-113616 Android: Crash when mapping QVideoFrame object
(minimize/restore)
* QTBUG-116519 [Reg 6.2 -> 6.5] Repeated QSoundEffect is broken on
PulseAudio
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
* QTBUG-120465 QML Camera unloading crash on iOS
* QTBUG-121187Spectrum App Crashes after recording sound in "Record
and Playback" Mode
* QTBUG-120026 Retrieving videoDevices blocks main event loop
* QTBUG-119737 MediaRecorder.isAvailable not defined
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
* QTBUG-121221Camera Example - Recording Denied with "Invalid
Argument" Error
* QTBUG-113317 QVideoWidget rendering video incorrectly on macOS
Monterey
* QTBUG-121943 QPlatformMediaDevices is accessed before main on Android
* QTBUG-122640 QtMultimedia plugins are not deployed to Android .apks
* QTBUG-122193 QSoundEffect hangs on Loading
* QTBUG-122638 [gstreamer] deadlock when switching camera
* QTBUG-122706 onBufferProgressChanged not emited at all
* QTBUG-122750 [Regression] QSoundEffect cuts audio with FFmpeg backend
* QTBUG-121678 eglfs: Capturing the screen crashes on a Qt Quick
application
* QTBUG-122753 Qt Multimedia: implicit instantiation of undefined
template 'std::char_traits<unsigned char>' (libc++ 19 / musl libc /
amd64)
* QTBUG-121182 QML Video Example: Simultaneous videos playback crashes
the App on Android
* QTBUG-122649Playing multiple videos simultaneously fails for the
second video with the FFMPEG backend on Android.
* QTBUG-122199 [ffmpeg] player crash in libavcodec if libnvidia-decode
is not installed
* QTBUG-122608 [REG 6.6.1-6.6.2] [windows] QMediaPlayer failed to set
topology on custom QVideoSink
* QTBUG-122817 [REG 6.6.1-6.6.2] [windows] QML MediaPlayer unable to
play a video when 'audioOutput' is not specified
* QTBUG-98437 QMediaPlayer does not emit destroyed signal
* QTBUG-122887 Android: MediaPlayer: AudioOutput via HDMI not possible
* QTBUG-122959 GStreamer: "stop camera" does not stop camera
* QTBUG-123105 ror: no matching conversion for functional-style cast
from 'const char[5]' to 'QStringView'
* QTBUG-122575 Mediaplayer example not showing video on some Android
emulators
* QTBUG-112312 QFFmpeg EGL VAAPI failures
* QTBUG-123117 MediaPlayer crashes on seek after loop reset.
* QTBUG-123312 [gstreamer] video playback broken with gstreamer older
than 1.20
* QTBUG-123205 Allow defining platform specific gstreamers
colorconversion-plugins
* QTBUG-119583 ScreenCapture-Graphic&Multimedia- Issue when a captured
window is being closed
* QTBUG-123139 GStreamer: Qt Camera in stops after switching VideoOutput
* QTBUG-113421 Qt Camera in QML Dies after closes the drawer with Camera
* QTBUG-122968 QML Camera: Using zoom and switching cameras breaks the
example
* QTBUG-119350 QML Camera zoom goes out of the screen on some Android
devices
* QTBUG-120266 [Windows] App hangs on destroying QML Video component
during video playback
* QTBUG-123131 Modified video frames are not updated for rendering
* QTBUG-123215 fatal error: qplatformmediadevices_p.h: No such file or
directory when building from source for Qt 6.6.2 on Windows
* QTBUG-122184 [Crash] The 'Widgets camera' app crashes on Android when
starting and stopping the video recording
* QTBUG-123045 [Examples] Qt warning on changing audio input in Audio
Source example
* QTBUG-123597 QAudioDecoder crashes on files without audio track
* QTBUG-123451 Incorrect frame rate selectiion for QCamera on iOS
* QTBUG-123526 No video input devices with QT_MEDIA_BACKEND set to
ffmpeg
* QTBUG-123899 [GStreamer] createVideoProfile unit test failure
* QTBUG-123997 Public ABI breakage between 6.6 and 6.7 for
QAudioSink::stateChanged(QtAudio::State)
* QTBUG-124115 QtMultimedia configure fails for GPU-less yocto target
* QTBUG-123967 QML media player example project fails to play AV1
encoded videos.
* QTBUG-120671 User control issues in QML Media Player with WASM
* QTBUG-119914 VideoSink frame to image does not work on android
* QTBUG-117771 Qt6.5.3 QMediaPlayer play video an error on android 11
* QTBUG-124253 Direct3D debug layer reports error when playing videos of
same size and pixel format
* QTBUG-120567 Incorrect interactions between QML Camera and
CameraPermission
* QTBUG-123904 [gstreamer] tst_QMediaCaptureSession::testAudioMute test
failure
* QTBUG-112316 wasm: declarative-camera fails to show camera
* QTBUG-123905 [gstreamer]
tst_QMediaCaptureSession::stress_test_setup_and_teardown test failure
* QTBUG-120622 Recorder sample app does not work as expected with
WebAssembly
* QTBUG-118072 MediaPlayer with VideoOutput doesn't autoplay
* QTBUG-120963 QScreenCapture/QWindowCapture with HDR shows dark scene
* QTBUG-123447 Incorrect log format in qaudioengine_pulse.cpp
* QTBUG-121172 [REG 6.5.5 - > 6.5.6] Declarative Camera: Black Screen
Issue when Clicking "View" Button in Video Mode
* QTBUG-124414 [gstreamer] MediaPlayer emits BufferedMedia in
StoppedState
* QTBUG-124415 [gstreamer] MediaPlayer emits too many state change
signals
* QTBUG-122140 The video freezes when recording it with higher
resolution in widgets camera example
* QTBUG-124182 [gstreamer] tst_QCameraBackend::testNativeMetadata test
failure
* QTBUG-124776 [gstreamer] uridecodebin with https source spurious
playback failure
* QTBUG-124431 When using QMediaRecorder or QAudioInput with alsa it
chooses the wrong Endianess with ALSA audio
* QTBUG-124544 [gstreamer] duration is not extracted from metadata
* QTBUG-125080 [gstreamer] audio io crashes with FEATURE_alsa
* QTBUG-124615 Top flaky test: tst_qmediaplayerbackend::play_createsFram
esWithExpectedContentAndIncreasingFrameTime_whenPlayingRtspMediaStream
on MacOS_14 ARM64, MacOS_12, MacOS_13, Ubuntu_22_04, openSUSE_15_5.
* QTBUG-125006 MediaPlayer fails to play rpt video stream using sdp
file.
* QTBUG-124298 [iOS] Loading a new sound stops the play for other sounds
* QTBUG-123044 android: Playing something through QMediaPlayer and
adjusting volume from physical buttons shows wrong mode
* QTBUG-124189 tst_qcamerabackend: crash on exit
* QTBUG-122118 QML Camera Application Example does not work with Android
11 device
* QTBUG-119472 Camera with ffmpeg backend freezes the application
* QTBUG-124228 [gstreamer]
tst_QMediaCaptureSession::can_change_CameraDevice_on_attached_Camera
crashes sometimes
* QTBUG-125397 [gstreamer] setPlaybackRate has no effect before play()
* QTBUG-125552 Document dynamic linking of FFmpeg with Qt Multimedia on
macOS and Windows
* QTBUG-124537 YUYV format from QCamera is buggy
* QTBUG-124534 heap overflow in planarYUV420_to_ARGB32
* QTBUG-123749 QVideoFrame::toImage gives corrupt images when no RHI
backend is present
* QTBUG-125632 wasm: Cannot play video in Firefox
* QTBUG-125213 Flaky crashes on ASAN-compiled tst_qsoundeffect
* QTBUG-119102 Cannot record video using QML or widgets camera example
on macOS with built-in camera or iOS device continuity camera
* QTBUG-125389 Deadlock during destruction in
tst_QMediaCaptureSession::testAudioMute
* QTBUG-126119 Test #43: tst_qmediacapturesession .........***Failed
* QTBUG-125957 Lost last frame when encoding custom video frames
* QTBUG-126203 [darwin] MediaPlayer does not always take into account
the selected audio output device
* QTBUG-123220 Green Line Artifact in QML VideoOutput component
* QTBUG-118571 Android tests on CI part 1/3 (camera & media
capture/player)
* QTBUG-126449 qmltyperegistrar: Build time warnings for qtmultimedia
* QTBUG-113399 QVideoSink with Qt 6 on Android ignores requested camera
settings
* QTBUG-121452 Qt ScreenCapture Example Fails to Capture Screen Content
* QTBUG-114674 Audio fails silently on iOS 16 following app suspended
* QTBUG-124396 [Boot2Qt] "The wayland connection broke" when running
audioooutput example app
* QTBUG-122635 QML video example crashes immediately after launch,
because of missing qmlvideo module
* QTBUG-124925 [REG 6.5.5 -> 6.5.6] Spectrum App Crashes after recording
sound in "Record and Playback" Mode
* QTBUG-126254 [darwin] Camera example crashes when recording with
webcam, "AudioChannelLayout is invalid"
* QTBUG-126958 avfvideorenderer control - don't use invalid pointers
* QTBUG-126988 [macOS] QAudioSource::start returns invalid pointer if
start failed
* QTBUG-122104 Missing Info.plist in audio devices example does not
allow using the application on macOS
* QTBUG-126968 wasm: MediaPlayer won't work if source is set at creation
* QTBUG-126192 ios: Zoom factor does not notify changes and cannot zoom
back to 1.0
* QTBUG-126817 Qt6MultimediaConfig.cmake fails due to missing FFmpeg
* QTBUG-126428 Android: Regression with playing video (H.264)
* QTBUG-116766 [Boot2Qt] List of cameras should contain only available
(connected) ones
* QTBUG-124206 [GStreamer]
tst_QAudioDecoderBackend::play_emitsFormatError_whenMediaHasNoAudioTrack
does not report errors
* QTBUG-127453 WASM: seekableChanged is not firing
* QTBUG-127675 Spurious assertion failure in
tst_QSoundEffect::testSetSourceWhilePlaying
* QTBUG-127320 QMediaPlayer unable to open files with absolute paths
without scheme
* QTBUG-127533 Android front face camera upside down / not mirrored
* QTBUG-128264 (No such file or directory):
/home/qt/work/qt/3rdparty/ffmpeg/qt_attribution.json
* QTBUG-127494 [WASM] Multiple VideoOutputs cannot play independently
* QTBUG-127745 tst_qvideoframecolormanagement failed on Ubuntu 24.04
offscreen(arm64)
* QTBUG-127744 tst_qvideoframe failed on Ubuntu 24.04 offscreen(arm64)
* QTBUG-127746 tst_qmediaplayerbackend failed on Ubuntu 24.04
offscreen(arm64)
* QTBUG-127784 Inaccurate color handling when no RHI backend is
available
* QTBUG-128246 QMultimedia UYVY rendering is in lower image quality
* QTBUG-125901 IOCTLcall on VIDIOC_ENUM_FRAMEINTERVALS fails to
enumarate frame interval/rate for FFmpeg V4L2 cameras
* QTBUG-127681 Spurious crash in
stressTest_setupAndTeardown_keepAudioOutput on android
* QTBUG-128759 [REG 6.7.2->6.7.3] change in configure options, gstreamer
on LoA
* QTBUG-128335 Error messages are invisible in media player error dialog
on Windows
* QTBUG-125356 multimedia/screencapture/CMakeLists.txt is missing
INSTALL_EXAMPLEDIR
* QTBUG-127853 Use cmake's ability to embed frameworks/dylibs (ffmpeg on
iOS)
* QTBUG-117099 Video jerks when playing (Windows backend)
* QTBUG-117746 eglfs: Capturing the screen crashes
* QTBUG-117878 Cannot capture screen from QQuickWidget
* QTBUG-111045 QSoundEffect not playing
* QTBUG-118099 Volume Discrepancies Between QMediaPlayer and
QSoundEffect with ffmpeg
* QTBUG-111815 Bumpy rendering of D3D11 textures
* QTBUG-111459 Heavy jittering in video playback if animations are
active
* QTBUG-109213 Video flickering when there is a ParticleSystem component
or playing some animation at same time
* QTBUG-121750 QCameraImageProcessing fails to set settings on linux
v4l2 camera
* QTBUG-116324 Request to implement thumbnail realization for multimedia
FFMPEG backend
* QTBUG-122577 QScreenCapture tests are flaky on OpenSuse 15.5
* QTBUG-108754 Video not stretched properly
* QTBUG-111190 V4L2m2m encoder gets failed on linux
* QTBUG-122224 [Crash] The audiorecorder example crashes when selecting
output and start recording
* QTBUG-87969 MediaPlayer looses current position when playbackRate
changes
* QTBUG-123356 ERROR: Crash detected
* QTBUG-123224 tst_qmediacapturesession crashes in
CI(opensuse-15.5-host-asan)
* QTBUG-123023 [Examples] Audio input devices list is not updated when
connecting new device
* QTBUG-123459 [gstreamer] player example does not update "Buffering"
percentage
* QTBUG-119535 [Boot2Qt] Switching between audio output devices while
playing video causes the player app to freeze
* QTBUG-123177 OpenSUSE crash in tst_QMediaCaptureSession with
PulseAudio
* QTBUG-113627 D3D11 Removing Device on QVideoSink save frame
* QTBUG-96985 Video and MediaPlayer don't allow to use relative URLs
* QTBUG-123931 With gstreamer as backend, playing mp4 file resulted in
internal data stream error
* QTBUG-124501 [gstreamer] media player does not play without outputs
connected
* QTBUG-124183 [gstreamer] tst_QCameraBackend::testNativeMetadata test
failure due to duration timeout error
* QTBUG-124647 YUYV and UYVY pixel formats are not rendered correctly
with FFmpeg backend
* QTBUG-124586 QML video media player segmentation fault on AMD GPU with
FFMPEG
* QTBUG-125251 [gstreamer] spurious assertion failure on shutdown
* QTBUG-125956 Unit testing of new APIs
* QTBUG-124725 [Camera] The video recorded with webcam on macOS is
corrupted - it only displays green flashing noise
* QTBUG-125613 Investigate lacking video format support on Android 14
with FFmpeg media player
* QTBUG-117888 Wide camera is not supported?
* QTBUG-122757 FFmpeg+Intel VAAPI decoding of certain h264/mp4 videos
fails in 6.6.x+
* QTBUG-126106 QVideoFrames sent to QML as signal arguments are
deallocated too late
* QTBUG-126143 QMediaFormat on Linux does not show MP3
* QTBUG-126799 [gstreamer] playback rate / seeking unreliable
* QTBUG-123056 GStreamer: `setLoops` sometimes not working
* QTBUG-127031 [QMediaPlayer] switching video output while playback is
paused does not update new sink
* QTBUG-126014 [ffmpeg] setVideoOutput/setAudioOutput while playing
seems broken
* QTBUG-127346 [gstreamer] QMediaPlayer: subsequent playback broken
* QTBUG-127484 CMake Error if gstreamer_gl_wayland (or gl_x11) feature
is enabled
* QTBUG-95952 Seemingly unnecessary check for pulse-mainloop-glib
* QTBUG-127137 [ffmpeg, macos]
tst_QMediaPlayerBackend::stressTest_setupAndTeardown crashes on CI
* QTBUG-127733 tst_QAudioSink::pullResumeFromUnderrun() failed on Ubuntu
24.04 offscreen and X11
* QTBUG-127927 [gstreamer] record_video_without_preview assertion
failure on CI
* QTBUG-118594QML Camera wrong Orientation on iOS
* QTBUG-128336 Camera widget example does not record audio with default
AAC format
* QTBUG-118877 -qreal float configuration option does not compile
* QTBUG-112014 QMediaPlayer hangs up on setPosition(...) when using
gstreamer backend
* QTBUG-124372 After seeking using the GStreamer backend, the stream
goes into a paused state.

### qttools
* QTBUG-119555 [REG] Qt 6.6.1 breaks qt_add_translations
* QTBUG-115166 qt_add_qml_module() causes non-Ninja generators to think
that projects are never up-to-date
* QTBUG-77650 qdoc's --outputdir argument usage is not intuitive
* QTBUG-120265 QDoc incorrectly generates list of types for
\compareswith
* QTBUG-119999 Failed links are always reported as originating from the
beginning of the documentation comment
* QTBUG-121226 qdoc extraimages.HTML not supported
* QTBUG-121377 Dependency update on qt/qttools failed
* QTBUG-118808 qt_add_translations with source autodetection mishandles
id-based generated UI headers
* QTBUG-121186 New QSharedPointer methods do not show up under "New
Classes and Functions"
* QTBUG-121563 bad license identifier in qttools/src/qdoc/qdoc/tests/gen
eratedoutput/testdata/templatedcallables/templated_callables.*
* QTBUG-121774 QDoc: May generate incorrect file names for examples in
specific conditions
* QTBUG-121850 QDoc: SHA1-files generated for QHP files differ across
platforms
* QTBUG-121855 missing RHI related headers (class documentation is
wrong)
* QTBUG-109214 Documentation for QtAndroidPrivate is still wrong for
CMake
* QTBUG-118990 assistant.exe index navigation fails
* QTBUG-122418 qdoc: validatedqdocoutputfiles test fails address
sanitizer check
* QTBUG-121378 Ignore \deprecated [x.y] if x.y is a future version
* QTBUG-120323 qdoc: Document \attribution command
* QTBUG-122994 [Reg 6.6.1->6.6.2] Performance regression in
qhelpcollection.cpp
* QTBUG-123034 Accidental strikethrough (&lt;s&gt;) in QSpan documentation
* QTBUG-123011 wrong xxx_lupdate_project.json is generated when no
targets are specified in qt6_add_lupdate
* QTBUG-123109 qdoc fails to compile with clang 18
* QTBUG-123338 cmake translation handling not backwards compatible
* QTBUG-123405 [REG 6.6 -> 6.7.0 RC] Translations were generated in the
wrong folder
* QTBUG-122261 CMake Property Reference: duplicate anchors
* QTBUG-123622 QDoc: Issues with generating output from qtglobal.cpp
* QTBUG-123995 CMake error "Too many parentheses." on qt_add_lupdate
* QTBUG-119515 QHelpEngineCore::setReadOnly does not close the
connection
* QTBUG-124188 [REG 6.6 -> 6.7] Automatic resource embedding path of
qt_add_translations() has changed from Qt 6.6 to Qt 6.7
* QTBUG-125066 Configure fails in qttools if PrintSupport is disabled
* QTBUG-120751 error: ‘DeviceProfileDialog’ in namespace
‘qdesigner_internal::Ui’ does not name a type
* QTBUG-115448 qttools -unity-build-batch-size 100000 fails
* QTBUG-119469 Targets not yet defined: zstd::libzstd_static
* QTBUG-125983 Reg->6.7.1: Qt Designer: Can no longer change int
properties
* QTBUG-125969 [REG 6.2->6.3] qdoc: \target and \keyword within \fn
topic not written to index
* QTBUG-126116 tst_validateQdocOutputFiles fails on AddressSanitizer
* QTBUG-126182 Qt Designeron archlinux always crash when edit an *.ui
file
* QTBUG-126189 [REG 6.7.1->6.7.2&6.8.0] lconvert, lrelease, lupdate and
few others not combiled in no-gui build
* QTBUG-126167 CMake fails to configure simple project
* QTBUG-126139 Linguist shipped with Qt6 breaks how language tag is
handled
* QTBUG-126088 qdoc: Protect \trademark from translations
* QTBUG-126152 qdoc: Macro arguments cannot contain formatting commands
* QTBUG-126274 [REG: 6.7.1->6.7.2] Windows/Win11/Vista styles: designer:
Spinbox values are shown doubled
* QTBUG-125310 tst_lupdate asserts on mingw13
* QTBUG-101446 QT/LLVM RTTI settings - Undefined reference to `typeinfo'
when compiling Qt Everywhere from source
* QTBUG-126960 qdoc: No warning generated for a missing qhp subproject
index title
* QTBUG-127052 qt_add_translations does not add the generated .ts files
to the source list of the target
* QTBUG-127056 qt_add_translations has no way of returning the
automatically determined .ts file paths
* QTBUG-61277 Doc: Some modules missing from "All QML Modules" page
* QTBUG-127146 [REG 5.15 -> 6.0] TR_EXCLUDE became too strict
* QTBUG-124200 Linguist 'does not know the plural rules for Luganda'
* QTBUG-27936 Regression: lupdate is very very slow
* QTBUG-127513 qttool: depends on network-support, but should only be
optional
* QTBUG-127564 qdoc: qhp group: selector does not work for groups
without a \group page
* QTBUG-127630 qdoc crashes when building Qt Creator developer
documentation
* QTBUG-127789 Generated TS files are missing the language and
sourcelanguage attributes
* QTBUG-127792Generated TS file with plural forms contain incorrect
<numerusform> entry count
* QTBUG-127828 qt_add_translations: TS_FILE_DIR is ignored when
PLURALS_TS_FILE set
* QTBUG-127841 Windows ARM: qttools - tst_lconvert::initTestCase() fails
* QTBUG-128186 qlitehtml is built in a directory called "value-NOTFOUND"
* QTBUG-126994 [DocBook] Too much escaping in code
* QTBUG-128411 Remove 'corefeatures.html' from qdoc manual
* QTBUG-124709 Linguist examples pollute the source tree with *_en.ts
files
* QTBUG-128356
https://doc.qt.io/qt-6/qscreen.html#physicalDotsPerInchChanged missing
an entry?
* QTBUG-128644 QDoc fails to compile against Clang-19 RC1-RC4, Clang 20
* QTBUG-128926 QDoc: When linked against clang from LLVM 19, QDoc
segfaults when generating qt3d documentation
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
* QTBUG-116599 qttools: race condition in test_translation_api CMake
test
* QTBUG-122691 Dependency update on qt/qttools failed in 6.7
* QTCREATORBUG-30427 Crash in help
* QTCREATORBUG-30459 [REG 12.0.2 -> 13.0] Help mode resizes incorrectly
* QTBUG-123611 libclang15-based lupdate fails with MSVC2022
* QTCREATORBUG-30625 [Reg 12 -> 13] Help: links to QML properties do not
work anymore
* QTBUG-119429 Top flaky test: tst_lupdate::good on Windows_11_22H2,
Windows_11_23H2, and Windows_10_22H2.
* QTBUG-125076 [Reg 6.5->6.7.0] Doc for QQuickItem no longer says
"Instantiated by: Item"
* QTBUG-127352 lupdate's -extension option doesn't work
* QTBUG-123130 QDoc with Clang 18 drops `noexcept` specifier from
compiler generated methods documented with \fn
* QTBUG-80417 QDateTimeEdit cannot handle OffsetFromUTC or TimeZone as
time-spec
* PYSIDE-2492 uic does not generate enumeration name into enum values
causing type checking warnings
* QTBUG-127179 Qt Creator puts wrong fields for spacer objects
* QTBUG-127751 tst_lupdate failed on Ubuntu 24.04 offscreen(arm64)
* PYSIDE-2840 Enum properties unsupported in Qt Designer custom widgets
* QTBUG-128173 Doc: Remove use of defunct QDoc command
"\tableofcontents"
* QTBUG-128368 Make sure that also qt6_ CMake commands are in the help
index
* QTBUG-128424 Warning messages during configure are not helpful
* QTBUG-128365 Wrong "Line"(QFrame) orientation

### qtdoc
* QTBUG-119996 Demo hangman don't work on Qt6.7
* QTBUG-117090 CMake docs: incorrect code example for
qt_generate_qml_app_script
* QTBUG-119175 [DocumentViewer] The app crashes when opening 3d model
file (obj)
* QTBUG-120372 Typo in the document
* QTBUG-119458 Initializing with QQuickView is missing cmake instruction
* QTBUG-120230 'coffee' fails when cross-compiling on Windows
* QTBUG-120364 [6.7 beta1] Qt Dice demo crashes on Android devices
* QTBUG-120471 Fix minor issues in stocqt
* QTBUG-121165 Error in WebAssembly documentation
* QTBUG-112024 Robotarm fails to launch on embedded devices
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
* QTBUG-122178 [Media Player Example] App hangs when previous track is
clicked
* QTBUG-122767 QTP0001 warning for FX & Material Showroom example
* QTBUG-122569 Calqlatr example package name not unique
* QTBUG-122444 Qt Dice Example: The control menu's lower half is cut off
in landscape mode
* QTBUG-123164 New example demos/osmbuildings not compiling on Android
* QTBUG-121144 Dice example: text not centered
* QTBUG-122907 Show real time data for lighting viewer (or document that
it is demo data)
* QTBUG-124146 [demos/hangman] Clicking on the vowels button crashes the
demo
* QTBUG-123414 Coffee Machine Example calculates its initial size too
big in case of two monitors on macOS
* QTBUG-123305 Incorrect link
* QTBUG-122605 Calqlatr example landscape grid buttons not showing
symbols correctly
* QTBUG-122682 "Porting to iOS" documentation only mentions qmake, not
CMake
* QTBUG-123714 [REG 6.7.0 beta3 -> beta4] demos/calqlatr not launching
when building with qmake
* QTBUG-122273 [MediaPlayerApp] The file names on the playlist in the
app have specific format on Android
* QTBUG-124707 Coffee Machine example coffee cup image breaks with Qt
6.7.0 on Android
* QTBUG-124844 Invalid plural form qsTr example
* QTBUG-125057 [DocumentViewer] Printing becomes inactive after loading
txt file
* QTBUG-126104 Android mobile examples link redirects to WASM page
* QTBUG-126019 Clean up What's new in Qt 6.8 page
* QTBUG-124144 No buildings in osmbuildings - example
* QTBUG-126273 Two conflicting pages for 'Inter-process Communication'
* QTBUG-55199 macdeployqt does not copy SVG image format plugins
* QTBUG-126517 Qt 6.8 stocqt example does not show its content
* QTBUG-126578 Fix warnings of StocQt
* QTBUG-122683 Update trademark information
* QTBUG-127547 The link in INTEGRITY doc leads to Qt for wasm doc
* QTBUG-126866 Archiving the application does not have debug info files
(dSYM) included as expected
* QTBUG-127814 Calqlatr fails to remove the unary minus character
* QTBUG-127835 demos/lightningviewer not launching when installed
outside of build dir
* QTBUG-128225 Failing to deploy examples that link to dynamic lib qml
modules, but don't explicitly import them
* QTBUG-127989 [Regr: 6.7.2 -> 6.8.0-beta2] Build fails with MinGW
* QTBUG-128399 Add a link to What's New at the top of a landing page of
a Qt release
* QTBUG-118038 Qt6WaylandCompositor could not be found because
dependency Wayland could not be found
* QTBUG-122041 [DocumentViewer] The app is crashing when opening the
file on Android device
* QTBUG-128351 car-configurator: Runtime warnings
* QTBUG-127851 Car rendering example breaks qtdoc builds with examples,
if CMake version is below 3.21.1
* QTBUG-128729 qtdoc module fails yocto build
* QTBUG-128673 [DocumentViewer] The app crashes on Linux when asserting
an instance of RuntimeLoader QML Type
* QTBUG-128436 new ARM-based desktop platforms are not mentioned in
What's New
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
* QTBUG-122646 6.8.0 sources having 6.7.0 version strings
* QTBUG-123543 Incomplete docs about the status of Linux on ARM desktops
in 6.7
* QTBUG-124518 The debian packages documentation has incorrect example
* QTBUG-123445 Weird beheaviour of and errors on the console from the
"Coffee Machine" example
* QTBUG-126094 Spelling of Qt Qml/QML very inconsistent
* QTBUG-125329 Grpc generators: fix Policy CMP0071
* QTBUG-100100 Demos should use `qt6_add_qml_module` instead of
`qt6_add_resources`
* QTBUG-124657 qsTrNoOp() is not defined in QML
* QTBUG-126201 Qt examples output CMake warning about Qt policy QTP0004
* QTBUG-127560 maroon demo lags when enabling sounds
* QTBUG-127736 6.8.0 sources having 6.7.0 version strings (debian-
packages.qdoc)
* QTBUG-127926 Outdated Android docs still refer to
QtAndroid::androidActivity()
* QTBUG-123315 [REG 6.6.1 -> 6.6.2] Run time errors from coffee demo
* QTBUG-128278 Incorrent and incomplete statements about using compiled
QML
* QTBUG-128173 Doc: Remove use of defunct QDoc command
"\tableofcontents"
* QTBUG-128678 Reintroduce support of iOS 16
* QTBUG-92811 Misleading identification of third party tool

### qtlocation
* QTBUG-121766 GeoJsonViewer example cannot open files.
* QTBUG-123112 GeoJson Viewer example doesn't show maps on Android
* QTBUG-121412 Make sure that QtLocation examples use new QPermissions
API
* QTBUG-128173 Doc: Remove use of defunct QDoc command
"\tableofcontents"

### qtpositioning
* QTBUG-106049 Qt Android's QGeoCoordinate API returns altitude in wrong
reference frame
* QTBUG-119477 SatelliteInfo example crashes
* QTBUG-115933 [QtPositioning] geoclue2 backend crashes randomly
* QTBUG-121997 BUS ERROR in examples/positioning/satelliteinfo on
aarch64
* QTBUG-127847 QtPositioning Android backend always checks for precise
location

### qtsensors
* QTBUG-110806 license discrepency?
* QTBUG-128173 Doc: Remove use of defunct QDoc command
"\tableofcontents"

### qtconnectivity
* QTBUG-119060 Read access violation when calling stop() during
Bluetooth service discovery
* QTBUG-119063 Segfault in Bluetooth module's Windows COM de-init
* QTBUG-120410 NDEF Editor Example - Clicking on 'read tag' will erase
existing records
* QTBUG-82413 Cannot connect to a second Bluetooth device
* QTBUG-124650 Missing BLE 5.x Extended Advertisements for Windows
* QTBUG-127407 annotatedurl example build failing
* QTBUG-127110 Platforms still use the inefficient qvsnprintf() fall-
back
* QTBUG-123430 QBluetoothSocket::errorOccured is not emitted in certain
circumstances
* QTBUG-128173 Doc: Remove use of defunct QDoc command
"\tableofcontents"

### qtwayland
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
* QTBUG-120950 QtWayland: Vulkan window mouse request move areas is
error
* QTBUG-111576 Wayland client leaks memory
* QTBUG-120533 Various runtime warnings about Wayland text input
* QTBUG-121364 FAIL!: appman-qmltestrunner::ApplicationManager::test_s
tartAndStopApplication(StartStop)
* QTBUG-121399 tst_QWizard::task177022_setFixedSize() failed on Wayland
* QTBUG-116600 The Virtual keyboard is not hidden when the TextField
loses focus on the Wayland client.
* QTBUG-78317 tst_seatv4::animatedCursor() failed on linux qemu
* QTBUG-122965 Qt 6.5.4 don't generate XDG_RUNTIME_DIR
* QTBUG-123007 Under Wayland Qt does not correctly handle key modifiers
during key repeating
* QTBUG-107858 qtwayland caches clipboard content
* QTBUG-122412 Buggy rendering on RHEL 8 with 200% system scaling
* QTBUG-120070 Missing support for better GNOME-like client-side
decorations
* QTBUG-97037 DragHandler / startSystemMove window move issue with QT6
Webengine on Wayland
* QTBUG-123489 Qt Wayland Client requires QtGui to be build with support
for wayland
* QTBUG-124259 Top flaky test:
tst_xdgdecorationv1::clientSidePreferredByCompositor on openSUSE_15_5
X86_64.
* QTBUG-124304 [REG 6.7.1-> 6.7.0] no-gui (-DFEATURE_gui=OFF) build
fails, qtspeech
* QTBUG-118813 Window modal dialogs can go behind their parent dialogs
with XdgShell
* QTBUG-124807 Horizontal scrolling not working under Wayland with
Alt+Wheel
* QTBUG-124284 Client-side decorations don't work on systems without
working OpenGL drivers
* QTBUG-124285 Qt on Wayland accesses OpenGL drivers in pure QtWidgets
applications
* QTBUG-119377 qmllint warnings with wayland shell types
* QTBUG-124839 Ctrl+Tab popup list of documents rendered behind main
window on Plasma 6 Wayland
* QTBUG-121551 Qt virtualkeyboard cannot compose Korean on text-input-v3
* QTBUG-125872 Windows are blurry with 200% scaling on Ubuntu 22.04 with
dev branch
* QTBUG-124502 Drag and drop operation can crash the compositor
* QTBUG-126275 [REG Qt 6.6.3 -> 6.7.0] Wayland: Can't scroll with
mousewheel in editor
* QTBUG-126262 ERROR: AddressSanitizer:tst_surface heap-use-after-free
* QTBUG-118640 Qt sends the pointer event serial instead of the tablet
event serial in data_device:start_drag or xdg_toplevel::move.
* QTBUG-125878 Cannot pinch-to-zoom after the qt 6.7.1 upgrade
[regression]
* QTBUG-126313 QScroller gesture blocks mouse clicks
* QTBUG-113404 Wayland: Gestures are not delivered to correct top level
widget
* QTBUG-122197 QScreen::size is wrong on GNOME Wayland with 200% scaling
* QTBUG-127487 Touch Dragging on minimal-qml wayland compositor does not
work
* QTBUG-117920 Unable to move/resize/close Qt Application using a wacom
tablet stylus in GNOME Environment
* QTBUG-127301 Clipboard cannot be changed from compositor if client has
copied something
* QTBUG-120035 [weston] Setting fixed size for the main level widget
crashes the application when maximized
* QTBUG-95817 Quick windows breakon nvidia wayland when resized
* QTBUG-100148 Hover state of QCombobox has not been reset
* QTBUG-121446 text input : mismatch between QString and byte counts in
protocols
* QTBUG-124265 configure -qpa "wayland;xcb"
* QTBUG-87805 Port mkspec QT_QPA_DEFAULT_PLATFORM mechanism to CMake
* QTBUG-125589 weired console message with simple application
* QTBUG-118877 -qreal float configuration option does not compile
* QTBUG-112432 wayland plugin should distinguish touchpads from mice,
etc.

### qt3d
* QTBUG-119657 Double free with RHI resources while using Qt3D compute
* QTBUG-77665 Phong fragment shader does not account correctly for
ambient color
* QTBUG-120241 Incorrect handling of ambient color in phong shaders in
qt3d (Regression)
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
* QTBUG-124708 QText2DEntity jagged text when using RHI OpenGL backend
* QTBUG-120472 [Qt3D] PointLineSize example produces an error
* QTBUG-69463 Camera view matrix computation unstable (regression)
* QTBUG-123483 Qt3D: Fix Stereo back buffer selection
* QTBUG-124907 fatal error: 'quick3daction_p.h' file not found
* QTBUG-124658 QAbstractCameraController documentation contains mistakes
* QTBUG-124891 Unredistributable files in qt3d / qtquick3d
* QTBUG-126251 Render to Texture broken following stereo rendering fixes
* QTBUG-128939 [REG 6.8.0 RC snapshot -> 6.8.0 RC snapshot]
Unredistributable files in qt3d

### qtimageformats
* QTBUG-118797 ICNS format: QImageReader::setAllocationLimit() bug
* QTBUG-113349 [static linking] duplicate symbol with QIIOFHelper
* QTBUG-127540 WebP: QImage detach in WebPPictureImportRGB(A) can cause
a crash
* QTBUG-127965 QImage not loading simple heic file

### qtserialbus
* QTBUG-114397 QCanDbcFileParser will not parse signals with certain
valid utf-8 encoded characters
* QTBUG-123012 vectorcan can not set the DataBitRateKey and the
BitRateKey

### qtserialport
* QTBUG-120412 Blocking receiver example - Will crash when clicking
'start' if no Serial port is selected
* QTBUG-128748 Unused static functions in qserialport_p.h

### qtwebsockets
* QTBUG-123346 Expired (and near-expiring) certificates shipped with
examples
* QTBUG-120492 QWebSocket connecting to an URL without a path sends GET
request without leading /
* QTBUG-110025 Android tests aren't bundling OpenSSL for any test

### qtwebchannel
* QTBUG-119303 WebChannel 'standalone' application does not build with
non-shadow build dir

### qtwebengine
* QTBUG-119789 [Accessibility] Qt 6.5.3 cannot be built with the option
' -no-feature-accessibility''.
* QTBUG-112142 [Qt WebEngine] ScreenCapture should provide a way to
select window/screen to capture
* QTBUG-118120 qtwebengine: build failure with x86_64h
* QTBUG-120245 A crash occurred in C:\Users\qt\work\qt\qtwebengine_stand
alone_tests\tests\auto\pdfquick\multipageview\tst_multipageview.exe
* QTBUG-118398 QWebEngineView in QScrollArea is not scrollable
* QTBUG-119776 PDF Multipage viewer example - Clicking on previous
(upward arrow) will crash the example
* QTBUG-104767 Using PdfPageImage instead of Image on PDF file results
in EXC_BAD_ACCESS (SIGSEGV)
* QTBUG-120446 Alternated item color in list is not always alternated
* QTBUG-119722 [REG 5 → 6] Default context menu is missing icons
* QTBUG-86869 Unrecognized Chrome version when using Selenium and
Chromedriver
* QTBUG-118746 Japanese input on macOS regressed in Qt 6.5.3
* QTBUG-119245 Qt Web Engine alert quotes not working
* QTBUG-83338 Default implementations of javaScriptAlert/Confirm/Prompt
treat message as rich text
* QTBUG-119991 Unable to print at all if the first page of multi page
document is not printed
* QTBUG-120218 QML WebEngineView.printToPdf(): paper formats are wrong
in the resulting document
* QTBUG-115502 PdfMultiPageView: repeated pinch-zooming jumps to wrong
zoom level
* QTBUG-119416 Loading a specific page in a PDF document does not always
show the correct page
* QTBUG-121564 tst_MultiPageView::pinchDragPinch is flaky
* QTBUG-120689
tst_qwebenginepage::getUserMediaRequestDesktopVideoManyPages is flaky
* QTBUG-121502 crash in QPdfIOHandler if document is deleted too early
* QTBUG-85473 QML WebEngineSettings misses ScrollAnimatorEnabled but
QWebEngineSettings has it
* QTBUG-120273 QWebEngineView shows blank content on initial show when
page bg set to transparent
* QTBUG-121227 QWebEngineView shows blank content on initial show when
page bg set to transparent
* QTBUG-112013 QWebEnginePage.setBackground(Qt::black) doesn't work for
page loading.
* QTBUG-120926 QWebEnginePage::setBackgroundColor doesn't work properly
* QTBUG-122137 REG: QtWebEngine / Pdfwidgets no longer supports plugins
* QTBUG-122153 QWebEngineView::setFocus() doesn't give focus to the view
after calling QWebEngineView::load() for the second time
* QTBUG-92114 Shift-Tab moves focus forward instead of backward in
WebEngineView inside QQuickWidget
* QTBUG-121589 Can't build qt6 due to failed ozone platform assertion
* QTBUG-118035 QtWebengine build fails on pure wayland
* QTBUG-122997 The Spellcheck example doesn't work on macOS
* QTBUG-77450 Issues with clipboard permissions
* QTBUG-122655 6.8.0 toplevel build fails on macOS, qtwebengine
* QTBUG-123548 PDF multipage viewer converts a simple local filename in
the cwd to an http url
* QTBUG-120764 PDF Viewer Widget example search error
* QTBUG-106565 The coordinate of QPdfSelection seems like to be wrong
when pdf page contains non-displayable area
* QTBUG-100630 PdfLinkModel don't give the right rect everytime
* QTBUG-123765 Segfault when dropping elements from Spotify in Firefox
* QTBUG-120131 Auto-scrolling does not work with quicknanobrowser
example
* QTBUG-122916 Print preview: crash when pressing a resize button
* QTBUG-122970 Copying and pasting using shortcuts is not working in
MacOS
* QTBUG-124527 qtwebengine integrations fail on 6.7: qt-testrunner.py
ERROR: Full test run failed repeatedly, aborting!
* QTBUG-124375 Qt Webengine spellcheck_buildflags.h not found on macOS
* QTBUG-124353 [REG 6.5.3 - 6.6.0] Massive memory leak on WebEngineView
resizing
* QTBUG-123536 PdfPageView documentation page features PdfMultiPageView
in examples
* QTBUG-124004 Browser doesn't send onbeforeunload events when closing
* QTBUG-124790 QtWebengine 6.8 (dev) doesn't render with basic html
files
* QTBUG-124635 [REG 6.7.0->6.7.1] WebEngine does not render anything on
embedded
* QTBUG-124747 [REG 6.7.0->6.7.1] iOS examples not compiling
* QTBUG-124506 [Qt PDF] Multiple definition error for static builds
* QTBUG-125415 error: no member named 'pix' in
'QQuickPdfPageImagePrivate'
* QTBUG-121359 QtWebEngineView crashes when scrolling using the
touchpad.
* QTBUG-123008 QWebEngineWebAuthUxRequest: document PinEntryError and
PinEntryReason as \qmlproperty\value's
* QTBUG-125452 QT_FEATURE_webengine_system_icu=ON results in broken
runtime
* QTBUG-126138 Correct QML PdfSelection documentation
* QTBUG-126401 Qt webengine leaks its WebEngineQuickWidget
* QTBUG-113574 Incorrect sizing and bad text rendering with WebEngine
using fractional scaling on Wayland
* QTBUG-125035 Webengine: issues compiling with ninja 1.12
* QTBUG-125096 Print button WebEngine PDF viewer works only once
* QTBUG-126722 WebEngine: GPU detection is missing "VmWare" in vendor
list
* QTBUG-124172 FindGn: fix search path to find Gn when installed on the
host with custom install dirs
* QTBUG-113636 qtwebengine: add option to build gn only
* QTBUG-127318 QWebEngineView findText does not clear previous
findText's highlight results at certain conditions
* QTBUG-127544 qtwebengine/examples/webenginewidgets/permissionbrowser
fail to compile with -Werror=format-security
* QTBUG-124110 [REG] Warning on WebEngineView creation
* QTBUG-111927 Link hovering may not change cursor shape in web view
* QTBUG-123889 Qt webengine doesn't update cursor properly when
entering/leaving widgets
* QTBUG-115929 [REG 6.3 -> 6.4/.5] Mouse cursor is pointer-only when
leaving window at bottom edge
* QTBUG-127611 [macOS] Crash on WebEngineView destruction
* QTBUG-124878 --no-sandbox through command line does not seem to have
any effect
* QTBUG-124274 WebEngine build fails on openSUSE 15 due to libre2
* QTBUG-125300 Potential requirement on C runtime version for Qt 6.5.5
(and newer)?
* QTBUG-126312 Persistent QML WebEngineProfile causes crash upon loading
a new website
* QTBUG-127464 Intel CET hardening needs an opt-out for WebEngine
* QTBUG-122407 bitbake meta-toolchain-qt6 fails with missing cups-config
* QTBUG-120248 [Qt WebEngine] More configure-time checks and
documentation for required libraries
* QTBUG-120370 QQuickWebEngineDownloadItem is not public
* QTBUG-128140 Dead link for QWebEngineScript::sourceUrl
* QTBUG-127951 navigator.mediaDevices.enumerateDevices not returning
granted devices with PersistentPermissionsPolicy::AskEveryTime
* QTBUG-128361 Draggable elements don't work
* QTBUG-126256 [REG 6.6 -> 6.7] WebOTP crashes renderer process
* QTBUG-127797 screen sharing capabilities over WebRTC is not working
* QTBUG-119908 HTML &lt;select&gt; Element Triggers Program Crash in QT on
EGLFS/KMS Platforms
* QTBUG-127726 Screen sharing crashes in DesktopCapturer
* QTBUG-112825 Changing the user agent should disable client hints
* QTBUG-119878 [Reg 5.15->6.x] Crash and/or bad output when printing via
Qt WebEngine's PDF plugin
* QTBUG-119077 CMake deployment API does not deploy Qt Webengine
* QTBUG-120692 Cannot cross-compile webengine for x86_64
* QTBUG-85731 Screen sharing does not work on Google Meet
* QTBUG-86948 When using QImageReader to load a PDF then the PDF images
can be blurry and seem to be at half the size they should be
* QTBUG-120420 QtWebEngine inspector crashes
* QTCREATORBUG-30308 QtCreator is not able to debug pdb files when lib
linked with pdbpagesize
* QTBUG-120414 Recipe Browser example crashes
* QTBUG-122699 Failed DCHECK in v8 when watching livestream
* QTBUG-120247 [Qt WebEngine] Make it easier to re-configure after
installing missing libraries for qpa-xcb support
* QTBUG-124632 QtWebengine needs to be skipped with Windows 11 on ARM
* QTBUG-124558 Top flaky test:
tst_qwebengineglobalsettings::dnsOverHttps on Windows_11_22H2 X86_64 and
QUEMU
* QTBUG-122469 Top flaky test: tst_qwebengineprofile::clearDataFromCache
on MacOS_13 ARM64.
* QTBUG-123790 Large number of warnings are output when exiting
QWebEngineView.
* QTBUG-126049 text dump does not work realibly with 122-based
* QTBUG-123500 Unable to read out javascript engine version
* QTBUG-126085 QQuickWebEngineProfile::defaultProfile() doesn't produce
a working profile
* QTBUG-126546 Attribution documentation processed twice in CI
* QTBUG-112281 Support ANGLE on Linux
* QTBUG-127110 Platforms still use the inefficient qvsnprintf() fall-
back
* QTBUG-126655 QtWebEngine fails Yocto CI build
* QTBUG-128308 [Windows] Startup crash in gl::GLContextEGL::Initialize()
on AMD GPUs
* QTBUG-128652 tst_qmltests crashed on ubuntu-24.04-arm64-offscreen-
tests
* QTBUG-128653 tst_qquickwebengineview failed on
ubuntu-24.04-arm64-offscreen-tests

### qtwebview
* QTBUG-112346 qmllint fails when WebView is used
* QTBUG-117882 Qt 6.6.0rc QWebView on Windows locks
* QTBUG-70166 iOS Webview not able to return an object

### qtcharts
* QTBUG-119900 Deleting a visible QAbstractSeries with OpenGL enabled
causes an error
* QTBUG-127434 The labelsVisible property affects the titleVisible
property behavior if labelsVisible is set to false and titleVisible is
set to true.
* QTBUG-127982 The QLineSeries hovered signal is only re-emitted when
the mouse leaves the hover area.
* QTBUG-120282 Configuring qtcharts from sources fails because of
dependency cycle
* QTBUG-125262 Missing values from QAbstractAxis::AxisType
* QTBUG-126452 qmltyperegistrar: Build warnings in qtcharts

### qtdatavis3d
* QTBUG-122185 Manual testing - itemmodeltest crashes
* QTBUG-122209 Manual testing - "Cannot override Final property" error
in qmldynamicdata
* QTBUG-127724 tst_qmltest_datavis crash on Ubuntu 24.04 offscreen
* QTBUG-118877 -qreal float configuration option does not compile

### qtvirtualkeyboard
* QTBUG-121658 Virtual keyboard example crashes after startup on Android
* QTBUG-127120 CMake error in qtvirtualkeyboard: CMake Error: The inter-
target dependency graph contains the following strongly connected
component (cycle)
* QTBUG-126842 VirtualKeyboard is always shown on primary screen
* QTBUG-123416 [Qt Virtual Keyboard] Built-in style uses font family
that doesn't exist on all platforms
* QTBUG-114551 [VKB] Selection handle coordinates fail to take
InputPanel's parent's transformation into account
* QTBUG-120262 Use SPDX-License-Ref in 3rdparty directories
* QTBUG-121643 qt6-declarative: possible build-time race condition
around qmlcachegen
* QTBUG-112963 [Regression] Qt Virtual Keyboard not closed automatically
on IM commit
* QTBUG-80663 inputpanel::tst_plugin::test_zhuyinInputMethod is
extremely unstable

### qtscxml
* QTBUG-120576 The Note is duplicated for EventConnection::occurred
* QTBUG-120578 The date type of "event" in occurred should be specified
* QTBUG-109371 Restarting a stopped QScxmlStateMachine machine creates
an invalid state
* QTBUG-120262 Use SPDX-License-Ref in 3rdparty directories
* QTBUG-128173 Doc: Remove use of defunct QDoc command
"\tableofcontents"
* QTBUG-128368 Make sure that also qt6_ CMake commands are in the help
index

### qtspeech
* QTBUG-120655 tst_qtexttospeech (Failed)
* QTBUG-122950FAIL!:
tst_qtexttospeech_qml::Voice::test_default_voice() Compared values are
not the same
* QTBUG-122884 QML TextToSpeech enqueue does not work with Darwin engine
* QTBUG-122900 Android App dies immediately if I add TextToSpeech to the
project
* QTBUG-124868 Enable QTextToSpeech Speechd QLoggingCategory

### qtnetworkauth
* QTBUG-121727 The test: "tst_oauth1::getToken" has failed.
* QTBUG-81624 [OAuth] QOAuthHttpServerReplyHandler token double-encoding
* QTBUG-124333 [OAuth] Ability to open and close the loopback HTTP
server on a need-basis
* QTBUG-66415 Access token callback clears scope
* QTBUG-104655 QAbstractOAuth2::setState doesn't work as expected

### qtremoteobjects
* QTBUG-120242 SubClassReplicaTest crashes
* QTBUG-128368 Make sure that also qt6_ CMake commands are in the help
index

### qtquick3d
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
* QTBUG-121414 fuzzyQuaternionCompare discards tiny headRotations
causing 'jumps' that are visible in XR
* QTBUG-122143 balsam ktx build error with ASAN build
* QTBUG-108755 [REGRESSION] number of drawcalls don't show up in QML
profiler
* QTBUG-122801 XR_EXT_UUID makes spatial anchors unsupported on Quest3
in XR (fix available)
* QTBUG-123015 When configuring with -no-qml-debug then it will fail to
build QtQuick3D
* QTBUG-122052 View3D as sourceItem of texture in XR not working
* QTBUG-122722 qt6-declarative/quick3d build-time race condition around
qmlcachegen
* QTBUG-123316 QQuickGeometry JointSemantic does not work with F32Type
* QTBUG-111709 FAIL!: tst_Input::singleTap2D
* QTBUG-122890 Using MSAA, IBL and principled material causes graphical
artifacts on vulkan
* QTBUG-123846 Extended Scene Environment: Image based lighting Exposure
has no effect
* QTBUG-123442 Changing ExtendedSceneEnvironment texture properties at
runtime doesn't change the used texture
* QTBUG-115972 "flat varying" variables don't get parsed correctly into
shaders
* QTBUG-119622 Shadows are not working correctly
* QTBUG-125943 Sometimes models with receivesShadows = false are
completely black
* QTBUG-124469 qtquick3d examples crash
* QTBUG-125339 tinyexr: compile error with gcc-14
* QTBUG-125875 Manual test modelblendparticles segfaults on startup
* QTBUG-125876 Instanced models are not taken into account in shadow
mapping bounds
* QTBUG-125987 PickResult QML Type documentation no longer generated
* QTBUG-126440 Bone texture not set for depth pre-pass (and possibly
other passes)
* QTBUG-126657 Car configurator demo: shadow mapping glitches
* QTBUG-127326 materialeditor binaries missing
* QTBUG-127688 Remove obsolete Android Manifest Entries from examples
* QTBUG-120001 Game can be played in the results screen in Qt Quick 3D -
Quick Ball example
* QTBUG-127413 Building failure with FEATURE_quick_shadereffect=OFF
* QTBUG-119888 Texts overlap with each other in Qt Quick3D
* QTBUG-128370 Instance table cache not invalidated when instance table
is deleted
* QTBUG-127878 XrVirtualMouse clicks not received by ListView delegates
* QTBUG-128922 Invalid frustum dimensions in shadowmap shader
* QTBUG-120279 Cyclic dependency error in qtquick3d
* QTBUG-120109 WasdController: Models stutter in Qt Quick 3D Physics
example
* QTBUG-122142 D3D12 chokes on doublesided materials with multiview
rendering
* QTBUG-119196 Bad rendering in Qt Quick 3D - Particles 3D Testbed
example
* QTBUG-101143 QML_FOREIGN refering to a class in another library leaves
the type empty in qmltypes file
* QTBUG-122248 tst_QQuick3DNode::testProperties - comparing floats using
the operator== fails on VxWorks on 32bit arm
* QTBUG-124891 Unredistributable files in qt3d / qtquick3d
* QTBUG-126193 Crash in XR when clicking on Slider in Android Style
* QTBUG-125371 Problematic calling of qt_find_package(Qt6) in
qt_internal_project_setup
* QTBUG-127110 Platforms still use the inefficient qvsnprintf() fall-
back

### qtshadertools
* QTBUG-120513 Apps crash on shader compile on INTEGRITY (6.7 beta 1)
* QTBUG-126634 cmake/qsb fails to create the .qsb subdirectory

### qt5compat
* QTBUG-122795 Incompatibility in QTextCodec between Qt5 and Qt6 (lack
of BOM)
* QTBUG-128173 Doc: Remove use of defunct QDoc command
"\tableofcontents"

### qtmqtt
* QTBUG-120947 QMqttClient::setProtocolVersion's description seems to be
incorrect

### qtopcua
* QTBUG-120911 Qt OPC UA landing page misses license information
* QTBUG-122277 QtOpcUa does not compile using VS2022 17.9.0 on "subst"
drive
* QTBUG-120243 DiscoveryTest for open62541 crashes
* QTBUG-120960 "Backend support" table in QOpcUaMonitoringParameters is
confusing
* QTBUG-127840 Windows ARM: qtopcua -
Tst_QOpcUaSecurity::keyPairs(open62541) fails

### qtlanguageserver
* QTBUG-124592 LSP: confusing type in WorkspaceEdit breaks JSON
serialization

### qthttpserver
* QTBUG-121219 QtHttpServer crashes when during GET of a larger content
remote closes connection
* QTBUG-120746 QWebSocket immediately disconnects after without
receiving anything
* QTBUG-122154 tst_QHttpServer::multipleResponses() QCOMPARE(reply-
>attribute(QNetworkRequest::HttpStatusCodeAttribute).toInt(), 200)
returned TRUE unexpectedly.
* QTBUG-108068 QNetworkAccessManager should handle all informational
HTTP replies
* QTBUG-121462 Websocket support is easy to misuse
* QTBUG-127333 FAIL! :
tst_QHttpServerResponse::mimeTypeDetection(image/svg+xml) Compared
values are not the same
* QTBUG-105892 QHttpServer: afterRequest handlers are not executed after
each request
* QTBUG-128113 API Review for qthttpserver module

### qtquick3dphysics
* QTBUG-120045 Application crashes in Qt Quick 3D Physics
* QTBUG-120569 TriangleMeshShape geometry does not cook good, when
TexCoordSemantic used.
* QTBUG-121033 onBodyContact being called after object is deleted
* QTBUG-123888 discrepancy between PTHREAD_POOL_SIZE and
QThreadPrivate::idealThreadCount
* QTBUG-124796 QT quick 3d physics- Cannon example- shadow flickering
* QTBUG-127319 Add command line help for cooker
* QTBUG-127748 geometry_update crashed on Ubuntu 24.04 offscreen(arm64)
* QTBUG-100100 Demos should use `qt6_add_qml_module` instead of
`qt6_add_resources`

### qtgrpc
* QTBUG-120227 AddressSanitizer: heap-use-after-free in QtProtobufRepeat
edTypesJsonDeserializationTest::RepeatedComplexMessageTest()
* QTBUG-120432 Protobuf: Nested enums lack their protobuf and metatype
regestering
* QTBUG-120426 Document QGrpcRpcInfo::ReplyType
* QTBUG-120945 QGrpcChannelOptions::withMetadata
* QTBUG-121507 Qt GRPC in"All Modules" does not link to landing page
* QTBUG-121429 qtprotobuf.html:Clash between C++ namespace and group
documentation
* QTBUG-121544 qtprotobufgen generates the corrupted
protobufwellknowntypes_exports.qpb.h
* QTBUG-121585 wrong license filename in LICENSES folder ?
* QTBUG-121865 Qt GRPC module documentation link is broken
* QTBUG-121862 optional fields are not copied in messages
* QTBUG-121854 EXPORT_MACRO option has no effect in qt_add_protobuf call
* QTBUG-121856 qtgrpcgen do not generate C++ export files
* QTBUG-122677 magic8ball doesn't receive errorOccurred() if server is
not started
* QTBUG-122700 qt_add_protobuf doesn't set neither OUTPUT_HEADERS nor
OUTPUT_TARGETS
* QTBUG-121560 JSON serializer adds an object when deserializing empty
JSON arrays
* QTBUG-122816 QtGrpc generator asserts when no messages defined in
.proto file
* QTBUG-122908 Qt Chat example crashes
* QTBUG-123345 Qt GRPC HTTP2 regression
* QTBUG-123818 QGrpcBidirStream is dropping packets
* QTBUG-123996 QGrpcReply is never deleted and causes errorOccurred
after successful response
* QTBUG-124217 Calls to QGrpcCallReply::subscribe do not compile
* QTBUG-124917 [macOS] Cannot run 'magic8ball' example on macOS
* QTBUG-124899 Confusing note for server side generation
* QTBUG-125355 Ubuntu 24.04 x64: qtgrpc build fails - struct redeclared
with different access
* QTBUG-125369 Grpc: writesDone http2 implementation is broken
* QTBUG-125729 FAIL!: tst_protobuf_basictypes_qml::qtprotobufBasicTest
::test_complexMessageTypeCheck
* QTBUG-125328 Grpc genenerators: implicitly created export.qpb.h is
broken
* QTBUG-125375 QtGrpc: deadline doesn't respect server response
* QTBUG-126480 ASAN: tst_grpc_client_unarycall SEGV on unknown address
0x000000000000
* QTBUG-124594 Protobuf deserialization is slow and the bottleneck for a
vectormap application
* QTBUG-127341 Error when building for Android: qqmlgrpchttp2channel.cpp
* QTBUG-127857 -skip-tests and -skip-examples are case sensitive
* QTBUG-126451 gRPC: client-side streaming is throttling under high load
* QTBUG-126383 CMake: Failed to find required Qt component
"ProtobufQuick".
* QTBUG-128174 magic8 SimpleGrpcServer.exe build failed with MinGW
* QTBUG-127945 New example grpc/vehicle not compiling on iOS
* QTBUG-119913 When accessing protobuf message properties, propety
values always detaches the internal shared data
* QTBUG-118996 Memory leak in qprotobufserializer.h
* QTBUG-114079 qt_add_protobuf() macro should warn a user in case of
adding proto files with the same name
* QTBUG-120946 QGrpcHttp2Channel description refers to deprecated
call/channel credentials
* QTBUG-121813 qt_attribution.json issues
* QTBUG-122952 error: 'size' is not a member of 'std'
* QTBUG-123400 QtProtobuf: cannot use Qt reserved names as fields
* QTBUG-123493 QtProtobuf requires qRegisterProtobufTypes for
deserializing
* QTBUG-124915 Malformed XML generated by QML test
* QTBUG-124413 use of EXTRA_NAMESPACE with qt6_add_protobuf ends up in
front of Timestamp
* QTBUG-125016 protobuf tests are fragile
* QTBUG-125236 QtGrpc: rework interceptors
* QTBUG-125240 Core Protobuf types need QML registration
* QTBUG-127174 protobuf scalar types stop working if registered using
QML_USING
* QTBUG-125406 QtGrpc: rework documentation
* QTBUG-128196 Make the move ctor default inlined in the generated code
* QTBUG-128368 Make sure that also qt6_ CMake commands are in the help
index
* QTBUG-123643 QtProtobuf: Extra Namespace option does not work

### qtquickeffectmaker
* QTBUG-126255 Qt Quick Effect Maker ships copyrighted Rawpixel-sourced
images in violation of Rawpixel's Business License
* QTBUG-111760 target_link_libraries(foo INTERFACE Qt::Core) fails for
interface libs with CMake < 3.19 on Windows

### qtgraphs
* QTBUG-119661 tst_barstest crashes when trying the 'Swap value axis'
button
* QTBUG-119686 Height Map's slice graph does not update correctly
* QTBUG-119617 Spectogram crashes with polar graph if axis segment count
changed
* QTBUG-118414 There is a dark row in a surface with smooth shading
* QTBUG-120130 Only one series is visible in tst_surfacetest
* QTBUG-119695 Bars are too close to the floor
* QTBUG-120255 Surface gallery spectrogram demo polar graph has a gap at
the edge
* QTBUG-120209 Clearing a selected point does not work on the surface
* QTBUG-120310 Cannot exit surface slice graph view
* QTBUG-120292 'Change' buttons don't work in tst_surfacetest
* QTBUG-120400 SliceItemLabel appears even if the hide label button is
pressed
* QTBUG-120562 QtGraphs: Examples don't show in Qt Creator for Qt 6.7
* QTBUG-120657 Slice view in polar mode is incorrect
* QTBUG-120664 Changing theme doesn't update LineSeries
* QTBUG-120701 Surface graph is visible when the whole array is out of
bounds on the row axis
* QTBUG-120744 Surface is not rendered after selecting ascending data in
tst_surfacetest
* QTBUG-120128 Uniform color does not work in selected bars
* QTBUG-120480 Graph jumps to slice view when changing other properties
* QTBUG-120743 LineSeries doesn't respect minimum axis values
* QTBUG-120552 Wireframe can be toggled on when series is not visible
* QTBUG-120731 Surface slice rendering is black when data is descending
* QTBUG-121391 Shader errors with 2D grid lines if both 2D and 3D
features are on
* QTBUG-121208 Line widths not updating
* QTBUG-121372 Theme3D::baseColors is written as Theme3D::baseColor in
the document
* QTBUG-121386 tst_input fails to build if bars feature is not
configured on
* QTBUG-121476 Unity build fails with duplicated noRoleIndex definition
* QTBUG-121474 setSeriesGradient and connectSeriesGradient are
duplicated in 3 places
* QTBUG-121440 Rotating a graph with touch is unusable if slice
selection mode is in use
* QTBUG-121400 Incorrect doc reference to input handler
* QTBUG-121520 QtGraphs fails to configure manual tests without
multimedia
* QTBUG-120977 Texture appears the wrong way round with descending data
* QTBUG-121439 AxisHandling example's axis dragging doesn't work as it
should with touch
* QTBUG-121655 Q missing in front of SeriesTheme and GraphTheme
* QTBUG-121686 Callout example doesn't show lines
* QTBUG-121905 A lot of warnings from public headers
* QTBUG-121695 Setting selectedColor in XYSeries does not work
* QTBUG-121680 Crash if axisX or axisY is set to null after being first
set
* QTBUG-121687 It should not be possible to enter negative width
* QTBUG-121688 It should not be possible to set an invalid value to
capStyle
* QTBUG-121998 Q3DSurface/Q3DBars opens up as white screen by default
* QTBUG-122169 Custom pointMarker can't access outside the component
* QTBUG-122172 Manual testing - tst_barstest crashes
* QTBUG-122182 Surface graph selected point is incorrect in polar mode
* QTBUG-122247 Surface oscilloscope example labels show wrong numbers
* QTBUG-121770 QXYSeries select and deselect functions do not seem to
work
* QTBUG-121739 QBarSet selectBars and selectAllBars do not work
* QTBUG-121720 BarSeries axisX and axisY can be given invalid axes
* QTBUG-121209 Line Properties example crashes
* QTBUG-122308 Manual testing - tst_qmlsurfacelayers is not usable
* QTBUG-122445 SettingsView causes artifacts when hidden
* QTBUG-122446 GraphsView accepts events it doesn't handle
* QTBUG-122443 Lines and PointMarkers aren't clipped by GraphsView
* QTBUG-122450 Sometimes crashes in testbed
* QTBUG-122688 Bars gradient does not update
* QTBUG-122428 [REG] Axis dragging does not work in Graph Gallery
example
* QTBUG-122600 Manual testing - tst_volumetrictest is missing a file
* QTBUG-122943 Public GraphPositionQuery methods are broken
* QTBUG-123166 ScatterSeries doesn't create theme when it's not set
* QTBUG-121210 Axis Y line size not updating correctly
* QTBUG-123382 Crash on Axis Formatting
* QTBUG-122207 Undefined in bars qml example
* QTBUG-123369 [REG] Selecting a bar in bars example does not select it
in the table view
* QTBUG-123226 Custom item updating is incorrect
* QTBUG-123759 Surface graph slice view is activated when trying to
rotate the graph
* QTBUG-123624 Graph Gallery example crashes
* QTBUG-123630 Selected point in scatter graph is resized or stretched
* QTBUG-123433 Axis Handling example crashes with index out of range
error
* QTBUG-123371 [REG] Zooming into the graph in textured topography
example works incorrectly
* QTBUG-123957 [REG] Opaque items have rendering artefacts in bars and
scatter
* QTBUG-121801 QSeriesTheme setBorderWidth does not check for invalid
values
* QTBUG-124008 Surface graph picking is inaccurrate
* QTBUG-121993 AxisLabel and GridLine are Components
* QTBUG-123984 [REG] Returning from slice view does not work if slice
mode is changed while in the slice view
* QTBUG-124473 tst_qmltheme is broken
* QTBUG-124539 Surface gallery heightmap initial subgrid color is
sometimes incorrect
* QTBUG-124471 Transparency doesn't work on Uniform Color
* QTBUG-124880 Fix material property name
* QTBUG-124879 Issue on tst_theme
* QTBUG-125017 2D qml GraphsView autotests crash
* QTBUG-121718 BarCategoryAxis max returns empty string
* QTBUG-124902 baseColors property doesn't work in a GraphsTheme
* QTBUG-122435 Several Q3DScene properties do not work
* QTBUG-124812 QBarSeries::remove doesn't remove visible series
* QTBUG-125082 tst_qmltheme light adjustment sliders do not so anything
for bars
* QTBUG-125084 Some 2D graph types are missing overview documentation
* QTBUG-125137 qmlbarscatter manual test is broken
* QTBUG-125004 Disabling label background from theme causes black/white
rectangles
* QTBUG-125259 Surface graph doesn't clip on the y-axis
* QTBUG-124833 Textured topography example is shown incorrectly
* QTBUG-125392 Live data does not work for Bar Graphs
* QTBUG-125714 qmlperf crashes in bar graph
* QTBUG-125774 Wrong bar type is being used when plotareabackground is
disabled
* QTBUG-125855 Fix panning event on widget graph gallery
* QTBUG-125882 [REG] All examples crash on macOS and Linux
* QTBUG-125194 labelFont does not work correctly
* QTBUG-126102 Grid on surface is not changing color
* QTBUG-126269 Toggling labels off and on shows a empty label
* QTBUG-125907 Autotest crashes at QBarSet::replace
* QTBUG-126811 Crash in AreaSeries when no axis are defined
* QTBUG-125470 Default series theme should be valid
* QTBUG-126875 AreaSeries does not update if upper/lowerSeries is
manipulated in QML
* QTBUG-127066 Surface gallery hide background toggle seems to do
nothing
* QTBUG-125550 Incorrect interpretation of index 255 color in
QCustom3DVolume's colorTable
* QTBUG-126506 Main view is rendered on top of slice view on resize with
widget apps
* QTBUG-116628 Main graph enlarges ontop of slice view for a one frame
* QTBUG-119273 Qt Graphs axishandling example fails to build with
Boot2Qt
* QTBUG-127348 Crash in widgetgraphgallery
* QTBUG-127180 Color in slice view does not follow the background color
* QTBUG-125782 Color scheme is not automatically updated if platform
color sceheme changes
* QTBUG-126829 Docs for theme are incorrect
* QTBUG-127500 Occasional crash when doing slice selection in surface
* QTBUG-127498 Shadows do not work
* QTBUG-127253 PointGroup pointer not deleted
* QTBUG-127105 PieSeries draws extra lines when moved to second monitor
* QTBUG-127391 testbed pie graph stops responding when resized
* QTBUG-127593 Docs for min & max camera zoom levels is incorrect
* QTBUG-127631 PieSeries labels don't hide when labelVisible set to
false
* QTBUG-127502 Main view is wrong after return from slice view in
oscilloscope example
* QTBUG-126830 C++ docs are incorrect after the widget & composition
change
* QTBUG-126627 QtGraphs/6.8: Many uninitialized class member variables
* QTBUG-127728 XYSeries is not removed from graph after clear() is
called
* QTBUG-127734 tst_itemmodel crash
* QTBUG-127765 PieSeries is not centered in view
* QTBUG-122267 Manual testing - data points in tst_minimalscatter stay
hidden
* QTBUG-127743 Selecting a point with the same index from another series
does not work
* QTBUG-127763 Selecting a point from another series leaves selected
point in previous series hidden
* QTBUG-127831 Build fails if one graphtype is disabled
* QTBUG-127808 Slice view gets messed up with Legacy optimization
* QTBUG-127877 Scatter graph item size does not update instantly
* QTBUG-127879 A rectangle is visible in slice view if selectionMode
does not contain Item
* QTBUG-127922 Triggers is valuetype assertion with gradients
* QTBUG-127923 Warning in bars example
* QTBUG-127932 Clear control points if points are 0
* QTBUG-127801 Slice view is broken in QML for Bars3D
* QTBUG-127497 Wrong bar mesh used after data range change
* QTBUG-128213 Rendering issues with pie chart
* QTBUG-127769 Animation does not work in tst_directional
* QTBUG-128432 Graph Gallery example shows broken UI when resizing the
window
* QTBUG-128799 The Graph Gallery crashes on launch on Android device
* QTBUG-128889 WASM examples for 3D crash at start
* QTBUG-120244 tst_qgscatter crashes
* QTBUG-117936 Polar axis support for Scatter3D does not work
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
* QTBUG-113199 Changing a theme or color styles between object and range
gradient accumulates memory in scatter and bars
* QTBUG-122733 Spline control points are not updated in realtime
* QTBUG-124668 Remove definition of "animated" property from splines
* QTBUG-124503 Crash if setting a null GraphTheme to GraphsView
* QTBUG-125014 Bars examples broken on Windows due to theming
* QTBUG-125005 Switching between light and dark colorScheme leaves some
properties to wrong state
* QTBUG-125109 Autotest fails on tst_datetimeaxis
* QTBUG-125158 bargraph crash when barcount changed to 0 and selection
enabled
* QTBUG-125340 Crash when setting the GraphView width/height
* QTBUG-125464 Limited borderColor amount not handled
* QTBUG-125779 GraphsTheme colors are not initialized if platform
doesn't have default color scheme
* QTBUG-125462 Area renderer not using theme borderWidth property
* QTBUG-125428 Its not possible to hide/show series within GraphsView
* QTBUG-125463 Point renderer default marker border
* QTBUG-125710 BarChangingSetCount example doesn't work with custom bar
components
* QTBUG-125753 Fix PointRenderer series add/remove/visibility
* QTBUG-125752 Fix AreaRenderer series add/remove/visibility
* QTBUG-125886 QtGraphs namespace should be QtGraphs3D instead of
QGraphs3D
* QTBUG-125754 Fix PieRenderer series add/remove/visibility
* QTBUG-126653 Weird implementation in QBarSet
* QTBUG-127045 Pass QString by const ref in QDateTimeAxis
* QTBUG-127043 Add missing FINAL in QDateTimeAxis
* QTBUG-126662 2D Graphs: low performance on scrolling axis
* QTBUG-127270 Spline hover positioning not correct
* QTBUG-127118 Check qsizetype validity across classes
* QTBUG-127719 Check examples for memory issues
* QTBUG-118877 -qreal float configuration option does not compile
* QTBUG-128251 QBarSeries clicked Signal Not Emitted in Qt 6.8.0 Beta3
(Graphs: 2D)
* QTBUG-125480 Issues on 3d widget graph examples

Known Issues
------------

* Check that your system meets Qt's requirements:
https://doc.qt.io/qt-6.8/supported-platforms.html
* RTA reported issues from Qt 6.8
https://bugreports.qt.io/issues/?filter=26458
* See Qt 6.8 known issues from:
https://wiki.qt.io/Qt_6.8_Known_Issues
* Qt 6.8.0 Open issues in Jira:
https://bugreports.qt.io/issues/?filter=26530

Credits for the release goes to:
---------------------------------

Eirik Aavitsland  
Amir Masoud Abdol  
Matt Aber  
Cristian Adam  
James Addison  
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
Mahmoud Badri  
Karolina Sofia Bang  
Mate Barany  
Chris Von Bargen  
Vladimir Belyavsky  
Nicholas Bennett  
Lena Biliaieva  
Alex Blasche  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
Tatiana Borisova  
Joerg Bornemann  
Rym Bouabid  
Assam Boudjelthia  
Mark Brand  
Aurélien Brooke  
Kai Uwe Broulik  
Michael Brüning  
Alex Bu  
Alexander Busse  
Olivier De Cannière  
Alexei Cazacov  
Kaloyan Chehlarski  
Mike Chen  
Kirikaze Chiyuki  
Wang Chuan  
Ed Cooke  
Miguel Costa  
Alexandru Croitor  
Mitch Curtis  
Thibaut Cuvelier  
Giuseppe D'Angelo  
Szabolcs David  
Noah Davis  
Oliver Dawes  
Pavel Dubsky  
Artem Dyomin  
Alexey Edelev  
David Edmundson  
Oliver Eftevaag  
Christian Ehrlicher  
Hatem ElKharashy  
Andreas Eliasson  
Amr Essam  
Fabio Falsini  
David Faure  
Ilya Fedin  
Wang Fei  
Nicolas Fella  
Ted Feng  
Jesus Fernandez  
Isak Fyksen  
Simo Fält  
GHENADY  
Samuel Gaist  
Florian de Gaulejac  
Zoltan Gera  
Nazar Gerasymchuk  
Joshua Goins  
Andrei Golubev  
Aleix Pol Gonzalez  
Julian Greilich  
Robert Griebl  
Mikko Gronoff  
Magnus Groß  
Jan Grulich  
Johannes Grunenberg  
Kaj Grönholm  
Richard Moe Gustavsen  
Lucie Gérard  
Kamil Hajdukiewicz  
Rob Hall  
Mikko Hallamaa  
Amanda Hamblin-Trué  
Jøger Hansegård  
Inkamari Harjula  
Andre Hartmann  
Thomas Hartmann  
Andreas Hartmetz  
Elias Hautala  
Tero Heikkinen  
Jani Heikkinen  
Miikka Heikkinen  
Moss Heim  
Paul Heimann  
Christian Heimlich  
Jari Helaakoski  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Dominik Holland  
Mats Honkamaa  
Alexander Hulander  
Marc Hüskens  
Samuli Hölttä  
Sam James  
Allan Sandfeld Jensen  
Tim Jenssen  
Jukka Jokiniva  
Jonas Karlsson  
Kevin Keating  
Timothée Keller  
Jonathan Ketchker  
Igor Khanin  
Ahmed El Khazari  
Ali Kianian  
Kristof Kiszel  
Marius Kittler  
Friedemann Kleint  
André Klitzing  
Michal Klocek  
Ingo Klöcker  
Jarek Kobus  
Tobias Koenig  
Sze Howe Koh  
Jarkko Koivikko  
Antti Kokko  
Niko Korkala  
Tomi Korpipää  
Jani Korteniemi  
Fabian Kosmale  
Tomasz Kozłowski  
Volker Krause  
Mike Krus  
Jaroslaw Kubik  
Anton Kudryavtsev  
Santhosh Kumar  
Ghenady Kuznetsov  
Keith Kyzivat  
Kai Köhne  
Lauri Laanmets  
Inho Lee  
Frédéric Lefebvre  
Paul Lemire  
Chris Lerner  
Wladimir Leuschner  
Thorbjørn Lindeijer  
Jie Liu  
Jarno Lämsä  
Robert Löhning  
Thiago Macieira  
Andras Mantia  
Sergio Martins  
Łukasz Matysiak  
Ievgenii Meshcheriakov  
Leena Miettinen  
Jan Moeller  
Safiyyah Moosa  
Bartlomiej Moskal  
Marc Mutz  
Tommi Mänttäri  
Antti Määttä  
Jithin Nair  
Antonio Napolitano  
Martin Negyokru  
Andy Nichols  
Mårten Nordheim  
Dennis Oberst  
Kimmo Ollila  
Matti Paaso  
Tinja Paavoseppä  
Kwanghyo Park  
Ari Parkkila  
Jerome Pasion  
Samuli Piippo  
Rayam Pinto  
Timur Pocheptsov  
Milla Pohjanheimo  
Lauri Pohjanheimo  
Joni Poikelin  
Aleix Pol  
Michał Policht  
Cajus Pollmeier  
Jacek Poplawski  
Alessandro Portale  
Rami Potinkara  
Lorn Potter  
Sakaria Pouke  
Shyamnath Premnadh  
MohammadHossein Qanbari  
Liang Qi  
Matthias Rauter  
David Redondo  
Arno Rehn  
Topi Reinio  
Shawn Rutledge  
Toni Saario  
Filip Sajdak  
Ahmad Samir  
Lars Schmertmann  
Philip Schuchardt  
David Schulz  
Carl Schwan  
Thomas Senyk  
Luca Di Sera  
Dmitry Shachnev  
Sami Shalayel  
Orgad Shaneh  
Andy Shaw  
Tian Shilin  
Venugopal Shivashankar  
Pierre-Yves Siret  
Kristoffer Skau  
Nils Petter Skålerud  
Ivan Solovev  
Krzysztof Sommerfeld  
Axel Spoerl  
Stefan Steinwasser  
Martin Storsjö  
Christian Strømme  
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
Elias Toivola  
Orkun Tokdemir  
Jens Trillmann  
Jere Tuliniemi  
Tuukka Turunen  
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
Alexander Volkov  
Ville Voutilainen  
Juha Vuolle  
Olli Vuolteenaho  
Sune Vuorela  
Jaishree Vyas  
Jannis Völker  
Dongmei Wang  
Gary Wang  
Michael Weghorn  
Bernd Weimer  
Edward Welbourne  
Fushan Wen  
Paul Wicking  
Piotr Wierciński  
Milian Wolff  
Oliver Wolff  
Li Xinwei  
Weng Xuetian  
Lu YaNing  
Semih Yavuz  
Marianne Yrjänä  
Wang Yu  
Zhao Yuhang  
Vlad Zahorodnii  
Marcin Zdunek  
JiDe Zhang  
Liu Zheng  
Yifan Zhu  
Yansheng Zhu  
Volodymyr Zibarov  
Wang Zichong  
Eike Ziller  
hjk  
shjiu  
Fredrik Ålund  
Michał Łoś  
