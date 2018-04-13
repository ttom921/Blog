---
title: 記錄C#語法的使用
categories:
  - 程式
tags:
  - C#
date: 2018-04-13 09:55:01
---
#### C# 6 的三個新的表示式
介紹 C# 6 的三個新語法：nameof 表示式、字串插值、和 null 條件運算子。
* nameof 表示式
  C# 6 新增的 nameof 關鍵字可用來取得某變數的名稱。請看底下這個簡單範例，便能了解其作用：
  ```
  string firstName = "Joey";
  string varName = nameof(firstName);  // 編譯結果：varName = "firstName"
  ```
  比如說，為了防錯，我們經常在函式中預先檢查參數值是否合法，並將不合法的參數透過拋異常（exception）的方式通知呼叫端（或者寫入 log 檔案以供將來診斷問題）。像這樣：

  ```
  void LoadProduct(string productId)
    {
        if (productId == null)
        {
            throw new ArgumentNullException(nameof(productId));
        }
    }
  ```
  
* 字串插值
  NET Framework 提供的字串格式化方法 String.Format(...) 是一種對號入座的寫法，相當好用。
  現在，C# 6 提供了另一種格式化字串的寫法，名曰「字串插值」（string interpolation）。
  $"{變數名稱:格式規範}"
  ```
  string firstName = "Michael";
  string lastName = "Tsai";
  int salary = 22000;

  string msg1 = String.Format("{0} {1} 的月薪是 {2:C0}", firstName, lastName, salary);
  string msg2 = $"{firstName} {lastName} 的月薪是 {salary :C0}";
  Console.WriteLine(msg1);
  Console.WriteLine(msg2);
  ```

* Null 條件運算子
  保險起見，在需要存取某物件的屬性之前，我們通常會先檢查該物件是否為 null
  ```
  static void NullPropagationDemo(string s)
  {
    if (s?.Length == 4) // 只有當 s 不為空時才存取它的 Length 屬性。
    {
        // Do something.
    }
  }
  
  int? length = productList?.Length; // 若 productList 是 null，則 length 也是 null。 
  Customer obj = productList?[0];    // 若 productList 是 null，則 obj 也是 null。
  int length = productList?.Length ?? 0;  // 若 productList 是 null，則 length 是 0。
  string name = productList?[0].FullName; // 若 productList 是 null，則 name 是 null。
  ```
* 參考  
  *  [C# 6 的三個新的表示式](https://www.huanlintalk.com/2015/01/csharp6-enhanced-expressions.html)
   