[![Build Status](https://travis-ci.org/desta-study/lab10.svg?branch=master)](https://travis-ci.org/desta-study/lab10)
the demo application redirects data from stdin to a file **log.txt** using a package **print**.


## Laboratory work XI
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
#Устанавливаем значение переменной окружения GITHUB_USERNAME
$ export GITHUB_USERNAME=desta-study
#Устанавливаем значение переменной окружения GITHUB_TOKEN
$ export GITHUB_TOKEN=<сгенирированный_токен>
```
Проводим первоначальные настройки, устанавливаем hunter
```ShellSession
$ cd ${GITHUB_USERNAME}/workspace
$ pushd .
$ source scripts/activate
$ go get github.com/github/hub
```
Работа с конфигом hub, установка значений переменным окружения
```ShellSession
#Создаем директорию config
$ mkdir ~/.config
#Заносим данные в hub(GITHUB_USERNAME, GITHUB_TOKEN)
$ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
#Устанавливаем глобальное значение hub.protocol
$ git config --global hub.protocol https
```
Работа с пакетом девятой лабораторной работы, получение контрольной суммы пакета
```ShellSession
#Устанавливаем v0.1.0.0.tar.gz
$ wget https://github.com/${GITHUB_USERNAME}/lab09/archive/v0.1.0.0.tar.gz
$ export PRINT_SHA1=`openssl sha1 v0.1.0.0.tar.gz | cut -d'=' -f2 | cut -c2-41`
#Выводим контрольную сумму на экран консоли
$ echo $PRINT_SHA1
#Удаляем v0.1.0.0.tar.gz
$ rm -rf v0.1.0.0.tar.gz
```
Работа с удаленным и локальным репозиторием Hunter, просмотр информации о ветках
```ShellSession
#Клонируем удаленный репозиторий https://github.com/ruslo/hunter в projects/hunter
$ git clone https://github.com/ruslo/hunter projects/hunter
#Меняем директорию на projects/hunter и переключаемся на ветвь v0.19.137
$ cd projects/hunter && git checkout v0.19.137
#Выводим branches в консоль
$ git remote show //origin
#Форкаем репозиторий
$ hub fork
#Выводим branches в консоль
$ git remote show 
#Выводим информации о branch
$ git remote show ${GITHUB_USERNAME}

```
Работа с Hunter
```ShellSession
#Создаем директорию cmake/projects/print
$ mkdir cmake/projects/print
#Вносим изменения в hunter.cmake
$ cat > cmake/projects/print/hunter.cmake <<EOF
include(hunter_add_version)
include(hunter_cacheable)
include(hunter_cmake_args)
include(hunter_download)
include(hunter_pick_scheme)
#Указываем данные о версии
hunter_add_version(
#Имя пакета
    PACKAGE_NAME
    print
#Версия пакета
    VERSION
    "0.1.0.0"
#Ссылка на пакет
    URL
    "https://github.com/${GITHUB_USERNAME}/lab09/archive/v0.1.0.0.tar.gz"
#Контрольная сумма
    SHA1
    ${PRINT_SHA1}
)
#Указываем версию по умолчанию
hunter_pick_scheme(DEFAULT url_sha1_cmake)
#Указываем hunter_cmake_args
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
Вносим пакет print в  hunter
```ShellSession
#Вносим данные о пакете print в default.cmake
$ cat >> cmake/configs/default.cmake <<EOF
hunter_config(print VERSION 0.1.0.0)
EOF

```
Работа с локальными и удаленными репозиториями hunter
```ShellSession
#Добавляем все отредактированные файлы в подтвержденные
$ git add .
#Создаем коммит с сообщением
$ git commit -m"added print package"
Выгружаем локальный репозиторий ветки ${GITHUB_USERNAME} в удаленный репозиторий ветки master
$ git push ${GITHUB_USERNAME} master
#Добавляем тэг на нашем репозитории
$ git tag v0.19.137.1
#Отправляем на удаленную ветку все теги локальной ветки
$ git push ${GITHUB_USERNAME} master --tags
#Выходим из директории
$ cd ..
```
Работа с удаленным репозиторием десятой лабораторной работы
```ShellSession
#Экспортируем переменную HUNTER_ROOT
$ export HUNTER_ROOT=`pwd`/hunter
#Создаем директорию lab10 и переходим в нее
$ mkdir lab10 && cd lab10
#Инициализируем локальный репозиторий
$ git init
#Устанавливаем связь с удаленным репозиторием десятой лабораторной работы
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab10
```
Работа с файлами(demo.cpp)
```ShellSession
#Созданием директории sources
$ mkdir sources
#Создание demo.cpp и запись кода в demo.cpp
$ cat > sources/demo.cpp <<EOF
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
Получение HunterGate.cmake и его перенос в локальный репозиторий
```ShellSession
#Устанавливаем пакет по адресу https://github.com/hunter-packages/gate/archive/v0.8.1.tar.gz 
$ wget https://github.com/hunter-packages/gate/archive/v0.8.1.tar.gz 
#Разархивируем его
$ tar -xzvf v0.8.1.tar.gz gate-0.8.1/cmake/HunterGate.cmake
#Создаем директорию cmake
$ mkdir cmake
#Переносим gate-0.8.1/cmake/HunterGate.cmake в директорию cmake
$ mv gate-0.8.1/cmake/HunterGate.cmake cmake
#Удаляем директорию gate-0.8.1
$ rm -rf gate*/
#Удаляем пакет v0.8.1.tar.gz
$ rm *.tar.gz
```
Работа с CMakeLists.txt
```ShellSession
#Вносим в CMakeLists.txt информацию о минимальной версии CMake и устанавливаем CMAKE_CXX_STANDARD
$ cat > CMakeLists.txt <<EOF
cmake_minimum_required(VERSION 3.0)

set(CMAKE_CXX_STANDARD 11)
EOF
```
Загрузка пакета, получение контрольной суммы
```
#Установка пакета по адресу https://github.com/${GITHUB_USERNAME}/hunter/archive/v0.19.137.1.tar.gz
#В v0.19.137.1.tar.gz содержится пакет print
$ wget https://github.com/${GITHUB_USERNAME}/hunter/archive/v0.19.137.1.tar.gz
#Экспортируем контрольную сумму
$ export HUNTER_SHA1=`openssl sha1 v0.19.137.1.tar.gz | cut -d'=' -f2 | cut -c2-41`
#Выводим контрольную сумму на экран консоли
$ echo $HUNTER_SHA1
#feabd55227870adfe44776d09e09789860e73e35
#Удаляем v0.19.137.1.tar.gz
$ rm -rf v0.19.137.1.tar.gz
```
Работа с CMakeLists.txt
```ShellSession
#Подключение HunterGate.cmake в CMakeLists.txt
$ cat >> CMakeLists.txt <<EOF
#Подключение HunterGate.cmake
include(cmake/HunterGate.cmake)
#Настройки HunterGate
HunterGate(
#Ссылка на пакет по адресу
    URL "https://github.com/${GITHUB_USERNAME}/hunter/archive/v0.19.137.1.tar.gz"
#Контрольная сумма    
    SHA1 "${HUNTER_SHA1}"
)
EOF
```
Работа с CMakeLists.txt
```ShellSession
$ cat >> CMakeLists.txt <<EOF

project(demo)
#Добавляем пакет print
hunter_add_package(print)
#Находим пакет print
find_package(print)

add_executable(demo \${CMAKE_CURRENT_SOURCE_DIR}/sources/demo.cpp)
target_link_libraries(demo print)

install(TARGETS demo RUNTIME DESTINATION bin)
EOF
```
Редактирование .gitignore
```ShellSession
$ cat > .gitignore <<EOF
*build*/
*install*/
*.swp
EOF
```
Редактирование README.md
```ShellSession
#Вставка markdown и текста
$ cat > README.md <<EOF
[![Build Status](https://travis-ci.org/${GITHUB_USERNAME}/lab10.svg?branch=master)](https://travis-ci.org/${GITHUB_USERNAME}/lab10)
the demo application redirects data from stdin to a file **log.txt** using a package **print**.
EOF
```
Редактирование .travis.yml
```ShellSession
$ cat > .travis.yml <<EOF
#Задаем среду программирования
language: cpp
#Параметр script отвечает за дальнейшую сборку проекта
script:   
- cmake -H. -B_build
- cmake --build _build
EOF
```
Работа с Travis
```ShellSession
#Отображаем предупреждения или ошибки в файле .travis.yml
$ travis lint
#Hooray, .travis.yml looks valid :)
```
Отправка на удаленный репозиторий десятой лабораторной работы
```ShellSession
#Добавляем все отредактированные файлы в подтвержденные
$ git add .
#Создаем коммит с сообщением
$ git commit -m"first commit"
#Выгружаем локальный репозиторий в удаленный репозиторий десятой лабораторной
$ git push origin master
```
Работа с Travis
```ShellSession
#Авторизуемся своим GITHUB аккаунтом
$ travis login --auto
#Включаем репозиторий в Travis
$ travis enable
```
Работа с Cmake
```ShellSession
#-H. устанавливаем каталог в который сгенерируется файл CMakeLists.txt
#-B_build указывает директорию для собираемых файлов
#-D - заменяет команду set
$ cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
#--build _build создает бинарное дерево проекта
#--target указывает необходимые для обработки цели
$ cmake --build _build --target install
#Создаем директорию artifacts и переходим в нее
$ mkdir artifacts && cd artifacts
$ echo "text1 text2 text3" | ../_install/bin/demo
$ cat log.txt
text1
text2
text3
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

