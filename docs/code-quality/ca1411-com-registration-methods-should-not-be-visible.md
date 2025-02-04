---
title: "CA1411: COM registration methods should not be visible"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "CA1411"
  - "ComRegistrationMethodsShouldNotBeVisible"
helpviewer_keywords:
  - "ComRegistrationMethodsShouldNotBeVisible"
  - "CA1411"
ms.assetid: a59f96f1-1f38-4596-b656-947df5c55311
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
 - CSharp
 - VB
ms.workload:
  - "multiple"
---
# CA1411: COM registration methods should not be visible

|||
|-|-|
|TypeName|ComRegistrationMethodsShouldNotBeVisible|
|CheckId|CA1411|
|Category|Microsoft.Interoperability|
|Breaking Change|Breaking|

## Cause

A method that is marked with the <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName> or the <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName> attribute is externally visible.

## Rule description
When an assembly is registered with Component Object Model (COM), entries are added to the registry for each COM-visible type in the assembly. Methods that are marked with the <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute> and <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute> attributes are called during the registration and unregistration processes, respectively, to run user code that is specific to the registration/unregistration of these types. This code should not be called outside these processes.

## How to fix violations
To fix a violation of this rule, change the accessibility of the method to `private` or `internal` (`Friend` in [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]).

## When to suppress warnings
Do not suppress a warning from this rule.

## Example
The following example shows two methods that violate the rule.

[!code-csharp[FxCop.Interoperability.ComRegistration2#1](../code-quality/codesnippet/CSharp/ca1411-com-registration-methods-should-not-be-visible_1.cs)]
[!code-vb[FxCop.Interoperability.ComRegistration2#1](../code-quality/codesnippet/VisualBasic/ca1411-com-registration-methods-should-not-be-visible_1.vb)]

## Related rules
[CA1410: COM registration methods should be matched](../code-quality/ca1410-com-registration-methods-should-be-matched.md)

## See also

- <xref:System.Runtime.InteropServices.RegistrationServices?displayProperty=fullName>
- [Registering Assemblies with COM](/dotnet/framework/interop/registering-assemblies-with-com)
- [Regasm.exe (Assembly Registration Tool)](/dotnet/framework/tools/regasm-exe-assembly-registration-tool)