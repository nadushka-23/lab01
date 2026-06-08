# Лабораторная работа №1

## Изучение утилит для разработки проектов

**Цель:** Научиться работать с базовыми Unix-утилитами, скачать и собрать библиотеку Boost.

## 1. Подготовка окружения
Работа велась в среде WSL (Ubuntu). Были установлены необходимые переменные окружения и создана рабочая директория `~/workspace/lab01`.

## 2. Домашнее задание (Работа с Boost)

### 1. Скачивание архива
```bash
wget [https://archives.boost.io/release/1.69.0/source/boost_1_69_0.tar.gz](https://archives.boost.io/release/1.69.0/source/boost_1_69_0.tar.gz)
```

### 2. Распаковка

```bash
tar -xzf boost_1_69_0.tar.gz
cd boost_1_69_0
```

### 3. Подсчёт количества файлов в корне (без поддиректорий)

```bash
ls -l | grep ^- | wc -l
```
#### Вывод терминала: 4

### 4. Общее количество файлов (с поддиректориями)

```bash
find . -type f | wc -l
```
#### Вывод терминала: 75805

### 5. Количество заголовочных файлов `.hpp`

```bash
find . -type f -name "*.hpp" | wc -l
```
#### Вывод терминала: 28098

### 6. Количество файлов `.cpp`

```bash
find . -type f -name "*.cpp" | wc -l
```
#### Вывод терминала: 13786
### 7. Количество прочих файлов

```bash
find . -type f ! -name "*.hpp" ! -name "*.cpp" | wc -l
```
#### Вывод терминала: 33921
### 8. Найти файл `libs/asio/example/cpp03/chat/chat_message.hpp`

```bash
find . -name "chat_message.hpp"
```
#### Вывод терминала: 
./boost_output/include/boost/any.hpp
./boost_output/include/boost/fusion/algorithm/query/any.hpp
./boost_output/include/boost/fusion/algorithm/query/detail/any.hpp
./boost_output/include/boost/fusion/include/any.hpp
./boost_output/include/boost/hana/any.hpp
./boost_output/include/boost/hana/fwd/any.hpp
./boost_output/include/boost/type_erasure/any.hpp
./boost_output/include/boost/spirit/home/support/algorithm/any.hpp
./boost_output/include/boost/proto/detail/any.hpp
./boost_output/include/boost/xpressive/detail/utility/any.hpp
./boost_1_69_0/boost/any.hpp
./boost_1_69_0/boost/fusion/algorithm/query/any.hpp
./boost_1_69_0/boost/fusion/algorithm/query/detail/any.hpp
./boost_1_69_0/boost/fusion/include/any.hpp
./boost_1_69_0/boost/hana/any.hpp
./boost_1_69_0/boost/hana/fwd/any.hpp
./boost_1_69_0/boost/type_erasure/any.hpp
./boost_1_69_0/boost/spirit/home/support/algorithm/any.hpp
./boost_1_69_0/boost/proto/detail/any.hpp
./boost_1_69_0/boost/xpressive/detail/utility/any.hpp

###9. Поиск строки boost::asio (первые 5 строк)
```bash
grep -r "boost::asio" --include=".hpp" --include=".cpp" . 2>/dev/null | head -5
```
#### Результат: ./libs/asio/example/cpp03/chat/posix_chat_client.cpp:using boost::asio::ip::tcp; ./libs/asio/example/cpp03/chat/posix_chat_client.cpp:namespace posix = boost::asio::posix; ./libs/asio/example/cpp03/chat/posix_chat_client.cpp: posix_chat_client(boost::asio::io_context& io_context, ./libs/asio/example/cpp03/chat/posix_chat_client.cpp: boost::asio::async_connect(socket_, endpoints, ./libs/asio/example/cpp03/chat/posix_chat_client.cpp: boost::asio::placeholders::error));


### 10. Сборка Boost

```bash
./bootstrap.sh --prefix=${HOME}/workspace/boost
./b2 install
```
#### Вывод терминала прописан в файле build_process.log
### 11. Копирование статических библиотек
```bash
 mkdir -p ~/boost/libs find ~/boost_1_69_0/stage/lib -name "*.a" -exec cp {} ~/boost/libs/ ;
```
#### Результат: библиотеки скопированы в ~/boost/libs


### 12. Топ-10 самых больших файлов

```bash
find . -type f -exec du -h {} + | sort -rh | head -n 10
```
#### Вывод терминала: 
4.5M    /home/nadushka_23/workspace/lab01/boost_output/lib/libboost_wave.a
3.2M    /home/nadushka_23/workspace/lab01/boost_output/lib/libboost_regex.a
2.7M    /home/nadushka_23/workspace/lab01/boost_output/lib/libboost_math_tr1l.a
2.7M    /home/nadushka_23/workspace/lab01/boost_output/lib/libboost_math_tr1.a
2.6M    /home/nadushka_23/workspace/lab01/boost_output/lib/libboost_math_tr1f.a
2.3M    /home/nadushka_23/workspace/lab01/boost_output/lib/libboost_unit_test_framework.a
2.3M    /home/nadushka_23/workspace/lab01/boost_output/lib/libboost_test_exec_monitor.a
2.3M    /home/nadushka_23/workspace/lab01/boost_output/include/boost/typeof/vector200.hpp
1.9M    /home/nadushka_23/workspace/lab01/boost_output/include/boost/geometry/srs/projections/epsg_traits.hpp
1.6M    /home/nadushka_23/workspace/lab01/boost_output/lib/libboost_program_options.a
## Вывод

Освоены: `wget`, `tar`, `find`, `grep`, `ls`, `wc`, `du`, `sort`, сборка проектов через `./configure && make`.


