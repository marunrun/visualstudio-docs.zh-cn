---
title: 创建选项页面 |微软文档
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], creating
ms.assetid: 9f4e210c-4b47-4daa-91fa-1c301c4587f9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1607af2a6f68bd5593f9a185188b25b364926fe4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739513"
---
# <a name="create-an-options-page"></a>创建选项页

本演练创建一个简单的工具/选项页，该页使用属性网格来检查和设置属性。

 要将这些属性保存到设置文件中并从中还原它们，请按照以下步骤操作，然后请参阅[创建设置类别](../extensibility/creating-a-settings-category.md)。

 MPF 提供两个类，以帮助您创建工具选项页、<xref:Microsoft.VisualStudio.Shell.Package>类和<xref:Microsoft.VisualStudio.Shell.DialogPage>类。 通过对类进行子类分类，`Package`创建 VSPackage 为这些页面提供容器。 通过派生`DialogPage`类创建每个工具选项页。

## <a name="prerequisites"></a>先决条件

 从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-tools-options-grid-page"></a>创建工具选项网格页

 在本节中，您将创建一个简单的工具选项属性网格。 使用此网格可以显示和更改属性的值。

### <a name="to-create-the-vsix-project-and-add-a-vspackage"></a>创建 VSIX 项目并添加 VS 包

1. 每个 Visual Studio 扩展都从 VSIX 部署项目开始，该项目将包含扩展资产。 创建[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]名为 的`MyToolsOptionsExtension`VSIX 项目。 您可以通过搜索"vsix"在 **"新项目**"对话框中找到 VSIX 项目模板。

2. 通过添加名为 的`MyToolsOptionsPackage`可视化工作室包项目模板来添加 VS 包。 在**解决方案资源管理器**中，右键单击项目节点并选择"**添加新** > **项**"。 在 **"添加新项目"对话框**中，转到**可视化 C# 项目** > **扩展性**并选择**可视化工作室包**。 在对话框底部的 **"名称"** 字段中，将文件名更改为`MyToolsOptionsPackage.cs`。 有关如何创建 VSPackage 的详细信息，请参阅[使用 VSPackage 创建扩展](../extensibility/creating-an-extension-with-a-vspackage.md)。

### <a name="to-create-the-tools-options-property-grid"></a>创建"工具选项"属性网格

1. 在代码编辑器中打开*MyToolsOptions 包*文件。

2. 使用 语句添加以下内容。

   ```csharp
   using System.ComponentModel;
   ```

3. 声明类`OptionPageGrid`并从 派生它<xref:Microsoft.VisualStudio.Shell.DialogPage>。

   ```csharp
   public class OptionPageGrid : DialogPage
   {  }
   ```

4. 将<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>应用`VSPackage`到 类以为选项页网格向类分配选项类别和选项页名称。 结果应如下所示：

    ```csharp
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)]
    [ProvideMenuResource("Menus.ctmenu", 1)]
    [Guid(GuidList.guidMyToolsOptionsPkgString)]
    [ProvideOptionPage(typeof(OptionPageGrid),
        "My Category", "My Grid Page", 0, 0, true)]
    public sealed class MyToolsOptionsPackage : Package
    ```

5. 向`OptionPageGrid`类`OptionInteger`添加属性。

    - 应用<xref:System.ComponentModel.CategoryAttribute?displayProperty=fullName>以将 属性网格类别分配给属性。

    - 应用<xref:System.ComponentModel.DisplayNameAttribute?displayProperty=fullName>以向属性分配名称。

    - 应用<xref:System.ComponentModel.DescriptionAttribute?displayProperty=fullName>以将 说明分配给属性。

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
    > 默认实现 支持<xref:Microsoft.VisualStudio.Shell.DialogPage>具有适当转换器或结构或数组的属性，这些属性可以扩展到具有适当转换器的属性。 有关转换器列表，请参阅<xref:System.ComponentModel>命名空间。

6. 生成项目并启动调试。

7. 在 Visual Studio 的实验实例中，在 **"工具"** 菜单上单击 **"选项**"。

     在左侧窗格中，应看到 **"我的类别**"。 （选项类别按字母顺序列出，因此应显示列表的中途。打开**我的类别**，然后单击**我的网格页面**。 选项网格显示在右侧窗格中。 属性类别是 **"我的选项**"，属性名称为 **"我的整数选项**"。 属性描述"**我的整数"选项**将显示在窗格的底部。 将值从初始值 256 更改为其他值。 单击 **"确定**"，然后重新打开 **"我的网格页面**"。 您可以看到新值仍然存在。

     您的选项页面也可通过 Visual Studio 的搜索框获得。 在 IDE 顶部附近的搜索框中，键入 **"我的类别"，** 您将看到结果中列出的 **"我的类别 ->我的网格页面**"。

## <a name="create-a-tools-options-custom-page"></a>创建工具选项自定义页面

 在本节中，您将创建一个包含自定义 UI 的工具选项页面。 使用此页面显示和更改属性的值。

1. 在代码编辑器中打开*MyToolsOptions 包*文件。

2. 使用 语句添加以下内容。

    ```csharp
    using System.Windows.Forms;
    ```

3. 在`OptionPageGrid`类`OptionPageCustom`之前添加一个类。 派生新类从`DialogPage`。

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

5. 将第二<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>个应用到 VSPackage 类。 此属性为类分配一个选项类别和选项页名称。

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

6. 向项目添加新**的用户控件**，称为 MyUserControl。

7. 将**TextBox**控件添加到用户控件。

     在工具栏上的"**属性"** 窗口中，单击"**事件"** 按钮，然后双击 **"离开**"事件。 新的事件处理程序将显示在*MyUserControl.cs*代码中。

8. 将公共`OptionsPage`字段（方法`Initialize`）添加到控件类，并更新事件处理程序以将选项值设置为文本框的内容：

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

     该`optionsPage`字段包含对父`OptionPageCustom`实例的引用。 该方法`Initialize`显示在`OptionString` **TextBox**中。 当焦点离开**TextBox**时，`OptionString`事件处理程序将**TextBox**的当前值写入 。

9. 在包代码文件中，向`OptionPageCustom.Window``OptionPageCustom`类添加属性的重写以创建、初始化和返回 的`MyUserControl`实例。 类现在应如下所示：

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

11. 在实验实例中，单击 **"工具** > **选项**"。

12. 找到**我的类别**，然后**我的自定义页面**。

13. 更改**OptionString**的值。 单击 **"确定**"，然后重新打开 **"我的自定义页面**"。 您可以看到新值已保留。

## <a name="access-options"></a>访问选项

 在本节中，从承载关联的工具选项页的 VSPackage 中获取选项的值。 相同的技术可用于获取任何公共属性的值。

1. 在包代码文件中，向**MyToolsOptions 包**类添加名为**OptionInteger**的公共属性。

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

     此代码调用<xref:Microsoft.VisualStudio.Shell.Package.GetDialogPage%2A>以创建或检索`OptionPageGrid`实例。 `OptionPageGrid`调用<xref:Microsoft.VisualStudio.Shell.DialogPage.LoadSettingsFromStorage%2A>以加载其选项，即公共属性。

2. 现在添加名为**MyToolsOptions命令**的自定义命令项模板以显示该值。 在"**添加新项目"** 对话框中，转到**可视化 C#** > **扩展性**并选择 **"自定义命令**"。 在窗口底部的 **"名称"** 字段中，将命令文件名更改为*MyToolsOptionsCommand.cs*。

3. 在*MyToolsOptionsCommand*文件中，将命令`ShowMessageBox`方法的正文替换为以下内容：

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
        MyToolsOptionsPackage myToolsOptionsPackage = this.package as MyToolsOptionsPackage;
        System.Windows.Forms.MessageBox.Show(string.Format(CultureInfo.CurrentCulture, "OptionInteger: {0}", myToolsOptionsPackage.OptionInteger));
    }

    ```

4. 生成项目并启动调试。

5. 在实验实例中，在 **"工具"** 菜单上，单击 **"调用我的工具选项命令**"。

     消息框显示 的`OptionInteger`当前值。

## <a name="see-also"></a>请参阅

- [选项和选项页](../extensibility/internals/options-and-options-pages.md)
