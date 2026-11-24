Release notes
=============
Qt 6.12.1 release is a patch release made on the top of Qt 6.12.0.
As a patch release, Qt 6.12.1 does not add any new functionality but provides
bug fixes and other improvements and maintains both forward and backward
compatibility (source and binary) with the 6.12.x series.

For detailed information about Qt 6.12, refer to the online documentation
included in this distribution. The documentation is also available online:

https://doc.qt.io/qt-6/index.html

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


Important Changes
-----------------

### Security fixes
* [CVE-2026-95611](https://nvd.nist.gov/vuln/detail/CVE-2026-95611) in qtsvg
* [CVE-2026-100140](https://nvd.nist.gov/vuln/detail/CVE-2026-100140) in qt5compat
* [CVE-2026-105924](https://nvd.nist.gov/vuln/detail/CVE-2026-105924) in qtbase
* [CVE-2026-105925](https://nvd.nist.gov/vuln/detail/CVE-2026-105925) in qt5compat
* [CVE-2026-105943](https://nvd.nist.gov/vuln/detail/CVE-2026-105943) in qtbase
* [CVE-2026-110944](https://nvd.nist.gov/vuln/detail/CVE-2026-110944) in qthttpserver
* [CVE-2026-111487](https://nvd.nist.gov/vuln/detail/CVE-2026-111487) in qt3d
* [CVE-2026-114366](https://nvd.nist.gov/vuln/detail/CVE-2026-114366) in qtwebsockets
* [CVE-2026-114369](https://nvd.nist.gov/vuln/detail/CVE-2026-114369) in qtwebsockets
* [CVE-2026-116337](https://nvd.nist.gov/vuln/detail/CVE-2026-116337) in qtbase
* [CVE-2026-118968](https://nvd.nist.gov/vuln/detail/CVE-2026-118968) in qtmultimedia
* [CVE-2026-120973](https://nvd.nist.gov/vuln/detail/CVE-2026-120973) in qtconnectivity
* [CVE-2026-121815](https://nvd.nist.gov/vuln/detail/CVE-2026-121815) in qtdeclarative
* [CVE-2026-123706](https://nvd.nist.gov/vuln/detail/CVE-2026-123706) in qtdeclarative
* [CVE-2026-124670](https://nvd.nist.gov/vuln/detail/CVE-2026-124670) in qtbase
* [CVE-2026-126606](https://nvd.nist.gov/vuln/detail/CVE-2026-126606) in qtsvg
* [CVE-2026-131915](https://nvd.nist.gov/vuln/detail/CVE-2026-131915) in qtbase

### qtbase
* 3c687a8cd5a Fix targeted D-Bus signals always starting well-known
  services
    * Fixed a bug that caused QDBusMessage not to obey the setting of
      setAutoStartService() when sending a signal targeted to a well-
      known service name.

* d858876a41f QDBusMessage: reject empty interface names in signals
    * Fixed a bug that caused QDBusConnection to crash when attempting
      to send a signal QDBusMessage with an empty interface.

* 7e1c2e5cbcc windeployqt: Deploy the third-party libraries the Qt
  libraries need
    * windeployqt now deploys the non-Qt libraries that the deployed
      binaries link against, if those libraries are located in the Qt
      binary directory. This is the case for a Qt that was built against
      system libraries instead of the bundled ones, for example a Qt
      from a package manager. Pass --no-third-party-libraries to turn
      this off.

* 8ddeb85691d QXmlStreamReader: don't resolve the DTD before it is
  complete
    * notationDeclarations() and entityDeclarations() no longer return
      something while the DTD's internal subset is still being parsed,
      which a caller can observe from a comment or processing
      instruction inside the DTD. They could only give a partial answer
      there, and did so by removing those declarations from the parser,
      corrupting the remainder of the parse. They return an empty list
      now.

* db67ef7b288 QByteArray: fix UB (signed overflow) in
  fromBase64Encoding()
    * Fixed an integer overflow in fromBase64Encoding() that could lead
      to a buffer overflow.

* bb135c7dae2 QCollator/Darwin: fix handling of UCGetCollationKey()
  return status
    * Fixed a bug in creating QCollatorSortKeys for empty strings on
      Apple systems without ICU. Please note the Apple API has behavior
      quirks making sort keys collate differently from
      QCollator::compare(). Users are advised to build with ICU to get
      identical behavior in all platforms.

* ee259ae879b QString: fix UB (type mismatch) in asprintf() %jd handling
    * Fixed asprintf() to correctly extract `j` as intmax_t, not as long
      int.

* 38bb7edf0e4 QXmlStreamReader: clear entityLength in init()
    * Fixed several bugs that would cause compliant documents to run
      into entityExpansionLimit() when a QXmlStreamReader instance was
      reused (clear(), setDevice(), ...). A backwards-compatible work
      around is to create a new QXmlStreamReader for each XML document
      to parse.

* 3c25467efe6 QString: add missing %j length modifier to asprintf()'s %u
    * Fixed asprintf() ignoring %ju/%jx/%jo (uintmax_t arguments), which
      let format string and argument list get out of sync, potentially
      leading to memory errors (%s, %n).

* 249cfdbae6d QString: fix UB (OOB read) in insert(i, QL1SV)
    * Fixed bugs in insert(QLatin1StringView): insertion of a string
      that starts with a NUL byte was skipped and was indexing out of
      bounds of empty, non-null QLatin1StringViews.

* ec49e23877b Avoid libdbus abort/corrupt message when cross-marshalling
  a Unix fd
    * Fixed a crash (libdbus assertion) or corrupt message when cross-
      marshalling a QDBusArgument carrying a unix file descriptor whose
      dup() fails: the send now fails with a D-Bus error instead of
      aborting the process.

* ee7f3479436 QAbstractFileProvider: forward-declare QFileInfo
    * qabstractfileiconprovider.h no longer includes qfileinfo.h;
      qfileiconprovider.h no longer includes qfileinfo.h and
      qscopedpointer.h.

* ecdff5005d0 QXmlStreamReader: fix parameter entities leaking from one
  doc to the next
    * Fixed bugs that caused entities and parameter entities to leak
      from document to document when the QXmlStreamReader instance was
      reused (clear(), setDevice(), ...). A backwards-compatible work-
      around is to use QXmlStreamReader instances for only one XML
      document each, and not across mulitple documents.

* a887c4939c0 QThread: fix improper check for adoption in
  setTerminationEnabled()
    * Fixed an improper condition in checking if the current thread was
      started with QThread in the implementation of
      setTerminationEnabled() - previously, the check concluded all
      threads were started with it. This function is documented to only
      work with those threads started with QThread.

* 1fcd9a59c87 Detect malformed format in temporal data parsing and
  refuse to parse
    * Fixed a bug in (only) 6.12.0's parsing of dates and times that
      meant an unmatched single quote in a format string could lead to
      an apparently valid parse of an empty string. Prior to 6.12 the
      handling of single quotes did not match the documentation or their
      handling during serialization and the handling of an unmatched
      single quote was undocumented. An unmatched single quote is now
      rejected, causing the parse to fail, and this is documented.

* 8990013efcb Network: let a lone "*" in no_proxy bypass every host
    * Fixed a bug that caused an environment variable of "no_proxy=*" to
      be ignored.

* 4902cb2a841 QString/QByteArray: fix UB (signed overflow) in repeated()
    * Fixed an integer overflow that could have caused out-of-bounds
      access on the result object.

* 82da437d75d QCborValue: default-construct the value for extended types
  by enum
    * Fixed a bug that caused QCborValue variables constructed with just
      a Type of Tag, DateTime, RegularExpression, Url, or Uuid to be in
      an invalid state. This did not affect constructing QCborValue
      using the dedicated constructors for the respective Qt types.

* 20bf6a0d09d Upgrade PCRE2 to 10.49
    * PCRE2 was updated to version 10.49.

* 3d22ffe6b02 QStringConverter/ICU: fix buffer overflow encoding empty
  strings
    * Fixed a crash when encoding an empty string with ICU stateful
      codecs such as ISO-2022-KR.

* c8e56913ff4 Update md4c to 0.6.0
    * Updated md4c to version 0.6.0.

* 331e246039e Read attribution files for vcpkg-provided system libraries
    * Third-party libraries provided by vcpkg now carry license and
      provenance information in Qt's SBOM, read from attribution files
      generated in the vcpkg install prefix.

* 9bcbed5743a Android: stop mapping shared storage on API 30 and above
    * QDesktopServices::openUrl() no longer shares files from outside
      the application's own directories on Android 11 and later. An
      application that needs to share from elsewhere can declare its own
      FileProvider, which Qt uses in preference to its own.

* 9b25108f4c4 Android: let the back key cancel native message dialogs
    * Make a native message box cancellable if it has an escape button.

* 3942d1be955 Update bundled libpng to version 1.6.59
    * libpng was updated to version 1.6.59

* dc2250fe125 QFuture: don't keep a link to a finished parent in
  setContinuation()
    * Fixed a crash when cancelChain() was called on a continuation that
      had been attached to an already-finished future.

* d36bee0bdd3 QAuthenticator: pass the SPN to SSPI for NTLM as well
    * On Windows, NTLM authentication now sends the target SPN (the
      "spn" option, or HTTP/<host>) to SSPI, as Negotiate already did.

* 6d60e928fbe QMetaType/QVariant: don't round FP when converting to bool
    * Fixed a bug that would cause conversion of certain small but non-
      zero floating point numbers to result in a false value when
      converted to bool (that is, using .toBool() or .value<bool>(), or
      QMetaType::convert()).

* 159ef553aae QStringDecoder: count ICU-pending input when finalizing
  without output
    * Fixed a bug that would cause finalize() to ignore incomplete input
      from ICU-based codecs.

* 00cfd41a841 SQLite: Update SQLite to v3.54.0
    * Updated SQLite to v3.54.0

* f27b903ab18 QString/QByteArrayView: disable __builtin_constant_p for
  GCC < 17
    * Worked around a GCC bug where code could crash or misbehave when
      calling QByteArrayView search functions (indexOf(), count(),
      startsWith(), etc.) with a string of length 1.
    * Worked around a GCC bug where code could crash or misbehave when
      calling QStringView search functions (indexOf(), count(),
      startsWith(), etc.) with a string of length 1.

* 1cd9095eaa8 QLocale::uiLanguages(): Use lang and script for
  equivalents for fallback
    * Truncated fallback locales are added immediately after the last
      entry in the OS list of preferred locales with the same (likely-
      implied) language and script, rather than at the end of the list.
      Previously this did not occur when the OS list contained multiple
      entries for the same language and script which did not include the
      most likely region. For example, an OS preferred list of "en-
      AU:en-GB:de-DE" will now result in prefering US English to German.

* 2da0bee6a52 Refine benchmark significant digit formatting
    * Benchmark results now use a modified version of the 'e' format,
      where the exponent is omitted if zero and only multiples of three
      are used as exponents. Where a standard deviation is given, it
      uses the same exponent as the mean to which it relates. This shold
      make results easier to read and to relate to one another.

* d5b16405339 QStringDecoder: flush ICU converters in finalize()
    * Fixed a bug that caused finalize() to lose the final character
      when decoding with some stateful ICU codecs, such as ISCII.

* 5a2979ed024 Fix formatting of 128-bit integers in quint128toBasicLatin
    * Fixed INT128 values whose lower 19 digits start with a zero being
      read back with a missing digit.

* 40741556d22 moc: fix crash on stringizing an empty macro argument
  adjacent to a string literal
    * Fixed a crash when stringifying empty macro arguments in certain
      situations.

* 8cf838b26a3 Remove IILE in Q_PRESUME: back to statement
    * The Q_PRESUME() macro was changed from an immediately-invoked
      lambda expression to a do{}while statement. This was necessary
      because GCC does not apply the assumption back to the outer scope
      in all cases. Code that was using this macro as an expression will
      need to be adapted.

* 1ce52bf2c77 SQLite: Update SQLite to v3.54.1
    * Updated SQLite to v3.54.1

* af8d6ddf8b2 Upgrade Harfbuzz to 14.6.0
    * Upgraded Harfbuzz to version 14.6.0

* 194c55e386e QPainterPath: validate paths read from a QDataStream
    * The QDataStream operator>> now rejects structurally invalid paths
      and sets the stream status to ReadCorruptData.

* f976525a814 Update Freetype to 2.15.0
    * Updated bundled Freetype to 2.15.0.

* 4f3e5d68ac3 ohos: support sub window maximization on API 26
    * Sub windows that have Qt::WindowMaximizeButtonHint can now be
      maximized in freeform window mode.

* 1f02b348caa QByteArray: fix UB (signed overflow) in toHex()
    * Fixed an integer overflow in toHex() that could lead to a buffer
      overflow.

* 69364c7e9b0 QByteArray: fix UB (signed overflow) in toBase64()
    * Fixed an integer overflow in toBase64() that could lead to a
      buffer overflow.

* 0cefc50359f QByteArray: fix UB (signed overflow) in
  toPercentEncoding()
    * Fixed an integer overflow in toPercentEncoding() that could lead
      to a buffer overflow.

* bc662b56b33 QString: fix %{j,t,z}n to write full width
    * Fixed partial writes on %jn, %zn and %tn.

* f200e69bc71 QDataStream: distinguish a truncated read from an empty
  QByteArray/QString
    * Reading a QByteArray or QString from a truncated stream now leaves
      the value null (isNull() returns true), instead of producing an
      empty but non-null value, so a truncated read can be told apart
      from a genuinely empty one without inspecting status().
      Distinguishing from a null QByteArray or QString still requires
      inspecting status().

* a50ed6d8624 Update bundled libjpeg-turbo to version 3.2.1
    * libjpeg-turbo was updated to version 3.2.1

* c99306c8ef0 harmonydeployqt: Support HAP signing with plain passwords
    * Added the --signing-plain-key-password and --signing-plain-store-
      password options to sign the HAP with plain text passwords. This
      does not require DevEco Studio.

* 6a7bd4e1e30 3rdparty: Update TinyCBOR from upstream to 7.1
    * TinyCBOR was updated to version 7.1.

* 9fc0dfe6f6d Update zlib to 1.4
    * zlib was updated to version 1.4.

* dc5d7cb3127 Upgrade Harfbuzz to 15.1.0
    * Upgraded Harfbuzz to version 15.1.0

### qtdeclarative
* 1671f484d5 Flickable: keep using pixelDelta on touchpads with rounded
  deltas
    * Flickable no longer starts a wheel flick in the middle of a
      touchpad gesture when individual updates report a pixelDelta that
      rounded down to (0, 0).

* bcbfae6761 QQuickTextInput: don't call QMimeData::text() for canPaste
    * canPaste now reflects whether the clipboard advertises a text
      format without calling QMimeData::text() to inspect the payload. A
      provider that advertises text but returns an empty payload is
      therefore considered pasteable.

* fcaf926941 ScrollBar: don't jump the content when the content size is
  re-estimated
    * Dragging the handle of a ScrollBar that is attached to a view
      whose delegates vary in size no longer makes the content jump as
      the view refines its content size estimate.

* 60bdcd0ab5 Show dialogs even if QQuickWindow is not toplevel
    * Fix opening dialogs when embedded using createWindowContainer

* 0c23cce932 TreeModel: Reject rows that are nested too deeply to be
  converted
    * Deeply nested rows no longer exhaust the stack. Rows nested too
      deeply to be converted from JavaScript are rejected with a
      warning.

* d3b321d0c0 Controls: expand Material windows by default on Android
    * ApplicationWindow now uses expanded client areas by default on
      Android. Set flags to Qt.Window to keep the window inside the
      system bars.

* 8b95325289 Add public API to create a QML preview target for
  executables
    * Executable targets linking against Qt6::Qml now get a
      module_qmlpreview target by default. This can be changed by
      setting QT_QML_NO_QML_PREVIEW.
    * Added the qt6_add_qml_preview for manually adding qmlpreview
      targets for executable targets.

### qtmultimedia
* 5857ec310 dr_libs: update dr_wav to upstream snapshot 019e75ba
    * Updated dr_wav to 0.14.6-snapshot-019e75ba.

* 779bdf1e0 ffmpeg: update docs for 9.0.2
    * FFmpeg: update to v9.0.2

* cbbd53252 dr_libs: update dr_wav to upstream release 0.14.6
    * Updated dr_wav to 0.14.6.

### qttools
* f946ca162 QDoc: Keep case-distinct member links valid
    * Links to members with names differing only in case resolve to the
      correct documentation anchor.

* e4ce30fbd QDoc: Keep legacy HTML fragment IDs distinct
    * HTML pages now use distinct fragment IDs for colliding headings,
      targets, and members.

* cb0d0b3c0 QDoc: Add source locations to reports
    * Reports include source locations when available. Identical reports
      from different source locations appear separately.

* 69a2ac546 QDoc: Warn about missing documentation for signals and slots
    * QDoc now warns about missing documentation for C++ signals and
      slots.

* cbede258b QDoc: Document functions declared with C linkage
    * QDoc now generates documentation for functions declared with
      extern "C".

* 6f58b6c8b QDoc: Resolve QML method links with signatures
    * QML method links support dotted syntax with parameter types for
      overload selection. Invalid signatures produce warnings instead of
      silently selecting an overload.

* c48591fa2 QtHelp: Make read-only mode prevent writes to the collection
  file
    * In read-only mode, QHelpEngineCore now opens the collection file
      read-only, and functions that would modify it fail and return
      false. The active filter is no longer saved in that mode.

### qtconnectivity
* dfbb8d09 NDEF: Do not accept unexpected Unchanged type name field
    * Fixed a bug when QNdefMessage::fromByteArray() incorrectly
      accepted a stray record chunk of a chunked payload (TNF=0x06) when
      the initial record chunk has not been seen yet. Such message is
      now discarded as malformed.

### qtserialbus
* 053cc6e9 CAN: Vector: Preserve the ESI flag on received frames
    * Received CAN FD frames now expose the error state indicator
      reported by the driver.

* aa978991 CAN: Vector: Preserve the FD flag on short frames
    * Received short CAN FD frames without bitrate switching now retain
      their CAN FD flag.

* eccd79f1 CAN: Clamp vendor CAN receive payload lengths
    * Received classic CAN payloads are limited to 8 bytes, including on
      CAN FD-enabled channels.

* 635e4159 CAN: Fix canbusutil receive flag display
    * The --info option now displays the bitrate switch, error state
      indicator, and local echo flags correctly.

### qtwebsockets
* c2725d4 QWebSocket: fix off-by-one header size limit
    * A handshake header whose size is exactly the limit (100 lines of 8
      KiB plus the terminator) is now refused rather than accepted.

* 406276a QWebSocket: fix quadratic copy and scan during pre-handshake
    * An over-sized handshake response now closes the connection, and
      QWebSocket::closeCode() reports
      QWebSocketProtocol::CloseCodeTooMuchData. The size limit is also
      now applied as the response arrives, rather than only while the
      end of the headers has not been seen.

* bf5c401 QWebSocketServer: Fix quadratic copy and scan during pre-
  handshake
    * The handshake header size limit is now applied as the request
      arrives, rather than only while the end of the headers has not
      been seen. An over-sized request now fails with
      QWebSocketProtocol::CloseCodeTooMuchData and "Header is too
      large." instead of CloseCodeProtocolError and "Invalid handshake
      request."

### qt5compat
* 8936dce Enable exceptions in Qt5CoreCompat
    * Is now built with exceptions enabled. Before, exceptions (e.g.
      thrown from QtCore) could still travel through the module's code,
      but would not run the module's cleanup, leaking resources such as
      memory and mutex locks.

* a5cb88f QXmlSimpleReader: fix unbounded recursion when parsing nested
  elements
    * Fixed a stack overflow when parsing documents with very deeply
      nested elements.

* e995c82 QXmlSimpleReader: add a property to control entity expansion
  limit
    * The entity expansion limit of 4096 characters is now applied more
      strictly, which can lead to some previously valid documents to be
      considered malformed. Use setProperty() with a new property
      "http://qt-project.org/xml/properties/entity-expansion-limit" to
      adjust the limit.

### qthttpserver
* 2397a20 Reject invalid or out-of-range Content-Length
    * A request with a malformed Content-Length (non-numeric, negative,
      or too large to represent) is now rejected with 400 (Bad Request)
      over HTTP/1.Previously such a value was ignored and the request
      processed as if it had no body.

* d302ddc Parse Transfer-Encoding as a coding list instead of a
  substring
    * Transfer-Encoding is now parsed as a list of transfer-codings
      rather than matched as a substring. Requests are rejected when the
      header contains a coding other than "chunked" (including
      "identity") with 501 Not Implemented, or when "chunked" is
      combined with another coding or appears more than once with 400
      Bad Request. Previously such requests were accepted.

### qtgrpc
* 1b7265c2 tests: Update the vendored protobuf conformance protos to
  33.4
    * The vendored protobuf conformance test protos were updated to
      protobuf 33.4.

* 1f54a6e4 Fix optional field check to exclude required fields in proto2
    * proto2 required fields are now always written to the wire. A
      required field holding its type's default value used to be
      omitted, producing a message that conformant parsers reject as
      missing that field.
    * Generated proto2 required fields no longer provide hasX() and
      clearX() and are no longer stored as std::optional. A required
      field is always present, so the presence API never applied to it.

* eadcf62c qtprotobufgen: Omit proto2 group fields instead of emitting
  broken code
    * A .proto containing proto2 groups now generates compilable code.
      Group fields are skipped with a warning, because Qt Protobuf does
      not implement the group wire format. Such a field previously
      produced a property with an empty type name, which moc rejected.

* de58c4b2 qtprotobufgen: Escape json_name in the generated field
  metadata
    * A json_name containing quotes, backslashes, newlines, comment
      delimiters or a leading digit now generates correct code. Such
      names previously broke the generated source or produced wrong JSON
      keys.

* 2fea64c9 qtprotobufgen: Keep copied .proto comments inside the
  generated comment
    * With COPY_COMMENTS, a .proto comment containing "*/", "/*" or "$"
      is now copied verbatim into the generated comment. Such comments
      previously ended the generated comment early or lost text.

* 4bf01591 QProtobufSerializer: add message size limits
    * serialize() now fails for messages of 2 GiB or larger.
      deserialize() rejects input of 2 GiB or larger. The environment
      variable QT_PROTOBUF_MAXIMUM_INPUT_SIZE can lower the
      deserialization limit. It is read only once per process, so
      changing it later has no effect.

* c52b5588 QGrpcOperation: fail the RPC when a request message can't be
  serialized
    * An RPC now finishes with an Internal status when a request message
      fails to serialize, instead of sending an empty message.

### qtgraphs
* afe22bf4 2D: Fix QLogValueAxis accepting invalid values
    * QLogValueAxis::setMin rejects 0.0 but the default value was 0.0.
      Now the default is 1.

* a2fb47bf 2D: Optimize piemodelmapper
    * The QPieModelMapper doesn't reinitialize the model every time
      something changes.

* 037cc750 2D: Optimize barmodelmapper
    * The QBarModelMapper doesn't reinitialize the model every time
      something changes.

### qtopenapi
* d1ab2a6 Operation credentials should not be global
    * Fixed a bug when operation credentials associated with a specific
      operation were applied globally and shared with other operations.
      Credentials are now applied individually for each operation.


Fixes
-----

### qtbase
* [QTBUG-149950](https://qt-project.atlassian.net/browse/QTBUG-149950) tst_QWidget::renderRTL() is flaky on macOS
* [QTBUG-150039](https://qt-project.atlassian.net/browse/QTBUG-150039) Incorrect Vulkan usage: VUID-VkImageCreateInfo-
initialLayout-12478
* [QTBUG-149985](https://qt-project.atlassian.net/browse/QTBUG-149985) macOS: crash when mixing offscreen & swapchain if
setSamples(1)
* [QTBUG-149606](https://qt-project.atlassian.net/browse/QTBUG-149606) Android asset file engine handler does not handle ./ in
paths
* [QTBUG-149947](https://qt-project.atlassian.net/browse/QTBUG-149947) UB in QDesktopUnixServices::openUrl when dbus disabled
* [QTBUG-147629](https://qt-project.atlassian.net/browse/QTBUG-147629) REG->6.12 B/Linux/Wayland: Crash in
QDesktopServices::openUrl()
* [QTBUG-150208](https://qt-project.atlassian.net/browse/QTBUG-150208) High memory usage during plugin load
* [QTBUG-150211](https://qt-project.atlassian.net/browse/QTBUG-150211) Targeted D-Bus signals always start well-known services
even when autoStartService is disabled
* [QTBUG-149626](https://qt-project.atlassian.net/browse/QTBUG-149626) [QT5&QT6][WPS]:No “forbidden” drop indicator on OHOS
when the drop target rejects the drag
* [QTBUG-147607](https://qt-project.atlassian.net/browse/QTBUG-147607) QSpinBox/QDoubleSpinBox: wrong orizontal size in Windows
11
* [QTBUG-150187](https://qt-project.atlassian.net/browse/QTBUG-150187) Don't create a QByteArray in
QXmlStreamReader::addData(QASV) before we didn't know we need one
(SERBUG-16 cont'd)
* [QTBUG-149997](https://qt-project.atlassian.net/browse/QTBUG-149997) QtCore / serialization: addData() multiplies a size by
two unchecked (SERBUG-16)
* [QTBUG-149104](https://qt-project.atlassian.net/browse/QTBUG-149104) [VxWorks] CI test runner misclassifies a running RTP as
FINISHED and aborts it — tst_qcomplextext permanently fails on
qemu_armv7 (bidiTest)
* [QTBUG-150214](https://qt-project.atlassian.net/browse/QTBUG-150214) SBOM: ATTRIBUTION_ENTRY_INDEX appears to act as a start
offset, so all following attribution entries are recorded against the
target
* [QTBUG-148575](https://qt-project.atlassian.net/browse/QTBUG-148575) QCryptographicHash/QMessageAuthenticationCode trigger
OpenSSL bug #32079 (double-free)
* [QTBUG-150298](https://qt-project.atlassian.net/browse/QTBUG-150298) windeployqt does not deploy the third-party libraries
the Qt libraries need
* [QTBUG-150328](https://qt-project.atlassian.net/browse/QTBUG-150328) Undocked QToolBar prevents QMainWindow contents from
responding to resize
* [QTBUG-150040](https://qt-project.atlassian.net/browse/QTBUG-150040) Ubuntu 26.04 x64: tst_qioring fails in qtbase
* [QTBUG-146830](https://qt-project.atlassian.net/browse/QTBUG-146830) [REG 6.10.3 -> 6.11.1] Android system bars disappear
* [QTBUG-148337](https://qt-project.atlassian.net/browse/QTBUG-148337) Top-level window content is offset by the status-bar
height with Qt 6.10.3 despite identical, correctly-reported WindowInsets
values, compared to Qt 6.8.3 on the same device
* [QTBUG-149521](https://qt-project.atlassian.net/browse/QTBUG-149521) Apps built with targetSdk<35 won't fill cutouts on A15+
device
* [QTBUG-149619](https://qt-project.atlassian.net/browse/QTBUG-149619) [REG 5.15 -> 6.11] Raster paint engine has a ~10x
performance cliff at 96 pixels for translucent cosmetic lines
* [QTBUG-150343](https://qt-project.atlassian.net/browse/QTBUG-150343) QtCore / text: QString::assign_helper(char32_t*)
multiplication overflow-that-isn't (TXTBUG-03e)
* [QTBUG-149290](https://qt-project.atlassian.net/browse/QTBUG-149290) [REG 6.11.1->6.11.2] macOS: Ugly borders around
QLineEdit/QSpinBox in dark mode
* [QTBUG-150480](https://qt-project.atlassian.net/browse/QTBUG-150480) Q(Plain)TextEdit provides inaccurate values for
ImCursorRectangle / ImAnchorRectangle
* [QTBUG-67490](https://qt-project.atlassian.net/browse/QTBUG-67490) QCollatorSortKey doesn't work on macOS
* [QTBUG-150259](https://qt-project.atlassian.net/browse/QTBUG-150259) macOS: QCollatorSortKey comparisons involving empty
strings violate strict weak ordering.
* [QTBUG-88704](https://qt-project.atlassian.net/browse/QTBUG-88704) QCollatorSortKey is not working properly without ICU
support
* [QTBUG-150366](https://qt-project.atlassian.net/browse/QTBUG-150366) QtCore / text: QString::toStdString() integer overflow
(TXTBUG-03h)
* [QTBUG-150216](https://qt-project.atlassian.net/browse/QTBUG-150216) QtCore / serialization: XML reader carries entity state
across clear(): entityReferenceStack (SERBUG-03a)
* [QTBUG-149980](https://qt-project.atlassian.net/browse/QTBUG-149980) QtCore / serialization: XML reader carries entity state
across clear(): entityHash (SERBUG-03c)
* [QTBUG-150580](https://qt-project.atlassian.net/browse/QTBUG-150580) QString::insert(n, QL1SV l1s) OOB read for empty, non-
null l1s
* [QTBUG-150579](https://qt-project.atlassian.net/browse/QTBUG-150579) QString::insert(0, "\0"_L1) doesn't insert anything
* [QTBUG-149231](https://qt-project.atlassian.net/browse/QTBUG-149231) QDBus: process aborts when cross-marshalling a message
with a stale unix file descriptor
* [QTBUG-150377](https://qt-project.atlassian.net/browse/QTBUG-150377) Android a11y: Changes to "Accessible.name" are announced
with unnecessary verbosity
* [QTBUG-109643](https://qt-project.atlassian.net/browse/QTBUG-109643) Windows Display Scale >100% negates
QTextCursor::setCursorWidth(0)
* [QTBUG-150262](https://qt-project.atlassian.net/browse/QTBUG-150262) QtCore / serialization: XML reader carries entity state
across clear(): parameterEntityHash (SERBUG-03d)
* [QTBUG-150017](https://qt-project.atlassian.net/browse/QTBUG-150017) [macOS 27] Item-view check-state indicators are
invisible with macos style
* [QTBUG-127506](https://qt-project.atlassian.net/browse/QTBUG-127506) tst_QWidget::render_windowOpacity() failed on Ubuntu
24.04(arm64) GNOME Wayland
* [QTBUG-128185](https://qt-project.atlassian.net/browse/QTBUG-128185) Fix tst_QWidget::render_windowOpacity() failed on Ubuntu
24.04(arm64) GNOME Wayland
* [QTBUG-128371](https://qt-project.atlassian.net/browse/QTBUG-128371) Windows ARM: Fix blacklisted
tst_qwidget::render_windowOpacity()
* [QTBUG-144911](https://qt-project.atlassian.net/browse/QTBUG-144911) Android: Crash/Assertion when TalkBack screen reader
turned on while Qt app in foreground
* [QTBUG-150776](https://qt-project.atlassian.net/browse/QTBUG-150776) QtDBus: registerComplexDBusType() leaks a
QDBusRawTypeHandler for every distinct unrecognized D-Bus type signature
* [QTBUG-100251](https://qt-project.atlassian.net/browse/QTBUG-100251) Modifiers are not specified for mouse and touch events
* [QTBUG-150755](https://qt-project.atlassian.net/browse/QTBUG-150755) QHttp2Connection: delete-during iteration / re-entrant-
signal use-after-free
* [QTBUG-107731](https://qt-project.atlassian.net/browse/QTBUG-107731) markdown writer: formatted spans mess up table
formatting
* [QTBUG-150372](https://qt-project.atlassian.net/browse/QTBUG-150372) Windows: Qt tools linked with lld-link ≤ 20 fail to
start ("side-by-side configuration is incorrect") since QTBUG-147634
* [QTBUG-150556](https://qt-project.atlassian.net/browse/QTBUG-150556) Application crashes when AnimatedImage finishes the
first loop of a remote GIF with caching disabled
* [QTBUG-150279](https://qt-project.atlassian.net/browse/QTBUG-150279) Wayland: QRhiWidget deadlocks on window destruction if
driver returns VK_ERROR_OUT_OF_DATE_KHR
* [QTBUG-150340](https://qt-project.atlassian.net/browse/QTBUG-150340) QtCore / text: QByteArray/QString::repeated()
multiplication overflow (TXTBUG-03c)
* [QTBUG-149398](https://qt-project.atlassian.net/browse/QTBUG-149398) QCborValue(Type) does not equal explicitly default-
constructed objects
* [QTBUG-149393](https://qt-project.atlassian.net/browse/QTBUG-149393) WASM: QWasmInputContext ignores the "deleteContent"
inputType, breaking backspace on WebKit-embedded virtual keyboards
* [QTBUG-149339](https://qt-project.atlassian.net/browse/QTBUG-149339) QOCI: bindValue() binds a QString's buffer by raw
pointer without keeping it alive until the deferred OCIStmtExecute()
read — use-after-free causes intermittent ORA-01480
* [QTBUG-150286](https://qt-project.atlassian.net/browse/QTBUG-150286) QPlainTextEdit memory usage increases sharply after
laying out blocks in Qt 6.11.2
* [QTBUG-150583](https://qt-project.atlassian.net/browse/QTBUG-150583) QStringEncoder::encode() writes out of bounds and
crashes when encoding an empty string with ISO-2022-KR
* [QTBUG-103375](https://qt-project.atlassian.net/browse/QTBUG-103375) [REG:5.15->6] Shift_JIS support for QDomDocument on Qt6
* [QTBUG-150353](https://qt-project.atlassian.net/browse/QTBUG-150353) Qt Wayland EventThread shutdown can leave a prepared
read and deadlock QWaylandDisplay destruction
* [QTBUG-150636](https://qt-project.atlassian.net/browse/QTBUG-150636) qtbase build failure with md4c 0.6.0
* [QTBUG-151090](https://qt-project.atlassian.net/browse/QTBUG-151090) Print preview replays the first page without the
painter's starting state
* [QTBUG-150746](https://qt-project.atlassian.net/browse/QTBUG-150746) QtXml:  Dead code in the builder and parser: foundDtd in
parseProlog() (XMLBUG-13d)
* [QTBUG-149286](https://qt-project.atlassian.net/browse/QTBUG-149286) Qt Concurrent: map/filter/reduce APIs crash on a null
QThreadPool* instead of reporting a canceled QFuture
* [QTBUG-150359](https://qt-project.atlassian.net/browse/QTBUG-150359) markdown writer: a line should not end with a monospace-
span opening backtick
* [QTBUG-99681](https://qt-project.atlassian.net/browse/QTBUG-99681) QTextEdit: multi-line monospace text is not written to
proper markdown
* [QTBUG-111707](https://qt-project.atlassian.net/browse/QTBUG-111707) markdown writer needs to add more newlines after (some)
list items
* [QTBUG-150914](https://qt-project.atlassian.net/browse/QTBUG-150914) syncqt-generated version headers do not use actual
module version
* [QTBUG-150915](https://qt-project.atlassian.net/browse/QTBUG-150915) syncqt generates faulty integer version numbers in
module version headers
* [QTBUG-150656](https://qt-project.atlassian.net/browse/QTBUG-150656) QtXml:  Dead code in the builder and parser: tagStack
(XMLBUG-13a)
* [QTBUG-151000](https://qt-project.atlassian.net/browse/QTBUG-151000) Qt Test: catch2 attribution entry does not declare
QtParts
* [QTBUG-149821](https://qt-project.atlassian.net/browse/QTBUG-149821) Platform theme builds palettes from a default-
constructed QPalette, so unset colour roles paint black
* [QTBUG-150982](https://qt-project.atlassian.net/browse/QTBUG-150982) [Regression 6.10 -> 6.11] QRhi OpenGL: recording a pass
is quadratic in the number of buffers it uses
* [QTBUG-150673](https://qt-project.atlassian.net/browse/QTBUG-150673) QtXml:  Dead code in the builder and parser:
start/endEntity (XMLBUG-13b)
* [QTBUG-150691](https://qt-project.atlassian.net/browse/QTBUG-150691) HarmonyOS: OHOS branch in QtMkspecHelpers is unreachable
because LINUX is set
* [QTBUG-120498](https://qt-project.atlassian.net/browse/QTBUG-120498) QOpenGLWidget as QGraphicsView viewport crashes Qt on
Android
* [QTBUG-151012](https://qt-project.atlassian.net/browse/QTBUG-151012) QTimeZonePrivate::isValidId() accepts .. and ... as
zone-id path components
* [QTBUG-150999](https://qt-project.atlassian.net/browse/QTBUG-150999) FreeType: set SecurityCritical on freetype-bdf,
freetype-pcf and freetype-zlib
* [QTBUG-151163](https://qt-project.atlassian.net/browse/QTBUG-151163) Wayland protocol abort due to input method error
* [QTBUG-150886](https://qt-project.atlassian.net/browse/QTBUG-150886) wasm: first paint only commits after a resize
* [QTBUG-151154](https://qt-project.atlassian.net/browse/QTBUG-151154) Grabbing broken for Graphics View with OpenGL viewport
* [QTBUG-151272](https://qt-project.atlassian.net/browse/QTBUG-151272) QFuture::cancelChain() crashes when then() was attached
to an already finished future
* [QTBUG-148551](https://qt-project.atlassian.net/browse/QTBUG-148551) QFuture::unwrap() aborts with "futureData already has a
parent" on an already-finished future
* [QTBUG-150206](https://qt-project.atlassian.net/browse/QTBUG-150206) forcing 10 successful runs for modified / new functions
can hit the ctest timeout
* [QTBUG-148522](https://qt-project.atlassian.net/browse/QTBUG-148522) QTabBar icons rendered blurry at fractional device pixel
ratio (e.g. 125%) — regression from QIcon::paint() change in
CE_TabBarTabLabel
* [QTBUG-151036](https://qt-project.atlassian.net/browse/QTBUG-151036) QSocks5SocketEngine stops delivering buffered data when
the socket's read buffer is limited, stalling transfers through a SOCKS5
proxy
* [QTBUG-95791](https://qt-project.atlassian.net/browse/QTBUG-95791) find_package(Qt6LinguistTools) fails due to undefined
__qt_internal_promote_target_to_global
* [QTBUG-150675](https://qt-project.atlassian.net/browse/QTBUG-150675) QtXml:  Dead code in the builder and parser: internal
entities in save() (XMLBUG-13c)
* [QTBUG-150655](https://qt-project.atlassian.net/browse/QTBUG-150655) QtXml: Entity values round-trip through a Latin-1
conversion (XMLBUG-12)
* [QTBUG-146796](https://qt-project.atlassian.net/browse/QTBUG-146796) QCoreApplication::compressEvent() generates deprecation
warnings when compiling Qt
* [QTBUG-149000](https://qt-project.atlassian.net/browse/QTBUG-149000) QVariant(0.1).toBool() == false, but should be true
* [QTBUG-151043](https://qt-project.atlassian.net/browse/QTBUG-151043) Calling winId on a dockwidget while docked breaks
colorscheme integration on Windows
* [QTBUG-149525](https://qt-project.atlassian.net/browse/QTBUG-149525) QFileInfo::canonicalPath() returns "." instead of an
empty string
* [QTBUG-150715](https://qt-project.atlassian.net/browse/QTBUG-150715) [Qt 6.8] SIGSEGV in QCoreApplication::notifyInternal2()
during shutdown when ~QCoreApplication() races with QThread dispatching
posted events
* [QTBUG-67507](https://qt-project.atlassian.net/browse/QTBUG-67507) The polygon draw is very slow when partly clipped and
line width > 1
* [QTBUG-151308](https://qt-project.atlassian.net/browse/QTBUG-151308) [REG 6.11.2 -> 6.12.0] QSpinBox content has wrong
alignment when it's styled via stylesheet
* [QTBUG-148646](https://qt-project.atlassian.net/browse/QTBUG-148646) QSpinBox up button does not respond when border is set
via stylesheet
* [QTBUG-151199](https://qt-project.atlassian.net/browse/QTBUG-151199) ODBC driver with PostgreSQL datasource generates syntax
errors for named placeholders
* [QTBUG-96636](https://qt-project.atlassian.net/browse/QTBUG-96636) Some Postgresql jsonb operators mistaken for prepared
statement placeholders.
* [QTBUG-151350](https://qt-project.atlassian.net/browse/QTBUG-151350) Android: Crash (Nullpointer-Exception) with Talkback
enabled
* [QTBUG-151306](https://qt-project.atlassian.net/browse/QTBUG-151306) QKeySequence::toString() truncates to negative sizes
* [QTBUG-150569](https://qt-project.atlassian.net/browse/QTBUG-150569) size < 0 ⇒ size == 0 is a security nightmare
* [QTBUG-151369](https://qt-project.atlassian.net/browse/QTBUG-151369) Doc: QStandardPaths docs say Documents and GenericData
paths are never empty, but they can be on Android 11+
* [QTBUG-151361](https://qt-project.atlassian.net/browse/QTBUG-151361) Docs still claim zero-interval timers fire after window
system events
* [QTBUG-47115](https://qt-project.atlassian.net/browse/QTBUG-47115) QTimer::singleShot inconsistency
* [QTBUG-44914](https://qt-project.atlassian.net/browse/QTBUG-44914) Setting link color from QGuiApplication works, contrary
to what docs state
* [QTBUG-52465](https://qt-project.atlassian.net/browse/QTBUG-52465) Document that QAbstractItemView::selectionModel is null
after creation
* [QTBUG-40752](https://qt-project.atlassian.net/browse/QTBUG-40752) QTcpServer::incomingConnection() documentation ambigious
* [QTBUG-44193](https://qt-project.atlassian.net/browse/QTBUG-44193) QUrl::fromLocalFile documentation is vague.
* [QTBUG-45203](https://qt-project.atlassian.net/browse/QTBUG-45203) AllDockWidgetAreas is not valid Dock Area for Dock Widget
* [QTBUG-151370](https://qt-project.atlassian.net/browse/QTBUG-151370) Doc: Describe the Qt::ToolBarArea enum and its values
* [QTBUG-151162](https://qt-project.atlassian.net/browse/QTBUG-151162) Extra semicolon warnings in qicon.h, qrangemodel.h,
qrangemodel_impl.h, and qrangemodeladapter.h
* [QTBUG-151282](https://qt-project.atlassian.net/browse/QTBUG-151282) tst_applicationmanager_multi-process (Failed)
* [QTBUG-150998](https://qt-project.atlassian.net/browse/QTBUG-150998) XSVG: set SecurityCritical
* [QTBUG-141436](https://qt-project.atlassian.net/browse/QTBUG-141436) delayed touch events aren't processed correctly
* [QTBUG-148523](https://qt-project.atlassian.net/browse/QTBUG-148523) QIcon::pixmap() returns different results for identical
calls on an addFile() icon — engine mutates a cached entry's
devicePixelRatio
* [QTBUG-147167](https://qt-project.atlassian.net/browse/QTBUG-147167)  QMenu items unresponsive in fullscreen when overlapping
hidden menu bar area
* [QTBUG-123298](https://qt-project.atlassian.net/browse/QTBUG-123298) Qt 6.5 on MacOS - In full screen, topmost QMenu action
doesn't fire
* [QTBUG-41820](https://qt-project.atlassian.net/browse/QTBUG-41820) Unclear, why QAbstractItemView::selectedIndexes() is
protected
* [QTBUG-151050](https://qt-project.atlassian.net/browse/QTBUG-151050) Crash in QArrayData::deallocate() only in release builds
* [QTBUG-151379](https://qt-project.atlassian.net/browse/QTBUG-151379) [Regression 6.8.9->6.12.0] uic checks class name and
does not allow chevrons
* [QTBUG-151338](https://qt-project.atlassian.net/browse/QTBUG-151338) QColorSpace ignores the cicp tag of ICC profiles with a
Lab PCS
* [QTBUG-148288](https://qt-project.atlassian.net/browse/QTBUG-148288) With a OS preferred locale list of two (non-US) English
variants followed by a second language, the expanded list in
QLocale::uiLanguages() prefers the second language before "en"
* [QTBUG-45475](https://qt-project.atlassian.net/browse/QTBUG-45475) QImage::copy doesn't always result in an QImage of the
specified size
* [QTBUG-145766](https://qt-project.atlassian.net/browse/QTBUG-145766) [REG 6.11.0 -> 6.12.0] Benchmark times in scientific
notation
* [QTBUG-50321](https://qt-project.atlassian.net/browse/QTBUG-50321) Incorrect QWidget documentation for
mouseDoubleClickEvent()
* [QTBUG-149515](https://qt-project.atlassian.net/browse/QTBUG-149515) macOS: QWidget::restoreGeometry() shrinks a window by
2px per axis when the saved size equals availableGeometry()
* [QTBUG-108346](https://qt-project.atlassian.net/browse/QTBUG-108346) tst_qquicktextedit::pasteHtmlIntoMarkdown is flaky on
Ubuntu 20.04
* [QTBUG-120515](https://qt-project.atlassian.net/browse/QTBUG-120515) QT_* paths unconditionnally set to defaults when qt.conf
is present
* [QTBUG-144738](https://qt-project.atlassian.net/browse/QTBUG-144738) QRhiGles2: Failed to make context current. Expect bad
things to happen
* [QTBUG-142195](https://qt-project.atlassian.net/browse/QTBUG-142195) Android lock task mode app stops on short power button
* [QTBUG-139606](https://qt-project.atlassian.net/browse/QTBUG-139606) [REG 6.9.1 -> 6.9.2] App window blank when switching
from background to foreground
* [QTBUG-130678](https://qt-project.atlassian.net/browse/QTBUG-130678) Android app crashes when activity enter 'Pause'
* [QTBUG-128676](https://qt-project.atlassian.net/browse/QTBUG-128676) QInputDialog::getItem makes app not responsible and
might generate an error with the EGL lib: EGL_BAD_MATCH
* [QTBUG-139006](https://qt-project.atlassian.net/browse/QTBUG-139006) QtMainLoopThread crashes on x86_64 android emulator due
to graphics backend initialization fail
* [QTBUG-144727](https://qt-project.atlassian.net/browse/QTBUG-144727) Scene Graph - Vulkan under QML example crashes at close
* [QTBUG-144546](https://qt-project.atlassian.net/browse/QTBUG-144546) [Android] Vulkan under QML example crashes when
unlocking the screen
* [QTBUG-140402](https://qt-project.atlassian.net/browse/QTBUG-140402) Qt Quick application crashes occasionally when put into
inactive in split screen
* [QTBUG-129320](https://qt-project.atlassian.net/browse/QTBUG-129320) openglunderqml and hellogles3 throws errors on Android
* [QTBUG-93363](https://qt-project.atlassian.net/browse/QTBUG-93363) QT + Android + UI becomes unresponsive when switching
apps
* [QTBUG-140490](https://qt-project.atlassian.net/browse/QTBUG-140490) QAndroidPlatformOpenGLWindow::eglSurface() and deadlock
protector crash
* [QTBUG-144207](https://qt-project.atlassian.net/browse/QTBUG-144207) Failed to acquire deadlock protector for
QAndroidPlatformOpenGLWindow::eglSurface()
* [QTBUG-150278](https://qt-project.atlassian.net/browse/QTBUG-150278) Crash when quickly editing text due to
QAndroidInputContext lock
* [QTBUG-119891](https://qt-project.atlassian.net/browse/QTBUG-119891) Android:
tst_QWidget::testWindowIconChangeEventPropagation() gets stuck
* [QTBUG-106384](https://qt-project.atlassian.net/browse/QTBUG-106384) Empty Android app freezes when switching programs
* [QTBUG-129319](https://qt-project.atlassian.net/browse/QTBUG-129319) vulkanunderqml example throws errors
* [QTBUG-94459](https://qt-project.atlassian.net/browse/QTBUG-94459) Android reports incorrect screen size after rotation
* [QTBUG-145846](https://qt-project.atlassian.net/browse/QTBUG-145846) [QTTAS] ANR error appears when running qtquickview
example app on the device
* [QTBUG-139004](https://qt-project.atlassian.net/browse/QTBUG-139004) Android: Qt Application Hangs When Restarted Immediately
After Closure
* [QTBUG-87436](https://qt-project.atlassian.net/browse/QTBUG-87436) tst_QOpenGLWidget fails on Android
* [QTBUG-102043](https://qt-project.atlassian.net/browse/QTBUG-102043) tst_openglwidget has crashing cases
* [QTBUG-50303](https://qt-project.atlassian.net/browse/QTBUG-50303) Documentation for QTextCharFormat::setAnchor unclear
* [QTBUG-50448](https://qt-project.atlassian.net/browse/QTBUG-50448) Document that QGraphicsRectItem::setRect() doesn't change
the position of an item within the scene
* [QTBUG-49996](https://qt-project.atlassian.net/browse/QTBUG-49996) CSS styling QPushButton does not work as documented on
Android
* [QTBUG-151716](https://qt-project.atlassian.net/browse/QTBUG-151716) tst_android::safeAreaWithWindowFlagsAndStates() fails
repeatedly in CI
* [QTBUG-49970](https://qt-project.atlassian.net/browse/QTBUG-49970) Documentation for QObject::disconnect() does not mention
multiple connections
* [QTBUG-151284](https://qt-project.atlassian.net/browse/QTBUG-151284) HarmonyOS: QWidget::move()/resize() on a main window in
non-PC mode leaves the widget geometry out of sync with the window
* [QTBUG-151743](https://qt-project.atlassian.net/browse/QTBUG-151743) [REG 6.11 → 6.12] moc crashes on stringifying an empty
cpp argument
* [QTBUG-150268](https://qt-project.atlassian.net/browse/QTBUG-150268) QtCore / serialization: XML reader carries entity state
across clear(): dtdAttributes (SERBUG-03f)
* [QTBUG-151400](https://qt-project.atlassian.net/browse/QTBUG-151400) QOpenGLWindow and QOpenGLWidget crash on Windows GDI
Driver
* [QTBUG-150344](https://qt-project.atlassian.net/browse/QTBUG-150344) QtCore / text: QtPrivate::convertToUtf8(QL1SV)
multiplication overflow (TXTBUG-03f)
* [QTBUG-141842](https://qt-project.atlassian.net/browse/QTBUG-141842) [macOS] Sporadic crashes on
QCocoaFileDialogHelper::setDirectory()
* [QTBUG-135003](https://qt-project.atlassian.net/browse/QTBUG-135003) FileDialog.currentFolder shows inconsitent behavior on
macOS
* [QTBUG-151178](https://qt-project.atlassian.net/browse/QTBUG-151178) macOS: QCocoaScreen::m_format is uninitialized while the
NSScreen is not yet available, so every QPixmap created then is broken
* [QTBUG-150535](https://qt-project.atlassian.net/browse/QTBUG-150535) xdgdesktopportal: FileDialog reopened as OpenFile after
SaveFile still shows the Save dialog
* [QTBUG-151074](https://qt-project.atlassian.net/browse/QTBUG-151074) Icon of QToolButton uses different foreground color from
its label when using Windows 11 style
* [QTBUG-151681](https://qt-project.atlassian.net/browse/QTBUG-151681) Supported Android API
* [QTBUG-150782](https://qt-project.atlassian.net/browse/QTBUG-150782) QAbstractItemModel::compareData() is not antisymmetric
for mixed-type data — breaks documented "safe for std::sort" contract
AND regresses QSortFilterProxyModel sorting
* [QTBUG-148623](https://qt-project.atlassian.net/browse/QTBUG-148623) [REG 6.10 → 6.11] Windows QPA: window class de-
duplication tests the un-prefixed class name, so a second Qt instance in
one process cannot register its window classes and its windows never
paint
* [QTBUG-84005](https://qt-project.atlassian.net/browse/QTBUG-84005) Windows QPA: RegisterClassEx failed when mixing Qt
versions with identical Qt namespaces
* [QTBUG-101467](https://qt-project.atlassian.net/browse/QTBUG-101467) QTabBar doesn't accept scroll events, resulting in janky
behaviour in scrollview
* [QTBUG-150346](https://qt-project.atlassian.net/browse/QTBUG-150346) macOS: Native child window shows stale/smaller content
during live resize (parent flushes, then swaps, and child copies from
the old back buffer)
* [QTBUG-151008](https://qt-project.atlassian.net/browse/QTBUG-151008) [QPA] vkkhrdisplay reports an empty QScreen::name() and
a generic 100 DPI although it reads the real values from Vulkan
* [QTBUG-150318](https://qt-project.atlassian.net/browse/QTBUG-150318) QtCore / text: toHex separator length overflow on 32-bit
(TXTBUG-03)
* [QTBUG-150341](https://qt-project.atlassian.net/browse/QTBUG-150341) QtCore / text: QByteArray::toBase64() multiplication
overflow (TXTBUG-03d)
* [QTBUG-150327](https://qt-project.atlassian.net/browse/QTBUG-150327) QtCore / text: toPercentEncoding() resize() overflow on
32-bit  (TXTBUG-03b)
* [QTBUG-151091](https://qt-project.atlassian.net/browse/QTBUG-151091) Style sheet: *, *::tab rule overrides more specific type
selectors
* [QTBUG-143746](https://qt-project.atlassian.net/browse/QTBUG-143746) Specificity is lost with too many style rules
* [QTBUG-150354](https://qt-project.atlassian.net/browse/QTBUG-150354) QtCore / text: QString::arg() integer overflow
(TXTBUG-03g)
* [QTBUG-149612](https://qt-project.atlassian.net/browse/QTBUG-149612) macOS: synthesized table elements can delete their
parent accessibility interface
* [QTBUG-151524](https://qt-project.atlassian.net/browse/QTBUG-151524) [QT5&QT6]Subwindow background becomes semi-transparent
after focus switches to the main window
* [QTBUG-151788](https://qt-project.atlassian.net/browse/QTBUG-151788) WebAssembly: copying images fails because the PNG Blob
has an empty MIME type
* [QTBUG-151746](https://qt-project.atlassian.net/browse/QTBUG-151746) [WASM] deleteLater() doesn't delete objects if called
from a JS callback
* [QTBUG-151766](https://qt-project.atlassian.net/browse/QTBUG-151766) [Reg 6.8→6.12] uic rejects signal/slot connections whose
signature contains a template type, e.g. setValues(QList<double>)
("Invalid connection"); not covered by the QTBUG-151379 fix
* [QTBUG-44780](https://qt-project.atlassian.net/browse/QTBUG-44780) QMimeDatabase does not guard against cyclic parent
hierarchies
* [QTBUG-151828](https://qt-project.atlassian.net/browse/QTBUG-151828) [REG 6.11 → 6.12] QString s(maxSize() + 1, u'x')
segfaults instead of bad_alloc or std::terminate()
* [QTBUG-149611](https://qt-project.atlassian.net/browse/QTBUG-149611) QFont::setPointSize warning on hover-leave of a styled
QToolButton with a pixel-size font
* [QTBUG-48442](https://qt-project.atlassian.net/browse/QTBUG-48442) After setting a font with QApplication::setFont QWizard
title is too small
* [QTBUG-150334](https://qt-project.atlassian.net/browse/QTBUG-150334) QtCore / text: QString::asprintf(): %jn/%zn/%tn write 4
bytes into a wider object  (TXTBUG-08)
* [QTBUG-149987](https://qt-project.atlassian.net/browse/QTBUG-149987) QtCore / serialization: QDataStream:  Truncation decodes
as a valid-empty value  (SERBUG-09)
* [QTBUG-134286](https://qt-project.atlassian.net/browse/QTBUG-134286) QSortFilterProxyModel memory overflow when source model
emits dataChanged() with out of bound column numbers
* [QTBUG-151740](https://qt-project.atlassian.net/browse/QTBUG-151740) [Reg 6.8→6.12] QDockWidget::dockLocation crashes (null
QMainWindow) when the dock widget has no QMainWindow parent, documented
to return NoDockWidgetArea; QFormBuilder::save() crashes too
* [QTBUG-151310](https://qt-project.atlassian.net/browse/QTBUG-151310) Can't use tab to navigate QCheckBoxes in a non-exclusive
QButtonGroup
* [QTBUG-151639](https://qt-project.atlassian.net/browse/QTBUG-151639) tst_QRhi::indexedIndirectMultiDrawShaderDrawParams(OpenGL)
test failure in Guix
* [QTBUG-142074](https://qt-project.atlassian.net/browse/QTBUG-142074) readonly TextInput cause warning that application copied
from clipboard on Android
* [QTBUG-151842](https://qt-project.atlassian.net/browse/QTBUG-151842) Android: clipboard changes run
QQuickTextInput/QQuickTextEdit::q_canPasteChanged() on the Android UI
thread, causing a use-after-free
* [QTBUG-135605](https://qt-project.atlassian.net/browse/QTBUG-135605) QSortFilterProxyModel::invalidateFilter() /
beginFilterChange(), endFilterChange() after invalidate() does not emit
all signals in proxy models
* [QTBUG-151795](https://qt-project.atlassian.net/browse/QTBUG-151795) QRhiVulkan::create() dereferences a null QVulkanInstance
(SIGSEGV) when Vulkan is forced on the offscreen QPA
* [QTBUG-151881](https://qt-project.atlassian.net/browse/QTBUG-151881) QBackingStoreDefaultCompositor::toTexture() copies the
whole backing store, even if only a small part is dirty
* [QTBUG-151830](https://qt-project.atlassian.net/browse/QTBUG-151830) [qtbase] Build fails in qprintdialog_unix.cpp with
accessibility disabled
* [QTBUG-151859](https://qt-project.atlassian.net/browse/QTBUG-151859) [Regression] Manifest not embedded with VS generator on
Windows
* [QTBUG-149206](https://qt-project.atlassian.net/browse/QTBUG-149206) harmonydeployqt can only sign with DevEco-managed
material because it signs through hvigor
* [QTBUG-151713](https://qt-project.atlassian.net/browse/QTBUG-151713) CMake deploy scripts don't include the platform plugin
* [QTBUG-149323](https://qt-project.atlassian.net/browse/QTBUG-149323) LinkDropDemo: Unable to Retrieve URL When Dragging a
Hyperlink from a Native App to Qt
* [QTBUG-130303](https://qt-project.atlassian.net/browse/QTBUG-130303) QT_CMAKE_EXPORT_NAMESPACE not found if find_package(Qt6)
is called in a function
* [QTBUG-139973](https://qt-project.atlassian.net/browse/QTBUG-139973) Stationary touch points when switching windows
* [QTBUG-149456](https://qt-project.atlassian.net/browse/QTBUG-149456) [REG 6.8→6.9] MinGW: adopted std::thread/pthread never
emits QThread::finished(), leaks QThreadData and QThreadStorage data
* [QTBUG-150314](https://qt-project.atlassian.net/browse/QTBUG-150314) HarmonyOS: ctest test bundle HAP is unusable outside a
full arm64 build
* [QTBUG-149501](https://qt-project.atlassian.net/browse/QTBUG-149501) Duplicate character committed when Celia keyboard sends
setPreviewText after insertText (Spanish layout)
* [QTBUG-150215](https://qt-project.atlassian.net/browse/QTBUG-150215) QtCore / serialization: XML reader carries entity state
across clear(): entityLength (SERBUG-03b)
* [QTBUG-150546](https://qt-project.atlassian.net/browse/QTBUG-150546) macOS: Ugly borders for QLineEdit with custom background
* [QTBUG-149896](https://qt-project.atlassian.net/browse/QTBUG-149896) tst_QAbstractItemView::QTBUG46785_mouseout_hover_state()
'delegate.m_paintedWithoutHover' returned FALSE
* [QTBUG-149848](https://qt-project.atlassian.net/browse/QTBUG-149848) [QT5&QT6]Green “+” indicator is missing at some
positions inside DropArea on OHOS
* [QTBUG-150323](https://qt-project.atlassian.net/browse/QTBUG-150323) qvkgen abort in native HarmonyOS build
* [QTBUG-133406](https://qt-project.atlassian.net/browse/QTBUG-133406) Unrechable code in MetaTypeQFutureHelper
* [QTBUG-150570](https://qt-project.atlassian.net/browse/QTBUG-150570) HarmonyOS: NonFullScreenWindows reported false in non-
free-window mode forces every popup and dialog to (0,0)
* [QTBUG-145768](https://qt-project.atlassian.net/browse/QTBUG-145768) tst_QDateTime::springForward:Asia/Singapore fails on
some platforms
* [QTBUG-149228](https://qt-project.atlassian.net/browse/QTBUG-149228) [REG 6.11->6.12] ASSERT: "dockNum < docks.size()"
* [QTBUG-122436](https://qt-project.atlassian.net/browse/QTBUG-122436) Android a11y: Changes to Accessible.ignored and
Item.visible are not propagated to the screen reader
* [QTBUG-144006](https://qt-project.atlassian.net/browse/QTBUG-144006) Android: Drag and drop does not work using DragHandler
and DropArea.
* [QTBUG-76544](https://qt-project.atlassian.net/browse/QTBUG-76544) DropArea doesn't work on Android
* [QTBUG-140200](https://qt-project.atlassian.net/browse/QTBUG-140200) Modal QML Popup not modal to a11y layer
* [QTBUG-150912](https://qt-project.atlassian.net/browse/QTBUG-150912) Static QMessageBox functions are not protected against
deleting parent
* [QTBUG-149559](https://qt-project.atlassian.net/browse/QTBUG-149559) `QCborValue::type()` changes after `toCbor()` and
`fromCbor()` round-trip for an empty `QDateTime`
* [QTBUG-146211](https://qt-project.atlassian.net/browse/QTBUG-146211) IME under text-input-v3 is never disabled on COSMIC
* [QTBUG-141712](https://qt-project.atlassian.net/browse/QTBUG-141712) tst_Android::testFullScreenDimensions() fails
* [QTBUG-150968](https://qt-project.atlassian.net/browse/QTBUG-150968) Windows: first font fallback lookup populates every
installed font family, blocking the GUI thread for seconds with many
fonts installed
* [QTBUG-151119](https://qt-project.atlassian.net/browse/QTBUG-151119) Qt Concurrent: Document that map/filter can monopolize a
thread pool
* [QTBUG-151210](https://qt-project.atlassian.net/browse/QTBUG-151210) QDoc: Links in member documentation prefer global
targets over class members
* [QTBUG-150504](https://qt-project.atlassian.net/browse/QTBUG-150504) Qt Creator Combo Box Padding Issue
* [QTBUG-151082](https://qt-project.atlassian.net/browse/QTBUG-151082) Blacklist tst_QWidget::palettePropagation2 as it is
failing on wayland
* [QTBUG-141832](https://qt-project.atlassian.net/browse/QTBUG-141832) Creating a QJSEngine still results in a segfault on
sparc64 with Qt6
* [QTBUG-151287](https://qt-project.atlassian.net/browse/QTBUG-151287) Some editable widgets appear unusable
* [QTBUG-151285](https://qt-project.atlassian.net/browse/QTBUG-151285) The QSpinBox frame looks clipped on the left and right
* [QTBUG-151321](https://qt-project.atlassian.net/browse/QTBUG-151321) Icons (buttons) in list headers are practically
invisible
* [QTBUG-147941](https://qt-project.atlassian.net/browse/QTBUG-147941) QDirListing does not detect Windows junctions
* [QTBUG-149869](https://qt-project.atlassian.net/browse/QTBUG-149869) Fix uncontrolled recursion problem in
QMimeBinaryProvider/QMimeMagicRule
* [QTBUG-48876](https://qt-project.atlassian.net/browse/QTBUG-48876) qmake on Windows generates wrong Makefile when
MSys2/sh.exe is in the PATH
* [QTBUG-149556](https://qt-project.atlassian.net/browse/QTBUG-149556) Evaluate HiTrace instrumentation patches for merging
into HarmonyOS branch mainline
* [QTBUG-137726](https://qt-project.atlassian.net/browse/QTBUG-137726) Highlighted text color remain black in windows11 style
* [QTBUG-49319](https://qt-project.atlassian.net/browse/QTBUG-49319) QML RegExpValidator not accepting input for regExp length
greater than 1024
* [QTBUG-55078](https://qt-project.atlassian.net/browse/QTBUG-55078) Not all roles supported by QStringListModel
* [QTBUG-54693](https://qt-project.atlassian.net/browse/QTBUG-54693) QFileDialog::getOpenFileName crashes when parent is
deleted while dialog is open
* [QTBUG-151381](https://qt-project.atlassian.net/browse/QTBUG-151381) Play Store complains about deprecated Window management
API use
* [QTBUG-118489](https://qt-project.atlassian.net/browse/QTBUG-118489) Can't tab to last button in QDialogButtonBox
* [QTBUG-151309](https://qt-project.atlassian.net/browse/QTBUG-151309) Plugins from a mismatching Qt version are loaded via
QT_PLUGIN_PATH even when a matching system plugin exists (Wayland shell
integration → crash)
* [QTBUG-150493](https://qt-project.atlassian.net/browse/QTBUG-150493) HarmonyOS: a subwindow hidden together with its main
window is still reported as an ordinary visible window
* [QTBUG-142157](https://qt-project.atlassian.net/browse/QTBUG-142157) QCursor::pos() doesn't match enter event position
* [QTBUG-151525](https://qt-project.atlassian.net/browse/QTBUG-151525) QWaylandShmBackingStore can reuse a buffer whose device
pixel ratio no longer matches the window
* [QTBUG-151727](https://qt-project.atlassian.net/browse/QTBUG-151727) CMake potentially emits the same cmake_autogen commands
into multiple targets that may race
* [QTBUG-150333](https://qt-project.atlassian.net/browse/QTBUG-150333) QtCore / text: QString::asprintf(): h/hh do not narrow
the argument  (TXTBUG-07)
* [QTBUG-150796](https://qt-project.atlassian.net/browse/QTBUG-150796) QT_NO_CPU_FEATURE is ignored
* [QTBUG-146582](https://qt-project.atlassian.net/browse/QTBUG-146582) Disabled QCheckBox indicator has poor contrast in dark
mode on Ubuntu GNOME
* [QTBUG-151899](https://qt-project.atlassian.net/browse/QTBUG-151899) Fix issues in Mach-O parser
* [QTBUG-151888](https://qt-project.atlassian.net/browse/QTBUG-151888) Fix issues in COFF/PE parser implementation
* [QTBUG-150822](https://qt-project.atlassian.net/browse/QTBUG-150822) Public qvirtualkeyboard_namespace.h includes a private
header and fails to compile without private include paths
* [QTBUG-151669](https://qt-project.atlassian.net/browse/QTBUG-151669) Top flaky test: tst_QTcpSocket
readNotificationsAfterBind
* [QTBUG-151793](https://qt-project.atlassian.net/browse/QTBUG-151793) [REG] Resizing glyph caches with texture resize
workaround broken
* [QTBUG-152104](https://qt-project.atlassian.net/browse/QTBUG-152104) macOS framework builds: moc fails on bare includes in
qmake projects that pull in a header-only module

### qtsvg
* [QTBUG-151324](https://qt-project.atlassian.net/browse/QTBUG-151324) [REG 6.11 -> 6.12] QImageReader::format() may return an
empty format for SVG read from a device without a file name

### qtdeclarative
* [QTBUG-149607](https://qt-project.atlassian.net/browse/QTBUG-149607) Cannot assign object of type "Foo" to property of type
"Foo_QMLTYPE_0*" as the former is neither the same as the latter nor a
sub-class of it."
* [QTBUG-149933](https://qt-project.atlassian.net/browse/QTBUG-149933) Unclear crash in the qml engine's property calculation
* [QTBUG-149567](https://qt-project.atlassian.net/browse/QTBUG-149567) Flickable stutters when scrolling slowly with a
touchpad, and keeps moving after the fingers are lifted
* [QTBUG-70822](https://qt-project.atlassian.net/browse/QTBUG-70822) Having variable name same as class method name produces
an error
* [QTBUG-148401](https://qt-project.atlassian.net/browse/QTBUG-148401) Update QML tree view models support documentation
* [QTBUG-149610](https://qt-project.atlassian.net/browse/QTBUG-149610) TextInput canPaste is recomputed eagerly on
QClipboard::dataChanged() (2 s stall per focus-in on Wayland)
* [QTBUG-121594](https://qt-project.atlassian.net/browse/QTBUG-121594) Paste Action can't be disabled in context menu of
TextField
* [QTBUG-149806](https://qt-project.atlassian.net/browse/QTBUG-149806) QtQuick.VectorImage leaks internal item tree on every
source change
* [QTBUG-150048](https://qt-project.atlassian.net/browse/QTBUG-150048) ListView: negative model index reaches
QQmlListCompositor::find() when the event loop is spun during delegate
creation
* [QTBUG-149512](https://qt-project.atlassian.net/browse/QTBUG-149512) Intermittent access violation in QV4::MemoryManager
during incremental GC on 6.12.0 Beta3 (Windows 11, MSVC 2022)
* [QTBUG-149247](https://qt-project.atlassian.net/browse/QTBUG-149247) VectorImage/svgtoqml gives wrong results when applying
group opacity
* [QTBUG-148990](https://qt-project.atlassian.net/browse/QTBUG-148990) Property alias change notification is not documented
* [QTBUG-62912](https://qt-project.atlassian.net/browse/QTBUG-62912) Hover is not reset properly with touchscreens
* [QTBUG-114420](https://qt-project.atlassian.net/browse/QTBUG-114420) MouseArea containsMouse is unreliable for touch events
* [QTBUG-40856](https://qt-project.atlassian.net/browse/QTBUG-40856) MouseArea containsMouse flag is not reset on Touch Screen
* [QTBUG-150371](https://qt-project.atlassian.net/browse/QTBUG-150371) Touch delivery can leave a phantom point on the
touchscreen, so fingertip hover is never cleared
* [QTBUG-150363](https://qt-project.atlassian.net/browse/QTBUG-150363) [VxWorks] qtdeclarative: 8 autotests fail on VxWorks
26.03 (QEMU armv7 + x86_64, static build)
* [QTBUG-150326](https://qt-project.atlassian.net/browse/QTBUG-150326) qmlls: don't freeze on shutdown
* [QTBUG-150640](https://qt-project.atlassian.net/browse/QTBUG-150640) Compiled QML reads the wrong property of a value type
that derives from another Q_GADGET
* [QTBUG-147141](https://qt-project.atlassian.net/browse/QTBUG-147141) Get rid of QQmlJSMetaMethod::otherFunctionIndex
* [QTBUG-149040](https://qt-project.atlassian.net/browse/QTBUG-149040) [QtQmlModels] ListModel.append() stack-overflows on a
deeply-nested JS object (via QJSValue::toVariant())
* [QTBUG-150558](https://qt-project.atlassian.net/browse/QTBUG-150558) QmlPreview in-place update crashes when a lazily loaded
.mjs is still pending
* [QTBUG-150561](https://qt-project.atlassian.net/browse/QTBUG-150561) Live preview doesn't hot reload looping animation when
duration is changed
* [QTBUG-150769](https://qt-project.atlassian.net/browse/QTBUG-150769) [REG 6.11.2] Sporadic crashes on QQuickItemView
destuction
* [QTBUG-61938](https://qt-project.atlassian.net/browse/QTBUG-61938) [regression] Mouse Move Event Generated on Touch Release
* [QTBUG-68970](https://qt-project.atlassian.net/browse/QTBUG-68970) Bad mouse move event
* [QTBUG-121913](https://qt-project.atlassian.net/browse/QTBUG-121913) Emitter.InfiniteLife is short
* [QTBUG-124663](https://qt-project.atlassian.net/browse/QTBUG-124663) Auto-scrolling a ListView breaks drag operation
* [QTBUG-147855](https://qt-project.atlassian.net/browse/QTBUG-147855) Popup.Window dismisses itself on macOS trackpad movement
(not with a mouse)
* [QTBUG-151107](https://qt-project.atlassian.net/browse/QTBUG-151107) MenuItem hides its shortcut when sized to its implicit
width
* [QTBUG-133087](https://qt-project.atlassian.net/browse/QTBUG-133087) Shortcut key sequence not shown in MenuItem
* [QTBUG-151077](https://qt-project.atlassian.net/browse/QTBUG-151077) tst_snippets fails in static builds — Qt.labs.qmlmodels
QML plugin is not linked   into the test binary
* [QTBUG-150834](https://qt-project.atlassian.net/browse/QTBUG-150834) Qt.labs.sharedimage: verifyMem() size checks overflow
int, so a malformed header passes and QImage reads out of bounds
* [QTBUG-60984](https://qt-project.atlassian.net/browse/QTBUG-60984) Crash when marking for garbage collection
* [QTBUG-130819](https://qt-project.atlassian.net/browse/QTBUG-130819) Crash with ListView having a section delegate when model
resets
* [QTBUG-151133](https://qt-project.atlassian.net/browse/QTBUG-151133) Crash converting a large JS array to a sequence type
* [QTBUG-151092](https://qt-project.atlassian.net/browse/QTBUG-151092) Binding of property causes QML app to crash
* [QTBUG-151089](https://qt-project.atlassian.net/browse/QTBUG-151089) A visible ToolTip stops a modal Popup below it from
blocking presses
* [QTBUG-146164](https://qt-project.atlassian.net/browse/QTBUG-146164) Inconsistent close behavior for nested Popups across
popupType variants
* [QTBUG-146849](https://qt-project.atlassian.net/browse/QTBUG-146849) Quickshell crashes after reload when using
Qt.labs.StyleKit
* [QTBUG-151189](https://qt-project.atlassian.net/browse/QTBUG-151189) qmlpreview hot reload crashes the client when a saved
change adds an object (component rebuild)
* [QTBUG-141832](https://qt-project.atlassian.net/browse/QTBUG-141832) Creating a QJSEngine still results in a segfault on
sparc64 with Qt6
* [QTBUG-150672](https://qt-project.atlassian.net/browse/QTBUG-150672) QtQuickView.connectSignalListener() returns a valid id
even when the connection failed
* [QTBUG-150923](https://qt-project.atlassian.net/browse/QTBUG-150923) QQuickWindow: updateChildWindowStackingOrder() walks the
whole item tree on every polish, even without child windows
* [QTBUG-151273](https://qt-project.atlassian.net/browse/QTBUG-151273) Heap-use-after-free in QML garbage collector when using
generators (regression since 6.8)
* [QTBUG-151172](https://qt-project.atlassian.net/browse/QTBUG-151172) Quick.Dialogs MessageDialog does not show when
QQuickView is embedded in QWidget
* [QTBUG-151368](https://qt-project.atlassian.net/browse/QTBUG-151368) Doc: SpinBox docs don't say when the up and down
indicators are disabled
* [QTBUG-41634](https://qt-project.atlassian.net/browse/QTBUG-41634) Missing documentation for SpinBoxStyle
* [QTBUG-44198](https://qt-project.atlassian.net/browse/QTBUG-44198) Qml / C++ integration documentation
* [QTBUG-150990](https://qt-project.atlassian.net/browse/QTBUG-150990) Composite singleton in a JS array becomes null when
assigned to an object list property
* [QTBUG-151124](https://qt-project.atlassian.net/browse/QTBUG-151124) Crash when QObjectWrapper::ensureWrapper() dereferences
a null wrapper when an AOT-compiled call returns a QObject queued for
deletion during an incremental GC
* [QTBUG-151176](https://qt-project.atlassian.net/browse/QTBUG-151176) TableView delegate with a required property evaluates
its bindings with a null QML context — all globals (Math, console) and
ids resolve to  undefined
* [QTBUG-150967](https://qt-project.atlassian.net/browse/QTBUG-150967) [REG 6.11->6.12] AOT code silently discarded for modules
built with NO_RESOURCE_TARGET_PATH
* [QTBUG-150375](https://qt-project.atlassian.net/browse/QTBUG-150375) Non-native FileDialog does not react to the "Enter" key
* [QTBUG-147240](https://qt-project.atlassian.net/browse/QTBUG-147240) Dynamically created FileDialog with Qt.WindowModal
modality shown as non-modal
* [QTBUG-151518](https://qt-project.atlassian.net/browse/QTBUG-151518) ListModel: possible crash when writing to an object from
get() after its row was removed
* [QTBUG-151666](https://qt-project.atlassian.net/browse/QTBUG-151666) tst_qmlcachegen fails to link when cross-compiling on a
Windows host for a UNIX target
* [QTBUG-151403](https://qt-project.atlassian.net/browse/QTBUG-151403) Fails to find QML plugin
* [QTBUG-46554](https://qt-project.atlassian.net/browse/QTBUG-46554) Canvas.requestAnimationFrame undocumented
* [QTBUG-150992](https://qt-project.atlassian.net/browse/QTBUG-150992) Image loaded before its item has a window uses
qApp->devicePixelRatio() and is never reloaded for the actual window DPR
* [QTBUG-151376](https://qt-project.atlassian.net/browse/QTBUG-151376) [Regression 6.8.9->6.12.0] Bindings that switch on a
component-local QML `enum` evaluate significantly slower in Qt 6.12.0
than in 6.8.9 if QML_DISABLE_DISK_CACHE is enabled
* [QTBUG-151353](https://qt-project.atlassian.net/browse/QTBUG-151353) [Reg] Image reloads unnecessarily when reparenting into
a window with dpr != 1
* [QTBUG-113232](https://qt-project.atlassian.net/browse/QTBUG-113232) Scalable image formats not rendered at correct DPR when
extension is left out
* [QTBUG-120190](https://qt-project.atlassian.net/browse/QTBUG-120190) SVG blurry on retina when source provided as data scheme
* [QTBUG-50249](https://qt-project.atlassian.net/browse/QTBUG-50249) ImageParticle documentation regarding opacityTable is
confusing
* [QTBUG-146169](https://qt-project.atlassian.net/browse/QTBUG-146169) ListView displays duplicate section label when
currentIndex is set
* [QTBUG-151330](https://qt-project.atlassian.net/browse/QTBUG-151330) BorderImage with an SVG source has half the implicit
size on high-DPI screens
* [QTBUG-151653](https://qt-project.atlassian.net/browse/QTBUG-151653) FunctionFilter regression
* [QTBUG-151511](https://qt-project.atlassian.net/browse/QTBUG-151511) Crash in MemoryManager::collectFromJSStack() for a
derived class without a constructor (regression from the QTBUG-151273
fix)
* [QTBUG-151685](https://qt-project.atlassian.net/browse/QTBUG-151685) Writing a value-type alias in QML loses a sibling sub-
property's binding
* [QTBUG-150828](https://qt-project.atlassian.net/browse/QTBUG-150828) Synchronizer: changing source on a property without
NOTIFY/bindable erases an end() iterator
* [QTBUG-148608](https://qt-project.atlassian.net/browse/QTBUG-148608) SortFilterProxyModel: FunctionFilter and FunctionSorter
double-delete their parameter object
* [QTBUG-151727](https://qt-project.atlassian.net/browse/QTBUG-151727) CMake potentially emits the same cmake_autogen commands
into multiple targets that may race
* [QTBUG-151791](https://qt-project.atlassian.net/browse/QTBUG-151791) Crash in
QRhiImplementation::sanityCheckResourceOwnership() when rendering
distance field text with D3D11
* [QTBUG-151612](https://qt-project.atlassian.net/browse/QTBUG-151612) SIGSEGV in QSGRhiDistanceFieldGlyphCache
* [QTBUG-151704](https://qt-project.atlassian.net/browse/QTBUG-151704) JavaScript objects passed through QML signals lose
reference semantics in Qt 6.12
* [QTBUG-149404](https://qt-project.atlassian.net/browse/QTBUG-149404) XMLHttpRequest memory leak caused by network error
* [QTCREATORBUG-35096](https://qt-project.atlassian.net/browse/QTCREATORBUG-35096) QML code completion suggests unscoped enum values
when RegisterEnumClassesUnscoped is false
* [QTBUG-138142](https://qt-project.atlassian.net/browse/QTBUG-138142) qmllint DropArea Reading non-constant and non-notifiable
property hasColor
* [QTBUG-151826](https://qt-project.atlassian.net/browse/QTBUG-151826) ternary operator returns undefined
* [QTBUG-151670](https://qt-project.atlassian.net/browse/QTBUG-151670) Render thread crash when an updated text has more than
threshold on 6.12.0
* [QTBUG-151717](https://qt-project.atlassian.net/browse/QTBUG-151717) Crash in QQmlIncubator::forceComplete
* [QTBUG-151790](https://qt-project.atlassian.net/browse/QTBUG-151790) qmlcache gen produces incorrect code and breaks KDE
applications
* [QTBUG-151316](https://qt-project.atlassian.net/browse/QTBUG-151316) Hiding or showing an item makes the batch renderer
rebuild every batch in the scene, in some cases unnecessarily
* [QTBUG-85965](https://qt-project.atlassian.net/browse/QTBUG-85965) Batch rendering order may go wrong if batch's first node
gets invisible
* [QTBUG-151313](https://qt-project.atlassian.net/browse/QTBUG-151313) Reg: QObject from Q_PROPERTY wrongly gets
JavaScriptOwnership with Qt Quick Compiler
* [QTBUG-141215](https://qt-project.atlassian.net/browse/QTBUG-141215) Doc: QML TreeModel scheme image not readable in dark
mode
* [QTBUG-142250](https://qt-project.atlassian.net/browse/QTBUG-142250) assertion failure in QQuickItemLayer::componentComplete
when using QQuickSlider
* [QTBUG-150293](https://qt-project.atlassian.net/browse/QTBUG-150293) [REG 6.8.9->6.12.0]
qmlcompiler/tutorials/helloworld/chapter3 not compiling on QNX
* [QTBUG-151831](https://qt-project.atlassian.net/browse/QTBUG-151831) Qt Quick render loops don't recreate the swapchain after
VK_ERROR_OUT_OF_DATE_KHR, window stops rendering (Vulkan)
* [QTBUG-63976](https://qt-project.atlassian.net/browse/QTBUG-63976) Updating ListModel in another thread results in the view
and model having different number of items
* [QTBUG-63935](https://qt-project.atlassian.net/browse/QTBUG-63935) ListModel.sync() leaves one model object hanging
* [QTBUG-145710](https://qt-project.atlassian.net/browse/QTBUG-145710) QML tools and runtime engine have gaps and discrepancies
in handling undefined properties
* [QTBUG-150075](https://qt-project.atlassian.net/browse/QTBUG-150075) FAILED:
examples/demos/osmbuildings/CMakeFiles/osmbuildings_qmllint /Users/qt/wo
rk/qt/qtdoc_standalone_examples/examples/demos/osmbuildings/CMakeFiles/o
smbuildings_qmllint
* [QTBUG-108362](https://qt-project.atlassian.net/browse/QTBUG-108362) TDZ checks are broken in QML
* [QTBUG-148459](https://qt-project.atlassian.net/browse/QTBUG-148459) Null dereference in
QQmlConnections::connectSignalsToMethods() during asynchronous
incubation
* [QTBUG-130890](https://qt-project.atlassian.net/browse/QTBUG-130890) QML ListView unable to properly show dynamic delegates
of different heights
* [QTBUG-150082](https://qt-project.atlassian.net/browse/QTBUG-150082) [Android] Qt Quick examples do not respect safe-area
margins, causing content to overlap the system status bar
* [QTBUG-151367](https://qt-project.atlassian.net/browse/QTBUG-151367) Quick Rectangle asserts with small widths
* [QTBUG-147814](https://qt-project.atlassian.net/browse/QTBUG-147814) QML cold-load import resolution is dominated by qrc-
engine per-lookup cost
* [QTBUG-142189](https://qt-project.atlassian.net/browse/QTBUG-142189) QtQuick Switch mouse/touch tests fail related to center
point for macOS style
* [QTBUG-151381](https://qt-project.atlassian.net/browse/QTBUG-151381) Play Store complains about deprecated Window management
API use

### qtmultimedia
* [QTBUG-149942](https://qt-project.atlassian.net/browse/QTBUG-149942) [FFmpeg] Race blocking adding frames to encoder
* [QTBUG-
150172](https://qt-project.atlassian.net/browse/QTBUG-150172) play_playsTransformedVideoOutput_whenVideoFileHasTransformationMe
tadata failure on macOS 26 host
* [QTBUG-126276](https://qt-project.atlassian.net/browse/QTBUG-126276) QMediaRecorder fails to encode to Matroska file format
with some codecs
* [QTBUG-150171](https://qt-project.atlassian.net/browse/QTBUG-150171) XPASS in tst_QMediaRecorderBackend on macOS 26 host
* [QTBUG-150059](https://qt-project.atlassian.net/browse/QTBUG-150059) Cannot compile with "-no-opengl"
* [QTBUG-150386](https://qt-project.atlassian.net/browse/QTBUG-150386) Ubuntu 26.04 x64: tst_gstreamer_backend reports
incorrect video bitrate metadata
* [QTBUG-150290](https://qt-project.atlassian.net/browse/QTBUG-150290) [QT5&QT6]Camera Demo: Live Camera Preview Is Blank While
Photo Capture and Video Recording Work Normally
* [QTBUG-150974](https://qt-project.atlassian.net/browse/QTBUG-150974) Crash in QWindowsAudioDevice format probing
(performFormatProbe)
* [QTBUG-150720](https://qt-project.atlassian.net/browse/QTBUG-150720) [REG 6.12.0 beta -> RC] Android: MediaPlayer example
cannot open any https source with the FFmpeg backend ("certificate
verify failed")
* [QTBUG-150678](https://qt-project.atlassian.net/browse/QTBUG-150678) PipeWire: QAudioSink is used after delete when the
output device is removed
* [QTBUG-151116](https://qt-project.atlassian.net/browse/QTBUG-151116) [macOS] Crash in
DeviceDisconnectMonitor::removeListenerBlock on audio device disconnect
* [QTBUG-151203](https://qt-project.atlassian.net/browse/QTBUG-151203) QSoundEffect constructor crashes with SIGSEGV when
PipeWire client.conf is missing
* [QTBUG-151185](https://qt-project.atlassian.net/browse/QTBUG-151185) Memory leak: FFmpeg backend: the AVIOContext of a
QIODevice source is never freed (on Android: every content:// URL)
* [QTBUG-149931](https://qt-project.atlassian.net/browse/QTBUG-149931) QFFmpegVideoBuffer::maxNits() multiplies the mastering
display luminance by 10000 a second time
* [QTBUG-149925](https://qt-project.atlassian.net/browse/QTBUG-149925) Still image capture is limited to QCameraFormat
resolution
* [QTBUG-150969](https://qt-project.atlassian.net/browse/QTBUG-150969) wasm64: QWasmVideoFrameGrabber accesses an invalid
Emscripten handle in requestAnimationFrame callback
* [QTBUG-150044](https://qt-project.atlassian.net/browse/QTBUG-150044) [FFmpeg] Recording of QVideoFrameInput includes pause
duration
* [QTBUG-151655](https://qt-project.atlassian.net/browse/QTBUG-151655) QtMultimedia (Windows/WASAPI): one \Device\MMCSS handle
leaked every time an audio sink stream starts
(AvSetMmThreadCharacteristicsA without AvRevertMmThreadCharacteristics)
* [QTBUG-151157](https://qt-project.atlassian.net/browse/QTBUG-151157) MediaPlayer on macOS 27 - no way to turn off automatic
subtitles
* [QTBUG-151155](https://qt-project.atlassian.net/browse/QTBUG-151155) WAV decoding: frames count from header is not trusted
* [QTBUG-151984](https://qt-project.atlassian.net/browse/QTBUG-151984) PipeWire backend: audio input devices have mode Output,
QAudioInput::setDevice() ignores them
* [QTBUG-152004](https://qt-project.atlassian.net/browse/QTBUG-152004) Qt Multimedia does not compile for Android with C++20:
QAndroidAudioSourceStream/SinkStream lack SourceType/SinkType
* [QTBUG-148572](https://qt-project.atlassian.net/browse/QTBUG-148572) QtMultimedia fails to build on yocto for selected
targets
* [QTBUG-151355](https://qt-project.atlassian.net/browse/QTBUG-151355) Crashing/flaky qtmultimedia tests in Windows after
adding audio in CI
* [QTBUG-151052](https://qt-project.atlassian.net/browse/QTBUG-151052) QScreenCapture::stop() crashes in pw_thread_loop_stop
after OpenPipeWireRemote fails
* [QTBUG-151333](https://qt-project.atlassian.net/browse/QTBUG-151333) QAudioSink crashes when the audio device disconnects
after reset()

### qttools
* [QTBUG-149632](https://qt-project.atlassian.net/browse/QTBUG-149632) uic fails to build .ui files containing <set> tags where
data has CR/LF
* [QTBUG-2801](https://qt-project.atlassian.net/browse/QTBUG-2801) Disable geometry property for the internal children of
containers
* [QTBUG-136340](https://qt-project.atlassian.net/browse/QTBUG-136340) Build fails without cssparser feature
* [QTBUG-150869](https://qt-project.atlassian.net/browse/QTBUG-150869) QDoc: Shared property accessors may link to deprecated
or non-deterministic targets
* [QTBUG-145807](https://qt-project.atlassian.net/browse/QTBUG-145807) QDoc: Property anchor for shared notifier signals is
non-deterministic
* [QTBUG-128356](https://qt-project.atlassian.net/browse/QTBUG-128356) https://doc.qt.io/qt-
6/qscreen.html#physicalDotsPerInchChanged missing an entry?
* [QTBUG-150871](https://qt-project.atlassian.net/browse/QTBUG-150871) QDoc: Apply consistent precedence when resolving
ambiguous link targets
* [QTBUG-136339](https://qt-project.atlassian.net/browse/QTBUG-136339) Build fails without texthtmlparser feature
* [QTBUG-150643](https://qt-project.atlassian.net/browse/QTBUG-150643) Duplicate entries in Qt WebEngine's list of 3rd party
licenses
* [QTBUG-121925](https://qt-project.atlassian.net/browse/QTBUG-121925) \list does not accept a comment symbol after it
* [QTBUG-150084](https://qt-project.atlassian.net/browse/QTBUG-150084) QHelpEngine::setupData() creates empty file in read-only
mode
* [QTBUG-130137](https://qt-project.atlassian.net/browse/QTBUG-130137) [Reg 5->6]  Qt Assistant does not support to open a link
in a new tab by pressing the middle mouse button
* [QTBUG-109158](https://qt-project.atlassian.net/browse/QTBUG-109158) assistant doesn't provide a context menu in the
documentation page
* [QTBUG-101045](https://qt-project.atlassian.net/browse/QTBUG-101045) Assistant: Document page loses keyboard focus after
search
* [QTBUG-150820](https://qt-project.atlassian.net/browse/QTBUG-150820) QDoc: \relates on \enum modifies outer scope
* [QTBUG-151158](https://qt-project.atlassian.net/browse/QTBUG-151158) QDoc: Template Generator drops captions
* [QTBUG-151174](https://qt-project.atlassian.net/browse/QTBUG-151174) QDoc: Undocumented base classes listed as unlinked text
in Inherits
* [QTBUG-151169](https://qt-project.atlassian.net/browse/QTBUG-151169) QDoc: \important admonitions not rendered by Template
Generator
* [QTBUG-151276](https://qt-project.atlassian.net/browse/QTBUG-151276) QDoc: Template Generator output sends member-local links
to another member’s section
* [QTBUG-151277](https://qt-project.atlassian.net/browse/QTBUG-151277) QDoc: Template Generator suppresses explicit links to
deprecated targets
* [QTBUG-151053](https://qt-project.atlassian.net/browse/QTBUG-151053) QDoc: Respect empty template override files
* [QTBUG-151066](https://qt-project.atlassian.net/browse/QTBUG-151066) QDoc: .index related-node identifiers depend on enabled
output generators
* [QTBUG-151243](https://qt-project.atlassian.net/browse/QTBUG-151243) QDoc generates mismatched member anchors and links
* [QTBUG-151210](https://qt-project.atlassian.net/browse/QTBUG-151210) QDoc: Links in member documentation prefer global
targets over class members
* [QTBUG-72107](https://qt-project.atlassian.net/browse/QTBUG-72107) \l font in QToolButton's documentation results in a link
to the font row in the stylesheet reference documentation
* [QTBUG-151295](https://qt-project.atlassian.net/browse/QTBUG-151295) QDoc: Module pages misreport whether a module has
namespaces
* [QTBUG-151108](https://qt-project.atlassian.net/browse/QTBUG-151108) QDoc: Qualify enum values in template-generated docs
* [QTBUG-151300](https://qt-project.atlassian.net/browse/QTBUG-151300) QDoc generates duplicate fragment IDs on legacy HTML
pages
* [QTBUG-151319](https://qt-project.atlassian.net/browse/QTBUG-151319) QDoc: Deprecation note uses the singular for shared
documentation
* [QTBUG-151323](https://qt-project.atlassian.net/browse/QTBUG-151323) QDoc: Metacommands apply twice to QML properties
documented together
* [QTBUG-151322](https://qt-project.atlassian.net/browse/QTBUG-151322) QDoc: Deprecation note omits the QML module name for
shared documentation
* [QTBUG-151328](https://qt-project.atlassian.net/browse/QTBUG-151328) QDoc: Render deprecation notes in template-generated
output
* [QTBUG-151317](https://qt-project.atlassian.net/browse/QTBUG-151317) Windows: qttools fails to compile with clang-cl based
compilers (clang-cl / icx / icpx): litehtml needs C++ exceptions but the
target gets no exception flag
* [QTBUG-150880](https://qt-project.atlassian.net/browse/QTBUG-150880) QDoc: Decouple non-function child filtering from output
ordering
* [QTBUG-151404](https://qt-project.atlassian.net/browse/QTBUG-151404) QDoc: Warnings repeat for each output format
* [QTBUG-151680](https://qt-project.atlassian.net/browse/QTBUG-151680) QDoc: Deprecated pages get "-obsolete" twice in .qhp and
.index
* [QTBUG-136345](https://qt-project.atlassian.net/browse/QTBUG-136345) allow to build tool "qhelpgenerator" without "assistant"
* [QTBUG-146939](https://qt-project.atlassian.net/browse/QTBUG-146939) qdoc: SIGABRT rendering collection pages with no CMake
info
* [QTBUG-136247](https://qt-project.atlassian.net/browse/QTBUG-136247) QDoc doesn´t resolve \externalpage title correctly
* [QTBUG-147652](https://qt-project.atlassian.net/browse/QTBUG-147652) Do not unconditionally capitalize first word in brief
texts
* [QTBUG-150798](https://qt-project.atlassian.net/browse/QTBUG-150798) QDoc: Text doesn't consistently preserve an Atom's state
and dynamic type when copying it into a Text
* [QTBUG-151775](https://qt-project.atlassian.net/browse/QTBUG-151775) QDoc: Render shared-comment detail once per group
* [QTBUG-151785](https://qt-project.atlassian.net/browse/QTBUG-151785) QDoc: Preserve QML property-group anchors in template
output
* [QTBUG-151846](https://qt-project.atlassian.net/browse/QTBUG-151846) [Reg 6.8→6.12] QFormBuilder::save() writes an empty
<set></set> for zero-valued flag properties (default QGraphicsView,
QListWidget, QScrollArea), which uic 6.12 rejects ("Invalid property
value")
* [QTBUG-136164](https://qt-project.atlassian.net/browse/QTBUG-136164) Saving UI-file using QFormBuilder missing properties
(unsupported?)
* [QTBUG-151840](https://qt-project.atlassian.net/browse/QTBUG-151840) [REG 6.13.0->6.12.0] non-gui build fails,
qttools/assistant
* [QTBUG-151992](https://qt-project.atlassian.net/browse/QTBUG-151992) QDoc fails on QDOC_SHOW_INTERNAL environment variable
* [QTBUG-152097](https://qt-project.atlassian.net/browse/QTBUG-152097) Help files get completely rejected
* [QTBUG-111594](https://qt-project.atlassian.net/browse/QTBUG-111594) QLiteHtml doesn't support animated images
* [QTBUG-102998](https://qt-project.atlassian.net/browse/QTBUG-102998) Qt Assistant ignores sub and sup tags
* [QTCREATORBUG-31339](https://qt-project.atlassian.net/browse/QTCREATORBUG-31339) Assistant/QLiteHtml: Image resources of Qt
Examples are displayed in garbled form
* [QTBUG-115448](https://qt-project.atlassian.net/browse/QTBUG-115448) qttools -unity-build-batch-size 100000 fails
* [QTBUG-151329](https://qt-project.atlassian.net/browse/QTBUG-151329) QDoc: Incorrect grammar in shared-comment \since notes
* [QTBUG-151761](https://qt-project.atlassian.net/browse/QTBUG-151761) Documentation of \code and friends needs some love

### qtdoc
* [QTBUG-147185](https://qt-project.atlassian.net/browse/QTBUG-147185) The landing page about Qt VNC Server is not listed under
modules any more
* [QTBUG-150260](https://qt-project.atlassian.net/browse/QTBUG-150260) FAILED:
examples/demos/samegame/CMakeFiles/samegame_qmllint /home/qt/work/qt/qtd
oc_standalone_examples/examples/demos/samegame/CMakeFiles/samegame_qmlli
nt
* [QTBUG-151075](https://qt-project.atlassian.net/browse/QTBUG-151075) Doc: Add official manufacturer info to Qt 6
Documentation
* [QTBUG-144849](https://qt-project.atlassian.net/browse/QTBUG-144849) Port Thermostat example away from Qt Charts
* [QTBUG-147382](https://qt-project.atlassian.net/browse/QTBUG-147382) windeployqt: Help output listed is outdated
* [QTBUG-46340](https://qt-project.atlassian.net/browse/QTBUG-46340) Linux Deployment, libqxcb depens on libQtDBus
* [QTBUG-44900](https://qt-project.atlassian.net/browse/QTBUG-44900) Need a page that describes Qt's OOM policy
* [QTBUG-150298](https://qt-project.atlassian.net/browse/QTBUG-150298) windeployqt does not deploy the third-party libraries
the Qt libraries need

### qtqa
* [PYSIDE-3504](https://qt-project.atlassian.net/browse/PYSIDE-3504) shiboken6-generator Linux wheel needs system
libxml2.so.2, which fails on Ubuntu 26.04

### qtsensors
* [QTBUG-150277](https://qt-project.atlassian.net/browse/QTBUG-150277) Android sensors plugin aborts in JNI GetMethodID when
Java getDefaultSensor() returns null (Honor devices)

### qtconnectivity
* [QTBUG-147192](https://qt-project.atlassian.net/browse/QTBUG-147192) HarmonyOS: port QtConnectivity (bluetooth) module
* [QTBUG-149351](https://qt-project.atlassian.net/browse/QTBUG-149351) QtBluetooth autotests on HarmonyOS stall on the adapter
and permission dialogs

### qtserialbus
* [QTBUG-151309](https://qt-project.atlassian.net/browse/QTBUG-151309) Plugins from a mismatching Qt version are loaded via
QT_PLUGIN_PATH even when a matching system plugin exists (Wayland shell
integration → crash)

### qtwebchannel
* [QTBUG-151078](https://qt-project.atlassian.net/browse/QTBUG-151078) Per-connection state is never released when a transport
is removed
* [QTBUG-151393](https://qt-project.atlassian.net/browse/QTBUG-151393) connectToSignal accepts a method index that is not a
signal
* [QTBUG-151516](https://qt-project.atlassian.net/browse/QTBUG-151516) QFuture continuation reads a result that doesn't exist
* [QTBUG-151083](https://qt-project.atlassian.net/browse/QTBUG-151083) Remote method arguments are dispatched without type,
arity or class validation
* [QTBUG-151298](https://qt-project.atlassian.net/browse/QTBUG-151298) Peer can cancel the framework's internal destroyed()
subscription

### qtvirtualkeyboard
* [QTBUG-147666](https://qt-project.atlassian.net/browse/QTBUG-147666) Virtual Keyboard PopupList warns about overriding
`contentWidth`
* [QTBUG-133246](https://qt-project.atlassian.net/browse/QTBUG-133246) Duplicated: "Note: Hunspell in Qt Virtual Keyboard"...
configure output

### qtspeech
* [QTBUG-151355](https://qt-project.atlassian.net/browse/QTBUG-151355) Crashing/flaky qtmultimedia tests in Windows after
adding audio in CI

### qtremoteobjects
* [QTBUG-150498](https://qt-project.atlassian.net/browse/QTBUG-150498) Flaky fail on Remote Objects
TestModelView::testDataInsertion()
* [QTBUG-132487](https://qt-project.atlassian.net/browse/QTBUG-132487) Crash: Remote Objects TestModelView::testDataInsertion()
random internal error

### qtlottie
* [QTBUG-152025](https://qt-project.atlassian.net/browse/QTBUG-152025) CMake: qtlottie is looking for itself

### qtquick3d
* [QTBUG-149579](https://qt-project.atlassian.net/browse/QTBUG-149579) Quick 3D: memory grows when swapping CustomMaterials
stored in a QML singleton
* [QTBUG-149590](https://qt-project.atlassian.net/browse/QTBUG-149590) Quick 3D: sky material uniform buffers are never
released when the material is destroyed
* [QTBUG-150763](https://qt-project.atlassian.net/browse/QTBUG-150763) Qt Quick 3D: the automatic disk shader cache
(q3dshadercache.qsbc) never hits for default materials
* [QTBUG-151125](https://qt-project.atlassian.net/browse/QTBUG-151125) Qt Quick 3D: memory grows when QQuickWindow is destroyed
and recreated
* [QTBUG-149278](https://qt-project.atlassian.net/browse/QTBUG-149278) XrController.isActive reads an uninitialised member and
never notifies
* [QTBUG-151378](https://qt-project.atlassian.net/browse/QTBUG-151378) Rendering issues with Order Independent Transparency
(OIT) method
* [QTBUG-151528](https://qt-project.atlassian.net/browse/QTBUG-151528) Weighted-Blended OIT composite pass blending is
incorrect
* [QTBUG-151397](https://qt-project.atlassian.net/browse/QTBUG-151397) qmllint warnings (id-shadows-member) in Qt Quick 3D's
OIT example
* [QTBUG-151610](https://qt-project.atlassian.net/browse/QTBUG-151610) Crash when using ExtendedSceneEnvironment's lightProbe
on OpenGL and AMD graphics card
* [QTBUG-145125](https://qt-project.atlassian.net/browse/QTBUG-145125) QSSGRenderUserPass uses QHash with const char* keys
* [QTBUG-151940](https://qt-project.atlassian.net/browse/QTBUG-151940) QQuickWindow::releaseResources() leaks about half of the
same-size QQuick3DTextureData textures (QSSGBufferManager::clear() skips
QHash entries)
* [QTBUG-145979](https://qt-project.atlassian.net/browse/QTBUG-145979) Document SSGI capabilities in Qt Quick 3D Overview pages
* [QTBUG-138669](https://qt-project.atlassian.net/browse/QTBUG-138669) Increased ram usage on every window resize
* [QTBUG-150709](https://qt-project.atlassian.net/browse/QTBUG-150709) Visibility changes to models in different layers does
not always work
* [QTBUG-151294](https://qt-project.atlassian.net/browse/QTBUG-151294) QtConcurrent::run() never runs its task when Qt is built
without thread support

### qt5compat
* [QTBUG-150303](https://qt-project.atlassian.net/browse/QTBUG-150303) [REG Qt 5→6] Potential deadlock d/t -fno-exceptions
[Qt5Support]

### qtcoap
* [QTBUG-151973](https://qt-project.atlassian.net/browse/QTBUG-151973) tst_QCoapClient::initTestCase()
'waitForHost(QUrl{timeServerUrl()}, QtCoap::SecurityMode::Certificate)'
returned FALSE.

### qtmqtt
* [QTBUG-149866](https://qt-project.atlassian.net/browse/QTBUG-149866) Implement checks for Maximum Packet and Buffer Sizes
* [QTBUG-150345](https://qt-project.atlassian.net/browse/QTBUG-150345) The Qt Mqtt app can freeze for 30 seconds when
disconnecting or closing

### qtopcua
* [QTBUG-151032](https://qt-project.atlassian.net/browse/QTBUG-151032) SBOM: open62541 PURL and CPE carry a doubled or stray
"v" (@vv1.5.7)

### qthttpserver
* [QTBUG-150270](https://qt-project.atlassian.net/browse/QTBUG-150270) Fix unbounded chunk-size/chunk-extension line
accumulation in QHttpServerParser
* [QTBUG-150274](https://qt-project.atlassian.net/browse/QTBUG-150274) Fix chunked body-size gate integer overflow
* [QTBUG-150275](https://qt-project.atlassian.net/browse/QTBUG-150275) Fix Content-Length quint64->qint64 wrap

### qtquick3dphysics
* [QTBUG-151719](https://qt-project.atlassian.net/browse/QTBUG-151719) Incorrect .qch namespace for QtQuick 3D Physics doc
package
* [QTBUG-151188](https://qt-project.atlassian.net/browse/QTBUG-151188) Qt Quick 3D Physics: memory leak on TriangleMeshShape
destruction
* [QTBUG-151976](https://qt-project.atlassian.net/browse/QTBUG-151976)  qt/tqtc-qtquick3dphysics: building sources fails on
webassembly-windows
* [QTBUG-151206](https://qt-project.atlassian.net/browse/QTBUG-151206) [REG 6.12.0->6.13.0 ff] quick3dphysics examples not
compiling on wasm_singlethread

### qtgrpc
* [QTBUG-149955](https://qt-project.atlassian.net/browse/QTBUG-149955) Protobuf-based parser gets nullopt instead of 0
* [QTBUG-150065](https://qt-project.atlassian.net/browse/QTBUG-150065)  qtprotobufgen generates uncompilable code for fields
named after C++20 keywords
* [QTBUG-150055](https://qt-project.atlassian.net/browse/QTBUG-150055) qtprotobufgen generates uncompilable code for proto2
group fields
* [QTBUG-151627](https://qt-project.atlassian.net/browse/QTBUG-151627) Memory growth regularly observed with Qt GRPC during
long run
* [QTBUG-151064](https://qt-project.atlassian.net/browse/QTBUG-151064) [QtProtobuf] Add configurable maximum message size at
(de)serializer level

### qtgraphs
* [QTBUG-146023](https://qt-project.atlassian.net/browse/QTBUG-146023) Gap appears is value axes when some series have axes and
others don't
* [QTBUG-150068](https://qt-project.atlassian.net/browse/QTBUG-150068) grid lines and axis ticks are misaligned with the data
after changing ValueAxis.zoom
* [QTBUG-150973](https://qt-project.atlassian.net/browse/QTBUG-150973) QLogValueAxis (QtGraphs 6.12) accepts invalid ranges,
zoom and base, and propagates NaN/Inf into visualMin/visualMax
* [QTBUG-150986](https://qt-project.atlassian.net/browse/QTBUG-150986) QCustomSeriesCanvasRenderer::canvasPaint is not
documented
* [QTBUG-148070](https://qt-project.atlassian.net/browse/QTBUG-148070) Graphs2D: QValueAxis labelFormat fails with any integer
format
* [QTBUG-150641](https://qt-project.atlassian.net/browse/QTBUG-150641) GraphsView: ValueAxis titleText overlaps tick labels
* [QTBUG-151362](https://qt-project.atlassian.net/browse/QTBUG-151362) Add/Remove Pie Series removes multiple series  at once
* [QTBUG-151626](https://qt-project.atlassian.net/browse/QTBUG-151626) Static build: Qt6Graphs package not found,
Qt6::Graphs2DImpl missing from Qt6GraphsDependencies.cmake
* [QTBUG-147936](https://qt-project.atlassian.net/browse/QTBUG-147936) CanvasPainter backend draws custom shader bars wrongly
* [QTBUG-143546](https://qt-project.atlassian.net/browse/QTBUG-143546) Setting angleSpanVisibleLimit inside PieSeries
declaratively does not work
* [QTBUG-151774](https://qt-project.atlassian.net/browse/QTBUG-151774) QCustomSeriesCanvasRenderer documentation page is not
under Graphs2D
* [QTBUG-149245](https://qt-project.atlassian.net/browse/QTBUG-149245) XYModelMapper crashes with SplineSeries

### qtopenapi
* [QTBUG-149429](https://qt-project.atlassian.net/browse/QTBUG-149429) Replace quoted includes with angle-bracket includes in
OpenAPI public headers
* [QTBUG-151989](https://qt-project.atlassian.net/browse/QTBUG-151989) Fix Axivion build issue in qt-openapi-generator-common

### qtapplicationmanager (Commercial only)
* [QTBUG-150642](https://qt-project.atlassian.net/browse/QTBUG-150642) CMake Error, applicationmanager/application-features
* [QTBUG-151035](https://qt-project.atlassian.net/browse/QTBUG-151035) SBOM: bundled libdbus PURL
pkg:github/d-bus/dbus@dbus-1.15.9 does not resolve, and no CPE is
declared
* [QTBUG-150312](https://qt-project.atlassian.net/browse/QTBUG-150312) tst_windowitem_multi-process (Failed)

### qmlcompilerplus (Commercial only)
* [QTBUG-134790](https://qt-project.atlassian.net/browse/QTBUG-134790) QML AnchorChanges do not compile in strict mode

Known Issues
------------
* Check that your system meets Qt's requirements:
  https://doc-snapshots.qt.io/qt6-6.12/supported-platforms.html
* RTA reported issues from Qt 6.12
  https://qt-project.atlassian.net/issues/?filter=24555
* See Qt 6.12 known issues from:
  https://wiki.qt.io/Qt_6.12_Known_Issues
* Qt 6.12.1 Open issues in Jira:
  https://qt-project.atlassian.net/issues/?filter=24684

Credits for the release goes to:
---------------------------------

* Eirik Aavitsland
* Cristian Adam
* Laszlo Agocs
* Dilek Akcay
* Owais Akhtar
* Dmitrii Akshintsev
* Albert Astals Cid
* Andreas Bacher
* Mate Barany
* Yuri Barreira
* Andreas Belke
* Vladimir Belyavsky
* Nicholas Bennett
* Lena Biliaieva
* Tim Blechmann
* Eskil Abrahamsen Blomfeldt
* Ana Bobillo
* David Boddie
* Tatiana Borisova
* Joerg Bornemann
* Rym Bouabid
* Assam Boudjelthia
* Taylor Braun-Jones
* Aurélien Brooke
* Alex Bu
* Oswald Buddenhagen
* Olivier De Cannière
* Méven Car
* Alexei Cazacov
* Jean-Michaël Celerier
* Zbigniew Chyla
* Alexandru Croitor
* Mitch Curtis
* Giuseppe D'Angelo
* Alexey Edelev
* David Edmundson
* Oliver Eftevaag
* Christian Ehrlicher
* Hatem ElKharashy
* Kim Eojin
* David Faure
* Nicolas Fella
* Andrey Filipenkov
* Simo Fält
* Gabriel Gazzán
* Guy Git
* Frederik Gladhorn
* Julian Greilich
* Robert Griebl
* Jan Grulich
* Kaj Grönholm
* Richard Moe Gustavsen
* Mikko Hallamaa
* Stian Halseth
* Carsten Hartenfels
* Andre Hartmann
* Andreas Hartmetz
* Jani Heikkinen
* Jeff Heller
* Ulf Hermann
* Volker Hilsheimer
* Dominik Holland
* Samuli Hölttä
* Linus Jahn
* Morteza Jamshidi
* Allan Sandfeld Jensen
* Jukka Jokiniva
* Jonas Karlsson
* Dmitry Kazakov
* Igor Khanin
* Dennis Kim
* Friedemann Kleint
* Michal Klocek
* Seokha Ko
* Jarek Kobus
* Kai Koehne
* Sze Howe Koh
* Jarkko Koivikko
* Antti Kokko
* Eitan Korh
* Fabian Kosmale
* Adam Krzykala
* Santhosh Kumar
* Kai Köhne
* Eric Larson
* Inho Lee
* Frédéric Lefebvre
* Paul Lemire
* Denis Letov
* Shane Liu
* Jie Liu
* Shawn Luo
* Robert Löhning
* Thiago Macieira
* Olaf Mandel
* Jan Moeller
* Baurzhan Muftakhidinov
* Marc Mutz
* Antti Määttä
* Andy Nichols
* Iason Nikolas
* Przemyslaw Nogaj
* Mårten Nordheim
* Evgeniy Nuromskiy
* Dennis Oberst
* Sukyoung Oh
* Matti Paaso
* Kwanghyo Park
* Jerome Pasion
* Mauro Persano
* Yauheni Pervenenka
* Karim Pinter
* Lauri Pohjanheimo
* Joni Poikelin
* Lorn Potter
* Dheerendra Purohit
* Liang Qi
* Daniel Campos Ramos
* David Redondo
* Arno Rehn
* Topi Reinio
* Jianquan Ren
* Hannah von Reth
* Will Rose
* Shawn Rutledge
* Volodymyr Samokhatko
* Timon Sassor
* Simon Schmeisser
* SanthoshKumar Selvaraj
* Thomas Senyk
* Sami Shalayel
* Tian Shilin
* Venugopal Shivashankar
* Nils Peter Skålerud
* Nils Petter Skålerud
* Ivan Solovev
* Axel Spoerl
* Magdalena Stojek
* Christian Strømme
* Yuan Su
* Tarja Sundqvist
* Jan Arve Sæther
* Morten Sørvig
* Sadegh Taghavi
* John Thacker
* Marcus Tillmanns
* Zhang Tingan
* Elias Toivola
* Sami Varanka
* Doris Verria
* Tor Arne Vestbø
* Xiaohan Wang
* Aleksander Wawrzyniak
* Michael Weghorn
* Bernd Weimer
* Edward Welbourne
* Paul Wicking
* Bernhard M. Wiedemann
* Szymon Wojtach
* Oliver Wolff
* Cai Xiangrong
* Haozhe Xie
* Semih Yavuz
* Zhao Yuhang
* Zhang Yunzhe
* Sol ZHu
* Arkadiusz Zarębski
* Kun Zhang
* Liu Zheng
* Bohan Zhou
* Wang Zichong
* Eike Ziller
* İsa Tunahan Öztürk
* Dawid Śliwa
