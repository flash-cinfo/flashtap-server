# flashtap-server

## Установка сервера на Linux

Давайте установим сервер на ваш Linux сервер
Для компиляции сервера, вам понадобяться библиотеки
- Freeglut
- Glew
- SFML
Все это вы можете установить через ваш пакетный менеджер

### После установки библиотек
После установки библиотек вам понадобиться скомпилировать сервер
для этого мы копируем гитхаб сервера
`git clone https://github.com/flash-cinfo/flashtap-server`
переходим в папку build этими коммандами
```
cd flashtap-server
git clone https://github.com/flash-cinfo/flash-engine
mkdir build
cd build
```
конфигурируем CMake
```
cmake ..
```
компилируем проект
```
make $(nproc)
```
после этого запускаем сервер
```
cd ..
./server
```
Сервер запуститься по дефолту на порте 56000
Порт можно изменить в файле server.txt