Release note  
============  

Qt 6.1 introduces many new features and improvements as well as bugfixes  
over the 6.0.x series. For more details, refer to the online  
documentation included in this distribution. The documentation is also  
available online:  
  
https://doc.qt.io/qt-6/index.html  
  
The Qt version 6.1 series is binary compatible with the 6.0.x series.  
Applications compiled for 6.0 will continue to run with 6.1.  
  
Some of the changes listed in this file include issue tracking numbers  
corresponding to tasks in the Qt Bug Tracker:  
  
https://bugreports.qt.io/  
  
Each of these identifiers can be entered in the bug tracker to obtain  
more information about a particular change.  
  
To make it easier to port to Qt 6, we have created a porting guide to  
summarize those changes and provide guidance to handle them. In the  
guide, you can find links to articles about changes that may affect your  
application and help you transition from Qt 5.15 to Qt 6:  
  
https://doc.qt.io/qt-6/portingguide.html  
  
Important Changes  
-----------------  
  
### qtbase  
* 85cd9b144b QVarLengthArray: fix aliasing error in insert(it, n, v)  
Fixed an aliasing bug affecting insertions of objects aliasing existing  
elements.  
  
* f63f4b3e62 Revert "Windows: Add synthesized fonts also when there is a  
style name"  
Fixed a regression where different font styles and/or weights would not  
be available.  
  
* 8db031cb0f Change QCollator's default locale to QLocale().collation()  
The default locale used by QCollator is now the collation locale of the  
default QLocale. This restores the ability (lost at 5.14) to control the  
locale used by QString::localeAwareCompare(), while retaining the use of  
a collation locale when the default is the system locale.  
  
* c4012ff5f0 Make QFutureWatcher::isFinished() consistent with the  
watched QFuture  
The QFutureWatcher::isFinished() method now indicates if the related  
QFuture is finished, instead of indicating if the finished() signal was  
delivered. This makes it consistent with the future that is being  
watched.  
  
* 3fa9c19481 QCryptographicHash: don't present the same data over and  
over again  
Fixed a bug where presenting more than 4GiB in a single addData() call  
would calculate the wrong result().  
  
* 36760514a9 QXpmHandler: fix re-entrancy bug in xpm_color_name  
Fixed a race condition when concurrently writing .xpm files.  
  
* e0c6f50849 QXpmHandler: actually limit characters-per-pixel to four  
Instead of writing a corrupt file, rejects to write XPM files with more  
than 64^4 colors (more than four characters per pixel) now.  
  
* 77672e6c16 Fix memory leak if eXIf has incorrect crc  
Fix for possible memory leak in libpng was backported.  
  
### qtsvg  
* 77483e3 Limit font size to avoid numerous overflows  
Avoid numerous overflows by limiting font size to 0xffff. This fixes  
oss-fuzz issue 31701.  
  
### qtdoc  
* 41c06b3f Move Qt Shader Tools, Qt Quick 3D, Qt Quick Timeline to GPL  
section  
Mark Qt Shader Tools, Qt Quick 3D, and Qt Quick Timeline in the module  
overview as available under Commercial/GPLv3 only.  
  
### qtvirtualkeyboard  
* 6c42bcb Fix processing of hard Qt::Key_Backspace and Qt::Key_Delete  
Fix processing of hard backspace and delete keys.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-94501 GStreamer::Gl dependency is not recorded correctly in a  
static build  
* QTBUG-94069 MacOS ComboBox Focus Ring is Too Tall  
* QTBUG-82835 Stale socket notifications can be emitted to new sockets  
* QTBUG-94175 QGraphicsProxyWidget: rendered Arabic text incomplete in  
large font sizes when OpenGL is used  
* QTBUG-65637 Window minimizing broken after building QT app with Mac OS  
High Sierra SDK  
* QTBUG-94246 Memory leak in qsql_oci plugin  
* QTBUG-91919 Qt will crash if changing screen resolution on Mac  
* QTBUG-94706 missing documentaiton details about QFile::copy()  
* QTBUG-94538 Change cursor theme is not applied immediately . The Qt5  
app needs to be restarted.  
* QTBUG-85529 Polytonic Greek characters cannot be composed both ways  
* QTBUG-83869 Correction to the documentation:  
https://doc.qt.io/qt-5/qtransform.html#basic-matrix-operations  
* QTBUG-85714 QOpenGLWidget with NativeWindow QDockWidget does not  
render when undocked  
* QTBUG-94839 QSystemTrayIcon::isSystemTrayAvailable() opens a new file  
descriptor on each call which isn't closed  
* QTBUG-91398 When QFont::NoFontMerging is set then if bold or italics  
is requested that is not provided by the font then it will end up not  
synthesizing this  
* QTBUG-92477 Memory leak in QFontDatabase  
* QTBUG-93890 Crash in webOS emulator with recent meta-qt6  
* QTBUG-78043 non-native QFileDialog displaying incorrect mapped network  
drive names  
* QTBUG-94973 Build fails when configuring twice with CMake and with  
both INSTALL_MKSPECSDIR and QT_QMAKE_TARGET_MKSPEC set  
* QTBUG-91125 QTextFormat::FullWidthSelection does not work with right-  
to-left text layout  
* QTBUG-90683 Some keyboard shortcuts will crash Qt when matching is  
attempted on macOS 10.15 or higher  
* QTBUG-65637 Window minimizing broken after building QT app with Mac OS  
High Sierra SDK  
* QTBUG-92561 Strange selection behavior of with ExtendedSelection +  
SelectRows  
* QTBUG-83619 Stylesheet: QAbstractItemView::indicator changes selected  
item text color  
* QTBUG-94981 QTreeView: expandToDepth() and expandAll() ends  
prematurely for asynchronous models  
* QTBUG-95013 pt_BR translations not loaded  
* QTBUG-95198 Building QtMultimedia qmake projects is broken on Windows  
* QTBUG-94788 QListView will be reset when setSelectionMode  is  
MultiSelection  
* QTBUG-94226 QListView - broken drag-n-drop items movement  
* QTBUG-94802 [Reg-5.15.4->5.15.5]Menu separator is not visible  
* QTBUG-38776 QDockWidget titlebar icons are not drawn with high DPI  
* QTBUG-94069 MacOS ComboBox Focus Ring is Too Tall  
* QTBUG-94824 In qlinedit, icon and text overlap  
* QTBUG-86846 the password box not refreshed under Chinese input method  
* QTBUG-94942 QML type registration emits "qt6quick_metatypes.json:  
illegal value"  
* QTBUG-94737 Crash in QThreadOnce test  
* QTBUG-95009 QNetworkDiskCache::cacheSize() returns a size twice as  
large as the real one.  
* QTBUG-95277 HTTP2: QNetworkReply::encrypted not emitted  
* QTBUG-94733 When the display is set to 150% and a QMdiSubWindow is  
maximized then the icons can be incorrectly displayed  
* QTBUG-95293 QCocoaAccessibilityElement incorrect selector for  
"enabled": should be isAccessibilityEnabled not  
accessibilityEnabledAttribute  
* QTBUG-95255 After setDefaultAction for a QToolButton and call  
setChecked, then checked status wrong  
* QTBUG-91048 QFutureWatcher::isFinished() stays false after  
waitForFinished()  
* QTBUG-95283 No TLS backend available in statically built project  
* QTBUG-91459 When using Speech Recognition on a multiple monitor setup  
telling it to click a button does not always work on the secondary  
monitor  
* QTBUG-77656 Crash when waking up with multiple displays in clamshell  
mode  
* QTBUG-95383 QFileSystemModel sort extremely inefficient with wildcards  
* QTBUG-95429 Expired certificates in tst_QSslCertificate  
* QTBUG-95619 [Mac] Memory leak in  
QNSWindow::applicationActivationChanged  
* QTBUG-95273 QFuture::then() documentation about threading is unclear  
* QTBUG-20894 QCompleter unexpectedly changes QLineEdit text  
* QTBUG-56595 QXcbConnection::getTimestamp() returns old timestamp  
* QTBUG-95631 Stylesheet issue when try to change background color with  
a editable combobox on hover  
* QTBUG-94215 [Reg 5.15.2->5.15.3/6] QString::lastIndexOf is broken  
* QTBUG-93360 Compile Qt with gcc 11  
* QTBUG-94973 Build fails when configuring twice with CMake and with  
both INSTALL_MKSPECSDIR and QT_QMAKE_TARGET_MKSPEC set  
* QTBUG-87429 tst_QRhi::renderToTextureArrayOfTexturedQuad fails on  
Android Emulator in CI  
* QTBUG-94463 QThreadPool creates one thread more than maxThreadCount  
* QTBUG-95050 [REG: 5.2->5.14] Locale used by  
QString::localeAwareCompare() no longer changeable  
* QTBUG-95199 Incorrect propagation of iOS bitcode and -fapplication-  
extension flags to user projects  
* QTBUG-91713 QtBase benchmarks fail for qtimezone, qdiriterator, and  
qfile  
* QTBUG-95303 Internal module pri files are missing public include  
header locations  
* QTBUG-80957 QFutureInterface: reportResults with an empty vector  
breaks results  
* QTBUG-95429 Expired certificates in tst_QSslCertificate  
* QTBUG-70137 Dockwidgets - Placing QDockWidget is almost impossible  
* QTBUG-71590 Qt is using "Non-SDK" interfaces, will be blocked by  
Android  
* QTBUG-95552 Reproducible crash from wheelEvent in QGraphicsScene  
containing a QWidget with a Q*BoxLayout  
  
### qtsvg  
* QTBUG-94878 QSvgRenderer crash  
* QTBUG-92184 QtSVG cannot understand minified SVGs if they contain arcs  
  
### qtdeclarative  
* QTBUG-92840 FolderListModel docs have gone missing  
* QTBUG-92563 Extra, incorrect HoverMove sent after MouseButtonRelease  
* QTBUG-95073 TextEdit inconsistency with some key events (modifiers)  
* QTBUG-75553 QML Canvas, reset line dash failed  
* QTBUG-89375 No C++ documentation for containmentMask  
* QTBUG-94622 svg Image is  Pixelated when windows is scaled  
* QTBUG-95132 Memory Leak when using QQuickPaintedItem with RHI  
* QTBUG-95417 Regression 5.15.4: gc() within generator functions crash  
* QTBUG-95591 QtQuick documentation references private class  
"QQuickColorGroup"  
* QTBUG-95811 KeyNavigation: all properties should be marked as attached  
* QTBUG-94798 crash in QQuickDesignerSupport with gcc at ubuntu  
* QTBUG-94971 QHoverEvent::scenePosition() is actually local position  
* QTBUG-94622 svg Image is  Pixelated when windows is scaled  
* QTBUG-94928 loop QQuickDesignerSupport with simple example  
* QTBUG-75862 FocusReason is broken in Controls 2  
* QTBUG-89380 Cannot use QtObject as containmentMask  
* QTBUG-94844 Rendering errors with ShaderEffect after hiding and  
reshowing a window  
  
### qtactiveqt  
* QTBUG-95407 activeqt/qutlook fails to configure  
  
### qttools  
* QTBUG-91082 [REG: 5.12->5.13] Assistant does not support custom  
filters anymore  
* QTBUG-95561 Typo in the "Introduction To QDoc" manual page.  
* QTBUG-87677 windeployqt locates a release version of icudtXX.dll for a  
debug binary  
* QTBUG-94056 Qt6.1.1 Assistant Manual has incorrect version: 6.1.0  
  
### qttranslations  
* QTBUG-94718 TS files generated by ts-${catalog}-${lang} should contain  
source text location information  
* QTBUG-95014 pt_BR translations load incorrect catalogs  
  
### qtdoc  
* QTBUG-92848 Update Documentation of Qt6: Deploying QML Applications -  
Ahead-of-Time Compilation  
  
### qtwayland  
* QTBUG-94602 Releasing wayland buffer from Qt compositor side  
  
### qt3d  
* QTBUG-93035 Adding a disable entity to the scene and enabling it later  
isn't properly picked up  
* QTBUG-93035 Adding a disable entity to the scene and enabling it later  
isn't properly picked up  
* QTBUG-95130 Qt3D ShaderProgram sources cannot compile on iOS (RHI)  
  
### qtquickcontrols2  
* QTBUG-92824 QtQuick.Controls Button.qml wrong parent used for  
transitionDuration (line 77)  
* QTBUG-93041 If Button is used as delegate of ListView then application  
fails  
* QTBUG-83630 Qt Quick Control 2 Tooltip can be way too big when you  
have newlines  
* QTBUG-83630 Qt Quick Control 2 Tooltip can be way too big when you  
have newlines  
  
### qtdatavis3d  
* QTBUG-94441 Axis title labels do not respect the Abstract3DAxis's  
titleFixed property  
* QTBUG-80194 Q3DScatter Memory Leak  
* QTBUG-78767 baseGradient for Surface3DSeries is applied incorrectly  
when the trailing line(s) of the QSurfaceDataArray contain NaN only  
* QTBUG-94364 Rotate and zoom do not work on Android  
* QTBUG-95112 Surfacedata containing only nans at row 0 fails to render  
surface and crashes the next time surface is rendered  
* QTBUG-94331 Some examples do not work correctly on macOS  
  
### qtvirtualkeyboard  
* QTBUG-94017 Cursor position moves when un-converted Japanese is  
deleted  
* QTBUG-68412 tst_plugin::test_pinyinInputMethod crashes on arm  
* QTBUG-94715 Qt Virtualkeyboards support for Chinese language doesn't  
work properly  
* QTBUG-95664 VirtualKeyboardSettings: Readonly property is not marked  
as such  
* QTBUG-95893 Missing documentation for dictionary API  
* QTBUG-94017 Cursor position moves when un-converted Japanese is  
deleted  
  
### qtquicktimeline  
* QDS-3216 Flickering when using default value as implcit first keyframe  
  
### qtquick3d  
* QTBUG-95212 Error when empty scene is loaded  
  
### qtcoap  
* QTBUG-94763 [CoAP] When resource is observed the QT CoAP client sends  
an acknowledgement packet which is not empty.  
  
### qtopcua  
* QTBUG-86726 qt_add_resource BASE argument doesn't behave as the qmake  
counterpart  
  
Known Issues  
------------  

* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-6/gettingstarted.html#platform-requirements  
* RTA reported issues from Qt 6.1  
https://bugreports.qt.io/issues/?filter=22879  
* Supported development platforms are listed here:  
https://bugreports.qt.io/browse/QTBUG-86432  
  
### Linux
* Minimum glibc version for prebuild binaries is still 2.28, see  
https://bugreports.qt.io/browse/QTBUG-88833.  
Workaround: compile Qt 6.1.2 by yourself or update glibc to 2.28 or newer  
  
### Windows
* Wrong rendering in Dialog with native Windows style  
https://bugreports.qt.io/browse/QTBUG-91755  
    
Credits for the  release goes to:  
---------------------------------  
  
Aavitsland Eirik  
Achtelik Mike  
Agocs Laszlo  
Blomfeldt Eskil Abrahamsen  
Bornemann Joerg  
Boudjelthia Assam  
Buddenhagen Oswald  
Croitor Alexandru  
Curtis Mitch  
D'Angelo Giuseppe  
Edelev Alexey  
Eftevaag Oliver  
Ehrlicher Christian  
Fella Nicolas  
Frantzis Alexandros  
Golubev Andrei  
Haixiang Tang  
Halmet Heikki  
Hartmann Thomas  
Heikkinen Jani  
Hermann Ulf  
Hilsheimer Volker  
Holland Dominik  
Jenssen Tim  
Jokiniva Jukka  
Jung Jaeyoon  
Karlsson Jonas  
Katz Jeremy  
Kittler Marius  
Kleint Friedemann  
Koh Sze Howe  
Koivikko Jarkko  
Korpipaa Tomi  
Kosmale Fabian  
Krus Mike  
Kurazyan Sona  
Kvinge Jonas  
Köhne Kai  
Lemire Paul  
Löhning Robert  
Mutz Marc  
Nishihara Yuya  
Nordheim Mårten  
Pocheptsov Timur  
Qi Liang  
Rocha André de la  
Rutledge Shawn  
Sera Luca Di  
Shao Tianlu  
Shaw Andy  
Shivashankar Venugopal  
Solovev Ivan  
Suzuki Tasuku  
Sæther Jan Arve  
Sørvig Morten Johan  
Tan Tyson  
Tkachenko Ivan  
Trotsenko Alex  
Varanka Sami  
Vertriest Nico  
Vestbø Tor Arne  
Volkov Alexander  
Welbourne Edward  
Wicking Paul  
Xinwei Li  
Zhang JiDe  
