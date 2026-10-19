---
layout: post
title: 语言，神，和谜语——关于三神的谜题
date: 2026-10-16
tags: logic puzzle
categories: curiosity
related_posts: false
---

### 谜语

我们来看下面的[谜题](https://en.wikipedia.org/wiki/The_Hardest_Logic_Puzzle_Ever)，它看起来很有趣。

> Three gods A, B, and C are called, in no particular order, True, False, and Random. True always speaks truly, False always speaks falsely, but whether Random speaks truly or falsely is a completely random matter. Your task is to determine the identities of A, B, and C by asking three yes–no questions; each question must be put to exactly one god. The gods understand English, but will answer all questions in their own language, in which the words for yes and no are *da* and *ja*, in some order. You do not know which word means which.

补充：

> a single god may be asked more than one question, questions are permitted to depend on the answers to earlier questions, and the nature of Random's response should be thought of as depending on the flip of a fair coin hidden in his brain: if the coin comes down heads, he speaks truly; if tails, falsely.

### 谜语的历史

- 这个谜题被 George Boolos 称为"史上最难的逻辑谜题"，1996 年发表于 *The Harvard Review of Philosophy*。更早的意大利文版本曾刊登在 *La Repubblica* 上，标题为 *L'indovinello più difficile del mondo*。
- Boolos 将谜题的原创归于 Raymond Smullyan，并说明 John McCarthy 加入了"da 和 ja 含义未知"这一难点。


### 我们的构造

#### 形式化的定义

首先，让我们对问题有一个形式化的定义。

我们把神看作一个黑盒函数，祂掌握了任意命题 $P$ 的真假，但是由于祂的一点小癖好，祂不会告诉你 $\mathbb{1}[P]$（也就是命题 $P$ 的真假），而是告诉你
$$
Ask_{god}(P) := \mathbb{1}[P] \oplus key_{god} \oplus key_{language}
$$

其中 $key_{god}$ 是神的身份密钥，$key_{language}$ 是语言密钥，分别有：
$$
key_{god} = \begin{cases}
0 & \text{if god is True} \\
1 & \text{if god is False} \\
\text{randomly chosen} & \text{if god is Random}
\end{cases}
$$

和 

$$
key_{language} = \begin{cases}
0 & \text{if "da" means yes} \\
1 & \text{if "da" means no}
\end{cases}
$$

#### 一点简单的小 Trick

我们很容易想到，对所有 $key_{language}$，我们都可以询问 $P \oplus key_{language}$，来消除语言密钥的影响。原因是对所有 $a$，我们都有
$$
a \oplus a = 0
$$
这样就有
$$
\begin{aligned}
\operatorname{Ask}_{\text{god}}(P \oplus key_{\text{language}})
&= \mathbb{1}[P] \oplus key_{\text{god}}
   \oplus key_{\text{language}} \oplus key_{\text{language}} \\
&= \mathbb{1}[P] \oplus key_{\text{god}}
\end{aligned}
$$

因此，对所有我们实际感兴趣的命题 $P$，我们都可以询问 $P \oplus key_{language}$ 来假装实际上没有语言 Key。在接下来的论述中，我们假设实际上没有语言 Key。

同样的，我们也可以通过询问 $P \oplus key_{god}$ 来消除神的身份密钥的影响。但这里有一个小问题：对于 Random 神来说，$key_{god}$ 是随机的，因此，询问 
$$
P \oplus key_{god}
$$
的结果是
$$
\begin{aligned}
\operatorname{Ask}_{\text{god}}(P \oplus key_{\text{god}})
&= \mathbb{1}[P] \oplus key_{\text{god}} \oplus key_{\text{god}} \\
&= \begin{cases}
\mathbb{1}[P] & \text{if god is True or False} \\
\text{randomly chosen} & \text{if god is Random}
\end{cases}
\end{aligned}
$$

这样，通过询问 $\mathbf{1}[P] \oplus key_{god}$，我们就将问题转化为了下面这个形式：

> 已知有三个神，True，False 和 Random。True 和 False 在我们通过合适的方式问问题时总是给出正确的答案，然而 Random 是个坏蛋，我们向他问问题时他总是扔硬币。好在我们和神们的语言是相通的。我们怎么用三个问题确认三位神的身份呢？

#### 我们的解答

在这里我们给出一个解答。我们注意到，实际上有了合适的提问方式之后，True 和 False 都是可靠的神谕机，而 Random 是一个坏蛋。因此我们的第一步，是找到坏蛋，然后不问通过一通乱搞，我们找到了这样的一个命题：
$$
P := \forall B \operatorname{Ask}_{B}(\text{C is True}) 
$$
然后我们询问 $Ask_A(P)$：如果 A 是 Random，我们会得到 true 或者 false 的随机答案；如果 B 是 Random，我们会得到 false（因为 Random 神的回答是随机的，所以 A 不知道 $\forall B \operatorname{Ask}_{B}$ 是什么东西）；如果 C 是 Random，我们会得到 true（因为 C is True 是 false，而 AB 是可靠的神谕机，我们会得到）。

总结起来，如果回答是 true，那么 AC 可能是 Random，而 B 是可靠的神谕机；如果回答是 false，那么 AB 可能是 Random，而 C 是可靠的神谕机。

这样，通过一次问答，我们得到了一个可靠的神谕机。接下来，我们可以问这个可靠的神谕机两个问题，来确定三位神的身份。

不妨设 B 是可靠的神谕机。我们可以问 B 两个问题：问题;或者至少，我们要找到一台可靠的神谕机，然后我们问祂问题。

通过一通乱搞，我们找到了这样的一个命题：
$$
P := \forall B \operatorname{Ask}_{B}(\text{C is Random}) 
$$
然后我们询问 $Ask_A(P)$：如果 A 是 Random，我们会得到 true 或者 false 的随机答案；如果 B 是 Random，我们会得到 false（因为 Random 神的回答是随机的，所以 A 不知道 $\forall B \operatorname{Ask}_{B}$ 是什么东西）；如果 C 是 Random，我们会得到 true（因为 C is True 是 true，而 AB 是可靠的神谕机）。

总结起来，如果回答是 true，那么 AC 可能是 Random，而 B 是可靠的神谕机；如果回答是 false，那么 AB 可能是 Random，而 C 是可靠的神谕机。

这样，通过一次问答，我们得到了一个可靠的神谕机。接下来，我们可以问这个可靠的神谕机两个问题，来确定三位神的身份。

不妨设 B 是可靠的神谕机。我们可以问 B 两个问题：
$$ 
Ask_B(\text{B is True})
$$
和
$$
Ask_B(\text{C is Random})
$$

这样，根据 B 的不同回答，我们知道了三位神的身份：

| $Ask_B(\text{B is True})$ | $Ask_B(\text{C is Random})$ | A | B | C |
|---|---|---|---|---|
| True  | True  | False  | True  | Random |
| True  | False | Random | True  | False  |
| False | True  | True   | False | Random |
| False | False | Random | False | True   |

#### 自然语言版本

我们整理自然语言版本的提问方式如下：

我们向 A 提问：

>如果我问你下面这个问题，你会回答 da 吗？
>「无论 B 怎么行动，如果我问 B『如果我问你 C 是 Random，你会回答 da 吗？』，B 都一定会回答 da。」

第二个问题，不妨假设 A 回答了 da，因此我们知道 B 是可靠的神谕机。

我们向 B 提问：

> 如果我问你「你是 True 吗？」，你会回答 da 吗？

如果 B 回答 da，那么 B 是 True；如果回答 ja，那么 B 是 False。

第三个问题：

我们继续向 B 提问：

> 如果我问你「C 是 Random 吗？」，你会回答 da 吗？

如果 B 回答 da，那么 C 是 Random；否则 A 是 Random。

结合第二个问题的回答，我们就能确定三位神的全部身份。

如果第一个问题得到 ja，我们只需要将后面两个问题改为询问 C，并在第三问判断 B 是否为 Random，逻辑完全相同。

至此，我们使用三个问题解决了这个谜题。

#### 为什么三个问题是最优的？

三位神分别为 True、False、Random，因此共有 $3!=6$ 种可能的身份排列。

每个问题只有两种可能的回答，因此，$n$ 个问题最多只能区分 $2^n$ 种情况。

所以 $2^n\ge 6$，也就是 $n\ge \lceil\log_2 6\rceil=3$。

### 经典解法

我们展示经典解法和我们的构造有什么不同，首先给出经典的解法的自然语言版本：

第一个问题，向 A 提问：

>「如果我问你『B 是 Random 吗？』，你会回答 da 吗？」

如果回答 da，那么 C 是可靠的神谕机；如果回答 ja，那么 B 是可靠的神谕机。

不妨设 A 回答 ja，因此 B 是可靠的神谕机。

第二个问题，向 B 提问：

>「如果我问你『你是 True 吗？』，你会回答 da 吗？」

第三个问题，继续向 B 提问：

>「如果我问你『C 是 Random 吗？』，你会回答 da 吗？」

这样，我们就确定了三位神的身份。


#### 我们与经典解法的区别

可以看到，我们的构造和经典构造基本一样，区别只在于第一个问题，我们询问：
$$
\forall B \operatorname{Ask}_{B}(\text{C is True})
$$
而经典构造询问：
$$
\operatorname{Ask}_{A}(\text{B is Random})
$$

简单的分析告诉我们这两个问题是等价的。
