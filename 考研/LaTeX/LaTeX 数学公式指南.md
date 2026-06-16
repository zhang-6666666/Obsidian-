---
tags:
  - LaTeX
  - 数学
created: 2026-06-14
---

# LaTeX 数学公式指南

> **配合阅读**：[[考研/LaTeX/LaTeX 符号速查表|LaTeX 符号速查表]] — 写公式时快速翻查

## 引言

### LaTeX 是什么？

LaTeX 是一套数学公式排版语言，用简单的文本命令就能写出漂亮的数学公式。Obsidian 内置了 MathJax 渲染引擎，直接支持 LaTeX 数学公式。

### 在 Obsidian 里怎么写？

| 写法        | 效果           | 场景       |
| --------- | ------------ | -------- |
| `$...$`   | 行内公式，与文字混排   | 一句话里插入公式 |
| `$$...$$` | 块级公式，独占一行，居中 | 重要公式独立展示 |

**例子**：
- 行内：`已知 $f(x) = x^2 + 1$，求 $f'(x)$` → 已知 $f(x) = x^2 + 1$，求 $f'(x)$
- 块级：`$$\int_0^1 x^2 dx = \frac{1}{3}$$` 会居中独立显示
$$\int_0^1 x^2 dx = \frac{1}{3}$$
### 为什么考研要学？

考研数学笔记里要写大量公式——导数、积分、极限、矩阵。手写截图的笔记不好搜索、不好修改。用 LaTeX 写的公式纯文本可搜索，和笔记融为一体。

---

## 模块一：基本语法

### 核心要点

1. **所有公式**包在 `$` 或 `$$` 里
2. **花括号 `{}`** 用来"打包" — 告诉 LaTeX 哪些内容是一组的
3. **反斜杠 `\`** 是命令的开头 — `\frac`、`\sqrt`、`\alpha` 都是命令

### 花括号的三种用法

| 用法 | 例子 | 说明 |
|------|------|------|
| 命令参数 | `\frac{a}{b}` | `a` 和 `b` 是 `\frac` 的两个参数 |
| 限定范围 | `x^{2n}` | 上标不止一个字符时，用 `{}` 包起来 |
| 分组控制 | `{a+b}` | 把多个字符当作一个整体 |

```latex
$$x^10$$    % 错误：只有 1 是上标，后面 0 变回正常字
$$x^{10}$$  % 正确：整个 10 都是上标
```

### 注释

`%` 后面的内容不会被渲染，用来写备注。

---

## 模块二：上下标

| 语法 | 例子 | 渲染效果 |
|------|------|----------|
| `^` 上标 | `x^2` | $x^2$ |
| `_` 下标 | `a_n` | $a_n$ |
| 同时使用 | `a_n^2` 或 `a^2_n` | $a_n^2$ |
| 多字符 | `x^{10}` `a_{ij}` | $x^{10}$、$a_{ij}$ |

**常见场景**：
```latex
$$e^{x+y}$$          % e 的 x+y 次方
$$\sum_{n=1}^{\infty}$$  % 求和符号的上下限
$$\int_{0}^{1}$$         % 积分的上下限
```

---

## 模块三：分数与根号

### 分数

| 语法              | 效果                      |                           |
| --------------- | ----------------------- | ------------------------- |
| `\frac{分子}{分母}` | $$\frac{a}{b}$$         |                           |
| 嵌套分数            | `\frac{\frac{a}{b}}{c}` | $$\frac{\frac{a}{b}}{c}$$ |

```latex
$$\frac{dy}{dx}$$                  % 导数
$$\frac{1}{x^2 + 1}$$             % 有理分式
$$\lim_{x \to 0} \frac{\sin x}{x} = 1$$  % 重要极限
```

### 根号

| 语法 | 效果 |
|------|------|
| `\sqrt{x}` | $\sqrt{x}$ |
| `\sqrt[n]{x}` | $\sqrt[n]{x}$ |

```latex
$$\sqrt{x^2 + y^2}$$     % 平方根
$$\sqrt[3]{8} = 2$$      % 立方根
$$\sqrt{\frac{a}{b}}$$   % 分数在根号里
```

---

## 模块四：希腊字母

> 英文名前面加 `\` 就是对应的希腊字母。首字母大写 = 大写希腊字母。

### 常用小写

| 命令 | 字母 | 命令 | 字母 | 命令 | 字母 |
|------|:---:|------|:---:|------|:---:|
| `\alpha` | $\alpha$ | `\beta` | $\beta$ | `\gamma` | $\gamma$ |
| `\delta` | $\delta$ | `\epsilon` | $\epsilon$ | `\varepsilon` | $\varepsilon$ |
| `\theta` | $\theta$ | `\lambda` | $\lambda$ | `\mu` | $\mu$ |
| `\pi` | $\pi$ | `\sigma` | $\sigma$ | `\phi` | $\phi$ |
| `\varphi` | $\varphi$ | `\omega` | $\omega$ | `\rho` | $\rho$ |

### 常用大写

| 命令 | 字母 | 命令 | 字母 | 命令 | 字母 |
|------|:---:|------|:---:|------|:---:|
| `\Gamma` | $\Gamma$ | `\Delta` | $\Delta$ | `\Theta` | $\Theta$ |
| `\Lambda` | $\Lambda$ | `\Pi` | $\Pi$ | `\Sigma` | $\Sigma$ |
| `\Phi` | $\Phi$ | `\Omega` | $\Omega$ | `\Psi` | $\Psi$ |

> **注意**：有些大写希腊字母和英文字母一样（如 Alpha = A），所以没有单独的 `\Alpha` 命令。

---

## 模块五：运算符

### 基本运算

| 语法 | 效果 | 说明 |
|------|:---:|------|
| `+` `-` | $+$ $-$ | 直接输入 |
| `\times` | $\times$ | 叉乘 |
| `\cdot` | $\cdot$ | 点乘 |
| `\div` | $\div$ | 除号 |
| `\pm` | $\pm$ | 正负号 |
| `\mp` | $\mp$ | 负正号 |
| `\ast` | $\ast$ | 星号 |

### 大型运算符

| 语法 | 行内效果 | 块级效果 | 说明 |
|------|:---:|:---:|------|
| `\sum` | $\sum$ | $$\sum$$ | 求和 |
| `\prod` | $\prod$ | $$\prod$$ | 连乘 |
| `\int` | $\int$ | $$\int$$ | 积分 |
| `\iint` | $\iint$ | $$\iint$$ | 二重积分 |
| `\oint` | $\oint$ | $$\oint$$ | 环路积分 |
| `\lim` | $\lim$ | $$\lim$$ | 极限 |

### 带上限下限

```latex
$$\sum_{n=1}^{\infty} \frac{1}{n^2} = \frac{\pi^2}{6}$$     % 级数求和
$$\int_{0}^{1} x^2 \, dx = \frac{1}{3}$$                     % 定积分
$$\lim_{x \to 0} \frac{\sin x}{x} = 1$$                      % 极限
```

> `\,` 是加一个小空格，让 dx 和前面不贴在一起，更好看。

---

## 模块六：关系符号

| 语法          |     效果      | 语法                |        效果         |
| ----------- | :---------: | ----------------- | :---------------: |
| `=`         |     $=$     | `\neq`            |      $\neq$       |
| `<` `>`     |   $<$ $>$   | `\leq` `\geq`     |   $\leq$ $\geq$   |
| `\approx`   |  $\approx$  | `\equiv`          |     $\equiv$      |
| `\sim`      |   $\sim$    | `\propto`         |     $\propto$     |
| `\ll` `\gg` | $\ll$ $\gg$ | `\Rightarrow`     |   $\Rightarrow$   |
| `\to`       |    $\to$    | `\Leftrightarrow` | $\Leftrightarrow$ |
| `\because`  | $\because$  | `\therefore`      |   $\therefore$    |

---

## 模块七：括号与定界符

### 普通括号

直接输入：`( ) [ ] { }`。但 `{` 和 `}` 是 LaTeX 特殊字符，需要用 `\{` 和 `\}`。

### 自适应括号 — 最重要

用 `\left` 和 `\right` 让括号自动匹配内容高度：

```latex
$$(\frac{a}{b})$$                    % 括号太小，包不住分数
$$\left(\frac{a}{b}\right)$$        % 自适应大小，好看！
```

| 命令 | 效果 |
|------|------|
| `\left( ... \right)` | 自适应圆括号 |
| `\left[ ... \right]` | 自适应方括号 |
| `\left\{ ... \right\}` | 自适应花括号 |
| `\left\| ... \right\|` | 自适应范数 / 绝对值 |

**注意**：`\left` 和 `\right` 必须成对出现。如果只需要单边，用 `\right.` 或 `\left.` 作为隐形占位符：

```latex
$$\left. \frac{dy}{dx} \right|_{x=0}$$    % 导数在某点的值
```

---

## 模块八：常用函数

> 函数名要用 `\` 前缀，否则会被当作变量斜体显示。

| 命令 | 效果 | 命令 | 效果 |
|------|:---:|------|:---:|
| `\sin` | $\sin$ | `\cos` | $\cos$ |
| `\tan` | $\tan$ | `\cot` | $\cot$ |
| `\arcsin` | $\arcsin$ | `\arccos` | $\arccos$ |
| `\ln` | $\ln$ | `\log` | $\log$ |
| `\lim` | $\lim$ | `\max` | $\max$ |
| `\min` | $\min$ | `\exp` | $\exp$ |

```latex
$$\sin^2 x + \cos^2 x = 1$$
$$\ln(ab) = \ln a + \ln b$$
$$\lim_{x \to 0} \frac{\ln(1+x)}{x} = 1$$
```

---

## 模块九：矩阵

用 `\begin{matrix}...\end{matrix}` 环境。行内用 `&` 分列，用 `\\` 换行。

| 环境 | 括号类型 |
|------|----------|
| `matrix` | 无括号 |
| `pmatrix` | 圆括号 `( )` |
| `bmatrix` | 方括号 `[ ]` |
| `Bmatrix` | 花括号 `{ }` |
| `vmatrix` | 竖线 `| |` |
| `Vmatrix` | 双竖线 `|| ||` |

**例子**：

```latex
$$\begin{pmatrix}
a & b \\
c & d
\end{pmatrix}$$
```

渲染为：

$$
\begin{pmatrix}
a & b \\
c & d
\end{pmatrix}
$$

**考研常用 — 行列式**：

```latex
$$\begin{vmatrix}
a_{11} & a_{12} \\
a_{21} & a_{22}
\end{vmatrix}
= a_{11}a_{22} - a_{12}a_{21}$$
```

---

## 模块十：多行公式

### aligned — 多行对齐

在 `$$` 里用 `\begin{aligned}`，`&` 指定对齐点，`\\` 换行：

```latex
$$\begin{aligned}
f(x) &= x^3 + 2x^2 - 5x + 1 \\
f'(x) &= 3x^2 + 4x - 5 \\
f''(x) &= 6x + 4
\end{aligned}$$
```

渲染为：

$$
\begin{aligned}
f(x) &= x^3 + 2x^2 - 5x + 1 \\
f'(x) &= 3x^2 + 4x - 5 \\
f''(x) &= 6x + 4
\end{aligned}
$$

### cases — 分段函数

```latex
$$f(x) = \begin{cases}
x^2, & x \geq 0 \\
-x, & x < 0
\end{cases}$$
```

渲染为：

$$
f(x) = \begin{cases}
x^2, & x \geq 0 \\
-x, & x < 0
\end{cases}
$$

---

## 模块十一：考研高数常用示例

> 把前面学的组合起来，下面都是考研里频繁出现的写法。

### 导数

```latex
$$f'(x) = \lim_{h \to 0} \frac{f(x+h) - f(x)}{h}$$
$$\frac{d}{dx} \left( x^n \right) = n x^{n-1}$$
```
$$f'(x) = \lim_{h \to 0} \frac{f(x+h) - f(x)}{h}$$
$$\frac{d}{dx} \left( x^n \right) = n x^{n-1}$$
### 偏导数

```latex
$$\frac{\partial z}{\partial x} \quad \frac{\partial^2 z}{\partial x \partial y}$$
$$f_x = \frac{\partial f}{\partial x}$$
```
$$\frac{\partial z}{\partial x} \quad \frac{\partial^2 z}{\partial x \partial y}$$
$$f_x = \frac{\partial f}{\partial x}$$
### 极限

```latex
$$\lim_{x \to \infty} \left( 1 + \frac{1}{x} \right)^x = e$$
$$\lim_{x \to 0} \frac{\sin x}{x} = 1$$
```
$$\lim_{x \to \infty} \left( 1 + \frac{1}{x} \right)^x = e$$
$$\lim_{x \to 0} \frac{\sin x}{x} = 1$$
### 积分

```latex
$$\int_a^b f(x)\, dx = F(b) - F(a)$$
$$\iint_D f(x,y)\, dx\, dy$$
$$\int_{-\infty}^{+\infty} e^{-x^2}\, dx = \sqrt{\pi}$$
```
$$\int_a^b f(x)\, dx = F(b) - F(a)$$
$$\iint_D f(x,y)\, dx\, dy$$
$$\int_{-\infty}^{+\infty} e^{-x^2}\, dx = \sqrt{\pi}$$
### 麦克劳林展开

```latex
$$f(x) = f(0) + f'(0)x + \frac{f''(0)}{2!} x^2 + \cdots + \frac{f^{(n)}(0)}{n!} x^n + o(x^n)$$
```
$$f(x) = f(0) + f'(0)x + \frac{f''(0)}{2!} x^2 + \cdots + \frac{f^{(n)}(0)}{n!} x^n + o(x^n)$$
### 偏导数 + 全微分

```latex
$$dz = \frac{\partial z}{\partial x} dx + \frac{\partial z}{\partial y} dy$$
```
   $$dz = \frac{\partial z}{\partial x} dx + \frac{\partial z}{\partial y} dy$$
---

## 速查入口

写公式时忘了符号，直接打开：[[考研/LaTeX/LaTeX 符号速查表|LaTeX 符号速查表]]

## 实际应用示例

[[考研/高数/多元函数微分学|多元函数微分学]] 笔记中可逐步用 LaTeX 改写公式。
