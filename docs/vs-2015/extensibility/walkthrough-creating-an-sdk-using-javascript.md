---
title: 演练：使用 JavaScript 创建 SDK |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: a8c89d5d-5b78-4435-817f-c5f25ca6d715
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3e953d9051b9bc7e95dc29e02eb580c4d93fca26
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68148822"
---
# <a name="walkthrough-creating-an-sdk-using-javascript"></a>演练：使用 JavaScript 创建 SDK
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本演练介绍了如何使用 JavaScript 创建简单的数学运算 SDK 作为 Visual Studio 扩展 (VSIX)。  本演练分为以下部分：  
  
- [若要创建 SimpleMathVSIX 扩展 SDK 项目](../extensibility/walkthrough-creating-an-sdk-using-javascript.md#createSimpleMathVSIX)  
  
- [若要创建使用 SDK 的示例应用](../extensibility/walkthrough-creating-an-sdk-using-javascript.md#createSampleApp)  
  
  对于 JavaScript，没有任何类库项目类型。 在本演练中，在 VSIX 项目中直接创建示例 arithmetic.js 文件。 在实践中，我们建议您首先生成和测试的 JavaScript 和 CSS 文件为 Windows 应用商店应用程序 — 例如，通过使用**空白应用**模板，将其放在一个 VSIX 项目之前。  
  
## <a name="prerequisites"></a>系统必备  
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[Visual Studio SDK](../extensibility/visual-studio-sdk.md)。  
  
## <a name="createSimpleMathVSIX"></a> 若要创建 SimpleMathVSIX 扩展 SDK 项目  
  
1. 在菜单栏上，依次选择“文件”  、“新建”  、“项目”  。  
  
2. 在模板类别列表中下**Visual C#** ，选择**扩展性**，然后选择**VSIX 项目**模板。  
  
3. 在中**名称**文字框中，指定`SimpleMathVSIX`，然后选择**确定**按钮。  
  
4. 如果**Visual Studio 包向导**出现，请选择**下一步**按钮**欢迎**页上，然后在**7 的第 1 页**，选择**完成**按钮。  
  
     尽管**清单设计器**随即打开，我们将继续本演练简单通过直接修改清单文件。  
  
5. 在中**解决方案资源管理器**，打开 source.extension.vsixmanifest 文件的快捷菜单，然后选择**查看代码**。 使用此代码替换文件中的现有内容。  
  
    ```  
    <?xml version="1.0" encoding="utf-8"?>  
    <PackageManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011" xmlns:d="http://schemas.microsoft.com/developer/vsx-schema-design/2011">  
      <Metadata>  
        <Identity Id="SimpleMathVSIX" Version="1.0" Language="en-US" Publisher="myname" />  
        <DisplayName>Simple Math</DisplayName>  
        <Description>Does basic arithmetic calculations.</Description>  
      </Metadata>  
      <Installation Scope="Global" AllUsers="true">  
        <InstallationTarget Id="Microsoft.ExtensionSDK" TargetPlatformIdentifier="Windows" TargetPlatformVersion="v8.0" SdkName="SimpleMath" SdkVersion="1.0" />  
      </Installation>  
      <Dependencies>  
        <Dependency Id="Microsoft.Framework.NDP" DisplayName="Microsoft .NET Framework" d:Source="Manual" Version="4.5" />  
      </Dependencies>  
      <Assets>  
        <Asset Type="Microsoft.ExtensionSDK" d:Source="File" Path="SDKManifest.xml" />  
      </Assets>  
    </PackageManifest>  
    ```  
  
6. 在中**解决方案资源管理器**，打开 SimpleMathVSIX 项目的快捷菜单，然后选择**添加**，**新项**。  
  
7. 在中**数据**类别中，选择**XML 文件**，将文件命名`SDKManifest.xml`，然后选择**添加**按钮。  
  
8. 在中**解决方案资源管理器**，打开 SDKManifest.xml 文件的快捷菜单，然后选择**打开**以显示中的文件**XML 编辑器**。  
  
9. 将以下代码添加到在 SDKManifest.xml 文件中。  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <FileList  
      DisplayName="Simple Math"  
      MinVSVersion="14.0"  
      AppliesTo="JavaScript+WindowsAppContainer"  
      SupportsMultipleVersions="Error"  
      MoreInfo="http://www.msdn.microsoft.com/">  
  
      <!-- JS -->  
      <File Content="js\arithmetic.js" />  
    </FileList>  
  
    ```  
  
10. 在中**解决方案资源管理器**，在 SDKManifest.xml 文件的快捷菜单，选择**属性**。  
  
11. 在中**属性**窗口中，将**包含在 VSIX**属性设置为**True**。  
  
12. 在中**解决方案资源管理器**，在 SimpleMathVSIX 项目的快捷菜单，选择**添加**，**新文件夹**，然后将该文件夹和`Redist`。  
  
13. 添加下创建此文件夹结构的 Redist 子文件夹：  
  
     \Redist\CommonConfiguration\Neutral\SimpleMath\js\  
  
14. 在 \js\ 文件夹的快捷菜单，选择**外**，**新项**。  
  
15. 下**Visual C# 项**，选择**Web**类别中，并选择**JavaScript 文件**项。 将文件命名`arithmetic.js`，然后选择**添加**按钮。  
  
16. Arithmetic.js 中插入以下代码：  
  
    ```  
    (function (global) {  
        "use strict";  
        global.Arithmetic = {  
            add: function (firstNumber, secondNumber) {  
                return firstNumber + secondNumber;  
            },  
  
            subtract: function (firstNumber, secondNumber) {  
                return firstNumber - secondNumber;  
            },  
  
            multiply: function (firstNumber, secondNumber) {  
                return firstNumber * secondNumber;  
            },  
  
            divide: function (firstNumber, secondNumber) {  
                return firstNumber / secondNumber;  
            }  
        };  
    })(this);  
  
    ```  
  
17. 在中**解决方案资源管理器**，在 arithmetic.js 文件的快捷菜单，选择**属性**。 更改这些属性：  
  
    - 设置**包含在 VSIX**属性设置为**True**。  
  
    - 设置**复制到输出目录**属性设置为**始终复制**。  
  
18. 在中**解决方案资源管理器**，在 SimpleMathVSIX 项目的快捷菜单，选择**生成**。  
  
19. 生成项目的快捷菜单上成功完成后，选择**在文件资源管理器中打开文件夹**。 导航到 \bin\debug\\，并运行`SimpleMathVSIX.vsix`进行安装。  
  
20. 选择**安装**按钮并让安装完成。  
  
21. 重新启动 Visual Studio。  
  
## <a name="createSampleApp"></a> 若要创建使用 SDK 的示例应用  
  
1. 在菜单栏上，依次选择“文件”  、“新建”  、“项目”  。  
  
2. 在模板类别列表中下**JavaScript**，选择**Windows 应用商店**，然后选择**空白应用**模板。  
  
3. 在中**名称**框中，指定`ArithmeticUI`。 选择**确定**按钮。  
  
4. 在中**解决方案资源管理器**，打开 ArithmeticUI 项目的快捷菜单，然后选择**添加**，**引用**。  
  
5. 下**Windows**，选择**扩展**，您会发现**简单的数学运算**显示。  
  
6. 选择**简单的数学运算**复选框，然后选择**确定**按钮。  
  
7. 在中**解决方案资源管理器**下**引用**，请注意，**简单的数学运算**显示引用。 展开它，请注意，没有包括 arithmetic.js \js\ 文件夹。 您可以打开 arithmetic.js 若要确认已安装你的源代码。  
  
8. 使用以下代码替换 default.htm 的内容。  
  
    ```  
    <!DOCTYPE html>  
    <html>  
    <head>  
        <meta charset="utf-8" />  
        <title>ArithmeticUI</title>  
  
        <!-- WinJS references -->  
        <link href="//Microsoft.WinJS.1.0/css/ui-dark.css" rel="stylesheet" />  
        <script src="//Microsoft.WinJS.1.0/js/base.js"></script>  
        <script src="//Microsoft.WinJS.1.0/js/ui.js"></script>  
  
        <!-- ArithmeticUI references -->  
        <link href="/css/default.css" rel="stylesheet" />  
        <script src="/js/default.js"></script>  
        <script src="/SimpleMath/js/arithmetic.js"></script>  
    </head>  
    <body>  
        <form>  
        <div id="calculator" class="ms-grid">  
            <input name="firstNumber" id="firstNumber" type="number" step="any">  
            <div id="operators">  
                <button class="operator" type="button">+</button>  
                <button class="operator" type="button">-</button>  
                <button class="operator" type="button">*</button>  
                <button class="operator" type="button">/</button>  
            </div>  
            <input id="secondNumber" type="number">  
            <button class="calculate" type="button">=</button>  
            <input id="result" type="number" name="result" disabled="" readonly="">  
        </div>  
        </form>  
    </body>  
    </html>  
    ```  
  
9. 使用下一步的代码替换 \js\default.js 的内容。  
  
    ```  
    (function () {  
        "use strict";  
  
        var app = WinJS.Application;  
        var operation = null;  
  
        function calculateResult() {  
            var firstNumber = parseFloat(document.querySelector("#firstNumber").value),  
                secondNumber = parseFloat(document.querySelector("#secondNumber").value),  
                result = 0;  
  
            if (isNaN(firstNumber) || isNaN(secondNumber)) {  
                result = 0;  
            }  
            else {  
                switch (operation) {  
                    case "+":  
                        result = Arithmetic.add(firstNumber, secondNumber);  
                        break;  
                    case "-":  
                        result = Arithmetic.subtract(firstNumber, secondNumber);  
                        break;  
                    case "*":  
                        result = Arithmetic.multiply(firstNumber, secondNumber);  
                        break;  
                    case "/":  
                        result = Arithmetic.divide(firstNumber, secondNumber);  
                        break;  
                    default:  
                }  
            }  
            document.querySelector("#result").value = result.toString();  
        }  
  
        app.onactivated = function (args) {  
            document.querySelector("#calculator").addEventListener("click", function (event) {  
                if (event.target.tagName.toLowerCase() === "button") {  
                    switch (event.target.className) {  
                        case "operator":  
                            operation = event.target.innerText;  
                            break;  
                        case "calculate":  
                            calculateResult();  
                            break;  
                        default:  
                            break;  
                    }  
                }  
            });  
        };  
  
        app.start();  
    })();  
    ```  
  
10. 使用此代码替换 \css\default.css 的内容：  
  
    ```  
    form {  
        display: -ms-grid;  
        -ms-grid-rows: 1fr auto 1fr;  
        -ms-grid-columns: 1fr auto 1fr;  
        height: 100%;  
        width: 100%;  
    }  
  
    button, input[type=number] {  
        margin-right: 5px;  
        -ms-grid-row-align: center;  
    }  
  
    #calculator {  
        -ms-grid-column: 2;  
        -ms-grid-row: 2;  
        display: -ms-grid;  
        -ms-grid-rows: 1fr;  
        -ms-grid-columns: auto min-content auto auto auto;  
    }  
  
    .ms-grid input {  
        width: 5em;  
    }  
  
    #firstNumber {  
        -ms-grid-column: 1;  
        -ms-grid-row-align: center;  
    }  
  
    #operators {  
        -ms-grid-column: 2;  
        -ms-grid-row-align: center;  
    }  
  
        #operators button.operator {  
            margin-bottom: 5px;  
            height: 40px;  
        }  
  
    #secondNumber {  
        -ms-grid-column: 3;  
    }  
  
    button.calculate {  
        -ms-grid-column: 4;  
        -ms-grid-row-align: center;  
        height: 40px;  
    }  
  
    #result {  
        -ms-grid-column: 5;  
    }  
  
    ```  
  
11. 选择 F5 键以生成并运行应用。  
  
12. 在应用 UI 中，输入任何两个数字，选择一个操作，然后选择 **=** 按钮。 将显示正确的结果。  
  
## <a name="see-also"></a>请参阅  
 [获取软件开发工具包](../extensibility/creating-a-software-development-kit.md)
