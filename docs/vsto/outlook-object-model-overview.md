---
title: Outlook 对象模型概述
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.ProjectItem.OutlookAddin
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook [Office development in Visual Studio], object model overview
- object models [Office development in Visual Studio], Office
- objects [Office development in Visual Studio], Office object models
- object models [Office development in Visual Studio], Outlook
- Office object models
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6545815a0a24a3ba8579298151194fdd81edee77
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72985683"
---
# <a name="outlook-object-model-overview"></a>Outlook 对象模型概述
  若要开发 Microsoft Office Outlook 的 VSTO 外接程序，可以与 Outlook 对象模型提供的对象进行交互。 Outlook 对象模型提供表示用户界面中的项的类和接口。 例如， <xref:Microsoft.Office.Interop.Outlook.Application> 对象表示整个应用程序， <xref:Microsoft.Office.Interop.Outlook.Folder> 对象表示包含电子邮件或其他项的文件夹， <xref:Microsoft.Office.Interop.Outlook.MailItem> 对象表示电子邮件。

 本主题简要概述了 Outlook 对象模型中一些主要对象。 有关可了解整个 Outlook 对象模型的详细信息的资源，请参阅[使用 outlook 对象模型文档](#refdoc)。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="access-objects-in-an-outlook-project"></a>访问 Outlook 项目中的对象
 Outlook 提供了许多可与之交互的对象。 若要有效地使用对象模型，你应熟悉以下顶级对象：

- <xref:Microsoft.Office.Interop.Outlook.Application>

- <xref:Microsoft.Office.Interop.Outlook.Explorer>

- <xref:Microsoft.Office.Interop.Outlook.Inspector>

- <xref:Microsoft.Office.Interop.Outlook.Folder>

- <xref:Microsoft.Office.Interop.Outlook.MailItem>

- <xref:Microsoft.Office.Interop.Outlook.AppointmentItem>

- <xref:Microsoft.Office.Interop.Outlook.TaskItem>

- <xref:Microsoft.Office.Interop.Outlook.ContactItem>

### <a name="application-object"></a>应用程序对象
 <xref:Microsoft.Office.Interop.Outlook.Application> 对象表示 Outlook 应用程序，并且它是 Outlook 对象模型中最高级别的对象。 此对象的一些最重要的成员包括：

- [CreateItem](/previous-versions/office/developer/office-2003/aa220082(v=office.11)) 方法，可用于创建新项，如电子邮件、任务或约会。

- <xref:Microsoft.Office.Interop.Outlook._Application.Explorers%2A> 属性，可用于访问将文件夹的内容显示在 Outlook 用户界面 (UI) 中的窗口。

- <xref:Microsoft.Office.Interop.Outlook._Application.Inspectors%2A> 属性，可用于访问显示单个项（如电子邮件或会议请求）的内容的窗口。

  若要获取 <xref:Microsoft.Office.Interop.Outlook.Application> 对象的实例，请使用项目中 `ThisAddIn` 类的应用程序字段。 有关详细信息，请参阅[PROGRAM VSTO 外接程序](../vsto/programming-vsto-add-ins.md)。

> [!NOTE]
> 若要在使用 Outlook 对象模型防护阻止的属性和方法时避免出现安全警告，请从 `ThisAddIn` 类的应用程序字段获取 Outlook 对象。 有关详细信息，请参阅[Office 解决方案的特定安全注意事项](../vsto/specific-security-considerations-for-office-solutions.md)。

### <a name="explorer-object"></a>资源管理器对象
 <xref:Microsoft.Office.Interop.Outlook.Explorer> 对象表示一个窗口，该窗口显示包含项（如电子邮件、任务或约会）的文件夹的内容。 <xref:Microsoft.Office.Interop.Outlook.Explorer> 对象包括方法和属性，可用于修改窗口以及窗口更改时引发的事件。

 若要获取 <xref:Microsoft.Office.Interop.Outlook.Explorer> 对象，请执行以下操作之一：

- 使用 <xref:Microsoft.Office.Interop.Outlook._Application.Explorers%2A> 对象的 <xref:Microsoft.Office.Interop.Outlook.Application> 属性来访问 Outlook 中的所有 <xref:Microsoft.Office.Interop.Outlook.Explorer> 对象。

- 使用 <xref:Microsoft.Office.Interop.Outlook._Application.ActiveExplorer%2A> 对象的 <xref:Microsoft.Office.Interop.Outlook.Application> 方法以获取当前具有焦点的 <xref:Microsoft.Office.Interop.Outlook.Explorer> 。

- 使用 <xref:Microsoft.Office.Interop.Outlook.Folder> 对象的 `GetExplorer` 方法以获取当前文件夹的 <xref:Microsoft.Office.Interop.Outlook.Explorer>。

### <a name="inspector-object"></a>检查器对象
 <xref:Microsoft.Office.Interop.Outlook.Inspector> 对象表示一个窗口，该窗口显示单个项，如电子邮件、任务或约会。 <xref:Microsoft.Office.Interop.Outlook.Inspector> 对象包括方法和属性，可用于修改窗口以及窗口更改时引发的事件。

 若要获取 <xref:Microsoft.Office.Interop.Outlook.Inspector> 对象，请执行以下操作之一：

- 使用 <xref:Microsoft.Office.Interop.Outlook._Application.Inspectors%2A> 对象的 <xref:Microsoft.Office.Interop.Outlook.Application> 属性来访问 Outlook 中的所有 <xref:Microsoft.Office.Interop.Outlook.Inspector> 对象。

- 使用 <xref:Microsoft.Office.Interop.Outlook._Application.ActiveInspector%2A> 对象的 <xref:Microsoft.Office.Interop.Outlook.Application> 方法以获取当前具有焦点的 <xref:Microsoft.Office.Interop.Outlook.Inspector> 。

- 使用特定项的 `GetInspector` 方法（如 <xref:Microsoft.Office.Interop.Outlook.MailItem> 或 <xref:Microsoft.Office.Interop.Outlook.AppointmentItem>）来检索与之关联的检查器。

### <a name="folder-object"></a>Folder 对象
 <xref:Microsoft.Office.Interop.Outlook.Folder> 对象表示包含电子邮件、联系人、任务和其他项的文件夹。 Outlook 提供了 16 个默认的 <xref:Microsoft.Office.Interop.Outlook.Folder> 对象。

 默认的 <xref:Microsoft.Office.Interop.Outlook.Folder> 对象由 <xref:Microsoft.Office.Interop.Outlook.OlDefaultFolders> 枚举值定义。 例如，应用于对象的

 OlDefaultFolders olFolderInbox 对应于 Outlook 中的**收件箱**文件夹。

 有关演示如何访问默认 <xref:Microsoft.Office.Interop.Outlook.Folder> 和创建新 <xref:Microsoft.Office.Interop.Outlook.Folder>的示例，请参阅[如何：以编程方式创建自定义文件夹项](../vsto/how-to-programmatically-create-custom-folder-items.md)。

### <a name="mailitem-object"></a>MailItem 对象
 <xref:Microsoft.Office.Interop.Outlook.MailItem> 对象表示一封电子邮件。 <xref:Microsoft.Office.Interop.Outlook.MailItem> 对象通常在文件夹中，如 **“收件箱”**、 **“已发送的项目”** 和 **“发件箱”**。 <xref:Microsoft.Office.Interop.Outlook.MailItem> 公开可用于创建和发送电子邮件的属性和方法。

 有关演示如何创建电子邮件的示例，请参阅[如何：以编程方式创建电子邮件项](../vsto/how-to-programmatically-create-an-e-mail-item.md)。

### <a name="appointmentitem-object"></a>AppointmentItem 对象
 <xref:Microsoft.Office.Interop.Outlook.AppointmentItem> 对象表示会议、一次约会，或 **“日历”** 文件夹中的定期约会或会议。 <xref:Microsoft.Office.Interop.Outlook.AppointmentItem> 对象包含执行操作（如响应或转发会议请求）的方法和指定会议详细信息（如位置和时间）的属性。

 有关演示如何创建约会的示例，请参阅[如何：以编程方式创建会议请求](../vsto/how-to-programmatically-create-a-meeting-request.md)。

### <a name="taskitem-object"></a>TaskItem 对象
 <xref:Microsoft.Office.Interop.Outlook.TaskItem> 对象表示要在指定时间范围内执行的任务。 <xref:Microsoft.Office.Interop.Outlook.TaskItem> 对象位于 **“任务”** 文件夹中。

 若要创建任务，请使用 [对象的](/previous-versions/office/developer/office-2003/aa220082(v=office.11)) CreateItem <xref:Microsoft.Office.Interop.Outlook.Application> 方法，并为参数传入值 <xref:Microsoft.Office.Interop.Outlook.OlItemType.olTaskItem> 。

### <a name="contactitem-object"></a>ContactItem 对象
 <xref:Microsoft.Office.Interop.Outlook.ContactItem>对象表示 "**联系人**" 文件夹中的联系人。 <xref:Microsoft.Office.Interop.Outlook.ContactItem> 对象包含它们表示的人员的各种联系信息，如街道地址、电子邮件地址和电话号码。

 有关演示如何创建新联系人的示例，请参阅[如何：以编程方式将条目添加到 Outlook 联系人](../vsto/how-to-programmatically-add-an-entry-to-outlook-contacts.md)。 有关演示如何搜索现有联系人的示例，请参阅[如何：以编程方式搜索特定联系人](../vsto/how-to-programmatically-search-for-a-specific-contact.md)。

## <a name="refdoc"></a>使用 Outlook 对象模型文档
 有关 Outlook 对象模型的完整信息，可以参考 Outlook 主互操作程序集 (PIA) 引用和 VBA 对象模型引用。

### <a name="primary-interop-assembly-reference"></a>主互操作程序集引用
 Outlook PIA 引用记录了 Outlook 2010 的主互操作程序集中的类型。 有关详细信息，请参阅[Outlook 2010 主互操作程序集引用](/previous-versions/office/developer/office-2010/bb652780(v=office.14))。

 除了提供 PIA 中所有类型的信息以外，本文档还提供有关 PIA 的结构和常见 Outlook 自动化任务的代码示例的其他信息。

### <a name="vba-object-model-reference"></a>VBA 对象模型引用
 VBA 对象模型引用在 Outlook 对象模型被公开到 Visual Basic for Applications (VBA) 代码时记录该对象模型。 有关详细信息，请参阅[Outlook 2010 对象模型引用](/office/vba/api/overview/Outlook/object-model)。

 VBA 对象模型引用中的所有对象和成员都对应于 Outlook PIA 中的类型和成员。 例如，VBA 对象模型引用中的检查器对象对应于 Outlook PIA 中的 <xref:Microsoft.Office.Interop.Outlook.Inspector> 对象。 虽然 VBA 对象模型引用提供大多数属性、方法和事件的代码示例，但如果想要将其用于使用 Visual Studio 创建的 Outlook VSTO 外接程序项目，则必须将本引用中的 VBA 代码转换成 Visual Basic 或 Visual C#。

### <a name="related-topics"></a>相关主题

|Title|描述|
|-----------|-----------------|
|[处理联系人项](../vsto/working-with-contact-items.md)|提供了演示如何使用联系人执行任务的主题。|
|[使用邮件项](../vsto/working-with-mail-items.md)|提供了演示如何使用邮件项执行任务的主题。|
|[使用文件夹](../vsto/working-with-folders.md)|提供了演示如何使用文件夹执行任务的主题。|
|[使用日历项](../vsto/working-with-calendar-items.md)|提供了演示如何使用日历项执行任务的主题。|
|[如何：以编程方式确定当前的 Outlook 项](../vsto/how-to-programmatically-determine-the-current-outlook-item.md)|演示如何显示当前文件夹的名称及有关所选项的一些信息。|
