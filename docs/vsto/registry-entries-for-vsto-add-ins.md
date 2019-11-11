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
ms.openlocfilehash: a98164488d548a15c07e67b9a02cad2341f7300b
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72985652"
---
# <a name="registry-entries-for-vsto-add-ins"></a>VSTO 外接程序的注册表项
  部署使用 Visual Studio 创建的 VSTO 外接程序时，必须创建一组特定的注册表项。 这些注册表项可提供一些信息，使 Microsoft Office 应用程序能够发现和加载 VSTO 外接程序。

 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

 生成项目时，Visual Studio 在开发计算机上创建这些注册表项，以便可以轻松运行和调试 VSTO 外接程序。 如果使用 ClickOnce 部署 VSTO 外接程序，则将在最终用户计算机上自动创建注册表项。 如果使用 Windows Installer 部署 VSTO 外接程序，则必须将 InstallShield 受限版本项目配置为在最终用户计算机上创建注册表项。

 有关如何在 VSTO 外接程序加载过程中使用注册表项的详细信息，请参阅 [Architecture of VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md)。

> [!NOTE]
> 在本主题中，文本 *外接程序 ID* 表示 VSTO 外接程序的唯一 ID。 默认情况下，该 ID 是 VSTO 外接程序程序集的名称。

## <a name="register-vsto-add-ins-for-the-current-user-vs-all-users"></a>为当前用户和所有用户注册 VSTO 外接程序
 安装 VSTO 外接程序后，可以按两种方式注册：

- 仅适用于当前用户（即，它仅供安装 VSTO 外接程序时登录到计算机的用户使用）。 在这种情况下，将在**HKEY_CURRENT_USER**下创建注册表项。

- 对于所有用户（即，登录到计算机的任何用户都可以使用 VSTO 外接程序）。 在这种情况下，将在**HKEY_LOCAL_MACHINE**下创建注册表项。

  使用 Visual Studio 创建的所有 VSTO 外接程序均可针对当前用户注册。 但是，仅在特定场景下才可针对所有用户注册 VSTO 外接程序。 这些场景取决于计算机上 Microsoft Office 的版本和 VSTO 外接程序的部署方式。

### <a name="microsoft-office-version"></a>Microsoft Office 版本
 Office 应用程序可以加载在**HKEY_LOCAL_MACHINE**或**HKEY_CURRENT_USER**下注册的 VSTO 外接程序。

 若要加载在**HKEY_LOCAL_MACHINE**下注册的 VSTO 外接程序，计算机必须安装更新包976477。 有关详细信息，请参阅 [http://go.microsoft.com/fwlink/?LinkId=184923](https://support.microsoft.com/help/976811/a-2007-office-system-application-does-not-load-an-add-in-that-is-devel)。

### <a name="deployment-type"></a>部署类型
 如果使用 ClickOnce 部署 VSTO 外接程序，则仅可针对当前用户注册 VSTO 外接程序。 这是因为 ClickOnce 仅支持在**HKEY_CURRENT_USER**下创建密钥。 如果想要向计算机上的所有用户注册 VSTO 外接程序，则必须使用 Windows Installer 部署 VSTO 外接程序。 有关这些部署类型的详细信息，请参阅[使用 ClickOnce 部署 office 解决方案](../vsto/deploying-an-office-solution-by-using-clickonce.md)和[使用 Windows Installer 部署 office 解决方案](../vsto/deploying-an-office-solution-by-using-windows-installer.md)。

## <a name="registry-entries"></a>注册表项
 对于除 Visio 外的所有应用程序，所需的 VSTO 外接程序注册表项都位于以下注册表项下，其中的*根*为**HKEY_CURRENT_USER**或**HKEY_LOCAL_MACHINE**。

 **除 Visio 外的所有应用程序**

|Office 版本|配置路径|
|--------------------|------------------------|
|32 位|*根*\Software\Microsoft\Office\\*应用程序名称*\Addins\\*外接程序 ID*|
|64 位|*根*\Software\Wow6432Node\Microsoft\Office\\*应用程序名称*\Addins\\*外接程序 ID*|

 **Visio**

|Office 版本|配置路径|
|--------------------|------------------------|
|32 位|*根*\Software\Microsoft\Visio\Addins\\*外接程序 ID*|
|64 位|*根*\Software\Wow6432Node\Visio\Addins\\*外接程序 ID*|

 下表列出了此注册表项下的条目。

|条目|键入|“值”|
|-----------|----------|-----------|
|**描述**|REG_SZ|必须的。 VSTO 外接程序的简短说明。<br /><br /> 当用户在 Microsoft Office 应用程序的 **“选项”** 对话框的 **“外接程序”** 窗格中选择 VSTO 外接程序时，将会显示此说明。|
|**FriendlyName**|REG_SZ|必须的。 Microsoft Office 应用程序中的 **“COM 外接程序”** 对话框中显示的 VSTO 外接程序的描述性名称。 默认值为 VSTO 外接程序 ID。|
|**LoadBehavior**|REG_DWORD|必须的。 一个值，用于指定应用程序在何时尝试加载 VSTO 外接程序以及 VSTO 外接程序的当前状态（已加载或卸载）。<br /><br /> 默认情况下，此项设置为 3，指定在启动时加载 VSTO 外接程序。 有关详细信息，请参阅[LoadBehavior 值](#LoadBehavior)。 **注意：** 如果用户禁用 VSTO 外接程序，则该操作会修改**HKEY_CURRENT_USER**注册表配置单元中的**LoadBehavior**值。 对于每个用户，HKEY_CURRENT_USER 配置单元中**LoadBehavior**值的值将覆盖**HKEY_LOCAL_MACHINE** hive 中定义的默认**LoadBehavior** 。|
|**清单**|REG_SZ|必须的。 VSTO 外接程序部署清单的完整路径。 该路径可以是本地计算机上的某个位置，也可以是网络共享 (UNC) 或 Web 服务器 (HTTP)。<br /><br /> 如果使用 Windows Installer 部署解决方案，则必须向 **清单** 路径添加前缀 **file:///** 。 还必须将字符串 **&#124;vstolocal** （即，后面跟**vstolocal**的管道字符 **&#124;** ）追加到此路径的末尾。 这可确保从安装文件夹，而非 ClickOnce 缓存加载你的解决方案。 有关详细信息，请参阅[使用 Windows Installer 部署 Office 解决方案](../vsto/deploying-an-office-solution-by-using-windows-installer.md)。 **注意：** 当你在开发计算机上生成 VSTO 外接程序时，Visual Studio 会自动将 **&#124;vstolocal**字符串追加到此注册表项。|

### <a name="OutlookEntries"></a>Outlook 窗体区域的注册表项
 如果在 Outlook 的 VSTO 外接程序中创建自定义窗体区域，则会使用其他注册表项在 Outlook 中注册该窗体区域。 这些项是在针对窗体区域支持的每个邮件类别的不同注册表项下创建的。 这些注册表项位于以下位置，其中的*根*为**HKEY_CURRENT_USER**或**HKEY_LOCAL_MACHINE**。

 *根*\Software\Microsoft\Office\Outlook\FormRegions\\*message 类*

 与所有 VSTO 外接程序共享的其他注册表项类似，生成项目时，Visual Studio 会在开发计算机上创建窗体区域注册表项。 如果使用 ClickOnce 部署 VSTO 外接程序，则将在最终用户计算机上自动创建注册表项。 如果使用 Windows Installer 部署 VSTO 外接程序，则必须将 InstallShield 受限版本项目配置为在最终用户计算机上创建注册表项。

 有关窗体区域注册表项的详细信息，请参阅[在自定义窗体中指定窗体区域的位置](/office/vba/outlook/Concepts/Creating-Form-Regions/specify-the-location-of-a-form-region-in-a-custom-form)。 有关 Outlook 窗体区域的详细信息，请参阅[创建 outlook 窗体区域](../vsto/creating-outlook-form-regions.md)。

## <a name="LoadBehavior"></a>LoadBehavior 值
 *Root*\Software\Microsoft\Office 下的**LoadBehavior**项\\*application name*\Addins\\*外接程序 ID*键包含指定 VSTO 外接程序运行时行为的值的按位组合。 最低顺序位（值 0 和 1）指示 VSTO 外接程序当前是已卸载还是已加载。 其他位指示应用程序何时尝试加载 VSTO 外接程序。

 通常，在最终用户计算机上安装 VSTO 外接程序时， **LoadBehavior**条目将设置为0、3或16（采用十进制）。 默认情况下，在生成或发布 VSTO 外接程序时，Visual Studio 会将外接程序的 **LoadBehavior** 条目设置为 3。

 下表列出了 **LoadBehavior** 条目的所有可能的值。 此表中的一些描述涉及手动或以编程方式加载 VSTO 外接程序。 若要手动加载 VSTO 外接程序，在应用程序的 **“COM 外接程序”** 对话框中选择 VSTO 外接程序旁的复选框。 若要以编程方式加载 VSTO 外接程序，请将表示 VSTO 外接程序的 <xref:Microsoft.Office.Core.COMAddIn.Connect%2A> 对象的 <xref:Microsoft.Office.Core.COMAddIn> 属性设置为 **true**。

|值（采用十进制）|VSTO 外接程序状态|VSTO 外接程序加载行为|描述|
|--------------------------|-------------------------|--------------------------------|-----------------|
|0|已卸载|不自动加载|应用程序从不尝试自动加载 VSTO 外接程序。 用户可尝试手动加载 VSTO 外接程序，也可以编程方式加载 VSTO 外接程序。<br /><br /> 如果 VSTO 外接程序加载成功，则 **LoadBehavior** 值保持为 0，但将更新 **“COM 外接程序”** 对话框中的 VSTO 外接程序状态，以指示已加载 VSTO 外接程序。|
|1|已加载|不自动加载|应用程序从不尝试自动加载 VSTO 外接程序。 用户可尝试手动加载 VSTO 外接程序，也可以编程方式加载 VSTO 外接程序。<br /><br /> 虽然 " **COM 外**接程序" 对话框指示已在应用程序启动后加载 vsto 外接程序，但只有在手动或以编程方式加载 vsto 外接程序时才会加载它。<br /><br /> 如果应用程序成功加载 VSTO 外接程序，则 **LoadBehavior** 值更改为 0，并在应用程序关闭后仍然保持为 0。|
|2|已卸载|在启动时加载|应用程序不会尝试自动加载 VSTO 外接程序。 用户可尝试手动加载 VSTO 外接程序，也可以编程方式加载 VSTO 外接程序。<br /><br /> 如果应用程序成功加载 VSTO 外接程序，则 **LoadBehavior** 值更改为 3，并在应用程序关闭后仍然保持为 3。|
|3|已加载|在启动时加载|应用程序在启动时尝试加载 VSTO 外接程序。 在 Visual Studio 中生成或发布 VSTO 外接程序时，这是默认值。<br /><br /> 如果应用程序成功加载 VSTO 外接程序，则 **LoadBehavior** 值保持为 3。 如果加载 VSTO 外接程序时出错，则 **LoadBehavior** 值更改为 2，并在应用程序关闭后仍然保持为 2。|
|8|已卸载|按需加载|应用程序不会尝试自动加载 VSTO 外接程序。 用户可尝试手动加载 VSTO 外接程序，也可以编程方式加载 VSTO 外接程序。<br /><br /> 如果应用程序成功加载 VSTO 外接程序，则 **LoadBehavior** 值更改为 9。|
|9|已加载|按需加载|VSTO 外接程序将仅在应用程序需要它时加载，例如，用户单击使用 VSTO 外接程序中的功能的 UI 元素（例如，功能区中的自定义按钮）时。<br /><br /> 如果应用程序成功加载 VSTO 外接程序，则 **LoadBehavior** 值保持为 9，但将更新 **“COM 外接程序”** 对话框中的外接程序状态，以指示当前已加载 VSTO 外接程序。 如果加载 VSTO 外接程序时出错，则 **LoadBehavior** 值更改为 8。|
|16|已加载|第一次时加载，然后按需加载|如果想要按需加载 VSTO 外接程序，请设置此值。 用户第一次运行应用程序时，应用程序将加载 VSTO 外接程序。 用户下一次运行应用程序时，应用程序将加载 VSTO 外接程序定义的任何 UI 元素，但不会加载 VSTO 外接程序，直到用户单击与 VSTO 外接程序关联的 UI 元素。<br /><br /> 应用程序第一次成功加载 VSTO 外接程序时， **LoadBehavior** 值在加载 VSTO 外接程序后保持为 16。 应用程序关闭后， **LoadBehavior** 值更改为 9。|

## <a name="see-also"></a>请参阅
- [Visual Studio 中 Office 解决方案的体系结构](../vsto/architecture-of-office-solutions-in-visual-studio.md)
- [VSTO 外接程序的体系结构](../vsto/architecture-of-vsto-add-ins.md)
- [构建 Office 解决方案](../vsto/building-office-solutions.md)
- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)
