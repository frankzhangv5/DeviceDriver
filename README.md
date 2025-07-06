# Device Proxy

本项目包含了Android Debug Bridge (ADB) 和 HarmonyOS Device Connector (HDC) 的多平台可执行程序和动态库文件。

## 文件目录结构

```
device-proxy/
├── adb/
│   ├── linux/
│   │   ├── adb                    # Linux平台ADB可执行文件
│   │   └── version.txt            # ADB版本信息
│   └── win/
│       ├── adb.exe                # Windows平台ADB可执行文件
│       ├── AdbWinApi.dll          # Windows ADB API动态库
│       ├── AdbWinUsbApi.dll       # Windows ADB USB API动态库
│       └── version.txt            # ADB版本信息
└── hdc/
    ├── linux/
    │   ├── hdc                    # Linux平台HDC可执行文件
    │   ├── libusb_shared.so       # Linux USB共享库
    │   └── version.txt            # HDC版本信息
    └── win/
        ├── hdc.exe                # Windows平台HDC可执行文件
        └── version.txt            # HDC版本信息
```

## 平台设置方法

### Linux 平台

#### 需要下载的文件
- `adb/linux/adb` - Linux平台ADB可执行文件
- `hdc/linux/hdc` - Linux平台HDC可执行文件  
- `hdc/linux/libusb_shared.so` - Linux USB共享库

#### ADB 设置

#### ADB 设置

1. **添加可执行权限**
   ```bash
   chmod +x adb/linux/adb
   ```

2. **设置环境变量**
   
   临时设置（当前会话有效）：
   ```bash
   export PATH=$PATH:$(pwd)/adb/linux
   ```
   
   永久设置（添加到 ~/.bashrc 或 ~/.zshrc）：
   ```bash
   echo 'export PATH=$PATH:'$(pwd)'/adb/linux' >> ~/.bashrc
   source ~/.bashrc
   ```

3. **验证安装**
   ```bash
   adb version
   ```

#### HDC 设置

1. **添加可执行权限**
   ```bash
   chmod +x hdc/linux/hdc
   chmod +x hdc/linux/libusb_shared.so
   ```

2. **设置环境变量**
   
   临时设置（当前会话有效）：
   ```bash
   export PATH=$PATH:$(pwd)/hdc/linux
   export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$(pwd)/hdc/linux
   ```
   
   永久设置（添加到 ~/.bashrc 或 ~/.zshrc）：
   ```bash
   echo 'export PATH=$PATH:'$(pwd)'/hdc/linux' >> ~/.bashrc
   echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:'$(pwd)'/hdc/linux' >> ~/.bashrc
   source ~/.bashrc
   ```

3. **验证安装**
   ```bash
   hdc version
   ```

### Windows 平台

#### 需要下载的文件
- `adb/win/adb.exe` - Windows平台ADB可执行文件
- `adb/win/AdbWinApi.dll` - Windows ADB API动态库
- `adb/win/AdbWinUsbApi.dll` - Windows ADB USB API动态库
- `hdc/win/hdc.exe` - Windows平台HDC可执行文件

#### ADB 设置

1. **设置环境变量**
   
   通过系统设置：
   - 右键"此电脑" → "属性" → "高级系统设置" → "环境变量"
   - 在"系统变量"中找到"Path"，点击"编辑"
   - 点击"新建"，添加ADB目录的完整路径（例如：`D:\device-proxy\adb\win`）
   - 点击"确定"保存所有对话框
   
   通过命令行（需要管理员权限）：
   ```cmd
   setx PATH "%PATH%;D:\device-proxy\adb\win" /M
   ```

2. **验证安装**
   ```cmd
   adb version
   ```

#### HDC 设置

1. **设置环境变量**
   
   通过系统设置：
   - 右键"此电脑" → "属性" → "高级系统设置" → "环境变量"
   - 在"系统变量"中找到"Path"，点击"编辑"
   - 点击"新建"，添加HDC目录的完整路径（例如：`D:\device-proxy\hdc\win`）
   - 点击"确定"保存所有对话框
   
   通过命令行（需要管理员权限）：
   ```cmd
   setx PATH "%PATH%;D:\device-proxy\hdc\win" /M
   ```

2. **验证安装**
   ```cmd
   hdc version
   ```

## 使用说明

### ADB 常用命令

```bash
# 查看连接的设备
adb devices

# 安装APK
adb install app.apk

# 卸载应用
adb uninstall com.example.app

# 推送文件到设备
adb push local_file /sdcard/

# 从设备拉取文件
adb pull /sdcard/file local_file

# 进入设备shell
adb shell
```

### HDC 常用命令

```bash
# 查看连接的设备
hdc list targets

# 安装HAP包
hdc install app.hap

# 卸载应用
hdc uninstall com.example.app

# 推送文件到设备
hdc file send local_file /data/local/tmp/

# 从设备拉取文件
hdc file recv /data/local/tmp/file local_file

# 进入设备shell
hdc shell
```

## 声明

**重要声明：**

本项目中的所有可执行程序和动态库文件均来自官方开源渠道：

- **ADB (Android Debug Bridge)** 来自 Google 官方 Android SDK Platform Tools
  - 官方仓库：https://github.com/aosp-mirror/platform_system_core
  - 许可证：Apache License 2.0

- **HDC (HarmonyOS Device Connector)** 来自华为官方 HarmonyOS SDK
  - 官方仓库：https://gitee.com/openharmony/developtools_hdc
  - 许可证：Apache License 2.0

所有文件均按照官方开源许可证条款进行分发和使用。使用前请确保遵守相应的开源许可证要求。

## 许可证

本项目遵循 Apache License 2.0 许可证。详情请参阅各工具的官方许可证文件。 