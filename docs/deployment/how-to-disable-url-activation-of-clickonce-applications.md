---
title: 禁用 ClickOnce 应用程序的 URL 激活
description: 了解如何在您希望用户从 "开始" 菜单启动应用程序时，为 ClickOnce 应用程序禁用 "自动启动"。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- disallowUrlActivation
- URL activation, ClickOnce applications
- ClickOnce deployment, URL activation
ms.assetid: db31a16b-960f-4264-91d7-c7c40f876068
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 46e46278f5465de029aa9536744f51843397d743
ms.sourcegitcommit: 75bfdaab9a8b23a097c1e8538ed1cde404305974
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94351227"
---
# <a name="how-to-disable-url-activation-of-clickonce-applications"></a>如何：禁用 ClickOnce 应用程序的 URL 激活

通常，从 Web 服务器安装 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序后它会立即自动启动。 出于安全原因，可以决定禁用此行为，并告诉用户改为从“开始”菜单启动该应用程序。 以下过程描述了如何禁用 URL 激活。

此方法仅适用于从 Web 服务器安装到用户计算机上的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序。 它不能用于仅联机应用程序，仅联机应用程序可以通过使用其 URL 启动。 有关仅联机应用程序与已安装应用程序之间的差异的详细信息，请参阅[选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)。

此过程使用 Windows 软件开发工具包 (SDK) 工具 MageUI.exe。 此工具的详细信息，请参阅[MageUI.exe（图形化客户端中的清单生成和编辑工具）](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)。 你还可以使用 Visual Studio 执行此过程。

## <a name="procedure"></a>过程

### <a name="to-disable-url-activation-for-your-application"></a>禁用应用程序的 URL 激活的步骤

1. 在 MageUI.exe 中打开部署清单。 如果尚未创建一个，请按照 [演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)中的步骤进行操作。

2. 选择“部署选项”选项卡。

3. 清除“安装后自动运行应用程序”复选框。

4. 保存并对清单进行签名。

## <a name="see-also"></a>请参阅

- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)