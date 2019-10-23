---
title: 使用编码的 UI 测试日志分析编码的 UI 测试
ms.date: 11/04/2016
ms.topic: conceptual
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
author: jillre
ms.openlocfilehash: 73916d309fa0e070bf4b05ba0d5a8fc02bef29f8
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665322"
---
# <a name="analyzing-coded-ui-tests-using-coded-ui-test-logs"></a>使用编码的 UI 测试日志分析编码的 UI 测试

编码的 UI 测试日志筛选并录制关于编码的 UI 测试运行的重要信息。 这些日志以允许快速调试问题的形式呈现。

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

## <a name="step-1-enable-logging"></a>步骤 1：启用日志记录

根据方案使用以下方法之一启用日志：

- 测试项目中不存在 App.config  文件：

   1. 确定运行测试时启动了哪个 QTAgent\*.exe  进程。 一种方法是查看 Windows“任务管理器”  中的“详细信息”  选项卡。

   2. 从 %ProgramFiles(x86)%\Microsoft Visual Studio\\\<version>\\\<edition>\Common7\IDE  文件夹打开相应的 .config  文件。 例如，如果运行的进程是 QTAgent_40.exe  ，则打开 QTAgent_40.exe.config  。

   2. 将 EqtTraceLevel  的值修改为所需的日志级别。

      ```xml
      <!-- You must use integral values for "value".
           Use 0 for off, 1 for error, 2 for warn, 3 for info, and 4 for verbose. -->
      <add name="EqtTraceLevel" value="4" />
      ```

   3. 保存该文件。

- 如果测试项目中存在 App.config  文件：

  - 打开项目中 App.config 文件，并在配置节点下添加以下代码  ：

    ```xml
    <system.diagnostics>
      <switches>
        <add name="EqtTraceLevel" value="4" />
      </switches>
    </system.diagnostics>`
    ```

- 从测试代码本身启用日志记录：

   ```csharp
   Microsoft.VisualStudio.TestTools.UITesting.PlaybackSettings.LoggerOverrideState = HtmlLoggerState.AllActionSnapshot;
   ```

## <a name="step-2-run-your-coded-ui-test-and-view-the-log"></a>步骤 2：运行编码的 UI 测试并查看日志

对 QTAgent\*.exe.config  文件就地运行编码的 UI 测试并对其进行修改时，可在“测试资源管理器”  结果中看到一条输出链接。 日志文件不仅在测试失败时生成，而且在跟踪级别设置为“详细”  时也会对成功的测试生成。

1. 在“测试”菜单上，选择“窗口”，然后选择“测试资源管理器”    。

2. 在 **“生成”** 菜单上，选择 **“生成解决方案”** 。

3. 在测试资源管理器中，选择想要运行的编码的 UI 测试、打开其快捷菜单，然后选择“运行选定测试”   。

     自动测试会运行并指示它们是否通过。

    > [!TIP]
    > 要查看测试资源管理器，请选择“测试” > “窗口”，然后选择“测试资源管理器”     。

4. 在“测试资源管理器”结果中选择“输出”链接   。

     ![测试资源管理器中的输出链接](../test/media/cuit_htmlactionlog1.png)

     随即显示测试的输出，其中包括指向操作日志的链接。

     ![编码的 UI 测试中的结果和输出链接](../test/media/cuit_htmlactionlog2.png)

5. 选择 UITestActionLog.html 链接  。

     该日志显示在你的 Web 浏览器中。

     ![编码的 UI 测试日志文件](../test/media/cuit_htmlactionlog3.png)

## <a name="see-also"></a>请参阅

- [使用 UI 自动化来测试代码](../test/use-ui-automation-to-test-your-code.md)
- [如何：通过 Microsoft Visual Studio 运行测试](https://msdn.microsoft.com/Library/1a1207a9-2a33-4a1e-a1e3-ddf0181b1046)
