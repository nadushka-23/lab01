# Лабораторная работа №1

## Изучение утилит для разработки проектов

Цель: научиться работать с базовыми Unix-утилитами, скачать и собрать библиотеку Boost.

## Подготовка окружения

```bash
export GITHUB_USERNAME=<имя пользователя>
mkdir -p ${HOME}/workspace
cd ${HOME}/workspace
```

## Установка Node.js (v6.11.5) из исходников

```bash
wget https://nodejs.org/dist/v6.11.5/node-v6.11.5.tar.gz
tar -xzf node-v6.11.5.tar.gz
cd node-v6.11.5
./configure --prefix=${HOME}/workspace/usr
make -j4
make install
export PATH=${HOME}/workspace/usr/bin:${PATH}
```

## Установка gist

```bash
npm install gist -g
gist --login
```

## Домашнее задание (работа с Boost)

### 1. Скачивание архива

```bash
wget https://sourceforge.net/projects/boost/files/boost/1.65.1/boost_1_65_1.tar.gz
```

### 2. Распаковка

```bash
tar -xzf boost_1_65_1.tar.gz
cd boost_1_65_1
```

### 3. Подсчёт количества файлов в корне (без поддиректорий)

```bash
ls -l | grep ^- | wc -l
```

### 4. Общее количество файлов (с поддиректориями)

```bash
find . -type f | wc -l
```

### 5. Количество заголовочных файлов `.hpp`

```bash
find . -type f -name "*.hpp" | wc -l
```

### 6. Количество файлов `.cpp`

```bash
find . -type f -name "*.cpp" | wc -l
```

### 7. Количество прочих файлов

```bash
find . -type f ! -name "*.hpp" ! -name "*.cpp" | wc -l
```

### 8. Найти файл `libs/asio/example/cpp03/chat/chat_message.hpp`

```bash
find . -name "chat_message.hpp"
```

### 9. Поиск строки `boost::asio` во всех `.hpp` файлах

```bash
grep -rl "boost::asio" --include="*.hpp" .
```

### 10. Сборка Boost

```bash
./bootstrap.sh --prefix=${HOME}/workspace/boost
./b2 install
```

### 11. Топ-10 самых больших файлов

```bash
find . -type f -exec du -h {} + | sort -rh | head -n 10
```

## Вывод

Освоены: `wget`, `tar`, `find`, `grep`, `ls`, `wc`, `du`, `sort`, сборка проектов через `./configure && make`.

## Ответы на вопросы к защите

**1. Чем `find` отличается от `grep`?**
`find` ищет **файлы и каталоги** по имени, размеру, типу, дате и т.п. — то есть работает с метаданными файловой системы. `grep` ищет **текст внутри файлов** по регулярному выражению. Часто связку используют вместе: `find ... | xargs grep ...` или `grep -r` (рекурсивный grep).

**2. Что делает `wc -l`?**
`wc` — word count. Флаг `-l` выводит число строк во входе. Например, `find . -type f | wc -l` посчитает количество файлов.

**3. Что делает `du -h`?**
`du` (disk usage) — показывает занимаемое файлами место. `-h` (human-readable) выводит размер в удобных единицах (K, M, G).

**4. Что делает `sort -rh`?**
`sort` сортирует строки. `-h` — числовая сортировка с пониманием суффиксов K/M/G, `-r` — в обратном порядке (от большего к меньшему). Используется, чтобы найти самые большие файлы.

**5. Зачем `./configure && make && make install`?**
Это классический порядок сборки из исходников:
- `./configure` — проверяет окружение (компилятор, библиотеки), генерирует `Makefile` под текущую систему.
- `make` — компилирует исходники по сгенерированному `Makefile`.
- `make install` — копирует собранные бинарники, заголовки и библиотеки в системные каталоги (обычно `/usr/local`).

