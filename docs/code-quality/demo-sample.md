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
ms.openlocfilehash: 071c16267486e1dda1e183cad3c488345974a3cc
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745926"
---
# <a name="sample-c-project-for-code-analysis"></a>用于代码分析的示例 C++ 项目

以下过程说明如何为[演练：分析 C/C++ 代码的缺陷](../code-quality/walkthrough-analyzing-c-cpp-code-for-defects.md)创建示例。 这些过程将创建：

- 名为 CppDemo 的 Visual Studio 解决方案。

- 名为 CodeDefects 的静态库项目。

- 名为 Annotations 的静态库项目。

这些过程还提供了标头代码以及静态库的 .cpp 文件  。

## <a name="create-the-cppdemo-solution-and-the-codedefects-project"></a>创建 CppDemo 解决方案和 CodeDefects 项目

1. 单击“文件”菜单，指向“新建”，然后单击“新建项目”    。

2. 在“项目类型”树列表中，如果 C++ 不是 VS 中的默认语言，则展开“其他语言”   。

3. 展开“Visual C++”，然后单击“常规”   。

4. 在“模板”中单击“空项目”   。

5. 在“名称”文本框中，键入“CodeDefects”   。

6. 选择“为解决方案创建目录”复选框  。

7. 在“解决方案名称”文本框中，键入“CppDemo”   。

## <a name="configure-the-codedefects-project-as-a-static-library"></a>将 CodeDefects 项目配置为静态库

1. 在“解决方案资源管理器”中右键单击 CodeDefects，再单击“属性”   。

2. 展开“配置属性”，然后单击“常规”   。

3. 在“常规”列表中，选择“目标扩展”旁边的列中的文本，然后键入“.lib”    。

4. 在“项目默认值”中，单击“配置类型”旁边的列，然后单击“静态库(.lib)”    。

## <a name="add-the-header-and-source-file-to-the-codedefects-project"></a>将标头和源文件添加到 CodeDefects 项目

1. 在解决方案资源管理器中，展开 CodeDefects，右键单击“头文件”，单击“添加”，然后单击“新项”     。

2. 在“添加新项”对话框中，单击“代码”，然后单击“头文件(.h)”    。

3. 在“名称”框中，键入“Bug.h”，然后单击“添加”    。

4. 复制以下代码并将其粘贴到 Visual Studio 编辑器中的“Bug.h”文件中  。

    ```cpp
    #include <windows.h>

    //
    //These 3 functions are consumed by the sample
    //  but are not defined. This project cannot be linked!
    //

    bool CheckDomain( LPCSTR );
    HRESULT ReadUserAccount();

    //
    //These constants define the common sizes of the
    //  user account information throughout the program
    //

    const int USER_ACCOUNT_LEN = 256;
    const int ACCOUNT_DOMAIN_LEN = 128;
    ```

5. 在解决方案资源管理器中，右键单击“源文件”，指向“新建”，然后单击“新项”    。

6. 在“添加新项”对话框中，单击“C++ 文件(.cpp)”  

7. 在“名称”框中，键入“Bug.cpp”，然后单击“添加”    。

8. 复制以下代码并将其粘贴到 Visual Studio 编辑器中的 Bug.cpp 文件中  。

    ```cpp
    #include <stdlib.h>
    #include "Bug.h"

    // the user account
    TCHAR g_userAccount[USER_ACCOUNT_LEN] = "";
    int len = 0;

    bool ProcessDomain()
    {
        TCHAR* domain = new TCHAR[ACCOUNT_DOMAIN_LEN];
        // ReadUserAccount gets a 'domain\user' input from
        //the user into the global 'g_userAccount'
        if (ReadUserAccount() )
        {

            // Copies part of the string prior to the '\'
            // character onto the 'domain' buffer
            for( len = 0 ; (len < ACCOUNT_DOMAIN_LEN) && (g_userAccount[len] != '\0') ; len++  )
            {
                if ( g_userAccount[len] == '\\' )
                {
                    // Stops copying on the domain and user separator ('\')
                    break;
                }
                domain[len] = g_userAccount[len];
            }
            if((len= ACCOUNT_DOMAIN_LEN) || (g_userAccount[len] != '\\'))
            {
                // '\' was not found. Invalid domain\user string.
                delete [] domain;
                return false;
            }
            else
            {
                domain[len]='\0';
            }
            // Process domain string
            bool result = CheckDomain( domain );

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
        return i+j;
    }
    ```

9. 单击“文件”菜单，然后单击“全部保存”   。

## <a name="add-the-annotations-project-and-configure-it-as-a-static-library"></a>添加 Annotations 项目并将其配置为静态库

1. 在解决方案资源管理器中，单击“CppDemo”，指向“添加”，然后单击“新项目”    。

2. 在“添加新项目”对话框中，展开 Visual C++，单击“常规”，然后单击“空项目”    。

3. 在“名称”文本框中，键入“Annotations”，然后单击“添加”    。

4. 在解决方案资源管理器中，右键单击“Annotations”，然后单击“属性”   。

5. 展开“配置属性”，然后单击“常规”   。

6. 在“常规”列表中，选择“目标扩展”旁边的列中的文本，然后键入“.lib”    。

7. 在“项目默认值”中，单击“配置类型”旁边的列，然后单击“静态库(.lib)”    。

## <a name="add-the-header-file-and-source-file-to-the-annotations-project"></a>将头文件和源文件添加到 Annotations 项目

1. 在解决方案资源管理器中，展开“Annotations”，右键单击“头文件”，单击“添加”，然后单击“新项”     。

2. 在“添加新项”对话框中，单击“头文件(.h)”   。

3. 在“名称”框中，键入“annotations.h”，然后单击“添加”    。

4. 复制以下代码并将其粘贴到 Visual Studio 编辑器中的“annotations.h”文件中  。

    ```cpp
    #include <CodeAnalysis/SourceAnnotations.h>

    struct LinkedList
    {
        struct LinkedList* next;
        int data;
    };

    typedef struct LinkedList LinkedList;

    [returnvalue:SA_Post( Null=SA_Maybe )] LinkedList* AllocateNode();

    ```

5. 在解决方案资源管理器中，右键单击“源文件”，指向“新建”，然后单击“新项”    。

6. 在“添加新项”对话框中，单击“代码”，然后单击“C++文件(.cpp)”   

7. 在“名称”框中，键入“annotations.cpp”，然后单击“添加”    。

8. 复制以下代码并将其粘贴到 Visual Studio 编辑器中的“annotations.cpp”文件中  。

    ```cpp
    #include <CodeAnalysis/SourceAnnotations.h>
    #include <windows.h>
    #include <stdlib.h>
    #include "annotations.h"

    LinkedList* AddTail( LinkedList *node, int value )
    {
        LinkedList *newNode = NULL;

        // finds the last node
        while ( node->next != NULL )
        {
            node = node->next;
        }

        // appends the new node
        newNode = AllocateNode();
        newNode->data = value;
        newNode->next = 0;
        node->next = newNode;

        return newNode;
    }

    ```

9. 单击“文件”菜单，然后单击“全部保存”   。
