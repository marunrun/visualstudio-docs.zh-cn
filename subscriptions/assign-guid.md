---
title: 向 Visual Studio 订阅者分配特定 GUID | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.date: 04/20/2020
ms.topic: conceptual
description: 了解管理员如何将特定订阅 GUID 分配给订阅者
ms.openlocfilehash: e2e8cd4f5d07f218fc23c0b7b6f28ababc25263f
ms.sourcegitcommit: 0b8497b720eb06bed8ce2194731177161b65eb84
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "82072588"
---
# <a name="assign-specific-subscriptions-in-the-visual-studio-subscriptions-administration-portal"></a>在 Visual Studio 订阅管理门户中分配特定订阅

管理员现可使用 Visual Studio 订阅管理门户为个人用户分配订阅。  在组织具有需要短期访问订阅的临时员工或供应商的情况下，这非常有用。  管理员可以分配已部分使用的订阅，让其新订阅的使用时间更长一点。  

<br>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4t4cl]


## <a name="assign-specific-subscription-guids-to-users"></a>向用户分配特定的订阅 GUID

向个人分配特定订阅的过程涉及利用两个现有的管理流程将特定订阅全局唯一标识符 (GUID) 分配给单个用户。  这一过程包括以下三步：首先导出当前订阅和分配的列表，然后使用该列表标识要分配的特定 GUID，最后使用批量添加过程上传新分配。

### <a name="export-your-subscriptions-information"></a>导出订阅信息

要执行导出，请按照以下步骤操作：
1. 登录[管理门户](https://manage.visualstudio.com)。
2. 选择“导出”选项卡，文件将下载到本地计算机  。 该文件将包含用户订阅所在的协议名称以及导出日期。
> [!div class="mx-imgBorder"]
> ![导出订阅者](_img/exporting-subscriptions/exporting-subscriptions.png)

### <a name="identify-the-guids-you-want-to-assign"></a>确定要分配的 GUID

如果以前使用过“导出”工具，你就会发现新字段已添加到生成的电子表格中。  这些字段将有助于你确定每个订阅的状态以及要分配给用户的订阅的状态。  

- **订阅状态**：此字段将指示“已分配”或“未分配”。  如果订阅的状态为“已分配”，则该订阅还将具有与其关联的用户信息，如姓名、电子邮件等。 
- **使用状态**：使用状态将指示“新”和“已使用”，前者指示它从未分配给用户，后者指示它已在某个时间点分配给了用户。  

你可以使用这些字段中的值以及电子表格中的其他信息来确定要分配给单个用户的订阅。 可以在 Excel 中应用筛选器，以帮助按状态、订阅级别、到期日期等缩小列表范围。 

### <a name="upload-your-new-assignments"></a>上传新分配

最后一步是下载**批量添加**模板，填写要分配的订阅所需的信息，然后上传模板。  有关该过程的完整说明，请参阅[添加多个用户](assign-license-bulk.md)一文。  

> [!IMPORTANT]
> 为确保成功上传，请确保：
> - 在选择“批量添加”时使用对话框中链接的模板  。  请勿使用本地存储的模板副本，因为它可能未包含所有必填字段。  使用旧模板会导致上传失败。 
> - 模板中所有显示为“必填”的字段都已填充  。
> - “错误消息”列中未列出任何错误  。
> - 每个 GUID 在模板中只使用一次。 
> - 模板中的订阅级别与导出列表中 GUID 的订阅匹配。 
> - GUID 尚未分配给导出列表中的其他用户。 

## <a name="frequently-asked-questions"></a>常见问题
### <a name="qhow-do-i-change-which-subscription-is-currently-assigned-to-an-individual-user"></a>问：如何更改当前分配给单个用户的订阅？
答：如果要更改分配给用户的 GUID，必须首先删除该用户的订阅。  有关详细信息，请参阅[删除订阅](delete-license.md)一文。  删除该用户的订阅后，请使用上述过程导出列表并上传新的订阅信息。  

## <a name="see-also"></a>请参阅
- [Visual Studio 文档](/visualstudio/)
- [Azure DevOps 文档](/azure/devops/)
- [Azure 文档](/azure/)
- [Microsoft 365 文档](/microsoft-365/)

## <a name="next-steps"></a>后续步骤
现在，你已为用户分配了订阅，接下来了解如何执行其他管理任务。
- [分配单个订阅](assign-license.md)
- [分配多个订阅](assign-license-bulk.md)
- [编辑订阅](edit-license.md)
- [删除订阅](delete-license.md)
- [确定最大使用量](maximum-usage.md)


