Release note
============
Qt 5.15.19 release is a patch release made on the top of Qt 5.15.18. As a patch  
release, Qt 5.15.19 does not add any new functionality but provides bug fixes  
and other improvements.  
  
For detailed information about Qt, see the Qt 5.15 online documentation:  
https://doc.qt.io/qt-5/index.html. 

Important Changes
-----------------

### Security fixes

* CVE-2024-38081 in qtbase
* CVE-2025-30348 in qtbase
* CVE-2025-23050 in qtconnectivity

### qtbase
* 0ae1c77a5b4 Update to Harfbuzz 10.0.1
Updated Harfbuzz to 10.0.1.

* 9eb4f32dc2f Upgrade to Harfbuzz 10.1.0
Upgraded Harfbuzz to version 10.1.0.

* de0d2a36fd4 SQLite: Update SQLite to v3.47.1
Updated SQLite to v3.47.1

* 02c25108ff9 QCupsPrintEngine::setProperty(): defend against malformed
PPK_CupsOptions values
Fixed a bug where setting a value string-list with an odd number of
elements as the PPK_CupsOptions value would read uninitialized data.

* e74b1a7c73f Update bundled libjpeg-turbo to version 3.1.0
libjpeg-turbo was updated to version 3.1.0

* 4e1a36c1c71 Update bundled libpng to version 1.6.45
libpng was updated to version 1.6.45

* 6506f3c0843 Update public suffix list
Updated the public suffix list to upstream SHA
47264b57765919188b9f4144de8d95cf77e1b6dc.

* 8d6fc55d658 Update Harfbuzz to version 10.2.0
Upgraded Harfbuzz to version 10.2.0.

* bfb2f4bd80f Update bundled libpng to version 1.6.47
libpng was updated to version 1.6.47

* 84b21c42b88 Update Harfbuzz to version 10.3.0
Upgraded Harfbuzz to version 10.3.0.

* c3005aceaf0 QLocale: fix UB (signed overflow) in formattedDataSize()
Fix issue when calling formattedDataSize() with
numeric_limits<qint64>::min().

* 6b9f815b209 Upgrade Harfbuzz to 10.4.0
Upgraded Harfbuzz to version 10.4.0.

* 3d20cd0105c QFileSystemEngine/Win: Use GetTempPath2 when available
On Windows, generating temporary directories for processes with
elevated privileges may now return a different path with a stricter set
of permissions. Please consult Microsoft's documentation from when they
made the same change for the .NET framework:
https://support.microsoft.com/en-us/topic/gettemppath-changes-in-
windows-february-cumulative-update-
preview-4cc631fb-9d97-4118-ab6d-f643cd0a7259

* ef73b27b698 SQLite: Update SQLite to v3.47.2
Updated SQLite to v3.47.2

* f84274b2e41 SQLite: Update SQLite to v3.48.0
Updated SQLite to v3.48.0

* 129e9efab5e SQLite: Update SQLite to v3.49.0
Updated SQLite to v3.49.0

* c7df5bc7088 SQLite: Update SQLite to v3.49.1
Updated SQLite to v3.49.1

* ec91b8eac62 QAbstractSlider: fix missing "emission" of
SliderOrientationChange
Fixed the missing "emission" of protected
sliderChange(SliderOrientationChange).

* 204d4835f73 Long live qstdlibdetection.h!
Added Q_STL_ macros for stdlib detection (libc++, libstdc++, MSSTL,
Dinkumware, STLport, SGI, RogueWave). If your STL is lacking, please
file a bug report. Note that these macros are not considered public API
just yet.

* 4d1fe707e5e 3rdparty: update TinyCBOR to v0.6.1
The copy of TinyCBOR in Qt was updated to 0.6.1.

* 6c63f3fb188 Upgrade Harfbuzz to 11.0.0
Upgraded Harfbuzz to version 11.0.0.

* 92f6b2d685e Update PCRE2 to 10.45
PCRE2 was updated to version 10.45.

* 40b8b3aee78 Upgrade Harfbuzz to 11.1.0
Upgraded Harfbuzz to version 11.1.0.

* da38b58a336 QByteArray(View)::lastIndexOf: Guard against needle >
haystack
Fixed a bug in lastIndexOf() that could lead to out-of-bounds access
when the needle is longer than the haystack.

* 90956fa1ef1 qDecodeDataUrl(): fix precondition violation in call to
QByteArrayView::at()
Fixed a bug in the handling of data: URLs that could lead to a crash if
Qt was built with assertions enabled. This affects QNetworkManager and
links in QTextDocument.

### qtimageformats
* df662c7f Update bundled libwebp to version 1.5.0
Update bundled libwebp to version 1.5.0


Fixes
-----

### qtbase
* [QTBUG-130150](https://qt-project.atlassian.net/browse/QTBUG-130150) QTBUG-85172 is marked as fixed, but seems to have been
reverted as it still doesn't show in Qt 5.15
* [QTBUG-85172](https://qt-project.atlassian.net/browse/QTBUG-85172) QOCI: update documentation to state building plugin
requires at least Oracle Instant Client SDK v12.1
* [QTBUG-116511](https://qt-project.atlassian.net/browse/QTBUG-116511) Android 11 and above setNativeLocks failed: "Function
not implemented"
* [QTBUG-129509](https://qt-project.atlassian.net/browse/QTBUG-129509) (Regression) Erratic scrolling behavior using the mouse
in 6.7.3
* [QTBUG-129514](https://qt-project.atlassian.net/browse/QTBUG-129514) Reversed mouse buttons don't work properly on 6.7.3
* [QTBUG-110841](https://qt-project.atlassian.net/browse/QTBUG-110841)  [REG: 5.10.1->5.11.0-alpha] Mouse events not observed
when Super (Windows) key is held down.
* [QTBUG-21329](https://qt-project.atlassian.net/browse/QTBUG-21329) QTransform::quadToQuad() doesn't work, when passed
QRectFs
* [QTBUG-128906](https://qt-project.atlassian.net/browse/QTBUG-128906) Konsole crashes with SIGSEGV
* [QTBUG-132597](https://qt-project.atlassian.net/browse/QTBUG-132597) Incorrect description of QTemporaryFile behavior when
two placeholders are present
* [QTBUG-132314](https://qt-project.atlassian.net/browse/QTBUG-132314) GPU driver crash in iOS 18
* [QTBUG-133269](https://qt-project.atlassian.net/browse/QTBUG-133269) QTextStream: suspicious negation when streaming numbers
* [QTBUG-127549](https://qt-project.atlassian.net/browse/QTBUG-127549) QDomNode::save() takes huge amount of time. 10x worse
performance when compared to Qt 5
* [QTBUG-127517](https://qt-project.atlassian.net/browse/QTBUG-127517) Reports of misaligned loads with asan on AArch64 / xcb
* [QTBUG-88721](https://qt-project.atlassian.net/browse/QTBUG-88721) QTextDocument::find() does not work well with
QRegularExpressions
* [QTBUG-52292](https://qt-project.atlassian.net/browse/QTBUG-52292) Pantheon desktop is not recognized as Gtk desktop
* [QTBUG-135471](https://qt-project.atlassian.net/browse/QTBUG-135471) tst_QXmlStream does not test non-wellformed documents
properly
* [QTBUG-96276](https://qt-project.atlassian.net/browse/QTBUG-96276) _NET_STARTUP_ID not supported
* [QTBUG-135076](https://qt-project.atlassian.net/browse/QTBUG-135076) [QNX] Stale QNX Screen events under load
* [QTBUG-105150](https://qt-project.atlassian.net/browse/QTBUG-105150) QStandardItem is using un-documented value of
Qt::ItemDataRole
* [QTBUG-135597](https://qt-project.atlassian.net/browse/QTBUG-135597) QAbstractSlider is not using SliderOrientationChange
* [QTBUG-118231](https://qt-project.atlassian.net/browse/QTBUG-118231) Android app 'pause' or 'screen-off' causes
'eglSwapBuffers failed' and various logcat errors
* [QTBUG-112746](https://qt-project.atlassian.net/browse/QTBUG-112746) QAnyStringView missing implicit conversion from char[]
with unknown size
* [QTBUG-130613](https://qt-project.atlassian.net/browse/QTBUG-130613) Documentation of Q_GLOBAL_STATIC(MyType, staticType) is
confusing
* [QTBUG-132646](https://qt-project.atlassian.net/browse/QTBUG-132646) Add a variant of QTemporaryFile::rename() that
overwrites
* [QTBUG-132831](https://qt-project.atlassian.net/browse/QTBUG-132831) QSet::remove() unconditionally detaches
* [QTBUG-132500](https://qt-project.atlassian.net/browse/QTBUG-132500) [REG 6.7 -> 6.8] QSet::unite() no longer consistently
picks equivalent elements from `other`
* [QTBUG-132536](https://qt-project.atlassian.net/browse/QTBUG-132536) QSet::intersect() picks equivalent elements
inconsistently  from `other` or *this
* [QTBUG-83817](https://qt-project.atlassian.net/browse/QTBUG-83817) potential out-of-bounds access in qcssparser
* [QTBUG-134557](https://qt-project.atlassian.net/browse/QTBUG-134557) QOpenGLFramebufferObject seems to leak
QOpenGLSharedResourceGuards
* [QTBUG-98988](https://qt-project.atlassian.net/browse/QTBUG-98988) Qt bugs when portal implementation is not available
* [QTBUG-122704](https://qt-project.atlassian.net/browse/QTBUG-122704) QPainterPath de-serialisation from QDataStream fails if
item isn't empty
* [QTBUG-104840](https://qt-project.atlassian.net/browse/QTBUG-104840) heap-use-after-free in QTest::ignoreMessage
* [QTBUG-135962](https://qt-project.atlassian.net/browse/QTBUG-135962) Configure failure with lttng enabled

### qtdeclarative
* [QTBUG-114984](https://qt-project.atlassian.net/browse/QTBUG-114984) Software Renderer: Updating a layer-enabled subtree
while it is invisible produces wrong outcomes
* [QTBUG-134664](https://qt-project.atlassian.net/browse/QTBUG-134664) FAIL!  :
tst_examples::examples(examples/quick/multieffect/testbed/qml/main.qml)
Received a fatal error
* [QTBUG-135387](https://qt-project.atlassian.net/browse/QTBUG-135387) Division by zero when changing path elements of
ShapePath imperatively
* [QTBUG-102862](https://qt-project.atlassian.net/browse/QTBUG-102862) Build failure with lttng enabled

### qtdoc
* [QTBUG-127830](https://qt-project.atlassian.net/browse/QTBUG-127830) Android API 34 and higer does not works with Qt5

### qtserialport
* [QTBUG-109455](https://qt-project.atlassian.net/browse/QTBUG-109455) read() returns qint64 not int
* [QTBUG-120221](https://qt-project.atlassian.net/browse/QTBUG-120221) clang-tidy, and probably clang complains about dllimport
vs. inline in qtserialportinfo.h
* [QTBUG-105561](https://qt-project.atlassian.net/browse/QTBUG-105561) QSerialPort Mark/Space Emulation causes recursion and
crash
* [QTBUG-131679](https://qt-project.atlassian.net/browse/QTBUG-131679) QSerialPort does not have Mark/Space parity emulation
for reading the data
* [QTBUG-67544](https://qt-project.atlassian.net/browse/QTBUG-67544) QSerialPort emits errorOccurred with NoError

### qtwebengine
* [QTBUG-130631](https://qt-project.atlassian.net/browse/QTBUG-130631) Windows: Python 2 function "has_key" fails in lts-5.15
while removing Python 2
* [QTBUG-131693](https://qt-project.atlassian.net/browse/QTBUG-131693) Windows: Unguarded uses of Python 2 attribute time.clock
used in lts-5.15, build fails while removing Python 2
* CVE-2025-0436: Integer overflow in Skia
* CVE-2025-0762: Use after free in DevTools
* CVE-2025-0996: Inappropriate implementation in Browser UI
* CVE-2025-0999: Heap buffer overflow in V8
* CVE-2025-1426: Heap buffer overflow in GPU
* CVE-2025-1919
* CVE-2025-2136
* CVE-2025-2783: Incorrect handle provided in unspecified circumstances in Mojo on Windows
* CVE-2025-3619
* CVE-2024-10827: Use after free in Serial
* CVE-2024-11477
* CVE-2024-12694: Use after free in Compositing
* CVE-2025-24201
* CVE-2025-24855 Fix use-after-free of XPath context node
* CVE-2024-55549: Fix UAF related to excluded namespaces
* Security bug 378701682
* Security bug 383772517
* Security bug 382135228
* Security bug 384565015
* Security bug 396460489
* Security bug 396481096
* Security bug 399002829

### qtpurchasing
* [QTBUG-128265](https://qt-project.atlassian.net/browse/QTBUG-128265) QtHangman example build fails in Qt 5.15.18 for Android

### qtnetworkauth
* [QTBUG-135257](https://qt-project.atlassian.net/browse/QTBUG-135257) NetworkAuth Coverity findings

### qtremoteobjects
* [QTBUG-129923](https://qt-project.atlassian.net/browse/QTBUG-129923) 5.15: QtRemoteObject listener count keeps increasing at
server side.

### qtquicktimeline
* [QTBUG-122812](https://qt-project.atlassian.net/browse/QTBUG-122812) Binding is not restored for Timeline component

### qtquick3d
* [QTBUG-125963](https://qt-project.atlassian.net/browse/QTBUG-125963) application crash when using View3d in singleton and
apply effects to View3d

Known Issues
------------

 * Check that your system meets Qt's requirements:
https://doc.qt.io/qt-5.15/supported-platforms.html

* The RTA (release test automation) reported issues in Qt 5.15.x:
https://qt-project.atlassian.net/issues/?filter=14473

* Qt 5.15.19 Open issues in Jira:
https://qt-project.atlassian.net/issues/?filter=10547

Credits for the  release goes to:
---------------------------------

Eirik Aavitsland  
Nicholas Bennett  
Eskil Abrahamsen Blomfeldt  
Kai Uwe Broulik  
Michael Brüning  
Alexei Cazacov  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Christian Ehrlicher  
Lionel Fafchamps  
David Faure  
Ilya Fedin  
Ulf Hermann  
Samuli Hölttä  
Jonas Karlsson  
Ahmed El Khazari  
André Klitzing  
Michal Klocek  
Sona Kurazyan  
Inho Lee  
Thiago Macieira  
Bartlomiej Moskal  
Marc Mutz  
Andy Nichols  
Mårten Nordheim  
Tinja Paavoseppä  
Pasi Petäjäjärvi  
Liang Qi  
Johannes Rosenqvist  
Shawn Rutledge  
Ahmad Samir  
Dmitry Shachnev  
Andy Shaw  
Ivan Solovev  
Christian Strømme  
Tarja Sundqvist  
Duan Ting  
Tuomas Vaarala  
Tor Arne Vestbø  
Juha Vuolle  
Edward Welbourne  
Milian Wolff  
Lu YaNing  
