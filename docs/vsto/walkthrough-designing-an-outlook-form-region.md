---
title: 演练：设计 Outlook 窗体区域
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4a346686ee89862abef046c066614eddce1cf3a3
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71255762"
---
# <a name="walkthrough-design-an-outlook-form-region"></a>演练：设计 Outlook 窗体区域
  自定义窗体区域扩展标准或自定义 Microsoft Office Outlook 窗体。 在本演练中，你将设计作为新页出现在联系人项目的检查器窗口中的自定义窗体区域。 通过将地址信息发送到 Windows Live 本地搜索网站，此窗体区域将显示为联系人列出的每个地址的映射。 有关窗体区域的信息，请参阅[创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

 本演练阐释了以下任务：

- 创建新的 Outlook VSTO 外接程序项目。

- 将窗体区域添加到 VSTO 外接程序项目。

- 设计窗体区域的布局。

- 自定义窗体区域的行为。

- 测试 Outlook 窗体区域。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Outlook_14_short](../vsto/includes/outlook-14-short-md.md)]或更高版本。

  ![视频链接](../vsto/media/playvideo.gif "视频链接")有关本主题的视频版本，请参阅[视频如何：设计 Outlook 窗体区域](http://go.microsoft.com/fwlink/?LinkID=140824)。

## <a name="create-a-new-outlook-vsto-add-in-project"></a>创建新的 Outlook VSTO 外接程序项目
 首先创建基本的 VSTO 外接程序项目。

### <a name="to-create-a-new-outlook-vsto-add-in-project"></a>创建新的 Outlook VSTO 外接程序项目

1. 在[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中，创建名为**MapItAddIn**的 Outlook VSTO 外接程序项目。

2. 在 **“新建项目”** 对话框中，选择 **“创建解决方案的目录”** 。

3. 将项目保存到任一目录。

     有关详细信息，请参阅[如何：在 Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)中创建 Office 项目。

## <a name="add-a-form-region-to-the-outlook-vsto-add-in-project"></a>向 Outlook VSTO 外接程序项目添加窗体区域
 Outlook VSTO 外接程序解决方案可包含一个或多个 Outlook 窗体区域项。 使用 "**新建 Outlook 窗体区域**" 向导将窗体区域项添加到项目。

### <a name="to-add-a-form-region-to-the-outlook-vsto-add-in-project"></a>向 Outlook VSTO 外接程序项目添加窗体区域

1. 在**解决方案资源管理器**中，选择**MapItAddIn**项目。

2. 在 **“项目”** 菜单上，单击 **“添加新项”** 。

3. 在 "**添加新项**" 对话框中，选择 " **Outlook 窗体区域**"，将文件命名为**Mapit.vb**，然后单击 "**添加**"。

     " **NewOutlook 窗体区域**" 向导将启动。

4. 在 "**选择窗体区域的创建方式**" 页上，单击 "**设计新的窗体区域**"，然后单击 "**下一步**"。

5. 在 "**选择要创建的窗体区域的类型**" 页上，单击 "**独立**"，然后单击 "**下一步**"。

     *单独*的窗体区域向 Outlook 窗体添加新页。 有关窗体区域类型的详细信息，请参阅[创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)。

6. 在 "**提供说明性文本并选择显示首选项**" 页上，在 "**名称**" 框中键入 " **Map** "。

     打开联系人项目时，此名称将显示在检查器窗口的功能区中。

7. 选择处于**撰写模式下的检查**器和处于**读取模式的检查**器，然后单击 "**下一步**"。

8. 在 "**标识将显示此窗体区域的邮件类**" 页上，清除 "**邮件**"，选择 "**联系人**"，然后单击 "**完成**"。

     *MapIt.cs*或*mapit.vb*文件将添加到你的项目中。

## <a name="design-the-layout-of-the-form-region"></a>设计窗体区域的布局
 使用*窗体区域设计器*直观地开发窗体区域。 可将托管的控件拖到窗体区域设计器图面。 使用设计器和 "**属性**" 窗口来调整控件的布局和外观。

### <a name="to-design-the-layout-of-the-form-region"></a>设计窗体区域的布局

1. 在**解决方案资源管理器**中，展开 " **MapItAddIn** " 项目，然后双击 " *MapIt.cs* " 或 " *Mapit.vb* " 以打开窗体区域设计器。

2. 右键单击设计器，然后单击 "**属性**"。

3. 在 "**属性**" 窗口中，将 " **Size** " 设置为 **"664，469"** 。

     这可确保窗体区域的大小足以显示映射。

4. 在 **“视图”** 菜单上单击 **“工具箱”** 。

5. 从 "**工具箱**" 的 "**公共控件**" 选项卡中，将**WebBrowser**添加到窗体区域。

     **WebBrowser**将显示为联系人列出的每个地址的地图。

## <a name="customize-the-behavior-of-the-form-region"></a>自定义窗体区域的行为
 将代码添加到窗体区域事件处理程序，从而自定义窗体区域在运行时的行为方式。 对于此窗体区域而言，代码将检查 Outlook 项的属性，并确定是否显示 Map It 窗体区域。 如果它显示该窗体区域，代码将导航到 Windows Live 本地搜索并加载 Outlook 联系人项目中列出的每个地址的映射。

### <a name="to-customize-the-behavior-of-the-form-region"></a>自定义窗体区域的行为

1. 在**解决方案资源管理器**中，右键单击 " *MapIt.cs* " 或 " *mapit.vb*"，然后单击 "**查看代码**"。

    在代码编辑器中打开*MapIt.cs*或*mapit.vb* 。

2. 展开**窗体区域工厂**代码区域。

    将公开名为 `MapItFactory` 的窗体区域工厂类。

3. 将以下代码添加到 `MapItFactory_FormRegionInitializing` 事件处理程序中。 将在用户打开联系人项目时调用此事件处理程序。 下面的代码确定联系人项目是否包含地址。 如果联系人项不包含地址，则此代码会将<xref:System.ComponentModel.CancelEventArgs.Cancel%2A> <xref:Microsoft.Office.Tools.Outlook.FormRegionInitializingEventArgs>类的属性设置为**true** ，并且不显示窗体区域。 否则，VSTO 外接程序将引发 <xref:Microsoft.Office.Tools.Outlook.FormRegionControl.FormRegionShowing> 事件，并显示窗体区域。

    [!code-csharp[Trin_Outlook_FR_Separate#1](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Separate_O12/MapIt.cs#1)]
    [!code-vb[Trin_Outlook_FR_Separate#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Separate_O12/MapIt.vb#1)]

4. 将以下代码添加到 <xref:Microsoft.Office.Tools.Outlook.FormRegionControl.FormRegionShowing> 事件处理程序中。 这段代码执行下列任务：

   - 将联系人项目中的每个地址连接起来，并创建一个 URL 字符串。

   - 调用 <xref:System.Windows.Forms.WebBrowser> 对象的 <xref:System.Windows.Forms.WebBrowser.Navigate%2A> 方法，并将 URL 字符串作为参数传递。

     本地搜索网站将在 Map It 窗体区域中出现，并在便笺本中显示每个地址。

     [!code-csharp[Trin_Outlook_FR_Separate#2](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Separate_O12/MapIt.cs#2)]
     [!code-vb[Trin_Outlook_FR_Separate#2](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Separate_O12/MapIt.vb#2)]

## <a name="test-the-outlook-form-region"></a>测试 Outlook 窗体区域
 运行项目时，Visual Studio 将打开 Outlook。 打开联系人项目以查看 Map It 窗体区域。 Map It 窗体区域显示为包含地址的任何联系人项目的窗体中的页面。

### <a name="to-test-the-map-it-form-region"></a>测试 Map It 窗体区域

1. 按 F5 运行项目。

     Outlook 将打开。

2. 在 Outlook 的 "**主页**" 选项卡上，单击 "**新建项目**"，然后单击 "**联系人**"。

3. 在 contact 窗体中，键入**王 Beebe**作为联系人姓名，然后指定以下三个地址。

    |地址类型|Address|
    |------------------|-------------|
    |**节假日**|**4567 Main St 号，NY**|
    |**Home**|**1234北部圣彼得堡，纽约州**|
    |**其他**|**3456主要圣北京，华盛顿州**|

4. 保存并关闭联系人项目。

5. 重新打开**王 Beebe** contact 项。

    在 Outlook 中，可以通过打开联系人的通讯簿或者在**搜索人员**中键入王 Beebe，在 "**查找**" 组中完成此操作。

6. 在项的功能区的 "**显示**" 组中，单击 "**映射**"，以打开映射 it 窗体区域。

     Map It 窗体区域出现，并显示本地搜索网站。 "**业务**"、"**家庭**" 和**其他**地址将显示在 "暂存" 面板中。 在便笺本中，选择需映射的地址。

## <a name="next-steps"></a>后续步骤
 可从以下主题了解有关如何自定义 Outlook 应用程序 UI 的详细信息：

- 若要了解如何自定义 Outlook 项的功能区，请参阅[自定义 outlook 功能区](../vsto/customizing-a-ribbon-for-outlook.md)。

## <a name="see-also"></a>请参阅
- [在运行时访问窗体区域](../vsto/accessing-a-form-region-at-run-time.md)
- [创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)
- [创建 Outlook 窗体区域的准则](../vsto/guidelines-for-creating-outlook-form-regions.md)
- [演练：导入在 Outlook 中设计的窗体区域](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)
- [如何：向 Outlook 外接程序项目添加窗体区域](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)
- [将窗体区域与 Outlook 邮件类关联](../vsto/associating-a-form-region-with-an-outlook-message-class.md)
- [Outlook 窗体区域中的自定义操作](../vsto/custom-actions-in-outlook-form-regions.md)
- [如何：阻止 Outlook 显示窗体区域](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md)
