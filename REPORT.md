# Отчет по лабораторной работе №3
## ВЫполнил: Артеменко Арина ИУ8-22

## Репозиторий: https://github.com/gest475/lab003

## Цель работы
Освоить систему сборки CMake, научиться описывать статические библиотеки и приложения.

## Выполненные команды и их вывод

`cd ~/workspace`


`mkdir -p projects/lab03 && cd projects/lab03`


`git init`
*Вывод:*
[master (root-commit) 2ff4ce9] Initial commit: add README.md

1 file changed, 1 insertion(+)

create mode 100644 README.md

`mkdir -p sources include examples`


`git add .`


`git commit -m "added sources"`
*Вывод:*
[master 6e81afc] added sources

4 files changed, 33 insertions(+)


`cat > formatter_lib/CMakeLists.txt <<EOF`

`cat > formatter_ex_lib/CMakeLists.txt <<EOF`


`cat > hello_world_application/CMakeLists.txt <<EOF`


`cat > solver_lib/CMakeLists.txt <<EOF`


`cat > solver_application/CMakeLists.txt <<EOF`


`cat > CMakeLists.txt <<EOF`


`git add .`


`git commit -m "add CMakeLists.txt for all modules"`

*Вывод:*

[master 7e76299] add CMakeLists.txt for all modules

6 files changed, 52 insertions(+)

create mode 100644 CMakeLists.txt

create mode 100644 formatter_ex_lib/CMakeLists.txt

create mode 100644 formatter_lib/CMakeLists.txt

create mode 100644 hello_world_application/CMakeLists.txt

create mode 100644 solver_application/CMakeLists.txt

create mode 100644 solver_lib/CMakeLists.txt
