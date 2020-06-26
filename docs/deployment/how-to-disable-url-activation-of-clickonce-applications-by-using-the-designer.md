---
title: 使用设计器禁用 ClickOnce 应用程序的 URL 激活
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- disallowURLActivation
- URL activation, ClickOnce applications
- ClickOnce deployment, URL activation
ms.assetid: a337a582-e67c-409a-b52e-607cd1a8fc57
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 818ab634d48fb666ecab5d89464ea017040bd250
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382479"
---
# <a name="how-to-disable-url-activation-of-clickonce-applications-by-using-the-designer"></a>如何：使用设计器禁用 ClickOnce 应用程序的 URL 激活
通常，在 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 从 Web 服务器安装应用程序后，该应用程序将立即自动启动。 出于安全原因，你可以决定禁用此行为，并告诉用户从 "**开始**" 菜单启动应用程序。 以下过程描述了如何禁用 URL 激活。

 此方法仅适用于从 Web 服务器安装到用户计算机上的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序。 它不能用于仅联机的应用程序，只能通过使用其 URL 来启动这些应用程序。 有关仅联机应用程序与已安装应用程序之间的差异的详细信息，请参阅[选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)。

 此过程使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 你还可以使用来完成此任务 [!INCLUDE[winsdklong](../deployment/includes/winsdklong_md.md)] 。 有关详细信息，请参阅[如何：禁用 ClickOnce 应用程序的 URL 激活](../deployment/how-to-disable-url-activation-of-clickonce-applications.md)。

## <a name="procedure"></a>过程

#### <a name="to-disable-url-activation-for-your-application"></a>禁用应用程序的 URL 激活的步骤

1. 在**解决方案资源管理器**中右键单击项目名称，然后单击 "**属性**"。

2. 在 "**属性**" 页上，单击 "**发布**" 选项卡。

3. 单击“选项”。

4. 单击 "**清单**"。

5. 选中标签为 "**阻止应用程序通过 URL 激活**" 的复选框。

6. 部署应用程序。

## <a name="see-also"></a>请参阅
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)