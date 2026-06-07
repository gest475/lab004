# Отчет по лабораторной работе №4: Continuous Integration

## Выполнил: Артеменко Арина ИУ8-22

## Цель работы
Изучение систем непрерывной интеграции на примере Travis CI и GitHub Actions.

## Ход выполнения

### 1. Настройка окружения
```
export GITHUB_USERNAME=gest475
export GITHUB_TOKEN=ghp_6Rgd0JgVHDZQ1N4zK9VE16a8Nh5DFQ4ZBPVQ
```
### 2. Установка RVM (Ruby Version Manager)

`\curl -sSL https://get.rvm.io | bash -s -- --ignore-dotfiles`

**Вывод:**
```
Turning on ignore dotfiles mode.
Downloading https://github.com/rvm/rvm/archive/master.tar.gz
Installing RVM to /home/maryu/.rvm/
Installation of RVM in /home/maryu/.rvm/ is almost complete.
```
### 3. Установка Ruby

`source /home/maryu/.rvm/scripts/rvm`

`rvm autolibs disable`

`rvm install ruby-3.0.0`

**Вывод:**
```
ruby-3.0.0 - #downloading ruby-3.0.0
ruby-3.0.0 - #extracting
ruby-3.0.0 - #configuring
ruby-3.0.0 - #compiling
ruby-3.0.0 - #installing
Install of ruby-3.0.0 - #complete
```

`rvm use 3.0.0 --default`

`ruby --version`

**Вывод:**
```
ruby 3.0.0p0 (2020-12-25 revision 95aff21468) [x86_64-linux]
```
### 4. Установка Travis CLI

`gem install travis`

**Вывод:**
```
Successfully installed travis-1.14.0
30 gems installed
```

### 5. Клонирование репозитория с кодом lab03

`git clone https://github.com/gest475/lab003 projects/lab004`

**Вывод:**
```
Cloning into 'projects/lab004'...
Receiving objects: 100% (48/48), 10.18 KiB | 297.00 KiB/s, done.
```

### 6. Создание конфигурационного файла .travis.yml

`cat > .travis.yml <<EOF`
```
language: cpp

script:
- cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
- cmake --build _build
- cmake --build _build --target install

addons:
  apt:
    sources:
      - george-edison55-precise-backports
    packages:
      - cmake
      - cmake-data
EOF
```

`cat .travis.yml`

**Вывод:**
```
language: cpp

script:
- cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
- cmake --build _build
- cmake --build _build --target install

addons:
  apt:
    sources:
      - george-edison55-precise-backports
    packages:
      - cmake
      - cmake-data
```
### 7. Проверка синтаксиса .travis.yml

`travis lint`

**Вывод:**
```
Hooray, .travis.yml looks valid :)
```

### 8. Авторизация в Travis CI

`travis login --github-token ${GITHUB_TOKEN} --com`

**Вывод:**
```
Successfully logged in as gest475!
```

### 9. Попытка активации репозитория в Travis CI

`travis enable --com -r gest475/lab004`

**Вывод:**
```
repository not known to Travis CI (or no access?)
triggering sync: done
repository not known to https://api.travis-ci.com/: gest475/lab004
```

`travis accounts --com`

**Вывод:**
```
gest475 (alsxndrsps): not subscribed, 0 repositories
To set up a subscription, please visit app.travis-ci.com.
```

### 10. Альтернативное решение: настройка GitHub Actions

Создание директории и файла workflow:

`mkdir -p .github/workflows`

`cat > .github/workflows/ci.yml <<'EOF'
```
name: CI

on:
push:
branches: [ main, master ]
pull_request:
branches: [ main, master ]

jobs:
build:
runs-on: ubuntu-latest

steps:

uses: actions/checkout@v4

name: Configure CMake
run: cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install

name: Build
run: cmake --build _build

name: Install
run: cmake --build _build --target install
EOF
```
`cat .github/workflows/ci.yml`

**Вывод:**
```
name: CI

on:
  push:
    branches: [ main, master ]
  pull_request:
    branches: [ main, master ]

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v4
    
    - name: Configure CMake
      run: cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
    
    - name: Build
      run: cmake --build _build
    
    - name: Install
      run: cmake --build _build --target install
```
## 11. Создание README.md и добавление бейджа

`echo '# lab004' > README.md`

`echo '' >> README.md`

`echo '[![CI](https://github.com/gest475/lab004/actions/workflows/ci.yml/badge.svg)](https://github.com/gest475/lab004/actions/workflows/ci.yml)' >> README.md`

`cat README.md`

**Вывод:**
```markdown
# lab004

[![CI](https://github.com/gest475/lab004/actions/workflows/ci.yml/badge.svg)](https://github.com/gest475/lab004/actions/workflows/ci.yml)
```

## 12. Установка GitHub CLI и авторизация

`sudo apt install gh -y`

`gh --version`

**Вывод:**
```
gh version 2.45.0 (2025-07-18 Ubuntu 2.45.0-1ubuntu0.3)
```

`unset GITHUB_TOKEN`

`gh auth login --web`

**Вывод:**
```
First copy your one-time code: 1C90-0E7A
Authentication complete.
Logged in as gest475
```

## 13. Создание репозитория на GitHub

`gh repo create lab004 --public --source=. --remote=origin --push`

**Вывод:**
```
Created repository gest475/lab004 on GitHub
https://github.com/gest475/lab004
```

## 14. Фиксация изменений и отправка на GitHub

`git add .travis.yml .github/workflows/ci.yml README.md`

`git commit -m "added Travis CI and GitHub Actions configuration"`

**Вывод:**
```
[main 100fdf7] added Travis CI and GitHub Actions configuration
1 file changed, 14 insertions(+)
create mode 100644 .travis.yml
```

`git push -u origin main`

**Вывод:**
```
Enumerating objects: 51, done.
Counting objects: 100% (51/51), done.
Writing objects: 100% (51/51), 10.56 KiB | 3.52 MiB/s, done.
Total 51 (delta 18), reused 47 (delta 17), pack-reused 0
To https://github.com/gest475/lab004

[new branch] main -> main
branch 'main' set up to track 'origin/main'.
```
## 15. Проверка статуса сборки GitHub Actions

`gh run list --repo gest475/lab004`

**Вывод:**
```
STATUS TITLE WORKFLOW BRANCH ID
success added GitHub Actions CI and badge CI main 27089814029
```
