[![Build Status](https://travis-ci.org/desta-study/lab10.svg?branch=master)](https://travis-ci.org/desta-study/lab10)
the demo application redirects data from stdin to a file **log.txt** using a package **print**.


## Laboratory work X
Данная лабораторная работа посвещена изучению систем управления пакетами на примере **Hunter**

```ShellSession
$ open https://github.com/ruslo/hunter
```

## Tasks

- [X] 1. Создать публичный репозиторий с названием **lab10** на сервисе **GitHub**
- [X] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [X] 3. Выполнить инструкцию учебного материала
- [X] 4. Ознакомиться со ссылками учебного материала
- [X] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**


## Tutorial
Делаем первоначальные настройки, добавляя значения переменным окружения
```ShellSession
$ export GITHUB_USERNAME=<имя_пользователя>   #Устанавливаем значение переменной окружения GITHUB_USERNAME
$ export GITHUB_TOKEN=<сгенирированный_токен>   #Устанавливаем значение переменной окружения GITHUB_TOKEN
```
#### Устанавливаем hunter
```ShellSession
$ cd ${GITHUB_USERNAME}/workspace
$ pushd .
$ source scripts/activate
$ go get github.com/github/hub
```
#### Работа с конфигом hub
```ShellSession
$ mkdir ~/.config
$ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
$ git config --global hub.protocol https
```

#### Работа с пакетом девятой лабораторной работы, получение контрольной суммы пакета
```ShellSession
$ wget https://github.com/${GITHUB_USERNAME}/lab09/archive/v0.1.0.0.tar.gz  #Устанавливаем v0.1.0.0.tar.gz
$ export PRINT_SHA1=`openssl sha1 v0.1.0.0.tar.gz | cut -d'=' -f2 | cut -c2-41` #Экспортируем(04aa0c99724692f83d4b47404691e79c16fd5914)
$ echo $PRINT_SHA1  #Выводим контрольную сумму на экран консоли
$ rm -rf v0.1.0.0.tar.gz  #Удаляем v0.1.0.0.tar.gz
```
#### Работа с удаленным и локальным репозиторием Hunter
```ShellSession
$ git clone https://github.com/ruslo/hunter projects/hunter  #Клонируем удаленный репозиторий https://github.com/ruslo/hunter в projects/hunter
$ cd projects/hunter && git checkout v0.19.137    #Меняем директорию на projects/hunter и переключаемся на ветвь v0.19.137
$ git remote show   #Выводим branches в консоль
$ hub fork    #Форкаем репозиторий
$ git remote show   #Выводим branches в консоль
$ git remote show ${GITHUB_USERNAME}    #Выводим информации о branch
```

####Работа с Hunter
```ShellSession
$ mkdir cmake/projects/print    #Создаем директорию cmake/projects/print
$ cat > cmake/projects/print/hunter.cmake <<EOF   #Вносим изменения в hunter.cmake
include(hunter_add_version)
include(hunter_cacheable)
include(hunter_cmake_args)
include(hunter_download)
include(hunter_pick_scheme)
hunter_add_version(
    PACKAGE_NAME
    print
    VERSION
    "0.1.0.0"
    URL
    "https://github.com/${GITHUB_USERNAME}/lab09/archive/v0.1.0.0.tar.gz"
    SHA1
    ${PRINT_SHA1}
)
hunter_pick_scheme(DEFAULT url_sha1_cmake)
hunter_cmake_args(
    print
    CMAKE_ARGS
    BUILD_EXAMPLES=NO
    BUILD_TESTS=NO
)
hunter_cacheable(print)
hunter_download(PACKAGE_NAME print)
EOF
```
#### Вносим пакет print в  hunter
```ShellSession
$ cat >> cmake/configs/default.cmake <<EOF  #Вносим данные о пакете print в default.cmake
hunter_config(print VERSION 0.1.0.0)
EOF

```
#### Работа с локальными и удаленными репозиториями hunter
```ShellSession
$ git add .   #Добавляем все отредактированные файлы в подтвержденные
$ git commit -m"added print package"  #Создаем коммит с сообщением
$ git push ${GITHUB_USERNAME} master    
$ git tag v0.19.137.1 #Добавляем тэг на нашем репозитории
$ git push ${GITHUB_USERNAME} master --tags   #Отправляем на удаленную ветку все теги локальной ветки
$ cd ..
```
#### Работа с удаленным репозиторием десятой лабораторной работы
```ShellSession
$ export HUNTER_ROOT=`pwd`/hunter  #Экспортируем переменную HUNTER_ROOT
$ mkdir lab10 && cd lab10   #Создаем директорию lab10 и переходим в нее
$ git init    #Инициализируем локальный репозиторий
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab10   #Устанавливаем связь с удаленным репозиторием десятой лабораторной работы
```
#### Работа с файлами(demo.cpp)
```ShellSession
$ mkdir sources   #Созданием директории sources
$ cat > sources/demo.cpp <<EOF  #Создание demo.cpp и запись кода в demo.cpp
#include <print.hpp>

int main(int argc, char** argv) {
	std::string text;
	while(std::cin >> text) {
		std::ofstream out("log.txt", std::ios_base::app);
		print(text, out);
		out << std::endl;
	}
}
EOF
```
#### Получение HunterGate.cmake и его перенос в локальный репозиторий
```ShellSession
$ wget https://github.com/hunter-packages/gate/archive/v0.8.1.tar.gz #Устанавливаем пакет по адресу https://github.com/hunter-packages/gate/archive/v0.8.1.tar.gz 
$ tar -xzvf v0.8.1.tar.gz gate-0.8.1/cmake/HunterGate.cmake		#Разархивируем его
$ mkdir cmake		#Создаем директорию cmake
$ mv gate-0.8.1/cmake/HunterGate.cmake cmake 	#Переносим gate-0.8.1/cmake/HunterGate.cmake в директорию cmake
$ rm -rf gate*/		#Удаляем директорию gate-0.8.1
$ rm *.tar.gz		#Удаляем пакет v0.8.1.tar.gz
```
#### Работа с CMakeLists.txt
```ShellSession
$ cat > CMakeLists.txt <<EOF	#Вносим в CMakeLists.txt информацию о минимальной версии CMake и устанавливаем CMAKE_CXX_STANDARD
cmake_minimum_required(VERSION 3.0)

set(CMAKE_CXX_STANDARD 11)
EOF
```
#### Загрузка пакета, получение контрольной суммы
```
$ wget https://github.com/${GITHUB_USERNAME}/hunter/archive/v0.19.137.1.tar.gz	#Установка пакета по адресу https://github.com/${GITHUB_USERNAME}/hunter/archive/v0.19.137.1.tar.gz
$ export HUNTER_SHA1=`openssl sha1 v0.19.137.1.tar.gz | cut -d'=' -f2 | cut -c2-41`	#Экспортируем контрольную сумму
$ echo $HUNTER_SHA1	#Выводим контрольную сумму на экран консоли
#04aa0c99724692f83d4b47404691e79c16fd5914
$ rm -rf v0.19.137.1.tar.gz		#Удаляем v0.19.137.1.tar.gz
```
#### Работа с CMakeLists.txt
```ShellSession
$ cat >> CMakeLists.txt <<EOF	#Подключение HunterGate.cmake в CMakeLists.txt
include(cmake/HunterGate.cmake)
HunterGate(
    URL "https://github.com/${GITHUB_USERNAME}/hunter/archive/v0.19.137.1.tar.gz" 
    SHA1 "${HUNTER_SHA1}"
)
EOF
```

#### Работа с CMakeLists.txt
```ShellSession
$ cat >> CMakeLists.txt <<EOF

project(demo)	#Добавляем пакет print
hunter_add_package(print)	#Находим пакет print
find_package(print)

add_executable(demo \${CMAKE_CURRENT_SOURCE_DIR}/sources/demo.cpp)
target_link_libraries(demo print)

install(TARGETS demo RUNTIME DESTINATION bin)
EOF
```
#### Редактирование .gitignore
```ShellSession
$ cat > .gitignore <<EOF
*build*/
*install*/
*.swp
EOF
```
#### Редактирование README.md
```ShellSession
$ cat > README.md <<EOF		#Вставка markdown и текста
the demo application redirects data from stdin to a file **log.txt** using a package **print**.
EOF
```
#### Редактирование .travis.yml
```ShellSession
$ cat > .travis.yml <<EOF		#Задаем среду программирования
language: cpp
script:   
- cmake -H. -B_build
- cmake --build _build
EOF
```
#### Работа с Travis
```ShellSession
$ travis lint
```
#### Отправка на удаленный репозиторий десятой лабораторной работы
```ShellSession
$ git add .		#Добавляем все отредактированные файлы в подтвержденные
$ git commit -m"first commit"		#Создаем коммит с сообщением
$ git push origin master		#Выгружаем локальный репозиторий в удаленный репозиторий десятой лабораторной
```
Работа с Travis
```ShellSession
#Авторизуемся своим GITHUB аккаунтом
$ travis login --auto
#Включаем репозиторий в Travis
$ travis enable
```
#### Работа с Cmake
```
$ cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
$ cmake --build _build --target install
$ mkdir artifacts && cd artifacts		#Создаем директорию artifacts и переходим в нее
$ echo "text1 text2 text3" | ../_install/bin/demo
$ cat log.txt
```

## Report

```ShellSession
$ popd
$ export LAB_NUMBER=10
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```

## Links

- [hub](https://hub.github.com/)
- [polly](https://github.com/ruslo/polly)
- [conan](https://conan.io)

```
Copyright (c) 2017 Братья Вершинины
```
