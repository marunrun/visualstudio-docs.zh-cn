---
title: 创建设置类别 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profile settings, creating categories
ms.assetid: 97c88693-05ff-499e-8c43-352ee073dcb7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5f4b2fa9d82181d0eb899bf9680e8a9debd6c50b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739606"
---
# <a name="create-a-settings-category"></a>创建设置类别

在本演练中，您将创建 Visual Studio 设置类别，并用它来将值保存到设置文件中并将值还原。 设置类别是显示为"自定义设置点"的相关属性的一组;即，作为 **"导入和导出设置"** 向导中的复选框。 （您可以在 **"工具"** 菜单中找到它。设置将作为类别保存或还原，并且单个设置不会显示在向导中。 有关详细信息，请参阅[环境设置](../ide/environment-settings.md)。

通过从类派生设置类别来<xref:Microsoft.VisualStudio.Shell.DialogPage>创建设置类别。

要开始本演练，必须首先完成["创建选项"页的第一](../extensibility/creating-an-options-page.md)部分。 生成的 Options 属性网格允许您检查和更改类别中的属性。 在设置文件中保存属性类别后，将检查该文件以查看属性值的存储方式。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-settings-category"></a>创建设置类别
 在本节中，您可以使用自定义设置点来保存和恢复设置类别的值。

### <a name="to-create-a-settings-category"></a>创建设置类别

1. 完成["创建选项"页](../extensibility/creating-an-options-page.md)。

2. 打开*VSPackage.resx*文件并添加以下三个字符串资源：

    |“属性”|“值”|
    |----------|-----------|
    |106|我的类别|
    |107|我的设置|
    |108|选项整数和期权浮动|

     这将创建名称为"我的类别"类别、对象"我的设置"和类别描述"Optioninger 和 OptionFloat"的资源。

    > [!NOTE]
    > 在这三个中，只有类别名称不会出现在 **"导入和导出设置"向导中**。

3. 在*MyToolsOptionsPackage.cs*中`float`，向`OptionFloat``OptionPageGrid`类添加名为的属性，如以下示例所示。

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
    > 名为`OptionPageGrid`"我的类别"的类别现在由两个属性`OptionInteger`和`OptionFloat`。

4. 向`MyToolsOptionsPackage`类<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>添加 a 并给它"我的类别"类别名称，将其命名为"我的设置"，并将"ToolsOptionPage"设置为 true。 将类别 ResourceID、对象名称资源 ID 和描述资源ID 设置为前面创建的相应字符串资源 ID。

    ```csharp
    [ProvideProfileAttribute(typeof(OptionPageGrid),
        "My Category", "My Settings", 106, 107, isToolsOptionPage:true, DescriptionResourceID = 108)]
    ```

5. 生成项目并启动调试。 在实验实例中，您应该看到 **"我的网格页**"现在同时具有整数和浮点值。

## <a name="examine-the-settings-file"></a>检查设置文件
 在本节中，您将属性类别值导出到设置文件。 检查文件，然后将值导入属性类别。

1. 通过按**F5**在调试模式下启动项目。 这将启动实验实例。

2. 打开 **"工具** > **选项"** 对话框。

3. 在左侧窗格中的树视图中，展开 **"我的类别"，** 然后单击"**我的网格页**"。

4. 将**OptionFloat**的值更改为 3.1416，将**选项 Integer**更改为 12。 单击“确定”。

5. 在“工具”**** 菜单上，单击“导入和导出设置”****。

     将显示"**导入和导出设置"** 向导。

6. 确保选择了 **"导出选定的环境设置**"，然后单击"**下一步**"。

     将显示 **"选择要导出的设置**"页。

7. 单击 **"我的设置**"。

     **描述**更改为**选项Integer和 OptionFloat**。

8. 请确保 **"我的设置"** 是唯一被选中的类别，然后单击"**下一步**"。

     将显示"**设置文件名称"** 页。

9. 命名新设置文件*MySettings.vs 设置*并将其保存在相应的目录中。 单击“完成”  。

     "**导出完整"** 页报告您的设置已成功导出。

10. 在“文件”**** 菜单中，指向“打开”****，再单击“文件”****。 找到 *"我的设置"，* 然后打开它。

     您可以在文件的以下部分找到导出的属性类别（您的 GUID 会有所不同）。

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

     请注意，整个类别名称是通过向类别名称添加下划线后跟对象名称来形成。 选项 Float 和 OptionInteger 及其导出的值将显示在类别中。

11. 关闭设置文件而不更改它。

12. 在 **"工具"** 菜单上，**单击"选项**"展开**我的类别**，单击 **"我的网格页面**"，然后将**OptionFloat**的值更改为 1.0，将**OptionInteger**更改为 1。 单击“确定”。

13. 在 **"工具"** 菜单上，单击"**导入和导出设置**"，选择 **"导入选定的环境设置**"，然后单击"**下一步**"。

     将显示"**保存当前设置"** 页。

14. 选择 **"否"，只需导入新设置**，然后单击"**下一步**"。

     将显示 **"选择要导入的设置集合**"。

15. 在树视图的"**我的设置"** 节点中选择 *"MySettings.vs 设置"* 文件。 如果文件未显示在树视图中，请单击"**浏览"** 并查找它。 单击“下一步”。 

     将显示 **"选择"以导入"** 对话框。

16. 确保选择了 **"我的设置"，** 然后单击"**完成**"。 当"**导入完成"** 页出现时，单击"**关闭**"。

17. 在 **"工具"** 菜单上，**单击"选项**"展开**我的类别**"，单击 **"我的网格页面"** 并验证属性类别值是否已还原。
