---
title: "CA1815: Override equals and operator equals on value types"
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
  - "CA1815"
  - "OverrideEqualsAndOperatorEqualsOnValueTypes"
helpviewer_keywords:
  - "OverrideEqualsAndOperatorEqualsOnValueTypes"
  - "CA1815"
ms.assetid: 0a8ab3a3-ee8e-46f7-985d-dcf00c89363b
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA1815: Override equals and operator equals on value types

|||
|-|-|
|TypeName|OverrideEqualsAndOperatorEqualsOnValueTypes|
|CheckId|CA1815|
|Category|Microsoft.Performance|
|Breaking Change|Non-breaking|

## Cause

A value type does not override <xref:System.Object.Equals%2A?displayProperty=fullName> or does not implement the equality operator (==). This rule does not check enumerations.

By default, this rule only looks at externally visible types, but this is [configurable](#configurability).

## Rule description

For value types, the inherited implementation of <xref:System.Object.Equals%2A> uses the Reflection library, and compares the contents of all fields. Reflection is computationally expensive, and comparing every field for equality might be unnecessary. If you expect users to compare or sort instances, or use them as hash table keys, your value type should implement <xref:System.Object.Equals%2A>. If your programming language supports operator overloading, you should also provide an implementation of the equality and inequality operators.

## How to fix violations

To fix a violation of this rule, provide an implementation of <xref:System.Object.Equals%2A>. If you can, implement the equality operator.

## When to suppress warnings

It is safe to suppress a warning from this rule if instances of the value type will not be compared to each other.

## Configurability

If you're running this rule from [FxCop analyzers](install-fxcop-analyzers.md) (and not with legacy analysis), you can configure which parts of your codebase to run this rule on, based on their accessibility. For example, to specify that the rule should run only against the non-public API surface, add the following key-value pair to an .editorconfig file in your project:

```ini
dotnet_code_quality.ca1815.api_surface = private, internal
```

You can configure this option for just this rule, for all rules, or for all rules in this category (Performance). For more information, see [Configure FxCop analyzers](configure-fxcop-analyzers.md).

## Example

The following code shows a structure (value type) that violates this rule:

[!code-csharp[FxCop.Performance.OverrideEqualsViolation#1](../code-quality/codesnippet/CSharp/ca1815-override-equals-and-operator-equals-on-value-types_1.cs)]

The following code fixes the previous violation by overriding <xref:System.ValueType.Equals%2A?displayProperty=fullName> and implementing the equality operators (==, !=):

[!code-csharp[FxCop.Performance.OverrideEqualsFixed#1](../code-quality/codesnippet/CSharp/ca1815-override-equals-and-operator-equals-on-value-types_2.cs)]

## Related rules

- [CA2224: Override equals on overloading operator equals](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)
- [CA2231: Overload operator equals on overriding ValueType.Equals](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md)
- [CA2226: Operators should have symmetrical overloads](../code-quality/ca2226-operators-should-have-symmetrical-overloads.md)

## See also

- <xref:System.Object.Equals%2A?displayProperty=fullName>