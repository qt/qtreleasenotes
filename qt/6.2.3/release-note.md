Release note  
============  
  
Qt 6.2.3 release is a patch release made on the top of Qt 6.2.2.  
As a patch release, Qt 6.2.3 does not add any new functionality but provides  
bug fixes and other improvements and maintains both forward and backward  
compatibility (source and binary) with Qt 6.2.2.  

For detailed information about Qt 6.2, refer to the online documentation  
included in this distribution. The documentation is also available online:  
  
https://doc.qt.io/qt-6/index.html  
  
The Qt version 6.2 series is binary compatible with the 6.1.x series.  
Applications compiled for 6.1 will continue to run with 6.2.  
  
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
* fa2197202a Do not include qloggingcategory.h in public headers  
The qguiapplication.h header no longer implicitly includes  
qloggingcategory.h. If your code depends on the transitive include,  
explicitly include <QLoggingCategory> where needed.  
  
* c13101b0b3 Fix deserializing Qt 5.x fonts through QDataStream  
Fixed a problem deserializing the family of fonts that had been  
serialized using QDataStream in Qt 5.  
  
* 5d344408cc QAnyStringView: fix broken implicit conversion from  
QStringBuilder  
Implicit conversion from QStringBuilder to QAnyStringView now works as  
advertised.  
  
* 03274775ec QImageReader: check allocation limit for minimum 32 bpp  
When checking allocation limit during image reading, the memory  
requirements are now calculated for a minimum of 32 bits per pixel,  
since Qt will typically convert an image to that depth when it is used  
in GUI. This means that the effective allocation limit is significantly  
smaller when reading 1 bpp and 8 bpp images.  
  
* b55957b904 QObject: don't #include qproperty.h  
The qobject.h header no longer implicitly includes qproperty.h. If your  
code depends on the transitive include, explicitly include <QProperty>  
where needed.  
  
* ac9cc22c09 QVERIFY_EXCEPTION_THROWN: re-throw unknown exceptions  
Now re-throws unknown exceptions (= not derived from std::exception)  
(was: swallowed them and returned from the test function), in order to  
play nice with pthread cancellation.  
  
* 440a87248e QSharedPointer: fix counter-productive QT_PREPEND_NAMESPACE  
use in qHash() impl  
The qHash(QSharedPointer<X>) overload can now use qHash(X*) overloads  
found (only) through ADL (was: ADL was disabled due to qualified lookup  
of qHash(X*)).  
  
* 150a897a83 Fix gaps between lines of selection  
Fixed an issue where there would sometimes be visible gaps in  
selections spanning multiple lines.  
  
* f622090b1d QNAM: Disable h2c by default  
Support for clear-text http/2 was disabled due to incompatibility with  
certain servers. If you were relying on this feature you must re-enable  
it by setting the QT_NETWORK_ALLOW_H2C environment variable. For a later  
version of Qt it will get a dedicated attribute.  
  
* 669b454378 Add _make_aab target  
Add the extra _make_aab targets for each executable target, that can be  
used to generate android app bundles. Also add aab metatarget to build  
all _make_aab targets that are created in the project.  
  
* ec613a4649 Fix overlapping text for Osaka font on macOS  
Fixed a problem where using the Osaka font would lead to overlapping  
text.  
  
* 9a9d960b12 QFuture: support cancellation of continuation chain through  
parent  
The chain of continuations attached to a future now can be cancelled  
through cancelling the future itself at any point of the execution of  
the chain, as it was documented. Previously canceling the future would  
cancel the chain only if it was done before the chain starts executing,  
otherwise the cancellation would be ignored. Now the part of the chain  
that wasn't started at the moment of cancellation will be canceled.  
  
* 46599ec418 Fix missing characters or assert with certain font sizes  
Fixed an issue where characters would in some rare cases be missing  
from text, depending on font metrics, font size and system scale factor.  
  
* 3bf23b7118 Don't change resolve mask when setting brush doesn't change  
palette  
Setting a brush on a palette that is identical to the current brush no  
longer sets the resolve mask bit for that particular role, so items  
using the palette will continue to inherit changes from parent items.  
  
* 82e965c35e QVarLengthArray: fix size update on failed append()  
Fixed a bug whereby a failed append() would leave the container with an  
inconsistent size().  
  
* 52c9543475 QVarLengthArray: fix UB (precondition violation) in range-  
erase()  
Fixed a bug where range-erase() could invoke undefined behavior when  
called with an empty range.  
  
* c721dff3f3 Trust CoreText-provided vertical metrics on macOS  
Fixed an issue where certain fonts, such as Monaco, would have a  
different line spacing than expected.  
  
* b05c9898cc QList: fix typo in QList(It, It)  
Fixed a regression that caused the range constructor to fail for pure  
input_iterator's.  
  
* 4e669763bd QVarLengthArray: widen append(p, n)'s contract  
The counted-range-append() function (append(ptr, n)) now accepts ptr ==  
nullptr, provided n == 0, too (was: triggered assertion).  
  
* f3842c09b7 QVariant: use a typedef name when saving user types to  
QDataStream  
If QDataStream is used with a QDataStream::Version < Qt_6_0 to  
serialize a user type that was registered via a typedef with the  
metatype system, the typedef's name is used in the stream instead of the  
non-typedef name. This restores compatibility with Qt 5, allowing  
existing content to read the same QDataStreams; reading from older Qt 6  
versions should not be affected. (Note: if more than one typedef name is  
registered, it's indetermine which name gets used)  
  
* 0952ec8a5f QStringBuilder: fix quadratic behavior in op+=  
Fixed quadratic behavior when repeatedly appending string-builder  
expressions (using operator+=) to QString/QByteArray objects.  
  
* 7f3ca223a6 QTestData: fix streaming of u8 string literals in C++20  
mode  
Fixed streaming of u8 string literals in C++20 mode.  
  
* 60f3d7f324 QByteArray: avoid detach() in a no-op replace()  
A replace(pos, n, after) call no longer detach()es when n ==  
after.size() == 0.  
  
* 3d446c236a SQLite: Update SQLite to v3.37.0  
Updated SQLite to v3.37.0  
  
### qtdeclarative  
* 72402a9160 Fix missing glyphs when changing distance field parameters  
Fixed an issue where glyphs would sometimes be missing when changing  
the environment variables that define how distance fields are generated  
to certain values.  
  
* 9e6274e180 qquickdeliveryagent: Fix drag events being sent in the  
wrong order  
Now sends DragArea leave events before enter events when appropriate  
(QTBUG-82263)  
  
* db9adec4b1 Fix focus for items inside a QQuickWidget in a  
QGraphicsProxyWidget  
  
  
* 0798e34ce6 Make atlasing of compressed textures opt-in again  
Disable atlasing of compressed textures by default. Can be enabled with  
QSG_ENABLE_COMPRESSED_ATLAS=1  
  
### qtwayland  
* 048f4317 Don't build XComposite buffer integration by default  
  
  
### qtlottie  
* d234a3c Fix loading of LottieAnimation::source  
Fixed bug that prevented LottieAnimation from loading its source from a  
relative URL.  
  
  
Fixes  
-----  
  
### qtbase  
* QTBUG-98099 Crash on exit with Application font and QFontComboBox  
* QTBUG-97908 Regression: PageUp and PageDown don't work in QScrollArea.  
* QTBUG-90352 Page Up/Page Down do not work in QTextBrowser  
* QTBUG-26269 QScrollArea: The viewport bleeds through another widget  
when the scroll bar is reset.  
* QTBUG-98093 QSlider is broken in MacOS Monterey  
* QTBUG-97995 Error deserializing QFont (from 5.15 to 6.2)  
* QTBUG-98377 QImage::reinterpretAsFormat wrong reference counting when  
out of memory  
* QTBUG-98403 tst_QPainter fails with macOS 12 x86 in developer build  
tests  
* QTBUG-98388 Vertical QPainter::drawLine() result on QWidget is skewed  
* QTBUG-97490 Static Build is unable to find QPrinter::NativeFormat  
* QTBUG-98137 Disabled button in QDialogButtonBox gets focus by Tab  
* QTBUG-98138 QAnyStringView argument doesn't accept QStringBuilder  
* QTBUG-95933 Using scanner input IRcode will result in an error when  
second character is uppercase  
* QTBUG-98280 QAuthenticator doesn't check if algorithm is supported  
* QTBUG-94036 tst_QAccessibilityMac::notificationsTest() fails  
* QTBUG-96405 setGraphicsApi :OpenGLRhi.  QML application resizing  
flickers and is sometimes blank  
* QTBUG-98286 Reg->Qt 6: QToolButton with style sheet : There are two  
Tool button arrows rendered  (all styles)  
* QTBUG-98544 Combination of 'HangulInputMethod' and 'QGraphicsTextItem'  
does not work as expected.  
* QTBUG-98372 Regression Qt5 > Qt6: Visible gaps between selected lines  
* QTBUG-98770 QList<T>::count(const T&) triggers undefined behavior  
sanitizer when list is empty  
* QTBUG-98289 QTableView : The last column/row is hidden by scrollbar  
when stylesheet is used.  
* QTBUG-92521 WASM: QToolTips occasionally makes app exception  
* QTBUG-91691 [REG: 5.15.0->5.15.1] QTextDocument tables with colspan  
collapses the starting column to minimum size  
* QTBUG-95240 QTextTabel: column width changes when merging other rows  
* QTBUG-97431 WASM - Tumbler does not work good/at all  
* QTBUG-92037 QMdiArea  setActiveSubWindow sublist.at(0) failed if  
setViewMode(QMdiArea::TabbedView);  
* QTBUG-96710 CMake isn't exposing an aab target for Android projects  
* QTBUG-96880 New line is ignored with Osaka font  
* QTBUG-98493 Using copy-restricted class in lambda for QFuture's  
then(), does not build  
* QTBUG-86372 [xcb] WindowTransparentForInput causing problems with  
resizing  
* QTBUG-98578 Documentation of qabstractnativeeventfilter  
* QTBUG-86633 QML - letters randomly disappear when resizing label  
* QTBUG-86671 Table cells overlap with image and relative width  
* QTBUG-97463 Showing Large image in QTextBrowser table overlaps  
* QTBUG-98444 QTableView, Deselecting column by [ctrl + click] on  
horizontal header only works when the first row is visible  
* QTBUG-98532 CMake - _qmltyperegistration.cpp do not get updated  
* QTBUG-98752 QFontDatabase::addApplicationFontFromData does not mention  
OpenType being supported  
* QTBUG-62602 Underline is displayed outside the text box  
* QTBUG-97649 androiddeployqt exits with signing if the path contains  
spaces  
* QTBUG-98504 QSystemTrayIcon example: selecting Quit from context menu  
shows unnecessary message  
* QTBUG-98762 REGRESSION: QPalette::setBrush does not reliably detach  
* QTBUG-65475 Application palette changes at runtime do not work for all  
widgets  
* QTBUG-98654 QX11Application: No such file  
* QTBUG-98875 QMouseEvent source() vs pointingDevice() unclear in  
documentation  
* QTBUG-82455 QTextDocument::contentsChange(int,int,int) values are  
incompatible with QTextCursor  
* QTBUG-72776 QKeyEvent key() only returns value of first surrogate for  
characters in Supplementary Planes  
* QTBUG-58995 [REG 5.7->5.8][Windows]: When using Courier with a large  
pixel size then it will show up as 13 points regardless  
* PYSIDE-1720 piside6-uic convert signal clicked(bool) to clicked  
* QTBUG-95192 Segmentation fault at application closing  
* QTBUG-80653 Keyboard LED states do not change with evdev keyboard  
* QTBUG-98726 CMake code for locating latest android.jar in Android SDK  
is incorrect  
* QTBUG-68636 Some popups (i.e.) menus are misplaced on gnome-shell  
* QTBUG-98856 Wrong cursor showing when restoreOverrideCursor in  
QDockWidget  
* QTBUG-95096 Qt 6's new and improved QList fails its removeAll  
benchmarks  
* QTBUG-94995 Changed QML files do not updated on device  
* QTBUG-98943 QMultiHash recursive emplace on VS2019  
* QTBUG-97818 Huge line spacing when font is Monaco  
* QTBUG-99036 [REG 5.15 → 6.3] QList(It, It) no longer works with pure  
input_iterators  
* QTBUG-97699 Building projects with static Qt (debug):  
qrc_openglblacklists.cpp.obj : warning LNK4099: PDB 'vc140.pdb' was not  
found with 'qrc_openglblacklists.cpp.obj'  
* QTBUG-92501 QtFuture::connect includes Q*::QPrivateSignal as one of  
the arguments  
* QTBUG-98843 Qt 6.2.2 Windows build fail  
* QTBUG-96463 [REG 5.15.2-6.2.0] Text with BIDI controls is underlined  
incorrectly  
* QTBUG-99165 cmake doesn't complain with android-30, but fails with  
unknown API S (ie android-31)  
* QTBUG-99223 CMake Error: File  
C:/Users/qt/work/install/lib/cmake/Qt6/qt_setup_tool_path.bat.in does  
not exist.  
* QTBUG-97752 QHash: non-readonly iteration access destroys iterator  
* QTBUG-96916 Qt 6 breaks compatibility of QVariant streaming into  
QDataStream  
* QTBUG-81503 qtbase contains code that isn't allowed to be distributed  
* QTBUG-98901 QtConcurrent::run crashes on program exit  
* QTBUG-99163 QTransform rotate big image will crash  
* QTBUG-99280 Splash screen appears on top model dialog with dynamic vs  
behind with static  
* QTBUG-99330 qdoc: Crash at QString::operator+=()  
* QTBUG-99186 uncaught exeption takes down app  
* QTBUG-99319 QApplication crash on second run when mouse roll over  
window  
* QTBUG-99371 QWidget::customContextMenuRequested coordinates are off  
for widgets in a QMenu  
* QTBUG-99147 <!---->  
* QTBUG-99413 QSysInfo::productType() incorrectly documented  
* COIN-777 *** Could not find any device matching '--platform iOS  
--minimum-deployment-target  
* QTBUG-63695 QStandardPaths does not document locations for QNX  
* QTBUG-99316 Yocto build fails in CI for qtdeclarative-native dev/6.3  
branch  
* QTBUG-99416 QT6 qtbase build fails claiming symlinks are present  
* QTBUG-99148 Broken html list rendering because <code> element  
* QTBUG-97841 MacOS Monterey - scrolling issues with touch pad  
* QTBUG-99623 Dependency update on qt/qtopcua failed in 6.3  
* QTBUG-99408 [SQL] The SQL driver for Firebird/Interbase does not  
unpack the QVariant before null check  
* QTBUG-98471 [REG: 5->6.2.1] Null QDateTime is not stored as NULL  
anymore in Oracle OCI  
* QTBUG-99710 Regression: QCache crash  
* QTBUG-99224 Crash in QPixmapCache  
* QTBUG-99240 Crashing in trimming QPixmapCache  
* QTBUG-99668 Using QDateTime with QTimeZone specified asserts in debug  
build  
* QTBUG-97601 Compilation speed decrease with Qt 6.2 compared to Qt  
5.15.2  
* QTCREATORBUG-26581 Multicursor mode enables during the selection  
without pressing "Alt"  
* QTBUG-97842 Move Android tools docs from qtdoc to qtbase  
* QTBUG-97115 When an application that is using a background service is  
closed then it will cause an ANR after hanging for about 30 seconds  
* QTBUG-95795 Crash when running a qt quick app on iOS simulator  
* QTBUG-98569 Error in meta-b2qt for Windows Toolchain  
* QTBUG-98653 QStringView::split returns invalid data  
* QTBUG-98642 Qml/QmlScene : malformed http request when opening a qml  
file over http with qml/qmlscene  
* QTBUG-93037 Conan builds are unable to run tst_qmake  
* QTBUG-97582 QFuture::cancel through then()/onCanceled/onFailed  
* QTBUG-98649 Qt Android creates View IDs in a way potentially leading  
to a collision  
* QTBUG-75862 FocusReason is broken in Controls 2  
* QTBUG-96957 Created output file is in inncorrect type and in different  
location  
* QTBUG-92231 SSL handshake failure after ignoreSslErrors  
* QTBUG-98151 Widgets over a QMdiArea are not repainted correctly  
* QTBUG-98561 Creating directory using symbolic link in path fails on  
QNX  
* QTBUG-89285 Document changes to State Machine Framework in Core  
Migration Guide  
* QTBUG-95237 [REG 6.0.4 -> 6.1.0] Integer-overflow in  
QFixed::operator+= through QImage::loadFromData(QByteArray)  
* QTBUG-98483 [macOS] QPushButton is broken in macOS Monterey  
* QTBUG-98937 KTX, ASTC image not displayed on Qt 6.2 and above  
* QTBUG-99615 Most QMutableEventPoint usage depends on Undefined  
Behaviour  
  
### qtsvg  
* QTBUG-98139 QSvgRenderer::boundsOnElement does not properly calculate  
the bounding box of a text when it has a transformation  
* QTBUG-99407 [REG 6.1.3  -> 6.2.0] Loading svg file takes too long  
  
### qtdeclarative  
* QTBUG-91886 Inconsistence in material style checked highlighted button  
* QTBUG-86453 Instantiator creates delegates when active is false if  
items are dynamically added to a ListModel  
* QTBUG-88331 Instantiator creates delegate when active is false and  
delegate is updated  
* QTBUG-97927 Focus frame placed in the wrong position after window  
resize  
* QTBUG-97914 Broken test tst_QQuickListView2::dragDelegateWithMouseArea  
* QTBUG-98440 TableView selectionModel property is not available in  
Quick 2.2  
* QTBUG-98469 tst_qqmllanguage::hangOnWarning() Not all expected  
messages were received  
* QTBUG-98468 CMake Error: AUTOMOC for target affectors_shared: The  
"moc" executable "/Users/qt/work/qt/qt5/qtbase/libexec/moc" does not  
exist  
* QTBUG-98248 SEGFAULT Crash in QQmlAnimationTimer::registerAnimation  
* QTBUG-95633 QQmlEngine::offlineStoragePath() documentation needs link  
to openDatabase()  
* QTBUG-98311 QML bitwise 'or' operator is not evaluated correctly when  
initializing C++ property and both operands are enum values  
* QTBUG-59223 tst_qqmlxmlhttprequest::send_options fails with  
LANG=de_DE.UTF-8  
* QTBUG-97782 Material SpinBox QML TypeErrors  
* QTBUG-58416 QtQuick Image: SVG Images are not properly scaled with  
High DPI Scaling  
* QTBUG-81018 Image sourceSize binding causes the size to become smaller  
unexpectedly  
* QTBUG-96147 qmlsc does not understand curly braced grouped properties  
* QTBUG-98017 QSGRhiTextureGlyphCache::createEmptyTexture() nullptr  
access crash  
* QTBUG-98742 qt6_target_qml_sources() doesn't ensure PREFIX argument  
starts with "/"  
* QTBUG-84196 Crash when calling QQmlEngine::retranslate  
* QTBUG-98792 Crash when using as-cast  
* QTBUG-82263 [REG: 5.13->5.14]: QML DropArea wrong signals order  
* QTBUG-97461 [REG 5.15.2->6.2] DragHandler does not work when there's a  
Drawer in the application  
* QTBUG-98844  [REG 6.1.0->6.1.1] DragHandler inside Dialog does not  
work  
* QTBUG-98482 RangeSlider does not update position/visualPosition based  
on from/to changes  
* QTBUG-97541 qt_add_qml_module does not properly handle singleton qml  
files  
* QTBUG-98811 FAIL!  :  
tst_qqmlxmlhttprequest::setRequestHeader_illegalName(Referer) Received a  
fatal error.  
* QTBUG-98830 qmlsc confuses precedence between properties and IDs  
* QTBUG-98717 Setting HoverHandler cursorShape in a Window crashes  
* QTBUG-75862 FocusReason is broken in Controls 2  
* QTBUG-71723 When showing a context menu for a TextField then it will  
lose the selection instead of keeping it  
* QTBUG-36332 QtQuick Controls: actions which depend on activeFocusItem  
are disabled when a menu is shown  
* QTBUG-91479 When a TextField is inside a QQuickWidget that is in a  
QGraphicsProxyWidget then clicking the TextField will not give it focus  
and as such it is not possible to type in it  
* QTBUG-98127 Weighted layout behavior is not documented  
* QTBUG-98730 Slider with negative width crash the application  
* QTBUG-98356 JIT crash on invalid yield syntax  
* QTBUG-98747 close.accepted behavior  
* QTBUG-94765 AnimatedSprite has glitches  
* QTBUG-99025 Property "hasOwnProperty" not found on type "Item"  
* QTBUG-98367 Segmentation fault with Binding on font.bold  
* QTBUG-75799 Strange flickering when restarting an animation with  
PauseAnimation and ScaleAnimator  
* QTBUG-98937 KTX, ASTC image not displayed on Qt 6.2 and above  
* QTBUG-99113 qmlsc confuses ambiguous types in the same module  
* QTBUG-99275 agent:2021/12/16 18:36:00 build.go:394: FAILED:  
tests/auto/quickcontrols2/controls/basic/tst_basic  
* QTBUG-86533 Yocto and QNX builds are missing -rpath-link linker flag  
which causes non-prefix builds to fail  
* QTBUG-96888 Not possible to quickly click buttons  
* QTBUG-49049 arcTo doesn't always get drawn  
* QTBUG-99529 Touchpad scrolling list overshoot is buggy  
* QTBUG-99400 [Reg 5.2 -> 5.3] qmlplugindump: error details missing on  
linux  
* QTBUG-98130 QtQuick and controls examples use qt_add_resources to add  
QML files  
* QTBUG-98402 tst_qquickimage::mirror() is failing on macOS 12  
* QTBUG-86044 When a ListView is removing items with a transition and  
there is delay remove used then when the last item is removed the footer  
does not go to the top of the view  
* QTBUG-97423 heap-use-after-free in SwipeView::test_orientation  
* QTBUG-98722 SignalSpy.qml triggers a memory leak in the QML engine  
* QTBUG-86633 QML - letters randomly disappear when resizing label  
* QTBUG-98492 tst_HoverHandler::mouseAreaAndUnderlyingHoverHandler and  
tst_HoverHandler::hoverHandlerAndUnderlyingMouseArea are flaky on macos  
* QTBUG-99214 Tests that rely on QProcess with the main app lib fail on  
Android  
* QTBUG-57098 Popup's CloseOnEscape policy prevents escape key from  
being used without closing the popup  
* QTBUG-99367 Custom ScrollBar style not used after upgrade from 5.15 to  
6.2  
* QTBUG-99615 Most QMutableEventPoint usage depends on Undefined  
Behaviour  
* QTBUG-99608 tst_qmlcachegen (Failed)  
  
### qtmultimedia  
* QTBUG-97758 QAudioOutput::setDevice doesn't work in Linux  
* QTBUG-98124 Qt Multimedia has an unnecessary dependency to libwayland-  
dev when Qt is configured without Wayland.  
* QTBUG-97080 Wrong video preview orientation on landscape  
* QTBUG-97861 QSoundEffect stop not working  
* QTBUG-97828 Add support for gapless/seamless playback in Qt6  
* QTBUG-97815 QCamera ::setVideoOutput is removed but documentation  
still refers it  
* QTBUG-98559 QtMultimedia Camera Not View on Android 10  
* QTBUG-97909 Implement MediaPlayer Buffering Listener  
* QTBUG-98262 MediaRecorder.stop() does not work on macOS 10.15  
(Catalina)  
* QTBUG-98860 Crash during media capture with OpenGL-based rhi  
* QTBUG-98191 QMediaPlayer position reported incorrectly for flac files  
after a seek  
* QTBUG-98306 [REG][macOS] Video orientation is broken  
* QTBUG-99011 QMediaFormat::supportedFileFormats return value is  
incomplete  
* QTBUG-96946 Part of the app greyed out while recording is on  
* QTBUG-97780 Video object does not throw an error when source path is  
not resolved  
* QTBUG-99142 QtMultimedia: Invalid target given to  
qt_is_imported_target: Qt6::QSGVivanteVideoNodeFactory  
* QTBUG-99129 Android media player isSeekable() always returns true  
* QTBUG-99181 Fix loadMediaInLoadingState test  
* QTBUG-99183 Fix processEOS test in Android  
* QTBUG-99182 Fix unloadMedia test  
* QTBUG-99210 Fix playPauseStop test in Android  
* QTBUG-99134 Declarative Camera issues on video  
* QTBUG-99296 Crash when recording audio-only after video recording  
* QTBUG-99176 Recorder example: Crash when switching audio input off  
* QTBUG-96985 Video and MediaPlayer don't allow to use relative URLs  
* QTBUG-97817 Camera example doesn't work  
* QTBUG-99358 Fix SurfaceTest Test in Android  
* QTBUG-99359 Fix Metadata Test in Android  
* QTBUG-99360 Fix audioVideoAvailable Test in Android  
* QTBUG-96202 SoundEffect does not work in Qt6.2 beta3 in Windows and  
Linux  
* QTBUG-96599 No documentation for how to support different video  
formats  
* QTBUG-98419 [macOS] Audio Recorder example crashes on start on macOS  
10.15 (Catalina)  
  
### qttools  
* QTBUG-97380 tst_lupdate fails with Windows 10 21H1 and Windows 11 21H2  
* QTBUG-98916 Qt Designer sets font family which was set to something  
else in ui file to Segeo UI  
* QTBUG-46322 When setting a family name that has a comma in the name it  
will not match the font correctly  
* QTBUG-99232 REG->6.3: Linguist occasionally asserts  
* QTBUG-99404 Qt Designer: Crash when editing spacer objectName in the  
Object Inspector Tab  
* QTBUG-99409 qdoc: Trailing newline in the master .qdocconf fails the  
build.  
  
### qtdoc  
* QTBUG-98327 qt6 doc error  
* QTBUG-98773 Documented default for libexec in qt.conf is wrong for  
Windows  
* QTBUG-99167 XML support in Qt talks about XML Pattern  
* QTBUG-97842 Move Android tools docs from qtdoc to qtbase  
* QTBUG-96785 "Getting Started with Qt for Android" documentation needs  
an update  
  
### qtpositioning  
* QTBUG-97705 PositionSource doesn't stay active nor start on initial  
property values  
* QTBUG-98780 error: use of undeclared identifier 'lcPositioning'  
* QTBUG-99329  
org.qtproject.qt.android.positioning.QtPositioning.positionUpdated calls  
non-existent method  
  
### qtsensors  
* QTBUG-98737 Dependency update to qt/qtsensors failed  
  
### qtconnectivity  
* QTBUG-98323 Assertion failure when running bluetooth/btchat example  
* QTBUG-98353 QBluetoothSocket.connectToService failing on Android  
devices with a java error  
* QTBUG-96742 Timing issues in BTLE peripheral on Android  
* QTBUG-96743 BTLE on Android: Characteristic supposed to support both  
Notification and Indication supports neither  
* QTBUG-98719 QBluetoothSocket deletion occasionally crashes on Windows  
* QTBUG-98582 QT Bluetooth LE crashed when connect/disconnect to a  
device  
* QTBUG-98878 Bluetooth LE characteristic Indication manual test fails  
on darwin server  
* QTBUG-97900 Crash when connecting to Bluetooth device on macOS 12  
* QTBUG-96557 Qt bluetooth can not scan device on Mac 12 beta  
* QTBUG-97578 QT Bluetooth hang when scan services/characterictics  
* QTBUG-98781 BT LE test case platform support enhancement  
* QTBUG-98955 tst_QBluetoothServiceInfo::tst_assignment fails on macOS  
12 ARM  
* QTBUG-98351 Thread-safe Android BT LE Java implementation  
* QTBUG-99222 Re-enable Bluetooth autotests on macOS  
  
### qtwayland  
* QTBUG-98010 Screen information unavailable on Wayland  
* QTBUG-98897  error: ‘QWaylandOutput* QWaylandOutputPrivate::q_func()’  
is private within this context  
* QTBUG-95962 Wayland: Crash in XDG Shell when resizing window with  
mouse  
* QTBUG-90530 Low resolution title bar icon on Wayland on Hi DPI  
displays  
* QTBUG-95032 Dialogs on Wayland/Sway not drawn correctly when using  
client side decorations  
* QTBUG-97985 Wayland: XComposite backend does not update surfaces  
properly  
* QTBUG-97950 Application slowly reads every file in /usr/bin before  
starting  
  
### qt3d  
* QTBUG-95439 Qt 3D Planets arm64-v8a example  "Invalid minSdkVersion  
version, minSdkVersion must be >= 23"  
* QTBUG-97254 Pugixml workaround for QTBUG-11923 causes C1001 in  
MSVC2019 with PCH  
* QTBUG-98097 Qt3D license only GPL or Commercial?  
* QTBUG-97950 Application slowly reads every file in /usr/bin before  
starting  
* QTBUG-98420 Configure failure with system assimp  
  
### qtserialbus  
* QTBUG-98800 [PeakCAN] Incorrect QCanBusFrame::TimeStamp conversion  
* QTBUG-96566 Serialbus can example fails to build  
  
### qtserialport  
* QTBUG-98735 C:/Users/qt/work/install/include/QtCore/6.3.0/QtCore\priva  
te/qobject_p.h:497:78: error: 'q_func' is a private member of  
'QSerialPortPrivate'  
  
### qtwebengine  
* QTBUG-97836 QtWebEngineCore still not compiling from source  
* QTBUG-97926 QWebengine can not play the  embeded vimeo video  
* QTBUG-97472 [REG] Crash/segfault in ozone implementation when calling  
XkbGetState  
* QTBUG-92539 Weird behavior when pasting certain HTML into element with  
contentEditable attribute set  
* QTBUG-90904 Crash on calling QAccessible::registerAccessibleInterface  
* QTBUG-98400 CVE-2021-3541 in chromium  
* QTBUG-98401 CVE-2021-3517 in chromium  
* QTBUG-71277 Nanobrowser example has confusing project layout  
* QTBUG-98918 [REG] recentlyAudible does not implement 2s cooldown  
anymore  
* QTBUG-97414 tst_CertificateError::fatalError()  
'!page.error->isOverridable()' returned FALSE.  
* QTBUG-99511 Top level cross build fails  
* QTBUG-99526 developer tools no longer highlights page elements when  
inspecting them  
* QTBUG-99263 QProcess::finished not emitted  
* QTBUG-99215 Html popups do not work correctly.  
* QTBUG-98941 [Qt5.15.4][QWebEngine]QWebEnginePage::print() function  
printing a grey paper while printing a PDF in Qt5.15.4  
  
### qtwebview  
* QTBUG-99372 FAILED: tests/auto/webview/qwebview/tst_qwebview  when  
builing for QNX  
* QTBUG-86533 Yocto and QNX builds are missing -rpath-link linker flag  
which causes non-prefix builds to fail  
  
### qtcharts  
* QTBUG-98282 QPieSlice label does not indicate it takes html formatted  
text  
* QTBUG-99044 [REG Qt5 -> Qt6.2]: Chart with QLineSeries and  
QScatterSeries does not receive mouse events  
  
### qtvirtualkeyboard  
* QTBUG-97439 [REG 5.15.2->6.2] Virtual Keyboard is hidden by QML dialog  
  
### qtscxml  
* QTBUG-98738  
/Users/qt/work/qt/qtscxml/src/statemachineqml/state_p.h:92:66: error:  
unknown type name 'm_childrenComputedProperty'  
  
### qtremoteobjects  
* QTBUG-97704 POD type replication issue  
* QTBUG-99269 tst_Integration_External test is failing on MacOS-arm64  
  
### qtlottie  
* QTBUG-98794 LottieAnimation::source not loaded in Qt 6  
  
### qtquick3d  
* QTBUG-98342 View3D mapping functions do not work correctly with  
orthographic camera and 2x pixel ratio  
* QTBUG-98330 Particlesystem keeps updating particles even when not  
visible  
* QTBUG-98583 R32F QQuick3DTextureData does not work  
* QDS-3025 Adding a spotlight under another node that is not in global  
origin places the light gizmo to global origin in 3D view  
* QTBUG-99012 Scene rendering getting slower per QQuick3DGeometry  
updates  
* QTBUG-97254 Pugixml workaround for QTBUG-11923 causes C1001 in  
MSVC2019 with PCH  
* QDS-5064 Instances created by using XML files are not visible in Form  
Editor  
* QTBUG-98749 Application crashes if there are more then 8 light sources  
* QTBUG-97925 ProgressiveAA does not work if there are  
PrincipledMaterials in scene  
* QTBUG-98748 TriangleFan primitive type can't be used [should handle  
this more gracefully and print a warning]  
* QTBUG-98756 U16Type doesn't work for joint indexes  
* QTBUG-98111 Particle emitter bursts do not work with animated emitter  
* QDS-5552 Long delay before emitting after particle system is rewinded  
* QTBUG-98420 Configure failure with system assimp  
* QTBUG-97857 Item2D shouldn't be always pickable  
* QTBUG-99615 Most QMutableEventPoint usage depends on Undefined  
Behaviour  
  
Known Issues  
------------  
  
* Check that your system meets Qt's requirements:  
https://doc.qt.io/qt-6/gettingstarted.html#platform-requirements  
* RTA reported issues from Qt 6.2  
https://bugreports.qt.io/issues/?filter=23315  
* Supported development platforms are listed here:  
https://bugreports.qt.io/browse/QTBUG-90021  
* See Qt 6.2 Known Issues from:  
https://wiki.qt.io/Qt_6.2_Known_Issues  
  
Credits for the  release goes to:  
---------------------------------  
  
Aavitsland Eirik  
Agocs Laszlo  
Apostolou Dimitrios  
Astals Cid Albert  
Belyavsky Vladimir  
Bennett Nicholas  
Blechmann Tim  
Blomfeldt Eskil Abrahamsen  
Borisova Tatiana  
Bornemann Joerg  
Boudjelthia Assam  
Brüning Michael  
Buhr Andreas  
Burtsev Kirill  
Cieślak Michał  
Croitor Alexandru  
Curtis Mitch  
David Szabolcs  
Edelev Alexey  
Eftevaag Oliver  
Ehrlicher Christian  
Eklund Iikka  
ElKharashy Hatem  
Gaist Samuel  
Gehör Pekka  
Goldstein Maximilian  
Golubev Andrei  
Grulich Jan  
Grönholm Kaj  
Gustavsen Richard Moe  
Halmet Heikki  
Hao Zhang  
Hartmann Andre  
Hartmann Thomas  
Heikkinen Jani  
Heikkinen Miikka  
Hermann Ulf  
Hilsheimer Volker  
Jensen Allan Sandfeld  
Kleint Friedemann  
Klocek Michal  
Knoll Lars  
Kobus Jarek  
Koivikko Jarkko  
Kosmale Fabian  
Krus Mike  
Kurazyan Sona  
Köhne Kai  
Lee Inho  
Leinonen Tony  
Lemanissier Eric  
Lemire Paul  
Macieira Thiago  
Martinec Tamas  
Martinec Tamás  
Meshcheriakov Ievgenii  
Miettinen Leena  
Mira Samuel  
Mutz Marc  
Määttä Antti  
Neumärker Delf  
Nishihara Yuya  
Nordheim Mårten  
Paavoseppä Tinja  
Paeglis Gatis  
Petäjäjärvi Pasi  
Piippo Samuli  
Pocheptsov Timur  
Pohjanheimo Milla  
Pol Aleix  
Potinkara Rami  
Potter Lorn  
Qi Liang  
Rehn Arno  
Reinio Topi  
Rocha André de la  
Rutledge Shawn  
Saario Toni  
Schulz David  
Scott Craig  
Shachnev Dmitry  
Shao Tianlu  
Shaw Andy  
Shivashankar Venugopal  
Solovev Ivan  
Srebrny Piotr  
Strømme Christian  
Su Frank  
Sæther Jan Arve  
Sørvig Morten Johan  
Tkachenko Ivan  
Trillmann Jens  
Trotsenko Alex  
Tuliniemi Jere  
Tvete Paul Olav  
Varanka Sami  
Varga Peter  
Verria Doris  
Vestbø Tor Arne  
Volkov Alexander  
Vuolle Juha  
Wang ChunLin  
Welbourne Edward  
Wicking Paul  
Wolff Oliver  
Xuetian Weng  
Yu Zhang  
Zahorodnii Vlad  
Zhao Yuhang  
hjk hjk  
