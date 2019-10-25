---
title: 创建适用于 Web 性能测试的请求级插件
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- request-level plug-in, creating
- Web performance tests, requests
ms.assetid: d0b5b23c-7e94-4637-be6c-2620a5442d46
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ce0a8030253e69b35deda379cffcf7475dc8bb62
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72653626"
---
# <a name="how-to-create-a-request-level-plug-in"></a>如何：创建请求级插件

请求  是构成 Web 性能测试的声明性语句。 使用 Web 性能测试插件，可以隔离代码并在 Web 性能测试中的主要声明性语句外部重用代码。 可以创建插件并将其添加到单个请求以及包含它的 Web 性能测试中。 自定义的请求插件  提供一种调用代码的方式（作为特定的请求在 Web 性能测试中运行）。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

每个 Web 性能测试请求插件都具有 PreRequest 方法和 PostRequest 方法。 将请求插件附加到某个特定的 http 请求之后，在发出请求之前将会激发 PreRequest 事件，并在收到请求之后激发 PostRequest 事件。

通过从 <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin> 基类派生你自己的类，可以创建自定义的 Web 性能测试请求插件。

可以将自定义的 Web 性能测试请求插件用于已记录的 Web 性能测试。 自定义的 Web 性能测试请求插件使你只需编写极少量的代码即可获得对 Web 性能测试的更大程度控制。 此外，还可以将它们用于编码 Web 性能测试。 请参阅[生成和运行编码的 Web 性能测试](../test/generate-and-run-a-coded-web-performance-test.md)。

## <a name="to-create-a-request-level-plug-in"></a>创建请求级插件

1. 在解决方案资源管理器中，右键单击解决方案，选择“添加”，然后选择“新建项目”    。

2. 创建新的“类库”项目  。

3. 在解决方案资源管理器中，右击新类库中的“引用”文件夹并选择“添加引用”    。

     将显示“添加引用”对话框  。

4. 选择“.NET”选项卡，向下滚动，选择“Microsoft.VisualStudio.QualityTools.WebTestFramework”，然后选择“确定”   

     对“Microsoft.VisualStudio.QualityTools.WebTestFramework”的引用将添加到解决方案资源管理器的“引用”文件夹中    。

5. 在解决方案资源管理器中，右键单击 Web 性能和负载测试项目（其中包含要添加 Web 性能测试请求测试插件的负载测试）的顶级节点  。 选择“添加引用”  。

     将显示“添加引用”对话框  。

6. 选择“项目”选项卡，选择“类库项目”，然后选择“确定”    。

7. 在代码编辑器中，编写插件的代码  。 首先，创建一个从 <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin> 派生的新公共类。

8. 实现 <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin.PreRequest*> 或/和 <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin.PostRequest*> 事件处理程序内的代码。 有关示例实现，请参见下面的“示例”部分。

9. 在编写完代码后，生成新项目。

10. 打开要在其中添加请求插件的 Web 性能测试。

11. 右击要在其中添加请求插件的请求，然后选择“添加请求插件”  。

     随即显示“添加 Web 测试请求插件”对话框  。

12. 在“选择插件”下，选择新插件  。

13. 在“选定插件的属性”窗格中，设置要在运行时使用的插件的初始值  。

    > [!NOTE]
    > 可根据需要从插件中公开任意多个属性；只需将其设置为公共、可设置并属于 Integer、Boolean 或 String 等基本类型。 以后还可以使用“属性”窗口更改 Web 性能测试插件属性。

14. 选择 **“确定”** 。

     将插件添加到“请求插件”文件夹中，该文件夹是 HTTP 请求的子文件夹  。

    > [!WARNING]
    > 在运行使用插件的 Web 性能测试或负载测试时，可能会出现与下类似的错误：
    >
    > **请求失败：\<插件> 事件中的异常：无法加载文件或程序集 '\<"Plug-in name".dll file>, Version=\<n.n.n.n>, Culture=neutral, PublicKeyToken=null' 或其依赖项之一。系统找不到指定的文件。**
    >
    > 如果对任何插件进行代码更改并创建新 DLL 版本 (Version=0.0.0.0)，则会引发这种情况，但插件仍会引用原来的插件版本  。 若要更正此问题，请执行以下步骤：
    >
    > 1. 在 Web 性能和负载测试项目中，将看到引用警告。 移除和重新添加对插件 DLL 的引用。
    > 2. 从测试或适当位置移除插件，然后再重新添加。

## <a name="example"></a>示例

可以使用以下代码来创建自定义的 Web 性能测试插件，其中会显示两个对话框。 一个对话框显示与要附加请求外接程序的请求相关联的 URL。 第二个对话框显示代理的计算机名称。

> [!NOTE]
> 下面的代码要求您添加对 System.Windows.Forms 的引用。

```csharp
using System;
using System.Collections.Generic;
using System.Windows.Forms;
using Microsoft.VisualStudio.TestTools.WebTesting;

namespace RequestPluginNamespace
{
    public class MyWebRequestPlugin : WebTestRequestPlugin
    {
        public override void PostRequest(object sender, PostRequestEventArgs e)
        {
            MessageBox.Show(e.WebTest.Context.AgentName);
        }
        public override void PreRequest(object sender, PreRequestEventArgs e)
        {
            MessageBox.Show(e.Request.Url);
        }
    }
}
```

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin>
- [为负载测试创建自定义代码和插件](../test/create-custom-code-and-plug-ins-for-load-tests.md)
- [为 Web 性能测试编码自定义提取规则](../test/code-a-custom-extraction-rule-for-a-web-performance-test.md)
- [为 Web 性能测试编码自定义验证规则](../test/code-a-custom-validation-rule-for-a-web-performance-test.md)
- [如何：创建负载测试插件](../test/how-to-create-a-load-test-plug-in.md)
- [生成和运行编码的 Web 性能测试](../test/generate-and-run-a-coded-web-performance-test.md)