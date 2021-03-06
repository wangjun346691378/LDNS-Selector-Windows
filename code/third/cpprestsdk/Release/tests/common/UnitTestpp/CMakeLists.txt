include_directories(${Casablanca_INCLUDE_DIR} src .)

set(UT_SOURCES
  src/AssertException.cpp
  src/CompositeTestReporter.cpp
  src/CurrentTest.cpp
  src/DeferredTestReporter.cpp
  src/DeferredTestResult.cpp
  src/GlobalSettings.cpp
  src/MemoryOutStream.cpp
  src/ReportAssert.cpp
  src/Test.cpp
  src/TestDetails.cpp
  src/TestList.cpp
  src/TestReporter.cpp
  src/TestReporterStdout.cpp
  src/TestResults.cpp
  src/TestRunner.cpp
  src/XmlTestReporter.cpp
  )

set(TEST_SOURCES
  src/tests/TestAssertHandler.cpp
  src/tests/TestCheckMacros.cpp
  src/tests/TestChecks.cpp
  src/tests/TestCompositeTestReporter.cpp
  src/tests/TestCurrentTest.cpp
  src/tests/TestDeferredTestReporter.cpp
  src/tests/TestMemoryOutStream.cpp
  src/tests/TestTest.cpp
  src/tests/TestTestList.cpp
  src/tests/TestTestMacros.cpp
  src/tests/TestTestResults.cpp
  src/tests/TestTestRunner.cpp
  src/tests/TestTestSuite.cpp
  src/tests/TestUnitTestPP.cpp
  src/tests/TestXmlTestReporter.cpp
  )

if(UNIX)
  set(UT_SOURCES ${UT_SOURCES}
    src/Posix/SignalTranslator.cpp
    src/Posix/TimeHelpers.cpp
    )
elseif(WIN32)
  set(UT_SOURCES ${UT_SOURCES} src/Win32/TimeHelpers.cpp)

  add_definitions(-DWIN32 -D_USRDLL -D_CRT_SECURE_NO_DEPRECATE -DUNITTEST_DLL_EXPORT)
endif()

add_library(${LIB}unittestpp ${UT_SOURCES})
target_link_libraries(${LIB}unittestpp ${ANDROID_STL_FLAGS})