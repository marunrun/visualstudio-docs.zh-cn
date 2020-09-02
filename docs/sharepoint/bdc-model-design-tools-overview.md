---
title: BDC 模型设计工具概述 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.BDC.Method_Details
- VS.SharePointTools.BDC.Explorer
- VS.SharePointTools.BDC.Diagram
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], visual tools
- Business Data Connectivity service [SharePoint development in Visual Studio], visual tools
- Business Data Connectivity service [SharePoint development in Visual Studio], BDC Explorer
- BDC [SharePoint development in Visual Studio], method details
- Business Data Connectivity service [SharePoint development in Visual Studio], designer
- Business Data Connectivity service [SharePoint development in Visual Studio], method details
- BDC [SharePoint development in Visual Studio], BDC Explorer
- BDC [SharePoint development in Visual Studio], designer
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7a2531f1cc6352a03acf0b3d6af82c35e47c2743
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "64827954"
---
# <a name="bdc-model-design-tools-overview"></a>BDC 模型设计工具概述
  您可以通过使用 "bdc 设计器"、" **Bdc 方法详细信息** " 窗口和 " **Bdc 资源管理器**" (bdc) 模型中设计业务数据连接。

 利用 **BDC 资源管理器** ，您可以浏览模型、搜索模型以及定义类型描述符。

## <a name="bdc-designer"></a>BDC 设计器
 BDC 设计器使您能够在模型中定义实体，并以直观方式排列它们之间的关系。 使用 BDC 设计器来完成以下任务：

- 将实体添加到模型。

- 从模型中删除实体。

- 定义实体之间的关系。

  若要打开 BDC 设计器，请双击项目中的模型文件，或打开模型文件的快捷菜单，然后选择 " **打开**"。 通过将实体从**工具箱**拖放到设计器上，**将实体添加**到模型。 若要创建两个实体之间的关联，请在 "**工具箱**" 中选择 "**关联**" 控件，选择第一个实体，然后选择第二个实体。

## <a name="bdc-method-details-window"></a>"BDC 方法详细信息" 窗口
 使用 " **BDC 方法详细信息** " 窗口可定义方法的参数、实例和筛选器描述符。

 可以在 " **BDC 方法详细信息** " 窗口中快速生成 Finder、特定的 Finder、创建者、更新程序和删除器方法。 生成这些方法时，Visual Studio 会将元数据（例如参数、实例和类型描述符）添加到方法。 你可以修改此元数据，以满足你的特定方案。

 若要打开 " **BDC 方法详细信息**" 窗口，请在菜单栏上选择 "**查看**  >  **其他 Windows**  >  **BDC 方法详细信息**"。

 若要在 " **Bdc 方法详细信息** " 窗口中查看方法，请在 Bdc 设计器中选择实体。 所选实体的方法将显示在 " **BDC 方法详细信息** " 窗口中。 如果未在 BDC 设计器中选择实体，则 " **BDC 方法详细信息** " 窗口不会显示任何信息。

 展开或折叠 " **BDC 方法详细信息** " 窗口中的节点可定义参数、实例和筛选器描述符。 使用 **BDC 资源管理器** 定义类型描述符。

## <a name="bdc-explorer"></a>BDC 资源管理器
 " **BDC 资源管理器** " 显示构成模型的元素。 若要打开 " **BDC 资源管理器**"，请在菜单栏上选择 "**查看**  >  **其他 Windows**  >  **BDC 资源管理器**"。 若要浏览模型，请在 " **BDC 资源管理器**" 中展开节点。 每个节点都表示模型文件的 XML 中的一个元素。

 在 **BDC 资源管理器**中选择节点时，所选的每个节点的属性将显示在 " **属性** " 窗口中。 其中的许多属性与模型文件中的属性相对应。 您可以使用 **BDC 资源管理器**顶部的搜索框来搜索模型。

> [!NOTE]
> **BDC 资源管理器**不显示标识符、自定义属性、本地化的字符串、关联组、操作、筛选器描述符、操作控件列表和默认参数值。

### <a name="define-type-descriptors"></a>定义类型描述符
 使用 **BDC 资源管理器** 定义类型描述符。 使用 BDC 资源管理器，您可以定义一次类型描述符，然后在您的模型中的其他位置重用该类型描述符。 若要实现此目的，请复制类型描述符，并将其粘贴到任何其他参数或类型描述符。

> [!NOTE]
> 对原始类型描述符所做的更改不会影响该类型描述符的副本。

 有关详细信息，请参阅 [如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)。

## <a name="see-also"></a>另请参阅
- [如何：创建 BDC 模型](../sharepoint/how-to-create-a-bdc-model.md)
- [如何：向模型添加实体](../sharepoint/how-to-add-an-entity-to-a-model.md)
- [如何：添加 Finder 方法](../sharepoint/how-to-add-a-finder-method.md)
- [如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)
- [如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)
- [如何：添加删除器方法](../sharepoint/how-to-add-a-deleter-method.md)
- [如何：添加更新程序方法](../sharepoint/how-to-add-an-updater-method.md)
- [创建实体之间的关联](../sharepoint/creating-an-association-between-entities.md)
- [演练：使用业务数据在 SharePoint 中创建外部列表](../sharepoint/walkthrough-creating-an-external-list-in-sharepoint-by-using-business-data.md)
- [将业务数据集成到 SharePoint 中](../sharepoint/integrating-business-data-into-sharepoint.md)
- [创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
