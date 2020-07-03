---
title: 创建选项页 |Microsoft Docs
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], creating
ms.assetid: 9f4e210c-4b47-4daa-91fa-1c301c4587f9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: be826b73e28a73216ea88ceba8e23eb1e9ea457b
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903812"
---
# <a name="create-an-options-page"></a>创建选项页

本演练将创建一个简单的 "工具/选项" 页，该页使用属性网格来检查和设置属性。

 若要将这些属性保存到并从设置文件还原它们，请执行以下步骤，然后参阅[创建设置类别](../extensibility/creating-a-settings-category.md)。

 MPF 提供了两个类来帮助你创建工具选项页、 <xref:Microsoft.VisualStudio.Shell.Package> 类和 <xref:Microsoft.VisualStudio.Shell.DialogPage> 类。 通过为类创建子类，创建 VSPackage 以为这些页面提供容器 `Package` 。 可以通过从类派生来创建每个 "工具选项" 页 `DialogPage` 。

## <a name="prerequisites"></a>必备条件

 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-tools-options-grid-page"></a>创建 "工具选项" 网格页

 在本部分中，将创建一个简单的 "工具选项" 属性网格。 使用此网格可以显示和更改属性的值。

### <a name="to-create-the-vsix-project-and-add-a-vspackage"></a>创建 VSIX 项目并添加 VSPackage

1. 每个 Visual Studio 扩展都从一个 VSIX 部署项目开始，该项目将包含扩展资产。 创建一个 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 名为的 VSIX 项目 `MyToolsOptionsExtension` 。 可以通过搜索 "vsix" 在 "**新建项目**" 对话框中找到 VSIX 项目模板。

2. 通过添加名为的 Visual Studio 包项模板来添加 VSPackage `MyToolsOptionsPackage` 。 在**解决方案资源管理器**中，右键单击项目节点，然后选择 "**添加**  >  **新项**"。 在 "**添加新项" 对话框**中，选择 " **visual c # 项**" "  >  **扩展性**"，然后选择 " **visual Studio 包**"。 在对话框底部的 "**名称**" 字段中，将文件名更改为 `MyToolsOptionsPackage.cs` 。 有关如何创建 VSPackage 的详细信息，请参阅[使用 VSPackage 创建扩展](../extensibility/creating-an-extension-with-a-vspackage.md)。

### <a name="to-create-the-tools-options-property-grid"></a>创建 "工具选项" 属性网格

1. 在代码编辑器中打开*MyToolsOptionsPackage*文件。

2. 添加以下 using 语句。

   ```csharp
   using System.ComponentModel;
   ```

3. 声明一个 `OptionPageGrid` 类，并从派生该类 <xref:Microsoft.VisualStudio.Shell.DialogPage> 。

   ```csharp
   public class OptionPageGrid : DialogPage
   {  }
   ```

4. 将应用 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> 到 `VSPackage` 类，以便将 OptionPageGrid 的选项类别和选项页名称分配给该类。 结果应如下所示：

    ```csharp
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)]
    [ProvideMenuResource("Menus.ctmenu", 1)]
    [Guid(GuidList.guidMyToolsOptionsPkgString)]
    [ProvideOptionPage(typeof(OptionPageGrid),
        "My Category", "My Grid Page", 0, 0, true)]
    public sealed class MyToolsOptionsPackage : Package
    ```

5. 将 `OptionInteger` 属性添加到 `OptionPageGrid` 类。

    - 应用 <xref:System.ComponentModel.CategoryAttribute?displayProperty=fullName> 以分配给属性 "属性" 网格类别。

    - 应用将 <xref:System.ComponentModel.DisplayNameAttribute?displayProperty=fullName> 分配给属性的名称。

    - 应用将 <xref:System.ComponentModel.DescriptionAttribute?displayProperty=fullName> 分配给属性的说明。

    ```csharp
    public class OptionPageGrid : DialogPage
    {
        private int optionInt = 256;

        [Category("My Category")]
        [DisplayName("My Integer Option")]
        [Description("My integer option")]
        public int OptionInteger
        {
            get { return optionInt; }
            set { optionInt = value; }
        }
    }
    ```

    > [!NOTE]
    > 的默认实现 <xref:Microsoft.VisualStudio.Shell.DialogPage> 支持具有适当转换器的属性，或者是可以扩展为具有适当转换器的属性的结构或数组的属性。 有关转换器的列表，请参阅 <xref:System.ComponentModel> 命名空间。

6. 生成项目并启动调试。

7. 在 Visual Studio 的实验实例中，单击 "**工具**" 菜单上的 "**选项**"。

     在左侧窗格中，应会看到 **"我的类别**"。 （选项类别按字母顺序列出，因此它应显示在列表中的下一半。）打开 **"我的类别**"，然后单击 **"我的网格" 页**。 选项网格将显示在右窗格中。 "属性" 类别为 "**我的选项**"，属性名称为 **"我的整数" 选项**。 属性说明 "**我的整数" 选项**显示在窗格的底部。 将值从其初始值256更改为其他值。 单击 **"确定"**，然后重新打开**网格页**。 您可以看到新值仍然存在。

     还可以通过 Visual Studio 的搜索框使用 "选项" 页。 在 IDE 顶部附近的 "搜索" 框中，键入 **"我的类别**"，将看到 "我的**网格" 页**在结果中列出 >。

## <a name="create-a-tools-options-custom-page"></a>创建 "工具选项" 自定义页面

 在本部分中，将使用自定义 UI 创建 "工具选项" 页。 使用此页可以显示和更改属性的值。

1. 在代码编辑器中打开*MyToolsOptionsPackage*文件。

2. 添加以下 using 语句。

    ```csharp
    using System.Windows.Forms;
    ```

3. 在 `OptionPageCustom` 类的前面添加一个类 `OptionPageGrid` 。 从派生新类 `DialogPage` 。

    ```csharp
    public class OptionPageCustom : DialogPage
    {
        private string optionValue = "alpha";

        public string OptionString
        {
            get { return optionValue; }
            set { optionValue = value; }
        }
    }
    ```

4. 添加 GUID 属性。 添加 OptionString 属性：

    ```csharp
    [Guid("00000000-0000-0000-0000-000000000000")]
    public class OptionPageCustom : DialogPage
    {
        private string optionValue = "alpha";

        public string OptionString
        {
            get { return optionValue; }
            set { optionValue = value; }
        }
    }
    ```

5. 将第二个应用 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> 到 VSPackage 类。 此属性为类分配选项类别和选项页名称。

    ```csharp
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)]
    [ProvideMenuResource("Menus.ctmenu", 1)]
    [Guid(GuidList.guidMyToolsOptionsPkgString)]
    [ProvideOptionPage(typeof(OptionPageGrid),
        "My Category", "My Grid Page", 0, 0, true)]
    [ProvideOptionPage(typeof(OptionPageCustom),
        "My Category", "My Custom Page", 0, 0, true)]
    public sealed class MyToolsOptionsPackage : Package
    ```

6. 将名为 MyUserControl 的新**用户控件**添加到项目。

7. 向用户控件添加**TextBox**控件。

     在 "**属性**" 窗口的工具栏上，单击 "**事件**" 按钮，然后双击 "**离开**" 事件。 新的事件处理程序显示在*MyUserControl.cs*代码中。

8. 向 `OptionsPage` control 类添加公共字段 `Initialize` 和方法，并更新事件处理程序，以将选项值设置为文本框的内容：

    ```csharp
    public partial class MyUserControl : UserControl
    {
        public MyUserControl()
        {
            InitializeComponent();
        }

        internal OptionPageCustom optionsPage;

        public void Initialize()
        {
            textBox1.Text = optionsPage.OptionString;
        }

        private void textBox1_Leave(object sender, EventArgs e)
        {
            optionsPage.OptionString = textBox1.Text;
        }
    }
    ```

     `optionsPage`字段保存对父实例的引用 `OptionPageCustom` 。 `Initialize`方法 `OptionString` 在**文本框**中显示。 **TextBox** `OptionString` 当焦点离开**textbox**时，事件处理程序会将文本框的当前值写入。

9. 在包代码文件中，将属性的替代添加 `OptionPageCustom.Window` 到类， `OptionPageCustom` 以创建、初始化和返回的实例 `MyUserControl` 。 该类现在应如下所示：

    ```csharp
    [Guid("00000000-0000-0000-0000-000000000000")]
    public class OptionPageCustom : DialogPage
    {
        private string optionValue = "alpha";

        public string OptionString
        {
            get { return optionValue; }
            set { optionValue = value; }
        }

        protected override IWin32Window Window
        {
            get
            {
                MyUserControl page = new MyUserControl();
                page.optionsPage = this;
                page.Initialize();
                return page;
            }
        }
    }
    ```

10. 生成并运行该项目。

11. 在实验实例中，单击 "**工具**" "  >  **选项**"。

12. 查找**我的类别**，然后查找**我的自定义页面**。

13. 更改**OptionString**的值。 单击 **"确定"**，然后重新打开**自定义页面**。 您可以看到新值已保存。

## <a name="access-options"></a>访问选项

 在本部分中，将从承载 "关联的工具选项" 页的 VSPackage 获取选项的值。 可以使用相同的方法来获取任何公共属性的值。

1. 在包代码文件中，将名为**OptionInteger**的公共属性添加到**MyToolsOptionsPackage**类。

    ```csharp
    public int OptionInteger
    {
        get
        {
            OptionPageGrid page = (OptionPageGrid)GetDialogPage(typeof(OptionPageGrid));
            return page.OptionInteger;
        }
    }

    ```

     此代码调用 <xref:Microsoft.VisualStudio.Shell.Package.GetDialogPage%2A> 来创建或检索 `OptionPageGrid` 实例。 `OptionPageGrid`调用 <xref:Microsoft.VisualStudio.Shell.DialogPage.LoadSettingsFromStorage%2A> 以加载其选项，这些选项是公共属性。

2. 现在，添加一个名为**MyToolsOptionsCommand**的自定义命令项模板以显示值。 在 "**添加新项**" 对话框中，选择 " **Visual c #**  >  **扩展性**" 并选择 "**自定义命令**"。 在窗口底部的 "**名称**" 字段中，将命令文件名更改为*MyToolsOptionsCommand.cs*。

3. 在*MyToolsOptionsCommand*文件中，将命令的方法的主体替换 `ShowMessageBox` 为以下内容：

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
        MyToolsOptionsPackage myToolsOptionsPackage = this.package as MyToolsOptionsPackage;
        System.Windows.Forms.MessageBox.Show(string.Format(CultureInfo.CurrentCulture, "OptionInteger: {0}", myToolsOptionsPackage.OptionInteger));
    }

    ```

4. 生成项目并启动调试。

5. 在实验实例中，单击 "**工具**" 菜单上的 "**调用 MyToolsOptionsCommand**"。

     将显示一个消息框，其中显示的当前值 `OptionInteger` 。

## <a name="see-also"></a>另请参阅

- [选项和选项页](../extensibility/internals/options-and-options-pages.md)
