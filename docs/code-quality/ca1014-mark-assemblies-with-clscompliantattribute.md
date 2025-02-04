---
title: "CA1014: Mark assemblies with CLSCompliantAttribute"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "CA1014"
  - "MarkAssembliesWithClsCompliant"
helpviewer_keywords:
  - "CA1014"
  - "MarkAssembliesWithClsCompliant"
ms.assetid: 4fe57449-cf45-4745-bcd2-6345f1ed266d
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
 - CPP
 - CSharp
 - VB
ms.workload:
  - "multiple"
---
# CA1014: Mark assemblies with CLSCompliantAttribute

|||
|-|-|
|TypeName|MarkAssembliesWithClsCompliant|
|CheckId|CA1014|
|Category|Microsoft.Design|
|Breaking Change|Non-breaking|

## Cause
An assembly does not have the <xref:System.CLSCompliantAttribute?displayProperty=fullName> attribute applied to it.

## Rule description
The Common Language Specification (CLS) defines naming restrictions, data types, and rules to which assemblies must conform if they will be used across programming languages. Good design dictates that all assemblies explicitly indicate CLS compliance with <xref:System.CLSCompliantAttribute>. If the attribute is not present on an assembly, the assembly is not compliant.

It is possible for a CLS-compliant assembly to contain types or type members that are not compliant.

## How to fix violations
To fix a violation of this rule, add the attribute to the assembly. Instead of marking the whole assembly as noncompliant, you should determine which type or type members are not compliant and mark these elements as such. If possible, you should provide a CLS-compliant alternative for noncompliant members so that the widest possible audience can access all the functionality of your assembly.

## When to suppress warnings
Do not suppress a warning from this rule. If you do not want the assembly to be compliant, apply the attribute and set its value to `false`.

## Example
The following example shows an assembly that has the <xref:System.CLSCompliantAttribute?displayProperty=fullName> attribute applied that declares it CLS-compliant.

[!code-csharp[FxCop.Design.AssembliesCls#1](../code-quality/codesnippet/CSharp/ca1014-mark-assemblies-with-clscompliantattribute_1.cs)]
[!code-cpp[FxCop.Design.AssembliesCls#1](../code-quality/codesnippet/CPP/ca1014-mark-assemblies-with-clscompliantattribute_1.cpp)]
[!code-vb[FxCop.Design.AssembliesCls#1](../code-quality/codesnippet/VisualBasic/ca1014-mark-assemblies-with-clscompliantattribute_1.vb)]

## See also

- <xref:System.CLSCompliantAttribute?displayProperty=fullName>
- [Language Independence and Language-Independent Components](/dotnet/standard/language-independence-and-language-independent-components)