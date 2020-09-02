---
title: 使用 DebuggerDisplay 属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- attributes [C#], debugger
- DebuggerDisplay attribute
- DebuggerDisplayAttribute class
ms.assetid: f4eb7c76-af4e-493b-9ab6-9cb05949d9b3
caps.latest.revision: 50
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: aba6feb17a4e7bd4cabfe40bd45480a0f7a9f552
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65683928"
---
# <a name="using-the-debuggerdisplay-attribute"></a>使用 DebuggerDisplay 特性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

<xref:System.Diagnostics.DebuggerDisplayAttribute> 控制对象、属性或字段在调试器变量窗口中的显示方式。 此特性可应用于类型、委托、属性、字段和程序集。  
  
 `DebuggerDisplay` 特性有一个参数，此参数是要在值列中为类型的实例显示的字符串。 此字符串可以包含大括号（`{` 和 `}`）。 一对大括号之间的文本将作为字段、属性或方法进行计算。  
  
 如果一个类中有重写的 `ToString()` 方法，调试器将使用该重写的方法而非默认 `{<typeName>}`。 因此，如果你已重写 `ToString()` 方法，调试器将使用重写的方法而非默认`{<typeName>}`，你无需使用 `DebuggerDisplay`。 在同时使用这两者时， `DebuggerDisplay` 特性将优先于 `ToString()` 方法。  
  
 调试器是否计算此隐式 `ToString()` 调用取决于“工具”/“选项”/“调试”  对话框中的用户设置。 Visual Basic 不实现此隐式 `ToString()` 计算。  
  
> [!IMPORTANT]
> 如果在“工具”/“选项”/“调试”  对话框中选中了“在变量窗口中显示对象的原始结构”  复选框，则将忽略 `DebuggerDisplay` 特性。  
  
 下表显示 `DebuggerDisplay` 特性的一些可能用法和示例输出。  
  
|特性|输出显示在 " **值** " 列中) |  
|---------------|------------------------------------------------|  
|`[DebuggerDisplay("x = {x} y = {y}")]`<br /><br /> 在具有 `x` 和 `y`字段的类型上使用。|`x = 5 y = 18`|  
|`[DebuggerDisplay("String value is {getString()}")]`参数语法在不同的语言中会有所不同。 因此，使用时要小心。|`String value is [5, 6, 6]`|  
  
 `DebuggerDisplay` 还可以接受命名参数。  
  
|参数|目标|  
|----------------|-------------|  
|`Name`, `Type`|这些参数影响变量窗口的 **“名称”** 和 **“类型”** 列。 （可将它们设置为使用与构造函数相同的语法的字符串。）如果过度使用这些参数或使用这些参数不当，则会导致混乱的输出。|  
|`Target`, `TargetTypeName`|指定在程序集级别使用该特性时的目标类型。|  
  
 autoexp.cs 文件在程序集级别使用 DebuggerDisplay 特性。 autoexp.cs 文件确定 Visual Studio 用于 .NET 对象的默认扩展。 可以检查 autoexp.cs 文件以获得如何使用 DebuggerDisplay 特性的示例，也可以修改和编译 autoexp.cs 文件以更改默认扩展。 在修改 autoexp.cs 文件之前，一定要对该文件进行备份。  
  
 若要生成 autoexp.cs，请打开 VS2015 开发人员命令提示，并运行以下命令  
  
```  
cd <directory containing autoexp.cs>  
csc /t:library autoexp.cs  
```  
  
 将在下一调试会话中选取对 autoexp.dll 的更改。  
  
## <a name="using-expressions-in-debuggerdisplay"></a>在 DebuggerDisplay 中使用表达式  
 虽然您可以在 DebuggerDisplay 特性中的大括号之间使用常规表达式，但建议不要这样做。  
  
 DebuggerDisplay 中的常规表达式只能隐式访问目标类型的当前实例的 `this` 指针。 该表达式不能访问别名、局部变量或指针。 如果表达式引用属性，则不处理这些属性上的特性。 例如，如果字段 `[DebuggerDisplay("Object {count - 2}"`  是 8，则 C# 代码 `Object 6` 将显示 `count` 。  
  
 在 DebuggerDisplay 中使用表达式可能导致以下问题：  
  
- 计算表达式是调试器中最消耗资源的操作，并且表达式在每次显示时都会被计算。 在单步执行代码时，这可能会导致性能问题。 例如，当元素的数量很大时，一个用来在集合或列表中显示值的复杂表达式可能会很慢。  
  
- 表达式是通过当前堆栈帧的语言表达式计算器计算的，而不是通过表达式记录语言的计算器计算的。 当语言不同时，这可能导致不可预知的结果。  
  
- 计算表达式可更改应用程序的状态。 例如，设置属性值的表达式在执行代码时会改变属性值。  
  
  减少表达式计算可能出现的问题的一种方法是创建执行操作并返回字符串的私有属性。 然后，DebuggerDisplay 特性可以显示该私有属性的值。 以下示例实现了这种模式：  
  
```csharp  
[DebuggerDisplay("{DebuggerDisplay,nq}")]  
public sealed class MyClass   
{      
    public int count { get; set; }      
    public bool flag { get; set; }      
    private string DebuggerDisplay  
   {         
        get  
        {  
             return string.Format("("Object {0}", count - 2);  
        }      
    }  
}  
```  
  
## <a name="example"></a>示例  
 下面的代码示例演示如何使用 `DebuggerDisplay`以及 `DebuggerBrowseable` 和 `DebuggerTypeProxy`。 在调试器变量窗口（如 **“监视”** 窗口）中查看时，它生成类似以下内容的扩展：  
  
|**Name**|**“值”**|**Type**|  
|--------------|---------------|--------------|  
|键|"three"|object {string}|  
|“值”|3|object {int}|  
  
```csharp  
[DebuggerDisplay("{value}", Name = "{key}")]  
internal class KeyValuePairs  
{  
    private IDictionary dictionary;  
    private object key;  
    private object value;  
    public KeyValuePairs(IDictionary dictionary, object key, object value)  
    {  
        this.value = value;  
        this.key = key;  
        this.dictionary = dictionary;  
    }  
  
    public object Key  
    {  
        get { return key; }  
        set  
        {  
            object tempValue = dictionary[key];  
            dictionary.Remove(key);  
            key = value;  
            dictionary.Add(key, tempValue);  
        }  
    }  
  
    public object Value  
    {  
        get { return this.value; }  
        set  
        {  
            this.value = value;  
            dictionary[key] = this.value;  
        }  
    }  
}  
  
[DebuggerDisplay("{DebuggerDisplay,nq}")]  
[DebuggerTypeProxy(typeof(HashtableDebugView))]  
class MyHashtable  
{  
    public Hashtable hashtable;  
  
    public MyHashtable()  
    {  
        hashtable = new Hashtable();    
    }    private string DebuggerDisplay    {        get { return "Count = " + hashtable.Count); }    }  
  
    private class HashtableDebugView  
    {  
        private MyHashtable myhashtable;  
        public HashtableDebugView(MyHashtable myhashtable)  
        {  
            this.myhashtable = myhashtable;  
        }  
  
        [DebuggerBrowsable(DebuggerBrowsableState.RootHidden)]  
        public KeyValuePairs[] Keys  
        {  
            get  
            {  
                KeyValuePairs[] keys = new KeyValuePairs[myhashtable.hashtable.Count];  
  
                int i = 0;  
                foreach (object key in myhashtable.hashtable.Keys)  
                {  
                    keys[i] = new KeyValuePairs(myhashtable.hashtable, key, myhashtable.hashtable[key]);  
                    i++;  
                }  
                return keys;  
            }  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [使用 DebuggerTypeProxy 特性](../debugger/using-debuggertypeproxy-attribute.md)[增强调试和调试器显示特性](https://msdn.microsoft.com/library/72bb7aa9-459b-42c4-9163-9312fab4c410)
