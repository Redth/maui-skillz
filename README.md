# 🛠️ MAUI Skillz

A collection of GitHub Copilot custom skills and reference documentation for .NET MAUI development. These skills extend Copilot's capabilities with deep knowledge of MAUI workloads, release management, native bindings, and more.

## 📋 Table of Contents

- [Overview](#overview)
- [Skills](#skills)
  - [MAUI Workload Discovery](#maui-workload-discovery)
  - [MAUI Release Notes](#maui-release-notes)
  - [iOS Slim Bindings](#ios-slim-bindings)
  - [Android Slim Bindings](#android-slim-bindings)
- [Documentation](#documentation)
- [Getting Started](#getting-started)
- [Contributing](#contributing)
- [License](#license)

## Overview

This repository contains **GitHub Copilot custom skills** that provide specialized knowledge and workflows for .NET MAUI development. Skills are defined using `SKILL.md` files that teach Copilot how to perform complex, multi-step tasks specific to the MAUI ecosystem.

### What are Copilot Skills?

Copilot Skills are structured prompts and workflows that extend GitHub Copilot's knowledge in specific domains. They enable Copilot to:

- Perform domain-specific tasks with expert-level accuracy
- Follow established patterns and best practices
- Access and process external data sources (NuGet, .NET releases, etc.)
- Generate consistent, well-formatted outputs

## Skills

### MAUI Workload Discovery

> **Location:** [`.claude/skills/maui-workload-discovery/SKILL.md`](.claude/skills/maui-workload-discovery/SKILL.md)

Discovers .NET SDK versions, workload sets, manifest versions, and workload dependencies for MAUI development environments.

**Use this skill when you need to know:**
- What Xcode version is required for .NET X?
- What Android SDK packages are needed for .NET MAUI?
- What JDK version is required?
- What is the latest workload set for .NET X?
- What workload versions ship with .NET X?
- What is the latest MAUI NuGet package version?

**Data Sources:**
- .NET Release Metadata API
- NuGet.org Package APIs
- Workload Manifest Packages

---

### MAUI Release Notes

> **Location:** [`.claude/skills/maui-release-notes/SKILL.md`](.claude/skills/maui-release-notes/SKILL.md)

Generates and maintains formatted release notes documentation for .NET MAUI workload releases.

**Use this skill when you need to:**
- Generate or update MAUI release notes
- Create a release notes document for .NET MAUI
- Document current MAUI workload versions
- Check for new MAUI workload releases

**Output Structure:**
```
release-notes/
├── maui-release-notes.md           # Index page with links to all releases
├── maui-release-notes-YYYYMMDD.md  # Dated release notes (most recent)
└── ...                             # Historical release notes
```

---

### iOS Slim Bindings

> **Location:** [`.claude/skills/ios-slim-bindings/SKILL.md`](.claude/skills/ios-slim-bindings/SKILL.md)

Creates and updates slim/native platform interop bindings for iOS using the Native Library Interop (NLI) approach. Guides through Swift/Objective-C wrapper creation, Xcode project configuration, API definition generation, and integration into .NET MAUI apps.

**Use this skill when you need to:**
- Create iOS bindings for a native library
- Wrap an iOS SDK for use in .NET MAUI
- Create a Swift wrapper exposing native APIs to C#
- Integrate xcframeworks into .NET projects
- Update bindings when native SDKs change
- Troubleshoot iOS binding build/runtime errors

**Key Features:**
- Complete project structure setup
- Swift wrapper implementation patterns
- CocoaPods and Swift Package Manager integration
- Objective Sharpie API definition generation
- Async/await support via completion handlers
- Comprehensive troubleshooting guide

---

### Android Slim Bindings

> **Location:** [`.claude/skills/android-slim-bindings/SKILL.md`](.claude/skills/android-slim-bindings/SKILL.md)

Creates and updates slim/native platform interop bindings for Android using the Native Library Interop (NLI) approach. Guides through Java/Kotlin wrapper creation, Gradle project configuration, Maven dependency resolution, and integration into .NET MAUI apps.

**Use this skill when you need to:**
- Create Android bindings for a native library
- Wrap an Android SDK for use in .NET MAUI
- Create a Java/Kotlin wrapper exposing native APIs to C#
- Integrate AAR/JAR files into .NET projects
- Resolve Maven dependency conflicts
- Fix "Java dependency is not satisfied" errors (XA4241/XA4242)
- Update bindings when native SDKs change
- Troubleshoot Android binding build/runtime errors

**Key Features:**
- Complete project structure setup with Gradle Wrapper
- Java and Kotlin wrapper implementation patterns
- Comprehensive Maven dependency analysis
- NuGet package mapping for common Android libraries
- Metadata.xml transforms for binding customization
- Java Dependency Verification support (.NET 9+)
- Callback interface patterns for async operations
- Comprehensive troubleshooting guide

## Documentation

Reference guides for .NET MAUI development tasks:

| Document | Description |
|----------|-------------|
| [Android Bindings Guide](docs/android-bindings-guide.md) | Creating C# bindings for native Android libraries (AAR/JAR) |
| [iOS Bindings Guide](docs/ios-bindings-guide.md) | Creating C# bindings for native iOS libraries (xcframeworks) |
| [Workload Discovery Process](docs/workload-discovery-process.md) | Technical details on discovering .NET workload information |

## Getting Started

### Using the Skills

1. **Clone this repository** to your local machine or add it to your Copilot knowledge base
2. **Reference a skill** in your Copilot chat:
   - Ask questions that match the skill's activation triggers
   - Example: *"What Xcode version is required for .NET 10?"*
   - Example: *"Generate MAUI release notes for the latest workloads"*

### Project Structure

```
maui-skillz/
├── .claude/
│   └── skills/                      # Copilot/Claude custom skills
│       ├── maui-release-notes/
│       │   └── SKILL.md             # Release notes generation skill
│       ├── maui-workload-discovery/
│       │   └── SKILL.md             # Workload discovery skill
│       ├── ios-slim-bindings/
│       │   └── SKILL.md             # iOS slim bindings skill
│       └── android-slim-bindings/
│           └── SKILL.md             # Android slim bindings skill
├── docs/                            # Reference documentation
│   ├── android-bindings-guide.md    # Android binding tutorials
│   ├── ios-bindings-guide.md        # iOS binding tutorials
│   └── ...
├── release-notes/                   # Generated release notes output
│   ├── maui-release-notes.md        # Release notes index
│   └── maui-release-notes-*.md      # Dated release notes
└── README.md                        # This file
```

## Contributing

Contributions are welcome! Here's how you can help:

1. **Add new skills** - Create a new folder under `.claude/skills/` with a `SKILL.md` file
2. **Improve documentation** - Enhance the guides in `docs/`
3. **Report issues** - File bugs or suggest improvements via GitHub Issues
4. **Share feedback** - Let us know how these skills work for your workflows

### Skill File Format

Skills use a YAML frontmatter followed by markdown instructions:

```markdown
---
name: skill-name
description: Brief description of what the skill does
---

# When to use this skill
- Trigger condition 1
- Trigger condition 2

# Instructions
Step-by-step workflow...
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

<p align="center">
  <sub>Built with 💜 for the .NET MAUI community</sub>
</p>
