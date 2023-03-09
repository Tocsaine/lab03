lab03

Основные команды:

cmake_minimum_required(VERSION 3.22.1) - задает минимальную версию утилиты для сборки
project (name) - задает название проекту
set(CMAKE_CXX_COMPILER dir) - задает компиллятор

Создание и структура библиотек:
создаем директорию библиотеки (к примеру, formatter_lib)
Далее в нем создаем директорию d, в которую помещаем хедер и .cpp файл библиотеки
после этого в директории библиотеки создаем директорию prep
nano CMakeLists.txt
Прописываем Cmake
после этого в папке prep пишем следующе
1. cmake ..
2. make (cmake --build .)

part 1

cmake_minimum_required(VERSION 3.22.1)
set(CMAKE_CXX_COMPILER "/usr/bin/g++")
project(formatter_lib)
set(Formation ~/formatter_lib/d/formatter.cpp)
add_library(formatter_lib STATIC ${Formation})

part 2

cmake_minimum_required(VERSION 3.22.1)
set(CMAKE_CXX_COMPILER "/usr/bin/g++")
project(formatter_ex_lib)
set(Formation_ex ~/formatter_ex_lib/d/formatter_ex.cpp)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib formatter_lib_dir)
add_library(formatter_ex_lib STATIC ${Formation_ex})
target_include_directories(formatter_ex_lib PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib/d)

target_link_libraries(formatter_ex_lib formatter_lib)

part 3

hello_world_app:

cmake_minimum_required(VERSION 3.22.1)
set(CMAKE_CXX_COMPILER "/usr/bin/g++")
project(hello_world)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib formatetr_ex_lib_dir)
add_executable(hello_world ${CMAKE_CURRENT_SOURCE_DIR}/hello_world.cpp)
target_include_directories(hello_world PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib/d)
target_link_libraries(hello_world formatter_ex_lib)

Solver:

cmake_minimum_required(VERSION 3.22.1)
set(CMAKE_CXX_COMPILER "/usr/bin/g++")
project(solver)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib formatter_ex_lib_dir)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../solver_lib solver_lib_dir)
add_executable(solver "~/solver/d/equation.cpp")
target_include_directories(solver PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib/d ${CMAKE_CURRENT_SOURCE_DIR}/../solver_lib/d)
target_link_libraries(solver formatter_ex_lib solver_lib)

