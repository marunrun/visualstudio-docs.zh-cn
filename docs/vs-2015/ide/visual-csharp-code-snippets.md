---
title: Visual C# 代码片段 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- snippets [C#], default snippets
- snippets [C#], Code Snippet Inserter
- Code Snippet Inserter [J#]
- Code Snippet Inserter [C#]
- Visual C#, default snippets
ms.assetid: dbea3dd6-e650-4190-b874-c9f097d7de6e
caps.latest.revision: 37
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 4655ea7160d353fc8735a9025f36de368f247ba8
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65698185"
---
# <a name="visual-c-code-snippets"></a>Visual C# 代码段
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

代码片段是现成的代码段，可快速插入到代码中。 例如，`for` 代码片段刻创建一个空 `for` 循环。 有些代码片段为外侧代码片段，让你可以选择代码行，然后选择包含所选代码行的代码片段。 例如，选择代码行并激活 `for` 代码片段时，会通过循环块内的代码行创建 `for` 循环。 使用代码片段可以更快、更容易且更可靠地编写程序代码。  
  
 可以在光标位置插入代码片段，或者在当前所选代码旁插入外侧代码片段。 可以通过 **IntelliSense** 菜单上的 **Insert Code Snippet** 或 **Surround With** 命令调用代码片段插入器，也可分别使用 CTRL+K 再加 X 或 CTRL+K 再加 S 键盘快捷键调用。  
  
 代码片段插入器显示所有可用代码片段的代码片段名称。 代码片段插入器还包括输入对话框，可在其中键入代码片段名称或部分代码片段。 代码片段插入器突出显示与代码片段名称最接近的匹配。 在任何时候按 Tab 键都可消除代码片段插入器，并插入当前选定的代码片段。 按 ESC 键或在代码编辑器中单击鼠标可解除代码片段插入器，而不会插入代码片段。  
  
## <a name="default-code-snippets"></a>默认代码片段  
 默认情况下，Visual Studio 包含以下代码片段。  
  
|名称（或快捷方式）|描述|要插入代码片段的有效位置|  
|--------------------------|-----------------|---------------------------------------|  
|#if|创建 [#if](https://msdn.microsoft.com/library/48cabbff-ca82-491f-a56a-eeccd528c7c2) 指令和 [#endif](https://msdn.microsoft.com/library/6a5fca55-5aee-441f-86f6-1c99fbe9ec05) 指令。|任何位置。|  
|#region|创建 [#region](https://msdn.microsoft.com/library/672c87d1-9771-4f64-ab3f-0ad3d4ffb2b4) 指令和 [#endregion](https://msdn.microsoft.com/library/16099660-91b2-49e5-9646-77f9ef069526) 指令。|任何位置。|  
|~|创建包含类的析构函数。|在类中。|  
|attribute|为派生自 <xref:System.Attribute> 的类创建声明。|在命名空间（包括全局命名空间）、类或结构中。|  
|checked|创建 [checked](https://msdn.microsoft.com/library/718a1194-988d-48a3-b089-d6ee8bd1608d) 块。|在方法、索引器、属性访问器或事件访问器内。|  
|class|创建类声明。|在命名空间（包括全局命名空间）、类或结构中。|  
|ctor|创建包含类的构造函数。|在类中。|  
|cw|创建对 <xref:System.Console.WriteLine%2A> 的调用。|在方法、索引器、属性访问器或事件访问器内。|  
|do|创建 [do](https://msdn.microsoft.com/library/50725f79-9ba6-4898-aa78-6e331568a1bb)`while` 循环。|在方法、索引器、属性访问器或事件访问器内。|  
|else|创建 [else](https://msdn.microsoft.com/library/d9a1d562-8cf5-4bd4-9ba7-8ad970cd25b2) 块。|在方法、索引器、属性访问器或事件访问器内。|  
|enum|创建[枚举](https://msdn.microsoft.com/library/bbeb9a0f-e9b3-41ab-b0a6-c41b1a08974c)声明。|在命名空间（包括全局命名空间）、类或结构中。|  
|equals|创建一个方法声明，该声明对 <xref:System.Object> 类中定义的 <xref:System.Object.Equals%2A> 方法进行重写。|在类或结构中。|  
|equals|为某个从异常（默认情况下为 <xref:System.Exception>）派生的类创建声明。|在命名空间（包括全局命名空间）、类或结构中。|  
|for|创建 [for](https://msdn.microsoft.com/library/34041a40-2c87-467a-9ffb-a0417d8f67a8) 循环。|在方法、索引器、属性访问器或事件访问器内。|  
|foreach|创建 [foreach](https://msdn.microsoft.com/library/5a9c5ddc-5fd3-457a-9bb6-9abffcd874ec) 循环。|在方法、索引器、属性访问器或事件访问器内。|  
|forr|创建 [for](https://msdn.microsoft.com/library/34041a40-2c87-467a-9ffb-a0417d8f67a8) 循环，每次迭代后会减少循环变量。|在方法、索引器、属性访问器或事件访问器内。|  
|if|创建 [if](https://msdn.microsoft.com/library/d9a1d562-8cf5-4bd4-9ba7-8ad970cd25b2) 块。|在方法、索引器、属性访问器或事件访问器内。|  
|Indexer — 索引器|创建索引器声明。|在类或结构中。|  
|interface|创建[接口](https://msdn.microsoft.com/library/7da38e81-4f99-4bc5-b07d-c986b687eeba)声明。|在命名空间（包括全局命名空间）、类或结构中。|  
|invoke|创建安全调用事件的块。|在方法、索引器、属性访问器或事件访问器内。|  
|iterator|创建迭代器。|在类或结构中。|  
|iterindex|使用嵌套类创建“已命名”迭代器和索引器对。|在类或结构中。|  
|lock|创建 [lock](https://msdn.microsoft.com/library/656da1a4-707e-4ef6-9c6e-6d13b646af42) 块。|在方法、索引器、属性访问器或事件访问器内。|  
|mbox|创建对 <xref:System.Windows.Forms.MessageBox.Show%2A?displayProperty=fullName> 的调用。 可能还需要添加对 System.Windows.Forms.dll 的引用。|在方法、索引器、属性访问器或事件访问器内。|  
|namespace|创建[命名空间](https://msdn.microsoft.com/library/0a788423-9110-42e0-97d9-bda41ca4870f)声明。|在命名空间（包括全局命名空间）中。|  
|prop|创建[自动实现的属性](https://msdn.microsoft.com/library/aa55fa97-ccec-431f-b5e9-5ac789fd32b7)声明。|在类或结构中。|  
|propfull|创建具有 get 和 set 访问器的属性声明。|在类或结构中。|  
|propg|创建一个带有专用“set”访问器的只读[自动实现的属性](https://msdn.microsoft.com/library/aa55fa97-ccec-431f-b5e9-5ac789fd32b7)。|在类或结构中。|  
|sim|创建 [static](https://msdn.microsoft.com/library/5509e215-2183-4da3-bab4-6b7e607a4fdf)[int](https://msdn.microsoft.com/library/212447b4-5d2a-41aa-88ab-84fe710bdb52) Main 方法声明。|在类或结构中。|  
|struct|创建[结构](https://msdn.microsoft.com/library/ff3dd9b7-dc93-4720-8855-ef5558f65c7c)声明。|在命名空间（包括全局命名空间）、类或结构中。|  
|svm|创建 [static](https://msdn.microsoft.com/library/5509e215-2183-4da3-bab4-6b7e607a4fdf)[void](https://msdn.microsoft.com/library/0d2d8a95-fe20-4fbd-bf5d-c1e54bce71d4) Main 方法声明。|在类或结构中。|  
|switch|创建 [switch](https://msdn.microsoft.com/library/44bae8b8-8841-4d85-826b-8a94277daecb) 块。|在方法、索引器、属性访问器或事件访问器内。|  
|try|创建 [try-catch](https://msdn.microsoft.com/library/cb5503c7-bfa1-4610-8fc2-ddcd2e84c438) 块。|在方法、索引器、属性访问器或事件访问器内。|  
|tryf|创建 [try-finally](https://msdn.microsoft.com/library/c27623fb-7261-4464-862c-7a369d3c8f0a) 块。|在方法、索引器、属性访问器或事件访问器内。|  
|unchecked|创建 [unchecked](https://msdn.microsoft.com/library/0c021f7c-923f-4b3d-a58f-55336f5ac27e) 块。|在方法、索引器、属性访问器或事件访问器内。|  
|unsafe|创建 [unsafe](https://msdn.microsoft.com/library/7e818009-1c6e-4b9e-b769-3728a01586a0) 块。|在方法、索引器、属性访问器或事件访问器内。|  
|using|创建 [using](https://msdn.microsoft.com/library/b42b8e61-5e7e-439c-bb71-370094b44ae8) 指令。|在命名空间（包括全局命名空间）中。|  
|while|创建 [while](https://msdn.microsoft.com/library/72a0765c-6852-4aca-b327-4a11cb7f5c59) 循环。|在方法、索引器、属性访问器或事件访问器内。|  
  
## <a name="see-also"></a>请参阅  
 [代码片段函数](../ide/code-snippet-functions.md)   
 [代码片段](../ide/code-snippets.md)   
 [如何：使用替换创建新的代码段](https://msdn.microsoft.com/8d56d43c-097a-475b-aa85-cae1554b6338)   
 [模板参数](../ide/template-parameters.md)   
 [如何：使用外侧代码片段](../ide/how-to-use-surround-with-code-snippets.md)   
 [如何：还原 C# 重构代码段](../ide/how-to-restore-csharp-refactoring-snippets.md)
