---
title: 在 Visual Studio 订阅管理门户中删除订阅分配 |Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.assetid: e49242bc-e9f2-49e8-8caa-f574d508aba6
ms.date: 06/16/2020
ms.topic: how-to
description: 了解管理员如何删除订阅分配
ms.openlocfilehash: e6ce84aa84e25bcdeb44b93954289a65a3454010
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85902908"
---
# <a name="delete-assignments-in-visual-studio-subscriptions"></a>删除 Visual Studio 订阅中的分配
当订阅者不再需要 Visual Studio 订阅时，比如当他们离开公司、完成项目或转换为新的作业角色时，你可以删除他们的订阅，并将订阅分配给其他人。 请注意，重新分配订阅时，并非所有订阅者权益都将重置。  新用户将能够认领任何无人认领的密钥并查看以前认领过的密钥，但认领限制**不**会重置。  组织若具有企业协议 (EA)，将重置供原始用户使用的任何权益（如 Pluralsight 培训）。 

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4yG2q]

## <a name="delete-a-subscription-assignment"></a>删除订阅分配
1. 单击要删除的订阅者名称。 若要选择多个要删除的订阅者，可以单击订阅者名称左侧的圆圈来选择每个订阅者。  或者，你可以按住 CTRL 键，然后单击要删除的每个订阅者。 若要删除某一范围的订阅服务器，请单击第一个订阅服务器，按 Shift 键，然后单击最后一个。  按 CTRL + A，选择并删除所有订阅者。 
2. 若要删除所选订阅者，请单击“删除”。
3. 出现要求确认删除的消息时，单击“确定”。
   > [!div class="mx-imgBorder"]
   > ![删除订阅者](_img/delete-license/delete-subscribers.png)

   > [!NOTE]
   > 使用模板进行批量删除的功能不可用。 对于通过 Azure Active Directory 安全组来管理订阅分配的组织，请参阅[我们的文章](assign-license-bulk.md#use-azure-active-directory-groups-to-assign-subscriptions)，详细了解如何进行删除。  

## <a name="see-also"></a>请参阅
- [Visual Studio 文档](https://docs.microsoft.com/visualstudio/)
- [Azure DevOps 文档](https://docs.microsoft.com/azure/devops/)
- [Azure 文档](https://docs.microsoft.com/azure/)
- [Microsoft 365 文档](https://docs.microsoft.com/microsoft-365/)

## <a name="next-steps"></a>后续步骤
- 需要更改订阅而不删除它？  了解如何[编辑订阅](edit-license.md)
- 有关查找特定订阅的帮助，请查阅[搜索订阅](search-license.md)。
- 需要创建所有订阅的列表？  请参阅[导出订阅](exporting-subscriptions.md)。


