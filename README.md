# Sayon for Visual Studio Code

Support for writing [Sayon](https://github.com/sayon-lang/sayon) in VS Code.

- Syntax highlighting, including the expressions inside string interpolation.
- The Sayon icon on `.sayon` files.
- Comment toggling (`#` for a line, `##` for a block), bracket matching, and auto-closing pairs.
- Indentation after a block's first line, with four spaces and LF line endings by default.
- Everything Sayon's language server offers: errors and warnings as you type, hover with signatures and doc comments, Go to Definition, Find All References, Rename Symbol, Format Document, parameter hints while you write a call, and completion that knows where you are (the fields of a structure, an enum's variants after `case`, types after `:`, module paths in imports, and functions with placeholders for their arguments).

The language server is part of Sayon itself, `sayon lsp`, so the extension needs nothing else. It runs the `sayon` named by the `sayon.path` setting, or else the one on your `PATH`, or else the one Sayon's installer put in place (which helps when VS Code was already open during the install). After updating Sayon, run **Sayon: Restart the Language Server**.

## Installing from this repository

Package the extension and install it:

```sh
python scripts/package.py
code --install-extension out/sayon-0.0.1.vsix
```

Or with `vsce`:

```sh
npx @vscode/vsce package
code --install-extension sayon-0.0.1.vsix
```

## Testing

```sh
node test/client.cjs
```

This runs the extension's client in Node against a real `sayon lsp`, with a small stand-in for the parts of VS Code's API the extension uses: it opens a document, waits for its diagnostics, and asks each provider for answers. It uses the `sayon` that `SAYON` names, or else the one on your `PATH`. The tests in [sayon-lang/sayon](https://github.com/sayon-lang/sayon) run it too, with the `sayon` they just built, when this repository is checked out next to it as `../sayon-vscode`.

## License

[Apache License 2.0 with LLVM's exception](LICENSE), the same as Sayon.
