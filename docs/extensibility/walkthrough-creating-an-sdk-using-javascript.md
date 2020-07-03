---
title: 演练：使用 JavaScript 创建 SDK |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: a8c89d5d-5b78-4435-817f-c5f25ca6d715
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 29dac6cca7936dde8be2ebc57366f6370b8bcbc6
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904948"
---
# <a name="walkthrough-create-an-sdk-using-javascript"></a>演练：使用 JavaScript 创建 SDK
本演练介绍了如何使用 JavaScript 以 Visual Studio 扩展（VSIX）的形式创建简单的数学 SDK。  本演练分为以下几个部分：

- [创建 SimpleMathVSIX 扩展 SDK 项目](../extensibility/walkthrough-creating-an-sdk-using-javascript.md#createSimpleMathVSIX)

- [创建使用 SDK 的示例应用](../extensibility/walkthrough-creating-an-sdk-using-javascript.md#createSampleApp)

  对于 JavaScript，没有类库项目类型。 在本演练中，示例*arithmetic.js*文件是直接在 VSIX 项目中创建的。 在实际情况下，我们建议您首先构建 JavaScript 和 CSS 文件作为 Windows 应用商店应用程序（例如，通过使用**空白应用**程序模板），然后将它们放在 VSIX 项目中。

## <a name="prerequisites"></a>必备条件
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)。

## <a name="to-create-the-simplemathvsix-extension-sdk-project"></a><a name="createSimpleMathVSIX"></a>创建 SimpleMathVSIX 扩展 SDK 项目

1. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

2. 在模板类别列表中的 " **Visual c #**" 下，选择 "**扩展性**"，然后选择 " **VSIX 项目**" 模板。

3. 在 "**名称**" 文本框中，指定 `SimpleMathVSIX` 并选择 "**确定"** 按钮。

4. 如果显示**Visual Studio 包向导**，请选择 "**欢迎**" 页上的 "**下一步**" 按钮，然后在**第1页**，单击 "**完成**" 按钮。

     尽管**清单设计器**会打开，但我们将通过直接修改清单文件来简化本演练。

5. 在**解决方案资源管理器**中，打开**source.extension.vsixmanifest**文件的快捷菜单，然后选择 "**查看代码**"。 使用此代码替换文件中的现有内容。

    ```xml
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

6. 在**解决方案资源管理器**中，打开**SimpleMathVSIX**项目的快捷菜单，然后选择 "**添加**  >  **新项**"。

7. 在 "**数据**" 类别中，选择 " **XML 文件**"，为文件命名 `SDKManifest.xml` ，然后选择 "**添加**" 按钮。

8. 在**解决方案资源管理器**中，打开**SDKManifest.xml**文件的快捷菜单，然后选择 "**打开**" 以在**XML 编辑器**中显示该文件。

9. 将以下代码添加到**SDKManifest.xml**文件中。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <FileList
      DisplayName="Simple Math"
      MinVSVersion="14.0"
      AppliesTo="JavaScript+WindowsAppContainer"
      SupportsMultipleVersions="Error"
      MoreInfo="https://msdn.microsoft.com/">

      <!-- JS -->
      <File Content="js\arithmetic.js" />
    </FileList>

    ```

10. 在**解决方案资源管理器**的**SDKManifest.xml**文件的快捷菜单上，选择 "**属性**"。

11. 在 "**属性**" 窗口中，将 "**包括在 VSIX 中**" 属性设置为 " **True**"。

12. 在**解决方案资源管理器**的**SimpleMathVSIX**项目的快捷菜单上，选择 "**添加**  >  **新文件夹**"，然后命名文件夹 `Redist` 。

13. 添加已再发行的子文件夹，以创建此文件夹结构：

     *\Redist\CommonConfiguration\Neutral\SimpleMath\js\\*

14. 在**\js \\ **文件夹的快捷菜单上，选择 "**添加**  >  **新项**"。

15. 在 " **Visual c # 项**" 下，选择 " **Web** " 类别，然后选择**JavaScript 文件**项。 命名该文件 `arithmetic.js` ，然后选择 "**添加**" 按钮。

16. 将以下代码插入*arithmetic.js*：

    ```csharp
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

17. 在**解决方案资源管理器**的**arithmetic.js**文件的快捷菜单上，选择 "**属性**"。 进行这些属性更改：

    - 将 "**包括在 VSIX 中**" 属性设置为 " **True**"。

    - 将 "**复制到输出目录**" 属性设置为 "**始终复制**"。

18. 在**解决方案资源管理器**的**SimpleMathVSIX**项目的快捷菜单上，选择 "**生成**"。

19. 成功完成生成后，在项目的快捷菜单上，选择 "**在文件资源管理器中打开文件夹**"。 导航到**\bin\debug \\ **，然后运行 `SimpleMathVSIX.vsix` 安装。

20. 选择 "**安装**" 按钮，让安装完成。

21. 重启 Visual Studio。

## <a name="to-create-a-sample-app-that-uses-the-sdk"></a><a name="createSampleApp"></a>创建使用 SDK 的示例应用

1. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

2. 在模板类别列表中的 " **JavaScript**" 下，选择 " **Windows 应用商店**"，然后选择 "**空白应用**" 模板。

3. 在 "**名称**" 框中，指定 `ArithmeticUI` 。 选择“确定”  按钮。

4. 在**解决方案资源管理器**中，打开**ArithmeticUI**项目的快捷菜单，然后选择 "**添加**  >  **引用**"。

5. 在 " **Windows**" 下，选择 "**扩展**"，并注意显示了**简单的数学**。

6. 选中 "**简单数学**" 复选框，然后选择 **"确定"** 按钮。

7. 在**解决方案资源管理器**的 "**引用**" 下，请注意显示了**简单的数学**引用。 展开它，请注意，有一个**\js \\ **文件夹，其中包含**arithmetic.js**。 可以打开**arithmetic.js**以确认是否已安装源代码。

8. 使用以下代码替换*default.htm*的内容。

   ```html
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

9. 使用以下代码替换*\js\default.js*的内容。

    ```csharp
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

10. 将*\css\default.css*的内容替换为以下代码：

    ```xml
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

11. 选择**F5**键生成并运行应用。

12. 在应用程序 UI 中，输入任意两个数字，选择一个操作，然后选择 **=** 按钮。 显示正确的结果。

## <a name="see-also"></a>另请参阅
- [创建软件开发工具包](../extensibility/creating-a-software-development-kit.md)
