---
title: "CA1000: Do not declare static members on generic types"
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
  - "CA1000"
  - "DoNotDeclareStaticMembersOnGenericTypes"
helpviewer_keywords:
  - "DoNotDeclareStaticMembersOnGenericTypes"
  - "CA1000"
ms.assetid: 5c0da594-f8d0-4f40-953d-56bf7fbd2087
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
 - CSharp
 - VB
ms.workload:
  - "multiple"
---
# CA1000: Do not declare static members on generic types

|||
|-|-|
|TypeName|DoNotDeclareStaticMembersOnGenericTypes|
|CheckId|CA1000|
|Category|Microsoft.Design|
|Breaking Change|Breaking|

## Cause

A generic type contains a `static` (`Shared` in Visual Basic) member.

By default, this rule only looks at externally visible types, but this is [configurable](#configurability).

## Rule description

When a `static` member of a generic type is called, the type argument must be specified for the type. When a generic instance member that does not support inference is called, the type argument must be specified for the member. The syntax for specifying the type argument in these two cases is different and easily confused, as the following calls demonstrate:

```vb
' Shared method in a generic type.
GenericType(Of Integer).SharedMethod()

' Generic instance method that does not support inference.
someObject.GenericMethod(Of Integer)()
```

```csharp
// Static method in a generic type.
GenericType<int>.StaticMethod();

// Generic instance method that does not support inference.
someObject.GenericMethod<int>();
```

Generally, both of the prior declarations should be avoided so that the type argument does not have to be specified when the member is called. This results in a syntax for calling members in generics that is no different from the syntax for non-generics. For more information, see [CA1004: Generic methods should provide type parameter](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md).

## How to fix violations

To fix a violation of this rule, remove the static member or change it to an instance member.

## When to suppress warnings

Do not suppress a warning from this rule. Providing generics in a syntax that is easy to understand and use reduces the time that is required to learn and increases the adoption rate of new libraries.

## Configurability

If you're running this rule from [FxCop analyzers](install-fxcop-analyzers.md) (and not with legacy analysis), you can configure which parts of your codebase to run this rule on, based on their accessibility. For example, to specify that the rule should run only against the non-public API surface, add the following key-value pair to an .editorconfig file in your project:

```ini
dotnet_code_quality.ca1000.api_surface = private, internal
```

You can configure this option for just this rule, for all rules, or for all rules in this category (Design). For more information, see [Configure FxCop analyzers](configure-fxcop-analyzers.md).

## Related rules

- [CA1005: Avoid excessive parameters on generic types](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)
- [CA1010: Collections should implement generic interface](../code-quality/ca1010-collections-should-implement-generic-interface.md)
- [CA1002: Do not expose generic lists](../code-quality/ca1002-do-not-expose-generic-lists.md)
- [CA1006: Do not nest generic types in member signatures](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)
- [CA1004: Generic methods should provide type parameter](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)
- [CA1003: Use generic event handler instances](../code-quality/ca1003-use-generic-event-handler-instances.md)
- [CA1007: Use generics where appropriate](../code-quality/ca1007-use-generics-where-appropriate.md)

## See also

- [Generics](/dotnet/csharp/programming-guide/generics/index)