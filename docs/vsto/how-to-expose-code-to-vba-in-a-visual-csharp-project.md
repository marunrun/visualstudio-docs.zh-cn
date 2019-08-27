---
title: 如何：在中向 VBA 代码公开C#项目
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual C# [Office development in Visual Studio], exposing code to VBA
- VBA [Office development in Visual Studio], exposing code in document-level customizations
- document-level customizations [Office development in Visual Studio], exposing code
- exposing code to VBA
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: ac41f4da29b95ba1fcd1601f98104956d584212a
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63419492"
---
# <a name="how-to-expose-code-to-vba-in-a-visual-c-project"></a>如何：向视觉对象中的 VBA 公开代码C#项目
  如果您希望两种类型的代码与彼此进行交互，您可以公开 Visual C# 项目中为 Visual Basic for Applications (VBA) 代码的代码。

 Visual C# 过程是不同于 Visual Basic 过程。 有关详细信息，请参阅[如何：向 VBA 公开代码在 Visual Basic 项目中的](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md)。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="expose-code-in-a-visual-c-project"></a>公开 Visual C# 项目中的代码
 若要使 VBA 代码能够调用 Visual C# 项目中的代码，修改代码，以便对于 COM 可见，并将**ReferenceAssemblyFromVbaProject**属性设置为**True**在设计器中。

 有关演练，演示如何在视觉对象中调用方法C#从 VBA 项目，请参阅[演练：从 Visual C 中的 VBA 调用代码&#35;项目](../vsto/walkthrough-calling-code-from-vba-in-a-visual-csharp-project.md)。

### <a name="to-expose-code-in-a-visual-c-project-to-vba"></a>若要公开到 VBA Visual C# 项目中的代码

1. 打开或创建基于 Word 文档、 Excel 工作簿或 Excel 模板支持的宏，并且已经包含 VBA 代码的文档级项目。

    有关支持的宏的文档文件格式的详细信息，请参阅[结合 VBA 和文档级自定义项](../vsto/combining-vba-and-document-level-customizations.md)。

   > [!NOTE]
   > 此功能无法在 Word 模板项目中使用。

2. 请确保允许文档中的 VBA 代码不提示用户启用宏的情况下运行。 通过在 Word 或 Excel 的“信任中心”设置中将 Office 项目的位置添加到受信任位置列表中，可以信任要运行的 VBA 代码。

3. 添加你想要向 VBA 公开到你的项目中的公共类的成员，并声明将新成员**公共**。

4. 将以下内容应用<xref:System.Runtime.InteropServices.ComVisibleAttribute>和<xref:System.Runtime.InteropServices.ClassInterfaceAttribute>属性到要向 VBA 公开的类。 这些特性使类对于 COM 可见，但不生成类接口。

   ```csharp
   [System.Runtime.InteropServices.ComVisible(true)]
   [System.Runtime.InteropServices.ClassInterface(
       System.Runtime.InteropServices.ClassInterfaceType.None)]
   ```

5. 重写**GetAutomationObject**以返回向 VBA 公开类的实例在项目中主机项类的方法：

   - 如果您正在公开到 VBA 是主机项类，重写**GetAutomationObject**属于此类，并返回类的当前实例的方法。

     ```csharp
     protected override object GetAutomationObject()
     {
         return this;
     }
     ```

   - 如果您正在公开不向 VBA 是主机项类，重写**GetAutomationObject**方法的任何主机项在项目中，并返回非主机项类的实例。 例如，以下代码假定你将公开一个名为类`DocumentUtilities`向 VBA。

     ```csharp
     protected override object GetAutomationObject()
     {
         return new DocumentUtilities();
     }
     ```

     有关主机项的详细信息，请参阅[主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)。

6. 从要向 VBA 公开的类中提取一个接口。 在中**提取接口**对话框框中，选择想要包括接口声明中的公共成员。 有关详细信息，请参阅[提取接口重构](../ide/reference/extract-interface.md)。

7. 添加**公共**到接口声明关键字。

8. 通过添加以下来使该接口对 COM 可见<xref:System.Runtime.InteropServices.ComVisibleAttribute>到接口属性。

   ```csharp
   [System.Runtime.InteropServices.ComVisible(true)]
   ```

9. 设计器中打开 （针对 Word) 的文档或工作表 （针对 Excel) [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

10. 在 **“属性”** 窗口中，选择 **“ReferenceAssemblyFromVbaProject”** 属性，并将值更改为 **“True”**。

    > [!NOTE]
    > 如果工作簿或文档尚未包含 VBA 代码，或如果文档中的 VBA 代码不受信任运行，在设置时，将收到一条错误消息**ReferenceAssemblyFromVbaProject**属性设置为**True**. 这是因为在这种情况下，Visual Studio 无法修改文档中的 VBA 项目。

11. 在显示的消息中单击 **“确定”** 。 此消息提醒你如果你添加 VBA 代码到工作簿或文档时运行中的项目[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]，下次生成项目时，将丢失的 VBA 代码。 这是因为中的文档中生成输出文件夹覆盖每次生成项目。

     此时，Visual Studio 将项目配置，以便为程序集可以调用 VBA 项目。 Visual Studio 还将添加一个名为方法`GetManagedClass`到 VBA 项目。 可以从任何位置调用此方法要访问向 VBA 公开的类的 VBA 项目中。

12. 生成项目。

## <a name="see-also"></a>请参阅
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
- [结合 VBA 和文档级自定义项](../vsto/combining-vba-and-document-level-customizations.md)
- [演练：从 Visual C 中的 VBA 调用代码&#35;项目](../vsto/walkthrough-calling-code-from-vba-in-a-visual-csharp-project.md)
- [如何：向 VBA 公开代码在 Visual Basic 项目中](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md)
