Release notes
=============
Qt 6.12 introduces many new features and improvements as well as bugfixes
over the 6.11.x series. For more details, refer to the online
documentation included in this distribution. The documentation is also
available online:

https://doc.qt.io/qt-6/whatsnew612.html

The Qt version 6.12 series is binary compatible with the 6.11.x series.
Applications compiled for 6.11 will continue to run with 6.12.

Some of the changes listed in this file include issue tracking numbers
corresponding to tasks in the Qt Bug Tracker:

https://qt-project.atlassian.net/

Each of these identifiers can be entered in the bug tracker to obtain
more information about a particular change.

To make it easier to port to Qt 6, we have created a porting guide to
summarize what changed between Qt 5 and Qt 6 and provide guidance on how to
adapt to those changes. In the guide, you can find links to articles about
changes that may affect your application and help you transition from Qt
5.15 to Qt 6:

https://doc.qt.io/qt-6/portingguide.html

Removed modules
-----------------
Compared to 6.11.x series 6.12 release does not ship with qtwebengine nor qtpdf
modules as these are going to be released separately from now on. Please note this
also include the qtwebview's qtwebengine backend, which will now also ship with the
qtwebengine release.

Important Changes
-----------------
### Security fixes
* [CVE-2026-6210](https://nvd.nist.gov/vuln/detail/CVE-2026-6210) in qtsvg
* [CVE-2026-8168](https://nvd.nist.gov/vuln/detail/CVE-2026-8168) in qtsvg
* [CVE-2026-9499](https://nvd.nist.gov/vuln/detail/CVE-2026-9499) in qt5compat
* [CVE-2026-13326](https://nvd.nist.gov/vuln/detail/CVE-2026-13326) in qtconnectivity
* [CVE-2025-14576](https://nvd.nist.gov/vuln/detail/CVE-2025-14576) in qtdeclarative
* [CVE-2026-15037](https://nvd.nist.gov/vuln/detail/CVE-2026-15037) in qtbase
* [CVE-2026-16762](https://nvd.nist.gov/vuln/detail/CVE-2026-16762) in qtbase
* [CVE-2026-19248](https://nvd.nist.gov/vuln/detail/CVE-2026-19248) in qtbase
* [CVE-2026-76151](https://nvd.nist.gov/vuln/detail/CVE-2026-76151) in qtbase
* [CVE-2026-78253](https://nvd.nist.gov/vuln/detail/CVE-2026-78253) in qtbase
* [CVE-2026-79616](https://nvd.nist.gov/vuln/detail/CVE-2026-79616) in qtdeclarative
* [CVE-2026-79680](https://nvd.nist.gov/vuln/detail/CVE-2026-79680) in qtvncserver
* [CVE-2026-82292](https://nvd.nist.gov/vuln/detail/CVE-2026-82292) in qtbase
* [CVE-2026-96432](https://nvd.nist.gov/vuln/detail/CVE-2026-96432) in qtbase
* [CVE-2026-97845](https://nvd.nist.gov/vuln/detail/CVE-2026-97845) in qt5compat
* [CVE-2026-101201](https://nvd.nist.gov/vuln/detail/CVE-2026-101201) in qt5compat

### qtbase
* 6da0a51f1a0 rhi: vulkan: use VK_EXT_device_fault to report device loss
  details
    * The QRhi Vulkan backend now uses the VK_EXT_device_fault
      extension, when available, to log detailed information on
      VK_ERROR_DEVICE_LOST.

* 8a9827352d8 CMake: Enable the openssl-hash feature by default
    * The openssl-hash feature is now enabled by default if openssl-
      linked is on. This enables a more robust implementation of
      QCryptographicHash.

* b4a8c46b08b CMake: Un-TP qt_deploy_translations
    * qt_deploy_translations has been taken out of technical preview.

* 0feba1d77ba CMake: Un-TP qt_extract_metatypes
    * qt_extract_metatypes has been taken out of technical preview.

* a2c8bd42126 CMake: Un-TP qt_finalize_project
    * qt_finalize_project has been taken out of technical preview.

* 7238aba9dea CMake: Un-TP deployment variables
    * The variables QT_DEPLOY_SUPPORT and QT_ENABLE_VERBOSE_DEPLOYMENT
      have been taken out of technical preview.

* d1e98cb4db1 CMake: Un-TP QT_RESOURCE_PREFIX
    * QT_RESOURCE_PREFIX has been taken out of technical preview.

* ce9613fd8b2 CMake: Un-TP QT_TARGETS_FOLDER
    * QT_TARGETS_FOLDER has been taken out of technical preview.

* ccb28cec1ac QFileSystemWatcher: Allow using inotify on FreeBSD
    * Starting with FreeBSD 15, this class will use the inotify backend
      instead of the kqueue one.

* 5f326ad2925 macOS: Dispose of QNSWindow when our view is embedded in
  non-Qt NSView
    * QCocoaNativeInterface::setEmbeddedInForeignView is no longer
      necessary or supported to embed the underlying QNSView of a
      QWindow into a non-Qt view hierarchy.

* a514ff658b4 Add QDataStream stream operators to QHttpHeaders
    * Added QDataStream operators.

* bdfa2cc942b Add QStyleHints::toolTipWakeUpDelay
    * Added toolTipWakeUpDelay to allow control over the delay before
      tool tips should be shown.

* a030508de6b Let QFile::copy() accept optional permissions
    * It is now possible to pass permissions to QFile::copy() to control
      the permissions with which the copy is created.

* 7e2bdddf4a3 Change QtTest's text format's formatResult() to use 'e'
  format
    * In benchmark results the plain text logger now uses the 'e' format
      rather than the truncated (rather than rounded) 'f' format used
      previously.

* a64a75f340d Defer permission setting in QSaveFile until commit()
    * QSaveFile now defers setting requested permissions until commit()
      is called. While writing the file it uses restrictive permissions
      to limit the scope for interference.

* 444b9f854e0 Add QAccessibilityHints::motionPreference
    * Added motionPreference, a property that can be used to honor the
      users request to reduce the amount of non-essential animations in
      their UI.

* 4660aeb95a6 CMake: Rename qt_no_entrypoint to QT_NO_ENTRYPOINT
    * The qt_no_entrypoint target property has been renamed to
      QT_NO_ENTRYPOINT and taken out of technology preview. The old name
      is still recognized for backward compatibility.

* 0c234ada743 macOS: Maintain QWindow geometry when non-flipped parent
  is resized
    * QWindows parented into non-flipped NSViews will try to maintain
      their position relative to their superview's top left corner when
      the superview is resized, via an explicit auto resizing mask. To
      opt out of this behavior set the view's
      translatesAutoresizingMaskIntoConstraints property to NO, or set
      an explicit auto resizing mask after reparenting the window.

* 93424c985e1 QVarLengthArray: add QList-style removeAt(i)
    * Added QList-style removeAt() function.

* 3cfa7e094a1 QStyle: add
  standardIcon(SP_TabScrollLeft/Right/Up/DownButton)
    * The enum QStyle::StandardPixmap gained the four new values
      SP_TabScrollLeftButton/SP_TabScrollRightButton/
      SP_TabScrollUpButton/SP_TabScrollDownButton.

* 08e24689237 QHostInfo: add clearCache() to clear DNS result cache
    * Added clearCache(), which clears any cached host name lookups, if
      the QHostInfo caching is enabled.

* 922204acfe5 CMake: Introduce QTP0006 for Wayland protocol source
  visibility
    * Added CMake policy QTP0006. When set to NEW,
      qt_generate_wayland_protocol_client_sources and
      qt_generate_wayland_protocol_server_sources default to
      PRIVATE_CODE instead of PUBLIC_CODE.

* 77b25e0e2b9 QImageReader: Introduce effectiveSize, repecting
  autoTransform
    * Introduced effectiveSize() which respects autoTransform()

* c0d29ed52bc Introduce QSslKeyingMaterial
    * Implement keying material exporters as defined in RFC 5705 (TLS
      Keying Material) and RFC 8446 (TLS 1.3).

* 981068f6b0c configure: Add optional module filter to -list-features
    * Added an optional module argument to -list-features to filter the
      output to features from a specific module. Use -list-modules to
      discover available module names.

* d3241edb024 configure: Add -list-modules option
    * Added -list-modules option that prints the names of modules that
      can be passed to -list-features.

* 39d74003a08 QVariant: add ctors from rvalues [2/2]: special cases
    * Now supports construction from rvalues.

* 7011cfb0b50 QList: make detach() public API
    * detach() is now public API. Before, it was already a public
      method, but it was undocumented.

* 901da294d5d QString: make detach() public API
    * detach() is now public API. Before, it was already a public
      method, but it was undocumented.

* 2069bf8a583 Add option to statically link compiler runtime libraries
    * Added CMake feature static_compiler_runtime which removes the
      dependency on the Visual C++ Redistributable on Windows.

* 330e4084919 Treat CLDR-alias-equivalent names the same in QTimeZone
    * The constructor now accepts IANA IDs that a supported ID's
      QTimeZone instance's hasAlternativeName() would recognise as an
      alias for the supported ID. In line with this,
      isTimeZoneIdAvailable() will now report such IDs as available.

* 2c6071114a2 Wayland: Add linux-dmabuf-v1 protocol
    * Added version 5 of stable linux-dmabuf protocol.

* 25f910633e4 QRM: extend RowOptions to allow customizing headerData
    * The RowOptions template can now be specialized to provide a custom
      headerData implementation.

* 790366c92aa QNX QPA: add Vulkan surface support via
  VK_QNX_screen_surface
    * Added Vulkan surface support to the QNX QPA plugin. QWindow-based
      Vulkan rendering via QVulkanInstance and the Qt RHI Vulkan backend
      is now available on QNX 8.0 targets using the
      VK_QNX_screen_surface extension.

* 0cd0d6e0377 Create infrastructure for variance calculations in
  benchmarks
    * Add reporting of variance or standard deviation to benchmark
      metrics, whenever more than one run of the measurement contributed
      to the result, if supported by the measurer.

* fc721205258 Include CLDR-canonical aliases in availableTimeZoneIds()
    * The availableTimeZoneIds() list now includes some standard (though
      potentially out of date) aliases for supported IANA IDs, in
      addition to those supported IDs, to improve cross-platform
      consistency and support long-term stability of names.

* 487f04b286f Port QTimeZone::isTimeZoneIdAvailable() to take
  QByteArrayView
    * isTimeZoneIdAvailable() now accepts a QByteArrayView, saving the
      need to allocate a copy for this query.

* 4b8e0d10a06 rhi: add indirect drawing
    * Added indirect rendering. It is now possible to create a
      QRhiBuffer with usage IndirectBuffer, fill it with an array of
      QRhiIndirectDrawCommand or QRhiIndexedIndirectDrawCommand
      structures (from either CPU uploads or GPU compute shaders), and
      issue QRhiCommandBuffer::drawIndirect() or
      QRhiCommandBuffer::drawIndexedIndirect() calls on all supported
      backends.

* be28eff4167 Add Qt::compareThreeWay() overload for std::pair
    * Added Qt::compareThreeWay() overload for std::pair<>.

* a233557704d Q(Multi)Map: add relational operators
    * The classes now implement all six relational operators, and also
      provide operator<=>() in C++20 mode.

* 725bb96ab16 QFSFileEngine/Unix: properly set QT_OPEN_LARGEFILE for
  open()
    * Fixed a bug that would cause QFile to be limited to 2 GB file
      sizes on some 32-bit operating systems, when creating a new file
      or opening an existing one for reading and writing.

* 1b0480b99cb QTreeView: add itemDecorationRect()
    * QTreeView gained the new function itemDecorationRect(const
      QModelIndex &).

* 21d6543cf11 QTextCursor: special-case emoji in deletePreviousChar()
    * Fixed deletePreviousChar() (Backspace) to delete entire emoji
      sequences (e.g. emoji with skin tone modifiers, ZWJ sequences,
      keycap sequences, or flag emoji) in a single keystroke, while
      preserving the existing per-codepoint deletion behavior for non-
      emoji grapheme clusters such as Devanagari or Thai.

* 2cf8cec9b79 a11y Android: Listen to ACTION_SHOW_ON_SCREEN and pass it
  to QAccessible
    * React to the A11y ACTION_SHOW_ON_SCREEN signal.

* 23442ca37a3 qfloat16: add missing unary operator+
    * Added unary operator+, to complement the API.

* 4cc6c8bfbb6 qfloat16: add increment and decrement operators
    * Added increment and decrement operators.

* c06d96392f6 QSortFilterProxyModel: add protected slot to ignore source
  dataChange
    * QSortFilterProxyModel now has a dataChangeRelevances protected
      slot for subclasses to redeclare and allow them to indicate
      whether a source data change is relevant to them. This can be used
      as a performance optimization.

* cca990f6f97 Make QTZ::hasTransitions() conform to its documentation
    * QTimeZone::hasTransitions() has always been documented to answer a
      question about the backend capabilities, not the individual
      zone. (This is in contrast with hasDaylightTime(), which does
      answer a zone- specific question.) On Windows and Darwin, however,
      the implementations answered whether the zone had
      transitions. From 6.12 they shall, correctly, report the backend
      capability.

* 318a7dbaa7d wayland: Support XdgSessionManager
    * Update wayland-protocols

* cb18a8e32ca Modernize QMainWindow's unified title and toolbar mode
    * QMainWindow's unified title and toolbar mode is no longer
      implemented via the deprecated textured NSWindow style mask and
      content border thickness. Instead it's handled via
      Qt::ExpandedClientAreaHint and Qt::NoTitleBarBackgroundHint, with
      a dedicated NSVisualEffectView for the titelbar background where
      applicable.

* b8641962e8b CMake/Android: switch to Gradle over javac in Android
  builds
    * Switch to Gradle over javac for Android Jar builds.

* 7f9f09a0e38 Add Qt::InputMethodHint::IhmNoFullscreen to affect IM
  sizing
    * Added Qt::InputMethodHint::IhmNoFullscreen to request that the
      platform should not make input method panels fullscreen.

* 0ce1367e710 QAIM: promote private helper for QVariant comparison to
  protected API
    * QAbstractItemModel::compareData is a new protected helper that
      model implementors can use to compare two QVariants, optionally
      using a QCollator to configure the exact sorting behavior.

* b3a9ad3f651 Update VulkanMemoryAllocator to v3.3.0
    * Updated VulkanMemoryAllocator to 3.3.0

* 2cd781551b8 QRM: add interfaceVersion method
    * QRangeModel in Qt 6.11 broke binary compatibility with Qt 6.10 by
      adding a new implementation for multiData. If you are using
      QRangeModel, recompile your code if calls to QRM::data() or
      QRM::multiData() fail to return valid data.

* c7fe11a6e73 Maintain stable frame position and size for
  Qt::ExpandedClientAreaHint
    * Setting the Qt::ExpandedClientAreaHint now correctly expands the
      window's geometry, to give a consistent frame geometry.

* 7df0e02850c QCalendarPermission: Add WriteOnly access mode
    * Added QCalendarPermission::WriteOnly access mode.

* 669e3b3ef30 Android: call moveTaskToBack() instead of exit on back key
    * moveTaskToBack() on back key instead of app exit.

* d46c50d3543 QRM: add supportedDrag/DropActions as properties
    * A QRangeModel's support for drag'n'drop actions can be configured
      using the new supportedDragActions and supportedDropActions
      properties.

* d86e0a23fea QRM: set ItemIsDrag/DropEnabled flags if there are mime
  types
    * The flags() implementation sets the ItemIsDragEnabled flag for all
      items in a model that supports mime types (including the default
      mime type), and the ItemIsDropEnabled flag for items in models
      that are not read-only. ItemIsDropEnabled is also set for the
      invalid index to allow dropping of data into empty spaces of a
      view.

* e9df4df9317 QVectorND: add qHash() overloads
    * Added qHash() overload. If you defined your own, even though you
      didn't own the type, you should wrap QVector2/3/4D in a custom
      type (that you actually own), and define a qHash() for that
      instead.

* ea4b5ce6a4e Android: add support for Qt::ImhNoEditMenu hint
    * Added support for the Qt::ImhNoEditMenu input method hint on
      Android, which suppresses the built-in edit popup menu for text
      input fields.

* 4ca5d74a86c iOS: Embed shared library dependencies into app bundles
  automatically
    * Qt frameworks and other shared library dependencies are now
      automatically embedded into iOS app bundles when using a shared
      build of Qt with the Xcode generator. Set
      QT_NO_XCODE_EMBED_FRAMEWORKS on the app target to opt out.

* db9a9f50197 CMake: Increase minimum required CMake version to 3.25
    * Building and using Qt now requires at least CMake version 3.25.

* 6c12b7323db macOS: Use ScreenCaptureKit for QScreen::grabWindow
    * QScreen::grabWindow now uses ScreenCaptureKit instead of the
      deprecated CGDisplayCreateImageForRect. A permission dialog will
      still be shown on first capture, if the application does not have
      permission to capture all applications. Once such permission is
      given another dialog will occasionally be presented to the user,
      informing them that the app is doing non-interactive screen
      recording.

* 497c1d120ef QAIM: use QVariant::compare in compareData before
  comparing as strings
    * The implementation of lessThan now compares the two QVariants
      using the new QAbstractItemModel::compareData helper. This uses
      QVariant::compare, falling back to comparing the variants as
      strings only if this produces an unordered result.

* c596e7af244 Make Qt default to being relocatable on Apple platforms,
  even for static
    * Non-sandboxed apps on macOS, built against a custom static build
      of Qt with -feature-relocatable enabled, will no longer use the
      app's executable location as basis for the QLibraryInfo prefix
      path. To adjust the prefix path explicitly, use an explicit
      qt.conf.

* 4adcacbd033 Apple: Make QStandardPaths::TemplatesLocation not
  supported
    * QStandardPaths::writableLocation(TemplatesLocation) and
      standardLocations(TemplatesLocation) no longer return a path under
      the application's Documents directory, matching the existing
      documentation that lists TemplatesLocation as not supported on
      iOS.

* b3f968687ce iOS: Remove duplicate writable path from PicturesLocation
  list
    * QStandardPaths::standardLocations(PicturesLocation) no longer
      contains a duplicate entry for the writable Documents/Pictures
      path.

* ee58a085f65 QRM: default construct items managed by owning pointers in
  setData
    * In models that store default- constructible items as owning
      pointers, calling setData on an uninitialized item now default-
      constructs the item if needed.

* d27e5e5540d QSharedPointer: add qSharedPointerStaticCast
    * Added qSharedPointerStaticCast.

* cfda2da6b60 iOS: Stop synthesizing PublicShareLocation and document
  the actual path
    * QStandardPaths::PublicShareLocation on iOS now returns
      "<APPROOT>/Public" (under the sandbox container root), matching
      what NSSharedPublicDirectory resolves to, instead of the
      previously synthesized "<APPROOT>/Documents/Public" inside the
      application's Documents directory. Applications relying on user-
      visible behavior via the Files app should use
      QStandardPaths::DocumentsLocation.

* 37608cbd4fb macOS: Include system-wide /Library/Preferences in config
  locations
    * QStandardPaths::standardLocations() now includes the system-wide
      /Library/Preferences directory for ConfigLocation,
      GenericConfigLocation, and AppConfigLocation, matching the
      behavior of the data and cache locations.

* d0067948c55 rhi: add a ShaderDrawParameters feature flag
    * Added QRhi::ShaderDrawParameters to query support for
      gl_BaseInstance, gl_BaseVertex and gl_DrawID when using indirect
      and multi-draw pipelines.

* 38ea699049b Update D3D12MemoryAllocator to v3.1.0
    * Updated D3D12MemoryAllocator to 3.1.0

* 544aa70c93c QGtk3Dialog: Support QFontDialog filtering options
    * The native GTK3 font dialog now supports the QFontDialog font
      filtering options.

* ec2e49beb53 rhi: allow texture render targets to select a depth array
  layer
    * Texture render targets can now attach a single layer of a depth
      texture array as their depth/stencil attachment.

* c1ba3a3bd5c QDesktopUnixServices: remove fallback for a
  !QT_CONFIG(process) build
    * Configurations without QProcess will no longer fall back to the C
      library system call to launch the external process for opening
      URLs.

* 5d672e5468f QDesktopUnixServices: use the portal if available in
  open{Document,Url}
    * On XDG Unix systems like Linux and FreeBSD, this class will now
      prefer to use the XDG desktop portal D-Bus service (if available)
      to conclude its actions, instead of using the xdg-open application
      or another fallback. There may be differences in behavior on how
      the portal acts versus what the application does.

* 63b93c90d23 Android: bump to Gradle 9.5.1 and AGP 9.2.1
    * Updated Gradle to 9.5.1 and AGP to 9.2.1.

* 87c5b3e99c6 QDom: Change default InvalidDataPolicy to ReturnNullNode
    * The default InvalidDataPolicy has changed from AcceptInvalidChars
      to ReturnNullNode. Factory functions in QDomDocument now return a
      null node when called with data invalid per XML 1.0, instead of
      silently accepting it.

* 002acd47bb3 Apple: Follow bundle conventions for paths in bundled
  applications
    * QLibraryInfo paths for bundled applications now follow bundle
      structure conventions such as Frameworks, PlugIns and Resources,
      removing the need for a qt.conf in most cases.

* 91c39b355d7 macdeployqt: Stop writing a qt.conf into the bundle
    * macdeployqt no longer writes a qt.conf into the deployed bundle.
      Bundled applications now resolve their plugin and QML import paths
      from the bundle layout directly.

* 18d550d9d2b moc: Add support for #include_next
    * moc now supports the #include_next preprocessor directive.

* 8e78bf1f1c3 moc: Add support for __has_include_next
    * moc now supports the __has_include_next preprocessor operator.

* 24f48f1e677 QXmlStreamEntityResolver: protect resolveEntity() against
  premature use
    * , as this is \internal API.

* 4d542c62aa3 QRandomGenerator: control insecure PRNG fallback behavior
    * QRandomGenerator now warns when it falls back to using insecure
      PRNG for generating the random value. The new
      FEATURE_randomgenerator_disable_fallback can be used to disable
      such fallback at compile time and terminate the application if
      CSPRNG is not available for some reason.

* 532f6c08815 QAccessible*Interface: disable copying
    * The QAccessible*Interface classes were made uncopyable. As
      polymorphic types, they shouldn't be.

* 3a743101a04 QSet: add missing insert(cit, T&&) overload
    * Added insert(const_iterator, T&&) overload.

* 9a2bd5ae09b Deprecate Q_FLAGS and Q_ENUMS
    * Use of deprecated Q_FLAGS and Q_ENUMS macros now causes
      deprecation compiler warnings on compilers that support
      deprecating preprocessor macros (only Clang and MSVC, at this
      time).

* 070d00ac040 Update our copy of Linux's perf_event.h to version 7.0
    * QtTest's benchmarks now use the version of Linux's perf_event.h
      from kernel version 7.0

* 71ffdf8e7b0 QSet: add rvalue-this overload of values()
    * Added rvalue-this overload of values().

* 850a1343a24 qpa/wayland: Only enable text-input-v3 surfaces when
  needed
    * Make it so that surfaces under text-input-v3 are only enabled if
      they are entered and want to receive text input.

* 7777c16bcfd iOS: Default to the host architecture for simulator builds
    * Qt builds for the iOS simulator SDK now default to the host
      architecture, instead of always defaulting to x86_64.

* bcbb05d4f77 Keep the OpenGL shader cache in the application-specific
  location
    * The OpenGL program binaries are now stored in the application-
      specific cache location, not the generic (shared) one, in order to
      alleviate security concerns. This change is not applicable when
      using Qt Quick, since the modern QRhi-based program/pipeline cache
      mechanism in Qt Quick has always used the per-application cache
      location. This patch makes the legacy OpenGL program binary cache,
      and so applications that directly use APIs such as
      QOpenGLShaderProgram, behave similarly.

* 7d1638279b5 Update date and time parsing and serialization
  documentation
    * Core functions to parse dates, times and datetimes now handle
      single quotes in their format strings the same way as
      serialization does. In particular, a backslash no longer escapes a
      single quote between single quotes (this was never the documented
      behavior, but used to work); instead, use a pair of adjacent
      single quotes, which is always read as a simple single quote
      rather than the start or end of a verbatim text.

* 2c08493c62d QNetworkProxy: support socks5h scheme with libproxy
  backend
    * The class now supports a scheme of "socks5h" in *_PROXY
      environment variables, when using the libproxy backend on Unix
      systems ("socks5h" indicates the SOCKS5 server is capable of
      resolving hostnames).

* f17fdd13ca2 Document license for XSVG in Qt Gui
    * Code based on XSVG moved from Qt SVG to Qt GUI.

* a7daf78bc1d QTextTable: top-align cells that cross a page break
    * Fixed vertical alignment of table cells crossing a page break:
      cells with AlignMiddle or AlignBottom that straddle a page
      boundary are now top-aligned.

* 0d5f0be1a19 CMake: Add QTP0007 policy to quote / escape deploy script
  arguments
    * Added the QTP0007 policy. When set to NEW,
      qt_generate_deploy_app_script() writes the values of the arguments
      it forwards to qt_deploy_runtime_dependencies(), like
      DEPLOY_TOOL_OPTIONS, as quoted arguments into the generated deploy
      script, so values containing whitespace, backslashes or double
      quotes, are passed on unchanged. Projects that added several
      option values into one whitespace-separated value, have to pass
      them as separate list elements when enabling the policy.

* ce913874322 CMake: Add QTP0008 policy to implement deploy commands as
  functions
    * Added the QTP0008 policy. When set to NEW, the version-less
      qt_generate_deploy_script() and qt_generate_deploy_app_script()
      commands are implemented as functions instead of macros, so
      argument values containing backslashes or ${var} references are
      passed on unchanged.

* 56a48ada92a QTextStream: deprecate op>>(char*)
    * Deprecated operator>>(char*) due to security concerns. Use
      operator>>(QByteArray&) instead.

* a726853b49e Long live QHttpHeaderRangeSet!
    * Added.

* 1913a0f92bd Add cancel() to QTest's touch event sequence
    * QTest::touchEvent() sequences gained a cancel() method to simulate
      a canceled touch sequence.

* a420ae5522d QXmlStreamReader: reject entityExpansionLimit()s <= 0
    * setEntityExpansionLimit() now rejects limits < 1. Such limits are
      not sensible: the built-in XML entities (&lt;, &gt;, ...) each
      expand to a single character, so a limit below 1 would cause even
      the simplest of XML files to be rejected as non-well-formed.

* 8566632bf9b QXmlStreamReader: fix entity expansion limit accounting to
  fit docs
    * Now enforces the entityExpansionLimit() exactly (was: allowed
      exceeding it by the top-level entity reference length, measuring
      the net length increase caused by the expansion).

* 4d51214d955 QByteArray: fix crash if zlib reurns Z_BUF_ERROR
    * Fixed a bug that could cause qUncompress() to crash or have
      undefined behavior on specific corrupted input streams.

* edf711fd5a0 Upgrade Harfbuzz to 14.5.0
    * Upgraded Harfbuzz to version 14.5.0

* 51906ad8769 QByteArray::fromPercentEncoding: don't leak information
  from the buffer
    * Fixed a bug that that left some bytes of the result of
      fromPercentEncoding() uninitialized if the input content was
      malformed, potentially leaking old heap contents.

### qtsvg
* 6b0aba55 QSvgIOHandler: Add animation support for QMovie/AnimatedImage
    * Animated SVGs can now be used with QMovie and QML AnimatedImage.

### qtdeclarative
* 4c4e7bbfa7 Make the rate at which to update hover and cursor
  configurable
    * You can now configure the minimum time interval between updating
      mouse hover and cursor when items animate under it, by setting
      QT_QUICK_FRAME_SYNCHRONOUS_HOVER_INTERVAL to a number of
      milliseconds. By default we use 100 milliseconds, to reduce CPU
      usage, rather than doing it before every frame rendered, as we did
      in previous Qt versions. It can also be set to -1 to send hover
      events and update the cursor only when the mouse moves, not when
      something moves under a stationary cursor.

* ea3c5d96bf Compiler: Rename FixSuggestion::fixDescription to
  description
    * The fixDescription on a QQmlSA::FixSuggestion has been renamed to
      description.

* f6617324df Compiler: Remove FixSuggestion::hint
    * The member QQmlSA::FixSuggestion::hint has been removed. It was
      unused.

* eeb25ba79c SpinBox: add text editing context menu
    * SpinBox now provides a ContextMenu by default. If you already have
      a custom context menu for it, ContextMenu will not open its own on
      e.g. right click.

* 60cc1b60f3 QtQml: Clean up calling of QObject methods
    * When calling invokable QObject methods that take QString arguments
      from JavaScript with null or undefined, those values are always
      correctly converted to "null" or "undefined", respectively, now.
      This is what JavaScript does when you coerce null or undefined to
      string. Previously, the values would be coerced to empty strings
      in some cases. Furthermore, when calling an invokable QObject
      method that takes a QVariant as argument with a JavaScript array,
      the JavaScript array is always coerced to a QVariantList now. This
      is in line with how JavaScript objects are coerced to QVariantMap
      in the same situation. Previously the JavaScript array was passed
      as QJSValue wrapped into QVariant in some cases.

* 5222eee20a Compiler: Rename logging categories' level into severity
    * The level property of of a warning category and whether that
      category is enabled  have been merged into a new property
      severity. As previously, the possible values are disable, info,
      warning, and error. Disabling a category can now be done by
      setting it to a severity of disable instead of explicitly
      disabling it. The QQmlSA was updated and some keys of the
      plugin.json files have changed accordingly.

* e6b698c2e7 QtQml: Do not instantiate components with missing required
  properties
    * When instantiating an object from QML using
      Component.createObject() and some of its required properties
      cannot be set due to type mismatches, the object creation is
      aborted now. This is in line with what happens if a required
      property is missing altogether.

* b10f78ed88 MenuItem: show action shortcut's key sequence
    * Shortcuts from actions are now shown by MenuItem. Set
      Qt::AA_DontShowShortcutsInContextMenus to disable this behavior.

* baf2205158 TestCase: deprecate optional property
    * Deprecated optional property. Use skip() instead.

* 37b9ac9d82 qmllint: Remove unused category
    * The restricted-type qmllint warning has been removed. It is now
      possible to use all combinations of enum scoping and access
      scoping.

* 75debe18ea qmllint: Add --only-explicit-categories option
    * You can now pass the --only-explicit-categories flag to qmllint.
      It disables all warning categories by default and only keeps the
      explicitly set ones. This can be used to automatically apply all
      fixits for a particular category. See the qmllint documentation
      for more details.

* 9421552937 Quick: Add the Color singleton
    * Added the Color singleton holding utility functions for colors.
      Most of these are typed versions of the same functions on the Qt
      global object.

* 5e923ea80f qmllint: move qmlTranslationMethodMismatch to qdslintplugin
    * The qmllint translation-function-mismatch warning category was
      moved to the Qt Design Studio plugin and renamed to
      QtDesignStudio.TranslationFunctionMismatch. All usages of the
      warning in command line arguments, qmllint disable comments, or
      config files need to be updated to the new name.

* b3cd1c53b9 QQmlSA: Remove QQmlSA pass debug classes and qmlPlugin lint
  category
    * The qmlPlugin logging category has been removed. It was disabled
      by default and not used by any qmllint warnings. Additionally, the
      DebugElementPass and DebugPropertyPass classes in QQmlSA have been
      removed.

* f55a093c97 Attached ToolTip: show automatically if visible not set
    * Added policy property that controls whether attached ToolTips are
      shown automatically if the visible property hasn't been explicitly
      set. The delay and timeout properties are also set automatically
      if they weren't explicitly set.

* ad5ecde6cf RangeSlider: add property to allow crossing handles
    * Added crossingEnabled property in RangeSlider.

* c62aa7abcc QuickControls: Add a "QtQuick.Controls.Native" style
    * There is a QtQuick.Controls.Native style now. Importing
      QtQuick.Controls.Native chooses the best-suited style for the
      platform you compile for at compile time. It therefore combines
      the benefits of compile-time style selection with the possibility
      to have a platform-specific look-and-feel for your application.

* 37a0bb4587 Add insertRow() to QQmlTreeModel
    * Added a new method to QQmlTreeModel that inserts a node into the
      list of parent's children at the given index.

* 3e9268dd81 QML: Add support for multiple arguments in String.arg()
    * String.arg() now accepts multiple arguments, allowing substitution
      of multiple placeholders in a single call. This protects against
      issues when arguments themselves contain placeholders.

* ea7503c8c5 Introduce QQmlEngine::setExternalSingletonInstance
    * added QQmEngine::setExternalSingletonInstance            for
      easier management  of singletons that interface            between
      C++ and QML.

* afaed1a839 Allow using QML_UNCREATABLE() with QML_SINGLETON
    * Allow QML_UNCREATABLE() with QML_SINGLETON.

* 124b09d10f QML: Add Qt.escapeHtml() function
    * Added Qt.escapeHtml() function that escapes HTML special
      characters in a string, wrapping QString::toHtmlEscaped().

* e44e7f61c8 Text: Support all QTextCharFormat::UnderlineStyle in Qt
  Quick
    * Added support for all QTextCharFormat underline styles
      (DashUnderline, DotLine, DashDotLine, DashDotDotLine,
      WaveUnderline, SpellCheckUnderline) and underline colors in Text,
      TextEdit and TextInput elements when using the RHI renderer. The
      software renderer falls back to SingleUnderline for all styles.
      This enables proper rendering of IME composition indicators,
      spell-check underlines, and syntax highlighter underline styles in
      Qt Quick.

* 95898cacd0 a11y Android: Listen to ACTION_SHOW_ON_SCREEN and pass it
  to QAccessible
    * React to the A11y ACTION_SHOW_ON_SCREEN signal.

* 785b676f73 Add highlightOnHover to prevent changing highlightedIndex
  by hovering
    * Added highlightOnHover property to control whether hovering over
      items changes the highlightedIndex.

* 74eeda555f Use sourceModel property in the QML SFPM instead of model
    * The `model` property of SortFilterProxyModel is deprecated. Use
      `sourceModel` property instead.

* 61ab4ea724 Use resource file mapper in qmlpreview
    * The qmlpreview command line utility can now resolve qrc paths to
      local files and update the preview if local files associated with
      QML documents loaded from the resource file system change. Use the
      --resource command line option to inform qmlpreview about the
      resource file system for your program.

* 1a24cc3200 Add _qmlpreview build targets for QML modules
    * The CMake build system now offers a <exe>_qmlpreview target for
      each executable with a QML module. When you "build" that target,
      the build system starts the qmlpreview utility with the correct
      arguments and allows you to QML-preview your executable. In
      particular it automatically resolves the .qrc file paths.

* ceedc35ead Adjust length when writing out of bound on QmlListWrapper
    * Lists of type `list<QtObject>` or similar will adjust their length
      when writing to them out of bounds. This is in line with how JS
      arrays adjust their length on out-of-bound accesses.

* d488549225 QML SFPM: Rename 'sort' to 'compare' in FunctionSorter
    * FunctionSorter: the designated QML method has been renamed from
      'sort' to 'compare'.

* 31296fd078 Menu: add separatorsCollapsible property
    * Added separatorsCollapsible property that automatically hides
      orphaned menu separators when adjacent items are hidden
      dynamically.

* 4c61813534 QtQuick: Provide RESET accessor for Rectangle.color
    * You can now reset the color of a Rectangle (for example by
      assigning undefined to the property in QML).

* 3c560a156d Prevent Item to get dirty when effectively invisible
    * Items that are effectively invisible no longer trigger re-
      rendering the scene.

* daa2b2d087 AnimatedImage: add loops, finishBehavior and finished()
    * Added loops, finishBehavior properties and finished() signal to
      control animation repetition, matching the existing AnimatedSprite
      API.

* d0e43ab2f4 Improve function filter with roles being specified as
  separate arguments
    * The filter method in SortFilterProxyModel has been refactored to
      use separate role arguments instead of a synthetic type for
      improved readability.

* 24ebb6f00b QML SFPM: Add AllOfFilter and AnyOfFilter composite filters
    * Added AllOfFilter and AnyOfFilter composite filter types that
      group child filters with logical AND and OR respectively. Both
      types support nesting, enabled, and inverted properties.

* 8bc3054bea QQuickColorValueType: Add rgba property
    * Added property rgba to the color value type. This property returns
      the QColor::rgba() value of the color.

* 526e2985f2 QQuickText: use ObjectReplacementCharacter for inline
  images
    * Inline images in StyledText now participate correctly in text
      eliding, wrapping, and line breaking.

* 47aec5d16d Implement QQmlTreeModel::moveRows()
    * Added a new method to QQmlTreeModel that moves a node with its
      children inside the tree.

* 369e91214d QmlModels: Add RegExpFilter for QML SortFilterProxyModel
    * Added RegExpFilter for SortFilterProxyModel.

* 0f70ac3fc6 QmlModels: Add RangeFilter for QML SortFilterProxyModel
    * Added RangeFilter for SortFilterProxyModel.

* 51dfeb00f8 qml: Add option to quit automatically after some time
    * The qml commandline tool now accepts a parameter to automatically
      quit after some time.

* 8b3c722553 SearchField: Navigate suggestions with keys when the text
  is empty
    * SearchField now allows navigation with keys if its TextInput is
      empty.

* eb25b82d40 a11y: Implement QAccessibleViewportInterface for
  QQuickListView
    * QML ListView now exposes its visible item range and total item
      count to screen readers via QAccessibleViewportInterface.

* f118798234 CMake: Remove QML plugin symlinks from Resources of
  deployed bundles
    * Deployed macOS app bundles no longer contain symlinks to QML
      plugin binaries under Resources/qml. The plugins are deployed to
      PlugIns and located via the plugin search path.

* a6749c7582 CMake: Source the build-dir qt.conf from the QML import
  scanner
    * The qt.conf generated next to an executable in the build directory
      now records QML modules that are imported only from QML (without a
      corresponding CMake dependency), by sourcing the import paths from
      qmlimportscanner in addition to the declared dependencies.

* 32c260cc6a Introduce QQuickPopup::ClosePolicy::CloseMultiple
    * Added flag CloseMultiple. Setting this flag combination with
      CloseOnRelease*/CloseOnPress* will cause non-top-most popups to
      close, when both the popup and it's child popups are clicked
      outside. This was previously the default behavior for popups with
      the Popup.Item popupType. The default behavior has been changed to
      always only close the top-most popup, unless this flag is used.

### qtmultimedia
* 62b1fa249 Quick: introduce source resolver to allow qml source
  rewriting
    * QSoundEffect will always emit sourceChanged after setSource.

* 785c3d521 Examples: audiosource - Add recording functionality
    * Added recording in audiosource example using dr_wav.

* d6eef6da2 QMediaMetaData: deprecate ThumbnailImage
    * QMediaMetaData::ThumbnailImage is deprecated. Backends will
      populate it with the same value as QMediaMetaData::CoverArtImage.

* a950b07dc wasm: use WebGL texImage2D for zero-copy VideoFrame upload
    * Video can now be handled by WebGL

* 8c79ec419 Introduce QGStreamerVideoSource class
    * Added private QGStreamerVideoSource class for setting a custom
      GStreamer video source element to a capture session.

* db9ff046d Make QGStreamerVideoSource attachable to
  QMediaCaptureSession
    * Added method QMediaCaptureSession::setNativeVideoSource allowing
      run specific native video pipelines.

* 89eeb6528 Implement GStreamerVideoSource for qml
    * Added GStreamerVideoSource qml element for setting a custom
      gstreamer camera element to a media capture session.

* 8119a0a73 CMake: add a feature to disable MultimediaQuick
    * Added the multimedia-quick feature. Configure with -no-feature-
      multimedia-quick to disable the Qt Multimedia Quick/QML
      integration even when Qt Quick is available.

* 7f71286a9 wasm: Replace OpenAL audio capture backend with Web Audio
  API AudioWorklets
    * QAudioSource now uses Web Audio API AudioWorklets instead of
      OpenAL, enabling browser-native low-latency capture.

* df6d97fa3 QScreen/WindowCapture: Add maximumFrameRate property
    * Added a maximumFrameRate property to QScreenCapture and QWindowCapture
      for setting a target frame rate.

* 22b672190 QNX: Add io-snd audio backend for QNX 8.0+
    * Added io-snd audio backend for QNX 8.0+, replacing the legacy QSA
      backend which remains available for older QNX versions.

* dac72847d macOS: Migrate window-capturing to ScreenCaptureKit
    * On macOS, theQWindowCapture backend has been migrated to use
      ScreenCaptureKit. QWindowCapture is now hardware-accelerated on
      macOS. The macOS "Screen Recording" permission dialog will now be
      triggered when enumerating capturable windows with
      QWindowCapture::capturableWindows().
      WindowCapture::capturableWindows() will now return an empty list
      if the user denies the "Screen Recording" permission.
      WindowCapture::capturableWindows() will no longer return windows
      that are not capturable, and will no longer include minor system
      UI elements such as the menu bar and dock.

* f273a88e9 Expose qgstreamerinterface as a part of spi (semi-private
  interface)
    * Add semi-private (spi) QGStreamerInterface which replaces
      QGStreamerPlatfromSpecificInterface.

* 994ece805 Introduce QFFmpegFrameRateAdapter
    * Setting QMediaRecorder::videoFrameRate now enables a frame rate
      adapter to preserve video duration and synchronization with audio.

* 34422d14a Migrate macOS screen capture to ScreenCaptureKit
    * On macOS, the QScreenCapture backend has been migrated to use
      ScreenCaptureKit. QScreenCapture will no longer request screen
      recording permissions when constructed, but rather whenever
      .setActive(true) is called.

* 9c8e0d9ce Update signalsmith-stretch QtMM third-party
    * signalsmith-stretch updated to v1.1.0

* a90f61390 FFmpeg: Point documentation to FFmpeg version n8.1.2
    * FFmpeg has upgraded to version n8.1.2.

* cc84d8756 3rdparty: update dr_wav snapshot
    * Update dr_wav to 0.14.6-snapshot-955edd32

* 31b7bbebd dr_libs: pull in upstream snapshot and fuzzing fixes
    * Update dr_wav to 0.14.6-snapshot-ee937527 and fix integer
      overflow/assertion failures.

* dbd7a47a8 FFmpeg: Point documentation to FFmpeg version 9.0.1
    * FFmpeg has upgraded to version 9.0.1.

### qttools
* dddb5be23 QDoc: Display explicitly defaulted functions
    * tag in the synopsis.

* 8ea2ab2e4 QDoc: Display explicitly deleted functions
    * tag in the synopsis.

* 6ecfdad36 QDoc: Validate template parameter documentation using \a
  command
    * The \a command now validates template parameter names. QDoc warns
      about undocumented template parameters in classes and type
      aliases, and about undocumented non-type or template-template
      parameters in functions.

* fe4d2974e QDoc: Allow customization of \preliminary status
  descriptions
    * The output generated by the \preliminary command can now be
      customized to match terminology used in the API documentation for
      work-in-progress entities.

* 51167e9ba QDoc: Allow documenting hidden friends without class prefix
    * Hidden friend functions can now be documented using their natural
      free-function syntax instead of requiring class-qualified names.

* efe584231 QDoc: Honor list start values of zero and below
    * The \list command now correctly honors start values of zero and
      below (such as \list 0 or \list -5).

* 8b1ca61f1 QDoc: Use actual header files for include statements
    * Include statements in class documentation now reflect actual
      header file names. Projects using Qt-style convenience headers
      continue to work automatically.

* d4b6e0678 QDoc: Decouple index file generation from HtmlGenerator
    * Index files are now generated in the base output directory rather
      than format-specific subdirectories. Projects requesting multiple
      output formats will produce a single index file instead of
      duplicates in each format directory.

* 170190584 QDoc: Add Markdown output support to TemplateGenerator
    * The template generator now produces Markdown output if you set
      template.extension = md in the configuration.

* 713d4a852 QDoc: Make recognized code languages configurable
    * The programming languages that QDoc accepts in code blocks has
      been made configurable, allowing code that will be marked up using
      online tools to be included in documentation without warnings.

* 73438a25f QDoc: Improve parsing of \qmlmethod and \qmlsignal arguments
    * QDoc now warns if \qmlmethod signatures do not document the return
      type.

* f2e56b6b0 QDoc: Render SFINAE constraints as requires clauses
    * Functions using enable_if-based SFINAE constraints now display
      requires clauses in the documentation output.

* 0b831cc7e CMake: Add LLVM 22 to supported QDoc Clang versions
    * QDoc now supports Clang from LLVM 22.

* ad652e3fc QDoc: Add \qmluncreatabletype topic command
    * QDoc now detects QML_UNCREATABLE macro and also has a
      \qmluncreatabletype topic command to explicitly document a QML
      type as uncreatable.

* f0df12af9 Add Objective-C name mangler tool
    * Added the objcnamemangler tool and the qt6_mangle_objc_symbols()
      CMake function for patching Objective-C symbol namespaces in
      Mach-O binaries at build time.

* 50aab7bad QDoc: Introduce InternalAuto Node status
    * Introduced a new InternalAuto status for entities that are
      automatically determined to be internal. In .index files, this is
      visible as status="internal-auto" attribute.

* d115dde1b QDoc: Introduce 'parsecppcomments' configuration variable
    * Setting 'parsecppcomments' configuration variable to 'no' turns
      off C++ documentation parsing and speeds up generation of QML-only
      documentation sets.

* 69046206a Qt Widgets Designer: Add a local socket client option taking
  a server name
    * In addition to the existing TCP client option allowing to remotely
      open .ui files, a local socket client option taking a server name
      has been added.

### qtpositioning
* 0edc43e6 Fix QGeoAreaMonitorPolling implementation
    * The startUpdates() and stopUpdates() methods of the underlying
      position source are now always invoked via a QueuedConnection.
      This means that they are always executed in the same thread where
      the source lives. Previously e.g. the stopUpdates() method could
      be executed from the thread where the last watcher lives. It also
      means that the updates are stopped not immediately after the last
      watcher is disconnected, but when the control reaches the event
      loop in the source's thread.

* 07bd7beb Add IRNSS and SBAS satellite systems
    * The SatelliteSystem enum is extended to report two new satellite
      types: IRNSS and SBAS. These are properly recognized using nmea
      and android backends.

### qtconnectivity
* e58324a2 Rework LE advertising on Android
    * The Android backend now respects the advertising minimum and
      maximum interval parameters provided via
      QLowEnergyAdvertisingParameters when starting the BTLE
      advertising.

### qtwayland
* a8cd81790 Implement version 4 of linux-dmabuf
    * Added support for linux-dmabuf-v1 stable protocol, version 4. To
      use it, select "linux-dmabuf-v1" as the client buffer integration.
      The old (version 3) implementation can still be used under the
      name "linux-dmabuf-unstable-v1" for compatibility.

### qtimageformats
* 8550f4fb Update bundled libtiff to version 4.7.2
    * Bundled libtiff was updated to version 4.7.2

* 41c34040 Fix config behavior of mng and jasper from "auto" to "no",
  matching doc
    * The mng and jasper (jpeg2000) image format handlers are no longer
      built by default if the required codec libraries are found on the
      system, but must be explicitly requested in the configure options.
      This matches the configure help documentation for those options.

### qtvirtualkeyboard
* 9194888b Add plugin parameter handling
    * It is now possible to append plugin parameters to QT_IM_MODULE.

### qtquick3d
* 5febd8b7c SSR: expose more properties
    * Add ExtendedSceneEnvironment::ssrMaxSteps property

* 0a6a58b8c Add manual LOD factor for instancing
    * Added instancingLodFactor property to manually select the LOD
      level when rendering an instance table.

* c56711cd9 Add QQuick3DQuadTextureProvider
    * Added QQuick3DQuadTextureProvider

* 35479bd21 Add SkyMaterial
    * Added SkyMaterial QML type and SceneEnvironment::skyMaterial
      property.

* 8fe7f89a7 SkyMaterial: add screenspace mode and multi-view support
    * Added the skyboxMode property for direct screen-space sky
      rendering, decoupled from the IBL cubemap.

* fa987e1f6 Update meshoptimizer to 1.2
    * meshoptimizer was updated to version 1.2.

* 35df9d013 Update the bundled OpenXR SDK to 1.1.61
    * The bundled OpenXR SDK was updated to version 1.1.61.

### qtshadertools
* 89ee6f7 CMake: Hide verbose output of qt_add_shaders() by default
    * qt_add_shaders() 'X.vert -> X.vert.qsb exposed as ://Y' messages
      are now logged at DEBUG level instead of NOTICE level, which will
      hide them from the configuration output by default.

* c73fa5a Update SPIRV-Cross
    * SPIRV-Cross has been updated to current HEAD.

* 3b13852 Update glslang to 16.3.0
    * glslang has been updated to 16.3.0

### qt5compat
* 2931727 Deprecate QBinaryJson::toRawData() immediately in 6.12
    * Deprecated the toRawData() method, because the returned memory has
      to be manually released by the user, in stark contrast to Qt 5,
      where it remained owned by the object. A backward-compatible
      alternative is to use toBinaryData() instead.

* 89bbdb3 QXmlSimpleReader: fix unbounded recursion when parsing nested
  elements
    * Fixed a stack overflow when parsing documents with very deeply
      nested elements.

### qtopcua
* 719131a6 Port to open62541 v1.5
    * The open62541 plugin now loads the files in the
      issuerListDirectory() and issuerRevocationListDirectory()
      directories.

* 9b195c2f Update bundled open62541 to v1.5.7
    * The bundled open62541 was updated to v1.5.7

### qthttpserver
* 00f7eb0 Limit the number of connections for each IP address
    * Added configurable limit to the number of active connections for
      each IP address.

* cc82a6a Limit the number of simultaneous connections
    * Added configurable limit of total simultaneous connections.

### qtquick3dphysics
* 8041a3d Add basic joints support
    * Add basic joints support with DistanceJoint, FixedJoint,
      PrismaticJoint, RevoluteJoint and SphericalJoint qml elements.

* a1c0197 Correct PhysX attribution metadata
    * Corrected the recorded upstream commit, copyright holders and
      version string of the bundled NVIDIA PhysX SDK, and added a PURL
      for SBOM generation.

### qtgrpc
* 25a55b55 qtprotobufgen: Generate QtProtobuf messages as 'final' in
  6.11
    * Generated QtProtobuf message classes are now final by default. A
      new GENERATE_NON_FINAL_MESSAGES option was added to restore the
      previous behavior for backwards compatibility.

* 364c4760 Make the FINAL attribute of QtProtobuf class properties
  configurable
    * Generated QtProtobuf message properties are now FINAL by default.
      A new GENERATE_NON_FINAL_PROPERTIES option was added to restore
      the previous behavior for backwards compatibility.

* 3bd1f97a Add correctly named Q_PROPERTY for repeated message fields
    * Added correctly named Q_PROPERTY declarations for repeated message
      fields. The old *Data-suffixed properties are deprecated and will
      be removed in Qt 7.

* 8c8f0e3c QGrpcHttp2Channel: reject messages exceeding a configurable
  size limit
    * Added setMaximumReceiveMessageSize() to limit the size of incoming
      messages. The default is 4 MiB, matching the gRPC specification.
      The environment variable QT_GRPC_MAXIMUM_RECEIVE_MESSAGE_SIZE
      provides a global override without requiring code changes.

* de604ccd QGrpcChannelOptions: allow narrowing accepted compression
  algorithms
    * Added setAcceptedCompressionAlgorithms() and
      supportedCompressionAlgorithms() to control accepted server
      compression. Pass an empty set to refuse it.

* bdea8cf7 QGrpcHttp2Channel: implement client-side request compression
    * Added setRequestCompression() to compress outbound RPC payloads
      with gzip or deflate. Call options take precedence over channel
      options.

* 2c8eaf65 QGrpcHttp2Channel: drain the outgoing queue iteratively
    * Fixed a stack overflow that could crash the client when burst-
      writing a very large number of messages on a client-streaming or
      bidirectional RPC.

* 15cfbac8 QGrpcHttp2Channel: raise the default HTTP/2 receive window
    * The default HTTP/2 receive window was raised from 64 KiB to 4 MiB
      per stream and 16 MiB per connection. The per-stream window can be
      tuned via the QT_GRPC_HTTP2_STREAM_RECEIVE_WINDOW_SIZE environment
      variable and the connection window via
      QT_GRPC_HTTP2_CONNECTION_RECEIVE_WINDOW_SIZE

* 2cedde7a QGrpcHttp2Channel: add reconnect backoff and connect timeout
    * The channel no longer reconnects immediately after a connection
      failure. It now applies exponential backoff with jitter, starting
      at 1 s and capped at 120 s, and aborts a single connection attempt
      that hangs for more than 20 s. The environment variables
      QT_GRPC_INITIAL_RECONNECT_BACKOFF_MS,
      QT_GRPC_MAXIMUM_RECONNECT_BACKOFF_MS, and
      QT_GRPC_CONNECT_TIMEOUT_MS override the three defaults.

* c4719934 QGrpcHttp2Channel: add a configurable maximum metadata size
    * The channel now rejects metadata larger than 16 KiB, matching the
      gRPC specification. The environment variable
      QT_GRPC_MAXIMUM_METADATA_SIZE overrides the limit.

### qtgraphs
* ffae6892 Add RegisterEnumClassesUnscoped to classes with scoped enums
    * QGraphsView, QBarDataProxy, and QSurface3DSeries now register
      their scoped enums to QML as scoped, matching their C++ semantics.
      Code relying on unscoped access to ZoomStyle, PanStyle,
      RemoveLabels, or Shading enumerators from QML needs to be updated
      to use the scoped names.

* 8ac251da Fix GUI/render-thread data race in canvas-painter 2D
  renderers
    * 2D graphs can now be rendered with QCanvasPainter.

* 973bac0d Fix GUI/render-thread data race in canvas-painter custom
  series
    * Custom 2D series can now be rendered with QCanvasPainter.

* 6b319ed8 Change public setters in widgetitems to public Q_SLOTS
    * The public setters in widget items are now declared as slots.

### qtopenapi
* 9b1e946 De-virtualize generated api operation methods
    * Generated client API methods are no longer virtual.

* 03484d1 Replace fromJsonObject/asJsonObject API with
  fromJsonValue/asJsonValue
    * The fromJsonObject/asJsonObject API methods of the generated
      objects and models are replaced with fromJsonValue/asJsonValue.

* 649b21d Rename generated model property getters and state checkers
    * Generated model property getters no longer carry a Value suffix
      (getName() instead of getNameValue()), and the property state
      checkers use a Value infix (isNameValueSet(), isNameValueValid()).
      Q_PROPERTY now exposes the property name directly.

* 77bba94 Give user a possibility to choose a policy for saving files
    * add setFileConflictPolicy() and fileConflictPolicy() API.


Fixes
-----

### qtbase
* [QTBUG-137726](https://qt-project.atlassian.net/browse/QTBUG-137726) Highlighted text color remain black in windows11 style
* [QTBUG-141772](https://qt-project.atlassian.net/browse/QTBUG-141772) openSUSE 16.0 qtbase -
tst_QComboBox::popupPositionAfterStyleChange() Compared values are not
the same
* [QTBUG-142030](https://qt-project.atlassian.net/browse/QTBUG-142030) Color picking not working on multi-monitor setup with
different scaling factors
* [QTBUG-117424](https://qt-project.atlassian.net/browse/QTBUG-117424) qmake generates outdated C++ language level options for
gcc like c++1z for C++17
* [QTBUG-142078](https://qt-project.atlassian.net/browse/QTBUG-142078) precompiled headers not populated when linking Private
libs
* [QTBUG-129754](https://qt-project.atlassian.net/browse/QTBUG-129754) Top flaky test: tst_qgesturerecognizer::touchReplay
* [QTBUG-141984](https://qt-project.atlassian.net/browse/QTBUG-141984) qnetworkproxy_win.cpp has always true condition
* [QTBUG-142819](https://qt-project.atlassian.net/browse/QTBUG-142819) The "minimal" QPA plugin still uses GDI font backend
* [QTBUG-143185](https://qt-project.atlassian.net/browse/QTBUG-143185) Quick3D material shader cache not generated on Windows
with OpenGL and Intel graphics
* [QTBUG-143115](https://qt-project.atlassian.net/browse/QTBUG-143115) QPushButton stylesheet rendering issue: 1px dashed
border incorrectly rendered as dotted
* [QTBUG-143873](https://qt-project.atlassian.net/browse/QTBUG-143873) Circular header dependency in text classes
* [QTBUG-143841](https://qt-project.atlassian.net/browse/QTBUG-143841) QMainWindow::tabifyDockWidgets() is a visual no-op,
leaks memory and causes crashes on floating dock widgets
* [QTBUG-144106](https://qt-project.atlassian.net/browse/QTBUG-144106) AddressSanitizer: odr-violation: global
'm_wl_output_listener' defined in both  libQt6WlShellIntegration.so.6
and  libQt6WaylandClient.so.6
* [QTBUG-143775](https://qt-project.atlassian.net/browse/QTBUG-143775) QFileSystemModel data corruption and segmentation faults
during frequent filesystem updates
* [QTBUG-144335](https://qt-project.atlassian.net/browse/QTBUG-144335) [REG 6.11.0 -> 6.12.0] tst_QIcon_Svg::svgActualSize()
Compared values are not the same
* [QTBUG-144480](https://qt-project.atlassian.net/browse/QTBUG-144480) Visual Studio 2026 / MSVC2026 compiler error:
tst_qvariant
* [QTBUG-143786](https://qt-project.atlassian.net/browse/QTBUG-143786) QOpenGLWindow can't opaque on Gnome wayland
* [QTBUG-144394](https://qt-project.atlassian.net/browse/QTBUG-144394) [REG 6.11.0 -> 6.12.0] tst_parserstress (Failed)
* [QTBUG-140725](https://qt-project.atlassian.net/browse/QTBUG-140725) QWinRegistryKey inconsistent handling of data members in
swap()/move-SMFs
* [QTBUG-129567](https://qt-project.atlassian.net/browse/QTBUG-129567) tst_QWidget_window::tst_dnd_events() timeout on Ubuntu
24.04 GNOME X11
* [QTBUG-143862](https://qt-project.atlassian.net/browse/QTBUG-143862) QImageReader::size() does not account for image rotation
* [QTBUG-144715](https://qt-project.atlassian.net/browse/QTBUG-144715) QtWayland TextInput v1 Coordinate Bug Demo
* [QTBUG-144821](https://qt-project.atlassian.net/browse/QTBUG-144821) [REG 6.11.0 -> 6.12.0] tst_qtexttospeech (Failed)
* [QTBUG-143158](https://qt-project.atlassian.net/browse/QTBUG-143158) New example linguist/localizedclock-idbased fails to
compile on Wasm
* [QTBUG-144923](https://qt-project.atlassian.net/browse/QTBUG-144923) QUrlQuery's move constructor is out-of-line (should be
inline)
* [QTBUG-144961](https://qt-project.atlassian.net/browse/QTBUG-144961) QFont/Info/Metrics/F are missing move SMFs
* [QTBUG-144813](https://qt-project.atlassian.net/browse/QTBUG-144813)  [REG 6.11.0 -> 6.12.0] FAIL!  :
tst_protobuf_enumtypes_qml::tst_enumtypes::compile() module
"qtprotobufnamespace.tests.enums" is not installed
* [QTBUG-144820](https://qt-project.atlassian.net/browse/QTBUG-144820) [REG 6.11.0 -> 6.12.0] FAIL!  : data::tst_simulation-
behavior::compile() module "Simu" is not installed
* [QTBUG-88089](https://qt-project.atlassian.net/browse/QTBUG-88089) Make CMake artifacts configuration mergeable.
* [QTBUG-138610](https://qt-project.atlassian.net/browse/QTBUG-138610) QTemporaryFile::rename() overwrites existing file on
Android
* [QTBUG-145185](https://qt-project.atlassian.net/browse/QTBUG-145185) QtProcessConfigureArgs.cmake does not recognize . as
RELATIVE_PATH
* [QTBUG-144515](https://qt-project.atlassian.net/browse/QTBUG-144515) QEventDispatcherUNIX: wake-up pipe drained before posted
events from handler are processed
* [QTBUG-145008](https://qt-project.atlassian.net/browse/QTBUG-145008) wasm: eventloop/main_exec manual test crash
* [QTBUG-140144](https://qt-project.atlassian.net/browse/QTBUG-140144) REG: Qt 6.9.1 -> 6.9.2: QFileDialog (non-native) is
missing some icons for directories
* [QTBUG-95817](https://qt-project.atlassian.net/browse/QTBUG-95817) Quick windows break  on nvidia wayland when resized
* [QTBUG-112693](https://qt-project.atlassian.net/browse/QTBUG-112693) TextArea cannot delete multi-symbol emoji using
backspace at once, such as 👨‍👨‍👧‍👧
* [QTBUG-133843](https://qt-project.atlassian.net/browse/QTBUG-133843) Emoji is broken down into segments when deleting it
* [QTBUG-145393](https://qt-project.atlassian.net/browse/QTBUG-145393) eglSwapBuffers() is called on every touch move event on
an empty Window {} in Qt Quick on QNX
* [QTBUG-87665](https://qt-project.atlassian.net/browse/QTBUG-87665) tst_QOpenGL::fboMRT() fails on Android Emulator within a
virtual machine in the CI
* [QTBUG-143525](https://qt-project.atlassian.net/browse/QTBUG-143525) FileDialog not opening inside QDialog
* [QTBUG-142070](https://qt-project.atlassian.net/browse/QTBUG-142070) Freetype font engine cannot handle custom
QT_MAX_CACHED_GLYPH_SIZE correctly for software rendering
* [QTBUG-115232](https://qt-project.atlassian.net/browse/QTBUG-115232) Border artifact in link in QTextEdit
* [QTBUG-145714](https://qt-project.atlassian.net/browse/QTBUG-145714) tst_qmlwebsockets (Failed)
* [QTBUG-145715](https://qt-project.atlassian.net/browse/QTBUG-145715) tst_shapelayer (Failed)
* [QTBUG-135973](https://qt-project.atlassian.net/browse/QTBUG-135973) [REG 6.8 → 6.9] CMAKE add_custom_command with POST_BUILD
is not being evaluated after build but before
* [QTBUG-145737](https://qt-project.atlassian.net/browse/QTBUG-145737) Vulkan validation warning in tst_qrhi::oneDimTexture
* [QTBUG-140898](https://qt-project.atlassian.net/browse/QTBUG-140898) [REG 6.9.1->6.9.2] Wrong menu icons size with Windows
Vista style
* [QTBUG-144939](https://qt-project.atlassian.net/browse/QTBUG-144939) Scissor rectangle stays set with some rhi backends after
resetClipping()
* [QTBUG-143506](https://qt-project.atlassian.net/browse/QTBUG-143506) Fonts: Variable weight does not resolve weights
correctly on macOS with Freetype
* [QTBUG-143884](https://qt-project.atlassian.net/browse/QTBUG-143884) QFontMetrics::tightBoundingRect is not accurate
* [QTBUG-132888](https://qt-project.atlassian.net/browse/QTBUG-132888) CBDT fonts not detected as color on macOS with Freetype
engine
* [QTBUG-141851](https://qt-project.atlassian.net/browse/QTBUG-141851) Windows: Reg->6.5[?] [Qt]: Fonts are not displayed
correctly anymore
* [QTBUG-139010](https://qt-project.atlassian.net/browse/QTBUG-139010) QGraphicsScene background caching does not work well
with Windows fractional scaling
* [QTBUG-143485](https://qt-project.atlassian.net/browse/QTBUG-143485) [Reg 6.9.3 -> 6.10.1][Apple Pencil] Scrolling/dragging
gets cancelled when Apple Pencil's "Hover" mode is enabled
* [QTBUG-123853](https://qt-project.atlassian.net/browse/QTBUG-123853) QWizard not respecting dark mode on Windows with Fusion
* [QTBUG-128467](https://qt-project.atlassian.net/browse/QTBUG-128467)  Incompatible QTabletEvent::rotation() value for Apple
Pencil
* [QTBUG-128466](https://qt-project.atlassian.net/browse/QTBUG-128466) Incorrect QInputDevice::capabilities() value for Apple
Pencil
* [QTBUG-110448](https://qt-project.atlassian.net/browse/QTBUG-110448) Cannot remove window min/max buttons Ubuntu Wayland
* [QTBUG-145389](https://qt-project.atlassian.net/browse/QTBUG-145389) Qt6 Wayland apps crash on ChromeOS: wp_viewport and
wp_fractional_scale_v1 destroyed after wl_surface in
QWaylandWindow::reset()
* [QTBUG-145390](https://qt-project.atlassian.net/browse/QTBUG-145390) xdg-shell: setSizeHints() sends set_max_size values >
QWINDOWSIZE_MAX when CSD decorations are active
* [QTBUG-145853](https://qt-project.atlassian.net/browse/QTBUG-145853) [qtbase] Wayland plugin build fails with -no-feature-egl
* [QTBUG-136045](https://qt-project.atlassian.net/browse/QTBUG-136045) macOS: Window geometry is not updated correctly when the
OS rejects a change by setGeometry
* [QTBUG-144565](https://qt-project.atlassian.net/browse/QTBUG-144565) QJsonDocument move ctor and swap() are out-of-line
(should be inline)
* [QTBUG-123455](https://qt-project.atlassian.net/browse/QTBUG-123455) [Wayland] Embedded window does not receive keyboard
focus
* [QTBUG-145577](https://qt-project.atlassian.net/browse/QTBUG-145577) "Zone specifiers are only meaningful for a full
datetime" warning when formatting time with QLocale::LongFormat
* [QTBUG-145605](https://qt-project.atlassian.net/browse/QTBUG-145605) CLDR supplies time formats with zone specifiers
* [QTBUG-145990](https://qt-project.atlassian.net/browse/QTBUG-145990) QShaderVersion is only qHash-able on INTEGRITY
* [QTBUG-146013](https://qt-project.atlassian.net/browse/QTBUG-146013) Compile error in QByteArray move ctor on Clang 15 with
GCC 15 --gcc-toolchain
* [QTBUG-146017](https://qt-project.atlassian.net/browse/QTBUG-146017) QTextDocumentFragment::fromHtml("<tt/>") segfaults
immediately
* [QTBUG-88704](https://qt-project.atlassian.net/browse/QTBUG-88704) QCollatorSortKey is not working properly without ICU
support
* [QTBUG-127269](https://qt-project.atlassian.net/browse/QTBUG-127269) Cannot use Q_DECLARE_FLAGS for nested class
* [QTBUG-146569](https://qt-project.atlassian.net/browse/QTBUG-146569) Reconfiguring certain parent qt repos fails with
"add_library cannot create ALIAS target"
* [QTBUG-87410](https://qt-project.atlassian.net/browse/QTBUG-87410) tst_QTextStream has failing tests on Android
* [QTBUG-103456](https://qt-project.atlassian.net/browse/QTBUG-103456) Android: System.exit on back button press
* [QTBUG-127705](https://qt-project.atlassian.net/browse/QTBUG-127705) Android splashscreen not removed
* [QTBUG-144316](https://qt-project.atlassian.net/browse/QTBUG-144316) [REG: 6.8.3->6.8.6] Static builds of Qt Multimedia fail
to link ffmpeg libraries in qmake projects
* [QTBUG-146558](https://qt-project.atlassian.net/browse/QTBUG-146558) QVectorND are equality-comparable, but not hashable
* [QTBUG-132709](https://qt-project.atlassian.net/browse/QTBUG-132709) setOverrideCursor gives incorrect cursor size on high-
dpi display with 2 screens
* [QTBUG-126980](https://qt-project.atlassian.net/browse/QTBUG-126980) Drag-n-drop from zip file opened in Windows Explorer is
empty
* [QTBUG-146723](https://qt-project.atlassian.net/browse/QTBUG-146723) Qt::ImhNoEditMenu does not work for input fields running
on android
* [QTBUG-109173](https://qt-project.atlassian.net/browse/QTBUG-109173) Caret disappear on QLineEdit
* [QTBUG-128900](https://qt-project.atlassian.net/browse/QTBUG-128900) macOS 15 deployment target build failure due to obsolete
API 'CGDisplayCreateImageForRect'
* [QTBUG-146800](https://qt-project.atlassian.net/browse/QTBUG-146800) QSslSocket fails with Schannel on Windows Server 2016
* [QTBUG-146769](https://qt-project.atlassian.net/browse/QTBUG-146769) HarmonyOS: font size is too big
* [QTBUG-146744](https://qt-project.atlassian.net/browse/QTBUG-146744) QDate roundtrip parsing fails with 2-digit year format
for Jalali and IslamicCivil calendars
* [QTBUG-146680](https://qt-project.atlassian.net/browse/QTBUG-146680) tst_QDockWidget::dockLocationChanged() hits qCritical
* [QTBUG-146912](https://qt-project.atlassian.net/browse/QTBUG-146912) QVariant compares a uchar and QChar as unordered
* [QTBUG-140497](https://qt-project.atlassian.net/browse/QTBUG-140497) QSpinBox taking up too little space with stylesheet
* [QTBUG-21468](https://qt-project.atlassian.net/browse/QTBUG-21468) tst_qstylesheetstyle is broken
* [QTBUG-146995](https://qt-project.atlassian.net/browse/QTBUG-146995) ConnectionCacheExpiryTimeoutSecondsAttribute=0 does not
prevent connection reuse
* [QTBUG-147034](https://qt-project.atlassian.net/browse/QTBUG-147034) CMake: Don't create unneeded folders on configure
* [QTBUG-87308](https://qt-project.atlassian.net/browse/QTBUG-87308) Handling of Chakma in QDateTimeParser
* [QTBUG-110669](https://qt-project.atlassian.net/browse/QTBUG-110669) Q/Date/Time: align unquoting format strings for both
from/toString()
* [QTBUG-147280](https://qt-project.atlassian.net/browse/QTBUG-147280) Qt Windows fails to render traditional Mongolian
* [QTBUG-147291](https://qt-project.atlassian.net/browse/QTBUG-147291) OHOS_ABI and OHOS_ARCH both need to be set
* [QTBUG-147326](https://qt-project.atlassian.net/browse/QTBUG-147326) get_filename_component(REALPATH) doesn't prepend drive-
letter in cmake 4.0+ for drive-less paths
* [QTBUG-147354](https://qt-project.atlassian.net/browse/QTBUG-147354) FAIL!  : tst_QNmeaPositionInfoSource_RealTime::getPositi
onInfoFromNmea(RMC_wrong_lat_dir) The computed value is expected to be
equal to the baseline, but is not
* [QTBUG-127304](https://qt-project.atlassian.net/browse/QTBUG-127304) Undefined behavior in tst_qsvgrenderer
* [QTBUG-147402](https://qt-project.atlassian.net/browse/QTBUG-147402) QT_HARMONYOS_TARGET_ARCHS defaults to arm64-v8a
regardless of Qt's architecture
* [QTBUG-147475](https://qt-project.atlassian.net/browse/QTBUG-147475) Render target caching issues with D3D11 rhi backend
* [QTBUG-147500](https://qt-project.atlassian.net/browse/QTBUG-147500) Qt in-source build is broken
* [QTBUG-84033](https://qt-project.atlassian.net/browse/QTBUG-84033) Android 32bit - No large files support
* [QTBUG-147503](https://qt-project.atlassian.net/browse/QTBUG-147503) QNX: Qt Labs StyleKit style plugin silently becomes the
default widget style
* [QTBUG-147024](https://qt-project.atlassian.net/browse/QTBUG-147024) qtlottie: FAIL!  :
tst_VectorImage::parseNoAssumeTrustedSource()
* [QTBUG-147552](https://qt-project.atlassian.net/browse/QTBUG-147552) tst_qgraphicslayout hangs, QOhosView::destroyed
connection missed when invokeInQtThread task is dropped at Qt event loop
exit
* [QTBUG-147329](https://qt-project.atlassian.net/browse/QTBUG-147329) Black 1px row at bottom of texture-based widgets at
fractional DPR
* [QTBUG-144266](https://qt-project.atlassian.net/browse/QTBUG-144266) On Windows platform, visual artifacts remain on the
screen when moving a widget window within the main application window.
* [QTBUG-147559](https://qt-project.atlassian.net/browse/QTBUG-147559) [REG] Application do not start on visionOS with
6.12-beta1
* [QTBUG-147473](https://qt-project.atlassian.net/browse/QTBUG-147473) The network manual test fails
* [QTBUG-147551](https://qt-project.atlassian.net/browse/QTBUG-147551) Font with non-zero slant trait but no italic trait
incorrectly classified as oblique, drawn with synthetic italic
* [QTBUG-147538](https://qt-project.atlassian.net/browse/QTBUG-147538) ABI break in 6.12 beta 1: qstrnicmp missing
* [QTBUG-147758](https://qt-project.atlassian.net/browse/QTBUG-147758) [Android] cmake error: Missing .gitignore
* [QTBUG-147792](https://qt-project.atlassian.net/browse/QTBUG-147792) SOCKS5 proxy connection fails when the proxy replies
with a domain name (ATYP=0x03) in BND.ADDR
* [QTBUG-147033](https://qt-project.atlassian.net/browse/QTBUG-147033) Reg [6.9.3 -> 6.10.0 ] QTableView with AnyKeyPressed
duplicates first typed character in WASM.
* [QTBUG-147502](https://qt-project.atlassian.net/browse/QTBUG-147502) QNX: combobox/menu popups and the drag pixmap window are
forced fullscreen
* [QTBUG-147754](https://qt-project.atlassian.net/browse/QTBUG-147754) QCollator does not preserve collation options when
detaching
* [QTBUG-147629](https://qt-project.atlassian.net/browse/QTBUG-147629) REG->6.12 B/Linux/Wayland: Crash in
QDesktopServices::openUrl()
* [QTBUG-147819](https://qt-project.atlassian.net/browse/QTBUG-147819) HarmonyOS: Lazy paste-on-demand broken when a UDMF
record has only a provider and no direct entry
* [QTBUG-147734](https://qt-project.atlassian.net/browse/QTBUG-147734) [Reg->6.12] QBackingStore::flush() assertion for a top-
level window whose QWidget parent lives in another top-level
* [QTBUG-147959](https://qt-project.atlassian.net/browse/QTBUG-147959) OHOS raster backingstore blit writes past the
destination buffer when flushing a scrolled native child window (SIGSEGV
in memcpy)
* [QTBUG-147824](https://qt-project.atlassian.net/browse/QTBUG-147824) Build error - Android SDK Build Tools version
* [QTBUG-142393](https://qt-project.atlassian.net/browse/QTBUG-142393) WebAssembly locateFile ignores prefix argument
* [QTBUG-136242](https://qt-project.atlassian.net/browse/QTBUG-136242) wasm: Paste in standardContextMenu is not enabled by
default while clipboard access is allowed
* [QTBUG-146118](https://qt-project.atlassian.net/browse/QTBUG-146118) C++ constructors from different object files that run
before main function runs come in uncontrollable order, causing WASM app
crash
* [QTBUG-147924](https://qt-project.atlassian.net/browse/QTBUG-147924) qt_extract_metatypes() causes build failure with
identically named source files in different directories
* [QTBUG-147278](https://qt-project.atlassian.net/browse/QTBUG-147278) infinite autoscroll in QTableView
* [QTBUG-148296](https://qt-project.atlassian.net/browse/QTBUG-148296) CMake junctions cause qt6_deploy_qml_imports to miss
deploy_qml_imports/<target>.cmake
* [QTBUG-148220](https://qt-project.atlassian.net/browse/QTBUG-148220) QCompleter with QFileSystemModel: no completion when
editing a component of a not-yet-listed path
* [QTBUG-148343](https://qt-project.atlassian.net/browse/QTBUG-148343) Broken QML type registration when including .moc file
* [QTBUG-147940](https://qt-project.atlassian.net/browse/QTBUG-147940) ohos: nullptr dereference when QOhosSettings is accessed
during platform integration startup
* [QTBUG-147588](https://qt-project.atlassian.net/browse/QTBUG-147588) QMetaType::fromName() for const/non-const pointers
affected by registration order
* [QTBUG-148397](https://qt-project.atlassian.net/browse/QTBUG-148397) tst_QtParseTimeZone::prefix() fails on MacOS
* [QTBUG-148356](https://qt-project.atlassian.net/browse/QTBUG-148356) [Regr:6.11.1->6.12.0b1] QDateTime::fromString is broken?
* [QTBUG-147648](https://qt-project.atlassian.net/browse/QTBUG-147648) [Regr:6.11->6.12b2] qtimezoneprivate.cpp: use of non-
standard typeof breaks MSVC build in QTZP::findLongNamePrefix()
* [QTBUG-147418](https://qt-project.atlassian.net/browse/QTBUG-147418) Integer-overflow in QJalaliCalendar::isLeapYear
* [QTBUG-145018](https://qt-project.atlassian.net/browse/QTBUG-145018) [Regr: 6.7->6.8] Submenus of a QToolButton menu are
nonfunctional in WASM builds
* [QTBUG-146738](https://qt-project.atlassian.net/browse/QTBUG-146738) tooltips aren't at the cursor position when hovering
with a tablet stylus
* [QTBUG-148156](https://qt-project.atlassian.net/browse/QTBUG-148156) [Reg: Qt 6.12.0 beta1 -> 6.12.0 beta2] "libcrypto_3.so
does not exist!" when building certain examples on Windows (Android)
* [QTBUG-148545](https://qt-project.atlassian.net/browse/QTBUG-148545) Markdown doesn't turn image title into a tooltip
* [QTBUG-148550](https://qt-project.atlassian.net/browse/QTBUG-148550) HTML export doesn't preserve title on every tag where it
could
* [QTBUG-147419](https://qt-project.atlassian.net/browse/QTBUG-147419) Integer-overflow in QJalaliCalendar::dateToJulianDay
* [QTBUG-147826](https://qt-project.atlassian.net/browse/QTBUG-147826) QToolButton::setDefaultAction creates multiple
connections to QToolButtonPrivate::onDefaultActionChanged
* [QTBUG-136999](https://qt-project.atlassian.net/browse/QTBUG-136999) Top flaky test: tst_QWindow::testInputEvents
* [QTBUG-148691](https://qt-project.atlassian.net/browse/QTBUG-148691) QThreadStorage<T> with trivial T leaks every localData()
* [QTBUG-146211](https://qt-project.atlassian.net/browse/QTBUG-146211) IME under text-input-v3 is never disabled on COSMIC
* [QTBUG-148255](https://qt-project.atlassian.net/browse/QTBUG-148255) QThread tasks are not named on VxWorks
* [QTBUG-149024](https://qt-project.atlassian.net/browse/QTBUG-149024) qmldir file not found at
"/home/qt/work/qt/qtgraphs_build/qml/QtGraphs"
* [QTBUG-147695](https://qt-project.atlassian.net/browse/QTBUG-147695) [Qt5&Qt6] Incorrect rendering due to a mismatch between
the geometry in the system and in Qt
* [QTBUG-147569](https://qt-project.atlassian.net/browse/QTBUG-147569) [VxWorks] qtdeclarative autotests hit the 4 hours limit
before finishing
* [QTBUG-148792](https://qt-project.atlassian.net/browse/QTBUG-148792) Integer-overflow in QIslamicCivilCalendar
* [QTBUG-148549](https://qt-project.atlassian.net/browse/QTBUG-148549) Maximized / minimize window landing on wrong screen
* [QTBUG-149005](https://qt-project.atlassian.net/browse/QTBUG-149005) tst_qquickmenu (Failed)
* [QTBUG-149041](https://qt-project.atlassian.net/browse/QTBUG-149041) Qt RHI D3D: Crash in backend due to dangling QWindow
pointer (missing unregisterWindow)
* [QTBUG-148404](https://qt-project.atlassian.net/browse/QTBUG-148404) HarmonyOS: it should not be necessary to pass
QT_CHAINLOAD_TOOLCHAIN_FILE for user projects
* [QTBUG-144744](https://qt-project.atlassian.net/browse/QTBUG-144744) New class QSslKeyingMaterial is not fit for release
* [QTBUG-149045](https://qt-project.atlassian.net/browse/QTBUG-149045) Incomplete qtbase docs after cmake --build -t docs
* [QTBUG-149013](https://qt-project.atlassian.net/browse/QTBUG-149013) Inconsistent parsing/formatting of single quotes in
QDateTime
* [QTBUG-149105](https://qt-project.atlassian.net/browse/QTBUG-149105) standarddialogs: Application crashes when creating
dialog, menu, or combo box subwindows
* [QTBUG-148852](https://qt-project.atlassian.net/browse/QTBUG-148852) [MultiMedia] camera: Mute has no effect during video
recording.
* [QTBUG-148805](https://qt-project.atlassian.net/browse/QTBUG-148805) AndroidTestRunner not treating --timeout correctly
* [QTBUG-148766](https://qt-project.atlassian.net/browse/QTBUG-148766) harmonydeployqt breaks macos-quick-minimal build
* [QTBUG-145447](https://qt-project.atlassian.net/browse/QTBUG-145447)  QTextDocument: AlignMiddle on a cell which crosses a
page boundary causes text to be clipped
* [QTBUG-147896](https://qt-project.atlassian.net/browse/QTBUG-147896) IME/key input keeps going to the previously-focused
QLineEdit instead of the QML TextField inside an embedded QQuickView
* [QTBUG-149460](https://qt-project.atlassian.net/browse/QTBUG-149460) REG 6.12.0 Beta 2 ->6.12.0 Beta 3: uic crashes on file
where connection hints were removed.
* [QTBUG-144844](https://qt-project.atlassian.net/browse/QTBUG-144844) Cmake install fails on top level build on Windows on ARM
* [QTBUG-148991](https://qt-project.atlassian.net/browse/QTBUG-148991) Investigate and fix broken IME preview candidates
* [QTBUG-149358](https://qt-project.atlassian.net/browse/QTBUG-149358) `QStyleHints::toolTipWakeUpDelay` is no longer
accessible in QML
* [QTBUG-149124](https://qt-project.atlassian.net/browse/QTBUG-149124) HarmonyOS: prebuilt Qt hardcodes the build machine's SDK
path, so building an app fails with an unrelated "GLESv3 could not be
found"
* [QTBUG-149121](https://qt-project.atlassian.net/browse/QTBUG-149121) HarmonyOS: CMake build artifacts are installed into
src/harmonyos/templates and copied into every generated project
* [QTBUG-149381](https://qt-project.atlassian.net/browse/QTBUG-149381) DragApp: Application Crashes When Dragging Images to
DropApplication; Same Issue Reproduced with Mixed Text and Image Drag
* [QTBUG-149436](https://qt-project.atlassian.net/browse/QTBUG-149436) [Regr:6.11->6.12] QDateTime/QDate/QTime::fromString(): a
single literal space in the format now matches any run of whitespace,
including TAB and newline (regression from 6.11)
* [QTBUG-149601](https://qt-project.atlassian.net/browse/QTBUG-149601) [Regr:6.11->6.13] fromString() with "yyyy-MM-dd" accepts
a signed five-digit year ("+10000-01-02"), producing a valid QDateTime
whose ISO serialization is an empty string
* [QTBUG-149448](https://qt-project.atlassian.net/browse/QTBUG-149448) QMenu: QMenu popup position causes QAction area to
overlap QMenuBar
* [QTBUG-148547](https://qt-project.atlassian.net/browse/QTBUG-148547) textedit: QTextEdit loses focus after opening a file on
HarmonyOS
* [QTBUG-149300](https://qt-project.atlassian.net/browse/QTBUG-149300) Dnslookup: QDnsLookup Fails with "Not yet supported on
this OS"
* [QTBUG-83465](https://qt-project.atlassian.net/browse/QTBUG-83465) Shortcut can occasionally get triggered during drag and
drop
* [QTBUG-48612](https://qt-project.atlassian.net/browse/QTBUG-48612) QQuickWidget will crash if the quickwidget is deleted
while handling a QDrag in an invokable call.
* [QTBUG-65701](https://qt-project.atlassian.net/browse/QTBUG-65701) Drag attached property crashes when item it's attached to
is destroyed
* [QTBUG-116344](https://qt-project.atlassian.net/browse/QTBUG-116344) Segmentation fault on Wayland when enabling drag and
drop on QListWidget
* [QTBUG-124663](https://qt-project.atlassian.net/browse/QTBUG-124663) Auto-scrolling a ListView breaks drag operation
* [QTBUG-149201](https://qt-project.atlassian.net/browse/QTBUG-149201) [VxWorks] some file operation related CI tests are
failing with 26.03 on x86
* [QTBUG-149800](https://qt-project.atlassian.net/browse/QTBUG-149800) Shader fails to link, GLSL ES version mismatch between
stages
* [QTBUG-149864](https://qt-project.atlassian.net/browse/QTBUG-149864) Deprecate QTextStream::operator>>(char *)
* [QTBUG-149668](https://qt-project.atlassian.net/browse/QTBUG-149668) [Reg Qt 6.11.2->6.12.0b3] Configuring a CMake project
now takes ~9x longer
* [QTBUG-149443](https://qt-project.atlassian.net/browse/QTBUG-149443) MoltenVK: vkQueueSubmit blocks for ~1 s on
QSurface::VulkanSurface windows
* [QTBUG-149228](https://qt-project.atlassian.net/browse/QTBUG-149228) [REG 6.11->6.12] ASSERT: "dockNum < docks.size()"
* [QTBUG-149199](https://qt-project.atlassian.net/browse/QTBUG-149199) REG->6.10.3: Variable fonts rendering issue introduced
in v6.10.3
* [QTBUG-97041](https://qt-project.atlassian.net/browse/QTBUG-97041) QML Text with markdown backticks for code formatting does
not respect font size
* [QTBUG-38701](https://qt-project.atlassian.net/browse/QTBUG-38701) Android QTouchDevice::Capabilities say it support
QTouchDevice::NormalizedPosition but it is wrong
* [QTBUG-149632](https://qt-project.atlassian.net/browse/QTBUG-149632) uic fails to build .ui files containing <set> tags where
data has CR/LF
* [QTBUG-149394](https://qt-project.atlassian.net/browse/QTBUG-149394) QOdfWriter does not respect QTextTableCellFormat
* [QTBUG-149993](https://qt-project.atlassian.net/browse/QTBUG-149993) QtCore / serialization: reallocateStack() signed-shift
overflow (SERBUG-14)
* [QTBUG-149995](https://qt-project.atlassian.net/browse/QTBUG-149995) QtCore / serialization: entityLength narrows to int
(SERBUG-15)
* [QTBUG-150052](https://qt-project.atlassian.net/browse/QTBUG-150052) QtCore / serialization: SimpleStack::reserve() signed-
shift overflow (SERBUG-14 cont'd)
* [QTBUG-150087](https://qt-project.atlassian.net/browse/QTBUG-150087) QXmlStreamReader accepts a negative expansion limit
* [QTBUG-150083](https://qt-project.atlassian.net/browse/QTBUG-150083) QXmlStreamReader incorrectly subtracts the top entity
length from the expansion limit
* [QTBUG-147509](https://qt-project.atlassian.net/browse/QTBUG-147509) Repeatedly populating a QStandardItemModel, calling
QTreeView::expandAll() and clearing using Model::removeRows() shows
increasing memory
* [QTBUG-149288](https://qt-project.atlassian.net/browse/QTBUG-149288) [Regr:6.11->6.12] The `t` format specifier of
QDateTime::fromString() no longer accepts time zone names such as "CET"
* [QTBUG-150292](https://qt-project.atlassian.net/browse/QTBUG-150292) iOS: getTimeStamp() truncates subsecond precision,
disrupting flick momentum (Qt 6.12 regression)
* [QTBUG-150280](https://qt-project.atlassian.net/browse/QTBUG-150280) [REG 6.11.2 -> 6.12.0-beta1] QWheelEvent-s with
QInputDevice::Capability::PixelScroll and zero pixelDelta
* [QTBUG-148713](https://qt-project.atlassian.net/browse/QTBUG-148713) QTime::fromString() with the "zzz" format accepts a
fractional part longer than three digits and silently truncates it
(regression from 6.11)
* [QTBUG-141433](https://qt-project.atlassian.net/browse/QTBUG-141433) QSaveFile has no std::filesystem::path support
* [QTBUG-137566](https://qt-project.atlassian.net/browse/QTBUG-137566) Make snippets in qtbase compilable and add to the build
system
* [QTBUG-116910](https://qt-project.atlassian.net/browse/QTBUG-116910) ToolTips are not easy to use
* [QTBUG-143916](https://qt-project.atlassian.net/browse/QTBUG-143916) Fix QDoc warnings for Qt 6.11
* [QTBUG-96239](https://qt-project.atlassian.net/browse/QTBUG-96239) Document CMake component in CMake function documentation
* [QTBUG-127648](https://qt-project.atlassian.net/browse/QTBUG-127648) DragEvent coordinates are rounded to nearest integer
when Item scale is a real value other than 1
* [QTBUG-140852](https://qt-project.atlassian.net/browse/QTBUG-140852) [wayland] drop event has wrong buttons()
* [QTBUG-143921](https://qt-project.atlassian.net/browse/QTBUG-143921) QNetworkAccessManager: HostNotFound after IPv6↔IPv4
switch due to stale networkLayerState
* [QTBUG-144183](https://qt-project.atlassian.net/browse/QTBUG-144183) ImageWriter crashes in png_icc_check_header when writing
a clipboard QImage to PNG on macOS
* [QTBUG-141942](https://qt-project.atlassian.net/browse/QTBUG-141942) Crash in png lib
* [QTBUG-125246](https://qt-project.atlassian.net/browse/QTBUG-125246) PNG with invalid colorSpace doesn't preserve ICC data
* [QTBUG-144582](https://qt-project.atlassian.net/browse/QTBUG-144582) [REG 6.11.0 -> 6.12.0] tst_qjsonbinding (Failed)
* [QTBUG-144800](https://qt-project.atlassian.net/browse/QTBUG-144800) Buffer sharing limitted to SHM in qtwayland compositors
* [QTBUG-135968](https://qt-project.atlassian.net/browse/QTBUG-135968) Top flaky test: tst_QFreeList::threadedTest
* [QTBUG-141419](https://qt-project.atlassian.net/browse/QTBUG-141419) QNetworkAccessManager high CPU usage if outgoing packet
is rejected by nftables
* [QTBUG-143734](https://qt-project.atlassian.net/browse/QTBUG-143734) svgtoqml tool has hidden dependency on
QMinimalIntegrationPlugin
* [QTBUG-104088](https://qt-project.atlassian.net/browse/QTBUG-104088) QWidget::geometry() and QWidget::mapToParent()
documentation is not accurate
* [QTBUG-142797](https://qt-project.atlassian.net/browse/QTBUG-142797) QMainWindow: inconsistent behavior when saving and
restoring geometry with dock widgets
* [QTBUG-142906](https://qt-project.atlassian.net/browse/QTBUG-142906) Moving window across displays stops animations
* [QTBUG-145713](https://qt-project.atlassian.net/browse/QTBUG-145713) xamples\grpc\vehicle\vehicle_server.exe : fatal error
LNK1120: 3 unresolved externals
* [QTBUG-140076](https://qt-project.atlassian.net/browse/QTBUG-140076) [REG 6.9.0 -> 6.9.1] Memory leaks on
QPainter::drawText() in static QGuiApplication
* [QTBUG-140413](https://qt-project.atlassian.net/browse/QTBUG-140413) heap-use-after-free when using a QSslCertificate in a
static QCoreApplication
* [QTBUG-145799](https://qt-project.atlassian.net/browse/QTBUG-145799) qmlpreview doesn't work with loadFromModule()
* [QTBUG-135579](https://qt-project.atlassian.net/browse/QTBUG-135579) Enabling vertical document-mode tabs in QMainWindow does
not immideiatly update unified toolbar bottom border
* [QTBUG-135581](https://qt-project.atlassian.net/browse/QTBUG-135581) Unified toolbar bottom border sometimes duplicated, and
sometimes missing
* [QTBUG-135580](https://qt-project.atlassian.net/browse/QTBUG-135580) Tab title text corruption when dragging in unified
toolbar mode
* [QTBUG-143161](https://qt-project.atlassian.net/browse/QTBUG-143161) Keyboard takes full screen on android and there is no
way to hide the extra features
* [QTBUG-143699](https://qt-project.atlassian.net/browse/QTBUG-143699) Crash in QOpenGLFunctions::glClear in various Controls
auto tests
* [QTBUG-146572](https://qt-project.atlassian.net/browse/QTBUG-146572) Extraction of CLDR data gets different results between
core.zip and git versions of data
* [QTBUG-112717](https://qt-project.atlassian.net/browse/QTBUG-112717) Eliding is not functional for Quick Text (StyledText)
with inline images
* [QTBUG-97536](https://qt-project.atlassian.net/browse/QTBUG-97536) Text layout is broken if it contains inline images and
eliding is used
* [QTBUG-57191](https://qt-project.atlassian.net/browse/QTBUG-57191) StyledText format Images are not elided in Text component
* [QTBUG-36163](https://qt-project.atlassian.net/browse/QTBUG-36163) Using wrap end elide on text with embedded image breaks
it's layout
* [QTBUG-39107](https://qt-project.atlassian.net/browse/QTBUG-39107) Images in text disappear if lineLaidOut signal is
connected
* [QTBUG-43820](https://qt-project.atlassian.net/browse/QTBUG-43820) QML styledText doesn't show <img> when onLineLaidOut is
connected
* [QTBUG-113829](https://qt-project.atlassian.net/browse/QTBUG-113829) Text.WrapAnywhere with Styled text (testing with img
tag) crops image
* [QTBUG-133284](https://qt-project.atlassian.net/browse/QTBUG-133284) letter spacing + inline images + StyledText = bad
spacing
* [QTBUG-107857](https://qt-project.atlassian.net/browse/QTBUG-107857) Qt Shared Library project on iOS fails to build
* [QTBUG-145975](https://qt-project.atlassian.net/browse/QTBUG-145975) tst_selftests fails on QNX 8.0: libc++ newlocale stub
crashes sub-binaries with LC_ALL=en_US.UTF-8
* [QTBUG-146891](https://qt-project.atlassian.net/browse/QTBUG-146891) HarmonyOS: crash with napi_get_last_error_info() when
quit
* [QTBUG-145768](https://qt-project.atlassian.net/browse/QTBUG-145768) tst_QDateTime::springForward:Asia/Singapore fails on
some platforms
* [QTBUG-139833](https://qt-project.atlassian.net/browse/QTBUG-139833) [a11y] Auditive feedback during scroll missing
* [QTBUG-144929](https://qt-project.atlassian.net/browse/QTBUG-144929) QObject::disconnect(const Connection &) const_cast<>s
its argument
* [QTBUG-144910](https://qt-project.atlassian.net/browse/QTBUG-144910) QCanvasPainterWidget and QRhiWidget are unexpectedly
slow with Vulkan on some platforms
* [QTBUG-135052](https://qt-project.atlassian.net/browse/QTBUG-135052) [QtQuick3dXr]  Vulkan performance much worse compared to
OpenGLES on Quest 3
* [QTBUG-147014](https://qt-project.atlassian.net/browse/QTBUG-147014) [VxWorks] tst_qfile absolutePathLinkToRelativePath fails
with VxWorks 26.03
* [QTBUG-147015](https://qt-project.atlassian.net/browse/QTBUG-147015) [VxWorks]  tst_qframe fails on VxWorks 26.03
* [QTBUG-146803](https://qt-project.atlassian.net/browse/QTBUG-146803) [FFmpeg, Android]: tst_qtexttospeech (Failed)
* [QTBUG-146124](https://qt-project.atlassian.net/browse/QTBUG-146124) [Android] Broken legacyPackaging configuration
* [QTBUG-147136](https://qt-project.atlassian.net/browse/QTBUG-147136) QDoc: Wildcard patterns in `excludefiles` configuration
variable do not work as expected
* [QTBUG-147406](https://qt-project.atlassian.net/browse/QTBUG-147406) Constructing QBindable from QProperty makes binaries
depend on the exact-versioned private symbol
QUntypedPropertyBinding(QPropertyBindingPrivate*)
* [QTBUG-117514](https://qt-project.atlassian.net/browse/QTBUG-117514) QFuture::then marked as private
* [QTBUG-147287](https://qt-project.atlassian.net/browse/QTBUG-147287) HarmonyOS: port qtnetwork module - wi-fi
* [QTBUG-147224](https://qt-project.atlassian.net/browse/QTBUG-147224) failure:tst_QClipboard::clearBeforeSetText() clipboard
text is empty instead of expected string
* [QTBUG-147476](https://qt-project.atlassian.net/browse/QTBUG-147476) HarmonyOS: port qtcoap module
* [QTBUG-147401](https://qt-project.atlassian.net/browse/QTBUG-147401) HarmonyOS: port qtsvg module
* [QTBUG-147485](https://qt-project.atlassian.net/browse/QTBUG-147485) [libtst_qfocusevent] failure:
tst_QFocusEvent::checkReason_ActiveWindow()
* [QTBUG-147464](https://qt-project.atlassian.net/browse/QTBUG-147464) [libtst_qbackingstore]
failure:tst_QBackingStore::paint() backing-store pixel color compare
failure
* [QTBUG-126265](https://qt-project.atlassian.net/browse/QTBUG-126265) uic: Code Injection to Potential Code Execution
* [QTBUG-146552](https://qt-project.atlassian.net/browse/QTBUG-146552) A11y: QAccessible::state::expandable/expanded not fully
implemented
* [QTBUG-147764](https://qt-project.atlassian.net/browse/QTBUG-147764) QMdiSubWindow title elision is computed with the wrong
DPI on non-default-DPI screens
* [QTBUG-147798](https://qt-project.atlassian.net/browse/QTBUG-147798) tst_QFontDatabase::systemFixedFonts fails on RHEL
* [QTBUG-147957](https://qt-project.atlassian.net/browse/QTBUG-147957) Failure: tst_QWidget_window::mouseMoveWithPopup()
* [QTBUG-89545](https://qt-project.atlassian.net/browse/QTBUG-89545) CMake: on macOS (w/ framework build) the module includes
the binary
* [QTBUG-147352](https://qt-project.atlassian.net/browse/QTBUG-147352) Fail! : tst_QHeaderView::defaultSectionSizeTestStyles
* [QTBUG-148210](https://qt-project.atlassian.net/browse/QTBUG-148210) HarmonyOS: QOhosFileIconEngine lacks permissions and JS
module includes
* [QTBUG-148227](https://qt-project.atlassian.net/browse/QTBUG-148227) HarmonyOS: OH_FileUri conversion helper leaks its result
buffer
* [QTBUG-118858](https://qt-project.atlassian.net/browse/QTBUG-118858) On Android widget type is not announced by talkback
* [QTBUG-148234](https://qt-project.atlassian.net/browse/QTBUG-148234) HarmonyOS: Wrong update sequence: maximize applied
before queued move
* [QTBUG-148464](https://qt-project.atlassian.net/browse/QTBUG-148464) HarmonyOS: QCoreApplication::checkPermission() never
reports Denied
* [QTBUG-148423](https://qt-project.atlassian.net/browse/QTBUG-148423) harmonyostestrunner: --app-args / test-function filters
produce invalid io.qt.appArgsJson, breaking app launch
* [QTBUG-148361](https://qt-project.atlassian.net/browse/QTBUG-148361) A11y: Ensure correct implementation of the "expandable"
state property for MenuItem and ComboBox
* [QTBUG-147397](https://qt-project.atlassian.net/browse/QTBUG-147397) Third-party GLX context manipulation causes stale TLS in
QRhiGles2, leading to GL failures
* [QTBUG-147770](https://qt-project.atlassian.net/browse/QTBUG-147770) QRhiGles2 crash: "Failed to compile shader" in
setGraphicsPipeline when          RHI uses Core Profile OpenGL context
with Mesa/glvnd
* [QTBUG-148838](https://qt-project.atlassian.net/browse/QTBUG-148838) QThread sleep functions min delay is affected by other
QTimers
* [QTBUG-148419](https://qt-project.atlassian.net/browse/QTBUG-148419) textedit: Application crashes when entering Chinese
punctuation in QTextEdit
* [QTBUG-148751](https://qt-project.atlassian.net/browse/QTBUG-148751) [REG 6.11.2->6.12.0] webenginequick/quicknanobrowser not
launching on linux and Windows
* [QTBUG-148511](https://qt-project.atlassian.net/browse/QTBUG-148511) Soft keyboard flickers between uppercase and lowercase
in English input due to missing
OH_TextEditorProxy_SetGetLeftTextOfCursorFunc /
OH_TextEditorProxy_SetGetRightTextOfCursorFunc adaptation
* [QTBUG-135599](https://qt-project.atlassian.net/browse/QTBUG-135599) Network test failures in Windows 11 24h2
* [QTBUG-148567](https://qt-project.atlassian.net/browse/QTBUG-148567) harmonyos: samegame(demo) failed with harmonydeployqt
* [QTBUG-148627](https://qt-project.atlassian.net/browse/QTBUG-148627) HarmonyOS: honor --release when invoking hvigor
* [QTBUG-148993](https://qt-project.atlassian.net/browse/QTBUG-148993) Mouse dragging causes noticeable lag/jank in window
movement
* [QTBUG-147228](https://qt-project.atlassian.net/browse/QTBUG-147228) QMetalLayer displayLock triggers spurious TSan "double
lock of a mutex" on macOS
* [QTBUG-146626](https://qt-project.atlassian.net/browse/QTBUG-146626) AppContextDirs::resourceDir not mapped to any
QStandardPaths location
* [QTBUG-148544](https://qt-project.atlassian.net/browse/QTBUG-148544) dockwidgets: A Dock Widget Cannot Be Re-Docked After
Fully Entering the Floating State, and Dragging Is Laggy
* [QTBUG-149350](https://qt-project.atlassian.net/browse/QTBUG-149350) Autotest runs on HarmonyOS stall on system dialogs that
cannot be suppressed
* [QTBUG-149374](https://qt-project.atlassian.net/browse/QTBUG-149374)  OHOS: expose bundle versionName via
QCoreApplication::applicationVersion()
* [QTBUG-147339](https://qt-project.atlassian.net/browse/QTBUG-147339) Fail! : tst_QHeaderView::visualIndexAt,
tst_QHeaderView::sectionSize
* [QTBUG-148571](https://qt-project.atlassian.net/browse/QTBUG-148571) Missing gesture functionalities and sensitivity issues
in imagegestures example
* [QTBUG-149294](https://qt-project.atlassian.net/browse/QTBUG-149294) ARKUI_KEYCODE_ALT_RIGHT is mapped to Qt::Key_AltGr
instead of Qt::Key_Alt
* [QTBUG-148858](https://qt-project.atlassian.net/browse/QTBUG-148858) whitespaces in --codesign with
qt_generate_deploy_qml_app_script fails
* [QTBUG-115209](https://qt-project.atlassian.net/browse/QTBUG-115209) ccache 0% hit rate after configure -redo
* [QTBUG-149444](https://qt-project.atlassian.net/browse/QTBUG-149444) QSaveFile creates and deletes an extra file on every
open() of a new target
* [QTBUG-85782](https://qt-project.atlassian.net/browse/QTBUG-85782) Applicaton blocked forever if Drag-Drop in progress while
modal dialog opens
* [QTBUG-46093](https://qt-project.atlassian.net/browse/QTBUG-46093) print dialoge duplex not selectable
* [QTBUG-149334](https://qt-project.atlassian.net/browse/QTBUG-149334) mapviewer: Two-finger pinch gesture unexpectedly zooms
map to maximum level and rotates it on HarmonyOS
* [QTBUG-149770](https://qt-project.atlassian.net/browse/QTBUG-149770) Unsupported value: android-37.0
* [QTBUG-149323](https://qt-project.atlassian.net/browse/QTBUG-149323) LinkDropDemo: Unable to Retrieve URL When Dragging a
Hyperlink from a Native App to Qt
* [QTBUG-148466](https://qt-project.atlassian.net/browse/QTBUG-148466) HarmonyOS: ohos networkinformation plugin reaches into
qpa plugin's private sources for net enums
* [QTBUG-149899](https://qt-project.atlassian.net/browse/QTBUG-149899) HarmonyOS: handle JS promise in QOhosWindowProxy
* [QTBUG-128660](https://qt-project.atlassian.net/browse/QTBUG-128660) QScreen::availableGeometry().topLeft() is wrong for
high-DPI displays
* [QTBUG-150187](https://qt-project.atlassian.net/browse/QTBUG-150187) Don't create a QByteArray in
QXmlStreamReader::addData(QASV) before we didn't know we need one
(SERBUG-16 cont'd)
* [QTBUG-44549](https://qt-project.atlassian.net/browse/QTBUG-44549) Documentation says that stylesheets doesn't work with
custom styles which is not true
* [QTBUG-150218](https://qt-project.atlassian.net/browse/QTBUG-150218) cmake regression in QtWebengine 6.12 beta 4

### qtsvg
* [QTBUG-147867](https://qt-project.atlassian.net/browse/QTBUG-147867) [VxWorks] qsvggenerator autotest fails in CI with Vx
26.03
* [QTBUG-148224](https://qt-project.atlassian.net/browse/QTBUG-148224) Headers/6.13.0/QtSvg/private/qsvgpaintserver_p.h:29:10:
fatal error: 'qtsvgexports.h' file not found
* [QTBUG-147932](https://qt-project.atlassian.net/browse/QTBUG-147932) [VxWorks] qicon_svg autotest fails in CI with Vx 26.03
* [QTBUG-148685](https://qt-project.atlassian.net/browse/QTBUG-148685) QImageReader::imageCount() returns 0 for an animated
SVG, and the returned value depends on which getter was called first
* [QTBUG-140076](https://qt-project.atlassian.net/browse/QTBUG-140076) [REG 6.9.0 -> 6.9.1] Memory leaks on
QPainter::drawText() in static QGuiApplication
* [QTBUG-145372](https://qt-project.atlassian.net/browse/QTBUG-145372) QPainterPath assertion failure in
QSvgPaintEngine::drawPath when path contains CurveToElement
* [QTBUG-146726](https://qt-project.atlassian.net/browse/QTBUG-146726) parseFont() creates and appends a QSvgFontStyle even if
everything is set to `inherit`

### qtdeclarative
* [QTBUG-134767](https://qt-project.atlassian.net/browse/QTBUG-134767) responsive layouts example update to use
'ApplicationWindow'
* [QTBUG-142067](https://qt-project.atlassian.net/browse/QTBUG-142067) TableView: Bindings to top/bottomRow and
left/rightColumn properties are not updated
* [QTBUG-143260](https://qt-project.atlassian.net/browse/QTBUG-143260) ASSERT: "scope->isFullyResolved()" in qmllint
* [QTBUG-133087](https://qt-project.atlassian.net/browse/QTBUG-133087) Shortcut key sequence not shown in MenuItem
* [QTBUG-140173](https://qt-project.atlassian.net/browse/QTBUG-140173) Qt Quick Test: Optional TestCase can wait indefinitely
if "when: false" is applied
* [QTBUG-140155](https://qt-project.atlassian.net/browse/QTBUG-140155) Qmllint issue when using Controls.SpinBox.textFromValue
* [QTBUG-143554](https://qt-project.atlassian.net/browse/QTBUG-143554) "" == 0   returns false in the compiler
* [QTBUG-142682](https://qt-project.atlassian.net/browse/QTBUG-142682) qmllint should warn when trying to override a
nonexistant property
* [QTBUG-142946](https://qt-project.atlassian.net/browse/QTBUG-142946) QML tools don't yet accept explicit overrides
* [QTBUG-132135](https://qt-project.atlassian.net/browse/QTBUG-132135) qt.qml.gc.allocatorStats is confused in incremental gc
mode
* [QTBUG-136650](https://qt-project.atlassian.net/browse/QTBUG-136650) Not possible to have a frameless QML ColorDialog
* [QTBUG-144302](https://qt-project.atlassian.net/browse/QTBUG-144302) tst_dialogs (Failed)
* [QTBUG-144370](https://qt-project.atlassian.net/browse/QTBUG-144370) gcc 15.2.1 ubsan: something wrong with linking
QQmlDelegateModelItem in quicktemplates
* [QTBUG-138704](https://qt-project.atlassian.net/browse/QTBUG-138704) QmlTreeModel misses API for insertRow()
* [QTBUG-142264](https://qt-project.atlassian.net/browse/QTBUG-142264) Top flaky test:
tst_qmlls_qqmlcodemodel::reloadLotsOfFiles
* [QTBUG-130605](https://qt-project.atlassian.net/browse/QTBUG-130605) Invalid alias target location unless I bind it
* [QTCREATORBUG-31078](https://qt-project.atlassian.net/browse/QTCREATORBUG-31078) Bogus warning in Qt Creator / TableModel /
Delegate
* [QTBUG-144701](https://qt-project.atlassian.net/browse/QTBUG-144701) [REG 6.10.2 → 6.10.3, 6.11] Valid QML code fails to load
with wrong error about property assignment
* [QTBUG-144313](https://qt-project.atlassian.net/browse/QTBUG-144313) FlexboxLayout QML Type not available in VxWorks.
* [QTBUG-144815](https://qt-project.atlassian.net/browse/QTBUG-144815) SearchField is missing selectAll() method
* [QTBUG-124476](https://qt-project.atlassian.net/browse/QTBUG-124476) QML alias triggers ASSERT coreIndex >= 0
* [QTBUG-140138](https://qt-project.atlassian.net/browse/QTBUG-140138) qmllint doesn't understand object list bindings to
attached and grouped properties
* [QTCREATORBUG-34161](https://qt-project.atlassian.net/browse/QTCREATORBUG-34161) Bogus warning when using a signal with an argument
in QML
* [QTBUG-144907](https://qt-project.atlassian.net/browse/QTBUG-144907) Updating path with stroke gradient is broken in Qt Quick
* [QTBUG-144917](https://qt-project.atlassian.net/browse/QTBUG-144917) QML Import couldn't be resolved
* [QTBUG-141251](https://qt-project.atlassian.net/browse/QTBUG-141251) TextInput and Text vertical alignment does not match
when using multiple fonts
* [QTBUG-132452](https://qt-project.atlassian.net/browse/QTBUG-132452) qmllint issues
* [QTBUG-133703](https://qt-project.atlassian.net/browse/QTBUG-133703) QQuickSystemPalette uses deprecated
QGuiApplication::paletteChanged() signal
* [QTBUG-144920](https://qt-project.atlassian.net/browse/QTBUG-144920) Add common selection APIs for SearchField
* [QTBUG-145062](https://qt-project.atlassian.net/browse/QTBUG-145062) qmlls 6.11: lots of import path warnings on project
created with qt creator's wizard
* [QTBUG-145103](https://qt-project.atlassian.net/browse/QTBUG-145103) Ensure SearchField supports RTL languages
* [QTBUG-145074](https://qt-project.atlassian.net/browse/QTBUG-145074) Ambiguous type detected. App 254.0 is defined multiple
times
* [QTBUG-145572](https://qt-project.atlassian.net/browse/QTBUG-145572) qmllint crashes in
QQmlJS::LinterRenamedComponents::isTypeRenamedTo
* [QTBUG-143453](https://qt-project.atlassian.net/browse/QTBUG-143453) Inconsistent SVG rendering with QML Image when using
asynchronous loading at 175% DPI on Windows
* [QTBUG-39617](https://qt-project.atlassian.net/browse/QTBUG-39617) QML TextArea doesn't support
QTextCharFormat::SpellCheckUnderline
* [QTBUG-125575](https://qt-project.atlassian.net/browse/QTBUG-125575) Underline (Spellchecking) in QSyntaxHighlighter not
showing in TextArea
* [QTBUG-145715](https://qt-project.atlassian.net/browse/QTBUG-145715) tst_shapelayer (Failed)
* [QTBUG-142700](https://qt-project.atlassian.net/browse/QTBUG-142700) QtQuick: native Tooltip text update causes wrong
placement
* [QTBUG-143742](https://qt-project.atlassian.net/browse/QTBUG-143742) Button is checked when a TapHandler is declared inside
it
* [QTBUG-145826](https://qt-project.atlassian.net/browse/QTBUG-145826) Qt Quick Compiler cannot properly handle conversion from
QJSPrimitiveValue to float
* [QTBUG-138207](https://qt-project.atlassian.net/browse/QTBUG-138207) Releasing QQuickItemGrabResult before ready signal was
sent can lead to crashes
* [QTBUG-117786](https://qt-project.atlassian.net/browse/QTBUG-117786) QmlCompiler does not recognize a component within itself
* [QTBUG-131786](https://qt-project.atlassian.net/browse/QTBUG-131786) popupType "Popup.Window" propagates events
* [QTBUG-145585](https://qt-project.atlassian.net/browse/QTBUG-145585) `modal: true` does not block input to the parent window
when using `popupType: Popup.Window`
* [QTBUG-141362](https://qt-project.atlassian.net/browse/QTBUG-141362) Popup allows mouse fallthrough regardless of mode
* [QTBUG-141459](https://qt-project.atlassian.net/browse/QTBUG-141459) ComboBox popup doesn't open correctly on the selected
item with FluentWinUI3 style.
* [QTBUG-143354](https://qt-project.atlassian.net/browse/QTBUG-143354) qmlpreview command line utility doesn't update when QML
sources change
* [QTBUG-142198](https://qt-project.atlassian.net/browse/QTBUG-142198) list<QtObject> does not automatically increase its
length upon an out-of-bounds write, unlike other list types or JS arrays
* [QTBUG-139082](https://qt-project.atlassian.net/browse/QTBUG-139082) Landing page in docs for the "Qt.labs" and its modules
* [QTBUG-144856](https://qt-project.atlassian.net/browse/QTBUG-144856) Check and fix Q_ALLOCA_VAR usage in QtDeclarative
* [QTBUG-145030](https://qt-project.atlassian.net/browse/QTBUG-145030) ASSERT: "!std::isnan(value)" in
QQuickColorValueType::alpha
* [QTBUG-146158](https://qt-project.atlassian.net/browse/QTBUG-146158) QJSEngine::importModule fails to report errors
* [QTBUG-145794](https://qt-project.atlassian.net/browse/QTBUG-145794) QQmlEngineDebugServiceImpl::buildObjectList() omits
objects in child contexts, making delegates invisible to the debugger
* [QTBUG-131865](https://qt-project.atlassian.net/browse/QTBUG-131865) [QtQuick.Controls.Windows] Indeterminate ProgressBar
does not animate
* [QTBUG-146743](https://qt-project.atlassian.net/browse/QTBUG-146743) tst_QQuickDrawer::iOS::position(bottom) Compared doubles
are not the same (fuzzy compare)
* [QTBUG-146199](https://qt-project.atlassian.net/browse/QTBUG-146199) Unconstricted caching when loading anonymous QML through
QQmlComponent::setData()
* [QTBUG-146210](https://qt-project.atlassian.net/browse/QTBUG-146210) QQmlEngine: calling addImportPath() causes
asynchronously loading components to never become ready
* [QTBUG-123771](https://qt-project.atlassian.net/browse/QTBUG-123771) QQmlComponent seems unable to create a component that
has a required alias
* [QTBUG-142760](https://qt-project.atlassian.net/browse/QTBUG-142760) [Qt gPRC] QML API uses
std::shared_ptr<QAbstractGrpcChannel>, but that is not registered in QML
* [QTBUG-143881](https://qt-project.atlassian.net/browse/QTBUG-143881) qmllint complains about opaque pointer types
* [QTBUG-145611](https://qt-project.atlassian.net/browse/QTBUG-145611) "Go To C++ Definition" does not find file
* [QTBUG-134722](https://qt-project.atlassian.net/browse/QTBUG-134722) ColorEqual fails correctly comparing rgba constructed
colors with hsva constructed colors
* [QTBUG-112717](https://qt-project.atlassian.net/browse/QTBUG-112717) Eliding is not functional for Quick Text (StyledText)
with inline images
* [QTBUG-97536](https://qt-project.atlassian.net/browse/QTBUG-97536) Text layout is broken if it contains inline images and
eliding is used
* [QTBUG-57191](https://qt-project.atlassian.net/browse/QTBUG-57191) StyledText format Images are not elided in Text component
* [QTBUG-36163](https://qt-project.atlassian.net/browse/QTBUG-36163) Using wrap end elide on text with embedded image breaks
it's layout
* [QTBUG-39107](https://qt-project.atlassian.net/browse/QTBUG-39107) Images in text disappear if lineLaidOut signal is
connected
* [QTBUG-43820](https://qt-project.atlassian.net/browse/QTBUG-43820) QML styledText doesn't show <img> when onLineLaidOut is
connected
* [QTBUG-113829](https://qt-project.atlassian.net/browse/QTBUG-113829) Text.WrapAnywhere with Styled text (testing with img
tag) crops image
* [QTBUG-115285](https://qt-project.atlassian.net/browse/QTBUG-115285) Styled text vs Rich text white space before img tag
* [QTBUG-133284](https://qt-project.atlassian.net/browse/QTBUG-133284) letter spacing + inline images + StyledText = bad
spacing
* [QTBUG-138732](https://qt-project.atlassian.net/browse/QTBUG-138732) QmlTreeModel misses API for moveRow()
* [QTBUG-88646](https://qt-project.atlassian.net/browse/QTBUG-88646) tst_qquicktext::contentSize() failed on msvc2019
developer build in CI
* [QTBUG-109411](https://qt-project.atlassian.net/browse/QTBUG-109411) Quick Text's implicitWidth doesn't respect
maximumLineCount
* [QTBUG-142933](https://qt-project.atlassian.net/browse/QTBUG-142933) Layout.fillWidth does not work correctly with the Text
element.
* [QTBUG-140875](https://qt-project.atlassian.net/browse/QTBUG-140875) QML Text - multi-line text is not always elided
correctly when item is resized
* [QTBUG-147178](https://qt-project.atlassian.net/browse/QTBUG-147178) Error  error: reference to 'Default' is ambiguous in
qqmljstyperesolver
* [QTBUG-147163](https://qt-project.atlassian.net/browse/QTBUG-147163) ASSERT: "isFileBeingCompiled ||
!root->moduleName().isEmpty()"
* [QTBUG-144984](https://qt-project.atlassian.net/browse/QTBUG-144984) Unable to navigate SearchField suggestions with keys
when the text is empty
* [QTBUG-147284](https://qt-project.atlassian.net/browse/QTBUG-147284) error: static assertion failed: Pointer Meta Types must
either point to fully-defined types or be declared with
Q_DECLARE_OPAQUE_POINTER(T *)
* [QTBUG-147277](https://qt-project.atlassian.net/browse/QTBUG-147277) StyledText: <span> breaks paragraph direction detection
* [QTBUG-117901](https://qt-project.atlassian.net/browse/QTBUG-117901) Changing a text element can cause re-upload of entire
scene
* [QTBUG-147215](https://qt-project.atlassian.net/browse/QTBUG-147215) qmltc errors out on non-type-compilation-relevant
warnings
* [QTBUG-146732](https://qt-project.atlassian.net/browse/QTBUG-146732) Repeated $/addBuildDirs notifications does not refresh
.qmlls.build.ini for existing build paths.
* [QTBUG-146733](https://qt-project.atlassian.net/browse/QTBUG-146733) No workspace/semanticTokens/refresh sent after
$/addBuildDirs
* [QTBUG-147697](https://qt-project.atlassian.net/browse/QTBUG-147697) ASSERT: "ast" in QQmlJS::possibleLastStatements
* [QTBUG-147398](https://qt-project.atlassian.net/browse/QTBUG-147398) [Boot to Qt 6.12.0 beta1] "QStyleKitStyle: No StyleKit
style loaded, calculating sub*Rect with QCommonStyle" warnings in stdout
* [QTBUG-147447](https://qt-project.atlassian.net/browse/QTBUG-147447) macdeployqt bundles ~30MB of Qml Frameworks crap due to
libqstylekitstyle plugin
* [QTBUG-126757](https://qt-project.atlassian.net/browse/QTBUG-126757) Stale QML cache is not updated on AGL
* [QTBUG-147384](https://qt-project.atlassian.net/browse/QTBUG-147384) QML .qmlc cache not invalidated when mtime is not
reliable
* [QTBUG-138621](https://qt-project.atlassian.net/browse/QTBUG-138621) Crash in qv4mm during destruction
* [QTBUG-134687](https://qt-project.atlassian.net/browse/QTBUG-134687) Crash in GC MarkStack drain step
* [QTBUG-147835](https://qt-project.atlassian.net/browse/QTBUG-147835) QML engine no longer adopts QObjects from smart variant
wrapper
* [QTBUG-146736](https://qt-project.atlassian.net/browse/QTBUG-146736) QML SFPM: FunctionFilter and FunctionSorter cannot find
filter or compare (sort) method when inherited
* [QTBUG-113724](https://qt-project.atlassian.net/browse/QTBUG-113724) ListView section delegates get tab focus after first row
of their section
* [QTBUG-144377](https://qt-project.atlassian.net/browse/QTBUG-144377) qmllint suggests to remove an import that is actually
used
* [QTBUG-148521](https://qt-project.atlassian.net/browse/QTBUG-148521) qmlformat: indent error (another one)
* [QTBUG-148180](https://qt-project.atlassian.net/browse/QTBUG-148180) qmlcontextpropertydump mismatch between host and target
build for vxworks
* [QTBUG-146164](https://qt-project.atlassian.net/browse/QTBUG-146164) Inconsistent close behavior for nested Popups across
popupType variants
* [QTBUG-147847](https://qt-project.atlassian.net/browse/QTBUG-147847) Dialog size incorrectly overridden by implicit size
resize logic when size is explicitly set
* [QTBUG-148683](https://qt-project.atlassian.net/browse/QTBUG-148683) Regression: Projects with QML modules fail to build
* [QTBUG-148618](https://qt-project.atlassian.net/browse/QTBUG-148618)  QQuickFontInfo::underline()/overline()/strikeOut()
declared but not implemented
* [QTBUG-146177](https://qt-project.atlassian.net/browse/QTBUG-146177) TextArea doesn't emit textEdited signal with é ç à
* [QTBUG-148164](https://qt-project.atlassian.net/browse/QTBUG-148164) Long property list<string> x: ... makes compilation take
forever
* [QTBUG-148696](https://qt-project.atlassian.net/browse/QTBUG-148696) QMLTC: QQuickItemChangeListener requires RTTI, blocking
compilation
* [QTBUG-148690](https://qt-project.atlassian.net/browse/QTBUG-148690) qmlls autocompletions: local importPaths (.qmlls.ini)
ignored when QML file is currently invalid
* [QTBUG-149041](https://qt-project.atlassian.net/browse/QTBUG-149041) Qt RHI D3D: Crash in backend due to dangling QWindow
pointer (missing unregisterWindow)
* [QTBUG-149005](https://qt-project.atlassian.net/browse/QTBUG-149005) tst_qquickmenu (Failed)
* [QTBUG-148695](https://qt-project.atlassian.net/browse/QTBUG-148695) VectorImage.generatedItem is not reset to null when the
source is cleared; it keeps a stale item from the previous load
* [QTBUG-149365](https://qt-project.atlassian.net/browse/QTBUG-149365) TextInput hides the selected text behind the selection
rectangle
* [QTBUG-149359](https://qt-project.atlassian.net/browse/QTBUG-149359) Qt Quick value types docs still missing \inqmlmodule
* [QTBUG-149089](https://qt-project.atlassian.net/browse/QTBUG-149089) qmlls returns no semantic tokens for any QML document
containing an `id` that starts with an underscore
* [QTBUG-146688](https://qt-project.atlassian.net/browse/QTBUG-146688) qmllint: bogus singleton warnings on examples
* [QTBUG-148729](https://qt-project.atlassian.net/browse/QTBUG-148729) qmllint: don't lint JS files like QML files
* [QTBUG-149307](https://qt-project.atlassian.net/browse/QTBUG-149307) Doing QQmlComponent::setData() repeatedly retains an
mmap of the cache file per iteration
* [QTBUG-149028](https://qt-project.atlassian.net/browse/QTBUG-149028) [QtQmlModels] ListModel.move(): signed integer overflow
in canMove() bypasses bounds check, crashes in std::rotate
* [QTBUG-149043](https://qt-project.atlassian.net/browse/QTBUG-149043) [QtQmlModels] FunctionSorter.compare() with untyped
parameters crashes unconditionally on first invocation
* [QTBUG-148815](https://qt-project.atlassian.net/browse/QTBUG-148815) PropertyChanges fails to rebind a property alias to a
BINDABLE property
* [QTBUG-149510](https://qt-project.atlassian.net/browse/QTBUG-149510) VectorImage: statusChanged(Ready) is emitted before
generatedItem exists, and a zero-size SVG reports status Ready with a
null generatedItem
* [QTBUG-149576](https://qt-project.atlassian.net/browse/QTBUG-149576) TextEdit.textDocument.source loads content without
emitting textChanged
* [QTBUG-120180](https://qt-project.atlassian.net/browse/QTBUG-120180) setting TextEdit.textDocument.source moves the cursor to
the end
* [QTBUG-148730](https://qt-project.atlassian.net/browse/QTBUG-148730) qmllint: missing-property warning on existing property
* [QTBUG-148643](https://qt-project.atlassian.net/browse/QTBUG-148643) ObjectRegistry: Use after free when using an unusual
usage pattern
* [QTBUG-143581](https://qt-project.atlassian.net/browse/QTBUG-143581) qmllint: no missing-property warning when writing into
unknown property
* [QTBUG-149373](https://qt-project.atlassian.net/browse/QTBUG-149373) Item textures are a device pixel short at fractional
devicePixelRatio
* [QTBUG-138244](https://qt-project.atlassian.net/browse/QTBUG-138244) No warning when exposing namepsace with lower case name
to QML
* [QTBUG-150766](https://qt-project.atlassian.net/browse/QTBUG-150766) REG: Error reading pregenerated distance field caches
spanning multiple textures
* [QTBUG-142189](https://qt-project.atlassian.net/browse/QTBUG-142189) QtQuick Switch mouse/touch tests fail related to center
point for macOS style
* [QTBUG-142186](https://qt-project.atlassian.net/browse/QTBUG-142186) MetaObject change in DelegateModel leads to crash in
Plasma
* [QTBUG-138532](https://qt-project.atlassian.net/browse/QTBUG-138532) qmllint: unterminated-case
* [QTBUG-53987](https://qt-project.atlassian.net/browse/QTBUG-53987) Cursor is not updated on mouse wheel over flickable
* [QTBUG-54019](https://qt-project.atlassian.net/browse/QTBUG-54019) regression in certain MouseArea hover use cases
* [QTBUG-90457](https://qt-project.atlassian.net/browse/QTBUG-90457) HoverHandler.cursorShape doesn't change dynamically
within same bounds
* [QTBUG-136976](https://qt-project.atlassian.net/browse/QTBUG-136976) QHoverEvent::HoverMove Triggered Repeatedly on
Stationary Mouse When Unrelated QQuickItem Changes
* [QTBUG-140340](https://qt-project.atlassian.net/browse/QTBUG-140340) [REG: 5->6] Input event delivery performance regression
in Qt 6
* [QTBUG-143113](https://qt-project.atlassian.net/browse/QTBUG-143113) tst_HoverHandler::touchDrag failing on QNX
* [QTBUG-143195](https://qt-project.atlassian.net/browse/QTBUG-143195) public QSGTextNode API is missing a way to add ranges of
colored text
* [QTBUG-143112](https://qt-project.atlassian.net/browse/QTBUG-143112) Fill not correctly rendered by curve renderer when pack
goes backwards
* [QTBUG-35598](https://qt-project.atlassian.net/browse/QTBUG-35598) QtQuick Controls TextField and TextArea miss mouse
context menu
* [QTBUG-143313](https://qt-project.atlassian.net/browse/QTBUG-143313) qmllint -  warnings about shadowing methods need to
silenced until they become actionable
* [QTBUG-140200](https://qt-project.atlassian.net/browse/QTBUG-140200) Modal QML Popup not modal to a11y layer
* [QTBUG-143483](https://qt-project.atlassian.net/browse/QTBUG-143483) Document new qmllint warnings (qmlShadow,
qmlPropertyOverride, qmlIdShadowsMember, ...)
* [QTBUG-143618](https://qt-project.atlassian.net/browse/QTBUG-143618) qmllint does not report parser warnings to the user
* [QTBUG-142436](https://qt-project.atlassian.net/browse/QTBUG-142436) QmlPreview's window handling is unreliable
* [QTBUG-143701](https://qt-project.atlassian.net/browse/QTBUG-143701) tst_QQuickContextMenu::textControlsMenuKey is flaky on
several platforms
* [QTBUG-141701](https://qt-project.atlassian.net/browse/QTBUG-141701) [a11y] App language is not transparent to Screen Reader
* [QTBUG-134903](https://qt-project.atlassian.net/browse/QTBUG-134903) Duplicate context menus when using custom context Menus
in text controls
* [QTBUG-116910](https://qt-project.atlassian.net/browse/QTBUG-116910) ToolTips are not easy to use
* [QTBUG-119261](https://qt-project.atlassian.net/browse/QTBUG-119261) Change signals for inset properties not emitted for
Popup/ToolTip
* [QTBUG-67720](https://qt-project.atlassian.net/browse/QTBUG-67720) CMake: Avoid to deliver Qt Labs binarys in an apk
* [QTBUG-68047](https://qt-project.atlassian.net/browse/QTBUG-68047) tst_qquicktext::hAlignImplicitWidth asserts on macOS
* [QTBUG-46487](https://qt-project.atlassian.net/browse/QTBUG-46487) PathView. DelegateModel::item: index out range error when
model is reset with less number of items
* [QTBUG-143916](https://qt-project.atlassian.net/browse/QTBUG-143916) Fix QDoc warnings for Qt 6.11
* [QTBUG-144278](https://qt-project.atlassian.net/browse/QTBUG-144278) QML compiler fails with -DQT_NO_CAST_FROM_ASCII=1
* [QTBUG-144582](https://qt-project.atlassian.net/browse/QTBUG-144582) [REG 6.11.0 -> 6.12.0] tst_qjsonbinding (Failed)
* [QTBUG-127648](https://qt-project.atlassian.net/browse/QTBUG-127648) DragEvent coordinates are rounded to nearest integer
when Item scale is a real value other than 1
* [QTBUG-136806](https://qt-project.atlassian.net/browse/QTBUG-136806) QtQml restores QmlIR from CompilationUnits when loading
AOT-compiled artefacts
* [QTBUG-144999](https://qt-project.atlassian.net/browse/QTBUG-144999) Build Failure with easingCurve Value Type in Direct Mode
* [QTBUG-115140](https://qt-project.atlassian.net/browse/QTBUG-115140) qtdeclarative -unity-build-batch-size 100000 fails
* [QTBUG-143173](https://qt-project.atlassian.net/browse/QTBUG-143173) Flickable margins are broken on non-scrolling axis
* [QTBUG-145384](https://qt-project.atlassian.net/browse/QTBUG-145384) Action of hidden Dialog steals shortcut from visible
Dialog
* [QTBUG-135879](https://qt-project.atlassian.net/browse/QTBUG-135879) TapHandler receives events in the background when a pop-
up window is active when using an active stylus.
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.
* [QTBUG-145861](https://qt-project.atlassian.net/browse/QTBUG-145861) tst_inputpanelcontrols (failed)
* [QTBUG-
146156](https://qt-project.atlassian.net/browse/QTBUG-146156) tst_QQuickFolderDialogImpl::Imagine::bindCurrentFolder(sub-dir-1)
fails, blocking dependency update
* [QTBUG-145799](https://qt-project.atlassian.net/browse/QTBUG-145799) qmlpreview doesn't work with loadFromModule()
* [QTBUG-144177](https://qt-project.atlassian.net/browse/QTBUG-144177) RHEL 10: qtdeclarative auto test failures on Wayland
* [QTBUG-143734](https://qt-project.atlassian.net/browse/QTBUG-143734) svgtoqml tool has hidden dependency on
QMinimalIntegrationPlugin
* [QTBUG-96304](https://qt-project.atlassian.net/browse/QTBUG-96304) Performance bad in handling events (especially wheel
events) in deep & large QML hierarchies
* [QTBUG-146552](https://qt-project.atlassian.net/browse/QTBUG-146552) A11y: QAccessible::state::expandable/expanded not fully
implemented
* [QTBUG-147250](https://qt-project.atlassian.net/browse/QTBUG-147250) lottietoqml: animated stroke properties (width and dash
offset) does not work
* [QTBUG-139833](https://qt-project.atlassian.net/browse/QTBUG-139833) [a11y] Auditive feedback during scroll missing
* [QTBUG-140673](https://qt-project.atlassian.net/browse/QTBUG-140673) a11y: QML ScrollBar doesn't report current
position/value on accessibility layer
* [QTBUG-142387](https://qt-project.atlassian.net/browse/QTBUG-142387) Internal error with Qt.callLater() on invalid context
* [QTBUG-104016](https://qt-project.atlassian.net/browse/QTBUG-104016) After calling Qt.CallLater C++ context is destroyed
while the QML contex is not
* [QTBUG-147406](https://qt-project.atlassian.net/browse/QTBUG-147406) Constructing QBindable from QProperty makes binaries
depend on the exact-versioned private symbol
QUntypedPropertyBinding(QPropertyBindingPrivate*)
* [QTBUG-147652](https://qt-project.atlassian.net/browse/QTBUG-147652) Do not unconditionally capitalize first word in brief
texts
* [QTBUG-148751](https://qt-project.atlassian.net/browse/QTBUG-148751) [REG 6.11.2->6.12.0] webenginequick/quicknanobrowser not
launching on linux and Windows
* [QTBUG-147828](https://qt-project.atlassian.net/browse/QTBUG-147828) TextArea.placeholderText does not respect wrapMode
* [QTBUG-147814](https://qt-project.atlassian.net/browse/QTBUG-147814) QML cold-load import resolution is dominated by qrc-
engine per-lookup cost
* [QTBUG-149361](https://qt-project.atlassian.net/browse/QTBUG-149361) Animated SVG loops broken: QMovie always plays one
cycle, AnimatedImage ignores `loops` and never finishes
* [QTBUG-148858](https://qt-project.atlassian.net/browse/QTBUG-148858) whitespaces in --codesign with
qt_generate_deploy_qml_app_script fails
* [QTBUG-149806](https://qt-project.atlassian.net/browse/QTBUG-149806) QtQuick.VectorImage leaks internal item tree on every
source change
* [QTBUG-149360](https://qt-project.atlassian.net/browse/QTBUG-149360) qmllint/qmlls segfaults when the imported QtQuick module
resolves without usable type information
* [QTBUG-149446](https://qt-project.atlassian.net/browse/QTBUG-149446) Qt 6.11.2: reading an alias-to-a-local-alias returns
garbage / crashes

### qtmultimedia
* [QTBUG-145861](https://qt-project.atlassian.net/browse/QTBUG-145861) tst_inputpanelcontrols (failed)
* [QTBUG-146764](https://qt-project.atlassian.net/browse/QTBUG-146764) SpatialSound [Quick3D] position changing is ignored in
Qt 6.11.1 (Regression from 6.11.0)
* [QTBUG-146787](https://qt-project.atlassian.net/browse/QTBUG-146787) [REG 6.11.1->6.12.0] multimedia/audiosource not compiled
on Android x86_64 and armv7
* [QTBUG-145207](https://qt-project.atlassian.net/browse/QTBUG-145207) wasm: iOS camera is oriented wrong
* [QTBUG-146027](https://qt-project.atlassian.net/browse/QTBUG-146027) wasm: screen capture fails
* [QTBUG-143782](https://qt-project.atlassian.net/browse/QTBUG-143782) wasm: Threadlock on main thread causes app freeze
* [QTBUG-147200](https://qt-project.atlassian.net/browse/QTBUG-147200) [REG Qt 6.11.0->6.11.1] Android: Deadlock on app
shutdown when QAndroidAudioDevices is destroyed
* [QTBUG-146803](https://qt-project.atlassian.net/browse/QTBUG-146803) [FFmpeg, Android]: tst_qtexttospeech (Failed)
* [QTBUG-147454](https://qt-project.atlassian.net/browse/QTBUG-147454) wasm: cannot display two cameras
* [QTBUG-147897](https://qt-project.atlassian.net/browse/QTBUG-147897) Camera recording doesn't work on Linux (Regression)
* [QTBUG-143067](https://qt-project.atlassian.net/browse/QTBUG-143067) Quitting a camera application hangs on HMD Skyline
TA-1600
* [QTBUG-133914](https://qt-project.atlassian.net/browse/QTBUG-133914) FFmpeg plugin tests may fail to build on Linux and
Android
* [QTBUG-149497](https://qt-project.atlassian.net/browse/QTBUG-149497) Windows, FFmpeg backend: QCamera::setCameraFormat()
ignores the frame rate of the format
* [QTBUG-149907](https://qt-project.atlassian.net/browse/QTBUG-149907) A muted SoundEffect silences the sound effects that
started before it
* [QTBUG-149917](https://qt-project.atlassian.net/browse/QTBUG-149917) An audio output device change doubles a playing
SoundEffect's voices
* [QTBUG-142743](https://qt-project.atlassian.net/browse/QTBUG-142743) QtMultimediaPrivate::QRtAudioEngine::getEngineFor crash
with remote connection
* [QTBUG-149229](https://qt-project.atlassian.net/browse/QTBUG-149229) Android: Deadlock on app shutdown when
QAndroidVideoDevices is destroyed
* [QTBUG-145999](https://qt-project.atlassian.net/browse/QTBUG-145999) iOS: QAudioSink remains ActiveState/NoError after audio
output silently stops
* [QTBUG-142694](https://qt-project.atlassian.net/browse/QTBUG-142694) [REG 6.8.3-6.10.1] Sporadic crashes on
QSoundEffectPrivateWithPlayer::play
* [QTBUG-138597](https://qt-project.atlassian.net/browse/QTBUG-138597) Grant Android runtime permissions to the android bundles
* [QTBUG-147533](https://qt-project.atlassian.net/browse/QTBUG-147533) Qt Multimedia FFmpeg backend cannot force RTSP-over-TCP
for QMediaPlayer RTSP streams
* [QTBUG-117901](https://qt-project.atlassian.net/browse/QTBUG-117901) Changing a text element can cause re-upload of entire
scene
* [QTBUG-147351](https://qt-project.atlassian.net/browse/QTBUG-147351) tst_QCameraBackend::testVirtualCameraRemoval flaky on CI
* [QTBUG-141688](https://qt-project.atlassian.net/browse/QTBUG-141688) Android: Camera does not recover after minimizing.
* [QTBUG-147146](https://qt-project.atlassian.net/browse/QTBUG-147146) Regression: Can's suspend QAudioSink just after calling
start() with a callback
* [QTBUG-148543](https://qt-project.atlassian.net/browse/QTBUG-148543) [iOS] QAudioSource fails to capture since 6.9 — open()
no longer sets the AVAudioSession category (AudioUnit init -10851)
* [QTBUG-148761](https://qt-project.atlassian.net/browse/QTBUG-148761) Upgrade to FFmpeg n9.0
* [QTBUG-148852](https://qt-project.atlassian.net/browse/QTBUG-148852) [MultiMedia] camera: Mute has no effect during video
recording.
* [QTBUG-147011](https://qt-project.atlassian.net/browse/QTBUG-147011) Crash on application exit in PipeWire audio backend —
QRtAudioEngine deleted synchronously after the event loop has stopped
(regression in 6.11.1)
* [QTBUG-150720](https://qt-project.atlassian.net/browse/QTBUG-150720) [REG 6.12.0 beta -> RC] Android: MediaPlayer example
cannot open any https source with the FFmpeg backend ("certificate
verify failed")

### qttools
* [QTBUG-142486](https://qt-project.atlassian.net/browse/QTBUG-142486) QDoc incorrectly processes links to articles whose
titles has the "#" symbol
* [QTBUG-143636](https://qt-project.atlassian.net/browse/QTBUG-143636) QDoc emits "No such parameter 'other'" warnings for
auto-generated SMF docs
* [QTBUG-143642](https://qt-project.atlassian.net/browse/QTBUG-143642) QDoc emits "Can't link to 'ClassName()'" warnings for
classes with Q_DISABLE_COPY
* [QTBUG-140343](https://qt-project.atlassian.net/browse/QTBUG-140343) Conversion operators get an extra return type
* [QTBUG-143856](https://qt-project.atlassian.net/browse/QTBUG-143856) QDoc: \list command silently ignores starting values
below 1
* [QTBUG-143769](https://qt-project.atlassian.net/browse/QTBUG-143769) QDoc: Inconsistent formatting of \compares,
\compareswith output
* [QTBUG-143569](https://qt-project.atlassian.net/browse/QTBUG-143569) QTimeEdit and QDateEdit show internal signals
* [QTBUG-144206](https://qt-project.atlassian.net/browse/QTBUG-144206) Qt Designer: Item widgets' items lack fully-qualified
enums
* [PYSIDE-3278](https://qt-project.atlassian.net/browse/PYSIDE-3278) pyside6-uic: Item widgets' items have enum setters that
are inconsistent with those of other classes
* [PYSIDE-2492](https://qt-project.atlassian.net/browse/PYSIDE-2492) uic does not generate enumeration name into enum values
causing type checking warnings
* [QTBUG-144445](https://qt-project.atlassian.net/browse/QTBUG-144445) QDoc: C++ module status is not propagated to module
members
* [QTBUG-144451](https://qt-project.atlassian.net/browse/QTBUG-144451) QDoc: \include snippet matching uses substring instead
of exact name
* [QTBUG-144788](https://qt-project.atlassian.net/browse/QTBUG-144788) \details command fails to parse macro or inline commands
in the summary
* [QTBUG-145113](https://qt-project.atlassian.net/browse/QTBUG-145113) QDoc: TemplateGenerator produces empty hrefs for same-
module collection and member entries
* [QTBUG-106220](https://qt-project.atlassian.net/browse/QTBUG-106220) Improve diagnostics when documenting non-declared
function
* [QTBUG-90708](https://qt-project.atlassian.net/browse/QTBUG-90708) Error message for wrong filename as value of
\quotefromfile is cryptic
* [QTBUG-119307](https://qt-project.atlassian.net/browse/QTBUG-119307) Qdoc table width argument doesn't work
* [QTBUG-95813](https://qt-project.atlassian.net/browse/QTBUG-95813) QDoc manual is inconsistent with --help output
* [QTBUG-111970](https://qt-project.atlassian.net/browse/QTBUG-111970) qdoc renders fixed-size array parameters incorrectly
* [QTBUG-145735](https://qt-project.atlassian.net/browse/QTBUG-145735) QDoc: ContentBuilder silently drops some (not all) Link
atoms
* [QTBUG-145738](https://qt-project.atlassian.net/browse/QTBUG-145738) QDoc: Skip already-resolved links and clear broken link
hrefs in resolver
* [QTBUG-145755](https://qt-project.atlassian.net/browse/QTBUG-145755) qdoc: improve \note in \enum \value block
* [QTBUG-145818](https://qt-project.atlassian.net/browse/QTBUG-145818) QDoc: Template generator aborts on undefined anchorId,
synopsis, and typeWord during full Qt doc build
* [QTBUG-145790](https://qt-project.atlassian.net/browse/QTBUG-145790) QDoc: no warning when \fn doc comment targets a hidden
friend function
* [QTBUG-124306](https://qt-project.atlassian.net/browse/QTBUG-124306) QHash: Document qHashEquals
* [QTBUG-145807](https://qt-project.atlassian.net/browse/QTBUG-145807) QDoc: Property anchor for shared notifier signals is
non-deterministic
* [QTBUG-145823](https://qt-project.atlassian.net/browse/QTBUG-145823) QDoc: Template generator crashes on classes with module
state or "Until" status
* [QTBUG-145914](https://qt-project.atlassian.net/browse/QTBUG-145914) QDoc: Template generator emits malformed anchor
attributes on section headings
* [QTBUG-145938](https://qt-project.atlassian.net/browse/QTBUG-145938) QDoc: Template generator fails to link qualified-name
references
* [QTBUG-145940](https://qt-project.atlassian.net/browse/QTBUG-145940) QDoc: Template generator drops section anchors from
resolved link URLs
* [QTBUG-146227](https://qt-project.atlassian.net/browse/QTBUG-146227) QDoc: Confusing output for \since command in a \qmlenum
topic
* [QTBUG-144141](https://qt-project.atlassian.net/browse/QTBUG-144141) QDoc: Hidden friend ADL resolution fails for out-of-line
defined friends
* [QTBUG-146577](https://qt-project.atlassian.net/browse/QTBUG-146577) QDoc: ASan validation reports use-after-poison against
libclang's BumpPtrAllocator
* [QTBUG-146599](https://qt-project.atlassian.net/browse/QTBUG-146599) QDoc: Restore alternating row classes in template-
generated tables
* [QTBUG-146604](https://qt-project.atlassian.net/browse/QTBUG-146604) QDoc: Synthesize module-page CMake metadata for Qt
command family
* [QTBUG-146603](https://qt-project.atlassian.net/browse/QTBUG-146603) QDoc: Restore markdown rendering whitespace integrity
around block tags
* [QTBUG-146721](https://qt-project.atlassian.net/browse/QTBUG-146721) QDoc: Preserve genus/domain hints when resolving
autolinks
* [QTBUG-146722](https://qt-project.atlassian.net/browse/QTBUG-146722) QDoc: Attribute broken-link warnings to the originator
* [QTBUG-146767](https://qt-project.atlassian.net/browse/QTBUG-146767) QDoc: indexes configuration variable does not resolve
relative paths against the qdocconf location
* [QTBUG-146863](https://qt-project.atlassian.net/browse/QTBUG-146863) QDoc: templateGenerator generates incorrect relative
links for cross-module references
* [QTBUG-146864](https://qt-project.atlassian.net/browse/QTBUG-146864) QDoc: TemplateGenerator duplicates anchor segments
* [QTBUG-146865](https://qt-project.atlassian.net/browse/QTBUG-146865) QDoc suppresses links to index-loaded nodes due to local
inclusion filtering
* [QTBUG-146866](https://qt-project.atlassian.net/browse/QTBUG-146866) QDoc: cannot identify upstream module for placeholder
collection nodes
* [QTBUG-146895](https://qt-project.atlassian.net/browse/QTBUG-146895) QDoc: Template generator leaks doc.qt.io URLs into
snapshot doc builds
* [QTBUG-146896](https://qt-project.atlassian.net/browse/QTBUG-146896) QDoc: PageMetadata URL field is empty for pages without
an explicit \url
* [QTBUG-147230](https://qt-project.atlassian.net/browse/QTBUG-147230) QDoc may crash when \relates targets an invalid relation
target, such as a module or group
* [QTBUG-146867](https://qt-project.atlassian.net/browse/QTBUG-146867) HTML id used for two different functions in QDataStream
* [QTBUG-147379](https://qt-project.atlassian.net/browse/QTBUG-147379) QDoc: (Template generator) table cells flatten rich
content to plain text
* [QTBUG-147380](https://qt-project.atlassian.net/browse/QTBUG-147380) QDoc: document showautogenerateddocs configuration
variable
* [QTBUG-147312](https://qt-project.atlassian.net/browse/QTBUG-147312) QDoc: \since in a \concept topic does not list concepts
in a \sincelist output
* [QTBUG-147135](https://qt-project.atlassian.net/browse/QTBUG-147135) QDoc: Impaired performance when generating projects with
no C++ documentation
* [QTBUG-147136](https://qt-project.atlassian.net/browse/QTBUG-147136) QDoc: Wildcard patterns in `excludefiles` configuration
variable do not work as expected
* [QTBUG-147504](https://qt-project.atlassian.net/browse/QTBUG-147504) QDoc ignores \internal comment blocks entirely unless
--showinternal is set
* [QTBUG-147619](https://qt-project.atlassian.net/browse/QTBUG-147619) QDoc: 'No documentation for' warnings generated for
slots with _q_ prefix
* [QTBUG-148305](https://qt-project.atlassian.net/browse/QTBUG-148305) CMake Error at
tst_validateQdocOutputFilesWrapperRelWithDebInfo.cmake
* [QTBUG-119610](https://qt-project.atlassian.net/browse/QTBUG-119610) QDoc: DocParser::getRestOfLine() doesn't chop trailing
backslash on Windows
* [QTBUG-149524](https://qt-project.atlassian.net/browse/QTBUG-149524) qdoc/webxml: Specifying several \fn tags for overloads
per function can cause  documentation to disappear from the .webxml
files
* [QTBUG-149320](https://qt-project.atlassian.net/browse/QTBUG-149320) \qmlattachedmethod is missing from qdoc command
reference
* [QTBUG-149298](https://qt-project.atlassian.net/browse/QTBUG-149298) QtObject QML documentation claims it's a singleton
* [QTBUG-150175](https://qt-project.atlassian.net/browse/QTBUG-150175) Support Clang/LLVM 23 in QDoc
* [QTBUG-138855](https://qt-project.atlassian.net/browse/QTBUG-138855) qttools test_i18n_subdir*_xcode tests are flaky
* [QTBUG-145851](https://qt-project.atlassian.net/browse/QTBUG-145851) QT_NO_SINGLE_ARG_QHASH may silently call a different
qHash() instead of complaining when a qHash() overload without a seed is
used.
* [QTBUG-139199](https://qt-project.atlassian.net/browse/QTBUG-139199) qttools configure error if llvm-provided packages are
used
* [QTBUG-143734](https://qt-project.atlassian.net/browse/QTBUG-143734) svgtoqml tool has hidden dependency on
QMinimalIntegrationPlugin
* [QTBUG-143274](https://qt-project.atlassian.net/browse/QTBUG-143274) QDoc: DocBook output missing template declarations in
function signatures
* [QTBUG-146905](https://qt-project.atlassian.net/browse/QTBUG-146905) QDoc: WebXML module pages are empty
* [QTBUG-126993](https://qt-project.atlassian.net/browse/QTBUG-126993) Qt Widgets Designer: Setting property visibility to
false in the property sheet does not change visibility
* [QTCREATORBUG-34100](https://qt-project.atlassian.net/browse/QTCREATORBUG-34100) Qt Widgets Designer Form Class Wizard templates
are aweful
* [QTBUG-100310](https://qt-project.atlassian.net/browse/QTBUG-100310) lupdate does not support trailing commas in Python

### qtdoc
* [QTBUG-141601](https://qt-project.atlassian.net/browse/QTBUG-141601) ColorPalette example uses inappropriate colors in dark
mode
* [QTBUG-144125](https://qt-project.atlassian.net/browse/QTBUG-144125) FAILED:
examples/demos/samegame/CMakeFiles/samegame_qmllint /home/qt/work/qt/qtd
oc_standalone_examples/examples/demos/samegame/CMakeFiles/samegame_qmlli
nt
* [QTBUG-144835](https://qt-project.atlassian.net/browse/QTBUG-144835) ToyCustomizer: fix 3D rendering on Showcase view
* [QTBUG-144916](https://qt-project.atlassian.net/browse/QTBUG-144916) Id for object PaginatedResource shadows property
"colors"
* [QTBUG-142732](https://qt-project.atlassian.net/browse/QTBUG-142732) [Reg 6.8.5 -> 6.10.1] FX & Material Showroom demo:
Camera controls no longer work
* [QTBUG-146827](https://qt-project.atlassian.net/browse/QTBUG-146827) [REG 6.11.1->6.12.0] demos/coffee not launching when
compiled with qmake
* [QTBUG-148837](https://qt-project.atlassian.net/browse/QTBUG-148837) The landing page https://doc.qt.io/qt-6/index.html does
not explain the essense of "Extensions"
* [QTBUG-149539](https://qt-project.atlassian.net/browse/QTBUG-149539) Put the actual content about Qt onto the "Product
information" page in docs
* [QTBUG-143916](https://qt-project.atlassian.net/browse/QTBUG-143916) Fix QDoc warnings for Qt 6.11
* [QTBUG-145074](https://qt-project.atlassian.net/browse/QTBUG-145074) Ambiguous type detected. App 254.0 is defined multiple
times
* [QTBUG-146674](https://qt-project.atlassian.net/browse/QTBUG-146674) Warning: C:/Users/qt/work/qt/qtdoc/examples/demos/todoli
st/content/NewTask.qml:64:5: unknown grouped property scope backButton
* [QTBUG-148699](https://qt-project.atlassian.net/browse/QTBUG-148699) FAILED:
examples/demos/samegame/CMakeFiles/samegame_qmllint /home/qt/work/qt/qtd
oc_standalone_examples/examples/demos/samegame/CMakeFiles/samegame_qmlli
nt
* [QTBUG-150075](https://qt-project.atlassian.net/browse/QTBUG-150075) FAILED:
examples/demos/osmbuildings/CMakeFiles/osmbuildings_qmllint /Users/qt/wo
rk/qt/qtdoc_standalone_examples/examples/demos/osmbuildings/CMakeFiles/o
smbuildings_qmllint
* [QTBUG-149044](https://qt-project.atlassian.net/browse/QTBUG-149044) Android: back key no longer delivers a close event to
the window

### qtqa
* [QTBUG-144457](https://qt-project.atlassian.net/browse/QTBUG-144457) Sbom license check with parentheses.

### qtlocation
* [QTBUG-144282](https://qt-project.atlassian.net/browse/QTBUG-144282) Incorrect usage of qFuzzyCompare() abounds in Qt source
[Qt Location]
* [QTBUG-143916](https://qt-project.atlassian.net/browse/QTBUG-143916) Fix QDoc warnings for Qt 6.11

### qtpositioning
* [QTBUG-142093](https://qt-project.atlassian.net/browse/QTBUG-142093) Top crashing test:
tst_QGeoAreaMonitorSource::multipleThreads
* [QTBUG-144952](https://qt-project.atlassian.net/browse/QTBUG-144952) Fix UB in Q{GeoPath,Polygon}Private
* [QTBUG-144929](https://qt-project.atlassian.net/browse/QTBUG-144929) QObject::disconnect(const Connection &) const_cast<>s
its argument

### qtsensors
* [QTBUG-145446](https://qt-project.atlassian.net/browse/QTBUG-145446) QtSensors needs QUIP23 security headers review
* [QTBUG-147834](https://qt-project.atlassian.net/browse/QTBUG-147834) [REG 6.12.0 beta1 -> beta2] sensors/showcase not
compiling on Android

### qtconnectivity
* [QTBUG-138597](https://qt-project.atlassian.net/browse/QTBUG-138597) Grant Android runtime permissions to the android bundles
* [QTBUG-147192](https://qt-project.atlassian.net/browse/QTBUG-147192) HarmonyOS: port QtConnectivity (bluetooth) module
* [QTBUG-144929](https://qt-project.atlassian.net/browse/QTBUG-144929) QObject::disconnect(const Connection &) const_cast<>s
its argument

### qtwayland
* [QTBUG-144115](https://qt-project.atlassian.net/browse/QTBUG-144115) Crash when destroying WaylandCompositor while some
clients are connected
* [QTBUG-137154](https://qt-project.atlassian.net/browse/QTBUG-137154) [Wayland] Graph gallery could not be run on fancy-
compositor
* [QTBUG-144800](https://qt-project.atlassian.net/browse/QTBUG-144800) Buffer sharing limitted to SHM in qtwayland compositors
* [QTBUG-131910](https://qt-project.atlassian.net/browse/QTBUG-131910) QWaylandSeat::sendFullKeyEvent does not handle AltGr and
numlock
* [QTBUG-144929](https://qt-project.atlassian.net/browse/QTBUG-144929) QObject::disconnect(const Connection &) const_cast<>s
its argument
* [QTBUG-109728](https://qt-project.atlassian.net/browse/QTBUG-109728) QtWayand documentation incomplete

### qt3d
* [QTBUG-146870](https://qt-project.atlassian.net/browse/QTBUG-146870) ARM64EC: qt3d build fails to /3rdparty/imgui/
* [QTBUG-147317](https://qt-project.atlassian.net/browse/QTBUG-147317) error: use of undeclared identifier 'QQml_colorProvider'

### qtimageformats
* [QTBUG-146201](https://qt-project.atlassian.net/browse/QTBUG-146201) ARM64EC: building qtimageformats fails to 3rdparty:
/libwebp/ + /libtiff/

### qtserialbus
* [QTBUG-144929](https://qt-project.atlassian.net/browse/QTBUG-144929) QObject::disconnect(const Connection &) const_cast<>s
its argument

### qtwebsockets
* [QTBUG-150785](https://qt-project.atlassian.net/browse/QTBUG-150785) wasm-ld: error:
/home/qt/work/install/target/lib/libQt6WebSockets.a(qwebsocket_p.cpp.o):
undefined symbol: QWebSocketPrivate::doClose

### qtwebchannel
* [QTBUG-144929](https://qt-project.atlassian.net/browse/QTBUG-144929) QObject::disconnect(const Connection &) const_cast<>s
its argument

### qtwebview
* [QTBUG-149209](https://qt-project.atlassian.net/browse/QTBUG-149209) Do not confuse users on the Welcome screen in QtC that
we would ship a browser

### qtcharts
* [QTBUG-145091](https://qt-project.atlassian.net/browse/QTBUG-145091) QtChart report a nullptr access warning when destroying
an OpenGL enabled chart
* [QTBUG-149235](https://qt-project.atlassian.net/browse/QTBUG-149235) The uic process failed to compile

### qtdatavis3d
* [QTBUG-147253](https://qt-project.atlassian.net/browse/QTBUG-147253) Windows 11 x64: MinGW GCC 15 werror in qtdatavis3d
* [QTBUG-147587](https://qt-project.atlassian.net/browse/QTBUG-147587) Reg->6.12/Wayland: QtDatavisualization examples no
longer work

### qtvirtualkeyboard
* [QTBUG-131374](https://qt-project.atlassian.net/browse/QTBUG-131374) The wordCandidateList field is not visible on the
virtual keyboard in a widget application.

### qtscxml
* [QTBUG-144929](https://qt-project.atlassian.net/browse/QTBUG-144929) QObject::disconnect(const Connection &) const_cast<>s
its argument

### qtspeech
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-144929](https://qt-project.atlassian.net/browse/QTBUG-144929) QObject::disconnect(const Connection &) const_cast<>s
its argument

### qtnetworkauth
* [QTBUG-147593](https://qt-project.atlassian.net/browse/QTBUG-147593) Qt Network Authorization is missing links to source code
in its C++ Reference
* [QTBUG-148994](https://qt-project.atlassian.net/browse/QTBUG-148994) tst_QOAuthHttpServerReplyHandler::localhostHttps()
Compared values are not the same
* [QTBUG-144929](https://qt-project.atlassian.net/browse/QTBUG-144929) QObject::disconnect(const Connection &) const_cast<>s
its argument

### qtremoteobjects
* [QTBUG-144493](https://qt-project.atlassian.net/browse/QTBUG-144493) Review, possibly improve, and document comment behavior
in QtRO .rep file
* [QTBUG-143752](https://qt-project.atlassian.net/browse/QTBUG-143752) Find and fix QRemoteObject* classes whose Q_PROPERTY
properties are writable from QML side but not notifiable
* [QTBUG-146198](https://qt-project.atlassian.net/browse/QTBUG-146198) Reg=>6.12: Crash in QtRemoteObjects when comparing
QVariant of a dynamically created enum against int
* [QTBUG-143519](https://qt-project.atlassian.net/browse/QTBUG-143519) Improve Qt Remote Object Compiler logics when dealing
with strings
* [QTBUG-147375](https://qt-project.atlassian.net/browse/QTBUG-147375) HarmonyOS: port qtremoteobject module

### qtlottie
* [QTBUG-142546](https://qt-project.atlassian.net/browse/QTBUG-142546) lottietoqml: Remaining issues with time offsets
* [QTBUG-145066](https://qt-project.atlassian.net/browse/QTBUG-145066) Lottie: opacity of linked layer's transform shouldn't be
applied
* [QTBUG-146801](https://qt-project.atlassian.net/browse/QTBUG-146801) FAIL!  : tst_VectorImage::parseBrokenFile()
'!item->childItems().isEmpty()' returned FALSE
* [QTBUG-147250](https://qt-project.atlassian.net/browse/QTBUG-147250) lottietoqml: animated stroke properties (width and dash
offset) does not work
* [QTBUG-143151](https://qt-project.atlassian.net/browse/QTBUG-143151) lottietoqml: Support combinations of animated paths
* [QTBUG-148400](https://qt-project.atlassian.net/browse/QTBUG-148400) Anchor point-only animation is silently skipped
* [QTBUG-147789](https://qt-project.atlassian.net/browse/QTBUG-147789) Gradient fill renders incorrectly when shape has an
inner group transform

### qtquick3d
* [QTBUG-145014](https://qt-project.atlassian.net/browse/QTBUG-145014) [Frustum Culling] Shadows disappear when caster is
culled but its shadow remains in view.
* [QTBUG-146613](https://qt-project.atlassian.net/browse/QTBUG-146613) ARM64EC: qtquick3d build fails to
\3rdparty\meshoptimizer\
* [QTBUG-148517](https://qt-project.atlassian.net/browse/QTBUG-148517) [Sky Material] after update Qt 6.12 Beta 2 flickering
lighting appeared, although the environment itself changes relatively
smoothly.
* [QTBUG-140404](https://qt-project.atlassian.net/browse/QTBUG-140404) QQuick3DViewport::pick() returns no result if there is
only backfaces under mouse
* [QTBUG-150709](https://qt-project.atlassian.net/browse/QTBUG-150709) Visibility changes to models in different layers does
not always work
* [QTBUG-150753](https://qt-project.atlassian.net/browse/QTBUG-150753) visionOS: Rendering broken
* [QTBUG-146558](https://qt-project.atlassian.net/browse/QTBUG-146558) QVectorND are equality-comparable, but not hashable
* [QTBUG-144929](https://qt-project.atlassian.net/browse/QTBUG-144929) QObject::disconnect(const Connection &) const_cast<>s
its argument

### qtshadertools
* [QTBUG-145988](https://qt-project.atlassian.net/browse/QTBUG-145988) QtShaderTools: investigate op==/qHash() asymmetries
* [QTBUG-146851](https://qt-project.atlassian.net/browse/QTBUG-146851) qt6_add_shaders fails when shader file paths contain '@'
characters

### qt5compat
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST
* [QTBUG-144929](https://qt-project.atlassian.net/browse/QTBUG-144929) QObject::disconnect(const Connection &) const_cast<>s
its argument
* [QTBUG-149054](https://qt-project.atlassian.net/browse/QTBUG-149054) QBinaryJson::to{Raw,Binary}Data() does not own the
allocated memory
* [QTBUG-149430](https://qt-project.atlassian.net/browse/QTBUG-149430) QStringRef can compute a negative size when passed a Qt6
QString

### qtcoap
* [QTBUG-144351](https://qt-project.atlassian.net/browse/QTBUG-144351) Test 'qcoapoption' crashed on Android 16 startup due to
missing 'libQt6Network_x86_64.so' library

### qtopcua
* [QTBUG-143916](https://qt-project.atlassian.net/browse/QTBUG-143916) Fix QDoc warnings for Qt 6.11
* [QTBUG-144929](https://qt-project.atlassian.net/browse/QTBUG-144929) QObject::disconnect(const Connection &) const_cast<>s
its argument

### qtlanguageserver
* [QTBUG-141558](https://qt-project.atlassian.net/browse/QTBUG-141558) Replace instances of QT_NO_ASCONST with QT_NO_QASCONST

### qthttpserver
* [QTBUG-144180](https://qt-project.atlassian.net/browse/QTBUG-144180) "ERROR: AddressSanitizer: stack-use-after-return" in
tst_QHttpServer::checkRouteLambdaCapture()
* [QTBUG-143593](https://qt-project.atlassian.net/browse/QTBUG-143593) Add maximum_connections to QHttpServerConfiguration
* [QTBUG-144929](https://qt-project.atlassian.net/browse/QTBUG-144929) QObject::disconnect(const Connection &) const_cast<>s
its argument

### qtquick3dphysics
* [QTBUG-146708](https://qt-project.atlassian.net/browse/QTBUG-146708) HarmonyOS: PTHREAD_CANCEL_DISABLE defined, but no
related pthread functions available
* [QTBUG-146978](https://qt-project.atlassian.net/browse/QTBUG-146978) ARM64EC: qtquick3dphysics build fatal error LNK1361

### qtgrpc
* [QTBUG-146735](https://qt-project.atlassian.net/browse/QTBUG-146735) Qt6ProtobufWellKnownTypes config fails to find .proto
files when cross-compiling
* [QTBUG-146828](https://qt-project.atlassian.net/browse/QTBUG-146828) Host protoc lookup unreliable in cross-compile builds
* [QTBUG-147222](https://qt-project.atlassian.net/browse/QTBUG-147222) qtgrpc fails to configure on yocto (meta-qt6)
* [QTBUG-148062](https://qt-project.atlassian.net/browse/QTBUG-148062) GRPC: Client crashes when writing a large number of
messages to a streaming RPC
* [QTBUG-147934](https://qt-project.atlassian.net/browse/QTBUG-147934) QtGrpc: Provide write backpressure for streaming RPCs
* [QTBUG-148149](https://qt-project.atlassian.net/browse/QTBUG-148149) QGrpcHttp2Channel: sanitize server-controlled bytes in
warning logs
* [QTBUG-147829](https://qt-project.atlassian.net/browse/QTBUG-147829) QGrpcHttp2Channel: add exponential reconnect backoff
* [QTBUG-144005](https://qt-project.atlassian.net/browse/QTBUG-144005) Make FINAL attribute of qtprotobuf class properties
configurable
* [QTBUG-144179](https://qt-project.atlassian.net/browse/QTBUG-144179) "ERROR: AddressSanitizer: use-after-poison" in qtgrpc
* [QTBUG-145124](https://qt-project.atlassian.net/browse/QTBUG-145124) QML and protobuf: Issue with repeated nested message
* [QTBUG-145935](https://qt-project.atlassian.net/browse/QTBUG-145935) GRPC: Add test coverage for Protobuf JSON serialization
* [QTBUG-148066](https://qt-project.atlassian.net/browse/QTBUG-148066) GRPC: Allow bounding the outgoing message queue for
streaming RPCs

### qtquickeffectmaker
* [QTBUG-144260](https://qt-project.atlassian.net/browse/QTBUG-144260) Fix "unlinked page" messages

### qtgraphs
* [QTBUG-142686](https://qt-project.atlassian.net/browse/QTBUG-142686) Memory leak when querying max texture size
* [QTBUG-143757](https://qt-project.atlassian.net/browse/QTBUG-143757) QtGraphs fails Yocto build for meta-qt6
* [QTBUG-145607](https://qt-project.atlassian.net/browse/QTBUG-145607) Graphs2D doesn't build without Quick3D
* [QTBUG-145248](https://qt-project.atlassian.net/browse/QTBUG-145248) labelFormat non ascii characters cannot be displayed
* [QTBUG-147244](https://qt-project.atlassian.net/browse/QTBUG-147244) QtGraphs fails Yocto build for meta-qt6
* [QTBUG-145578](https://qt-project.atlassian.net/browse/QTBUG-145578) Ghost lines appear after removing a series from a multi-
series chart
* [QTBUG-147540](https://qt-project.atlassian.net/browse/QTBUG-147540) QGraphsView::removeSeries is not thread-safe: crash
after removal
* [QTBUG-147722](https://qt-project.atlassian.net/browse/QTBUG-147722) [Reg 6.11.1 -> 6.12.0b1] DateTimeAxis incorrectly rounds
sub-minute intervals
* [QTBUG-148514](https://qt-project.atlassian.net/browse/QTBUG-148514) Crash when a selected point is removed and the user
presses empty space again
* [QTBUG-147723](https://qt-project.atlassian.net/browse/QTBUG-147723) [Reg 6.11.1 -> 6.12.0b1] GraphsView axes are incorrectly
positioned at startup
* [QTBUG-149369](https://qt-project.atlassian.net/browse/QTBUG-149369) QQuickDragHandler list desyncs from marker list in
PointRenderer, when dragging after a marker teardown/rebuild
* [QTBUG-149930](https://qt-project.atlassian.net/browse/QTBUG-149930) GraphsView: Toggling panStyle/zoomStyle can lead to a
crash
* [QTBUG-150193](https://qt-project.atlassian.net/browse/QTBUG-150193) QtGraphs2D.impl dependency is not set in qmldir causing
a crash
* [QTBUG-142704](https://qt-project.atlassian.net/browse/QTBUG-142704) AreaSeries fills wrong parts of the graph and may
sometimes flicker when points are removed
* [QTBUG-143258](https://qt-project.atlassian.net/browse/QTBUG-143258) API Review: Should the timeZone be QTimeZone instead of
string
* [QTBUG-143622](https://qt-project.atlassian.net/browse/QTBUG-143622) Incorrect usage of qFuzzyCompare() abounds in Qt source
[QtGraphs and QtDatavis]
* [QTBUG-143860](https://qt-project.atlassian.net/browse/QTBUG-143860) API Review: The changed signal argument cannot have the
same name as the property they are signaling for
* [QTBUG-142559](https://qt-project.atlassian.net/browse/QTBUG-142559) Memory use goes up steadily when re-creating GraphsView
* [QTBUG-144866](https://qt-project.atlassian.net/browse/QTBUG-144866) ValueAxis title overlaps tick labels in GraphsView
* [QTBUG-148186](https://qt-project.atlassian.net/browse/QTBUG-148186) Graphs 2D: Painter backend doesn't use synchronizing

### qttasktree
* [QTBUG-144929](https://qt-project.atlassian.net/browse/QTBUG-144929) QObject::disconnect(const Connection &) const_cast<>s
its argument

### qtopenapi
* [QTBUG-147745](https://qt-project.atlassian.net/browse/QTBUG-147745) code generation error with openapi: 3.1.0
* [QTBUG-147530](https://qt-project.atlassian.net/browse/QTBUG-147530) JAVA invoked as bare unqualified command in the
Qt6OpenApiToolsGeneratorMacros.cmake file
* [QTBUG-149429](https://qt-project.atlassian.net/browse/QTBUG-149429) Replace quoted includes with angle-bracket includes in
OpenAPI public headers

### qtcanvaspainter
* [QTBUG-146192](https://qt-project.atlassian.net/browse/QTBUG-146192) Path group issue when two paths share the same group and
the QCanvasPath addresses happen to be the same
* [QTBUG-144925](https://qt-project.atlassian.net/browse/QTBUG-144925) Canvas Painter cannot render
underline/overline/strikeout text
* [QTBUG-147481](https://qt-project.atlassian.net/browse/QTBUG-147481) Unused glyph logic broken (missing) from distance field
glyph cache
* [QTBUG-143321](https://qt-project.atlassian.net/browse/QTBUG-143321) canvaspainter/compacthealth not launching on SLES 15 SP6
* [QTBUG-144831](https://qt-project.atlassian.net/browse/QTBUG-144831) Path caching not working as expected with certain
settings
* [QTBUG-144910](https://qt-project.atlassian.net/browse/QTBUG-144910) QCanvasPainterWidget and QRhiWidget are unexpectedly
slow with Vulkan on some platforms
* [QTBUG-147258](https://qt-project.atlassian.net/browse/QTBUG-147258) New example canvas2d/canvas2dtester not launching from
installed location
* [QTBUG-149588](https://qt-project.atlassian.net/browse/QTBUG-149588) Custom brush animations not working
* [QTBUG-149400](https://qt-project.atlassian.net/browse/QTBUG-149400) canvas2dtester example not available in Qt Creator
* [QTBUG-150086](https://qt-project.atlassian.net/browse/QTBUG-150086) Canvas2D BoxShadow radius not working correctly

### qtapplicationmanager (Commercial only)
* [QTBUG-129127](https://qt-project.atlassian.net/browse/QTBUG-129127) Fix problems with the new am_package CMake macros
* [QTBUG-144122](https://qt-project.atlassian.net/browse/QTBUG-144122) [qtapplicationmanager] do_install_ptest_base fails due
to duplicate copy target race condition in bubblewrap test
* [QTBUG-147286](https://qt-project.atlassian.net/browse/QTBUG-147286) tst_main (Failed)

### qtinterfaceframework (Commercial only)
* [QTBUG-147753](https://qt-project.atlassian.net/browse/QTBUG-147753) ModuleNotFoundError: No module named 'qface'
* [QTBUG-148650](https://qt-project.atlassian.net/browse/QTBUG-148650) Error: two test QML modules deploy to the same directory
"Simu" under resfile/qml

### qmlcompilerplus (Commercial only)
* [QTBUG-147164](https://qt-project.atlassian.net/browse/QTBUG-147164) error: no matching constructor for initialization of
'QQmlJSCodeGenerator'
* [QTBUG-148626](https://qt-project.atlassian.net/browse/QTBUG-148626) Error: two test QML modules deploy to the same directory
"QmlBench" under resfile/qml

Known Issues
------------
* Check that your system meets Qt's requirements:
  https://doc-snapshots.qt.io/qt6-6.12/supported-platforms.html
* RTA reported issues from Qt 6.12
  https://qt-project.atlassian.net/issues/?filter=24555
* See Qt 6.12 known issues from:
  https://wiki.qt.io/Qt_6.12_Known_Issues
* Qt 6.12.0 Open issues in Jira:
  https://qt-project.atlassian.net/issues/?filter=24554

Credits for the release goes to:
---------------------------------

* Eirik Aavitsland
* Cristian Adam
* Chris Adams
* Laszlo Agocs
* Dilek Akcay
* Owais Akhtar
* Dmitrii Akshintsev
* Alexander Akulich
* Konsta Alajärvi
* Stanislav Aleksandrov
* Even Oscar Andersen
* Purdea Andrei
* Dimitrios Apostolou
* Viktor Arvidsson
* Xavier BESSON
* Mate Barany
* Thierry Bastian
* Rogelio J. Baucells
* Oliver Beard
* Andreas Belke
* Vladimir Belyavsky
* Jens Bender
* Nicholas Bennett
* Lena Biliaieva
* Alex Blasche
* Tim Blechmann
* Eskil Abrahamsen Blomfeldt
* David Boddie
* Tatiana Borisova
* Joerg Bornemann
* Rym Bouabid
* Assam Boudjelthia
* Carlo Bramini
* Aurélien Brooke
* Kai Uwe Broulik
* Alex Bu
* Oswald Buddenhagen
* Robin Burchell
* Eren Bursali
* Olivier De Cannière
* Alexei Cazacov
* Jean-Michaël Celerier
* Christophe Chapuis
* Kaloyan Chehlarski
* Luqiao Chen
* Michael Cho
* Wang Chuan
* Zbigniew Chyla
* Albert Astals Cid
* Paul Colby
* Alexandru Croitor
* Christoph Cullmann
* Mitch Curtis
* Giuseppe D'Angelo
* Pranta Dastider
* Daniele E. Domenichelli
* Jake Drahos
* Pavel Dubsky
* Artem Dyomin
* Adrian Eddy
* Alexey Edelev
* David Edmundson
* Oliver Eftevaag
* Christian Ehrlicher
* Hatem ElKharashy
* Andreas Eliasson
* Susumu Endo
* Fabio Falsini
* David Faure
* Mylo Fawcett
* Ilya Fedin
* Nicolas Fella
* Simo Fält
* Zoltan Gera
* John Paul Adrian Glaubitz
* Joshua Goins
* Julian Greilich
* Robert Griebl
* Magnus Groß
* Jan Grulich
* Kaj Grönholm
* Nicolas Guichard
* Lin Guo
* Richard Moe Gustavsen
* Lucie Gérard
* Mikko Hallamaa
* Pinlong Han
* Inkamari Harjula
* Andre Hartmann
* Andreas Hartmetz
* Pete Hau
* Elias Hautala
* Tero Heikkinen
* Jani Heikkinen
* Miikka Heikkinen
* Moss Heim
* Jeff Heller
* Liu Heng
* Ulf Hermann
* Øystein Heskestad
* Volker Hilsheimer
* Dominik Holland
* Zhang Hongyuan
* Mats Honkamaa
* Xaver Hugl
* Samuli Hölttä
* Riccardo Ieva
* Ayesha Ishaq
* Linus Jahn
* Masoud Jami
* Morteza Jamshidi
* Johnny Jazeix
* Allan Sandfeld Jensen
* Tim Jenssen
* Lau Jespersen
* Wu JiangYu
* Jukka Jokiniva
* ULADZISLAU KUZMIN
* Jonas Karlsson
* Sergey Katunin
* Rainer Keller
* Igor Khanin
* Ali Kianian
* Dennis Kim
* Kwangsub Kim
* Friedemann Kleint
* André Klitzing
* Michal Klocek
* Ingo Klöcker
* Seokha Ko
* Jarek Kobus
* Kai Koehne
* Sze Howe Koh
* Jarkko Koivikko
* Antti Kokko
* Niko Korkala
* Tomi Korpipää
* Fabian Kosmale
* Volker Krause
* Mike Krus
* Adam Krzykala
* Anton Kudryavtsev
* Santhosh Kumar
* Jonas Kvinge
* Kai Köhne
* Cristian Le
* Inho Lee
* Frédéric Lefebvre
* Paul Lemire
* Marek Lesniak
* Pier-Yves Lessard
* Wladimir Leuschner
* Lewis
* Xiong LinLin
* Felix Lionardo
* Shane Liu
* Jie Liu
* Shaohua Luo
* Robert Löhning
* Stuart MacDonald
* Thiago Macieira
* Olaf Mandel
* Sergio Martins
* Leena Miettinen
* Shveta Mittal
* Jan Moeller
* Safiyyah Moosa
* Sheree Morphett
* Kenji Mouri
* Ahmad Hasan Mubashshir
* Marc Mutz
* Antti Määttä
* Martin Neudorfer
* Bartlomiej Neumann
* Andy Nichols
* Daniel Nicoletti
* Mårten Nordheim
* Dennis Oberst
* Sukyoung Oh
* Kimmo Ollila
* Frank Osterfeld
* Matti Paaso
* Kwanghyo Park
* Weisser, Pascal
* Jerome Pasion
* Miika Pernu
* Mauro Persano
* Evgen Pervenenka
* Vyacheslav Petrovets
* Nhung Pham
* Samuli Piippo
* Karim Pinter
* Timur Pocheptsov
* Lauri Pohjanheimo
* Joni Poikelin
* Gleb Popov
* Rami Potinkara
* Lorn Potter
* Sakaria Pouke
* Shyamnath Premnadh
* Dheerendra Purohit
* Imre Péntek
* MohammadHossein Qanbari
* Liang Qi
* Darshan Ramesh
* Matthias Rauter
* David Redondo
* Arno Rehn
* Topi Reinio
* Konstantin Ritt
* Alexey Rochev
* Shawn Rutledge
* Manikandan K. S.
* Toni Saario
* Ahmad Samir
* Volodymyr Samokhatko
* Timon Sassor
* Daniel Savi
* Lars Schmertmann
* David Schulz
* Luca Di Sera
* Dmitry Shachnev
* Nick Shaforostov
* Sami Shalayel
* Eugene Shalygin
* Raman Shamotsin
* Andy Shaw
* Gilsu Shin
* Venugopal Shivashankar
* Pierre-Yves Siret
* Kristoffer Skau
* Nils Petter Skålerud
* John Smith
* Ivan Solovev
* André Somers
* Axel Spoerl
* Patrick Stewart
* Magdalena Stojek
* Christian Strømme
* Tarja Sundqvist
* Lars Sutterud
* Tasuku Suzuki
* Michael Szczerba
* Michał Szolc
* Jan Arve Sæther
* Morten Sørvig
* Sadegh Taghavi
* Patrik Teivonen
* Nodir Temirkhodjaev
* John Thacker
* Alexandros Theodotou
* Marcus Tillmanns
* Aleksandr Timofeev
* Ivan Tkachenko
* Elias Toivola
* Jens Trillmann
* Jere Tuliniemi
* Paul Olav Tvete
* Esa Törmänen
* Tuomas Vaarala
* Jonathan Vannier
* Sami Varanka
* Doris Verria
* Tor Arne Vestbø
* Ville Voutilainen
* Juha Vuolle
* Olli Vuolteenaho
* Sune Vuorela
* Jaishree Vyas
* Vadim Vysokoostrovskiy
* Jannis Völker
* Jenny Wang
* Miao Wang
* Yixue Wang
* Aleksander Wawrzyniak
* Michael Weghorn
* Bernd Weimer
* Edward Welbourne
* Paul Wicking
* Piotr Wiercinski
* Anna Wojciechowska
* Szymon Wojtach
* Oliver Wolff
* Han Xueyan
* Lu YaNing
* Andrei Yankovich
* Semih Yavuz
* Jasuhan Yoganathan
* Wang Yu
* He YuMing
* Zhao Yuhang
* Erin of Yukis
* Sol ZHu
* Vlad Zahorodnii
* Arkadiusz Zarębski
* Oleksii Zbykovskyi
* Li Zequan
* Alexey Zerkin
* Chloe Zhai
* JiDe Zhang
* Yingzhen Zhao
* Liu Zheng
* Sol Zhu
* Wang Zichong
* Eike Ziller
* Volodymyr Zolotopupov
* hjk
* Johanna Äijälä
* İsa Tunahan Öztürk
* Dawid Śliwa
* Жора Змейкин
