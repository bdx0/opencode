# OpenCode Project Context

## Project Overview

OpenCode is an open source AI coding agent that provides a terminal-based user interface (TUI) for AI-assisted development. It's designed as a 100% open source alternative to Claude Code with a focus on terminal-based interaction and support for multiple AI providers.

### Key Features
- Terminal-based UI (TUI) built with SolidJS
- Support for multiple AI providers (Anthropic, OpenAI, Google, Azure, etc.)
- Built-in LSP (Language Server Protocol) support
- Client/server architecture allowing remote operation
- Two built-in agents: "build" (full access) and "plan" (read-only)
- Available as both CLI tool and desktop application

### Architecture
- **Monorepo structure** using Bun and Turborepo
- **Core packages**:
  - `packages/opencode`: Main application logic and server
  - `packages/app`: Shared web UI components (SolidJS)
  - `packages/desktop`: Native desktop app (Tauri wrapper)
  - `packages/console`: Console infrastructure
  - `packages/sdk`: JavaScript SDK
  - `packages/plugin`: Plugin system

## Development Environment

### Requirements
- Bun 1.3+ (primary runtime)
- Node.js 20+
- Rust toolchain (for desktop app)
- Platform-specific libraries for Tauri (if building desktop)

### Package Management
- Uses Bun as the primary package manager
- Monorepo managed with workspaces
- Dependencies specified in root `package.json` and individual package files

## Building and Running

### Development Setup
```bash
# Install dependencies
bun install

# Start development server
bun dev
```

### Running Against Different Directories
```bash
# Run OpenCode in a specific directory
bun dev <directory>

# Run OpenCode in the root of the repo
bun dev .
```

### Standalone Executable
```bash
# Build standalone executable
./packages/opencode/script/build.ts --single

# Run the built executable
./packages/opencode/dist/opencode-<platform>/bin/opencode
```

### Web App Development
```bash
# Run web UI for testing UI changes
bun run --cwd packages/app dev
```

### Desktop App Development
```bash
# Run native desktop app (requires Rust)
bun run --cwd packages/desktop tauri dev

# Build production desktop app
bun run --cwd packages/desktop tauri build
```

## Development Conventions

### Code Style
- Functions: Keep logic within a single function unless breaking it out adds clear reuse
- Destructuring: Avoid unnecessary destructuring of variables
- Control flow: Avoid `else` statements when possible
- Error handling: Prefer `.catch(...)` instead of `try`/`catch`
- Types: Use precise types, avoid `any`
- Variables: Stick to immutable patterns, avoid `let`
- Naming: Choose concise single-word identifiers when they remain descriptive
- Runtime APIs: Use Bun helpers like `Bun.file()` when appropriate

### Commit Messages
Follow conventional commit standards:
- `feat:` new features
- `fix:` bug fixes
- `docs:` documentation changes
- `chore:` maintenance tasks
- `refactor:` code refactoring
- `test:` adding/updating tests

Optionally include package scope:
- `feat(app):` feature in app package
- `fix(desktop):` bug fix in desktop package

## Project Structure

```
packages/
├── app/           # Shared web UI components (SolidJS)
├── console/       # Console infrastructure
├── desktop/       # Tauri desktop wrapper
├── opencode/      # Core application logic & server
├── plugin/        # Plugin system
├── sdk/           # JavaScript SDK
├── ui/            # UI components
├── util/          # Utility functions
└── web/           # Web application
```

## Key Technologies

- **Runtime**: Bun (primary), Node.js
- **Framework**: SolidJS (UI)
- **Build System**: Bun, Turborepo
- **Desktop**: Tauri
- **Language**: TypeScript
- **Package Manager**: Bun
- **Deployment**: SST (with Cloudflare Workers)

## Agents

OpenCode includes two built-in agents:
- **build**: Default agent with full access for development work
- **plan**: Read-only agent for analysis and code exploration
  - Denies file edits by default
  - Asks permission before running bash commands
  - Ideal for exploring unfamiliar codebases

## Configuration

- Uses `bunfig.toml` for Bun configuration
- Nix flake for reproducible development environments
- SST for cloud infrastructure deployment
- Husky for git hooks

## Testing and Quality

- Unit tests using Bun's built-in test runner
- Type checking with TypeScript
- Prettier for code formatting
- Git hooks for quality enforcement

## Deployment

- Deployed using SST framework
- Infrastructure defined in `infra/` directory
- Multiple environments (development, production)
- Cloudflare Workers as primary hosting platform

## Contributing

- Follow the style guide in STYLE_GUIDE.md
- Small, focused pull requests preferred
- All PRs must reference an existing issue
- UI changes should include screenshots/videos
- Explain how you verified logic changes work
- Keep PR descriptions concise and avoid AI-generated walls of text