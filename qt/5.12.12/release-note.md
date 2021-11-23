Release note  
============  
Qt 5.12.12 release is a patch release made on the top of Qt 5.12.11.  
As a patch release, Qt 5.12.12 does not add any new functionality but provides  
bug fixes and other improvements and maintains both forward and backward  
compatibility (source and binary) with Qt 5.12.11.  
  
For detailed information about Qt 5.12, refer to the online documentation  
included in this distribution. The documentation is also available online:  
  
  https://doc.qt.io/qt-5.12/index.html  
  
The Qt version 5.12 series is binary compatible with the 5.11.x series.  
Applications compiled for 5.11 will continue to run with 5.12.  
  
Some of the changes listed in this file include issue tracking numbers  
corresponding to tasks in the Qt Bug Tracker:  
  
  https://bugreports.qt.io/  
  
Each of these identifiers can be entered in the bug tracker to obtain more  
information about a particular change.   
  
Important Changes  
-----------------  
  
### qtbase  
* eeedebf33e Update bundled libjpeg-turbo to version 2.1.0  
libjpeg-turbo was updated to version 2.1.0  
  
* 3ae80cfa8e SQLite: Update SQLite to v3.35.5  
Updated SQLite to v3.35.5  
  
* c5e45d735c QVarLengthArray: fix aliasing error in insert(it, n, v)  
Fixed an aliasing bug affecting insertions of objects aliasing existing  
elements.  
  
* 419505ab01 QXpmHandler: fix re-entrancy bug in xpm_color_name  
Fixed a race condition when concurrently writing .xpm files.  
  
* 1d8bcfbb55 QXpmHandler: actually limit characters-per-pixel to four  
Instead of writing a corrupt file, rejects to write XPM files with more  
than 64^4 colors (more than four characters per pixel) now.  
  
* 508c39a3ae Fix license information for libjpeg-turbo  
Clarified that libjpeg-turbo is actually covered by three licenses, not  
only IJG.  
  
* ec2f36c6b2 Update bundled libjpeg-turbo to version 2.1.1  
libjpeg-turbo was updated to version 2.1.1  
  
* a268e8c4f7 SQLite: Update SQLite to v3.36.0  
Updated SQLite to v3.36.0  
  
### qtwayland  
* 190646bc Fix the logic for decoding modifiers map in Wayland text  
input protocol  
Fix modifiers map decoding logic when receiving the map from the  
compositor.  
  
### qtimageformats  
* 370dd41 Update bundled libtiff to version 4.3.0  
Bundled libtiff was updated to version 4.3.0  
  
### qtvirtualkeyboard  
* 4ab966e9 Fix high CPU utilization caused by key repeat timer  
Fixed high CPU utilization caused by key repeat timer.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-91770 qvnc: Arbitrary memory read vulnerability  
* QTBUG-89899 Integer-overflow in QFixed::QFixed  
* QTBUG-89172 Integer-overflow in QFixed::fromReal(qreal r) through  
QImage::.loadFromData(QByteArray);  
* QTBUG-93494 iOS A11Y VoiceOver: QAccessible::EditableText not  
implemented as "TextField" and value is missing last character  
* QTBUG-93779 [elxr] (error #412) unresolved symbols: 1  
* QTBUG-94070 Memory corruption in sqlite plugin  
* QTBUG-65637 Window minimizing broken after building QT app with Mac OS  
High Sierra SDK  
* QTBUG-89379 QQuickWindow::QtTextRendering cause font problem on Apple  
M1  
* QTBUG-95005 Typo in QOpenGLPaintDevice::dotsPerMeterY  
* QTBUG-95429 Expired certificates in tst_QSslCertificate  
* QTBUG-56595 QXcbConnection::getTimestamp() returns old timestamp  
* QTBUG-86394 QNetworkInterface methods broken when targeting Android 11  
(API-30)  
* QTBUG-95639 MariaDB 10.6 prepared queries metadata cache causes  
breakage in mysql driver  
* QTBUG-95239 Massive memory consumption when rendering small svg  
* QTBUG-95661 Test result counts are incorrect  
* QTBUG-96399 Crash with SIGSEGV in QXcbConnection::getSelectionOwner  
* QTBUG-95042 QFrame Qt::WA_TranslucentBackground is broken with  
specific window flags and drawable child item  
  
### qtsvg  
* QTBUG-95891 svg file freezes QImage  
  
### qtdeclarative  
* QTBUG-69577 while using both qml and JavaScriptCore.framwork, iOS app  
got a non-public api references error  
  
### qttranslations  
* QTBUG-95014 pt_BR translations load incorrect catalogs  
* QTBUG-95013 pt_BR translations not loaded  
  
### qtwayland  
* QTBUG-94602 Releasing wayland buffer from Qt compositor side  
* QTBUG-97094 Wayland modifiers map decoding has flawed logic  
  
### qtwebchannel  
* QTBUG-74611 Flaky tests/auto/webchannel crashes on multiple platforms  
in CI  
  
### qtwebengine  
* QTBUG-71895 [REG 5.10->5.11] When calling clearHttpCache() it can  
cause a crash when loading a url  
* Security fixes from Chromium up to version 95.0.4638.69, including:  
  - CVE-2021-3517:  libxml2: Heap-based buffer overflow in  
    xmlEncodeEntitiesInternal() in entities.c  
  - CVE-2021-3541: libxml2 Exponential entity expansion attack bypasses all  
    existing protection mechanisms  
  - CVE-2021-30522: Use after free in WebAudio  
  - CVE-2021-30547: Out of bounds write in ANGLE  
  - CVE-2021-30553: Use after free in Network service  
  - CVE-2021-30559: Out of bounds write in ANGLE  
  - CVE-2021-30560: Use after free in Blink XSLT  
  - CVE-2021-30569: Use after free in sqlite  
  - CVE-2021-30585: Use after free in sensor handling  
  - CVE-2021-30603: Race in WebAudio  
  - CVE-2021-30618: Inappropriate implementation in DevTools  
  - CVE-2021-30627: Type Confusion in Blink layout  
  - Security bug 1184294  
  - Security bug 1197786  
  - Security bug 1198216  
  - Security bug 1202534  
  - Security bug 1204814  
  - Security bug 1242257  
  - Security bug 1252858  
  
### qtvirtualkeyboard  
* QTBUG-94259 High CPU load on embedded targets caused by timers  
* QTBUG-85245 Candidate characters are mixed in uppercase and lowercase  
when using Pinyin in Simplified Chinese  
  
Known Issues  
------------  
  
Credits for the  release goes to:  
---------------------------------  
  
Aavitsland Eirik  
Achtelik Mike  
Brüning Michael  
Buddenhagen Oswald  
D'Angelo Giuseppe  
Dawes Rodney  
Heikkinen Jani  
Hermann Ulf  
Holland Dominik  
Jensen Allan Sandfeld  
Koivikko Jarkko  
Kosmale Fabian  
Köhne Kai  
Lemire Paul  
Macieira Thiago  
Mutz Marc  
Okada Shinichi  
Pocheptsov Timur  
Qi Liang  
Rutledge Shawn  
Shaw Andy  
Sørvig Morten Johan  
Thibault Samuel  
Trillmann Jens  
Valdmann Jüri  
Vestbø Tor Arne  
Welbourne Edward  
