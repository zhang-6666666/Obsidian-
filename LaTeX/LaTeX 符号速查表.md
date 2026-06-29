---
tags:
  - LaTeX
  - 速查表
  - 数学
created: 2026-06-14
---

# LaTeX 符号速查表

> 教学指南：[[LaTeX 数学公式指南|LaTeX 数学公式指南]]

---

## 基本语法

| 语法 | 说明 |
|------|------|
| `$...$` | 行内公式 |
| `$$...$$` | 块级公式 |
| `{ }` | 花括号分组 |
| `%` | 注释 |

## 上下标

| 命令 | 效果 |
|------|:---:|
| `x^2` | $x^2$ |
| `a_n` | $a_n$ |
| `x^{10}` | $x^{10}$ |
| `a_{ij}` | $a_{ij}$ |

## 分数与根号

| 命令            | 效果            |
| ------------- | ------------- |
| `\frac{a}{b}` | $\frac{a}{b}$ |
| `\sqrt{x}`    | $\sqrt{x}$    |
| `\sqrt[n]{x}` | $\sqrt[n]{x}$ |

## 希腊字母

| 命令 | 效果 | 命令 | 效果 |
|------|:---:|------|:---:|
| `\alpha` | $\alpha$ | `\beta` | $\beta$ |
| `\gamma` | $\gamma$ | `\delta` | $\delta$ |
| `\epsilon` | $\epsilon$ | `\varepsilon` | $\varepsilon$ |
| `\zeta` | $\zeta$ | `\eta` | $\eta$ |
| `\theta` | $\theta$ | `\vartheta` | $\vartheta$ |
| `\lambda` | $\lambda$ | `\mu` | $\mu$ |
| `\nu` | $\nu$ | `\xi` | $\xi$ |
| `\pi` | $\pi$ | `\varpi` | $\varpi$ |
| `\rho` | $\rho$ | `\sigma` | $\sigma$ |
| `\tau` | $\tau$ | `\phi` | $\phi$ |
| `\varphi` | $\varphi$ | `\chi` | $\chi$ |
| `\psi` | $\psi$ | `\omega` | $\omega$ |

| 大写 | 效果 | 大写 | 效果 |
|------|:---:|------|:---:|
| `\Gamma` | $\Gamma$ | `\Delta` | $\Delta$ |
| `\Theta` | $\Theta$ | `\Lambda` | $\Lambda$ |
| `\Xi` | $\Xi$ | `\Pi` | $\Pi$ |
| `\Sigma` | $\Sigma$ | `\Upsilon` | $\Upsilon$ |
| `\Phi` | $\Phi$ | `\Psi` | $\Psi$ |
| `\Omega` | $\Omega$ | | |

## 运算符

| 命令       |    效果    | 命令         |     效果     |
| -------- | :------: | ---------- | :--------: |
| `+` `-`  | $+$ $-$  | `\times`   |  $\times$  |
| `\cdot`  | $\cdot$  | `\div`     |   $\div$   |
| `\pm`    |  $\pm$   | `\mp`      |   $\mp$    |
| `\ast`   |  $\ast$  | `\star`    |  $\star$   |
| `\circ`  | $\circ$  | `\bullet`  | $\bullet$  |
| `\oplus` | $\oplus$ | `\otimes`  | $\otimes$  |
| `\sum`   |  $\sum$  | `\prod`    |  $\prod$   |
| `\int`   |  $\int$  | `\iint`    |  $\iint$   |
| `\iiint` | $\iiint$ | `\oint`    |  $\oint$   |
| `\lim`   |  $\lim$  | `\partial` | $\partial$ |
| `\nabla` | $\nabla$ | `\infty`   |  $\infty$  |

## 关系符号

| 命令 | 效果 | 命令 | 效果 |
|------|:---:|------|:---:|
| `=` | $=$ | `\neq` | $\neq$ |
| `<` `>` | $<$ $>$ | `\leq` `\geq` | $\leq$ $\geq$ |
| `\ll` `\gg` | $\ll$ $\gg$ | `\approx` | $\approx$ |
| `\equiv` | $\equiv$ | `\sim` | $\sim$ |
| `\propto` | $\propto$ | `\simeq` | $\simeq$ |
| `\to` | $\to$ | `\Rightarrow` | $\Rightarrow$ |
| `\Leftrightarrow` | $\Leftrightarrow$ | `\iff` | $\iff$ |
| `\because` | $\because$ | `\therefore` | $\therefore$ |
| `\forall` | $\forall$ | `\exists` | $\exists$ |
| `\in` | $\in$ | `\notin` | $\notin$ |
| `\subset` | $\subset$ | `\subseteq` | $\subseteq$ |
| `\cap` | $\cap$ | `\cup` | $\cup$ |

## 括号与定界符

| 命令 | 效果 | 命令 | 效果 |
|------|------|------|------|
| `( )` | $( )$ | `[ ]` | $[ ]$ |
| `\{ \}` | $\{ \}$ | `\|` | $\|$ |
| `\langle \rangle` | $\langle \rangle$ | `\lceil \rceil` | $\lceil \rceil$ |
| `\left( ... \right)` | 自适应 | `\left. \right\|` | 单边 |

## 常用函数

| 命令 | 效果 | 命令 | 效果 |
|------|:---:|------|:---:|
| `\sin` | $\sin$ | `\cos` | $\cos$ |
| `\tan` | $\tan$ | `\cot` | $\cot$ |
| `\sec` | $\sec$ | `\csc` | $\csc$ |
| `\arcsin` | $\arcsin$ | `\arccos` | $\arccos$ |
| `\arctan` | $\arctan$ | `\ln` | $\ln$ |
| `\log` | $\log$ | `\exp` | $\exp$ |
| `\max` | $\max$ | `\min` | $\min$ |
| `\deg` | $\deg$ | `\dim` | $\dim$ |
| `\gcd` | $\gcd$ | `\det` | $\det$ |

## 矩阵环境

| 环境 | 括号 | 环境 | 括号 |
|------|------|------|------|
| `matrix` | 无 | `pmatrix` | `( )` |
| `bmatrix` | `[ ]` | `Bmatrix` | `{ }` |
| `vmatrix` | `\| \|` | `Vmatrix` | `\|\| \|\|` |

```latex
\begin{pmatrix}
a & b \\
c & d
\end{pmatrix}
```

## 多行公式环境

| 环境 | 用途 |
|------|------|
| `aligned` | 多行对齐（`&` 对齐点，`\\` 换行） |
| `cases` | 分段函数 |

## 箭头与重音

| 命令 | 效果 | 命令 | 效果 |
|------|:---:|------|:---:|
| `\vec{a}` | $\vec{a}$ | `\hat{a}` | $\hat{a}$ |
| `\tilde{a}` | $\tilde{a}$ | `\bar{a}` | $\bar{a}$ |
| `\dot{a}` | $\dot{a}$ | `\ddot{a}` | $\ddot{a}$ |
| `\overline{abc}` | $\overline{abc}$ | `\underline{abc}` | $\underline{abc}$ |
| `\overrightarrow{AB}` | $\overrightarrow{AB}$ | `\widehat{abc}` | $\widehat{abc}$ |

## 空格与省略号

| 命令 | 效果 | 说明 |
|------|:---:|------|
| `\,` | $a\,b$ | 小空格 |
| `\;` | $a\;b$ | 中空格 |
| `\quad` | $a\quad b$ | 大空格 |
| `\qquad` | $a\qquad b$ | 更大空格 |
| `\dots` | $\dots$ | 省略号（靠下） |
| `\cdots` | $\cdots$ | 省略号（居中） |
| `\vdots` | $\vdots$ | 竖省略号 |
| `\ddots` | $\ddots$ | 斜省略号 |

## 杂项

| 命令 | 效果 | 说明 |
|------|:---:|------|
| `\text{...}` | 普通文字 | 在数学模式中插入文本 |
| `\mathrm{...}` | 直立体 | 非斜体字母 |
| `\mathbb{R}` | $\mathbb{R}$ | 空心字（实数集） |
| `\mathcal{L}` | $\mathcal{L}$ | 花体字 |
| `\prime` 或 `'` | $'$ | 导数撇号 |
| `\circ` | $\circ$ | 度 / 复合 |

---

## 考研高频速写

| 场景 | 代码 |
|------|------|
| 导数 | `f'(x)` `\frac{dy}{dx}` `f^{(n)}(x)` |
| 偏导数 | `\frac{\partial z}{\partial x}` |
| 极限 | `\lim_{x \to a} f(x)` |
| 积分 | `\int_a^b f(x)\, dx` |
| 二重积分 | `\iint_D f(x,y)\, dx\, dy` |
| 求和 | `\sum_{n=1}^{\infty} a_n` |
| 无穷大 | `\infty` |
| 约等于 | `\approx` |
| 正负号 | `\pm` |
| 因为/所以 | `\because` `\therefore` |
| 向量 | `\vec{a}` |
| 矩阵 | `\begin{pmatrix} a & b \\ c & d \end{pmatrix}` |
| 分段函数 | `\begin{cases} ... \end{cases}` |
| 实数集 | `\mathbb{R}` |
| 自然常数 | `e`（普通字母即可） |
