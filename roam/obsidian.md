---
tags:
  - tools
---
# 1 环境配置
## 1.1 图片相关
### 1.1.1 设置图片存放文件夹

1. 设置 - 文件与链接 - 附件默认存放路径 - 当前文件所在文件夹下指定的子文件夹
2. 子文件夹名称 设置为 `assets`

### 1.1.2 自动清理未使用图片

1. 设置 - 第三方插件 - 安全模式 - 关闭
2. 社区插件市场 - `Clear Unused Images`
3. 修改 `Clear Unused Images` 选项
![[Pasted image 20260511114300.png|524]]
4. 在命令面板使用

## 1.2 标题自动编号

1. 下载插件 `Number Headings`
2. 设置如下
![[Pasted image 20260511114956.png|413]]

## 1.3 给表格加上横向滑动条

1. 设置 - 外观 - CSS代码片段
![[Pasted image 20260416105633.png]]
2. 选择文件夹，新建 css 文件，写入以下内容
```css
.markdown-source-view div.cm-embed-block.cm-table-widget {
    overflow-x: auto;
}
.markdown-source-view div.cm-embed-block.cm-table-widget > div > table {
    width: max-content !important;
}
.markdown-reading-view .markdown-preview-view.markdown-rendered table {
    width: max-content !important;
}
```
3. 开启 table-scroll 后刷新

# 2 快捷键

| 作用    | 快捷键          |
| ----- | ------------ |
| 搜索文件  | `C-o`        |
| 执行命令  | `C-p`        |
| 切换标签页 | `C-<数字>`     |
| 多光标   | `Alt-<鼠标左键>` |

# 3 语法
## 3.1 markdown 书写规范

**空行**：
1. 标题前后各空一行
2. 一段内容结束空一行

**空格**：
1. 中文内容中的英文和数字前后加空格
2. 粗体、斜体、高亮文本前后加空格

## 3.2 基础

```cpp
# <标题>            // 标题（1-6级）
#<标签>             // 标签

**<文字>**          // 粗体
==<文字>==          // 高亮
*<文字>*            // 斜体   
~~<文字>~~          // 删除线

-                   // 无序列表
1.                  // 有序列表
- [ ]               // 任务列表

[<文字描述>](<链接>) // 外部链接

%%<内容>%%          // 注释
`<代码>`            // 代码块
>                   // 引用

// 提示框     
>[!<CallOut>]-      // - 可选，用于折叠
>>                  // 提示框中多层嵌套
```

**CallOut 官方支持如下**：
- note
- abstract, summary, tldr
- info, todo
- tip, hint, important
- success, check, done
- question, help, faq
- warning, caution, attention
- failure, fail, missing
- danger, error
- bug
- example
- quote, cite

## 3.3 内部链接

```cpp
[[<文件>]]          // 链接到文件
[[##<标题>]]        // 链接到标题
[[<文件>#<标题>]]   // 链接到标题
[[^^<段落>]]        // 链接到段落
[[<链接>|<别名>]]   // 给链接起别名
![[<链接>]]         // 将链接内容嵌入到当前笔记
```

## 3.4 笔记属性

设置 - 编辑器 - 笔记属性 -> 显示
```cpp
---       // 文件开头添加笔记属性
```

## 3.5 自定义 CSS 样式

`ctrl + shift + i` 

# 4 关系图谱与笔记联动

实现左侧点击关系图谱中节点时，右侧自动显示对应笔记
1. 打开关系图谱
2. 右上角选择 左右分屏
3. 右键 关系图谱标签页 选择 锁定


# 5 数学（latex）

| 类型   | 语法        | 示例                     | 渲染效果               |
| ---- | --------- | ---------------------- | ------------------ |
| 行内公式 | `$...$`   | `$E=mc^2$`             | $E=mc^2$           |
| 块级公式 | `$$...$$` | `$$\sum_{i=1}^n x_i$$` | $\sum_{i=1}^n x_i$ |

| 符号      | LaTeX 代码                         | 示例                               |
| ------- | -------------------------------- | -------------------------------- |
| 分数      | `\frac{a}{b}`                    | $\frac{a}{b}$                    |
| 平方 / 上标 | `x^2`                            | $x^2$                            |
| 下标      | `x_i`                            | $x_i$​                           |
| 根号      | `\sqrt{x}`                       | $\sqrt{x}$​                      |
| 求和      | `\sum_{i=1}^n`                   | $\sum_{i=1}^n$​                  |
| 积分      | `\int_a^b`                       | $\int_a^b$                       |
| 极限      | `\lim_{x\to\infty}`              | $\lim_{x\to\infty}​$             |
| 加减乘除    | `+ - \times \div`                | $+ - \times \div$                |
| 不等号     | `\le \ge \ne`                    | $\le \ge \ne$                    |
| 希腊字母    | `\alpha \beta \gamma \theta \pi` | $\alpha \beta \gamma \theta \pi$ |

| 功能   | 代码模板                                               | 渲染效果                                            |
| ---- | -------------------------------------------------- | ----------------------------------------------- |
| 多行对齐 | `$$\begin{aligned}a&=b\\c&=d\end{aligned}$$`       | $\begin{aligned}a&=b\\c&=d\end{aligned}$        |
| 矩阵   | `$$\begin{pmatrix}1&2\\3&4\end{pmatrix}$$`         | $\begin{pmatrix}1&2\\3&4\end{pmatrix}$          |
| 行列式  | `$$\begin{vmatrix}a&b\\c&d\end{vmatrix}$$`         | $\begin{vmatrix}a&b\\c&d\end{vmatrix}$          |
| 分段函数 | `$$f(x)=\begin{cases}x&x\ge0\\-x&x<0\end{cases}$$` | $f(x)=\begin{cases}x&x\ge0\\-x&x<0\end{cases}$​ |
