---
title: 演练：下载按需使用 ClickOnce 部署 API 使用设计器的附属程序集 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Windows Forms, globalization
- ClickOnce deployment, globalization
- localization, Windows Forms
- ClickOnce, on-demand download
- Windows Forms, localization
- ClickOnce deployment, localization
- walkthroughs, localization
ms.assetid: 82b85a47-b223-4221-a17c-38a52c3fb6e2
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 559fb1f3613b42bd2c972f61b45736b07e76a318
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62420010"
---
# <a name="walkthrough-downloading-satellite-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer"></a>演练：使用 ClickOnce 部署使用设计器的 API 按需下载附属程序集

[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过使用附属程序集，可以为多个区域性配置 Windows 窗体应用程序。 *附属程序集* 是一种包含除应用程序默认区域性以外区域性的应用程序资源的程序集。

如中所述[本地化 ClickOnce 应用程序](../deployment/localizing-clickonce-applications.md)，可以包括适用于多个区域性相同的多个附属程序集[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]部署。 默认情况下，即使单个客户端可能只需要一个附属程序集， [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 也会将部署中的所有附属程序集下载到客户端计算机中。

本演练演示如何将附属程序集标记为可选，并且只下载客户端计算机的当前区域性设置需要的程序集。

> [!NOTE]
> 出于测试目的，下面的代码示例以编程方式将区域性设置为 `ja-JP`。 有关如何为生产环境调整此代码的信息，请参阅本主题中后面的“后续步骤”部分。

### <a name="to-mark-satellite-assemblies-as-optional"></a>将附属程序集标记为可选

1. 生成你的项目。 此操作将针对作为本地化目标的所有区域性生成附属程序集。

2. 在解决方案资源管理器中右键单击项目名称，并单击“属性”。

3. 单击“发布”选项卡，然后单击“应用程序文件”。

4. 选中“显示所有文件”复选框以显示附属程序集。 默认情况下，所有附属程序集都会包含在部署中，且在此对话框中可见。

     附属程序集将包含一个名称，形式*isoCode*\ApplicationName.resources.dll，其中*isoCode*是 RFC 1766 格式的语言标识符。

5. 单击**新...** 中**下载组**为每个语言标识符的列表。 如果提示输入下载组名称，请输入语言标识符。 例如，对于日语附属程序集，将指定下载组名称`ja-JP`。

6. 关闭“应用程序文件”对话框。

### <a name="to-download-satellite-assemblies-on-demand-in-c"></a>在 C\# 中按需下载附属程序集

1. 打开 Program.cs 文件。 如果未在解决方案资源管理器中看到此文件，则选择项目，然后在“项目”菜单上单击“显示所有文件”。

2. 使用下面的代码下载适当的附属程序集，并启动应用程序。

     [!code-csharp[ClickOnce.SatelliteAssemblies#1](../snippets/csharp/VS_Snippets_Winforms/ClickOnce.SatelliteAssemblies/CS/Program.cs#1)]

### <a name="to-download-satellite-assemblies-on-demand-in-visual-basic"></a>在 Visual Basic 中按需下载附属程序集

1. 在应用程序的“属性”窗口中，单击“应用程序”选项卡。

2. 在选项卡页的底部，单击“查看应用程序事件”。

3. 将下列导入内容添加到 ApplicationEvents.VB 文件的开头。

     [!code-vb[ClickOnce.SatelliteAssembliesVB#1](../snippets/visualbasic/VS_Snippets_Winforms/ClickOnce.SatelliteAssembliesVB/VB/ApplicationEvents.vb#1)]

4. 向 `MyApplication` 类添加下面的代码。

     [!code-vb[ClickOnce.SatelliteAssembliesVB#2](../snippets/visualbasic/VS_Snippets_Winforms/ClickOnce.SatelliteAssembliesVB/VB/ApplicationEvents.vb#2)]

## <a name="next-steps"></a>后续步骤

在生产环境中，可能需要删除代码示例中将 <xref:System.Threading.Thread.CurrentUICulture%2A> 设置为特定值的行，因为在默认情况下，客户端计算机会设置正确的值。 例如，当在日语客户端计算机上运行应用程序时，默认情况下， <xref:System.Threading.Thread.CurrentUICulture%2A> 将设置为 `ja-JP` 。 在部署应用程序之前，以编程的方式执行设置是测试附属程序集的一种好方法。

## <a name="see-also"></a>请参阅

- [演练：使用 ClickOnce 部署 API 按需下载附属程序集](../deployment/walkthrough-downloading-satellite-assemblies-on-demand-with-the-clickonce-deployment-api.md)
- [本地化 ClickOnce 应用程序](../deployment/localizing-clickonce-applications.md)
