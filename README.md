# NLMS 演算法作業展示

這是一個關於 **正規化最小均方演算法 (Normalized Least Mean Squares)** 的作業說明。

---

## 1. 演算法簡介
NLMS 是一種常見的自適應濾波演算法，其核心目的是透過迭代更新係數，使誤差函數最小化。

### 核心特性：
* **穩定性**：透過正規化輸入向量能量來改善收斂。
* **計算效率**：適合即時處理。
* **自適應性**：能根據環境變化動態調整。

---

## 2. 演算法步驟 (附圖說明)

下圖展示了 NLMS 的初始化與計算流程：

![NLMS Algorithm Steps](https://你的圖片連結或上傳後的路徑)
> *圖 1：NLMS 演算法的數學更新公式*

---

## 3. 數學公式解析

根據上圖，演算法流程如下：

### A. 初始化 (Initialization)
$$\mathbf{\hat{h}}(0) = \text{zeros}(p)$$
* 將濾波器權重向量設為長度為 $p$ 的零向量。

### B. 反覆計算 (Computation)
對於每個時間點 $n = 0, 1, 2, \dots$：

1.  **輸入向量**：
    $$\mathbf{x}(n) = [x(n), x(n-1), \dots, x(n-p+1)]^T$$
2.  **估計誤差**：
    $$e(n) = d(n) - \mathbf{\hat{h}}^H(n)\mathbf{x}(n)$$
3.  **係數更新**：
    $$\mathbf{\hat{h}}(n+1) = \mathbf{\hat{h}}(n) + \frac{\mu e^*(n)\mathbf{x}(n)}{\mathbf{x}^H(n)\mathbf{x}(n)}$$

---

## 4. 參數對照表

| 符號 | 定義 |
| :--- | :--- |
| $\mu$ | 步長 (Step size) |
| $p$ | 濾波器階數 |
| $d(n)$ | 期望信號 |
| $e(n)$ | 誤差信號 |

---

## 5. 實作建議
在使用 Python 實作時，建議使用 `NumPy` 進行向量運算：
```python
# 範例程式碼片段
import numpy as np
e = d - np.dot(h.conj().T, x)
h = h + (mu * e.conj() * x) / (np.dot(x.conj().T, x))
