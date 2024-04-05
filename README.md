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

### Hands on
Creating a "Hellow world" example

   20  cd esp
   21  git clone --recursive https://github.com/espressif/esp-who.git
   26  cd esp-who/
   30  git clone --recursive https://github.com/espressif/esp-idf.git
   32  cd esp-idf/
   34  ./install.sh
   35  more export.sh
   36  source export.sh
   37  source ./export.sh
   38  pwd
   39  cd ..
   40  cp -r $IDF_PATH/examples/get-started/hello_world .
   42  cd hello_world/
   49  idf.py menuconfig
   51  idf.py build



### 軟體獲取

開啟終端機（例如 Linux 環境下的 Terminal），將軟體程式碼複製到本機：

```
git clone --recursive https://github.com/espressif/esp-who.git
```

執行以上指令會預設產生一個 `esp-who` 的資料夾。

> 注意不要忘記 `--recursive` 選項。 如果你在克隆 ESP-IDF 時沒有帶這個選項，你還需要運進入對應資料夾中，執行以下指令下載對應的子模組：
```
git submodule update --init --recursive
```

### 設定路徑

請參考[設定路徑](https://docs.espressif.com/projects/esp-idf/zh_CN/v3.1.1/get-started/index.html#get-started-setup-path)章節，將`IDF_PATH ` 設定為`esp-who/esp-idf`。
