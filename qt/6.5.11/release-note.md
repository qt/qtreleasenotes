Release note
============

Qt 6.5.11 long-term supported (LTS) commercial release is a patch
release made on the top of Qt 6.5.10. As a patch release,
Qt 6.5.11 does not add any new functionality but provides bug fixes and
other improvements and maintains both forward and backward
compatibility (source and binary) with the 6.5.x series.

Source codes are available via the Qt online installer and
the Qt Code Review tool (https://codereview.qt-project.org/). To get the
sources via Qt Code Review, you need to log in with a Qt Account that
has a valid commercial license. For detailed instructions, see
https://wiki.qt.io/Qt_6.5_Release#Getting_Source_Codes.

For detailed information about Qt, see the Qt 6.5 online documentation:
https://doc.qt.io/qt-6.5/.

Important Changes
-----------------

### qtbase
* 80f09dce0c7 qvsnprintf: fail if the result size doesn't fit into an
int
Fixed a bug that would cause q(v)snprintf() to report success on some
platforms, even though the result was truncated.

* 3987a7601eb Upgrade Harfbuzz to 11.4.1
Upgraded Harfbuzz to version 11.4.1.

* d129e4ae782 QJsonDocument/Value: fix integer truncation in
fromJson(QByteArray)
Fixed a bug on 64-bit platforms where fromJson(QByteArray) could report
one of the Unterminated errors for valid input whose size merely
exceeded INT_MAX (2GiB).

* 008396a4886 Upgrade PCRE2 to 10.46
PCRE2 was updated to version 10.46.

* 18b0dd976f7 Suppress construction of QTimeZone(Qt::TimeSpec)
Construction from a Qt::TimeSpec, which was never meant to be
supported, is now rejected at compile time, where previously compilers
(mis)interpreted the enum as an int so called the (int offsetSeconds)
constructor, with results consistently at odds with what the user
presumably expected.

* 702051c07d9 QUrl: fix comparisons of URLs with password but no
explicit username
Fixed a number of bugs in QUrl where a URL modified using the setXxx()
functions would fail to compare equal to itself after going through
toString() and setUrl() round-trip.

* 4ac3f21552a Upgrade Harfbuzz to 11.4.5
Upgraded Harfbuzz to version 11.4.5.

* 259ce11e836 Update bundled libjpeg-turbo to version 3.1.2
libjpeg-turbo was updated to version 3.1.1

* e95ae3a7c9c Update Freetype to 2.14.0
Updated bundled Freetype to 2.14.0.

* f188c6fe3c0 Upgrade Harfbuzz to 11.5.0
Upgraded Harfbuzz to version 11.5.0.

* 71b517ef57e Update Freetype to 2.14.1
Updated bundled Freetype to 2.14.1.

* 32e157cdf5b Upgrade Harfbuzz to 11.5.1
Upgraded Harfbuzz to version 11.5.1.

* cb5089767b4 Upgrade Harfbuzz to 12.1.0
Upgraded Harfbuzz to version 12.1.0.

* a4e374e1e94 Upgrade PCRE2 to 10.47
PCRE2 was updated to version 10.47.

* 4537ed92a1c Upgrade Harfbuzz to 12.2.0
Upgraded Harfbuzz to version 12.2.0.

* 993547d1194 SQLite: Update SQLite to v3.51.0
Updated SQLite to v3.51.0

### qtdeclarative
* 2c0b9362b1 Initialize QQuickGradientStop position to zero
The position property is now always initialized to 0.0; previously it
was left uninitialized.

### qtmultimedia
* a56a5b757 Update FFmpeg version in documentation
Updated FFmpeg to n7.1.2.

### qtimageformats
* f88f413 Update bundled libtiff to version 4.7.1
Bundled libtiff was updated to version 4.7.1

### qtopcua
* e51d4b2e Fix status code handling for monitored items
Report the right status code for monitored item updates


Fixes
-----

### qtbase
* [QTBUG-135964](https://bugreports.qt.io/browse/QTBUG-135964) Windows theme uses wrong colors if high-contrast mode is
activated
* [QTBUG-138561](https://bugreports.qt.io/browse/QTBUG-138561) QFont::exactMatch index out of bounds
* [QTBUG-129193](https://bugreports.qt.io/browse/QTBUG-129193) Qt compiled with gcc 13 and -march=bdver4/-mtune=bdver4
causes segfaults in tests, downstream applications
* [QTBUG-139128](https://bugreports.qt.io/browse/QTBUG-139128) QObject::connect(): clarify what a valid method is, in
the string-based overloads
* [QTBUG-139211](https://bugreports.qt.io/browse/QTBUG-139211) tst_qquickpopup (Failed)
* [QTBUG-100991](https://bugreports.qt.io/browse/QTBUG-100991) Some tests crash on Android CI
* [QTBUG-131695](https://bugreports.qt.io/browse/QTBUG-131695) tst_qquickpopup tst_QQuickPopup::fadeDimmer is flaky
* [QTBUG-125083](https://bugreports.qt.io/browse/QTBUG-125083) [Android] ANRs related to QtNativeInputConnection
* [QTBUG-132695](https://bugreports.qt.io/browse/QTBUG-132695) Crash in QGuiApplication::applicationStateChanged() when
quitting app
* [QTBUG-139400](https://bugreports.qt.io/browse/QTBUG-139400) Properly manage QtEditText focus and InputConnection
callbacks
* [QTBUG-76976](https://bugreports.qt.io/browse/QTBUG-76976) QSortFilterProxyModel::mapFromSource returns a valid
QModelIndex for the filtered out item
* [QTBUG-138946](https://bugreports.qt.io/browse/QTBUG-138946) QSlider issues on macOS 26
* [QTBUG-138465](https://bugreports.qt.io/browse/QTBUG-138465) Line edits are not visible on macOS 26
* [QTBUG-139360](https://bugreports.qt.io/browse/QTBUG-139360) Editable combo box on macOS Tahoe
* [QTBUG-132911](https://bugreports.qt.io/browse/QTBUG-132911) Typo in QPermission docs
* [QTBUG-121586](https://bugreports.qt.io/browse/QTBUG-121586) [Reg 5.15->6.x] QActionGroup signals missing from
documentation
* [QTBUG-138678](https://bugreports.qt.io/browse/QTBUG-138678) Crash in QTextEdit while inserting a column into a HTML
table
* [QTBUG-129689](https://bugreports.qt.io/browse/QTBUG-129689) QStorageInfo valid information not reset after path is
cleared on Linux
* [QTBUG-120031](https://bugreports.qt.io/browse/QTBUG-120031) xcb: Modal state may get lost due to a race
* [QTBUG-139983](https://bugreports.qt.io/browse/QTBUG-139983) macOS (Tahoe): assert in
tst_QStyleSheetStyle::complexWidgetFocus()
* [QTBUG-127528](https://bugreports.qt.io/browse/QTBUG-127528) QApplication::fontMetrics() deprecation message is too
vague
* [QTBUG-119753](https://bugreports.qt.io/browse/QTBUG-119753) QSqlRecord access causes hang/memory leak and crash
using QODBC driver
* [QTBUG-137120](https://bugreports.qt.io/browse/QTBUG-137120) [Regression] Right and top dockwidget area are not
resizable anymore
* [QTBUG-139930](https://bugreports.qt.io/browse/QTBUG-139930)  [REG 6.5.9 -> 6.5.10] Unable to resize QDockWidget when
placed in top/right dock area
* [QTBUG-120688](https://bugreports.qt.io/browse/QTBUG-120688) Explicitly document behavior for QFileInfo if file is
directory
* [QTBUG-136485](https://bugreports.qt.io/browse/QTBUG-136485) QDockWidgets sends visibilityChanged on destruction
* [QTBUG-139944](https://bugreports.qt.io/browse/QTBUG-139944) macOS: title/text alignment on push buttons
* [QTBUG-40561](https://bugreports.qt.io/browse/QTBUG-40561) QDomText::splitText leaks memory
* [QTBUG-140203](https://bugreports.qt.io/browse/QTBUG-140203) [qtbase] Build failure with -no-ssl
* [QTBUG-134896](https://bugreports.qt.io/browse/QTBUG-134896) QUrl's qHash() is inconsistent with its operator==
* [QTBUG-134900](https://bugreports.qt.io/browse/QTBUG-134900) QUrl's operator==() is taking bygone data into account
* [QTBUG-138459](https://bugreports.qt.io/browse/QTBUG-138459) WindowStaysOnTopHint flag removes fullscreen on window
* [QTBUG-122674](https://bugreports.qt.io/browse/QTBUG-122674) Build failure on x32 ABI
* [QTBUG-138947](https://bugreports.qt.io/browse/QTBUG-138947) QProgressBar completely blank on macOS 26
* [QTBUG-138942](https://bugreports.qt.io/browse/QTBUG-138942) Mac style (Widget and Quick) has issues on macOS 26
* [QTBUG-131923](https://bugreports.qt.io/browse/QTBUG-131923) QPainter::drawImage with CompositionMode_Source into
non-alpha image format produces transparent pixels
* [QTBUG-140856](https://bugreports.qt.io/browse/QTBUG-140856) Android software keyboard is not working in landscape
mode
* [QTBUG-140672](https://bugreports.qt.io/browse/QTBUG-140672) [VxWorks] 6.8.4 -> 6.8.5 build regression on Intel in
qfloat16.h
* [QTBUG-112898](https://bugreports.qt.io/browse/QTBUG-112898) i letter should be İ in uppercase in Turkish
* [QTBUG-138583](https://bugreports.qt.io/browse/QTBUG-138583) QLocale::toUpper() is not 64-bit-safe on ICU
* [QTBUG-134093](https://bugreports.qt.io/browse/QTBUG-134093) Android application crashes on 16 KB page size
* [QTBUG-2163](https://bugreports.qt.io/browse/QTBUG-2163) Support for conditions in special casing of unicode
characters is missing in Qt
* [QTBUG-107028](https://bugreports.qt.io/browse/QTBUG-107028) tst_qquicktextfield and tst_qquicktextarea fail on
Android
* [QTBUG-100259](https://bugreports.qt.io/browse/QTBUG-100259) tst_controls crash on Android
* [QTBUG-100258](https://bugreports.qt.io/browse/QTBUG-100258) tst_focus crashes on Android
* [QTBUG-139415](https://bugreports.qt.io/browse/QTBUG-139415) tst_controls has failing test cases
* [QTBUG-138705](https://bugreports.qt.io/browse/QTBUG-138705) Windows backend of QLocale::toLower() does not implement
Greek Final Sigma rule
* [QTBUG-37759](https://bugreports.qt.io/browse/QTBUG-37759) QWidget-gestures do not work
* [QTBUG-46195](https://bugreports.qt.io/browse/QTBUG-46195) [Windows]: Swipe gesture is not always recognized and
sometimes in the wrong direction
* [QTBUG-138699](https://bugreports.qt.io/browse/QTBUG-138699) Square push buttons (macOS 26)
* [QTBUG-138700](https://bugreports.qt.io/browse/QTBUG-138700) Tabs have wrong shape on macOS 26
* [QTBUG-138948](https://bugreports.qt.io/browse/QTBUG-138948) Radio button alignment issues on macOS 26
* [QTBUG-138738](https://bugreports.qt.io/browse/QTBUG-138738) Incorrect focus ring rendering
* [QTBUG-138893](https://bugreports.qt.io/browse/QTBUG-138893) QTimeZone(Qt::UTC) returns incorrect UTC offset (+1
second)
* [QTBUG-136493](https://bugreports.qt.io/browse/QTBUG-136493) FFmpeg not properly configured with multi-abi builds
* [QTBUG-138659](https://bugreports.qt.io/browse/QTBUG-138659) QTextBoundaryFinder is copyable (deep-copies lookup
tables), but not movable
* [QTBUG-139951](https://bugreports.qt.io/browse/QTBUG-139951) [VxWorks] 6.8.4 -> 6.8.5 regression build failure with
VxWorks 24.03
* [QTBUG-66621](https://bugreports.qt.io/browse/QTBUG-66621) webassembly: strings with toUpper() not correct
* [QTBUG-69421](https://bugreports.qt.io/browse/QTBUG-69421) WebAssembly: characters are not displayed properly
* [QTBUG-74511](https://bugreports.qt.io/browse/QTBUG-74511) Possible REG: Wasm changes in qunicodetables will be lost
* [QTBUG-140643](https://bugreports.qt.io/browse/QTBUG-140643) QLocale::timeFormat(QLocale::NarrowFormat) returns
seconds for some locales

### qtdeclarative
* [QTBUG-94251](https://bugreports.qt.io/browse/QTBUG-94251) tst_QQuickPopup fails with OpenSUSE 15.3
* [QTBUG-133256](https://bugreports.qt.io/browse/QTBUG-133256) Crash on dynamically removing items from a custom
QtQuick.Controls.Container with transitions
* [QTBUG-46798](https://bugreports.qt.io/browse/QTBUG-46798) Destroying an item crashes ListView
* [QTBUG-78261](https://bugreports.qt.io/browse/QTBUG-78261) tst_focus::policy is failing
* [QTBUG-78162](https://bugreports.qt.io/browse/QTBUG-78162) tst_qquicktextinput::mouseSelectionMode() is flaky on
OpenSuse 15.0
* [QTBUG-137160](https://bugreports.qt.io/browse/QTBUG-137160) qt quick Loader active=false with unfinished Menu crash
* [QTBUG-139552](https://bugreports.qt.io/browse/QTBUG-139552) tst_qquickmenu: Test case loadMenuAsynchronously fails
due to warning
* [QTBUG-137172](https://bugreports.qt.io/browse/QTBUG-137172) "section" property in ListView behaviour is broken
(degradation)
* [QTBUG-138480](https://bugreports.qt.io/browse/QTBUG-138480) Top flaky test:
tst_qquickwidget::focusOnClickInProxyWidget
* [QTBUG-138465](https://bugreports.qt.io/browse/QTBUG-138465) Line edits are not visible on macOS 26
* [QTBUG-141161](https://bugreports.qt.io/browse/QTBUG-141161) FAIL!  : tst_qquickwidget::focusOnClickInProxyWidget()
Received a fatal error.
* [QTBUG-139400](https://bugreports.qt.io/browse/QTBUG-139400) Properly manage QtEditText focus and InputConnection
callbacks
* [QTBUG-141182](https://bugreports.qt.io/browse/QTBUG-141182) QML ProgressBar has broken layout on macOS 26
* [QTBUG-141105](https://bugreports.qt.io/browse/QTBUG-141105) [REG] SIGSEGV in QQmlDelegateModelItem::destroyObject(),
accesses invalid QObjectData
* [QTBUG-140900](https://bugreports.qt.io/browse/QTBUG-140900) Crash when assigning a function declaration to a
ListElement(for nested lists)
* [QTBUG-139211](https://bugreports.qt.io/browse/QTBUG-139211) tst_qquickpopup (Failed)
* [QTBUG-139306](https://bugreports.qt.io/browse/QTBUG-139306) Popup inside an async Loader crashes Qt Quick app if
there is direct property binding (possible racing condition)
* [QTBUG-138947](https://bugreports.qt.io/browse/QTBUG-138947) QProgressBar completely blank on macOS 26
* [QTBUG-138942](https://bugreports.qt.io/browse/QTBUG-138942) Mac style (Widget and Quick) has issues on macOS 26
* [QTBUG-138946](https://bugreports.qt.io/browse/QTBUG-138946) QSlider issues on macOS 26
* [QTBUG-140364](https://bugreports.qt.io/browse/QTBUG-140364) QQuickGradientStop does not use default position when it
is not provided

### qtmultimedia
* [QTBUG-135021](https://bugreports.qt.io/browse/QTBUG-135021) docs link to QVideoFrameFormat::PixelFormat goes to
wikipedia instead
* [QTBUG-137950](https://bugreports.qt.io/browse/QTBUG-137950) Application crash when loading a camera CaptureSession
on Windows

### qttools
* [QTBUG-126189](https://bugreports.qt.io/browse/QTBUG-126189) [REG 6.7.1->6.7.2&6.8.0] lconvert, lrelease, lupdate and
few others not combiled in no-gui build
* [QTBUG-125066](https://bugreports.qt.io/browse/QTBUG-125066) Configure fails in qttools if PrintSupport is disabled

### qtlocation
* [QTBUG-139780](https://bugreports.qt.io/browse/QTBUG-139780) Qt Positioning: Discrepancy between documented type
names and actual type names

### qtpositioning
* [QTBUG-139654](https://bugreports.qt.io/browse/QTBUG-139654) Update QtPositioning documentation to use QDoc commands
* [QTBUG-139780](https://bugreports.qt.io/browse/QTBUG-139780) Qt Positioning: Discrepancy between documented type
names and actual type names
* [QTBUG-139560](https://bugreports.qt.io/browse/QTBUG-139560) Access functions are documented even when their
properties are not

### qtwayland
* [QTBUG-139250](https://bugreports.qt.io/browse/QTBUG-139250) Top-level tool window doesnt oppen
* [QTBUG-135354](https://bugreports.qt.io/browse/QTBUG-135354) wayland\custom-extension and wayland\custom-shell
examples fails to build with Boot to Qt on Windows
* [QTBUG-130652](https://bugreports.qt.io/browse/QTBUG-130652) REG: Hiding and reshowing a sub-window crashes Wayland
client
* [QTBUG-101948](https://bugreports.qt.io/browse/QTBUG-101948) QWaylandWindow::doApplyConfigure called from the wrong
thread

### qtwebengine
* [QTBUG-138159](https://bugreports.qt.io/browse/QTBUG-138159) Build error:
QtWebEngineCore/private/qtwebenginecoreglobal_p.h: No such file or
directory
* [QTBUG-127109](https://bugreports.qt.io/browse/QTBUG-127109) trouble configuring QtPDF for iOS
* [QTBUG-138881](https://bugreports.qt.io/browse/QTBUG-138881) Windows Debug: QQuickWebEngineScriptCollection crashes
after adding custom library path
* [QTBUG-136622](https://bugreports.qt.io/browse/QTBUG-136622) Accessiblity:voice over can't read table content

### qtvirtualkeyboard
* [QTBUG-139038](https://bugreports.qt.io/browse/QTBUG-139038) Overlay issue with Virtual Keyboard + Material Style
* [QTBUG-124178](https://bugreports.qt.io/browse/QTBUG-124178) Virtualkeyboard of Qt 5.15.15 crash on Ubuntu
* [QTBUG-126402](https://bugreports.qt.io/browse/QTBUG-126402) QML virtual keyboard behavior regression between 5.x and
6.x
* [QTBUG-137731](https://bugreports.qt.io/browse/QTBUG-137731) Shadow Input is not properly displayed with
DesktopInputPanel with fullScreenMode = true
* [QTBUG-140553](https://bugreports.qt.io/browse/QTBUG-140553) qmllint does not recognize
VirtualKeyboardSettings.wordCandidateList
* [QTBUG-136149](https://bugreports.qt.io/browse/QTBUG-136149) Qt Virtual Keyboard: Add alt texts

### qtremoteobjects
* [QTBUG-139754](https://bugreports.qt.io/browse/QTBUG-139754) FAIL!  : tst_clientSSL::testRun()
'socketClient->waitForEncrypted(-1)' returned FALSE

### qtquick3d
* [QTBUG-136334](https://bugreports.qt.io/browse/QTBUG-136334) The documentation of qt6_add_lightprobe_images is
missing
* [QTBUG-140780](https://bugreports.qt.io/browse/QTBUG-140780) Setting Sphere Geometry pickable: true, causes crash in
Quick 3D
* [QTBUG-139324](https://bugreports.qt.io/browse/QTBUG-139324) Quick3D Frame view is empty in creator QML profiler

Known Issues
------------

Credits for the release goes to:
---------------------------------

Eirik Aavitsland  
Chris Adams  
Albert Astals Cid  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
David Boddie  
Joerg Bornemann  
Assam Boudjelthia  
Marcell Brauner  
Aurélien Brooke  
Kai Uwe Broulik  
Michael Brüning  
Eren Bursali  
Olivier De Cannière  
Kaloyan Chehlarski  
Mitch Curtis  
Giuseppe D'Angelo  
Pavel Dubsky  
Alexey Edelev  
Christian Ehrlicher  
Andreas Eliasson  
David Faure  
Robert Griebl  
Richard Moe Gustavsen  
Moss Heim  
Ulf Hermann  
Volker Hilsheimer  
Samuli Hölttä  
Morteza Jamshidi  
Allan Sandfeld Jensen  
Jonas Karlsson  
Igor Khanin  
Michal Klocek  
Sze Howe Koh  
Jarkko Koivikko  
Antti Kokko  
Santhosh Kumar  
Kai Köhne  
Frédéric Lefebvre  
Robert Löhning  
Thiago Macieira  
Marc Mutz  
Antti Määttä  
Mårten Nordheim  
Karim Pinter  
Timur Pocheptsov  
Rami Potinkara  
Dheerendra Purohit  
Khem Raj  
Matthias Rauter  
Topi Reinio  
Shawn Rutledge  
Ahmad Samir  
SanthoshKumar Selvaraj  
Ivan Solovev  
Axel Spoerl  
Tarja Sundqvist  
Paul Olav Tvete  
Tor Arne Vestbø  
Jannis Voelker  
Edward Welbourne  
Zhao Yuhang  
