---
title: Visual C++ 代码片段
ms.date: 11/04/2016
ms.topic: reference
author: corob-msft
ms.author: corob
manager: markl
dev_langs:
- CPP
ms.workload:
- cplusplus
ms.openlocfilehash: db6ea1e233d32872322926a4d75b847ee6a49ba3
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77277827"
---
# <a name="visual-c-code-snippets"></a>Visual C++ 代码片段

在 Visual Studio 中，你可以使用代码片段将常用代码添加到 C++ 代码文件。 一般情况下，可用于使用代码片段的方法与 C# 中的方法大致相同，只是默认的代码片段集不同。

你可以在代码的特定位置添加代码片段（插入）或在所选的代码外侧使用代码片段。

## <a name="insert-a-code-snippet"></a>插入代码片段

若要插入代码片段，请打开一个 C++ 代码文件（.cpp  或 .h  ），单击文件内的某个位置，然后执行以下操作之一：

- 右键单击以获取上下文菜单并选择“插入代码片段” 

- 在“编辑”/“IntelliSense”  菜单中，选择“插入代码片段” 

- 使用热键：CTRL+K+X   

将出现一个以“#if”  开头的选择列表。 选择“#if”  后，显示添加到文件的以下代码：

```cpp
#if 0

#endif // 0
```

然后，可以使用正确的条件替换 0  。

## <a name="use-a-code-snippet-to-surround-selected-code"></a>使用代码片段来包围所选代码

若要使用代码片段来包围所选代码，请选择一行（或多行），然后执行下列操作之一：

- 右键单击以获取上下文菜单并选择“外侧代码” 

- 在“编辑” > “IntelliSense”菜单中，选择“外侧代码”   

- 在键盘上按：Ctrl+K+S   

选择“#if”  。 将显示如下所示的内容：

```cpp
#if 0
#include "pch.h"  // or whatever line you had selected
#endif // 0
```

然后，你可以使用正确的条件替换 0。

## <a name="where-can-i-find-a-complete-list-of-the-c-code-snippets"></a>在哪里可以找到 C++ 代码片段的完整列表？

可以通过以下方式找到 C++ 代码片段的完整列表：转到“代码片段管理器”  （位于“工具”  菜单中），并将“语言”  设置为“Visual C++”  。 在下面的窗口中，展开“Visual C++”  。 将显示所有 C++ 代码片段的名称，按字母顺序排序。

大多数代码片段的名称都具有自我说明性，但某些名称可能令人困惑。

## <a name="class-vs-classi"></a>class 与 classi 代码片段比较

class  代码片段具有名为 `MyClass` 的类的定义，以及相应的默认构造函数和析构函数，其中，构造函数和析构函数的定义位于该类的外部：

```cpp
class MyClass
{
public:
    MyClass();
    ~MyClass();

private:

};

MyClass::MyClass()
{
}

MyClass::~MyClass()
{
}
```

classi 代码片段也提供名为 `MyClass` 的类的定义，但默认构造函数和析构函数在类定义的内部进行定义  ：

```cpp
class MyClass
{
public:
    MyClass()
    {
    }

    ~MyClass()
    {
    }

private:

};
```

## <a name="for-vs-forr-vs-rfor"></a>for、forr 与 rfor 比较

有三个不同的 for 代码片段，可提供不同种类的 `for` 循环  。

rfor 代码片段具有[基于范围](/cpp/cpp/range-based-for-statement-cpp)的 for 循环（链接）  。 该构造优于基于索引的 `for` 循环。

```cpp
for (auto& i : v)
{

}
```

for 代码片段具有 `for` 循环，此循环中的条件以对象的长度 (`size_t`) 为依据  。

```cpp
for (size_t i = 0; i < length; i++)
{

}
```

forr 代码片段具有反向 `for` 循环，此循环中的条件以对象的长度（整数）为依据  。

```cpp
for (int i = length - 1; i >= 0; i--)
{

}
```

## <a name="the-destructor-snippet-"></a>析构函数代码片段 (~)

析构函数代码片段 ( **~** ) 在不同上下文中显示不同的行为。 如果在类中插入此代码片段，则它将为该类提供一个析构函数。 例如，给定以下代码：

```cpp
class SomeClass {

};
```

如果插入析构函数代码片段，则将为 `SomeClass` 提供析构函数：

```cpp
class SomeClass {
    ~SomeClass()
    {

    }
};
```

如果尝试在类外部插入析构函数代码片段，则会提供一个具有占位符名称的析构函数：

```cpp
~TypeNamePlaceholder()
{
```

## <a name="see-also"></a>请参阅

- [代码片段](../ide/code-snippets.md)