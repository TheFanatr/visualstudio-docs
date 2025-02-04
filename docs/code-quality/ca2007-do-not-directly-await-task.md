---
title: "CA2007: Do not directly await a Task"
ms.date: 03/08/2019
ms.topic: reference
f1_keywords:
  - "CA2007"
  - "DoNotDirectlyAwaitATaskAnalyzer"
helpviewer_keywords:
  - "CA2007"
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
 - CSharp
---
# CA2007: Do not directly await a Task

|||
|-|-|
|TypeName|DoNotDirectlyAwaitATaskAnalyzer|
|CheckId|CA2007|
|Category|Microsoft.Reliability|
|Breaking Change|Non-breaking|

## Cause

An asynchronous method [awaits](/dotnet/csharp/language-reference/keywords/await) a <xref:System.Threading.Tasks.Task> directly.

## Rule description

When an asynchronous method awaits a <xref:System.Threading.Tasks.Task> directly, continuation occurs in the same thread that created the task. This behavior can be costly in terms of performance and can result in a deadlock on the UI thread. Consider calling <xref:System.Threading.Tasks.Task.ConfigureAwait(System.Boolean)?displayProperty=nameWithType> to signal your intention for continuation.

This rule was introduced with [FxCop analyzers](install-fxcop-analyzers.md) and doesn't exist in legacy FxCop analysis.

## How to fix violations

To fix violations, call <xref:System.Threading.Tasks.Task.ConfigureAwait%2A> on the awaited <xref:System.Threading.Tasks.Task>. You can pass either `true` or `false` for the `continueOnCapturedContext` parameter.

- Calling `ConfigureAwait(true)` on the task has the same behavior as not explicitly calling <xref:System.Threading.Tasks.Task.ConfigureAwait%2A>. By explicitly calling this method, you're letting readers know you intentionally want to perform the continuation on the original synchronization context.

- Call `ConfigureAwait(false)` on the task to schedule continuations to the thread pool, thereby avoiding a deadlock on the UI thread. Passing `false` is a good option for app-independent libraries.

## When to suppress warnings

You can suppress this warning if you know that the consumer is not a graphical user interface (GUI) app or if the consumer does not have a <xref:System.Threading.SynchronizationContext>.

## Example

The following code snippet generates the warning:

```csharp
public async Task Execute()
{
    Task task = null;
    await task;
}
```

To fix the violation, call <xref:System.Threading.Tasks.Task.ConfigureAwait%2A> on the awaited <xref:System.Threading.Tasks.Task>:

```csharp
public async Task Execute()
{
    Task task = null;
    await task.ConfigureAwait(false);
}
```

## Configurability

You can configure whether you want to exclude asynchronous methods that don't return a value from this rule. To exclude these kinds of methods, add the following key-value pair to an .editorconfig file in your project:

```ini
# Package version 2.9.0 and later
dotnet_code_quality.CA2007.exclude_async_void_methods = true

# Package version 2.6.3 and earlier
dotnet_code_quality.CA2007.skip_async_void_methods = true
```

You can also configure which output assembly kinds to apply this rule to. For example, to only apply this rule to code that produces a console application or a dynamically linked library (that is, not a UI app), add the following key-value pair to an .editorconfig file in your project:

```ini
dotnet_code_quality.CA2007.output_kind = ConsoleApplication, DynamicallyLinkedLibrary
```

For more information, see [Configure FxCop analyzers](configure-fxcop-analyzers.md).

## See also

- [Should I await a task with ConfigureAwait(false)?](https://github.com/Microsoft/vs-threading/blob/master/doc/cookbook_vs.md#should-i-await-a-task-with-configureawaitfalse)
- [Install FxCop analyzers in Visual Studio](install-fxcop-analyzers.md)