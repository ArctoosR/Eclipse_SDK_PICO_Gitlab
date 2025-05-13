# pico-examples-windows



### Описание

Данный проект содержит набор примеров для платы Raspberry Pi Pico, которые могут быть скомпилированы в Eclipse IDE for C/C++ Developers в операционной системе Windows. Все примеры построены на базе Raspberry Pi Pico C/C++ SDK. Для сборки не нужно использование CMake/Make. Более подробно о сборке проектов в Eclipse: [https://hamlab.net/mcu/raspbery_pi_pico_rp2040.html](https://hamlab.net/mcu/raspbery_pi_pico_rp2040.html)

### Клонирование репозитория

Для клонирования репозитория выполните следующие команды:

    git clone https://gitlab.com/osandr/pico-examples-windows.git
	cd pico-examples-windows
	git submodule init
	git submodule update

### Необходимые инструменты

 * Eclipse Embedded CDT версии >= 2022-12
 * Toolchain GNU Arm Embedded GCC версии >= 10.3 (можно скачать здесь [gcc-arm-none-eabi-10.3](https://developer.arm.com/-/media/Files/downloads/gnu-rm/10.3-2021.10/gcc-arm-none-eabi-10.3-2021.10-win32.zip))  

### Настройки о сборка примеров
 * Создать переменную окружения PICO\_TOOLCHAIN\_PATH=X:\toolchain\_path\bin;
 * Создать рабочий каталог Eclipse в любом удобном месте на диске;
 * Произвести импорт проектов в Eclipse используя Existing Projects into Workspace
 * Проекты примеров не нуждаются в настройках и можно сразу же выполнять их сборку

### Запуск отладки
 * Для отладки не нужно иметь специальное устройство-отладчик. Для этих целей используется программа [pico-debug](https://github.com/majbthrd/pico-debug "pico-debug"), которая загружается в RAM-память MCU и исполняется на ядре CPU2. Программа превращает Rasperri Pi Pico в устройство USB-HID, реализующее интерфейс CMSIS-DAP
 * Произведите сборку программу pico-debug. На выходе должен получиться файл *pico-debug-gimmecache.uf2* Так же в репозитории программы можно скачать уже собранную версию
 * Переведите Raspberry Pi Pico в режим Mass Storage Device, для чего зажав кнопку Boot подключите плату к USB
 * Скопируйте файл *pico-debug-gimmecache.uf2* на виртуальный накопитель, после чего он будет отключен и программа pico-debug начнет исполняться
 * Запустите OpenOCD: `pico-examples-windows\Tools\OpenOCD-20211118-0.11.0\bin\openocd.exe -f board/pico-debug.cfg` 
 * Откройте *Run->Debug Configurations...* и выберите в разделе *GDB OpenOCD Debugging* конфигурацию, соответствующую вашему проекту
