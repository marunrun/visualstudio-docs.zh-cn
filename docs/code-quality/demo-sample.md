---
title: 用于代码分析的示例 C++ 项目
ms.date: 11/04/2016
ms.topic: sample
helpviewer_keywords:
- demo sample [Visual Studio ALM]
- code analysis, samples
ms.assetid: 09e1b9f7-5916-4ed6-a001-5c2d7e710682
author: mikeblome
ms.author: mblome
manager: markl
ms.workload:
- multiple
ms.openlocfilehash: 84f6ddc2012617a5216c58fa0761dc100fb8942f
ms.sourcegitcommit: 8e123bcb21279f2770b28696995450270b4ec0e9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75402746"
---
# <a name="sample-c-project-for-code-analysis"></a>用于代码分析的示例 C++ 项目

以下过程说明如何为[演练：分析 C/C++ 代码的缺陷](../code-quality/walkthrough-analyzing-c-cpp-code-for-defects.md)创建示例。 这些过程将创建：

- 名为 CppDemo 的 [!INCLUDEvsprvs] 解决方案。

- 名为 CodeDefects 的静态库项目。

- 名为 Annotations 的静态库项目。

这些过程还提供了标头代码以及静态库的 .cpp 文件  。

## <a name="create-the-cppdemo-solution-and-the-codedefects-project"></a>创建 CppDemo 解决方案和 CodeDefects 项目

1. 打开 [!INCLUDEvsprvs] 并选择“创建新项目” 

2. 将语言筛选器更改为 C++ 

3. 选择空项目，然后单击“下一步”  

4. 在“项目名称”文本框中，键入“CodeDefects”  

5. 在“解决方案名称”文本框中，键入“CppDemo”  

6. 单击“创建” 

## <a name="configure-the-codedefects-project-as-a-static-library"></a>将 CodeDefects 项目配置为静态库

1. 在“解决方案资源管理器”中右键单击 CodeDefects，再单击“属性”   。

2. 展开“配置属性”，然后单击“常规”   。

3. 在“常规”列表中，将“配置类型”更改为“静态库(.lib)”    。

4. 在“高级”列表中，将“目标文件扩展名”更改为“.lib”   

## <a name="add-the-header-and-source-file-to-the-codedefects-project"></a>将标头和源文件添加到 CodeDefects 项目

1. 在解决方案资源管理器中，展开 CodeDefects，右键单击“头文件”，单击“添加”，然后单击“新项”     。

2. 在“添加新项”对话框中，单击“代码”，然后单击“头文件(.h)”    。

3. 在“名称”框中，键入“Bug.h”，然后单击“添加”    。

4. 复制以下代码并将其粘贴到编辑器中的“Bug.h”文件中  。

```cpp
#pragma once

#include <windows.h>

// These functions are consumed by the sample
// but are not defined. This project cannot be linked!
bool CheckDomain(LPCTSTR);
HRESULT ReadUserAccount();

// These constants define the common sizes of the
// user account information throughout the program
const int USER_ACCOUNT_LEN = 256;
const int ACCOUNT_DOMAIN_LEN = 128;
```

5. 在解决方案资源管理器中，右键单击“源文件”，指向“新建”，然后单击“新项”    。

6. 在“添加新项”对话框中，单击“C++ 文件(.cpp)”  

7. 在“名称”框中，键入“Bug.cpp”，然后单击“添加”    。

8. 复制以下代码并将其粘贴到编辑器中的“Bug.cpp”文件中  。

```cpp
#include "Bug.h"

// the user account
TCHAR g_userAccount[USER_ACCOUNT_LEN] = {};
int len = 0;

bool ProcessDomain()
{
    TCHAR* domain = new TCHAR[ACCOUNT_DOMAIN_LEN];
    // ReadUserAccount gets a 'domain\user' input from
    //the user into the global 'g_userAccount'
    if (ReadUserAccount())
    {
        // Copies part of the string prior to the '\'
        // character onto the 'domain' buffer
        for (len = 0; (len < ACCOUNT_DOMAIN_LEN) && (g_userAccount[len] != L'\0'); len++)
        {
            if (g_userAccount[len] == '\\')
            {
                // Stops copying on the domain and user separator ('\')
                break;
            }
            domain[len] = g_userAccount[len];
        }
        if ((len = ACCOUNT_DOMAIN_LEN) || (g_userAccount[len] != '\\'))
        {
            // '\' was not found. Invalid domain\user string.
            delete[] domain;
            return false;
        }
        else
        {
            domain[len] = '\0';
        }
        // Process domain string
        bool result = CheckDomain(domain);

        delete[] domain;
        return result;
    }
    return false;
}

int path_dependent(int n)
{
    int i;
    int j;
    if (n == 0)
        i = 1;
    else
        j = 1;
    return i + j;
}
```

9. 单击“文件”菜单，然后单击“全部保存”   。

## <a name="add-the-annotations-project-and-configure-it-as-a-static-library"></a>添加 Annotations 项目并将其配置为静态库

1. 在解决方案资源管理器中，单击“CppDemo”，指向“添加”，然后单击“新项目”    。

2. 在“添加新项目”对话框中，将语言筛选器更改为“C++”并选择“空项目”，然后单击“下一步”     。

3. 在“项目名称”文本框中，键入“Annotations”，然后单击“创建”    。

4. 在解决方案资源管理器中，右键单击“Annotations”，然后单击“属性”   。

5. 展开“配置属性”，然后单击“常规”   。

6. 在“常规”列表中，将“配置类型”更改为“静态库(.lib)”，然后单击“静态库(.lib)”    。

7. 在“高级”列表中，选择“目标文件扩展名”旁边的列中的文本，然后键入“.lib”    。


## <a name="add-the-header-file-and-source-file-to-the-annotations-project"></a>将头文件和源文件添加到 Annotations 项目

1. 在解决方案资源管理器中，展开“Annotations”，右键单击“头文件”，单击“添加”，然后单击“新项”     。

2. 在“添加新项”对话框中，单击“头文件(.h)”   。

3. 在“名称”框中，键入“annotations.h”，然后单击“添加”    。

4. 复制以下代码并将其粘贴到编辑器中的“annotations.h”文件中  。

```cpp
#pragma once
#include <sal.h>

struct LinkedList
{
    struct LinkedList* next;
    int data;
};

typedef struct LinkedList LinkedList;

_Ret_maybenull_ LinkedList* AllocateNode();
```

5. 在解决方案资源管理器中，右键单击“源文件”，指向“新建”，然后单击“新项”    。

6. 在“添加新项”对话框中，单击“代码”，然后单击“C++文件(.cpp)”   

7. 在“名称”框中，键入“annotations.cpp”，然后单击“添加”    。

8. 复制以下代码并将其粘贴到编辑器中的“annotations.cpp”文件中  。

```cpp
#include "annotations.h"

LinkedList* AddTail(LinkedList* node, int value)
{
    // finds the last node
    while (node->next != nullptr)
    {
        node = node->next;
    }

    // appends the new node
    LinkedList* newNode = AllocateNode();
    newNode->data = value;
    newNode->next = 0;
    node->next = newNode;

    return newNode;
}
```

9. 单击“文件”菜单，然后单击“全部保存”   。


解决方案现已完成，应顺利生成，没有错误。
