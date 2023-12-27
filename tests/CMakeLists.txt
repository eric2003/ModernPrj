
include(FetchContent)

FetchContent_Declare(
  googletest
  GIT_REPOSITORY https://github.com/google/googletest.git
  GIT_TAG        release-1.12.0
)
FetchContent_MakeAvailable(googletest)

include(GoogleTest)

function ( ADD_MYTEST_EXE filename )
  add_executable( ${filename}
    ${filename}.cc
  )
  
  target_link_libraries( ${filename}
    PRIVATE
      GTest::gtest_main
      GTest::gmock
  )
  
  if ( MSVC )
    target_compile_options( ${filename}
      PRIVATE
        /bigobj
    )
  endif()
  gtest_discover_tests( ${filename} )
endfunction()

set ( H5_TESTS
  gmock-port_test
  gmock_test
)

foreach ( my_test ${H5_TESTS})
  ADD_MYTEST_EXE( ${my_test} )
endforeach ()




