---
title: 创建设置类别 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- profile settings, creating categories
ms.assetid: 97c88693-05ff-499e-8c43-352ee073dcb7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 03d50ca998efa034b1d4392c1fb7cecb8de8ed06
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904029"
---
# <a name="create-a-settings-category"></a>创建设置类别

在本演练中，您将创建一个 Visual Studio 设置类别，并使用它将值保存到并从设置文件还原值。 设置类别是一组显示为 "自定义设置点" 的相关属性;即**导入和导出设置**向导中的复选框。 （您可以在 "**工具**" 菜单上找到它。）设置会作为类别进行保存或还原，并且不会在向导中显示各个设置。 有关详细信息，请参阅[环境设置](../ide/environment-settings.md)。

您可以通过从类中派生来创建设置类别 <xref:Microsoft.VisualStudio.Shell.DialogPage> 。

若要开始本演练，必须先完成 "[创建选项" 页面](../extensibility/creating-an-options-page.md)的第一个部分。 "生成的选项" 属性网格使你可以检查和更改类别中的属性。 将属性类别保存到设置文件中后，将检查该文件以查看属性值的存储方式。

## <a name="prerequisites"></a>必备条件
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-settings-category"></a>创建设置类别
 在本部分中，将使用自定义设置点保存和还原 "设置" 类别的值。

### <a name="to-create-a-settings-category"></a>创建设置类别

1. 完成 "[创建选项" 页](../extensibility/creating-an-options-page.md)。

2. 打开*VSPackage*文件并添加以下三个字符串资源：

    |名称|值|
    |----------|-----------|
    |106|我的类别|
    |107|我的设置|
    |108|OptionInteger 和 OptionFloat|

     这会创建将类别命名为 "我的类别"、对象 "我的设置" 和类别说明 "OptionInteger and OptionFloat" 的资源。

    > [!NOTE]
    > 在这三种情况下，"**导入和导出设置**向导" 中将不显示类别名称。

3. 在*MyToolsOptionsPackage.cs*中，将一个 `float` 名为的属性添加 `OptionFloat` 到 `OptionPageGrid` 类，如下面的示例中所示。

    ```csharp
    public class OptionPageGrid : DialogPage
    {
        private int optionInt = 256;
        private float optionFloat = 3.14F;

        [Category("My Options")]
        [DisplayName("My Integer option")]
        [Description("My integer option")]
        public int OptionInteger
        {
            get { return optionInt; }
            set { optionInt = value; }
        }
        [Category("My Options")]
        [DisplayName("My Float option")]
        [Description("My float option")]
        public float OptionFloat
        {
            get { return optionFloat; }
            set { optionFloat = value; }
        }
    }
    ```

    > [!NOTE]
    > `OptionPageGrid`名为 "My category" 的类别现在包含两个属性，即 `OptionInteger` 和 `OptionFloat` 。

4. 将添加 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> 到 `MyToolsOptionsPackage` 类，并将其命名为 "my Category"，为其指定 ObjectName "my Settings"，并将 isToolsOptionPage 设置为 true。 将 categoryResourceID、objectNameResourceID 和 DescriptionResourceID 设置为前面创建的相应字符串资源 Id。

    ```csharp
    [ProvideProfileAttribute(typeof(OptionPageGrid),
        "My Category", "My Settings", 106, 107, isToolsOptionPage:true, DescriptionResourceID = 108)]
    ```

5. 生成项目并启动调试。 在实验实例中，应会看到 **"我的网格" 页**现在包含整数值和浮点值。

## <a name="examine-the-settings-file"></a>检查设置文件
 在本部分中，将属性类别值导出到设置文件。 检查该文件，然后将这些值导入回属性类别。

1. 通过按**F5**在调试模式下启动项目。 这将启动实验实例。

2. 打开 "**工具**  >  **选项**" 对话框。

3. 在左侧窗格中的树视图中，展开 **"我的类别**"，然后单击 **"我的网格" 页**。

4. 将**OptionFloat**的值更改为3.1416，将**OptionInteger**更改为12。 单击 **“确定”** 。

5. 在“工具”菜单上，单击“导入和导出设置”。

     此时将显示**导入和导出设置**向导。

6. 确保选中 "**导出所选环境设置**"，然后单击 "**下一步**"。

     此时将显示 "**选择要导出的设置**" 页。

7. 单击 **"我的设置"**。

     **说明**更改为 " **OptionInteger" 和 "OptionFloat**"。

8. 请确保 "**我的设置**" 是所选的唯一类别，然后单击 "**下一步**"。

     显示**设置文件**页的名称。

9. 将新的设置文件命名为*mysetting* ，并将其保存到相应的目录中。 单击“完成”。

     "**导出完成**" 页将报告你的设置已成功导出。

10. 在“文件”**** 菜单中，指向“打开”****，再单击“文件”****。 找到*mysetting .vssettings*并将其打开。

     可以在文件的以下部分中找到导出的属性类别（Guid 将有所不同）。

    ```
    <Category name="My Category_My Settings"
          Category="{4802bc3e-3d9d-4591-8201-23d1a05216a6}"
          Package="{6bb6942e-014c-489e-a612-a935680f703d}"
          RegisteredName="My Category_My Settings">
          PackageName="MyToolsOptionsPackage">
       <PropertyValue name="OptionFloat">3.1416</PropertyValue>
       <PropertyValue name="OptionInteger">12</PropertyValue>
    </Category>
    ```

     请注意，通过将下划线添加到类别名称后接对象名称，来形成完整的类别名称。 "OptionFloat" 和 "OptionInteger" 显示在 "类别" 中，及其导出值。

11. 关闭设置文件而不进行更改。

12. 在 "**工具**" 菜单上，依次单击 "**选项**"、 **"我的类别**"、"**我的网格" 页**，然后将**OptionFloat**的值更改为1.0，并将**OptionInteger**更改为1。 单击 **“确定”** 。

13. 单击 "**工具**" 菜单上的 "**导入和导出设置**"，选择 "**导入选定的环境设置**"，然后单击 "**下一步**"

     此时将显示 "**保存当前设置**" 页。

14. 选择 **"否，仅导入新设置"** ，然后单击 "**下一步**"。

     此时将显示 "**选择要导入的设置集合**" 页。

15. 在树视图的 "**我的设置**" 节点中选择 " *mysetting" .vssettings*文件。 如果该文件未出现在树视图中，请单击 "**浏览**" 并找到该文件。 单击“下一步”。

     此时将显示 "**选择要导入的设置**" 对话框。

16. 请确保选择 **"我的设置**"，然后单击 "**完成**"。 出现 "**导入完成**" 页后，单击 "**关闭**"。

17. 在 "**工具**" 菜单上，依次单击 "**选项**"、 **"我的类别**"、"**我的网格页**" 和 "验证属性类别值已还原"。
