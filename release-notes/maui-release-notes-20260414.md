# .NET MAUI Workload Release Notes - April 14, 2026

> **Date:** April 14, 2026  
> **Source:** NuGet feeds queried at generation time (`dotnet-workloads` Azure DevOps feed; package links target NuGet.org)

This document provides version information for .NET MAUI and related platform workloads for this release.

⬅️ [Back to Release Notes Index](maui-release-notes.md)

---

# .NET 11 (Preview 3)

## Workloads

**Workload Set:** [Microsoft.NET.Workloads.11.0.100-preview.3 @ 11.0.100-preview.3.26213.1](https://www.nuget.org/packages/Microsoft.NET.Workloads.11.0.100-preview.3/11.100.0-preview.3.26213.1)

The Preview 3 workload set and the individual Preview 3 manifest versions below were discovered from the public `dotnet-workloads` Azure DevOps feed ahead of NuGet.org publication. Official .NET 11 release metadata still reported `11.0.100-preview.2.26159.112` as the latest SDK at the time of writing.

## Installation

```bash
dotnet workload update --version 11.0.100-preview.3.26213.1 \
  --source https://pkgs.dev.azure.com/dnceng/public/_packaging/dotnet-workloads/nuget/v3/index.json
# Or install specific workloads
dotnet workload install maui ios maccatalyst android --version 11.0.100-preview.3.26213.1 \
  --source https://pkgs.dev.azure.com/dnceng/public/_packaging/dotnet-workloads/nuget/v3/index.json
```

### Recommended Tools:
- Xcode: 26.3
- Java JDK: 21.0.8
- Android API-36

<details>
<summary><h3>Workload Versions</h3></summary>

| Workload | Full ID | Version | SDK Band | Links |
|----------|---------|---------|----------|-------|
| **MAUI** | Microsoft.NET.Sdk.Maui | 11.0.0-preview.3.26203.7 | 11.0.100-preview.3 | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.Maui.Manifest-11.0.100-preview.3/11.0.0-preview.3.26203.7) · [Release](https://github.com/dotnet/maui/releases) |
| **iOS** | Microsoft.NET.Sdk.iOS | 26.2.11588-net11-p3 | 11.0.100-preview.3 | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.iOS.Manifest-11.0.100-preview.3/26.2.11588-net11-p3) · [Release](https://github.com/dotnet/macios/releases/tag/dotnet-11.0.1xx-preview3-11588) |
| **Mac Catalyst** | Microsoft.NET.Sdk.MacCatalyst | 26.2.11588-net11-p3 | 11.0.100-preview.3 | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.MacCatalyst.Manifest-11.0.100-preview.3/26.2.11588-net11-p3) · [Release](https://github.com/dotnet/macios/releases/tag/dotnet-11.0.1xx-preview3-11588) |
| **Android** | Microsoft.NET.Sdk.Android | 36.99.0-preview.3.10 | 11.0.100-preview.3 | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.Android.Manifest-11.0.100-preview.3/36.99.0-preview.3.10) · [Release](https://github.com/dotnet/android/releases/tag/36.99.0-preview.3.10) |
| **tvOS** | Microsoft.NET.Sdk.tvOS | 26.2.11588-net11-p3 | 11.0.100-preview.3 | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.tvOS.Manifest-11.0.100-preview.3/26.2.11588-net11-p3) · [Release](https://github.com/dotnet/macios/releases/tag/dotnet-11.0.1xx-preview3-11588) |
| **macOS** | Microsoft.NET.Sdk.macOS | 26.2.11588-net11-p3 | 11.0.100-preview.3 | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.macOS.Manifest-11.0.100-preview.3/26.2.11588-net11-p3) · [Release](https://github.com/dotnet/macios/releases/tag/dotnet-11.0.1xx-preview3-11588) |

</details>

<details>
<summary><h3>MAUI NuGet Packages</h3></summary>

The following NuGet packages are the core .NET MAUI libraries. The **Implicit Version** is bundled with the workload, while **Latest Version** may be newer due to out-of-band releases.

| Package | Implicit Version | Latest Version |
|---------|------------------|----------------|
| **Microsoft.Maui.Controls** | [11.0.0-preview.3.26203.7](https://www.nuget.org/packages/Microsoft.Maui.Controls/11.0.0-preview.3.26203.7) | [11.0.0-preview.3.26203.7](https://www.nuget.org/packages/Microsoft.Maui.Controls/11.0.0-preview.3.26203.7) |
| **Microsoft.Maui.Controls.Compatibility** | [11.0.0-preview.3.26203.7](https://www.nuget.org/packages/Microsoft.Maui.Controls.Compatibility/11.0.0-preview.3.26203.7) | [11.0.0-preview.3.26203.7](https://www.nuget.org/packages/Microsoft.Maui.Controls.Compatibility/11.0.0-preview.3.26203.7) |
| **Microsoft.Maui.Essentials** | [11.0.0-preview.3.26203.7](https://www.nuget.org/packages/Microsoft.Maui.Essentials/11.0.0-preview.3.26203.7) | [11.0.0-preview.3.26203.7](https://www.nuget.org/packages/Microsoft.Maui.Essentials/11.0.0-preview.3.26203.7) |
| **Microsoft.Maui.Graphics** | [11.0.0-preview.3.26203.7](https://www.nuget.org/packages/Microsoft.Maui.Graphics/11.0.0-preview.3.26203.7) | [11.0.0-preview.3.26203.7](https://www.nuget.org/packages/Microsoft.Maui.Graphics/11.0.0-preview.3.26203.7) |
| **Microsoft.Maui.Maps** | [11.0.0-preview.3.26203.7](https://www.nuget.org/packages/Microsoft.Maui.Maps/11.0.0-preview.3.26203.7) | [11.0.0-preview.3.26203.7](https://www.nuget.org/packages/Microsoft.Maui.Maps/11.0.0-preview.3.26203.7) |

</details>

<details>
<summary><h3>Native Tool & SDK Compatibility</h3></summary>

#### Apple (iOS, Mac Catalyst, tvOS, macOS)

| Tool | Min Version | Recommended Version |
|------|-------------|---------------------|
| **Xcode** | ≥ 26.3 | 26.3 |

#### Java JDK (Android)

| Tool | Min / Required Version | Recommended Version |
|------|-------------------------|---------------------|
| **Java JDK** | ≥ 21.0 and < 22.0 | 21.0.8 |

#### Android SDK Packages (Required)

| SDK Package | Description |
|-------------|-------------|
| **`build-tools;36.0.0`** | Android SDK Build-Tools 36 |
| **`cmdline-tools;19.0`** | Android SDK Command-line Tools |
| **`platforms;android-36`** | Android SDK Platform 36 |
| **`platform-tools`** | Android SDK Platform-Tools 36.0.0 |

#### Android SDK Packages (Optional)

| Package | Description |
|---------|-------------|
| `emulator` | Android Emulator |
| `ndk-bundle` | NDK |
| `platforms;android-37` | Android SDK Platform (Preview) |
| System Images | Google APIs ARM 64 v8a / x86_64 |

#### MAUI Windows Dependencies

| Dependency | Minimum Version | Recommended |
|------------|-----------------|-------------|
| **Windows App SDK** | ≥ 1.8.251106002 | 1.8.251106002 |
| **Windows SDK Build Tools** | ≥ 10.0.26100.4654 | 10.0.26100.4654 |
| **Win2D** | ≥ 1.3.2 | 1.3.2 |
| **WebView2** | ≥ 1.0.3179.45 | 1.0.3179.45 |

</details>

---

# Reference

## Version Notation

| Notation | Meaning |
|----------|---------|
| `[21.0,22.0)` | ≥ 21.0 AND < 22.0 |
| `[26.3,)` | ≥ 26.3 (no upper bound) |

For more information, see the [.NET Workload Sets documentation](https://learn.microsoft.com/dotnet/core/tools/dotnet-workload-sets).

## Platform GitHub Repositories

| Platform | Repository | Releases |
|----------|------------|----------|
| MAUI | [dotnet/maui](https://github.com/dotnet/maui) | [Releases](https://github.com/dotnet/maui/releases) |
| iOS, Mac Catalyst, tvOS, macOS | [dotnet/macios](https://github.com/dotnet/macios) | [Releases](https://github.com/dotnet/macios/releases) |
| Android | [dotnet/android](https://github.com/dotnet/android) | [Releases](https://github.com/dotnet/android/releases) |

> NOTE: macios releases may not use exact versions in their name/tag. For Preview 3, the closest matching release tag is `dotnet-11.0.1xx-preview3-11588`.
