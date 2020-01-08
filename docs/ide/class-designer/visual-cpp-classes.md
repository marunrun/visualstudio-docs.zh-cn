---
title: 类设计器中的 C++ 类
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.inheritancelinelabel
helpviewer_keywords:
- Class Designer [Visual Studio], classes
ms.assetid: 75e56f8c-11ef-42a3-b7ec-3d2cf25c581b
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: d68391bbd4c6c873940bbc2714ee41db8309b629
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75590730"
---
# <a name="c-classes-in-class-designer"></a>类设计器中的 C++ 类

类设计器支持 C++ 类，直观显示本机 C++ 类的方式与直观显示 Visual Basic 和 C# 类形状时大致相同，不同之处在于 C++ 类可以有多个继承关系  。 可以展开类形状来显示类中的更多字段和方法，也可以折叠类形状来节省空间。

> [!NOTE]
> 类设计器不支持联合（一种特殊类型的类，仅分配联合的最大数据成员所需的内存量）  。

## <a name="simple-inheritance"></a>简单继承

如果将存在单类继承关系的多个类拖到类图上，它们将会通过箭头相连。 箭头指向基类的方向。 例如，如果类图中有以下类，这两个类将会通过箭头相连，箭头从 B 指向 A：

```cpp
class A {};
class B : A {};
```

也可以只将类 B 拖到类图中，右键单击 B 的类形状，然后单击“显示基类”  。 此操作将显示其基类：答：

## <a name="multiple-inheritance"></a>多重继承

类设计器支持直观显示多类继承关系  。 当派生类有多个基类的特性时，就会用到*多重继承*。 下面的示例展示了多重继承：

```cpp
class Bird {};
class Swimmer {};
class Penguin : public Bird, public Swimmer {};
```

如果将存在多类继承关系的多个类拖到类图上，它们将会通过箭头相连。 箭头指向基类的方向。

右键单击类形状，然后单击“显示基类”  ，可以显示选定类的基类。

> [!NOTE]
> C++ 代码不支持“显示派生类”  命令。 可以转到类视图，依次展开类型节点和“Derived Types”子文件夹，然后将这些类型拖到类图上，即可显示派生类   。

有关多类继承的详细信息，请参阅[多重继承](https://msdn.microsoft.com/library/6td5yws2.aspx)和[多个基类](/cpp/cpp/multiple-base-classes)。

## <a name="abstract-classes"></a>抽象类

类设计器支持抽象类（亦称为“抽象基类”）  。 这些是永不实例化，但可从中派生其他类的类。 以本文前面“多重继承”部分中的示例为例，可以将 `Bird` 类实例化成各个单独的对象，如下所示：

```cpp
int main()
{
   Bird sparrow;
   Bird crow;
   Bird eagle;
}
```

不过，你可能不打算将 `Swimmer` 类实例化成各个单独的对象。 可能只打算从它派生其他类型的动物类，例如，`Penguin`、`Whale` 和 `Fish`。 在这种情况下，需要将 `Swimmer` 类声明为抽象基类。

若要将类声明为抽象类，可以使用 `abstract` 关键字。 标记为 abstract 或抽象类中包含的成员是虚成员，必须由派生自抽象类的类实现。

```cpp
class Swimmer abstract
{
   virtual void swim();
   void dive();
};
```

此外，也可以通过添加至少一个纯虚函数，将类声明为抽象类：

```cpp
class Swimmer
{
   virtual void swim() = 0;
   void dive();
};
```

在类图中显示这些声明时，类名 `Swimmer` 及其纯虚函数 `swim` 会连同标注“抽象类”  一起在抽象类形状中以斜体显示。 请注意，抽象类类型形状与常规类类型形状大致相同，不同之处在于抽象类类型形状的边框是虚线。

派生自抽象基类的类必须替代基类中的每个纯虚函数，否则无法实例化派生类。 比方说，如果 `Fish` 类派生自 `Swimmer` 类，`Fish` 必须替代 `swim` 方法：

```cpp
class Fish : public Swimmer
{
   void swim(int speed);
};

int main()
{
   Fish guppy;
}
```

在类图中显示此代码时，类图会绘制一条从 `Fish` 到 `Swimmer` 的继承线  。

## <a name="anonymous-classes"></a>匿名类

类设计器支持匿名类  。 *匿名类类型*是指未使用标识符声明的类。 匿名类不能有构造函数或析构函数，不能作为自变量传递给函数，也不能作为返回值从函数返回。 匿名类可用于将类名替换为 typedef 名称，如以下示例所示：

```cpp
typedef struct
{
    unsigned x;
    unsigned y;
} POINT;
```

结构也可以是匿名的。 类设计器显示匿名类和结构的方式与显示各自类型的方式相同  。 虽然可以声明并显示匿名类和结构，但类设计器不会使用你指定的标记名称  。 而是使用类视图生成的名称。 类或结构作为 __unnamed 元素显示在类视图和类设计器中   。

有关匿名类的详细信息，请参阅[匿名类类型](/cpp/cpp/anonymous-class-types)。

## <a name="template-classes"></a>模板类

类设计器支持直观显示模板类  。 支持嵌套声明。 下表列出了一些典型声明。

| Code 元素 | 类设计器视图 |
| - | - |
| `template <class T>`<br /><br /> `class A {};` | `A<T>`<br /><br /> 模板类 |
| `template <class T, class U>`<br /><br /> `class A {};` | `A<T, U>`<br /><br /> 模板类 |
| `template <class T, int i>`<br /><br /> `class A {};` | `A<T, i>`<br /><br /> 模板类 |
| `template <class T, template <class K> class U>`<br /><br /> `class A {};` | `A<T, U>`<br /><br /> 模板类 |

下表列出了一些分部专用化示例。

|代码元素|类设计器视图|
|------------------| - |
|`template<class T, class U>`<br /><br /> `class A {};`|`A<T, U>`<br /><br /> 模板类|
|`template<class T>`<br /><br /> `class A<T, T> {};`|`A<T, T>`<br /><br /> 模板类|
|`template <class T>`<br /><br /> `class A<T, int> {};`|`A<T, int>`<br /><br /> 模板类|
|`template <class T1, class T2>`<br /><br /> `class A<T1*, T2*> {};`|`A<T1*, T2*>`<br /><br /> 模板类|

下表列出了一些分部专用化继承示例。

|代码元素|类设计器视图|
|------------------| - |
|`template <class T, class U>`<br /><br /> `class A {};`<br /><br /> `template <class TC>`<br /><br /> `class A<T, int> {};`<br /><br /> `class B : A<int, float>`<br /><br /> `{};`<br /><br /> `class C : A<int, int>`<br /><br /> `{};`|`A<T, U>`<br /><br /> 模板类<br /><br /> `B`<br /><br /> 类<br /><br /> （指向类 A）<br /><br /> `C`<br /><br /> 类<br /><br /> （指向类 A）|

下表列出了一些分部专用化模板函数示例。

|代码元素|类设计器视图|
|------------------| - |
|`class A`<br /><br /> `{`<br /><br /> `template <class T, class U>`<br /><br /> `void func(T a, U b);`<br /><br /> `template <class T>`<br /><br /> `void func(T a, int b);`<br /><br /> `};`|`A`<br /><br /> func\<T, U>（+ 1 重载）|
|`template <class T1>`<br /><br /> `class A {`<br /><br /> `template <class T2>`<br /><br /> `class B {};`<br /><br /> `};`<br /><br /> `template<> template<>`<br /><br /> `class A<type>::B<type> {};`|`A<T1>`<br /><br /> 模板类<br /><br /> `B<T2>`<br /><br /> 模板类<br /><br /> （B 包含在类 A 中的“嵌套类型”  下）|
|`template <class T>`<br /><br /> `class C {};`<br /><br /> `class A : C<int> {};`|`A`<br /><br /> 类<br /><br /> -> C\<int><br /><br /> `C<T>`<br /><br /> 模板类|

下表列出了一些模板继承示例。

|代码元素|类设计器视图|
|------------------| - |
|`template <class T>`<br /><br /> `class C {};`<br /><br /> `template<>`<br /><br /> `class C<int> {`<br /><br /> `class B {};`<br /><br /> `}`<br /><br /> `class A : C<int>::B {};`|`A`<br /><br /> 类<br /><br /> ->B<br /><br /> `C<int>`<br /><br /> 类<br /><br /> （B 包含在类 C 中的“嵌套类型”  下）<br /><br /> `C<T>`<br /><br /> 模板类|

下表列出了一些规范专用化类连接示例。

|代码元素|类设计器视图|
|------------------| - |
|`template <class T>`<br /><br /> `class C {};`<br /><br /> `template<>`<br /><br /> `class C<int> {};`<br /><br /> `class A : C<int> {};`<br /><br /> `class D : C<float> {};`|`A`<br /><br /> 类<br /><br /> ->C\<int><br /><br /> `C<int>`<br /><br /> 类<br /><br /> `C<T>`<br /><br /> 模板类<br /><br /> `D`<br /><br /> 类<br /><br /> ->C\<float>|
|`class B {`<br /><br /> `template <class T>`<br /><br /> `T min (const T &a, const T &b);`<br /><br /> `};`|`B`<br /><br /> min \<T>|

## <a name="see-also"></a>请参阅

- [使用 C++ 代码](working-with-visual-cpp-code.md)
- [类和结构](/cpp/cpp/classes-and-structs-cpp)
- [匿名类类型](/cpp/cpp/anonymous-class-types)
- [多重继承](https://msdn.microsoft.com/library/6td5yws2.aspx)
- [多个基类](/cpp/cpp/multiple-base-classes)
- [模板](/cpp/cpp/templates-cpp)
