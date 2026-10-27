# Sayon for Visual Studio Code

Editing support for the [Sayon](https://github.com/sayon-lang/sayon) programming language:

- Syntax highlighting, including expressions inside string interpolation
- The Sayon icon for `.sayon` files
- Comment toggling (`#` for lines, `##` for blocks), bracket matching, and auto-closing pairs
- Indentation after block headers, with four spaces and LF line endings by default
- From Sayon's language server, `sayon lsp`: errors and warnings as you type, hover with signatures and doc comments, Go to Definition, Find All References, Rename Symbol, Format Document, parameter hints as you write a call, and completion that fits the place: what an argument's type takes first, a structure's fields, an enum's variants after `case`, types after `:`, module paths in imports, and standard modules with their imports, functions with placeholders for their arguments

The language server comes with Sayon: the extension runs the program the setting `sayon.path` names, or else `sayon` from the `PATH`, or else the one Sayon's setup installed, as when VS Code was already open while it ran. **Sayon: Restart the Language Server** starts it again, as after updating Sayon. The extension has no dependencies of its own.

## Installing from the repository

Package the extension and install it:

```sh
python scripts/package.py
code --install-extension out/sayon-0.0.1.vsix
```

Or with the `vsce` tool:

```sh
npx @vscode/vsce package
code --install-extension sayon-0.0.1.vsix
```

## Testing

```sh
node test/client.cjs
```

It runs the extension's client in Node against `sayon lsp`, with a stand-in for the part of VS Code's API the extension uses: a document opens, its diagnostics arrive, and the extension's providers answer. It uses the `sayon` that `SAYON` names, or else the one on the `PATH`. The tests of [sayon-lang/sayon](https://github.com/sayon-lang/sayon) run it too, with the `sayon` they build, when this repository is checked out beside it as `../sayon-vscode`.

## License

[Apache License, Version 2.0, with LLVM's exception](LICENSE), as Sayon.
