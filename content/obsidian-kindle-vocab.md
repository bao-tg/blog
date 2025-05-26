# Developer Documentation – Obsidian Kindle Vocabulary Builder Plugin

Welcome to the developer documentation for the [**Obsidian Kindle Vocabulary Builder**](https://github.com/bao-tg/obsidian-kindle-vocab-plugin). This guide will help you understand the architecture, extend functionality, and contribute effectively to the plugin.

---

## 1. Overview

* **Plugin Name**: `obsidian-kindle-vocab-plugin`
* **Project Origin**:
  Originally developed as a Spring 2025 course project at VinUniversity. It emerged from a personal pain point — the lack of a simple way to export Kindle Vocabulary Builder data into Markdown for use in Obsidian.

> I decided to open-source this tool to learn from the developer community. Building in public is the best way to grow and get feedback.

* **Key Features**:

  * Generate Markdown from your Kindle lookups (`vocab.db`)
  * Integrate your own dictionary files (CSV)
  * Mark words as "Learned/Unlearned" with checkbox interactivity
  * View stats like % learned
  * Sort words by timestamp or unlearned-first

* **Target Users**: Users of both **Kindle** and **Obsidian**.

<img src="demo/demo.gif" alt="Demo" width="800">

---

## 2. Getting Started

> Based on the [Obsidian Plugin Development Guide](https://docs.obsidian.md/Plugins/Getting+started/Build+a+plugin)

### 2.1 Prerequisites

Make sure you have the following installed:

* [Node.js](https://nodejs.org/)
* Git
* A code editor like [VSCode](https://code.visualstudio.com/)

### 2.2 Local Development Setup

⚠️ **Important:** Always use a separate development vault. Do not develop plugins in your main Obsidian vault.

Create the `plugins` directory inside your vault
```bash
cd path/to/your-dev-vault
mkdir -p .obsidian/plugins
cd .obsidian/plugins
```

Clone the repository
```bash
git clone https://github.com/bao-tg/obsidian-kindle-vocab-plugin
cd obsidian-kindle-vocab-plugin
```

Install dependencies and build/run
```bash
npm install
npm run dev
```

Then:
* Reload your plugins.
* Open **Developer Tools** in Obsidian and load the plugin.
* Enable the plugin under **Settings > Community Plugins**.
* Reload the plugin in Settings after making updates.

---

## 3. Plugin Architecture

```bash
src/                            
├── commands/                  
│   └── CommandsHandlers.ts     # Registers and defines custom plugin commands
├── data/                      # (Empty or reserved) For future data storage or constants
├── modals/                    
│   ├── DatabaseUploadModal.ts   # Modal to upload Kindle's vocab.db file
│   ├── DictionaryUploadModal.ts # Modal to upload custom dictionary CSV
│   └── SyncDatabaseModal.ts     # Modal for syncing database and generating Markdown
├── ribbon/                    
│   └── RibbonHandlers.ts       # Adds and handles ribbon icon behavior
├── settings/                  
│   ├── Settings.ts             # Defines the plugin's settings schema and defaults
│   └── SettingTab.ts           # Renders the settings tab UI in Obsidian
├── utils/                    
│   ├── MarkdownFormat.ts       # Generates interactive Markdown output and listeners
│   └── PathHelper.ts           # Path resolution for vault, plugin data, etc.
└── main.ts                   # Entry point: initializes plugin, settings, and features
```

---

## 4. Contributing

We welcome community contributions! Follow the steps below to contribute:

1. Fork the repository.
2. Create a feature branch:

```bash
git checkout -b feature/my-feature
```

3. Write clear and meaningful commit messages.
4. Run linting before committing:

```bash
npm run lint
```

5. Submit a Pull Request with a detailed description of your changes.

---

## 5. Licensing & Credits

This project is licensed under the [MIT License](https://github.com/bao-tg/obsidian-kindle-vocab-plugin/blob/master/LICENSE).

* **Author**: Truong Gia Bao
* **GitHub**: [@bao-tg](https://github.com/bao-tg)

### Sponsor This Project

If you find this plugin useful and would like to support its development:

<a href="https://www.buymeacoffee.com/baotg" target="_blank">
  <img src="https://cdn.buymeacoffee.com/buttons/v2/default-violet.png" alt="Buy Me A Coffee" width="140">
</a>

---

## 6. References & Resources

* [Obsidian Plugin Developer Docs](https://docs.obsidian.md/Plugins/Getting+started/Build+a+plugin)
* [Obsidian API Reference](https://publish.obsidian.md/api/)
* [TypeScript Handbook](https://www.typescriptlang.org/docs/)
* [esbuild Documentation](https://esbuild.github.io/)
* [GCIDE Dictionary](https://gcide.gnu.org.ua/)
* [Webster’s Dictionary CSV](https://github.com/matthewreagan/WebstersEnglishDictionary)
* [Wiktionary](https://en.wiktionary.org/wiki/Wiktionary:Main_Page)
* [Microsoft Docs – DRM](https://learn.microsoft.com/vi-vn/windows-hardware/drivers/audio/digital-rights-management)
