cmake_minimum_required(VERSION 2.8.8)
#
# The KenLM cmake files make use of add_library(... OBJECTS ...)
# 
# This syntax allows grouping of source files when compiling
# (effectively creating "fake" libraries based on source subdirs).
# 
# This syntax was only added in cmake version 2.8.8
#
# see http://www.cmake.org/Wiki/CMake/Tutorials/Object_Library


# This CMake file was created by Lane Schwartz <dowobeha@gmail.com>

# Explicitly list the source files for this subdirectory
#
# If you add any source files to this subdirectory
#    that should be included in the kenlm library,
#        (this excludes any unit test files)
#    you should add them to the following list:
#
# In order to allow CMake files in the parent directory
#    to see this variable definition, we set PARENT_SCOPE.
#
# In order to set correct paths to these files
#    when this variable is referenced by CMake files in the parent directory,
#    we prefix all files with ${CMAKE_CURRENT_SOURCE_DIR}.
#
set(KENLM_UTIL_STREAM_SOURCE 
		${CMAKE_CURRENT_SOURCE_DIR}/chain.cc
		${CMAKE_CURRENT_SOURCE_DIR}/io.cc
		${CMAKE_CURRENT_SOURCE_DIR}/line_input.cc
		${CMAKE_CURRENT_SOURCE_DIR}/multi_progress.cc
		${CMAKE_CURRENT_SOURCE_DIR}/rewindable_stream.cc
	PARENT_SCOPE)



if(BUILD_TESTING)
  # Explicitly list the Boost test files to be compiled
  set(KENLM_BOOST_TESTS_LIST
    io_test
    sort_test
    stream_test
  )

  AddTests(TESTS ${KENLM_BOOST_TESTS_LIST}
           DEPENDS $<TARGET_OBJECTS:kenlm_util>
           LIBRARIES ${Boost_LIBRARIES} pthread)
endif()
