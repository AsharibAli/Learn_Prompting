---
sidebar_position: 1
---

# 🔴 軟提示

提示微調(Prompt Tuning)(@lester2021power) 是模型微調（@khashabi2021prompt）的一種替代方法，它會固定模型權重並更新提示的引數，生成的提示被稱為“軟提示”。

import Image from '@site/docs/assets/trainable/prompt_tuning.webp';

<div style={{textAlign: 'center'}}>
  <img src={Image} style={{width: "500px"}}/>
</div>

<div style={{textAlign: 'center'}}>
模型微調與提示調整的對比 (Lester et al.)
</div>

上面的圖片對比了模型微調和提示調整。在模型微調中，你會在不同任務上對同一個模型進行微調。這會產生一些不同的模型，但你不能保證可以輕鬆地對不同的任務進行批處理輸入。

另一方面，提示調整可以讓你為所有任務使用同一個模型。你只需要在推理時附加適當的提示，這樣可以使不同任務之間的批處理更容易。這是常規提示的同樣優點。此外，為單個模型跨多個任務訓練的軟提示通常會具有相同的標記長度。

## 工作原理

為了理解軟提示背後的基本邏輯，讓我們思考一下如何在給定提示**What's 2+2?**上進行模型推理：

對於給定的: `What's 2+2?`.

1) 它可能被標記為 `What, 's, 2, +, 2, ?`. 

2) 然後，每個標記將被轉換為一組值的向量。

3) 這些向量可以視為模型引數。模型可以進一步訓練，僅調整這些提示的權重。

請注意，一旦我們開始更新這些權重，標記的向量就不再對應於詞彙表中實際的嵌入。

# 結果 

提示調整對較大的模型表現更好。較大的模型也需要較少的軟提示標記。但是，超過20個標記並不會產生顯著的效能提高。