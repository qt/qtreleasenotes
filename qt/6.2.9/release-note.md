Release note
============
Qt 6.2.9 release is a patch release made on the top of Qt 6.2.8. As a patch
release, Qt 6.2.9 does not add any new functionality but provides bug fixes
and other improvements.

For detailed information about Qt, see the Qt 6.2 online documentation:
https://doc.qt.io/qt-6.2/.

Important Changes
-----------------

### qtbase
* 9390a445105 QTimer: fix new-style slot invocation for receiver in
another thread
Fixed a bug that caused slots connected to single-slot timers using the
new-style connection mechanism to be delivered in the wrong thread.

* 3ee64cd69b9 SQLite: Update SQLite to v3.41.2
Updated SQLite to v3.41.2

* 1e46bc05d23 QMultiHash: fix missing update to m_size
to not be counted, resulting in a hash map with an incorrect element
count and which could cause an assertion failure depending on how the
hash was later mutated.

* 9241a0dd4d3 QPluginLoader: don't instantiante multiple, identical
instances
staticInstances() will not call duplicated registrations of the same
instantiation function, which can only happen as a result of duplicated
Q_IMPORT_PLUGIN for the same plugin name.

* acec01dec35 win: Fix default fallback font for some languages
Fixed an issue querying a default font for certain languages not
supported by the primary system font.

* c14ef6aade5 QStandardPaths/unix: ignore relative paths in all $XDG_*
env vars
Improved conformance to the Freedesktop basedir spec by ignoring any
relative paths in XDG_* environment variables.

* 38bdcbd3a44 QDnsLookup/Unix: make sure we don't overflow the buffer
Fixed a bug that could cause a buffer overflow in Unix systems while
parsing corrupt, malicious, or truncated replies.

* 4e26f06a98a SQLite: Update SQLite to v3.42.0
Updated SQLite to v3.42.0

* f0b68ff6eeb PCRE2: upgrade to 10.42
PCRE2 has been updated to 10.42.

### qtsvg
* c4f0404 Don't rasterize gigantic shapes
Unreasonably large shapes are now ignored in SVG files to avoid
stalling the application. The check can be disabled by setting
QT_SVG_DISABLE_SIZE_LIMIT=1 in the environment.

* 03df51a QSvgFont: Initialize used member, remove unused
Fixed undefined behavior from using uninitialized variable.

### qtpositioning
* e6426f11 CoreLocation plugin: introduce RequestAlwaysPermission
parameter
Introduce an explicit RequestAlwaysPermission parameter to the
corelocation plugin. When specified and set to true, this parameters
enables the "Always" location request. When not specified or set to
false, only the "When In Use" location permission is requested. By
default this parameter is not specified.

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


Fixes
-----

### qtbase
* QTBUG-112162 QTimer::singleShot() can call receiver in wrong thread
* QTBUG-111027 Adding asset pack to package crashes androiddeployqt
* QTBUG-100128 QListWidget/QListView: item widget disappears when item
is dragged and dropped on itself
* QTBUG-56064 QStandardItem:: setEnabled() has no effect on QComboBox
items when SH_ComboBox_UseNativePopup is applied
* QTBUG-111347 QMessageAuthenticationCode is not re-entrant
* QTBUG-112534 QMultiHash functions (size, isEmpty) return unexpected
values
* QTBUG-97571 Text in column header is not elided for QHeaderView
* QTBUG-102745 Static plugin loaded twice
* QTBUG-96877 Qt6 won't render into cutout area (regression)
* QTBUG-108614 QComboBox will emit currentIndexChanged when the index
isn't changed
* QTBUG-112465 androiddeployqt fail on Android build platform:
android-33-ext5
* QTBUG-105921 Qt: OpenGL does not seem to work on Wayland? (NVIDIA
515.65.01)
* QTBUG-106701 Crash with any QML app on external display with iPadOS
16.1 on M1 iPad
* QTBUG-112735 Typo in QTextStream documentation ("ISO-5589-1")
* QTBUG-111869 irritating gotcha and crash in QCompleter popup()
* QTBUG-103792 TextField inside a multi sampling layer breaks rendering
with OpenGL RHI backend
* QTBUG-112953 QTextDocument::contentsChange is emitted several times
when iBus is on
* QTBUG-99990 windows: Painting an image with DPR >1.0  to a QPrinter
does not produce correct result
* QTBUG-58043 XDG environment variables with relative paths should be
ignored
* QTBUG-110080 Using FileDialog or FolderDialog makes the mouse cursor
disappear
* QTBUG-8682 QPlainTextEdit: When scrolling vertically using the arrow
keys then the valueChanged() signal is not emitted from the vertical
scrollbar
* QTBUG-25365 ValueChanged() signal is not emitted by QScrollBar when
Page Up/Dn is Hit in  QPlainTextEdit having scrollbar
* QTBUG-113127 It is qt_gl_read_framebuffer_rgba8 that cause a crash
which show info "nvoglv32!DrvPresentBuffers+0xf71ab" at the top of stack
nvoglv32.dll
* QTBUG-112816 REG [6.5.0->6.5.1] corelib/platform/androidnotifier not
compiling on Android
* QDS-9687 Examples cannot be downloaded
* QTBUG-112334 False doc for void QList::resize(qsizetype size)
* QTBUG-112697 QMessageBox return immediately on macOS if called from
MenuBar and after a modal dialog [REG]
* QTBUG-113289 Access to GL_POINT_SPRITE fails in GL core profile
* QTBUG-112990 QProcess::startDetached() freezes threads on QNX?
* QTBUG-113315 Segmentation fault in a VirtualBox Linux guest with
-march=native
* QTBUG-107545 Taking a second future from QPromise overwrites the first
one
* QTBUG-113209 Qt::ItemNeverHasChildren prevents itemChanged() from
being fired
* QTBUG-93768 Recursive loop with QCocoaAccessible::unignoredChildren
causes crash
* QTBUG-104785 [REGR:5->6] Performance regression in QLocale on macOS
* QTBUG-112738 QDir::entryInfoList() broken on Android when nameFilters
used
* QTBUG-112663 QFile on Android unable to open file content:// with
space in the name
* QTBUG-113337 [REG 6.4.3 -> 6.5.0] Integer overflow in qfixed_p.h when
rendering SVG image on the minimal plugin
* QTBUG-105323 [Regression] Keyboard is not properly hidden on ios
* QTBUG-110019 Address Book example crashes on exit
* QTBUG-111200 [REG: 5->6] QDomDocument now drops standalone attribute
* QTBUG-63481 tst_QSslSocket_onDemandCertificates_member::onDemandRootCe
rtLoadingMemberMethods tests fail in the CI
* QTBUG-94232 androiddeployqt is broken when manually defining
dependencies
* QTBUG-105109 Example code related to QHash::erase() fails clazy
* QTBUG-110632 Assertion failure in qqmltreemodeltotablemodel.cpp when
adding/removing files from directory watched by QFileSystemModel used by
TreeView
* QTBUG-78648 RHI: Does not work with Windows10 inside VMWare (Fusion)
* QTBUG-112746 QAnyStringView missing implicit conversion from char[]
with unknown size
* QTBUG-111514 QtCore fails to link with lld 16.0
* QTBUG-101648 On Windows Touch device(Surface Pro) need to know if
external keyboard is connected or not
* QTBUG-101875 Properly register the input devices on Android
* QTBUG-112432 wayland plugin should distinguish touchpads from mice,
etc.
* QTBUG-113706 WASM: QInputDevice::devices() erroneously reports that a
touchscreen exists
* QTBUG-113711 Windows: QInputDevice::devices() returns empty list

### qtsvg
* QTBUG-111850 [REG 6.2.2 -> 6.2.3] Loading particular svg file takes
far too long

### qtdeclarative
* QTBUG-112322 BorderImage docs: description of border property is in a
confusing place
* QTBUG-25244 SVG: Unsupported Image Format when using BorderImage
* QTBUG-32132 Qml do not updates roles names on
QAbstractItemModel::reset signal
* QTBUG-103220 QQmlDelegateModel::_q_modelReset should handle roleNames
changes
* QTBUG-105000 [REG: 5.15.2->5.15.10] State.when does not work for
objects anymore
* QTBUG-108024 [Non-qmlsc] `State.when` evaluation fails when an object
is bound
* QTBUG-105535 When PropertyChanges transitions to a constant value with
a PropertyAnimation, the binding from previous state is still active
* QTBUG-112354 AnchorChanges in states are not released
* QTBUG-106677 "Back" button breaks UI of Coffee Machine Example
* QTBUG-91425 DelegateModel: Crash when DelegateModelGroup is used for
delegate geometry and model is cleared
* QTBUG-109721 Non-Editable ComboBox wrongly propagates KeyEvent that
has already been accepted
* QTBUG-84920 StackView's depth is not updating after clear()
* QTBUG-110114 Qt Quick Controls Button: Unable to override
Accessible.role
* QTBUG-70939 QML ComboBox popup menu doesn't respect scaling
* QTBUG-112924 movementStarted/movementEnded signals are not emitted,
the flickStarted/flickEnded signals with flick behavior still occur.
* QTBUG-112945 QML RangeSlider does not work well on touch screen
* QTBUG-113442 qmlformat creates temp file with trailing "~" which is
not removed
* QTBUG-104987 REG: flicking TableView is broken
* QTBUG-99363 [Reg 5.15 -> 6.2] Properties are not set on createObject
* QTBUG-113446 KTX, ASTC, PKM image not displayed using NinePatchImage
* QTBUG-113565 Enhance the warning about the vendor and platform
specificness of compressed texture format support in the Image docs
* QTBUG-100678 QML Runtime Tool help all option is not working
* QTBUG-35244 QWindow visibility/visible property conflict
* QTBUG-111012 [Reg 5.15 -> 6.x] QSGGeometry::DrawLineLoop is no longer
supported
* QTBUG-106118 Changing contentItem to ScrollView breaks scrollbar
visibility
* QTBUG-113015 [QDoc] Duplicate QML property name causes confusion:
qml[attached]property QWindow::Visibility Window::visibility

### qtmultimedia
* QTBUG-108009 QML Camera maximumZoomFactor in iPad
* QTBUG-98102 [macOS] Specific video can't be played
* QTBUG-108083 Video color change while playing in QML MediaPlayer
* QTBUG-113008 REG [6.5.0->6.5.1] camera example not compiling on
Android
* QTBUG-112973 MediaPlayer example cannot open any file
* QTBUG-110005 windows: Crash if using asynchronous IO device as a media
source
* QTBUG-113029 Android: declarative-camera example: Captured image is
not rotated for landscape orientation
* QTBUG-105372 QML Camera - setting zoomFactor does not work
* QTBUG-112714 Unable to access camera
* QTBUG-111567 masOS audio deadlock with AudioOutputUnitStart /
AudioOutputUnitStop

### qttools
* QTBUG-112892 tst_macdeployqt::basicapp is failing randomly in lts-6.2

### qtdoc
* QTBUG-112327 Typo in the document?
* QTBUG-110022 Docs missed for ANDROID_MIN_SDK_VERSION and
ANDROID_TARGET_SDK_VERSION variables

### qtpositioning
* QTBUG-109359 Qt on iOS always asks for "always" location permission.

### qtsensors
* QTBUG-113435 dummy plugin gets built by default

### qtconnectivity
* QTBUG-111116 QT BLE scanner example causes high cpu usage
* QTBUG-112843 [REG 6.5.0->6.5.1] nfc/annotatedurl not compiling on
Android

### qtwayland
* QTBUG-110420 QtWayland fails to build

### qt3d
* QTBUG-101167 RenderSettings.OnDemand does not re-render if only
geometry got updated

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
* QTBUG-104869 QWebEngineDownloadItem::totalBytes() always returns -1
* QTBUG-111574 documentation is wrong for WebEngineCertificateError
* QTBUG-111784 Regression: macOS: Some video do not show pictures after
WebGL fix
* QTBUG-112007 Qt WebEngine 3rd party licensing documentation is
generated but hidden
* QTBUG-106359 QtPDF multipage example should switch to search result
tab during searching
* QTBUG-111939 Dependency update on qt/qtwebengine failed in 6.5.0
* QTBUG-106072 QtPdf can't open password-protected PDF files on
Windows/Android
* QTBUG-87275 Incorrect parsing of local urls in qml
* QTBUG-111894 [REG 6.4.3->6.4.2] webenginequick/quicknanobrowser not
launching
* QTBUG-111958 opus detection in QtWebEngine still needs perl
* QTBUG-88482 License terms are missing for Qtpdf
* QTBUG-112644 FileNotFoundError: [Errno 2] No such file or directory:
'Gn_EXECUTABLE-NOTFOUND'
* QTBUG-112282 Support Metal RHI
* QTBUG-112280 Support Metal and D3D RHI backends
* QTBUG-111067 Qt PDF Multipage example is crashing on desktop when
loading pdf files
* QTBUG-111909 QWebEngineView::print margin issues
* QTBUG-109401 Add DirectX support to QWebEngine
* QTBUG-112772 Developer tools open with "screencast" enabled (again)
* QTBUG-111697 Build failure with GCC 13
* QTBUG-112700 [REG] [macOS] Using getUserMedia() opens new window's tab
in Dock
* QTBUG-113109 [REG 6.4 -> 6.5] WebEngineScripts don't always run on
pages containing iframes
* QTBUG-113035 Under the current conditions specified in the
documentation, it is not possible to build the module through cross-
compilation
* QTBUG-112645 QWebEnginePage::WebWindowType not covered by tests
* QTBUG-113400 If QWebEngineProcess is terminated and a JavaScript is
being run that leads to crash
* QTBUG-112466 libQt6Pdf.so is always built with an embedded copy of
libpng
* QTBUG-113270 Improve docs with details about the use of GPL components
from Chromium
* QTBUG-113524 WebEngine cannot use https after using -sign-for-
notarization
* QTBUG-113579 Clipboard write action doesn't work on 6.5.0
* QTBUG-113802 CrossBuilding QtPdf fails because of wrong path to
qt.toolchain.cmake
* QTBUG-113859 [REG 6.4->6.5] Accessibility crash when clicking on a
link in a list on macOS
* QTBUG-112522 Webengine Widgets Client Certificate Example: Compilation
Fails
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
* QTBUG-111306 tst_MultiPageView::navigation uses fixed positions
* QTBUG-108154 Saving to MHTML while printing to PDF crashes with
SIGSEGV
* QTBUG-112685 CMake policies are not in sync between qt repos and
macros included in top-level CMakeLists.txt
* QTBUG-114883 [REG 6.2.8 -> 6.2.9] shadow build fails on windows,
webengine

### qtwebview
* QTBUG-114495  FAIL!  : tst_QWebView::load()

### qtcharts
* QTBUG-112917 sizeBy method of QScatterSeries is not behaving as
expected.
* QTBUG-112904 Scatter points become invisible or are plotted
incorrectly while size configuration is applied.
* QTBUG-112919 PointsConfiguration not cleared even when there are no
points in QScatterSeries

### qtquick3d
* QTBUG-101688 QtQuick3D: Fix compiler warnings for QNX

### qtmqtt
* QTBUG-111846 MQTT Subscriptions Example Crashes

Known Issues
------------

* Check that your system meets Qt's requirements:
https://doc.qt.io/qt-6.2/supported-platforms.html

* The RTA (release test automation) reported issues in Qt 6.2.x:
https://bugreports.qt.io/issues/?filter=23315

* Qt 6.2.9 Open issues in Jira:
https://bugreports.qt.io/issues/?filter=25172

Credits for the  release goes to:
---------------------------------

Eirik Aavitsland
Amir Masoud Abdol
Laszlo Agocs
Yigit Akcay
Anu Aliyas
Dimitrios Apostolou
Sebastian Beckmann
Rolf Eike Beer
Nicholas Bennett
Eskil Abrahamsen Blomfeldt
Mikolaj Boc
Joerg Bornemann
Assam Boudjelthia
Michael Brüning
Marco Bubke
Alexandru Croitor
Mitch Curtis
Giuseppe D'Angelo
Szabolcs David
Artem Dyomin
Alexey Edelev
David Edmundson
Christian Ehrlicher
Iikka Eklund
Andreas Eliasson
Fabio Falsini
David Faure
Ilya Fedin
Robert Griebl
Richard Moe Gustavsen
Lucie Gérard
Heikki Halmet
Jani Heikkinen
Ulf Hermann
Volker Hilsheimer
Sam James
Allan Sandfeld Jensen
Maurice Kalinowski
Jonas Karlsson
Friedemann Kleint
Michal Klocek
Lars Knoll
Seokha Ko
Tomi Korpipaa
Fabian Kosmale
Kai Köhne
Inho Lee
Jaehak Lee
Paul Lemire
Moody Liu
Robert Löhning
Thiago Macieira
Christophe Marin
Samuel Mira
Jan Moeller
Bartlomiej Moskal
Marc Mutz
Antti Määttä
Martin Negyokru
Mårten Nordheim
Dennis Oberst
Samuli Piippo
Rami Potinkara
The Qt Project
Liang Qi
Topi Reinio
Aleksandr Reviakin
Alexey Rochev
Shawn Rutledge
Toni Saario
Ahmad Samir
Dmitry Shachnev
Venugopal Shivashankar
Ivan Solovev
Axel Spoerl
Christian Strømme
Tarja Sundqvist
Benjamin Terrier
Peter Varga
Doris Verria
Tor Arne Vestbø
Bernd Weimer
Edward Welbourne
Oliver Wolff
Semih Yavuz
