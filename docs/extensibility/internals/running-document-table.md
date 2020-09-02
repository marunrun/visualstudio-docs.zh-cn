---
title: 运行文档表 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80705557"
---
# <a name="running-document-table"></a>运行文档表
IDE 将在名为正在运行的文档表 (RDT) 的内部结构中维护所有当前打开的文档的列表。 此列表包括内存中所有打开的文档，无论当前是否正在编辑这些文档。 文档是保存的任何项，包括项目中的文件或主项目文件 (例如，.vcxproj 文件) 。

## <a name="elements-of-the-running-document-table"></a>正在运行的文档表的元素
 正在运行的文档表包含以下条目。

|元素|说明|
|-------------|-----------------|
|文档名字对象|一个字符串，用于唯一标识文档数据对象。 这是管理文件的项目系统的绝对文件路径 (例如 C:\MyProject\MyFile) 。 此字符串还用于存储在文件系统以外的存储中的项目，例如数据库中的存储过程。 在这种情况下，项目系统可以使用唯一的字符串，它可以识别并可能进行分析以确定如何存储文档。|
|层次结构所有者|拥有文档的层次结构对象，由 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 接口表示。|
|项 ID|层次结构中特定项的项标识符。 此值在拥有此文档的层次结构中的所有文档中是唯一的，但不保证此值在不同的层次结构中是唯一的。|
|文档数据对象|至少，这是 `IUnknown`<br /><br /> 的名称。 IDE 不需要 `IUnknown` 自定义编辑器的文档数据对象的接口之外的任何特定接口。 但是，对于标准编辑器，需要使用编辑器的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> 接口实现来处理项目中的文件持久性调用。 有关详细信息，请参阅 [保存标准文档](../../extensibility/internals/saving-a-standard-document.md)。|
|Flags|在将项添加到 RDT 时，用于控制是否保存文档、是否应用读取或编辑锁定等的标志。 有关详细信息，请参见 <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> 枚举。|
|编辑锁定计数|编辑锁的计数。 编辑锁定指示某些编辑器已打开文档进行编辑。 当编辑锁的计数转换为零时，系统会提示用户保存文档（如果已修改）。 例如，每次使用 " **新建窗口** " 命令在编辑器中打开文档时，都会在 RDT 中为该文档添加一个编辑锁定。 为了设置编辑锁定，文档必须具有层次结构或项 ID。|
|读取锁定计数|读取锁的计数。 "读取锁定" 指示正在通过某种机制（如向导）读取文档。 读取锁定会在 RDT 中保留文档，同时指示文档无法编辑。 即使文档没有层次结构或项 ID，也可以设置读取锁定。 此功能允许您在内存中打开文档，并在 RDT 中输入文档，而无需将文档归任何层次结构所有。 此功能很少使用。|
|锁定持有者|接口的实例 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> 。 锁持有者是由功能（如在编辑器外打开和编辑文档的向导）实现的。 锁定持有者允许功能将编辑锁定添加到文档中，以防止文档在仍处于编辑状态时被关闭。 通常情况下，仅通过文档窗口 (来添加编辑锁，即编辑器) 。|

 RDT 中的每个条目都具有与之关联的唯一层次结构或项 ID，这通常对应于项目中的一个节点。 所有可编辑的文档通常归层次结构所有。 在 RDT 控件中所做的项可控制哪个项目，或者更准确地说，哪个层次结构当前拥有正在编辑的文档数据对象。 使用 RDT 中的信息，IDE 可以防止多个项目同时打开文档。

 层次结构还控制数据的持久性，并使用 RDT 中的信息来更新 " **保存** " 和 " **另存为** " 对话框。 当用户修改文档，然后从 "**文件**" 菜单中选择 "**退出**" 命令时，IDE 将在 "**保存更改**" 对话框中提示您显示当前修改的所有项目和项目项。 这允许用户选择要保存的文档。 要保存的文档的列表 (也就是说，具有更改) 的文档将从 RDT 生成。 您希望在退出应用程序时在 " **保存更改** " 对话框中看到的任何项都应在 RDT 中具有记录。 RDT 使用每个文档的标志条目中指定的值来协调保存哪些文档以及是否提示用户保存操作。 有关 RDT 标志的详细信息，请参阅 <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> 枚举。

## <a name="edit-locks-and-read-locks"></a>编辑锁和读取锁
 编辑锁和读取锁定驻留在 RDT 中。 文档窗口会递增和递减编辑锁定。 因此，当用户打开新的文档窗口时，编辑锁计数将递增1。 当编辑锁的数量达到零时，将向层次结构发出信号，以便保留或保存相关文档的数据。 然后，层次结构可以以任何方式持久保存数据，包括将其作为文件或存储库中的项保存。 您可以使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.LockDocument%2A> 接口中的方法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable> 来添加编辑锁和读取锁定，并使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnlockDocument%2A> 方法来删除这些锁。

 通常，当编辑器的文档窗口被实例化时，窗口框架会自动在 RDT 中为文档添加编辑锁定。 但是，如果您创建的文档的自定义视图不使用标准文档窗口 (也就是说，它不会实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> 接口) ，则需要设置您自己的编辑锁定。 例如，在向导中，将编辑文档而不在编辑器中打开。 为了使文档锁通过向导和类似的实体打开，这些实体必须实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> 接口。 若要注册文档锁持有者，请调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.RegisterDocumentLockHolder%2A> 方法，并传入 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> 实现。 这样做会将文档锁持有者添加到 RDT。 实现文档锁持有者的另一种情况是，通过一个特殊的工具窗口打开文档。 在此实例中，您无法使工具窗口关闭文档。 但是，通过在 RDT 中注册为文档锁持有者，IDE 可以调用方法的实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder.CloseDocumentHolder%2A> 来提示关闭文档。

## <a name="other-uses-of-the-running-document-table"></a>正在运行的文档表的其他用法
 IDE 中的其他实体使用 RDT 来获取有关文档的信息。 例如，源代码管理器在获取文件的最新版本后，使用 RDT 指示系统在编辑器中重新加载文档。 为此，源代码管理管理器会在 RDT 中查找文件，以查看其中是否有任何打开。 如果是，则源代码管理管理器首先检查层次结构是否实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> 方法。 如果项目未实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> 方法，则源代码管理器会 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A> 直接在文档数据对象上检查方法的实现。

 如果用户请求该文档，IDE 还会使用 RDT 将 resurface (置于打开的文档的) 前面。 有关详细信息，请参阅 [使用 "打开文件" 命令显示文件](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md)。 若要确定文件是否在 RDT 中打开，请执行以下操作之一。

- 查询文档名字对象 (即，整个文档路径) ，以找出项目是否已打开。

- 使用 "层次结构" 或 "项 ID" 请求项目系统获取完整文档路径，然后在 RDT 中查看项目。

## <a name="see-also"></a>另请参阅
- [RDT_ReadLock 用法](../../extensibility/internals/rdt-readlock-usage.md)
- [持久性和正在运行的文档表](../../extensibility/internals/persistence-and-the-running-document-table.md)
