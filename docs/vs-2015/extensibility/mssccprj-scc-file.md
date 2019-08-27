---
title: MSSCCPRJ。SCC 文件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, MSSCCPRJ.SCC file
- MSSCCPRJ.SCC file
ms.assetid: 6f2e39d6-b79d-407e-976f-b62a3cedd378
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 705e0fa821000716dc9cd729901fbb7db5fd759c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68194213"
---
# <a name="mssccprjscc-file"></a>MSSCCPRJ.SCC 文件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当 Visual Studio 解决方案或项目使用 IDE 的源控件下放置时，IDE 会从源代码管理插件中字符串的形式接收两个关键信息。 这些字符串，"AuxPath"和"项目名称"，是不透明的 IDE，但它们由该插件以在版本控制中找到解决方案或项目。 IDE 通常获取这些字符串第一次通过调用[SccGetProjPath](../extensibility/sccgetprojpath-function.md)，它然后将其保存在解决方案或项目文件中为未来调用[SccOpenProject](../extensibility/sccopenproject-function.md)。 在解决方案和项目文件中嵌入的"AuxPath"和"项目名称"字符串自动时未更新用户的分支，分叉，或将版本控制中的解决方案和项目文件复制。 若要确保解决方案和项目文件指向其在版本控制中的正确位置，用户必须手动更新这些字符串。 字符串应该是不透明，因为它可能始终无法清除更新方式。  
  
 源代码管理插件可以通过存储在名为 MSSCCPRJ 的特殊文件中的"AuxPath"和"项目名称"字符串来避免此问题。SCC 文件。 它是本地的客户端的文件拥有和维护的插件。 此文件永远不会置于源代码管理下，但生成的每个包含受源代码管理文件的目录的插件。 若要确定哪些文件是 Visual Studio 解决方案和项目文件，源代码管理插件可以将根据标准或用户提供的列表的文件扩展名进行比较。 一旦检测到 IDE，插件支持 MSSCCPRJ。SCC 文件，它将停止将嵌入"AuxPath"和"项目名称"将字符串读入解决方案和项目文件从 MSSCCPRJ 读取这些字符串。SCC 文件相反。  
  
 源代码管理插件支持 MSSCCPRJ。SCC 文件必须遵守以下准则：  
  
- 只能有一个 MSSCCPRJ。SCC 文件，每个目录。  
  
- MSSCCPRJ。SCC 文件可以为给定目录中的源代码管理下的多个文件包含"AuxPath"和"项目名称"。  
  
- "AuxPath"字符串不能在其中的引号。 它允许包含引号作为分隔符 （例如，一对双引号可用来指示空字符串）。 从 MSSCCPRJ 中读取时，IDE 将条带"AuxPath"字符串中的所有引号。SCC 文件。  
  
- MSSCCPRJ 中的"项目名称"字符串。SCC 文件必须从返回的字符串完全匹配`SccGetProjPath`函数。 如果该函数返回的字符串具有引号，MSSCCPRJ 中的字符串。SCC 文件必须包含引号，反之亦然。  
  
- MSSCCPRJ。SCC 文件创建或更新时将文件置于源代码管理下。  
  
- 如果检测到 MSSCCPRJ。获取删除源代码管理文件、 一个提供程序应重新生成该下一次执行源代码管理操作，有关该目录。  
  
- MSSCCPRJ。SCC 文件必须严格遵循定义的格式。  
  
## <a name="an-illustration-of-the-mssccprjscc-file-format"></a>MSSCCPRJ 进行了说明。SCC 文件格式  
 下面是 MSSCCPRJ 的示例。SCC 文件格式 （仅作为指南，提供和不应在文件正文中包含的行号）：  
  
 [第 1 行] `SCC = This is a Source Code Control file`  
  
 [第 2 行]  
  
 [第 3 行] `[TestApp.sln]`  
  
 [第 4 行] `SCC_Aux_Path = "\\server\vss\"`  
  
 [第 5 行] `SCC_Project_Name = "$/TestApp"`  
  
 [第 6 行]  
  
 [第 7 行] `[TestApp.csproj]`  
  
 [第 8 行] `SCC_Aux_Path = "\\server\vss\"`  
  
 [第 9 行] `SCC_Project_Name = "$/TestApp"`  
  
 第一行状态文件的用途，并可作为此类型的所有文件的签名。 此行应显示与所有 MSSCCPRJ 考虑到这完全相同。SCC 文件：  
  
 `SCC = This is a Source Code Control file`  
  
 后面是由方括号中的文件名称标记每个文件的设置的一部分。 对于要跟踪每个文件重复本部分中。 此行是一个示例文件名称，即`[TestApp.csproj]`。 IDE 需要以下两行。 但是，它不定义的样式定义的值。 这些变量就`SCC_Aux_Path`和`SCC_Project_Name`。  
  
 `SCC_Aux_Path = "\\server\vss\"`  
  
 `SCC_Project_Name = "$/TestApp"`  
  
 到本部分中没有结束分隔符。 Scc.h 标头文件中定义的文件，以及在文件中，出现的所有文本名称。 有关详细信息，请参阅[字符串用作键用于查找源代码管理插件](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)。  
  
## <a name="see-also"></a>请参阅  
 [源代码管理插件](../extensibility/source-control-plug-ins.md)   
 [作为用于查找源代码管理插件的密钥的字符串](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)
