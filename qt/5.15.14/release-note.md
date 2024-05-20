Release note  
============  
  
Qt 5.15.14 long-term supported (LTS) commercial release is a patch  
release made on the top of Qt 5.15.13 (LTS). As a patch release,  
Qt 5.15.14 does not add any new functionality but provides bug fixes and  
other improvements. The release maintains both forward and backward  
compatibility (source and binary) with Qt 5.15.13.  
Source codes are available via the Qt online installer and  
the Qt Code Review tool (https://codereview.qt-project.org/). To get the  
sources via Qt Code Review, you need to log in with a Qt Account that  
has a valid commercial license. For detailed instructions, see  
https://wiki.qt.io/Qt_5.15_Release#Getting_Source_Codes.  
For detailed information about Qt, see the Qt 5.15 online documentation:  
https://doc.qt.io/qt-5/index.html.    
  
Important Changes  
-----------------  
  
### qtbase  
* f7f8274ca4 Text: fix Soft hyphen rendering in QTextLayout::glyphRuns()  
Fixed an issue where spaces would sometimes be shown in soft hyphen  
positions in a string.  
  
* c6944f8cfc qstrncpy: NUL-terminate even when src is nullptr  
Now NUL-terminates the target buffer even when the source pointer is  
nullptr, provided the target buffer has space for at least one byte.  
  
* 8ce99064c9 SQLite: Update SQLite to v3.41.0  
Updated SQLite to v3.41.0  
  
* a42883c2a7 QFSFileEngine: fix overflow bug when using lseek64  
Fixed a bug where opening a file in append mode may fail if the file  
size was bigger than INT_MAX.  
  
* bc885ca2d8 SQLite: Update SQLite to v3.41.1  
Updated SQLite to v3.41.1  
  
* 4cb8325c99 SQLite: Update SQLite to v3.41.2  
Updated SQLite to v3.41.2  
  
* 29dd3b1151 QDnsLookup/Unix: make sure we don't overflow the buffer  
Fixed a bug that could cause a buffer overflow in Unix systems while  
parsing corrupt, malicious, or truncated replies.  
  
* 51fd0b8093 QTest::WatchDog: fix missing timeout resets on test  
function change  
Fixed a bug which caused QTEST_FUNCTION_TIMEOUT to be applied to the  
whole test execution, as opposed to each test function.  
  
### qtsvg  
* f430b95 QSvgFont: Initialize used member, remove unused  
Fixed undefined behavior from using uninitialized variable.  
  
### qtconnectivity  
* bb2f0018 SDP scanner: encode input URLs and escape XML-specific  
characters  
sdpscanner now %-encodes the URLs and escapes all XML-specific  
characters in them before adding the result to the generated XML output.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-46990 Soft hyphen rendered as space  
* QTBUG-62620 [QtQuick, TextEdit] Soft hypen and incorrectly drawn  
selection  
* QTBUG-67038 Soft hyphens are broken  
* QTBUG-102483 Soft hyphen rendered as space on macOS  
* QTBUG-111292 tst_QTimer::zeroTimer fails with SLES 15.4  
* QTBUG-108556 FAIL!  : tst_QTimer::zeroTimer in Ubuntu 20.04 and SLES  
15.4  
* QTBUG-96701 android-build projects cannot be used in Android Studio  
* QTBUG-111275 Inserting a QDate into an Oracle DB with a prepared  
statements fails for timezones like CET  
* QTBUG-110058 QCryptographicHash is not re-entrant  
* QTBUG-110068 qmake: Generated Visual Studio project defaults  
"GenerateDebugInformation" to "false"  
* QTBUG-110497 Qt's CMake Config files reset CMAKE_AUTOMOC_MACRO_NAMES  
* QTBUG-108013 QStandardPaths::PicturesLocation paths on Android  
* QTBUG-104892 QStandardPaths::DocumentsLocation on emulated android  
device returning the same directory twice  
* QTBUG-81860 Android: Add "content:" scheme paths to QStandardPaths  
* QTBUG-106369 Crash when closing modal window with macOS on-screen  
keyboard  
* QTBUG-111183 Qt crash on macOS when using keyboard viewer  
* QTBUG-105250 Access NULL m_platformWindow in qnsview_complextext.mm  
* QTBUG-85544 androiddeployqt fails with message that neither  
libqtforandroid.so or libqtforandroidGL.so are included  
* QTBUG-97636 Qtbase for Android with examples fails to build  
* QTBUG-83997 Can't deploy a simple console application  
* QTBUG-93185 Android platform plugin not linked when using only QtCore  
* QTBUG-56064 QStandardItem:: setEnabled() has no effect on QComboBox  
items when SH_ComboBox_UseNativePopup is applied  
* QTBUG-111347 QMessageAuthenticationCode is not re-entrant  
* QTBUG-74478 mouse flicking on qtabwidget non-current tab causes  
segfault  
* QTBUG-100128 QListWidget/QListView: item widget disappears when item  
is dragged and dropped on itself  
* QTBUG-112465 androiddeployqt fail on Android build platform:  
android-33-ext5  
* QTBUG-112735 Typo in QTextStream documentation ("ISO-5589-1")  
* QTBUG-112953 QTextDocument::contentsChange is emitted several times  
when iBus is on  
* QTBUG-110401 NoSuchMethodError:  
org.qtproject.qt5.android.QtLayout.onSizeChanged  
* QTBUG-112504 QMessageLogger compilation fails with Android NDK r25 and  
SDK < 33  
* QDS-9687 Examples cannot be downloaded  
* QTBUG-112990 QProcess::startDetached() freezes threads on QNX?  
* QTBUG-113315 Segmentation fault in a VirtualBox Linux guest with  
-march=native  
* QTBUG-109466 QTEST_FUNCTION_TIMEOUT applies to the whole test, not per  
function  
* QTBUG-108554 FAIL!  : tst_QTimer::singleShotToFunctors in Ubuntu_20_04  
* QTBUG-111598 Implement get/get_if for QVariant to make it nicer for  
non-default constructible types  
* QTBUG-63481 tst_QSslSocket_onDemandCertificates_member::onDemandRootCe  
rtLoadingMemberMethods tests fail in the CI  
* QTBUG-94232 androiddeployqt is broken when manually defining  
dependencies  
* QTBUG-87728 tst_QGraphicsAnchorLayout::layoutDirection() failed on  
Ubuntu 20.04 in CI  
* QTBUG-87137 tst_QApplication::sendEventsOnProcessEvents() failed on  
Ubuntu 20.04/22.04 and RHEL 9  
* QTBUG-112760 tst_QWidget fails with SLES 15.4  
* QTBUG-104241 tst_QOpenGLWidget::stackWidgetOpaqueChildIsVisible fails  
with Ubuntu 22.04, openSUSE Leap 15.4 and RHEL 9  
* QTBUG-84258 tst_Gestures::graphicsItemGesture fails  
* QTBUG-63433 tst_QWindow:testInputEvents fails on RHEL 7.4 and 9  
* QTBUG-94250 tst_QListView::internalDragDropMove fails with OpenSUSE  
15.3 and RHEL 9  
* QTBUG-62967 tst_QItemDelegate::enterKey(plaintextedit tab) fails on  
openSUSE 42.3  
* QTBUG-89169 tst_QGlyphRun::drawRightToLeft() failed on openSUSE 15.2  
* QTBUG-89209 tst_NetworkSelfTest::smbServer() failed on openSUSE 15.2  
in CI  
  
### qtdeclarative  
* QTBUG-111542 UI problem with iOS deployments  
* QTBUG-87190 Application freezes when there is no control to focus next  
* QTBUG-111935 Qt V4 JIT engine generates bad JIT code on ARM64 (and  
potentially all arches)  
* QTBUG-91425 DelegateModel: Crash when DelegateModelGroup is used for  
delegate geometry and model is cleared  
* QTBUG-111294 tst_HoverHandler::movingItemWithHoverHandler fails with  
SLES 15.4  
* QTBUG-99765 tst_QQuickDropArea::containsDrag_internal fails in Ubuntu  
20.04  
* QTBUG-112360 tst_qquicktext::contentSize fails with SLES 15 SP4  
* QTBUG-82052 tst_QQuickTextEdit::linkHover() is flaky on macOS 10.14  
* QTBUG-64397 tst_qquickwidget::enterLeave() fails often in the CI  
  
### qtmultimedia  
* QTBUG-111296 tst_QAudioDeviceInfo::codecs fails with SLES 15.4  
* QTBUG-112930 tst_QMediaPlayerBackend::playlistObject fails with sles  
15.4  
  
### qtdoc  
* QTBUG-85544 androiddeployqt fails with message that neither  
libqtforandroid.so or libqtforandroidGL.so are included  
* QTBUG-97636 Qtbase for Android with examples fails to build  
* QTBUG-83997 Can't deploy a simple console application  
* QTBUG-93185 Android platform plugin not linked when using only QtCore  
  
### qtlocation  
* QTBUG-91085 [REG 5.15.2->5.15.3] geojson_viewer not launching on macOS  
  
### qtconnectivity  
* QTBUG-112843 [REG 6.5.0->6.5.1] nfc/annotatedurl not compiling on  
Android  
  
### qtwayland  
* QTBUG-111250 Configure tests fail for dmabuf support  
* QTBUG-87303 Wayland context menus can go off the screen because Qt  
does not do set_constraint_adjustment  
* QTBUG-97037 DragHandler / startSystemMove window move issue with QT6  
Webengine on Wayland  
  
### qt3d  
* QTBUG-111291 tst_GraphicsHelperGL4::bindFrameBufferAttachment fails  
with SLES 15.4  
* QTBUG-102315 tst_dynamicnodecreation::createEntityAndDynamicChild  
fails with Ubuntu 20.04  
  
### qtwebengine  
* QTBUG-104869 QWebEngineDownloadItem::totalBytes() always returns -1  
* QTBUG-111697 Build failure with GCC 13  
* QTBUG-110504 Webengine extremely slow in loading webpage in debug  
build  
* QTBUG-108240 WebEngine can't be built with MSVC 14.34 and LLVM 15.0.6  
* QTBUG-111297  tst_QWebEnginePage::mouseMovementProperties fails with  
SLES 15.4  
* QTBUG-110713 Building QtWebEngine + debug mode + Universal build fails  
* QTBUG-106334 TouchInputTest fails with RHEL 9 and SLES 15.4  
  
### qtwebview  
* QTBUG-82810 [Android] Deadlock for dynamically loading webview  
  
### qtcharts  
* QTBUG-108018 Camera Example crashes on macOS 13 ventura  
* QTBUG-109762 Setting plotArea makes the background to disappear  
* QTBUG-111293 tst_QBarSeries::mousehovered fails with SLES 15.4  
  
### qtquick3d  
* QTBUG-112263 Progressive AA does not work when using principled  
materials  
* QTBUG-110039 Assert triggered when antialiasing is enabled with  
Quick3D in Qt 5.15  
* QTBUG-112969 [Reg 5.15.11 -> 5.15.12] Crash when updating shader  
variable in CustomMaterial  
  
Known Issues  
------------  
  
* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-5.15/supported-platforms.html  
  
* The RTA (release test automation) reported issues in Qt 5.15.x:  
https://bugreports.qt.io/issues/?filter=21874  
  
* Qt 5.15.14 Open issues in Jira:  
https://bugreports.qt.io/issues/?filter=25091  
  
Credits for the  release goes to:  
---------------------------------  
  
Amir Masoud Abdol  
Sebastian Beckmann  
Vladimir Belyavsky  
Eskil Abrahamsen Blomfeldt  
Assam Boudjelthia  
Michael Brüning  
Andreas Buhr  
Nicolas Deherly  
Artem Dyomin  
Alexey Edelev  
Christian Ehrlicher  
Andreas Eliasson  
Fabio Falsini  
Ilya Fedin  
Andrei Golubev  
Heikki Halmet  
Andre Hartmann  
Ulf Hermann  
Sam James  
Allan Sandfeld Jensen  
Michal Klocek  
Lars Knoll  
Tomi Korpipää  
Fabian Kosmale  
Kai Köhne  
Inho Lee  
Robert Löhning  
Thiago Macieira  
Bartlomiej Moskal  
Marc Mutz  
Mårten Nordheim  
Aleix Pol  
Rami Potinkara  
Liang Qi  
Ahmad Samir  
Carl Schwan  
Andy Shaw  
Ivan Solovev  
Axel Spoerl  
Tarja Sundqvist  
Jan Arve Sæther  
Morten Sørvig  
Paul Olav Tvete  
Peter Varga  
Tor Arne Vestbø  
Bernd Weimer  
Edward Welbourne  
Vlad Zahorodnii  
