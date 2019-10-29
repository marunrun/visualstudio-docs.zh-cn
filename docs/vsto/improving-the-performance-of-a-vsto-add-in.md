---
title: 提高 VSTO 外接程序的性能
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 564672e01eeffbdcb53bf1af08f329d2f6bf218f
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72985774"
---
# <a name="improve-the-performance-of-a-vsto-add-in"></a>提高 VSTO 外接程序的性能
  可以通过优化为 Office 应用程序创建的 VSTO 外接程序为用户提供更好的体验，以便他们快速启动、关闭和打开项，以及执行其他任务。 如果你的 VSTO 外接程序是用于 Outlook 的，则还可以降低由于性能不佳而禁用 VSTO 外接程序的风险。 可以通过实现以下策略来提高 VSTO 外接程序的性能：

- [按需加载 VSTO 外接程序](#Load)。

- [使用 Windows Installer 发布 Office 解决方案](#Publish)。

- [绕过功能区反射](#Bypass)。

- [在单独的执行线程中执行成本高昂的操作](#Perform)。

  有关如何优化 Outlook VSTO 外接程序的详细信息，请参阅[使 VSTO 外接程序保持启用状态的性能标准](/previous-versions/office/jj228679(v=office.15)#ol15WhatsNew_AddinDisabling)。

## <a name="Load"></a> 按需加载 VSTO 外接程序
 可以将 VSTO 外接程序配置为仅在下列情况下加载：

- 安装 VSTO外接程序后，用户第一次启动应用程序时。

- 随后任何时间启动应用程序后，用户与 VSTO 外接程序第一次交互时。

  例如，当用户选择标记为 **"获取我的数据"** 的自定义按钮时，VSTO 外接程序可能会用数据填充工作表。 应用程序必须至少加载一次 VSTO 外接程序，以便 "**获取我的数据**" 按钮可显示在功能区中。 但是，当用户下次启动应用程序时，VSTO 外接程序不会再次加载。 VSTO 外接程序仅在用户选择 **“获取我的数据”** 按钮时加载。

### <a name="to-configure-a-clickonce-solution-to-load-vsto-add-ins-on-demand"></a>配置 ClickOnce 解决方案以按需加载 VSTO 外接程序

1. 在 **“解决方案资源管理器”** 中，选择项目节点。

2. 在菜单栏上，依次选择“查看” > “属性页”。

3. 在 **“发布”** 选项卡上，选择 **“选项”** 按钮。

4. 在 **“发布选项”** 对话框中，选择 **“Office 设置”** 列表项，选择 **“按需加载”** 选项，然后选择 **“确定”** 按钮。

### <a name="to-configure-a-windows-installer-solution-to-load-vsto-add-ins-on-demand"></a>配置 Windows Installer 解决方案以按需加载 VSTO 外接程序

1. 在注册表中，将根 \Software\Microsoft\Office 的 `LoadBehavior` 条目设置 **\\_ApplicationName_\ADDINS\\_外接程序 ID_** 键设置为**0x10**。

     有关详细信息，请参阅[VSTO 外接程序的注册表项](../vsto/registry-entries-for-vsto-add-ins.md)。

### <a name="to-configure-a-solution-to-load-vsto-add-ins-on-demand-while-you-debug-the-solution"></a>将解决方案配置为在调试解决方案时按需加载 VSTO 外接程序

1. 创建一个脚本，用于将 **_根_\Software\Microsoft\Office\\_ApplicationName_\ADDINS\\_外接程序 ID_** 键的 `LoadBehavior` 项设置为**0x10**。

     下面的代码演示了此脚本的一个示例。

    ```cmd/sh
    [HKEY_CURRENT_USER\Software\Microsoft\Office\Excel\Addins\MyAddIn]
    "Description"="MyAddIn"
    "FriendlyName"="MyAddIn"
    "LoadBehavior"=dword:00000010
    "Manifest"="c:\\Temp\\MyAddIn\\bin\\Debug\\MyAddIn.vsto|vstolocal"

    ```

2. 创建一个使用脚本更新注册表的生成后事件。

     下面的代码演示了可添加到生成后事件的命令字符串的示例。

    ```cmd/sh
    regedit /s "$(SolutionDir)$(SolutionName).reg"

    ```

     有关如何在C#项目中创建生成后事件的信息，请参阅[如何：指定生成事件&#40;C&#35;](../ide/how-to-specify-build-events-csharp.md)。

     有关如何在 Visual Basic 项目中创建生成后事件的信息，请参阅[如何：指定生成&#40;事件 Visual Basic&#41;](../ide/how-to-specify-build-events-visual-basic.md)。

## <a name="Publish"></a>使用 Windows Installer 发布 Office 解决方案
 如果使用 Windows Installer 发布解决方案，则在加载 VSTO 外接程序时，Visual Studio 2010 Tools for Office runtime 会绕过以下步骤。

- 验证清单架构。

- 自动检查更新。

- 验证部署清单的数字签名。

  > [!NOTE]
  > 如果将 VSTO 外接程序部署到用户计算机上的安全位置，则不需要此方法。

  有关详细信息，请参阅[使用 Windows Installer 部署 Office 解决方案](../vsto/deploying-an-office-solution-by-using-windows-installer.md)。

## <a name="Bypass"></a>绕过功能区反射
 如果使用 [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)]生成解决方案，请确保在部署解决方案时，用户已安装了 Visual Studio 2010 Tools for Office runtime 的最新版本。 早期版本的 VSTO 运行时反映为解决方案程序集，以定位功能区自定义项。 此过程可导致 VSTO 外接程序加载变慢。

 作为替代方法，可以通过使用反射来标识功能区自定义，从而防止 Visual Studio 2010 Tools for Office runtime 的任何版本使用反射。 若要遵循此策略，请重写 `CreateRibbonExtensibility` 方法，并显式返回功能区对象。 如果 VSTO 外接程序不包含任何功能区自定义项，请在方法内部返回 `null`。

 下面的示例根据字段的值返回一个功能区对象。

 [!code-vb[Trin_Ribbon_Choose_Ribbon#1](../vsto/codesnippet/VisualBasic/trin_ribbon_choose_ribbon_4/ThisWorkbook.vb#1)]
 [!code-csharp[Trin_Ribbon_Choose_Ribbon#1](../vsto/codesnippet/CSharp/trin_ribbon_choose_ribbon_4/ThisWorkbook.cs#1)]

## <a name="Perform"></a>在单独的执行线程中执行成本高昂的操作
 请考虑在单独的线程中执行耗时的任务（如长时间运行的任务、数据库连接或其他类型的网络调用）。 有关详细信息，请参阅[Office 中的线程支持](../vsto/threading-support-in-office.md)。

> [!NOTE]
> 调入 Office 对象模型的所有代码都必须在主线程中执行。

## <a name="see-also"></a>请参阅

- [按需加载 VSTO 外接程序](https://blogs.msdn.microsoft.com/andreww/2008/07/14/demand-loading-vsto-add-ins/)
- [延迟加载 Office 外接程序中的 CLR](https://blogs.msdn.microsoft.com/andreww/2008/04/19/delay-loading-the-clr-in-office-add-ins/)
- [使用 Visual Studio 创建 Office VSTO 外接程序](create-vsto-add-ins-for-office-by-using-visual-studio.md)
