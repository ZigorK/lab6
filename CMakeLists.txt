cmake_minimum_required(VERSION 3.10)

# Установка версии проекта
set(PATCH_VERSION "1" CACHE INTERNAL "Patch version")
set(PROJECT_VERSION 0.0.${PATCH_VERSION})
project(lab6 VERSION ${PROJECT_VERSION})

# Добавление исполняемого файла
add_executable(lab6 main.cpp Document.h Primitive.h DocumentController.h)

# Установка стандарта C++
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Настройка флагов компилятора
if (CMAKE_CXX_COMPILER_ID STREQUAL "MSVC")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /std:c++17")
else()
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++17")
endif()

# Установка путей для инсталляции
install(TARGETS lab6 DESTINATION bin)

# Настройка CPack
set(CPACK_GENERATOR "DEB;productbuild") # Используем DEB для Linux и productbuild для macOS
set(CPACK_PACKAGE_VERSION "${PROJECT_VERSION}")
set(CPACK_PACKAGE_NAME "lab6")
set(CPACK_PACKAGE_DESCRIPTION "Описание вашего проекта")
set(CPACK_PACKAGE_VENDOR "Ваше имя или компания")
set(CPACK_PACKAGE_CONTACT "Ваш контактный email")

# Дополнительная конфигурация для DEB
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Ваше имя или email")
set(CPACK_DEBIAN_PACKAGE_SECTION "utils")
set(CPACK_DEBIAN_PACKAGE_PRIORITY "optional")
set(CPACK_DEBIAN_PACKAGE_ARCHITECTURE "amd64")

# Дополнительная конфигурация для macOS (productbuild)
set(CPACK_PRODUCTBUILD_PRODUCT "com.yourcompany.lab6")
set(CPACK_PRODUCTBUILD_IDENTITY "Developer ID Installer: Your Name (Team ID)") # Замените на ваш идентификатор разработчика
set(CPACK_PRODUCTBUILD_BUNDLE_ID "com.yourcompany.lab6")
set(CPACK_PRODUCTBUILD_SIGNING_IDENTITY "") # Укажите идентификатор подписи, если необходимо

include(CPack)
