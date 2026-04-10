# 1. 环境搭建
## 1.1 配置 windows 功能
1. 配置 windows 功能
![[Pasted image 20260410103334.png|697]]

2. 重启生效

## 1.2 安装 wsl2 和 ubuntu22.04
1. 命令行中输入以下命令
```powershell
wsl --update
wsl --version # 验证安装
wsl --install -d Ubuntu-22.04
```

## 1.3 vscode 安装 wsl 插件
![[Pasted image 20260410103847.png]]

## 1.4 vscode 连接 wsl
#### 方法1：vscode 中点击 远程资源管理器
1. 点击左侧边栏红色方框部分
![[Pasted image 20260410104019.png]]

2. vscode 中出现下图内容表示连接成功
![[Pasted image 20260410104240.png]]

#### 方法2：登录 wsl2 后 powershell 中输入命令
```bash
code
```

# 2. 编译调试 C++ 代码
## 2.1 编译 C++ 代码
### 2.1.1 使用 gcc 编译
#### 方法1：命令行
```bash
g++ -std=<C++标准> -g <源文件路径> -o <可执行文件路径> \
    -I<头文件路径> \
    -L<库文件路径> \
    -l<库名>
```
- `-std`：指定 C++ 标准
- `-g`：生成调试信息
- `-o`：指定输出的可执行文件名
- `-I`：指定头文件路径
- `-L`：指定库文件路径
- `-l`：指定库名（eg：若库文件名是 `libvtk.so`，则写成 `-lvtk`，省去前面的 `lib` 和后缀）
- `-fPIC`：位置无关编码。在制作动态库时使用，其次在编译 `PIE` 可执行文件时必须使用 `PIC` 代码
- `-O<级别>`：优化级别

> **PIE（Position-Independent Executable）**：位置无关可执行文件，一种安全机制，让程序每次加载到内存的位置都不一样。若要生成 `PIE` 程序，则所有代码必须是位置无关（`PIC`）。现代64位 `linux` 全部默认开启 `PIE`。

---

**使用示例**：`gcc` 编译运行 `qt5` 项目
1. 安装 `qt5` 相关依赖
```bash
sudo apt install -y build-essential cmake qtbase5-dev qtchooser qt5-qmake qttools5-dev
```

2. 编写示例代码 `main.cpp`
```C++
#include <QApplication>
#include <QPushButton>

int main(int argc, char *argv[])
{
    QApplication app(argc, argv);

    QPushButton button("Hello Qt WSL!");
    button.resize(200, 100);
    button.show();

    return app.exec();
}
```

3. 使用 `gcc` 编译
``` bash
g++ -fPIC main.cpp -o qt-test \ 
-I/usr/include/x86_64-linux-gnu/qt5 \ 
-I/usr/include/x86_64-linux-gnu/qt5/QtCore \ 
-I/usr/include/x86_64-linux-gnu/qt5/QtGui \ 
-I/usr/include/x86_64-linux-gnu/qt5/QtWidgets \ 
-lQt5Core -lQt5Gui -lQt5Widgets
# 可以发现这样执行头文件路径、链接库文件的方式较为繁琐，可考虑使用 pkg-config 简化
```

4. 运行程序
```C++
./qt-test
```

5. 最终效果
![[Pasted image 20260410135812.png]]

#### 方法2：vscode 
1. 示例代码：在 [[#方法1：命令行]] 完整示例 2. 中

2. 配置 `IntelliSence`：`Ctrl +Shift + p` 打开命令面板
![[Pasted image 20260410142041.png|449]]
在包含路径中输入头文件路径
![[Pasted image 20260410142427.png]]

3. 配置 `tasks.json`：`vscode` 右上角选择 “运行 C/C++ 文件”
![[Pasted image 20260410143125.png]]
![[Pasted image 20260410143130.png]]
此时出现错误，因为我们还没进行头文件路径执行、链接库等操作
![[Pasted image 20260410143135.png]]
打开 `tasks.json`
![[Pasted image 20260410143411.png]]
指定头文件路径，链接库
![[Pasted image 20260410143543.png]]
重新点击`vscode` 右上角 “运行 C/C++ 文件”

> **tasks.json**：编译任务文件，`vscode` 编译代码用 配置文件
> 
> **c_cpp_properties.json**：`C++` 编辑配置文件（配置 `IntelliSence`时的相关信息就在这里）

### 2.1.2 使用 cmake 编译（推荐）
无论是使用 命令行 还是 `vscode` 都得先编写 `CMakeLists.txt` 文件，该文件的目标是编译链接 `Qt` 库进行简单的窗口展示
```CMakeLists.txt
cmake_minimum
```
#### 方法1：命令行

#### 方法2：vscode 

## 2.2 调试 C++ 代码
### 2.2.1 使用 命令行 调试
1. 配置调试信息、优化级别：以 `gcc` 为例，增加 `-g` 选项，`-O0`

2. 使用 `gdb` 进行调试
```bash
gdb <可执行文件/core dump文件> # 启动 gdb 并加载程序 / core dump
gdb -p <PID> # 启动 gdb 并附加到正在运行的进程
```

3. `gdb` 常用操作
```bash
l # 查看源码
bt # 查看调用栈
f # 切换栈帧
b # 打断点
r # 运行/重新运行
n # 单步执行（不进入函数）
s # 单步执行（进入函数）
f # 从函数返回
c # 继续
q # 退出 gdb
p # 打印/修改变量
```

---

**使用示例**：使用 `gdb` 调试 `core dump`
```bash
# 1. 启动 gdb 并打开 core dump文件
gdb <core dump文件>
# 2. 查看调用栈信息
bt 
# 3. 查看崩溃点
# 4. 查看变量值
p <变量>
# 5. 修改后重新测试
r
# 6. 没问题后退出 gdb
q
```

> **core dump**：`core dump` 文件为程序崩溃时的内存快照，用于分析程序崩溃原因

### 2.2.2 使用 vscode 调试
`vscode` 新版 `C/C++` 插件无需手写 `launch.json` 就能一键调试了。使用流程如下图所示：
![[Pasted image 20260410155840.png]]
1. 打断点

2. 点击右上角 “调试 C/C++ 文件”

3. 上方出现调试面板：继续、逐过程、单步调试、单步跳出、重启、停止

4. 左侧用于查看：局部变量、监视变量变化、调用栈信息、断点信息等

5. 下方为终端输出，用于查看：日志信息

> launch.json：调试任务文件，`vscode` 调试代码用 配置文件

# 3. todo 编译调试 Java 代码
