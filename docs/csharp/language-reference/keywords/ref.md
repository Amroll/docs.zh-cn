---
title: ref（C# 参考）
ms.date: 03/06/2018
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- ref_CSharpKeyword
- ref
helpviewer_keywords:
- parameters [C#], ref
- ref keyword [C#]
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 63f984f4004cfce9694e7e7405ec2477bc370731
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2018
---
# <a name="ref-c-reference"></a>ref（C# 参考）

`ref` 关键字指示按引用传递的值。 它用在三种不同的上下文中： 

- 在方法签名和方法调用中，按引用将参数传递给方法。 有关详细信息，请参阅[引用传递参数](#passing-an-argument-by-reference)。

- 在方法签名中，按引用将值返回给调用方。 有关详细信息，请参阅[引用返回值](#reference-return-values)。

- 在成员正文中，指示引用返回值是否作为调用方欲修改的引用被存储在本地，或在一般情况下，局部变量按引用访问另一个值。 有关详细信息，请参阅 [ref 局部变量](#ref-locals)。

## <a name="passing-an-argument-by-reference"></a>按引用传递参数

在方法的参数列表中使用 `ref` 关键字时，它指示参数按引用传递，而非按值传递。 按引用传递的效果是，对所调用方法中参数进行的任何更改都反映在调用方法中。 例如，如果调用方传递本地变量表达式或数组元素访问表达式，所调用方法会替换 ref 参数引用的对象，然后，当该方法返回时，调用方的本地变量或数组元素将开始引用新对象。

> [!NOTE]
>  不要混淆通过引用传递的概念与引用类型的概念。 这两种概念是不同的。 无论方法参数是值类型还是引用类型，均可由 `ref` 修改。 当通过引用传递时，不会对值类型装箱。  

若要使用 `ref` 参数，方法定义和调用方法均必须显式使用 `ref` 关键字，如下面的示例所示。  

[!code-csharp-interactive[csrefKeywordsMethodParams#6](../../../../samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#1)]

传递到 `ref` 或 `in` 形参的实参必须先经过初始化，然后才能传递。 这与 [out](out-parameter-modifier.md) 形参不同，在传递之前，不需要显式初始化该形参的实参。

类的成员不能具有仅在 `ref`、`in` 或 `out` 方面不同的签名。 如果类型的两个成员之间的唯一区别在于其中一个具有 `ref` 参数，而另一个具有 `out` 或 `in` 参数，则会发生编译器错误。 例如，以下代码将不会编译。  

```csharp
class CS0663_Example
{
    // Compiler error CS0663: "Cannot define overloaded 
    // methods that differ only on ref and out".
    public void SampleMethod(out int i) { }
    public void SampleMethod(ref int i) { }
}
```
但是，当一个方法具有 `ref`、`in` 或 `out` 参数，另一个方法具有值参数时，则可以重载方法，如下面的示例所示。
  
[!code-csharp[csrefKeywordsMethodParams#6](../../../../samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#2)]
  
 在其他要求签名匹配的情况下（如隐藏或重写），`in`、`ref` 和 `out` 是签名的一部分，相互之间不匹配。  
  
 属性不是变量。 它们是方法，不能传递到 `ref` 参数。  
  
 有关如何传递数组的信息，请参阅[使用 ref 和 out传递数组](../../../csharp/programming-guide/arrays/passing-arrays-using-ref-and-out.md)。  
  
 不能将 `ref`、`in` 和 `out` 关键字用于以下几种方法：  
  
- 异步方法，通过使用 [async](../../../csharp/language-reference/keywords/async.md) 修饰符定义。  
- 迭代器方法，包括 [yield return](../../../csharp/language-reference/keywords/yield.md) 或 `yield break` 语句。  

## <a name="passing-an-argument-by-reference-an-example"></a>按引用传递参数：示例

前面的示例按引用传递值类型。 还可使用 `ref` 关键字按引用传递引用类型。 按引用传递引用类型使所调用方能够替换调用方中引用参数引用的对象。 对象的存储位置按引用参数的值传递到方法。 如果更改参数存储位置中的值（以指向新对象），你还可以将存储位置更改为调用方所引用的位置。 下面的示例将引用类型的实例作为 `ref` 参数传递。   
  
[!code-csharp[csrefKeywordsMethodParams#6](../../../../samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#3)]

有关如何通过值和引用传递引用类型的详细信息，请参阅[传递引用类型参数](../../../csharp/programming-guide/classes-and-structs/passing-reference-type-parameters.md)。
  
## <a name="reference-return-values"></a>引用返回值

引用返回值（或 ref 返回值）是由方法按引用向调用方返回的值。 即是说，调用方可以修改方法所返回的值，此更改反映在包含方法的对象的状态中。 

使用 `ref` 关键字来定义引用返回值：

- 在方法签名中。 例如，下列方法签名指示 `GetCurrentPrice` 方法按引用返回了 <xref:System.Decimal> 值。

   ```csharp
   public ref decimal GetCurrentValue()
   ``` 
- 在 `return` 标记和方法的 `return` 语句中返回的变量之间。 例如:
 
   ```csharp
   return ref DecimalArray[0];
   ``` 

为方便调用方修改对象的状态，引用返回值必须存储在被显式定义为 [ref 局部变量](#ref-locals)的变量中。 

有关示例，请参阅 [ref 返回值和 ref 局部变量示例](#a-ref-returns-and-ref-locals-example)

## <a name="ref-locals"></a>ref 局部变量

ref 局部变量用于指代使用 `return ref` 返回的值。  必须将 ref 局部变量初始化，并赋予 ref 返回值。 任何对 ref 本地变量值的修改都将反映在对象的状态中，该对象的方法按引用返回值。

在变量声明前或在方法（该方法将按引用返回值）调用前使用 `ref` 关键字定义 ref 局部变量。 

例如，下列语句定义名为 `GetEstimatedValue` 的方法返回的 ref 局部变量值：

```csharp
ref decimal estValue = ref Building.GetEstimatedValue();
```

可通过相同方式按引用访问值。 在某些情况下，按引用访问值可避免潜在的高开销复制操作，从而提高性能。 例如，以下语句显示用户可如何定义一个用于引用值的 ref 局部变量值。

```csharp
ref VeryLargeStruct reflocal = ref veryLargeStruct;
```

请注意，在这两个示例中，必须在两个位置同时使用 `ref` 关键字，否则编译器将生成错误 CS8172：“无法使用值对按引用变量进行初始化”。 
 
## <a name="a-ref-returns-and-ref-locals-example"></a>ref 返回值和 ref 局部变量示例

下列示例定义一个具有两个 <xref:System.String> 字段（`Title` 和 `Author`）的 `Book` 类。 还定义包含 `Book` 对象的专用数组的 `BookCollection` 类。 通过调用 `GetBookByTitle` 方法，可按引用返回个别 book 对象。

[!code-csharp[csrefKeywordsMethodParams#6](../../../../samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#4)]

调用方将 `GetBookByTitle` 方法所返回的值存储为 ref 局部变量时，调用方对返回值所做的更改将反映在 `BookCollection` 对象中，如下例所示。

[!code-csharp[csrefKeywordsMethodParams#6](../../../../samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#5)]

## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)  
 [C# 编程指南](../../../csharp/programming-guide/index.md)  
 [传递参数](../../../csharp/programming-guide/classes-and-structs/passing-parameters.md)  
 [方法参数](../../../csharp/language-reference/keywords/method-parameters.md)  
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)
