# 解題紀錄 LeetCode 3

## 題目：最長無重複字元的子字串（Longest Substring Without Repeating Characters）

## 📙 題目描述

Given a string `s`, find the length of the longest substring without duplicate characters.  
給定一個字串，找出最長s的長度 子字串 沒有重複的字元。

**範例1：**

```txt
輸入： s = "abcabcbb"
輸出： 3
解釋：答案是“abc”，長度為 3。
```

**範例2：**

```txt
輸入： s = "bbbbb"
輸出： 1
解釋：答案是“b”，長度為 1。
```

---

## ✒️ 解題思路

1. **使用sliding window演算法**
   - 使用兩個指標來維護一個動態窗口，該窗口會根據條件擴展或收縮，而不需要每次重新計算整個區間。
2. **宣告變數**
   - ``left`` 標記左邊界``right``標記右邊界。
   - 宣告能儲存位置的陣列 ``lastIndex[]`` 查找是否出現過，以及最後位置，這是以``ASCII``為**key**，位置為**value**的方法。
   - 宣告``maxLen``儲存最長長度。
3. **開始滑動**🔜
   - ``right``會不斷**遞增**
   - 確認此**字母最後位置是否在區間裡**
       - ✅ 更新``left``位置避開重複字元
       - ❎ 繼續
   - **紀錄字母位置**
   - **更新長度**
       - 如果目前長度大於 ``maxLen``則更新``maxLen``

## 💻 C 語言解法

```c
int lengthOfLongestSubstring(char* s) {
    int lastIndex[128] = {0}; // 記住每個字母最後出現的位置
    int maxLen = 0, left = 0; // 記住最長的長度，還有左位置

    for (int right = 0; s[right] != '\0'; right++) { 
        if (lastIndex[s[right]] > left) { // 如果這個字母出現過
            left = lastIndex[s[right]]; // 要往右跳，避開重複字
        }
        lastIndex[s[right]] = right + 1; // 記住這個字母最後出現的位置
        int currentLen = right - left + 1; // 算出目前的長度
        if (currentLen > maxLen) { 
            maxLen = currentLen;
        }
    }
    return maxLen; 
}

```

---

## 🕛時間複雜度分析

- **O(n)**（迴圈遍歷）

---
