---
title: 调试 HTML、 CSS 和 JavaScript 示例代码 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 51893967-98c8-4141-ba40-03646f221760
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 134b4e3c5195e9008d951062ec813a939d0d4fe6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68161473"
---
# <a name="debug-html-css-and-javascript-sample-code"></a>调试 HTML、CSS 和 JavaScript 示例代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

适用于 Windows 和 Windows Phone] (../Image/windows_and_phone_content.png"windows_and_phone_content")  
  
 本主题中的代码是示例文件[快速入门：调试 HTML 和 CSS](../debugger/quickstart-debug-html-and-css.md)。 此版本的代码中修复了快速入门中有意出现的错误。  
  
## <a name="sample-code"></a>代码示例  
 快速入门的 \<body> 标记中使用了以下 HTML 代码。  
  
```html  
<div id="flipTemplate" data-win-control="WinJS.Binding.Template"  
         style="display:none">  
    <div class="fixedItem" >  
        <img src="#" data-win-bind="src: flipImg" />  
    </div>  
</div>  
<div id="fView" data-win-control="WinJS.UI.FlipView" data-win-options="{  
    itemDataSource: Data.items.dataSource, itemTemplate: flipTemplate }">  
</div>  
```  
  
 以下 CSS 显示了在 default.css 中增加的代码。  
  
```css  
#fView {  
    background-color:#0094ff;  
    height: 500px;  
    margin: 25px;  
}  
```  
  
 以下代码示例展示了 default.js 中的完整 JavaScript 代码。 对此代码的 WinJS 命名空间的引用位于模板的 default.html 文件中。  
  
```javascript  
(function () {  
    "use strict";  
  
    var app = WinJS.Application;  
    var activation = Windows.ApplicationModel.Activation;  
  
    var myData = [];  
    for (var x = 0; x < 4; x++) {  
        myData[x] = { flipImg: "/images/logo.png" }  
    };  
  
    var pages = new WinJS.Binding.List(myData, { proxy: true });  
  
    app.onactivated = function (args) {  
        if (args.detail.kind === activation.ActivationKind.launch) {  
            if (args.detail.previousExecutionState !==  
            activation.ApplicationExecutionState.terminated) {  
                // TODO: . . .  
            } else {  
                // TODO: . . .  
            }  
            args.setPromise(WinJS.UI.processAll());  
  
            updateImages();  
        }  
    };  
  
    function updateImages() {  
  
        pages.setAt(0, { flipImg: "http://go.microsoft.com/fwlink/?LinkID=223195" });  
        pages.setAt(1, { flipImg: "http://go.microsoft.com/fwlink/?LinkID=223196" });  
        pages.setAt(2, { flipImg: "http://go.microsoft.com/fwlink/?LinkID=223197" });  
    };  
  
    app.oncheckpoint = function (args) {  
    };  
  
    app.start();  
  
    var publicMembers = {  
        items: pages  
    };  
  
    WinJS.Namespace.define("Data", publicMembers);  
  
})();  
```  
  
## <a name="see-also"></a>请参阅  
 [快速入门：调试 HTML 和 CSS](../debugger/quickstart-debug-html-and-css.md)
