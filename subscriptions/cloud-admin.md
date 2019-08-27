---
title: 设置云订阅的管理员 | Microsoft Docs
author: evanwindom
ms.author: jaunger
manager: lank
ms.date: 07/17/2019
ms.topic: conceptual
description: 设置云订阅的管理员
ms.openlocfilehash: 62a350e6061444e3c75878dfd89739011c4641d5
ms.sourcegitcommit: 57866dd72fd0e15ce61128df70729b427a2d02eb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68315202"
---
# <a name="set-up-administrators-for-visual-studio-cloud-subscriptions"></a>设置 Visual Studio 云订阅的管理员

Visual Studio 云订阅由管理员进行管理。 管理员可以分配订阅、编辑分配、添加或删除订阅以及执行其他的订阅管理工作。

## <a name="the-azure-subscription-owner-is-the-first-administrator"></a>Azure 订阅所有者是第一个管理员

当购买 Visual Studio 云订阅后，如果你是购买时所用的 Azure 订阅的所有者，系统会自动将你设置为这些订阅的管理员。

可通过 [Visual Studio Marketplace](https://marketplace.visualstudio.com/subscriptions) 或联系云解决方案提供商购买云订阅。 如果通过 Visual Studio Marketplace 购买，在购买过程的最后，你将获得管理用户的机会。 选择该选项后将转到 Visual Studio 订阅管理门户 - [https://manage.visualstudio.com](https://manage.visualstudio.com)。

购买订阅后，你随时可以访问[管理门户](https://manage.visualstudio.com)。 只需登录到门户，并在左上角选择相应的 Azure 订阅即可。

如果你是购买云订阅所用的 Azure 订阅的所有者，还可以分配其他管理员。

## <a name="add-administrators"></a>添加管理员

添加管理员需执行以下操作：

1. 在 [portal.azure.com](https://portal.azure.com) 上连接到 Azure 门户。
2. 使用用于购买 Visual Studio 云订阅的帐户登录。
3. 在左侧导航窗格中，向下滚动到“成本管理 + 计费”  。
4. 在“我的订阅”列表中，选择用于进行购买的 Azure 订阅  。
5. 左侧导航窗格中列表顶部附近单击“访问控制”  。
6. 在页面顶部单击“添加”选项卡  。
7. 单击“添加角色分配”  。
8. 在右侧的弹出窗格中，在窗格顶部单击“角色”下拉列表，向下滚动，然后选择“用户访问管理员”   。
9. 在用户列表中向下滚动至你想要创建管理员的用户并选择该用户。 
10. 单击“保存”  。
11. 单击“角色分配”选项卡，验证所选用户现在是否显示为“用户访问管理员”  。

新管理员这时可以登录到[管理门户](https://manage.visualstudio.com)，从页面左上角的列表中选择用于购买云订阅的同一个 Azure 订阅，然后开始管理这些订阅。

> [!NOTE]
> 如果看到具有访问权限的用户要编辑你未以管理员身份建立的云订阅，他们可能具有基础 Azure 订阅中的角色，使他们能够管理订阅。 这些角色包括：所有者、参与者、服务管理员或共同管理员。有关详细信息，请访问[添加账单管理员](/azure/devops/organizations/billing/add-backup-billing-managers?view=vsts)。

有关 Visual Studio 云订阅的信息，请参阅“购买订阅”下的[概述](vscloud-overview.md)。 要购买 Visual Studio 云订阅，请访问 Visual Studio Marketplace：[https://marketplace.visualstudio.com/subscriptions](https://marketplace.visualstudio.com/subscription)。
