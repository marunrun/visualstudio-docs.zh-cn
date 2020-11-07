---
title: 启用 ClickOnce 安全设置 |Microsoft Docs
description: 了解发布向导如何自动启用 ClickOnce 应用程序的代码访问安全性以发布应用程序。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- security [Visual Studio], ClickOnce applications
- ClickOnce deployment, security settings
- security settings, ClickOnce deployment
ms.assetid: 73cd3e9d-cd72-4ad2-8cae-94d6bb6b01e0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: db31d0182c598b32933cf2d4260706a2252a9b6f
ms.sourcegitcommit: 75bfdaab9a8b23a097c1e8538ed1cde404305974
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94351162"
---
# <a name="how-to-enable-clickonce-security-settings"></a>如何：启用 ClickOnce 安全设置
必须启用 ClickOnce 应用程序的代码访问安全性才能发布应用程序。 使用发布向导发布应用程序时，会自动执行此操作。

 在某些情况下，启用代码访问安全性会影响生成或调试应用程序时的性能;在这些情况下，你可能希望暂时禁用安全设置。

 可以在 " **项目设计器** " 的 " **安全** " 页上启用或禁用 ClickOnce 安全设置。

### <a name="to-enable-clickonce-security-settings"></a>启用 ClickOnce 安全设置

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击“安全”选项卡。 

3. 选中“启用 ClickOnce 安全设置”  复选框。

     你现在可以在 "安全" 页上为你的应用程序自定义安全设置。

    > [!NOTE]
    > 每次用 **发布** 向导发布应用程序时，都将自动选择此复选框。

### <a name="to-disable-clickonce-security-settings"></a>禁用 ClickOnce 安全设置

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击“安全”选项卡。 

3. 清除 " **启用 ClickOnce 安全设置** " 复选框。

     应用程序将以 "完全信任" 安全设置运行;" **安全性** " 页上的所有设置都将被忽略。

    > [!NOTE]
    > 每次用发布向导发布应用程序时，都将选中此复选框;你必须在每次成功发布后再次将其清除。

## <a name="see-also"></a>请参阅
- [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)
- [ClickOnce 应用程序的代码访问安全性](../deployment/code-access-security-for-clickonce-applications.md)
