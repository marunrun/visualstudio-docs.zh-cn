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
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387717"
---
# <a name="bdc-model-design-tools-overview"></a>BDC 模型设计工具概述
  可以通过使用 BDC 设计器中，设计业务数据连接 (BDC) 模型**BDC 方法详细信息**窗口中，并**BDC 资源管理器**。

 **BDC 资源管理器**使您能够浏览该模型，搜索该模型，并定义类型描述符。

## <a name="bdc-designer"></a>BDC 设计器
 BDC 设计器使您可以在模型中定义实体并直观地与另一个排列它们之间的关系。 使用 BDC 设计器完成以下任务：

- 将实体添加到模型。

- 从模型中删除实体。

- 定义实体之间的关系。

  若要打开 BDC 设计器中，双击你的项目中的模型文件或打开模型文件的快捷菜单，然后选择**打开**。 将实体添加到模型中，通过拖动或复制**实体**从**工具箱**拖到设计器。 若要创建两个实体之间的关联，请选择**关联**控制**工具箱**，选择第一个实体，然后选择第二个实体。

## <a name="bdc-method-details-window"></a>BDC 方法详细信息窗口
 使用**BDC 方法详细信息**窗口，以定义参数、 实例和筛选器描述符的一种方法。

 你可以快速生成中的查找器、 特定的 Finder、 创建者、 更新程序和删除器方法**BDC 方法详细信息**窗口。 生成这些方法时，Visual Studio 会将元数据，例如参数、 实例和类型描述符添加到该方法。 您可以修改此元数据以满足您的特定方案。

 若要打开**BDC 方法详细信息**窗口，请在菜单栏上，选择**视图** > **其他 Windows** > **BDC 方法详细信息**.

 若要查看中的方法**BDC 方法详细信息**窗口中，在 BDC 设计器中选择的实体。 所选实体的方法显示在**BDC 方法详细信息**窗口。 如果没有在 BDC 设计器中，选择实体**BDC 方法详细信息**窗口会显示任何信息。

 展开或折叠中的节点**BDC 方法详细信息**窗口，以定义参数、 实例和筛选器描述符。 使用**BDC 资源管理器**定义类型描述符。

## <a name="bdc-explorer"></a>BDC 资源管理器
 **BDC 资源管理器**显示构成的模型的元素。 若要打开**BDC 资源管理器**，在菜单栏上依次选择**视图** > **其他 Windows** > **BDC 资源管理器**。 若要浏览该模型，展开在节点**BDC 资源管理器**。 每个节点表示模型文件的 XML 中的元素。

 选择中的节点时**BDC 资源管理器**，选择每个节点的属性将显示在**属性**窗口。 其中的许多属性对应于模型文件中的特性。 可以通过使用顶部的搜索框搜索模型**BDC 资源管理器**。

> [!NOTE]
> **BDC 资源管理器**不显示标识符、 自定义属性、 本地化的字符串、 关联组、 操作、 筛选器描述符、 操作控件列表和默认参数值。

### <a name="define-type-descriptors"></a>定义类型描述符
 使用**BDC 资源管理器**定义类型描述符。 BDC 资源管理器，可将类型描述符定义一次，然后在重用您的模型中的其他位置该类型描述符。 若要实现此目的，复制的类型描述符并将其粘贴到任何其他参数或类型描述符。

> [!NOTE]
> 对原始的类型描述符的更改不会影响该类型描述符的副本。

 有关详细信息，请参阅[如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)。

## <a name="see-also"></a>请参阅
- [如何：创建 BDC 模型](../sharepoint/how-to-create-a-bdc-model.md)
- [如何：向模型添加实体](../sharepoint/how-to-add-an-entity-to-a-model.md)
- [如何：添加 Finder 方法](../sharepoint/how-to-add-a-finder-method.md)
- [如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)
- [如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)
- [如何：添加 Deleter 方法](../sharepoint/how-to-add-a-deleter-method.md)
- [如何：添加 Updater 方法](../sharepoint/how-to-add-an-updater-method.md)
- [创建实体之间的关联](../sharepoint/creating-an-association-between-entities.md)
- [演练：使用业务数据在 SharePoint 中创建外部列表](../sharepoint/walkthrough-creating-an-external-list-in-sharepoint-by-using-business-data.md)
- [将业务数据集成到 SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md)
- [创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
