Release note
============

Qt 6.5.8 release is a patch release made on the top of Qt 6.5.7.
As a patch release, Qt 6.5.8 does not add any new functionality but provides
bug fixes and other improvements and maintains both forward and backward
compatibility (source and binary) with Qt 6.5.7.
For detailed information about Qt 6.5, refer to the online documentation
included in this distribution. The documentation is also available online:

https://doc.qt.io/qt-6/index.html

The Qt version 6.5 series is binary compatible with the 6.4.x series.
Applications compiled for 6.4 will continue to run with 6.5.

Some of the changes listed in this file include issue tracking numbers
corresponding to tasks in the Qt Bug Tracker:

https://qt-project.atlassian.net/

Each of these identifiers can be entered in the bug tracker to obtain
more information about a particular change.

To make it easier to port to Qt 6, we have created a porting guide to
summarize those changes and provide guidance to handle them. In the
guide, you can find links to articles about changes that may affect your
application and help you transition from Qt 5.15 to Qt 6:

https://doc.qt.io/qt-6/portingguide.html

Important Changes
-----------------

### Security fixes

* Not applicable

### qtbase
* b3bb539dac7 Update to Harfbuzz 10.0.1
Updated Harfbuzz to 10.0.1.

* 8850092d716 SQLite: Update SQLite to v3.47.0
Updated SQLite to v3.47.0

* 2739e32191c moc: handle nested structs with meta content
Fixed a bug that caused moc to attempt to parse a nested struct (not
class) with meta keywords and this produced code that wouldn't compile.
Nested classes and structures are permitted, but must be defined outside
of the declaration of the outer class.

* 34c8ff0b6ac Remove assert in QImageTextureGlyphCache::fillTexture()
Fixed possible assert when transforming bitmap fonts.

* 1fa6d281f83 Freetype: Fix artificial oblique combined with other
transforms
Fixed an issue where artificially obliquened text would look incorrect
when other transformations were also applied and the Freetype backend
was in use.

* 14e7a804798 Upgrade to Harfbuzz 10.1.0
Upgraded Harfbuzz to version 10.1.0.

* 71818d08d0f Don't count overflowing inline image height to previous
line
Fixed an issue which could cause the height of a word-wrapped text line
to grow if the immediate line after it began with an inline image.

* 5d165a40a9f QCupsPrintEngine::setProperty(): defend against malformed
PPK_CupsOptions values
Fixed a bug where setting a value string-list with an odd number of
elements as the PPK_CupsOptions value would read uninitialized data.

* de1172f1407 Windows: Fix arbitrary outline on emojis
Fixed an issue where emojis would sometimes get an outline.

* c53a2f3ee5d SQLite: Update SQLite to v3.47.1
Updated SQLite to v3.47.1

### qtdeclarative
* caf8e0b596 QQuickItem: Correct coordinate conversion to QPointF
The function mapToItem(item, real x, real y) now returns a point with
real values instead of rounding to an integer.

* d974feafa5 QQmlComponent: Fix ordering of callbacks on
loadFromModule()
The QQmlParserStatus callbacks are invoked on objects loaded using
QQmlComponent::loadFromModule() at appropriate times now. You can rely
on any initial properties having been set before componentComplete() is
called and you can rely on the object having a valid QML context.

### qtmultimedia
* 1c413c06b Override the signal 'videoFrameChanged' in qml video sink
Removed QVideoFrame parameter from the not documented qml signal
VideoSink.videoFrameChanged.

* 0c1da9def Don't add file extension when the filename already has an
extension
QMediaRecorder::setOutputLocation and QImageCapture::captureToFile will
no longer alter the suffix/extension if the provided path already
includes an extension, even if this extension does not align with the
recommended extensions for the MIME type.

* 52ec2007b Make backend selection case insensitive
Backend selection using the QT_MEDIA_BACKEND environment variable is
now case insensitive.

* 64d572c84 Disable HW textures conversion by default on native Windows
backend
HW texture conversion (zero copy texture transfer) is disabled by
default with the native Windows media backend. Set the
QT_DISABLE_HW_TEXTURES_CONVERSION environment variable to '0' to re-
enable it.

* 371d4593f QCamera, docs: Update focusMode and focusDistance
documentation
focusDistance can now be applied without focusMode already being set to
FocusModeManual.

* e47816345 QCamera: Change QML manualExposureTime property type to
float
QML binding for QCamera::manualExposureTime has changed from type int
to float.


Fixes
-----

### qtbase
* [QTBUG-129434](https://qt-project.atlassian.net/browse/QTBUG-129434) [[Regr: 6.7.2 -> 6.7.3]] QTranslator::load finds
languages in wrong order
* [QTBUG-129509](https://qt-project.atlassian.net/browse/QTBUG-129509) (Regression) Erratic scrolling behavior using the mouse
in 6.7.3
* [QTBUG-129514](https://qt-project.atlassian.net/browse/QTBUG-129514) Reversed mouse buttons don't work properly on 6.7.3
* [QTBUG-110841](https://qt-project.atlassian.net/browse/QTBUG-110841)  [REG: 5.10.1->5.11.0-alpha] Mouse events not observed
when Super (Windows) key is held down.
* [QTBUG-128359](https://qt-project.atlassian.net/browse/QTBUG-128359) Right-click menu logic error
* [QTBUG-129398](https://qt-project.atlassian.net/browse/QTBUG-129398) QButtonGroup::addButton() doesn't guarantee negative ids
(as promised in docs)
* [QTBUG-129386](https://qt-project.atlassian.net/browse/QTBUG-129386) QProgressBar Windows style has changed for the chunks.
* [QTBUG-127596](https://qt-project.atlassian.net/browse/QTBUG-127596) Application crash on opening in ~QBindingObserverPtr()
* [QTBUG-129697](https://qt-project.atlassian.net/browse/QTBUG-129697) QT stopped understanding HTTP response compressed with
gzip.
* [QTBUG-91262](https://qt-project.atlassian.net/browse/QTBUG-91262) Qpainter draws text with gray edge on qimage
* [QTBUG-126187](https://qt-project.atlassian.net/browse/QTBUG-126187) HW Keyboard input is broken after touching UI
* [QTBUG-128731](https://qt-project.atlassian.net/browse/QTBUG-128731) macOS: Crash when disconnecting screen when app is in
fullscreen
* [QTBUG-124496](https://qt-project.atlassian.net/browse/QTBUG-124496) QObject::timerEvent may be called before the timer
elapsed
* [QTBUG-129596](https://qt-project.atlassian.net/browse/QTBUG-129596) Crash when closing inactive tab in tabbar for MDI window
* [QTBUG-130304](https://qt-project.atlassian.net/browse/QTBUG-130304) QDBusMessage::createMethodCall with a bad "service"
argument crashes in libdbus-1
* [QTBUG-123579](https://qt-project.atlassian.net/browse/QTBUG-123579) QLocale::toDatetime does not always work when it should?
* [QTBUG-116511](https://qt-project.atlassian.net/browse/QTBUG-116511) Android 11 and above setNativeLocks failed: "Function
not implemented"
* [QTBUG-129092](https://qt-project.atlassian.net/browse/QTBUG-129092) "OpenType support missing for..." Qt warnings
* [QTBUG-130056](https://qt-project.atlassian.net/browse/QTBUG-130056) Fail to link after qt_add_translations added to
CMakeLists.txt
* [QTBUG-130720](https://qt-project.atlassian.net/browse/QTBUG-130720) Typo on enum QStyle::StyleHint
* [QTBUG-124003](https://qt-project.atlassian.net/browse/QTBUG-124003) xcb: Mouse enter event is no longer delivered when mouse
leaves windows with pressed button
* [QTBUG-124898](https://qt-project.atlassian.net/browse/QTBUG-124898) [Reg 6.2 -> 6.5] Qt.uiLanguage does not work for locale
changes
* [QTBUG-128478](https://qt-project.atlassian.net/browse/QTBUG-128478) tst_qcompleter crashes on Linux, mostly on RHEL
* [QTBUG-130498](https://qt-project.atlassian.net/browse/QTBUG-130498) Q_ENUM for sub classes does not work
* [QTBUG-129582](https://qt-project.atlassian.net/browse/QTBUG-129582) QComboBox with null view crashing application
* [QTBUG-114873](https://qt-project.atlassian.net/browse/QTBUG-114873) Rendering is broken when moving window between monitors
with OpenGL on macOS
* [QTBUG-129791](https://qt-project.atlassian.net/browse/QTBUG-129791) Issue with Showmaximized function in case of QMainWindow
with Qt::FramelessWindowHint flag
* [QTBUG-130865](https://qt-project.atlassian.net/browse/QTBUG-130865) [Windows] QWidget::showMaximized() does not follow
SPI_SETWORKAREA correctly when Qt::FramelessWindowHint is set
* [QTBUG-116554](https://qt-project.atlassian.net/browse/QTBUG-116554) [macOS] Crash on QCocoaDrag::maybeDragMultipleItems()
* [QTBUG-130930](https://qt-project.atlassian.net/browse/QTBUG-130930) Freetype: Assert when rotating drawing bitmap font with
rotated painter
* [QTBUG-131093](https://qt-project.atlassian.net/browse/QTBUG-131093) [REG 6.5.3 - 6.7.3] [macOS] Global scale factor has no
effect on platform's window size anymore
* [QTBUG-97436](https://qt-project.atlassian.net/browse/QTBUG-97436) Italic rotated text on Linux renders incorrectly
* [QTBUG-130832](https://qt-project.atlassian.net/browse/QTBUG-130832) [REG 6.8.0 -> dev] Windows System Tray Icon: Context
menu's incorrect position
* [QTBUG-128405](https://qt-project.atlassian.net/browse/QTBUG-128405) Unavoidable race condition when using
QPromise::setException()?
* [QTBUG-130811](https://qt-project.atlassian.net/browse/QTBUG-130811) XCB: Async operations between XCB and X11 cause
flakiness in QXcbScreen::topLevelAt()
* [QTBUG-84258](https://qt-project.atlassian.net/browse/QTBUG-84258) tst_Gestures::graphicsItemGesture fails
* [QTBUG-69648](https://qt-project.atlassian.net/browse/QTBUG-69648) tst_Gestures::graphicsItemTreeGesture fails on Ubuntu
18.04.
* [QTBUG-67393](https://qt-project.atlassian.net/browse/QTBUG-67393) tst_Gestures::explicitGraphicsObjectTarget fails on
Ubuntu 17.10.
* [QTBUG-67392](https://qt-project.atlassian.net/browse/QTBUG-67392) tst_Gestures::graphicsItemTreeGesture fails on Ubuntu
17.10.
* [QTBUG-67389](https://qt-project.atlassian.net/browse/QTBUG-67389) tst_Gestures::graphicsView fails on Ubuntu 17.10.
* [QTBUG-68861](https://qt-project.atlassian.net/browse/QTBUG-68861) tst_Gestures::graphicsItemGesture autotest fails on
Ubuntu 18.04
* [QTBUG-70224](https://qt-project.atlassian.net/browse/QTBUG-70224) tst_Gestures::testReuseCanceledGestures autotest fails on
Ubuntu 18.04 & SLES 15
* [QTBUG-70223](https://qt-project.atlassian.net/browse/QTBUG-70223) tst_Gestures::partialGesturePropagation autotest fails on
Ubuntu 18.04 & SLES 15
* [QTBUG-67395](https://qt-project.atlassian.net/browse/QTBUG-67395) tst_Gestures::autoCancelGestures2 fails on Ubuntu 17.10
* [QTBUG-70227](https://qt-project.atlassian.net/browse/QTBUG-70227) tst_Gestures::panelStacksBehindParent autotest fails on
Ubuntu 18.04
* [QTBUG-70226](https://qt-project.atlassian.net/browse/QTBUG-70226) tst_Gestures::panelPropagation autotest fails on Ubuntu
18.04
* [QTBUG-70209](https://qt-project.atlassian.net/browse/QTBUG-70209) tst_Gestures::graphicsViewParentPropagation autotest
fails on Ubuntu 18.04
* [QTBUG-70153](https://qt-project.atlassian.net/browse/QTBUG-70153) tst_Gestures::autoCancelGestures2 autotest fails on
Ubuntu 18.04
* [QTBUG-130980](https://qt-project.atlassian.net/browse/QTBUG-130980) There is a bug with line spacing when QLabel displays
rich text.
* [QTBUG-130552](https://qt-project.atlassian.net/browse/QTBUG-130552) QNetworkConnectionMonitorPrivate::updateState crash
* [QTBUG-131108](https://qt-project.atlassian.net/browse/QTBUG-131108) tst_QFont::italicOblique CI test fails on Android 15
* [QTBUG-131262](https://qt-project.atlassian.net/browse/QTBUG-131262) Freetype: Variable font named instances with slant not
detected as oblique
* [QTBUG-118117](https://qt-project.atlassian.net/browse/QTBUG-118117) [REG 6.4.3->6.5.3] Opening a modeless QDialog removes a
previously set taskbar icon overlay from native API on Windows 11
* [QTBUG-115992](https://qt-project.atlassian.net/browse/QTBUG-115992) Window containing native windows window is excessively
repainted on move
* [QTBUG-118231](https://qt-project.atlassian.net/browse/QTBUG-118231) Android app 'pause' or 'screen-off' causes
'eglSwapBuffers failed' and various logcat errors
* [QTBUG-131587](https://qt-project.atlassian.net/browse/QTBUG-131587) Flaky emoji rendering on Windows
* [QTBUG-125053](https://qt-project.atlassian.net/browse/QTBUG-125053) QAbstractListModel fails to populate QML model
* [QTBUG-127340](https://qt-project.atlassian.net/browse/QTBUG-127340) [Reg 6.7->6.8] Wrong item count in ListView/Repeater
* [QTBUG-128420](https://qt-project.atlassian.net/browse/QTBUG-128420) Qt 6.8 does not support build paths with white spaces
anymore
* [QTBUG-129716](https://qt-project.atlassian.net/browse/QTBUG-129716) Submenu item not correctly aligned in rtl mode (gap to
main menu)
* [QTBUG-121653](https://qt-project.atlassian.net/browse/QTBUG-121653) License clarification for unicode & unicode-cldr related
files
* [QTCREATORBUG-28838](https://qt-project.atlassian.net/browse/QTCREATORBUG-28838) QtC indentation hickup on enable_if_t<LHS < RHS>
in template-initializer
* [QTBUG-130613](https://qt-project.atlassian.net/browse/QTBUG-130613) Documentation of Q_GLOBAL_STATIC(MyType, staticType) is
confusing
* [COIN-1154](https://qt-project.atlassian.net/browse/COIN-1154) Failed to start Android emulator on RHEL
* [QTBUG-121457](https://qt-project.atlassian.net/browse/QTBUG-121457) Amend qt_internal_add_docs to accept INDEX_DIRECTORIES
argument
* [QTBUG-130884](https://qt-project.atlassian.net/browse/QTBUG-130884) xdg-desktop-portal should be enabled only environments
that actually supports it
* [QTBUG-131343](https://qt-project.atlassian.net/browse/QTBUG-131343) Crash in QXcbScreen::setMonitor() via KDE/xembed-sni-
proxy

### qtdeclarative
* [QTBUG-127308](https://qt-project.atlassian.net/browse/QTBUG-127308) [REG 6.6 → 6.8] qmlRestrictedType warning errorneously
triggers for enum class
* [QTBUG-129329](https://qt-project.atlassian.net/browse/QTBUG-129329) QML Preview doesn't update properly
* [QTBUG-129310](https://qt-project.atlassian.net/browse/QTBUG-129310) Possible garbage collector bug
* [QTBUG-85860](https://qt-project.atlassian.net/browse/QTBUG-85860) BusyIndicator in inconsistent state when running property
changed too fast
* [QTBUG-126784](https://qt-project.atlassian.net/browse/QTBUG-126784)  QQuickWindow::graphicsConfiguration() documentation
wrong
* [QTBUG-128875](https://qt-project.atlassian.net/browse/QTBUG-128875) [PDF] Zooming in and out the pdf file then opening
another one causes to app to crash
* [QTBUG-128895](https://qt-project.atlassian.net/browse/QTBUG-128895) [Reg 6.2 -> 6.5] QtQuick.Templates causes crashes if
QtQuick types are not registered
* [QTBUG-129165](https://qt-project.atlassian.net/browse/QTBUG-129165) regression ListView not updating count
* [QTBUG-127340](https://qt-project.atlassian.net/browse/QTBUG-127340) [Reg 6.7->6.8] Wrong item count in ListView/Repeater
* [QTBUG-125053](https://qt-project.atlassian.net/browse/QTBUG-125053) QAbstractListModel fails to populate QML model
* [QTBUG-129699](https://qt-project.atlassian.net/browse/QTBUG-129699) Crash in void
QQuickDeliveryAgentPrivate::clearFocusInScope when closing Application
* [QTBUG-128843](https://qt-project.atlassian.net/browse/QTBUG-128843) Crash when Qt QML is built with -ltcg flag
* [QTBUG-119034](https://qt-project.atlassian.net/browse/QTBUG-119034) result of Item.mapToItem call is round to integer
* [QTBUG-129759](https://qt-project.atlassian.net/browse/QTBUG-129759) Document delegateModel of ComboBox
* [QTBUG-130143](https://qt-project.atlassian.net/browse/QTBUG-130143) Crash in QQmlAbstractBinding::removeFromObject()
* [QTBUG-129681](https://qt-project.atlassian.net/browse/QTBUG-129681) QML imports break on UNC paths that contain `%` chars
* [QTBUG-124478](https://qt-project.atlassian.net/browse/QTBUG-124478) Qt6.5.1 QML - Scrolling issue when using a trackpad on
macOS when there are nested scroll areas
* [QTBUG-129622](https://qt-project.atlassian.net/browse/QTBUG-129622) [Reg 6.7.2 -> 6.7.3] Crash in QQuickItem::setX
* [QTBUG-119530](https://qt-project.atlassian.net/browse/QTBUG-119530) QML - screen reader reads twice the title of the
application
* [QTBUG-130689](https://qt-project.atlassian.net/browse/QTBUG-130689) There are no  any QML Screen change notifications when
you change the MacBook display resolution
* [QTBUG-130517](https://qt-project.atlassian.net/browse/QTBUG-130517) PinchHandler unexpectedly resets target's rotation even
if rotationAxis.enabled is false
* [QTBUG-128269](https://qt-project.atlassian.net/browse/QTBUG-128269) QQmlEngine destructor hangs on
QQmlTypeLoader::invalidate
* [QTBUG-130820](https://qt-project.atlassian.net/browse/QTBUG-130820) Documentation for ComboBox find() Method has wrong
enumeration value MatchEndsWidth
* [QTBUG-130536](https://qt-project.atlassian.net/browse/QTBUG-130536) Disabled MenuItem propagates clicks to underlying mouse
area in drawer
* [QTBUG-130867](https://qt-project.atlassian.net/browse/QTBUG-130867) QQmlComponent::loadFromModule() bug
* [QTBUG-130856](https://qt-project.atlassian.net/browse/QTBUG-130856) Calling replace() on QQuickWindow::data causes a crash
* [QTBUG-130331](https://qt-project.atlassian.net/browse/QTBUG-130331) Cannot use VirtualKeyboard when using several modal
Popup
* [QTBUG-129520](https://qt-project.atlassian.net/browse/QTBUG-129520) Click/mouseRelease signals are not received by a button
in a Popup if the InputPanel is placed in front of the Popup
* [QTBUG-118879](https://qt-project.atlassian.net/browse/QTBUG-118879) QML ListElement does not work with enums when "as"
import is used
* [QTBUG-127122](https://qt-project.atlassian.net/browse/QTBUG-127122) some MouseArea's signals are weirdly triggered
* [QTBUG-130974](https://qt-project.atlassian.net/browse/QTBUG-130974) A regular expression pattern gives unexpected results in
QML and QJSEngine.
* [QTBUG-131263](https://qt-project.atlassian.net/browse/QTBUG-131263) FAIL!  : tst_qqmllanguage::retrieveQmlTypeId()
'qmlTypeId("testhelper", 1, 0, "PurelyDeclarativeSingleton") >= 0'
returned FALSE
* [QTBUG-128577](https://qt-project.atlassian.net/browse/QTBUG-128577) Property "visible" of QML Item seems to affect how mouse
event is delivered
* [QTBUG-125135](https://qt-project.atlassian.net/browse/QTBUG-125135) [Reg 6.5.3->6.5.4]Qml Popup component is not closing
anymore when instantiated via QQuickWidget.
* [QTBUG-115536](https://qt-project.atlassian.net/browse/QTBUG-115536) Setting Window.contentOrientation breaks Popup on
regular desktop
* [QTBUG-123499](https://qt-project.atlassian.net/browse/QTBUG-123499) tst_MptaInterop::touchesThenPinch fails in Qt 6
* [QTBUG-123764](https://qt-project.atlassian.net/browse/QTBUG-123764) MessageDialog detailed text does not show in Fusion
style on dark mode

### qtactiveqt
* [QTBUG-123498](https://qt-project.atlassian.net/browse/QTBUG-123498) [Reg 6.2.0 -> 6.2.11 (possibly 6.2.3->6.2.4)][ActiveQt]
Resizing QTableView header inside a QAXCLASS freezes COM application
* [QTBUG-111760](https://qt-project.atlassian.net/browse/QTBUG-111760) target_link_libraries(foo INTERFACE Qt::Core) fails for
interface libs with CMake < 3.19 on Windows

### qtmultimedia
* [QTBUG-126592](https://qt-project.atlassian.net/browse/QTBUG-126592) MediaPlayer never stops on some audio - ffmpeg
* [QTBUG-129232](https://qt-project.atlassian.net/browse/QTBUG-129232) Fix misleading diagnostics in CMake output when FFmpeg
is not found
* [QTBUG-129184](https://qt-project.atlassian.net/browse/QTBUG-129184) Bad type for GstURIDecodeBin property
* [QTBUG-129053](https://qt-project.atlassian.net/browse/QTBUG-129053) Deadlock in tst_qsoundeffect
* [QTBUG-129469](https://qt-project.atlassian.net/browse/QTBUG-129469) Test #42: tst_qmediaplayerbackend ..........***Failed
* [QTBUG-129712](https://qt-project.atlassian.net/browse/QTBUG-129712) Test timed out:
makeCustomGStreamerCamera_fromPipelineDescription_userProvidedGstElement
* [QTBUG-129501](https://qt-project.atlassian.net/browse/QTBUG-129501) [REG 6.7.2-6.7.3] QMediaRecorder doesn't respect the
output file extension
* [QTBUG-129597](https://qt-project.atlassian.net/browse/QTBUG-129597) Assertion error, QSoundEffect object creation on worker
thread using QtConcurrent
* [QTBUG-46409](https://qt-project.atlassian.net/browse/QTBUG-46409) tst_qaudiodeviceinfo fails in RHEL
* [QTBUG-130441](https://qt-project.atlassian.net/browse/QTBUG-130441) Configuring Qt Multimedia fails even if -no-feature-
ffmpeg is specified
* [QTBUG-130600](https://qt-project.atlassian.net/browse/QTBUG-130600) [gstreamer] Intel IPU6 camera shows up as multiple
devices
* [QTBUG-130387](https://qt-project.atlassian.net/browse/QTBUG-130387) [gstreamer] QMediaRecorder - recorder broken when audio
input present
* [QTBUG-112512](https://qt-project.atlassian.net/browse/QTBUG-112512) QSoundEffect cuts out on very short sounds ( ~ 0.2 - 0.3
seconds )
* [QTBUG-130668](https://qt-project.atlassian.net/browse/QTBUG-130668) QSoundEffect::setSource does not change audio source
* [QTBUG-127745](https://qt-project.atlassian.net/browse/QTBUG-127745) tst_qvideoframecolormanagement failed on Ubuntu 24.04
offscreen(arm64)
* [QTBUG-127744](https://qt-project.atlassian.net/browse/QTBUG-127744) tst_qvideoframe failed on Ubuntu 24.04 offscreen(arm64)
* [QTBUG-127746](https://qt-project.atlassian.net/browse/QTBUG-127746) tst_qmediaplayerbackend failed on Ubuntu 24.04
offscreen(arm64)
* [QTBUG-127784](https://qt-project.atlassian.net/browse/QTBUG-127784) Inaccurate color handling when no RHI backend is
available
* [QTBUG-127543](https://qt-project.atlassian.net/browse/QTBUG-127543) QSoundEffect/SoundEffect audioDevice property has no
effect when device is changed
* [QTBUG-124350](https://qt-project.atlassian.net/browse/QTBUG-124350) [Boot2Qt] Switching the cameras in QML camera app causes
the app to crash
* [QTBUG-129351](https://qt-project.atlassian.net/browse/QTBUG-129351) [Boot2Qt][Camera] The QML camera app crashed when
swtiching the camera from USB to CSI
* [QTBUG-119506](https://qt-project.atlassian.net/browse/QTBUG-119506) AudioOutputExample-Graphic&Multimedia-Example Unplugging
& plugging headphones don't work as expected
* [QTBUG-129379](https://qt-project.atlassian.net/browse/QTBUG-129379) Declarative camera example: video recording stutters.
* [QTBUG-130911](https://qt-project.atlassian.net/browse/QTBUG-130911) Android: Regression for recording after ffmpeg update to
7.1
* [QTBUG-112014](https://qt-project.atlassian.net/browse/QTBUG-112014) QMediaPlayer hangs up on setPosition(...) when using
gstreamer backend
* [QTBUG-124372](https://qt-project.atlassian.net/browse/QTBUG-124372) After seeking using the GStreamer backend, the stream
goes into a paused state.
* [QTBUG-126799](https://qt-project.atlassian.net/browse/QTBUG-126799) [gstreamer] playback rate / seeking unreliable
* [QTBUG-127565](https://qt-project.atlassian.net/browse/QTBUG-127565) Top flaky test: tst_qmediaplayerbackend::finiteLoops
* [QTBUG-122757](https://qt-project.atlassian.net/browse/QTBUG-122757) FFmpeg+Intel VAAPI decoding of certain h264/mp4 videos
fails in 6.6.x+
* [QTBUG-126106](https://qt-project.atlassian.net/browse/QTBUG-126106) QVideoFrames sent to QML as signal arguments are
deallocated too late
* [QTBUG-129486](https://qt-project.atlassian.net/browse/QTBUG-129486) re-enable test for gstreamer without blocking the
dependency updater
* [QTBUG-121542](https://qt-project.atlassian.net/browse/QTBUG-121542) Video playback with QtMultimedia stutters when using
d3d11 backend, WindowsMediaFoundation, and having an animation on the
scene.
* [QTBUG-117099](https://qt-project.atlassian.net/browse/QTBUG-117099) Video jerks when playing (Windows backend)
* [QTBUG-110453](https://qt-project.atlassian.net/browse/QTBUG-110453)  tst_QVideoWidget::fullScreen fails with Android target
in RHEL-8.4
* [QTBUG-118310](https://qt-project.atlassian.net/browse/QTBUG-118310) QML Camera - setting WhiteBalance, Exposure, ISO doesn't
work as expected
* [QTBUG-129831](https://qt-project.atlassian.net/browse/QTBUG-129831) QCamera::setCameraDevice has unclear behavior
* [QTBUG-124517](https://qt-project.atlassian.net/browse/QTBUG-124517) [gstreamer] GST_MESSAGE_BUFFERING not delivered if
(uri)decodebin doesn't contain a queue
* [QTBUG-125251](https://qt-project.atlassian.net/browse/QTBUG-125251) [gstreamer] spurious assertion failure on shutdown

### qtlocation
* [QTBUG-130139](https://qt-project.atlassian.net/browse/QTBUG-130139) Flickable: an outer flickable can sometimes be stuck in
dragging mode when dragging on an inner flickable

### qtsensors
* [QTBUG-128167](https://qt-project.atlassian.net/browse/QTBUG-128167) The android implementation is using an
obsolete/deprecated/removed function ALooper_pollAll

### qtconnectivity
* [QTBUG-129763](https://qt-project.atlassian.net/browse/QTBUG-129763) qapduutils.cpp fails to compile on mingw developer build
with -force-asserts

### qtwayland
* [QTBUG-127980](https://qt-project.atlassian.net/browse/QTBUG-127980) Segmentation fault after Qt.quit()
* [QTBUG-130581](https://qt-project.atlassian.net/browse/QTBUG-130581) Virtual Keyboard Hints are not reported for the second
top level wayland window

### qtserialport
* [QTBUG-109455](https://qt-project.atlassian.net/browse/QTBUG-109455) read() returns qint64 not int
* [QTBUG-120221](https://qt-project.atlassian.net/browse/QTBUG-120221) clang-tidy, and probably clang complains about dllimport
vs. inline in qtserialportinfo.h

### qtwebengine
* [QTBUG-128241](https://qt-project.atlassian.net/browse/QTBUG-128241) HTML selection tag crashes app when clicked on
* [QTBUG-130256](https://qt-project.atlassian.net/browse/QTBUG-130256) [Regression]The content of QWebEngineView disappears when
setting the std::locale::global
* CVE-2024-9369: Insufficient data validation in Mojo
* CVE-2024-9602: Type Confusion in V8
* CVE-2024-9603: Type Confusion in V8
* CVE-2024-9965: Insufficient data validation in DevTools
* CVE-2024-9966: Inappropriate implementation in Navigations
* CVE-2024-10229: Inappropriate implementation in Extensions
* CVE-2024-10230: Type Confusion in V8
* CVE-2024-10231: Type Confusion in V8
* CVE-2024-10487: Out of bounds write in Dawn
* CVE-2024-10827: Use after free in Serial
* CVE-2024-11110: Inappropriate implementation in Blink
* CVE-2024-11112: Use after free in Media
* CVE-2024-11114: Inappropriate implementation in Views
* CVE-2024-11116: Inappropriate implementation in Paint
* CVE-2024-11117: Inappropriate implementation in FileSystem
* Security bug 356098278
* Security bug 361651894
* Security bug 366635354
* Security bug 369630648

### qtdatavis3d
* [QTBUG-128460](https://qt-project.atlassian.net/browse/QTBUG-128460) Main window crashes/black out when QtDataVisualization
3D chart in QMdiSubWindow destroyed

### qtnetworkauth
* [QTBUG-129590](https://qt-project.atlassian.net/browse/QTBUG-129590) tst_oauth2 SSL certificate usage fails

### qtquicktimeline
* [QTBUG-122812](https://qt-project.atlassian.net/browse/QTBUG-122812) Binding is not restored for Timeline component

### qtquick3d
* [QTBUG-129140](https://qt-project.atlassian.net/browse/QTBUG-129140) [REG] Lightprobe using texture data causes crash
* [QTBUG-127760](https://qt-project.atlassian.net/browse/QTBUG-127760) qtdoc dice example debug assertion failure
* [QTBUG-130381](https://qt-project.atlassian.net/browse/QTBUG-130381) quick3d/embree: AVX code paths not disabled with GCC 14
* [QTBUG-128352](https://qt-project.atlassian.net/browse/QTBUG-128352) Potential thread safety issue in many Qt Quick 3D
examples
* [QTBUG-131361](https://qt-project.atlassian.net/browse/QTBUG-131361) Intel skylake fails to build for Boot2Qt lts-6.5(.8)

### qtinterfaceframework (Commercial only)
* [QTBUG-130082](https://qt-project.atlassian.net/browse/QTBUG-130082) Doc: wrong annotation name for defaultServerMode

Known Issues
------------

* Check that your system meets Qt's requirements:
https://doc.qt.io/qt-6.5/supported-platforms.html

* The RTA (release test automation) reported issues in Qt 6.5.x:
https://qt-project.atlassian.net/issues/?filter=15085

* See Qt 6.5 known issues from:
https://wiki.qt.io/Qt_6.5_Known_Issues

* Qt 6.5.8 Open issues in Jira:
https://qt-project.atlassian.net/issues/?filter=15048

Credits for the release goes to:
---------------------------------

Dilek Akcay  
Mate Barany  
Vladimir Belyavsky  
Tim Blechmann  
Eskil Abrahamsen Blomfeldt  
Joerg Bornemann  
Kai Uwe Broulik  
Michael Brüning  
Wang Chuan  
Alexandru Croitor  
Mitch Curtis  
Pavel Dubsky  
Artem Dyomin  
Alexey Edelev  
Oliver Eftevaag  
Christian Ehrlicher  
Andreas Eliasson  
Robert Griebl  
Richard Moe Gustavsen  
Mikko Hallamaa  
Jøger Hansegård  
Moss Heim  
Ulf Hermann  
Volker Hilsheimer  
Zhang Hongyuan  
Allan Sandfeld Jensen  
Jonas Karlsson  
Timothée Keller  
Ahmed El Khazari  
Friedemann Kleint  
Jarek Kobus  
Jani Korteniemi  
Fabian Kosmale  
Santhosh Kumar  
Kai Köhne  
Inho Lee  
Wladimir Leuschner  
Thiago Macieira  
Shveta Mittal  
Safiyyah Moosa  
Bartlomiej Moskal  
Marc Mutz  
Antti Määttä  
Mårten Nordheim  
Tinja Paavoseppä  
Jerome Pasion  
Evgen Pervenenko  
Samuli Piippo  
Joni Poikelin  
Rami Potinkara  
Sakaria Pouke  
Dheerendra Purohit  
Liang Qi  
Topi Reinio  
Shawn Rutledge  
Lars Schmertmann  
Sami Shalayel  
Jiu Shanheng  
Andy Shaw  
Venugopal Shivashankar  
Nils Petter Skålerud  
Ivan Solovev  
Axel Spoerl  
Christian Strømme  
Tarja Sundqvist  
Lars Sutterud  
Jan Arve Sæther  
Morten Sørvig  
Orkun Tokdemir  
Sami Varanka  
Doris Verria  
Tor Arne Vestbø  
Petri Virkkunen  
Juha Vuolle  
Edward Welbourne  
Paul Wicking  
Oliver Wolff  
Milian Wolff  
