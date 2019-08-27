---
title: 创建 Outlook 窗体区域
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- MICROSOFT.OFFICE.TOOLS.OUTLOOK.FORMREGION
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio]
- form regions [Office development in Visual Studio], creating
- Outlook [Office development in Visual Studio], form regions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: dc0f56331c11c6c33561774d38ef79e286a4133a
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63445569"
---
# <a name="create-outlook-form-regions"></a>创建 Outlook 窗体区域
  窗体区域可用于自定义 Microsoft Office Outlook 窗体。 Visual Studio 提供了高级工具，可使你更轻松地设计、开发和调试窗体区域。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

 本主题提供以下信息：

- [使用窗体区域的优点](#Enhance)

- [将 Outlook 窗体区域添加到你的项目](#Adding)

- [使用窗体区域设计器](#UsingFormRegionDesigner)

- [使用在 Outlook 中设计的窗体区域](#UsingFormRegionDesignedOutlook)

- [将自定义代码添加到窗体区域](#AddingCustomCode)

- [生成项目](#Building)

- [调试窗体区域](#Debugging)

- [部署窗体区域](#Deploying)

## <a name="Enhance"></a> 使用窗体区域的优点
 相较于传统的 Outlook 窗体开发，窗体区域提供了许多增强功能：

- 自定义任何标准窗体的默认页。

- 将多达 12 个额外页面添加到任何标准窗体。

- 替换或增强任何标准窗体。

- 在阅读窗格和检查器中显示自定义 UI。

  有关详细信息，请参阅[自定义窗体页和窗体区域](/office/vba/outlook/Concepts/Forms/customizing-form-pages-and-form-regions)。

## <a name="Adding"></a> 将 Outlook 窗体区域添加到你的项目
 可以使用**新建 Outlook 窗体区域**向导来设计新的窗体区域或导入在 Outlook 中设计的窗体区域。 此外，如果有在其他 Outlook VSTO 外接程序项目中使用的窗体区域，则可以重新使用现有的窗体区域。

### <a name="CreatingFormRegion"></a> 使用向导创建新的窗体区域
 若要创建的窗体区域，添加**Outlook 窗体区域**向 Outlook VSTO 外接程序项目的项。 这将启动**新建 Outlook 窗体区域**向导。

 使用向导来指示是要设计新的窗体区域还是导入在 Outlook 中设计的窗体区域。 有关设计新的窗体区域的详细信息，请参阅[使用的窗体区域设计器](#UsingFormRegionDesigner)。 有关使用在 Outlook 中设计的窗体区域的详细信息，请参阅[导入在 Outlook 中设计的窗体区域](#UsingFormRegionDesignedOutlook)。

 使用向导来指定要创建的窗体区域类型。 下表介绍每种窗体区域类型。

|区域类型|描述|
|-----------------|-----------------|
|独立|将窗体区域作为新页添加到 Outlook 窗体中。|
|相邻|将窗体区域附加到 Outlook 窗体的默认页的底部。|
|Replacement|将窗体区域作为替换 Outlook 窗体默认页的新页添加。|
|全部替换|使用窗体区域替换整个 Outlook 窗体。|

 也可使用向导来指定显示条件及选择要扩展的窗体类型。 有关详细信息，请参阅[如何：向 Outlook 外接程序项目添加窗体区域](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)。

 在向导中所做的选择将影响其他向导页中可用的选项。 例如，如果您选择**相邻**或**单独**中**创建新的 Outlook 窗体区域**页上，则**标题**和**说明**字段中都不可用**提供说明性文本并选择显示首选项**页。 这是因为 Outlook 在显示相邻或独立的窗体区域时并不使用这些字段。

#### <a name="form-region-files"></a>窗体区域文件
 完成后**新建 Outlook 窗体区域**向导、 Visual Studio 会自动将以下文件添加到你的项目：

- 窗体区域代码文件。 此文件的名称为指定的名称**Outlook 窗体区域**中的项**添加新项**对话框。 向此文件添加用于处理窗体区域事件的代码。

- 窗体区域设计器代码文件。 此文件包含窗体区域设计器生成的代码，不应直接对其进行编辑。

- Outlook 窗体存储 (*.ofs*) 文件。

    > [!NOTE]
    > 如果导入在 Outlook 中设计的窗体区域，那么仅将此文件添加到项目。

#### <a name="form-region-factory-class"></a>窗体区域工厂类
 窗体区域代码文件包含实现 <xref:Microsoft.Office.Tools.Outlook.IFormRegionFactory> 接口的分部类。 这是窗体区域工厂类。 窗体区域工厂类负责创建窗体区域的新实例。

 可以通过展开来找到此类**窗体区域工厂**区域。

 **新建 Outlook 窗体区域**向导将属性添加到此类的指定窗体区域的内部名称和显示窗体区域的邮件类。 将文件添加到项目中后，可手动修改这些特性。

 大部分窗体区域工厂类在窗体区域设计器文件中实现。 但是，`FormRegionInitializing` 事件处理程序在窗体区域代码文件中公开。 可使用此事件处理程序来指定 Outlook 是否应显示窗体区域。 有关详细信息，请参阅[处理窗体区域事件](#HandlingFormRegionEvents)。

### <a name="AddingExistingFormRegion"></a> 将现有的窗体区域添加到你的项目
 如果具有在其他 Outlook 项目中使用的 Outlook 窗体区域，可通过使用 **“添加现有项”** 对话框在当前 Outlook VSTO 外接程序项目中重新使用它。

 现有的窗体区域必须具有代码文件 (*.vb*或 *.cs*); 不能添加 Outlook 窗体存储 (*.ofs*) 通过使用文件**添加现有项**对话框。 但是，可通过导入 Outlook 窗体存储文件来创建新的窗体区域。 有关详细信息，请参阅[如何：向 Outlook 外接程序项目添加窗体区域](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)。

## <a name="UsingFormRegionDesigner"></a> 使用窗体区域设计器
 窗体区域设计器可帮助你设计窗体区域的布局和外观。 可以将托管的控件拖到设计器图面中，双击控件以打开事件处理程序，然后中设置属性**属性**窗口。

> [!NOTE]
> 您可以找到影响窗体区域在下方的 Outlook 中的显示的方式的属性**清单**中的节点**属性**窗口。

 仅当你在 **“新建 Outlook 窗体区域”** 向导的 **“选择窗体区域的创建方式”** 页中选择 **“设计新的窗体区域”** 时，窗体区域设计器才可用。

 可通过三种方法打开窗体区域设计器：

- 在中**解决方案资源管理器**，双击窗体区域代码文件。

- 在中**解决方案资源管理器**，右键单击窗体区域代码文件，并单击**视图设计器**。

- 在中**解决方案资源管理器**，选择窗体区域代码文件，然后在**视图**菜单中，单击**设计器**。

  窗体区域设计器仅支持托管的控件。 不能添加本机 Outlook 控件。

## <a name="UsingFormRegionDesignedOutlook"></a> 导入在 Outlook 中设计的窗体区域
 在 Outlook 中进行设计时，可向窗体区域添加本机 Outlook 控件。 本机 Outlook 控件使你能够在设计时绑定到 Outlook 数据。 但不能使用窗体区域设计器来添加托管的控件或更改窗体区域的设计。

 您可以通过使用窗体区域导入 Outlook VSTO 外接程序项目**新建 Outlook 窗体区域**向导。 上**选择你想要创建窗体区域**页上，选择**导入 Outlook 窗体存储 (.ofs) 文件**。 然后可以浏览到 Outlook 窗体存储文件的位置 (*.ofs*) 文件。 (Outlook 将窗体区域作为保存 *.ofs*文件。)

 **新建 Outlook 窗体区域**向导副本 *.ofs*文件到项目目录，并控制将引用添加到窗体区域设计器文件。 然后可处理窗体区域代码文件中的控件事件。

 若要处理 Visual Basic 项目中的事件，从代码编辑器顶部的方法名列表中选择一个事件。

 若要处理 C# 项目中的事件，订阅 <xref:Microsoft.Office.Tools.Outlook.FormRegionControl.FormRegionShowing> 方法中的控件事件。 有关详细信息，请参阅[如何：订阅和取消订阅事件&#40;C&#35;编程指南&#41;](/dotnet/csharp/programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events)。

 可在窗体区域工厂类的 `InitializeManifest` 方法中更改窗体区域属性。

> [!NOTE]
> 若要导入窗体区域，进行的项目所面向的 Outlook 版本必须与开发计算机上安装的版本相同。 例如，如果您安装了 Outlook 2010，导入窗体区域才会起在项目中的已通过使用**Outlook 2010 外接程序**项目模板。

### <a name="update-an-imported-form-regions-design"></a>更新导入窗体区域的设计
 可以添加、删除或更改窗体区域上的控件。 执行此操作之前，请备份添加到窗体区域代码文件的所有代码。 然后，打开 *.ofs*文件在 Outlook 中，修改窗体区域，然后保存这些更改。 使用**新建 Outlook 窗体区域**向导来导入已修改 *.ofs*文件。 然后可将代码粘贴到新的窗体区域代码文件中。

## <a name="AddingCustomCode"></a> 将自定义代码添加到窗体区域
 <xref:Microsoft.Office.Tools.Outlook> 命名空间使你可以访问某些类，这些类表示窗体区域、显示窗体区域的 Outlook 项和其他有用项。 **Outlook 窗体区域**项会自动在项目中添加对此程序集的引用，并插入适当**使用**或**导入**顶部的语句窗体区域代码文件。

 可在 `Microsoft.Office.Interop.Outlook` 命名空间中使用类、方法和属性来完成大部分 Outlook 编程任务。 有关 Outlook 对象模型的详细信息，请参阅[Outlook 对象模型概述](../vsto/outlook-object-model-overview.md)。 有关 Outlook 对象模型的使用，请参阅的典型任务的示例[Outlook 解决方案](../vsto/outlook-solutions.md)。

### <a name="HandlingFormRegionEvents"></a> 处理窗体区域事件
 **Outlook 窗体区域**项到窗体区域代码文件会自动添加以下三个事件处理程序。

|Event|描述|
|-----------|-----------------|
|FormRegionInitializing|在初始化窗体区域之前发生。 可检查此事件处理程序中的条件以确定 Outlook 是否应显示窗体区域。 有关详细信息，请参阅[如何：防止 Outlook 显示窗体区域](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md)。|
|FormRegionShowing|在创建窗体区域的实例之后且在窗体区域显示之前发生。|
|FormRegionClosed|在窗体区域关闭之前发生。|

## <a name="Building"></a> 生成项目
 生成包含窗体区域的 Outlook VSTO 外接程序项目时，Visual Studio 会向注册表中添加以下信息：

- 与一个或多个窗体区域关联的每个邮件类的键。

- 每个窗体区域的项以及表示 Outlook VSTO 外接程序的名称的关联值。

  Outlook 使用此信息来加载窗体区域。

## <a name="Debugging"></a> 调试窗体区域
 可调试包含窗体区域的 Outlook VSTO 外接程序，正如调试其他 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 项目一样。 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 调试器时，Visual Studio 会自动启动 Outlook。

 若要查看窗体区域，必须打开适当的 Outlook 项。 例如，如果相邻的窗体区域附加到邮件项的底部，则打开邮件项。

## <a name="Deploying"></a> 部署窗体区域
 将窗体区域与关联的 Outlook VSTO 外接程序一起自动部署。 因此，不必执行任何特殊的任务来部署窗体区域。 有关部署 VSTO 外接程序的详细信息，请参阅[部署 Office 解决方案](../vsto/deploying-an-office-solution.md)。

## <a name="related-topics"></a>相关主题

|标题|描述|
|-----------|-----------------|
|[准则创建 Outlook 窗体区域](../vsto/guidelines-for-creating-outlook-form-regions.md)|提供有助于优化窗体区域和避免潜在问题的信息。|
|[如何：向 Outlook 外接程序项目添加窗体区域](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)|演示如何创建窗体区域，从而通过扩展标准或自定义 Microsoft Office Outlook 窗体**新建 Outlook 窗体区域**向导。|
|[将窗体区域与 Outlook 消息类相关联](../vsto/associating-a-form-region-with-an-outlook-message-class.md)|说明如何通过将窗体区域与每个项的邮件类关联来指定显示窗体区域的 Microsoft Office Outlook 项。|
|[演练：设计 Outlook 窗体区域](../vsto/walkthrough-designing-an-outlook-form-region.md)|演示如何设计在联系人项目的检查器窗口中作为新页出现的自定义窗体区域。|
|[演练：导入在 Outlook 中设计的窗体区域](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)|演示如何设计的窗体区域在 Microsoft Office Outlook 中，然后将窗体区域导入 Outlook VSTO 外接程序项目通过使用**新建 Outlook 窗体区域**向导。|
|[访问在运行时的窗体区域](../vsto/accessing-a-form-region-at-run-time.md)|介绍如何编写代码，以便显示、隐藏或修改窗体区域上的控件，以及如何使用户能够使用 `Globals` 类从项目的其他区域运行代码。|
|[如何：防止 Outlook 显示窗体区域](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md)|演示如何防止 Microsoft Office Outlook 显示特定项的窗体区域。|
|演示如何访问显示窗体区域的 Outlook 项。|
|[Outlook 窗体区域中的自定义操作](../vsto/custom-actions-in-outlook-form-regions.md)|描述如何使用户能够对 Outlook 项做出响应。|
