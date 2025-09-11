Release note
============
Qt 6.2.13 release is a patch release made on the top of Qt 6.2.12. As a patch
release, Qt 6.2.13 does not add any new functionality but provides bug fixes
and other improvements.
For detailed information about Qt, see the Qt 6.2 online documentation:
https://doc.qt.io/qt-6.2/.

Important Changes
-----------------

### Security fixes
* CVE-2024-39936 in qtbase
* CVE-2024-36048 in qtnetworkauth
* CVE-2023-7104 in qtwebengine
* CVE-2024-2625: Object lifecycle issue in V8 in qtwebengine
* CVE-2024-2626: Out of bounds read in Swiftshader in qtwebengine
* CVE-2024-3157: Out of bounds write in Compositing in qtwebengine
* CVE-2024-3159: Out of bounds memory access in V8 in qtwebengine
* CVE-2024-3516: Heap buffer overflow in ANGLE in qtwebengine
* CVE-2024-3837: Use after free in QUIC in qtwebengine
* CVE-2024-3839: Out of bounds read in Fonts in qtwebengine
* CVE-2024-3914: Use after free in V8 in qtwebengine
* CVE-2024-4058: Type Confusion in ANGLE in qtwebengine
* CVE-2024-4558: Use after free in ANGLE in qtwebengine
* CVE-2024-5274: Type Confusion in V8 in qtwebengine
* CVE-2024-5496: Use after free in Media Session in qtwebengine
* CVE-2024-5499: Out of bounds write in Streams API in qtwebengine
* CVE-2024-5840: Policy Bypass in CORS in qtwebengine
* CVE-2024-5841: Use after free in V8 in qtwebengine
* CVE-2024-5845: Use after free in Audio in qtwebengine
* CVE-2024-5846: Use after free in PDFium in qtwebengine
* CVE-2024-5847: Use after free in PDFium in qtwebengine
* CVE-2024-6291: Use after free in Swiftshader in qtwebengine
* CVE-2024-6989: Use after free in Loader in qtwebengine
* CVE-2024-6992: Out of bounds memory access in ANGLE in qtwebengine
* CVE-2024-6993: Inappropriate implementation in Canvas in qtwebengine
* CVE-2024-6996: Race in Frames in qtwebengine
* CVE-2024-7000: Use after free in CSS in qtwebengine
* CVE-2024-7532: Out of bounds memory access in ANGLE in qtwebengine
* CVE-2024-7535: Inappropriate implementation in V8 in qtwebengine
* CVE-2024-7536: Use after free in WebAudio in qtwebengine
* Security bug 40063014 in qtwebengine
* Security bug 40068800 in qtwebengine
* Security bug 40940917 in qtwebengine
* Security bug 41495984 in qtwebengine
* Security bug 326349405 in qtwebengine
* Security bug 326521449 in qtwebengine
* Security bug 327183408 in qtwebengine
* Security bug 327698060 in qtwebengine
* Security bug 329674887 in qtwebengine
* Security bug 333453962 in qtwebengine
* Security bug 336214779 in qtwebengine
* Security bug 339736513 in qtwebengine
* Security bug 340606786 in qtwebengine
* Security bug 340895241 in qtwebengine
* Security bug 341640868 in qtwebengine
* Security bug 329699609 in qtwebengine
* Security bug 338574384 in qtwebengine
* Security bug 340221135 in qtwebengine

### qtbase
* dd9698343ee SQLite: Update SQLite to v3.45.2
Updated SQLite to v3.45.2

* e5b126aff0f SQLite: Update SQLite to v3.45.3
Updated SQLite to v3.45.3

* 8c6d4def377 Update bundled libjpeg-turbo to version 3.0.3
libjpeg-turbo was updated to version 3.0.3

* 0526ab34af3 Update public suffix list
Updated the public suffix list to upstream SHA
903a83ff7bfc3148e3692e09396f9f3bdc9462ef.

* 97b56515de0 Change the mimetype database embedded into QtCore
For licensing reasons, QtCore no longer ships a copy of the MIME
database from freedesktop.org's shared-mime-info project, but the one
from the Apache Tika project. The tika definitions don't have icons or
translated descriptions, but are sufficient for matching file types.

* f48bf9431f1 QMimeDatabase: pick up XML mimetypes from :/qt-
project.org/mime/packages
QMimeDatabase can now pick up XML mimetype definitions from :/qt-
project.org/mime/packages. GPL-compatible projects which provide self-
contained binaries can use this to provide a copy of freedesktop.org.xml
that will be used instead of the TIKA mimetypes.

* 04094bd913a Add __attribute__((format(printf()))) to q(v)nprintf()
Added attributes for GCC-compatible compilers to detect format/argument
mismatches. If this throws warnings for your calls now, don't ignore
them. printf() format mistakes could be security-relevant. You may also
find that you relied on undocumented behavior, such as that certain
implementations (Windows, Android, WASM) of qsnprintf() support
char16_t* instead of wchar_t* for %ls. In that case, you should port to
qUtf16Printable() and QString::asprintf(), or suppress the warning and
port away from the platform dependence at your earliest convenience.

* 6baf85f92c0 QArrayDataOps: fix FP equality comparison
Fixed a bug when two QLists holding NaN values were considered to be
equal.

* ff8fecc4b8f Fix partial_ordering::unordered != 0 comparison
Fixed a bug where partial_ordering::unordered != 0 comparison produced
an incorrect result.

* d5ce641d9a8 PCRE: upgrade to 10.44
PCRE2 was updated to version 10.44.

* 24ab9089296 SQLite: Update identified license
Change identified license for SQLite from 'Public Domain' to more
accurate 'SQLite Blessing': https://spdx.org/licenses/blessing.html

* 57cfdd09679 SQLite: Update SQLite to v3.46.0
Updated SQLite to v3.46.0

* 3a0fd5f7cb9 SQLite: Update SQLite to v3.46.1
Updated SQLite to v3.46.1

* 13ab2d7795e Update Freetype to 2.13.3
Updated bundled Freetype to version 2.13.3.

### qtdoc
* 18fc38e83 Update iOS supported platforms and toolchain to iOS 17/Xcode
15
Xcode 15 is now both supported and required for Qt for iOS. To develop
for iOS 17 devices, please use Qt Creator 13, or generate an Xcode
project using qmake or CMake and use Xcode directly.

### qtconnectivity
* 19be33ef sdpscanner: fix format strings for (u)int64_t
Fixed a bug involving broken serialization of SDP_(U)INT64 DTDs on Big-
Endian machines.

### qtimageformats
* a20536e0 Update bundled libwebp to version 1.4.0
Update bundled libwebp to version 1.4.0


Fixes
-----

### qtbase
* [QTBUG-123454](https://bugreports.qt.io/browse/QTBUG-123454) Windows DirectWrite fontengine crash with fractional dpi
and woff / woff2 fonts
* [QTBUG-123324](https://bugreports.qt.io/browse/QTBUG-123324) dSYM warning: skipping debug map object with duplicate
name and timestamp
* [QTBUG-123032](https://bugreports.qt.io/browse/QTBUG-123032) [REG: 6.6.1->6.6.2] Override cursor changes together
with window creation and destruction crashes on KDE
* [QTBUG-124254](https://bugreports.qt.io/browse/QTBUG-124254) Names can start with a non-letter char in Address Book
example
* [QTBUG-123848](https://bugreports.qt.io/browse/QTBUG-123848) Short cuts involving 2 (or more) modifier keys are not
longer handled by the Input Methods on macos.
* [QTBUG-106516](https://bugreports.qt.io/browse/QTBUG-106516) Multi-modifier key events not correctly handled on macOS
* [QTBUG-103019](https://bugreports.qt.io/browse/QTBUG-103019) MinGW Qt6Platform.pc has an extra '>' after '-D_UNICODE'
* [QTBUG-123054](https://bugreports.qt.io/browse/QTBUG-123054) Reg[5->6] QSvgRenderer generated images are not
identical
* [QTBUG-111960](https://bugreports.qt.io/browse/QTBUG-111960) NPE: Attempt to invoke virtual method
setActivityDisplayRotation() on a null object reference
* [QTBUG-125531](https://bugreports.qt.io/browse/QTBUG-125531) Unable to drag files into the xwayland widget of
QTextEdit
* [QTBUG-86203](https://bugreports.qt.io/browse/QTBUG-86203) Documentation on QtAndroid:androidService(),
QtAndroid:androidContext() unclear
* [QTBUG-126084](https://bugreports.qt.io/browse/QTBUG-126084) QDockWidget unplugged from floating tab is in the wrong
position
* [QTBUG-126524](https://bugreports.qt.io/browse/QTBUG-126524) can't build 6.2 on Linux
* [QTBUG-126381](https://bugreports.qt.io/browse/QTBUG-126381) qcssparser.cpp ASSERT: "d->parsed.metaType() ==
QMetaType::fromType<QList<QVariant>>()"
* [QTBUG-126610](https://bugreports.qt.io/browse/QTBUG-126610) HTTP2 Support leaks information
* [QTBUG-123554](https://bugreports.qt.io/browse/QTBUG-123554) xcb: Enabling touch device while application is running
causes a crash on first touch
* [QTBUG-127055](https://bugreports.qt.io/browse/QTBUG-127055) QThread::terminate() ABA problem
* [QTBUG-126820](https://bugreports.qt.io/browse/QTBUG-126820) Move all QKeyCombination-returning operators into the
namespace Qt
* [QTBUG-127473](https://bugreports.qt.io/browse/QTBUG-127473) [REG 5.15 -> 6] QList::op==() is broken for FP types
* [QTBUG-127512](https://bugreports.qt.io/browse/QTBUG-127512) tst_QTextLayout::softHyphens(16) failed on Ubuntu
24.04(both x64 and arm64) GNOME
* [QTBUG-127392](https://bugreports.qt.io/browse/QTBUG-127392) Avoid warning: Ignoring window icon xxx exceeds maximum
xcb request length 65535
* [QTBUG-127759](https://bugreports.qt.io/browse/QTBUG-127759) Qt::partial_ordering::unordered implements op!=()
incorrectly
* [QTBUG-124310](https://bugreports.qt.io/browse/QTBUG-124310) QT_DISTANCEFIELD_DEFAULT_BASEFONTSIZE=128 causes a
QDistanceField crash
* [QTBUG-127926](https://bugreports.qt.io/browse/QTBUG-127926) Outdated Android docs still refer to
QtAndroid::androidActivity()
* [QTBUG-122967](https://bugreports.qt.io/browse/QTBUG-122967) [macOS]Calling winId() renders additional undesired
pixmap if scaling factor is not 1
* [QTBUG-116577](https://bugreports.qt.io/browse/QTBUG-116577) ASSERT: "sumFactors > 0.0"  in qgridlayoutengine.cpp
* [QTBUG-117500](https://bugreports.qt.io/browse/QTBUG-117500) Sporadic crash on  QFontEngineMulti::ensureEngineAt()
* [QTBUG-109367](https://bugreports.qt.io/browse/QTBUG-109367) Android native ExtractEditText does not receive text
updates from qml TextEdit in fullscreen mode and landscape orientation
* [QTBUG-101307](https://bugreports.qt.io/browse/QTBUG-101307) tst_qbytearrayview fails to compile with ubsan
* [QTBUG-125588](https://bugreports.qt.io/browse/QTBUG-125588) QString::arg(char16_t{}) prefers the integral, not the
QChar overload
* [QTBUG-126053](https://bugreports.qt.io/browse/QTBUG-126053) QString::arg(u8' ') prefers the integral, not the QChar
overload, when built in C++20
* [QTBUG-126054](https://bugreports.qt.io/browse/QTBUG-126054) QString::arg(wchar_t{}) prefers the integral overload
instead of the QChar one
* [QTBUG-126055](https://bugreports.qt.io/browse/QTBUG-126055) [REG SiC 6.4 -> 6.5] QString::arg(qfloat16{}) is
ambiguous if QFLOAT16_IS_NATIVE
* [QTBUG-124572](https://bugreports.qt.io/browse/QTBUG-124572) Program crash when using a specific glyph from a popular
font file on Linux
* [QTBUG-124465](https://bugreports.qt.io/browse/QTBUG-124465) QDate::fromString very slow in 6.7.0
* [QTBUG-127110](https://bugreports.qt.io/browse/QTBUG-127110) Platforms still use the inefficient qvsnprintf() fall-
back
* [PYSIDE-2492](https://bugreports.qt.io/browse/PYSIDE-2492) uic does not generate enumeration name into enum values
causing type checking warnings
* [QTBUG-91077](https://bugreports.qt.io/browse/QTBUG-91077) startSystemMove/startSystemResize causing mouse events to
be lost on X11(MATE)
* [QTBUG-104867](https://bugreports.qt.io/browse/QTBUG-104867) QtTest: QCOMPARE prints matching <null>s for mismatches
when unable to convert to string
* [QTBUG-125730](https://bugreports.qt.io/browse/QTBUG-125730) QAnyStringView('\xE4') creates an invalid UTF-8 string
(expected: valid L1)

### qtdeclarative
* [QTBUG-123111](https://bugreports.qt.io/browse/QTBUG-123111) Particle System Application stuck on GUI thread
* [QTBUG-121128](https://bugreports.qt.io/browse/QTBUG-121128) [REG 6.5.3 -> 6.5.4][Reg 6.2.10 -> 6.2.11] QModelIndex
is not a type error
* [QTBUG-120506](https://bugreports.qt.io/browse/QTBUG-120506) [Reg 6.5 -> 6.6] Using `CameraLens.ProjectionType` as
type hinting cause runtime error
* [QTBUG-122252](https://bugreports.qt.io/browse/QTBUG-122252) [REG: 6.4->6.5] Qt.point cannot be used as a return type
* [QTBUG-113384](https://bugreports.qt.io/browse/QTBUG-113384) QQuickWidget - touchpad click not working after
scrolling
* [QTBUG-123395](https://bugreports.qt.io/browse/QTBUG-123395) QML EXC_BAD_ACCESS crash
* [QTBUG-123596](https://bugreports.qt.io/browse/QTBUG-123596) Crash JS for x in o  { delete o[x] } if o is a
sparsearray
* [QTBUG-83408](https://bugreports.qt.io/browse/QTBUG-83408) Text disappears with ElideRight.
* [QTBUG-33608](https://bugreports.qt.io/browse/QTBUG-33608) Elide property of Text breaks component resizing
* [QTBUG-122250](https://bugreports.qt.io/browse/QTBUG-122250) GridView is missing documentation for reuseItems
* [QTBUG-120033](https://bugreports.qt.io/browse/QTBUG-120033) Binding not evaluated
* [QTBUG-123227](https://bugreports.qt.io/browse/QTBUG-123227) Qt Quick Test missing cmake support
* [QTBUG-82311](https://bugreports.qt.io/browse/QTBUG-82311) Crash/Assert rendering text with emoji when style is set
* [QTBUG-119866](https://bugreports.qt.io/browse/QTBUG-119866) TapHandler is used in most of the code snippet of
DragHandler
* [QTBUG-125224](https://bugreports.qt.io/browse/QTBUG-125224) Cannot stop animation if it was restarted before the
last loop completed
* [QTBUG-124456](https://bugreports.qt.io/browse/QTBUG-124456) [6.4.2] Margins in QuickLayouts causing a QList
exception (index out of range)
* [QTBUG-126626](https://bugreports.qt.io/browse/QTBUG-126626) Hovered property stays when popup is opened from drawer
* [QTBUG-124572](https://bugreports.qt.io/browse/QTBUG-124572) Program crash when using a specific glyph from a popular
font file on Linux
* [QTBUG-30768](https://bugreports.qt.io/browse/QTBUG-30768) When an item in a ListView is snapped into place then it
does not take account for the section header
* [QTBUG-124553](https://bugreports.qt.io/browse/QTBUG-124553) [Reg 5.15 -> 6.2] QML Binding is overwritten after
initialization
* [QTBUG-127809](https://bugreports.qt.io/browse/QTBUG-127809) TableView forceLayout does not correct contentX/contentY
after columnWidth/rowHeight changed
* [QTBUG-107143](https://bugreports.qt.io/browse/QTBUG-107143) qmllint ignore RegisterEnumClassesUnscoped
* [QTBUG-123999](https://bugreports.qt.io/browse/QTBUG-123999) Heap buffer overflow in JS Set.delete
* [QTBUG-127628](https://bugreports.qt.io/browse/QTBUG-127628) FAIL!  : tst_QQuickMultiPointTouchArea::inFlickable()
Compared doubles are not the same (fuzzy compare)
* [QTBUG-118024](https://bugreports.qt.io/browse/QTBUG-118024) Still referenced objects are deleted during swap
operation between two ListModel instances

### qttools
* [QTBUG-119429](https://bugreports.qt.io/browse/QTBUG-119429) Top flaky test: tst_lupdate::good on Windows_11_22H2,
Windows_11_23H2, and Windows_10_22H2.
* [PYSIDE-2492](https://bugreports.qt.io/browse/PYSIDE-2492) uic does not generate enumeration name into enum values
causing type checking warnings

### qtdoc
* [QTBUG-122682](https://bugreports.qt.io/browse/QTBUG-122682) "Porting to iOS" documentation only mentions qmake, not
CMake
* [QTBUG-124146](https://bugreports.qt.io/browse/QTBUG-124146) [demos/hangman] Clicking on the vowels button crashes
the demo
* [QTBUG-127547](https://bugreports.qt.io/browse/QTBUG-127547) The link in INTEGRITY doc leads to Qt for wasm doc
* [QTBUG-127926](https://bugreports.qt.io/browse/QTBUG-127926) Outdated Android docs still refer to
QtAndroid::androidActivity()

### qtpositioning
* [QTBUG-119477](https://bugreports.qt.io/browse/QTBUG-119477) SatelliteInfo example crashes

### qtwayland
* [QTBUG-123007](https://bugreports.qt.io/browse/QTBUG-123007) Under Wayland Qt does not correctly handle key modifiers
during key repeating
* [QTBUG-107858](https://bugreports.qt.io/browse/QTBUG-107858) qtwayland caches clipboard content
* [QTBUG-124807](https://bugreports.qt.io/browse/QTBUG-124807) Horizontal scrolling not working under Wayland with
Alt+Wheel
* [QTBUG-124502](https://bugreports.qt.io/browse/QTBUG-124502) Drag and drop operation can crash the compositor

### qtwebengine
* [QTBUG-108843](https://bugreports.qt.io/browse/QTBUG-108843) [WebRTC] Crash inside
RTCStatsCollector::ProduceAudioRTPStreamStats_n
* [QTBUG-112522](https://bugreports.qt.io/browse/QTBUG-112522) Webengine Widgets Client Certificate Example:
Compilation Fails
* [QTBUG-111894](https://bugreports.qt.io/browse/QTBUG-111894) [REG 6.4.3->6.4.2] webenginequick/quicknanobrowser not
launching
* [QTBUG-112661](https://bugreports.qt.io/browse/QTBUG-112661) WebEngine Quick Nano Browser Example: Crashes
* [QTBUG-114883](https://bugreports.qt.io/browse/QTBUG-114883) [REG 6.2.8 -> 6.2.9] shadow build fails on windows,
webengine
* [QTBUG-122655](https://bugreports.qt.io/browse/QTBUG-122655) 6.8.0 toplevel build fails on macOS, qtwebengine

### qtnetworkauth
* [QTBUG-124333](https://bugreports.qt.io/browse/QTBUG-124333) [OAuth] Ability to open and close the loopback HTTP
server on a need-basis

### qtremoteobjects
* [QTBUG-139754](https://bugreports.qt.io/browse/QTBUG-139754) FAIL!  : tst_clientSSL::testRun()
'socketClient->waitForEncrypted(-1)' returned FALSE

Known Issues
------------

* Check that your system meets Qt's requirements:
https://doc.qt.io/qt-6.2/supported-platforms.html

* The RTA (release test automation) reported issues in Qt 6.2.x:
https://bugreports.qt.io/issues/?filter=23315

* Qt 6.2.13 Open issues in Jira:
https://bugreports.qt.io/issues/?filter=26436

Credits for the  release goes to:
---------------------------------

Eirik Aavitsland  
Laszlo Agocs  
Mate Barany  
Vladimir Belyavsky  
Nicholas Bennett  
Eskil Abrahamsen Blomfeldt  
Michael Brüning  
Olivier De Cannière  
Alexei Cazacov  
Mike Chen  
Albert Astals Cid  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Oliver Dawes  
Artem Dyomin  
Alexey Edelev  
Christian Ehrlicher  
Hatem ElKharashy  
Andreas Eliasson  
David Faure  
Richard Moe Gustavsen  
Ulf Hermann  
Volker Hilsheimer  
Marc Hüskens  
Ahmed El Khazari  
Friedemann Kleint  
Michal Klocek  
Jarek Kobus  
Fabian Kosmale  
Jaroslaw Kubik  
Santhosh Kumar  
Kai Köhne  
Inho Lee  
Chris Lerner  
Thiago Macieira  
Marc Mutz  
Antti Määttä  
Mårten Nordheim  
Timur Pocheptsov  
Rami Potinkara  
Shyamnath Premnadh  
Liang Qi  
Shawn Rutledge  
Ahmad Samir  
Andy Shaw  
Pierre-Yves Siret  
Ivan Solovev  
Axel Spoerl  
Martin Storsjö  
Tarja Sundqvist  
Jan Arve Sæther  
Doris Verria  
Tor Arne Vestbø  
Juha Vuolle  
Edward Welbourne  
Vlad Zahorodnii  
Liu Zheng  
