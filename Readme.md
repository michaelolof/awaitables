## Awaitables

This is an experimental repo designed to highlight both the possibilities, and limitations, of using async await for monads other than Task like types.

### Async State Machinery

You can find documentation on task like types at https://github.com/dotnet/roslyn/pull/43635/files. Whilst the extension points to allow a task to be awaited or used as the return type of an async method are designed around task based scenarios, they can be abused for a much larger selection of monads.

### Implemented Awaitables

- `Option<T>`
- `Result<T>`
- `AwaitableEnumerable<T>`

### Limitations

All three implementations have only limited testing and carry out only limited validation, as they were designed to highlight the possibilities of state machine based rewriting in C#, rather than to be used in production.
However all three of them *almost work*. `Result<T>` and `Option<T>` are allocation free and highly efficient, and `AwaitableEnumerable<T>` only allocates the enumerable required to store the result of the method. There is just one critical limitation they all share, and which the language currently provides no way around: They do not respect the semantics of try/catch/finally or using blocks.
