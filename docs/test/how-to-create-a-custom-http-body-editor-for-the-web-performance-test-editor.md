---
title: 为 Web 性能测试编辑器创建自定义 HTTP 正文编辑器
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- Web performance tests, custom HTTP body editor
ms.assetid: a0b2d8ff-3e2a-487e-9172-90047174f336
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 30ce24b0cb48e88ddb77cf3576d40f95ed022ba0
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68926513"
---
# <a name="how-to-create-a-custom-http-body-editor-for-the-web-performance-test-editor"></a>如何：为 Web 性能测试编辑器创建自定义 HTTP 正文编辑器

可创建自定义内容编辑器，通过它来编辑 Web 服务请求的字符串主体内容或二进制主体内容，例如 SOAP、REST、asmx、wcf、RIA 和其他 Web 服务请求类型。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

可以实现以下类型的编辑器：

- **字符串内容编辑器** 此编辑器是使用 <xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin> 接口实现的。

- **二进制内容编辑器** 此编辑器是使用 <xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin> 接口实现的。

这些接口包含在 <xref:Microsoft.VisualStudio.TestTools.WebTesting> 命名空间中。

## <a name="create-a-windows-control-library-project"></a>创建 Windows 控件库项目

1. 在 Visual Studio 中，创建新的“Windows 窗体控件库”项目  。 将项目命名为 MessageEditors  。

   项目将添加到新解决方案中，设计器中将显示一个名为 UserControl1.cs 的 <xref:System.Windows.Forms.UserControl>  。

1. 从“工具箱”的“公共控件”类别下，将 <xref:System.Windows.Forms.RichTextBox> 拖动到 UserControl1 的曲面上   。

1. 选择 <xref:System.Windows.Forms.RichTextBox> 控件右上角的操作标记标志符号（![智能标记字形](../test/media/vs_winformsmttagglyph.gif)），然后选择“在父容器中停靠”  。

1. 在解决方案资源管理器中，右键单击“Windows 窗体库”项目，然后选择“属性”   。

1. 在“属性”中，选择“应用程序”选项卡   。

1. 在“目标框架”下拉列表中，选择 .NET Framework 4（或更高版本）  。

1. 随即显示“目标框架更改”对话框  。

1. 选择 **“是”** 。

1. 在解决方案资源管理器中，右键单击“引用”节点并选择“添加引用”    。

1. 将显示“添加引用”对话框  。

1. 选择“.NET”选项卡，向下滚动并选择“Microsoft.VisualStudio.QualityTools.WebTestFramework”，然后选择“确定”    。

1. 如果视图设计器仍未打开，请在解决方案资源管理器中右键单击“UserControl1.cs”，然后选择“视图设计器”     。

1. 在设计曲面上，右键单击并选择“查看代码”  。

1. （可选）将类和构造函数的名称从 UserControl1 更改为有意义的名称，例如 MessageEditorControl：

    > [!NOTE]
    > 此示例使用 MessageEditorControl。

    ```csharp
    namespace MessageEditors
    {
        public partial class MessageEditorControl : UserControl
        {
            public MessageEditorControl()
            {
                InitializeComponent();
            }
        }
    }
    ```

1. 添加以下属性，以允许在 RichTextBox1 中获取和设置文本。 <xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin> 接口将使用 EditString，<xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin> 将使用 EditByteArray：

    ```csharp
    public String EditString
    {
       get
       {
           return this.richTextBox1.Text;
       }
       set
       {
           this.richTextBox1.Text = value;
       }
    }

    public byte[] EditByteArray
    {
       get
       {
           return System.Convert.FromBase64String(richTextBox1.Text);
       }
       set
       {
           richTextBox1.Text = System.Convert.ToBase64String(value, 0, value.Length);
       }
    }
    ```

## <a name="add-a-class-to-the-windows-control-library-project"></a>向 Windows 控件库项目中添加类

向项目中添加类。 该类将用于实现 <xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin> 和 <xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin> 接口。

**此过程中的代码概述**

在前面过程中创建的 MessageEditorControl <xref:System.Windows.Forms.UserControl> 将实例化为 messageEditorControl：

```csharp
private MessageEditorControl messageEditorControl
```

messageEditorControl 实例承载在 <xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin.CreateEditor*> 方法创建的插件对话框中。 此外，messageEditorControl 的 <xref:System.Windows.Forms.RichTextBox> 将由 <xref:Microsoft.VisualStudio.TestTools.WebTesting.IHttpBody> 中的内容进行填充。 但是，除非 <xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin.SupportsContentType*> 返回 `true`，否则无法创建插件。 对于此编辑器，如果 <xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin.SupportsContentType*> 中的 `true` 包含“xml”，则 <xref:Microsoft.VisualStudio.TestTools.WebTesting.IHttpBody.ContentType*> 返回 <xref:Microsoft.VisualStudio.TestTools.WebTesting.IHttpBody>。

当完成字符串主体的编辑并且用户在插件对话框中单击“确定”时，将调用 <xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin.GetNewValue*> 以获取字符串形式的已编辑文本，并在 Web 测试性能编辑器的请求中更新“字符串主体”   。

### <a name="create-a-class-and-implement-the-istringhttpbodyeditorplugin-interface"></a>创建类并实现 IStringHttpBodyEditorPlugin 接口

1. 在解决方案资源管理器中，右键单击 Windows 窗体控件库项目并选择“添加新项”   。

   随即出现“添加新项”  对话框。

2. 选择“类”  。

3. 在“名称”文本框中，为类键入有意义的名称，例如 `MessageEditorPlugins`  。

4. 选择“添加”  。

   Class1 将添加到该项目中，并在代码编辑器中显示。

5. 在代码编辑器中，添加以下 `using` 语句：

    ```csharp
    using Microsoft.VisualStudio.TestTools.WebTesting;
    ```

6. 粘贴到以下代码以实现该接口：

    ```csharp
    /// <summary>
    /// Editor for generic text based hierarchical messages such as XML and JSON.
    /// </summary>
    public class XmlMessageEditor : IStringHttpBodyEditorPlugin
    {
        public XmlMessageEditor()
        {
        }

        /// <summary>
        /// Determine if this plugin supports the content type.
        /// </summary>
        /// <param name="contentType">The content type to test.</param>
        /// <returns>Returns true if the plugin supports the specified content type.</returns>
        public bool SupportsContentType(string contentType)
        {
            return contentType.ToLower().Contains("xml");
        }

        /// <summary>
        /// Create a UserControl to edit the specified bytes.
        /// This control will be hosted in the
        /// plugin dialog which provides OK and Cancel buttons.
        /// </summary>
        /// <param name="contentType">The content type of the BinaryHttpBody.</param>
        /// <param name="initialValue">The bytes to edit. The bytes are the payload of a BinaryHttpBody.</param>
        /// <returns>A UserControl capable of displaying and editing the byte array value of the specified content type.</returns>
        public object CreateEditor(string contentType, string initialValue)
        {
            messageEditorControl = new MessageEditorControl();
            messageEditorControl.EditString = initialValue;
            return this.messageEditorControl;
        }

        /// <summary>
        /// Gets the edited bytes after the OK button is clicked on the plugin dialog.
        /// </summary>
        public string GetNewValue()
        {
            return messageEditorControl.EditString;
        }

        private MessageEditorControl messageEditorControl;
    }
    ```

## <a name="add-a-ibinaryhttpbodyeditorplugin-to-the-class"></a>向类中添加 IBinaryHttpBodyEditorPlugin

实现 <xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin> 接口。

**此过程中的代码概述**

<xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin> 接口的代码实现与前面过程中介绍的 <xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin> 类似。 但是，二进制版本使用字节数组来处理二进制数据而不是字符串。

在第一个过程中创建的 MessageEditorControl <xref:System.Windows.Forms.UserControl> 将实例化为 messageEditorControl：

```csharp
private MessageEditorControl messageEditorControl
```

messageEditorControl 实例承载在 <xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin.CreateEditor*> 方法创建的插件对话框中。 此外，messageEditorControl 的 <xref:System.Windows.Forms.RichTextBox> 将由 <xref:Microsoft.VisualStudio.TestTools.WebTesting.IHttpBody> 中的内容进行填充。 但是，除非 <xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin.SupportsContentType*> 返回 `true`，否则无法创建插件。 对于此编辑器，如果 <xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin.SupportsContentType*> 中的 `true` 包含“msbin1”，<xref:Microsoft.VisualStudio.TestTools.WebTesting.IHttpBody.ContentType*> 返回 <xref:Microsoft.VisualStudio.TestTools.WebTesting.IHttpBody>。

当完成字符串主体的编辑并且用户在插件对话框中单击“确定”时，将调用 <xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin.GetNewValue*> 以获取字符串形式的已编辑文本，并在 Web 测试性能编辑器的请求中更新“BinaryHttpBody.Data”   。

### <a name="to-add-the-ibinaryhttpbodyeditorplugin-to-the-class"></a>向类中添加 IBinaryHttpBodyEditorPlugin

- 在前面过程中添加的 XmlMessageEditor 类下编写或复制以下代码以从 <xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin> 接口实例化 Msbin1MessageEditor 类并实现所需方法：

    ```csharp
    /// <summary>
        /// Editor for MSBin1 content type (WCF messages)
        /// </summary>
        public class Msbin1MessageEditor : IBinaryHttpBodyEditorPlugin
        {
            /// <summary>
            ///
            /// </summary>
            public Msbin1MessageEditor()
            {
            }

            /// <summary>
            /// Determine if this plugin supports a content type.
            /// </summary>
            /// <param name="contentType">The content type to test.</param>
            /// <returns>Returns true if the plugin supports the specified content type.</returns>
            public bool SupportsContentType(string contentType)
            {
                return contentType.ToLower().Contains("msbin1");
            }

            /// <summary>
            /// Create a UserControl to edit the specified bytes. This control will be hosted in the
            /// plugin dialog which provides OK and Cancel buttons.
            /// </summary>
            /// <param name="contentType">The content type of the BinaryHttpBody.</param>
            /// <param name="initialValue">The bytes to edit. The bytes are the payload of a BinaryHttpBody.</param>
            /// <returns>A UserControl capable of displaying and editing the byte array value of the specified content type.</returns>
            public object CreateEditor(string contentType, byte[] initialValue)
            {
                messageEditorControl = new MessageEditorControl();
                messageEditorControl.EditByteArray = initialValue;
                return messageEditorControl;
            }

            /// <summary>
            /// Gets the edited bytes after the OK button is clicked on the plugin dialog.
            /// </summary>
            public byte[] GetNewValue()
            {
                return messageEditorControl.EditByteArray;
            }

            private MessageEditorControl messageEditorControl;
            private object originalMessage;
        }
    ```

## <a name="build-and-deploy-the-plug-ins"></a>生成和部署插件

1. 在“生成”菜单上，选择“生成 \<Windows 窗体控件库项目名称>”   。

2. 关闭 Visual Studio 的所有实例。

   > [!NOTE]
   > 关闭 Visual Studio，确保在尝试复制 .dll 文件前不会锁定它  。

3. 将生成的 .dll 文件（如 MessageEditors.dll）从项目的 bin\debug 文件夹复制到 %ProgramFiles%\Microsoft Visual Studio\2017\\\<edition>\Common7\IDE\PrivateAssemblies\WebTestPlugins     。

4. 打开 Visual Studio。

   .dll 现已在 Visual Studio 中注册  。

## <a name="verify-the-plug-ins-using-a-web-performance-test"></a>使用 Web 性能测试验证插件

1. 创建测试项目。

2. 创建 Web 性能测试，然后在浏览器中输入指向 Web 服务的 URL。

3. 记录完成后，在 Web 性能测试编辑器中展开对 Web 服务的请求，然后选择“字符串主体”或“二进制主体”   。

4. 在“属性”窗口中，选择“字符串主体”或“二进制主体”，然后选择省略号 (…)   。

   “编辑 HTTP 主体数据”对话框随即显示  。

5. 现在即可编辑数据，然后选择“确定”  。 此操作会调用适用的 GetNewValue 方法以更新 <xref:Microsoft.VisualStudio.TestTools.WebTesting.IHttpBody> 中的内容。

## <a name="compile-the-code"></a>编译代码

确认 Windows 控件库项目的目标框架为 .NET Framework 4.5。 默认情况下，Windows 控件库项目以 .NET Framework 4.5 客户端框架为目标，此框架不允许包含 Microsoft.VisualStudio.QualityTools.WebTestFramework 引用。

有关详细信息，请参阅[项目设计器中应用程序页 (C#)](../ide/reference/application-page-project-designer-csharp.md)。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.IHttpBody>
- <xref:System.Windows.Forms.UserControl>
- <xref:System.Windows.Forms.RichTextBox>
- [为负载测试创建自定义代码和插件](../test/create-custom-code-and-plug-ins-for-load-tests.md)
- [如何：创建请求级插件](../test/how-to-create-a-request-level-plug-in.md)
- [为 Web 性能测试编码自定义提取规则](../test/code-a-custom-extraction-rule-for-a-web-performance-test.md)
- [为 Web 性能测试编码自定义验证规则](../test/code-a-custom-validation-rule-for-a-web-performance-test.md)
- [如何：创建负载测试插件](../test/how-to-create-a-load-test-plug-in.md)
- [生成和运行编码的 Web 性能测试](../test/generate-and-run-a-coded-web-performance-test.md)
- [如何：为 Web 性能测试结果查看器创建 Visual Studio 外接程序](../test/how-to-create-an-add-in-for-the-web-performance-test-results-viewer.md)