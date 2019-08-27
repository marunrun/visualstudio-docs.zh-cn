---
title: 演练：分析 C-C++代码进行缺陷 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- C/C++, code analysis
- code analysis, walkthroughs
- code, analyzing C/C++
- code analysis tool, walkthroughs
ms.assetid: eaee55b8-85fe-47c7-a489-9be0c46ae8af
caps.latest.revision: 37
author: mikeblome
ms.author: mblome
manager: jillfra
ms.openlocfilehash: dcd862b6ff9c94b8de3fc8b5a56164549fefe8ca
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68142039"
---
# <a name="walkthrough-analyzing-cc-code-for-defects"></a>演练：分析 C/C++ 代码的缺陷
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本演练演示如何分析 C /C++通过代码分析工具用于 C 的潜在代码的代码缺陷 /C++代码。  
  
 在本演练中，您逐步完成使用代码分析来分析你 C 的过程 /C++代码以查找潜在的代码缺陷。  
  
 您将完成以下步骤：  
  
- 对本机代码中运行代码分析。  
  
- 分析代码缺陷警告。  
  
- 将警告视为错误。  
  
- 批注源代码，以改进代码缺陷分析。  
  
## <a name="prerequisites"></a>先决条件  
  
- [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)] 或 [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)]。  
  
- 一份[演示示例](../code-quality/demo-sample.md)。  
  
- 基本了解 C /C++。  
  
### <a name="to-run-code-defect-analysis-on-native-code"></a>若要对本机代码运行的代码缺陷分析  
  
1. 打开中的演示解决方案[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。  
  
     演示解决方案现在将出现**解决方案资源管理器**。  
  
2. 在“生成”菜单上，单击“重新生成解决方案”   。  
  
     该解决方案版本，无任何错误或警告。  
  
3. 在中**解决方案资源管理器**，选择 CodeDefects 项目。  
  
4. 在“项目”菜单上，单击“属性”   。  
  
     **CodeDefects 属性页**显示对话框。  
  
5. 单击**代码分析**。  
  
6. 单击**于 c 语言时启用代码分析 /C++上生成**复选框。  
  
7. 重新生成 CodeDefects 项目。  
  
     代码分析警告显示在**错误列表**。  
  
### <a name="to-analyze-code-defect-warnings"></a>若要分析的代码缺陷警告  
  
1. 上**视图**菜单上，单击**错误列表**。  
  
     具体取决于您在中选择的开发人员配置文件[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，可能需要指向**其他 Windows**上**视图**菜单，并单击**错误列表**。  
  
2. 在中**错误列表**，双击以下警告：  
  
     警告 C6230:语义不同类型之间的隐式强制转换： 在 Boolean 上下文中使用 HRESULT。  
  
     代码编辑器中显示导致警告函数中的行`bool``ProcessDomain()`。 此警告表示 HRESULT 正在使用在 if 语句中布尔值结果的地方。  
  
3. 通过使用 SUCCEEDED 宏来更正此警告。 你的代码应类似于以下代码：  
  
    ```  
    if (SUCCEEDED (ReadUserAccount()) )  
    ```  
  
4. 在中**错误列表**，双击以下警告：  
  
     警告 C6282:运算符不正确： 分配到测试上下文中的常量。 已 = = 预期？  
  
5. 通过测试的相等性来更正此警告。 你的代码应类似于下面的代码：  
  
    ```  
    if ((len == ACCOUNT_DOMAIN_LEN) || (g_userAccount[len] != '\\'))  
    ```  
  
### <a name="to-treat-warning-as-an-error"></a>若要将警告视为错误  
  
1. 在 Bug.cpp 文件中，添加以下`#pragma`要警告 C6001 视为错误的文件的开头的语句：  
  
    ```  
    #pragma warning (error: 6001)  
    ```  
  
2. 重新生成 CodeDefects 项目。  
  
     在中**错误列表**，C6001 现在显示为一个错误。  
  
3. 更正中的其余两个 C6001 错误**错误列表**通过初始化`i`和`j`为 0。  
  
4. 重新生成 CodeDefects 项目。  
  
     项目版本，无任何警告或错误。  
  
### <a name="to-correct-the-source-code-annotation-warnings-in-annotationc"></a>若要更正 annotation.c 中的源的代码批注警告  
  
1. 在解决方案资源管理器，选择注释项目。  
  
2. 在“项目”菜单上，单击“属性”   。  
  
     **批注属性页**显示对话框。  
  
3. 单击**代码分析**。  
  
4. 选择**于 c 语言时启用代码分析 /C++上生成**复选框。  
  
5. 重新生成批注项目。  
  
6. 在中**错误列表**，双击以下警告：  
  
     警告 C6011:取消引用 NULL 指针 newNode。  
  
     此警告意味着调用方未能检查返回值。 在这种情况下，调用**AllocateNode**可能返回 NULL 值 （请参阅 AllocateNode 的函数声明的 annotations.h 标头文件）。  
  
7. 打开 annotations.cpp 文件。  
  
8. 若要更正此警告，请使用 if 语句来测试返回的值。 你的代码应类似于以下代码：  
  
     `if (NULL != newNode)`  
  
     `{`  
  
     `newNode->data = value;`  
  
     `newNode->next = 0;`  
  
     `node->next = newNode;`  
  
     `}`  
  
9. 重新生成批注项目。  
  
     项目版本，无任何警告或错误。  
  
### <a name="to-use-source-code-annotation"></a>若要使用源代码批注  
  
1. 批注形式参数和返回值的函数的`AddTail`使用 Pre 和 Post 条件，在此示例中所示：  
  
     `[returnvalue:SA_Post (Null=SA_Maybe)] LinkedList* AddTail`  
  
     `(`  
  
     `[SA_Pre(Null=SA_Maybe)] LinkedList* node,`  
  
     `int value`  
  
     `)`  
  
2. 重新生成批注项目。  
  
3. 在中**错误列表**，双击以下警告：  
  
     警告 C6011:取消引用 NULL 指针 node。  
  
     此警告指示传递到函数的节点可能为 null，并指示产生该警告的行号。  
  
4. 若要更正此警告，请使用 if 语句来测试返回的值。 你的代码应类似于以下代码：  
  
    ```  
    . . .  
    LinkedList *newNode = NULL;   
    if (NULL == node)  
    {  
         return NULL;  
        . . .  
    }  
    ```  
  
5. 重新生成批注项目。  
  
     项目版本，无任何警告或错误。  
  
## <a name="see-also"></a>请参阅  
 [演练：分析托管代码的代码缺陷](../code-quality/walkthrough-analyzing-managed-code-for-code-defects.md)
