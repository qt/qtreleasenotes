Release note
============
  
Qt 5.15.16 release is a patch release made on the top of Qt 5.15.15. As a patch  
release, Qt 5.15.16 does not add any new functionality but provides bug fixes  
and other improvements.  
  
For detailed information about Qt, see the Qt 5.15 online documentation:  
https://doc.qt.io/qt-5/index.html.    

Important Changes
-----------------
  
### Security fixes  
  
*  CVE-2023-43114 in qtbase  
  
### qtbase

* 602bd58 Update Harfbuzz to 8.2.2  
Update Harfbuzz to version 8.2.2  

* 6b92ef96e96 Update Harfbuzz to 7.2.0
The included version of the text shaping library Harfbuzz has been
disabled on a selection of older platforms where the updated versions do
not compile. There may be regressions in text appearance with certain
fonts when rendering languages that depend on OpenType features due to
this. A possible mitigation is to build an older Harfbuzz version
manually and use -system-harfbuzz to use this with Qt. This affects the
following platforms: QNX, Integrity, WinRT, Intel ICC compiler, MacOS
10.15 and lower, MSVC 2015 and lower.

* a9607e7c1dc SQLite: Update SQLite to v3.43.0
Updated SQLite to v3.43.0

* 683b422ac8e Update bundled zlib to version 1.3
zlib was updated to version 1.3.

* b455c20d762 Fix crash when reading corrupt font data
Fixed a possible crash that could happen when loading corrupted font
data.

* 579e5474cd6 SQLite: Update SQLite to v3.43.1
Updated SQLite to v3.43.1

* 03cf5f24f64 Un-deprecate qSwap()
Un-deprecated qSwap().

* 4dc3ccc297a SQLite: Update SQLite to v3.43.2
Updated SQLite to v3.43.2

* 2b00e5a82b3 Update bundled libjpeg-turbo to version 3.0.1
libjpeg-turbo was updated to version 3.0.1

### qtconnectivity
* fe2dee18 QBluetoothUuid: remove default case labels and fix the
fallout
Fixed missing result of
characteristicToString(CharacteristicType::WeightScaleFeature).

### qtimageformats
* 56b3633 Update bundled libtiff to version 4.5.1
Bundled libtiff was updated to version 4.5.1

* 2dd4c7a Update bundled libwebp to version 1.3.1
Update bundled libwebp to version 1.3.1

* 426b918 Update bundled libtiff to version 4.6.0
Bundled libtiff was updated to version 4.6.0

* f2a126d Update bundled libwebp to version 1.3.2
Update bundled libwebp to version 1.3.2


Fixes
-----

### qtbase
* QTBUG-114435 Regression 5.15.14: Cannot open Files from Android
FileDialog with spaces or umlauts
* QTBUG-116166 Network tests fail with OpenSSL 3.1.1
* QTBUG-116517 Zero-width space in qaccessiblewidgets.cpp causing
compilation error
* QTBUG-116696 Menus have window type _NET_WM_WINDOW_TYPE_NORMAL instead
of _NET_WM_WINDOW_TYPE_POPUP_MENU
* QTBUG-39887 Regression bug: QWidget::setAttribute() does not set
Qt::WA_X11NetWmWindowType in Qt 5.
* QTBUG-116715 docs: qsettings path on embdded linux
* QTBUG-3287 Reads a '\0'-terminated string from the QDataStream
* QTBUG-93858 Some XKB letter keysyms are not properly converted to
corresponding Qt keys
* QTBUG-116773 Adding "Fuzzed" .otf font files causes access violation
exception
* QTBUG-107598 HorizontalHeaderView crashes the app if it's synced to
model changed from bg thread
* QTBUG-117950 qxkbcommon.cpp:242:16: error: 'XKB_KEY_dead_lowline' was
not declared in this scope
* QTBUG-118150 Sporadic Crash in QXkbCommon::lookupLatinKeysym, when
Events with Control-Modifiers are sent
* QTBUG-117804 Incomplete JPEG writing after libjpeg-turbo 3.0.0 upgrade
* QTBUG-93763 Systematic announcement of combobox selected element
* QTBUG-116085 QXmlSimpleReader truncates character references of non-
BMP characters
* QTBUG-114613 QWindow::winId() crashes when QWindowPrivate::create()
fails
* QTBUG-80315 MouseArea: Press and hold with stylus warn and doesn't
call pressAndHold
* QTBUG-91545 [iOS] Selection in TextEdit not working for Readonly text
* QTBUG-111514 QtCore fails to link with lld 16.0

### qtdeclarative
* QTBUG-105090 tst_QQuickMenu AddressSanitizer: heap-use-after-free in
QQmlData::signalHasEndpoint(int)
* QTBUG-96700 Strikethrough formatting changes to underline.
* QTBUG-97594 Mac - Strikeout bugged in QML TextEdit for Japanese
* QTBUG-86255 Crash with asynchronous Loader in GridView
* QTBUG-105000 [REG: 5.15.2->5.15.10] State.when does not work for
objects anymore
* QTBUG-100560 Crash when closing SwipeDelegate in onCompleted handler
* QTBUG-115319 Issue with number as a context property name
* QTBUG-117018 Qt 5.15.15 jsruntime/qv4sequenceobject.cpp fails to build
in Debian 12 (bookworm) with GCC 12.2
* QTBUG-110114 Qt Quick Controls Button: Unable to override
Accessible.role
* QTBUG-84858 [REG 5.14->5.15] crash on close in QQuickItemLayer
destructor on Linux
* QTBUG-117479 Segmentation fault in qml debugger

### qtactiveqt
* QTBUG-100657 Crash while receiving COM IDispatch events when
initializing
* QTBUG-96871 Crash on calling connect on   QAxObject source instance

### qtmultimedia
* QTBUG-82697 QML CameraCapture supportedResolutions contains duplicates

### qttools
* QTBUG-115465 Designer injects bogus "<normaloff>.</normaloff>." for
icon properties

### qtdoc
* QTBUG-116489 tutorials/alarms not compiling

### qtlocation
* QTBUG-116645 [Android] providerList() returns NULL list

### qtwayland
* QTBUG-115757 [REG: 6.5.1-6.5.2] Drag and Drop segfaults programs
* QTBUG-97037 DragHandler / startSystemMove window move issue with QT6
Webengine on Wayland
* QTBUG-112161 Drag and drop with wayland display error

### qt3d
* QTBUG-116494 Documentation for QCylinderMesh misses Detailed
Description

### qtquickcontrols2
* QTBUG-108610 HorizontalHeaderView & VerticalHeaderView does not
disconnect from QQmlTableModel::headerDataChanged and can crash app
* QTBUG-94455 tst_QQuickFileDialogImpl::defaults() leaks memory

### qtvirtualkeyboard
* QTBUG-118758 [VKB] Switching style at runtime causes keys to go blank

### qtopcua
* QTBUG-104418 tst_opcua:AbsoluteNodeTest is flaky on Mac

Known Issues
------------
  
 * Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-5.15/supported-platforms.html  
  
* The RTA (release test automation) reported issues in Qt 5.15.x:  
https://bugreports.qt.io/issues/?filter=21874  
  
* Qt 5.15.15 Open issues in Jira:  
https://bugreports.qt.io/issues/?filter=25360  
  
Credits for the  release goes to:
---------------------------------

Eirik Aavitsland
Vladimir Belyavsky
Eskil Abrahamsen Blomfeldt
Joerg Bornemann
Assam Boudjelthia
Kai Uwe Broulik
Andrey Butirsky
Albert Astals Cid
Mitch Curtis
David Edmundson
Christian Ehrlicher
Andreas Eliasson
Richard Moe Gustavsen
Jani Heikkinen
Ulf Hermann
Volker Hilsheimer
Jukka Jokiniva
Friedemann Kleint
Michal Klocek
Lars Knoll
Sze Howe Koh
Jarkko Koivikko
Fabian Kosmale
Kai Köhne
Wladimir Leuschner
Marc Mutz
Mårten Nordheim
Dennis Oberst
Timur Pocheptsov
Joni Poikelin
MohammadHossein Qanbari
Liang Qi
Topi Reinio
Ahmad Samir
Nick Shaforostov
Andy Shaw
Ivan Solovev
Tarja Sundqvist
Tarja Sundvist
Jan Arve Sæther
Tor Arne Vestbø
Alexander Volkov
Edward Welbourne
