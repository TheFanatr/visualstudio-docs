---
title: "CA1821: Remove empty finalizers"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "RemoveEmptyFinalizers"
  - "CA1821"
helpviewer_keywords:
  - "CA1821"
ms.assetid: 3f4855a0-e4a0-46e6-923c-4c3b7074048d
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA1821: Remove empty finalizers

|||
|-|-|
|TypeName|RemoveEmptyFinalizers|
|CheckId|CA1821|
|Category|Microsoft.Performance|
|Breaking Change|Non-breaking|

## Cause

A type implements a finalizer that is empty, calls only the base type finalizer, or calls only conditionally emitted methods.

## Rule description

Whenever you can, avoid finalizers because of the additional performance overhead that's involved in tracking object lifetime. The garbage collector runs the finalizer before it collects the object. This means that at least two collections are required to collect the object. An empty finalizer incurs this added overhead without any benefit.

## How to fix violations

Remove the empty finalizer. If a finalizer is required for debugging, enclose the whole finalizer in `#if DEBUG / #endif` directives.

## When to suppress warnings

Do not suppress a message from this rule.

## Example

The following example shows an empty finalizer that should be removed, a finalizer that should be enclosed in `#if DEBUG / #endif` directives, and a finalizer that uses the `#if DEBUG / #endif` directives correctly.

[!code-csharp[FxCop.Performance.RemoveEmptyFinalizers#1](../code-quality/codesnippet/CSharp/ca1821-remove-empty-finalizers_1.cs)]
