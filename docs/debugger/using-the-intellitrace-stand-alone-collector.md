---
title: 使用 IntelliTrace 独立收集器 |Microsoft Docs
ms.date: 07/30/2019
ms.topic: conceptual
f1_keywords:
- vs.historicaldebug.collectdataoutsideVS
helpviewer_keywords:
- IntelliTrace, debugging applications in production
ms.assetid: 1bde9807-8219-4a2a-a440-ac5ee5178159
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a5349c08497bc52c32a4ffed30b74f2d3bd71e4e
ms.sourcegitcommit: 257fc60eb01fefafa9185fca28727ded81b8bca9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72911313"
---
# <a name="using-the-intellitrace-stand-alone-collector-c-visual-basic"></a>使用 IntelliTrace 独立收集器（C#、Visual Basic）

**IntelliTrace 独立收集器** 可让你收集生产服务器或其他环境中应用的 IntelliTrace 诊断数据，而无需在目标计算机上安装 Visual Studio 或更改目标系统环境。 IntelliTrace 独立收集器可用于 Web、SharePoint、WPF 和 Windows 窗体应用中。 数据收集完毕后，只需删除收集器以进行卸载。

 在操作中观察 IntelliTrace： [收集并分析生成的 IntelliTrace 数据以便进行调试（第 9 频道视频）](https://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Collecting-and-analyzing-data-in-production)

> [!NOTE]
> 通过在 **跟踪** 模式下使用 **Microsoft 监视代理** ，你还可以收集远程计算机上运行的 Web 及 SharePoint 应用的相同 IntelliTrace 数据。
>
> 可通过在 **监视** 模式下运行代理来收集 IntelliTrace 数据中与性能相关的事件。 与**跟踪** 模式或 **IntelliTrace 独立收集器** 相比， **IntelliIntelliTrace 独立收集器 stand-alone collector**模式对性能的影响更小。 安装时，Microsoft 监视代理确实会改变目标系统的环境。 请参阅[使用 Microsoft Monitoring Agent](../debugger/using-the-microsoft-monitoring-agent.md)。
> IntelliTrace 独立收集器不支持处理快照。

 **惠?**

- .NET Framework 3.5 或更高版本

- 开发计算机或其他计算机上的 Visual Studio Enterprise（但不是 Professional 或 Community 版本），可用来打开 .iTrace 文件

  > [!NOTE]
  > 务必保存符号 (.pdb) 文件。 要调试 IntelliTrace 并单步调试代码，你必须有相匹配的源文件和符号文件。 请参阅[部署后诊断问题](../debugger/diagnose-problems-after-deployment.md)。

  **常见问题解答**

- [哪些应用上可使用该收集器？](#WhatApps)

- [如何开始？](#GetStarted)

- [如何在应用速度不减的前提下获取最多的数据？](#Minimizing)

- [可从哪些其他渠道获取 IntelliTrace 数据？](#WhereElse)

## <a name="WhatApps"></a> 哪些应用上可使用该收集器？

- Internet Information Services （IIS）版本7.0、7.5、8.0、12.0 和16.0 上托管的 ASP.NET Web 应用

- SharePoint 2010 及 SharePoint 2013 应用程序

- Windows Presentation Foundation (WPF) 和 Windows 窗体应用。

## <a name="GetStarted"></a> 如何开始？

1. [安装收集器](#BKMK_Install_the_IntelliTrace_Stand_Alone_Collector)

2. [设置回收器目录的权限](#ConfigurePermissionsRunningCollector)

3. [安装 IntelliTrace PowerShell cmdlet 收集 Web 应用程序或 SharePoint 应用程序的数据](#BKMK_Set_up_the_IntelliTrace_PowerShell_commandlets)

4. [设置 .iTrace 文件目录的权限](#BKMK_Create_and_Configure_a_Log_File_Directory)

5. [从 Web 应用程序或 SharePoint 应用程序中收集数据](#BKMK_Collect_Data_from_IIS_Application_Pools)

     或

     [收集托管应用中的数据](#BKMK_Collect_Data_from_Executables)

6. [在 Visual Studio Enterprise 中打开 .iTrace 文件](#BKMK_View_IntelliTrace_Log_Files)

## <a name="BKMK_Install_the_IntelliTrace_Stand_Alone_Collector"></a> 安装收集器

1. 在应用服务器上创建收集器目录，如： C:\IntelliTraceCollector

2. 从[Microsoft 下载中心](https://visualstudio.microsoft.com/downloads/#intellitrace-standalone-collector-for-visual-studio-2019)、 [My.visualstudio.com](https://my.visualstudio.com/Downloads?q=intellitrace%20standalone%20collector%20visual%20studio%202017)或 Visual Studio 2013 Update 3 安装文件夹中获取收集器。 [IntelliTrace Collector for Visual Studio 2013 Update 4](https://www.microsoft.com/download/details.aspx?id=44909)：

   - **Microsoft 下载中心**或**my.visualstudio.com**：

     1. 选择 **IntelliTraceCollector.exe**旁的“下载”。

     2. 将 IntelliTraceCollector.exe 保存到收集器目录，如： **C:\IntelliTraceCollector**

     3. 运行 IntelliTraceCollector.exe。 此程序会提取 IntelliTraceCollection.cab 文件。

        \- 或 -

   - **Visual Studio 安装文件夹**：

     1. 从安装收集器的文件夹中复制 Intellitracecollection.cab，例如：

          **..\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\CommonExtensions\Microsoft\IntelliTrace**

          或者，对于以前版本的 Visual Studio：

          **..\Microsoft Visual Studio 12.0\Common7\IDE\CommonExtensions\Microsoft\IntelliTrace\12.0.0**

     2. 将 IntelliTraceCollection.cab 放在收集器目录中，如： **C:\IntelliTraceCollector**

3. 扩展 IntelliTraceCollection.cab：

   1. 以管理员身份打开应用服务器上的命令提示符窗口。

   2. 浏览到收集器目录，如： **C:\IntelliTraceCollector**

   3. 使用 **expand** 命令来扩展 IntelliTraceCollection.cab，加上最后的句点（“.”）：

        `expand  /f:* IntelliTraceCollection.cab .`

       > [!NOTE]
       > 该句点（“.”）保留包含本地化收集计划的子文件夹。

## <a name="ConfigurePermissionsRunningCollector"></a> 设置回收器目录的权限

1. 以管理员身份打开应用服务器上的命令提示符窗口。

2. 使用 Windows **icacls** 命令授予服务器管理员访问收集器目录的完全权限。 例如:

     `icacls "C:\IntelliTraceCollector" /grant "` *\<Domain\AdministratorID>* `":F`

3. 要收集 Web 应用或 SharePoint 应用程序中的数据，请：

    1. 向将运行 IntelliTrace PowerShell cmdlet 的人员授予访问收集器目录的完全权限。

         例如:

         `icacls "C:\IntelliTraceCollector" /grant "` *\<Domain\UserID>* `":F`

    2. 授予 Web 应用或 SharePoint 应用程序的应用程序池对收集器目录的读取和执行权限。

         例如:

        - 对于“DefaultAppPool” 应用程序池中的 Web 应用：

             `icacls "C:\IntelliTraceCollector" /grant "IIS APPPOOL\DefaultAppPool":RX`

        - 对于“SharePoint - 80” 应用程序池中的一个 SharePoint 应用程序：

             `icacls "C:\IntelliTraceCollector" /grant "IIS APPPOOL\SharePoint - 80":RX`

## <a name="BKMK_Set_up_the_IntelliTrace_PowerShell_commandlets"></a> 安装 IntelliTrace PowerShell cmdlet 收集 Web 应用程序或 SharePoint 应用程序的数据

1. 确保应用服务器上的 PowerShell 已启用。 可在大多数 Windows Server 版本上将此功能添加到“服务器管理器” 管理工具中。

     ![使用服务器管理器添加 PowerShell](../debugger/media/intellitrace_servermanager_addpowershell.png "INTELLITRACE_ServerManager_AddPowerShell")

2. 安装 IntelliTrace PowerShell cmdlet。

    1. 以管理员身份打开 PowerShell 命令窗口。

        1. 依次选择“开始”、“所有程序”、“附件”、“Windows PowerShell”。

        2. 选择下列步骤之一：

            - 在 64 位操作系统上，打开“Windows PowerShell”快捷菜单。 选择 **“以管理员身份运行”** 。

            - 在 32 位操作系统上，打开“Windows PowerShell (x86)”快捷菜单。 选择 **“以管理员身份运行”** 。

    2. 在 PowerShell 命令窗口，使用 **导入模块** 命令导入 **Microsoft.VisualStudio.IntelliTrace.PowerShell.dll**。

         例如:

         `Import-Module "C:\IntelliTraceCollector\Microsoft.VisualStudio.IntelliTrace.PowerShell.dll"`

## <a name="BKMK_Create_and_Configure_a_Log_File_Directory"></a> 设置 .iTrace 文件目录的权限

1. 在应用服务器上创建 .iTrace 文件目录，如：C:\IntelliTraceLogFiles

   > [!NOTE]
   > - 为避免应用速度变慢，请选择本地高速磁盘上不常用的位置。
   >   - 你可以将 .iTrace 文件和收集器文件放在同一位置。 但是，如果你有一个 Web 应用或 SharePoint 应用程序，务必确保该位置与托管应用程序的目录位置不同。
   >
   > [!IMPORTANT]
   > - .iTrace 文件目录中只可包含那些与收集器兼容的标识。 .iTrace 文件中可能包含敏感信息，如用户、数据库、其他源位置及连接字符串数据，因为 IntelliTrace 可记录进入方法参数或作为返回值的任何数据。
   >   - 确保那些可打开 .iTrace 文件的人员拥有查看敏感数据的权限。 共享 .iTrace 文件时要格外小心。 如果其他人员必须访问，请将文件复制到安全的共享位置。

2. 针对 Web 应用或 SharePoint 应用程序，授予其应用程序池对 .iTrace 文件目录的完全权限。 你可以使用 Windows **icacls** 命令或使用 Windows 资源管理器（或文件资源管理器）。

    例如:

   - 要使用 Windows **icacls** 命令设置权限，请：

     - 对于“DefaultAppPool” 应用程序池中的 Web 应用：

        `icacls "C:\IntelliTraceLogFiles" /grant "IIS APPPOOL\DefaultAppPool":F`

     - 对于“SharePoint - 80” 应用程序池中的一个 SharePoint 应用程序：

        `icacls "C:\IntelliTraceLogFiles" /grant "IIS APPPOOL\SharePoint - 80":F`

       或

   - 要设置 Windows 资源管理器（或文件资源管理器）的权限，请：

     1. 打开 .iTrace 文件目录的“属性” 。

     2. 在“安全” 选项卡上，选择“编辑”，然后单击“添加”。

     3. 确保“内置安全主体” 出现在“选择此对象类型” 框中。 如果“内置安全主体”未在那里出现，请选择“对象类型”进行添加。

     4. 确保本地计算机出现在“从此处” 框中。 如果本地计算机未在那里出现，请选择“位置”进行更改。

     5. 在“输入要选择的对象名称” 框中，添加 Web 应用或 SharePoint 应用程序的应用程序池。

     6. 选择“检查名称” 来解析名称。 选择 **“确定”** 。

     7. 确保该应用程序池拥有“完全控制”。

## <a name="BKMK_Collect_Data_from_IIS_Application_Pools"></a> 从 Web 应用程序或 SharePoint 应用程序中收集数据

1. 要开始收集数据，首先以管理员身份打开 PowerShell 命令窗口，然后运行此命令：

     `Start-IntelliTraceCollection` `"` *\<ApplicationPool>* `"` *\<PathToCollectionPlan>* *\<FullPathToITraceFileDirectory>*

    > [!IMPORTANT]
    > 运行此命令后，键入“Y” 确认你希望开始收集数据。

     如，要收集 **SharePoint - 80** 应用程序池中 SharePoint 应用程序中的数据，请：

     `Start-IntelliTraceCollection "SharePoint - 80" "C:\IntelliTraceCollector\collection_plan.ASP.NET.default.xml" "C:\IntelliTraceLogFiles"`

    |||
    |-|-|
    |*应用程序池*|应用程序运行的应用程序池名|
    |*收集计划路径*|收集计划路径，配置收集器设置的 .xml 文件。<br /><br /> 你可指定收集器附带的一个计划。 以下计划适合 Web 应用和 SharePoint 应用程序：<br /><br /> -   collection_plan.ASP.NET.default.xml<br />     仅收集 IntelliTrace 事件和 SharePoint 事件，包括异常、数据库调用及 Web 服务器请求。<br />-   collection_plan.ASP.NET.trace.xml<br />     收集 collection_plan.ASP.NET.default.xml 中的函数调用及所有数据。 该计划非常适合进行详细分析，但其可能导致你的应用速度比 collection_plan.ASP.NET.default.xml 更慢。<br /><br /> 为避免应用速度变慢，自定义这些计划或创建自己的计划。 为安全起见，将所有自定义计划放在收集器文件所在的同一安全位置。 请参阅 [创建并自定义 IntelliTrace 收集计划](https://devblogs.microsoft.com/devops/modifying-an-intellitrace-collection-plan-for-the-stand-alone-collector/) 和 [如何在应用速度不减的前提下获取最多的数据？](#Minimizing) **注意：** 默认情况下，.Itrace 文件的最大大小为 100 MB。 .iTrace 文件大小达到该上限时，收集器会删除文件中最早的项以便为更新的项让出空间。 要更改该上限，请修改此收集计划的 `MaximumLogFileSize` 属性。 <br /><br /> *从何处可找到这些收集计划的本地版本？*<br /><br /> 可在收集器子文件夹中找到本地计划。|
    |*跟踪文件目录的完整路径*|跟踪 .iTrace 文件目录的完整路径。 **安全说明：** 提供完整路径，而不是相对路径。|

     收集器连接到应用程序池并开始收集数据。

     *此时可打开 .iTrace 文件吗？* 不可以，数据收集过程中该文件处于锁定状态。

2. 再现此问题。

3. 若要创建 .Itrace 文件的检查点，请使用以下语法：

     `Checkpoint-IntelliTraceCollection` `"` *\<ApplicationPool>* `"`

4. 要检查收集状态，请使用该语法：

     `Get-IntelliTraceCollectionStatus`

5. 要停止收集数据，请使用该语法：

     `Stop-IntelliTraceCollection` `"` *\<ApplicationPool>* `"`

    > [!IMPORTANT]
    > 运行此命令后，键入“Y” 确认你希望停止收集数据。 否则，收集器可能会继续收集数据、iTrace 文件将继续处于锁定状态或文件中可能包含一些无用的数据。

6. [在 Visual Studio Enterprise 中打开 .iTrace 文件](#BKMK_View_IntelliTrace_Log_Files)

## <a name="BKMK_Collect_Data_from_Executables"></a> 收集托管应用中的数据

1. 要同时启动应用并收集数据，请使用该语法：

     *\<FullPathToIntelliTraceCollectorExecutable>* `\IntelliTraceSC.exe launch /cp:` *\<PathToCollectionPlan>* `/f:` *\<FullPathToITraceFileDirectoryAndFileName>* *\<PathToAppExecutableFileAndFileName>*

     如，要收集名为 **MyApp**的应用中的数据，请：

     `C:IntelliTraceCollectorIntelliTraceSC.exe launch /cp:"C:IntelliTraceCollectorcollection_plan.ASP.NET.default.xml" /f:"C:IntelliTraceLogFilesMyApp.itrace" "C:MyAppMyApp.exe"`

    |||
    |-|-|
    |*IntelliTrace 收集器可执行文件完整路径*|收集器可执行文件的完整路径，IntelliTraceSC.exe|
    |*收集计划路径*|收集计划路径，配置收集器设置的 .xml 文件。<br /><br /> 你可指定收集器附带的一个计划。 以下计划适合托管应用：<br /><br /> -   collection_plan.ASP.NET.default.xml<br />     仅收集 IntelliTrace 事件，包括异常、数据库调用及 Web 服务器请求。<br />-   collection_plan.ASP.NET.trace.xml<br />     收集 collection_plan.ASP.NET.default.xml 中的函数调用及所有数据。 该计划非常适合进行详细分析，但其可能导致你的应用速度比 collection_plan.ASP.NET.default.xml 更慢。<br /><br /> 为避免应用速度变慢，自定义这些计划或创建自己的计划。 为安全起见，将所有自定义计划放在收集器文件所在的同一安全位置。 请参阅 [创建并自定义 IntelliTrace 收集计划](https://devblogs.microsoft.com/devops/modifying-an-intellitrace-collection-plan-for-the-stand-alone-collector/) 和 [如何在应用速度不减的前提下获取最多的数据？](#Minimizing) **注意：** 默认情况下，.Itrace 文件的最大大小为 100 MB。 .iTrace 文件大小达到该上限时，收集器会删除文件中最早的项以便为更新的项让出空间。 要更改该上限，请修改此收集计划的 `MaximumLogFileSize` 属性。 <br /><br /> *从何处可找到这些收集计划的本地版本？*<br /><br /> 可在收集器子文件夹中找到本地计划。|
    |*.iTrace文件目录及文件名完整路径*|.iTrace 文件目录及包含 **.itrace** 扩展名的 .iTrace 文件名的完整路径。 **安全说明：** 提供完整路径，而不是相对路径。|
    |*应用可执行文件及文件名路径*|托管应用的路径及文件名|

2. 通过退出应用来停止数据收集。

3. [在 Visual Studio Enterprise 中打开 .iTrace 文件](#BKMK_View_IntelliTrace_Log_Files)

## <a name="BKMK_View_IntelliTrace_Log_Files"></a> 在 Visual Studio Enterprise 中打开 .iTrace 文件

> [!NOTE]
> 要调试 IntelliTrace 并单步调试代码，你必须有相匹配的源文件和符号文件。 请参阅[部署后诊断问题](../debugger/diagnose-problems-after-deployment.md)。

1. 将 .iTrace 文件移到或复制到装有 Visual Studio Enterprise（但不是 Professional 或 Community 版）的计算机中。

2. 双击 Visual Studio 外的 .iTrace 文件或从 Visual Studio 内打开文件。

     Visual Studio 显示“IntelliTrace 摘要” 页面。 你可以查看大多数部分中的事件或其他项，请选择一项并开始使用 IntelliTrace 调试事件发生地点及其时间点。 请参阅[使用保存的 IntelliTrace 数据](../debugger/using-saved-intellitrace-data.md)。

    > [!NOTE]
    > 要调试 IntelliTrace 并单步调试代码，你的开发计算机上必须有相匹配的源文件和符号文件。 请参阅[部署后诊断问题](../debugger/diagnose-problems-after-deployment.md)。

## <a name="Minimizing"></a> 如何在应用速度不减的前提下获取最多的数据？
 IntelliTrace 可收集大量数据，因此对应用性能的影响取决于 IntelliTrace 收集的数据及其分析的代码类型。 请参阅 [优化生产服务器上的 IntelliTrace 收集](https://devblogs.microsoft.com/devops/optimizing-intellitrace-collection-on-production-server/)。

 以下是在应用速度不减的前提下获取最多的数据的一些方法：

- 只在认为存在问题或可以再现该问题时运行收集器。

   开始收集，再现该问题，然后停止收集。 在 Visual Studio Enterprise 中打开 .iTrace 文件并检查相关数据。 请参阅 [在 Visual Studio Enterprise 中打开 .iTrace 文件](#BKMK_View_IntelliTrace_Log_Files)模式对性能的影响更小。

- 针对 Web 应用和 SharePoint 应用程序，收集器会记录共享指定应用程序池的各应用的数据。 虽然你只能在一个收集计划中指定一个单应用的模块，但这可能使任何共享同一应用程序池的应用速度变慢。

   要防止收集器使应用速度变慢，请将各应用托管在各自的应用程序池中。

- 检查 IntelliTrace 要收集数据的收集计划中的事件。 编辑收集计划以禁用无关或不感兴趣的事件。

   要禁用事件，请将 `enabled` 元素的 `<DiagnosticEventSpecification>` 属性设为 `false`：

   `<DiagnosticEventSpecification enabled="false">`

   如果 `enabled` 属性不存在，则该事件已启用。

   *这如何提高性能？*

  - 可通过禁用与应用无关的事件来减少启动时间。 如，禁用未使用 Windows 工作流的应用的 Windows 工作流事件。

  - 可以通过禁用访问注册表但不显示注册表设置问题的应用的注册表事件，提高启动和运行时性能。

- 检查 IntelliTrace 要收集数据的收集计划中的模块。 编辑收集计划，只加入你感兴趣的模块：

  1. 打开收集计划。 查找 `<ModuleList>` 元素。

  2. 在 `<ModuleList>`中，将 `isExclusionList` 属性设为 `false`。

  3. 使用 `<Name>` 元素为各模块指定以下一项：文件名、字符串值（以便加入任何名称中包含该字符串的模块）或公钥。

     如，要只从 Fabrikam Fiber Web 应用的 Web 主模块中收集数据，请创建一个与此类似的列表：

  ```xml
  <ModuleList isExclusionList="false">
     <Name>FabrikamFiber.Web.dll</Name>
  </ModuleList>
  ```

   要从任何名称中包含“Fabrikam”的模块中收集数据，请创建一个与此类似的列表：

  ```xml
  <ModuleList isExclusionList="false">
     <Name>Fabrikam</Name>
  </ModuleList>
  ```

   要通过指定模块公钥标记从中收集数据，请创建一个与此类似的列表：

  ```xml
  <ModuleList isExclusionList="false">
     <Name>PublicKeyToken:B77A5C561934E089</Name>
     <Name>PublicKeyToken:B03F5F7F11D50A3A</Name>
     <Name>PublicKeyToken:31BF3856AD364E35</Name>
     <Name>PublicKeyToken:89845DCD8080CC91</Name>
     <Name>PublicKeyToken:71E9BCE111E9429C</Name>
  </ModuleList>
  ```

   *这如何提高性能？*

   这可减少应用启动、运行时 IntelliTrace 收集的方法调用信息及其他检测数据的数量。 你可使用该数据来：

  - 收集数据后单步调试代码。

  - 检查函数调用接收及返回的值。

    *为何不排除模块呢？*

    通常情况下，收集计划通过将 `isExclusionList` 属性设为 `true`来排除模块。 然而，排除的模块可能仍然会收集不符合列表标准以及你可能不感兴趣的模块中的数据，如第三方或开源模块。

- *是否存在 IntelliTrace 不会收集的任何数据？*

   是的，为减少对性能的影响，IntelliTrace 只会收集以下数据：方法接收及返回的基元数据类型值以及顶层对象字段中的基元数据类型值。

   如，假定你有一个 `AlterEmployee` 方法签名，其包含一个整数 `id` 和一个 `Employee` 对象 `oldemployee`：

   `public Employee AlterEmployee(int id, Employee oldemployee)`

   `Employee` 类型具有以下属性： `Id`、 `Name`和 `HomeAddress`。 `Employee` 和 `Address` 类型之间存在关联。

   ![员工与地址之间的关系](../debugger/media/employeeaddressrelationship.png "EmployeeAddressRelationship")

   收集器记录 `id`方法返回的 `Employee.Id`、 `Employee.Name` 、 `Employee` 和 `AlterEmployee` 对象的值。 但是，除记录 `Address` 对象是否为空以外，收集器不会记录该对象的其他信息。 收集器也不会记录 `AlterEmployee` 方法中局部变量相关的数据，除非其他方法将这些局部变量用作参数，记录为方法参数。

## <a name="WhereElse"></a> 可从哪些其他渠道获取 IntelliTrace 数据？

可以从 Visual Studio Enterprise 中的 IntelliTrace 调试会话获取 IntelliTrace 数据。 请参阅[IntelliTrace 功能](../debugger/intellitrace-features.md)。

## <a name="where-can-i-get-more-information"></a>在何处可以获取详细信息？
 [使用保存的 IntelliTrace 数据](../debugger/using-saved-intellitrace-data.md)

 [IntelliTrace](../debugger/intellitrace.md)

### <a name="blogs"></a>博客
 [远程使用 IntelliTrace 独立收集器](https://devblogs.microsoft.com/devops/using-the-intellitrace-standalone-collector-remotely/)

 [创建并自定义 IntelliTrace 收集计划](https://devblogs.microsoft.com/devops/modifying-an-intellitrace-collection-plan-for-the-stand-alone-collector/)

 [优化生产服务器上的 IntelliTrace 收集](https://devblogs.microsoft.com/devops/optimizing-intellitrace-collection-on-production-server/)

 [Microsoft DevOps](https://devblogs.microsoft.com/devops/)

### <a name="forums"></a>论坛
 [Visual Studio 调试器](https://social.msdn.microsoft.com/Forums/en-US/home)

### <a name="videos"></a>视频
 [第 9 频道：收集和分析 IntelliTrace 数据](https://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Collecting-and-analyzing-data-in-production)
