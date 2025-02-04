---
title: "CA1008: Enums should have zero value"
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
  - "CA1008"
  - "EnumsShouldHaveZeroValue"
helpviewer_keywords:
  - "CA1008"
  - "EnumsShouldHaveZeroValue"
ms.assetid: 3503a73c-360c-416d-8ee4-c2aa44365a05
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
# CA1008: Enums should have zero value

|||
|-|-|
|TypeName|EnumsShouldHaveZeroValue|
|CheckId|CA1008|
|Category|Microsoft.Design|
|Breaking Change|Non-breaking - When you are prompted to add a **None** value to a non-flag enumeration. Breaking - When you are prompted to rename or remove any enumeration values.|

## Cause

An enumeration without an applied <xref:System.FlagsAttribute?displayProperty=fullName> does not define a member that has a value of zero. Or, an enumeration that has an applied <xref:System.FlagsAttribute> defines a member that has a value of zero but its name is not 'None'. Or, the enumeration defines multiple, zero-valued members.

By default, this rule only looks at externally visible enumerations, but this is [configurable](#configurability).

## Rule description

The default value of an uninitialized enumeration, just like other value types, is zero. A non-flags-attributed enumeration should define a member that has the value of zero so that the default value is a valid value of the enumeration. If appropriate, name the member 'None'. Otherwise, assign zero to the most frequently used member. By default, if the value of the first enumeration member is not set in the declaration, its value is zero.

If an enumeration that has the <xref:System.FlagsAttribute> applied defines a zero-valued member, its name should be 'None' to indicate that no values have been set in the enumeration. Using a zero-valued member for any other purpose is contrary to the use of the <xref:System.FlagsAttribute> in that the AND and OR bitwise operators are useless with the member. This implies that only one member should be assigned the value zero. If multiple members that have the value zero occur in a flags-attributed enumeration, `Enum.ToString()` returns incorrect results for members that are not zero.

## How to fix violations

To fix a violation of this rule for non-flags-attributed enumerations, define a member that has the value of zero; this is a non-breaking change. For flags-attributed enumerations that define a zero-valued member, name this member 'None' and delete any other members that have a value of zero; this is a breaking change.

## When to suppress warnings

Do not suppress a warning from this rule except for flags-attributed enumerations that have previously shipped.

## Configurability

If you're running this rule from [FxCop analyzers](install-fxcop-analyzers.md) (and not with legacy analysis), you can configure which parts of your codebase to run this rule on, based on their accessibility. For example, to specify that the rule should run only against the non-public API surface, add the following key-value pair to an .editorconfig file in your project:

```ini
dotnet_code_quality.ca1008.api_surface = private, internal
```

You can configure this option for just this rule, for all rules, or for all rules in this category (Design). For more information, see [Configure FxCop analyzers](configure-fxcop-analyzers.md).

## Example

The following example shows two enumerations that satisfy the rule and an enumeration, `BadTraceOptions`, that violates the rule.

[!code-cpp[FxCop.Design.EnumsZeroValue#1](../code-quality/codesnippet/CPP/ca1008-enums-should-have-zero-value_1.cpp)]
[!code-csharp[FxCop.Design.EnumsZeroValue#1](../code-quality/codesnippet/CSharp/ca1008-enums-should-have-zero-value_1.cs)]
[!code-vb[FxCop.Design.EnumsZeroValue#1](../code-quality/codesnippet/VisualBasic/ca1008-enums-should-have-zero-value_1.vb)]

## Related rules

- [CA2217: Do not mark enums with FlagsAttribute](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)
- [CA1700: Do not name enum values 'Reserved'](../code-quality/ca1700-do-not-name-enum-values-reserved.md)
- [CA1712: Do not prefix enum values with type name](../code-quality/ca1712-do-not-prefix-enum-values-with-type-name.md)
- [CA1028: Enum storage should be Int32](../code-quality/ca1028-enum-storage-should-be-int32.md)
- [CA1027: Mark enums with FlagsAttribute](../code-quality/ca1027-mark-enums-with-flagsattribute.md)

## See also

- <xref:System.Enum?displayProperty=fullName>