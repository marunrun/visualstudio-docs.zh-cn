---
title: 创建设置类别 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profile settings, creating categories
ms.assetid: 97c88693-05ff-499e-8c43-352ee073dcb7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 02ef202436e12ae075c41f507577bacaa968c60b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66341585"
---
# <a name="create-a-settings-category"></a>创建设置类别

在本演练中创建 Visual Studio 设置类别和使用它来保存到的值并设置文件中还原值。 设置类别是一组显示为"自定义设置点;"的相关属性也就是说，作为中的复选框**导入和导出设置**向导。 (您可以在找到它**工具**菜单。)设置进行保存或还原为类别，以及各项设置不会显示在该向导。 有关详细信息，请参阅[环境设置](../ide/environment-settings.md)。

通过从它派生来创建设置类别<xref:Microsoft.VisualStudio.Shell.DialogPage>类。

若要开始本演练，必须先完成第一部分[创建选项页](../extensibility/creating-an-options-page.md)。 生成的选项属性网格可以检查和更改类别中的属性。 在设置文件中保存的属性类别后，您将检查文件以查看如何存储属性值。

## <a name="prerequisites"></a>系统必备
 从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-settings-category"></a>创建设置类别
 在本部分中，使用自定义设置点来保存和还原设置类别的值。

### <a name="to-create-a-settings-category"></a>若要创建设置类别

1. 完成[创建选项页](../extensibility/creating-an-options-page.md)。

2. 打开*VSPackage.resx*文件，并添加以下三个字符串资源：

    |名称|值|
    |----------|-----------|
    |106|我的类别|
    |107|我的设置|
    |108|OptionInteger 和 OptionFloat|

     该名称的类别"My Category"、 对象"我的设置"，和类别说明"OptionInteger 和 OptionFloat"，这将创建资源。

    > [!NOTE]
    > 这三个字段，仅类别名称中没有**导入和导出设置**向导。

3. 在中*MyToolsOptionsPackage.cs*，添加`float`名为属性`OptionFloat`到`OptionPageGrid`类，如以下示例所示。

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
    > `OptionPageGrid`现在名为"My Category"类别包含两个属性，`OptionInteger`和`OptionFloat`。

4. 添加<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>到`MyToolsOptionsPackage`类并为其提供 CategoryName"My Category"，为其提供的对象名"我的设置"，并将 isToolsOptionPage 设置为 true。 设置 categoryResourceID、 objectNameResourceID 和 DescriptionResourceID 为 Id 前面创建的相应字符串资源。

    ```csharp
    [ProvideProfileAttribute(typeof(OptionPageGrid),
        "My Category", "My Settings", 106, 107, isToolsOptionPage:true, DescriptionResourceID = 108)]
    ```

5. 生成项目并启动调试。 在实验实例中应看到**我的网格页**现在具有整数和浮点值。

## <a name="examine-the-settings-file"></a>检查设置文件
 在本部分中，您将属性类别值导出到设置文件。 检查文件，然后返回到的属性类别导入值。

1. 在调试模式下启动项目，通过按**F5**。 这将启动实验实例。

2. 打开**工具** > **选项**对话框。

3. 在树视图中的左窗格中，展开**My Category** ，然后单击**我的网格页**。

4. 更改的值**OptionFloat**为 3.1416 和**OptionInteger**到 12。 单击 **“确定”** 。

5. 在“工具”  菜单上，单击“导入和导出设置”  。

     **导入和导出设置**向导显示。

6. 请确保**导出选定的环境设置**已选中，然后单击**下一步**。

     **选择要导出的设置**页将出现。

7. 单击**我的设置**。

     **描述**更改为**OptionInteger 和 OptionFloat**。

8. 请确保**我的设置**是唯一的类别，选择，然后单击**下一步**。

     **名称设置文件**页将出现。

9. 将新的设置文件命名*MySettings.vssettings*并将其保存在相应的目录中。 单击 **“完成”** 。

     **导出完成**页将报告已成功导出你的设置。

10. 上**文件**菜单，依次指向**打开**，然后单击**文件**。 找到*MySettings.vssettings*并将其打开。

     您可以找到导出的文件 （你 Guid 将不同） 的以下部分中的属性类别。

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

     请注意，通过添加类别名称的对象名称后跟一条下划线来形成完整类别名称。 OptionFloat 和 OptionInteger 显示在类别中，以及其导出的值。

11. 关闭而不更改其设置文件。

12. 上**工具**菜单上，单击**选项**，展开**My Category**，单击**我的网格页**然后更改的值**OptionFloat**为 1.0 并**OptionInteger**为 1。 单击 **“确定”** 。

13. 上**工具**菜单上，单击**导入和导出设置**，选择**导入选定的环境设置**，然后单击**下一步**。

     **保存当前设置**页将出现。

14. 选择**否，仅导入新设置**，然后单击**下一步**。

     **选择要导入的设置集合**页将出现。

15. 选择*MySettings.vssettings*中的文件**我的设置**节点的树视图。 如果文件未出现在树视图中，单击**浏览**并找到它。 单击 **“下一步”** 。

     **选择要导入的设置**对话框随即出现。

16. 请确保**我的设置**已选中，然后单击**完成**。 当**导入完整**页面出现后，单击**关闭**。

17. 上**工具**菜单上，单击**选项**，展开**My Category**，单击**我的网格页**并验证是否具有的属性类别值已还原。