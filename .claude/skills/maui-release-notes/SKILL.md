---
name: maui-release-notes
description: Generate or update .NET MAUI workload release notes documentation. Creates well-formatted markdown documents showing workload versions, platform dependencies, and installation instructions for .NET MAUI development environments. Maintains a release history with dated snapshots.
---

# When to use this skill
Activate this skill when the user asks:
- Generate/create MAUI release notes
- Update the workload release notes document
- Create a release notes document for .NET MAUI
- Document the current MAUI workload versions
- What format should MAUI release notes use?
- Add a new .NET version section to release notes
- Check for new MAUI workload releases

# Overview
This skill generates formatted markdown documentation for .NET MAUI workload releases. It focuses on **document structure and formatting** while relying on the `maui-workload-discovery` skill to obtain actual version data.

The release notes system consists of:
1. **Index Page** (`release-notes/maui-release-notes.md`) - Lists all release notes with version summaries and links
2. **Dated Release Notes** (`release-notes/maui-release-notes-YYYYMMDD.md`) - Detailed release notes for each update

# File Structure

```
release-notes/
├── maui-release-notes.md              # Index page with links to all releases
├── maui-release-notes-20260119.md     # Dated release notes (most recent)
├── maui-release-notes-20260115.md     # Previous release notes
├── maui-release-notes-20260110.md     # Older release notes
└── ...
```

# Workflow

## Step 1: Gather workload data
Use the `maui-workload-discovery` skill to fetch live data from NuGet for the target .NET versions. Typically include the **two most recent major .NET versions** (e.g., .NET 10 and .NET 9).

Required data per .NET version:
- Workload set package ID and versions (NuGet + CLI format)
- Individual workload versions (MAUI, iOS, Mac Catalyst, Android, tvOS, macOS)
- MAUI NuGet package versions:
  - **Implicit version**: The version bundled with the MAUI workload (from `microsoft.net.sdk.maui` manifest)
  - **Latest version**: The newest version available on NuGet.org (may be higher due to out-of-band releases)
- Apple platform dependencies (Xcode version range, recommended version, SDK version)
- Android dependencies (JDK version range, recommended version, SDK packages)
- Manifest package IDs used as data sources

## Step 2: Check for version changes
Before creating new release notes, check if versions have changed:

1. **Find the most recent dated release notes file** in `release-notes/` matching pattern `maui-release-notes-YYYYMMDD.md`
2. **Extract versions** from the most recent file (workload set version, MAUI version, iOS version, Android version)
3. **Compare with newly fetched data** from Step 1
4. **If any version has changed**, proceed to create a new dated release notes file
5. **If no changes**, inform the user that versions are up to date

### Version Change Detection Algorithm
```
function hasVersionChanges(newData, mostRecentReleaseNotes):
    // Key versions to compare (for each .NET version):
    versionsToCompare = [
        "workloadSetVersion",    // e.g., 10.102.0
        "mauiVersion",           // e.g., 10.0.1
        "iosVersion",            // e.g., 26.2.10191
        "androidVersion"         // e.g., 36.1.12
    ]
    
    for each dotNetVersion in newData:
        for each versionKey in versionsToCompare:
            if newData[versionKey] != mostRecentReleaseNotes[versionKey]:
                return true
    
    return false
```

## Step 3: Generate dated release notes file
If versions have changed (or no previous release notes exist), create a new dated file:

```
release-notes/maui-release-notes-{YYYYMMDD}.md
```

Where `{YYYYMMDD}` is the current date (e.g., `20260119`).

## Step 4: Update the index page
After creating a new dated release notes file, update the index page at:

```
release-notes/maui-release-notes.md
```

Add the new release entry at the **top** of the releases list (most recent first).

# Index Page Template

The index page (`release-notes/maui-release-notes.md`) provides an overview of all releases with detailed version summaries.

```markdown
# .NET MAUI Workload Release Notes

> **Last Updated:** {current_date}

This page lists all .NET MAUI workload release notes. Each entry links to detailed release notes with full dependency information and installation instructions.

---

## Releases

### {MMMM D, YYYY}

📄 [Full Release Notes](maui-release-notes-{YYYYMMDD}.md)

#### .NET {major} (only include if this version was updated)

**Workload Set:** `{workload_set_version}` (CLI: `{cli_version}`)

| Workload | Version | Requirements |
|----------|---------|--------------|
| MAUI | {maui_version} | |
| iOS | {ios_version} | Xcode ≥ {xcode_version} |
| Mac Catalyst | {maccatalyst_version} | Xcode ≥ {xcode_version} |
| tvOS | {tvos_version} | Xcode ≥ {xcode_version} |
| macOS | {macos_version} | Xcode ≥ {xcode_version} |
| Android | {android_version} | API {android_api}, JDK {jdk_version} |

| MAUI NuGet Packages | Implicit | Latest |
|---------------------|----------|--------|
| Microsoft.Maui.Controls | {implicit_version} | {latest_version} |

---

### {Previous Date}
...
```

### Index Entry Format
Each release entry in the index should include:

1. **Date heading** - The date of the release (e.g., `### January 19, 2026`)
2. **Link to full notes** - Relative link to the dated release notes file (at top for quick access)
3. **Per .NET version section** - Only include .NET versions that had updates in this release
   - Workload set version (NuGet and CLI format)
   - Workload versions table with Requirements column:
     - MAUI, iOS, Mac Catalyst, tvOS, macOS, Android versions
     - Requirements: Xcode version for Apple platforms, Android API + JDK for Android
   - MAUI NuGet packages (implicit workload version vs latest out-of-band version)

### Requirements Column
The Requirements column provides at-a-glance info for common developer needs:
- **Apple platforms (iOS, Mac Catalyst, tvOS, macOS):** `Xcode ≥ {version}` - the minimum Xcode version required
- **Android:** `API {level}, JDK {version}` - target API level and JDK version
- **MAUI:** Leave empty (no special requirements beyond the platform workloads)

### Conditional .NET Version Sections
Only include a .NET version section if that version had updates:
- If both .NET 10 and .NET 9 updated: Include both sections
- If only .NET 10 updated: Only include .NET 10 section
- If only .NET 9 updated: Only include .NET 9 section

This keeps the index focused on what actually changed in each release.

### Changes Detection Per .NET Version
When comparing versions, track changes per .NET version separately:
- Compare .NET 10 current vs .NET 10 previous
- Compare .NET 9 current vs .NET 9 previous
- Only generate section for versions with actual changes

# Dated Release Notes Template

Each dated release notes file (`release-notes/maui-release-notes-YYYYMMDD.md`) contains the full detailed release information.

## Header Section
```markdown
# .NET MAUI Workload Release Notes - {Month Day, Year}

> **Date:** {current_date}  
> **Source:** NuGet.org workload manifests (live data)

This document provides version information for .NET MAUI and related platform workloads across the two most recent major .NET versions.

⬅️ [Back to Release Notes Index](maui-release-notes.md)

---
```

## Per-.NET Version Section
For each .NET version (start with the newest), create a section with this structure:

### Version Header
```markdown
# .NET {major}

**Workload Set:** [Microsoft.NET.Workloads.{major}.0.{band}](https://www.nuget.org/packages/Microsoft.NET.Workloads.{major}.0.{band}/{nuget_version}) version `{nuget_version}`
```

### MAUI NuGet Packages
```markdown
## MAUI NuGet Packages

The following NuGet packages are the core .NET MAUI libraries. The **Implicit Version** is bundled with the workload, while **Latest Version** may be newer due to out-of-band releases.

| Package | Implicit Version | Latest Version | Release Notes |
|---------|------------------|----------------|---------------|
| Microsoft.Maui.Controls | [{workload_version}](https://www.nuget.org/packages/Microsoft.Maui.Controls/{workload_version}) | [{latest_version}](https://www.nuget.org/packages/Microsoft.Maui.Controls/{latest_version}) | [GitHub](https://github.com/dotnet/maui/releases/tag/{latest_version}) |
| Microsoft.Maui.Controls.Compatibility | [{workload_version}](https://www.nuget.org/packages/Microsoft.Maui.Controls.Compatibility/{workload_version}) | [{latest_version}](https://www.nuget.org/packages/Microsoft.Maui.Controls.Compatibility/{latest_version}) | |
| Microsoft.Maui.Essentials | [{workload_version}](https://www.nuget.org/packages/Microsoft.Maui.Essentials/{workload_version}) | [{latest_version}](https://www.nuget.org/packages/Microsoft.Maui.Essentials/{latest_version}) | |
| Microsoft.Maui.Graphics | [{workload_version}](https://www.nuget.org/packages/Microsoft.Maui.Graphics/{workload_version}) | [{latest_version}](https://www.nuget.org/packages/Microsoft.Maui.Graphics/{latest_version}) | |
| Microsoft.Maui.Maps | [{workload_version}](https://www.nuget.org/packages/Microsoft.Maui.Maps/{workload_version}) | [{latest_version}](https://www.nuget.org/packages/Microsoft.Maui.Maps/{latest_version}) | |
```

Note: 
- **Implicit Version**: The version bundled with the workload, used by default when no explicit `PackageReference` is specified. This comes from the MAUI workload manifest (`microsoft.net.sdk.maui` version).
- **Latest Version**: The newest version available on NuGet.org for this .NET major version. May include additional bug fixes and features released out-of-band.
- To use a newer version than the implicit workload version, add an explicit PackageReference to your project file.

### Workload Versions Table
```markdown
## Workload Versions

| Workload | Full ID | Version | SDK Band | Links |
|----------|---------|---------|----------|-------|
| **MAUI** | Microsoft.NET.Sdk.Maui | {version} | {band} | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.Maui.Manifest-{band}/{version}) · [Release](https://github.com/dotnet/maui/releases/tag/{version}) |
| **iOS** | Microsoft.NET.Sdk.iOS | {version} | {band} | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.iOS.Manifest-{band}/{version}) · [Release](https://github.com/dotnet/macios/releases/tag/{apple_release_tag}) |
| **Mac Catalyst** | Microsoft.NET.Sdk.MacCatalyst | {version} | {band} | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.MacCatalyst.Manifest-{band}/{version}) · [Release](https://github.com/dotnet/macios/releases/tag/{apple_release_tag}) |
| **Android** | Microsoft.NET.Sdk.Android | {version} | {band} | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.Android.Manifest-{band}/{version}) · [Release](https://github.com/dotnet/android/releases/tag/{version}) |
| **tvOS** | Microsoft.NET.Sdk.tvOS | {version} | {band} | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.tvOS.Manifest-{band}/{version}) · [Release](https://github.com/dotnet/macios/releases/tag/{apple_release_tag}) |
| **macOS** | Microsoft.NET.Sdk.macOS | {version} | {band} | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.macOS.Manifest-{band}/{version}) · [Release](https://github.com/dotnet/macios/releases/tag/{apple_release_tag}) |
```

### Installation Command
```markdown
## Installation

\`\`\`bash
# Update existing workloads to this version
dotnet workload update --version {cli_version}

# Or install specific workloads
dotnet workload install maui ios maccatalyst android --version {cli_version}
\`\`\`
```

### Apple Platform Dependencies
```markdown
## Apple Platform Dependencies (iOS, Mac Catalyst, tvOS, macOS)

Apple platform workloads require Xcode to be installed.

| Workload | Xcode Requirement | Recommended Xcode | Apple SDK |
|----------|-------------------|-------------------|-----------|
| iOS | ≥ {min_version} | {recommended} | {sdk_version} |
| Mac Catalyst | ≥ {min_version} | {recommended} | {sdk_version} |
| tvOS | ≥ {min_version} | {recommended} | {sdk_version} |
| macOS | ≥ {min_version} | {recommended} | {sdk_version} |
```

### Android Dependencies
```markdown
## Android Dependencies

| Dependency | Requirement | Recommended |
|------------|-------------|-------------|
| **JDK** | ≥ {min} and < {max} | {recommended} |

### Required Android SDK Packages

| Package | Description |
|---------|-------------|
| `build-tools;{version}` | Android SDK Build-Tools {major} |
| `cmdline-tools;{version}` | Android SDK Command-line Tools |
| `platforms;android-{api}` | Android SDK Platform {api} |
| `platform-tools` | Android SDK Platform-Tools (recommended: {version}) |

### Optional Android SDK Packages

| Package | Description |
|---------|-------------|
| `emulator` | Android Emulator (recommended: {version}) |
| `ndk-bundle` | NDK (recommended: {version}) |
| `platforms;android-{preview_api}` | Android SDK Platform {preview_api} (Preview) |
| System Images | Google APIs ARM 64 v8a / x86_64 for android-{api} |
```

### Windows Dependencies
```markdown
## MAUI Windows Dependencies

| Dependency | Minimum Version | Recommended |
|------------|-----------------|-------------|
| **Windows App SDK** | ≥ {version} | {version} |
| **Windows SDK Build Tools** | ≥ {version} | {version} |
| **Win2D** | ≥ {version} | {version} |
| **WebView2** | ≥ {version} | {version} |
```

Note: Windows dependencies are found in the MAUI workload manifest's `WorkloadDependencies.json`.

### Appium Testing Dependencies (Optional)
```markdown
## Appium Testing Dependencies (Optional)

| Component | Minimum Version | Recommended |
|-----------|-----------------|-------------|
| **Appium** | ≥ {version} | {version} |
| **Windows Driver** | ≥ {version} | {version} |
| **XCUITest Driver** | ≥ {version} | {version} |
| **Mac2 Driver** | ≥ {version} | {version} |
| **UIAutomator2 Driver** | ≥ {version} | {version} |
```

Note: Appium dependencies may be found in MAUI manifest or require separate lookup.

### Data Sources
```markdown
## Data Sources

- [Microsoft.NET.Workloads.{major}.0.{band}](https://www.nuget.org/packages/Microsoft.NET.Workloads.{major}.0.{band}/{version}) version `{version}`
- [Microsoft.NET.Sdk.Maui.Manifest-{band}](https://www.nuget.org/packages/Microsoft.NET.Sdk.Maui.Manifest-{band}/{version}) version `{version}`
- [Microsoft.NET.Sdk.iOS.Manifest-{band}](https://www.nuget.org/packages/Microsoft.NET.Sdk.iOS.Manifest-{band}/{version}) version `{version}`
- [Microsoft.NET.Sdk.Android.Manifest-{band}](https://www.nuget.org/packages/Microsoft.NET.Sdk.Android.Manifest-{band}/{version}) version `{version}`
```

## Reference Section (End of Document)
```markdown
---

# Reference

## Version Notation

| Notation | Meaning |
|----------|---------|
| `[17.0,22.0)` | ≥ 17.0 AND < 22.0 |
| `[26.2,)` | ≥ 26.2 (no upper bound) |
| `[1.7.250909003,)` | ≥ 1.7.250909003 (no upper bound) |

For more information, see the [.NET Workload Sets documentation](https://learn.microsoft.com/dotnet/core/tools/dotnet-workload-sets).

## Platform GitHub Repositories

| Platform | Repository | Releases |
|----------|------------|----------|
| MAUI | [dotnet/maui](https://github.com/dotnet/maui) | [Releases](https://github.com/dotnet/maui/releases) |
| iOS, Mac Catalyst, tvOS, macOS | [dotnet/macios](https://github.com/dotnet/macios) | [Releases](https://github.com/dotnet/macios/releases) |
| Android | [dotnet/android](https://github.com/dotnet/android) | [Releases](https://github.com/dotnet/android/releases) |
```

# Link Construction Guide

## NuGet Package Links

### Workload Set Package
```
https://www.nuget.org/packages/Microsoft.NET.Workloads.{major}.0.{band}/{nuget_version}
```
Example: `https://www.nuget.org/packages/Microsoft.NET.Workloads.10.0.100/10.102.0`

### Workload Manifest Packages
```
https://www.nuget.org/packages/Microsoft.NET.Sdk.{Workload}.Manifest-{band}/{version}
```
Examples:
- `https://www.nuget.org/packages/Microsoft.NET.Sdk.Maui.Manifest-10.0.100/10.0.1`
- `https://www.nuget.org/packages/Microsoft.NET.Sdk.iOS.Manifest-10.0.100/26.2.10191`
- `https://www.nuget.org/packages/Microsoft.NET.Sdk.Android.Manifest-10.0.100/36.1.12`

### MAUI NuGet Packages
```
https://www.nuget.org/packages/{PackageName}/{version}
```
Example: `https://www.nuget.org/packages/Microsoft.Maui.Controls/10.0.30`

## GitHub Release Links

### MAUI Releases
Tag format: Version number directly (e.g., `10.0.30`, `9.0.120`)
```
https://github.com/dotnet/maui/releases/tag/{version}
```
Example: `https://github.com/dotnet/maui/releases/tag/10.0.30`

### Android Releases
Tag format: Version number directly (e.g., `36.1.12`, `35.0.105`)
```
https://github.com/dotnet/android/releases/tag/{version}
```
Example: `https://github.com/dotnet/android/releases/tag/36.1.12`

### Apple Platform Releases (iOS, Mac Catalyst, tvOS, macOS)
Tag format: `dotnet-{dotnetVersion}.0.1xx-xcode{xcodeVersion}-{buildNumber}`

The Apple workload versions follow pattern: `{xcodeVersion}.{buildNumber}` (e.g., `26.2.10191`)
- Xcode version: First two parts (e.g., `26.2`)
- Build number: Last part (e.g., `10191`)

To construct the release tag:
1. Extract Xcode version from workload version (e.g., `26.2` from `26.2.10191`)
2. Extract build number (e.g., `10191` from `26.2.10191`)
3. Determine .NET version (e.g., `10` for .NET 10, `9` for .NET 9)
4. Build tag: `dotnet-{dotnetVersion}.0.1xx-xcode{xcodeVersion}-{buildNumber}`

```
https://github.com/dotnet/macios/releases/tag/dotnet-{dotnetVersion}.0.1xx-xcode{xcodeVersion}-{buildNumber}
```

Examples:
- iOS version `26.2.10191` on .NET 10 → `https://github.com/dotnet/macios/releases/tag/dotnet-10.0.1xx-xcode26.2-10191`
- iOS version `26.0.9783` on .NET 9 → `https://github.com/dotnet/macios/releases/tag/dotnet-9.0.1xx-xcode26.0-9783`

### Apple Release Tag Algorithm
```
function getAppleReleaseTag(workloadVersion, dotnetMajorVersion):
    parts = workloadVersion.split('.')
    xcodeVersion = parts[0] + '.' + parts[1]  // e.g., "26.2"
    buildNumber = parts[2]                      // e.g., "10191"
    return "dotnet-" + dotnetMajorVersion + ".0.1xx-xcode" + xcodeVersion + "-" + buildNumber
```

# Formatting Rules

## Version Range Conversion
Convert NuGet interval notation to human-readable format:
| NuGet Notation | Display Format |
|----------------|----------------|
| `[17.0,22.0)` | `≥ 17.0 and < 22.0` |
| `[26.2,)` | `≥ 26.2` |
| `[1.0,)` | `≥ 1.0` |

## Table Alignment
- Use consistent column widths
- Bold workload/component names in the first column
- Use backticks for package names and version numbers in inline contexts
- Use `≥` symbol (not `>=`) for version requirements

## Section Separators
- Use `---` horizontal rules between major .NET version sections
- Add blank lines before and after tables for readability

## Date Format
Use format: `Month Day, Year` (e.g., `January 19, 2026`)

# Update Workflow

When generating or updating release notes:

## New Release Detected (versions changed)

1. **Fetch latest workload data** using `maui-workload-discovery` skill
2. **Compare with most recent release** (find latest `maui-release-notes-YYYYMMDD.md`)
3. **If versions changed**:
   - Create new dated file: `release-notes/maui-release-notes-{YYYYMMDD}.md`
   - Generate complete release notes using the dated template
   - Update `release-notes/maui-release-notes.md` index:
     - Add new entry at the **top** of the Releases section
     - Update the "Last Updated" date
4. **If no changes**: Inform user that versions are current

## Finding the Most Recent Release Notes

```bash
# List dated release notes files, sorted by date (newest first)
ls -1 release-notes/maui-release-notes-*.md | sort -r | head -1
```

Or programmatically:
1. List all files matching `release-notes/maui-release-notes-YYYYMMDD.md`
2. Extract the date portion (YYYYMMDD) from each filename
3. Sort by date descending
4. The first file is the most recent

## Version Comparison

Extract these key versions from the most recent release notes for comparison:
- Workload set version (from `**Workload Set:**` line)
- MAUI workload version (from Workload Versions table)
- iOS workload version (from Workload Versions table)
- Android workload version (from Workload Versions table)

Compare with newly fetched data. Any difference triggers a new release.

# Inputs

| Parameter | Required | Example | Notes |
|-----------|----------|---------|-------|
| dotnetVersions | no | ["10.0", "9.0"] | Default: two most recent stable versions |
| includePrerelease | no | false | Whether to include preview workloads |

# Output

When versions have changed:
1. **New dated release notes file**: `release-notes/maui-release-notes-{YYYYMMDD}.md`
2. **Updated index page**: `release-notes/maui-release-notes.md` with new entry at top

When versions are current:
- Informational message that no updates are needed

# Dependencies
This skill requires data from the `maui-workload-discovery` skill. Always use live NuGet data rather than cached or hardcoded versions.

# Example Usage

## Check for updates and generate release notes
1. Use `maui-workload-discovery` to fetch current data for .NET 10 and .NET 9
2. Find the most recent `maui-release-notes-YYYYMMDD.md` file
3. Compare versions from Step 1 with versions in the most recent file
4. If any version changed:
   - Create `release-notes/maui-release-notes-20260119.md` with full release details
   - Add entry to top of `release-notes/maui-release-notes.md` with version summary
5. If no changes, report "Workload versions are up to date"

## First-time setup (no existing release notes)
1. Use `maui-workload-discovery` to fetch current data
2. Create `release-notes/maui-release-notes-{YYYYMMDD}.md` with full details
3. Create `release-notes/maui-release-notes.md` index page with initial entry

## Comparing versions example
```
Previous (from maui-release-notes-20260115.md):
  .NET 10: workload-set=10.101.0, maui=10.0.0, ios=26.1.10100, android=36.1.10

Current (from NuGet):
  .NET 10: workload-set=10.102.0, maui=10.0.1, ios=26.2.10191, android=36.1.12

Result: Versions changed! Create maui-release-notes-20260119.md
Changes: "Workload set updated to 10.102.0. MAUI 10.0.1, iOS 26.2.10191, Android 36.1.12."
```

# Reference
- Index page: [release-notes/maui-release-notes.md](../../../release-notes/maui-release-notes.md)
- Data source skill: [maui-workload-discovery](../maui-workload-discovery/SKILL.md)
- Background: [docs/workload-discovery-process.md](../../../docs/workload-discovery-process.md)
