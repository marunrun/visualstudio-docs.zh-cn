---
title: 迁移到 .NET Framework 4.5 时更新 Outlook 窗体区域
titleSuffix: ''
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
ms.openlocfilehash: 9d8978703630e99ecb930e18e7d128eddff8792f
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91584394"
---
# <a name="update-outlook-form-regions-when-migrated-to-net-framework-45"></a>迁移到 .NET Framework 4.5 时更新 Outlook 窗体区域

  如果具有窗体区域的 Outlook VSTO 外接程序项目的目标框架更改为 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本，则必须对生成的窗体区域代码和在运行时实例化某些窗体区域类的任何代码进行更改。

## <a name="update-the-generated-form-region-code"></a>更新生成的窗体区域代码
 如果该项目的目标框架更改为 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本，则必须更改生成的窗体区域代码。 对在 Visual Studio 中设计的窗体区域和从 Outlook 导入的窗体区域所做的更改是不同的。 有关这些类型的窗体区域之间的差异的详细信息，请参阅 [创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)。

### <a name="to-update-the-generated-code-for-a-form-region-that-you-designed-in-visual-studio"></a>若要更新在 Visual Studio 中设计的窗体区域的生成代码

1. 在代码编辑器中打开窗体区域代码隐藏文件。 此文件命名为 *YourFormRegion*.Designer.cs 或 *YourFormRegion*.Designer.vb。 若要在 Visual Basic 项目中查看此文件，可单击 **“解决方案资源管理器”** 中的 **“显示全部文件”** 按钮。

2. 修改窗体区域类的声明，以便它从 <xref:Microsoft.Office.Tools.Outlook.FormRegionBase> 而不是从 `Microsoft.Office.Tools.Outlook.FormRegionControl` 派生。

3. 修改窗体区域类的构造函数，如下面的代码示例中所示。

     下面的代码示例演示了面向 .NET Framework 3.5 的项目中的窗体区域类的构造函数。

    ```vb
    Public Sub New(ByVal formRegion As Microsoft.Office.Interop.Outlook.FormRegion)
        MyBase.New(formRegion)
        Me.InitializeComponent()
    End Sub
    ```

    ```csharp
    public FormRegion1(Microsoft.Office.Interop.Outlook.FormRegion formRegion)
        : base(formRegion)
    {
        this.InitializeComponent();
    }
    ```

     下面的代码示例演示了面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]的项目中的窗体区域类的构造函数。

    ```vb
    Public Sub New(ByVal formRegion As Microsoft.Office.Interop.Outlook.FormRegion)
        MyBase.New(Globals.Factory, formRegion)
        Me.InitializeComponent()
    End Sub
    ```

    ```csharp
    public FormRegion1(Microsoft.Office.Interop.Outlook.FormRegion formRegion)
        : base(Globals.Factory, formRegion)
    {
        this.InitializeComponent();
    }
    ```

4. 如下所示修改 `InitializeManifest` 方法的签名。 请确保不要修改方法中的代码；此代码表示在设计器中应用的窗体区域设置。 在 Visual C# 项目中，必须展开名为 `Form Region Designer generated code` 的区域区才能查看此方法。

     下面的代码示例演示了面向 .NET Framework 3.5 的项目中的 `InitializeManifest` 方法的签名。

    ```vb
    Private Shared Sub InitializeManifest(ByVal manifest As Microsoft.Office.Tools.Outlook.FormRegionManifest)

        ' Do not change code in this method.
    End Sub
    ```

    ```csharp
    private static void InitializeManifest(Microsoft.Office.Tools.Outlook.FormRegionManifest manifest)
    {
        // Do not change code in this method.
    }
    ```

     下面的代码示例演示了面向 `InitializeManifest` 的项目中的 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]方法的签名。

    ```vb
    Private Shared Sub InitializeManifest(ByVal manifest As Microsoft.Office.Tools.Outlook.FormRegionManifest,
        ByVal factory As Microsoft.Office.Tools.Outlook.Factory)

        ' Do not change code in this method.
    End Sub
    ```

    ```csharp
    private static void InitializeManifest(Microsoft.Office.Tools.Outlook.FormRegionManifest manifest,
        Microsoft.Office.Tools.Outlook.Factory factory)
    {
        // Do not change code in this method.
    }
    ```

5. 将新的 Outlook 窗体区域项添加到项目。 打开新窗体区域的代码隐藏文件，在文件中找到*YourNewFormRegion* `Factory` 和 `WindowFormRegionCollection` 类，然后将这些类复制到剪贴板。

6. 删除添加到项目的新窗体区域。

7. 在要更新的窗体区域的代码隐藏文件中，将其放在重定目标的项目中，找到*YourOriginalFormRegion* `Factory` 和 `WindowFormRegionCollection` 类并将它们替换为从新的窗体区域复制的代码。

8. 在*YourNewFormRegion* `Factory` 和 `WindowFormRegionCollection` 类中，搜索对*YourNewFormRegion*类的所有引用并改为更改对*YourOriginalFormRegion*类的每个引用。 例如，如果正在更新的窗体区域名为 `SalesDataFormRegion` 且在步骤 5 中创建的新窗体区域名为 `FormRegion1`，则将 `FormRegion1` 的所有引用更改为 `SalesDataFormRegion`。

#### <a name="to-update-the-generated-code-for-a-form-region-that-you-imported-from-outlook"></a>若要更新从 Outlook 导入的窗体区域的生成代码

1. 在代码编辑器中打开窗体区域代码隐藏文件。 此文件命名为 *YourFormRegion*.Designer.cs 或 *YourFormRegion*.Designer.vb。 若要在 Visual Basic 项目中查看此文件，可单击 **“解决方案资源管理器”** 中的 **“显示全部文件”** 按钮。

2. 修改窗体区域类的声明，以便它从 <xref:Microsoft.Office.Tools.Outlook.ImportedFormRegionBase> 而不是从 `Microsoft.Office.Tools.Outlook.ImportedFormRegion` 派生。

3. 修改窗体区域类的构造函数，如下面的代码示例中所示。

     下面的代码示例演示了面向 .NET Framework 3.5 的项目中的窗体区域类的构造函数。

    ```vb
    Public Sub New(ByVal formRegion As Microsoft.Office.Interop.Outlook.FormRegion)
        MyBase.New(formRegion)
    End Sub
    ```

    ```csharp
    public ImportedFormRegion1(Microsoft.Office.Interop.Outlook.FormRegion formRegion)
        : base(formRegion)
    {
        this.FormRegionShowing += new System.EventHandler(this.TaskFormRegion_FormRegionShowing);
        this.FormRegionClosed += new System.EventHandler(this.TaskFormRegion_FormRegionClosed);
    }
    ```

     下面的代码示例演示了面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]的项目中的窗体区域类的构造函数的签名。

    ```vb
    Public Sub New(ByVal formRegion As Microsoft.Office.Interop.Outlook.FormRegion)
        MyBase.New(Globals.Factory, formRegion)
    End Sub
    ```

    ```csharp
    public ImportedFormRegion1(Microsoft.Office.Interop.Outlook.FormRegion formRegion)
        : base(Globals.Factory, formRegion)
    {
        this.FormRegionShowing += new System.EventHandler(this.TaskFormRegion_FormRegionShowing);
        this.FormRegionClosed += new System.EventHandler(this.TaskFormRegion_FormRegionClosed);
    }
    ```

4. 对于初始化窗体区域类中控件的 `InitializeControls` 方法中的每一行代码，如下所示修改代码。

     下面的代码示例演示如何初始化面向 .NET Framework 3.5 的项目中的控件。 在此代码中，`GetFormRegionControl` 方法具有指定返回的控件类型的类型参数。

    ```vb
    Me.olkTextBox1 = Me.GetFormRegionControl(Of Microsoft.Office.Interop.Outlook.OlkTextBox)("OlkTextBox1")
    ```

    ```csharp
    this.olkTextBox1 = this.GetFormRegionControl<Microsoft.Office.Interop.Outlook.OlkTextBox>("OlkTextBox1");
    ```

     下面的代码示例演示如何初始化面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]的项目中的控件。 在此代码中， <xref:Microsoft.Office.Tools.Outlook.ImportedFormRegionBase.GetFormRegionControl%2A> 方法不具有类型参数。 必须将返回值强制转换为正在初始化的控件的类型。

    ```vb
    Me.olkTextBox1 = CType(GetFormRegionControl("OlkTextBox1"), Microsoft.Office.Interop.Outlook.OlkTextBox)
    ```

    ```csharp
    this.olkTextBox1 = (Microsoft.Office.Interop.Outlook.OlkTextBox)GetFormRegionControl("OlkTextBox1");
    ```

5. 将新的 Outlook 窗体区域项添加到项目。 打开新窗体区域的代码隐藏文件，在文件中找到*YourNewFormRegion* `Factory` 和 `WindowFormRegionCollection` 类，然后将这些类复制到剪贴板。

6. 删除添加到项目的新窗体区域。

7. 在要更新的窗体区域的代码隐藏文件中，将其放在重定目标的项目中，找到*YourOriginalFormRegion* `Factory` 和 `WindowFormRegionCollection` 类并将它们替换为从新的窗体区域复制的代码。

8. 在*YourNewFormRegion* `Factory` 和 `WindowFormRegionCollection` 类中，搜索对*YourNewFormRegion*类的所有引用并改为更改对*YourOriginalFormRegion*类的每个引用。 例如，如果正在更新的窗体区域名为 `SalesDataFormRegion` 且在步骤 5 中创建的新窗体区域名为 `FormRegion1`，则将 `FormRegion1` 的所有引用更改为 `SalesDataFormRegion`。

## <a name="instantiate-form-region-classes"></a>实例化窗体区域类
 必须修改动态实例化某些窗体区域类的任何代码。 在面向 .NET Framework 3.5 的项目中，你可以直接实例化窗体区域类（比如 `Microsoft.Office.Tools.Outlook.FormRegionManifest`）。 在面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的项目中，这些类是你无法直接实例化的接口。

 如果项目的目标框架更改为 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本，则必须使用 `Globals.Factory` 属性提供的方法实例化这些接口。 有关属性的详细信息 `Globals.Factory` ，请参阅 [对 Office 项目中对象的全局访问](../vsto/global-access-to-objects-in-office-projects.md)。

 下表列出了要用于实例化面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的项目中的类型的窗体区域类型和方法。

|类型|要使用的工厂方法|
|----------|---------------------------|
|<xref:Microsoft.Office.Tools.Outlook.FormRegionCustomAction>|<xref:Microsoft.Office.Tools.Outlook.Factory.CreateFormRegionCustomAction%2A>|
|<xref:Microsoft.Office.Tools.Outlook.FormRegionInitializingEventArgs>|<xref:Microsoft.Office.Tools.Outlook.Factory.CreateFormRegionInitializingEventArgs%2A>|
|<xref:Microsoft.Office.Tools.Outlook.FormRegionManifest>|<xref:Microsoft.Office.Tools.Outlook.Factory.CreateFormRegionManifest%2A>|

## <a name="see-also"></a>另请参阅
- [将 Office 解决方案迁移到 .NET Framework 4 或更高版本](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)
- [创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)
