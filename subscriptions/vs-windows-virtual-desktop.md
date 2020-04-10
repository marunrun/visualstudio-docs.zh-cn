---
title: Visual Studio 订阅中的 Microsoft Windows 虚拟桌面权益 | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.assetid: 872c5746-5357-4764-949b-aa525a0adf1a
ms.date: 04/01/2020
ms.topic: conceptual
description: 了解如何通过 Visual Studio 订阅利用 Microsoft Windows 虚拟桌面
ms.openlocfilehash: 3954a3e86c319b8d433e509a8b283201c3313410
ms.sourcegitcommit: 054815dc9821c3ea219ae6f31ebd9cd2dc8f6af5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2020
ms.locfileid: "80573081"
---
# <a name="access-windows-virtual-desktop-in-subscriptions"></a>在订阅中访问 Windows 虚拟桌面 
Visual Studio 订阅者现在可以将其 Azure 开发/测试个人额度用于 Microsoft Windows 虚拟桌面服务。  
Windows 虚拟桌面是在云中运行的综合性桌面和应用虚拟化服务。 这是唯一一种可提供简化管理、多会话 Windows 10、对 Office 365 专业增强版的优化以及对远程桌面服务 (RDS) 环境的支持的虚拟桌面基础结构 (VDI)。 只需几分钟即可在 Azure 上部署和缩放 Windows 桌面和应用，并获得内置的安全性和符合性功能。
下面是在 Azure 中运行 Windows 虚拟桌面时可以执行的操作：
- 设置多会话 Windows 10 部署，使整个 Windows 10 操作系统获得可伸缩性
- 虚拟化 Office 365 ProPlus，并将其优化为可在多用户虚拟方案中运行
- 为 Windows 7 虚拟桌面提供免费的扩展安全更新
- 将现有的远程桌面服务 (RDS) 和 Windows Server 桌面与应用迁移到任何计算机
- 虚拟化桌面和应用
- 使用统一的管理体验管理 Windows 10、Windows Server 和 Windows 7 桌面与应用。有关可以使用 Windows 虚拟桌面执行哪些操作的详细信息，请观看[介绍视频](https://docs.microsoft.com/azure/virtual-desktop/overview)。

## <a name="use-windows-virtual-desktop-with-azure"></a>将 Windows 虚拟桌面与 Azure 配合使用 
Visual Studio 订阅者现在可通过多种方法使用 Azure 订阅为 Windows 虚拟桌面服务付费：
- [Azure 开发测试个人额度](vs-azure.md)。  在订阅中获得 Azure 开发测试个人额度的订阅者可以使用这些额度为 Windows 虚拟桌面服务付费。  每月额度量取决于订阅级别。
- [Azure 开发测试即用即付订阅](vs-azure-payg.md)。  可以创建 Azure 订阅并附加付款方式，以便以无缝方式为 Windows 虚拟桌面使用情况付费。 
- [Azure 企业协议开发测试套餐](azure-ea-devtest.md)。  通过此套餐，具有企业协议的订阅者可以按折扣定价通过 Azure 为 Windows 虚拟桌面付费。 

## <a name="requirements"></a>要求
Windows 虚拟桌面需要 Azure Active Directory (Azure AD)，VM 将加入到其中。  用户必须是此 Azure AD 的成员。  可通过两个选项实现 Azure AD：
- Azure AD Directory 服务。  对于大多数用户而言，这是较简单的实现选项。
- 运行域控制器提升的虚拟机。  此选项需要执行更多设置工作，但大多数用户的操作成本更低。
若要查看使用 Windows 虚拟桌面的先决条件的完整列表，请访问 Windows 虚拟桌面[概述页](https://docs.microsoft.com/azure/virtual-desktop/overview#requirements)。 

## <a name="get-started"></a>入门 
满足所有先决条件后，将需要完成几项操作来完成实现。  请查看以下入门教程：
- [创建 Windows 虚拟桌面租户](https://docs.microsoft.com/azure/virtual-desktop/tenant-setup-azure-active-directory)
- 使用 Azure 门户[创建主机池](https://docs.microsoft.com/azure/virtual-desktop/create-host-pools-azure-marketplace)
- [管理 Windows 虚拟桌面的应用组](https://docs.microsoft.com/azure/virtual-desktop/manage-app-groups)

## <a name="eligibility"></a>资格
| 订阅级别                                                 |     信道                                            | 好处                                                          | 是否续订？    |
|--------------------------------------------------------------------|---------------------------------------------------------|------------------------------------------------------------------|---------------|
| Visual Studio Enterprise（标准）   | VL、Azure、零售、 | 可用|  是          |
| 带有 GitHub Enterprise 的 Visual Studio Enterprise  | VL | 可用|  是          |
| Visual Studio Professional（标准） | VL、Azure、零售                                       | 可用                                                             |  是             |
| 带有 GitHub Enterprise 的 Visual Studio Professional | VL                                       | 可用                                        |  是           |
| Visual Studio Test Professional（标准）                         | VL、零售                                              | 可用|  是          |
| MSDN 平台（标准）                                          | VL、零售                                              | 可用                                         |  是          |
| Visual Studio Enterprise（标准）  | NFR<sup>1</sup> |不可用  | 不可用 |
| Visual Studio Enterprise、Visual Studio Professional（月度云） | Azure | 不可用 | 不可用 |

<sup>1</sup>  包括：  不得转售 (NFR)、FTE、最有价值专家 (MVP)、区域总监 (RD)、Microsoft 合作伙伴网络 (MPN)、Visual Studio 行业合作伙伴 (VSIP)、Microsoft 认证培训师、BizSpark、Imagine

> [!NOTE]
> Microsoft 不再在云订阅中提供 Visual Studio Professional 年度订阅和 Visual Studio Enterprise 年度订阅。 现有客户体验以及续订、增加、减少或取消订阅的能力不会发生变化。 建议新客户访问 [https://visualstudio.microsoft.com/vs/pricing/](https://visualstudio.microsoft.com/vs/pricing/)，查看各 Visual Studio 购买选项。

无法确定正在使用哪些订阅？  连接到 [https://my.visualstudio.com/subscriptions](https://my.visualstudio.com/subscriptions?wt.mc_id=o~msft~docs)，查看分配给电子邮件地址的所有订阅。 如果没有看到所有订阅，则可能是有一个或多个订阅分配给了不同的电子邮件地址。  你需要使用其他电子邮件地址登录来查看那些订阅。

## <a name="see-also"></a>请参阅
- [Azure 文档](https://docs.microsoft.com/azure/)
- [Windows 虚拟桌面文档](https://docs.microsoft.com/azure/virtual-desktop/)

## <a name="next-steps"></a>后续步骤
-   如果需要购买 Visual Studio 订阅，请查看：
     - 通过 Microsoft Store [购买的零售定价](https://visualstudio.microsoft.com/vs/pricing/)
     - [批量许可计划](https://www.microsoft.com/licensing/default)
-   了解 [Windows 虚拟桌面](https://docs.microsoft.com/azure/virtual-desktop/overview) 
