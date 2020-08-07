---
title: 在管理门户中编辑订阅 | Microsoft Docs
author: evanwindom
ms.author: lank
manager: cabuschl
ms.assetid: 97ac8e4d-7a03-42f8-98cb-15bcaa90ef65
ms.date: 07/30/2020
ms.topic: how-to
description: 了解管理员如何编辑订阅分配。
ms.openlocfilehash: fb43f9ceae86acf5804a6cd32dd383dcd2e9af38
ms.sourcegitcommit: b8ec700fc4c14c68c6ce280f29c19870261990d8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2020
ms.locfileid: "87453731"
---
# <a name="edit-visual-studio-subscription-assignments"></a>编辑 Visual Studio 订阅分配
作为订阅管理员，可以更改分配给组织内个人的订阅。  本文讨论可以进行更改的类型并提供必要的步骤。

   > [!NOTE]
   > 如果需要更改通过 Azure Active Directory 组分配的订阅者的订阅详细信息，则需要将其从组中删除，并将他们分别添加到管理门户。  

## <a name="change-subscriber-information"></a>更改订阅者信息
可以编辑订阅者的信息来更正错误或更新信息。

若要对订阅者进行编辑，请在鼠标悬停在订阅者的电子邮件地址旁时，选择出现的省略号 (…)。 此时将显示下拉列表。  选择“编辑”  ，以修改订阅者的详细信息。 
> [!div class="mx-imgBorder"]
> ![选择要对其进行编辑的订阅者](_img/edit-license/select-subscriber.png "单击省略号，然后选择“编辑”。")

可以更新订阅者的名字、姓氏、订阅级别、电子邮件地址、国家/地区、语言、下载和引用字段。 编辑订阅者的信息，然后单击“保存”  。

## <a name="edit-multiple-subscribers-using-bulk-edit"></a>使用批量编辑对多个订阅者进行编辑


可使用批量编辑进程一次编辑多个订阅者。 此功能主要用于正在更改公司电子邮件地址的组织，或者决定对下载进行限制的组织。

<br>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4vkAF]

   > [!IMPORTANT]
   > 订阅级别（即 Enterprise、Professional 等）和订阅 GUID 无法使用批量编辑进行更改。  如果需要向用户分配特定的订阅 GUID，请使用通过选择订阅 ID 添加用户的过程。 如果尝试上传批量编辑模板中的这些更改项，上传将失败。

1. 若要一次编辑多个订阅者，请导航到“订阅者”选项卡。在顶部功能区中，单击“批量编辑”  。

2. 批量编辑使用 Excel 模板编辑订阅者信息。 在“批量编辑”框中，单击“导出此 excel”，以下载当前包含其所有信息的订阅者列表  。
   > [!div class="mx-imgBorder"]
   > ![编辑许可证 - 导出批量编辑列表](_img/edit-license/edit-license-bulk-edit-export.png "单击“导出此 excel”以创建当前订阅的列表。")

3. 接下来，将文件保存到本地，以便能够轻松找到该文件，并在上传之前对其进行必要的更改。 为确保上传成功，请勿在批量编辑文件中编辑订阅级别或订阅 GUID  ，否则会导致上传失败。

4. 返回到 Visual Studio 订阅管理门户，在“批量编辑”对话框中，单击“浏览”  。 选择之前保存的 Excel 文件，然后单击“确定”  。 屏幕上随即显示上传进度。
   > [!div class="mx-imgBorder"]
   > ![编辑许可证 - 批量编辑文件上传](_img/edit-license/edit-license-bulk-file-upload1.png "浏览到已完成的 Excel 文件的位置，选择该文件，然后单击“确定”。")

5. 文件上传后，将看到上传成功的通知。 此时，编辑将反映到订阅者信息当中。

## <a name="see-also"></a>请参阅
- [Visual Studio 文档](https://docs.microsoft.com/visualstudio/)
- [Azure DevOps 文档](https://docs.microsoft.com/azure/devops/)
- [Azure 文档](https://docs.microsoft.com/azure/)
- [Microsoft 365 文档](https://docs.microsoft.com/microsoft-365/)

## <a name="next-steps"></a>后续步骤
- 是否需要分配特定订阅 ID？ 请查看分配订阅 ID。 
- 有关查找特定订阅的帮助，请查阅[搜索订阅](search-license.md)。
- 需要创建所有订阅的列表？  请查阅[导出订阅](exporting-subscriptions.md)。
