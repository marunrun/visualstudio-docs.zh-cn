---
title: 从其他 Office 解决方案调用 VSTO 外接程序中的代码
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- VBA [Office development in Visual Studio], calling code in application-level add-ins
- application-level add-ins [Office development in Visual Studio], calling code from other solutions
- calling add-in code
- add-ins [Office development in Visual Studio], calling code from other solutions
- interoperability [Office development in Visual Studio]
- calling code from VBA
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5dbf56278a3987fafa0e0a0263c17460b56fafaf
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62939243"
---
# <a name="call-code-in-vsto-add-ins-from-other-office-solutions"></a>从其他 Office 解决方案调用 VSTO 外接程序中的代码
  可以向其他解决方案（包括其他 Microsoft Office 解决方案）公开 VSTO 外接程序中的对象。 如果 VSTO 外接程序提供了你希望使其他解决方案能够使用的服务，这一点非常有用。 例如，如果您有执行从 Web 服务的财务数据计算的 Microsoft Office Excel 的 VSTO 外接程序中，其他解决方案可以通过调用 Excel VSTO 外接程序在运行时执行这些计算。

 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

 此过程包括以下两个主要步骤：

- 在 VSTO 外接程序中，向其他解决方案公开对象。

- 在其他解决方案中，访问由 VSTO 外接程序公开的对象，然后调用对象的成员。

## <a name="types-of-solutions-that-can-call-code-in-an-add-in"></a>可以在外接程序中调用代码的解决方案类型
 您可以公开 VSTO 外接程序中向以下类型的解决方案的对象：

- 在与 VSTO 外接程序相同的应用程序进程中加载的文档中的 Visual Basic for Applications (VBA) 代码。

- 在与 VSTO 外接程序相同的应用程序进程中加载的文档级自定义项。

- 使用 Visual Studio 中的 Office 项目模板创建的其他 VSTO 外接程序。

- COM VSTO 外接程序（即直接实现 <xref:Extensibility.IDTExtensibility2> 接口的 VSTO 外接程序）。

- 在不同于 VSTO 外接程序的进程中运行的任何解决方案（这些类型的解决方案也称为 *进程外客户端*）。 其中包括使 Office 应用程序实现自动化的应用程序（例如 Windows 窗体或控制台应用程序），以及在其他进程中加载的 VSTO 外接程序。

## <a name="expose-objects-to-other-solutions"></a>向其他解决方案公开对象
 若要向其他解决方案公开 VSTO 外接程序中的对象，请在 VSTO 外接程序中执行下列步骤：

1. 定义要向其他解决方案公开的类。

2. 重写 <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> 类中的 `ThisAddIn` 方法。 返回要向其他解决方案公开的类的实例。

### <a name="define-the-class-you-want-to-expose-to-other-solutions"></a>定义你想要向其他解决方案公开的类
 要公开的类必须至少是公共类，必须将 <xref:System.Runtime.InteropServices.ComVisibleAttribute> 属性设置为 **true**，并且必须公开 [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) 接口。

 建议通过执行以下步骤公开 [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) 接口：

1. 定义一个接口，该接口声明要向其他解决方案公开的成员。 可以在 VSTO 外接程序项目中定义此接口。 但是，如果要向非 VBA 解决方案公开类，以便调用 VSTO 外接程序的解决方案无需引用 VSTO 外接程序项目即可引用此接口，则可能需要在单独的类库项目中定义此接口。

2. 将 <xref:System.Runtime.InteropServices.ComVisibleAttribute> 属性应用到此接口，并将此属性设置为 **true**。

3. 修改你的类以实现此接口。

4. 将应用<xref:System.Runtime.InteropServices.ClassInterfaceAttribute>属性为您的类，并将此属性设置为**无**的值<xref:System.Runtime.InteropServices.ClassInterfaceType>枚举。

5. 如果你想要公开此类向进程外客户端，可能还需要执行以下操作：

   - 从 <xref:System.Runtime.InteropServices.StandardOleMarshalObject>派生类。 有关详细信息，请参阅[公开向进程外客户端类](#outofproc)。

   - 在定义此接口的项目中设置“为 COM 互操作注册”  属性。 此属性是必需的仅当你想要启用客户端使用早期绑定来调入 VSTO 外接程序。

   下面的代码示例演示一个 `AddInUtilities` 类，该类具有可由其他解决方案调用的 `ImportData` 方法。 若要查看较大的演练上下文中此代码，请参阅[演练：从 VBA 调用 VSTO 外接程序中的代码](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md)。

   [!code-csharp[Trin_AddInInteropWalkthrough #3](../vsto/codesnippet/CSharp/Trin_AddInInteropWalkthrough/AddInUtilities.cs#3)]
   [!code-vb[Trin_AddInInteropWalkthrough#3](../vsto/codesnippet/VisualBasic/Trin_AddInInteropWalkthrough/AddInUtilities.vb#3)]

### <a name="expose-classes-to-vba"></a>公开到 VBA 类
 执行上述步骤时，VBA 代码只能调用在接口中声明的方法。 VBA 代码无法调用类中的任何其他方法，包括类从基类（如 <xref:System.Object>）中获取的方法。

 或者可以公开[IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch)通过设置接口<xref:System.Runtime.InteropServices.ClassInterfaceAttribute>属性的值 AutoDispatch 或 AutoDual<xref:System.Runtime.InteropServices.ClassInterfaceType>枚举。 如果您将该接口公开，您无需声明中单独的接口的方法。 不过，VBA 代码可以调用类中的任何公共方法和非静态方法，包括从基类（如 <xref:System.Object>）获取的方法。 此外，使用早期绑定的进程外客户端不能调用你的类。

### <a name="outofproc"></a> 公开向进程外客户端类
 如果要向进程外客户端公开 VSTO 外接程序中的类，则应从 <xref:System.Runtime.InteropServices.StandardOleMarshalObject> 派生该类，以确保进程外客户端可以调用公开的 VSTO 外接程序对象。 否则，尝试在进程外客户端中获取已公开对象的实例可能会意外失败。

 此失败是因为对 Office 应用程序的对象模型的所有调用必须都对主 UI 线程，但从进程外客户端对您的对象的调用都将到达任意 RPC （远程过程调用） 线程。 .NET Framework 中的 COM 封送处理机制不会切换线程，而是尝试将对你的对象的调用封送到传入 RPC 线程（而不是主 UI 线程）中。 如果你的对象是从 <xref:System.Runtime.InteropServices.StandardOleMarshalObject>派生的类的实例，则对你的对象的传入调用会自动封送到用于创建公开对象的线程中，该线程将是主机应用程序的主 UI 线程。

 在 Office 解决方案中使用线程的详细信息，请参阅[Office 中的线程支持](../vsto/threading-support-in-office.md)。

### <a name="override-the-requestcomaddinautomationservice-method"></a>重写 RequestComAddInAutomationService 方法
 以下代码示例演示了如何重写 VSTO 外接程序中 <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> 类中的 `ThisAddIn` 。 该示例假定您已经定义了一个名为类`AddInUtilities`你想要向其他解决方案公开。 若要查看较大的演练上下文中此代码，请参阅[演练：从 VBA 调用 VSTO 外接程序中的代码](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md)。

 [!code-csharp[Trin_AddInInteropWalkthrough#1](../vsto/codesnippet/CSharp/Trin_AddInInteropWalkthrough/ThisAddIn.cs#1)]
 [!code-vb[Trin_AddInInteropWalkthrough#1](../vsto/codesnippet/VisualBasic/Trin_AddInInteropWalkthrough/ThisAddIn.vb#1)]

 加载 VSTO 外接程序后， [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 将调用 <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> 方法。 在运行时将返回的对象分配给 COMAddIn.Object 属性<xref:Microsoft.Office.Core.COMAddIn>表示 VSTO 外接程序中的对象。 此 <xref:Microsoft.Office.Core.COMAddIn> 对象可供其他 Office 解决方案以及使 Office 实现自动化的解决方案使用。

## <a name="access-objects-from-other-solutions"></a>从其他解决方案访问对象
 若要调用 VSTO 外接程序中公开的对象，请在客户端解决方案中执行下列步骤：

1. 获取表示公开的 VSTO 外接程序的 <xref:Microsoft.Office.Core.COMAddIn> 对象。 通过在主机 Office 应用程序的对象模型中使用 `Application.COMAddIns` 属性，客户端可以访问所有可用的 VSTO 外接程序。

2. 访问的 COMAddIn.Object 属性<xref:Microsoft.Office.Core.COMAddIn>对象。 此属性从 VSTO 外接程序返回公开的对象。

3. 调用已公开对象的成员。

   使用 COMAddIn.Object 属性的返回值的方式是不同的 VBA 客户端和非 VBA 客户端。 对于进程外客户端，需要其他代码以避免可能的争用情况。

### <a name="access-objects-from-vba-solutions"></a>从 VBA 解决方案访问对象
 下面的代码示例演示如何使用 VBA 调用 VSTO 外接程序公开的方法。 此 VBA 宏将调用一个名为方法`ImportData`VSTO 外接程序中名为定义**ExcelImportData**。 若要查看较大的演练上下文中此代码，请参阅[演练：从 VBA 调用 VSTO 外接程序中的代码](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md)。

```vb
Sub CallVSTOMethod()
    Dim addIn As COMAddIn
    Dim automationObject As Object
    Set addIn = Application.COMAddIns("ExcelImportData")
    Set automationObject = addIn.Object
    automationObject.ImportData
End Sub
```

### <a name="access-objects-from-non-vba-solutions"></a>从非 VBA 解决方案访问对象
 在非 VBA 解决方案中，您必须将 COMAddIn.Object 属性值转换为它实现的接口，然后针对接口对象调用公开的方法。 以下代码示例演示了如何从不同的 VSTO 外接程序中调用 `ImportData` 方法，这些外接程序是通过使用 Visual Studio 中的 Office 开发人员工具创建的。

```vb
Dim addIn As Office.COMAddIn = Globals.ThisAddIn.Application.COMAddIns.Item("ExcelImportData")
Dim utilities As ExcelImportData.IAddInUtilities = TryCast( _
    addIn.Object, ExcelImportData.IAddInUtilities)
utilities.ImportData()
```

```csharp
object addInName = "ExcelImportData";
Office.COMAddIn addIn = Globals.ThisAddIn.Application.COMAddIns.Item(ref addInName);
ExcelImportData.IAddInUtilities utilities = (ExcelImportData.IAddInUtilities)addIn.Object;
utilities.ImportData();
```

 在此示例中，如果你尝试强制转换到 COMAddIn.Object 属性的值`AddInUtilities`类而不是`IAddInUtilities`接口，该代码将引发<xref:System.InvalidCastException>。

## <a name="see-also"></a>请参阅
- [VSTO 外接程序](../vsto/programming-vsto-add-ins.md)
- [演练：从 VBA 调用 VSTO 外接程序中的代码](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md)
- [开发 Office 解决方案](../vsto/developing-office-solutions.md)
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [VSTO 外接程序的体系结构](../vsto/architecture-of-vsto-add-ins.md)
- [通过使用扩展性接口自定义 UI 功能](../vsto/customizing-ui-features-by-using-extensibility-interfaces.md)
