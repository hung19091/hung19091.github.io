---
layout: post
title: AutoSubmit-note
categories: program
---

[進場確認單清單]
var a_arr = document.getElementsByTagName('a');
a_arr = [...a_arr].filter((ele) => ele.textContent.indexOf('進廠確認單清單') > 0);
a_arr[0].click();

獲取iframe內的按鈕清單
var frame = document.getElementsByTagName('iframe')[0];
var btn_arr = frame.contentWindow.document.getElementsByTagName("button");

查詢
//document.getElementById('btnQuery').click();
[...btn_arr].filter((ele) => ele.textContent == '查詢')[0].click();


[編輯]按鈕
//var btn_arr = document.getElementsByTagName('button');
var edit_btn_arr = [...btn_arr].filter((ele) => ele.textContent == '編輯');
