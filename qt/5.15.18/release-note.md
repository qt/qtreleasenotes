Release note
============
Qt 5.15.18 release is a patch release made on the top of Qt 5.15.17. As a patch  
release, Qt 5.15.18 does not add any new functionality but provides bug fixes  
and other improvements.  
  
For detailed information about Qt, see the Qt 5.15 online documentation:  
https://doc.qt.io/qt-5/index.html. 

Important Changes
-----------------

### Security fixes

*  CVE-2024-39936 in qtbase

### qtbase
* 89d9b0b5c86 SQLite: Update SQLite to v3.45.3
Updated SQLite to v3.45.3

* b4eb2e4d792 QBitArray: avoid overflow in size-to-storage calculations
Fixed a bug with QBitArrays whose size() came within 7 of the
size_type's maximum.

* 3a83362b6cf QBitArray: fix potential truncation in QDataStream op>>()
Fixed undetected overflows in the deserialisation (opertor>>()) from
QDataStream.

* 2d567667423 Update bundled libjpeg-turbo to version 3.0.3
libjpeg-turbo was updated to version 3.0.3

* 158d77c6835 Update public suffix list
Updated the public suffix list to upstream SHA
903a83ff7bfc3148e3692e09396f9f3bdc9462ef.

* d740e998748 Change the mimetype database embedded into QtCore
For licensing reasons, QtCore no longer ships a copy of the MIME
database from freedesktop.org's shared-mime-info project, but the one
from the Apache Tika project. The tika definitions don't have icons or
translated descriptions, but are sufficient for matching file types.

* 338879f7658 QMimeDatabase: pick up XML mimetypes from :/qt-
project.org/mime/packages
QMimeDatabase can now pick up XML mimetype definitions from :/qt-
project.org/mime/packages. GPL-compatible projects which provide self-
contained binaries can use this to provide a copy of freedesktop.org.xml
that will be used instead of the TIKA mimetypes.

* a9240644fec PCRE: upgrade to 10.44
PCRE2 was updated to version 10.44.

* a5a68b29e8e macOS: Be honest about the system locale
QLocale::system() on macOS no longer pretends to support LANG or other
environment variables as overrides, as this is not a feature that the
system locale on macOS supports. To override the locale of an
application, use QLocale::setDefault(), or pass -AppleLocale en_US.

* eae7ff5c23f Add __attribute__((format(printf()))) to q(v)nprintf()
Added attributes for GCC-compatible compilers to detect format/argument
mismatches. If this throws warnings for your calls now, don't ignore
them. printf() format mistakes could be security-relevant. You may also
find that you relied on undocumented behavior, such as that certain
implementations (Windows, Android, WASM) of qsnprintf() support
char16_t* instead of wchar_t* for %ls. In that case, you should port to
qUtf16Printable() and QString::asprintf(), or suppress the warning and
port away from the platform dependence at your earliest convenience.

* a11b6c03edc SQLite: Update identified license
Change identified license for SQLite from 'Public Domain' to more
accurate 'SQLite Blessing': https://spdx.org/licenses/blessing.html

* c8ab6bcce17 SQLite: Update SQLite to v3.46.0
Updated SQLite to v3.46.0

* b04c103f4f4 SQLite: Update SQLite to v3.46.1
Updated SQLite to v3.46.1

* d1d57fc6cfd Update Freetype to 2.13.3
Updated bundled Freetype to version 2.13.3.

* 12b9b83fe95 Update to Harfbuzz 9.0.0
Updated Harfbuzz to 9.0.0.

* fae00c52f9a Update bundled libjpeg-turbo to version 3.0.4
libjpeg-turbo was updated to version 3.0.4

* 62bccfc81df Update bundled libpng to version 1.6.44
libpng was updated to version 1.6.44

* 3e7fd13b074 Update to Harfbuzz 10.0.1
Updated Harfbuzz to 10.0.1.

### qtconnectivity
* 071e67f4 sdpscanner: fix format strings for (u)int64_t
Fixed a bug involving broken serialization of SDP_(U)INT64 DTDs on Big-
Endian machines.

### qtimageformats
* 24c36ed Update bundled libwebp to version 1.4.0
Update bundled libwebp to version 1.4.0

* fa0105b Update bundled libtiff to version 4.7.0
Bundled libtiff was updated to version 4.7.0


Fixes
-----

### qtbase
* [QTBUG-111960](https://bugreports.qt.io/browse/QTBUG-111960) NPE: Attempt to invoke virtual method
setActivityDisplayRotation() on a null object reference
* [QTBUG-124179](https://bugreports.qt.io/browse/QTBUG-124179) Configure script not respecting specified c++ standard
* [QTBUG-125531](https://bugreports.qt.io/browse/QTBUG-125531) Unable to drag files into the xwayland widget of
QTextEdit
* [QTBUG-119167](https://bugreports.qt.io/browse/QTBUG-119167) Atspi.Table.get_row_column_extents_at_index can cause
segfault in tree
* [QTBUG-125954](https://bugreports.qt.io/browse/QTBUG-125954) Segfault in QAccessibleTableInterface::cellAt
* [QTBUG-125762](https://bugreports.qt.io/browse/QTBUG-125762) Malayalam Font Rendering Issue
* [QTBUG-126530](https://bugreports.qt.io/browse/QTBUG-126530) Qt app memory keeps growing with accessibility enabled
* [QTBUG-123554](https://bugreports.qt.io/browse/QTBUG-123554) xcb: Enabling touch device while application is running
causes a crash on first touch
* [QTBUG-127179](https://bugreports.qt.io/browse/QTBUG-127179) Qt Creator puts wrong fields for spacer objects
* [PYSIDE-2492](https://bugreports.qt.io/browse/PYSIDE-2492) uic does not generate enumeration name into enum values
causing type checking warnings
* [QTBUG-127055](https://bugreports.qt.io/browse/QTBUG-127055) QThread::terminate() ABA problem
* [QTBUG-122202](https://bugreports.qt.io/browse/QTBUG-122202) QLocale::uiLanguages() returns english language if run
from Finder
* [QTBUG-90971](https://bugreports.qt.io/browse/QTBUG-90971) macOS system locale isn't consistent with itself
* [QTBUG-124310](https://bugreports.qt.io/browse/QTBUG-124310) QT_DISTANCEFIELD_DEFAULT_BASEFONTSIZE=128 causes a
QDistanceField crash
* [QTBUG-128214](https://bugreports.qt.io/browse/QTBUG-128214) Building for android 34 fails with errors about ministro
* [QTBUG-113865](https://bugreports.qt.io/browse/QTBUG-113865) [Text Editor]Using undo function causes the app to crash
* [QTBUG-122973](https://bugreports.qt.io/browse/QTBUG-122973) QDateTime::operator== documentation is wrong
* [QTBUG-110841](https://bugreports.qt.io/browse/QTBUG-110841)  [REG: 5.10.1->5.11.0-alpha] Mouse events not observed
when Super (Windows) key is held down.
* [QTBUG-117500](https://bugreports.qt.io/browse/QTBUG-117500) Sporadic crash on  QFontEngineMulti::ensureEngineAt()
* [QTBUG-123158](https://bugreports.qt.io/browse/QTBUG-123158) Font rendering uses glyph metrics wrong
* [QTBUG-109367](https://bugreports.qt.io/browse/QTBUG-109367) Android native ExtractEditText does not receive text
updates from qml TextEdit in fullscreen mode and landscape orientation
* [QTBUG-82311](https://bugreports.qt.io/browse/QTBUG-82311) Crash/Assert rendering text with emoji when style is set
* [QTBUG-124572](https://bugreports.qt.io/browse/QTBUG-124572) Program crash when using a specific glyph from a popular
font file on Linux
* [QTBUG-127110](https://bugreports.qt.io/browse/QTBUG-127110) Platforms still use the inefficient qvsnprintf() fall-
back
* [QTBUG-91077](https://bugreports.qt.io/browse/QTBUG-91077) startSystemMove/startSystemResize causing mouse events to
be lost on X11(MATE)
* [QTBUG-104867](https://bugreports.qt.io/browse/QTBUG-104867) QtTest: QCOMPARE prints matching <null>s for mismatches
when unable to convert to string
* [QTBUG-118877](https://bugreports.qt.io/browse/QTBUG-118877) -qreal float configuration option does not compile
* [QTBUG-115158](https://bugreports.qt.io/browse/QTBUG-115158) Time zone names and abbreviations are not localised

### qtdeclarative
* [QTBUG-123596](https://bugreports.qt.io/browse/QTBUG-123596) Crash JS for x in o  { delete o[x] } if o is a
sparsearray
* [QTBUG-122250](https://bugreports.qt.io/browse/QTBUG-122250) GridView is missing documentation for reuseItems
* [QTBUG-125895](https://bugreports.qt.io/browse/QTBUG-125895) Broken compatibility with compilers that do not support
std::make_unique
* [QTBUG-125224](https://bugreports.qt.io/browse/QTBUG-125224) Cannot stop animation if it was restarted before the
last loop completed
* [QTBUG-124572](https://bugreports.qt.io/browse/QTBUG-124572) Program crash when using a specific glyph from a popular
font file on Linux
* [QTBUG-123999](https://bugreports.qt.io/browse/QTBUG-123999) Heap buffer overflow in JS Set.delete
* [QTBUG-118024](https://bugreports.qt.io/browse/QTBUG-118024) Still referenced objects are deleted during swap
operation between two ListModel instances

### qtmultimedia
* [QTBUG-125601](https://bugreports.qt.io/browse/QTBUG-125601) SoundEffect does not play if trying to play again right
after it ends
* [QTBUG-120647](https://bugreports.qt.io/browse/QTBUG-120647) QImage::convertToFormat gives wrong result on iOS when
linking QtMultimedia

### qttools
* [QTBUG-124200](https://bugreports.qt.io/browse/QTBUG-124200) Linguist 'does not know the plural rules for Luganda'
* [QTBUG-128840](https://bugreports.qt.io/browse/QTBUG-128840) License information for Android Billing API incomplete /
not rendering
* [PYSIDE-2492](https://bugreports.qt.io/browse/PYSIDE-2492) uic does not generate enumeration name into enum values
causing type checking warnings

### qtdoc
* [QTBUG-124585](https://bugreports.qt.io/browse/QTBUG-124585) Compiler is missing for Windows 11 22H2

### qtwayland
* [QTBUG-124807](https://bugreports.qt.io/browse/QTBUG-124807) Horizontal scrolling not working under Wayland with
Alt+Wheel
* [QTBUG-124502](https://bugreports.qt.io/browse/QTBUG-124502) Drag and drop operation can crash the compositor

### qtandroidextras
* [QTBUG-86203](https://bugreports.qt.io/browse/QTBUG-86203) Documentation on QtAndroid:androidService(),
QtAndroid:androidContext() unclear

### qtquickcontrols2
* [QTBUG-102487](https://bugreports.qt.io/browse/QTBUG-102487) [REG 5.15.8 -> 5.15.9 + 6.2.3 -> 6.3.0] SwipeView shows
last page on first page
* [QTBUG-51078](https://bugreports.qt.io/browse/QTBUG-51078) Use of Item obligatory in SwipeView?
* [QTBUG-51669](https://bugreports.qt.io/browse/QTBUG-51669) QQC2: SwipeView is not working as expected
* [QTBUG-99547](https://bugreports.qt.io/browse/QTBUG-99547) PathView item does not appear in certain circumstance

Known Issues
------------

 * Check that your system meets Qt's requirements:
https://doc.qt.io/qt-5.15/supported-platforms.html

* The RTA (release test automation) reported issues in Qt 5.15.x:
https://qt-project.atlassian.net/issues/?filter=14473

* Qt 5.15.18 Open issues in Jira:
https://qt-project.atlassian.net/issues/?filter=10306

Credits for the  release goes to:
---------------------------------

Eirik Aavitsland  
Vladimir Belyavsky  
Nicholas Bennett  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
Joerg Bornemann  
Assam Boudjelthia  
Albert Astals Cid  
Alexandru Croitor  
Giuseppe D'Angelo  
Oliver Dawes  
Christian Ehrlicher  
Hatem ElKharashy  
Andreas Eliasson  
David Faure  
Nazar Gerasymchuk  
Jøger Hansegård  
Ulf Hermann  
Volker Hilsheimer  
Ahmed El Khazari  
Friedemann Kleint  
Jarek Kobus  
Fabian Kosmale  
Santhosh Kumar  
Kai Köhne  
Inho Lee  
Marc Mutz  
Antti Määttä  
Mårten Nordheim  
Frank Osterfeld  
Joni Poikelin  
Rami Potinkara  
Liang Qi  
Topi Reinio  
Shawn Rutledge  
Ahmad Samir  
Pierre-Yves Siret  
Tarja Sundqvist  
Tor Arne Vestbø  
Dongmei Wang  
Edward Welbourne  
Oliver Wolff  
Liu Zheng  
