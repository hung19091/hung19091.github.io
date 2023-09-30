---
layout: post
title: AutoSubmit-note
categories: program
---

## JS
{% highlight javascript %}
驗證訊息
available=true
version=試用版
expiry_date=2023/10/10

{"available":"true","version":"試用版","expiry_date":"2023/10/10"}
https://hirosama.iinaa.net/products/autoSubmit/key01.html


狀態
wait for login
login success-wait for search
search success-wait for edit
editing-wait for verify
verify success-edit next

//[進場確認單清單]
let a_arr = document.getElementsByTagName('a');
[...a_arr].filter((ele) => ele.textContent.indexOf('進廠確認單清單') > 0)[0].click();

//獲取iframe內的按鈕清單
let frame = document.getElementsByTagName('iframe')[0];
let btn_arr = frame.contentWindow.document.getElementsByTagName("button");

//查詢
//document.getElementById('btnQuery').click();
[...btn_arr].filter((ele) => ele.textContent == '查詢')[0].click();

//判斷是否有[列印]按鈕
function hasPrintBtn(ele){
    let arrTemp = [...ele.parentNode.getElementsByTagName('button')].filter((ele) => ele.textContent == '列印');
    return (arrTemp.length > 0) ? true:false;
}

//[編輯]按鈕，且不含[列印]按鈕，順序由上而下
//let btn_arr = document.getElementsByTagName('button');
//let edit_btn_arr = [...btn_arr].filter((ele) => ele.textContent == '編輯' && ele.style.display != 'none');
let edit_btn_arr = [...btn_arr].filter((ele) => ele.textContent == '編輯' && ele.style.display != 'none' && !hasPrintBtn(ele));
edit_btn_arr[0].click();

//[列印]按鈕
//[...edit_btn_arr[4].parentNode.getElementsByTagName('button')].filter((ele) => ele.textContent == '列印')


//驗證碼輸入框
let frame_Verify = frame.contentWindow.document.getElementsByTagName("iframe")[0];
let input_arr_Verify = frame_Verify.contentWindow.document.getElementsByTagName("input");
input_arr_Verify = [...input_arr_Verify].filter((ele) => ele.id == 'VerificationCode');
//驗證碼輸入後的訊息
let msg_arr = [...frame_Verify.contentWindow.document.getElementsByTagName("div")].filter((ele) => ele.id == 'divMessage');
msg_arr[0].textContent;
//關閉驗證碼輸入後的訊息
msg_arr[0].parentNode.getElementsByTagName('button')[0].click();

//關閉輸入驗證碼的div(僅能在iframe內部使用)
window.parent.$('#divAddE20').dialog('close');
{% endhighlight %}

## VB
{% highlight vb %}
Imports System.Text
Imports Newtonsoft.Json
Imports Newtonsoft.Json.Linq

Public Class Form1
    Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load
        Dim webClient As New System.Net.WebClient
        webClient.Headers.Add("User-Agent: Other")
        webClient.Encoding = Encoding.UTF8
        Dim result As String = webClient.DownloadString("https://hirosama.iinaa.net/products/autoSubmit/key01.html")

        Dim jstr_start = result.IndexOf("{""available")
        Dim jstr_length = result.IndexOf("""}") - jstr_start + 2
        result = result.Substring(jstr_start, jstr_length)
        Console.WriteLine(result)

        Dim JSONString = JsonConvert.SerializeObject(result)
        Dim jObj As JObject = JObject.Parse(result)
        Console.WriteLine("available = " & jObj("available").ToString())
        Console.WriteLine("version = " & jObj("version").ToString())
        Console.WriteLine("expiry_date = " & jObj("expiry_date").ToString())
    End Sub
End Class
{% endhighlight %}

## 更改Textbox密碼樣式
{% highlight vb %}
Private Sub PictureBox1_Click(sender As Object, e As EventArgs) Handles PictureBox1.Click
    If TextBox1.PasswordChar = Nothing Then
        TextBox1.PasswordChar = "●"
    Else
        TextBox1.PasswordChar = Nothing
    End If
End Sub

Private Sub PictureBox1_MouseEnter(sender As Object, e As EventArgs) Handles PictureBox1.MouseEnter
    PictureBox1.BorderStyle = BorderStyle.Fixed3D
End Sub

Private Sub Form1_MouseEnter(sender As Object, e As EventArgs) Handles Me.MouseEnter
    PictureBox1.BorderStyle = BorderStyle.None
End Sub
{% endhighlight %}

## Other URL
```
更改user-agent
https://tech-blog.cymetrics.io/posts/nick/google-recaptcha/
https://github.com/cefsharp/CefSharp/discussions/3982

reCAPTCHA v3 分數偵測器
https://antcpt.com/score_detector/

tensorflow-ocr
https://pylessons.com/tensorflow-ocr-captcha

tensorflow-hub
https://kozyrk.medium.com/chinese-all-about-tensorflow-f1e2ab1b89b1

Keras作者推荐的OCR项目Keras-OCR，基于tf.keras+tf2.0，方便易用
https://blog.csdn.net/javastart/article/details/104032570

用於讀取驗證碼的 OCR 模型
https://keras.io/examples/vision/captcha_ocr/

最近用Timer踩了一个坑，分享一下避免别人继续踩
https://www.cnblogs.com/huangxincheng/p/4070353.html

CefSharp-如何在 C# 中處理 Javascript 事件？
https://github.com/cefsharp/CefSharp/wiki/Frequently-asked-questions#JSEvent

CefSharp-官網
http://cefsharp.github.io/

CefSharp-擷取/停用按鍵事件以停用退格鍵功能
https://github.com/cefsharp/CefSharp/issues/1512

CefSharp-瀏覽器 SendKeys
https://stackoverflow.com/questions/44736904/issue-with-cefsharp-browser-sendkeys
```
