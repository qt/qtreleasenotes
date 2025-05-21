Release note
============
Qt 6.9.1 release is a patch release made on the top of Qt 6.9.0.
As a patch release, Qt 6.9.1 does not add any new functionality but provides
bug fixes and other improvements and maintains both forward and backward
compatibility (source and binary) with Qt 6.9.0.

For detailed information about Qt 6.9, refer to the online documentation
included in this distribution. The documentation is also available online:

https://doc.qt.io/qt-6/index.html

The Qt version 6.9 series is binary compatible with the 6.8.x series.
Applications compiled for 6.8 will continue to run with 6.9.

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
N/A

### qtbase
* de3cf05b77e QUrl: decode square brackets in fromLocalFile()
' to their percent-encoded forms. This will be visible in calls to
toString(), toEncoded(), or the encoded form of path(). QUrl's
comparison operator will consider the old (created from an encoded URL
string) and new forms to be different.

* bf37860a719 Upgrade Harfbuzz to 10.4.0
Upgraded Harfbuzz to version 10.4.0.

* 26cda01b299 Distinguish system locale from corresponding CLDR-derived
one
Message logging now distinguishes the system locale from the
corresponding locale - generated from its language, script and territory
- based on CLDR data.

* 8e94b67ba11 CBOR/JSON: fix crash when comparing strings with different
length
Fixed bug that could result in a crash or failing to find a entry in
the map/object with non- ASCII keys.

* cd395a79993 3rdparty: update TinyCBOR to v0.6.1
The copy of TinyCBOR in Qt was updated to 0.6.1.

* 8287fb63ef6 QConcatenateTablesProxyModel: cache roleNames()
The roleNames property is only updated (lazily) on addSourceModel() and
removeSourceModel() now (was: on every call of the function). If your
source models change their roleNames() dynamically, you need to call
invalidateRoleNamesCache() manually when they do.

* a833d93f595 Only default top levels to
Qt::WA_ContentsMarginsRespectsSafeArea
The Qt::WA_ContentsMarginsRespectsSafeArea attribute is no longer set
by default for non-top-level widgets. Top level widgets still default to
Qt::WA_ContentsMarginsRespectsSafeArea=true, so children are laid out in
the safe areas, but overriding the attribute for the top level now
allows placing widgets in the non-safe areas without also setting the
Qt::WA_ContentsMarginsRespectsSafeArea attribute to false for every
descendant widget that overlaps the non-safe area.

* d027d6d9da0 QUuid: fix qHash() on 64-bit platforms
Improved the performance of the qHash() function on 64-bit platforms by
populating all bits of the output (was: only lower 32 bits).

* 10e546f015e QNetworkAccessManager: don't resend non-idempotent
requests
Non-idempotent requests are no longer incorrectly re-sent if the
connection breaks down while reading the response.

* 469c071d698 QVariant/QMetaType: fix conversions to/from qfloat16
Implemented converting of qfloat16 to and from the other numeric types,
text conversions to and from QString and QByteArray, and conversions to
and from QJsonValue and QCborValue. This should make qfloat16 behave the
same as float and double.

* b7585188961 JSON/CBOR: fix conversions from QVariant containing longs
and qfloat16
Fixed conversions from QVariant when the variant contained long,
unsigned long, or qfloat16.

* 4ac20b3e5ae Pass VxWorks touch ranges via environment variable
The user can now override touch ranges that the driver returns, by
setting the new parameters "rangex" and "rangey" on the environment
variable QT_QPA_VXEVDEV_TOUCHSCREEN_PARAMETERS with comma-separated min
and max touch ranges for X and Y axis respectively. For example, add
rangex=10,815:rangey=15,1024

* a9418f0ab5a Account for rounding error when rounding height metrics
Fixed an issue where the line distance for hinted fonts would be off by
one for specific sizes of some fonts.

* 6a684a53b37 QFileSystemEngine/Win: Use GetTempPath2 when available
On Windows, generating temporary directories for processes with
elevated privileges may now return a different path with a stricter set
of permissions. Please consult Microsoft's documentation from when they
made the same change for the .NET framework:
https://support.microsoft.com/en-us/topic/gettemppath-changes-in-
windows-february-cumulative-update-
preview-4cc631fb-9d97-4118-ab6d-f643cd0a7259

* 9e59a924a04 QTextMarkdownImporter: Fix heap-buffer-overflow
Fixed a heap buffer overflow in QTextMarkdownImporter. The first marker
for Front Matter must begin at the first character of a Markdown
document, and both markers must be exactly ---\n or ---\r\n.

* cfda487726e QXmlStreamReader::addData: lock encoding for QLatin1 case
Fixed a bug when calling addData() with a Latin1-encoded string
containing a full XML document with an encoding attribute, could result
in incorrect parsing of this document.

* 01ff6e19f7a QUrl: expand the square brackets encoding to decoded
setPath() calls
") are now transformed to their percent-encoded forms ("%5B" and "%5D")
when present as inputs to setPath(), setQuery(), and setFragment() if
the parsing mode is QUrl::DecodedMode (the default).

* a1b4480c531 Upgrade Harfbuzz to 11.0.0
Upgraded Harfbuzz to version 11.0.0.

* 6a8b3344c09 QPointer: don't cause UB when checking for nullptr
For `QPointer<Derived> p`, `!p` and comparing `p` to nullptr no longer
perform invalid downcasts when the object held in `p` is in the process
of being destroyed and has already been demoted from Derived to one of
its base classes. Before, these expressions invoked data(), which casts
from QObject* to Derived*, a cast which is invalid.

* ec8f043ec51 QXmlStreamReader: fix addData() unnecessary conversion to
UTF-8
Fixed a bug when addData(QAnyStringView) was incorrectly recoding
UTF-16 and Latin1 data to UTF-8, thus potentially mangling it.

* 95f659aedab windeployqt: Deploy Qt dependencies of local non Qt
dependencies
windeployqt now takes local non Qt dependencies into consideration
during deployment.

* 62f382f2711 QStringConverter: widen nameForEncoding()'s contract
The nameForEncoding() function now returns nullptr for an invalid
Encoding value. Before, such a call resulted in undefined behavior.

* 4f89fbc9a9e Make F11 the fullscreen keyboard shortcut on Gnome (as on
KDE & Windows)
The fullscreen keyboard shortcut is now F11 on Gnome, not Ctrl-F11.

* 4b20e23ed7a QAbstractSlider: fix missing "emission" of
SliderOrientationChange
Fixed the missing "emission" of protected
sliderChange(SliderOrientationChange).

* bb8acc8e0e7 Upgrade Harfbuzz to 11.1.0
Upgraded Harfbuzz to version 11.1.0.

* 21cd27b3b99 qDecodeDataUrl(): fix precondition violation in call to
QByteArrayView::at()
Fixed a bug in the handling of data: URLs that could lead to a crash if
Qt was built with assertions enabled. This affects QNetworkManager and
links in QTextDocument.

* 1e486c14d4b Fix long-form zone parts in date-time strings
The tttt format specifier now uses the full long name of the zone,
falling back to its IANA ID only if this cannot be determined. Both
forms are now recognized when reading a datetime from a string.

* 63093b04105 SQLite: Update SQLite to v3.49.2
Updated SQLite to v3.49.2

* 60cf2f867b2 Upgrade Harfbuzz to 11.2.1
Upgraded Harfbuzz to version 11.2.1.

* 55edaffa7cc Update bundled libpng to version 1.6.48
libpng was updated to version 1.6.48

### qtdeclarative
* 216156f164 StackView: Use PushTransition for pushItem(s)
The default operation for pushItem(s) is now PushTransition as
documented. Previously, Immediate was used.

* 167b4b6057 Auto-depend on QtQuick when linking against QtQuick
If a QML module target is linked against Qt6::Quick, QtQuick is
automatically added to its QML dependencies. This avoids tooling errors
when e.g. a QQuickItem derived type is exported by the module.

* 61c15cb94f TableView: emit commit on editor loss of focus, unless
Qt::Key_Escape
The edit delegate will now emit the onCommit signal when it loses
focus, unless it was closed from Qt::Key_Escape.

* a85de80908 QQuickPopupItem: Set tabFence to be true by default
The popupItem always acts as a tab fence, preventing tab focus
navigation in and out of the popup, except when the popup is a Drawer,
in which case this behavior depends on the drawer's modality.

* 4fc898246a Close all other Menus when showing non-sub-menu
All non-sub-menus are now closed when a menu is opened. This is to fix
an issue (QTBUG-134903) where duplicate menus are shown when opening a
custom non-ContextMenu on a text editing control like TextField or
TextArea. This means that rather than two context menus incorrectly
being opened, an extra one will briefly be visible before immediately
being closed. For information on how to avoid this, please see the
"Context menus" section of Menu's documentation.

* 1c3bbebb23 QQmlBind: Only restore previous state if current state is
still active
The Binding element now only restores previous bindings or values if
its own binding is still active on destruction or changes to its "when"
property. If it has been overridden by another Binding element, it will
not disable that one anymore.

* 842210ac62 QtQml: Do not check revisions when resolving aliases
You can now create aliases to revisioned properties that would be
unavailable when accessed without qualification. Aliases are always
qualified after all.

### qtmultimedia
* bac0163d0 QMake: Add possibility to link and embed FFmpeg frameworks
on iOS
Added the CONFIG value add_ios_ffmpeg_libraries that can be used in iOS
apps that need FFmpeg frameworks for QtMultimedia.

### qt3d
* bcdee8075 Make module ready for source SBOM checking
Renaming the license files with prefix LICENSE. to have them ignored by
reuse tool.

### qtquick3d
* 5d1ea1280 Update TinyEXR to v1.0.12
Updated TinyEXR to v1.0.12

### qtopcua
* 251cec4e Fix handling of ByteString node ids with null bytes
Fix a bug that prevented ByteString node ids    with null bytes from
being used.

### qtinterfaceframework (Commercial only)
* 994c52f2 Update license check
Rename license file with LICENSE. prefix. This way the file is ignored
by the reuse tool.


Fixes
-----

### qtbase
* [QTBUG-134073](https://bugreports.qt.io/browse/QTBUG-134073) QMimeData does not escape square brackets in text/uri-
list
* [QTBUG-134101](https://bugreports.qt.io/browse/QTBUG-134101) Qt 6.9.0 with uncompressed libraries doesn't work with
split APKs
* [QTBUG-107904](https://bugreports.qt.io/browse/QTBUG-107904) Qt Designer crashes when set a negative value in border-
image
* [QTBUG-131893](https://bugreports.qt.io/browse/QTBUG-131893) QToolButton menu selections fail to highlight when in
QMdiSubwindow
* [QTBUG-115356](https://bugreports.qt.io/browse/QTBUG-115356) QMenu clips text for actions with icons with larger
fonts
* [QTBUG-134210](https://bugreports.qt.io/browse/QTBUG-134210) Infinite recursion of a QSortFilterProxyModel with a
QConcatenateTablesProxyModel  as source
* [QTBUG-131256](https://bugreports.qt.io/browse/QTBUG-131256) QTextEdit will block and crash by
QEventLoop::WaitForMoreEvents when  pressing or dragging selected text
* [QTBUG-132187](https://bugreports.qt.io/browse/QTBUG-132187) QDrawUtil: qDrawPlainRoundedRect does not work well for
high-dpi screens
* [QTBUG-134235](https://bugreports.qt.io/browse/QTBUG-134235) Build failure of qtbase/src/widgets/styles/qdrawutil.cpp
with disabled features
* [QTBUG-132705](https://bugreports.qt.io/browse/QTBUG-132705) Qt CMake content uses compiler config from qtbase,
instead the current modules
* [QTBUG-134392](https://bugreports.qt.io/browse/QTBUG-134392) Copyright holder missing
qtbase/config.tests/armintrin/main.cpp
* [QTBUG-133406](https://bugreports.qt.io/browse/QTBUG-133406) Unrechable code in MetaTypeQFutureHelper
* [QTBUG-134316](https://bugreports.qt.io/browse/QTBUG-134316) [Reg] QFileOpenEvent isn't emitted for custom URI
* [QTBUG-133412](https://bugreports.qt.io/browse/QTBUG-133412) QFileDialog drive icons incorrect scaling on screen with
non-integer device pixel ratio
* [QTBUG-132929](https://bugreports.qt.io/browse/QTBUG-132929) QStyleHints::setColorScheme() doesn't affect the
application's theme on Ubuntu
* [QTBUG-133922](https://bugreports.qt.io/browse/QTBUG-133922) fr_CH is listed twice by QLocale::matchingLocales
* [QTBUG-134393](https://bugreports.qt.io/browse/QTBUG-134393) qtwasmserver doesn't use the provided path parameter to
serve assets
* [QTBUG-134473](https://bugreports.qt.io/browse/QTBUG-134473) Font rendering of Qt Creators Text Editor is broken
* [QTBUG-134415](https://bugreports.qt.io/browse/QTBUG-134415) Qt FTBFS with GCC < 15 + TSAN + PCH + developer-build
* [QTBUG-133744](https://bugreports.qt.io/browse/QTBUG-133744) QString assertion failure using UTF-16 character in
QJsonObject key
* [QTBUG-134533](https://bugreports.qt.io/browse/QTBUG-134533) Fusion style: SH_EtchDisabledText in disable QMenu looks
blurry
* [QTBUG-125534](https://bugreports.qt.io/browse/QTBUG-125534) qt-internal-{ninja,strip}.bat.in are installed as
executable
* [QTBUG-134538](https://bugreports.qt.io/browse/QTBUG-134538) QRandomGenerator, QSimd: RDSEED should be checked for
validity
* [QTBUG-130063](https://bugreports.qt.io/browse/QTBUG-130063) QKeySequence(<QString>) doesn't parse correctly when we
have a space
* [QTBUG-133942](https://bugreports.qt.io/browse/QTBUG-133942) Qt::ExpandedClientAreaHint results in losing default
window title on Windows
* [QTBUG-134080](https://bugreports.qt.io/browse/QTBUG-134080) "QObject::~QObject: Timers cannot be stopped from
another thread" message in Qt 6.8.2 plugins
* [QTBUG-133861](https://bugreports.qt.io/browse/QTBUG-133861) [macOS] QML Preview: Closing the preview window produces
QObject::killTimer warning
* [QTBUG-132697](https://bugreports.qt.io/browse/QTBUG-132697) FAIL!  :
tst_QQmlDebugJS::setBreakpointInScriptThatQuits(custom)
'm_process->waitForFinished()' returned FALSE.
* [QTBUG-102984](https://bugreports.qt.io/browse/QTBUG-102984) QML debugger and profiler tests hangs on macOS/x86_64 in
CI
* [QTBUG-132381](https://bugreports.qt.io/browse/QTBUG-132381) [REG 6.8 -> 6.9] Crash when QGuiApplication is static
* [QTBUG-40283](https://bugreports.qt.io/browse/QTBUG-40283) QSettings: Documentation and implementation differ
* [QTBUG-134075](https://bugreports.qt.io/browse/QTBUG-134075) Windows Server 2016 is no longer working
* [QTBUG-134497](https://bugreports.qt.io/browse/QTBUG-134497) Mouse hover stylesheet does not renders correct color in
windows11
* [QTBUG-134699](https://bugreports.qt.io/browse/QTBUG-134699) Performance regression in QDirIterator when going from
6.5.3 to 6.8.2 [REG 6.5.3->6.8.2]
* [QTBUG-133710](https://bugreports.qt.io/browse/QTBUG-133710) Fix padding in tabs for pre elements
* [QTBUG-133702](https://bugreports.qt.io/browse/QTBUG-133702) [Android] QDesktopServices::openUrl(): FileProvider
unable to get URI for sharing file
* [QTBUG-134447](https://bugreports.qt.io/browse/QTBUG-134447) Modal dialog looks disabled
* [QTBUG-133941](https://bugreports.qt.io/browse/QTBUG-133941) Qt::ExpandedClientAreaHint results in losing window icon
on Windows
* [QTBUG-133945](https://bugreports.qt.io/browse/QTBUG-133945) Qt::ExpandedClientAreaHint results in wrong color for
close button on Windows
* [QTBUG-15125](https://bugreports.qt.io/browse/QTBUG-15125) QDomAttr QDomElement::setAttributeNode ( const QDomAttr &
newAttr ) does NOT replaces attribute with the same name as newAttr.
* [QTBUG-28721](https://bugreports.qt.io/browse/QTBUG-28721) QXmlStreamWriter writes newline at beginning of stream if
auto formatting is enabled.
* [QTBUG-133834](https://bugreports.qt.io/browse/QTBUG-133834) Fusion Style: QMdiArea close button looks clipped with
fractional scaling
* [QTBUG-134768](https://bugreports.qt.io/browse/QTBUG-134768) QLocale::toStrings uses E instead of e
* [QTBUG-134785](https://bugreports.qt.io/browse/QTBUG-134785) Provide QLocale::toString() floating-point formats for
locale-appropriate case of exponent
* [QTBUG-134694](https://bugreports.qt.io/browse/QTBUG-134694) QNetworkAccessManager re-sends destructive requests
(POST, possibly others) without user intervention
* [QTBUG-134930](https://bugreports.qt.io/browse/QTBUG-134930) [REG 6.9] QLabel scaled pixmap is broken
* [QTBUG-134756](https://bugreports.qt.io/browse/QTBUG-134756) QJsonValue::fromVariant converts integers incorrectly
* [QTBUG-134313](https://bugreports.qt.io/browse/QTBUG-134313) can't drag application/x-color from one Qt application
to another (is it hex or raw?)
* [QTBUG-130912](https://bugreports.qt.io/browse/QTBUG-130912) [Windows] Child window with Qt.WindowDoesNotAcceptFocus
flag set still grabs focus
* [QTBUG-134610](https://bugreports.qt.io/browse/QTBUG-134610) Disconnect all -> crash in QAccessibilityCache
* [QTBUG-132459](https://bugreports.qt.io/browse/QTBUG-132459) Windows11 style: QProgressBar needs some work
* [QTBUG-132310](https://bugreports.qt.io/browse/QTBUG-132310) Crash in QCocoaAccessible::shouldBeIgnored
* [QTBUG-134702](https://bugreports.qt.io/browse/QTBUG-134702) QT_QPA_PLATFORMTHEME=generic doesn't work on KDE and GTK
environments
* [QTBUG-134703](https://bugreports.qt.io/browse/QTBUG-134703) Setting XDG_CURRENT_DESKTOP to xdgdesktopportal, flatpak
or snap causes an instant crash
* [QTBUG-134602](https://bugreports.qt.io/browse/QTBUG-134602) Rendering of QQuickText slightly elevated.
* [QTBUG-130576](https://bugreports.qt.io/browse/QTBUG-130576) Touches Are Handled Incorrectly with QDialog on Qt 6.8.x
Android
* [QTBUG-127925](https://bugreports.qt.io/browse/QTBUG-127925) Touch events end up in wrong place with Widgets gallery
on Android
* [QTBUG-135109](https://bugreports.qt.io/browse/QTBUG-135109) some POSIX-style TZ strings are not supported by Qt on
some Linux-based platform
* [QTBUG-135159](https://bugreports.qt.io/browse/QTBUG-135159) QIcon::fromTheme selects 32px icon instead of 16@2x with
devicePixelRatio 2
* [QTBUG-127517](https://bugreports.qt.io/browse/QTBUG-127517) Reports of misaligned loads with asan on AArch64 / xcb
* [QTBUG-134788](https://bugreports.qt.io/browse/QTBUG-134788) Copyright footer shows previous year
* [QTBUG-76976](https://bugreports.qt.io/browse/QTBUG-76976) QSortFilterProxyModel::mapFromSource returns a valid
QModelIndex for the filtered out item
* [QTBUG-134626](https://bugreports.qt.io/browse/QTBUG-134626) [6.8.1 -> 6.8.2] Thicker text underline with certain
fonts (X11)
* [QTBUG-134784](https://bugreports.qt.io/browse/QTBUG-134784) macos: Crash in Voice Over/Accessiblity when resetting a
table model
* [QTBUG-135238](https://bugreports.qt.io/browse/QTBUG-135238) QDateTime::toTimeZone doc's code snippet calls
deprecated ::toTimeSpec
* [QTBUG-135163](https://bugreports.qt.io/browse/QTBUG-135163) QThread::isRunning returns false while the thread is
still running
* [QTBUG-135033](https://bugreports.qt.io/browse/QTBUG-135033) QXmlStreamReader::addData() can parse Latin1 data
incorrectly
* [QTBUG-134634](https://bugreports.qt.io/browse/QTBUG-134634) tst_QUuid::uint128 fails on big-endian
* [QTBUG-135287](https://bugreports.qt.io/browse/QTBUG-135287) QDirIterator::next no longer returns "" upon iterator
exhaustion
* [QTBUG-130142](https://bugreports.qt.io/browse/QTBUG-130142) 6.8 Regresssion:  QDirIterator::next segfaults
* [QTBUG-135264](https://bugreports.qt.io/browse/QTBUG-135264) Error in qml qmake project with qt 6.8.3
* [QTBUG-135225](https://bugreports.qt.io/browse/QTBUG-135225) qtbase build fails without process(environment) feature
* [QTBUG-135230](https://bugreports.qt.io/browse/QTBUG-135230) Configuring xmlstreamreader out of the build fails
* [QTBUG-135152](https://bugreports.qt.io/browse/QTBUG-135152) qtbase build fails if configured with -no-feature-
desktopservices
* [QTBUG-135338](https://bugreports.qt.io/browse/QTBUG-135338) Sorting indicator size not honored in itemview header
with windows11 style
* [QTBUG-135135](https://bugreports.qt.io/browse/QTBUG-135135) QMySqlDriver QDateTime is not consistant between
read/write
* [QTBUG-135471](https://bugreports.qt.io/browse/QTBUG-135471) tst_QXmlStream does not test non-wellformed documents
properly
* [QTBUG-135433](https://bugreports.qt.io/browse/QTBUG-135433) QUrl::setPath and QUrl::fromUserInput encodes local
paths differently from QUrl::fromLocalFile
* [QTBUG-134807](https://bugreports.qt.io/browse/QTBUG-134807) macos: Voice Over/Accessiblity for tabs is lacking
* [QTBUG-135620](https://bugreports.qt.io/browse/QTBUG-135620) Qt6WebEngineCoreDeploySupport fails when generating RPM
* [QTBUG-109553](https://bugreports.qt.io/browse/QTBUG-109553) CMake deployment API creates too deep directory
hierarchy when DESTDIR is set
* [QTBUG-135340](https://bugreports.qt.io/browse/QTBUG-135340) Regression: Stylesheet breaks QGraphicsProxyWidget
* [QTBUG-128916](https://bugreports.qt.io/browse/QTBUG-128916) QComboBox drop down is not visible on Windows11 in some
situation
* [QTBUG-128329](https://bugreports.qt.io/browse/QTBUG-128329) qt combobox 放入到QGraphicsProxyWidget下拉框不显示
* [QTBUG-135628](https://bugreports.qt.io/browse/QTBUG-135628) QCheckbox without text is right cropped
* [QTBUG-133117](https://bugreports.qt.io/browse/QTBUG-133117) Windows11Style: Check boxes and radio buttons slightly
cropped at 150%
* [QTBUG-135609](https://bugreports.qt.io/browse/QTBUG-135609) Build failure when building iOS on macOS
* [QTBUG-133963](https://bugreports.qt.io/browse/QTBUG-133963) [REG Qt 6.5 -> 6.7] Shortcuts on macOs using
Meta/Command require Shift as well
* [QTBUG-99957](https://bugreports.qt.io/browse/QTBUG-99957) No rule to make target 'qtbase/src/platformsupport/input/
CMakeFiles/InputSupportPrivate.dir/cmake_pch.hxx.gch
* [QTBUG-135650](https://bugreports.qt.io/browse/QTBUG-135650) [6.9.0] Build error during bootstrap
* [QTBUG-135294](https://bugreports.qt.io/browse/QTBUG-135294) Duplicate data tags in tst_qgraphicslinearlayout
* [QTBUG-135578](https://bugreports.qt.io/browse/QTBUG-135578) Possible QTimer ABI break between Qt 6.7 and Qt 6.9
* [QTBUG-54484](https://bugreports.qt.io/browse/QTBUG-54484) QSortFilterProxyModel crash on filter item out
* [QTBUG-50821](https://bugreports.qt.io/browse/QTBUG-50821) QSortFilterProxyModel crash when dataChanged during
setFilter*
* [QTBUG-134139](https://bugreports.qt.io/browse/QTBUG-134139) Windows: Qt::Popup window has wrong initial size on
system with displays with different DPI scales
* [QTBUG-135044](https://bugreports.qt.io/browse/QTBUG-135044) tst_QStringApiSymmetry fails under ASAN
(GenerationalCollator is leaked?)
* [QTBUG-135619](https://bugreports.qt.io/browse/QTBUG-135619) QVariant::canConvert behaves inconsistently with the
documentation
* [QTBUG-135285](https://bugreports.qt.io/browse/QTBUG-135285) QVariant::toInt() asserts if the contained real number
exceeds integer limits
* [QTBUG-135076](https://bugreports.qt.io/browse/QTBUG-135076) [QNX] Stale QNX Screen events under load
* [QTBUG-135129](https://bugreports.qt.io/browse/QTBUG-135129) QXmlStreamReader::addData(QASV) overload unconditionally
converts UTF-16 and L1 to UTF-8
* [QTBUG-135806](https://bugreports.qt.io/browse/QTBUG-135806) qtbase autotests to compile without draganddrop
* [QTBUG-135442](https://bugreports.qt.io/browse/QTBUG-135442) QDockWidget/QMainWindow leak widgetItems from
QDockAreaLayoutItem on dragging and QDockWidget::close()
* [QTBUG-134881](https://bugreports.qt.io/browse/QTBUG-134881) android_content_uri test crashes during test process.
* [QTBUG-132191](https://bugreports.qt.io/browse/QTBUG-132191) wasm: QTcpSocket signals connected rather errorOccurred
* [QTBUG-135648](https://bugreports.qt.io/browse/QTBUG-135648) [REG 6.7->6.8] macOS: FindWrapResolv.cmake fails
check_cxx_source_compiles with strict flags (-Werror -Wzero-as-null-
pointer-constant)
* [QTBUG-133923](https://bugreports.qt.io/browse/QTBUG-133923) Missing documentation for QFlags' equality operators
* [QTBUG-135079](https://bugreports.qt.io/browse/QTBUG-135079) windeployqt missing plugins
* [QTBUG-135640](https://bugreports.qt.io/browse/QTBUG-135640) Data race in QPointer
(QtSharedPointer::ExternalRefCountData::getAndRef)
* [QTBUG-135636](https://bugreports.qt.io/browse/QTBUG-135636) tst_QTimer::crossThreadSingleShotToFunctor() leaks
(almost) all timers
* [QTBUG-135854](https://bugreports.qt.io/browse/QTBUG-135854) Qt Keyboard Shortcut: Fullscreen incorrectly mapped in
GNOME
* [QTBUG-135933](https://bugreports.qt.io/browse/QTBUG-135933) QMenus with a layout and widgets are no longer shown
* [QTBUG-129108](https://bugreports.qt.io/browse/QTBUG-129108) Menus and action visibility
* [QTBUG-135597](https://bugreports.qt.io/browse/QTBUG-135597) QAbstractSlider is not using SliderOrientationChange
* [QTBUG-136019](https://bugreports.qt.io/browse/QTBUG-136019)  c1: fatal error C1083: Cannot open source file: 'C:\Use
rs\qt\work\qt\qt3d_build\src\plugins\renderers\opengl\debug\OpenGLRender
erPlugin_resource.rc': No such file or directory
* [QTBUG-11967](https://bugreports.qt.io/browse/QTBUG-11967) QDateEdit/CalendarPopup(true) has incorrect sizing
* [QTBUG-136079](https://bugreports.qt.io/browse/QTBUG-136079) error: 'QPixmapCache' has not been declared
* [QTBUG-134695](https://bugreports.qt.io/browse/QTBUG-134695) [REG] QPdfWriter: embed font issue: generates very big
pdf file on windows : the workaround doesn't work anymore
* [QTBUG-135950](https://bugreports.qt.io/browse/QTBUG-135950) Cocoa window: Updates are not received
* [QTBUG-136042](https://bugreports.qt.io/browse/QTBUG-136042) Qt MySQL driver does not add milliseconds for QDateTime
in formatValue()
* [QTBUG-95071](https://bugreports.qt.io/browse/QTBUG-95071) mysql client version detection broken with MariaDB 10.6
* [QTBUG-136024](https://bugreports.qt.io/browse/QTBUG-136024) The oracle OCI SQl Plugin is unusable
* [QTBUG-131955](https://bugreports.qt.io/browse/QTBUG-131955) SVG Icons strentched in QListViewWidget items
* [QTBUG-135326](https://bugreports.qt.io/browse/QTBUG-135326) Linux: QLoggingCategory::setFilterRules() with enabled
CTF tracing causes a crash
* [QTBUG-135617](https://bugreports.qt.io/browse/QTBUG-135617) Compile Android without permissions -feature
* [QTBUG-133841](https://bugreports.qt.io/browse/QTBUG-133841) 'Failed to initialize graphics backend for OpenGL'
causes the example apps to crash on launch
* [QTBUG-135693](https://bugreports.qt.io/browse/QTBUG-135693) Compile Android without accessibility -feature
* [QTBUG-135675](https://bugreports.qt.io/browse/QTBUG-135675) Compile Android without clipboard -feature
* [QTBUG-125586](https://bugreports.qt.io/browse/QTBUG-125586) QVariantAnimation: currentValue should not change when
calling setStartValue() and setEndValue()
* [QTBUG-136039](https://bugreports.qt.io/browse/QTBUG-136039) CMake build fail with axcontainer and infinite loop
* [QTBUG-134259](https://bugreports.qt.io/browse/QTBUG-134259) Update SSL overview with link to export control
documentation
* [QTBUG-135890](https://bugreports.qt.io/browse/QTBUG-135890) Allow configuring Windows without clipboard feature
* [QTBUG-135893](https://bugreports.qt.io/browse/QTBUG-135893) Allow configuring Windows without highdpiscaling feature
* [QTBUG-136341](https://bugreports.qt.io/browse/QTBUG-136341) Build fails without style_windows & style_stylesheet
features
* [QTBUG-136241](https://bugreports.qt.io/browse/QTBUG-136241) wasm: standardContextMenu is not shown
* [QTBUG-130278](https://bugreports.qt.io/browse/QTBUG-130278) [Reg 6.7.2 -> 6.8.0][macOS] QLocale::LongFormat no
longer produces reversible conversion between QDateTime and QString
* [QTBUG-135867](https://bugreports.qt.io/browse/QTBUG-135867) [REG 6.9] Linux/XCB: Possible holes in transparent
windows on HiDPI
* [QTBUG-136562](https://bugreports.qt.io/browse/QTBUG-136562) tabbing between textfields and buttons does not work
* [QTBUG-135934](https://bugreports.qt.io/browse/QTBUG-135934) Mac-style QMenu icons never show Disabled mode
* [QTBUG-130474](https://bugreports.qt.io/browse/QTBUG-130474) QLineEdit/QCompleter popup shows in top-level window
* [QTBUG-136050](https://bugreports.qt.io/browse/QTBUG-136050) Input text appears next to Qt window
* [QTBUG-136233](https://bugreports.qt.io/browse/QTBUG-136233) [Webassembly] Ghost input field disrupts surface
geometry
* [QTBUG-136362](https://bugreports.qt.io/browse/QTBUG-136362) [REG 6.8 -> 6.9] QTableView: Header sections' incorrect
painting
* [QTBUG-136477](https://bugreports.qt.io/browse/QTBUG-136477) Header scrolls to opposite direction
* [QTBUG-136210](https://bugreports.qt.io/browse/QTBUG-136210) Qt installer .pc files unusable due to spurious prefix
* [QTBUG-135800](https://bugreports.qt.io/browse/QTBUG-135800) [REG 6.8 → 6.9] XMLHttpRequest() errors from
qt.network.http2 and rest api data are not displaying to Multimedia
* [QTBUG-136453](https://bugreports.qt.io/browse/QTBUG-136453) QTableView auto-section-resize broken since Qt 6.9
* [QTBUG-136497](https://bugreports.qt.io/browse/QTBUG-136497) Android app fails to restart when permission is revoked
* [QTBUG-136077](https://bugreports.qt.io/browse/QTBUG-136077) [Regression 6.8.2->6.8.3] Android apps hang with black
screen or splash screen
* [QTBUG-135961](https://bugreports.qt.io/browse/QTBUG-135961) Blank screen when app is woken up from background
* [QTBUG-136485](https://bugreports.qt.io/browse/QTBUG-136485) QDockWidgets sends visibilityChanged on destruction
* [QTBUG-136549](https://bugreports.qt.io/browse/QTBUG-136549) Race condition and crash when HTTP error received while
QHttp2Stream is uploading
* [QTBUG-133761](https://bugreports.qt.io/browse/QTBUG-133761) Update Qt Creator help mode colours to match the current
themes
* [QTBUG-134148](https://bugreports.qt.io/browse/QTBUG-134148) When relying on implicit PCH, QML_ELEMENT is not
processed by qmltyperegistrar
* [QTBUG-133882](https://bugreports.qt.io/browse/QTBUG-133882) Polish string types overview
* [QTBUG-134250](https://bugreports.qt.io/browse/QTBUG-134250) qdoc fails to report warnings for incorrect \fn
signatures
* [QTBUG-127549](https://bugreports.qt.io/browse/QTBUG-127549) QDomNode::save() takes huge amount of time. 10x worse
performance when compared to Qt 5
* [QTBUG-134557](https://bugreports.qt.io/browse/QTBUG-134557) QOpenGLFramebufferObject seems to leak
QOpenGLSharedResourceGuards
* [QTBUG-83817](https://bugreports.qt.io/browse/QTBUG-83817) potential out-of-bounds access in qcssparser
* [QTBUG-115926](https://bugreports.qt.io/browse/QTBUG-115926) WASM: In the QML Accessibility demo application, menu
items are not getting focus.
* [QTBUG-126659](https://bugreports.qt.io/browse/QTBUG-126659) New QMap.qHash leading to ambiguous calls
* [QTBUG-134683](https://bugreports.qt.io/browse/QTBUG-134683) Deprecated one argument version of qHash still required
in qHashMulti
* [QTBUG-134690](https://bugreports.qt.io/browse/QTBUG-134690) qHashMulti and qHashMultiCommutative use the slower
seed==0 algorithms for strings
* [QTBUG-86387](https://bugreports.qt.io/browse/QTBUG-86387) Support consuming XCFramework with qmake
* [QTBUG-118901](https://bugreports.qt.io/browse/QTBUG-118901) qt_feature for exceptions
* [QTBUG-134671](https://bugreports.qt.io/browse/QTBUG-134671) [VxWorks] QEGLPlatformContext::getProcAddress doesn't
work with static ogl libraries
* [QTBUG-133215](https://bugreports.qt.io/browse/QTBUG-133215) [Reg 6.6 -> 6.8] QMainWindow removes titlebar exception
* [QTBUG-127012](https://bugreports.qt.io/browse/QTBUG-127012) iOS: ASSERT: "qmlType.metaObject()" in
fileqqmltypedata.cpp, line 1019
* [QTBUG-134883](https://bugreports.qt.io/browse/QTBUG-134883) QML on Windows: Unable to assign ClassA to ClassA
* [QTBUG-133522](https://bugreports.qt.io/browse/QTBUG-133522) Continuation on 'mapped' yields single result only
* [QTBUG-130480](https://bugreports.qt.io/browse/QTBUG-130480) Windows 11 Style does not change the palette before
QEvent::PaletteChange
* [QTBUG-122980](https://bugreports.qt.io/browse/QTBUG-122980) [REG -> dev] Unity Build broken
* [QTBUG-135055](https://bugreports.qt.io/browse/QTBUG-135055) QScroller::grabGesture() appears to leak its
QFlickGestureRecognizer
* [QTBUG-134999](https://bugreports.qt.io/browse/QTBUG-134999) [Boot2Qt ] 'Failed to build graphics pipeline' when
running 'orderindependenttransparency' example
* [QTBUG-131459](https://bugreports.qt.io/browse/QTBUG-131459) QDoc: No warning if \qmltype contains \inherits with
non-existing type
* [QTBUG-134913](https://bugreports.qt.io/browse/QTBUG-134913) QLocale::toDouble() gives unexpected result for same
decimal and grouping symbol
* [QTBUG-135151](https://bugreports.qt.io/browse/QTBUG-135151) UB when active menu of a menu bar is being deleted
* [QTBUG-135146](https://bugreports.qt.io/browse/QTBUG-135146) [vxworks] not possible to build vkb with static build
and dlopen feature turned off
* [QTBUG-99563](https://bugreports.qt.io/browse/QTBUG-99563) The QMutable*Event construct is Undefined Behaviour
* [QTBUG-135382](https://bugreports.qt.io/browse/QTBUG-135382) Invalid year zero date asserts in
QDateTimeParser::parse()
* [QTBUG-129754](https://bugreports.qt.io/browse/QTBUG-129754) Top flaky test: tst_qgesturerecognizer::touchReplay
* [QTBUG-135626](https://bugreports.qt.io/browse/QTBUG-135626) QPointer causes unneccessary (invalid) downcasts
* [QTBUG-135621](https://bugreports.qt.io/browse/QTBUG-135621) gn.py needs an -isysroot argument but configure doesn't
create it
* [QTBUG-119205](https://bugreports.qt.io/browse/QTBUG-119205) tst_Android::orientationChange is flaky on android
* [QTBUG-135966](https://bugreports.qt.io/browse/QTBUG-135966) Blacklist tst_QFileDialog::clearLineEdit() on vxworks
* [QTBUG-135976](https://bugreports.qt.io/browse/QTBUG-135976) Memory leaks in QAlphaWidget and QRollEffect
* [QTBUG-134627](https://bugreports.qt.io/browse/QTBUG-134627) [VxWorks] QTranslator load fails reading from SD card
* [QTBUG-136101](https://bugreports.qt.io/browse/QTBUG-136101) Minimal configuration compile with autotests
* [QTBUG-131894](https://bugreports.qt.io/browse/QTBUG-131894) qtranslator loads wrong locale
* [QTBUG-136550](https://bugreports.qt.io/browse/QTBUG-136550) QMYSQL: QT application built with libmariadb3.4 won't
connect to MariaDB 10
* [QTBUG-10506](https://bugreports.qt.io/browse/QTBUG-10506) QCalendarWidget in Chinese locale shows wrong weekday
names
* [QTBUG-84877](https://bugreports.qt.io/browse/QTBUG-84877) QLocale::system() uses short names of days and months for
narrow formats
* [QTBUG-131897](https://bugreports.qt.io/browse/QTBUG-131897) pdf viewer is not working on nano browser and simple
browser sample apps
* [QTBUG-136687](https://bugreports.qt.io/browse/QTBUG-136687) [regression 6.9.0] Wasm LibreOffice no longer gets
keyboard input events

### qtsvg
* [QTBUG-134044](https://bugreports.qt.io/browse/QTBUG-134044) SvgHandler might access out of bound
* [QTBUG-135596](https://bugreports.qt.io/browse/QTBUG-135596) SVG Stroke Animation Rendering Issue in Qt6.9.0
* [QTBUG-49160](https://bugreports.qt.io/browse/QTBUG-49160) Rendering SVG icon in QFileBox on Fedora22 crashes Qt

### qtdeclarative
* [QTBUG-134087](https://bugreports.qt.io/browse/QTBUG-134087) qtquickview_java QML button signal not connected when
starting example
* [QTBUG-130791](https://bugreports.qt.io/browse/QTBUG-130791) qt_target_qml_sources cannot be subdir of
qt_add_qml_module
* [QTBUG-134274](https://bugreports.qt.io/browse/QTBUG-134274) QML LocationPermission is not a type
* [QTBUG-127098](https://bugreports.qt.io/browse/QTBUG-127098) qmllint: False positive for required property
* [QTBUG-134226](https://bugreports.qt.io/browse/QTBUG-134226) Warning about application/x-color in QtQuick Drag
* [QTBUG-134247](https://bugreports.qt.io/browse/QTBUG-134247) TableView: edit delegate commit upon losing focus
* [QTBUG-134001](https://bugreports.qt.io/browse/QTBUG-134001) [iOS] The dial handle is misaligned with the circular
path of the dial
* [QTBUG-129424](https://bugreports.qt.io/browse/QTBUG-129424) iOS style: Dial handle doesn't follow groove
* [QTBUG-134398](https://bugreports.qt.io/browse/QTBUG-134398) Qt Design Studio does not work with Qt 6.8 because of
QML caching
* [QTBUG-134442](https://bugreports.qt.io/browse/QTBUG-134442) tst_qqmlcomponent::loadFromQrc() randomly fails on QNX
* [QTBUG-134492](https://bugreports.qt.io/browse/QTBUG-134492) Thread sanitizer (TSAN) warns about data race with QSG
Scenegraph (qsgmaterial)
* [QTBUG-133886](https://bugreports.qt.io/browse/QTBUG-133886) Regression in 6.9: Hover in ComboBox broken with
ApplicationWindow
* [QTBUG-134725](https://bugreports.qt.io/browse/QTBUG-134725) Mark QQC2 fusion style as a dependency for macos style
* [QTBUG-67368](https://bugreports.qt.io/browse/QTBUG-67368) QJSValue::strictlyEquals documentation error
* [QTBUG-132931](https://bugreports.qt.io/browse/QTBUG-132931) QJSEngine leaks memory
* [QTBUG-130116](https://bugreports.qt.io/browse/QTBUG-130116) Broken accessibility tree in (at least) certain lists
* [QTBUG-133424](https://bugreports.qt.io/browse/QTBUG-133424) Named platform icons are blurry on macOS when displayed
with IconImage/IconLabel
* [QTBUG-134664](https://bugreports.qt.io/browse/QTBUG-134664) FAIL!  :
tst_examples::examples(examples/quick/multieffect/testbed/qml/main.qml)
Received a fatal error
* [QTBUG-122043](https://bugreports.qt.io/browse/QTBUG-122043) The button appears to be pressed twice, even if it's
pressed only once while you are pressing another button at the same time
on the Android app
* [QTBUG-135039](https://bugreports.qt.io/browse/QTBUG-135039) Import in one component affects type resolution in
another one
* [QTBUG-127107](https://bugreports.qt.io/browse/QTBUG-127107) qmllint does not warn about redeclaration of JS
variables
* [QTBUG-95887](https://bugreports.qt.io/browse/QTBUG-95887) tst_FlickableInterop is flaky on opensuse
* [QTBUG-132886](https://bugreports.qt.io/browse/QTBUG-132886) qmlformat: The colon in the switch statement is in the
wrong position.
* [QTBUG-133316](https://bugreports.qt.io/browse/QTBUG-133316) qmldom/qmlformat: Comments are broken in certain
positions
* [QTBUG-123386](https://bugreports.qt.io/browse/QTBUG-123386) QmlFormat. Incorrect handling of some comments
* [QTBUG-134781](https://bugreports.qt.io/browse/QTBUG-134781) qmlls: lints out-of-date versions of files in the linter
* [QTBUG-122405](https://bugreports.qt.io/browse/QTBUG-122405) tst_qquickhoverhandler::window is flaky on OpenSuse
* [QTBUG-134688](https://bugreports.qt.io/browse/QTBUG-134688) Aliases of properties of bindables don't emit change
signals
* [QTBUG-132763](https://bugreports.qt.io/browse/QTBUG-132763) Regression: keyboard navigation jumps to main view when
drawer is open
* [QTBUG-75215](https://bugreports.qt.io/browse/QTBUG-75215) tst_qquickapplication::active() is flaky on opensuse
* [QTBUG-123550](https://bugreports.qt.io/browse/QTBUG-123550) Top flaky test: tst_qquickapplication::active on
openSUSE_15_5 X86_64.
* [QTBUG-135288](https://bugreports.qt.io/browse/QTBUG-135288) qmlsc: crash on if + for
* [QTBUG-134887](https://bugreports.qt.io/browse/QTBUG-134887) [REG 6.9 -> 6.10] qmllint: bogus required property
warning with generalized grouped property
* [QTBUG-122031](https://bugreports.qt.io/browse/QTBUG-122031) tst_qquickapplication::state() is flaky on opensuse
* [QTBUG-134903](https://bugreports.qt.io/browse/QTBUG-134903) Duplicate context menus when using custom context Menus
in text controls
* [QTBUG-135740](https://bugreports.qt.io/browse/QTBUG-135740) Quick dialogs and templates to compile when draganddrop
feature is disabled
* [QTBUG-129329](https://bugreports.qt.io/browse/QTBUG-129329) QML Preview doesn't update properly
* [QTBUG-135437](https://bugreports.qt.io/browse/QTBUG-135437) code snippet doesn't build due to a function reference
from inside Component
* [QTBUG-135279](https://bugreports.qt.io/browse/QTBUG-135279) FTBFS libc++abi: terminating due to uncaught exception
of type std::runtime_error: file is already signed. pass -f to sign
regardless
* [QTBUG-135475](https://bugreports.qt.io/browse/QTBUG-135475) QML Plugin Example shows a blank window
* [QTBUG-135649](https://bugreports.qt.io/browse/QTBUG-135649) qmlcachegen reaches Q_UNREACHABLE
* [QTBUG-134911](https://bugreports.qt.io/browse/QTBUG-134911) Regression: C++ generated from QML throws compiler
warning (declaration of unit vs. global declaration)
* [QTBUG-134778](https://bugreports.qt.io/browse/QTBUG-134778) Binding: short syntax broken with ComponentBehavior:
Bound
* [QTBUG-135815](https://bugreports.qt.io/browse/QTBUG-135815) QSG wrongly batches QSGGeometryNodes with different
lineWidth
* [QTBUG-134782](https://bugreports.qt.io/browse/QTBUG-134782) Binding: Documentation should point to multiple bindings
with new syntax
* [QTBUG-135200](https://bugreports.qt.io/browse/QTBUG-135200) QQ4A example documentation does not point where to find
the examples
* [QTBUG-135342](https://bugreports.qt.io/browse/QTBUG-135342) qmlcachegen crashes in QQmlJSTypeResolver::genericType
* [QTBUG-134405](https://bugreports.qt.io/browse/QTBUG-134405) Fix QtQuickView multi-view examples
* [QTBUG-135980](https://bugreports.qt.io/browse/QTBUG-135980) error: 'O_RDONLY' was not declared in this scope
* [QTBUG-135965](https://bugreports.qt.io/browse/QTBUG-135965) Application freezes when trigger an Action's shortcut in
sub-sub Menu
* [QTBUG-135387](https://bugreports.qt.io/browse/QTBUG-135387) Division by zero when changing path elements of
ShapePath imperatively
* [QTBUG-134206](https://bugreports.qt.io/browse/QTBUG-134206) Using ListElement with QML Type Compiler leads to link
errors
* [QTBUG-134772](https://bugreports.qt.io/browse/QTBUG-134772) Occasional crashs on debug service rampdowns
* [QTBUG-135367](https://bugreports.qt.io/browse/QTBUG-135367) Compiler warning in qmlcachegen generated code
* [QTBUG-135975](https://bugreports.qt.io/browse/QTBUG-135975) Hover event delivery causes memory leak
* [QTBUG-134922](https://bugreports.qt.io/browse/QTBUG-134922) [REG 6.7 → 6.8] Regression with Qml Binding type
(destruction) in 6.8
* [QTBUG-135946](https://bugreports.qt.io/browse/QTBUG-135946) Allow configuring without quicktemplates2-hover feature
* [QTCREATORBUG-32634](https://bugreports.qt.io/browse/QTCREATORBUG-32634) Autocompletion for enum doesn't work without
restarting qml language server
* [QTBUG-136031](https://bugreports.qt.io/browse/QTBUG-136031) MouseArea in a ApplicationWindow's background can not be
hovered since 6.9.0
* [QTBUG-136120](https://bugreports.qt.io/browse/QTBUG-136120) Qml Runtime fails to correct escape -a after --
* [QTBUG-127913](https://bugreports.qt.io/browse/QTBUG-127913) QQuickTextNodeEngine renders
QChar::ObjectReplacementCharacter at low-DPI
* [QTBUG-135334](https://bugreports.qt.io/browse/QTBUG-135334) [Reg 6.4 -> 6.5] qmlRegisterSingletonInstance does not
work with importPath over http
* [QTBUG-134606](https://bugreports.qt.io/browse/QTBUG-134606) eventPoint documentation is hard to read
* [QTBUG-136452](https://bugreports.qt.io/browse/QTBUG-136452) qmllint - no way to treat `missing-enum-entry` as
warning
* [QTBUG-135020](https://bugreports.qt.io/browse/QTBUG-135020) qmllint: clean up linting categories
* [QTBUG-136142](https://bugreports.qt.io/browse/QTBUG-136142) QQmlTableModel is not notifying about changes of its
data
* [QTBUG-136008](https://bugreports.qt.io/browse/QTBUG-136008) [REG: 6.8.2 -> 6.9] False warning about missing required
property when using inline component
* [QTBUG-135244](https://bugreports.qt.io/browse/QTBUG-135244) qmlcachegen takes a long time to compile
fluentwinui3/Slider.qml
* [QTBUG-136058](https://bugreports.qt.io/browse/QTBUG-136058) [Reg] qmllint: mix up between required properties
* [QTBUG-136127](https://bugreports.qt.io/browse/QTBUG-136127) Crash when calling Object.value() on QQmlListModel
* [QTBUG-136250](https://bugreports.qt.io/browse/QTBUG-136250) TextEditor example: can't set multiple font attributes
at the same time
* [QTBUG-135457](https://bugreports.qt.io/browse/QTBUG-135457) [REG 6.8 → 6.9] ninja fails every time in every build
* [QTBUG-136253](https://bugreports.qt.io/browse/QTBUG-136253) Menu key on Windows doesn't open the context menu on the
focused item
* [QTBUG-136248](https://bugreports.qt.io/browse/QTBUG-136248) Crash in QQmlPrivate::callQObjectMethod
* [QTBUG-53863](https://bugreports.qt.io/browse/QTBUG-53863) tst_QQuickListView::populateTransitions(static, no
populate) crashes randomly
* [QTBUG-136192](https://bugreports.qt.io/browse/QTBUG-136192) qmlformat fails to write file
* [QTBUG-136552](https://bugreports.qt.io/browse/QTBUG-136552) QMLLS crashes
* [QTBUG-136933](https://bugreports.qt.io/browse/QTBUG-136933) Can't build QtQ4A examples from command line
* [QTBUG-134880](https://bugreports.qt.io/browse/QTBUG-134880) Disable edge-to-edge feature of Android 15 on
qtquickview examples
* [QTBUG-134269](https://bugreports.qt.io/browse/QTBUG-134269) Attached properties using REVISION produce error
* [QTBUG-134250](https://bugreports.qt.io/browse/QTBUG-134250) qdoc fails to report warnings for incorrect \fn
signatures
* [QTBUG-110243](https://bugreports.qt.io/browse/QTBUG-110243) Resources are lost when linking static libraries using
CMake build system in a separate project
* [QTCREATORBUG-32591](https://bugreports.qt.io/browse/QTCREATORBUG-32591) qmlls still not work in qt creator
* [QTBUG-133530](https://bugreports.qt.io/browse/QTBUG-133530) Several Controls tests failing after test coverage
restored
* [QTBUG-134251](https://bugreports.qt.io/browse/QTBUG-134251) Qt Quick for Android is hard to find
* [QTBUG-134768](https://bugreports.qt.io/browse/QTBUG-134768) QLocale::toStrings uses E instead of e
* [QTBUG-109553](https://bugreports.qt.io/browse/QTBUG-109553) CMake deployment API creates too deep directory
hierarchy when DESTDIR is set
* [QTBUG-117948](https://bugreports.qt.io/browse/QTBUG-117948) qt_generate_deploy_qml_app_script() deploys QML plugin
target but not the corresponding backing target
* [QTBUG-35598](https://bugreports.qt.io/browse/QTBUG-35598) QtQuick Controls TextField and TextArea miss mouse
context menu
* [QTBUG-135164](https://bugreports.qt.io/browse/QTBUG-135164) TextArea with description and no name results in empty
a11y description
* [QTBUG-133492](https://bugreports.qt.io/browse/QTBUG-133492) Issue found on Qt 6.8 variant that doesn't exist on 6.6
* [QTBUG-129947](https://bugreports.qt.io/browse/QTBUG-129947) tst_QQuickTextEdit::mouseSelection() is flaky on macOS
arm 12/13
* [QTBUG-135032](https://bugreports.qt.io/browse/QTBUG-135032) Uncreatable value types behave erratically
* [QTBUG-105856](https://bugreports.qt.io/browse/QTBUG-105856) The Menu Item will continue to be highlighted after the
sub menu is closed
* [QTBUG-133793](https://bugreports.qt.io/browse/QTBUG-133793) QT_QML_GENERATE_QMLLS_INI doesn't update file if build
directory changes
* [QTBUG-134790](https://bugreports.qt.io/browse/QTBUG-134790) QML AnchorChanges do not compile in strict mode
* [QTBUG-136101](https://bugreports.qt.io/browse/QTBUG-136101) Minimal configuration compile with autotests
* [QTBUG-136251](https://bugreports.qt.io/browse/QTBUG-136251) TextEditor example: selection is lost when you open the
Font or Color dialog from the context menu

### qtactiveqt
* [QTBUG-123520](https://bugreports.qt.io/browse/QTBUG-123520) QAxObject has invalid properties that can not be set
either

### qtmultimedia
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
* [QTBUG-119141](https://bugreports.qt.io/browse/QTBUG-119141) MediaPlayer-example The data of the files is editable,
but cannot be saved
* [QTBUG-135021](https://bugreports.qt.io/browse/QTBUG-135021) docs link to QVideoFrameFormat::PixelFormat goes to
wikipedia instead
* [QTBUG-135043](https://bugreports.qt.io/browse/QTBUG-135043) qtmultimedia FTBFS due to a CMake error in
QtFFmpegMediaPluginImpl
* [QTBUG-135172](https://bugreports.qt.io/browse/QTBUG-135172) FindFFmpeg.cmake doesn't look for correct libraries on
iOS
* [QTBUG-134882](https://bugreports.qt.io/browse/QTBUG-134882) QAudioDevice::isFormatSupported() not working on Android
* [QTBUG-135307](https://bugreports.qt.io/browse/QTBUG-135307) Regression 6.8.2 > 6.8.3: Media player does not play mp3
* [QTBUG-122754](https://bugreports.qt.io/browse/QTBUG-122754) [windows] QML media player always uses audio stream,
even when there is no media playing
* [QTBUG-135939](https://bugreports.qt.io/browse/QTBUG-135939) qgstreameraudiooutput.cpp is missing the inclusion of
header files
* [QTBUG-132167](https://bugreports.qt.io/browse/QTBUG-132167) QCamera: Handle AVCaptureDevice being in suspended state
* [QTBUG-135256](https://bugreports.qt.io/browse/QTBUG-135256) Camera not functioning if permission granted later
* [QTBUG-136003](https://bugreports.qt.io/browse/QTBUG-136003) QVideoSink documentation mentions nonexistent paint()
function
* [QTBUG-129626](https://bugreports.qt.io/browse/QTBUG-129626) [ffmpeg] pc files not found when building against a
system ffmpeg
* [QTBUG-136052](https://bugreports.qt.io/browse/QTBUG-136052) VideoOutput crash with opacity animation
* [QTBUG-135360](https://bugreports.qt.io/browse/QTBUG-135360) Unexpected Qt Multimedia warning message
* [QTBUG-135911](https://bugreports.qt.io/browse/QTBUG-135911) QRhi claims to not support a working texture format.
* [QTBUG-136191](https://bugreports.qt.io/browse/QTBUG-136191) Screencapture example crashes on permission granted
* [QTBUG-137070](https://bugreports.qt.io/browse/QTBUG-137070) [REG 6.9.1 prev snapshot->6.9.1] Multimedia examples not
compiling, Wasm
* [QTBUG-133914](https://bugreports.qt.io/browse/QTBUG-133914) FFmpeg plugin tests may fail to build on Linux and
Android
* [QTBUG-129758](https://bugreports.qt.io/browse/QTBUG-129758) Audio playback does not work on linux/aarch64 (sailfish
os)
* [QTBUG-134196](https://bugreports.qt.io/browse/QTBUG-134196) R16 video texture formats don't have a working fallback
for GLES 2.0
* [QTBUG-135239](https://bugreports.qt.io/browse/QTBUG-135239) external QAudioDevice no longer provides sample rates
* [QTBUG-134229](https://bugreports.qt.io/browse/QTBUG-134229) Changing playback speed results in cracking and out-of-
sync sound when playing audio/video on Android
* [QTBUG-125238](https://bugreports.qt.io/browse/QTBUG-125238) QVideoFrame::toImage fails on Android with 16 bit per
component planar YUV formats
* [QTBUG-134430](https://bugreports.qt.io/browse/QTBUG-134430) QCamera stops working entirely if device is disconnected
* [QTBUG-135618](https://bugreports.qt.io/browse/QTBUG-135618) [MacOS] Sporadic crashes when call
QVideoFrame::toImage()
* [QTBUG-135951](https://bugreports.qt.io/browse/QTBUG-135951) QMediaRecorder captures video at a much worse quality on
Linux
* [QTBUG-135873](https://bugreports.qt.io/browse/QTBUG-135873) Crash when trying to play video

### qttools
* [QTBUG-131459](https://bugreports.qt.io/browse/QTBUG-131459) QDoc: No warning if \qmltype contains \inherits with
non-existing type
* [QTBUG-134520](https://bugreports.qt.io/browse/QTBUG-134520) qdoc: delimiters surrounding alt text are in the
generated HTML attribs.
* [QTBUG-134693](https://bugreports.qt.io/browse/QTBUG-134693) [REG 6.8 -> 6.9] qt_add_translations creates QM files in
PROJECT_BINARY_DIR instead of CMAKE_CURRENT_BINARY_DIR
* [QTBUG-134250](https://bugreports.qt.io/browse/QTBUG-134250) qdoc fails to report warnings for incorrect \fn
signatures
* [QTBUG-131856](https://bugreports.qt.io/browse/QTBUG-131856) \qmlproperty docs don't mention how to document enum
type
* [QTBUG-136115](https://bugreports.qt.io/browse/QTBUG-136115) REG: QDoc never links using relative hrefs when running
in single-exec mode
* [QTBUG-135398](https://bugreports.qt.io/browse/QTBUG-135398) [REG 6.8.3->6.9.0] MSVC2022 x64: Widget Designer crash
when QWebEngineView is dragged to canvas
* [QTBUG-94345](https://bugreports.qt.io/browse/QTBUG-94345)  Qt Designer crash in QQuickWidget plugin
* [QTBUG-100285](https://bugreports.qt.io/browse/QTBUG-100285) Windows: Qt Designer crash when selecting QWebEngineView
* [QTBUG-136164](https://bugreports.qt.io/browse/QTBUG-136164) Saving UI-file using QFormBuilder missing properties
(unsupported?)
* [QTBUG-132707](https://bugreports.qt.io/browse/QTBUG-132707) Missing links in Qt Linguist Manual: Text ID based
translations doc
* [QTBUG-133739](https://bugreports.qt.io/browse/QTBUG-133739) Update qdoc manual for \deprecated and \moduleState
* [QTBUG-120508](https://bugreports.qt.io/browse/QTBUG-120508) Qt Linguist: Unreadable HTML tags in dark mode
* [QTBUG-127452](https://bugreports.qt.io/browse/QTBUG-127452) Linguist unreadable after switching to dark theme
* [QTBUG-136578](https://bugreports.qt.io/browse/QTBUG-136578) Linguist is unusable in dark mode
* [QTBUG-134195](https://bugreports.qt.io/browse/QTBUG-134195) Qt Widgets Designer/Property editor: theme icons
dropdown shown for  maximumSize Width property
* [QTBUG-134256](https://bugreports.qt.io/browse/QTBUG-134256) Coverity: Use after free in Qt Designer's property
editor
* [QTBUG-134595](https://bugreports.qt.io/browse/QTBUG-134595) Build of qttools/linguist fails with features mdiarea,
fontcombobox or syntaxhighlighting disabled
* [QTBUG-124852](https://bugreports.qt.io/browse/QTBUG-124852) Linguist tool bar looks funny

### qtdoc
* [QTBUG-132704](https://bugreports.qt.io/browse/QTBUG-132704)  Car Configurator demo crashes on startup
* [QTBUG-133957](https://bugreports.qt.io/browse/QTBUG-133957) Add information about source SBOM in SBOM page
* [QTBUG-127953](https://bugreports.qt.io/browse/QTBUG-127953) Basic support for CMake FetchContent
* [QTBUG-135250](https://bugreports.qt.io/browse/QTBUG-135250) Editorial notes on `Qt for Wayland Requirements` page
* [QTBUG-135289](https://bugreports.qt.io/browse/QTBUG-135289) [Examples] Lightning Viewer app misses tags
* [QTBUG-100340](https://bugreports.qt.io/browse/QTBUG-100340) Remove documentation of QPF2 fonts
* [QTBUG-134789](https://bugreports.qt.io/browse/QTBUG-134789) "Contents" menu hidden behind images
* [QTBUG-136036](https://bugreports.qt.io/browse/QTBUG-136036) colorpaletteclient doesn't compile if qml-network is
disabled
* [QTBUG-136482](https://bugreports.qt.io/browse/QTBUG-136482) REG [6.9.0->6.9.1] demos/hangman not compiling on
Android
* [QTBUG-134220](https://bugreports.qt.io/browse/QTBUG-134220) The xcb-xinerama is missing from table listing Qt
requirements on X11
* [QTBUG-134104](https://bugreports.qt.io/browse/QTBUG-134104) Specific Options for Platforms documentation should have
VxWorks
* [QTBUG-35598](https://bugreports.qt.io/browse/QTBUG-35598) QtQuick Controls TextField and TextArea miss mouse
context menu
* [QTBUG-134251](https://bugreports.qt.io/browse/QTBUG-134251) Qt Quick for Android is hard to find
* [QTBUG-133574](https://bugreports.qt.io/browse/QTBUG-133574) Setting QT_DEFAULT_MAJOR_VERSION to 6 doesn't select Qt6
over Qt5
* [QTBUG-129105](https://bugreports.qt.io/browse/QTBUG-129105) Car configurator can't download assets from
download.qt.io

### qtlocation
* [QTBUG-134097](https://bugreports.qt.io/browse/QTBUG-134097) TapHandler with a MapPolyline is not getting tapped
events when the Map is rotated

### qtconnectivity
* [QTBUG-133975](https://bugreports.qt.io/browse/QTBUG-133975) BLUETOOTH_SCAN permission in Split APK / AAB
(QtBluetoothUtility.java)
* [QTBUG-133788](https://bugreports.qt.io/browse/QTBUG-133788) Ndef editor example cross-compiling on Windows to
Boot2Qt fails
* [QTBUG-99410](https://bugreports.qt.io/browse/QTBUG-99410) [macOS 12.1] Bluetooth data stream blocked when main menu
opened
* [QTBUG-136576](https://bugreports.qt.io/browse/QTBUG-136576) QNdefNfcSmartPosterRecord might leak memory

### qtwayland
* [QTBUG-134264](https://bugreports.qt.io/browse/QTBUG-134264) "QtShell Compositor" -example install instructions
missing
* [QTBUG-134126](https://bugreports.qt.io/browse/QTBUG-134126) bakedlightmap example: wayland assertion error
* [QTBUG-63039](https://bugreports.qt.io/browse/QTBUG-63039) Threaded scenegraph crash with Nvidia drivers in wayland
* [QTBUG-136343](https://bugreports.qt.io/browse/QTBUG-136343) [REG Qt 6.9] Wayland: QCompleter popup closes
application with protocol error

### qt3d
* [QTBUG-123885](https://bugreports.qt.io/browse/QTBUG-123885) [cmake] name clash between qt3d and qtquick3d - assimp
target
* [QTBUG-106079](https://bugreports.qt.io/browse/QTBUG-106079) qmllint produces warnings from Qt3D imports and
components
* [QTBUG-124708](https://bugreports.qt.io/browse/QTBUG-124708) QText2DEntity jagged text when using RHI OpenGL backend
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

### qtserialbus
* [QTBUG-135299](https://bugreports.qt.io/browse/QTBUG-135299) error: ‘QElapsedTimer’ was not declared in this scope
* [QTBUG-135791](https://bugreports.qt.io/browse/QTBUG-135791) QModbusClient: : sendRawRequest returns pointer, if
delete immediately, QModbusRtuSerialClientPrivate: : onReadyRead
function crash
* [QTBUG-135132](https://bugreports.qt.io/browse/QTBUG-135132) [qtserialbus] Cannot build manual tests

### qtwebengine
* [QTBUG-134107](https://bugreports.qt.io/browse/QTBUG-134107) Qt WebEngine NumLock detection broken using
KeyboardDriver::Xkb
* [QTBUG-134416](https://bugreports.qt.io/browse/QTBUG-134416) Log noise when building Qt WebEngine documentation
* [QTBUG-135047](https://bugreports.qt.io/browse/QTBUG-135047) Excessive X11 pixmap usage on 6.9
* [QTBUG-128440](https://bugreports.qt.io/browse/QTBUG-128440) Top flaky test:
tst_qwebengineview::inputContextQueryInput
* [QTBUG-135620](https://bugreports.qt.io/browse/QTBUG-135620) Qt6WebEngineCoreDeploySupport fails when generating RPM
* [QTBUG-109553](https://bugreports.qt.io/browse/QTBUG-109553) CMake deployment API creates too deep directory
hierarchy when DESTDIR is set
* [QTBUG-119077](https://bugreports.qt.io/browse/QTBUG-119077) CMake deployment API does not deploy Qt Webengine
* [QTBUG-126722](https://bugreports.qt.io/browse/QTBUG-126722) WebEngine: GPU detection is missing "VmWare" in vendor
list
* [QTBUG-135647](https://bugreports.qt.io/browse/QTBUG-135647) WebEngine fatal error in XWayland at startup -> GLX:
Failed to find frame buffer configuration.
* [QTBUG-135032](https://bugreports.qt.io/browse/QTBUG-135032) Uncreatable value types behave erratically
* [QTBUG-136533](https://bugreports.qt.io/browse/QTBUG-136533) Developer tools open with "screencast" enabled (again,
chapter 2)
* [QTBUG-123607](https://bugreports.qt.io/browse/QTBUG-123607) Vulkan backend rendering only black on X11
* [QTBUG-134481](https://bugreports.qt.io/browse/QTBUG-134481) qwebengine_convert_dict Cannot encode command 'TRY ...'
to utf8.
* [QTBUG-136637](https://bugreports.qt.io/browse/QTBUG-136637) Missing libxml2.so.2 with libxml2 2.14
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

### qtcharts
* [QTBUG-115358](https://bugreports.qt.io/browse/QTBUG-115358) QBarCategoryAxis is exported twice
* [QTBUG-134519](https://bugreports.qt.io/browse/QTBUG-134519) tst_QBarSeries::mousehovered() is flaky on Ubuntu 24.04
X11(GNOME)

### qtvirtualkeyboard
* [QTBUG-137250](https://bugreports.qt.io/browse/QTBUG-137250) REG->6.9.0: VirtualKeyboard not working (Linux)

### qtscxml
* [QTBUG-134901](https://bugreports.qt.io/browse/QTBUG-134901) [REG 6.8.2 -> 6.9.0-RC] QStateMachine and QScxml qmake
projects do not compile

### qtspeech
* [QTBUG-135969](https://bugreports.qt.io/browse/QTBUG-135969) Top flaky test: tst_QTextToSpeech::synthesize

### qtnetworkauth
* [QTBUG-135257](https://bugreports.qt.io/browse/QTBUG-135257) NetworkAuth Coverity findings

### qtquicktimeline
* [QTBUG-132502](https://bugreports.qt.io/browse/QTBUG-132502) No way to switch to timeline editor
* [QTBUG-133543](https://bugreports.qt.io/browse/QTBUG-133543) An invalid keyframe file can make the application crash.

### qtquick3d
* [QTBUG-134291](https://bugreports.qt.io/browse/QTBUG-134291) ExtendedSceneEnvironment crash with multiview on HTC
Vive
* [QTBUG-135115](https://bugreports.qt.io/browse/QTBUG-135115) Oit doesn't work with custom materials
* [QTBUG-135125](https://bugreports.qt.io/browse/QTBUG-135125) OIT alpha is applied twice making rendering darker
* [QTBUG-134999](https://bugreports.qt.io/browse/QTBUG-134999) [Boot2Qt ] 'Failed to build graphics pipeline' when
running 'orderindependenttransparency' example
* [QTBUG-136240](https://bugreports.qt.io/browse/QTBUG-136240) RuntimeLoader example fails on QNX
* [QTBUG-135052](https://bugreports.qt.io/browse/QTBUG-135052) [QtQuick3dXr]  Vulkan performance much worse compared to
OpenGLES on Quest 3
* [QTBUG-135823](https://bugreports.qt.io/browse/QTBUG-135823) Qt Quick 3D: OITWeightedBlended silently fails in
WebAssembly

### qtopcua
* [QTBUG-134944](https://bugreports.qt.io/browse/QTBUG-134944) Issue with Alarm Acknowledgement - BadNodeIdUnknown with
ByteString NodeId

### qthttpserver
* [QTBUG-132748](https://bugreports.qt.io/browse/QTBUG-132748) Random assert fail in  tst_qhttpserverrequestfilter
* [QTBUG-134250](https://bugreports.qt.io/browse/QTBUG-134250) qdoc fails to report warnings for incorrect \fn
signatures
* [QTBUG-129103](https://bugreports.qt.io/browse/QTBUG-129103) HttpServer documentation needs an overhaul

### qtquick3dphysics
* [QTBUG-134277](https://bugreports.qt.io/browse/QTBUG-134277) [clang-cl] PhysX build failure

### qtgrpc
* [QTBUG-134266](https://bugreports.qt.io/browse/QTBUG-134266) grpc chat example doesn't install all libraries
* [QTBUG-134309](https://bugreports.qt.io/browse/QTBUG-134309) qgrpchttp2channel.cpp:121:25: error: unused variable
'HttpScheme' with developer build for Android
* [QTBUG-134439](https://bugreports.qt.io/browse/QTBUG-134439) qprotobufpropertyordering.cpp:313:47: error: comparison
of integers of different signs with x86 and armeabi-v7a developer builds
for Android
* [QTBUG-134647](https://bugreports.qt.io/browse/QTBUG-134647) Cannot cross-compile grpc examples
* [QTBUG-134885](https://bugreports.qt.io/browse/QTBUG-134885) Fail to build with protobuf-30
* [QTBUG-134250](https://bugreports.qt.io/browse/QTBUG-134250) qdoc fails to report warnings for incorrect \fn
signatures
* [QTBUG-134273](https://bugreports.qt.io/browse/QTBUG-134273) QtGrpc: Abstract namespaces are not working with
QLocalSocket
* [QTBUG-132738](https://bugreports.qt.io/browse/QTBUG-132738) Errors in some examples

### qtquickeffectmaker
* [QTBUG-121928](https://bugreports.qt.io/browse/QTBUG-121928) Remove Copyright year from About Qt & command line tools

### qtgraphs
* [QTBUG-134002](https://bugreports.qt.io/browse/QTBUG-134002) QBarCategoryAxis::setCategories only works once.
* [QTBUG-134641](https://bugreports.qt.io/browse/QTBUG-134641) the Custom3DItem is still in Scatter3D after it is
deleted by removeCustomItem
* [QTBUG-134598](https://bugreports.qt.io/browse/QTBUG-134598) Qt Graphs Module documentation misses title
* [QTBUG-135388](https://bugreports.qt.io/browse/QTBUG-135388) Axis titles don't align correctly
* [QTBUG-136631](https://bugreports.qt.io/browse/QTBUG-136631) Surface Graph has draws extra unused triangles
* [QTBUG-136654](https://bugreports.qt.io/browse/QTBUG-136654) Building qtgraphs on mac fails with due to -Wcast-
function-type-mismatch
* [QTBUG-135384](https://bugreports.qt.io/browse/QTBUG-135384) Printing the 3D graph causes the Graph Printing example
to crash
* [QTBUG-135386](https://bugreports.qt.io/browse/QTBUG-135386) [Boot2Qt] Cannot save 3D graph to PDF

### qtapplicationmanager (Commercial only)
* [QTBUG-134214](https://bugreports.qt.io/browse/QTBUG-134214) [WARN | am.system] when running 'hello-world' on Boot to
Qt
* [QTBUG-134539](https://bugreports.qt.io/browse/QTBUG-134539) Failed to verify signature (no chain of trust)
* [QTBUG-136234](https://bugreports.qt.io/browse/QTBUG-136234) FAIL!  :
qml::ApplicationManager::test_applicationInterface() 'function returned
false' returned FALSE. ()
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM
* [QTBUG-135860](https://bugreports.qt.io/browse/QTBUG-135860) qt_add_qml_module(): Reject invalid inputs

### qtinterfaceframework (Commercial only)
* [QTBUG-134742](https://bugreports.qt.io/browse/QTBUG-134742) The documentation and the snippet seem to be
contradicting
* [QTBUG-134684](https://bugreports.qt.io/browse/QTBUG-134684) A crash occurred in C:\Users\qt\work\qt\qtinterfaceframe
work_standalone_tests\tests\auto\core\qifabstractfeature\tst_qifabstract
feature.exe.
* [QTBUG-131434](https://bugreports.qt.io/browse/QTBUG-131434) qtqa license test must read Source SBOM

Known Issues
------------
* Check that your system meets Qt's requirements:
https://doc.qt.io/qt-6.9/supported-platforms.html
* RTA reported issues from Qt 6.9
https://bugreports.qt.io/issues/?filter=27175
* See Qt 6.9 known issues from:
https://wiki.qt.io/Qt_6.9_Known_Issues
* Qt 6.9.1 Open issues in Jira:
https://bugreports.qt.io/issues/?filter=27443

Credits for the  release goes to:
---------------------------------

Eirik Aavitsland  
Laszlo Agocs  
Dmitrii Akshintsev  
Konsta Alajärvi  
Anu Aliyas  
Albert Astals Cid  
Even Oscar Andersen  
Soheil Armin  
YAMAMOTO Atsushi  
Mate Barany  
Sebastian Beckmann  
Vladimir Belyavsky  
Nicholas Bennett  
Lena Biliaieva  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
David Boddie  
Joerg Bornemann  
Assam Boudjelthia  
Aurélien Brooke  
Kai Uwe Broulik  
Michael Brüning  
Benjamin Buch  
Olivier De Cannière  
Alexei Cazacov  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Paul Dubsky  
Pavel Dubsky  
Artem Dyomin  
Alexey Edelev  
David Edmundson  
Oliver Eftevaag  
Christian Ehrlicher  
Hatem ElKharashy  
Andreas Eliasson  
David Faure  
Ilya Fedin  
Nicolas Fella  
Samuel Gaist  
Julian Greilich  
Robert Griebl  
Johannes Grunenberg  
Richard Moe Gustavsen  
Lucie Gérard  
Mikko Hallamaa  
Jøger Hansegård  
Inkamari Harjula  
Jani Heikkinen  
Tero Heikkinen  
Miikka Heikkinen  
Moss Heim  
Jari Helaakoski  
Ulf Hermann  
Øystein Heskestad  
Volker Hilsheimer  
Dominik Holland  
Zhang Hongyuan  
Masoud Jami  
Morteza Jamshidi  
Allan Sandfeld Jensen  
Tim Jenßen  
Jonas Karlsson  
Ali Kianian  
Friedemann Kleint  
Michal Klocek  
Jarek Kobus  
Jarkko Koivikko  
Niko Korkala  
Tomi Korpipää  
Jani Korteniemi  
Fabian Kosmale  
Volker Krause  
Santhosh Kumar  
Kai Köhne  
Cristian Le  
Inho Lee  
Frédéric Lefebvre  
Paul Lemire  
Wladimir Leuschner  
Jie Liu  
Jarno Lämsä  
Robert Löhning  
Thiago Macieira  
Thorbjørn Lund Martsum  
Leena Miettinen  
Safiyyah Moosa  
Bartlomiej Moskal  
Marc Mutz  
Tommi Mänttäri  
Antti Määttä  
Andy Nichols  
Mårten Nordheim  
Dennis Oberst  
Kwanghyo Park  
Jerome Pasion  
Mikhail Paulyshka  
Mauro Persano  
Samuli Piippo  
Karim Pinter  
Milla Pohjanheimo  
Lauri Pohjanheimo  
Joni Poikelin  
Rami Potinkara  
Lorn Potter  
Sakaria Pouke  
Dheerendra Purohit  
MohammadHossein Qanbari  
Liang Qi  
Matthias Rauter  
Topi Reinio  
Shawn Rutledge  
Otto Ryynänen  
Emir SARI  
Ahmad Samir  
Lars Schmertmann  
Luca Di Sera  
Sami Shalayel  
Tian Shilin  
Kristoffer Skau  
Nils Petter Skålerud  
Ivan Solovev  
Axel Spoerl  
Alexander Stippich  
Magdalena Stojek  
Martin Storsjö  
Christian Strømme  
Lars Sutterud  
Jan Arve Sæther  
Morten Sørvig  
Nodir Temirkhodjaev  
Jere Tuliniemi  
Paul Olav Tvete  
Esa Törmänen  
Tuomas Vaarala  
Sami Varanka  
Peter Varga  
Doris Verria  
Tor Arne Vestbø  
Petri Virkkunen  
Juha Vuolle  
Olli Vuolteenaho  
Jannis Völker  
Michael Weghorn  
Edward Welbourne  
Paul Wicking  
Oliver Wolff  
Milian Wolff  
Semih Yavuz  
Marianne Yrjänä  
Vlad Zahorodnii  
Eike Ziller  
Michał Łoś  
