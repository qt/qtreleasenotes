Release note  
============  
  
Qt 5.15.4 release is a patch release made on the top of Qt 5.15.3. As a patch  
release, Qt 5.15.4 does not add any new functionality but provides bug fixes  
and other improvements.  
  
For detailed information about Qt, see the Qt 5.15 online documentation:  
https://doc.qt.io/qt-5/index.html.  
  
Important Changes  
-----------------  
  
### qtbase  
* cb1eed0989 Update bundled libjpeg-turbo to version 2.0.6  
libjpeg-turbo was updated to version 2.0.6  
  
* 8e6489f5eb Support family names that end/start with space  
Fixed matching against fonts which has a family name that ends or  
starts with a space.  
  
* dde0c0a45c SQLite: Update to 3.35.2  
Updated SQLite to v3.35.2  
  
* 107d14825a Disable Harfbuzz/CoreText hotfix on older macOS/iOS  
versions  
Fixed a regression when combining letter spacing with the default font  
on macOS 10.15 and lower or iOS 13 or lower.  
  
* 8f2959c345 QTextHtmlParserNode: Limit colspan to avoid segfault  
QTextDocument::setHtml: column spans are limited to 20480, an  
arbitrarily high but reasonable value.  
  
### qtwayland  
* 560d8a3b Fix race condition when attaching client to text input  
Fixed a problem where a virtual keyboard would not be updated correctly  
if two clients were started at almost the same time.  
  
### qtimageformats  
* f67ef5b Update bundled libwebp to version 1.2.0  
Update bundled libwebp to version 1.2.0  
  
* f98953f Update bundled libtiff to version 4.2.0  
Bundled libtiff was updated to version 4.2.0  
  
### qtserialbus  
* 17ac276 Fix Modbus custom command size calculation  
Fix Modbus TCP custom command size calculation.  
  
* 4e7a1e8 Fix Modbus custom command response processing  
Fix Modbus custom command response processing.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-89889 tst_QDateTime::systemTimeZoneChange fails on 32bit systems  
* QTBUG-88543 QDateTime::fromString does not accept Qt::TextDate format  
from toString() in Vietnamese locale  
* QTBUG-32778 Documentation colors conflicting with system theme make  
text unreadable  
* QTBUG-87871 QMdiSubWindow's window icon size is incorrect for system  
scaling 150% or more  
* QTBUG-83632 In top level frameless window Qt.CrossCursor does not  
comes in effect  
* QTBUG-83295 QLineEdit::editingFinished() not emitted when pressing the  
clear button and moving focus away  
* QTBUG-90949 UI rendering and interaction dead lock when used as an  
window embedded application  
* QTBUG-91401 Error loading PNG: Unsupported ICC profile class 70727472  
* QTBUG-87078 xcb: showMaximized() in full screen only restores the  
window with some WMs  
* QTBUG-91532 tst_QMenu::QTBUG_89082_actionTipsHide() failing on Windows  
* QTBUG-63275 Android QScreen::grabWindow(0) & sample code  
Screenshot::shootScreen() fails on Android  
* QTBUG-72231 WASM: DropShadow leads to misrendering in other places  
* QTBUG-89366 [REG 5.15] Style Sheet text-align: bottom  
* QTBUG-91735 qstylesheetstyle.cpp position() pointer is accessed before  
checking hasPosition()  
* QTBUG-86857 QPushButton style "text-align: bottom" not working in Qt  
5.15.1  
* QTBUG-91073 Android:  cursor movement in TextEdit is not tracked, so  
it can go behind the soft-keyboard  
* QTBUG-91539 QThread::quit() is unreliable on Windows  
* QTBUG-91455 Qt.ImhFormattedNumbersOnly flag does not show minus sign  
in iOS keyboard  
* QTBUG-91909 QtConcurrenceThreadEngine > ThreadEngineStarter<VOID>?  
* QTBUG-90568 package (rpcs3)  fails to build when QT(qtconcurrent) was  
built with gcc-11  
* QTBUG-91764 [REG 5.15.2->5.15.3]: When specifing a letterSpacing for  
the default font, it will end up displaying incorrect characters  
* QTBUG-87326 Removal of "old time-zone lookup fallbacks" breaks TZ  
handling on Gentoo  
* QTBUG-92046 Description of Julian calendar is wrong  
* QTBUG-92173 [iOS]: Crash occurs when showing a new QQuickWindow after  
the first one is deleted  
* QTBUG-66448 Android KEYCODE_MEDIA_PLAY_PAUSE is incorrectly translated  
to Qt.Key_MediaPlay in QML  
* QTBUG-90396 QFontDialog highlights default value for the font style  
list  
* QTBUG-86134 [Reg 5.9 -> 5.12] QPushButton: icon not aligned when menu-  
indicator is removed  
* QTBUG-90250 QPushButton: menu indicator with stylesheet not drawn  
correctly  
* QTBUG-92178 Editable Tree Model fails QAbstractItemModelTester  
* QTBUG-92275 Slow and memory intensive handling of input to  
QDateTime::fromString  
* QTBUG-91223 qt_memrotate270, qt_memrotate180 , qt_memrotate90,  
segfaults  
* QTBUG-88031 iOS: quickcontrols2/gallery fails to build in release mode  
(Failed to parse qmlimportscanner output)  
* QTBUG-92490 Stylesheet with pseudo state on QPlainTextEdit  
* QTBUG-89735 MultiPointTouchArea delays release on three finger tap  
* QTBUG-90699 tst_QApplication::focusWidget() and focusMouseClick()  
failed on macos 10.15 in CI  
* QTBUG-91261 Invalid pointer return with QGridLayout::itemAt(-1)  
* QTBUG-91029 Windows/Accessibility: Focused QListWidget is not  
announced by screen readers  
* QTBUG-91788 Assert when removing a model from  
QConcatenateTablesProxyModel that is bound to a QSortFilterProxyModel  
* QTBUG-92220 QAbstractItemModelTester false positive  
* QTBUG-92040 [macOS] Labs platform context menu items are disabled on  
modal window  
* QTBUG-95429 Expired certificates in tst_QSslCertificate  
* QTBUG-56552 QDateTime/QTime truncates milliseconds when converting to  
Qt::ISODate string  
* QTBUG-82617 Crash on exit via back button on Huawei Mate 20 Pro  
* QTBUG-85449 Crashes at the destructors of std::thread and std::mutex.  
* QTBUG-83043 Crash in libqtforandroid.so  
* QTBUG-91253 QConcatenateTablesProxyModel crushes being sourceModel in  
QSortFilterProxyModel  
* QTBUG-79140 [REG 5.13.0 -> 5.14.0]OTF fonts don't work correctly  
* QTBUG-89050 there seems to be no way to search backwards in  
QStringView with QRegularExpression  
* QTBUG-84258 tst_Gestures::graphicsItemGesture fails  
* QTBUG-91385 Cannot run pdf examples on iOS  
  
### qtsvg  
* QTBUG-91507 Out of bounds read in function  
`QRadialFetchSimd<QSimdSse2>::fetch` when input craft svg file  
* QTBUG-90744 [REG: 5.13 -> 5.14] QPixmap::load returns false for svg  
files if file encoding not utf-8 & format not specified  
  
### qtdeclarative  
* QTBUG-91196 Locale QML documetnation lists misspelled property  
* QTBUG-90239 TextField with regex clears text if unmatched char is  
typed  
* QTBUG-91519 [REG 5.14.2 -> 5.15.0] Call QQmlIncubator::clear() inside  
QQmlIncubator::setInitialState() crashes afterward  
* QTBUG-91491 Crash in Generator::method_next when creating new  
properties on Generator  
* QTBUG-90362 The first character in text input fields appears last on  
Android 10/11  
* QTBUG-87197 MouseArea containsMouse value incorrect after visibility  
changes  
* QTBUG-92076 TableView: forceLayout() fails when all columns are hidden  
* QTBUG-92099 TableView: content height doesn't change when adding new  
rows  
* QTBUG-90740 Quick test: inline components within components passed to  
createTemporaryObject cause crash  
* QTBUG-90762 QuickTest: List testcases when testcase is inline  
component  
* QTBUG-92236 When the cache for a QML file is generated and then loaded  
it will cause a crash  
* QTBUG-92036 Visual ordering flips when QSGRenderNode is used with  
DepthAwareRendering  
* QTBUG-89892 crash when assigning null to anchors.horizontalCenter  
* QTBUG-91749 Incorrect batching using overlapping QSGGeometry with  
lines having a width > 1  
* QTBUG-91867 TextInput cursorDelegate position not updated after left  
padding change  
* QTBUG-46350 Crash when deleting item currently set in PropertyChanges  
target  
* QTBUG-91276 DelegateModel can crash with retranslate()  
* QTBUG-41867 disabled particle Emitter still causes QSG renderer  
uploads  
* QTBUG-86708 When using DelegateModelGroup to group items then when a  
created item which is set to not be included will trigger an assert  
  
### qtactiveqt  
* QTBUG-92237 Document the qaxserver_no_register configuration  
  
### qtmultimedia  
* QTBUG-51064 QML Video type doesn't work with core profile  
* QTBUG-62694 Setting default surface format with 3.2 core profile  
breaks video decoding with a custom QAbstractVideoSurface on macOS  
  
### qttools  
* QTBUG-91754 qdoc crash when generic documents of qtbase  
  
### qtdoc  
* QTBUG-86614 When a service is set to be started at boot time it is not  
being started after a reboot of the device  
* QTBUG-92388 Documentation page on rcc is freaking out  
  
### qtwayland  
* QTBUG-86177 Some subsurfaces change but are never committed  
* QTBUG-91096 >1 Programs on QtWayland causes QtVirtualKeyboard to not  
work  
* QTBUG-89680 Touch is ignored if up and down arrives in the same  
wl_touch.frame  
  
### qtserialbus  
* QTBUG-62192 MODBUS custom command doesn't work  
* QTBUG-91037 MODBUS custom command doesn't work  
  
### qtquickcontrols2  
* QTBUG-61021 Autocomplete of editable ComboBox not working on Android  
* QTBUG-87236 NinePatchImage causes crash due to repeated presses.  
* QTBUG-88162 Crash when NinePatchImage's source is changed  
  
### qtdatavis3d  
* PYSIDE-1438 Using QBar3DSeries.dataProvider().addRow() segfaults  
  
### qtremoteobjects  
* QTBUG-91229 tst_Server_Process::testRun fails with macOS 10.15  
* QTBUG-82284 TestModelView::testDataInsertionTree fails for Windows 7  
* QTBUG-84640 Disconnected ExternalIODevice Not Handled  
  
Known Issues  
------------  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Laszlo Agocs  
Nikolay Avtomonov  
Alex Blasche  
Eskil Abrahamsen Blomfeldt  
Assam Boudjelthia  
Michael Brasser  
Andreas Buhr  
Wang Chuan  
Giuseppe D'Angelo  
Alexey Edelev  
David Edmundson  
Oliver Eftevaag  
Christian Ehrlicher  
David Faure  
Samuel Gaist  
Pablo Luis Garcia  
Maximilian Goldstein  
Jan Grulich  
Richard Moe Gustavsen  
Heikki Halmet  
Andreas Hartmetz  
Jani Heikkinen  
Karsten Heimrich  
Ulf Hermann  
Volker Hilsheimer  
Allan Sandfeld Jensen  
Christoph Keller  
Hyunkook Khang  
Friedemann Kleint  
Michal Klocek  
Sze Howe Koh  
Fabian Kosmale  
Sona Kurazyan  
Kai Köhne  
Paul Lemire  
Robert Löhning  
Piotr Mikolajczyk  
Bartlomiej Moskal  
Mårten Nordheim  
Pasi Petäjäjärvi  
Timur Pocheptsov  
Joni Poikelin  
Aleix Pol  
Lorn Potter  
Liang Qi  
Topi Reinio  
Andre de la Rocha  
Dong Rui  
Shawn Rutledge  
Siyeon Seo  
Dmitry Shachnev  
Nick Shaforostov  
Andy Shaw  
Brett Stottlemyer  
Tarja Sundqvist  
Jan Arve Sæther  
Morten Johan Sørvig  
Alex Trotsenko  
Tuomas Vaarala  
Doris Verria  
Tor Arne Vestbø  
Alexander Volkov  
Ville Voutilainen  
Edward Welbourne  
Paul Wicking  
Weng Xuetian  
Zhang Yu  
JiDe Zhang  
