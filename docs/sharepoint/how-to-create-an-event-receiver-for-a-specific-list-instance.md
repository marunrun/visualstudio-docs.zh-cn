---
title: 如何：创建事件接收器的特定列表实例 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, event receivers
- event receivers [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 34114c12ef47fb796de7354aa3133af1fc704267
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63408559"
---
# <a name="how-to-create-an-event-receiver-for-a-specific-list-instance"></a>如何：创建事件接收器的特定列表实例
  列表实例事件接收方响应的列表定义的任何实例中发生的事件。 虽然事件接收方模板不会启用特定列表实例的目标，你可修改的范围限定为列表定义以响应特定列表实例中的事件的事件接收器。

 若要在面向特定列表实例， *Elements.xml*对于事件接收器中，将为`ListTemplateId`与`ListUrl`和添加列表实例的 URL。

## <a name="create-a-list-instance-event-receiver"></a>创建列表实例事件接收器
 以下步骤说明如何修改列表项事件接收方仅对自定义公告列表实例中发生的事件作出响应。

#### <a name="to-modify-an-event-receiver-to-respond-to-a-specific-list-instance"></a>若要修改事件接收器以响应特定列表实例

1. 在浏览器中打开 SharePoint 网站。

2. 在导航窗格中，**列出了**链接。

3. 在中**所有网站内容**页上，选择**创建**链接。

4. 在中**创建**对话框框中，选择**公告**类型，将公告命名**TestAnnouncements**，然后选择**创建**按钮。

5. 在[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]，创建一个事件接收器项目。

6. 在中**所需哪种类型的事件接收器？** 列表中，选择**列表项事件**。

    > [!NOTE]
    > 您还可以选择任何其他类型的范围限于列表定义，例如，事件接收器**列出的电子邮件事件**或**列出的工作流事件**。

7. 在中**哪个项应为事件源？** 列表中，选择**公告**。

8. 在中**处理以下事件**列表中，选择**添加项**复选框，，然后选择**完成**按钮。

9. 在中**解决方案资源管理器**，EventReceiver1，下打开*Elements.xml*。

     事件接收器当前使用以下行来引用公告列表定义：

    ```xml
    <Receivers ListTemplateId="104">
    ```

     将此行更改为以下文本：

    ```xml
    <Receivers ListUrl="Lists/TestAnnouncements">
    ```

     这会指示只应对发生在新的事件的事件接收器**TestAnnouncements**刚创建的公告列表。 您可以更改`ListURL`属性来引用 SharePoint 服务器上的任何列表实例。

10. 打开代码文件，事件接收器和 ItemAdding 方法中放置一个断点。

11. 选择**F5**键生成并运行解决方案。

12. 在 SharePoint 中，选择**TestAnnouncements**导航窗格。

13. 选择**添加新公告**链接。

14. 了解相关公告中，输入一个标题，然后选择**保存**按钮。

     请注意，新项添加到自定义公告列表时命中断点。

15. 选择**F5**键以继续。

16. 在导航窗格中，选择**列出了**链接，，然后选择**公告**链接。

17. 添加新公告。

     请注意，在新的公告不会触发的事件接收器，因为接收方已配置为仅在自定义公告列表实例中，事件响应**TestAnnouncements**。

## <a name="see-also"></a>请参阅
- [如何：创建事件接收器](../sharepoint/how-to-create-an-event-receiver.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
