# Actions (`degit.json`)

tiged can run post-clone actions defined in a `degit.json` file at the root of the working directory (the repo being cloned). Currently two actions are supported: `clone` and `remove`.

## File location

`degit.json` lives at the top level of the repo you are cloning; it is read by tiged after extraction and executed in the destination directory.

```json
[
  { "action": "clone", "src": "user/another-repo" },
  { "action": "remove", "files": ["LICENSE"] }
]
```

## `clone` action

Clones an additional repo into the current working directory, preserving existing files. The cloned repo can contain its own `degit.json`, allowing chained actions.

```json
[
  { "action": "clone", "src": "user/additional-starter-files" }
]
```

Useful when you want to layer multiple templates together or inject files into a repo you don't control.

## `remove` action

Deletes files at the specified paths after cloning:

```json
[
  { "action": "remove", "files": ["LICENSE", "CHANGELOG.md"] }
]
```

You can also rename a file by removing one and cloning another:

```json
[
  { "action": "remove", "files": ["readme.md"] },
  { "action": "clone", "src": "user/my-readme-template" }
]
```

## Chaining actions

Actions run in array order. A later `remove` can clean up files brought in by an earlier `clone`:

```json
[
  { "action": "clone", "src": "user/eslint-config" },
  { "action": "remove", "files": ["eslint-config/package.json"] }
]
```

## Limitations

- Not all repos distribute a `degit.json`; this is something you add to your own repos or templates.
- Actions execute after the initial clone only. They do not run when the destination was not cloned by tiged.
