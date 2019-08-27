---
title: 下载按需程序集通过 ClickOnce 使用设计器
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- assemblies, downloading [ClickOnce]
- Windows applications, ClickOnce deployments
- ClickOnce deployment, on-demand download
- on-demand assemblies, ClickOnce
ms.assetid: 59a0dd5f-1cab-4f2f-b780-0ab7399905d5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5a8c5def5c4ebdf8f34efef50dca8dc4656bbd7d
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66263440"
---
# <a name="walkthrough-download-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer"></a>演练：下载 ClickOnce 部署 API 使用设计器中使用按需程序集
默认情况下， [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序中包含的所有程序集都会在应用程序首次运行时进行下载。 但是，可能有一小部分用户使用部分应用程序。 在这种情况下，你希望仅当创建其类型之一时才下载程序集。 下面的演练演示如何将应用程序中的某些程序集标记为“可选”，以及如何在公共语言运行时需要它们时使用 <xref:System.Deployment.Application> 命名空间中的类下载它们。

> [!NOTE]
> 应用程序必须在完全信任下运行才能使用此过程。

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请单击 **“工具”** 菜单上的 **“导入和导出设置”** 。 有关详细信息，请参阅[重置设置](../ide/environment-settings.md#reset-settings)。

## <a name="create-the-projects"></a>创建项目

### <a name="to-create-a-project-that-uses-an-on-demand-assembly-with-visual-studio"></a>通过 Visual Studio 创建使用按需程序集的项目

1. 在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]中创建新的 Windows 窗体项目。 在“文件”  菜单上，指向“添加”  ，然后单击“新建项目”  。 在对话框中选择“类库”  项目，并将它命名为 `ClickOnceLibrary`。

   > [!NOTE]
   > 在 Visual Basic 中，我们建议修改项目属性以将此项目的根命名空间更改为 `Microsoft.Samples.ClickOnceOnDemand` 或更改为所选的命名空间。 为简单起见，此演练中的两个项目处于同一个命名空间中。

2. 定义一个名为 `DynamicClass` 的类，它具有名为 `Message`的单个属性。

    [!code-vb[ClickOnceLibrary#1](../deployment/codesnippet/VisualBasic/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer_1.vb)]
    [!code-csharp[ClickOnceLibrary#1](../deployment/codesnippet/CSharp/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer_1.cs)]

3. 在“解决方案资源管理器”  中选择 Windows 窗体项目。 添加对 <xref:System.Deployment.Application> 程序集的引用以及对 `ClickOnceLibrary` 项目的项目引用。

   > [!NOTE]
   > 在 Visual Basic 中，我们建议修改项目属性以将此项目的根命名空间更改为 `Microsoft.Samples.ClickOnceOnDemand` 或更改为所选的命名空间。 为简单起见，此演练中的两个项目处于同一个命名空间中。

4. 右键单击窗体，在菜单中单击“查看代码”  ，然后将以下引用添加到窗体。

    [!code-csharp[ClickOnceOnDemand#1](../deployment/codesnippet/CSharp/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer_2.cs)]
    [!code-vb[ClickOnceOnDemand#1](../deployment/codesnippet/VisualBasic/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer_2.vb)]

5. 添加以下代码以按需下载此程序集。 此代码演示如何使用泛型 <xref:System.Collections.DictionaryBase.Dictionary%2A> 类将一组程序集映射到一个组名称。 因为我们在此演练中只下载单个程序集，所以组中只有一个程序集。 在实际应用程序中，你可能要同时下载与应用程序中的单个功能相关的所有程序集。 通过映射表可以将属于某个功能的所有 DLL 与下载组名称关联，从而使你可以轻松地实现此目标。

    [!code-csharp[ClickOnceOnDemand#2](../deployment/codesnippet/CSharp/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer_3.cs)]
    [!code-vb[ClickOnceOnDemand#2](../deployment/codesnippet/VisualBasic/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer_3.vb)]

6. 在 **“视图”** 菜单上单击 **“工具箱”** 。 将 <xref:System.Windows.Forms.Button> 从“工具箱”  拖动到窗体上。 双击按钮并将下面的代码添加到 <xref:System.Windows.Forms.Control.Click> 事件处理程序。

    [!code-csharp[ClickOnceOnDemand#3](../deployment/codesnippet/CSharp/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer_4.cs)]
    [!code-vb[ClickOnceOnDemand#3](../deployment/codesnippet/VisualBasic/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer_4.vb)]

## <a name="mark-assemblies-as-optional"></a>标记为可选的程序集

### <a name="to-mark-assemblies-as-optional-in-your-clickonce-application-by-using-visual-studio"></a>使用 Visual Studio 在 ClickOnce 应用程序中将程序集标记为可选

1. 在“解决方案资源管理器”  中右键单击 Windows 窗体项目，然后单击“属性”  。 选择“发布”  选项卡。

2. 单击“应用程序文件”  按钮。

3. 在列表中找到 ClickOnceLibrary.dll  。 将“发布状态”  下拉框设置为“包括”  。

4. 展开“组”  下拉框，然后选择“新建”  。 输入名称 `ClickOnceLibrary` 作为新的组名称。

5. 继续发布应用程序，如中所述[如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。

### <a name="to-mark-assemblies-as-optional-in-your-clickonce-application-by-using-manifest-generation-and-editing-tool--graphical-client-mageuiexe"></a>使用清单生成和编辑工具在 ClickOnce 应用程序中将程序集标记为可选 — 图形客户端 (MageUI.exe)

1. 创建你[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]清单中所述[演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)。

2. 关闭 MageUI.exe 之前，选择包含部署应用程序清单的选项卡，然后在该选项卡中选择“文件”  选项卡。

3. 在应用程序文件的列表中找到 ClickOnceLibrary.dll，然后将其“文件类型”  列设置“无”  。 对于“组”  列，输入 `ClickOnceLibrary.dll`。

## <a name="test-the-new-assembly"></a>测试新程序集

测试按需程序集：

1. 启动使用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]部署的应用程序。

2. 在主窗体显示时按 <xref:System.Windows.Forms.Button>。 你应在消息框窗口中看到一个显示为“Hello, World!”的字符串

## <a name="see-also"></a>请参阅

- <xref:System.Deployment.Application.ApplicationDeployment>
