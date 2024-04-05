# AIoT_one
AIoT第一堂
## 認識晶片  YD-ESP32-S3-EYE 
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

### 準備工作

- 閱讀 [ESP-IDF程式指南](https://espressif-docs.readthedocs-hosted.com/projects/esp-idf/zh-cn/latest/get-started/index.html)，參考對應章節，設定工具鏈；
- windows 可以使用 https://dl.espressif.com/dl/esp-idf/
- 準備 USB Type-C 線，用於連接 PC 和 YD-ESP32-S3-EYE 開發板；
- 選擇適合開發環境的工具，例如 Terminal (Linux/MacOS) 或 MinGW (Windows) 等。

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
