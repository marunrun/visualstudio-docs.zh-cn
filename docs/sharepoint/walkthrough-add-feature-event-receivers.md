---
title: 演练：添加功能事件接收器 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, advanced packaging tools
- SharePoint development in Visual Studio, event receivers
- SharePoint development in Visual Studio, feature event receivers
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0fc22e0c8ae0b0bdaf0729b3cdb3847cd25f580f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63008195"
---
# <a name="walkthrough-add-feature-event-receivers"></a>演练：添加功能事件接收器
  功能事件接收器是在 SharePoint 中与功能相关的以下事件之一发生时执行的方法：

- 安装一项功能。

- 激活某个功能。

- 一项功能将停用。

- 删除一项功能。

  本演练演示如何将事件接收器添加到 SharePoint 项目中的功能。 它演示了以下任务：

- 使用功能事件接收器创建空项目。

- 处理**FeatureDeactivating**方法。

- 使用 SharePoint 项目对象模型添加到公告列表的公告。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- 支持的 Microsoft Windows 和 SharePoint 版本。

- Visual Studio。

## <a name="create-a-feature-event-receiver-project"></a>创建功能事件接收器项目
 首先，创建一个项目以包含的功能事件接收器。

#### <a name="to-create-a-project-with-a-feature-event-receiver"></a>若要使用的功能事件接收器创建项目

1. 在菜单栏上依次选择**文件** > **新建** > **项目**显示**新建项目**对话框。

2. 展开**SharePoint**节点下的**Visual C#** 或**Visual Basic**，然后选择**2010年**节点。

3. 在中**模板**窗格中，选择**SharePoint 2010 项目**模板。

     您的功能事件接收器使用此项目类型，因为它们没有项目模板。

4. 在中**名称**框中，输入**FeatureEvtTest**，然后选择**确定**按钮以显示**SharePoint 自定义向导**。

5. 上**指定用于调试的网站和安全级别**页上，输入你想要添加的新的自定义字段项的 SharePoint 服务器站点的 URL 或使用默认位置 (http://\<*系统名称*> /)。

6. 在中**此 SharePoint 解决方案的信任级别是什么？** 部分中，选择**部署为场解决方案**选项按钮。

     有关沙盒解决方案与场解决方案的详细信息，请参阅[沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

7. 选择**完成**按钮，然后请注意，显示下一项功能，名为 Feature1**功能**节点。

## <a name="add-an-event-receiver-to-the-feature"></a>向功能添加事件接收器
 接下来，向功能添加事件接收器，并添加停用功能时执行的代码。

#### <a name="to-add-an-event-receiver-to-the-feature"></a>若要添加到功能事件接收器

1. 打开功能节点的快捷菜单，然后选择**添加功能**创建一项功能。

2. 下**功能**节点，打开快捷菜单**Feature1**，然后选择**添加事件接收器**将事件接收器添加到该功能。

     这会添加下 Feature1 的代码文件。 在这种情况下，它名为任一*Feature1.EventReceiver.cs*或*Feature1.EventReceiver.vb*，取决于你的项目的开发语言。

3. 如果你的项目以[!INCLUDE[csprcs](../sharepoint/includes/csprcs-md.md)]，如果尚不存在的事件接收器的顶部添加以下代码：

     [!code-csharp[SP_FeatureEvt#1](../sharepoint/codesnippet/CSharp/featureevttest2/features/feature1/feature1.eventreceiver.cs#1)]

4. 事件接收器类包含多个注释掉的方法，后者将作为事件。 替换**FeatureDeactivating**使用以下方法：

     [!code-vb[SP_FeatureEvt#2](../sharepoint/codesnippet/VisualBasic/featureevt2vb/features/feature1/feature1.eventreceiver.vb#2)]
     [!code-csharp[SP_FeatureEvt#2](../sharepoint/codesnippet/CSharp/featureevttest2/features/feature1/feature1.eventreceiver.cs#2)]

## <a name="test-the-feature-event-receiver"></a>测试功能事件接收器
 接下来，停用功能来测试是否**FeatureDeactivating**方法输出到 SharePoint 公告列表的公告。

#### <a name="to-test-the-feature-event-receiver"></a>若要测试的功能事件接收器

1. 将项目的值设置**活动部署配置**属性设置为**无激活**。

     设置此属性可防止功能在 SharePoint 中激活，并使你能够调试功能事件接收器。 有关详细信息，请参阅[调试 SharePoint 解决方案](../sharepoint/debugging-sharepoint-solutions.md)。

2. 选择**F5**键以运行该项目并将其部署到 SharePoint。

3. 在 SharePoint Web 页的顶部，打开**站点操作**菜单，然后选择**站点设置**。

4. 下**站点操作**一部分**站点设置**页上，选择**管理站点功能**链接。

5. 上**功能**页上，选择**激活**按钮旁边**FeatureEvtTest Feature1**功能。

6. 上**功能**页上，选择**停用**按钮旁边**FeatureEvtTest Feature1**功能，然后选择**停用此功能**确认链接来停用功能。

7. 选择**主页**按钮。

     请注意，在中会显示一个通知**公告**列表后停用功能。

## <a name="see-also"></a>请参阅

- [如何：创建事件接收器](../sharepoint/how-to-create-an-event-receiver.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)