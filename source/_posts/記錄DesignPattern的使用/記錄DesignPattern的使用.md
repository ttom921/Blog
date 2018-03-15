---
title: 記錄DesignPattern的使用
categories:
  - 記錄
tags:
  - DesignPattern
date: 2018-03-15 11:10:47
---
* Singleton在c#的使用
```
public class ConvertHelp
{
    #region Singleton
    private static readonly Lazy<ConvertHelp> lazy =
    new Lazy<ConvertHelp>(() => new ConvertHelp());
    public static ConvertHelp Instance { get { return lazy.Value; } }
    public ConvertHelp()
    {
            
    }
    #endregion Singleton
}
```