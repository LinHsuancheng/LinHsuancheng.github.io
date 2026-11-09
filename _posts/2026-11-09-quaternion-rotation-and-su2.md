---
layout: post
title: 四元数，旋转和 SU(2) 与 SO(3) 的双覆盖关系
date: 2026-11-09
tags: math physics
categories: curiosity
related_posts: false
---

总的来说，我们要讲讲四元数、旋转，以及 SU(2) 与 SO(3) 的双覆盖关系。

# 四元数，以及四元数乘法

## 关于四元数的简单定义

我们在这里简单给出四元数的定义，以及一些直觉。

首先，四元数是形如 $q = s + xi + yj + zk$ 的数

其中 $s$ 被称为实部，$xi + yj + zk$ 被称为虚部

四元数的加法简单定义为：$q_1 + q_2 = (s_1 + s_2) + (x_1 + x_2)i + (y_1 + y_2)j + (z_1 + z_2)k$

四元数的乘法满足结合律，且
$$
\begin{aligned}
ij &= k \\
jk &= i \\
ki &= j
\end{aligned}
$$

另外有：

$$
\begin{aligned}
ji &= -k \\
kj &= -i \\
ik &= -j
\end{aligned}
$$

我们可以知道，四元数的加法满足交换律、结合律，四元数的乘法满足结合律以及虚部的反交换律。

## 关于四元数和旋转

我们在上一节中给出了四元数的简单定义，然而我们暂时还看不出四元数的乘法究竟和旋转有什么关系。现在我们来给出四元数乘法与旋转之间的基本的直觉。

在这一小节，我们的全部任务是：给出一个空间向量，看看如何通过四元数乘法得到对应旋转变换后的向量。

### 四元数的乘法，与 Rodrigues 公式

首先，我们认为空间中的一个向量 $\mathbf{v} = v_x \hat{\mathbf{i}} + v_y \hat{\mathbf{j}} + v_z \hat{\mathbf{k}}$
对应的纯虚四元数是 $v = v_x i + v_y j + v_z k$。在后续相当部分的推导中，我们将不加区分地使用这两者。

选取两个向量(或者纯虚四元数)：
$$
\alpha = \alpha_x i + \alpha_y j + \alpha_z k, \quad \beta = \beta_x i + \beta_y j + \beta_z k
$$

我们计算它们的乘积：
$$
\alpha\beta = -(\alpha_x\beta_x + \alpha_y\beta_y + \alpha_z\beta_z) + (\alpha_y\beta_z - \beta_y\alpha_z)i + (\alpha_z\beta_x - \beta_z\alpha_x)j + (\alpha_x\beta_y - \beta_x\alpha_y)k
$$

我们可以注意到，$\alpha\beta$ 的实部恰好是 $-\boldsymbol{\alpha} \cdot \boldsymbol{\beta}$，而虚部恰好是 $\boldsymbol{\alpha} \times \boldsymbol{\beta}$

因此我们得到恒等式(Rodrigues 公式)：

$$
\alpha\beta = -\boldsymbol{\alpha} \cdot \boldsymbol{\beta} + \boldsymbol{\alpha} \times \boldsymbol{\beta}
$$

(注意这里的左式，$\alpha, \beta$ 是四元数，而右式中，$\boldsymbol{\alpha}, \boldsymbol{\beta}$ 作为向量，分别计算四元数的实部和虚部。)

这是一个有用的恒等式，我们将在接下来的推导中不断地使用它。

### 绕轴旋转的向量分解

我们考察空间中的一个向量 $\mathbf{v}$，和轴向量 $\mathbf{n}$

如果要将向量 $\mathbf{v}$ 绕轴 $\mathbf{n}$ 旋转角 $\theta$，我们容易写出其表达式为：
$$
\mathbf{v}' = \mathbf{v}_{\parallel} + \mathbf{v}_{\perp} \cos\theta + (\mathbf{n} \times \mathbf{v}_{\perp}) \sin\theta
$$

其中 $\mathbf{v}_{\parallel} = (\mathbf{n} \cdot \mathbf{v})\mathbf{n}$ 是 $\mathbf{v}$ 平行于 $\mathbf{n}$ 的部分， $\mathbf{v}_{\perp} = \mathbf{v} - \mathbf{v}_{\parallel}$ 恰好是 $\mathbf{v}$ 垂直部分

可以看到，这个形式和四元数乘法有诸多相似之处。自然（至少我们认为自然）的想法是尝试构造合适的四元数乘法 $v' = operation(v)$，使得变换后的 $v'$ 恰好对应 $v$ 绕 $\mathbf{n}$ 旋转角 $\theta$ 的结果。

### 四元数乘法和旋转之间的一一对应

考虑空间中的一个方向向量：
$$
\mathbf{n} = n_x \hat{\mathbf{i}} + n_y \hat{\mathbf{j}} + n_z \hat{\mathbf{k}}
$$
其中 $n_x^2 + n_y^2 + n_z^2 = 1$

我们考虑它对应的纯虚四元数：
$$
n = n_x i + n_y j + n_z k
$$

容易计算得到：
$$
n^2 = (n_x i + n_y j + n_z k)(n_x i + n_y j + n_z k) = -1
$$

可以看到，这里的 $n$ 与虚数单位 $i$ 有几乎一样的形式，因此（虽然我也不知道怎样可以把回答写得更合理一些，这个因此太傻逼了）我们可以仿造旋转元 $e^{i\theta}$ 构造 $q_\theta$：
$$
q_\theta = e^{n\theta} = \cos\theta + n \sin\theta
$$

对于 $v = v_{\parallel} + v_{\perp}$
最符合直觉的变换是直接看 $qv$ 长什么样：
$$
qv = (\cos\theta + n \sin\theta)v = (\cos\theta + n \sin\theta)v_{\parallel} + (\cos\theta + n \sin\theta)v_{\perp}
$$

先计算第二部分（比较简单），我们使用四元数的乘法结合律和纯虚四元数乘法恒等式：

$$
(\cos\theta + n \sin\theta) v_{\perp} = v_{\perp} \cos\theta + (n \times v_{\perp}) \sin\theta
$$
（注意 $n$ 和 $v_{\perp}$ 的垂直关系）

可以看到，这恰好是 $v_{\perp}$ 绕 $n$ 旋转 $\theta$ 角后的结果

对于第一部分：
$$
(\cos\theta + n \sin\theta) v_{\parallel} = v_{\parallel} \cos\theta + (n v_{\parallel}) \sin\theta = v_{\parallel} \cos\theta - (\mathbf{n} \cdot \mathbf{v}_{\parallel}) \sin\theta
$$
（注意 $v_{\parallel}$ 和 $n$ 的平行关系）

我们希望的是 $v_{\parallel}$ 经过变换之后得到的结果是 $v_{\parallel}$ 不变，然而我们实际得到的是 $v_{\parallel} \cos\theta - (\mathbf{n} \cdot \mathbf{v}_{\parallel}) \sin\theta$，(这实际上是四维的等倾变换)，因此我们需要对 $qv$ 做另外的调整。

经过尝试（虽然我也不知道经过怎样的尝试），我们发现这样的计算是对的：
$$
q v q^* = (\cos\theta + n \sin\theta) v (\cos\theta - n \sin\theta)
$$
其中 $q^*$ 是 $q$ 的共轭。

我们对这个变换同样计算 $v$ 平行和 $v$ 垂直

对于 $v_{\parallel}$，首先有：
$$
v_{\parallel} q^* = v_{\parallel}(\cos\theta - n \sin\theta) = (\cos\theta - n \sin\theta)v_{\parallel} = q^* v_{\parallel}
$$
注意这里 $n$ 和 $v_{\parallel}$ 平行，$n \cdot v_{\parallel}$ 是可交换的。

因此，
$$
q v_{\parallel} q^* = q q^* v_{\parallel} = v_{\parallel}
$$

可见，$v_{\parallel}$ 经过变换之后保持不变。这和旋转的性质一致。我们找到了一个好的变换！


对于 $v_{\perp}$ 有：
$$
v_{\perp} q^* = v_{\perp}(\cos\theta - n \sin\theta) = v_{\perp} \cos\theta - (v_{\perp} \times n) \sin\theta = v_{\perp} \cos\theta + (n \times v_{\perp}) \sin\theta = q v_{\perp}
$$

因此，
$$
\begin{aligned}
q v_{\perp} q^* &= q^2 v_{\perp} = (\cos 2\theta + n \sin 2\theta) v_{\perp} \\
&= v_{\perp} \cos 2\theta + (n \times v_{\perp}) \sin 2\theta
\end{aligned}
$$
可以看到，$q v q^*$ 这个变换将平行部分保持不变，将垂直部分绕 $n$ 旋转了 $2\theta$

综合起来，我们就得到：
$$
q v q^* = v_{\parallel} + v_{\perp} \cos 2\theta + (n \times v_{\perp}) \sin 2\theta
$$
这恰好对应将 $v$ 绕轴 $n$ 旋转角 $2\theta$ 的变换

因此，将空间中的向量 $v$ 按四元数乘法变换绕 $n$ 旋转 $\theta$ 的一般表达式为 $v' = q v q^*$，其中 $q = e^{n\theta/2} = \cos(\theta/2) + n \sin(\theta/2)$。（为了得到旋转角 $\theta$，四元数中的角度取 $\theta/2$）

# 泡利矩阵和 $\mathrm{SU}(2)$

上一节中，我们展示了基本的四元数乘法与旋转之间的对应关系。在这一节，我们将展示如何将四元数打包为一个 $2 \times 2$ 的幺正矩阵，并揭示四元数与 $\mathrm{SU}(2)$ 之间的关系。

在此之前，我们需要做一个这样的约定：我们知道四元数单位 $i, j, k$ 满足 $i^2 = j^2 = k^2 = -1$，如果想要直接实现 $i, j, k$ 和幺正矩阵 $\sigma_x, \sigma_y, \sigma_z$ 之间的映射，就会有 $\sigma_x^2 = \sigma_y^2 = \sigma_z^2 = -I$。这个 $-1$ 看起来很麻烦，因此我们需要将这个 $-1$ 打包为虚数单位 $-i$，对应的矩阵即为 $-i\sigma$，其中 $\sigma$ 是一个 $2 \times 2$ 矩阵。分别有 $i$ 对应 $-i\sigma_x$，$j$ 对应 $-i\sigma_y$，$k$ 对应 $-i\sigma_z$，满足 $\sigma^2 = I$

## 泡利矩阵

我们通过一些推导，来得到 $\sigma_x, \sigma_y, \sigma_z$ 的具体形式
首先，如果这个四元数打包能够成立，一个符合直觉的想法是 $1$ 应当对应单位矩阵。

因此，我们有 $i^2 = j^2 = k^2 = ijk = -1$。

对应的：

$$
(-i\sigma_x)^2 = (-i\sigma_y)^2 = (-i\sigma_z)^2 = -I
$$

也即 $\sigma_x^2 = \sigma_y^2 = \sigma_z^2 = I$

由于 $\sigma$ 对应某种非恒等变换，因此它们是非平凡的，也即 $\sigma_x, \sigma_y, \sigma_z \neq \pm I$。

其次，由于反交换律，我们有 $(-i\sigma_x)(-i\sigma_y) = -(-i\sigma_y)(-i\sigma_x)$，etc。

从 $\sigma_x \sigma_y = i\sigma_z$ 以及 $\sigma_{x,y,z}$ 非平凡，$\sigma_{x,y,z}$ 的特征值只能是一个为 $1$，一个为 $-1$。

因此，$\sigma$ 最自然的一个解（不妨设为 $\sigma_z$）是：

$$
\sigma_z = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}
$$

现在计算另外两个矩阵。

对于 $\sigma_x = \begin{pmatrix} a & b \\ c & d \end{pmatrix}$，首先，$-i\sigma_x$ 与 $-i\sigma_z$ 反交换，即 $\sigma_x\sigma_z = -\sigma_z\sigma_x$，得到：
$$
\begin{pmatrix} a & -b \\ c & -d \end{pmatrix} = \begin{pmatrix} -a & -b \\ c & d \end{pmatrix}
$$
即 $a = -a$，$d = -d$，即 $a = d = 0$

同时，由于 $\sigma_x$ 行列式为特征值之积，$\det(\sigma_x) = -1$，有 $bc = 1$

因此，一个可行的解是
$$
\sigma_x = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}
$$

对于 $\sigma_y$，首先 $\sigma_y$ 与 $\sigma_z$ 同样反交换，因此同样得到 $a = d = 0$，$bc = 1$
同时，$\sigma_y$ 与 $\sigma_x$ 反交换，得到 $b = -c$，结合 $bc = 1$，可取 $b = -i$，$c = i$。

因此三个矩阵可行的一组解为
- $\sigma_x = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}$
- $\sigma_y = \begin{pmatrix} 0 & -i \\ i & 0 \end{pmatrix}$
- $\sigma_z = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}$

这正是我们需要的泡利矩阵，它们有这样的一些性质：
- 它们都是 Hermitian 矩阵。
- 它们都是 traceless 矩阵。
- 任意选取方向向量 $\mathbf{n}$，$\mathbf{n} \cdot \boldsymbol{\sigma}$ 是 Hermitian 且 traceless 的矩阵。

## Pauli 矩阵和四元数的一一对应

现在我们有三个方向基底：$\boldsymbol{\sigma} = (\sigma_x, \sigma_y, \sigma_z)$。而在四元数中，我们把三维向量 $\mathbf{v} = (v_x, v_y, v_z)$ 写成 $v_x i + v_y j + v_z k$。

仿照这一操作，我们可以将任意三维矢量 $\mathbf{v}$ 打包成一个无迹厄米矩阵：

$$
X = \mathbf{v} \cdot \boldsymbol{\sigma} = v_x \sigma_x + v_y \sigma_y + v_z \sigma_z = \begin{pmatrix} v_z & v_x - i v_y \\ v_x + i v_y & -v_z \end{pmatrix}
$$

我们已经知道，$-i\sigma_x, -i\sigma_y, -i\sigma_z$ 和纯虚四元数 $i, j, k$ 有一一对应的关系。因此，将纯虚四元数的 $i, j, k$ 替换为 $-i\sigma_x, -i\sigma_y, -i\sigma_z$，纯虚四元数乘法变为：

$$
(\mathbf{a} \cdot \boldsymbol{\sigma})(\mathbf{b} \cdot \boldsymbol{\sigma}) = (\mathbf{a} \cdot \mathbf{b})I + i(\mathbf{a} \times \mathbf{b}) \cdot \boldsymbol{\sigma}
$$

其中 $I$ 为单位矩阵，$\boldsymbol{\sigma}$ 为向量 $(\sigma_x, \sigma_y, \sigma_z)$。

## Pauli 矩阵与旋转

由于四元数和 Pauli 矩阵之间的一一对应，我们在上一节中得到的四元数性质一定可以直接迁移到 Pauli 矩阵上，因此可以仿照四元数旋转矩阵的推导，得到 Pauli 矩阵生成的旋转变换。

对于单位向量 $\mathbf{n}$，有 $(\mathbf{n} \cdot \boldsymbol{\sigma})^2 = |\mathbf{n}|^2 I = I$
这意味着，如果我们配上一个 $-i$，即 $(-i \mathbf{n} \cdot \boldsymbol{\sigma})^2$，它的平方正是 $-I$。

因此类似可生成旋转矩阵：
$$
U(\theta) = \exp\left(-i \frac{\theta}{2} \mathbf{n} \cdot \boldsymbol{\sigma}\right) = \cos\frac{\theta}{2} I - i \sin\frac{\theta}{2} (\mathbf{n} \cdot \boldsymbol{\sigma})
$$

我们仿照四元数旋转 $q v q^*$ 得到变换：
$$
X' = U X U^\dagger
$$

这个变换的几何意义通过四元数是明显的，$X' = U X U^\dagger$ 在打包/解包操作后对应变换 $\mathbf{v}' = O\mathbf{v}$ 是一个旋转变换，如果 $U = e^{-i \frac{\theta}{2} \mathbf{n} \cdot \boldsymbol{\sigma}}$，那么 $O$ 就是绕着方向 $\mathbf{n}$ 旋转 $\theta$ 角度的旋转变换！

### $\mathrm{SU}(2)$ 双覆盖和自旋
事实上，上述构造的 $U$ 是 $\mathrm{SU}(2)$ 中的元素。因为有 $U^\dagger U = e^{i\theta \mathbf{n} \cdot \boldsymbol{\sigma}} e^{-i\theta \mathbf{n} \cdot \boldsymbol{\sigma}} = e^{0} = I$，且 $U$ 可以通过 $U(\alpha) = e^{-i\alpha \mathbf{n} \cdot \boldsymbol{\sigma}}$ 让 $\alpha$ 从 $\theta$ 连续地变形到 $0$，而行列式保持不变，因此 $\det(U) = 1$。(我们省略了这是一个满射的证明，这可以通过每一个 $\mathrm{SU}(2)$ 元素都可以写成特定形式来证明)

而每个 $U$ 都诱导一个变换 $U \to (X \to U X U^\dagger)$，不难发现，$U$ 和 $-U$ 都对应同一个变换 $X \to U X U^\dagger = (-U) X (-U)^\dagger$，而 $X \to U X U^\dagger$ 又对应 $\mathrm{SO}(3)$（我们同样省略了满射的证明）。因此，我们得到了 $\mathrm{SU}(2) \to \mathrm{SO}(3)$ 的一个二对一映射：

$$
\pm U \to (X \to U X U^\dagger)
$$

我们由此说 $\mathrm{SU}(2)$ 和 $\mathrm{SO}(3)$ 具有双覆盖关系 $SU(2)/{\pm I} \cong SO(3)$。

我们用一个小例子说明这一点。在三维现实世界 $\mathrm{SO}(3)$ 中，$U(\pi) X U^\dagger(\pi)$ 对应的是旋转 $2\pi$ 角度，看起来回到了原位，但是在底层旋转空间 $\mathrm{SU}(2)$ 中，角度只经过了 $\pi$，$U = e^{\pi n \cdot \sigma} = -I$。只有再经过 $\pi$ 才回到恒等变换 $U = e^{2\pi n \cdot \sigma} = I$，这时，在现实世界中我们已经转了两圈，总共 $4\pi$ 了！事实上，这正是电子自旋的来源，我们有一个很不错的视频来说明这一点 [Dirac's belt trick, Topology, and Spin ½ particles - YouTube](https://www.youtube.com/watch?v=ACZC_XEyg9U)