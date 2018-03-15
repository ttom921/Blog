---
title: 記錄WPF的使用
categories:
  - 記錄
tags:
  - WPF
date: 2018-03-15 10:55:55
---
* OpenFileDialog和WPF
  可以使用Microsoft.Win32.OpenFileDialog 來達到
```
private void Button_Click(object sender, RoutedEventArgs e)
{
    var openFileDialog = new Microsoft.Win32.OpenFileDialog()
    {
        Filter = "Excel Files (*.xlsx)|*.xlsx"
    };
    var result = openFileDialog.ShowDialog();
    if (result == true)
    {
        this.textblock_filename.Text = openFileDialog.FileName;
    }
}
``` 