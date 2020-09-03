---
title: MSSCCPRJ.SCC.SCC 文件 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194213"
---
# <a name="mssccprjscc-file"></a>MSSCCPRJ.SCC 文件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当使用 IDE 在源代码管理下放置 Visual Studio 解决方案或项目时，IDE 将以字符串的形式从源代码管理插件接收两个关键部分的信息。 这些字符串 "AuxPath" 和 "ProjName" 在 IDE 中是不透明的，但插件使用它们来查找版本控制中的解决方案或项目。 IDE 通常通过调用 [SccGetProjPath](../extensibility/sccgetprojpath-function.md)获取这些字符串，然后将它们保存在解决方案或项目文件中，以便以后调用 [SccOpenProject](../extensibility/sccopenproject-function.md)。 在解决方案和项目文件中嵌入时，当用户分支、分叉或复制版本控制中的解决方案和项目文件时，不会自动更新 "AuxPath" 和 "ProjName" 字符串。 为了确保解决方案和项目文件指向其版本控制中的正确位置，用户必须手动更新这些字符串。 因为字符串应是不透明的，所以可能并不总是清楚地说明如何更新它们。  
  
 源代码管理插件可以通过将 "AuxPath" 和 "ProjName" 字符串存储在名为 MSSCCPRJ.SCC 的特殊文件中来避免此问题。SCC 文件。 它是插件拥有和维护的本地客户端文件。 此文件从不置于源代码管理下，而是由包含受源代码管理的文件的每个目录的插件生成的。 为了确定哪些文件是 Visual Studio 解决方案和项目文件，源代码管理插件可以将文件扩展名与标准或用户提供的列表进行比较。 IDE 检测到插件支持 MSSCCPRJ.SCC。SCC 文件，它将停止将 "AuxPath" 和 "ProjName" 字符串嵌入到解决方案和项目文件中，并从 MSSCCPRJ.SCC 读取这些字符串。请改用 SCC 文件。  
  
 支持 MSSCCPRJ.SCC 的源代码管理插件。SCC 文件必须遵循以下准则：  
  
- 只能有一个 MSSCCPRJ.SCC。每个目录的 SCC 文件。  
  
- 一个 MSSCCPRJ.SCC。SCC 文件可包含给定目录内受源代码管理的多个文件的 "AuxPath" 和 "ProjName"。  
  
- "AuxPath" 字符串内不能有引号。 允许使用引号作为分隔符 (例如，一对双引号可用于表示) 的空字符串。 从 MSSCCPRJ.SCC 读取 "AuxPath" 字符串时，IDE 将从该字符串中去除所有引号。SCC 文件。  
  
- MSSCCPRJ.SCC 中的 "ProjName" 字符串。SCC 文件必须与从函数返回的字符串完全匹配 `SccGetProjPath` 。 如果函数返回的字符串具有引号，则为 MSSCCPRJ.SCC 中的字符串。SCC 文件必须具有引号，反之亦然。  
  
- 一个 MSSCCPRJ.SCC。每当文件置于源代码管理下时，就会创建或更新 SCC 文件。  
  
- 如果 MSSCCPRJ.SCC，则为。SCC 文件被删除，提供程序应在下一次执行有关该目录的源代码管理操作时重新生成它。  
  
- 一个 MSSCCPRJ.SCC。SCC 文件必须严格遵循定义的格式。  
  
## <a name="an-illustration-of-the-mssccprjscc-file-format"></a>MSSCCPRJ.SCC 的插图。SCC 文件格式  
 下面是 MSSCCPRJ.SCC 的一个示例。SCC 文件格式 (行号仅作为指南提供，不应包含在文件正文中) ：  
  
 [第1行] `SCC = This is a Source Code Control file`  
  
 [第2行]  
  
 [第3行] `[TestApp.sln]`  
  
 [第4行] `SCC_Aux_Path = "\\server\vss\"`  
  
 [第5行] `SCC_Project_Name = "$/TestApp"`  
  
 [第6行]  
  
 [第7行] `[TestApp.csproj]`  
  
 [第8行] `SCC_Aux_Path = "\\server\vss\"`  
  
 [第9行] `SCC_Project_Name = "$/TestApp"`  
  
 第一行指出了文件的用途，并用作此类型的所有文件的签名。 在所有 MSSCCPRJ.SCC 中，该行应与此完全相同。SCC 文件：  
  
 `SCC = This is a Source Code Control file`  
  
 下面是每个文件的设置部分，由方括号括起来。 此部分对于正在跟踪的每个文件都是重复的。 此行是文件名的示例，即 `[TestApp.csproj]` 。 IDE 需要以下两行。 但是，它不定义定义的值的样式。 变量为 `SCC_Aux_Path` 和 `SCC_Project_Name` 。  
  
 `SCC_Aux_Path = "\\server\vss\"`  
  
 `SCC_Project_Name = "$/TestApp"`  
  
 此部分没有结束分隔符。 文件的名称以及出现在文件中的所有文本都在 scc 标头文件中定义。 有关详细信息，请参阅 [用于查找源代码管理插件的键的字符串](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)。  
  
## <a name="see-also"></a>另请参阅  
 [源代码管理插件](../extensibility/source-control-plug-ins.md)   
 [作为用于查找源代码管理插件的密钥的字符串](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)
