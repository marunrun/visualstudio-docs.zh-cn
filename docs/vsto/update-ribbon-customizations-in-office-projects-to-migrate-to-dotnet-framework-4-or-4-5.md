---
title: Office 项目中的更新功能区自定义迁移到.NET Framework 4、 4.5
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office projects [Office development in Visual Studio], migrating to .NET Framework 4
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 03424ecb477a32ecff31a83d341a6eef178a31e0
ms.sourcegitcommit: cc5fd59e5dc99181601b7db8b28d7f8a83a36bab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2019
ms.locfileid: "66836080"
---
# <a name="update-ribbon-customizations-in-office-projects-that-you-migrate-to-the-net-framework-4-or-the-net-framework-45"></a>更新迁移到.NET Framework 4 或.NET Framework 4.5 的 Office 项目中的功能区自定义
  如果您的项目包含已通过使用功能区自定义**功能区 （可视化设计器）** 项目项，必须对你的项目代码进行以下更改，如果目标框架更改为[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]或更高版本。

- 修改生成的功能区代码。

- 修改在运行时实例化功能区控件、处理功能区事件或以编程方式设置功能区组件位置的任何代码。

## <a name="update-the-generated-ribbon-code"></a>更新生成的功能区代码
 如果已将项目的目标框架更改为 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本，则必须通过执行以下步骤更改功能区项的生成代码。 你需要更新的代码文件取决于编程语言和你创建项目的方式：

- 在 Visual Basic 项目中，或在 Visual C# 项目中创建[!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)]或[!INCLUDE[vs_dev10_long](../sharepoint/includes/vs-dev10-long-md.md)]功能区代码隐藏文件中执行的所有步骤 (*YourRibbonItem*。Designer.cs 或*YourRibbonItem*。Designer.vb)。 若要查看 Visual Basic 项目中的代码隐藏文件，请单击**显示所有文件**按钮**解决方案资源管理器**。

- 在 Visual C# 项目，在 Visual Studio 2008 中创建，然后升级到[!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)]，在功能区代码文件中执行的前两个步骤 (*YourRibbonItem*.cs 或*YourRibbonItem*.vb)，并功能区代码隐藏文件中执行剩余步骤。

### <a name="to-change-the-generated-ribbon-code"></a>若要更改生成的功能区代码

1. 修改 Ribbon 类的声明，使它可以从 <xref:Microsoft.Office.Tools.Ribbon.RibbonBase> 而不是从 `Microsoft.Office.Tools.Ribbon.OfficeRibbon` 派生。

2. 修改 Ribbon 类的构造函数，如下所示。 如果你已向构造函数添加了自己的所有代码，则不要更改你的代码。 在 Visual Basic 项目中，仅修改无参数构造函数。 忽略另一个构造函数。

     下面的代码示例介绍了面向 .NET Framework 3.5 的项目中的 Ribbon 类的默认构造函数。

    ```vb
    Public Sub New()
        MyBase.New()
        InitializeComponent()
    End Sub
    ```

    ```csharp
    public Ribbon1()
    {
        InitializeComponent();
    }
    ```

     下面的代码示例介绍了面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的项目中的 Ribbon 类的默认构造函数。

    ```vb
    Public Sub New()
        MyBase.New(Globals.Factory.GetRibbonFactory())
        InitializeComponent()
    End Sub
    ```

    ```csharp
    public Ribbon1()
        : base(Globals.Factory.GetRibbonFactory())
    {
        InitializeComponent();
    }
    ```

3. 在 `InitializeComponent` 方法中，修改构造功能区控件的任何代码，使代码能够改用 <xref:Microsoft.Office.Tools.Ribbon.RibbonFactory> 对象的一种帮助器方法。

    > [!NOTE]
    > 在 Visual C# 项目中，必须展开名为 `Component Designer generated code` 的区域才能查看 `InitializeComponent` 方法。

     例如，假设文件包含以下代码行，该代码行可实例化面向 .NET Framework 3.5 的项目中名为 `button1` 的 <xref:Microsoft.Office.Tools.Ribbon.RibbonButton>。

    ```vb
    Me.button1 = New Microsoft.Office.Tools.Ribbon.RibbonButton()
    ```

    ```csharp
    this.button1 = new Microsoft.Office.Tools.Ribbon.RibbonButton();
    ```

     在面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的项目中，必须改用以下代码。

    ```vb
    Me.button1 = Me.Factory.CreateRibbonButton()
    ```

    ```csharp
    this.button1 = this.Factory.CreateRibbonButton();
    ```

     功能区控件的帮助器方法的完整列表，请参阅[实例化功能区控件](#ribboncontrols)。

4. 在 Visual C# 项目中，修改 `InitializeComponent` 方法中的任何代码行，该方法使用 <xref:System.EventHandler%601> 委托来改用特定功能区委托。

     例如，假设文件包含以下代码行，该代码行可处理面向 .NET Framework 3.5 的项目中的 <xref:Microsoft.Office.Tools.Ribbon.RibbonButton.Click> 事件。

    \<CodeContentPlaceHolder > 8</CodeContentPlaceHolder>中的项目是面向[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]或更高版本，必须改为使用下面的代码。

    \<CodeContentPlaceHolder > 9</CodeContentPlaceHolder>功能区委托的完整列表，请参阅[处理功能区事件](#ribbonevents)。

5. 在 Visual Basic 项目中，找到文件末尾的 `ThisRibbonCollection` 类。 修改此类的声明，以便它不再继承自 `Microsoft.Office.Tools.Ribbon.RibbonReadOnlyCollection`。

## <a name="ribboncontrols"></a> 实例化功能区控件
 必须修改可动态实例化功能区控件的任何代码。 在面向.NET Framework 3.5 的项目中，功能区控件是你可以直接在某些方案中进行实例化的类。 在面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的项目中，这些控件是你无法直接实例化的接口。 你必须通过使用由 <xref:Microsoft.Office.Tools.Ribbon.RibbonFactory> 对象提供的方法创建控件。

 可通过两种方法来访问 <xref:Microsoft.Office.Tools.Ribbon.RibbonFactory> 对象：

- 通过使用功能区类的工厂属性。 可从 Ribbon 类中的代码使用此方法。

- 通过使用 `Globals.Factory.GetRibbonFactory` 方法。 可从 Ribbon 类外的代码使用此方法。 有关全局类的详细信息，请参阅[对 Office 项目中的对象的全局访问](../vsto/global-access-to-objects-in-office-projects.md)。

  下面的代码示例演示了如何在面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的项目中的 Ribbon 类中创建 <xref:Microsoft.Office.Tools.Ribbon.RibbonButton>。

\<CodeContentPlaceHolder > 10</CodeContentPlaceHolder> \<CodeContentPlaceHolder > 11</CodeContentPlaceHolder>下表列出了可以以编程方式创建的控件和要用于创建面向的项目中的控件的方法[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]或更高版本。

|控件|在 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 和更高版本的项目中使用的 RibbonFactory 方法|
|-------------| - |
|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonButton%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonButtonGroup>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonButtonGroup%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonCheckBox%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonComboBox%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonDialogLauncher>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonDialogLauncher%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>：|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonDropDown%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDownItem>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonDropDownItem%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonEditBox%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonGallery%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonGroup>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonGroup%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonLabel>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonLabel%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonManager>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonManager%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonMenu%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonSeparator>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonSeparator%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonSplitButton%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonTab%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonToggleButton%2A>|

## <a name="ribbonevents"></a> 处理功能区事件
 必须修改可以处理功能区控件的事件的任何代码。 在面向 .NET Framework 3.5 的项目中，这些事件由泛型 <xref:System.EventHandler%601> 委托处理。 在面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的项目中，这些事件现在由其他委托处理。

 下表列出了功能区事件以及在面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的项目中与它们关联的委托。

|Event|委托在 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 和更高版本的项目中使用|
|-----------| - |
|生成的 Ribbon 类中的 <xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon.LoadImage> 事件|<xref:Microsoft.Office.Tools.Ribbon.RibbonLoadImageEventHandler>|
|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon.Load>|<xref:Microsoft.Office.Tools.Ribbon.RibbonUIEventHandler>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton.Click><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox.Click><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox.ItemsLoading><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox.TextChanged><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown.ButtonClick><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown.ItemsLoading><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown.SelectionChanged><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox.TextChanged><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.ButtonClick><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.Click><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.ItemsLoading><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGroup.DialogLauncherClick><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu.ItemsLoading><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton.Click><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click>|<xref:Microsoft.Office.Tools.Ribbon.RibbonControlEventHandler>|

## <a name="set-the-position-of-a-ribbon-component-programmatically"></a>以编程方式设置的功能区组件位置
 必须修改可设置功能区组、选项卡或控件位置的任何代码。 在面向.NET Framework 3.5 的项目中，你可以使用静态 `Microsoft.Office.Tools.Ribbon.RibbonPosition` 类的 `AfterOfficeId` 和 `BeforeOfficeId` 方法来分配组、选项卡或控件的 `Position` 属性。 在面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的项目中，你必须通过使用由 <xref:Microsoft.Office.Tools.Ribbon.RibbonFactory> 对象提供的 <xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.RibbonPosition%2A> 属性来访问这些方法。

 可通过两种方法来访问 <xref:Microsoft.Office.Tools.Ribbon.RibbonFactory> 对象：

- 通过使用 Ribbon 类的 `Factory` 属性。 可从 Ribbon 类中的代码使用此方法。

- 通过使用 `Globals.Factory.GetRibbonFactory` 方法。 可从 Ribbon 类外的代码使用此方法。 有关全局类的详细信息，请参阅[对 Office 项目中的对象的全局访问](../vsto/global-access-to-objects-in-office-projects.md)。

  下面的代码示例演示了面向 .NET Framework 3.5 的项目中 Ribbon 类的选项卡的 `Position` 属性。

```vb
Me.tab1.Position = RibbonPosition.AfterOfficeId("TabHome")
```

```csharp
this.tab1.Position = RibbonPosition.AfterOfficeId("TabHome");
```

 下面的代码示例演示了面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 的项目中的相同任务。

```vb
Me.tab1.Position = Me.Factory.RibbonPosition.AfterOfficeId("TabHome")
```

```csharp
this.tab1.Position = this.Factory.RibbonPosition.AfterOfficeId("TabHome");
```

## <a name="see-also"></a>请参阅
- [迁移到.NET Framework 4 或更高版本的 Office 解决方案](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)
- [功能区设计器](../vsto/ribbon-designer.md)
