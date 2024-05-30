# AIoT_one
AIoT第一堂
## 認識晶片  YD-ESP32-S3-EYE 
ESP32-S3-EYE是一款小型人工智慧開發板，配備了ESP32-S3晶片和ESP-WHO人工智慧開發框架。 該開發板擁有2百萬像素的攝影機、一個LCD顯示器、一個麥克風，以及8MB的八線PSRAM和8MB的flash存儲，非常適合於圖像識別和音頻處理等應用 (espressif)。
#### 外觀
<img width="188" alt="image" src="https://github.com/itemhsu/AIoT_one/assets/25599185/b9614508-a8ab-4292-939e-a71ca91c49dc">
<img width="162" alt="image" src="https://github.com/itemhsu/AIoT_one/assets/25599185/36f3e026-77a8-4a8b-843d-d8be1b0d645f">

#### 上電
USB 接上電腦之後就會啟動

<img width="170" alt="image" src="https://github.com/itemhsu/AIoT_one/assets/25599185/b3d7389b-4874-40e2-8cff-1dbcf672bfc0">

#### 影像顯示測試
左上角按鈕按一下

<img width="163" alt="image" src="https://github.com/itemhsu/AIoT_one/assets/25599185/32fb46d2-7d8b-45c1-8963-3bc72777ec9c">

#### 人臉偵測展示
左上角按鈕再按一下

<img width="753" alt="image" src="https://github.com/itemhsu/AIoT_one/assets/25599185/cc70abee-1753-42f2-8190-f01e40cb9dac">

#### ESP32 SoC 晶片支援以下功能：

* 2.4 GHz Wi-Fi
* 藍牙 4.2
* 高性能雙核心
* 超低功耗協處理器
* 多種週邊
* 便宜

## 期末評分
### 現有的範例
```
examples/
├── cat_face_detection
│   ├── lcd
│   ├── README.rst
│   ├── terminal
│   └── web
├── code_recognition
│   ├── CMakeLists.txt
│   ├── main
│   ├── README.md
│   ├── sdkconfig.defaults
│   ├── sdkconfig.defaults.esp32
│   ├── sdkconfig.defaults.esp32s2
│   └── sdkconfig.defaults.esp32s3
├── color_detection
│   ├── lcd
│   ├── README_CN.md
│   └── README.md
├── esp32-s3-eye
│   ├── CMakeLists.txt
│   ├── main
│   ├── partitions.csv
│   ├── README_CN.md
│   ├── README.md
│   └── sdkconfig.defaults
├── human_face_detection
│   ├── lcd
│   ├── README.rst
│   ├── terminal
│   └── web
├── human_face_recognition
│   ├── lcd
│   ├── README_CN.md
│   ├── README.md
│   └── terminal
└── motion_detection
    ├── lcd
    ├── README.rst
    ├── terminal
    └── web
```
### 評分方式
| 項目 | 分數 |
| --- | --- |
| Terminal 範例執行成功 | 60 |
| 復原範例執行成功 | +10 |
| 完成Terminal 範例 Markdown 操作手冊 | +5 | 
| LCD 範例執行成功 | +5 |
| 完成LCD 範例 Markdown 操作手冊 | +5 | 
| WEB 範例執行成功 | +5 |
| 完成WEB 範例 Markdown 操作手冊 | +5 | 
| 修改代碼成功 | +5 |
| 完成修改代碼操作手冊 | +5 | 
| 更新模型成功 | +10 |
| 完成更新模型操作手冊 | +5 | 
| 自訓練模型成功 | +15 |
| 完成自訓練模型操作手冊 | +5 | 


## 軟體開發

ESP-EYE 可在 Linux、MacOs、Windows 作業系統中完成軟體燒寫。 目前，必須進行開發環境的工具鏈配置，詳見下方介紹。
<img width="512" alt="image" src="https://github.com/itemhsu/AIoT_one/assets/25599185/4a687851-2312-4cd2-be3f-c022780da6b6">


### 準備工作

- 閱讀 [ESP-IDF程式指南](https://espressif-docs.readthedocs-hosted.com/projects/esp-idf/zh-cn/latest/get-started/index.html)，參考對應章節，設定工具鏈；
- windows 可以使用 https://dl.espressif.com/dl/esp-idf/
- 準備 USB Type-C 線，用於連接 PC 和 YD-ESP32-S3-EYE 開發板；
- 選擇適合開發環境的工具，例如 Terminal (Linux/MacOS) 或 MinGW (Windows) 等。
- AWS主控台登入
  - URL https://049281306005.signin.aws.amazon.com/console
  - 使用者名稱 class0@NTUT
### AWS Linux 範例
請使用這一區

<img width="331" alt="image" src="https://github.com/itemhsu/AIoT_one/assets/25599185/7c7799d4-8784-418d-aafd-65d8c1684f92">

#### Launch SageMaker Notebook
* use "C4-XLarge", that has 4 cpus
#### Setting Sagemaker Enviroment
* New a sagemaker terminal
* Change directory: for future file operation
```
cd SageMaker
```
* Installing new software on Amazon Linux, which is based on RHEL/CentOS, typically involves using the yum package manager (for Amazon Linux 2 and earlier
```
sudo yum update
sudo yum install ninja-build
```
cmake is already install , so we skip install cmake.
* mkdir esp for future working
```
mkdir esp
```
#### Local install
您需要在本機上安裝 ESP32 刷機工具。 ESP-IDF（物聯網開發框架）提供了 esptool.py，這是一個用於刷新 ESP32 裝置的 Python 實用程式。
如果您還沒有安裝 ESP-IDF 及其工具，可以使用 pip 單獨安裝 esptool.py：
```
pip install esptool
```

#### 使用 Minicom 来查看ESP32的输出
* 安装 Minicom
如果您还没有安装 Minicom，可以通过您的 Linux 发行版的包管理器进行安装。例如，在基于 Debian 的系统（如 Ubuntu）上，您可以使用以下命令安装：
```
sudo apt-get install minicom
```

对于 Amazon Linux 或基于 RHEL 的系统，使用：
```
sudo yum install minicom
```

* 配置 Minicom
在启动 Minicom 之前，您需要知道您的设备连接到的串行端口号以及设备通讯的相关参数（如波特率）。通常，ESP32 等设备的默认波特率是 115200。

查找设备的串行端口：您可以使用 `dmesg | grep tty` 命令来查看设备连接的串行端口。通常，设备会被标记为 `/dev/ttyUSB0` 或 `/dev/ttyACM0`。MacOS 标记为 `/dev/tty.SLAB_USBtoUART`

* 配置 Minicom：运行 Minicom 的配置界面来设置串行端口参数。
```
sudo minicom -s
```
  * 在配置界面中，选择 "Serial port setup" 来设置串行端口参数。您需要设置以下几项：
    * Serial Device: 修改为您的设备串行端口，例如 /dev/ttyUSB0。
    * Bps/Par/Bits: 设置波特率（例如 115200）和其他通讯参数（通常为 8N1）。
    * Exit: 退出配置界面。
* 使用 Minicom 查看输出
配置完成后，您可以启动 Minicom 以连接到您的设备并查看输出：

* 退出 Minicom
要退出 Minicom，您可以按 Ctrl-A 然后按 Z 键来进入 Minicom 的帮助菜单，再按 X 键退出。

### MacOS 範例
ESP-IDF 將使用 Mac OS 上預設安裝的 Python 版本。


安裝 pip:
```
brew install pip
```
安裝 pyserial:
```
pip install --user pyserial
```

安裝 CMake 和 Ninja 編譯工具：
```
brew install cmake ninja
```
強烈建議同時安裝 ccache 以獲得更快的編譯速度。 
```
brew install ccache
```
### CMake 介紹
 CMake是一個開源的跨平台自動化建置系統，它使用一個名為CMakeLists.txt的檔案來描述建置流程，可以產生標準的建置文件，例如Unix的Makefile或Windows的專案檔案。 以下是CMake的一些關鍵特性和基礎概念的簡介：

#### 關鍵特性
* 跨平台支援：CMake支援多種平台，包括但不限於Linux、macOS、Windows。
* 生成器：CMake可以產生多種編譯器和IDE的專案文件，如Makefile、Ninja、Visual Studio專案檔等。
* 可擴充：透過編寫模組和函數，可以擴展CMake的功能。
#### 基礎概念
* 變數：CMake中的變數用於儲存訊息，可以在CMakeLists.txt檔案中設定和引用。
* 指令：CMake腳本由一系列指令組成，每個指令代表一個操作，如設定變數、新增庫等。
* 目標：目標是建置過程中的關鍵概念，可以是執行檔、庫檔等。
* 屬性：目標、測試、目錄和全域等可以有屬性，屬性用來定義特定行為。
#### 開始使用
* 安裝CMake：首先，需要在你的系統上安裝CMake。
* 撰寫CMakeLists.txt檔案：這是CMake專案的核心文件，描述如何建構專案。
* 設定專案：使用cmake命令列工具對專案進行配置，產生建置檔。
* 建置專案：透過產生的建置檔案（如Makefile）建置專案。

### Ninja  介紹
是一個緊湊且快速的建置系統，旨在盡快處理專案建置。 與許多傳統的建置系統不同，Ninja 以其簡單性和高效性而著稱，使其成為需要快速迭代周期的大型專案的首選。 以下介紹了 Ninja 的脫穎而出之處：

#### 主要特徵：
* 速度：忍者註重速度。 它透過避免不必要的工作並優化增量建置的建置過程來實現這一點。
* 簡單性：雖然 Ninja 建立檔案是人類可讀的，但它們並不適合手寫。 相反，它們是由 CMake 等更高層級的建置系統產生的，提供簡單且高效的工作流程（Ninja Build）。
#### 何時使用Ninja：
* Ninja 本身並不是一個成熟的建造系統，而是被設計為用作更大的建造系統的一部分。 它對於需要最小化建置時間的專案特別有益，例如 Google Chrome 和 Android 的一部分（Ninja Build）。
* 對於需要快速、可靠且最小設定來編譯程式碼的開發人員來說，它是理想的選擇（Ninja Build）。
#### Ninja的工作原理：
* Ninja 建構在 build.ninja 檔案中進行描述，其中包括檔案應如何編譯的規則以及檔案之間的依賴關係（CnBlogs）。
* 它使用簡單的語法來定義建置規則和依賴項，從而最佳化增量建置。 當檔案變更時，Ninja 僅重建受該變更影響的專案部分（CnBlogs）（維基百科）。
#### Ninja入門：
* 安裝：Ninja 可以使用macOS 上的Homebrew（brew install ninja）、Windows 上的Chocolatey（choco install ninja）等套件管理器進行安裝，或者透過Conda 和Pip（Earthly - 讓建置超級簡單）等其他套件管理器進行安裝。
* 建立您的第一個專案：要使用 Ninja 建置項目，您通常需要 CMake 等更高層級的建置系統來產生 build.ninja 檔案。 檔案產生後，您可以執行 Ninja 來編譯專案（Earthly - 讓建置超級簡單）。
#### 增量構建：
* Ninja 擅長增量構建，僅重新編譯更改的文件，從而大大縮短大型專案的構建時間（Earthly - 讓構建超級簡單）。
* 典型的工作流程包括使用 CMake (cmake -G Ninja ..) 產生 Ninja 建置文件，然後執行 Ninja 來建置專案 (ninja)。 這個過程很簡單，可以顯著加快開發週期（Earthly - 讓建置超級簡單）。

### Project Building Hands on 
Creating a "Hellow world" example
* 切換到名為 esp 的目錄：
```
cd esp
```
* 遞歸克隆 esp-who 專案的 Git 儲存庫：
```
git clone --recursive https://github.com/espressif/esp-who.git
```
* 遞歸克隆 esp-idf 專案的 Git 儲存庫：
```
git clone --recursive https://github.com/espressif/esp-idf.git
```
* 切換到 esp-idf 目錄：
```
cd esp-idf/
```
* 執行 install.sh 腳本，安裝開發環境：
```
./install.sh
```
* 執行 export.sh 腳本，設置環境變量：
```
source ./export.sh
```
* 返回上一級目錄：
```
cd ..
```

* 從 IDF_PATH 環境變量指定的路徑復制 hello_world 範例到當前目錄：
```
cp -r $IDF_PATH/examples/get-started/hello_world .
```
* 切換到 hello_world 目錄：
```
cd hello_world/
```

* 執行 idf.py 工具進行配置（例如設置項目參數）：
```
idf.py set-target esp32s3
idf.py menuconfig
```
<img width="513" alt="image" src="https://github.com/itemhsu/AIoT_one/assets/25599185/cd5da1d0-5404-4e36-82f2-ad104b90d7fe">

* 使用 idf.py 工具構建項目：
```
idf.py fullclean
idf.py build
```
注意構建後的燒錄指令

<img width="1133" alt="image" src="https://github.com/itemhsu/AIoT_one/assets/25599185/65dba0ad-f191-46ef-8665-6b4b2c273061">


### Image Flashing Hands on 
要把 AWS 云上的 Amazon Linux 环境中构建的 ESP32 项目烧录到您本地的设备上，您需要通过以下几个步骤操作：
#### 下载构建结果
* 将构建好的固件（通常是 .bin 文件）从您的云服务器下载到您的本地计算机。您可以使用 SageMaker Download 。有三個檔案要下載
  *  build/partition_table/partition-table.bin 
  *  build/bootloader/bootloader.bin
  *  build/hello_world.bin
* 例如，選取路徑如下：

<img width="362" alt="image" src="https://github.com/itemhsu/AIoT_one/assets/25599185/10518230-f321-413f-aa3b-3fb3a2dd2cdf">

* 選擇檔案

<img width="268" alt="image" src="https://github.com/itemhsu/AIoT_one/assets/25599185/2f3f6977-1953-481a-adb5-c98d29adcb55">

* 點選Download

<img width="133" alt="image" src="https://github.com/itemhsu/AIoT_one/assets/25599185/58bddf32-afad-46f9-95c9-8867fd9aecd9">

#### 燒錄韌體

* 使用 ESP-IDF 提供的燒錄工具將下載的韌體燒錄到您的裝置上。 esp32燒錄指令可能看起來像這樣：
  
```
esptool.py --chip esp32 -p /dev/tty.SLAB_USBtoUART  write_flash -z 0x1000 ./bootloader.bin 0x8000 ./partition-table.bin  0x10000 ./hello_world.bin
```
* esp32s3 燒錄指令可能看起來像這樣：
```
esptool.py --chip esp32s3 -p /dev/tty.usbmodem11301 erase_flash
esptool.py --chip esp32s3 -p /dev/tty.usbmodem11301 -b 460800 --before default_reset --after hard_reset write_flash --flash_mode dio --flash_size 4MB --flash_freq 40m 0x0 bootloader.bin 0x8000 partition-table.bin 0x10000 hello_world.bin
```
linux 
```
esptool.py --chip esp32s3 -p /dev/ttyACM0 erase_flash
esptool.py --chip esp32s3 -p /dev/ttyACM0 -b 460800 --before default_reset --after hard_reset write_flash --flash_mode dio --flash_size 4MB --flash_freq 40m 0x0 bootloader.bin 0x8000 partition-table.bin 0x10000 hello_world.bin

```
#### 執行結果（minicom）
```
rst:0xc (SW_CPU_RESET),boot:0x13 (SPI_FAST_FLASH_BOOT)
configsip: 0, SPIWP:0xee
clk_drv:0x00,q_drv:0x00,d_drv:0x00,cs0_drv:0x00,hd_drv:0x00,wp_drv:0x00
mode:DIO, clock div:2
load:0x3fff0030,len:7176
load:0x40078000,len:15564
ho 0 tail 12 room 4
load:0x40080400,len:4
load:0x40080404,len:3904
entry 0x40080640
I (31) boot: ESP-IDF v5.3-dev-3220-g9c99a385ad 2nd stage bootloader
I (31) boot: compile time Apr  5 2024 08:51:47
I (33) boot: Multicore bootloader
I (37) boot: chip revision: v1.0
I (41) boot.esp32: SPI Speed      : 40MHz
I (45) boot.esp32: SPI Mode       : DIO
I (50) boot.esp32: SPI Flash Size : 2MB
I (54) boot: Enabling RNG early entropy source...
I (60) boot: Partition Table:
I (63) boot: ## Label            Usage          Type ST Offset   Length
I (71) boot:  0 nvs              WiFi data        01 02 00009000 00006000
I (78) boot:  1 phy_init         RF data          01 01 0000f000 00001000
I (86) boot:  2 factory          factory app      00 00 00010000 00100000
I (93) boot: End of partition table
I (97) esp_image: segment 0: paddr=00010020 vaddr=3f400020 size=09414h ( 37908) map
I (119) esp_image: segment 1: paddr=0001943c vaddr=3ffb0000 size=02200h (  8704) load
I (122) esp_image: segment 2: paddr=0001b644 vaddr=40080000 size=049d4h ( 18900) load
I (132) esp_image: segment 3: paddr=00020020 vaddr=400d0020 size=13850h ( 79952) map
I (161) esp_image: segment 4: paddr=00033878 vaddr=400849d4 size=077ech ( 30700) load
I (179) boot: Loaded app from partition at offset 0x10000
I (179) boot: Disabling RNG early entropy source...
I (191) cpu_start: Multicore app
I (199) cpu_start: Pro cpu start user code
I (199) cpu_start: cpu freq: 160000000 Hz
I (200) app_init: Application information:
I (202) app_init: Project name:     hello_world
I (208) app_init: App version:      1
I (212) app_init: Compile time:     Apr  5 2024 08:52:04
I (218) app_init: ELF file SHA256:  bb6384479...
I (223) app_init: ESP-IDF:          v5.3-dev-3220-g9c99a385ad
I (230) efuse_init: Min chip rev:     v0.0
I (234) efuse_init: Max chip rev:     v3.99
I (239) efuse_init: Chip rev:         v1.0
I (245) heap_init: Initializing. RAM available for dynamic allocation:
I (252) heap_init: At 3FFAE6E0 len 00001920 (6 KiB): DRAM
I (258) heap_init: At 3FFB2AC8 len 0002D538 (181 KiB): DRAM
I (264) heap_init: At 3FFE0440 len 00003AE0 (14 KiB): D/IRAM
I (270) heap_init: At 3FFE4350 len 0001BCB0 (111 KiB): D/IRAM
I (277) heap_init: At 4008C1C0 len 00013E40 (79 KiB): IRAM
I (284) spi_flash: detected chip: generic
I (287) spi_flash: flash io: dio
W (291) spi_flash: Detected size(4096k) larger than the size in the binary image header(2048k). Using the.
I (305) main_task: Started on CPU0
I (315) main_task: Calling app_main()
Hello world!
This is esp32 chip with 2 CPU core(s), WiFi/BTBLE, silicon revision v1.0, 2MB external flash
Minimum free heap size: 305360 bytes
Restarting in 10 seconds...
Restarting in 9 seconds...
Restarting in 8 seconds...
Restarting in 7 seconds...
Restarting in 6 seconds...
Restarting in 5 seconds...
Restarting in 4 seconds...
Restarting in 3 seconds...
Restarting in 2 seconds...
Restarting in 1 seconds...
Restarting in 0 seconds...
Restarting now.
ets Jun  8 2016 00:22:57
```
#### hello_world_main.c
```c
/*
 * SPDX-FileCopyrightText: 2010-2022 Espressif Systems (Shanghai) CO LTD
 *
 * SPDX-License-Identifier: CC0-1.0
 */

#include <stdio.h>
#include <inttypes.h>
#include "sdkconfig.h"
#include "freertos/FreeRTOS.h"
#include "freertos/task.h"
#include "esp_chip_info.h"
#include "esp_flash.h"
#include "esp_system.h"

void app_main(void)
{
    printf("Hello world!\n");

    /* Print chip information */
    esp_chip_info_t chip_info;
    uint32_t flash_size;
    esp_chip_info(&chip_info);
    printf("This is %s chip with %d CPU core(s), %s%s%s%s, ",
           CONFIG_IDF_TARGET,
           chip_info.cores,
           (chip_info.features & CHIP_FEATURE_WIFI_BGN) ? "WiFi/" : "",
           (chip_info.features & CHIP_FEATURE_BT) ? "BT" : "",
           (chip_info.features & CHIP_FEATURE_BLE) ? "BLE" : "",
           (chip_info.features & CHIP_FEATURE_IEEE802154) ? ", 802.15.4 (Zigbee/Thread)" : "");

    unsigned major_rev = chip_info.revision / 100;
    unsigned minor_rev = chip_info.revision % 100;
    printf("silicon revision v%d.%d, ", major_rev, minor_rev);
    if(esp_flash_get_size(NULL, &flash_size) != ESP_OK) {
        printf("Get flash size failed");
        return;
    }

    printf("%" PRIu32 "MB %s flash\n", flash_size / (uint32_t)(1024 * 1024),
           (chip_info.features & CHIP_FEATURE_EMB_FLASH) ? "embedded" : "external");

    printf("Minimum free heap size: %" PRIu32 " bytes\n", esp_get_minimum_free_heap_size());

    for (int i = 10; i >= 0; i--) {
        printf("Restarting in %d seconds...\n", i);
        vTaskDelay(1000 / portTICK_PERIOD_MS);
    }
    printf("Restarting now.\n");
    fflush(stdout);
    esp_restart();
}
```
