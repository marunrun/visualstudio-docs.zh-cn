---
title: 将许可证分配给 Visual Studio 订阅的用户组 | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.date: 07/24/2019
ms.topic: conceptual
description: 了解管理员如何将许可证分配给多个订阅者
ms.openlocfilehash: 7d54dcf3cf3e7fea7845a4e9a0053de4ba734ae9
ms.sourcegitcommit: ce1ab8a25c66a83e60eab80ed8e1596fe66dd85c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2019
ms.locfileid: "68610517"
---
# <a name="assign-subscriptions-to-multiple-users"></a>将订阅分配给多个用户
你可以在订阅管理门户中一次添加一个多个用户，也可以采用大用户组形式添加。  要添加各个用户，请参阅[添加单个用户](assign-license.md)。

## <a name="use-bulk-add-to-assign-subscriptions"></a>使用批量添加分配订阅
1. 登录 Visual Studio 订阅管理门户，网址： https://manage.visualstudio.com 。
2. 若要一次添加多个订阅者，请导航到“管理订阅者”选项卡  。在顶部功能区，单击“批量添加”  。
   > [!div class="mx-imgBorder"]
   > ![添加多个订阅者](media/add-multiple-subscribers.png)

2. 批量添加会使用 Microsoft Excel 模板上传订阅者信息。 在“上传多个订阅者”对话框中，单击“下载”下载模板  。
   > [!div class="mx-imgBorder"]
   > ![下载 Excel 模板以上传多个订阅者](media/download-template-upload-subscribers.png)
   >
   > [!NOTE]
   > 请务必下载本模板的最新版本。 如果使用旧版本，批量上传可能会失败。

3. 在 Excel 电子表格的字段中，填写想要为其分配订阅的个人的信息。 （“引用”是可选字段。  ）完成后将文件保存在本地。

   为顺利地完成上传，请查看以下最佳做法：

    - 确保所有表单域均不含逗号。
    - 删除表单域前后的空格。
    - 确保用户名在名字和姓氏两部分之间不含额外空格（例如，用户姓名为两部分的“Maggie May”，则应输成“MaggieMay”，因为系统不会删减额外空格）。

4. 返回到 Visual Studio 订阅管理门户。 在“上传多个订阅者”对话框中，单击“浏览”   。
   > [!div class="mx-imgBorder"]
   > ![浏览到之前保存的模板以上传多个订阅者](media/bulk-add-browse-saved-template.png)

5. 导航到之前保存的 Excel 文件，然后单击“确定”  。
   > [!div class="mx-imgBorder"]
   > ![上传 Excel 模板以上传多个订阅者](media/bulk-upload-subscribers.png)

    将显示上传进度对话框。

    如果模板中存在错误，则无法上传。系统会显示该错误，你可以更正模板，然后再次尝试批量上传。
   > [!div class="mx-imgBorder"]
   > ![如果上传多个订阅者失败，将显示错误消息](media/bulk-add-template-failed.png)

    上传成功后，系统会显示订阅者列表和一条确认消息。
   > [!div class="mx-imgBorder"]
   > ![如果上传多个订阅者成功，将显示确认消息](media/bulk-add-template-success.png)

## <a name="next-steps"></a>后续步骤
- 只有一两个订阅者要添加？  请查阅[添加单个用户](assign-license.md)
- 了解如何[编辑](edit-license.md)现有订阅
- 需要帮助？ 联系 [Visual Studio 管理和订阅支持](https://visualstudio.microsoft.com/support/support-overview-vs)。
