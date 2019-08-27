---
title: 如何：向 VBA 公开代码在 Visual Basic 项目中
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- VBA [Office development in Visual Studio], exposing code in document-level customizations
- document-level customizations [Office development in Visual Studio], exposing code
- Visual Basic [Office development in Visual Studio], exposing code to VBA
- exposing code to VBA
- host items [Office development in Visual Studio], exposing code to VBA
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0213df05e12ae69b4e24841971a518acc008599f
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63419417"
---
# <a name="how-to-expose-code-to-vba-in-a-visual-basic-project"></a>如何：向 VBA 公开代码在 Visual Basic 项目中
  您可以公开中的代码[!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)]项目到 Visual Basic for Applications (VBA) 代码，如果您希望两种类型的代码与彼此进行交互。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 Visual Basic 过程是不同于 Visual C# 过程。 有关详细信息，请参阅[如何：在 Visual C 中向 VBA 代码公开&#35;项目](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md)。

 该过程与不同主机项类中的代码比其他类中的代码：

- [公开主机项类中的代码](#HostItemCode)

- [公开不是主机项类中的代码](#NonHostItem)

  ![视频链接](../vsto/media/playvideo.gif "链接至视频")相关的视频演示，请参阅[如何实现：从 VBA 调用 VSTO 代码？](http://go.microsoft.com/fwlink/?LinkId=136757).

## <a name="HostItemCode"></a> 公开主机项类中的代码
 若要使 VBA 代码能够调用主机项类中的 Visual Basic 代码，设置**EnableVbaCallers**主机项的属性**True**。

 有关演示如何公开主机项类的方法，然后从 VBA 调用它的演练，请参阅[演练：在 Visual Basic 项目中从 VBA 调用代码](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md)。 有关主机项的详细信息，请参阅[主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)。

#### <a name="to-expose-code-in-a-host-item-to-vba"></a>若要公开主机项向 VBA 中的代码

1. 打开或创建文档级[!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)]基于 Word 文档、 Excel 工作簿或 Excel 模板支持的宏，并且已经包含 VBA 代码的项目。

     有关支持的宏的文档文件格式的详细信息，请参阅[结合 VBA 和文档级自定义项](../vsto/combining-vba-and-document-level-customizations.md)。

    > [!NOTE]
    > 此功能无法在 Word 模板项目中使用。

2. 请确保允许文档中的 VBA 代码不提示用户启用宏的情况下运行。 通过在 Word 或 Excel 的“信任中心”设置中将 Office 项目的位置添加到受信任位置列表中，可以信任要运行的 VBA 代码。

3. 添加属性、 方法或你想要向 VBA 到一个在项目中，主机项类公开的事件并将声明将新成员**公共**。 类的名称取决于应用程序：

    - 在 Word 项目中，主机项类名为`ThisDocument`默认情况下。

    - 在 Excel 项目中，主机项类名为`ThisWorkbook`， `Sheet1`， `Sheet2`，和`Sheet3`默认情况下。

4. 设置**EnableVbaCallers**主机项的属性**True**。 此属性现已推出**属性**时的宿主项是在设计器中打开的窗口。

     设置此属性后，Visual Studio 将自动设置**ReferenceAssemblyFromVbaProject**属性设置为**True**。

    > [!NOTE]
    > 如果工作簿或文档尚未包含 VBA 代码，或如果文档中的 VBA 代码不受信任运行，在设置时，将收到一条错误消息**EnableVbaCallers**属性设置为**True**。 这是因为在这种情况下，Visual Studio 无法修改文档中的 VBA 项目。

5. 在显示的消息中单击 **“确定”** 。 此消息提醒您将 VBA 代码添加到工作簿或文档，而如果您正在运行中的项目[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]下, 一次生成项目时，将丢失的 VBA 代码。 这是因为每次生成项目时，覆盖生成输出文件夹中的文档。

     此时，Visual Studio 将项目配置，以便为程序集可以调用 VBA 项目。 Visual Studio 还将添加名为的属性`CallVSTOAssembly`到`ThisDocument`， `ThisWorkbook`， `Sheet1`， `Sheet2`，或`Sheet3`VBA 项目中的模块。 此属性可用于访问向 VBA 公开的类的公共成员。

6. 生成项目。

## <a name="NonHostItem"></a> 公开不是主机项类中的代码
 若要使 VBA 代码能够调用不是主机项类中的 Visual Basic 代码，修改代码，因此它是对 VBA 可见。

### <a name="to-expose-code-that-is-not-in-a-host-item-class-to-vba"></a>将不在主机项类向 VBA 代码

1. 打开或创建文档级[!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)]基于 Word 文档、 Excel 工作簿或 Excel 模板支持的宏，并且已经包含 VBA 代码的项目。

     有关支持的宏的文档文件格式的详细信息，请参阅[结合 VBA 和文档级自定义项](../vsto/combining-vba-and-document-level-customizations.md)。

    > [!NOTE]
    > 此功能无法在 Word 模板项目中使用。

2. 请确保允许文档中的 VBA 代码不提示用户启用宏的情况下运行。 通过在 Word 或 Excel 的“信任中心”设置中将 Office 项目的位置添加到受信任位置列表中，可以信任要运行的 VBA 代码。

3. 添加你想要向 VBA 公开到你的项目中的公共类的成员，并声明将新成员**公共**。

4. 将以下内容应用<xref:System.Runtime.InteropServices.ComVisibleAttribute>和<xref:Microsoft.VisualBasic.ComClassAttribute>属性到要向 VBA 公开的类。 这些特性使类对于 VBA 可见。

    ```vb
    <Microsoft.VisualBasic.ComClass()> _
    <System.Runtime.InteropServices.ComVisibleAttribute(True)> _
    ```

5. 替代项目中主机项类的 **GetAutomationObject** 方法，以返回要向 VBA 公开的类的实例。 下面的代码示例假定你将公开一个名为类`DocumentUtilities`向 VBA。

    ```vb
    Protected Overrides Function GetAutomationObject() As Object
        Return New DocumentUtilities()
    End Function
    ```

6. 打开的文档 （对于 Word) 或 （针对 Excel) 的工作表设计器中[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

7. 在 **“属性”** 窗口中，选择 **“ReferenceAssemblyFromVbaProject”** 属性，并将值更改为 **“True”**。

    > [!NOTE]
    > 如果工作簿或文档尚未包含 VBA 代码，或如果文档中的 VBA 代码不受信任运行，在设置时，将收到一条错误消息**ReferenceAssemblyFromVbaProject**属性设置为 **，则返回 True**. 这是因为在这种情况下，Visual Studio 无法修改文档中的 VBA 项目。

8. 在显示的消息中单击 **“确定”** 。 此消息提醒您将 VBA 代码添加到工作簿或文档，而如果您正在运行中的项目[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]下, 一次生成项目时，将丢失的 VBA 代码。 这是因为每次生成项目时，覆盖生成输出文件夹中的文档。

     此时，Visual Studio 将项目配置，以便为程序集可以调用 VBA 项目。 Visual Studio 还将添加一个名为方法`GetManagedClass`到 VBA 项目。 可以从任何位置调用此方法要访问向 VBA 公开的类的 VBA 项目中。

9. 生成项目。

## <a name="see-also"></a>请参阅
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
- [结合 VBA 和文档级自定义项](../vsto/combining-vba-and-document-level-customizations.md)
- [演练：在 Visual Basic 项目中从 VBA 调用代码](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md)
- [如何：在 Visual C 中向 VBA 代码公开&#35;项目](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md)
