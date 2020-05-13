---
title: MSSCCPRJ.SCC 文件 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, MSSCCPRJ.SCC file
- MSSCCPRJ.SCC file
ms.assetid: 6f2e39d6-b79d-407e-976f-b62a3cedd378
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 89511b7c8b69c5793eceef7d58153dde253a4f47
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702469"
---
# <a name="mssccprjscc-file"></a>MSSCCPRJ.SCC 文件
当您使用 IDE 将 Visual Studio 解决方案或项目置于源代码管理之下时，IDE 会收到两个关键信息。 信息来自以字符串形式形式的源代码管理插件。 这些字符串"AuxPath"和"ProjName"对 IDE 不透明，但插件会使用这些字符串在版本控件中查找解决方案或项目。 IDE 通常通过调用[SccGetProjPath](../extensibility/sccgetprojpath-function.md)第一次获取这些字符串，然后将它们保存在解决方案或项目文件中，以便将来调用[SccOpenProject](../extensibility/sccopenproject-function.md)。 嵌入解决方案和项目文件时，"AuxPath"和"ProjName"字符串不会自动更新，当用户分支、分叉或复制版本控制中的解决方案和项目文件时。 为了确保解决方案和项目文件指向其在版本控件中的正确位置，用户必须手动更新字符串。 由于字符串是不透明的，因此并不总是清楚应如何更新它们。

 源代码管理插件可以通过将"AuxPath"和"ProjName"字符串存储在称为*MSSCCPRJ.SCC*文件的特殊文件中来避免此问题。 它是一个本地的客户端文件，由插件拥有和维护。 此文件永远不会置于源代码管理之下，但由包含源代码管理文件的每个目录的插件生成。 要确定哪些文件是 Visual Studio 解决方案和项目文件，源代码管理插件可以将文件扩展名与标准或用户提供的列表进行比较。 一旦 IDE 检测到插件支持*MSSCCPRJ.SCC*文件，它将停止将"AuxPath"和"ProjName"字符串嵌入到解决方案和项目文件中，而是从*MSSCCPRJ.SCC*文件中读取这些字符串。

 支持*MSSCCPRJ.SCC*文件的源代码管理插件必须遵守以下准则：

- 每个目录只能有一个*MSSCCPRJ.SCC*文件。

- *MSSCCPRJ.SCC*文件可以包含给定目录中受源代码管理中的多个文件的"辅助路径"和"ProjName"。

- "辅助路径"字符串内不得有引号。 它允许它周围具有引号作为分隔符（例如，一对双引号可用于指示空字符串）。 从*MSSCCPRJ.SCC*文件读取"辅助路径"字符串时，IDE 将删除其所有引号。

- MSSCCPRJ 中的"ProjName"字符串 *。SCC 文件*必须与从函数返回的`SccGetProjPath`字符串完全匹配。 如果函数返回的字符串周围有引号，*则 MSSCCPRJ.SCC*文件中的字符串必须围绕它具有引号，反之亦然。

- 每当文件置于源代码管理之下时，都会创建或更新*MSSCCPRJ.SCC*文件。

- 如果*MSSCCPRJ.SCC*文件被删除，提供程序应在下次执行有关该目录的源代码管理操作时重新生成该文件。

- *MSSCCPRJ.SCC*文件必须严格遵守定义的格式。

## <a name="an-illustration-of-the-mssccprjscc-file-format"></a>MSSCCPRJ 的插图。SCC 文件格式
 下面是*MSSCCPRJ.SCC*文件格式的示例（行号仅作为指南提供，不应包含在文件正文中）：

- [第1行]`SCC = This is a Source Code Control file`

- [第2行]

- [第3行]`[TestApp.sln]`

- [第4行]`SCC_Aux_Path = "\\server\vss\"`

- [第5行]`SCC_Project_Name = "$/TestApp"`

- [第6行]

- [第7行]`[TestApp.csproj]`

- [第8行]`SCC_Aux_Path = "\\server\vss\"`

- [第9行]`SCC_Project_Name = "$/TestApp"`

 第一行表示文件的用途，并用作此类型所有文件的签名。 此行应在所有*MSSCCPRJ.SCC*文件中完全一样显示：

 `SCC = This is a Source Code Control file`

 以下部分详细介绍了每个文件的设置，这些设置以方括号中的文件名标记。 对于要跟踪的每个文件，将重复此部分。 此行是文件名的示例，`[TestApp.csproj]`即 。 IDE 需要以下两行。 但是，它不定义定义的值的样式。 变量是`SCC_Aux_Path`和`SCC_Project_Name`。

 `SCC_Aux_Path = "\\server\vss\"`

 `SCC_Project_Name = "$/TestApp"`

 此部分没有结束分隔符。 文件的名称以及文件中出现的所有文本都在 scc.h 标头文件中定义。 有关详细信息，请参阅[用作查找源代码管理插件的键的字符串](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)。

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [用作查找源代码管理插件的键](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)
