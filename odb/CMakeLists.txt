set(CURRENT_TARGET odb)

list(APPEND CURRENT_TARGET_INCLUDES
    ${PROJECT_SOURCE_DIR}
    )

list(APPEND CURRENT_TARGET_UNGROUPED_HEADERS
    cache-traits.hxx
    callback.hxx
    connection.hxx
    container-traits.hxx
    core.hxx
    database.hxx
    exception.hxx
    forward.hxx
    function-table.hxx
    lazy-pointer-traits.hxx
    lazy-ptr.hxx
    lazy-ptr-impl.hxx
    nested-container.hxx
    no-id-object-result.hxx
    no-op-cache-traits.hxx
    nullable.hxx
    object-result.hxx
    pointer-traits.hxx
    polymorphic-info.hxx
    polymorphic-map.hxx
    polymorphic-object-result.hxx
    post.hxx
    pre.hxx
    prepared-query.hxx
    query-dynamic.hxx
    query.hxx
    result.hxx
    schema-catalog.hxx
    schema-catalog-impl.hxx
    schema-version.hxx
    section.hxx
    session.hxx
    simple-object-result.hxx
    statement.hxx
    statement-processing-common.hxx
    std-array-traits.hxx
    std-deque-traits.hxx
    std-forward-list-traits.hxx
    std-list-traits.hxx
    std-map-traits.hxx
    std-set-traits.hxx
    std-unordered-map-traits.hxx
    std-unordered-set-traits.hxx
    std-vector-traits.hxx
    tracer.hxx
    traits.hxx
    transaction.hxx
    vector.hxx
    vector-impl.hxx
    vector-traits.hxx
    version.hxx
    view-image.hxx
    view-result.hxx
    wrapper-traits.hxx
    )

list(APPEND CURRENT_TARGET_DETAILS_HEADERS
    details/buffer.hxx
    details/condition.hxx
    details/config.hxx
    details/c-string.hxx
    details/exception.hxx
    details/export.hxx
    details/function-wrapper.hxx
    details/lock.hxx
    details/mutex.hxx
    details/shared-ptr-fwd.hxx
    details/shared-ptr.hxx
    details/thread.hxx
    details/tls.hxx
    details/transfer-ptr.hxx
    details/type-info.hxx
    details/unique-ptr.hxx
    details/unused.hxx
    details/wrapper-p.hxx
    )

list(APPEND CURRENT_TARGET_DETAILS_META_HEADERS
    details/meta/answer.hxx
    details/meta/class-p.hxx
    details/meta/polymorphic-p.hxx
    details/meta/remove-const.hxx
    details/meta/remove-const-volatile.hxx
    details/meta/remove-pointer.hxx
    details/meta/remove-volatile.hxx
    details/meta/static-assert.hxx
    )

list(APPEND CURRENT_TARGET_DETAILS_SHARED_PTR_HEADERS
    details/shared-ptr/base.hxx
    details/shared-ptr/counter-type.hxx
    details/shared-ptr/exception.hxx
    )

list(APPEND CURRENT_TARGET_DETAILS_WIN32_HEADERS
    details/win32/windows.hxx
    details/win32/condition.hxx
    details/win32/exceptions.hxx
    details/win32/init.hxx
    details/win32/mutex.hxx
    details/win32/once.hxx
    details/win32/once-init.hxx
    details/win32/thread.hxx
    details/win32/tls.hxx
    details/win32/tls-init.hxx
    )

list(APPEND CURRENT_TARGET_DETAILS_POSIX_HEADERS
    details/posix/condition.hxx
    details/posix/exceptions.hxx
    details/posix/mutex.hxx
    details/posix/thread.hxx
    details/posix/tls.hxx
    )

list(APPEND CURRENT_TARGET_UNGROUPED_SOURCES
    connection.cxx
    connection.ixx
    connection.txx
    database.cxx
    database.ixx
    database.txx
    exceptions.cxx
    lazy-ptr.ixx
    lazy-ptr.txx
    lazy-ptr-impl.ixx
    lazy-ptr-impl.txx
    no-id-object-result.txx
    polymorphic-map.ixx
    polymorphic-map.txx
    polymorphic-object-result.txx
    prepared-query.cxx
    query-dynamic.cxx
    query-dynamic.ixx
    query-dynamic.txx
    result.cxx
    result.txx
    schema-catalog.cxx
    section.cxx
    session.cxx
    session.ixx
    session.txx
    simple-object-result.txx
    statement.cxx
    statement-processing.cxx
    tracer.cxx
    transaction.ixx
    transaction.cxx
    vector.ixx
    vector-impl.ixx
    vector-impl.cxx
    vector-traits.txx
    view-result.txx
    )

list(APPEND CURRENT_TARGET_DETAILS_SOURCES
    details/buffer.cxx
    details/function-wrapper.ixx
    details/function-wrapper.txx
    )

list(APPEND CURRENT_TARGET_DETAILS_SHARED_PTR_SOURCES
    details/shared-ptr/base.cxx
    details/shared-ptr/base.ixx
    details/shared-ptr/base.txx
    )

list(APPEND CURRENT_TARGET_DETAILS_WIN32_SOURCES
    details/win32/condition.cxx
    details/win32/condition.ixx
    details/win32/exceptions.cxx
    details/win32/init.cxx
    details/win32/mutex.ixx
    details/win32/once.cxx
    details/win32/thread.cxx
    details/win32/tls.cxx
    details/win32/tls.ixx
    details/win32/tls.txx
    )

list(APPEND CURRENT_TARGET_DETAILS_POSIX_SOURCES
    details/posix/condition.ixx
    details/posix/exceptions.cxx
    details/posix/mutex.ixx
    details/posix/thread.cxx
    details/posix/thread.ixx
    details/posix/tls.txx
    details/posix/tls.ixx
    )

list(APPEND CURRENT_TARGET_HEADERS
    ${CURRENT_TARGET_UNGROUPED_HEADERS}
    ${CURRENT_TARGET_DETAILS_HEADERS}
    ${CURRENT_TARGET_DETAILS_META_HEADERS}
    ${CURRENT_TARGET_DETAILS_SHARED_PTR_HEADERS}
    )

list(APPEND CURRENT_TARGET_SOURCES
    ${CURRENT_TARGET_UNGROUPED_SOURCES}
    ${CURRENT_TARGET_DETAILS_SOURCES}
    ${CURRENT_TARGET_DETAILS_SHARED_PTR_SOURCES}
    )

if(UNIX OR APPLE)
    list(APPEND CURRENT_TARGET_HEADERS
        ${CURRENT_TARGET_DETAILS_POSIX_HEADERS}
        )

    list(APPEND CURRENT_TARGET_SOURCES
        ${CURRENT_TARGET_DETAILS_POSIX_SOURCES}
        )

    add_definitions(-DODB_THREADS_POSIX)
elseif(WIN32)
    if(BUILD_SHARED_LIBRARIES)
        list(APPEND CURRENT_TARGET_DETAILS_WIN32_SOURCES
            details/win32/dll.cxx
            )
    endif()
    list(APPEND CURRENT_TARGET_HEADERS
        ${CURRENT_TARGET_DETAILS_WIN32_HEADERS}
        )

    list(APPEND CURRENT_TARGET_SOURCES
        ${CURRENT_TARGET_DETAILS_WIN32_SOURCES}
        )

    add_definitions(-DODB_THREADS_WIN32)
endif()

if(BUILD_SHARED_LIBRARIES)
    add_library(${CURRENT_TARGET} SHARED
        ${CURRENT_TARGET_HEADERS}
        ${CURRENT_TARGET_SOURCES}
        )
else()
    add_library(${CURRENT_TARGET} STATIC
        ${CURRENT_TARGET_HEADERS}
        ${CURRENT_TARGET_SOURCES}
        )
endif()

include_directories(${CURRENT_TARGET_INCLUDES})

target_link_libraries(${CURRENT_TARGET} ${CURRENT_TARGET_LIBRARIES})

target_compile_options(${CURRENT_TARGET} PUBLIC $<$<COMPILE_LANGUAGE:C>:-Wall -Wextra -Wno-unused-function -Wno-unused-parameter -Werror-implicit-function-declaration -Wno-missing-braces -Wno-missing-field-initializers -std=gnu99 -fno-strict-aliasing>)

if(USE_LIBC++)
    target_compile_options(${CURRENT_TARGET} PUBLIC $<$<COMPILE_LANGUAGE:CXX>:-Wall -Wextra -Wno-unused-function -Wno-unused-parameter -Werror-implicit-function-declaration -Wno-missing-field-initializers -fno-strict-aliasing -std=gnu++14 -stdlib=libc++>)
else()
    target_compile_options(${CURRENT_TARGET} PUBLIC $<$<COMPILE_LANGUAGE:CXX>:-Wall -Wextra -Wno-unused-function -Wno-unused-parameter -Werror-implicit-function-declaration -Wno-missing-field-initializers -fno-strict-aliasing -std=gnu++14>)
endif()

target_compile_options(${CURRENT_TARGET} PUBLIC $<$<CONFIG:DEBUG>:-g>)

set_target_properties(${CURRENT_TARGET} PROPERTIES ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})
set_target_properties(${CURRENT_TARGET} PROPERTIES BINARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})
set_target_properties(${CURRENT_TARGET} PROPERTIES LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})

if(APPLE AND ARM_BUILD)
    set_target_properties(${CURRENT_TARGET} PROPERTIES XCODE_ATTRIBUTE_CODE_SIGN_IDENTITY ${APPLE_SIGN_IDENTITY})
endif()
