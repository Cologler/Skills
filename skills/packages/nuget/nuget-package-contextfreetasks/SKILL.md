---
name: nuget-package-contextfreetasks
description: Use when writing C# async methods that do not need to capture the synchronization context (such as library or background logic, or code that would use ConfigureAwait(false)), or when modifying existing ContextFreeTask code.
metadata:
  homepage: "https://github.com/ufcpp/ContextFreeTask"
  version: "ContextFreeTasks 0.4.0"
  last-updated: "2026-11-25"
  generated-by: "gpt-6"
---

# ContextFreeTasks

## Why this package is useful

`ContextFreeTask` and `ContextFreeTask<T>` let an async method avoid capturing the synchronization context without adding `ConfigureAwait(false)` to each await. This reduces repetition and the risk of accidentally omitting it.

## Usage

Use `ContextFreeTask` or `ContextFreeTask<T>` as the return type of an async method that does not need to resume on the captured synchronization context.

```csharp
using ContextFreeTasks;

static async ContextFreeTask<string> ReadTrimmedAsync(HttpClient client, string url)
{
    string text = await client.GetStringAsync(url); // ConfigureAwait(false) is unnecessary here.
    return text.Trim();
}
```

Use `ContextFreeTask` instead of `ContextFreeTask<T>` for methods that do not return a value. Both can be awaited directly.

The context-free behavior applies to the method body, not its caller. A caller using ordinary `async Task` still captures its own context when awaiting a `ContextFreeTask`; use `await operation.ConfigureAwait(false)` if the caller also needs to avoid capture.

### Task interoperability

Use `.Task` when a `Task` is required, such as when preserving an existing API contract or passing the operation to `Task.WhenAll`.

```csharp
static Task<string> ReadAsync(HttpClient client, string url)
    => ReadTrimmedAsync(client, url).Task;
```

Exposing `.Task` does not change the method body's behavior.

## Notes

Keep code that requires the original context, such as UI updates, outside these methods. `ContextFreeTask` does not move work to another thread or provide `ValueTask`-style allocation optimizations.

Assume the project already references the `ContextFreeTasks` NuGet package. Only check the affected project's dependencies if a compiler error suggests it is missing, and ask the user for approval before adding it.

## Further reference

The [project homepage](https://github.com/ufcpp/ContextFreeTask) and its linked source cover the task-like pattern and async method builder implementation intentionally omitted here. Consult them only when those internals or less common helpers such as `ContextFreeTask.Run` are needed.

Do not fetch the homepage for information already covered here.
