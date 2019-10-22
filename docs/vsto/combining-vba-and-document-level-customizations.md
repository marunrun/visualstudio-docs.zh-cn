---
title: 合并 VBA 和文档级自定义项
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.VBAInterop.InvalidAssemblyVersion
- VST.VBAInterop.ProjectLoadFailure
- VST.VBAInterop.MissingGUID
- VST.VBAInterop.EnableComCallers
- VST.VBAInterop.PersistVBACode
- VST.VBAInterop.ReferenceAssemblyFromVBA
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], Visual Basic for Applications and
- VBA [Office development in Visual Studio]
- Office documents [Office development in Visual Studio], Visual Basic for Applications and
- VBA [Office development in Visual Studio], about VBA and document-level customizations
- managed code [Office development in Visual Studio], Visual Basic for Applications and
- document-level customizations [Office development in Visual Studio], Visual Basic for Applications and
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b3bab9c132439c6efa53842f1e13c6c5be31db00
ms.sourcegitcommit: 6c55c40da74ed8969dcba56acbd30458fdb69c5a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2019
ms.locfileid: "70977605"
---
# <a name="combine-vba-and-document-level-customizations"></a>合并 VBA 和文档级自定义项
  在属于 Microsoft Office Word 或 Microsoft Office Excel 的文档级自定义项的文档中，可以使用 Visual Basic for Applications (VBA) 代码。 可以从自定义程序集调用文档中的 VBA 代码，也可以将项目配置为使文档中的 VBA 代码能够调用自定义程序集中的代码。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="behavior-of-vba-code-in-a-document-level-customization"></a>文档级自定义项中 VBA 代码的行为
 在 Visual Studio 中打开项目时，文档将以设计模式打开。 当文档处于设计模式时，VBA 代码不运行，因此你可以在不运行 VBA 代码的情况下处理文档和代码。

 运行解决方案时，VBA 和自定义程序集中的事件处理程序选取文档中引发的事件，并且两组代码都会运行。 无法预先确定哪组代码将在另一组代码之前运行；必须在每个单独的情况下通过测试来确定这一点。 如果没有仔细调整和测试这两组代码，可能会得到意外的结果。

## <a name="call-vba-code-from-the-customization-assembly"></a>从自定义程序集调用 VBA 代码
 可以在 Word 文档中调用宏，也可以在 Excel 工作簿中调用宏和函数。 若要执行此操作，请使用以下方法之一：

- 对于 Word，调用 <xref:Microsoft.Office.Interop.Word.Application> 类的 <xref:Microsoft.Office.Interop.Word._Application.Run%2A> 方法。

- 对于 Excel，调用 <xref:Microsoft.Office.Interop.Excel._Application.Run%2A> 类的 <xref:Microsoft.Office.Interop.Excel.Application> 方法。

  对于每个方法，第一个参数标识要调用的宏或函数的名称，其余的可选参数指定要传递到宏或函数的参数。 对于 Word 和 Excel，第一个参数的格式可能不同：

- 对于 Word，第一个参数是一个字符串，该字符串可以是模板、模块和宏名称的任意组合。 如果指定文档名称，则你的代码只能运行与当前上下文相关的文档中的宏，而不是任何文档中的任何宏。

- 对于 Excel，第一个参数可以是指定宏名称的字符串、指示函数位置的 <xref:Microsoft.Office.Interop.Excel.Range> 或已注册 DLL (XLL) 函数的注册 ID。 如果传递字符串，则将在活动工作表的上下文中计算该字符串。

  下面的代码示例演示如何从 Excel 文档级项目调用名为 `MyMacro` 的宏。 此示例假定 `MyMacro` 是在 `Sheet1`中定义的 。

```vb
Globals.Sheet1.Application.Run("MyMacro")
```

```csharp
Globals.Sheet1.Application.Run("MyMacro", missing, missing, missing,
    missing, missing, missing, missing, missing, missing, missing,
    missing, missing, missing, missing, missing, missing, missing,
    missing, missing, missing, missing, missing, missing, missing,
    missing, missing, missing, missing, missing, missing);
```

> [!NOTE]
> 有关使用全局`missing`变量代替 Visual C#中的可选参数的信息，请参阅在[Office 解决方案中编写代码](../vsto/writing-code-in-office-solutions.md)。

## <a name="call-code-in-document-level-customizations-from-vba"></a>从 VBA 调用文档级自定义项中的代码
 可以配置 Word 或 Excel 的文档级项目，以便文档中的 Visual Basic for Applications (VBA) 代码能够调用自定义程序集中的代码。 这在以下应用场景中很有用：

- 你希望使用与某个文档相关联的文档级自定义项中的功能扩展同一文档中的现有 VBA 代码。

- 你希望将你使用文档级自定义项开发的服务提供给能够通过在文档中编写 VBA 代码来访问服务的最终用户。

  Visual Studio 中的 Office 开发工具可为 VSTO 外接程序提供相似的功能。如果你正在开发 VSTO 外接程序，可以从其他 Microsoft Office 解决方案调用 VSTO 外接程序中的代码。 有关详细信息，请参阅[从其他 Office 解决方案调用 VSTO 外接程序中的代码](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md)。

> [!NOTE]
> 此功能无法在 Word 模板项目中使用。 它只能在 Word 文档、Excel 工作簿或 Excel 模板项目中使用。

## <a name="requirements"></a>要求
 你的项目必须满足以下要求，然后才能使 VBA 代码调入自定义项程序集：

- 文档必须具有以下文件扩展名之一：

  - 对于 Word： *. docm*或 *.doc*

  - 对于 Excel： *. xlsm*、 *. xltm*、 *.xls*或 *.xlt*

- 文档必须已经包含其中有 VBA 代码的 VBA 项目。

- 必须在不提示用户启用宏的情况下允许文档中的 VBA 代码运行。 通过在 Word 或 Excel 的“信任中心”设置中将 Office 项目的位置添加到受信任位置列表中，可以信任要运行的 VBA 代码。

- Office 项目必须至少包含一个公共类，该类包含一个或多个要向 VBA 公开的公共成员。

     可以向 VBA 公开方法、属性和事件。 公开的类可以是主机项类（如 Word 的 `ThisDocument` 或 Excel 的 `ThisWorkbook` 和 `Sheet1` ）或你在项目中定义的其他类。 有关宿主项的详细信息，请参阅[主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)。

## <a name="enable-vba-code-to-call-into-the-customization-assembly"></a>使 VBA 代码能够调入自定义程序集
 可通过两种不同方式向文档中的 VBA 代码公开自定义项程序集中的成员：

- 可以向 VBA 公开 [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] 项目中某个主机项类的成员。 若要这样做，请在设计器中打开主机项（即文档、工作表或工作簿），并在 **“属性”** 窗口中将主机项的 **EnableVbaCallers** 属性设置为 **True** 。 Visual Studio 会自动执行使 VBA 代码能够调用类成员所需的所有工作。

- 可以向 VBA公开 Visual C# 项目中任何公共类的成员或 [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] 项目中非主机项类的成员。 通过此选项，你可以更自由地选择要向 VBA 公开的类，但它也需要更多的手动步骤。

   为此，必须执行下列主要步骤：

  1. 向 COM 公开该类。

  2. 替代项目中主机项类的 **GetAutomationObject** 方法，以返回要向 VBA 公开的类的实例。

  3. 将项目中任何主机项类的 **ReferenceAssemblyFromVbaProject** 属性设置为 **True**。 这会将自定义项程序集的类型库嵌入程序集，并将对该类型库的引用添加到文档中的 VBA 项目。

  有关详细说明，请[参阅如何：在 Visual Basic 项目](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md)中向 VBA 公开代码， [以及如何：在 Visual C&#35;项目](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md)中向 VBA 公开代码。

  **EnableVbaCallers** 和 **ReferenceAssemblyFromVbaProject** 属性仅在设计时在 **“属性”** 窗口中可用，无法在运行时使用。 若要查看这些属性，请在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中打开主机项的设计器。 有关设置这些属性时 Visual Studio 执行的特定任务的详细信息，请参阅[由主机项属性执行的任务](#PropertyTasks)。

> [!NOTE]
> 如果工作簿或文档尚未包含 VBA 代码，或者如果运行文档中的 VBA 代码时不信任该代码，则在将 **“EnableVbaCallers”** 或 **“ReferenceAssemblyFromVbaProject”** 属性设置为 **“True”** 时，你将收到一条错误消息。 这是因为在这种情况下，Visual Studio 无法修改文档中的 VBA 项目。

## <a name="use-members-in-vba-code-to-call-into-the-customization-assembly"></a>使用 VBA 代码中的成员调入自定义项程序集
 在将项目配置为使 VBA 代码能够调入自定义项程序集后，Visual Studio 会将以下成员添加到文档中的 VBA 项目：

- 对于所有项目，Visual Studio 都会添加一个名为 `GetManagedClass`的全局方法。

- 对于在其中使用 [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] 属性公开主机项类成员的 **“属性”** 项目，Visual Studio 还会将一个名为 `CallVSTOAssembly` 的属性添加到 VBA 项目中的 `ThisDocument`、 `ThisWorkbook`、 `Sheet1`、 `Sheet2`或 `Sheet3` 模块。

  可以使用 `CallVSTOAssembly` 属性或 `GetManagedClass` 方法来访问向项目中的 VBA 代码公开的类的公共成员。

> [!NOTE]
> 在开发和部署解决方案时，可以在多个不同的文档副本中添加 VBA 代码。 有关详细信息，请参阅[向文档添加 VBA 代码的准则](#Guidelines)。

### <a name="use-the-callvstoassembly-property-in-a-visual-basic-project"></a>在 Visual Basic 项目中使用 CallVSTOAssembly 属性
 使用 `CallVSTOAssembly` 属性来访已添加到主机项类的公共成员。 例如，下面的 VBA 宏调用一个名为 `MyVSTOMethod` 的方法，该方法是在 Excel 工作簿项目的 `Sheet1` 类中定义的。

```vb
Sub MyMacro()
    Sheet1.CallVSTOAssembly.MyVSTOMethod()
End Sub
```

 与直接使用 `GetManagedClass` 方法相比，使用此属性，可以更加方便地调入自定义项程序集。 `CallVSTOAssembly` 返回一个对象，该对象表示向 VBA 公开的主机项类。 所返回对象的成员和方法参数将出现在 IntelliSense 中。

 `CallVSTOAssembly` 属性具有类似于以下代码的声明。 此代码假定已向 VBA 公开 Excel 工作簿项目中的名为 `Sheet1` 的 `ExcelWorkbook1` 主机项类。

```vb
Property Get CallVSTOAssembly() As ExcelWorkbook1.Sheet1
    Set CallVSTOAssembly = GetManagedClass(Me)
End Property
```

### <a name="use-the-getmanagedclass-method"></a>使用 GetManagedClass 方法
 若要使用全局 `GetManagedClass` 方法，请传入与主机项类相对应的 VBA 对象，该主机项来包含 **GetAutomationObject** 方法的替代。 然后，使用返回的对象访问向 VBA 公开的类。

 例如，下面的 VBA 宏调用一个名为 `MyVSTOMethod` 的方法，该方法是在名为 `Sheet1` 的 Excel 工作簿项目的 `ExcelWorkbook1`主机项类中定义的。

```vb
Sub CallVSTOMethod
    Dim VSTOSheet1 As ExcelWorkbook1.Sheet1
    Set VSTOSheet1 = GetManagedClass(Sheet1)
    VSTOSheet1.MyVSTOMethod
End Sub
```

 `GetManagedClass` 方法具有以下声明。

```vb
GetManagedClass(pdispInteropObject Object) As Object
```

 此方法返回一个对象，该对象表示向 VBA 公开的类。 所返回对象的成员和方法参数将出现在 IntelliSense 中。

## <a name="Guidelines"></a>向文档添加 VBA 代码的准则
 可在多个不同的文档副本中添加调入文档级自定义项的 VBA 代码。

 在开发和测试解决方案时，对于当你在 Visual Studio 中调试或运行项目时将打开的文档（即位于生成输出文件夹中的文档），你可以在其中编写 VBA 代码。 但是，在下次生成项目时，添加到此文档的任何 VBA 代码都将被覆盖，因为 Visual Studio 会将生成输出文件夹中的文档替换为主项目文件夹中文档的副本。

 如果要保存在调试或运行解决方案时添加到文档的 VBA 代码，请将 VBA 代码复制到项目文件夹内的文档中。 有关生成过程的详细信息，请参阅[生成 office 解决方案](../vsto/building-office-solutions.md)。

 准备好部署解决方案时，可以在三个主要文档位置中添加 VBA 代码。

### <a name="in-the-project-folder-on-the-development-computer"></a>开发计算机上的项目文件夹中
 如果你能够完全控制文档中的 VBA 代码和自定义项代码，则此位置非常方便。 由于文档位于开发计算机上，因此，如果更改自定义项代码，你可以轻松地修改 VBA 代码。 当你生成、调试和发布解决方案时，添加到此文档副本的 VBA 代码将保留在文档中。

 当文档在设计器中处于打开状态时，无法向其中添加 VBA 代码。 必须先在设计器中关闭文档，然后在 Word 或 Excel 中直接打开该文档。

> [!CAUTION]
> 如果添加在可以打开文档时运行的 VBA 代码，在极少数情况下，此代码可能损坏文档，或或使文档无法在设计器中打开。

### <a name="in-the-publish-or-installation-folder"></a>在发布或安装文件夹中
 在某些情况下，可能适合将 VBA 代码添加到发布文件夹或安装文件夹中的文档。 例如，如果 VBA 代码是由其他开发人员在未安装 Visual Studio 的计算机上编写和测试的，你可以选择此选项。

 如果用户直接从发布文件夹安装解决方案，则你必须在每次发布解决方案时将 VBA 代码添加到文档。 发布解决方案时，Visual Studio 将覆盖位于发布位置中的文档。

 如果用户从发布文件夹以外的安装文件夹安装解决方案，则可以避免在每次发布解决方案时向文档中添加 VBA 代码。 准备将发布更新从发布文件夹移动到安装文件夹时，请将除文档之外的所有文件复制到安装文件夹中。

### <a name="on-the-end-user-computer"></a>在最终用户计算机上
 如果最终用户是 VBA 开发人员并且将要调入你在文档级自定义项中提供的服务，则可以告诉他们如何通过在其文档副本中使用 `CallVSTOAssembly` 属性或 `GetManagedClass` 方法来调用你的代码。 当你将更新发布到解决方案时，不会覆盖最终用户计算机上的文档中的 VBA 代码，因为发布更新不会修改该文档。

## <a name="PropertyTasks"></a>由主机项属性执行的任务
 使用 **EnableVbaCallers** 和 **ReferenceAssemblyFromVbaProject** 属性时，Visual Studio 会执行几组不同的任务。

### <a name="enablevbacallers"></a>“属性”
 当你在 Visual Basic 项目中将主机项的 **EnableVbaCallers** 属性设置为 **True** 时，Visual Studio 将执行以下任务：

1. 向主机项类添加 <xref:Microsoft.VisualBasic.ComClassAttribute> 和 <xref:System.Runtime.InteropServices.ComVisibleAttribute> 特性。

2. 替代主机项类的 **GetAutomationObject** 方法。

3. 将主机项的 **ReferenceAssemblyFromVbaProject** 属性设置为 **True**。

   当你将 **EnableVbaCallers** 属性重新设置为 **False**时，Visual Studio 将执行以下任务：

4. 从 <xref:Microsoft.VisualBasic.ComClassAttribute> 类删除 <xref:System.Runtime.InteropServices.ComVisibleAttribute> 和 `ThisDocument` 特性。

5. 从主机项类删除 **GetAutomationObject** 方法。

   > [!NOTE]
   > Visual Studio 不会自动将 **ReferenceAssemblyFromVbaProject** 属性重新设置为 **False**。 可以使用 **“属性”** 窗口将此属性手动设置为 **False** 。

### <a name="referenceassemblyfromvbaproject"></a>ReferenceAssemblyFromVbaProject
 当 Visual Basic 项目或 Visual C# 项目中任何主机项的 **ReferenceAssemblyFromVbaProject** 属性设置为 **True**时，Visual Studio 将执行以下任务：

1. 为自定义程序集生成一个类型库，并将该类型库嵌入程序集。

2. 在文档内的 VBA 项目中添加对以下类型库的引用：

   - 自定义程序集的类型库。

   - Microsoft Visual Studio Tools for Office Execution Engine 9.0 类型库。 此类型库包含在 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]中。

   将 **ReferenceAssemblyFromVbaProject** 属性重新设置为 **False**时，Visual Studio 将执行以下任务：

3. 文档内的 VBA 项目中删除类型库引用。

4. 从程序集中删除嵌入的类型库。

## <a name="troubleshoot"></a>疑难解答
 下表列出了一些常见错误以及修复错误的建议。

|Error|建议|
|-----------|----------------|
|设置了 **EnableVbaCallers** 或 **ReferenceAssemblyFromVbaProject** 属性后，一条错误消息指明文档未包含 VBA 项目，或者你没有访问文档中的 VBA 项目的权限。|确保项目中的文档至少包含一个 VBA 宏、VBA 项目具有运行所需的足够的信任级别，并且 VBA 项目未受密码保护。|
|设置了 **“属性”** 或 **ReferenceAssemblyFromVbaProject** 属性后，一条错误消息指明缺少 <xref:System.Runtime.InteropServices.GuidAttribute> 声明或该声明已损坏。|确保声明位于项目中的 AssemblyInfo.cs 或*AssemblyInfo*文件中，并且此特性设置为有效的 GUID。 <xref:System.Runtime.InteropServices.GuidAttribute>|
|设置了 **“属性”** 或 **ReferenceAssemblyFromVbaProject** 属性后，一条错误消息指明 <xref:System.Reflection.AssemblyVersionAttribute> 指定的版本号无效。|确保项目中<xref:System.Reflection.AssemblyVersionAttribute>的*AssemblyInfo.cs*或*AssemblyInfo*文件中的声明设置为有效的程序集版本号。 有关有效的程序集版本号的信息，请参见 <xref:System.Reflection.AssemblyVersionAttribute> 类。|
|重命名自定义程序集后，调入自定义程序集的 VBA 代码将停止工作。|如果在向 VBA 代码公开自定义程序集之后更改其名称，则文档中的 VBA 项目与自定义程序集之间的链接将断开。 若要修复此问题，请将项目中的 **ReferenceFromVbaAssembly** 属性更改为 **False** ，并随后更改回 **True**，然后将 VBA 代码中对旧程序集名称的任何引用替换为新程序集名称。|

## <a name="see-also"></a>请参阅
- [如何：在 Visual Basic 项目中向 VBA 公开代码](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md)
- [如何：在 Visual C&#35;项目中向 VBA 公开代码](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md)
- [演练：在 Visual Basic 项目中调用 VBA 中的代码](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md)
- [演练：在 Visual C&#35;项目中调用 VBA 中的代码](../vsto/walkthrough-calling-code-from-vba-in-a-visual-csharp-project.md)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
- [Visual Studio 中的 VBA 和 Office 解决方案比较](../vsto/vba-and-office-solutions-in-visual-studio-compared.md)
- [程序文档级自定义项](../vsto/programming-document-level-customizations.md)
