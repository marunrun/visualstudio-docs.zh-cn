---
title: 如何：为特定列表实例创建事件接收器 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: 54c384742afba3d5af7f08ee62a9ec56c7f1438c
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016966"
---
# <a name="how-to-create-an-event-receiver-for-a-specific-list-instance"></a>如何：为特定列表实例创建事件接收器
  列表实例事件接收器对在列表定义的任何实例中发生的事件做出响应。 尽管事件接收器模板不启用特定列表实例的目标，但你可以修改作用域为列表定义的事件接收器，以响应特定列表实例中的事件。

 若要针对特定列表实例，请在事件接收器的*Elements.xml*中将替换 `ListTemplateId` 为， `ListUrl` 并添加列表实例的 URL。

## <a name="create-a-list-instance-event-receiver"></a>创建列表实例事件接收器
 以下步骤演示如何修改列表项事件接收器，以便仅响应在自定义公告列表实例中发生的事件。

#### <a name="to-modify-an-event-receiver-to-respond-to-a-specific-list-instance"></a>修改事件接收器以响应特定的列表实例

1. 在浏览器中打开 SharePoint 网站。

2. 导航窗格中的 "**列表**" 链接。

3. 在 "**所有网站内容**" 页上，选择 "**创建**" 链接。

4. 在 "**创建**" 对话框中，选择 "**公告**" 类型，为公告**TestAnnouncements**命名，然后选择 "**创建**" 按钮。

5. 在中 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，创建一个事件接收器项目。

6. 在 "**要执行哪种类型的事件接收器？"** 列表中，选择 "**列表项事件**"。

    > [!NOTE]
    > 你还可以选择作用域到列表定义的任何其他类型的事件接收器，例如，**列出电子邮件事件**或**列表工作流事件**。

7. 在 "**哪个项应为事件源？"** 列表中，选择 "**公告**"。

8. 在 "**处理以下事件**" 列表中，选中 "**要添加的项**" 复选框，然后选择 "**完成**" 按钮。

9. 在**解决方案资源管理器**的 "EventReceiver1" 下，打开*Elements.xml*。

     事件接收器当前使用以下行来引用公告列表定义：

    ```xml
    <Receivers ListTemplateId="104">
    ```

     将此行更改为以下文本：

    ```xml
    <Receivers ListUrl="Lists/TestAnnouncements">
    ```

     这会指示事件接收器仅响应刚创建的新**TestAnnouncements**公告列表中发生的事件。 您可以更改该 `ListURL` 属性以引用 SharePoint 服务器上的任何列表实例。

10. 打开事件接收器的代码文件，并在 ItemAdding 方法中添加一个断点。

11. 选择**F5**键生成并运行解决方案。

12. 在 SharePoint 中，在导航窗格中选择 " **TestAnnouncements** " 链接。

13. 选择 "**添加新公告**" 链接。

14. 输入公告的标题，然后选择 "**保存**" 按钮。

     请注意，当新项添加到自定义公告列表中时，将命中该断点。

15. 选择**F5**键以继续。

16. 在导航窗格中，选择 "**列表**" 链接，然后选择 "**公告**" 链接。

17. 添加新公告。

     请注意，由于接收方配置为仅响应自定义公告列表实例**TestAnnouncements**中的事件，因此事件接收器不会在新公告上触发。

## <a name="see-also"></a>另请参阅
- [如何：创建事件接收器](../sharepoint/how-to-create-an-event-receiver.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
