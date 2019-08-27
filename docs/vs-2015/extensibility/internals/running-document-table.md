---
title: 运行文档表 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- read locks
- running document table (RDT), IVsDocumentLockHolder interface
- running document table (RDT)
- running document table (RDT), edit locks
- document data objects, running document table
ms.assetid: bbec74f3-dd8e-48ad-99c1-2df503c15f5a
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7ea32df892efa47c91d8292bdc9065080318a059
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68155560"
---
# <a name="running-document-table"></a>运行文档表
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

IDE 维护名为运行文档表 (RDT) 的内部结构中的所有当前打开的文档的列表。 此列表包括所有打开的文档在内存中，而不考虑是否当前正在编辑这些文档。 文档是包括一个项目或主项目文件 （例如，.vcxproj 文件） 中的文件的保存的任何项。  
  
## <a name="elements-of-the-running-document-table"></a>运行文档表的元素  
 运行文档表包含以下各项。  
  
|元素|描述|  
|-------------|-----------------|  
|文档名字对象|一个字符串，唯一标识该文档数据对象。 这将是一个管理文件 (例如，C:\MyProject\MyFile) 的项目系统绝对文件路径。 此字符串还用于在文件系统，如在数据库中的存储过程以外的存储中保存的项目。 在这种情况下，项目系统可以创造的唯一字符串，它可以识别和可能是分析以确定如何将文档存储。|  
|层次结构所有者|拥有该文档，由表示的层次结构对象<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>接口。|  
|项 ID|在层次结构中的特定项的项标识符。 此值是唯一的而拥有本文档的层次结构中的所有文档，但此值不能保证是唯一不同的层次结构。|  
|文档数据对象|最小值，这是 `IUnknown`<br /><br /> 的名称。 IDE 不需要任何特定的接口之外`IUnknown`自定义编辑器的文档数据对象的接口。 但是，对于标准编辑器中，在编辑器实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>处理从项目文件持久性调用所需的接口。 有关详细信息，请参阅[正在保存标准文档](../../extensibility/internals/saving-a-standard-document.md)。|  
|Flags|用于控制是否保存文档时，是否将应用的读取或编辑锁的标志，依此类推，可在项添加到 RDT 时指定。 有关详细信息，请参见 <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> 枚举。|  
|编辑锁计数|编辑锁定计数。 编辑锁定指示某些编辑器已打开进行编辑的文档。 当编辑锁定计数将转换为零，提示用户保存文档，如果已修改。 例如，每次使用编辑器中打开文档时**新的窗口**命令时，编辑锁添加 RDT 中该文档。 为了使编辑锁定设置，该文档必须有一个层次结构或项 id。|  
|读取锁计数|读取的计数锁。 一个读取的锁定指示通过一些机制，如向导读取文档。 一个读取的锁定将文档保留在 RDT 中处于活动状态时，该值指示不能编辑该文档。 可以设置一个读取的锁定，即使该文档不会有一个层次结构或项 id。 此功能，可在内存中打开文档，并将其填入 RDT 而无需所拥有的任何层次结构的文档。 很少使用此功能。|  
|锁的持有者|实例<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder>接口。 锁持有者被实现的功能，例如打开和编辑文档编辑器之外的向导。 锁持有者允许将编辑锁定添加到文档后，若要防止文档被关闭，但它仍正在编辑的功能。 通常情况下，编辑锁仅添加的文档窗口 （即，编辑器）。|  
  
 RDT 中的每个条目都有唯一的层次结构或与之关联，这通常对应于项目中的一个节点的项 ID。 可用于编辑的所有文档通常都属于层次结构。 条目在 RDT 中进行控制的项目，或-更准确地说 — 的层次结构中，当前拥有所编辑的文档数据对象。 在 RDT 中使用的信息，IDE 可以避免文档中，在每次打开多个项目。  
  
 在层次结构还控制数据的持久性，并在 RDT 中使用的信息来更新**保存**并**另存为**对话框。 当用户修改文档，然后选择**退出**命令**文件**菜单中，IDE 会提示他们与**保存更改**对话框以显示它们的所有项目和当前修改的项目项。 这允许用户选择的要保存的文档。 若要保存的文档的列表 （即，需要更改这些文档） 从 RDT 生成。 你希望看到中任何项**保存更改**对话框在退出该应用程序时应已 RDT 中的记录。 RDT 协调是否已保存的文档，并且是否保存有关提示用户使用的每个文档的标志条目中指定的值的操作。 RDT 标志的详细信息，请参阅<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS>枚举。  
  
## <a name="edit-locks-and-read-locks"></a>编辑锁和读取锁  
 编辑锁定和读的锁定驻留在 RDT。 文档窗口递增和递减编辑锁定。 因此，当用户在打开新文档窗口中，编辑锁计数递增 1。 当编辑锁的数目达到零时，层次结构是发出信号，以持久保存或保存的数据关联的文档。 在层次结构稍后可以保存以任何方式，包括持久保存为文件或存储库中的项的数据。 可以使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.LockDocument%2A>中的方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable>界面，用于添加编辑锁和读取锁定，和<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnlockDocument%2A>方法如何解除这些锁定。  
  
 通常情况下，实例化一个编辑器的文档窗口时，窗口框架会自动添加文档的编辑锁 RDT 中。 但是，如果你创建文档的自定义视图，不使用标准的文档窗口 (即，它不实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame>接口)，则需要设置自己编辑的锁。 例如，在向导中，文档编辑而无需在编辑器中打开。 为了使文档锁定，若要打开的向导和类似的实体，这些实体还必须实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder>接口。 若要注册文档锁持有者，请调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.RegisterDocumentLockHolder%2A>方法，并传入你<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder>实现。 执行此操作向 RDT 文档锁持有者。 用于实现文档锁持有者的另一种情况是如果打开的文档中通过特殊工具窗口。 在本例中，您不能具有工具窗口中关闭文档。 但是，通过注册为 RDT 中文档锁持有者，IDE 可以调用的实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder.CloseDocumentHolder%2A>方法提示文档的关闭。  
  
## <a name="other-uses-of-the-running-document-table"></a>运行文档表的其他用法  
 在 IDE 中的其他实体使用 RDT 来获取有关文档的信息。 例如，源代码控制管理器使用 RDT 来告诉系统以获取最新版本的文件之后重新加载编辑器中的文档。 若要执行此操作，源代码控制管理器查找中 RDT 若要查看其中任何一个已打开的文件。 如果它们是的则源代码控制管理器首先检查以查看层次结构实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A>方法。 如果项目不实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A>方法，则源控制管理器的实现会检查<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A>文档的数据对象直接的方法。  
  
 IDE 还使用 RDT resurface （自带到前面） 打开的文档，如果用户请求该文档。 有关详细信息，请参阅[通过使用打开文件命令显示文件](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md)。 若要确定是否在 RDT 中打开文件，请执行下列操作之一。  
  
- 若要了解是否项已打开的文档名字对象 （即完整的文档路径） 的查询。  
  
- 使用层次结构或项 ID 要求完整的文档路径，项目系统，然后在 RDT 中查找项。  
  
## <a name="see-also"></a>请参阅  
 [RDT_ReadLock 用法](../../extensibility/internals/rdt-readlock-usage.md)   
 [持久性和正在运行的文档表](../../extensibility/internals/persistence-and-the-running-document-table.md)
