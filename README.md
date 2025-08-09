# WxMiniGameTools
## 微信小游戏工具集

1. [unveilr](https://github.com/r3x5ur/unveilr)
2. [brotli.exe](https://github.com/google/brotli/releases/tag/v1.1.0)
3. [ghidra](https://github.com/NationalSecurityAgency/ghidra)
4. [ghidra-wasm-plugin](https://github.com/nneonneo/ghidra-wasm-plugin)
5. [Il2CppDumper](https://github.com/Perfare/Il2CppDumper/releases/tag/v6.7.40)
6. [ILSpy](https://github.com/icsharpcode/ILSpy)
7. [watb](https://github.com/WebAssembly/wabt)
8. [unityweb.exe](https://github.com/jozsefsallai/unityweb/releases/tag/v1.0.2)
9. [uwdtool](https://github.com/SiMaLaoShi/UWDTool_Tuanjie)
10. [twiggy ](https://github.com/rustwasm/twiggy)

### unverilr

### brotli

```sh
unveilr wx -f  "D:\WeChat Files\WeChat Files\Applet\wxxxxxxx\34" 解包applet的内容
```

## 命令说明

### 1. Brotli 压缩/解压工具

#### Brotli 解压

```bash
bash
D:\GitHub\WxMiniGameTools\bin\brotli.exe -d "%1"
```

**功能**: 解压 Brotli 格式的压缩文件
**参数**: `-d` 表示解压模式
**用途**: 微信小游戏中的资源文件通常使用 Brotli 压缩，此命令用于解压这些文件
**输出**: 生成解压后的原始文件

#### Brotli 压缩

```bash
bash
D:\GitHub\WxMiniGameTools\bin\brotli.exe "%1"
```

**功能**: 将文件压缩为 Brotli 格式
**用途**: 重新打包微信小游戏资源时使用
**输出**: 生成 `.br` 压缩文件

------

### 2. WebAssembly 处理工具

#### WebAssembly 二进制转文本

```bash
bash
K:\wabt-1.0.35\bin\wasm2wat.exe "%1" -o "%1".wat
```

**功能**: 将 WebAssembly 二进制文件 (.wasm) 转换为可读的文本格式 (.wat)
**参数**: `-o` 指定输出文件名
**用途**: 分析和理解 WebAssembly 代码结构
**输出**: 生成 `.wat` 文本文件，可用文本编辑器查看

#### WebAssembly 文本转二进制

```bash
bash
K:\wabt-1.0.35\bin\wat2wasm.exe "%1" -o "%1".wasm
```

**功能**: 将 WebAssembly 文本文件 (.wat) 编译为二进制格式 (.wasm)
**用途**: 修改 WebAssembly 代码后重新编译
**输出**: 生成可执行的 `.wasm` 二进制文件

------

### 3. 微信小程序解包工具

```bash
bash
D:\GitHub\WxMiniGameTools\bin\unveilr.exe wx -f "%1"
```

**功能**: 解包微信小程序/小游戏的包体文件
**参数**:

- `wx`: 指定微信平台
- `-f`: 指定输入文件路径
  **用途**: 提取小程序的源代码、资源文件等
  **示例**:

```bash
bash
unveilr wx -f "D:\WeChat Files\WeChat Files\Applet\wxxxxxxx\34"
```

**输出**: 在指定目录生成解包后的文件结构

------

### 4. WebAssembly 代码分析工具

```bash
bash
D:\GitHub\WxMiniGameTools\bin\run_twiggy.bat "%1"
```

**功能**: 分析 WebAssembly 文件的代码大小和结构
**用途**:

- 查看代码占用空间分布
- 找出体积较大的函数和模块
- 优化 WebAssembly 文件大小
  **输出**: 生成详细的代码分析报告

------

### 5. Unity WebData 处理工具

#### Unity WebData 打包

```bash
bash
D:\GitHub\WxMiniGameTools\bin\uwdtool.exe --pack -i "%1" -o "%1".bin
```

**功能**: 将 Unity 资源文件打包为 WebData 格式
**参数**:

- `--pack`: 打包模式
- `-i`: 输入目录路径
- `-o`: 输出文件路径
  **用途**: 重新打包修改后的 Unity 游戏资源
  **输出**: 生成 `.bin` 格式的 WebData 文件

#### Unity WebData 解包

```bash
bash
D:\GitHub\WxMiniGameTools\bin\uwdtool.exe --unpack -i "%1" -o "%1"_unpack
```

**功能**: 解包 Unity WebData 文件
**参数**:

- `--unpack`: 解包模式
- `-i`: 输入文件路径
- `-o`: 输出目录路径
  **用途**: 提取 Unity 游戏中的资源文件、脚本等
  **输出**: 在指定目录生成解包后的资源文件

------

## 完整工作流程示例

### 微信小游戏逆向分析流程

```
获取小游戏包
unveilr 解包
brotli 解压资源
uwdtool 解包Unity资源
wasm2wat 转换WebAssembly
twiggy 分析代码结构
使用Ghidra等工具进一步分析
```

### 实际操作步骤

1. **获取小游戏文件**

```bash
bash   # 微信小游戏缓存路径通常在：
   # C:\Users\用户名\Documents\WeChat Files\Applet\
   
```

1. **解包小游戏**

```bash
bash   unveilr.exe wx -f "小游戏包路径"
   
```

1. **解压 Brotli 文件**

```bash
bash   brotli.exe -d 压缩文件.br
   
```

1. **处理 Unity 资源**

```bash
bash   # 解包
   uwdtool.exe --unpack -i game.data -o game_unpacked
   
   # 修改后重新打包
   uwdtool.exe --pack -i game_unpacked -o game_new.data
   
```

1. **分析 WebAssembly**

```bash
bash   # 转换为可读格式
   wasm2wat.exe game.wasm -o game.wat
   
   # 分析代码结构
   run_twiggy.bat game.wasm
```
