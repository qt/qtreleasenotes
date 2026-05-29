Release notes
=============

Qt 6.5.9 release is a patch release made on the top of Qt 6.5.8.
As a patch release, Qt 6.5.9 does not add any new functionality but provides
bug fixes and other improvements and maintains both forward and backward
compatibility (source and binary) with Qt 6.5.8.
For detailed information about Qt 6.5, refer to the online documentation
included in this distribution. The documentation is also available online:

https://doc.qt.io/qt-6/index.html

The Qt version 6.5 series is binary compatible with the 6.4.x series.
Applications compiled for 6.4 will continue to run with 6.5.

Some of the changes listed in this file include issue tracking numbers
corresponding to tasks in the Qt Bug Tracker:

https://qt-project.atlassian.net/

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

* [CVE-2025-30348](https://nvd.nist.gov/vuln/detail/CVE-2025-30348) in qtbase
* [CVE-2025-4211](https://nvd.nist.gov/vuln/detail/CVE-2025-4211) in qtbase
* [CVE-2025-23050](https://nvd.nist.gov/vuln/detail/CVE-2025-23050) in qtconnectivity

### qtbase
* 63751cede3c QStringView: fix construction from arrays of unknown size
  * Made construction from arrays of unknown size compile. Such arrays will
use the const Char* constructor, determining the size of the array at
runtime.

* 2cc79682fc1 qstringfwd.h: don't include qglobal.h
  * The qstringfwd.h header no longer includes qglobal.h. A backwards-
compatible fix is to include qglobal.h yourself instead of relying on
the transitive include.

* c94e17bf322 Q{Any,Utf8}StringView: fix construction from arrays of
unknown size
  * Made construction from arrays of unknown size compile. Such arrays will
use the const Char* constructor, determining the size of the array at
runtime.

* 5f86d995ab0 Update bundled libjpeg-turbo to version 3.1.0
  * libjpeg-turbo was updated to version 3.1.0

* 510e9426432 QSaveFile: make it so flush() errors imply commit() failed
  * Fixed a bug that caused commit() to return true and overwrite its
intended target file even though it failed to flush buffered data to the
storage, which could cause data loss. This issue can be worked around by
calling flush() first and only calling commit() if that returns success.

* e3909af6425 Update bundled libpng to version 1.6.45
  * libpng was updated to version 1.6.45

* d9be50bcea8 CMake: Add PURL and CPE info to 3rd party attribution
files
  * Added PURL and CPE information to the attribution files of 3rd party
sources.

* 63e368e180e Update public suffix list
  * Updated the public suffix list to upstream SHA
47264b57765919188b9f4144de8d95cf77e1b6dc.

* 18dcb2ab5d4 Update Harfbuzz to version 10.2.0
  * Upgraded Harfbuzz to version 10.2.0.

* e1efc67bc13 QSet: don't detach in remove()/removeIf() if nothing is
being removed
  * remove() and removeIf() no longer unconditionally detach, but only if
something is actually being removed.

* 67f722e10c0 Long live qstdlibdetection.h!
  * Added Q_STL_ macros for stdlib detection (libc++, libstdc++, MSSTL,
Dinkumware, STLport, SGI, RogueWave). If your STL is lacking, please
file a bug report. Note that these macros are not considered public API
just yet.

* 0ead0332d9a qEnvironmentVariableIntValue: fix off-by-one with MSVC's
getenv_s
  * Fixed a bug that caused qEnvironmentVariableIntValue() to fail to parse
octal values from -020000000000 to -010000000000 with MSVC. Other
compilers were not affected.

* 027e80bfdbf Unbreak QSet::intersect()
  * Fixed a regression (introduced for Qt 5.2) in intersect() that caused
equivalent elements of `*this` to be overwritten by elements of `other`
if `other.size()` was larger than `this->size()`.

* 58ff6490235 QByteArray(View)::lastIndexOf: Guard against needle >
haystack
  * Fixed a bug in lastIndexOf() that could lead to out-of-bounds access
when the needle is longer than the haystack.

* 6012106f94f Update bundled libpng to version 1.6.47
  * libpng was updated to version 1.6.47

* 7e936922e1a Update license rule to Unicode-3.0
  * UCD-generated data files now come under Unicode-3.0

* 7ef3291e4fc Update UCD to Unicode 16.0.0
  * Updated the Unicode Character Database to UCD revision 34/Unicode 16.

* 0aedb5ae617 Update Harfbuzz to version 10.3.0
  * Upgraded Harfbuzz to version 10.3.0.

* ff660b68a3b Upgrade Harfbuzz to 10.4.0
  * Upgraded Harfbuzz to version 10.4.0.

* f4f79133db4 QLocale: fix UB (signed overflow) in formattedDataSize()
  * Fix issue when calling formattedDataSize() with
numeric_limits<qint64>::min().

* 69b076d902f 3rdparty: update TinyCBOR to v0.6.1
  * The copy of TinyCBOR in Qt was updated to 0.6.1.

* c449ff9cb49 QNetworkAccessManager: don't resend non-idempotent
requests
  * Non-idempotent requests are no longer incorrectly re-sent if the
connection breaks down while reading the response.

* 05ad1f79512 QUuid: fix qHash() on 64-bit platforms
  * Improved the performance of the qHash() function on 64-bit platforms by
populating all bits of the output (was: only lower 32 bits).

* 59d7eb9bbb4 QFileSystemEngine/Win: Use GetTempPath2 when available
  * On Windows, generating temporary directories for processes with elevated
privileges may now return a different path with a stricter set of
permissions. Please consult Microsoft's documentation from when they
made the same change for the .NET framework:
https://support.microsoft.com/en-us/topic/gettemppath-changes-in-
windows-february-cumulative-update-
preview-4cc631fb-9d97-4118-ab6d-f643cd0a7259

* 536610798a3 QXmlStreamReader::addData: lock encoding for QLatin1 case
  * Fixed a bug when calling addData() with a Latin1-encoded string
containing a full XML document with an encoding attribute, could result
in incorrect parsing of this document.

* b492063e8ee QProcess: fix startCommand() with whitespace-only strings
  * Fixed a bug that would cause startCommand() to crash if passed a string
that was empty or contained only whitespace characters.

* 1cc555919de SQLite: Update SQLite to v3.47.2
  * Updated SQLite to v3.47.2

* 4af97ce92d1 Update PCRE2 to 10.45
  * PCRE2 was updated to version 10.45.

* 7902480f565 QDialogButtonBox: Fix focus chain and default button
assignment
  * Default button becomes focus proxy of a QDialogButtonBox. This ensures
that Enter triggers the default button, instead of the first button in
the layout.

* 0934c0eda54 SQLite: Update SQLite to v3.48.0
  * Updated SQLite to v3.48.0

* 64d4a2281bb SQLite: Update SQLite to v3.49.0
  * Updated SQLite to v3.49.0

* 753f6a6262e SQLite: Update SQLite to v3.49.1
  * Updated SQLite to v3.49.1

* ede1f9a8d6b Upgrade Harfbuzz to 11.0.0
  * Upgraded Harfbuzz to version 11.0.0.

* 26e5700511a QCoreApplication: make removeNativeEventFilter() remove
from main thread
  * Fixed a mismatch on which event dispatcher was modified between
installNativeEventFilter() and removeNativeEventFilter(). Now both
functions in QCoreApplication access the main thread's event dispatcher.
To access the current thread's dispatcher, use
QAbstractEventDispatcher's functions.

* 692a356241e QXmlStreamReader: fix addData() unnecessary conversion to
UTF-8
  * Fixed a bug when addData(QAnyStringView) was incorrectly recoding UTF-16
and Latin1 data to UTF-8, thus potentially mangling it.

* b8bc9f60b2b Upgrade Harfbuzz to 11.1.0
  * Upgraded Harfbuzz to version 11.1.0.

* 98ead1c74d9 qDecodeDataUrl(): fix precondition violation in call to
QByteArrayView::at()
  * Fixed a bug in the handling of data: URLs that could lead to a crash if
Qt was built with assertions enabled. This affects QNetworkManager and
links in QTextDocument.

* 3bd897bd3fd SQLite: Update SQLite to v3.49.2
  * Updated SQLite to v3.49.2

* 8662666ae1f Upgrade Harfbuzz to 11.2.1
  * Upgraded Harfbuzz to version 11.2.1.

* a24f6dafe6a Update bundled libpng to version 1.6.48
  * libpng was updated to version 1.6.48

### qtdeclarative
* 5b5136ca40 IR Builder: Fix translation binding parsing
  * ListElement now supports disambiguation strings when QT_TR_NOOP is used.

* c9640966ea Qml: Fix import order for certain name resolutions
  * When a type name is provided by two different imports, the type from the
last import takes precedence. This is now also the case when resolving
singletons, attached types, and types for as-casts. This aligns with the
behavior for regular type resolution.

### qtmultimedia
* e7a2cd02b QAudioDevice: Make comparison only rely on id and mode
  * Comparison of QAudioDevice now only relies on .id() and .mode()
properties

* 958d97e07 Update FFmpeg version in documentation
  * Updated FFmpeg to n7.1.

* f8c073dd3 Fix product name and ID for the pffft third party dependency
  * Update pffft product name and id.

* 4aa004479 Document where to find FFmpeg build scripts
  * Add link to where FFmpeg build scripts can be found.

* 8268f11ee Update pffft version to the latest version from upstream
  * Updated pffft to 02fe771.

* e57e01f39 Remove security critical label from pffft and Eigen
dependencies
  * Removed security critical label from pffft and Eigen third party
dependencies.

### qtimageformats
* 242de6b8 Update bundled libwebp to version 1.5.0
  * Update bundled libwebp to version 1.5.0

### qtserialport
* de3697f3 Windows: fix readyRead() signal emission
  * Fixed a bug where the readyRead() signal did not follow the QIODevice
docs and could be emitted recursively.

### qtwebengine
* f2afb7206 Merge remote-tracking branch 'origin/6.8' into HEAD
  * Qt WebEngine lts-6.5 is now using the Qt WebEngine 6.8 code base

* de57e1b0b Add new API for screen capturing
  * Add QQuickWebEngineView::desktopMediaRequested() signal

* dbfa94722 Add WebEngineDriver
  * Added WebEngineDriver

* 56a4d784e Add hasPostData to QWebEngineNavigationRequest
  * hasFormData has been added to indicate navigations request (re)posting
form data.

* 7302e3eb4 Allow succeeding URLRequestJobs without actual content
loading
  * QWebEngineUrlRequestJob::NoError is deprecated

* 02b8b5afb Implement optional website permission persistence
  * Added new API to control permission persistence.

* 3df5f39db Add QWebEnginePermission and rewrite permissions API
  * Added new API for querying and modifying website permissions.

* aee2b8e8c [Backport] Make download API asynchronous
  * QWebEngineProfile::downloadRequested() is not limited to synchronous
usage anymore. QWebEngineDownloadRequest can be accepted or rejected
later without blocking the browsing session.

### qtnetworkauth
* 5612c95 Change QAbstractOAuth2::expirationAt also when invalidated
  * Change expirationAt also if expires_in wasn't provided, or has invalid
value, and becomes invalid.

### qtquick3d
* 60542106b Update TinyEXR to v1.0.12
  * Updated TinyEXR to v1.0.12

### qt5compat
* 9253006 QStringRef: fix lost null-ness when converting to QStringView
  * Fixed a Qt 6 regression where conversion to QStringView would no longer
preserve nullness.

* d7c66fe QStringRef: preserve null-ness when converting to
QAnyStringView
  * Fixed missing conversion to QAnyStringView.


Fixes
-----

### qtbase
* [QTBUG-130309](https://qt-project.atlassian.net/browse/QTBUG-130309) QSortFilterProxyModel invalidate is slow when there's a
large number of persistent indicies
* [QTBUG-131880](https://qt-project.atlassian.net/browse/QTBUG-131880) [macOS] Crash on [NSSavePanel
didEndPanelWithReturnCode:]
* [QTBUG-110898](https://qt-project.atlassian.net/browse/QTBUG-110898) Window disappears when monitor is disconnected
* [QTBUG-130714](https://qt-project.atlassian.net/browse/QTBUG-130714) Qt applications crash when dragging to a different X11
Screen
* [QTBUG-131731](https://qt-project.atlassian.net/browse/QTBUG-131731) REG: Possible crash on macOS when disabling emoji
parsing
* [QTBUG-116042](https://qt-project.atlassian.net/browse/QTBUG-116042) configure fails when BUILDDIR path contains "++"
* [QTBUG-129576](https://qt-project.atlassian.net/browse/QTBUG-129576) [Boot2Qt] Running "QQuickRenderControl RHI Example" app
with OpenGL graphic api causes the view to become black
* [QTBUG-131913](https://qt-project.atlassian.net/browse/QTBUG-131913) Incorrect QTimeZone documentation
* [QTBUG-117709](https://qt-project.atlassian.net/browse/QTBUG-117709) Protobuf CMakefiles don't work when protobuf libraries
aren't installed
* [QTBUG-117242](https://qt-project.atlassian.net/browse/QTBUG-117242) QtStartUpFunction is written as QtCleanUpFunction
* [QTBUG-117606](https://qt-project.atlassian.net/browse/QTBUG-117606) QLineEdit loses its frames when hovering
* [QTBUG-127522](https://qt-project.atlassian.net/browse/QTBUG-127522) QBENCHMARK result does not output global data tag
* [QTBUG-122797](https://qt-project.atlassian.net/browse/QTBUG-122797) QStringRef doesn't convert to QAnyStringView
* [QTBUG-122798](https://qt-project.atlassian.net/browse/QTBUG-122798) [REG 5.15 -> 6.7 (or earlier)] QStringRef -> QStringView
conversion loses null-ness
* [QTBUG-112746](https://qt-project.atlassian.net/browse/QTBUG-112746) QAnyStringView missing implicit conversion from char[]
with unknown size
* [QTBUG-130275](https://qt-project.atlassian.net/browse/QTBUG-130275) Segmentation Fault when using InsertWidget with too-
large index
* [QTBUG-131959](https://qt-project.atlassian.net/browse/QTBUG-131959) Build failure on QtFuture::whenAll(QFuture<void>,
QFuture<void>)
* [QTBUG-132332](https://qt-project.atlassian.net/browse/QTBUG-132332) QSaveFile will empty file if no space left on device
* [QTBUG-21329](https://qt-project.atlassian.net/browse/QTBUG-21329) QTransform::quadToQuad() doesn't work, when passed
QRectFs
* [QTBUG-132258](https://qt-project.atlassian.net/browse/QTBUG-132258) _qt_internal_create_command_script fails on windows if
spaces present
* [QTBUG-132340](https://qt-project.atlassian.net/browse/QTBUG-132340) QmlTools not automatically found
* [QTBUG-130766](https://qt-project.atlassian.net/browse/QTBUG-130766) QtConcurrent::blockingMapped has incorrect argument
deduction for generic lambdas
* [QTBUG-132115](https://qt-project.atlassian.net/browse/QTBUG-132115) QDateTimeParser::parse assertion triggered in case of
invalid date
* [QTBUG-129287](https://qt-project.atlassian.net/browse/QTBUG-129287) QDateTime fails to parse some dates
* [QTBUG-123843](https://qt-project.atlassian.net/browse/QTBUG-123843) Swipping with three finger between apps may cause a
crash after interacting with a text input field
* [QTBUG-132622](https://qt-project.atlassian.net/browse/QTBUG-132622) Failed to find required Qt component "Protobuf"
* [QTBUG-132616](https://qt-project.atlassian.net/browse/QTBUG-132616) Failed to find the host tool "Qt6::qtwaylandscanner"
* [QTBUG-132277](https://qt-project.atlassian.net/browse/QTBUG-132277) Qt fails to adhere to HTTP/2 HPACK dynamic table size
changes
* [QTBUG-122609](https://qt-project.atlassian.net/browse/QTBUG-122609) moc takes 'constexpr' as function return type
* [QTBUG-128906](https://qt-project.atlassian.net/browse/QTBUG-128906) Konsole crashes with SIGSEGV
* [QTBUG-132091](https://qt-project.atlassian.net/browse/QTBUG-132091) macOS: Key modifiers aren't ignored when dragging
'within the application'
* [QTBUG-57209](https://qt-project.atlassian.net/browse/QTBUG-57209) Wrong documentation for QOpenGLTexture::setWrapMode
* [QTBUG-132952](https://qt-project.atlassian.net/browse/QTBUG-132952) Mouse messages for QDockWidget are incorrectly cast to
QMainWindow causing a crash
* [QTBUG-130884](https://qt-project.atlassian.net/browse/QTBUG-130884) xdg-desktop-portal should be enabled only environments
that actually supports it
* [QTBUG-133289](https://qt-project.atlassian.net/browse/QTBUG-133289) Moving window container crashes if the window has been
destroyed
* [QTBUG-132597](https://qt-project.atlassian.net/browse/QTBUG-132597) Incorrect description of QTemporaryFile behavior when
two placeholders are present
* [QTBUG-132945](https://qt-project.atlassian.net/browse/QTBUG-132945) QDuplicateTracker::clear() leaks memory
* [QTBUG-132831](https://qt-project.atlassian.net/browse/QTBUG-132831) QSet::remove() unconditionally detaches
* [QTBUG-133516](https://qt-project.atlassian.net/browse/QTBUG-133516) Windows MinGW: TestNamespace errors in qcomobject
* [QTBUG-118032](https://qt-project.atlassian.net/browse/QTBUG-118032) Application crash due to double invocation of
continuation in multithreaded QPromise and QFuture usage
* [QTBUG-133101](https://qt-project.atlassian.net/browse/QTBUG-133101) GCC defines __PIC__ with -fPIE (was: Weird
QObject::findChild() behavior)
* [QTBUG-133644](https://qt-project.atlassian.net/browse/QTBUG-133644) [REG 6.6.3 -> 6.8.1] Assertion failure at QApplication
destruction
* [QTBUG-133725](https://qt-project.atlassian.net/browse/QTBUG-133725) qml_tool_autogen target loses almost all dependencies on
other autogen and sync_headers targets
* [QTBUG-132536](https://qt-project.atlassian.net/browse/QTBUG-132536) QSet::intersect() picks equivalent elements
inconsistently  from `other` or *this
* [QTBUG-133782](https://qt-project.atlassian.net/browse/QTBUG-133782) Mistakenly rounding down "bytesPerLine" for QPixmap
* [QTBUG-132314](https://qt-project.atlassian.net/browse/QTBUG-132314) GPU driver crash in iOS 18
* [QTBUG-131338](https://qt-project.atlassian.net/browse/QTBUG-131338) qtbase tst_android testFullScreenDimensions is flaky
* [QTBUG-133406](https://qt-project.atlassian.net/browse/QTBUG-133406) Unrechable code in MetaTypeQFutureHelper
* [QTBUG-127549](https://qt-project.atlassian.net/browse/QTBUG-127549) QDomNode::save() takes huge amount of time. 10x worse
performance when compared to Qt 5
* [QTBUG-15125](https://qt-project.atlassian.net/browse/QTBUG-15125) QDomAttr QDomElement::setAttributeNode ( const QDomAttr &
newAttr ) does NOT replaces attribute with the same name as newAttr.
* [QTBUG-134694](https://qt-project.atlassian.net/browse/QTBUG-134694) QNetworkAccessManager re-sends destructive requests
(POST, possibly others) without user intervention
* [QTBUG-133269](https://qt-project.atlassian.net/browse/QTBUG-133269) QTextStream: suspicious negation when streaming numbers
* [QTBUG-132310](https://qt-project.atlassian.net/browse/QTBUG-132310) Crash in QCocoaAccessible::shouldBeIgnored
* [QTBUG-134768](https://qt-project.atlassian.net/browse/QTBUG-134768) QLocale::toStrings uses E instead of e
* [QTBUG-134785](https://qt-project.atlassian.net/browse/QTBUG-134785) Provide QLocale::toString() floating-point formats for
locale-appropriate case of exponent
* [QTBUG-127517](https://qt-project.atlassian.net/browse/QTBUG-127517) Reports of misaligned loads with asan on AArch64 / xcb
* [QTBUG-134702](https://qt-project.atlassian.net/browse/QTBUG-134702) QT_QPA_PLATFORMTHEME=generic doesn't work on KDE and GTK
environments
* [QTBUG-103476](https://qt-project.atlassian.net/browse/QTBUG-103476) Custom`Delegate::destroyEditor()` is not called for some
editor when removing a tree branch
* [QTBUG-129920](https://qt-project.atlassian.net/browse/QTBUG-129920) QMetaProperty::revision() always returns a fixed value
fixed number 0xFF00 + number
* [QTBUG-122166](https://qt-project.atlassian.net/browse/QTBUG-122166) Qt Test tutorials missing a link to the source code
* [QTBUG-135033](https://qt-project.atlassian.net/browse/QTBUG-135033) QXmlStreamReader::addData() can parse Latin1 data
incorrectly
* [QTBUG-124931](https://qt-project.atlassian.net/browse/QTBUG-124931) Wrong aligenment for right to left languages in the main
menu with Windows 11
* [QTBUG-123798](https://qt-project.atlassian.net/browse/QTBUG-123798) tst_QComboBox::popupPositionAfterStyleChange() flaky on
QNX
* [QTBUG-88721](https://qt-project.atlassian.net/browse/QTBUG-88721) QTextDocument::find() does not work well with
QRegularExpressions
* [QTBUG-124512](https://qt-project.atlassian.net/browse/QTBUG-124512) QProcess::startCommand crash if empty string is passed
* [QTBUG-124151](https://qt-project.atlassian.net/browse/QTBUG-124151) Layout Item Is Not Properly Deleted if Layout Is
Disabled
* [QTBUG-120694](https://qt-project.atlassian.net/browse/QTBUG-120694) QDockWidget resize issue with Qt 6.6.1
* [QTBUG-102196](https://qt-project.atlassian.net/browse/QTBUG-102196) QDockWidget: wrong mouse cursor icon used when dock
widget floating, has custom title bar & contains window container
* [QTBUG-123989](https://qt-project.atlassian.net/browse/QTBUG-123989) Building Qt for Android with examples fails with missing
QObject:connect() overload
* [QTBUG-134703](https://qt-project.atlassian.net/browse/QTBUG-134703) Setting XDG_CURRENT_DESKTOP to xdgdesktopportal, flatpak
or snap causes an instant crash
* [QTBUG-122588](https://qt-project.atlassian.net/browse/QTBUG-122588) AA_UseStyleSheetPropagationInWidgetStyles does not work
if parent widget is already shown
* [QTBUG-118489](https://qt-project.atlassian.net/browse/QTBUG-118489) Can't tab to last button in QDialogButtonBox
* [QTBUG-123939](https://qt-project.atlassian.net/browse/QTBUG-123939) tst_qdialogbuttonbox non-deterministic failure
* [QTBUG-135109](https://qt-project.atlassian.net/browse/QTBUG-135109) some POSIX-style TZ strings are not supported by Qt on
some Linux-based platform
* [QTBUG-135471](https://qt-project.atlassian.net/browse/QTBUG-135471) tst_QXmlStream does not test non-wellformed documents
properly
* [QTBUG-134415](https://qt-project.atlassian.net/browse/QTBUG-134415) Qt FTBFS with GCC < 15 + TSAN + PCH + developer-build
* [QTBUG-117091](https://qt-project.atlassian.net/browse/QTBUG-117091) Crash during updateApplicationBadge
* [QTBUG-124783](https://qt-project.atlassian.net/browse/QTBUG-124783) QCoreApplication::removeNativeEventFilter does not use
MainThread eventDispatcher
* [QTBUG-124135](https://qt-project.atlassian.net/browse/QTBUG-124135) qtbase/cmake produced pkg-config .pc files no longer
emit dependencies
* [QTBUG-132575](https://qt-project.atlassian.net/browse/QTBUG-132575) QEasingCurve streaming operators (in/out a QDataStream)
will crash
* [QTBUG-83604](https://qt-project.atlassian.net/browse/QTBUG-83604) QSlider with ticks is glitchy with QFusionStyle
* [QTBUG-120574](https://qt-project.atlassian.net/browse/QTBUG-120574) QComboBox popup high decreases when hiding view items
* [QTBUG-135076](https://qt-project.atlassian.net/browse/QTBUG-135076) [QNX] Stale QNX Screen events under load
* [QTBUG-107904](https://qt-project.atlassian.net/browse/QTBUG-107904) Qt Designer crashes when set a negative value in border-
image
* [QTBUG-135294](https://qt-project.atlassian.net/browse/QTBUG-135294) Duplicate data tags in tst_qgraphicslinearlayout
* [QTBUG-135129](https://qt-project.atlassian.net/browse/QTBUG-135129) QXmlStreamReader::addData(QASV) overload unconditionally
converts UTF-16 and L1 to UTF-8
* [QTBUG-133923](https://qt-project.atlassian.net/browse/QTBUG-133923) Missing documentation for QFlags' equality operators
* [QTBUG-120604](https://qt-project.atlassian.net/browse/QTBUG-120604) Custom sort/filter model example - The arrow on the
magnifying glass is too high
* [QTBUG-94708](https://qt-project.atlassian.net/browse/QTBUG-94708) qCDebug() and friends could pass the category as a tag in
Android
* [QTBUG-131906](https://qt-project.atlassian.net/browse/QTBUG-131906) FAIL!  :
tst_qqmlecmascript::componentCreation(invalidMode) Not all expected
messages were received
* [QTBUG-132102](https://qt-project.atlassian.net/browse/QTBUG-132102) Windows: Fusion style: Combo-box list: Item with icon
and long text sometimes has elide
* [QTBUG-128900](https://qt-project.atlassian.net/browse/QTBUG-128900) macOS 15 deployment target build failure due to obsolete
API 'CGDisplayCreateImageForRect'
* [QTBUG-132244](https://qt-project.atlassian.net/browse/QTBUG-132244) SQLite not found in qttools when building system SQLite
in Windows
* [QTBUG-132785](https://qt-project.atlassian.net/browse/QTBUG-132785) QFile::rename() deletes file and fails to rename on
Windows/NFS
* [QTBUG-132646](https://qt-project.atlassian.net/browse/QTBUG-132646) Add a variant of QTemporaryFile::rename() that
overwrites
* [QTBUG-128420](https://qt-project.atlassian.net/browse/QTBUG-128420) Qt 6.8 does not support build paths with white spaces
anymore
* [QTBUG-132690](https://qt-project.atlassian.net/browse/QTBUG-132690) Qt 6.5 documentation states Api 34 is supported, but it
isn't
* [QTBUG-105009](https://qt-project.atlassian.net/browse/QTBUG-105009) [REG 5.15.2->6.3.1/6.4.0 Beta2] You can still insert
Chinese text into a QTextEdit when "readOnly" property is enabled.
* [QTBUG-110838](https://qt-project.atlassian.net/browse/QTBUG-110838) edit components ReadOnly invalid via some input method
* [QTBUG-119182](https://qt-project.atlassian.net/browse/QTBUG-119182) Readonly QLineEdit writable using input method
* [QTBUG-74471](https://qt-project.atlassian.net/browse/QTBUG-74471) QFileSystemModel shows directories with
setFilter(QDir::Files)
* [QTBUG-114957](https://qt-project.atlassian.net/browse/QTBUG-114957) Clarify handling of FileDialog.nameFilter on Android
* [QTBUG-126054](https://qt-project.atlassian.net/browse/QTBUG-126054) QString::arg(wchar_t{}) prefers the integral overload
instead of the QChar one
* [QTBUG-132500](https://qt-project.atlassian.net/browse/QTBUG-132500) [REG 6.7 -> 6.8] QSet::unite() no longer consistently
picks equivalent elements from `other`
* [QTBUG-132633](https://qt-project.atlassian.net/browse/QTBUG-132633) QDir::mkpath() is missing an overload with permissions
* [QTBUG-106025](https://qt-project.atlassian.net/browse/QTBUG-106025) REG: isSignalConnected creates a dead lock.
* [QTBUG-107893](https://qt-project.atlassian.net/browse/QTBUG-107893) cmake: multi-ABI Android builds do not forward cmake
arguments
* [QTBUG-83817](https://qt-project.atlassian.net/browse/QTBUG-83817) potential out-of-bounds access in qcssparser
* [QTBUG-134557](https://qt-project.atlassian.net/browse/QTBUG-134557) QOpenGLFramebufferObject seems to leak
QOpenGLSharedResourceGuards
* [QTBUG-134756](https://qt-project.atlassian.net/browse/QTBUG-134756) QJsonValue::fromVariant converts integers incorrectly
* [QTBUG-135055](https://qt-project.atlassian.net/browse/QTBUG-135055) QScroller::grabGesture() appears to leak its
QFlickGestureRecognizer
* [QTBUG-135151](https://qt-project.atlassian.net/browse/QTBUG-135151) UB when active menu of a menu bar is being deleted
* [QTBUG-122137](https://qt-project.atlassian.net/browse/QTBUG-122137) REG: QtWebEngine / Pdfwidgets no longer supports plugins
* [QTBUG-133522](https://qt-project.atlassian.net/browse/QTBUG-133522) Continuation on 'mapped' yields single result only
* [QTBUG-134913](https://qt-project.atlassian.net/browse/QTBUG-134913) QLocale::toDouble() gives unexpected result for same
decimal and grouping symbol
* [QTBUG-131653](https://qt-project.atlassian.net/browse/QTBUG-131653) Race condition between androiddeployqt runs for apk and
aab package builds
* [QTBUG-122704](https://qt-project.atlassian.net/browse/QTBUG-122704) QPainterPath de-serialisation from QDataStream fails if
item isn't empty
* [QTBUG-129754](https://qt-project.atlassian.net/browse/QTBUG-129754) Top flaky test: tst_qgesturerecognizer::touchReplay
* [QTBUG-135442](https://qt-project.atlassian.net/browse/QTBUG-135442) QDockWidget/QMainWindow leak widgetItems from
QDockAreaLayoutItem on dragging and QDockWidget::close()
* [QTBUG-135597](https://qt-project.atlassian.net/browse/QTBUG-135597) QAbstractSlider is not using SliderOrientationChange

### qtdeclarative
* [QTBUG-101159](https://qt-project.atlassian.net/browse/QTBUG-101159) SelectionRectangle does work with TableView in Android
* [QTBUG-130266](https://qt-project.atlassian.net/browse/QTBUG-130266) WheelHandler documentation examples are written for tap
handler
* [QTBUG-131776](https://qt-project.atlassian.net/browse/QTBUG-131776) TableView: calling positionWithAtColumn when a syncView
is set, fails
* [QTBUG-128462](https://qt-project.atlassian.net/browse/QTBUG-128462) Qt Quick Dialog colors are wrong when switching themes
* [QTBUG-132050](https://qt-project.atlassian.net/browse/QTBUG-132050) [Reg 6.8 -> 6.9] Different behavior in QML regex
compared to javascript
* [QTBUG-129231](https://qt-project.atlassian.net/browse/QTBUG-129231) Sporadic crash on QQuickListViewPrivate::fixup()
* [QTBUG-129427](https://qt-project.atlassian.net/browse/QTBUG-129427) Focus frame causes items in a RowLayout to change
position when focus navigating
* [QTBUG-131774](https://qt-project.atlassian.net/browse/QTBUG-131774) [REG 5.15 → 6] remove warning on signal connect with no
arguments
* [QTBUG-132423](https://qt-project.atlassian.net/browse/QTBUG-132423) [Reg 6.2.13->6.5] qtquickcompiler.prf is missing from
cross-compiling kits, so "CONFIG += qtquickcompiler" no longer works
when cross-compiling
* [QTBUG-130807](https://qt-project.atlassian.net/browse/QTBUG-130807) MouseArea::hoverEnabled property unexpectedly propagated
to child Controls.
* [QTBUG-132192](https://qt-project.atlassian.net/browse/QTBUG-132192) Item is not updated if it would be invisible under
software render
* [QTBUG-131633](https://qt-project.atlassian.net/browse/QTBUG-131633) QML Palette documentation is incomplete
* [QTBUG-132118](https://qt-project.atlassian.net/browse/QTBUG-132118) Crash when adding JS resources to a QML document
directory
* [QTBUG-106598](https://qt-project.atlassian.net/browse/QTBUG-106598) MessageDialog won't open if its parent is a plain item
* [QTBUG-132635](https://qt-project.atlassian.net/browse/QTBUG-132635) MessageDialog doesn’t open when in QQuickWidget
* [QTBUG-128229](https://qt-project.atlassian.net/browse/QTBUG-128229) JavaScript library has cyclic dependeny on itself when
importing its own qml module
* [QTBUG-132805](https://qt-project.atlassian.net/browse/QTBUG-132805) qmllint: default property
* [QTBUG-132684](https://qt-project.atlassian.net/browse/QTBUG-132684) Using QT_TR_NOOP with disambiguation string in a
ListElement causes runtime error
* [QTBUG-132921](https://qt-project.atlassian.net/browse/QTBUG-132921) Crash in QmlCacheGeneratedCode
* [QTBUG-133323](https://qt-project.atlassian.net/browse/QTBUG-133323) gcc 15: build error with src/qmldom/qqmldomtop.cpp
* [QTBUG-128420](https://qt-project.atlassian.net/browse/QTBUG-128420) Qt 6.8 does not support build paths with white spaces
anymore
* [QTBUG-133341](https://qt-project.atlassian.net/browse/QTBUG-133341) flaky test
Tst_touchMouse::touchCancelWillCancelMousePress
* [QTBUG-132648](https://qt-project.atlassian.net/browse/QTBUG-132648) tst_TouchMouse::touchButtonOnFlickable is flaky on
opensuse
* [QTBUG-132630](https://qt-project.atlassian.net/browse/QTBUG-132630) tst_qquickmousearea::doubleTap is flaky on opensuse
* [QTBUG-133342](https://qt-project.atlassian.net/browse/QTBUG-133342) Tst_QQuickMultiPointTouchArea::inFlickable2 is flaky on
Opensuse
* [QTBUG-133343](https://qt-project.atlassian.net/browse/QTBUG-133343) Tst_qquickmousearea::doubleTap flaky on Opensuse
* [QTBUG-132941](https://qt-project.atlassian.net/browse/QTBUG-132941) Top flaky test:
tst_QQuickMouseArea::nestedFlickableStopAtBounds
* [QTBUG-133344](https://qt-project.atlassian.net/browse/QTBUG-133344) Tst_qquickpinchhandler::scale is flaky on Opensuse
* [QTBUG-119545](https://qt-project.atlassian.net/browse/QTBUG-119545) Document that the URL passed to Qt.createQmlObject() can
make it override existing components
* [QTBUG-89432](https://qt-project.atlassian.net/browse/QTBUG-89432) QML enum documentation should make a greater distinction
between using enums declared in C++ and declaring enums in QML
* [QTBUG-130370](https://qt-project.atlassian.net/browse/QTBUG-130370) Missing docs for QML_NAMESPACE_EXTENDED()
* [QTBUG-128632](https://qt-project.atlassian.net/browse/QTBUG-128632) Incorrect qmllint warning about unresolved type
* [QTBUG-127098](https://qt-project.atlassian.net/browse/QTBUG-127098) qmllint: False positive for required property
* [QTBUG-134442](https://qt-project.atlassian.net/browse/QTBUG-134442) tst_qqmlcomponent::loadFromQrc() randomly fails on QNX
* [QTBUG-134001](https://qt-project.atlassian.net/browse/QTBUG-134001) [iOS] The dial handle is misaligned with the circular
path of the dial
* [QTBUG-129424](https://qt-project.atlassian.net/browse/QTBUG-129424) iOS style: Dial handle doesn't follow groove
* [QTBUG-67368](https://qt-project.atlassian.net/browse/QTBUG-67368) QJSValue::strictlyEquals documentation error
* [QTBUG-134664](https://qt-project.atlassian.net/browse/QTBUG-134664) FAIL!  :
tst_examples::examples(examples/quick/multieffect/testbed/qml/main.qml)
Received a fatal error
* [QTBUG-134492](https://qt-project.atlassian.net/browse/QTBUG-134492) Thread sanitizer (TSAN) warns about data race with QSG
Scenegraph (qsgmaterial)
* [QTBUG-122043](https://qt-project.atlassian.net/browse/QTBUG-122043) The button appears to be pressed twice, even if it's
pressed only once while you are pressing another button at the same time
on the Android app
* [QTBUG-95887](https://qt-project.atlassian.net/browse/QTBUG-95887) tst_FlickableInterop is flaky on opensuse
* [QTBUG-122405](https://qt-project.atlassian.net/browse/QTBUG-122405) tst_qquickhoverhandler::window is flaky on OpenSuse
* [QTBUG-134688](https://qt-project.atlassian.net/browse/QTBUG-134688) Aliases of properties of bindables don't emit change
signals
* [QTBUG-75215](https://qt-project.atlassian.net/browse/QTBUG-75215) tst_qquickapplication::active() is flaky on opensuse
* [QTBUG-123550](https://qt-project.atlassian.net/browse/QTBUG-123550) Top flaky test: tst_qquickapplication::active on
openSUSE_15_5 X86_64.
* [QTBUG-133784](https://qt-project.atlassian.net/browse/QTBUG-133784) [Qt 6.5.8] qmlsc: Direct calls generates C++ code with
wrong header path for qplatformdialoghelper.h
* [QTBUG-135849](https://qt-project.atlassian.net/browse/QTBUG-135849) qv4compileddata_p.h:1558:31: error: comparison of
integers of different signs
* [QTBUG-134043](https://qt-project.atlassian.net/browse/QTBUG-134043) tst_QQuickColorDialogImpl::dialogCanMoveBetweenWindows
is flaky
* [QTBUG-135868](https://qt-project.atlassian.net/browse/QTBUG-135868) CMake fail, qml/qmldom/CMakeLists.txt
* [QTBUG-134778](https://qt-project.atlassian.net/browse/QTBUG-134778) Binding: short syntax broken with ComponentBehavior:
Bound
* [QTBUG-131961](https://qt-project.atlassian.net/browse/QTBUG-131961) Qml engine crashes when running SameValueZero
* [QTBUG-125289](https://qt-project.atlassian.net/browse/QTBUG-125289) Add an overload of toScriptValue that only produces
vanilla JavaScript types
* [QTBUG-130374](https://qt-project.atlassian.net/browse/QTBUG-130374) tst_qquicktextedit is flaky on Linux
* [QTBUG-130879](https://qt-project.atlassian.net/browse/QTBUG-130879) "Failed to build texture render target for layer" error
log when using Flickable, resizeContent and layer.enabled
* [QTBUG-133530](https://qt-project.atlassian.net/browse/QTBUG-133530) Several Controls tests failing after test coverage
restored
* [QTBUG-134768](https://qt-project.atlassian.net/browse/QTBUG-134768) QLocale::toStrings uses E instead of e

### qtactiveqt
* [QTBUG-123520](https://qt-project.atlassian.net/browse/QTBUG-123520) QAxObject has invalid properties that can not be set
either

### qtmultimedia
* [QTBUG-131530](https://qt-project.atlassian.net/browse/QTBUG-131530) declarative-camera crashes on startup under iOS 18.1
* [QTBUG-130970](https://qt-project.atlassian.net/browse/QTBUG-130970) [wayland] qtmm examples crash on rockchip when using
wayland
* [QTBUG-131284](https://qt-project.atlassian.net/browse/QTBUG-131284) The QML video example crashes when running fullscreen
mode for the video and getting back to the main app view
* [QTBUG-124351](https://qt-project.atlassian.net/browse/QTBUG-124351) [Boot2Qt][Wayland] The widgets camera app crashes when
taking the picture in the full screen
* [QTBUG-131107](https://qt-project.atlassian.net/browse/QTBUG-131107) QVideoFrame::toImage / qImageFromVideoFrame not safe to
call from worker thread
* [QTBUG-130901](https://qt-project.atlassian.net/browse/QTBUG-130901) Crash on Some Android Device when using Multimedia
* [QTBUG-126305](https://qt-project.atlassian.net/browse/QTBUG-126305) Setting camera pixel format and resolution is failed.
* [QTBUG-114104](https://qt-project.atlassian.net/browse/QTBUG-114104) R8 is not supported on GLES 2.0 only systems
* [QTBUG-131882](https://qt-project.atlassian.net/browse/QTBUG-131882) QtMultimedia - crashes with 'darwin' plugin (iOS)
* [QTBUG-129394](https://qt-project.atlassian.net/browse/QTBUG-129394) Qt Dice freeze (not hang, just jerky)
* [QTBUG-132266](https://qt-project.atlassian.net/browse/QTBUG-132266) QSoundEffect plays choppy WAV sound effects on macOS
* [QTBUG-132478](https://qt-project.atlassian.net/browse/QTBUG-132478) Memory leak in video playback
* [QTBUG-133201](https://qt-project.atlassian.net/browse/QTBUG-133201) Recording audio can crash if audio was previously
recorded with a codec with a bigger buffer size
* [QTBUG-113247](https://qt-project.atlassian.net/browse/QTBUG-113247) Crash when recording wav audio
* [QTBUG-132532](https://qt-project.atlassian.net/browse/QTBUG-132532) Audiorecoder example bugs
* [QTBUG-133096](https://qt-project.atlassian.net/browse/QTBUG-133096) QML ImageCapture property fileFormat is read-only
* [QTBUG-133250](https://qt-project.atlassian.net/browse/QTBUG-133250) QImageCapture::fileFormatChanged signal fires when value
is unchanged
* [QTBUG-130386](https://qt-project.atlassian.net/browse/QTBUG-130386) [QML] MediaPlayer{}/Video{} crashes when changing the
media source right after calling play()
* [QTBUG-132463](https://qt-project.atlassian.net/browse/QTBUG-132463) Recording video and audio with AAC audio codec don't
play back correctly in Windows Media Player or Quicktime on macOS
* [QTBUG-134135](https://qt-project.atlassian.net/browse/QTBUG-134135) qandroidvideoframebuffer.cpp gives "error: variable
length arrays in C++ are a Clang extension" errors with NDK r27c
* [QTBUG-134046](https://qt-project.atlassian.net/browse/QTBUG-134046) [Android] The audiorecorder example app is crashing when
trying to record anything with disallowed permissions
* [QTBUG-133773](https://qt-project.atlassian.net/browse/QTBUG-133773) Cannot record a video with QML camera
* [QTBUG-134882](https://qt-project.atlassian.net/browse/QTBUG-134882) QAudioDevice::isFormatSupported() not working on Android
* [QTBUG-128908](https://qt-project.atlassian.net/browse/QTBUG-128908) HLS video stream (m3u8) has glitches and delay in the
first segment

### qtdoc
* [QTBUG-130567](https://qt-project.atlassian.net/browse/QTBUG-130567) Doc: wrong link to XWayland
* [QTBUG-122178](https://qt-project.atlassian.net/browse/QTBUG-122178) [Media Player Example] App hangs when previous track is
clicked
* [QTBUG-116765](https://qt-project.atlassian.net/browse/QTBUG-116765) qmlformat: unnecessarily formats single line to multiple
lines
* [QTBUG-135250](https://qt-project.atlassian.net/browse/QTBUG-135250) Editorial notes on `Qt for Wayland Requirements` page
* [QTBUG-134789](https://qt-project.atlassian.net/browse/QTBUG-134789) "Contents" menu hidden behind images
* [QTBUG-132690](https://qt-project.atlassian.net/browse/QTBUG-132690) Qt 6.5 documentation states Api 34 is supported, but it
isn't

### qtpositioning
* [QTBUG-133935](https://qt-project.atlassian.net/browse/QTBUG-133935) QML Qt Positioning memory use after free() / double
free()

### qtconnectivity
* [QTBUG-131940](https://qt-project.atlassian.net/browse/QTBUG-131940) Bluetooth examples does not work on iOS
* [QTBUG-132202](https://qt-project.atlassian.net/browse/QTBUG-132202) Qt bluetooth qlowenergycontroller_winrt.cpp incorrectly
assumes CharacteristicUserDescription returns UTF16 when it actually
returns UTF8
* [QTBUG-133534](https://qt-project.atlassian.net/browse/QTBUG-133534) Warn user that too large data can make
QLowEnergyAdvertisingData::setManufacturerData fail in error
* [QTBUG-133788](https://qt-project.atlassian.net/browse/QTBUG-133788) Ndef editor example cross-compiling on Windows to
Boot2Qt fails
* [QTBUG-99410](https://qt-project.atlassian.net/browse/QTBUG-99410) [macOS 12.1] Bluetooth data stream blocked when main menu
opened
* [QTBUG-132455](https://qt-project.atlassian.net/browse/QTBUG-132455) [Android] Lots of deprecated API is used

### qtwayland
* [QTBUG-105703](https://qt-project.atlassian.net/browse/QTBUG-105703) QWaylandWindow::createDecoration() is called from
multiple threads
* [QTBUG-134264](https://qt-project.atlassian.net/browse/QTBUG-134264) "QtShell Compositor" -example install instructions
missing

### qt3d
* [QTBUG-119137](https://qt-project.atlassian.net/browse/QTBUG-119137) ERROR: AddressSanitizer: heap-use-after-free in
tst_qmesh::checkSourceUpdate() in qt3d

### qtserialbus
* [QTBUG-135299](https://qt-project.atlassian.net/browse/QTBUG-135299) error: ‘QElapsedTimer’ was not declared in this scope

### qtserialport
* [QTBUG-105561](https://qt-project.atlassian.net/browse/QTBUG-105561) QSerialPort Mark/Space Emulation causes recursion and
crash
* [QTBUG-131679](https://qt-project.atlassian.net/browse/QTBUG-131679) QSerialPort does not have Mark/Space parity emulation
for reading the data
* [QTBUG-84689](https://qt-project.atlassian.net/browse/QTBUG-84689) readyRead() signal will be reemitted even I have called
waitForReadyRead()
* [QTBUG-67544](https://qt-project.atlassian.net/browse/QTBUG-67544) QSerialPort emits errorOccurred with NoError

### qtwebengine
* [QTBUG-119789](https://qt-project.atlassian.net/browse/QTBUG-119789) [Accessibility] Qt 6.5.3 cannot be built with the option
' -no-feature-accessibility''.
* [QTBUG-112142](https://qt-project.atlassian.net/browse/QTBUG-112142) [Qt WebEngine] ScreenCapture should provide a way to
select window/screen to capture
* [QTBUG-118120](https://qt-project.atlassian.net/browse/QTBUG-118120) qtwebengine: build failure with x86_64h
* [QTBUG-120245](https://qt-project.atlassian.net/browse/QTBUG-120245) A crash occurred in C:\Users\qt\work\qt\qtwebengine_stan
dalone_tests\tests\auto\pdfquick\multipageview\tst_multipageview.exe
* [QTBUG-118398](https://qt-project.atlassian.net/browse/QTBUG-118398) QWebEngineView in QScrollArea is not scrollable
* [QTBUG-119776](https://qt-project.atlassian.net/browse/QTBUG-119776) PDF Multipage viewer example - Clicking on previous
(upward arrow) will crash the example
* [QTBUG-104767](https://qt-project.atlassian.net/browse/QTBUG-104767) Using PdfPageImage instead of Image on PDF file results
in EXC_BAD_ACCESS (SIGSEGV)
* [QTBUG-120446](https://qt-project.atlassian.net/browse/QTBUG-120446) Alternated item color in list is not always alternated
* [QTBUG-119722](https://qt-project.atlassian.net/browse/QTBUG-119722) [REG 5 → 6] Default context menu is missing icons
* [QTBUG-86869](https://qt-project.atlassian.net/browse/QTBUG-86869) Unrecognized Chrome version when using Selenium and
Chromedriver
* [QTBUG-118746](https://qt-project.atlassian.net/browse/QTBUG-118746) Japanese input on macOS regressed in Qt 6.5.3
* [QTBUG-119245](https://qt-project.atlassian.net/browse/QTBUG-119245) Qt Web Engine alert quotes not working
* [QTBUG-83338](https://qt-project.atlassian.net/browse/QTBUG-83338) Default implementations of javaScriptAlert/Confirm/Prompt
treat message as rich text
* [QTBUG-119991](https://qt-project.atlassian.net/browse/QTBUG-119991) Unable to print at all if the first page of multi page
document is not printed
* [QTBUG-120218](https://qt-project.atlassian.net/browse/QTBUG-120218) QML WebEngineView.printToPdf(): paper formats are wrong
in the resulting document
* [QTBUG-115502](https://qt-project.atlassian.net/browse/QTBUG-115502) PdfMultiPageView: repeated pinch-zooming jumps to wrong
zoom level
* [QTBUG-119416](https://qt-project.atlassian.net/browse/QTBUG-119416) Loading a specific page in a PDF document does not
always show the correct page
* [QTBUG-121564](https://qt-project.atlassian.net/browse/QTBUG-121564) tst_MultiPageView::pinchDragPinch is flaky
* [QTBUG-
120689](https://qt-project.atlassian.net/browse/QTBUG-120689) tst_qwebenginepage::getUserMediaRequestDesktopVideoManyPages is
flaky
* [QTBUG-121502](https://qt-project.atlassian.net/browse/QTBUG-121502) crash in QPdfIOHandler if document is deleted too early
* [QTBUG-85473](https://qt-project.atlassian.net/browse/QTBUG-85473) QML WebEngineSettings misses ScrollAnimatorEnabled but
QWebEngineSettings has it
* [QTBUG-120273](https://qt-project.atlassian.net/browse/QTBUG-120273) QWebEngineView shows blank content on initial show when
page bg set to transparent
* [QTBUG-121227](https://qt-project.atlassian.net/browse/QTBUG-121227) QWebEngineView shows blank content on initial show when
page bg set to transparent
* [QTBUG-112013](https://qt-project.atlassian.net/browse/QTBUG-112013) QWebEnginePage.setBackground(Qt::black) doesn't work for
page loading.
* [QTBUG-120926](https://qt-project.atlassian.net/browse/QTBUG-120926) QWebEnginePage::setBackgroundColor doesn't work properly
* [QTBUG-122137](https://qt-project.atlassian.net/browse/QTBUG-122137) REG: QtWebEngine / Pdfwidgets no longer supports plugins
* [QTBUG-122153](https://qt-project.atlassian.net/browse/QTBUG-122153) QWebEngineView::setFocus() doesn't give focus to the
view after calling QWebEngineView::load() for the second time
* [QTBUG-92114](https://qt-project.atlassian.net/browse/QTBUG-92114) Shift-Tab moves focus forward instead of backward in
WebEngineView inside QQuickWidget
* [QTBUG-121589](https://qt-project.atlassian.net/browse/QTBUG-121589) Can't build qt6 due to failed ozone platform assertion
* [QTBUG-118035](https://qt-project.atlassian.net/browse/QTBUG-118035) QtWebengine build fails on pure wayland
* [QTBUG-122997](https://qt-project.atlassian.net/browse/QTBUG-122997) The Spellcheck example doesn't work on macOS
* [QTBUG-77450](https://qt-project.atlassian.net/browse/QTBUG-77450) Issues with clipboard permissions
* [QTBUG-122655](https://qt-project.atlassian.net/browse/QTBUG-122655) 6.8.0 toplevel build fails on macOS, qtwebengine
* [QTBUG-123548](https://qt-project.atlassian.net/browse/QTBUG-123548) PDF multipage viewer converts a simple local filename in
the cwd to an http url
* [QTBUG-120764](https://qt-project.atlassian.net/browse/QTBUG-120764) PDF Viewer Widget example search error
* [QTBUG-106565](https://qt-project.atlassian.net/browse/QTBUG-106565) The coordinate of QPdfSelection seems like to be wrong
when pdf page contains non-displayable area
* [QTBUG-100630](https://qt-project.atlassian.net/browse/QTBUG-100630) PdfLinkModel don't give the right rect everytime
* [QTBUG-123765](https://qt-project.atlassian.net/browse/QTBUG-123765) Segfault when dropping elements from Spotify in Firefox
* [QTBUG-120131](https://qt-project.atlassian.net/browse/QTBUG-120131) Auto-scrolling does not work with quicknanobrowser
example
* [QTBUG-122916](https://qt-project.atlassian.net/browse/QTBUG-122916) Print preview: crash when pressing a resize button
* [QTBUG-122970](https://qt-project.atlassian.net/browse/QTBUG-122970) Copying and pasting using shortcuts is not working in
MacOS
* [QTBUG-124527](https://qt-project.atlassian.net/browse/QTBUG-124527) qtwebengine integrations fail on 6.7: qt-testrunner.py
ERROR: Full test run failed repeatedly, aborting!
* [QTBUG-124375](https://qt-project.atlassian.net/browse/QTBUG-124375) Qt Webengine spellcheck_buildflags.h not found on macOS
* [QTBUG-124353](https://qt-project.atlassian.net/browse/QTBUG-124353) [REG 6.5.3 - 6.6.0] Massive memory leak on WebEngineView
resizing
* [QTBUG-123536](https://qt-project.atlassian.net/browse/QTBUG-123536) PdfPageView documentation page features PdfMultiPageView
in examples
* [QTBUG-124004](https://qt-project.atlassian.net/browse/QTBUG-124004) Browser doesn't send onbeforeunload events when closing
* [QTBUG-124790](https://qt-project.atlassian.net/browse/QTBUG-124790) QtWebengine 6.8 (dev) doesn't render with basic html
files
* [QTBUG-124635](https://qt-project.atlassian.net/browse/QTBUG-124635) [REG 6.7.0->6.7.1] WebEngine does not render anything on
embedded
* [QTBUG-124747](https://qt-project.atlassian.net/browse/QTBUG-124747) [REG 6.7.0->6.7.1] iOS examples not compiling
* [QTBUG-124506](https://qt-project.atlassian.net/browse/QTBUG-124506) [Qt PDF] Multiple definition error for static builds
* [QTBUG-125415](https://qt-project.atlassian.net/browse/QTBUG-125415) error: no member named 'pix' in
'QQuickPdfPageImagePrivate'
* [QTBUG-121359](https://qt-project.atlassian.net/browse/QTBUG-121359) QtWebEngineView crashes when scrolling using the
touchpad.
* [QTBUG-123008](https://qt-project.atlassian.net/browse/QTBUG-123008) QWebEngineWebAuthUxRequest: document PinEntryError and
PinEntryReason as \qmlproperty\value's
* [QTBUG-125452](https://qt-project.atlassian.net/browse/QTBUG-125452) QT_FEATURE_webengine_system_icu=ON results in broken
runtime
* [QTBUG-126138](https://qt-project.atlassian.net/browse/QTBUG-126138) Correct QML PdfSelection documentation
* [QTBUG-126401](https://qt-project.atlassian.net/browse/QTBUG-126401) Qt webengine leaks its WebEngineQuickWidget
* [QTBUG-113574](https://qt-project.atlassian.net/browse/QTBUG-113574) Incorrect sizing and bad text rendering with WebEngine
using fractional scaling on Wayland
* [QTBUG-125035](https://qt-project.atlassian.net/browse/QTBUG-125035) Webengine: issues compiling with ninja 1.12
* [QTBUG-125096](https://qt-project.atlassian.net/browse/QTBUG-125096) Print button WebEngine PDF viewer works only once
* [QTBUG-126722](https://qt-project.atlassian.net/browse/QTBUG-126722) WebEngine: GPU detection is missing "VmWare" in vendor
list
* [QTBUG-124172](https://qt-project.atlassian.net/browse/QTBUG-124172) FindGn: fix search path to find Gn when installed on the
host with custom install dirs
* [QTBUG-113636](https://qt-project.atlassian.net/browse/QTBUG-113636) qtwebengine: add option to build gn only
* [QTBUG-127318](https://qt-project.atlassian.net/browse/QTBUG-127318) QWebEngineView findText does not clear previous
findText's highlight results at certain conditions
* [QTBUG-127544](https://qt-project.atlassian.net/browse/QTBUG-127544) qtwebengine/examples/webenginewidgets/permissionbrowser
fail to compile with -Werror=format-security
* [QTBUG-124110](https://qt-project.atlassian.net/browse/QTBUG-124110) [REG] Warning on WebEngineView creation
* [QTBUG-111927](https://qt-project.atlassian.net/browse/QTBUG-111927) Link hovering may not change cursor shape in web view
* [QTBUG-123889](https://qt-project.atlassian.net/browse/QTBUG-123889) Qt webengine doesn't update cursor properly when
entering/leaving widgets
* [QTBUG-115929](https://qt-project.atlassian.net/browse/QTBUG-115929) [REG 6.3 -> 6.4/.5] Mouse cursor is pointer-only when
leaving window at bottom edge
* [QTBUG-127611](https://qt-project.atlassian.net/browse/QTBUG-127611) [macOS] Crash on WebEngineView destruction
* [QTBUG-124878](https://qt-project.atlassian.net/browse/QTBUG-124878) --no-sandbox through command line does not seem to have
any effect
* [QTBUG-124274](https://qt-project.atlassian.net/browse/QTBUG-124274) WebEngine build fails on openSUSE 15 due to libre2
* [QTBUG-125300](https://qt-project.atlassian.net/browse/QTBUG-125300) Potential requirement on C runtime version for Qt 6.5.5
(and newer)?
* [QTBUG-126312](https://qt-project.atlassian.net/browse/QTBUG-126312) Persistent QML WebEngineProfile causes crash upon
loading a new website
* [QTBUG-127464](https://qt-project.atlassian.net/browse/QTBUG-127464) Intel CET hardening needs an opt-out for WebEngine
* [QTBUG-122407](https://qt-project.atlassian.net/browse/QTBUG-122407) bitbake meta-toolchain-qt6 fails with missing cups-
config
* [QTBUG-120248](https://qt-project.atlassian.net/browse/QTBUG-120248) [Qt WebEngine] More configure-time checks and
documentation for required libraries
* [QTBUG-120370](https://qt-project.atlassian.net/browse/QTBUG-120370) QQuickWebEngineDownloadItem is not public
* [QTBUG-128140](https://qt-project.atlassian.net/browse/QTBUG-128140) Dead link for QWebEngineScript::sourceUrl
* [QTBUG-127951](https://qt-project.atlassian.net/browse/QTBUG-127951) navigator.mediaDevices.enumerateDevices not returning
granted devices with PersistentPermissionsPolicy::AskEveryTime
* [QTBUG-128361](https://qt-project.atlassian.net/browse/QTBUG-128361) Draggable elements don't work
* [QTBUG-126256](https://qt-project.atlassian.net/browse/QTBUG-126256) [REG 6.6 -> 6.7] WebOTP crashes renderer process
* [QTBUG-127797](https://qt-project.atlassian.net/browse/QTBUG-127797) screen sharing capabilities over WebRTC is not working
* [QTBUG-119908](https://qt-project.atlassian.net/browse/QTBUG-119908) HTML \<select\> Element Triggers Program Crash in QT on
EGLFS/KMS Platforms
* [QTBUG-127726](https://qt-project.atlassian.net/browse/QTBUG-127726) Screen sharing crashes in DesktopCapturer
* [QTBUG-128784](https://qt-project.atlassian.net/browse/QTBUG-128784) OpenGL context creation issues when D3D11 RHI is used
(sic)
* [QTBUG-108763](https://qt-project.atlassian.net/browse/QTBUG-108763) Incorrect documentation for
QWebEngineUrlRequestInterceptor.interceptRequest
* [QTBUG-128241](https://qt-project.atlassian.net/browse/QTBUG-128241) HTML selection tag crashes app when clicked on
* [QTBUG-128897](https://qt-project.atlassian.net/browse/QTBUG-128897) Pure virtual function call on
NativeSkiaOutputDevice::Present()
* [QTBUG-128857](https://qt-project.atlassian.net/browse/QTBUG-128857) Qt WebEngine underperforms compared to Google Chrome by
factor of  2 ~ 3
* [QTBUG-104065](https://qt-project.atlassian.net/browse/QTBUG-104065) [REG 6.2->6.3] QtWebEngine font color issue
* [QTBUG-129884](https://qt-project.atlassian.net/browse/QTBUG-129884) Webengine tests hang after
qmltests::GetUserMedia::test_getUserMedia(desktop video) on Windows 11
* [QTBUG-130034](https://qt-project.atlassian.net/browse/QTBUG-130034) Top flaky test:
tst_qwebenginepage::getUserMediaRequestDesktopVideoManyPages
* [QTBUG-130035](https://qt-project.atlassian.net/browse/QTBUG-130035) Top flaky test: tst_qwebenginepage::getUserMediaRequest
* [QTBUG-130327](https://qt-project.atlassian.net/browse/QTBUG-130327) Missing closing bracket in QWebEngineUrlSchemeHandler
documentation
* [QTBUG-129796](https://qt-project.atlassian.net/browse/QTBUG-129796) Blocking main frame request from a Google Search crashes
the process
* [QTBUG-130500](https://qt-project.atlassian.net/browse/QTBUG-130500) Various network tests are failing on macOS 15
* [QTBUG-129826](https://qt-project.atlassian.net/browse/QTBUG-129826) [6.8] Minimum python version isn't correct anymore
* [QTBUG-130599](https://qt-project.atlassian.net/browse/QTBUG-130599) [Regr: 6.7->6.8]JavascriptCanAccessClipboard doesn't
allowing copying to clipboard on 6.8
* [QTBUG-130790](https://qt-project.atlassian.net/browse/QTBUG-130790) error: 'cortex-a53' does not support feature 'crc'
* [QTBUG-131397](https://qt-project.atlassian.net/browse/QTBUG-131397) WebEngineProfile doesn't instantiate in QML if property
declarations are in a specific order
* [QTBUG-
131342](https://qt-project.atlassian.net/browse/QTBUG-131342) qtwebengine/src/core/compositor/native_skia_output_device_vulkan.
cpp:252:34: error: use of undeclared identifier 'importMemoryHandleInfo'
* [QTBUG-129153](https://qt-project.atlassian.net/browse/QTBUG-129153) Sporadic crash on NativeSkiaOutputDevice::BeginPaint()
* [QTBUG-131156](https://qt-project.atlassian.net/browse/QTBUG-131156) Scripts injected on DocumentReady and Deferred are not
always executed on google.com
* [QTBUG-131304](https://qt-project.atlassian.net/browse/QTBUG-131304) Broken rendering when reparenting WebEngineView to
another window
* [QTBUG-123095](https://qt-project.atlassian.net/browse/QTBUG-123095) Wheel scrolling issues in WebEngine
* [QTBUG-131896](https://qt-project.atlassian.net/browse/QTBUG-131896) A sentence is cut in the middle in the Native Dialogs
section in Qt WebEngine features
* [QTBUG-132564](https://qt-project.atlassian.net/browse/QTBUG-132564) qwebengine-convert-dict fails on .dic wordlist
* [QTBUG-128893](https://qt-project.atlassian.net/browse/QTBUG-128893) sbom for qtpdf gets lost , as it ends up as qtwebengine
sbom
* [QTBUG-130608](https://qt-project.atlassian.net/browse/QTBUG-130608) Dropdown in WebEngineView are not zoomed and aligned
properly when parent of WebEngineView is zoomed.
* [QTBUG-132411](https://qt-project.atlassian.net/browse/QTBUG-132411) Chromium version isn't reduced in user-agent string
* [QTBUG-131969](https://qt-project.atlassian.net/browse/QTBUG-131969) "Spellchecking can not be enabled" error logged when
disabling spell checking
* [QTBUG-132682](https://qt-project.atlassian.net/browse/QTBUG-132682) [REG 6.9] Segfault in
{{QtWebEngineCore::NativeSkiaOutputDeviceOpenGL::texture()}} with
offscreen platform
* [QTBUG-133558](https://qt-project.atlassian.net/browse/QTBUG-133558) DRM video fails to play on macOS
* [QTBUG-133590](https://qt-project.atlassian.net/browse/QTBUG-133590) tst_qwebengineview::keyboardFocusAfterPopup on macos
* [QTBUG-133649](https://qt-project.atlassian.net/browse/QTBUG-133649) When calling QWebEngineView::setFocus after calling
QWebEngineView::setFocus for the second time, focus is given to another
widget
* [QTBUG-131841](https://qt-project.atlassian.net/browse/QTBUG-131841) PdfScrollablePageView does not work in the app
* [QTBUG-134248](https://qt-project.atlassian.net/browse/QTBUG-134248) QDoc: error: Documentation warnings (6) exceeded the
limit (2) for 'QtWebEngine'.
* [QTBUG-133495](https://qt-project.atlassian.net/browse/QTBUG-133495) Missing Documentation of 3rd party component usage
* [QTBUG-134107](https://qt-project.atlassian.net/browse/QTBUG-134107) Qt WebEngine NumLock detection broken using
KeyboardDriver::Xkb
* [QTBUG-134416](https://qt-project.atlassian.net/browse/QTBUG-134416) Log noise when building Qt WebEngine documentation
* [QTBUG-112825](https://qt-project.atlassian.net/browse/QTBUG-112825) Changing the user agent should disable client hints
* [QTBUG-119878](https://qt-project.atlassian.net/browse/QTBUG-119878) [Reg 5.15->6.x] Crash and/or bad output when printing
via Qt WebEngine's PDF plugin
* [QTBUG-119077](https://qt-project.atlassian.net/browse/QTBUG-119077) CMake deployment API does not deploy Qt Webengine
* [QTBUG-120692](https://qt-project.atlassian.net/browse/QTBUG-120692) Cannot cross-compile webengine for x86_64
* [QTBUG-85731](https://qt-project.atlassian.net/browse/QTBUG-85731) Screen sharing does not work on Google Meet
* [QTBUG-86948](https://qt-project.atlassian.net/browse/QTBUG-86948) When using QImageReader to load a PDF then the PDF images
can be blurry and seem to be at half the size they should be
* [QTBUG-120420](https://qt-project.atlassian.net/browse/QTBUG-120420) QtWebEngine inspector crashes
* [QTCREATORBUG-30308](https://qt-project.atlassian.net/browse/QTCREATORBUG-30308) QtCreator is not able to debug pdb files when lib
linked with pdbpagesize
* [QTBUG-120414](https://qt-project.atlassian.net/browse/QTBUG-120414) Recipe Browser example crashes
* [QTBUG-122699](https://qt-project.atlassian.net/browse/QTBUG-122699) Failed DCHECK in v8 when watching livestream
* [QTBUG-120247](https://qt-project.atlassian.net/browse/QTBUG-120247) [Qt WebEngine] Make it easier to re-configure after
installing missing libraries for qpa-xcb support
* [QTBUG-124632](https://qt-project.atlassian.net/browse/QTBUG-124632) QtWebengine needs to be skipped with Windows 11 on ARM
* [QTBUG-124558](https://qt-project.atlassian.net/browse/QTBUG-124558) Top flaky test:
tst_qwebengineglobalsettings::dnsOverHttps on Windows_11_22H2 X86_64 and
QUEMU
* [QTBUG-122469](https://qt-project.atlassian.net/browse/QTBUG-122469) Top flaky test:
tst_qwebengineprofile::clearDataFromCache on MacOS_13 ARM64.
* [QTBUG-123790](https://qt-project.atlassian.net/browse/QTBUG-123790) Large number of warnings are output when exiting
QWebEngineView.
* [QTBUG-126049](https://qt-project.atlassian.net/browse/QTBUG-126049) text dump does not work realibly with 122-based
* [QTBUG-123500](https://qt-project.atlassian.net/browse/QTBUG-123500) Unable to read out javascript engine version
* [QTBUG-126085](https://qt-project.atlassian.net/browse/QTBUG-126085) QQuickWebEngineProfile::defaultProfile() doesn't produce
a working profile
* [QTBUG-126546](https://qt-project.atlassian.net/browse/QTBUG-126546) Attribution documentation processed twice in CI
* [QTBUG-112281](https://qt-project.atlassian.net/browse/QTBUG-112281) Support ANGLE on Linux
* [QTBUG-127110](https://qt-project.atlassian.net/browse/QTBUG-127110) Platforms still use the inefficient qvsnprintf() fall-
back
* [QTBUG-126655](https://qt-project.atlassian.net/browse/QTBUG-126655) QtWebEngine fails Yocto CI build
* [QTBUG-128308](https://qt-project.atlassian.net/browse/QTBUG-128308) [Windows] Startup crash in
gl::GLContextEGL::Initialize() on AMD GPUs
* [QTBUG-128653](https://qt-project.atlassian.net/browse/QTBUG-128653) tst_qquickwebengineview failed on
ubuntu-24.04-arm64-offscreen-tests
* [QTBUG-128652](https://qt-project.atlassian.net/browse/QTBUG-128652) tst_qmltests crashed on ubuntu-24.04-arm64-offscreen-
tests
* [QTBUG-126317](https://qt-project.atlassian.net/browse/QTBUG-126317) libexec/gn on MacOS is not universal
* [QTBUG-131607](https://qt-project.atlassian.net/browse/QTBUG-131607) Crash on NativeSkiaOutputDeviceDirect3D11::texture()
with nullptr access
* [QTBUG-117478](https://qt-project.atlassian.net/browse/QTBUG-117478) qtwebengine h264 broken on Windows
* [QTBUG-132479](https://qt-project.atlassian.net/browse/QTBUG-132479) [Windows] After download is interrupted,
QWebEngineDownloadRequest::resume() crashes with "Observers can only be
added once!"
* [QTBUG-132473](https://qt-project.atlassian.net/browse/QTBUG-132473) QWebEngineDownloadRequest::DownloadInterrupted creates
multiple, inconsistent QWebEngineDownloadRequest objects
* [QTBUG-133970](https://qt-project.atlassian.net/browse/QTBUG-133970) QtPDF spdx files not included in MinGW content
* [QTBUG-131434](https://qt-project.atlassian.net/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-135040](https://qt-project.atlassian.net/browse/QTBUG-135040) macos: Voice Over rect is wrongly calculated for
WebEngine
* CVE-2024-12693: Out of bounds memory access in V8
* CVE-2024-12694: Use after free in Compositing
* CVE-2024-55549: Fix UAF related to excluded namespaces
* CVE-2024-11477 / Security bug 383772517
* CVE-2025-0437: Out of bounds read in Metrics
* CVE-2025-0441: Inappropriate implementation in Fenced Frames
* CVE-2025-0443: Insufficient data validation in Extensions
* CVE-2025-0436: Integer overflow in Skia
* CVE-2025-0438: Stack buffer overflow in Tracing
* CVE-2025-0447: Inappropriate implementation in Navigation
* CVE-2025-0611: Object corruption in V8
* CVE-2025-0762: Use after free in DevTools
* CVE-2025-0996: Inappropriate implementation in Browser UI
* CVE-2025-0998: Out of bounds memory access in V8
* CVE-2025-0999: Heap buffer overflow in V8
* CVE-2025-1006: Use after free in Network
* CVE-2025-1426: Heap buffer overflow in GPU
* CVE-2025-1915
* CVE-2025-1918
* CVE-2025-1919
* CVE-2025-1921
* CVE-2025-2136
* CVE-2025-2783: Incorrect handle provided in unspecified circumstances in Mojo on Windows
* CVE-2025-3071: Inappropriate implementation in Navigations
* CVE-2025-3619
* CVE-2025-4051: Insufficient data validation in DevTools
* CVE-2025-4052: Inappropriate implementation in DevTools
* CVE-2025-4609: Incorrect handle provided in unspecified circumstances in Mojo
* CVE-2025-4664: Insufficient policy enforcement in Loader
* CVE-2025-24201
* CVE-2025-24855 Fix use-after-free of XPath context node
* Security bug 359992017
* Security bug 378541479
* Security bug 378701682
* Security bug 378725734
* Security bug 378917565
* Security bug 379418979
* Security bug 379715150
* Security bug 379869752
* Security bug 382135228
* Security bug 383772517
* Security bug 384565015
* Security bug 385386138
* Security bug 389707046
* Security bug 390465670
* Security bug 396460489
* Security bug 396481096
* Security bug 397187119
* Security bug 399002829
* Security bug 403364367
* Security bug 409243443
* Security bug 413080347
* Security bug 414858409

### qtvirtualkeyboard
* [QTBUG-127557](https://qt-project.atlassian.net/browse/QTBUG-127557) QtVirtualKeyboard crash introduced in 6.5.4
* [QTBUG-131347](https://qt-project.atlassian.net/browse/QTBUG-131347) Incorrect decimal point for German keyboard

### qtscxml
* [QTBUG-132510](https://qt-project.atlassian.net/browse/QTBUG-132510) Superfluous optional components

### qtspeech
* [QTBUG-117516](https://qt-project.atlassian.net/browse/QTBUG-117516) [Qt TextToSpeech] Cannot get the list of languages on
android device

### qtnetworkauth
* [QTBUG-131948](https://qt-project.atlassian.net/browse/QTBUG-131948) OAuth2 expirationAt doest not change when invalidated
* [QTBUG-131949](https://qt-project.atlassian.net/browse/QTBUG-131949) Use UTC instead of local time for internal expiresAt
representation
* [QTBUG-135257](https://qt-project.atlassian.net/browse/QTBUG-135257) NetworkAuth Coverity findings

### qt5compat
* [QTBUG-122798](https://qt-project.atlassian.net/browse/QTBUG-122798) [REG 5.15 -> 6.7 (or earlier)] QStringRef -> QStringView
conversion loses null-ness
* [QTBUG-122797](https://qt-project.atlassian.net/browse/QTBUG-122797) QStringRef doesn't convert to QAnyStringView

### qtquick3dphysics
* [QTBUG-134277](https://qt-project.atlassian.net/browse/QTBUG-134277) [clang-cl] PhysX build failure

### qtapplicationmanager (Commercial only)
* [QTBUG-134539](https://qt-project.atlassian.net/browse/QTBUG-134539) Failed to verify signature (no chain of trust)

### qtinterfaceframework (Commercial only)
* [QTBUG-134742](https://qt-project.atlassian.net/browse/QTBUG-134742) The documentation and the snippet seem to be
contradicting

Known Issues
------------

* Check that your system meets Qt's requirements:
https://doc.qt.io/qt-6.5/supported-platforms.html

* The RTA (release test automation) reported issues in Qt 6.5.x:
https://qt-project.atlassian.net/issues/?filter=15085

* See Qt 6.5 known issues from:
https://wiki.qt.io/Qt_6.5_Known_Issues

* Qt 6.5.9 Open issues in Jira:
https://qt-project.atlassian.net/issues/?filter=15048

Credits for the release goes to:
---------------------------------

* Eirik Aavitsland
* Anu Aliyas
* Karolina Sofia Bang
* Vladimir Belyavsky
* Nicholas Bennett
* Tim Blechmann
* Eskil Abrahamsen Blomfeldt
* Joerg Bornemann
* Rym Bouabid
* Assam Boudjelthia
* Kai Uwe Broulik
* Michael Brüning
* Benjamin Buch
* Olivier De Cannière
* Alexei Cazacov
* Kaloyan Chehlarski
* Albert Astals Cid
* Alexandru Croitor
* Mitch Curtis
* Giuseppe D'Angelo
* Szabolcs David
* Pavel Dubsky
* Artem Dyomin
* Alexey Edelev
* David Edmundson
* Oliver Eftevaag
* Christian Ehrlicher
* Andreas Eliasson
* Fabio Falsini
* David Faure
* Nicolas Fella
* Alexander Golubev
* Robert Griebl
* Johannes Grunenberg
* Richard Moe Gustavsen
* Lucie Gérard
* Mikko Hallamaa
* Jøger Hansegård
* Jani Heikkinen
* Moss Heim
* Ulf Hermann
* Volker Hilsheimer
* Dominik Holland
* Botond István Horváth
* Allan Sandfeld Jensen
* Teemu Jokitulppo
* Jonas Karlsson
* Friedemann Kleint
* Michal Klocek
* Sze Howe Koh
* Niko Korkala
* Fabian Kosmale
* Santhosh Kumar
* Kai Köhne
* Inho Lee
* Frédéric Lefebvre
* Paul Lemire
* Wladimir Leuschner
* Robert Löhning
* Thiago Macieira
* Ievgenii Meshcheriakov
* Safiyyah Moosa
* Bartlomiej Moskal
* Marc Mutz
* Martin Negyokru
* Andy Nichols
* Mårten Nordheim
* Dennis Oberst
* Samuli Piippo
* Timur Pocheptsov
* Joni Poikelin
* Rami Potinkara
* Dheerendra Purohit
* MohammadHossein Qanbari
* Liang Qi
* Khem Raj
* Matthias Rauter
* Topi Reinio
* Shawn Rutledge
* Ahmad Samir
* Lars Schmertmann
* Sami Shalayel
* Tian Shilin
* Kristoffer Skau
* Nils Petter Skålerud
* Ivan Solovev
* Axel Spoerl
* Patryk Stachniak
* Patrick Stewart
* Magdalena Stojek
* Christian Strømme
* Tarja Sundqvist
* Audun Sutterud
* Lars Sutterud
* Tasuku Suzuki
* Jan Arve Sæther
* Nodir Temirkhodjaev
* Tuomas Vaarala
* Peter Varga
* Doris Verria
* Tor Arne Vestbø
* Juha Vuolle
* Olli Vuolteenaho
* Jaishree Vyas
* Michael Weghorn
* Edward Welbourne
* Paul Wicking
* Milian Wolff
* Oliver Wolff
* Semih Yavuz
* Yansheng Zhu
