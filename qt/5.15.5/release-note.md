Release note  
============  
  
Qt 5.15.5 release is a patch release made on the top of Qt 5.15.4. As a patch  
release, Qt 5.15.5 does not add any new functionality but provides bug fixes  
and other improvements.  
  
For detailed information about Qt, see the Qt 5.15 online documentation:  
https://doc.qt.io/qt-5/index.html.  
  
Important Changes  
-----------------  
  
### qtbase  
* d2068a8108 Read DPI from X Settings initially as well  
Qt now reads Xft/DPI from X settings at startup, and will prefer this  
value over Xft.dpi from X resources.  
  
* 4ec4a46d79 Update bundled libjpeg-turbo to version 2.1.0  
libjpeg-turbo was updated to version 2.1.0  
  
* 9e8f580d76 Windows: Work-around misreporting of Script and Roman  
Fixed text in "Roman" and "Script" bitmap fonts not showing in Qt Quick  
applications.  
  
* 4dccd73b40 Windows: Add synthesized fonts also when there is a style  
name  
Fixed an issue where bold/italic would not be synthesized for fonts if  
QFont::NoFontMerging was set.  
  
* a15c16f5c8 Fix memory leak when using small caps font  
Fixed a memory leak when initializing a small caps font.  
  
* 54eac7e5ac SQLite: Update SQLite to v3.35.5  
Updated SQLite to v3.35.5  
  
* 096c622368 macOS: Fix synthesized bold  
Fixed an issue where boldness would not be correctly synthesized for  
families with no bold variant.  
  
* 716303c35a Write out the HTML correctly for nested lists  
The output of toHtml() now handles nested lists correctly.  
  
* dc9c43b115 QVector: fix compilation failure in C++20 mode w/strict  
iterators  
Fixed a compile error in QVector(int, T) that occurred in C++20 mode  
with QT_STRICT_ITERATORS.  
  
### qtconnectivity  
* bc3352eb CoreBluetooth: add a workaround to enable using scan options  
Enable setting a scan option (that allows duplicates)  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-91892 [Reg : 5.15.2 -> 5.15.3] Clipped layout margins  
* QTBUG-86806 QFile::copy() calls syncToDisk() on the wrong object  
* QTBUG-92838 Redownloading same file in parallel produces a warning  
about removal of cache file  
* QTBUG-92051 The keyboard does not appear after changing the focus  
* QTBUG-91885 QSqlTableModel support column names with dots  
* QTBUG-91720 Webassembly: TapHandler onSingleTap stopped working  
* QTBUG-77427 setDropAction() is not respected in ItemViews during move  
operation on MAC  
* QTBUG-65927 Shift the coordinates under Android when I use QML + c++.  
* QTBUG-84029 Reg:Frameless Window when moved 0 0 shifts few pixel to  
left  
* QTBUG-91284 Http2: authenticationRequired is not emitted  
* PYSIDE-1404 Incompatible import of "Object" in compiled UI  
* QTBUG-91194 Android Service - Exception on startup  
* QTBUG-66727 [Android]: When changing focus between TextInput fields  
there is a flicker of the QQuickWidget  
* QTBUG-91758 [REG 5.13.2->5.14.0]: QPainter renders <Spaces> in Text  
wrong when units  set to micrometers  
* QTBUG-93032 Reg:5.15.2->5.15.3 QPushButton Focus rect is change of  
behavior  
* QTBUG-92240 MDI Sub window title remains in main window title when  
DontMaximizeSubWindowOnActivation option used  
* QTBUG-93475 QPainter rotate causes pixmap rendering issues  
* QTBUG-90840 QSyntaxHighlighter does not apply capitalization with  
QTextCharFormat::setFontCapitalization  
* QTBUG-91770 qvnc: Arbitrary memory read vulnerability  
* QTBUG-85702 qt5_add_big_resources does not work with QT_NAMESPACE  
* QTBUG-61652 Android's virtual keyboard "OK" button must not accept the  
QDialog  
* QTBUG-91362 Cursor handle in wrong place when app is launched i split  
screen  
* QTBUG-85826 Some Windows fonts don't work in Text  
* QTBUG-91398 When QFont::NoFontMerging is set then if bold or italics  
is requested that is not provided by the font then it will end up not  
synthesizing this  
* QTBUG-93779 [elxr] (error #412) unresolved symbols: 1  
* QTBUG-63393 [iOS]: When typing in a TextEdit and then using Undo, it  
is only possible to undo the very last change  
* QTBUG-70137 Dockwidgets - Placing QDockWidget is almost impossible  
* QTBUG-93677 QStringView::mid() does not work for length < 0  
* QTBUG-71123 "moc" failed to parse auto in trailing-return-type signals  
and slots  
* QTBUG-82037 When an application built with CMake is using a statically  
linked version of Qt then it will not include the SVG based image format  
* QTBUG-93501 Missing support for PLUGIN_EXTENDS (qmake) and  
QT_PLUGIN_EXTENDS (CMake) with Qt static builds  
* QTBUG-71701 QFileSystemModel fails to locate a host from the root  
node's visible children  
* QTBUG-49771 Backspace key is not working when CapsLock is on  
* QTBUG-85634 Japanese and Chinese characters have no effect by bold  
enabled  
* QTBUG-92584 QSqlTableModel ORDER BY doesn't quote table name [with  
spaces]  
* QTBUG-88374 QTextDocument::toHtml: nested lists (ul, ol) not nested in  
output  
* QTBUG-93494 iOS A11Y VoiceOver: QAccessible::EditableText not  
implemented as "TextField" and value is missing last character  
* QTBUG-88651 Can't Hide Menu Separator  
* QTBUG-93620 W System.err: java.lang.NoSuchMethodException:  
notifyQtAndroidPluginRunning  
* QTBUG-93831 [REG 5.15.2->5.15.4]: Android: Copy-pasting text is not  
possible after pasting  
* QTBUG-92188 Stack smashing detected using QImage::scaled  
* QTBUG-84494 Keyboard layout not managed on Keys.event  
* QTBUG-90030 Persistent index handling in QAbstractItemModel is wrong  
* QTBUG-92886 QAbstractItemModelTester false positive removing rows with  
no columns  
* QTBUG-92488 When a QComboBox is set to use Fusion style after changing  
the size adjust policy to AdjustToContents then it will cut off the last  
item in a list and force it to be scrollable  
* QTBUG-93736 QCombobox last item become inaccessible when a listview is  
used in popup  
* QTBUG-42469 QTreeWidget animated crashes when QTreeWidgetItems are set  
hidden to true  
* QTBUG-67944 If user pressed back button during application startup.  
Application becomes unresponsive.  
* QTBUG-91385 Cannot run pdf examples on iOS  
* QTBUG-58013 Cursor position changes not properly passed to input  
method  
* QTBUG-90799 Select handles Left- and RightPoint goes to the wrong  
place when double tapping on a word on the widget dialog  
* QTBUG-90395 FTBFS: qendian.h missing <limits> include  
* QTBUG-61037  tst_QTimeLine::interpolation is flaky; so is frameRate  
* QTBUG-64446 tst_QWidget::multipleToplevelFocusCheck() on linux  
* QTBUG-46116 tst_qwidget fails in the CI  
* QTBUG-62583 tst_QNetworkReply::ioHttpRedirectPolicy() fails in the CI  
with Linux Jethro armv7  
* QTBUG-86677 QToolBar button resize chops text  
* QTBUG-82339 tst_QGestureRecognizer::panGesture Two finger failed  
* QTBUG-88989 Build errors on Android with latest gradle  
* QTBUG-73990 Context Menu Items Fonts and Hotkeys Not Displaying  
* QTBUG-94036 tst_QAccessibilityMac::notificationsTest() fails  
  
### qtdeclarative  
* QTBUG-86017 DelegateModel: Warning and assert with a persisted item  
* QTBUG-93048 Signal and Handler Event System   demo Grammatical errors  
* QTBUG-93404 QML Debugging : Breakpoints' internal ID is not assigned  
properly  
* QTBUG-63673 PinchArea uses wrong coordinate system when inside a  
rotated container item  
* QTBUG-92224 Show let type variable in Locals  
* QTBUG-93264 TableView: first column does not unhide when changing  
column width  
* QTBUG-74572 When using a syntax highligher on the QQuickTextDocument,  
then triggering a rehighlight does not automatically update the text  
control using it  
* QTBUG-69577 while using both qml and JavaScriptCore.framwork, iOS app  
got a non-public api references error  
* QTBUG-92984 Image is painted with wrong Z order  
* QTBUG-91716 TapHandler works only in the upper left corner of the  
screen when QQuickView given another window as parent  
* QTBUG-94016 TapHandler cannot stop propogating event point  
* QTBUG-90395 FTBFS: qendian.h missing <limits> include  
* QTBUG-80415 segfault in software renderer inside  
QSGSoftwareInternalImageNode  
* QTBUG-27671 QMLTest: Some subtests of  
tests/auto/qmltest/events/tst_events.qml are flaky  
  
### qttools  
* QTBUG-49591 Qt Designer: QTableWidget : Horizontal labels are not  
visible (horizontalHeaderVisible property is not saved correctly) when  
in page-based container  
* QTBUG-85513 QTableWidget header item alignment defaults to  
Qt::AlignHCenter|Qt::AlignVCenter visually but Designer shows AlignLeft  
* QTBUG-91558 [REG 6.0/5.15.4] lconvert can not read .qm files  
  
### qtdoc  
* QTBUG-88987 Update VxWorks 7 documentation to include details about  
llvm support  
* QTBUG-56322 Qt for Android source package build error in examples  
  
### qtlocation  
* QTBUG-85636 [Regression] Qml Positioning with nmea source file does  
not work  
  
### qtsensors  
* QTBUG-56322 Qt for Android source package build error in examples  
  
### qtquickcontrols  
* QTBUG-92444 Warning with QML FileDialog  
  
### qtquickcontrols2  
* QTBUG-93039 Crash when scrolling ScrollView with zero-sized item  
* QTBUG-92214 QML Dial with stepsize set gives unexpected result  
* QTBUG-91924 With the Imagine style then it is possible that the  
background of a GroupBox is clipped by two pixels  
* QTBUG-89126 REG: ScrollView doesn't remove ScrollBar after settinging  
the new one  
* QTBUG-93958 Crash with ScrollView + TextArea + Item when the app is  
closing  
* QDS-4212 Changing Range Slider snap mode changes it's orientation  
* QTBUG-83630 Qt Quick Control 2 Tooltip can be way too big when you  
have newlines  
  
### qtcharts  
* QTBUG-59040 QtCharts performance bad when min/max values changed  
* QTBUG-79218 When zooming out enough then the labels on the axes will  
end up showing drawing errors  
  
### qtdatavis3d  
* QTBUG-91103 QML theme shows as totally dark when specified during  
creation  
* QTBUG-65264 Using Theme3D with qtquickcompiler makes black graph  
  
### qtscxml  
* QTBUG-89521 When connecting to the relevant state changed signals for  
a StateMachine then when running via Valgrind there is an invalid read  
on exit  
* QTBUG-92367 [REG 5.15.2->5.15.3]: ScxmlStateMachine submitEvent should  
not always expect data  
  
### qtremoteobjects  
* QTBUG-85795 [QtRemoteObjects] QSortFilterProxyModel sort not working  
properrly  
  
### qtquick3d  
* QTBUG-91718 When a DirectionalLight has rotation or castShadow or a  
PerspectiveCamera is in its own node then an assert can occur  
* QTBUG-90817 Quick3D Model bounds not set in an imported scene  
* QTBUG-90564 Crash if some importer plugin can't be loaded  
* QTBUG-93410 custom shader loading fails with qt quick compiler  
* QTBUG-93445 Shader cache always writes uncompressed data  
* QTBUG-89681 Occasionally exit abnormally during system startup  
* QTBUG-90677 When the default material has NoLighting set then it  
causes any opacityMap set to be ignored  
* QTBUG-93864 1bpp PNG image can't be loaded as Quick3D 5.x Texture  
  
Known Issues  
------------  
  
Credits for the  release goes to:  
---------------------------------  
  
Eirik Aavitsland  
Laszlo Agocs  
Dimitrios Apostolou  
Luca Beldi  
Eskil Abrahamsen Blomfeldt  
Kai Uwe Broulik  
Andreas Buhr  
Albert Astals Cid  
Alexandru Croitor  
Mitch Curtis  
Giuseppe D'Angelo  
Alexey Edelev  
Ilya Fedin  
Pekka Gehör  
Maximilian Goldstein  
Henning Gruendl  
Nicolas Guichard  
Richard Moe Gustavsen  
Zhang Hao  
Miikka Heikkinen  
Karsten Heimrich  
Ulf Hermann  
Volker Hilsheimer  
Allan Sandfeld Jensen  
Friedemann Kleint  
Michal Klocek  
Jarek Kobus  
Tomi Korpipaa  
Fabian Kosmale  
Kai Köhne  
Qiang Li  
Thiago Macieira  
Tamás Martinec  
Bartlomiej Moskal  
Marc Mutz  
Antti Määttä  
Andy Nichols  
Aleksei Nikiforov  
Mårten Nordheim  
Tapio Oksa  
Jukka Passi  
Mauro Persano  
Pasi Petäjäjärvi  
Samuli Piippo  
Timur Pocheptsov  
Joni Poikelin  
Romain Pokrzywka  
Lorn Potter  
Konstantin Ritt  
Shawn Rutledge  
Lars Schmertmann  
Andy Shaw  
Ivan Solovev  
Piotr Srebrny  
Tarja Sundqvist  
Paul Olav Tvete  
Sami Varanka  
Doris Verria  
Juha Vuolle  
Dongmei Wang  
Edward Welbourne  
