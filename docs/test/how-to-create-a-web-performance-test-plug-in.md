---
title: 创建 Web 性能测试插件
ms.date: 10/03/2016
ms.topic: how-to
f1_keywords:
- vs.test.web.webtestplugin
helpviewer_keywords:
- Web performance tests, creating plug-ins
- plug-ins, creating in Web performance tests
ms.assetid: a612f2d2-9806-477d-a126-12842f07da6e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3c9651f4003647e18ba52e916aeb21e176274de5
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287930"
---
# <a name="how-to-create-a-web-performance-test-plug-in"></a>如何：创建 Web 性能测试插件

使用 Web 性能测试插件，可以隔离代码并在 Web 性能测试中的主要声明性语句外部重用代码。 自定义的 Web 性能测试插件为在运行 Web 性能测试时调用某些代码提供了途径。 在每个测试迭代中，Web 性能测试插件都要运行一次。 此外，如果重写测试插件中的 PreRequest 或 PostRequest 方法，这些请求插件将分别在每个请求之前或之后运行。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

通过从 <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestPlugin> 基类派生你自己的类，可以创建自定义的 Web 性能测试插件。

可以将自定义的 Web 性能测试插件用于已记录的 Web 性能测试，这样你只需编写极少量的代码即可获得对 Web 性能测试的更大程度控制。 此外，还可以将它们用于编码 Web 性能测试。 有关详细信息，请参阅[生成和运行编码的 Web 性能测试](../test/generate-and-run-a-coded-web-performance-test.md)。

> [!NOTE]
> 也可以创建负载测试插件。请参阅[如何：创建负载测试插件](../test/how-to-create-a-load-test-plug-in.md)。

## <a name="to-create-a-custom-web-performance-test-plug-in"></a>创建自定义 Web 性能测试插件

1. 打开包含 Web 性能测试的 Web 性能和负载测试项目。

2. 在解决方案资源管理器中，右键单击解决方案，选择“添加”，然后选择“新建项目”  。

3. 创建新的“类库”项目。

   新的类库项目将添加到解决方案资源管理器中，并且新类会出现在代码编辑器中 。

4. 在解决方案资源管理器中，右击新类库中的“引用”文件夹并选择“添加引用”  。

   将显示“添加引用”对话框。

5. 选择“.NET”选项卡，向下滚动，然后选择“Microsoft.VisualStudio.QualityTools.WebTestFramework” 

6. 选择 **“确定”** 。

     对“Microsoft.VisualStudio.QualityTools.WebTestFramework”的引用将添加到解决方案资源管理器的“引用”文件夹中  。

7. 在解决方案资源管理器中，右键单击 Web 性能和负载测试项目（其中包含要添加 Web 性能测试插件的负载测试）的顶级节点，然后选择“添加引用” 。

8. 将显示“添加引用”对话框。

9. 选择“项目”选项卡，然后选择“类库项目” 。

10. 选择 **“确定”** 。

11. 在代码编辑器中，编写插件的代码。 首先，创建一个从 <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestPlugin> 派生的新公共类。

12. 实现一个或多个事件处理程序内的代码。 有关示例实现，请参见下面的“示例”部分。

    - <xref:Microsoft.VisualStudio.TestTools.WebTesting.PostWebTestRecordingEventArgs>

    - <xref:Microsoft.VisualStudio.TestTools.WebTesting.PostWebTestEventArgs>

    - <xref:Microsoft.VisualStudio.TestTools.WebTesting.PreRequestEventArgs>

    - <xref:Microsoft.VisualStudio.TestTools.WebTesting.PostRequestEventArgs>

    - <xref:Microsoft.VisualStudio.TestTools.WebTesting.PrePageEventArgs>

    - <xref:Microsoft.VisualStudio.TestTools.WebTesting.PostPageEventArgs>

    - <xref:Microsoft.VisualStudio.TestTools.WebTesting.PreTransactionEventArgs>

    - <xref:Microsoft.VisualStudio.TestTools.WebTesting.PostTransactionEventArgs>

13. 在编写完代码后，生成新项目。

14. 打开 Web 性能测试。

15. 若要添加 Web 性能测试插件，请在工具栏上选择“添加 Web 测试插件”。

     随即显示“添加 Web 测试插件”对话框。

16. 在“选择插件”下，选择 Web 性能测试插件类。

17. 在“选定插件的属性”窗格中，设置要在运行时使用的插件的初始值。

    > [!NOTE]
    > 可根据需要从插件中公开任意多个属性；只需将其设置为公共、可设置并属于 Integer、Boolean 或 String 等基本类型。 以后还可以使用“属性”窗口更改 Web 性能测试插件属性。

18. 选择 **“确定”** 。

     该插件将添加到“Web 测试插件”文件夹中。

    > [!WARNING]
    > 在运行使用插件的 Web 性能测试或负载测试时，可能会出现与下类似的错误：
    >
    > **请求失败：\<plug-in> 事件中的异常：无法加载文件或程序集 '\<"Plug-in name".dll file>, Version=\<n.n.n.n>, Culture=neutral, PublicKeyToken=null' 或其依赖项之一。系统找不到指定的文件。**
    >
    > 如果对任何插件进行代码更改并创建新 DLL 版本 (Version=0.0.0.0)，则会引发这种情况，但插件仍会引用原来的插件版本。 若要更正此问题，请执行以下步骤：
    >
    > 1. 在 Web 性能和负载测试项目中，将看到引用警告。 移除和重新添加对插件 DLL 的引用。
    > 2. 从测试或适当位置移除插件，然后再重新添加。

## <a name="example"></a>示例

下面的代码用于创建一个自定义的 Web 性能测试插件，该插件向表示测试迭代的 <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestContext> 添加一项。

运行 Web 性能测试后，可使用此插件在 Web 性能结果查看器的“上下文”选项卡中查看名为“TestIteratnionNumber”的已添加项  。

```csharp
using System;
using System.Collections.Generic;
using System.Text;
using System.ComponentModel;
using Microsoft.VisualStudio.TestTools.WebTesting;

namespace SampleRules
{
    [Description("This plugin can be used to set the ParseDependentsRequests property for each request")]
    public class SampleWebTestPlugin : WebTestPlugin
    {
        private bool m_parseDependents = true;

        public override void PreWebTest(object sender, PreWebTestEventArgs e)
        {
            // TODO: Add code to execute before the test.
        }

        public override void PostWebTest(object sender, PostWebTestEventArgs e)
        {
            // TODO: Add code to execute after the test.
        }

        public override void PreRequest(object sender, PreRequestEventArgs e)
        {
            // Code to execute before each request.
            // Set the ParseDependentsRequests value on the request
            e.Request.ParseDependentRequests = m_parseDependents;
        }

        // Properties for the plugin.
        [DefaultValue(true)]
        [Description("All requests will have their ParseDependentsRequests property set to this value")]
        public bool ParseDependents
        {
            get
            {
                return m_parseDependents;
            }
            set
            {
                m_parseDependents = value;
            }
        }
    }
}
```

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin>
- [为负载测试创建自定义代码和插件](../test/create-custom-code-and-plug-ins-for-load-tests.md)
- [如何：创建请求级插件](../test/how-to-create-a-request-level-plug-in.md)
- [为 Web 性能测试编码自定义提取规则](../test/code-a-custom-extraction-rule-for-a-web-performance-test.md)
- [为 Web 性能测试编码自定义验证规则](../test/code-a-custom-validation-rule-for-a-web-performance-test.md)
- [如何：创建负载测试插件](../test/how-to-create-a-load-test-plug-in.md)
- [生成和运行编码的 Web 性能测试](../test/generate-and-run-a-coded-web-performance-test.md)
