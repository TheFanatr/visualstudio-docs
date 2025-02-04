---
title: "CA1725: Parameter names should match base declaration"
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
  - "ParameterNamesShouldMatchBaseDeclaration"
  - "CA1725"
helpviewer_keywords:
  - "CA1725"
  - "ParameterNamesShouldMatchBaseDeclaration"
ms.assetid: 9b657ab0-fe81-4f4c-9481-ba746988c922
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA1725: Parameter names should match base declaration

|||
|-|-|
|TypeName|ParameterNamesShouldMatchBaseDeclaration|
|CheckId|CA1725|
|Category|Microsoft.Naming|
|Breaking Change|Breaking|

## Cause

The name of a parameter in a method override does not match the name of the parameter in the base declaration of the method or the name of the parameter in the interface declaration of the method.

By default, this rule only looks at externally visible methods, but this is [configurable](#configurability).

## Rule description

Consistent naming of parameters in an override hierarchy increases the usability of the method overrides. A parameter name in a derived method that differs from the name in the base declaration can cause confusion about whether the method is an override of the base method or a new overload of the method.

## How to fix violations

To fix a violation of this rule, rename the parameter to match the base declaration. The fix is a breaking change for COM visible methods.

## When to suppress warnings

Do not suppress a warning from this rule except for COM visible methods in libraries that have previously shipped.

## Configurability

If you're running this rule from [FxCop analyzers](install-fxcop-analyzers.md) (and not with legacy analysis), you can configure which parts of your codebase to run this rule on, based on their accessibility. For example, to specify that the rule should run only against the non-public API surface, add the following key-value pair to an .editorconfig file in your project:

```ini
dotnet_code_quality.ca1725.api_surface = private, internal
```

You can configure this option for just this rule, for all rules, or for all rules in this category (Naming). For more information, see [Configure FxCop analyzers](configure-fxcop-analyzers.md).