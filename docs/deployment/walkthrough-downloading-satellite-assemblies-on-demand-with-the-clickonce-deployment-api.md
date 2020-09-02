---
title: 用 ClickOnce 部署 API 按需下载附属程序集
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, globalization
- localization, Windows Forms
- Windows Forms, localization
- globalization, ClickOnce
- satellite assemblies, ClickOnce
- ClickOnce deployment, on-demand download
- localization, ClickOnce deployment
- ClickOnce deployment, localization
ms.assetid: fdaa553f-a27e-44eb-a4e2-08c122105a87
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 34cde3a2444525e48455e445894fd5ab1c66fab8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "66262973"
---
# <a name="walkthrough-download-satellite-assemblies-on-demand-with-the-clickonce-deployment-api"></a>演练：通过 ClickOnce 部署 API 按需下载附属程序集
通过使用附属程序集，可以为多个区域性配置 Windows 窗体应用程序。 *附属程序集* 是一种包含除应用程序默认区域性以外区域性的应用程序资源的程序集。

 如 [本地化 ClickOnce 应用程序](../deployment/localizing-clickonce-applications.md)中所述，可以在同一部署中包含多个区域性的多个附属程序集 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 默认情况下，即使单个客户端可能只需要一个附属程序集， [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 也会将部署中的所有附属程序集下载到客户端计算机中。

 本演练演示如何将附属程序集标记为可选，并且只下载客户端计算机的当前区域性设置需要的程序集。 下面的过程使用 [!INCLUDE[winsdklong](../deployment/includes/winsdklong_md.md)]中可用的工具。 还可在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]中执行此任务。  另请参阅 [演练：使用 clickonce 部署 api 按需下载附属程序集](/previous-versions/visualstudio/visual-studio-2012/ms366788(v=vs.110)) 或 [演练：在设计器中使用 clickonce 部署 Api 按需下载附属程序集](/previous-versions/visualstudio/visual-studio-2013/ms366788(v=vs.120))。

> [!NOTE]
> 出于测试目的，下面的代码示例以编程方式将区域性设置为 `ja-JP`。 有关如何为生产环境调整此代码的信息，请参阅本主题中后面的“后续步骤”部分。

## <a name="prerequisites"></a>先决条件
 本主题假定你知道如何使用 Visual Studio 将本地化的资源添加到应用程序。 有关详细说明，请参阅 [演练：本地化 Windows 窗体](/previous-versions/visualstudio/visual-studio-2010/y99d1cd3(v=vs.100))。

### <a name="to-download-satellite-assemblies-on-demand"></a>按需下载附属程序集

1. 将以下代码添加到应用程序以启用按需下载附属程序集。

    [!code-csharp[ClickOnce.SatelliteAssembliesSDK#1](../deployment/codesnippet/CSharp/walkthrough-downloading-satellite-assemblies-on-demand-with-the-clickonce-deployment-api_1.cs)]
    [!code-vb[ClickOnce.SatelliteAssembliesSDK#1](../deployment/codesnippet/VisualBasic/walkthrough-downloading-satellite-assemblies-on-demand-with-the-clickonce-deployment-api_1.vb)]

2. 使用 [Resgen.exe (资源文件生成器) ](/dotnet/framework/tools/resgen-exe-resource-file-generator) 或生成应用程序的附属程序集 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

3. 使用 MageUI.exe 生成应用程序清单，或打开现有的应用程序清单**。 有关此工具的详细信息，请参阅[MageUI.exe（图形化客户端中的清单生成和编辑工具）](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)。

4. 单击“文件” **** 选项卡。

5. 单击“省略号”按钮 (...)，然后选择包含所有应用程序的程序集和文件（包括使用 Resgen.exe 生成的附属程序集）的目录**********。 附属程序集 (* \<isoCode>\ApplicationName.resources.dll*格式的名称，其中 \<isoCode> 是 RFC 1766 格式的语言标识符。 ) 

6. 单击“填充” **** 将文件添加到部署。

7. 选择每个附属程序集的“可选” **** 复选框。

8. 将每个附属程序集的组字段设置为它的 ISO 语言标识符。 例如，对于日语附属程序集，可以指定 `ja-JP`中可用的工具。 这将使在步骤 1 添加的代码能够下载适当的附属程序集，这取决于用户的 <xref:System.Threading.Thread.CurrentUICulture%2A> 属性设置。

## <a name="next-steps"></a>后续步骤
 在生产环境中，可能需要删除将 <xref:System.Threading.Thread.CurrentUICulture%2A> 设置为特定值的代码示例中的行，因为客户端计算机将以默认方式设置正确值。 例如，当在日语客户端计算机上运行应用程序时，默认情况下， <xref:System.Threading.Thread.CurrentUICulture%2A> 将设置为 `ja-JP` 。 以编程方式设置此值是在部署应用程序之前测试附属程序集的一个很好的方法。

## <a name="see-also"></a>另请参阅
- [本地化 ClickOnce 应用程序](../deployment/localizing-clickonce-applications.md)
