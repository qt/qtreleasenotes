Release note  
============  
  
Qt 5.15.15 release is a patch release made on the top of Qt 5.15.14. As a patch  
release, Qt 5.15.14 does not add any new functionality but provides bug fixes  
and other improvements.  
  
For detailed information about Qt, see the Qt 5.15 online documentation:  
https://doc.qt.io/qt-5/index.html.    
  
Important Changes  
-----------------  
  
### Security fixes  
  
* CVE-2023-32763 in qtbase  
  
* CVE-2023-38197 in qtbase  
  
* CVE-2023-37369 in qtbase  
  
* CVE-2023-34410 in qtbase  
  
### qtbase  
* 1f1dbb3633a QPixmapCache: fix leaking of QStrings and Keys on clear()  
Fixed QString key data not being freed on clear().  
  
* a893942c6fe SSL: upgrade the default DH parameters  
The default Diffie-Hellman parameters are now using the 2048-bit MODP  
group from RFC 3526.  
  
* c555b695924 Update bundled libpng to version 1.6.40  
libpng was updated to version 1.6.40  
  
* fc5f7d1cfd7 SQLite: Update SQLite to v3.42.0  
Updated SQLite to v3.42.0  
  
* f1adb5bea86 QSslDiffieHellmanParameters: fix mem-leak  
Fixed a memory leak in parsing of PEM-encoded Diffie-Hellman  
parameters.  
  
* 400a01b20af Update bundled libjpeg-turbo to version 3.0.0  
libjpeg-turbo was updated to version 3.0.0  
  
* 6ad56dce346 Update Harfbuzz to 7.2.0  
The included version of the text shaping library Harfbuzz has been  
disabled on a selection of older platforms where the updated versions do  
not compile. There may be regressions in text appearance with certain  
fonts when rendering languages that depend on OpenType features due to  
this. A possible mitigation is to build an older Harfbuzz version  
manually and use -system-harfbuzz to use this with Qt. This affects the  
following platforms: QNX, Integrity, WinRT, Intel ICC compiler, MacOS  
10.15 and lower, MSVC 2015 and lower.  
  
### qtlocation  
* fd429f76 CoreLocation plugin: introduce RequestAlwaysPermission  
parameter  
Introduce an explicit RequestAlwaysPermission parameter to the  
corelocation plugin. When specified and set to true, this parameters  
enables the "Always" location request. When not specified or set to  
false, only the "When In Use" location permission is requested. By  
default this parameter is not specified.  
  
### qtimageformats  
* 8d1d06d Update bundled libwebp to version 1.3.1  
Update bundled libwebp to version 1.3.1  
  
* 985ad54 Update bundled libtiff to version 4.5.1  
Bundled libtiff was updated to version 4.5.1  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-112663 QFile on Android unable to open file content:// with  
space in the name  
* QTBUG-112738 QDir::entryInfoList() broken on Android when nameFilters  
used  
* QTBUG-113415 QLocale::system().monthName(3).simplified() segfaults  
* QTBUG-113337 [REG 6.4.3 -> 6.5.0] Integer overflow in qfixed_p.h when  
rendering SVG image on the minimal plugin  
* QTBUG-112351 Incorrect description of QtConcurrent::run()  
* QTBUG-108482 Mention more clearly that only a subset of features of  
supported HTML tags are implemented  
* QTBUG-109781 QXmlStreamReader asserts trying to construct XmlStringRef  
of negative len on external input  
* QTBUG-114829 [REG 6.5.1 -> 6.5.2] Crash/failed assert by passing  
certain xml file to QXmlStreamReader  
* QTBUG-110785 QFbCursor memory leak  
* QTBUG-114847 QMAKE_APPLE_DEVICE_ARCHS not documented  
* QTBUG-114991 QVariant<double> comparison uses <float> on  `-qreal  
float`  platforms  
* QTBUG-115062 Incorrect handling of  
QT_FATAL_CRITICALS/QT_FATAL_WARNINGS (non-UB data race)  
* QTBUG-92113 QXmlStreamReader freezes  
* QTBUG-95188 Out-of-memory in QXmlStreamReader  
* QTBUG-113319 ICOReader does not read AND mask for 16bpp/24bpp ico  
* QTBUG-115215 Changing screen positions does not get updated correctly  
* QTBUG-115263 QHostInfo is leaking QSlotObjectBase in  
tst_QHostInfo::lookupConnectToFunctionPointerDeleted()  
* QTBUG-109832 QMYSQL plugin no longer works with older supported  
versions of MySQL/MariaDB  
* QTBUG-40315 doc: QFontMetrics::elidedText(...) does not work as  
expected for ElideNone  
* QTBUG-90942 QtCore license?  
* QTBUG-112200 Possible memory leak with Fusion style  
* QTBUG-61037  tst_QTimeLine::interpolation is flaky; so is frameRate  
* QTBUG-113592 tst_QTableView::columnViewportPosition failing with WinRT  
msvc2015-x86_64 target  
  
### qtdeclarative  
* QTBUG-100678 QML Runtime Tool help all option is not working  
* QTBUG-114475 QML QQuickPointerHandler crashes  
* QTBUG-87334 Graphical issue on some Android smartphones: white line at  
the top and the right side of the screen  
* QTBUG-115179 Clip optimization in  
QQuickDeliveryAgentPrivate::pointerTargets is too aggressive  
* QTBUG-58718 Problems with JS array sorting after unshift  
  
### qtmultimedia  
* QTBUG-111296 tst_QAudioDeviceInfo::codecs fails with SLES 15.4  
* QTBUG-112930 tst_QMediaPlayerBackend::playlistObject fails with sles  
15.4  
  
### qttools  
* QTBUG-113152 [REG 5.15.8 -> 5.15.9] qt5_create_translation breaks  
projects with multiple same-named ts files  
  
### qtdoc  
* QTBUG-113588 Check attribution details for opengl32sw.dll  
  
### qtlocation  
* QTBUG-109359 Qt on iOS always asks for "always" location permission.  
  
### qtwayland  
* QTBUG-97037 DragHandler / startSystemMove window move issue with QT6  
Webengine on Wayland  
* QTBUG-101366 Failure with more than one EGL-based client buffer  
integration  
  
### qt3d  
* QTBUG-111291 tst_GraphicsHelperGL4::bindFrameBufferAttachment fails  
with SLES 15.4  
  
### qtquickcontrols2  
* QTBUG-112945 QML RangeSlider does not work well on touch screen  
  
### qtcharts  
* QTBUG-114943 Crash in Qt Audio Example on iPhone with Qt Kit 6.2.9 for  
iOS  
  
### qtmqtt  
* QTBUG-112984 Qt MQTT crashes when disconnecting *without fully  
unsubscribing first*, after receiving a message  
  
Known Issues  
------------  
  
* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-5.15/supported-platforms.html  
  
* The RTA (release test automation) reported issues in Qt 5.15.x:  
https://bugreports.qt.io/issues/?filter=21874  
  
* Qt 5.15.15 Open issues in Jira:  
https://bugreports.qt.io/issues/?filter=25225  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Laszlo Agocs  
Nicholas Bennett  
Cliff Bilbrey  
Eskil Abrahamsen Blomfeldt  
Joerg Bornemann  
Assam Boudjelthia  
Michael Brüning  
John Chadwick  
Giuseppe D'Angelo  
Pranta Dastider  
Christian Ehrlicher  
Ilya Fedin  
Tang Haixiang  
Heikki Halmet  
Jani Heikkinen  
Ulf Hermann  
Volker Hilsheimer  
Allan Sandfeld Jensen  
Friedemann Kleint  
Sze Howe Koh  
Fabian Kosmale  
Ievgenii Meshcheriakov  
Safiyyah Moosa  
Marc Mutz  
Mårten Nordheim  
Dennis Oberst  
Joni Poikelin  
Liang Qi  
Matthias Rauter  
Topi Reinio  
Shawn Rutledge  
Ahmad Samir  
Thomas Senyk  
Ivan Solovev  
Axel Spoerl  
Christian Strømme  
Tarja Sundqvist  
Jan Arve Sæther  
Morten Sørvig  
Doris Verria  
Tor Arne Vestbø  
Edward Welbourne  
Oliver Wolff  
