---
title: 演练：分析 C + + 代码的缺陷 |Microsoft Docs
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
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: c822dbcc6a1ece2040da22a3442dd584c3926d97
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "77272433"
---
# <a name="walkthrough-analyzing-cc-code-for-defects"></a>演练：对 C/C++ 代码进行缺陷分析
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本演练演示如何使用适用于 C/c + + 代码的代码分析工具分析 C/c + + 代码是否存在可能的代码缺陷。  
  
 在本演练中，您将逐步完成使用代码分析来分析 C/c + + 代码是否存在可能的代码缺陷的过程。  
  
 您将完成下列步骤：  
  
- 在本机代码上运行代码分析。  
  
- 分析代码缺陷警告。  
  
- 将警告视为错误。  
  
- 批注源代码以改进代码缺陷分析。  
  
## <a name="prerequisites"></a>先决条件  
  
- [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)] 或 [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)]。  
  
- [演示示例](../code-quality/demo-sample.md)的副本。  
  
- 基本了解 C/c + +。  
  
### <a name="to-run-code-defect-analysis-on-native-code"></a>在本机代码上运行代码缺陷分析  
  
1. 在中打开演示解决方案 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。  
  
     演示解决方案现在将填充 **解决方案资源管理器**。  
  
2. 在“生成”菜单上，单击“重新生成解决方案” 。  
  
     解决方案生成时不会出现任何错误或警告。  
  
3. 在 **解决方案资源管理器**中，选择 CodeDefects 项目。  
  
4. 在 **“项目”** 菜单上，单击 **“属性”** 。  
  
     随即显示 " **CodeDefects 属性页** " 对话框。  
  
5. 单击“代码分析”。  
  
6. 单击 " **生成时启用 c/c + + 代码分析** " 复选框。  
  
7. 重新生成 CodeDefects 项目。  
  
     代码分析警告显示在 **错误列表**中。  
  
### <a name="to-analyze-code-defect-warnings"></a>分析代码缺陷警告  
  
1. 在 **“视图”** 菜单上单击 **“错误列表”** 。  
  
     根据在中选择的开发人员配置文件 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ，可能需要指向 "**视图**" 菜单上的 "**其他窗口**"，然后单击 "**错误列表**"。  
  
2. 在 **错误列表**中，双击以下警告：  
  
     警告 C6230：语义不同类型之间的隐式强制转换：在 Boolean 上下文中使用 HRESULT。  
  
     代码编辑器显示导致函数中出现警告的行 `bool``ProcessDomain()` 。 此警告意味着在需要布尔值结果的 "if" 语句中使用 HRESULT。  
  
3. 使用 SUCCEEDED 宏更正此警告。 你的代码应与以下代码类似：  
  
    ```  
    if (SUCCEEDED (ReadUserAccount()) )  
    ```  
  
4. 在 **错误列表**中，双击以下警告：  
  
     警告 C6282：运算符不正确：在测试上下文中对常量赋值。 Was = = 预期？  
  
5. 通过测试相等性来更正此警告。 你的代码应类似于以下代码：  
  
    ```  
    if ((len == ACCOUNT_DOMAIN_LEN) || (g_userAccount[len] != '\\'))  
    ```  
  
### <a name="to-treat-warning-as-an-error"></a>将警告视为错误  
  
1. 在 Bug .cpp 文件中，将以下语句添加 `#pragma` 到文件的开头，以将警告 C6001 视为错误：  
  
    ```  
    #pragma warning (error: 6001)  
    ```  
  
2. 重新生成 CodeDefects 项目。  
  
     在 **错误列表**中，C6001 现在显示为 "错误"。  
  
3. 在 **错误列表** 中，通过 `i` 将和初始化为0来更正其余两个 C6001 错误 `j` 。  
  
4. 重新生成 CodeDefects 项目。  
  
     项目生成时不会出现任何警告或错误。  
  
### <a name="to-correct-the-source-code-annotation-warnings-in-annotationc"></a>更正 annotation 中的源代码批注警告  
  
1. 在解决方案资源管理器中，选择 "批注" 项目。  
  
2. 在 **“项目”** 菜单上，单击 **“属性”** 。  
  
     将显示 " **批注属性页** " 对话框。  
  
3. 单击“代码分析”。  
  
4. 选中 " **生成时启用 c/c + + 代码分析"** 复选框。  
  
5. 重新生成批注项目。  
  
6. 在 **错误列表**中，双击以下警告：  
  
     警告 C6011：取消对 NULL 指针 "newNode" 的引用。  
  
     此警告指示调用方检查返回值失败。 在这种情况下，对 **AllocateNode** 的调用可能会返回 NULL 值 (请参阅 AllocateNode) 的函数声明的标头文件。  
  
7. 打开批注 .cpp 文件。  
  
8. 若要更正此警告，请使用 "if" 语句测试返回值。 你的代码应与以下代码类似：  
  
     `if (NULL != newNode)`  
  
     `{`  
  
     `newNode->data = value;`  
  
     `newNode->next = 0;`  
  
     `node->next = newNode;`  
  
     `}`  
  
9. 重新生成批注项目。  
  
     项目生成时不会出现任何警告或错误。  
  
### <a name="to-use-source-code-annotation"></a>使用源代码批注  
  
1. 使用 Pre 和 Post 条件注释函数的形参和返回值， `AddTail` 如本示例所示：  
  
     `[returnvalue:SA_Post (Null=SA_Maybe)] LinkedList* AddTail`  
  
     `(`  
  
     `[SA_Pre(Null=SA_Maybe)] LinkedList* node,`  
  
     `int value`  
  
     `)`  
  
2. 重新生成注释项目。  
  
3. 在 **错误列表**中，双击以下警告：  
  
     警告 C6011：取消引用 NULL 指针 "node"。  
  
     此警告表明传递到函数的节点可能为 null，并指示引发警告的行号。  
  
4. 若要更正此警告，请使用 "if" 语句测试返回值。 你的代码应与以下代码类似：  
  
    ```  
    . . .  
    LinkedList *newNode = NULL;   
    if (NULL == node)  
    {  
         return NULL;  
        . . .  
    }  
    ```  
  
5. 重新生成注释项目。  
  
     项目生成时不会出现任何警告或错误。  
  
## <a name="see-also"></a>另请参阅  
 [演练：对托管代码进行代码缺陷分析](../code-quality/walkthrough-analyzing-managed-code-for-code-defects.md)
