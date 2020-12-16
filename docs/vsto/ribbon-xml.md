---
title: Ribbon XML
description: 如果要以功能区 (可视化设计器) 项不支持的方式自定义功能区，请参阅如何使用功能区 (XML) 项。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VSTO.Ribbon.RibbonXMLItem
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom Ribbon, XML
- customizing the Ribbon, XML
- Ribbon [Office development in Visual Studio], XML
- callback methods
- custom Ribbon, displaying
- custom Ribbon, defining behavior
- XML [Office development in Visual Studio], Ribbon
- customizing the Ribbon, defining behavior
- Ribbon [Office development in Visual Studio], customizing
- customizing the Ribbon, displaying
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 1c9e1cf4c6af266495b3d85d96aa8cce1697cca7
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2020
ms.locfileid: "97528416"
---
# <a name="ribbon-xml"></a>Ribbon XML
  功能区 (XML) 项使你可以通过使用 XML 来自定义功能区。 如果要以功能区 (可视化设计器) 项不支持的方式自定义功能区，请使用功能区 (XML) 项。 有关可对每个项执行的操作的比较，请参阅 [功能区概述](../vsto/Ribbon-overview.md)。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

## <a name="add-a-ribbon-xml-item-to-a-project"></a>向项目添加功能区 (XML) 项
 在 **“添加新项”** 对话框中，可将 **“功能区 (XML)”** 项添加到任何 Office 项目。 Visual Studio 自动将以下文件添加到项目：

- 功能区 XML 文件。 此文件定义功能区用户界面 (UI)。 使用此文件添加 UI 元素，例如选项卡、组和控件。 有关详细信息，请参阅本主题后面的 [功能区 XML 文件引用](#RibbonDescriptorFile) 。

- 功能区代码文件。 此文件包含 *功能区类*。 此类的名称即你在 **“添加新项”** 对话框中为 **“功能区 (XML)”** 项指定的名称。 Microsoft Office 应用程序使用此类的实例来加载自定义功能区。 有关详细信息，请参阅本主题后面的 [功能区类引用](#RibbonExtensionClass) 。

  默认情况下，这些文件会在功能区的 " **外接程序** " 选项卡中添加一个自定义组。

## <a name="display-the-custom-ribbon-in-a-microsoft-office-application"></a>在 Microsoft Office 应用程序中显示自定义功能区
 将 **功能区 (XML)** 项添加到项目后，必须将代码添加到 **ThisAddin**、 **ThisWorkbook** 或 **ThisDocument** 类，以便重写方法， `CreateRibbonExtensibilityObject` 并将功能区 XML 类返回到 Office 应用程序。

 下面的代码示例替代 `CreateRibbonExtensibilityObject` 方法并返回名为 MyRibbon 的功能区 XML 类。

 [!code-csharp[Trin_Ribbon_Custom_Tab_XML#1](../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.cs#1)]
 [!code-vb[Trin_Ribbon_Custom_Tab_XML#1](../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.vb#1)]

## <a name="define-the-behavior-of-the-custom-ribbon"></a>定义自定义功能区的行为
 您可以通过创建 *回调方法* 来响应用户操作，例如单击功能区上的按钮。 回叫方法类似于 Windows 窗体控件中的事件，但它们由 UI 元素的 XML 中的特性标识。 可在功能区类中编写方法，并且控件调用名称与特性值相同的方法。 例如，你可以创建一个在用户单击功能区上的按钮时调用的回调方法。 创建回叫方法需要两个步骤：

- 将特性分配给功能区 XML 文件中的控件，该文件标识代码中的回叫方法。

- 定义功能区类中的回叫方法。

> [!NOTE]
> Outlook 还需要一个额外的步骤。 有关详细信息，请参阅 [自定义 Outlook 功能区](../vsto/customizing-a-ribbon-for-outlook.md)。

 有关演示如何从功能区实现应用程序自动化的演练，请参阅 [演练：使用功能区 XML 创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)。

### <a name="assign-callback-methods-to-controls"></a>将回叫方法分配给控件
 若要将回叫方法分配给功能区 XML 文件中的控件，添加指定回叫方法类型和方法名称的特性。 例如，下面的元素定义具有名为 **OnToggleButton1** 的 `OnToggleButton1`。

```xml
<toggleButton id="toggleButton1" onAction="OnToggleButton1" />
```

 用户执行与特定控件关联的主要任务时调用 **onAction** 。 例如，用户单击切换按钮时调用该按钮的 **onAction** 回叫方法。

 在特性中指定的方法可具有任何名称。 但该名称必须与在功能区代码文件中定义的方法的名称相匹配。

 有许多不同类型的回叫方法可分配给功能区控件。 有关可用于每个控件的回调方法的完整列表，请参阅技术文章 [为开发人员自定义 Office (2007) 功能区用户界面， (第3部分（共) 3 部分 ](/previous-versions/office/developer/office-2007/aa722523(v=office.12))）。

### <a name="define-callback-methods"></a><a name="CallBackMethods"></a> 定义回调方法
 定义功能区代码文件中功能区类中的回叫方法。 回叫方法具有以下几个要求：

- 它必须声明为公共。

- 其名称必须匹配分配给功能区 XML 文件中控件的回叫方法的名称。

- 其签名必须与可用于关联功能区控件的某类回叫方法匹配。

  有关功能区控件的回叫方法签名的完整列表，请参阅技术文章 [为开发人员自定义 Office (2007) 功能区用户界面， (第3部分（共) 3 部分 ](/previous-versions/office/developer/office-2007/aa722523(v=office.12))）。 Visual Studio 不对在功能区代码文件中创建的回叫方法提供 IntelliSense 支持。 如果创建的回叫方法与有效签名不匹配，代码虽然能够编译，但当用户单击控件时不会执行任何操作。

  所有回叫方法都有表示调用了方法的控件的 <xref:Microsoft.Office.Core.IRibbonControl> 参数。 可使用此参数重用多个控件的相同回叫方法。 下面的代码示例演示根据用户单击的控件执行不同任务的 **onAction** 回叫方法。

  [!code-csharp[Trin_RibbonOutlookBasic#2](../vsto/codesnippet/CSharp/Trin_RibbonOutlookBasic/Ribbon1.cs#2)]
  [!code-vb[Trin_RibbonOutlookBasic#2](../vsto/codesnippet/VisualBasic/Trin_RibbonOutlookBasic/Ribbon1.vb#2)]

## <a name="ribbon-xml-file-reference"></a><a name="RibbonDescriptorFile"></a> 功能区 XML 文件引用
 可以通过将元素和特性添加到功能区 XML 文件来定义自定义功能区。 默认情况下，功能区 XML 文件包含以下 XML。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<customUI xmlns="http://schemas.microsoft.com/office/2006/01/customui" onLoad="OnLoad">
  <ribbon>
    <tabs>
      <tab idMso="TabAddIns">
        <group id="MyGroup"
               label="My Group">
        </group>
      </tab>
    </tabs>
  </ribbon>
</customUI>
```

 下表介绍功能区 XML 文件中的默认元素。

|元素|说明|
|-------------|-----------------|
|**customUI**|表示 VSTO 外接程序项目中的自定义功能区。|
|**弯**|表示功能区。|
|**选项卡**|表示一组功能区选项卡。|
|**"选项卡**|表示单个功能区选项卡。|
|**group**|表示功能区选项卡上的一组控件。|

 这些元素具有指定自定义功能区的外观和行为的特性。 下表介绍功能区 XML 文件中的默认特性。

|Attribute|父元素|描述|
|---------------|--------------------|-----------------|
|**onLoad**|**customUI**|标识当应用程序加载功能区时调用的方法。|
|**idMso**|**"选项卡**|标识要显示在功能区中的内置选项卡。|
|**id**|**group**|标识组。|
|**label**|**group**|指定在组上显示的文本。|

 功能区 XML 文件中的默认元素和特性是可用元素和特性一小部分。 有关可用元素和属性的完整列表，请参阅技术文章 [为开发人员自定义 Office (2007) 功能区用户界面， (第2部分（共) 3 部分 ](/previous-versions/office/developer/office-2007/aa338199(v=office.12))）。

## <a name="ribbon-class-reference"></a><a name="RibbonExtensionClass"></a> 功能区类引用
 Visual Studio 在功能区代码文件中生成功能区类。 将功能区上控件的回叫方法添加到此类。 此类实现 <xref:Microsoft.Office.Core.IRibbonExtensibility> 接口。

 下表介绍此类中的默认方法。

|方法|说明|
|------------|-----------------|
|`GetCustomUI`|返回功能区 XML 文件的内容。 Microsoft Office 应用程序调用此方法以获取一个 XML 字符串，该字符串定义自定义功能区的用户界面。 此方法实现 <xref:Microsoft.Office.Core.IRibbonExtensibility.GetCustomUI%2A> 方法。 **注意：** `GetCustomUI`只应实现以返回功能区 XML 文件的内容;不应使用它来初始化 VSTO 外接程序。   特别是，不应在 `GetCustomUI` 实现中尝试显示对话框或其他窗口。 否则，自定义功能区可能不会正常运行。 如果必须运行初始化 VSTO 外接程序的代码，请将代码添加到 `ThisAddIn_Startup` 事件处理程序。|
|`OnLoad`|将 <xref:Microsoft.Office.Core.IRibbonControl> 参数分配给 `Ribbon` 字段。 Microsoft Office 应用程序在加载自定义功能区时调用此方法。 您可以使用此字段动态更新自定义功能区。 有关详细信息，请参阅技术文章 [为开发人员自定义 Office (2007) 功能区用户界面 (第1部分（共) 3 部分 ](/previous-versions/office/developer/office-2007/aa338202(v=office.12))）。|
|`GetResourceText`|由 `GetCustomUI` 方法调用，以获取功能区 XML 文件的内容。|

## <a name="see-also"></a>另请参阅
- [功能区概述](../vsto/ribbon-overview.md)
- [演练：使用功能区 XML 创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)
- [Office UI 自定义](../vsto/office-ui-customization.md)
