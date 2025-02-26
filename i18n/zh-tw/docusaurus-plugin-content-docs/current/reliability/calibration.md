---
sidebar_position: 10
---

# 🔴 校準大語言模型

透過校準輸出分佈(@zhao2021calibrate)，可以抵消 LLM 表現出的某些偏差。

**校準輸出分佈究竟意味著什麼？**

讓我們透過一個快速範例來說明：假設我們有一個 %%sentiment analysis|sentiment analysis%% ，有兩個可能的標籤，`Positive` 和 `Negative`。
思考一下 LLM 被提示輸入 `Input: nothing Sentiment:` 時會發生什麼。
這個輸入不包含任何 LLM 可以用來進行情感預測的 _上下文_ ，因此被稱為**無上下文**輸入。

由於 nothing 既不是積極的概念，也不是消極的概念，因此我們期望 LLM 為 Positive 和 Negative 的輸出機率約為 0.5。然而，通常（包括此範例）情況並非如此。

```
p("Positive" | "Input: nothing Sentiment:") = 0.9

p("Negative" | "Input: nothing Sentiment:") = 0.1
```

在給定一個無上下文輸入的標籤機率的情況下，我們知道 LLM 的**輸出分佈**很可能偏向標籤 `Positive`。這可能會導致 LLM 對所有輸入都偏向 `Positive`，即使輸入實際上不是積極的。

如果我們能夠以某種方式**校準**輸出分佈，使得無上下文輸入為 `Positive` 和 `Negative` 都被分配機率 0.5，那麼我們通常可以消除對 `Positive` 的偏見，並使 LLM 在無上下文輸入和有上下文輸入上更可靠。

## 非技術性解決方案

解決此問題的一種非技術性方法是提供一些 few-shot 範例，其中無上下文範例被有效地分配為 `Positive` 和 `Negative` 的機率均為 0.5。

例如，我們可以提供以下 few-shot 範例，顯示每個無上下文範例都被分類為 Positive 和 Negative：
```
Input: 我討厭這部電影。 Sentiment: Negative
Input: 我喜歡這部電影。 Sentiment: Positive
Input: N/A Sentiment: Positive
Input: N/A Sentiment: Negative
Input: nothing Sentiment: Positive
Input: nothing Sentiment: Negative
Input: 我喜歡雞蛋。 Sentiment:
```

據我所知，這種解決方案在文獻中尚未得到探討，我不確定它在實踐中的效果如何。然而，這是一個簡單的解決方案，可以展示校準試圖實現什麼。

## 技術解決方案

另一個解決方案是 __上下文校準__(@zhao2021calibrate)，在此解決方案中，我們調整特殊的校準引數，以確保像 `Input: nothing Sentiment:` 這樣的無上下文輸入被分配到兩個標籤的機率約為 0.5。請注意，在實踐中，該方法透過多個不同的無上下文輸入（例如 `Input: N/A Sentiment:`，`Input: [MASK] Sentiment:`）進行校準。它平均了最適合每個無上下文輸入的校準引數，以找到 LLM 的最佳校準引數。

### 範例

讓我們透過一個範例來計算一個無上下文輸入的校準引數。請注意，由於 GPT-3 不能限制在 `Positive` 和 `Negative` 標籤上，因此此範例無法在 GPT-3 上重現。

再次考慮上面的範例，LLM 為無上下文輸入分配以下標籤的機率：

```
p("Positive" | "Input: nothing Sentiment:") = 0.9

p("Negative" | "Input: nothing Sentiment:") = 0.1
```

我們想要找到一些機率分佈 `q`，使得:

```
q("Positive" | "Input: nothing Sentiment:") = 0.5

q("Negative" | "Input: nothing Sentiment:") = 0.5
```

我們將透過建立一個線性變換來調整（校準）$p$的機率來實現這一點。

$\^{q} = \text{Softmax}(W\^{p} + b)$

該方程式接受原始機率 $\^{p}$ 並將權重 $W$ 和偏差 $b$ 應用於它們。權重 $W$ 和偏差 $b$ 是校準引數，當應用於無上下文範例的機率時，將產生 $\^{q}$ = [0.5，0.5]。

#### 計算 W 和 b

我們需要某種方式來計算權重 $W$ 和偏差 $b$ 。一種方法是：
$W = \text{diag}(\^{p})^{-1}$ 

$b = 0$

雖然 $W$ 的定義可能一開始看起來有點奇怪，但它只是取 $\^{p}$ 中每個值的倒數，以便找到將原始機率 $\^{p}$ 轉換為校準機率[0.5，0.5]的 $W$ 。

讓我們驗證這對於上面的範例是否有效：

$\^{p} = [0.9, 0.1]$

$W = \text{diag}(\^{p})^{-1} = \text{diag}([0.9, 0.1])^{-1} 
= \begin{bmatrix}
   0.9 & 0 \\
   0 & 0.1
\end{bmatrix}^{-1}
= \begin{bmatrix}
   1.11 & 0 \\
   0 & 10
\end{bmatrix}$

$\^{q} = \text{Softmax}(W\^{p} + b) = \text{Softmax}(\begin{bmatrix}
   1.11 & 0 \\
   0 & 10
\end{bmatrix}*{[0.9, 0.1]} + 0)
= \text{Softmax}([1, 1])
=[0.5, 0.5]$

正如上面所提到的，我們將為多個不同的無上下文輸入執行相同的過程，並平均適用於每個無上下文輸入的最佳校準引數，以找到LLM的最佳校準引數。這意味著最終的校準引數可能不會將任何無上下文輸入對映到完全為[0.5，0.5]的機率。

### 另一種方法

$b$ 也可以設定為 $-\^{p}$ ，$W$ 設定為單位矩陣。該方法在生成任務上表現更好，而不是分類任務(@zhao2021calibrate)。

## 總結

LLM 通常會對某些標籤產生偏見。校準可以用於抵消這種偏見。