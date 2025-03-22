# VSCode Extension Starter Kit

![Microsoft](https://img.shields.io/badge/Microsoft-FEB800)
![VS Code](https://img.shields.io/badge/VS%20Code-1.98+-blue.svg)
![TypeScript](https://img.shields.io/badge/TypeScript-5.7.3-blue.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

A minimal, production-ready starter kit for building Visual Studio Code extensions in TypeScript. This template provides everything you need to start developing high-quality VS Code extensions with modern tooling.

## Quick Start

```bash
# Clone and setup
git clone https://github.com/rmcnldyo/vscode-extension-starter.git my-extension && \
cd my-extension && \
npm install

# Start development
npm run watch

# In a new terminal, launch the extension
code --new-window .
```

Then:
1. Press `F5` to launch the extension
2. Open Command Palette (`Cmd+Shift+P` or `Ctrl+Shift+P`)
3. Type "Hello World" and select the command
4. You should see a notification message

## Table of Contents

[Features](#features)
[Prerequisites](#prerequisites)
[Installation](#installation)
[Development Workflow](#development-workflow)
[Project Structure](#project-structure)
[Testing](#testing)
[Debugging](#debugging)
[Packaging and Publishing](#packaging-and-publishing)
[Extension Capabilities](#extension-capabilities)
[Resources](#resources)
[Contributing](#contributing)
[License](#license)
[Changelog](#changelog)
[Acknowledgements](#acknowledgements)

## Features

- 🚀 **Modern TypeScript** - Full TypeScript support with strict type checking
- ⚡ **ESBuild** - Fast builds and hot reloading during development
- 🧪 **Testing Framework** - Built-in testing setup with Mocha
- 🔍 **ESLint** - Code quality and style consistency with modern flat config
- 📦 **Easy Packaging** - Simple commands to package and publish your extension
- 📄 **TypeScript Definitions** - Complete VSCode API type definitions
- 🔄 **Watch Mode** - Auto-reloads and type-checks as you code
- 🛠️ **Production Ready** - Optimized bundle for marketplace distribution
- 🔌 **Modern Activation** - Uses VS Code's recommended activation patterns
- 📋 **Parallel Execution** - Efficient build pipeline with npm-run-all

## Prerequisites

- **Node.js** - Version 18.x or higher (recommended)
- **Visual Studio Code** - Version 1.98.0 or higher
- **Git** - For version control

## Installation

You can get started in two ways: by cloning this repository or by using the Yeoman generator to create a new extension from scratch.

### Option 1: Clone this Repository

```bash
# Clone the repository
git clone https://github.com/rmcnldyo/vscode-extension-starter.git my-extension

# Navigate to the project directory
cd my-extension

# Install dependencies
npm install
```

### Option 2: Use the Yeoman Generator (as recommended by microsoft)

#### Install the Generator

Install Yeoman and the VS Code Extension generator:

```bash
npm install -g yo generator-code
```

#### Run Yo Code

The Yeoman generator will walk you through the steps required to create your extension, prompting for the required information:

```bash
yo code
```

#### Generator Output

The generator will:
* Create a base folder structure
* Template out a properly configured `package.json`
* Import any assets required for your extension
* Set up the extension's activation events and contribution points

### Development Setup

It's recommended to install the following VS Code extensions for the best development experience:

- ESLint
- Extension Test Runner
- TSLint Problem Matcher

## Development Workflow

### Start Development Server

```bash
# Start the development server with hot reloading
npm run watch
```

This command runs the TypeScript compiler and ESBuild in watch mode, enabling real-time compilation as you code.

### Launch the Extension

1. Press `F5` in VS Code to launch a new Extension Development Host window
2. Your extension will be loaded and ready for testing
3. Run the "Hello World" command from the Command Palette (`Ctrl+Shift+P` or `Cmd+Shift+P`)
4. You should see a notification message "Hello World from vscode-extension-starter!"

### Build for Production

```bash
# Create a production build
npm run package
```

This creates an optimized bundle using ESBuild, preparing your extension for packaging and distribution.

## Project Structure

```
vscode-extension-starter/
├── .vscode/             # VS Code configuration files
├── src/                 # Source code
│   ├── extension.ts     # Main extension entry point
│   └── test/            # Test files
├── dist/                # Compiled output (generated)
├── package.json         # Extension manifest and npm configuration
├── tsconfig.json        # TypeScript configuration
├── eslint.config.mjs    # ESLint configuration (flat config format)
└── esbuild.js           # ESBuild bundling script
```

### Key Files

- **src/extension.ts**: The main entry point for your extension
- **package.json**: Defines extension metadata, contributions, and dependencies
- **tsconfig.json**: TypeScript compiler configuration
- **esbuild.js**: Configuration for bundling your extension with performance optimizations

### Understanding Extension Activation

This starter uses VS Code's modern activation model:

- The empty `activationEvents` array in `package.json` indicates that the extension uses package.json's `contributes` section for automatic activation
- The extension will activate when a user invokes the contributed command (`vscode-extension-starter.helloWorld`)
- This approach follows VS Code's best practices for optimizing startup time

## Testing

This starter includes a test setup using Mocha:

```bash
# Run all tests
npm test

# Watch tests during development
npm run watch-tests
```

### Creating Tests

- Add test files in the `src/test` directory with names ending in `.test.ts`
- Use the VS Code Extension Test Runner to run and debug tests

## Debugging

1. Set breakpoints in your code in `src/extension.ts`
2. Press `F5` to start debugging
3. Trigger your extension's functionality in the Extension Development Host
4. View debugging output in the Debug Console

## Packaging and Publishing

### Create a VSIX Package

```bash
# Install vsce if you haven't already
npm install -g @vscode/vsce

# Package the extension for distribution
npm run vscode:prepublish
vsce package
```

This will create a `.vsix` file that can be installed manually or published to the VS Code Marketplace.

### Publishing to Marketplace

1. Create a publisher on the [VS Code Marketplace](https://marketplace.visualstudio.com/manage)
2. Get a Personal Access Token from [Azure DevOps](https://dev.azure.com)
3. Login with `vsce login your-publisher-name`
4. Publish with `vsce publish`

### Marketplace Requirements

For a successful marketplace listing, ensure you have:

- A descriptive `README.md` with screenshots or GIFs showing your extension
- A clear icon (at least 128x128px) defined in `package.json`
- Appropriate categories and tags in `package.json`
- A license file
- A well-written description with proper formatting

Refer to the [VS Code Extension Publishing Guide](https://code.visualstudio.com/api/working-with-extensions/publishing-extension) for more details.

### Extension Capabilities

VS Code extensions can contribute to many areas:

- **Commands**: Register custom commands users can trigger
- **Menus**: Add items to VS Code's menus
- **Keybindings**: Define custom keyboard shortcuts
- **Languages**: Add language support or enhance existing languages
- **Themes**: Provide color themes or icon themes
- **Views & Panels**: Add custom views to the sidebar or panels
- **Settings**: Contribute configurable settings
- **Webviews**: Create custom UI with web technologies

### Adding Commands

Add new commands in `package.json`:

```json
"contributes": {
  "commands": [
    {
      "command": "my-extension.newCommand",
      "title": "My New Command"
    }
  ]
}
```

Then implement them in `extension.ts`:

```typescript
const disposable = vscode.commands.registerCommand('my-extension.newCommand', () => {
  // Command implementation
});
context.subscriptions.push(disposable);
```

## Resources

- [VS Code Extension API](https://code.visualstudio.com/api) - Comprehensive documentation
- [VS Code Extension Samples](https://github.com/microsoft/vscode-extension-samples) - Official examples
- [VS Code Extension Development](https://code.visualstudio.com/api/get-started/your-first-extension) - Getting started guide
- [Publishing Extensions](https://code.visualstudio.com/api/working-with-extensions/publishing-extension) - Guide to publishing
- [Extension Guidelines](https://code.visualstudio.com/api/references/extension-guidelines) - Best practices

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for version history and updates.

## Contributing

We welcome contributions to improve this template! Here's how you can help:

1. **Report Issues**: Found a bug or have a feature request? [Open an issue](https://github.com/microsoft/vscode-generator-code/issues/new).
2. **Fix Issues**: Check the [open issues](https://github.com/microsoft/vscode-generator-code/issues) to find something to work on.
3. **Submit PRs**: Submit pull requests with bug fixes or enhancements.

Please follow the [contribution guidelines](https://github.com/microsoft/vscode-generator-code/blob/main/.github/CONTRIBUTING.md) when submitting code.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgements

This starter project uses [Yeoman](https://github.com/yeoman/yo) and the [VS Code Extension Generator](https://github.com/microsoft/vscode-generator-code) recommended by Microsoft as its foundation.
