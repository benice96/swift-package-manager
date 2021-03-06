# This source file is part of the Swift.org open source project
#
# Copyright (c) 2014 - 2019 Apple Inc. and the Swift project authors
# Licensed under Apache License v2.0 with Runtime Library Exception
#
# See http://swift.org/LICENSE.txt for license information
# See http://swift.org/CONTRIBUTORS.txt for Swift project authors

add_library(TSCBasic
  Await.swift
  ByteString.swift
  CacheableSequence.swift
  CodableResult.swift
  CollectionAlgorithms.swift
  CollectionExtensions.swift
  Condition.swift
  CStringArray.swift
  DeltaAlgorithm.swift
  DiagnosticsEngine.swift
  DictionaryExtensions.swift
  DictionaryLiteralExtensions.swift
  EditDistance.swift
  FileInfo.swift
  FileSystem.swift
  GraphAlgorithms.swift
  JSON.swift
  JSONMapper.swift
  KeyedPair.swift
  LazyCache.swift
  Lock.swift
  misc.swift
  OSLog.swift
  ObjectIdentifierProtocol.swift
  OrderedDictionary.swift
  OrderedSet.swift
  OutputByteStream.swift
  Path.swift
  PathShims.swift
  Process.swift
  ProcessEnv.swift
  ProcessSet.swift
  RegEx.swift
  Result.swift
  SHA256.swift
  SortedArray.swift
  StringConversions.swift
  SynchronizedQueue.swift
  TemporaryFile.swift
  TerminalController.swift
  Thread.swift
  Tuple.swift)
target_link_libraries(TSCBasic PUBLIC
  TSCLibc)
# NOTE(compnerd) workaround for CMake not setting up include flags yet
set_target_properties(TSCBasic PROPERTIES
  INTERFACE_INCLUDE_DIRECTORIES ${CMAKE_Swift_MODULE_DIRECTORY})


if(CMAKE_SYSTEM_NAME STREQUAL Windows)
install(TARGETS TSCBasic
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin)
endif()

# Don't use GNU strerror_r on Android.
if(CMAKE_SYSTEM_NAME STREQUAL Android)
  target_compile_options(TSCBasic PUBLIC "SHELL:-Xcc -U_GNU_SOURCE")
endif()

set_property(GLOBAL APPEND PROPERTY TSC_EXPORTS TSCBasic)
