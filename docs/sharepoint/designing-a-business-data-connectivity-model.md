---
title: 设计业务数据连接模型 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], designing a model
- Business Data Connectivity service [SharePoint development in Visual Studio], designing a model
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8f322d18afdb8e14ee87ae31d30dd6bdd57b07c5
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63431289"
---
# <a name="design-a-business-data-connectivity-model"></a>设计业务数据连接模型
  可以通过将实体和方法添加到模型文件来开发业务数据连接 (BDC) 服务的模型。 实体描述数据字段的集合。 例如，实体可以表示在数据库中的表。 一种方法执行如添加、 删除或更新实体所表示的数据的任务。 有关详细信息，请参阅[将业务数据集成到 SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md)。

## <a name="add-entities"></a>添加实体
 可以通过拖动或复制添加实体**实体**从 Visual Studio**工具箱**到 BDC 设计器上。 有关详细信息，请参阅[如何：将实体添加到模型](../sharepoint/how-to-add-an-entity-to-a-model.md)。

 在类中定义的实体的字段。 例如，您可能会添加一个名为字段`Address`到`Customer`类。 您可以向项目添加新类，或使用现有类使用其他工具，例如对象关系设计器 （O/R 设计器） 创建的。 实体的名称和类表示实体的名称不需要匹配。 在模型中定义的方法时，可以与实体相关类。

## <a name="add-methods"></a>添加方法
 当用户查看、 添加、 更新或删除列表或基于模型的 Web 部件中的信息时，BDC 服务模型中调用方法。 必须将方法添加到每个用户可以执行的任务的模型。 通过选择任意五种基本方法类型从创建方法**BDC 方法详细信息**窗口。 下表介绍 BDC 模型的五个基本方法。

|方法|描述|
|------------|-----------------|
|查找器|返回的实体实例的集合。 当用户打开列表或 Web 部件时调用。 有关详细信息，请参阅[如何：添加 Finder 方法](../sharepoint/how-to-add-a-finder-method.md)。|
|特定的 Finder|返回特定实体实例。 当用户在列表中查看特定项的详细信息时调用。 有关详细信息，请参阅[如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)。|
|创建者|将新数据添加到数据源的实体。 当用户选择时，调用**新项**基于模型的列表的功能区上的按钮。 有关详细信息，请参阅[如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)。|
|更新者|修改列表中的数据。 当用户更新列表中的信息时调用。 有关详细信息，请参阅[如何：添加 Updater 方法](../sharepoint/how-to-add-an-updater-method.md)。|
|删除者|删除数据。 当用户从列表中删除项时调用。 有关详细信息，请参阅[如何：添加 Deleter 方法](../sharepoint/how-to-add-a-deleter-method.md)。|

## <a name="define-method-parameters"></a>定义方法的参数
 创建一个方法，在 Visual Studio 将添加适用于的方法类型的输入和输出参数。 这些参数将是仅仅作为占位符。 在大多数情况下，必须修改参数，以便它们在传递或返回正确的数据类型。 例如，默认情况下，Finder 方法返回一个字符串。 在大多数情况下，你想要修改的 Finder 方法的返回参数，以便它返回实体的集合。 可以通过修改该参数的类型描述符来实现此目的。 类型描述符是描述参数的数据类型的特性集合。 有关详细信息，请参阅[如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)。

 Visual Studio，可复制在模型中的参数之间的类型描述符。 例如，可以定义名为的类型描述符`CustomerTD`的返回参数`GetCustomer`方法。 可以将复制`CustomerTD`类型在描述符**BDC 资源管理器**，然后将其粘贴到的输入参数的类型描述符`CreateCustomer`方法。 这样可防止您无需多次定义的相同的类型描述符。

## <a name="method-instances"></a>方法实例
 创建一个方法，在 Visual Studio 将添加默认方法实例。 方法实例是一种方法，以及参数的默认值的引用。 单个方法可以有多个方法实例。 每个实例是一组默认值和方法签名的组合。 有关详细信息，请参阅[如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)。

 运行项目时，方法实例出现在 SharePoint 列表上方的下拉列表中。 用户可以选择方法实例来查看数据。

 若要添加到方法实例的默认值，您必须直接修改模型的 XML。 有关详细信息，请参阅[DefaultValue](http://go.microsoft.com/fwlink/?LinkID=169279)。

## <a name="add-filter-descriptors"></a>添加筛选器描述符
 模型的使用者可能想要检索的实体与某些条件匹配的实例。 若要启用此功能，可以向方法添加筛选器描述符。 筛选器描述符，将值传递给方法执行之前筛选方法的结果集的模型使用者。 有关详细信息，请参阅[如何：将筛选器参数添加到操作，以限制从外部系统实例](http://go.microsoft.com/fwlink/?LinkID=169267)。

 SharePoint 提供多种功能，使用户能够提供的筛选器值。 例如，业务数据 Web 部件提供筛选器文本框。 用户可通过在该文本框中输入值来限制列表中的数据。 有关如何将筛选器描述符添加到方法的详细信息，请参阅[如何：将筛选器描述符添加到 Finder 方法](../sharepoint/how-to-add-a-filter-descriptor-to-a-finder-method.md)。

### <a name="filter-descriptor-properties"></a>筛选器描述符属性
 必须设置的值**关联的类型描述符**，**名称**，并**类型**筛选器描述符的属性。 所有其他属性是可选的。

 **关联的类型描述符**属性将筛选器描述符与输入参数。 当用户提供一个筛选器值时，BDC 服务该将值传递到该方法使用输入的参数。

 **类型**属性描述你想要使用的筛选模式。 在 SharePoint 中，您选择的筛选模式会影响显示用户界面 (UI) 中的文本。 例如，对于比较运算符筛选模式，文本**等同于**将显示为上述业务数据 Web 部件控件。 有关每种筛选模式的详细信息，请参阅[类型的筛选器受 BDC](http://go.microsoft.com/fwlink/?LinkId=169287)。

 有关属性的筛选器描述符的详细信息，请参阅[FilterDescriptor](http://go.microsoft.com/fwlink/?LinkID=169280)。

### <a name="provide-default-values"></a>提供默认值
 在某些情况下，用户可能会提供一个筛选器值。 通过将默认值添加到方法的实例，或通过在你的方法的代码中设置的默认值，可以提供默认值。 有关如何将默认值添加到方法实例的详细信息，请参阅[MethodInstance](http://go.microsoft.com/fwlink/?LinkID=169282)。 有关如何在您的方法的代码中设置输入参数的默认值的示例，请参阅[如何：将筛选器描述符添加到 Finder 方法](../sharepoint/how-to-add-a-filter-descriptor-to-a-finder-method.md)。

## <a name="validate-the-model"></a>验证模型
 您可以在开发过程中验证您的模型。 Visual Studio 将标识可以防止您的模型按预期方式运行的问题。 这些问题出现在 Visual Studio**错误列表**。

 可以通过打开 BDC 设计器的快捷菜单，然后选择验证模型**验证**。 如果模型包含任何错误，它们显示在**错误列表**。 你可以通过双击列表中的错误，快速将光标移至包含错误的代码。 作为替代方法，你可以选择**F8**或**Shift**+**F8**密钥，以便单步前进或后退列表中的错误。

 模型的规则违反以某种方式时，会发生验证错误。 例如，如果**IsCollection**类型描述符的属性设置为**true**，但没有子类型描述符存在，将出现验证错误。 您可能必须要了解一些在 Visual Studio 中显示的错误的 BDC 模型的规则，请参阅**错误列表**。 BDC 模型的规则的详细信息，请参阅[BDCMetadata 架构](http://go.microsoft.com/fwlink/?LinkID=169275)。

## <a name="debug-the-solution-that-contains-the-model"></a>调试包含模型的解决方案
 就像调试任何代码在 Visual Studio 中的，您可以调试您的代码。 若要调试你的代码，在代码中的任意位置设置断点，然后启动调试器。 Visual Studio 将打开 SharePoint 站点。 在 SharePoint 中创建列表或使用您的业务数据 Web 部件。 然后，您可以单步执行代码。 有关调试 SharePoint 项目的详细信息，请参阅[进行故障排除 SharePoint 解决方案](../sharepoint/troubleshooting-sharepoint-solutions.md)。

 此外可以调试自定义程序集添加到项目中的代码。 但是，若要调试自定义程序集中的代码，必须将程序集添加到解决方案包。 有关详细信息，请参阅[如何：添加和删除其他程序集](../sharepoint/how-to-add-and-remove-additional-assemblies.md)。

 有关将自定义程序集添加到你的项目的详细信息，请参阅[如何：在 BDC 功能中包含自定义程序集](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)。

### <a name="configure-bdc-security"></a>配置 BDC 安全性
 您可能需要修改您在 SharePoint 中的安全设置，然后您可以调试你的解决方案。 若要修改这些设置，请打开业务数据连接服务应用程序在 SharePoint 2010 管理中心网站。 在中**设置元数据存储区权限**对话框中，添加你的用户帐户，并选择以下选项之一：

|任务|选项|
|----------|------------|
|若要将模型部署到 BDC 服务。|Edit|
|若要创建列表和 Web 部件使用外部内容中您的模型类型 （实体）。|可选择在客户端|
|若要创建、 读取、 更新和删除实体数据。|执行|

 有关这些设置的详细信息，请参阅[业务数据连接服务管理](http://go.microsoft.com/fwlink/?LinkID=178883)。

 此外可以设置单独的模型或外部内容类型的安全权限。 有关如何设置模型的安全权限的详细信息，请参阅[BDC 模型管理](http://go.microsoft.com/fwlink/?LinkID=178884)。 有关如何设置外部内容类型的安全权限的详细信息，请参阅[外部内容类型管理](http://go.microsoft.com/fwlink/?LinkID=178885)。

> [!NOTE]
> 使用这些设置来调试你的本地 SharePoint 服务器上的解决方案。 有关如何在生产 SharePoint 服务器上配置 BDC 相关安全性设置的详细信息，请参阅[Business Data Connectivity Services 安全性概述](http://go.microsoft.com/fwlink/?LinkID=178886)。

### <a name="retract-models-that-become-corrupt"></a>收回损坏的模型
 当您第一次启动调试器时，Visual Studio 会将整个模型部署到 SharePoint。 每次之后，Visual Studio 使用的部署之间所做的任何更改更新 SharePoint 中的模型。

 可能会想要完全取消将模型从 SharePoint 的 Visual Studio 的情况。 例如，模型可能会损坏。  若要重新部署到 SharePoint 模型，将设置**增量更新**到模型属性**False**，然后启动调试器。 **增量更新**属性将出现在**属性**窗口中选择表示该模型中的节点时**BDC 资源管理器**。 默认情况下，模型的名称是**BdcModel1**。

### <a name="change-identifier-names-of-entities-in-the-model"></a>更改模型中的实体的标识符名称
 如果您部署模型后更改标识符的名称，可能会收到部署错误。 不能通过设置来解决此错误**增量更新**到模型属性**False**。 必须手动，收回模型，然后再次部署该解决方案。 有关详细信息，请参阅[进行故障排除 SharePoint 解决方案](../sharepoint/troubleshooting-sharepoint-solutions.md)。 可以通过设置避免此错误**增量更新**属性设置为**False**在最初部署该模型之前。

## <a name="locate-documentation-for-bdc-model-elements"></a>查找有关 BDC 模型元素的文档，
 Visual Studio 将 XML 元素添加到每个实体的模型方法或创建其他项。 元素属性作为属性出现在**属性**窗口。 有关元素和属性在设计模型时，Visual Studio 生成的信息，请参阅[BDCMetadata 架构](http://go.microsoft.com/fwlink/?LinkID=169275)。

## <a name="related-topics"></a>相关主题

|标题|描述|
|-----------|-----------------|
|[BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)|描述可用于以可视方式设计 BDC 模型的工具。|
|[如何：向模型添加实体](../sharepoint/how-to-add-an-entity-to-a-model.md)|演示如何将外部内容类型或实体，添加到模型。|
|[如何：添加 Finder 方法](../sharepoint/how-to-add-a-finder-method.md)|演示如何添加一个方法，使用户可以在列表或 Web 部件中查看实体的列表。|
|[如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)|演示如何添加一个方法，使用户能够查看特定实体的详细信息。|
|[如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)|演示如何添加一个方法，使用户能够直接从列表或 Web 部件添加到数据源的记录。|
|[如何：添加 Deleter 方法](../sharepoint/how-to-add-a-deleter-method.md)|演示如何添加一个方法，使用户能够从数据源中删除数据，通过使用选项列表中的用户界面 (UI) 或 Web 部件中。|
|[如何：添加 Updater 方法](../sharepoint/how-to-add-an-updater-method.md)|演示如何添加一个方法，使用户可以直接从列表或 Web 部件更改数据源中的数据记录。|
|[如何：将参数添加到方法](../sharepoint/how-to-add-a-parameter-to-a-method.md)|演示如何使用 Visual Studio 中的方法的详细信息窗口向方法中添加输入和返回参数。|
|[如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)|演示如何在模型中定义参数数据类型。|
|[如何：定义方法实例](../sharepoint/how-to-define-a-method-instance.md)|演示如何创建 BDC 所执行的方法的实例。|
|[如何：将筛选器描述符添加到 Finder 方法](../sharepoint/how-to-add-a-filter-descriptor-to-a-finder-method.md)|演示如何使用户能够限制返回的 Finder 方法实例的数目。|
|[创建实体之间的关联](../sharepoint/creating-an-association-between-entities.md)|介绍如何定义模型中的实体之间的关系。 业务数据 Web 部件、 外部列表和自定义应用程序可以在用户界面 (UI) 中显示这些数据关系。|
|[如何：创建实体之间的关联](../sharepoint/how-to-create-an-association-between-entities.md)|演示如何定义模型中的实体之间的关系。|
|[演练：创建在 SharePoint 中使用业务数据的外部列表](../sharepoint/walkthrough-creating-an-external-list-in-sharepoint-by-using-business-data.md)|提供演示如何创建和测试 SharePoint 外部列表中显示的联系人的模型的分步说明。|
|[将业务数据集成到 SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md)|提供创建和设计的 BDC 服务模型的概述。|
