#PROJECT(QEDISSERVER)

INCLUDE(${PROJECT_SOURCE_DIR}/CMakeCommon)

AUX_SOURCE_DIRECTORY(. QEDISSERVER_SRC)

LINK_DIRECTORIES(../../leveldb)
LINK_DIRECTORIES(../../rocksdb)
INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR}/QBase; ${PROJECT_SOURCE_DIR}/QedisCore)

ADD_EXECUTABLE(qedis_server ${QEDISSERVER_SRC})
SET(EXECUTABLE_OUTPUT_PATH  ../../bin)

TARGET_LINK_LIBRARIES(qedis_server qediscore; qbaselib; leveldb; rocksdb)
ADD_DEPENDENCIES(qedis_server qbaselib; qediscore; leveldb; rocksdb)
IF(${QEDIS_CLUSTER} EQUAL 1)
    INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR}/QSentinel)
    TARGET_LINK_LIBRARIES(qedis_server qcluster)
    ADD_DEPENDENCIES(qedis_server qcluster)
ENDIF()

