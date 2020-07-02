---
title: '如何：在 c # 项目中向 VBA 公开代码'
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: 21d7672d3c08012e75d73ee8bf4d9816b850eb2c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544828"
---
# <a name="how-to-expose-code-to-vba-in-a-visual-c-project"></a>如何：在 Visual c # 项目中向 VBA 公开代码
  如果希望两种类型的代码彼此交互，可以在 Visual c # 项目中公开代码，以便 Visual Basic for Applications （VBA）代码。

 Visual c # 进程不同于 Visual Basic 进程。 有关详细信息，请参阅[如何：在 Visual Basic 项目中向 VBA 公开代码](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md)。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="expose-code-in-a-visual-c-project"></a>在 Visual c # 项目中公开代码
 若要使 VBA 代码能够调用 Visual c # 项目中的代码，请修改代码，使其对 COM 可见，然后在设计器中将**ReferenceAssemblyFromVbaProject**属性设置为**True** 。

 有关演示如何从 VBA 调用 Visual c # 项目中的方法的演练，请参阅[演练：在 Visual c&#35; 项目中调用 VBA 中的代码](../vsto/walkthrough-calling-code-from-vba-in-a-visual-csharp-project.md)。

### <a name="to-expose-code-in-a-visual-c-project-to-vba"></a>在 Visual c # 项目中向 VBA 公开代码

1. 打开或创建一个文档级项目，该项目基于支持宏的 Word 文档、Excel 工作簿或 Excel 模板，并且已经包含 VBA 代码。

    有关支持宏的文档文件格式的详细信息，请参阅[结合 VBA 和文档级自定义项](../vsto/combining-vba-and-document-level-customizations.md)。

   > [!NOTE]
   > 此功能无法在 Word 模板项目中使用。

2. 确保在不提示用户启用宏的情况下允许文档中的 VBA 代码运行。 通过在 Word 或 Excel 的“信任中心”设置中将 Office 项目的位置添加到受信任位置列表中，可以信任要运行的 VBA 代码。

3. 将要向 VBA 公开的成员添加到项目中的公共类，并将新成员声明为**公共**成员。

4. 将以下和属性应用于要 <xref:System.Runtime.InteropServices.ComVisibleAttribute> <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> 向 VBA 公开的类。 这些特性使类对于 COM 可见，但不生成类接口。

   ```csharp
   [System.Runtime.InteropServices.ComVisible(true)]
   [System.Runtime.InteropServices.ClassInterface(
       System.Runtime.InteropServices.ClassInterfaceType.None)]
   ```

5. 重写项目中主机项类的**GetAutomationObject**方法，以返回要向 VBA 公开的类的实例：

   - 如果要向 VBA 公开主机项类，请重写属于此类的**GetAutomationObject**方法，并返回类的当前实例。

     ```csharp
     protected override object GetAutomationObject()
     {
         return this;
     }
     ```

   - 如果要向 VBA 公开不是主机项的类，请重写项目中任何主机项的**GetAutomationObject**方法，并返回非宿主项类的实例。 例如，下面的代码假设你要公开一个名 `DocumentUtilities` 为 VBA 的类。

     ```csharp
     protected override object GetAutomationObject()
     {
         return new DocumentUtilities();
     }
     ```

     有关宿主项的详细信息，请参阅[主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)。

6. 从要向 VBA 公开的类中提取接口。 在 "**提取接口**" 对话框中，选择要包括在接口声明中的公共成员。 有关详细信息，请参阅[提取接口重构](../ide/reference/extract-interface.md)。

7. 将**public**关键字添加到接口声明。

8. 通过向接口添加以下特性，使接口对 COM 可见 <xref:System.Runtime.InteropServices.ComVisibleAttribute> 。

   ```csharp
   [System.Runtime.InteropServices.ComVisible(true)]
   ```

9. 在的设计器中打开文档（对于 Word）或工作表（对于 Excel） [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

10. 在 **“属性”** 窗口中，选择 **“ReferenceAssemblyFromVbaProject”** 属性，并将值更改为 **“True”**。

    > [!NOTE]
    > 如果工作簿或文档尚未包含 VBA 代码，或者文档中的 VBA 代码不受信任，无法运行，则在您将**ReferenceAssemblyFromVbaProject**属性设置为**True**时，您将收到一条错误消息。 这是因为在这种情况下，Visual Studio 无法修改文档中的 VBA 项目。

11. 在显示的消息中单击 **“确定”** 。 此消息提醒你，如果在运行项目时将 VBA 代码添加到工作簿或文档，则在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 下次生成项目时，vba 代码将丢失。 这是因为每次生成项目时，都会覆盖生成输出文件夹中的文档。

     此时，Visual Studio 会将项目配置为使 VBA 项目可以调入程序集。 Visual Studio 还会将一个名为的方法添加 `GetManagedClass` 到 VBA 项目。 可以从 VBA 项目中的任何位置调用此方法，以访问向 VBA 公开的类。

12. 生成项目。

## <a name="see-also"></a>请参阅
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
- [合并 VBA 和文档级自定义项](../vsto/combining-vba-and-document-level-customizations.md)
- [演练：在 Visual C&#35; 项目中调用 VBA 中的代码](../vsto/walkthrough-calling-code-from-vba-in-a-visual-csharp-project.md)
- [如何：在 Visual Basic 项目中向 VBA 公开代码](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md)
