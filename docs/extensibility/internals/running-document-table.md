---
title: 正在运行的文档表 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- read locks
- running document table (RDT), IVsDocumentLockHolder interface
- running document table (RDT)
- running document table (RDT), edit locks
- document data objects, running document table
ms.assetid: bbec74f3-dd8e-48ad-99c1-2df503c15f5a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9e6aa882921786b1592922372581beae8c4c2443
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705557"
---
# <a name="running-document-table"></a>运行文档表
IDE 在称为正在运行的文档表 （RDT） 的内部结构中维护所有当前打开的文档的列表。 此列表包括内存中的所有打开的文档，无论这些文档当前是否正在编辑。 文档是持久化的任何项，包括项目或主项目文件中的文件（例如 .vcxproj 文件）。

## <a name="elements-of-the-running-document-table"></a>正在运行的文档表的元素
 正在运行的文档表包含以下条目。

|元素|描述|
|-------------|-----------------|
|文档名字|唯一标识文档数据对象的字符串。 这将是管理文件的项目系统（例如，C：_MyProject_MyFile）的绝对文件路径。 此字符串还用于保存在文件系统以外的存储中的项目，例如数据库中的存储过程。 在这种情况下，项目系统可以发明一个唯一的字符串，它可以识别并可能解析，以确定如何存储文档。|
|层次结构所有者|拥有文档的层次结构对象，由<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>接口表示。|
|项目 ID|层次结构中特定项的项标识符。 此值在层次结构中拥有此文档的所有文档中是唯一的，但不能保证此值在不同的层次结构中是唯一的。|
|文档数据对象|至少，这是一个`IUnknown`<br /><br /> 的名称。 IDE 不需要自定义编辑器文档数据对象的`IUnknown`接口之外的任何特定接口。 但是，对于标准编辑器，需要编辑器实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>接口来处理来自项目的文件持久性调用。 有关详细信息，请参阅[保存标准文档](../../extensibility/internals/saving-a-standard-document.md)。|
|标志|当条目添加到 RDT 时，可以指定控制文档是否保存、是否应用读取锁或编辑锁的标志，等等。 有关详细信息，请参见 <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> 枚举。|
|编辑锁计数|编辑锁计数。 编辑锁指示某些编辑器打开了文档进行编辑。 当编辑的计数锁定转换为零时，如果文档已被修改，系统将提示用户保存文档。 例如，每次使用 **"新建窗口"** 命令在编辑器中打开文档时，RDT 中都会为该文档添加编辑锁。 为了设置编辑锁，文档必须具有层次结构或项目 ID。|
|读取锁计数|读取锁计数。 读取锁表示文档正在通过某些机制（如向导）进行读取。 读取锁在 RDT 中保留文档处于活动状态，同时指示无法编辑文档。 即使文档没有层次结构或项目 ID，也可以设置读取锁。 此功能允许您在内存中打开文档，并在 RDT 中输入它，而无需任何层次结构拥有该文档。 此功能很少使用。|
|锁架|接口的<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder>实例。 锁架由打开和编辑编辑器外部文档的向导等功能实现。 锁定持有人允许该功能向文档添加编辑锁，以防止文档在仍在编辑时关闭。 通常，编辑锁仅由文档窗口（即编辑器）添加。|

 RDT 中的每个条目都有与其关联的唯一层次结构或项 ID，通常对应于项目中的一个节点。 所有可用于编辑的文档通常归层次结构所有。 RDT 中所做的条目控制当前具有要编辑的文档数据对象的哪个项目（或者更准确地说）哪个层次结构。 使用 RDT 中的信息，IDE 可以防止文档一次被多个项目打开。

 层次结构还控制数据的持久性，并使用 RDT 中的信息更新 **"保存****和保存为"** 对话框。 当用户修改文档，然后从 **"文件"** 菜单中选择 **"退出**"命令时，IDE 会用 **"保存更改"** 对话框提示他们，向他们显示当前修改的所有项目和项目项。 这允许用户选择要保存的文档。 要保存的文档列表（即具有更改的文档）是从 RDT 生成的。 您希望在退出应用程序时在"**保存更改"** 对话框中看到的任何项都应在 RDT 中具有记录。 RDT 协调保存的文档以及是否使用每个文档的"标志"条目中指定的值提示用户进行保存操作。 有关 RDT 标志的详细信息，请参阅<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS>枚举。

## <a name="edit-locks-and-read-locks"></a>编辑锁和读取锁
 编辑锁和读取锁驻留在 RDT 中。 文档窗口递增并递减编辑锁。 因此，当用户打开新的文档窗口时，编辑锁计数将递增 1。 当编辑锁数达到零时，将发出策略，以保留或保存关联文档的数据。 然后，层次结构可以以任何方式保留数据，包括作为文件或存储库中的项保留。 可以使用接口中<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.LockDocument%2A><xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable>的方法添加编辑锁和读取锁，<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnlockDocument%2A>以及删除这些锁的方法。

 通常，当实例化编辑器的文档窗口时，窗口框架会自动在 RDT 中为文档添加编辑锁。 但是，如果创建不使用标准文档窗口的文档的自定义视图（即，它不实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame>接口），则需要设置自己的编辑锁。 例如，在向导中，在不在编辑器中打开的情况下编辑文档。 为了使向导和类似实体打开文档锁，这些实体必须实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder>接口。 要注册文档锁定持有者，<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.RegisterDocumentLockHolder%2A>请调用 方法并传递实现。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> 这样做会将文档锁定持有者添加到 RDT。 实现文档锁定持有者的另一个方案是，如果通过专用工具窗口打开文档。 在这种情况下，您无法让工具窗口关闭文档。 但是，通过在 RDT 中注册为文档锁定持有者，IDE 可以调用方法的<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder.CloseDocumentHolder%2A>实现以提示文档的关闭。

## <a name="other-uses-of-the-running-document-table"></a>正在运行的文档表的其他用途
 IDE 中的其他实体使用 RDT 获取有关文档的信息。 例如，源代码管理管理器在获取文件的最新版本后，使用 RDT 告诉系统在编辑器中重新加载文档。 为此，源代码管理管理器会查找 RDT 中的文件，以查看这些文件中是否有任何文件处于打开状态。 如果是，则源代码管理管理器首先检查层次结构是否实现该方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A>。 如果项目未实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A>该方法，则源代码管理管理器将直接检查文档数据对象上<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A>方法的实现。

 如果用户请求该文档，IDE 还使用 RDT 重新显示（将打开的文档带到前面）。 有关详细信息，请参阅[使用打开的文件命令显示文件](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md)。 要确定该文件是否在 RDT 中打开，请执行以下操作之一。

- 查询文档名字对象（即完整文档路径），以了解项目是否打开。

- 使用层次结构或项目 ID 向项目系统询问完整的文档路径，然后在 RDT 中向上查找该项目。

## <a name="see-also"></a>请参阅
- [RDT_ReadLock 用法](../../extensibility/internals/rdt-readlock-usage.md)
- [持久性和正在运行的文档表](../../extensibility/internals/persistence-and-the-running-document-table.md)
