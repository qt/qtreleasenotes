Release notes
=============
Qt WebEngine and Qt Pdf 6.140.0 marks the first independent release of Qt WebEngine and Qt Pdf, aka QWE

The QWE 6.140 series is binary compatible with the versions that were part of the Qt 6.11.x series.
Applications compiled for 6.11 will continue to run with 6.140, except for the possible runtime issue mentioned below.

Source incompatible changes
---------------------------
In order to comply with upcoming EU regulation about safe defaults. The qrc URL scheme is no
longer reachable from remote sources by default. This protects remote content from accessing
qrc resources not meant for public access. If you have applications that rely on remote
content accessing qrc resources, we recommend installing a more limited custom URL scheme handler
that only share exactly what you mean to share.


Important Changes
-----------------

* 89737c9fb QPdfView: add ctrl-mouse-wheel zoom at the cursor position
    * QPdfView now allows control-mouse-wheel zooming.

* c14b47f34 Add userInitiated into QWebEngineNavigationRequest
    * Added userInitiated property to indicate whether the navigation
      was triggered by a user gesture (keyboard or mouse event).

* 496f6ae28 doc: QPdfDocument::render() is newly overloaded in 6.12
    * QPdfDocument::render is now overloaded to add format and fillColor
      as optional arguments.

* 4a5272390 CMake: Add new version numbering schema
    * WebEngine and Pdf now have their own version numbering

* e7c9a5bd9 Make 'qrc' a local scheme
    * qrc resources are no longer reachable from remote schemes by
      default.


Fixes
-----

* [QTBUG-143317](https://qt-project.atlassian.net/browse/QTBUG-143317) QPdfView assert on exit in the example
* [QTBUG-143974](https://qt-project.atlassian.net/browse/QTBUG-143974) FAILED:
examples/pdf/singlepage/CMakeFiles/singlepage_qmllint
* [QTBUG-142806](https://qt-project.atlassian.net/browse/QTBUG-142806) Pdfviewer example highlights wrong part of word if word
contains multiple instances of searched text
* [QTBUG-145902](https://qt-project.atlassian.net/browse/QTBUG-145902) [qtwebengine] Crash during Skia/EGL initialization
* [QTBUG-145398](https://qt-project.atlassian.net/browse/QTBUG-145398) tst_qquickwebengineviewgraphics fails on macOS 26 x86_64
* [QTBUG-145344](https://qt-project.atlassian.net/browse/QTBUG-145344) Browser based on QtWebEngine would missing web page or
get flickering while enter web site with video content
* [QTBUG-145749](https://qt-project.atlassian.net/browse/QTBUG-145749) QWebEngineClientCertificateSelection does not include
certificates from PKCS#11 hardware tokens (smart cards)
* [QTBUG-147006](https://qt-project.atlassian.net/browse/QTBUG-147006) error: unknown type name
'QTEST_DISABLE_KEYPAD_NAVIGATION'
* [QTBUG-145876](https://qt-project.atlassian.net/browse/QTBUG-145876) [qtwebengine] webAuthUxRequested does not fire unless an
authentication method is available
* [QTBUG-146565](https://qt-project.atlassian.net/browse/QTBUG-146565) [qtwebengine] QWebEngineWebAuthUxRequest objects have
garbage/uninitialized fields
* [QTBUG-146775](https://qt-project.atlassian.net/browse/QTBUG-146775) QtWebEngine crashes on multi-planar NativePixmap import
due to DRM render node mismatch under EGL/Wayland
* [QTBUG-146564](https://qt-project.atlassian.net/browse/QTBUG-146564) [qtwebengine] Crash during QWebEnginePage destruction
with outstanding QWebEngineWebAuthUxRequest
* [QTBUG-150566](https://qt-project.atlassian.net/browse/QTBUG-150566) [Reg 6.11.2->6.12.0rc] QPdfView: Crash when calling
setDocument(nullptr)
* [QTBUG-150218](https://qt-project.atlassian.net/browse/QTBUG-150218) cmake regression in QtWebengine 6.12 beta 4
* [QTBUG-151015](https://qt-project.atlassian.net/browse/QTBUG-151015) QPdfView's destructor crashes if it is the parent of its
current QPdfDocument
* [QTBUG-147636](https://qt-project.atlassian.net/browse/QTBUG-147636) [Reg 6.8.5 -> 6.8.6] Qt WebEngine: HTML "select"
dropdown cannot be dismissed by touch
* [QTBUG-148847](https://qt-project.atlassian.net/browse/QTBUG-148847) [Weston + Qt Quick only] WebEngineView shuts down
<select> element right after the element is drawn
* [QTBUG-151613](https://qt-project.atlassian.net/browse/QTBUG-151613) Crash in
DisplaySoftwareOutputSurface::Device::swapFrame() on Windows
* [QTBUG-150300](https://qt-project.atlassian.net/browse/QTBUG-150300) When WebEngineView is deeply nested inside a scrollable
item, its <select> drop-downs appear in the wrong location
* [QTBUG-137870](https://qt-project.atlassian.net/browse/QTBUG-137870) cmake: qt can only be built once
* [QTBUG-144178](https://qt-project.atlassian.net/browse/QTBUG-144178) RHEL 10: qtwebengine auto test failures on Wayland
* [QTBUG-150317](https://qt-project.atlassian.net/browse/QTBUG-150317) 6.140 gets udpate round from dev
* [QTBUG-149209](https://qt-project.atlassian.net/browse/QTBUG-149209) Do not confuse users on the Welcome screen in QtC that
we would ship a browser

Known Issues
------------

Credits for the release goes to:
---------------------------------

* Dimitrios Apostolou
* Vladimir Belyavsky
* Eskil Abrahamsen Blomfeldt
* Albert Astals Cid
* Joerg Bornemann
* Marcell Brauner
* Michael Brüning
* Eren Bursali
* Olivier De Cannière
* Kaloyan Chehlarski
* Alexandru Croitor
* Simo Fält
* Jani Heikkinen
* Tero Heikkinen
* Moss Heim
* Allan Sandfeld Jensen
* Jukka Jokiniva
* Dennis Kim
* Friedemann Kleint
* Michal Klocek
* Sze Howe Koh
* Antti Kokko
* Kai Köhne
* David Loki
* Marc Mutz
* Jerome Pasion
* Yauheni Pervenenka
* Samuli Piippo
* Topi Reinio
* Shawn Rutledge
* Toni Saario
* Ratchanan Srirattanamet
* Benjamin Terrier
* Elias Toivola
* Peter Varga
* Tor Arne Vestbø
