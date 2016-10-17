# Sets the minimum version of CMake required to build the native
# library. You should either keep the default value or only pass a
# value of 3.4.0 or lower.

cmake_minimum_required(VERSION 3.4.1)

# Creates and names a library, sets it as either STATIC
# or SHARED, and provides the relative paths to its source code.
# You can define multiple libraries, and CMake builds it for you.
# Gradle automatically packages shared libraries with your APK.

add_library( # Sets the name of the library.
             native-lib

             # Sets the library as a shared library.
             SHARED

             # Provides a relative path to your source file(s).
             # Associated headers in the same location as their source
             # file are automatically included.
             src/main/cpp/native-lib.cpp )

# Searches for a specified prebuilt library and stores the path as a
# variable. Because system libraries are included in the search path by
# default, you only need to specify the name of the public NDK library
# you want to add. CMake verifies that the library exists before
# completing its build.

find_library( # Sets the name of the path variable.
              log-lib

              # Specifies the name of the NDK library that
              # you want CMake to locate.
              log )

# Specifies libraries CMake should link to your target library. You
# can link multiple libraries, such as libraries you define in the
# build script, prebuilt third-party libraries, or system libraries.

target_link_libraries( # Specifies the target library.
                       native-lib

                       # Links the target library to the log library
                       # included in the NDK.
                       ${log-lib} )

set ( ROOT_DIR src/main/cpp )
############# DeflatingDecompressor #############

add_library( DeflatingDecompressor-v3
             SHARED
             ${ROOT_DIR}/DeflatingDecompressor/DeflatingDecompressor.cpp )

find_library( z-lib
              z )

target_link_libraries( DeflatingDecompressor-v3
                        ${z-lib})

############# LineBreak-v2 #############

add_library( LineBreak-v2
             SHARED
              ${ROOT_DIR}/LineBreak/LineBreaker.cpp  ${ROOT_DIR}/LineBreak/liblinebreak-2.0/linebreak.c  ${ROOT_DIR}/LineBreak/liblinebreak-2.0/linebreakdata.c  ${ROOT_DIR}/LineBreak/liblinebreak-2.0/linebreakdef.c )

target_link_libraries( LineBreak-v2 )


############# expat #############

set( EXPAT_DIR  ${ROOT_DIR}/expat-2.0.1 )

add_library( expat
             SHARED
			 ${EXPAT_DIR}/lib/xmlparse.c ${EXPAT_DIR}/lib/xmlrole.c ${EXPAT_DIR}/lib/xmltok.c )

include_directories ( ${EXPAT_DIR})
include_directories ( ${EXPAT_DIR}/lib)

target_link_libraries( expat )

############# NativeFormats #############

add_library( NativeFormats-v4
             SHARED
			${ROOT_DIR}/NativeFormats/main.cpp
			${ROOT_DIR}/NativeFormats/JavaNativeFormatPlugin.cpp
			${ROOT_DIR}/NativeFormats/JavaPluginCollection.cpp
			${ROOT_DIR}/NativeFormats/util/AndroidUtil.cpp
			${ROOT_DIR}/NativeFormats/util/JniEnvelope.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/constants/ZLXMLNamespace.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/drm/FileEncryptionInfo.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/encoding/DummyEncodingConverter.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/encoding/Utf16EncodingConverters.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/encoding/Utf8EncodingConverter.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/encoding/JavaEncodingConverter.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/encoding/ZLEncodingCollection.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/encoding/ZLEncodingConverter.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/filesystem/ZLDir.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/filesystem/ZLFSManager.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/filesystem/ZLFile.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/filesystem/ZLInputStreamDecorator.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/filesystem/zip/ZLGzipInputStream.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/filesystem/zip/ZLZDecompressor.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/filesystem/zip/ZLZipDir.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/filesystem/zip/ZLZipEntryCache.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/filesystem/zip/ZLZipHeader.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/filesystem/zip/ZLZipInputStream.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/language/ZLCharSequence.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/language/ZLLanguageDetector.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/language/ZLLanguageList.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/language/ZLLanguageMatcher.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/language/ZLStatistics.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/language/ZLStatisticsGenerator.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/language/ZLStatisticsItem.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/language/ZLStatisticsXMLReader.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/library/ZLibrary.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/logger/ZLLogger.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/util/ZLFileUtil.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/util/ZLLanguageUtil.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/util/ZLStringUtil.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/util/ZLUnicodeUtil.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/xml/ZLAsynchronousInputStream.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/xml/ZLPlainAsynchronousInputStream.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/xml/ZLXMLReader.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/xml/expat/ZLXMLReaderInternal.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/unix/filesystem/ZLUnixFSDir.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/unix/filesystem/ZLUnixFSManager.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/unix/filesystem/ZLUnixFileInputStream.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/unix/filesystem/ZLUnixFileOutputStream.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/core/src/unix/library/ZLUnixLibrary.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/text/src/model/ZLCachedMemoryAllocator.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/text/src/model/ZLTextModel.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/text/src/model/ZLTextParagraph.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/text/src/model/ZLTextStyleEntry.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/text/src/model/ZLVideoEntry.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/text/src/fonts/FontManager.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/text/src/fonts/FontMap.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/ui/src/android/filesystem/JavaFSDir.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/ui/src/android/filesystem/JavaInputStream.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/ui/src/android/filesystem/ZLAndroidFSManager.cpp
			${ROOT_DIR}/NativeFormats/zlibrary/ui/src/android/library/ZLAndroidLibraryImplementation.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/bookmodel/BookModel.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/bookmodel/BookReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/EncodedTextReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/FormatPlugin.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/PluginCollection.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/fb2/FB2BookReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/fb2/FB2CoverReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/fb2/FB2MetaInfoReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/fb2/FB2Plugin.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/fb2/FB2Reader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/fb2/FB2TagManager.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/fb2/FB2UidReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/css/CSSInputStream.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/css/CSSSelector.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/css/StringInputStream.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/css/StyleSheetParser.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/css/StyleSheetTable.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/css/StyleSheetUtil.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/html/HtmlBookReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/html/HtmlDescriptionReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/html/HtmlEntityCollection.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/html/HtmlPlugin.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/html/HtmlReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/html/HtmlReaderStream.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/oeb/NCXReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/oeb/OEBBookReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/oeb/OEBCoverReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/oeb/OEBEncryptionReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/oeb/OEBMetaInfoReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/oeb/OEBPlugin.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/oeb/OEBSimpleIdReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/oeb/OEBTextStream.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/oeb/OEBUidReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/oeb/OPFReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/oeb/XHTMLImageFinder.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/pdb/BitReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/pdb/DocDecompressor.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/pdb/HtmlMetainfoReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/pdb/HuffDecompressor.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/pdb/MobipocketHtmlBookReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/pdb/MobipocketPlugin.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/pdb/PalmDocLikePlugin.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/pdb/PalmDocLikeStream.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/pdb/PalmDocStream.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/pdb/PdbPlugin.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/pdb/PdbReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/pdb/PdbStream.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/pdb/SimplePdbPlugin.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/rtf/RtfBookReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/rtf/RtfDescriptionReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/rtf/RtfPlugin.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/rtf/RtfReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/rtf/RtfReaderStream.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/txt/PlainTextFormat.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/txt/TxtBookReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/txt/TxtPlugin.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/txt/TxtReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/util/EntityFilesCollector.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/util/MergedStream.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/util/MiscUtil.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/util/XMLTextStream.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/xhtml/XHTMLReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/xhtml/XHTMLTagInfo.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/doc/DocBookReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/doc/DocMetaInfoReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/doc/DocPlugin.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/doc/DocStreams.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/doc/OleMainStream.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/doc/OleStorage.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/doc/OleStream.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/doc/OleStreamParser.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/doc/OleStreamReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/doc/OleUtil.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/doc/DocInlineImageReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/doc/DocFloatImageReader.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/formats/doc/DocAnsiConverter.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/library/Author.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/library/Book.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/library/Comparators.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/library/Tag.cpp
			${ROOT_DIR}/NativeFormats/fbreader/src/library/UID.cpp )

include_directories ( ${ROOT_DIR}/NativeFormats/util
            ${ROOT_DIR}/NativeFormats/zlibrary/core/src/constants
            ${ROOT_DIR}/NativeFormats/zlibrary/core/src/drm
            ${ROOT_DIR}/NativeFormats/zlibrary/core/src/encoding
            ${ROOT_DIR}/NativeFormats/zlibrary/core/src/filesystem
            ${ROOT_DIR}/NativeFormats/zlibrary/core/src/image
            ${ROOT_DIR}/NativeFormats/zlibrary/core/src/language
            ${ROOT_DIR}/NativeFormats/zlibrary/core/src/library
            ${ROOT_DIR}/NativeFormats/zlibrary/core/src/logger
            ${ROOT_DIR}/NativeFormats/zlibrary/core/src/util
            ${ROOT_DIR}/NativeFormats/zlibrary/core/src/xml
            ${ROOT_DIR}/NativeFormats/zlibrary/text/src/model
            ${ROOT_DIR}/NativeFormats/zlibrary/text/src/fonts )

target_link_libraries( NativeFormats-v4
						${z-lib} ${log-lib} expat)