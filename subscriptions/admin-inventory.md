---
title: 清点预生产环境 | Visual Studio Marketplace
author: evanwindom
ms.author: lank
manager: lank
ms.date: 02/17/2020
ms.topic: conceptual
description: 了解管理员管理预生产库存的职责
ms.openlocfilehash: 0eacd177b0901d866bbb974aca81a0e77cdaf25d
ms.sourcegitcommit: e3b9cbeea282f1b531c6a3f60515ebfe1688aa0e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/18/2020
ms.locfileid: "77439110"
---
# <a name="inventory-of-pre-production-environment"></a>清点预生产环境
Visual Studio 订阅对用户而非设备计数，从而简化了资产管理。

Visual Studio 管理员必须将 Visual Studio 订阅分配给**特定的指定人员**。 不允许使用诸如 Dev1、Dev2 之类的命名约定，也不允许使用诸如“FeatureTeam”之类的团队名称  。

下面是一些简化预生产环境清点过程的方法：
- 检查用户分配。 Microsoft 提供名为 [Visual Studio 管理门户](https://manage.visualstudio.com/)的网站，帮助你跟踪 Visual Studio 订阅分配。
- 使用本地或基于云的 Active Directory 列出用户。 如果使用 Active Directory 管理用户访问权限，可能能够根据目录成员身份识别开发用户和测试用户。
- 使用自动化工具清点系统。 可能还需要使用软件清点工具，帮助管理软件资产以及区分预生产环境与生产环境。 许多拥有 Microsoft System Center 的客户会创建命名约定，帮助在清点过程中自动处理这部分内容。
- 以手动核对的方式获得帮助。 让员工参与进来，帮助核对开发和测试用户与开发和测试环境。

## <a name="resources"></a>资源
- [Visual Studio 授权白皮书](https://visualstudio.microsoft.com/wp-content/uploads/2019/06/Visual-Studio-Licensing-Whitepaper-May-2019.pdf)
- [Visual Studio 管理和订阅支持](https://visualstudio.microsoft.com/support/support-overview-vs)
- [批量许可条款](https://www.microsoft.com/licensing/product-licensing/products.aspx)

## <a name="next-steps"></a>后续步骤
详细了解管理员的职责：
- [管理员职责](admin-responsibilities.md)
- [管理大型团队和外部承包商](manage-teams.md)
- [跟踪用户分配和处理订单](assignments-orders.md)
- 使用[最大用量](maximum-usage.md)跟踪购买承诺

## <a name="see-also"></a>请参阅
- [Visual Studio 文档](/visualstudio/)
- [Azure DevOps 文档](/azure/devops/)
- [Azure 文档](/azure/)
- [Microsoft 365 文档](/microsoft-365/)
