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
ms.openlocfilehash: 2add0dfced6a3b8e8263dafe133ee3a2f86637f5
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63420940"
---
# <a name="improve-the-performance-of-a-vsto-add-in"></a>提高 VSTO 外接程序的性能
  可以通过优化为 Office 应用程序创建的 VSTO 外接程序为用户提供更好的体验，以便他们快速启动、关闭和打开项，以及执行其他任务。 如果你的 VSTO 外接程序是用于 Outlook 的，则还可以降低由于性能不佳而禁用 VSTO 外接程序的风险。 可以通过实现以下策略来提高 VSTO 外接程序的性能：

- [按需加载 VSTO 外接程序](#Load)。

- [使用 Windows Installer 发布 Office 解决方案](#Publish)。

- [绕过功能区反射](#Bypass)。

- [在单独的执行线程中执行成本高昂的操作](#Perform)。

  有关如何优化 Outlook VSTO 外接程序的详细信息，请参阅[性能条件，以使 VSTO 外接启用](http://go.microsoft.com/fwlink/?LinkID=266503)。

## <a name="Load"></a> 按需加载 VSTO 外接程序
 可以将 VSTO 外接程序配置为仅在下列情况下加载：

- 安装 VSTO外接程序后，用户第一次启动应用程序时。

- 随后任何时间启动应用程序后，用户与 VSTO 外接程序第一次交互时。

  例如，VSTO 外接程序中可能会填充工作表的数据时用户选择标记的自定义按钮**获取我的数据**。 应用程序必须加载 VSTO 外接程序中至少一次，以便**获取我的数据**按钮可以在功能区中出现。 但是，VSTO 外接程序不会再次加载当用户启动应用程序下一次。 VSTO 外接程序仅在用户选择 **“获取我的数据”** 按钮时加载。

### <a name="to-configure-a-clickonce-solution-to-load-vsto-add-ins-on-demand"></a>配置 ClickOnce 解决方案以按需加载 VSTO 外接程序

1. 在 **“解决方案资源管理器”** 中，选择项目节点。

2. 在菜单栏上，依次选择“查看” > “属性页”。

3. 在 **“发布”** 选项卡上，选择 **“选项”** 按钮。

4. 在 **“发布选项”** 对话框中，选择 **“Office 设置”** 列表项，选择 **“按需加载”** 选项，然后选择 **“确定”** 按钮。

### <a name="to-configure-a-windows-installer-solution-to-load-vsto-add-ins-on-demand"></a>配置 Windows Installer 解决方案以按需加载 VSTO 外接程序

1. 在注册表中，设置`LoadBehavior`的条目 **_根_\Software\Microsoft\Office\\_ApplicationName_\Addins\\ _外接程序 ID_** 关键**0x10**。

     有关详细信息，请参阅[VSTO 外接程序的注册表项](../vsto/registry-entries-for-vsto-add-ins.md)。

### <a name="to-configure-a-solution-to-load-vsto-add-ins-on-demand-while-you-debug-the-solution"></a>将解决方案配置为在调试解决方案时按需加载 VSTO 外接程序

1. 创建一个脚本，设置`LoadBehavior`的条目 **_根_\Software\Microsoft\Office\\_ApplicationName_\Addins\\ _外接程序 ID_** 关键**0x10**。

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

     有关如何创建生成后事件中的信息C#项目，请参阅[如何：指定生成事件&#40;C&#35;&#41;](../ide/how-to-specify-build-events-csharp.md)。

     有关如何在 Visual Basic 项目中创建生成后事件的信息，请参阅[如何：指定生成事件&#40;Visual Basic&#41;](../ide/how-to-specify-build-events-visual-basic.md)。

## <a name="Publish"></a> 使用 Windows Installer 发布 Office 解决方案
 如果使用 Windows Installer 发布解决方案，Visual Studio 2010 Tools for Office 运行时绕过以下步骤，VSTO 外接程序加载时。

- 验证清单架构。

- 自动检查更新。

- 验证部署清单的数字签名。

  > [!NOTE]
  > 此方法不需要在 VSTO 外接程序部署到用户的计算机上的安全位置。

  有关详细信息，请参阅[使用 Windows Installer 部署 Office 解决方案](../vsto/deploying-an-office-solution-by-using-windows-installer.md)。

## <a name="Bypass"></a> 绕过功能区反射
 如果通过使用生成的解决方案[!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)]，请确保部署解决方案时，你的用户已安装 Visual Studio 2010 Tools for Office 运行时的最新版本。 该运行时的较旧版本反射到解决方案程序集查找功能区自定义。 此过程可导致 VSTO 外接程序加载变慢。

 或者，可以防止任何版本的 Visual Studio 2010 Tools for Office 运行时使用反射来标识功能区自定义。 若要遵循此策略，重写`CreateRibbonExtensibility`方法，并显式返回功能区对象。 如果 VSTO 外接程序中不包含任何功能区自定义项，则返回`null`在该方法。

 以下示例返回基于字段的值的功能区对象。

 [!code-vb[Trin_Ribbon_Choose_Ribbon#1](../vsto/codesnippet/VisualBasic/trin_ribbon_choose_ribbon_4/ThisWorkbook.vb#1)]
 [!code-csharp[Trin_Ribbon_Choose_Ribbon#1](../vsto/codesnippet/CSharp/trin_ribbon_choose_ribbon_4/ThisWorkbook.cs#1)]

## <a name="Perform"></a> 在单独的执行线程中执行成本高昂的操作
 请考虑在单独的线程中执行耗时的任务（如长时间运行的任务、数据库连接或其他类型的网络调用）。 有关详细信息，请参阅[Office 中的线程支持](../vsto/threading-support-in-office.md)。

> [!NOTE]
> 调入 Office 对象模型的所有代码都必须在主线程中执行。

## <a name="see-also"></a>请参阅

- [按需加载 VSTO 外接程序](https://blogs.msdn.microsoft.com/andreww/2008/07/14/demand-loading-vsto-add-ins/)
- [延迟加载 Office 外接程序中的 CLR](https://blogs.msdn.microsoft.com/andreww/2008/04/19/delay-loading-the-clr-in-office-add-ins/)
- [使用 Visual Studio 创建适用于 Office VSTO 加载项](create-vsto-add-ins-for-office-by-using-visual-studio.md)
