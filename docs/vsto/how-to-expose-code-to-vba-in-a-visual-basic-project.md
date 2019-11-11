---
title: 如何：在 Visual Basic 项目中向 VBA 公开代码
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
ms.openlocfilehash: e5a0f962d93713137b23e20e35dc75108925859d
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72985930"
---
# <a name="how-to-expose-code-to-vba-in-a-visual-basic-project"></a>如何：在 Visual Basic 项目中向 VBA 公开代码
  如果你希望两种类型的代码彼此交互，则可以将 [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] 项目中的代码公开到 Visual Basic for Applications （VBA）代码。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 Visual Basic 过程与视觉对象C#不同。 有关详细信息，请参阅[如何：在 Visual C&#35;项目中向 VBA 公开代码](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md)。

 对于主机项类中的代码，该进程与其他类中的代码的进程不同：

- [公开主机项类中的代码](#HostItemCode)

- [公开不在主机项类中的代码](#NonHostItem)

## <a name="HostItemCode"></a>公开主机项类中的代码
 若要使 VBA 代码能够调用主机项类中 Visual Basic 代码，请将主机项的**EnableVbaCallers**属性设置为**True**。

 有关演示如何公开主机项类的方法，然后从 VBA 中调用该方法的演练，请参阅[演练：在 Visual Basic 项目中调用 VBA 中的代码](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md)。 有关宿主项的详细信息，请参阅[主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)。

#### <a name="to-expose-code-in-a-host-item-to-vba"></a>向 VBA 公开主机项中的代码

1. 打开或创建一个文档级 [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] 项目，该项目基于支持宏的 Word 文档、Excel 工作簿或 Excel 模板，并且已经包含 VBA 代码。

     有关支持宏的文档文件格式的详细信息，请参阅[结合 VBA 和文档级自定义项](../vsto/combining-vba-and-document-level-customizations.md)。

    > [!NOTE]
    > 此功能无法在 Word 模板项目中使用。

2. 确保在不提示用户启用宏的情况下允许文档中的 VBA 代码运行。 通过在 Word 或 Excel 的“信任中心”设置中将 Office 项目的位置添加到受信任位置列表中，可以信任要运行的 VBA 代码。

3. 将你想要向 VBA 公开的属性、方法或事件添加到项目中的某个主机项类，然后将该新成员声明为**公共**成员。 类的名称取决于应用程序：

    - 在 Word 项目中，默认情况下，主机项类命名为 `ThisDocument`。

    - 在 Excel 项目中，默认情况下，主机项类命名为 `ThisWorkbook`、`Sheet1`、`Sheet2`和 `Sheet3`。

4. 将主机项的**EnableVbaCallers**属性设置为**True**。 当宿主项在设计器中处于打开状态时，此属性将出现在 "**属性**" 窗口中。

     设置此属性后，Visual Studio 会自动将**ReferenceAssemblyFromVbaProject**属性设置为**True**。

    > [!NOTE]
    > 如果工作簿或文档尚未包含 VBA 代码，或者文档中的 VBA 代码不受信任，无法运行，则将**EnableVbaCallers**属性设置为**True**时，你将收到一条错误消息。 这是因为在这种情况下，Visual Studio 无法修改文档中的 VBA 项目。

5. 在显示的消息中单击 **“确定”** 。 此消息提醒你，如果在从 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中运行项目时将 VBA 代码添加到工作簿或文档中，则在下次生成项目时，VBA 代码将丢失。 这是因为每次生成项目时，都会覆盖生成输出文件夹中的文档。

     此时，Visual Studio 会将项目配置为使 VBA 项目可以调入程序集。 Visual Studio 还会将一个名为 `CallVSTOAssembly` 的属性添加到 VBA 项目中的 `ThisDocument`、`ThisWorkbook`、`Sheet1`、`Sheet2`或 `Sheet3` 模块中。 您可以使用此属性来访问向 VBA 公开的类的公共成员。

6. 生成项目。

## <a name="NonHostItem"></a>公开不在主机项类中的代码
 若要使 VBA 代码能够调用不在宿主项类中 Visual Basic 代码，请修改代码，使其对 VBA 可见。

### <a name="to-expose-code-that-is-not-in-a-host-item-class-to-vba"></a>向 VBA 公开不在主机项类中的代码

1. 打开或创建一个文档级 [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] 项目，该项目基于支持宏的 Word 文档、Excel 工作簿或 Excel 模板，并且已经包含 VBA 代码。

     有关支持宏的文档文件格式的详细信息，请参阅[结合 VBA 和文档级自定义项](../vsto/combining-vba-and-document-level-customizations.md)。

    > [!NOTE]
    > 此功能无法在 Word 模板项目中使用。

2. 确保在不提示用户启用宏的情况下允许文档中的 VBA 代码运行。 通过在 Word 或 Excel 的“信任中心”设置中将 Office 项目的位置添加到受信任位置列表中，可以信任要运行的 VBA 代码。

3. 将要向 VBA 公开的成员添加到项目中的公共类，并将新成员声明为**公共**成员。

4. 将以下 <xref:System.Runtime.InteropServices.ComVisibleAttribute> 和 <xref:Microsoft.VisualBasic.ComClassAttribute> 属性应用于要向其公开的类。 这些属性使类对 VBA 可见。

    ```vb
    <Microsoft.VisualBasic.ComClass()> _
    <System.Runtime.InteropServices.ComVisibleAttribute(True)> _
    ```

5. 替代项目中主机项类的 **GetAutomationObject** 方法，以返回要向 VBA 公开的类的实例。 下面的代码示例假定你向 VBA 公开名为 `DocumentUtilities` 的类。

    ```vb
    Protected Overrides Function GetAutomationObject() As Object
        Return New DocumentUtilities()
    End Function
    ```

6. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中打开文档（对于 Word）或工作表（对于 Excel）设计器。

7. 在 **“属性”** 窗口中，选择 **“ReferenceAssemblyFromVbaProject”** 属性，并将值更改为 **“True”** 。

    > [!NOTE]
    > 如果工作簿或文档尚未包含 VBA 代码，或者文档中的 VBA 代码不受信任，无法运行，则将**ReferenceAssemblyFromVbaProject**属性设置为**True**时，你将收到一条错误消息。 这是因为在这种情况下，Visual Studio 无法修改文档中的 VBA 项目。

8. 在显示的消息中单击 **“确定”** 。 此消息提醒你，如果在从 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中运行项目时将 VBA 代码添加到工作簿或文档中，则在下次生成项目时，VBA 代码将丢失。 这是因为每次生成项目时，都会覆盖生成输出文件夹中的文档。

     此时，Visual Studio 会将项目配置为使 VBA 项目可以调入程序集。 Visual Studio 还会将一个名为 `GetManagedClass` 的方法添加到 VBA 项目。 可以从 VBA 项目中的任何位置调用此方法，以访问向 VBA 公开的类。

9. 生成项目。

## <a name="see-also"></a>请参阅
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
- [合并 VBA 和文档级自定义项](../vsto/combining-vba-and-document-level-customizations.md)
- [演练：在 Visual Basic 项目中调用 VBA 中的代码](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md)
- [如何：在 Visual C&#35;项目中向 VBA 公开代码](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md)
