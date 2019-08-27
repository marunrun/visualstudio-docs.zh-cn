---
title: 如何：创建诊断数据适配器
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- Diagnostic Data Adapter, creating
ms.assetid: bd7ad36c-54cb-4d2a-9aea-9d10ad98d7ba
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 517d4e0558aeca1518316520191ae6c662b41a9e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62950716"
---
# <a name="how-to-create-a-diagnostic-data-adapter"></a>如何：创建诊断数据适配器

若要创建诊断数据适配器，请使用 Visual Studio 创建一个类库，然后将 Visual Studio Enterprise 提供的诊断数据适配器 API 添加到该类库中。 处理测试运行期间引发的事件时，以流或文件的形式将所需的任何信息发送到框架提供的 <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionSink>。 测试完成时，发送到 <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionSink> 的流或文件将以附件形式存储到测试结果中。 如果根据这些测试结果创建 Bug，或者在使用[!INCLUDE[mtrlong](../test/includes/mtrlong_md.md)] 时，这些文件也会链接到 Bug。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

可以创建一个诊断数据适配器，它会影响在其上运行测试的计算机，或用于运行受测应用程序的环境中包含的计算机。 例如，该诊断数据适配器在运行测试的测试计算机上收集文件，或在充当应用程序的 Web 服务器角色的计算机上收集文件。

可以为诊断数据适配器指定一个友好名称，使用 Microsoft 测试管理器或 Visual Studio 创建测试设置时会显示该名称。 利用测试设置可以定义在运行测试时，哪个计算机角色将在环境中运行特定诊断数据适配器。 也可以在创建测试设置时配置诊断数据适配器。 例如，可以创建用于从 Web 服务器收集自定义日志的诊断数据适配器。 在创建测试设置时，可以选择在执行此 Web 服务器角色的一台或多台计算机上运行此诊断数据适配器，并且可以修改测试设置的配置以便仅收集已创建的最后三个日志。 有关测试设置的详细信息，请参阅[使用测试设置收集诊断信息](../test/collect-diagnostic-information-using-test-settings.md)。

运行测试时将引发事件，这使诊断数据适配器可以在测试中的该点执行任务。

> [!IMPORTANT]
> 这些事件可以在不同的线程中引发，特别是当你在多台计算机上运行测试时。 因此，必须注意可能的线程问题，不要意外损坏自定义适配器的内部数据。 请确保您的诊断数据适配器是线程安全的。

下面是创建诊断数据适配器时可以使用的关键事件的部分列表。 有关诊断数据适配器事件的完整列表，请参见 <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents> 抽象类。

|事件|说明|
|-|-----------------|
|<xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents.SessionStart>|开始测试运行|
|<xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents.SessionEnd>|结束测试运行|
|<xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents.TestCaseStart>|开始测试运行中的每个测试|
|<xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents.TestCaseEnd>|结束测试运行中的每个测试|
|<xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents.TestStepStart>|开始测试中的每个测试步骤|
|<xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents.TestStepEnd>|结束测试中的每个测试步骤|

> [!NOTE]
> 完成手动测试时，不再将数据集合事件发送到诊断数据适配器。 测试重新运行时，将具有新的测试用例标识符。 如果用户在测试期间重置测试（这会引发 <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents.TestCaseReset> 事件）或更改测试步骤结果，将不会向诊断数据适配器发送任何数据收集事件，但测试用例标识符保持不变。 若要确定是否重置了测试用例，必须跟踪诊断数据适配器中的测试用例标识符。

使用下面的过程可创建诊断数据适配器，以收集基于在创建测试设置时所配置的信息的数据文件。

有关诊断数据适配器项目（包括自定义配置编辑器）的完整示例，请参阅[用于创建诊断数据适配器的示例项目](../test/quickstart-create-a-load-test-project.md)。

## <a name="create-and-install-a-diagnostic-data-adapter"></a>创建并安装诊断数据适配器

1. 创建新的“类库”项目。

2. 添加程序集“Microsoft.VisualStudio.QualityTools.ExecutionCommon”。

   1. 在解决方案资源管理器中，右键单击“引用”，然后选择“添加引用”命令。

   2. 选择“.NET”并查找“Microsoft.VisualStudio.QualityTools.ExecutionCommon.dll”。

   3. 选择 **“确定”**。

3. 添加程序集“Microsoft.VisualStudio.QualityTools.Common”。

   1. 在解决方案资源管理器中右键单击“引用”，然后选择“添加引用”命令。

   2. 选择“/.NET”并查找“Microsoft.VisualStudio.QualityTools.Common.dll”。

   3. 选择 **“确定”**。

4. 将以下 `using` 语句添加到您的类文件中：

   ```csharp
   using Microsoft.VisualStudio.TestTools.Common;
   using Microsoft.VisualStudio.TestTools.Execution;
   using System.Linq;
   using System.Text;
   using System.Xml;
   using System;
   ```

5. 将 <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectorTypeUriAttribute> 添加到诊断数据适配器的类中以将它标识为诊断数据适配器，用诊断数据适配器的相应信息来替换“公司”、“产品”和“版本”：

   ```csharp
   [DataCollectorTypeUri("datacollector://Company/Product/Version")]
   ```

6. 将 <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectorFriendlyNameAttribute> 特性添加到类中，用您的诊断数据适配器的相应信息来替换参数：

   ```csharp
   [DataCollectorFriendlyName("Collect Log Files", false)]
   ```

    此友好名称将显示在测试设置活动中。

   > [!NOTE]
   > 还可以添加 <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectorConfigurationEditorAttribute> 以指定用于此数据适配器的自定义配置编辑器的 `Type`，并可以选择指定要用于该编辑器的帮助文件。
   >
   > 还可以应用 <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectorEnabledByDefaultAttribute> 指定应始终启用该编辑器。

7. 您的诊断数据适配器类必须从 <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollector> 类继承，如下所示：

   ```csharp
   public class MyDiagnosticDataAdapter : DataCollector
   ```

8. 添加局部变量，如下所示：

   ```csharp
   private DataCollectionEvents dataEvents;
   private DataCollectionLogger dataLogger;
   private DataCollectionSink dataSink;
   private XmlElement configurationSettings;
   ```

9. 添加 <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollector.Initialize*> 方法和“Dispose”方法。 在 `Initialize` 方法中，可按如下所示初始化数据接收器、测试设置中的任何配置数据，以及注册要使用的事件处理程序：

    ```csharp
    public override void Initialize(
        XmlElement configurationElement,
        DataCollectionEvents events,
        DataCollectionSink sink,
        DataCollectionLogger logger,
        DataCollectionEnvironmentContext environmentContext)
    {
           dataEvents = events;  // The test events
           dataLogger = logger;  // The error and warning log
           dataSink = sink;      // Saves collected data
           // Configuration from the test settings
           configurationSettings = configurationElement;

           // Register common events for the data collector
           // Not all of the events are used in this class
        dataEvents.SessionStart +=
            new EventHandler<SessionStartEventArgs>(OnSessionStart);
        dataEvents.SessionEnd +=
            new EventHandler<SessionEndEventArgs>(OnSessionEnd);
        dataEvents.TestCaseStart +=
            new EventHandler<TestCaseStartEventArgs>(OnTestCaseStart);
        dataEvents.TestCaseEnd +=
            new EventHandler<TestCaseEndEventArgs>(OnTestCaseEnd);
    }

    public override void Dispose(bool disposing)
    {
        if (disposing)
        {
            // Unregister the registered events
            dataEvents.SessionStart -=
                new EventHandler<SessionStartEventArgs>(OnSessionStart);
            dataEvents.SessionEnd -=
                new EventHandler<SessionEndEventArgs>(OnSessionEnd);
            dataEvents.TestCaseStart -=
                new EventHandler<TestCaseStartEventArgs>(OnTestCaseStart);
            dataEvents.TestCaseEnd -=
                new EventHandler<TestCaseEndEventArgs>(OnTestCaseEnd);
        }
    }
    ```

10. 使用下面的事件处理程序代码和私有方法收集在测试期间生成的日志文件：

    ```csharp
    public void OnTestCaseEnd(sender, TestCaseEndEventArgs e)
    {
        // Get any files to be collected that are
        // configured in your test settings
        List<string> files = getFilesToCollect();

        // For each of the files, send the file to the data sink
        // which will attach it to the test results or to a bug
        foreach (string file in files)
        {
            dataSink.SendFileAsync(e.Context, file, false);
        }
    }

    // A private method that returns the file names
    private List<string> getFilesToCollect()
    {
        // Get a namespace manager with our namespace
        XmlNamespaceManager nsmgr =
            new XmlNamespaceManager(
                configurationSettings.OwnerDocument.NameTable);
        nsmgr.AddNamespace("ns",
            "http://MyCompany/schemas/MyDataCollector/1.0");

        // Find all of the "File" elements under our configuration
        XmlNodeList files =
            configurationSettings.SelectNodes(
                "//ns:MyDataCollector/ns:File");

        // Build the list of files to collect from the
        // "FullPath" attributes of the "File" nodes.
        List<string> result = new List<string>();
        foreach (XmlNode fileNode in files)
        {
            XmlAttribute pathAttribute =
                fileNode.Attributes["FullPath"];
            if (pathAttribute != null &&
                !String.IsNullOrEmpty(pathAttribute.Value))
            {
                result.Add(pathAttribute.Value);
            }
        }

        return result;
    }
    ```

     可以将这些文件附加到测试结果。 如果根据这些测试结果创建 Bug，或者在使用[!INCLUDE[mtrlong](../test/includes/mtrlong_md.md)]时，这些文件也会附加到 Bug。

     如果您要使用自己的编辑器来收集要在测试设置中使用的数据，请参见[如何：为诊断数据适配器创建自定义数据编辑器](../test/quickstart-create-a-load-test-project.md)。

11. 要在测试完成时根据用户在测试设置中所做配置收集日志文件，则必须创建一个 App.config 文件并将其添加至解决方案。 此文件具有以下格式，并且必须包含供诊断数据适配器进行识别的 URI。 将“Company/ProductName/Version”替换为实际值。

    > [!NOTE]
    > 如果不需要为诊断数据适配器配置任何信息，则无需创建配置文件。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <configSections>
        <section name="DataCollectorConfiguration" type="Microsoft.VisualStudio.TestTools.Execution.DataCollectorConfigurationSection, Microsoft.VisualStudio.QualityTools.ExecutionCommon, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a "/>
      </configSections>
      <DataCollectorConfiguration xmlns="http://microsoft.com/schemas/VisualStudio/TeamTest/2010">
        <DataCollector typeUri="datacollector://MyCompany/MyProduct/1.0">
          <DefaultConfiguration>
            <!-- Your default config settings -->
            <Binaries>
              <Binary FullPath="C:\Example\Example.dll"/>
              <Binary FullPath="\\Server2\Example2.dll"/>
            </Binaries>
            <Symbols>
              <Symbol FullPath="\\ExampleServer\ExampleSymbol.pdb"/>
            </Symbols>
          </DefaultConfiguration>
        </DataCollector>
      </DataCollectorConfiguration>
    </configuration>
    ```

    > [!NOTE]
    > 默认配置元素可以包含您需要的任何数据。 如果用户未在测试设置中配置诊断数据适配器，则在执行诊断数据适配器时将向其传递默认数据。 由于您添加到 `<DefaultConfigurations>` 部分的 XML 不可能属于已声明架构的一部分，因此可以忽略它生成的任何 XML 错误。
    >
    > 在基于安装目录的以下路径中，还存在其他配置文件示例：*Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies\DataCollectors*。

     有关如何在运行测试时配置测试设置以使用环境的详细信息，请参阅[在手动测试中收集诊断数据 (Azure Test Plans)](/azure/devops/test/mtm/collect-more-diagnostic-data-in-manual-tests?view=vsts)。

     有关安装配置文件的更多信息，请参见[如何：安装自定义诊断数据适配器](../test/quickstart-create-a-load-test-project.md)

12. 生成解决方案以创建诊断数据适配器程序集。

13. 有关安装自定义编辑器的信息，请参见[如何：安装自定义诊断数据适配器](../test/quickstart-create-a-load-test-project.md)。

14. 有关如何在运行测试时配置测试设置以使用环境的详细信息，请参阅[在手动测试中收集诊断数据 (Azure Test Plans)](/azure/devops/test/mtm/collect-more-diagnostic-data-in-manual-tests?view=vsts)。

15. 若要选择诊断数据适配器，必须先选择现有的测试设置，或从 Microsoft 测试管理器或 Visual Studio 中创建一个新测试设置。 该适配器将显示在测试设置的“数据和诊断”选项卡上，并具有你指派给该类的友好名称。

16. 将这些测试设置设置为活动状态。 有关测试设置的详细信息，请参阅[使用测试设置收集诊断信息](../test/collect-diagnostic-information-using-test-settings.md)。

17. 使用选择了你的诊断数据适配器的测试设置运行测试。

    您指定的数据文件将被附加到测试结果中。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectorConfigurationEditorAttribute>
- <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionEvents>
- <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollector>
- <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectionSink>
- <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectorTypeUriAttribute>
- <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectorFriendlyNameAttribute>
- <xref:Microsoft.VisualStudio.TestTools.Execution.DataCollectorEnabledByDefaultAttribute>
- [使用测试设置收集诊断信息](../test/collect-diagnostic-information-using-test-settings.md)
- [在手动测试中收集诊断数据 (Azure Test Plans)](/azure/devops/test/mtm/collect-more-diagnostic-data-in-manual-tests?view=vsts)
- [在测试时收集诊断数据 (Azure Test Plans)](/azure/devops/test/collect-diagnostic-data?view=vsts)
- [如何：为诊断数据适配器创建自定义数据编辑器](../test/quickstart-create-a-load-test-project.md)