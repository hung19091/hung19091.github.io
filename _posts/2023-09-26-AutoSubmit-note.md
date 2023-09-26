---
layout: post
title: AutoSubmit-note
categories: program
---

```
驗證訊息
available=true
version=試用版
expiry_date=2023/10/10

{"available":"true","version":"試用版","expiry_date":"2023/10/10"}


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
input_arr_Verify = [...btn_arr_Verify].filter((ele) => ele.id == 'VerificationCode');
//驗證碼輸入後的訊息
let msg_arr = [...frame_Verify.contentWindow.document.getElementsByTagName("div")].filter((ele) => ele.id == 'divMessage');
msg_arr[0].textContent;
//關閉驗證碼輸入後的訊息
msg_arr[0].parentNode.getElementsByTagName('button')[0].click();

//關閉輸入驗證碼的div
window.parent.$('#divAddE20').dialog('close');
```
