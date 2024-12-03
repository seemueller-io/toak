# code-tokenizer-md
for me but you can use it too

![code-tokenizer-md](./code-tokenizer-md.jpg)

> Push the limits of possible 

## Quick Start
```bash
$ cd your-git-repo
$ npx code-tokenizer-md
```

## Overview

`code-tokenizer-md` is a tool that processes git repository files, cleans code, redacts sensitive information, and generates markdown documentation with token counts using the Llama 3 tokenizer.

## Philosophy
> Human-first technologies for a better tomorrow.


```mermaid
graph TD
   Start[Start] -->|Read| Git[Git Files]
   Git -->|Clean| TC[TokenCleaner]
   TC -->|Redact| Clean[Clean Code]
   Clean -->|Generate| MD[Markdown]
   MD -->|Count| Results[Token Counts]
   style Start fill:#000000,stroke:#FFFFFF,stroke-width:4px,color:#ffffff
   style Git fill:#222222,stroke:#FFFFFF,stroke-width:2px,color:#ffffff
   style TC fill:#333333,stroke:#FFFFFF,stroke-width:2px,color:#ffffff
   style Clean fill:#444444,stroke:#FFFFFF,stroke-width:2px,color:#ffffff
   style MD fill:#555555,stroke:#FFFFFF,stroke-width:2px,color:#ffffff
   style Results fill:#666666,stroke:#FFFFFF,stroke-width:2px,color:#ffffff
```

## Features

### Data Processing
- Reads tracked files from git repository
- Removes comments, imports, and unnecessary whitespace
- Redacts sensitive information (API keys, tokens, JWT, hashes)
- Counts tokens using llama3-tokenizer-js
- Supports nested .code-tokenizer-md-ignore files

### Token Cleaning
- Removes single-line and multi-line comments
- Strips console.log statements
- Removes import statements
- Cleans up whitespace and empty lines

### Security Features
- Redacts API keys and secrets
- Masks JWT tokens
- Hides authorization tokens
- Redacts Base64 encoded strings
- Masks cryptographic hashes

## Requirements

- Node.js (>=14.0.0)
- Git repository
- Bun runtime (for development)

## Installation

```bash
npm install code-tokenizer-md
```

## Usage

### CLI
```bash
npx code-tokenizer-md
```

### Programmatic Usage

```typescript
import { MarkdownGenerator } from 'code-tokenizer-md';

const generator = new MarkdownGenerator({
  dir: './project',
  outputFilePath: './output.md',
  verbose: true
});

const result = await generator.createMarkdownDocument();
```

## Configuration

### MarkdownGenerator Options

```typescript
interface MarkdownGeneratorOptions {
  dir?: string;                    // Project directory (default: '.')
  outputFilePath?: string;         // Output file path (default: './prompt.md')
  fileTypeExclusions?: Set<string>;// File types to exclude
  fileExclusions?: string[];      // File patterns to exclude
  customPatterns?: Record<string, any>;      // Custom cleaning patterns
  customSecretPatterns?: Record<string, any>;// Custom redaction patterns
  verbose?: boolean;              // Enable verbose logging (default: true)
}
```

### Ignore File Configuration

Create a `.code-tokenizer-md-ignore` file in any directory to specify exclusions. The tool supports nested ignore files that affect their directory and subdirectories.

Example `.code-tokenizer-md-ignore`:
```plaintext
# Ignore specific files
secrets.json
config.private.ts

# Ignore directories
build/
temp/

# Glob patterns
**/*.test.ts
**/._*
```

#### Default Exclusions

The tool automatically excludes common file types and patterns:

File Types:
- Images: .jpg, .jpeg, .png, .gif, .bmp, .svg, .webp, etc.
- Fonts: .ttf, .woff, .woff2, .eot, .otf
- Binaries: .exe, .dll, .so, .dylib, .bin
- Archives: .zip, .tar, .gz, .rar, .7z
- Media: .mp3, .mp4, .avi, .mov, .wav
- Data: .db, .sqlite, .sqlite3
- Config: .lock, .yaml, .yml, .toml, .conf

File Patterns:
- Configuration files: .*rc, tsconfig.json, package-lock.json
- Version control: .git*, .hg*, .svn*
- Environment files: .env*
- Build outputs: build/, dist/, out/
- Dependencies: node_modules/
- Documentation: docs/, README*, CHANGELOG*
- IDE settings: .idea/, .vscode/
- Test files: test/, spec/, __tests__/

## Development

This project uses [Bun](https://bun.sh) for development. To contribute:

### Setup
```bash
git clone <repository>
cd code-tokenizer-md
bun install
```

### Scripts
```bash
# Build the project
bun run build

# Run tests
bun test

# Lint code
bun run lint

# Fix linting issues
bun run lint:fix

# Format code
bun run format

# Fix all (format + lint)
bun run fix

# Development mode
bun run dev

# Publish development version
bun run deploy:dev
```

### Project Structure
```
src/
├── index.ts              # Main exports
├── TokenCleaner.ts       # Code cleaning and redaction
├── MarkdownGenerator.ts  # Markdown generation logic
├── cli.ts               # CLI implementation
├── fileExclusions.ts    # File exclusion patterns
└── fileTypeExclusions.ts # File type exclusions
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Open a Pull Request

### Guidelines
- Write TypeScript code following the project's style
- Include appropriate error handling
- Add documentation for new features
- Include tests for new functionality
- Update the README for significant changes


## Note

This tool requires a git repository to function properly as it uses `git ls-files` to identify tracked files.

## License

### GNU AFFERO GENERAL PUBLIC LICENSE
Version 3, 19 November 2007
© 2024 Geoff Seemueller

