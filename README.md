# apl-vscode

A Visual Studio Code extension that adds language support for APL. The package contributes file associations, syntax highlighting, snippets, a color theme, and a lightweight language server that tokenizes source and reports basic grammar and symbol issues. The repository name is `apl-vscode`, while the extension's package metadata identifies the language as APL.

## Editor features

- Recognizes `.apl` and `.aplh` files as APL source.
- Highlights syntax through the TextMate grammar in `syntaxes/`.
- Provides starter snippets and editor language configuration.
- Runs tokenization and basic parsing and semantic checks through a language-server client.
- Offers a APL module-test command in editor context and title menus.
- Includes a APL color theme and language icon assets.

The analysis is lightweight and gives editing feedback; it does not replace a compiler or runtime.

## Requirements and local build

The extension targets VS Code 1.80 or later and uses Node.js tooling. Install dependencies and compile the TypeScript source with:

```bash
npm install
npm run build
```

This writes compiled extension code under `out/`. To create a VSIX package, use:

```bash
npx vsce package
```

The package metadata in `package.json` defines the extension identifier, activation events, commands, language registration, and build scripts.

## Build with Docker

```bash
docker build -t apl-vscode .
docker run --rm -v "$(pwd):/app" -v "$(pwd)/output:/output" apl-vscode
```

From the parent project workspace, the Makefile target `vscode-docker-package` invokes the same Docker packaging flow.

## Source layout

- `src/extension.ts` activates the extension and registers editor behavior.
- `src/server.ts` starts the language server.
- `src/aplParser.ts`, `src/aplSemantics.ts`, and `src/aplTarget.ts` implement language analysis.
- `syntaxes/` contains the highlighting grammar, and `snippets/` contains code templates.
- `themes/` and the image assets provide editor presentation.
- `language-configuration.json` defines comments, brackets, and editor behavior.

Use `npm run watch` while editing TypeScript. When changing parser or semantic behavior, update or add a representative APL sample and verify it in VS Code's extension development host. Keep generated VSIX files and local build output out of source control unless intentionally distributing them.

