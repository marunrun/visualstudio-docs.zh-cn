---
title: VSTO 外接程序的注册表项
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- LoadBehavior entry
- add-ins [Office development in Visual Studio], registry entries
- registry keys [Office development in Visual Studio]
- application-level add-ins [Office development in Visual Studio], registry entries
- registry entries [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b02b50c42692ec2fd455358df5157e0b8481562b
ms.sourcegitcommit: b32fbbcbc43910b0ed7ce79aa9a22f2ed36ab57e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2020
ms.locfileid: "79416518"
---
# <a name="registry-entries-for-vsto-add-ins"></a>VSTO 外接程序的注册表项
  部署使用 Visual Studio 创建的 VSTO 外接程序时，必须创建一组特定的注册表项。 这些注册表项可提供一些信息，使 Microsoft Office 应用程序能够发现和加载 VSTO 外接程序。

 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

 生成项目时，Visual Studio 在开发计算机上创建这些注册表项，以便可以轻松运行和调试 VSTO 外接程序。 如果使用 ClickOnce 部署 VSTO 外接程序，注册表项将自动在最终用户计算机上创建。 如果使用 Windows 安装程序部署 VSTO 外接程序，则必须配置安装程序有限版项目才能在最终用户计算机上创建注册表项。

 有关如何在 VSTO 外接程序加载过程中使用注册表项的详细信息，请参阅 [Architecture of VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md)。

> [!NOTE]
> 在本主题中，文本 *外接程序 ID* 表示 VSTO 外接程序的唯一 ID。 默认情况下，该 ID 是 VSTO 外接程序程序集的名称。

## <a name="register-vsto-add-ins-for-the-current-user-vs-all-users"></a>注册当前用户的 VSTO 加载项与所有用户
 安装 VSTO 外接程序后，可以按两种方式注册：

- 仅适用于当前用户（也就是说，它仅在安装 VSTO 外接程序时登录到计算机的用户可用）。 在这种情况下，注册表项在**HKEY_CURRENT_USER**下创建。

- 对于所有用户（即，登录到计算机的任何用户都可以使用 VSTO 外接程序）。 在这种情况下，注册表项在**HKEY_LOCAL_MACHINE**下创建。

  使用 Visual Studio 创建的所有 VSTO 外接程序均可针对当前用户注册。 但是，仅在特定场景下才可针对所有用户注册 VSTO 外接程序。 这些场景取决于计算机上 Microsoft Office 的版本和 VSTO 外接程序的部署方式。

### <a name="deployment-type"></a>部署类型
 如果使用 ClickOnce 部署 VSTO 外接程序，则仅可针对当前用户注册 VSTO 外接程序。 这是因为 ClickOnce 仅支持**在 HKEY_CURRENT_USER**下创建密钥。 如果想要向计算机上的所有用户注册 VSTO 外接程序，则必须使用 Windows Installer 部署 VSTO 外接程序。 有关这些部署类型的详细信息，请参阅使用[ClickOnce 部署 Office 解决方案](../vsto/deploying-an-office-solution-by-using-clickonce.md)，并使用[Windows 安装程序部署 Office 解决方案](../vsto/deploying-a-vsto-solution-by-using-windows-installer.md)。

## <a name="registry-entries"></a>注册表项
 所需的 VSTO 外接程序注册表项位于以下注册表项下，*其中 Root* **是HKEY_CURRENT_USER**或**HKEY_LOCAL_MACHINE，** 具体取决于安装是针对当前用户还是所有用户。

|办公室应用程序|配置路径|
|------------------|------------------|
|Visio|*根*[软件]\\微软*Visio*_Addins\\*外接程序 ID*|
|所有其他|*根*[软件]微软\\ *_Office Office 应用程序名称*\\\Addins*外接程序 ID*|

> [!NOTE]
> 如果安装程序的目标是 64 位 Windows 上的所有用户，则建议它包括两个注册表项，一个在 HKEY_LOCAL_MACHINE_Software_Microsoft 下，另一个在\\HKEY_LOCAL_MACHINE_软件**WOW6432Node**_Microsoft 配置单元下。 这是因为用户可以在计算机上使用 32 位或 64 位版本的 Office。
>
>如果安装程序的目标是当前用户，则无需安装到 WOW6432Node，因为HKEY_CURRENT_USER\软件路径是共享的。
>
>有关详细信息，请参阅[注册表中的 32 位和 64 位应用程序数据](/windows/win32/sysinfo/32-bit-and-64-bit-application-data-in-the-registry)

 下表列出了此注册表项下的条目。

|条目|类型|值|
|-----------|----------|-----------|
|**说明**|REG_SZ|必需。 VSTO 外接程序的简短说明。<br /><br /> 当用户在 Microsoft Office 应用程序的 **“选项”** 对话框的 **“外接程序”** 窗格中选择 VSTO 外接程序时，将会显示此说明。|
|**友好名称**|REG_SZ|必需。 Microsoft Office 应用程序中的 **“COM 外接程序”** 对话框中显示的 VSTO 外接程序的描述性名称。 默认值为 VSTO 外接程序 ID。|
|**LoadBehavior**|REG_DWORD|必需。 一个值，用于指定应用程序在何时尝试加载 VSTO 外接程序以及 VSTO 外接程序的当前状态（已加载或卸载）。<br /><br /> 默认情况下，此项设置为 3，指定在启动时加载 VSTO 外接程序。 有关详细信息，请参阅[Load行为值](#LoadBehavior)。 **注：** 如果用户禁用 VSTO 外接程序，则该操作将修改**HKEY_CURRENT_USER**注册表配置单元中的**LoadAction**值。 对于每个用户，HKEY_CURRENT_USER配置单元中的**LoadBehavior**值将覆盖**HKEY_LOCAL_MACHINE**配置单元中定义的默认**LoadBehavior。**|
|**清单**|REG_SZ|必需。 VSTO 外接程序部署清单的完整路径。 该路径可以是本地计算机上的某个位置，也可以是网络共享 (UNC) 或 Web 服务器 (HTTP)。<br /><br /> 如果使用 Windows Installer 部署解决方案，则必须向 **清单** 路径添加前缀 **file:///** 。 还必须将&#124;**vstolocal（** 即管道字符 **&#124;** 后跟**vstolocal）** 的字符串追加到此路径的末尾。 这可确保从安装文件夹，而非 ClickOnce 缓存加载你的解决方案。 有关详细信息，请参阅使用[Windows 安装程序部署 Office 解决方案](../vsto/deploying-a-vsto-solution-by-using-windows-installer.md)。 **注：** 在开发计算机上构建 VSTO 外接程序时，Visual Studio 会自动将 **&#124;vstolocal**字符串追加到此注册表项中。|

### <a name="registry-entries-for-outlook-form-regions"></a><a name="OutlookEntries"></a>Outlook 窗体区域的注册表项
 如果在 Outlook 的 VSTO 外接程序中创建自定义窗体区域，则会使用其他注册表项在 Outlook 中注册该窗体区域。 这些项是在针对窗体区域支持的每个邮件类别的不同注册表项下创建的。 这些注册表项位于以下位置，*根*位于**HKEY_CURRENT_USER**或**HKEY_LOCAL_MACHINE。**

 *根*[软件]微软\Office\Outlook\Form\\区域*消息类*

 与所有 VSTO 外接程序共享的其他注册表项类似，生成项目时，Visual Studio 会在开发计算机上创建窗体区域注册表项。 如果使用 ClickOnce 部署 VSTO 外接程序，注册表项将自动在最终用户计算机上创建。 如果使用 Windows 安装程序部署 VSTO 外接程序，则必须配置安装程序有限版项目才能在最终用户计算机上创建注册表项。

 有关窗体区域注册表项的详细信息，请参阅[在自定义窗体中指定窗体区域的位置](/office/vba/outlook/Concepts/Creating-Form-Regions/specify-the-location-of-a-form-region-in-a-custom-form)。 有关 Outlook 窗体区域的详细信息，请参阅[创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)。

## <a name="loadbehavior-values"></a><a name="LoadBehavior"></a>加载行为值
 *Root*_Software_Microsoft_Office\\*应用程序名称*"加载\\项 *"* 下的**LoadBehavior**条目包含指定 VSTO 外接程序的运行时行为的值的位形组合。 最低顺序位（值 0 和 1）指示 VSTO 外接程序当前是已卸载还是已加载。 其他位指示应用程序何时尝试加载 VSTO 外接程序。

 通常，当在最终用户计算机上安装 VSTO 外接程序时 **，LoadBehavior**条目旨在设置为 0、3 或 16（十进制）。 默认情况下，在生成或发布 VSTO 外接程序时，Visual Studio 会将外接程序的 **LoadBehavior** 条目设置为 3。

 下表列出了 **LoadBehavior** 条目的所有可能的值。 此表中的一些描述涉及手动或以编程方式加载 VSTO 外接程序。 若要手动加载 VSTO 外接程序，在应用程序的 **“COM 外接程序”** 对话框中选择 VSTO 外接程序旁的复选框。 若要以编程方式加载 VSTO 外接程序，请将表示 VSTO 外接程序的 <xref:Microsoft.Office.Core.COMAddIn.Connect%2A> 对象的 <xref:Microsoft.Office.Core.COMAddIn> 属性设置为 **true**。

|值（采用十进制）|VSTO 外接程序状态|VSTO 外接程序加载行为|说明|
|--------------------------|-------------------------|--------------------------------|-----------------|
|0|已卸载|不自动加载|应用程序从不尝试自动加载 VSTO 外接程序。 用户可尝试手动加载 VSTO 外接程序，也可以编程方式加载 VSTO 外接程序。<br /><br /> 如果 VSTO 外接程序加载成功，则 **LoadBehavior** 值保持为 0，但将更新 **“COM 外接程序”** 对话框中的 VSTO 外接程序状态，以指示已加载 VSTO 外接程序。|
|1|已加载|不自动加载|应用程序从不尝试自动加载 VSTO 外接程序。 用户可尝试手动加载 VSTO 外接程序，也可以编程方式加载 VSTO 外接程序。<br /><br /> 尽管**COM 外接程序**对话框指示在应用程序启动后加载 VSTO 外接程序，但在手动或以编程方式加载之前不会加载 VSTO 外接程序。<br /><br /> 如果应用程序成功加载 VSTO 外接程序，则 **LoadBehavior** 值更改为 0，并在应用程序关闭后仍然保持为 0。|
|2|已卸载|在启动时加载|应用程序不会尝试自动加载 VSTO 外接程序。 用户可尝试手动加载 VSTO 外接程序，也可以编程方式加载 VSTO 外接程序。<br /><br /> 如果应用程序成功加载 VSTO 外接程序，则 **LoadBehavior** 值更改为 3，并在应用程序关闭后仍然保持为 3。|
|3|已加载|在启动时加载|应用程序在启动时尝试加载 VSTO 外接程序。 在 Visual Studio 中生成或发布 VSTO 外接程序时，这是默认值。<br /><br /> 如果应用程序成功加载 VSTO 外接程序，则 **LoadBehavior** 值保持为 3。 如果加载 VSTO 外接程序时出错，则 **LoadBehavior** 值更改为 2，并在应用程序关闭后仍然保持为 2。|
|8|已卸载|按需加载|应用程序不会尝试自动加载 VSTO 外接程序。 用户可尝试手动加载 VSTO 外接程序，也可以编程方式加载 VSTO 外接程序。<br /><br /> 如果应用程序成功加载 VSTO 外接程序，则 **LoadBehavior** 值更改为 9。|
|9|已加载|按需加载|VSTO 外接程序将仅在应用程序需要它时加载，例如，用户单击使用 VSTO 外接程序中的功能的 UI 元素（例如，功能区中的自定义按钮）时。<br /><br /> 如果应用程序成功加载 VSTO 外接程序，则 **LoadBehavior** 值保持为 9，但将更新 **“COM 外接程序”** 对话框中的外接程序状态，以指示当前已加载 VSTO 外接程序。 如果加载 VSTO 外接程序时出错，则 **LoadBehavior** 值更改为 8。|
|16|已加载|第一次时加载，然后按需加载|如果想要按需加载 VSTO 外接程序，请设置此值。 用户第一次运行应用程序时，应用程序将加载 VSTO 外接程序。 用户下一次运行应用程序时，应用程序将加载 VSTO 外接程序定义的任何 UI 元素，但不会加载 VSTO 外接程序，直到用户单击与 VSTO 外接程序关联的 UI 元素。<br /><br /> 应用程序第一次成功加载 VSTO 外接程序时， **LoadBehavior** 值在加载 VSTO 外接程序后保持为 16。 应用程序关闭后， **LoadBehavior** 值更改为 9。|

## <a name="see-also"></a>另请参阅
- [可视化工作室中的 Office 解决方案架构](../vsto/architecture-of-office-solutions-in-visual-studio.md)
- [Architecture of VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md)
- [构建 Office 解决方案](../vsto/building-office-solutions.md)
- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)
 