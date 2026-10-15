---
name: nuget-package-contextfreetasks
description: Use when writing C# async library methods that should avoid capturing the synchronization context without repeating ConfigureAwait(false), or when adapting ContextFreeTask methods to Task APIs.
metadata:
  homepage: "https://github.com/ufcpp/ContextFreeTask"
  version: "ContextFreeTasks 0.4.0"
  last-updated: "2026-10-16"
  generated-by: "gpt-6"
---

# ContextFreeTasks

## Prerequisite

For a project-local skill, inspect every project in the consuming repository or solution for `ContextFreeTasks`, including imported package references and resolved dependencies. A central `PackageVersion` entry alone does not prove installation. If no project references it, ask whether to install the package or remove this skill, and wait for the user's choice. Only if installation is chosen, run `dotnet add <project.csproj> package ContextFreeTasks`. This check does not apply to the skill catalog itself.

## When and why

Use `ContextFreeTask` or `ContextFreeTask<T>` as an async method's return type when its body does not need the caller's synchronization context. This replaces repeated `ConfigureAwait(false)` calls inside that method, reducing repetition and missed awaits. Requires C# 7 or later.

Keep context-dependent code, such as UI updates, outside these methods. This is a `Task` wrapper, not a `ValueTask` allocation optimization or a request to run work on another thread.

## Usage

```csharp
using ContextFreeTasks;
using System.Net.Http;
using System.Threading.Tasks;

static async ContextFreeTask<string> ReadTrimmedAsync(HttpClient client, string url)
{
    // This method needs no caller context, so ConfigureAwait(false) is unnecessary here.
    string text = await client.GetStringAsync(url);
    return text.Trim();
}

// Preserve an existing Task-based API contract with the wrapped Task property.
static Task<string> ReadAsync(HttpClient client, string url)
    => ReadTrimmedAsync(client, url).Task;
```

Use non-generic `async ContextFreeTask` for methods without a result. Await either form directly. Use `.Task` when passing the result to APIs such as `Task.WhenAll`.

The context-free behavior belongs to the method body. A caller using ordinary `async Task` still captures its own context when awaiting a `ContextFreeTask`; use `await operation.ConfigureAwait(false)` there if that caller also needs to avoid capture. Merely exposing `.Task` does not change the method body's behavior.

## Further reference

The [project homepage](https://github.com/ufcpp/ContextFreeTask) and its linked source cover the task-like pattern and async method builder implementation intentionally omitted here. Consult them only when those internals or less common helpers such as `ContextFreeTask.Run` are needed.

Do not fetch the homepage for information already covered here.
