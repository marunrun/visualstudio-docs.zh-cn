---
title: 创建负载测试插件
ms.date: 10/19/2016
ms.topic: conceptual
f1_keywords:
- vs.test.load.loadtestplugin
helpviewer_keywords:
- code, load tests
- plug-ins, load test
- load tests, plug-ins
ms.assetid: 27806972-1b15-4388-833d-6d0632816f1f
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e2eea116eb18e192720410b71136de9d823ed0fe
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72653670"
---
# <a name="how-to-create-a-load-test-plug-in"></a>如何：创建负载测试插件

可以创建负载测试插件，以便在负载测试运行过程中的不同时间运行代码。 可以创建插件来扩展或修改负载测试的内置功能。 例如，可以编写负载测试插件代码，以便在负载测试运行过程中设置或修改负载测试模式。 若要执行此操作，必须创建一个继承 <xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin> 接口的类。 此类必须实现此接口的 <xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin.Initialize*> 方法。 有关详细信息，请参阅 <xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin>。

> [!TIP]
> 还可以创建 Web 性能测试插件。 有关详细信息，请参阅[如何：创建 Web 性能测试插件](../test/how-to-create-a-web-performance-test-plug-in.md)。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

<!-- markdownlint-disable MD003 MD020 -->
## <a name="to-create-a-load-test-plug-in-in-c"></a>用 C# 语言创建负载测试插件
<!-- markdownlint-enable MD003 MD020 -->

1. 打开包含 Web 性能测试的 Web 性能和负载测试项目。

2. 向该测试项目中添加一个负载测试，并对其进行配置以运行 Web 性能测试。

     有关详细信息，请参阅[快速入门：创建负载测试项目](../test/quickstart-create-a-load-test-project.md)。

3. 将新的“类库”项目添加到该解决方案中  。 （在“解决方案资源管理器”中，右键单击解决方案，选择“添加”，然后选择“新建项目”    。）

4. 在解决方案资源管理器中，右击新类库中的“引用”文件夹并选择“添加引用”    。

   将显示“添加引用”对话框  。

5. 选择“.NET”选项卡，向下滚动，然后选择“Microsoft.VisualStudio.QualityTools.LoadTestFramework”   。

6. 选择 **“确定”** 。

   将对 Microsoft.VisualStudio.QualityTools.LoadTestFramework 的引用添加到解决方案资源管理器的“引用”文件夹中    。

7. 在解决方案资源管理器中，右键单击 Web 性能和负载测试项目（其中包含要添加负载测试插件的负载测试）的顶级节点，然后选择“添加引用”   。

   将显示“添加引用”对话框  。

8. 选择“项目”选项卡，然后选择“类库项目”  。

9. 选择 **“确定”** 。

10. 在代码编辑器中，为 <xref:Microsoft.VisualStudio.TestTools.LoadTesting> 命名空间添加一个 `using` 语句  。

11. 为在类库项目中创建的类实现 <xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin> 接口。 有关示例实现，请参见下面的“示例”部分。

12. 在编写完代码后，生成新项目。

13. 右键单击负载测试的顶级节点，然后选择“添加负载测试插件”  。

     随即显示“添加负载测试插件”对话框  。

14. 在“选择插件”下，选择负载测试插件类  。

15. 在“选定插件的属性”窗格中，设置要在运行时使用的插件的初始值  。

    > [!NOTE]
    > 可根据需要从插件中公开任意多个属性；只需将其设置为公共、可设置并属于 Integer、Boolean 或 String 等基本类型。 以后还可使用“属性”窗口更改 Web 性能测试插件属性  。

16. 选择 **“确定”** 。

     将插件添加到“负载测试插件”文件夹中  。

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

下面的代码演示在 LoadTestFinished 事件发生后运行自定义代码的负载测试插件。 如果此代码在远程计算机上的某个测试代理上运行，并且该测试代理没有 localhost SMTP 服务，则负载测试将保持“正在进行”状态，因为将打开一个消息框。

> [!NOTE]
> 下面的代码要求您添加对 System.Windows.Forms 的引用。

```csharp
using System;
using Microsoft.VisualStudio.TestTools.LoadTesting;
using System.Net.Mail;
using System.Windows.Forms;

namespace LoadTestPluginTest
{
    public class MyLoadTestPlugin : ILoadTestPlugin
    {
        LoadTest myLoadTest;

        public void Initialize(LoadTest loadTest)
        {
            myLoadTest = loadTest;
            myLoadTest.LoadTestFinished += new
                EventHandler(myLoadTest_LoadTestFinished);
        }

        void myLoadTest_LoadTestFinished(object sender, EventArgs e)
        {
            try
            {
                // place custom code here
                MailAddress MyAddress = new MailAddress("someone@example.com");
                MailMessage MyMail = new MailMessage(MyAddress, MyAddress);
                MyMail.Subject = "Load Test Finished -- Admin Email";
                MyMail.Body = myLoadTest..Name + " has finished.";

                SmtpClient MySmtpClient = new SmtpClient("localhost");
                MySmtpClient.Send(MyMail);
            }

            catch (SmtpException ex)
            {
                MessageBox.Show(ex.InnerException.Message +
                    ".\r\nMake sure you have a valid SMTP.", "LoadTestPlugin", MessageBoxButtons.OK, MessageBoxIcon.Warning, MessageBoxDefaultButton.Button1);
            }
        }
    }
}
```

有八种事件与一个负载测试相关联，可在负载测试插件中处理该负载测试，以便使用该负载测试运行自定义代码。 以下是事件的列表，这些事件提供对负载测试运行的不同时间段的访问：

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.LoadTestStarting>

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.LoadTestFinished>

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.LoadTestWarmupComplete>

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.TestStarting>

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.TestFinished>

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.ThresholdExceeded>

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.Heartbeat>

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.LoadTestAborted>

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin>
- [为负载测试创建自定义代码和插件](../test/create-custom-code-and-plug-ins-for-load-tests.md)
- [如何：创建 Web 性能测试插件](../test/how-to-create-a-web-performance-test-plug-in.md)