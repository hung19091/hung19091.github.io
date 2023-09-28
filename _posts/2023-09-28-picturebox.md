---
layout: post
title: VB.NET 透明pictureBox，顯示底下的元件
categories: program
---
原文連結:[https://stackoverflow.com/questions/32241014/transparency-of-picture-box](<https://stackoverflow.com/questions/32241014/transparency-of-picture-box>"原文連結")



如果您打算將其用作遊標，則建議使用圖形物件繪製圖像。但是，如果您有時想使用 PictureBox（出於諸如能夠使用其Image屬性快速更改圖像等原因），那也是可能的。

此程式碼將透過在 PictureBox 後面的背景上繪製每個控制項來繪製更好的「透明」背景。

如何使用：

1）建立自訂類別。

2) 置於Inherits PictureBox該Public Class ...線下方。

3）將此程式碼貼到類別中：
```
Protected Overrides Sub OnPaintBackground(e As System.Windows.Forms.PaintEventArgs)
    MyBase.OnPaintBackground(e)

    If Parent IsNot Nothing Then
        Dim index As Integer = Parent.Controls.GetChildIndex(Me)

        For i As Integer = Parent.Controls.Count - 1 To index + 1 Step -1
            Dim c As Control = Parent.Controls(i)
            If c.Bounds.IntersectsWith(Bounds) AndAlso c.Visible = True Then
                Dim bmp As New Bitmap(c.Width, c.Height, e.Graphics)
                c.DrawToBitmap(bmp, c.ClientRectangle)
                e.Graphics.TranslateTransform(c.Left - Left, c.Top - Top)
                e.Graphics.DrawImageUnscaled(bmp, Point.Empty)
                e.Graphics.TranslateTransform(Left - c.Left, Top - c.Top)
                bmp.Dispose()
            End If
        Next
    End If
End Sub
```
4) 建立您的專案。

5) 從工具箱中選擇您的類別並將其新增至您的表單/使用者控制項。


不確定有沒有用，先存著
